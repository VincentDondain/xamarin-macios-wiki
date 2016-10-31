#Kernel.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/Availability.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/Availability.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/Availability.h	2016-09-20 00:11:22.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/Availability.h	2016-10-22 20:21:05.000000000 +0200
@@ -135,6 +135,7 @@
 #define __MAC_10_11_4       101104
 #define __MAC_10_12         101200
 #define __MAC_10_12_1       101201
+#define __MAC_10_12_2       101202
 /* __MAC_NA is not defined to a value but is uses as a token by macros to indicate that the API is unavailable */
 
 #define __IPHONE_2_0      20000
@@ -164,6 +165,7 @@
 #define __IPHONE_9_3      90300
 #define __IPHONE_10_0    100000
 #define __IPHONE_10_1    100100
+#define __IPHONE_10_2    100200
 /* __IPHONE_NA is not defined to a value but is uses as a token by macros to indicate that the API is unavailable */
 
 #define __TVOS_9_0        90000
@@ -171,11 +173,13 @@
 #define __TVOS_9_2        90200
 #define __TVOS_10_0      100000
 #define __TVOS_10_0_1    100001
+#define __TVOS_10_1      100100
 
 #define __WATCHOS_1_0     10000
 #define __WATCHOS_2_0     20000
 #define __WATCHOS_3_0     30000
 #define __WATCHOS_3_1     30100
+#define __WATCHOS_3_1_1   30101
 
 #include <AvailabilityInternal.h>
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityInternal.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityInternal.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityInternal.h	2016-09-20 00:11:19.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityInternal.h	2016-10-22 20:20:56.000000000 +0200
@@ -80,7 +80,7 @@
 #ifdef __IPHONE_OS_VERSION_MIN_REQUIRED
     /* make sure a default max version is set */
     #ifndef __IPHONE_OS_VERSION_MAX_ALLOWED
-        #define __IPHONE_OS_VERSION_MAX_ALLOWED     __IPHONE_10_1
+        #define __IPHONE_OS_VERSION_MAX_ALLOWED     __IPHONE_10_2
     #endif
     /* make sure a valid min is set */
     #if __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_2_0
@@ -254,6 +254,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=2.0,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=2.0,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=2.0,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=2.0,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=2.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=2.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_2_1                    __attribute__((availability(ios,introduced=2.1)))
@@ -413,6 +419,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=2.1,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=2.1,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=2.1,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=2.1,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=2.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=2.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_2_2                    __attribute__((availability(ios,introduced=2.2)))
@@ -566,6 +578,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=2.2,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=2.2,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=2.2,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=2.2,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=2.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=2.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_3_0                    __attribute__((availability(ios,introduced=3.0)))
@@ -713,6 +731,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=3.0,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=3.0,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=3.0,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=3.0,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=3.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=3.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_3_1                    __attribute__((availability(ios,introduced=3.1)))
@@ -854,6 +878,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=3.1,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=3.1,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=3.1,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=3.1,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=3.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=3.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_3_2                    __attribute__((availability(ios,introduced=3.2)))
@@ -989,6 +1019,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=3.2,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=3.2,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=3.2,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=3.2,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=3.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=3.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_4_0                    __attribute__((availability(ios,introduced=4.0)))
@@ -1118,6 +1154,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=4.0,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=4.0,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=4.0,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=4.0,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=4.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=4.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_4_1                    __attribute__((availability(ios,introduced=4.1)))
@@ -1241,6 +1283,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=4.1,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=4.1,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=4.1,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=4.1,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=4.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=4.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_4_2                    __attribute__((availability(ios,introduced=4.2)))
@@ -1358,6 +1406,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=4.2,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=4.2,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=4.2,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=4.2,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=4.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=4.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_4_3                    __attribute__((availability(ios,introduced=4.3)))
@@ -1469,6 +1523,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=4.3,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=4.3,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=4.3,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=4.3,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=4.3)))
             #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=4.3)))
             #define __AVAILABILITY_INTERNAL__IPHONE_5_0                    __attribute__((availability(ios,introduced=5.0)))
@@ -1574,6 +1634,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=5.0,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=5.0,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=5.0,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=5.0,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=5.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=5.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_5_1                    __attribute__((availability(ios,introduced=5.1)))
@@ -1673,6 +1739,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=5.1,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=5.1,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=5.1,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=5.1,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=5.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=5.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_6_0                    __attribute__((availability(ios,introduced=6.0)))
@@ -1766,6 +1838,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=6.0,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=6.0,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=6.0,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=6.0,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=6.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=6.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_6_1                    __attribute__((availability(ios,introduced=6.1)))
@@ -1853,6 +1931,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=6.1,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=6.1,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=6.1,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=6.1,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=6.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=6.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_7_0                    __attribute__((availability(ios,introduced=7.0)))
@@ -1934,6 +2018,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=7.0,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=7.0,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=7.0,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=7.0,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=7.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=7.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_7_1                    __attribute__((availability(ios,introduced=7.1)))
@@ -2009,6 +2099,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=7.1,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=7.1,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=7.1,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=7.1,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=7.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=7.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_8_0                    __attribute__((availability(ios,introduced=8.0)))
@@ -2078,6 +2174,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=8.0,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=8.0,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=8.0,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=8.0,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=8.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=8.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_8_1                    __attribute__((availability(ios,introduced=8.1)))
@@ -2141,6 +2243,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=8.1,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=8.1,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=8.1,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=8.1,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=8.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=8.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_8_2                    __attribute__((availability(ios,introduced=8.2)))
@@ -2198,6 +2306,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=8.2,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=8.2,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=8.2,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=8.2,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=8.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=8.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_8_3                    __attribute__((availability(ios,introduced=8.3)))
@@ -2249,6 +2363,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=8.3,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=8.3,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=8.3,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=8.3,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=8.3)))
             #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=8.3)))
             #define __AVAILABILITY_INTERNAL__IPHONE_8_4                    __attribute__((availability(ios,introduced=8.4)))
@@ -2294,6 +2414,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=8.4,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=8.4,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=8.4,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=8.4,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=8.4)))
             #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=8.4)))
             #define __AVAILABILITY_INTERNAL__IPHONE_9_0                    __attribute__((availability(ios,introduced=9.0)))
