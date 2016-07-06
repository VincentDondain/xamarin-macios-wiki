#Metal.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLArgument.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLArgument.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLArgument.h	2015-08-23 01:47:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLArgument.h	2016-05-21 06:45:26.000000000 +0200
@@ -185,8 +185,7 @@
 @property (readonly) MTLTextureType textureType; // texture1D, texture2D...
 @property (readonly) MTLDataType    textureDataType; // half, float, int, or uint.
 
+@property (readonly) BOOL           isDepthTexture NS_AVAILABLE(10_12, 10_0); // true for depth textures
+
 @end
 NS_ASSUME_NONNULL_END
-
-
-
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLBlitCommandEncoder.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLBlitCommandEncoder.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLBlitCommandEncoder.h	2015-08-23 01:47:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLBlitCommandEncoder.h	2016-05-21 06:45:26.000000000 +0200
@@ -105,5 +105,6 @@
  */
 - (void)copyFromBuffer:(id <MTLBuffer>)sourceBuffer sourceOffset:(NSUInteger)sourceOffset toBuffer:(id <MTLBuffer>)destinationBuffer destinationOffset:(NSUInteger)destinationOffset size:(NSUInteger)size;
 
+
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLBuffer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLBuffer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLBuffer.h	2015-08-23 01:47:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLBuffer.h	2016-05-21 06:45:27.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLCommandBuffer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLCommandBuffer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLCommandBuffer.h	2015-08-23 01:47:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLCommandBuffer.h	2016-05-18 02:19:27.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLCommandQueue.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLCommandQueue.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLCommandQueue.h	2015-08-23 01:47:07.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLCommandQueue.h	2016-05-21 06:45:28.000000000 +0200
@@ -46,4 +46,4 @@
 - (void)insertDebugCaptureBoundary;
 
 @end
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputeCommandEncoder.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputeCommandEncoder.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputeCommandEncoder.h	2015-08-23 01:47:07.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputeCommandEncoder.h	2016-05-21 06:45:28.000000000 +0200
@@ -103,6 +103,8 @@
  */
 - (void)setThreadgroupMemoryLength:(NSUInteger)length atIndex:(NSUInteger)index;
 
+
+
 /*
  @method dispatchThreadgroups:threadsPerThreadgroup:
  @abstract Enqueue a compute function dispatch.
@@ -115,7 +117,8 @@
  @param indirectBuffer A buffer object that the device will read dispatchThreadgroups arguments from, see MTLDispatchThreadgroupsIndirectArguments.
  @param indirectBufferOffset Byte offset within @a indirectBuffer to read arguments from.  @a indirectBufferOffset must be a multiple of 4.
  */
-- (void)dispatchThreadgroupsWithIndirectBuffer:(id <MTLBuffer>)indirectBuffer indirectBufferOffset:(NSUInteger)indirectBufferOffset threadsPerThreadgroup:(MTLSize)threadsPerThreadgroup NS_AVAILABLE(10_11, NA);
+- (void)dispatchThreadgroupsWithIndirectBuffer:(id <MTLBuffer>)indirectBuffer indirectBufferOffset:(NSUInteger)indirectBufferOffset threadsPerThreadgroup:(MTLSize)threadsPerThreadgroup NS_AVAILABLE(10_11, 9_0);
+
 
 
 @end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputePipeline.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputePipeline.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputePipeline.h	2015-08-23 01:47:07.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLComputePipeline.h	2016-05-21 06:45:28.000000000 +0200
@@ -75,4 +75,3 @@
 
 @end
 NS_ASSUME_NONNULL_END
-
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDefines.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDefines.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDefines.h	2015-08-23 01:47:07.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDefines.h	2016-05-21 06:45:29.000000000 +0200
@@ -37,4 +37,3 @@
 #endif
 
 
-#define MTL_DEPRECATED __attribute__((deprecated))
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h	2015-10-24 01:55:41.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h	2016-05-21 06:45:30.000000000 +0200
@@ -25,6 +25,7 @@
 @protocol MTLSamplerState;
 @protocol MTLRenderPipelineState;
 @protocol MTLComputePipelineState;
