#CoreGraphics.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConverter.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConverter.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConverter.h	2016-07-10 09:19:46.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConverter.h	1970-01-01 01:00:00.000000000 +0100
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
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CoreGraphics.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CoreGraphics.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CoreGraphics.h	2016-07-10 09:19:46.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CoreGraphics.h	2016-07-25 07:06:13.000000000 +0200
@@ -10,7 +10,6 @@
 #include <CoreGraphics/CGAffineTransform.h>
 #include <CoreGraphics/CGBitmapContext.h>
 #include <CoreGraphics/CGColor.h>
-#include <CoreGraphics/CGColorConverter.h>
 #include <CoreGraphics/CGColorConversionInfo.h>
 #include <CoreGraphics/CGColorSpace.h>
 #include <CoreGraphics/CGContext.h>

```