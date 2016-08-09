#HealthKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKMetadata.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKMetadata.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKMetadata.h	2016-07-25 07:45:47.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKMetadata.h	2016-08-07 06:37:56.000000000 +0200
@@ -257,4 +257,5 @@
  */
 HK_EXTERN NSString * const HKMetadataKeyMenstrualCycleStart HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuery.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuery.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuery.h	2016-07-25 08:13:31.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuery.h	2016-08-07 07:24:52.000000000 +0200
@@ -255,10 +255,11 @@
  
  @param         operatorType    The operator type for the expression.
  @param         totalDistance   The value that the workout's totalEnergyBurned is being compared to. It is the right hand side of the
-                                expression. The unit for this value should be of type Distance
+                                expression. The unit for this value should be of type Distance.
  */
 + (NSPredicate *)predicateForWorkoutsWithOperatorType:(NSPredicateOperatorType)operatorType totalDistance:(HKQuantity *)totalDistance;
 
+
 @end
 
 @interface HKQuery (HKActivitySummaryPredicates)
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkout.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkout.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkout.h	2016-07-25 08:13:31.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkout.h	2016-08-07 06:37:56.000000000 +0200
@@ -164,6 +164,7 @@
  */
 @property (readonly, strong, nullable) HKQuantity *totalDistance;
 
+
 /*!
  @method        workoutWithActivityType:startDate:endDate:
 
@@ -207,7 +208,7 @@
  @param         workoutEvents           An array of HKWorkoutEvents. The workout's duration is derived from these events. (Optional)
  @param         totalEnergyBurned       The amount of energy that was burned during the workout. (Optional)
  @param         totalDistance           The total distance that was traveled during the workout. (Optional)
- @param         device                  The HKDevice associated with the workout (optional).
+ @param         device                  The HKDevice associated with the workout. (Optional)
  @param         metadata                Metadata for the workout. (Optional)
  */
 + (instancetype)workoutWithActivityType:(HKWorkoutActivityType)workoutActivityType
@@ -251,7 +252,7 @@
  @param         duration                The duration of the workout. If 0, the difference between startDate and endDate is used.
  @param         totalEnergyBurned       The amount of energy that was burned during the workout. (Optional)
  @param         totalDistance           The total distance that was traveled during the workout. (Optional)
- @param         device                  The HKDevice associated with the workout (optional).
+ @param         device                  The HKDevice associated with the workout. (Optional)
  @param         metadata                Metadata for the workout. (Optional)
  */
 + (instancetype)workoutWithActivityType:(HKWorkoutActivityType)workoutActivityType
@@ -263,6 +264,7 @@
                                  device:(nullable HKDevice *)device
                                metadata:(nullable NSDictionary<NSString *, id> *)metadata HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
+
 @end
 
 // Predicate Key Paths
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkoutSession.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkoutSession.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkoutSession.h	2016-07-25 07:55:08.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkoutSession.h	2016-08-07 07:24:52.000000000 +0200
@@ -6,6 +6,7 @@
 //
 
 #import <HealthKit/HKWorkout.h>
+#import <HealthKit/HKMetadata.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -54,6 +55,7 @@
  */
 @property (assign) HKWorkoutSessionLocationType locationType;
 
+
 @end
 
 

```