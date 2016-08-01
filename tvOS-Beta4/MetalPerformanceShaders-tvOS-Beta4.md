#MetalPerformanceShaders.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSCNN.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSCNN.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSCNN.h	2016-07-10 07:17:32.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSCNN.h	2016-07-25 07:09:21.000000000 +0200
@@ -387,8 +387,9 @@
 
 @end    /* MPSCNNConvolutionDescriptor */
 
-/*! @enum       MPSCNNKernelWeightsStorageFormat
- *  @abstract   Options used to control how kernel weights are stored and used in the CNN kernels
+/*! @enum       MPSCNNConvolutionFlags
+ *  @abstract   Options used to control how kernel weights are stored and used in the CNN kernels.
+ *              For future expandability.
  */
 #if defined(DOXYGEN)
 typedef enum MPSCNNConvolutionFlags
@@ -486,29 +487,32 @@
 /*!
  *  @class      MPSCNNFullyConnected
  *  @dependency This depends on Metal.framework
- *  @discussion The MPSCNNFullyConnected specifies a fully connected convolution layer a.k.a. Inner product layer
- *              Fully connected layer in CNN is one where every input channel
- *              is connected to every output channel. Kernel width is equal to width of source image
- *              and kernel height is equal to height of source image. Width and height of output is 1x1
- *              Thus it takes srcW x srcH x Ni MPSCNNImage, convolves it with Weights[No][SrcW][srcH][Ni]
- *              and produces 1 x 1 x No output.
- *              Thus following must be true
+ *  @discussion The MPSCNNFullyConnected specifies a fully connected convolution layer a.k.a. Inner product 
+ *              layer. A fully connected CNN layer is one where every input channel is connected
+ *              to every output channel. The kernel width is equal to width of source image
+ *              and the kernel height is equal to the height of source image. Width and height of the output 
+ *              is 1x1. Thus, it takes a srcW x srcH x Ni MPSCNNImage, convolves it with Weights[No][SrcW][srcH][Ni]
+ *              and produces a 1 x 1 x No output. The following must be true:
+ *@code
  *                         kernelWidth  == source.width
  *                         kernelHeight == source.height
  *                         clipRect.size.width == 1
  *                         clipRect.size.height == 1
- *              One can think of fully connected layer as matrix multiplication where image is flattened into a vector of length
- *              srcW*srcH*Ni and weights are arragned in a matrix of dimension No x (srcW*srcH*Ni) to product output vector
- *              of length No.
- *              strideInPixelsX, strideInPixelsX, group must to 1. offset is not applicable and ignored. Since clipRect clamped
- *              to destination image bounds, if the destination is 1x1, one doesn't need to set clipRect.
+ *@endcode
+ *              One can think of a fully connected layer as a matrix multiplication that flattens an image into a vector of length
+ *              srcW*srcH*Ni. The weights are arragned in a matrix of dimension No x (srcW*srcH*Ni) for product output vectors
+ *              of length No. The strideInPixelsX, strideInPixelsY, and group must be 1. Offset is not applicable and is ignored. 
+ *              Since clipRect is clamped to the destination image bounds, if the destination is 1x1, one doesn't need to set the
+ *              clipRect.
  *
- *              Note that one can implement inner product using MPSCNNConvolution by setting
+ *              Note that one can implement an inner product using MPSCNNConvolution by setting
+ *@code
  *                     offset = (kernelWidth/2,kernelHeight/2)
  *                     clipRect.origin = (ox,oy), clipRect.size = (1,1)
- *                     strideX = strideX = group = 1
- *              However using MPSCNNFullyConnected for this better for performance as it lets us choose best approach
- *              to implement it which may not be possible when its implemented using general convolution. For example,
+ *                     strideX = strideY = group = 1
+ *@endcode
+ *              However, using the MPSCNNFullyConnected for this is better for performance as it lets us choose the most 
+ *              performant method which may not be possible when using a general convolution. For example,
  *              we may internally use matrix multiplication or special reduction kernels for a specific platform.
 */
 MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
