#CoreVideo.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVBase.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVBase.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVBase.h	2015-08-23 03:02:42.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVBase.h	2016-05-18 02:00:26.000000000 +0200
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
@@ -188,7 +196,7 @@
     @constant       kCVSMPTETimeType5994
                         59.94 Frame
 */
-enum
+typedef CF_ENUM(uint32_t, CVSMPTETimeType)
 {
     kCVSMPTETimeType24        = 0,
     kCVSMPTETimeType25        = 1,
@@ -208,14 +216,14 @@
     @constant       kCVSMPTETimeRunning
                         Time is running.
 */
-enum
+typedef CF_OPTIONS(uint32_t, CVSMPTETimeFlags)
 {
     kCVSMPTETimeValid     = (1L << 0),
     kCVSMPTETimeRunning   = (1L << 1)
 };
 
 
-enum {
+typedef CF_OPTIONS(int32_t, CVTimeFlags) {
     kCVTimeIsIndefinite = 1 << 0
 };
 
@@ -267,7 +275,7 @@
 } CVTimeStamp; 
 
 // Flags for the CVTimeStamp structure
-enum
+typedef CF_OPTIONS(uint64_t, CVTimeStampFlags)
 {
     kCVTimeStampVideoTimeValid              = (1L << 0),
     kCVTimeStampHostTimeValid               = (1L << 1),
@@ -277,14 +285,11 @@
     
     // There are flags for each field to make it easier to detect interlaced vs progressive output
     kCVTimeStampTopField                    = (1L << 16),
-    kCVTimeStampBottomField                 = (1L << 17)
-};
+    kCVTimeStampBottomField                 = (1L << 17),
 
-//	Some commonly used combinations of timestamp flags
-enum
-{
-    kCVTimeStampVideoHostTimeValid   = (kCVTimeStampVideoTimeValid | kCVTimeStampHostTimeValid),
-    kCVTimeStampIsInterlaced	     = (kCVTimeStampTopField | kCVTimeStampBottomField)
+    // Some commonly used combinations of timestamp flags
+    kCVTimeStampVideoHostTimeValid          = (kCVTimeStampVideoTimeValid | kCVTimeStampHostTimeValid),
+    kCVTimeStampIsInterlaced                = (kCVTimeStampTopField | kCVTimeStampBottomField)
 };
 
 CV_EXPORT const CVTime kCVZeroTime;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVBuffer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVBuffer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVBuffer.h	2015-08-23 03:02:42.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVBuffer.h	2016-05-18 02:00:26.000000000 +0200
@@ -50,12 +50,7 @@
 
 #pragma mark CVBufferRef
 
-typedef uint32_t CVAttachmentMode;
-#if COREVIDEO_USE_DERIVED_ENUMS_FOR_CONSTANTS
-enum : CVAttachmentMode
-#else
-enum
-#endif
+typedef CF_ENUM(uint32_t, CVAttachmentMode)
 {
 	kCVAttachmentMode_ShouldNotPropagate    = 0,
 	kCVAttachmentMode_ShouldPropagate       = 1
@@ -135,7 +130,7 @@
     @result     A CFDictionary with all buffer attachments identified by there keys. If no attachment is present, the dictionary is empty.  Returns NULL
 		for invalid attachment mode.
 */
-CV_EXPORT CFDictionaryRef CV_NULLABLE CVBufferGetAttachments( CVBufferRef CV_NONNULL buffer, CVAttachmentMode attachmentMode ) __OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_4_0);
+CV_EXPORT CFDictionaryRef CF_RETURNS_NOT_RETAINED CV_NULLABLE CVBufferGetAttachments( CVBufferRef CV_NONNULL buffer, CVAttachmentMode attachmentMode ) __OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_4_0);
 
 /*!
     @function   CVBufferSetAttachments
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVDisplayLink.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVDisplayLink.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVDisplayLink.h	2015-08-23 03:02:42.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVDisplayLink.h	2016-05-18 02:00:26.000000000 +0200
@@ -138,7 +138,7 @@
     @param	userInfo  User data for the callback to identify the context.
     @result     CVReturn. kCVReturnSuccess if successfull.
 */