@@ -2333,6 +2459,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=9.0,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=9.0,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=9.0,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=9.0,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=9.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=9.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_9_1                    __attribute__((availability(ios,introduced=9.1)))
@@ -2366,6 +2498,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=9.1,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=9.1,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=9.1,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=9.1,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=9.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=9.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_9_2                    __attribute__((availability(ios,introduced=9.2)))
@@ -2393,6 +2531,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=9.2,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=9.2,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=9.2,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=9.2,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=9.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=9.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_9_3                    __attribute__((availability(ios,introduced=9.3)))
@@ -2414,6 +2558,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=9.3,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=9.3,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=9.3,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=9.3,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=9.3)))
             #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=9.3)))
             #define __AVAILABILITY_INTERNAL__IPHONE_10_0                    __attribute__((availability(ios,introduced=10.0)))
@@ -2429,6 +2579,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=10.0,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=10.0,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=10.0,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=10.0,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=10.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=10.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_10_1                    __attribute__((availability(ios,introduced=10.1)))
@@ -2438,8 +2594,23 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=10.1,deprecated=10.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=10.1,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=10.1,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=10.1,deprecated=10.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=10.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=10.1)))
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2                    __attribute__((availability(ios,introduced=10.2)))
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2    __attribute__((availability(ios,introduced=10.2,deprecated=10.2)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=10.2,deprecated=10.2,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __attribute__((availability(ios,introduced=10.2,deprecated=10.2)))
+            #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=10.2)))
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=10.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_NA                               __attribute__((availability(ios,unavailable)))
             #define __AVAILABILITY_INTERNAL__IPHONE_NA_DEP__IPHONE_NA                __attribute__((availability(ios,unavailable)))
             #define __AVAILABILITY_INTERNAL__IPHONE_NA_DEP__IPHONE_NA_MSG(_msg)      __attribute__((availability(ios,unavailable)))
@@ -16980,6 +17151,1613 @@
             #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
             #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
         #endif
+        /* set up old style internal macros (up to 10.2) */
+        #if __IPHONE_OS_VERSION_MAX_ALLOWED < __IPHONE_10_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2                      __AVAILABILITY_INTERNAL_UNAVAILABLE
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_10_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2                      __AVAILABILITY_INTERNAL_WEAK_IMPORT
+        #else
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2                      __AVAILABILITY_INTERNAL_REGULAR
+        #endif
+        #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_NA           __AVAILABILITY_INTERNAL__IPHONE_10_2
+        #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_NA_MSG(_msg) __AVAILABILITY_INTERNAL__IPHONE_10_2
+        #if __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_2
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_3
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_4
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_0
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_1
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_9_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_2
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_9_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_9_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_3
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_10_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_10_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_10_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_10_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_10_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_10_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_10_0
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_10_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_10_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_10_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_10_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_10_1
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_10_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL__IPHONE_10_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_10_2
+        #else
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_2_DEP__IPHONE_10_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+        #endif
         /* set up internal macros (n/a) */
         #define __AVAILABILITY_INTERNAL__IPHONE_NA                               __AVAILABILITY_INTERNAL_UNAVAILABLE
         #define __AVAILABILITY_INTERNAL__IPHONE_NA_DEP__IPHONE_NA                __AVAILABILITY_INTERNAL_UNAVAILABLE
@@ -16991,7 +18769,7 @@
     #define __MAC_OS_X_VERSION_MIN_REQUIRED __ENVIRONMENT_MAC_OS_X_VERSION_MIN_REQUIRED__
     /* make sure a default max version is set */
     #ifndef __MAC_OS_X_VERSION_MAX_ALLOWED
-        #define __MAC_OS_X_VERSION_MAX_ALLOWED __MAC_10_12_1
+        #define __MAC_OS_X_VERSION_MAX_ALLOWED __MAC_10_12_2
     #endif
 
     #if defined(__has_attribute) && defined(__has_feature)
@@ -17112,6 +18890,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.0,deprecated=10.12.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_10_12_2    __attribute__((availability(macosx,introduced=10.0,deprecated=10.12.2)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.0,deprecated=10.12.2,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.0,deprecated=10.12.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.0)))
             #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.0)))
             #define __AVAILABILITY_INTERNAL__MAC_10_1                  __attribute__((availability(macosx,introduced=10.1)))
@@ -17223,6 +19007,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.1,deprecated=10.12.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_10_12_2    __attribute__((availability(macosx,introduced=10.1,deprecated=10.12.2)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.1,deprecated=10.12.2,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.1,deprecated=10.12.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.1)))
             #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.1)))
             #define __AVAILABILITY_INTERNAL__MAC_10_2                  __attribute__((availability(macosx,introduced=10.2)))
@@ -17328,6 +19118,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_2_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.2,deprecated=10.12.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_2_DEP__MAC_10_12_2    __attribute__((availability(macosx,introduced=10.2,deprecated=10.12.2)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_2_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.2,deprecated=10.12.2,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_2_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.2,deprecated=10.12.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_2_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.2)))
             #define __AVAILABILITY_INTERNAL__MAC_10_2_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.2)))
             #define __AVAILABILITY_INTERNAL__MAC_10_3                  __attribute__((availability(macosx,introduced=10.3)))
@@ -17427,6 +19223,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_3_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.3,deprecated=10.12.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_3_DEP__MAC_10_12_2    __attribute__((availability(macosx,introduced=10.3,deprecated=10.12.2)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_3_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.3,deprecated=10.12.2,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_3_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.3,deprecated=10.12.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_3_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.3)))
             #define __AVAILABILITY_INTERNAL__MAC_10_3_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.3)))
             #define __AVAILABILITY_INTERNAL__MAC_10_4                  __attribute__((availability(macosx,introduced=10.4)))
@@ -17520,6 +19322,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_4_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.4,deprecated=10.12.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_4_DEP__MAC_10_12_2    __attribute__((availability(macosx,introduced=10.4,deprecated=10.12.2)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_4_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.4,deprecated=10.12.2,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_4_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.4,deprecated=10.12.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_4_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.4)))
             #define __AVAILABILITY_INTERNAL__MAC_10_4_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.4)))
             #define __AVAILABILITY_INTERNAL__MAC_10_5                  __attribute__((availability(macosx,introduced=10.5)))
