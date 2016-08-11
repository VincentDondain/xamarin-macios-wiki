#CoreFoundation.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFDateFormatter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFDateFormatter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFDateFormatter.h	2015-10-02 23:20:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFDateFormatter.h	2016-05-20 07:42:52.000000000 +0200
@@ -43,6 +37,48 @@
 // should not rely on styles and localization, but set the format string and
 // use nothing but numbers.
 
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFURL.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFURL.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFURL.h	2015-10-02 23:20:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CFURL.h	2016-06-01 05:52:12.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CoreFoundation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CoreFoundation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CoreFoundation.h	2015-10-02 23:20:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreFoundation.framework/Headers/CoreFoundation.h	2016-05-20 07:43:23.000000000 +0200
```