#CoreLocation.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLAvailability.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLAvailability.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLAvailability.h	2015-08-23 02:48:53.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLAvailability.h	2016-05-16 02:07:13.000000000 +0200
@@ -14,10 +14,20 @@
 
 #import <Availability.h>
 
+#ifndef __TVOS_PROHIBITED
+#define __TVOS_PROHIBITED
+#endif
+
+#ifndef __WATCHOS_PROHIBITED
+#define __WATCHOS_PROHIBITED
+#endif
+
+#ifndef CL_MAC_CODEBASE
+#define CL_MAC_CODEBASE !TARGET_OS_IPHONE
+#endif
 
 #ifdef __cplusplus
 #define CL_EXTERN extern "C" __attribute__((visibility ("default")))
 #else
 #define CL_EXTERN extern __attribute__((visibility ("default")))
 #endif
-
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLBeaconRegion.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLBeaconRegion.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLBeaconRegion.h	2015-08-23 02:48:53.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLBeaconRegion.h	2016-06-01 05:02:52.000000000 +0200
@@ -44,7 +44,7 @@
  *    value.
  *
  */
-NS_CLASS_AVAILABLE(NA, 7_0)
+NS_CLASS_AVAILABLE(NA, 7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
 @interface CLBeaconRegion : CLRegion
 
 /*
@@ -87,7 +87,7 @@
  *    If not specified, it will default to a pre-determined value for the device.
  *
  */
-- (NSMutableDictionary *)peripheralDataWithMeasuredPower:(nullable NSNumber *)measuredPower;
+- (NSMutableDictionary<NSString *, id> *)peripheralDataWithMeasuredPower:(nullable NSNumber *)measuredPower;
 
 /*
  *  proximityUUID
@@ -136,7 +136,7 @@
  *    A single beacon within a CLBeaconRegion.
  *
  */
-NS_CLASS_AVAILABLE(NA, 7_0)
+NS_CLASS_AVAILABLE(NA, 7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
 @interface CLBeacon : NSObject <NSCopying, NSSecureCoding>
 {
 	CLBeaconInternal *_internal;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLError.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLError.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLError.h	2015-08-23 02:48:53.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLError.h	2016-05-16 02:07:13.000000000 +0200
@@ -1,4 +1,3 @@
-
 /*
  *  CLError.h
  *  CoreLocation
@@ -46,6 +45,6 @@
  *    When an error with code kCLErrorRegionMonitoringResponseDelayed is received, this key may be populated
  *    in the userInfo dictionary.  The value is a CLRegion that the location service can more effectively monitor.
  */
-extern NSString *const kCLErrorUserInfoAlternateRegionKey NS_AVAILABLE(10_7, 5_0);
+extern NSString *const kCLErrorUserInfoAlternateRegionKey NS_AVAILABLE(10_7, 5_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLErrorDomain.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLErrorDomain.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLErrorDomain.h	2015-08-23 02:48:53.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLErrorDomain.h	2016-05-16 02:07:13.000000000 +0200
@@ -1,4 +1,3 @@
-
 /*
  *  CLErrorDomain.h
  *  CoreLocation
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLHeading.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLHeading.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLHeading.h	2015-08-23 02:48:53.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLHeading.h	2016-05-16 02:07:13.000000000 +0200
@@ -1,4 +1,3 @@
-
 /*
  *  CLHeading.h
  *  CoreLocation
@@ -38,7 +37,7 @@
  *  Discussion:
  *    Represents a vector pointing to magnetic North constructed from axis component values x, y, and z. An accuracy of the heading calculation is also provided along with timestamp information.
  */
-NS_CLASS_AVAILABLE(10_7, 3_0)
+NS_CLASS_AVAILABLE(10_7, 3_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
 @interface CLHeading : NSObject <NSCopying, NSSecureCoding>
 {
 @private
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocation.h	2015-08-23 02:48:53.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocation.h	2016-05-22 06:00:55.000000000 +0200
@@ -147,6 +147,30 @@
 #endif
 
 /*
+ *  CLFloor
+ *
+ *  Discussion:
+ *    Encapsulates the information about a floor.
+ */
+NS_CLASS_AVAILABLE(NA, 8_0)
+@interface CLFloor : NSObject <NSCopying, NSSecureCoding>
+
+/*
+ *  level
+ *
+ *  Discussion:
+ *    This is a logical representation that will vary on definition from building-to-building.
+ *    Floor 0 will always represent the floor designated as "ground".
+ *    This number may be negative to designate floors below the ground floor
+ *    and positive to indicate floors above the ground floor.
+ *    It is not intended to match any numbering that might actually be used in the building.
+ *    It is erroneous to use as an estimate of altitude.
+ */
+@property(readonly, nonatomic) NSInteger level;
+
+@end
+
+/*
  *  CLLocation
  *  
  *  Discussion:
@@ -235,7 +259,7 @@
  *  Range:
  *    0.0 - 359.9 degrees, 0 being true North
  */
-@property(readonly, nonatomic) CLLocationDirection course __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_2_2);
+@property(readonly, nonatomic) CLLocationDirection course __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_2_2) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  speed
@@ -243,7 +267,7 @@
  *  Discussion:
  *    Returns the speed of the location in m/s. Negative if speed is invalid.
  */
-@property(readonly, nonatomic) CLLocationSpeed speed __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_2_2);
+@property(readonly, nonatomic) CLLocationSpeed speed __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_2_2) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  timestamp
@@ -254,6 +278,16 @@
 @property(readonly, nonatomic, copy) NSDate *timestamp;
 
 /*
+ *  floor
+ *
+ *  Discussion:
+ *    Contains information about the logical floor that you are on
+ *    in the current building if you are inside a supported venue.
+ *    This will be nil if the floor is unavailable.
+ */
+@property(readonly, nonatomic, copy, nullable) CLFloor *floor __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_8_0);
+
+/*
  *  description
  *  
  *  Discussion:
@@ -267,7 +301,7 @@
  *  Discussion:
  *    Deprecated. Use -distanceFromLocation: instead.
  */
-- (CLLocationDistance)getDistanceFrom:(const CLLocation *)location __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_NA,__MAC_NA,__IPHONE_2_0,__IPHONE_3_2);
+- (CLLocationDistance)getDistanceFrom:(const CLLocation *)location __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_NA,__MAC_NA,__IPHONE_2_0,__IPHONE_3_2) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  distanceFromLocation:
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager+CLVisitExtensions.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager+CLVisitExtensions.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager+CLVisitExtensions.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager+CLVisitExtensions.h	2016-05-16 02:07:13.000000000 +0200
@@ -0,0 +1,47 @@
+/*
+ *  CLLocationManager+CLVisitExtensions.h
+ *  CoreLocation
+ *
+ *  Copyright (c) 2014 Apple Inc. All rights reserved.
+ *
+ */
+
+#import <CoreLocation/CLLocationManager.h>
+
+#import <CoreLocation/CLAvailability.h>
+#if !CL_MAC_CODEBASE // whole file
+
+NS_ASSUME_NONNULL_BEGIN
+
+@interface CLLocationManager (CLVisitExtensions)
+
+/*
+ *  startMonitoringVisits
+ *
+ *  Discussion:
+ *    Begin monitoring for visits.  All CLLLocationManagers allocated by your
+ *    application, both current and future, will deliver detected visits to
+ *    their delegates.  This will continue until -stopMonitoringVisits is sent
+ *    to any such CLLocationManager, even across application relaunch events.
+ *
+ *    Detected visits are sent to the delegate's -locationManager:didVisit:
+ *    method.
+ */
+- (void)startMonitoringVisits NS_AVAILABLE(NA, 8_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+
+/*
+ *  stopMonitoringVisits
+ *
+ *  Discussion:
+ *    Stop monitoring for visits.  To resume visit monitoring, send
+ *    -startMonitoringVisits.
+ *
+ *    Note that stopping and starting are asynchronous operations and may not
+ *    immediately reflect in delegate callback patterns.
+ */
+- (void)stopMonitoringVisits NS_AVAILABLE(NA, 8_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+
+@end
+
+NS_ASSUME_NONNULL_END
+#endif // whole file
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager.h	2015-08-23 02:48:53.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager.h	2016-06-01 05:54:00.000000000 +0200
@@ -1,4 +1,3 @@
-
 /*
  *  CLLocationManager.h
  *  CoreLocation
@@ -39,13 +38,39 @@
  *      
  */
 typedef NS_ENUM(int, CLAuthorizationStatus) {
-    kCLAuthorizationStatusNotDetermined = 0, // User has not yet made a choice with regards to this application
-    kCLAuthorizationStatusRestricted,        // This application is not authorized to use location services.  Due
-                                             // to active restrictions on location services, the user cannot change
-                                             // this status, and may not have personally denied authorization
-    kCLAuthorizationStatusDenied,            // User has explicitly denied authorization for this application, or
-                                             // location services are disabled in Settings
-    kCLAuthorizationStatusAuthorized         // User has authorized this application to use location services
+	// User has not yet made a choice with regards to this application
+	kCLAuthorizationStatusNotDetermined = 0,
+
+	// This application is not authorized to use location services.  Due
+	// to active restrictions on location services, the user cannot change
+	// this status, and may not have personally denied authorization
+	kCLAuthorizationStatusRestricted,
+
+	// User has explicitly denied authorization for this application, or
+	// location services are disabled in Settings.
+	kCLAuthorizationStatusDenied,
+
+	// User has granted authorization to use their location at any time,
+	// including monitoring for regions, visits, or significant location changes.
+	//
+	// This value should be used on iOS, tvOS and watchOS.  It is available on
+	// MacOS, but kCLAuthorizationStatusAuthorized is synonymous and preferred.
+	kCLAuthorizationStatusAuthorizedAlways NS_ENUM_AVAILABLE(10_12, 8_0),
+
+	// User has granted authorization to use their location only when your app
+	// is visible to them (it will be made visible to them if you continue to
+	// receive location updates while in the background).  Authorization to use
+	// launch APIs has not been granted.
+	//
+	// This value is not available on MacOS.  It should be used on iOS, tvOS and
+	// watchOS.
+	kCLAuthorizationStatusAuthorizedWhenInUse NS_ENUM_AVAILABLE(NA, 8_0),
+
+	// User has authorized this application to use location services.
+	//
+	// This value is deprecated or prohibited on iOS, tvOS and watchOS.
+	// It should be used on MacOS.
+	kCLAuthorizationStatusAuthorized NS_ENUM_DEPRECATED(10_6, NA, 2_0, 8_0, "Use kCLAuthorizationStatusAuthorizedAlways") __TVOS_PROHIBITED __WATCHOS_PROHIBITED = kCLAuthorizationStatusAuthorizedAlways
 };
 
 /*
@@ -65,9 +90,7 @@
 
 @class CLLocation;
 @class CLHeading;
-#if TARGET_OS_IPHONE
 @class CLBeaconRegion;
-#endif
 @protocol CLLocationManagerDelegate;
 
 /*
@@ -99,7 +122,7 @@
  *  Discussion:
  *      Returns YES if the device supports the heading service, otherwise NO.
  */
-+ (BOOL)headingAvailable __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_4_0);
++ (BOOL)headingAvailable __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  significantLocationChangeMonitoringAvailable
@@ -107,7 +130,7 @@
  *  Discussion:
  *      Returns YES if the device supports significant location change monitoring, otherwise NO.
  */
-+ (BOOL)significantLocationChangeMonitoringAvailable __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_4_0);
++ (BOOL)significantLocationChangeMonitoringAvailable __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  isMonitoringAvailableForClass:
@@ -116,7 +139,7 @@
  *      Determines whether the device supports monitoring for the specified type of region.
  *      If NO, all attempts to monitor the specified type of region will fail.
  */
