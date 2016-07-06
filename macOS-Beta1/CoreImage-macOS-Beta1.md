#CoreImage.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIColor.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIColor.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIColor.h	2015-08-25 05:35:43.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIColor.h	2016-05-21 07:18:49.000000000 +0200
@@ -27,6 +27,11 @@
 + (instancetype)colorWithRed:(CGFloat)r green:(CGFloat)g blue:(CGFloat)b alpha:(CGFloat)a;
 + (instancetype)colorWithRed:(CGFloat)r green:(CGFloat)g blue:(CGFloat)b;
 
+/* Create a new color object in a given colorspace. 
+ * Will return null if the colorspace is not kCGColorSpaceModelRGB. */
++ (nullable instancetype)colorWithRed:(CGFloat)r green:(CGFloat)g blue:(CGFloat)b alpha:(CGFloat)a colorSpace:(CGColorSpaceRef)colorSpace NS_AVAILABLE(10_12, 10_0);
++ (nullable instancetype)colorWithRed:(CGFloat)r green:(CGFloat)g blue:(CGFloat)b colorSpace:(CGColorSpaceRef)colorSpace NS_AVAILABLE(10_12, 10_0);
+
 /* Create a new color object, 'representation' should be a string in one of
  * the formats returned by the stringRepresentation method. */
 + (instancetype)colorWithString:(NSString *)representation;
@@ -41,6 +46,10 @@
 - (instancetype)initWithRed:(CGFloat)r green:(CGFloat)g blue:(CGFloat)b alpha:(CGFloat)a;
 - (instancetype)initWithRed:(CGFloat)r green:(CGFloat)g blue:(CGFloat)b NS_AVAILABLE(10_11, 9_0);
 
+/* Initialize a new color object in a given colorspace.
+ * Will return null if the colorspace is not kCGColorSpaceModelRGB. */
+- (nullable instancetype)initWithRed:(CGFloat)r green:(CGFloat)g blue:(CGFloat)b alpha:(CGFloat)a colorSpace:(CGColorSpaceRef)colorSpace NS_AVAILABLE(10_12, 10_0);
+- (nullable instancetype)initWithRed:(CGFloat)r green:(CGFloat)g blue:(CGFloat)b colorSpace:(CGColorSpaceRef)colorSpace NS_AVAILABLE(10_12, 10_0);
 
 /* Return the number of color components (including alpha). */
 @property (readonly) size_t numberOfComponents;
@@ -65,6 +74,18 @@
  * The value of the NSString will be the same each time it is called. */
 @property (readonly) NSString *stringRepresentation;
 
+// Some convenience methods to create CIColors in the sRGB colorspace.
++ (instancetype)blackColor NS_AVAILABLE(10_12, 10_0);
++ (instancetype)whiteColor NS_AVAILABLE(10_12, 10_0);
++ (instancetype)grayColor NS_AVAILABLE(10_12, 10_0);
++ (instancetype)redColor NS_AVAILABLE(10_12, 10_0);
++ (instancetype)greenColor NS_AVAILABLE(10_12, 10_0);
++ (instancetype)blueColor NS_AVAILABLE(10_12, 10_0);
++ (instancetype)cyanColor NS_AVAILABLE(10_12, 10_0);
++ (instancetype)magentaColor NS_AVAILABLE(10_12, 10_0);
++ (instancetype)yellowColor NS_AVAILABLE(10_12, 10_0);
++ (instancetype)clearColor NS_AVAILABLE(10_12, 10_0);
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIContext.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIContext.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIContext.h	2016-02-20 00:10:58.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIContext.h	2016-05-21 08:03:12.000000000 +0200
@@ -19,14 +19,6 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-#if __has_feature(objc_generics)
-# define CI_DICTIONARY(KeyType, ValueType) NSDictionary<KeyType, ValueType>
-# define CI_ARRAY(ValueType) NSArray <ValueType>
-#else
-# define CI_DICTIONARY(KeyType, ValueType) NSDictionary
-# define CI_ARRAY(ValueType) NSArray
-#endif
-
 
 NS_CLASS_AVAILABLE(10_4, 5_0)
 @interface CIContext : NSObject
@@ -52,11 +44,19 @@
 CORE_IMAGE_EXPORT NSString * const kCIContextWorkingFormat NS_AVAILABLE(10_4,8_0);
 
 /* A boolean NSNumber controlling the quality of affine downsample operations.
- * @YES imply that more quality is desired.
- * On iOS the the default value is @NO.
- * On OSX the the default value is @YES. */
+ * @YES implies that more quality is desired.
+ * On iOS the default value is @NO.
+ * On OSX the default value is @YES. */
 CORE_IMAGE_EXPORT NSString * const kCIContextHighQualityDownsample NS_AVAILABLE(10_11,9_0);
 
+/* A boolean NSNumber controlling whether output renders produce alpha-premultiplied pixels.
+ * The default value is @YES. */
+CORE_IMAGE_EXPORT NSString * const kCIContextOutputPremultiplied NS_AVAILABLE(10_4,7_0);
+
+/* A boolean NSNumber controlling how intermediate buffers are cached.
+ * If @NO, the context will empty intermediates during and after renders.
+ * The default value is @YES. */
+CORE_IMAGE_EXPORT NSString * const kCIContextCacheIntermediates NS_AVAILABLE(10_12,10_0);
 
 /* An NSNumber with a boolean value. When @YES the context will use
  * software rendering. */
@@ -64,7 +64,10 @@
 
 /* An NSNumber with a boolean value. When @YES the context will use 
  * low priority rendering on the GPU. */
-CORE_IMAGE_EXPORT NSString * const kCIContextPriorityRequestLow NS_AVAILABLE_IOS(8_0);
+CORE_IMAGE_EXPORT NSString * const kCIContextPriorityRequestLow NS_AVAILABLE(10_12, 8_0);
+
+
+#pragma mark - contextWithCGLContext
 
 /* Create a new CoreImage context object, all output will be drawn
  * into the surface attached to the OpenGL context 'cglctx'. If 'pixelFormat' is
@@ -76,7 +79,7 @@
 + (CIContext *)contextWithCGLContext:(CGLContextObj)cglctx
 						 pixelFormat:(nullable CGLPixelFormatObj)pixelFormat
 						  colorSpace:(nullable CGColorSpaceRef)colorSpace
-							 options:(nullable CI_DICTIONARY(NSString*,id) *)options
+							 options:(nullable NSDictionary<NSString*,id> *)options
     NS_AVAILABLE_MAC(10_6);
 #endif
 
@@ -86,43 +89,93 @@
 #if !TARGET_OS_IPHONE
 + (CIContext *)contextWithCGLContext:(CGLContextObj)cglctx
 						 pixelFormat:(nullable CGLPixelFormatObj)pixelFormat
-							 options:(nullable CI_DICTIONARY(NSString*,id) *)options
+							 options:(nullable NSDictionary<NSString*,id> *)options
     NS_DEPRECATED_MAC(10_4,10_6);
 #endif
 
-/* Create a new CoreImage context object, all output will be drawn
- * into the CG context 'cgctx'. */
+
+#pragma mark - contextWithCGContext
+
+/* Create a context specifying a destination CGContext.
+ *
+ * Core Image will use an internal destination context when methods such
+ * as [context render:to...] or [context createCGImage:...] are called.
+ *
+ * The [context drawImage:...] render methods will render to the CGContext.
+ */
 + (CIContext *)contextWithCGContext:(CGContextRef)cgctx
-                            options:(nullable CI_DICTIONARY(NSString*,id) *)options
+                            options:(nullable NSDictionary<NSString*,id> *)options
     NS_AVAILABLE(10_4,9_0);
 
-+ (CIContext *)contextWithOptions:(nullable CI_DICTIONARY(NSString*,id) *)options
-    NS_AVAILABLE(10_11,5_0);
 
+#pragma mark - context without specifying a destination
+
+/* Create a context without specifying a destination CG/GL/Metal context.
+ *
+ * Core Image will use an internal destination context when methods such
+ * as [context render:to...] or [context createCGImage:...] are called.
+ *
+ * The [context drawImage:...] render methods will not operate on this type
+ * of context.
+ */
+
++ (CIContext *)contextWithOptions:(nullable NSDictionary<NSString*,id> *)options
+    NS_AVAILABLE(10_4,5_0);
+
++ (CIContext *)context NS_AVAILABLE(10_4,5_0);
+
+- (instancetype)initWithOptions:(nullable NSDictionary<NSString*,id> *)options
+NS_AVAILABLE(10_4,5_0);
+
+- (instancetype)init NS_AVAILABLE(10_4,5_0);
+
+
+#pragma mark - contextWithEAGLContext
+
+/* Create a context specifying a destination EAGLContext.
+ *
+ * Core Image will use an internal destination context when methods such
+ * as [context render:to...] or [context createCGImage:...] are called.
+ *
+ * The [context drawImage:...] render methods will render to the EAGLContext.
+ */
 #if TARGET_OS_IPHONE
-/* Create a new CoreImage context object using 'eaglContext' 
- * Calls to drawImage:atPoint:fromRect: and drawImage:inRect:fromRect:
- * will draw directly though the context. */
 + (CIContext *)contextWithEAGLContext:(EAGLContext *)eaglContext
     NS_AVAILABLE_IOS(5_0);
 
 + (CIContext *)contextWithEAGLContext:(EAGLContext *)eaglContext
-                              options:(nullable CI_DICTIONARY(NSString*,id) *)options
+                              options:(nullable NSDictionary<NSString*,id> *)options
     NS_AVAILABLE_IOS(5_0);
 #endif
 
+
+#pragma mark - contextWithMTLDevice
+
 /* If a system has more than one MTLDevice, then you can create a CIContext
  * that uses a specific device. If a client wishes to use the default MTLDevice
  * then call [CIContext contextWithOptions:] instead. */
 + (CIContext *)contextWithMTLDevice:(id<MTLDevice>)device NS_AVAILABLE(10_11,9_0);
 
 + (CIContext *)contextWithMTLDevice:(id<MTLDevice>)device
-                            options:(nullable CI_DICTIONARY(NSString*,id) *)options
+                            options:(nullable NSDictionary<NSString*,id> *)options
     NS_AVAILABLE(10_11,9_0);
 
+
+#pragma mark - properties
+
 // The working color space of the CIContext
+// The property will be null if the context was created with color management disabled.
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH) && SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH >= 2)
+@property (nullable, nonatomic, readonly) CGColorSpaceRef workingColorSpace NS_AVAILABLE(10_11,9_0);
+#else
 @property (nonatomic, readonly) CGColorSpaceRef workingColorSpace NS_AVAILABLE(10_11,9_0);
+#endif
+
+// The working pixel format of the CIContext used for intermediate buffers
+@property (nonatomic, readonly) CIFormat workingFormat NS_AVAILABLE(10_11,9_0);
+
 
