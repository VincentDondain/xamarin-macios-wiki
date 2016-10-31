#ImageCaptureCore.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICCameraDevice.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICCameraDevice.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICCameraDevice.h	2016-09-20 01:01:22.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICCameraDevice.h	2016-10-22 20:46:19.000000000 +0200
@@ -331,7 +331,7 @@
     @discussion Use 'requestEnableTethering' and 'requestDisableTethering' to enable or disable tethered capture on the device.
 
 */
-@property             BOOL            tetheredCaptureEnabled;
+@property(readonly)             BOOL            tetheredCaptureEnabled;
 
 /*! 
   @method filesOfType:

```