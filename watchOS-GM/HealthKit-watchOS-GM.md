#HealthKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKMetadata.h /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKMetadata.h
--- /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKMetadata.h	2016-08-09 23:13:46.000000000 -0500
+++ /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKMetadata.h	2016-08-06 23:32:51.000000000 -0500
@@ -257,5 +257,53 @@
  */
 HK_EXTERN NSString * const HKMetadataKeyMenstrualCycleStart HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
+/*!
+ @constant      HKMetadataKeyLapLength
+ @abstract      Represents the length of a lap recorded during a workout.
+ @discussion    The expected value type is an HKQuantity object compatible with a length unit. This key may be set on an
+                HKWorkout object to represent the length of a lap.
+ */
+HK_EXTERN NSString * const HKMetadataKeyLapLength HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
+
+/*!
+ @enum          HKWorkoutSwimmingLocationType
+ @abstract      This enumerated type is used to represent the location type of a swimming workout.
+ @discussion    This value indicates whether a swimming workout was performed in a pool or open water.
+ */
+typedef NS_ENUM(NSInteger, HKWorkoutSwimmingLocationType) {
+    HKWorkoutSwimmingLocationTypeUnknown = 0,
+    HKWorkoutSwimmingLocationTypePool,
+    HKWorkoutSwimmingLocationTypeOpenWater,
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
+
+/*!
+ @constant      HKMetadataKeySwimmingLocationType
+ @abstract      Represents the location type of a swimming workout.
+ @discussion    The expected value type is an NSNumber containing an HKWorkoutSwimmingLocationType value. This key may
+                be set on an HKWorkout object to represent the swimming location type.
+ */
+HK_EXTERN NSString * const HKMetadataKeySwimmingLocationType HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
+
+/*!
+ @enum          HKSwimmingStrokeStyle
+ @abstract      Represents a style of stroke used during a swimming workout.
+ */
+typedef NS_ENUM(NSInteger, HKSwimmingStrokeStyle) {
+    HKSwimmingStrokeStyleUnknown = 0,
+    HKSwimmingStrokeStyleMixed,
+    HKSwimmingStrokeStyleFreestyle,
+    HKSwimmingStrokeStyleBackstroke,
+    HKSwimmingStrokeStyleBreaststroke,
+    HKSwimmingStrokeStyleButterfly,
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
+
+/*!
+ @constant      HKMetadataKeySwimmingStrokeStyle
+ @abstract      Represents the predominant stroke style during a lap of a swimming workout.
+ @discussion    The expected value type is an NSNumber containing an HKSwimmingStrokeStyle value. This key may be set on
+                an HKWorkoutEvent object with the type HKWorkoutEventTypeLap to represent the predominant style used
+                during the lap.
+ */
+HK_EXTERN NSString * const HKMetadataKeySwimmingStrokeStyle HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuery.h /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuery.h
--- /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuery.h	2016-08-09 23:11:50.000000000 -0500
+++ /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuery.h	2016-08-06 23:29:55.000000000 -0500
@@ -259,6 +259,17 @@
  */
 + (NSPredicate *)predicateForWorkoutsWithOperatorType:(NSPredicateOperatorType)operatorType totalDistance:(HKQuantity *)totalDistance;
 
+/*!
+ @method        predicateForWorkoutsWithOperatorType:totalSwimmingStrokeCount:
+ @abstract      Creates a predicate for use with HKQuery subclasses.
+ @discussion    Creates a query predicate that matches HKWorkouts by the given operator type and totalSwimmingStrokeCount
+ 
+ @param         operatorType                The operator type for the expression.
+ @param         totalSwimmingStrokeCount    The value that the workout's totalSwimmingStrokeCount is being compared to.
+                                            It is the right hand side of the expression. The unit for this value should
+                                            be of type Count.
+ */
++ (NSPredicate *)predicateForWorkoutsWithOperatorType:(NSPredicateOperatorType)operatorType totalSwimmingStrokeCount:(HKQuantity *)totalSwimmingStrokeCount;
 
 @end
 
diff -ruN /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKTypeIdentifiers.h /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKTypeIdentifiers.h
--- /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKTypeIdentifiers.h	2016-08-06 23:38:37.000000000 -0500
+++ /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKTypeIdentifiers.h	2016-08-09 22:26:38.000000000 -0500
@@ -34,6 +34,8 @@
 HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierNikeFuel HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);                  // Scalar(Count),               Cumulative
 HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierAppleExerciseTime HK_AVAILABLE_IOS_WATCHOS(9_3, 2_2);         // Time                         Cumulative
 HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierPushCount HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);                // Scalar(Count),               Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDistanceSwimming HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);         // Length,                      Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierSwimmingStrokeCount HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);      // Scalar(Count),               Cumulative
 
 // Vitals
 HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierHeartRate HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);                 // Scalar(Count)/Time,          Discrete
