#CoreImage.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIFilterGenerator.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIFilterGenerator.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIFilterGenerator.h	2016-05-04 00:21:22.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIFilterGenerator.h	2016-06-26 17:49:40.000000000 +0200
@@ -33,8 +33,7 @@
 NS_CLASS_AVAILABLE_MAC(10_5)
 @interface CIFilterGenerator : NSObject <NSSecureCoding, NSCopying, CIFilterConstructor>
 {
-    @private
-    struct CIFilterGeneratorStruct *__strong _filterGeneratorStruct;
+    @private struct CIFilterGeneratorStruct *_filterGeneratorStruct;
 }
 
 /** This creates an empty CIFilterGenerator in which you connect filters and images. */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImage.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImage.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImage.h	2016-05-21 08:27:44.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImage.h	2016-06-27 06:14:18.000000000 +0200
@@ -272,11 +272,13 @@
 
 /* Return a new image by color matching from the colorSpace to the context's working space.
  * This method will return nil if the CGColorSpace is not kCGColorSpaceModelRGB. */
-- (nullable CIImage *)imageByColorMatchingColorSpaceToWorkingSpace:(CGColorSpaceRef)colorSpace NS_AVAILABLE(10_12, 10_0);
+- (nullable CIImage *)imageByColorMatchingColorSpaceToWorkingSpace:(CGColorSpaceRef)colorSpace NS_AVAILABLE(10_12, 10_0)
+  NS_SWIFT_NAME(matchedToWorkingSpace(from:));
 
 /* Return a new image by color matching from the context's working space to the colorSpace.
  * This method will return nil if the CGColorSpace is not kCGColorSpaceModelRGB. */
-- (nullable CIImage *)imageByColorMatchingWorkingSpaceToColorSpace:(CGColorSpaceRef)colorSpace NS_AVAILABLE(10_12, 10_0);
+- (nullable CIImage *)imageByColorMatchingWorkingSpaceToColorSpace:(CGColorSpaceRef)colorSpace NS_AVAILABLE(10_12, 10_0)
+  NS_SWIFT_NAME(matchedFromWorkingSpace(to:));
 
 /* Return a new image by multiplying the receiver's RGB values by its alpha. */
 - (CIImage *)imageByPremultiplyingAlpha NS_AVAILABLE(10_12, 10_0);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImageAccumulator.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImageAccumulator.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImageAccumulator.h	2016-05-21 07:18:49.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImageAccumulator.h	2016-06-26 17:49:40.000000000 +0200
