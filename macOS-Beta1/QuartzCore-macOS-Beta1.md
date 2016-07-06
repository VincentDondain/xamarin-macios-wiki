#QuartzCore.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAAnimation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAAnimation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAAnimation.h	2015-08-27 05:25:24.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAAnimation.h	2016-06-06 06:02:04.000000000 +0200
@@ -1,17 +1,19 @@
 /* CoreAnimation - CAAnimation.h
 
-   Copyright (c) 2006-2015, Apple Inc.
+   Copyright (c) 2006-2016, Apple Inc.
    All rights reserved. */
 
 #import <QuartzCore/CALayer.h>
 #import <Foundation/NSObject.h>
 
 @class NSArray, NSString, CAMediaTimingFunction, CAValueFunction;
+@protocol CAAnimationDelegate;
 
 NS_ASSUME_NONNULL_BEGIN
 
 /** The base animation class. **/
 
+CA_CLASS_AVAILABLE (10.5, 2.0, 9.0, 2.0)
 @interface CAAnimation : NSObject
     <NSCoding, NSCopying, CAMediaTiming, CAAction>
 {
@@ -39,7 +41,7 @@
  * lifetime of the animation object. Defaults to nil. See below for the
  * supported delegate methods. */
 
-@property(nullable, strong) id delegate;
+@property(nullable, strong) id /*<CAAnimationDelegate>*/ delegate;
 
 /* When true, the animation is removed from the render tree once its
  * active duration has passed. Defaults to YES. */
@@ -50,6 +52,9 @@
 
 /* Delegate methods for CAAnimation. */
 
+@protocol CAAnimationDelegate <NSObject>
+@end
+
 @interface NSObject (CAAnimationDelegate)
 
 /* Called when the animation begins its active duration. */
@@ -68,6 +73,7 @@
 
 /** Subclass for property-based animations. **/
 
+CA_CLASS_AVAILABLE (10.5, 2.0, 9.0, 2.0)
 @interface CAPropertyAnimation : CAAnimation
 
 /* Creates a new animation object with its `keyPath' property set to
@@ -106,6 +112,7 @@
 
 /** Subclass for basic (single-keyframe) animations. **/
 
+CA_CLASS_AVAILABLE (10.5, 2.0, 9.0, 2.0)
 @interface CABasicAnimation : CAPropertyAnimation
 
 /* The objects defining the property values being interpolated between.
@@ -141,6 +148,7 @@
 
 /** General keyframe animation class. **/
 
+CA_CLASS_AVAILABLE (10.5, 2.0, 9.0, 2.0)
 @interface CAKeyframeAnimation : CAPropertyAnimation
 
 /* An array of objects providing the value of the animation function for
@@ -214,25 +222,26 @@
 /* `calculationMode' strings. */
 
 CA_EXTERN NSString * const kCAAnimationLinear
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAAnimationDiscrete
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAAnimationPaced
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAAnimationCubic
-    __OSX_AVAILABLE_STARTING (__MAC_10_7, __IPHONE_4_0);
+    CA_AVAILABLE_STARTING (10.7, 4.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAAnimationCubicPaced
-    __OSX_AVAILABLE_STARTING (__MAC_10_7, __IPHONE_4_0);
+    CA_AVAILABLE_STARTING (10.7, 4.0, 9.0, 2.0);
 
 /* `rotationMode' strings. */
 
 CA_EXTERN NSString * const kCAAnimationRotateAuto
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAAnimationRotateAutoReverse
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 /** Subclass for mass-spring animations. */
 
+CA_CLASS_AVAILABLE (10.11, 9.0, 9.0, 2.0)
 @interface CASpringAnimation : CABasicAnimation
 
 /* The mass of the object attached to the end of the spring. Must be greater
@@ -268,6 +277,7 @@
 
 /** Transition animation subclass. **/
 
+CA_CLASS_AVAILABLE (10.5, 2.0, 9.0, 2.0)
 @interface CATransition : CAAnimation
 
 /* The name of the transition. Current legal transition types include
@@ -304,28 +314,29 @@
 /* Common transition types. */
 
 CA_EXTERN NSString * const kCATransitionFade
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCATransitionMoveIn
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCATransitionPush
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCATransitionReveal
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 /* Common transition subtypes. */
 
 CA_EXTERN NSString * const kCATransitionFromRight
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCATransitionFromLeft
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCATransitionFromTop
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCATransitionFromBottom
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 
 /** Animation subclass for grouped animations. **/
 
+CA_CLASS_AVAILABLE (10.5, 2.0, 9.0, 2.0)
 @interface CAAnimationGroup : CAAnimation
 
 /* An array of CAAnimation objects. Each member of the array will run
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CABase.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CABase.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CABase.h	2015-08-27 05:25:24.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CABase.h	2016-06-03 05:03:17.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CABase.h
 
-   Copyright (c) 2006-2015, Apple Inc.
+   Copyright (c) 2006-2016, Apple Inc.
    All rights reserved. */
 
 #ifndef CABASE_H
@@ -19,6 +19,8 @@
 #include <Availability.h>
 #include <TargetConditionals.h>
 
+/* NOTE: remove these definitions before we GM */
+
 /* The earliest Mac SDK we support is 10.9 */
 
 #ifndef __MAC_10_10
@@ -33,6 +35,12 @@
 #ifndef __MAC_10_11
 # define __MAC_10_11    101100
 #endif
+#ifndef __MAC_10_11_3
+# define __MAC_10_11_3  101103
+#endif
+#ifndef __MAC_10_12
+# define __MAC_10_12    101200
+#endif
 
 /* The earliest iOS SDK we support is 7.0 */
 
@@ -57,20 +65,120 @@
 #ifndef __IPHONE_9_0
 # define __IPHONE_9_0   90000
 #endif
+#ifndef __IPHONE_9_1
+# define __IPHONE_9_1   90100
+#endif
+#ifndef __IPHONE_9_2
+# define __IPHONE_9_2   90200
+#endif
+#ifndef __IPHONE_9_3
+# define __IPHONE_9_3   90300
+#endif
+#ifndef __IPHONE_10_0
+# define __IPHONE_10_0  100000
+#endif
+
+/* NOTE: For compatibility, WatchOS and TVOS both have
+   __IPHONE_OS_VERSION_MIN_REQUIRED set to __IPHONE_9_0. When targetting newer
+   trains, be sure to use the appropriate checks. */
+
+/* The earliest watchOS SDK we support is 2.0. */
+
+#ifndef __WATCHOS_2_0
+# define __WATCHOS_2_0  20000
+#endif
+#ifndef __WATCHOS_3_0
+# define __WATCHOS_3_0  30000
+#endif
+
+#ifndef __TVOS_9_0
+# define __TVOS_9_0     90000
+#endif
+#ifndef __TVOS_9_2
+# define __TVOS_9_2     90200
+#endif
+#ifndef __TVOS_10_0
+# define __TVOS_10_0    100000
+#endif
+
+#define GET_CA_AVAIL_MACRO(_1,_2,_3,_4,NAME,...) NAME
+#define GET_CA_AVAIL_IOS_MACRO(_1,_2,_3,NAME,...) NAME
+#define CA_CLASS_AVAILABLE(...) __attribute__((visibility("default"))) GET_CA_AVAIL_MACRO(__VA_ARGS__, CA_AVAILABLE_STARTING4, CA_AVAILABLE_STARTING3, CA_AVAILABLE_STARTING2, CA_AVAILABLE_STARTING1)(__VA_ARGS__)
+#define CA_AVAILABLE_STARTING(...) GET_CA_AVAIL_MACRO(__VA_ARGS__, CA_AVAILABLE_STARTING4, CA_AVAILABLE_STARTING3, CA_AVAILABLE_STARTING2, CA_AVAILABLE_STARTING1)(__VA_ARGS__)
+#define CA_AVAILABLE_STARTING1(m) __OSX_AVAILABLE(m)
+#define CA_AVAILABLE_STARTING2(m,i) __OSX_AVAILABLE(m) __IOS_AVAILABLE(i)
+#define CA_AVAILABLE_STARTING3(m,i,t) __OSX_AVAILABLE(m) __IOS_AVAILABLE(i) __TVOS_AVAILABLE(t)
+#define CA_AVAILABLE_STARTING4(m,i,t,w) __OSX_AVAILABLE(m) __IOS_AVAILABLE(i) __TVOS_AVAILABLE(t) __WATCHOS_AVAILABLE(w)
+
+#define CA_CLASS_AVAILABLE_IOS(...) __attribute__((visibility("default"))) GET_CA_AVAIL_IOS_MACRO(__VA_ARGS__, CA_AVAILABLE_IOS_STARTING3, CA_AVAILABLE_IOS_STARTING2, CA_AVAILABLE_IOS_STARTING1)(__VA_ARGS__)
+#define CA_AVAILABLE_IOS_STARTING(...) GET_CA_AVAIL_IOS_MACRO(__VA_ARGS__, CA_AVAILABLE_IOS_STARTING3, CA_AVAILABLE_IOS_STARTING2, CA_AVAILABLE_IOS_STARTING1)(__VA_ARGS__)
+#define CA_AVAILABLE_IOS_STARTING1(i) __IOS_AVAILABLE(i)
+#define CA_AVAILABLE_IOS_STARTING2(i,t) __IOS_AVAILABLE(i) __TVOS_AVAILABLE(t)
+#define CA_AVAILABLE_IOS_STARTING3(i,t,w) __IOS_AVAILABLE(i) __TVOS_AVAILABLE(t) __WATCHOS_AVAILABLE(w)
+
+#define GET_CA_AVAIL_BUT_DEPR_MACRO(_1,_2,_3,_4,_5,_6,_7,_8,_9,NAME,...) NAME
+#define GET_CA_AVAIL_BUT_DEPR_IOS_MACRO(_1,_2,_3,_4,_5,_6,_7,NAME,...) NAME
+#define CA_AVAILABLE_BUT_DEPRECATED(...) GET_CA_AVAIL_BUT_DEPR_MACRO(__VA_ARGS__, CA_AVAILABLE_BUT_DEPRECATED9, CA_AVAILABLE_BUT_DEPRECATED8, CA_AVAILABLE_BUT_DEPRECATED7, CA_AVAILABLE_BUT_DEPRECATED6, CA_AVAILABLE_BUT_DEPRECATED5, CA_AVAILABLE_BUT_DEPRECATED4, CA_AVAILABLE_BUT_DEPRECATED3, CA_AVAILABLE_BUT_DEPRECATED2, CA_AVAILABLE_BUT_DEPRECATED1)(__VA_ARGS__)
+#define CA_AVAILABLE_BUT_DEPRECATED1(m0)
+#define CA_AVAILABLE_BUT_DEPRECATED2(m0,m1)
+#define CA_AVAILABLE_BUT_DEPRECATED3(m0,m1,w) __OSX_DEPRECATED(m0,m1,w)
+#define CA_AVAILABLE_BUT_DEPRECATED4(m0,m1,i0,i1)
+#define CA_AVAILABLE_BUT_DEPRECATED5(m0,m1,i0,i1,w) __OSX_DEPRECATED(m0,m1,w) __IOS_DEPRECATED(i0,i1,w)
+#define CA_AVAILABLE_BUT_DEPRECATED6(m0,m1,i0,i1,t0,t1)
+#define CA_AVAILABLE_BUT_DEPRECATED7(m0,m1,i0,i1,t0,t1,w) __OSX_DEPRECATED(m0,m1,w) __IOS_DEPRECATED(i0,i1,w) __TVOS_DEPRECATED(t0,t1,w)
+#define CA_AVAILABLE_BUT_DEPRECATED8(m0,m1,i0,i1,t0,t1,w0,w1)
+#define CA_AVAILABLE_BUT_DEPRECATED9(m0,m1,i0,i1,t0,t1,w0,w1,w) __OSX_DEPRECATED(m0,m1,w) __IOS_DEPRECATED(i0,i1,w) __TVOS_DEPRECATED(t0,t1,w) __WATCHOS_DEPRECATED(w0,w1,w)
+
+#define CA_AVAILABLE_BUT_DEPRECATED_IOS(...) GET_CA_AVAIL_BUT_DEPR_IOS_MACRO(__VA_ARGS__, CA_AVAILABLE_BUT_DEPRECATED_IOS7, CA_AVAILABLE_BUT_DEPRECATED_IOS6, CA_AVAILABLE_BUT_DEPRECATED_IOS5, CA_AVAILABLE_BUT_DEPRECATED_IOS4, CA_AVAILABLE_BUT_DEPRECATED_IOS3, CA_AVAILABLE_BUT_DEPRECATED_IOS2, CA_AVAILABLE_BUT_DEPRECATED_IOS1)(__VA_ARGS__)
+#define CA_AVAILABLE_BUT_DEPRECATED_IOS1(i0)
+#define CA_AVAILABLE_BUT_DEPRECATED_IOS2(i0,i1)
+#define CA_AVAILABLE_BUT_DEPRECATED_IOS3(i0,i1,w) __IOS_DEPRECATED(i0,i1,w)
+#define CA_AVAILABLE_BUT_DEPRECATED_IOS4(i0,i1,t0,t1)
+#define CA_AVAILABLE_BUT_DEPRECATED_IOS5(i0,i1,t0,t1,w) __IOS_DEPRECATED(i0,i1,w) __TVOS_DEPRECATED(t0,t1,w)
+#define CA_AVAILABLE_BUT_DEPRECATED_IOS6(i0,i1,t0,t1,w0,w1)
+#define CA_AVAILABLE_BUT_DEPRECATED_IOS7(i0,i1,t0,t1,w0,w1,w) __IOS_DEPRECATED(i0,i1,w) __TVOS_DEPRECATED(t0,t1,w) __WATCHOS_DEPRECATED(w0,w1,w)
 
 #ifdef CA_BUILDING_CA
 # undef __OSX_AVAILABLE_STARTING
 # undef __OSX_AVAILABLE_BUT_DEPRECATED
+# undef CA_AVAILABLE_STARTING
+# undef CA_AVAILABLE_IOS_STARTING
+# undef CA_AVAILABLE_BUT_DEPRECATED_STARTING
+# undef CA_AVAILABLE_BUT_DEPREDATED_IOS
 #endif
 #ifndef __OSX_AVAILABLE_STARTING
-# define __OSX_AVAILABLE_STARTING(m,i)
+# define __OSX_AVAILABLE_STARTING(m0,i)
 # define __OSX_AVAILABLE_BUT_DEPRECATED(m0,m1,i0,i1)
+# define CA_AVAILABLE_STARTING(...)
+# define CA_AVAILABLE_IOS_STARTING(...)
+# define CA_AVAILABLE_BUT_DEPRECATED_STARTING(...)
+# define CA_AVAILABLE_BUT_DEPREDATED_IOS(...)
+#endif
+
+/* Clunky, but we have no better way of specifying OSX only. */
+
+#if !TARGET_OS_IPHONE && !TARGET_OS_WATCH && !TARGET_OS_TV
+# define CA_OSX_VERSION(v) ((v) > 0 && MAC_OS_X_VERSION_MIN_REQUIRED >= (v))
+#else
+# define CA_OSX_VERSION(v) (0)
+#endif
+
+#if TARGET_OS_IPHONE
+# define CA_IOS_VERSION(v) ((v) > 0 && __IPHONE_OS_VERSION_MIN_REQUIRED >= (v))
+#else
+# define CA_IOS_VERSION(v) (0)
+#endif
+
+#if TARGET_OS_TV
+# define CA_TV_VERSION(v) ((v) > 0 && __TV_OS_VERSION_MIN_REQUIRED >= (v))
+#else
+# define CA_TV_VERSION(v) (0)
 #endif
 
-#if !TARGET_OS_IPHONE
-#define CA_OS_VERSION(m, i) ((m) > 0 && MAC_OS_X_VERSION_MIN_REQUIRED >= (m))
+#if TARGET_OS_WATCH
+# define CA_WATCH_VERSION(v) ((v) > 0 && __WATCH_OS_VERSION_MIN_REQUIRED >= (v))
 #else
-#define CA_OS_VERSION(m, i) ((i) > 0 && __IPHONE_OS_VERSION_MIN_REQUIRED >= (i))
+# define CA_WATCH_VERSION(v) (0)
 #endif
 
 #ifdef __cplusplus
@@ -89,7 +197,7 @@
 #endif
 
 #ifndef CA_EXTERN
-# define CA_EXTERN extern
+# define CA_EXTERN extern __attribute__((visibility("default")))
 #endif
 
 #ifndef CA_INLINE
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAConstraintLayoutManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAConstraintLayoutManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAConstraintLayoutManager.h	2015-08-27 05:25:25.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAConstraintLayoutManager.h	2016-06-03 05:03:16.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CAConstraintLayoutManager.h
 
-   Copyright (c) 2006-2015, Apple Inc.
+   Copyright (c) 2006-2016, Apple Inc.
    All rights reserved. */
 
 #import <QuartzCore/CALayer.h>
@@ -56,6 +56,7 @@
 
 /** The constraint-based layout manager. **/
 
+CA_CLASS_AVAILABLE (10.5)
 @interface CAConstraintLayoutManager : NSObject
 
 /* Returns a new layout manager object. */
@@ -66,6 +67,7 @@
 
 /** The class representing a single layout constraint. **/
 
+CA_CLASS_AVAILABLE (10.5)
 @interface CAConstraint : NSObject <NSCoding>
 {
 @private
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAEmitterBehavior.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAEmitterBehavior.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAEmitterBehavior.h	2015-08-27 05:25:24.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAEmitterBehavior.h	2016-06-03 05:03:16.000000000 +0200
@@ -1,12 +1,13 @@
 /* CoreAnimation - CAEmitterBehavior.h
 
-   Copyright (c) 2013-2015, Apple Inc.
+   Copyright (c) 2013-2016, Apple Inc.
    All rights reserved. */
 
 #import <QuartzCore/CALayer.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
+CA_CLASS_AVAILABLE (10.9, 7.0, 9.0, 2.0)
 @interface CAEmitterBehavior : NSObject <NSCoding>
 {
 @private
@@ -110,9 +111,7 @@
  *
  * For spot-lights:
  *   NSNumber directionLatitude, directionLongitude: the light's direction.
- *   NSNumber coneAngle, coneEdgeSoftness: the spot's lighting cone.
- *
- * See CALight.h for more description of the lighting behavior. */
+ *   NSNumber coneAngle, coneEdgeSoftness: the spot's lighting cone. */
 
 CA_EXTERN NSString * const kCAEmitterBehaviorLight;
 
@@ -129,4 +128,13 @@
 
 CA_EXTERN NSString * const kCAEmitterBehaviorAttractor;
 
+/* `simpleAttractor': simple radial force field.
+ *
+ * NSNumber stiffness: the spring stiffness.
+ * NSNumber radius: attractor radius, no effect inside.
+ * CGPoint position: the attractor's 2D position.
+ * NSNumber falloff: falloff value. */
+
+CA_EXTERN NSString * const kCAEmitterBehaviorSimpleAttractor;
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAEmitterCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAEmitterCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAEmitterCell.h	2015-08-27 05:25:24.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAEmitterCell.h	2016-05-26 06:48:20.000000000 +0200
@@ -1,12 +1,13 @@
 /* CoreAnimation - CAEmitterCell.h
 
-   Copyright (c) 2007-2015, Apple Inc.
+   Copyright (c) 2007-2016, Apple Inc.
    All rights reserved. */
 
 #import <QuartzCore/CALayer.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
+CA_CLASS_AVAILABLE (10.6, 5.0, 9.0, 2.0)
 @interface CAEmitterCell : NSObject <NSCoding, CAMediaTiming>
 {
 @private
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAEmitterLayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAEmitterLayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAEmitterLayer.h	2015-08-27 05:25:25.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAEmitterLayer.h	2016-05-26 06:28:17.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CAEmitterLayer.h
 
-   Copyright (c) 2007-2015, Apple Inc.
+   Copyright (c) 2007-2016, Apple Inc.
    All rights reserved. */
 
 /* Particle emitter layer.
@@ -20,6 +20,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+CA_CLASS_AVAILABLE (10.6, 5.0, 9.0, 2.0)
 @interface CAEmitterLayer : CALayer
 
 /* The array of emitter cells attached to the layer. Each object must
@@ -103,40 +104,40 @@
 /** `emitterShape' values. **/
 
 CA_EXTERN NSString * const kCAEmitterLayerPoint
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_5_0);
+    CA_AVAILABLE_STARTING (10.6, 5.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAEmitterLayerLine
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_5_0);
+    CA_AVAILABLE_STARTING (10.6, 5.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAEmitterLayerRectangle
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_5_0);
+    CA_AVAILABLE_STARTING (10.6, 5.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAEmitterLayerCuboid
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_5_0);
+    CA_AVAILABLE_STARTING (10.6, 5.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAEmitterLayerCircle
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_5_0);
+    CA_AVAILABLE_STARTING (10.6, 5.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAEmitterLayerSphere
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_5_0);
+    CA_AVAILABLE_STARTING (10.6, 5.0, 9.0, 2.0);
 
 /** `emitterMode' values. **/
 
 CA_EXTERN NSString * const kCAEmitterLayerPoints
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_5_0);
+    CA_AVAILABLE_STARTING (10.6, 5.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAEmitterLayerOutline
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_5_0);
+    CA_AVAILABLE_STARTING (10.6, 5.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAEmitterLayerSurface
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_5_0);
+    CA_AVAILABLE_STARTING (10.6, 5.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAEmitterLayerVolume
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_5_0);
+    CA_AVAILABLE_STARTING (10.6, 5.0, 9.0, 2.0);
 
 /** `renderMode' values. **/
 
 CA_EXTERN NSString * const kCAEmitterLayerUnordered
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_5_0);
+    CA_AVAILABLE_STARTING (10.6, 5.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAEmitterLayerOldestFirst
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_5_0);
+    CA_AVAILABLE_STARTING (10.6, 5.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAEmitterLayerOldestLast
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_5_0);
+    CA_AVAILABLE_STARTING (10.6, 5.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAEmitterLayerBackToFront
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_5_0);
+    CA_AVAILABLE_STARTING (10.6, 5.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAEmitterLayerAdditive
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_5_0);
+    CA_AVAILABLE_STARTING (10.6, 5.0, 9.0, 2.0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAGradientLayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAGradientLayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAGradientLayer.h	2015-08-27 05:25:25.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAGradientLayer.h	2016-06-03 05:03:17.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CAGradientLayer.h
 
-   Copyright (c) 2008-2015, Apple Inc.
+   Copyright (c) 2008-2016, Apple Inc.
    All rights reserved. */
 
 /* The gradient layer draws a color gradient over its background color,
@@ -11,6 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+CA_CLASS_AVAILABLE (10.6, 3.0, 9.0, 2.0)
 @interface CAGradientLayer : CALayer
 
 /* The array of CGColorRef objects defining the color of each gradient
@@ -48,6 +49,6 @@
 /** `type' values. **/
 
 CA_EXTERN NSString * const kCAGradientLayerAxial
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CALayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CALayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CALayer.h	2015-08-27 05:25:25.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CALayer.h	2016-06-03 05:03:15.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CALayer.h
 
-   Copyright (c) 2006-2015, Apple Inc.
+   Copyright (c) 2006-2016, Apple Inc.
    All rights reserved. */
 
 #import <QuartzCore/CAMediaTiming.h>
@@ -11,7 +11,8 @@
 #import <Foundation/NSDictionary.h>
 
 @class NSEnumerator, CAAnimation, CALayerArray;
-@protocol CAAction;
+@protocol CAAction, CALayerDelegate;
+@protocol CALayoutManager;
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -40,6 +41,7 @@
 
 /** The base layer class. **/
 
+CA_CLASS_AVAILABLE (10.5, 2.0, 9.0, 2.0)
 @interface CALayer : NSObject <NSCoding, CAMediaTiming>
 {
 @private
@@ -84,7 +86,7 @@
  * on the result of the -presentationLayer will query the presentation
  * values of the layer tree. */
 
-- (nullable id)presentationLayer;
+- (nullable instancetype)presentationLayer;
 
 /* When called on the result of the -presentationLayer method, returns
  * the underlying layer with the current model values. When called on a
@@ -92,7 +94,7 @@
  * this method after the transaction that produced the presentation
  * layer has completed is undefined. */
 
-- (id)modelLayer;
+- (instancetype)modelLayer;
 
 /** Property methods. **/
 
@@ -341,7 +343,7 @@
  * as large as the layer bounds). Defaults to one. Animatable. */
 
 @property CGFloat contentsScale
-  __OSX_AVAILABLE_STARTING (__MAC_10_7, __IPHONE_4_0);
+  CA_AVAILABLE_STARTING (10.7, 4.0, 9.0, 2.0);
 
 /* A rectangle in normalized image coordinates defining the scaled
  * center part of the `contents' image.
@@ -364,6 +366,13 @@
 
 @property CGRect contentsCenter;
 
+/* A hint for the desired storage format of the layer contents provided by
+ * -drawLayerInContext. Defaults to kCAContentsFormatRGBA8Uint. Note that this
+ * does not affect the interpretation of the `contents' property directly. */
+
+@property(copy) NSString *contentsFormat
+  CA_AVAILABLE_STARTING (10.12, 10.0, 10.0, 3.0);
+
 /* The filter types to use when rendering the `contents' property of
  * the layer. The minification filter is used when to reduce the size
  * of image data, the magnification filter to increase the size of
@@ -419,7 +428,7 @@
  * default value is NO. */
 
 @property BOOL drawsAsynchronously
-  __OSX_AVAILABLE_STARTING (__MAC_10_8, __IPHONE_6_0);
+  CA_AVAILABLE_STARTING (10.8, 6.0, 9.0, 2.0);
 
 /* Called via the -display method when the `contents' property is being
  * updated. Default implementation does nothing. The context may be
@@ -567,7 +576,7 @@
  * When nil (the default value) only the autoresizing style of layout
  * is done (unless a subclass overrides -layoutSublayers). */
 
-@property(nullable, strong) id layoutManager;
+@property(nullable, strong) id /*<CALayoutManager>*/ layoutManager;
 
 /* Returns the preferred frame size of the layer in the coordinate
  * space of the superlayer. The default implementation calls the layout
@@ -724,7 +733,7 @@
  * below (for those that it implements). The value of this property is
  * not retained. Default value is nil. */
 
-@property(nullable, weak) id delegate;
+@property(nullable, weak) id /*<CALayerDelegate>*/ delegate;
 
 /* When non-nil, a dictionary dereferenced to find property values that
  * aren't explicitly defined by the layer. (This dictionary may in turn
@@ -742,6 +751,9 @@
 
 /** Layout manager protocol. **/
 
+@protocol CALayoutManager <NSObject>
+@end
+
 @interface NSObject (CALayoutManager)
 
 /* Called when the preferred size of 'layer' may have changed. The
@@ -785,6 +797,9 @@
 
 /** Delegate methods. **/
 
+@protocol CALayerDelegate <NSObject>
+@end
+
 @interface NSObject (CALayerDelegate)
 
 /* If defined, called by the default implementation of the -display
@@ -797,6 +812,14 @@
 
 - (void)drawLayer:(CALayer *)layer inContext:(CGContextRef)ctx;
 
+/* If defined, called by the default implementation of the -display method.
+ * Allows the delegate to configure any layer state affecting contents prior
+ * to -drawLayer:InContext: such as `contentsFormat' and `opaque'. It will not
+ * be called if the delegate implements -displayLayer. */
+
+- (void)layerWillDraw:(CALayer *)layer
+  CA_AVAILABLE_STARTING (10.12, 10.0, 10.0, 3.0);
+
 /* Called by the default -layoutSublayers implementation before the layout
  * manager is checked. Note that if the delegate method is invoked, the
  * layout manager will be ignored. */
@@ -817,54 +840,63 @@
 /** Layer `contentsGravity' values. **/
 
 CA_EXTERN NSString * const kCAGravityCenter
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAGravityTop
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAGravityBottom
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAGravityLeft
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAGravityRight
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAGravityTopLeft
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAGravityTopRight
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAGravityBottomLeft
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAGravityBottomRight
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAGravityResize
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAGravityResizeAspect
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAGravityResizeAspectFill
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
+
+/** Layer `contentsFormat` values. **/
+
+CA_EXTERN NSString * const kCAContentsFormatRGBA8Uint /* RGBA UInt8 per component */
+  CA_AVAILABLE_STARTING (10.12, 10.0, 10.0, 3.0);
+CA_EXTERN NSString * const kCAContentsFormatRGBA16Float /* RGBA half-float 16-bit per component */
+  CA_AVAILABLE_STARTING (10.12, 10.0, 10.0, 3.0);
+CA_EXTERN NSString * const kCAContentsFormatGray8Uint /* Grayscale with alpha (if not opaque) UInt8 per component */
+  CA_AVAILABLE_STARTING (10.12, 10.0, 10.0, 3.0);
 
 /** Contents filter names. **/
 
 CA_EXTERN NSString * const kCAFilterNearest
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAFilterLinear
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 /* Trilinear minification filter. Enables mipmap generation. Some
  * renderers may ignore this, or impose additional restrictions, such
  * as source images requiring power-of-two dimensions. */
 
 CA_EXTERN NSString * const kCAFilterTrilinear
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 
 /** Layer event names. **/
 
 CA_EXTERN NSString * const kCAOnOrderIn
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAOnOrderOut
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 /** The animation key used for transitions. **/
 
 CA_EXTERN NSString * const kCATransition
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAMediaTiming.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAMediaTiming.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAMediaTiming.h	2015-08-27 05:25:25.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAMediaTiming.h	2016-06-03 05:03:17.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CAMediaTiming.h
 
-   Copyright (c) 2006-2015, Apple Inc.
+   Copyright (c) 2006-2016, Apple Inc.
    All rights reserved. */
 
 #import <QuartzCore/CABase.h>
@@ -79,12 +79,12 @@
 /* `fillMode' options. */
 
 CA_EXTERN NSString * const kCAFillModeForwards
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAFillModeBackwards
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAFillModeBoth
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAFillModeRemoved
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAMediaTimingFunction.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAMediaTimingFunction.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAMediaTimingFunction.h	2015-08-27 05:25:25.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAMediaTimingFunction.h	2016-06-03 05:03:16.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CAMediaTimingFunction.h
 
-   Copyright (c) 2006-2015, Apple Inc.
+   Copyright (c) 2006-2016, Apple Inc.
    All rights reserved. */
 
 #import <QuartzCore/CAMediaTiming.h>
@@ -16,6 +16,7 @@
  * to define the pacing of an animation over its duration (or over the
  * duration of one keyframe). */
 
+CA_CLASS_AVAILABLE (10.5, 2.0, 9.0, 2.0)
 @interface CAMediaTimingFunction : NSObject <NSCoding>
 {
 @private
@@ -47,14 +48,14 @@
 /** Timing function names. **/
 
 CA_EXTERN NSString * const kCAMediaTimingFunctionLinear
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAMediaTimingFunctionEaseIn
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAMediaTimingFunctionEaseOut
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAMediaTimingFunctionEaseInEaseOut
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAMediaTimingFunctionDefault
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAMetalLayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAMetalLayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAMetalLayer.h	2015-08-27 05:25:25.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAMetalLayer.h	2016-06-03 05:03:15.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CAMetalLayer.h
 
-   Copyright (c) 2013-2015, Apple Inc.
+   Copyright (c) 2013-2016, Apple Inc.
    All rights reserved. */
 
 #import <QuartzCore/CALayer.h>
@@ -40,7 +40,7 @@
 /* Note: The default value of the `opaque' property for CAMetalLayer
  * instances is true. */
 
-NS_CLASS_AVAILABLE(10_11, 8_0)
+CA_CLASS_AVAILABLE (10.11, 8.0, 9.0, 2.0)
 @interface CAMetalLayer : CALayer
 {
 @private
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAOpenGLLayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAOpenGLLayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAOpenGLLayer.h	2015-08-27 05:25:25.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAOpenGLLayer.h	2016-06-03 05:03:15.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CAOpenGLLayer.h
 
-   Copyright (c) 2006-2015, Apple Inc.
+   Copyright (c) 2006-2016, Apple Inc.
    All rights reserved. */
 
 #import <QuartzCore/CALayer.h>
@@ -9,6 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+CA_CLASS_AVAILABLE (10.5)
 @interface CAOpenGLLayer : CALayer
 {
 @private
@@ -29,7 +30,7 @@
 
 - (BOOL)canDrawInCGLContext:(CGLContextObj)ctx
     pixelFormat:(CGLPixelFormatObj)pf forLayerTime:(CFTimeInterval)t
-    displayTime:(const CVTimeStamp *)ts;
+    displayTime:(nullable const CVTimeStamp *)ts;
 
 /* Called when a new frame needs to be generated for layer time 't'.
  * 'ctx' is attached to the rendering destination. It's state is
@@ -39,7 +40,7 @@
  * after rendering. */
 
 - (void)drawInCGLContext:(CGLContextObj)ctx pixelFormat:(CGLPixelFormatObj)pf
-    forLayerTime:(CFTimeInterval)t displayTime:(const CVTimeStamp *)ts;
+    forLayerTime:(CFTimeInterval)t displayTime:(nullable const CVTimeStamp *)ts;
 
 /* This method will be called by the CAOpenGLLayer implementation when
  * a pixel format object is needed for the layer. Should return an
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CARemoteLayerClient.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CARemoteLayerClient.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CARemoteLayerClient.h	2015-08-27 05:25:25.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CARemoteLayerClient.h	2016-06-03 05:03:16.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CARemoteLayerClient.h
 
-   Copyright (c) 2010-2015, Apple Inc.
+   Copyright (c) 2010-2016, Apple Inc.
    All rights reserved. */
 
 #import <QuartzCore/CABase.h>
@@ -11,6 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+CA_CLASS_AVAILABLE (10.7)
 @interface CARemoteLayerClient : NSObject
 {
 @private
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CARemoteLayerServer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CARemoteLayerServer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CARemoteLayerServer.h	2015-08-27 05:25:25.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CARemoteLayerServer.h	2016-06-03 05:03:17.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CARemoteLayerServer.h
 
-   Copyright (c) 2010-2015, Apple Inc.
+   Copyright (c) 2010-2016, Apple Inc.
    All rights reserved. */
 
 #import <QuartzCore/CALayer.h>
@@ -9,6 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+CA_CLASS_AVAILABLE (10.7)
 @interface CARemoteLayerServer : NSObject
 {
 @private
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CARenderer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CARenderer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CARenderer.h	2015-08-27 05:25:25.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CARenderer.h	2016-06-03 05:03:16.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CARenderer.h
 
-   Copyright (c) 2007-2015, Apple Inc.
+   Copyright (c) 2007-2016, Apple Inc.
    All rights reserved. */
 
 /* This class lets an application manually drive the rendering of a
@@ -37,6 +37,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+CA_CLASS_AVAILABLE (10.5)
 @interface CARenderer : NSObject
 {
 @private
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAReplicatorLayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAReplicatorLayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAReplicatorLayer.h	2015-08-27 05:25:25.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAReplicatorLayer.h	2016-06-03 05:03:16.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CAReplicatorLayer.h
 
-   Copyright (c) 2008-2015, Apple Inc.
+   Copyright (c) 2008-2016, Apple Inc.
    All rights reserved. */
 
 #import <QuartzCore/CALayer.h>
@@ -15,6 +15,7 @@
  * instance of z replicator layer's sublayers. This may change in the
  * future. */
 
+CA_CLASS_AVAILABLE (10.6, 3.0, 9.0, 2.0)
 @interface CAReplicatorLayer : CALayer
 
 /* The number of copies to create, including the source object.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAScrollLayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAScrollLayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAScrollLayer.h	2015-08-27 05:25:25.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAScrollLayer.h	2016-06-03 05:03:16.000000000 +0200
@@ -1,12 +1,13 @@
 /* CoreAnimation - CAScrollLayer.h
 
-   Copyright (c) 2006-2015, Apple Inc.
+   Copyright (c) 2006-2016, Apple Inc.
    All rights reserved. */
 
 #import <QuartzCore/CALayer.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
+CA_CLASS_AVAILABLE (10.5, 2.0, 9.0, 2.0)
 @interface CAScrollLayer : CALayer
 
 /* Changes the origin of the layer to point 'p'. */
@@ -46,12 +47,12 @@
 /* `scrollMode' values. */
 
 CA_EXTERN NSString * const kCAScrollNone
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAScrollVertically
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAScrollHorizontally
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAScrollBoth
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAShapeLayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAShapeLayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAShapeLayer.h	2015-08-27 05:25:25.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAShapeLayer.h	2016-06-06 06:02:04.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CAShapeLayer.h
 
-   Copyright (c) 2008-2015, Apple Inc.
+   Copyright (c) 2008-2016, Apple Inc.
    All rights reserved. */
 
 #import <QuartzCore/CALayer.h>
@@ -30,6 +30,7 @@
  * Note: rasterization may favor speed over accuracy, e.g. pixels with
  * multiple intersecting path segments may not give exact results. */
 
+CA_CLASS_AVAILABLE (10.6, 3.0, 9.0, 2.0)
 @interface CAShapeLayer : CALayer
 
 /* The path defining the shape to be rendered. If the path extends
@@ -101,26 +102,26 @@
 /* `fillRule' values. */
 
 CA_EXTERN NSString *const kCAFillRuleNonZero
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 CA_EXTERN NSString *const kCAFillRuleEvenOdd
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 
 /* `lineJoin' values. */
 
 CA_EXTERN NSString *const kCALineJoinMiter
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 CA_EXTERN NSString *const kCALineJoinRound
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 CA_EXTERN NSString *const kCALineJoinBevel
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 
 /* `lineCap' values. */
 
 CA_EXTERN NSString *const kCALineCapButt
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 CA_EXTERN NSString *const kCALineCapRound
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 CA_EXTERN NSString *const kCALineCapSquare
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CATextLayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CATextLayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CATextLayer.h	2015-08-27 05:25:25.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CATextLayer.h	2016-06-03 05:03:16.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CATextLayer.h
 
-   Copyright (c) 2006-2015, Apple Inc.
+   Copyright (c) 2006-2016, Apple Inc.
    All rights reserved. */
 
 #import <QuartzCore/CALayer.h>
@@ -11,6 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+CA_CLASS_AVAILABLE (10.5, 2.0, 9.0, 2.0)
 @interface CATextLayer : CALayer
 {
 @private
@@ -67,25 +68,25 @@
 /* Truncation modes. */
 
 CA_EXTERN NSString * const kCATruncationNone
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_3_2);
+    CA_AVAILABLE_STARTING (10.5, 3.2, 9.0, 2.0);
 CA_EXTERN NSString * const kCATruncationStart
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_3_2);
+    CA_AVAILABLE_STARTING (10.5, 3.2, 9.0, 2.0);
 CA_EXTERN NSString * const kCATruncationEnd
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_3_2);
+    CA_AVAILABLE_STARTING (10.5, 3.2, 9.0, 2.0);
 CA_EXTERN NSString * const kCATruncationMiddle
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_3_2);
+    CA_AVAILABLE_STARTING (10.5, 3.2, 9.0, 2.0);
 
 /* Alignment modes. */
 
 CA_EXTERN NSString * const kCAAlignmentNatural
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_3_2);
+    CA_AVAILABLE_STARTING (10.5, 3.2, 9.0, 2.0);
 CA_EXTERN NSString * const kCAAlignmentLeft
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_3_2);
+    CA_AVAILABLE_STARTING (10.5, 3.2, 9.0, 2.0);
 CA_EXTERN NSString * const kCAAlignmentRight
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_3_2);
+    CA_AVAILABLE_STARTING (10.5, 3.2, 9.0, 2.0);
 CA_EXTERN NSString * const kCAAlignmentCenter
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_3_2);
+    CA_AVAILABLE_STARTING (10.5, 3.2, 9.0, 2.0);
 CA_EXTERN NSString * const kCAAlignmentJustified
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_3_2);
+    CA_AVAILABLE_STARTING (10.5, 3.2, 9.0, 2.0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CATiledLayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CATiledLayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CATiledLayer.h	2015-08-27 05:25:25.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CATiledLayer.h	2016-06-03 05:03:15.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CATiledLayer.h
 
-   Copyright (c) 2006-2015, Apple Inc.
+   Copyright (c) 2006-2016, Apple Inc.
    All rights reserved. */
 
 /* This is a subclass of CALayer providing a way to asynchronously
@@ -26,6 +26,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+CA_CLASS_AVAILABLE (10.5, 2.0, 9.0, 2.0)
 @interface CATiledLayer : CALayer
 
 /* The time in seconds that newly added images take to "fade-in" to the
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CATransaction.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CATransaction.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CATransaction.h	2015-08-27 05:25:25.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CATransaction.h	2016-06-03 05:03:17.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CATransaction.h
 
-   Copyright (c) 2006-2015, Apple Inc.
+   Copyright (c) 2006-2016, Apple Inc.
    All rights reserved. */
 
 #import <QuartzCore/CABase.h>
@@ -28,6 +28,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+CA_CLASS_AVAILABLE (10.5, 2.0, 9.0, 2.0)
 @interface CATransaction : NSObject
 
 /* Begin a new transaction for the current thread; nests. */
@@ -111,12 +112,12 @@
 /** Transaction property ids. **/
 
 CA_EXTERN NSString * const kCATransactionAnimationDuration
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCATransactionDisableActions
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCATransactionAnimationTimingFunction
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCATransactionCompletionBlock
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_4_0);
+    CA_AVAILABLE_STARTING (10.6, 4.0, 9.0, 2.0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CATransform3D.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CATransform3D.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CATransform3D.h	2015-08-27 05:25:24.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CATransform3D.h	2016-06-03 05:03:16.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CATransform3D.h
 
-   Copyright (c) 2006-2015, Apple Inc.
+   Copyright (c) 2006-2016, Apple Inc.
    All rights reserved. */
 
 #ifndef CATRANSFORM_H
@@ -29,32 +29,32 @@
 /* The identity transform: [1 0 0 0; 0 1 0 0; 0 0 1 0; 0 0 0 1]. */
 
 CA_EXTERN const CATransform3D CATransform3DIdentity
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 /* Returns true if 't' is the identity transform. */
 
 CA_EXTERN bool CATransform3DIsIdentity (CATransform3D t)
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 /* Returns true if 'a' is exactly equal to 'b'. */
 
 CA_EXTERN bool CATransform3DEqualToTransform (CATransform3D a,
     CATransform3D b)
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 /* Returns a transform that translates by '(tx, ty, tz)':
  * t' =  [1 0 0 0; 0 1 0 0; 0 0 1 0; tx ty tz 1]. */
 
 CA_EXTERN CATransform3D CATransform3DMakeTranslation (CGFloat tx,
     CGFloat ty, CGFloat tz)
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 /* Returns a transform that scales by `(sx, sy, sz)':
  * t' = [sx 0 0 0; 0 sy 0 0; 0 0 sz 0; 0 0 0 1]. */
 
 CA_EXTERN CATransform3D CATransform3DMakeScale (CGFloat sx, CGFloat sy,
     CGFloat sz)
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 /* Returns a transform that rotates by 'angle' radians about the vector
  * '(x, y, z)'. If the vector has length zero the identity transform is
@@ -62,21 +62,21 @@
 
 CA_EXTERN CATransform3D CATransform3DMakeRotation (CGFloat angle, CGFloat x,
     CGFloat y, CGFloat z)
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 /* Translate 't' by '(tx, ty, tz)' and return the result:
  * t' = translate(tx, ty, tz) * t. */
 
 CA_EXTERN CATransform3D CATransform3DTranslate (CATransform3D t, CGFloat tx,
     CGFloat ty, CGFloat tz)
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 /* Scale 't' by '(sx, sy, sz)' and return the result:
  * t' = scale(sx, sy, sz) * t. */
 
 CA_EXTERN CATransform3D CATransform3DScale (CATransform3D t, CGFloat sx,
     CGFloat sy, CGFloat sz)
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 /* Rotate 't' by 'angle' radians about the vector '(x, y, z)' and return
  * the result. If the vector has zero length the behavior is undefined:
@@ -84,35 +84,35 @@
 
 CA_EXTERN CATransform3D CATransform3DRotate (CATransform3D t, CGFloat angle,
     CGFloat x, CGFloat y, CGFloat z)
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 /* Concatenate 'b' to 'a' and return the result: t' = a * b. */
 
 CA_EXTERN CATransform3D CATransform3DConcat (CATransform3D a, CATransform3D b)
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 /* Invert 't' and return the result. Returns the original matrix if 't'
  * has no inverse. */
 
 CA_EXTERN CATransform3D CATransform3DInvert (CATransform3D t)
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 /* Return a transform with the same effect as affine transform 'm'. */
 
 CA_EXTERN CATransform3D CATransform3DMakeAffineTransform (CGAffineTransform m)
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 /* Returns true if 't' can be represented exactly by an affine transform. */
 
 CA_EXTERN bool CATransform3DIsAffine (CATransform3D t)
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 /* Returns the affine transform represented by 't'. If 't' can not be
  * represented exactly by an affine transform the returned value is
  * undefined. */
 
 CA_EXTERN CGAffineTransform CATransform3DGetAffineTransform (CATransform3D t)
-    __OSX_AVAILABLE_STARTING (__MAC_10_5, __IPHONE_2_0);
+    CA_AVAILABLE_STARTING (10.5, 2.0, 9.0, 2.0);
 
 CA_EXTERN_C_END
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CATransformLayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CATransformLayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CATransformLayer.h	2015-08-27 05:25:25.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CATransformLayer.h	2016-06-03 05:03:16.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CATransformLayer.h
 
-   Copyright (c) 2006-2015, Apple Inc.
+   Copyright (c) 2006-2016, Apple Inc.
    All rights reserved. */
 
 #import <QuartzCore/CALayer.h>
@@ -29,6 +29,7 @@
  * their sublayers, applying the effects of the transform layer's
  * geometry when hit-testing each sublayer. */
 
+CA_CLASS_AVAILABLE (10.6, 3.0, 9.0, 2.0)
 @interface CATransformLayer : CALayer
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAValueFunction.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAValueFunction.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAValueFunction.h	2015-08-27 05:25:25.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CAValueFunction.h	2016-06-03 05:03:16.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CAValueFunction.h
 
-   Copyright (c) 2008-2015, Apple Inc.
+   Copyright (c) 2008-2016, Apple Inc.
    All rights reserved. */
 
 #import <QuartzCore/CABase.h>
@@ -8,6 +8,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+CA_CLASS_AVAILABLE (10.6, 3.0, 9.0, 2.0)
 @interface CAValueFunction : NSObject <NSCoding>
 {
 @protected
@@ -28,44 +29,44 @@
  * corresponding rotation matrix. */
 
 CA_EXTERN NSString * const kCAValueFunctionRotateX
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAValueFunctionRotateY
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAValueFunctionRotateZ
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 
 /* The `scale' function takes three input values and constructs a
  * 4x4 matrix representing the corresponding scale matrix. */
 
 CA_EXTERN NSString * const kCAValueFunctionScale
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 
 /* The `scaleX', `scaleY', `scaleZ' functions take a single input value
  * and construct a 4x4 matrix representing the corresponding scaling
  * matrix. */
 
 CA_EXTERN NSString * const kCAValueFunctionScaleX
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAValueFunctionScaleY
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAValueFunctionScaleZ
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 
 /* The `translate' function takes three input values and constructs a
  * 4x4 matrix representing the corresponding scale matrix. */
 
 CA_EXTERN NSString * const kCAValueFunctionTranslate
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 
 /* The `translateX', `translateY', `translateZ' functions take a single
  * input value and construct a 4x4 matrix representing the corresponding
  * translation matrix. */
 
 CA_EXTERN NSString * const kCAValueFunctionTranslateX
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAValueFunctionTranslateY
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 CA_EXTERN NSString * const kCAValueFunctionTranslateZ
-    __OSX_AVAILABLE_STARTING (__MAC_10_6, __IPHONE_3_0);
+    CA_AVAILABLE_STARTING (10.6, 3.0, 9.0, 2.0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CoreAnimation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CoreAnimation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CoreAnimation.h	2015-08-27 05:25:24.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/CoreAnimation.h	2016-06-03 05:03:16.000000000 +0200
@@ -1,6 +1,6 @@
 /* CoreAnimation - CoreAnimation.h
 
-   Copyright (c) 2006-2015, Apple Inc.
+   Copyright (c) 2006-2016, Apple Inc.
    All rights reserved. */
 
 #ifndef COREANIMATION_H
@@ -31,6 +31,7 @@
 #import <QuartzCore/CATextLayer.h>
 #import <QuartzCore/CATiledLayer.h>
 #import <QuartzCore/CATransaction.h>
+#import <QuartzCore/CATransform3D.h>
 #import <QuartzCore/CATransformLayer.h>
 #import <QuartzCore/CAValueFunction.h>
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/QuartzCore.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/QuartzCore.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/QuartzCore.h	2015-08-27 05:25:23.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/QuartzCore.framework/Headers/QuartzCore.h	2016-06-03 05:03:16.000000000 +0200
@@ -1,6 +1,6 @@
 /* QuartzCore.h
 
-   Copyright (c) 2004-2015, Apple Inc.
+   Copyright (c) 2004-2016, Apple Inc.
    All rights reserved. */
 
 #ifndef QUARTZCORE_H

```