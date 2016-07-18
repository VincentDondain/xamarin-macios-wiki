#UIKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h	2016-06-27 06:29:57.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h	2016-07-13 05:30:12.000000000 +0200
@@ -427,10 +427,10 @@
     UIAccessibilityHearingDeviceEarLeft    = 1 << 1,
     UIAccessibilityHearingDeviceEarRight   = 1 << 2,
     UIAccessibilityHearingDeviceEarBoth    = UIAccessibilityHearingDeviceEarLeft | UIAccessibilityHearingDeviceEarRight,
-} NS_ENUM_AVAILABLE_IOS(10_0);
+} NS_ENUM_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED;
 
 // Returns the current pairing status of MFi hearing aids
-UIKIT_EXTERN UIAccessibilityHearingDeviceEar UIAccessibilityHearingDevicePairedEar(void) NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UIAccessibilityHearingDevicePairedEarDidChangeNotification NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UIAccessibilityHearingDeviceEar UIAccessibilityHearingDevicePairedEar(void) NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN NSString *const UIAccessibilityHearingDevicePairedEarDidChangeNotification NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED;
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIApplication.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIApplication.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIApplication.h	2016-06-27 06:32:24.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIApplication.h	2016-07-13 05:29:34.000000000 +0200
@@ -12,6 +12,7 @@
 #import <UIKit/UIInterface.h>
 #import <UIKit/UIDevice.h>
 #import <UIKit/UIAlert.h>
+#import <UIKit/UIContentSizeCategory.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -188,7 +189,7 @@
 @property(nonatomic,readonly) UIUserInterfaceLayoutDirection userInterfaceLayoutDirection NS_AVAILABLE_IOS(5_0);
 
 // Return the size category
-@property(nonatomic,readonly) NSString *preferredContentSizeCategory NS_AVAILABLE_IOS(7_0);
+@property(nonatomic,readonly) UIContentSizeCategory preferredContentSizeCategory NS_AVAILABLE_IOS(7_0);
 
 @end
 
@@ -394,7 +395,7 @@
 - (void)application:(UIApplication *)application didUpdateUserActivity:(NSUserActivity *)userActivity NS_AVAILABLE_IOS(8_0);
 
 #pragma mark -- CloudKit Sharing Invitation Handling --
-- (void) application:(UIApplication *)application userAcceptedCloudKitShareWithMetadata:(CKShareMetadata *)cloudKitShareMetadata NS_AVAILABLE_IOS(10_0);
+- (void) application:(UIApplication *)application userDidAcceptCloudKitShareWithMetadata:(CKShareMetadata *)cloudKitShareMetadata NS_AVAILABLE_IOS(10_0);
 
 @end
 
@@ -467,27 +468,6 @@
 UIKIT_EXTERN NSString *const UIApplicationOpenURLOptionsAnnotationKey NS_AVAILABLE_IOS(9_0);   // value is a property-list typed object corresponding to what the originating application passed in UIDocumentInteractionController's annotation property
 UIKIT_EXTERN NSString *const UIApplicationOpenURLOptionsOpenInPlaceKey NS_AVAILABLE_IOS(9_0);   // value is a bool NSNumber, set to YES if the file needs to be copied before use
 
-// Content size category constants
-UIKIT_EXTERN NSString *const UIContentSizeCategoryUnspecified NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UIContentSizeCategoryExtraSmall NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UIContentSizeCategorySmall NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UIContentSizeCategoryMedium NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UIContentSizeCategoryLarge NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UIContentSizeCategoryExtraLarge NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UIContentSizeCategoryExtraExtraLarge NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UIContentSizeCategoryExtraExtraExtraLarge NS_AVAILABLE_IOS(7_0);
-
-// Accessibility sizes
-UIKIT_EXTERN NSString *const UIContentSizeCategoryAccessibilityMedium NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UIContentSizeCategoryAccessibilityLarge NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UIContentSizeCategoryAccessibilityExtraLarge NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UIContentSizeCategoryAccessibilityExtraExtraLarge NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UIContentSizeCategoryAccessibilityExtraExtraExtraLarge NS_AVAILABLE_IOS(7_0);
-
-// Notification is emitted when the user has changed the preferredContentSizeCategory for the system
-UIKIT_EXTERN NSString *const UIContentSizeCategoryDidChangeNotification NS_AVAILABLE_IOS(7_0); // userInfo dictionary will contain new value for UIContentSizeCategoryNewValueKey
-UIKIT_EXTERN NSString *const UIContentSizeCategoryNewValueKey NS_AVAILABLE_IOS(7_0); // NSString instance with new content size category in userInfo
-
 // This notification is posted after the user takes a screenshot (for example by pressing both the home and lock screen buttons)
 UIKIT_EXTERN NSString *const UIApplicationUserDidTakeScreenshotNotification NS_AVAILABLE_IOS(7_0);
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIButton.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIButton.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIButton.h	2016-06-27 06:29:57.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIButton.h	2016-07-13 05:30:12.000000000 +0200
@@ -31,7 +31,7 @@
 
 + (instancetype)buttonWithType:(UIButtonType)buttonType;
 