-+ (BOOL)isMonitoringAvailableForClass:(Class)regionClass __OSX_AVAILABLE_STARTING(__MAC_10_10,__IPHONE_7_0);
++ (BOOL)isMonitoringAvailableForClass:(Class)regionClass __OSX_AVAILABLE_STARTING(__MAC_10_10,__IPHONE_7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  regionMonitoringAvailable
@@ -124,7 +147,7 @@
  *  Discussion:
  *      Deprecated. Use +isMonitoringAvailableForClass: instead.
  */
-+ (BOOL)regionMonitoringAvailable __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_8,__MAC_10_10,__IPHONE_4_0,__IPHONE_7_0);
++ (BOOL)regionMonitoringAvailable __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_8,__MAC_10_10,__IPHONE_4_0,__IPHONE_7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  regionMonitoringEnabled
@@ -132,7 +155,7 @@
  *  Discussion:
  *      Deprecated. Use +isMonitoringAvailableForClass: and +authorizationStatus instead.
  */
-+ (BOOL)regionMonitoringEnabled __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_8, __MAC_10_10,__IPHONE_4_0, __IPHONE_6_0);
++ (BOOL)regionMonitoringEnabled __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_8, __MAC_10_10,__IPHONE_4_0, __IPHONE_6_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  isRangingAvailable
@@ -141,7 +164,7 @@
  *      Determines whether the device supports ranging.
  *      If NO, all attempts to range beacons will fail.
  */
