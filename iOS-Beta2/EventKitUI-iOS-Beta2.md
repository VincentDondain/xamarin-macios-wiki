#EventKitUI.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/EventKitUI.framework/Headers/EventKitUIDefines.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/EventKitUI.framework/Headers/EventKitUIDefines.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/EventKitUI.framework/Headers/EventKitUIDefines.h	2016-05-25 06:29:10.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/EventKitUI.framework/Headers/EventKitUIDefines.h	2016-06-27 08:28:44.000000000 +0200
@@ -13,4 +13,24 @@
 #define EVENTKITUI_EXTERN               extern __attribute__((visibility ("default")))
 #endif
 
-#define EVENTKITUI_CLASS_AVAILABLE(_iphoneIntro) __attribute__((visibility("default"))) NS_CLASS_AVAILABLE(NA, _iphoneIntro)
\ No newline at end of file
+#define EVENTKITUI_CLASS_AVAILABLE(_iphoneIntro) __attribute__((visibility("default"))) NS_CLASS_AVAILABLE(NA, _iphoneIntro)
+
+#ifndef EKUI_HAS_HEADER
+#define EKUI_HAS_HEADER(include_path) (defined(__has_include) && __has_include(include_path))
+#endif
+
+#ifndef EKUI_IS_NANO
+#define EKUI_IS_NANO (defined(TARGET_OS_WATCH) && TARGET_OS_WATCH)
+#endif
+
+#ifndef EKUI_IS_ZEUS
+#define EKUI_IS_ZEUS (defined(TARGET_OS_TV) && TARGET_OS_TV)
+#endif
+
+#ifndef EKUI_IS_IOS
+#define EKUI_IS_IOS (defined(TARGET_OS_IOS) && TARGET_OS_IOS)
+#endif
+
+#ifndef EKUI_IS_SIMULATOR
+#define EKUI_IS_SIMULATOR (defined(TARGET_OS_SIMULATOR) && TARGET_OS_SIMULATOR)
+#endif

```