#CoreFoundation.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFAvailability.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFAvailability.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFAvailability.h	2016-06-27 07:17:00.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFAvailability.h	2016-07-10 07:31:29.000000000 +0200
@@ -18,6 +18,7 @@
 
 #if (TARGET_OS_MAC || TARGET_OS_EMBEDDED || TARGET_OS_IPHONE || TARGET_OS_WIN32)
 #include <Availability.h>
+#include <os/availability.h>
 
 // Even if unused, these must remain here for compatibility, because projects rely on them being included.
 #include <AvailabilityMacros.h>
@@ -133,7 +134,7 @@
     ...
 };
 */
-#define CF_ENUM(...) __CF_ENUM_GET_MACRO(__VA_ARGS__, __CF_NAMED_ENUM, __CF_ANON_ENUM)(__VA_ARGS__)
+#define CF_ENUM(...) __CF_ENUM_GET_MACRO(__VA_ARGS__, __CF_NAMED_ENUM, __CF_ANON_ENUM, )(__VA_ARGS__)
 
 #if __has_attribute(swift_wrapper)
 #define _CF_TYPED_ENUM __attribute__((swift_wrapper(enum)))
@@ -162,116 +163,4 @@
 #define CF_SWIFT_UNAVAILABLE(_msg)
 #endif
 
