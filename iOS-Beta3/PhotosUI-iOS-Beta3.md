#PhotosUI.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PhotosUI.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PhotosUI.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PhotosUI.h	2016-06-28 08:43:14.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PhotosUI.h	2016-07-13 05:48:48.000000000 +0200
@@ -8,7 +8,9 @@
 #ifndef PhotosUI_PhotosUI_h
 #define PhotosUI_PhotosUI_h
 
+#if !TARGET_OS_TV
 #import <PhotosUI/PHContentEditingController.h>
+#endif
 #import <PhotosUI/PHLivePhotoView.h>
 
 #endif

```