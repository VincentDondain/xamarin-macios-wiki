#MediaPlayer.framework

``` diff
diff -ruN /Applications/Xcode8-GM.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPError.h /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPError.h
--- /Applications/Xcode8-GM.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPError.h	2016-08-12 08:47:13.000000000 +0200
+++ /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPError.h	2016-09-15 02:06:22.000000000 +0200
@@ -20,6 +20,7 @@
     MPErrorNetworkConnectionFailed,                 // the device could not connect to the network
     MPErrorNotFound,                                // the id could not be found in the current storefront
     MPErrorNotSupported,                            // the request is not supported (ex: trying to add items to a smart playlist)
+    MPErrorCancelled NS_ENUM_AVAILABLE_IOS(10_1),   // the request was cancelled before it could complete
 } NS_ENUM_AVAILABLE_IOS(9_3);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-GM.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMusicPlayerController.h /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMusicPlayerController.h
--- /Applications/Xcode8-GM.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMusicPlayerController.h	2016-05-04 00:21:21.000000000 +0200
+++ /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMusicPlayerController.h	2016-09-15 02:06:22.000000000 +0200
@@ -11,11 +11,10 @@
 #import <MediaPlayer/MPMediaItem.h>
 #import <MediaPlayer/MPMediaQuery.h>
 #import <MediaPlayer/MPMediaPlayback.h>
+#import <MediaPlayer/MPMusicPlayerQueueDescriptor.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
-@class MPMediaItem, MPMediaQuery, MPMusicPlayerControllerInternal;
-
 typedef NS_ENUM(NSInteger, MPMusicPlaybackState) {
     MPMusicPlaybackStateStopped,
     MPMusicPlaybackStatePlaying,
@@ -83,6 +82,13 @@
 - (void)setQueueWithQuery:(MPMediaQuery *)query;
 - (void)setQueueWithItemCollection:(MPMediaItemCollection *)itemCollection;
 - (void)setQueueWithStoreIDs:(NSArray<NSString *> *)storeIDs NS_AVAILABLE_IOS(9_3);
+- (void)setQueueWithDescriptor:(MPMusicPlayerQueueDescriptor *)descriptor NS_AVAILABLE_IOS(10_1);
+
+// The completion handler will be called when the first item from the queue is buffered and ready to play.
+// If a first item has been specified using MPMusicPlayerQueueDescriptor, the error will be non-nil if the specified item cannot be prepared for playback.
+// If a first item is not specified, the error will be non-nil if an item cannot be prepared for playback.
+// Errors will be in MPErrorDomain.
+- (void)prepareToPlayWithCompletionHandler:(void (^)(NSError *_Nullable error))completionHandler NS_AVAILABLE_IOS(10_1);
 
 // Skips to the next item in the queue. If already at the last item, this will end playback.
 - (void)skipToNextItem;
diff -ruN /Applications/Xcode8-GM.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMusicPlayerQueueDescriptor.h /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMusicPlayerQueueDescriptor.h
--- /Applications/Xcode8-GM.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMusicPlayerQueueDescriptor.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMusicPlayerQueueDescriptor.h	2016-09-15 02:06:22.000000000 +0200
@@ -0,0 +1,51 @@
+//
+//  MPMusicPlayerQueueDescriptor.h
+//  MediaPlayerFramework
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <MediaPlayer/MediaPlayerDefines.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class MPMediaItem, MPMediaItemCollection, MPMediaQuery;
+
+MP_EXTERN_CLASS_AVAILABLE(10_1)
+__TVOS_PROHIBITED
+@interface MPMusicPlayerQueueDescriptor : NSObject<NSSecureCoding>
+
+@end
+
+MP_EXTERN_CLASS_AVAILABLE(10_1)
+__TVOS_PROHIBITED
+@interface MPMusicPlayerMediaItemQueueDescriptor : MPMusicPlayerQueueDescriptor
+
+- (instancetype)initWithQuery:(MPMediaQuery *)query;
+- (instancetype)initWithItemCollection:(MPMediaItemCollection *)itemCollection;
+
+@property (nonatomic, copy, readonly) MPMediaQuery *query;
+@property (nonatomic, strong, readonly) MPMediaItemCollection *itemCollection;
+@property (nonatomic, strong, nullable) MPMediaItem *startItem;
+
+- (void)setStartTime:(NSTimeInterval)startTime forItem:(MPMediaItem *)mediaItem;
+- (void)setEndTime:(NSTimeInterval)endTime forItem:(MPMediaItem *)mediaItem;
+
+@end
+
+MP_EXTERN_CLASS_AVAILABLE(10_1)
+__TVOS_PROHIBITED
+@interface MPMusicPlayerStoreQueueDescriptor : MPMusicPlayerQueueDescriptor
+
+- (instancetype)initWithStoreIDs:(NSArray<NSString *> *)storeIDs;
+
+@property (nonatomic, copy, nullable) NSArray<NSString *> *storeIDs;
+@property (nonatomic, copy, nullable) NSString *startItemID;
+
+- (void)setStartTime:(NSTimeInterval)startTime forItemWithStoreID:(NSString *)storeID;
+- (void)setEndTime:(NSTimeInterval)endTime forItemWithStoreID:(NSString *)storeID;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-GM.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayer.h /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayer.h
--- /Applications/Xcode8-GM.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayer.h	2016-08-12 08:47:13.000000000 +0200
+++ /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayer.h	2016-09-15 02:06:22.000000000 +0200
@@ -18,6 +18,7 @@
 #import <MediaPlayer/MPMoviePlayerController.h>
 #import <MediaPlayer/MPMoviePlayerViewController.h>
 #import <MediaPlayer/MPMusicPlayerController.h>
+#import <MediaPlayer/MPMusicPlayerQueueDescriptor.h>
 #import <MediaPlayer/MPNowPlayingInfoCenter.h>
 #import <MediaPlayer/MPNowPlayingInfoLanguageOption.h>
 #import <MediaPlayer/MPPlayableContentDataSource.h>

```