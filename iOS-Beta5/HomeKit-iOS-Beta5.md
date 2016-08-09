#HomeKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicTypes.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicTypes.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicTypes.h	2016-07-27 08:18:49.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicTypes.h	2016-08-06 09:54:04.000000000 +0200
@@ -471,7 +471,7 @@
 HM_EXTERN NSString * const HMCharacteristicTypeSelectedStreamConfiguration NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
 
 /*!
- * @brief Characteristic type for image snapshot control point. The value is a tlv8 data.
+ * @brief Characteristic type for volume control. The value is float.
  */
 HM_EXTERN NSString * const HMCharacteristicTypeVolume NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
 

```