#WatchKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKBackgroundTask.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKBackgroundTask.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKBackgroundTask.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKBackgroundTask.h	2016-05-25 05:22:23.000000000 +0200
@@ -0,0 +1,69 @@
+//
+//  WKBackgroundTask.h
+//  WatchKit
+//
+//  Copyright (c) 2016 Apple. All rights reserved.
+//
+
+#if TARGET_OS_WATCH
+
+#import <ClockKit/ClockKit.h>
+#import <WatchKit/WatchKit.h>
+#import <WatchKit/WKExtension.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+@interface WKRefreshBackgroundTask : NSObject
+@property (readonly, nullable) id<NSSecureCoding> userInfo;
+
+- (void)setTaskCompleted;   // developer should call this when this task has been completed
+@end
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+@interface WKApplicationRefreshBackgroundTask : WKRefreshBackgroundTask
+- (void)setTaskCompleted;   // developer should call this when this task has been completed
+@end
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+@interface WKSnapshotRefreshBackgroundTask : WKRefreshBackgroundTask
+@property (readonly) BOOL returnToGlanceableUI WK_DEPRECATED_WATCHOS(3.0, 3.0, "use returnToDefaultState");  // to be removed before branching for seed on 5/15
+@property (readonly) BOOL returnToDefaultState;
+
+// developer should call setTaskCompletedWithDefaultStateRestored when preparation for snapshot has been completed
+// restoredDefaultState             -   YES if the app is its default state
+// estimatedSnapshotExpiration      -      Date at which the snapshot should be scheduled for replacement.
+//                                         If nil then the snapshot needs to be replaced asap.
+//                                         Use [NSDate distantFuture] if the snapshot doesn't need to be replaced.
+// userInfo                         -   Will be returned with the task that eventually runs
+- (void)setTaskCompletedWithDefaultStateRestored:(BOOL)restoredDefaultState
+                     estimatedSnapshotExpiration:(NSDate *)estimatedSnapshotExpiration
+                                        userInfo:(nullable id<NSSecureCoding>)userInfo
+NS_SWIFT_NAME(setTaskCompleted(restoredDefaultState:estimatedSnapshotExpiration:userInfo:));
+
+@end
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+@interface WKURLSessionRefreshBackgroundTask : WKRefreshBackgroundTask
+@property (readonly, copy) NSString *sessionIdentifier;
+- (void)setTaskCompleted;   // developer should call this when this task has been completed
+@end
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+@interface WKWatchConnectivityRefreshBackgroundTask : WKRefreshBackgroundTask
+- (void)setTaskCompleted;   // developer should call this when this task has been completed
+@end
+
+@interface WKExtension (WKBackgroundTasks)
+
+// there can only be one background refresh request at any given time. Scheduling a second request will cancel the previously scheduled request
+- (void)scheduleBackgroundRefreshWithPreferredDate:(NSDate *)preferredFireDate userInfo:(nullable id<NSSecureCoding>)userInfo scheduledCompletion:(void(^)(NSError * _Nullable error))scheduledCompletion WK_AVAILABLE_WATCHOS_ONLY(3.0);
+
+// there can only be one snapshot refresh request at any given time. Scheduling a second request will cancel the previously scheduled request
+- (void)scheduleSnapshotRefreshWithPreferredDate:(NSDate *)preferredFireDate userInfo:(nullable id<NSSecureCoding>)userInfo scheduledCompletion:(void(^)(NSError * _Nullable error))scheduledCompletion WK_AVAILABLE_WATCHOS_ONLY(3.0);
+
+@end
+
+NS_ASSUME_NONNULL_END
+
+#endif //TARGET_OS_WATCH
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKCrownSequencer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKCrownSequencer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKCrownSequencer.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKCrownSequencer.h	2016-05-25 05:22:23.000000000 +0200
@@ -0,0 +1,37 @@
+//
+//  WKCrownSequencer.h
+//  WatchKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+NS_ASSUME_NONNULL_BEGIN
+
+@protocol WKCrownDelegate;
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+@interface WKCrownSequencer : NSObject
+
+@property (nonatomic, weak, nullable) id<WKCrownDelegate> delegate;
+@property (nonatomic, readonly) double rotationsPerSecond;
+@property (nonatomic, readonly, getter=isIdle) BOOL idle;
+
+- (instancetype)init NS_UNAVAILABLE;
+// Sets this sequencer as focused, automatically resigns focus of any WKPickerViews
+- (void)focus;
+- (void)resignFocus;
+
+@end
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+@protocol WKCrownDelegate <NSObject>
+
+@optional
+// called when the crown rotates, rotationalDelta is the change since the last call (sign indicates direction).
+- (void)crownDidRotate:(nullable WKCrownSequencer *)crownSequencer rotationalDelta:(double)rotationalDelta;
+// called when the crown becomes idle
+- (void)crownDidBecomeIdle:(nullable WKCrownSequencer *)crownSequencer;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKExtension.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKExtension.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKExtension.h	2015-10-03 02:04:42.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKExtension.h	2016-05-25 05:22:23.000000000 +0200
@@ -21,11 +25,16 @@
 - (void)openSystemURL:(NSURL *)url;
 
 @property (nonatomic, weak, nullable) id<WKExtensionDelegate> delegate;
