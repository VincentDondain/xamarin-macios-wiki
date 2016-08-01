#VideoToolbox.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTCompressionProperties.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTCompressionProperties.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTCompressionProperties.h	2016-05-04 00:21:26.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTCompressionProperties.h	2016-07-28 05:05:15.000000000 +0200
@@ -234,6 +234,7 @@
 		Video encoders should use standard keys where available, and follow standard patterns where not.
 */
 VT_EXPORT const CFStringRef kVTCompressionPropertyKey_ProfileLevel __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_8_0); // Read/write, CFString (enumeration), Optional
+	
 
 VT_EXPORT const CFStringRef kVTProfileLevel_H264_Baseline_1_3 __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_8_0);
 VT_EXPORT const CFStringRef kVTProfileLevel_H264_Baseline_3_0 __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_8_0);
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTUtilities.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTUtilities.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTUtilities.h	2016-07-12 06:15:23.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTUtilities.h	2016-07-28 05:05:16.000000000 +0200
@@ -3,7 +3,7 @@
  
 	Framework:  VideoToolbox
  
-	Copyright � 2013-2014 Apple Inc. All rights reserved.
+	Copyright © 2013-2014 Apple Inc. All rights reserved.
  
 */
 

```