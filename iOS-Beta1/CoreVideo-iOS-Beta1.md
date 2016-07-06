#CoreVideo.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVBase.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVBase.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVBase.h	2015-10-02 23:51:01.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVBase.h	2016-05-18 02:29:54.000000000 +0200
@@ -2,7 +2,7 @@
  *  CVBase.h
  *  CoreVideo
  *
- *  Copyright (c) 2004-2015 Apple Inc. All rights reserved.
+ *  Copyright (c) 2004-2016 Apple Inc. All rights reserved.
  *
  */
  
@@ -52,10 +52,18 @@
 #define __AVAILABILITY_INTERNAL__MAC_10_11        __AVAILABILITY_INTERNAL_WEAK_IMPORT
 #endif
 
+#ifndef __AVAILABILITY_INTERNAL__MAC_10_12
+#define __AVAILABILITY_INTERNAL__MAC_10_12        __AVAILABILITY_INTERNAL_WEAK_IMPORT
+#endif
+
 #ifndef __AVAILABILITY_INTERNAL__IPHONE_9_0
 #define __AVAILABILITY_INTERNAL__IPHONE_9_0        __AVAILABILITY_INTERNAL_WEAK_IMPORT
 #endif
 
+#ifndef __AVAILABILITY_INTERNAL__IPHONE_10_0
+#define __AVAILABILITY_INTERNAL__IPHONE_10_0        __AVAILABILITY_INTERNAL_WEAK_IMPORT
+#endif
+
 #include <CoreFoundation/CFBase.h>
 
 #if defined(__cplusplus)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVImageBuffer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVImageBuffer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVImageBuffer.h	2015-10-02 23:51:01.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVImageBuffer.h	2016-05-18 04:03:33.000000000 +0200
@@ -86,7 +86,8 @@
 CV_EXPORT const CFStringRef CV_NONNULL kCVImageBufferTransferFunction_EBU_3213 __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_5,__MAC_10_6,__IPHONE_NA,__IPHONE_NA);			// Should not be used.
 CV_EXPORT const CFStringRef CV_NONNULL kCVImageBufferTransferFunction_SMPTE_C __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_5,__MAC_10_6,__IPHONE_NA,__IPHONE_NA);			// Should not be used.
 CV_EXPORT const CFStringRef CV_NONNULL kCVImageBufferTransferFunction_ITU_R_2020 __OSX_AVAILABLE_STARTING(__MAC_10_11,__IPHONE_9_0);
-
+CV_EXPORT const CFStringRef CV_NONNULL kCVImageBufferTransferFunction_SMPTE_ST_428_1 __OSX_AVAILABLE_STARTING(__MAC_10_12,__IPHONE_10_0);
+	
 /* Chroma siting information. For progressive images, only the TopField value is used. */
 CV_EXPORT const CFStringRef CV_NONNULL kCVImageBufferChromaLocationTopFieldKey __OSX_AVAILABLE_STARTING(__MAC_10_5,__IPHONE_4_0);			// CFString with one of the following CFString values
 CV_EXPORT const CFStringRef CV_NONNULL kCVImageBufferChromaLocationBottomFieldKey __OSX_AVAILABLE_STARTING(__MAC_10_5,__IPHONE_4_0);		// CFString with one of the following CFString values
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVOpenGLESTextureCache.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVOpenGLESTextureCache.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVOpenGLESTextureCache.h	2015-10-02 23:51:01.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVOpenGLESTextureCache.h	2016-05-18 04:03:33.000000000 +0200
@@ -82,7 +82,7 @@
     @param      sourceImage The CVImageBuffer that you want to create a CVOpenGLESTexture from.
     @param      textureAttributes A CFDictionaryRef containing attributes to be used for creating the CVOpenGLESTexture objects.  May be NULL.
     @param      target Specifies the target texture.  GL_TEXTURE_2D and GL_RENDERBUFFER are the only targets currently supported.
-    @param      internalFormat Specifies the number of color components in the texture.  Examples are GL_RGBA, GL_LUMINANCE, GL_RGBA8_OES, GL_RED, and GL_RG.
+    @param      internalFormat Specifies the number of color components in the texture.  Examples are GL_RGBA, GL_LUMINANCE, GL_RGBA8_OES, GL_RG, and GL_RED (NOTE: On GLES3 use GL_R8 instead of GL_RED).
     @param      width Specifies the width of the texture image.
     @param      height Specifies the height of the texture image.
     @param      format Specifies the format of the pixel data.  Examples are GL_RGBA and GL_LUMINANCE.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelBuffer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelBuffer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelBuffer.h	2015-10-02 23:51:01.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelBuffer.h	2016-05-14 17:17:44.000000000 +0200