+#pragma mark - render methods
 
 /* DEPRECATED, please use drawImage:inRect:fromRect: instead.
  * Render the subregion 'fromRect' of 'image' to point 'atPoint' in the context's destination. */
@@ -138,27 +191,76 @@
 
 /* Render the region 'fromRect' of image 'image' into a temporary buffer using
  * the context, then create and return a new CoreGraphics image with
- * the results. The caller is responsible for releasing the returned
- * image. */
+ * the results. The caller is responsible for releasing the returned image.
+ * The return value will be null if size is empty or too big. */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH) && SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH >= 2)
+- (nullable CGImageRef)createCGImage:(CIImage *)image
+                            fromRect:(CGRect)fromRect
+CF_RETURNS_RETAINED;
+#else
 - (CGImageRef)createCGImage:(CIImage *)image
                    fromRect:(CGRect)fromRect
 CF_RETURNS_RETAINED;
+#endif
 
 /* Create a new CGImage from the specified subrect of the image. If
- * non-nil the new image will be created in the specified format and
- * colorspace. */
+ * non-nil the new image will be created in the specified format and colorspace.
+ * The CGColorSpace must be kCGColorSpaceModelRGB or kCGColorSpaceModelMonochrome
+ * and must match the specified CIFormat.
+ * This will return null if fromRect is empty or infinite or the format isn't supported.
+ */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH) && SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH >= 2)
+- (nullable CGImageRef)createCGImage:(CIImage *)image
+                            fromRect:(CGRect)fromRect
+                              format:(CIFormat)format
+                          colorSpace:(nullable CGColorSpaceRef)colorSpace
+CF_RETURNS_RETAINED;
+#else
 - (CGImageRef)createCGImage:(CIImage *)image
                    fromRect:(CGRect)fromRect
                      format:(CIFormat)format
                  colorSpace:(nullable CGColorSpaceRef)colorSpace
 CF_RETURNS_RETAINED;
+#endif
+
+/* Create a new CGImage from the specified subrect of the image.
+ * The new CGImageRef will be created in the specified format and colorspace.
+ * The return value will be null if fromRect is empty or infinite.
+ * The CGColorSpace must be kCGColorSpaceModelRGB or kCGColorSpaceModelMonochrome
+ * and must match the specified CIFormat.
+ * This will return null if fromRect is empty or infinite or the format isn't supported.
+ * If deferred is NO, then the CIImage will be rendered once when this method is called.
+ * If deferred is YES, then the CIImage will be rendered whenever the CGImage is rendered.
+ */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH) && SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH >= 2)
+- (nullable CGImageRef)createCGImage:(CIImage *)image
+                            fromRect:(CGRect)fromRect
+                              format:(CIFormat)format
+                          colorSpace:(nullable CGColorSpaceRef)colorSpace
+                            deferred:(BOOL)deferred
+CF_RETURNS_RETAINED NS_AVAILABLE(10_12,10_0);
+#else
+- (CGImageRef)createCGImage:(CIImage *)image
+                   fromRect:(CGRect)fromRect
+                     format:(CIFormat)format
+                 colorSpace:(nullable CGColorSpaceRef)colorSpace
+                   deferred:(BOOL)deferred
+CF_RETURNS_RETAINED NS_AVAILABLE(10_12,10_0);
+#endif
 
 /* Create a CoreGraphics layer object suitable for creating content for
  * subsequently rendering into this CI context. The 'info' parameter is
- * passed into CGLayerCreate () as the auxiliaryInfo dictionary. */
+ * passed into CGLayerCreate () as the auxiliaryInfo dictionary.
+ * This will return null if size is empty or infinite. */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH) && SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH >= 2)
+- (nullable CGLayerRef)createCGLayerWithSize:(CGSize)size
+                                        info:(nullable CFDictionaryRef)info
+CF_RETURNS_RETAINED NS_DEPRECATED_MAC(10_4,10_11);
+#else
 - (CGLayerRef)createCGLayerWithSize:(CGSize)size
                                info:(nullable CFDictionaryRef)info
 CF_RETURNS_RETAINED NS_DEPRECATED_MAC(10_4,10_11);
+#endif
 
 /* Render 'image' to the given bitmap.
  * Passing a 'colorSpace' value of null means:
@@ -209,14 +311,18 @@
         bounds:(CGRect)bounds
     colorSpace:(nullable CGColorSpaceRef)colorSpace NS_AVAILABLE(10_11,5_0);
 
-/* Render 'bounds' of 'image' to a Metal texture
- * optionally specifying what command buffer to use. */
+/* Render 'bounds' of 'image' to a Metal texture, optionally specifying what command buffer to use.
+ * Texture type must be MTLTexture2D.
+ */
 - (void)render:(CIImage *)image
   toMTLTexture:(id<MTLTexture>)texture
  commandBuffer:(nullable id<MTLCommandBuffer>)commandBuffer
         bounds:(CGRect)bounds
     colorSpace:(CGColorSpaceRef)colorSpace NS_AVAILABLE(10_11,9_0);
 
+
+#pragma mark -
+
 /* Runs the context's garbage collector to reclaim any resources that
  * are no longer required (e.g. removes textures from the texture cache
  * that reference deleted images.) This method is called automatically
@@ -225,14 +331,14 @@
 
 /* Frees any cached data (such as temporary images) associated with the
  * context. This also runs the garbage collector. */
-- (void)clearCaches NS_AVAILABLE_MAC(10_4);
+- (void)clearCaches NS_AVAILABLE(10_4,10_0);
 
 /* Returns the maximum dimension for input images that can be processed 
- * on the currect context. */
+ * on the context. */
 - (CGSize)inputImageMaximumSize NS_AVAILABLE_IOS(5_0);
 
 /* Returns the maximum dimension for image that can be rendered 
- * on the currect context. */
+ * on the context. */
 - (CGSize)outputImageMaximumSize NS_AVAILABLE_IOS(5_0);
 
 @end
@@ -248,20 +354,67 @@
 /* These two methods lets you create a CIContext based on an offline gpu index.
  * The first method takes only the GPU index as a parameter, the second, takes
  * an optional colorspace, options dictionary and a CGLContext which can be
- * shared with other GL resources.
+ * shared with other GL resources.  The return value will be null if index is 
+ * out of range (e.g. if the device has no offline GPUs).
  */
 #if !TARGET_OS_IPHONE
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH) && SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH >= 2)
++ (nullable CIContext *)contextForOfflineGPUAtIndex:(unsigned int)index NS_AVAILABLE_MAC(10_10);
++ (nullable CIContext *)contextForOfflineGPUAtIndex:(unsigned int)index
+                                         colorSpace:(nullable CGColorSpaceRef)colorSpace
+                                            options:(nullable NSDictionary<NSString*,id> *)options
+                                      sharedContext:(nullable CGLContextObj)sharedContext NS_AVAILABLE_MAC(10_10);
+#else
 +(CIContext *)contextForOfflineGPUAtIndex:(unsigned int)index NS_AVAILABLE_MAC(10_10);
 +(CIContext *)contextForOfflineGPUAtIndex:(unsigned int)index
                                colorSpace:(nullable CGColorSpaceRef)colorSpace
-                                  options:(nullable CI_DICTIONARY(NSString*,id) *)options
+                                  options:(nullable NSDictionary<NSString*,id> *)options
                             sharedContext:(nullable CGLContextObj)sharedContext NS_AVAILABLE_MAC(10_10);
 #endif
+#endif
 
 
 @end
 
-#undef CI_DICTIONARY
-#undef CI_ARRAY
+@interface CIContext (ImageRepresentation)
+
+/* Render a CIImage to TIFF data. Image must have a finite non-empty extent. */
+/* The CGColorSpace must be kCGColorSpaceModelRGB or kCGColorSpaceModelMonochrome */
+/* and must match the specified CIFormat. */
+/* No options keys are supported at this time. */
+- (nullable NSData*) TIFFRepresentationOfImage:(CIImage*)image
+                                        format:(CIFormat)format
+                                    colorSpace:(CGColorSpaceRef)colorSpace
+                                       options:(NSDictionary*)options NS_AVAILABLE(10_12,10_0);
+
+/* Render a CIImage to JPEG data. Image must have a finite non-empty extent. */
+/* The CGColorSpace must be kCGColorSpaceModelRGB or kCGColorSpaceModelMonochrome. */
+/* Supported options keys are kCGImageDestinationLossyCompressionQuality */
+- (nullable NSData*) JPEGRepresentationOfImage:(CIImage*)image
+                                    colorSpace:(CGColorSpaceRef)colorSpace
+                                       options:(NSDictionary*)options NS_AVAILABLE(10_12,10_0);
+
+/* Render a CIImage to TIFF file. Image must have a finite non-empty extent. */
+/* The CGColorSpace must be kCGColorSpaceModelRGB or kCGColorSpaceModelMonochrome */
+/* and must match the specified CIFormat. */
+/* No options keys are supported at this time. */
+- (BOOL) writeTIFFRepresentationOfImage:(CIImage*)image
+                                  toURL:(NSURL*)url
+                                 format:(CIFormat)format
+                             colorSpace:(CGColorSpaceRef)colorSpace 
+                                options:(NSDictionary*)options
+                                  error:(NSError **)errorPtr NS_AVAILABLE(10_12,10_0);
+
+/* Render a CIImage to JPEG file. Image must have a finite non-empty extent. */
+/* The CGColorSpace must be kCGColorSpaceModelRGB or kCGColorSpaceModelMonochrome. */
+/* Supported options keys are kCGImageDestinationLossyCompressionQuality */
+- (BOOL) writeJPEGRepresentationOfImage:(CIImage*)image
+                                  toURL:(NSURL*)url
+                             colorSpace:(CGColorSpaceRef)colorSpace
+                                options:(NSDictionary*)options
+                                  error:(NSError **)errorPtr NS_AVAILABLE(10_12,10_0);
+
+
+@end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIDetector.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIDetector.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIDetector.h	2015-08-25 05:35:43.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIDetector.h	2016-05-21 08:27:44.000000000 +0200
@@ -9,53 +9,51 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-#if __has_feature(objc_generics)
-# define CI_DICTIONARY(KeyType, ValueType) NSDictionary<KeyType, ValueType>
-# define CI_ARRAY(ValueType) NSArray <ValueType>
-#else
-# define CI_DICTIONARY(KeyType, ValueType) NSDictionary
-# define CI_ARRAY(ValueType) NSArray
-#endif
-
-
 @class CIImage;
 @class CIContext;
 @class CIFeature;
 