@@ -17607,6 +19415,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_5_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.5,deprecated=10.12.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_5_DEP__MAC_10_12_2    __attribute__((availability(macosx,introduced=10.5,deprecated=10.12.2)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_5_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.5,deprecated=10.12.2,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_5_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.5,deprecated=10.12.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_5_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.5)))
             #define __AVAILABILITY_INTERNAL__MAC_10_5_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.5)))
             #define __AVAILABILITY_INTERNAL__MAC_10_6                  __attribute__((availability(macosx,introduced=10.6)))
@@ -17688,6 +19502,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_6_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.6,deprecated=10.12.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_6_DEP__MAC_10_12_2    __attribute__((availability(macosx,introduced=10.6,deprecated=10.12.2)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_6_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.6,deprecated=10.12.2,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_6_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.6,deprecated=10.12.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_6_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.6)))
             #define __AVAILABILITY_INTERNAL__MAC_10_6_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.6)))
             #define __AVAILABILITY_INTERNAL__MAC_10_7                  __attribute__((availability(macosx,introduced=10.7)))
@@ -17763,6 +19583,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_7_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.7,deprecated=10.12.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_7_DEP__MAC_10_12_2    __attribute__((availability(macosx,introduced=10.7,deprecated=10.12.2)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_7_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.7,deprecated=10.12.2,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_7_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.7,deprecated=10.12.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_7_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.7)))
             #define __AVAILABILITY_INTERNAL__MAC_10_7_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.7)))
             #define __AVAILABILITY_INTERNAL__MAC_10_8                  __attribute__((availability(macosx,introduced=10.8)))
@@ -17832,6 +19658,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_8_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.8,deprecated=10.12.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_8_DEP__MAC_10_12_2    __attribute__((availability(macosx,introduced=10.8,deprecated=10.12.2)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_8_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.8,deprecated=10.12.2,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_8_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.8,deprecated=10.12.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_8_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.8)))
             #define __AVAILABILITY_INTERNAL__MAC_10_8_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.8)))
             #define __AVAILABILITY_INTERNAL__MAC_10_9                  __attribute__((availability(macosx,introduced=10.9)))
@@ -17895,6 +19727,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_9_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.9,deprecated=10.12.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_9_DEP__MAC_10_12_2    __attribute__((availability(macosx,introduced=10.9,deprecated=10.12.2)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_9_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.9,deprecated=10.12.2,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_9_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.9,deprecated=10.12.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_9_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.9)))
             #define __AVAILABILITY_INTERNAL__MAC_10_9_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.9)))
             #define __AVAILABILITY_INTERNAL__MAC_10_10                  __attribute__((availability(macosx,introduced=10.10)))
@@ -17952,6 +19790,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_10_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.10,deprecated=10.12.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_DEP__MAC_10_12_2    __attribute__((availability(macosx,introduced=10.10,deprecated=10.12.2)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_10_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.10,deprecated=10.12.2,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_10_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.10,deprecated=10.12.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_10_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.10)))
             #define __AVAILABILITY_INTERNAL__MAC_10_10_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.10)))
             #define __AVAILABILITY_INTERNAL__MAC_10_10_2                  __attribute__((availability(macosx,introduced=10.10.2)))
@@ -18003,6 +19847,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_10_2_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.10.2,deprecated=10.12.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_2_DEP__MAC_10_12_2    __attribute__((availability(macosx,introduced=10.10.2,deprecated=10.12.2)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_10_2_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.10.2,deprecated=10.12.2,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_10_2_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.10.2,deprecated=10.12.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_10_2_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.10.2)))
             #define __AVAILABILITY_INTERNAL__MAC_10_10_2_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.10.2)))
             #define __AVAILABILITY_INTERNAL__MAC_10_10_3                  __attribute__((availability(macosx,introduced=10.10.3)))
@@ -18048,6 +19898,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_10_3_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.10.3,deprecated=10.12.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_3_DEP__MAC_10_12_2    __attribute__((availability(macosx,introduced=10.10.3,deprecated=10.12.2)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_10_3_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.10.3,deprecated=10.12.2,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_10_3_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.10.3,deprecated=10.12.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_10_3_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.10.3)))
             #define __AVAILABILITY_INTERNAL__MAC_10_10_3_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.10.3)))
             #define __AVAILABILITY_INTERNAL__MAC_10_11                  __attribute__((availability(macosx,introduced=10.11)))
@@ -18087,6 +19943,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_11_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11,deprecated=10.12.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_DEP__MAC_10_12_2    __attribute__((availability(macosx,introduced=10.11,deprecated=10.12.2)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_11_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11,deprecated=10.12.2,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_11_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11,deprecated=10.12.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_11_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.11)))
             #define __AVAILABILITY_INTERNAL__MAC_10_11_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.11)))
             #define __AVAILABILITY_INTERNAL__MAC_10_11_2                  __attribute__((availability(macosx,introduced=10.11.2)))
@@ -18120,6 +19982,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_11_2_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11.2,deprecated=10.12.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_2_DEP__MAC_10_12_2    __attribute__((availability(macosx,introduced=10.11.2,deprecated=10.12.2)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_11_2_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11.2,deprecated=10.12.2,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_11_2_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11.2,deprecated=10.12.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_11_2_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.11.2)))
             #define __AVAILABILITY_INTERNAL__MAC_10_11_2_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.11.2)))
             #define __AVAILABILITY_INTERNAL__MAC_10_11_3                  __attribute__((availability(macosx,introduced=10.11.3)))
@@ -18147,6 +20015,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_11_3_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11.3,deprecated=10.12.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_3_DEP__MAC_10_12_2    __attribute__((availability(macosx,introduced=10.11.3,deprecated=10.12.2)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_11_3_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11.3,deprecated=10.12.2,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_11_3_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11.3,deprecated=10.12.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_11_3_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.11.3)))
             #define __AVAILABILITY_INTERNAL__MAC_10_11_3_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.11.3)))
             #define __AVAILABILITY_INTERNAL__MAC_10_11_4                  __attribute__((availability(macosx,introduced=10.11.4)))
