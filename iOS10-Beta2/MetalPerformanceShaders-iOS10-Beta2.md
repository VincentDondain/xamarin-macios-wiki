#MetalPerformanceShaders.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSCNN.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSCNN.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSCNN.h	2016-05-21 08:10:52.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSCNN.h	2016-06-26 07:44:29.000000000 +0200
@@ -38,9 +38,31 @@
  *
  *              The Z/depth component of the offset, clipRect.origin and clipRect.size
  *              indexes which images to use. If the MPSImage contains only a single image
- *              (is not a texture array) then these should be offset.z = 0, clipRect.origin.z = 0
+ *              then these should be offset.z = 0, clipRect.origin.z = 0
  *              and clipRect.size.depth = 1. If the MPSImage contains multiple images,
- *              then it is an error to specify images that are not present in the MPSImage.
+ *              clipRect.size.depth refers to number of images to process. Both source 
+ *              and destination MPSImages must have at least this many images. offset.z 
+ *              refers to starting source image index. Thus offset.z + clipRect.size.depth must
+ *              be <= source.numberOfImages. Similarly, clipRect.origin.z refers to starting 
+ *              image index in destination. So clipRect.origin.z + clipRect.size.depth must be
+ *              <= destination.numberOfImage.
+ *
+ *              destinationFeatureChannelOffset property can be used to control where the MPSKernel will
+ *              start writing in feature channel dimension. For example, if the destination image has
+ *              64 channels, and MPSKernel outputs 32 channels, by default channels 0-31 of destination
+ *              will be populated by MPSKernel. But if we want this MPSKernel to populate channel 32-63
+ *              of the destination, we can set destinationFeatureChannelOffset = 32.
+ *              A good example of this is concat (concatenation) operation in Tensor Flow. Suppose
+ *              we have a src = w x h x Ni which goes through CNNConvolution_0 which produces
+ *              output O0 = w x h x N0 and CNNConvolution_1 which produces output O1 = w x h x N1 followed
+ *              by concatenation which produces O = w x h x (N0 + N1). We can achieve this by creating
+ *              an MPSImage with dimensions O = w x h x (N0 + N1) and using this as destination of
+ *              both convolutions as follows
+ *                  CNNConvolution0: destinationFeatureChannelOffset = 0, this will output N0 channels starting at
+ *                                   channel 0 of destination thus populating [0,N0-1] channels.
+ *                  CNNConvolution1: destinationFeatureChannelOffset = N0, this will output N1 channels starting at
+ *                                   channel N0 of destination thus populating [N0,N0+N1-1] channels.
+ *
  *
  */
 MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
@@ -51,6 +73,7 @@
  *  @abstract   The position of the destination clip rectangle origin relative to the source buffer.
  *  @discussion The offset is defined to be the position of clipRect.origin in source coordinates.
  *              Default: {0,0,0}, indicating that the top left corners of the clipRect and source image align.
+ *              offset.z is the index of starting source image in batch processing mode.
  *
  *              See Also: @ref subsubsection_mpsoffset
  */
@@ -61,12 +84,31 @@
  *  @discussion A MTLRegion that indicates which part of the destination to overwrite. If the clipRect does not lie
  *              completely within the destination image, the intersection between clip rectangle and destination bounds is
  *              used.   Default: MPSRectNoClip (MPSKernel::MPSRectNoClip) indicating the entire image.
+ *              clipRect.origin.z is the index of starting destination image in batch processing mode. clipRect.size.depth
+ *              is the number of images to process in batch processing mode.
  *
  *              See Also: @ref subsubsection_clipRect
  */
 @property (readwrite, nonatomic) MTLRegion               clipRect;
 
 
+/*! @property   destinationFeatureChannelOffset
+ *  @abstract   The number of channels in the destination MPSImage to skip before writing output.
+ *  @discussion This is the starting offset into the destination image in the feature channel dimension
+ *              at which destination data is written.
+ *              This allows an application to pass a subset of all the channels in MPSImage as output of MPSKernel.
+ *              E.g. Suppose MPSImage has 24 channels and a MPSKernel outputs 8 channels. If
+ *              we want channels 8 to 15 of this MPSImage to be used as output, we can set destinationFeatureChannelOffset = 8.
+ *              Note that this offset applies independently to each image when the MPSImage
+ *              is a container for multiple images and the MPSCNNKernel is processing multiple images (clipRect.size.depth > 1).
+ *              The default value is 0 and any value specifed shall be a multiple of 4. If MPSKernel outputs N channels,
+ *              destination image MUST have at least destinationFeatureChannelOffset + N channels. Using a destination
+ *              image with insufficient number of feature channels result in an error.
+ *              E.g. if the MPSCNNConvolution outputs 32 channels, and destination has 64 channels, then it is an error to set
+ *              destinationFeatureChannelOffset > 32.
+ */
+@property (readwrite, nonatomic) NSUInteger              destinationFeatureChannelOffset;
+
 /*! @property   edgeMode
  *  @abstract   The MPSImageEdgeMode to use when texture reads stray off the edge of an image
  *  @discussion Most MPSKernel objects can read off the edge of the source image. This can happen 
@@ -75,6 +117,9 @@
  *              Convolution filter.   Default:  MPSImageEdgeModeZero. 
  *
  *              See Also: @ref subsubsection_edgemode
+ *              Note: For @ref MPSCNNPoolingAverage specifying edge mode @ref MPSImageEdgeModeClamp
+ *                      is interpreted as a "shrink-to-edge" operation, which shrinks the effective
+ *                      filtering window to remain within the source image borders.
  */
 @property (readwrite, nonatomic) MPSImageEdgeMode        edgeMode;
 
@@ -87,8 +132,8 @@
  */
 -(void) encodeToCommandBuffer: (nonnull id <MTLCommandBuffer>) commandBuffer
                   sourceImage: (MPSImage * __nonnull) sourceImage
-             destinationImage: (MPSImage * __nonnull) destinationImage;
-
+             destinationImage: (MPSImage * __nonnull) destinationImage
+                NS_SWIFT_NAME( encode(commandBuffer:sourceImage:destinationImage:));
 
 /*!
  *  sourceRegionForDestinationSize: is used to determine which region of the
@@ -116,8 +161,8 @@
  *  @param      destinationSize The size of the full virtual destination image.
  *  @return     The area in the virtual source image that will be read.
  */
--(MPSRegion) sourceRegionForDestinationSize: (MTLSize) destinationSize;
-
+-(MPSRegion) sourceRegionForDestinationSize: (MTLSize) destinationSize
+                  NS_SWIFT_NAME( sourceRegion(destinationSize:));
 @end
 
 
