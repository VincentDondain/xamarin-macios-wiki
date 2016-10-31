#Ruby.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Ruby.framework/Headers/ruby/config.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Ruby.framework/Headers/ruby/config.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Ruby.framework/Headers/ruby/config.h	2016-07-30 23:46:12.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Ruby.framework/Headers/ruby/config.h	2016-07-31 01:39:33.000000000 +0200
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