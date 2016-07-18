#HomeKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshot.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshot.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshot.h	2016-06-29 07:12:58.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshot.h	2016-07-13 05:37:17.000000000 +0200
@@ -13,6 +13,7 @@
 /*!
  * @abstract Represents a camera snapshot.
  */
+__IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0)
 @interface HMCameraSnapshot : HMCameraSource
 
 /*!
```