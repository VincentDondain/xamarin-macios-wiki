#Metal.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLBlitCommandEncoder.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLBlitCommandEncoder.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLBlitCommandEncoder.h	2016-05-16 08:17:34.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLBlitCommandEncoder.h	2016-06-26 08:49:26.000000000 +0200
@@ -110,7 +110,7 @@
  @method updateFence:
  @abstract Update the event to capture all GPU work so far enqueued by this encoder.
  @discussion The event is updated at kernel submission to maintain global order and prevent deadlock.
- Drivers may delay fence updates until the end of the encoder. Drivers may also wait on fences at the beginning of an encoder. It is therefore illegal to both update and wait on the same fence in the same encoder.
+ Drivers may delay fence updates until the end of the encoder. Drivers may also wait on fences at the beginning of an encoder. It is therefore illegal to wait on a fence after it has been updated in the same encoder.
  */
 - (void)updateFence:(id <MTLFence>)fence NS_AVAILABLE(NA, 10_0);
 
@@ -118,7 +118,7 @@
  @method waitForFence:
  @abstract Prevent further GPU work until the event is reached.
  @discussion The event is evaluated at kernel submision to maintain global order and prevent deadlock.
- Drivers may delay fence updates until the end of the encoder. Drivers may also wait on fences at the beginning of an encoder. It is therefore illegal to both update and wait on the same fence in the same encoder.
+ Drivers may delay fence updates until the end of the encoder. Drivers may also wait on fences at the beginning of an encoder. It is therefore illegal to wait on a fence after it has been updated in the same encoder.
  */
 - (void)waitForFence:(id <MTLFence>)fence NS_AVAILABLE(NA, 10_0);
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLCommandBuffer.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLCommandBuffer.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLCommandBuffer.h	2016-05-18 02:19:27.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLCommandBuffer.h	2016-06-26 08:34:35.000000000 +0200
@@ -82,7 +82,7 @@
     MTLCommandBufferErrorNotPermitted = 7,
     MTLCommandBufferErrorOutOfMemory = 8,
     MTLCommandBufferErrorInvalidResource = 9,
-    MTLCommandBufferErrorMemoryless = 10,
+    MTLCommandBufferErrorMemoryless NS_AVAILABLE_IOS(10_0) = 10 ,
 } NS_ENUM_AVAILABLE(10_11, 8_0);
 
 typedef void (^MTLCommandBufferHandler)(id <MTLCommandBuffer>);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputeCommandEncoder.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputeCommandEncoder.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputeCommandEncoder.h	2016-05-18 03:41:30.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputeCommandEncoder.h	2016-06-26 07:42:15.000000000 +0200
@@ -60,7 +60,7 @@
  @method setBuffers:offsets:withRange:
  @brief Set an array of global buffers for all compute kernels with the given bind point range.
  */
-- (void)setBuffers:(const id <MTLBuffer> __nullable [__nullable])buffers offsets:(const NSUInteger [__nullable])offsets withRange:(NSRange)range;
+- (void)setBuffers:(const id <MTLBuffer> __nullable [])buffers offsets:(const NSUInteger [])offsets withRange:(NSRange)range;
 
 /*!
  @method setTexture:atIndex:
@@ -106,6 +106,8 @@
 
 
 
+- (void)setStageInRegion:(MTLRegion)region NS_AVAILABLE(10_12, 10_0);
+
 /*
  @method dispatchThreadgroups:threadsPerThreadgroup:
  @abstract Enqueue a compute function dispatch.
@@ -125,7 +127,7 @@
  @method updateFence:
  @abstract Update the event to capture all GPU work so far enqueued by this encoder.
  @discussion The event is updated at kernel submission to maintain global order and prevent deadlock.
- Drivers may delay fence updates until the end of the encoder. Drivers may also wait on fences at the beginning of an encoder. It is therefore illegal to both update and wait on the same fence in the same encoder.
+ Drivers may delay fence updates until the end of the encoder. Drivers may also wait on fences at the beginning of an encoder. It is therefore illegal to wait on a fence after it has been updated in the same encoder.
  */
 - (void)updateFence:(id <MTLFence>)fence NS_AVAILABLE(NA, 10_0);
 
