#ScreenSaver.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ScreenSaver.framework/Headers/ScreenSaverView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ScreenSaver.framework/Headers/ScreenSaverView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ScreenSaver.framework/Headers/ScreenSaverView.h	2015-08-23 04:25:25.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ScreenSaver.framework/Headers/ScreenSaverView.h	2016-05-11 19:42:32.000000000 +0200
@@ -65,11 +65,11 @@
 static __inline__ NSRect SSCenteredRectInRect(NSRect innerRect, NSRect outerRect)
 {
 #if CGFLOAT_IS_DOUBLE
-    innerRect.origin.x = floor((outerRect.size.width - innerRect.size.width) / (CGFloat) 2.0);
-    innerRect.origin.y = floor((outerRect.size.height - innerRect.size.height) / (CGFloat) 2.0);
+    innerRect.origin.x = outerRect.origin.x + floorf((outerRect.size.width - innerRect.size.width) / 2);
+    innerRect.origin.y = outerRect.origin.y + floorf((outerRect.size.height - innerRect.size.height) / 2);
 #else
-    innerRect.origin.x = floorf((outerRect.size.width - innerRect.size.width) / (CGFloat) 2.0);
-    innerRect.origin.y = floorf((outerRect.size.height - innerRect.size.height) / (CGFloat) 2.0);
+    innerRect.origin.x = outerRect.origin.x + floorf((outerRect.size.width - innerRect.size.width) / 2);
+    innerRect.origin.y = outerRect.origin.y + floorf((outerRect.size.height - innerRect.size.height) / 2);
 #endif
     return innerRect;
 }

```