-+ (BOOL)isRangingAvailable __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_7_0);
++ (BOOL)isRangingAvailable __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  authorizationStatus
@@ -159,7 +182,7 @@
  *  Discussion:
  *      Deprecated. Use +locationServicesEnabled instead.
  */
-@property(readonly, nonatomic) BOOL locationServicesEnabled __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_NA,__MAC_NA,__IPHONE_2_0,__IPHONE_4_0);
+@property(readonly, nonatomic) BOOL locationServicesEnabled __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_NA,__MAC_NA,__IPHONE_2_0,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  purpose
@@ -171,7 +194,7 @@
  *
  *      Deprecated.  Set the purpose string in Info.plist using key NSLocationUsageDescription.
  */
-@property(copy, nonatomic, nullable) NSString *purpose __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7, __MAC_NA, __IPHONE_3_2, __IPHONE_6_0);
+@property(copy, nonatomic, nullable) NSString *purpose __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7, __MAC_NA, __IPHONE_3_2, __IPHONE_6_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *	activityType
@@ -181,7 +204,7 @@
  *		the determination of when location updates may be automatically paused.
  *		By default, CLActivityTypeOther is used.
  */
-@property(assign, nonatomic) CLActivityType activityType __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_6_0);
+@property(assign, nonatomic) CLActivityType activityType __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_6_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  distanceFilter
@@ -202,7 +225,7 @@
  *      power performance, be sure to specify an appropriate accuracy for your usage scenario (eg,
  *      use a large accuracy value when only a coarse location is needed). Use kCLLocationAccuracyBest to
  *      achieve the best possible accuracy. Use kCLLocationAccuracyBestForNavigation for navigation.
- *      By default, kCLLocationAccuracyBest is used.
+ *      The default value varies by platform.
  */
 @property(assign, nonatomic) CLLocationAccuracy desiredAccuracy;
 
@@ -213,7 +236,33 @@
  *		Specifies that location updates may automatically be paused when possible.
  *		By default, this is YES for applications linked against iOS 6.0 or later.
  */
