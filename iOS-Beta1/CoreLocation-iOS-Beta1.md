#CoreLocation.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLAvailability.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLAvailability.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLAvailability.h	2015-10-03 00:41:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLAvailability.h	2016-06-01 05:03:00.000000000 +0200
@@ -14,14 +14,6 @@
 
 #import <Availability.h>
 
-#ifndef __MAC_TBD
-#define __MAC_TBD __MAC_NA
-#endif
-
-#ifndef __AVAILABILITY_INTERNAL__MAC_TBD
-#define __AVAILABILITY_INTERNAL__MAC_TBD __AVAILABILITY_INTERNAL_UNAVAILABLE
-#endif
-
 #ifndef __TVOS_PROHIBITED
 #define __TVOS_PROHIBITED
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLBeaconRegion.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLBeaconRegion.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLBeaconRegion.h	2015-10-03 00:41:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLBeaconRegion.h	2016-06-01 05:02:52.000000000 +0200
@@ -96,7 +96,7 @@
  *    Proximity identifier associated with the region.
  *
  */
-@property (readonly, nonatomic, strong) NSUUID *proximityUUID;
+@property (readonly, nonatomic, copy) NSUUID *proximityUUID;
 
 /*
  *  major
@@ -105,7 +105,7 @@
  *    Most significant value associated with the region. If a major value wasn't specified, this will be nil.
  *
  */
-@property (readonly, nonatomic, strong, nullable) NSNumber *major;
+@property (readonly, nonatomic, copy, nullable) NSNumber *major;
 
 /*
  *  minor
@@ -114,7 +114,7 @@
  *    Least significant value associated with the region. If a minor value wasn't specified, this will be nil.
  *
  */
