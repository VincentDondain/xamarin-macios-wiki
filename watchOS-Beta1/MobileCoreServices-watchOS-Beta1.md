#MobileCoreServices.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MobileCoreServices.framework/Headers/UTCoreTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MobileCoreServices.framework/Headers/UTCoreTypes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MobileCoreServices.framework/Headers/UTCoreTypes.h	2016-02-19 23:35:19.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MobileCoreServices.framework/Headers/UTCoreTypes.h	2016-05-26 06:51:33.000000000 +0200
@@ -731,7 +731,7 @@
 extern const CFStringRef kUTTypeICO                                  __OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_3_0);
 extern const CFStringRef kUTTypeRawImage                             __OSX_AVAILABLE_STARTING(__MAC_10_10,__IPHONE_8_0);
 extern const CFStringRef kUTTypeScalableVectorGraphics               __OSX_AVAILABLE_STARTING(__MAC_10_10,__IPHONE_8_0);
-extern const CFStringRef kUTTypeLivePhoto                            __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_9_1);
+extern const CFStringRef kUTTypeLivePhoto                            __OSX_AVAILABLE_STARTING(__MAC_10_12,__IPHONE_9_1);
 
 #pragma mark - Audiovisual content types
 /*
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MobileCoreServices.framework/Headers/UTType.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MobileCoreServices.framework/Headers/UTType.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MobileCoreServices.framework/Headers/UTType.h	2015-08-08 06:00:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MobileCoreServices.framework/Headers/UTType.h	2016-05-21 08:04:00.000000000 +0200
@@ -429,10 +429,7 @@
  *  Discussion:
  *    Compares two identified types for equality. Types are equal if
  *    their identifier strings are equal using a case-insensitive
- *    comparison. In addition, if one or both of the identifiers is a
- *    dynamic identifier, then the types are equal if either
- *    identifier's tag specification is a subset of the other
- *    identifier's tag specification.
+ *    comparison.
  *  
  *  Mac OS X threading:
  *    Thread safe since version 10.3

```