diff -ruN /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkout.h /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkout.h
--- /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkout.h	2016-08-06 23:37:56.000000000 -0500
+++ /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkout.h	2016-08-09 22:26:38.000000000 -0500
@@ -164,6 +164,13 @@
  */
 @property (readonly, strong, nullable) HKQuantity *totalDistance;
 
+/*!
+ @property      totalSwimmingStrokeCount
+ @abstract      The total count of swimming strokes that was accumulated during a workout
+ @discussion    This metric should represent the total count of swimming strokes accumulated during the course of the
+                workout. It should be a quantity with a unit representing count.
+ */
+@property (readonly, strong, nullable) HKQuantity *totalSwimmingStrokeCount HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
 
 /*!
  @method        workoutWithActivityType:startDate:endDate:
@@ -264,6 +271,30 @@
                                  device:(nullable HKDevice *)device
                                metadata:(nullable NSDictionary<NSString *, id> *)metadata HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
+/*!
+ @method        workoutWithActivityType:startDate:endDate:workoutEvents:totalEnergyBurned:totalDistance:totalSwimmingStrokeCount:device:metadata:
+ @discussion    If the optional total parameters are specified, matching samples that add up to the calculated total quantities
+                should be associated with this workout using addSamples:toWorkout:completion: in HKHealthStore.
+ 
+ @param         workoutActivityType         The activity type of the workout
+ @param         startDate                   The point in time that the workout was started
+ @param         endDate                     The point in time that the workout was ended
+ @param         workoutEvents               An array of HKWorkoutEvents. The workout's duration is derived from these events. (Optional)
+ @param         totalEnergyBurned           The amount of energy that was burned during the workout. (Optional)
+ @param         totalDistance               The total distance that was traveled during the workout. (Optional)
+ @param         totalSwimmingStrokeCount    The total count of swimming strokes that was accumulated during the workout. (Optional)
+ @param         device                      The HKDevice associated with the workout. (Optional)
+ @param         metadata                    Metadata for the workout. (Optional)
+ */
++ (instancetype)workoutWithActivityType:(HKWorkoutActivityType)workoutActivityType
+                              startDate:(NSDate *)startDate
+                                endDate:(NSDate *)endDate
+                          workoutEvents:(nullable NSArray<HKWorkoutEvent *> *)workoutEvents
+                      totalEnergyBurned:(nullable HKQuantity *)totalEnergyBurned
+                          totalDistance:(nullable HKQuantity *)totalDistance
+               totalSwimmingStrokeCount:(nullable HKQuantity *)totalSwimmingStrokeCount
+                                 device:(nullable HKDevice *)device
+                               metadata:(nullable NSDictionary<NSString *, id> *)metadata HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
 
 @end
 
@@ -272,10 +303,12 @@
 HK_EXTERN NSString * const HKPredicateKeyPathWorkoutTotalDistance HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 HK_EXTERN NSString * const HKPredicateKeyPathWorkoutTotalEnergyBurned HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 HK_EXTERN NSString * const HKPredicateKeyPathWorkoutType HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
+HK_EXTERN NSString * const HKPredicateKeyPathWorkoutTotalSwimmingStrokeCount HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
 
 // Sort Identifiers
 HK_EXTERN NSString * const HKWorkoutSortIdentifierDuration HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 HK_EXTERN NSString * const HKWorkoutSortIdentifierTotalDistance HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 HK_EXTERN NSString * const HKWorkoutSortIdentifierTotalEnergyBurned HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
+HK_EXTERN NSString * const HKWorkoutSortIdentifierTotalSwimmingStrokeCount HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkoutSession.h /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkoutSession.h
--- /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkoutSession.h	2016-08-06 23:38:37.000000000 -0500
+++ /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkoutSession.h	2016-08-09 22:26:23.000000000 -0500
@@ -55,6 +55,19 @@
  */
 @property (assign) HKWorkoutSessionLocationType locationType;
 
+/*!
+ @property      swimmingLocationType
+ @abstract      Indicates the type of swimming location (pool vs. open water) where the workout will take place.
+ */
+@property (assign) HKWorkoutSwimmingLocationType swimmingLocationType;
+
+/*!
+ @property      lapLength
+ @abstract      Indicates the length of the pool, when the workout location type is pool.
+ @discussion    This metric represents the length of the pool where the workout takes place. It should be a quantity with
+                a unit representing length.
+ */
+@property (copy, nullable) HKQuantity *lapLength;
 
 @end
 

```