@@ -617,7 +621,9 @@
 
 
 /*!
- * NOTE:    The encodeToCommandBuffer API in MPSCNNKernel can be used to encode a MPSCNNPooling kernel
+ *          Pooling window notes
+ *          ====================
+ *          The encodeToCommandBuffer API in MPSCNNKernel can be used to encode a MPSCNNPooling kernel
  *          to a MTLCommandBuffer. The exact location of the pooling window for each output value is determined
  *          as follows: The pooling window center for the first (top left) output pixel of the clipping
  *          rectangle is at spatial coordinates (offset.x, offset.y) in the input image. From this
@@ -667,14 +673,14 @@
  *          single feature channel of a source image. In the first examples we use strides that are
  *          larger than the pooling window sizes in order to clarify the placement of each
  *          individual pooling window.
- *
- *          Source image: width = 8, height = 5
- *          Destination cliprect: width = 3, height = 2
+ *@code
+ *              Source image: width = 8, height = 5
+ *              Destination cliprect: width = 3, height = 2
  *              o - source pixel center, one for each destination cliprect pixel
  *              x - filter taps in the pooling windows
- *
+ *@endcode
  *          1) Filter size = 2x2, stride = 3x3, offset = (0,0)
- *
+ *@code
  *              x  x     x  x     x  x
  *                |-----------------------|
  *              x |xo|  |x |xo|  |x |xo|  |
@@ -687,15 +693,16 @@
  *                |-----------------------|
  *                |  |  |  |  |  |  |  |  |
  *                |-----------------------|
- *
+ *@endcode
  *          One can use @ref offset to move the pooling windows within the source image:
  *          Using the formula offset.xy += (int)floor( ((L.xy - 1) % s.xy) / 2 ) + 1 from above
  *          for even filter sizes gives:
+ *@code
  *              offset.x = floor( (7 % 3) / 2) + 1 = 0 + 1 = 1 and
  *              offset.y = floor( (4 % 3) / 2) + 1 = 0 + 1 = 1.
- *
+ *@endcode
  *          2) Filter size = 2x2, stride = 3x3, offset = (1,1)
- *
+ *@code
  *                |-----------------------|
  *                |x |x |  |x |x |  |x |x |
  *                |-----------------------|
@@ -707,16 +714,17 @@
  *                |-----------------------|
  *                |x |xo|  |x |xo|  |x |xo|
  *                |-----------------------|
- *
+ *@endcode
  *
  *          Our third example shows the placement of additional taps when we increase
  *          the size of the pooling window to 3x3.
  *          In this case the recommended formula for offsets with odd filter sizes gives:
+ *@code
  *              offset.x = ceil( (7 % 3) / 2) = 1 and
  *              offset.y = ceil( (4 % 3) / 2) = 1.
- *
+ *@endcode
  *          3) Filter size = 3x3, stride = 3x3, offset = (1,1)
- *
+ *@code
  *                |-----------------------|
  *                |x |x |x |x |x |x |x |x |x
  *                |-----------------------|
@@ -729,7 +737,7 @@
  *                |x |xo|x |x |xo|x |x |xo|x
  *                |-----------------------|
  *                 x  x  x  x  x  x  x  x  x
- *
+ *@endcode
  *          In order to avoid large boundary effects with max pooling in examples 1) and 3) the user can use
  *          @ref MPSImageEdgeModeClamp for @ref edgeMode, which has the same effect as constraining the pooling
  *          windows to be confined completely within the source image.
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MetalPerformanceShaders.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MetalPerformanceShaders.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MetalPerformanceShaders.h	2016-07-10 09:31:51.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MetalPerformanceShaders.h	2016-07-25 07:09:21.000000000 +0200
@@ -36,7 +36,7 @@
  *  MetalPerformanceShaders.framework is a framework of highly optimized compute and graphics shaders that are
  *  designed to integrate easily and efficiently into your Metal application.  These data-parallel 
  *  primitives are specially tuned to take advantage of the unique hardware characteristics of each
- *  iOS GPUs to ensure optimal performance. Applications adopting MetalPerformanceShaders can be sure of achieving 
+ *  iOS GPU to ensure optimal performance. Applications adopting MetalPerformanceShaders can be sure of achieving
  *  optimal performance without needing to update their own hand-written shaders for each new iOS GPU 
  *  generation. MetalPerformanceShaders can be used along with the application's existing Metal resources (such as 
  *  the MTLCommandBuffer, MTLBuffer and MTLTexture objects) and shaders.
@@ -44,6 +44,10 @@
  *  In iOS 9, MetalPerformanceShaders.framework provides a series of commonly-used image processing primitives for 
  *  image effects on Metal textures.
  *
+ *  In iOS 10, MetalPerformanceShaders.framework adds support for the following kernels:
+ *  -  collection of kernels to implement and run neural networks using previously obtained training data, on the GPU
+ *  -  new image processing filters to perform color-conversion and for building a gaussian pyramid
+ *
  *  @section section_data    Data containers
  *  @subsection subsection_metal_containers  MTLTextures and MTLBuffers
  *
@@ -199,8 +203,7 @@
  *                                              MPSKernel that the destination storage format already has too much precision for
  *                                              what is ultimately required downstream, and the MPSKernel may use reduced precision
  *                                              internally when it feels that a less precise result would yield better performance.
- *                                              The expected performance win is often small, perhaps 0-20%. When enabled, the
- *                                              precision of the result may vary by hardware and operating system.
+ *                                              When enabled, the precision of the result may vary by hardware and operating system.
  *
  *  @section subsection_availableFilters     Available MPSKernels
  *
@@ -445,17 +448,18 @@
  *      MPSCNNSpatialNormalization      <MetalPerformanceShaders/MPSCNN.h>
  *      MPSCNNCrossChannelNormalization <MetalPerformanceShaders/MPSCNN.h>
  *      MPSCNNSoftmax                   <MetalPerformanceShaders/MPSCNN.h>      exp(pixel(x,y,k))/sum(exp(pixel(x,y,0)) ... exp(pixel(x,y,N-1))
+ *      MPSCNNLogSoftmax                <MetalPerformanceShaders/MPSCNN.h>      pixel(x,y,k) - ln(sum(exp(pixel(x,y,0)) ... exp(pixel(x,y,N-1)))
  *
  *  MPSCNNKernels operate on MPSImages.  MPSImages are at their core MTLTextures. However, whereas
  *  MTLTextures commonly represent image or texel data, a MPSImage is a more abstract representation
  *  of image features. The channels within a MPSImage do not necessarily correspond to colors in a
  *  color space. (Though, they can.) As a result, there can be many more than four of them. 32 or 64 channels
  *  per pixel is not uncommon.  This is achieved on the MTLTexture hardware abstraction by inserting
- *  extra RGBA pixels to handle the additional feature channels (if any) beyond 4. Thus, each CNN pixel
- *  in a 32 channel image is represented as 8 horizontally consecutive RGBA pixels in the texture.
- *  The width of the MTLTexture is correspondingly wider than the width of the MPSImage. Thus, in the common
- *  vernacular, MPSCNNKernels are layer operations why MPS(Temporary)Images are used to store layer
- *  inputs and outputs.
+ *  extra RGBA pixels to handle the additional feature channels (if any) beyond 4. These extra pixels are
+ *  stored as multiple slices of a 2D image array.  Thus, each CNN pixel in a 32-channel image is represented
+ *  as 8 array slices, with 4-channels stored per-pixel in each slice.  The width and height of the MTLTexture
+ *  is the same as the width and height of the MPSImage.  The number of slices in the MTLTexture is given by
+ *  the number of feature channels rounded up to a multiple of 4.
  *
  *  MPSImages can be created from existing MTLTextures. They may also be created anew from a MPSImageDescriptor
  *  and backed with either standard texture memory, or as MPSTemporaryImages using memory drawn from MPS's
@@ -481,6 +485,7 @@
  *      MPSCNNFullyConnected takes weights in the order weight[outputChannels][sourceWidth][sourceHeight][inputChannels]
  *  - Initialize MPSCNNKernels once and reuse them
  *  - You can use MPSCNNNeurons and other Filters in MPS to perform pre-processing of images, such as scaling and resizing.
+ *  - Specify a neuron filter with MPSCNNConvolution descriptor to combine the convolution and neuron operations.
  *  - Use MPSTemporaryImages for intermediate images that live for a short period of time (less than one MTLCommandBuffer).
  *      MPSTemporaryImages can reduce the amount of memory used by the convolutional neural network by several fold, and
  *      similarly reduce the amount of CPU time spent allocating storage and latency between MTLCommandBuffer.commit

```