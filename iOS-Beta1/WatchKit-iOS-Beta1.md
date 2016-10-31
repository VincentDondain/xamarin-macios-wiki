#WatchKit.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKBackgroundTask.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKBackgroundTask.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKBackgroundTask.h	2016-09-24 04:06:15.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKBackgroundTask.h	2016-10-22 04:14:54.000000000 +0200
@@ -13,6 +13,16 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+// If the app fails to complete its background tasks within the allocated time,
+// the system terminates the app and generates a crash report.
+// These crash reports contain a unique exception code that describes the reason for the crash.
+// To address these issues, decrease the amount of work that the app performs while running in the background.
+//
+// 0xc51bad01 - The app used too much CPU time
+// 0xc51bad02 - The app used too much wall time
+// 0xc51bad03 - The app did not receive sufficient runtime due to other system tasks.
+//
+
 WK_AVAILABLE_WATCHOS_ONLY(3.0)
 @interface WKRefreshBackgroundTask : NSObject
 @property (readonly, nullable) id<NSSecureCoding> userInfo;
@@ -35,7 +45,7 @@
 //                                         Use [NSDate distantFuture] if the snapshot doesn't need to be replaced.
 // userInfo                         -   Will be returned with the task that eventually runs
 - (void)setTaskCompletedWithDefaultStateRestored:(BOOL)restoredDefaultState
-                     estimatedSnapshotExpiration:(NSDate *)estimatedSnapshotExpiration
+                     estimatedSnapshotExpiration:(nullable NSDate *)estimatedSnapshotExpiration
                                         userInfo:(nullable id<NSSecureCoding>)userInfo
 NS_SWIFT_NAME(setTaskCompleted(restoredDefaultState:estimatedSnapshotExpiration:userInfo:));
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKExtension.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKExtension.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKExtension.h	2016-09-24 04:06:15.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKExtension.h	2016-10-22 04:14:54.000000000 +0200
@@ -48,7 +48,7 @@
 - (void)applicationDidEnterBackground;
 
 // iOS app started a workout. -[HKHealthStore startWorkoutSession:] should be called from here
-- (void)handleWorkoutConfiguration:(HKWorkoutConfiguration *)workoutConfiguration;
+- (void)handleWorkoutConfiguration:(HKWorkoutConfiguration *)workoutConfiguration WK_AVAILABLE_WATCHOS_ONLY(3.0);
 
 - (void)handleUserActivity:(nullable NSDictionary *)userInfo;
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceController.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceController.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceController.h	2016-10-05 06:02:58.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceController.h	2016-10-22 04:14:54.000000000 +0200
@@ -92,7 +92,7 @@
 - (void)pickerDidSettle:(WKInterfacePicker *)picker WK_AVAILABLE_WATCHOS_ONLY(2.0);
 
 - (void)table:(WKInterfaceTable *)table didSelectRowAtIndex:(NSInteger)rowIndex;  // row selection if controller has WKInterfaceTable property
-- (void)handleActionWithIdentifier:(nullable NSString *)identifier forNotification:(UNNotification *)notification WK_CLASS_AVAILABLE_IOS(10.0); // when the app is launched from a notification. If launched from app icon in notification UI, identifier will be empty
+- (void)handleActionWithIdentifier:(nullable NSString *)identifier forNotification:(UNNotification *)notification WK_AVAILABLE_IOS_ONLY(10.0); // when the app is launched from a notification. If launched from app icon in notification UI, identifier will be empty
 - (void)handleUserActivity:(nullable NSDictionary *)userInfo; // called on root controller(s) with user info
 
 - (void)setTitle:(nullable NSString *)title;        // title of controller. displayed when controller active
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceDevice.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceDevice.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceDevice.h	2016-09-24 04:06:15.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceDevice.h	2016-10-22 04:14:54.000000000 +0200
@@ -53,6 +53,7 @@
     WKWaterResistanceRatingWR50 NS_SWIFT_NAME(wr50),
 } WK_AVAILABLE_WATCHOS_ONLY(3.0);
 #endif
+
 @interface WKInterfaceDevice : NSObject
 
 + (WKInterfaceDevice *)currentDevice;
@@ -82,6 +83,7 @@
 #if TARGET_OS_WATCH
 @property (nonatomic,readonly) WKWaterResistanceRating waterResistanceRating WK_AVAILABLE_WATCHOS_ONLY(3.0);
 #endif
+
 - (void)playHaptic:(WKHapticType)type WK_AVAILABLE_WATCHOS_ONLY(2.0);
 
 @end

```