-@property (nonatomic,readonly, nullable) WKInterfaceController *rootInterfaceController;
+@property (nonatomic, readonly, nullable) WKInterfaceController *rootInterfaceController;
 
-@end
+typedef NS_ENUM(NSInteger, WKApplicationState) {
+    WKApplicationStateActive,
+    WKApplicationStateInactive,
+    WKApplicationStateBackground,
+} WK_AVAILABLE_WATCHOS_ONLY(3.0);
+@property (nonatomic, readonly) WKApplicationState applicationState WK_AVAILABLE_WATCHOS_ONLY(3.0);
 
-@class UILocalNotification;
+@end
 
 WK_AVAILABLE_WATCHOS_ONLY(2.0)
 @protocol WKExtensionDelegate <NSObject>
@@ -35,15 +44,23 @@
 - (void)applicationDidFinishLaunching;
 - (void)applicationDidBecomeActive;
 - (void)applicationWillResignActive;
+- (void)applicationWillEnterForeground;
+- (void)applicationDidEnterBackground;
+
+// iOS app started a workout. -[HKHealthStore startWorkoutSession:] should be called from here
+- (void)handleWorkoutConfiguration:(HKWorkoutConfiguration *)workoutConfiguration;
 
-- (void)handleActionWithIdentifier:(nullable NSString *)identifier forRemoteNotification:(NSDictionary *)remoteNotification; // when the app is launched from a notification. If launched from app icon in notification UI, identifier will be empty
-- (void)handleActionWithIdentifier:(nullable NSString *)identifier forLocalNotification:(UILocalNotification *)localNotification; // when the app is launched from a notification. If launched from app icon in notification UI, identifier will be empty
-- (void)handleActionWithIdentifier:(nullable NSString *)identifier forRemoteNotification:(NSDictionary *)remoteNotification withResponseInfo:(NSDictionary *)responseInfo; // when the app is launched from a notification. If launched from app icon in notification UI, identifier will be empty
-- (void)handleActionWithIdentifier:(nullable NSString *)identifier forLocalNotification:(UILocalNotification *)localNotification withResponseInfo:(NSDictionary *)responseInfo; // when the app is launched from a notification. If launched from app icon in notification UI, identifier will be empty
 - (void)handleUserActivity:(nullable NSDictionary *)userInfo;
 
