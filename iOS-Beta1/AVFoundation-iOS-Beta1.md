#AVFoundation.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h	2016-09-22 23:56:42.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h	2016-10-22 04:44:53.000000000 +0200
@@ -346,11 +346,18 @@
 
 /*!
   @property		containsFragments
-  @abstract		Indicates whether the asset is extended by at least one movie fragment.
+  @abstract		Indicates whether the asset is extended by at least one fragment.
   @discussion	For QuickTime movie files and MPEG-4 files, the value of this property is YES if canContainFragments is YES and at least one 'moof' box is present after the 'moov' box.
 */
 @property (nonatomic, readonly) BOOL containsFragments NS_AVAILABLE(10_11, 9_0);
 
+/*!
+  @property		overallDurationHint
+  @abstract		Indicates the total duration of fragments that either exist now or may be appended in the future in order to extend the duration of the asset.
+  @discussion	For QuickTime movie files and MPEG-4 files, the value of this property is obtained from the 'mehd' box of the 'mvex' box, if present. If no total fragment duration hint is available, the value of this property is kCMTimeInvalid.
+*/
+@property (nonatomic, readonly) CMTime overallDurationHint NS_AVAILABLE(10_12_3, 10_3);
+
 @end
 
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureDevice.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureDevice.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureDevice.h	2016-09-24 02:45:16.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureDevice.h	2016-10-22 02:35:49.000000000 +0200
@@ -437,21 +437,27 @@
 AVF_EXPORT AVCaptureDeviceType const AVCaptureDeviceTypeBuiltInTelephotoCamera NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED;
 
 /*!
- @constant AVCaptureDeviceTypeBuiltInDuoCamera
+ @constant AVCaptureDeviceTypeBuiltInDualCamera
     A device that consists of two fixed focal length cameras, one wide and one telephoto. Note that devices of this type may only be discovered using an AVCaptureDeviceDiscoverySession.
 
     A device of this device type supports the following new features:
     - Auto switching from one camera to the other when zoom factor, light level, and focus position allow this.
-	- Higher quality zoom for still captures by fusing images from both cameras.
+    - Higher quality zoom for still captures by fusing images from both cameras.
 
     A device of this device type does not support the following features:
-	- AVCaptureExposureModeCustom and manual exposure bracketing.
+    - AVCaptureExposureModeCustom and manual exposure bracketing.
     - Locking focus with a lens position other than AVCaptureLensPositionCurrent.
-	- Locking auto white balance with device white balance gains other than AVCaptureWhiteBalanceGainsCurrent.
+    - Locking auto white balance with device white balance gains other than AVCaptureWhiteBalanceGainsCurrent.
 
     Even when locked, exposure duration, ISO, aperture, white balance gains, or lens position may change when the device switches from one camera to the other. The overall exposure, white balance, and focus position however should be consistent.
  */