-@property(nonatomic)          UIEdgeInsets contentEdgeInsets UI_APPEARANCE_SELECTOR; // default is UIEdgeInsetsZero. On tvOS, detault is nonzero except for custom buttons on tvOS 10 or later.
+@property(nonatomic)          UIEdgeInsets contentEdgeInsets UI_APPEARANCE_SELECTOR; // default is UIEdgeInsetsZero. On tvOS 10 or later, default is nonzero except for custom buttons.
 @property(nonatomic)          UIEdgeInsets titleEdgeInsets;                // default is UIEdgeInsetsZero
 @property(nonatomic)          BOOL         reversesTitleShadowWhenHighlighted; // default is NO. if YES, shadow reverses to shift between engrave and emboss appearance
 @property(nonatomic)          UIEdgeInsets imageEdgeInsets;                // default is UIEdgeInsetsZero
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICloudSharingController.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICloudSharingController.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICloudSharingController.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICloudSharingController.h	2016-07-13 05:30:12.000000000 +0200
@@ -5,7 +5,10 @@
 //  Copyright © 2016 Apple Inc. All rights reserved.
 //
 
-#import <UIKit/UIKit.h>
+#import <Foundation/Foundation.h>
+#import <UIKit/UIKitDefines.h>
+#import <UIKit/UIViewController.h>
+#import <UIKit/UIActivityItemProvider.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIContentSizeCategory.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIContentSizeCategory.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIContentSizeCategory.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIContentSizeCategory.h	2016-07-13 05:30:12.000000000 +0200
@@ -0,0 +1,37 @@
+//
+//  UIContentSizeCategory.h
+//  UIKit
+//
+//  Copyright (c) 2016-2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <UIKit/UIKitDefines.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+typedef NSString * UIContentSizeCategory NS_STRING_ENUM NS_AVAILABLE_IOS(10_0);
+
+// Content size category constants
+
+UIKIT_EXTERN UIContentSizeCategory const UIContentSizeCategoryUnspecified NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UIContentSizeCategory const UIContentSizeCategoryExtraSmall NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIContentSizeCategory const UIContentSizeCategorySmall NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIContentSizeCategory const UIContentSizeCategoryMedium NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIContentSizeCategory const UIContentSizeCategoryLarge NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIContentSizeCategory const UIContentSizeCategoryExtraLarge NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIContentSizeCategory const UIContentSizeCategoryExtraExtraLarge NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIContentSizeCategory const UIContentSizeCategoryExtraExtraExtraLarge NS_AVAILABLE_IOS(7_0);
+
+// Accessibility sizes
+UIKIT_EXTERN UIContentSizeCategory const UIContentSizeCategoryAccessibilityMedium NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIContentSizeCategory const UIContentSizeCategoryAccessibilityLarge NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIContentSizeCategory const UIContentSizeCategoryAccessibilityExtraLarge NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIContentSizeCategory const UIContentSizeCategoryAccessibilityExtraExtraLarge NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIContentSizeCategory const UIContentSizeCategoryAccessibilityExtraExtraExtraLarge NS_AVAILABLE_IOS(7_0);
+
+// Notification is emitted when the user has changed the preferredContentSizeCategory for the system
+UIKIT_EXTERN NSNotificationName const UIContentSizeCategoryDidChangeNotification NS_AVAILABLE_IOS(7_0); // userInfo dictionary will contain new value for UIContentSizeCategoryNewValueKey
+UIKIT_EXTERN NSString *const UIContentSizeCategoryNewValueKey NS_AVAILABLE_IOS(7_0); // NSString instance with new content size category in userInfo
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h	2016-06-27 07:06:58.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h	2016-07-11 07:25:47.000000000 +0200
@@ -46,6 +46,7 @@
 
 #if __has_include(<UIKit/UIContentSizeCategoryAdjusting.h>)
 #import <UIKit/UIContentSizeCategoryAdjusting.h>
+#import <UIKit/UIContentSizeCategory.h>
 #import <UIKit/UIControl.h>
 #import <UIKit/UIDataDetectors.h>
 #import <UIKit/UIDatePicker.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINibLoading.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINibLoading.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINibLoading.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINibLoading.h	2016-07-13 05:30:12.000000000 +0200
@@ -13,7 +13,7 @@
 UIKIT_EXTERN NSString * const UINibExternalObjects NS_AVAILABLE_IOS(3_0);
 
 @interface NSBundle(UINibLoadingAdditions)
-- (NSArray *)loadNibNamed:(NSString *)name owner:(nullable id)owner options:(nullable NSDictionary *)options;
+- (nullable NSArray *)loadNibNamed:(NSString *)name owner:(nullable id)owner options:(nullable NSDictionary *)options;
 @end
 
 @interface NSObject(UINibLoadingAdditions)
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableView.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableView.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableView.h	2016-06-27 06:32:24.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableView.h	2016-07-14 06:20:58.000000000 +0200
@@ -142,8 +142,8 @@
 - (BOOL)tableView:(UITableView *)tableView shouldIndentWhileEditingRowAtIndexPath:(NSIndexPath *)indexPath;
 
 // The willBegin/didEnd methods are called whenever the 'editing' property is automatically changed by the table (allowing insert/delete/move). This is done by a swipe activating a single row