-@property (readonly, nonatomic, strong, nullable) NSNumber *minor;
+@property (readonly, nonatomic, copy, nullable) NSNumber *minor;
 
 /*
  *  notifyEntryStateOnDisplay
@@ -127,6 +127,8 @@
 
 @end
 
+@class CLBeaconInternal;
+
 /*
  *  CLBeacon
  *
@@ -136,6 +138,9 @@
  */
 NS_CLASS_AVAILABLE(NA, 7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
 @interface CLBeacon : NSObject <NSCopying, NSSecureCoding>
+{
+	CLBeaconInternal *_internal;
+}
 
 /*
  *  proximityUUID
@@ -144,7 +149,7 @@
  *    Proximity identifier associated with the beacon.
  *
  */
-@property (readonly, nonatomic, strong) NSUUID *proximityUUID;
+@property (readonly, nonatomic, copy) NSUUID *proximityUUID;
 
 /*
  *  major
@@ -153,7 +158,7 @@
  *    Most significant value associated with the beacon.
  *
  */
-@property (readonly, nonatomic, strong) NSNumber *major;
+@property (readonly, nonatomic, copy) NSNumber *major;
 
 /*
  *  minor
@@ -162,7 +167,7 @@
  *    Least significant value associated with the beacon.
  *
  */
-@property (readonly, nonatomic, strong) NSNumber *minor;
+@property (readonly, nonatomic, copy) NSNumber *minor;
 
 /*
  *  proximity
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLCircularRegion.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLCircularRegion.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLCircularRegion.h	2015-10-03 00:41:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLCircularRegion.h	2016-06-01 05:03:00.000000000 +0200
@@ -19,7 +19,7 @@
  *  Discussion:
  *    A circular geographic area.
  */
-NS_CLASS_AVAILABLE(NA, 7_0)
+NS_CLASS_AVAILABLE(10_10, 7_0)
 @interface CLCircularRegion : CLRegion
 
 /*
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLError.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLError.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLError.h	2015-10-03 00:41:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLError.h	2016-06-01 05:03:00.000000000 +0200
@@ -1,4 +1,3 @@
-
 /*
  *  CLError.h
  *  CoreLocation
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLErrorDomain.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLErrorDomain.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLErrorDomain.h	2015-10-03 00:41:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLErrorDomain.h	2016-06-01 05:03:00.000000000 +0200
@@ -1,4 +1,3 @@
-
 /*
  *  CLErrorDomain.h
  *  CoreLocation
@@ -16,6 +15,8 @@
  *  
  *  Discussion:
  *    Error returned as the domain to NSError from CoreLocation.
+ *
+ *  The file CLError.h defines constants for the errors in kCLErrorDomain.
  */
 extern NSString *const kCLErrorDomain;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLGeocoder.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLGeocoder.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLGeocoder.h	2015-10-03 00:41:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLGeocoder.h	2016-06-01 05:03:00.000000000 +0200
@@ -5,8 +5,6 @@
  *  Copyright (c) 2010 Apple Inc. All rights reserved.
  */
 
-#if TARGET_OS_IPHONE
-
 #import <Foundation/Foundation.h>
 #import <CoreLocation/CLLocation.h>
 #import <CoreLocation/CLAvailability.h>
@@ -20,7 +18,7 @@
 // geocoding handler, CLPlacemarks are provided in order of most confident to least confident
 typedef void (^CLGeocodeCompletionHandler)(NSArray< CLPlacemark *> * __nullable placemarks, NSError * __nullable error);
 
-NS_CLASS_AVAILABLE(TBD,5_0)
+NS_CLASS_AVAILABLE(10_8,5_0)
 @interface CLGeocoder : NSObject
 {
 @private
@@ -46,5 +44,3 @@
 @end
 
 NS_ASSUME_NONNULL_END
-
-#endif //TARGET_OS_IPHONE
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLHeading.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLHeading.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLHeading.h	2015-10-03 00:41:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLHeading.h	2016-06-01 05:03:00.000000000 +0200
@@ -1,4 +1,3 @@
-
 /*
  *  CLHeading.h
  *  CoreLocation
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocation.h	2015-10-03 00:41:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocation.h	2016-05-22 06:00:55.000000000 +0200
@@ -58,10 +58,11 @@
  *    longitude:
  *      The longitude in degrees.
  */
-typedef struct {
+struct CLLocationCoordinate2D {
 	CLLocationDegrees latitude;
 	CLLocationDegrees longitude;
-} CLLocationCoordinate2D;
+};
+typedef struct CLLocationCoordinate2D CLLocationCoordinate2D;
 
 /*
  *  CLLocationDistance
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager+CLVisitExtensions.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager+CLVisitExtensions.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager+CLVisitExtensions.h	2015-10-03 00:41:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager+CLVisitExtensions.h	2016-06-01 05:03:00.000000000 +0200
@@ -8,6 +8,8 @@
 
 #import <CoreLocation/CLLocationManager.h>
 
+#import <CoreLocation/CLAvailability.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 @interface CLLocationManager (CLVisitExtensions)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager.h	2015-10-03 00:41:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager.h	2016-06-01 05:54:00.000000000 +0200
@@ -1,4 +1,3 @@
-
 /*
  *  CLLocationManager.h
  *  CoreLocation
@@ -53,15 +52,24 @@
 
 	// User has granted authorization to use their location at any time,
 	// including monitoring for regions, visits, or significant location changes.
-	kCLAuthorizationStatusAuthorizedAlways NS_ENUM_AVAILABLE(NA, 8_0),
+	//
+	// This value should be used on iOS, tvOS and watchOS.  It is available on
+	// MacOS, but kCLAuthorizationStatusAuthorized is synonymous and preferred.
+	kCLAuthorizationStatusAuthorizedAlways NS_ENUM_AVAILABLE(10_12, 8_0),
 
 	// User has granted authorization to use their location only when your app
 	// is visible to them (it will be made visible to them if you continue to
 	// receive location updates while in the background).  Authorization to use
 	// launch APIs has not been granted.
+	//
+	// This value is not available on MacOS.  It should be used on iOS, tvOS and
+	// watchOS.
 	kCLAuthorizationStatusAuthorizedWhenInUse NS_ENUM_AVAILABLE(NA, 8_0),
 
-	// This value is deprecated, but was equivalent to the new -Always value.
+	// User has authorized this application to use location services.
+	//
+	// This value is deprecated or prohibited on iOS, tvOS and watchOS.
+	// It should be used on MacOS.
 	kCLAuthorizationStatusAuthorized NS_ENUM_DEPRECATED(10_6, NA, 2_0, 8_0, "Use kCLAuthorizationStatusAuthorizedAlways") __TVOS_PROHIBITED __WATCHOS_PROHIBITED = kCLAuthorizationStatusAuthorizedAlways
 };
 
@@ -131,7 +139,7 @@
  *      Determines whether the device supports monitoring for the specified type of region.
  *      If NO, all attempts to monitor the specified type of region will fail.
  */
-+ (BOOL)isMonitoringAvailableForClass:(Class)regionClass __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
++ (BOOL)isMonitoringAvailableForClass:(Class)regionClass __OSX_AVAILABLE_STARTING(__MAC_10_10,__IPHONE_7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  regionMonitoringAvailable
@@ -139,7 +147,7 @@
  *  Discussion:
  *      Deprecated. Use +isMonitoringAvailableForClass: instead.
  */
-+ (BOOL)regionMonitoringAvailable __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7,__MAC_NA,__IPHONE_4_0,__IPHONE_7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
++ (BOOL)regionMonitoringAvailable __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_8,__MAC_10_10,__IPHONE_4_0,__IPHONE_7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  regionMonitoringEnabled
@@ -147,7 +155,7 @@
  *  Discussion:
  *      Deprecated. Use +isMonitoringAvailableForClass: and +authorizationStatus instead.
  */
-+ (BOOL)regionMonitoringEnabled __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_NA, __MAC_NA,__IPHONE_4_0, __IPHONE_6_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
++ (BOOL)regionMonitoringEnabled __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_8, __MAC_10_10,__IPHONE_4_0, __IPHONE_6_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  isRangingAvailable
@@ -309,7 +317,7 @@
  *       Attempts to register a region larger than this will generate a kCLErrorRegionMonitoringFailure.
  *       This value may vary based on the hardware features of the device, as well as on dynamically changing resource constraints.
  */
-@property (readonly, nonatomic) CLLocationDistance maximumRegionMonitoringDistance __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+@property (readonly, nonatomic) CLLocationDistance maximumRegionMonitoringDistance __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  monitoredRegions
@@ -319,7 +327,7 @@
  *       has been instructed to monitor a region, during this or previous launches of your application, it will
  *       be present in this set.
  */
-@property (readonly, nonatomic, copy) NSSet<__kindof CLRegion *> *monitoredRegions __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+@property (readonly, nonatomic, copy) NSSet<__kindof CLRegion *> *monitoredRegions __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  rangedRegions
@@ -505,7 +513,7 @@
  *
  *      This is done asynchronously and may not be immediately reflected in monitoredRegions.
  */
-- (void)stopMonitoringForRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+- (void)stopMonitoringForRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  startMonitoringForRegion:
@@ -519,7 +527,7 @@
  *
  *      This is done asynchronously and may not be immediately reflected in monitoredRegions.
  */
-- (void)startMonitoringForRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_TBD,__IPHONE_5_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+- (void)startMonitoringForRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_5_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  requestStateForRegion:
@@ -528,7 +536,7 @@
  *      Asynchronously retrieve the cached state of the specified region. The state is returned to the delegate via
  *      locationManager:didDetermineState:forRegion:.
  */
-- (void)requestStateForRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+- (void)requestStateForRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_10,__IPHONE_7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  startRangingBeaconsInRegion:
@@ -598,7 +606,7 @@
  *  Discussion:
  *      Returns YES if the device supports deferred location updates, otherwise NO.
  */
-+ (BOOL)deferredLocationUpdatesAvailable __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_6_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
++ (BOOL)deferredLocationUpdatesAvailable __OSX_AVAILABLE_STARTING(__MAC_10_9,__IPHONE_6_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManagerDelegate.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManagerDelegate.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManagerDelegate.h	2015-10-03 00:41:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManagerDelegate.h	2016-05-16 02:07:13.000000000 +0200
@@ -1,4 +1,3 @@
-
 /*
  *  CLLocationManagerDelegate.h
  *  CoreLocation
@@ -18,6 +17,7 @@
 @class CLLocation;
 @class CLHeading;
 @class CLBeacon;
+@class CLVisit;
 
 /*
  *  CLLocationManagerDelegate
@@ -54,7 +54,7 @@
  *    locations is an array of CLLocation objects in chronological order.
  */
 - (void)locationManager:(CLLocationManager *)manager
-	 didUpdateLocations:(NSArray<CLLocation *> *)locations __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_6_0);
+	 didUpdateLocations:(NSArray<CLLocation *> *)locations __OSX_AVAILABLE_STARTING(__MAC_10_9,__IPHONE_6_0);
 
 /*
  *  locationManager:didUpdateHeading:
@@ -82,7 +82,7 @@
  *    a call to requestStateForRegion:.
  */
 - (void)locationManager:(CLLocationManager *)manager
-	didDetermineState:(CLRegionState)state forRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+	didDetermineState:(CLRegionState)state forRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_10,__IPHONE_7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  locationManager:didRangeBeacons:inRegion:
@@ -115,7 +115,7 @@
  *    CLLocationManager instance with a non-nil delegate that implements this method.
  */
 - (void)locationManager:(CLLocationManager *)manager
-	didEnterRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+	didEnterRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  locationManager:didExitRegion:
@@ -125,7 +125,7 @@
  *    CLLocationManager instance with a non-nil delegate that implements this method.
  */
 - (void)locationManager:(CLLocationManager *)manager
-	didExitRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+	didExitRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  locationManager:didFailWithError:
@@ -144,7 +144,7 @@
  */
 - (void)locationManager:(CLLocationManager *)manager
 	monitoringDidFailForRegion:(nullable CLRegion *)region
-	withError:(NSError *)error __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+	withError:(NSError *)error __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  locationManager:didChangeAuthorizationStatus:
@@ -161,7 +161,7 @@
  *    Invoked when a monitoring for a region started successfully.
  */
 - (void)locationManager:(CLLocationManager *)manager
-	didStartMonitoringForRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_TBD,__IPHONE_5_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+	didStartMonitoringForRegion:(CLRegion *)region __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_5_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  Discussion:
@@ -190,7 +190,7 @@
  *    criteria are met (see CLError), otherwise error will be nil.
  */
 - (void)locationManager:(CLLocationManager *)manager
-	didFinishDeferredUpdatesWithError:(nullable NSError *)error __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_6_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+	didFinishDeferredUpdatesWithError:(nullable NSError *)error __OSX_AVAILABLE_STARTING(__MAC_10_9,__IPHONE_6_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  locationManager:didVisit:
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLPlacemark.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLPlacemark.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLPlacemark.h	2015-10-03 00:41:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLPlacemark.h	2016-06-01 05:03:00.000000000 +0200
@@ -5,8 +5,6 @@
  *  Copyright (c) 2010 Apple Inc. All rights reserved.
  */
 
-#if TARGET_OS_IPHONE
-
 #import <Foundation/Foundation.h>
 #import <CoreLocation/CLAvailability.h>
 
@@ -24,7 +22,7 @@
  *    information such as the country, state, city, and street address.
  */
 
-NS_CLASS_AVAILABLE(TBD,5_0)
+NS_CLASS_AVAILABLE(10_8,5_0)
 @interface CLPlacemark : NSObject <NSCopying, NSSecureCoding>
 {
 @private
@@ -88,6 +86,4 @@
 @property (nonatomic, readonly, copy, nullable) NSArray<NSString *> *areasOfInterest; // eg. Golden Gate Park
 @end
 
-#endif //TARGET_OS_IPHONE
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLRegion.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLRegion.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLRegion.h	2015-10-03 00:41:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLRegion.h	2016-06-01 05:03:00.000000000 +0200
@@ -12,6 +12,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+@class CLRegionInternal;
+
 /*
  * CLRegionState
  *
@@ -23,7 +25,7 @@
 	CLRegionStateUnknown,
 	CLRegionStateInside,
 	CLRegionStateOutside
-} NS_ENUM_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+} NS_ENUM_AVAILABLE(10_10, 7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  * CLProximity
@@ -37,7 +39,7 @@
 	CLProximityImmediate,
 	CLProximityNear,
 	CLProximityFar
-} NS_ENUM_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+} NS_ENUM_AVAILABLE(NA, 7_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 /*
  *  CLRegion
@@ -47,7 +49,10 @@
  */
 NS_CLASS_AVAILABLE(10_7, 4_0)
 @interface CLRegion : NSObject <NSCopying, NSSecureCoding>
-
+{
+@protected
+	CLRegionInternal *_internal;
+}
 /*
  *  initCircularRegionWithCenter:radius:identifier:
  *  
@@ -60,7 +65,7 @@
  */
 - (instancetype)initCircularRegionWithCenter:(CLLocationCoordinate2D)center
 									  radius:(CLLocationDistance)radius
-								  identifier:(NSString *)identifier __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7,__MAC_NA,__IPHONE_4_0,__IPHONE_7_0) __TVOS_PROHIBITED;
+								  identifier:(NSString *)identifier __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7,__MAC_10_10,__IPHONE_4_0,__IPHONE_7_0) __TVOS_PROHIBITED;
 
 /*
  *  center
@@ -70,7 +75,7 @@
  *
  *    This method has been deprecated, please see CLCircularRegion.
  */
-@property (readonly, nonatomic) CLLocationCoordinate2D center __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7,__MAC_NA,__IPHONE_4_0,__IPHONE_7_0) __TVOS_PROHIBITED;
+@property (readonly, nonatomic) CLLocationCoordinate2D center __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7,__MAC_10_10,__IPHONE_4_0,__IPHONE_7_0) __TVOS_PROHIBITED;
 
 /*
  *  radius
@@ -80,7 +85,7 @@
  *
  *    This method has been deprecated, please see CLCircularRegion.
  */
-@property (readonly, nonatomic) CLLocationDistance radius __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7,__MAC_NA,__IPHONE_4_0,__IPHONE_7_0) __TVOS_PROHIBITED;
+@property (readonly, nonatomic) CLLocationDistance radius __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7,__MAC_10_10,__IPHONE_4_0,__IPHONE_7_0) __TVOS_PROHIBITED;
 
 /*
  *  identifier
@@ -97,7 +102,7 @@
  *    App will be launched and the delegate will be notified via locationManager:didEnterRegion:
  *    when the user enters the region. By default, this is YES.
  */
