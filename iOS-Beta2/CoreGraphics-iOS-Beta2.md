#CoreGraphics.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConversionInfo.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConversionInfo.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConversionInfo.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConversionInfo.h	2016-06-28 08:17:39.000000000 +0200
@@ -0,0 +1,51 @@
+/* CoreGraphics - CGColorConversionInfo.h
+   Copyright (c) 2016 Apple Inc.
+   All rights reserved. */
+
+#ifndef CGCOLORCONVERSIONINFO_H_
+#define CGCOLORCONVERSIONINFO_H_
+
+#include <CoreGraphics/CGBase.h>
+#include <CoreFoundation/CFAvailability.h>
+#include <CoreGraphics/CGColorSpace.h>
+
+typedef const struct CF_BRIDGED_TYPE(id) CGColorConversionInfo* CGColorConversionInfoRef;
+
+CF_IMPLICIT_BRIDGING_ENABLED
+
+CF_ASSUME_NONNULL_BEGIN
+
+CG_EXTERN CFTypeID CGColorConversionInfoGetTypeID(void);
+
+typedef CF_ENUM (uint32_t, CGColorConversionInfoTransformType) {
+  kCGColorConversionTransformFromSpace = 0,
+  kCGColorConversionTransformToSpace,
+  kCGColorConversionTransformApplySpace
+};
+
+/* Create CGColorConversionInfoRef for converting color from `src' color space to `dst' color space
+ * using kCGRenderingIntentDefault rendering intent.
+ * Requirements: CG color spaces must be calibrated (no Device{Gray,RGB,CMYK}, Indexed or DeviceN are allowed).
+ */
+
+CG_EXTERN CGColorConversionInfoRef __nullable CGColorConversionInfoCreate(cg_nullable CGColorSpaceRef src, cg_nullable CGColorSpaceRef dst)
+    CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+
+/* Create CGColorConversionInfoRef from a list of CG color spaces, transform types and rendering intents.
+ * ColorSpaces are iterated from first to last. The list of triples:
+ * {CGColorSpaceRef, CGColorConversionInfoTransformType, CGColorRenderingIntent} must be terminated with NULL
+ * Requirements: CG color spaces must be calibrated (no Device{Gray,RGB,CMYK}, Indexed or DeviceN are allowed).
+ */
+
+CG_EXTERN CGColorConversionInfoRef __nullable CGColorConversionInfoCreateFromList
+  (CFDictionaryRef __nullable options, cg_nullable CGColorSpaceRef, CGColorConversionInfoTransformType, CGColorRenderingIntent, ...)
+  CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+
+/* CFBooleanRef which can be used as option to create CGColorConversionInfoRef, when Black Point Compensation is desired */
+CG_EXTERN const CFStringRef kCGColorConversionBlackPointCompensation CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+
+CF_ASSUME_NONNULL_END
+
+CF_IMPLICIT_BRIDGING_DISABLED
+
+#endif /* CGCOLORCONVERSIONINFO_H_ */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConverter.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConverter.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConverter.h	2016-06-03 04:58:47.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConverter.h	2016-06-28 08:17:39.000000000 +0200
@@ -7,9 +7,11 @@
 
 #include <CoreGraphics/CGBase.h>
 #include <CoreFoundation/CFAvailability.h>
-#include <CoreGraphics/CGColorSpace.h>
+#include <CoreGraphics/CGColorConversionInfo.h>
 
-typedef const struct CGColorConverter* CGColorConverterRef;
+// #warning CGColorConverter is deprecated, please use CGColorConversionInfo
+
+typedef CGColorConversionInfoRef CGColorConverterRef;
 
 CF_IMPLICIT_BRIDGING_ENABLED
 
@@ -18,23 +20,30 @@
 CG_EXTERN CFTypeID CGColorConverterGetTypeID(void);
 
 typedef CF_ENUM (uint32_t, CGColorConverterTransformType) {
-  kCGColorConverterTransformFromSpace = 0,
-  kCGColorConverterTransformToSpace,
-  kCGColorConverterTransformApplySpace
+  kCGColorConverterTransformFromSpace  = kCGColorConversionTransformFromSpace,
+  kCGColorConverterTransformToSpace    = kCGColorConversionTransformToSpace,
+  kCGColorConverterTransformApplySpace = kCGColorConversionTransformApplySpace
 };
 
 
 /* Create CGColorConverterRef from a list of CG color spaces, transform types and rendering intents.
  * ColorSpaces are iterated from first to last. The list of triples:
  * {CGColorSpaceRef, CGColorConverterTransformType, CGColorRenderingIntent} needs to be terminated with NULL
- * Requirements: CG color spaces must be calibrated (no Device{Gray,RGB,CMYK}, Indexed or DeviceN).
+ * Requirements: CG color spaces must be calibrated (no Device{Gray,RGB,CMYK}, Indexed or DeviceN are allowed).
  */
+
 CG_EXTERN CGColorConverterRef __nullable CGColorConverterCreate
-  (CFDictionaryRef __nullable options, cg_nullable CGColorSpaceRef, CGColorConverterTransformType, CGColorRenderingIntent, ...);
+  (CFDictionaryRef __nullable options, cg_nullable CGColorSpaceRef, CGColorConverterTransformType, CGColorRenderingIntent, ...)
+  CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+
+CG_EXTERN CGColorConverterRef __nullable CGColorConverterCreateSimple(cg_nullable CGColorSpaceRef from, cg_nullable CGColorSpaceRef to)
+    CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
 
-CG_EXTERN CGColorConverterRef __nullable CGColorConverterCreateSimple(cg_nullable CGColorSpaceRef from, cg_nullable CGColorSpaceRef to);
+CG_EXTERN CGColorConverterRef __nullable CGColorConverterRetain(CGColorConverterRef cg_nullable)
+    CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
 
-CG_EXTERN void CGColorConverterRelease(CGColorConverterRef cg_nullable);
+CG_EXTERN void CGColorConverterRelease(CGColorConverterRef cg_nullable)
+CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
 
 CF_ASSUME_NONNULL_END
 
```