#UIKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSFileProviderExtension.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSFileProviderExtension.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSFileProviderExtension.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSFileProviderExtension.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  NSFileProviderExtension.h
 //  UIKit
 //
-//  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSLayoutConstraint.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSLayoutConstraint.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSLayoutConstraint.h	2016-06-29 06:37:32.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSLayoutConstraint.h	2016-07-14 06:20:58.000000000 +0200
@@ -2,7 +2,7 @@
 //  NSLayoutConstraint.h
 //  UIKit
 //	
-//  Copyright (c) 2009-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2009-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/NSObject.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h	2016-06-27 06:29:57.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h	2016-07-13 05:30:12.000000000 +0200
@@ -3,7 +3,7 @@
 //  UIAccessibility.h
 //  UIKit
 //
-//  Copyright (c) 2008-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2008-2016 Apple Inc. All rights reserved.
 //
 
 #import <CoreGraphics/CoreGraphics.h>
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
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityConstants.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityConstants.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityConstants.h	2016-06-27 07:06:59.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityConstants.h	2016-07-14 06:20:58.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIAccessibilityConstants.h
 //  UIKit
 //
-//  Copyright (c) 2009-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2009-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityElement.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityElement.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityElement.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityElement.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIAccessibilityElement.h
 //  UIAccessibility
 //
-//  Copyright (c) 2008-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2008-2016 Apple Inc. All rights reserved.
 //
 
 #import <CoreGraphics/CoreGraphics.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityZoom.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityZoom.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityZoom.h	2016-06-29 06:52:46.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityZoom.h	2016-07-13 05:30:13.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIAccessibilityZoom.h
 //  UIKit
 //
-//  Copyright (c) 2011-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2011-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivity.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivity.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivity.h	2016-06-29 06:52:46.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivity.h	2016-07-14 06:20:59.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIActivity.h
 //  UIKit
 //
-//  Copyright 2012-2015 Apple Inc. All rights reserved.
+//  Copyright 2012-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityIndicatorView.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityIndicatorView.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityIndicatorView.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityIndicatorView.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIActivityIndicatorView.h
 //  UIKit
 //
-//  Copyright (c) 2005-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
 //
 
 #import <UIKit/UIView.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityItemProvider.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityItemProvider.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityItemProvider.h	2016-06-29 06:52:46.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityItemProvider.h	2016-07-13 05:30:13.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIActivityItemProvider.h
 //  UIKit
 //
-//  Copyright 2012-2015 Apple Inc. All rights reserved.
+//  Copyright 2012-2016 Apple Inc. All rights reserved.
 //
 #import <Foundation/Foundation.h>
 #import <CoreGraphics/CoreGraphics.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIApplication.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIApplication.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIApplication.h	2016-06-27 06:32:24.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIApplication.h	2016-07-13 05:29:34.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIApplication.h
 //  UIKit
 //
-//  Copyright (c) 2005-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
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
@@ -2,7 +2,7 @@
 //  UIButton.h
 //  UIKit
 //
-//  Copyright (c) 2005-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
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
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionView.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionView.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionView.h	2016-06-29 06:52:46.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionView.h	2016-07-13 05:30:13.000000000 +0200
@@ -2,7 +2,7 @@
 //  UICollectionView.h
 //  UIKit
 //
-//  Copyright (c) 2011-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2011-2016 Apple Inc. All rights reserved.
 //
 
 #import <UIKit/UIScrollView.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewFlowLayout.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewFlowLayout.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewFlowLayout.h	2016-06-29 06:52:46.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewFlowLayout.h	2016-07-13 05:30:13.000000000 +0200
@@ -2,7 +2,7 @@
 //  UICollectionViewFlowLayout.h
 //  UIKit
 //
-//  Copyright (c) 2011-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2011-2016 Apple Inc. All rights reserved.
 //
 
 #import <UIKit/UICollectionViewLayout.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewLayout.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewLayout.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewLayout.h	2016-06-29 06:52:46.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewLayout.h	2016-07-13 05:29:35.000000000 +0200
@@ -2,7 +2,7 @@
 //  UICollectionViewLayout.h
 //  UIKit
 //
