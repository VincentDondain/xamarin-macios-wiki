#CoreFoundation.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFArray.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFArray.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFArray.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFArray.h	2016-06-01 05:52:12.000000000 +0200
@@ -384,7 +384,7 @@
 		undefined.
 */
 CF_EXPORT
-void CFArrayApplyFunction(CFArrayRef theArray, CFRange range, CFArrayApplierFunction applier, void *context);
+void CFArrayApplyFunction(CFArrayRef theArray, CFRange range, CFArrayApplierFunction CF_NOESCAPE applier, void *context);
 
 /*!
 	@function CFArrayGetFirstIndexOfValue
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFAvailability.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFAvailability.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFAvailability.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFAvailability.h	2016-05-23 04:36:46.000000000 +0200
@@ -1,11 +1,20 @@
 /*	CFAvailability.h
 	Copyright (c) 2013-2015, Apple Inc. All rights reserved.
+ 
+	Portions Copyright (c) 2014-2016 Apple Inc. and the Swift project authors
+	Licensed under Apache License v2.0 with Runtime Library Exception
+	See http://swift.org/LICENSE.txt for license information
+	See http://swift.org/CONTRIBUTORS.txt for the list of Swift project authors
 */
 
 #if !defined(__COREFOUNDATION_CFAVAILABILITY__)
 #define __COREFOUNDATION_CFAVAILABILITY__ 1
 
+#if DEPLOYMENT_RUNTIME_SWIFT
+#include <CoreFoundation/TargetConditionals.h>
+#else
 #include <TargetConditionals.h>
+#endif
 
 #if (TARGET_OS_MAC || TARGET_OS_EMBEDDED || TARGET_OS_IPHONE || TARGET_OS_WIN32)
 #include <Availability.h>
@@ -126,6 +135,21 @@
 */
 #define CF_ENUM(...) __CF_ENUM_GET_MACRO(__VA_ARGS__, __CF_NAMED_ENUM, __CF_ANON_ENUM)(__VA_ARGS__)
 
+#if __has_attribute(swift_wrapper)
+#define _CF_TYPED_ENUM __attribute__((swift_wrapper(enum)))
+#else
+#define _CF_TYPED_ENUM
+#endif
+
+#if __has_attribute(swift_wrapper)
+#define _CF_TYPED_EXTENSIBLE_ENUM __attribute__((swift_wrapper(struct)))
+#else
+#define _CF_TYPED_EXTENSIBLE_ENUM
+#endif
+
+#define CF_STRING_ENUM _CF_TYPED_ENUM
+#define CF_EXTENSIBLE_STRING_ENUM _CF_TYPED_EXTENSIBLE_ENUM
+
 // Extension availability macros
 #define CF_EXTENSION_UNAVAILABLE(_msg)      __OS_EXTENSION_UNAVAILABLE(_msg)
 #define CF_EXTENSION_UNAVAILABLE_MAC(_msg)  __OSX_EXTENSION_UNAVAILABLE(_msg)
@@ -138,4 +162,116 @@
 #define CF_SWIFT_UNAVAILABLE(_msg)
 #endif
 
+
+//
+// New-Style Availability
+//
+#ifndef API_AVAILABLE
+/*
+ Macros for defining which versions/platform a given symbol can be used.
+ 
+ @see http://clang.llvm.org/docs/AttributeReference.html#availability
+ */
+
+//
+// API Introductions
+//
+// Use to specify the release that a particular API became available.
+//
+// Platform names:
+//   macosx, ios, tvos, watchos
+//
+// Examples:
+//    API_AVAILABLE(macosx(10.10))
+//    API_AVAILABLE(macosx(10.9), ios(10.0))
+//    API_AVAILABLE(macosx(10.4), ios(8.0), watchos(2.0), tvos(10.0))
+//
+#define __API_AVAILABLE_PLATFORM_macosx(x) macosx,introduced=x
+#define __API_AVAILABLE_PLATFORM_ios(x) ios,introduced=x
+#define __API_AVAILABLE_PLATFORM_watchos(x) watchos,introduced=x
+#define __API_AVAILABLE_PLATFORM_tvos(x) tvos,introduced=x
+
+#define __API_A(x) __attribute__((availability(__API_AVAILABLE_PLATFORM_##x)))
+#define __API_AVAILABLE1(x) __API_A(x)
+#define __API_AVAILABLE2(x,y) __API_A(x) __API_A(y)
+#define __API_AVAILABLE3(x,y,z)  __API_A(x) __API_A(y) __API_A(z)
+#define __API_AVAILABLE4(x,y,z,t) __API_A(x) __API_A(y) __API_A(z) __API_A(t)
+#define __API_AVAILABLE_GET_MACRO(_1,_2,_3,_4,NAME,...) NAME
+#define API_AVAILABLE(...) __API_AVAILABLE_GET_MACRO(__VA_ARGS__,__API_AVAILABLE4, __API_AVAILABLE3, __API_AVAILABLE2, __API_AVAILABLE1)(__VA_ARGS__)
+#pragma mark -
+
+
+//
+// API Deprecations
+//
+// Use to specify the release that a particular API became unavailable.
+//
+// Platform names:
+//   macosx, ios, tvos, watchos
+//
+// Examples:
+//
+//    API_DEPRECATED("No longer supported", macosx(10.4, 10.8))
+//    API_DEPRECATED("No longer supported", macosx(10.4, 10.8), ios(2.0, 3.0), watchos(2.0, 3.0), tvos(9.0, 10.0))
+//
+//    API_DEPRECATED_WITH_REPLACEMENT("-setName:", tvos(10.0, 10.4), ios(9.0, 10.0))
+//    API_DEPRECATED_WITH_REPLACEMENT("SomeClassName", macosx(10.4, 10.6), watchos(2.0, 3.0))
+//
+#define __API_DEPRECATED_PLATFORM_macosx(x,y) macosx,introduced=x,deprecated=y
+#define __API_DEPRECATED_PLATFORM_ios(x,y) ios,introduced=x,deprecated=y
+#define __API_DEPRECATED_PLATFORM_watchos(x,y) watchos,introduced=x,deprecated=y
+#define __API_DEPRECATED_PLATFORM_tvos(x,y) tvos,introduced=x,deprecated=y
+
+#define __API_D(msg,x) __attribute__((availability(__API_DEPRECATED_PLATFORM_##x,message=msg)))
+#define __API_DEPRECATED_MSG2(msg,x) __API_D(msg,x)
+#define __API_DEPRECATED_MSG3(msg,x,y) __API_D(msg,x) __API_D(msg,y)
+#define __API_DEPRECATED_MSG4(msg,x,y,z) __API_DEPRECATED_MSG3(msg,x,y) __API_D(msg,z)
+#define __API_DEPRECATED_MSG5(msg,x,y,z,t) __API_DEPRECATED_MSG4(msg,x,y,z) __API_D(msg,t)
+#define __API_DEPRECATED_MSG_GET_MACRO(_1,_2,_3,_4,_5,NAME,...) NAME
+#define API_DEPRECATED(...) __API_DEPRECATED_MSG_GET_MACRO(__VA_ARGS__,__API_DEPRECATED_MSG5,__API_DEPRECATED_MSG4,__API_DEPRECATED_MSG3,__API_DEPRECATED_MSG2,__API_DEPRECATED_MSG1)(__VA_ARGS__)
+
+#define __API_R(rep,x) __attribute__((availability(__API_DEPRECATED_PLATFORM_##x,replacement=rep)))
+#define __API_DEPRECATED_REP2(rep,x) __API_R(rep,x)
+#define __API_DEPRECATED_REP3(rep,x,y) __API_R(rep,x) __API_R(rep,y)
+#define __API_DEPRECATED_REP4(rep,x,y,z)  __API_DEPRECATED_REP3(rep,x,y) __API_R(rep,z)
+#define __API_DEPRECATED_REP5(rep,x,y,z,t) __API_DEPRECATED_REP4(rep,x,y,z) __API_R(rep,t)
+#define __API_DEPRECATED_REP_GET_MACRO(_1,_2,_3,_4,_5,NAME,...) NAME
+#define API_DEPRECATED_WITH_REPLACEMENT(...) __API_DEPRECATED_REP_GET_MACRO(__VA_ARGS__,__API_DEPRECATED_REP5,__API_DEPRECATED_REP4,__API_DEPRECATED_REP3,__API_DEPRECATED_REP2,__API_DEPRECATED_REP1)(__VA_ARGS__)
+
+#pragma mark -
+
+
+//
+// API Unavailability
+// Use to specify that an API is unavailable for a particular platform.
+//
+// Example:
+//    API_UNAVAILABLE(macosx)
+//    API_UNAVAILABLE(watchos, tvos)
+//
+#define __API_UNAVAILABLE_PLATFORM_macosx macosx,unavailable
+#define __API_UNAVAILABLE_PLATFORM_ios ios,unavailable
+#define __API_UNAVAILABLE_PLATFORM_watchos watchos,unavailable
+#define __API_UNAVAILABLE_PLATFORM_tvos tvos,unavailable
+
+#define __API_U(x) __attribute__((availability(__API_UNAVAILABLE_PLATFORM_##x)))
+#define __API_UNAVAILABLE1(x) __API_U(x)
+#define __API_UNAVAILABLE2(x,y) __API_U(x) __API_U(y)
+#define __API_UNAVAILABLE3(x,y,z) __API_UNAVAILABLE2(x,y) __API_U(z)
+#define __API_UNAVAILABLE_GET_MACRO(_1,_2,_3,NAME,...) NAME
+#define API_UNAVAILABLE(...) __API_UNAVAILABLE_GET_MACRO(__VA_ARGS__,__API_UNAVAILABLE3,__API_UNAVAILABLE2,__API_UNAVAILABLE1)(__VA_ARGS__)
+#pragma mark -
+
+
+//
+// Swift Deprecations
+// Use to specify that an API is deprecated for Swift.
+//
+// Example:
+//    API_DEPRECATED_FOR_SWIFT("Please use array literals instead")
+//
+#define API_DEPRECATED_FOR_SWIFT(msg) __attribute__((availability(swift,deprecated,message=msg)))
+
+#endif // API_AVAILABLE
+
 #endif // __COREFOUNDATION_CFAVAILABILITY__
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFBag.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFBag.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFBag.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFBag.h	2016-05-23 04:36:46.000000000 +0200
@@ -68,7 +68,7 @@
 void CFBagGetValues(CFBagRef theBag, const void **values);
 
 CF_EXPORT
-void CFBagApplyFunction(CFBagRef theBag, CFBagApplierFunction applier, void *context);
+void CFBagApplyFunction(CFBagRef theBag, CFBagApplierFunction CF_NOESCAPE applier, void *context);
 
 CF_EXPORT
 void CFBagAddValue(CFMutableBagRef theBag, const void *value);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFBase.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFBase.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFBase.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFBase.h	2016-05-20 07:42:52.000000000 +0200
@@ -1,11 +1,20 @@
 /*	CFBase.h
 	Copyright (c) 1998-2015, Apple Inc. All rights reserved.
+ 
+	Portions Copyright (c) 2014-2016 Apple Inc. and the Swift project authors
+	Licensed under Apache License v2.0 with Runtime Library Exception
+	See http://swift.org/LICENSE.txt for license information
+	See http://swift.org/CONTRIBUTORS.txt for the list of Swift project authors
 */
 
 #if !defined(__COREFOUNDATION_CFBASE__)
 #define __COREFOUNDATION_CFBASE__ 1
 
+#if DEPLOYMENT_RUNTIME_SWIFT
+#include <CoreFoundation/TargetConditionals.h>
+#else
 #include <TargetConditionals.h>
+#endif
 #include <CoreFoundation/CFAvailability.h>
 
 #if (defined(__CYGWIN32__) || defined(_WIN32)) && !defined(__WIN32__)
@@ -68,14 +77,18 @@
     #include <MacTypes.h>
   #endif
 #else