-
 /** Detects features in images.
- 
+
  This class potentially holds onto a lot of state. Hence it may be beneficial from a performance perspective to re-use the same CIDetector instance. Specifying a CIContext when creating a detector may have an impact on performance since this context may be used when analyzing an image.
  */
 NS_CLASS_AVAILABLE(10_7, 5_0)
 @interface CIDetector : NSObject {}
 
 /** Returns a new detector instance of the given type.
- 
- The type is used to specify the usage intent.
- 
+
+ The type is used to specify the detection intent.
+ This will return value if the detector type is not supported.
+
  The context argument specifies the CIContext to be used to operate on the image. May be nil.
- 
+
  If the input image to -featuresInImage: is the output of a CoreImage operation, it may improve performance to specify the same context that was used to operate on that image.
- 
+
  The detector may do image processing in this context and if the image is on the GPU and the specified context is a GPU context this may avoid additional upload to / download from the GPU. If the input image is on the CPU (or the output from a CPU based context) specifying a GPU based context (or vice versa) may reduce performance.
- 
+
  The options parameter lets you optinally specify a accuracy / performance tradeoff. Can be nil or an empty dictionary. */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH) && SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH >= 2)
++ (nullable CIDetector *)detectorOfType:(NSString*)type
+                                context:(nullable CIContext *)context
+                                options:(nullable NSDictionary<NSString *,id> *)options
+    NS_AVAILABLE(10_7, 5_0);
+#else
 + (CIDetector *)detectorOfType:(NSString*)type
-                       context:(nullable CIContext *)context
-                       options:(nullable CI_DICTIONARY(NSString*,id) *)options
+                      context:(nullable CIContext *)context
+                      options:(nullable NSDictionary<NSString *,id> *)options
     NS_AVAILABLE(10_7, 5_0);
+#endif
 
 /** Returns an array of CIFeature instances in the given image.
  The array is sorted by confidence, highest confidence first. */
-- (CI_ARRAY(CIFeature*) *)featuresInImage:(CIImage *)image
+- (NSArray<CIFeature *> *)featuresInImage:(CIImage *)image
     NS_AVAILABLE(10_7, 5_0);
 
 /** Returns an array of CIFeature instances in the given image.
- The array is sorted by confidence, highest confidence first. 
+ The array is sorted by confidence, highest confidence first.
  The options dictionary can contain a CIDetectorImageOrientation key value. */
-- (CI_ARRAY(CIFeature*) *)featuresInImage:(CIImage *)image
-                                  options:(nullable CI_DICTIONARY(NSString*,id) *)options
+- (NSArray<CIFeature *> *)featuresInImage:(CIImage *)image
+                                  options:(nullable NSDictionary<NSString *,id> *)options
     NS_AVAILABLE(10_8, 5_0);
 
 @end
@@ -92,11 +90,11 @@
 /*The key in the options dictionary used to specify that feature tracking should be used. */
 CORE_IMAGE_EXPORT NSString* const CIDetectorTracking NS_AVAILABLE(10_8, 6_0);
 
-/* The key in the options dictionary used to specify the minimum size that the 
+/* The key in the options dictionary used to specify the minimum size that the
  detector will recognize as a feature. */
 
 /* For face detector, the value for this key is an float NSNumber
- from 0.0 ... 1.0 that represents a percentage of shorter edge of an input image. 
+ from 0.0 ... 1.0 that represents a percentage of shorter edge of an input image.
  valid values range: 0.01 <= CIDetectorMinFeatureSize <= 0.5.
  Setting a higher value for this parameter is used for performance gain only. The default value is 0.15. */
 
@@ -138,9 +136,4 @@
 CORE_IMAGE_EXPORT NSString* const CIDetectorReturnSubFeatures __OSX_AVAILABLE_STARTING(__MAC_10_11, __IPHONE_9_0);
 #endif
 
-
-
-#undef CI_DICTIONARY
-#undef CI_ARRAY
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIFeature.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIFeature.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIFeature.h	2015-08-25 05:35:43.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIFeature.h	2016-05-21 07:51:21.000000000 +0200
@@ -125,7 +125,11 @@
 @property (readonly) CGPoint topRight;
 @property (readonly) CGPoint bottomLeft;
 @property (readonly) CGPoint bottomRight;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH) && SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH >= 2)
+@property (nullable, readonly) NSString* messageString;
+#else
 @property (readonly) NSString* messageString;
+#endif
 
 
 @end
@@ -144,7 +148,11 @@
 @property (readonly) CGPoint topRight;
 @property (readonly) CGPoint bottomLeft;
 @property (readonly) CGPoint bottomRight;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH) && SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH >= 2)
+@property (nullable, readonly) NSArray *subFeatures;
+#else
 @property (readonly) NSArray *subFeatures;
+#endif
 
 
 @end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIFilter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIFilter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIFilter.h	2015-08-25 05:35:43.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIFilter.h	2016-05-21 08:27:44.000000000 +0200
@@ -1,4 +1,4 @@
-/* 
+/*
    CoreImage - CIFilter.h
 
    Copyright (c) 2015 Apple, Inc.
@@ -12,14 +12,6 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-#if __has_feature(objc_generics)
-# define CI_DICTIONARY(KeyType, ValueType) NSDictionary<KeyType, ValueType>
-# define CI_ARRAY(ValueType) NSArray <ValueType>
-#else
-# define CI_DICTIONARY(KeyType, ValueType) NSDictionary
-# define CI_ARRAY(ValueType) NSArray
-#endif
-
 /* Filter attributes keys */
 
 /** Name of the filter */
@@ -155,7 +147,7 @@
 CORE_IMAGE_EXPORT NSString * const kCIApplyOptionUserInfo NS_AVAILABLE_MAC(10_4);
 
 /* If used, the value of the kCIApplyOptionColorSpace key be must be an RGB CGColorSpaceRef.
- * Using this option specifies that the output of the kernel is in this color space. 
+ * Using this option specifies that the output of the kernel is in this color space.
  * If not specified, the output of the kernel is in the working color space of the rendering CIContext. */
 CORE_IMAGE_EXPORT NSString * const kCIApplyOptionColorSpace NS_AVAILABLE_MAC(10_4);
 
@@ -195,7 +187,7 @@
 @protocol CIFilterConstructor;
 
 /** CIFilter are filter objects for Core Image that encapsulate the filter with its attributes
- 
+
  The CIFilter class produces a CIImage object as output. Typically, a filter takes one or more images as input. Some filters, however, generate an image based on other types of input parameters. The parameters of a CIFilter object are set and retrieved through the use of key-value pairs. You use the CIFilter object in conjunction with the CIImage, CIContext, CIVector, CIImageAccumulator, and CIColor objects to take advantage of the built-in Core Image filters when processing images. CIFilter objects are also used along with CIKernel, CISampler, and CIFilterShape objects to create custom filters. */
 
 NS_CLASS_AVAILABLE(10_4, 5_0)
@@ -206,39 +198,36 @@
 
 @property (readonly, nonatomic, nullable) CIImage *outputImage NS_AVAILABLE(10_10, 5_0);
 
-/* name of the filter */
-#if TARGET_OS_IPHONE
-@property (nonatomic, readonly) NSString *name NS_AVAILABLE_IOS(5_0);
-#else
-/* On OSX this property is read-write.  This can be useful when
- * using CIFilters with CALayers to construct unique keypaths.
+/* The name of the filter. On OSX and iOS 10, this property is read-write.
+ * This can be useful when using CIFilters with CoreAnimation or SceneKit.
  * For example, to set an attribute of a filter attached to a layer,
- * a path such as "filters.myExposureFilter.inputEV" could be used. 
+ * a unique path such as "filters.myExposureFilter.inputEV" could be used.
  * CALayer animations may also access filter attributes via key-paths. */
-@property (nonatomic, copy) NSString *name NS_AVAILABLE_MAC(10_5);
+@property (nonatomic, copy) NSString *name;
+- (NSString *)name NS_AVAILABLE(10_5,5_0);
+- (void)setName:(NSString *)aString NS_AVAILABLE(10_5,10_0);
 
 /* The 'enabled' property is used only by CoreAnimation and is animatable.
- * In Core Animation, a CIFilter only applied to its input when this 
+ * In Core Animation, a CIFilter only applied to its input when this
  * property is set to true. */
 @property (getter=isEnabled) BOOL enabled NS_AVAILABLE_MAC(10_5);
-#endif
 
 
 /** Returns an array containing the names of all inputs in the filter. */
-@property (nonatomic, readonly) CI_ARRAY(NSString*) *inputKeys;
+@property (nonatomic, readonly) NSArray<NSString *> *inputKeys;
 
 /** Returns an array containing the names of all outputs in the filter. */
-@property (nonatomic, readonly) CI_ARRAY(NSString*) *outputKeys;
+@property (nonatomic, readonly) NSArray<NSString *> *outputKeys;
 
 /** Sets all inputs to their default values (where default values are defined, other inputs are left as-is). */
 - (void)setDefaults;
 
 /** Returns a dictionary containing key/value pairs describing the filter. (see description of keys below) */
-@property (nonatomic, readonly) CI_DICTIONARY(NSString*,id) *attributes;
+@property (nonatomic, readonly) NSDictionary<NSString *,id> *attributes;
 
 
 /** Used by CIFilter subclasses to apply the array of argument values 'args' to the kernel function 'k'. The supplied arguments must be type-compatible with the function signature of the kernel.
- 
+
  The key-value pairs defined by 'dict' (if non-nil) are used to control exactly how the kernel is evaluated. Valid keys include:
  kCIApplyOptionExtent: the size of the produced image. Value is a four element NSArray [X Y WIDTH HEIGHT].
  kCIApplyOptionDefinition: the Domain of Definition of the produced image. Value is either a CIFilterShape object, or a four element NSArray defining a rectangle.
@@ -248,7 +237,7 @@
 */
 - (nullable CIImage *)apply:(CIKernel *)k
 				  arguments:(nullable NSArray *)args
-			        options:(nullable CI_DICTIONARY(NSString*,id) *)dict NS_AVAILABLE_MAC(10_4);
+			        options:(nullable NSDictionary<NSString *,id> *)dict NS_AVAILABLE_MAC(10_4);
 
 /** Similar to above except that all argument values and option key-value are specified inline. The list of key-value pairs must be terminated by the 'nil' object. */
 - (nullable CIImage *)apply:(CIKernel *)k, ... NS_REQUIRES_NIL_TERMINATION NS_AVAILABLE_MAC(10_4) NS_SWIFT_UNAVAILABLE("");
@@ -260,7 +249,7 @@
  Use these methods to create filters and find filters. */
 @interface CIFilter (CIFilterRegistry)
 
-/** Creates a new filter of type 'name'. 
+/** Creates a new filter of type 'name'.
  On OSX, all input values will be undefined.
  On iOS, all input values will be set to default values. */
 + (nullable CIFilter *) filterWithName:(NSString *) name;
@@ -277,25 +266,25 @@
  On OSX, any of the filter input parameters not specified in the dictionary will be undefined.
  On iOS, any of the filter input parameters not specified in the dictionary will be set to default values. */
 + (nullable CIFilter *)filterWithName:(NSString *)name