@@ -79,12 +79,17 @@
   kCVPixelFormatType_422YpCbCr8FullRange = 'yuvf', /* Component Y'CbCr 8-bit 4:2:2, full range, ordered Y'0 Cb Y'1 Cr */
   kCVPixelFormatType_OneComponent8  = 'L008',     /* 8 bit one component, black is zero */
   kCVPixelFormatType_TwoComponent8  = '2C08',     /* 8 bit two component, black is zero */
+  kCVPixelFormatType_30RGBLEPackedWideGamut = 'w30r', /* little-endian RGB101010, 2 MSB are zero, wide-gamut (384-895) */
   kCVPixelFormatType_OneComponent16Half  = 'L00h',     /* 16 bit one component IEEE half-precision float, 16-bit little-endian samples */
   kCVPixelFormatType_OneComponent32Float = 'L00f',     /* 32 bit one component IEEE float, 32-bit little-endian samples */
   kCVPixelFormatType_TwoComponent16Half  = '2C0h',     /* 16 bit two component IEEE half-precision float, 16-bit little-endian samples */
   kCVPixelFormatType_TwoComponent32Float = '2C0f',     /* 32 bit two component IEEE float, 32-bit little-endian samples */
   kCVPixelFormatType_64RGBAHalf          = 'RGhA',     /* 64 bit RGBA IEEE half-precision float, 16-bit little-endian samples */
   kCVPixelFormatType_128RGBAFloat        = 'RGfA',     /* 128 bit RGBA IEEE float, 32-bit little-endian samples */
+  kCVPixelFormatType_14Bayer_GRBG        = 'grb4',     /* Bayer 14-bit Little-Endian, packed in 16-bits, ordered G R G R... alternating with B G B G... */
+  kCVPixelFormatType_14Bayer_RGGB        = 'rgg4',     /* Bayer 14-bit Little-Endian, packed in 16-bits, ordered R G R G... alternating with G B G B... */
+  kCVPixelFormatType_14Bayer_BGGR        = 'bgg4',     /* Bayer 14-bit Little-Endian, packed in 16-bits, ordered B G B G... alternating with G R G R... */
+  kCVPixelFormatType_14Bayer_GBRG        = 'gbr4',     /* Bayer 14-bit Little-Endian, packed in 16-bits, ordered G B G B... alternating with R G R G... */
 };
 
 	
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVReturn.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVReturn.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVReturn.h	2015-10-02 23:51:01.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVReturn.h	2016-05-14 17:04:01.000000000 +0200
@@ -48,6 +48,7 @@
     @constant   kCVReturnWouldExceedAllocationThreshold The allocation request failed because it would have exceeded a specified allocation threshold (see kCVPixelBufferPoolAllocationThresholdKey).
     @constant   kCVReturnPoolAllocationFailed The allocation for the buffer pool failed. Most likely because of lack of resources. Check if your parameters are in range.
     @constant   kCVReturnInvalidPoolAttributes A CVBufferPool cannot be created with the given attributes.
+    @constant   kCVReturnRetry a scan hasn't completely traversed the CVBufferPool due to a concurrent operation. The client can retry the scan.
 */
 
 typedef int32_t CVReturn;
@@ -83,6 +84,7 @@
     kCVReturnWouldExceedAllocationThreshold  = -6689,
     kCVReturnPoolAllocationFailed            = -6690,
     kCVReturnInvalidPoolAttributes           = -6691,
+    kCVReturnRetry                           = -6692,
 	
     kCVReturnLast                            = -6699
     
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CoreVideo.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CoreVideo.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CoreVideo.h	2015-10-02 23:51:01.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CoreVideo.h	2016-05-14 17:04:01.000000000 +0200
@@ -48,7 +48,7 @@
 #include <CoreVideo/CVDirect3DTextureCache.h>
 #endif
 
-#if COREVIDEO_SUPPORTS_METAL
+#if TARGET_OS_MAC
 #include <CoreVideo/CVMetalTexture.h>
 #include <CoreVideo/CVMetalTextureCache.h>
 #endif

```