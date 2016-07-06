#CoreGraphics.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGBase.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGBase.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGBase.h	2016-06-03 04:52:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGBase.h	2016-06-28 05:17:41.000000000 +0200
@@ -279,7 +279,7 @@
 
 #if !TARGET_IPHONE_SIMULATOR
 
-typedef struct  CF_BRIDGED_TYPE(id) __IOSurface *IOSurfaceRef;
+typedef struct  CF_BRIDGED_TYPE(id) __IOSurface *IOSurfaceRef __attribute__((swift_name("IOSurfaceRef")));
 
 #endif
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConversionInfo.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConversionInfo.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConversionInfo.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConversionInfo.h	2016-06-28 05:17:41.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConverter.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConverter.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConverter.h	2016-06-03 04:52:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConverter.h	2016-06-28 05:17:41.000000000 +0200
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
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGDirectDisplayMetal.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGDirectDisplayMetal.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGDirectDisplayMetal.h	2016-06-03 04:52:13.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGDirectDisplayMetal.h	2016-06-28 05:17:41.000000000 +0200
@@ -15,7 +15,7 @@
 /* Return the Metal device for the GPU currently being used to drive a given display */
 /* Note: On systems with automatic graphics switching enabled, this value can change at
    almost any time. */
-CG_EXTERN id<MTLDevice> __nullable CGDirectDisplayCopyCurrentMetalDevice(CGDirectDisplayID display) CG_AVAILABLE_STARTING(__MAC_10_11, __IPHONE_NA);
+CG_EXTERN id<MTLDevice> __nullable CGDirectDisplayCopyCurrentMetalDevice(CGDirectDisplayID display) CF_RETURNS_RETAINED CG_AVAILABLE_STARTING(__MAC_10_11, __IPHONE_NA);
 
 #endif /* __OBJC__ */
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGDisplayStream.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGDisplayStream.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGDisplayStream.h	2016-06-03 04:52:13.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGDisplayStream.h	2016-06-28 05:17:41.000000000 +0200
@@ -11,7 +11,6 @@
 #include <dispatch/dispatch.h>
 
 #include <CoreGraphics/CGDirectDisplay.h>
-#include <IOSurface/IOSurfaceAPI.h>
 
 CF_IMPLICIT_BRIDGING_ENABLED
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGImage.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGImage.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGImage.h	2016-06-03 04:58:47.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGImage.h	2016-06-28 08:12:29.000000000 +0200
@@ -20,29 +20,37 @@
 CF_ASSUME_NONNULL_BEGIN
 
 typedef CF_ENUM(uint32_t, CGImageAlphaInfo) {
-  kCGImageAlphaNone,               /* For example, RGB. */
-  kCGImageAlphaPremultipliedLast,  /* For example, premultiplied RGBA */
-  kCGImageAlphaPremultipliedFirst, /* For example, premultiplied ARGB */
-  kCGImageAlphaLast,               /* For example, non-premultiplied RGBA */
-  kCGImageAlphaFirst,              /* For example, non-premultiplied ARGB */
-  kCGImageAlphaNoneSkipLast,       /* For example, RBGX. */
-  kCGImageAlphaNoneSkipFirst,      /* For example, XRGB. */
-  kCGImageAlphaOnly                /* No color data, alpha data only */
+    kCGImageAlphaNone,               /* For example, RGB. */
+    kCGImageAlphaPremultipliedLast,  /* For example, premultiplied RGBA */
+    kCGImageAlphaPremultipliedFirst, /* For example, premultiplied ARGB */
+    kCGImageAlphaLast,               /* For example, non-premultiplied RGBA */
+    kCGImageAlphaFirst,              /* For example, non-premultiplied ARGB */
+    kCGImageAlphaNoneSkipLast,       /* For example, RBGX. */
+    kCGImageAlphaNoneSkipFirst,      /* For example, XRGB. */
+    kCGImageAlphaOnly                /* No color data, alpha data only */
 };
 
+typedef CF_ENUM(uint32_t, CGImageByteOrderInfo) {
+    kCGImageByteOrderMask     = 0x7000,
+    kCGImageByteOrder16Little = (1 << 12),
+    kCGImageByteOrder32Little = (2 << 12),
+    kCGImageByteOrder16Big    = (3 << 12),
+    kCGImageByteOrder32Big    = (4 << 12)
+} CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+
 typedef CF_OPTIONS(uint32_t, CGBitmapInfo) {
-  kCGBitmapAlphaInfoMask = 0x1F,
-  
-  kCGBitmapFloatInfoMask = 0xF00,
-  kCGBitmapFloatComponents = (1 << 8),
-  
-  kCGBitmapByteOrderMask = 0x7000,
-  kCGBitmapByteOrderDefault = (0 << 12),
-  kCGBitmapByteOrder16Little = (1 << 12),
-  kCGBitmapByteOrder32Little = (2 << 12),
-  kCGBitmapByteOrder16Big = (3 << 12),
-  kCGBitmapByteOrder32Big = (4 << 12)
-} CF_ENUM_AVAILABLE(10_4, 2_0);
+    kCGBitmapAlphaInfoMask = 0x1F,
+
+    kCGBitmapFloatInfoMask = 0xF00,
+    kCGBitmapFloatComponents = (1 << 8),
+
+    kCGBitmapByteOrderMask     = kCGImageByteOrderMask,
+    kCGBitmapByteOrderDefault  = (0 << 12),
+    kCGBitmapByteOrder16Little = kCGImageByteOrder16Little,
+    kCGBitmapByteOrder32Little = kCGImageByteOrder32Little,
+    kCGBitmapByteOrder16Big    = kCGImageByteOrder16Big,
+    kCGBitmapByteOrder32Big    = kCGImageByteOrder32Big
+} CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 #ifdef __BIG_ENDIAN__
 # define kCGBitmapByteOrder16Host kCGBitmapByteOrder16Big
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CoreGraphics.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CoreGraphics.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CoreGraphics.h	2016-06-03 04:52:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CoreGraphics.h	2016-06-28 05:17:41.000000000 +0200
@@ -11,6 +11,7 @@
 #include <CoreGraphics/CGBitmapContext.h>
 #include <CoreGraphics/CGColor.h>
 #include <CoreGraphics/CGColorConverter.h>
+#include <CoreGraphics/CGColorConversionInfo.h>
 #include <CoreGraphics/CGColorSpace.h>
 #include <CoreGraphics/CGContext.h>
 #include <CoreGraphics/CGDataConsumer.h>

```