-                  withInputParameters:(nullable CI_DICTIONARY(NSString*,id) *)params NS_AVAILABLE(10_10, 8_0);
+                  withInputParameters:(nullable NSDictionary<NSString *,id> *)params NS_AVAILABLE(10_10, 8_0);
 
 /** Returns an array containing all published filter names in a category. */
-+ (CI_ARRAY(NSString*) *)filterNamesInCategory:(nullable NSString *)category;
++ (NSArray<NSString *> *)filterNamesInCategory:(nullable NSString *)category;
 
 /** Returns an array containing all published filter names that belong to all listed categories. */
-+ (CI_ARRAY(NSString*) *)filterNamesInCategories:(nullable CI_ARRAY(NSString*) *)categories;
++ (NSArray<NSString *> *)filterNamesInCategories:(nullable NSArray<NSString *> *)categories;
 
 
 /** Publishes a new filter called 'name'.
- 
+
  The constructor object 'anObject' should implement the filterWithName: method.
  That method will be invoked with the name of the filter to create.
  The class attributes must have a kCIAttributeFilterCategories key associated with a set of categories.
  @param   attributes    Dictionary of the registration attributes of the filter. See below for attribute keys.
 */
 + (void)registerFilterName:(NSString *)name
-			   constructor:(id<CIFilterConstructor>)anObject
-		   classAttributes:(CI_DICTIONARY(NSString*,id) *)attributes NS_AVAILABLE(10_4, 9_0);
+               constructor:(id<CIFilterConstructor>)anObject
+           classAttributes:(NSDictionary<NSString *,id> *)attributes NS_AVAILABLE(10_4, 9_0);
 
 /** Returns the localized name of a filter for display in the UI. */
 + (nullable NSString *)localizedNameForFilterName:(NSString *)filterName NS_AVAILABLE(10_4, 9_0);
@@ -307,7 +296,7 @@
 + (nullable NSString *)localizedDescriptionForFilterName:(NSString *)filterName NS_AVAILABLE(10_4, 9_0);
 
 /** Returns the URL to the localized reference documentation describing the filter.
-    
+
  The URL can be a local file or a remote document on a webserver. It is possible, that this method returns nil (like filters that predate this feature). A client of this API has to handle this case gracefully. */
 + (nullable NSURL *)localizedReferenceDocumentationForFilterName:(NSString *)filterName NS_AVAILABLE(10_4, 9_0);
 
@@ -317,27 +306,31 @@
 /** Methods to serialize arrays of filters to xmp. */
 @interface CIFilter (CIFilterXMPSerialization)
 
-/* Given an array of filters, serialize the filters' parameters 
+/* Given an array of filters, serialize the filters' parameters
    into XMP form that is suitable for embedding in to an image.
    At this time the only filters classes that are serialized
-   are, CIAffineTransform, CICrop, and the filters returned by 
-   [CIImage autoAdjustmentFilters].  
+   are, CIAffineTransform, CICrop, and the filters returned by
+   [CIImage autoAdjustmentFilters].
    The parameters of other filter classes will not be serialized.
+   The return value will be null if none of the filters can be serialized.
  */
-+ (NSData*)serializedXMPFromFilters:(CI_ARRAY(CIFilter*) *)filters
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH) && SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH >= 2)
++ (nullable NSData*)serializedXMPFromFilters:(NSArray<CIFilter *> *)filters
+                            inputImageExtent:(CGRect)extent
+    NS_AVAILABLE(10_9, 6_0);
+#else
++ (NSData*)serializedXMPFromFilters:(NSArray<CIFilter *> *)filters
                    inputImageExtent:(CGRect)extent
     NS_AVAILABLE(10_9, 6_0);
+#endif
 
 /* Return an array of CIFilters de-serialized from XMP data.
  */
-+ (CI_ARRAY(CIFilter*) *)filterArrayFromSerializedXMP:(NSData *)xmpData
-                                      inputImageExtent:(CGRect)extent
-                                                 error:(NSError **)outError
++ (NSArray<CIFilter *> *)filterArrayFromSerializedXMP:(NSData *)xmpData
+                                     inputImageExtent:(CGRect)extent
+                                                error:(NSError **)outError
     NS_AVAILABLE(10_9, 6_0);
 
 @end
 
-#undef CI_DICTIONARY
-#undef CI_ARRAY
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImage.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImage.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImage.h	2015-08-25 05:35:43.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImage.h	2016-05-21 08:27:44.000000000 +0200
@@ -1,8 +1,8 @@
-/* 
+/*
    CoreImage - CIImage.h
 
    Copyright (c) 2015 Apple, Inc.
-   All rights reserved. 
+   All rights reserved.
 */
 
 #import <Foundation/Foundation.h>
@@ -14,14 +14,6 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-#if __has_feature(objc_generics)
-# define CI_DICTIONARY(KeyType, ValueType) NSDictionary<KeyType, ValueType>
-# define CI_ARRAY(ValueType) NSArray <ValueType>
-#else
-# define CI_DICTIONARY(KeyType, ValueType) NSDictionary
-# define CI_ARRAY(ValueType) NSArray
-#endif
-
 @class CIContext, CIFilterShape, CIColor, CIFilter;
 
 @protocol MTLTexture;
@@ -67,15 +59,15 @@
 CORE_IMAGE_EXPORT CIFormat kCIFormatRGf NS_AVAILABLE(10_11, 9_0);
 
 
-/* Image options dictionary keys. 
+/* Image options dictionary keys.
    These keys can be passed with appropriate values to the methods:
      + [CIImage imageWith... options:]
      - [CIImage initWith... options:]
    to modify the default behavior of how CIImages are created.
 */
 
-/* A CGColorSpaceRef defining the color space of the image. This value 
- * overrides the image's implicit color space. 
+/* A CGColorSpaceRef defining the color space of the image. This value
+ * overrides the image's implicit color space.
  * If [NSNull null] then dont color manage the image. */
 CORE_IMAGE_EXPORT NSString * const kCIImageColorSpace;
 
@@ -94,12 +86,12 @@
 /* Creates a new image from the contents of 'image'. */
 + (CIImage *)imageWithCGImage:(CGImageRef)image;
 + (CIImage *)imageWithCGImage:(CGImageRef)image
-                      options:(nullable CI_DICTIONARY(NSString*,id) *)options;
+                      options:(nullable NSDictionary<NSString *,id> *)options;
 
 /* Creates a new image from the contents of 'layer'. */
 + (CIImage *)imageWithCGLayer:(CGLayerRef)layer NS_DEPRECATED_MAC(10_4,10_11);
 + (CIImage *)imageWithCGLayer:(CGLayerRef)layer
-                      options:(nullable CI_DICTIONARY(NSString*,id) *)options NS_DEPRECATED_MAC(10_4,10_11);
+                      options:(nullable NSDictionary<NSString *,id> *)options NS_DEPRECATED_MAC(10_4,10_11);
 
 /* Creates a new image whose bitmap data is from 'data'. Each row contains 'bytesPerRow'
  * bytes. The dimensions of the image are defined by 'size'. 'format' defines
@@ -128,35 +120,41 @@
  */
 + (CIImage *)imageWithTexture:(unsigned int)name
                          size:(CGSize)size
-					  flipped:(BOOL)flipped
-                      options:(nullable CI_DICTIONARY(NSString*,id) *)options NS_AVAILABLE_MAC(10_9);
+                      flipped:(BOOL)flipped
+                      options:(nullable NSDictionary<NSString *,id> *)options NS_AVAILABLE_MAC(10_9);
 
+// imageWithMTLTexture will return nil if textureType is not MTLTextureType2D.
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH) && SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH >= 2)
++ (nullable CIImage *)imageWithMTLTexture:(id<MTLTexture>)texture
+                                  options:(nullable NSDictionary<NSString *,id> *)options NS_AVAILABLE(10_11, 9_0);
+#else
 + (CIImage *)imageWithMTLTexture:(id<MTLTexture>)texture
-                         options:(nullable CI_DICTIONARY(NSString*,id) *)options NS_AVAILABLE(10_11, 9_0);
+                         options:(nullable NSDictionary<NSString *,id> *)options NS_AVAILABLE(10_11, 9_0);
+#endif
 
 + (nullable CIImage *)imageWithContentsOfURL:(NSURL *)url;
 + (nullable CIImage *)imageWithContentsOfURL:(NSURL *)url
-                                     options:(nullable CI_DICTIONARY(NSString*,id) *)options;
+                                     options:(nullable NSDictionary<NSString *,id> *)options;
 
 + (nullable CIImage *)imageWithData:(NSData *)data;
 + (nullable CIImage *)imageWithData:(NSData *)data
-                            options:(nullable CI_DICTIONARY(NSString*,id) *)options;
+                            options:(nullable NSDictionary<NSString *,id> *)options;
 
 /* Creates a new image whose data is from the contents of a CVImageBuffer. */
 + (CIImage *)imageWithCVImageBuffer:(CVImageBufferRef)imageBuffer NS_AVAILABLE(10_4, 9_0);
 + (CIImage *)imageWithCVImageBuffer:(CVImageBufferRef)imageBuffer
-                            options:(nullable CI_DICTIONARY(NSString*,id) *)options NS_AVAILABLE(10_4, 9_0);
+                            options:(nullable NSDictionary<NSString *,id> *)options NS_AVAILABLE(10_4, 9_0);
 
 /* Creates a new image whose data is from the contents of a CVPixelBufferRef. */
 + (CIImage *)imageWithCVPixelBuffer:(CVPixelBufferRef)pixelBuffer NS_AVAILABLE(10_11, 5_0);
 + (CIImage *)imageWithCVPixelBuffer:(CVPixelBufferRef)pixelBuffer
-                            options:(nullable CI_DICTIONARY(NSString*,id) *)options NS_AVAILABLE(10_11, 5_0);
+                            options:(nullable NSDictionary<NSString *,id> *)options NS_AVAILABLE(10_11, 5_0);
 
 /* Creates a new image from the contents of an IOSurface. */
 #if !TARGET_OS_IPHONE
 + (CIImage *)imageWithIOSurface:(IOSurfaceRef)surface NS_AVAILABLE_MAC(10_6);
 + (CIImage *)imageWithIOSurface:(IOSurfaceRef)surface
