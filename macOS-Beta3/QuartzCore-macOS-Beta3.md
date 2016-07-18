#QuartzCore.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAMetalLayer.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAMetalLayer.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAMetalLayer.h	2016-06-28 06:24:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAMetalLayer.h	2016-07-09 09:11:14.000000000 +0200
@@ -93,7 +93,8 @@
  * If non-nil, the rendered content will be colormatched to the colorspace of
  * the context containing this layer (typically the display's colorspace). */
 
-@property CGColorSpaceRef colorspace;
+@property (nullable) CGColorSpaceRef colorspace;
+
 
 /* If any rendering context on the screen has this enabled, all content will be
  * clamped to its NSScreen’s maximumExtendedDynamicRangeColorComponentValue
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAOpenGLLayer.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAOpenGLLayer.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAOpenGLLayer.h	2016-06-28 06:24:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAOpenGLLayer.h	2016-07-09 09:11:14.000000000 +0200
@@ -73,7 +73,7 @@
  * If non-nil, the rendered content will be colormatched to the colorspace of
  * the context containing this layer (typically the display's colorspace). */
 
-@property CGColorSpaceRef colorspace;
+@property (nullable) CGColorSpaceRef colorspace;
 
 /* If any rendering context on the screen has this enabled, all content will be
  * clamped to its NSScreen’s maximumExtendedDynamicRangeColorComponentValue

```