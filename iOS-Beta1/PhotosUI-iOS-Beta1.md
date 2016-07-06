#PhotosUI.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHContentEditingController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHContentEditingController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHContentEditingController.h	2015-10-03 02:24:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHContentEditingController.h	2016-06-01 05:16:03.000000000 +0200
@@ -8,8 +8,9 @@
 #import <Foundation/Foundation.h>
 #import <UIKit/UIImage.h>
 
-@class PHAdjustmentData, PHContentEditingInput, PHContentEditingOutput;
+NS_ASSUME_NONNULL_BEGIN
 
+@class PHAdjustmentData, PHContentEditingInput, PHContentEditingOutput;
 
 // Protocol to which the principal view controller of the extension must conform.
 @protocol PHContentEditingController <NSObject>
@@ -31,3 +32,5 @@
 @property (readonly, nonatomic) BOOL shouldShowCancelConfirmation;
 
 @end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHLivePhotoView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHLivePhotoView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHLivePhotoView.h	2015-10-03 02:24:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHLivePhotoView.h	2016-06-01 05:16:03.000000000 +0200
@@ -15,15 +15,15 @@
 typedef NS_OPTIONS(NSUInteger, PHLivePhotoBadgeOptions) {
     PHLivePhotoBadgeOptionsOverContent  = 1 << 0,               ///< Include treatments so this image can be shown directly over the content of the Live Photo
     PHLivePhotoBadgeOptionsLiveOff      = 1 << 1,               ///< To indicate that the Live Photo aspect is turned off and it will be treated as a still (e.g. for sharing)
-} NS_ENUM_AVAILABLE_IOS(9_1);
+} PHOTOS_ENUM_AVAILABLE_IOS_TVOS(9_1, 10_0);
 
 typedef NS_ENUM(NSInteger, PHLivePhotoViewPlaybackStyle) {
     PHLivePhotoViewPlaybackStyleUndefined = 0,
     PHLivePhotoViewPlaybackStyleFull,
     PHLivePhotoViewPlaybackStyleHint,
-} NS_ENUM_AVAILABLE_IOS(9_1);
+} PHOTOS_ENUM_AVAILABLE_IOS_TVOS(9_1, 10_0);
 
-NS_CLASS_AVAILABLE_IOS(9_1)
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(9_1, 10_0)
 @interface PHLivePhotoView : UIView
 
 /// System badge images representing Live Photo content

```