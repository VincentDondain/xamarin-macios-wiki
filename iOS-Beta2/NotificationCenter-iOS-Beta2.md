#NotificationCenter.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetProviding.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetProviding.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetProviding.h	2016-05-28 06:36:03.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetProviding.h	2016-06-26 09:23:54.000000000 +0200
@@ -42,7 +42,7 @@
 
 // If implemented, called when the active display mode changes.
 // The widget may wish to change its preferredContentSize to better accommodate the new display mode.
-- (void)widgetActiveDisplayModeDidChange:(NCWidgetDisplayMode)activeDisplayMode withMaximumSize:(CGSize)maxSize;
+- (void)widgetActiveDisplayModeDidChange:(NCWidgetDisplayMode)activeDisplayMode withMaximumSize:(CGSize)maxSize NS_AVAILABLE_IOS(10_0);
 
 // Widgets wishing to customize the default margin insets can return their preferred values.
 // Widgets that choose not to implement this method will receive the default margin insets.

```