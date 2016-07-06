#CoreLocation.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLHeading.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLHeading.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLHeading.h	2016-06-01 05:03:00.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLHeading.h	2016-06-27 07:31:31.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocation.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocation.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocation.h	2016-05-22 06:00:55.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocation.h	2016-06-27 06:01:45.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager.h	2016-06-01 05:54:00.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocationManager.h	2016-06-27 06:01:45.000000000 +0200
@@ -408,7 +408,7 @@
  *  Discussion:
  *      Start updating locations.
  */
-- (void)startUpdatingLocation __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+- (void)startUpdatingLocation __TVOS_PROHIBITED;
 
 /*
  *  stopUpdatingLocation

```