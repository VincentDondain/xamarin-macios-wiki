#Ruby.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Ruby.framework/Headers/ruby/config.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Ruby.framework/Headers/ruby/config.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Ruby.framework/Headers/ruby/config.h	2015-08-01 01:01:32.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Ruby.framework/Headers/ruby/config.h	2016-05-11 15:49:43.000000000 +0200
@@ -111,6 +111,7 @@
 #define HAVE_STRUCT_TIMEVAL 1
 #define HAVE_STRUCT_TIMESPEC 1
 #define HAVE_STRUCT_TIMEZONE 1
+#define HAVE_CLOCKID_T 1
 #define HAVE_RB_FD_INIT 1
 #define HAVE_INT8_T 1
 #define SIZEOF_INT8_T 1
@@ -213,7 +214,6 @@
 #define HAVE_SIGPROCMASK 1
 #define HAVE_SIGACTION 1
 #define HAVE_SIGSETJMP 1
-#define HAVE__SETJMP 1
 #define HAVE__LONGJMP 1
 #define HAVE_GETSID 1
 #define HAVE_SETSID 1
@@ -233,6 +233,7 @@
 #define HAVE_MKTIME 1
 #define HAVE_TIMEGM 1
 #define HAVE_GMTIME_R 1
+#define HAVE_CLOCK_GETTIME 1
 #define HAVE_GETTIMEOFDAY 1
 #define HAVE_POLL 1
 #define HAVE_PREAD 1
@@ -242,9 +243,9 @@
 #define HAVE_DUP 1
 #define HAVE_POSIX_MEMALIGN 1
 #define HAVE_IOCTL 1
-#define RUBY_SETJMP(env) _setjmp(env)
-#define RUBY_LONGJMP(env,val) _longjmp(env,val)
-#define RUBY_JMP_BUF jmp_buf
+#define RUBY_SETJMP(env) sigsetjmp(env,0)
+#define RUBY_LONGJMP(env,val) siglongjmp(env,val)
+#define RUBY_JMP_BUF sigjmp_buf
 #define HAVE_STRUCT_TM_TM_ZONE 1
 #define HAVE_TM_ZONE 1
 #define HAVE_STRUCT_TM_TM_GMTOFF 1
@@ -279,10 +280,10 @@
 #define LIBDIR_BASENAME "lib"
 #define HAVE_PTHREAD_H 1
 #define RUBY_EXEC_PREFIX "/System/Library/Frameworks/Ruby.framework/Versions/2.0/usr"
-#if defined __x86_64__
-#define RUBY_PLATFORM_CPU "x86_64"
-#endif /* defined __x86_64__ */
 #if defined __i386__
 #define RUBY_PLATFORM_CPU "i386"
 #endif /* defined __i386__ */
+#if defined __x86_64__
+#define RUBY_PLATFORM_CPU "x86_64"
+#endif /* defined __x86_64__ */
 #endif /* INCLUDE_RUBY_CONFIG_H */

```