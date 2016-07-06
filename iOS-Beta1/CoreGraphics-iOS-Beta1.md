#CoreGraphics.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGBase.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGBase.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGBase.h	2016-02-20 00:02:13.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGBase.h	2016-05-26 06:16:33.000000000 +0200
@@ -9,6 +9,8 @@
 #include <stddef.h>
 #include <float.h>
 #include <TargetConditionals.h>
+#include <CoreFoundation/CFBase.h>
+#include <CoreFoundation/CFAvailability.h>
 
 /* Definition of `__CG_HAS_COMPILER_ATTRIBUTE'. */
 
@@ -255,4 +257,20 @@
 # define CG_PRIVATE_EXTERN CG_LOCAL
 #endif
 
+#if !TARGET_IPHONE_SIMULATOR
+
+typedef struct  CF_BRIDGED_TYPE(id) __IOSurface *IOSurfaceRef;
+
+#endif
+
+/* 'cg_nullable' will be dropped for new Swift clients. All others get currently the old behavior */
+
+#if defined(SWIFT_SDK_OVERLAY_COREGRAPHICS_EPOCH) && SWIFT_SDK_OVERLAY_COREGRAPHICS_EPOCH >= 0
+#   define cg_nullable
+#else
+#   define cg_nullable __nullable
+#endif
+
+
+
 #endif /* CGBASE_H_ */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGBitmapContext.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGBitmapContext.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGBitmapContext.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGBitmapContext.h	2016-06-02 06:59:41.000000000 +0200
@@ -40,7 +40,7 @@
 
 CG_EXTERN CGContextRef __nullable CGBitmapContextCreateWithData(
     void * __nullable data, size_t width, size_t height, size_t bitsPerComponent,
-    size_t bytesPerRow, CGColorSpaceRef __nullable space, uint32_t bitmapInfo,
+    size_t bytesPerRow, CGColorSpaceRef cg_nullable space, uint32_t bitmapInfo,
     CGBitmapContextReleaseDataCallback __nullable releaseCallback,
     void * __nullable releaseInfo)
     CG_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_4_0);
@@ -62,64 +62,64 @@
 
 CG_EXTERN CGContextRef __nullable CGBitmapContextCreate(void * __nullable data,
     size_t width, size_t height, size_t bitsPerComponent, size_t bytesPerRow,
-    CGColorSpaceRef __nullable space, uint32_t bitmapInfo)
+    CGColorSpaceRef cg_nullable space, uint32_t bitmapInfo)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the data associated with the bitmap context `context', or NULL if
    `context' is not a bitmap context. */
 
-CG_EXTERN void * __nullable CGBitmapContextGetData(CGContextRef __nullable context)
+CG_EXTERN void * __nullable CGBitmapContextGetData(CGContextRef cg_nullable context)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Return the width of the bitmap context `context', or 0 if `context' is
    not a bitmap context. */
 
-CG_EXTERN size_t CGBitmapContextGetWidth(CGContextRef __nullable context)
+CG_EXTERN size_t CGBitmapContextGetWidth(CGContextRef cg_nullable context)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Return the height of the bitmap context `context', or 0 if `context' is
    not a bitmap context. */
 
-CG_EXTERN size_t CGBitmapContextGetHeight(CGContextRef __nullable context)
+CG_EXTERN size_t CGBitmapContextGetHeight(CGContextRef cg_nullable context)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Return the bits per component of the bitmap context `context', or 0 if
    `context' is not a bitmap context. */
 
-CG_EXTERN size_t CGBitmapContextGetBitsPerComponent(CGContextRef __nullable context)
+CG_EXTERN size_t CGBitmapContextGetBitsPerComponent(CGContextRef cg_nullable context)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Return the bits per pixel of the bitmap context `context', or 0 if
    `context' is not a bitmap context. */
 
-CG_EXTERN size_t CGBitmapContextGetBitsPerPixel(CGContextRef __nullable context)
+CG_EXTERN size_t CGBitmapContextGetBitsPerPixel(CGContextRef cg_nullable context)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Return the bytes per row of the bitmap context `context', or 0 if
    `context' is not a bitmap context. */
 
-CG_EXTERN size_t CGBitmapContextGetBytesPerRow(CGContextRef __nullable context)
+CG_EXTERN size_t CGBitmapContextGetBytesPerRow(CGContextRef cg_nullable context)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Return the color space of the bitmap context `context', or NULL if
    `context' is not a bitmap context. */
 
 CG_EXTERN CGColorSpaceRef __nullable CGBitmapContextGetColorSpace(
-    CGContextRef __nullable context)
+    CGContextRef cg_nullable context)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Return the alpha info of the bitmap context `context', or
    "kCGImageAlphaNone" if `context' is not a bitmap context. */
 
 CG_EXTERN CGImageAlphaInfo CGBitmapContextGetAlphaInfo(
-    CGContextRef __nullable context)
+    CGContextRef cg_nullable context)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Return the bitmap info of the bitmap context `context', or 0 if `context'
    is not a bitmap context. */
 
 CG_EXTERN CGBitmapInfo CGBitmapContextGetBitmapInfo(
-    CGContextRef __nullable context)
+    CGContextRef cg_nullable context)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Return an image containing a snapshot of the bitmap context `context'. If
@@ -136,7 +136,7 @@
    actual physical copy of the data may be avoided. */
 
 CG_EXTERN CGImageRef __nullable CGBitmapContextCreateImage(
-    CGContextRef __nullable context)
+    CGContextRef cg_nullable context)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 CF_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColor.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColor.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColor.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColor.h	2016-06-02 06:59:41.000000000 +0200
@@ -23,8 +23,8 @@
    (including alpha) specified by `components'. `space' may be any color
    space except a pattern color space. */
 
-CG_EXTERN CGColorRef __nullable CGColorCreate(CGColorSpaceRef __nullable space,
-  const CGFloat * __nullable components)
+CG_EXTERN CGColorRef __nullable CGColorCreate(CGColorSpaceRef cg_nullable space,
+  const CGFloat * cg_nullable components)
   CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Create a color in the "Generic" gray color space. */
@@ -50,74 +50,74 @@
    retained and released in a properly nested fashion, just like any other
    CF type. */
 
-CG_EXTERN CGColorRef __nullable CGColorGetConstantColor(CFStringRef __nullable colorName)
+CG_EXTERN CGColorRef __nullable CGColorGetConstantColor(CFStringRef cg_nullable colorName)
   CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_NA);
 
 /* Create a color in color space `space' with pattern `pattern' and
    components `components'. `space' must be a pattern color space. */
 
-CG_EXTERN CGColorRef __nullable CGColorCreateWithPattern(CGColorSpaceRef __nullable space,
-  CGPatternRef __nullable pattern, const CGFloat * __nullable components)
+CG_EXTERN CGColorRef __nullable CGColorCreateWithPattern(CGColorSpaceRef cg_nullable space,
+  CGPatternRef cg_nullable pattern, const CGFloat * cg_nullable components)
   CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Create a copy of `color'. */
 
-CG_EXTERN CGColorRef __nullable CGColorCreateCopy(CGColorRef __nullable color)
+CG_EXTERN CGColorRef __nullable CGColorCreateCopy(CGColorRef cg_nullable color)
   CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Create a copy of `color' with alpha set to `alpha'. */
 
-CG_EXTERN CGColorRef __nullable CGColorCreateCopyWithAlpha(CGColorRef __nullable color,
+CG_EXTERN CGColorRef __nullable CGColorCreateCopyWithAlpha(CGColorRef cg_nullable color,
   CGFloat alpha) CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Create a copy of `color' by matching existing color to destination color space. */
 
-CG_EXTERN CGColorRef __nullable CGColorCreateCopyByMatchingToColorSpace(__nullable CGColorSpaceRef,
-  CGColorRenderingIntent intent, CGColorRef __nullable color, __nullable CFDictionaryRef options)
+CG_EXTERN CGColorRef __nullable CGColorCreateCopyByMatchingToColorSpace(cg_nullable CGColorSpaceRef,
+  CGColorRenderingIntent intent, CGColorRef cg_nullable color, __nullable CFDictionaryRef options)
   CG_AVAILABLE_STARTING(__MAC_10_11, __IPHONE_9_0);
 
 /* Equivalent to `CFRetain(color)', except it doesn't crash (as CFRetain
    does) if `color' is NULL. */
 
-CG_EXTERN CGColorRef __nullable CGColorRetain(CGColorRef __nullable color)
+CG_EXTERN CGColorRef cg_nullable CGColorRetain(CGColorRef cg_nullable color)
   CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Equivalent to `CFRelease(color)', except it doesn't crash (as CFRelease
    does) if `color' is NULL. */
 
-CG_EXTERN void CGColorRelease(CGColorRef __nullable color)
+CG_EXTERN void CGColorRelease(CGColorRef cg_nullable color)
   CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Return true if `color1' is equal to `color2'; false otherwise. */
 
-CG_EXTERN bool CGColorEqualToColor(CGColorRef __nullable color1, CGColorRef __nullable color2)
+CG_EXTERN bool CGColorEqualToColor(CGColorRef cg_nullable color1, CGColorRef cg_nullable color2)
   CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Return the number of color components (including alpha) associated with
    `color'. */
 
-CG_EXTERN size_t CGColorGetNumberOfComponents(CGColorRef __nullable color)
+CG_EXTERN size_t CGColorGetNumberOfComponents(CGColorRef cg_nullable color)
   CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Return the color components (including alpha) associated with `color'. */
 
-CG_EXTERN const CGFloat * __nullable CGColorGetComponents(CGColorRef __nullable color)
+CG_EXTERN const CGFloat * __nullable CGColorGetComponents(CGColorRef cg_nullable color)
   CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Return the alpha component associated with `color'. */
 
-CG_EXTERN CGFloat CGColorGetAlpha(CGColorRef __nullable color)
+CG_EXTERN CGFloat CGColorGetAlpha(CGColorRef cg_nullable color)
   CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Return the color space associated with `color'. */
 
-CG_EXTERN CGColorSpaceRef __nullable CGColorGetColorSpace(CGColorRef __nullable color)
+CG_EXTERN CGColorSpaceRef __nullable CGColorGetColorSpace(CGColorRef cg_nullable color)
   CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Return the pattern associated with `color', if it's a color in a pattern
    color space; NULL otherwise. */
 
-CG_EXTERN CGPatternRef __nullable CGColorGetPattern(CGColorRef __nullable color)
+CG_EXTERN CGPatternRef __nullable CGColorGetPattern(CGColorRef cg_nullable color)
   CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Return the CFTypeID for CGColors. */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConverter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConverter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConverter.h	2016-02-19 23:40:48.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorConverter.h	2016-06-03 04:58:47.000000000 +0200
@@ -5,6 +5,7 @@
 #ifndef CGCOLORCONVERTER_H_
 #define CGCOLORCONVERTER_H_
 
+#include <CoreGraphics/CGBase.h>
 #include <CoreFoundation/CFAvailability.h>
 #include <CoreGraphics/CGColorSpace.h>
 
@@ -29,11 +30,11 @@
  * Requirements: CG color spaces must be calibrated (no Device{Gray,RGB,CMYK}, Indexed or DeviceN).
  */
 CG_EXTERN CGColorConverterRef __nullable CGColorConverterCreate
-  (CFDictionaryRef __nullable options, __nullable CGColorSpaceRef, CGColorConverterTransformType, CGColorRenderingIntent, ...);
+  (CFDictionaryRef __nullable options, cg_nullable CGColorSpaceRef, CGColorConverterTransformType, CGColorRenderingIntent, ...);
 
-CG_EXTERN CGColorConverterRef __nullable CGColorConverterCreateSimple(__nullable CGColorSpaceRef from, __nullable CGColorSpaceRef to);
+CG_EXTERN CGColorConverterRef __nullable CGColorConverterCreateSimple(cg_nullable CGColorSpaceRef from, cg_nullable CGColorSpaceRef to);
 
-CG_EXTERN void CGColorConverterRelease(CGColorConverterRef __nullable);
+CG_EXTERN void CGColorConverterRelease(CGColorConverterRef cg_nullable);
 
 CF_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorSpace.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorSpace.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorSpace.h	2016-02-19 23:50:33.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGColorSpace.h	2016-06-03 04:52:14.000000000 +0200
@@ -66,7 +66,7 @@
   CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_9_0);
   
 CG_EXTERN const CFStringRef kCGColorSpaceDisplayP3
-  CG_AVAILABLE_STARTING(__MAC_10_10, __IPHONE_9_0);
+  CG_AVAILABLE_STARTING(__MAC_10_11_2, __IPHONE_9_3);
 
 /* The name of the "Generic" linear RGB color space. This is the same as
    `kCGColorSpaceGenericRGB' but with a 1.0 gamma. */
@@ -113,19 +113,56 @@
 CG_EXTERN const CFStringRef kCGColorSpaceDCIP3
 CG_AVAILABLE_STARTING(__MAC_10_11, __IPHONE_9_0);
 
+/*  The name of the extended sRGB color space.
+    The extended sRGB color space allows to specify colors beyond the range of [0.0, 1.0],
+    while still preserving the colorimetry and encoding of sRGB (see above for more details).
+    The negative values will be encoded as the signed reflection of original encoding functions,
+    i.e. y(x) = sign(x)*f(abs(x)) where f(x) represents the encoding function. 
+    The capitalization in the name is for avoiding interpretational ambiguity.  */
+
+CG_EXTERN const CFStringRef kCGColorSpaceExtendedSRGB
+CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+
+/*  The name of the sRGB color space variant with linear gamma */
+
+CG_EXTERN const CFStringRef kCGColorSpaceLinearSRGB
+CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+
+/*  The name of the extended sRGB color space variant with linear gamma */
+
+CG_EXTERN const CFStringRef kCGColorSpaceExtendedLinearSRGB
+CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+
+/*  The name of the extended Gray color space. This color space has the same colorimetry as Generic Gray 2.2.
+    The negative values will be encoded as the signed reflection of original encoding functions,
+    i.e. y(x) = sign(x)*f(abs(x)) where f(x) represents the encoding function. */
+
+CG_EXTERN const CFStringRef kCGColorSpaceExtendedGray
+CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+
+/*  The name of the Generic Gray 2.2 color space variant with linear gamma */
+
+CG_EXTERN const CFStringRef kCGColorSpaceLinearGray
+CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+
+/*  The name of the extended Generic Gray 2.2 color space variant with linear gamma */
+
+CG_EXTERN const CFStringRef kCGColorSpaceExtendedLinearGray
+CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+
 /* Create a DeviceGray color space. */
 
-CG_EXTERN CGColorSpaceRef __nullable CGColorSpaceCreateDeviceGray(void)
+CG_EXTERN CGColorSpaceRef cg_nullable CGColorSpaceCreateDeviceGray(void)
   CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Create a DeviceRGB color space. */
 
-CG_EXTERN CGColorSpaceRef __nullable CGColorSpaceCreateDeviceRGB(void)
+CG_EXTERN CGColorSpaceRef cg_nullable CGColorSpaceCreateDeviceRGB(void)
   CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Create a DeviceCMYK color space. */
 
-CG_EXTERN CGColorSpaceRef __nullable CGColorSpaceCreateDeviceCMYK(void)
+CG_EXTERN CGColorSpaceRef cg_nullable CGColorSpaceCreateDeviceCMYK(void)
   CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Create a calibrated gray color space. `whitePoint' is an array of 3
@@ -165,7 +202,7 @@
 /* Create an ICC-based color space using the ICC profile specified by
    `data'. */
 
-CG_EXTERN CGColorSpaceRef __nullable CGColorSpaceCreateWithICCProfile(CFDataRef __nullable data)
+CG_EXTERN CGColorSpaceRef __nullable CGColorSpaceCreateWithICCProfile(CFDataRef cg_nullable data)
   CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Create an ICC-based color space. `nComponents' specifies the number of
@@ -182,7 +219,7 @@
    on whether `nComponents' is 1, 3, or 4, respectively. */
 
 CG_EXTERN CGColorSpaceRef __nullable CGColorSpaceCreateICCBased(size_t nComponents,
-  const CGFloat * __nullable range, CGDataProviderRef __nullable profile,
+  const CGFloat * __nullable range, CGDataProviderRef cg_nullable profile,
   CGColorSpaceRef __nullable alternate)
   CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
@@ -196,8 +233,8 @@
    the range 0 to 255 that is scaled to the range of the corresponding color
    component in the base color space. */
 
-CG_EXTERN CGColorSpaceRef __nullable CGColorSpaceCreateIndexed(CGColorSpaceRef __nullable baseSpace,
-  size_t lastIndex, const unsigned char * __nullable colorTable)
+CG_EXTERN CGColorSpaceRef __nullable CGColorSpaceCreateIndexed(CGColorSpaceRef cg_nullable baseSpace,
+  size_t lastIndex, const unsigned char * cg_nullable colorTable)
   CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Create a pattern color space. `baseSpace' is the underlying color space
@@ -212,32 +249,32 @@
    reference. For MacOS X, `ref' should be a ColorSyncProfileRef. */
 
 CG_EXTERN CGColorSpaceRef __nullable
-  CGColorSpaceCreateWithPlatformColorSpace(const void * __nullable ref)
+  CGColorSpaceCreateWithPlatformColorSpace(const void * cg_nullable ref)
   CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_9_0);
 
 /* Create a color space using `name' as the identifier for the color
    space. */
 