@@ -18168,6 +20042,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11.4,deprecated=10.12.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_10_12_2    __attribute__((availability(macosx,introduced=10.11.4,deprecated=10.12.2)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11.4,deprecated=10.12.2,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11.4,deprecated=10.12.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.11.4)))
             #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.11.4)))
             #define __AVAILABILITY_INTERNAL__MAC_10_12                  __attribute__((availability(macosx,introduced=10.12)))
@@ -18183,6 +20063,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.12,deprecated=10.12.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_10_12_2    __attribute__((availability(macosx,introduced=10.12,deprecated=10.12.2)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.12,deprecated=10.12.2,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.12,deprecated=10.12.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.12)))
             #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.12)))
             #define __AVAILABILITY_INTERNAL__MAC_10_12_1                  __attribute__((availability(macosx,introduced=10.12.1)))
@@ -18192,8 +20078,23 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.12.1,deprecated=10.12.1)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_10_12_2    __attribute__((availability(macosx,introduced=10.12.1,deprecated=10.12.2)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.12.1,deprecated=10.12.2,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.12.1,deprecated=10.12.2)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.12.1)))
             #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.12.1)))
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_2                  __attribute__((availability(macosx,introduced=10.12.2)))
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_2_DEP__MAC_10_12_2    __attribute__((availability(macosx,introduced=10.12.2,deprecated=10.12.2)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_12_2_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.12.2,deprecated=10.12.2,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_12_2_DEP__MAC_10_12_2_MSG(_msg)    __attribute__((availability(macosx,introduced=10.12.2,deprecated=10.12.2)))
+            #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_2_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.12.2)))
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_2_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.12.2)))
             #define __AVAILABILITY_INTERNAL__MAC_NA                        __attribute__((availability(macosx,unavailable)))
             #define __AVAILABILITY_INTERNAL__MAC_NA_DEP__MAC_NA            __attribute__((availability(macosx,unavailable)))
             #define __AVAILABILITY_INTERNAL__MAC_NA_DEP__MAC_NA_MSG(_msg)  __attribute__((availability(macosx,unavailable)))
@@ -18202,6 +20103,13 @@
 
     #ifndef __AVAILABILITY_INTERNAL__MAC_10_0
         /* use old style attributes */
+        #if __MAC_OS_X_VERSION_MAX_ALLOWED < __MAC_10_12_2
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_2        __AVAILABILITY_INTERNAL_UNAVAILABLE
+        #elif __MAC_OS_X_VERSION_MIN_REQUIRED < __MAC_10_12_2
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_2        __AVAILABILITY_INTERNAL_WEAK_IMPORT
+        #else
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_2        __AVAILABILITY_INTERNAL_REGULAR
+        #endif
         #if __MAC_OS_X_VERSION_MAX_ALLOWED < __MAC_10_12_1
             #define __AVAILABILITY_INTERNAL__MAC_10_12_1        __AVAILABILITY_INTERNAL_UNAVAILABLE
         #elif __MAC_OS_X_VERSION_MIN_REQUIRED < __MAC_10_12_1
@@ -19146,6 +21054,89 @@
             #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL__MAC_10_12_1
             #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_12_1
         #endif
+        #if __MAC_OS_X_VERSION_MIN_REQUIRED >= __MAC_10_12_2
+            #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_2_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_2_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_3_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_3_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_4_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_4_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_5_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_5_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_6_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_6_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_7_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_7_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_8_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_8_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_9_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_9_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_2_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_2_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_3_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_3_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_2_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_2_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_3_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_3_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_2_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_2_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+        #else
+            #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL__MAC_10_0
+            #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_0
+            #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL__MAC_10_1
+            #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_1
+            #define __AVAILABILITY_INTERNAL__MAC_10_2_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL__MAC_10_2
+            #define __AVAILABILITY_INTERNAL__MAC_10_2_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_2
+            #define __AVAILABILITY_INTERNAL__MAC_10_3_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL__MAC_10_3
+            #define __AVAILABILITY_INTERNAL__MAC_10_3_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_3
+            #define __AVAILABILITY_INTERNAL__MAC_10_4_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL__MAC_10_4
+            #define __AVAILABILITY_INTERNAL__MAC_10_4_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_4
+            #define __AVAILABILITY_INTERNAL__MAC_10_5_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL__MAC_10_5
+            #define __AVAILABILITY_INTERNAL__MAC_10_5_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_5
+            #define __AVAILABILITY_INTERNAL__MAC_10_6_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL__MAC_10_6
+            #define __AVAILABILITY_INTERNAL__MAC_10_6_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_6
+            #define __AVAILABILITY_INTERNAL__MAC_10_7_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL__MAC_10_7
+            #define __AVAILABILITY_INTERNAL__MAC_10_7_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_7
+            #define __AVAILABILITY_INTERNAL__MAC_10_8_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL__MAC_10_8
+            #define __AVAILABILITY_INTERNAL__MAC_10_8_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_8
+            #define __AVAILABILITY_INTERNAL__MAC_10_9_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL__MAC_10_9
+            #define __AVAILABILITY_INTERNAL__MAC_10_9_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_9
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL__MAC_10_10
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_10
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_2_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL__MAC_10_10_2
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_2_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_10_2
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_3_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL__MAC_10_10_3
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_3_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_10_3
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL__MAC_10_11
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_11
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_2_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL__MAC_10_11_2
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_2_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_11_2
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_3_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL__MAC_10_11_3
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_3_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_11_3
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL__MAC_10_11_4
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_11_4
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL__MAC_10_12
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_12
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL__MAC_10_12_1
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_12_1
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_2_DEP__MAC_10_12_2              __AVAILABILITY_INTERNAL__MAC_10_12_2
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_2_DEP__MAC_10_12_2_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_12_2
+        #endif
         #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_NA             __AVAILABILITY_INTERNAL__MAC_10_0
         #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_NA_MSG(_msg)   __AVAILABILITY_INTERNAL__MAC_10_0
         #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_NA             __AVAILABILITY_INTERNAL__MAC_10_1
@@ -19184,6 +21175,8 @@
         #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_NA_MSG(_msg)   __AVAILABILITY_INTERNAL__MAC_10_12
         #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_NA             __AVAILABILITY_INTERNAL__MAC_10_12_1
         #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_NA_MSG(_msg)   __AVAILABILITY_INTERNAL__MAC_10_12_1