-@property (nonatomic, assign) BOOL notifyOnEntry __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_7_0);
+@property (nonatomic, assign) BOOL notifyOnEntry __OSX_AVAILABLE_STARTING(__MAC_10_10,__IPHONE_7_0);
 
 /*
  *  notifyOnExit
@@ -106,7 +111,7 @@
  *    App will be launched and the delegate will be notified via locationManager:didExitRegion:
  *    when the user exits the region. By default, this is YES.
  */
-@property (nonatomic, assign) BOOL notifyOnExit __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_7_0);
+@property (nonatomic, assign) BOOL notifyOnExit __OSX_AVAILABLE_STARTING(__MAC_10_10,__IPHONE_7_0);
 
 /*
  *  containsCoordinate:
@@ -116,7 +121,7 @@
  *
  *    This method has been deprecated, please see CLCircularRegion.
  */
-- (BOOL)containsCoordinate:(CLLocationCoordinate2D)coordinate __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7,__MAC_NA,__IPHONE_4_0,__IPHONE_7_0) __TVOS_PROHIBITED;
+- (BOOL)containsCoordinate:(CLLocationCoordinate2D)coordinate __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7,__MAC_10_10,__IPHONE_4_0,__IPHONE_7_0) __TVOS_PROHIBITED;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLVisit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLVisit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLVisit.h	2015-10-03 00:41:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLVisit.h	2016-06-01 05:03:00.000000000 +0200
@@ -9,6 +9,8 @@
 #import <Foundation/Foundation.h>
 #import <CoreLocation/CLLocation.h>
 
+#import <CoreLocation/CLAvailability.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 /*

```