-CV_EXPORT CVReturn CVDisplayLinkSetOutputCallback( CVDisplayLinkRef CV_NONNULL displayLink, CVDisplayLinkOutputCallback CV_NONNULL callback, void * CV_NULLABLE userInfo ) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER;
+CV_EXPORT CVReturn CVDisplayLinkSetOutputCallback( CVDisplayLinkRef CV_NONNULL displayLink, CVDisplayLinkOutputCallback CV_NULLABLE callback, void * CV_NULLABLE userInfo ) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER;
 
 /*!
 	 @function   CVDisplayLinkSetOutputHandler
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVImageBuffer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVImageBuffer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVImageBuffer.h	2015-08-23 03:02:42.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVImageBuffer.h	2016-05-18 04:03:33.000000000 +0200
@@ -66,6 +66,8 @@
 CV_EXPORT const CFStringRef CV_NONNULL kCVImageBufferYCbCrMatrix_ITU_R_709_2 __OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_4_0);			// CFString
 CV_EXPORT const CFStringRef CV_NONNULL kCVImageBufferYCbCrMatrix_ITU_R_601_4 __OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_4_0);			// CFString
 CV_EXPORT const CFStringRef CV_NONNULL kCVImageBufferYCbCrMatrix_SMPTE_240M_1995 __OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_4_0);		// CFString
+CV_EXPORT const CFStringRef CV_NONNULL kCVImageBufferYCbCrMatrix_DCI_P3 __OSX_AVAILABLE_STARTING(__MAC_10_11,__IPHONE_9_0);				// CFString
+CV_EXPORT const CFStringRef CV_NONNULL kCVImageBufferYCbCrMatrix_P3_D65 __OSX_AVAILABLE_STARTING(__MAC_10_11,__IPHONE_9_0);				// CFString
 CV_EXPORT const CFStringRef CV_NONNULL kCVImageBufferYCbCrMatrix_ITU_R_2020 __OSX_AVAILABLE_STARTING(__MAC_10_11,__IPHONE_9_0);		// CFString
 
 CV_EXPORT const CFStringRef CV_NONNULL kCVImageBufferColorPrimariesKey __OSX_AVAILABLE_STARTING(__MAC_10_5,__IPHONE_4_0);				// CFString describing the color primaries. This key can be one of the following values
@@ -84,7 +86,8 @@
 CV_EXPORT const CFStringRef CV_NONNULL kCVImageBufferTransferFunction_EBU_3213 __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_5,__MAC_10_6,__IPHONE_NA,__IPHONE_NA);			// Should not be used.
 CV_EXPORT const CFStringRef CV_NONNULL kCVImageBufferTransferFunction_SMPTE_C __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_5,__MAC_10_6,__IPHONE_NA,__IPHONE_NA);			// Should not be used.
 CV_EXPORT const CFStringRef CV_NONNULL kCVImageBufferTransferFunction_ITU_R_2020 __OSX_AVAILABLE_STARTING(__MAC_10_11,__IPHONE_9_0);
-
+CV_EXPORT const CFStringRef CV_NONNULL kCVImageBufferTransferFunction_SMPTE_ST_428_1 __OSX_AVAILABLE_STARTING(__MAC_10_12,__IPHONE_10_0);
+	
 /* Chroma siting information. For progressive images, only the TopField value is used. */
 CV_EXPORT const CFStringRef CV_NONNULL kCVImageBufferChromaLocationTopFieldKey __OSX_AVAILABLE_STARTING(__MAC_10_5,__IPHONE_4_0);			// CFString with one of the following CFString values
 CV_EXPORT const CFStringRef CV_NONNULL kCVImageBufferChromaLocationBottomFieldKey __OSX_AVAILABLE_STARTING(__MAC_10_5,__IPHONE_4_0);		// CFString with one of the following CFString values
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVMetalTextureCache.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVMetalTextureCache.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVMetalTextureCache.h	2015-08-23 03:02:42.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVMetalTextureCache.h	2016-05-18 02:00:26.000000000 +0200
@@ -68,7 +68,7 @@
 					CFDictionaryRef CV_NULLABLE cacheAttributes,
 					id <MTLDevice> CV_NONNULL metalDevice,
 					CFDictionaryRef CV_NULLABLE textureAttributes,
-					CVMetalTextureCacheRef CV_NULLABLE * CV_NONNULL cacheOut ) __OSX_AVAILABLE_STARTING(__MAC_10_11,__IPHONE_8_0);
+					CV_RETURNS_RETAINED_PARAMETER CVMetalTextureCacheRef CV_NULLABLE * CV_NONNULL cacheOut ) __OSX_AVAILABLE_STARTING(__MAC_10_11,__IPHONE_8_0);
 
 /*!
     @function   CVMetalTextureCacheCreateTextureFromImage
@@ -115,7 +115,7 @@
 								       size_t width,
 								       size_t height,
 								       size_t planeIndex,
-									   CVMetalTextureRef CV_NULLABLE * CV_NONNULL textureOut ) __OSX_AVAILABLE_STARTING(__MAC_10_11,__IPHONE_8_0);
+									   CV_RETURNS_RETAINED_PARAMETER CVMetalTextureRef CV_NULLABLE * CV_NONNULL textureOut ) __OSX_AVAILABLE_STARTING(__MAC_10_11,__IPHONE_8_0);
 
 /*!
     @function   CVMetalTextureCacheFlush
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelBuffer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelBuffer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelBuffer.h	2015-08-23 03:02:42.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelBuffer.h	2016-05-18 02:00:26.000000000 +0200
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
 
 	
@@ -97,12 +102,7 @@
 		should be passed both to the lock and unlock functions.  Non-symmetrical usage of this
 		flag will result in undefined behavior.
 */
