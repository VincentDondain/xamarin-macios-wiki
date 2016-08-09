#Metal.framework

``` diff
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h	2016-07-23 21:42:47.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h	2016-08-02 21:01:53.000000000 +0200
@@ -148,17 +148,13 @@
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
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h	2016-07-23 21:42:48.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLLibrary.h	2016-08-03 03:59:16.000000000 +0200
@@ -141,18 +141,6 @@
  */
 @property (readonly) NSDictionary<NSString *, MTLFunctionConstant *> *functionConstantsDictionary NS_AVAILABLE(10_12, 10_0);
 
-/*!
- @property functionConstants
- @abstract Array containing the ubershader constants used by this function.
- */
-@property (readonly) NSArray<MTLFunctionConstant *> *functionConstants NS_DEPRECATED(10_12, 10_12, 10_0, 10_0);
-
-/*!
- @method functionConstantIndexByName:type:
- @abstract Returns the index of an ubershader constant and its type
- */
-- (NSUInteger)functionConstantIndexByName:(NSString *)name type:(MTLDataType *)type NS_DEPRECATED(10_12, 10_12, 10_0, 10_0);
-
 @end
 
 typedef NS_ENUM(NSUInteger, MTLLanguageVersion) {

```