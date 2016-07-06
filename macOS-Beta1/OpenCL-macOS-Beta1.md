#OpenCL.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/OpenCL.framework/Headers/cl_platform.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/OpenCL.framework/Headers/cl_platform.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/OpenCL.framework/Headers/cl_platform.h	2015-08-27 04:21:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/OpenCL.framework/Headers/cl_platform.h	2016-06-03 05:01:16.000000000 +0200
@@ -324,6 +324,14 @@
  */
 
 /* Define basic vector types */
+    
+#ifndef __has_feature         // Optional of course.
+    #define __has_feature(x) 0  // Compatibility with non-clang compilers.
+#endif
+#ifndef __has_extension
+    #define __has_extension __has_feature // Compatibility with pre-3.0 compilers.
+#endif
+    
 #if defined( __VEC__ )
    #include <altivec.h>   /* may be omitted depending on compiler. AltiVec spec provides no way to detect whether the header is required. */
    typedef vector unsigned char     __cl_uchar16;
@@ -348,8 +356,10 @@
     #else
         #include <xmmintrin.h>
     #endif
-    #if defined( __GNUC__ )
-        typedef float __cl_float4   __attribute__((vector_size(16)));
+    #if __has_extension(attribute_ext_vector_type)
+        typedef     __attribute__((ext_vector_type(4)))     float __cl_float4;
+    #elif defined( __GNUC__ )
+        typedef     __attribute__((vector_size(16)))        float __cl_float4;
     #else
         typedef __m128 __cl_float4;
     #endif
@@ -362,16 +372,26 @@
     #else
         #include <emmintrin.h>
     #endif
-    #if defined( __GNUC__ )
-        typedef cl_uchar    __cl_uchar16    __attribute__((vector_size(16)));
-        typedef cl_char     __cl_char16     __attribute__((vector_size(16)));
-        typedef cl_ushort   __cl_ushort8    __attribute__((vector_size(16)));
-        typedef cl_short    __cl_short8     __attribute__((vector_size(16)));
-        typedef cl_uint     __cl_uint4      __attribute__((vector_size(16)));
-        typedef cl_int      __cl_int4       __attribute__((vector_size(16)));
-        typedef cl_ulong    __cl_ulong2     __attribute__((vector_size(16)));
-        typedef cl_long     __cl_long2      __attribute__((vector_size(16)));
-        typedef cl_double   __cl_double2    __attribute__((vector_size(16)));
+    #if __has_extension(attribute_ext_vector_type)
+        typedef cl_uchar    __attribute__((ext_vector_type(16)))    __cl_uchar16;
+        typedef cl_char     __attribute__((ext_vector_type(16)))    __cl_char16;
+        typedef cl_ushort   __attribute__((ext_vector_type(8)))     __cl_ushort8;
+        typedef cl_short    __attribute__((ext_vector_type(8)))     __cl_short8;
+        typedef cl_uint     __attribute__((ext_vector_type(4)))     __cl_uint4;
+        typedef cl_int      __attribute__((ext_vector_type(4)))     __cl_int4;
+        typedef cl_ulong    __attribute__((ext_vector_type(2)))     __cl_ulong2;
+        typedef cl_long     __attribute__((ext_vector_type(2)))     __cl_long2;
+        typedef cl_double   __attribute__((ext_vector_type(2)))     __cl_double2;
+    #elif defined( __GNUC__ )
+        typedef cl_uchar    __attribute__((vector_size(16)))        __cl_uchar16;
+        typedef cl_char     __attribute__((vector_size(16)))        __cl_char16;
+        typedef cl_ushort   __attribute__((vector_size(16)))        __cl_ushort8;
+        typedef cl_short    __attribute__((vector_size(16)))        __cl_short8;
+        typedef cl_uint     __attribute__((vector_size(16)))        __cl_uint4;
+        typedef cl_int      __attribute__((vector_size(16)))        __cl_int4;
+        typedef cl_ulong    __attribute__((vector_size(16)))        __cl_ulong2;
+        typedef cl_long     __attribute__((vector_size(16)))        __cl_long2;
+        typedef cl_double   __attribute__((vector_size(16)))        __cl_double2;
     #else
         typedef __m128i __cl_uchar16;
         typedef __m128i __cl_char16;
@@ -396,16 +416,24 @@
 
 #if defined( __MMX__ )
     #include <mmintrin.h>