-@property(assign, nonatomic) BOOL pausesLocationUpdatesAutomatically __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_6_0);
+@property(assign, nonatomic) BOOL pausesLocationUpdatesAutomatically __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_6_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+
+/*
+ *  allowsBackgroundLocationUpdates
+ *
+ *  Discussion:
+ *      By default, this is NO for applications linked against iOS 9.0 or later,
+ *      regardless of minimum deployment target.
+ *
+ *      With UIBackgroundModes set to include "location" in Info.plist, you must
+ *      also set this property to YES at runtime whenever calling
+ *      -startUpdatingLocation with the intent to continue in the background.
+ *
+ *      Setting this property to YES when UIBackgroundModes does not include
+ *      "location" is a fatal error.
+ *
+ *      Resetting this property to NO is equivalent to omitting "location" from
+ *      the UIBackgroundModes value.  Access to location is still permitted
+ *      whenever the application is running (ie not suspended), and has
+ *      sufficient authorization (ie it has WhenInUse authorization and is in
+ *      use, or it has Always authorization).  However, the app will still be
+ *      subject to the usual task suspension rules.
+ *
+ *      See -requestWhenInUseAuthorization and -requestAlwaysAuthorization for
+ *      more details on possible authorization values.
+ */
+@property(assign, nonatomic) BOOL allowsBackgroundLocationUpdates __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_9_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  location
@@ -229,7 +278,7 @@
  *  Discussion:
  *      Deprecated. Use +headingAvailable instead.
  */
-@property(readonly, nonatomic) BOOL headingAvailable __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_NA,__MAC_NA,__IPHONE_3_0,__IPHONE_4_0);
+@property(readonly, nonatomic) BOOL headingAvailable __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_NA,__MAC_NA,__IPHONE_3_0,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  headingFilter
@@ -239,7 +288,7 @@
  *      be notified of updates less than the stated filter value. Pass in kCLHeadingFilterNone to be
  *      notified of all updates. By default, 1 degree is used.
  */
-@property(assign, nonatomic) CLLocationDegrees headingFilter __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_3_0);
+@property(assign, nonatomic) CLLocationDegrees headingFilter __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_3_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  headingOrientation
@@ -250,7 +299,7 @@
  *      CLDeviceOrientationFaceDown are ignored.
  *      
  */
-@property(assign, nonatomic) CLDeviceOrientation headingOrientation __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_4_0);
+@property(assign, nonatomic) CLDeviceOrientation headingOrientation __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  heading
@@ -258,7 +307,7 @@
  *  Discussion:
  *      Returns the latest heading update received, or nil if none is available.
  */
-@property(readonly, nonatomic, copy, nullable) CLHeading *heading __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_4_0);
+@property(readonly, nonatomic, copy, nullable) CLHeading *heading __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  maximumRegionMonitoringDistance
@@ -268,7 +317,7 @@
  *       Attempts to register a region larger than this will generate a kCLErrorRegionMonitoringFailure.
  *       This value may vary based on the hardware features of the device, as well as on dynamically changing resource constraints.
  */
-@property (readonly, nonatomic) CLLocationDistance maximumRegionMonitoringDistance __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_4_0);
+@property (readonly, nonatomic) CLLocationDistance maximumRegionMonitoringDistance __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  monitoredRegions
@@ -278,7 +327,7 @@
  *       has been instructed to monitor a region, during this or previous launches of your application, it will
  *       be present in this set.
  */
-@property (readonly, nonatomic, copy) NSSet<__kindof CLRegion *> *monitoredRegions __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_4_0);
+@property (readonly, nonatomic, copy) NSSet<__kindof CLRegion *> *monitoredRegions __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  rangedRegions
@@ -286,7 +335,72 @@
  *  Discussion:
  *       Retrieve a set of objects representing the regions for which this location manager is actively providing ranging.
  */
-@property (readonly, nonatomic, copy) NSSet<__kindof CLRegion *> *rangedRegions __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_7_0);
+@property (readonly, nonatomic, copy) NSSet<__kindof CLRegion *> *rangedRegions __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+
+/*
+ *  requestWhenInUseAuthorization
+ *
+ *  Discussion:
+ *      When +authorizationStatus == kCLAuthorizationStatusNotDetermined,
+ *      calling this method will trigger a prompt to request "when-in-use"
+ *      authorization from the user.  If possible, perform this call in response
+ *      to direct user request for a location-based service so that the reason
+ *      for the prompt will be clear.  Any authorization change as a result of
+ *      the prompt will be reflected via the usual delegate callback:
+ *      -locationManager:didChangeAuthorizationStatus:.
+ *
+ *      If received, "when-in-use" authorization grants access to the user's
+ *      location via -startUpdatingLocation/-startRangingBeaconsInRegion while
+ *      in the foreground.  If updates have been started when going to the
+ *      background, then a status bar banner will be displayed to maintain
+ *      visibility to the user, and updates will continue until stopped
+ *      normally, or the app is killed by the user.
+ *
+ *      "When-in-use" authorization does NOT enable monitoring API on regions,
+ *      significant location changes, or visits, and -startUpdatingLocation will
+ *      not succeed if invoked from the background.
+ *
+ *      When +authorizationStatus != kCLAuthorizationStatusNotDetermined, (ie
+ *      generally after the first call) this method will do nothing.
+ *
+ *      If the NSLocationWhenInUseUsageDescription key is not specified in your
+ *      Info.plist, this method will do nothing, as your app will be assumed not
+ *      to support WhenInUse authorization.
+ */
+- (void)requestWhenInUseAuthorization __OSX_AVAILABLE_STARTING(__MAC_NA, __IPHONE_8_0);
+
+/*
+ *  requestAlwaysAuthorization
+ *
+ *  Discussion:
+ *      When +authorizationStatus == kCLAuthorizationStatusNotDetermined,
+ *      calling this method will trigger a prompt to request "always"
+ *      authorization from the user.  If possible, perform this call in response
+ *      to direct user request for a location-based service so that the reason
+ *      for the prompt will be clear.  Any authorization change as a result of
+ *      the prompt will be reflected via the usual delegate callback:
+ *      -locationManager:didChangeAuthorizationStatus:.
+ *
+ *      If received, "always" authorization grants access to the user's
+ *      location via any CLLocationManager API, and grants access to
+ *      launch-capable monitoring API such as geofencing/region monitoring,
+ *      significante location visits, etc.  Even if killed by the user, launch
+ *      events triggered by monitored regions or visit patterns will cause a
+ *      relaunch.
+ *
+ *      "Always" authorization presents a significant risk to user privacy, and
+ *      as such requesting it is discouraged unless background launch behavior
+ *      is genuinely required.  Do not call +requestAlwaysAuthorization unless
+ *      you think users will thank you for doing so.
+ *
+ *      When +authorizationStatus != kCLAuthorizationStatusNotDetermined, (ie
+ *      generally after the first call) this method will do nothing.
+ *
+ *      If the NSLocationAlwaysUsageDescription key is not specified in your
+ *      Info.plist, this method will do nothing, as your app will be assumed not
+ *      to support Always authorization.
+ */
+- (void)requestAlwaysAuthorization __OSX_AVAILABLE_STARTING(__MAC_NA, __IPHONE_8_0) __TVOS_PROHIBITED;
 
 /*
  *  startUpdatingLocation
@@ -294,7 +408,7 @@
  *  Discussion:
  *      Start updating locations.
  */
