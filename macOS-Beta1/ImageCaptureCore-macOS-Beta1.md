#ImageCaptureCore.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICCameraDevice.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICCameraDevice.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICCameraDevice.h	2015-08-23 03:41:02.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICCameraDevice.h	2016-05-11 18:08:51.000000000 +0200
@@ -73,13 +73,6 @@
 */
 extern NSString *const ICCameraDeviceCanAcceptPTPCommands;
 
-/*!
- @const      ICCameraDeviceSupportsFastPTP
- @abstract   ICCameraDeviceSupportsFastPTP
- @discussion Indicates that the camera supports fast PTP commands.
- */
-extern NSString *const ICCameraDeviceSupportsFastPTP;
-
 //------------------------------------------------------------------------------------------------------------------------------
 // Allowed keys in the options dictionary used when downloading a file from the camera
 
@@ -345,7 +338,7 @@
   @abstract This method returns an array of files on the camera of type fileType. 
   @discussion The fileType string is one of the following Uniform Type Identifier strings: kUTTypeImage, kUTTypeMovie, kUTTypeAudio, or kUTTypeData.
 */
-- ( NSArray<NSString*>*)filesOfType:( NSString*)fileUTType;
+- (nullable NSArray<NSString*>*)filesOfType:( NSString*)fileUTType;
 
 /*! 
   @method requestSyncClock
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICCameraItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICCameraItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICCameraItem.h	2015-08-23 03:41:03.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICCameraItem.h	2016-05-11 18:08:51.000000000 +0200
@@ -71,7 +71,7 @@
     @abstract ￼The file system path of the item for items on a device with transportType of ICTransportTypeMassStorage.
 
 */
-@property(readonly)                                             NSString*       fileSystemPath;
+@property(nullable,readonly)                                             NSString*       fileSystemPath;
 
 /*!
     @property locked
@@ -99,14 +99,14 @@
     @abstract ￼Creation date of this file. This information is usually the same as the EXIF creation date.
 
 */
-@property(readonly)                                             NSDate*         creationDate;
+@property(nullable,readonly)                                             NSDate*         creationDate;
 
 /*!
     @property modificationDate
     @abstract ￼Modification date of this file. This information is usually the same as the EXIF modification date.
 
 */
-@property(readonly)                                             NSDate*         modificationDate;
+@property(nullable,readonly)                                             NSDate*         modificationDate;
 
 /*!
     @property thumbnailIfAvailable
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICDeviceBrowser.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICDeviceBrowser.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICDeviceBrowser.h	2015-08-23 03:41:02.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICDeviceBrowser.h	2016-05-11 18:08:51.000000000 +0200
@@ -122,7 +122,7 @@
     @abstract This method returns a device object that should be selected by the client application when it is launched.
     @discussion If the client application that calls this method is the auto-launch application associated with a device and that device is the last device attached (through USB, FireWire or network), then that device will be the preferred device. The best place to call this method is in the implmentation of the ICDeviceBrowser delegate method "deviceBrowser:didAddDevice:moreComing:", if the "moreComing" parameter passed to the delegate is "NO"; or in the delegate method "deviceBrowserDidEnumerateLocalDevices:".
 */
-- ( ICDevice*)preferredDevice;
+- ( nullable ICDevice*)preferredDevice;
 
 /*! 
   @method init

```