#MetalPerformanceShaders.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSCNN.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSCNN.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSCNN.h	2016-06-26 07:44:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSCNN.h	2016-07-10 07:17:32.000000000 +0200
@@ -133,7 +133,7 @@
 -(void) encodeToCommandBuffer: (nonnull id <MTLCommandBuffer>) commandBuffer
                   sourceImage: (MPSImage * __nonnull) sourceImage
              destinationImage: (MPSImage * __nonnull) destinationImage
-                NS_SWIFT_NAME( encode(commandBuffer:sourceImage:destinationImage:));
+                MPS_SWIFT_NAME( encode(commandBuffer:sourceImage:destinationImage:));
 
 /*!
  *  sourceRegionForDestinationSize: is used to determine which region of the
@@ -162,7 +162,7 @@
  *  @return     The area in the virtual source image that will be read.
  */
 -(MPSRegion) sourceRegionForDestinationSize: (MTLSize) destinationSize
-                  NS_SWIFT_NAME( sourceRegion(destinationSize:));
+                  MPS_SWIFT_NAME( sourceRegion(destinationSize:));
 @end
 
 
@@ -1011,6 +1011,26 @@
 
 @end    /* MPSCNNSoftMax */
 
+/*!
+ *  @class      MPSCNNLogSoftMax
+ *  @dependency This depends on Metal.framework
+ *  @discussion The logarithmic softmax filter can be achieved by taking the natural logarithm of the
+ *              the result of the softmax filter. The results are often used to construct a loss function to be
+ *              minimized when training neural networks.
+ *              For each feature channel per pixel in an image in a feature map, the logarithmic softmax filter
+ *              computes the following:
+ *                  result channel in pixel = pixel(x,y,k)) - ln{sum(exp(pixel(x,y,0)) ... exp(pixel(x,y,N-1))}
+ *                      where N is the number of feature channels and y = ln{x} satisfies e^y = x.
+ *
+ */
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
+@interface MPSCNNLogSoftMax : MPSCNNKernel
+
+@end    /* MPSCNNLogSoftMax */
+
+
+
+
 #ifdef __cplusplus
 }       /* extern "C" */
 #endif
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageConversion.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageConversion.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageConversion.h	2016-06-26 07:44:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageConversion.h	2016-07-10 07:17:32.000000000 +0200
@@ -11,8 +11,7 @@
 #define MPS_Conversions_h
 
 #include <MetalPerformanceShaders/MPSImageKernel.h>
-
-#include <CoreGraphics/CGColorConverter.h>
+#include <CoreGraphics/CGColorConversionInfo.h>
 
 
 /*!
@@ -53,7 +52,7 @@
  *  @param      backgroundColor     An array of CGFloats giving the background color to use when flattening an image.
  *                                  The color is in the source colorspace.  The length of the array is the number 
  *                                  of color channels in the src colorspace. If NULL, use {0}.
- *  @param      colorConverter      The colorspace converter to use. May be NULL, indicating no
+ *  @param      conversionInfo      The colorspace conversion to use. May be NULL, indicating no
  *                                  color space conversions need to be done.
  *
  *  @result     An initialized MPSImageConversion object.
@@ -62,7 +61,7 @@
                               srcAlpha:(MPSAlphaType) srcAlpha
                              destAlpha:(MPSAlphaType) destAlpha
                        backgroundColor:(nullable CGFloat*) backgroundColor
-                        colorConverter:(nullable CGColorConverterRef) colorConverter;
+                        conversionInfo:(nullable CGColorConversionInfoRef) conversionInfo;
 
 
 @end  /* MPSImageConversion */
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageKernel.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageKernel.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageKernel.h	2016-06-26 07:44:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageKernel.h	2016-07-10 07:17:32.000000000 +0200
@@ -146,7 +146,7 @@
 -(BOOL)    encodeToCommandBuffer: (nonnull id <MTLCommandBuffer>)commandBuffer
                   inPlaceTexture: (__nonnull id <MTLTexture> __strong * __nonnull) texture
            fallbackCopyAllocator: (nullable MPSCopyAllocator) copyAllocator
-                NS_SWIFT_NAME(encode(commandBuffer:inPlaceTexture:fallbackCopyAllocator:));
+                MPS_SWIFT_NAME(encode(commandBuffer:inPlaceTexture:fallbackCopyAllocator:));
 
 
 /*!
@@ -158,7 +158,7 @@
 -(void) encodeToCommandBuffer: (nonnull id <MTLCommandBuffer>) commandBuffer
                 sourceTexture: (nonnull id <MTLTexture>) sourceTexture
            destinationTexture: (nonnull id <MTLTexture>) destinationTexture
-            NS_SWIFT_NAME(encode(commandBuffer:sourceTexture:destinationTexture:));
+            MPS_SWIFT_NAME(encode(commandBuffer:sourceTexture:destinationTexture:));
 
 
 /*!
@@ -188,7 +188,7 @@
  *  @return     The area in the virtual source image that will be read.
  */
 -(MPSRegion) sourceRegionForDestinationSize: (MTLSize) destinationSize
-            NS_SWIFT_NAME(sourceRegion(destinationSize:));
+            MPS_SWIFT_NAME(sourceRegion(destinationSize:));
 
 @end
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSMatrixMultiplication.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSMatrixMultiplication.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSMatrixMultiplication.h	2016-06-26 07:44:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSMatrixMultiplication.h	2016-07-10 07:17:32.000000000 +0200
@@ -142,7 +142,7 @@
                    leftMatrix: (MPSMatrix const* __nonnull) leftMatrix
                   rightMatrix: (MPSMatrix const* __nonnull) rightMatrix
                  resultMatrix: (MPSMatrix* __nonnull) resultMatrix
