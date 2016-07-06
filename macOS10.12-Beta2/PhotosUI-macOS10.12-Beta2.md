#PhotosUI.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHContentEditingController.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHContentEditingController.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHContentEditingController.h	2016-06-02 04:08:52.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHContentEditingController.h	2016-06-27 04:21:50.000000000 +0200
@@ -7,8 +7,9 @@
 
 #import <Foundation/Foundation.h>
 
-@class PHAdjustmentData, PHContentEditingInput, PHContentEditingOutput;
+NS_ASSUME_NONNULL_BEGIN
 
+@class PHAdjustmentData, PHContentEditingInput, PHContentEditingOutput;
 
 // Protocol to which the principal view controller of the extension must conform.
 @protocol PHContentEditingController <NSObject>
@@ -21,7 +22,7 @@
 - (void)startContentEditingWithInput:(PHContentEditingInput *)contentEditingInput placeholderImage:(NSImage *)placeholderImage;
 
 // Called when the user finishes the editing session. The receiver should prevent the user from editing the asset further. Also, it should create the editing output and call the completion handler. The completion handler returns after the output has been consumed, so it is safe to perform clean up after it returns. The completion handler can (and should best) be called on a background queue.
-- (void)finishContentEditingWithCompletionHandler:(void (^)(PHContentEditingOutput *))completionHandler;
+- (void)finishContentEditingWithCompletionHandler:(void (^)(PHContentEditingOutput * _Nullable))completionHandler;
 
 // Called if the user cancels the editing session. (Can be called while the receiver is producing the editing output.)
 - (void)cancelContentEditing;
@@ -30,3 +31,5 @@
 @property (readonly, nonatomic) BOOL shouldShowCancelConfirmation;
 
 @end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHLivePhotoView.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHLivePhotoView.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHLivePhotoView.h	2016-06-02 04:08:52.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHLivePhotoView.h	2016-06-27 04:21:50.000000000 +0200
@@ -16,9 +16,14 @@
     PHLivePhotoViewPlaybackStyleUndefined = 0,
     PHLivePhotoViewPlaybackStyleFull,
     PHLivePhotoViewPlaybackStyleHint,
-} NS_ENUM_AVAILABLE(10_12, 9_1);
+} NS_ENUM_AVAILABLE_MAC(10_12);
 
-NS_CLASS_AVAILABLE(10_12, 9_1)
+typedef NS_ENUM(NSInteger, PHLivePhotoViewContentMode) {
+	PHLivePhotoViewContentModeAspectFit,
+	PHLivePhotoViewContentModeAspectFill,
+} NS_ENUM_AVAILABLE_MAC(10_12);
+
+NS_CLASS_AVAILABLE_MAC(10_12)
 @interface PHLivePhotoView : NSView
 
 @property (readwrite, nonatomic, weak, nullable) id<PHLivePhotoViewDelegate> delegate;
@@ -26,18 +31,20 @@
 /// Live photo displayed in the receiver.
 @property (readwrite, nonatomic, strong, nullable) PHLivePhoto *livePhoto;
 
+/// The mode in which the receiver will display its content. Defaults to PHLivePhotoViewContentModeAspectFit.
+@property (readwrite, nonatomic, assign) PHLivePhotoViewContentMode contentMode;
+
 /// The audio volume during playback
 @property (readwrite, nonatomic, assign) float audioVolume;
 
 /// Indicates whether the audio of the Live Photo is muted.
 @property (readwrite, nonatomic, assign, getter=isMuted) BOOL muted;
 
-/// Gesture used to trigger playback. By default, added to the receiver. Can be moved to a different view.
-@property (readonly, nonatomic, strong) NSGestureRecognizer *playbackGestureRecognizer;
-
 /// The following methods allow the client to manually trigger playback. If the live photo is changed during playback, it will be immediately interrupted.
 - (void)startPlaybackWithStyle:(PHLivePhotoViewPlaybackStyle)playbackStyle;
 - (void)stopPlayback;
+/// Stops live photo playback. If animated is NO, the photo is immediately displayed.
+- (void)stopPlaybackAnimated:(BOOL)animated;
 
 /// Directly access the livePhotoBadge in cases where it should be added to a different place in the view hierachy and not the live photo view. This can be useful when the live photo view is added to a scroll view.
 @property (readonly, nonatomic, strong, nullable) NSView *livePhotoBadgeView NS_AVAILABLE_MAC(10_12);
@@ -45,7 +52,7 @@
 @end
 
 
-NS_CLASS_AVAILABLE(10_12, 9_1)
+NS_CLASS_AVAILABLE_MAC(10_12)
 @protocol PHLivePhotoViewDelegate <NSObject>
 @optional
 

```