@@ -133,7 +135,7 @@
  @method waitForFence:
  @abstract Prevent further GPU work until the event is reached.
  @discussion The event is evaluated at kernel submision to maintain global order and prevent deadlock.
- Drivers may delay fence updates until the end of the encoder. Drivers may also wait on fences at the beginning of an encoder. It is therefore illegal to both update and wait on the same fence in the same encoder.
+ Drivers may delay fence updates until the end of the encoder. Drivers may also wait on fences at the beginning of an encoder. It is therefore illegal to wait on a fence after it has been updated in the same encoder.
  */
 - (void)waitForFence:(id <MTLFence>)fence NS_AVAILABLE(NA, 10_0);
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputePipeline.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputePipeline.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputePipeline.h	2016-05-18 03:41:30.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputePipeline.h	2016-06-26 07:42:15.000000000 +0200
@@ -8,6 +8,7 @@
 #import <Metal/MTLDefines.h>
 #import <Metal/MTLDevice.h>
 #import <Metal/MTLArgument.h>
+#import <Metal/MTLStageInputOutputDescriptor.h>
 
 NS_ASSUME_NONNULL_BEGIN
 NS_CLASS_AVAILABLE(10_11, 8_0)
@@ -39,6 +40,13 @@
  */
 @property (readwrite, nonatomic) BOOL threadGroupSizeIsMultipleOfThreadExecutionWidth;
 
+
+/*!
+ @property computeDataDescriptor
+ @abstract An MTLStageInputOutputDescriptor to fetch data from buffers
+ */
+@property (nullable, copy, nonatomic) MTLStageInputOutputDescriptor *stageInputDescriptor NS_AVAILABLE(10_12, 10_0);
+
 /*!
  @method reset
  @abstract Restore all compute pipeline descriptor properties to their default values.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h	2016-05-18 02:19:28.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h	2016-06-26 07:26:24.000000000 +0200
@@ -24,6 +24,7 @@
 @protocol MTLSamplerState;
 @protocol MTLRenderPipelineState;
 @protocol MTLComputePipelineState;
+@protocol MTLHeap;
 @protocol MTLFence;
 
 @class MTLSamplerDescriptor;
@@ -37,10 +38,9 @@
 @class MTLComputePipelineDescriptor;
 @class MTLComputePipelineReflection;
 @class MTLCommandQueueDescriptor;
-
-@protocol MTLHeap;
 @class MTLHeapDescriptor;
 
+
 /*!
  @brief Returns a reference to the preferred system default Metal device.
  @discussion On Mac OS X systems that support automatic graphics switching, calling
@@ -48,7 +48,7 @@
  GPU.  On other systems that support more than one GPU it will return the GPU that
  is associated with the main display.
  */
-MTL_EXTERN id <MTLDevice> __nullable MTLCreateSystemDefaultDevice(void) NS_AVAILABLE(10_11, 8_0);
+MTL_EXTERN id <MTLDevice> __nullable MTLCreateSystemDefaultDevice(void) NS_AVAILABLE(10_11, 8_0) NS_RETURNS_RETAINED;
 
 /*!
  @brief Returns all Metal devices in the system.
@@ -56,7 +56,7 @@
  decision about which GPU to use up to the application based on whatever criteria
  it deems appropriate.
 */
