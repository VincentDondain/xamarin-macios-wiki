#HealthKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkout.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkout.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkout.h	2016-07-11 07:19:32.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkout.h	2016-07-25 08:13:31.000000000 +0200
@@ -106,7 +106,7 @@
  @abstract      Represents a particular event that occurred during a workout
  */
 HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
-@interface HKWorkoutEvent : NSObject <NSSecureCoding>
+@interface HKWorkoutEvent : NSObject <NSSecureCoding, NSCopying>
 
 @property (readonly, assign) HKWorkoutEventType type;
 @property (readonly, copy) NSDate *date;

```