+
 @class MTLSamplerDescriptor;
 @class MTLRenderPipelineColorAttachmentDescriptor;
 @class MTLDepthStencilDescriptor;
@@ -35,6 +36,8 @@
 @class MTLRenderPipelineReflection;
 @class MTLComputePipelineDescriptor;
 @class MTLComputePipelineReflection;
+@class MTLCommandQueueDescriptor;
+
 
 /*!
  @brief Returns a reference to the preferred system default Metal device.
@@ -57,16 +60,29 @@
 {
     MTLFeatureSet_iOS_GPUFamily1_v1 NS_ENUM_AVAILABLE_IOS(8_0) __TVOS_UNAVAILABLE = 0,
     MTLFeatureSet_iOS_GPUFamily2_v1 NS_ENUM_AVAILABLE_IOS(8_0) __TVOS_UNAVAILABLE = 1,
-    
+
     MTLFeatureSet_iOS_GPUFamily1_v2 NS_ENUM_AVAILABLE_IOS(9_0) __TVOS_UNAVAILABLE = 2,
     MTLFeatureSet_iOS_GPUFamily2_v2 NS_ENUM_AVAILABLE_IOS(9_0) __TVOS_UNAVAILABLE = 3,
+    MTLFeatureSet_iOS_GPUFamily3_v1 NS_ENUM_AVAILABLE_IOS(9_0) __TVOS_UNAVAILABLE = 4,
+
+    MTLFeatureSet_iOS_GPUFamily1_v3 NS_ENUM_AVAILABLE_IOS(10_0) __TVOS_UNAVAILABLE = 5,
+    MTLFeatureSet_iOS_GPUFamily2_v3 NS_ENUM_AVAILABLE_IOS(10_0) __TVOS_UNAVAILABLE = 6,
+    MTLFeatureSet_iOS_GPUFamily3_v2 NS_ENUM_AVAILABLE_IOS(10_0) __TVOS_UNAVAILABLE = 7,
 
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
@@ -78,6 +94,7 @@
     MTLPipelineOptionBufferTypeInfo     = 1 << 1,
 } NS_ENUM_AVAILABLE(10_11, 8_0);
 
+
 /* Convenience typedefs that make it easy to declare storage for certain return types. */
 typedef __autoreleasing MTLRenderPipelineReflection * __nullable MTLAutoreleasedRenderPipelineReflection;
 typedef __autoreleasing MTLComputePipelineReflection * __nullable MTLAutoreleasedComputePipelineReflection;
@@ -96,7 +113,6 @@
  */
 NS_AVAILABLE(10_11, 8_0)
 @protocol MTLDevice <NSObject>
-
 /*!
  @property name
  @abstract The full name of the vendor device.
@@ -141,6 +157,7 @@
  */
 - (id <MTLCommandQueue>)newCommandQueueWithMaxCommandBufferCount:(NSUInteger)maxCommandBufferCount;
 
+
 /*!
  @method newBufferWithLength:options:
  @brief Create a buffer by allocating new memory.
@@ -280,6 +297,7 @@
  */
 - (void)newComputePipelineStateWithDescriptor:(MTLComputePipelineDescriptor *)descriptor options:(MTLPipelineOption)options completionHandler:(MTLNewComputePipelineStateWithReflectionCompletionHandler)completionHandler NS_AVAILABLE(10_11, 9_0);
 
