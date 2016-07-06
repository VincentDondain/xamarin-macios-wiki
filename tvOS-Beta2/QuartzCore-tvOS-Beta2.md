#QuartzCore.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAAnimation.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAAnimation.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAAnimation.h	2016-06-06 06:02:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAAnimation.h	2016-06-28 08:20:54.000000000 +0200
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
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CABase.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CABase.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CABase.h	2016-06-06 06:02:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CABase.h	2016-06-27 05:56:57.000000000 +0200
@@ -19,88 +19,6 @@
 #include <Availability.h>
 #include <TargetConditionals.h>
 
-/* NOTE: remove these definitions before we GM */
-
-/* The earliest Mac SDK we support is 10.9 */
-
-#ifndef __MAC_10_10
-# define __MAC_10_10    101000
-#endif
-#ifndef __MAC_10_10_2
-# define __MAC_10_10_2  101002
-#endif
-#ifndef __MAC_10_10_3
-# define __MAC_10_10_3  101003
-#endif
-#ifndef __MAC_10_11
-# define __MAC_10_11    101100
-#endif
-#ifndef __MAC_10_11_3
-# define __MAC_10_11_3  101103
-#endif
-#ifndef __MAC_10_12
-# define __MAC_10_12    101200
-#endif
-
-/* The earliest iOS SDK we support is 7.0 */
-
-#ifndef __IPHONE_7_1
-# define __IPHONE_7_1   70100
-#endif
-#ifndef __IPHONE_8_0
-# define __IPHONE_8_0   80000
-#endif
-#ifndef __IPHONE_8_1
-# define __IPHONE_8_1   80100
-#endif
-#ifndef __IPHONE_8_2
-# define __IPHONE_8_2   80200
-#endif
-#ifndef __IPHONE_8_3
-# define __IPHONE_8_3   80300
-#endif
-#ifndef __IPHONE_8_4
-# define __IPHONE_8_4   80400
-#endif
-#ifndef __IPHONE_9_0
-# define __IPHONE_9_0   90000
-#endif
-#ifndef __IPHONE_9_1
-# define __IPHONE_9_1   90100
-#endif
-#ifndef __IPHONE_9_2
-# define __IPHONE_9_2   90200
-#endif
-#ifndef __IPHONE_9_3
-# define __IPHONE_9_3   90300
-#endif
-#ifndef __IPHONE_10_0
-# define __IPHONE_10_0  100000
-#endif
-
-/* NOTE: For compatibility, WatchOS and TVOS both have
-   __IPHONE_OS_VERSION_MIN_REQUIRED set to __IPHONE_9_0. When targetting newer
-   trains, be sure to use the appropriate checks. */
-
-/* The earliest watchOS SDK we support is 2.0. */
-
-#ifndef __WATCHOS_2_0
-# define __WATCHOS_2_0  20000
-#endif
-#ifndef __WATCHOS_3_0
-# define __WATCHOS_3_0  30000
-#endif
-
-#ifndef __TVOS_9_0
-# define __TVOS_9_0     90000
-#endif
-#ifndef __TVOS_9_2
-# define __TVOS_9_2     90200
-#endif
-#ifndef __TVOS_10_0
-# define __TVOS_10_0    100000
-#endif
-
 #define GET_CA_AVAIL_MACRO(_1,_2,_3,_4,NAME,...) NAME
 #define GET_CA_AVAIL_IOS_MACRO(_1,_2,_3,NAME,...) NAME
 #define CA_CLASS_AVAILABLE(...) __attribute__((visibility("default"))) GET_CA_AVAIL_MACRO(__VA_ARGS__, CA_AVAILABLE_STARTING4, CA_AVAILABLE_STARTING3, CA_AVAILABLE_STARTING2, CA_AVAILABLE_STARTING1)(__VA_ARGS__)
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CADisplayLink.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CADisplayLink.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CADisplayLink.h	2016-05-26 06:48:20.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CADisplayLink.h	2016-06-27 05:56:57.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CALayer.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CALayer.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CALayer.h	2016-06-06 06:02:29.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CALayer.h	2016-06-27 05:56:45.000000000 +0200
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