-CG_EXTERN CGColorSpaceRef __nullable CGColorSpaceCreateWithName(CFStringRef __nullable name)
+CG_EXTERN CGColorSpaceRef __nullable CGColorSpaceCreateWithName(CFStringRef cg_nullable name)
   CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Equivalent to `CFRetain(space)', except it doesn't crash (as CFRetain
    does) if `space' is NULL. */
 
-CG_EXTERN CGColorSpaceRef __nullable CGColorSpaceRetain(CGColorSpaceRef __nullable space)
+CG_EXTERN CGColorSpaceRef cg_nullable CGColorSpaceRetain(CGColorSpaceRef cg_nullable space)
   CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Equivalent to `CFRelease(space)', except it doesn't crash (as CFRelease
    does) if `space' is NULL. */
 
-CG_EXTERN void CGColorSpaceRelease(CGColorSpaceRef __nullable space)
+CG_EXTERN void CGColorSpaceRelease(CGColorSpaceRef cg_nullable space)
   CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the name used to create the color space `space', or NULL if the
    color space was not created using `CGColorSpaceCreateWithName'. */
 
-CG_EXTERN CFStringRef __nullable CGColorSpaceCopyName(CGColorSpaceRef __nullable space)
-  CG_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+CG_EXTERN CFStringRef __nullable CGColorSpaceCopyName(CGColorSpaceRef cg_nullable space)
+  CG_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_10_0);
 
 /* Return the CFTypeID for CGColorSpaces. */
 
@@ -246,26 +283,26 @@
 
 /* Return the number of color components in the color space `space'. */
 
-CG_EXTERN size_t CGColorSpaceGetNumberOfComponents(CGColorSpaceRef __nullable space)
+CG_EXTERN size_t CGColorSpaceGetNumberOfComponents(CGColorSpaceRef cg_nullable space)
   CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the color space model of `space'. */
 
-CG_EXTERN CGColorSpaceModel CGColorSpaceGetModel(CGColorSpaceRef __nullable space)
+CG_EXTERN CGColorSpaceModel CGColorSpaceGetModel(CGColorSpaceRef cg_nullable space)
   CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Return the base color space of `space' if `space' is a pattern or indexed
    color space; otherwise, return NULL. To determine whether a color space
    is an indexed or pattern color space, use `CGColorSpaceGetModel'. */
 
-CG_EXTERN CGColorSpaceRef __nullable CGColorSpaceGetBaseColorSpace(CGColorSpaceRef __nullable space)
+CG_EXTERN CGColorSpaceRef __nullable CGColorSpaceGetBaseColorSpace(CGColorSpaceRef cg_nullable space)
   CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Return the number of entries in the color table of `space' if `space' is
    an indexed color space; otherwise, return 0. To determine whether a color
    space is an indexed color space, use `CGColorSpaceGetModel'. */
 
-CG_EXTERN size_t CGColorSpaceGetColorTableCount(CGColorSpaceRef __nullable space)
+CG_EXTERN size_t CGColorSpaceGetColorTableCount(CGColorSpaceRef cg_nullable space)
   CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Copy the entries in the color table of `space' to `table' if `space' is
@@ -275,14 +312,29 @@
    `CGColorSpaceCreateIndexed'. To determine whether a color space is an
    indexed color space, use `CGColorSpaceGetModel'. */
 
-CG_EXTERN void CGColorSpaceGetColorTable(CGColorSpaceRef __nullable space,
-  uint8_t * __nullable table) CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
+CG_EXTERN void CGColorSpaceGetColorTable(CGColorSpaceRef cg_nullable space,
+  uint8_t * cg_nullable table) CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Return a copy of the ICC profile of `space', or NULL if the color space
    doesn't have an ICC profile. */
 
-CG_EXTERN CFDataRef __nullable CGColorSpaceCopyICCProfile(CGColorSpaceRef __nullable space)
-  CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_6_0);
+CG_EXTERN CFDataRef __nullable CGColorSpaceCopyICCProfile(CGColorSpaceRef cg_nullable space);
+//__CG_DEPRECATED_WITH_MSG("Don't this function; call "
+//                         "`CGColorSpaceCopyICCData' instead.");
+
+CG_EXTERN CFDataRef __nullable CGColorSpaceCopyICCData(CGColorSpaceRef cg_nullable space)
+CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+
+/* Return true if gamut of the RGB color space is greater than 75% of NTSC gamut */
+
+CG_EXTERN bool CGColorSpaceIsWideGamutRGB(CGColorSpaceRef)
+CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+
+/* Return true if `space' can be used as a destination color space; false
+ otherwise. */
+
+CG_EXTERN bool CGColorSpaceSupportsOutput(CGColorSpaceRef space)
+CG_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
 
 CF_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGContext.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGContext.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGContext.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGContext.h	2016-06-03 04:58:48.000000000 +0200
@@ -135,13 +135,13 @@
    Note that the path is not considered part of the graphics state, and is
    not saved. */
 