-  #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE)) || (TARGET_OS_EMBEDDED || TARGET_OS_IPHONE)
+  #if ((TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE)) || (TARGET_OS_EMBEDDED || TARGET_OS_IPHONE)) && !DEPLOYMENT_RUNTIME_SWIFT
     #include <libkern/OSTypes.h>
   #endif
 #endif
 
 #if !defined(__MACTYPES__)
 #if !defined(_OS_OSTYPES_H)
+#if DEPLOYMENT_RUNTIME_SWIFT
+    typedef _Bool                   Boolean;
+#else
     typedef unsigned char           Boolean;
+#endif
     typedef unsigned char           UInt8;
     typedef signed char             SInt8;
     typedef unsigned short          UInt16;
@@ -271,14 +284,14 @@
 
 
 #if !__has_feature(nullability)
-#ifndef __nullable
-#define __nullable
+#ifndef _Nullable
+#define _Nullable
 #endif
-#ifndef __nonnull
-#define __nonnull
+#ifndef _Nonnull
+#define _Nonnull
 #endif
-#ifndef __null_unspecified
-#define __null_unspecified
+#ifndef _Null_unspecified
+#define _Null_unspecified
 #endif
 #endif
 
@@ -296,6 +309,17 @@
 # define CF_SWIFT_NAME(_name)
 #endif
 
+#if __has_attribute(noescape)
+#define CF_NOESCAPE __attribute__((noescape))
+#else
+#define CF_NOESCAPE
+#endif
+
+#if __has_attribute(not_tail_called)
+#define CF_NO_TAIL_CALL __attribute__((not_tail_called))
+#else
+#define CF_NO_TAIL_CALL
+#endif
 
 #if !__has_feature(objc_generics_variance)
 #ifndef __covariant
@@ -388,6 +412,15 @@
 #define kCFCoreFoundationVersionNumber10_10_1   1151.16
 #define kCFCoreFoundationVersionNumber10_10_2   1152
 #define kCFCoreFoundationVersionNumber10_10_3   1153.18
+#define kCFCoreFoundationVersionNumber10_10_4   1153.18
+#define kCFCoreFoundationVersionNumber10_10_5   1153.18
+#define kCFCoreFoundationVersionNumber10_10_Max 1199
+#define kCFCoreFoundationVersionNumber10_11     1253
+#define kCFCoreFoundationVersionNumber10_11_1   1255.1
+#define kCFCoreFoundationVersionNumber10_11_2   1256.14
+#define kCFCoreFoundationVersionNumber10_11_3   1256.14
+#define kCFCoreFoundationVersionNumber10_11_4   1258.1
+#define kCFCoreFoundationVersionNumber10_11_Max 1299
 #endif
 
 #if TARGET_OS_IPHONE
@@ -410,6 +443,15 @@
 #define kCFCoreFoundationVersionNumber_iOS_8_0 1140.1
 #define kCFCoreFoundationVersionNumber_iOS_8_1 1141.14
 #define kCFCoreFoundationVersionNumber_iOS_8_2 1142.16
+#define kCFCoreFoundationVersionNumber_iOS_8_3 1144.17
+#define kCFCoreFoundationVersionNumber_iOS_8_4 1145.15
+#define kCFCoreFoundationVersionNumber_iOS_8_x_Max 1199
+#define kCFCoreFoundationVersionNumber_iOS_9_0 1240.1
+#define kCFCoreFoundationVersionNumber_iOS_9_1 1241.11
+#define kCFCoreFoundationVersionNumber_iOS_9_2 1242.13
+#define kCFCoreFoundationVersionNumber_iOS_9_3 1242.13
+#define kCFCoreFoundationVersionNumber_iOS_9_4 1280.38
+#define kCFCoreFoundationVersionNumber_iOS_9_x_Max 1299
 #endif
 
 #if __LLP64__
@@ -617,11 +659,14 @@
 CF_EXPORT
 void CFRelease(CFTypeRef cf);
 
+#if DEPLOYMENT_RUNTIME_SWIFT
+#else
 CF_EXPORT
 CFTypeRef CFAutorelease(CFTypeRef CF_RELEASES_ARGUMENT arg) CF_AVAILABLE(10_9, 7_0);
 
 CF_EXPORT
 CFIndex CFGetRetainCount(CFTypeRef cf);
+#endif
 
 CF_EXPORT
 Boolean CFEqual(CFTypeRef cf1, CFTypeRef cf2);
@@ -637,7 +682,7 @@
 
 CF_IMPLICIT_BRIDGING_DISABLED
 
-// This function is unavailable in ARC mode.
+// This function is unavailable in ARC mode. On OS X 10.12 and later, this function simply returns the argument.
 CF_EXPORT
 CFTypeRef CFMakeCollectable(CFTypeRef cf) CF_AUTOMATED_REFCOUNT_UNAVAILABLE;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFBinaryHeap.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFBinaryHeap.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFBinaryHeap.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFBinaryHeap.h	2016-05-20 07:42:52.000000000 +0200
@@ -251,7 +251,7 @@
 		what is expected by the applier function, the behavior is
 		undefined.
 */
-CF_EXPORT void		CFBinaryHeapApplyFunction(CFBinaryHeapRef heap, CFBinaryHeapApplierFunction applier, void *context);
+CF_EXPORT void		CFBinaryHeapApplyFunction(CFBinaryHeapRef heap, CFBinaryHeapApplierFunction CF_NOESCAPE applier, void *context);
 
 /*!
 	@function CFBinaryHeapAddValue
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFCalendar.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFCalendar.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFCalendar.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFCalendar.h	2016-05-23 04:36:46.000000000 +0200
@@ -22,12 +22,12 @@
 CFCalendarRef CFCalendarCopyCurrent(void);
 
 CF_EXPORT
-CFCalendarRef CFCalendarCreateWithIdentifier(CFAllocatorRef allocator, CFStringRef identifier);
+CFCalendarRef CFCalendarCreateWithIdentifier(CFAllocatorRef allocator, CFCalendarIdentifier identifier);
 	// Create a calendar.  The identifiers are the kCF*Calendar
 	// constants in CFLocale.h.
 
 CF_EXPORT
-CFStringRef CFCalendarGetIdentifier(CFCalendarRef calendar);
+CFCalendarIdentifier CFCalendarGetIdentifier(CFCalendarRef calendar);
 	// Returns the calendar's identifier.
 
 CF_EXPORT
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFDateFormatter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFDateFormatter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFDateFormatter.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFDateFormatter.h	2016-05-20 07:42:52.000000000 +0200
@@ -12,6 +12,8 @@
 CF_IMPLICIT_BRIDGING_ENABLED
 CF_EXTERN_C_BEGIN
 
+typedef CFStringRef CFDateFormatterKey CF_STRING_ENUM;
+
 typedef struct CF_BRIDGED_MUTABLE_TYPE(id) __CFDateFormatter *CFDateFormatterRef;
 
 // CFDateFormatters are not thread-safe.  Do not use one from multiple threads!
@@ -23,14 +25,6 @@
 CF_EXPORT
 CFTypeID CFDateFormatterGetTypeID(void);
 
-typedef CF_ENUM(CFIndex, CFDateFormatterStyle) {	// date and time format styles
-	kCFDateFormatterNoStyle = 0,
-	kCFDateFormatterShortStyle = 1,
-	kCFDateFormatterMediumStyle = 2,
-	kCFDateFormatterLongStyle = 3,
-	kCFDateFormatterFullStyle = 4
-};
-
 // The exact formatted result for these date and time styles depends on the
 // locale, but generally:
 //     Short is completely numeric, such as "12/13/52" or "3:30pm"
@@ -43,6 +37,48 @@
 // should not rely on styles and localization, but set the format string and
 // use nothing but numbers.
 
+typedef CF_ENUM(CFIndex, CFDateFormatterStyle) {	// date and time format styles
+    kCFDateFormatterNoStyle = 0,
+    kCFDateFormatterShortStyle = 1,
+    kCFDateFormatterMediumStyle = 2,
+    kCFDateFormatterLongStyle = 3,
+    kCFDateFormatterFullStyle = 4
+};
+
+typedef CF_OPTIONS(CFOptionFlags, CFISO8601DateFormatOptions) {
+    /* The format for year is inferred based on whether or not the week of year option is specified.
+     - if week of year is present, "YYYY" is used to display week dates.
+     - if week of year is not present, "yyyy" is used by default.
+     */
+    kCFISO8601DateFormatWithYear API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = (1UL << 0),
+    kCFISO8601DateFormatWithMonth API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = (1UL << 1),
+
+    kCFISO8601DateFormatWithWeekOfYear API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = (1UL << 2),  // This includes the "W" prefix (e.g. "W49")
+
+    /* The format for day is inferred based on provided options.
+     - if month is not present, day of year ("DDD") is used.
+     - if month is present, day of month ("dd") is used.
+     - if either weekOfMonth or weekOfYear is present, local day of week ("ee") is used.
+     */
+    kCFISO8601DateFormatWithDay API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = (1UL << 4),
+
+    kCFISO8601DateFormatWithTime API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = (1UL << 5),  // This uses the format "HH:mm:ss"
+    kCFISO8601DateFormatWithTimeZone API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = (1UL << 6),
+
+    kCFISO8601DateFormatWithSpaceBetweenDateAndTime API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = (1UL << 7),  // Use space instead of "T"
+    kCFISO8601DateFormatWithDashSeparatorInDate API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = (1UL << 8),  // Add separator for date ("-")
+    kCFISO8601DateFormatWithColonSeparatorInTime API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = (1UL << 9),  // Add separator for time (":")
+    kCFISO8601DateFormatWithColonSeparatorInTimeZone API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = (1UL << 10),  // Add ":" separator in timezone (eg. +08:00)
+
+    kCFISO8601DateFormatWithFullDate API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = kCFISO8601DateFormatWithYear | kCFISO8601DateFormatWithMonth | kCFISO8601DateFormatWithDay | kCFISO8601DateFormatWithDashSeparatorInDate,
+    kCFISO8601DateFormatWithFullTime API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = kCFISO8601DateFormatWithTime | kCFISO8601DateFormatWithColonSeparatorInTime | kCFISO8601DateFormatWithTimeZone | kCFISO8601DateFormatWithColonSeparatorInTimeZone,
+
+    kCFISO8601DateFormatWithInternetDateTime API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = kCFISO8601DateFormatWithFullDate | kCFISO8601DateFormatWithFullTime,  // RFC3339
+};
+
+CF_EXPORT
+CFDateFormatterRef CFDateFormatterCreateISO8601Formatter(CFAllocatorRef allocator, CFISO8601DateFormatOptions formatOptions) API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
 CF_EXPORT
 CFDateFormatterRef CFDateFormatterCreate(CFAllocatorRef allocator, CFLocaleRef locale, CFDateFormatterStyle dateStyle, CFDateFormatterStyle timeStyle);
 	// Returns a CFDateFormatter, localized to the given locale, which
@@ -97,39 +133,39 @@
 void CFDateFormatterSetProperty(CFDateFormatterRef formatter, CFStringRef key, CFTypeRef value);
 
 CF_EXPORT
-CFTypeRef CFDateFormatterCopyProperty(CFDateFormatterRef formatter, CFStringRef key);
+CFTypeRef CFDateFormatterCopyProperty(CFDateFormatterRef formatter, CFDateFormatterKey key);
 	// Set and get various properties of the date formatter, the set of
 	// which may be expanded in the future.
 
