#AVFoundation.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCapturePhotoOutput.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCapturePhotoOutput.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCapturePhotoOutput.h	2016-05-25 04:40:24.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCapturePhotoOutput.h	2016-06-27 06:04:33.000000000 +0200
@@ -162,12 +162,9 @@
     Settings that govern the behavior of isFlashScene and isStillImageStabilizationScene.
 
  @discussion
-    You can influence the return values of isFlashScene and isStillImageStabilizationScene by setting this property, indicating the flashMode and autoStillImageStabilizationEnabled values that should be considered for scene monitoring. For instance, if you set flashMode to AVCaptureFlashModeOff, isFlashScene always reports NO. If you set it to AVCaptureFlashModeAuto or AVCaptureFlashModeOn, isFlashScene answers YES or NO based on the current scene's lighting conditions. Note that there is some overlap in the light level ranges that benefit from still image stabilization and flash. If your photoSettingsForSceneMonitoring indicate that both still image stabilization and flash scenes should be monitored, still image stabilization takes precedence, and isFlashScene becomes YES at lower overall light levels. The default values for this property are as follows:
-     
-     - flashMode == AVCaptureFlashModeAuto.
-     - autoStillImageStabilizationEnabled == YES.
+    You can influence the return values of isFlashScene and isStillImageStabilizationScene by setting this property, indicating the flashMode and autoStillImageStabilizationEnabled values that should be considered for scene monitoring. For instance, if you set flashMode to AVCaptureFlashModeOff, isFlashScene always reports NO. If you set it to AVCaptureFlashModeAuto or AVCaptureFlashModeOn, isFlashScene answers YES or NO based on the current scene's lighting conditions. Note that there is some overlap in the light level ranges that benefit from still image stabilization and flash. If your photoSettingsForSceneMonitoring indicate that both still image stabilization and flash scenes should be monitored, still image stabilization takes precedence, and isFlashScene becomes YES at lower overall light levels. The default value for this property is nil. See isStillImageStabilizationScene and isFlashScene for further discussion.
  */
-@property(nonatomic, copy) AVCapturePhotoSettings *photoSettingsForSceneMonitoring;
+@property(nullable, nonatomic, copy) AVCapturePhotoSettings *photoSettingsForSceneMonitoring;
 
 /*!
  @property highResolutionCaptureEnabled
@@ -678,7 +675,7 @@
  
     AVCapturePhotoBracketSettings do not support flashMode, autoStillImageStabilizationEnabled, livePhotoMovieFileURL or livePhotoMovieMetadata.
  */
-- (instancetype)initWithFormat:(nullable NSDictionary<NSString *, id> *)format rawPixelFormatType:(OSType)rawPixelFormatType bracketedSettings:(NSArray<AVCaptureBracketedStillImageSettings *> *)bracketedSettings;
++ (instancetype)photoBracketSettingsWithRawPixelFormatType:(OSType)rawPixelFormatType processedFormat:(nullable NSDictionary<NSString *, id> *)processedFormat bracketedSettings:(NSArray<AVCaptureBracketedStillImageSettings *> *)bracketedSettings;
 
 /*!
  @property bracketedSettings
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureStillImageOutput.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureStillImageOutput.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureStillImageOutput.h	2016-05-24 07:21:25.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureStillImageOutput.h	2016-06-27 06:16:15.000000000 +0200
@@ -218,7 +218,7 @@
  @discussion
     AVCaptureStillImageOutput can only satisfy a limited number of image requests in a single bracket without exhausting system resources. The maximum number of still images that may be taken in a single bracket depends on the size of the images being captured, and consequently may vary with AVCaptureSession -sessionPreset and AVCaptureDevice -activeFormat. Some formats do not support bracketed capture and return a maxBracketedCaptureStillImageCount of 0. This read-only property is key-value observable. If you exceed -maxBracketedCaptureStillImageCount, then -captureStillImageBracketAsynchronouslyFromConnection:withSettingsArray:completionHandler: fails and the completionHandler is called [settings count] times with a NULL sample buffer and AVErrorMaximumStillImageCaptureRequestsExceeded.
  */
-@property(nonatomic, readonly) NSUInteger maxBracketedCaptureStillImageCount NS_AVAILABLE_IOS(8_0);
+@property(nonatomic, readonly) NSUInteger maxBracketedCaptureStillImageCount NS_DEPRECATED_IOS(8_0, 10_0, "Use AVCapturePhotoOutput maxBracketedCapturePhotoCount instead");
 
 /*!
  @property lensStabilizationDuringBracketedCaptureSupported
@@ -228,7 +228,7 @@
  @discussion
     The receiver's lensStabilizationDuringBracketedCaptureEnabled property can only be set if this property returns YES. Its value may change as the session's -sessionPreset or input device's -activeFormat changes. This read-only property is key-value observable.
  */
