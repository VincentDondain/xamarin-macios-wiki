#VideoToolbox.framework

``` diff
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTCompressionProperties.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTCompressionProperties.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTCompressionProperties.h	2016-07-28 05:05:15.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTCompressionProperties.h	2016-08-06 08:20:31.000000000 +0200
@@ -234,7 +234,6 @@
 		Video encoders should use standard keys where available, and follow standard patterns where not.
 */
 VT_EXPORT const CFStringRef kVTCompressionPropertyKey_ProfileLevel __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_8_0); // Read/write, CFString (enumeration), Optional
-	
 
 VT_EXPORT const CFStringRef kVTProfileLevel_H264_Baseline_1_3 __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_8_0);
 VT_EXPORT const CFStringRef kVTProfileLevel_H264_Baseline_3_0 __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_8_0);
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTErrors.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTErrors.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTErrors.h	2016-07-27 05:07:20.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTErrors.h	2016-08-06 03:00:13.000000000 +0200
@@ -55,6 +55,7 @@
 	kVTFrameSiloInvalidTimeRangeErr			= -12216,
 	kVTCouldNotFindTemporalFilterErr		= -12217,
 	kVTPixelTransferNotPermittedErr			= -12218,
+	kVTColorCorrectionImageRotationFailedErr	= -12219,
 };
 
 /*!

```