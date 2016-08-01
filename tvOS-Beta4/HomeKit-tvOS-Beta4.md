#HomeKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryProfile.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryProfile.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryProfile.h	2016-07-13 06:01:10.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryProfile.h	2016-07-25 09:09:14.000000000 +0200
@@ -15,7 +15,7 @@
 /*!
  * @abstract Represents a profile implemented by an accessory.
  */
-__IOS_AVAILABLE(__IPHONE_10_0) __WATCHOS_AVAILABLE(__WATCHOS_3_0) __TVOS_AVAILABLE(__TVOS_10_0)
+__IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0)
 @interface HMAccessoryProfile : NSObject
 
 - (instancetype)init NS_UNAVAILABLE;

```