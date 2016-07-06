#CoreMotion.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAccelerometer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAccelerometer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAccelerometer.h	2015-08-15 08:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAccelerometer.h	2016-06-01 05:55:10.000000000 +0200
@@ -9,6 +9,8 @@
 #import <Foundation/Foundation.h>
 #import <CoreMotion/CMLogItem.h>
 
+#import <CoreMotion/CMAvailability.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 /*
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAltimeter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAltimeter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAltimeter.h	2015-08-15 08:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAltimeter.h	2016-06-01 05:55:10.000000000 +0200
@@ -9,6 +9,8 @@
 #import <Foundation/Foundation.h>
 #import <CoreMotion/CMAltitude.h>
 
+#import <CoreMotion/CMAvailability.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 /*
@@ -20,6 +22,15 @@
 typedef void (^CMAltitudeHandler)(CMAltitudeData * __nullable altitudeData, NSError * __nullable error) NS_AVAILABLE(NA,8_0) __TVOS_PROHIBITED;
 
 /*
+ * CMSignificantElevationSampleHandler
+ *
+ * Discussion
+ *   This block type is used to receive significant elevation samples accumulated by user in a given date range.
+ *   An error may be returned if the query fails.
+ */
+typedef void (^CMSignificantElevationSampleHandler)(CMSignificantElevationSample * _Nullable significantElevationSample, NSError * _Nullable error) NS_AVAILABLE(NA,10_0) __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
+
+/*
  *  CMAltimeter
  *
  *  Discussion:
@@ -37,6 +48,14 @@
 + (BOOL)isRelativeAltitudeAvailable;
 
 /*
+ *  isSignificantElevationAvailable
+ *
+ *  Discussion:
+ *		Determines whether the device supports significant elevation changes.
+ */
++ (BOOL)isSignificantElevationAvailable NS_AVAILABLE(NA,10_0) __WATCHOS_PROHIBITED;
+
+/*
  *  startRelativeAltitudeUpdatesToQueue:withHandler:
  *
  *  Discussion:
@@ -57,6 +76,31 @@
  */
 - (void)stopRelativeAltitudeUpdates;
 
+/*
+ *  startSignificantElevationUpdatesWithHandler:
+ *
+ *  Discussion:
+ *    Starts significant elevation updates on a serial queue from the given date.
+ */
+- (void)startSignificantElevationUpdatesWithHandler:(CMSignificantElevationSampleHandler)handler NS_AVAILABLE(NA,10_0) __WATCHOS_PROHIBITED;
+
+/*
+ *  stopSignificantElevationUpdates
+ *
+ *  Discussion:
+ *      Stops significant elevation updates.
+ */
+- (void)stopSignificantElevationUpdates  NS_AVAILABLE(NA,10_0) __WATCHOS_PROHIBITED;
+
+/*
+ *  querySignificantElevationChangeFromDate:fromDate:toDate:withHandler:
+ *
+ *  Discussion:
+ *    Queries significant elevation change for the given date range.
+ *
+ */
+- (void)querySignificantElevationChangeFromDate:(NSDate *)fromDate toDate:(NSDate *)toDate withHandler:(CMSignificantElevationSampleHandler)handler  NS_AVAILABLE(NA,10_0) __WATCHOS_PROHIBITED;
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAltitude.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAltitude.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAltitude.h	2015-08-15 08:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAltitude.h	2016-06-01 05:55:10.000000000 +0200
@@ -9,6 +9,8 @@
 #import <Foundation/Foundation.h>
 #import <CoreMotion/CMLogItem.h>
 
+#import <CoreMotion/CMAvailability.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 /*
@@ -40,4 +42,53 @@
 
 @end
 