@@ -436,26 +481,6 @@
  */
 -(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device NS_UNAVAILABLE;
 
-/*!
- * NOTE:    The encodeToCommandBuffer API in MPSCNNKernel can be used to encode a convolution kernel
- *          to a MTLCommandBuffer.  The source and destination images must be MPSImage objects.
- */
-
-/*!
- *  @abstract   Convenience API to encode a MPSCNNConvolutionKernel into a command Buffer.  
- *              Most often the very first layer is convolution layer and input is simple metal texture
- *              with <= 4 channels e.g. jpeg, tiff etc.
- *              Alternatively, one can create MPSImage with [MPSImage initWithTexture:srcTexture] and use
- *              regular [MPSKernel encodeToCommandBuffer:MPSImage:MPSImage].
- *  @param      commandBuffer       A valid MTLCommandBuffer to receive the encoded filter
- *  @param      sourceTexture       A valid metal texture object containing the source image.
- *  @param      destinationImage    A valid MPSImage to be overwritten by result image. destinationImage texture may not alias sourceTexture.
- */
--(void) encodeToCommandBuffer: (nonnull id <MTLCommandBuffer>) commandBuffer
-                sourceTexture: (__nonnull id<MTLTexture>) sourceTexture
-             destinationImage: (MPSImage * __nonnull) destinationImage;
-
-
 @end    /* MPSCNNConvolution */
     
 /*!
@@ -615,14 +640,100 @@
  *          of the pooling window are read from outside the input image boundaries (when filter size is
  *          larger than unity). Also it may mean that some values from the bottom and right stripes are
  *          not included at all in the pooling resulting in loss of valuable information.
+ *
  *          A scheme used in some common libraries is to shift the source offset according to the following
  *          formula:
- *              offset.xy += (int)floor( ((L.xy - 1) % s.xy) / 2 ) + (int)floor( (f.xy-1) % 2 ), where
+ *              offset.xy += { (int)ceil( ((L.xy - 1) % s.xy) / 2 ), for odd f.xy
+ *                           { (int)floor( ((L.xy - 1) % s.xy) / 2 ) + 1, for even f.xy, where
  *          L is the size of the input image (or more accurately the size corresponding to the scaled cliprect
  *          in source coordinates, which commonly coincides with the source image itself),
  *          s.xy is (strideInPixelsX, strideInPixelsY) and f.xy is (kernelWidth, kernelHeight).
- *          This offset distributes the pooling window centers evenly in the effective source cliprect
- *          and is commonly used in CNN libraries.
+ *          This offset distributes the pooling window centers evenly in the effective source cliprect,
+ *          when the output size is rounded up wrt. stride ( output size = ceil( input size / stride ) )
+ *          and is commonly used in CNN libraries (for example TensorFlow uses this offset scheme
+ *          in its maximum pooling implementation tf.nn.max_pool with 'SAME' - padding, for 'VALID'
+ *          padding one can simply set offset.xy += floor(f.xy/2) to get the first pooling window
+ *          inside the source image completely).
+ *          For @ref MPSCNNPoolingMax the way the input image borders are handled (see @ref edgeMode)
+ *          can become important: if there are negative values in the source image near the borders of the
+ *          image and the pooling window crosses the borders, then using @ref MPSImageEdgeModeZero may
+ *          cause the maximum pooling operation to override the negative input data values with zeros
+ *          coming from outside the source image borders, resulting in large boundary effects. A simple
+ *          way to avoid this is to use @ref MPSImageEdgeModeClamp for @ref edgeMode, which for
+ *          @ref MPSCNNPoolingMax effectively causes all pooling windows to remain within the source image.
+ *
+ *          Below are a couple of examples that can be used to visualize the effects of different
+ *          offset values for pooling. The illustrations show the pooling window placements inside a
+ *          single feature channel of a source image. In the first examples we use strides that are
+ *          larger than the pooling window sizes in order to clarify the placement of each
+ *          individual pooling window.
+ *
+ *          Source image: width = 8, height = 5
+ *          Destination cliprect: width = 3, height = 2
+ *              o - source pixel center, one for each destination cliprect pixel
+ *              x - filter taps in the pooling windows
+ *
+ *          1) Filter size = 2x2, stride = 3x3, offset = (0,0)
+ *
+ *              x  x     x  x     x  x
+ *                |-----------------------|
+ *              x |xo|  |x |xo|  |x |xo|  |
+ *                |-----------------------|
+ *                |  |  |  |  |  |  |  |  |
+ *                |-----------------------|
+ *              x |x |  |x |x |  |x |x |  |
+ *                |-----------------------|
+ *              x |xo|  |x |xo|  |x |xo|  |
+ *                |-----------------------|
+ *                |  |  |  |  |  |  |  |  |
+ *                |-----------------------|
+ *
+ *          One can use @ref offset to move the pooling windows within the source image:
+ *          Using the formula offset.xy += (int)floor( ((L.xy - 1) % s.xy) / 2 ) + 1 from above
+ *          for even filter sizes gives:
+ *              offset.x = floor( (7 % 3) / 2) + 1 = 0 + 1 = 1 and
+ *              offset.y = floor( (4 % 3) / 2) + 1 = 0 + 1 = 1.
+ *
+ *          2) Filter size = 2x2, stride = 3x3, offset = (1,1)
+ *
+ *                |-----------------------|
+ *                |x |x |  |x |x |  |x |x |
+ *                |-----------------------|
+ *                |x |xo|  |x |xo|  |x |xo|
+ *                |-----------------------|
+ *                |  |  |  |  |  |  |  |  |
+ *                |-----------------------|
+ *                |x |x |  |x |x |  |x |x |
+ *                |-----------------------|
+ *                |x |xo|  |x |xo|  |x |xo|
+ *                |-----------------------|
+ *
+ *
+ *          Our third example shows the placement of additional taps when we increase
+ *          the size of the pooling window to 3x3.
+ *          In this case the recommended formula for offsets with odd filter sizes gives:
+ *              offset.x = ceil( (7 % 3) / 2) = 1 and
+ *              offset.y = ceil( (4 % 3) / 2) = 1.
+ *
+ *          3) Filter size = 3x3, stride = 3x3, offset = (1,1)
+ *
+ *                |-----------------------|
+ *                |x |x |x |x |x |x |x |x |x
+ *                |-----------------------|
+ *                |x |xo|x |x |xo|x |x |xo|x
+ *                |-----------------------|
+ *                |x |x |x |x |x |x |x |x |x
+ *                |-----------------------|
+ *                |x |x |x |x |x |x |x |x |x
+ *                |-----------------------|
+ *                |x |xo|x |x |xo|x |x |xo|x
+ *                |-----------------------|
+ *                 x  x  x  x  x  x  x  x  x
+ *
+ *          In order to avoid large boundary effects with max pooling in examples 1) and 3) the user can use
+ *          @ref MPSImageEdgeModeClamp for @ref edgeMode, which has the same effect as constraining the pooling
+ *          windows to be confined completely within the source image.
+ *
  */
 
 @end    /* MPSCNNPooling */
@@ -644,6 +755,11 @@
  *  @dependency This depends on Metal.framework
  *  @discussion Specifies the average pooling filter.  For each pixel, returns the mean value of pixels
  *              in the kernelWidth x kernelHeight filter region.
+ *              When @ref edgeMode is @ref MPSImageEdgeModeClamp the filtering window is shrunk to remain
+ #              within the source image borders. What this means is that close to image borders the filtering window
+ *              will be smaller in order to fit inside the source image and less values will be used to compute the
+ *              average. In case the filtering window is entirely outside the source image border the
+ *              outputted value will be zero.
  */
 MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
 @interface  MPSCNNPoolingAverage : MPSCNNPooling
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImage.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImage.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImage.h	2016-05-21 08:10:52.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImage.h	2016-06-26 08:51:26.000000000 +0200
@@ -126,16 +126,16 @@
  *              such that 4 consecutive channels are stored in each slice of this array.
  *              If the number of feature channels is N, number of array slices needed is (N+3)/4.
  *              E.g. a CNN image with width 3 and height 2 with 9 channels will be stored as
- * 
+ * @code
  *              slice 2         R???   R???   R???
  *                              R???   R???   R???
  *
  *              slice 1      RGBA   RGBA   RGBA
- *                           RGBA   RGBA   RGBA
+ *                           RGBA   RGBA   RGBA         (ASCII art /diagonal offset/ intended to show a Z dimension)
  *
  *              slice 0   RGBA   RGBA  RGBA
  *                        RGBA   RGBA  RGBA
- *
+ *@endcode
  *              Thus width and height of underlying 2d texture array is same as width and height of MPSImage
  *              and array length is equal to (featureChannels + 3) / 4. Channels marked with ? are just
  *              for padding and should not contain NaNs or Infs.
@@ -261,21 +261,6 @@
 @property (copy, atomic, nullable)  NSString *label;
 
 /*!
- *  @abstract   Initialize a MPSImage object using a metal texture
- *  @param      texture         The MTLTexture allocated by the developer to be used as backing for MPSImage.
- *  @return     A valid MPSImage object or nil, if failure.
- *  @discussion  The number of featureChannels in the image will be inferred from the number of channels in
- *               the texture.pixelFormat. The number of feature channels must be between 1 and 4.
- *
- *               This is a convenience method intended for MTLTextures containing typical image data 
- *               which application may obtain from MetalKit or other libraries such as that drawn from a JPEG or PNG,
- *               The number of feature channels shall be equal to the number of color channels
- *               in the MTLPixelFormat. If texture.textureType == MTLTextureType2DArray, numberOfImages is
- *               set to texture.arrayLength
- */
--(nonnull instancetype) initWithTexture: (nonnull id <MTLTexture>) texture;
-
-/*!
  *  @abstract   Initialize an empty image object
  *  @param      device              The device that the image will be used. May not be NULL.
  *  @param      imageDescriptor     The MPSImageDescriptor. May not be NULL.
@@ -286,6 +271,42 @@
  */
 -(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
                        imageDescriptor: (const MPSImageDescriptor * __nonnull) imageDescriptor;
+
+/*!
+ *  @abstract   Initialize an MPSImage object using Metal texture. Metal texture has been created by
+ *              user for specific number of feature channels and number of images.
+ *  @param      texture          The MTLTexture allocated by the user to be used as backing for MPSImage.
+ *  @param      featureChannels  Number of feature channels this texture contains.
+ *  @return     A valid MPSImage object or nil, if failure.
+ *  @discussion Application can let MPS framework allocate texture with properties specified in imageDescriptor 
+ *              using initWithDevice:MPSImageDescriptor API above. However in memory intensive application, 
+ *              you can save memory (and allocation/deallocation time) by using MPSTemporaryImage where MPS 
+ *              framework aggressively reuse memory underlying textures on same command buffer. See MPSTemporaryImage
+ *              class for details below. However, in certain cases, application developer may want more control
+ *              on allocation, placement, reusing/recycling of memory backing textures used in application using
+ *              Metal Heaps API. In this case, application can create MPSImage from pre-allocated texture using 
+ *              initWithTexture:featureChannels.
+ *
+ *              MTLTextureType of texture can be MTLTextureType2D ONLY if featureChannels <= 4 in which case
+ *              MPSImage.numberOfImages is set to 1. Else it should be MTLTextureType2DArray with
+ *              arrayLength == numberOfImage * ((featureChannels + 3)/4). MPSImage.numberOfImages is set to
+ *              texture.arrayLength / ((featureChannels + 3)/4).
+ *
+ *              For MTLTextures containing typical image data which application may obtain from MetalKit or 
+ *              other libraries such as that drawn from a JPEG or PNG, featureChannels should
+ *              be set to number of valid color channel e.g. for RGB data, even thought MTLPixelFormat will be
+ *              MTLPixelFormatRGBA, featureChannels should be set to 3.
+ *
+ */
+-(nonnull instancetype) initWithTexture: (nonnull id <MTLTexture>) texture
+                        featureChannels: (NSUInteger) featureChannels;
+
+
+/*
+ * Use initWithDevice:texture: or initWithDevice:imageDescriptor: instead
+ */
+-(nonnull instancetype) init NS_UNAVAILABLE;
+
 /*!
  *  @method         setPurgeableState
  *  @abstract       Set (or query) the purgeability state of a MPSImage
@@ -295,77 +316,79 @@
  */
 - (MPSPurgeableState)setPurgeableState:(MPSPurgeableState)state;
 
-/*
- * Use initWithDevice:texture: or initWithDevice:imageDescriptor: instead
- */
--(nonnull instancetype) init NS_UNAVAILABLE;
-
 @end
 
 /*!
  *  @class      MPSTemporaryImage
  *  @dependency MPSImage
- *  @discussion MPSTemporaryImages are provided as a fast way to store intermediate data
+ *  @abstract   MPSTemporaryImages are provided as a fast way to store transient data
  *              that will be used promptly and discarded.
  *
- *              MPSTemporaryImages use an internal cache of preallocated reusable memory
- *              to hold pixel data to avoid typical memory allocation performance penalties
- *              common to ordinary MPSImages and MTLTextures.  Multiple MPSTemporaryImages
- *              in the same MTLCommandBuffer can alias the same overlapping piece of memory.
- *              This avoids the CPU cost of allocating memory and can greatly reduce the
- *              overall memory footprint.
- *
- *              To avoid data corruption, MPSTemporaryImages impose some restrictions:
- *
- *              - The textures are MTLStorageModePrivate.
- *
- *              - The temporary image may not be used on any other MTLCommandBuffer.
- *
- *              - The MPSTemporaryImage must be used by the same thread as the
- *                one managing the MTLCommandBuffer on which it is created.
- *
- *              - You must release the MPSTemporaryImage immediately so that its memory
- *                can be reused. If sufficient reusable memory is not available for the next
- *                MPSTemporaryImage on the MTLCommandBuffer, new memory will be allocated
- *                and any performance benefits are lost.
+ *  @discussion MPSTemporaryImages can provide for profound reduction in the aggregate 
+ *              texture memory and associated CPU-side allocation cost in your application. 
+ *              MPS achieves this by automatically identifying MPSTemporaryImages that
+ *              do not overlap in time over the course of a MTLCommandBuffer and so can 
+ *              reuse the same memory. MPSTemporaryImages leverage MPS's internal cache
+ *              of preallocated reusable memory to hold pixel data to avoid typical 
+ *              memory allocation performance penalties common to ordinary MPSImages and 
+ *              MTLTextures.
+ *
+ *              To avoid data corruption due to aliasing, MPSTemporaryImages impose some
+ *              important restrictions:
+ *
+ *              - The textures are MTLStorageModePrivate. You can not, for example, use
+ *                [MTLTexture getBytes...] or [MTLTexture replaceRegion...] with them. 
+ *                MPSTemporaryImages are strictly read and written by the GPU.
+ *
+ *              - The temporary image may be used only on a single MTLCommandBuffer.
+ *                This limits the chronology to a single linear time stream.
+ *
+ *              - The readCount property must be managed correctly. Please see
+ *                the description of the readCount property for full details.
  *
  *              - see also pixel format restrictions for MPSImages in general.
  *
- *              You may have more than one MPSTemporaryImage allocated concurrently.
+ *              Since MPSTemporaryImages can only be used with a single MTLCommandBuffer,
+ *              and can not be used off the GPU, they generally should not be kept 
+ *              around past the completion of the MTLCommandBuffer. The lifetime of
+ *              MPSTemporaryImages is expected to be typically extremely short, perhaps 
+ *              only a few lines of code.
+ *
+ *              To keep the lifetime of the underlying texture allocation as short as 
+ *              possible, the underlying texture is not allocated until the first time
+ *              the MPSTemporaryImage is used by a MPSCNNKernel or the .texture property
+ *              is read. The readCount property serves to limit the lifetime on the
+ *              other end.
  *
- *              You may use the MPSTemporaryImage.texture with non-CNN MPSKernel -encode... methods,
+ *              You may use the MPSTemporaryImage.texture with MPSUnaryImageKernel -encode... methods,
  *              iff featureChannels <= 4 and the MTLTexture conforms to requirements of that MPSKernel.
+ *              In such cases, the readCount is not modified, since the enclosing object
+ *              is not available. There is no locking mechanism provided to prevent a MTLTexture
+ *              returned from the .texture property from becoming invalid when the
+ *              readCount reaches 0.
+ *
+ *              MPSTemporaryImages can otherwise be used wherever MPSImages are used.
+ *
+ *
  */
 MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
 @interface  MPSTemporaryImage : MPSImage
 
+
 /*!
  *  @abstract   Initialize a MPSTemporaryImage for use on a MTLCommandBuffer
  *
- *  @discussion MPSTemporaryImages aggresively reuse cached memory to avoid expensive
- *              allocation and deallocation of texture memory. They are intended to be used
- *              to hold short-lived CNN image data, typically for image data that is produced
- *              then consumed immediately and needed no further.
- *
- *              Please see MPSTemporaryImage and MPSImage class documentation for
- *              important restrictions.
- *
- *  @param      commandBuffer       The MTLCommandBuffer on which the MPSTemporaryImage will be exclusively used
- *
- *  @param      imageDescriptor  A valid imageDescriptor describing the MPSImage format to create.
- *
- *  @result     A valid MPSTemporaryImage.  The image is MTLStorageModePrivate. It becomes
- *              invalid when the MTLCommandBuffer is committed. In order to receive the intended
- *              performance advantages of the MPSTemporaryImage, it should in general
- *              be released within a few lines of code of its allocation.
- *
- *              Note: the allocation of the underlying MTLTexture object is deferred until
- *                    it is needed.  You should in general refrain from calling
- *                    MPSTemporaryImage.texture, as this could force the texture to
- *                    have a lifetime longer than it should otherwise.
+ *  @param      commandBuffer   The MTLCommandBuffer on which the MPSTemporaryImage will be exclusively used
+ *
+ *  @param      imageDescriptor A valid imageDescriptor describing the MPSImage format to create.
+ *
+ *  @return     A valid MPSTemporaryImage.  The object will be released when the command buffer
+ *              is committed. The underlying texture will become invalid before this time
+ *              due to the action of the readCount property.
+ *
  */
--(nonnull instancetype) initForCommandBuffer: (nonnull id <MTLCommandBuffer>) commandBuffer
-                             imageDescriptor: (const MPSImageDescriptor * __nonnull) imageDescriptor;
++(nonnull instancetype) temporaryImageWithCommandBuffer: (nonnull id <MTLCommandBuffer>) commandBuffer
+                                        imageDescriptor: (const MPSImageDescriptor * __nonnull) imageDescriptor;
 
 
 /*!
@@ -379,20 +402,70 @@
  *                      MTLStorageMode must be MTLStorageModePrivate
  *                      depth must be 1
  *
+ *  @param commandBuffer        The command buffer on which the MPSTemporaryImage may be used
+ *  @param textureDescriptor    A texture descriptor describing the MPSTemporaryImage texture
  *
+ *  @return     A valid MPSTemporaryImage.  The object will be released when the command buffer
+ *              is committed. The underlying texture will become invalid before this time
+ *              due to the action of the readCount property.
  */
--(nonnull instancetype) initForCommandBuffer: (nonnull id <MTLCommandBuffer>) commandBuffer
-                           textureDescriptor: (const MTLTextureDescriptor * __nonnull) textureDescriptor;
++(nonnull instancetype) temporaryImageWithCommandBuffer: (nonnull id <MTLCommandBuffer>) commandBuffer
+                                      textureDescriptor: (const MTLTextureDescriptor * __nonnull) textureDescriptor;
 
 
-/*! Unavailable. Use initForCommandBuffer:textureDescriptor: or -initForCommandBuffer:imageDescriptor: instead. */
+/*!
+ *  @abstract       Help MPS decide which allocations to make ahead of time
+ *  @discussion     The texture cache that underlies the MPSTemporaryImage can automatically allocate new storage as
+ *                  needed as you create new temporary images.  However, sometimes a more global view of what you
+ *                  plan to make is useful for maximizing memory reuse to get the most efficient operation.
+ *                  This class method hints to the cache what the list of images will be.
+ *
+ *                  It is never necessary to call this method. It is purely a performance and memory optimization.
+ *
+ *  @param commandBuffer        The command buffer on which the MPSTemporaryImages will be used
+ *  @param descriptorList       A NSArray of MPSImageDescriptors, indicating images that will be created
+ */
++(void) prefetchStorageWithCommandBuffer: (nonnull id <MTLCommandBuffer>) commandBuffer
+                     imageDescriptorList: (NSArray <MPSImageDescriptor*> * __nonnull) descriptorList;
+
+/*! Unavailable. Use temporaryImageForCommandBuffer:textureDescriptor: or -temporaryImageForCommandBuffer:imageDescriptor: instead. */
 -(nonnull instancetype) initWithTexture: (nonnull id <MTLTexture>) texture
-                        featureChannels: (NSUInteger) featureChannels  NS_UNAVAILABLE;
+                        featureChannels: (NSUInteger) featureChannels NS_UNAVAILABLE;
 
-/*! Unavailable. Use initForCommandBuffer:imageDescriptor: instead. */
+/*! Unavailable. Use itemporaryImageForCommandBuffer:textureDescriptor: instead. */
 -(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device
                        imageDescriptor: (const MPSImageDescriptor * __nonnull) imageDescriptor      NS_UNAVAILABLE;
 
+/*
+ *  @abstract       The number of times a temporary image may be read by a MPSCNNKernel
+ *                  before its contents become undefined.
+ *
+ *  @discussion     MPSTemporaryImages must release their underlying textures for reuse
+ *                  immediately after last use. So as to facilitate *prompt* convenient 
+ *                  memory recycling, each time a MPSTemporaryImage is read by a 
+ *                  MPSCNNKernel -encode... method, its readCount is automatically 
+ *                  decremented. When the readCount reaches 0, the underlying texture is 
+ *                  automatically made available for reuse to MPS for its own needs and for 
+ *                  other MPSTemporaryImages prior to return from the -encode.. function.  
+ *                  The contents of the texture become undefined at this time. 
+ *
+ *                  By default, the readCount is initialized to 1, indicating a image that
+ *                  may be overwritten any number of times, but read only once.
+ *
+ *                  You may change the readCount as desired to allow MPSCNNKernels to read
+ *                  the MPSTemporaryImage additional times. However, it is an error to change
+ *                  the readCount once it is zero. It is an error to read or write to a
+ *                  MPSTemporaryImage with a zero readCount. You may set the readCount to 0
+ *                  yourself to cause the underlying texture to be returned to MPS. Writing
+ *                  to a MPSTemporaryImage does not adjust the readCount.
+ *
+ *                  The Metal API Validation layer will assert if a MPSTemporaryImage is
+ *                  deallocated with non-zero readCount to help identify cases when resources
+ *                  are not returned promptly.
+ */
+@property (readwrite, nonatomic)  NSUInteger  readCount;
+
+
 @end
 
 #ifdef __cplusplus
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageKernel.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageKernel.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageKernel.h	2016-05-21 08:10:52.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSImageKernel.h	2016-06-26 07:44:29.000000000 +0200
@@ -145,7 +145,8 @@
  */
 -(BOOL)    encodeToCommandBuffer: (nonnull id <MTLCommandBuffer>)commandBuffer
                   inPlaceTexture: (__nonnull id <MTLTexture> __strong * __nonnull) texture
-           fallbackCopyAllocator: (nullable MPSCopyAllocator) copyAllocator;
+           fallbackCopyAllocator: (nullable MPSCopyAllocator) copyAllocator
+                NS_SWIFT_NAME(encode(commandBuffer:inPlaceTexture:fallbackCopyAllocator:));
 
 
 /*!
@@ -156,7 +157,8 @@
  */
 -(void) encodeToCommandBuffer: (nonnull id <MTLCommandBuffer>) commandBuffer
                 sourceTexture: (nonnull id <MTLTexture>) sourceTexture
-           destinationTexture: (nonnull id <MTLTexture>) destinationTexture;
+           destinationTexture: (nonnull id <MTLTexture>) destinationTexture
+            NS_SWIFT_NAME(encode(commandBuffer:sourceTexture:destinationTexture:));
 
 
 /*!
@@ -185,7 +187,8 @@
  *  @param      destinationSize The size of the full virtual destination image.
  *  @return     The area in the virtual source image that will be read.
  */
--(MPSRegion) sourceRegionForDestinationSize: (MTLSize) destinationSize;
+-(MPSRegion) sourceRegionForDestinationSize: (MTLSize) destinationSize
+            NS_SWIFT_NAME(sourceRegion(destinationSize:));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSMatrix.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSMatrix.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSMatrix.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSMatrix.h	2016-06-26 07:44:29.000000000 +0200
@@ -0,0 +1,165 @@
+#ifndef MPSMatrix_h
+#define MPSMatrix_h
+
+#include <MetalPerformanceShaders/MPSTypes.h>
+
+#ifdef __cplusplus
+extern "C" {
+#endif
+
+/*!
+ *  @class      MPSMatrixDescriptor
+ *
+ *  @dependency This depends on Metal.framework
+ *
+ *  @discussion A MPSMatrixDescriptor describes the sizes, strides, and data type of a
+ *              2-dimensional array of data.  All storage is assumed to be in row-major
+ *              order.
+ */
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
+@interface MPSMatrixDescriptor: NSObject
+
+/*! @property   rows
+ *  @discussion The number of rows in the matrix.
+ */
+@property (readwrite, nonatomic) NSUInteger rows;
+
+/*! @property   columns
+ *  @discussion The number of columns in the matrix.
+ */
+@property (readwrite, nonatomic) NSUInteger columns;
+
+/*! @property   dataType
+ *  @discussion The type of the data which makes up the values of the matrix.
+ */
+@property (readwrite, nonatomic) MPSDataType dataType;
+
+/*! @property   rowBytes
+ *  @discussion The stride, in bytes, between corresponding elements of
+ *              consecutive rows.  Must be a multiple of the element size.
+ */
+@property (readwrite, nonatomic) NSUInteger rowBytes;
+
+/*!
+ *  @abstract   Create a MPSMatrixDescriptor with the specified dimensions and data type.
+ *
+ *  @param      rows                The number of rows of the matrix.
+ *
+ *  @param      columns             The number of columns of the matrix.
+ *
+ *  @param      rowBytes            The number of bytes between starting elements of consecutive
+ *                                  rows.  Must be a multiple of the element size.
+ *
+ *  @param      dataType            The type of the data to be stored in the matrix.
+ *
+ *  @discussion For performance considerations the optimal row stride may not necessarily be equal
+ *              to the number of columns in the matrix.  The MPSMatrix class provides a method which
+ *              may be used to determine this value, see the rowBytesFromColumns API in the MPSMatrix
+ *              class.
+ */
++(__nonnull instancetype) matrixDescriptorWithDimensions: (NSUInteger)              rows
+                                                 columns: (NSUInteger)              columns
+                                                rowBytes: (NSUInteger)              rowBytes
+                                                dataType: (MPSDataType)             dataType;
+
+/*!
+ *  @abstract   Return the recommended row stride, in bytes, for a given number of
+ *              columns.
+ *
+ *  @param      columns         The number of columns in the matrix for which the recommended
+ *                              row stride, in bytes, is to be determined.
+ *
+ *  @param      dataType        The type of matrix data values.
+ *
+ *  @discussion To achieve best performance the optimal stride between rows of a matrix is not
+ *              necessarily equivalent to the number of columns.  This method returns the row stride, in
+ *              bytes, which gives best performance for a given number of columns.  Using this row stride
+ *              to construct your array is recommended, but not required (provided that the stride
+ *              used is still large enough to allocate a full row of data).
+ */
++(size_t) rowBytesFromColumns: (NSUInteger) columns
+                     dataType: (MPSDataType) dataType;
+
+@end // MPSMatrixDescriptor
+
+/*!
+ *  @class      MPSMatrix
+ *
+ *  @dependency This depends on Metal.framework
+ *
+ *  @discussion A MPSMatrix object describes a 2-dimensional array of data and provides storage
+ *              for its values.  MPSMatrix objects serve as inputs and outputs of MPSMatrixKernel
+ *              objects.
+ *
+ *              Implementation note:
+ *              A MPSMatrix object maintains its internal storage using a MTLBuffer object and thus
+ *              the same rules for maintaining coherency of a MTLBuffer's data between CPU memory and GPU
+ *              memory apply to a MPSMatrix.  Data is assumed to be stored in row-major layout.
+ */
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
+@interface MPSMatrix: NSObject
+
+/*! @property   device
+ *  @discussion The device on which the MPSMatrix will be used.
+ */
+@property (readonly, retain, nonatomic, nonnull) id<MTLDevice> device;
+
+/*! @property   rows
+ *  @discussion The number of rows in the MPSMatrix.
+ */
+@property (readonly, nonatomic) NSUInteger rows;
+
+/*! @property   columns
+ *  @discussion The number of columns in the MPSMatrix.
+ */
+@property (readonly, nonatomic) NSUInteger columns;
+
+/*! @property   dataType
+ *  @discussion The type of the MPSMatrix data.
+ */
+@property (readonly, nonatomic) MPSDataType dataType;
+
+/*! @property   rowBytes
+ *  @discussion The stride, in bytes, between corresponding elements of
+ *              consecutive rows.
+ */
+@property (readonly, nonatomic) NSUInteger rowBytes;
+
+/*! @property   data
+ *  @discussion An MTLBuffer to store the data.
+ */
+@property (readonly, nonnull, nonatomic) id<MTLBuffer> data;
+
+/*!
+ *  @abstract   Initialize a MPSMatrix object with a MTLBuffer.
+ *
+ *  @param      buffer          The MTLBuffer object which contains the data to use for the
+ *                              MPSMatrix. May not be NULL.
+ *
+ *  @param      descriptor      The MPSMatrixDescriptor. May not be NULL.
+ *
+ *  @return     A valid MPSMatrix object or nil, if failure.
+ *
+ *  @discussion This function returns a MPSMatrix object which uses the supplied MTLBuffer.  The
+ *              dimensions and stride of the matrix are specified by the MPSMatrixDescriptor object.
+ *
+ *              The provided MTLBuffer must have enough storage to hold
+ *
+ *                  (descriptor.rows-1) * descriptor.rowBytes + descriptor.columns * (element size) bytes.
+ *
+ */
+-(nonnull instancetype) initWithBuffer: (nonnull id<MTLBuffer>) buffer
+                            descriptor: (nonnull MPSMatrixDescriptor*) descriptor;
+
+/*
+ * Use one of the above initialization methods instead.
+ */
+-(nonnull instancetype) init NS_UNAVAILABLE;
+
+@end // MPSMatrix
+
+#ifdef __cplusplus
+}   // extern "C"
+#endif
+
+#endif /* MPSMatrix_h */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSMatrixMultiplication.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSMatrixMultiplication.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSMatrixMultiplication.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSMatrixMultiplication.h	2016-06-26 07:44:29.000000000 +0200
@@ -0,0 +1,152 @@
+/*!
+ *  @header MPSMatrixMultiplication.h
+ *  @framework MetalPerformanceShaders.framework
+ *
+ *  @copyright Copyright (c) 2016 Apple Inc. All rights reserved.
+ *  @abstract MetalPerformanceShaders filter base classes
+ */
+#ifndef MPSMatrixMultiplication_h
+#define MPSMatrixMultiplication_h
+
+#import <MetalPerformanceShaders/MPSKernel.h>
+#import <MetalPerformanceShaders/MPSMatrix.h>
+
+/*!
+ *  @class      MPSMatrixMultiplication
+ *
+ *  @dependency This depends on Metal.framework.
+ *
+ *  @abstract   A matrix multiplication kernel.
+ *
+ *  @discussion A MPSMatrixMultiplication object computes:
+ *
+ *                  C = alpha * op(A) * op(B) + beta * C
+ *
+ *              A, B, and C are matrices which are represented by MPSMatrix
+ *              objects. alpha and beta are scalar values (of the same data type
+ *              as values of C) which are applied as shown above.  A and B may
+ *              each have an optional transposition operation applied.
+ *
+ *              A, B, and C (also referred to in later discussions as the left input
+ *              matrix, the right input matrix, and the result matrix respectively).
+ *
+ *              A MPSMatrixMultiplication object is initialized with the transpose
+ *              operators to apply to A and B, sizes for the operation to perform,
+ *              and the scalar values alpha and beta.
+ *
+ */
+MPS_CLASS_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0)
+@interface MPSMatrixMultiplication : MPSKernel
+/*! @property   resultMatrixOrigin
+ *
+ *  @discussion The origin, relative to [0, 0] in the result matrix, at which to
+ *              start writing (and reading if necessary) results.  This property is
+ *              modifiable and defaults to [0, 0] at initialization time.  If a
+ *              different origin is desired then this should be modified prior to
+ *              encoding the kernel.  The z value must be 0.
+ */
+@property (readwrite, nonatomic) MTLOrigin resultMatrixOrigin;
+
+/*! @property   leftMatrixOrigin
+ *
+ *  @discussion The origin, relative to [0, 0] in the left input matrix, at which to
+ *              start reading values.  This property is modifiable and defaults to
+ *              [0, 0] at initialization time.  If a different origin is desired then
+ *              this should be modified prior to encoding the kernel.  The z value
+ *              must be 0.
+ */
+@property (readwrite, nonatomic) MTLOrigin leftMatrixOrigin;
+
+/*! @property   rightMatrixOrigin
+ *
+ *  @discussion The origin, relative to [0, 0] in the right input matrix, at which to
+ *              start reading values.  This property is modifiable and defaults to
+ *              [0, 0] at initialization time.  If a different origin is desired then
+ *              this should be modified prior to encoding the kernel.  The z value
+ *              must be 0.
+ */
+@property (readwrite, nonatomic) MTLOrigin rightMatrixOrigin;
+
+/*!
+ *  @abstract   Initialize an MPSMatrixMultiplication object on a device for a given size
+ *              and desired transpose and scale values.
+ *
+ *  @param      device          The device on which the kernel will execute.
+ *
+ *  @param      transposeLeft   A boolean value which indicates if the left input matrix should be
+ *                              used in transposed form.  If 'YES' then op(A) = A**T, otherwise
+ *                              op(A) = A.
+ *
+ *  @param      transposeRight  A boolean value which indicates if the right input matrix should be
+ *                              used in transposed form.  If 'YES' then op(B) = B**T, otherwise
+ *                              op(B) = B.
+ *
+ *  @param      resultRows      The number of rows in the result matrix, M in BLAS GEMM description.
+ *
+ *  @param      resultColumns   The number of columns in the result matrix, N in BLAS GEMM description.
+ *
+ *  @param      interiorColumns The number of columns of the left input matrix after the
+ *                              appropriate transpose operation has been applied. K in BLAS
+ *                              GEMM description.
+ *
+ *  @param      alpha           The scale factor to apply to the product.  Specified in double
+ *                              precision.  Will be converted to the appropriate precision in the
+ *                              implementation subject to rounding and/or clamping as necessary.
+ *
+ *  @param      beta            The scale factor to apply to the initial values of C.  Specified
+ *                              in double precision.  Will be converted to the appropriate precision in the
+ *                              implementation subject to rounding and/or clamping as necessary.
+ *
+ *  @return     A valid MPSMatrixMultiplication object or nil, if failure.
+ */
+-(nonnull instancetype) initWithDevice: (nonnull id<MTLDevice>) device
+                         transposeLeft: (BOOL) transposeLeft
+                        transposeRight: (BOOL) transposeRight
+                            resultRows: (NSUInteger) resultRows
+                         resultColumns: (NSUInteger) resultColumns
+                       interiorColumns: (NSUInteger) interiorColumns
+                                 alpha: (double) alpha
+                                  beta: (double) beta;
+
+/*!
+ @discussion Use the above initialization method instead.
+ */
+-(nonnull instancetype) initWithDevice: (nonnull id <MTLDevice>) device NS_UNAVAILABLE;
+
+/*!
+ *  @abstract   Encode a MPSMatrixMultiplication object to a command buffer.
+ *
+ *  @param      commandBuffer   A valid MTLCommandBuffer to receive the encoded kernel.
+ *
+ *  @param      leftMatrix      A valid MPSMatrix object which specifies the left input matrix.
+ *
+ *  @param      rightMatrix     A valid MPSMatrix object which specifies the right input matrix.
+ *
+ *  @param      resultMatrix    A valid MPSMatrix object which specifies the addend matrix which will
+ *                              also be overwritten by the result.
+ *
+ *  @discussion Certain constraints apply to the sizes of the matrices depending on the transposition
+ *              operations and sizes requested at initialization time as well as the origins at the time
+ *              this routine is called:
+ *
+ *              The left input matrix must be large enough to hold an array of size resultRows x interiorColumns
+ *              elements beginning at leftMatrixOrigin.
+ *
+ *              The right input matrix must be large enough to hold an array of size interiorColumns x resultColumns
+ *              elements beginning at rightMatrixOrigin.
+ *
+ *              The result matrix must be large enough to hold an array of size resultRows x resultColumns
+ *              elements beginning at resultMatrixOrigin.
+ */
+-(void) encodeToCommandBuffer: (nonnull id <MTLCommandBuffer>) commandBuffer
+                   leftMatrix: (MPSMatrix const* __nonnull) leftMatrix
+                  rightMatrix: (MPSMatrix const* __nonnull) rightMatrix
+                 resultMatrix: (MPSMatrix* __nonnull) resultMatrix
+                    NS_SWIFT_NAME(encode(commandBuffer:leftMatrix:rightMatrix:resultMatrix:));
+
+
+
+@end // MPSMatrixMultiplication
+
+
+#endif /* MPSMatrixMultiplication_h */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSTypes.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSTypes.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSTypes.h	2016-05-21 08:10:52.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MPSTypes.h	2016-06-26 07:44:29.000000000 +0200
@@ -187,6 +187,18 @@
     MPSImageFeatureChannelFormatFloat32     MPS_ENUM_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0, __TVOS_10_0)  = 4,
     
 };