+        #define __AVAILABILITY_INTERNAL__MAC_10_12_2_DEP__MAC_NA             __AVAILABILITY_INTERNAL__MAC_10_12_2
+        #define __AVAILABILITY_INTERNAL__MAC_10_12_2_DEP__MAC_NA_MSG(_msg)   __AVAILABILITY_INTERNAL__MAC_10_12_2
         #define __AVAILABILITY_INTERNAL__MAC_NA_DEP__MAC_NA               __AVAILABILITY_INTERNAL_UNAVAILABLE
         #define __AVAILABILITY_INTERNAL__MAC_NA_DEP__MAC_NA_MSG(_msg)     __AVAILABILITY_INTERNAL_UNAVAILABLE
     #endif
@@ -19250,7 +21243,16 @@
 #define __API_DEPRECATED_MSG5(msg,x,y,z,t) __API_DEPRECATED_MSG4(msg,x,y,z) __API_D(msg,t)
 #define __API_DEPRECATED_MSG_GET_MACRO(_1,_2,_3,_4,_5,NAME,...) NAME
 
-#define __API_R(rep,x) __attribute__((availability(__API_DEPRECATED_PLATFORM_##x,replacement=rep)))
+#if defined(__has_feature)
+    #if __has_feature(attribute_availability_with_replacement)
+        #define __API_R(rep,x) __attribute__((availability(__API_DEPRECATED_PLATFORM_##x,replacement=rep)))
+    #else
+        #define __API_R(rep,x) __attribute__((availability(__API_DEPRECATED_PLATFORM_##x)))
+    #endif
+#else
+    #define __API_R(rep,x) __attribute__((availability(__API_DEPRECATED_PLATFORM_##x)))
+#endif
+
 #define __API_DEPRECATED_REP2(rep,x) __API_R(rep,x)
 #define __API_DEPRECATED_REP3(rep,x,y) __API_R(rep,x) __API_R(rep,y)
 #define __API_DEPRECATED_REP4(rep,x,y,z)  __API_DEPRECATED_REP3(rep,x,y) __API_R(rep,z)
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityMacros.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityMacros.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityMacros.h	2016-09-20 00:11:19.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityMacros.h	2016-10-22 20:20:56.000000000 +0200
@@ -108,6 +108,7 @@
 #define MAC_OS_X_VERSION_10_11_4    101104
 #define MAC_OS_X_VERSION_10_12      101200
 #define MAC_OS_X_VERSION_10_12_1    101201
+#define MAC_OS_X_VERSION_10_12_2    101202
 
 /* 
  * If min OS not specified, assume 10.4 for intel
@@ -131,13 +132,13 @@
 #endif
 
 /*
- * if max OS not specified, assume larger of (10.12.1, min)
+ * if max OS not specified, assume larger of (10.12.2, min)
  */
 #ifndef MAC_OS_X_VERSION_MAX_ALLOWED
-    #if MAC_OS_X_VERSION_MIN_REQUIRED > MAC_OS_X_VERSION_10_12_1
+    #if MAC_OS_X_VERSION_MIN_REQUIRED > MAC_OS_X_VERSION_10_12_2
         #define MAC_OS_X_VERSION_MAX_ALLOWED MAC_OS_X_VERSION_MIN_REQUIRED
     #else
-        #define MAC_OS_X_VERSION_MAX_ALLOWED MAC_OS_X_VERSION_10_12_1
+        #define MAC_OS_X_VERSION_MAX_ALLOWED MAC_OS_X_VERSION_10_12_2
     #endif
 #endif
 
