#CoreText.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFont.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFont.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFont.h	2016-07-09 02:38:24.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFont.h	2016-07-25 07:22:36.000000000 +0200
@@ -156,6 +156,8 @@
     @function   CTFontCreateWithName
     @abstract   Returns a new font reference for the given name.
 
+    @discussion This function uses font descriptor matching so only registered fonts can be returned; see CTFontManager.h for more information.
+
     @param      name
                 The font name for which you wish to create a new font reference. A valid PostScript name is preferred, although other font name types will be matched in a fallback manner.
 
@@ -211,6 +213,8 @@
     @function   CTFontCreateWithNameAndOptions
     @abstract   Returns a new font reference for the given name.
 
+    @discussion This function uses font descriptor matching so only registered fonts can be returned; see CTFontManager.h for more information.
+
     @param      name
                 The font name for which you wish to create a new font reference. A valid PostScript name is preferred, although other font name types will be matched in a fallback manner.
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreText.framework/Headers/SFNTLayoutTypes.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreText.framework/Headers/SFNTLayoutTypes.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreText.framework/Headers/SFNTLayoutTypes.h	2016-07-09 02:38:24.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreText.framework/Headers/SFNTLayoutTypes.h	2016-07-25 08:33:01.000000000 +0200
@@ -27,7 +27,7 @@
     The following values can be used to set run feature values. Note that unless the
     feature is defaulted differently in different fonts, the zero value for the
     selectors represents the default value. Consult the following URL for further info:
-    <http://developer.apple.com/fonts/registry/>
+    <https://developer.apple.com/fonts/TrueType-Reference-Manual/RM09/AppendixF.html>
 */
 
 

```