-//  Copyright (c) 2011-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2011-2016 Apple Inc. All rights reserved.
 //
 
 #import <UIKit/UIKitDefines.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewTransitionLayout.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewTransitionLayout.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewTransitionLayout.h	2016-06-29 06:52:46.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewTransitionLayout.h	2016-07-13 05:30:13.000000000 +0200
@@ -2,7 +2,7 @@
 //  UICollectionView.h
 //  UIKit
 //
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
 #import <UIKit/UICollectionViewLayout.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIColor.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIColor.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIColor.h	2016-06-29 06:37:32.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIColor.h	2016-07-14 06:20:58.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIColor.h
 //  UIKit
 //
-//  Copyright (c) 2005-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
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
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIControl.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIControl.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIControl.h	2016-06-27 06:32:24.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIControl.h	2016-07-14 06:20:58.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIControl.h
 //  UIKit
 //
-//  Copyright (c) 2005-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDevice.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDevice.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDevice.h	2016-06-27 06:29:56.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDevice.h	2016-07-14 06:20:58.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIDevice.h
 //  UIKit
 //
-//  Copyright (c) 2007-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2007-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDocument.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDocument.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDocument.h	2016-06-29 06:37:33.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDocument.h	2016-07-14 06:20:59.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIDocument.h
 //  UIKit
 //
-//  Copyright (c) 1997-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 1997-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDynamicAnimator.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDynamicAnimator.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDynamicAnimator.h	2016-06-29 06:52:46.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDynamicAnimator.h	2016-07-13 05:30:13.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIDynamicAnimator.h
 //  UIKit
 //
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIEvent.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIEvent.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIEvent.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIEvent.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIEvent.h
 //  UIKit
 //
-//  Copyright (c) 2005-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFocus.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFocus.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFocus.h	2016-06-27 06:32:25.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFocus.h	2016-07-14 06:20:59.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIFocus.h
 //  UIKit
 //
-//  Copyright © 2015 Apple Inc. All rights reserved.
+//  Copyright © 2015-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFocusGuide.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFocusGuide.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFocusGuide.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFocusGuide.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIFocusGuide.h
 //  UIKit
 //
-//  Copyright © 2015 Apple Inc. All rights reserved.
+//  Copyright © 2015-2016 Apple Inc. All rights reserved.
 //
 
 #import <UIKit/UILayoutGuide.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIFont.h
 //  UIKit
 //
-//  Copyright (c) 2007-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2007-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h	2016-06-27 06:29:56.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h	2016-07-11 07:32:59.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIFontDescriptor.h
 //  UIKit
 //
-//  Copyright (c) 2013-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2013-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGeometry.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGeometry.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGeometry.h	2016-06-27 07:06:58.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGeometry.h	2016-07-13 05:29:34.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIGeometry.h
 //  UIKit
 //
-//  Copyright (c) 2005-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
 //
 
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGestureRecognizer.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGestureRecognizer.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGestureRecognizer.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGestureRecognizer.h	2016-07-13 05:29:35.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIGestureRecognizer.h
 //  UIKit
 //
-//  Copyright (c) 2008-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2008-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphics.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphics.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphics.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphics.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIGraphics.h
 //  UIKit
 //
-//  Copyright (c) 2005-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGuidedAccessRestrictions.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGuidedAccessRestrictions.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGuidedAccessRestrictions.h	2016-06-29 06:52:46.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGuidedAccessRestrictions.h	2016-07-13 05:30:13.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIGuidedAccessRestrictions.h
 //  UIKit
 //
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImage.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImage.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImage.h	2016-06-27 07:06:58.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImage.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIImage.h
 //  UIKit
 //
-//  Copyright (c) 2005-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImageAsset.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImageAsset.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImageAsset.h	2016-06-29 06:52:46.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImageAsset.h	2016-07-13 05:30:13.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIImageAsset.h
 //  UIKit
 //
-//  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
 #import <UIKit/UIImage.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImageView.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImageView.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImageView.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImageView.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIImageView.h
 //  UIKit
 //
-//  Copyright (c) 2006-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2006-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIInterface.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIInterface.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIInterface.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIInterface.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIInterface.h
 //  UIKit
 //
-//  Copyright (c) 2005-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h	2016-06-27 07:06:58.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h	2016-07-11 07:25:47.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIKit.h
 //  UIKit
 //
-//  Copyright (c) 2005-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
 //
 
 #import <UIKit/UIKitDefines.h>