+/*
+ *  CMSignificantElevationSample
+ *
+ *  Discussion:
+ *      Contains a significant user elevation change sample.
+ */
+NS_CLASS_AVAILABLE(NA, 10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_PROHIBITED
+@interface CMSignificantElevationSample : NSObject <NSCopying, NSSecureCoding>
+
+/*
+ *  startDate
+ *
+ *  Discussion:
+ *    Start time of period for which the elevation sample is valid.
+ *
+ */
+@property(readonly, nonatomic) NSDate *startDate;
+
+/*
+ *  endDate
+ *
+ *  Discussion:
+ *    End time of period for which the elvation sample is valid.
+ *
+ */
+@property(readonly, nonatomic) NSDate *endDate;
+
+/*
+ *  elevationAscended
+ *
+ *  Discussion:
+ *    Significant elevation ascent in meters.
+ *    Values are accumulated from the start time of updates / query.
+ *
+ */
+@property(readonly, nonatomic) NSNumber *elevationAscended;
+
+/*
+ *  elevationDescended
+ *
+ *  Discussion:
+ *    Significant elevation descent in meters.
+ *    Values are accumulated from the start time of updates / query.
+ *
+ */
+@property(readonly, nonatomic) NSNumber *elevationDescended;
+
+@end
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAttitude.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAttitude.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAttitude.h	2015-08-15 08:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAttitude.h	2016-06-01 05:55:10.000000000 +0200
@@ -8,6 +8,8 @@
 
 #import <Foundation/Foundation.h>
 
+#import <CoreMotion/CMAvailability.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 /*
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAvailability.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAvailability.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAvailability.h	2015-08-15 08:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAvailability.h	2016-06-01 05:55:10.000000000 +0200
@@ -8,14 +8,6 @@
 
 #import <Availability.h>
 
-#ifndef __MAC_TBD
-#define __MAC_TBD __MAC_NA
-#endif
-
-#ifndef __AVAILABILITY_INTERNAL__MAC_TBD
-#define __AVAILABILITY_INTERNAL__MAC_TBD __AVAILABILITY_INTERNAL_UNAVAILABLE
-#endif
-
 #ifdef __cplusplus
 #define CM_EXTERN extern "C" __attribute__((visibility ("default")))
 #else
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMDeviceMotion.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMDeviceMotion.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMDeviceMotion.h	2015-08-15 08:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMDeviceMotion.h	2016-06-01 05:55:10.000000000 +0200
@@ -11,6 +11,8 @@
 #import <CoreMotion/CMGyro.h>
 #import <CoreMotion/CMMagnetometer.h>
 
+#import <CoreMotion/CMAvailability.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 /*
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMGyro.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMGyro.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMGyro.h	2015-08-15 08:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMGyro.h	2016-06-01 05:55:10.000000000 +0200
@@ -9,6 +9,8 @@
 #import <Foundation/Foundation.h>
 #import <CoreMotion/CMLogItem.h>
 
+#import <CoreMotion/CMAvailability.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 /*
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMLogItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMLogItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMLogItem.h	2015-08-15 08:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMLogItem.h	2016-06-01 05:55:10.000000000 +0200
@@ -8,6 +8,8 @@
 
 #import <Foundation/Foundation.h>
 
+#import <CoreMotion/CMAvailability.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 NS_CLASS_AVAILABLE(NA,4_0)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMMagnetometer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMMagnetometer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMMagnetometer.h	2015-08-15 08:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMMagnetometer.h	2016-06-01 05:55:10.000000000 +0200
@@ -9,6 +9,8 @@
 #import <Foundation/Foundation.h>
 #import <CoreMotion/CMLogItem.h>
 
+#import <CoreMotion/CMAvailability.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 /*
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMMotionActivity.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMMotionActivity.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMMotionActivity.h	2015-08-15 08:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMMotionActivity.h	2016-06-01 05:55:10.000000000 +0200
@@ -9,6 +9,8 @@
 #import <Foundation/Foundation.h>
 #import <CoreMotion/CMLogItem.h>
 
+#import <CoreMotion/CMAvailability.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 /*
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMMotionActivityManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMMotionActivityManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMMotionActivityManager.h	2015-08-15 08:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMMotionActivityManager.h	2016-06-01 05:55:10.000000000 +0200
@@ -8,6 +8,8 @@
 #import <Foundation/Foundation.h>
 #import <CoreMotion/CMMotionActivity.h>
 
+#import <CoreMotion/CMAvailability.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 /*
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMMotionManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMMotionManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMMotionManager.h	2015-08-15 08:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMMotionManager.h	2016-06-01 05:03:19.000000000 +0200
@@ -13,6 +13,8 @@
 #import <CoreMotion/CMDeviceMotion.h>
 #import <CoreMotion/CMMagnetometer.h>
 
+#import <CoreMotion/CMAvailability.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 /* 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMPedometer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMPedometer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMPedometer.h	2015-08-15 08:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMPedometer.h	2016-06-01 05:03:06.000000000 +0200
@@ -8,6 +8,8 @@
 
 #import <Foundation/Foundation.h>
 
+#import <CoreMotion/CMAvailability.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 /*
@@ -108,6 +110,64 @@
  */
 @property(readonly, nonatomic, nullable) NSNumber *currentCadence NS_AVAILABLE(NA,9_0);
 
+/*
+ * averageActivePace
+ *
+ *
+ * Discussion:
+ *
+ *      For updates this returns the average active pace since
+ *      startPedometerUpdatesFromDate:withHandler:, in s/m (seconds per meter).
+ *      For historical queries this returns average active pace between startDate
+ *      and endDate. The average active pace omits the non-active time, giving
+ *      the average pace from when the user was moving. Value is nil if any of
+ *      the following are true:
+ *
+ *         (1) (For historical queries) this information is not available,
+ *             e.g. the user did not move between startDate and endDate;
+ *         (2) Unsupported platform.
+ *
+ */
+@property(readonly, nonatomic, nullable) NSNumber *averageActivePace NS_AVAILABLE(NA,10_0);
+
+@end
+
+/*
+ *  CMPedometerEventType
+ *
+ *  Discussion:
+ *      Events describing the transitions of pedestrian activity.
+ */
+typedef NS_ENUM(NSInteger, CMPedometerEventType) {
+	CMPedometerEventTypePause,
+	CMPedometerEventTypeResume
+} NS_ENUM_AVAILABLE(NA, 10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_PROHIBITED;
+
+/*
+ *  CMPedometerEvent
+ *
+ *  Discussion:
+ *      An event marking the change in user's pedestrian activity.
+ */
+NS_CLASS_AVAILABLE(NA, 10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_PROHIBITED
+@interface CMPedometerEvent : NSObject <NSSecureCoding, NSCopying>
+
+/*
+ *  date
+ *
+ *  Discussion:
+ *      The time of occurence of event.
+ */
+@property(readonly, nonatomic) NSDate *date;
+
+/*
+ *  type
+ *
+ *  Discussion:
+ *      Event type describing the transition of pedestrian activity.
+ */
+@property(readonly, nonatomic) CMPedometerEventType type;
+
 @end
 
 /*
@@ -120,6 +180,15 @@
 typedef void (^CMPedometerHandler)(CMPedometerData * __nullable pedometerData, NSError * __nullable error) __TVOS_PROHIBITED;
 
 /*
+ *  CMPedometerEventHandler
+ *
+ *  Discussion:
+ *      Typedef of block that will be invoked when pedometer event is available.
+ *      Error types are defined in "CMError.h".
+ */
+typedef void (^CMPedometerEventHandler)(CMPedometerEvent * __nullable pedometerEvent, NSError * __nullable error) NS_AVAILABLE(NA, 10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_PROHIBITED;
+
+/*
  *  CMPedometer
  *
  *  Discussion:
@@ -183,6 +252,14 @@
 + (BOOL)isCadenceAvailable NS_AVAILABLE(NA,9_0);
 
 /*
+ *  isPedometerEventTrackingAvailable
+ *
+ *  Discussion:
+ *      Determines whether the device supports pedometer events.
+ */
++ (BOOL)isPedometerEventTrackingAvailable NS_AVAILABLE(NA,10_0) __WATCHOS_AVAILABLE(3_0);
+
+/*
  *  queryPedometerDataFromDate:toDate:withHandler:
  *
  *  Discussion:
@@ -219,6 +296,23 @@
  */
 - (void)stopPedometerUpdates;
 
+/*
+ *  startPedometerEventUpdatesWithHandler:
+ *
+ *  Discussion:
+ *      Starts pedometer event updates on a serial queue.
+ *      Events are available only when the apps are running in foreground / background.
+ */
+- (void)startPedometerEventUpdatesWithHandler:(CMPedometerEventHandler)handler NS_AVAILABLE(NA,10_0) __WATCHOS_AVAILABLE(3_0);
+
+/*
+ *  stopPedometerEventUpdates
+ *
+ *  Discussion:
+ *      Stops pedometer event updates.
+ */
+- (void)stopPedometerEventUpdates NS_AVAILABLE(NA,10_0) __WATCHOS_AVAILABLE(3_0);
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMSensorRecorder.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMSensorRecorder.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMSensorRecorder.h	2016-03-03 03:44:03.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMSensorRecorder.h	2016-06-01 05:55:10.000000000 +0200
@@ -9,6 +9,8 @@
 #import <Foundation/Foundation.h>
 #import <CoreMotion/CMAccelerometer.h>
 
+#import <CoreMotion/CMAvailability.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 /*
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMStepCounter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMStepCounter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMStepCounter.h	2015-08-15 08:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMStepCounter.h	2016-06-01 05:55:10.000000000 +0200
@@ -8,6 +8,8 @@
 
 #import <Foundation/Foundation.h>
 
+#import <CoreMotion/CMAvailability.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 /*
@@ -98,3 +100,4 @@
 @end
 
 NS_ASSUME_NONNULL_END
+

```