-CF_EXPORT const CFStringRef kCFDateFormatterIsLenient;	// CFBoolean
-CF_EXPORT const CFStringRef kCFDateFormatterTimeZone;		// CFTimeZone
-CF_EXPORT const CFStringRef kCFDateFormatterCalendarName;	// CFString
-CF_EXPORT const CFStringRef kCFDateFormatterDefaultFormat;	// CFString
-CF_EXPORT const CFStringRef kCFDateFormatterTwoDigitStartDate; // CFDate
-CF_EXPORT const CFStringRef kCFDateFormatterDefaultDate;	// CFDate
-CF_EXPORT const CFStringRef kCFDateFormatterCalendar;		// CFCalendar
-CF_EXPORT const CFStringRef kCFDateFormatterEraSymbols;	// CFArray of CFString
-CF_EXPORT const CFStringRef kCFDateFormatterMonthSymbols;	// CFArray of CFString
-CF_EXPORT const CFStringRef kCFDateFormatterShortMonthSymbols; // CFArray of CFString
-CF_EXPORT const CFStringRef kCFDateFormatterWeekdaySymbols;	// CFArray of CFString
-CF_EXPORT const CFStringRef kCFDateFormatterShortWeekdaySymbols; // CFArray of CFString
-CF_EXPORT const CFStringRef kCFDateFormatterAMSymbol;		// CFString
-CF_EXPORT const CFStringRef kCFDateFormatterPMSymbol;		// CFString
-CF_EXPORT const CFStringRef kCFDateFormatterLongEraSymbols CF_AVAILABLE(10_5, 2_0);   // CFArray of CFString
-CF_EXPORT const CFStringRef kCFDateFormatterVeryShortMonthSymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
-CF_EXPORT const CFStringRef kCFDateFormatterStandaloneMonthSymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
-CF_EXPORT const CFStringRef kCFDateFormatterShortStandaloneMonthSymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
-CF_EXPORT const CFStringRef kCFDateFormatterVeryShortStandaloneMonthSymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
-CF_EXPORT const CFStringRef kCFDateFormatterVeryShortWeekdaySymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
-CF_EXPORT const CFStringRef kCFDateFormatterStandaloneWeekdaySymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
-CF_EXPORT const CFStringRef kCFDateFormatterShortStandaloneWeekdaySymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
-CF_EXPORT const CFStringRef kCFDateFormatterVeryShortStandaloneWeekdaySymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
-CF_EXPORT const CFStringRef kCFDateFormatterQuarterSymbols CF_AVAILABLE(10_5, 2_0); 	// CFArray of CFString
-CF_EXPORT const CFStringRef kCFDateFormatterShortQuarterSymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
-CF_EXPORT const CFStringRef kCFDateFormatterStandaloneQuarterSymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
-CF_EXPORT const CFStringRef kCFDateFormatterShortStandaloneQuarterSymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
-CF_EXPORT const CFStringRef kCFDateFormatterGregorianStartDate CF_AVAILABLE(10_5, 2_0); // CFDate
-CF_EXPORT const CFStringRef kCFDateFormatterDoesRelativeDateFormattingKey CF_AVAILABLE(10_6, 4_0); // CFBoolean
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterIsLenient;	// CFBoolean
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterTimeZone;		// CFTimeZone
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterCalendarName;	// CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterDefaultFormat;	// CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterTwoDigitStartDate; // CFDate
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterDefaultDate;	// CFDate
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterCalendar;		// CFCalendar
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterEraSymbols;	// CFArray of CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterMonthSymbols;	// CFArray of CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterShortMonthSymbols; // CFArray of CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterWeekdaySymbols;	// CFArray of CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterShortWeekdaySymbols; // CFArray of CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterAMSymbol;		// CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterPMSymbol;		// CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterLongEraSymbols CF_AVAILABLE(10_5, 2_0);   // CFArray of CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterVeryShortMonthSymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterStandaloneMonthSymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterShortStandaloneMonthSymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterVeryShortStandaloneMonthSymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterVeryShortWeekdaySymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterStandaloneWeekdaySymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterShortStandaloneWeekdaySymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterVeryShortStandaloneWeekdaySymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterQuarterSymbols CF_AVAILABLE(10_5, 2_0); 	// CFArray of CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterShortQuarterSymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterStandaloneQuarterSymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterShortStandaloneQuarterSymbols CF_AVAILABLE(10_5, 2_0); // CFArray of CFString
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterGregorianStartDate CF_AVAILABLE(10_5, 2_0); // CFDate
+CF_EXPORT const CFDateFormatterKey kCFDateFormatterDoesRelativeDateFormattingKey CF_AVAILABLE(10_6, 4_0); // CFBoolean
 
 // See CFLocale.h for these calendar constants:
 //	const CFStringRef kCFGregorianCalendar;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFDictionary.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFDictionary.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFDictionary.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFDictionary.h	2016-05-20 07:42:52.000000000 +0200
@@ -574,7 +574,7 @@
 		undefined.
 */
 CF_EXPORT
-void CFDictionaryApplyFunction(CFDictionaryRef theDict, CFDictionaryApplierFunction applier, void *context);
+void CFDictionaryApplyFunction(CFDictionaryRef theDict, CFDictionaryApplierFunction CF_NOESCAPE applier, void *context);
 
 /*!
 	@function CFDictionaryAddValue
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFError.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFError.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFError.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFError.h	2016-05-23 04:36:46.000000000 +0200
@@ -36,6 +36,8 @@
 CF_IMPLICIT_BRIDGING_ENABLED
 CF_EXTERN_C_BEGIN
 
+typedef CFStringRef CFErrorDomain CF_EXTENSIBLE_STRING_ENUM;
+
 /*!
 	@typedef CFErrorRef
 	    This is the type of a reference to CFErrors.  CFErrorRef is toll-free bridged with NSError.
@@ -51,10 +53,10 @@
 
 
 // Predefined domains; value of "code" will correspond to preexisting values in these domains.
-CF_EXPORT const CFStringRef kCFErrorDomainPOSIX		    CF_AVAILABLE(10_5, 2_0);
-CF_EXPORT const CFStringRef kCFErrorDomainOSStatus	    CF_AVAILABLE(10_5, 2_0);
-CF_EXPORT const CFStringRef kCFErrorDomainMach		    CF_AVAILABLE(10_5, 2_0);
-CF_EXPORT const CFStringRef kCFErrorDomainCocoa		    CF_AVAILABLE(10_5, 2_0);
+CF_EXPORT const CFErrorDomain kCFErrorDomainPOSIX		    CF_AVAILABLE(10_5, 2_0);
+CF_EXPORT const CFErrorDomain kCFErrorDomainOSStatus	    CF_AVAILABLE(10_5, 2_0);
+CF_EXPORT const CFErrorDomain kCFErrorDomainMach		    CF_AVAILABLE(10_5, 2_0);
+CF_EXPORT const CFErrorDomain kCFErrorDomainCocoa		    CF_AVAILABLE(10_5, 2_0);
 
 // Keys in userInfo for localizable, end-user presentable error messages. At minimum provide one of first two; ideally provide all three.
 CF_EXPORT const CFStringRef kCFErrorLocalizedDescriptionKey         CF_AVAILABLE(10_5, 2_0);   // Key to identify the end user-presentable description in userInfo.
@@ -82,7 +84,7 @@
 	@result A reference to the new CFError.
 */
 CF_EXPORT
-CFErrorRef CFErrorCreate(CFAllocatorRef allocator, CFStringRef domain, CFIndex code, CFDictionaryRef userInfo) CF_AVAILABLE(10_5, 2_0);
+CFErrorRef CFErrorCreate(CFAllocatorRef allocator, CFErrorDomain domain, CFIndex code, CFDictionaryRef userInfo) CF_AVAILABLE(10_5, 2_0);
 
 /*!
 	@function CFErrorCreateWithUserInfoKeysAndValues
@@ -97,7 +99,7 @@
 	@result A reference to the new CFError. numUserInfoValues CF types are gathered from each of userInfoKeys and userInfoValues to create the userInfo dictionary.
 */
 CF_EXPORT
-CFErrorRef CFErrorCreateWithUserInfoKeysAndValues(CFAllocatorRef allocator, CFStringRef domain, CFIndex code, const void *const *userInfoKeys, const void *const *userInfoValues, CFIndex numUserInfoValues) CF_AVAILABLE(10_5, 2_0);
+CFErrorRef CFErrorCreateWithUserInfoKeysAndValues(CFAllocatorRef allocator, CFErrorDomain domain, CFIndex code, const void *const *userInfoKeys, const void *const *userInfoValues, CFIndex numUserInfoValues) CF_AVAILABLE(10_5, 2_0);
 
 /*!
 	@function CFErrorGetDomain
@@ -106,7 +108,7 @@
 	@result The error domain of the CFError. Since this is a "Get" function, the caller shouldn't CFRelease the return value.
 */
 CF_EXPORT
