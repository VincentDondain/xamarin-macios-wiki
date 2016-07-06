#MediaPlayer.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPContentItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPContentItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPContentItem.h	2016-02-27 05:48:04.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPContentItem.h	2016-05-28 06:47:30.000000000 +0200
@@ -38,22 +38,22 @@
 /// cover for a song, or a movie poster for a movie.
 @property (nonatomic, strong, nullable) MPMediaItemArtwork *artwork;
 
-/// Represents whether the content item is a container of other content items.
-/// An example of a container content item might be an album, which contains
-/// multiple songs.
-@property (nonatomic, assign, getter = isContainer) BOOL container;
-
-/// Represents whether this content item is playable or not. A content item can
-/// be both a container, and playable. For example, a container item like a
-/// playlist might be set as playable if the app would like to provide the
-/// option of playing the playlist's tracks in order when selected.
-@property (nonatomic, assign, getter = isPlayable) BOOL playable;
-
 /// Represents the current playback progress of the item.
 /// 0.0 = not watched/listened/viewed, 1.0 = fully watched/listened/viewed
 /// Default is -1.0 (no progress indicator shown)
 @property (nonatomic, assign) float playbackProgress;
 
+/// Represents whether this content item is streaming content, i.e. from the cloud
+/// where the content is not stored locally.
+@property (nonatomic, assign, getter = isStreamingContent) BOOL streamingContent NS_AVAILABLE_IOS(10_0);
+
+/// Represents whether this content item is explicit content
+@property (nonatomic, assign, getter = isExplicitContent) BOOL explicitContent NS_AVAILABLE_IOS(10_0);
+
+@property (nonatomic, assign, getter = isContainer) BOOL container;
+
+@property (nonatomic, assign, getter = isPlayable) BOOL playable;
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaItem.h	2015-11-14 07:12:04.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaItem.h	2016-05-28 06:29:03.000000000 +0200
@@ -102,6 +102,9 @@
 MP_EXTERN NSString * const MPMediaItemPropertyArtwork;
 @property (nonatomic, readonly, nullable) MPMediaItemArtwork *artwork NS_AVAILABLE_IOS(7_0);
 
+MP_EXTERN NSString *const MPMediaItemPropertyIsExplicit NS_AVAILABLE_IOS(7_0);
+@property (nonatomic, readonly, getter = isExplicitItem) BOOL explicitItem NS_AVAILABLE_IOS(10_0);
+
 MP_EXTERN NSString * const MPMediaItemPropertyLyrics;
 @property (nonatomic, readonly, nullable) NSString *lyrics NS_AVAILABLE_IOS(8_0);
 
@@ -155,19 +158,18 @@
 //-----------------------------------------------------
 
 MP_EXTERN_CLASS_AVAILABLE(3_0)
-__TVOS_PROHIBITED
 @interface MPMediaItemArtwork : NSObject
 
-// Initializes an MPMediaItemArtwork instance with the given full-size image.
-// The crop rect of the image is assumed to be equal to the bounds of the 
-// image as defined by the image's size in points, i.e. tightly cropped.
-- (instancetype)initWithImage:(UIImage *)image NS_DESIGNATED_INITIALIZER NS_AVAILABLE_IOS(5_0);
+- (instancetype)initWithBoundsSize:(CGSize)boundsSize requestHandler:(UIImage *(^)(CGSize size))requestHandler NS_DESIGNATED_INITIALIZER NS_AVAILABLE_IOS(10_0);
 
 // Returns the artwork image for an item at a given size (in points).
 - (nullable UIImage *)imageWithSize:(CGSize)size;
 
 @property (nonatomic, readonly) CGRect bounds; // The bounds of the full size image (in points).