-                        options:(nullable CI_DICTIONARY(NSString*,id) *)options NS_AVAILABLE_MAC(10_6);
+                        options:(nullable NSDictionary<NSString *,id> *)options NS_AVAILABLE_MAC(10_6);
 #endif
 
 /* Return or initialize a new image with an infinite amount of the color
@@ -170,17 +168,17 @@
 
 - (instancetype)initWithCGImage:(CGImageRef)image;
 - (instancetype)initWithCGImage:(CGImageRef)image
-                        options:(nullable CI_DICTIONARY(NSString*,id) *)options;
+                        options:(nullable NSDictionary<NSString *,id> *)options;
 
 - (instancetype)initWithCGLayer:(CGLayerRef)layer
     NS_DEPRECATED_MAC(10_4,10_11,"Use initWithCGImage: instead.");
 - (instancetype)initWithCGLayer:(CGLayerRef)layer
-                        options:(nullable CI_DICTIONARY(NSString*,id) *)options
+                        options:(nullable NSDictionary<NSString *,id> *)options
     NS_DEPRECATED_MAC(10_4,10_11,"Use initWithCGImage:options instead.");
 
 - (nullable instancetype)initWithData:(NSData *)data;
 - (nullable instancetype)initWithData:(NSData *)data
-                              options:(nullable CI_DICTIONARY(NSString*,id) *)options;
+                              options:(nullable NSDictionary<NSString *,id> *)options;
 
 - (instancetype)initWithBitmapData:(NSData *)data
                        bytesPerRow:(size_t)bytesPerRow
@@ -196,34 +194,40 @@
 - (instancetype)initWithTexture:(unsigned int)name
                            size:(CGSize)size
                         flipped:(BOOL)flipped
-                        options:(nullable CI_DICTIONARY(NSString*,id) *)options NS_AVAILABLE_MAC(10_9);
+                        options:(nullable NSDictionary<NSString *,id> *)options NS_AVAILABLE_MAC(10_9);
 
+// initWithMTLTexture will return nil if textureType is not MTLTextureType2D.
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH) && SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH >= 2)
+- (nullable instancetype)initWithMTLTexture:(id<MTLTexture>)texture
+                                    options:(nullable NSDictionary<NSString *,id> *)options NS_AVAILABLE(10_11, 9_0);
+#else
 - (instancetype)initWithMTLTexture:(id<MTLTexture>)texture
-                           options:(nullable CI_DICTIONARY(NSString*,id) *)options NS_AVAILABLE(10_11, 9_0);
+                           options:(nullable NSDictionary<NSString *,id> *)options NS_AVAILABLE(10_11, 9_0);
+#endif
 
 - (nullable instancetype)initWithContentsOfURL:(NSURL *)url;
 - (nullable instancetype)initWithContentsOfURL:(NSURL *)url
-                                       options:(nullable CI_DICTIONARY(NSString*,id) *)options;
+                                       options:(nullable NSDictionary<NSString *,id> *)options;
 
 #if !TARGET_OS_IPHONE
 - (instancetype)initWithIOSurface:(IOSurfaceRef)surface NS_AVAILABLE_MAC(10_6);
 
 - (instancetype)initWithIOSurface:(IOSurfaceRef)surface
-                          options:(nullable CI_DICTIONARY(NSString*,id) *)options NS_AVAILABLE_MAC(10_6);
+                          options:(nullable NSDictionary<NSString *,id> *)options NS_AVAILABLE_MAC(10_6);
 
 - (instancetype)initWithIOSurface:(IOSurfaceRef)surface
                             plane:(size_t)plane
                            format:(CIFormat)format
-                          options:(nullable CI_DICTIONARY(NSString*,id) *)options NS_DEPRECATED_MAC(10_9,10_11);
+                          options:(nullable NSDictionary<NSString *,id> *)options NS_DEPRECATED_MAC(10_9,10_11);
 #endif
 
 - (instancetype)initWithCVImageBuffer:(CVImageBufferRef)imageBuffer NS_AVAILABLE(10_4, 9_0);
 - (instancetype)initWithCVImageBuffer:(CVImageBufferRef)imageBuffer
-                              options:(nullable CI_DICTIONARY(NSString*,id) *)options NS_AVAILABLE(10_4, 9_0);
+                              options:(nullable NSDictionary<NSString *,id> *)options NS_AVAILABLE(10_4, 9_0);
 
 - (instancetype)initWithCVPixelBuffer:(CVPixelBufferRef)pixelBuffer NS_AVAILABLE(10_11, 5_0);
 - (instancetype)initWithCVPixelBuffer:(CVPixelBufferRef)pixelBuffer
-                              options:(nullable CI_DICTIONARY(NSString*,id) *)options NS_AVAILABLE(10_11, 5_0);
+                              options:(nullable NSDictionary<NSString *,id> *)options NS_AVAILABLE(10_11, 5_0);
 
 - (instancetype)initWithColor:(CIColor *)color;
 
@@ -234,29 +238,60 @@
 /* Returns a new image representing the original image with a transform
  * appied to it based on an orientation value.
  * Orientation values from 1 to 8 as defined in the TIFF spec are supported.
+ * See also the CGImagePropertyOrientation type for what the 1 to 8 values do.
  * Returns original image if the image is of infinite extent. */
 - (CIImage *)imageByApplyingOrientation:(int)orientation NS_AVAILABLE(10_10, 8_0);
 
 /* Returns a CGAffineTransform for an orientation value that can be appied to an image.
  * Orientation values from 1 to 8 as defined in the TIFF spec are supported.
+ * See also the CGImagePropertyOrientation type for what the 1 to 8 values do.
  * Returns CGAffineTransformIdentity if the image is of infinite extent.*/
 - (CGAffineTransform)imageTransformForOrientation:(int)orientation NS_AVAILABLE(10_10, 8_0);
 
-/* Return a new image formed by compositing the receiver image over 'dest'. */
+/* Return a new image formed by compositing the receiver image over 'dest'.
+ * This is equivalent to the CISourceOverCompositing filter. */
 - (CIImage *)imageByCompositingOverImage:(CIImage *)dest NS_AVAILABLE(10_4, 8_0);
 
 /* Return a new image cropped to a rectangle. */
 - (CIImage *)imageByCroppingToRect:(CGRect)rect;
 
-/* Return a new infinte image by replicating the pixels of the receiver image's extent. */
+/* Return a new infinite image by replicating the edge pixels of the receiver image. */
 - (CIImage *)imageByClampingToExtent NS_AVAILABLE(10_10, 8_0);
 
+/* Return a new infinite image by replicating the edge pixels of a rectangle.
+ * This is equivalent to the CICrop filter. */
+- (CIImage *)imageByClampingToRect:(CGRect)rect NS_AVAILABLE(10_12, 10_0);
+
 /* A convenience method for applying a filter to an image.
  * The method returns outputImage of the filter after setting the
  * filter's inputImage to the method receiver and other parameters
  * from from the key/value pairs of 'params'. */
 - (CIImage *)imageByApplyingFilter:(NSString *)filterName
-               withInputParameters:(nullable CI_DICTIONARY(NSString*,id) *)params NS_AVAILABLE(10_10, 8_0);
+               withInputParameters:(nullable NSDictionary<NSString *,id> *)params NS_AVAILABLE(10_10, 8_0);
+
+
+/* Return a new image by color matching from the colorSpace to the context's working space.
+ * This method will return nil if the CGColorSpace is not kCGColorSpaceModelRGB. */
+- (nullable CIImage *)imageByColorMatchingColorSpaceToWorkingSpace:(CGColorSpaceRef)colorSpace NS_AVAILABLE(10_12, 10_0);
+
+/* Return a new image by color matching from the context's working space to the colorSpace.
+ * This method will return nil if the CGColorSpace is not kCGColorSpaceModelRGB. */
+- (nullable CIImage *)imageByColorMatchingWorkingSpaceToColorSpace:(CGColorSpaceRef)colorSpace NS_AVAILABLE(10_12, 10_0);
+
+/* Return a new image by multiplying the receiver's RGB values by its alpha. */
+- (CIImage *)imageByPremultiplyingAlpha NS_AVAILABLE(10_12, 10_0);
+
+/* Return a new image by dividing the receiver's RGB values by its alpha. */
+- (CIImage *)imageByUnpremultiplyingAlpha NS_AVAILABLE(10_12, 10_0);
+
+/* Return a new image with alpha set to 1 within the rectangle and 0 outside. */
+- (CIImage *)imageBySettingAlphaOneInExtent:(CGRect)extent NS_AVAILABLE(10_12, 10_0);
+
+/* Return a new image by applying a gaussian blur to the receiver. */
+- (CIImage *)imageByApplyingGaussianBlurWithSigma:(double)sigma NS_AVAILABLE(10_12, 10_0);
+
+/* Return a new image by changing the recevier's properties. */
+- (CIImage *)imageBySettingProperties:(NSDictionary*)properties NS_AVAILABLE(10_12, 10_0);
 
 
 /* Return a rect the defines the bounds of non-(0,0,0,0) pixels */
@@ -265,7 +300,7 @@
 /* Returns the metadata properties of an image. If the image is the
  * output of one or more CIFilters, then the metadata of the root inputImage
  * will be returned. See also kCIImageProperties. */
-@property (atomic, readonly) CI_DICTIONARY(NSString*,id) *properties NS_AVAILABLE(10_8, 5_0);
+@property (atomic, readonly) NSDictionary<NSString *,id> *properties NS_AVAILABLE(10_8, 5_0);
 
 /* Return the Domain of Definition of the image. */
 @property (atomic, readonly) CIFilterShape *definition NS_AVAILABLE_MAC(10_4);
@@ -278,6 +313,15 @@
  * This method will return nil, if the color space cannot be determined. */
 @property (atomic, readonly, nullable) CGColorSpaceRef colorSpace NS_AVAILABLE(10_4, 9_0) CF_RETURNS_NOT_RETAINED;
 
+/* Returns a CVPixelBufferRef if the CIImage was created with [CIImage imageWithCVPixelBuffer] and no options.
+ * Otherwise this property will be nil and calling [CIContext render:toCVPixelBuffer:] is recommended.
+ * Modifying the contents of this pixelBuffer will cause the CIImage to render with undefined results. */
+@property (nonatomic, readonly, nullable) CVPixelBufferRef pixelBuffer NS_AVAILABLE(10_12, 10_0);
+
+/* Returns a CGImageRef if the CIImage was created with [CIImage imageWithCGImage] or [CIImage imageWithURL] and no options.
+ * Otherwise this property will be nil and calling [CIContext createCGImage:fromRect:] is recommended. */
+@property (nonatomic, readonly, nullable) CGImageRef CGImage NS_AVAILABLE(10_12,10_0);
+
 /* Returns the rectangle of 'image' that is required to render the
  * rectangle 'rect' of the receiver.  This may return a null rect. */
 - (CGRect)regionOfInterestForImage:(CIImage *)image
@@ -290,7 +334,7 @@
 
 /* Image auto adjustment keys. */
 
-/* These are the options dictionary keys which can be specified when calling 
+/* These are the options dictionary keys which can be specified when calling
  * the autoAdjustmentFiltersWithOptions: method.
  */
 
@@ -324,18 +368,16 @@
 /* Return an array of filters to apply to an image to improve its
  * skin tones, saturation, contrast, shadows and repair red-eyes or LED-eyes.
  *
- * The options dictionary can contain a CIDetectorImageOrientation key value. 
+ * The options dictionary can contain a CIDetectorImageOrientation key value.
  * The value for this key is an integer NSNumber from 1..8 such as that
  * found in kCGImagePropertyOrientation.  If present, the adjustment will be done
  * based on that orientation but any coordinates in the returned filters will
  * still be based on those of the sender image.
  */
