#CoreLocation.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLAvailability.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLAvailability.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLAvailability.h	2016-05-16 02:07:13.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLAvailability.h	2016-06-27 04:30:34.000000000 +0200
@@ -22,10 +22,6 @@
 #define __WATCHOS_PROHIBITED
 #endif
 
-#ifndef CL_MAC_CODEBASE
-#define CL_MAC_CODEBASE !TARGET_OS_IPHONE
-#endif
-
 #ifdef __cplusplus
 #define CL_EXTERN extern "C" __attribute__((visibility ("default")))
 #else
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLHeading.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLHeading.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLHeading.h	2016-05-16 02:07:13.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLHeading.h	2016-06-27 04:30:34.000000000 +0200
@@ -111,14 +111,6 @@
  */
 @property(readonly, nonatomic, copy) NSDate *timestamp;
 
-/*
- *  description
- *  
- *  Discussion:
- *    Returns a string representation of the heading.
- */
-@property (nonatomic, readonly, copy) NSString *description;
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocation.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocation.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocation.h	2016-05-22 06:00:55.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocation.h	2016-06-27 06:01:45.000000000 +0200
@@ -288,14 +288,6 @@
 @property(readonly, nonatomic, copy, nullable) CLFloor *floor __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_8_0);
 
 /*
- *  description
- *  
- *  Discussion:
- *    Returns a string representation of the location.
- */
-@property (nonatomic, readonly, copy) NSString *description;
-
-/*
  *  getDistanceFrom:
  *
  *  Discussion:
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager+CLVisitExtensions.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager+CLVisitExtensions.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager+CLVisitExtensions.h	2016-05-16 02:07:13.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager+CLVisitExtensions.h	2016-06-27 04:30:34.000000000 +0200
@@ -9,7 +9,6 @@
 #import <CoreLocation/CLLocationManager.h>
 
 #import <CoreLocation/CLAvailability.h>
-#if !CL_MAC_CODEBASE // whole file
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -44,4 +43,3 @@
 @end
 
 NS_ASSUME_NONNULL_END
-#endif // whole file
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager.h	2016-06-01 05:54:00.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager.h	2016-06-27 06:01:45.000000000 +0200
@@ -408,7 +408,7 @@
  *  Discussion:
  *      Start updating locations.
  */
-- (void)startUpdatingLocation __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+- (void)startUpdatingLocation __TVOS_PROHIBITED;
 
 /*
  *  stopUpdatingLocation
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLVisit.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLVisit.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLVisit.h	2016-05-16 02:07:13.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLVisit.h	2016-06-27 04:30:34.000000000 +0200
@@ -10,7 +10,6 @@
 #import <CoreLocation/CLLocation.h>
 
 #import <CoreLocation/CLAvailability.h>
-#if !CL_MAC_CODEBASE // whole file
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -62,4 +61,3 @@
 @end
 
 NS_ASSUME_NONNULL_END
-#endif // whole file

```