@@ -3398,6 +3399,315 @@
 #endif
 
 
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_12_2_AND_LATER
+ * 
+ * Used on declarations introduced in Mac OS X 10.12.2 
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_2_AND_LATER     __OSX_AVAILABLE_STARTING(__MAC_10_12_2, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MAX_ALLOWED < MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_2_AND_LATER     UNAVAILABLE_ATTRIBUTE
+#elif MAC_OS_X_VERSION_MIN_REQUIRED < MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_2_AND_LATER     WEAK_IMPORT_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_2_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_12_2_AND_LATER_BUT_DEPRECATED
+ *
+ * Used on declarations introduced in Mac OS X 10.12.2,
+ * and deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_2_AND_LATER_BUT_DEPRECATED     __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_12_2, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_2_AND_LATER_BUT_DEPRECATED    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_2_AND_LATER_BUT_DEPRECATED    AVAILABLE_MAC_OS_X_VERSION_10_12_2_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_0_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2
+ *
+ * Used on declarations introduced in Mac OS X 10.0,
+ * but later deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_0_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_0_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_0_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    AVAILABLE_MAC_OS_X_VERSION_10_0_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_1_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2
+ *
+ * Used on declarations introduced in Mac OS X 10.1,
+ * but later deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_1_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_1_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_1_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    AVAILABLE_MAC_OS_X_VERSION_10_1_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2
+ *
+ * Used on declarations introduced in Mac OS X 10.2,
+ * but later deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_2, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    AVAILABLE_MAC_OS_X_VERSION_10_2_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2
+ *
+ * Used on declarations introduced in Mac OS X 10.3,
+ * but later deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_3, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    AVAILABLE_MAC_OS_X_VERSION_10_3_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2
+ *
+ * Used on declarations introduced in Mac OS X 10.4,
+ * but later deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_4, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2
+ *
+ * Used on declarations introduced in Mac OS X 10.5,
+ * but later deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_5, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_6_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2
+ *
+ * Used on declarations introduced in Mac OS X 10.6,
+ * but later deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_6_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_6, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_6_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_6_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    AVAILABLE_MAC_OS_X_VERSION_10_6_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_7_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2
+ *
+ * Used on declarations introduced in Mac OS X 10.7,
+ * but later deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_7_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_7_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_7_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    AVAILABLE_MAC_OS_X_VERSION_10_7_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_8_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2
+ *
+ * Used on declarations introduced in Mac OS X 10.8,
+ * but later deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_8_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_8, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_8_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_8_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    AVAILABLE_MAC_OS_X_VERSION_10_8_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_9_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2
+ *
+ * Used on declarations introduced in Mac OS X 10.9,
+ * but later deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_9_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_9, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_9_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_9_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    AVAILABLE_MAC_OS_X_VERSION_10_9_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_10_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2
+ *
+ * Used on declarations introduced in Mac OS X 10.10,
+ * but later deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_10_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_10, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_10_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_10_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    AVAILABLE_MAC_OS_X_VERSION_10_10_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_10_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2
+ *
+ * Used on declarations introduced in Mac OS X 10.10.2,
+ * but later deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_10_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_10_2, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_10_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_10_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    AVAILABLE_MAC_OS_X_VERSION_10_10_2_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_10_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2
+ *
+ * Used on declarations introduced in Mac OS X 10.10.3,
+ * but later deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_10_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_10_3, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_10_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_10_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    AVAILABLE_MAC_OS_X_VERSION_10_10_3_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_11_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2
+ *
+ * Used on declarations introduced in Mac OS X 10.11,
+ * but later deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_11, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    AVAILABLE_MAC_OS_X_VERSION_10_11_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_11_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2
+ *
+ * Used on declarations introduced in Mac OS X 10.11.2,
+ * but later deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_11_2, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    AVAILABLE_MAC_OS_X_VERSION_10_11_2_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_11_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2
+ *
+ * Used on declarations introduced in Mac OS X 10.11.3,
+ * but later deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_11_3, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    AVAILABLE_MAC_OS_X_VERSION_10_11_3_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_11_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2
+ *
+ * Used on declarations introduced in Mac OS X 10.11.4,
+ * but later deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_11_4, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    AVAILABLE_MAC_OS_X_VERSION_10_11_4_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_12_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2
+ *
+ * Used on declarations introduced in Mac OS X 10.12,
+ * but later deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_12, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    AVAILABLE_MAC_OS_X_VERSION_10_12_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_12_1_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2
+ *
+ * Used on declarations introduced in Mac OS X 10.12.1,
+ * but later deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_1_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_12_1, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_1_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_1_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2    AVAILABLE_MAC_OS_X_VERSION_10_12_1_AND_LATER
+#endif
+
+/*
+ * DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2_AND_LATER
+ *
+ * Used on types deprecated in Mac OS X 10.12.2
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2_AND_LATER    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12_2, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_2
+    #define DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2_AND_LATER    DEPRECATED_ATTRIBUTE
+#else
+    #define DEPRECATED_IN_MAC_OS_X_VERSION_10_12_2_AND_LATER
+#endif
+
+
 
 
 #endif  /* __AVAILABILITYMACROS__ */
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOWorkLoop.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOWorkLoop.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOWorkLoop.h	2016-09-30 03:22:00.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOWorkLoop.h	2016-10-23 23:48:33.000000000 +0200
@@ -143,9 +143,6 @@
     struct ExpansionData {
 	IOOptionBits options;
 	IOEventSource *passiveEventChain;
-#if DEBUG
-	void * allocationBacktrace[16];
-#endif /* DEBUG */
 #if IOKITSTATS
 	struct IOWorkLoopCounter *counter;
 #else
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/bluetooth/BluetoothAssignedNumbers.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/bluetooth/BluetoothAssignedNumbers.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/bluetooth/BluetoothAssignedNumbers.h	2016-10-08 04:49:44.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/bluetooth/BluetoothAssignedNumbers.h	2016-10-24 00:26:16.000000000 +0200
@@ -659,7 +659,7 @@
 
 // HCI Versions
 
-enum BluetoothHCIVersions
+typedef enum BluetoothHCIVersions
 {
 	kBluetoothHCIVersionCoreSpecification1_0b												=	0x00,
 	kBluetoothHCIVersionCoreSpecification1_1												=	0x01,
@@ -670,12 +670,12 @@
 	kBluetoothHCIVersionCoreSpecification4_0												=	0x06,
     kBluetoothHCIVersionCoreSpecification4_1												=	0x07,
     kBluetoothHCIVersionCoreSpecification4_2												=	0x08
-};
+} BluetoothHCIVersions;
 
 
 // LMP Versions
 
-enum BluetoothLMPVersions
+typedef enum BluetoothLMPVersions
 {
 	kBluetoothLMPVersionCoreSpecification1_0b												=	0x00,
 	kBluetoothLMPVersionCoreSpecification1_1												=	0x01,
@@ -686,7 +686,7 @@
 	kBluetoothLMPVersionCoreSpecification4_0												=	0x06,
 	kBluetoothLMPVersionCoreSpecification4_1												=	0x07,
     kBluetoothLMPVersionCoreSpecification4_2												=	0x08
-};
+} BluetoothLMPVersions;
 
 #ifdef	__cplusplus
 	}
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IODisplay.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IODisplay.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IODisplay.h	2016-10-08 04:23:33.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IODisplay.h	2016-10-24 00:21:33.000000000 +0200
@@ -33,6 +33,8 @@
 extern const OSSymbol * gIODisplayMinValueKey;
 extern const OSSymbol * gIODisplayMaxValueKey;
 
+extern const OSSymbol * gIODisplayBrightnessProbeKey;
+extern const OSSymbol * gIODisplayLinearBrightnessProbeKey;
 extern const OSSymbol * gIODisplayContrastKey;
 extern const OSSymbol * gIODisplayBrightnessKey;
 extern const OSSymbol * gIODisplayLinearBrightnessKey;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IOGraphicsTypes.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IOGraphicsTypes.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IOGraphicsTypes.h	2016-10-08 04:23:33.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IOGraphicsTypes.h	2016-10-24 00:21:33.000000000 +0200
@@ -282,7 +282,8 @@
     kIOWSAA_Transactional       = 0x10,  // If this bit is present, transition is to/from transactional operation model.
     // These attributes are internal
     kIOWSAA_DeferStart          = 0x100,
-    kIOWSAA_DeferEnd            = 0x200
+    kIOWSAA_DeferEnd            = 0x200,
+    kIOWSAA_Reserved            = 0xF0000000
 };
 
 // values for kIOMirrorAttribute
@@ -1327,6 +1328,8 @@
 #define kIODisplayMinValueKey           "min"
 #define kIODisplayMaxValueKey           "max"
 