-- (CI_ARRAY(CIFilter *) *)autoAdjustmentFiltersWithOptions:(nullable CI_DICTIONARY(NSString*,id) *)options
+- (NSArray<CIFilter *> *)autoAdjustmentFilters NS_AVAILABLE(10_8, 5_0);
+- (NSArray<CIFilter *> *)autoAdjustmentFiltersWithOptions:(nullable NSDictionary<NSString *,id> *)options
     NS_AVAILABLE(10_8, 5_0);
 
 @end
 
-#undef CI_DICTIONARY
-#undef CI_ARRAY
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImageAccumulator.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImageAccumulator.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImageAccumulator.h	2015-08-25 05:35:43.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImageAccumulator.h	2016-05-21 07:18:49.000000000 +0200
@@ -17,7 +17,26 @@
 /* Create a new accumulator object. 
    For pixel format options see CIImage.h.
    The specified color space is used to render the image. 
-   If no color space is specified, no color matching is done. */
+   If no color space is specified, no color matching is done. 
+   The return values will be null if the format is unsupported or the extent is too big.
+*/
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH) && SWIFT_SDK_OVERLAY_COREIMAGE_EPOCH >= 2)
++ (nullable instancetype)imageAccumulatorWithExtent:(CGRect)extent
+                                             format:(CIFormat)format;
+
++ (nullable instancetype)imageAccumulatorWithExtent:(CGRect)extent
+                                             format:(CIFormat)format
+                                         colorSpace:(CGColorSpaceRef)colorSpace
+NS_AVAILABLE(10_7, 9_0);
+
+- (nullable instancetype)initWithExtent:(CGRect)extent
+                                 format:(CIFormat)format;
+
+- (nullable instancetype)initWithExtent:(CGRect)extent
+                                 format:(CIFormat)format
+                             colorSpace:(CGColorSpaceRef)colorSpace
+NS_AVAILABLE(10_7, 9_0);
+#else
 + (instancetype)imageAccumulatorWithExtent:(CGRect)extent
                                     format:(CIFormat)format;
 
@@ -26,12 +45,14 @@
                                 colorSpace:(CGColorSpaceRef)colorSpace
 NS_AVAILABLE(10_7, 9_0);
 
-- (instancetype)initWithExtent:(CGRect)extent format:(CIFormat)format;
+- (instancetype)initWithExtent:(CGRect)extent
+                        format:(CIFormat)format;
 
 - (instancetype)initWithExtent:(CGRect)extent
                         format:(CIFormat)format
                     colorSpace:(CGColorSpaceRef)colorSpace
 NS_AVAILABLE(10_7, 9_0);
+#endif
 
 /* Return the extent of the accumulator. */
 @property (readonly) CGRect extent;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImageProcessor.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImageProcessor.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImageProcessor.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImageProcessor.h	2016-05-21 08:19:52.000000000 +0200
@@ -0,0 +1,154 @@
+/* 
+   CoreImage - CIImageProcessor.h
+
+   Copyright (c) 2016 Apple Inc.
+   All rights reserved. 
+*/
+
+#import <CoreImage/CIImage.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@protocol MTLTexture, MTLCommandBuffer;
+
+@protocol CIImageProcessorInput;
+@protocol CIImageProcessorOutput;
+
+
+@interface CIImage (CIImageProcessor)
+
+// Creates a new image by modifying an input image.
+//
+// The receiver of the method is the input image to be processed.
+//
+// The return value of the method is a new image that represents the processed image.
+//
+// extent:         Declares the bounding rectangle of non-clear pixels in the output.
+//
+// description:    Provides a unique name for your processor.
+//
+// argumentDigest: Provides a 64-bit digest of arguments that affect the processor's output of the receiver.
+//                 This digest allows Core Image to resuse a cache of processor's output when given the
+//                 same input image and arguments. The digest should be calulated from the aguments using
+//                 CommonDigest.h or similar algorithm.
+//                 If the digest is 0, then Core Image will not be able to cache of processor's output.
+//
+// inputFormat:    The pixel format for the input of the processor. The format must be
+//                 one of kCIFormatBGRA8, kCIFormatRGBAh or kCIFormatR8.
+//                 On OS X, the format kCIFormatRGBAf is also supported. If the requested
+//                 inputFormat is 0, then the input will be a supported format that best
+//                 matches the rendering context's workingFormat.
+//                 If a processor wants data in a colorspace other than the context workingspace,
+//                 then call imageByColorMatchingWorkingSpaceToColorSpace on the processor input.
+//                 If a processor wants it input as alpha-unpremultiplied RGBA data, then call
+//                 imageByUnpremultiplyingAlpha on the processor input.
+//
+// outputFormat:   The pixel format for the output of the processor. The format must be
+//                 one of kCIFormatBGRA8, kCIFormatRGBAh or kCIFormatR8.
+//                 On OS X, the format kCIFormatRGBAf is also supported. If the requested
+//                 outputFormat is 0, then the output will be a supported format that best
+//                 matches the rendering context's workingFormat.
+//                 If a processor returns data in a colorspace other than the context workingspace,
+//                 then call imageByColorMatchingColorSpaceToWorkingSpace on the processor output.
+//                 If a processor returns data as alpha-unpremultiplied RGBA data, then call,
+//                 imageByPremultiplyingAlpha on the processor output.
+//
+// options:        Currenty unused.
+//
+// roiCallback:    A block that will be called one or more times per render to determine what portion
+//                 of the input image is needed to render a given 'destRect' of the output.
+//
+// processor:      A block will be called to produce the requested region of the output image
+//                 given the required region of the input image.
+//                 This block is passed two objects:
+//                   'input'   The id<CIImageProcessorInput> that the block consumes to produces output.
+//                             The input.region may be larger than the rect returned by 'roiCallback'.
+//                   'output'  The id<CIImageProcessorOutput> that the block must provide results to.
+//                 The contents of these two objects not valid outside the scope of the processor block.
+//
+- (nullable CIImage *)imageWithExtent:(CGRect)extent
+                 processorDescription:(NSString*)description
+                       argumentDigest:(uint64_t)argumentDigest
+                          inputFormat:(CIFormat)inputFormat
+                         outputFormat:(CIFormat)outputFormat
+                              options:(nullable NSDictionary<NSString *,id>*)options
+                          roiCallback:(CGRect (^) (CGRect destRect))roiCallback
+                            processor:(void (^) (id<CIImageProcessorInput> input, id<CIImageProcessorOutput> output))processor
+NS_AVAILABLE(10_12, 10_0);
+
+@end
+
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@protocol CIImageProcessorInput
+
+// The rectangular region of the input image that the processor block can use to provide the output.
+// This will be contain (but may be larger than) the rect returned by 'roiCallback'.
+@property (nonatomic, readonly) CGRect region;
+
+
+// The bytes per row of the input buffer that the processor block can read from.
+@property (nonatomic, readonly) size_t bytesPerRow;
+
+// The pixel format of the input buffer that the processor block can read from.
+@property (nonatomic, readonly) CIFormat format;
+
+// The base address of the input buffer that the processor block can read from.
+// This memory must not be modified by the block.
+@property (readonly, nonatomic) const void *baseAddress NS_RETURNS_INNER_POINTER;
+
+
+#if !TARGET_OS_IPHONE
+// An input IOSurface that the processor block can read from.
+// This surface must not be modified by the block.
+@property (nonatomic, readonly) IOSurfaceRef surface;
+#endif
+
+// An input CVPixelBuffer that the processor block can read from.
+// This buffer must not be modified by the block.
+@property (nonatomic, readonly, nullable) CVPixelBufferRef pixelBuffer;
+
+
+// A MTLTexture object that can be bound as input (if processing using Metal).
+// This texture must not be modified by the block.
+@property (nonatomic, readonly, nullable) id<MTLTexture> metalTexture;
+
+@end
+
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@protocol CIImageProcessorOutput
+
+// The rectangular region of the output image that the processor block must provide.
+@property (nonatomic, readonly) CGRect region;
+
+
+// The bytes per row of the output buffer that the processor block can write to.
+@property (nonatomic, readonly) size_t bytesPerRow;
+
+// The pixel format of the output buffer that the processor block can write to.
+@property (nonatomic, readonly) CIFormat format;
+
+// The base address of the output buffer that the processor block can write output pixels to.
+@property (readonly, nonatomic) void *baseAddress NS_RETURNS_INNER_POINTER;
+
+
+#if !TARGET_OS_IPHONE
+// An output IOSurface that the processor block can write to.
+@property (nonatomic, readonly) IOSurfaceRef surface;
+#endif
+
+// A output CVPixelBuffer that the processor block can write to.
+@property (nonatomic, readonly, nullable) CVPixelBufferRef pixelBuffer;
+
+
+// A MTLTexture object that can be bound as output (if processing using Metal).
+@property (nonatomic, readonly, nullable) id<MTLTexture> metalTexture;
+
+// Returns a MTLCommandBuffer that can be used for encoding commands (if rendering using Metal).
+@property (nonatomic, readonly, nullable) id<MTLCommandBuffer> metalCommandBuffer;
+
+@end
+
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImageProvider.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImageProvider.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImageProvider.h	2015-08-25 05:35:43.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImageProvider.h	2016-05-21 07:18:49.000000000 +0200
@@ -1,33 +1,27 @@
-/* 
+/*
    CoreImage - CIImageProvider.h
 
    Copyright (c) 2015 Apple, Inc.
-   All rights reserved. 
+   All rights reserved.
 */
 
 #import <CoreImage/CIImage.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
-#if __has_feature(objc_generics)
-# define CI_DICTIONARY(KeyType, ValueType) NSDictionary<KeyType, ValueType>
-# define CI_ARRAY(ValueType) NSArray <ValueType>
-#else
-# define CI_DICTIONARY(KeyType, ValueType) NSDictionary
-# define CI_ARRAY(ValueType) NSArray
-#endif
-
-
 @interface CIImage (CIImageProvider)
 
-/* Create a new CIImage lazily populated with with data provided by 'p' when
- * required. 'p' is retained until the image is deallocated. */
+/* Create a new CIImage populated when rendered with  data provided by 'p'.
+ * The provider object 'p' is retained until the image is deallocated. 
+ * The 'options' dictionary supports kCIImageProviderTileSize as well as
+ * other options defined in CIImage.h 
+ */
 + (CIImage *)imageWithImageProvider:(id)p
 							   size:(size_t)width
                                    :(size_t)height
 							 format:(CIFormat)f
 						 colorSpace:(nullable CGColorSpaceRef)cs
-                            options:(nullable CI_DICTIONARY(NSString*,id) *)options
+                            options:(nullable NSDictionary<NSString *,id> *)options
     NS_AVAILABLE(10_4, 9_0);
 
 - (instancetype)initWithImageProvider:(id)p