-    #if defined( __GNUC__ )
-        typedef cl_uchar    __cl_uchar8     __attribute__((vector_size(8)));
-        typedef cl_char     __cl_char8      __attribute__((vector_size(8)));
-        typedef cl_ushort   __cl_ushort4    __attribute__((vector_size(8)));
-        typedef cl_short    __cl_short4     __attribute__((vector_size(8)));
-        typedef cl_uint     __cl_uint2      __attribute__((vector_size(8)));
-        typedef cl_int      __cl_int2       __attribute__((vector_size(8)));
-        typedef cl_ulong    __cl_ulong1     __attribute__((vector_size(8)));
-        typedef cl_long     __cl_long1      __attribute__((vector_size(8)));
-        typedef cl_float    __cl_float2     __attribute__((vector_size(8)));
+    #if __has_extension(attribute_ext_vector_type)
+        typedef cl_uchar    __attribute__((ext_vector_type(8)))     __cl_uchar8;
+        typedef cl_char     __attribute__((ext_vector_type(8)))     __cl_char8 ;
+        typedef cl_ushort   __attribute__((ext_vector_type(4)))     __cl_ushort4   ;
+        typedef cl_short    __attribute__((ext_vector_type(4)))     __cl_short4;
+        typedef cl_uint     __attribute__((ext_vector_type(2)))     __cl_uint2;
+        typedef cl_int      __attribute__((ext_vector_type(2)))     __cl_int2;
+        typedef cl_ulong    __attribute__((ext_vector_type(1)))     __cl_ulong1;
+        typedef cl_long     __attribute__((ext_vector_type(1)))     __cl_long1;
+    #elif defined( __GNUC__ )
+        typedef cl_uchar    __attribute__((vector_size(8)))         __cl_uchar8;
+        typedef cl_char     __attribute__((vector_size(8)))         __cl_char8;
+        typedef cl_ushort   __attribute__((vector_size(8)))         __cl_ushort4;
+        typedef cl_short    __attribute__((vector_size(8)))         __cl_short4;
+        typedef cl_uint     __attribute__((vector_size(8)))         __cl_uint2;
+        typedef cl_int      __attribute__((vector_size(8)))         __cl_int2;
+        typedef cl_ulong    __attribute__((vector_size(8)))         __cl_ulong1;
+        typedef cl_long     __attribute__((vector_size(8)))         __cl_long1;
     #else
         typedef __m64       __cl_uchar8;
         typedef __m64       __cl_char8;
@@ -415,7 +443,6 @@
         typedef __m64       __cl_int2;
         typedef __m64       __cl_ulong1;
         typedef __m64       __cl_long1;
-        typedef __m64       __cl_float2;
     #endif
     #define __CL_UCHAR8__   1
     #define __CL_CHAR8__    1
@@ -425,7 +452,6 @@
     #define __CL_UINT2__    1
     #define __CL_ULONG1__   1
     #define __CL_LONG1__    1
-    #define __CL_FLOAT2__   1
 #endif
 
 #if defined( __AVX__ )
@@ -434,17 +460,60 @@
     #else
         #include <immintrin.h> 
     #endif
-    #if defined( __GNUC__ )
-        typedef cl_float    __cl_float8     __attribute__((vector_size(32)));
-        typedef cl_double   __cl_double4    __attribute__((vector_size(32)));
+    #if __has_extension(attribute_ext_vector_type)
+        typedef cl_float    __attribute__((ext_vector_type(8)))     __cl_float8;
+        typedef cl_double   __attribute__((ext_vector_type(4)))     __cl_double4;
+    #elif defined( __GNUC__ )
+        typedef cl_float    __attribute__((vector_size(32)))        __cl_float8;
+        typedef cl_double   __attribute__((vector_size(32)))        __cl_double4;
     #else
-        typedef __m256      __cl_float8;
-        typedef __m256d     __cl_double4;
+        typedef __m256       __cl_float8;
+        typedef __m256d      __cl_double4;
     #endif
+
     #define __CL_FLOAT8__   1
     #define __CL_DOUBLE4__  1
+    
 #endif
 
+#if defined( __AVX2__ )
+    #if defined( __MINGW64__ )
+        #include <intrin.h>
+    #else
+        #include <immintrin.h>
+    #endif
+#if __has_extension(attribute_ext_vector_type)
+    typedef cl_ushort   __attribute__((ext_vector_type(16)))    __cl_ushort16;
+    typedef cl_short    __attribute__((ext_vector_type(16)))    __cl_short16;
+    typedef cl_uint     __attribute__((ext_vector_type(8)))     __cl_uint8;
+    typedef cl_int      __attribute__((ext_vector_type(8)))     __cl_int8;
+    typedef cl_uint     __attribute__((ext_vector_type(4)))     __cl_ulong4;
+    typedef cl_int      __attribute__((ext_vector_type(4)))     __cl_long4;
+#elif defined( __GNUC__ )
+    typedef cl_ushort   __attribute__((vector_size(32)))        __cl_ushort16;
+    typedef cl_short    __attribute__((vector_size(32)))        __cl_short16;
+    typedef cl_uint     __attribute__((vector_size(32)))        __cl_uint8;
+    typedef cl_int      __attribute__((vector_size(32)))        __cl_int8;
+    typedef cl_uint     __attribute__((vector_size(32)))        __cl_ulong4;
+    typedef cl_int      __attribute__((vector_size(32)))        __cl_long4;
+#else
+    typedef __m256i       __cl_ushort16;
+    typedef __m256i       __cl_short16;
+    typedef __m256i       __cl_uint8;
+    typedef __m256i       __cl_int8;
+    typedef __m256i       __cl_ulong4;
+    typedef __m256i       __cl_long4;
+#endif
+    
+#define __CL_USHORT16__ 1
+#define __CL_SHORT16__  1
+#define __CL_UINT8__    1
+#define __CL_INT8__     1
+#define __CL_ULONG4__   1
+#define __CL_LONG4__    1
+    
+#endif
+    
 /* Define alignment keys */
 #if defined( __GNUC__ )
     #define CL_ALIGNED(_x)          __attribute__ ((aligned(_x)))

```