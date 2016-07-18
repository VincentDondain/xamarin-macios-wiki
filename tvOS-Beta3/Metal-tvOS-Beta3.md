#Metal.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h	2016-06-26 07:26:24.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h	2016-07-10 07:16:11.000000000 +0200
@@ -239,9 +239,17 @@
 /*!
  @method newDefaultLibrary
  @abstract Returns the default library for the main bundle.
+ @discussion use newDefaultLibraryWithBundle:error: to get an NSError in case of failure.
  */
 - (nullable id <MTLLibrary>)newDefaultLibrary;
 
+/*
+ @method newDefaultLibraryWithBundle:error:
+ @abstract Returns the default library for a given bundle.
+ @return A pointer to the library, nil if an error occurs.
+*/
+- (nullable id <MTLLibrary>)newDefaultLibraryWithBundle:(NSBundle *)bundle error:(__autoreleasing NSError **)error NS_AVAILABLE(10_12, 10_0);
+
 /*!
  @method newLibraryWithFile:
  @abstract Load a MTLLibrary from a metallib file.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h	2016-06-26 07:26:24.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h	2016-07-10 09:23:03.000000000 +0200
@@ -203,6 +203,7 @@
     MTLLibraryErrorCompileFailure   = 3,
     MTLLibraryErrorCompileWarning   = 4,
     MTLLibraryErrorFunctionNotFound NS_AVAILABLE(10_12, 10_0) = 5,
+    MTLLibraryErrorNotFound NS_AVAILABLE(10_12, 10_0) = 6,
 } NS_ENUM_AVAILABLE(10_11, 8_0);
 
 MTL_EXTERN NSString *const MTLRenderPipelineErrorDomain;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLStageInputOutputDescriptor.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLStageInputOutputDescriptor.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLStageInputOutputDescriptor.h	2016-06-26 06:48:53.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLStageInputOutputDescriptor.h	2016-07-10 07:14:41.000000000 +0200
@@ -107,24 +107,12 @@
 @end
 
 NS_CLASS_AVAILABLE(10_12, 10_0)
-@interface MTLBufferLayoutDescriptorArray : NSObject
-- (MTLBufferLayoutDescriptor *)objectAtIndexedSubscript:(NSUInteger)index;
-- (void)setObject:(nullable MTLBufferLayoutDescriptor *)bufferDesc atIndexedSubscript:(NSUInteger)index;
-@end
-
-NS_CLASS_AVAILABLE(10_12, 10_0)
 @interface MTLAttributeDescriptor : NSObject <NSCopying>
 @property (assign, nonatomic) MTLAttributeFormat format;
 @property (assign, nonatomic) NSUInteger offset;
 @property (assign, nonatomic) NSUInteger bufferIndex;
 @end
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
-@interface MTLAttributeDescriptorArray : NSObject
-- (MTLAttributeDescriptor *)objectAtIndexedSubscript:(NSUInteger)index;
-- (void)setObject:(nullable MTLAttributeDescriptor *)attributeDesc atIndexedSubscript:(NSUInteger)index;
-@end
-
 /*
  MTLStageInputOutputDescriptor
  */
@@ -133,8 +121,8 @@
 
 + (MTLStageInputOutputDescriptor *)stageInputOutputDescriptor;
 
-@property (readonly) MTLBufferLayoutDescriptorArray *layouts;
-@property (readonly) MTLAttributeDescriptorArray *attributes;
+@property (readonly) NSArray<MTLBufferLayoutDescriptor *> *layouts;
+@property (readonly) NSArray<MTLAttributeDescriptor *> *attributes;
 
 /* only used for compute with MTLStepFunction...Indexed */
 @property (assign, nonatomic) MTLIndexType indexType;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLVertexDescriptor.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLVertexDescriptor.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLVertexDescriptor.h	2016-06-26 07:42:16.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLVertexDescriptor.h	2016-07-10 07:14:41.000000000 +0200
@@ -9,8 +9,10 @@
 #import <Metal/MTLDevice.h>
 
 NS_ASSUME_NONNULL_BEGIN
-/*
- MTLVertexFormat is deprecated, use MTLAttributeFormat instead
+
+/*!
+ @enum MTLVertexFormat
+ @abstract specifies how the vertex attribute data is laid out in memory.
 */
 typedef NS_ENUM(NSUInteger, MTLVertexFormat)
 {

```