-CFStringRef CFErrorGetDomain(CFErrorRef err) CF_AVAILABLE(10_5, 2_0);
+CFErrorDomain CFErrorGetDomain(CFErrorRef err) CF_AVAILABLE(10_5, 2_0);
 
 /*!
 	@function CFErrorGetCode
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFLocale.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFLocale.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFLocale.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFLocale.h	2016-06-01 05:51:58.000000000 +0200
@@ -8,10 +8,14 @@
 #include <CoreFoundation/CFBase.h>
 #include <CoreFoundation/CFArray.h>
 #include <CoreFoundation/CFDictionary.h>
+#include <CoreFoundation/CFNotificationCenter.h>
 
 CF_IMPLICIT_BRIDGING_ENABLED
 CF_EXTERN_C_BEGIN
 
+typedef CFStringRef CFLocaleIdentifier CF_EXTENSIBLE_STRING_ENUM;
+typedef CFStringRef CFLocaleKey CF_STRING_ENUM;
+
 typedef const struct CF_BRIDGED_TYPE(NSLocale) __CFLocale *CFLocaleRef;
 
 CF_EXPORT
@@ -65,25 +69,25 @@
 	// Returns the array of canonicalized CFString locale IDs that the user prefers.
 
 CF_EXPORT
-CFStringRef CFLocaleCreateCanonicalLanguageIdentifierFromString(CFAllocatorRef allocator, CFStringRef localeIdentifier);
+CFLocaleIdentifier CFLocaleCreateCanonicalLanguageIdentifierFromString(CFAllocatorRef allocator, CFStringRef localeIdentifier);
 	// Map an arbitrary language identification string (something close at
 	// least) to a canonical language identifier.
 
 CF_EXPORT
-CFStringRef CFLocaleCreateCanonicalLocaleIdentifierFromString(CFAllocatorRef allocator, CFStringRef localeIdentifier);
+CFLocaleIdentifier CFLocaleCreateCanonicalLocaleIdentifierFromString(CFAllocatorRef allocator, CFStringRef localeIdentifier);
 	// Map an arbitrary locale identification string (something close at
 	// least) to the canonical identifier.
 
 CF_EXPORT
-CFStringRef CFLocaleCreateCanonicalLocaleIdentifierFromScriptManagerCodes(CFAllocatorRef allocator, LangCode lcode, RegionCode rcode);
+CFLocaleIdentifier CFLocaleCreateCanonicalLocaleIdentifierFromScriptManagerCodes(CFAllocatorRef allocator, LangCode lcode, RegionCode rcode);
 	// Map a Mac OS LangCode and RegionCode to the canonical locale identifier.
 
 CF_EXPORT
-CFStringRef CFLocaleCreateLocaleIdentifierFromWindowsLocaleCode(CFAllocatorRef allocator, uint32_t lcid) CF_AVAILABLE(10_6, 4_0);
+CFLocaleIdentifier CFLocaleCreateLocaleIdentifierFromWindowsLocaleCode(CFAllocatorRef allocator, uint32_t lcid) CF_AVAILABLE(10_6, 4_0);
 	// Map a Windows LCID to the canonical locale identifier.
 
 CF_EXPORT
-uint32_t CFLocaleGetWindowsLocaleCodeFromLocaleIdentifier(CFStringRef localeIdentifier) CF_AVAILABLE(10_6, 4_0);
+uint32_t CFLocaleGetWindowsLocaleCodeFromLocaleIdentifier(CFLocaleIdentifier localeIdentifier) CF_AVAILABLE(10_6, 4_0);
 	// Map a locale identifier to a Windows LCID.
 
 typedef CF_ENUM(CFIndex, CFLocaleLanguageDirection) {
@@ -101,7 +105,7 @@
 CFLocaleLanguageDirection CFLocaleGetLanguageLineDirection(CFStringRef isoLangCode) CF_AVAILABLE(10_6, 4_0);
 
 CF_EXPORT
-CFDictionaryRef CFLocaleCreateComponentsFromLocaleIdentifier(CFAllocatorRef allocator, CFStringRef localeID);
+CFDictionaryRef CFLocaleCreateComponentsFromLocaleIdentifier(CFAllocatorRef allocator, CFLocaleIdentifier localeID);
 	// Parses a locale ID consisting of language, script, country, variant,
 	// and keyword/value pairs into a dictionary. The keys are the constant
 	// CFStrings corresponding to the locale ID components, and the values
@@ -111,7 +115,7 @@
 	// kCFLocaleCalendarIdentifier=kCFJapaneseCalendar.
 
 CF_EXPORT
-CFStringRef CFLocaleCreateLocaleIdentifierFromComponents(CFAllocatorRef allocator, CFDictionaryRef dictionary);
+CFLocaleIdentifier CFLocaleCreateLocaleIdentifierFromComponents(CFAllocatorRef allocator, CFDictionaryRef dictionary);
 	// Reverses the actions of CFLocaleCreateDictionaryFromLocaleIdentifier,
 	// creating a single string from the data in the dictionary. The
 	// dictionary {kCFLocaleLanguageCode=en, kCFLocaleCountryCode=US,
@@ -119,7 +123,7 @@
 	// "en_US@calendar=japanese".
 
 CF_EXPORT
-CFLocaleRef CFLocaleCreate(CFAllocatorRef allocator, CFStringRef localeIdentifier);
+CFLocaleRef CFLocaleCreate(CFAllocatorRef allocator, CFLocaleIdentifier localeIdentifier);
 	// Returns a CFLocaleRef for the locale named by the "arbitrary" locale identifier.
 
 CF_EXPORT
@@ -129,62 +133,64 @@
 	// or hold onto it.  In the future, there may be mutable locales.
 
 CF_EXPORT
-CFStringRef CFLocaleGetIdentifier(CFLocaleRef locale);
+CFLocaleIdentifier CFLocaleGetIdentifier(CFLocaleRef locale);
 	// Returns the locale's identifier.  This may not be the same string
 	// that the locale was created with (CFLocale may canonicalize it).
 
 CF_EXPORT
-CFTypeRef CFLocaleGetValue(CFLocaleRef locale, CFStringRef key);
+CFTypeRef CFLocaleGetValue(CFLocaleRef locale, CFLocaleKey key);
 	// Returns the value for the given key.  This is how settings and state
 	// are accessed via a CFLocale.  Values might be of any CF type.
 
 CF_EXPORT
-CFStringRef CFLocaleCopyDisplayNameForPropertyValue(CFLocaleRef displayLocale, CFStringRef key, CFStringRef value);
+CFStringRef CFLocaleCopyDisplayNameForPropertyValue(CFLocaleRef displayLocale, CFLocaleKey key, CFStringRef value);
 	// Returns the display name for the given value.  The key tells what
 	// the value is, and is one of the usual locale property keys, though
 	// not all locale property keys have values with display name values.
 
 
-CF_EXPORT const CFStringRef kCFLocaleCurrentLocaleDidChangeNotification CF_AVAILABLE(10_5, 2_0);
+CF_EXPORT const CFNotificationName kCFLocaleCurrentLocaleDidChangeNotification CF_AVAILABLE(10_5, 2_0);
 
 
 // Locale Keys
-CF_EXPORT const CFStringRef kCFLocaleIdentifier;
-CF_EXPORT const CFStringRef kCFLocaleLanguageCode;
-CF_EXPORT const CFStringRef kCFLocaleCountryCode;
-CF_EXPORT const CFStringRef kCFLocaleScriptCode;
-CF_EXPORT const CFStringRef kCFLocaleVariantCode;
-
-CF_EXPORT const CFStringRef kCFLocaleExemplarCharacterSet;
-CF_EXPORT const CFStringRef kCFLocaleCalendarIdentifier;
-CF_EXPORT const CFStringRef kCFLocaleCalendar;
-CF_EXPORT const CFStringRef kCFLocaleCollationIdentifier;
-CF_EXPORT const CFStringRef kCFLocaleUsesMetricSystem;
-CF_EXPORT const CFStringRef kCFLocaleMeasurementSystem; // "Metric" or "U.S."
-CF_EXPORT const CFStringRef kCFLocaleDecimalSeparator;
-CF_EXPORT const CFStringRef kCFLocaleGroupingSeparator;
-CF_EXPORT const CFStringRef kCFLocaleCurrencySymbol;
-CF_EXPORT const CFStringRef kCFLocaleCurrencyCode; // ISO 3-letter currency code
-CF_EXPORT const CFStringRef kCFLocaleCollatorIdentifier CF_AVAILABLE(10_6, 4_0);
-CF_EXPORT const CFStringRef kCFLocaleQuotationBeginDelimiterKey CF_AVAILABLE(10_6, 4_0);
-CF_EXPORT const CFStringRef kCFLocaleQuotationEndDelimiterKey CF_AVAILABLE(10_6, 4_0);
-CF_EXPORT const CFStringRef kCFLocaleAlternateQuotationBeginDelimiterKey CF_AVAILABLE(10_6, 4_0);
-CF_EXPORT const CFStringRef kCFLocaleAlternateQuotationEndDelimiterKey CF_AVAILABLE(10_6, 4_0);
+CF_EXPORT const CFLocaleKey kCFLocaleIdentifier;
+CF_EXPORT const CFLocaleKey kCFLocaleLanguageCode;
+CF_EXPORT const CFLocaleKey kCFLocaleCountryCode;
+CF_EXPORT const CFLocaleKey kCFLocaleScriptCode;
+CF_EXPORT const CFLocaleKey kCFLocaleVariantCode;
+
+CF_EXPORT const CFLocaleKey kCFLocaleExemplarCharacterSet;
+CF_EXPORT const CFLocaleKey kCFLocaleCalendarIdentifier;
+CF_EXPORT const CFLocaleKey kCFLocaleCalendar;
+CF_EXPORT const CFLocaleKey kCFLocaleCollationIdentifier;
+CF_EXPORT const CFLocaleKey kCFLocaleUsesMetricSystem;
+CF_EXPORT const CFLocaleKey kCFLocaleMeasurementSystem; // "Metric" or "U.S."
+CF_EXPORT const CFLocaleKey kCFLocaleDecimalSeparator;
+CF_EXPORT const CFLocaleKey kCFLocaleGroupingSeparator;
+CF_EXPORT const CFLocaleKey kCFLocaleCurrencySymbol;
+CF_EXPORT const CFLocaleKey kCFLocaleCurrencyCode; // ISO 3-letter currency code
+CF_EXPORT const CFLocaleKey kCFLocaleCollatorIdentifier CF_AVAILABLE(10_6, 4_0);
+CF_EXPORT const CFLocaleKey kCFLocaleQuotationBeginDelimiterKey CF_AVAILABLE(10_6, 4_0);
+CF_EXPORT const CFLocaleKey kCFLocaleQuotationEndDelimiterKey CF_AVAILABLE(10_6, 4_0);
+CF_EXPORT const CFLocaleKey kCFLocaleAlternateQuotationBeginDelimiterKey CF_AVAILABLE(10_6, 4_0);
+CF_EXPORT const CFLocaleKey kCFLocaleAlternateQuotationEndDelimiterKey CF_AVAILABLE(10_6, 4_0);
 
 // Values for kCFLocaleCalendarIdentifier
-CF_EXPORT const CFStringRef kCFGregorianCalendar;
-CF_EXPORT const CFStringRef kCFBuddhistCalendar;
-CF_EXPORT const CFStringRef kCFChineseCalendar;
-CF_EXPORT const CFStringRef kCFHebrewCalendar;
-CF_EXPORT const CFStringRef kCFIslamicCalendar;
-CF_EXPORT const CFStringRef kCFIslamicCivilCalendar;
-CF_EXPORT const CFStringRef kCFJapaneseCalendar;
-CF_EXPORT const CFStringRef kCFRepublicOfChinaCalendar CF_AVAILABLE(10_6, 4_0);
-CF_EXPORT const CFStringRef kCFPersianCalendar CF_AVAILABLE(10_6, 4_0);
-CF_EXPORT const CFStringRef kCFIndianCalendar CF_AVAILABLE(10_6, 4_0);
-CF_EXPORT const CFStringRef kCFISO8601Calendar CF_AVAILABLE(10_6, 4_0);
-CF_EXPORT const CFStringRef kCFIslamicTabularCalendar CF_AVAILABLE(10_10, 8_0);
-CF_EXPORT const CFStringRef kCFIslamicUmmAlQuraCalendar CF_AVAILABLE(10_10, 8_0);
+typedef CFStringRef CFCalendarIdentifier CF_STRING_ENUM;
+
+CF_EXPORT const CFCalendarIdentifier kCFGregorianCalendar;
+CF_EXPORT const CFCalendarIdentifier kCFBuddhistCalendar;
+CF_EXPORT const CFCalendarIdentifier kCFChineseCalendar;
+CF_EXPORT const CFCalendarIdentifier kCFHebrewCalendar;
+CF_EXPORT const CFCalendarIdentifier kCFIslamicCalendar;
+CF_EXPORT const CFCalendarIdentifier kCFIslamicCivilCalendar;
+CF_EXPORT const CFCalendarIdentifier kCFJapaneseCalendar;
+CF_EXPORT const CFCalendarIdentifier kCFRepublicOfChinaCalendar CF_AVAILABLE(10_6, 4_0);
+CF_EXPORT const CFCalendarIdentifier kCFPersianCalendar CF_AVAILABLE(10_6, 4_0);
+CF_EXPORT const CFCalendarIdentifier kCFIndianCalendar CF_AVAILABLE(10_6, 4_0);
+CF_EXPORT const CFCalendarIdentifier kCFISO8601Calendar CF_AVAILABLE(10_6, 4_0);
+CF_EXPORT const CFCalendarIdentifier kCFIslamicTabularCalendar CF_AVAILABLE(10_10, 8_0);
+CF_EXPORT const CFCalendarIdentifier kCFIslamicUmmAlQuraCalendar CF_AVAILABLE(10_10, 8_0);
 
 CF_EXTERN_C_END
 CF_IMPLICIT_BRIDGING_DISABLED
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFNotificationCenter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFNotificationCenter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFNotificationCenter.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFNotificationCenter.h	2016-05-20 07:43:20.000000000 +0200
@@ -11,9 +11,11 @@
 CF_IMPLICIT_BRIDGING_ENABLED
 CF_EXTERN_C_BEGIN
 
+typedef CFStringRef CFNotificationName CF_EXTENSIBLE_STRING_ENUM;
+
 typedef struct CF_BRIDGED_MUTABLE_TYPE(id) __CFNotificationCenter * CFNotificationCenterRef;
 
-typedef void (*CFNotificationCallback)(CFNotificationCenterRef center, void *observer, CFStringRef name, const void *object, CFDictionaryRef userInfo);
+typedef void (*CFNotificationCallback)(CFNotificationCenterRef center, void *observer, CFNotificationName name, const void *object, CFDictionaryRef userInfo);
 
 typedef CF_ENUM(CFIndex, CFNotificationSuspensionBehavior) {
     CFNotificationSuspensionBehaviorDrop = 1,
@@ -54,17 +56,17 @@
 
 CF_EXPORT void CFNotificationCenterAddObserver(CFNotificationCenterRef center, const void *observer, CFNotificationCallback callBack, CFStringRef name, const void *object, CFNotificationSuspensionBehavior suspensionBehavior);
 
-CF_EXPORT void CFNotificationCenterRemoveObserver(CFNotificationCenterRef center, const void *observer, CFStringRef name, const void *object);
+CF_EXPORT void CFNotificationCenterRemoveObserver(CFNotificationCenterRef center, const void *observer, CFNotificationName name, const void *object);
 CF_EXPORT void CFNotificationCenterRemoveEveryObserver(CFNotificationCenterRef center, const void *observer);
 
-CF_EXPORT void CFNotificationCenterPostNotification(CFNotificationCenterRef center, CFStringRef name, const void *object, CFDictionaryRef userInfo, Boolean deliverImmediately);
+CF_EXPORT void CFNotificationCenterPostNotification(CFNotificationCenterRef center, CFNotificationName name, const void *object, CFDictionaryRef userInfo, Boolean deliverImmediately);
 
 CF_ENUM(CFOptionFlags) {
     kCFNotificationDeliverImmediately = (1UL << 0),
     kCFNotificationPostToAllSessions = (1UL << 1)
 };
 
-CF_EXPORT void CFNotificationCenterPostNotificationWithOptions(CFNotificationCenterRef center, CFStringRef name, const void *object, CFDictionaryRef userInfo, CFOptionFlags options);
+CF_EXPORT void CFNotificationCenterPostNotificationWithOptions(CFNotificationCenterRef center, CFNotificationName name, const void *object, CFDictionaryRef userInfo, CFOptionFlags options);
 
 
 CF_EXTERN_C_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFNumberFormatter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFNumberFormatter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFNumberFormatter.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFNumberFormatter.h	2016-05-20 07:43:23.000000000 +0200
@@ -12,6 +12,8 @@
 CF_IMPLICIT_BRIDGING_ENABLED
 CF_EXTERN_C_BEGIN
 
+typedef CFStringRef CFNumberFormatterKey CF_STRING_ENUM;
+
 typedef struct CF_BRIDGED_MUTABLE_TYPE(id) __CFNumberFormatter *CFNumberFormatterRef;
 
 // CFNumberFormatters are not thread-safe.  Do not use one from multiple threads!
@@ -88,51 +90,51 @@
 
 
 CF_EXPORT
-void CFNumberFormatterSetProperty(CFNumberFormatterRef formatter, CFStringRef key, CFTypeRef value);
+void CFNumberFormatterSetProperty(CFNumberFormatterRef formatter, CFNumberFormatterKey key, CFTypeRef value);
 
 CF_EXPORT
-CFTypeRef CFNumberFormatterCopyProperty(CFNumberFormatterRef formatter, CFStringRef key);
+CFTypeRef CFNumberFormatterCopyProperty(CFNumberFormatterRef formatter, CFNumberFormatterKey key);
 	// Set and get various properties of the number formatter, the set of
 	// which may be expanded in the future.
 
-CF_EXPORT const CFStringRef kCFNumberFormatterCurrencyCode;		// CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterDecimalSeparator;	// CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterCurrencyDecimalSeparator; // CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterAlwaysShowDecimalSeparator; // CFBoolean
-CF_EXPORT const CFStringRef kCFNumberFormatterGroupingSeparator;	// CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterUseGroupingSeparator;	// CFBoolean
-CF_EXPORT const CFStringRef kCFNumberFormatterPercentSymbol;		// CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterZeroSymbol;		// CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterNaNSymbol;		// CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterInfinitySymbol;		// CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterMinusSign;		// CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterPlusSign;		// CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterCurrencySymbol;		// CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterExponentSymbol;		// CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterMinIntegerDigits;	// CFNumber
-CF_EXPORT const CFStringRef kCFNumberFormatterMaxIntegerDigits;	// CFNumber
-CF_EXPORT const CFStringRef kCFNumberFormatterMinFractionDigits;	// CFNumber
-CF_EXPORT const CFStringRef kCFNumberFormatterMaxFractionDigits;	// CFNumber
-CF_EXPORT const CFStringRef kCFNumberFormatterGroupingSize;		// CFNumber
-CF_EXPORT const CFStringRef kCFNumberFormatterSecondaryGroupingSize;	// CFNumber
-CF_EXPORT const CFStringRef kCFNumberFormatterRoundingMode;		// CFNumber
-CF_EXPORT const CFStringRef kCFNumberFormatterRoundingIncrement;	// CFNumber
-CF_EXPORT const CFStringRef kCFNumberFormatterFormatWidth;		// CFNumber
-CF_EXPORT const CFStringRef kCFNumberFormatterPaddingPosition;	// CFNumber
-CF_EXPORT const CFStringRef kCFNumberFormatterPaddingCharacter;	// CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterDefaultFormat;		// CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterMultiplier;		// CFNumber
-CF_EXPORT const CFStringRef kCFNumberFormatterPositivePrefix;		// CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterPositiveSuffix;		// CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterNegativePrefix;		// CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterNegativeSuffix;		// CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterPerMillSymbol;		// CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterInternationalCurrencySymbol; // CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterCurrencyGroupingSeparator CF_AVAILABLE(10_5, 2_0); // CFString
-CF_EXPORT const CFStringRef kCFNumberFormatterIsLenient CF_AVAILABLE(10_5, 2_0);		// CFBoolean
-CF_EXPORT const CFStringRef kCFNumberFormatterUseSignificantDigits CF_AVAILABLE(10_5, 2_0);	// CFBoolean
-CF_EXPORT const CFStringRef kCFNumberFormatterMinSignificantDigits CF_AVAILABLE(10_5, 2_0);	// CFNumber
-CF_EXPORT const CFStringRef kCFNumberFormatterMaxSignificantDigits CF_AVAILABLE(10_5, 2_0);	// CFNumber
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterCurrencyCode;		// CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterDecimalSeparator;	// CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterCurrencyDecimalSeparator; // CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterAlwaysShowDecimalSeparator; // CFBoolean
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterGroupingSeparator;	// CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterUseGroupingSeparator;	// CFBoolean
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterPercentSymbol;		// CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterZeroSymbol;		// CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterNaNSymbol;		// CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterInfinitySymbol;		// CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterMinusSign;		// CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterPlusSign;		// CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterCurrencySymbol;		// CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterExponentSymbol;		// CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterMinIntegerDigits;	// CFNumber
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterMaxIntegerDigits;	// CFNumber
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterMinFractionDigits;	// CFNumber
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterMaxFractionDigits;	// CFNumber
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterGroupingSize;		// CFNumber
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterSecondaryGroupingSize;	// CFNumber
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterRoundingMode;		// CFNumber
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterRoundingIncrement;	// CFNumber
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterFormatWidth;		// CFNumber
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterPaddingPosition;	// CFNumber
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterPaddingCharacter;	// CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterDefaultFormat;		// CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterMultiplier;		// CFNumber
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterPositivePrefix;		// CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterPositiveSuffix;		// CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterNegativePrefix;		// CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterNegativeSuffix;		// CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterPerMillSymbol;		// CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterInternationalCurrencySymbol; // CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterCurrencyGroupingSeparator CF_AVAILABLE(10_5, 2_0); // CFString
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterIsLenient CF_AVAILABLE(10_5, 2_0);		// CFBoolean
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterUseSignificantDigits CF_AVAILABLE(10_5, 2_0);	// CFBoolean
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterMinSignificantDigits CF_AVAILABLE(10_5, 2_0);	// CFNumber
+CF_EXPORT const CFNumberFormatterKey kCFNumberFormatterMaxSignificantDigits CF_AVAILABLE(10_5, 2_0);	// CFNumber
 
 typedef CF_ENUM(CFIndex, CFNumberFormatterRoundingMode) {
     kCFNumberFormatterRoundCeiling = 0,
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFPreferences.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFPreferences.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFPreferences.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFPreferences.h	2016-06-01 05:51:58.000000000 +0200
@@ -10,6 +10,7 @@
 #include <CoreFoundation/CFString.h>
 
 CF_IMPLICIT_BRIDGING_ENABLED
+CF_ASSUME_NONNULL_BEGIN
 CF_EXTERN_C_BEGIN
 
 CF_EXPORT
@@ -40,25 +41,25 @@
 it returns it; otherwise returns NULL.  Caller must release the
 returned value */
 CF_EXPORT
