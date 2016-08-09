#Ruby.framework

``` diff
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Ruby.framework/Headers/ruby/config.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Ruby.framework/Headers/ruby/config.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Ruby.framework/Headers/ruby/config.h	2016-07-23 01:54:55.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Ruby.framework/Headers/ruby/config.h	2016-08-02 02:27:33.000000000 +0200
@@ -280,10 +280,10 @@
 #define LIBDIR_BASENAME "lib"
 #define HAVE_PTHREAD_H 1
 #define RUBY_EXEC_PREFIX "/System/Library/Frameworks/Ruby.framework/Versions/2.0/usr"
-#if defined __i386__
-#define RUBY_PLATFORM_CPU "i386"
-#endif /* defined __i386__ */
 #if defined __x86_64__
 #define RUBY_PLATFORM_CPU "x86_64"
 #endif /* defined __x86_64__ */
+#if defined __i386__
+#define RUBY_PLATFORM_CPU "i386"
+#endif /* defined __i386__ */
 #endif /* INCLUDE_RUBY_CONFIG_H */

```