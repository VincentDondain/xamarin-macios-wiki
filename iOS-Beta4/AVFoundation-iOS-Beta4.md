#AVFoundation.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCapturePhotoOutput.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCapturePhotoOutput.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCapturePhotoOutput.h	2016-07-10 08:19:50.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCapturePhotoOutput.h	2016-07-25 07:29:09.000000000 +0200
@@ -87,6 +87,38 @@
 - (void)capturePhotoWithSettings:(AVCapturePhotoSettings *)settings delegate:(id<AVCapturePhotoCaptureDelegate>)delegate;
 
 /*!
+ @property preparedPhotoSettingsArray
+ @abstract
+    An array of AVCapturePhotoSettings instances for which the receiver is prepared to capture.
+
+ @discussion
+    @seealso setPreparedPhotoSettingsArray:completionHandler:
+    Some types of photo capture, such as bracketed captures and RAW captures, require the receiver to allocate additional buffers or prepare other resources. To prevent photo capture requests from executing slowly due to lazy resource allocation, you may call -setPreparedPhotoSettingsArray:completionHandler: with an array of settings objects representative of the types of capture you will be performing (e.g., settings for a bracketed capture, RAW capture, and/or still image stabilization capture). By default, the receiver prepares sufficient resources to capture photos with default settings, +[AVCapturePhotoSettings photoSettings].
+ */
+@property(nonatomic, readonly) NSArray<AVCapturePhotoSettings *> *preparedPhotoSettingsArray;
+
+/*!
+ @method setPreparedPhotoSettingsArray:completionHandler:
+ @abstract
+    Method allowing the receiver to prepare resources in advance for future -capturePhotoWithSettings:delegate: requests.
+ 
+ @param preparedPhotoSettingsArray
+    An array of AVCapturePhotoSettings instances indicating the types of capture for which the receiver should prepare resources.
+ @param completionHandler
+    A completion block to be fired on a serial dispatch queue once the receiver has finished preparing. You may pass nil to indicate you do not wish to be called back when preparation is complete.
+ 
+ @discussion
+    Some types of photo capture, such as bracketed captures and RAW captures, require the receiver to allocate additional buffers or prepare other resources. To prevent photo capture requests from executing slowly due to lazy resource allocation, you may call this method with an array of settings objects representative of the types of capture you will be performing (e.g., settings for a bracketed capture, RAW capture, and/or still image stabilization capture). You may call this method even before calling -[AVCaptureSession startRunning] in order to hint the receiver up front which features you'll be utilizing. Each time you call this method with an array of settings, the receiver evaluates what additional resources it needs to allocate, as well as existing resources that can be reclaimed, and calls back your completionHandler when it has finished preparing (and possibly reclaiming) needed resources. By default, the receiver prepares sufficient resources to capture photos with default settings, +[AVCapturePhotoSettings photoSettings]. If you wish to reclaim all possible resources, you may call this method with an empty array.
+ 
+    Preparation for photo capture is always optional. You may call -capturePhotoWithSettings:delegate: without first calling -setPreparedPhotoSettingsArray:completionHandler:, but be advised that some of your photo captures may execute slowly as additional resources are allocated just-in-time.
+ 
+    If you call this method while your AVCaptureSession is not running, your completionHandler does not fire immediately. It only fires once you've called -[AVCaptureSession startRunning], and the needed resources have actually been prepared. If you call -setPreparedPhotoSettingsArray:completionHandler: with an array of settings, and then call it a second time, your first prepare call's completionHandler fires immediately with prepared == NO.
+ 
+    Prepared settings persist across session starts/stops and committed configuration changes. This property participates in -[AVCaptureSession beginConfiguration] / -[AVCaptureSession commitConfiguration] deferred work behavior. That is, if you call -[AVCaptureSession beginConfiguration], change your session's input/output topology, and call this method, preparation is deferred until you call -[AVCaptureSession commitConfiguration], enabling you to atomically commit a new configuration as well as prepare to take photos in that new configuration.
+ */
+- (void)setPreparedPhotoSettingsArray:(NSArray<AVCapturePhotoSettings *> *)preparedPhotoSettingsArray completionHandler:(nullable void (^)(BOOL prepared, NSError * _Nullable error))completionHandler;
+
+/*!
  @property availablePhotoPixelFormatTypes
  @abstract
     An array of kCVPixelBufferPixelFormatTypeKey values that are currently supported by the receiver.
@@ -172,7 +204,7 @@
     Indicates whether the photo render pipeline should be configured to deliver high resolution still images.
 
  @discussion
-    Some AVCaptureDeviceFormats support outputting higher resolution stills than their streaming resolution (See AVCaptureDeviceFormat.highResolutionStillImageDimensions). Under some conditions, AVCaptureSession needs to set up the photo render pipeline differently to support high resolution still image capture. If you intend to take high resolution still images at all, you should set this property to YES before calling AVCaptureSession -startRunning. Once you've opted in for high resolution capture, you are free to issue photo capture requests with or without highResolutionCaptureEnabled in the AVCapturePhotoSettings. If you have not set this property to YES and call capturePhotoWithSettings:delegate: with settings.highResolutionCaptureEnabled set to YES, an NSInvalidArgumentException will be thrown.
+    Some AVCaptureDeviceFormats support outputting higher resolution stills than their streaming resolution (See AVCaptureDeviceFormat.highResolutionStillImageDimensions). Under some conditions, AVCaptureSession needs to set up the photo render pipeline differently to support high resolution still image capture. If you intend to take high resolution still images at all, you should set this property to YES before calling -[AVCaptureSession startRunning]. Once you've opted in for high resolution capture, you are free to issue photo capture requests with or without highResolutionCaptureEnabled in the AVCapturePhotoSettings. If you have not set this property to YES and call capturePhotoWithSettings:delegate: with settings.highResolutionCaptureEnabled set to YES, an NSInvalidArgumentException will be thrown.
  */
 @property(nonatomic, getter=isHighResolutionCaptureEnabled) BOOL highResolutionCaptureEnabled;
 