@@ -46,6 +46,7 @@
 
 #if __has_include(<UIKit/UIContentSizeCategoryAdjusting.h>)
 #import <UIKit/UIContentSizeCategoryAdjusting.h>
+#import <UIKit/UIContentSizeCategory.h>
 #import <UIKit/UIControl.h>
 #import <UIKit/UIDataDetectors.h>
 #import <UIKit/UIDatePicker.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIKitDefines.h
 //  UIKit
 //
-//  Copyright (c) 2007-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2007-2016 Apple Inc. All rights reserved.
 //
 
 #import <Availability.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILabel.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILabel.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILabel.h	2016-06-27 06:29:56.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILabel.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UILabel.h
 //  UIKit
 //
-//  Copyright (c) 2006-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2006-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILocalNotification.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILocalNotification.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILocalNotification.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILocalNotification.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UILocalNotification.h
 //  UIKit
 //
-//  Copyright (c) 2007-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2007-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIManagedDocument.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIManagedDocument.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIManagedDocument.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIManagedDocument.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIManagedDocument.h
 //  UIKit
 //
-//  Copyright (c) 2011-2015 Apple Inc.
+//  Copyright (c) 2011-2016 Apple Inc.
 //  All rights reserved.
 //
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIMenuController.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIMenuController.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIMenuController.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIMenuController.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIMenuController.h
 //  UIKit
 //
-//  Copyright (c) 2009-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2009-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINavigationController.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINavigationController.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINavigationController.h	2016-06-27 06:32:24.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINavigationController.h	2016-07-13 05:29:34.000000000 +0200
@@ -2,7 +2,7 @@
 //  UINavigationController.h
 //  UIKit
 //
-//  Copyright (c) 2007-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2007-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINibLoading.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINibLoading.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINibLoading.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINibLoading.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UINibLoading.h
 //  UIKit
 //
-//  Copyright (c) 2005-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
@@ -13,7 +13,7 @@
 UIKIT_EXTERN NSString * const UINibExternalObjects NS_AVAILABLE_IOS(3_0);
 
 @interface NSBundle(UINibLoadingAdditions)
-- (NSArray *)loadNibNamed:(NSString *)name owner:(nullable id)owner options:(nullable NSDictionary *)options;
+- (nullable NSArray *)loadNibNamed:(NSString *)name owner:(nullable id)owner options:(nullable NSDictionary *)options;
 @end
 
 @interface NSObject(UINibLoadingAdditions)
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPanGestureRecognizer.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPanGestureRecognizer.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPanGestureRecognizer.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPanGestureRecognizer.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIPanGestureRecognizer.h
 //  UIKit
 //
-//  Copyright (c) 2008-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2008-2016 Apple Inc. All rights reserved.
 //
 
 #import <CoreGraphics/CoreGraphics.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPasteboard.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPasteboard.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPasteboard.h	2016-06-29 06:37:32.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPasteboard.h	2016-07-13 05:29:35.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIPasteboard.h
 //  UIKit
 //
-//  Copyright (c) 2008-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2008-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverBackgroundView.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverBackgroundView.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverBackgroundView.h	2016-06-29 06:52:46.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverBackgroundView.h	2016-07-13 05:30:13.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIPopoverBackgroundView.h
 //  UIKit
 //
-//  Copyright (c) 2011-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2011-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverPresentationController.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverPresentationController.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverPresentationController.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverPresentationController.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIPopoverPresentationController.h
 //  UIKit
 //
-//  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
 #import <UIKit/UIPresentationController.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverSupport.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverSupport.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverSupport.h	2016-06-29 06:52:46.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverSupport.h	2016-07-13 05:30:13.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIPopoverSupport.h
 //  UIKit
 //
-//  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
 #import <UIKit/UIViewController.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPresentationController.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPresentationController.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPresentationController.h	2016-06-27 06:29:56.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPresentationController.h	2016-07-14 06:20:58.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIPresentationController.h
 //  UIKit
 //
-//  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPressesEvent.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPressesEvent.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPressesEvent.h	2016-06-29 06:52:46.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPressesEvent.h	2016-07-13 05:30:13.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIPressesEvent.h
 //  UIKit
 //
-//  Copyright (c) 2005-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
 //
 
 #import <UIKit/UIEvent.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrinterPickerController.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrinterPickerController.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrinterPickerController.h	2016-06-29 06:52:46.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrinterPickerController.h	2016-07-13 05:30:13.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIPrinterPickerController.h
 //  UIKit
 //