-MTL_EXTERN NSArray <id<MTLDevice>> *MTLCopyAllDevices(void) NS_AVAILABLE_MAC(10_11);
+MTL_EXTERN NSArray <id<MTLDevice>> *MTLCopyAllDevices(void) NS_AVAILABLE_MAC(10_11) NS_RETURNS_RETAINED;
 
 typedef NS_ENUM(NSUInteger, MTLFeatureSet)
 {
@@ -149,6 +149,18 @@
 @property (readonly, getter=isHeadless) BOOL headless NS_AVAILABLE_MAC(10_11);
 
 /*!
+ @property sharedMemorySize
+ @abstract Return the maximum amount of shared system memory this device can use.
+*/
+@property (readonly) uint64_t sharedMemorySize NS_AVAILABLE(10_12, 10_0);
+ 
+/*!
+ @property dedicatedMemorySize
+ @abstract Return the maximum amount of dedicated memory this device has.
+*/
+@property (readonly) uint64_t dedicatedMemorySize NS_AVAILABLE(10_12, 10_0);
+ 
+/*!
  @property depth24Stencil8PixelFormatSupported
  @abstract If YES, device supports MTLPixelFormatDepth24Unorm_Stencil8.
  */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLFunctionConstantValues.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLFunctionConstantValues.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLFunctionConstantValues.h	2016-05-18 03:41:30.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLFunctionConstantValues.h	2016-06-26 07:42:15.000000000 +0200
@@ -21,7 +21,6 @@
 // using names
 - (void)setConstantValue:(const void *)value type:(MTLDataType)type withName:(NSString *)name;
 
-
 // delete all the constants
 - (void)reset;
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLHeap.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLHeap.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLHeap.h	2016-05-18 03:41:30.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLHeap.h	2016-06-26 07:42:15.000000000 +0200
@@ -14,7 +14,6 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-
 /*!
  @class MTLHeapDescriptor
  */
@@ -79,16 +78,17 @@
 @property (readonly) MTLCPUCacheMode cpuCacheMode;
 
 /*!
- @property totalSize
- @abstract The total size of the heap specificed at creation, in bytes.
+ @property size
+ @abstract Heap size in bytes, specified at creation time and rounded up to device specific alignment.
  */
-@property (readonly) NSUInteger totalSize;
+@property (readonly) NSUInteger size;
+
 
 /*!
- @property currentSize
- @abstract The size of all resources allocated from the heap, in bytes.
+ @property usedSize
+ @abstract The size in bytes, of all resources allocated from the heap.
  */
-@property (readonly) NSUInteger currentSize;
+@property (readonly) NSUInteger usedSize;
 
 /*!
  @method maxAvailableSizeWithAlignment:
@@ -122,5 +122,4 @@
 
 @end
 
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h	2016-05-16 08:17:34.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h	2016-06-26 07:26:24.000000000 +0200
@@ -30,7 +30,18 @@
 @property (readonly) NSUInteger                   attributeIndex;
 @property (readonly) MTLDataType                  attributeType NS_AVAILABLE(10_11, 8_3);
 @property (readonly, getter=isActive) BOOL        active;
+@property (readonly, getter=isPatchData) BOOL              patchData NS_AVAILABLE(10_12, 10_0);
+@property (readonly, getter=isPatchControlPointData) BOOL  patchControlPointData NS_AVAILABLE(10_12, 10_0);
+
+@end
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface MTLAttribute : NSObject
 
+@property (nullable, readonly) NSString          *name;
+@property (readonly) NSUInteger                   attributeIndex;
+@property (readonly) MTLDataType                  attributeType;
+@property (readonly, getter=isActive) BOOL        active;
 @property (readonly, getter=isPatchData) BOOL              patchData NS_AVAILABLE(10_12, 10_0);
 @property (readonly, getter=isPatchControlPointData) BOOL  patchControlPointData NS_AVAILABLE(10_12, 10_0);
 
@@ -113,6 +124,12 @@
 @property (nullable, readonly) NSArray <MTLVertexAttribute *> *vertexAttributes;
 
 /*!
+ @property stageInputAttributes
+ @abstract Returns an array describing the attributes
+ */
+@property (nullable, readonly) NSArray <MTLAttribute *> *stageInputAttributes NS_AVAILABLE(10_12, 10_0);
+
+/*!
  @property name
  @abstract The name of the function in the shading language.
  */
@@ -229,7 +246,7 @@
  avoid waiting on the compiler.
  */
 - (nullable id <MTLFunction>) newFunctionWithName:(NSString *)name constantValues:(MTLFunctionConstantValues *)constantValues
-					error:(__autoreleasing NSError **)error;
+					error:(__autoreleasing NSError **)error NS_AVAILABLE(10_12, 10_0);
 
 /*!
  @method newFunctionWithName:constantValues:completionHandler:
@@ -237,7 +254,7 @@
  @discussion This method is asynchronous since it is will call the compiler.
  */
 - (void) newFunctionWithName:(NSString *)name constantValues:(MTLFunctionConstantValues *)constantValues
-			completionHandler:(void (^)(id<MTLFunction> __nullable function, NSError* error))completionHandler;
+			completionHandler:(void (^)(id<MTLFunction> __nullable function, NSError* error))completionHandler NS_AVAILABLE(10_12, 10_0);
 
 /*!
  @property functionNames
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderCommandEncoder.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderCommandEncoder.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderCommandEncoder.h	2016-05-18 03:41:30.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderCommandEncoder.h	2016-06-26 08:49:27.000000000 +0200
@@ -11,6 +11,7 @@
 #import <Metal/MTLCommandBuffer.h>
 #import <Metal/MTLRenderPass.h>
 #import <Metal/MTLFence.h>
+#import <Metal/MTLStageInputOutputDescriptor.h>
 
 NS_ASSUME_NONNULL_BEGIN
 @protocol MTLDevice;
@@ -30,11 +31,6 @@
     MTLPrimitiveTypeTriangleStrip = 4,
 } NS_ENUM_AVAILABLE(10_11, 8_0);
 
-typedef NS_ENUM(NSUInteger, MTLIndexType) {
-    MTLIndexTypeUInt16 = 0,
-    MTLIndexTypeUInt32 = 1,
-} NS_ENUM_AVAILABLE(10_11, 8_0);
-
 typedef NS_ENUM(NSUInteger, MTLVisibilityResultMode) {
     MTLVisibilityResultModeDisabled = 0,
     MTLVisibilityResultModeBoolean = 1,
@@ -115,7 +111,6 @@
     MTLRenderStageFragment = (1UL << 1),
 } NS_ENUM_AVAILABLE_IOS(10_0);
 
-
 /*!
  @protocol MTLRenderCommandEncoder
  @discussion MTLRenderCommandEncoder is a container for graphics rendering state and the code to translate the state into a command format that the device can execute. 
@@ -153,7 +148,7 @@
  @method setVertexBuffers:offsets:withRange:
  @brief Set an array of global buffers for all vertex shaders with the given bind point range.
  */
-- (void)setVertexBuffers:(const id <MTLBuffer> __nullable [__nullable])buffers offsets:(const NSUInteger [__nullable])offsets withRange:(NSRange)range;
+- (void)setVertexBuffers:(const id <MTLBuffer> __nullable [])buffers offsets:(const NSUInteger [])offsets withRange:(NSRange)range;
 
 /*!
  @method setVertexTexture:atIndex:
@@ -213,7 +208,7 @@
 @method setDepthClipMode:
 @brief Controls what is done with fragments outside of the near or far planes.
 */
-- (void)setDepthClipMode:(MTLDepthClipMode)depthClipMode NS_AVAILABLE(10_11, 9_0);
+- (void)setDepthClipMode:(MTLDepthClipMode)depthClipMode NS_AVAILABLE(10_11, NA);
 
 /*!
  @method setDepthBias:slopeScale:clamp:
@@ -257,7 +252,7 @@
  @method setFragmentBuffers:offsets:withRange:
  @brief Set an array of global buffers for all fragment shaders with the given bind point range.
  */
-- (void)setFragmentBuffers:(const id <MTLBuffer> __nullable [__nullable])buffers offsets:(const NSUInteger [__nullable])offset withRange:(NSRange)range;
+- (void)setFragmentBuffers:(const id <MTLBuffer> __nullable [])buffers offsets:(const NSUInteger [])offset withRange:(NSRange)range;
 
 /*!
  @method setFragmentTexture:atIndex:
@@ -441,8 +436,12 @@
  */
 - (void)drawIndexedPrimitives:(MTLPrimitiveType)primitiveType indexType:(MTLIndexType)indexType indexBuffer:(id <MTLBuffer>)indexBuffer indexBufferOffset:(NSUInteger)indexBufferOffset indirectBuffer:(id <MTLBuffer>)indirectBuffer indirectBufferOffset:(NSUInteger)indirectBufferOffset NS_AVAILABLE(10_11, 9_0);
 
+/*!
+ @method textureBarrier:
+ @brief Ensure that following fragment shaders can read textures written by previous draw calls (in particular the framebuffer)
+ */
+- (void)textureBarrier NS_AVAILABLE_MAC(10_11);
 
-@optional
 /*!
  @method updateFence:afterStages:
  @abstract Update the event to capture all GPU work so far enqueued by this encoder for the given stages.
@@ -458,7 +457,6 @@
  On iOS, render command encoder fence waits always occur the beginning of the encoder.
  */
 - (void)waitForFence:(id <MTLFence>)fence beforeStages:(MTLRenderStages)stages NS_AVAILABLE_IOS(10_0);
-@required
 
 -(void)setTessellationFactorBuffer:(nullable id <MTLBuffer>)buffer offset:(NSUInteger)offset instanceStride:(NSUInteger)instanceStride NS_AVAILABLE(10_12, 10_0);
 
@@ -466,11 +464,11 @@
 
 -(void)drawPatches:(NSUInteger)numberOfPatchControlPoints patchStart:(NSUInteger)patchStart patchCount:(NSUInteger)patchCount patchIndexBuffer:(nullable id <MTLBuffer>)patchIndexBuffer patchIndexBufferOffset:(NSUInteger)patchIndexBufferOffset instanceCount:(NSUInteger)instanceCount baseInstance:(NSUInteger)baseInstance NS_AVAILABLE(10_12, 10_0);
 
--(void)drawPatches:(NSUInteger)numberOfPatchControlPoints patchIndexBuffer:(nullable id <MTLBuffer>)patchIndexBuffer patchIndexBufferOffset:(NSUInteger)patchIndexBufferOffset indirectBuffer:(id <MTLBuffer>)indirectBuffer indirectBufferOffset:(NSUInteger)indirectBufferOffset NS_AVAILABLE(10_12, 10_0);
+-(void)drawPatches:(NSUInteger)numberOfPatchControlPoints patchIndexBuffer:(nullable id <MTLBuffer>)patchIndexBuffer patchIndexBufferOffset:(NSUInteger)patchIndexBufferOffset indirectBuffer:(id <MTLBuffer>)indirectBuffer indirectBufferOffset:(NSUInteger)indirectBufferOffset NS_AVAILABLE(10_12, NA);
 
 -(void)drawIndexedPatches:(NSUInteger)numberOfPatchControlPoints patchStart:(NSUInteger)patchStart patchCount:(NSUInteger)patchCount patchIndexBuffer:(nullable id <MTLBuffer>)patchIndexBuffer patchIndexBufferOffset:(NSUInteger)patchIndexBufferOffset controlPointIndexBuffer:(id <MTLBuffer>)controlPointIndexBuffer controlPointIndexBufferOffset:(NSUInteger)controlPointIndexBufferOffset instanceCount:(NSUInteger)instanceCount baseInstance:(NSUInteger)baseInstance NS_AVAILABLE(10_12, 10_0);
 
--(void)drawIndexedPatches:(NSUInteger)numberOfPatchControlPoints patchIndexBuffer:(nullable id <MTLBuffer>)patchIndexBuffer patchIndexBufferOffset:(NSUInteger)patchIndexBufferOffset controlPointIndexBuffer:(id <MTLBuffer>)controlPointIndexBuffer controlPointIndexBufferOffset:(NSUInteger)controlPointIndexBufferOffset indirectBuffer:(id <MTLBuffer>)indirectBuffer indirectBufferOffset:(NSUInteger)indirectBufferOffset NS_AVAILABLE(10_12, 10_0);
+-(void)drawIndexedPatches:(NSUInteger)numberOfPatchControlPoints patchIndexBuffer:(nullable id <MTLBuffer>)patchIndexBuffer patchIndexBufferOffset:(NSUInteger)patchIndexBufferOffset controlPointIndexBuffer:(id <MTLBuffer>)controlPointIndexBuffer controlPointIndexBufferOffset:(NSUInteger)controlPointIndexBufferOffset indirectBuffer:(id <MTLBuffer>)indirectBuffer indirectBufferOffset:(NSUInteger)indirectBufferOffset NS_AVAILABLE(10_12, NA);
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLResource.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLResource.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLResource.h	2016-05-16 08:17:34.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLResource.h	2016-06-26 08:49:27.000000000 +0200
@@ -206,16 +206,20 @@
 /*!
  @method makeAliasable
  @abstract Allow future heap sub-allocations to alias against this resource's memory.
- @discussion It is illegal to call this method on a non heap-based resource. The debug layer will raise an exception.
- One a resource is made aliasable, the decision cannot be reverted.
+ @discussion It is illegal to call this method on a non heap-based resource. 
+ It is also illegal to call this method on texture views created from heap-based textures.
+ The debug layer will raise an exception. Calling this method on textures sub-allocated
+ from Buffers backed by heap memory has no effect.
+ Once a resource is made aliasable, the decision cannot be reverted.
  */
 -(void) makeAliasable NS_AVAILABLE(NA, 10_0);
 
 /*!
  @method isAliasable
  @abstract Returns whether future heap sub-allocations may alias against this resource's memory.
- @return YES if <st>makeAliasable</st> was previously called on this resource. NO otherwise.
- Also returns NO when storage mode is memoryless.
+ @return YES if <st>makeAliasable</st> was previously successfully called on this resource. NO otherwise.
+ If resource is sub-allocated from other resource created on the heap, isAliasable returns 
+ aliasing state of that base resource. Also returns NO when storage mode is memoryless.
  */
 -(BOOL) isAliasable NS_AVAILABLE(NA, 10_0);
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLSampler.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLSampler.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLSampler.h	2016-05-18 03:41:30.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLSampler.h	2016-06-26 07:26:25.000000000 +0200
@@ -64,9 +64,33 @@
     MTLSamplerAddressModeRepeat = 2,
     MTLSamplerAddressModeMirrorRepeat = 3,
     MTLSamplerAddressModeClampToZero = 4,
+    /*!
+     @constant MTLSamplerAddressModeClampToBorderColor
+     Clamp to border color returns the value specified by the borderColor variable of the MTLSamplerDesc.
+     */
+    MTLSamplerAddressModeClampToBorderColor NS_AVAILABLE_MAC(10_12) = 5,
 } NS_ENUM_AVAILABLE(10_11, 8_0);
 
 /*!
+ @enum MTLSamplerBorderColor
+ @abstract Specify the color value that will be clamped to when the sampler address mode is MTLSamplerAddressModeClampToBorderColor.
+ 
+ @constant MTLSamplerBorderColorTransparentBlack
+ Transparent black returns {0,0,0,1} for clamped texture values.
+ 
+ @constant MTLSamplerBorderColorOpaqueBlack
+ OpaqueBlack returns {0,0,0,1} for clamped texture values.
+ 
+ @constant MTLSamplerBorderColorOpaqueWhite
+ OpaqueWhite returns {1,1,1,1} for clamped texture values.
+ */
+typedef NS_ENUM(NSUInteger, MTLSamplerBorderColor) {
+    MTLSamplerBorderColorTransparentBlack = 0,  // {0,0,0,0}
+    MTLSamplerBorderColorOpaqueBlack = 1,       // {0,0,0,1}
+    MTLSamplerBorderColorOpaqueWhite = 2,       // {1,1,1,1}
+};
+
+/*!
  @class MTLSamplerDescriptor
  @abstract A mutable descriptor used to configure a sampler.  When complete, this can be used to create an immutable MTLSamplerState.
  */
