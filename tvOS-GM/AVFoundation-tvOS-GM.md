#AVFoundation.framework

``` diff
diff -ruN /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureDevice.h /Applications/Xcode8-GM.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureDevice.h
--- /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureDevice.h	2016-08-05 00:58:46.000000000 -0500
+++ /Applications/Xcode8-GM.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureDevice.h	2016-08-05 00:30:12.000000000 -0500
@@ -59,7 +59,7 @@
     An AVCaptureDevice represents a physical device that provides realtime input media data, such as video and audio.
 
  @discussion
-    Each instance of AVCaptureDevice corresponds to a device, such as a camera or microphone. Instances of AVCaptureDevice cannot be created directly. An array of all currently available devices can also be obtained using the devices class method. Devices can provide one or more streams of a given media type. Applications can search for devices that provide media of a specific type using the devicesWithMediaType: and defaultDeviceWithMediaType: class methods.
+    Each instance of AVCaptureDevice corresponds to a device, such as a camera or microphone. Instances of AVCaptureDevice cannot be created directly. An array of all currently available devices can also be obtained using the AVCaptureDeviceDiscoverySession. Devices can provide one or more streams of a given media type. Applications can search for devices matching desired criteria by using AVCaptureDeviceDiscoverySession, or may obtain a reference to the default device matching desired criteria by using +[AVCaptureDevice defaultDeviceWithDeviceType:mediaType:position:].
 
     Instances of AVCaptureDevice can be used to provide media data to an AVCaptureSession by creating an AVCaptureDeviceInput with the device and adding that to the capture session.
  */
@@ -81,7 +81,7 @@
  @discussion
     This method returns an array of AVCaptureDevice instances for input devices currently connected and available for capture. The returned array contains all devices that are available at the time the method is called. Applications should observe AVCaptureDeviceWasConnectedNotification and AVCaptureDeviceWasDisconnectedNotification to be notified when the list of available devices has changed.
  */
-+ (NSArray *)devices;
++ (NSArray *)devices NS_DEPRECATED_IOS(4_0, 10_0, "Use AVCaptureDeviceDiscoverySession instead.");
 
 /*!
  @method devicesWithMediaType:
@@ -96,7 +96,7 @@
  @discussion
     This method returns an array of AVCaptureDevice instances for input devices currently connected and available for capture that provide media of the given type. Media type constants are defined in AVMediaFormat.h. The returned array contains all devices that are available at the time the method is called. Applications should observe AVCaptureDeviceWasConnectedNotification and AVCaptureDeviceWasDisconnectedNotification to be notified when the list of available devices has changed.
  */
-+ (NSArray *)devicesWithMediaType:(NSString *)mediaType;
++ (NSArray *)devicesWithMediaType:(NSString *)mediaType NS_DEPRECATED_IOS(4_0, 10_0, "Use AVCaptureDeviceDiscoverySession instead.");
 
 /*!
  @method defaultDeviceWithMediaType:
@@ -411,6 +411,83 @@
 
 
 /*!
+ @group AVCaptureDeviceType string constants
+ 
+ @discussion
+    The AVCaptureDeviceType string constants are intended to be used in combination with the AVCaptureDeviceDiscoverySession class to obtain a list of devices matching certain search criteria.
+ */
+typedef NSString *AVCaptureDeviceType NS_STRING_ENUM NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED;
+
+/*!
+ @constant AVCaptureDeviceTypeBuiltInMicrophone
+    A built-in microphone.
+ */
+AVF_EXPORT AVCaptureDeviceType const AVCaptureDeviceTypeBuiltInMicrophone NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED;
+
+/*!
+ @constant AVCaptureDeviceTypeBuiltInWideAngleCamera
+    A built-in wide angle camera device. These devices are suitable for general purpose use.
+ */
+AVF_EXPORT AVCaptureDeviceType const AVCaptureDeviceTypeBuiltInWideAngleCamera NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED;
+
+/*!
+ @constant AVCaptureDeviceTypeBuiltInTelephotoCamera
+    A built-in camera device with a longer focal length than a wide angle camera. Note that devices of this type may only be discovered using an AVCaptureDeviceDiscoverySession.
+ */
+AVF_EXPORT AVCaptureDeviceType const AVCaptureDeviceTypeBuiltInTelephotoCamera NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED;
+
+/*!
+ @constant AVCaptureDeviceTypeBuiltInDuoCamera
+    A device that consists of two fixed focal length cameras, one wide and one telephoto. Note that devices of this type may only be discovered using an AVCaptureDeviceDiscoverySession.
+
+    A device of this device type supports the following new features:
+    - Auto switching from one camera to the other when zoom factor, light level, and focus position allow this.
+	- Higher quality zoom for still captures by fusing images from both cameras.
+
+    A device of this device type does not support the following features:
+	- AVCaptureExposureModeCustom and manual exposure bracketing.
+    - Locking focus with a lens position other than AVCaptureLensPositionCurrent.
+	- Locking auto white balance with device white balance gains other than AVCaptureWhiteBalanceGainsCurrent.
+
+    Even when locked, exposure duration, ISO, aperture, white balance gains, or lens position may change when the device switches from one camera to the other. The overall exposure, white balance, and focus position however should be consistent.
+ */
+AVF_EXPORT AVCaptureDeviceType const AVCaptureDeviceTypeBuiltInDuoCamera NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED;
+
+@interface AVCaptureDevice (AVCaptureDeviceType)
+
+/*!
+ @property deviceType
+ @abstract
+    The type of the capture device.
+
+ @discussion
+    A capture device's type never changes.
+ */
+@property(nonatomic, readonly) AVCaptureDeviceType deviceType NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED;
+
+/*!
+ @method defaultDeviceWithDeviceType:
+ @abstract
+    Returns an AVCaptureDevice instance for the default device of the given device type, media type, and position.
+
+ @param deviceType
+    The device type supported by the returned device. It must be a valid AVCaptureDeviceType.
+ @param mediaType
+    The media type, such as AVMediaTypeVideo, AVMediaTypeAudio, or AVMediaTypeMuxed, supported by the returned device. Pass nil to consider devices with any media type.
+ @param position
+    The position supported by the returned device. Pass AVCaptureDevicePositionUnspecified to consider devices with any position.
+ @result
+    The default device with the given device type, media type and position or nil if no device with that media type exists and nil otherwise.
+
+ @discussion
+    This method returns the default device of the given combination of device type, media type, and position currently available on the system.
+ */
++ (AVCaptureDevice *)defaultDeviceWithDeviceType:(AVCaptureDeviceType)deviceType mediaType:(NSString *)mediaType position:(AVCaptureDevicePosition)position NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED;
+
+@end
+
+
+/*!
  @enum AVCaptureFlashMode
  @abstract
     Constants indicating the mode of the flash on the receiver's device, if it has one.
@@ -648,6 +725,16 @@
 - (BOOL)isFocusModeSupported:(AVCaptureFocusMode)focusMode;
 
 /*!
+ @property lockingFocusWithCustomLensPositionSupported
+ @abstract
+    Indicates whether the receiver supports a lens position other than AVCaptureLensPositionCurrent.
+
+ @discussion
+    If lockingFocusWithCustomLensPositionSupported returns NO, setFocusModeLockedWithLensPosition: may only be called with AVCaptureLensPositionCurrent. Passing any other lens position will result in an exception.
+ */
+@property(nonatomic, readonly, getter=isLockingFocusWithCustomLensPositionSupported) BOOL lockingFocusWithCustomLensPositionSupported NS_AVAILABLE_IOS(10_0);
+
+/*!
  @property focusMode
  @abstract
     Indicates current focus mode of the receiver, if it has one.
@@ -1031,6 +1118,16 @@
 - (BOOL)isWhiteBalanceModeSupported:(AVCaptureWhiteBalanceMode)whiteBalanceMode;
 
 /*!
+ @property lockingWhiteBalanceWithCustomDeviceGainsSupported
+ @abstract
+    Indicates whether the receiver supports white balance gains other than AVCaptureWhiteBalanceGainsCurrent.
+
+ @discussion
+    If lockingWhiteBalanceWithCustomDeviceGainsSupported returns NO, setWhiteBalanceModeLockedWithDeviceWhiteBalanceGains: may only be called with AVCaptureWhiteBalanceGainsCurrent. Passing any other white balance gains will result in an exception.
+ */
+@property(nonatomic, readonly, getter=isLockingWhiteBalanceWithCustomDeviceGainsSupported) BOOL lockingWhiteBalanceWithCustomDeviceGainsSupported NS_AVAILABLE_IOS(10_0);
+
+/*!
  @property whiteBalanceMode
  @abstract
     Indicates current white balance mode of the receiver, if it has adjustable white balance.
@@ -1470,6 +1567,51 @@
 @end
 
 
+/*!
+ @class AVCaptureDeviceDiscoverySession
+ @abstract
+    The AVCaptureDeviceDiscoverySession allows clients to search for devices by certain criteria.
+
+ @discussion
+    This class allows clients to discover devices by providing certain search criteria. The objective of this class is to help find devices by device type and optionally by media type or position and allow you to key-value observe changes to the returned devices list.
+ */
+NS_CLASS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED
+@interface AVCaptureDeviceDiscoverySession : NSObject
+
+/*!
+ @method discoverySessionWithDeviceTypes:
+ @abstract
+    Returns an AVCaptureDeviceDiscoverySession instance for the given device types, media type, and position.
+
+ @param deviceTypes
+    An array specifying the device types to include in the list of discovered devices.
+ @param mediaType
+    The media type, such as AVMediaTypeVideo, AVMediaTypeAudio, or AVMediaTypeMuxed, to include in the list of discovered devices. Pass nil to search for devices with any media type.
+ @param position
+    The position to include in the list of discovered devices. Pass AVCaptureDevicePositionUnspecified to search for devices with any position.
+ @result
+    The AVCaptureDeviceDiscoverySession from which the list of devices can be obtained.
+
+ @discussion
+    The list of device types is mandatory. This is used to make sure that clients only get access to devices of types they expect. This prevents new device types from automatically being included in the list of devices.
+ */
++ (instancetype)discoverySessionWithDeviceTypes:(NSArray<AVCaptureDeviceType> *)deviceTypes mediaType:(NSString *)mediaType position:(AVCaptureDevicePosition)position;
+
+- (instancetype)init NS_UNAVAILABLE;
+
+/*!
+ @property devices
+ @abstract
+    The list of devices that comply to the search criteria specified on the discovery session.
+
+ @discussion
+    The returned array contains only devices that are available at the time the method is called. Applications can key-value observe this property to be notified when the list of available devices has changed.
+ */
+@property(nonatomic, readonly) NSArray<AVCaptureDevice *> *devices;
+
+@end
+
+
 @class AVFrameRateRangeInternal;
 
 /*!

```