-- (void)startUpdatingLocation;
+- (void)startUpdatingLocation __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  stopUpdatingLocation
@@ -305,12 +419,36 @@
 - (void)stopUpdatingLocation;
 
 /*
+ *  requestLocation
+ *
+ *  Discussion:
+ *      Request a single location update.
+ *
+ *      The service will attempt to determine location with accuracy according
+ *      to the desiredAccuracy property.  The location update will be delivered
+ *      via the standard delegate callback, i.e. locationManager:didUpdateLocations:
+ *
+ *      If the best available location has lower accuracy, then it will be
+ *      delivered via the standard delegate callback after timeout.
+ *
+ *      If no location can be determined, the locationManager:didFailWithError:
+ *      delegate callback will be delivered with error location unknown.
+ *
+ *      There can only be one outstanding location request and this method can
+ *      not be used concurrently with startUpdatingLocation or
+ *      allowDeferredLocationUpdates.  Calling either of those methods will
+ *      immediately cancel the location request.  The method
+ *      stopUpdatingLocation can be used to explicitly cancel the request.
+ */
+- (void)requestLocation __OSX_AVAILABLE_STARTING(__MAC_NA, __IPHONE_9_0);
+
+/*
  *  startUpdatingHeading
  *
  *  Discussion:
  *      Start updating heading.
  */
-- (void)startUpdatingHeading __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_3_0);
+- (void)startUpdatingHeading __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_3_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  stopUpdatingHeading
@@ -318,7 +456,7 @@
  *  Discussion:
  *      Stop updating heading.
  */
-- (void)stopUpdatingHeading __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_3_0);
+- (void)stopUpdatingHeading __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_3_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  dismissHeadingCalibrationDisplay
@@ -326,7 +464,7 @@
  *  Discussion:
  *      Dismiss the heading calibration immediately.
  */
-- (void)dismissHeadingCalibrationDisplay __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_3_0);
+- (void)dismissHeadingCalibrationDisplay __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_3_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  startMonitoringSignificantLocationChanges
@@ -337,7 +475,7 @@
  *      location service.
  *
  */
-- (void)startMonitoringSignificantLocationChanges __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_4_0);
+- (void)startMonitoringSignificantLocationChanges __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  stopMonitoringSignificantLocationChanges
@@ -346,7 +484,7 @@
  *      Stop monitoring significant location changes.
  *
  */
-- (void)stopMonitoringSignificantLocationChanges __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_4_0);
+- (void)stopMonitoringSignificantLocationChanges __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  startMonitoringForRegion:desiredAccuracy:
@@ -364,8 +502,8 @@
  *      This is done asynchronously and may not be immediately reflected in monitoredRegions.
  */
 - (void)startMonitoringForRegion:(CLRegion *)region
-                 desiredAccuracy:(CLLocationAccuracy)accuracy __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_NA, __MAC_NA,__IPHONE_4_0, __IPHONE_6_0);
-		
+                 desiredAccuracy:(CLLocationAccuracy)accuracy __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_NA, __MAC_NA,__IPHONE_4_0, __IPHONE_6_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+
 /*
  *  stopMonitoringForRegion:
  *
@@ -375,7 +513,7 @@
  *
  *      This is done asynchronously and may not be immediately reflected in monitoredRegions.
  */
-- (void)stopMonitoringForRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_4_0);
+- (void)stopMonitoringForRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  startMonitoringForRegion:
@@ -389,7 +527,7 @@
  *
  *      This is done asynchronously and may not be immediately reflected in monitoredRegions.
  */
-- (void)startMonitoringForRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_5_0);
+- (void)startMonitoringForRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_5_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  requestStateForRegion:
@@ -398,7 +536,7 @@
  *      Asynchronously retrieve the cached state of the specified region. The state is returned to the delegate via
  *      locationManager:didDetermineState:forRegion:.
  */
-- (void)requestStateForRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_10,__IPHONE_7_0);
+- (void)requestStateForRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_10,__IPHONE_7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  startRangingBeaconsInRegion:
@@ -406,9 +544,7 @@
  *  Discussion:
  *      Start calculating ranges for beacons in the specified region.
  */