-- (void)didReceiveRemoteNotification:(NSDictionary *)userInfo;
-- (void)didReceiveLocalNotification:(UILocalNotification *)notification;
+- (void)handleBackgroundTasks:(NSSet <WKRefreshBackgroundTask *> *)backgroundTasks WK_AVAILABLE_WATCHOS_ONLY(3.0);
+
+// deprecated
+- (void)handleActionWithIdentifier:(nullable NSString *)identifier forRemoteNotification:(NSDictionary *)remoteNotification WK_DEPRECATED_WATCHOS(2.0, 3.0, "use UNUserNotificationCenterDelegate");
+- (void)handleActionWithIdentifier:(nullable NSString *)identifier forLocalNotification:(UILocalNotification *)localNotification WK_DEPRECATED_WATCHOS(2.0, 3.0, "use UNUserNotificationCenterDelegate");
+- (void)handleActionWithIdentifier:(nullable NSString *)identifier forRemoteNotification:(NSDictionary *)remoteNotification withResponseInfo:(NSDictionary *)responseInfo WK_DEPRECATED_WATCHOS(2.0, 3.0, "use UNUserNotificationCenterDelegate");
+- (void)handleActionWithIdentifier:(nullable NSString *)identifier forLocalNotification:(UILocalNotification *)localNotification withResponseInfo:(NSDictionary *)responseInfo WK_DEPRECATED_WATCHOS(2.0, 3.0, "use UNUserNotificationCenterDelegate");
+- (void)didReceiveRemoteNotification:(NSDictionary *)userInfo WK_DEPRECATED_WATCHOS(2.0, 3.0, "use UNUserNotificationCenterDelegate");
+- (void)didReceiveLocalNotification:(UILocalNotification *)notification WK_DEPRECATED_WATCHOS(2.0, 3.0, "use UNUserNotificationCenterDelegate");
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKGestureRecognizer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKGestureRecognizer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKGestureRecognizer.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKGestureRecognizer.h	2016-05-25 05:22:23.000000000 +0200
@@ -0,0 +1,87 @@
+//
+//  WKGestureRecognizer.h
+//  WatchKit
+//
+//  Copyright © 2015 Apple Inc. All rights reserved.
+//
+
+
+#import <WatchKit/WKDefines.h>
+
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+typedef NS_ENUM(NSInteger, WKGestureRecognizerState) {
+    WKGestureRecognizerStatePossible,   // = UIGestureRecognizerStatePossible
+    WKGestureRecognizerStateBegan,      // = UIGestureRecognizerStateBegan
+    WKGestureRecognizerStateChanged,    // = UIGestureRecognizerStateChanged
+    WKGestureRecognizerStateEnded,      // = UIGestureRecognizerStateEnded
+    WKGestureRecognizerStateCancelled,  // = UIGestureRecognizerStateCancelled
+    WKGestureRecognizerStateFailed,     // = UIGestureRecognizerStateFailed
+    WKGestureRecognizerStateRecognized  // = UIGestureRecognizerStateRecognized
+};
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+typedef NS_OPTIONS(NSUInteger, WKSwipeGestureRecognizerDirection) {
+    WKSwipeGestureRecognizerDirectionRight = 1 << 0,    // = UISwipeGestureRecognizerDirectionRight
+    WKSwipeGestureRecognizerDirectionLeft  = 1 << 1,    // = UISwipeGestureRecognizerDirectionLeft
+    WKSwipeGestureRecognizerDirectionUp    = 1 << 2,    // = UISwipeGestureRecognizerDirectionUp
+    WKSwipeGestureRecognizerDirectionDown  = 1 << 3     // = UISwipeGestureRecognizerDirectionDown
+};
+
+
+NS_ASSUME_NONNULL_BEGIN
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+@interface WKGestureRecognizer : NSObject   // abstract class
+
+@property(nonatomic, readonly) WKGestureRecognizerState state;
+@property(nonatomic, getter=isEnabled) BOOL enabled;
+
+- (CGPoint)locationInObject;      // always refers to the interface object the gesture recognizer is attached to
+- (CGRect)objectBounds;           // locationInObject's viewBounds
+- (NSUInteger)numberOfTouches;    // always 1 in watchOS 3
+
+@end
+
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+@interface WKTapGestureRecognizer : WKGestureRecognizer
+
+@property(nonatomic) NSUInteger numberOfTapsRequired;
+@property(nonatomic, readonly) NSUInteger numberOfTouchesRequired;  // always 1 in watchOS 3
+
+@end
+
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+@interface WKLongPressGestureRecognizer : WKGestureRecognizer
+
+@property(nonatomic) CFTimeInterval minimumPressDuration;
+@property(nonatomic, readonly) NSUInteger numberOfTouchesRequired;  // always 1 in watchOS 3
+@property(nonatomic) NSUInteger numberOfTapsRequired;
+@property(nonatomic) CGFloat allowableMovement;
+
+@end
+
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+@interface WKSwipeGestureRecognizer : WKGestureRecognizer
+
+@property(nonatomic) WKSwipeGestureRecognizerDirection direction;
+@property(nonatomic, readonly) NSUInteger numberOfTouchesRequired;  // always 1 in watchOS 3
+
+@end
+
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+@interface WKPanGestureRecognizer : WKGestureRecognizer
+
+@property(nonatomic, readonly) NSUInteger maximumNumberOfTouches;   // always 1 in watchOS 3
+@property(nonatomic, readonly) NSUInteger minimumNumberOfTouches;   // always 1 in watchOS 3
+
+- (CGPoint)translationInObject;   // always refers to the interface object the gesture recognizer is attached to
+- (CGPoint)velocityInObject;      // always refers to the interface object the gesture recognizer is attached to
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceController.h	2015-10-31 03:27:49.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceController.h	2016-06-03 05:34:20.000000000 +0200
@@ -77,6 +79,7 @@
 - (void)awakeWithContext:(nullable id)context;   // context from controller that did push or modal presentation. default does nothing
 
 @property (nonatomic, readonly) CGRect contentFrame;
