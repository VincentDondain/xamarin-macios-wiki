#Metal.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLArgument.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLArgument.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLArgument.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLArgument.h	2016-05-16 08:17:33.000000000 +0200
@@ -185,8 +185,8 @@
 @property (readonly) MTLTextureType textureType; // texture1D, texture2D...
 @property (readonly) MTLDataType    textureDataType; // half, float, int, or uint.
 
+@property (readonly) BOOL           isDepthTexture NS_AVAILABLE(10_12, 10_0); // true for depth textures
+@property (readonly) NSUInteger     arrayLength NS_AVAILABLE(10_12, 10_0);
+
 @end
 NS_ASSUME_NONNULL_END
-
-
-
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLBlitCommandEncoder.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLBlitCommandEncoder.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLBlitCommandEncoder.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLBlitCommandEncoder.h	2016-05-16 08:17:34.000000000 +0200
@@ -10,6 +10,7 @@
 #import <Metal/MTLCommandEncoder.h>
 #import <Metal/MTLBuffer.h>
 #import <Metal/MTLTexture.h>
+#import <Metal/MTLFence.h>
 
 NS_ASSUME_NONNULL_BEGIN
 /*!
@@ -105,5 +106,21 @@
  */
 - (void)copyFromBuffer:(id <MTLBuffer>)sourceBuffer sourceOffset:(NSUInteger)sourceOffset toBuffer:(id <MTLBuffer>)destinationBuffer destinationOffset:(NSUInteger)destinationOffset size:(NSUInteger)size;
 
+/*!
+ @method updateFence:
+ @abstract Update the event to capture all GPU work so far enqueued by this encoder.
+ @discussion The event is updated at kernel submission to maintain global order and prevent deadlock.
+ Drivers may delay fence updates until the end of the encoder. Drivers may also wait on fences at the beginning of an encoder. It is therefore illegal to both update and wait on the same fence in the same encoder.
+ */
+- (void)updateFence:(id <MTLFence>)fence NS_AVAILABLE(NA, 10_0);
+
+/*!
+ @method waitForFence:
+ @abstract Prevent further GPU work until the event is reached.
+ @discussion The event is evaluated at kernel submision to maintain global order and prevent deadlock.
+ Drivers may delay fence updates until the end of the encoder. Drivers may also wait on fences at the beginning of an encoder. It is therefore illegal to both update and wait on the same fence in the same encoder.
+ */
+- (void)waitForFence:(id <MTLFence>)fence NS_AVAILABLE(NA, 10_0);
+
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLBuffer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLBuffer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLBuffer.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLBuffer.h	2016-05-16 08:17:34.000000000 +0200
@@ -66,5 +66,20 @@
 */
 - (id <MTLTexture>)newTextureWithDescriptor:(MTLTextureDescriptor*)descriptor offset:(NSUInteger)offset bytesPerRow:(NSUInteger)bytesPerRow NS_AVAILABLE_IOS(8_0);
 
+/*!
+ @method addDebugMarker:range:
+ @abstract Adds a marker to a specific range in the buffer.
+ When inspecting a buffer in the GPU debugging tools the marker will be shown.
+ @param marker A label used for the marker.
+ @param range The range of bytes the marker is using.
+ */
+- (void)addDebugMarker:(NSString*)marker range:(NSRange)range NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @method removeAllDebugMarkers
+ @abstract Removes all debug markers from a buffer.
+ */
+- (void)removeAllDebugMarkers NS_AVAILABLE(10_12, 10_0);
+
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLCommandBuffer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLCommandBuffer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLCommandBuffer.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLCommandBuffer.h	2016-05-18 02:19:27.000000000 +0200
@@ -70,6 +70,7 @@
  @constant MTLCommandBufferErrorNotPermitted This process does not have access to use this device.
  @constant MTLCommandBufferErrorOutOfMemory Insufficient memory was available to execute this command buffer.
  @constant MTLCommandBufferErrorInvalidResource The command buffer referenced an invalid resource.  This is most commonly caused when the caller deletes a resource before executing a command buffer that refers to it.
+ @constant MTLCommandBufferErrorMemoryless One or more internal resources limits reached that prevent using memoryless render pass attachments. See error string for more detail.
  */
 typedef NS_ENUM(NSUInteger, MTLCommandBufferError)
 {
@@ -81,6 +82,7 @@
     MTLCommandBufferErrorNotPermitted = 7,
     MTLCommandBufferErrorOutOfMemory = 8,
     MTLCommandBufferErrorInvalidResource = 9,
+    MTLCommandBufferErrorMemoryless = 10,
 } NS_ENUM_AVAILABLE(10_11, 8_0);
 
 typedef void (^MTLCommandBufferHandler)(id <MTLCommandBuffer>);
@@ -146,6 +148,7 @@
  */
 - (void)presentDrawable:(id <MTLDrawable>)drawable atTime:(CFTimeInterval)presentationTime;
 
+
 /*!
  @method waitUntilScheduled
  @abstract Synchronously wait for this command buffer to be scheduled.
@@ -183,7 +186,7 @@
 - (id <MTLBlitCommandEncoder>)blitCommandEncoder;
 
 /*!
- @method renderCommandEncoderWithFramebuffer:
+ @method renderCommandEncoderWithDescriptor:
  @abstract returns a render command endcoder to encode into this command buffer.
  */
 - (id <MTLRenderCommandEncoder>)renderCommandEncoderWithDescriptor:(MTLRenderPassDescriptor *)renderPassDescriptor;
@@ -194,8 +197,9 @@
  */
 - (id <MTLComputeCommandEncoder>)computeCommandEncoder;
 
+
 /*!
- @method parallelRenderCommandEncoderWithFramebuffer:
+ @method parallelRenderCommandEncoderWithDescriptor:
  @abstract returns a parallel render pass encoder to encode into this command buffer.
  */
 - (id <MTLParallelRenderCommandEncoder>)parallelRenderCommandEncoderWithDescriptor:(MTLRenderPassDescriptor *)renderPassDescriptor;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLCommandQueue.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLCommandQueue.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLCommandQueue.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLCommandQueue.h	2016-05-16 08:17:34.000000000 +0200
@@ -46,4 +46,4 @@
 - (void)insertDebugCaptureBoundary;
 
 @end
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputeCommandEncoder.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputeCommandEncoder.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputeCommandEncoder.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputeCommandEncoder.h	2016-05-18 03:41:30.000000000 +0200
@@ -11,6 +11,7 @@
 #import <Metal/MTLCommandEncoder.h>
 #import <Metal/MTLTexture.h>
 #import <Metal/MTLCommandBuffer.h>
+#import <Metal/MTLFence.h>
 
 NS_ASSUME_NONNULL_BEGIN
 @protocol MTLFunction;
@@ -103,6 +104,8 @@
  */
 - (void)setThreadgroupMemoryLength:(NSUInteger)length atIndex:(NSUInteger)index;
 