-
-//
-// New-Style Availability
-//
-#ifndef API_AVAILABLE
-/*
- Macros for defining which versions/platform a given symbol can be used.
- 
- @see http://clang.llvm.org/docs/AttributeReference.html#availability
- */
-
-//
-// API Introductions
-//
-// Use to specify the release that a particular API became available.
-//
-// Platform names:
-//   macosx, ios, tvos, watchos
-//
-// Examples:
-//    API_AVAILABLE(macosx(10.10))
-//    API_AVAILABLE(macosx(10.9), ios(10.0))
-//    API_AVAILABLE(macosx(10.4), ios(8.0), watchos(2.0), tvos(10.0))
-//
-#define __API_AVAILABLE_PLATFORM_macosx(x) macosx,introduced=x
-#define __API_AVAILABLE_PLATFORM_ios(x) ios,introduced=x
-#define __API_AVAILABLE_PLATFORM_watchos(x) watchos,introduced=x
-#define __API_AVAILABLE_PLATFORM_tvos(x) tvos,introduced=x
-
-#define __API_A(x) __attribute__((availability(__API_AVAILABLE_PLATFORM_##x)))
-#define __API_AVAILABLE1(x) __API_A(x)
-#define __API_AVAILABLE2(x,y) __API_A(x) __API_A(y)
-#define __API_AVAILABLE3(x,y,z)  __API_A(x) __API_A(y) __API_A(z)
-#define __API_AVAILABLE4(x,y,z,t) __API_A(x) __API_A(y) __API_A(z) __API_A(t)
-#define __API_AVAILABLE_GET_MACRO(_1,_2,_3,_4,NAME,...) NAME
-#define API_AVAILABLE(...) __API_AVAILABLE_GET_MACRO(__VA_ARGS__,__API_AVAILABLE4, __API_AVAILABLE3, __API_AVAILABLE2, __API_AVAILABLE1)(__VA_ARGS__)
-#pragma mark -
-
-
-//
-// API Deprecations
-//
-// Use to specify the release that a particular API became unavailable.
-//
-// Platform names:
-//   macosx, ios, tvos, watchos
-//
-// Examples:
-//
-//    API_DEPRECATED("No longer supported", macosx(10.4, 10.8))
-//    API_DEPRECATED("No longer supported", macosx(10.4, 10.8), ios(2.0, 3.0), watchos(2.0, 3.0), tvos(9.0, 10.0))
-//
-//    API_DEPRECATED_WITH_REPLACEMENT("-setName:", tvos(10.0, 10.4), ios(9.0, 10.0))
-//    API_DEPRECATED_WITH_REPLACEMENT("SomeClassName", macosx(10.4, 10.6), watchos(2.0, 3.0))
-//
-#define __API_DEPRECATED_PLATFORM_macosx(x,y) macosx,introduced=x,deprecated=y
-#define __API_DEPRECATED_PLATFORM_ios(x,y) ios,introduced=x,deprecated=y
-#define __API_DEPRECATED_PLATFORM_watchos(x,y) watchos,introduced=x,deprecated=y
-#define __API_DEPRECATED_PLATFORM_tvos(x,y) tvos,introduced=x,deprecated=y
-
-#define __API_D(msg,x) __attribute__((availability(__API_DEPRECATED_PLATFORM_##x,message=msg)))
-#define __API_DEPRECATED_MSG2(msg,x) __API_D(msg,x)
-#define __API_DEPRECATED_MSG3(msg,x,y) __API_D(msg,x) __API_D(msg,y)
-#define __API_DEPRECATED_MSG4(msg,x,y,z) __API_DEPRECATED_MSG3(msg,x,y) __API_D(msg,z)
-#define __API_DEPRECATED_MSG5(msg,x,y,z,t) __API_DEPRECATED_MSG4(msg,x,y,z) __API_D(msg,t)
-#define __API_DEPRECATED_MSG_GET_MACRO(_1,_2,_3,_4,_5,NAME,...) NAME
-#define API_DEPRECATED(...) __API_DEPRECATED_MSG_GET_MACRO(__VA_ARGS__,__API_DEPRECATED_MSG5,__API_DEPRECATED_MSG4,__API_DEPRECATED_MSG3,__API_DEPRECATED_MSG2,__API_DEPRECATED_MSG1)(__VA_ARGS__)
-
-#define __API_R(rep,x) __attribute__((availability(__API_DEPRECATED_PLATFORM_##x,replacement=rep)))
-#define __API_DEPRECATED_REP2(rep,x) __API_R(rep,x)
-#define __API_DEPRECATED_REP3(rep,x,y) __API_R(rep,x) __API_R(rep,y)
-#define __API_DEPRECATED_REP4(rep,x,y,z)  __API_DEPRECATED_REP3(rep,x,y) __API_R(rep,z)
-#define __API_DEPRECATED_REP5(rep,x,y,z,t) __API_DEPRECATED_REP4(rep,x,y,z) __API_R(rep,t)
-#define __API_DEPRECATED_REP_GET_MACRO(_1,_2,_3,_4,_5,NAME,...) NAME
-#define API_DEPRECATED_WITH_REPLACEMENT(...) __API_DEPRECATED_REP_GET_MACRO(__VA_ARGS__,__API_DEPRECATED_REP5,__API_DEPRECATED_REP4,__API_DEPRECATED_REP3,__API_DEPRECATED_REP2,__API_DEPRECATED_REP1)(__VA_ARGS__)
-
-#pragma mark -
-
-
-//
-// API Unavailability
-// Use to specify that an API is unavailable for a particular platform.
-//
-// Example:
-//    API_UNAVAILABLE(macosx)
-//    API_UNAVAILABLE(watchos, tvos)
-//
-#define __API_UNAVAILABLE_PLATFORM_macosx macosx,unavailable
-#define __API_UNAVAILABLE_PLATFORM_ios ios,unavailable
-#define __API_UNAVAILABLE_PLATFORM_watchos watchos,unavailable
-#define __API_UNAVAILABLE_PLATFORM_tvos tvos,unavailable
-
-#define __API_U(x) __attribute__((availability(__API_UNAVAILABLE_PLATFORM_##x)))
-#define __API_UNAVAILABLE1(x) __API_U(x)
-#define __API_UNAVAILABLE2(x,y) __API_U(x) __API_U(y)
-#define __API_UNAVAILABLE3(x,y,z) __API_UNAVAILABLE2(x,y) __API_U(z)
-#define __API_UNAVAILABLE_GET_MACRO(_1,_2,_3,NAME,...) NAME
-#define API_UNAVAILABLE(...) __API_UNAVAILABLE_GET_MACRO(__VA_ARGS__,__API_UNAVAILABLE3,__API_UNAVAILABLE2,__API_UNAVAILABLE1)(__VA_ARGS__)
-#pragma mark -
-
-
-//
-// Swift Deprecations
-// Use to specify that an API is deprecated for Swift.
-//
-// Example:
-//    API_DEPRECATED_FOR_SWIFT("Please use array literals instead")
-//
-#define API_DEPRECATED_FOR_SWIFT(msg) __attribute__((availability(swift,deprecated,message=msg)))
-
-#endif // API_AVAILABLE
-
 #endif // __COREFOUNDATION_CFAVAILABILITY__
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFString.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFString.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFString.h	2016-06-27 06:03:21.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFString.h	2016-07-12 05:21:15.000000000 +0200
@@ -238,8 +238,8 @@
 /* This function creates a mutable string that has a developer supplied and directly editable backing store.
 The string will be manipulated within the provided buffer (if any) until it outgrows capacity; then the
 externalCharactersAllocator will be consulted for more memory. When the CFString is deallocated, the
-buffer will be freed with the externalCharactersAllocator. Provide kCFAllocatorNull here to prevent the buffer
-from ever being reallocated or deallocated by CFString. See comments at top of this file for more info.
+buffer will be freed with the externalCharactersAllocator. If you provide kCFAllocatorNull here, and the buffer 
+needs to grow, then CFString will switch to using the default allocator. See comments at top of this file for more info.
 */
 CF_EXPORT
 CFMutableStringRef CFStringCreateMutableWithExternalCharactersNoCopy(CFAllocatorRef alloc, UniChar *chars, CFIndex numChars, CFIndex capacity, CFAllocatorRef externalCharactersAllocator);

```