-@property (nonatomic, readonly) CGRect imageCropRect; // The actual content area of the artwork, in the bounds of the full size image (in points).
+
+@property (nonatomic, readonly) CGRect imageCropRect NS_DEPRECATED_IOS(3_0, 10_0);
+- (instancetype)initWithImage:(UIImage *)image NS_DEPRECATED_IOS(5_0, 10_0);
+- (id)init NS_UNAVAILABLE;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPNowPlayingInfoCenter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPNowPlayingInfoCenter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPNowPlayingInfoCenter.h	2015-09-30 23:40:10.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPNowPlayingInfoCenter.h	2016-05-28 06:47:29.000000000 +0200
@@ -35,6 +35,12 @@
 // In addition, metadata properties specific to the current playback session
 // may also be specified -- see "Additional metadata properties" below.
 
+typedef NS_ENUM(NSUInteger, MPNowPlayingInfoMediaType) {
+    MPNowPlayingInfoMediaTypeNone = 0,
+    MPNowPlayingInfoMediaTypeAudio,
+    MPNowPlayingInfoMediaTypeVideo,
+} NS_AVAILABLE_IOS(10_0);
+
 MP_EXTERN_CLASS_AVAILABLE(5_0)
 @interface MPNowPlayingInfoCenter : NSObject
 
@@ -85,6 +91,9 @@
 // The total number of chapters in the now playing item.
 MP_EXTERN NSString *const MPNowPlayingInfoPropertyChapterCount NS_AVAILABLE_IOS(5_0); // NSNumber (NSUInteger)
 
+// A boolean denoting whether the now playing item is a live stream.
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyIsLiveStream NS_AVAILABLE_IOS(10_0); // NSNumber (BOOL)
+
 // A list of available language option groups in the now playing item
 // Only one language option in a given group can be played at once.
 MP_EXTERN NSString *const MPNowPlayingInfoPropertyAvailableLanguageOptions NS_AVAILABLE_IOS(9_0); // NSArrayRef of MPNowPlayingInfoLanguageOptionGroup
@@ -92,5 +101,33 @@
 // A list of currently active language options in the now playing item.
 MP_EXTERN NSString *const MPNowPlayingInfoPropertyCurrentLanguageOptions NS_AVAILABLE_IOS(9_0); // NSArray of MPNowPlayingInfoLanguageOption
 
+// An identifier that represents the collection to which the now playing item belongs.
+// This can refer to an artist, album, playlist, etc.
+// This can be used to ask the now playing app to resume playback of the collection.
+MP_EXTERN NSString *const MPNowPlayingInfoCollectionIdentifier NS_AVAILABLE_IOS(9_3); // NSString
+
+// An opaque identifier that uniquely represents the now playing item,
+// even across app relaunches. This can be in any format and is only used to
+// reference this item back to the now playing app.
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyExternalContentIdentifier NS_AVAILABLE_IOS(10_0); // NSString
+
+// An optional opaque identifier that uniquely represents the profile that the
+// now playing item is being played from, even across app relauches.
+// This can be in any format and is only used to reference this profile back to
+// the now playing app.
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyExternalUserProfileIdentifier NS_AVAILABLE_IOS(10_0); // NSString
+
+// Represents the current playback progress of the now playing item.
+// 0.0 = not watched/listened/viewed, 1.0 = fully watched/listened/viewed
+// This value is different that ElapsedPlaybackTime and does not need to be exact
+// as it is used as a high level indicator as to how far along the user is.
+// For example, a movie may wish to set the now playing item as fully watched
+// when the credits begin to roll.
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyPlaybackProgress NS_AVAILABLE_IOS(10_0); // NSNumber (float)
+
+// Indicates the media type of the now playing item
+// This can be used to determine what kind of user interface the system displays.
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyMediaType NS_AVAILABLE_IOS(10_0); // NSNumber (MPNowPlayingInfoMediaType)
+
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentDataSource.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentDataSource.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentDataSource.h	2015-09-30 23:40:10.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentDataSource.h	2016-05-28 06:47:29.000000000 +0200
@@ -35,6 +35,14 @@
 /// not supported for any content items.
 - (BOOL)childItemsDisplayPlaybackProgressAtIndexPath:(NSIndexPath *)indexPath;
 
