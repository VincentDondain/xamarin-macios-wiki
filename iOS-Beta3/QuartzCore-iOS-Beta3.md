#QuartzCore.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CADisplayLink.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CADisplayLink.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CADisplayLink.h	2016-06-28 08:20:54.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CADisplayLink.h	2016-07-11 07:07:00.000000000 +0200
@@ -68,7 +68,7 @@
  * DEPRECATED - use preferredFrameRate. */
 
 @property(nonatomic) NSInteger frameInterval
-  CA_AVAILABLE_BUT_DEPRECATED_IOS (3.1, 10.0, 2.0, 3.0, 9.0, 10.0, "use preferredFrameRate");
+  CA_AVAILABLE_BUT_DEPRECATED_IOS (3.1, 10.0, 2.0, 3.0, 9.0, 10.0, "use preferredFramesPerSecond");
 
 /* Defines the desired callback rate in frames per second for this display link.
  * A value of 100.0 would result in 100 callbacks per second.
@@ -77,9 +77,6 @@
  * cadence of the display hardware. CoreAnimation will make the best attempt
  * at issuing callbacks at the requested rate, but there are no guarantees. */
 
-/* Use preferredFramesPerSecond, not preferredFrameRate! */
-@property(nonatomic) float preferredFrameRate CA_DEPRECATED;
-
 @property(nonatomic) NSInteger preferredFramesPerSecond CA_AVAILABLE_IOS_STARTING(10.0, 10.0, 3.0);
 
 @end

```