-AVF_EXPORT AVCaptureDeviceType const AVCaptureDeviceTypeBuiltInDuoCamera NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED;
+AVF_EXPORT AVCaptureDeviceType const AVCaptureDeviceTypeBuiltInDualCamera NS_AVAILABLE_IOS(10_2) __TVOS_PROHIBITED;
+
+/*!
+ @constant AVCaptureDeviceTypeBuiltInDuoCamera
+    A deprecated synonym for AVCaptureDeviceTypeBuiltIntDualCamera. Please use AVCaptureDeviceTypeBuiltInDualCamera instead.
+ */
+AVF_EXPORT AVCaptureDeviceType const AVCaptureDeviceTypeBuiltInDuoCamera NS_DEPRECATED_IOS(10_0, 10_2, "Use AVCaptureDeviceTypeBuiltInDualCamera instead") __TVOS_PROHIBITED;
 
 @interface AVCaptureDevice (AVCaptureDeviceType)
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCapturePhotoOutput.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCapturePhotoOutput.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCapturePhotoOutput.h	2016-08-05 07:59:19.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCapturePhotoOutput.h	2016-10-22 02:05:25.000000000 +0200
@@ -169,6 +169,16 @@
 @property(nonatomic, readonly) BOOL isStillImageStabilizationScene;
 
 /*!
+ @property dualCameraFusionSupported
+ @abstract
+    Indicates whether the DualCamera image fusion feature is supported by the receiver.
+
+ @discussion
+    This property may change as the session's -sessionPreset or source device's -activeFormat change. When using the AVCaptureDevice with deviceType AVCaptureDeviceTypeBuiltInDualCamera, the wide-angle and telephoto camera images can be fused together to improve image quality in some configurations. When DualCamera image fusion is not supported by the current configuration, your capture requests always resolve dualCameraFusionEnabled to NO. This property is key-value observable.
+ */
+@property(nonatomic, readonly, getter=isDualCameraFusionSupported) BOOL dualCameraFusionSupported NS_AVAILABLE_IOS(10_2);
+
+/*!
  @property supportedFlashModes
  @abstract
     An array of AVCaptureFlashMode constants for the current capture session configuration.
@@ -515,7 +525,7 @@
     An instance of AVCapturePhotoSettings.
  
  @discussion
-    If you wish an uncompressed format, your dictionary must contain kCVPixelBufferPixelFormatTypeKey, and the format specified must be present in AVCapturePhotoOutput's -availablePhotoPixelFormatTypes array. kCVPixelBufferPixelFormatTypeKey is the only supported key when expressing uncompressed output. If you wish a compressed format, your dictionary must contain AVVideoCodecKey and the codec specified must be present in AVCapturePhotoOutput's -availablePhotoCodecTypes array. If you are specifying a compressed format, the AVVideoQualityKey is also supported. Passing a nil format dictionary is analogous to calling +photoSettings.
+    If you wish an uncompressed format, your dictionary must contain kCVPixelBufferPixelFormatTypeKey, and the format specified must be present in AVCapturePhotoOutput's -availablePhotoPixelFormatTypes array. kCVPixelBufferPixelFormatTypeKey is the only supported key when expressing uncompressed output. If you wish a compressed format, your dictionary must contain AVVideoCodecKey and the codec specified must be present in AVCapturePhotoOutput's -availablePhotoCodecTypes array. If you are specifying a compressed format, the AVVideoCompressionPropertiesKey is also supported, with a payload dictionary containing a single AVVideoQualityKey. Passing a nil format dictionary is analogous to calling +photoSettings.
  */
 + (instancetype)photoSettingsWithFormat:(nullable NSDictionary<NSString *, id> *)format;
 
@@ -547,7 +557,7 @@
     An instance of AVCapturePhotoSettings.
  
  @discussion
-    rawPixelFormatType must be one of the OSTypes contained in AVCapturePhotoOutput's -availableRawPhotoPixelFormatTypes array. If you wish an uncompressed processedFormat, your dictionary must contain kCVPixelBufferPixelFormatTypeKey, and the processedFormat specified must be present in AVCapturePhotoOutput's -availablePhotoPixelFormatTypes array. kCVPixelBufferPixelFormatTypeKey is the only supported key when expressing uncompressed processedFormat. If you wish a compressed format, your dictionary must contain AVVideoCodecKey and the codec specified must be present in AVCapturePhotoOutput's -availablePhotoCodecTypes array. If you are specifying a compressed format, the AVVideoQualityKey is also supported. Passing a nil processedFormat dictionary is analogous to calling +photoSettingsWithRawPixelFormatType:. See AVCapturePhotoOutput's -capturePhotoWithSettings:delegate: inline documentation for a discussion of restrictions on AVCapturePhotoSettings when requesting RAW capture.
+    rawPixelFormatType must be one of the OSTypes contained in AVCapturePhotoOutput's -availableRawPhotoPixelFormatTypes array. If you wish an uncompressed processedFormat, your dictionary must contain kCVPixelBufferPixelFormatTypeKey, and the processedFormat specified must be present in AVCapturePhotoOutput's -availablePhotoPixelFormatTypes array. kCVPixelBufferPixelFormatTypeKey is the only supported key when expressing uncompressed processedFormat. If you wish a compressed format, your dictionary must contain AVVideoCodecKey and the codec specified must be present in AVCapturePhotoOutput's -availablePhotoCodecTypes array. If you are specifying a compressed format, the AVVideoCompressionPropertiesKey is also supported, with a payload dictionary containing a single AVVideoQualityKey. Passing a nil processedFormat dictionary is analogous to calling +photoSettingsWithRawPixelFormatType:. See AVCapturePhotoOutput's -capturePhotoWithSettings:delegate: inline documentation for a discussion of restrictions on AVCapturePhotoSettings when requesting RAW capture.
  */
 + (instancetype)photoSettingsWithRawPixelFormatType:(OSType)rawPixelFormatType processedFormat:(nullable NSDictionary<NSString *, id> *)processedFormat;
 