-//  Copyright (c) 2013-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2013-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIRegion.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIRegion.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIRegion.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIRegion.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIRegion.h
 //  UIKit
 //
-//  Copyright © 2015 Apple Inc. All rights reserved.
+//  Copyright © 2015-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIResponder.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIResponder.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIResponder.h	2016-06-27 06:29:56.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIResponder.h	2016-07-13 05:29:34.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIResponder.h
 //  UIKit
 //
-//  Copyright (c) 2005-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScreen.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScreen.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScreen.h	2016-06-27 06:29:57.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScreen.h	2016-07-14 06:20:58.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIScreen.h
 //  UIKit
 //
-//  Copyright (c) 2007-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2007-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScrollView.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScrollView.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScrollView.h	2016-06-27 06:32:24.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScrollView.h	2016-07-13 05:29:34.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIScrollView.h
 //  UIKit
 //
-//  Copyright (c) 2007-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2007-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchContainerViewController.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchContainerViewController.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchContainerViewController.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchContainerViewController.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UISearchContainerViewController.h
 //  UIKit
 //
-//  Copyright © 2015 Apple Inc. All rights reserved.
+//  Copyright © 2015-2016 Apple Inc. All rights reserved.
 //
 
 #import <UIKit/UIViewController.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchController.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchController.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchController.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchController.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UISearchController.h
 //  UIKit
 //
-//  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
 #import <UIKit/UIPresentationController.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchDisplayController.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchDisplayController.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchDisplayController.h	2016-06-27 06:32:24.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchDisplayController.h	2016-07-13 05:29:35.000000000 +0200
@@ -2,7 +2,7 @@
 //  UISearchDisplayController.h
 //  UIKit
 //
-//  Copyright (c) 2009-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2009-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISplitViewController.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISplitViewController.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISplitViewController.h	2016-06-27 06:29:57.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISplitViewController.h	2016-07-14 06:20:59.000000000 +0200
@@ -2,7 +2,7 @@
 //  UISplitViewController.h
 //  UIKit
 //
-//  Copyright (c) 2009-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2009-2016 Apple Inc. All rights reserved.
 //
 
 #import <UIKit/UIViewController.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIStackView.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIStackView.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIStackView.h	2016-06-27 06:32:25.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIStackView.h	2016-07-13 05:30:13.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIStackView.h
 //  UIKit
 //
-//  Copyright © 2015 Apple Inc. All rights reserved.
+//  Copyright © 2015-2016 Apple Inc. All rights reserved.
 //
 
 #import <UIKit/UIView.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBar.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBar.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBar.h	2016-06-27 06:29:57.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBar.h	2016-07-14 06:20:58.000000000 +0200
@@ -2,7 +2,7 @@
 //  UITabBar.h
 //  UIKit
 //
-//  Copyright (c) 2008-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2008-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBarItem.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBarItem.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBarItem.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBarItem.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UITabBarItem.h
 //  UIKit
 //
-//  Copyright (c) 2008-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2008-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableView.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableView.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableView.h	2016-06-27 06:32:24.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableView.h	2016-07-14 06:20:58.000000000 +0200
@@ -2,7 +2,7 @@
 //  UITableView.h
 //  UIKit
 //
-//  Copyright (c) 2005-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
@@ -142,8 +142,8 @@
 - (BOOL)tableView:(UITableView *)tableView shouldIndentWhileEditingRowAtIndexPath:(NSIndexPath *)indexPath;
 
 // The willBegin/didEnd methods are called whenever the 'editing' property is automatically changed by the table (allowing insert/delete/move). This is done by a swipe activating a single row
-- (void)tableView:(UITableView*)tableView willBeginEditingRowAtIndexPath:(NSIndexPath *)indexPath __TVOS_PROHIBITED;
-- (void)tableView:(UITableView*)tableView didEndEditingRowAtIndexPath:(NSIndexPath *)indexPath __TVOS_PROHIBITED;
+- (void)tableView:(UITableView *)tableView willBeginEditingRowAtIndexPath:(NSIndexPath *)indexPath __TVOS_PROHIBITED;
+- (void)tableView:(UITableView *)tableView didEndEditingRowAtIndexPath:(nullable NSIndexPath *)indexPath __TVOS_PROHIBITED;
 
 // Moving/reordering
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableViewController.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableViewController.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableViewController.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableViewController.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UITableViewController.h
 //  UIKit
 //