-- (void)tableView:(UITableView*)tableView willBeginEditingRowAtIndexPath:(NSIndexPath *)indexPath __TVOS_PROHIBITED;
-- (void)tableView:(UITableView*)tableView didEndEditingRowAtIndexPath:(NSIndexPath *)indexPath __TVOS_PROHIBITED;
+- (void)tableView:(UITableView *)tableView willBeginEditingRowAtIndexPath:(NSIndexPath *)indexPath __TVOS_PROHIBITED;
+- (void)tableView:(UITableView *)tableView didEndEditingRowAtIndexPath:(nullable NSIndexPath *)indexPath __TVOS_PROHIBITED;
 
 // Moving/reordering
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITraitCollection.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITraitCollection.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITraitCollection.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITraitCollection.h	2016-07-13 05:30:12.000000000 +0200
@@ -11,6 +11,7 @@
 #import <UIKit/UIDevice.h>
 #import <UIKit/UIInterface.h>
 #import <UIKit/UITouch.h>
+#import <UIKit/UIContentSizeCategory.h>
 
 /*! A trait collection encapsulates the system traits of an interface's environment. */
 NS_ASSUME_NONNULL_BEGIN
@@ -48,8 +49,8 @@
 + (UITraitCollection *)traitCollectionWithForceTouchCapability:(UIForceTouchCapability)capability NS_AVAILABLE_IOS(9_0);
 @property (nonatomic, readonly) UIForceTouchCapability forceTouchCapability NS_AVAILABLE_IOS(9_0); // unspecified: UIForceTouchCapabilityUnknown
 
-+ (UITraitCollection *)traitCollectionWithPreferredContentSizeCategory:(NSString *)preferredContentSizeCategory NS_AVAILABLE_IOS(10_0);
-@property (nonatomic, copy, readonly) NSString *preferredContentSizeCategory NS_AVAILABLE_IOS(10_0); // unspecified: UIContentSizeCategoryUnspecified
++ (UITraitCollection *)traitCollectionWithPreferredContentSizeCategory:(UIContentSizeCategory)preferredContentSizeCategory NS_AVAILABLE_IOS(10_0);
+@property (nonatomic, copy, readonly) UIContentSizeCategory preferredContentSizeCategory NS_AVAILABLE_IOS(10_0); // unspecified: UIContentSizeCategoryUnspecified
 
 + (UITraitCollection *)traitCollectionWithDisplayGamut:(UIDisplayGamut)displayGamut NS_AVAILABLE_IOS(10_0);
 @property (nonatomic, readonly) UIDisplayGamut displayGamut NS_AVAILABLE_IOS(10_0); // unspecified: UIDisplayGamutUnspecified
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewPropertyAnimator.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewPropertyAnimator.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewPropertyAnimator.h	2016-06-27 06:29:56.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewPropertyAnimator.h	2016-07-13 05:29:34.000000000 +0200
@@ -52,7 +52,7 @@
 + (instancetype)runningPropertyAnimatorWithDuration:(NSTimeInterval)duration
                                               delay:(NSTimeInterval)delay
                                             options:(UIViewAnimationOptions)options
-                                         animations:(void (^ __nullable)(void))animations
+                                         animations:(void (^)(void))animations
                                          completion:(void (^ __nullable)(UIViewAnimatingPosition finalPosition))completion;
 
 /// Animatable view properties that are set by the animation block will be
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIVisualEffectView.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIVisualEffectView.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIVisualEffectView.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIVisualEffectView.h	2016-07-13 05:30:12.000000000 +0200
@@ -24,8 +24,9 @@
     UIBlurEffectStyleExtraLight,
     UIBlurEffectStyleLight,
     UIBlurEffectStyleDark,
-    UIBlurEffectStyleRegular NS_ENUM_AVAILABLE_IOS(10_0) = 4, // Adapts to user interface style
-    UIBlurEffectStyleProminent NS_ENUM_AVAILABLE_IOS(10_0) = 5, // Adapts to user interface style
+    UIBlurEffectStyleExtraDark __TVOS_AVAILABLE(10_0) __IOS_PROHIBITED __WATCHOS_PROHIBITED,
+    UIBlurEffectStyleRegular NS_ENUM_AVAILABLE_IOS(10_0), // Adapts to user interface style
+    UIBlurEffectStyleProminent NS_ENUM_AVAILABLE_IOS(10_0), // Adapts to user interface style
 } NS_ENUM_AVAILABLE_IOS(8_0);
 
 NS_CLASS_AVAILABLE_IOS(8_0) @interface UIVisualEffect : NSObject <NSCopying, NSSecureCoding> @end
```