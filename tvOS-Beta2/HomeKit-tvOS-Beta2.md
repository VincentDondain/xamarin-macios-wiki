#HomeKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryCategoryTypes.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryCategoryTypes.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryCategoryTypes.h	2016-05-26 07:14:11.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryCategoryTypes.h	2016-06-29 05:45:57.000000000 +0200
@@ -52,7 +52,7 @@
 /*
 * @brief Category type for IP Camera.
 */
-HM_EXTERN NSString * const HMAccessoryCategoryTypeIPCamera NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0);
+HM_EXTERN NSString * const HMAccessoryCategoryTypeIPCamera NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Category type for Lightbulb.
@@ -90,6 +90,11 @@
 HM_EXTERN NSString * const HMAccessoryCategoryTypeThermostat NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
+ * @brief Category type for Video Doorbell.
+ */
+HM_EXTERN NSString * const HMAccessoryCategoryTypeVideoDoorbell NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
  * @brief Category type for Window.
  */
 HM_EXTERN NSString * const HMAccessoryCategoryTypeWindow NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraStream.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraStream.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraStream.h	2016-05-26 07:14:11.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraStream.h	2016-06-29 05:45:57.000000000 +0200
@@ -20,7 +20,26 @@
 /*!
  * @brief Represents the audio setting for the current stream.
  */
-@property(assign, nonatomic) HMCameraAudioStreamSetting audioStreamSetting;
+@property (assign, nonatomic, readonly) HMCameraAudioStreamSetting audioStreamSetting __TVOS_PROHIBITED;
+
+/*!
+ * @brief Sets the audio stream setting.
+ *
+ * @param audioStreamSetting New audio stream setting.
+ *
+ */
+- (void)setAudioStreamSetting:(HMCameraAudioStreamSetting)audioStreamSetting __TVOS_PROHIBITED API_DEPRECATED_WITH_REPLACEMENT("updateAudioStreamSetting:completionHandler:", ios(10.0, 10.0), watchos(3.0, 3.0));
+
+/*!
+ * @brief Updates the settings of the audio stream.
+ *
+ * @param audioStreamSetting New audio stream setting.
+ *
+ * @param completion Block that is invoked once the request is processed.
+ *                   The NSError provides more information on the status of the request, error
+ *                   will be nil on success.
+ */
+- (void)updateAudioStreamSetting:(HMCameraAudioStreamSetting)audioStreamSetting completionHandler:(void (^)(NSError * __nullable error))completion __TVOS_PROHIBITED;
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraStreamControl.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraStreamControl.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraStreamControl.h	2016-05-26 07:14:11.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraStreamControl.h	2016-06-29 05:45:57.000000000 +0200
@@ -71,7 +71,7 @@
  *
  * @param error When stream stops because of an error, 'error' will be populated.
  */
-- (void)cameraStreamControl:(HMCameraStreamControl *)cameraStreamControl didStopStreamWithError:(NSError *)error;
+- (void)cameraStreamControl:(HMCameraStreamControl *)cameraStreamControl didStopStreamWithError:(NSError *__nullable)error;
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicTypes.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicTypes.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicTypes.h	2016-05-26 07:14:11.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicTypes.h	2016-06-27 08:09:38.000000000 +0200
@@ -312,7 +312,8 @@
 
 /*!
  * @brief Characteristic type for current position of a door/window. The value of the characteristic is an
- *        uint8 value in percent.
+ *        uint8 value in percent. A value of 0 indicates closed/most shade/least light allowed state and a
+ *        value of 100 indicates open/no shade/most light allowed state.
  */
 HM_EXTERN NSString * const HMCharacteristicTypeCurrentPosition NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
@@ -428,10 +429,9 @@
 HM_EXTERN NSString * const HMCharacteristicTypeTargetSecuritySystemState NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
- * @brief Characteristic type for target position of a door/window. The value of the characteristic is an
- *        uint8 value in percent. For shades/awnings, a value of 0 indicates no shade and a value of 100
- *        indicates most shade. For blinds, a value of 0 indicates most light is allowed in and 100
- *        indicates least light is allowed.
+ * @brief Characteristic type for target position of a door/window/window covering. The value of the
+ *        characteristic is an uint8 value in percent. A value of 0 indicates closed/most shade/least
+ *        light allowed state and a value of 100 indicates open/no shade/most light allowed state.
  */
 HM_EXTERN NSString * const HMCharacteristicTypeTargetPosition NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
@@ -446,6 +446,11 @@
 HM_EXTERN NSString * const HMCharacteristicTypeStreamingStatus NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
 
 /*!
+ * @brief Characteristic type for setup stream endpoint. The value is a tlv8 data.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeSetupStreamEndpoint NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
  * @brief Characteristic type for supported video stream configuration. The value is a tlv8 data.
  */
 HM_EXTERN NSString * const HMCharacteristicTypeSupportedVideoStreamConfiguration NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMError.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMError.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMError.h	2016-05-28 06:33:50.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMError.h	2016-06-27 06:50:35.000000000 +0200
@@ -101,6 +101,9 @@
     HMErrorCodeLocationForHomeDisabled                 NS_ENUM_AVAILABLE_IOS(9_0) = 84,
     HMErrorCodeNotAuthorizedForLocationServices        NS_ENUM_AVAILABLE_IOS(9_0) = 85,
     HMErrorCodeReferToUserManual                       NS_ENUM_AVAILABLE_IOS(9_3) = 86,
+    HMErrorCodeInvalidOrMissingAuthorizationData       NS_ENUM_AVAILABLE_IOS(10) = 87,
+    HMErrorCodeBridgedAccessoryNotReachable            NS_ENUM_AVAILABLE_IOS(10) = 88,
+    HMErrorCodeNotAuthorizedForMicrophoneAccess        NS_ENUM_AVAILABLE_IOS(10) = 89,
 } NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMServiceTypes.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMServiceTypes.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMServiceTypes.h	2016-05-23 08:18:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMServiceTypes.h	2016-06-29 07:12:58.000000000 +0200
@@ -91,6 +91,11 @@
 HM_EXTERN NSString * const HMServiceTypeDoor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
+ * @brief Service type for doorbell.
+ */
+HM_EXTERN NSString * const HMServiceTypeDoorbell NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
  * @brief Service type for humidity sensor.
  */
 HM_EXTERN NSString * const HMServiceTypeHumiditySensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
@@ -150,9 +155,24 @@
  */
 HM_EXTERN NSString * const HMServiceTypeWindowCovering NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
+/*!
+ * @brief Service type for stream management.
+ */
 HM_EXTERN NSString * const HMServiceTypeCameraRTPStreamManagement NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ * @brief Service type for camera control.
+ */
 HM_EXTERN NSString * const HMServiceTypeCameraControl NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ * @brief Service type for microphone.
+ */
 HM_EXTERN NSString * const HMServiceTypeMicrophone NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ * @brief Service type for speaker.
+ */
 HM_EXTERN NSString * const HMServiceTypeSpeaker NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
 
 NS_ASSUME_NONNULL_END

```