+   
+/*! @typedef    MPSDataType
+ *  @discussion A value to specify a type of data.
+ *
+ *  @constant   MPSDataTypeFloatBit     A common bit for all floating point data types.
+ *  @constant   MSPDataTypeFloat32      32-bit floating point (single-precision).
+ */
+typedef NS_ENUM(uint32_t, MPSDataType)
+{
+    MPSDataTypeFloatBit MPS_ENUM_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0) = 0x10000000,
+    MPSDataTypeFloat32  MPS_ENUM_AVAILABLE_STARTING( __MAC_10_12, __IPHONE_10_0, __TVOS_10_0) = MPSDataTypeFloatBit | 32
+};
     
 /*!
  *  @struct     MPSOffset
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MetalPerformanceShaders.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MetalPerformanceShaders.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MetalPerformanceShaders.h	2016-05-21 08:10:52.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalPerformanceShaders.framework/Headers/MetalPerformanceShaders.h	2016-06-26 07:44:29.000000000 +0200
@@ -15,6 +15,7 @@
 #import <MetalPerformanceShaders/MPSImageResampling.h>
 #import <MetalPerformanceShaders/MPSImageThreshold.h>
 #import <MetalPerformanceShaders/MPSImageTranspose.h>
+#import <MetalPerformanceShaders/MPSMatrixMultiplication.h>
 
 
 //
@@ -54,17 +55,21 @@
  *  @subsection subsection_mpsimage  MPSImages
  *  Convolutional neural networking (CNN) filters may need more than the four data channels that a
  *  MTLTexture can provide. In these cases, the MPSImage is used instead as an abstraction
- *  layer on top of a MTLTexture. When more than 4 channels are needed, extra RGBA pixels are inserted
- *  horizontally adjacent to the start of each pixel to hold the additional channels. The MPSImage
- *  tracks this information as the number of "feature channels" in an image. The underlying MTLTexture.width 
- *  may be several times that of the MPSImage.width to hold the extra data.
+ *  layer on top of a MTLTexture. When more than 4 channels are needed, additional textures in the texture2d 
+ *  array are added to hold additional channels in sets of four. The MPSImage tracks this information as the 
+ *  number of "feature channels" in an image.
  *
  *  @subsection subsection_mpstemporaryimage  MPSTemporaryImages
  *  The MPSTemporaryImage (subclass of MPSImage) extends the MPSImage to provide advanced caching of
  *  unused memory to increase performance and reduce memory footprint. They are intended as fast
  *  GPU-only storage for intermediate image data needed only transiently within a single MTLCommandBuffer.
  *  They accelerate the common case of image data which is created only to be consumed and destroyed
- *  immediately by the next operation(s) in a MTLCommandBuffer.
+ *  immediately by the next operation(s) in a MTLCommandBuffer.  MPSTemporaryImages provide convenient and 
+ *  simple way to save memory by automatically aliasing other MPSTemporaryImages in the MTLCommandBuffer.
+ *  Because they alias (share texel storage with) other textures in the same MTLCommandBuffer, the valid 
+ *  lifetime of the data in a MPSTeporaryImage is extremely short, limited to a portion of a MTLCommandBuffer. 
+ *  You can not read or write data to a MPSTemporaryImage using the CPU, or use the data in other MTLCommandBuffers.
+ *  Use regular MPSImages for more persistent storage.
  *
  *  @section section_discussion     The MPSKernel
  *
@@ -425,9 +430,8 @@
  *
  *
  *  @subsection subsection_CNN     Convolutional Neural Networks
- *  Convolutional Neural Networks (CNN) is a machine learning method commonly used for object
- *  recognition within images that attempts to model the visual cortex as a sequence of convolution,
- *  rectification, pooling and normalization steps. Several CNN filters commonly derived from the MPSCNNKernel
+ *  Convolutional Neural Networks (CNN) is a machine learning technique that attempts to model the visual cortex as a sequence 
+ *  of convolution, rectification, pooling and normalization steps. Several CNN filters commonly derived from the MPSCNNKernel
  *  base class are provided to help you implement these steps as efficiently as possible.
  *
  *      MPSCNNNeuronLinear              <MetalPerformanceShaders/MPSCNN.h>      A linear neuron activation function
@@ -435,6 +439,7 @@
  *      MPSCNNNeuronSigmoid             <MetalPerformanceShaders/MPSCNN.h>      A sigmoid neuron activation function 1/(1+e**-x)
  *      MPSCNNNeuronTanH                <MetalPerformanceShaders/MPSCNN.h>      A neuron activation function using hyperbolic tangent
  *      MPSCNNConvolution               <MetalPerformanceShaders/MPSCNN.h>      A 4D convolution tensor
+ *      MPSCNNFullyConnected            <MetalPerformanceShaders/MPSCNN.h>      A fully connected CNN layer
  *      MPSCNNPoolingMax                <MetalPerformanceShaders/MPSCNN.h>      The maximum value in the pooling area
  *      MPSCNNPoolingAverage            <MetalPerformanceShaders/MPSCNN.h>      The average value in the pooling area
  *      MPSCNNSpatialNormalization      <MetalPerformanceShaders/MPSCNN.h>
@@ -442,13 +447,15 @@
  *      MPSCNNSoftmax                   <MetalPerformanceShaders/MPSCNN.h>      exp(pixel(x,y,k))/sum(exp(pixel(x,y,0)) ... exp(pixel(x,y,N-1))
  *
  *  MPSCNNKernels operate on MPSImages.  MPSImages are at their core MTLTextures. However, whereas
- *   MTLTextures commonly represent image or texel data, a MPSImage is a more abstract representation
+ *  MTLTextures commonly represent image or texel data, a MPSImage is a more abstract representation
  *  of image features. The channels within a MPSImage do not necessarily correspond to colors in a
  *  color space. (Though, they can.) As a result, there can be many more than four of them. 32 or 64 channels
  *  per pixel is not uncommon.  This is achieved on the MTLTexture hardware abstraction by inserting
  *  extra RGBA pixels to handle the additional feature channels (if any) beyond 4. Thus, each CNN pixel
  *  in a 32 channel image is represented as 8 horizontally consecutive RGBA pixels in the texture.
- *  The width of the MTLTexture is correspondingly wider than the width of the MPSImage.
+ *  The width of the MTLTexture is correspondingly wider than the width of the MPSImage. Thus, in the common
+ *  vernacular, MPSCNNKernels are layer operations why MPS(Temporary)Images are used to store layer
+ *  inputs and outputs.
  *
  *  MPSImages can be created from existing MTLTextures. They may also be created anew from a MPSImageDescriptor
  *  and backed with either standard texture memory, or as MPSTemporaryImages using memory drawn from MPS's
@@ -456,7 +463,33 @@
  *  but come with significant restrictions that should be understood before using them. For example, their contents
  *  are only valid during the GPU-side execution of a single MTLCommandBuffer and can not be read from or written to
  *  by the CPU. They are provided as an efficient way to hold CNN computations that are used immediately within the
- *  scope of the same MTLCommandBuffer and then discarded.
+ *  scope of the same MTLCommandBuffer and then discarded. We also support concatenation by allowing the user to 
+ *  define from which destination feature channel to start writing the output of the current layer. In this way
+ *  the application can make a large MPSImage or MPSTemporaryImage and fill in parts of it with multiple layers
+ *  (as long as the destination feature channel offset is a multiple of 4).
+ *
+ *  Some CNN Tips:
+ *  - Think carefully about the edge mode requested for pooling layers. The default is clamp to zero, but there
+ *    are times when clamp to edge value may be better.
+ *  - To avoid falling off the edge of an image for filters that have a filter area (convolution, pooling) set the
+ *    MPSCNNKernel.offset = (MPSOffset){ .x = kernelWidth/2, .y = kernelHeight/2, .z = 0}; and reduce the size 
+ *    of the output image by {kernelWidth-1, kernelHeight-1,0}. The filter area stretcheds up and to the left
+ *    of the MPSCNNKernel.offset by {kernelWidth/2, kernelHeight/2}. While consistent with other MPS imaging operations,
+ *    this behavior is different from some other CNN implementations.
+ *  - Please remember:
+ *      MPSCNNConvolution takes weights in the order weight[outputChannels][kernelHeight][kernelWidth][inputChannels / groups]
+ *      MPSCNNFullyConnected takes weights in the order weight[outputChannels][sourceWidth][sourceHeight][inputChannels]
+ *  - Initialize MPSCNNKernels once and reuse them
+ *  - You can use MPSCNNNeurons and other Filters in MPS to perform pre-processing of images, such as scaling and resizing.
+ *  - Use MPSTemporaryImages for intermediate images that live for a short period of time (less than one MTLCommandBuffer).
+ *      MPSTemporaryImages can reduce the amount of memory used by the convolutional neural network by several fold, and
+ *      similarly reduce the amount of CPU time spent allocating storage and latency between MTLCommandBuffer.commit
+ *      and when the work actually starts on the GPU.  MPSTemporaryImage are for short lived storage within the time 
+ *      period of the execution of a single MTLCommandBuffer. You can not read or write to a MPSTemporaryImage using the CPU.
+ *      Generally, they should be created as needed and thrown away promptly.  Persistent objects should not retain them.
+ *      Please be sure to understand the use of the MPSTemporaryImage.readCount.
+ *  - Because MPS encodes its work in place in your MTLCommandBuffer, you always have the option to insert your own
+ *      code in between MPSCNNKernels as a Metal shader for tasks not covered by MPS. You need not use MPS for everything.
  *
  *  @section  section_validation    MPS API validation
  *  MPS uses the same API validation layer that Metal uses to alert you to API mistakes while

```