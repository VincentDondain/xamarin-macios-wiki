#UIKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFeedbackGenerator.h /Applications/Xcode8-GM.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFeedbackGenerator.h
--- /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFeedbackGenerator.h	1969-12-31 18:00:00.000000000 -0600
+++ /Applications/Xcode8-GM.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFeedbackGenerator.h	2016-08-11 23:59:13.000000000 -0500
@@ -0,0 +1,21 @@
+//
+//  UIFeedbackGenerator.h
+//  UIKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+
+#import <Foundation/Foundation.h>
+#import <UIKit/UIKitDefines.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+// UIFeedbackGenerator is an abstract class that should not be used directly
+UIKIT_CLASS_AVAILABLE_IOS_ONLY(10_0) @interface UIFeedbackGenerator : NSObject
+
+/// informs self that it will likely receive events soon, so that it can ensure minimal latency for any feedback generated
+/// safe to call more than once before the generator receives an event, if events are still imminently possible
+- (void)prepare;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImpactFeedbackGenerator.h /Applications/Xcode8-GM.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImpactFeedbackGenerator.h
--- /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImpactFeedbackGenerator.h	1969-12-31 18:00:00.000000000 -0600
+++ /Applications/Xcode8-GM.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImpactFeedbackGenerator.h	2016-08-11 23:59:12.000000000 -0500
@@ -0,0 +1,28 @@
+//
+//  UIImpactFeedbackGenerator.h
+//  UIKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <UIKit/UIFeedbackGenerator.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+typedef NS_ENUM(NSInteger, UIImpactFeedbackStyle) {
+    UIImpactFeedbackStyleLight,
+    UIImpactFeedbackStyleMedium,
+    UIImpactFeedbackStyleHeavy
+};
+
+// UIImpactFeedbackGenerator is used to give user feedback when an impact between UI elements occurs
+UIKIT_CLASS_AVAILABLE_IOS_ONLY(10_0) @interface UIImpactFeedbackGenerator : UIFeedbackGenerator
+
+- (instancetype)initWithStyle:(UIImpactFeedbackStyle)style;
+
+/// call when your UI element impacts something else
+- (void)impactOccurred;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h /Applications/Xcode8-GM.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h
--- /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h	2016-08-06 03:20:59.000000000 -0500
+++ /Applications/Xcode8-GM.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h	2016-08-17 01:00:09.000000000 -0500
@@ -219,3 +219,9 @@
 #import <UIKit/UIViewPropertyAnimator.h>
 #endif
 
+#if __has_include(<UIKit/UIFeedbackGenerator.h>)
+#import <UIKit/UIFeedbackGenerator.h>
+#import <UIKit/UISelectionFeedbackGenerator.h>
+#import <UIKit/UIImpactFeedbackGenerator.h>
+#import <UIKit/UINotificationFeedbackGenerator.h>
+#endif
diff -ruN /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINotificationFeedbackGenerator.h /Applications/Xcode8-GM.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINotificationFeedbackGenerator.h
--- /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINotificationFeedbackGenerator.h	1969-12-31 18:00:00.000000000 -0600
+++ /Applications/Xcode8-GM.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINotificationFeedbackGenerator.h	2016-08-11 23:59:13.000000000 -0500
@@ -0,0 +1,26 @@
+//
+//  UINotificationFeedbackGenerator.h
+//  UIKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <UIKit/UIFeedbackGenerator.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+typedef NS_ENUM(NSInteger, UINotificationFeedbackType) {
+    UINotificationFeedbackTypeSuccess,
+    UINotificationFeedbackTypeWarning,
+    UINotificationFeedbackTypeError
+};
+
+// UINotificationFeedbackGenerator is used to give user feedback when an notification is displayed
+UIKIT_CLASS_AVAILABLE_IOS_ONLY(10_0) @interface UINotificationFeedbackGenerator : UIFeedbackGenerator
+
+/// call when a notification is displayed, passing the corresponding type
+- (void)notificationOccurred:(UINotificationFeedbackType)notificationType;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISelectionFeedbackGenerator.h /Applications/Xcode8-GM.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISelectionFeedbackGenerator.h
--- /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISelectionFeedbackGenerator.h	1969-12-31 18:00:00.000000000 -0600
+++ /Applications/Xcode8-GM.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISelectionFeedbackGenerator.h	2016-08-11 23:59:13.000000000 -0500
@@ -0,0 +1,20 @@
+//
+//  UISelectionFeedbackGenerator.h
+//  UIKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <UIKit/UIFeedbackGenerator.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+// UISelectionFeedbackGenerator is used to give user feedback when a selection changes
+UIKIT_CLASS_AVAILABLE_IOS_ONLY(10_0) @interface UISelectionFeedbackGenerator : UIFeedbackGenerator
+
+/// call when the selection changes (not on initial selection)
+- (void)selectionChanged;
+
+@end
+
+NS_ASSUME_NONNULL_END

```