+@property (nonatomic, strong, readonly) WKCrownSequencer *crownSequencer;
 
 - (void)willActivate;      // Called when watch interface is active and able to be updated. Can be called when interface is not visible.
 - (void)didDeactivate;     // Called when watch interface is no longer active and cannot be updated.
@@ -89,8 +92,7 @@
 - (void)pickerDidSettle:(WKInterfacePicker *)picker WK_AVAILABLE_WATCHOS_ONLY(2.0);
 
 - (void)table:(WKInterfaceTable *)table didSelectRowAtIndex:(NSInteger)rowIndex;  // row selection if controller has WKInterfaceTable property
-- (void)handleActionWithIdentifier:(nullable NSString *)identifier forRemoteNotification:(NSDictionary *)remoteNotification; // when the app is launched from a notification. If launched from app icon in notification UI, identifier will be empty
-- (void)handleActionWithIdentifier:(nullable NSString *)identifier forLocalNotification:(UILocalNotification *)localNotification; // when the app is launched from a notification. If launched from app icon in notification UI, identifier will be empty
+- (void)handleActionWithIdentifier:(nullable NSString *)identifier forNotification:(UNNotification *)notification WK_CLASS_AVAILABLE_IOS(10.0); // when the app is launched from a notification. If launched from app icon in notification UI, identifier will be empty
 - (void)handleUserActivity:(nullable NSDictionary *)userInfo; // called on root controller(s) with user info
 
 - (void)setTitle:(nullable NSString *)title;        // title of controller. displayed when controller active
@@ -154,6 +156,10 @@
 - (void)beginGlanceUpdates WK_AVAILABLE_WATCHOS_ONLY(2.0);
 - (void)endGlanceUpdates WK_AVAILABLE_WATCHOS_ONLY(2.0);
 
+// deprecated
+- (void)handleActionWithIdentifier:(nullable NSString *)identifier forRemoteNotification:(NSDictionary *)remoteNotification WK_DEPRECATED_WATCHOS_IOS(2.0, 3.0, 8.2, 10.0, "use UNUserNotificationCenterDelegate");
+- (void)handleActionWithIdentifier:(nullable NSString *)identifier forLocalNotification:(UILocalNotification *)localNotification WK_DEPRECATED_WATCHOS_IOS(2.0, 3.0, 8.2, 10.0, "use UNUserNotificationCenterDelegate");
+
 @end
 
 WK_CLASS_AVAILABLE_IOS(8_2)
@@ -161,14 +167,16 @@
 
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
 
-- (void)didReceiveRemoteNotification:(NSDictionary *)remoteNotification withCompletion:(void(^)(WKUserNotificationInterfaceType interface)) completionHandler;
-- (void)didReceiveLocalNotification:(UILocalNotification *)localNotification withCompletion:(void(^)(WKUserNotificationInterfaceType interface)) completionHandler;
+- (void)didReceiveNotification:(UNNotification *)notification withCompletion:(void(^)(WKUserNotificationInterfaceType interface)) completionHandler WK_AVAILABLE_WATCHOS_IOS(3.0, 10.0);
 