+#define kIODisplayBrightnessProbeKey        "brightness-probe"
+#define kIODisplayLinearBrightnessProbeKey  "linear-brightness-probe"
 #define kIODisplayBrightnessKey             "brightness"
 #define kIODisplayLinearBrightnessKey       "linear-brightness"
 #define kIODisplayUsableLinearBrightnessKey "usable-linear-brightness"
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDEventService.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDEventService.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDEventService.h	2016-10-06 05:59:49.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDEventService.h	2016-10-24 00:28:50.000000000 +0200
@@ -70,13 +70,6 @@
     kHIDDispatchOptionKeyboardNoRepeat                  = (1<<0)
 };
 
-enum
-{
-    kHIDShutdownDebugModeStackshots = 1,
-    kHIDShutdownDebugModePanic,
-    kHIDShutdownDebugModeDisabled
-};
-
 
 class IOHIDEventService;
 class   IOHIDPointing;
@@ -152,10 +145,6 @@
                 IOTimerEventSource *    nmiTimer;
                 UInt32                  stackshotHeld;
                 IOTimerEventSource *    stackshotTimer;
-                UInt32                  shutdownDebugMode;
-                UInt32                  shutdownDebugKeyMask;
-                UInt32                  shutdownDebugDelay;
-                IOTimerEventSource *    shutdownDebugTimer;
             } debug;
             bool                    swapISO;
 #else
@@ -226,12 +215,6 @@
     void                    debuggerTimerCallback(IOTimerEventSource *sender);
 
     void                    stackshotTimerCallback(IOTimerEventSource *sender);
-
-#if TARGET_OS_IPHONE
-    void                    forcedShutdownDebugTimerCallback(IOTimerEventSource *sender);
-    void                    forcedShutdownDebugInit();
-  
-#endif
 #endif
     
     void                    multiAxisTimerCallback(IOTimerEventSource *sender);
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDUtility.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDUtility.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDUtility.h	2016-10-06 05:59:49.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDUtility.h	2016-10-24 00:28:50.000000000 +0200
@@ -67,6 +67,14 @@
       }
       return result;
     }
+    bool isTopRow () const {
+        bool result = false;
+        if ((usagePage() == kHIDPage_KeyboardOrKeypad) &&
+            (((usage() >= kHIDUsage_Keyboard1) && (usage() <= kHIDUsage_Keyboard0)) || (usage() == kHIDUsage_KeyboardHyphen) || (usage() == kHIDUsage_KeyboardDeleteOrBackspace))) {
+            result = true;
+        }
+        return result;
+    }
 };
 
 struct KeyAttribute {
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/scsi/SCSICmds_INQUIRY_Definitions.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/scsi/SCSICmds_INQUIRY_Definitions.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/scsi/SCSICmds_INQUIRY_Definitions.h	2016-09-30 04:04:47.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/scsi/SCSICmds_INQUIRY_Definitions.h	2016-10-24 00:50:50.000000000 +0200
@@ -630,6 +630,7 @@
 */
 #define kIOPropertySCSIProductRevisionLevel			"Product Revision Level"
 
+#ifndef __OPEN_SOURCE__
 
 /*!
 @enum INQUIRY Page Codes
@@ -649,6 +650,10 @@
 Page Code B1h.
 @constant kINQUIRY_PageB2_PageCode
 Page Code B2h.
+@constant kINQUIRY_PageC0_PageCode
+Page Code C0h.
+@constant kINQUIRY_PageC1_PageCode
+Page Code C1h.
 */
 enum
 {
@@ -658,8 +663,44 @@
 	kINQUIRY_Page89_PageCode				= 0x89,
 	kINQUIRY_PageB0_PageCode				= 0xB0,
 	kINQUIRY_PageB1_PageCode				= 0xB1,
-	kINQUIRY_PageB2_PageCode				= 0xB2
-};	
+	kINQUIRY_PageB2_PageCode				= 0xB2,
+	kINQUIRY_PageC0_PageCode				= 0xC0,
+	kINQUIRY_PageC1_PageCode				= 0xC1
+};
+
+#else
+
+/*!
+ @enum INQUIRY Page Codes
+ @discussion INQUIRY Page Codes to be used when EVPD is set in the
+ INQUIRY command.
+ @constant kINQUIRY_Page00_PageCode
+ Page Code 00h.
+ @constant kINQUIRY_Page80_PageCode
+ Page Code 80h.
+ @constant kINQUIRY_Page83_PageCode
+ Page Code 83h.
+ @constant kINQUIRY_Page89_PageCode
+ Page Code 89h.
+ @constant kINQUIRY_PageB0_PageCode
+ Page Code B0h.
+ @constant kINQUIRY_PageB1_PageCode
+ Page Code B1h.
+ @constant kINQUIRY_PageB2_PageCode
+ Page Code B2h.
+ */
+enum
+{
+    kINQUIRY_Page00_PageCode				= 0x00,
+    kINQUIRY_Page80_PageCode				= 0x80,
+    kINQUIRY_Page83_PageCode				= 0x83,
+    kINQUIRY_Page89_PageCode				= 0x89,
+    kINQUIRY_PageB0_PageCode				= 0xB0,
+    kINQUIRY_PageB1_PageCode				= 0xB1,
+    kINQUIRY_PageB2_PageCode				= 0xB2,
+};
+
+#endif /* __OPEN_SOURCE__ */
 
 
 /*!
@@ -1090,6 +1131,74 @@
 
 #pragma pack(pop)
 
+#ifndef __OPEN_SOURCE__
+
+#pragma pack(push, 1)
+
+enum
+{
+	kC0DataMaxStringLen = 32,
+};
+
+typedef struct  SCSICmd_INQUIRY_PageCx_Header
+{
+
+	UInt8		PERIPHERAL_DEVICE_TYPE; 	// 7-5 = Qualifier. 4-0 = Device type.
+	UInt8		PAGE_CODE;					// Must be equal to C0h or C1h
+	UInt8		RESERVED;
+	UInt8		PAGE_LENGTH;
+
+} SCSICmd_INQUIRY_PAGECx_Header;
+
+/*!
+ @struct SCSICmd_INQUIRY_PageC0_Data
+ @discussion INQUIRY Page C0h data as defined in Apple Target
+ Disk Mode specification. This is a vendor specific data structure.
+ This section contains all structures and definitions used by 
+ the INQUIRY command in response to a request for page C0h.
+ */
+
+typedef struct SCSICmd_INQUIRY_PageC0_Data
+{
+
+	SCSICmd_INQUIRY_PAGECx_Header	fHeader;
+	UInt8							fTdmPageVersion;
+	UInt8							fTdmProtocolVersion;
+	UInt8							fReserved1;
+	UInt8							fReserved2;
+	UInt8							fMacModelId[kC0DataMaxStringLen];
+	UInt8							fSerialNumber[kC0DataMaxStringLen];
+	UInt32							fMaxReadSize;
+	UInt32							fMaxWriteSize;
+	UInt32							fNativeBlockSize;
+	UInt64							fFeatures;
+	UInt64							fWorkArounds;
+
+} SCSICmd_INQUIRY_PageC0_Data;
+
+/*!
+ @struct SCSICmd_INQUIRY_PageC1_Data
+ @discussion INQUIRY Page C1h data as defined in Apple Target
+ Disk Mode specification. This is a vendor specific data structure.
+ This section contains all structures and definitions used by
+ the INQUIRY command in response to a request for page C1h.
+ */
+
+typedef struct SCSICmd_INQUIRY_PageC1_Data
+{
+
+	SCSICmd_INQUIRY_PAGECx_Header	fHeader;
+	UInt8							fTdmPowerRequirementsPageVersion;
+	UInt8							fReserved1;
+	UInt16							fReserved2;
+	UInt32							fPowerRequired;
+
+} SCSICmd_INQUIRY_PageC1_Data;
+
+#pragma pack(pop)
+
+#endif /* __OPEN_SOURCE__ */
+
 /*!
 @define kIOPropertySATVendorIdentification
 Vendor Identification of the SATL.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/c++/OSData.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/c++/OSData.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/c++/OSData.h	2016-09-30 03:21:47.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/c++/OSData.h	2016-10-23 23:48:22.000000000 +0200
@@ -734,6 +734,7 @@
 private:
     virtual void setDeallocFunction(DeallocFunction func);
     OSMetaClassDeclareReservedUsed(OSData, 0);
+    bool isSerializable(void);
 
 private:
     OSMetaClassDeclareReservedUnused(OSData, 1);
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/version.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/version.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/version.h	2016-09-30 03:21:54.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/version.h	2016-10-23 23:48:29.000000000 +0200
@@ -35,7 +35,7 @@
 /* VERSION_MINOR, version_minor is an integer that represents the minor version
  * of the kernel
  */