+
 /*!
  @method supportsFeatureSet:
  @abstract Returns TRUE if the feature set is supported by this MTLDevice.
@@ -295,4 +313,3 @@
 
 @end
 NS_ASSUME_NONNULL_END
-
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDrawable.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDrawable.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDrawable.h	2015-08-23 01:47:07.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDrawable.h	2016-05-21 06:45:31.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLFence.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLFence.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLFence.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLFence.h	2016-05-21 06:45:31.000000000 +0200
@@ -0,0 +1,11 @@
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLFunctionConstantValues.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLFunctionConstantValues.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLFunctionConstantValues.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLFunctionConstantValues.h	2016-05-21 06:45:31.000000000 +0200
@@ -0,0 +1,29 @@
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
+// delete all the constants
+- (void)reset;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLHeap.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLHeap.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLHeap.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLHeap.h	2016-05-21 06:45:33.000000000 +0200
@@ -0,0 +1,18 @@
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
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h	2015-08-23 01:47:07.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h	2016-05-21 06:45:33.000000000 +0200
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
+} NS_ENUM_AVAILABLE(10_12, NA);
 
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
+@property (readonly, getter=isPatchData) BOOL              patchData NS_AVAILABLE(10_12, NA);
+@property (readonly, getter=isPatchControlPointData) BOOL  patchControlPointData NS_AVAILABLE(10_12, NA);
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
+@property (readonly) MTLPatchType patchType NS_AVAILABLE(10_12, NA);
+
+/*!
+ @property patchControlPointCount
+ @abstract Returns the number of patch control points if it was specified in the shader. Returns -1 if it
+ was not specified.
+ */
+@property (readonly) NSInteger patchControlPointCount NS_AVAILABLE(10_12, NA);
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLParallelRenderCommandEncoder.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLParallelRenderCommandEncoder.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLParallelRenderCommandEncoder.h	2015-08-23 01:47:07.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLParallelRenderCommandEncoder.h	2016-05-21 06:45:33.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLPixelFormat.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLPixelFormat.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLPixelFormat.h	2015-08-23 01:47:07.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLPixelFormat.h	2016-05-21 06:45:34.000000000 +0200
@@ -74,6 +74,9 @@
     MTLPixelFormatRG11B10Float = 92,
     MTLPixelFormatRGB9E5Float = 93,
 
+    MTLPixelFormatBGR10_XR      NS_AVAILABLE_IOS(NA) = 554,
+    MTLPixelFormatBGR10_XR_sRGB NS_AVAILABLE_IOS(NA) = 555,
+
     /* Normal 64 bit formats */
 
     MTLPixelFormatRG32Uint  = 103,
@@ -86,6 +89,9 @@
     MTLPixelFormatRGBA16Sint   = 114,
     MTLPixelFormatRGBA16Float  = 115,
 
+    MTLPixelFormatBGRA10_XR      NS_AVAILABLE_IOS(NA) = 552,
+    MTLPixelFormatBGRA10_XR_sRGB NS_AVAILABLE_IOS(NA) = 553,
+
     /* Normal 128 bit formats */
 
     MTLPixelFormatRGBA32Uint  = 123,
@@ -184,6 +190,7 @@
 
     /* Depth */
 
+    MTLPixelFormatDepth16Unorm          NS_AVAILABLE_MAC(10_12) = 250,
     MTLPixelFormatDepth32Float  = 252,
 
     /* Stencil */
@@ -195,5 +202,9 @@
     MTLPixelFormatDepth24Unorm_Stencil8  NS_AVAILABLE_MAC(10_11) = 255,
     MTLPixelFormatDepth32Float_Stencil8  NS_AVAILABLE(10_11, 9_0) = 260,
 
+    MTLPixelFormatX32_Stencil8  NS_AVAILABLE(10_12, NA) = 261,
+    MTLPixelFormatX24_Stencil8  NS_AVAILABLE_MAC(10_12) = 262,
+
 } NS_ENUM_AVAILABLE(10_11, 8_0);
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderCommandEncoder.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderCommandEncoder.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderCommandEncoder.h	2015-08-23 01:47:07.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderCommandEncoder.h	2016-05-21 06:45:34.000000000 +0200
@@ -9,6 +9,7 @@
 #import <Metal/MTLDefines.h>
 #import <Metal/MTLCommandEncoder.h>
 #import <Metal/MTLCommandBuffer.h>
+#import <Metal/MTLRenderPass.h>
 
 NS_ASSUME_NONNULL_BEGIN
 @protocol MTLDevice;
