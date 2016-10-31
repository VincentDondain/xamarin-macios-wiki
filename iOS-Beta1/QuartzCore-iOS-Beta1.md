#QuartzCore.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CADisplayLink.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CADisplayLink.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CADisplayLink.h	2016-10-01 08:56:08.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CADisplayLink.h	2016-10-24 05:44:17.000000000 +0200
@@ -68,7 +68,7 @@
  * DEPRECATED - use preferredFrameRate. */
 
 @property(nonatomic) NSInteger frameInterval
-  CA_AVAILABLE_BUT_DEPRECATED_IOS (3.1, 10.0, 2.0, 3.0, 9.0, 10.0, "use preferredFramesPerSecond");
+  CA_AVAILABLE_BUT_DEPRECATED_IOS (3.1, 10.0, 9.0, 10.0, 2.0, 3.0, "use preferredFramesPerSecond");
 
 /* Defines the desired callback rate in frames per second for this display link.
  * A value of 100.0 would result in 100 callbacks per second.

```