#UserNotifications.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNError.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNError.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNError.h	2016-06-26 07:15:52.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNError.h	2016-07-11 07:07:18.000000000 +0200
@@ -18,4 +18,7 @@
     UNErrorCodeAttachmentNotInDataStore,
     UNErrorCodeAttachmentMoveIntoDataStoreFailed,
     UNErrorCodeAttachmentCorrupt,
+    
+    UNErrorCodeNotificationInvalidNoDate = 1400,
+    UNErrorCodeNotificationInvalidNoContent,
 } __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationCategory.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationCategory.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationCategory.h	2016-06-26 07:15:52.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationCategory.h	2016-07-11 07:07:18.000000000 +0200
@@ -39,7 +39,7 @@
 
 @property (NS_NONATOMIC_IOSONLY, readonly, assign) UNNotificationCategoryOptions options;
 
-+ (instancetype)categoryWithIdentifier:(NSString *)identifier actions:(NSArray<UNNotificationAction *> *)actions minimalActions:(NSArray<UNNotificationAction *> *)minimalActions intentIdentifiers:(NSArray<NSString *> *)intentIdentifiers options:(UNNotificationCategoryOptions)options;
++ (instancetype)categoryWithIdentifier:(NSString *)identifier actions:(NSArray<UNNotificationAction *> *)actions intentIdentifiers:(NSArray<NSString *> *)intentIdentifiers options:(UNNotificationCategoryOptions)options;
 
 - (instancetype)init NS_UNAVAILABLE;
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNUserNotificationCenter.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNUserNotificationCenter.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNUserNotificationCenter.h	2016-06-26 08:24:28.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNUserNotificationCenter.h	2016-07-11 07:04:37.000000000 +0200
@@ -36,6 +36,9 @@
 // The delegate can only be set from an application
 @property (NS_NONATOMIC_IOSONLY, nullable, weak) id <UNUserNotificationCenterDelegate> delegate;
 
+// Returns YES if the current device supports content extensions
+@property (NS_NONATOMIC_IOSONLY, readonly) BOOL supportsContentExtensions;
+
 // The UNUserNotificationCenter for the current application
 + (UNUserNotificationCenter *)currentNotificationCenter;
 

```