-#if TARGET_OS_IPHONE
-- (void)startRangingBeaconsInRegion:(CLBeaconRegion *)region __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_7_0);
-#endif
+- (void)startRangingBeaconsInRegion:(CLBeaconRegion *)region __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  stopRangingBeaconsInRegion:
@@ -416,9 +552,7 @@
  *  Discussion:
  *      Stop calculating ranges for the specified region.
  */
-#if TARGET_OS_IPHONE
-- (void)stopRangingBeaconsInRegion:(CLBeaconRegion *)region __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_7_0);
-#endif
+- (void)stopRangingBeaconsInRegion:(CLBeaconRegion *)region __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *	allowDeferredLocationUpdatesUntilTraveled:timeout:
@@ -455,7 +589,7 @@
  *		criteria have not been met.
  */
 - (void)allowDeferredLocationUpdatesUntilTraveled:(CLLocationDistance)distance
-					  timeout:(NSTimeInterval)timeout __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_6_0);
+					  timeout:(NSTimeInterval)timeout __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_6_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *	disallowDeferredLocationUpdates
@@ -464,7 +598,7 @@
  *		Disallow deferred location updates if previously enabled. Any outstanding
  *		updates will be sent and regular location updates will resume.
  */
-- (void)disallowDeferredLocationUpdates __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_6_0);
+- (void)disallowDeferredLocationUpdates __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_6_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  deferredLocationUpdatesAvailable
@@ -472,7 +606,7 @@
  *  Discussion:
  *      Returns YES if the device supports deferred location updates, otherwise NO.
  */
-+ (BOOL)deferredLocationUpdatesAvailable __OSX_AVAILABLE_STARTING(__MAC_10_9,__IPHONE_6_0);
++ (BOOL)deferredLocationUpdatesAvailable __OSX_AVAILABLE_STARTING(__MAC_10_9,__IPHONE_6_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManagerDelegate.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManagerDelegate.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManagerDelegate.h	2015-08-23 02:48:53.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManagerDelegate.h	2016-05-16 02:07:13.000000000 +0200
@@ -1,4 +1,3 @@
-
 /*
  *  CLLocationManagerDelegate.h
  *  CoreLocation
@@ -7,16 +6,18 @@
  *
  */
 
+#import <Availability.h>
 #import <Foundation/Foundation.h>
-#import <CoreLocation/CLAvailability.h>
 #import <CoreLocation/CLLocationManager.h>
 #import <CoreLocation/CLRegion.h>
+#import <CoreLocation/CLVisit.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
 @class CLLocation;
 @class CLHeading;
 @class CLBeacon;
+@class CLVisit;
 
 /*
  *  CLLocationManagerDelegate
@@ -34,13 +35,13 @@
  *  Discussion:
  *    Invoked when a new location is available. oldLocation may be nil if there is no previous location
  *    available.
-*
+ *
  *    This method is deprecated. If locationManager:didUpdateLocations: is
  *    implemented, this method will not be called.
  */
 - (void)locationManager:(CLLocationManager *)manager
 	didUpdateToLocation:(CLLocation *)newLocation
-		   fromLocation:(CLLocation *)oldLocation __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_6, __MAC_NA, __IPHONE_2_0, __IPHONE_6_0);
+		   fromLocation:(CLLocation *)oldLocation __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_6, __MAC_NA, __IPHONE_2_0, __IPHONE_6_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  locationManager:didUpdateLocations:
@@ -53,7 +54,7 @@
  *    locations is an array of CLLocation objects in chronological order.
  */
 - (void)locationManager:(CLLocationManager *)manager
-	 didUpdateLocations:(NSArray *)locations __OSX_AVAILABLE_STARTING(__MAC_10_9,__IPHONE_6_0);
+	 didUpdateLocations:(NSArray<CLLocation *> *)locations __OSX_AVAILABLE_STARTING(__MAC_10_9,__IPHONE_6_0);
 
 /*
  *  locationManager:didUpdateHeading:
@@ -62,7 +63,7 @@
  *    Invoked when a new heading is available.
  */
 - (void)locationManager:(CLLocationManager *)manager
-       didUpdateHeading:(CLHeading *)newHeading __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_3_0);
+       didUpdateHeading:(CLHeading *)newHeading __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_3_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  locationManagerShouldDisplayHeadingCalibration:
@@ -71,7 +72,7 @@
  *    Invoked when a new heading is available. Return YES to display heading calibration info. The display 
  *    will remain until heading is calibrated, unless dismissed early via dismissHeadingCalibrationDisplay.
  */
-- (BOOL)locationManagerShouldDisplayHeadingCalibration:(CLLocationManager *)manager  __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_3_0);
+- (BOOL)locationManagerShouldDisplayHeadingCalibration:(CLLocationManager *)manager  __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_3_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  locationManager:didDetermineState:forRegion:
@@ -81,7 +82,7 @@
  *    a call to requestStateForRegion:.
  */
 - (void)locationManager:(CLLocationManager *)manager
-	didDetermineState:(CLRegionState)state forRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_10,__IPHONE_7_0);
+	didDetermineState:(CLRegionState)state forRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_10,__IPHONE_7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  locationManager:didRangeBeacons:inRegion:
@@ -93,10 +94,8 @@
  *    Similarly if a specific beacon no longer appears in beacons, it may be assumed the beacon is no longer received
  *    by the device.
  */
