#Metal.framework

``` diff
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h	2016-07-22 23:59:19.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h	2016-08-03 03:46:35.000000000 +0200
@@ -147,17 +147,13 @@
 @property (readonly, getter=isHeadless) BOOL headless NS_AVAILABLE_MAC(10_11);
 
 /*!
- @property sharedMemorySize
- @abstract Return the maximum amount of shared system memory this device can use.
-*/
-@property (readonly) uint64_t sharedMemorySize NS_AVAILABLE(10_12, 10_0);
- 
-/*!
- @property dedicatedMemorySize
- @abstract Return the maximum amount of dedicated memory this device has.
-*/
-@property (readonly) uint64_t dedicatedMemorySize NS_AVAILABLE(10_12, 10_0);
- 
+ @property recommendedMaxWorkingSetSize
+ @abstract Returns an approximation of how much memory this device can use with good performance.
+ @discussion Performance may be improved by keeping the total size of all resources (texture and buffers)
+ and heaps less than this threshold, beyond which the device is likely to be overcommitted and incur a
+ performance penalty. */
+@property (readonly) uint64_t recommendedMaxWorkingSetSize NS_AVAILABLE_MAC(10_12);
+
 /*!
  @property depth24Stencil8PixelFormatSupported
  @abstract If YES, device supports MTLPixelFormatDepth24Unorm_Stencil8.
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h	2016-07-22 22:51:15.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h	2016-08-03 03:59:16.000000000 +0200
@@ -135,18 +135,11 @@
  */
 @property (readonly) NSString *name;
 
-
-/*!
- @property functionConstants
- @abstract Array containing the ubershader constants used by this function.
- */
-@property (readonly) NSArray<MTLFunctionConstant *> *functionConstants NS_AVAILABLE(10_12, 10_0);
-
 /*!
- @method functionConstantIndexByName:type:
- @abstract Returns the index of an ubershader constant and its type
+ @property functionConstantsDictionary
+ @abstract A dictionary containing information about all function contents, keyed by the constant names.
  */
-- (NSUInteger)functionConstantIndexByName:(NSString *)name type:(MTLDataType *)type NS_AVAILABLE(10_12, 10_0);
+@property (readonly) NSDictionary<NSString *, MTLFunctionConstant *> *functionConstantsDictionary NS_AVAILABLE(10_12, 10_0);
 
 @end
 
@@ -203,7 +196,7 @@
     MTLLibraryErrorCompileFailure   = 3,
     MTLLibraryErrorCompileWarning   = 4,
     MTLLibraryErrorFunctionNotFound NS_AVAILABLE(10_12, 10_0) = 5,
-    MTLLibraryErrorNotFound NS_AVAILABLE(10_12, 10_0) = 6,
+    MTLLibraryErrorFileNotFound NS_AVAILABLE(10_12, 10_0) = 6,
 } NS_ENUM_AVAILABLE(10_11, 8_0);
 
 MTL_EXTERN NSString *const MTLRenderPipelineErrorDomain;
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLStageInputOutputDescriptor.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLStageInputOutputDescriptor.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLStageInputOutputDescriptor.h	2016-07-22 22:51:15.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLStageInputOutputDescriptor.h	2016-08-03 03:46:36.000000000 +0200
@@ -107,12 +107,24 @@
 @end
 
 NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface MTLBufferLayoutDescriptorArray : NSObject
+- (MTLBufferLayoutDescriptor *)objectAtIndexedSubscript:(NSUInteger)index;
+- (void)setObject:(nullable MTLBufferLayoutDescriptor *)bufferDesc atIndexedSubscript:(NSUInteger)index;
+@end
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
 @interface MTLAttributeDescriptor : NSObject <NSCopying>
 @property (assign, nonatomic) MTLAttributeFormat format;
 @property (assign, nonatomic) NSUInteger offset;
 @property (assign, nonatomic) NSUInteger bufferIndex;
 @end
 
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface MTLAttributeDescriptorArray : NSObject
+- (MTLAttributeDescriptor *)objectAtIndexedSubscript:(NSUInteger)index;
+- (void)setObject:(nullable MTLAttributeDescriptor *)attributeDesc atIndexedSubscript:(NSUInteger)index;
+@end
+
 /*
  MTLStageInputOutputDescriptor
  */
@@ -121,8 +133,8 @@
 
 + (MTLStageInputOutputDescriptor *)stageInputOutputDescriptor;
 
-@property (readonly) NSArray<MTLBufferLayoutDescriptor *> *layouts;
-@property (readonly) NSArray<MTLAttributeDescriptor *> *attributes;
+@property (readonly) MTLBufferLayoutDescriptorArray *layouts;
+@property (readonly) MTLAttributeDescriptorArray *attributes;
 
 /* only used for compute with MTLStepFunction...Indexed */
 @property (assign, nonatomic) MTLIndexType indexType;

```