-typedef CVOptionFlags CVPixelBufferLockFlags;
-#if COREVIDEO_USE_DERIVED_ENUMS_FOR_CONSTANTS
-enum : CVPixelBufferLockFlags
-#else
-enum
-#endif
+typedef CF_OPTIONS(CVOptionFlags, CVPixelBufferLockFlags)
 {
 	kCVPixelBufferLock_ReadOnly = 0x00000001,
 };
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelBufferPool.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelBufferPool.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelBufferPool.h	2015-08-23 03:02:42.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelBufferPool.h	2016-05-18 02:00:26.000000000 +0200
@@ -76,7 +76,7 @@
     @param      pool  The CVPixelBufferPoolRef to retrieve the attributes from
     @result     Returns the pool attributes dictionary, or NULL on failure.
 */
-CV_EXPORT CFDictionaryRef CV_NULLABLE CVPixelBufferPoolGetAttributes( CVPixelBufferPoolRef CV_NONNULL pool ) __OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_4_0);
+CV_EXPORT CFDictionaryRef CF_RETURNS_NOT_RETAINED CV_NULLABLE CVPixelBufferPoolGetAttributes( CVPixelBufferPoolRef CV_NONNULL pool ) __OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_4_0);
 
 /*!
     @function   CVPixelBufferPoolGetPixelBufferAttributes
@@ -86,7 +86,7 @@
     @param      pool  The CVPixelBufferPoolRef to retrieve the attributes from
     @result     Returns the pixel buffer attributes dictionary, or NULL on failure.
 */
-CV_EXPORT CFDictionaryRef CV_NULLABLE CVPixelBufferPoolGetPixelBufferAttributes( CVPixelBufferPoolRef CV_NONNULL pool ) __OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_4_0);
+CV_EXPORT CFDictionaryRef CF_RETURNS_NOT_RETAINED CV_NULLABLE CVPixelBufferPoolGetPixelBufferAttributes( CVPixelBufferPoolRef CV_NONNULL pool ) __OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_4_0);
 
 /*!
     @function   CVPixelBufferPoolCreatePixelBuffer
@@ -142,12 +142,7 @@
 		This flag will cause CVPixelBufferPoolFlush to flush all unused buffers regardless of age.
 */
 
-typedef CVOptionFlags CVPixelBufferPoolFlushFlags;
-#if COREVIDEO_USE_DERIVED_ENUMS_FOR_CONSTANTS
-enum : CVPixelBufferPoolFlushFlags
-#else
-enum
-#endif
+typedef CF_OPTIONS(CVOptionFlags,CVPixelBufferPoolFlushFlags)
 {
 	kCVPixelBufferPoolFlushExcessBuffers = 1,
 };
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelFormatDescription.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelFormatDescription.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelFormatDescription.h	2015-08-23 03:02:42.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelFormatDescription.h	2016-05-18 02:00:26.000000000 +0200
@@ -123,10 +123,10 @@
 CV_EXPORT const CFStringRef CV_NONNULL kCVPixelFormatFillExtendedPixelsCallback __OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_4_0);
 
 /* Create a description of a pixel format from a provided OSType */
-CV_EXPORT CFDictionaryRef CV_NULLABLE CVPixelFormatDescriptionCreateWithPixelFormatType(CFAllocatorRef CV_NULLABLE allocator, OSType pixelFormat) __OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_4_0);
+CV_EXPORT CFDictionaryRef CF_RETURNS_RETAINED CV_NULLABLE CVPixelFormatDescriptionCreateWithPixelFormatType(CFAllocatorRef CV_NULLABLE allocator, OSType pixelFormat) __OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_4_0);
 
 /* Get a CFArray of CFNumbers containing all known pixel formats as OSTypes */
-CV_EXPORT CFArrayRef CV_NULLABLE CVPixelFormatDescriptionArrayCreateWithAllPixelFormatTypes(CFAllocatorRef CV_NULLABLE allocator) __OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_4_0);
+CV_EXPORT CFArrayRef CF_RETURNS_RETAINED CV_NULLABLE CVPixelFormatDescriptionArrayCreateWithAllPixelFormatTypes(CFAllocatorRef CV_NULLABLE allocator) __OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_4_0);
 
 /* Register a new pixel format with CoreVideo */
 CV_EXPORT void CVPixelFormatDescriptionRegisterDescriptionWithPixelFormatType(CFDictionaryRef CV_NONNULL description, OSType pixelFormat) __OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_4_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVReturn.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVReturn.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVReturn.h	2015-08-23 03:02:42.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVReturn.h	2016-05-14 17:04:01.000000000 +0200
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
     
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CoreVideo.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CoreVideo.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CoreVideo.h	2015-08-23 03:02:42.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CoreVideo.h	2016-05-18 02:00:26.000000000 +0200
@@ -48,7 +48,7 @@
 #include <CoreVideo/CVDirect3DTextureCache.h>
 #endif
 
-#if COREVIDEO_SUPPORTS_METAL
+#if TARGET_OS_MAC
 #include <CoreVideo/CVMetalTexture.h>
 #include <CoreVideo/CVMetalTextureCache.h>
 #endif

```