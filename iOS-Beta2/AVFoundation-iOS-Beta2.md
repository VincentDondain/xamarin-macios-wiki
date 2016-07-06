#AVFoundation.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h	2016-05-25 07:22:12.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h	2016-06-27 06:16:12.000000000 +0200
@@ -3,7 +3,7 @@
 
 	Framework:  AVFoundation
  
-	Copyright 2010-2015 Apple Inc. All rights reserved.
+	Copyright 2010-2016 Apple Inc. All rights reserved.
 
 */
 
@@ -324,7 +324,10 @@
 
 @interface AVAsset (AVAssetProtectedContent)
 
-/* Indicates whether or not the asset has protected content.
+/*!
+  @property		hasProtectedContent
+  @abstract		Indicates whether or not the asset has protected content.
+  @discussion	Assets containing protected content may not be playable without successful authorization, even if the value of the "playable" property is YES.  See the properties in the AVAssetUsability category for details on how such an asset may be used.  On OS X, clients can use the interfaces in AVPlayerItemProtectedContentAdditions.h to request authorization to play the asset.
 */
 @property (nonatomic, readonly) BOOL hasProtectedContent NS_AVAILABLE(10_7, 4_2);
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetWriterInput.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetWriterInput.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetWriterInput.h	2016-05-04 00:21:25.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetWriterInput.h	2016-06-27 06:04:30.000000000 +0200
@@ -256,7 +256,14 @@
  
  @discussion
 	The timing information in the sample buffer, considered relative to the time passed to -[AVAssetWriter startSessionAtSourceTime:], will be used to determine the timing of those samples in the output file.
- 
+
+	For track types other than audio tracks, to determine the duration of all samples in the output file other than the very last sample that's appended, the difference between the sample buffer's output DTS and the following sample buffer's output DTS will be used. The duration of the last sample is determined as follows:
+	1. If a marker sample buffer with kCMSampleBufferAttachmentKey_EndsPreviousSampleDuration is appended following the last media-bearing sample, the difference between the output DTS of the marker sample buffer and the output DTS of the last media-bearing sample will be used.
+	2. If the marker sample buffer is not provided and if the output duration of the last media-bearing sample is valid, it will be used.
+	3. if the output duration of the last media-bearing sample is not valid, the duration of the second-to-last sample will be used.
+
+	For audio tracks, the properties of each appended sample buffer are used to determine corresponding output durations.
+
 	The receiver will retain the CMSampleBuffer until it is done with it, and then release it.  Do not modify a CMSampleBuffer or its contents after you have passed it to this method.
  
 	If the sample buffer contains audio data and the AVAssetWriterInput was intialized with an outputSettings dictionary then the format must be linear PCM. If the outputSettings dictionary was nil then audio data can be provided in a compressed format, and it will be passed through to the output without any re-compression. Note that advanced formats like AAC will have encoder delay present in their bitstreams. This data is inserted by the encoder and is necessary for proper decoding, but it is not meant to be played back. Clients who provide compressed audio bitstreams must use kCMSampleBufferAttachmentKey_TrimDurationAtStart to mark the encoder delay (generally restricted to the first sample buffer). Packetization can cause there to be extra audio frames in the last packet which are not meant to be played back. These remainder frames should be marked with kCMSampleBufferAttachmentKey_TrimDurationAtEnd. CMSampleBuffers obtained from AVAssetReader will already have the necessary trim attachments. Please see http://developer.apple.com/mac/library/technotes/tn2009/tn2258.html for more information about encoder delay. When attaching trims make sure that the output PTS of the sample buffer is what you expect. For example if you called -[AVAssetWriter startSessionAtSourceTime:kCMTimeZero] and you want your audio to start at time zero in the output file then make sure that the output PTS of the first non-fully trimmed audio sample buffer is kCMTimeZero.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCapturePhotoOutput.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCapturePhotoOutput.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCapturePhotoOutput.h	2016-05-25 04:40:24.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCapturePhotoOutput.h	2016-06-27 06:04:33.000000000 +0200
@@ -132,7 +132,7 @@
     Indicates whether the current scene is dark enough to warrant use of still image stabilization.
 
  @discussion