@@ -11,7 +11,7 @@
 NS_CLASS_AVAILABLE(10_4, 9_0)
 @interface CIImageAccumulator : NSObject
 {
-    __strong void *_state;
+    void *_state;
 }
 
 /* Create a new accumulator object. 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImageProcessor.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImageProcessor.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImageProcessor.h	2016-05-21 08:19:52.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIImageProcessor.h	2016-06-26 17:49:40.000000000 +0200
@@ -14,68 +14,103 @@
 @protocol CIImageProcessorInput;
 @protocol CIImageProcessorOutput;
 
+// In order to use a CIImageProcessorInput & CIImageProcessorOutput you must
+// subclass from a CIImageProcessorKernel and override the methods you need to
+// produce the desired output.
 
-@interface CIImage (CIImageProcessor)
 
-// Creates a new image by modifying an input image.
-//
-// The receiver of the method is the input image to be processed.
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface CIImageProcessorKernel : NSObject
+
+// Override this class method to implement your processor's subclass of CIImageProcessorKernel.
+// The class method will be called to produce the requested region of the output image
+// given the required regions of the input images and other arguments.
+//
+// The class method is passed two objects:
+//     'inputs’  An array of id<CIImageProcessorInput> that the block consumes to produces output.
+//               The input.region may be larger than the rect returned by 'roiForInputAtIndex'.
+//     'output'  The id<CIImageProcessorOutput> that the block must provide results to.
+//     ‘arguments’ The arguments dictionary passed to applyWithExtent:inputs:arguments:error:
+// The contents of these objects are not valid outside the scope of this method.
+//
+// Note that since this is a class method you cannot use or capture any state by accident.
+// All the parameters that affect the output results must be passed in ‘inputs’ and ‘arguments'.
+// This supports 0, 1, 2 or more input images.
+//
++ (BOOL)processWithInputs:(nullable NSArray<id<CIImageProcessorInput>> *)inputs
+                arguments:(nullable NSDictionary<NSString*,id> *)arguments
+                   output:(id <CIImageProcessorOutput>)output
+                    error:(NSError **)error;
+
+// Override this class method to implement your processor’s ROI callback, the default implementation would return outputRect.
+// This will be called one or more times per render to determine what portion
+// of the input images are needed to render a given 'outputRect' of the output.
+// This will not be called if there are 0 input images.
+//
+// Note that since this is a class method you cannot use or capture any state by accident.
+// All the parameters that affect the output results must be passed in ‘inputs’ and ‘arguments’.
+//
++ (CGRect)roiForInput:(int)input
+            arguments:(nullable NSDictionary<NSString*,id> *)arguments
+           outputRect:(CGRect)outputRect;
+
+// Override this class method if you want your any of the inputs to be in a specific supported CIPixelFormat.
+// The format must be one of kCIFormatBGRA8, kCIFormatRGBAh, kCIFormatRGBAf or kCIFormatR8.
+// If the requested inputFormat is 0, then the input will be a supported format that best
+// matches the rendering context's workingFormat.
+//
+// If a processor wants data in a colorspace other than the context workingspace,
+// then call imageByColorMatchingWorkingSpaceToColorSpace on the processor input.
+// If a processor wants it input as alpha-unpremultiplied RGBA data, then call
+// imageByUnpremultiplyingAlpha on the processor input.
+//
++ (CIFormat)formatForInputAtIndex:(int)input;
+
+// Override this class property if you want your processor's output to be in a specific supported CIPixelFormat.
+// The format must be one of kCIFormatBGRA8, kCIFormatRGBAh, kCIFormatRGBAf or kCIFormatR8.
+// If the outputFormat is 0, then the output will be a supported format that best
+// matches the rendering context's workingFormat.
+//
+// If a processor returns data in a colorspace other than the context workingspace,
+// then call imageByColorMatchingColorSpaceToWorkingSpace on the processor output.
+// If a processor returns data as alpha-unpremultiplied RGBA data, then call,
+// imageByPremultiplyingAlpha on the processor output.
+//
+#if __has_feature(objc_class_property)
+@property (class, readonly) CIFormat outputFormat;
+#else
++(CIFormat)outputFormat;
+#endif
+
+// Override this class property to return false if you want your processor to be given
+// CIImageProcessorInput objects that have not been synchonized for CPU access.
 //
-// The return value of the method is a new image that represents the processed image.
+// Generally, if your subclass uses the GPU your should override this method to return false.
+// If not overridden, true is returned.
 //
-// extent:         Declares the bounding rectangle of non-clear pixels in the output.
-//
-// description:    Provides a unique name for your processor.
-//
-// argumentDigest: Provides a 64-bit digest of arguments that affect the processor's output of the receiver.
-//                 This digest allows Core Image to resuse a cache of processor's output when given the
-//                 same input image and arguments. The digest should be calulated from the aguments using
-//                 CommonDigest.h or similar algorithm.
-//                 If the digest is 0, then Core Image will not be able to cache of processor's output.
-//
-// inputFormat:    The pixel format for the input of the processor. The format must be
-//                 one of kCIFormatBGRA8, kCIFormatRGBAh or kCIFormatR8.
-//                 On OS X, the format kCIFormatRGBAf is also supported. If the requested
-//                 inputFormat is 0, then the input will be a supported format that best
-//                 matches the rendering context's workingFormat.
-//                 If a processor wants data in a colorspace other than the context workingspace,
-//                 then call imageByColorMatchingWorkingSpaceToColorSpace on the processor input.
-//                 If a processor wants it input as alpha-unpremultiplied RGBA data, then call
-//                 imageByUnpremultiplyingAlpha on the processor input.
-//
-// outputFormat:   The pixel format for the output of the processor. The format must be
-//                 one of kCIFormatBGRA8, kCIFormatRGBAh or kCIFormatR8.
-//                 On OS X, the format kCIFormatRGBAf is also supported. If the requested
-//                 outputFormat is 0, then the output will be a supported format that best
-//                 matches the rendering context's workingFormat.
-//                 If a processor returns data in a colorspace other than the context workingspace,
-//                 then call imageByColorMatchingColorSpaceToWorkingSpace on the processor output.
-//                 If a processor returns data as alpha-unpremultiplied RGBA data, then call,
-//                 imageByPremultiplyingAlpha on the processor output.
-//
-// options:        Currenty unused.
-//
-// roiCallback:    A block that will be called one or more times per render to determine what portion
-//                 of the input image is needed to render a given 'destRect' of the output.
-//
-// processor:      A block will be called to produce the requested region of the output image
-//                 given the required region of the input image.
-//                 This block is passed two objects:
-//                   'input'   The id<CIImageProcessorInput> that the block consumes to produces output.
-//                             The input.region may be larger than the rect returned by 'roiCallback'.
-//                   'output'  The id<CIImageProcessorOutput> that the block must provide results to.
-//                 The contents of these two objects not valid outside the scope of the processor block.
-//
-- (nullable CIImage *)imageWithExtent:(CGRect)extent
-                 processorDescription:(NSString*)description
-                       argumentDigest:(uint64_t)argumentDigest
-                          inputFormat:(CIFormat)inputFormat
-                         outputFormat:(CIFormat)outputFormat
-                              options:(nullable NSDictionary<NSString *,id>*)options
-                          roiCallback:(CGRect (^) (CGRect destRect))roiCallback
-                            processor:(void (^) (id<CIImageProcessorInput> input, id<CIImageProcessorOutput> output))processor
-NS_AVAILABLE(10_12, 10_0);
+#if __has_feature(objc_class_property)
+@property (class, readonly) bool synchronizeInputs;
+#else
++(bool)synchronizeInputs;
+#endif
+
 
+// Call this method on your CIImageProcessorKernel subclass to create a new CIImage of the specified extent.
+// The inputs and arguments will be retained so that your subclass can be called when the image is drawn.
+// Arguments is a dictionary containing inmutable objects of type NSData, NSString, NSNumber,
+// CIVector or CIColor.
+//
+// This method will return [CIImage emptyImage] if extent is empty.
+//
+// This method will return nil and an error if:
+// * calling outputFormat on your subclass returns an unsupported format
+// * calling formatForInputAtIndex: on your subclass returns an unsupported format
+// * your subclass does not implement processWithInputs:arguments:output:error:
+//
++ (nullable CIImage *)applyWithExtent:(CGRect)extent
+                               inputs:(nullable NSArray<CIImage*> *)inputs
+                            arguments:(nullable NSDictionary<NSString*,id> *)args
+                                error:(NSError **)error;
 @end
 
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIRAWFilter.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIRAWFilter.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIRAWFilter.h	2016-05-21 08:03:12.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIRAWFilter.h	2016-06-26 17:49:40.000000000 +0200
@@ -6,6 +6,8 @@
 
 #import <CoreImage/CIFilter.h>
 #import <CoreImage/CoreImageDefines.h>
+#import <CoreVideo/CoreVideo.h>
+
 
 @class NSURL;
 @class NSDictionary;
@@ -23,7 +25,12 @@
  Note that when using this initializer, you should pass in a source type identifier hint (kCGImageSourceTypeIdentifierHint) key/value pair in order to help the decoder determine the file type, as otherwise confusion and incorrect results are possible. */
 + (CIFilter *)filterWithImageData:(NSData *)data options:(NSDictionary *)options NS_AVAILABLE(10_5, 10_0);
 
-
+/** Returns a CIFilter that will in turn return a properly processed CIImage as "outputImage".
+ 
+ Note that when using this initializer, you should pass in a CVPixelBufferRef with one of the following Raw pixel format types
+    kCVPixelFormatType_14Bayer_GRBG, kCVPixelFormatType_14Bayer_RGGB, kCVPixelFormatType_14Bayer_BGGR, kCVPixelFormatType_14Bayer_GBRG
+ as well as the root properties attachment from the CMSampleBufferRef. */
++ (CIFilter *)filterWithCVPixelBuffer:(CVPixelBufferRef)pixelBuffer properties:(NSDictionary *)properties options:(NSDictionary *)options NS_AVAILABLE(10_12, 10_0);
 
 /** NSNumber (BOOL) : Setting Draft Mode to YES can improve image decoding speed without minimal loss of quality.
     The default value is NO. */

```