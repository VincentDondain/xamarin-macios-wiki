#WatchKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKBackgroundTask.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKBackgroundTask.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKBackgroundTask.h	2016-05-25 05:22:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKBackgroundTask.h	2016-06-26 09:37:58.000000000 +0200
@@ -27,7 +27,6 @@
 
 WK_AVAILABLE_WATCHOS_ONLY(3.0)
 @interface WKSnapshotRefreshBackgroundTask : WKRefreshBackgroundTask
-@property (readonly) BOOL returnToGlanceableUI WK_DEPRECATED_WATCHOS(3.0, 3.0, "use returnToDefaultState");  // to be removed before branching for seed on 5/15
 @property (readonly) BOOL returnToDefaultState;
 
 // developer should call setTaskCompletedWithDefaultStateRestored when preparation for snapshot has been completed
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKGestureRecognizer.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKGestureRecognizer.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKGestureRecognizer.h	2016-05-25 05:22:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKGestureRecognizer.h	2016-06-26 09:37:58.000000000 +0200
@@ -39,7 +39,6 @@
 
 - (CGPoint)locationInObject;      // always refers to the interface object the gesture recognizer is attached to
 - (CGRect)objectBounds;           // locationInObject's viewBounds
-- (NSUInteger)numberOfTouches;    // always 1 in watchOS 3
 
 @end
 
@@ -48,7 +47,6 @@
 @interface WKTapGestureRecognizer : WKGestureRecognizer
 
 @property(nonatomic) NSUInteger numberOfTapsRequired;
-@property(nonatomic, readonly) NSUInteger numberOfTouchesRequired;  // always 1 in watchOS 3
 
 @end
 
@@ -57,7 +55,6 @@
 @interface WKLongPressGestureRecognizer : WKGestureRecognizer
 
 @property(nonatomic) CFTimeInterval minimumPressDuration;
-@property(nonatomic, readonly) NSUInteger numberOfTouchesRequired;  // always 1 in watchOS 3
 @property(nonatomic) NSUInteger numberOfTapsRequired;
 @property(nonatomic) CGFloat allowableMovement;
 
@@ -68,7 +65,6 @@
 @interface WKSwipeGestureRecognizer : WKGestureRecognizer
 
 @property(nonatomic) WKSwipeGestureRecognizerDirection direction;
-@property(nonatomic, readonly) NSUInteger numberOfTouchesRequired;  // always 1 in watchOS 3
 
 @end
 
@@ -76,9 +72,6 @@
 WK_AVAILABLE_WATCHOS_ONLY(3.0)
 @interface WKPanGestureRecognizer : WKGestureRecognizer
 
-@property(nonatomic, readonly) NSUInteger maximumNumberOfTouches;   // always 1 in watchOS 3
-@property(nonatomic, readonly) NSUInteger minimumNumberOfTouches;   // always 1 in watchOS 3
-
 - (CGPoint)translationInObject;   // always refers to the interface object the gesture recognizer is attached to
 - (CGPoint)velocityInObject;      // always refers to the interface object the gesture recognizer is attached to
 

```