-    This property reports whether the current scene being previewed by the camera is dark enough to benefit from still image stabilization. You can influence this property's answers by setting the photoSettingsForSceneMonitoring property, indicating whether autoStillImageStabilization monitoring should be on or off. If you set autoStillImageStabilization to NO, isStillImageStabilizationScene always reports NO. If you set it to YES, this property returns YES or NO depending on the current scene's lighting conditions. Note that some very dark scenes do not benefit from still image stabilization, but do benefit from flash. This property may be key-value observed.
+    This property reports whether the current scene being previewed by the camera is dark enough to benefit from still image stabilization. You can influence this property's answers by setting the photoSettingsForSceneMonitoring property, indicating whether autoStillImageStabilization monitoring should be on or off. If you set autoStillImageStabilization to NO, isStillImageStabilizationScene always reports NO. If you set it to YES, this property returns YES or NO depending on the current scene's lighting conditions. Note that some very dark scenes do not benefit from still image stabilization, but do benefit from flash. By default, this property always returns NO unless you set photoSettingsForSceneMonitoring to a non-nil value. This property may be key-value observed.
  */
 @property(nonatomic, readonly) BOOL isStillImageStabilizationScene;
 
@@ -152,7 +152,7 @@
     Indicates whether the current scene is dark enough to warrant use of the flash.
 
  @discussion
-    This property reports whether the current scene being previewed by the camera is dark enough to need the flash. If -supportedFlashModes only contains AVCaptureFlashModeOff, isFlashScene always reports NO. You can influence this property's answers by setting the photoSettingsForSceneMonitoring property, indicating the flashMode you wish to monitor. If you set flashMode to AVCaptureFlashModeOff, isFlashScene always reports NO. If you set it to AVCaptureFlashModeAuto or AVCaptureFlashModeOn, isFlashScene answers YES or NO based on the current scene's lighting conditions. By default, isFlashScene assumes your desired flashMode is AVCaptureFlashModeAuto. Note that there is some overlap in the light level ranges that benefit from still image stabilization and flash. If your photoSettingsForSceneMonitoring indicate that both still image stabilization and flash scenes should be monitored, still image stabilization takes precedence, and isFlashScene becomes YES at lower overall light levels. This property may be key-value observed.
+    This property reports whether the current scene being previewed by the camera is dark enough to need the flash. If -supportedFlashModes only contains AVCaptureFlashModeOff, isFlashScene always reports NO. You can influence this property's answers by setting the photoSettingsForSceneMonitoring property, indicating the flashMode you wish to monitor. If you set flashMode to AVCaptureFlashModeOff, isFlashScene always reports NO. If you set it to AVCaptureFlashModeAuto or AVCaptureFlashModeOn, isFlashScene answers YES or NO based on the current scene's lighting conditions. By default, this property always returns NO unless you set photoSettingsForSceneMonitoring to a non-nil value. Note that there is some overlap in the light level ranges that benefit from still image stabilization and flash. If your photoSettingsForSceneMonitoring indicate that both still image stabilization and flash scenes should be monitored, still image stabilization takes precedence, and isFlashScene becomes YES at lower overall light levels. This property may be key-value observed.
  */
 @property(nonatomic, readonly) BOOL isFlashScene;
 
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
@@ -648,7 +645,7 @@
     A concrete subclass of AVCapturePhotoSettings that describes a bracketed capture.
  
  @discussion
-    In addition to the properties expressed in the base class, an AVCapturePhotoBracketSettings contains an array of AVCaptureBracketedStillImageSettings objects, where each describes one individual photo in the bracket. bracketedSettings.count must be <= AVCapturePhotoOutput's -maxBracketedCapturePhotoCount. Capturing a photo bracket may require the allocation of additional resources. By calling -prepareToCapturePhotoWithSettings:completionHandler: in advance, you can deterministically know when the AVCapturePhotoOutput instance is ready to capture a bracket with the given settings with no additional delay for allocation.
+    In addition to the properties expressed in the base class, an AVCapturePhotoBracketSettings contains an array of AVCaptureBracketedStillImageSettings objects, where each describes one individual photo in the bracket. bracketedSettings.count must be <= AVCapturePhotoOutput's -maxBracketedCapturePhotoCount. Capturing a photo bracket may require the allocation of additional resources.
 
     When you request a bracketed capture, your AVCapturePhotoCaptureDelegate's -captureOutput:didFinishProcessing{Photo | RawPhoto}... callbacks are called back bracketSettings.count times and provided with the corresponding AVCaptureBracketedStillImageSettings object from your request.
  */