@@ -35,7 +29,7 @@
                                      :(size_t)height
                                format:(CIFormat)f
                            colorSpace:(nullable CGColorSpaceRef)cs
-                              options:(nullable CI_DICTIONARY(NSString*,id) *)options
+                              options:(nullable NSDictionary<NSString *,id> *)options
     NS_AVAILABLE(10_4, 9_0);
 
 @end
@@ -50,13 +44,13 @@
  *
  * By default, this method will be called to requests the full image
  * data regardless of what subregion is needed for the current render.
- * All of the image is loaded or none of it is. 
+ * All of the image is loaded or none of it is.
  *
  * If the kCIImageProviderTileSize option is specified, then only the
  * tiles that are needed are requested.
  *
  * Changing the virtual memory mapping of the supplied buffer (e.g. using
- * vm_copy () to modify it) will give undefined behavior. 
+ * vm_copy () to modify it) will give undefined behavior.
  */
 - (void)provideImageData:(void *)data
 			 bytesPerRow:(size_t)rowbytes
@@ -87,7 +81,4 @@
  */
 CORE_IMAGE_EXPORT NSString * const kCIImageProviderUserInfo NS_AVAILABLE(10_4, 9_0);
 
-#undef CI_DICTIONARY
-#undef CI_ARRAY
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIKernel.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIKernel.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIKernel.h	2015-08-25 05:35:43.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIKernel.h	2016-05-21 07:18:49.000000000 +0200
@@ -8,14 +8,6 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-#if __has_feature(objc_generics)
-# define CI_DICTIONARY(KeyType, ValueType) NSDictionary<KeyType, ValueType>
-# define CI_ARRAY(ValueType) NSArray <ValueType>
-#else
-# define CI_DICTIONARY(KeyType, ValueType) NSDictionary
-# define CI_ARRAY(ValueType) NSArray
-#endif
-
 /* Block callback used by Core Image to ask what rectangles of a kernel's input images
  * are needed to produce a desired rectangle of the kernel's output image.
  *
@@ -59,7 +51,7 @@
  * On OSX after 10.10, the array will contain instances of CIKernel, CIColorKernel or CIWarpKernel classes.
  * On iOS, the array will contain instances of CIKernel, CIColorKernel or CIWarpKernel classes.
  */
-+ (nullable CI_ARRAY(CIKernel*) *)kernelsWithString:(NSString *)string  NS_AVAILABLE(10_4, 8_0);
++ (nullable NSArray<CIKernel *> *)kernelsWithString:(NSString *)string  NS_AVAILABLE(10_4, 8_0);
 
 /* The string argument should contain a program with one kernel.
  * On OSX 10.10 and before, this returns a CIKernel object.
@@ -106,7 +98,7 @@
  */
 - (nullable CIImage *)applyWithExtent:(CGRect)extent
                           roiCallback:(CIKernelROICallback)callback
-                            arguments:(nullable CI_ARRAY(id) *)args  NS_AVAILABLE(10_11, 8_0);
+                            arguments:(nullable NSArray<id> *)args  NS_AVAILABLE(10_11, 8_0);
 @end
 
 
@@ -134,7 +126,7 @@
  * On iOS9 [CIColorKernel kernelWithString:] will return a CIColorKernel object or nil.
  * On OS X [CIColorKernel kernelWithString:] will return a CIColorKernel object or nil.
  */
-+ (nullable instancetype)kernelWithString:(NSString *)string  NS_AVAILABLE(10_10, 8_0);
++ (nullable instancetype)kernelWithString:(NSString *)string;
 
 /* Apply the receiver CIColorKernel to produce a new CIImage object.
  *
@@ -146,7 +138,7 @@
  * then the first object in the array must be a CIImage.
  */
 - (nullable CIImage *)applyWithExtent:(CGRect)extent
-                            arguments:(nullable CI_ARRAY(id) *)args  NS_AVAILABLE(10_11, 8_0);
+                            arguments:(nullable NSArray<id> *)args;
 @end
 
 
@@ -172,7 +164,7 @@
  * On iOS9 [CIWarpKernel kernelWithString:] will return a CIWarpKernel object or nil.
  * On OS X [CIWarpKernel kernelWithString:] will return a CIWarpKernel object or nil.
  */
-+ (nullable instancetype)kernelWithString:(NSString *)string  NS_AVAILABLE(10_10, 8_0);
++ (nullable instancetype)kernelWithString:(NSString *)string;
 
 /* Apply the receiver CIWarpKernel to produce a new CIImage object.
  *
@@ -193,10 +185,7 @@
 - (nullable CIImage *)applyWithExtent:(CGRect)extent
                           roiCallback:(CIKernelROICallback)callback
                            inputImage:(CIImage*)image
-                            arguments:(nullable CI_ARRAY(id) *)args  NS_AVAILABLE(10_11, 8_0);
+                            arguments:(nullable NSArray<id> *)args;
 @end
 
-#undef CI_DICTIONARY
-#undef CI_ARRAY
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIRAWFilter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIRAWFilter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIRAWFilter.h	2015-08-25 05:35:43.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIRAWFilter.h	2016-05-21 08:03:12.000000000 +0200
@@ -9,7 +9,6 @@
 
 @class NSURL;
 @class NSDictionary;
-@class NSString;
 @class NSData;
 
 /** CIRAWFilter is a category of CIFilter which returns a CIFilter initialized with a RAW image. It allows the user to influence key aspects of the raw processing, such as white balance, exposure, sharpening or boost. */
@@ -17,98 +16,113 @@
 @interface CIFilter (CIRAWFilter)
 
 /** Returns a CIFilter that will in turn return a properly processed CIImage as "outputImage". */
-+ (CIFilter *)filterWithImageURL:(NSURL *)url options:(NSDictionary *)options;
++ (CIFilter *)filterWithImageURL:(NSURL *)url options:(NSDictionary *)options NS_AVAILABLE(10_5, 10_0);
 
 /** Returns a CIFilter that will in turn return a properly processed CIImage as "outputImage".
 
- Note that when using this initializer, you should pass in a source type identifier hint (kCGImageSourceTypeIdentifierHint) key/value pair in order to help the decoder determine the file type, as otherwise confusion and incorrect results are possible. An example of use would be: [opts setObject:(id)CGImageSourceGetTypeWithExtension ((CFStringRef)[[url path] pathExtension]) forKey:kCGImageSourceTypeIdentifierHint]; */
-+ (CIFilter *)filterWithImageData:(NSData *)data options:(NSDictionary *)options;
+ Note that when using this initializer, you should pass in a source type identifier hint (kCGImageSourceTypeIdentifierHint) key/value pair in order to help the decoder determine the file type, as otherwise confusion and incorrect results are possible. */
++ (CIFilter *)filterWithImageData:(NSData *)data options:(NSDictionary *)options NS_AVAILABLE(10_5, 10_0);
+
 
-/** NSString: Version string representing the decoder version to be used. A newly initialized object defaults to the newest available decoder version for the given image type. User can request an alternative, older version in order to maintain compatibility with older releases. Must be one of kCISupportedDecoderVersions (below), otherwise a nil output image will be generated. */
-CORE_IMAGE_EXPORT NSString *const kCIInputDecoderVersionKey NS_AVAILABLE(10_5, 9_0);
 
+/** NSNumber (BOOL) : Setting Draft Mode to YES can improve image decoding speed without minimal loss of quality.
+    The default value is NO. */
+CORE_IMAGE_EXPORT NSString *const kCIInputAllowDraftModeKey NS_AVAILABLE(10_5, 10_0);
+
+/** NSString: Version string representing the decoder version to be used. A newly initialized object defaults to the newest available decoder version for the given image type. User can request an alternative, older version in order to maintain compatibility with older releases. Must be one of kCISupportedDecoderVersions (below), otherwise a nil output image will be generated. */
+CORE_IMAGE_EXPORT NSString *const kCIInputDecoderVersionKey NS_AVAILABLE(10_5, 10_0);
 
 /** NSArray (NSDictionary) : Array of all supported decoder versions for the given image type, sorted in increasingly newer order. Each entry is a NSDictionary with a number of key/value pairs. All entries would represent a valid version identifier to be passed in for kCIInputDecoderVersion. This value can be only read; setting this value will raise an exception. Currently, the only defined key is @"version" which has as a value an NSString uniquely describing a given decoder version. This string may not be suitable for user interface display. */
-CORE_IMAGE_EXPORT NSString *const kCISupportedDecoderVersionsKey NS_AVAILABLE(10_5, 9_0);
+CORE_IMAGE_EXPORT NSString *const kCISupportedDecoderVersionsKey NS_AVAILABLE(10_5, 10_0);
+
 
 
 /** @const      kCIInputEVKey
  NSNumber (float) : Exposure adjustment, default = 0.0. Declared in CIFilter.h */
 
 
-/** NSNumber (float) : A value in the range of 0...1, controling the amount of boost applied to the image. A value of 0 indicates no boost, i.e. linear response. Default is 1, full boost. */
-CORE_IMAGE_EXPORT NSString *const kCIInputBoostKey NS_AVAILABLE(10_5, 9_0);
+
+/** NSNumber (float) : A value in the range of 0...1, controling the amount of boost applied to the image. 
+    A value of 0 indicates no boost, i.e. linear response. Default is 1, full boost. */
+CORE_IMAGE_EXPORT NSString *const kCIInputBoostKey NS_AVAILABLE(10_5, 10_0);
+
+/** NSNumber (float) : The amount to boost the shadow areas of the image. Can be used to lighten details in shadows. 
+    Has no effect if the image used for initialization was not RAW. */
+CORE_IMAGE_EXPORT NSString *const kCIInputBoostShadowAmountKey NS_AVAILABLE(10_5, 10_0);
+
+
 
 /** NSNumber (float): The X value of the chromaticity. You can always query this value and you'll get the current X value for neutral X,Y. */
-CORE_IMAGE_EXPORT NSString *const kCIInputNeutralChromaticityXKey NS_AVAILABLE(10_5, 9_0);
+CORE_IMAGE_EXPORT NSString *const kCIInputNeutralChromaticityXKey NS_AVAILABLE(10_5, 10_0);
 
 /** NSNumber (float): The Y value of the chromaticity. You can always query this value and you'll get the current Y value for neutral X,Y. */
-CORE_IMAGE_EXPORT NSString *const kCIInputNeutralChromaticityYKey NS_AVAILABLE(10_5, 9_0);
+CORE_IMAGE_EXPORT NSString *const kCIInputNeutralChromaticityYKey NS_AVAILABLE(10_5, 10_0);
 
 /** NSNumber (float) : The color temperature to be considered neutral. You can always query this value and you'll get the current value for temperature. */
