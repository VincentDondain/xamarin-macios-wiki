#TVMLKit.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/TVMLKit.framework/Headers/TVMLKitDefines.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/TVMLKit.framework/Headers/TVMLKitDefines.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/TVMLKit.framework/Headers/TVMLKitDefines.h	2016-08-12 07:08:36.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/TVMLKit.framework/Headers/TVMLKitDefines.h	2016-10-24 07:02:51.000000000 +0200
@@ -8,10 +8,20 @@
 #ifndef _TVMLKit_TVMLKitDefines_
 #define _TVMLKit_TVMLKitDefines_
 
-#import <TVServices/TVServicesDefines.h>
+#if !defined(TV_EXTERN)
+#ifdef __cplusplus
+#define TV_EXTERN   extern "C" __attribute__((visibility ("default")))
+#else
+#define TV_EXTERN   extern __attribute__((visibility ("default")))
+#endif
+#endif
 
 #if !defined(TV_EXTERN_CLASS)
-#define TV_EXTERN_CLASS __attribute__((visibility("default")))
+#ifdef __cplusplus
+#define TV_EXTERN_CLASS   extern "C" __attribute__((visibility ("default")))
+#else
+#define TV_EXTERN_CLASS   extern __attribute__((visibility ("default")))
+#endif
 #endif
 
 #if !defined(TV_EXTERN_CLASS_AVAILABLE)

```