@@ -36,7 +37,7 @@
 typedef NS_ENUM(NSUInteger, MTLVisibilityResultMode) {
     MTLVisibilityResultModeDisabled = 0,
     MTLVisibilityResultModeBoolean = 1,
-    MTLVisibilityResultModeCounting NS_ENUM_AVAILABLE(10_11, NA) = 2,
+    MTLVisibilityResultModeCounting NS_ENUM_AVAILABLE(10_11, 9_0) = 2,
 } NS_ENUM_AVAILABLE(10_11, 8_0);
 
 typedef struct {
@@ -83,6 +84,26 @@
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
+
 /*!
  @protocol MTLRenderCommandEncoder
  @discussion MTLRenderCommandEncoder is a container for graphics rendering state and the code to translate the state into a command format that the device can execute. 
@@ -158,8 +179,6 @@
  */
 - (void)setVertexSamplerStates:(const id <MTLSamplerState> __nullable [__nullable])samplers lodMinClamps:(const float [__nullable])lodMinClamps lodMaxClamps:(const float [__nullable])lodMaxClamps withRange:(NSRange)range;
 
-/* Vertex Shaders */
-
 /*!
  @method setViewport:
  @brief Set the viewport, which is used to transform vertexes from normalized device coordinates to window coordinates.  Fragments that lie outside of the viewport are clipped, and optionally clamped for fragments outside of znear/zfar.
@@ -283,8 +302,7 @@
  */
 - (void)setStencilReferenceValue:(uint32_t)referenceValue;
 
-
-/*! 
+/*!
  @method setStencilFrontReferenceValue:backReferenceValue:
  @brief Set the stencil reference value for the back and front stencil buffers independently.
  */
@@ -298,6 +316,29 @@
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
@@ -311,7 +352,7 @@
 - (void)drawPrimitives:(MTLPrimitiveType)primitiveType vertexStart:(NSUInteger)vertexStart vertexCount:(NSUInteger)vertexCount instanceCount:(NSUInteger)instanceCount;
 
 /*!
- @method drawPrimitives:vertexStart:vertexCount:instanceCount:
+ @method drawPrimitives:vertexStart:vertexCount:
  @brief Draw primitives without an index list.
  @param primitiveType The type of primitives that elements are assembled into.
  @param vertexStart For each instance, the first index to draw
@@ -332,7 +373,7 @@
 - (void)drawIndexedPrimitives:(MTLPrimitiveType)primitiveType indexCount:(NSUInteger)indexCount indexType:(MTLIndexType)indexType indexBuffer:(id <MTLBuffer>)indexBuffer indexBufferOffset:(NSUInteger)indexBufferOffset instanceCount:(NSUInteger)instanceCount;
 
 /*!
- @method drawIndexedPrimitives:indexCount:indexType:indexBuffer:indexBufferOffset:instanceCount:
+ @method drawIndexedPrimitives:indexCount:indexType:indexBuffer:indexBufferOffset:
  @brief Draw primitives with an index list.
  @param primitiveType The type of primitives that elements are assembled into.
  @param indexCount The number of indexes to read from the index buffer for each instance.
@@ -343,7 +384,7 @@
 - (void)drawIndexedPrimitives:(MTLPrimitiveType)primitiveType indexCount:(NSUInteger)indexCount indexType:(MTLIndexType)indexType indexBuffer:(id <MTLBuffer>)indexBuffer indexBufferOffset:(NSUInteger)indexBufferOffset;
 
 /*!
- @method drawPrimitives:vertexStart:vertexCount:instanceCount:
+ @method drawPrimitives:vertexStart:vertexCount:instanceCount:baseInstance:
  @brief Draw primitives without an index list.
  @param primitiveType The type of primitives that elements are assembled into.
  @param vertexStart For each instance, the first index to draw
@@ -351,10 +392,10 @@
  @param instanceCount The number of instances drawn.
  @param baseInstance Offset for instance_id.
  */
-- (void)drawPrimitives:(MTLPrimitiveType)primitiveType vertexStart:(NSUInteger)vertexStart vertexCount:(NSUInteger)vertexCount instanceCount:(NSUInteger)instanceCount baseInstance:(NSUInteger)baseInstance NS_AVAILABLE(10_11, NA);
+- (void)drawPrimitives:(MTLPrimitiveType)primitiveType vertexStart:(NSUInteger)vertexStart vertexCount:(NSUInteger)vertexCount instanceCount:(NSUInteger)instanceCount baseInstance:(NSUInteger)baseInstance NS_AVAILABLE(10_11, 9_0);
 
 /*!
- @method drawIndexedPrimitives:indexCount:indexType:indexBuffer:indexBufferOffset:instanceCount:
+ @method drawIndexedPrimitives:indexCount:indexType:indexBuffer:indexBufferOffset:instanceCount:baseVertex:baseInstance:
  @brief Draw primitives with an index list.
  @param primitiveType The type of primitives that elements are assembled into.
  @param indexCount The number of indexes to read from the index buffer for each instance.
@@ -365,7 +406,7 @@
  @param baseVertex Offset for vertex_id. NOTE: this can be negative
  @param baseInstance Offset for instance_id.
  */
-- (void)drawIndexedPrimitives:(MTLPrimitiveType)primitiveType indexCount:(NSUInteger)indexCount indexType:(MTLIndexType)indexType indexBuffer:(id <MTLBuffer>)indexBuffer indexBufferOffset:(NSUInteger)indexBufferOffset instanceCount:(NSUInteger)instanceCount baseVertex:(NSInteger)baseVertex baseInstance:(NSUInteger)baseInstance NS_AVAILABLE(10_11, NA);
+- (void)drawIndexedPrimitives:(MTLPrimitiveType)primitiveType indexCount:(NSUInteger)indexCount indexType:(MTLIndexType)indexType indexBuffer:(id <MTLBuffer>)indexBuffer indexBufferOffset:(NSUInteger)indexBufferOffset instanceCount:(NSUInteger)instanceCount baseVertex:(NSInteger)baseVertex baseInstance:(NSUInteger)baseInstance NS_AVAILABLE(10_11, 9_0);
 
 /*!
  @method drawPrimitives:indirectBuffer:indirectBufferOffset:
@@ -374,7 +415,7 @@
  @param indirectBuffer A buffer object that the device will read drawPrimitives arguments from, see MTLDrawPrimitivesIndirectArguments.
  @param indirectBufferOffset Byte offset within @a indirectBuffer to start reading indexes from.  @a indirectBufferOffset must be a multiple of 4.
  */
-- (void)drawPrimitives:(MTLPrimitiveType)primitiveType indirectBuffer:(id <MTLBuffer>)indirectBuffer indirectBufferOffset:(NSUInteger)indirectBufferOffset NS_AVAILABLE(10_11, NA);
+- (void)drawPrimitives:(MTLPrimitiveType)primitiveType indirectBuffer:(id <MTLBuffer>)indirectBuffer indirectBufferOffset:(NSUInteger)indirectBufferOffset NS_AVAILABLE(10_11, 9_0);
 
 /*!
  @method drawIndexedPrimitives:indexType:indexBuffer:indexBufferOffset:indirectBuffer:indirectBufferOffset:
@@ -386,7 +427,7 @@
  @param indirectBuffer A buffer object that the device will read drawIndexedPrimitives arguments from, see MTLDrawIndexedPrimitivesIndirectArguments.
  @param indirectBufferOffset Byte offset within @a indirectBuffer to start reading indexes from.  @a indirectBufferOffset must be a multiple of 4.
  */
-- (void)drawIndexedPrimitives:(MTLPrimitiveType)primitiveType indexType:(MTLIndexType)indexType indexBuffer:(id <MTLBuffer>)indexBuffer indexBufferOffset:(NSUInteger)indexBufferOffset indirectBuffer:(id <MTLBuffer>)indirectBuffer indirectBufferOffset:(NSUInteger)indirectBufferOffset NS_AVAILABLE(10_11, NA);
+- (void)drawIndexedPrimitives:(MTLPrimitiveType)primitiveType indexType:(MTLIndexType)indexType indexBuffer:(id <MTLBuffer>)indexBuffer indexBufferOffset:(NSUInteger)indexBufferOffset indirectBuffer:(id <MTLBuffer>)indirectBuffer indirectBufferOffset:(NSUInteger)indirectBufferOffset NS_AVAILABLE(10_11, 9_0);
 
 /*!
  @method textureBarrier:
@@ -394,5 +435,18 @@
  */
 - (void)textureBarrier NS_AVAILABLE_MAC(10_11);
 
+
+-(void)setTessellationFactorBuffer:(nullable id <MTLBuffer>)buffer offset:(NSUInteger)offset instanceStride:(NSUInteger)instanceStride NS_AVAILABLE(10_12, NA);
+
+-(void)setTessellationFactorScale:(float)scale NS_AVAILABLE(10_12, NA);
+
+-(void)drawPatches:(NSUInteger)numberOfPatchControlPoints patchStart:(NSUInteger)patchStart patchCount:(NSUInteger)patchCount patchIndexBuffer:(nullable id <MTLBuffer>)patchIndexBuffer patchIndexBufferOffset:(NSUInteger)patchIndexBufferOffset instanceCount:(NSUInteger)instanceCount baseInstance:(NSUInteger)baseInstance NS_AVAILABLE(10_12, NA);
+
+-(void)drawPatches:(NSUInteger)numberOfPatchControlPoints patchIndexBuffer:(nullable id <MTLBuffer>)patchIndexBuffer patchIndexBufferOffset:(NSUInteger)patchIndexBufferOffset indirectBuffer:(id <MTLBuffer>)indirectBuffer indirectBufferOffset:(NSUInteger)indirectBufferOffset NS_AVAILABLE(10_12, NA);
+
+-(void)drawIndexedPatches:(NSUInteger)numberOfPatchControlPoints patchStart:(NSUInteger)patchStart patchCount:(NSUInteger)patchCount patchIndexBuffer:(nullable id <MTLBuffer>)patchIndexBuffer patchIndexBufferOffset:(NSUInteger)patchIndexBufferOffset controlPointIndexBuffer:(id <MTLBuffer>)controlPointIndexBuffer controlPointIndexBufferOffset:(NSUInteger)controlPointIndexBufferOffset instanceCount:(NSUInteger)instanceCount baseInstance:(NSUInteger)baseInstance NS_AVAILABLE(10_12, NA);
+
+-(void)drawIndexedPatches:(NSUInteger)numberOfPatchControlPoints patchIndexBuffer:(nullable id <MTLBuffer>)patchIndexBuffer patchIndexBufferOffset:(NSUInteger)patchIndexBufferOffset controlPointIndexBuffer:(id <MTLBuffer>)controlPointIndexBuffer controlPointIndexBufferOffset:(NSUInteger)controlPointIndexBufferOffset indirectBuffer:(id <MTLBuffer>)indirectBuffer indirectBufferOffset:(NSUInteger)indirectBufferOffset NS_AVAILABLE(10_12, NA);
+
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderPass.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderPass.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderPass.h	2015-08-23 01:47:07.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderPass.h	2016-05-16 08:17:34.000000000 +0200
@@ -21,6 +21,8 @@
     MTLStoreActionDontCare = 0,
     MTLStoreActionStore = 1,
     MTLStoreActionMultisampleResolve = 2,
+    MTLStoreActionStoreAndMultisampleResolve NS_ENUM_AVAILABLE(10_12,10_0) = 3,
+    MTLStoreActionUnknown NS_ENUM_AVAILABLE(10_12,10_0) = 4,
 } NS_ENUM_AVAILABLE(10_11, 8_0);
 
 typedef struct
