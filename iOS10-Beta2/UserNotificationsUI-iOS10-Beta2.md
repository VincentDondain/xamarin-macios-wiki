#UserNotificationsUI.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotificationsUI.framework/Headers/UNNotificationContentExtension.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotificationsUI.framework/Headers/UNNotificationContentExtension.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotificationsUI.framework/Headers/UNNotificationContentExtension.h	2016-06-01 05:02:51.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotificationsUI.framework/Headers/UNNotificationContentExtension.h	2016-06-28 08:28:28.000000000 +0200
@@ -12,15 +12,15 @@
 
 typedef NS_ENUM(NSUInteger, UNNotificationContentExtensionMediaPlayPauseButtonType) {
     UNNotificationContentExtensionMediaPlayPauseButtonTypeNone,
-    UNNotificationContentExtensionMediaPlayPauseButtonTypeAudio,
-    UNNotificationContentExtensionMediaPlayPauseButtonTypeMovie,
-} __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE __OSX_UNAVAILABLE;
+    UNNotificationContentExtensionMediaPlayPauseButtonTypeDefault,
+    UNNotificationContentExtensionMediaPlayPauseButtonTypeOverlay,
+} __IOS_AVAILABLE(10_0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE __OSX_UNAVAILABLE;
 
 typedef NS_ENUM(NSUInteger, UNNotificationContentExtensionResponseOption) {
     UNNotificationContentExtensionResponseOptionDoNotDismiss,
     UNNotificationContentExtensionResponseOptionDismiss,
     UNNotificationContentExtensionResponseOptionDismissAndForwardAction,
-} __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE __OSX_UNAVAILABLE;
+} __IOS_AVAILABLE(10_0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE __OSX_UNAVAILABLE;
 
 NS_ASSUME_NONNULL_BEGIN
 

```