+
+
 /*
  @method dispatchThreadgroups:threadsPerThreadgroup:
  @abstract Enqueue a compute function dispatch.
@@ -118,5 +121,21 @@
 - (void)dispatchThreadgroupsWithIndirectBuffer:(id <MTLBuffer>)indirectBuffer indirectBufferOffset:(NSUInteger)indirectBufferOffset threadsPerThreadgroup:(MTLSize)threadsPerThreadgroup NS_AVAILABLE(10_11, 9_0);
 
 
+/*!
+ @method updateFence:
+ @abstract Update the event to capture all GPU work so far enqueued by this encoder.
+ @discussion The event is updated at kernel submission to maintain global order and prevent deadlock.
+ Drivers may delay fence updates until the end of the encoder. Drivers may also wait on fences at the beginning of an encoder. It is therefore illegal to both update and wait on the same fence in the same encoder.
+ */
+- (void)updateFence:(id <MTLFence>)fence NS_AVAILABLE(NA, 10_0);
+
+/*!
+ @method waitForFence:
+ @abstract Prevent further GPU work until the event is reached.
+ @discussion The event is evaluated at kernel submision to maintain global order and prevent deadlock.
+ Drivers may delay fence updates until the end of the encoder. Drivers may also wait on fences at the beginning of an encoder. It is therefore illegal to both update and wait on the same fence in the same encoder.
+ */
+- (void)waitForFence:(id <MTLFence>)fence NS_AVAILABLE(NA, 10_0);
+
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputePipeline.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputePipeline.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputePipeline.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputePipeline.h	2016-05-16 08:17:34.000000000 +0200
@@ -75,4 +75,3 @@
 
 @end
 NS_ASSUME_NONNULL_END
-
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDefines.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDefines.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDefines.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDefines.h	2016-05-16 08:17:34.000000000 +0200
@@ -37,4 +37,3 @@
 #endif
 
 
-#define MTL_DEPRECATED __attribute__((deprecated))
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h	2016-05-16 07:34:12.000000000 +0200
@@ -24,6 +24,8 @@
 @protocol MTLSamplerState;
 @protocol MTLRenderPipelineState;
 @protocol MTLComputePipelineState;
+@protocol MTLFence;
+
 @class MTLSamplerDescriptor;
 @class MTLRenderPipelineColorAttachmentDescriptor;
 @class MTLDepthStencilDescriptor;
@@ -34,6 +36,10 @@
 @class MTLRenderPipelineReflection;
 @class MTLComputePipelineDescriptor;
 @class MTLComputePipelineReflection;
+@class MTLCommandQueueDescriptor;
+
+@protocol MTLHeap;
+@class MTLHeapDescriptor;
 
 /*!
  @brief Returns a reference to the preferred system default Metal device.
@@ -56,17 +62,29 @@
 {
     MTLFeatureSet_iOS_GPUFamily1_v1 NS_ENUM_AVAILABLE_IOS(8_0) __TVOS_UNAVAILABLE = 0,
     MTLFeatureSet_iOS_GPUFamily2_v1 NS_ENUM_AVAILABLE_IOS(8_0) __TVOS_UNAVAILABLE = 1,
-    
+
     MTLFeatureSet_iOS_GPUFamily1_v2 NS_ENUM_AVAILABLE_IOS(9_0) __TVOS_UNAVAILABLE = 2,
     MTLFeatureSet_iOS_GPUFamily2_v2 NS_ENUM_AVAILABLE_IOS(9_0) __TVOS_UNAVAILABLE = 3,
     MTLFeatureSet_iOS_GPUFamily3_v1 NS_ENUM_AVAILABLE_IOS(9_0) __TVOS_UNAVAILABLE = 4,
 
+    MTLFeatureSet_iOS_GPUFamily1_v3 NS_ENUM_AVAILABLE_IOS(10_0) __TVOS_UNAVAILABLE = 5,
+    MTLFeatureSet_iOS_GPUFamily2_v3 NS_ENUM_AVAILABLE_IOS(10_0) __TVOS_UNAVAILABLE = 6,
+    MTLFeatureSet_iOS_GPUFamily3_v2 NS_ENUM_AVAILABLE_IOS(10_0) __TVOS_UNAVAILABLE = 7,
+
     MTLFeatureSet_OSX_GPUFamily1_v1 NS_ENUM_AVAILABLE_MAC(10_11) = 10000,
 
-    
+    MTLFeatureSet_OSX_GPUFamily1_v2 NS_ENUM_AVAILABLE_MAC(10_12) = 10001,
+    MTLFeatureSet_OSX_ReadWriteTextureTier2 NS_ENUM_AVAILABLE_MAC(10_12) = 10002,
 
+
+    MTLFeatureSet_tvOS_GPUFamily1_v1 __TVOS_AVAILABLE(9.0) __IOS_UNAVAILABLE __OSX_UNAVAILABLE = 30000,
+
+    MTLFeatureSet_tvOS_GPUFamily1_v2 __TVOS_AVAILABLE(10.0) __IOS_UNAVAILABLE __OSX_UNAVAILABLE = 30001,
 } NS_ENUM_AVAILABLE(10_11, 8_0) __TVOS_AVAILABLE(9.0);
 
+
+#define MTLFeatureSet_TVOS_GPUFamily1_v1 MTLFeatureSet_tvOS_GPUFamily1_v1
+
 /*!
  @enum MTLPipelineOption
  @abstract Controls the creation of the pipeline
@@ -78,6 +96,14 @@
     MTLPipelineOptionBufferTypeInfo     = 1 << 1,
 } NS_ENUM_AVAILABLE(10_11, 8_0);
 
+/*!
+ @abstract Represent a memory size and alignment in bytes.
+ */
+typedef struct {
+    NSUInteger size;
+    NSUInteger align;
+} MTLSizeAndAlign;
+
 /* Convenience typedefs that make it easy to declare storage for certain return types. */
 typedef __autoreleasing MTLRenderPipelineReflection * __nullable MTLAutoreleasedRenderPipelineReflection;
 typedef __autoreleasing MTLComputePipelineReflection * __nullable MTLAutoreleasedComputePipelineReflection;
@@ -96,7 +122,6 @@
  */
 NS_AVAILABLE(10_11, 8_0)
 @protocol MTLDevice <NSObject>
-
 /*!
  @property name
  @abstract The full name of the vendor device.
@@ -142,6 +167,26 @@
 - (id <MTLCommandQueue>)newCommandQueueWithMaxCommandBufferCount:(NSUInteger)maxCommandBufferCount;
 
 /*!
+ @method heapTextureSizeAndAlignWithDescriptor:
+ @abstract Determine the byte size of textures when sub-allocated from a heap.
+ @discussion This method can be used to help determine the required heap size.
+ */
+- (MTLSizeAndAlign)heapTextureSizeAndAlignWithDescriptor:(MTLTextureDescriptor *)desc NS_AVAILABLE(NA, 10_0);
+
+/*!
+ @method heapBufferSizeAndAlignWithLength:options:
+ @abstract Determine the byte size of buffers when sub-allocated from a heap.
+ @discussion This method can be used to help determine the required heap size.
+ */
+- (MTLSizeAndAlign)heapBufferSizeAndAlignWithLength:(NSUInteger)length options:(MTLResourceOptions)options NS_AVAILABLE(NA, 10_0);
+
+/*!
+ @method newHeapWithDescriptor:
+ @abstract Create a new heap with the given descriptor.
+ */
+- (id <MTLHeap>)newHeapWithDescriptor:(MTLHeapDescriptor *)descriptor NS_AVAILABLE(NA, 10_0);
+
+/*!
  @method newBufferWithLength:options:
  @brief Create a buffer by allocating new memory.
  */
@@ -271,6 +316,12 @@
 - (void)newComputePipelineStateWithDescriptor:(MTLComputePipelineDescriptor *)descriptor options:(MTLPipelineOption)options completionHandler:(MTLNewComputePipelineStateWithReflectionCompletionHandler)completionHandler NS_AVAILABLE(10_11, 9_0);
 
 /*!
+ @method newFence
+ @abstract Create a new MTLFence object
+ */
+- (id <MTLFence>)newFence NS_AVAILABLE(NA, 10_0);
+
+/*!
  @method supportsFeatureSet:
  @abstract Returns TRUE if the feature set is supported by this MTLDevice.
  */