-CFPropertyListRef CFPreferencesCopyAppValue(CFStringRef key, CFStringRef applicationID);
+_Nullable CFPropertyListRef CFPreferencesCopyAppValue(CFStringRef key, CFStringRef applicationID);
 
 /* Convenience to interpret a preferences value as a boolean directly.
 Returns false if the key doesn't exist, or has an improper format; under
 those conditions, keyExistsAndHasValidFormat (if non-NULL) is set to false */
 CF_EXPORT
-Boolean CFPreferencesGetAppBooleanValue(CFStringRef key, CFStringRef applicationID, Boolean *keyExistsAndHasValidFormat);
+Boolean CFPreferencesGetAppBooleanValue(CFStringRef key, CFStringRef applicationID,  Boolean * _Nullable keyExistsAndHasValidFormat);
 
 /* Convenience to interpret a preferences value as an integer directly.
 Returns 0 if the key doesn't exist, or has an improper format; under
 those conditions, keyExistsAndHasValidFormat (if non-NULL) is set to false */
 CF_EXPORT
-CFIndex CFPreferencesGetAppIntegerValue(CFStringRef key, CFStringRef applicationID, Boolean *keyExistsAndHasValidFormat);
+CFIndex CFPreferencesGetAppIntegerValue(CFStringRef key, CFStringRef applicationID, Boolean * _Nullable keyExistsAndHasValidFormat);
 
 /* Sets the given value for the given key in the "normal" place for
 application preferences.  key must not be NULL.  If value is NULL,
 key is removed instead. */
 CF_EXPORT
-void CFPreferencesSetAppValue(CFStringRef key, CFPropertyListRef value, CFStringRef applicationID);
+void CFPreferencesSetAppValue(CFStringRef key, _Nullable CFPropertyListRef value, CFStringRef applicationID);
 
 /* Adds the preferences for the given suite to the app preferences for
    the specified application.  To write to the suite domain, use
@@ -80,40 +81,40 @@
 location specified by app-user-host is searched.  The returned
 CFType must be released by the caller when it is finished with it. */
 CF_EXPORT
-CFPropertyListRef CFPreferencesCopyValue(CFStringRef key, CFStringRef applicationID, CFStringRef userName, CFStringRef hostName);
+_Nullable CFPropertyListRef CFPreferencesCopyValue(CFStringRef key, CFStringRef applicationID, CFStringRef userName, CFStringRef hostName);
 
 /* Convenience to fetch multiple keys at once.  Keys in 
 keysToFetch that are not present in the returned dictionary
 are not present in the domain.  If keysToFetch is NULL, all
 keys are fetched. */
 CF_EXPORT
-CFDictionaryRef CFPreferencesCopyMultiple(CFArrayRef keysToFetch, CFStringRef applicationID, CFStringRef userName, CFStringRef hostName);
+CFDictionaryRef CFPreferencesCopyMultiple(_Nullable CFArrayRef keysToFetch, CFStringRef applicationID, CFStringRef userName, CFStringRef hostName);
 
 /* The primitive set function; all arguments except value must be
 non-NULL.  If value is NULL, the given key is removed */
 CF_EXPORT
-void CFPreferencesSetValue(CFStringRef key, CFPropertyListRef value, CFStringRef applicationID, CFStringRef userName, CFStringRef hostName);
+void CFPreferencesSetValue(CFStringRef key, _Nullable CFPropertyListRef value, CFStringRef applicationID, CFStringRef userName, CFStringRef hostName);
 
 /* Convenience to set multiple values at once.  Behavior is undefined
 if a key is in both keysToSet and keysToRemove */
 CF_EXPORT
-void CFPreferencesSetMultiple(CFDictionaryRef keysToSet, CFArrayRef keysToRemove, CFStringRef applicationID, CFStringRef userName, CFStringRef hostName);
+void CFPreferencesSetMultiple(_Nullable CFDictionaryRef keysToSet, _Nullable CFArrayRef keysToRemove, CFStringRef applicationID, CFStringRef userName, CFStringRef hostName);
 
 CF_EXPORT
 Boolean CFPreferencesSynchronize(CFStringRef applicationID, CFStringRef userName, CFStringRef hostName);
 
 /* Constructs and returns the list of the name of all applications
-which have preferences in the scope of the given user and host.
+which have preferences in the scope of the given user and host, or NULL if no applications are there.
 The returned value must be released by the caller; neither argument
-may be NULL. */
+may be NULL. Does not supported sandboxed applications. */
 CF_EXPORT