-@property(nonatomic, readonly, getter=isLensStabilizationDuringBracketedCaptureSupported) BOOL lensStabilizationDuringBracketedCaptureSupported NS_AVAILABLE_IOS(9_0);
+@property(nonatomic, readonly, getter=isLensStabilizationDuringBracketedCaptureSupported) BOOL lensStabilizationDuringBracketedCaptureSupported NS_DEPRECATED_IOS(9_0, 10_0, "Use AVCapturePhotoOutput lensStabilizationDuringBracketedCaptureSupported instead");
 
 /*!
  @property lensStabilizationDuringBracketedCaptureEnabled
@@ -238,7 +238,7 @@
  @discussion
     On a receiver where -isLensStabilizationDuringBracketedCaptureSupported returns YES, lens stabilization may be applied to the bracket to reduce blur commonly found in low light photos. When lens stabilization is enabled, bracketed still image captures incur additional latency. Lens stabilization is more effective with longer-exposure captures, and offers limited or no benefit for exposure durations shorter than 1/30 of a second. It is possible that during the bracket, the lens stabilization module may run out of correction range and therefore will not be active for every frame in the bracket. Each emitted CMSampleBuffer from the bracket will have an attachment of kCMSampleBufferAttachmentKey_StillImageLensStabilizationInfo indicating additional information about stabilization was applied to the buffer, if any. The default value of -isLensStabilizationDuringBracketedCaptureEnabled is NO. This value will be set to NO when -isLensStabilizationDuringBracketedCaptureSupported changes to NO. Setting this property throws an NSInvalidArgumentException if -isLensStabilizationDuringBracketedCaptureSupported returns NO. This property is key-value observable.
  */
-@property(nonatomic, getter=isLensStabilizationDuringBracketedCaptureEnabled) BOOL lensStabilizationDuringBracketedCaptureEnabled NS_AVAILABLE_IOS(9_0);
+@property(nonatomic, getter=isLensStabilizationDuringBracketedCaptureEnabled) BOOL lensStabilizationDuringBracketedCaptureEnabled NS_DEPRECATED_IOS(9_0, 10_0, "Use AVCapturePhotoOutput with AVCapturePhotoBracketSettings instead");
 
 /*!
  @method prepareToCaptureStillImageBracketFromConnection:withSettingsArray:completionHandler:
@@ -258,7 +258,7 @@
     -maxBracketedCaptureStillImageCount tells you the maximum number of images that may be taken in a single bracket given the current AVCaptureDevice/AVCaptureSession/AVCaptureStillImageOutput configuration. But before taking a still image bracket, additional resources may need to be allocated. By calling -prepareToCaptureStillImageBracketFromConnection:withSettingsArray:completionHandler: first, you are able to deterministically know when the receiver is ready to capture the bracket with the specified settings array.
 
  */
-- (void)prepareToCaptureStillImageBracketFromConnection:(AVCaptureConnection *)connection withSettingsArray:(NSArray *)settings completionHandler:(void (^)(BOOL prepared, NSError *error))handler NS_AVAILABLE_IOS(8_0);
+- (void)prepareToCaptureStillImageBracketFromConnection:(AVCaptureConnection *)connection withSettingsArray:(NSArray *)settings completionHandler:(void (^)(BOOL prepared, NSError *error))handler NS_DEPRECATED_IOS(8_0, 10_0, "Use AVCapturePhotoOutput setPreparedPhotoSettingsArray:completionHandler: instead");
 
 /*!
  @method captureStillImageBracketAsynchronouslyFromConnection:withSettingsArray:completionHandler:
@@ -277,7 +277,7 @@
  @discussion
     If you have not called -prepareToCaptureStillImageBracketFromConnection:withSettingsArray:completionHandler: for this still image bracket request, the bracket may not be taken immediately, as the receiver may internally need to prepare resources.
  */
-- (void)captureStillImageBracketAsynchronouslyFromConnection:(AVCaptureConnection *)connection withSettingsArray:(NSArray *)settings completionHandler:(void (^)(CMSampleBufferRef sampleBuffer, AVCaptureBracketedStillImageSettings *stillImageSettings, NSError *error))handler NS_AVAILABLE_IOS(8_0);
+- (void)captureStillImageBracketAsynchronouslyFromConnection:(AVCaptureConnection *)connection withSettingsArray:(NSArray *)settings completionHandler:(void (^)(CMSampleBufferRef sampleBuffer, AVCaptureBracketedStillImageSettings *stillImageSettings, NSError *error))handler NS_DEPRECATED_IOS(8_0, 10_0, "Use AVCapturePhotoOutput capturePhotoWithSettings:delegate: instead");
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItem.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItem.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItem.h	2016-05-25 04:39:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItem.h	2016-06-27 06:16:16.000000000 +0200
@@ -957,6 +957,14 @@
 @property (nonatomic, readonly) double indicatedBitrate;
 
 /*!
+ @property		indicatedAverageBitrate
+ @abstract		Average throughput required to play the stream, as advertised by the server. Measured in bits per second.
+ @discussion	Value is negative if unknown. Corresponds to "sc-indicated-avg-bitrate".
+ This property is not observable.
+ */
+@property (nonatomic, readonly) double indicatedAverageBitrate NS_AVAILABLE(10_12, 10_0);
+
+/*!
  @property		averageVideoBitrate
  @abstract		The average bitrate of video track if it is unmuxed. Average bitrate of combined content if muxed. Measured in bits per second.
  @discussion	Value is negative if unknown. Corresponds to "c-avg-video-bitrate".
```