@@ -212,7 +244,7 @@
     Indicates whether the receiver is configured for Live Photo capture
 
  @discussion
-    Default value is NO. This property may only be set to YES if livePhotoCaptureSupported is YES. Live Photo capture requires a lengthy reconfiguration of the capture render pipeline, so if you intend to do any Live Photo captures at all, you should set livePhotoCaptureEnabled to YES before calling AVCaptureSession -startRunning.
+    Default value is NO. This property may only be set to YES if livePhotoCaptureSupported is YES. Live Photo capture requires a lengthy reconfiguration of the capture render pipeline, so if you intend to do any Live Photo captures at all, you should set livePhotoCaptureEnabled to YES before calling -[AVCaptureSession startRunning].
  */
 @property(nonatomic, getter=isLivePhotoCaptureEnabled) BOOL livePhotoCaptureEnabled;
 
@@ -232,7 +264,7 @@
     Indicates whether Live Photo movies are trimmed in real time to avoid excessive movement.
 
  @discussion
-    This property defaults to YES when livePhotoCaptureSupported is YES. Changing this property's value while your session is running will cause a lengthy reconfiguration of the session. You should set livePhotoAutoTrimmingEnabled to YES or NO before calling AVCaptureSession -startRunning. When set to YES, Live Photo movies are analyzed in real time and trimmed if there's excessive movement before or after the photo is taken. Nominally, Live Photos are approximately 3 seconds long. With trimming enabled, they may be shorter, depending on movement. This feature prevents common problems such as Live Photo movies containing shoe or pocket shots.
+    This property defaults to YES when livePhotoCaptureSupported is YES. Changing this property's value while your session is running will cause a lengthy reconfiguration of the session. You should set livePhotoAutoTrimmingEnabled to YES or NO before calling -[AVCaptureSession startRunning]. When set to YES, Live Photo movies are analyzed in real time and trimmed if there's excessive movement before or after the photo is taken. Nominally, Live Photos are approximately 3 seconds long. With trimming enabled, they may be shorter, depending on movement. This feature prevents common problems such as Live Photo movies containing shoe or pocket shots.
  */
 @property(nonatomic, getter=isLivePhotoAutoTrimmingEnabled) BOOL livePhotoAutoTrimmingEnabled;
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoSettings.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoSettings.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoSettings.h	2016-07-10 10:02:26.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoSettings.h	2016-07-25 07:40:26.000000000 +0200
@@ -165,7 +165,9 @@
 	 */
 	AVF_EXPORT NSString *const AVVideoAllowFrameReorderingKey /* NSNumber (BOOL) */							 NS_AVAILABLE(10_10, 7_0);
 
-	AVF_EXPORT NSString *const AVVideoProfileLevelKey /* NSString, H.264 only, one of: */                    NS_AVAILABLE(10_8, 4_0);
+	AVF_EXPORT NSString *const AVVideoProfileLevelKey /* NSString, profile/level constants are specific to a particular encoder, one of: */               NS_AVAILABLE(10_8, 4_0);
+
+
 		AVF_EXPORT NSString *const AVVideoProfileLevelH264Baseline30 /* Baseline Profile Level 3.0 */        NS_AVAILABLE(10_8, 4_0);
 		AVF_EXPORT NSString *const AVVideoProfileLevelH264Baseline31 /* Baseline Profile Level 3.1 */        NS_AVAILABLE(10_8, 4_0);
         AVF_EXPORT NSString *const AVVideoProfileLevelH264Baseline41 /* Baseline Profile Level 4.1 */        NS_AVAILABLE(10_8, 5_0);

```