-CFArrayRef CFPreferencesCopyApplicationList(CFStringRef userName, CFStringRef hostName) CF_DEPRECATED(10_0, 10_9, 2_0, 7_0);
+_Nullable CFArrayRef CFPreferencesCopyApplicationList(CFStringRef userName, CFStringRef hostName) CF_DEPRECATED(10_0, 10_9, 2_0, 7_0);
 
 /* Constructs and returns the list of all keys set in the given
-location.  The returned value must be released by the caller;
+location, or NULL if no keys are set.  The returned value must be released by the caller;
 all arguments must be non-NULL */
 CF_EXPORT
-CFArrayRef CFPreferencesCopyKeyList(CFStringRef applicationID, CFStringRef userName, CFStringRef hostName);
+_Nullable CFArrayRef CFPreferencesCopyKeyList(CFStringRef applicationID, CFStringRef userName, CFStringRef hostName);
 
 #ifndef CF_OPEN_SOURCE
 
@@ -127,6 +128,7 @@
 #endif
 
 CF_EXTERN_C_END
+CF_ASSUME_NONNULL_END
 CF_IMPLICIT_BRIDGING_DISABLED
 
 #endif /* ! __COREFOUNDATION_CFPREFERENCES__ */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFRunLoop.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFRunLoop.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFRunLoop.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFRunLoop.h	2016-05-23 04:36:46.000000000 +0200
@@ -16,6 +16,8 @@
 CF_IMPLICIT_BRIDGING_ENABLED
 CF_EXTERN_C_BEGIN
 
+typedef CFStringRef CFRunLoopMode CF_EXTENSIBLE_STRING_ENUM;
+
 typedef struct CF_BRIDGED_MUTABLE_TYPE(id) __CFRunLoop * CFRunLoopRef;
 
 typedef struct CF_BRIDGED_MUTABLE_TYPE(id) __CFRunLoopSource * CFRunLoopSourceRef;
@@ -43,24 +45,24 @@
     kCFRunLoopAllActivities = 0x0FFFFFFFU
 };
 
-CF_EXPORT const CFStringRef kCFRunLoopDefaultMode;
-CF_EXPORT const CFStringRef kCFRunLoopCommonModes;
+CF_EXPORT const CFRunLoopMode kCFRunLoopDefaultMode;
+CF_EXPORT const CFRunLoopMode kCFRunLoopCommonModes;
 
 CF_EXPORT CFTypeID CFRunLoopGetTypeID(void);
 
 CF_EXPORT CFRunLoopRef CFRunLoopGetCurrent(void);
 CF_EXPORT CFRunLoopRef CFRunLoopGetMain(void);
 
-CF_EXPORT CFStringRef CFRunLoopCopyCurrentMode(CFRunLoopRef rl);
+CF_EXPORT CFRunLoopMode CFRunLoopCopyCurrentMode(CFRunLoopRef rl);
 
 CF_EXPORT CFArrayRef CFRunLoopCopyAllModes(CFRunLoopRef rl);
 
-CF_EXPORT void CFRunLoopAddCommonMode(CFRunLoopRef rl, CFStringRef mode);
+CF_EXPORT void CFRunLoopAddCommonMode(CFRunLoopRef rl, CFRunLoopMode mode);
 
-CF_EXPORT CFAbsoluteTime CFRunLoopGetNextTimerFireDate(CFRunLoopRef rl, CFStringRef mode);
+CF_EXPORT CFAbsoluteTime CFRunLoopGetNextTimerFireDate(CFRunLoopRef rl, CFRunLoopMode mode);
 
 CF_EXPORT void CFRunLoopRun(void);
-CF_EXPORT CFRunLoopRunResult CFRunLoopRunInMode(CFStringRef mode, CFTimeInterval seconds, Boolean returnAfterSourceHandled);
+CF_EXPORT CFRunLoopRunResult CFRunLoopRunInMode(CFRunLoopMode mode, CFTimeInterval seconds, Boolean returnAfterSourceHandled);
 CF_EXPORT Boolean CFRunLoopIsWaiting(CFRunLoopRef rl);
 CF_EXPORT void CFRunLoopWakeUp(CFRunLoopRef rl);
 CF_EXPORT void CFRunLoopStop(CFRunLoopRef rl);
@@ -69,17 +71,17 @@
 CF_EXPORT void CFRunLoopPerformBlock(CFRunLoopRef rl, CFTypeRef mode, void (^block)(void)) CF_AVAILABLE(10_6, 4_0); 
 #endif
 
-CF_EXPORT Boolean CFRunLoopContainsSource(CFRunLoopRef rl, CFRunLoopSourceRef source, CFStringRef mode);
-CF_EXPORT void CFRunLoopAddSource(CFRunLoopRef rl, CFRunLoopSourceRef source, CFStringRef mode);
-CF_EXPORT void CFRunLoopRemoveSource(CFRunLoopRef rl, CFRunLoopSourceRef source, CFStringRef mode);
-
-CF_EXPORT Boolean CFRunLoopContainsObserver(CFRunLoopRef rl, CFRunLoopObserverRef observer, CFStringRef mode);
-CF_EXPORT void CFRunLoopAddObserver(CFRunLoopRef rl, CFRunLoopObserverRef observer, CFStringRef mode);
-CF_EXPORT void CFRunLoopRemoveObserver(CFRunLoopRef rl, CFRunLoopObserverRef observer, CFStringRef mode);
-
-CF_EXPORT Boolean CFRunLoopContainsTimer(CFRunLoopRef rl, CFRunLoopTimerRef timer, CFStringRef mode);
-CF_EXPORT void CFRunLoopAddTimer(CFRunLoopRef rl, CFRunLoopTimerRef timer, CFStringRef mode);
-CF_EXPORT void CFRunLoopRemoveTimer(CFRunLoopRef rl, CFRunLoopTimerRef timer, CFStringRef mode);
+CF_EXPORT Boolean CFRunLoopContainsSource(CFRunLoopRef rl, CFRunLoopSourceRef source, CFRunLoopMode mode);
+CF_EXPORT void CFRunLoopAddSource(CFRunLoopRef rl, CFRunLoopSourceRef source, CFRunLoopMode mode);
+CF_EXPORT void CFRunLoopRemoveSource(CFRunLoopRef rl, CFRunLoopSourceRef source, CFRunLoopMode mode);
+
+CF_EXPORT Boolean CFRunLoopContainsObserver(CFRunLoopRef rl, CFRunLoopObserverRef observer, CFRunLoopMode mode);
+CF_EXPORT void CFRunLoopAddObserver(CFRunLoopRef rl, CFRunLoopObserverRef observer, CFRunLoopMode mode);
+CF_EXPORT void CFRunLoopRemoveObserver(CFRunLoopRef rl, CFRunLoopObserverRef observer, CFRunLoopMode mode);
+
+CF_EXPORT Boolean CFRunLoopContainsTimer(CFRunLoopRef rl, CFRunLoopTimerRef timer, CFRunLoopMode mode);
+CF_EXPORT void CFRunLoopAddTimer(CFRunLoopRef rl, CFRunLoopTimerRef timer, CFRunLoopMode mode);
+CF_EXPORT void CFRunLoopRemoveTimer(CFRunLoopRef rl, CFRunLoopTimerRef timer, CFRunLoopMode mode);
 
 typedef struct {
     CFIndex	version;
@@ -89,8 +91,8 @@
     CFStringRef	(*copyDescription)(const void *info);
     Boolean	(*equal)(const void *info1, const void *info2);
     CFHashCode	(*hash)(const void *info);
-    void	(*schedule)(void *info, CFRunLoopRef rl, CFStringRef mode);
-    void	(*cancel)(void *info, CFRunLoopRef rl, CFStringRef mode);
+    void	(*schedule)(void *info, CFRunLoopRef rl, CFRunLoopMode mode);
+    void	(*cancel)(void *info, CFRunLoopRef rl, CFRunLoopMode mode);
     void	(*perform)(void *info);
 } CFRunLoopSourceContext;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFSet.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFSet.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFSet.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFSet.h	2016-06-01 05:51:58.000000000 +0200
@@ -398,7 +398,7 @@
 		undefined.
 */
 CF_EXPORT
-void CFSetApplyFunction(CFSetRef theSet, CFSetApplierFunction applier, void *context);
+void CFSetApplyFunction(CFSetRef theSet, CFSetApplierFunction CF_NOESCAPE applier, void *context);
 
 /*!
 	@function CFSetAddValue
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFStream.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFStream.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFStream.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFStream.h	2016-06-01 05:51:59.000000000 +0200
@@ -17,6 +17,8 @@
 CF_IMPLICIT_BRIDGING_ENABLED
 CF_EXTERN_C_BEGIN
 
+typedef CFStringRef CFStreamPropertyKey CF_EXTENSIBLE_STRING_ENUM;
+
 typedef CF_ENUM(CFIndex, CFStreamStatus) {
     kCFStreamStatusNotOpen = 0,
     kCFStreamStatusOpening,  /* open is in-progress */
@@ -60,7 +62,7 @@
 
 /* Value will be a CFData containing all bytes thusfar written; used to recover the data written to a memory write stream. */
 CF_EXPORT
-const CFStringRef kCFStreamPropertyDataWritten;
+const CFStreamPropertyKey kCFStreamPropertyDataWritten;
 
 /* Pass kCFAllocatorNull for bytesDeallocator to prevent CFReadStream from deallocating bytes; otherwise, CFReadStream will deallocate bytes when the stream is destroyed */
 CF_EXPORT
@@ -86,25 +88,25 @@
 
 /* Property for file write streams; value should be a CFBoolean.  Set to TRUE to append to a file, rather than to replace its contents */
 CF_EXPORT
-const CFStringRef kCFStreamPropertyAppendToFile;
+const CFStreamPropertyKey kCFStreamPropertyAppendToFile;
 
 CF_EXPORT
-const CFStringRef kCFStreamPropertyFileCurrentOffset;   // Value is a CFNumber
+const CFStreamPropertyKey kCFStreamPropertyFileCurrentOffset;   // Value is a CFNumber
 
 
 /* Socket stream properties */
 
 /* Value will be a CFData containing the native handle */
 CF_EXPORT
-const CFStringRef kCFStreamPropertySocketNativeHandle;
+const CFStreamPropertyKey kCFStreamPropertySocketNativeHandle;
 
 /* Value will be a CFString, or NULL if unknown */
 CF_EXPORT
-const CFStringRef kCFStreamPropertySocketRemoteHostName;
+const CFStreamPropertyKey kCFStreamPropertySocketRemoteHostName;
 
 /* Value will be a CFNumber, or NULL if unknown */
 CF_EXPORT
-const CFStringRef kCFStreamPropertySocketRemotePortNumber;
+const CFStreamPropertyKey kCFStreamPropertySocketRemotePortNumber;
 
 CF_IMPLICIT_BRIDGING_DISABLED
 /* Socket streams; the returned streams are paired such that they use the same socket; pass NULL if you want only the read stream or the write stream */
@@ -158,7 +160,7 @@
    This call will block until at least one byte is available; it will NOT block
    until the entire buffer can be filled.  To avoid blocking, either poll using
    CFReadStreamHasBytesAvailable() or use the run loop and listen for the 
-   kCFStreamCanRead event for notification of data available. */
+   kCFStreamEventHasBytesAvailable event for notification of data available. */
 CF_EXPORT
 CFIndex CFReadStreamRead(CFReadStreamRef stream, UInt8 *buffer, CFIndex bufferLength);
 
@@ -183,7 +185,7 @@
    occurred, or 0 if the stream has been filled to capacity (for fixed-length
    streams).  If the stream is not full, this call will block until at least
    one byte is written.  To avoid blocking, either poll via CFWriteStreamCanAcceptBytes
-   or use the run loop and listen for the kCFStreamCanWrite event. */
+   or use the run loop and listen for the kCFStreamEventCanAcceptBytes event. */
 CF_EXPORT
 CFIndex CFWriteStreamWrite(CFWriteStreamRef stream, const UInt8 *buffer, CFIndex bufferLength);
 