@@ -660,14 +657,14 @@
 }
 
 /*!
- @method initWithFormat:rawPixelFormatType:bracketedSettings:
+ @method photoBracketSettingsWithRawPixelFormatType:processedFormat:bracketedSettings:
  @abstract
     Creates an instance of AVCapturePhotoBracketSettings.
  
- @param format
-    A dictionary of Core Video pixel buffer attributes or AVVideoSettings, analogous to AVCaptureStillImageOutput's outputSettings property. If you wish an uncompressed format, your dictionary must contain kCVPixelBufferPixelFormatTypeKey, and the format specified must be present in AVCapturePhotoOutput's -availablePhotoPixelFormatTypes array. kCVPixelBufferPixelFormatTypeKey is the only supported key when expressing uncompressed output. If you wish a compressed format, your dictionary must contain AVVideoCodecKey and the codec specified must be present in AVCapturePhotoOutput's -availablePhotoCodecTypes array. If you are specifying a compressed format, the AVVideoQualityKey is also supported. If you only wish to capture RAW, you may pass a nil format dictionary and a non-zero rawPixelFormatType. If you pass a nil format dictionary AND a rawPixelFormatType of 0, the default output of AVVideoCodecJPEG will be delivered.
  @param rawPixelFormatType
     One of the OSTypes contained in AVCapturePhotoOutput's -availableRawPhotoPixelFormatTypes array. May be set to 0 if you do not desire RAW capture.
+ @param processedFormat
+    A dictionary of Core Video pixel buffer attributes or AVVideoSettings, analogous to AVCaptureStillImageOutput's outputSettings property. If you wish an uncompressed format, your dictionary must contain kCVPixelBufferPixelFormatTypeKey, and the format specified must be present in AVCapturePhotoOutput's -availablePhotoPixelFormatTypes array. kCVPixelBufferPixelFormatTypeKey is the only supported key when expressing uncompressed output. If you wish a compressed format, your dictionary must contain AVVideoCodecKey and the codec specified must be present in AVCapturePhotoOutput's -availablePhotoCodecTypes array. If you are specifying a compressed format, the AVVideoQualityKey is also supported. If you only wish to capture RAW, you may pass a non-zero rawPixelFormatType and a nil processedFormat dictionary. If you pass a rawPixelFormatType of 0 AND a nil processedFormat dictionary, the default output of AVVideoCodecJPEG will be delivered.
  @param bracketedSettings
     An array of AVCaptureBracketedStillImageSettings objects (defined in AVCaptureStillImageOutput.h). All must be of the same type, either AVCaptureManualExposureBracketedStillImageSettings or AVCaptureAutoExposureBracketedStillImageSettings. bracketedSettings.count must be <= AVCapturePhotoOutput's -maxBracketedCapturePhotoCount.
  @result
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoComposition.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoComposition.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoComposition.h	2016-05-25 04:40:26.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoComposition.h	2016-06-27 04:08:29.000000000 +0200
@@ -97,17 +97,11 @@
  @discussion
     Collectively the properties colorPrimaries, colorYCbCrMatrix, and colorTransferFunction define the color space that the rendered frames will be tagged with. For custom video compositing these properties are also used to specify the required color space of the source frames.
 
-    Examples of common color spaces:
-	
-        TODO: SD
-        TODO: HD
-        TODO: HD-P3
+    For examples of common color spaces see AVVideoSettings.h.
 
     How to preserve the color space of the source frames:
  
         Decide which color space to be preserved by examining the source asset's video tracks. Copy the source track's primaries, matrix and transfer function into the video composition's colorPrimaries, colorYCbCrMatrix and colorTransferFunction respectively.
-		
-        TODO: <rdar://problem/25496972> sample code showing how to inspect the source asset track's primaries etc and setup a video composition to preserve them. Ideally we'll show the narrow-HD case and the wide-P3 case.
 
         - When using custom video compositing
 			Setting these properties will cause source frames to be converted into the specified color space and tagged as such. New frames allocated using -[AVVideoCompositionRenderContext newPixelBuffer] will also be tagged correctly.
@@ -266,17 +260,11 @@
  @discussion
     Collectively the properties colorPrimaries, colorYCbCrMatrix, and colorTransferFunction define the color space that the rendered frames will be tagged with. For custom video compositing these properties are also used to specify the required color space of the source frames.
 
-    Examples of common color spaces:
-	
-        TODO: SD
-        TODO: HD
-        TODO: HD-P3
+    For examples of common color spaces see AVVideoSettings.h.
 
     How to preserve the color space of the source frames:
  
         Decide which color space to be preserved by examining the source asset's video tracks. Copy the source track's primaries, matrix and transfer function into the video composition's colorPrimaries, colorYCbCrMatrix and colorTransferFunction respectively.
-		
-        TODO: <rdar://problem/25496972> sample code showing how to inspect the source asset track's primaries etc and setup a video composition to preserve them. Ideally we'll show the narrow-HD case and the wide-P3 case.
 
         - When using custom video compositing
 			Setting these properties will cause source frames to be converted into the specified color space and tagged as such. New frames allocated using -[AVVideoCompositionRenderContext newPixelBuffer] will also be tagged correctly.

```