+/// Provides a content item for the provided identifier.
+/// Provide nil if there is no content item corresponding to the identifier.
+/// Provide an error if there is an error that will not allow content items
+/// to be retrieved.
+/// Client applications should always call the completion handler after loading
+/// has finished, if this method is implemented.
+- (void)contentItemForIdentifier:(NSString *)identifier completionHandler:(void(^)(MPContentItem *__nullable, NSError * __nullable))completionHandler NS_AVAILABLE_IOS(10_0);
+
 @required
 /// Returns the number of child nodes at the specified index path. In a virtual
 /// filesystem, this would be the number of files in a specific folder. An empty
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentDelegate.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentDelegate.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentDelegate.h	2015-09-30 23:40:10.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentDelegate.h	2016-05-28 06:47:29.000000000 +0200
@@ -26,14 +26,25 @@
 /// appropriate error if there was an error beginning playback for the item.
 - (void)playableContentManager:(MPPlayableContentManager *)contentManager initiatePlaybackOfContentItemAtIndexPath:(NSIndexPath *)indexPath completionHandler:(void(^)(NSError * __nullable))completionHandler NS_AVAILABLE_IOS(7_1);
 
+
+/// This method is called when a media player interface wants the now playing
+/// app to setup a playback queue for later playback. The application should
+/// load content into its play queue but not start playback until a Play command is
+/// received or if the playable content manager requests to play something else.
+/// The app should call the provided completion handler once it is ready to play
+/// something.
+- (void)playableContentManager:(MPPlayableContentManager *)contentManager initializePlaybackQueueWithCompletionHandler:(void(^)(NSError * __nullable))completionHandler NS_AVAILABLE_IOS(9_0) NS_DEPRECATED_IOS(9_0, 9_3, "Use initializePlaybackQueueWithContentItems:completionHandler: instead");
+
 /// This method is called when a media player interface wants the now playing
 /// app to setup a playback queue for later playback. The application should
-/// load content into its play queue and prepare it for playback, but not start
-/// playback until a Play command is received or if the playable content manager
-/// requests to play something else.
+/// load content into its play queue based on the provided content items and
+/// prepare it for playback, but not start playback until a Play command is
+/// received or if the playable content manager requests to play something else.
+/// A nil contentItems array means that the app should prepare its queue with
+/// anything it deems appropriate.
 /// The app should call the provided completion handler once it is ready to play
 /// something.
-- (void)playableContentManager:(MPPlayableContentManager *)contentManager initializePlaybackQueueWithCompletionHandler:(void(^)(NSError * __nullable))completionHandler NS_AVAILABLE_IOS(9_0);
+- (void)playableContentManager:(MPPlayableContentManager *)contentManager initializePlaybackQueueWithContentItems:(nullable NSArray *)contentItems completionHandler:(void(^)(NSError * __nullable))completionHandler NS_AVAILABLE_IOS(9_3);
 
 /// This method is called when the content server notifies the manager that the current context has changed.
 - (void)playableContentManager:(MPPlayableContentManager *)contentManager didUpdateContext:(MPPlayableContentManagerContext *)context NS_AVAILABLE_IOS(8_4);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentManager.h	2015-09-30 23:40:10.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentManager.h	2016-05-28 06:47:29.000000000 +0200
@@ -25,6 +25,9 @@
 @property (nonatomic, weak, nullable) id<MPPlayableContentDelegate>   delegate;
 @property (nonatomic, readonly) MPPlayableContentManagerContext *context NS_AVAILABLE_IOS(8_4);
 
+/// Tells the content manager which MPBrowsableContentItems are currently playing based on their identifiers.
+@property (nonatomic, strong) NSArray<NSString *> *nowPlayingIdentifiers NS_AVAILABLE_IOS(10_0);
+
 /// Returns the application's instance of the content manager.
 + (instancetype)sharedContentManager;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommand.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommand.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommand.h	2015-09-30 23:40:11.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommand.h	2016-05-28 06:47:29.000000000 +0200
@@ -7,6 +7,7 @@
 
 #import <Foundation/Foundation.h>
 #import <MediaPlayer/MediaPlayerDefines.h>
+#import <MediaPlayer/MPRemoteControlTypes.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -59,7 +60,7 @@
 @interface MPSkipIntervalCommand : MPRemoteCommand
 
 /// An array of NSNumbers (NSTimeIntervals) that contain preferred skip intervals.
