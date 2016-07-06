#JavaScriptCore.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSBase.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSBase.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSBase.h	2016-05-25 07:00:15.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSBase.h	2016-06-26 08:50:23.000000000 +0200
@@ -138,7 +138,7 @@
 
 /* Enable the Objective-C API for platforms with a modern runtime. */
 #if !defined(JSC_OBJC_API_ENABLED)
-#define JSC_OBJC_API_ENABLED (defined(__clang__) && defined(__APPLE__) && !defined(BUILDING_GTK__) && ((defined(__MAC_OS_X_VERSION_MIN_REQUIRED) && !defined(__i386__)) || (defined(TARGET_OS_IPHONE) && TARGET_OS_IPHONE)))
+#define JSC_OBJC_API_ENABLED (defined(__clang__) && defined(__APPLE__) && ((defined(__MAC_OS_X_VERSION_MIN_REQUIRED) && !defined(__i386__)) || (defined(TARGET_OS_IPHONE) && TARGET_OS_IPHONE)))
 #endif
 
 #endif /* JSBase_h */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSStringRef.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSStringRef.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSStringRef.h	2016-05-04 00:21:21.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSStringRef.h	2016-06-26 07:42:24.000000000 +0200
@@ -41,7 +41,9 @@
     && !((defined(__CC_ARM) || defined(__ARMCC__)) && !defined(__linux__)) /* RVCT */
 /*!
 @typedef JSChar
-@abstract A Unicode character.
+@abstract A UTF-16 code unit. One, or a sequence of two, can encode any Unicode
+ character. As with all scalar types, endianness depends on the underlying
+ architecture.
 */
     typedef unsigned short JSChar;
 #else

```