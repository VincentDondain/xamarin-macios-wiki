#ImageCaptureCore.framework

``` diff
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICCommonConstants.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICCommonConstants.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICCommonConstants.h	2016-07-23 04:07:50.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageCaptureCore.framework/Headers/ICCommonConstants.h	2016-08-02 04:38:26.000000000 +0200
@@ -149,6 +149,7 @@
     ICReturnDeviceCouldNotPair                    = -9951,
     ICReturnDeviceCouldNotUnpair                  = -9952,
     ICReturnDeviceNeedsCredentials                = -9953,
+    ICReturnDeviceIsBusyEnumerating               = -9954,
 };
 
 ////------------------------------------------------------------------------------------------------------------------------------

```