@@ -285,4 +336,3 @@
 
 @end
 NS_ASSUME_NONNULL_END
-
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDrawable.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDrawable.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDrawable.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDrawable.h	2016-05-16 08:17:34.000000000 +0200
@@ -9,6 +9,8 @@
 #import <Metal/MTLDefines.h>
 
 NS_ASSUME_NONNULL_BEGIN
+
+
 /*!
  @protocol MTLDrawable
  @abstract All "drawable" objects (such as those coming from CAMetalLayer) are expected to conform to this protocol
@@ -22,5 +24,6 @@
 /* Present this drawable at the given host time */
 - (void)presentAtTime:(CFTimeInterval)presentationTime;
 
+
 @end
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLFence.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLFence.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLFence.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLFence.h	2016-05-16 08:17:34.000000000 +0200
@@ -0,0 +1,22 @@
+//
+//  MTFence.h
+//  Metal
+//
+//  Copyright (c) 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <Metal/MTLDefines.h>
+#import <Metal/MTLDevice.h>
+
+NS_AVAILABLE(NA, 10_0)
+@protocol MTLFence <NSObject>
+@property (nonnull, readonly) id <MTLDevice> device;
+
+/*!
+ @property label
+ @abstract A string to help identify this object.
+ */
+@property (nullable, copy, atomic) NSString *label;
+
+@end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLFunctionConstantValues.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLFunctionConstantValues.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLFunctionConstantValues.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLFunctionConstantValues.h	2016-05-16 08:17:34.000000000 +0200
@@ -0,0 +1,30 @@
+//
+//  MTLFunctionConstantValues.h
+//  Metal
+//
+//  Copyright (c) 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <Metal/MTLDefines.h>
+#import <Metal/MTLArgument.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface MTLFunctionConstantValues : NSObject <NSCopying>
+
+// using indices
+- (void)setConstantValue:(const void *)value type:(MTLDataType)type atIndex:(NSUInteger)index;
+- (void)setConstantValues:(const void *)values type:(MTLDataType)type withRange:(NSRange)range;
+
+// using names
+- (void)setConstantValue:(const void *)value type:(MTLDataType)type withName:(NSString *)name;
+
+
+// delete all the constants
+- (void)reset;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLHeap.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLHeap.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLHeap.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLHeap.h	2016-05-16 08:17:34.000000000 +0200
@@ -0,0 +1,126 @@
+//
+//  MTLHeap.h
+//  Metal
+//
+//  Copyright (c) 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <Metal/MTLDefines.h>
+#import <Metal/MTLResource.h>
+#import <Metal/MTLBuffer.h>
+#import <Metal/MTLTexture.h>
+#import <Metal/MTLTypes.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+
+/*!
+ @class MTLHeapDescriptor
+ */
+NS_CLASS_AVAILABLE(NA, 10_0)
+@interface MTLHeapDescriptor : NSObject <NSCopying>
+
+/*!
+ @property size
+ @abstract Requested size of the heap's backing memory.
+ @discussion The size may be rounded up to GPU page granularity.
+ */
+@property (readwrite, nonatomic) NSUInteger size;
+
+/*!
+ @property storageMode
+ @abstract Storage mode for the heap. Default is MTLStorageModePrivate.
+ @discussion All resources created from this heap share the same storage mode.
+ MTLStorageModeManaged and MTLStorageModeMemoryless are disallowed.
+ */
+@property (readwrite, nonatomic) MTLStorageMode storageMode;
+
+/*!
+ @property cpuCacheMode
+ @abstract CPU cache mode for the heap. Default is MTLCPUCacheModeDefaultCache.
+ @discussion All resources created from this heap share the same cache mode.
+ CPU cache mode is ignored for MTLStorageModePrivate.
+ */
+@property (readwrite, nonatomic) MTLCPUCacheMode cpuCacheMode;
+
+@end
+
+/*!
+ @protocol MTLHeap
+ */
+NS_AVAILABLE(NA, 10_0)
+@protocol MTLHeap <NSObject>
+
+/*!
+ @property label
+ @abstract A string to help identify this heap.
+ */
+@property (nullable, copy, atomic) NSString *label;
+
+/*!
+ @property device
+ @abstract The device this heap was created against. This heap can only be used with this device.
+ */
+@property (readonly) id <MTLDevice> device;
+
+/*!
+ @property storageMode
+ @abstract Current heap storage mode, default is MTLStorageModePrivate.
+ @discussion All resources created from this heap share the same storage mode.
+ */
+@property (readonly) MTLStorageMode storageMode;
+
+/*!
+ @property cpuCacheMode
+ @abstract CPU cache mode for the heap. Default is MTLCPUCacheModeDefaultCache.
+ @discussion All resources created from this heap share the same cache mode.
+ */
+@property (readonly) MTLCPUCacheMode cpuCacheMode;
+
+/*!
+ @property totalSize
+ @abstract The total size of the heap specificed at creation, in bytes.
+ */
+@property (readonly) NSUInteger totalSize;
+
+/*!
+ @property currentSize
+ @abstract The size of all resources allocated from the heap, in bytes.
+ */
+@property (readonly) NSUInteger currentSize;
+
+/*!
+ @method maxAvailableSizeWithAlignment:
+ @abstract The maximum size that can be successfully allocated from the heap in bytes, taking into notice given alignment. Alignment needs to be zero, or power of two.
+ @discussion Provides a measure of fragmentation within the heap.
+ */
+- (NSUInteger)maxAvailableSizeWithAlignment:(NSUInteger)alignment;
+
+/*!
+ @method newBufferWithLength:options:
+ @abstract Create a new buffer backed by heap memory.
+ @discussion The requested storage and CPU cache modes must match the storage and CPU cache modes of the heap.
+ @return The buffer or nil if heap is full.
+ */
+- (id <MTLBuffer>)newBufferWithLength:(NSUInteger)length 
+                              options:(MTLResourceOptions)options;
+
+/*!
+ @method newTextureWithDescriptor:
+ @abstract Create a new texture backed by heap memory.
+ @discussion The requested storage and CPU cache modes must match the storage and CPU cache modes of the heap, with the exception that the requested storage mode can be MTLStorageModeMemoryless. 
+ @return The texture or nil if heap is full.
+ */
+- (id <MTLTexture>)newTextureWithDescriptor:(MTLTextureDescriptor *)desc;
+
+/*!
+ @method setPurgeabilityState:
+ @abstract Set or query the purgeability state of the heap.
+ */
+- (MTLPurgeableState)setPurgeableState:(MTLPurgeableState)state;
+
+@end
+
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h	2016-05-16 08:17:34.000000000 +0200
@@ -15,14 +15,25 @@
 @protocol MTLFunction;
 @protocol MTLLibrary;
 @class MTLCompileOptions;
+@class MTLFunctionConstantValues;
+
+typedef NS_ENUM(NSUInteger, MTLPatchType) {
+    MTLPatchTypeNone = 0,
+    MTLPatchTypeTriangle = 1,
+    MTLPatchTypeQuad = 2,
+} NS_ENUM_AVAILABLE(10_12, 10_0);
 
 NS_CLASS_AVAILABLE(10_11, 8_0)
 @interface MTLVertexAttribute : NSObject
- 
-@property (nullable, readonly) NSString *name;
+
+@property (nullable, readonly) NSString          *name;
 @property (readonly) NSUInteger                   attributeIndex;
 @property (readonly) MTLDataType                  attributeType NS_AVAILABLE(10_11, 8_3);
 @property (readonly, getter=isActive) BOOL        active;
