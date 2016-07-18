#HomeKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshot.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshot.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshot.h	2016-06-29 05:45:57.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshot.h	2016-07-13 06:01:10.000000000 +0200
@@ -13,6 +13,7 @@
 /*!
  * @abstract Represents a camera snapshot.
  */
+__IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0)
 @interface HMCameraSnapshot : HMCameraSource
 
 /*!
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMService.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMService.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMService.h	2016-06-27 06:50:35.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMService.h	2016-07-13 06:00:32.000000000 +0200
@@ -101,13 +101,19 @@
 - (void)updateName:(NSString *)name completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
- * @brief This method is used to set up the service type of the device connected to a switch or an outlet.
+ * @brief This method is used to set up the service type of the device connected to a contact sensor, switch or an outlet.
  *
- * @param serviceType Service type of the device connected to a switch/outlet service.
+ * @param serviceType Service type of the device connected to a contact sensor/switch/outlet service.
  *
- * @discussion This method is only valid for services of type HMServiceTypeOutlet and HMServiceTypeSwitch.
- *             serviceType can be any of the HomeKit Accessory Profile defined services (except HMServiceTypeOutlet
- *             or HMServiceTypeSwitch) that supports HMCharacteristicTypePowerState characteristic.
+ * @discussion This method is only valid for the services of the following types:
+ *                 HMServiceTypeOutlet, HMServiceTypeContactSensor and HMServiceTypeSwitch
+ *
+ *             For services of type HMServiceTypeOutlet and HMServiceTypeSwitch, serviceType can be one of the
+ *             HomeKit Accessory Profile defined services (except HMServiceTypeOutlet or HMServiceTypeSwitch)
+ *             that supports HMCharacteristicTypePowerState characteristic.
+ *
+ *             For services of type HMServiceTypeContactSensor, serviceType can be one of the following services:
+ *                 HMServiceTypeDoor, HMServiceTypeGarageDoorOpener, HMServiceTypeWindow and HMServiceTypeWindowCovering
  *
  * @param completion Block that is invoked once the request is processed.
  *                   The NSError provides more information on the status of the request, error

```