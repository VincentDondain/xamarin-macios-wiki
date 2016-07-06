#QuartzCore.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAAnimation.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAAnimation.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAAnimation.h	2016-06-06 06:02:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAAnimation.h	2016-06-28 08:20:54.000000000 +0200
@@ -41,7 +41,7 @@
  * lifetime of the animation object. Defaults to nil. See below for the
  * supported delegate methods. */
 
-@property(nullable, strong) id /*<CAAnimationDelegate>*/ delegate;
+@property(nullable, strong) id <CAAnimationDelegate> delegate;
 
 /* When true, the animation is removed from the render tree once its
  * active duration has passed. Defaults to YES. */
@@ -53,9 +53,7 @@
 /* Delegate methods for CAAnimation. */
 
 @protocol CAAnimationDelegate <NSObject>
-@end
-
-@interface NSObject (CAAnimationDelegate)
+@optional
 
 /* Called when the animation begins its active duration. */
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CADisplayLink.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CADisplayLink.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CADisplayLink.h	2016-06-06 06:02:29.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CADisplayLink.h	2016-06-28 08:20:54.000000000 +0200
@@ -30,13 +30,13 @@
  * to a single run-loop, but it may be added in multiple modes at once.
  * While added to a run-loop it will implicitly be retained. */
 
-- (void)addToRunLoop:(NSRunLoop *)runloop forMode:(NSString *)mode;
+- (void)addToRunLoop:(NSRunLoop *)runloop forMode:(NSRunLoopMode)mode;
 
 /* Removes the receiver from the given mode of the runloop. This will
  * implicitly release it when removed from the last mode it has been
  * registered for. */
 
-- (void)removeFromRunLoop:(NSRunLoop *)runloop forMode:(NSString *)mode;
+- (void)removeFromRunLoop:(NSRunLoop *)runloop forMode:(NSRunLoopMode)mode;
 
 /* Removes the object from all runloop modes (releasing the receiver if
  * it has been implicitly retained) and releases the 'target' object. */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CALayer.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CALayer.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CALayer.h	2016-06-06 06:02:29.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CALayer.h	2016-06-27 05:56:45.000000000 +0200
@@ -719,7 +719,7 @@
  * below (for those that it implements). The value of this property is
  * not retained. Default value is nil. */
 
-@property(nullable, weak) id /*<CALayerDelegate>*/ delegate;
+@property(nullable, weak) id <CALayerDelegate> delegate;
 
 /* When non-nil, a dictionary dereferenced to find property values that
  * aren't explicitly defined by the layer. (This dictionary may in turn
@@ -758,9 +758,7 @@
 /** Delegate methods. **/
 
 @protocol CALayerDelegate <NSObject>
-@end
-
-@interface NSObject (CALayerDelegate)
+@optional
 
 /* If defined, called by the default implementation of the -display
  * method, in which case it should implement the entire display

```