-@property (nonatomic, copy) NSArray *preferredIntervals;
+@property (nonatomic, copy) NSArray<NSNumber *> *preferredIntervals;
 
 @end
 
@@ -101,9 +102,33 @@
 
 @end
 
+/// Command for changing the current playback position in a now playing item.
+/// Sends out MPChangePlaybackPositionCommandEvents.
 MP_EXTERN_CLASS_AVAILABLE(9_0)
 @interface MPChangePlaybackPositionCommand : MPRemoteCommand
 
 @end
 
+/// Command for changing the current shuffle mode to use during playback. To
+/// update the system's current representation of your app's shuffle mode, set
+/// the currentShuffleType property on this command to the proper shuffle type
+/// value.
+MP_EXTERN_CLASS_AVAILABLE(8_0)
+@interface MPChangeShuffleModeCommand : MPRemoteCommand
+
+@property (nonatomic, assign) MPShuffleType currentShuffleType;
+
+@end
+
+/// Command for changing the current repeat mode to use during playback. To
+/// update the system's current representation of your app's repeat mode, set
+/// the currentRepeatType property on this command to the proper repeat type
+/// value.
+MP_EXTERN_CLASS_AVAILABLE(8_0)
+@interface MPChangeRepeatModeCommand : MPRemoteCommand
+
+@property (nonatomic, assign) MPRepeatType currentRepeatType;
+
+@end
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandCenter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandCenter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandCenter.h	2015-09-30 23:40:10.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandCenter.h	2016-05-28 06:47:29.000000000 +0200
@@ -10,7 +10,14 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-@class MPRemoteCommand, MPSkipIntervalCommand, MPRatingCommand, MPChangePlaybackRateCommand, MPFeedbackCommand, MPChangePlaybackPositionCommand;
+@class MPChangePlaybackPositionCommand;
+@class MPChangePlaybackRateCommand;
+@class MPChangeRepeatModeCommand;
+@class MPChangeShuffleModeCommand;
+@class MPFeedbackCommand;
+@class MPRatingCommand;
+@class MPRemoteCommand;
+@class MPSkipIntervalCommand;
 
 MP_EXTERN_CLASS_AVAILABLE(7_1)
 @interface MPRemoteCommandCenter : NSObject
@@ -22,6 +29,9 @@
 @property (nonatomic, readonly) MPRemoteCommand *togglePlayPauseCommand;
 @property (nonatomic, readonly) MPRemoteCommand *enableLanguageOptionCommand;
 @property (nonatomic, readonly) MPRemoteCommand *disableLanguageOptionCommand;
+@property (nonatomic, readonly) MPChangePlaybackRateCommand *changePlaybackRateCommand;
+@property (nonatomic, readonly) MPChangeRepeatModeCommand *changeRepeatModeCommand;
+@property (nonatomic, readonly) MPChangeShuffleModeCommand *changeShuffleModeCommand;
 
 // Previous/Next Track Commands
 @property (nonatomic, readonly) MPRemoteCommand *nextTrackCommand;
@@ -34,13 +44,11 @@
 // Seek Commands
 @property (nonatomic, readonly) MPRemoteCommand *seekForwardCommand;
 @property (nonatomic, readonly) MPRemoteCommand *seekBackwardCommand;
+@property (nonatomic, readonly) MPChangePlaybackPositionCommand *changePlaybackPositionCommand NS_AVAILABLE_IOS(9_1);
 
 // Rating Command
 @property (nonatomic, readonly) MPRatingCommand *ratingCommand;
 
-// Playback Commands
-@property (nonatomic, readonly) MPChangePlaybackRateCommand *changePlaybackRateCommand;
-
 // Feedback Commands
 // These are generalized to three distinct actions. Your application can provide
 // additional context about these actions with the localizedTitle property in
@@ -49,9 +57,8 @@
 @property (nonatomic, readonly) MPFeedbackCommand *dislikeCommand;
 @property (nonatomic, readonly) MPFeedbackCommand *bookmarkCommand;
 