+
+@property (readonly, getter=isPatchData) BOOL              patchData NS_AVAILABLE(10_12, 10_0);
+@property (readonly, getter=isPatchControlPointData) BOOL  patchControlPointData NS_AVAILABLE(10_12, 10_0);
+
 @end
 
 /*!
@@ -45,6 +56,21 @@
     MTLFunctionTypeKernel = 3,
 } NS_ENUM_AVAILABLE(10_11, 8_0);
 
+
+/*!
+ @interface MTLFunctionConstant
+ @abstract describe an uberShader constant used by the function
+ */
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface MTLFunctionConstant : NSObject
+
+@property (readonly) NSString *name;
+@property (readonly) MTLDataType type;
+@property (readonly) NSUInteger index;
+@property (readonly) BOOL required;
+
+@end
+
 /*!
  @protocol MTLFunction
  @abstract A handle to to intermediate code used as inputs for either a MTLComputePipelineState or a MTLRenderPipelineState.
@@ -54,6 +80,12 @@
 @protocol MTLFunction <NSObject>
 
 /*!
+ @property label
+ @abstract A string to help identify this object.
+ */
+@property (nullable, copy, atomic) NSString *label  NS_AVAILABLE(10_12, 10_0);
+
+/*!
  @property device
  @abstract The device this resource was created against.  This resource can only be used with this device.
  */
@@ -65,6 +97,19 @@
  */
 @property (readonly) MTLFunctionType functionType;
 
+/*!
+ @property patchType
+ @abstract Returns the patch type. MTLPatchTypeNone if it is not a post tessellation vertex shader.
+ */
+@property (readonly) MTLPatchType patchType NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property patchControlPointCount
+ @abstract Returns the number of patch control points if it was specified in the shader. Returns -1 if it
+ was not specified.
+ */
+@property (readonly) NSInteger patchControlPointCount NS_AVAILABLE(10_12, 10_0);
+
 @property (nullable, readonly) NSArray <MTLVertexAttribute *> *vertexAttributes;
 
 /*!
@@ -73,12 +118,26 @@
  */
 @property (readonly) NSString *name;
 
+
+/*!
+ @property functionConstants
+ @abstract Array containing the ubershader constants used by this function.
+ */
+@property (readonly) NSArray<MTLFunctionConstant *> *functionConstants NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @method functionConstantIndexByName:type:
+ @abstract Returns the index of an ubershader constant and its type
+ */
+- (NSUInteger)functionConstantIndexByName:(NSString *)name type:(MTLDataType *)type NS_AVAILABLE(10_12, 10_0);
+
 @end
 
 typedef NS_ENUM(NSUInteger, MTLLanguageVersion) {
 
     MTLLanguageVersion1_0 NS_ENUM_AVAILABLE(NA, 9_0) = (1 << 16),
-    MTLLanguageVersion1_1 = (1 << 16) + 1,
+    MTLLanguageVersion1_1 NS_ENUM_AVAILABLE(10_11, 9_0) = (1 << 16) + 1,
+    MTLLanguageVersion1_2 NS_ENUM_AVAILABLE(10_12, 10_0) = (1 << 16) + 2,
 } NS_ENUM_AVAILABLE(10_11, 9_0);
 
 
@@ -126,6 +185,7 @@
     MTLLibraryErrorInternal         = 2,
     MTLLibraryErrorCompileFailure   = 3,
     MTLLibraryErrorCompileWarning   = 4,
+    MTLLibraryErrorFunctionNotFound NS_AVAILABLE(10_12, 10_0) = 5,
 } NS_ENUM_AVAILABLE(10_11, 8_0);
 
 MTL_EXTERN NSString *const MTLRenderPipelineErrorDomain;
@@ -163,6 +223,23 @@
 - (nullable id <MTLFunction>) newFunctionWithName:(NSString *)functionName;
 
 /*!
+ @method newFunctionWithName:constantValues:error:
+ @abstract Returns a pointer to a function object obtained by applying the constant values to the named function.
+ @discussion This method will call the compiler. Use newFunctionWithName:constantValues:completionHandler: to
+ avoid waiting on the compiler.
+ */
+- (nullable id <MTLFunction>) newFunctionWithName:(NSString *)name constantValues:(MTLFunctionConstantValues *)constantValues
+					error:(__autoreleasing NSError **)error;
+
+/*!
+ @method newFunctionWithName:constantValues:completionHandler:
+ @abstract Returns a pointer to a function object obtained by applying the constant values to the named function.
+ @discussion This method is asynchronous since it is will call the compiler.
+ */
+- (void) newFunctionWithName:(NSString *)name constantValues:(MTLFunctionConstantValues *)constantValues
+			completionHandler:(void (^)(id<MTLFunction> __nullable function, NSError* error))completionHandler;
+
+/*!
  @property functionNames
  @abstract The array contains NSString objects, with the name of each function in library.
  */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLParallelRenderCommandEncoder.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLParallelRenderCommandEncoder.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLParallelRenderCommandEncoder.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLParallelRenderCommandEncoder.h	2016-05-16 08:17:34.000000000 +0200
@@ -26,5 +26,28 @@
  */
 - (id <MTLRenderCommandEncoder>)renderCommandEncoder;
 
+/*!
+ @method setColorStoreAction:atIndex:
+ @brief If the the store action for a given color attachment was set to MTLStoreActionUnknown when the render command encoder was created,
+ setColorStoreAction:atIndex: must be used to finalize the store action before endEncoding is called.
+ @param storeAction The desired store action for the given color attachment.  This may be set to any value other than MTLStoreActionUnknown.
+ @param colorAttachmentIndex The index of the color attachment
+*/
+- (void)setColorStoreAction:(MTLStoreAction)storeAction atIndex:(NSUInteger)colorAttachmentIndex NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @method setDepthStoreAction:
+ @brief If the the store action for the depth attachment was set to MTLStoreActionUnknown when the render command encoder was created,
+ setDepthStoreAction: must be used to finalize the store action before endEncoding is called.
+*/
+- (void)setDepthStoreAction:(MTLStoreAction)storeAction NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @method setStencilStoreAction:
+ @brief If the the store action for the stencil attachment was set to MTLStoreActionUnknown when the render command encoder was created,
+ setStencilStoreAction: must be used to finalize the store action before endEncoding is called.
+*/
+- (void)setStencilStoreAction:(MTLStoreAction)storeAction NS_AVAILABLE(10_12, 10_0);
+
 @end
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLPixelFormat.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLPixelFormat.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLPixelFormat.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLPixelFormat.h	2016-05-16 08:17:34.000000000 +0200
@@ -74,6 +74,9 @@
     MTLPixelFormatRG11B10Float = 92,
     MTLPixelFormatRGB9E5Float = 93,
 
+    MTLPixelFormatBGR10_XR      NS_AVAILABLE_IOS(10_0) = 554,
+    MTLPixelFormatBGR10_XR_sRGB NS_AVAILABLE_IOS(10_0) = 555,
+
     /* Normal 64 bit formats */
 
     MTLPixelFormatRG32Uint  = 103,
@@ -86,6 +89,9 @@
     MTLPixelFormatRGBA16Sint   = 114,
     MTLPixelFormatRGBA16Float  = 115,
 
+    MTLPixelFormatBGRA10_XR      NS_AVAILABLE_IOS(10_0) = 552,
+    MTLPixelFormatBGRA10_XR_sRGB NS_AVAILABLE_IOS(10_0) = 553,
+
     /* Normal 128 bit formats */
 
     MTLPixelFormatRGBA32Uint  = 123,
@@ -195,5 +201,9 @@
     MTLPixelFormatDepth24Unorm_Stencil8  NS_AVAILABLE_MAC(10_11) = 255,
     MTLPixelFormatDepth32Float_Stencil8  NS_AVAILABLE(10_11, 9_0) = 260,
 
