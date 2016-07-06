#CoreMotion.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAltimeter.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAltimeter.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAltimeter.h	2016-06-01 05:03:19.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAltimeter.h	2016-06-27 07:31:50.000000000 +0200
@@ -8,7 +8,6 @@
 
 #import <Foundation/Foundation.h>
 #import <CoreMotion/CMAltitude.h>
-
 #import <CoreMotion/CMAvailability.h>
 
 NS_ASSUME_NONNULL_BEGIN
@@ -22,15 +21,6 @@
 typedef void (^CMAltitudeHandler)(CMAltitudeData * __nullable altitudeData, NSError * __nullable error) NS_AVAILABLE(NA,8_0) __TVOS_PROHIBITED;
 
 /*
- * CMSignificantElevationSampleHandler
- *
- * Discussion
- *   This block type is used to receive significant elevation samples accumulated by user in a given date range.
- *   An error may be returned if the query fails.
- */
-typedef void (^CMSignificantElevationSampleHandler)(CMSignificantElevationSample * _Nullable significantElevationSample, NSError * _Nullable error) NS_AVAILABLE(NA,10_0) __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
-
-/*
  *  CMAltimeter
  *
  *  Discussion:
@@ -48,14 +38,6 @@
 + (BOOL)isRelativeAltitudeAvailable;
 
 /*
- *  isSignificantElevationAvailable
- *
- *  Discussion:
- *		Determines whether the device supports significant elevation changes.
- */
-+ (BOOL)isSignificantElevationAvailable NS_AVAILABLE(NA,10_0) __WATCHOS_PROHIBITED;
-
-/*
  *  startRelativeAltitudeUpdatesToQueue:withHandler:
  *
  *  Discussion:
@@ -76,31 +58,6 @@
  */
 - (void)stopRelativeAltitudeUpdates;
 
-/*
- *  startSignificantElevationUpdatesWithHandler:
- *
- *  Discussion:
- *    Starts significant elevation updates on a serial queue from the given date.
- */
-- (void)startSignificantElevationUpdatesWithHandler:(CMSignificantElevationSampleHandler)handler NS_AVAILABLE(NA,10_0) __WATCHOS_PROHIBITED;
-
-/*
- *  stopSignificantElevationUpdates
- *
- *  Discussion:
- *      Stops significant elevation updates.
- */
-- (void)stopSignificantElevationUpdates  NS_AVAILABLE(NA,10_0) __WATCHOS_PROHIBITED;
-
-/*
- *  querySignificantElevationChangeFromDate:fromDate:toDate:withHandler:
- *
- *  Discussion:
- *    Queries significant elevation change for the given date range.
- *
- */
-- (void)querySignificantElevationChangeFromDate:(NSDate *)fromDate toDate:(NSDate *)toDate withHandler:(CMSignificantElevationSampleHandler)handler  NS_AVAILABLE(NA,10_0) __WATCHOS_PROHIBITED;
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAltitude.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAltitude.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAltitude.h	2016-06-01 05:03:19.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMAltitude.h	2016-06-27 07:31:50.000000000 +0200
@@ -8,7 +8,6 @@
 
 #import <Foundation/Foundation.h>
 #import <CoreMotion/CMLogItem.h>
-
 #import <CoreMotion/CMAvailability.h>
 
 NS_ASSUME_NONNULL_BEGIN
@@ -42,53 +41,4 @@
 
 @end
 
-/*
- *  CMSignificantElevationSample
- *
- *  Discussion:
- *      Contains a significant user elevation change sample.
- */
-NS_CLASS_AVAILABLE(NA, 10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_PROHIBITED
-@interface CMSignificantElevationSample : NSObject <NSCopying, NSSecureCoding>
-
-/*
- *  startDate
- *
- *  Discussion:
- *    Start time of period for which the elevation sample is valid.
- *
- */
-@property(readonly, nonatomic) NSDate *startDate;
-
-/*
- *  endDate
- *
- *  Discussion:
- *    End time of period for which the elvation sample is valid.
- *
- */
-@property(readonly, nonatomic) NSDate *endDate;
-
-/*
- *  elevationAscended
- *
- *  Discussion:
- *    Significant elevation ascent in meters.
- *    Values are accumulated from the start time of updates / query.
- *
- */
-@property(readonly, nonatomic) NSNumber *elevationAscended;
-
-/*
- *  elevationDescended
- *
- *  Discussion:
- *    Significant elevation descent in meters.
- *    Values are accumulated from the start time of updates / query.
- *
- */
-@property(readonly, nonatomic) NSNumber *elevationDescended;
-
-@end
-
 NS_ASSUME_NONNULL_END

```