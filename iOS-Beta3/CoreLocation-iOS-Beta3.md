#CoreLocation.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocation.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocation.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocation.h	2016-06-27 06:01:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreLocation.framework/Headers/CLLocation.h	2016-07-10 08:15:32.000000000 +0200
@@ -259,7 +259,7 @@
  *  Range:
  *    0.0 - 359.9 degrees, 0 being true North
  */
-@property(readonly, nonatomic) CLLocationDirection course __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_2_2) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+@property(readonly, nonatomic) CLLocationDirection course __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_2_2) __TVOS_PROHIBITED;
 
 /*
  *  speed
@@ -267,7 +267,7 @@
  *  Discussion:
  *    Returns the speed of the location in m/s. Negative if speed is invalid.
  */
-@property(readonly, nonatomic) CLLocationSpeed speed __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_2_2) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+@property(readonly, nonatomic) CLLocationSpeed speed __OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_2_2) __TVOS_PROHIBITED;
 
 /*
  *  timestamp

```