#MetalPerformanceShaders.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSCNN.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSCNN.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSCNN.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSCNN.h	2016-05-21 08:10:52.000000000 +0200
@@ -0,0 +1,905 @@
+#pragma mark MPSCNNPooling
+
+/*!
+ *  @class      MPSCNNPooling
+ *  @dependency This depends on Metal.framework
+ *  @discussion Pooling is a form of non-linear sub-sampling. Pooling partitions the input image into a set of
+ *              rectangles (overlapping or non-overlapping) and, for each such sub-region, outputs a value.
+ *              The pooling operation is used in computer vision to reduce the dimensionality of intermediate representations.
+ */
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
+@interface  MPSCNNPooling : MPSCNNKernel
+
+/*! @property   kernelWidth
+ *  @abstract   The width of the filter window
+ */
+@property(readonly, nonatomic) NSUInteger       kernelWidth;
+
+/*! @property   kernelHeight
+ *  @abstract   The height of the filter window
+ */
+@property(readonly, nonatomic) NSUInteger       kernelHeight;
+
+/*! @property   strideInPixelsX
+ *  @abstract   The output stride (downsampling factor) in the x dimension.  The default value is 1.
+ */
+
+@property(readonly, nonatomic) NSUInteger      strideInPixelsX;
+
+/*! @property   strideInPixelsY
+ *  @abstract   The output stride (downsampling factor) in the y dimension.  The default value is 1.
+ */
+@property(readonly, nonatomic) NSUInteger      strideInPixelsY;
+
+/*!
+ *  @abstract  Initialize a pooling filter
+ *  @param      device              The device the filter will run on
+ *  @param      kernelWidth         The width of the kernel.  Can be an odd or even value.
+ *  @param      kernelHeight        The height of the kernel.  Can be an odd or even value.
+ *  @return     A valid MPSCNNPooling object or nil, if failure.
+ *
+ */
+-(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
+                           kernelWidth: (NSUInteger) kernelWidth
+                          kernelHeight: (NSUInteger) kernelHeight;
+
+/*!
+ *  @abstract  Initialize a pooling filter
+ *  @param      device              The device the filter will run on
+ *  @param      kernelWidth         The width of the kernel.  Can be an odd or even value.
+ *  @param      kernelHeight        The height of the kernel.  Can be an odd or even value.
+ *  @param      strideInPixelsX     The output stride (downsampling factor) in the x dimension.
+ *  @param      strideInPixelsY     The output stride (downsampling factor) in the y dimension.
+ *  @return     A valid MPSCNNPooling object or nil, if failure.
+ *
+ */
+-(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
+                           kernelWidth: (NSUInteger) kernelWidth
+                          kernelHeight: (NSUInteger) kernelHeight
+                       strideInPixelsX: (NSUInteger) strideInPixelsX
+                       strideInPixelsY: (NSUInteger) strideInPixelsY NS_DESIGNATED_INITIALIZER;
+
+/*
+ * Use initWithDevice:kernelWidth:kernelHeight:strideInPixelsX:strideInPixelsY: instead
+ */
+-(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device NS_UNAVAILABLE;
+
+
+/*!
+ * NOTE:    The encodeToCommandBuffer API in MPSCNNKernel can be used to encode a MPSCNNPooling kernel
+ *          to a MTLCommandBuffer. The exact location of the pooling window for each output value is determined
+ *          as follows: The pooling window center for the first (top left) output pixel of the clipping
+ *          rectangle is at spatial coordinates (offset.x, offset.y) in the input image. From this
+ *          the top left corner of the pooling window is at
+ *              (offset.x - floor(kernelWidth/2), offset.y - floor(kernelHeight/2)) and
+ *          extends of course (kernelWidth, kernelHeight) pixels to the right and down direction, which means
+ *          that the last pixel to be included into the pooling window is at:
+ *              (offset.x + floor((kernelWidth-1)/2), offset.y + floor((kernelHeight-1)/2)),
+ *          so that for even kernel sizes the pooling window is extends one pixel more into the left and up
+ *          directions.
+ *          The following pooling windows can be then easily deduced from the first one by simple shifting
+ *          the source coordinates according to values of @ref strideInPixelsX and @ref strideInPixelsY.
+ *          For example the pooling window center w(x,y) for the output value at coordinate (x,y) of the
+ *          destination clip rectangle ((x,y) computed wrt. clipping rectangle origin) is at:
+ *              w(x,y) = ( offset.x + strideInPixelsX * x , offset.y + strideInPixelsY * y ).
+ *
+ *          Quite often it is desirable to distribute the pooling windows as evenly as possible in the
+ *          input image. As explained above, if offset is zero, then the center of the first pooling
+ *          window is at the top left corner of the input image, which means that the left and top stripes
+ *          of the pooling window are read from outside the input image boundaries (when filter size is
+ *          larger than unity). Also it may mean that some values from the bottom and right stripes are
+ *          not included at all in the pooling resulting in loss of valuable information.
+ *          A scheme used in some common libraries is to shift the source offset according to the following
+ *          formula:
+ *              offset.xy += (int)floor( ((L.xy - 1) % s.xy) / 2 ) + (int)floor( (f.xy-1) % 2 ), where
+ *          L is the size of the input image (or more accurately the size corresponding to the scaled cliprect
+ *          in source coordinates, which commonly coincides with the source image itself),
+ *          s.xy is (strideInPixelsX, strideInPixelsY) and f.xy is (kernelWidth, kernelHeight).
+ *          This offset distributes the pooling window centers evenly in the effective source cliprect
+ *          and is commonly used in CNN libraries.
+ */
+
+@end    /* MPSCNNPooling */
+
+
+/*!
+ *  @class MPSCNNPoolingMax
+ *  @dependency This depends on Metal.framework
+ *  @discussion Specifies the max pooling filter.  For each pixel, returns the maximum value of pixels
+ *              in the kernelWidth x kernelHeight filter region.
+ */
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
+@interface  MPSCNNPoolingMax : MPSCNNPooling
+@end    /* MPSCNNPoolingMax */
+
+
+/*!
+ *  @class MPSCNNPoolingAverage
+ *  @dependency This depends on Metal.framework
+ *  @discussion Specifies the average pooling filter.  For each pixel, returns the mean value of pixels
+ *              in the kernelWidth x kernelHeight filter region.
+ */
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
+@interface  MPSCNNPoolingAverage : MPSCNNPooling
+@end    /* MPSCNNPoolingAverage */
+
+
+
+#pragma mark MPSCNNNormalization
+
+/*!
+ *  @class MPSCNNSpatialNormalization
+ *  @dependency This depends on Metal.framework
+ *  @discussion Specifies the spatial normalization filter.
+ *              The spatial normalization for a feature channel applies the filter over local regions which extend
+ *              spatially, but are in separate feature channels (i.e., they have shape 1 x kernelWidth x kernelHeight).
+ *              For each feature channel, the function computes the sum of squares of X inside each rectangle, N2(i,j).
+ *              It then divides each element of X as follows:
+ *                  Y(i,j) = X(i,j) / (delta + alpha/(kw*kh) * N2(i,j))^beta,
+ *              where kw and kh are the kernelWidth and the kernelHeight.
+ *              It is the end-users responsibility to ensure that the combination of the
+ *              parameters delta and alpha does not result in a situation where the denominator
+ *              becomes zero - in such situations the resulting pixel-value is undefined.
+ */
+NS_CLASS_AVAILABLE( 10_12, 10_0 )
+@interface MPSCNNSpatialNormalization : MPSCNNKernel
+
+/*! @property   alpha
+ *  @abstract   The value of alpha.  Default is 1.0. Must be non-negative.
+ */
+@property (readwrite, nonatomic) float   alpha;
+
+/*! @property   beta
+ *  @abstract   The value of beta.  Default is 5.0
+ */
+@property (readwrite, nonatomic) float   beta;
+
+/*! @property   delta
+ *  @abstract   The value of delta.  Default is 1.0
+ */
+@property (readwrite, nonatomic) float   delta;
+
+/*! @property   kernelWidth
+ *  @abstract   The width of the filter window
+ */
+@property(readonly, nonatomic) NSUInteger       kernelWidth;
+
+/*! @property   kernelHeight
+ *  @abstract   The height of the filter window
+ */
+@property(readonly, nonatomic) NSUInteger       kernelHeight;
+
+/*!
+ *  @abstract  Initialize a spatial normalization filter
+ *  @param      device              The device the filter will run on
+ *  @param      kernelWidth         The width of the kernel
+ *  @param      kernelHeight        The height of the kernel
+ *  @return     A valid MPSCNNSpatialNormalization object or nil, if failure.
+ *
+ *  NOTE:  For now, kernelWidth must be equal to kernelHeight
+ */
+-(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
+                           kernelWidth: (NSUInteger) kernelWidth
+                          kernelHeight: (NSUInteger) kernelHeight NS_DESIGNATED_INITIALIZER;
+
+/*
+ * Use initWithDevice:kernelWidth:kernelHeight instead
+ */
+-(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device NS_UNAVAILABLE;
+
+/*!
+ * NOTE:    The encodeToCommandBuffer API in MPSUnaryImageKernel can be used to encode a
+ *          MPSCNNSpatialNormalization filter to a MTLCommandBuffer.
+ */
+@end    /* MPSCNNSpatialNormalization */
+
+/*!
+ *  @class MPSCNNLocalContrastNormalization
+ *  @dependency This depends on Metal.framework
+ *  @discussion Specifies the local contrast normalization filter.
+ *              The local contrast normalization is quite similar to spatial normalization
+ *              (see @ref MPSCNNSpatialNormalization) in that it applies the filter over local regions which extend
+ *              spatially, but are in separate feature channels (i.e., they have shape 1 x kernelWidth x kernelHeight),
+ *              but instead of dividing by the local "energy" of the feature, the denominator uses the local variance
+ *              of the feature - effectively the mean value of the feature is subtracted from the signal.
+ *              For each feature channel, the function computes the variance VAR(i,j) and
+ *              mean M(i,j) of X(i,j) inside each rectangle around the spatial point (i,j).
+ *
+ *              Then the result is computed for each element of X as follows:
+ *
+ *                  Y(i,j) = pm + ps * ( X(i,j) - p0 * M(i,j)) / (delta + alpha * VAR(i,j))^beta,
+ *
+ *              where kw and kh are the kernelWidth and the kernelHeight and pm, ps and p0 are parameters that
+ *              can be used to offset and scale the result in various ways. For example setting
+ *              pm=0, ps=1, p0=1, delta=0, alpha=1.0 and beta=0.5 scales input data so that the result has
+ *              unit variance and zero mean, provided that input variance is positive.
+ *              It is the end-users responsibility to ensure that the combination of the
+ *              parameters delta and alpha does not result in a situation where the denominator
+ *              becomes zero - in such situations the resulting pixel-value is undefined. A good way to guard
+ *              against tiny variances is to regulate the expression with a small value for delta, for example
+ *              delta = 1/1024 = 0.0009765625.
+ */
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
+@interface MPSCNNLocalContrastNormalization : MPSCNNKernel
+
+/*! @property   alpha
+ *  @abstract   The value of alpha.  Default is 1.0
+ */
+@property (readwrite, nonatomic) float   alpha;
+
+/*! @property   beta
+ *  @abstract   The value of beta.  Default is 0.5
+ */
+@property (readwrite, nonatomic) float   beta;
+
+/*! @property   delta
+ *  @abstract   The value of delta.  Default is 1/1024
+ */
+@property (readwrite, nonatomic) float   delta;
+
+/*! @property   p0
+ *  @abstract   The value of p0.  Default is 1.0
+ */
+@property (readwrite, nonatomic) float   p0;
+
+/*! @property   pm
+ *  @abstract   The value of pm.  Default is 0.0
+ */
+@property (readwrite, nonatomic) float   pm;
+
+/*! @property   ps
+ *  @abstract   The value of ps.  Default is 1.0
+ */
+@property (readwrite, nonatomic) float   ps;
+
+
+/*! @property   kernelWidth
+ *  @abstract   The width of the filter window
+ */
+@property(readonly, nonatomic) NSUInteger       kernelWidth;
+
+/*! @property   kernelHeight
+ *  @abstract   The height of the filter window
+ */
+@property(readonly, nonatomic) NSUInteger       kernelHeight;
+
+/*!
+ *  @abstract  Initialize a local contrast normalization filter
+ *  @param      device              The device the filter will run on
+ *  @param      kernelWidth         The width of the kernel
+ *  @param      kernelHeight        The height of the kernel
+ *  @return     A valid MPSCNNLocalContrastNormalization object or nil, if failure.
+ *
+ *  NOTE:  For now, kernelWidth must be equal to kernelHeight
+ */
+-(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
+                           kernelWidth: (NSUInteger) kernelWidth
+                          kernelHeight: (NSUInteger) kernelHeight NS_DESIGNATED_INITIALIZER;
+
+/*
+ * Use initWithDevice:kernelWidth:kernelHeight instead
+ */
+-(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device NS_UNAVAILABLE;
+
+/*!
+ * NOTE:    The encodeToCommandBuffer API in MPSUnaryImageKernel can be used to encode a
+ *          MPSCNNLocalContrastNormalization filter to a MTLCommandBuffer.
+ */
+@end    /* MPSCNNLocalContrastNormalization */
+
+
+/*!
+ *  @class MPSCNNCrossChannelNormalization
+ *  @dependency This depends on Metal.framework
+ *  @discussion Specifies the normalization filter across feature channels.
+ *               This normalization filter applies the filter to a local region across nearby feature channels,
+ *              but with no spatial extent (i.e., they have shape kernelSize x 1 x 1).
+ *              The normalized output is given by:
+ *                  Y(i,j,k) = X(i,j,k) / L(i,j,k)^beta,
+ *              where the normalizing factor is:
+ *                  L(i,j,k) = delta + alpha/N * (sum_{q in Q(k)} X(i,j,q)^2, where
+ *              N is the kernel size. The window Q(k) itself is defined as:
+ *                  Q(k) = [max(0, k-floor(N/2)), min(D-1, k+floor((N-1)/2)], where
+ *
+ *              k is the feature channel index (running from 0 to D-1) and
+ *              D is the number of feature channels, and alpha, beta and delta are paremeters.
+ *              It is the end-users responsibility to ensure that the combination of the
+ *              parameters delta and alpha does not result in a situation where the denominator
+ *              becomes zero - in such situations the resulting pixel-value is undefined.
+ */
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
+@interface MPSCNNCrossChannelNormalization : MPSCNNKernel
+
+/*! @property   alpha
+ *  @abstract   The value of alpha.  Default is 1.0. Must be non-negative.
+ */
+@property (readwrite, nonatomic) float   alpha;
+
+/*! @property   beta
+ *  @abstract   The value of beta.  Default is 5.0
+ */
+@property (readwrite, nonatomic) float   beta;
+
+/*! @property   delta
+ *  @abstract   The value of delta.  Default is 1.0
+ */
+@property (readwrite, nonatomic) float   delta;
+
+/*! @property   kernelSize
+ *  @abstract   The size of the square filter window.  Default is 5
+ */
+@property(readonly, nonatomic) NSUInteger       kernelSize;
+
+/*!
+ *  @abstract  Initialize a local response normalization filter in a channel
+ *  @param      device              The device the filter will run on
+ *  @param      kernelSize          The kernel filter size in each dimension.
+ *  @return     A valid MPSCNNCrossFeatureMapNormalization object or nil, if failure.
+ *
+ */
+-(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
+                            kernelSize: (NSUInteger) kernelSize NS_DESIGNATED_INITIALIZER;
+
+/*
+ * Use initWithDevice:kernelSize: instead
+ */
+-(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device NS_UNAVAILABLE;
+
+/*!
+ * NOTE:    The encodeToCommandBuffer API in MPSUnaryImageKernel can be used to encode a
+ *          MPSCNNCrossChannelNormalization filter to a MTLCommandBuffer.
+ */
+@end    /* MPSCNNCrossChannelNormalization */
+
+
+/*!
+ *  @class      MPSCNNSoftMax
+ *  @dependency This depends on Metal.framework
+ *  @discussion The softmax filter is a neural transfer function and is useful for classification tasks.
+ *              The softmax filter is applied across feature channels and in a convolutional manner at all
+ *              spatial locations. The softmax filter can be seen as the combination of an
+ *              activation function (exponential) and a normalization operator.
+ *              For each feature channel per pixel in an image in a feature map, the softmax filter computes the following:
+ *                  result channel in pixel = exp(pixel(x,y,k))/sum(exp(pixel(x,y,0)) ... exp(pixel(x,y,N-1))
+ *                      where N is the number of feature channels
+ *
+ */
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
+@interface MPSCNNSoftMax : MPSCNNKernel
+
+@end    /* MPSCNNSoftMax */
+
+#ifdef __cplusplus
+}       /* extern "C" */
+#endif
+
+
+#endif  /* MPS_MPSCNN_h */
+
+
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImage.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImage.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImage.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImage.h	2016-05-21 08:10:52.000000000 +0200
@@ -0,0 +1,403 @@
+/*!
+ *  @header MPSImage.h
+ *  @framework MetalPerformanceShaders.framework
+ *
+ *  @copyright Copyright (c) 2015 Apple Inc. All rights reserved.
+ *  @discussion A MPSImage is a MTLTexture abstraction that allows for more than 4 channels, and
+ *              for temporary images.
+ */
+
+#ifndef MPSImage_h
+#define MPSImage_h
+
+
+#include <MetalPerformanceShaders/MPSTypes.h>
+
+#ifdef __cplusplus
+extern "C" {
+#endif
+
+#pragma mark MPSImage
+
+/*!
+ *  @class      MPSImageDescriptor
+ *  @dependency This depends on Metal.framework
+ *  @abstract   A MPSImageDescriptor object describes a attributes of MPSImage and is used to
+ *              create one (see MPSImage discussion below)
+ */
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
+@interface MPSImageDescriptor : NSObject
+/*! @property   width
+ *  @abstract   The width of the CNN image.
+ *  @discussion The formal width of the CNN image in pixels.  Default = 1.
+ */
+@property (readwrite, nonatomic) NSUInteger width;
+
+/*! @property   height
+ *  @abstract   The height of the CNN image.
+ *  @discussion The formal height of the CNN image in pixels. Default = 1.
+ */
+@property (readwrite, nonatomic) NSUInteger height;
+
+/*! @property   featureChannels
+ *  @abstract   The number of feature channels per pixel.  Default = 1.
+ */
+@property (readwrite, nonatomic) NSUInteger featureChannels;
+
+/*! @property   numberOfImages
+ *  @abstract   The number of images for batch processing.   Default = 1.
+ */
+@property (readwrite, nonatomic) NSUInteger numberOfImages;
+
+/*! @property   pixelFormat
+ *  @abstract   The MTLPixelFormat expected for the underlying texture.
+ */
+@property (readonly, nonatomic) MTLPixelFormat pixelFormat;
+
+
+/*! @property   channelFormat
+ *  @abstract   The storage format to use for each channel in the image.
+ */
+@property (readwrite, nonatomic) MPSImageFeatureChannelFormat channelFormat;
+
+/*!
+ @property cpuCacheMode
+ @abstract Options to specify CPU cache mode of texture resource. Default = MTLCPUCacheModeDefaultCache
+ */
+@property (readwrite, nonatomic) MTLCPUCacheMode cpuCacheMode;
+
+/*!
+ @property storageMode
+ @abstract To specify storage mode of texture resource. 
+           Default = MTLStorageModeShared on iOS
+                     MTLStorageModeManaged on Mac OSX
+           MTLStorageModeShared not supported on Mac OSX. 
+           See Metal headers for synchronization requirements when using StorageModeManaged
+ */
+@property (readwrite, nonatomic) MTLStorageMode storageMode;
+
+/*!
+ *  @property   usage
+ *  @abstract   Description of texture usage.  Default = MTLTextureUsageShaderRead/Write
+ */
+@property (readwrite, nonatomic) MTLTextureUsage usage;
+
+/*! @abstract   Create a MPSImageDescriptor for a single read/write cnn image.
+ */
++(__nonnull instancetype) imageDescriptorWithChannelFormat: (MPSImageFeatureChannelFormat)channelFormat
+                                                     width: (NSUInteger)width
+                                                    height: (NSUInteger)height
+                                           featureChannels: (NSUInteger)featureChannels;
+
+/*! @abstract   Create a MPSImageDescriptor for a read/write cnn image with option to set usage and batch size (numberOfImages).
+ */
++(__nonnull instancetype) imageDescriptorWithChannelFormat: (MPSImageFeatureChannelFormat)channelFormat
+                                                     width: (NSUInteger)width
+                                                    height: (NSUInteger)height
+                                           featureChannels: (NSUInteger)featureChannels
+                                            numberOfImages: (NSUInteger)numberOfImages
+                                                     usage: (MTLTextureUsage)usage;
+
+@end
+
+typedef NS_ENUM(NSUInteger, MPSPurgeableState)
+{
+    MPSPurgeableStateAllocationDeferred MPS_ENUM_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0) = 0,                // The buffer hasn't been allocated yet. Attempts to set purgeability will be ignored.
+    MPSPurgeableStateKeepCurrent        MPS_ENUM_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0) = MTLPurgeableStateKeepCurrent,
+    
+    MPSPurgeableStateNonVolatile        MPS_ENUM_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0) = MTLPurgeableStateNonVolatile,
+    MPSPurgeableStateVolatile           MPS_ENUM_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0) = MTLPurgeableStateVolatile,
+    MPSPurgeableStateEmpty              MPS_ENUM_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0) = MTLPurgeableStateEmpty,
+} NS_ENUM_AVAILABLE(10_11, 8_0);
+
+/*!
+ *  @class      MPSImage
+ *  @dependency This depends on Metal.framework
+ *  @abstract   A MPSImage object describes a MTLTexture that may have more than 4 channels.
+ *  @discussion Some image types, such as those found in convolutional neural networks (CNN) 
+ *              image differs from a standard texture in that it may have more than 4 channels 
+ *              per image. While the channels could hold RGBA data, they will more commonly 
+ *              hold a number of structural permutations upon a RGBA image as the neural 
+ *              network progresses. It is not uncommon for each pixel to have 32 or 64 channels 
+ *              in it.
+ *
+ *              Since a standard MTLTexture may have no more than 4 channels, the additional
+ *              channels are stored in slices of 2d texture array (i.e. texture type is MTLTextureType2DArray) 
+ *              such that 4 consecutive channels are stored in each slice of this array.
+ *              If the number of feature channels is N, number of array slices needed is (N+3)/4.
+ *              E.g. a CNN image with width 3 and height 2 with 9 channels will be stored as
+ * 
+ *              slice 2         R???   R???   R???
+ *                              R???   R???   R???
+ *
+ *              slice 1      RGBA   RGBA   RGBA
+ *                           RGBA   RGBA   RGBA
+ *
+ *              slice 0   RGBA   RGBA  RGBA
+ *                        RGBA   RGBA  RGBA
+ *
+ *              Thus width and height of underlying 2d texture array is same as width and height of MPSImage
+ *              and array length is equal to (featureChannels + 3) / 4. Channels marked with ? are just
+ *              for padding and should not contain NaNs or Infs.
+ *
+ *              MPSImage can be container of multiple CNN images for batch processing. In order to create
+ *              MPSImage that contains N images, create MPSImageDescriptror with numberOfImages set to N.
+ *
+ *              Length of 2d texture array (i.e. number of slices) will be equal to ((featureChannels +3)/4)*numberOfImage
+ *              where consecutive (featureChannels+3)/4 slices of this array represent one image.
+ *
+ *              Although MPSImage can contain numberOfImages > 1, the actual number of images among these processed by MPSCNNKernel
+ *              is controlled by z-dimension of clipRect. MPSCNNKernel processes n=clipRect.size.depth images from this collection.
+ *              Starting index of image to process from source MPSImage is given by offset.z. Starting index of image in destination
+ *              MPSImage where this processed image is written to is given by clipRect.origin.z. Thus MPSCNNKernel takes n=clipRect.size.depth
+ *              image from source at indices [offset.z, offset.z+n], processed each independently and
+ *              stores the result in destination at indices [clipRect.origin.z, clipRect.origin.z+n] respectively.
+ *              Thus offset.z+n should be <= [src numberOfImage] and clipRect.origin.z+n should be <= [dest numberOfImages] and offset.z must
+ *              be >= 0. 
+ *              Example: Suppose MPSCNNConvolution takes an input image with 16 channels and outputs an image with 32 channels. This number of
+ *              slices needed in source 2d texture array is 2 and number of slices nneded in destination 2d array is 4. Suppose source batch size is
+ *              5 and desination batch size is 4. Thus number of source slices will be 2*5=10 and number of destination slices will be 4*4=16. If
+ *              you want to process image 2 and 3 of source and store the result at index 1 and 2 in destination, you can achieve this by setting
+ *              offset.z=2, clipRect.origin.z=1 and clipRect.size.depth=2. MPSCNNConvoluiton will take, in this case, slice 4 and 5 of source and
+ *              produce slice 4 to 7 of destination. Similarly slice 6 and 7 will be used to produce slice 8 to 11 of destination.
+ *
+ *              All MPSCNNKernels process images in the batch independently. That is, calling a MPSCNNKernel on an
+ *              batch is formally the same as calling it on each image in the batch sequentially.
+ *              Computational and GPU work submission overhead will be amortized over more work if batch processing is used. This is especially 
+ *              important for better performance on small images.
+ *
+ *              If the number of feature channel is <= 4 and numberOfImages=1 i.e. only one slice is needed by represent MPSImage, underlying
+ *              metal texture type is choosen to be MTLTextureType2D rather than MTLTextureType2DArray as explained above.
+ *
+ *              There are also MPSTemporaryImages,
+ *              intended for use for very short-lived image data that is produced and consumed
+ *              immediately in the same MTLCommandBuffer. They are a useful way to minimize CPU-side
+ *              texture allocation costs and greatly reduce the amount of memory used by your image
+ *              pipeline.
+ *
+ *              Creation of the underlying texture may in some cases occur lazily.  You should
+ *              in general avoid calling MPSImage.texture except when unavoidable to avoid
+ *              materializing memory for longer than necessary. When possible, use the other MPSImage
+ *              properties to get information about the MPSImage instead.
+ */
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
+@interface MPSImage :  NSObject
+
+/*! @property device
+ *  @abstract  The device on which the MPSImage will be used
+ */
+@property (readonly, retain, nonatomic, nonnull)  id <MTLDevice>    device;
+
+/*! @property   width
+ *  @abstract   The formal width of the image in pixels.
+ */
+@property (readonly, nonatomic) NSUInteger width;
+
+/*! @property   height
+ *  @abstract   The formal height of the image in pixels.
+ */
+@property (readonly, nonatomic) NSUInteger height;
+
+/*! @property   featureChannels
+ *  @abstract   The number of feature channels per pixel.
+ */
+@property (readonly, nonatomic) NSUInteger featureChannels;
+
+/*! @property   numberOfImages
+ *  @abstract   numberOfImages for batch processing
+ */
+@property (readonly, nonatomic) NSUInteger numberOfImages;
+
+/*! @property   textureType
+ *  @abstract   The type of the underlying texture, typically MTLTextureType2D
+ *              or MTLTextureType2DArray
+ */
+@property (readonly, nonatomic) MTLTextureType textureType;
+
+/*! @property   pixelFormat
+ *  @abstract   The MTLPixelFormat of the underlying texture
+ */
+@property (readonly, nonatomic) MTLPixelFormat pixelFormat;
+
+/*! @property   precision
+ *  @abstract   The number of bits of numeric precision available for each feature channel.
+ *  @discussion This is precision, not size.  That is, float is 24 bits, not 32. half
+ *              precision floating-point is 11 bits, not 16. SNorm formats have one less
+ *              bit of precision for the sign bit, etc. For formats like MTLPixelFormatB5G6R5Unorm
+ *              it is the precision of the most precise channel, in this case 6.  When this
+ *              information is unavailable, typically compressed formats, 0 will be returned.
+ */
+@property (readonly, nonatomic) NSUInteger precision;
+
+/*!
+ *  @property   usage
+ *  @abstract   Description of texture usage.
+ */
+@property (readonly, nonatomic) MTLTextureUsage usage;
+
+/*!
+ *  @property   pixelSize
+ *  @abstract   Number of bytes from the first byte of one pixel to the first byte of the next 
+ *              pixel in storage order.  (Includes padding.)
+ */
+@property (readonly, nonatomic) size_t  pixelSize;
+
+
+/*! @property   texture
+ *  @abstract   The associated MTLTexture object.
+ *              This is a 2D texture if numberOfImages is 1 and number of feature channels <= 4.
+ *              It is a 2D texture array otherwise.
+ *  @discussion To avoid the high cost of premature allocation of the underlying texture, avoid calling this
+ *              property except when strictly necessary. [MPSCNNKernel encode...] calls typically cause
+ *              their arguments to become allocated. Likewise, MPSImages initialized with -initWithTexture:
+ *              featureChannels: have already been allocated.
+ */
+@property (readonly, nonnull, nonatomic) id <MTLTexture> texture;
+
+/*!
+ @property label
+ @abstract A string to help identify this object.
+ */
+@property (copy, atomic, nullable)  NSString *label;
+
+/*!
+ *  @abstract   Initialize a MPSImage object using a metal texture
+ *  @param      texture         The MTLTexture allocated by the developer to be used as backing for MPSImage.
+ *  @return     A valid MPSImage object or nil, if failure.
+ *  @discussion  The number of featureChannels in the image will be inferred from the number of channels in
+ *               the texture.pixelFormat. The number of feature channels must be between 1 and 4.
+ *
+ *               This is a convenience method intended for MTLTextures containing typical image data 
+ *               which application may obtain from MetalKit or other libraries such as that drawn from a JPEG or PNG,
+ *               The number of feature channels shall be equal to the number of color channels
+ *               in the MTLPixelFormat. If texture.textureType == MTLTextureType2DArray, numberOfImages is
+ *               set to texture.arrayLength
+ */
+-(nonnull instancetype) initWithTexture: (nonnull id <MTLTexture>) texture;
+
+/*!
+ *  @abstract   Initialize an empty image object
+ *  @param      device              The device that the image will be used. May not be NULL.
+ *  @param      imageDescriptor     The MPSImageDescriptor. May not be NULL.
+ *  @return     A valid MPSImage object or nil, if failure.
+ *  @discussion Storage to store data needed is allocated lazily on first use of MPSImage or
+ *              when application calls MPSImage.texture
+ *
+ */
+-(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
+                       imageDescriptor: (const MPSImageDescriptor * __nonnull) imageDescriptor;
+/*!
+ *  @method         setPurgeableState
+ *  @abstract       Set (or query) the purgeability state of a MPSImage
+ *  @discussion     Usage is per [MTLResource setPurgeableState:], except that the MTLTexture might be
+ *                  MPSPurgeableStateAllocationDeferred, which means there is no texture to mark volatile / nonvolatile.
+ *                  Attempts to set purgeability on MTLTextures that have not been allocated will be ignored.
+ */
+- (MPSPurgeableState)setPurgeableState:(MPSPurgeableState)state;
+
+/*
+ * Use initWithDevice:texture: or initWithDevice:imageDescriptor: instead
+ */
+-(nonnull instancetype) init NS_UNAVAILABLE;
+
+@end
+
+/*!
+ *  @class      MPSTemporaryImage
+ *  @dependency MPSImage
+ *  @discussion MPSTemporaryImages are provided as a fast way to store intermediate data
+ *              that will be used promptly and discarded.
+ *
+ *              MPSTemporaryImages use an internal cache of preallocated reusable memory
+ *              to hold pixel data to avoid typical memory allocation performance penalties
+ *              common to ordinary MPSImages and MTLTextures.  Multiple MPSTemporaryImages
+ *              in the same MTLCommandBuffer can alias the same overlapping piece of memory.
+ *              This avoids the CPU cost of allocating memory and can greatly reduce the
+ *              overall memory footprint.
+ *
+ *              To avoid data corruption, MPSTemporaryImages impose some restrictions:
+ *
+ *              - The textures are MTLStorageModePrivate.
+ *
+ *              - The temporary image may not be used on any other MTLCommandBuffer.
+ *
+ *              - The MPSTemporaryImage must be used by the same thread as the
+ *                one managing the MTLCommandBuffer on which it is created.
+ *
+ *              - You must release the MPSTemporaryImage immediately so that its memory
+ *                can be reused. If sufficient reusable memory is not available for the next
+ *                MPSTemporaryImage on the MTLCommandBuffer, new memory will be allocated
+ *                and any performance benefits are lost.
+ *
+ *              - see also pixel format restrictions for MPSImages in general.
+ *
+ *              You may have more than one MPSTemporaryImage allocated concurrently.
+ *
+ *              You may use the MPSTemporaryImage.texture with non-CNN MPSKernel -encode... methods,
+ *              iff featureChannels <= 4 and the MTLTexture conforms to requirements of that MPSKernel.
+ */
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
+@interface  MPSTemporaryImage : MPSImage
+
+/*!
+ *  @abstract   Initialize a MPSTemporaryImage for use on a MTLCommandBuffer
+ *
+ *  @discussion MPSTemporaryImages aggresively reuse cached memory to avoid expensive
+ *              allocation and deallocation of texture memory. They are intended to be used
+ *              to hold short-lived CNN image data, typically for image data that is produced
+ *              then consumed immediately and needed no further.
+ *
+ *              Please see MPSTemporaryImage and MPSImage class documentation for
+ *              important restrictions.
+ *
+ *  @param      commandBuffer       The MTLCommandBuffer on which the MPSTemporaryImage will be exclusively used
+ *
+ *  @param      imageDescriptor  A valid imageDescriptor describing the MPSImage format to create.
+ *
+ *  @result     A valid MPSTemporaryImage.  The image is MTLStorageModePrivate. It becomes
+ *              invalid when the MTLCommandBuffer is committed. In order to receive the intended
+ *              performance advantages of the MPSTemporaryImage, it should in general
+ *              be released within a few lines of code of its allocation.
+ *
+ *              Note: the allocation of the underlying MTLTexture object is deferred until
+ *                    it is needed.  You should in general refrain from calling
+ *                    MPSTemporaryImage.texture, as this could force the texture to
+ *                    have a lifetime longer than it should otherwise.
+ */
+-(nonnull instancetype) initForCommandBuffer: (nonnull id <MTLCommandBuffer>) commandBuffer
+                             imageDescriptor: (const MPSImageDescriptor * __nonnull) imageDescriptor;
+
+
+/*!
+ *  @abstract       Low level interface for creating a MPSTemporaryImage using a MTLTextureDescriptor
+ *  @discussion     This function provides access to MTLPixelFormats not typically covered by -initForCommandBuffer:imageDescriptor:
+ *                  The feature channels will be inferred from the MTLPixelFormat without changing the width. 
+ *                  The following restrictions apply:
+ *  
+ *                      MTLTextureType must be MTLTextureType2D or MTLTextureType2DArray
+ *                      MTLTextureUsage must contain at least one of MTLTextureUsageShaderRead, MTLTextureUsageShaderWrite
+ *                      MTLStorageMode must be MTLStorageModePrivate
+ *                      depth must be 1
+ *
+ *
+ */
+-(nonnull instancetype) initForCommandBuffer: (nonnull id <MTLCommandBuffer>) commandBuffer
+                           textureDescriptor: (const MTLTextureDescriptor * __nonnull) textureDescriptor;
+
+
+/*! Unavailable. Use initForCommandBuffer:textureDescriptor: or -initForCommandBuffer:imageDescriptor: instead. */
+-(nonnull instancetype) initWithTexture: (nonnull id <MTLTexture>) texture
+                        featureChannels: (NSUInteger) featureChannels  NS_UNAVAILABLE;
+
+/*! Unavailable. Use initForCommandBuffer:imageDescriptor: instead. */
+-(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
+                       imageDescriptor: (const MPSImageDescriptor * __nonnull) imageDescriptor      NS_UNAVAILABLE;
+
+@end
+
+#ifdef __cplusplus
+}   // extern "C"
+#endif
+
+
+#endif /* MPSImage_h */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageConversion.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageConversion.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageConversion.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageConversion.h	2016-05-21 08:10:52.000000000 +0200
@@ -0,0 +1,70 @@
+/*!
+ *  @header MPSConversions.h
+ *  @framework MetalPerformanceShaders.framework
+ *
+ *  @copyright Copyright (c) 2015 Apple Inc. All rights reserved.
+ *  @abstract MetalPerformanceShaders conversion filters
+ *  @ignorefuncmacro MPS_CLASS_AVAILABLE_STARTING
+ */
+
+#ifndef MPS_Conversions_h
+#define MPS_Conversions_h
+
+#include <MetalPerformanceShaders/MPSImageKernel.h>
+
+#include <CoreGraphics/CGColorConverter.h>
+
+
+/*!
+ *  @class      MPSImageConversion
+ *  @discussion The MPSImageConversion filter performs a conversion from source to destination
+ *
+ */
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
+@interface  MPSImageConversion : MPSUnaryImageKernel
+
+/*! @property   sourceAlpha
+ *  @abstract   Premultiplication description for the source texture
+ *  @discussion Most colorspace conversion operations can not work directly on premultiplied data.
+ *              Use this property to tag premultiplied data so that the source texture can
+ *              be unpremultiplied prior to application of these transforms. 
+ *              Default: MPSPixelAlpha_AlphaIsOne
+ */
+@property (readonly, nonatomic) MPSAlphaType sourceAlpha;
+
+/*! @property   destinationAlpha
+ *  @abstract   Premultiplication description for the destinationAlpha texture
+ *  @discussion Colorspace conversion operations produce non-premultiplied data.
+ *              Use this property to tag cases where premultiplied results are required.
+ *              If MPSPixelAlpha_AlphaIsOne is used, the alpha channel will be set to 1. 
+ *              Default: MPSPixelAlpha_AlphaIsOne
+ */
+@property (readonly, nonatomic) MPSAlphaType destinationAlpha;
+
+
+
+/*!
+ *  @abstract   Create a converter that can convert texture colorspace, alpha and texture format
+ *  @discussion Create a converter that can convert texture colorspace, alpha and MTLPixelFormat. 
+ *              Optimized cases exist for NULL color space converter and no alpha conversion.
+ *  @param      device              The device the filter will run on
+ *  @param      srcAlpha            The alpha encoding for the source texture
+ *  @param      destAlpha           The alpha encoding for the destination texture
+ *  @param      backgroundColor     An array of CGFloats giving the background color to use when flattening an image.
+ *                                  The color is in the source colorspace.  The length of the array is the number 
+ *                                  of color channels in the src colorspace. If NULL, use {0}.
+ *  @param      colorConverter      The colorspace converter to use. May be NULL, indicating no
+ *                                  color space conversions need to be done.
+ *
+ *  @result     An initialized MPSImageConversion object.
+ */
+-(nonnull instancetype) initWithDevice:(nonnull id<MTLDevice>)device
+                              srcAlpha:(MPSAlphaType) srcAlpha
+                             destAlpha:(MPSAlphaType) destAlpha
+                       backgroundColor:(nullable CGFloat*) backgroundColor
+                        colorConverter:(nullable CGColorConverterRef) colorConverter;
+
+
+@end  /* MPSImageConversion */
+
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageConvolution.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageConvolution.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageConvolution.h	2015-10-02 23:45:19.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageConvolution.h	2016-05-21 08:10:52.000000000 +0200
@@ -14,9 +14,15 @@
 /*!
  *  @class      MPSImageConvolution
  *  @discussion The MPSImageConvolution convolves an image with given filter of odd width and height.
- *              Filter width/height can be either 3,5,7 or 9.
- *              For a separable filter, it will be more performant to run this filter as a 1-dimensional
- *              filter in each dimension separately.
+ *              The center of the kernel aligns with the MPSImageConvolution.offset. That is, the position 
+ *              of the top left corner of the area covered by the kernel is given by 
+ *              MPSImageConvolution.offset - {kernel_width>>1, kernel_height>>1, 0}
+ *
+ *              Optimized cases include 3x3,5x5,7x7,9x9,11x11, 1xN and Nx1. If a convolution kernel 
+ *              does not fall into one of these cases but is a rank-1 matrix (a.k.a. separable)
+ *              then it will fall on an optimzied separable path. Other convolutions will execute with
+ *              full MxN complexity.
+ *
  *              If there are multiple channels in the source image, each channel is processed independently.
  *  
  *  @performance Separable convolution filters may perform better when done in two passes. A convolution filter
@@ -39,7 +45,7 @@
  *
  */
 
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageConvolution : MPSUnaryImageKernel
 
 /*! @property kernelHeight
@@ -78,8 +84,37 @@
 -(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
                            kernelWidth: (NSUInteger)kernelWidth
                           kernelHeight: (NSUInteger)kernelHeight
-                               weights: (nonnull const float*)kernelWeights     NS_DESIGNATED_INITIALIZER;
+                               weights: (const float*__nonnull)kernelWeights     NS_DESIGNATED_INITIALIZER;
+
+
+@end
+
 
+/*!
+ *  @class      MPSImageLaplacian
+ *  @discussion The MPSImageLaplacian is an optimized variant of the MPSImageConvolution filter provided primarily for ease of use.
+ *              This filter uses an optimized convolution filter with a 3 x 3 kernel with the following weights:
+ *                  [ 0  1  0
+ *                    1 -4  1
+ *                    0  1  0 ]
+ *
+ *              The optimized convolution filter used by MPSImageLaplacian can also be used by creating a MPSImageConvolution
+ *              object with kernelWidth = 3, kernelHeight = 3 and weights as specified above.
+ */
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
+@interface  MPSImageLaplacian : MPSUnaryImageKernel
+
+/*! @property    bias
+ *  @discussion  The bias is a value to be added to convolved pixel before it is converted back to the storage format.
+ *               It can be used to convert negative values into a representable range for a unsigned MTLPixelFormat.
+ *               For example, many edge detection filters produce results in the range [-k,k]. By scaling the filter
+ *               weights by 0.5/k and adding 0.5, the results will be in range [0,1] suitable for use with unorm formats.
+ *               It can be used in combination with renormalization of the filter weights to do video ranging as part
+ *               of the convolution effect. It can also just be used to increase the brightness of the image.
+ *
+ *               Default value is 0.0f.
+ */
+@property (readwrite, nonatomic) float bias;
 
 @end
 
@@ -88,12 +123,12 @@
  *  @class      MPSImageBox
  *  @discussion The MPSImageBox convolves an image with given filter of odd width and height. The kernel elements
  *              all have equal weight, achieving a blur effect. (Each result is the unweighted average of the
- *              surrounding pixels.) This allows for much faster algorithms, espcially for for larger blur radii.
+ *              surrounding pixels.) This allows for much faster algorithms, espcially for larger blur radii.
  *              The box height and width must be odd numbers. The box blur is a separable filter. The implementation 
  *              is aware of this and will act accordingly to give best performance for multi-dimensional blurs.
  */
 
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageBox : MPSUnaryImageKernel
 
 
@@ -152,6 +187,7 @@
  *              The tent blur is a separable filter. The implementation is aware of this and will act accordingly
  *              to give best performance for multi-dimensional blurs.
  */
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface MPSImageTent : MPSImageBox
 
 @end
@@ -169,7 +205,7 @@
  *                  to be suitable for all common image processing needs demanding ~10 bits of precision or
  *                  less.
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageGaussianBlur : MPSUnaryImageKernel
 
 /*! @abstract   Initialize a gaussian blur filter for a particular sigma and device
@@ -208,7 +244,7 @@
  *
  *                  Luminance = v[0] * pixel.x + v[1] * pixel.y + v[2] * pixel.z;
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageSobel : MPSUnaryImageKernel
 
 /*! @abstract   Initialize a Sobel filter on a given device using the default color 
@@ -230,7 +266,7 @@
  *  @return     A valid object or nil, if failure.
  */
 -(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
-              linearGrayColorTransform: (nonnull const float *) transform      NS_DESIGNATED_INITIALIZER;
+              linearGrayColorTransform: (const float * __nonnull) transform      NS_DESIGNATED_INITIALIZER;
 
 /*! @property    colorTransform
  *  @discussion  Returns a pointer to the array of three floats used to convert RGBA, RGB or RG images
@@ -240,4 +276,116 @@
 
 @end  /* MPSImageSobel */
 
+
+
+/*!
+ *  @class      MPSImagePyramid
+ *  @discussion The MPSImagePyramid is a base class for creating different kinds of pyramid images
+ *
+ *              Currently supported pyramid-types are:
+ *              @ref MPSImageGaussianPyramid
+ *
+ *              The Gaussian image pyramid kernel is enqueued as a in-place operation using
+ *              @ref MPSUnaryImageKernel::encodeToCommandBuffer:inPlaceTexture:fallbackCopyAllocator:
+ *              and all mipmap levels after level=1, present in the provided image are filled using
+ *              the provided filtering kernel. The fallbackCopyAllocator parameter is not used.
+ *
+ *              The Gaussian image pyramid filter ignores @ref clipRect and @ref offset and fills
+ *              the entire mipmap levels.
+ *
+ *  @note       Make sure your texture type is compatible with mipmapping and supports texture views
+ *                  (see @ref MTLTextureUsagePixelFormatView).
+ *  @note       Recall the size of the nth mipmap level:
+ *              @code
+ *                  w_n = max(1, floor(w_0 / 2^n))
+ *                  h_n = max(1, floor(h_0 / 2^n)),
+ *              @endcode
+ *              where w_0, h_0 are the zeroth level width and height. ie the image dimensions themselves.
+ */
+
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
+@interface  MPSImagePyramid : MPSUnaryImageKernel
+
+/*! @abstract   Initialize a downwards 5-tap image pyramid with the default filter kernel and device
+ *  @param      device  The device the filter will run on
+ *
+ *  @discussion The filter kernel is the outer product of w = [ 1/16,  1/4,  3/8,  1/4,  1/16 ]^T, with itself
+ *
+ *  @return     A valid object or nil, if failure.
+ */
+
+-(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device;
+
+
+/*! @abstract   Initialize a downwards 5-tap image pyramid with a central weight parameter and device
+ *  @param      device  The device the filter will run on
+ *  @param      centerWeight Defines form of the filter-kernel  through the outer product ww^T, where
+ *              w = [ (1/4 - a/2),  1/4,  a,  1/4,  (1/4 - a/2) ]^T and 'a' is centerWeight.
+ *
+ *  @return     A valid object or nil, if failure.
+ */
+
+-(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
+                          centerWeight: (float) centerWeight;
+
+
+/*! @abstract   Initialize a downwards n-tap pyramid with a custom filter kernel and device
+ *  @param      device  The device the filter will run on
+ *  @param      kernelWidth The width of the filtering kernel. See @ref MPSImageConvolution.
+ *  @param      kernelHeight    The height of the filtering kernel. See @ref MPSImageConvolution.
+ *  @param      kernelWeights   A pointer to an array of kernelWidth * kernelHeight values to be
+ *                              used as the kernel.
+ *                              These are in row major order. See @ref MPSImageConvolution.
+ *
+ *  @return     A valid object or nil, if failure.
+ */
+
+-(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
+                           kernelWidth: (NSUInteger)kernelWidth
+                          kernelHeight: (NSUInteger)kernelHeight
+                               weights: (const float*__nonnull)kernelWeights NS_DESIGNATED_INITIALIZER;
+
+
+/*! @property kernelHeight
+ *  @abstract  The height of the filter window. Must be an odd number.
+ */
+@property (readonly, nonatomic)   NSUInteger  kernelHeight;
+
+/*! @property kernelWidth
+ *  @abstract  The width of the filter window. Must be an odd number.
+ */
+@property (readonly, nonatomic)   NSUInteger  kernelWidth;
+
+
+
+@end
+
+/*!
+ *  @class      MPSImageGaussianPyramid
+ *  @discussion The Gaussian image pyramid is constructed as follows:
+ *              First the zeroth level mipmap of the input image is filtered with the specified
+ *              convolution kernel.
+ *              The default the convolution filter kernel is
+ *              @code
+ *                  k = w w^T, where w = [ 1/16,  1/4,  3/8,  1/4,  1/16 ]^T,
+ *              @endcode
+ *              but the user may also tweak this kernel with a @ref centerWeight parameter: 'a':
+ *              @code
+ *                  k = w w^T, where w = [ (1/4 - a/2),  1/4,  a,  1/4,  (1/4 - a/2) ]^T
+ *              @endcode
+ *              or the user can provide a completely custom kernel. After this the image is downsampled by
+ *              removing all odd rows and columns, which defines the next level in the Gaussian image pyramid.
+ *              This procedure is continued until every mipmap level present in the image texture are
+ *              filled with the pyramid levels.
+ *
+ *              In case of the Gaussian pyramid the user must run the operation in-place using:
+ *              @ref MPSUnaryImageKernel::encodeToCommandBuffer:inPlaceTexture:fallbackCopyAllocator:,
+ *              where the fallback allocator is ignored.
+ */
+
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
+@interface  MPSImageGaussianPyramid : MPSImagePyramid
+@end
+
+
 #endif    /* MPS_MSImageConvolution_h */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageHistogram.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageHistogram.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageHistogram.h	2015-10-02 23:45:19.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageHistogram.h	2016-05-21 08:10:52.000000000 +0200
@@ -3,7 +3,7 @@
  *  @framework MetalPerformanceShaders.framework
  *
  *  @copyright Copyright (c) 2015 Apple Inc. All rights reserved.
- *  @abstract Metal Image histogram filters
+ *  @abstract MetalPerformanceShaders histogram filters
  */
 
 #ifndef MPS_MPSImageHistogram_h
@@ -28,14 +28,14 @@
  *  @discussion The MPSImageHistogram computes the histogram of an image.
  *              
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageHistogram : MPSKernel
 
 /*! @property   clipRectSource
  *  @abstract   The source rectangle to use when reading data.
  *  @discussion A MTLRegion that indicates which part of the source to read. If the clipRectSource does not lie
  *              completely within the source image, the intersection of the image bounds and clipRectSource will
- *              be used. The clipRectSource replaces the MPSUnaryImageKernel origin parameter for this filter.
+ *              be used. The clipRectSource replaces the MPSUnaryImageKernel offset parameter for this filter.
  *              The latter is ignored.   Default: MPSRectNoClip, use the entire source texture.
  */
 @property (readwrite, nonatomic) MTLRegion clipRectSource;
@@ -62,7 +62,7 @@
  */
 
 -(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
-                         histogramInfo: (nonnull const MPSImageHistogramInfo *) histogramInfo     NS_DESIGNATED_INITIALIZER;
+                         histogramInfo: (const MPSImageHistogramInfo * __nonnull) histogramInfo     NS_DESIGNATED_INITIALIZER;
 
 
 /*!
@@ -128,7 +128,7 @@
  *              they will probably not be equalized by it.) This filter usually will not be able 
  *              to work in place.
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageHistogramEqualization : MPSUnaryImageKernel
 
 /*! @property   histogramInfo
@@ -146,7 +146,7 @@
  */
 
 -(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
-                         histogramInfo: (nonnull const MPSImageHistogramInfo *) histogramInfo     NS_DESIGNATED_INITIALIZER;
+                         histogramInfo: (const MPSImageHistogramInfo * __nonnull) histogramInfo     NS_DESIGNATED_INITIALIZER;
 
 /*!
  *  @abstract Encode the transform function to a command buffer using a MTLComputeCommandEncoder.
@@ -186,7 +186,7 @@
  *              converts the image so that its histogram matches the desired histogram.
  *
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageHistogramSpecification : MPSUnaryImageKernel
 
 /*! @property   histogramInfo
@@ -228,7 +228,7 @@
  */
 
 -(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
-                         histogramInfo: (nonnull const MPSImageHistogramInfo *) histogramInfo     NS_DESIGNATED_INITIALIZER;
+                         histogramInfo: (const MPSImageHistogramInfo * __nonnull) histogramInfo     NS_DESIGNATED_INITIALIZER;
 
 
 /*!
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageIntegral.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageIntegral.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageIntegral.h	2015-10-02 23:45:19.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageIntegral.h	2016-05-21 08:10:52.000000000 +0200
@@ -24,7 +24,7 @@
  *              If the channels in the source image are integer values, it is recommended that
  *              an appropriate 32-bit integer image destination format is used.
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageIntegral : MPSUnaryImageKernel
 
 @end    /* MPSImageIntegral */
@@ -43,7 +43,7 @@
  *              If the channels in the source image are integer values, it is recommended that
  *              an appropriate 32-bit integer image destination format is used.
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageIntegralOfSquares : MPSUnaryImageKernel
 
 @end    /* MPSImageIntegralOfSquares */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageKernel.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageKernel.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageKernel.h	2015-10-02 23:45:19.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageKernel.h	2016-05-21 08:10:52.000000000 +0200
@@ -16,7 +16,7 @@
  *  @dependency This depends on Metal.framework
  *  @discussion A MPSUnaryImageKernel consumes one MTLTexture and produces one MTLTexture.
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface MPSUnaryImageKernel : MPSKernel
 
 
@@ -191,7 +196,7 @@
  *  @dependency This depends on Metal.framework
  *  @discussion A MPSBinaryImageKernel consumes two MTLTextures and produces one MTLTexture.
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface MPSBinaryImageKernel : MPSKernel
 
 /*! @property   primaryOffset
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageMedian.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageMedian.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageMedian.h	2015-10-02 23:45:19.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageMedian.h	2016-05-21 08:10:52.000000000 +0200
@@ -22,7 +22,7 @@
  *              NOTE: The MPSImageMedian filter currently only supports images with <= 8 bits/channel.
  *
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageMedian : MPSUnaryImageKernel
 
 /*! @property   kernelDiameter
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageMorphology.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageMorphology.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageMorphology.h	2015-10-02 23:45:19.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageMorphology.h	2016-05-21 08:10:52.000000000 +0200
@@ -18,7 +18,7 @@
  *              in the source image. If there are multiple channels in the source image, each channel is processed independently.
  *              The edgeMode property is assumed to always be MPSImageEdgeModeClamp for this filter.
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageAreaMax : MPSUnaryImageKernel
 
 /*! @property kernelHeight
@@ -54,14 +54,14 @@
  *               It has the same methods as MPSImageAreaMax
  *               The edgeMode property is assumed to always be MPSImageEdgeModeClamp for this filter.
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageAreaMin : MPSImageAreaMax
 
 @end  /* MPSImageAreaMin */
 
 /*!
  *  @class      MPSImageDilate
- *  @discussion The MIDilateFilter finds the maximum pixel value in a rectangular region centered around each pixel in the
+ *  @discussion The MPSImageDilate finds the maximum pixel value in a rectangular region centered around each pixel in the
  *              source image. It is like the MPSImageAreaMax, except that the intensity at each position is calculated relative
  *              to a different value before determining which is the maximum pixel value, allowing for shaped, non-rectangular
  *              morphological probes.
@@ -78,7 +78,7 @@
  *
  *              The edgeMode property is assumed to always be MPSImageEdgeModeClamp for this filter.
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageDilate : MPSUnaryImageKernel
 /*! @property kernelHeight
  *  @abstract  The height of the filter window. Must be an odd number.
@@ -112,7 +112,7 @@
 -(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
                            kernelWidth: (NSUInteger)kernelWidth
                           kernelHeight: (NSUInteger)kernelHeight
-                                values: (nonnull const float*) values       NS_DESIGNATED_INITIALIZER;
+                                values: (const float* __nonnull) values       NS_DESIGNATED_INITIALIZER;
 
 /* You must use initWithDevice:kernelWidth:kernelHeight:values: instead. */
 -(nonnull instancetype) initWithDevice:(nonnull id<MTLDevice>)device        NS_UNAVAILABLE;
@@ -137,11 +137,11 @@
  *              A filter that contains all zeros is identical to a MPSImageAreaMin filter. The center filter element
  *              is assumed to be 0, to avoid causing a general lightening of the image.
  *
- *              The definition of the filter for MPSImageErode is different from vImage. (MIErode_filter_value = 1.0f-vImageErode_filter_value.)
+ *              The definition of the filter for MPSImageErode is different from vImage. (MPSErode_filter_value = 1.0f-vImageErode_filter_value.)
  *              This allows MPSImageDilate and MPSImageErode to use the same filter, making open and close operators easier to write.
  *              The edgeMode property is assumed to always be MPSImageEdgeModeClamp for this filter.
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageErode : MPSImageDilate
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageResampling.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageResampling.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageResampling.h	2015-10-02 23:45:19.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageResampling.h	2016-05-21 07:59:09.000000000 +0200
@@ -3,7 +3,7 @@
  *  @framework MetalPerformanceShaders
  *
  *  @copyright Copyright (c) 2015 Apple Inc. All rights reserved.
- *  @abstract  Resampling filters for Metal Image
+ *  @abstract  Resampling filters for MetalPerformanceShaders
  */
 
 #ifndef MPS_MPSImageResampling_h
@@ -25,7 +25,7 @@
  *              Because the resampling function has negative lobes, Lanczos can result 
  *              in ringing near sharp edges, making it less suitable for vector art.
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageLanczosScale : MPSUnaryImageKernel
 
 /*! @property   scaleTransform
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageThreshold.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageThreshold.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageThreshold.h	2015-10-02 23:45:19.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageThreshold.h	2016-05-21 08:10:52.000000000 +0200
@@ -3,7 +3,7 @@
  *  @framework MetalPerformanceShaders
  *
  *  @copyright Copyright (c) 2015 Apple Inc. All rights reserved.
- *  @abstract Metal Image thresholding filters
+ *  @abstract MetalPerformanceShaders thresholding filters
  */
 
 #ifndef MPS_MPSImageThreshold_h
@@ -13,14 +13,14 @@
 
 /*!
  *  @class      MPSImageThresholdBinary
- *  @discussion The MIThreshold filter applies a fixed-level threshold to each pixel in the image.
+ *  @discussion The MPSThreshold filter applies a fixed-level threshold to each pixel in the image.
  *              The threshold functions convert a single channel image to a binary image.
  *              If the input image is not a single channel image, convert the inputimage to a single channel
  *              luminance image using the linearGrayColorTransform and then apply the threshold.
  *              The ThresholdBinary function is:
  *                  destinationPixelValue = sourcePixelValue > thresholdValue ? maximumValue : 0
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageThresholdBinary : MPSUnaryImageKernel
 
 /*!
@@ -34,7 +34,7 @@
 -(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
                         thresholdValue: (float)thresholdValue
                           maximumValue: (float)maximumValue
-              linearGrayColorTransform: (nullable const float *)transform       NS_DESIGNATED_INITIALIZER;
+              linearGrayColorTransform: (const float * __nullable)transform       NS_DESIGNATED_INITIALIZER;
 
 /* You must use initWithDevice:thresholdValue:maximumValue:linearGrayColorTransform: instead */
 -(nonnull instancetype) initWithDevice:(nonnull id<MTLDevice>)device            NS_UNAVAILABLE;
@@ -66,7 +66,7 @@
  *              The ThresholdBinaryInverse function is:
  *                  destinationPixelValue = sourcePixelValue > thresholdValue ? 0 : maximumValue
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageThresholdBinaryInverse : MPSUnaryImageKernel
 
 /*!
@@ -80,7 +80,7 @@
 -(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
                         thresholdValue: (float)thresholdValue
                           maximumValue: (float)maximumValue
-              linearGrayColorTransform: (nullable const float *)transform       NS_DESIGNATED_INITIALIZER;
+              linearGrayColorTransform: (const float * __nullable)transform       NS_DESIGNATED_INITIALIZER;
 
 /* You must use initWithDevice:thresholdValue:maximumValue:linearGrayColorTransform: instead */
 -(nonnull instancetype) initWithDevice:(nonnull id<MTLDevice>)device            NS_UNAVAILABLE;
@@ -111,7 +111,7 @@
  *              The ThresholdTruncate function is:
  *                  destinationPixelValue = sourcePixelValue > thresholdValue ? thresholdValue : sourcePixelValue
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageThresholdTruncate : MPSUnaryImageKernel
 
 /*! 
@@ -123,7 +123,7 @@
  */
 -(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
                         thresholdValue: (float)thresholdValue
-              linearGrayColorTransform: (nullable const float *)transform       NS_DESIGNATED_INITIALIZER;
+              linearGrayColorTransform: (const float * __nullable)transform       NS_DESIGNATED_INITIALIZER;
 
 /* You must use initWithDevice:thresholdValue:linearGrayColorTransform: instead */
 -(nonnull instancetype) initWithDevice:(nonnull id<MTLDevice>)device            NS_UNAVAILABLE;
@@ -150,7 +150,7 @@
  *              The ThresholdToZero function is:
  *                  destinationPixelValue = sourcePixelValue > thresholdValue ? sourcePixelValue : 0
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageThresholdToZero : MPSUnaryImageKernel
 
 /*!
@@ -162,7 +162,7 @@
  */
 -(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
                         thresholdValue: (float)thresholdValue
-              linearGrayColorTransform: (nullable const float *)transform       NS_DESIGNATED_INITIALIZER;
+              linearGrayColorTransform: (const float * __nullable)transform       NS_DESIGNATED_INITIALIZER;
 
 /* You must use initWithDevice:thresholdValue:linearGrayColorTransform: instead */
 -(nonnull instancetype) initWithDevice:(nonnull id<MTLDevice>)device            NS_UNAVAILABLE;
@@ -188,7 +188,7 @@
  *              The ThresholdToZeroINverse function is:
  *                  destinationPixelValue = sourcePixelValue > thresholdValue ? 0 : sourcePixelValue
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageThresholdToZeroInverse : MPSUnaryImageKernel
 
 /*!
@@ -200,7 +200,7 @@
  */
 -(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
                         thresholdValue: (float)thresholdValue
-              linearGrayColorTransform: (nullable const float *)transform       NS_DESIGNATED_INITIALIZER;
+              linearGrayColorTransform: (const float * __nullable)transform       NS_DESIGNATED_INITIALIZER;
 
 /* You must use initWithDevice:thresholdValue:linearGrayColorTransform: instead */
 -(nonnull instancetype) initWithDevice:(nonnull id<MTLDevice>)device            NS_UNAVAILABLE;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageTranspose.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageTranspose.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageTranspose.h	2015-10-02 23:45:19.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageTranspose.h	2016-05-21 08:10:52.000000000 +0200
@@ -3,7 +3,7 @@
  *  @framework MetalPerformanceShaders.framework
  *
  *  @copyright Copyright (c) 2015 Apple Inc. All rights reserved.
- *  @abstract Metal Image transpose filters
+ *  @abstract MetalPerformanceShaders transpose filters
  */
 
 #ifndef MPS_MPSImageTranspose_h
@@ -16,7 +16,7 @@
  *  @discussion The MPSImageTranspose transposes an image
  *
  */
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface  MPSImageTranspose : MPSUnaryImageKernel
 
 @end    /* MPSImageTranspose */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSKernel.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSKernel.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSKernel.h	2015-10-02 23:45:19.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSKernel.h	2016-05-21 08:10:52.000000000 +0200
@@ -24,7 +24,7 @@
  *  @return     YES             The device is supported.
  *              NO              The device is not supported
  */
-BOOL    MPSSupportsMTLDevice( __nullable id <MTLDevice> device );
+BOOL    MPSSupportsMTLDevice( __nullable id <MTLDevice> device )  MPS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0);
 
 
 /*!
@@ -84,7 +84,7 @@
  *                  @endcode
  */
 
-NS_CLASS_AVAILABLE( NA, 9_0  )
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)
 @interface MPSKernel  : NSObject <NSCopying>
 
 /****************
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSTypes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSTypes.h	2015-10-02 23:45:19.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSTypes.h	2016-05-21 08:10:52.000000000 +0200
@@ -27,72 +27,171 @@
 #endif
 #if __has_extension(enumerator_attributes)
 #    ifdef __IPHONE_OS_VERSION_MIN_REQUIRED
-#        define MPS_ENUM_AVAILABLE_STARTING(_osx, _ios)   __AVAILABILITY_INTERNAL##_ios
-#        define MPS_AVAILABLE_STARTING(_osx, _ios)        __AVAILABILITY_INTERNAL##_ios
+#        define MPS_CLASS_AVAILABLE_STARTING(_osx, _ios, _tvos)  __attribute__((visibility("default"))) __AVAILABILITY_INTERNAL##_ios
+#        define MPS_ENUM_AVAILABLE_STARTING(_osx, _ios, _tvos)   __AVAILABILITY_INTERNAL##_ios
+#        define MPS_AVAILABLE_STARTING(_osx, _ios, _tvos)        __AVAILABILITY_INTERNAL##_ios
 #    elif defined(__MAC_OS_X_VERSION_MIN_REQUIRED)
-#        define MPS_ENUM_AVAILABLE_STARTING(_osx, _ios)   __AVAILABILITY_INTERNAL##_osx
-#        define MPS_AVAILABLE_STARTING(_osx, _ios)        __AVAILABILITY_INTERNAL##_osx
+#        define MPS_CLASS_AVAILABLE_STARTING(_osx, _ios, _tvos)  __attribute__((visibility("default"))) __AVAILABILITY_INTERNAL##_osx
+#        define MPS_ENUM_AVAILABLE_STARTING(_osx, _ios, _tvos)   __AVAILABILITY_INTERNAL##_osx
+#        define MPS_AVAILABLE_STARTING(_osx, _ios, _tvos)        __AVAILABILITY_INTERNAL##_osx
+#    elif __has_feature(attribute_availability_tvos)
+#        define MPS_CLASS_AVAILABLE_STARTING(_osx, _ios, _tvos)  __attribute__((visibility("default"))) __OS_AVAILABILITY(_tvos,introduced=_vers)
+#        define MPS_ENUM_AVAILABLE_STARTING(_osx, _ios, _tvos)   __OS_AVAILABILITY(_tvos,introduced=_vers)
+#        define MPS_AVAILABLE_STARTING(_osx, _ios, _tvos)        __OS_AVAILABILITY(_tvos,introduced=_vers)
+#    elif __has_feature(attribute_availability_watchos)
+#        define MPS_CLASS_AVAILABLE_STARTING(_osx, _ios, _tvos)  __attribute__((visibility("default"))) __OS_AVAILABILITY(watchos,unavailable)
+#        define MPS_ENUM_AVAILABLE_STARTING(_osx, _ios, _tvos)   __OS_AVAILABILITY(watchos,unavailable)
+#        define MPS_AVAILABLE_STARTING(_osx, _ios, _tvos)        __OS_AVAILABILITY(watchos,unavailable)
 #    else
-#        define MPS_ENUM_AVAILABLE_STARTING(_osx, _ios)
-#        define MPS_AVAILABLE_STARTING(_osx, _ios)
+#        define MPS_ENUM_AVAILABLE_STARTING(_osx, _ios, _tvos)
+#        define MPS_AVAILABLE_STARTING(_osx, _ios, _tvos)
 #    endif
 #else
 #    define MPS_ENUM_AVAILABLE_STARTING( _a, _b )
 #endif
 
 
-/*! @typedef    MPSKernelOptions
+/*! @enum       MPSKernelOptions
  *  @memberof   MPSKernel
  *  @abstract   Options used when creating MPSKernel objects
- *
- *          MPSKernelOptionsNone                    Use default options
- *
- *          MPSKernelOptionsSkipAPIValidation       Most MetalImage functions will sanity check their arguments. This has a small but
- *                                                  non-zero CPU cost. Setting the MPSKernelOptionsSkipAPIValidation will skip these checks.
- *                                                  MPSKernelOptionsSkipAPIValidation does not skip checks for memory allocation failure.
- *                                                  Caution:  turning on MPSKernelOptionsSkipAPIValidation can result in undefined behavior
- *                                                  if the requested operation can not be completed for some reason. Most error states
- *                                                  will be passed through to Metal which may do nothing or abort the program if Metal
- *                                                  API validation is turned on.
- *
- *          MPSKernelOptionsAllowReducedPrecision   When possible, MPSKernels use a higher precision data representation internally than
- *                                                  the destination storage format to avoid excessive accumulation of computational
- *                                                  rounding error in the result. MPSKernelOptionsAllowReducedPrecision advises the
- *                                                  MPSKernel that the destination storage format already has too much precision for
- *                                                  what is ultimately required downstream, and the MPSKernel may use reduced precision
- *                                                  internally when it feels that a less precise result would yield better performance.  
- *                                                  The expected performance win is often small, perhaps 0-20%. When enabled, the
- *                                                  precision of the result may vary by hardware and operating system.
  */
+#if defined(DOXYGEN)
+typedef enum MPSKernelOptions
+#else
 typedef NS_OPTIONS(NSUInteger, MPSKernelOptions)
+#endif
 {
-    MPSKernelOptionsNone                         MPS_ENUM_AVAILABLE_STARTING( __MAC_NA, __IPHONE_9_0)  = 0,
-    MPSKernelOptionsSkipAPIValidation            MPS_ENUM_AVAILABLE_STARTING( __MAC_NA, __IPHONE_9_0)  = 1 << 0,
-    MPSKernelOptionsAllowReducedPrecision        MPS_ENUM_AVAILABLE_STARTING( __MAC_NA, __IPHONE_9_0)  = 1 << 1,
+    /*! Use default options */
+    MPSKernelOptionsNone                         MPS_ENUM_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)  = 0,
+    
+    /*! Most MPS functions will sanity check their arguments. This has a small but
+     *  non-zero CPU cost. Setting the MPSKernelOptionsSkipAPIValidation will skip these checks.
+     *  MPSKernelOptionsSkipAPIValidation does not skip checks for memory allocation failure.
+     *  Caution:  turning on MPSKernelOptionsSkipAPIValidation can result in undefined behavior
+     *  if the requested operation can not be completed for some reason. Most error states
+     *  will be passed through to Metal which may do nothing or abort the program if Metal
+     *  API validation is turned on. */
+    MPSKernelOptionsSkipAPIValidation            MPS_ENUM_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)  = 1 << 0,
+    
+    /*! When possible, MPSKernels use a higher precision data representation internally than
+     *  the destination storage format to avoid excessive accumulation of computational
+     *  rounding error in the result. MPSKernelOptionsAllowReducedPrecision advises the
+     *  MPSKernel that the destination storage format already has too much precision for
+     *  what is ultimately required downstream, and the MPSKernel may use reduced precision
+     *  internally when it feels that a less precise result would yield better performance.
+     *  The expected performance win is often small, perhaps 0-20%. When enabled, the
+     *  precision of the result may vary by hardware and operating system. */
+    MPSKernelOptionsAllowReducedPrecision        MPS_ENUM_AVAILABLE_STARTING( __MAC_10_11, __IPHONE_9_0, __TVOS_9_0)  = 1 << 1,
+    
+    /*! Some MPSKernels may automatically split up the work internally into multiple tiles.
+     *  This improves performance on larger textures and reduces the amount of memory needed by
+     *  MPS for temporary storage. However, if you are using your own tiling scheme to achieve
+     *  similar results, your tile sizes and MPS's choice of tile sizes may interfere with
+     *  one another causing MPS to subdivide your tiles for its own use inefficiently. Pass
+     *  MPSKernelOptionsDisableInternalTiling to force MPS to process your data tile as a
+     *  single chunk.   */
+    MPSKernelOptionsDisableInternalTiling        MPS_ENUM_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0) = 1 << 2,
+    
+    /*! Enabling this bit will cause various -encode... methods to call MTLCommandEncoder
+     *  push/popDebugGroup.  The debug string will be drawn from MPSKernel.label, if any
+     *  or the name of the class otherwise. */
+    MPSKernelOptionsInsertDebugGroups            MPS_ENUM_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0) = 1 << 3,
 };
     
-/*! @typedef    MPSImageEdgeMode
+/*! @enum       MPSImageEdgeMode
  *  @memberof   MPSKernel
  *  @abstract   Options used to control edge behaviour of filter when filter reads beyond boundary of src image
- *
- *          MPSImageEdgeModeClamp        Out of bound pixels are clamped to nearest edge pixel
- *
- *          MPSImageEdgeModeZero         Out of bound pixels are (0,0,0,1) for image with pixel format without alpha channel
- *                                       and (0,0,0,0) for image with pixel format that has an alpha channel
  */
+#if defined(DOXYGEN)
+typedef enum MPSImageEdgeMode
+#else
 typedef NS_ENUM(NSUInteger, MPSImageEdgeMode)
+#endif
 {
-    MPSImageEdgeModeZero                MPS_ENUM_AVAILABLE_STARTING(__MAC_NA, __IPHONE_9_0)  = 0,
-    MPSImageEdgeModeClamp               MPS_ENUM_AVAILABLE_STARTING(__MAC_NA, __IPHONE_9_0)  = 1,
+    /*! Out of bound pixels are clamped to nearest edge pixel */
+    MPSImageEdgeModeZero                MPS_ENUM_AVAILABLE_STARTING(__MAC_10_11, __IPHONE_9_0, __TVOS_9_0)  = 0,
+    
+    /*! Out of bound pixels are (0,0,0,1) for image with pixel format without alpha channel
+     *  and (0,0,0,0) for image with pixel format that has an alpha channel */
+    MPSImageEdgeModeClamp               MPS_ENUM_AVAILABLE_STARTING(__MAC_10_11, __IPHONE_9_0, __TVOS_9_0)  = 1,
+};
+    
+   
+/*! @typedef MPSAlphaType
+ *  @abstract Premultiplication description for the color channels of a texture
+ *  @discussion Some image data is premultiplied. That is to say that the color channels
+ *              are stored instead as color * alpha. This is an optimization for image compositing
+ *              (alpha blending), but it can get in the way of most other image filters,
+ *              especially those that apply non-linear affects like the MPSImageParametricCurveTransform
+ *              multidimensional lookup tables, and functions like convolution or resampling filters
+ *              that look at adjacent pixels, where the alpha may not be the same.
+ *  @code
+ *              Some basic conversion cases:
+ *                  source                              destination                         operation
+ *                  ------                              -----------                         ---------
+ *                  MPSAlphaTypeNonPremultiplied        MPSAlphaTypeNonPremultiplied        <none>
+ *                  MPSAlphaTypeNonPremultiplied        MPSAlphaTypeAlphaIsOne              composite with opaque background color
+ *                  MPSAlphaTypeNonPremultiplied        MPSAlphaTypePremultiplied           multiply color channels by alpha
+ *                  MPSAlphaTypeAlphaIsOne              MPSAlphaTypeNonPremultiplied        set alpha to 1
+ *                  MPSAlphaTypeAlphaIsOne              MPSAlphaTypeAlphaIsOne              set alpha to 1
+ *                  MPSAlphaTypeAlphaIsOne              MPSAlphaTypePremultiplied           set alpha to 1
+ *                  MPSAlphaTypePremultiplied           MPSAlphaTypeNonPremultiplied        divide color channels by alpha
+ *                  MPSAlphaTypePremultiplied           MPSAlphaTypeAlphaIsOne              composite with opaque background color
+ *                  MPSAlphaTypePremultiplied           MPSAlphaTypePremultiplied           <none>
+ *  @endcode
+ *
+ *              Color space conversion operations require the format to be either MPSPixelAlpha_NonPremultiplied or
+ *              MPSPixelAlpha_AlphaIsOne to work correctly. A number of MPSKernels have similar requirements. If
+ *              premultiplied data is provided or requested, extra operations will be added to the conversion to
+ *              ensure correct operation. Fully opaque images should use MPSAlphaTypeAlphaIsOne.
+ *
+ *  @constant   MPSAlphaTypeNonPremultiplied   Image is not premultiplied by alpha. Alpha is not guaranteed to be 1. (kCGImageAlphaFirst/Last)
+ *  @constant   MPSAlphaTypeAlphaIsOne         Alpha is guaranteed to be 1, even if it is not encoded as 1 or not encoded at all. (kCGImageAlphaNoneSkipFirst/Last, kCGImageAlphaNone)
+ *  @constant   MPSAlphaTypePremultiplied      Image is premultiplied by alpha. Alpha is not guaranteed to be 1. (kCGImageAlphaPremultipliedFirst/Last)
+ */
+
+typedef NS_ENUM( NSUInteger, MPSAlphaType )
+{
+    MPSAlphaTypeNonPremultiplied   MPS_ENUM_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0, __TVOS_10_0)  = 0,
+    MPSAlphaTypeAlphaIsOne         MPS_ENUM_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0, __TVOS_10_0)  = 1,
+    MPSAlphaTypePremultiplied      MPS_ENUM_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0, __TVOS_10_0)  = 2
+};
+
+    
+/*! @enum       MPSImageFeatureChannelFormat
+ *  @memberof   MPSImage
+ *  @abstract   Encodes the representation of a single channel within a MPSImage.
+ *  @discussion A MPSImage pixel may have many channels in it, sometimes many more than 4, the
+ *              limit of what MTLPixelFormats encode. The storage format for a single channel 
+ *              within a pixel can be given by the MPSImageFeatureChannelFormat. The number
+ *              of channels is given by the featureChannels parameter of appropriate MPSImage
+ *              APIs. The size of the pixel is size of the channel format multiplied by the
+ *              number of feature channels. No padding is allowed, except to round out to a full
+ *              byte.
+ */
+typedef NS_ENUM(NSUInteger, MPSImageFeatureChannelFormat)
+{
+    /*! invalid format */
+    MPSImageFeatureChannelFormatInvalid     MPS_ENUM_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0, __TVOS_10_0)  = 0,
+
+    /*! uint8_t with value [0,255] encoding [0,1.0] */
+    MPSImageFeatureChannelFormatUnorm8     MPS_ENUM_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0, __TVOS_10_0)   = 1,
+    
+    /*! uint16_t with value [0,65535] encoding [0,1.0] */
+    MPSImageFeatureChannelFormatUnorm16     MPS_ENUM_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0, __TVOS_10_0)  = 2,
+    
+    /*! IEEE-754 16-bit floating-point value. "half precision" Representable normal range is +-[2**-14, 65504], 0, Infinity, NaN. 11 bits of precision + exponent. */
+    MPSImageFeatureChannelFormatFloat16     MPS_ENUM_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0, __TVOS_10_0)  = 3,
+    
+    /*! IEEE-754 32-bit floating-point value.  "single precision" (standard float type in C) 24 bits of precision + exponent */
+    MPSImageFeatureChannelFormatFloat32     MPS_ENUM_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0, __TVOS_10_0)  = 4,
+    
 };
     
 /*!
- *  @typedef    MPSOffset
+ *  @struct     MPSOffset
  *  @memberof   MPSKernel
  *  @abstract   A signed coordinate with x, y and z components
- *  @field      x       The horizontal component of the offset. Units: pixels
- *  @field      y       The vertical component of the offset. Units: pixels
- *  @field      z       The depth component of the offset. Units: pixels
  */
 typedef struct
 {
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MetalPerformanceShaders.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MetalPerformanceShaders.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MetalPerformanceShaders.h	2015-10-02 23:45:19.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MetalPerformanceShaders.h	2016-05-21 08:10:52.000000000 +0200
@@ -5,6 +5,8 @@
  *  @copyright Copyright (c) 2015 Apple Inc. All rights reserved.
  */
 
+#import <MetalPerformanceShaders/MPSCNN.h>
+#import <MetalPerformanceShaders/MPSImageConversion.h>
 #import <MetalPerformanceShaders/MPSImageConvolution.h>
 #import <MetalPerformanceShaders/MPSImageHistogram.h>
 #import <MetalPerformanceShaders/MPSImageIntegral.h>
```