-#if TARGET_OS_IPHONE
 - (void)locationManager:(CLLocationManager *)manager
-	didRangeBeacons:(NSArray<CLBeacon *> *)beacons inRegion:(CLBeaconRegion *)region __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_7_0);
-#endif
+	didRangeBeacons:(NSArray<CLBeacon *> *)beacons inRegion:(CLBeaconRegion *)region __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  locationManager:rangingBeaconsDidFailForRegion:withError:
@@ -104,11 +103,9 @@
  *  Discussion:
  *    Invoked when an error has occurred ranging beacons in a region. Error types are defined in "CLError.h".
  */
-#if TARGET_OS_IPHONE
 - (void)locationManager:(CLLocationManager *)manager
 	rangingBeaconsDidFailForRegion:(CLBeaconRegion *)region
-	withError:(NSError *)error __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_7_0);
-#endif
+	withError:(NSError *)error __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  locationManager:didEnterRegion:
@@ -118,7 +115,7 @@
  *    CLLocationManager instance with a non-nil delegate that implements this method.
  */
 - (void)locationManager:(CLLocationManager *)manager
-	didEnterRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_4_0);
+	didEnterRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  locationManager:didExitRegion:
@@ -128,7 +125,7 @@
  *    CLLocationManager instance with a non-nil delegate that implements this method.
  */
 - (void)locationManager:(CLLocationManager *)manager
-	didExitRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_4_0);
+	didExitRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  locationManager:didFailWithError:
@@ -147,7 +144,7 @@
  */
 - (void)locationManager:(CLLocationManager *)manager
 	monitoringDidFailForRegion:(nullable CLRegion *)region
-	withError:(NSError *)error __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_4_0);
+	withError:(NSError *)error __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  locationManager:didChangeAuthorizationStatus:
@@ -164,13 +161,13 @@
  *    Invoked when a monitoring for a region started successfully.
  */
 - (void)locationManager:(CLLocationManager *)manager
-	didStartMonitoringForRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_5_0);
+	didStartMonitoringForRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_5_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  Discussion:
  *    Invoked when location updates are automatically paused.
  */
-- (void)locationManagerDidPauseLocationUpdates:(CLLocationManager *)manager __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_6_0);
+- (void)locationManagerDidPauseLocationUpdates:(CLLocationManager *)manager __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_6_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  Discussion:
@@ -179,7 +176,7 @@
  *    In the event that your application is terminated while suspended, you will
  *	  not receive this notification.
  */
-- (void)locationManagerDidResumeLocationUpdates:(CLLocationManager *)manager __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_6_0);
+- (void)locationManagerDidResumeLocationUpdates:(CLLocationManager *)manager __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_6_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  locationManager:didFinishDeferredUpdatesWithError:
@@ -193,7 +190,17 @@
  *    criteria are met (see CLError), otherwise error will be nil.
  */
 - (void)locationManager:(CLLocationManager *)manager
-	didFinishDeferredUpdatesWithError:(nullable NSError *)error __OSX_AVAILABLE_STARTING(__MAC_10_9,__IPHONE_6_0);
+	didFinishDeferredUpdatesWithError:(nullable NSError *)error __OSX_AVAILABLE_STARTING(__MAC_10_9,__IPHONE_6_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+
+/*
+ *  locationManager:didVisit:
+ *
+ *  Discussion:
+ *    Invoked when the CLLocationManager determines that the device has visited
+ *    a location, if visit monitoring is currently started (possibly from a
+ *    prior launch).
+ */
+- (void)locationManager:(CLLocationManager *)manager didVisit:(CLVisit *)visit __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_8_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLPlacemark.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLPlacemark.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLPlacemark.h	2015-08-23 02:48:53.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLPlacemark.h	2016-05-16 02:07:13.000000000 +0200
@@ -4,17 +4,16 @@
  *
  *  Copyright (c) 2010 Apple Inc. All rights reserved.
  */
+
 #import <Foundation/Foundation.h>
 #import <CoreLocation/CLAvailability.h>
 
-// The CLPlacemark API is very heavily nullable
+NS_ASSUME_NONNULL_BEGIN
 
 @class CLLocation;
 @class CLRegion;
 @class CLPlacemarkInternal;
 
-NS_ASSUME_NONNULL_BEGIN
-
 /*
  *  CLPlacemark
  *  
@@ -36,7 +35,7 @@
  * Discussion:
  *   Initialize a newly allocated placemark from another placemark, copying its data.
  */
-- (instancetype)initWithPlacemark:(CLPlacemark *)placemark;
+- (instancetype)initWithPlacemark:(CLPlacemark *) placemark;
 
 /*
  *  location
@@ -55,10 +54,10 @@
 @property (nonatomic, readonly, copy, nullable) CLRegion *region;
 
 /*
- * timeZone
+ *  timeZone
  *
- * Discussion:
- *    Returns the time zone associated with the placemark.
+ *  Discussion:
+ *		Returns the time zone associated with the placemark.
  */
 @property (nonatomic, readonly, copy, nullable) NSTimeZone *timeZone NS_AVAILABLE(10_11,9_0);
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLRegion.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLRegion.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLRegion.h	2015-08-23 02:48:53.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLRegion.h	2016-05-16 02:07:13.000000000 +0200
@@ -25,7 +25,7 @@
 	CLRegionStateUnknown,
 	CLRegionStateInside,
 	CLRegionStateOutside
-} NS_ENUM_AVAILABLE(10_10, 7_0);
+} NS_ENUM_AVAILABLE(10_10, 7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  * CLProximity
@@ -39,7 +39,7 @@
 	CLProximityImmediate,
 	CLProximityNear,
 	CLProximityFar
-} NS_ENUM_AVAILABLE(NA, 7_0);
+} NS_ENUM_AVAILABLE(NA, 7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  CLRegion
@@ -64,8 +64,8 @@
  *    This method has been deprecated, please see CLCircularRegion.
  */
 - (instancetype)initCircularRegionWithCenter:(CLLocationCoordinate2D)center
-                                      radius:(CLLocationDistance)radius
-                                  identifier:(NSString *)identifier __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7,__MAC_10_10,__IPHONE_4_0,__IPHONE_7_0);
+									  radius:(CLLocationDistance)radius
+								  identifier:(NSString *)identifier __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7,__MAC_10_10,__IPHONE_4_0,__IPHONE_7_0) __TVOS_PROHIBITED;
 
 /*
  *  center
@@ -75,7 +75,7 @@
  *
  *    This method has been deprecated, please see CLCircularRegion.
  */
