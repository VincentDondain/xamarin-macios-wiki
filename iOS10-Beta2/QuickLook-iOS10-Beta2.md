#QuickLook.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuickLook.framework/Headers/QLPreviewController.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuickLook.framework/Headers/QLPreviewController.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuickLook.framework/Headers/QLPreviewController.h	2016-05-26 07:33:21.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuickLook.framework/Headers/QLPreviewController.h	2016-06-26 10:27:02.000000000 +0200
@@ -12,8 +12,6 @@
 @protocol QLPreviewControllerDelegate;
 @protocol QLPreviewControllerDataSource;
 
-@class QLPreviewControllerReserved;
-
 NS_ASSUME_NONNULL_BEGIN
 
 NS_CLASS_AVAILABLE_IOS(4_0) QL_EXPORT

```