#OpenCL.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/OpenCL.framework/Headers/cl_gl_ext.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/OpenCL.framework/Headers/cl_gl_ext.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/OpenCL.framework/Headers/cl_gl_ext.h	2016-06-03 05:01:16.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/OpenCL.framework/Headers/cl_gl_ext.h	2016-06-28 05:31:00.000000000 +0200
@@ -109,7 +109,11 @@
                            cl_int *   __nullable /* errcode_ret */) CL_EXT_SUFFIX__VERSION_1_1;
 
 #ifdef AVAILABLE_MAC_OS_X_VERSION_10_7_AND_LATER
-typedef struct __IOSurface* IOSurfaceRef;
+#if __has_feature(objc_class_property)
+typedef struct  __attribute__((objc_bridge(id))) __IOSurface *IOSurfaceRef __attribute__((swift_name("IOSurfaceRef")));
+#else
+typedef struct  __attribute__((objc_bridge(id))) __IOSurface *IOSurfaceRef;
+#endif
 #endif
 
 cl_mem __nullable clCreateImageFromIOSurface2DAPPLE(cl_context __nonnull /* context */,

```