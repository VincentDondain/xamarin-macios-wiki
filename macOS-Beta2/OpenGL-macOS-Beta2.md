#OpenGL.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/OpenGL.framework/Headers/CGLIOSurface.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/OpenGL.framework/Headers/CGLIOSurface.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/OpenGL.framework/Headers/CGLIOSurface.h	2016-06-03 04:58:16.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/OpenGL.framework/Headers/CGLIOSurface.h	2016-06-28 05:24:12.000000000 +0200
@@ -15,7 +15,7 @@
 
 OPENGL_ASSUME_NONNULL_BEGIN
 
-typedef struct __IOSurface *IOSurfaceRef;
+typedef struct  OPENGL_BRIDGED_TYPE(id) __IOSurface *IOSurfaceRef OPENGL_SWIFT_NAME(IOSurfaceRef);
 
 /*!
             @function  CGLTexImageIOSurface2D
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/OpenGL.framework/Headers/CGLTypes.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/OpenGL.framework/Headers/CGLTypes.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/OpenGL.framework/Headers/CGLTypes.h	2016-06-03 04:58:16.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/OpenGL.framework/Headers/CGLTypes.h	2016-06-28 05:24:11.000000000 +0200
@@ -27,6 +27,18 @@
 #define OPENGL_NONNULL
 #endif
 
+#if __has_attribute(objc_bridge) && __has_feature(objc_bridge_id) && __has_feature(objc_bridge_id_on_typedefs)
+#define OPENGL_BRIDGED_TYPE(T)		__attribute__((objc_bridge(T)))
+#else
+#define OPENGL_BRIDGED_TYPE(T)
+#endif
+
+#if __has_feature(objc_class_property)
+#define OPENGL_SWIFT_NAME(name) __attribute__((swift_name(#name)))
+#else
+#define OPENGL_SWIFT_NAME(name)
+#endif
+
 /*
 ** CGL opaque data.
 */

```