+    MTLPixelFormatX32_Stencil8  NS_AVAILABLE(10_12, 10_0) = 261,
+    MTLPixelFormatX24_Stencil8  NS_AVAILABLE_MAC(10_12) = 262,
+
 } NS_ENUM_AVAILABLE(10_11, 8_0);
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderCommandEncoder.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderCommandEncoder.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderCommandEncoder.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderCommandEncoder.h	2016-05-18 03:41:30.000000000 +0200
@@ -9,6 +9,8 @@
 #import <Metal/MTLDefines.h>
 #import <Metal/MTLCommandEncoder.h>
 #import <Metal/MTLCommandBuffer.h>
+#import <Metal/MTLRenderPass.h>
+#import <Metal/MTLFence.h>
 
 NS_ASSUME_NONNULL_BEGIN
 @protocol MTLDevice;
@@ -83,6 +85,37 @@
     uint32_t baseInstance;
 } MTLDrawIndexedPrimitivesIndirectArguments;
 
+typedef struct {
+    uint32_t patchCount;
+    uint32_t instanceCount;
+    uint32_t patchStart;
+    uint32_t baseInstance;
+} MTLDrawPatchIndirectArguments;
+
+typedef struct {
+    /* NOTE: edgeTessellationFactor and insideTessellationFactor are interpreted as half (16-bit floats) */
+    uint16_t edgeTessellationFactor[4];
+    uint16_t insideTessellationFactor[2];
+} MTLQuadTessellationFactorsHalf;
+
+typedef struct {
+    /* NOTE: edgeTessellationFactor and insideTessellationFactor are interpreted as half (16-bit floats) */
+    uint16_t edgeTessellationFactor[3];
+    uint16_t insideTessellationFactor;
+} MTLTriangleTessellationFactorsHalf;
+
+/*!
+ @abstract Points at which a fence may be waited on or signaled.
+ @constant MTLRenderStageVertex   All vertex work prior to rasterization has completed.
+ @constant MTLRenderStageFragment All rendering work has completed.
+ */
+typedef NS_OPTIONS(NSUInteger, MTLRenderStages)
+{
+    MTLRenderStageVertex   = (1UL << 0),
+    MTLRenderStageFragment = (1UL << 1),
+} NS_ENUM_AVAILABLE_IOS(10_0);
+
+
 /*!
  @protocol MTLRenderCommandEncoder
  @discussion MTLRenderCommandEncoder is a container for graphics rendering state and the code to translate the state into a command format that the device can execute. 
@@ -158,8 +191,6 @@
  */
 - (void)setVertexSamplerStates:(const id <MTLSamplerState> __nullable [__nullable])samplers lodMinClamps:(const float [__nullable])lodMinClamps lodMaxClamps:(const float [__nullable])lodMaxClamps withRange:(NSRange)range;
 
-/* Vertex Shaders */
-
 /*!
  @method setViewport:
  @brief Set the viewport, which is used to transform vertexes from normalized device coordinates to window coordinates.  Fragments that lie outside of the viewport are clipped, and optionally clamped for fragments outside of znear/zfar.
@@ -283,8 +314,7 @@
  */
 - (void)setStencilReferenceValue:(uint32_t)referenceValue;
 
-
-/*! 
+/*!
  @method setStencilFrontReferenceValue:backReferenceValue:
  @brief Set the stencil reference value for the back and front stencil buffers independently.
  */
@@ -298,6 +328,29 @@
  */
 - (void)setVisibilityResultMode:(MTLVisibilityResultMode)mode offset:(NSUInteger)offset;
 