-// Subclasses can implement to return an array of suggestions to use as text responses to a remote notification.
-- (nonnull NSArray<NSString *> *)suggestionsForResponseToActionWithIdentifier:(NSString *)identifier forRemoteNotification:(NSDictionary *)remoteNotification inputLanguage:(NSString *)inputLanguage WK_AVAILABLE_WATCHOS_ONLY(2.0);
+// Subclasses can implement to return an array of suggestions to use as text responses to a notification.
+- (nonnull NSArray<NSString *> *)suggestionsForResponseToActionWithIdentifier:(NSString *)identifier forNotification:(UNNotification *)notification inputLanguage:(NSString *)inputLanguage WK_AVAILABLE_WATCHOS_ONLY(3.0);
 
-// Subclasses can implement to return an array of suggestions to use as text responses to a local notification.
-- (nonnull NSArray<NSString *> *)suggestionsForResponseToActionWithIdentifier:(NSString *)identifier forLocalNotification:(UILocalNotification *)localNotification inputLanguage:(NSString *)inputLanguage WK_AVAILABLE_WATCHOS_ONLY(2.0);
+// deprecated
+- (void)didReceiveRemoteNotification:(NSDictionary *)remoteNotification withCompletion:(void(^)(WKUserNotificationInterfaceType interface)) completionHandler WK_DEPRECATED_WATCHOS_IOS(2.0, 3.0, 8.2, 10.0, "use didReceiveNotification:withCompletion:");
+- (void)didReceiveLocalNotification:(UILocalNotification *)localNotification withCompletion:(void(^)(WKUserNotificationInterfaceType interface)) completionHandler WK_DEPRECATED_WATCHOS_IOS(2.0, 3.0, 8.2, 10.0, "use didReceiveNotification:withCompletion:");
+- (nonnull NSArray<NSString *> *)suggestionsForResponseToActionWithIdentifier:(NSString *)identifier forRemoteNotification:(NSDictionary *)remoteNotification inputLanguage:(NSString *)inputLanguage WK_AVAILABLE_WATCHOS_ONLY(2.0) WK_DEPRECATED_WATCHOS(2.0, 3.0, "use suggestionsForResponseToActionWithIdentifier:forNotification:inputLanguage:");
+- (nonnull NSArray<NSString *> *)suggestionsForResponseToActionWithIdentifier:(NSString *)identifier forLocalNotification:(UILocalNotification *)localNotification inputLanguage:(NSString *)inputLanguage WK_AVAILABLE_WATCHOS_ONLY(2.0) WK_DEPRECATED_WATCHOS(2.0, 3.0, "use suggestionsForResponseToActionWithIdentifier:forNotification:inputLanguage:");
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceDevice.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceDevice.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceDevice.h	2015-10-31 03:27:49.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceDevice.h	2016-05-25 05:22:23.000000000 +0200
@@ -37,6 +37,16 @@
     WKInterfaceSemanticContentAttributeForceRightToLeft,
 } WK_AVAILABLE_WATCHOS_ONLY(2.1);
 
+typedef NS_ENUM(NSInteger, WKInterfaceDeviceWristLocation) {
+    WKInterfaceDeviceWristLocationLeft,
+    WKInterfaceDeviceWristLocationRight,
+} WK_AVAILABLE_WATCHOS_ONLY(3.0);
+
+typedef NS_ENUM(NSInteger, WKInterfaceDeviceCrownOrientation) {
+    WKInterfaceDeviceCrownOrientationLeft,
+    WKInterfaceDeviceCrownOrientationRight,
+} WK_AVAILABLE_WATCHOS_ONLY(3.0);
+
 @interface WKInterfaceDevice : NSObject
 
 + (WKInterfaceDevice *)currentDevice;
@@ -52,6 +62,9 @@
 @property (nonatomic, readonly, copy)  NSString *preferredContentSizeCategory;
 @property (nonatomic, readonly) WKInterfaceLayoutDirection layoutDirection WK_AVAILABLE_WATCHOS_ONLY(2.1);
 
