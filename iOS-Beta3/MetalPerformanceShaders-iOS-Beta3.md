#MetalPerformanceShaders.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSCNN.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSCNN.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSCNN.h	2016-06-26 07:44:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSCNN.h	2016-07-10 07:17:32.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageConversion.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageConversion.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageConversion.h	2016-06-26 08:51:26.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageConversion.h	2016-07-10 09:31:51.000000000 +0200
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
```