@@ -617,6 +627,16 @@
 @property(nonatomic, getter=isAutoStillImageStabilizationEnabled) BOOL autoStillImageStabilizationEnabled;
 
 /*!
+ @property autoDualCameraFusionEnabled
+ @abstract
+    Specifies whether DualCamera image fusion should be used automatically.
+
+ @discussion
+    Default is YES unless you are capturing a RAW photo (RAW photos may not be processed by definition) or a bracket using AVCapturePhotoBracketSettings. When set to YES, and -[AVCapturePhotoOutput isDualCameraFusionSupported] is also YES, wide-angle and telephoto images may be fused to improve still image quality, depending on the current zoom factor, light levels, and focus position. You may determine whether DualCamera fusion is enabled for a particular capture request by inspecting the dualCameraFusionEnabled property of the AVCaptureResolvedPhotoSettings. Note that when using the deprecated AVCaptureStillImageOutput interface with the DualCamera, auto DualCamera fusion is always enabled and may not be turned off.
+ */
+@property(nonatomic, getter=isAutoDualCameraFusionEnabled) BOOL autoDualCameraFusionEnabled NS_AVAILABLE_IOS(10_2);
+
+/*!
  @property highResolutionPhotoEnabled
  @abstract
     Specifies whether photos should be captured at the highest resolution supported by the source AVCaptureDevice's activeFormat.
@@ -696,7 +716,7 @@
  @param rawPixelFormatType
     One of the OSTypes contained in AVCapturePhotoOutput's -availableRawPhotoPixelFormatTypes array. May be set to 0 if you do not desire RAW capture.
  @param processedFormat
-    A dictionary of Core Video pixel buffer attributes or AVVideoSettings, analogous to AVCaptureStillImageOutput's outputSettings property. If you wish an uncompressed format, your dictionary must contain kCVPixelBufferPixelFormatTypeKey, and the format specified must be present in AVCapturePhotoOutput's -availablePhotoPixelFormatTypes array. kCVPixelBufferPixelFormatTypeKey is the only supported key when expressing uncompressed output. If you wish a compressed format, your dictionary must contain AVVideoCodecKey and the codec specified must be present in AVCapturePhotoOutput's -availablePhotoCodecTypes array. If you are specifying a compressed format, the AVVideoQualityKey is also supported. If you only wish to capture RAW, you may pass a non-zero rawPixelFormatType and a nil processedFormat dictionary. If you pass a rawPixelFormatType of 0 AND a nil processedFormat dictionary, the default output of AVVideoCodecJPEG will be delivered.
+    A dictionary of Core Video pixel buffer attributes or AVVideoSettings, analogous to AVCaptureStillImageOutput's outputSettings property. If you wish an uncompressed format, your dictionary must contain kCVPixelBufferPixelFormatTypeKey, and the format specified must be present in AVCapturePhotoOutput's -availablePhotoPixelFormatTypes array. kCVPixelBufferPixelFormatTypeKey is the only supported key when expressing uncompressed output. If you wish a compressed format, your dictionary must contain AVVideoCodecKey and the codec specified must be present in AVCapturePhotoOutput's -availablePhotoCodecTypes array. If you are specifying a compressed format, the AVVideoCompressionPropertiesKey is also supported, with a payload dictionary containing a single AVVideoQualityKey. If you only wish to capture RAW, you may pass a non-zero rawPixelFormatType and a nil processedFormat dictionary. If you pass a rawPixelFormatType of 0 AND a nil processedFormat dictionary, the default output of AVVideoCodecJPEG will be delivered.
  @param bracketedSettings
     An array of AVCaptureBracketedStillImageSettings objects (defined in AVCaptureStillImageOutput.h). All must be of the same type, either AVCaptureManualExposureBracketedStillImageSettings or AVCaptureAutoExposureBracketedStillImageSettings. bracketedSettings.count must be <= AVCapturePhotoOutput's -maxBracketedCapturePhotoCount.
  @result
@@ -826,6 +846,13 @@
  */
 @property(readonly, getter=isStillImageStabilizationEnabled) BOOL stillImageStabilizationEnabled;
 
+/*!
+ @property dualCameraFusionEnabled
+ @abstract
+    Indicates whether DualCamera wide-angle and telephoto image fusion will be employed when capturing the photo.
+ */
+@property(readonly, getter=isDualCameraFusionEnabled) BOOL dualCameraFusionEnabled NS_AVAILABLE_IOS(10_2);
+
 @end
 
 NS_ASSUME_NONNULL_END

```