-#define VERSION_MINOR		1
+#define VERSION_MINOR		3
 
 /* VERSION_VARIANT, version_variant is a string that contains the revision,
  * stage, and prerelease level of the kernel
@@ -63,7 +63,7 @@
 #define	OSTYPE		"Darwin"
 
 /* OSRELEASE, osrelease, is a string as returned by uname -r */
-#define OSRELEASE	"16.1.0"
+#define OSRELEASE	"16.3.0"
 
 #ifndef ASSEMBLER
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/mach_time.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/mach_time.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/mach_time.h	2016-09-30 03:22:05.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/mach_time.h	2016-10-23 23:48:40.000000000 +0200
@@ -51,17 +51,13 @@
 /*
  * like mach_absolute_time, but advances during sleep
  */
-__OSX_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0)
-__TVOS_AVAILABLE(__TVOS_10_0)
-__WATCHOS_AVAILABLE(__WATCHOS_3_0)
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0)
 uint64_t			mach_continuous_time(void);
 
 /*
  * like mach_approximate_time, but advances during sleep
  */
-__OSX_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0)
-__TVOS_AVAILABLE(__TVOS_10_0)
-__WATCHOS_AVAILABLE(__WATCHOS_3_0)
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0)
 uint64_t			mach_continuous_approximate_time(void);
 
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/vm_statistics.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/vm_statistics.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/vm_statistics.h	2016-09-30 03:22:08.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/vm_statistics.h	2016-10-23 23:48:44.000000000 +0200
@@ -436,8 +436,6 @@
 /* DHMM data */
 #define VM_MEMORY_DHMM 84
 
-/* memory needed for DFR related actions */
-#define VM_MEMORY_DFR 85
 
 /* memory allocated by SceneKit.framework */
 #define VM_MEMORY_SCENEKIT 86
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_policy.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_policy.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_policy.h	2016-09-30 03:21:46.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_policy.h	2016-10-23 23:48:22.000000000 +0200
@@ -6589,7 +6589,7 @@
 struct mac_policy_conf {
 	const char		*mpc_name;		/** policy name */
 	const char		*mpc_fullname;		/** full name */
-	const char		**mpc_labelnames;	/** managed label namespaces */
+	char const * const *mpc_labelnames;	/** managed label namespaces */
 	unsigned int		 mpc_labelname_count;	/** number of managed label namespaces */
 	struct mac_policy_ops	*mpc_ops;		/** operation vector */
 	int			 mpc_loadtime_flags;	/** load time flags */
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h	2016-09-30 03:22:38.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h	2016-10-23 23:49:17.000000000 +0200
@@ -559,6 +559,7 @@
 #define DKIO_NOCACHE	0x80
 #define DKIO_TIER_MASK	0xF00
 #define DKIO_TIER_SHIFT	8
+#define DKIO_TIER_UPGRADE 0x1000
 
 /* Kernel Debug Sub Classes for Applications (DBG_APPS) */
 #define DBG_APP_LOGINWINDOW     0x03
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h	2016-09-30 03:22:43.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h	2016-10-23 23:49:21.000000000 +0200
@@ -29,7 +29,7 @@
  * System call switch table.
  *
  * DO NOT EDIT-- this file is automatically generated.
- * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3789.21.3/bsd/kern/syscalls.master
+ * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3789.30.76/bsd/kern/syscalls.master
  */
 
 #ifndef _SYS_SYSCALL_H_
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h	2016-09-30 03:22:43.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h	2016-10-23 23:49:21.000000000 +0200
@@ -29,7 +29,7 @@
  * System call switch table.
  *
  * DO NOT EDIT-- this file is automatically generated.
- * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3789.21.3/bsd/kern/syscalls.master
+ * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3789.30.76/bsd/kern/syscalls.master
  */
 
 #ifndef _SYS_SYSPROTO_H_

```