+@property (nonatomic,readonly) WKInterfaceDeviceWristLocation wristLocation WK_AVAILABLE_WATCHOS_ONLY(3.0);
+@property (nonatomic,readonly) WKInterfaceDeviceCrownOrientation crownOrientation WK_AVAILABLE_WATCHOS_ONLY(3.0);
+
 + (WKInterfaceLayoutDirection)interfaceLayoutDirectionForSemanticContentAttribute:(WKInterfaceSemanticContentAttribute)semanticContentAttribute WK_AVAILABLE_WATCHOS_ONLY(2.1);
 
 @property(nonatomic, readonly, copy) NSString *systemVersion  WK_AVAILABLE_WATCHOS_IOS(2.0,9.0); // e.g. @"2.0"
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceHMCamera.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceHMCamera.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceHMCamera.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceHMCamera.h	2016-05-25 05:22:23.000000000 +0200
@@ -0,0 +1,19 @@
+//
+//  WKInterfaceHMCamera.h
+//  WatchKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <WatchKit/WatchKit.h>
+#import <HomeKit/HomeKit.h>
+
+@class HMCameraSource;
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+@interface WKInterfaceHMCamera : WKInterfaceObject
+
+// Pass nil to clear out the camera source.
+- (void)setCameraSource:(nullable HMCameraSource *)cameraSource;
+
+@end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceInlineMovie.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceInlineMovie.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceInlineMovie.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceInlineMovie.h	2016-05-25 05:22:23.000000000 +0200
@@ -0,0 +1,33 @@
+//
+//  WKInterfaceInlineMovie.h
+//  WatchKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <WatchKit/WKDefines.h>
+#import <WatchKit/WKInterfaceObject.h>
+
+@class WKImage;
+
+NS_ASSUME_NONNULL_BEGIN
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+
+@interface WKInterfaceInlineMovie : WKInterfaceObject
+
+- (void)setMovieURL:(NSURL *)URL;
+- (void)setVideoGravity:(WKVideoGravity)videoGravity;	// default is WKVideoGravityResizeAspect
+- (void)setLoops:(BOOL)loops;                           // default is NO
+- (void)setAutoplays:(BOOL)autoplays;                   // default is YES
+
+- (void)setPosterImage:(nullable WKImage *)posterImage;
+
+- (void)play;
+- (void)playFromBeginning;
+- (void)pause;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfacePaymentButton.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfacePaymentButton.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfacePaymentButton.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfacePaymentButton.h	2016-05-25 05:22:23.000000000 +0200
@@ -0,0 +1,18 @@
+//
+//  WKInterfacePaymentButton.h
+//  WatchKit
+//
+//  Copyright (c) 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <WatchKit/WKDefines.h>
+#import <WatchKit/WKInterfaceObject.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+@interface WKInterfacePaymentButton : WKInterfaceObject
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceSCNScene.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceSCNScene.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceSCNScene.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceSCNScene.h	2016-05-25 05:22:23.000000000 +0200
@@ -0,0 +1,47 @@
+//
+//  WKInterfaceSCNScene.h
+//  WatchKit
+//
+//  Copyright (c) 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <WatchKit/WKDefines.h>
+#import <WatchKit/WKInterfaceObject.h>
+#import <SceneKit/SceneKit.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+@interface WKInterfaceSCNScene : WKInterfaceObject <SCNSceneRenderer>
+
+/*!
+ @property scene
+ @abstract Specifies the scene of the receiver
+ */
+@property(nonatomic, retain, nullable) SCNScene *scene;
+
+/*!
+ @property snapshot
+ @abstract Draws the contents of the view and returns them as a new image object
+ @discussion This method is thread-safe and may be called at any time.
+ */
+- (UIImage *)snapshot;
+
+/*!
+ @property preferredFramesPerSecond
+ @abstract The rate you want the view to redraw its contents.
+ @discussion When your application sets its preferred frame rate, the view chooses a frame rate as close to that as possible based on the capabilities of the screen the view is displayed on. The actual frame rate chosen is usually a factor of the maximum refresh rate of the screen to provide a consistent frame rate. For example, if the maximum refresh rate of the screen is 60 frames per second, that is also the highest frame rate the view sets as the actual frame rate. However, if you ask for a lower frame rate, it might choose 30, 20, 15 or some other factor to be the actual frame rate. Your application should choose a frame rate that it can consistently maintain.
+ The default value is 0 which means the display link will fire at the native cadence of the display hardware.
+ */
+@property(nonatomic) NSInteger preferredFramesPerSecond;
+
+/*!
+ @property antialiasingMode
+ @abstract Defaults to SCNAntialiasingModeNone.
+ */
+@property(nonatomic) SCNAntialiasingMode antialiasingMode;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceSKScene.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceSKScene.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceSKScene.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceSKScene.h	2016-05-25 05:22:23.000000000 +0200
@@ -0,0 +1,67 @@
+//
+//  WKInterfaceSKScene.h
+//  WatchKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <WatchKit/WKDefines.h>
+#import <WatchKit/WKInterfaceObject.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class SKScene, SKTransition, SKTexture, SKNode;
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+@interface WKInterfaceSKScene : WKInterfaceObject
+
+/**
+ Pause the entire interface
+ */
+@property (nonatomic, getter = isPaused) BOOL paused;
+
+/* Defines the desired rate for interface to render it's content.
+ Actual rate maybe be limited by hardware or other software. */
+@property (nonatomic) NSInteger preferredFramesPerSecond NS_AVAILABLE(10_12, 10_0);
+
+/**
+ Present an SKScene in the interface, replacing the current scene.
+ 
+ @param scene the scene to present.
+ */
+- (void)presentScene:(nullable SKScene *)scene;
+
+/**
+ Present an SKScene in the interface, replacing the current scene.
+ 
+ If there is currently a scene being presented in the interface, the transition is used to swap between them.
+ 
+ @param scene the scene to present.
+ @param transition the transition to use when presenting the scene.
+ */
+- (void)presentScene:(SKScene *)scene transition:(SKTransition *)transition;
+
+/**
+ The currently presented scene, otherwise nil. If in a transition, the 'incoming' scene is returned.
+ */
+@property (nonatomic, readonly, nullable) SKScene *scene;
+
+/**
+ Create an SKTexture containing a snapshot of how it would have been rendered in this interface.
+ The texture is tightly cropped to the size of the node.
+ @param node the node subtree to render to the texture.
+ */
+- (nullable SKTexture *)textureFromNode:(SKNode *)node;
+
+/**
+ Create an SKTexture containing a snapshot of how it would have been rendered in this interface.
+ The texture is cropped to the specified rectangle
+ @param node the node subtree to render to the texture.
+ @param crop the rectangle to crop to
+ */
+- (nullable SKTexture *)textureFromNode:(SKNode *)node crop:(CGRect)crop;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceTable.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceTable.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceTable.h	2015-10-03 02:04:42.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceTable.h	2016-05-25 05:22:23.000000000 +0200
@@ -25,6 +25,8 @@
 
 - (void)scrollToRowAtIndex:(NSInteger)index;
 