@@ -196,16 +198,16 @@
    (like before the stream has been opened).  See the documentation for particular 
    properties to determine their get- and set-ability. */
 CF_EXPORT
-CFTypeRef CFReadStreamCopyProperty(CFReadStreamRef stream, CFStringRef propertyName);
+CFTypeRef CFReadStreamCopyProperty(CFReadStreamRef stream, CFStreamPropertyKey propertyName);
 CF_EXPORT
-CFTypeRef CFWriteStreamCopyProperty(CFWriteStreamRef stream, CFStringRef propertyName);
+CFTypeRef CFWriteStreamCopyProperty(CFWriteStreamRef stream, CFStreamPropertyKey propertyName);
 
 /* Returns TRUE if the stream recognizes and accepts the given property-value pair; 
    FALSE otherwise. */
 CF_EXPORT
-Boolean CFReadStreamSetProperty(CFReadStreamRef stream, CFStringRef propertyName, CFTypeRef propertyValue);
+Boolean CFReadStreamSetProperty(CFReadStreamRef stream, CFStreamPropertyKey propertyName, CFTypeRef propertyValue);
 CF_EXPORT
-Boolean CFWriteStreamSetProperty(CFWriteStreamRef stream, CFStringRef propertyName, CFTypeRef propertyValue);
+Boolean CFWriteStreamSetProperty(CFWriteStreamRef stream, CFStreamPropertyKey propertyName, CFTypeRef propertyValue);
 
 /* Asynchronous processing - If you wish to neither poll nor block, you may register 
    a client to hear about interesting events that occur on a stream.  Only one client
@@ -229,14 +231,15 @@
 Boolean CFWriteStreamSetClient(CFWriteStreamRef stream, CFOptionFlags streamEvents, CFWriteStreamClientCallBack clientCB, CFStreamClientContext *clientContext);
 
 CF_EXPORT
-void CFReadStreamScheduleWithRunLoop(CFReadStreamRef stream, CFRunLoopRef runLoop, CFStringRef runLoopMode);
+void CFReadStreamScheduleWithRunLoop(CFReadStreamRef stream, CFRunLoopRef runLoop, CFRunLoopMode runLoopMode);
 CF_EXPORT
-void CFWriteStreamScheduleWithRunLoop(CFWriteStreamRef stream, CFRunLoopRef runLoop, CFStringRef runLoopMode);
+void CFWriteStreamScheduleWithRunLoop(CFWriteStreamRef stream, CFRunLoopRef runLoop, CFRunLoopMode runLoopMode);
 
 CF_EXPORT
-void CFReadStreamUnscheduleFromRunLoop(CFReadStreamRef stream, CFRunLoopRef runLoop, CFStringRef runLoopMode);
+void CFReadStreamUnscheduleFromRunLoop(CFReadStreamRef stream, CFRunLoopRef runLoop, CFRunLoopMode runLoopMode);
 CF_EXPORT
-void CFWriteStreamUnscheduleFromRunLoop(CFWriteStreamRef stream, CFRunLoopRef runLoop, CFStringRef runLoopMode);
+void CFWriteStreamUnscheduleFromRunLoop(CFWriteStreamRef stream, CFRunLoopRef runLoop, CFRunLoopMode runLoopMode);
+
 
 /*
  * Specify the dispatch queue upon which the client callbacks will be invoked.
@@ -262,6 +265,7 @@
 CF_EXPORT
 dispatch_queue_t CFWriteStreamCopyDispatchQueue(CFWriteStreamRef stream) CF_AVAILABLE(10_9, 7_0);
 
+
 /* The following API is deprecated starting in 10.5; please use CFRead/WriteStreamCopyError(), above, instead */
 typedef CF_ENUM(CFIndex, CFStreamErrorDomain) {
     kCFStreamErrorDomainCustom = -1L,      /* custom to the kind of stream in question */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFString.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFString.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFString.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFString.h	2016-06-01 05:52:12.000000000 +0200
@@ -37,8 +37,9 @@
 for many reasons; for instance it's possible that for users running in different
 languages these sometimes return NULL; or in a future OS release the first two might
 switch to always returning NULL. Never observing NULL returns in your usages of these
-functions does not mean they won't ever return NULL. (But note the CFStringGetCharactersPtr()
-exception mentioned further below.)
+functions does not mean they won't ever return NULL. In fact, this happened with the 
+introduction of tagged pointer strings in OS X 10.10, and a year later iOS 9. 
+(But please note the CFStringGetCharactersPtr() exception mentioned further below.)
 
 In your usages of these functions, if you get a NULL return, use the non-Ptr version
 of the functions as shown in this example:
@@ -284,13 +285,13 @@
 details.
 */
 CF_EXPORT
-ConstStringPtr CFStringGetPascalStringPtr(CFStringRef theString, CFStringEncoding encoding);	/* May return NULL at any time; be prepared for NULL */
+ConstStringPtr CFStringGetPascalStringPtr(CFStringRef theString, CFStringEncoding encoding);  /* May return NULL at any time; be prepared for NULL, if not now, in some other time or place. See discussion at top of this file. */
 
 CF_EXPORT
-const char *CFStringGetCStringPtr(CFStringRef theString, CFStringEncoding encoding);		/* May return NULL at any time; be prepared for NULL */
+const char *CFStringGetCStringPtr(CFStringRef theString, CFStringEncoding encoding);  /* May return NULL at any time; be prepared for NULL, if not now, in some other time or place. See discussion at top of this file. */
 
 CF_EXPORT
-const UniChar *CFStringGetCharactersPtr(CFStringRef theString);					/* May return NULL at any time; be prepared for NULL */
+const UniChar *CFStringGetCharactersPtr(CFStringRef theString);  /* May return NULL at any time; be prepared for NULL, if not now, in some other time or place. See discussion at top of this file. */
 
 /* The primitive conversion routine; allows you to convert a string piece at a time
        into a fixed size buffer. Returns number of characters converted. 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFTimeZone.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFTimeZone.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFTimeZone.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFTimeZone.h	2016-05-23 04:36:46.000000000 +0200
@@ -11,6 +11,8 @@
 #include <CoreFoundation/CFDate.h>
 #include <CoreFoundation/CFDictionary.h>
 #include <CoreFoundation/CFString.h>
+#include <CoreFoundation/CFNotificationCenter.h>
+#include <CoreFoundation/CFLocale.h>
 
 CF_IMPLICIT_BRIDGING_ENABLED
 CF_EXTERN_C_BEGIN
@@ -82,7 +84,7 @@
 CFStringRef CFTimeZoneCopyLocalizedName(CFTimeZoneRef tz, CFTimeZoneNameStyle style, CFLocaleRef locale) CF_AVAILABLE(10_5, 2_0);
 
 CF_EXPORT
-const CFStringRef kCFTimeZoneSystemTimeZoneDidChangeNotification CF_AVAILABLE(10_5, 2_0);
+const CFNotificationName kCFTimeZoneSystemTimeZoneDidChangeNotification CF_AVAILABLE(10_5, 2_0);
 
 CF_EXTERN_C_END
 CF_IMPLICIT_BRIDGING_DISABLED
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFTree.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFTree.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFTree.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFTree.h	2016-05-20 07:42:52.000000000 +0200
@@ -211,7 +211,7 @@
 		undefined.
 */
 CF_EXPORT
-void CFTreeApplyFunctionToChildren(CFTreeRef tree, CFTreeApplierFunction applier, void *context);
+void CFTreeApplyFunctionToChildren(CFTreeRef tree, CFTreeApplierFunction CF_NOESCAPE applier, void *context);
 
 /*!
         @function CFTreeFindRoot
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFURL.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFURL.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFURL.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFURL.h	2016-06-01 05:52:12.000000000 +0200
@@ -55,7 +55,7 @@
 CF_EXPORT
 CFDataRef CFURLCreateData(CFAllocatorRef allocator, CFURLRef url, CFStringEncoding encoding, Boolean escapeWhitespace);
 
-/* Any escape sequences in URLString will be interpreted via UTF-8. */
+/* Any percent-escape sequences in URLString will be interpreted via UTF-8. URLString must be a valid URL string. */
 CF_EXPORT
 CFURLRef CFURLCreateWithString(CFAllocatorRef allocator, CFStringRef URLString, CFURLRef baseURL);
 
@@ -116,7 +116,7 @@
 CF_EXPORT
 CFURLRef CFURLCopyAbsoluteURL(CFURLRef relativeURL);
 
-/* Returns the URL's string. */
+/* Returns the URL's string. Percent-escape sequences are not removed. */
 CF_EXPORT
 CFStringRef CFURLGetString(CFURLRef anURL);
 
@@ -148,38 +148,38 @@
 If a given CFURL can be decomposed (that is, conforms to RFC 1808), you
 can ask for each of the four basic pieces (scheme, net location, path,
 and resource specifer) separately, as well as for its base URL.  The
-basic pieces are returned with any percent escape sequences still in
+basic pieces are returned with any percent-escape sequences still in
 place (although note that the scheme may not legally include any
-percent escapes); this is to allow the caller to distinguish between
-percent sequences that may have syntactic meaning if replaced by the
+percent-escapes); this is to allow the caller to distinguish between
+percent-escape sequences that may have syntactic meaning if replaced by the
 character being escaped (for instance, a '/' in a path component).
 Since only the individual schemes know which characters are
-syntactically significant, CFURL cannot safely replace any percent
+syntactically significant, CFURL cannot safely replace any percent-
 escape sequences.  However, you can use
 CFURLCreateStringByReplacingPercentEscapes() to create a new string with
-the percent escapes removed; see below.
+the percent-escapes removed; see below.
 
 If a given CFURL can not be decomposed, you can ask for its scheme and its
 resource specifier; asking it for its net location or path will return NULL.
 
 To get more refined information about the components of a decomposable
 CFURL, you may ask for more specific pieces of the URL, expressed with
-the percent escapes removed.  The available functions are CFURLCopyHostName(),
+the percent-escapes removed.  The available functions are CFURLCopyHostName(),
 CFURLGetPortNumber() (returns an Int32), CFURLCopyUserName(),
 CFURLCopyPassword(), CFURLCopyQuery(), CFURLCopyParameters(), and
 CFURLCopyFragment().  Because the parameters, query, and fragment of an
 URL may contain scheme-specific syntaxes, these methods take a second
 argument, giving a list of characters which should NOT be replaced if
-percent escaped.  For instance, the ftp parameter syntax gives simple
+percent-escaped.  For instance, the ftp parameter syntax gives simple
 key-value pairs as "<key>=<value>;"  Clearly if a key or value includes
 either '=' or ';', it must be escaped to avoid corrupting the meaning of
 the parameters, so the caller may request the parameter string as
 
 CFStringRef myParams = CFURLCopyParameters(ftpURL, CFSTR("=;%"));
 
-requesting that all percent escape sequences be replaced by the represented
+requesting that all percent-escape sequences be replaced by the represented
 characters, except for escaped '=', '%' or ';' characters.  Pass the empty
-string (CFSTR("")) to request that all percent escapes be replaced, or NULL
+string (CFSTR("")) to request that all percent-escapes be replaced, or NULL
 to request that none be.
 */
 
@@ -187,12 +187,10 @@
 CF_EXPORT
 Boolean CFURLCanBeDecomposed(CFURLRef anURL); 
 
-/* The next several methods leave any percent escape sequences intact */
-
 CF_EXPORT
 CFStringRef CFURLCopyScheme(CFURLRef anURL);
 
-/* NULL if CFURLCanBeDecomposed(anURL) is false */
+/* Percent-escape sequences are not removed. NULL if CFURLCanBeDecomposed(anURL) is false */
 CF_EXPORT
 CFStringRef CFURLCopyNetLocation(CFURLRef anURL); 
 
@@ -204,15 +202,17 @@
 /* the normal POSIX appearance); CFURLCopyStrictPath()'s return value omits any */
 /* leading slash, and uses isAbsolute to report whether the URL's path is absolute. */
 