-CORE_IMAGE_EXPORT NSString *const kCIInputNeutralTemperatureKey NS_AVAILABLE(10_5, 9_0);
+CORE_IMAGE_EXPORT NSString *const kCIInputNeutralTemperatureKey NS_AVAILABLE(10_5, 10_0);
 
 /** NSNumber (float) : The tint to be considered neutral. You can always query this value and you'll get the current value for tint. */
-CORE_IMAGE_EXPORT NSString *const kCIInputNeutralTintKey NS_AVAILABLE(10_5, 9_0);
+CORE_IMAGE_EXPORT NSString *const kCIInputNeutralTintKey NS_AVAILABLE(10_5, 10_0);
 
-/** CIVector : (x, y) location in geometric coordinates of the unrotated output image that should be used as neutral. You can't query this value - it's undefined for reading. */
-CORE_IMAGE_EXPORT NSString *const kCIInputNeutralLocationKey NS_AVAILABLE(10_5, 9_0);
+/** CIVector : (x, y) location in geometric coordinates of the unrotated output image that should be used as neutral. 
+    You can't query this value - it's undefined for reading. */
+CORE_IMAGE_EXPORT NSString *const kCIInputNeutralLocationKey NS_AVAILABLE(10_5, 10_0);
 
 /** NSNumber (float) : The desired scale factor at which the image will be eventually drawn. Setting this value can greatly improve the drawing performance. A value of 1 would mean identity, values smaller than 1 will result in a smaller output image. Changing the Scale Factor with enabled Draft Mode may also improve performance. */
-CORE_IMAGE_EXPORT NSString *const kCIInputScaleFactorKey NS_AVAILABLE(10_5, 9_0);
+CORE_IMAGE_EXPORT NSString *const kCIInputScaleFactorKey NS_AVAILABLE(10_5, 10_0);
+
 
-/** NSNumber (BOOL) : If the optional scale factor is smaller than a certain factor, additionally setting Draft Mode to YES can improve image decoding speed without any perceivable loss of quality. Setting this argument to YES will not have any effect if the Scale Factor isn't below a threshold where it would be of benefit. Switching of this value from YES to NO is an expensive operation, and it's not recommended to use Draft Mode if the same image will need to be drawn without Draft Mode at a later time. */
-CORE_IMAGE_EXPORT NSString *const kCIInputAllowDraftModeKey NS_AVAILABLE(10_5, 9_0);
 
 
 /** NSNumber (BOOL) : Normally, an image is loaded in its proper orientation, given the associated metadata gives an indication about the orientation. For special purposes it may be useful to load the image in its physical orientation. The exact meaning of this is dependent on the image in question. The default value is NO. */
-CORE_IMAGE_EXPORT NSString *const kCIInputIgnoreImageOrientationKey NS_AVAILABLE(10_5, 9_0);
+CORE_IMAGE_EXPORT NSString *const kCIInputIgnoreImageOrientationKey NS_AVAILABLE(10_5, 10_0);
 
 
-/**
- @const      kCIInputImageOrientationKey
- @abstract   kCIInputImageOrientationKey
- @discussion NSNumber (int) : Overriding this value allows the user to change the orientation of the image. The valid values are in range 1...8 and follow the EXIF specification. Changing this value makes for instance rotation in 90-degree increments easy. The value is disregarded when the kCIInputIgnoreImageOrientationKey flag is set.
+/** NSNumber (int) : Overriding this value allows the user to change the orientation of the image. The valid values are in range 1...8 and follow the EXIF specification. Changing this value makes for instance rotation in 90-degree increments easy. The value is disregarded when the kCIInputIgnoreImageOrientationKey flag is set.
  */
-CORE_IMAGE_EXPORT NSString *const kCIInputImageOrientationKey NS_AVAILABLE(10_5, 9_0);
+CORE_IMAGE_EXPORT NSString *const kCIInputImageOrientationKey NS_AVAILABLE(10_5, 10_0);
+
+
 
 /** NSNumber (BOOL) : Determines if the default sharpening should be on. default = YES. Has no effect if the image used for initialization was not RAW. */
-CORE_IMAGE_EXPORT NSString *const kCIInputEnableSharpeningKey NS_AVAILABLE(10_5, 9_0);
+CORE_IMAGE_EXPORT NSString *const kCIInputEnableSharpeningKey NS_AVAILABLE(10_5, 10_0);
 
 /** NSNumber (BOOL) : Determines if progressive chromatic noise tracking (based on ISO and exposure time) should be used. default = YES. Has no effect if the image used for initialization was not RAW. */
-CORE_IMAGE_EXPORT NSString *const kCIInputEnableChromaticNoiseTrackingKey NS_AVAILABLE(10_5, 9_0);
+CORE_IMAGE_EXPORT NSString *const kCIInputEnableChromaticNoiseTrackingKey NS_AVAILABLE(10_5, 10_0);
 
 /** NSNumber (double) : The amount of noise reduction applied. Range is 0 to 1. */
-CORE_IMAGE_EXPORT NSString *const kCIInputNoiseReductionAmountKey AVAILABLE_MAC_OS_X_VERSION_10_7_AND_LATER;
+CORE_IMAGE_EXPORT NSString *const kCIInputNoiseReductionAmountKey NS_AVAILABLE(10_7, 10_0);
 
 /** NSNumber (BOOL) : Determines if the default vendor lens correction be on. default = YES if raw image used for initialization contains lens distortion parameters. */
-CORE_IMAGE_EXPORT NSString *const kCIInputEnableVendorLensCorrectionKey AVAILABLE_MAC_OS_X_VERSION_10_10_AND_LATER;
+CORE_IMAGE_EXPORT NSString *const kCIInputEnableVendorLensCorrectionKey NS_AVAILABLE(10_10, 10_0);
 
 /** NSNumber (double) : The amount of luminance noise reduction applied. Range is 0 to 1. */
-CORE_IMAGE_EXPORT NSString *const kCIInputLuminanceNoiseReductionAmountKey AVAILABLE_MAC_OS_X_VERSION_10_10_AND_LATER;
+CORE_IMAGE_EXPORT NSString *const kCIInputLuminanceNoiseReductionAmountKey NS_AVAILABLE(10_10, 10_0);
 
 /** NSNumber (double) : The amount of color noise reduction applied. Range is 0 to 1. */
-CORE_IMAGE_EXPORT NSString *const kCIInputColorNoiseReductionAmountKey AVAILABLE_MAC_OS_X_VERSION_10_10_AND_LATER;
+CORE_IMAGE_EXPORT NSString *const kCIInputColorNoiseReductionAmountKey NS_AVAILABLE(10_10, 10_0);
 
 /** NSNumber (double) : The amount of noise reduction sharpness applied. Range is 0 to 1. */
-CORE_IMAGE_EXPORT NSString *const kCIInputNoiseReductionSharpnessAmountKey AVAILABLE_MAC_OS_X_VERSION_10_10_AND_LATER;
+CORE_IMAGE_EXPORT NSString *const kCIInputNoiseReductionSharpnessAmountKey NS_AVAILABLE(10_10, 10_0);
 
 /** NSNumber (double) : The amount of noise reduction contrast applied. Range is 0 to 1. */
-CORE_IMAGE_EXPORT NSString *const kCIInputNoiseReductionContrastAmountKey AVAILABLE_MAC_OS_X_VERSION_10_10_AND_LATER;
+CORE_IMAGE_EXPORT NSString *const kCIInputNoiseReductionContrastAmountKey NS_AVAILABLE(10_10, 10_0);
 
 /** NSNumber (double) : The amount of noise reduction detail applied. Range is 0 to 1. */
-CORE_IMAGE_EXPORT NSString *const kCIInputNoiseReductionDetailAmountKey AVAILABLE_MAC_OS_X_VERSION_10_10_AND_LATER;
+CORE_IMAGE_EXPORT NSString *const kCIInputNoiseReductionDetailAmountKey NS_AVAILABLE(10_10, 10_0);
 
-/** NSNumber (float) : The amount to boost the shadow areas of the image. Can be used to lighten details in shadows. Has no effect if the image used for initialization was not RAW. */
-CORE_IMAGE_EXPORT NSString *const kCIInputBoostShadowAmountKey NS_AVAILABLE(10_5, 9_0);
 
-/** CIFilter (id) : CIFilter to be applied to the RAW image while it is in linear space. */
-CORE_IMAGE_EXPORT NSString *const kCIInputLinearSpaceFilter NS_AVAILABLE(10_7, 9_0);
 
-/** CIVector containing the full native size of the unscaled image. The vector's X value is the width, Y is the height. This is not affected by changing either kCIInputIgnoreImageOrientationKey or kCIInputImageOrientationKey. */
-CORE_IMAGE_EXPORT NSString *const kCIOutputNativeSizeKey NS_AVAILABLE(10_5, 9_0);
+/** CIFilter (id) : CIFilter to be applied to the RAW image while it is in linear space. */
+CORE_IMAGE_EXPORT NSString *const kCIInputLinearSpaceFilter NS_AVAILABLE(10_7, 10_0);
 
-/** Read-only NSSet containing a list of keys that affect the output image. Depending on the RAW decoder version (kCIInputDecoderVersionKey) and the input image type, some input keys might have no effect. */
-CORE_IMAGE_EXPORT NSString *const kCIActiveKeys NS_AVAILABLE(10_7, 9_0);
+/** CIVector containing the full native size of the unscaled image. The vector's X value is the width, Y is the height. 
+    This is not affected by changing either kCIInputIgnoreImageOrientationKey or kCIInputImageOrientationKey. */
+CORE_IMAGE_EXPORT NSString *const kCIOutputNativeSizeKey NS_AVAILABLE(10_5, 10_0);
+
+/** Read-only NSSet containing a list of keys that affect the output image. 
+    Depending on the RAW decoder version (kCIInputDecoderVersionKey) and the input image type, 
+    some input keys might have no effect. */
+CORE_IMAGE_EXPORT NSString *const kCIActiveKeys NS_AVAILABLE(10_7, 10_0);
 
 @end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CoreImage.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CoreImage.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CoreImage.h	2015-08-25 05:35:43.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CoreImage.h	2016-05-21 07:18:49.000000000 +0200
@@ -19,14 +19,15 @@
 #import <CoreImage/CIDetector.h>
 #import <CoreImage/CIFeature.h>
 #import <CoreImage/CIImageProvider.h>
+#import <CoreImage/CIImageProcessor.h>
 #import <CoreImage/CIImageAccumulator.h>
 #import <CoreImage/CIFilterConstructor.h>
 #import <CoreImage/CIFilterShape.h>
 #import <CoreImage/CISampler.h>
+#import <CoreImage/CIRAWFilter.h>
 #if !TARGET_OS_IPHONE
 #import <CoreImage/CIFilterGenerator.h>
 #import <CoreImage/CIPlugIn.h>
-#import <CoreImage/CIRAWFilter.h>
 #endif
 
 #endif /* __OBJC__ */

```