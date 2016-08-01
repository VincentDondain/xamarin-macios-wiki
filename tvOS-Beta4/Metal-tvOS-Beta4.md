#Metal.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h	2016-07-10 07:16:11.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Metal.framework/Headers/MTLDevice.h	2016-07-22 23:59:19.000000000 +0200
@@ -80,12 +80,10 @@
     MTLFeatureSet_tvOS_GPUFamily1_v1 __TVOS_AVAILABLE(9.0) __IOS_UNAVAILABLE __OSX_UNAVAILABLE = 30000,
 
     MTLFeatureSet_tvOS_GPUFamily1_v2 __TVOS_AVAILABLE(10.0) __IOS_UNAVAILABLE __OSX_UNAVAILABLE = 30001,
-    MTLFeatureSet_tvOS_GPUFamily2_v1 __TVOS_AVAILABLE(10.0) __IOS_UNAVAILABLE __OSX_UNAVAILABLE = 30002,
 } NS_ENUM_AVAILABLE(10_11, 8_0) __TVOS_AVAILABLE(9.0);
 
 
 #define MTLFeatureSet_TVOS_GPUFamily1_v1 MTLFeatureSet_tvOS_GPUFamily1_v1
-#define MTLFeatureSet_TVOS_GPUFamily2_v1 MTLFeatureSet_tvOS_GPUFamily2_v1 // NOTE: do not ship this in public headers
 
 /*!
  @enum MTLPipelineOption

```