-CG_EXTERN void CGContextSaveGState(CGContextRef __nullable c)
+CG_EXTERN void CGContextSaveGState(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Restore the current graphics state from the one on the top of the
    graphics state stack, popping the graphics state stack in the process. */
 
-CG_EXTERN void CGContextRestoreGState(CGContextRef __nullable c)
+CG_EXTERN void CGContextRestoreGState(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /** Coordinate space transformations. **/
@@ -149,78 +149,78 @@
 /* Scale the current graphics state's transformation matrix (the CTM) by
    `(sx, sy)'. */
 
-CG_EXTERN void CGContextScaleCTM(CGContextRef __nullable c,
+CG_EXTERN void CGContextScaleCTM(CGContextRef cg_nullable c,
     CGFloat sx, CGFloat sy)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Translate the current graphics state's transformation matrix (the CTM) by
    `(tx, ty)'. */
 
-CG_EXTERN void CGContextTranslateCTM(CGContextRef __nullable c,
+CG_EXTERN void CGContextTranslateCTM(CGContextRef cg_nullable c,
     CGFloat tx, CGFloat ty)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Rotate the current graphics state's transformation matrix (the CTM) by
    `angle' radians. */
 
-CG_EXTERN void CGContextRotateCTM(CGContextRef __nullable c, CGFloat angle)
+CG_EXTERN void CGContextRotateCTM(CGContextRef cg_nullable c, CGFloat angle)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Concatenate the current graphics state's transformation matrix (the CTM)
    with the affine transform `transform'. */
 
-CG_EXTERN void CGContextConcatCTM(CGContextRef __nullable c,
+CG_EXTERN void CGContextConcatCTM(CGContextRef cg_nullable c,
     CGAffineTransform transform)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the current graphics state's transformation matrix. Returns 
    CGAffineTransformIdentity in case of inavlid context. */
 
-CG_EXTERN CGAffineTransform CGContextGetCTM(CGContextRef __nullable c)
+CG_EXTERN CGAffineTransform CGContextGetCTM(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /** Drawing attribute functions. **/
 
 /* Set the line width in the current graphics state to `width'. */
 
-CG_EXTERN void CGContextSetLineWidth(CGContextRef __nullable c, CGFloat width)
+CG_EXTERN void CGContextSetLineWidth(CGContextRef cg_nullable c, CGFloat width)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Set the line cap in the current graphics state to `cap'. */
 
-CG_EXTERN void CGContextSetLineCap(CGContextRef __nullable c, CGLineCap cap)
+CG_EXTERN void CGContextSetLineCap(CGContextRef cg_nullable c, CGLineCap cap)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Set the line join in the current graphics state to `join'. */
 
-CG_EXTERN void CGContextSetLineJoin(CGContextRef __nullable c, CGLineJoin join)
+CG_EXTERN void CGContextSetLineJoin(CGContextRef cg_nullable c, CGLineJoin join)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Set the miter limit in the current graphics state to `limit'. */
 
-CG_EXTERN void CGContextSetMiterLimit(CGContextRef __nullable c, CGFloat limit)
+CG_EXTERN void CGContextSetMiterLimit(CGContextRef cg_nullable c, CGFloat limit)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Set the line dash patttern in the current graphics state of `c'. */
 
-CG_EXTERN void CGContextSetLineDash(CGContextRef __nullable c, CGFloat phase,
+CG_EXTERN void CGContextSetLineDash(CGContextRef cg_nullable c, CGFloat phase,
     const CGFloat * __nullable lengths, size_t count)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Set the path flatness parameter in the current graphics state of `c' to
    `flatness'. */
 
-CG_EXTERN void CGContextSetFlatness(CGContextRef __nullable c, CGFloat flatness)
+CG_EXTERN void CGContextSetFlatness(CGContextRef cg_nullable c, CGFloat flatness)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Set the alpha value in the current graphics state of `c' to `alpha'. */
 
-CG_EXTERN void CGContextSetAlpha(CGContextRef __nullable c, CGFloat alpha)
+CG_EXTERN void CGContextSetAlpha(CGContextRef cg_nullable c, CGFloat alpha)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Set the blend mode of `context' to `mode'. */
 
-CG_EXTERN void CGContextSetBlendMode(CGContextRef __nullable c, CGBlendMode mode)
+CG_EXTERN void CGContextSetBlendMode(CGContextRef cg_nullable c, CGBlendMode mode)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /** Path construction functions. **/
@@ -230,56 +230,56 @@
 
 /* Begin a new path. The old path is discarded. */
 
-CG_EXTERN void CGContextBeginPath(CGContextRef __nullable c)
+CG_EXTERN void CGContextBeginPath(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Start a new subpath at point `(x, y)' in the context's path. */
 
-CG_EXTERN void CGContextMoveToPoint(CGContextRef __nullable c,
+CG_EXTERN void CGContextMoveToPoint(CGContextRef cg_nullable c,
     CGFloat x, CGFloat y)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Append a straight line segment from the current point to `(x, y)'. */
 
-CG_EXTERN void CGContextAddLineToPoint(CGContextRef __nullable c,
+CG_EXTERN void CGContextAddLineToPoint(CGContextRef cg_nullable c,
     CGFloat x, CGFloat y)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Append a cubic Bezier curve from the current point to `(x,y)', with
    control points `(cp1x, cp1y)' and `(cp2x, cp2y)'. */
 
-CG_EXTERN void CGContextAddCurveToPoint(CGContextRef __nullable c, CGFloat cp1x,
+CG_EXTERN void CGContextAddCurveToPoint(CGContextRef cg_nullable c, CGFloat cp1x,
     CGFloat cp1y, CGFloat cp2x, CGFloat cp2y, CGFloat x, CGFloat y)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Append a quadratic curve from the current point to `(x, y)', with control
    point `(cpx, cpy)'. */
 
-CG_EXTERN void CGContextAddQuadCurveToPoint(CGContextRef __nullable c,
+CG_EXTERN void CGContextAddQuadCurveToPoint(CGContextRef cg_nullable c,
     CGFloat cpx, CGFloat cpy, CGFloat x, CGFloat y)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Close the current subpath of the context's path. */
 
-CG_EXTERN void CGContextClosePath(CGContextRef __nullable c)
+CG_EXTERN void CGContextClosePath(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /** Path construction convenience functions. **/
 
 /* Add a single rect to the context's path. */
 
-CG_EXTERN void CGContextAddRect(CGContextRef __nullable c, CGRect rect)
+CG_EXTERN void CGContextAddRect(CGContextRef cg_nullable c, CGRect rect)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Add a set of rects to the context's path. */
 
-CG_EXTERN void CGContextAddRects(CGContextRef __nullable c,
+CG_EXTERN void CGContextAddRects(CGContextRef cg_nullable c,
     const CGRect * __nullable rects, size_t count)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Add a set of lines to the context's path. */
 
-CG_EXTERN void CGContextAddLines(CGContextRef __nullable c,
+CG_EXTERN void CGContextAddLines(CGContextRef cg_nullable c,
     const CGPoint * __nullable points, size_t count)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
@@ -287,7 +287,7 @@
    function `CGPathAddEllipseInRect' for more information on how the path
    for the ellipse is constructed. */
 
-CG_EXTERN void CGContextAddEllipseInRect(CGContextRef __nullable c, CGRect rect)
+CG_EXTERN void CGContextAddEllipseInRect(CGContextRef cg_nullable c, CGRect rect)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Add an arc of a circle to the context's path, possibly preceded by a
@@ -297,7 +297,7 @@
    `clockwise' is 1 if the arc is to be drawn clockwise, 0 otherwise.
    `startAngle' and `endAngle' are measured in radians. */
 
-CG_EXTERN void CGContextAddArc(CGContextRef __nullable c, CGFloat x, CGFloat y,
+CG_EXTERN void CGContextAddArc(CGContextRef cg_nullable c, CGFloat x, CGFloat y,
     CGFloat radius, CGFloat startAngle, CGFloat endAngle, int clockwise)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
@@ -306,15 +306,15 @@
    tangent to the line from the current point to `(x1, y1)', and the line
    from `(x1, y1)' to `(x2, y2)'. */
 
-CG_EXTERN void CGContextAddArcToPoint(CGContextRef __nullable c,
+CG_EXTERN void CGContextAddArcToPoint(CGContextRef cg_nullable c,
     CGFloat x1, CGFloat y1, CGFloat x2, CGFloat y2, CGFloat radius)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Add `path' to the path of context. The points in `path' are transformed
    by the CTM of context before they are added. */
 
-CG_EXTERN void CGContextAddPath(CGContextRef __nullable c,
-    CGPathRef __nullable path)
+CG_EXTERN void CGContextAddPath(CGContextRef cg_nullable c,
+    CGPathRef cg_nullable path)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /** Path stroking. **/
@@ -327,7 +327,7 @@
    you can clip to the stroked version of a path by calling this function
    followed by a call to "CGContextClip". */
 
-CG_EXTERN void CGContextReplacePathWithStrokedPath(CGContextRef __nullable c)
+CG_EXTERN void CGContextReplacePathWithStrokedPath(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /** Path information functions. **/
@@ -335,26 +335,26 @@
 /* Return true if the path of `context' contains no elements, false
    otherwise. */
 
-CG_EXTERN bool CGContextIsPathEmpty(CGContextRef __nullable c)
+CG_EXTERN bool CGContextIsPathEmpty(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the current point of the current subpath of the path of
    `context'. */
 
-CG_EXTERN CGPoint CGContextGetPathCurrentPoint(CGContextRef __nullable c)
+CG_EXTERN CGPoint CGContextGetPathCurrentPoint(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the bounding box of the path of `context'. The bounding box is the
    smallest rectangle completely enclosing all points in the path, including
    control points for Bezier and quadratic curves. */
 
-CG_EXTERN CGRect CGContextGetPathBoundingBox(CGContextRef __nullable c)
+CG_EXTERN CGRect CGContextGetPathBoundingBox(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return a copy of the path of `context'. The returned path is specified in
    the current user space of `context'. */
 
-CG_EXTERN CGPathRef __nullable CGContextCopyPath(CGContextRef __nullable c)
+CG_EXTERN CGPathRef __nullable CGContextCopyPath(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Return true if `point' is contained in the current path of `context'. A
@@ -362,7 +362,7 @@
    region when the path is stroked or filled with opaque colors using the
    path drawing mode `mode'. `point' is specified is user space. */
 
-CG_EXTERN bool CGContextPathContainsPoint(CGContextRef __nullable c,
+CG_EXTERN bool CGContextPathContainsPoint(CGContextRef cg_nullable c,
     CGPoint point, CGPathDrawingMode mode)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
@@ -370,7 +370,7 @@
 
 /* Draw the context's path using drawing mode `mode'. */
 
-CG_EXTERN void CGContextDrawPath(CGContextRef __nullable c,
+CG_EXTERN void CGContextDrawPath(CGContextRef cg_nullable c,
     CGPathDrawingMode mode)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
@@ -379,58 +379,58 @@
 /* Fill the context's path using the winding-number fill rule. Any open
    subpath of the path is implicitly closed. */
 
-CG_EXTERN void CGContextFillPath(CGContextRef __nullable c)
+CG_EXTERN void CGContextFillPath(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Fill the context's path using the even-odd fill rule. Any open subpath of
    the path is implicitly closed. */
 
-CG_EXTERN void CGContextEOFillPath(CGContextRef __nullable c)
+CG_EXTERN void CGContextEOFillPath(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Stroke the context's path. */
 
-CG_EXTERN void CGContextStrokePath(CGContextRef __nullable c)
+CG_EXTERN void CGContextStrokePath(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Fill `rect' with the current fill color. */
 
-CG_EXTERN void CGContextFillRect(CGContextRef __nullable c, CGRect rect)
+CG_EXTERN void CGContextFillRect(CGContextRef cg_nullable c, CGRect rect)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Fill `rects', an array of `count' CGRects, with the current fill
    color. */
 
-CG_EXTERN void CGContextFillRects(CGContextRef __nullable c,
+CG_EXTERN void CGContextFillRects(CGContextRef cg_nullable c,
     const CGRect * __nullable rects, size_t count)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Stroke `rect' with the current stroke color and the current linewidth. */
 
-CG_EXTERN void CGContextStrokeRect(CGContextRef __nullable c, CGRect rect)
+CG_EXTERN void CGContextStrokeRect(CGContextRef cg_nullable c, CGRect rect)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Stroke `rect' with the current stroke color, using `width' as the the
    line width. */
 
-CG_EXTERN void CGContextStrokeRectWithWidth(CGContextRef __nullable c,
+CG_EXTERN void CGContextStrokeRectWithWidth(CGContextRef cg_nullable c,
     CGRect rect, CGFloat width)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Clear `rect' (that is, set the region within the rect to transparent). */
 
-CG_EXTERN void CGContextClearRect(CGContextRef __nullable c, CGRect rect)
+CG_EXTERN void CGContextClearRect(CGContextRef cg_nullable c, CGRect rect)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Fill an ellipse (an oval) inside `rect'. */
 
-CG_EXTERN void CGContextFillEllipseInRect(CGContextRef __nullable c,
+CG_EXTERN void CGContextFillEllipseInRect(CGContextRef cg_nullable c,
     CGRect rect)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Stroke an ellipse (an oval) inside `rect'. */
 
-CG_EXTERN void CGContextStrokeEllipseInRect(CGContextRef __nullable c,
+CG_EXTERN void CGContextStrokeEllipseInRect(CGContextRef cg_nullable c,
     CGRect rect)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
@@ -445,7 +445,7 @@
      }
      CGContextStrokePath(context); */
 
-CG_EXTERN void CGContextStrokeLineSegments(CGContextRef __nullable c,
+CG_EXTERN void CGContextStrokeLineSegments(CGContextRef cg_nullable c,
     const CGPoint * __nullable points, size_t count)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
@@ -455,14 +455,14 @@
    resulting path as the clip path for subsequent rendering operations. Use
    the winding-number fill rule for deciding what's inside the path. */
 
-CG_EXTERN void CGContextClip(CGContextRef __nullable c)
+CG_EXTERN void CGContextClip(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Intersect the context's path with the current clip path and use the
    resulting path as the clip path for subsequent rendering operations. Use
    the even-odd fill rule for deciding what's inside the path. */
 
-CG_EXTERN void CGContextEOClip(CGContextRef __nullable c)
+CG_EXTERN void CGContextEOClip(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Add `mask' transformed to `rect' to the clipping area of `context'. The
@@ -492,15 +492,15 @@
    not have alpha, and may not be masked by an image mask or masking
    color. */
 
-CG_EXTERN void CGContextClipToMask(CGContextRef __nullable c, CGRect rect,
-    CGImageRef __nullable mask)
+CG_EXTERN void CGContextClipToMask(CGContextRef cg_nullable c, CGRect rect,
+    CGImageRef cg_nullable mask)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Return the bounding box of the clip path of `c' in user space. The
    bounding box is the smallest rectangle completely enclosing all points in
    the clip. */
 
-CG_EXTERN CGRect CGContextGetClipBoundingBox(CGContextRef __nullable c)
+CG_EXTERN CGRect CGContextGetClipBoundingBox(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /** Clipping convenience functions. **/
@@ -508,14 +508,14 @@
 /* Intersect the current clipping path with `rect'. Note that this function
    resets the context's path to the empty path. */
 
-CG_EXTERN void CGContextClipToRect(CGContextRef __nullable c, CGRect rect)
+CG_EXTERN void CGContextClipToRect(CGContextRef cg_nullable c, CGRect rect)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Intersect the current clipping path with the clipping region formed by
    creating a path consisting of all rects in `rects'. Note that this
    function resets the context's path to the empty path. */
 
-CG_EXTERN void CGContextClipToRects(CGContextRef __nullable c,
+CG_EXTERN void CGContextClipToRects(CGContextRef cg_nullable c,
     const CGRect *  rects, size_t count)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
@@ -523,14 +523,14 @@
 
 /* Set the current fill color in the context `c' to `color'. */
 
-CG_EXTERN void CGContextSetFillColorWithColor(CGContextRef __nullable c,
-    CGColorRef __nullable color)
+CG_EXTERN void CGContextSetFillColorWithColor(CGContextRef cg_nullable c,
+    CGColorRef cg_nullable color)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Set the current stroke color in the context `c' to `color'. */
 
-CG_EXTERN void CGContextSetStrokeColorWithColor(CGContextRef __nullable c,
-    CGColorRef __nullable color)
+CG_EXTERN void CGContextSetStrokeColorWithColor(CGContextRef cg_nullable c,
+    CGColorRef cg_nullable color)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /** Color space functions. **/
@@ -539,16 +539,16 @@
    side-effect, set the fill color to a default value appropriate for the
    color space. */
 
-CG_EXTERN void CGContextSetFillColorSpace(CGContextRef __nullable c,
-    CGColorSpaceRef __nullable space)
+CG_EXTERN void CGContextSetFillColorSpace(CGContextRef cg_nullable c,
+    CGColorSpaceRef cg_nullable space)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Set the current stroke color space in `context' to `space'. As a
    side-effect, set the stroke color to a default value appropriate for the
    color space. */
 
-CG_EXTERN void CGContextSetStrokeColorSpace(CGContextRef __nullable c,
-    CGColorSpaceRef __nullable space)
+CG_EXTERN void CGContextSetStrokeColorSpace(CGContextRef cg_nullable c,
+    CGColorSpaceRef cg_nullable space)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /** Color functions. **/
@@ -559,8 +559,8 @@
    (N color components + 1 alpha component). The current fill color space
    must not be a pattern color space. */
 
-CG_EXTERN void CGContextSetFillColor(CGContextRef __nullable c,
-    const CGFloat * __nullable components)
+CG_EXTERN void CGContextSetFillColor(CGContextRef cg_nullable c,
+    const CGFloat * cg_nullable components)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Set the components of the current stroke color in `context' to the values
@@ -569,8 +569,8 @@
    space (N color components + 1 alpha component). The current stroke color
    space must not be a pattern color space. */
 
-CG_EXTERN void CGContextSetStrokeColor(CGContextRef __nullable c,
-    const CGFloat * __nullable components)
+CG_EXTERN void CGContextSetStrokeColor(CGContextRef cg_nullable c,
+    const CGFloat * cg_nullable components)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /** Pattern functions. **/
@@ -582,8 +582,8 @@
    + 1 alpha component). The current fill color space must be a pattern
    color space. */
 
-CG_EXTERN void CGContextSetFillPattern(CGContextRef __nullable c,
-    CGPatternRef __nullable pattern, const CGFloat * __nullable components)
+CG_EXTERN void CGContextSetFillPattern(CGContextRef cg_nullable c,
+    CGPatternRef cg_nullable pattern, const CGFloat * cg_nullable components)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Set the components of the current stroke color in `context' to the values
@@ -593,14 +593,14 @@
    components + 1 alpha component). The current stroke color space must be a
    pattern color space. */
 
-CG_EXTERN void CGContextSetStrokePattern(CGContextRef __nullable c,
-    CGPatternRef __nullable pattern, const CGFloat * __nullable components)
+CG_EXTERN void CGContextSetStrokePattern(CGContextRef cg_nullable c,
+    CGPatternRef cg_nullable pattern, const CGFloat * cg_nullable components)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Set the pattern phase in the current graphics state of `context' to
    `phase'. */
 
-CG_EXTERN void CGContextSetPatternPhase(CGContextRef __nullable c, CGSize phase)
+CG_EXTERN void CGContextSetPatternPhase(CGContextRef cg_nullable c, CGSize phase)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /** Color convenience functions. **/
@@ -608,21 +608,21 @@
 /* Set the current fill color space in `context' to `DeviceGray' and set the
    components of the current fill color to `(gray, alpha)'. */
 
-CG_EXTERN void CGContextSetGrayFillColor(CGContextRef __nullable c,
+CG_EXTERN void CGContextSetGrayFillColor(CGContextRef cg_nullable c,
     CGFloat gray, CGFloat alpha)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Set the current stroke color space in `context' to `DeviceGray' and set
    the components of the current stroke color to `(gray, alpha)'. */
 
-CG_EXTERN void CGContextSetGrayStrokeColor(CGContextRef __nullable c,
+CG_EXTERN void CGContextSetGrayStrokeColor(CGContextRef cg_nullable c,
     CGFloat gray, CGFloat alpha)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Set the current fill color space in `context' to `DeviceRGB' and set the
    components of the current fill color to `(red, green, blue, alpha)'. */
 
-CG_EXTERN void CGContextSetRGBFillColor(CGContextRef __nullable c, CGFloat red,
+CG_EXTERN void CGContextSetRGBFillColor(CGContextRef cg_nullable c, CGFloat red,
     CGFloat green, CGFloat blue, CGFloat alpha)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
@@ -630,7 +630,7 @@
    the components of the current stroke color to `(red, green, blue,
    alpha)'. */
 
-CG_EXTERN void CGContextSetRGBStrokeColor(CGContextRef __nullable c,
+CG_EXTERN void CGContextSetRGBStrokeColor(CGContextRef cg_nullable c,
     CGFloat red, CGFloat green, CGFloat blue, CGFloat alpha)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
@@ -638,7 +638,7 @@
    components of the current fill color to `(cyan, magenta, yellow, black,
    alpha)'. */
 
-CG_EXTERN void CGContextSetCMYKFillColor(CGContextRef __nullable c,
+CG_EXTERN void CGContextSetCMYKFillColor(CGContextRef cg_nullable c,
     CGFloat cyan, CGFloat magenta, CGFloat yellow, CGFloat black, CGFloat alpha)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
@@ -646,7 +646,7 @@
    the components of the current stroke color to `(cyan, magenta, yellow,
    black, alpha)'. */
 
-CG_EXTERN void CGContextSetCMYKStrokeColor(CGContextRef __nullable c,
+CG_EXTERN void CGContextSetCMYKStrokeColor(CGContextRef cg_nullable c,
     CGFloat cyan, CGFloat magenta, CGFloat yellow, CGFloat black, CGFloat alpha)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
@@ -655,7 +655,7 @@
 /* Set the rendering intent in the current graphics state of `context' to
    `intent'. */
 
-CG_EXTERN void CGContextSetRenderingIntent(CGContextRef __nullable c,
+CG_EXTERN void CGContextSetRenderingIntent(CGContextRef cg_nullable c,
     CGColorRenderingIntent intent)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
@@ -664,8 +664,8 @@
 /* Draw `image' in the rectangular area specified by `rect' in the context
    `c'. The image is scaled, if necessary, to fit into `rect'. */
 
-CG_EXTERN void CGContextDrawImage(CGContextRef __nullable c, CGRect rect,
-    CGImageRef __nullable image)
+CG_EXTERN void CGContextDrawImage(CGContextRef cg_nullable c, CGRect rect,
+    CGImageRef cg_nullable image)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Draw `image' tiled in the context `c'. The image is scaled to the size
@@ -675,8 +675,8 @@
    Unlike patterns, the image is tiled in user space, so transformations
    applied to the CTM affect the final result. */
 
-CG_EXTERN void CGContextDrawTiledImage(CGContextRef __nullable c, CGRect rect,
-    CGImageRef __nullable image)
+CG_EXTERN void CGContextDrawTiledImage(CGContextRef cg_nullable c, CGRect rect,
+    CGImageRef cg_nullable image)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Return the interpolation quality for image rendering of `context'. The
@@ -686,12 +686,12 @@
    contexts support all interpolation quality levels. */
 
 CG_EXTERN CGInterpolationQuality
-    CGContextGetInterpolationQuality(CGContextRef __nullable c)
+    CGContextGetInterpolationQuality(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Set the interpolation quality of `context' to `quality'. */
 
-CG_EXTERN void CGContextSetInterpolationQuality(CGContextRef __nullable c,
+CG_EXTERN void CGContextSetInterpolationQuality(CGContextRef cg_nullable c,
     CGInterpolationQuality quality)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
@@ -706,7 +706,7 @@
    turn off shadowing, set the shadow color to a fully transparent color (or
    pass NULL as the color), or use the standard gsave/grestore mechanism. */
 
-CG_EXTERN void CGContextSetShadowWithColor(CGContextRef __nullable c,
+CG_EXTERN void CGContextSetShadowWithColor(CGContextRef cg_nullable c,
     CGSize offset, CGFloat blur, CGColorRef __nullable color)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
@@ -715,7 +715,7 @@
    where color is black with 1/3 alpha (i.e., RGBA = {0, 0, 0, 1.0/3.0}) in
    the DeviceRGB color space. */
 
-CG_EXTERN void CGContextSetShadow(CGContextRef __nullable c, CGSize offset,
+CG_EXTERN void CGContextSetShadow(CGContextRef cg_nullable c, CGSize offset,
     CGFloat blur)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
@@ -728,8 +728,8 @@
    values of the gradient's locations. The option flags control whether the
    gradient is drawn before the start point or after the end point. */
 
-CG_EXTERN void CGContextDrawLinearGradient(CGContextRef __nullable c,
-    CGGradientRef __nullable gradient, CGPoint startPoint, CGPoint endPoint,
+CG_EXTERN void CGContextDrawLinearGradient(CGContextRef cg_nullable c,
+    CGGradientRef cg_nullable gradient, CGPoint startPoint, CGPoint endPoint,
     CGGradientDrawingOptions options)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
@@ -742,15 +742,15 @@
    values of the gradient's locations. The option flags control whether the
    gradient is drawn before the start circle or after the end circle. */
 
-CG_EXTERN void CGContextDrawRadialGradient(CGContextRef __nullable c,
-    CGGradientRef __nullable gradient, CGPoint startCenter, CGFloat startRadius,
+CG_EXTERN void CGContextDrawRadialGradient(CGContextRef cg_nullable c,
+    CGGradientRef cg_nullable gradient, CGPoint startCenter, CGFloat startRadius,
     CGPoint endCenter, CGFloat endRadius, CGGradientDrawingOptions options)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Fill the current clipping region of `context' with `shading'. */
 
-CG_EXTERN void CGContextDrawShading(CGContextRef __nullable c,
-    __nullable CGShadingRef shading)
+CG_EXTERN void CGContextDrawShading(CGContextRef cg_nullable c,
+    cg_nullable CGShadingRef shading)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /** Text functions. **/
@@ -759,60 +759,60 @@
    character spacing is added to the displacement between the origin of one
    character and the origin of the next. */
 
-CG_EXTERN void CGContextSetCharacterSpacing(CGContextRef __nullable c,
+CG_EXTERN void CGContextSetCharacterSpacing(CGContextRef cg_nullable c,
     CGFloat spacing)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Set the user-space point at which text will be drawn in the context `c'
    to `(x, y)'. */
 
-CG_EXTERN void CGContextSetTextPosition(CGContextRef __nullable c,
+CG_EXTERN void CGContextSetTextPosition(CGContextRef cg_nullable c,
     CGFloat x, CGFloat y)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the user-space point at which text will be drawn in `context'. */
 
-CG_EXTERN CGPoint CGContextGetTextPosition(CGContextRef __nullable c)
+CG_EXTERN CGPoint CGContextGetTextPosition(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Set the text matrix in the context `c' to `t'. */
 
-CG_EXTERN void CGContextSetTextMatrix(CGContextRef __nullable c,
+CG_EXTERN void CGContextSetTextMatrix(CGContextRef cg_nullable c,
     CGAffineTransform t)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the text matrix in the context `c'. Returns CGAffineTransformIdentity
    if `c' is not a valid context. */
 
-CG_EXTERN CGAffineTransform CGContextGetTextMatrix(CGContextRef __nullable c)
+CG_EXTERN CGAffineTransform CGContextGetTextMatrix(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Set the text drawing mode in the current graphics state of the context
    `c' to `mode'. */
 
-CG_EXTERN void CGContextSetTextDrawingMode(CGContextRef __nullable c,
+CG_EXTERN void CGContextSetTextDrawingMode(CGContextRef cg_nullable c,
     CGTextDrawingMode mode)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Set the font in the current graphics state of the context `c' to
    `font'. */
 
-CG_EXTERN void CGContextSetFont(CGContextRef __nullable c,
-    CGFontRef __nullable font)
+CG_EXTERN void CGContextSetFont(CGContextRef cg_nullable c,
+    CGFontRef cg_nullable font)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Set the font size in the current graphics state of the context `c' to
    `size'. */
 
-CG_EXTERN void CGContextSetFontSize(CGContextRef __nullable c, CGFloat size)
+CG_EXTERN void CGContextSetFontSize(CGContextRef cg_nullable c, CGFloat size)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Draw `glyphs', an array of `count' CGGlyphs, at the points specified by
    `positions'. Each element of `positions' specifies the position from the
    associated glyph; the positions are specified in user space. */
 
-CG_EXTERN void CGContextShowGlyphsAtPositions(CGContextRef __nullable c,
-    const CGGlyph * __nullable glyphs, const CGPoint * __nullable Lpositions,
+CG_EXTERN void CGContextShowGlyphsAtPositions(CGContextRef cg_nullable c,
+    const CGGlyph * cg_nullable glyphs, const CGPoint * cg_nullable Lpositions,
     size_t count)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
@@ -820,43 +820,43 @@
 
 /* Draw `page' in the current user space of the context `c'. */
 
-CG_EXTERN void CGContextDrawPDFPage(CGContextRef __nullable c,
-    CGPDFPageRef __nullable page)
+CG_EXTERN void CGContextDrawPDFPage(CGContextRef cg_nullable c,
+    CGPDFPageRef cg_nullable page)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /** Output page functions. **/
 
 /* Begin a new page. */
 
-CG_EXTERN void CGContextBeginPage(CGContextRef __nullable c,
+CG_EXTERN void CGContextBeginPage(CGContextRef cg_nullable c,
     const CGRect * __nullable mediaBox)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* End the current page. */
 
-CG_EXTERN void CGContextEndPage(CGContextRef __nullable c)
+CG_EXTERN void CGContextEndPage(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /** Context functions. **/
 
 /* Equivalent to `CFRetain(c)'. */
 
-CG_EXTERN CGContextRef __nullable CGContextRetain(CGContextRef __nullable c)
+CG_EXTERN CGContextRef cg_nullable CGContextRetain(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Equivalent to `CFRelease(c)'. */
 
-CG_EXTERN void CGContextRelease(CGContextRef __nullable c)
+CG_EXTERN void CGContextRelease(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Flush all drawing to the destination. */
 
-CG_EXTERN void CGContextFlush(CGContextRef __nullable c)
+CG_EXTERN void CGContextFlush(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Synchronized drawing. */
 
-CG_EXTERN void CGContextSynchronize(CGContextRef __nullable c)
+CG_EXTERN void CGContextSynchronize(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /** Antialiasing functions. **/
@@ -864,7 +864,7 @@
 /* Turn on antialiasing if `shouldAntialias' is true; turn it off otherwise.
    This parameter is part of the graphics state. */
 
-CG_EXTERN void CGContextSetShouldAntialias(CGContextRef __nullable c,
+CG_EXTERN void CGContextSetShouldAntialias(CGContextRef cg_nullable c,
     bool shouldAntialias)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
@@ -873,7 +873,7 @@
    context will perform antialiasing if both `allowsAntialiasing' and the
    graphics state parameter `shouldAntialias' are true. */
 
-CG_EXTERN void CGContextSetAllowsAntialiasing(CGContextRef __nullable c,
+CG_EXTERN void CGContextSetAllowsAntialiasing(CGContextRef cg_nullable c,
     bool allowsAntialiasing)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
@@ -884,7 +884,7 @@
    doesn't guarantee that font smoothing will occur: not all destination
    contexts support font smoothing. */
 
-CG_EXTERN void CGContextSetShouldSmoothFonts(CGContextRef __nullable c,
+CG_EXTERN void CGContextSetShouldSmoothFonts(CGContextRef cg_nullable c,
     bool shouldSmoothFonts)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
@@ -894,7 +894,7 @@
    they are antialiased when drawn and if both `allowsFontSmoothing' and the
    graphics state parameter `shouldSmoothFonts' are true. */
  
-CG_EXTERN void CGContextSetAllowsFontSmoothing(CGContextRef __nullable c,
+CG_EXTERN void CGContextSetAllowsFontSmoothing(CGContextRef cg_nullable c,
     bool allowsFontSmoothing)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
@@ -904,7 +904,7 @@
    parameter is part of the graphics state. */
 
 CG_EXTERN void CGContextSetShouldSubpixelPositionFonts(
-    CGContextRef __nullable c, bool shouldSubpixelPositionFonts)
+    CGContextRef cg_nullable c, bool shouldSubpixelPositionFonts)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* If `allowsFontSubpixelPositioning' is true, then allow font subpixel
@@ -915,7 +915,7 @@
    the graphics state parameter `shouldSubpixelPositionFonts' are true. */
 
 CG_EXTERN void CGContextSetAllowsFontSubpixelPositioning(
-    CGContextRef __nullable c, bool allowsFontSubpixelPositioning)
+    CGContextRef cg_nullable c, bool allowsFontSubpixelPositioning)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* If `shouldSubpixelQuantizeFonts' is true, then quantize the subpixel
@@ -924,7 +924,7 @@
    state. */
 
 CG_EXTERN void CGContextSetShouldSubpixelQuantizeFonts(
-    CGContextRef __nullable c, bool shouldSubpixelQuantizeFonts)
+    CGContextRef cg_nullable c, bool shouldSubpixelQuantizeFonts)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* If `allowsFontSubpixelQuantization' is true, then allow font subpixel
@@ -935,7 +935,7 @@
    state parameter `shouldSubpixelQuantizeFonts' are both true. */
 
 CG_EXTERN void CGContextSetAllowsFontSubpixelQuantization(
-    CGContextRef __nullable c, bool allowsFontSubpixelQuantization)
+    CGContextRef cg_nullable c, bool allowsFontSubpixelQuantization)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /** Transparency layer support. **/
@@ -956,7 +956,7 @@
    they had before `CGContextBeginTransparencyLayer' was called.
    Transparency layers may be nested. */
 
-CG_EXTERN void CGContextBeginTransparencyLayer(CGContextRef __nullable c,
+CG_EXTERN void CGContextBeginTransparencyLayer(CGContextRef cg_nullable c,
     CFDictionaryRef __nullable auxiliaryInfo)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
@@ -965,12 +965,12 @@
   transparency layer will be bounded by `rect' (specified in user space). */
 
 CG_EXTERN void CGContextBeginTransparencyLayerWithRect(
-    CGContextRef __nullable c, CGRect rect, CFDictionaryRef __nullable auxInfo)
+    CGContextRef cg_nullable c, CGRect rect, CFDictionaryRef __nullable auxInfo)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* End a tranparency layer. */
 
-CG_EXTERN void CGContextEndTransparencyLayer(CGContextRef __nullable c)
+CG_EXTERN void CGContextEndTransparencyLayer(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /** User space to device space tranformations. **/
@@ -979,30 +979,30 @@
    of `context' to device space (pixels). */
 
 CG_EXTERN CGAffineTransform
-    CGContextGetUserSpaceToDeviceSpaceTransform(CGContextRef __nullable c)
+    CGContextGetUserSpaceToDeviceSpaceTransform(CGContextRef cg_nullable c)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Transform `point' from the user space of `context' to device space. */
 
-CG_EXTERN CGPoint CGContextConvertPointToDeviceSpace(CGContextRef __nullable c,
+CG_EXTERN CGPoint CGContextConvertPointToDeviceSpace(CGContextRef cg_nullable c,
     CGPoint point)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Transform `point' from device space to the user space of `context'. */
 
-CG_EXTERN CGPoint CGContextConvertPointToUserSpace(CGContextRef __nullable c,
+CG_EXTERN CGPoint CGContextConvertPointToUserSpace(CGContextRef cg_nullable c,
     CGPoint point)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Transform `size' from the user space of `context' to device space. */
 
-CG_EXTERN CGSize CGContextConvertSizeToDeviceSpace(CGContextRef __nullable c,
+CG_EXTERN CGSize CGContextConvertSizeToDeviceSpace(CGContextRef cg_nullable c,
     CGSize size)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Transform `size' from device space to the user space of `context'. */
 
-CG_EXTERN CGSize CGContextConvertSizeToUserSpace(CGContextRef __nullable c,
+CG_EXTERN CGSize CGContextConvertSizeToUserSpace(CGContextRef cg_nullable c,
     CGSize size)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
@@ -1011,7 +1011,7 @@
    returns the smallest rectangle which contains the transformed corner
    points of `rect'. */
 
-CG_EXTERN CGRect CGContextConvertRectToDeviceSpace(CGContextRef __nullable c,
+CG_EXTERN CGRect CGContextConvertRectToDeviceSpace(CGContextRef cg_nullable c,
     CGRect rect)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
@@ -1020,7 +1020,7 @@
    returns the smallest rectangle which contains the transformed corner
    points of `rect'. */
 
-CG_EXTERN CGRect CGContextConvertRectToUserSpace(CGContextRef __nullable c,
+CG_EXTERN CGRect CGContextConvertRectToUserSpace(CGContextRef cg_nullable c,
     CGRect rect)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
@@ -1028,42 +1028,42 @@
 
 /* DEPRECATED; use the CoreText API instead. */
 
-CG_EXTERN void CGContextSelectFont(CGContextRef __nullable c,
-    const char * __nullable name, CGFloat size, CGTextEncoding textEncoding)
+CG_EXTERN void CGContextSelectFont(CGContextRef cg_nullable c,
+    const char * cg_nullable name, CGFloat size, CGTextEncoding textEncoding)
     CG_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_9,
                                 __IPHONE_2_0, __IPHONE_7_0);
 
 /* DEPRECATED; use the CoreText API instead. */
 
-CG_EXTERN void CGContextShowText(CGContextRef __nullable c,
-    const char * __nullable string, size_t length)
+CG_EXTERN void CGContextShowText(CGContextRef cg_nullable c,
+    const char * cg_nullable string, size_t length)
     CG_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_9,
                                 __IPHONE_2_0, __IPHONE_7_0);
 
 /* DEPRECATED; use the CoreText API instead. */
 
-CG_EXTERN void CGContextShowTextAtPoint(CGContextRef __nullable c,
-    CGFloat x, CGFloat y, const char * __nullable string, size_t length)
+CG_EXTERN void CGContextShowTextAtPoint(CGContextRef cg_nullable c,
+    CGFloat x, CGFloat y, const char * cg_nullable string, size_t length)
     CG_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_9,
                                 __IPHONE_2_0, __IPHONE_7_0);
 
 /* DEPRECATED; use the CoreText API instead. */
 
-CG_EXTERN void CGContextShowGlyphs(CGContextRef __nullable c,
+CG_EXTERN void CGContextShowGlyphs(CGContextRef cg_nullable c,
     const CGGlyph * __nullable g, size_t count)
     CG_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_9,
                                 __IPHONE_2_0, __IPHONE_7_0);
 
 /* DEPRECATED; use the CoreText API instead. */
 
-CG_EXTERN void CGContextShowGlyphsAtPoint(CGContextRef __nullable c, CGFloat x,
+CG_EXTERN void CGContextShowGlyphsAtPoint(CGContextRef cg_nullable c, CGFloat x,
     CGFloat y, const CGGlyph * __nullable glyphs, size_t count)
     CG_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_9,
                                 __IPHONE_2_0, __IPHONE_7_0);
 
 /* DEPRECATED; use the CoreText API instead. */
 
-CG_EXTERN void CGContextShowGlyphsWithAdvances(CGContextRef __nullable c,
+CG_EXTERN void CGContextShowGlyphsWithAdvances(CGContextRef cg_nullable c,
     const CGGlyph * __nullable glyphs, const CGSize * __nullable advances,
     size_t count)
     CG_AVAILABLE_BUT_DEPRECATED(__MAC_10_3, __MAC_10_9,
@@ -1071,8 +1071,8 @@
 
 /* DEPRECATED; use the CGPDFPage API instead. */
 
-CG_EXTERN void CGContextDrawPDFDocument(CGContextRef __nullable c, CGRect rect,
-    CGPDFDocumentRef __nullable document, int page)
+CG_EXTERN void CGContextDrawPDFDocument(CGContextRef cg_nullable c, CGRect rect,
+    CGPDFDocumentRef cg_nullable document, int page)
     CG_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_5,
                                 __IPHONE_NA, __IPHONE_NA);
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGDataConsumer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGDataConsumer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGDataConsumer.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGDataConsumer.h	2016-06-03 04:58:47.000000000 +0200
@@ -50,34 +50,34 @@
    passed to each of the callback functions. */
 
 CG_EXTERN CGDataConsumerRef __nullable CGDataConsumerCreate(
-    void * __nullable info, const CGDataConsumerCallbacks * __nullable cbks)
+    void * __nullable info, const CGDataConsumerCallbacks * cg_nullable cbks)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Create a data consumer which writes data to `url'. */
 
 CG_EXTERN CGDataConsumerRef __nullable CGDataConsumerCreateWithURL(
-    CFURLRef __nullable url)
+    CFURLRef cg_nullable url)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Create a data consumer which writes to `data'. */
 
 CG_EXTERN CGDataConsumerRef __nullable CGDataConsumerCreateWithCFData(
-    CFMutableDataRef __nullable data)
+    CFMutableDataRef cg_nullable data)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Equivalent to `CFRetain(consumer)'. */
 
-CG_EXTERN CGDataConsumerRef __nullable CGDataConsumerRetain(
-    CGDataConsumerRef __nullable consumer)
+CG_EXTERN CGDataConsumerRef cg_nullable CGDataConsumerRetain(
+    CGDataConsumerRef cg_nullable consumer)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Equivalent to `CFRelease(consumer)'. */
 
-CG_EXTERN void CGDataConsumerRelease(__nullable CGDataConsumerRef consumer)
+CG_EXTERN void CGDataConsumerRelease(cg_nullable CGDataConsumerRef consumer)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 CF_ASSUME_NONNULL_END
 
 CF_IMPLICIT_BRIDGING_DISABLED
 
-#endif	/* CGDATACONSUMER_H_ */
+#endif  /* CGDATACONSUMER_H_ */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGDataProvider.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGDataProvider.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGDataProvider.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGDataProvider.h	2016-05-26 06:29:44.000000000 +0200
@@ -115,7 +115,7 @@
 
 CG_EXTERN CGDataProviderRef __nullable CGDataProviderCreateSequential(
     void * __nullable info,
-    const CGDataProviderSequentialCallbacks * __nullable callbacks)
+    const CGDataProviderSequentialCallbacks * cg_nullable callbacks)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Create a direct-access data provider using `callbacks' to supply `size'
@@ -124,7 +124,7 @@
 
 CG_EXTERN CGDataProviderRef __nullable CGDataProviderCreateDirect(
     void * __nullable info, off_t size,
-    const CGDataProviderDirectCallbacks * __nullable callbacks)
+    const CGDataProviderDirectCallbacks * cg_nullable callbacks)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* The callback used by `CGDataProviderCreateWithData'. */
@@ -137,39 +137,39 @@
    passed `info' as its first argument. */
 
 CG_EXTERN CGDataProviderRef __nullable CGDataProviderCreateWithData(
-    void * __nullable info, const void * __nullable data, size_t size,
-    CGDataProviderReleaseDataCallback __nullable releaseData)
+    void * __nullable info, const void * cg_nullable data, size_t size,
+    CGDataProviderReleaseDataCallback cg_nullable releaseData)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Create a direct-access data provider which reads from `data'. */
 
 CG_EXTERN CGDataProviderRef __nullable CGDataProviderCreateWithCFData(
-    CFDataRef __nullable data)
+    CFDataRef cg_nullable data)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Create a data provider reading from `url'. */
 
 CG_EXTERN CGDataProviderRef __nullable CGDataProviderCreateWithURL(
-    CFURLRef __nullable url)
+    CFURLRef cg_nullable url)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Create a data provider reading from `filename'. */
 
 CG_EXTERN CGDataProviderRef __nullable CGDataProviderCreateWithFilename(
-    const char * __nullable filename)
+    const char * cg_nullable filename)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Equivalent to `CFRetain(provider)', but doesn't crash (as CFRetain does)
    if `provider' is NULL. */
 
 CG_EXTERN CGDataProviderRef __nullable CGDataProviderRetain(
-    CGDataProviderRef __nullable provider)
+    CGDataProviderRef cg_nullable provider)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Equivalent to `CFRelease(provider)', but doesn't crash (as CFRelease
    does) if `provider' is NULL. */
 
-CG_EXTERN void CGDataProviderRelease(CGDataProviderRef __nullable provider)
+CG_EXTERN void CGDataProviderRelease(CGDataProviderRef cg_nullable provider)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return a copy of the data specified by provider. Returns NULL if a
@@ -177,7 +177,7 @@
    underlying data is too large to fit in memory). */
 
 CG_EXTERN CFDataRef __nullable CGDataProviderCopyData(
-    CGDataProviderRef __nullable provider)
+    CGDataProviderRef cg_nullable provider)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 CF_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGFont.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGFont.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGFont.h	2016-02-20 00:02:13.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGFont.h	2016-05-26 06:29:44.000000000 +0200
@@ -62,15 +62,15 @@
    should be a pointer to an ATSFontRef. */
 
 CG_EXTERN CGFontRef __nullable CGFontCreateWithPlatformFont(
-    void * __nullable platformFontReference)
+    void * cg_nullable platformFontReference)
     CG_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_6,
                                 __IPHONE_NA, __IPHONE_NA);
 
 /* Return the font defined by the data provided by `provider', or NULL if
    the font can't be created. */
 
-CG_EXTERN CGFontRef __nullable CGFontCreateWithDataProvider(
-    CGDataProviderRef __nullable provider)
+CG_EXTERN CGFontRef cg_nullable CGFontCreateWithDataProvider(
+    CGDataProviderRef cg_nullable provider)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Return the font identified by `name', corresponding to the font's
@@ -78,7 +78,7 @@
    created. */
 
 CG_EXTERN CGFontRef __nullable CGFontCreateWithFontName(
-    CFStringRef __nullable name)
+    CFStringRef cg_nullable name)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Return a font based on `font' with the variation specification dictionary
@@ -90,93 +90,93 @@
    then the current value from `font' is used. */
 
 CG_EXTERN CGFontRef __nullable CGFontCreateCopyWithVariations(
-    CGFontRef __nullable font, CFDictionaryRef __nullable variations)
+    CGFontRef cg_nullable font, CFDictionaryRef __nullable variations)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Equivalent to `CFRetain(font)', except it doesn't crash (as CFRetain
    does) if `font' is NULL. */
 
-CG_EXTERN CGFontRef __nullable CGFontRetain(CGFontRef __nullable font)
+CG_EXTERN CGFontRef cg_nullable CGFontRetain(CGFontRef cg_nullable font)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Equivalent to `CFRelease(font)', except it doesn't crash (as CFRelease
    does) if `font' is NULL. */
 
-CG_EXTERN void CGFontRelease(CGFontRef __nullable font)
+CG_EXTERN void CGFontRelease(CGFontRef cg_nullable font)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the number of glyphs in `font'. */
 
-CG_EXTERN size_t CGFontGetNumberOfGlyphs(CGFontRef __nullable font)
+CG_EXTERN size_t CGFontGetNumberOfGlyphs(CGFontRef cg_nullable font)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the glyph space units/em for `font'. */
 
-CG_EXTERN int CGFontGetUnitsPerEm(CGFontRef __nullable font)
+CG_EXTERN int CGFontGetUnitsPerEm(CGFontRef cg_nullable font)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the PostScript name of `font'. */
 
-CG_EXTERN CFStringRef __nullable CGFontCopyPostScriptName(CGFontRef __nullable font)
+CG_EXTERN CFStringRef __nullable CGFontCopyPostScriptName(CGFontRef cg_nullable font)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Return the "full name" of `font'. */
 
-CG_EXTERN CFStringRef __nullable CGFontCopyFullName(CGFontRef __nullable font)
+CG_EXTERN CFStringRef __nullable CGFontCopyFullName(CGFontRef cg_nullable font)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Return the ascent of `font'. The ascent is the maximum distance above the
    baseline of glyphs in a font. The value is specified in glyph space
    units. */
 
-CG_EXTERN int CGFontGetAscent(CGFontRef __nullable font)
+CG_EXTERN int CGFontGetAscent(CGFontRef cg_nullable font)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Return the descent of `font'. The descent is the maximum distance below
    the baseline of glyphs in a font. The value is specified in glyph space
    units. */
 
-CG_EXTERN int CGFontGetDescent(CGFontRef __nullable font)
+CG_EXTERN int CGFontGetDescent(CGFontRef cg_nullable font)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Return the leading of `font'. The leading is the spacing between
    consecutive lines of text in a font. The value is specified in glyph
    space units. */
 
-CG_EXTERN int CGFontGetLeading(CGFontRef __nullable font)
+CG_EXTERN int CGFontGetLeading(CGFontRef cg_nullable font)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Return the cap height of `font'. The cap height is the distance above the
    baseline of the top of flat capital letters of glyphs in a font. The
    value is specified in glyph space units. */
 
-CG_EXTERN int CGFontGetCapHeight(CGFontRef __nullable font)
+CG_EXTERN int CGFontGetCapHeight(CGFontRef cg_nullable font)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Return the x-height of `font'. The x-height is the distance above the
    baseline of the top of flat, non-ascending lowercase letters (such as
    "x") of glyphs in a font. The value is specified in glyph space units. */
 
-CG_EXTERN int CGFontGetXHeight(CGFontRef __nullable font)
+CG_EXTERN int CGFontGetXHeight(CGFontRef cg_nullable font)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Return the font bounding box of `font'. The font bounding box is the
    union of all of the bounding boxes for all the glyphs in a font. The
    value is specified in glyph space units. */
 
-CG_EXTERN CGRect CGFontGetFontBBox(CGFontRef __nullable font)
+CG_EXTERN CGRect CGFontGetFontBBox(CGFontRef cg_nullable font)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Return the italic angle of `font', measured in degrees counter-clockwise
    from the vertical. */
 
-CG_EXTERN CGFloat CGFontGetItalicAngle(CGFontRef __nullable font)
+CG_EXTERN CGFloat CGFontGetItalicAngle(CGFontRef cg_nullable font)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Return the thickness of the dominant vertical stems of glyphs in `font'.
    The value is specified in glyph space units. */
 
-CG_EXTERN CGFloat CGFontGetStemV(CGFontRef __nullable font)
+CG_EXTERN CGFloat CGFontGetStemV(CGFontRef cg_nullable font)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Return an array of the variation axis dictionaries for `font'. Each
@@ -184,7 +184,7 @@
    listed below. This function returns NULL if `font' doesn't support
    variations. */
 
-CG_EXTERN CFArrayRef __nullable CGFontCopyVariationAxes(CGFontRef __nullable font)
+CG_EXTERN CFArrayRef __nullable CGFontCopyVariationAxes(CGFontRef cg_nullable font)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Return the variation specification dictionary from `font'. This
@@ -194,7 +194,7 @@
    CFNumberRef. This function returns NULL if `font' doesn't support
    variations. */
 
-CG_EXTERN CFDictionaryRef __nullable CGFontCopyVariations(CGFontRef __nullable font)
+CG_EXTERN CFDictionaryRef __nullable CGFontCopyVariations(CGFontRef cg_nullable font)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Get the advance of each glyph in `glyphs', an array of `count' glyphs,
@@ -202,7 +202,7 @@
    `count' integers. The advances are specified in glyph space. Returns
    false if advances can't be retrieved for any reason; true otherwise. */
 
-CG_EXTERN bool CGFontGetGlyphAdvances(CGFontRef __nullable font,
+CG_EXTERN bool CGFontGetGlyphAdvances(CGFontRef cg_nullable font,
     const CGGlyph *  glyphs, size_t count, int *  advances)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
@@ -212,7 +212,7 @@
    Returns false if bounding boxes can't be retrieved for any reason; true
    otherwise. */
 
-CG_EXTERN bool CGFontGetGlyphBBoxes(CGFontRef __nullable font,
+CG_EXTERN bool CGFontGetGlyphBBoxes(CGFontRef cg_nullable font,
     const CGGlyph *  glyphs, size_t count, CGRect *  bboxes)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
@@ -220,20 +220,20 @@
    in the font, return 0. */
 
 CG_EXTERN CGGlyph CGFontGetGlyphWithGlyphName(
-    CGFontRef __nullable font, CFStringRef __nullable name)
+    CGFontRef cg_nullable font, CFStringRef cg_nullable name)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Return the glyph name of `glyph' in `font', or NULL if `glyph' does not
    appear in `font'. */
 
 CG_EXTERN CFStringRef __nullable CGFontCopyGlyphNameForGlyph(
-    CGFontRef __nullable font, CGGlyph glyph)
+    CGFontRef cg_nullable font, CGGlyph glyph)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Return true if a subset in the PostScript format `format' can be created
    for `font'; false otherwise. */
 
-CG_EXTERN bool CGFontCanCreatePostScriptSubset(CGFontRef __nullable font,
+CG_EXTERN bool CGFontCanCreatePostScriptSubset(CGFontRef cg_nullable font,
     CGFontPostScriptFormat format)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
@@ -243,7 +243,7 @@
    encoding for the subset. */
 
 CG_EXTERN CFDataRef __nullable CGFontCreatePostScriptSubset(
-    CGFontRef __nullable font, CFStringRef __nullable subsetName,
+    CGFontRef cg_nullable font, CFStringRef cg_nullable subsetName,
     CGFontPostScriptFormat format, const CGGlyph * __nullable glyphs,
     size_t count, const CGGlyph encoding[256])
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
@@ -252,21 +252,21 @@
    `encoding'. */
 
 CG_EXTERN CFDataRef __nullable CGFontCreatePostScriptEncoding(
-    CGFontRef __nullable font, const CGGlyph encoding[256])
+    CGFontRef cg_nullable font, const CGGlyph encoding[256])
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Return an array of font table tags in `font'. Each entry in the array is
    a four-byte value representing a single TrueType or OpenType font table
    tag. */
 
-CG_EXTERN CFArrayRef __nullable CGFontCopyTableTags(CGFontRef __nullable font)
+CG_EXTERN CFArrayRef __nullable CGFontCopyTableTags(CGFontRef cg_nullable font)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Return the table in `font' corresponding to `tag', or NULL if no such
    table exists. */
 
 CG_EXTERN CFDataRef __nullable CGFontCopyTableForTag(
-    CGFontRef __nullable font, uint32_t tag)
+    CGFontRef cg_nullable font, uint32_t tag)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /*** Keys for the font variation axis dictionary. ***/
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGFunction.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGFunction.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGFunction.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGFunction.h	2016-06-03 04:58:47.000000000 +0200
@@ -81,20 +81,20 @@
 CG_EXTERN CGFunctionRef __nullable CGFunctionCreate(void * __nullable info,
     size_t domainDimension, const CGFloat *__nullable domain,
     size_t rangeDimension, const CGFloat * __nullable range,
-    const CGFunctionCallbacks * __nullable callbacks)
+    const CGFunctionCallbacks * cg_nullable callbacks)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Equivalent to `CFRetain(function)', except it doesn't crash (as CFRetain
    does) if `function' is NULL. */
 
-CG_EXTERN CGFunctionRef __nullable CGFunctionRetain(
-    CGFunctionRef __nullable function)
+CG_EXTERN CGFunctionRef cg_nullable CGFunctionRetain(
+    CGFunctionRef cg_nullable function)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Equivalent to `CFRelease(function)', except it doesn't crash (as
    CFRelease does) if `function' is NULL. */
 
-CG_EXTERN void CGFunctionRelease(CGFunctionRef __nullable function)
+CG_EXTERN void CGFunctionRelease(CGFunctionRef cg_nullable function)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 CF_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGGeometry.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGGeometry.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGGeometry.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGGeometry.h	2016-06-03 04:58:47.000000000 +0200
@@ -245,7 +245,7 @@
    `point'. Returns true on success; false otherwise. */
 
 CG_EXTERN bool CGPointMakeWithDictionaryRepresentation(
-    CFDictionaryRef __nullable dict, CGPoint * __nullable point)
+    CFDictionaryRef cg_nullable dict, CGPoint * cg_nullable point)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Return a dictionary representation of `size'. */
@@ -258,7 +258,7 @@
    `size'. Returns true on success; false otherwise. */
 
 CG_EXTERN bool CGSizeMakeWithDictionaryRepresentation(
-    CFDictionaryRef __nullable dict, CGSize * __nullable size)
+    CFDictionaryRef cg_nullable dict, CGSize * cg_nullable size)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Return a dictionary representation of `rect'. */
@@ -271,7 +271,7 @@
    `rect'. Returns true on success; false otherwise. */
 
 CG_EXTERN bool CGRectMakeWithDictionaryRepresentation(
-    CFDictionaryRef __nullable dict, CGRect * __nullable rect)
+    CFDictionaryRef cg_nullable dict, CGRect * cg_nullable rect)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /*** Definitions of inline functions. ***/
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGGradient.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGGradient.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGGradient.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGGradient.h	2016-05-26 06:16:33.000000000 +0200
@@ -54,7 +54,7 @@
    for those values. */
 
 CG_EXTERN CGGradientRef __nullable CGGradientCreateWithColorComponents(
-    CGColorSpaceRef __nullable space, const CGFloat * __nullable components,
+    CGColorSpaceRef cg_nullable space, const CGFloat * cg_nullable components,
     const CGFloat * __nullable locations, size_t count)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
@@ -75,21 +75,21 @@
    values. */
 
 CG_EXTERN CGGradientRef __nullable CGGradientCreateWithColors(
-    CGColorSpaceRef __nullable space, CFArrayRef __nullable colors,
-    const CGFloat * __nullable locations)
+    CGColorSpaceRef cg_nullable space, CFArrayRef cg_nullable colors,
+    const CGFloat * cg_nullable locations)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Equivalent to `CFRetain' except that it doesn't crash (as `CFRetain'
    does) if `gradient' is NULL. */
 
-CG_EXTERN CGGradientRef __nullable CGGradientRetain(
-    CGGradientRef __nullable gradient)
+CG_EXTERN CGGradientRef cg_nullable CGGradientRetain(
+    CGGradientRef cg_nullable gradient)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Equivalent to `CFRelease' except that it doesn't crash (as `CFRelease'
    does) if `gradient' is NULL. */
 
-CG_EXTERN void CGGradientRelease(CGGradientRef __nullable gradient)
+CG_EXTERN void CGGradientRelease(CGGradientRef cg_nullable gradient)
     CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 CF_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGImage.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGImage.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGImage.h	2016-02-24 22:44:01.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGImage.h	2016-06-03 04:58:47.000000000 +0200
@@ -61,8 +61,8 @@
 
 CG_EXTERN CGImageRef __nullable CGImageCreate(size_t width, size_t height,
     size_t bitsPerComponent, size_t bitsPerPixel, size_t bytesPerRow,
-    CGColorSpaceRef __nullable space, CGBitmapInfo bitmapInfo,
-    CGDataProviderRef __nullable provider,
+    CGColorSpaceRef cg_nullable space, CGBitmapInfo bitmapInfo,
+    CGDataProviderRef cg_nullable provider,
     const CGFloat * __nullable decode, bool shouldInterpolate,
     CGColorRenderingIntent intent)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
@@ -71,20 +71,20 @@
 
 CG_EXTERN CGImageRef __nullable CGImageMaskCreate(size_t width, size_t height,
     size_t bitsPerComponent, size_t bitsPerPixel, size_t bytesPerRow,
-    CGDataProviderRef __nullable provider, const CGFloat * __nullable decode,
+    CGDataProviderRef cg_nullable provider, const CGFloat * __nullable decode,
     bool shouldInterpolate)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return a copy of `image'. Only the image structure itself is copied; the
    underlying data is not. */
 
-CG_EXTERN CGImageRef __nullable CGImageCreateCopy(CGImageRef __nullable image)
+CG_EXTERN CGImageRef __nullable CGImageCreateCopy(CGImageRef cg_nullable image)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Create an image from `source', a data provider of JPEG-encoded data. */
 
 CG_EXTERN CGImageRef __nullable CGImageCreateWithJPEGDataProvider(
-    CGDataProviderRef __nullable source, const CGFloat * __nullable decode,
+    CGDataProviderRef cg_nullable source, const CGFloat * __nullable decode,
     bool shouldInterpolate,
     CGColorRenderingIntent intent)
     CG_AVAILABLE_STARTING(__MAC_10_1, __IPHONE_2_0);
@@ -92,7 +92,7 @@
 /* Create an image using `source', a data provider for PNG-encoded data. */
 
 CG_EXTERN CGImageRef __nullable CGImageCreateWithPNGDataProvider(
-    CGDataProviderRef __nullable source, const CGFloat * __nullable decode,
+    CGDataProviderRef cg_nullable source, const CGFloat * __nullable decode,
     bool shouldInterpolate,
     CGColorRenderingIntent intent)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
@@ -119,7 +119,7 @@
    release the original image after calling this function. */
 
 CG_EXTERN CGImageRef __nullable CGImageCreateWithImageInRect(
-    CGImageRef __nullable image, CGRect rect)
+    CGImageRef cg_nullable image, CGRect rect)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Create a new image from `image' masked by `mask', which may be an image
@@ -149,7 +149,7 @@
    itself be masked by an image mask or a masking color. */
 
 CG_EXTERN CGImageRef __nullable CGImageCreateWithMask(
-    CGImageRef __nullable image, CGImageRef __nullable mask)
+    CGImageRef cg_nullable image, CGImageRef cg_nullable mask)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Create a new image from `image' masked by `components', an array of 2N
@@ -169,7 +169,7 @@
    an image mask or masking color associated with it. */
 
 CG_EXTERN CGImageRef __nullable CGImageCreateWithMaskingColors(
-    CGImageRef __nullable image, const CGFloat * __nullable components)
+    CGImageRef cg_nullable image, const CGFloat * cg_nullable components)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Create a copy of `image', replacing the image's color space with `space'.
@@ -178,88 +178,88 @@
    of `image'. */
 
 CG_EXTERN CGImageRef __nullable CGImageCreateCopyWithColorSpace(
-    CGImageRef __nullable image, CGColorSpaceRef __nullable space)
+    CGImageRef cg_nullable image, CGColorSpaceRef cg_nullable space)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Equivalent to `CFRetain(image)'. */
 
-CG_EXTERN CGImageRef __nullable CGImageRetain(CGImageRef __nullable image)
+CG_EXTERN CGImageRef cg_nullable CGImageRetain(CGImageRef cg_nullable image)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Equivalent to `CFRelease(image)'. */
 
-CG_EXTERN void CGImageRelease(CGImageRef __nullable image)
+CG_EXTERN void CGImageRelease(CGImageRef cg_nullable image)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return true if `image' is an image mask, false otherwise. */
 
-CG_EXTERN bool CGImageIsMask(CGImageRef __nullable image)
+CG_EXTERN bool CGImageIsMask(CGImageRef cg_nullable image)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the width of `image'. */
 
-CG_EXTERN size_t CGImageGetWidth(CGImageRef __nullable image)
+CG_EXTERN size_t CGImageGetWidth(CGImageRef cg_nullable image)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the height of `image'. */
 
-CG_EXTERN size_t CGImageGetHeight(CGImageRef __nullable image)
+CG_EXTERN size_t CGImageGetHeight(CGImageRef cg_nullable image)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the number of bits/component of `image'. */
 
-CG_EXTERN size_t CGImageGetBitsPerComponent(CGImageRef __nullable image)
+CG_EXTERN size_t CGImageGetBitsPerComponent(CGImageRef cg_nullable image)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the number of bits/pixel of `image'. */
 
-CG_EXTERN size_t CGImageGetBitsPerPixel(CGImageRef __nullable image)
+CG_EXTERN size_t CGImageGetBitsPerPixel(CGImageRef cg_nullable image)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the number of bytes/row of `image'. */
 
-CG_EXTERN size_t CGImageGetBytesPerRow(CGImageRef __nullable image)
+CG_EXTERN size_t CGImageGetBytesPerRow(CGImageRef cg_nullable image)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the color space of `image', or NULL if `image' is an image
    mask. */
 
-CG_EXTERN CGColorSpaceRef __nullable CGImageGetColorSpace(CGImageRef __nullable image)
+CG_EXTERN CGColorSpaceRef __nullable CGImageGetColorSpace(CGImageRef cg_nullable image)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the alpha info of `image'. */
 
-CG_EXTERN CGImageAlphaInfo CGImageGetAlphaInfo(CGImageRef __nullable image)
+CG_EXTERN CGImageAlphaInfo CGImageGetAlphaInfo(CGImageRef cg_nullable image)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the data provider of `image'. */
 
-CG_EXTERN CGDataProviderRef __nullable CGImageGetDataProvider(CGImageRef __nullable image)
+CG_EXTERN CGDataProviderRef __nullable CGImageGetDataProvider(CGImageRef cg_nullable image)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the decode array of `image'. */
 
-CG_EXTERN const CGFloat * __nullable CGImageGetDecode(CGImageRef __nullable image)
+CG_EXTERN const CGFloat * __nullable CGImageGetDecode(CGImageRef cg_nullable image)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the interpolation parameter of `image'. */
 
-CG_EXTERN bool CGImageGetShouldInterpolate(CGImageRef __nullable image)
+CG_EXTERN bool CGImageGetShouldInterpolate(CGImageRef cg_nullable image)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the rendering intent of `image'. */
 
-CG_EXTERN CGColorRenderingIntent CGImageGetRenderingIntent(__nullable CGImageRef image)
+CG_EXTERN CGColorRenderingIntent CGImageGetRenderingIntent(cg_nullable CGImageRef image)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the bitmap info of `image'. */
 
-CG_EXTERN CGBitmapInfo CGImageGetBitmapInfo(CGImageRef __nullable image)
+CG_EXTERN CGBitmapInfo CGImageGetBitmapInfo(CGImageRef cg_nullable image)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Return the UTType of `image'. */
 
-CG_EXTERN CFStringRef  __nullable CGImageGetUTType(__nullable CGImageRef image)
+CG_EXTERN CFStringRef  __nullable CGImageGetUTType(cg_nullable CGImageRef image)
     CG_AVAILABLE_STARTING(__MAC_10_11, __IPHONE_9_0);
 
 CF_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGLayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGLayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGLayer.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGLayer.h	2016-06-03 04:58:47.000000000 +0200
@@ -24,46 +24,46 @@
    expansion. */
 
 CG_EXTERN CGLayerRef __nullable CGLayerCreateWithContext(
-    CGContextRef __nullable context,
+    CGContextRef cg_nullable context,
     CGSize size, CFDictionaryRef __nullable auxiliaryInfo)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Equivalent to `CFRetain(layer)', except it doesn't crash (as CFRetain
    does) if `layer' is NULL. */
 
-CG_EXTERN CGLayerRef __nullable CGLayerRetain(CGLayerRef __nullable layer)
+CG_EXTERN CGLayerRef cg_nullable CGLayerRetain(CGLayerRef cg_nullable layer)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Equivalent to `CFRelease(layer)', except it doesn't crash (as CFRelease
    does) if `layer' is NULL. */
 
-CG_EXTERN void CGLayerRelease(CGLayerRef __nullable layer)
+CG_EXTERN void CGLayerRelease(CGLayerRef cg_nullable layer)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Return the size of the layer `layer'. CGSizeZero if invalid `layer'. */
 
-CG_EXTERN CGSize CGLayerGetSize(CGLayerRef __nullable layer)
+CG_EXTERN CGSize CGLayerGetSize(CGLayerRef cg_nullable layer)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Return the context of `layer'. */
 
-CG_EXTERN CGContextRef __nullable CGLayerGetContext(CGLayerRef __nullable layer)
+CG_EXTERN CGContextRef __nullable CGLayerGetContext(CGLayerRef cg_nullable layer)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Draw the contents of `layer' into `rect' of `context'. The contents are
    scaled, if necessary, to fit into `rect'; the rectangle `rect' is in user
    space. */
 
-CG_EXTERN void CGContextDrawLayerInRect(CGContextRef __nullable context,
-    CGRect rect, CGLayerRef __nullable layer)
+CG_EXTERN void CGContextDrawLayerInRect(CGContextRef cg_nullable context,
+    CGRect rect, CGLayerRef cg_nullable layer)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Draw the contents of `layer' at `point' in `context'. This is equivalent
    to calling "CGContextDrawLayerInRect" with a rectangle having origin at
    `point' and size equal to the size of `layer'. */
 
-CG_EXTERN void CGContextDrawLayerAtPoint(CGContextRef __nullable context,
-    CGPoint point, CGLayerRef __nullable layer)
+CG_EXTERN void CGContextDrawLayerAtPoint(CGContextRef cg_nullable context,
+    CGPoint point, CGLayerRef cg_nullable layer)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Return the CFTypeID for CGLayerRefs. */
@@ -75,4 +75,4 @@
 
 CF_IMPLICIT_BRIDGING_DISABLED
 
-#endif	/* CGLAYER_H_ */
+#endif  /* CGLAYER_H_ */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFArray.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFArray.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFArray.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFArray.h	2016-06-03 04:58:47.000000000 +0200
@@ -22,33 +22,33 @@
 
 #/* Return the number of items in `array'. */
 
-CG_EXTERN size_t CGPDFArrayGetCount(CGPDFArrayRef __nullable array)
+CG_EXTERN size_t CGPDFArrayGetCount(CGPDFArrayRef cg_nullable array)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Look up the object at `index' in `array' and return the result in
    `value'. Return true on success; false otherwise. */
 
-CG_EXTERN bool CGPDFArrayGetObject(CGPDFArrayRef __nullable array, size_t index,
+CG_EXTERN bool CGPDFArrayGetObject(CGPDFArrayRef cg_nullable array, size_t index,
     CGPDFObjectRef __nullable * __nullable value)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Look up the object at `index' in `array' and, if it's a null, return
    true; otherwise, return false. */
 
-CG_EXTERN bool CGPDFArrayGetNull(CGPDFArrayRef __nullable array, size_t index)
+CG_EXTERN bool CGPDFArrayGetNull(CGPDFArrayRef cg_nullable array, size_t index)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Look up the object at `index' in `array' and, if it's a boolean, return
    the result in `value'. Return true on success; false otherwise. */
 
-CG_EXTERN bool CGPDFArrayGetBoolean(CGPDFArrayRef __nullable array,
+CG_EXTERN bool CGPDFArrayGetBoolean(CGPDFArrayRef cg_nullable array,
     size_t index, CGPDFBoolean * __nullable value)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Look up the object at `index' in `array' and, if it's an integer, return
    the result in `value'. Return true on success; false otherwise. */
 
-CG_EXTERN bool CGPDFArrayGetInteger(CGPDFArrayRef __nullable array,
+CG_EXTERN bool CGPDFArrayGetInteger(CGPDFArrayRef cg_nullable array,
     size_t index, CGPDFInteger * __nullable value)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
@@ -56,42 +56,42 @@
    integer), return the result in `value'. Return true on success; false
    otherwise. */
 
-CG_EXTERN bool CGPDFArrayGetNumber(CGPDFArrayRef __nullable array,
+CG_EXTERN bool CGPDFArrayGetNumber(CGPDFArrayRef cg_nullable array,
     size_t index, CGPDFReal * __nullable value)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Look up the object at `index' in `array' and, if it's a name, return the
    result in `value'. Return true on success; false otherwise. */
 
-CG_EXTERN bool CGPDFArrayGetName(CGPDFArrayRef __nullable array,
+CG_EXTERN bool CGPDFArrayGetName(CGPDFArrayRef cg_nullable array,
     size_t index, const char * __nullable *  __nullable value)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Look up the object at `index' in `array' and, if it's a string, return
    the result in `value'. Return true on success; false otherwise. */
 
-CG_EXTERN bool CGPDFArrayGetString(CGPDFArrayRef __nullable array,
+CG_EXTERN bool CGPDFArrayGetString(CGPDFArrayRef cg_nullable array,
     size_t index, CGPDFStringRef __nullable * __nullable value)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Look up the object at `index' in `array' and, if it's an array, return it
    in `value'. Return true on success; false otherwise. */
 
-CG_EXTERN bool CGPDFArrayGetArray(CGPDFArrayRef __nullable array,
+CG_EXTERN bool CGPDFArrayGetArray(CGPDFArrayRef cg_nullable array,
     size_t index, CGPDFArrayRef __nullable * __nullable value)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Look up the object at `index' in `array' and, if it's a dictionary,
    return it in `value'. Return true on success; false otherwise. */
 
-CG_EXTERN bool CGPDFArrayGetDictionary(CGPDFArrayRef __nullable array,
+CG_EXTERN bool CGPDFArrayGetDictionary(CGPDFArrayRef cg_nullable array,
     size_t index, CGPDFDictionaryRef __nullable * __nullable value)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Look up the object at `index' in `array' and, if it's a stream, return it
    in `value'. Return true on success; false otherwise. */
 
-CG_EXTERN bool CGPDFArrayGetStream(CGPDFArrayRef __nullable array,
+CG_EXTERN bool CGPDFArrayGetStream(CGPDFArrayRef cg_nullable array,
     size_t index, CGPDFStreamRef __nullable * __nullable value)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFContentStream.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFContentStream.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFContentStream.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFContentStream.h	2016-06-03 04:58:47.000000000 +0200
@@ -11,6 +11,8 @@
 
 CF_IMPLICIT_BRIDGING_ENABLED
 
+CF_ASSUME_NONNULL_BEGIN
+
 /* Create a content stream from `page'. */
 
 CG_EXTERN CGPDFContentStreamRef CGPDFContentStreamCreateWithPage(
@@ -20,7 +22,7 @@
 
 CG_EXTERN CGPDFContentStreamRef CGPDFContentStreamCreateWithStream(
   CGPDFStreamRef stream, CGPDFDictionaryRef streamResources,
-  CGPDFContentStreamRef parent)
+  CGPDFContentStreamRef cg_nullable parent)
   CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Increment the retain count of `cs'. */
@@ -36,16 +38,18 @@
 /* Return the array of CGPDFStreamRefs comprising the entire content stream
    of `cs'. */
 
-CG_EXTERN CFArrayRef CGPDFContentStreamGetStreams(CGPDFContentStreamRef cs)
+CG_EXTERN CFArrayRef __nullable CGPDFContentStreamGetStreams(CGPDFContentStreamRef cs)
   CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Return the resource named `name' in category `category' of the resource
    dictionaries of `cs'. */
 
-CG_EXTERN CGPDFObjectRef CGPDFContentStreamGetResource(
+CG_EXTERN CGPDFObjectRef __nullable CGPDFContentStreamGetResource(
   CGPDFContentStreamRef cs, const char *category, const char *name)
   CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
+CF_ASSUME_NONNULL_END
+
 CF_IMPLICIT_BRIDGING_DISABLED
 
 #endif /* CGPDFCONTENTSTREAM_H_ */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFContext.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFContext.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFContext.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFContext.h	2016-06-02 06:59:43.000000000 +0200
@@ -27,7 +27,7 @@
    value overrides the value of `kCGPDFContextMediaBox' if specified in the
    `auxiliaryInfo' dictionary. */
 
-CG_EXTERN CGContextRef __nullable CGPDFContextCreate(CGDataConsumerRef __nullable consumer,
+CG_EXTERN CGContextRef __nullable CGPDFContextCreate(CGDataConsumerRef cg_nullable consumer,
   const CGRect *__nullable mediaBox, CFDictionaryRef __nullable auxiliaryInfo)
   CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
@@ -35,7 +35,7 @@
    same manner as the above function, except that the output data will be
    written to `url'. */
 
-CG_EXTERN CGContextRef __nullable CGPDFContextCreateWithURL(CFURLRef __nullable url,
+CG_EXTERN CGContextRef __nullable CGPDFContextCreateWithURL(CFURLRef cg_nullable url,
   const CGRect * __nullable mediaBox, CFDictionaryRef __nullable auxiliaryInfo)
   CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
@@ -44,18 +44,18 @@
    additional data will be written to the context's destionation after
    closing. */
 
-CG_EXTERN void CGPDFContextClose(CGContextRef __nullable context)
+CG_EXTERN void CGPDFContextClose(CGContextRef cg_nullable context)
   CG_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_2_0);
 
 /* Begin a new page in the PDF context `context'. */
 
-CG_EXTERN void CGPDFContextBeginPage(CGContextRef __nullable context,
+CG_EXTERN void CGPDFContextBeginPage(CGContextRef cg_nullable context,
   CFDictionaryRef __nullable pageInfo)
   CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* End the current page in the PDF context `context'. */
 
-CG_EXTERN void CGPDFContextEndPage(CGContextRef __nullable context)
+CG_EXTERN void CGPDFContextEndPage(CGContextRef cg_nullable context)
   CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Add the metadata stream specified by `metadata' to the document catalog
@@ -65,26 +65,26 @@
    described in section 10.2.2, "Metadata Streams", of the PDF 1.7
    specification. */
 
-CG_EXTERN void CGPDFContextAddDocumentMetadata(CGContextRef __nullable context,
+CG_EXTERN void CGPDFContextAddDocumentMetadata(CGContextRef cg_nullable context,
   CFDataRef __nullable metadata) CG_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_4_0);
 
 /* Set the URL associated with `rect' to `url' in the PDF context
    `context'. */
 
-CG_EXTERN void CGPDFContextSetURLForRect(CGContextRef __nullable context, CFURLRef  url,
+CG_EXTERN void CGPDFContextSetURLForRect(CGContextRef cg_nullable context, CFURLRef  url,
   CGRect rect) CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Create a PDF destination named `name' at `point' in the current page of
    the PDF context `context'. */
 
-CG_EXTERN void CGPDFContextAddDestinationAtPoint(CGContextRef __nullable context,
+CG_EXTERN void CGPDFContextAddDestinationAtPoint(CGContextRef cg_nullable context,
   CFStringRef  name, CGPoint point)
   CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Specify a destination named `name' to jump to when clicking in `rect' of
    the current page of the PDF context `context'. */
 
-CG_EXTERN void CGPDFContextSetDestinationForRect(CGContextRef __nullable context,
+CG_EXTERN void CGPDFContextSetDestinationForRect(CGContextRef cg_nullable context,
   CFStringRef  name, CGRect rect)
   CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFDictionary.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFDictionary.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFDictionary.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFDictionary.h	2016-06-03 04:52:14.000000000 +0200
@@ -22,13 +22,13 @@
 
 /* Return the number of entries in `dictionary'. */
 
-CG_EXTERN size_t CGPDFDictionaryGetCount(CGPDFDictionaryRef __nullable dict)
+CG_EXTERN size_t CGPDFDictionaryGetCount(CGPDFDictionaryRef cg_nullable dict)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Look up the object associated with `key' in `dict' and return the result
    in `value'. Return true on success; false otherwise. */
 
-CG_EXTERN bool CGPDFDictionaryGetObject(CGPDFDictionaryRef __nullable dict,
+CG_EXTERN bool CGPDFDictionaryGetObject(CGPDFDictionaryRef cg_nullable dict,
     const char *  key, CGPDFObjectRef __nullable * __nullable value)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
@@ -36,7 +36,7 @@
    boolean, return the result in `value'. Return true on success; false
    otherwise. */
 
-CG_EXTERN bool CGPDFDictionaryGetBoolean(CGPDFDictionaryRef __nullable dict,
+CG_EXTERN bool CGPDFDictionaryGetBoolean(CGPDFDictionaryRef cg_nullable dict,
     const char *  key, CGPDFBoolean * __nullable value)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
@@ -44,7 +44,7 @@
    integer, return the result in `value'. Return true on success; false
    otherwise. */
 
-CG_EXTERN bool CGPDFDictionaryGetInteger(CGPDFDictionaryRef __nullable dict,
+CG_EXTERN bool CGPDFDictionaryGetInteger(CGPDFDictionaryRef cg_nullable dict,
     const char *  key, CGPDFInteger * __nullable value)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
@@ -52,28 +52,28 @@
    (real or integer), return the result in `value'. Return true on success;
    false otherwise. */
 
-CG_EXTERN bool CGPDFDictionaryGetNumber(CGPDFDictionaryRef __nullable dict,
+CG_EXTERN bool CGPDFDictionaryGetNumber(CGPDFDictionaryRef cg_nullable dict,
     const char *  key, CGPDFReal * __nullable value)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Look up the object associated with `key' in `dict' and, if it's a name,
    return the result in `value'. Return true on success; false otherwise. */
 
-CG_EXTERN bool CGPDFDictionaryGetName(CGPDFDictionaryRef __nullable dict,
+CG_EXTERN bool CGPDFDictionaryGetName(CGPDFDictionaryRef cg_nullable dict,
     const char *  key, const char * __nullable * __nullable value)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Look up the object associated with `key' in `dict' and, if it's a string,
    return the result in `value'. Return true on success; false otherwise. */
 
-CG_EXTERN bool CGPDFDictionaryGetString(CGPDFDictionaryRef __nullable dict,
+CG_EXTERN bool CGPDFDictionaryGetString(CGPDFDictionaryRef cg_nullable dict,
     const char *  key, CGPDFStringRef __nullable * __nullable value)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Look up the object associated with `key' in `dict' and, if it's an array,
    return the result in `value'. Return true on success; false otherwise. */
 
-CG_EXTERN bool CGPDFDictionaryGetArray(CGPDFDictionaryRef __nullable dict,
+CG_EXTERN bool CGPDFDictionaryGetArray(CGPDFDictionaryRef cg_nullable dict,
     const char *  key, CGPDFArrayRef __nullable * __nullable value)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
@@ -81,14 +81,14 @@
    dictionary, return the result in `value'. Return true on success; false
    otherwise. */
 
-CG_EXTERN bool CGPDFDictionaryGetDictionary(CGPDFDictionaryRef __nullable dict,
+CG_EXTERN bool CGPDFDictionaryGetDictionary(CGPDFDictionaryRef cg_nullable dict,
     const char *  key, CGPDFDictionaryRef __nullable * __nullable value)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Look up the object associated with `key' in `dict' and, if it's a stream,
    return the result in `value'. Return true on success; false otherwise. */
 
-CG_EXTERN bool CGPDFDictionaryGetStream(CGPDFDictionaryRef __nullable dict,
+CG_EXTERN bool CGPDFDictionaryGetStream(CGPDFDictionaryRef cg_nullable dict,
     const char *  key, CGPDFStreamRef __nullable * __nullable value)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
@@ -103,8 +103,8 @@
    key/value pair. Passes the current key, the associated value, and `info'
    to `function'. */
 
-CG_EXTERN void CGPDFDictionaryApplyFunction(CGPDFDictionaryRef __nullable dict,
-    CGPDFDictionaryApplierFunction __nullable function, void * __nullable info)
+CG_EXTERN void CGPDFDictionaryApplyFunction(CGPDFDictionaryRef cg_nullable dict,
+    CGPDFDictionaryApplierFunction cg_nullable function, void * __nullable info)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 CF_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFDocument.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFDocument.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFDocument.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFDocument.h	2016-06-02 06:59:41.000000000 +0200
@@ -23,31 +23,31 @@
 /* Create a PDF document, using `provider' to obtain the document's data. */
 
 CG_EXTERN CGPDFDocumentRef __nullable CGPDFDocumentCreateWithProvider(
-    CGDataProviderRef __nullable provider)
+    CGDataProviderRef cg_nullable provider)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Create a PDF document from `url'. */
 
 CG_EXTERN CGPDFDocumentRef __nullable CGPDFDocumentCreateWithURL(
-    CFURLRef __nullable url)
+    CFURLRef cg_nullable url)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Equivalent to `CFRetain(document)', except it doesn't crash (as CFRetain
    does) if `document' is NULL. */
 
-CG_EXTERN CGPDFDocumentRef __nullable CGPDFDocumentRetain(
-    CGPDFDocumentRef __nullable document)
+CG_EXTERN CGPDFDocumentRef cg_nullable CGPDFDocumentRetain(
+    CGPDFDocumentRef cg_nullable document)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Equivalent to `CFRelease(document)', except it doesn't crash (as
    CFRelease does) if `document' is NULL. */
 
-CG_EXTERN void CGPDFDocumentRelease(CGPDFDocumentRef __nullable document)
+CG_EXTERN void CGPDFDocumentRelease(CGPDFDocumentRef cg_nullable document)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the major and minor version numbers of `document'. */
 
-CG_EXTERN void CGPDFDocumentGetVersion(CGPDFDocumentRef __nullable document,
+CG_EXTERN void CGPDFDocumentGetVersion(CGPDFDocumentRef cg_nullable document,
   int *  majorVersion, int *  minorVersion)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
@@ -56,7 +56,7 @@
    supplied before certain operations are enabled; different passwords may
    enable different operations. */
 
-CG_EXTERN bool CGPDFDocumentIsEncrypted(CGPDFDocumentRef __nullable document)
+CG_EXTERN bool CGPDFDocumentIsEncrypted(CGPDFDocumentRef cg_nullable document)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Use `password' to decrypt `document' and grant permission for certain
@@ -64,14 +64,14 @@
    otherwise. */
 
 CG_EXTERN bool CGPDFDocumentUnlockWithPassword(
-    CGPDFDocumentRef __nullable document, const char *  password)
+    CGPDFDocumentRef cg_nullable document, const char *  password)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Return true if `document' is unlocked; false otherwise. A document is
    unlocked if it isn't encrypted, or if it is encrypted and a valid
    password was specified with `CGPDFDocumentUnlockWithPassword'. */
 
-CG_EXTERN bool CGPDFDocumentIsUnlocked(CGPDFDocumentRef __nullable document)
+CG_EXTERN bool CGPDFDocumentIsUnlocked(CGPDFDocumentRef cg_nullable document)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Return true if `document' allows printing; false otherwise. Typically,
@@ -79,7 +79,7 @@
    document's current password doesn't grant permission to perform
    printing. */
 
-CG_EXTERN bool CGPDFDocumentAllowsPrinting(CGPDFDocumentRef __nullable document)
+CG_EXTERN bool CGPDFDocumentAllowsPrinting(CGPDFDocumentRef cg_nullable document)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Return true if `document' allows copying; false otherwise. Typically,
@@ -87,38 +87,38 @@
    document's current password doesn't grant permission to perform
    copying. */
 
-CG_EXTERN bool CGPDFDocumentAllowsCopying(CGPDFDocumentRef __nullable document)
+CG_EXTERN bool CGPDFDocumentAllowsCopying(CGPDFDocumentRef cg_nullable document)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Return the number of pages in `document'. */
 
 CG_EXTERN size_t CGPDFDocumentGetNumberOfPages(
-    CGPDFDocumentRef __nullable document)
+    CGPDFDocumentRef cg_nullable document)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Return the page corresponding to `pageNumber', or NULL if no such page
    exists in the document. Pages are numbered starting at 1. */
 
 CG_EXTERN CGPDFPageRef __nullable CGPDFDocumentGetPage(
-    CGPDFDocumentRef __nullable document, size_t pageNumber)
+    CGPDFDocumentRef cg_nullable document, size_t pageNumber)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Return the document catalog of `document'. */
 
 CG_EXTERN CGPDFDictionaryRef __nullable CGPDFDocumentGetCatalog(
-    CGPDFDocumentRef __nullable document)
+    CGPDFDocumentRef cg_nullable document)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Return the info dictionary of `document'. */
 
 CG_EXTERN CGPDFDictionaryRef __nullable CGPDFDocumentGetInfo(
-    CGPDFDocumentRef __nullable document)
+    CGPDFDocumentRef cg_nullable document)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Return the "file identifier" array of `document'. */
 
 CG_EXTERN CGPDFArrayRef __nullable CGPDFDocumentGetID(
-    CGPDFDocumentRef __nullable document)
+    CGPDFDocumentRef cg_nullable document)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Return the CFTypeID for CGPDFDocumentRefs. */
@@ -131,7 +131,7 @@
 /* DEPRECATED; return the media box of page number `page' in `document'.
    CGRectNull is returned if cannot find `page' in `document'. */
 
-CG_EXTERN CGRect CGPDFDocumentGetMediaBox(CGPDFDocumentRef __nullable document,
+CG_EXTERN CGRect CGPDFDocumentGetMediaBox(CGPDFDocumentRef cg_nullable document,
     int page)
     CG_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_5,
                                 __IPHONE_NA, __IPHONE_NA);
@@ -140,7 +140,7 @@
    CGRectNull is returned if cannot find `page' in `document'. */
 
 
-CG_EXTERN CGRect CGPDFDocumentGetCropBox(CGPDFDocumentRef __nullable document,
+CG_EXTERN CGRect CGPDFDocumentGetCropBox(CGPDFDocumentRef cg_nullable document,
     int page)
     CG_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_5,
                                 __IPHONE_NA, __IPHONE_NA);
@@ -148,7 +148,7 @@
 /* DEPRECATED; return the bleed box of page number `page' in `document'.
    CGRectNull is returned if cannot find `page' in `document'. */
 
-CG_EXTERN CGRect CGPDFDocumentGetBleedBox(CGPDFDocumentRef __nullable document,
+CG_EXTERN CGRect CGPDFDocumentGetBleedBox(CGPDFDocumentRef cg_nullable document,
     int page)
     CG_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_5,
                                 __IPHONE_NA, __IPHONE_NA);
@@ -156,7 +156,7 @@
 /* DEPRECATED; return the trim box of page number `page' in `document'.
    CGRectNull is returned if cannot find `page' in `document'. */
 
-CG_EXTERN CGRect CGPDFDocumentGetTrimBox(CGPDFDocumentRef __nullable document,
+CG_EXTERN CGRect CGPDFDocumentGetTrimBox(CGPDFDocumentRef cg_nullable document,
     int page)
     CG_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_5,
                                 __IPHONE_NA, __IPHONE_NA);
@@ -164,7 +164,7 @@
 /* DEPRECATED; return the art box of page number `page' in `document'.
   CGRectNull is returned if cannot find `page' in `document'. */
 
-CG_EXTERN CGRect CGPDFDocumentGetArtBox(CGPDFDocumentRef __nullable document,
+CG_EXTERN CGRect CGPDFDocumentGetArtBox(CGPDFDocumentRef cg_nullable document,
     int page)
     CG_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_5,
                                 __IPHONE_NA, __IPHONE_NA);
@@ -172,7 +172,7 @@
 /* DEPRECATED; return the rotation angle (in degrees) of page number `page'
    in `document'. 0 if if cannot find `page' in `document'.*/
 
-CG_EXTERN int CGPDFDocumentGetRotationAngle(CGPDFDocumentRef __nullable document,
+CG_EXTERN int CGPDFDocumentGetRotationAngle(CGPDFDocumentRef cg_nullable document,
     int page)
     CG_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_5,
                                 __IPHONE_NA, __IPHONE_NA);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFObject.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFObject.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFObject.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFObject.h	2016-06-03 04:58:47.000000000 +0200
@@ -28,7 +28,7 @@
 
 /* A type to hold any object. */
 
-typedef union CGPDFObject *CGPDFObjectRef;
+typedef struct CGPDFObject *CGPDFObjectRef;
 
 /* An identifier to describe an object's type. */
 
@@ -46,7 +46,7 @@
 
 /* Return the type of `object'. */
 
-CG_EXTERN CGPDFObjectType CGPDFObjectGetType(CGPDFObjectRef __nullable object)
+CG_EXTERN CGPDFObjectType CGPDFObjectGetType(CGPDFObjectRef cg_nullable object)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Get the value of `object'. If the type of `object' is equal to `type',
@@ -56,7 +56,7 @@
    `object' to floating point and copy the result to `value' (if it's
    non-NULL) and return true. Otherwise, return false. */
 
-CG_EXTERN bool CGPDFObjectGetValue(CGPDFObjectRef __nullable object,
+CG_EXTERN bool CGPDFObjectGetValue(CGPDFObjectRef cg_nullable object,
     CGPDFObjectType type, void * __nullable value)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFOperatorTable.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFOperatorTable.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFOperatorTable.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFOperatorTable.h	2016-06-03 04:58:47.000000000 +0200
@@ -27,25 +27,25 @@
 
 /* Increment the retain count of `table'. */
 
-CG_EXTERN CGPDFOperatorTableRef __nullable CGPDFOperatorTableRetain(
-    CGPDFOperatorTableRef __nullable table)
+CG_EXTERN CGPDFOperatorTableRef cg_nullable CGPDFOperatorTableRetain(
+    CGPDFOperatorTableRef cg_nullable table)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Decrement the retain count of `table'. */
 
 CG_EXTERN void CGPDFOperatorTableRelease(
-    CGPDFOperatorTableRef __nullable table)
+    CGPDFOperatorTableRef cg_nullable table)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Set the callback for the operator named `name' to `callback' */
 
 CG_EXTERN void CGPDFOperatorTableSetCallback(
-    CGPDFOperatorTableRef __nullable table,
-    const char * __nullable name, CGPDFOperatorCallback __nullable callback)
+    CGPDFOperatorTableRef cg_nullable table,
+    const char * cg_nullable name, CGPDFOperatorCallback cg_nullable callback)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 CF_ASSUME_NONNULL_END
 
 CF_IMPLICIT_BRIDGING_DISABLED
 
-#endif	/* CGPDFOPERATORTABLE_H_ */
+#endif  /* CGPDFOPERATORTABLE_H_ */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFPage.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFPage.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFPage.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFPage.h	2016-06-03 04:58:47.000000000 +0200
@@ -30,24 +30,24 @@
 /* Equivalent to `CFRetain(page)', except it doesn't crash (as CFRetain
    does) if `page' is NULL. */
 
-CG_EXTERN CGPDFPageRef __nullable CGPDFPageRetain(CGPDFPageRef __nullable page)
+CG_EXTERN CGPDFPageRef __nullable CGPDFPageRetain(CGPDFPageRef cg_nullable page)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Equivalent to `CFRelease(page)', except it doesn't crash (as CFRelease
    does) if `page' is NULL. */
 
-CG_EXTERN void CGPDFPageRelease(CGPDFPageRef __nullable page)
+CG_EXTERN void CGPDFPageRelease(CGPDFPageRef cg_nullable page)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Return the document of `page'. */
 
 CG_EXTERN CGPDFDocumentRef __nullable CGPDFPageGetDocument(
-    CGPDFPageRef __nullable page)
+    CGPDFPageRef cg_nullable page)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Return the page number of `page'. */
 
-CG_EXTERN size_t CGPDFPageGetPageNumber(CGPDFPageRef __nullable page)
+CG_EXTERN size_t CGPDFPageGetPageNumber(CGPDFPageRef cg_nullable page)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Return the rectangle associated with `box' in `page'. This is the value
@@ -55,14 +55,14 @@
    page's dictionary. Return CGRectNull if `page' is not a valid CGPDFPageRef
    or `box' is not a valid CGPDFBox. */
 
-CG_EXTERN CGRect CGPDFPageGetBoxRect(CGPDFPageRef __nullable page, CGPDFBox box)
+CG_EXTERN CGRect CGPDFPageGetBoxRect(CGPDFPageRef cg_nullable page, CGPDFBox box)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Return the rotation angle (in degrees) of `page'. This is the value of
    the /Rotate entry in the page's dictionary. Return 0 if `page' is not a valid
    CGPDFPageRef. */
 
-CG_EXTERN int CGPDFPageGetRotationAngle(CGPDFPageRef __nullable page)
+CG_EXTERN int CGPDFPageGetRotationAngle(CGPDFPageRef cg_nullable page)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Return a transform mapping the box specified by `box' to `rect' as
@@ -79,14 +79,14 @@
        restrictive dimension. */
 
 CG_EXTERN CGAffineTransform CGPDFPageGetDrawingTransform(
-    CGPDFPageRef __nullable page, CGPDFBox box, CGRect rect, int rotate,
+    CGPDFPageRef cg_nullable page, CGPDFBox box, CGRect rect, int rotate,
     bool preserveAspectRatio)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Return the dictionary of `page'. */
 
 CG_EXTERN CGPDFDictionaryRef __nullable CGPDFPageGetDictionary(
-    CGPDFPageRef __nullable page)
+    CGPDFPageRef cg_nullable page)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Return the CFTypeID for CGPDFPageRefs. */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFScanner.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFScanner.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFScanner.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFScanner.h	2016-06-02 06:59:43.000000000 +0200
@@ -27,20 +27,20 @@
 
 /* Retain `scanner'. */
 
-CG_EXTERN CGPDFScannerRef __nullable CGPDFScannerRetain(
-    CGPDFScannerRef __nullable scanner)
+CG_EXTERN CGPDFScannerRef cg_nullable CGPDFScannerRetain(
+    CGPDFScannerRef cg_nullable scanner)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Release `scanner'. */
 
-CG_EXTERN void CGPDFScannerRelease(CGPDFScannerRef __nullable scanner)
+CG_EXTERN void CGPDFScannerRelease(CGPDFScannerRef cg_nullable scanner)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Scan the content stream of `scanner'. Returns true if the entire stream
    was scanned successfully; false if scanning failed for some reason (for
    example, if the stream's data is corrupted). */
 
-CG_EXTERN bool CGPDFScannerScan(CGPDFScannerRef __nullable scanner)
+CG_EXTERN bool CGPDFScannerScan(CGPDFScannerRef cg_nullable scanner)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 /* Return the content stream associated with `scanner'. */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFStream.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFStream.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFStream.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFStream.h	2016-06-03 04:58:47.000000000 +0200
@@ -26,14 +26,14 @@
 /* Return the dictionary of `stream'. */
 
 CG_EXTERN CGPDFDictionaryRef __nullable CGPDFStreamGetDictionary(
-    CGPDFStreamRef __nullable stream)
+    CGPDFStreamRef cg_nullable stream)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Return the data of `stream'. */
 
 CG_EXTERN CFDataRef __nullable CGPDFStreamCopyData(
-    CGPDFStreamRef __nullable stream,
-    CGPDFDataFormat * __nullable format)
+    CGPDFStreamRef cg_nullable stream,
+    CGPDFDataFormat * cg_nullable format)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 CF_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFString.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFString.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFString.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPDFString.h	2016-06-03 04:58:47.000000000 +0200
@@ -21,13 +21,13 @@
 
 /* Return the length of `string'. */
 
-CG_EXTERN size_t CGPDFStringGetLength(CGPDFStringRef __nullable string)
+CG_EXTERN size_t CGPDFStringGetLength(CGPDFStringRef cg_nullable string)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Return a pointer to the bytes of `string'. */
 
 CG_EXTERN const unsigned char * __nullable CGPDFStringGetBytePtr(
-    CGPDFStringRef __nullable string)
+    CGPDFStringRef cg_nullable string)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Return a CFString representing `string' as a "text string". See Section
@@ -35,14 +35,14 @@
    more information. */
 
 CG_EXTERN CFStringRef __nullable CGPDFStringCopyTextString(
-    CGPDFStringRef __nullable string)
+    CGPDFStringRef cg_nullable string)
     CG_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /* Convert `string' to a CFDate. See Section 3.8.3 "Dates", PDF Reference:
    Adobe PDF version 1.6 (5th ed.) for more information. */
 
 CG_EXTERN CFDateRef __nullable CGPDFStringCopyDate(
-    CGPDFStringRef __nullable string)
+    CGPDFStringRef cg_nullable string)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
 CF_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPath.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPath.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPath.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPath.h	2016-05-26 06:29:44.000000000 +0200
@@ -48,25 +48,25 @@
 
 /* Create a copy of `path'. */
 
-CG_EXTERN CGPathRef __nullable CGPathCreateCopy(CGPathRef __nullable path)
+CG_EXTERN CGPathRef __nullable CGPathCreateCopy(CGPathRef cg_nullable path)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Create a copy of `path' transformed by `transform'. */
 
 CG_EXTERN CGPathRef __nullable CGPathCreateCopyByTransformingPath(
-    CGPathRef __nullable path, const CGAffineTransform * __nullable transform)
+    CGPathRef cg_nullable path, const CGAffineTransform * __nullable transform)
     CG_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_5_0);
 
 /* Create a mutable copy of `path'. */
 
 CG_EXTERN CGMutablePathRef __nullable CGPathCreateMutableCopy(
-    CGPathRef __nullable path)
+    CGPathRef cg_nullable path)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Create a mutable copy of `path' transformed by `transform'. */
 
 CG_EXTERN CGMutablePathRef __nullable CGPathCreateMutableCopyByTransformingPath(
-    CGPathRef __nullable path, const CGAffineTransform * __nullable transform)
+    CGPathRef cg_nullable path, const CGAffineTransform * __nullable transform)
     CG_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_5_0);
 
 /* Return a path representing a rectangle bounded by `rect'. The rectangle
@@ -119,7 +119,7 @@
    representing the rounded rectangle will be transformed by `transform'
    before they are added to the path. */
 
-CG_EXTERN void CGPathAddRoundedRect(CGMutablePathRef __nullable path,
+CG_EXTERN void CGPathAddRoundedRect(CGMutablePathRef cg_nullable path,
     const CGAffineTransform * __nullable transform, CGRect rect,
     CGFloat cornerWidth, CGFloat cornerHeight)
     CG_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_7_0);
@@ -131,7 +131,7 @@
    added to the path. */
 
 CG_EXTERN CGPathRef __nullable CGPathCreateCopyByDashingPath(
-    CGPathRef __nullable path, const CGAffineTransform * __nullable transform,
+    CGPathRef cg_nullable path, const CGAffineTransform * __nullable transform,
     CGFloat phase, const CGFloat * __nullable lengths, size_t count)
     CG_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_5_0);
 
@@ -142,7 +142,7 @@
    added to the path. */
 
 CG_EXTERN CGPathRef __nullable CGPathCreateCopyByStrokingPath(
-    CGPathRef __nullable path, const CGAffineTransform * __nullable transform,
+    CGPathRef cg_nullable path, const CGAffineTransform * __nullable transform,
     CGFloat lineWidth, CGLineCap lineCap,
     CGLineJoin lineJoin, CGFloat miterLimit)
     CG_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_5_0);
@@ -150,19 +150,19 @@
 /* Equivalent to `CFRetain(path)', except it doesn't crash (as CFRetain
    does) if `path' is NULL. */
 
-CG_EXTERN CGPathRef __nullable CGPathRetain(CGPathRef __nullable path)
+CG_EXTERN CGPathRef cg_nullable CGPathRetain(CGPathRef cg_nullable path)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Equivalent to `CFRelease(path)', except it doesn't crash (as CFRelease
    does) if `path' is NULL. */
 
-CG_EXTERN void CGPathRelease(CGPathRef __nullable path)
+CG_EXTERN void CGPathRelease(CGPathRef cg_nullable path)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Return true if `path1' is equal to `path2'; false otherwise. */
 
-CG_EXTERN bool CGPathEqualToPath(CGPathRef __nullable path1,
-    CGPathRef __nullable path2)
+CG_EXTERN bool CGPathEqualToPath(CGPathRef cg_nullable path1,
+    CGPathRef cg_nullable path2)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /*** Path construction functions. ***/
@@ -170,7 +170,7 @@
 /* Move the current point to `(x, y)' in `path' and begin a new subpath. If
    `m' is non-NULL, then transform `(x, y)' by `m' first. */
 
-CG_EXTERN void CGPathMoveToPoint(CGMutablePathRef __nullable path,
+CG_EXTERN void CGPathMoveToPoint(CGMutablePathRef cg_nullable path,
     const CGAffineTransform * __nullable m, CGFloat x, CGFloat y)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
@@ -178,7 +178,7 @@
    `path' and move the current point to `(x, y)'. If `m' is non-NULL, then
    transform `(x, y)' by `m' first. */
 
-CG_EXTERN void CGPathAddLineToPoint(CGMutablePathRef __nullable path,
+CG_EXTERN void CGPathAddLineToPoint(CGMutablePathRef cg_nullable path,
     const CGAffineTransform * __nullable m, CGFloat x, CGFloat y)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
@@ -186,7 +186,7 @@
    point `(cpx, cpy)' in `path' and move the current point to `(x, y)'. If
    `m' is non-NULL, then transform all points by `m' first. */
 
-CG_EXTERN void CGPathAddQuadCurveToPoint(CGMutablePathRef __nullable path,
+CG_EXTERN void CGPathAddQuadCurveToPoint(CGMutablePathRef cg_nullable path,
     const CGAffineTransform *__nullable m, CGFloat cpx, CGFloat cpy,
     CGFloat x, CGFloat y)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
@@ -196,7 +196,7 @@
    current point to `(x, y)'. If `m' is non-NULL, then transform all points
    by `m' first. */
 
-CG_EXTERN void CGPathAddCurveToPoint(CGMutablePathRef __nullable path,
+CG_EXTERN void CGPathAddCurveToPoint(CGMutablePathRef cg_nullable path,
     const CGAffineTransform * __nullable m, CGFloat cp1x, CGFloat cp1y,
     CGFloat cp2x, CGFloat cp2y, CGFloat x, CGFloat y)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
@@ -204,7 +204,7 @@
 /* Append a line from the current point to the starting point of the current
    subpath of `path' and end the subpath. */
 
-CG_EXTERN void CGPathCloseSubpath(CGMutablePathRef __nullable path)
+CG_EXTERN void CGPathCloseSubpath(CGMutablePathRef cg_nullable path)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /*** Path construction convenience functions. ***/
@@ -212,7 +212,7 @@
 /* Add `rect' to `path'. If `m' is non-NULL, then first transform `rect' by
    `m' before adding it to `path'. */
 
-CG_EXTERN void CGPathAddRect(CGMutablePathRef __nullable path,
+CG_EXTERN void CGPathAddRect(CGMutablePathRef cg_nullable path,
     const CGAffineTransform * __nullable m, CGRect rect)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
@@ -220,7 +220,7 @@
    `path'. If `m' is non-NULL, then first transform each rectangle by `m'
    before adding it to `path'. */
 
-CG_EXTERN void CGPathAddRects(CGMutablePathRef __nullable path,
+CG_EXTERN void CGPathAddRects(CGMutablePathRef cg_nullable path,
     const CGAffineTransform * __nullable m, const CGRect * __nullable rects,
     size_t count)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
@@ -229,7 +229,7 @@
    append a line from each point to the next point in `points'. If `m' is
    non-NULL, then first transform each point by `m'. */
 
-CG_EXTERN void CGPathAddLines(CGMutablePathRef __nullable path,
+CG_EXTERN void CGPathAddLines(CGMutablePathRef cg_nullable path,
     const CGAffineTransform * __nullable m, const CGPoint * __nullable points,
     size_t count)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
@@ -245,7 +245,7 @@
    `m' is non-NULL, then the constructed Bézier curves representing the
    ellipse will be transformed by `m' before they are added to `path'. */
 
-CG_EXTERN void CGPathAddEllipseInRect(CGMutablePathRef __nullable path,
+CG_EXTERN void CGPathAddEllipseInRect(CGMutablePathRef cg_nullable path,
     const CGAffineTransform * __nullable m, CGRect rect)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
@@ -260,7 +260,7 @@
    curves representing the arc will be transformed by `matrix' before they
    are added to the path. */
 
-CG_EXTERN void CGPathAddRelativeArc(CGMutablePathRef __nullable path,
+CG_EXTERN void CGPathAddRelativeArc(CGMutablePathRef cg_nullable path,
     const CGAffineTransform * __nullable matrix, CGFloat x, CGFloat y,
     CGFloat radius, CGFloat startAngle, CGFloat delta)
     CG_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_5_0);
@@ -287,7 +287,7 @@
    `startAngle' to 2π, `endAngle' to 0, and `clockwise' to true. This avoids
    the instability problems discussed above. */
 
-CG_EXTERN void CGPathAddArc(CGMutablePathRef __nullable path,
+CG_EXTERN void CGPathAddArc(CGMutablePathRef cg_nullable path,
     const CGAffineTransform * __nullable m,
     CGFloat x, CGFloat y, CGFloat radius, CGFloat startAngle, CGFloat endAngle,
     bool clockwise)
@@ -301,7 +301,7 @@
    representing the arc will be transformed by `m' before they are added to
    `path'. */
 
-CG_EXTERN void CGPathAddArcToPoint(CGMutablePathRef __nullable path,
+CG_EXTERN void CGPathAddArcToPoint(CGMutablePathRef cg_nullable path,
     const CGAffineTransform * __nullable m, CGFloat x1, CGFloat y1,
     CGFloat x2, CGFloat y2, CGFloat radius)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
@@ -309,26 +309,26 @@
 /* Add `path2' to `path1'. If `m' is non-NULL, then the points in `path2'
    will be transformed by `m' before they are added to `path1'. */
 
-CG_EXTERN void CGPathAddPath(CGMutablePathRef __nullable path1,
-    const CGAffineTransform * __nullable m, CGPathRef __nullable path2)
+CG_EXTERN void CGPathAddPath(CGMutablePathRef cg_nullable path1,
+    const CGAffineTransform * __nullable m, CGPathRef cg_nullable path2)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /*** Path information functions. ***/
 
 /* Return true if `path' contains no elements, false otherwise. */
 
-CG_EXTERN bool CGPathIsEmpty(CGPathRef __nullable path)
+CG_EXTERN bool CGPathIsEmpty(CGPathRef cg_nullable path)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Return true if `path' represents a rectangle, false otherwise. */
 
-CG_EXTERN bool CGPathIsRect(CGPathRef __nullable path, CGRect * __nullable rect)
+CG_EXTERN bool CGPathIsRect(CGPathRef cg_nullable path, CGRect * __nullable rect)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Return the current point of the current subpath of `path'. If there is no
    current point, then return CGPointZero. */
 
-CG_EXTERN CGPoint CGPathGetCurrentPoint(CGPathRef __nullable path)
+CG_EXTERN CGPoint CGPathGetCurrentPoint(CGPathRef cg_nullable path)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Return the bounding box of `path'. The bounding box is the smallest
@@ -336,7 +336,7 @@
    points for Bézier cubic and quadratic curves. If the path is empty, then
    return `CGRectNull'. */
 
-CG_EXTERN CGRect CGPathGetBoundingBox(CGPathRef __nullable path)
+CG_EXTERN CGRect CGPathGetBoundingBox(CGPathRef cg_nullable path)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Return the path bounding box of `path'. The path bounding box is the
@@ -344,7 +344,7 @@
    including control points for Bézier cubic and quadratic curves. If the
    path is empty, then return `CGRectNull'. */
 
-CG_EXTERN CGRect CGPathGetPathBoundingBox(CGPathRef __nullable path)
+CG_EXTERN CGRect CGPathGetPathBoundingBox(CGPathRef cg_nullable path)
     CG_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_4_0);
 
 /* Return true if `point' is contained in `path'; false otherwise. A point
@@ -354,7 +354,7 @@
    fill rule is used. If `m' is non-NULL, then the point is transformed by
    `m' before determining whether the path contains it. */
 
-CG_EXTERN bool CGPathContainsPoint(CGPathRef __nullable path,
+CG_EXTERN bool CGPathContainsPoint(CGPathRef cg_nullable path,
     const CGAffineTransform * __nullable m, CGPoint point, bool eoFill)
     CG_AVAILABLE_STARTING(__MAC_10_4, __IPHONE_2_0);
 
@@ -384,8 +384,8 @@
 /* For element of `path', call `function', passing it the path element and
    `info'. */
 
-CG_EXTERN void CGPathApply(CGPathRef __nullable path, void * __nullable info,
-    CGPathApplierFunction __nullable function)
+CG_EXTERN void CGPathApply(CGPathRef cg_nullable path, void * __nullable info,
+    CGPathApplierFunction cg_nullable function)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 CF_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPattern.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPattern.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPattern.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGPattern.h	2016-06-03 04:58:47.000000000 +0200
@@ -46,7 +46,7 @@
     `releaseInfo' is called when the pattern is deallocated. */
 
 typedef void (*CGPatternDrawPatternCallback)(void * __nullable info,
-                                             CGContextRef __nullable context);
+                                             CGContextRef cg_nullable context);
 typedef void (*CGPatternReleaseInfoCallback)(void * __nullable info);
 
 struct CGPatternCallbacks {
@@ -66,19 +66,19 @@
 CG_EXTERN CGPatternRef __nullable CGPatternCreate(void * __nullable info,
     CGRect bounds, CGAffineTransform matrix, CGFloat xStep, CGFloat yStep,
     CGPatternTiling tiling, bool isColored,
-    const CGPatternCallbacks * __nullable callbacks)
+    const CGPatternCallbacks * cg_nullable callbacks)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Equivalent to `CFRetain(pattern)', except it doesn't crash (as CF does)
    if `pattern' is NULL. */
 
-CG_EXTERN CGPatternRef __nullable CGPatternRetain(CGPatternRef __nullable pattern)
+CG_EXTERN CGPatternRef cg_nullable CGPatternRetain(CGPatternRef cg_nullable pattern)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 /* Equivalent to `CFRelease(pattern)', except it doesn't crash (as CF does)
    if `pattern' is NULL. */
 
-CG_EXTERN void CGPatternRelease(CGPatternRef __nullable pattern)
+CG_EXTERN void CGPatternRelease(CGPatternRef cg_nullable pattern)
     CG_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
 
 CF_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGShading.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGShading.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGShading.h	2015-10-02 23:58:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreGraphics.framework/Headers/CGShading.h	2016-06-03 04:58:47.000000000 +0200
@@ -42,8 +42,8 @@
    shading will extend beyond the ending point of the axis. */
 
 CG_EXTERN CGShadingRef __nullable CGShadingCreateAxial(
-    CGColorSpaceRef __nullable space, CGPoint start, CGPoint end,
-    CGFunctionRef __nullable function, bool extendStart, bool extendEnd)
+    CGColorSpaceRef cg_nullable space, CGPoint start, CGPoint end,
+    CGFunctionRef cg_nullable function, bool extendStart, bool extendEnd)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Create a shading defining a color blend which varies between two circles.
@@ -62,21 +62,21 @@
    circle. */
 
 CG_EXTERN CGShadingRef __nullable CGShadingCreateRadial(
-    CGColorSpaceRef __nullable space,
+    CGColorSpaceRef cg_nullable space,
     CGPoint start, CGFloat startRadius, CGPoint end, CGFloat endRadius,
-    CGFunctionRef __nullable function, bool extendStart, bool extendEnd)
+    CGFunctionRef cg_nullable function, bool extendStart, bool extendEnd)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Equivalent to `CFRetain(shading)', except it doesn't crash (as CFRetain
    does) if `shading' is NULL. */
 
-CG_EXTERN CGShadingRef __nullable CGShadingRetain(CGShadingRef __nullable shading)
+CG_EXTERN CGShadingRef cg_nullable CGShadingRetain(CGShadingRef cg_nullable shading)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 /* Equivalent to `CFRelease(shading)', except it doesn't crash (as CFRelease
    does) if `shading' is NULL. */
 
-CG_EXTERN void CGShadingRelease(CGShadingRef __nullable shading)
+CG_EXTERN void CGShadingRelease(CGShadingRef cg_nullable shading)
     CG_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_2_0);
 
 CF_ASSUME_NONNULL_END

```