#CoreVideo.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVBase.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVBase.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVBase.h	2016-05-18 02:29:54.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVBase.h	2016-06-26 07:27:26.000000000 +0200
@@ -196,7 +196,7 @@
     @constant       kCVSMPTETimeType5994
                         59.94 Frame
 */
-enum
+typedef CF_ENUM(uint32_t, CVSMPTETimeType)
 {
     kCVSMPTETimeType24        = 0,
     kCVSMPTETimeType25        = 1,
@@ -216,14 +216,14 @@
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
 
@@ -275,7 +275,7 @@
 } CVTimeStamp; 
 
 // Flags for the CVTimeStamp structure
-enum
+typedef CF_OPTIONS(uint64_t, CVTimeStampFlags)
 {
     kCVTimeStampVideoTimeValid              = (1L << 0),
     kCVTimeStampHostTimeValid               = (1L << 1),
@@ -285,14 +285,11 @@
     
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVBuffer.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVBuffer.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVBuffer.h	2016-05-04 00:21:25.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVBuffer.h	2016-06-26 07:44:37.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVMetalTextureCache.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVMetalTextureCache.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVMetalTextureCache.h	2016-05-04 00:21:25.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVMetalTextureCache.h	2016-06-26 08:36:12.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelBuffer.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelBuffer.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelBuffer.h	2016-05-14 17:17:44.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelBuffer.h	2016-06-26 07:44:37.000000000 +0200
@@ -102,12 +102,7 @@
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelBufferPool.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelBufferPool.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelBufferPool.h	2016-05-04 00:21:26.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelBufferPool.h	2016-06-26 07:27:26.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelFormatDescription.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelFormatDescription.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelFormatDescription.h	2016-05-04 00:21:21.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreVideo.framework/Headers/CVPixelFormatDescription.h	2016-06-26 07:44:37.000000000 +0200
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

```