+- (void)performSegueForRow:(NSInteger)row WK_AVAILABLE_WATCHOS_ONLY(3.0);
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WatchKit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WatchKit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WatchKit.h	2016-02-25 05:39:03.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WatchKit.h	2016-05-25 05:22:23.000000000 +0200
@@ -19,6 +19,7 @@
 #import <WatchKit/WKInterfaceTimer.h>
 #import <WatchKit/WKInterfaceTable.h>
 #import <WatchKit/WKInterfaceMap.h>
+#import <WatchKit/WKInterfacePaymentButton.h>
 #import <WatchKit/WKInterfaceSeparator.h>
 #import <WatchKit/WKInterfaceSlider.h>
 #import <WatchKit/WKInterfaceSwitch.h>
@@ -30,6 +31,13 @@
 #import <WatchKit/WKAudioFilePlayerItem.h>
 #import <WatchKit/WKInterfaceActivityRing.h>
 #import <WatchKit/WKInterfaceMovie.h>
+#import <WatchKit/WKInterfaceInlineMovie.h>
+#import <WatchKit/WKInterfaceSKScene.h>
+#import <WatchKit/WKInterfaceSCNScene.h>
+#import <WatchKit/WKInterfaceHMCamera.h>
 #import <WatchKit/WKInterfacePicker.h>
 #import <WatchKit/WKAccessibility.h>
+#import <WatchKit/WKGestureRecognizer.h>
+#import <WatchKit/WKCrownSequencer.h>
+#import <WatchKit/WKBackgroundTask.h>
 #endif

```