-@property (readonly, nonatomic) CLLocationCoordinate2D center __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7,__MAC_10_10,__IPHONE_4_0,__IPHONE_7_0);
+@property (readonly, nonatomic) CLLocationCoordinate2D center __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7,__MAC_10_10,__IPHONE_4_0,__IPHONE_7_0) __TVOS_PROHIBITED;
 
 /*
  *  radius
@@ -85,7 +85,7 @@
  *
  *    This method has been deprecated, please see CLCircularRegion.
  */
-@property (readonly, nonatomic) CLLocationDistance radius __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7,__MAC_10_10,__IPHONE_4_0,__IPHONE_7_0);
+@property (readonly, nonatomic) CLLocationDistance radius __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7,__MAC_10_10,__IPHONE_4_0,__IPHONE_7_0) __TVOS_PROHIBITED;
 
 /*
  *  identifier
@@ -121,7 +121,7 @@
  *
  *    This method has been deprecated, please see CLCircularRegion.
  */
-- (BOOL)containsCoordinate:(CLLocationCoordinate2D)coordinate __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7,__MAC_10_10,__IPHONE_4_0,__IPHONE_7_0);
+- (BOOL)containsCoordinate:(CLLocationCoordinate2D)coordinate __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7,__MAC_10_10,__IPHONE_4_0,__IPHONE_7_0) __TVOS_PROHIBITED;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLVisit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLVisit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLVisit.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLVisit.h	2016-05-16 02:07:13.000000000 +0200
@@ -0,0 +1,65 @@
+/*
+ *  CLVisit.h
+ *  CoreLocation
+ *
+ *  Copyright (c) 2014 Apple Inc. All rights reserved.
+ *
+ */
+
+#import <Foundation/Foundation.h>
+#import <CoreLocation/CLLocation.h>
+
+#import <CoreLocation/CLAvailability.h>
+#if !CL_MAC_CODEBASE // whole file
+
+NS_ASSUME_NONNULL_BEGIN
+
+/*
+ *  CLVisit
+ *
+ *  Discussion
+ *    An instance of this class represents a possibly open-ended event
+ *    during which the device was at the specified coordinate.
+ */
+NS_CLASS_AVAILABLE(NA, 8_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+@interface CLVisit : NSObject <NSSecureCoding, NSCopying>
+
+/*
+ *  arrivalDate
+ *
+ *  Discussion:
+ *    The date when the visit began.  This may be equal to [NSDate
+ *    distantPast] if the true arrival date isn't available.
+ */
+@property (nonatomic, readonly, copy) NSDate *arrivalDate;
+
+/*
+ *  departureDate
+ *
+ *  Discussion:
+ *    The date when the visit ended.  This is equal to [NSDate
+ *    distantFuture] if the device hasn't yet left.
+ */
+@property (nonatomic, readonly, copy) NSDate *departureDate;
+
+/*
+ *  coordinate
+ *
+ *  Discussion:
+ *    The center of the region which the device is visiting.
+ */
+@property (nonatomic, readonly) CLLocationCoordinate2D coordinate;
+
+/*
+ *
+ *  horizontalAccuracy
+ *
+ *  Discussion:
+ *    An estimate of the radius (in meters) of the region which the
+ *    device is visiting.
+ */
+@property (nonatomic, readonly) CLLocationAccuracy horizontalAccuracy;
+@end
+
+NS_ASSUME_NONNULL_END
+#endif // whole file
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CoreLocation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CoreLocation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CoreLocation.h	2015-08-23 02:48:53.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CoreLocation.h	2016-05-16 02:07:13.000000000 +0200
@@ -24,7 +24,9 @@
 #import <CoreLocation/CLLocation.h>
 #import <CoreLocation/CLLocationManager.h>
 #import <CoreLocation/CLLocationManagerDelegate.h>
+#import <CoreLocation/CLLocationManager+CLVisitExtensions.h>
 #import <CoreLocation/CLPlacemark.h>
 #import <CoreLocation/CLGeocoder.h>
+#import <CoreLocation/CLVisit.h>
 
 #endif /* __CORELOCATION__ */

```