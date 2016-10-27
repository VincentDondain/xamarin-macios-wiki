#ImageCaptureCore.framework

``` diff
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICCommonConstants.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICCommonConstants.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICCommonConstants.h	2016-07-30 20:07:27.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICCommonConstants.h	2016-09-19 19:01:22.000000000 -0400
@@ -150,6 +150,7 @@
     ICReturnDeviceCouldNotUnpair                  = -9952,
     ICReturnDeviceNeedsCredentials                = -9953,
     ICReturnDeviceIsBusyEnumerating               = -9954,
+    ICReturnDeviceCommandGeneralFailure           = -9955
 };
 
 ////------------------------------------------------------------------------------------------------------------------------------

```