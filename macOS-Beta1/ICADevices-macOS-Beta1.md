#ICADevices.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ICADevices.framework/Headers/ICACamera.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ICADevices.framework/Headers/ICACamera.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ICADevices.framework/Headers/ICACamera.h	2015-08-23 04:14:41.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ICADevices.framework/Headers/ICACamera.h	2016-05-13 09:09:48.000000000 +0200
@@ -285,7 +285,7 @@
     kICACapabilityCanCameraSyncClock            = 'sclk',
     kICACapabilityCanCameraUploadData           = 'load',
     kICACapabilityMayStoreNewImagesInTempStore  = 'temp',
-    kICACapabilityMessageCameraSupportsFastPTP  = 'fptp'
+    kICACapabilityMessageCameraSupportsApplePTP = 'aptp'
 };
 
 //------------------------------------------------------------------------------------------------------------------------------
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ICADevices.framework/Headers/ICADevices.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ICADevices.framework/Headers/ICADevices.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ICADevices.framework/Headers/ICADevices.h	2015-08-23 04:14:41.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ICADevices.framework/Headers/ICADevices.h	2016-05-13 09:09:48.000000000 +0200
@@ -66,11 +66,12 @@
 extern const int   ICLoggingLevelBasicInfo;
 extern const int   ICLoggingLevelVerboseInfo;
 extern const int   ICLoggingLevelTimingInfo;
-
+    
 void    __ICLog( const char* format, ... ); // This function MUST be called only if ICLoggingEnabled is true.
-
+    
 #define __ICLOG(logLevel, params)   { if (ICLoggingEnabled && (logLevel & ICLoggingLevelMask)) __ICLog params; }
 
+
 //------------------------------------------------------------------------------------------------------------------------------
 
 #ifdef __cplusplus

```