#NotificationCenter.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetProviding.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetProviding.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetProviding.h	2015-10-03 02:07:04.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetProviding.h	2016-05-28 06:36:03.000000000 +0200
@@ -5,6 +5,8 @@
 //  Copyright (c) 2014 Apple. All rights reserved.
 //
 
+#import <NotificationCenter/NotificationCenterDefines.h>
+#import <NotificationCenter/NCWidgetTypes.h>
 #import <Foundation/Foundation.h>
 #import <UIKit/UIKit.h>
 
@@ -38,15 +40,38 @@
 // Instead, widgets should load cached state in 'viewWillAppear:' in order to match the state of the view from the last 'viewWillDisappear:', then transition smoothly to the new data when it arrives.
 - (void)widgetPerformUpdateWithCompletionHandler:(void (^)(NCUpdateResult result))completionHandler;
 
+// If implemented, called when the active display mode changes.
+// The widget may wish to change its preferredContentSize to better accommodate the new display mode.
+- (void)widgetActiveDisplayModeDidChange:(NCWidgetDisplayMode)activeDisplayMode withMaximumSize:(CGSize)maxSize;
+
 // Widgets wishing to customize the default margin insets can return their preferred values.
 // Widgets that choose not to implement this method will receive the default margin insets.
-- (UIEdgeInsets)widgetMarginInsetsForProposedMarginInsets:(UIEdgeInsets)defaultMarginInsets;
+- (UIEdgeInsets)widgetMarginInsetsForProposedMarginInsets:(UIEdgeInsets)defaultMarginInsets NS_DEPRECATED_IOS(8_0, 10_0, "This method will not be called on widgets linked against iOS versions 10.0 and later.");
+
+@end
+
+@interface UIVibrancyEffect (NCWidgetAdditions)
+
++ (UIVibrancyEffect *)widgetPrimaryVibrancyEffect NS_AVAILABLE_IOS(10_0); // For use with select supporting text and glyphs.
++ (UIVibrancyEffect *)widgetSecondaryVibrancyEffect NS_AVAILABLE_IOS(10_0); // For use with select supporting text and glyphs where further diminution is required.
 
 @end
 
-@interface UIVibrancyEffect (NotificationCenter)
+@interface NSExtensionContext (NCWidgetAdditions)
+
+// Widgets can change the largest display mode they make available from the default 'NCWidgetDisplayModeCompact' by messaging the extension context.
+// Modifying this property more than once during the lifetime of the widget (perhaps due to changes in the amount of available content) is supported.
+@property (nonatomic, assign) NCWidgetDisplayMode widgetLargestAvailableDisplayMode NS_AVAILABLE_IOS(10_0);
+@property (nonatomic, assign, readonly) NCWidgetDisplayMode widgetActiveDisplayMode NS_AVAILABLE_IOS(10_0);
 
-+ (UIVibrancyEffect *)notificationCenterVibrancyEffect;
+- (CGSize)widgetMaximumSizeForDisplayMode:(NCWidgetDisplayMode)displayMode NS_AVAILABLE_IOS(10_0);
 
 @end
+
+@interface UIVibrancyEffect (NCWidgetDeprecated)
+
++ (UIVibrancyEffect *)notificationCenterVibrancyEffect NS_DEPRECATED_IOS(8_0, 10_0, "Please use '-[UIVibrancyEffect widgetPrimaryVibrancyEffect]' instead.");
+
+@end
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetTypes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetTypes.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetTypes.h	2016-05-28 06:36:03.000000000 +0200
@@ -0,0 +1,13 @@
+//
+//  NCWidgetTypes.h
+//  NotificationCenter
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+typedef NS_ENUM(NSInteger, NCWidgetDisplayMode) {
+    NCWidgetDisplayModeCompact, // Fixed height
+    NCWidgetDisplayModeExpanded, // Variable height
+} NS_ENUM_AVAILABLE_IOS(10_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NotificationCenter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NotificationCenter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NotificationCenter.h	2015-10-03 02:07:04.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NotificationCenter.h	2016-05-28 06:36:03.000000000 +0200
@@ -7,3 +7,4 @@
 
 #import <NotificationCenter/NCWidgetProviding.h>
 #import <NotificationCenter/NCWidgetController.h>
+#import <NotificationCenter/NCWidgetTypes.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NotificationCenterDefines.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NotificationCenterDefines.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NotificationCenterDefines.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NotificationCenterDefines.h	2016-05-28 06:36:03.000000000 +0200
@@ -0,0 +1,14 @@
+//
+//  NotificationCenterDefines.h
+//  NotificationCenter
+//
+//  Copyright © 2015 Apple. All rights reserved.
+//
+
+#import <Availability.h>
+
+#ifdef __cplusplus
+#define NOTIFICATION_CENTER_EXTERN extern "C" __attribute__((visibility ("default")))
+#else
+#define NOTIFICATION_CENTER_EXTERN extern __attribute__((visibility ("default")))
+#endif

```