#CoreGraphics.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConverter.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConverter.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConverter.h	2016-07-10 07:49:33.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConverter.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,52 +0,0 @@
-/* CoreGraphics - CGColorConverter.h
-   Copyright (c) 2015 Apple Inc.
-   All rights reserved. */
-
-#ifndef CGCOLORCONVERTER_H_
-#define CGCOLORCONVERTER_H_
-
-#include <CoreGraphics/CGBase.h>
-#include <CoreFoundation/CFAvailability.h>
-#include <CoreGraphics/CGColorConversionInfo.h>
-
-// #warning CGColorConverter is deprecated, please use CGColorConversionInfo
-
-typedef CGColorConversionInfoRef CGColorConverterRef;
-
-CF_IMPLICIT_BRIDGING_ENABLED
-
-CF_ASSUME_NONNULL_BEGIN
-
-CG_EXTERN CFTypeID CGColorConverterGetTypeID(void);
-
-typedef CF_ENUM (uint32_t, CGColorConverterTransformType) {
-  kCGColorConverterTransformFromSpace  = kCGColorConversionTransformFromSpace,
-  kCGColorConverterTransformToSpace    = kCGColorConversionTransformToSpace,
-  kCGColorConverterTransformApplySpace = kCGColorConversionTransformApplySpace
-};
-
-
-/* Create CGColorConverterRef from a list of CG color spaces, transform types and rendering intents.
- * ColorSpaces are iterated from first to last. The list of triples:
- * {CGColorSpaceRef, CGColorConverterTransformType, CGColorRenderingIntent} needs to be terminated with NULL
- * Requirements: CG color spaces must be calibrated (no Device{Gray,RGB,CMYK}, Indexed or DeviceN are allowed).
- */
-
-CG_EXTERN CGColorConverterRef __nullable CGColorConverterCreate
-  (CFDictionaryRef __nullable options, cg_nullable CGColorSpaceRef, CGColorConverterTransformType, CGColorRenderingIntent, ...)
-  CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
-
-CG_EXTERN CGColorConverterRef __nullable CGColorConverterCreateSimple(cg_nullable CGColorSpaceRef from, cg_nullable CGColorSpaceRef to)
-    CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
-
-CG_EXTERN CGColorConverterRef __nullable CGColorConverterRetain(CGColorConverterRef cg_nullable)
-    CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
-
-CG_EXTERN void CGColorConverterRelease(CGColorConverterRef cg_nullable)
-CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
-
-CF_ASSUME_NONNULL_END
-
-CF_IMPLICIT_BRIDGING_DISABLED
-
-#endif /* CGCOLORCONVERTER_H_ */
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorSpace.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorSpace.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorSpace.h	2016-07-10 07:49:32.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorSpace.h	2016-07-25 08:00:46.000000000 +0200
@@ -325,7 +325,7 @@
 CG_EXTERN CFDataRef __nullable CGColorSpaceCopyICCData(CGColorSpaceRef cg_nullable space)
 CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
 
-/* Return true if gamut of the RGB color space is greater than 75% of NTSC gamut */
+/* Return true if gamut of the RGB color space is greater than 85% of NTSC gamut */
 
 CG_EXTERN bool CGColorSpaceIsWideGamutRGB(CGColorSpaceRef)
 CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGGradient.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGGradient.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGGradient.h	2016-07-13 05:52:11.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGGradient.h	2016-07-25 07:13:20.000000000 +0200
@@ -75,8 +75,8 @@
    values. */
 
 CG_EXTERN CGGradientRef __nullable CGGradientCreateWithColors(
-    CGColorSpaceRef cg_nullable space, CFArrayRef cg_nullable colors,
-    const CGFloat * cg_nullable locations)
+    CGColorSpaceRef __nullable space, CFArrayRef cg_nullable colors,
+    const CGFloat * __nullable locations)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Equivalent to `CFRetain' except that it doesn't crash (as `CFRetain'
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CoreGraphics.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CoreGraphics.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CoreGraphics.h	2016-07-10 07:49:34.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CoreGraphics.h	2016-07-25 07:17:19.000000000 +0200
@@ -10,7 +10,6 @@
 #include <CoreGraphics/CGAffineTransform.h>
 #include <CoreGraphics/CGBitmapContext.h>
 #include <CoreGraphics/CGColor.h>
-#include <CoreGraphics/CGColorConverter.h>
 #include <CoreGraphics/CGColorConversionInfo.h>
 #include <CoreGraphics/CGColorSpace.h>
 #include <CoreGraphics/CGContext.h>

```