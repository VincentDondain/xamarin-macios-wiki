#Metal.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h	2016-07-10 09:23:03.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h	2016-07-23 21:42:48.000000000 +0200
@@ -135,18 +135,23 @@
  */
 @property (readonly) NSString *name;
 
+/*!
+ @property functionConstantsDictionary
+ @abstract A dictionary containing information about all function contents, keyed by the constant names.
+ */
+@property (readonly) NSDictionary<NSString *, MTLFunctionConstant *> *functionConstantsDictionary NS_AVAILABLE(10_12, 10_0);
 
 /*!
  @property functionConstants
  @abstract Array containing the ubershader constants used by this function.
  */
-@property (readonly) NSArray<MTLFunctionConstant *> *functionConstants NS_AVAILABLE(10_12, 10_0);
+@property (readonly) NSArray<MTLFunctionConstant *> *functionConstants NS_DEPRECATED(10_12, 10_12, 10_0, 10_0);
 
 /*!
  @method functionConstantIndexByName:type:
  @abstract Returns the index of an ubershader constant and its type
  */
-- (NSUInteger)functionConstantIndexByName:(NSString *)name type:(MTLDataType *)type NS_AVAILABLE(10_12, 10_0);
+- (NSUInteger)functionConstantIndexByName:(NSString *)name type:(MTLDataType *)type NS_DEPRECATED(10_12, 10_12, 10_0, 10_0);
 
 @end
 
@@ -203,7 +208,7 @@
     MTLLibraryErrorCompileFailure   = 3,
     MTLLibraryErrorCompileWarning   = 4,
     MTLLibraryErrorFunctionNotFound NS_AVAILABLE(10_12, 10_0) = 5,
-    MTLLibraryErrorNotFound NS_AVAILABLE(10_12, 10_0) = 6,
+    MTLLibraryErrorFileNotFound NS_AVAILABLE(10_12, 10_0) = 6,
 } NS_ENUM_AVAILABLE(10_11, 8_0);
 
 MTL_EXTERN NSString *const MTLRenderPipelineErrorDomain;
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLStageInputOutputDescriptor.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLStageInputOutputDescriptor.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLStageInputOutputDescriptor.h	2016-07-08 17:00:08.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLStageInputOutputDescriptor.h	2016-07-23 21:42:49.000000000 +0200
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