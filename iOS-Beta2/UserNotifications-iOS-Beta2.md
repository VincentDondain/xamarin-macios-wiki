#UserNotifications.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationContent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationContent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationContent.h	2016-05-23 06:24:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationContent.h	2016-06-26 08:24:28.000000000 +0200
@@ -78,7 +78,7 @@
 @property (NS_NONATOMIC_IOSONLY, copy) NSString *title __TVOS_PROHIBITED;
 
 // Apps can set the userInfo for locally scheduled notification requests. The contents of the push payload will be set as the userInfo for remote notifications.
-@property (NS_NONATOMIC_IOSONLY, copy) NSDictionary *userInfo __TVOS_PROHIBITED;
+@property (NS_NONATOMIC_IOSONLY, copy) NSDictionary *userInfo;
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationTrigger.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationTrigger.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationTrigger.h	2016-05-23 06:11:18.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UserNotifications.framework/Headers/UNNotificationTrigger.h	2016-06-26 08:24:28.000000000 +0200
@@ -21,7 +21,7 @@
 @end
 
 // UNPushNotificationTrigger can be sent from a server using Apple Push Notification Service.
-__IOS_AVAILABLE(10.0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+__IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0)
 @interface UNPushNotificationTrigger : UNNotificationTrigger
 
 @end
@@ -52,12 +52,12 @@
 @end
 
 // UNLocationNotificationTrigger can be scheduled on the device to notify when the user enters or leaves a geographic region. The identifier on CLRegion must be unique. Scheduling multiple UNNotificationRequests with different regions containing the same identifier will result in undefined behavior. The number of UNLocationNotificationTriggers that may be scheduled by an application at any one time is limited by the system. Applications must have "when-in-use" authorization through CoreLocation. See the CoreLocation documentation for more information.
-__IOS_AVAILABLE(10.0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+__IOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0) __TVOS_PROHIBITED
 @interface UNLocationNotificationTrigger : UNNotificationTrigger
 
 @property (NS_NONATOMIC_IOSONLY, readonly, copy) CLRegion *region;
 
-+ (instancetype)triggerWithRegion:(CLRegion *)region repeats:(BOOL)repeats;
++ (instancetype)triggerWithRegion:(CLRegion *)region repeats:(BOOL)repeats __WATCHOS_PROHIBITED;
 
 @end
 

```