-@property (nonatomic, readonly) MPChangePlaybackPositionCommand *changePlaybackPositionCommand;
-
 + (MPRemoteCommandCenter *)sharedCommandCenter;
+- (id)init NS_UNAVAILABLE;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandEvent.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandEvent.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandEvent.h	2015-09-30 23:40:10.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandEvent.h	2016-05-28 06:47:29.000000000 +0200
@@ -8,7 +8,7 @@
 #import <Foundation/Foundation.h>
 #import <MediaPlayer/MediaPlayerDefines.h>
 #import <MediaPlayer/MPNowPlayingInfoLanguageOption.h>
-
+#import <MediaPlayer/MPRemoteControlTypes.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -91,6 +91,9 @@
 /// is being requested. See MPNowPlayingInfoLanguageOption isAutomaticLegibleLanguageOption
 @property (nonatomic, readonly) MPNowPlayingInfoLanguageOption *languageOption;
 
+/// Describes the extent of the changed language option
+@property (nonatomic, readonly) MPChangeLanguageOptionSetting setting;
+
 @end
 
 MP_EXTERN_CLASS_AVAILABLE(8_0)
@@ -101,4 +104,20 @@
 
 @end
 
+MP_EXTERN_CLASS_AVAILABLE(8_0)
+@interface MPChangeShuffleModeCommandEvent : MPRemoteCommandEvent
+
+/// The desired shuffle type to use when fulfilling the request.
+@property (nonatomic, readonly) MPShuffleType shuffleType;
+
+@end
+
+MP_EXTERN_CLASS_AVAILABLE(8_0)
+@interface MPChangeRepeatModeCommandEvent : MPRemoteCommandEvent
+
+/// The desired repeat type to use when fulfilling the request.
+@property (nonatomic, readonly) MPRepeatType repeatType;
+
+@end
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteControlTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteControlTypes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteControlTypes.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteControlTypes.h	2016-05-28 06:47:29.000000000 +0200
@@ -0,0 +1,27 @@
+//
+//  MPRemoteControlTypes.h
+//  MediaPlayerFramework
+//
+//  Copyright (c) 2016 Apple, Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <MediaPlayer/MediaPlayerDefines.h>
+
+typedef NS_ENUM(NSInteger, MPShuffleType) {
+    MPShuffleTypeOff,           /// Nothing is shuffled during playback.
+    MPShuffleTypeItems,         /// Individual items are shuffled during playback.
+    MPShuffleTypeCollections,   /// Collections (e.g. albums) are shuffled during playback.
+} NS_ENUM_AVAILABLE_IOS(3_0);
+
+typedef NS_ENUM(NSInteger, MPRepeatType) {
+    MPRepeatTypeOff,    /// Nothing is repeated during playback.
+    MPRepeatTypeOne,    /// Repeat a single item indefinitely.
+    MPRepeatTypeAll,    /// Repeat the current container or playlist indefinitely.
+} NS_ENUM_AVAILABLE_IOS(3_0);
+
+typedef NS_ENUM(NSInteger, MPChangeLanguageOptionSetting) {
+    MPChangeLanguageOptionSettingNone, /// No Language Option Change
+    MPChangeLanguageOptionSettingNowPlayingItemOnly, /// The Language Option change applies only the the now playing item
+    MPChangeLanguageOptionSettingPermanent /// The Language Option change should apply to all future playback
+} NS_ENUM_AVAILABLE_IOS(9_4);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayer.h	2016-02-27 05:48:04.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayer.h	2016-05-28 06:47:29.000000000 +0200
@@ -27,5 +27,6 @@
 #import <MediaPlayer/MPRemoteCommand.h>
 #import <MediaPlayer/MPRemoteCommandCenter.h>
 #import <MediaPlayer/MPRemoteCommandEvent.h>
+#import <MediaPlayer/MPRemoteControlTypes.h>
 #import <MediaPlayer/MPVolumeSettings.h>
-#import <MediaPlayer/MPVolumeView.h>
\ No newline at end of file
+#import <MediaPlayer/MPVolumeView.h>

```