@@ -116,6 +118,17 @@
 
 @end
 
+/*!
+ @enum MTLMultisampleDepthResolveFilter
+ @abstract Controls the MSAA depth resolve operation. Supported on iOS GPU Family 3 and later.
+ */
+typedef NS_ENUM(NSUInteger, MTLMultisampleDepthResolveFilter)
+{
+    MTLMultisampleDepthResolveFilterSample0 = 0,
+    MTLMultisampleDepthResolveFilterMin = 1,
+    MTLMultisampleDepthResolveFilterMax = 2,
+} NS_ENUM_AVAILABLE_IOS(9_0);
+
 NS_CLASS_AVAILABLE(10_11, 8_0)
 @interface MTLRenderPassDepthAttachmentDescriptor : MTLRenderPassAttachmentDescriptor
 
@@ -125,6 +138,12 @@
  */
 @property (nonatomic) double clearDepth;
 
+/*!
+ @property resolveFilter
+ @abstract The filter to be used for depth multisample resolve.  Defaults to MTLMultisampleDepthResolveFilterSample0.
+ */
+@property (nonatomic) MTLMultisampleDepthResolveFilter depthResolveFilter NS_AVAILABLE_IOS(9_0);
+
 @end
 
 NS_CLASS_AVAILABLE(10_11, 8_0)