-                    NS_SWIFT_NAME(encode(commandBuffer:leftMatrix:rightMatrix:resultMatrix:));
+                    MPS_SWIFT_NAME(encode(commandBuffer:leftMatrix:rightMatrix:resultMatrix:));
 
 
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSTypes.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSTypes.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSTypes.h	2016-06-26 07:44:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSTypes.h	2016-07-10 09:31:51.000000000 +0200
@@ -25,31 +25,51 @@
 #ifndef __has_extension         /* clang will define this. Other compilers maybe not. */
 #    define __has_extension(e)   0
 #endif
-#if __has_extension(enumerator_attributes)
+    
+#ifdef MPS_HIDE_AVAILABILITY
+#    define MPS_ENUM_AVAILABLE_STARTING(_osx, _ios, _tvos)
+#    define MPS_CLASS_AVAILABLE_STARTING(_osx, _ios, _tvos)
+#    define MPS_AVAILABLE_STARTING(_osx, _ios, _tvos)
+#else
 #    ifdef __IPHONE_OS_VERSION_MIN_REQUIRED
 #        define MPS_CLASS_AVAILABLE_STARTING(_osx, _ios, _tvos)  __attribute__((visibility("default"))) __AVAILABILITY_INTERNAL##_ios
-#        define MPS_ENUM_AVAILABLE_STARTING(_osx, _ios, _tvos)   __AVAILABILITY_INTERNAL##_ios
 #        define MPS_AVAILABLE_STARTING(_osx, _ios, _tvos)        __AVAILABILITY_INTERNAL##_ios
 #    elif defined(__MAC_OS_X_VERSION_MIN_REQUIRED)
 #        define MPS_CLASS_AVAILABLE_STARTING(_osx, _ios, _tvos)  __attribute__((visibility("default"))) __AVAILABILITY_INTERNAL##_osx
-#        define MPS_ENUM_AVAILABLE_STARTING(_osx, _ios, _tvos)   __AVAILABILITY_INTERNAL##_osx
 #        define MPS_AVAILABLE_STARTING(_osx, _ios, _tvos)        __AVAILABILITY_INTERNAL##_osx
 #    elif __has_feature(attribute_availability_tvos)
 #        define MPS_CLASS_AVAILABLE_STARTING(_osx, _ios, _tvos)  __attribute__((visibility("default"))) __OS_AVAILABILITY(_tvos,introduced=_vers)
-#        define MPS_ENUM_AVAILABLE_STARTING(_osx, _ios, _tvos)   __OS_AVAILABILITY(_tvos,introduced=_vers)
 #        define MPS_AVAILABLE_STARTING(_osx, _ios, _tvos)        __OS_AVAILABILITY(_tvos,introduced=_vers)
 #    elif __has_feature(attribute_availability_watchos)
 #        define MPS_CLASS_AVAILABLE_STARTING(_osx, _ios, _tvos)  __attribute__((visibility("default"))) __OS_AVAILABILITY(watchos,unavailable)
-#        define MPS_ENUM_AVAILABLE_STARTING(_osx, _ios, _tvos)   __OS_AVAILABILITY(watchos,unavailable)
 #        define MPS_AVAILABLE_STARTING(_osx, _ios, _tvos)        __OS_AVAILABILITY(watchos,unavailable)
 #    else
-#        define MPS_ENUM_AVAILABLE_STARTING(_osx, _ios, _tvos)
+#        define MPS_CLASS_AVAILABLE_STARTING(_osx, _ios, _tvos)
 #        define MPS_AVAILABLE_STARTING(_osx, _ios, _tvos)
 #    endif
-#else
-#    define MPS_ENUM_AVAILABLE_STARTING( _a, _b )
+#
+#    if __has_extension(enumerator_attributes)
+#       ifdef __IPHONE_OS_VERSION_MIN_REQUIRED
+#           define MPS_ENUM_AVAILABLE_STARTING(_osx, _ios, _tvos)   __AVAILABILITY_INTERNAL##_ios
+#       elif defined(__MAC_OS_X_VERSION_MIN_REQUIRED)
+#           define MPS_ENUM_AVAILABLE_STARTING(_osx, _ios, _tvos)   __AVAILABILITY_INTERNAL##_osx
+#       elif __has_feature(attribute_availability_tvos)
+#           define MPS_ENUM_AVAILABLE_STARTING(_osx, _ios, _tvos)   __OS_AVAILABILITY(_tvos,introduced=_vers)
+#       elif __has_feature(attribute_availability_watchos)
+#           define MPS_ENUM_AVAILABLE_STARTING(_osx, _ios, _tvos)   __OS_AVAILABILITY(watchos,unavailable)
+#       else
+#           define MPS_ENUM_AVAILABLE_STARTING(_osx, _ios, _tvos)
+#       endif
+#    else
+#       define MPS_ENUM_AVAILABLE_STARTING(_osx, _ios, _tvos)
+#    endif
 #endif
 
+#if __has_feature(objc_class_property)
+#   define  MPS_SWIFT_NAME(_name)    CF_SWIFT_NAME(_name)
+#else
+#   define  MPS_SWIFT_NAME(_name)
+#endif
 
 /*! @enum       MPSKernelOptions
  *  @memberof   MPSKernel

```