+/*!
+ @method setColorStoreAction:atIndex:
+ @brief If the the store action for a given color attachment was set to MTLStoreActionUnknown when the render command encoder was created,
+ setColorStoreAction:atIndex: must be used to finalize the store action before endEncoding is called.
+ @param storeAction The desired store action for the given color attachment.  This may be set to any value other than MTLStoreActionUnknown.
+ @param colorAttachmentIndex The index of the color attachment
+*/
+- (void)setColorStoreAction:(MTLStoreAction)storeAction atIndex:(NSUInteger)colorAttachmentIndex NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @method setDepthStoreAction:
+ @brief If the the store action for the depth attachment was set to MTLStoreActionUnknown when the render command encoder was created,
+ setDepthStoreAction: must be used to finalize the store action before endEncoding is called.
+*/
+- (void)setDepthStoreAction:(MTLStoreAction)storeAction NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @method setStencilStoreAction:
+ @brief If the the store action for the stencil attachment was set to MTLStoreActionUnknown when the render command encoder was created,
+ setStencilStoreAction: must be used to finalize the store action before endEncoding is called.
+*/
+- (void)setStencilStoreAction:(MTLStoreAction)storeAction NS_AVAILABLE(10_12, 10_0);
+
 /* Drawing */
 
 /*!
@@ -311,7 +364,7 @@
 - (void)drawPrimitives:(MTLPrimitiveType)primitiveType vertexStart:(NSUInteger)vertexStart vertexCount:(NSUInteger)vertexCount instanceCount:(NSUInteger)instanceCount;
 
 /*!
- @method drawPrimitives:vertexStart:vertexCount:instanceCount:
+ @method drawPrimitives:vertexStart:vertexCount:
  @brief Draw primitives without an index list.
  @param primitiveType The type of primitives that elements are assembled into.
  @param vertexStart For each instance, the first index to draw
@@ -332,7 +385,7 @@
 - (void)drawIndexedPrimitives:(MTLPrimitiveType)primitiveType indexCount:(NSUInteger)indexCount indexType:(MTLIndexType)indexType indexBuffer:(id <MTLBuffer>)indexBuffer indexBufferOffset:(NSUInteger)indexBufferOffset instanceCount:(NSUInteger)instanceCount;
 
 /*!
- @method drawIndexedPrimitives:indexCount:indexType:indexBuffer:indexBufferOffset:instanceCount:
+ @method drawIndexedPrimitives:indexCount:indexType:indexBuffer:indexBufferOffset:
  @brief Draw primitives with an index list.
  @param primitiveType The type of primitives that elements are assembled into.
  @param indexCount The number of indexes to read from the index buffer for each instance.
@@ -343,7 +396,7 @@
 - (void)drawIndexedPrimitives:(MTLPrimitiveType)primitiveType indexCount:(NSUInteger)indexCount indexType:(MTLIndexType)indexType indexBuffer:(id <MTLBuffer>)indexBuffer indexBufferOffset:(NSUInteger)indexBufferOffset;
 
 /*!
- @method drawPrimitives:vertexStart:vertexCount:instanceCount:
+ @method drawPrimitives:vertexStart:vertexCount:instanceCount:baseInstance:
  @brief Draw primitives without an index list.
  @param primitiveType The type of primitives that elements are assembled into.
  @param vertexStart For each instance, the first index to draw
@@ -354,7 +407,7 @@
 - (void)drawPrimitives:(MTLPrimitiveType)primitiveType vertexStart:(NSUInteger)vertexStart vertexCount:(NSUInteger)vertexCount instanceCount:(NSUInteger)instanceCount baseInstance:(NSUInteger)baseInstance NS_AVAILABLE(10_11, 9_0);
 
 /*!
- @method drawIndexedPrimitives:indexCount:indexType:indexBuffer:indexBufferOffset:instanceCount:
+ @method drawIndexedPrimitives:indexCount:indexType:indexBuffer:indexBufferOffset:instanceCount:baseVertex:baseInstance:
  @brief Draw primitives with an index list.
  @param primitiveType The type of primitives that elements are assembled into.
  @param indexCount The number of indexes to read from the index buffer for each instance.
@@ -389,5 +442,35 @@
 - (void)drawIndexedPrimitives:(MTLPrimitiveType)primitiveType indexType:(MTLIndexType)indexType indexBuffer:(id <MTLBuffer>)indexBuffer indexBufferOffset:(NSUInteger)indexBufferOffset indirectBuffer:(id <MTLBuffer>)indirectBuffer indirectBufferOffset:(NSUInteger)indirectBufferOffset NS_AVAILABLE(10_11, 9_0);
 
 
+@optional
+/*!
+ @method updateFence:afterStages:
+ @abstract Update the event to capture all GPU work so far enqueued by this encoder for the given stages.
+ @discussion Unlike <st>updateFence:</st>, this method will update the event when the given stage(s) complete, allowing for commands to overlap in execution.
+ On iOS, render command encoder fence updates are always delayed until the end of the encoder.
+ */
+- (void)updateFence:(id <MTLFence>)fence afterStages:(MTLRenderStages)stages NS_AVAILABLE_IOS(10_0);
+
+/*!
+ @method waitForFence:beforeStages:
+ @abstract Prevent further GPU work until the event is reached for the given stages.
+ @discussion Unlike <st>waitForFence:</st>, this method will only block commands assoicated with the given stage(s), allowing for commands to overlap in execution.
+ On iOS, render command encoder fence waits always occur the beginning of the encoder.
+ */
+- (void)waitForFence:(id <MTLFence>)fence beforeStages:(MTLRenderStages)stages NS_AVAILABLE_IOS(10_0);
+@required
+
+-(void)setTessellationFactorBuffer:(nullable id <MTLBuffer>)buffer offset:(NSUInteger)offset instanceStride:(NSUInteger)instanceStride NS_AVAILABLE(10_12, 10_0);
+
+-(void)setTessellationFactorScale:(float)scale NS_AVAILABLE(10_12, 10_0);
+
+-(void)drawPatches:(NSUInteger)numberOfPatchControlPoints patchStart:(NSUInteger)patchStart patchCount:(NSUInteger)patchCount patchIndexBuffer:(nullable id <MTLBuffer>)patchIndexBuffer patchIndexBufferOffset:(NSUInteger)patchIndexBufferOffset instanceCount:(NSUInteger)instanceCount baseInstance:(NSUInteger)baseInstance NS_AVAILABLE(10_12, 10_0);
+
+-(void)drawPatches:(NSUInteger)numberOfPatchControlPoints patchIndexBuffer:(nullable id <MTLBuffer>)patchIndexBuffer patchIndexBufferOffset:(NSUInteger)patchIndexBufferOffset indirectBuffer:(id <MTLBuffer>)indirectBuffer indirectBufferOffset:(NSUInteger)indirectBufferOffset NS_AVAILABLE(10_12, 10_0);
+
+-(void)drawIndexedPatches:(NSUInteger)numberOfPatchControlPoints patchStart:(NSUInteger)patchStart patchCount:(NSUInteger)patchCount patchIndexBuffer:(nullable id <MTLBuffer>)patchIndexBuffer patchIndexBufferOffset:(NSUInteger)patchIndexBufferOffset controlPointIndexBuffer:(id <MTLBuffer>)controlPointIndexBuffer controlPointIndexBufferOffset:(NSUInteger)controlPointIndexBufferOffset instanceCount:(NSUInteger)instanceCount baseInstance:(NSUInteger)baseInstance NS_AVAILABLE(10_12, 10_0);
+
+-(void)drawIndexedPatches:(NSUInteger)numberOfPatchControlPoints patchIndexBuffer:(nullable id <MTLBuffer>)patchIndexBuffer patchIndexBufferOffset:(NSUInteger)patchIndexBufferOffset controlPointIndexBuffer:(id <MTLBuffer>)controlPointIndexBuffer controlPointIndexBufferOffset:(NSUInteger)controlPointIndexBufferOffset indirectBuffer:(id <MTLBuffer>)indirectBuffer indirectBufferOffset:(NSUInteger)indirectBufferOffset NS_AVAILABLE(10_12, 10_0);
+
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderPass.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderPass.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderPass.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderPass.h	2016-05-16 08:17:34.000000000 +0200
@@ -21,6 +21,8 @@
     MTLStoreActionDontCare = 0,
     MTLStoreActionStore = 1,
     MTLStoreActionMultisampleResolve = 2,
+    MTLStoreActionStoreAndMultisampleResolve NS_ENUM_AVAILABLE(10_12,10_0) = 3,
+    MTLStoreActionUnknown NS_ENUM_AVAILABLE(10_12,10_0) = 4,
 } NS_ENUM_AVAILABLE(10_11, 8_0);
 
 typedef struct
@@ -190,6 +192,11 @@
  */
 @property (nullable, nonatomic, strong) id <MTLBuffer> visibilityResultBuffer;
 
+/*!
+ @property renderTargetArrayLength:
+ @abstract The number of active layers
+ */
+@property (nonatomic) NSUInteger renderTargetArrayLength NS_AVAILABLE_MAC(10_11);
 
 @end
 
@@ -203,4 +210,5 @@
     result.alpha = alpha;
     return result;
 }
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderPipeline.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderPipeline.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderPipeline.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderPipeline.h	2016-05-16 07:34:13.000000000 +0200
@@ -7,9 +7,11 @@
 
 #import <Metal/MTLDefines.h>
 #import <Metal/MTLDevice.h>
+#import <Metal/MTLRenderCommandEncoder.h>
 #import <Metal/MTLRenderPass.h>
 #import <Metal/MTLPixelFormat.h>
 #import <Metal/MTLArgument.h>
+#import <Metal/MTLFunctionConstantValues.h>
 
 NS_ASSUME_NONNULL_BEGIN
 @class MTLVertexDescriptor;
@@ -49,6 +51,36 @@
     MTLColorWriteMaskAll   = 0xf
 } NS_ENUM_AVAILABLE(10_11, 8_0);
 
+typedef NS_ENUM(NSUInteger, MTLPrimitiveTopologyClass) {
+    MTLPrimitiveTopologyClassUnspecified = 0,
+    MTLPrimitiveTopologyClassPoint = 1,
+    MTLPrimitiveTopologyClassLine = 2,
+    MTLPrimitiveTopologyClassTriangle = 3,
+} NS_ENUM_AVAILABLE_MAC(10_11);
+
+typedef NS_ENUM(NSUInteger, MTLTessellationPartitionMode) {
+    MTLTessellationPartitionModePow2 = 0,
+    MTLTessellationPartitionModeInteger = 1,
+    MTLTessellationPartitionModeFractionalOdd = 2,
+    MTLTessellationPartitionModeFractionalEven = 3,
+} NS_ENUM_AVAILABLE(10_12, 10_0);
+
+typedef NS_ENUM(NSUInteger, MTLTessellationFactorStepFunction) {
+    MTLTessellationFactorStepFunctionConstant = 0,
+    MTLTessellationFactorStepFunctionPerPatch = 1,
+    MTLTessellationFactorStepFunctionPerInstance = 2,
+    MTLTessellationFactorStepFunctionPerPatchAndPerInstance = 3,
+} NS_ENUM_AVAILABLE(10_12, 10_0);
+
+typedef NS_ENUM(NSUInteger, MTLTessellationFactorFormat) {
+    MTLTessellationFactorFormatHalf = 0,
+} NS_ENUM_AVAILABLE(10_12, 10_0);
+
+typedef NS_ENUM(NSUInteger, MTLTessellationControlPointIndexType) {
+    MTLTessellationControlPointIndexTypeNone = 0,
+    MTLTessellationControlPointIndexTypeUInt16 = 1,
+    MTLTessellationControlPointIndexTypeUInt32 = 2,
+} NS_ENUM_AVAILABLE(10_12, 10_0);
 
 @class MTLRenderPipelineColorAttachmentDescriptorArray;
 
