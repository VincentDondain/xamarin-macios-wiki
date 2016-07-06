#QuickLook.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuickLook.framework/Headers/QLPreviewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuickLook.framework/Headers/QLPreviewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuickLook.framework/Headers/QLPreviewController.h	2015-10-03 02:04:39.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuickLook.framework/Headers/QLPreviewController.h	2016-05-26 07:33:21.000000000 +0200
@@ -5,7 +5,6 @@
 //  Copyright 2008 Apple Inc. All rights reserved.
 //
 
-
 #import <UIKit/UIKit.h>
 #import <QuickLook/QLBase.h>
 
@@ -17,10 +16,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 4_0) QL_EXPORT
-@interface QLPreviewController : UIViewController {
-    QLPreviewControllerReserved * _reserved;
-}
+NS_CLASS_AVAILABLE_IOS(4_0) QL_EXPORT
+@interface QLPreviewController : UIViewController
 
 /*!
  * @abstract Returns YES if QLPreviewController can display this preview item.
@@ -34,7 +31,7 @@
 /*!
  * @abstract The Preview Panel data source.
  */
-@property(weak, nullable) id <QLPreviewControllerDataSource> dataSource;
+@property(nonatomic, weak, nullable) id <QLPreviewControllerDataSource> dataSource;
 
 /*!
  * @abstract Asks the Preview Controller to reload its data from its data source.
@@ -67,7 +64,7 @@
  * @abstract The Preview Controller delegate.
  * @discussion Should implement the <QLPreviewControllerDelegate> protocol
  */
-@property(weak, nullable) id <QLPreviewControllerDelegate> delegate;
+@property(nonatomic, weak, nullable) id <QLPreviewControllerDelegate> delegate;
 
 @end
 
@@ -101,6 +98,7 @@
 QL_EXPORT @protocol QLPreviewControllerDelegate <NSObject>
 @optional
 
+
 /*!
  * @abstract Invoked before the preview controller is closed.
  */
@@ -122,7 +120,7 @@
  * @abstract Invoked when the preview controller is about to be presented full screen or dismissed from full screen, to provide a zoom effect.
  * @discussion Return the origin of the zoom. It should be relative to view, or screen based if view is not set. The controller will fade in/out if the rect is CGRectZero.
  */
-- (CGRect)previewController:(QLPreviewController *)controller frameForPreviewItem:(id <QLPreviewItem>)item inSourceView:(UIView * __nullable * __nonnull)view;
+- (CGRect)previewController:(QLPreviewController *)controller frameForPreviewItem:(id <QLPreviewItem>)item inSourceView:(UIView * _Nullable * __nonnull)view;
 
 /*!
  * @abstract Invoked when the preview controller is about to be presented full screen or dismissed from full screen, to provide a smooth transition when zooming.
@@ -131,6 +129,13 @@
  */
 - (UIImage *)previewController:(QLPreviewController *)controller transitionImageForPreviewItem:(id <QLPreviewItem>)item contentRect:(CGRect *)contentRect;
 
+/*!
+ * @abstract Invoked when the preview controller is about to be presented full screen or dismissed from full screen, to provide a smooth transition when zooming.
+ * @discussion  Return the view that will crossfade with the preview.
+ */
+- (UIView* _Nullable)previewController:(QLPreviewController *)controller transitionViewForPreviewItem:(id <QLPreviewItem>)item NS_AVAILABLE_IOS(10_0);
+
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuickLook.framework/Headers/QLPreviewItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuickLook.framework/Headers/QLPreviewItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuickLook.framework/Headers/QLPreviewItem.h	2015-10-03 02:04:39.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuickLook.framework/Headers/QLPreviewItem.h	2016-05-26 07:50:44.000000000 +0200
@@ -5,12 +5,12 @@
 //  Copyright 2008 Apple Inc. All rights reserved.
 //
 
-
 #import <Foundation/Foundation.h>
-#import <QuickLook/QLBase.h>
+
+#include <QuickLook/QLBase.h>
 
 /*!
- * @abstract The QLPreviewItem protocol declares the methods that a QLPreviewController  instance uses to access the contents of a given item.
+ * @abstract The QLPreviewItem protocol declares the methods that a QLPreviewController instance uses to access the contents of a given item.
  */
 QL_EXPORT @protocol QLPreviewItem <NSObject>
 
@@ -18,9 +18,9 @@
 
 /*!
  * @abstract The URL of the item to preview.
- * @discussion The URL must be a file URL. 
+ * @discussion The URL must be a file URL.
  */
-@property(readonly, nonnull, nonatomic) NSURL * previewItemURL;
+@property(readonly, nullable, nonatomic) NSURL * previewItemURL;
 
 @optional
 
@@ -38,5 +38,3 @@
  */
 @interface NSURL (QLPreviewConvenienceAdditions) <QLPreviewItem>
 @end
-
-
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuickLook.framework/Headers/QuickLook.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuickLook.framework/Headers/QuickLook.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuickLook.framework/Headers/QuickLook.h	2015-10-03 02:04:39.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/QuickLook.framework/Headers/QuickLook.h	2016-05-26 07:50:44.000000000 +0200
@@ -1,22 +1,20 @@
 //
 //  QuickLook.h
-//  Quick Look
+//  QuickLook
 //
-//  Copyright 2008 Apple Inc.
-//  All rights reserved.
+//  Copyright (c) 2008-2015 Apple Inc. All rights reserved.
 //
- 
+
+
 #if !defined(__QUICKLOOK_QUICKLOOK__)
 #define __QUICKLOOK_QUICKLOOK__
 
 #include <CoreFoundation/CoreFoundation.h>
 #include <QuickLook/QLBase.h>
 
-
 #if __OBJC__
 #import <QuickLook/QLPreviewController.h>
 #import <QuickLook/QLPreviewItem.h>
 #endif
 
-
 #endif

```