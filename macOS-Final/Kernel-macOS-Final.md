#Kernel.framework

``` diff
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/Availability.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/Availability.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/Availability.h	2016-07-30 17:00:56.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/Availability.h	2016-09-19 18:11:22.000000000 -0400
@@ -134,6 +134,7 @@
 #define __MAC_10_11_3       101103
 #define __MAC_10_11_4       101104
 #define __MAC_10_12         101200
+#define __MAC_10_12_1       101201
 /* __MAC_NA is not defined to a value but is uses as a token by macros to indicate that the API is unavailable */
 
 #define __IPHONE_2_0      20000
@@ -162,16 +163,19 @@
 #define __IPHONE_9_2      90200
 #define __IPHONE_9_3      90300
 #define __IPHONE_10_0    100000
+#define __IPHONE_10_1    100100
 /* __IPHONE_NA is not defined to a value but is uses as a token by macros to indicate that the API is unavailable */
 
 #define __TVOS_9_0        90000
 #define __TVOS_9_1        90100
 #define __TVOS_9_2        90200
 #define __TVOS_10_0      100000
+#define __TVOS_10_0_1    100001
 
 #define __WATCHOS_1_0     10000
 #define __WATCHOS_2_0     20000
 #define __WATCHOS_3_0     30000
+#define __WATCHOS_3_1     30100
 
 #include <AvailabilityInternal.h>
 
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityInternal.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityInternal.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityInternal.h	2016-07-30 17:00:52.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityInternal.h	2016-09-19 18:11:19.000000000 -0400
@@ -80,7 +80,7 @@
 #ifdef __IPHONE_OS_VERSION_MIN_REQUIRED
     /* make sure a default max version is set */
     #ifndef __IPHONE_OS_VERSION_MAX_ALLOWED
-        #define __IPHONE_OS_VERSION_MAX_ALLOWED     __IPHONE_10_0
+        #define __IPHONE_OS_VERSION_MAX_ALLOWED     __IPHONE_10_1
     #endif
     /* make sure a valid min is set */
     #if __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_2_0
@@ -248,6 +248,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=2.0,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=2.0,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=2.0,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=2.0,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=2.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=2.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_2_1                    __attribute__((availability(ios,introduced=2.1)))
@@ -401,6 +407,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=2.1,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=2.1,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=2.1,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=2.1,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=2.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=2.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_2_2                    __attribute__((availability(ios,introduced=2.2)))
@@ -548,6 +560,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=2.2,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=2.2,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=2.2,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=2.2,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=2.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=2.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_3_0                    __attribute__((availability(ios,introduced=3.0)))
@@ -689,6 +707,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=3.0,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=3.0,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=3.0,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=3.0,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=3.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=3.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_3_1                    __attribute__((availability(ios,introduced=3.1)))
@@ -824,6 +848,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=3.1,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=3.1,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=3.1,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=3.1,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=3.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=3.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_3_2                    __attribute__((availability(ios,introduced=3.2)))
@@ -953,6 +983,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=3.2,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=3.2,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=3.2,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=3.2,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=3.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=3.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_4_0                    __attribute__((availability(ios,introduced=4.0)))
@@ -1076,6 +1112,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=4.0,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=4.0,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=4.0,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=4.0,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=4.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=4.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_4_1                    __attribute__((availability(ios,introduced=4.1)))
@@ -1193,6 +1235,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=4.1,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=4.1,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=4.1,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=4.1,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=4.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=4.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_4_2                    __attribute__((availability(ios,introduced=4.2)))
@@ -1304,6 +1352,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=4.2,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=4.2,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=4.2,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=4.2,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=4.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=4.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_4_3                    __attribute__((availability(ios,introduced=4.3)))
@@ -1409,6 +1463,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=4.3,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=4.3,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=4.3,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=4.3,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=4.3)))
             #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=4.3)))
             #define __AVAILABILITY_INTERNAL__IPHONE_5_0                    __attribute__((availability(ios,introduced=5.0)))
@@ -1508,6 +1568,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=5.0,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=5.0,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=5.0,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=5.0,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=5.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=5.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_5_1                    __attribute__((availability(ios,introduced=5.1)))
@@ -1601,6 +1667,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=5.1,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=5.1,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=5.1,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=5.1,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=5.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=5.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_6_0                    __attribute__((availability(ios,introduced=6.0)))
@@ -1688,6 +1760,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=6.0,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=6.0,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=6.0,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=6.0,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=6.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=6.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_6_1                    __attribute__((availability(ios,introduced=6.1)))
@@ -1769,6 +1847,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=6.1,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=6.1,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=6.1,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=6.1,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=6.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=6.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_7_0                    __attribute__((availability(ios,introduced=7.0)))
@@ -1844,6 +1928,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=7.0,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=7.0,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=7.0,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=7.0,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=7.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=7.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_7_1                    __attribute__((availability(ios,introduced=7.1)))
@@ -1913,6 +2003,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=7.1,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=7.1,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=7.1,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=7.1,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=7.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=7.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_8_0                    __attribute__((availability(ios,introduced=8.0)))
@@ -1976,6 +2072,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=8.0,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=8.0,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=8.0,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=8.0,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=8.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=8.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_8_1                    __attribute__((availability(ios,introduced=8.1)))
@@ -2033,6 +2135,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=8.1,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=8.1,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=8.1,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=8.1,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=8.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=8.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_8_2                    __attribute__((availability(ios,introduced=8.2)))
@@ -2084,6 +2192,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=8.2,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=8.2,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=8.2,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=8.2,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=8.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=8.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_8_3                    __attribute__((availability(ios,introduced=8.3)))
@@ -2129,6 +2243,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=8.3,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=8.3,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=8.3,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=8.3,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=8.3)))
             #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=8.3)))
             #define __AVAILABILITY_INTERNAL__IPHONE_8_4                    __attribute__((availability(ios,introduced=8.4)))
@@ -2168,6 +2288,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=8.4,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=8.4,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=8.4,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=8.4,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=8.4)))
             #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=8.4)))
             #define __AVAILABILITY_INTERNAL__IPHONE_9_0                    __attribute__((availability(ios,introduced=9.0)))
@@ -2201,6 +2327,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=9.0,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=9.0,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=9.0,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=9.0,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=9.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=9.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_9_1                    __attribute__((availability(ios,introduced=9.1)))
@@ -2228,6 +2360,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=9.1,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=9.1,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=9.1,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=9.1,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=9.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=9.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_9_2                    __attribute__((availability(ios,introduced=9.2)))
@@ -2249,6 +2387,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=9.2,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=9.2,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=9.2,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=9.2,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=9.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=9.2)))
             #define __AVAILABILITY_INTERNAL__IPHONE_9_3                    __attribute__((availability(ios,introduced=9.3)))
@@ -2264,6 +2408,12 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=9.3,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=9.3,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=9.3,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=9.3,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=9.3)))
             #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=9.3)))
             #define __AVAILABILITY_INTERNAL__IPHONE_10_0                    __attribute__((availability(ios,introduced=10.0)))
@@ -2273,8 +2423,23 @@
             #else
                     #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_0_MSG(_msg)    __attribute__((availability(ios,introduced=10.0,deprecated=10.0)))
             #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=10.0,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=10.0,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=10.0,deprecated=10.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=10.0)))
             #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=10.0)))
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1                    __attribute__((availability(ios,introduced=10.1)))
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1    __attribute__((availability(ios,introduced=10.1,deprecated=10.1)))
+            #if __has_feature(attribute_availability_with_message)
+                    #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=10.1,deprecated=10.1,message=_msg)))
+            #else
+                    #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __attribute__((availability(ios,introduced=10.1,deprecated=10.1)))
+            #endif
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_NA               __attribute__((availability(ios,introduced=10.1)))
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_NA_MSG(_msg)     __attribute__((availability(ios,introduced=10.1)))
             #define __AVAILABILITY_INTERNAL__IPHONE_NA                               __attribute__((availability(ios,unavailable)))
             #define __AVAILABILITY_INTERNAL__IPHONE_NA_DEP__IPHONE_NA                __attribute__((availability(ios,unavailable)))
             #define __AVAILABILITY_INTERNAL__IPHONE_NA_DEP__IPHONE_NA_MSG(_msg)      __attribute__((availability(ios,unavailable)))
@@ -15319,6 +15484,1502 @@
             #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_0              __AVAILABILITY_INTERNAL_DEPRECATED
             #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_0_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
         #endif
+        /* set up old style internal macros (up to 10.1) */
+        #if __IPHONE_OS_VERSION_MAX_ALLOWED < __IPHONE_10_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1                      __AVAILABILITY_INTERNAL_UNAVAILABLE
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_10_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1                      __AVAILABILITY_INTERNAL_WEAK_IMPORT
+        #else
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1                      __AVAILABILITY_INTERNAL_REGULAR
+        #endif
+        #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_NA           __AVAILABILITY_INTERNAL__IPHONE_10_1
+        #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_NA_MSG(_msg) __AVAILABILITY_INTERNAL__IPHONE_10_1
+        #if __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_1
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_2_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_2_2
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_0
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_1
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_3_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_3_2
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_0
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_1
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_2
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_4_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_4_3
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_0
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_5_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_5_1
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_0
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_6_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_6_1
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_0
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_7_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_7_1
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_0
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_1
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_2
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_3
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_8_4
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_8_4
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_9_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_0
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_9_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_1
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_9_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_9_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_9_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_9_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_9_2
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_2
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_9_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_9_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_9_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_9_3
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_9_3
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_10_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_10_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_10_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_10_0
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_10_0
+        #elif __IPHONE_OS_VERSION_MIN_REQUIRED < __IPHONE_10_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_REGULAR
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL__IPHONE_10_1
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL__IPHONE_10_1
+        #else
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_2_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_3_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_4_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_5_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_6_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_7_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_8_4_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_2_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_9_3_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_0_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__IPHONE_10_1_DEP__IPHONE_10_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+        #endif
         /* set up internal macros (n/a) */
         #define __AVAILABILITY_INTERNAL__IPHONE_NA                               __AVAILABILITY_INTERNAL_UNAVAILABLE
         #define __AVAILABILITY_INTERNAL__IPHONE_NA_DEP__IPHONE_NA                __AVAILABILITY_INTERNAL_UNAVAILABLE
@@ -15330,7 +16991,7 @@
     #define __MAC_OS_X_VERSION_MIN_REQUIRED __ENVIRONMENT_MAC_OS_X_VERSION_MIN_REQUIRED__
     /* make sure a default max version is set */
     #ifndef __MAC_OS_X_VERSION_MAX_ALLOWED
-        #define __MAC_OS_X_VERSION_MAX_ALLOWED __MAC_10_12
+        #define __MAC_OS_X_VERSION_MAX_ALLOWED __MAC_10_12_1
     #endif
 
     #if defined(__has_attribute) && defined(__has_feature)
@@ -15445,6 +17106,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_10_12_MSG(_msg)    __attribute__((availability(macosx,introduced=10.0,deprecated=10.12)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_10_12_1    __attribute__((availability(macosx,introduced=10.0,deprecated=10.12.1)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.0,deprecated=10.12.1,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.0,deprecated=10.12.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.0)))
             #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.0)))
             #define __AVAILABILITY_INTERNAL__MAC_10_1                  __attribute__((availability(macosx,introduced=10.1)))
@@ -15550,6 +17217,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_10_12_MSG(_msg)    __attribute__((availability(macosx,introduced=10.1,deprecated=10.12)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_10_12_1    __attribute__((availability(macosx,introduced=10.1,deprecated=10.12.1)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.1,deprecated=10.12.1,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.1,deprecated=10.12.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.1)))
             #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.1)))
             #define __AVAILABILITY_INTERNAL__MAC_10_2                  __attribute__((availability(macosx,introduced=10.2)))
@@ -15649,6 +17322,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_2_DEP__MAC_10_12_MSG(_msg)    __attribute__((availability(macosx,introduced=10.2,deprecated=10.12)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_2_DEP__MAC_10_12_1    __attribute__((availability(macosx,introduced=10.2,deprecated=10.12.1)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_2_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.2,deprecated=10.12.1,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_2_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.2,deprecated=10.12.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_2_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.2)))
             #define __AVAILABILITY_INTERNAL__MAC_10_2_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.2)))
             #define __AVAILABILITY_INTERNAL__MAC_10_3                  __attribute__((availability(macosx,introduced=10.3)))
@@ -15742,6 +17421,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_3_DEP__MAC_10_12_MSG(_msg)    __attribute__((availability(macosx,introduced=10.3,deprecated=10.12)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_3_DEP__MAC_10_12_1    __attribute__((availability(macosx,introduced=10.3,deprecated=10.12.1)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_3_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.3,deprecated=10.12.1,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_3_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.3,deprecated=10.12.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_3_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.3)))
             #define __AVAILABILITY_INTERNAL__MAC_10_3_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.3)))
             #define __AVAILABILITY_INTERNAL__MAC_10_4                  __attribute__((availability(macosx,introduced=10.4)))
@@ -15829,6 +17514,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_4_DEP__MAC_10_12_MSG(_msg)    __attribute__((availability(macosx,introduced=10.4,deprecated=10.12)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_4_DEP__MAC_10_12_1    __attribute__((availability(macosx,introduced=10.4,deprecated=10.12.1)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_4_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.4,deprecated=10.12.1,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_4_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.4,deprecated=10.12.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_4_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.4)))
             #define __AVAILABILITY_INTERNAL__MAC_10_4_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.4)))
             #define __AVAILABILITY_INTERNAL__MAC_10_5                  __attribute__((availability(macosx,introduced=10.5)))
@@ -15910,6 +17601,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_5_DEP__MAC_10_12_MSG(_msg)    __attribute__((availability(macosx,introduced=10.5,deprecated=10.12)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_5_DEP__MAC_10_12_1    __attribute__((availability(macosx,introduced=10.5,deprecated=10.12.1)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_5_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.5,deprecated=10.12.1,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_5_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.5,deprecated=10.12.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_5_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.5)))
             #define __AVAILABILITY_INTERNAL__MAC_10_5_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.5)))
             #define __AVAILABILITY_INTERNAL__MAC_10_6                  __attribute__((availability(macosx,introduced=10.6)))
@@ -15985,6 +17682,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_6_DEP__MAC_10_12_MSG(_msg)    __attribute__((availability(macosx,introduced=10.6,deprecated=10.12)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_6_DEP__MAC_10_12_1    __attribute__((availability(macosx,introduced=10.6,deprecated=10.12.1)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_6_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.6,deprecated=10.12.1,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_6_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.6,deprecated=10.12.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_6_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.6)))
             #define __AVAILABILITY_INTERNAL__MAC_10_6_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.6)))
             #define __AVAILABILITY_INTERNAL__MAC_10_7                  __attribute__((availability(macosx,introduced=10.7)))
@@ -16054,6 +17757,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_7_DEP__MAC_10_12_MSG(_msg)    __attribute__((availability(macosx,introduced=10.7,deprecated=10.12)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_7_DEP__MAC_10_12_1    __attribute__((availability(macosx,introduced=10.7,deprecated=10.12.1)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_7_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.7,deprecated=10.12.1,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_7_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.7,deprecated=10.12.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_7_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.7)))
             #define __AVAILABILITY_INTERNAL__MAC_10_7_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.7)))
             #define __AVAILABILITY_INTERNAL__MAC_10_8                  __attribute__((availability(macosx,introduced=10.8)))
@@ -16117,6 +17826,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_8_DEP__MAC_10_12_MSG(_msg)    __attribute__((availability(macosx,introduced=10.8,deprecated=10.12)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_8_DEP__MAC_10_12_1    __attribute__((availability(macosx,introduced=10.8,deprecated=10.12.1)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_8_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.8,deprecated=10.12.1,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_8_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.8,deprecated=10.12.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_8_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.8)))
             #define __AVAILABILITY_INTERNAL__MAC_10_8_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.8)))
             #define __AVAILABILITY_INTERNAL__MAC_10_9                  __attribute__((availability(macosx,introduced=10.9)))
@@ -16174,6 +17889,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_9_DEP__MAC_10_12_MSG(_msg)    __attribute__((availability(macosx,introduced=10.9,deprecated=10.12)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_9_DEP__MAC_10_12_1    __attribute__((availability(macosx,introduced=10.9,deprecated=10.12.1)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_9_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.9,deprecated=10.12.1,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_9_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.9,deprecated=10.12.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_9_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.9)))
             #define __AVAILABILITY_INTERNAL__MAC_10_9_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.9)))
             #define __AVAILABILITY_INTERNAL__MAC_10_10                  __attribute__((availability(macosx,introduced=10.10)))
@@ -16225,6 +17946,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_10_DEP__MAC_10_12_MSG(_msg)    __attribute__((availability(macosx,introduced=10.10,deprecated=10.12)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_DEP__MAC_10_12_1    __attribute__((availability(macosx,introduced=10.10,deprecated=10.12.1)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_10_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.10,deprecated=10.12.1,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_10_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.10,deprecated=10.12.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_10_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.10)))
             #define __AVAILABILITY_INTERNAL__MAC_10_10_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.10)))
             #define __AVAILABILITY_INTERNAL__MAC_10_10_2                  __attribute__((availability(macosx,introduced=10.10.2)))
@@ -16270,6 +17997,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_10_2_DEP__MAC_10_12_MSG(_msg)    __attribute__((availability(macosx,introduced=10.10.2,deprecated=10.12)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_2_DEP__MAC_10_12_1    __attribute__((availability(macosx,introduced=10.10.2,deprecated=10.12.1)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_10_2_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.10.2,deprecated=10.12.1,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_10_2_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.10.2,deprecated=10.12.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_10_2_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.10.2)))
             #define __AVAILABILITY_INTERNAL__MAC_10_10_2_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.10.2)))
             #define __AVAILABILITY_INTERNAL__MAC_10_10_3                  __attribute__((availability(macosx,introduced=10.10.3)))
@@ -16309,6 +18042,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_10_3_DEP__MAC_10_12_MSG(_msg)    __attribute__((availability(macosx,introduced=10.10.3,deprecated=10.12)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_3_DEP__MAC_10_12_1    __attribute__((availability(macosx,introduced=10.10.3,deprecated=10.12.1)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_10_3_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.10.3,deprecated=10.12.1,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_10_3_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.10.3,deprecated=10.12.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_10_3_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.10.3)))
             #define __AVAILABILITY_INTERNAL__MAC_10_10_3_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.10.3)))
             #define __AVAILABILITY_INTERNAL__MAC_10_11                  __attribute__((availability(macosx,introduced=10.11)))
@@ -16342,6 +18081,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_11_DEP__MAC_10_12_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11,deprecated=10.12)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_DEP__MAC_10_12_1    __attribute__((availability(macosx,introduced=10.11,deprecated=10.12.1)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_11_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11,deprecated=10.12.1,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_11_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11,deprecated=10.12.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_11_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.11)))
             #define __AVAILABILITY_INTERNAL__MAC_10_11_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.11)))
             #define __AVAILABILITY_INTERNAL__MAC_10_11_2                  __attribute__((availability(macosx,introduced=10.11.2)))
@@ -16369,6 +18114,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_11_2_DEP__MAC_10_12_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11.2,deprecated=10.12)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_2_DEP__MAC_10_12_1    __attribute__((availability(macosx,introduced=10.11.2,deprecated=10.12.1)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_11_2_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11.2,deprecated=10.12.1,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_11_2_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11.2,deprecated=10.12.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_11_2_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.11.2)))
             #define __AVAILABILITY_INTERNAL__MAC_10_11_2_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.11.2)))
             #define __AVAILABILITY_INTERNAL__MAC_10_11_3                  __attribute__((availability(macosx,introduced=10.11.3)))
@@ -16390,6 +18141,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_11_3_DEP__MAC_10_12_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11.3,deprecated=10.12)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_3_DEP__MAC_10_12_1    __attribute__((availability(macosx,introduced=10.11.3,deprecated=10.12.1)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_11_3_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11.3,deprecated=10.12.1,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_11_3_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11.3,deprecated=10.12.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_11_3_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.11.3)))
             #define __AVAILABILITY_INTERNAL__MAC_10_11_3_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.11.3)))
             #define __AVAILABILITY_INTERNAL__MAC_10_11_4                  __attribute__((availability(macosx,introduced=10.11.4)))
@@ -16405,6 +18162,12 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_10_12_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11.4,deprecated=10.12)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_10_12_1    __attribute__((availability(macosx,introduced=10.11.4,deprecated=10.12.1)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11.4,deprecated=10.12.1,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.11.4,deprecated=10.12.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.11.4)))
             #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.11.4)))
             #define __AVAILABILITY_INTERNAL__MAC_10_12                  __attribute__((availability(macosx,introduced=10.12)))
@@ -16414,8 +18177,23 @@
             #else
                 #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_10_12_MSG(_msg)    __attribute__((availability(macosx,introduced=10.12,deprecated=10.12)))
             #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_10_12_1    __attribute__((availability(macosx,introduced=10.12,deprecated=10.12.1)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.12,deprecated=10.12.1,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.12,deprecated=10.12.1)))
+            #endif
             #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.12)))
             #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.12)))
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_1                  __attribute__((availability(macosx,introduced=10.12.1)))
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_10_12_1    __attribute__((availability(macosx,introduced=10.12.1,deprecated=10.12.1)))
+            #if __has_feature(attribute_availability_with_message)
+                #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.12.1,deprecated=10.12.1,message=_msg)))
+            #else
+                #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_10_12_1_MSG(_msg)    __attribute__((availability(macosx,introduced=10.12.1,deprecated=10.12.1)))
+            #endif
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_NA_MSG(_msg)      __attribute__((availability(macosx,introduced=10.12.1)))
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_NA                __attribute__((availability(macosx,introduced=10.12.1)))
             #define __AVAILABILITY_INTERNAL__MAC_NA                        __attribute__((availability(macosx,unavailable)))
             #define __AVAILABILITY_INTERNAL__MAC_NA_DEP__MAC_NA            __attribute__((availability(macosx,unavailable)))
             #define __AVAILABILITY_INTERNAL__MAC_NA_DEP__MAC_NA_MSG(_msg)  __attribute__((availability(macosx,unavailable)))
@@ -16424,6 +18202,13 @@
 
     #ifndef __AVAILABILITY_INTERNAL__MAC_10_0
         /* use old style attributes */
+        #if __MAC_OS_X_VERSION_MAX_ALLOWED < __MAC_10_12_1
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_1        __AVAILABILITY_INTERNAL_UNAVAILABLE
+        #elif __MAC_OS_X_VERSION_MIN_REQUIRED < __MAC_10_12_1
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_1        __AVAILABILITY_INTERNAL_WEAK_IMPORT
+        #else
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_1        __AVAILABILITY_INTERNAL_REGULAR
+        #endif
         #if __MAC_OS_X_VERSION_MAX_ALLOWED < __MAC_10_12
             #define __AVAILABILITY_INTERNAL__MAC_10_12        __AVAILABILITY_INTERNAL_UNAVAILABLE
         #elif __MAC_OS_X_VERSION_MIN_REQUIRED < __MAC_10_12
@@ -17282,6 +19067,85 @@
             #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_10_12              __AVAILABILITY_INTERNAL__MAC_10_12
             #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_10_12_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_12
         #endif
+        #if __MAC_OS_X_VERSION_MIN_REQUIRED >= __MAC_10_12_1
+            #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_2_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_2_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_3_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_3_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_4_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_4_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_5_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_5_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_6_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_6_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_7_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_7_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_8_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_8_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_9_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_9_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_2_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_2_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_3_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_3_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_2_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_2_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_3_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_3_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL_DEPRECATED
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL_DEPRECATED_MSG(_msg)
+        #else
+            #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL__MAC_10_0
+            #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_0
+            #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL__MAC_10_1
+            #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_1
+            #define __AVAILABILITY_INTERNAL__MAC_10_2_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL__MAC_10_2
+            #define __AVAILABILITY_INTERNAL__MAC_10_2_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_2
+            #define __AVAILABILITY_INTERNAL__MAC_10_3_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL__MAC_10_3
+            #define __AVAILABILITY_INTERNAL__MAC_10_3_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_3
+            #define __AVAILABILITY_INTERNAL__MAC_10_4_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL__MAC_10_4
+            #define __AVAILABILITY_INTERNAL__MAC_10_4_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_4
+            #define __AVAILABILITY_INTERNAL__MAC_10_5_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL__MAC_10_5
+            #define __AVAILABILITY_INTERNAL__MAC_10_5_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_5
+            #define __AVAILABILITY_INTERNAL__MAC_10_6_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL__MAC_10_6
+            #define __AVAILABILITY_INTERNAL__MAC_10_6_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_6
+            #define __AVAILABILITY_INTERNAL__MAC_10_7_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL__MAC_10_7
+            #define __AVAILABILITY_INTERNAL__MAC_10_7_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_7
+            #define __AVAILABILITY_INTERNAL__MAC_10_8_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL__MAC_10_8
+            #define __AVAILABILITY_INTERNAL__MAC_10_8_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_8
+            #define __AVAILABILITY_INTERNAL__MAC_10_9_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL__MAC_10_9
+            #define __AVAILABILITY_INTERNAL__MAC_10_9_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_9
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL__MAC_10_10
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_10
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_2_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL__MAC_10_10_2
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_2_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_10_2
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_3_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL__MAC_10_10_3
+            #define __AVAILABILITY_INTERNAL__MAC_10_10_3_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_10_3
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL__MAC_10_11
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_11
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_2_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL__MAC_10_11_2
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_2_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_11_2
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_3_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL__MAC_10_11_3
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_3_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_11_3
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL__MAC_10_11_4
+            #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_11_4
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL__MAC_10_12
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_12
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_10_12_1              __AVAILABILITY_INTERNAL__MAC_10_12_1
+            #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_10_12_1_MSG(_msg)    __AVAILABILITY_INTERNAL__MAC_10_12_1
+        #endif
         #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_NA             __AVAILABILITY_INTERNAL__MAC_10_0
         #define __AVAILABILITY_INTERNAL__MAC_10_0_DEP__MAC_NA_MSG(_msg)   __AVAILABILITY_INTERNAL__MAC_10_0
         #define __AVAILABILITY_INTERNAL__MAC_10_1_DEP__MAC_NA             __AVAILABILITY_INTERNAL__MAC_10_1
@@ -17318,6 +19182,8 @@
         #define __AVAILABILITY_INTERNAL__MAC_10_11_4_DEP__MAC_NA_MSG(_msg)   __AVAILABILITY_INTERNAL__MAC_10_11_4
         #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_NA             __AVAILABILITY_INTERNAL__MAC_10_12
         #define __AVAILABILITY_INTERNAL__MAC_10_12_DEP__MAC_NA_MSG(_msg)   __AVAILABILITY_INTERNAL__MAC_10_12
+        #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_NA             __AVAILABILITY_INTERNAL__MAC_10_12_1
+        #define __AVAILABILITY_INTERNAL__MAC_10_12_1_DEP__MAC_NA_MSG(_msg)   __AVAILABILITY_INTERNAL__MAC_10_12_1
         #define __AVAILABILITY_INTERNAL__MAC_NA_DEP__MAC_NA               __AVAILABILITY_INTERNAL_UNAVAILABLE
         #define __AVAILABILITY_INTERNAL__MAC_NA_DEP__MAC_NA_MSG(_msg)     __AVAILABILITY_INTERNAL_UNAVAILABLE
     #endif
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityMacros.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityMacros.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityMacros.h	2016-07-30 17:00:52.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityMacros.h	2016-09-19 18:11:19.000000000 -0400
@@ -107,6 +107,7 @@
 #define MAC_OS_X_VERSION_10_11_3    101103
 #define MAC_OS_X_VERSION_10_11_4    101104
 #define MAC_OS_X_VERSION_10_12      101200
+#define MAC_OS_X_VERSION_10_12_1    101201
 
 /* 
  * If min OS not specified, assume 10.4 for intel
@@ -130,13 +131,13 @@
 #endif
 
 /*
- * if max OS not specified, assume larger of (10.12, min)
+ * if max OS not specified, assume larger of (10.12.1, min)
  */
 #ifndef MAC_OS_X_VERSION_MAX_ALLOWED
-    #if MAC_OS_X_VERSION_MIN_REQUIRED > MAC_OS_X_VERSION_10_12
+    #if MAC_OS_X_VERSION_MIN_REQUIRED > MAC_OS_X_VERSION_10_12_1
         #define MAC_OS_X_VERSION_MAX_ALLOWED MAC_OS_X_VERSION_MIN_REQUIRED
     #else
-        #define MAC_OS_X_VERSION_MAX_ALLOWED MAC_OS_X_VERSION_10_12
+        #define MAC_OS_X_VERSION_MAX_ALLOWED MAC_OS_X_VERSION_10_12_1
     #endif
 #endif
 
@@ -3102,6 +3103,301 @@
 #endif
 
 
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_12_1_AND_LATER
+ * 
+ * Used on declarations introduced in Mac OS X 10.12.1 
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_1_AND_LATER     __OSX_AVAILABLE_STARTING(__MAC_10_12_1, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MAX_ALLOWED < MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_1_AND_LATER     UNAVAILABLE_ATTRIBUTE
+#elif MAC_OS_X_VERSION_MIN_REQUIRED < MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_1_AND_LATER     WEAK_IMPORT_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_1_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_12_1_AND_LATER_BUT_DEPRECATED
+ *
+ * Used on declarations introduced in Mac OS X 10.12.1,
+ * and deprecated in Mac OS X 10.12.1
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_1_AND_LATER_BUT_DEPRECATED     __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_12_1, __MAC_10_12_1, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_1_AND_LATER_BUT_DEPRECATED    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_1_AND_LATER_BUT_DEPRECATED    AVAILABLE_MAC_OS_X_VERSION_10_12_1_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_0_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1
+ *
+ * Used on declarations introduced in Mac OS X 10.0,
+ * but later deprecated in Mac OS X 10.12.1
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_0_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12_1, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_0_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_0_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    AVAILABLE_MAC_OS_X_VERSION_10_0_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_1_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1
+ *
+ * Used on declarations introduced in Mac OS X 10.1,
+ * but later deprecated in Mac OS X 10.12.1
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_1_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1, __MAC_10_12_1, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_1_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_1_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    AVAILABLE_MAC_OS_X_VERSION_10_1_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1
+ *
+ * Used on declarations introduced in Mac OS X 10.2,
+ * but later deprecated in Mac OS X 10.12.1
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_2, __MAC_10_12_1, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    AVAILABLE_MAC_OS_X_VERSION_10_2_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1
+ *
+ * Used on declarations introduced in Mac OS X 10.3,
+ * but later deprecated in Mac OS X 10.12.1
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_3, __MAC_10_12_1, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    AVAILABLE_MAC_OS_X_VERSION_10_3_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1
+ *
+ * Used on declarations introduced in Mac OS X 10.4,
+ * but later deprecated in Mac OS X 10.12.1
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_4, __MAC_10_12_1, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1
+ *
+ * Used on declarations introduced in Mac OS X 10.5,
+ * but later deprecated in Mac OS X 10.12.1
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_5, __MAC_10_12_1, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_6_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1
+ *
+ * Used on declarations introduced in Mac OS X 10.6,
+ * but later deprecated in Mac OS X 10.12.1
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_6_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_6, __MAC_10_12_1, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_6_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_6_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    AVAILABLE_MAC_OS_X_VERSION_10_6_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_7_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1
+ *
+ * Used on declarations introduced in Mac OS X 10.7,
+ * but later deprecated in Mac OS X 10.12.1
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_7_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7, __MAC_10_12_1, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_7_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_7_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    AVAILABLE_MAC_OS_X_VERSION_10_7_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_8_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1
+ *
+ * Used on declarations introduced in Mac OS X 10.8,
+ * but later deprecated in Mac OS X 10.12.1
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_8_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_8, __MAC_10_12_1, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_8_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_8_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    AVAILABLE_MAC_OS_X_VERSION_10_8_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_9_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1
+ *
+ * Used on declarations introduced in Mac OS X 10.9,
+ * but later deprecated in Mac OS X 10.12.1
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_9_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_9, __MAC_10_12_1, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_9_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_9_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    AVAILABLE_MAC_OS_X_VERSION_10_9_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_10_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1
+ *
+ * Used on declarations introduced in Mac OS X 10.10,
+ * but later deprecated in Mac OS X 10.12.1
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_10_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_10, __MAC_10_12_1, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_10_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_10_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    AVAILABLE_MAC_OS_X_VERSION_10_10_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_10_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1
+ *
+ * Used on declarations introduced in Mac OS X 10.10.2,
+ * but later deprecated in Mac OS X 10.12.1
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_10_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_10_2, __MAC_10_12_1, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_10_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_10_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    AVAILABLE_MAC_OS_X_VERSION_10_10_2_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_10_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1
+ *
+ * Used on declarations introduced in Mac OS X 10.10.3,
+ * but later deprecated in Mac OS X 10.12.1
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_10_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_10_3, __MAC_10_12_1, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_10_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_10_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    AVAILABLE_MAC_OS_X_VERSION_10_10_3_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_11_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1
+ *
+ * Used on declarations introduced in Mac OS X 10.11,
+ * but later deprecated in Mac OS X 10.12.1
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_11, __MAC_10_12_1, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    AVAILABLE_MAC_OS_X_VERSION_10_11_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_11_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1
+ *
+ * Used on declarations introduced in Mac OS X 10.11.2,
+ * but later deprecated in Mac OS X 10.12.1
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_11_2, __MAC_10_12_1, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_2_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    AVAILABLE_MAC_OS_X_VERSION_10_11_2_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_11_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1
+ *
+ * Used on declarations introduced in Mac OS X 10.11.3,
+ * but later deprecated in Mac OS X 10.12.1
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_11_3, __MAC_10_12_1, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_3_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    AVAILABLE_MAC_OS_X_VERSION_10_11_3_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_11_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1
+ *
+ * Used on declarations introduced in Mac OS X 10.11.4,
+ * but later deprecated in Mac OS X 10.12.1
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_11_4, __MAC_10_12_1, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_11_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    AVAILABLE_MAC_OS_X_VERSION_10_11_4_AND_LATER
+#endif
+
+/*
+ * AVAILABLE_MAC_OS_X_VERSION_10_12_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1
+ *
+ * Used on declarations introduced in Mac OS X 10.12,
+ * but later deprecated in Mac OS X 10.12.1
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_12, __MAC_10_12_1, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_1
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    DEPRECATED_ATTRIBUTE
+#else
+    #define AVAILABLE_MAC_OS_X_VERSION_10_12_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1    AVAILABLE_MAC_OS_X_VERSION_10_12_AND_LATER
+#endif
+
+/*
+ * DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1_AND_LATER
+ *
+ * Used on types deprecated in Mac OS X 10.12.1
+ */
+#if __AVAILABILITY_MACROS_USES_AVAILABILITY
+    #define DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1_AND_LATER    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12_1, __IPHONE_NA, __IPHONE_NA)
+#elif MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_12_1
+    #define DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1_AND_LATER    DEPRECATED_ATTRIBUTE
+#else
+    #define DEPRECATED_IN_MAC_OS_X_VERSION_10_12_1_AND_LATER
+#endif
+
+
 
 
 #endif  /* __AVAILABILITYMACROS__ */
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOTimeStamp.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOTimeStamp.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOTimeStamp.h	2016-08-12 22:08:32.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOTimeStamp.h	2016-09-29 21:21:59.000000000 -0400
@@ -116,6 +116,7 @@
 #define IODBG_MDESC(code)			(KDBG_CODE(DBG_IOKIT, DBG_IOMDESC, code))
 #define IODBG_POWER(code)			(KDBG_CODE(DBG_IOKIT, DBG_IOPOWER, code))
 #define IODBG_IOSERVICE(code)		(KDBG_CODE(DBG_IOKIT, DBG_IOSERVICE, code))
+#define IODBG_IOREGISTRY(code)		(KDBG_CODE(DBG_IOKIT, DBG_IOREGISTRY, code))
 
 /* IOKit specific codes - within each subclass */
 
@@ -201,5 +202,8 @@
 #define IOSERVICE_TERM_UC_DEFER			25	/* 0x05080064 */
 #define IOSERVICE_DETACH			26	/* 0x05080068 */
 
+/* DBG_IOKIT/DBG_IOREGISTRY codes */
+#define IOREGISTRYENTRY_NAME_STRING              1	/* 0x05090004 */
+#define IOREGISTRYENTRY_NAME			 2	/* 0x05090008 */
 
 #endif /* ! IOKIT_IOTIMESTAMP_H */
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/bluetooth/Bluetooth.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/bluetooth/Bluetooth.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/bluetooth/Bluetooth.h	2016-08-17 21:39:57.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/bluetooth/Bluetooth.h	2016-10-07 22:35:28.000000000 -0400
@@ -365,7 +365,8 @@
 	kBluetoothL2CAPChannelReservedStart			= 0x0007,
     kBluetoothL2CAPChannelLEAP					= 0x002A,
     kBluetoothL2CAPChannelLEAS					= 0x002B,
-	kBluetoothL2CAPChannelMagnet				= 0x003A, // Magnet
+    kBluetoothL2CAPChannelMagicPairing			= 0x0030,
+	kBluetoothL2CAPChannelMagnet				= 0x003A,
     kBluetoothL2CAPChannelReservedEnd			= 0x003F,
     
     // Range 0x0040 to 0xFFFF are dynamically allocated.
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/bluetooth/BluetoothAssignedNumbers.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/bluetooth/BluetoothAssignedNumbers.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/bluetooth/BluetoothAssignedNumbers.h	2016-08-17 21:39:57.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/bluetooth/BluetoothAssignedNumbers.h	2016-10-07 22:49:44.000000000 -0400
@@ -649,6 +649,9 @@
     kBluetoothHCIExtendedInquiryResponseDataTypeServiceData128BitUUID						=	0x21,
     kBluetoothHCIExtendedInquiryResponseDataTypeSecureConnectionsConfirmationValue			=	0x22,
     kBluetoothHCIExtendedInquiryResponseDataTypeSecureConnectionsRandomValue				=	0x23,
+    kBluetoothHCIExtendedInquiryResponseDataTypeURI											=	0x24,
+    kBluetoothHCIExtendedInquiryResponseDataTypeIndoorPositioning							=	0x25,
+    kBluetoothHCIExtendedInquiryResponseDataTypeTransportDiscoveryData						=	0x26,
     kBluetoothHCIExtendedInquiryResponseDataType3DInformationData							=	0x3D,
 	kBluetoothHCIExtendedInquiryResponseDataTypeManufacturerSpecificData					=	0xFF
 };
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDDevice.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDDevice.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDDevice.h	2016-08-16 20:29:00.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDDevice.h	2016-10-05 23:59:49.000000000 -0400
@@ -272,10 +272,10 @@
                                    UInt32          type,
                                    OSDictionary *  properties,
                                    IOUserClient ** handler );
-    IOReturn newUserClientGated(task_t          owningTask,
-                                void *          security_id,
-                                OSDictionary *  properties,
-                                IOUserClient ** handler );
+    IOReturn newUserClientInternal(task_t          owningTask,
+                                   void *          security_id,
+                                   OSDictionary *  properties,
+                                   IOUserClient ** handler );
 
 /*! @function publishProperties
     @abstract Publish HID properties to the I/O Kit registry.
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDElement.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDElement.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDElement.h	2016-08-16 20:29:00.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDElement.h	2016-10-05 23:59:49.000000000 -0400
@@ -82,7 +82,9 @@
     OSMetaClassDeclareReservedUsed(IOHIDElement,  4);
     virtual UInt32                          getValue(IOOptionBits options) = 0;
 
-    OSMetaClassDeclareReservedUnused(IOHIDElement,  5);
+    OSMetaClassDeclareReservedUsed(IOHIDElement,  5);
+    virtual OSData *                        getDataValue(IOOptionBits options) = 0;
+    
     OSMetaClassDeclareReservedUnused(IOHIDElement,  6);
     OSMetaClassDeclareReservedUnused(IOHIDElement,  7);
     OSMetaClassDeclareReservedUnused(IOHIDElement,  8);
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDKeys.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDKeys.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDKeys.h	2016-08-16 20:29:00.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDKeys.h	2016-10-05 23:59:49.000000000 -0400
@@ -397,7 +397,8 @@
  */
 enum {
     kIOHIDValueOptionsFlagRelativeSimple    = (1<<0),
-    kIOHIDValueOptionsFlagPrevious          = (1<<1)
+    kIOHIDValueOptionsFlagPrevious          = (1<<1),
+    kIOHIDValueOptionsUpdateElementValues   = (1<<2)
 };
 typedef uint32_t IOHIDValueOptions;
 
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDProperties.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDProperties.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDProperties.h	2016-08-16 20:29:00.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDProperties.h	2016-10-05 23:59:49.000000000 -0400
@@ -88,7 +88,7 @@
  *
  * @abstract    CFArray of dictionaries that contain user defined key mappings.
  */
-#define kIOHIDUserUsageMapKey                       "UserKeyMapping"
+#define kIOHIDUserKeyUsageMapKey                     "UserKeyMapping"
 
 /*!
  * @define      kIOHIDKeyboardCapsLockDelayOverride
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDUsageTables.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDUsageTables.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDUsageTables.h	2016-08-16 20:29:00.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDUsageTables.h	2016-10-05 23:59:49.000000000 -0400
@@ -1549,6 +1549,7 @@
     kHIDUsage_Snsr_Property_PowerState_D3_Sleep                 = 0x0854,
     kHIDUsage_Snsr_Property_PowerState_D4_PowerOff              = 0x0855,
     /* 0x0855 - 0x085F Reserved */
+    kHIDUsage_Snsr_Light_Illuminance                            = 0x04D1,
     
     /* Specific Sensor Type Data Fields */
     /*** TODO ***/
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDEventDriver.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDEventDriver.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDEventDriver.h	2016-08-16 20:29:00.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDEventDriver.h	2016-10-05 23:59:49.000000000 -0400
@@ -77,6 +77,7 @@
         struct {
             OSArray *           elements;
             UInt8               bootMouseData[4];
+            bool                appleVendorSupported;
         } keyboard;
         
         struct {
@@ -85,6 +86,8 @@
             IOHIDElement *      touchCancelElement;
             bool                native;
             bool                collectionDispatch;
+            IOFixed             centroidX;
+            IOFixed             centroidY;
         } digitizer;
         
         struct {
@@ -140,6 +143,12 @@
             } shoulder;
 
         } gameController;
+      
+        struct {
+            OSArray *           elements;
+            OSArray *           pendingEvents;
+        } vendorMessage;
+
         UInt64  lastReportTime;
     };
     ExpansionData *             _reserved;
@@ -156,7 +165,8 @@
     bool                    parseUnicodeElement(IOHIDElement * element);
     bool                    parseLegacyUnicodeElement(IOHIDElement * element);
     bool                    parseGestureUnicodeElement(IOHIDElement * element);
-    
+    bool                    parseVendorMessageElement(IOHIDElement * element);
+  
     void                    processDigitizerElements();
     void                    processMultiAxisElements();
     void                    processGameControllerElements();
@@ -171,6 +181,7 @@
     void                    setKeyboardProperties();
     void                    setUnicodeProperties();
     void                    setAccelerationProperties();
+    void                    setVendorMessageProperties();
 
     UInt32                  checkGameControllerElement(IOHIDElement * element);
     UInt32                  checkMultiAxisElement(IOHIDElement * element);
@@ -191,7 +202,9 @@
     void                    handleUnicodeLegacyReport(AbsoluteTime timeStamp, UInt32 reportID);
     void                    handleUnicodeGestureReport(AbsoluteTime timeStamp, UInt32 reportID);
     IOHIDEvent *            handleUnicodeGestureCandidateReport(EventElementCollection * candidate, AbsoluteTime timeStamp, UInt32 reportID);
-    
+
+    void                    handleVendorMessageReport(AbsoluteTime timeStamp, IOMemoryDescriptor * report, UInt32 reportID, int phase);
+  
     bool                    serializeCharacterGestureState(void * ref, OSSerialize * serializer);
     bool                    conformTo (UInt32 usagePage, UInt32 usage);
     IOHIDEvent*             createDigitizerTransducerEventForReport(DigitizerTransducer * transducer, AbsoluteTime timeStamp, UInt32 reportID);
@@ -242,6 +255,8 @@
                                 UInt32                      usagePage,
                                 UInt32                      usage );
 
+    virtual void            dispatchEvent(IOHIDEvent * event, IOOptionBits options=0);
+
 public:
 
 
@@ -253,7 +268,8 @@
                                 bool *                      defer );
 
     virtual IOReturn        setProperties( OSObject * properties );
-    
+  
+  
     OSMetaClassDeclareReservedUnused(IOHIDEventDriver,  0);
     OSMetaClassDeclareReservedUnused(IOHIDEventDriver,  1);
     OSMetaClassDeclareReservedUnused(IOHIDEventDriver,  2);
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDUtility.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDUtility.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDUtility.h	2016-08-16 20:29:00.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDUtility.h	2016-10-05 23:59:49.000000000 -0400
@@ -69,4 +69,9 @@
     }
 };
 
+struct KeyAttribute {
+    uint32_t  _flags;
+    KeyAttribute (uint32_t  flags = 0):_flags(flags) {};
+};
+
 #endif /* IOHIDUtility_h */
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDParameter.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDParameter.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDParameter.h	2016-08-16 20:29:00.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDParameter.h	2016-10-05 23:59:49.000000000 -0400
@@ -139,7 +139,7 @@
 
 //
 //
-#define kIOHIDMouseClickNotification    "HIDClickNotification"
+#define kIOHIDResetStickyKeyNotification    "HIDResetStickyKeyNotification"
 
 // if kIOHIDMouseKeysOptionTogglesKey is 1, then a sequence of five
 // option keys in sequence will toggle mouse keys on or off
@@ -162,6 +162,7 @@
 
 // Parametric Acceleration Keys
 #define kHIDAccelParametricCurvesKey            "HIDAccelCurves"
+#define kHIDPointerReportRateKey                "HIDPointerReportRate"
 #define kHIDTrackingAccelParametricCurvesKey    "HIDTrackingAccelCurves"
 #define kHIDScrollAccelParametricCurvesKey      "HIDScrollAccelCurves"
 #define kHIDAccelParametricCurvesDebugKey       "HIDAccelCurvesDebug"
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDSystem.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDSystem.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDSystem.h	2016-08-16 20:29:00.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDSystem.h	2016-10-05 23:59:49.000000000 -0400
@@ -161,6 +161,7 @@
     IOService *	rootDomain;
     AbsoluteTime    displayStateChangeDeadline;
     AbsoluteTime    displaySleepWakeupDeadline;
+    UInt32          powerState;
 
     OSDictionary *  savedParameters;	// keep user settings
 
@@ -182,6 +183,10 @@
 
 
   virtual IOReturn powerStateDidChangeTo( IOPMPowerFlags, unsigned long, IOService * );
+  static IOReturn powerStateHandler( void *target, void *refCon,
+            UInt32 messageType, IOService *service, void *messageArgument, vm_size_t argSize );
+  void updatePowerState(UInt32 messageType);
+
  /* Resets */
     void    _setScrollCountParameters(OSDictionary *newSettings = NULL);
 
@@ -568,6 +573,7 @@
 
 public:
     virtual UInt32 eventFlags();
+    virtual void   sleepDisplayTickle();
 
     virtual void dispatchEvent(IOHIDEvent *event, IOOptionBits options=0);
 
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDUsageTables.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDUsageTables.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDUsageTables.h	2016-08-16 20:29:00.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDUsageTables.h	2016-10-05 23:59:49.000000000 -0400
@@ -1549,6 +1549,7 @@
     kHIDUsage_Snsr_Property_PowerState_D3_Sleep                 = 0x0854,
     kHIDUsage_Snsr_Property_PowerState_D4_PowerOff              = 0x0855,
     /* 0x0855 - 0x085F Reserved */
+    kHIDUsage_Snsr_Light_Illuminance                            = 0x04D1,
     
     /* Specific Sensor Type Data Fields */
     /*** TODO ***/
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostFamily.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostFamily.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostFamily.h	2016-08-16 20:30:24.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostFamily.h	2016-10-07 22:22:55.000000000 -0400
@@ -414,6 +414,7 @@
 #define kUSBHostBillboardDevicePropertyAlternateModeString      "AlternateModeString"
 #define kUSBHostBillboardDevicePropertyAddtionalInfoURLIndex    "iAddtionalInfoURL"
 #define kUSBHostBillboardDevicePropertyAddtionalInfoURL         "AddtionalInfoURL"
+#define kUSBHostBillboardDevicePropertydwAlternateModeVdo       "dwAlternateModeVdo"
 
 #if TARGET_OS_EMBEDDED
 #define kUSBHostInterfacePropertyStringIndex                    "iInterface"
@@ -435,7 +436,6 @@
 #define kUSBHostPortPropertyCompanionIndex                      "kUSBCompanionIndex"
 #define kUSBHostPortPropertyDisconnectInterval                  "kUSBDisconnectInterval"
 #define kUSBHostPortPropertyUsbCPortNumber                      "UsbCPortNumber"
-#define kUSBHostPortPropertyCompanionPresent                    "UsbCompanionPortPresent"               // OSNumber used to determine presence of companion properties
 #define kUSBHostPortPropertyCompanionPortNumber                 "UsbCompanionPortNumber"                // OSData  key to set/get the port number of the companion port
 
 #define kUSBHostHubPropertyPowerSupply                          "kUSBHubPowerSupply"                    // OSNumber mA available for downstream ports, 0 for bus-powered
@@ -453,7 +453,6 @@
 #define kUSBHostControllerPropertyHighSpeedCompanion            "kUSBHighSpeedCompanion"                // OSBoolean false to disable high-speed companion controller
 #define kUSBHostControllerPropertySuperSpeedCompanion           "kUSBSuperSpeedCompanion"               // OSBoolean false to disable superspeed companion controller
 #define kUSBHostControllerPropertyRevision                      "Revision"                              // OSData    Major/minor revision number of controller
-#define kUSBHostControllerPropertyCompanionPresent              "UsbCompanionControllerPresent"         // OSNumber used to determine presence of companion properties
 #define kUSBHostControllerPropertyCompanionControllerName       "UsbCompanionControllerName"            // OSString  key to set/get the name of the service, i.e. companion controller dictionary.
 
 #define kUSBHostPortPropertyExternalDeviceResetController       "kUSBHostPortExternalDeviceResetController"
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/StandardUSB.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/StandardUSB.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/StandardUSB.h	2016-08-16 20:30:24.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/StandardUSB.h	2016-10-07 22:22:55.000000000 -0400
@@ -334,7 +334,8 @@
         kDeviceCapabilityTypeSuperSpeedPlus         = 10,
         kDeviceCapabilityTypePrecisionMeasurement   = 11,
         kDeviceCapabilityTypeWirelessExt            = 12,
-        kDeviceCapabilityTypeBillboard              = 13
+        kDeviceCapabilityTypeBillboard              = 13,
+        kDeviceCapabilityTypeBillboardAltMode       = 15
     };
     
     typedef enum tDeviceCapabilityType tDeviceCapabilityType;
@@ -517,13 +518,25 @@
     typedef struct ContainerIDCapabilityDescriptor ContainerIDCapabilityDescriptor;
 
 
-    // USB Billboard 3.1.6.2: Billboard Capability Descriptor
-    struct BillboardAlternateModeCapability
+    // USB Billboard 3.1.6.2: Billboard Capability Descriptor V1.2
+    struct BillboardAltModeCapabilityCompatibility
     {
         uint16_t  wSVID;
-        uint32_t  bAlternateMode;
+        uint32_t  dwAlternateMode;
         uint8_t   iAlternateModeString;
-    };
+    }__attribute__((packed));
+
+    typedef struct BillboardAltModeCapabilityCompatibility BillboardAltModeCapabilityCompatibility;
+
+    // USB Billboard 3.1.6.2: Billboard Capability Descriptor V1.1 and 1.21+
+    struct BillboardAltModeCapability
+    {
+        uint16_t  wSVID;
+        uint8_t   bAlternateMode;
+        uint8_t   iAlternateModeString;
+    }__attribute__((packed));
+
+    typedef struct BillboardAltModeCapability BillboardAltModeCapability;
 
 #ifdef __cplusplus
     // USB Billboard 3.1.6.2: Billboard Capability Descriptor
@@ -532,23 +545,41 @@
 #else
     struct BillboardCapabilityDescriptor
     {
-        uint8_t                                 bLength;
-        uint8_t                                 bDescriptorType;
-        uint8_t                                 bDevCapabilityType;
-#endif
-        uint8_t                                 iAddtionalInfoURL;
-        uint8_t                                 bNumberOfAlternateModes;
-        uint8_t                                 bPreferredAlternateMode;
-        uint16_t                                VCONNPower;
-        uint8_t                                 bmConfigured[32];
-        uint16_t                                bcdVersion;
-        uint8_t                                 bAdditonalFailureInfo;
-        uint8_t                                 bReserved;
-        struct BillboardAlternateModeCapability BillboardAlternateModeCapabilities[];
-    } __attribute__((packed));
+        uint8_t  bLength;
+        uint8_t  bDescriptorType;
+        uint8_t  bDevCapabilityType;
+#endif
+        uint8_t  iAddtionalInfoURL;
+        uint8_t  bNumberOfAlternateModes;
+        uint8_t  bPreferredAlternateMode;
+        uint16_t VCONNPower;
+        uint8_t  bmConfigured[32];
+        uint16_t bcdVersion;
+        uint8_t  bAdditonalFailureInfo;
+        uint8_t  bReserved;
+        uint8_t  altModeCapabilities[];
+    }__attribute__((packed));
 
     typedef struct BillboardCapabilityDescriptor BillboardCapabilityDescriptor;
 
+#ifdef __cplusplus
+    // USB Billboard 3.1.6.3: Billboard Capability Descriptor V1.21
+    struct BillboardAltModeCapabilityDescriptor : public DeviceCapabilityDescriptor
+    {
+#else
+    struct BillboardAltModeCapabilityDescriptor
+    {
+        uint8_t   bLength;
+        uint8_t   bDescriptorType;
+        uint8_t   bDevCapabilityType;
+#endif
+        uint8_t   bIndex;
+        uint16_t  dwAlternateModeVdo;
+    }__attribute__((packed));
+
+    typedef struct BillboardAltModeCapabilityDescriptor BillboardAltModeCapabilityDescriptor;
+
+
 
 #ifdef __cplusplus
     // USB 3.0 9.6.4: Interface Association
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/task.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/task.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/task.h	2016-08-12 22:08:25.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/task.h	2016-09-29 21:22:10.000000000 -0400
@@ -104,6 +104,12 @@
 extern void		task_reference(task_t	task);
 
 #define TF_NONE                 0
+#define TF_LRETURNWAIT          0x00000100                              /* task is waiting for fork/posix_spawn/exec to complete */
+#define TF_LRETURNWAITER        0x00000200                              /* task is waiting for TF_LRETURNWAIT to get cleared */
+
+#define TPF_NONE                0
+#define TPF_EXEC_COPY           0x00000002                              /* task is the new copy of an exec */
+
 
 __END_DECLS
 
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/version.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/version.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/version.h	2016-08-12 22:08:27.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/version.h	2016-09-29 21:21:54.000000000 -0400
@@ -35,7 +35,7 @@
 /* VERSION_MINOR, version_minor is an integer that represents the minor version
  * of the kernel
  */
-#define VERSION_MINOR		0
+#define VERSION_MINOR		1
 
 /* VERSION_VARIANT, version_variant is a string that contains the revision,
  * stage, and prerelease level of the kernel
@@ -63,7 +63,7 @@
 #define	OSTYPE		"Darwin"
 
 /* OSRELEASE, osrelease, is a string as returned by uname -r */
-#define OSRELEASE	"16.0.0"
+#define OSRELEASE	"16.1.0"
 
 #ifndef ASSEMBLER
 
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/vm_statistics.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/vm_statistics.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/vm_statistics.h	2016-08-12 22:08:42.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/vm_statistics.h	2016-09-29 21:22:08.000000000 -0400
@@ -436,6 +436,8 @@
 /* DHMM data */
 #define VM_MEMORY_DHMM 84
 
+/* memory needed for DFR related actions */
+#define VM_MEMORY_DFR 85
 
 /* memory allocated by SceneKit.framework */
 #define VM_MEMORY_SCENEKIT 86
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_framework.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_framework.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_framework.h	2016-08-12 22:08:15.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_framework.h	2016-09-29 21:21:46.000000000 -0400
@@ -478,10 +478,8 @@
 int	mac_vnode_check_exec(vfs_context_t ctx, struct vnode *vp,
 	    struct image_params *imgp);
 int	mac_vnode_check_fsgetpath(vfs_context_t ctx, struct vnode *vp);
-int	mac_vnode_check_signature(struct vnode *vp,
-		struct cs_blob *cs_blob, struct image_params *imgp,
-		unsigned int *cs_flags,
-		int flags);
+int	mac_vnode_check_getattr(vfs_context_t ctx, struct ucred *file_cred,
+            struct vnode *vp, struct vnode_attr *va);
 int     mac_vnode_check_getattrlist(vfs_context_t ctx, struct vnode *vp,
 	    struct attrlist *alist);
 int	mac_vnode_check_getextattr(vfs_context_t ctx, struct vnode *vp,
@@ -525,6 +523,10 @@
 	    uid_t uid, gid_t gid);
 int	mac_vnode_check_setutimes(vfs_context_t ctx, struct vnode *vp,
 	    struct timespec atime, struct timespec mtime);
+int	mac_vnode_check_signature(struct vnode *vp,
+		struct cs_blob *cs_blob, struct image_params *imgp,
+		unsigned int *cs_flags,
+		int flags);
 int	mac_vnode_check_stat(vfs_context_t ctx,
 	    kauth_cred_t file_cred, struct vnode *vp);
 int	mac_vnode_check_truncate(vfs_context_t ctx,
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_policy.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_policy.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_policy.h	2016-08-12 22:08:16.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_policy.h	2016-09-29 21:21:46.000000000 -0400
@@ -1735,6 +1735,9 @@
 
   @return Return 0 if access is granted, otherwise an appropriate value for
   errno should be returned.
+
+  @note Policies may change the contents of vfa to alter the list of
+  file system attributes returned.
 */
 
 typedef int mpo_mount_check_getattr_t(
@@ -4658,25 +4661,34 @@
 	struct label *label
 );
 /**
-  @brief Access control check after determining the code directory hash
-  @param vp vnode vnode to combine into proc
-  @param label label associated with the vnode
-  @param cs_blob the code signature to check
-  @param cs_flags update code signing flags if needed
-  @param flags operational flag to mpo_vnode_check_signature
-  @param fatal_failure_desc description of fatal failure
-  @param fatal_failure_desc_len failure description len, failure is fatal if non-0
+  @brief Access control check for retrieving file attributes
+  @param active_cred Subject credential
+  @param file_cred Credential associated with the struct fileproc
+  @param vp Object vnode
+  @param vlabel Policy label for vp
+  @param va Vnode attributes to retrieve
+
+  Determine whether the subject identified by the credential can
+  get information about the passed vnode.  The active_cred hold
+  the credentials of the subject performing the operation, and
+  file_cred holds the credentials of the subject that originally
+  opened the file. This check happens during stat(), lstat(),
+  fstat(), and getattrlist() syscalls.  See <sys/vnode.h> for
+  definitions of the attributes.
 
   @return Return 0 if access is granted, otherwise an appropriate value for
   errno should be returned.
- */
-typedef int mpo_vnode_check_signature_t(
+
+  @note Policies may change the contents of va to alter the list of
+  file attributes returned.
+*/
+typedef int mpo_vnode_check_getattr_t(
+	kauth_cred_t active_cred,
+	kauth_cred_t file_cred, /* NULLOK */
 	struct vnode *vp,
-	struct label *label,
-	struct cs_blob *cs_blob,
-	unsigned int *cs_flags,
-	int flags,
-	char **fatal_failure_desc, size_t *fatal_failure_desc_len);
+	struct label *vlabel,
+	struct vnode_attr *va
+);
 /**
   @brief Access control check for retrieving file attributes
   @param cred Subject credential
@@ -5244,6 +5256,27 @@
 	struct timespec mtime
 );
 /**
+  @brief Access control check after determining the code directory hash
+  @param vp vnode vnode to combine into proc
+  @param label label associated with the vnode
+  @param cs_blob the code signature to check
+  @param cs_flags update code signing flags if needed
+  @param flags operational flag to mpo_vnode_check_signature
+  @param fatal_failure_desc description of fatal failure
+  @param fatal_failure_desc_len failure description len, failure is fatal if non-0
+
+  @return Return 0 if access is granted, otherwise an appropriate value for
+  errno should be returned.
+ */
+typedef int mpo_vnode_check_signature_t(
+	struct vnode *vp,
+	struct label *label,
+	struct cs_blob *cs_blob,
+	unsigned int *cs_flags,
+	int flags,
+	char **fatal_failure_desc, size_t *fatal_failure_desc_len
+);
+/**
   @brief Access control check for stat
   @param active_cred Subject credential
   @param file_cred Credential associated with the struct fileproc
@@ -6136,7 +6169,7 @@
  * Please note that this should be kept in sync with the check assumptions
  * policy in bsd/kern/policy_check.c (policy_ops struct).
  */
-#define MAC_POLICY_OPS_VERSION 45 /* inc when new reserved slots are taken */
+#define MAC_POLICY_OPS_VERSION 46 /* inc when new reserved slots are taken */
 struct mac_policy_ops {
 	mpo_audit_check_postselect_t		*mpo_audit_check_postselect;
 	mpo_audit_check_preselect_t		*mpo_audit_check_preselect;
@@ -6283,17 +6316,17 @@
 	mpo_proc_check_set_host_exception_port_t *mpo_proc_check_set_host_exception_port;
 	mpo_exc_action_check_exception_send_t	*mpo_exc_action_check_exception_send;
 	mpo_exc_action_label_associate_t	*mpo_exc_action_label_associate;
-	mpo_exc_action_label_copy_t	*mpo_exc_action_label_copy;
-	mpo_exc_action_label_destroy_t	*mpo_exc_action_label_destroy;
-	mpo_exc_action_label_init_t	*mpo_exc_action_label_init;
-	mpo_exc_action_label_update_t	*mpo_exc_action_label_update;
-
-	mpo_reserved_hook_t			*mpo_reserved17;
-	mpo_reserved_hook_t			*mpo_reserved18;
-	mpo_reserved_hook_t			*mpo_reserved19;
-	mpo_reserved_hook_t			*mpo_reserved20;
-	mpo_reserved_hook_t			*mpo_reserved21;
-	mpo_reserved_hook_t			*mpo_reserved22;
+	mpo_exc_action_label_copy_t		*mpo_exc_action_label_copy;
+	mpo_exc_action_label_destroy_t		*mpo_exc_action_label_destroy;
+	mpo_exc_action_label_init_t		*mpo_exc_action_label_init;
+	mpo_exc_action_label_update_t		*mpo_exc_action_label_update;
+
+	mpo_reserved_hook_t			*mpo_reserved1;
+	mpo_reserved_hook_t			*mpo_reserved2;
+	mpo_reserved_hook_t			*mpo_reserved3;
+	mpo_reserved_hook_t			*mpo_reserved4;
+	mpo_reserved_hook_t			*mpo_reserved5;
+	mpo_reserved_hook_t			*mpo_reserved6;
 
 	mpo_posixsem_check_create_t		*mpo_posixsem_check_create;
 	mpo_posixsem_check_open_t		*mpo_posixsem_check_open;
@@ -6371,7 +6404,7 @@
 	mpo_system_check_settime_t		*mpo_system_check_settime;
 	mpo_system_check_swapoff_t		*mpo_system_check_swapoff;
 	mpo_system_check_swapon_t		*mpo_system_check_swapon;
-	mpo_reserved_hook_t			*mpo_reserved31;
+	mpo_reserved_hook_t			*mpo_reserved7;
 
 	mpo_sysvmsg_label_associate_t		*mpo_sysvmsg_label_associate;
 	mpo_sysvmsg_label_destroy_t		*mpo_sysvmsg_label_destroy;
@@ -6404,9 +6437,9 @@
 	mpo_sysvshm_label_init_t		*mpo_sysvshm_label_init;
 	mpo_sysvshm_label_recycle_t		*mpo_sysvshm_label_recycle;
 
-	mpo_reserved_hook_t			*mpo_reserved23;
-	mpo_reserved_hook_t			*mpo_reserved24;
-	mpo_reserved_hook_t			*mpo_reserved25;
+	mpo_reserved_hook_t			*mpo_reserved8;
+	mpo_reserved_hook_t			*mpo_reserved9;
+	mpo_vnode_check_getattr_t		*mpo_vnode_check_getattr;
 	mpo_mount_check_snapshot_create_t	*mpo_mount_check_snapshot_create;
 	mpo_mount_check_snapshot_delete_t	*mpo_mount_check_snapshot_delete;
 	mpo_vnode_check_clone_t			*mpo_vnode_check_clone;
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/imgact.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/imgact.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/imgact.h	2016-08-12 22:09:15.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/imgact.h	2016-09-29 21:22:39.000000000 -0400
@@ -133,5 +133,6 @@
 #define	IMGPF_DISABLE_ASLR	0x00000020	/* disable ASLR */
 #define	IMGPF_ALLOW_DATA_EXEC	0x00000040	/* forcibly disallow data execution */
 #define	IMGPF_VFORK_EXEC	0x00000080	/* vfork followed by exec */
+#define	IMGPF_EXEC		0x00000100	/* exec */
 
 #endif	/* !_SYS_IMGACT */
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h	2016-08-12 22:09:15.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h	2016-09-29 21:22:38.000000000 -0400
@@ -369,6 +369,7 @@
 #define DBG_IOMDESC			6	/* Memory Descriptors */
 #define DBG_IOPOWER			7	/* Power Managerment */
 #define DBG_IOSERVICE			8	/* Matching etc. */
+#define DBG_IOREGISTRY			9	/* Registry */
 
 /* **** 9-32 reserved for internal IOKit usage **** */
 
@@ -567,6 +568,7 @@
 #define DBG_APP_APPKIT          0x0C
 #define DBG_APP_DFR             0x0E
 #define DBG_APP_SAMBA           0x80
+#define DBG_APP_EOSSUPPORT      0x81
 
 /* Kernel Debug codes for Throttling (DBG_THROTTLE) */
 #define OPEN_THROTTLE_WINDOW	0x1
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebugevents.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebugevents.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebugevents.h	2016-08-12 22:09:19.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebugevents.h	2016-09-29 21:22:44.000000000 -0400
@@ -334,6 +334,7 @@
         {0x1700034, "PMAP_flush_kernel_TLBS"},
         {0x1700038, "PMAP_flush_delayed_TLBS"},
         {0x170003c, "PMAP_flush_TLBS_TO"},
+        {0x1800000, "MACH_CLOCK_EPOCH_CHANGE"},
         {0x1900000, "MP_TLB_FLUSH"},
         {0x1900004, "MP_CPUS_CALL"},
         {0x1900008, "MP_CPUS_CALL_LOCAL"},
@@ -1702,23 +1703,33 @@
         {0x9008088, "wq_pthread_exit"},
         {0x900808c, "wq_workqueue_exit"},
         {0xa000100, "P_CS_Read"},
+        {0xa000104, "P_CS_ReadDone"},
         {0xa000110, "P_CS_Write"},
-        {0xa000180, "P_CS_ReadDone"},
-        {0xa000190, "P_CS_WriteDone"},
+        {0xa000114, "P_CS_WriteDone"},
         {0xa000200, "P_CS_ReadChunk"},
+        {0xa000204, "P_CS_ReadChunkDone"},
         {0xa000210, "P_CS_WriteChunk"},
-        {0xa000280, "P_CS_ReadChunkDone"},
-        {0xa000290, "P_CS_WriteChunkDone"},
-        {0xa000300, "P_CS_ReadCrypto"},
-        {0xa000310, "P_CS_WriteCrypto"},
-        {0xa000500, "P_CS_Originated_Read"},
-        {0xa000510, "P_CS_Originated_Write"},
-        {0xa000580, "P_CS_Originated_ReadDone"},
-        {0xa000590, "P_CS_Originated_WriteDone"},
-        {0xa000900, "P_CS_MetaRead"},
-        {0xa000910, "P_CS_MetaWrite"},
-        {0xa000980, "P_CS_MetaReadDone"},
-        {0xa000990, "P_CS_MetaWriteDone"},
+        {0xa000214, "P_CS_WriteChunkDone"},
+        {0xa000300, "P_CS_ReadMeta"},
+        {0xa000304, "P_CS_ReadMetaDone"},
+        {0xa000310, "P_CS_WriteMeta"},
+        {0xa000314, "P_CS_WriteMetaDone"},
+        {0xa000400, "P_CS_ReadCrypto"},
+        {0xa000404, "P_CS_ReadCryptoDone"},
+        {0xa000410, "P_CS_WriteCrypto"},
+        {0xa000414, "P_CS_WriteCryptoDone"},
+        {0xa000500, "P_CS_TransformRead"},
+        {0xa000504, "P_CS_TransformReadDone"},
+        {0xa000510, "P_CS_TransformWrite"},
+        {0xa000514, "P_CS_TransformWriteDone"},
+        {0xa000600, "P_CS_MigrationRead"},
+        {0xa000604, "P_CS_MigrationReadDone"},
+        {0xa000610, "P_CS_MigrationWrite"},
+        {0xa000614, "P_CS_MigrationWriteDone"},
+        {0xa000700, "P_CS_DirectRead"},
+        {0xa000704, "P_CS_DirectReadDone"},
+        {0xa000710, "P_CS_DirectWrite"},
+        {0xa000714, "P_CS_DirectWriteDone"},
         {0xa008000, "P_CS_SYNC_DISK"},
         {0xa008004, "P_CS_WaitForBuffer"},
         {0xa008008, "P_CS_NoBuffer"},
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h	2016-08-12 22:09:19.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h	2016-09-29 21:22:43.000000000 -0400
@@ -29,7 +29,7 @@
  * System call switch table.
  *
  * DO NOT EDIT-- this file is automatically generated.
- * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3789.1.28/bsd/kern/syscalls.master
+ * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3789.21.3/bsd/kern/syscalls.master
  */
 
 #ifndef _SYS_SYSCALL_H_
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h	2016-08-12 22:09:19.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h	2016-09-29 21:22:43.000000000 -0400
@@ -29,7 +29,7 @@
  * System call switch table.
  *
  * DO NOT EDIT-- this file is automatically generated.
- * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3789.1.28/bsd/kern/syscalls.master
+ * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3789.21.3/bsd/kern/syscalls.master
  */
 
 #ifndef _SYS_SYSPROTO_H_
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/ucred.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/ucred.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/ucred.h	2016-08-12 22:09:17.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/ucred.h	2016-09-29 21:22:41.000000000 -0400
@@ -148,6 +148,7 @@
 int		crcmp(kauth_cred_t cr1, kauth_cred_t cr2);
 int		suser(kauth_cred_t cred, u_short *acflag);
 int		set_security_token(struct proc * p);
+int		set_security_token_task_internal(struct proc *p, void *task);
 void		cru2x(kauth_cred_t cr, struct xucred *xcr);
 __END_DECLS
 #endif /* __APPLE_API_OBSOLETE */

```