@@ -116,6 +148,15 @@
 @property (nonatomic) MTLPixelFormat depthAttachmentPixelFormat;
 @property (nonatomic) MTLPixelFormat stencilAttachmentPixelFormat;
 
+@property (readwrite, nonatomic) MTLPrimitiveTopologyClass inputPrimitiveTopology NS_AVAILABLE_MAC(10_11);
+
+@property (readwrite, nonatomic) MTLTessellationPartitionMode tessellationPartitionMode NS_AVAILABLE(10_12, 10_0);
+@property (readwrite, nonatomic) NSUInteger maxTessellationFactor NS_AVAILABLE(10_12, 10_0);
+@property (readwrite, nonatomic, getter = isTessellationFactorScaleEnabled) BOOL tessellationFactorScaleEnabled NS_AVAILABLE(10_12, 10_0);
+@property (readwrite, nonatomic) MTLTessellationFactorFormat tessellationFactorFormat NS_AVAILABLE(10_12, 10_0);
+@property (readwrite, nonatomic) MTLTessellationControlPointIndexType tessellationControlPointIndexType NS_AVAILABLE(10_12, 10_0);
+@property (readwrite, nonatomic) MTLTessellationFactorStepFunction tessellationFactorStepFunction NS_AVAILABLE(10_12, 10_0);
+@property (readwrite, nonatomic) MTLWinding tessellationOutputWindingOrder NS_AVAILABLE(10_12, 10_0);
 
 /*!
  @method reset
@@ -149,4 +190,6 @@
 - (void)setObject:(nullable MTLRenderPipelineColorAttachmentDescriptor *)attachment atIndexedSubscript:(NSUInteger)attachmentIndex;
 
 @end
+
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLResource.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLResource.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLResource.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLResource.h	2016-05-16 08:17:34.000000000 +0200
@@ -16,7 +16,7 @@
  @constant MTLPurgeableStateNonVolatile
  The contents of this resource may not be discarded.
 
- @constant MTLPurgeableStateNoVolatile
+ @constant MTLPurgeableStateVolatile
  The contents of this resource may be discarded.
 
  @constant MTLPurgeableStateEmpty
@@ -36,7 +36,7 @@
 
 /*!
  @enum MTLCPUCacheMode
- @abstract Describes what CPU cache mode is used for the CPU's mapping of a resource.
+ @abstract Describes what CPU cache mode is used for the CPU's mapping of a texture resource.
  @constant MTLCPUCacheModeDefaultCache
  The default cache mode for the system.
  
@@ -54,29 +54,35 @@
 
 /*!
  @enum MTLStorageMode
- @abstract Describes location and CPU mapping of MTLResource (MTLTexture or MTLBuffer).
+ @abstract Describes location and CPU mapping of MTLTexture.
  @constant MTLStorageModeShared
- In this mode, CPU and device will nominally both use the same underlying memory when accessing the contents of the resource.
+ In this mode, CPU and device will nominally both use the same underlying memory when accessing the contents of the texture resource.
  However, coherency is only guaranteed at command buffer boundaries to minimize the required flushing of CPU and GPU caches.
  This is the default storage mode for iOS Textures.
 
  @constant MTLStorageModeManaged
  This mode relaxes the coherency requirements and requires that the developer make explicit requests to maintain
- coherency between a CPU and GPU version of the resource.  Changes due to CPU stores outside of the Metal API must be
- indicated to Metal via MTLBuffer::didModifyRange:(NSRange)range.  In order for CPU to access up to date GPU results,
+ coherency between a CPU and GPU version of the texture resource.  In order for CPU to access up to date GPU results,
  first, a blit synchronizations must be completed (see synchronize methods of MTLBlitCommandEncoder).
  Blit overhead is only incurred if GPU has modified the resource.
  This is the default storage mode for OS X Textures.
 
  @constant MTLStorageModePrivate
- This mode allows the data to be kept entirely to GPU (or driver) private memory that will never be accessed by the CPU directly, so no
+ This mode allows the texture resource data to be kept entirely to GPU (or driver) private memory that will never be accessed by the CPU directly, so no
  conherency of any kind must be maintained.
+ 
+ @constant MTLStorageModeMemoryless
+ This mode allows creation of resources that do not have a GPU or CPU memory backing, but do have on-chip storage for TBDR
+ devices. The contents of the on-chip storage is undefined and does not persist, but its configuration is controlled by the
+ MTLTexture descriptor. Textures created with MTLStorageModeMemoryless dont have an IOAccelResource at any point in their
+ lifetime. The only way to populate such resource is to perform rendering operations on it. Blit operations are disallowed.
 */
 typedef NS_ENUM(NSUInteger, MTLStorageMode)
 {
     MTLStorageModeShared  = 0,
     MTLStorageModeManaged NS_ENUM_AVAILABLE(10_11, NA) = 1,
     MTLStorageModePrivate = 2,
+    MTLStorageModeMemoryless NS_ENUM_AVAILABLE(NA, 10_0) = 3,
 } NS_ENUM_AVAILABLE(10_11, 9_0);
 
 /*!
@@ -96,6 +102,7 @@
  @constant MTLResourceStorageModeShared
  In this mode, CPU and device will nominally both use the same underlying memory when accessing the contents of the resource.
  However, coherency is only guaranteed at command buffer boundaries to minimize the required flushing of CPU and GPU caches.
+ This is the default storage mode for iOS Textures.
 
  @constant MTLResourceStorageModeManaged
  This mode relaxes the coherency requirements and requires that the developer make explicit requests to maintain
@@ -104,11 +111,18 @@
  first, a blit synchronizations must be completed (see synchronize methods of MTLBlitCommandEncoder).
  Blit overhead is only incurred if GPU has modified the resource.
  This storage mode is only defined for OS X.
+ This is the default storage mode for OS X Textures.
 
  @constant MTLResourceStorageModePrivate
  This mode allows the data to be kept entirely to GPU (or driver) private memory that will never be accessed by the CPU directly, so no
  conherency of any kind must be maintained.
 
+ @constant MTLResourceStorageModeMemoryless
+ This mode allows creation of resources that do not have a GPU or CPU memory backing, but do have on-chip storage for TBDR
+ devices. The contents of the on-chip storage is undefined and does not persist, but its configuration is controlled by the
+ MTLTexture descriptor. Textures created with MTLStorageModeMemoryless dont have an IOAccelResource at any point in their
+ lifetime. The only way to populate such resource is to perform rendering operations on it. Blit operations are disallowed.
+
  @discussion
  Note that resource options are a property of MTLTextureDescriptor (resourceOptions), so apply to texture creation.
  they are also passed directly into MTLBuffer creation methods.
@@ -119,14 +133,20 @@
 #define MTLResourceStorageModeShift  4
 #define MTLResourceStorageModeMask   (0xfUL << MTLResourceStorageModeShift)
 
+#define MTLResourceHazardTrackingModeShift  8
+#define MTLResourceHazardTrackingModeMask   (0x1UL << MTLResourceHazardTrackingModeShift)
+
 typedef NS_OPTIONS(NSUInteger, MTLResourceOptions)
 {
     MTLResourceCPUCacheModeDefaultCache  = MTLCPUCacheModeDefaultCache  << MTLResourceCPUCacheModeShift,
     MTLResourceCPUCacheModeWriteCombined = MTLCPUCacheModeWriteCombined << MTLResourceCPUCacheModeShift,
 
-    MTLResourceStorageModeShared  NS_ENUM_AVAILABLE(10_11, 9_0) = MTLStorageModeShared  << MTLResourceStorageModeShift,
-    MTLResourceStorageModeManaged NS_ENUM_AVAILABLE(10_11, NA)  = MTLStorageModeManaged << MTLResourceStorageModeShift,
-    MTLResourceStorageModePrivate NS_ENUM_AVAILABLE(10_11, 9_0) = MTLStorageModePrivate << MTLResourceStorageModeShift,
+    MTLResourceStorageModeShared     NS_ENUM_AVAILABLE(10_11, 9_0)  = MTLStorageModeShared     << MTLResourceStorageModeShift,
+    MTLResourceStorageModeManaged    NS_ENUM_AVAILABLE(10_11, NA)   = MTLStorageModeManaged    << MTLResourceStorageModeShift,
+    MTLResourceStorageModePrivate    NS_ENUM_AVAILABLE(10_11, 9_0)  = MTLStorageModePrivate    << MTLResourceStorageModeShift,
+    MTLResourceStorageModeMemoryless NS_ENUM_AVAILABLE(NA,    10_0) = MTLStorageModeMemoryless << MTLResourceStorageModeShift,
+
+    MTLResourceHazardTrackingModeUntracked NS_ENUM_AVAILABLE(NA, 10_0) = 0x1UL << MTLResourceHazardTrackingModeShift,
 
     // Deprecated spellings
     MTLResourceOptionCPUCacheModeDefault       = MTLResourceCPUCacheModeDefaultCache,
@@ -135,6 +155,8 @@
 
 @protocol MTLDevice;
 
+@protocol MTLHeap;
+
 /*!
  @protocol MTLResource
  @abstract Common APIs available for MTLBuffer and MTLTexture instances
@@ -165,7 +187,7 @@
  @abstract The resource storage mode used for the CPU mapping for this resource
  */
 @property (readonly) MTLStorageMode storageMode NS_AVAILABLE(10_11, 9_0);
