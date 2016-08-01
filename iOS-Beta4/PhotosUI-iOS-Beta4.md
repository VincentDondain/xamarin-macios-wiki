#PhotosUI.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PhotosUI.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PhotosUI.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PhotosUI.h	2016-07-13 05:48:48.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PhotosUI.h	2016-07-28 05:26:44.000000000 +0200
@@ -8,6 +8,8 @@
 #ifndef PhotosUI_PhotosUI_h
 #define PhotosUI_PhotosUI_h
 
+#import <TargetConditionals.h>
+
 #if !TARGET_OS_TV
 #import <PhotosUI/PHContentEditingController.h>
 #endif

```