@@ -191,4 +210,5 @@
     result.alpha = alpha;
     return result;
 }
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderPipeline.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderPipeline.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderPipeline.h	2015-08-23 01:47:07.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLRenderPipeline.h	2016-05-21 06:45:35.000000000 +0200
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
@@ -56,6 +58,30 @@
     MTLPrimitiveTopologyClassTriangle = 3,
 } NS_ENUM_AVAILABLE_MAC(10_11);
 
+typedef NS_ENUM(NSUInteger, MTLTessellationPartitionMode) {
+    MTLTessellationPartitionModePow2 = 0,
+    MTLTessellationPartitionModeInteger = 1,
+    MTLTessellationPartitionModeFractionalOdd = 2,
+    MTLTessellationPartitionModeFractionalEven = 3,
+} NS_ENUM_AVAILABLE(10_12, NA);
+
+typedef NS_ENUM(NSUInteger, MTLTessellationFactorStepFunction) {
+    MTLTessellationFactorStepFunctionConstant = 0,
+    MTLTessellationFactorStepFunctionPerPatch = 1,
+    MTLTessellationFactorStepFunctionPerInstance = 2,
+    MTLTessellationFactorStepFunctionPerPatchAndPerInstance = 3,
+} NS_ENUM_AVAILABLE(10_12, NA);
+
+typedef NS_ENUM(NSUInteger, MTLTessellationFactorFormat) {
+    MTLTessellationFactorFormatHalf = 0,
+} NS_ENUM_AVAILABLE(10_12, NA);
+
+typedef NS_ENUM(NSUInteger, MTLTessellationControlPointIndexType) {
+    MTLTessellationControlPointIndexTypeNone = 0,
+    MTLTessellationControlPointIndexTypeUInt16 = 1,
+    MTLTessellationControlPointIndexTypeUInt32 = 2,
+} NS_ENUM_AVAILABLE(10_12, NA);
+
 @class MTLRenderPipelineColorAttachmentDescriptorArray;
 
 NS_CLASS_AVAILABLE(10_11, 8_0)