- 
+
 /*!
  @method setPurgeableState
  @abstract Set (or query) the purgeability state of a resource
@@ -173,6 +195,31 @@
  FIXME: If the device is keeping a cached copy of the resource, both the shared copy and cached copy are made purgeable.  Any access to the resource by either the CPU or device will be undefined.
  */
 - (MTLPurgeableState)setPurgeableState:(MTLPurgeableState)state;
- 
+
+/*!
+ @property heap
+ @abstract The heap from which this resouce was created.
+ @discussion Nil when this resource is not backed by a heap.
+ */
+@property (readonly, nullable) id <MTLHeap> heap NS_AVAILABLE(NA, 10_0);
+
+/*!
+ @method makeAliasable
+ @abstract Allow future heap sub-allocations to alias against this resource's memory.
+ @discussion It is illegal to call this method on a non heap-based resource. The debug layer will raise an exception.
+ One a resource is made aliasable, the decision cannot be reverted.
+ */
+-(void) makeAliasable NS_AVAILABLE(NA, 10_0);
+
+/*!
+ @method isAliasable
+ @abstract Returns whether future heap sub-allocations may alias against this resource's memory.
+ @return YES if <st>makeAliasable</st> was previously called on this resource. NO otherwise.
+ Also returns NO when storage mode is memoryless.
+ */
+-(BOOL) isAliasable NS_AVAILABLE(NA, 10_0);
+
 @end
+
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLSampler.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLSampler.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLSampler.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLSampler.h	2016-05-18 03:41:30.000000000 +0200
@@ -181,4 +181,4 @@
 @property (readonly) id <MTLDevice> device;
 
 @end
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLTexture.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLTexture.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLTexture.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLTexture.h	2016-05-18 03:41:30.000000000 +0200
@@ -151,8 +151,7 @@
  @property rootResource
  @abstract The resource this texture was created from. It may be a texture or a buffer. If this texture is not reusing storage of another MTLResource, then nil is returned.
  */
-@property (nullable, readonly) id <MTLResource> rootResource;
-
+@property (nullable, readonly) id <MTLResource> rootResource NS_DEPRECATED(10_11, 10_12, 8_0, 10_0);
 
 /*!
  @property parentTexture
@@ -176,20 +175,19 @@
  @property buffer
  @abstract The buffer this texture view was created from, or nil if this is not a texture view or it was not created from a buffer.
  */
-@property (nullable, readonly) id <MTLBuffer> buffer NS_AVAILABLE_IOS(9_0);
+@property (nullable, readonly) id <MTLBuffer> buffer NS_AVAILABLE(10_12, 9_0);
 
 /*!
  @property bufferOffset
  @abstract The offset of the buffer this texture view was created from, or 0 if this is not a texture view.
  */
-@property (readonly) NSUInteger bufferOffset NS_AVAILABLE_IOS(9_0);
+@property (readonly) NSUInteger bufferOffset NS_AVAILABLE(10_12, 9_0);
 
 /*!
  @property bufferBytesPerRow
  @abstract The bytesPerRow of the buffer this texture view was created from, or 0 if this is not a texture view.
  */
-@property (readonly) NSUInteger bufferBytesPerRow NS_AVAILABLE_IOS(9_0);
-
+@property (readonly) NSUInteger bufferBytesPerRow NS_AVAILABLE(10_12, 9_0);
 
 
 /*!
@@ -291,8 +289,7 @@
  @method newTextureViewWithPixelFormat:textureType:levels:slices:
  @abstract Create a new texture which shares the same storage as the source texture, but with a different (but compatible) pixel format, texture type, levels and slices.
  */
-- (id<MTLTexture>)newTextureViewWithPixelFormat:(MTLPixelFormat)pixelFormat textureType:(MTLTextureType)textureType levels:(NSRange)levelRange slices:(NSRange)sliceRange;
-
+- (id<MTLTexture>)newTextureViewWithPixelFormat:(MTLPixelFormat)pixelFormat textureType:(MTLTextureType)textureType levels:(NSRange)levelRange slices:(NSRange)sliceRange NS_AVAILABLE(10_11, 9_0);
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLVertexDescriptor.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLVertexDescriptor.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLVertexDescriptor.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLVertexDescriptor.h	2016-05-16 08:17:34.000000000 +0200
@@ -69,6 +69,8 @@
     
     MTLVertexFormatInt1010102Normalized = 40,
     MTLVertexFormatUInt1010102Normalized = 41,
+    
+    
 } NS_ENUM_AVAILABLE(10_11, 8_0);
 
 typedef NS_ENUM(NSUInteger, MTLVertexStepFunction)
@@ -76,6 +78,8 @@
     MTLVertexStepFunctionConstant = 0,
     MTLVertexStepFunctionPerVertex = 1,
     MTLVertexStepFunctionPerInstance = 2,
+    MTLVertexStepFunctionPerPatch NS_ENUM_AVAILABLE(10_12, 10_0) = 3,
+    MTLVertexStepFunctionPerPatchControlPoint NS_ENUM_AVAILABLE(10_12, 10_0) = 4,
 } NS_ENUM_AVAILABLE(10_11, 8_0);
 
 NS_CLASS_AVAILABLE(10_11, 8_0)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/Metal.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/Metal.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/Metal.h	2015-10-02 23:43:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Metal.framework/Headers/Metal.h	2016-05-16 08:17:34.000000000 +0200
@@ -24,3 +24,4 @@
 #import <Metal/MTLRenderCommandEncoder.h>
 #import <Metal/MTLSampler.h>
 #import <Metal/MTLTexture.h>
+#import <Metal/MTLHeap.h>

```