-/* CFURLCopyFileSystemPath() returns the URL's path as a file system path for the */
-/* given path style.  All percent escape sequences are replaced.  The URL is not */
-/* resolved against its base before computing the path. */
+/* Percent-escape sequences are not removed. */
 CF_EXPORT
 CFStringRef CFURLCopyPath(CFURLRef anURL);
 
+/* Percent-escape sequences are not removed. */
 CF_EXPORT
 CFStringRef CFURLCopyStrictPath(CFURLRef anURL, Boolean *isAbsolute);
 
+/* CFURLCopyFileSystemPath() returns the URL's path as a file system path for the */
+/* given path style.  All percent-escape sequences are removed.  The URL is not */
+/* resolved against its base before computing the path. */
 CF_EXPORT
 CFStringRef CFURLCopyFileSystemPath(CFURLRef anURL, CFURLPathStyle pathStyle);
 
@@ -223,24 +223,29 @@
 
 /* Any additional resource specifiers after the path.  For URLs */
 /* that cannot be decomposed, this is everything except the scheme itself. */
+/* Percent-escape sequences are not removed. */
 CF_EXPORT
 CFStringRef CFURLCopyResourceSpecifier(CFURLRef anURL); 
 
+/* Percent-escape sequences are removed. */
 CF_EXPORT
 CFStringRef CFURLCopyHostName(CFURLRef anURL);
 
 CF_EXPORT
 SInt32 CFURLGetPortNumber(CFURLRef anURL); /* Returns -1 if no port number is specified */
 
+/* Percent-escape sequences are removed. */
 CF_EXPORT
 CFStringRef CFURLCopyUserName(CFURLRef anURL);
 
+/* Percent-escape sequences are removed. */
 CF_EXPORT
 CFStringRef CFURLCopyPassword(CFURLRef anURL);
 
-/* These remove all percent escape sequences except those for */
+/* CFURLCopyParameterString, CFURLCopyQueryString, and CFURLCopyFragment */
+/* remove all percent-escape sequences except those for */
 /* characters in charactersToLeaveEscaped.  If charactersToLeaveEscaped */
-/* is empty (""), all percent escape sequences are replaced by their */
+/* is empty (""), all percent-escape sequences are replaced by their */
 /* corresponding characters.  If charactersToLeaveEscaped is NULL, */
 /* then no escape sequences are removed at all */
 CF_EXPORT
@@ -252,16 +257,14 @@
 CF_EXPORT
 CFStringRef CFURLCopyFragment(CFURLRef anURL, CFStringRef charactersToLeaveEscaped);
 
+/* Percent-escape sequences are removed. */
 CF_EXPORT
 CFStringRef CFURLCopyLastPathComponent(CFURLRef url);
 
+/* Percent-escape sequences are removed. */
 CF_EXPORT
 CFStringRef CFURLCopyPathExtension(CFURLRef url);
 
-/* These functions all treat the base URL of the supplied url as */
-/* invariant.  In other words, the URL returned will always have */
-/* the same base as the URL supplied as an argument. */
-
 CF_EXPORT
 CFURLRef CFURLCreateCopyAppendingPathComponent(CFAllocatorRef allocator, CFURLRef url, CFStringRef pathComponent, Boolean isDirectory);
 
@@ -365,23 +368,23 @@
 CF_EXPORT
 CFRange CFURLGetByteRangeForComponent(CFURLRef url, CFURLComponentType component, CFRange *rangeIncludingSeparators);
 
-/* Returns a string with any percent escape sequences that do NOT */
+/* Returns a string with any percent-escape sequences that do NOT */
 /* correspond to characters in charactersToLeaveEscaped with their */
-/* equivalent.  Returns NULL on failure (if an invalid percent sequence */
+/* equivalent.  Returns NULL on failure (if an invalid percent-escape sequence */
 /* is encountered), or the original string (retained) if no characters */
-/* need to be replaced. Pass NULL to request that no percent escapes be */
-/* replaced, or the empty string (CFSTR("")) to request that all percent */
-/* escapes be replaced.  Uses UTF8 to interpret percent escapes. */
+/* need to be replaced. Pass NULL to request that no percent-escapes be */
+/* replaced, or the empty string (CFSTR("")) to request that all percent- */
+/* escapes be replaced.  Uses UTF8 to interpret percent-escapes. */
 CF_EXPORT
 CFStringRef CFURLCreateStringByReplacingPercentEscapes(CFAllocatorRef allocator, CFStringRef originalString, CFStringRef charactersToLeaveEscaped);
 
-/* As above, but allows you to specify the encoding to use when interpreting percent escapes */
+/* As above, but allows you to specify the encoding to use when interpreting percent-escapes */
 CF_EXPORT
 CFStringRef CFURLCreateStringByReplacingPercentEscapesUsingEncoding(CFAllocatorRef allocator, CFStringRef origString, CFStringRef charsToLeaveEscaped, CFStringEncoding encoding) CF_DEPRECATED(10_0, 10_11, 2_0, 9_0, "Use [NSString stringByRemovingPercentEncoding] or CFURLCreateStringByReplacingPercentEscapes() instead, which always uses the recommended UTF-8 encoding.");
 
 /* Creates a copy or originalString, replacing certain characters with */
-/* the equivalent percent escape sequence based on the encoding specified. */
-/* If the originalString does not need to be modified (no percent escape */
+/* the equivalent percent-escape sequence based on the encoding specified. */
+/* If the originalString does not need to be modified (no percent-escape */
 /* sequences are missing), may retain and return originalString. */
 /* If you are uncertain of the correct encoding, you should use UTF-8, */
 /* which is the encoding designated by RFC 2396 as the correct encoding */
@@ -744,7 +747,7 @@
 
 CF_EXPORT
 const CFStringRef kCFURLAttributeModificationDateKey CF_AVAILABLE(10_6, 4_0);
-    /* The time the resource's attributes were last modified (Read-write, value type CFDate) */
+    /* The time the resource's attributes were last modified (Read-only, value type CFDate) */
 
 CF_EXPORT
 const CFStringRef kCFURLLinkCountKey CF_AVAILABLE(10_6, 4_0);
@@ -771,20 +774,20 @@
     /* The label number assigned to the resource (Read-write, value type CFNumber) */
 
 CF_EXPORT
-const CFStringRef kCFURLLabelColorKey CF_AVAILABLE(10_6, 4_0);
-    /* The color of the assigned label (Currently not implemented, value type CGColorRef, must link with Application Services) */
+const CFStringRef kCFURLLabelColorKey API_DEPRECATED("Use NSURLLabelColorKey", macosx(10.6, 10.12), ios(4.0, 10.0), watchos(2.0, 3.0), tvos(9.0, 10.0));
+    /* not implemented */
 
 CF_EXPORT
 const CFStringRef kCFURLLocalizedLabelKey CF_AVAILABLE(10_6, 4_0);
     /* The user-visible label text (Read-only, value type CFString) */
 
 CF_EXPORT
-const CFStringRef kCFURLEffectiveIconKey CF_AVAILABLE(10_6, 4_0);
-    /* The icon normally displayed for the resource (Read-only, value type CGImageRef, must link with Application Services) */
+const CFStringRef kCFURLEffectiveIconKey API_DEPRECATED("Use NSURLEffectiveIconKey", macosx(10.6, 10.12), ios(4.0, 10.0), watchos(2.0, 3.0), tvos(9.0, 10.0));
+    /* not implemented */
 
 CF_EXPORT
-const CFStringRef kCFURLCustomIconKey CF_AVAILABLE(10_6, 4_0);
-    /* The custom icon assigned to the resource, if any (Currently not implemented, value type CGImageRef, must link with Application Services) */
+const CFStringRef kCFURLCustomIconKey API_DEPRECATED("Use NSURLCustomIconKey", macosx(10.6, 10.12), ios(4.0, 10.0), watchos(2.0, 3.0), tvos(9.0, 10.0));
+    /* not implemented */
 
 CF_EXPORT
 const CFStringRef kCFURLFileResourceIdentifierKey CF_AVAILABLE(10_7, 5_0);
@@ -827,6 +830,10 @@
     /* the URL's path as a file system path (Read-only, value type CFString) */
 
 CF_EXPORT
+const CFStringRef kCFURLCanonicalPathKey API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+    /* the URL's path as a canonical absolute file system path (Read-only, value type CFString) */
+
+CF_EXPORT
 const CFStringRef kCFURLIsMountTriggerKey CF_AVAILABLE(10_7, 4_0);
     /* true if this URL is a file system trigger directory. Traversing or opening a file system trigger will cause an attempt to mount a file system on the trigger directory. (Read-only, value type CFBoolean) */
 
@@ -1035,6 +1042,30 @@
 const CFStringRef kCFURLVolumeLocalizedNameKey CF_AVAILABLE(10_7, 5_0);
     /* The user-presentable name of the volume (Read-only, value type CFString) */
 
+CF_EXPORT
+const CFStringRef kCFURLVolumeIsEncryptedKey API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+    /* true if the volume is encrypted. (Read-only, value type CFBoolean) */
+
+CF_EXPORT
+const CFStringRef kCFURLVolumeIsRootFileSystemKey API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+    /* true if the volume is the root filesystem. (Read-only, value type CFBoolean) */
+
+CF_EXPORT
+const CFStringRef kCFURLVolumeSupportsCompressionKey API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+    /* true if the volume supports transparent decompression of compressed files using decmpfs. (Read-only, value type CFBoolean) */
+
+CF_EXPORT
+const CFStringRef kCFURLVolumeSupportsFileCloningKey API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+    /* true if the volume supports clonefile(2) (Read-only, value type CFBoolean) */
+
+CF_EXPORT
+const CFStringRef kCFURLVolumeSupportsSwapRenamingKey API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+    /* true if the volume supports renamex_np(2)'s RENAME_SWAP option (Read-only, value type CFBoolean) */
+
+CF_EXPORT
+const CFStringRef kCFURLVolumeSupportsExclusiveRenamingKey API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+    /* true if the volume supports renamex_np(2)'s RENAME_EXCL option (Read-only, value type CFBoolean) */
+
 /* UbiquitousItem Properties */
 
 CF_EXPORT
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CoreFoundation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CoreFoundation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CoreFoundation.h	2015-08-23 00:54:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CoreFoundation.h	2016-05-23 04:36:46.000000000 +0200
@@ -1,5 +1,10 @@
 /*	CoreFoundation.h
 	Copyright (c) 1998-2015, Apple Inc. All rights reserved.
+ 
+	Portions Copyright (c) 2014-2016 Apple Inc. and the Swift project authors
+	Licensed under Apache License v2.0 with Runtime Library Exception
+	See http://swift.org/LICENSE.txt for license information
+	See http://swift.org/CONTRIBUTORS.txt for the list of Swift project authors
 */
 
 #if !defined(__COREFOUNDATION_COREFOUNDATION__)
@@ -62,14 +67,15 @@
 #include <CoreFoundation/CFURLAccess.h>
 #include <CoreFoundation/CFUUID.h>
 #include <CoreFoundation/CFUtilities.h>
+#include <CoreFoundation/CFBundle.h>
 
 #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE)) || (TARGET_OS_EMBEDDED || TARGET_OS_IPHONE) || TARGET_OS_WIN32
-#include <CoreFoundation/CFBundle.h>
 #include <CoreFoundation/CFMessagePort.h>
 #include <CoreFoundation/CFPlugIn.h>
 #include <CoreFoundation/CFRunLoop.h>
 #include <CoreFoundation/CFStream.h>
 #include <CoreFoundation/CFSocket.h>
+#include <CoreFoundation/CFMachPort.h>
 
 #ifndef CF_OPEN_SOURCE
 #include <CoreFoundation/CFAttributedString.h>
@@ -82,7 +88,6 @@
 #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE)) || (TARGET_OS_EMBEDDED || TARGET_OS_IPHONE)
 #ifndef CF_OPEN_SOURCE
 #include <CoreFoundation/CFFileSecurity.h>
-#include <CoreFoundation/CFMachPort.h>
 #include <CoreFoundation/CFStringTokenizer.h>
 #include <CoreFoundation/CFFileDescriptor.h>
 #endif

```