@@ -124,6 +150,14 @@
 
 @property (readwrite, nonatomic) MTLPrimitiveTopologyClass inputPrimitiveTopology NS_AVAILABLE_MAC(10_11);
 
+@property (readwrite, nonatomic) MTLTessellationPartitionMode tessellationPartitionMode NS_AVAILABLE(10_12, NA);
+@property (readwrite, nonatomic) NSUInteger maxTessellationFactor NS_AVAILABLE(10_12, NA);
+@property (readwrite, nonatomic, getter = isTessellationFactorScaleEnabled) BOOL tessellationFactorScaleEnabled NS_AVAILABLE(10_12, NA);
+@property (readwrite, nonatomic) MTLTessellationFactorFormat tessellationFactorFormat NS_AVAILABLE(10_12, NA);
+@property (readwrite, nonatomic) MTLTessellationControlPointIndexType tessellationControlPointIndexType NS_AVAILABLE(10_12, NA);
+@property (readwrite, nonatomic) MTLTessellationFactorStepFunction tessellationFactorStepFunction NS_AVAILABLE(10_12, NA);
+@property (readwrite, nonatomic) MTLWinding tessellationOutputWindingOrder NS_AVAILABLE(10_12, NA);
+
 /*!
  @method reset
  @abstract Restore all pipeline descriptor properties to their default values.
@@ -156,4 +190,6 @@
 - (void)setObject:(nullable MTLRenderPipelineColorAttachmentDescriptor *)attachment atIndexedSubscript:(NSUInteger)attachmentIndex;
 
 @end
+
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLResource.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLResource.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLResource.h	2015-08-23 01:47:07.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLResource.h	2016-05-21 06:45:35.000000000 +0200
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
@@ -119,14 +133,17 @@
 #define MTLResourceStorageModeShift  4
 #define MTLResourceStorageModeMask   (0xfUL << MTLResourceStorageModeShift)
 
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
 
     // Deprecated spellings
     MTLResourceOptionCPUCacheModeDefault       = MTLResourceCPUCacheModeDefaultCache,
@@ -135,6 +152,7 @@
 
 @protocol MTLDevice;
 
+
 /*!
  @protocol MTLResource
  @abstract Common APIs available for MTLBuffer and MTLTexture instances
@@ -165,7 +183,7 @@
  @abstract The resource storage mode used for the CPU mapping for this resource
  */
 @property (readonly) MTLStorageMode storageMode NS_AVAILABLE(10_11, 9_0);
