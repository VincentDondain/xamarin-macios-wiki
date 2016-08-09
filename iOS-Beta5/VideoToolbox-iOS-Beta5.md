#VideoToolbox.framework

``` diff
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTErrors.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTErrors.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTErrors.h	2016-07-28 05:05:15.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTErrors.h	2016-08-06 08:20:31.000000000 +0200
@@ -55,6 +55,7 @@
 	kVTFrameSiloInvalidTimeRangeErr			= -12216,
 	kVTCouldNotFindTemporalFilterErr		= -12217,
 	kVTPixelTransferNotPermittedErr			= -12218,
+	kVTColorCorrectionImageRotationFailedErr	= -12219,
 };
 
 /*!

```