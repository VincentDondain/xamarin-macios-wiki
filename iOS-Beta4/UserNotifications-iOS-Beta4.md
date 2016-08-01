#UserNotifications.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationAction.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationAction.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationAction.h	2016-07-11 07:05:06.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationAction.h	2016-07-25 07:06:09.000000000 +0200
@@ -33,7 +33,7 @@
 @property (NS_NONATOMIC_IOSONLY, copy, readonly) NSString *title;
 
 // The options configured for this action.
-@property (NS_NONATOMIC_IOSONLY, assign, readonly) UNNotificationActionOptions options;
+@property (NS_NONATOMIC_IOSONLY, readonly) UNNotificationActionOptions options;
 
 // Use -[NSString localizedUserNotificationStringForKey:arguments:] to provide a string that will be localized at the time that the notification is presented.
 + (instancetype)actionWithIdentifier:(NSString *)identifier title:(NSString *)title options:(UNNotificationActionOptions)options;
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationCategory.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationCategory.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationCategory.h	2016-07-11 07:05:06.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationCategory.h	2016-07-25 07:06:09.000000000 +0200
@@ -31,13 +31,10 @@
 // The UNNotificationActions in the order they will be displayed.
 @property (NS_NONATOMIC_IOSONLY, readonly, copy) NSArray<UNNotificationAction *> *actions;
 
-// The UNNotificationActions in the order they will be displayed. Used instead of the actions property when only two actions can be displayed.
-@property (NS_NONATOMIC_IOSONLY, readonly, copy) NSArray<UNNotificationAction *> *minimalActions;
-
 // The intents supported support for notifications of this category. See <Intents/INIntentIdentifiers.h> for possible values.
 @property (NS_NONATOMIC_IOSONLY, readonly, copy) NSArray<NSString *> *intentIdentifiers;
 
-@property (NS_NONATOMIC_IOSONLY, readonly, assign) UNNotificationCategoryOptions options;
+@property (NS_NONATOMIC_IOSONLY, readonly) UNNotificationCategoryOptions options;
 
 + (instancetype)categoryWithIdentifier:(NSString *)identifier actions:(NSArray<UNNotificationAction *> *)actions intentIdentifiers:(NSArray<NSString *> *)intentIdentifiers options:(UNNotificationCategoryOptions)options;
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationRequest.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationRequest.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationRequest.h	2016-07-11 07:05:06.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationRequest.h	2016-07-25 07:06:09.000000000 +0200
@@ -21,7 +21,7 @@
 // The content that will be shown on the notification.
 @property (NS_NONATOMIC_IOSONLY, readonly, copy) UNNotificationContent *content;
 
-// The trigger that will or did cause the notification to be delivered.
+// The trigger that will or did cause the notification to be delivered. No trigger means deliver now.
 @property (NS_NONATOMIC_IOSONLY, readonly, copy, nullable) UNNotificationTrigger *trigger;
 
 + (instancetype)requestWithIdentifier:(NSString *)identifier content:(UNNotificationContent *)content trigger:(nullable UNNotificationTrigger *)trigger;
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationSettings.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationSettings.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationSettings.h	2016-07-11 07:05:06.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationSettings.h	2016-07-25 07:06:09.000000000 +0200
@@ -40,17 +40,17 @@
 __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0)
 @interface UNNotificationSettings : NSObject <NSCopying, NSSecureCoding>
 
-@property (NS_NONATOMIC_IOSONLY, readonly, assign) UNAuthorizationStatus authorizationStatus;
+@property (NS_NONATOMIC_IOSONLY, readonly) UNAuthorizationStatus authorizationStatus;
 
-@property (NS_NONATOMIC_IOSONLY, readonly, assign) UNNotificationSetting soundSetting __TVOS_PROHIBITED;
-@property (NS_NONATOMIC_IOSONLY, readonly, assign) UNNotificationSetting badgeSetting __WATCHOS_PROHIBITED;
-@property (NS_NONATOMIC_IOSONLY, readonly, assign) UNNotificationSetting alertSetting __TVOS_PROHIBITED;
+@property (NS_NONATOMIC_IOSONLY, readonly) UNNotificationSetting soundSetting __TVOS_PROHIBITED;
+@property (NS_NONATOMIC_IOSONLY, readonly) UNNotificationSetting badgeSetting __WATCHOS_PROHIBITED;
+@property (NS_NONATOMIC_IOSONLY, readonly) UNNotificationSetting alertSetting __TVOS_PROHIBITED;
 
-@property (NS_NONATOMIC_IOSONLY, readonly, assign) UNNotificationSetting notificationCenterSetting __TVOS_PROHIBITED;
-@property (NS_NONATOMIC_IOSONLY, readonly, assign) UNNotificationSetting lockScreenSetting __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
-@property (NS_NONATOMIC_IOSONLY, readonly, assign) UNNotificationSetting carPlaySetting __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+@property (NS_NONATOMIC_IOSONLY, readonly) UNNotificationSetting notificationCenterSetting __TVOS_PROHIBITED;
+@property (NS_NONATOMIC_IOSONLY, readonly) UNNotificationSetting lockScreenSetting __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+@property (NS_NONATOMIC_IOSONLY, readonly) UNNotificationSetting carPlaySetting __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
-@property (NS_NONATOMIC_IOSONLY, readonly, assign) UNAlertStyle alertStyle __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+@property (NS_NONATOMIC_IOSONLY, readonly) UNAlertStyle alertStyle __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 - (instancetype)init NS_UNAVAILABLE;
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationTrigger.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationTrigger.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationTrigger.h	2016-07-11 07:05:06.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationTrigger.h	2016-07-25 07:06:09.000000000 +0200
@@ -14,7 +14,7 @@
 __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0)
 @interface UNNotificationTrigger : NSObject <NSCopying, NSSecureCoding>
 
-@property (NS_NONATOMIC_IOSONLY, readonly, assign) BOOL repeats;
+@property (NS_NONATOMIC_IOSONLY, readonly) BOOL repeats;
 
 - (instancetype)init NS_UNAVAILABLE;
 
@@ -30,7 +30,7 @@
 __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0)
 @interface UNTimeIntervalNotificationTrigger : UNNotificationTrigger
 
-@property (NS_NONATOMIC_IOSONLY, readonly, assign) NSTimeInterval timeInterval;
+@property (NS_NONATOMIC_IOSONLY, readonly) NSTimeInterval timeInterval;
 
 + (instancetype)triggerWithTimeInterval:(NSTimeInterval)timeInterval repeats:(BOOL)repeats;
 

```