#PhotosUI.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHLivePhotoView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHLivePhotoView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHLivePhotoView.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHLivePhotoView.h	2016-06-02 04:08:52.000000000 +0200
@@ -0,0 +1,59 @@
+//
+//  PHLivePhotoView.h
+//  PhotosUI
+//
+//  Copyright © 2015 Apple Inc. All rights reserved.
+//
+
+#import <AppKit/AppKit.h>
+#import <Photos/PHLivePhoto.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@protocol PHLivePhotoViewDelegate;
+
+typedef NS_ENUM(NSInteger, PHLivePhotoViewPlaybackStyle) {
+    PHLivePhotoViewPlaybackStyleUndefined = 0,
+    PHLivePhotoViewPlaybackStyleFull,
+    PHLivePhotoViewPlaybackStyleHint,
+} NS_ENUM_AVAILABLE(10_12, 9_1);
+
+NS_CLASS_AVAILABLE(10_12, 9_1)
+@interface PHLivePhotoView : NSView
+
+@property (readwrite, nonatomic, weak, nullable) id<PHLivePhotoViewDelegate> delegate;
+
+/// Live photo displayed in the receiver.
+@property (readwrite, nonatomic, strong, nullable) PHLivePhoto *livePhoto;
+
+/// The audio volume during playback
+@property (readwrite, nonatomic, assign) float audioVolume;
+
+/// Indicates whether the audio of the Live Photo is muted.
+@property (readwrite, nonatomic, assign, getter=isMuted) BOOL muted;
+
+/// Gesture used to trigger playback. By default, added to the receiver. Can be moved to a different view.
+@property (readonly, nonatomic, strong) NSGestureRecognizer *playbackGestureRecognizer;
+
+/// The following methods allow the client to manually trigger playback. If the live photo is changed during playback, it will be immediately interrupted.
+- (void)startPlaybackWithStyle:(PHLivePhotoViewPlaybackStyle)playbackStyle;
+- (void)stopPlayback;
+
+/// Directly access the livePhotoBadge in cases where it should be added to a different place in the view hierachy and not the live photo view. This can be useful when the live photo view is added to a scroll view.
+@property (readonly, nonatomic, strong, nullable) NSView *livePhotoBadgeView NS_AVAILABLE_MAC(10_12);
+
+@end
+
+
+NS_CLASS_AVAILABLE(10_12, 9_1)
+@protocol PHLivePhotoViewDelegate <NSObject>
+@optional
+
+- (void)livePhotoView:(PHLivePhotoView *)livePhotoView willBeginPlaybackWithStyle:(PHLivePhotoViewPlaybackStyle)playbackStyle;
+
+- (void)livePhotoView:(PHLivePhotoView *)livePhotoView didEndPlaybackWithStyle:(PHLivePhotoViewPlaybackStyle)playbackStyle;
+
+@end
+
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PhotosUI.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PhotosUI.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PhotosUI.h	2015-08-24 08:23:04.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PhotosUI.h	2016-06-02 04:08:52.000000000 +0200
@@ -9,5 +9,6 @@
 #define PhotosUI_PhotosUI_h
 
 #import <PhotosUI/PHContentEditingController.h>
+#import <PhotosUI/PHLivePhotoView.h>
 
 #endif

```