- 
+
 /*!
  @method setPurgeableState
  @abstract Set (or query) the purgeability state of a resource
@@ -173,6 +191,9 @@
  FIXME: If the device is keeping a cached copy of the resource, both the shared copy and cached copy are made purgeable.  Any access to the resource by either the CPU or device will be undefined.
  */
 - (MTLPurgeableState)setPurgeableState:(MTLPurgeableState)state;
- 
+
+
 @end
+
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLSampler.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLSampler.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLSampler.h	2015-08-23 01:47:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLSampler.h	2016-05-18 03:41:30.000000000 +0200
@@ -140,6 +140,12 @@
  */
 @property (nonatomic) float lodMaxClamp;
 
+/*!
+ @property lodAverage
+ @abstract If YES, an average level of detail will be used when sampling from a texture. If NO, no averaging is performed.
+ @discussion lodAverage defaults to NO. This option is a performance hint. An implementation is free to ignore this property.
+ */
+@property (nonatomic) BOOL lodAverage NS_AVAILABLE_IOS(9_0);
 
 /*!
  @property compareFunction
@@ -175,4 +181,4 @@
 @property (readonly) id <MTLDevice> device;
 
 @end
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLTexture.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLTexture.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLTexture.h	2015-08-23 01:47:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLTexture.h	2016-05-21 06:45:36.000000000 +0200
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
@@ -303,8 +301,7 @@
  @method newTextureViewWithPixelFormat:textureType:levels:slices:
  @abstract Create a new texture which shares the same storage as the source texture, but with a different (but compatible) pixel format, texture type, levels and slices.
  */
-- (id<MTLTexture>)newTextureViewWithPixelFormat:(MTLPixelFormat)pixelFormat textureType:(MTLTextureType)textureType levels:(NSRange)levelRange slices:(NSRange)sliceRange;
-
+- (id<MTLTexture>)newTextureViewWithPixelFormat:(MTLPixelFormat)pixelFormat textureType:(MTLTextureType)textureType levels:(NSRange)levelRange slices:(NSRange)sliceRange NS_AVAILABLE(10_11, 9_0);
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLVertexDescriptor.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLVertexDescriptor.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLVertexDescriptor.h	2015-08-23 01:47:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLVertexDescriptor.h	2016-05-21 06:45:38.000000000 +0200
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
+    MTLVertexStepFunctionPerPatch NS_ENUM_AVAILABLE(10_12, NA) = 3,
+    MTLVertexStepFunctionPerPatchControlPoint NS_ENUM_AVAILABLE(10_12, NA) = 4,
 } NS_ENUM_AVAILABLE(10_11, 8_0);
 
 NS_CLASS_AVAILABLE(10_11, 8_0)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/Metal.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/Metal.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Metal.framework/Headers/Metal.h	2015-08-23 01:47:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/Metal.h	2016-05-21 06:45:38.000000000 +0200
@@ -24,3 +24,4 @@
 #import <Metal/MTLRenderCommandEncoder.h>
 #import <Metal/MTLSampler.h>
 #import <Metal/MTLTexture.h>
+#import <Metal/MTLHeap.h>

```