@@ -120,6 +144,12 @@
 @property (nonatomic) MTLSamplerAddressMode rAddressMode;
 
 /*!
+ @property borderColor
+ @abstract Set the color for the MTLSamplerAddressMode to one of the predefined in the MTLSamplerBorderColor enum.
+ */
+@property (nonatomic) MTLSamplerBorderColor borderColor NS_AVAILABLE_MAC(10_12);
+
+/*!
  @property normalizedCoordinates.
  @abstract If YES, texture coordates are from 0 to 1.  If NO, texture coordinates are 0..width, 0..height.
  @discussion normalizedCoordinates defaults to YES.  Non-normalized coordinates should only be used with 1D and 2D textures with the ClampToEdge wrap mode, otherwise the results of sampling are undefined.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLStageInputOutputDescriptor.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLStageInputOutputDescriptor.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLStageInputOutputDescriptor.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLStageInputOutputDescriptor.h	2016-06-26 06:48:53.000000000 +0200
@@ -0,0 +1,146 @@
+//
+//  MTLStageInputOutputDescriptor.h
+//  Metal
+//
+//  Copyright (c) 2014 Apple Inc. All rights reserved.
+//
+
+#import <Metal/MTLDefines.h>
+#import <Metal/MTLDevice.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+/*
+ MTLAttributeFormat
+*/
+typedef NS_ENUM(NSUInteger, MTLAttributeFormat)
+{
+    MTLAttributeFormatInvalid = 0,
+    
+    MTLAttributeFormatUChar2 = 1,
+    MTLAttributeFormatUChar3 = 2,
+    MTLAttributeFormatUChar4 = 3,
+    
+    MTLAttributeFormatChar2 = 4,
+    MTLAttributeFormatChar3 = 5,
+    MTLAttributeFormatChar4 = 6,
+    
+    MTLAttributeFormatUChar2Normalized = 7,
+    MTLAttributeFormatUChar3Normalized = 8,
+    MTLAttributeFormatUChar4Normalized = 9,
+    
+    MTLAttributeFormatChar2Normalized = 10,
+    MTLAttributeFormatChar3Normalized = 11,
+    MTLAttributeFormatChar4Normalized = 12,
+    
+    MTLAttributeFormatUShort2 = 13,
+    MTLAttributeFormatUShort3 = 14,
+    MTLAttributeFormatUShort4 = 15,
+    
+    MTLAttributeFormatShort2 = 16,
+    MTLAttributeFormatShort3 = 17,
+    MTLAttributeFormatShort4 = 18,
+    
+    MTLAttributeFormatUShort2Normalized = 19,
+    MTLAttributeFormatUShort3Normalized = 20,
+    MTLAttributeFormatUShort4Normalized = 21,
+    
+    MTLAttributeFormatShort2Normalized = 22,
+    MTLAttributeFormatShort3Normalized = 23,
+    MTLAttributeFormatShort4Normalized = 24,
+    
+    MTLAttributeFormatHalf2 = 25,
+    MTLAttributeFormatHalf3 = 26,
+    MTLAttributeFormatHalf4 = 27,
+    
+    MTLAttributeFormatFloat = 28,
+    MTLAttributeFormatFloat2 = 29,
+    MTLAttributeFormatFloat3 = 30,
+    MTLAttributeFormatFloat4 = 31,
+    
+    MTLAttributeFormatInt = 32,
+    MTLAttributeFormatInt2 = 33,
+    MTLAttributeFormatInt3 = 34,
+    MTLAttributeFormatInt4 = 35,
+    
+    MTLAttributeFormatUInt = 36,
+    MTLAttributeFormatUInt2 = 37,
+    MTLAttributeFormatUInt3 = 38,
+    MTLAttributeFormatUInt4 = 39,
+    
+    MTLAttributeFormatInt1010102Normalized = 40,
+    MTLAttributeFormatUInt1010102Normalized = 41,
+    
+    
+} NS_ENUM_AVAILABLE(10_12, 10_0);
+
+
+typedef NS_ENUM(NSUInteger, MTLIndexType) {
+    MTLIndexTypeUInt16 = 0,
+    MTLIndexTypeUInt32 = 1,
+} NS_ENUM_AVAILABLE(10_11, 8_0);
+
+
+typedef NS_ENUM(NSUInteger, MTLStepFunction)
+{
+    MTLStepFunctionConstant = 0,
+
+    // vertex functions only
+    MTLStepFunctionPerVertex = 1,
+    MTLStepFunctionPerInstance = 2,
+    MTLStepFunctionPerPatch NS_ENUM_AVAILABLE(10_12, 10_0) = 3,
+    MTLStepFunctionPerPatchControlPoint NS_ENUM_AVAILABLE(10_12, 10_0) = 4,
+
+    // compute functions only
+    MTLStepFunctionThreadPositionInGridX = 5,
+    MTLStepFunctionThreadPositionInGridY = 6,
+    MTLStepFunctionThreadPositionInGridXIndexed = 7,
+    MTLStepFunctionThreadPositionInGridYIndexed = 8,
+} NS_ENUM_AVAILABLE(10_12, 10_0);
+
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface MTLBufferLayoutDescriptor : NSObject <NSCopying>
+@property (assign, nonatomic) NSUInteger stride;
+@property (assign, nonatomic) MTLStepFunction stepFunction;
+@property (assign, nonatomic) NSUInteger stepRate;
+@end
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface MTLBufferLayoutDescriptorArray : NSObject
+- (MTLBufferLayoutDescriptor *)objectAtIndexedSubscript:(NSUInteger)index;
+- (void)setObject:(nullable MTLBufferLayoutDescriptor *)bufferDesc atIndexedSubscript:(NSUInteger)index;
+@end
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface MTLAttributeDescriptor : NSObject <NSCopying>
+@property (assign, nonatomic) MTLAttributeFormat format;
+@property (assign, nonatomic) NSUInteger offset;
+@property (assign, nonatomic) NSUInteger bufferIndex;
+@end
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface MTLAttributeDescriptorArray : NSObject
+- (MTLAttributeDescriptor *)objectAtIndexedSubscript:(NSUInteger)index;
+- (void)setObject:(nullable MTLAttributeDescriptor *)attributeDesc atIndexedSubscript:(NSUInteger)index;
+@end
+
+/*
+ MTLStageInputOutputDescriptor
+ */
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface MTLStageInputOutputDescriptor : NSObject <NSCopying>
+
++ (MTLStageInputOutputDescriptor *)stageInputOutputDescriptor;
+
+@property (readonly) MTLBufferLayoutDescriptorArray *layouts;
+@property (readonly) MTLAttributeDescriptorArray *attributes;
+
+/* only used for compute with MTLStepFunction...Indexed */
+@property (assign, nonatomic) MTLIndexType indexType;
+@property (assign, nonatomic) NSUInteger indexBufferIndex;
+
+- (void)reset;
+
+@end
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLVertexDescriptor.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLVertexDescriptor.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLVertexDescriptor.h	2016-05-18 03:41:30.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLVertexDescriptor.h	2016-06-26 07:42:16.000000000 +0200
@@ -10,7 +10,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 /*
- MTLVertexFormat
+ MTLVertexFormat is deprecated, use MTLAttributeFormat instead
 */
 typedef NS_ENUM(NSUInteger, MTLVertexFormat)
 {

```