-//  Copyright (c) 2008-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2008-2016 Apple Inc. All rights reserved.
 //
 #import <Foundation/Foundation.h>
 #import <UIKit/UIViewController.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextChecker.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextChecker.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextChecker.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextChecker.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UITextChecker.h
 //  UIKit
 //
-//  Copyright (c) 2009-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2009-2016 Apple Inc. All rights reserved.
 //
 
 #import <UIKit/UIKitDefines.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextField.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextField.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextField.h	2016-06-27 06:32:24.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextField.h	2016-07-14 06:20:58.000000000 +0200
@@ -2,7 +2,7 @@
 //  UITextField.h
 //  UIKit
 //
-//  Copyright (c) 2005-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInput.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInput.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInput.h	2016-06-27 06:32:24.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInput.h	2016-07-14 06:20:59.000000000 +0200
@@ -2,7 +2,7 @@
 //  UITextInput.h
 //  UIKit
 //
-//  Copyright (c) 2009-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2009-2016 Apple Inc. All rights reserved.
 //
 
 #import <CoreGraphics/CoreGraphics.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInputTraits.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInputTraits.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInputTraits.h	2016-06-27 06:32:24.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInputTraits.h	2016-07-14 06:20:58.000000000 +0200
@@ -2,7 +2,7 @@
 //  UITextInputTraits.h
 //  UIKit
 //
-//  Copyright (c) 2006-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2006-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextView.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextView.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextView.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextView.h	2016-07-14 06:20:58.000000000 +0200
@@ -2,7 +2,7 @@
 //  UITextView.h
 //  UIKit
 //
-//  Copyright (c) 2007-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2007-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITimingParameters.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITimingParameters.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITimingParameters.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITimingParameters.h	2016-07-13 05:30:12.000000000 +0200
@@ -6,6 +6,7 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <UIKit/UIView.h>
 #import <UIKit/UITimingCurveProvider.h>
 
 NS_ASSUME_NONNULL_BEGIN
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITraitCollection.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITraitCollection.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITraitCollection.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITraitCollection.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UITraitCollection.h
 //  UIKit
 //
-//  Copyright (c) 2013-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2013-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
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
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIUserNotificationSettings.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIUserNotificationSettings.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIUserNotificationSettings.h	2016-06-29 06:37:32.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIUserNotificationSettings.h	2016-07-13 05:29:34.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIUserNotificationSettings.h
 //  UIKit
 //
-//  Copyright (c) 2007-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2007-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIView.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIView.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIView.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIView.h	2016-07-13 05:29:34.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIView.h
 //  UIKit
 //
-//  Copyright (c) 2005-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewAnimating.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewAnimating.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewAnimating.h	2016-06-29 06:52:45.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewAnimating.h	2016-07-13 05:30:12.000000000 +0200
@@ -7,6 +7,7 @@
 
 
 #import <Foundation/Foundation.h>
+#import <CoreGraphics/CoreGraphics.h>
 
 typedef NS_ENUM(NSInteger, UIViewAnimatingState)
 {
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewController.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewController.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewController.h	2016-06-29 06:37:32.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewController.h	2016-07-13 05:30:12.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIViewController.h
 //  UIKit
 //
-//  Copyright (c) 2007-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2007-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitionCoordinator.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitionCoordinator.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitionCoordinator.h	2016-06-29 06:52:46.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitionCoordinator.h	2016-07-13 05:30:13.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIViewControllerTransitionCoordinator.h
 //  UIKit
 //
-//  Copyright (c) 2013-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2013-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitioning.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitioning.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitioning.h	2016-06-29 06:37:32.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitioning.h	2016-07-14 06:20:58.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIViewControllerTransitioning.h
 //  UIKit
 //
-//  Copyright (c) 2013-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2013-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
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
@@ -2,7 +2,7 @@
 //  UIVisualEffectView.h
 //  UIKit
 //
-//  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
 #import <UIKit/UIView.h>
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
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIWindow.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIWindow.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIWindow.h	2016-05-04 00:21:21.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIWindow.h	2016-07-14 06:20:58.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIWindow.h
 //  UIKit
 //
-//  Copyright (c) 2005-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>

```