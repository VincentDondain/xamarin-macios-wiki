#QuartzCore.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CADisplayLink.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CADisplayLink.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CADisplayLink.h	2016-08-07 06:40:36.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CADisplayLink.h	2016-10-24 06:42:10.000000000 +0200
@@ -68,7 +68,7 @@
  * DEPRECATED - use preferredFrameRate. */
 
 @property(nonatomic) NSInteger frameInterval
-  CA_AVAILABLE_BUT_DEPRECATED_IOS (3.1, 10.0, 2.0, 3.0, 9.0, 10.0, "use preferredFramesPerSecond");
+  CA_AVAILABLE_BUT_DEPRECATED_IOS (3.1, 10.0, 9.0, 10.0, 2.0, 3.0, "use preferredFramesPerSecond");
 
 /* Defines the desired callback rate in frames per second for this display link.
  * A value of 100.0 would result in 100 callbacks per second.

```