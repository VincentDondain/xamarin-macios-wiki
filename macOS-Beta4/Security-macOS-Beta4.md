#Security.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecKey.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecKey.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecKey.h	2016-07-13 01:23:36.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecKey.h	2016-07-25 06:55:49.000000000 +0200
@@ -555,7 +555,7 @@
  error parameter contains the reason.
 
 */
-_Nullable
+_Nullable CF_RETURNS_RETAINED
 SecKeyRef SecKeyDeriveFromPassword(CFStringRef password,
 	CFDictionaryRef parameters, CFErrorRef *error)
 	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);

```