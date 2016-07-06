#AppKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKit.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKit.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	AppKit.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 
 	This file is included by all AppKit application source files for easy building.  Using this file is preferred over importing individual files because it will use a precompiled version.
@@ -59,6 +59,8 @@
 #import <AppKit/NSDragging.h>
 #import <AppKit/NSDraggingItem.h>
 #import <AppKit/NSDraggingSession.h>
+#import <AppKit/NSFilePromiseProvider.h>
+#import <AppKit/NSFilePromiseReceiver.h>
 #import <AppKit/NSEPSImageRep.h>
 #import <AppKit/NSErrors.h>
 #import <AppKit/NSEvent.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitDefines.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitDefines.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitDefines.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitDefines.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	AppKitDefines.h
 	Application Kit
-	Copyright (c) 1995-2015, Apple Inc.
+	Copyright (c) 1995-2016, Apple Inc.
 	All rights reserved.
 */
 #ifndef _APPKITDEFINES_H
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitErrors.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitErrors.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitErrors.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitErrors.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	AppKitErrors.h
 	Application Kit
-	Copyright (c) 2004-2015, Apple Inc.
+	Copyright (c) 2004-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSATSTypesetter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSATSTypesetter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSATSTypesetter.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSATSTypesetter.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSATSTypesetter.h
         Application Kit
-        Copyright (c) 2002-2015, Apple Inc.
+        Copyright (c) 2002-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibility.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibility.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibility.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibility.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSAccessibility.h
 	Application Kit
-	Copyright (c) 2001-2015, Apple Inc.
+	Copyright (c) 2001-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -95,6 +95,12 @@
 /* Get the current accessibility display option for reduce transparency. If this property's value is true, UI (mainly window) backgrounds should not be semi-transparent; they should be opaque. You may listen for NSWorkspaceAccessibilityDisplayOptionsDidChangeNotification to be notified when this changes. */
 @property (readonly) BOOL accessibilityDisplayShouldReduceTransparency NS_AVAILABLE_MAC(10_10);
 
+/* Get the current accessibility display option for reduce motion. If this property's value is true, UI should avoid large animations, especially those that simulate the third dimension. You may listen for NSWorkspaceAccessibilityDisplayOptionsDidChangeNotification to be notified when this changes. */
+@property (readonly) BOOL accessibilityDisplayShouldReduceMotion NS_AVAILABLE_MAC(10_12);
+
+/* Get the current accessibility display option for invert colors. If this property's value is true then the display will be inverted. In these cases it may be needed for UI drawing to be adjusted to in order to display optimally when inverted.  You may listen for NSWorkspaceAccessibilityDisplayOptionsDidChangeNotification to be notified when this changes. */
+@property (readonly) BOOL accessibilityDisplayShouldInvertColors NS_AVAILABLE_MAC(10_12);
+
 @end
 
 /* Notification posted to the NSWorkspace notification center when any accessibility display options have changed. */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibilityConstants.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibilityConstants.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibilityConstants.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibilityConstants.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSAccessibilityConstants.h
 	Application Kit
-	Copyright (c) 2001-2015, Apple Inc.
+	Copyright (c) 2001-2016, Apple Inc.
 	All rights reserved.
 */
 #import <AppKit/AppKitDefines.h>
@@ -86,6 +86,7 @@
 NS_AVAILABLE_MAC(10_6);
 APPKIT_EXTERN NSString *const NSAccessibilityContainsProtectedContentAttribute NS_AVAILABLE_MAC(10_9);   // (NSNumber *) - (boolValue) contains protected content?
 APPKIT_EXTERN NSString *const NSAccessibilityAlternateUIVisibleAttribute NS_AVAILABLE_MAC(10_10);  //(NSNumber *) - (boolValue)
+APPKIT_EXTERN NSString *const NSAccessibilityRequiredAttribute NS_AVAILABLE_MAC(10_12);  //(NSNumber *) - (boolValue) whether a form field is required to have content for successful submission of the form
 
 
 /* Linkage attributes
@@ -135,6 +136,7 @@
 APPKIT_EXTERN NSString *const NSAccessibilityAttachmentTextAttribute;		//id - corresponding element
 APPKIT_EXTERN NSString *const NSAccessibilityLinkTextAttribute;			//id - corresponding element
 APPKIT_EXTERN NSString *const NSAccessibilityAutocorrectedTextAttribute NS_AVAILABLE_MAC(10_7);		//(NSNumber *)	    - (boolValue)
+APPKIT_EXTERN NSString *const NSAccessibilityTextAlignmentAttribute NS_AVAILABLE_MAC(10_12);		//(NSNumber *) - (NSTextAlignment)
 
 /* Textual list attributes and constants. Examples: unordered or ordered lists in a document.
  */
@@ -438,6 +440,7 @@
 APPKIT_EXTERN NSString *const NSAccessibilityValueIndicatorRole;
 APPKIT_EXTERN NSString *const NSAccessibilityImageRole;
 APPKIT_EXTERN NSString *const NSAccessibilityMenuBarRole;
+APPKIT_EXTERN NSString *const NSAccessibilityMenuBarItemRole NS_AVAILABLE_MAC(10_12);
 APPKIT_EXTERN NSString *const NSAccessibilityMenuRole;
 APPKIT_EXTERN NSString *const NSAccessibilityMenuItemRole;
 APPKIT_EXTERN NSString *const NSAccessibilityColumnRole;
@@ -475,7 +478,6 @@
 APPKIT_EXTERN NSString *const NSAccessibilityLayoutItemRole NS_AVAILABLE_MAC(10_6);
 APPKIT_EXTERN NSString *const NSAccessibilityHandleRole NS_AVAILABLE_MAC(10_6);
 
-
 /* Subroles
  */
 APPKIT_EXTERN NSString *const NSAccessibilityUnknownSubrole;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibilityElement.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibilityElement.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibilityElement.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibilityElement.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSAccessibilityElement.h
 	Application Kit
-	Copyright (c) 2013-2015, Apple Inc.
+	Copyright (c) 2013-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibilityProtocols.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibilityProtocols.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibilityProtocols.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibilityProtocols.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
  NSAccessibilityProtocols.h
  Application Kit
- Copyright (c) 2013-2015, Apple Inc.
+ Copyright (c) 2013-2016, Apple Inc.
  All rights reserved.
  */
 
@@ -182,6 +182,7 @@
 @protocol NSAccessibilityLayoutArea <NSAccessibilityGroup>
 @required
 - (NSString *)accessibilityLabel;
+
 // All of the layoutItem children
 - (nullable NSArray *)accessibilityChildren;
 
@@ -189,7 +190,7 @@
 - (nullable NSArray *)accessibilitySelectedChildren;
 
 // The focused layoutItem
-- (id)accessibilityFocusedUIElement;
+@property (readonly, strong) id accessibilityFocusedUIElement;
 
 @end
 
@@ -383,6 +384,10 @@
 // Invokes when clients request NSAccessibilitySharedFocusElementsAttribute
 @property (nullable, copy) NSArray *accessibilitySharedFocusElements NS_AVAILABLE_MAC(10_10);
 
+// Returns YES if the UIElement is required to have content for successful submission of a form
+// Invokes when clients request NSAccessibilityRequiredAttribute
+@property (getter=isAccessibilityRequired) BOOL accessibilityRequired NS_AVAILABLE_MAC(10_12);
+
 #pragma mark Application
 
 // Returns YES if the element is focused (generally, accessibilityFocused is equivalent to the
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSActionCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSActionCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSActionCell.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSActionCell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSActionCell.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAffineTransform.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAffineTransform.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAffineTransform.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAffineTransform.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSAffineTransform.h
         Application Kit
-        Copyright (c) 1997-2015, Apple Inc.
+        Copyright (c) 1997-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -13,7 +13,7 @@
 
 @interface NSAffineTransform (NSAppKitAdditons)
 // Transform a path
-- (NSBezierPath *)transformBezierPath:(NSBezierPath *)aPath;
+- (NSBezierPath *)transformBezierPath:(NSBezierPath *)path;
 
 // Setting a transform in NSGraphicsContext
 - (void)set;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAlert.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAlert.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAlert.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAlert.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSAlert.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -16,12 +16,12 @@
 @protocol NSAlertDelegate;
 
 
-/* The default alert style is NSWarningAlertStyle.  NSCriticalAlertStyle should be reserved for critical alerts and will cause the icon to be badged with a caution icon.
+/* The default alert style is NSAlertStyleWarning.  NSAlertStyleCritical should be reserved for critical alerts and will cause the icon to be badged with a caution icon.
 */
 typedef NS_ENUM(NSUInteger, NSAlertStyle) {
-    NSWarningAlertStyle = 0,
-    NSInformationalAlertStyle = 1,
-    NSCriticalAlertStyle = 2
+    NSAlertStyleWarning = 0,
+    NSAlertStyleInformational = 1,
+    NSAlertStyleCritical = 2
 };
 
 @interface NSAlert : NSObject
@@ -55,7 +55,9 @@
     BOOL _layoutDone;
     BOOL _showsHelp;
     BOOL _showsSuppressionButton;
+#ifndef __OBJC2__
     BOOL reserved;
+#endif
     id _suppressionButton;
     id _accessoryView;
 }
@@ -65,14 +67,6 @@
 */
 + (NSAlert *)alertWithError:(NSError *)error;
 
-
-/* This method is deprecated in 10.9 and will be formally deprecated in the following release.
- This was intended for use by apps migrating from the C-based API.  This uses alternate return codes that were compatible with this C-based API, but not with modern alerts, see NSAlertDefaultReturn, etc. in NSPanel.h
- Alerts should be created with the -init method and setting properties.
- */
-+ (NSAlert *)alertWithMessageText:(nullable NSString *)message defaultButton:(nullable NSString *)defaultButton alternateButton:(nullable NSString *)alternateButton otherButton:(nullable NSString *)otherButton informativeTextWithFormat:(NSString *)format, ... NS_FORMAT_FUNCTION(5,6) NS_DEPRECATED_MAC(10_3, 10_10, "Use -init instead");
-
-
 @property (copy) NSString *messageText;
 @property (copy) NSString *informativeText;
 
@@ -122,7 +116,10 @@
 
 @property NSAlertStyle alertStyle;
 
-@property (nullable, assign) id<NSAlertDelegate> delegate;
+/* The delegate of the receiver, currently only allows for custom help behavior of the alert.
+   For apps linked against 10.12, this property has zeroing weak memory semantics. When linked against an older SDK this back to having `retain` semantics, matching legacy behavior.
+ */
+@property (nullable, weak) id<NSAlertDelegate> delegate;
 
 /* -setShowsSuppressionButton: indicates whether or not the alert should contain a suppression checkbox.  The default is NO.  This checkbox is typically used to give the user an option to not show this alert again.  If shown, the suppression button will have a default localized title similar to @"Do not show this message again".  You can customize this title using [[alert suppressionButton] setTitle:].  When the alert is dismissed, you can get the state of the suppression button, using [[alert suppressionButton] state] and store the result in user defaults, for example.  This setting can then be checked before showing the alert again.  By default, the suppression button is positioned below the informative text, and above the accessory view (if any) and the alert buttons, and left-aligned with the informative text.  However do not count on the placement of this button, since it might be moved if the alert panel user interface is changed in the future. If you need a checkbox for purposes other than suppression text, it is recommended you create your own using an accessory view.
 */
@@ -146,13 +143,8 @@
 */
 - (NSModalResponse)runModal;
 
-/* This method is deprecated in 10.9 and will be formally deprecated in the following release.
- -beginSheetModalForWindow:completionHandler: should be used instead.
- */
-- (void)beginSheetModalForWindow:(NSWindow *)window modalDelegate:(nullable id)delegate didEndSelector:(nullable SEL)didEndSelector contextInfo:(nullable void *)contextInfo NS_DEPRECATED_MAC(10_3, 10_10, "Use -beginSheetModalForWindow:completionHandler: instead");
-
 /* Begins a sheet on the doc window using NSWindow's sheet API.
-   If the alert has an alertStyle of NSCriticalAlertStyle, it will be shown as a "critical" sheet; it will otherwise be presented as a normal sheet.
+   If the alert has an alertStyle of NSAlertStyleCritical, it will be shown as a "critical" sheet; it will otherwise be presented as a normal sheet.
  */
 - (void)beginSheetModalForWindow:(NSWindow *)sheetWindow completionHandler:(void (^ __nullable)(NSModalResponse returnCode))handler NS_AVAILABLE_MAC(10_9);
 
@@ -169,5 +161,25 @@
 - (BOOL)alertShowHelp:(NSAlert *)alert;
 @end
 
+
+@interface NSAlert (NSAlertDeprecated)
+
+/* This method is deprecated in 10.9 and will be formally deprecated in the following release.
+ This was intended for use by apps migrating from the C-based API.  This uses alternate return codes that were compatible with this C-based API, but not with modern alerts, see NSAlertDefaultReturn, etc. in NSPanel.h
+ Alerts should be created with the -init method and setting properties.
+ */
++ (NSAlert *)alertWithMessageText:(nullable NSString *)message defaultButton:(nullable NSString *)defaultButton alternateButton:(nullable NSString *)alternateButton otherButton:(nullable NSString *)otherButton informativeTextWithFormat:(NSString *)format, ... NS_FORMAT_FUNCTION(5,6) NS_DEPRECATED_MAC(10_3, 10_10, "Use -init instead");
+
+/* This method is deprecated in 10.9 and will be formally deprecated in the following release.
+ -beginSheetModalForWindow:completionHandler: should be used instead.
+ */
+- (void)beginSheetModalForWindow:(NSWindow *)window modalDelegate:(nullable id)delegate didEndSelector:(nullable SEL)didEndSelector contextInfo:(nullable void *)contextInfo NS_DEPRECATED_MAC(10_3, 10_10, "Use -beginSheetModalForWindow:completionHandler: instead");
+
+@end
+
+static const NSAlertStyle NSWarningAlertStyle API_DEPRECATED_WITH_REPLACEMENT("NSAlertStyleWarning", macosx(10.3, 10.12)) = NSAlertStyleWarning;
+static const NSAlertStyle NSInformationalAlertStyle API_DEPRECATED_WITH_REPLACEMENT("NSAlertStyleInformational", macosx(10.3, 10.12)) = NSAlertStyleInformational;
+static const NSAlertStyle NSCriticalAlertStyle API_DEPRECATED_WITH_REPLACEMENT("NSAlertStyleCritical", macosx(10.3, 10.12)) = NSAlertStyleCritical;
+
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAlignmentFeedbackFilter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAlignmentFeedbackFilter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAlignmentFeedbackFilter.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAlignmentFeedbackFilter.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
  NSAlignmentFeedbackFilter.h
  Application Kit
- Copyright (c) 2015, Apple Inc.
+ Copyright (c) 2015-2016, Apple Inc.
  All rights reserved.
  */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAnimation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAnimation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAnimation.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAnimation.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSAnimation.h
     Application Kit
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -52,7 +52,8 @@
 	unsigned int animating:1;
 	unsigned int blocking:1;
         unsigned int sendProgressAllTheTime:1;
-	unsigned int reserved:24;
+        unsigned int hasHandler:1;
+	unsigned int reserved:23;
     } _aFlags;
     struct __aSettings {
 	unsigned int animationCurve:8;
@@ -60,12 +61,15 @@
 	unsigned int reserved:22;
     } _aSettings;
     NSRunLoop *_scheduledRunLoop;
+#ifndef __OBJC2__
     NSInteger _reserved2;
     NSInteger _reserved3;
     NSInteger _reserved4;
+#endif
 }
 
-- (instancetype)initWithDuration:(NSTimeInterval)duration animationCurve:(NSAnimationCurve)animationCurve;
+- (instancetype)initWithDuration:(NSTimeInterval)duration animationCurve:(NSAnimationCurve)animationCurve NS_DESIGNATED_INITIALIZER;
+- (nullable instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
 
 - (void)startAnimation;
 - (void)stopAnimation;
@@ -123,6 +127,7 @@
     NSArray                *_viewAnimations;
     id                      _viewAnimationInfo;
     id                      _windowAnimationInfo;
+#ifndef __OBJC2__
     NSUInteger                  _reserved4a;
     NSUInteger                  _reserved4b;
     NSUInteger                  _reserved4c;
@@ -132,7 +137,8 @@
     NSUInteger                  _reserved5;
     NSUInteger                  _reserved6;
     NSUInteger                  _reserved7;
-    NSUInteger                  _reserved8;    
+    NSUInteger                  _reserved8;
+#endif
 }
 
 - (instancetype)initWithViewAnimations:(NSArray<NSDictionary<NSString *, id> *> *)viewAnimations;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAnimationContext.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAnimationContext.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAnimationContext.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAnimationContext.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSAnimationContext.h
     Application Kit
-    Copyright (c) 2006-2015, Apple Inc.
+    Copyright (c) 2006-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -25,7 +25,7 @@
 #endif
 }
 
-+ (void)runAnimationGroup:(void (^)(NSAnimationContext * context))changes completionHandler:(nullable void (^)(void))completionHandler NS_AVAILABLE_MAC(10_7);
++ (void)runAnimationGroup:(void (NS_NOESCAPE ^)(NSAnimationContext * context))changes completionHandler:(nullable void (^)(void))completionHandler NS_AVAILABLE_MAC(10_7);
 
 + (void)beginGrouping;
 + (void)endGrouping;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAppearance.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAppearance.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAppearance.h	2015-08-26 04:17:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAppearance.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSAppearance.h
         Application Kit
-        Copyright (c) 2011-2015, Apple Inc.
+        Copyright (c) 2011-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAppleScriptExtensions.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAppleScriptExtensions.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAppleScriptExtensions.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAppleScriptExtensions.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSAppleScriptExtensions.h
 	Application Kit
-	Copyright (c) 2002-2015, Apple Inc.
+	Copyright (c) 2002-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSApplication.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSApplication.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSApplication.h	2015-11-09 03:17:17.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSApplication.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSApplication.h
     Application Kit
-    Copyright (c) 1994-2015, Apple Inc.
+    Copyright (c) 1994-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -19,6 +19,7 @@
 @class NSGraphicsContext, NSImage, NSPasteboard, NSWindow;
 @class NSDockTile;
 @class NSUserActivity;
+@class CKShareMetadata;
 @protocol NSApplicationDelegate;
 
 /* The version of the AppKit framework */
@@ -55,6 +56,11 @@
 #define NSAppKitVersionNumber10_10_4 1348
 #define NSAppKitVersionNumber10_10_5 1348
 #define NSAppKitVersionNumber10_10_Max 1349
+#define NSAppKitVersionNumber10_11 1404
+#define NSAppKitVersionNumber10_11_1 1404.13
+#define NSAppKitVersionNumber10_11_2 1404.34
+#define NSAppKitVersionNumber10_11_3 1404.34
+
 
 /* Modes passed to NSRunLoop */
 APPKIT_EXTERN NSString *NSModalPanelRunLoopMode;
@@ -102,6 +108,10 @@
     NSApplicationOcclusionStateVisible = 1UL << 1,
 } NS_ENUM_AVAILABLE_MAC(10_9);
 
+typedef NS_OPTIONS(NSInteger, NSWindowListOptions) {
+    NSWindowListOrderedFrontToBack = (1 << 0), /* Onscreen application windows in front to back order. By default, -[NSApp windows] is used. */
+} NS_ENUM_AVAILABLE_MAC(10_12);
+
 /* Information used by the system during modal sessions */
 typedef struct _NSModalSession *NSModalSession;
 // threading information
@@ -115,11 +125,11 @@
     id                  _keyWindow;
     id                  _mainWindow;
     id                  _delegate;
-    id            	*_hiddenList;
-    int                 _hiddenCount;
+    id            	_hiddenList;
+    int                 _hiddenCount __unused;
     NSInteger               _context;
     void		*_appleEventSuspensionID;
-    __weak id			_previousKeyWindow;
+    NSWindow            *_previousKeyWindowX;
     short               _unusedApp;
     short               _running;
     struct __appFlags {
@@ -156,8 +166,7 @@
         unsigned int        _mightBeSwitching:1;
     }                   _appFlags;
     id                  _mainMenu;
-    id                  _appIcon;
-    void                *_unused;
+    id                  _unused[2];
     id                  _eventDelegate;
     _NSThreadPrivate     *_threadingSupport;
 }
@@ -166,7 +175,6 @@
 
 + (__kindof NSApplication *)sharedApplication;
 @property (nullable, assign) id<NSApplicationDelegate> delegate;
-@property (nullable, readonly, strong) NSGraphicsContext *context;
 - (void)hide:(nullable id)sender;
 - (void)unhide:(nullable id)sender;
 - (void)unhideWithoutActivation;
@@ -184,13 +192,13 @@
 
 - (void)finishLaunching;
 - (void)run;
-- (NSInteger)runModalForWindow:(NSWindow *)theWindow;
+- (NSInteger)runModalForWindow:(NSWindow *)window;
 - (void)stop:(nullable id)sender;
 - (void)stopModal;
 - (void)stopModalWithCode:(NSInteger)returnCode;
 - (void)abortModal;
 @property (nullable, readonly, strong) NSWindow *modalWindow;
-- (NSModalSession)beginModalSessionForWindow:(NSWindow *)theWindow NS_RETURNS_INNER_POINTER;
+- (NSModalSession)beginModalSessionForWindow:(NSWindow *)window NS_RETURNS_INNER_POINTER;
 - (NSInteger)runModalSession:(NSModalSession)session;
 - (void)endModalSession:(NSModalSession)session;
 - (void)terminate:(nullable id)sender;
@@ -204,15 +212,11 @@
 - (NSInteger)requestUserAttention:(NSRequestUserAttentionType)requestType;
 - (void)cancelUserAttentionRequest:(NSInteger)request;
 
+/*  Execute a block for each of the app's windows. Set *stop = YES if desired, to halt the enumeration early.
+ */
+- (void)enumerateWindowsWithOptions:(NSWindowListOptions)options usingBlock:(void (NS_NOESCAPE ^) (NSWindow *window, BOOL *stop))block NS_AVAILABLE_MAC(10_12);
 
-- (nullable NSEvent *)nextEventMatchingMask:(NSUInteger)mask untilDate:(nullable NSDate *)expiration inMode:(NSString *)mode dequeue:(BOOL)deqFlag;
-- (void)discardEventsMatchingMask:(NSUInteger)mask beforeEvent:(nullable NSEvent *)lastEvent;
-- (void)postEvent:(NSEvent *)event atStart:(BOOL)flag;
-@property (nullable, readonly, strong) NSEvent *currentEvent;
-
-- (void)sendEvent:(NSEvent *)theEvent;
 - (void)preventWindowOrdering;
-- (nullable NSWindow *)makeWindowsPerform:(SEL)aSelector inOrder:(BOOL)flag;
 @property (readonly, copy) NSArray<NSWindow *> *windows;
 - (void)setWindowsNeedUpdate:(BOOL)needUpdate;
 - (void)updateWindows;
@@ -237,13 +241,7 @@
 
 @property (readonly, strong) NSDockTile *dockTile NS_AVAILABLE_MAC(10_5);
 
-- (BOOL)sendAction:(SEL)theAction to:(nullable id)theTarget from:(nullable id)sender;
-- (nullable id)targetForAction:(SEL)theAction;
-- (nullable id)targetForAction:(SEL)theAction to:(nullable id)theTarget from:(nullable id)sender;
-- (BOOL)tryToPerform:(SEL)anAction with:(nullable id)anObject;
-- (nullable id)validRequestorForSendType:(NSString *)sendType returnType:(NSString *)returnType;
-
-- (void)reportException:(NSException *)theException;
+- (void)reportException:(NSException *)exception;
 + (void)detachDrawingThread:(SEL)selector toTarget:(id)target withObject:(nullable id)argument;
 
 /*  If an application delegate returns NSTerminateLater from -applicationShouldTerminate:, -replyToApplicationShouldTerminate: must be called with YES or NO once the application decides if it can terminate */
@@ -274,12 +272,33 @@
 
 @end
 
+@interface NSApplication(NSEvent)
+- (void)sendEvent:(NSEvent *)event;
+- (void)postEvent:(NSEvent *)event atStart:(BOOL)flag;
+@property (nullable, readonly, strong) NSEvent *currentEvent;
+#if __LP64__
+- (nullable NSEvent *)nextEventMatchingMask:(NSEventMask)mask untilDate:(nullable NSDate *)expiration inMode:(NSString *)mode dequeue:(BOOL)deqFlag;
+- (void)discardEventsMatchingMask:(NSEventMask)mask beforeEvent:(nullable NSEvent *)lastEvent;
+#else
+- (nullable NSEvent *)nextEventMatchingMask:(NSUInteger)mask untilDate:(nullable NSDate *)expiration inMode:(NSString *)mode dequeue:(BOOL)deqFlag;
+- (void)discardEventsMatchingMask:(NSUInteger)mask beforeEvent:(nullable NSEvent *)lastEvent;
+#endif
+@end
+
+@interface NSApplication(NSResponder)
+- (BOOL)sendAction:(SEL)action to:(nullable id)target from:(nullable id)sender;
+- (nullable id)targetForAction:(SEL)action;
+- (nullable id)targetForAction:(SEL)action to:(nullable id)target from:(nullable id)sender;
+- (BOOL)tryToPerform:(SEL)action with:(nullable id)object;
+- (nullable id)validRequestorForSendType:(NSString *)sendType returnType:(NSString *)returnType;
+@end
+
 @interface NSApplication(NSWindowsMenu)
 @property (nullable, strong) NSMenu *windowsMenu;
 - (void)arrangeInFront:(nullable id)sender;
 - (void)removeWindowsItem:(NSWindow *)win;
-- (void)addWindowsItem:(NSWindow *)win title:(NSString *)aString filename:(BOOL)isFilename;
-- (void)changeWindowsItem:(NSWindow *)win title:(NSString *)aString filename:(BOOL)isFilename;
+- (void)addWindowsItem:(NSWindow *)win title:(NSString *)string filename:(BOOL)isFilename;
+- (void)changeWindowsItem:(NSWindow *)win title:(NSString *)string filename:(BOOL)isFilename;
 - (void)updateWindowsItem:(NSWindow *)win;
 - (void)miniaturizeAll:(nullable id)sender;
 @end
@@ -366,6 +385,13 @@
 /* This will be called on the main thread when a user activity managed by AppKit/UIKit has been updated. You should use this as a last chance to add additional data to the userActivity. */
 - (void)application:(NSApplication *)application didUpdateUserActivity:(NSUserActivity *)userActivity NS_AVAILABLE_MAC(10_10);
 
+
+/* This will be called on the main thread after the user indicates they want to accept a CloudKit sharing invitation in your application.
+ 
+ You should use the CKShareMetadata object's shareURL and containerIdentifier to schedule a CKAcceptSharesOperation, then start using the resulting CKShare and its associated record(s), which will appear in the CKContainer's shared database in a zone matching that of the record's owner.
+*/
+- (void)application:(NSApplication *)application userAcceptedCloudKitShareWithMetadata:(CKShareMetadata *)metadata NS_AVAILABLE_MAC(10_12);
+
 /* Notifications:
  */
 - (void)applicationWillFinishLaunching:(NSNotification *)notification;
@@ -529,13 +555,13 @@
  ** runModalForWindow:relativeToWindow: was deprecated in Mac OS 10.0.  
  ** Please use -[NSWindow beginSheet:completionHandler:] instead
  */
-- (NSInteger)runModalForWindow:(null_unspecified NSWindow *)theWindow relativeToWindow:(null_unspecified NSWindow *)docWindow NS_DEPRECATED_MAC(10_0, 10_0);
+- (NSInteger)runModalForWindow:(null_unspecified NSWindow *)window relativeToWindow:(null_unspecified NSWindow *)docWindow NS_DEPRECATED_MAC(10_0, 10_0);
 
 /* 
  ** beginModalSessionForWindow:relativeToWindow: was deprecated in Mac OS 10.0.
  ** Please use -[NSWindow beginSheet:completionHandler:] instead
  */
-- (NSModalSession)beginModalSessionForWindow:(null_unspecified NSWindow *)theWindow relativeToWindow:(null_unspecified NSWindow *)docWindow NS_RETURNS_INNER_POINTER NS_DEPRECATED_MAC(10_0, 10_0);
+- (NSModalSession)beginModalSessionForWindow:(null_unspecified NSWindow *)window relativeToWindow:(null_unspecified NSWindow *)docWindow NS_RETURNS_INNER_POINTER NS_DEPRECATED_MAC(10_0, 10_0);
 
 // -application:printFiles: was deprecated in Mac OS 10.4. Implement application:printFiles:withSettings:showPrintPanels: in your application delegate instead.
 - (void)application:(null_unspecified NSApplication *)sender printFiles:(null_unspecified NSArray<NSString *> *)filenames NS_DEPRECATED_MAC(10_3, 10_4);
@@ -555,6 +581,13 @@
 - (void)endSheet:(NSWindow *)sheet NS_DEPRECATED_MAC(10_0, 10_10, "Use -[NSWindow endSheet:] instead");
 - (void)endSheet:(NSWindow *)sheet returnCode:(NSInteger)returnCode NS_DEPRECATED_MAC(10_0, 10_10, "Use -[NSWindow endSheet:returnCode:] instead");
 
+/* This method is soft deprecated starting with OS X 10.12. It will be officially deprecated in a future release. Use -enumerateWindowsWithOptions:usingBlock: instead.
+ */
+- (nullable NSWindow *)makeWindowsPerform:(SEL)selector inOrder:(BOOL)flag;
+
+/* This method is deprecated as of OS X 10.12. Beginning in OS X 10.11 it would always return nil. Prior to this it would return an undefined graphics context that was not generally suitable for drawing.
+ */
+@property (nullable, readonly, strong) NSGraphicsContext *context NS_DEPRECATED_MAC(10_0, 10_12, "This method always returns nil. If you need access to the current drawing context, use [NSGraphicsContext currentContext] inside of a draw operation.");
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSApplicationScripting.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSApplicationScripting.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSApplicationScripting.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSApplicationScripting.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSApplicationScripting.h
         AppKit Framework
-        Copyright (c) 1997-2015, Apple Inc.
+        Copyright (c) 1997-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSArrayController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSArrayController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSArrayController.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSArrayController.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSArrayController.h
 	Application Kit
-	Copyright (c) 2002-2015, Apple Inc.
+	Copyright (c) 2002-2016, Apple Inc.
 	All rights reserved.
  */
 
@@ -16,7 +16,9 @@
 
 @interface NSArrayController : NSObjectController {
 @private
+#ifndef __OBJC2__
     void *_reserved4;
+#endif
     id _rearrangementExtensions;
     NSMutableArray *_temporaryWorkObjects;
     struct __arrayControllerFlags {
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAttributedString.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAttributedString.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAttributedString.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAttributedString.h	2016-06-03 05:13:45.000000000 +0200
@@ -40,7 +40,7 @@
 APPKIT_EXTERN NSString *  NSObliquenessAttributeName NS_AVAILABLE(10_0, 7_0);         // NSNumber containing floating point value; skew to be applied to glyphs, default 0: no skew
 APPKIT_EXTERN NSString *  NSExpansionAttributeName NS_AVAILABLE(10_0, 7_0);           // NSNumber containing floating point value; log of expansion factor to be applied to glyphs, default 0: no expansion
 
-APPKIT_EXTERN NSString *  NSWritingDirectionAttributeName NS_AVAILABLE(10_6, 7_0);    // NSArray of NSNumbers representing the nested levels of writing direction overrides as defined by Unicode LRE, RLE, LRO, and RLO characters.  The control characters can be obtained by masking NSWritingDirection and NSTextWritingDirection values.  LRE: NSWritingDirectionLeftToRight|NSWritingDirectionEmbedding, RLE: NSWritingDirectionRightToLeft|NSWritingDirectionEmbedding, LRO: NSWritingDirectionLeftToRight|NSWritingDirectionOverride, RLO: NSWritingDirectionRightToLeft|NSWritingDirectionOverride,
+APPKIT_EXTERN NSString *  NSWritingDirectionAttributeName NS_AVAILABLE(10_6, 7_0);    // NSArray of NSNumbers representing the nested levels of writing direction overrides as defined by Unicode LRE, RLE, LRO, and RLO characters.  The control characters can be obtained by masking NSWritingDirection and NSWritingDirectionFormatType values.  LRE: NSWritingDirectionLeftToRight|NSWritingDirectionEmbedding, RLE: NSWritingDirectionRightToLeft|NSWritingDirectionEmbedding, LRO: NSWritingDirectionLeftToRight|NSWritingDirectionOverride, RLO: NSWritingDirectionRightToLeft|NSWritingDirectionOverride,
 
 APPKIT_EXTERN NSString *  NSVerticalGlyphFormAttributeName NS_AVAILABLE(10_7, 6_0);   // An NSNumber containing an integer value.  0 means horizontal text.  1 indicates vertical text.  If not specified, it could follow higher-level vertical orientation settings.  Currently on iOS, it's always horizontal.  The behavior for any other value is undefined.
 
@@ -191,7 +191,7 @@
 
 @interface NSAttributedString (NSAttributedStringDocumentFormats)
 // Methods initializing the receiver contents with an external document data.  options specify document attributes for interpreting the document contents.  NSDocumentTypeDocumentAttribute, NSCharacterEncodingDocumentAttribute, and NSDefaultAttributesDocumentAttribute are supported options key.  When they are not specified, these methods will examine the data and do their best to detect the appropriate attributes.  If dict is non-NULL, it will return a dictionary with various document-wide attributes accessible via NS...DocumentAttribute keys.
-- (nullable instancetype)initWithURL:(NSURL *)url options:(NSDictionary<NSString *, id> *)options documentAttributes:(NSDictionary<NSString *, id> * __nullable * __nullable)dict error:(NSError **)error NS_AVAILABLE(10_11, 9_0);
+- (nullable instancetype)initWithURL:(NSURL *)url options:(NSDictionary<NSString *, id> *)options documentAttributes:(NSDictionary<NSString *, id> * __nullable * __nullable)dict error:(NSError **)error NS_AVAILABLE(10_4, 9_0);
 - (nullable instancetype)initWithData:(NSData *)data options:(NSDictionary<NSString *, id> *)options documentAttributes:(NSDictionary<NSString *, id> * __nullable * __nullable)dict error:(NSError **)error NS_AVAILABLE(10_0, 7_0);
 
 // Generates an NSData object for the receiver contents in range.  It requires a document attributes dict specifying at least the NSDocumentTypeDocumentAttribute to determine the format to be written.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBezierPath.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBezierPath.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBezierPath.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBezierPath.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSBezierPath.h
         Application Kit
-        Copyright (c) 1997-2015, Apple Inc.
+        Copyright (c) 1997-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBitmapImageRep.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBitmapImageRep.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBitmapImageRep.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBitmapImageRep.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSBitmapImageRep.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -28,12 +28,12 @@
 };
 
 typedef NS_ENUM(NSUInteger, NSBitmapImageFileType) {
-    NSTIFFFileType,
-    NSBMPFileType,
-    NSGIFFileType,
-    NSJPEGFileType,
-    NSPNGFileType,
-    NSJPEG2000FileType
+    NSBitmapImageFileTypeTIFF,
+    NSBitmapImageFileTypeBMP,
+    NSBitmapImageFileTypeGIF,
+    NSBitmapImageFileTypeJPEG,
+    NSBitmapImageFileTypePNG,
+    NSBitmapImageFileTypeJPEG2000
 };
 
 typedef NS_ENUM(NSInteger, NSImageRepLoadStatus) {
@@ -46,14 +46,14 @@
 };
 
 typedef NS_OPTIONS(NSUInteger, NSBitmapFormat) {
-    NSAlphaFirstBitmapFormat            = 1 << 0,       // 0 means is alpha last (RGBA, CMYKA, etc.)
-    NSAlphaNonpremultipliedBitmapFormat = 1 << 1,       // 0 means is premultiplied
-    NSFloatingPointSamplesBitmapFormat  = 1 << 2,	// 0 is integer
-    
-    NS16BitLittleEndianBitmapFormat NS_ENUM_AVAILABLE_MAC(10_10) = (1 << 8),
-    NS32BitLittleEndianBitmapFormat NS_ENUM_AVAILABLE_MAC(10_10) = (1 << 9),
-    NS16BitBigEndianBitmapFormat NS_ENUM_AVAILABLE_MAC(10_10) = (1 << 10),
-    NS32BitBigEndianBitmapFormat NS_ENUM_AVAILABLE_MAC(10_10) = (1 << 11)
+    NSBitmapFormatAlphaFirst            = 1 << 0,       // 0 means is alpha last (RGBA, CMYKA, etc.)
+    NSBitmapFormatAlphaNonpremultiplied = 1 << 1,       // 0 means is premultiplied
+    NSBitmapFormatFloatingPointSamples  = 1 << 2,  // 0 is integer
+
+    NSBitmapFormatSixteenBitLittleEndian NS_ENUM_AVAILABLE_MAC(10_10) = (1 << 8),
+    NSBitmapFormatThirtyTwoBitLittleEndian NS_ENUM_AVAILABLE_MAC(10_10) = (1 << 9),
+    NSBitmapFormatSixteenBitBigEndian NS_ENUM_AVAILABLE_MAC(10_10) = (1 << 10),
+    NSBitmapFormatThirtyTwoBitBigEndian NS_ENUM_AVAILABLE_MAC(10_10) = (1 << 11)
 };
 
 APPKIT_EXTERN NSString *NSImageCompressionMethod;	// TIFF input/output (NSTIFFCompression in NSNumber)
@@ -167,4 +167,21 @@
 
 @end
 
+
+static const NSBitmapImageFileType NSTIFFFileType /*API_DEPRECATED_WITH_REPLACEMENT("NSBitmapImageFileTypeTIFF", macosx(10.0, 10.12))*/ = NSBitmapImageFileTypeTIFF;
+static const NSBitmapImageFileType NSBMPFileType /*API_DEPRECATED_WITH_REPLACEMENT("NSBitmapImageFileTypeBMP", macosx(10.0, 10.12))*/ = NSBitmapImageFileTypeBMP;
+static const NSBitmapImageFileType NSGIFFileType /*API_DEPRECATED_WITH_REPLACEMENT("NSBitmapImageFileTypeGIF", macosx(10.0, 10.12))*/ = NSBitmapImageFileTypeGIF;
+static const NSBitmapImageFileType NSJPEGFileType /*API_DEPRECATED_WITH_REPLACEMENT("NSBitmapImageFileTypeJPEG", macosx(10.0, 10.12))*/ = NSBitmapImageFileTypeJPEG;
+static const NSBitmapImageFileType NSPNGFileType /*API_DEPRECATED_WITH_REPLACEMENT("NSBitmapImageFileTypePNG", macosx(10.0, 10.12))*/ = NSBitmapImageFileTypePNG;
+static const NSBitmapImageFileType NSJPEG2000FileType /*API_DEPRECATED_WITH_REPLACEMENT("NSBitmapImageFileTypeJPEG2000", macosx(10.0, 10.12))*/ = NSBitmapImageFileTypeJPEG2000;
+
+static const NSBitmapFormat NSAlphaFirstBitmapFormat /*API_DEPRECATED_WITH_REPLACEMENT("NSBitmapFormatAlphaFirst", macosx(10.5, 10.12))*/ = NSBitmapFormatAlphaFirst;
+static const NSBitmapFormat NSAlphaNonpremultipliedBitmapFormat /*API_DEPRECATED_WITH_REPLACEMENT("NSBitmapFormatAlphaNonpremultiplied", macosx(10.0, 10.12))*/ = NSBitmapFormatAlphaNonpremultiplied;
+static const NSBitmapFormat NSFloatingPointSamplesBitmapFormat /*API_DEPRECATED_WITH_REPLACEMENT("NSBitmapFormatFloatingPointSamples", macosx(10.0, 10.12))*/ = NSBitmapFormatFloatingPointSamples;
+static const NSBitmapFormat NS16BitLittleEndianBitmapFormat /*API_DEPRECATED_WITH_REPLACEMENT("NSBitmapFormatSixteenBitLittleEndian", macosx(10.5, 10.12))*/ = NSBitmapFormatSixteenBitLittleEndian;
+static const NSBitmapFormat NS32BitLittleEndianBitmapFormat /*API_DEPRECATED_WITH_REPLACEMENT("NSBitmapFormatThirtyTwoBitLittleEndian", macosx(10.0, 10.12))*/ = NSBitmapFormatThirtyTwoBitLittleEndian;
+static const NSBitmapFormat NS16BitBigEndianBitmapFormat /*API_DEPRECATED_WITH_REPLACEMENT("NSBitmapFormatSixteenBitBigEndian", macosx(10.0, 10.12))*/ = NSBitmapFormatSixteenBitBigEndian;
+static const NSBitmapFormat NS32BitBigEndianBitmapFormat /*API_DEPRECATED_WITH_REPLACEMENT("NSBitmapFormatThirtyTwoBitBigEndian", macosx(10.0, 10.12))*/ = NSBitmapFormatThirtyTwoBitBigEndian;
+
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBox.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBox.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBox.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBox.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSBox.h
     Application Kit
-    Copyright (c) 1994-2015, Apple Inc.
+    Copyright (c) 1994-2016, Apple Inc.
     All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBrowser.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBrowser.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBrowser.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBrowser.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSBrowser.h
     Application Kit
-    Copyright (c) 1994-2015, Apple Inc.
+    Copyright (c) 1994-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -180,7 +180,7 @@
  */
 - (void)scrollRowToVisible:(NSInteger)row inColumn:(NSInteger)column NS_AVAILABLE_MAC(10_6);
 
-- (void)setTitle:(NSString *)aString ofColumn:(NSInteger)column;
+- (void)setTitle:(NSString *)string ofColumn:(NSInteger)column;
 - (nullable NSString *)titleOfColumn:(NSInteger)column;
 @property (copy) NSString *pathSeparator;
 - (BOOL)setPath:(NSString *)path;
@@ -250,7 +250,7 @@
 - (BOOL)sendAction;
 
 - (NSRect)titleFrameOfColumn:(NSInteger)column;
-- (void)drawTitleOfColumn:(NSInteger)column inRect:(NSRect)aRect;
+- (void)drawTitleOfColumn:(NSInteger)column inRect:(NSRect)rect;
 @property (readonly) CGFloat titleHeight;
 - (NSRect)frameOfColumn:(NSInteger)column;
 - (NSRect)frameOfInsideOfColumn:(NSInteger)column;
@@ -329,9 +329,9 @@
  */
 @property (strong) NSColor *backgroundColor NS_AVAILABLE_MAC(10_5);
 
-/* Begins editing the item at the specified path. theEvent may be nil if programatically editing. The cell's contents will be selected if select is YES. Overriding this method will not affect the editing behavior of the browser.
+/* Begins editing the item at the specified path. event may be nil if programatically editing. The cell's contents will be selected if select is YES. Overriding this method will not affect the editing behavior of the browser.
  */
-- (void)editItemAtIndexPath:(NSIndexPath *)indexPath withEvent:(NSEvent *)theEvent select:(BOOL)select NS_AVAILABLE_MAC(10_6);
+- (void)editItemAtIndexPath:(NSIndexPath *)indexPath withEvent:(nullable NSEvent *)event select:(BOOL)select NS_AVAILABLE_MAC(10_6);
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBrowserCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBrowserCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBrowserCell.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBrowserCell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSBrowserCell.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -13,6 +13,10 @@
 
 @interface NSBrowserCell : NSCell
 
+- (instancetype)initTextCell:(NSString *)string NS_DESIGNATED_INITIALIZER;
+- (instancetype)initImageCell:(nullable NSImage *)image NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
+
 + (nullable NSImage *)branchImage;
 + (nullable NSImage *)highlightedBranchImage;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButton.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButton.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButton.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButton.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSButton.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -20,14 +20,14 @@
 @property (nullable, strong) NSImage *image;
 @property (nullable, strong) NSImage *alternateImage;
 @property NSCellImagePosition imagePosition;
-- (void)setButtonType:(NSButtonType)aType;
+- (void)setButtonType:(NSButtonType)type;
 @property NSInteger state;
 @property (getter=isBordered) BOOL bordered;
 @property (getter=isTransparent) BOOL transparent;
 - (void)setPeriodicDelay:(float)delay interval:(float)interval;
 - (void)getPeriodicDelay:(float *)delay interval:(float *)interval;
 @property (copy) NSString *keyEquivalent;
-@property NSUInteger keyEquivalentModifierMask;
+@property NSEventModifierFlags keyEquivalentModifierMask;
 - (void)highlight:(BOOL)flag;
 - (BOOL)performKeyEquivalent:(NSEvent *)key;
 
@@ -36,6 +36,57 @@
 
 @end
 
+
+@interface NSButton(NSButtonConvenience)
+
+/*!
+ Creates a standard push button with a title and image.
+ @param title The localized title string that is displayed on the button.
+ @param image The image that is displayed alongside the title. In left-to-right localizations, the image is displayed to the left of the title. In right-to-left localizations, it is displayed to the right.
+ @param target The target object that receives action messages from the control.
+ @param action The action message sent by the control.
+ @return An initialized button object.
+ */
++ (instancetype)buttonWithTitle:(NSString *)title image:(NSImage *)image target:(nullable id)target action:(nullable SEL)action NS_AVAILABLE_MAC(10_12);
+
+/*!
+ Creates a standard push button with the provided title.
+ @param title The localized title string that is displayed on the button.
+ @param target The target object that receives action messages from the control.
+ @param action The action message sent by the control.
+ @return An initialized button object.
+ */
++ (instancetype)buttonWithTitle:(NSString *)title target:(nullable id)target action:(nullable SEL)action NS_AVAILABLE_MAC(10_12);
+
+/*!
+ Creates a standard push button with the provided image. Set the image's accessibilityDescription property to ensure accessibility for this control.
+ @param image The image to display in the body of the button.
+ @param target The target object that receives action messages from the control.
+ @param action The action message sent by the control.
+ @return An initialized button object.
+ */
++ (instancetype)buttonWithImage:(NSImage *)image target:(nullable id)target action:(nullable SEL)action NS_AVAILABLE_MAC(10_12);
+
+/*!
+ Creates a standard checkbox with the provided title.
+ @param title The localized title string that is displayed alongside the checkbox.
+ @param target The target object that receives action messages from the control.
+ @param action The action message sent by the control.
+ @return An initialized button object.
+ */
++ (instancetype)checkboxWithTitle:(NSString *)title target:(nullable id)target action:(nullable SEL)action NS_SWIFT_NAME(init(checkboxWithTitle:target:action:)) NS_AVAILABLE_MAC(10_12);
+
+/*!
+ Creates a standard radio button with the provided title.
+ @param title The localized title string that is displayed alongside the radio button.
+ @param target The target object that receives action messages from the control.
+ @param action The action message sent by the control.
+ @return An initialized button object.
+ */
++ (instancetype)radioButtonWithTitle:(NSString *)title target:(nullable id)target action:(nullable SEL)action NS_SWIFT_NAME(init(radioButtonWithTitle:target:action:)) NS_AVAILABLE_MAC(10_12);
+
+@end
+
 @interface NSButton(NSButtonAttributedStringMethods)
 @property (copy) NSAttributedString *attributedTitle;
 @property (copy) NSAttributedString *attributedAlternateTitle;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButtonCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButtonCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButtonCell.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButtonCell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSButtonCell.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -77,9 +77,11 @@
     unsigned int        useButtonImageSource:1;
     unsigned int        isDrawingFocus:1;
     unsigned int        allowTitleTightening:1;
-    unsigned int        __reserved:6;
+    unsigned int        imageHugsTitle:1;
+    unsigned int        __reserved:5;
 #else
-    unsigned int        __reserved:6;
+    unsigned int        __reserved:5;
+    unsigned int        imageHugsTitle:1;
     unsigned int        allowTitleTightening:1;
     unsigned int        isDrawingFocus:1;
     unsigned int        useButtonImageSource:1;
@@ -140,6 +142,9 @@
     id                  _alternateImageOrKeyEquivalentFont;
 }
 
+- (instancetype)initTextCell:(NSString *)string NS_DESIGNATED_INITIALIZER;
+- (instancetype)initImageCell:(nullable NSImage *)image NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
 
 @property (null_resettable, copy) NSString *title;
 @property (copy) NSString *alternateTitle;
@@ -150,13 +155,13 @@
 
 @property NSCellStyleMask highlightsBy;
 @property NSCellStyleMask showsStateBy;
-- (void)setButtonType:(NSButtonType)aType;
+- (void)setButtonType:(NSButtonType)type;
 @property (getter=isOpaque, readonly) BOOL opaque;
 @property (getter=isTransparent) BOOL transparent;
 - (void)setPeriodicDelay:(float)delay interval:(float)interval;
 - (void)getPeriodicDelay:(float *)delay interval:(float *)interval;
 @property (copy) NSString *keyEquivalent;
-@property NSUInteger keyEquivalentModifierMask;
+@property NSEventModifierFlags keyEquivalentModifierMask;
 @property (nullable, strong) NSFont *keyEquivalentFont;
 - (void)setKeyEquivalentFont:(NSString *)fontName size:(CGFloat)fontSize;
 - (void)performClick:(nullable id)sender; // Significant NSCell override, actually clicks itself.
@@ -167,25 +172,17 @@
 
 @end
 
-// NSGradientType :
-//
-// A concave gradient is darkest in the top left corner, 
-// a convex gradient is darkest in the bottom right corner.
-//
-// Weak versus strong is how much contrast exists between
-// the colors used in opposite corners
 typedef NS_ENUM(NSUInteger, NSGradientType) {
     NSGradientNone          = 0,
     NSGradientConcaveWeak   = 1,
     NSGradientConcaveStrong = 2,
     NSGradientConvexWeak    = 3,
     NSGradientConvexStrong  = 4
-};
+} NS_DEPRECATED_MAC(10_0, 10_12);
 
 @interface NSButtonCell(NSButtonCellExtensions)
 
-// NOTE: gradientType is not used
-@property NSGradientType gradientType;
+@property NSGradientType gradientType NS_DEPRECATED_MAC(10_0, 10_12, "The gradientType property is unused, and setting it has no effect.");
 
 // When disabled, the image and text of an NSButtonCell are normally dimmed with gray.
 // Radio buttons and switches use (imageDimsWhenDisabled == NO) so only their text is dimmed.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCIImageRep.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCIImageRep.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCIImageRep.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCIImageRep.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSCIImageRep.h
         Application Kit
-        Copyright (c) 2003-2015, Apple Inc.
+        Copyright (c) 2003-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCachedImageRep.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCachedImageRep.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCachedImageRep.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCachedImageRep.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSCachedImageRep.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -16,7 +16,7 @@
     /*All instance variables are private*/
     NSPoint _origin;
     NSWindow *_window;
-    __strong void *_cache;
+    void *_cache;
 }
 
 /* References the specified rect within the window; the window is retained */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCell.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSCell.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -95,10 +95,13 @@
 
 
 typedef NS_ENUM(NSUInteger, NSControlSize) {
-    NSRegularControlSize,
-    NSSmallControlSize, 
-    NSMiniControlSize
+    NSControlSizeRegular,
+    NSControlSizeSmall,
+    NSControlSizeMini,
 };
+static const NSControlSize NSRegularControlSize API_DEPRECATED_WITH_REPLACEMENT("NSControlSizeRegular", macosx(10.0, 10.12)) = NSControlSizeRegular;
+static const NSControlSize NSSmallControlSize API_DEPRECATED_WITH_REPLACEMENT("NSControlSizeSmall", macosx(10.0, 10.12)) = NSControlSizeSmall;
+static const NSControlSize NSMiniControlSize API_DEPRECATED_WITH_REPLACEMENT("NSControlSizeMini", macosx(10.0, 10.12)) = NSControlSizeMini;
 
 typedef struct __CFlags {
     unsigned int        state:1;
@@ -169,8 +172,10 @@
 + (BOOL)prefersTrackingUntilMouseUp;
 
 
-- (instancetype)initTextCell:(NSString *)aString;
-- (instancetype)initImageCell:(nullable NSImage *)image;
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
+- (instancetype)initTextCell:(NSString *)string NS_DESIGNATED_INITIALIZER;
+- (instancetype)initImageCell:(nullable NSImage *)image NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
 
 @property (nullable, assign) NSView *controlView; // Must be an NSControl subclass, non-control view subclasses not allowed!
 @property NSCellType type;
@@ -181,7 +186,13 @@
 @property (copy) NSString *title;
 @property (getter=isOpaque, readonly) BOOL opaque;
 @property (getter=isEnabled) BOOL enabled;
+
+#if __LP64__
+- (NSInteger)sendActionOn:(NSEventMask)mask;
+#else
 - (NSInteger)sendActionOn:(NSInteger)mask;
+#endif
+
 @property (getter=isContinuous) BOOL continuous;
 @property (getter=isEditable) BOOL editable;
 @property (getter=isSelectable) BOOL selectable;
@@ -210,15 +221,15 @@
 @property NSControlTint controlTint;
 @property NSControlSize controlSize;
 @property (nullable, strong) id representedObject;
-- (NSInteger)cellAttribute:(NSCellAttribute)aParameter;
-- (void)setCellAttribute:(NSCellAttribute)aParameter to:(NSInteger)value;
-- (NSRect)imageRectForBounds:(NSRect)theRect;
-- (NSRect)titleRectForBounds:(NSRect)theRect;
-- (NSRect)drawingRectForBounds:(NSRect)theRect;
+- (NSInteger)cellAttribute:(NSCellAttribute)parameter;
+- (void)setCellAttribute:(NSCellAttribute)parameter to:(NSInteger)value;
+- (NSRect)imageRectForBounds:(NSRect)rect;
+- (NSRect)titleRectForBounds:(NSRect)rect;
+- (NSRect)drawingRectForBounds:(NSRect)rect;
 @property (readonly) NSSize cellSize;
-- (NSSize)cellSizeForBounds:(NSRect)aRect;
+- (NSSize)cellSizeForBounds:(NSRect)rect;
 - (NSColor *)highlightColorWithFrame:(NSRect)cellFrame inView:(NSView *)controlView;
-- (void)calcDrawInfo:(NSRect)aRect;
+- (void)calcDrawInfo:(NSRect)rect;
 - (NSText *)setUpFieldEditorAttributes:(NSText *)textObj;
 - (void)drawInteriorWithFrame:(NSRect)cellFrame inView:(NSView *)controlView;
 - (void)drawWithFrame:(NSRect)cellFrame inView:(NSView *)controlView;
@@ -228,9 +239,9 @@
 - (BOOL)startTrackingAt:(NSPoint)startPoint inView:(NSView *)controlView;
 - (BOOL)continueTracking:(NSPoint)lastPoint at:(NSPoint)currentPoint inView:(NSView *)controlView;
 - (void)stopTracking:(NSPoint)lastPoint at:(NSPoint)stopPoint inView:(NSView *)controlView mouseIsUp:(BOOL)flag;
-- (BOOL)trackMouse:(NSEvent *)theEvent inRect:(NSRect)cellFrame ofView:(NSView *)controlView untilMouseUp:(BOOL)flag;
-- (void)editWithFrame:(NSRect)aRect inView:(NSView *)controlView editor:(NSText *)textObj delegate:(nullable id)anObject event:(NSEvent *)theEvent;
-- (void)selectWithFrame:(NSRect)aRect inView:(NSView *)controlView editor:(NSText *)textObj delegate:(nullable id)anObject start:(NSInteger)selStart length:(NSInteger)selLength;
+- (BOOL)trackMouse:(NSEvent *)event inRect:(NSRect)cellFrame ofView:(NSView *)controlView untilMouseUp:(BOOL)flag;
+- (void)editWithFrame:(NSRect)rect inView:(NSView *)controlView editor:(NSText *)textObj delegate:(nullable id)delegate event:(nullable NSEvent *)event;
+- (void)selectWithFrame:(NSRect)rect inView:(NSView *)controlView editor:(NSText *)textObj delegate:(nullable id)delegate start:(NSInteger)selStart length:(NSInteger)selLength;
 - (void)endEditing:(NSText *)textObj;
 - (void)resetCursorRect:(NSRect)cellFrame inView:(NSView *)controlView;
 
@@ -257,9 +268,9 @@
 */
 @property NSUserInterfaceLayoutDirection userInterfaceLayoutDirection NS_AVAILABLE_MAC(10_6);
 
-/* Returns a custom field editor for editing inside aControlView. This is an override point for NSCell subclasses designed to work with its own custom field editor. This message is sent to the selected cell of aControlView in -[NSWindow fieldEditor:forObject:]. Returning non-nil from this method indicates skipping the standard field editor querying processes including -windowWillReturnFieldEditor:toObject: delegation. The default NSCell implementation returns nil. The field editor returned from this method should have isFieldEditor == YES.
+/* Returns a custom field editor for editing inside controlView. This is an override point for NSCell subclasses designed to work with its own custom field editor. This message is sent to the selected cell of controlView in -[NSWindow fieldEditor:forObject:]. Returning non-nil from this method indicates skipping the standard field editor querying processes including -windowWillReturnFieldEditor:toObject: delegation. The default NSCell implementation returns nil. The field editor returned from this method should have isFieldEditor == YES.
  */
-- (nullable NSTextView *)fieldEditorForView:(NSView *)aControlView NS_AVAILABLE_MAC(10_6);
+- (nullable NSTextView *)fieldEditorForView:(NSView *)controlView NS_AVAILABLE_MAC(10_6);
 
 /* Tells the text cell to layout/render its content in single-line. If YES, the cell ignores the return value from -wraps, interprets NSLineBreakByWordWrapping and NSLineBreakByCharWrapping from -lineBreakMode as NSLineBreakByClipping, and configures the field editor to ignore key binding commands that insert paragraph/line separators. Also, the field editor bound to a single line cell filters paragraph/line separator insertion from user actions. Cells in the single line mode use the fixed baseline layout. The text baseline position is determined solely by the control size regardless of content font style/size.
  */
@@ -373,8 +384,8 @@
 
 // Use formatters instead.  See -[NSCell formatter] and -[NSCell setFormatter:].
 - (NSInteger)entryType NS_DEPRECATED_MAC(10_0, 10_0);
-- (void)setEntryType:(NSInteger)aType NS_DEPRECATED_MAC(10_0, 10_0);
-- (BOOL)isEntryAcceptable:(NSString *)aString NS_DEPRECATED_MAC(10_0, 10_0);
+- (void)setEntryType:(NSInteger)type NS_DEPRECATED_MAC(10_0, 10_0);
+- (BOOL)isEntryAcceptable:(NSString *)string NS_DEPRECATED_MAC(10_0, 10_0);
 - (void)setFloatingPointFormat:(BOOL)autoRange left:(NSUInteger)leftDigits right:(NSUInteger)rightDigits NS_DEPRECATED_MAC(10_0, 10_0);
 
 /* In 10.8 and higher, all the *Mnemonic* methods are deprecated. On MacOS they have typically not been used.
@@ -397,7 +408,7 @@
  
  This method is appropriate for the bezel of a control, like a box, that can be resized in both dimensions.
  */
-APPKIT_EXTERN void NSDrawNinePartImage(NSRect frame, NSImage * topLeftCorner, NSImage * topEdgeFill, NSImage * topRightCorner, NSImage * leftEdgeFill, NSImage * centerFill, NSImage * rightEdgeFill, NSImage * bottomLeftCorner, NSImage * bottomEdgeFill, NSImage * bottomRightCorner, NSCompositingOperation op, CGFloat alphaFraction, BOOL flipped) NS_AVAILABLE_MAC(10_5);
+APPKIT_EXTERN void NSDrawNinePartImage(NSRect frame, NSImage * __nullable topLeftCorner, NSImage * __nullable topEdgeFill, NSImage * __nullable topRightCorner, NSImage * __nullable leftEdgeFill, NSImage * __nullable centerFill, NSImage * __nullable rightEdgeFill, NSImage * __nullable bottomLeftCorner, NSImage * __nullable bottomEdgeFill, NSImage * __nullable bottomRightCorner, NSCompositingOperation op, CGFloat alphaFraction, BOOL flipped) NS_AVAILABLE_MAC(10_5);
 
 enum {
     NSAnyType				= 0,
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSClickGestureRecognizer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSClickGestureRecognizer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSClickGestureRecognizer.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSClickGestureRecognizer.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSClickGestureRecognizer.h
     Application Kit
-    Copyright (c) 2013-2015, Apple Inc.
+    Copyright (c) 2013-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -21,9 +21,7 @@
     NSInteger _activeButtonCount;
     NSInteger _currentClickCount;
     id _reserved0;
-#ifndef __OBJC2__
-    NSInteger _reserved1;
-#endif
+    id _reserved1;
 }
 
 /* bitfield of the button(s) required to recognize this click where bit 0 is the primary button, 1 is the secondary button, etc...
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSClipView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSClipView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSClipView.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSClipView.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSClipView.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -55,14 +55,14 @@
 
 @property (copy) NSColor *backgroundColor;
 @property BOOL drawsBackground;
-@property (nullable, assign) id /* NSView * */ documentView;
+@property (nullable, assign) __kindof NSView *documentView;
 @property (readonly) NSRect documentRect;
 @property (nullable, strong) NSCursor *documentCursor;
 @property (readonly) NSRect documentVisibleRect;
 - (void)viewFrameChanged:(NSNotification *)notification;
 - (void)viewBoundsChanged:(NSNotification *)notification;
 @property BOOL copiesOnScroll;
-- (BOOL)autoscroll:(NSEvent *)theEvent;
+- (BOOL)autoscroll:(NSEvent *)event;
 - (void)scrollToPoint:(NSPoint)newOrigin;
 
 /* This is used to constrain the bounds of the clip view under magnification and scrolling. This also comes with the deprecation of -constrainScrollPoint:. The logic of an existing -constrainScrollPoint: can be moved to -constrainBoundsRect: by adjusting the proposedBound's origin (as opposed to 'newOrigin').
@@ -88,8 +88,8 @@
 @end
 
 @interface NSView(NSClipViewSuperview)
-- (void)reflectScrolledClipView:(NSClipView *)aClipView;
-- (void)scrollClipView:(NSClipView *)aClipView toPoint:(NSPoint)aPoint;
+- (void)reflectScrolledClipView:(NSClipView *)clipView;
+- (void)scrollClipView:(NSClipView *)clipView toPoint:(NSPoint)point;
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionView.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionView.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSCollectionView.h
     Application Kit
-    Copyright (c) 2005-2015, Apple Inc.
+    Copyright (c) 2005-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -44,7 +44,7 @@
     NSCollectionViewScrollPositionNearestVerticalEdge  = 1 << 8, /* Nearer of Leading,Trailing */
 };
 
-@class NSCollectionView, NSCollectionViewLayout, NSCollectionViewLayoutAttributes, NSCollectionViewTransitionLayout, NSDraggingImageComponent, NSImageView, NSIndexSet, NSMutableIndexSet, NSNib, NSTextField;
+@class NSButton, NSCollectionView, NSCollectionViewLayout, NSCollectionViewLayoutAttributes, NSCollectionViewTransitionLayout, NSDraggingImageComponent, NSImageView, NSIndexSet, NSMutableIndexSet, NSNib, NSTextField;
 @protocol NSCollectionViewDataSource, NSCollectionViewDelegate;
 
 NS_ASSUME_NONNULL_BEGIN
@@ -73,6 +73,17 @@
 
 @end
 
+/* Section header views can conform to this protocol, to enable a CollectionView to find the section collapse toggle button (when present).
+*/
+@protocol NSCollectionViewSectionHeaderView <NSCollectionViewElement>
+@optional
+
+/* If your header contains a button that's set up to toggle section collapse, wire this outlet to it.  This enables CollectionView to automatically show and hide the button, based on whether the section's items all fit.
+*/
+@property (nullable, assign) IBOutlet NSButton *sectionCollapseButton NS_AVAILABLE_MAC(10_12);
+
+@end
+
 /* An NSCollectionViewItem associates a visual representation (view subtree) with a representedObject of arbitrary type.  It also tracks whether the representedObject is part of the enclosing NSCollectionView's current selection.  Note that NSCollectionViewItem inherits some useful properties -- in particular, "representedObject" and "view" -- from NSViewController.
 */
 
@@ -90,10 +101,11 @@
         unsigned int stayHiddenAfterReuse:1;
         unsigned int updateAnimationCount:16;
         unsigned int dragging:1;
-        unsigned int reserved:7;
+        unsigned int isTransientAccessibilityElement:1;
+        unsigned int reserved:6;
     } _cviFlags;
     NSData *_cachedArchive;
-    id _reserved2;
+    id _reserved2 __unused;
 }
 
 /* Non-retained backlink to the containing CollectionView.
@@ -156,7 +168,10 @@
         unsigned int scheduledResize:1;
         unsigned int isOpaque:1;
         unsigned int observingClipFrameChanges:1;
-        unsigned int reserved:15;
+        unsigned int allowsSectionDrop:1;
+        unsigned int backgroundViewScrollsWithContent:1;
+        unsigned int visMode:1;
+        unsigned int reserved:12;
     } _cvFlags;
     id _delegate;
     NSMutableArray *_backgroundLayers;
@@ -213,7 +228,13 @@
 
 #pragma mark *** Decoration ***
 
-@property (nullable, strong) NSView *backgroundView NS_AVAILABLE_MAC(10_11); // will be automatically resized to track the size of the collection view and placed behind all items and supplementary views.
+/* An optional background view that's positioned underneath all of the CollectionView's content.  Defaults to nil.  The backgroundView's scrolling behavior and frame are determined by the "backgroundViewScrollsWithContent" property, as described below.  If "backgroundColors" are also specified for the CollectionView, backgroundColor[0] is drawn anywhere the backgroundView's content allows it to show through.
+*/
+@property (nullable, strong) NSView *backgroundView NS_AVAILABLE_MAC(10_11);
+
+/* When YES, the CollectionView's backgroundView (if any) will match the CollectionView's frame and scroll with the CollectionView's items and other content.  When NO (the default, compatible with the behavior on OS X 10.11), the backgroundView is made to fill the CollectionView's visible area, and remains stationary when the CollectionView's content is scrolled.  Archived with the CollectionView's other persistent properties.
+*/
+@property BOOL backgroundViewScrollsWithContent NS_AVAILABLE_MAC(10_12);
 
 
 #pragma mark *** Layout ***
@@ -222,7 +243,7 @@
 
 To get an animated transition to the new layout, use [[collectionView animator] setCollectionViewLayout:].  You can use NSAnimationContext's completionHandler provisions to notify you when the transition is complete.
 */
-@property (nullable, strong) NSCollectionViewLayout *collectionViewLayout NS_AVAILABLE_MAC(10_11);
+@property (nullable, strong) __kindof NSCollectionViewLayout *collectionViewLayout NS_AVAILABLE_MAC(10_11);
 
 /* Returns the layout information for the item at the specified index path (or nil if no such item exists).  Use this method to retrieve the layout information for a particular item.  You should always use this method instead of querying the layout object directly.
 */
@@ -349,7 +370,7 @@
 */
 - (nullable NSCollectionViewItem *)itemAtIndex:(NSUInteger)index NS_AVAILABLE_MAC(10_6);
 
-/* Returns the NSCollectionViewItem associated with the represented object at the given indexPath.
+/* Returns the NSCollectionViewItem (if any) associated with the represented object at the given indexPath.  This method returns nil if the CollectionView isn't currently maintaining an NSCollectionViewItem instance for the given indexPath, as may be the case if the specified item is outside the CollectionView's visibleRect.
 */
 - (nullable NSCollectionViewItem *)itemAtIndexPath:(NSIndexPath *)indexPath NS_AVAILABLE_MAC(10_11);
 
@@ -460,7 +481,14 @@
 
 Invocations of this method can be nested.
 */
-- (void)performBatchUpdates:(void (^__nullable)(void))updates completionHandler:(void (^__nullable)(BOOL finished))completionHandler NS_AVAILABLE_MAC(10_11);
+- (void)performBatchUpdates:(void (NS_NOESCAPE ^__nullable)(void))updates completionHandler:(void (^__nullable)(BOOL finished))completionHandler NS_AVAILABLE_MAC(10_11);
+
+
+#pragma mark *** Section Collapse ***
+
+/* Toggles collapse of the CollectionView section that the sender resides in.  Typically you'll wire this action from a section header view's "sectionCollapse" button.  (See the NSCollectionViewSectionHeaderView protocol.)
+ */
+- (IBAction)toggleSectionCollapse:(id)sender NS_AVAILABLE_MAC(10_12);
 
 
 #pragma mark *** Scrolling ***
@@ -682,7 +710,7 @@
 
 /* Executes the given block for each NSIndexPath in the set.  The index paths are enumerated in the order defined by NSIndexPath's -compare: method.  For CollectionView item index paths, this means all index paths in section 0, in ascending order, followed by all index paths in section 1, and so on.  You may pass the NSEnumerationReverse option to enumerate in the reverse order.  Set *stop = YES if desired, to halt the enumeration early.
  */
-- (void)enumerateIndexPathsWithOptions:(NSEnumerationOptions)opts usingBlock:(void (^)(NSIndexPath *indexPath, BOOL *stop))block NS_AVAILABLE_MAC(10_11);
+- (void)enumerateIndexPathsWithOptions:(NSEnumerationOptions)opts usingBlock:(void (NS_NOESCAPE ^)(NSIndexPath *indexPath, BOOL *stop))block NS_AVAILABLE_MAC(10_11);
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionViewFlowLayout.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionViewFlowLayout.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionViewFlowLayout.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionViewFlowLayout.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSCollectionViewFlowLayout.h
     Application Kit
-    Copyright (c) 2015, Apple Inc.
+    Copyright (c) 2015-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -63,6 +63,10 @@
         unsigned int layoutDataIsValid:1;
         unsigned int delegateInfoIsValid:1;
         unsigned int roundsToScreenScale:1;
+        unsigned int sectionHeadersFloat:1;
+        unsigned int sectionFootersFloat:1;
+        unsigned int isSingleColumnOrRow:1;
+        unsigned int collapsesSectionsToFirstItem:1;
     } _gridLayoutFlags;
     
     CGFloat _interitemSpacing;
@@ -103,6 +107,26 @@
 @property NSSize footerReferenceSize;
 @property NSEdgeInsets sectionInset;
 
+/* Set these properties to YES to get headers that pin to the top of the visible area and footers that pin to the bottom while scrolling.  Archived with the layout's other persistent properties.  Enabling this feature may affect the parenting of header and footer views.
+*/
+@property BOOL sectionHeadersPinToVisibleBounds NS_AVAILABLE_MAC(10_12);
+@property BOOL sectionFootersPinToVisibleBounds NS_AVAILABLE_MAC(10_12);
+
+
+#pragma mark *** Section Collapse ***
+
+/* Returns YES if the specified section is currently collapsed; NO if not, or if there is no such section.  Defaults to NO.
+*/
+- (BOOL)sectionAtIndexIsCollapsed:(NSUInteger)sectionIndex NS_AVAILABLE_MAC(10_12);
+
+/* Collapses the specified section to a single row, if it is not already collapsed.
+*/
+- (void)collapseSectionAtIndex:(NSUInteger)sectionIndex NS_AVAILABLE_MAC(10_12);
+
+/* Un-collapses the specified section, if it is currently collapsed.
+*/
+- (void)expandSectionAtIndex:(NSUInteger)sectionIndex NS_AVAILABLE_MAC(10_12);
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionViewGridLayout.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionViewGridLayout.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionViewGridLayout.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionViewGridLayout.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSCollectionViewGridLayout.h
     Application Kit
-    Copyright (c) 2015, Apple Inc.
+    Copyright (c) 2015-2016, Apple Inc.
     All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionViewLayout.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionViewLayout.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionViewLayout.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionViewLayout.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSCollectionViewLayout.h
     Application Kit
-    Copyright (c) 2015, Apple Inc.
+    Copyright (c) 2015-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -24,7 +24,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-/* The elementKind used to identify an inter-item gap (for use in indicating a drop target).  A client can customize the default look of the inter-item gap drop target indicator by registering a supplementary view nib or class for this elementKind.
+/* The elementKind that NSCollectionView uses to identify an inter-item gap, when the proposedDropOperation is NSCollectionViewDropBefore.  A client can customize the default look of the inter-item gap drop target indicator by registering a supplementary view nib or class for this elementKind.  If your -collectionView:validateDrop:proposedIndexPath:dropOperation: method disallows NSCollectionViewDropBefore operations, the CollectionView won't show this indicator.
 */
 APPKIT_EXTERN NSString *const NSCollectionElementKindInterItemGapIndicator NS_AVAILABLE_MAC(10_11);
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionViewTransitionLayout.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionViewTransitionLayout.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionViewTransitionLayout.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionViewTransitionLayout.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSCollectionViewTransitionLayout.h
     Application Kit
-    Copyright (c) 2015, Apple Inc.
+    Copyright (c) 2015-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -34,7 +34,7 @@
     
     CGFloat _accuracy;
 }
-#endif // TARGET_OS_IPHONE || __OBJC2__
+#endif
 
 @property (assign) CGFloat transitionProgress;
 @property (readonly) NSCollectionViewLayout *currentLayout;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColor.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColor.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColor.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColor.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,13 +1,13 @@
 /*
 	NSColor.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
 /* NSColors store colors. Often the only NSColor message you send is the "set" method, which makes the receiver the current color in the drawing context. There is usually no need to dive in and get the individual components (for instance, red, green, blue) that make up a color.
 
-An NSColor may be in one of several fixed number of named colorspaces. Different named colorspaces have different ways of getting at the components which define colors in that colorspace. Implementations of NSColors exist for the following named colorspaces:
+An NSColor may be in one of several fixed number of "named" color spaces. Different named color spaces have different ways of getting at the components which define colors in that color space:
 
   NSDeviceCMYKColorSpace	Cyan, magenta, yellow, black, and alpha components
   NSDeviceWhiteColorSpace	White and alpha components
@@ -19,11 +19,11 @@
   NSNamedColorSpace		Catalog name, color name components
   NSCustomColorSpace		Color space specified using NSColorSpace, with appropriate number of CGFloat components
 
-The named colorspace NSCustomColorSpace allows flexibility of defining an arbitrary colorspace using an NSColorSpace. 
-
+The named color space NSCustomColorSpace allows flexibility of using an arbitrary color space (specified via an NSColorSpace), and is the way to get colors in sRGB or P3 colorspaces.  These color spaces are preferred over the historical "calibrated" color spaces. Create NSCustomColorSpace colors with +colorSpaceWithColorSpace:components:count:, or the likes of colorWithSRGBRed:green:blue:alpha:.
+ 
 Alpha component defines opacity on devices which support it (1.0 == full opacity). On other devices the alpha is ignored when the color is used.
 
-It's illegal to ask a color for components that are not defined for its colorspace. If you need to ask a color for a certain set of components (for instance, you need to know the RGB components of a color you got from the color panel), you should first convert the color to the appropriate colorspace using colorUsingColorSpace:, or the appropriate named colorspace using  colorUsingColorSpaceName:.  If the color is already in the specified colorspace, you get the same color back; otherwise you get a conversion which is usually lossy or is correct only for the current device. You might also get back nil if the specified conversion cannot be done.
+It's illegal to ask a color for components that are not defined for its colorspace. If you need to ask a color for a certain set of components (for instance, you need to know the RGB components of a color you got from the color panel), you should first convert the color to the appropriate colorspace using colorUsingColorSpace:, or the appropriate named colorspace using  colorUsingColorSpaceName:.  If the color is already in the specified colorspace, you get the same color back; otherwise a conversion occurs. You might also get back nil if the specified conversion cannot be done.
 
 Subclassers of NSColor need to implement the methods colorSpaceName, set, the various methods which return the components for that color space, and the NSCoding protocol. Some other methods such as colorWithAlphaComponent:, isEqual:, colorUsingColorSpaceName:device:, and CGColor may also be implemented if they make sense for the colorspace. If isEqual: is overridden, so should hash (because if [a isEqual:b] then [a hash] == [b hash]). Mutable subclassers (if any) should also implement copyWithZone: to a true copy.
 */
@@ -50,46 +50,51 @@
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
 - (nullable instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
 
-/* Create NSCalibratedWhiteColorSpace colors.
+
+/* Create colors with arbitrary colorspace. The colorspace should be component-based, and the number of components in the provided array should match the number dictated by the specified colorspace, plus one for alpha (supply 1.0 for opaque colors); otherwise an exception will be raised.
 */
-+ (NSColor *)colorWithCalibratedWhite:(CGFloat)white alpha:(CGFloat)alpha;
++ (NSColor *)colorWithColorSpace:(NSColorSpace *)space components:(const CGFloat *)components count:(NSInteger)numberOfComponents;
 
 
-/* Create NSCalibratedRGBColorSpace colors.
+/* Create NSCustomColorSpace colors in the sRGB, GenericGamma22Gray, or P3 colorspaces.
 */
-+ (NSColor *)colorWithCalibratedHue:(CGFloat)hue saturation:(CGFloat)saturation brightness:(CGFloat)brightness alpha:(CGFloat)alpha;
-+ (NSColor *)colorWithCalibratedRed:(CGFloat)red green:(CGFloat)green blue:(CGFloat)blue alpha:(CGFloat)alpha;
++ (NSColor *)colorWithSRGBRed:(CGFloat)red green:(CGFloat)green blue:(CGFloat)blue alpha:(CGFloat)alpha  NS_AVAILABLE_MAC(10_7);
++ (NSColor *)colorWithGenericGamma22White:(CGFloat)white alpha:(CGFloat)alpha  NS_AVAILABLE_MAC(10_7);
++ (NSColor *)colorWithDisplayP3Red:(CGFloat)red green:(CGFloat)green blue:(CGFloat)blue alpha:(CGFloat)alpha NS_AVAILABLE_MAC(10_12);
 
 
-/* Create colors in various device color spaces. 
-*/
-+ (NSColor *)colorWithDeviceWhite:(CGFloat)white alpha:(CGFloat)alpha;
-+ (NSColor *)colorWithDeviceHue:(CGFloat)hue saturation:(CGFloat)saturation brightness:(CGFloat)brightness alpha:(CGFloat)alpha;
-+ (NSColor *)colorWithDeviceRed:(CGFloat)red green:(CGFloat)green blue:(CGFloat)blue alpha:(CGFloat)alpha;
-+ (NSColor *)colorWithDeviceCyan:(CGFloat)cyan magenta:(CGFloat)magenta yellow:(CGFloat)yellow black:(CGFloat)black alpha:(CGFloat)alpha;
+/* Create a RGB-based color using HSB component values. An exception will be raised if the color model of the provided color space is not RGB.
+ */
++ (NSColor *)colorWithColorSpace:(NSColorSpace *)space hue:(CGFloat)hue saturation:(CGFloat)saturation brightness:(CGFloat)brightness alpha:(CGFloat)alpha NS_AVAILABLE_MAC(10_12);
 
 
-/* Create named colors from standard color catalogs (such as Pantone).
+/* Create NSCustomColorSpace colors that are compatible with sRGB colorspace; these variants are provided for easier reuse of code that uses UIColor on iOS. It's typically better to specify the colorspace explicitly with one of the above methods.
+ 
+If red, green, blue, or saturation, brightness, or white values are outside of the 0..1 range, these will create colors in the extended sRGB (or for colorWithWhite:alpha:, extendedGenericGamma22GrayColorSpace) color spaces. This behavior is compatible with iOS UIColor.
 */
-+ (nullable NSColor *)colorWithCatalogName:(NSString *)listName colorName:(NSString *)colorName;
++ (NSColor *)colorWithWhite:(CGFloat)white alpha:(CGFloat)alpha NS_AVAILABLE_MAC(10_9);
++ (NSColor *)colorWithRed:(CGFloat)red green:(CGFloat)green blue:(CGFloat)blue alpha:(CGFloat)alpha NS_AVAILABLE_MAC(10_9);
++ (NSColor *)colorWithHue:(CGFloat)hue saturation:(CGFloat)saturation brightness:(CGFloat)brightness alpha:(CGFloat)alpha NS_AVAILABLE_MAC(10_9);
 
 
-/* Create colors with arbitrary colorspace. The number of components in the provided array should match the number dictated by the specified colorspace, plus one for alpha (supply 1.0 for opaque colors); otherwise an exception will be raised.  If the colorspace is one which cannot be used with NSColors, nil is returned.
-*/
-+ (NSColor *)colorWithColorSpace:(NSColorSpace *)space components:(const CGFloat *)components count:(NSInteger)numberOfComponents;
+/* Create NSCalibratedWhiteColorSpace or NSCalibratedRGBColorSpace colors.  In general colors in sRGB or P3 color spaces should be preferred.
+ */
++ (NSColor *)colorWithCalibratedWhite:(CGFloat)white alpha:(CGFloat)alpha;
++ (NSColor *)colorWithCalibratedRed:(CGFloat)red green:(CGFloat)green blue:(CGFloat)blue alpha:(CGFloat)alpha;
++ (NSColor *)colorWithCalibratedHue:(CGFloat)hue saturation:(CGFloat)saturation brightness:(CGFloat)brightness alpha:(CGFloat)alpha;
 
 
-/* Create NSCustomColorSpace colors in the sRGB or GenericGamma22Gray colorspaces.  
-*/
-+ (NSColor *)colorWithGenericGamma22White:(CGFloat)white alpha:(CGFloat)alpha  NS_AVAILABLE_MAC(10_7);
-+ (NSColor *)colorWithSRGBRed:(CGFloat)red green:(CGFloat)green blue:(CGFloat)blue alpha:(CGFloat)alpha  NS_AVAILABLE_MAC(10_7);
+/* Create colors in various device color spaces.
+ */
++ (NSColor *)colorWithDeviceWhite:(CGFloat)white alpha:(CGFloat)alpha;
++ (NSColor *)colorWithDeviceRed:(CGFloat)red green:(CGFloat)green blue:(CGFloat)blue alpha:(CGFloat)alpha;
++ (NSColor *)colorWithDeviceHue:(CGFloat)hue saturation:(CGFloat)saturation brightness:(CGFloat)brightness alpha:(CGFloat)alpha;
++ (NSColor *)colorWithDeviceCyan:(CGFloat)cyan magenta:(CGFloat)magenta yellow:(CGFloat)yellow black:(CGFloat)black alpha:(CGFloat)alpha;
 
 
-/* Create NSCustomColorSpace colors that are compatible with sRGB colorspace; these variants are provided for easier reuse of code that uses UIColor on iOS. It's typically better to specify the colorspace explicitly with one of the above methods.
-*/
-+ (NSColor *)colorWithWhite:(CGFloat)white alpha:(CGFloat)alpha NS_AVAILABLE_MAC(10_9);
-+ (NSColor *)colorWithRed:(CGFloat)red green:(CGFloat)green blue:(CGFloat)blue alpha:(CGFloat)alpha NS_AVAILABLE_MAC(10_9);
-+ (NSColor *)colorWithHue:(CGFloat)hue saturation:(CGFloat)saturation brightness:(CGFloat)brightness alpha:(CGFloat)alpha NS_AVAILABLE_MAC(10_9);
+/* Create named colors from standard color catalogs (such as Pantone).
+ */
++ (nullable NSColor *)colorWithCatalogName:(NSString *)listName colorName:(NSString *)colorName;
 
 
 /* Some convenience methods to create colors in the calibrated color spaces...
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorList.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorList.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorList.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorList.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSColorList.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorPanel.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorPanel.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorPanel.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorPanel.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSColorPanel.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -13,16 +13,16 @@
 @class NSColorList, NSMutableArray;
 
 typedef NS_ENUM(NSInteger, NSColorPanelMode) {
-    /* If the color panel is not displaying a mode, the NSNoModeColorPanel will be returned */
-    NSNoModeColorPanel NS_ENUM_AVAILABLE_MAC(10_5) = -1,
-    NSGrayModeColorPanel		= 0,
-    NSRGBModeColorPanel			= 1,
-    NSCMYKModeColorPanel		= 2,
-    NSHSBModeColorPanel			= 3,
-    NSCustomPaletteModeColorPanel	= 4,
-    NSColorListModeColorPanel		= 5,
-    NSWheelModeColorPanel		= 6,
-    NSCrayonModeColorPanel		= 7
+    /* If the color panel is not displaying a mode, the NSColorPanelModeNone will be returned */
+    NSColorPanelModeNone NS_ENUM_AVAILABLE_MAC(10_5) = -1,
+    NSColorPanelModeGray            = 0,
+    NSColorPanelModeRGB             = 1,
+    NSColorPanelModeCMYK            = 2,
+    NSColorPanelModeHSB             = 3,
+    NSColorPanelModeCustomPalette   = 4,
+    NSColorPanelModeColorList       = 5,
+    NSColorPanelModeWheel           = 6,
+    NSColorPanelModeCrayon          = 7
 };
 
 typedef NS_OPTIONS(NSUInteger, NSColorPanelOptions) {
@@ -80,7 +80,7 @@
 
 + (NSColorPanel *)sharedColorPanel;
 + (BOOL)sharedColorPanelExists;
-+ (BOOL)dragColor:(NSColor *)color withEvent:(NSEvent *)theEvent fromView:(NSView *)sourceView;
++ (BOOL)dragColor:(NSColor *)color withEvent:(NSEvent *)event fromView:(NSView *)sourceView;
 + (void)setPickerMask:(NSColorPanelOptions)mask;
 + (void)setPickerMode:(NSColorPanelMode)mode;
 
@@ -90,8 +90,8 @@
 @property NSColorPanelMode mode;
 @property (copy) NSColor *color;
 @property (readonly) CGFloat alpha;
-- (void)setAction:(nullable SEL)aSelector;
-- (void)setTarget:(nullable id)anObject;
+- (void)setAction:(nullable SEL)selector;
+- (void)setTarget:(nullable id)target;
 - (void)attachColorList:(NSColorList *)colorList;
 - (void)detachColorList:(NSColorList *)colorList;
 @end
@@ -107,5 +107,16 @@
 /* Notifications */
 APPKIT_EXTERN NSString * NSColorPanelColorDidChangeNotification;
 
+
+static const NSColorPanelMode NSNoModeColorPanel NS_AVAILABLE_MAC(10_5) /*API_DEPRECATED_WITH_REPLACEMENT("NSColorPanelModeNone", macosx(10.5, 10.12))*/ = NSColorPanelModeNone;
+static const NSColorPanelMode NSGrayModeColorPanel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorPanelModeGray", macosx(10.0, 10.12))*/ = NSColorPanelModeGray;
+static const NSColorPanelMode NSRGBModeColorPanel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorPanelModeRGB", macosx(10.0, 10.12))*/ = NSColorPanelModeRGB;
+static const NSColorPanelMode NSCMYKModeColorPanel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorPanelModeCMYK", macosx(10.0, 10.12))*/ = NSColorPanelModeCMYK;
+static const NSColorPanelMode NSHSBModeColorPanel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorPanelModeHSB", macosx(10.0, 10.12))*/ = NSColorPanelModeHSB;
+static const NSColorPanelMode NSCustomPaletteModeColorPanel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorPanelModeCustomPalette", macosx(10.0, 10.12))*/ = NSColorPanelModeCustomPalette;
+static const NSColorPanelMode NSColorListModeColorPanel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorPanelModeColorList", macosx(10.0, 10.12))*/ = NSColorPanelModeColorList;
+static const NSColorPanelMode NSWheelModeColorPanel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorPanelModeWheel", macosx(10.0, 10.12))*/ = NSColorPanelModeWheel;
+static const NSColorPanelMode NSCrayonModeColorPanel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorPanelModeCrayon", macosx(10.0, 10.12))*/ = NSColorPanelModeCrayon;
+
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorPicker.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorPicker.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorPicker.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorPicker.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSColorPicker.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorPicking.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorPicking.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorPicking.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorPicking.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSColorPicking.h
     Application Kit
-    Copyright (c) 1994-2015, Apple Inc.
+    Copyright (c) 1994-2016, Apple Inc.
     All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorSpace.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorSpace.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorSpace.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorSpace.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSColorSpace.h
 	Application Kit
-	Copyright (c) 2004-2015, Apple Inc.
+	Copyright (c) 2004-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -18,14 +18,14 @@
 
 
 typedef NS_ENUM(NSInteger, NSColorSpaceModel) {
-    NSUnknownColorSpaceModel = -1,
-    NSGrayColorSpaceModel,
-    NSRGBColorSpaceModel,
-    NSCMYKColorSpaceModel,
-    NSLABColorSpaceModel,
-    NSDeviceNColorSpaceModel,
-    NSIndexedColorSpaceModel,
-    NSPatternColorSpaceModel
+    NSColorSpaceModelUnknown = -1,
+    NSColorSpaceModelGray,
+    NSColorSpaceModelRGB,
+    NSColorSpaceModelCMYK,
+    NSColorSpaceModelLAB,
+    NSColorSpaceModelDeviceN,
+    NSColorSpaceModelIndexed,
+    NSColorSpaceModelPatterned
 };
 
 
@@ -62,7 +62,17 @@
 
 @property (readonly) NSInteger numberOfColorComponents;		// Does not include alpha
 @property (readonly) NSColorSpaceModel colorSpaceModel;
-@property (nullable, readonly, copy) NSString *localizedName;			// Will return nil if no localized name
+@property (nullable, readonly, copy) NSString *localizedName;	// Will return nil if no localized name
+
++ (NSColorSpace *)sRGBColorSpace  NS_AVAILABLE_MAC(10_5);
++ (NSColorSpace *)genericGamma22GrayColorSpace  NS_AVAILABLE_MAC(10_6);             // The grayscale color space with gamma 2.2, compatible with sRGB
+
++ (NSColorSpace *)extendedSRGBColorSpace  NS_AVAILABLE_MAC(10_12);                  // sRGB compatible color space that allows specifying components beyond the range of [0.0, 1.0]
++ (NSColorSpace *)extendedGenericGamma22GrayColorSpace  NS_AVAILABLE_MAC(10_12);    // sRGB compatible gray color space that allows specifying components beyond the range of [0.0, 1.0]
+
++ (NSColorSpace *)displayP3ColorSpace  NS_AVAILABLE_MAC(10_12);     // Standard DCI-P3 primaries, a D65 white point, and the same gamma curve as the sRGB IEC61966-2.1 color space
+
++ (NSColorSpace *)adobeRGB1998ColorSpace  NS_AVAILABLE_MAC(10_5);
 
 + (NSColorSpace *)genericRGBColorSpace;		// NSColorSpace corresponding to Cocoa color space name NSCalibratedRGBColorSpace
 + (NSColorSpace *)genericGrayColorSpace;	// NSColorSpace corresponding to Cocoa color space name NSCalibratedWhiteColorSpace
@@ -71,17 +81,22 @@
 + (NSColorSpace *)deviceGrayColorSpace;		// NSColorSpace corresponding to Cocoa color space name NSDeviceWhiteColorSpace
 + (NSColorSpace *)deviceCMYKColorSpace;		// NSColorSpace corresponding to Cocoa color space name NSDeviceCMYKColorSpace
 
-+ (NSColorSpace *)sRGBColorSpace  NS_AVAILABLE_MAC(10_5);
-+ (NSColorSpace *)genericGamma22GrayColorSpace  NS_AVAILABLE_MAC(10_6);  // The "generic" color space with gamma 2.2.
-
-+ (NSColorSpace *)adobeRGB1998ColorSpace  NS_AVAILABLE_MAC(10_5);
-
-/* Return the list of color spaces available on the system that are displayed by the color panel, in the order they are displayed in the color panel. Doesn't return arbitrary color spaces which may have been created on the fly, or spaces without user displayable names. Pass model==NSUnknownColorSpaceModel to get all color spaces. Empty array is returned if no color spaces are available for the specified model. 
+/* Return the list of color spaces available on the system that are displayed by the color panel, in the order they are displayed in the color panel. Doesn't return arbitrary color spaces which may have been created on the fly, or spaces without user displayable names. Pass model==NSUnknownColorSpaceModel to get all color spaces. Empty array is returned if no color spaces are available for the specified model.
 */
 + (NSArray<NSColorSpace *> *)availableColorSpacesWithModel:(NSColorSpaceModel)model  NS_AVAILABLE_MAC(10_6);
 
 @end
 
+
+static const NSColorSpaceModel NSUnknownColorSpaceModel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorSpaceModelUnknown", macosx(10.0, 10.12))*/ = NSColorSpaceModelUnknown;
+static const NSColorSpaceModel NSGrayColorSpaceModel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorSpaceModelGray", macosx(10.0, 10.12))*/ = NSColorSpaceModelGray;
+static const NSColorSpaceModel NSRGBColorSpaceModel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorSpaceModelRGB", macosx(10.0, 10.12))*/ = NSColorSpaceModelRGB;
+static const NSColorSpaceModel NSCMYKColorSpaceModel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorSpaceModelCMYK", macosx(10.0, 10.12))*/ = NSColorSpaceModelCMYK;
+static const NSColorSpaceModel NSLABColorSpaceModel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorSpaceModelLAB", macosx(10.0, 10.12))*/ = NSColorSpaceModelLAB;
+static const NSColorSpaceModel NSDeviceNColorSpaceModel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorSpaceModelDeviceN", macosx(10.0, 10.12))*/ = NSColorSpaceModelDeviceN;
+static const NSColorSpaceModel NSIndexedColorSpaceModel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorSpaceModelIndexed", macosx(10.0, 10.12))*/ = NSColorSpaceModelIndexed;
+static const NSColorSpaceModel NSPatternColorSpaceModel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorSpaceModelPatterned", macosx(10.0, 10.12))*/ = NSColorSpaceModelPatterned;
+
 NS_ASSUME_NONNULL_END
 
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorWell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorWell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorWell.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorWell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSColorWell.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSComboBox.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSComboBox.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSComboBox.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSComboBox.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSComboBox.h
 	Application Kit
-	Copyright (c) 1996-2015, Apple Inc.
+	Copyright (c) 1996-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -45,7 +45,7 @@
 @property BOOL completes;
 
 - (nullable id <NSComboBoxDelegate>)delegate;
-- (void)setDelegate:(nullable id <NSComboBoxDelegate>)anObject;
+- (void)setDelegate:(nullable id <NSComboBoxDelegate>)delegate;
 
 /* These two methods can only be used when usesDataSource is YES */
 @property (nullable, assign) id<NSComboBoxDataSource> dataSource;
@@ -68,11 +68,11 @@
 @protocol NSComboBoxDataSource <NSObject>
 @optional
 /* These two methods are required when not using bindings */
-- (NSInteger)numberOfItemsInComboBox:(NSComboBox *)aComboBox;
-- (id)comboBox:(NSComboBox *)aComboBox objectValueForItemAtIndex:(NSInteger)index;
+- (NSInteger)numberOfItemsInComboBox:(NSComboBox *)comboBox;
+- (nullable id)comboBox:(NSComboBox *)comboBox objectValueForItemAtIndex:(NSInteger)index;
 
-- (NSUInteger)comboBox:(NSComboBox *)aComboBox indexOfItemWithStringValue:(NSString *)string;
-- (nullable NSString *)comboBox:(NSComboBox *)aComboBox completedString:(NSString *)string;
+- (NSUInteger)comboBox:(NSComboBox *)comboBox indexOfItemWithStringValue:(NSString *)string;
+- (nullable NSString *)comboBox:(NSComboBox *)comboBox completedString:(NSString *)string;
 @end
 
 @protocol NSComboBoxDelegate <NSTextFieldDelegate>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSComboBoxCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSComboBoxCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSComboBoxCell.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSComboBoxCell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSComboBoxCell.h
 	Application Kit
-	Copyright (c) 1996-2015, Apple Inc.
+	Copyright (c) 1996-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -33,7 +33,7 @@
     NSScrollView *_scrollView;
     NSWindow *_popUp;
     NSMutableArray *_popUpList;
-    __strong NSRect *_cellFrame;
+    NSRect *_cellFrame;
     void *_reserved;
  }
 
@@ -82,10 +82,10 @@
 @optional
 /* These two methods are required when not using bindings */
 - (NSInteger)numberOfItemsInComboBoxCell:(NSComboBoxCell *)comboBoxCell;
-- (id)comboBoxCell:(NSComboBoxCell *)aComboBoxCell objectValueForItemAtIndex:(NSInteger)index;
+- (id)comboBoxCell:(NSComboBoxCell *)comboBoxCell objectValueForItemAtIndex:(NSInteger)index;
 
-- (NSUInteger)comboBoxCell:(NSComboBoxCell *)aComboBoxCell indexOfItemWithStringValue:(NSString *)string;
-- (nullable NSString *)comboBoxCell:(NSComboBoxCell *)aComboBoxCell completedString:(NSString *)uncompletedString; 
+- (NSUInteger)comboBoxCell:(NSComboBoxCell *)comboBoxCell indexOfItemWithStringValue:(NSString *)string;
+- (nullable NSString *)comboBoxCell:(NSComboBoxCell *)comboBoxCell completedString:(NSString *)uncompletedString; 
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSControl.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSControl.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSControl.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSControl.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSControl.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -58,9 +58,14 @@
 - (instancetype)initWithFrame:(NSRect)frameRect NS_DESIGNATED_INITIALIZER;
 - (nullable instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
 - (void)sizeToFit;
+
+#if __LP64__
+- (NSInteger)sendActionOn:(NSEventMask)mask;
+#else
 - (NSInteger)sendActionOn:(NSInteger)mask;
+#endif
 
-- (BOOL)sendAction:(SEL)theAction to:(nullable id)theTarget;
+- (BOOL)sendAction:(nullable SEL)action to:(nullable id)target;
 - (void)takeIntValueFrom:(nullable id)sender;
 - (void)takeFloatValueFrom:(nullable id)sender;
 - (void)takeDoubleValueFrom:(nullable id)sender;
@@ -68,7 +73,7 @@
 - (void)takeObjectValueFrom:(nullable id)sender;
 - (void)takeIntegerValueFrom:(nullable id)sender NS_AVAILABLE_MAC(10_5);
 
-- (void)mouseDown:(NSEvent *)theEvent;
+- (void)mouseDown:(NSEvent *)event;
 
 @end
 
@@ -111,8 +116,8 @@
 - (BOOL)abortEditing;
 - (void)validateEditing;
 
-- (void)editWithFrame:(NSRect)aRect editor:(NSText *)textObj delegate:(nullable id)anObject event:(NSEvent *)theEvent NS_AVAILABLE_MAC(10_10);
-- (void)selectWithFrame:(NSRect)aRect editor:(NSText *)textObj delegate:(nullable id)anObject start:(NSInteger)selStart length:(NSInteger)selLength NS_AVAILABLE_MAC(10_10);
+- (void)editWithFrame:(NSRect)rect editor:(NSText *)textObj delegate:(nullable id)delegate event:(NSEvent *)event NS_AVAILABLE_MAC(10_10);
+- (void)selectWithFrame:(NSRect)rect editor:(NSText *)textObj delegate:(nullable id)delegate start:(NSInteger)selStart length:(NSInteger)selLength NS_AVAILABLE_MAC(10_10);
 - (void)endEditing:(NSText *)textObj NS_AVAILABLE_MAC(10_10);
 @end
 
@@ -132,7 +137,7 @@
 - (BOOL)control:(NSControl *)control textShouldEndEditing:(NSText *)fieldEditor;
 - (BOOL)control:(NSControl *)control didFailToFormatString:(NSString *)string errorDescription:(nullable NSString *)error;
 - (void)control:(NSControl *)control didFailToValidatePartialString:(NSString *)string errorDescription:(nullable NSString *)error;
-- (BOOL)control:(NSControl *)control isValidObject:(id)obj;
+- (BOOL)control:(NSControl *)control isValidObject:(nullable id)obj;
 
 - (BOOL)control:(NSControl *)control textView:(NSTextView *)textView doCommandBySelector:(SEL)commandSelector;
 - (NSArray<NSString *> *)control:(NSControl *)control textView:(NSTextView *)textView completions:(NSArray<NSString *> *)words forPartialWordRange:(NSRange)charRange indexOfSelectedItem:(NSInteger *)index;
@@ -160,11 +165,11 @@
 - (void)setNeedsDisplay;    // Use setNeedsDisplay:YES instead.
 - (void)calcSize;
 
-- (void)updateCell:(NSCell *)aCell;
-- (void)updateCellInside:(NSCell *)aCell;
-- (void)drawCellInside:(NSCell *)aCell;
-- (void)drawCell:(NSCell *)aCell;
-- (void)selectCell:(NSCell *)aCell;
+- (void)updateCell:(NSCell *)cell;
+- (void)updateCellInside:(NSCell *)cell;
+- (void)drawCellInside:(NSCell *)cell;
+- (void)drawCell:(NSCell *)cell;
+- (void)selectCell:(NSCell *)cell;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSController.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSController.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSController.h
 	Application Kit
-	Copyright (c) 2002-2015, Apple Inc.
+	Copyright (c) 2002-2016, Apple Inc.
 	All rights reserved.
  */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCursor.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCursor.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCursor.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCursor.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSCursor.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -57,8 +57,10 @@
 + (NSCursor *)contextualMenuCursor NS_AVAILABLE_MAC(10_6);
 + (NSCursor *)IBeamCursorForVerticalLayout NS_AVAILABLE_MAC(10_7);
 
-- (instancetype)initWithImage:(NSImage *)newImage hotSpot:(NSPoint)aPoint;
-- (instancetype)initWithImage:(NSImage *)newImage	foregroundColorHint:(nullable NSColor *)fg backgroundColorHint:(nullable NSColor *)bg hotSpot:(NSPoint)hotSpot;
+- (instancetype)initWithImage:(NSImage *)newImage hotSpot:(NSPoint)point NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
+
+- (instancetype)initWithImage:(NSImage *)newImage foregroundColorHint:(nullable NSColor *)fg backgroundColorHint:(nullable NSColor *)bg hotSpot:(NSPoint)hotSpot NS_DEPRECATED_MAC(10_0, 10_12, "Color hints are ignored. Use -initWithImage:hotSpot: instead");
 
 + (void)hide;
 + (void)unhide;
@@ -74,8 +76,8 @@
 - (void)setOnMouseEntered:(BOOL)flag;
 @property (getter=isSetOnMouseExited, readonly) BOOL setOnMouseExited;
 @property (getter=isSetOnMouseEntered, readonly) BOOL setOnMouseEntered;
-- (void)mouseEntered:(NSEvent *)theEvent;
-- (void)mouseExited:(NSEvent *)theEvent;
+- (void)mouseEntered:(NSEvent *)event;
+- (void)mouseExited:(NSEvent *)event;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCustomImageRep.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCustomImageRep.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCustomImageRep.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCustomImageRep.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSCustomImageRep.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -19,7 +19,7 @@
 - (instancetype)initWithSize:(NSSize)size flipped:(BOOL)drawingHandlerShouldBeCalledWithFlippedContext drawingHandler:(BOOL (^)(NSRect dstRect))drawingHandler NS_AVAILABLE_MAC(10_8);
 @property (nullable, readonly, copy) BOOL (^drawingHandler)(NSRect) NS_AVAILABLE_MAC(10_8);
 
-- (instancetype)initWithDrawSelector:(SEL)aMethod delegate:(id)anObject;
+- (instancetype)initWithDrawSelector:(SEL)selector delegate:(id)delegate;
 @property (nullable, readonly) SEL drawSelector;
 @property (nullable, readonly, assign) id delegate;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDataAsset.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDataAsset.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDataAsset.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDataAsset.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSDataAsset.h
 	Application Kit
-	Copyright (c) 2015, Apple Inc.
+	Copyright (c) 2015-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDatePicker.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDatePicker.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDatePicker.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDatePicker.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSDatePicker.h
 	Application Kit
-	Copyright (c) 2004-2015, Apple Inc.
+	Copyright (c) 2004-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDatePickerCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDatePickerCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDatePickerCell.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDatePickerCell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSDatePickerCell.h
 	Application Kit
-	Copyright (c) 2004-2015, Apple Inc.
+	Copyright (c) 2004-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -61,13 +61,17 @@
     NSColor *_backgroundColor;
     NSColor *_textColor;
     int _indexOfSelectedSubfield;
-    int _reserved0;
+    int _reserved0 __unused;
     id _reserved1;
     id _reserved2;
     id _reserved3;
     id _reserved4;
 }
 
+- (instancetype)initTextCell:(NSString *)string NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
+- (instancetype)initImageCell:(nullable NSImage *)image NS_UNAVAILABLE;
+
 #pragma mark *** Appearance Control ***
 
 @property NSDatePickerStyle datePickerStyle;
@@ -112,7 +116,7 @@
 
 @protocol NSDatePickerCellDelegate <NSObject>
 @optional
-- (void)datePickerCell:(NSDatePickerCell *)aDatePickerCell validateProposedDateValue:(NSDate * __nonnull *__nonnull)proposedDateValue timeInterval:(nullable NSTimeInterval *)proposedTimeInterval;
+- (void)datePickerCell:(NSDatePickerCell *)datePickerCell validateProposedDateValue:(NSDate * __nonnull *__nonnull)proposedDateValue timeInterval:(nullable NSTimeInterval *)proposedTimeInterval;
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDictionaryController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDictionaryController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDictionaryController.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDictionaryController.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSDictionaryController.h
 	Application Kit
-	Copyright (c) 2002-2015, Apple Inc.
+	Copyright (c) 2002-2016, Apple Inc.
 	All rights reserved.
  */
 
@@ -31,9 +31,9 @@
 NS_CLASS_AVAILABLE(10_5, NA)
 @interface NSDictionaryController : NSArrayController {
 @private
-    void *_reserved5;
-    void *_reserved6;
-    void *_reserved7;
+    void *_reserved5 __unused;
+    void *_reserved6 __unused;
+    void *_reserved7 __unused;
 	id _contentDictionary;
 	NSString *_initialKey;
 	id _initialValue;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDockTile.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDockTile.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDockTile.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDockTile.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSDockTile.h
 	Application Kit
-	Copyright (c) 2006-2015, Apple Inc.
+	Copyright (c) 2006-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -18,7 +18,7 @@
 
 NS_CLASS_AVAILABLE(10_5, NA)
 @interface NSDockTile : NSObject {
-    @private;
+    @private
     id _owner;
     void *_dockContextRef;
     NSView *_contentView;
@@ -31,7 +31,7 @@
     } _dFlags;
     NSSize _dockTileSize;
     id _miniViewController;
-    id reserved[4];
+    id reserved[4] __unused;
 }
 
 /* get the size of the dock tile, in screen coordinates
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDocument.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDocument.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDocument.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDocument.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSDocument.h
 	Application Kit
-	Copyright (c) 1997-2015, Apple Inc.
+	Copyright (c) 1997-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -86,8 +86,8 @@
     NSURL *_fileURL;
     NSString *_fileType;
     NSPrintInfo *_printInfo;
-    long _documentReserved;
-    NSView *savePanelAccessory;
+    long _documentReserved __unused;
+    NSView *savePanelAccessory __unused;
     id _displayName;
     id _privateData;
     NSUndoManager *_undoManager;
@@ -201,7 +201,7 @@
 
 This method is useful when code executed in a block passed to -performActivityWithSynchronousWaiting:usingBlock: may also invoke that method. For example, -saveDocumentWithDelegate:didSaveSelector:contextInfo:, which uses -performActivityWithSynchronousWaiting:usingBlock:, uses this around its invocation of -runModalSavePanelForSaveOperation:delegate:didSaveSelector: or -saveToURL:ofType:forSaveOperation:delegate:didSaveSelector:contextInfo: because both of those methods also use -performActivityWithSynchronousWaiting:usingBlock:. Without the use of this method that inner invocation of -performActivityWithSynchronousWaiting:usingBlock: would wait forever.
 */
-- (void)continueActivityUsingBlock:(void (^)(void))block NS_AVAILABLE_MAC(10_7);
+- (void)continueActivityUsingBlock:(void (NS_NOESCAPE ^)(void))block NS_AVAILABLE_MAC(10_7);
 
 /* Invoke the block on the main thread. If the main thread is blocked by an invocation of -performActivityWithSynchronousWaiting:usingBlock: or -performSynchronousFileAccessUsingBlock:, interrupt that blocking to invoke the block, and then resume blocking when the invocation of the block has returned. Invocations of this method always return before the passed-in block is invoked.
 
@@ -222,11 +222,11 @@
 - -updateChangeCountWithToken:forSaveOperation: and, sometimes, updateChangeCount:, to make using this mechanism when invoking -isDocumentEdited and -hasUnautosavedChanges meaningful.
 - -backupFileURL, since it depends on -fileURL.
  */
-- (void)performSynchronousFileAccessUsingBlock:(void (^)(void))block NS_AVAILABLE_MAC(10_7);
+- (void)performSynchronousFileAccessUsingBlock:(void (NS_NOESCAPE ^)(void))block NS_AVAILABLE_MAC(10_7);
 
 /* Do the same sort of thing as -performSynchronousFileAccessUsingBlock:, but without ever blocking the main thread, and perhaps not invoking the block until after the method invocation has returned, though still always on the same thread as the method invocation. The block is passed another block, the file access completion handler, which must be invoked when the file access is complete, though it can be invoked from any thread. This method is for use with file access that might begin on one thread but continue on another before it is complete. saveToURL:ofType:forSaveOperation:completionHandler: for for example uses this method instead of -performSynchronousFileAccessUsingBlock: because if it does asynchronous saving then there is no way for it to actually complete all of its file access before returning from the file access block.
 
-The distinction between entire activities and the file accessing part of activities established by having both activity performing methods and file access performing methods is worthwhile because sometimes it is valuable to perform file access without any risk of waiting for the user to dimiss a modal panel. For example, NSDocument's implementation of -[NSFilePresenter relinquishPresentedItemToWriter:] uses -performAsynchronousFileAccessUsingBlock: to ensure that the uses of -performSynchronousFileAccessUsingBlock: described above wait while another process is moving, renaming, or changing the file. Using -performActivityWithSynchronousWaiting:usingBlock: instead would not be appropriate because that would introduce the possibility of the other process' writing being blocked until the user has dismissed a sheet that is being presented as part of a previously scheduled activity.
+The distinction between entire activities and the file accessing part of activities established by having both activity performing methods and file access performing methods is worthwhile because sometimes it is valuable to perform file access without any risk of waiting for the user to dismiss a modal panel. For example, NSDocument's implementation of -[NSFilePresenter relinquishPresentedItemToWriter:] uses -performAsynchronousFileAccessUsingBlock: to ensure that the uses of -performSynchronousFileAccessUsingBlock: described above wait while another process is moving, renaming, or changing the file. Using -performActivityWithSynchronousWaiting:usingBlock: instead would not be appropriate because that would introduce the possibility of the other process' writing being blocked until the user has dismissed a sheet that is being presented as part of a previously scheduled activity.
 */
 - (void)performAsynchronousFileAccessUsingBlock:(void (^)(void (^fileAccessCompletionHandler)(void)))block NS_AVAILABLE_MAC(10_7);
 
@@ -324,7 +324,7 @@
 
 /* Given that a file is being saved, return the attributes that should be written to a file or file package located by a URL, formatted to a specified type, for a particular kind of save operation. If not successful, return nil after setting *outError to an NSError that encapsulates the reason why attributes could not be returned. The set of valid file attributes is a subset of those understood by the NSFileManager class. The default implementation of this method returns an empty dictionary for an NSSaveOperation or NSAutosaveInPlaceOperation, or a dictionary with an appropriate NSFileExtensionHidden entry for any other kind of save operation. You can override this method to customize the attributes that are written to document files.
 
-For backward binary comaptibility with Mac OS 10.5 and earlier the default implementation of this method instead returns a dictionary with NSFileHFSCreatorCode and NSFileHFSTypeCode entries that have a value of 0 for NSSaveOperation, in applications linked against Mac OS 10.5 or earlier.
+For backward binary compatibility with Mac OS 10.5 and earlier the default implementation of this method instead returns a dictionary with NSFileHFSCreatorCode and NSFileHFSTypeCode entries that have a value of 0 for NSSaveOperation, in applications linked against Mac OS 10.5 or earlier.
 
 For backward binary compatibility with Mac OS 10.3 and earlier, the default implementation of this method instead invokes [self fileAttributesToWriteToFile:[url path] ofType:typeName saveOperation:aSaveOperation] if -fileAttributesToWriteToFile:ofType:saveOperation: is overridden and the URL uses the "file:" scheme. The save operation used in this case will never be one of the autosaving ones; NSSaveToOperation will be used instead.
 
@@ -472,7 +472,7 @@
 
 /* Return YES if the receiving subclass of NSDocument supports Mac OS 10.8 autosaving of drafts, NO otherwise. The default implementation of this method returns YES for applications linked on or after Mac OS 10.8. You can override it and return YES to declare your NSDocument subclass' ability to do Mac OS 10.8 autosaving of drafts. You can also override it and return NO to opt out of this behavior after linking with 10.8. You should not invoke this method to find out whether autosaving of a draft will be done. Instances of subclasses that return YES from this method should be ready to properly handle save operations with NSAutosaveAsOperation.
 
-AppKit invokes this method at a variety of times. For example, when -updateChangeCount is called with NSChagneDone (without NSChangeDiscardable), NSDocument will the next autosave to use NSAutosaveAsOperation and return the document into a draft.
+AppKit invokes this method at a variety of times. For example, when -updateChangeCount is called with NSChangeDone (without NSChangeDiscardable), NSDocument will the next autosave to use NSAutosaveAsOperation and return the document into a draft.
 */
 + (BOOL)autosavesDrafts NS_AVAILABLE_MAC(10_8);
 
@@ -488,7 +488,7 @@
 
 #pragma mark *** Closing ***
 
-/* If there are changes that have not yet been saved to the document's file and saving cannot be done without asking the user first, present a panel to the user informing them that the document is modified and asking if it should be saved. If the user indicates that it should be, then try to save it. When saving is completed, regardless of success or failure, or has been rejected one way or another by the user, send the message selected by shouldCloseSelector to the delegate, with the contextInfo as the last argument. If the document is not modified then just send the mesage selected by shouldCloseSelector right away. The method selected by shouldCloseSelector must have the same signature as:
+/* If there are changes that have not yet been saved to the document's file and saving cannot be done without asking the user first, present a panel to the user informing them that the document is modified and asking if it should be saved. If the user indicates that it should be, then try to save it. When saving is completed, regardless of success or failure, or has been rejected one way or another by the user, send the message selected by shouldCloseSelector to the delegate, with the contextInfo as the last argument. If the document is not modified then just send the message selected by shouldCloseSelector right away. The method selected by shouldCloseSelector must have the same signature as:
 
     - (void)document:(NSDocument *)document shouldClose:(BOOL)shouldClose contextInfo:(void *)contextInfo;
 
@@ -743,7 +743,7 @@
 
 /* Returns the name for this document that is fit for presentation to the user. You can override this method, but overriding -[NSWindowController windowTitleForDocumentDisplayName:] is usually better, because a document's display name is used in error alerts, alerts presented during document saving, the alert that's presented when the user attempts to close a document that has unsaved changes, and save panels (as the default value of the "Save As:" field). In those places the document file's actual name really is what should be used.
 */
-@property (readonly, copy) NSString *displayName;
+@property (copy, null_resettable) NSString *displayName;
 
 /* Return the default draft name for the receiver. The default implementation returns the "Untitled" string for the user's current locale.
  
@@ -771,7 +771,7 @@
 
 /* Return the names of the types to which this document can be saved for a kind of save operation. For every kind of save operation except NSSaveToOperation the returned array must only include types for which the the application can play the Editor role. For NSSaveToOperation the returned array may include types for which the application can only play the Viewer role, and other types that the application can merely export. The default implementation of this method returns [[self class] writableTypes] with, except during NSSaveToOperations, types for which +isNativeType returns NO filtered out.
 
-You can override this method to limit the set of writable types when the documently currently contains data that is not representable in all types. For example, you can disallow saving to .rtf files when the document contains an attachment and can only be saved properly to .rtfd files. NSDocument uses this this method during save operations that present save panels, and during scripted save operations that do not. It may be called at additional times in future releases of Mac OS X. 
+You can override this method to limit the set of writable types when the document currently contains data that is not representable in all types. For example, you can disallow saving to .rtf files when the document contains an attachment and can only be saved properly to .rtfd files. NSDocument uses this this method during save operations that present save panels, and during scripted save operations that do not. It may be called at additional times in future releases of Mac OS X. 
 
 You can invoke this method when creating a custom save panel accessory view to easily present the same set of types that NSDocument would in its standard file format popup menu.
 */
@@ -787,7 +787,7 @@
 
 /* Conformance to the NSUserInterfaceValidations protocol. NSDocument's implementation of this method conditionally enables menu items for all of the action methods listed in this header file.
 */
-- (BOOL)validateUserInterfaceItem:(id <NSValidatedUserInterfaceItem>)anItem;
+- (BOOL)validateUserInterfaceItem:(id <NSValidatedUserInterfaceItem>)item;
 
 #pragma mark *** Ubiquitous Storage ***
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDocumentController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDocumentController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDocumentController.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDocumentController.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSDocumentController.h
 	Application Kit
-	Copyright (c) 1997-2015, Apple Inc.
+	Copyright (c) 1997-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -257,7 +257,7 @@
 
 /* Conformance to the NSUserInterfaceValidations protocol. NSDocumentController's implementation of this method conditionally enables menu items for all of the action methods listed in this header file, as well as the private action method for Open Recent menu items.
 */
-- (BOOL)validateUserInterfaceItem:(id <NSValidatedUserInterfaceItem>)anItem;
+- (BOOL)validateUserInterfaceItem:(id <NSValidatedUserInterfaceItem>)item;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDocumentScripting.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDocumentScripting.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDocumentScripting.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDocumentScripting.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSDocumentScripting.h
         AppKit Framework
-        Copyright (c) 1997-2015, Apple Inc.
+        Copyright (c) 1997-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDragging.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDragging.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDragging.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDragging.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSDragging.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -96,7 +96,7 @@
 
 /* Enumerate through each dragging item. Any changes made to the properties of the draggingItem are reflected in the drag and are automatically removed when the drag exits. Classes in the provided array must implement the NSPasteboardReading protocol. Cocoa classes that implement this protocol include NSImage, NSString, NSURL, NSColor, NSAttributedString, and NSPasteboardItem. For every item on the pasteboard, each class in the provided array will be queried for the types it can read using -readableTypesForPasteboard:. An instance will be created of the first class found in the provided array whose readable types match a conforming type contained in that pasteboard item. If an Instance is created from the pasteboard item data, it is placed into an NSDraggingItem along with the dragging properties of that item such as the dragging image. The NSDraggingItem is then passed as a parameter to the provided block. Additional search options, such as restricting the search to file URLs with particular content types, can be specified with a search options dictionary.  See the comments for the Pasteboard Reading Options keys in NSPasteboard.h for a full description. Note: all coordinate properties in the NSDraggingItem are in the coordinate system of view. If view is nil, the screen coordinate space is used.
 */
-- (void)enumerateDraggingItemsWithOptions:(NSDraggingItemEnumerationOptions)enumOpts forView:(NSView *)view classes:(NSArray<Class> *)classArray searchOptions:(NSDictionary<NSString *, id> *)searchOptions usingBlock:(void (^)(NSDraggingItem *draggingItem, NSInteger idx, BOOL *stop))block NS_AVAILABLE_MAC(10_7);
+- (void)enumerateDraggingItemsWithOptions:(NSDraggingItemEnumerationOptions)enumOpts forView:(nullable  NSView *)view classes:(NSArray<Class> *)classArray searchOptions:(NSDictionary<NSString *, id> *)searchOptions usingBlock:(void (^)(NSDraggingItem *draggingItem, NSInteger idx, BOOL *stop))block NS_AVAILABLE_MAC(10_7);
 
 @property (readonly) NSSpringLoadingHighlight springLoadingHighlight NS_AVAILABLE_MAC(10_11);
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDraggingItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDraggingItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDraggingItem.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDraggingItem.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSDraggingItem.h
 	Application Kit
-	Copyright (c) 2010-2015, Apple Inc.
+	Copyright (c) 2010-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -30,7 +30,8 @@
 + (NSDraggingImageComponent *)draggingImageComponentWithKey:(NSString *)key;
 
 /* Designated initializer */
-- (instancetype)initWithKey:(NSString *)key;
+- (instancetype)initWithKey:(NSString *)key NS_DESIGNATED_INITIALIZER;
+- (instancetype)init NS_UNAVAILABLE;
 
 /* key must be unique for each component in an NSDraggingItem. You can create your own named components, but the following names have special meaning. NSDraggingImageComponentIconKey is an image of the item being dragged. NSDraggingImageComponentLabelKey represents a textual label associate with the item, for example, a file name.
 */
@@ -61,7 +62,8 @@
 
 /* The designated initializer. When creating an NSDraggingItem the pasteboardWriter must implement the NSPasteboardWriting protocol.
 */
-- (instancetype)initWithPasteboardWriter:(id <NSPasteboardWriting>) pasteboardWriter;
+- (instancetype)initWithPasteboardWriter:(id <NSPasteboardWriting>) pasteboardWriter NS_DESIGNATED_INITIALIZER;
+- (instancetype)init NS_UNAVAILABLE;
 
 /* When you create an NSDraggingItem, item is the pasteboardWriter passed to initWithPasteboardWriter. However, when enumerating dragging items in an NSDraggingSession or NSDraggingInfo object, item is not the original pasteboardWriter. It is an instance of one of the classes provided to the enumeration method.
 */
@@ -75,9 +77,9 @@
 */
 @property (nullable, copy) NSArray<NSDraggingImageComponent *> * __nonnull (^imageComponentsProvider)(void);
 
-/* Alternate single image component setter. This method simplifies modifiying the components of an NSDraggingItem when there is only one component. This method will set the draggingFrame and imageComponentsProvider properties. frame is in the same coordinate space that the draggingFrame property is.
+/* Alternate single image component setter. This method simplifies modifiying the components of an NSDraggingItem when there is only one component. This method will set the draggingFrame and imageComponentsProvider properties. frame is in the same coordinate space that the draggingFrame property is. To hide this item, set contents to nil.
 */
-- (void)setDraggingFrame:(NSRect)frame contents:(id)contents;
+- (void)setDraggingFrame:(NSRect)frame contents:(nullable id)contents;
 
 /* An array of NSDraggingImageComponents that are used to create the drag image. Note: the array contains copies of the components. Changes made to these copies are not reflected in the drag. If needed, the imageComponentsProvider block is called to generate the image components.
 */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDraggingSession.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDraggingSession.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDraggingSession.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDraggingSession.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSDraggingSession.h
 	Application Kit
-	Copyright (c) 2010-2015, Apple Inc.
+	Copyright (c) 2010-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -72,7 +72,7 @@
 
 /* Enumerate through each dragging item. Any changes made to the properties of the draggingItem are reflected in the drag when the destination is not overriding them. Classes in the provided array must implement the NSPasteboardReading protocol. Cocoa classes that implement this protocol include NSImage, NSString, NSURL, NSColor, NSAttributedString, and NSPasteboardItem. For every item on the pasteboard, each class in the provided array will be queried for the types it can read using -readableTypesForPasteboard:. An instance will be created of the first class found in the provided array whose readable types match a conforming type contained in that pasteboard item. If an Instance is created from the pasteboard item data, it is placed into an NSDraggingItem along with the dragging properties of that item such as the drag image. The NSDraggingItem is then passed as a parameter to the provided block. Additional search options, such as restricting the search to file URLs with particular content types, can be specified with a search options dictionary.  See the comments for the Pasteboard Reading Options keys in NSPasteboard.h for a full description. Note: all coordinate properties in the NSDraggingItem are in the coordinate system of view. If view is nil, the screen coordinate space is used.
 */
-- (void)enumerateDraggingItemsWithOptions:(NSDraggingItemEnumerationOptions)enumOpts forView:(nullable NSView *)view classes:(NSArray<Class> *)classArray searchOptions:(NSDictionary<NSString *, id> *)searchOptions usingBlock:(void (^)(NSDraggingItem *draggingItem, NSInteger idx, BOOL *stop))block;
+- (void)enumerateDraggingItemsWithOptions:(NSDraggingItemEnumerationOptions)enumOpts forView:(nullable NSView *)view classes:(NSArray<Class> *)classArray searchOptions:(NSDictionary<NSString *, id> *)searchOptions usingBlock:(void (NS_NOESCAPE ^)(NSDraggingItem *draggingItem, NSInteger idx, BOOL *stop))block;
 @end
 
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDrawer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDrawer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDrawer.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDrawer.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSDrawer.h
         Application Kit
-        Copyright (c) 1999-2015, Apple Inc.
+        Copyright (c) 1999-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -49,10 +49,10 @@
     CFAbsoluteTime 	_drawerStartTime;
     CFTimeInterval 	_drawerTotalTime;
     CFRunLoopRef 	_drawerLoop;
-    __strong CFRunLoopTimerRef 	_drawerTimer;
+    CFRunLoopTimerRef 	_drawerTimer;
     id 			_drawerDelegate;
     unsigned int	_drawerFlags;
-    __strong CFRunLoopObserverRef _drawerObserver;
+    CFRunLoopObserverRef _drawerObserver;
 }
 
 - (instancetype)initWithContentSize:(NSSize)contentSize preferredEdge:(NSRectEdge)edge;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSEPSImageRep.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSEPSImageRep.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSEPSImageRep.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSEPSImageRep.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSEPSImageRep.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSErrors.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSErrors.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSErrors.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSErrors.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSErrors.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSEvent.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSEvent.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSEvent.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSEvent.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSEvent.h
     Application Kit
-    Copyright (c) 1994-2015, Apple Inc.
+    Copyright (c) 1994-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -20,29 +20,29 @@
 @class NSGraphicsContext, NSWindow, NSTrackingArea;
 
 typedef NS_ENUM(NSUInteger, NSEventType) {        /* various types of events */
-    NSLeftMouseDown             = 1,            
-    NSLeftMouseUp               = 2,
-    NSRightMouseDown            = 3,
-    NSRightMouseUp              = 4,
-    NSMouseMoved                = 5,
-    NSLeftMouseDragged          = 6,
-    NSRightMouseDragged         = 7,
-    NSMouseEntered              = 8,
-    NSMouseExited               = 9,
-    NSKeyDown                   = 10,
-    NSKeyUp                     = 11,
-    NSFlagsChanged              = 12,
-    NSAppKitDefined             = 13,
-    NSSystemDefined             = 14,
-    NSApplicationDefined        = 15,
-    NSPeriodic                  = 16,
-    NSCursorUpdate              = 17,
-    NSScrollWheel               = 22,
-    NSTabletPoint               = 23,
-    NSTabletProximity           = 24,
-    NSOtherMouseDown            = 25,
-    NSOtherMouseUp              = 26,
-    NSOtherMouseDragged         = 27,
+    NSEventTypeLeftMouseDown             = 1,
+    NSEventTypeLeftMouseUp               = 2,
+    NSEventTypeRightMouseDown            = 3,
+    NSEventTypeRightMouseUp              = 4,
+    NSEventTypeMouseMoved                = 5,
+    NSEventTypeLeftMouseDragged          = 6,
+    NSEventTypeRightMouseDragged         = 7,
+    NSEventTypeMouseEntered              = 8,
+    NSEventTypeMouseExited               = 9,
+    NSEventTypeKeyDown                   = 10,
+    NSEventTypeKeyUp                     = 11,
+    NSEventTypeFlagsChanged              = 12,
+    NSEventTypeAppKitDefined             = 13,
+    NSEventTypeSystemDefined             = 14,
+    NSEventTypeApplicationDefined        = 15,
+    NSEventTypePeriodic                  = 16,
+    NSEventTypeCursorUpdate              = 17,
+    NSEventTypeScrollWheel               = 22,
+    NSEventTypeTabletPoint               = 23,
+    NSEventTypeTabletProximity           = 24,
+    NSEventTypeOtherMouseDown            = 25,
+    NSEventTypeOtherMouseUp              = 26,
+    NSEventTypeOtherMouseDragged         = 27,
     /* The following event types are available on some hardware on 10.5.2 and later */
     NSEventTypeGesture NS_ENUM_AVAILABLE_MAC(10_5)       = 29,
     NSEventTypeMagnify NS_ENUM_AVAILABLE_MAC(10_5)       = 30,
@@ -50,43 +50,67 @@
     NSEventTypeRotate  NS_ENUM_AVAILABLE_MAC(10_5)       = 18,
     NSEventTypeBeginGesture NS_ENUM_AVAILABLE_MAC(10_5)  = 19,
     NSEventTypeEndGesture NS_ENUM_AVAILABLE_MAC(10_5)    = 20,
-
+    
 #if __LP64__
     NSEventTypeSmartMagnify NS_ENUM_AVAILABLE_MAC(10_8) = 32,
 #endif
     NSEventTypeQuickLook NS_ENUM_AVAILABLE_MAC(10_8) = 33,
-
+    
 #if __LP64__
     NSEventTypePressure NS_ENUM_AVAILABLE_MAC(10_10_3) = 34
 #endif
 };
 
+static const NSEventType NSLeftMouseDown 	API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeLeftMouseDown", macosx(10.0, 10.12)) = NSEventTypeLeftMouseDown;
+static const NSEventType NSLeftMouseUp 		API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeLeftMouseUp", macosx(10.0, 10.12)) = NSEventTypeLeftMouseUp;
+static const NSEventType NSRightMouseDown 	API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeRightMouseDown", macosx(10.0, 10.12)) = NSEventTypeRightMouseDown;
+static const NSEventType NSRightMouseUp		API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeRightMouseUp", macosx(10.0, 10.12)) = NSEventTypeRightMouseUp;
+static const NSEventType NSMouseMoved 		API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeMouseMoved", macosx(10.0, 10.12)) = NSEventTypeMouseMoved;
+static const NSEventType NSLeftMouseDragged	API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeLeftMouseDragged", macosx(10.0, 10.12)) = NSEventTypeLeftMouseDragged;
+static const NSEventType NSRightMouseDragged 	API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeRightMouseDragged", macosx(10.0, 10.12)) = NSEventTypeRightMouseDragged;
+static const NSEventType NSMouseEntered 	API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeMouseEntered", macosx(10.0, 10.12)) = NSEventTypeMouseEntered;
+static const NSEventType NSMouseExited 		API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeMouseExited", macosx(10.0, 10.12)) = NSEventTypeMouseExited;
+static const NSEventType NSKeyDown 		API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeKeyDown", macosx(10.0, 10.12)) = NSEventTypeKeyDown;
+static const NSEventType NSKeyUp 		API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeKeyUp", macosx(10.0, 10.12)) = NSEventTypeKeyUp;
+static const NSEventType NSFlagsChanged 	API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeFlagsChanged", macosx(10.0, 10.12)) = NSEventTypeFlagsChanged;
+static const NSEventType NSAppKitDefined 	API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeAppKitDefined", macosx(10.0, 10.12)) = NSEventTypeAppKitDefined;
+static const NSEventType NSSystemDefined 	API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeSystemDefined", macosx(10.0, 10.12)) = NSEventTypeSystemDefined;
+static const NSEventType NSApplicationDefined	API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeApplicationDefined", macosx(10.0, 10.12)) = NSEventTypeApplicationDefined;
+static const NSEventType NSPeriodic 		API_DEPRECATED_WITH_REPLACEMENT("NSEventTypePeriodic", macosx(10.0, 10.12)) = NSEventTypePeriodic;
+static const NSEventType NSCursorUpdate 	API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeCursorUpdate", macosx(10.0, 10.12)) = NSEventTypeCursorUpdate;
+static const NSEventType NSScrollWheel 		API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeScrollWheel", macosx(10.0, 10.12)) = NSEventTypeScrollWheel;
+static const NSEventType NSTabletPoint 		API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeTabletPoint", macosx(10.0, 10.12)) = NSEventTypeTabletPoint;
+static const NSEventType NSTabletProximity 	API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeTabletProximity", macosx(10.0, 10.12)) = NSEventTypeTabletProximity;
+static const NSEventType NSOtherMouseDown	API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeOtherMouseDown", macosx(10.0, 10.12)) = NSEventTypeOtherMouseDown;
+static const NSEventType NSOtherMouseUp 	API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeOtherMouseUp", macosx(10.0, 10.12)) = NSEventTypeOtherMouseUp;
+static const NSEventType NSOtherMouseDragged 	API_DEPRECATED_WITH_REPLACEMENT("NSEventTypeOtherMouseDragged", macosx(10.0, 10.12)) = NSEventTypeOtherMouseDragged;
+
 
 // For APIs introduced in Mac OS X 10.6 and later, this type is used with NS*Mask constants to indicate the events of interest.
 typedef NS_OPTIONS(unsigned long long, NSEventMask) { /* masks for the types of events */
-    NSLeftMouseDownMask         = 1 << NSLeftMouseDown,
-    NSLeftMouseUpMask           = 1 << NSLeftMouseUp,
-    NSRightMouseDownMask        = 1 << NSRightMouseDown,
-    NSRightMouseUpMask          = 1 << NSRightMouseUp,
-    NSMouseMovedMask            = 1 << NSMouseMoved,
-    NSLeftMouseDraggedMask      = 1 << NSLeftMouseDragged,
-    NSRightMouseDraggedMask     = 1 << NSRightMouseDragged,
-    NSMouseEnteredMask          = 1 << NSMouseEntered,
-    NSMouseExitedMask           = 1 << NSMouseExited,
-    NSKeyDownMask               = 1 << NSKeyDown,
-    NSKeyUpMask                 = 1 << NSKeyUp,
-    NSFlagsChangedMask          = 1 << NSFlagsChanged,
-    NSAppKitDefinedMask         = 1 << NSAppKitDefined,
-    NSSystemDefinedMask         = 1 << NSSystemDefined,
-    NSApplicationDefinedMask    = 1 << NSApplicationDefined,
-    NSPeriodicMask              = 1 << NSPeriodic,
-    NSCursorUpdateMask          = 1 << NSCursorUpdate,
-    NSScrollWheelMask           = 1 << NSScrollWheel,
-    NSTabletPointMask           = 1 << NSTabletPoint,
-    NSTabletProximityMask       = 1 << NSTabletProximity,
-    NSOtherMouseDownMask        = 1 << NSOtherMouseDown,
-    NSOtherMouseUpMask          = 1 << NSOtherMouseUp,
-    NSOtherMouseDraggedMask     = 1 << NSOtherMouseDragged,
+    NSEventMaskLeftMouseDown        = 1 << NSEventTypeLeftMouseDown,
+    NSEventMaskLeftMouseUp           = 1 << NSEventTypeLeftMouseUp,
+    NSEventMaskRightMouseDown        = 1 << NSEventTypeRightMouseDown,
+    NSEventMaskRightMouseUp          = 1 << NSEventTypeRightMouseUp,
+    NSEventMaskMouseMoved            = 1 << NSEventTypeMouseMoved,
+    NSEventMaskLeftMouseDragged      = 1 << NSEventTypeLeftMouseDragged,
+    NSEventMaskRightMouseDragged     = 1 << NSEventTypeRightMouseDragged,
+    NSEventMaskMouseEntered          = 1 << NSEventTypeMouseEntered,
+    NSEventMaskMouseExited           = 1 << NSEventTypeMouseExited,
+    NSEventMaskKeyDown               = 1 << NSEventTypeKeyDown,
+    NSEventMaskKeyUp                 = 1 << NSEventTypeKeyUp,
+    NSEventMaskFlagsChanged          = 1 << NSEventTypeFlagsChanged,
+    NSEventMaskAppKitDefined         = 1 << NSEventTypeAppKitDefined,
+    NSEventMaskSystemDefined         = 1 << NSEventTypeSystemDefined,
+    NSEventMaskApplicationDefined    = 1 << NSEventTypeApplicationDefined,
+    NSEventMaskPeriodic              = 1 << NSEventTypePeriodic,
+    NSEventMaskCursorUpdate          = 1 << NSEventTypeCursorUpdate,
+    NSEventMaskScrollWheel           = 1 << NSEventTypeScrollWheel,
+    NSEventMaskTabletPoint           = 1 << NSEventTypeTabletPoint,
+    NSEventMaskTabletProximity       = 1 << NSEventTypeTabletProximity,
+    NSEventMaskOtherMouseDown        = 1 << NSEventTypeOtherMouseDown,
+    NSEventMaskOtherMouseUp          = 1 << NSEventTypeOtherMouseUp,
+    NSEventMaskOtherMouseDragged     = 1 << NSEventTypeOtherMouseDragged,
     /* The following event masks are available on some hardware on 10.5.2 and later */
     NSEventMaskGesture NS_ENUM_AVAILABLE_MAC(10_5)          = 1 << NSEventTypeGesture,
     NSEventMaskMagnify NS_ENUM_AVAILABLE_MAC(10_5)          = 1 << NSEventTypeMagnify,
@@ -102,9 +126,34 @@
     NSEventMaskPressure NS_ENUM_AVAILABLE_MAC(10_10_3) = 1ULL << NSEventTypePressure,
 #endif
     
-    NSAnyEventMask              = NSUIntegerMax
+    NSEventMaskAny              = NSUIntegerMax,
+    
 };
 
+static const NSEventMask NSLeftMouseDownMask 		API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskLeftMouseDown", macosx(10.0, 10.12)) = NSEventMaskLeftMouseDown;
+static const NSEventMask NSLeftMouseUpMask 		API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskLeftMouseUp", macosx(10.0, 10.12)) = NSEventMaskLeftMouseUp;
+static const NSEventMask NSRightMouseDownMask	 	API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskRightMouseDown", macosx(10.0, 10.12)) = NSEventMaskRightMouseDown;
+static const NSEventMask NSRightMouseUpMask 		API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskRightMouseUp", macosx(10.0, 10.12)) = NSEventMaskRightMouseUp;
+static const NSEventMask NSMouseMovedMask 		API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskMouseMoved", macosx(10.0, 10.12)) = NSEventMaskMouseMoved;
+static const NSEventMask NSLeftMouseDraggedMask 	API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskLeftMouseDragged", macosx(10.0, 10.12)) = NSEventMaskLeftMouseDragged;
+static const NSEventMask NSRightMouseDraggedMask 	API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskRightMouseDragged", macosx(10.0, 10.12)) = NSEventMaskRightMouseDragged;
+static const NSEventMask NSMouseEnteredMask 		API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskMouseEntered", macosx(10.0, 10.12)) = NSEventMaskMouseEntered;
+static const NSEventMask NSMouseExitedMask 		API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskMouseExited", macosx(10.0, 10.12)) = NSEventMaskMouseExited;
+static const NSEventMask NSKeyDownMask 			API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskKeyDown", macosx(10.0, 10.12)) = NSEventMaskKeyDown;
+static const NSEventMask NSKeyUpMask 			API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskKeyUp", macosx(10.0, 10.12)) = NSEventMaskKeyUp;
+static const NSEventMask NSFlagsChangedMask 		API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskFlagsChanged", macosx(10.0, 10.12)) = NSEventMaskFlagsChanged;
+static const NSEventMask NSAppKitDefinedMask 		API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskAppKitDefined", macosx(10.0, 10.12)) = NSEventMaskAppKitDefined;
+static const NSEventMask NSSystemDefinedMask 		API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskSystemDefined", macosx(10.0, 10.12)) = NSEventMaskSystemDefined;
+static const NSEventMask NSApplicationDefinedMask 	API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskApplicationDefined", macosx(10.0, 10.12)) = NSEventMaskApplicationDefined;
+static const NSEventMask NSPeriodicMask 		API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskPeriodic", macosx(10.0, 10.12)) = NSEventMaskPeriodic;
+static const NSEventMask NSCursorUpdateMask 		API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskCursorUpdate", macosx(10.0, 10.12)) = NSEventMaskCursorUpdate;
+static const NSEventMask NSScrollWheelMask 		API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskScrollWheel", macosx(10.0, 10.12)) = NSEventMaskScrollWheel;
+static const NSEventMask NSTabletPointMask 		API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskTabletPoint", macosx(10.0, 10.12)) = NSEventMaskTabletPoint;
+static const NSEventMask NSTabletProximityMask	 	API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskTabletProximity", macosx(10.0, 10.12)) = NSEventMaskTabletProximity;
+static const NSEventMask NSOtherMouseDownMask 		API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskOtherMouseDown", macosx(10.0, 10.12)) = NSEventMaskOtherMouseDown;
+static const NSEventMask NSOtherMouseUpMask 		API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskOtherMouseUp", macosx(10.0, 10.12)) = NSEventMaskOtherMouseUp;
+static const NSEventMask NSOtherMouseDraggedMask 	API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskOtherMouseDragged", macosx(10.0, 10.12)) = NSEventMaskOtherMouseDragged;
+static const NSEventMask NSAnyEventMask			API_DEPRECATED_WITH_REPLACEMENT("NSEventMaskAny", macosx(10.0, 10.12)) = NSUIntegerMax;
 
 #if __LP64__
 NS_INLINE NSEventMask NSEventMaskFromType(NSEventType type) { return (1UL << type); }
@@ -114,32 +163,53 @@
 
 /* Device-independent bits found in event modifier flags */
 typedef NS_OPTIONS(NSUInteger, NSEventModifierFlags) {
-    NSAlphaShiftKeyMask         = 1 << 16,
-    NSShiftKeyMask              = 1 << 17,
-    NSControlKeyMask            = 1 << 18,
-    NSAlternateKeyMask          = 1 << 19,
-    NSCommandKeyMask            = 1 << 20,
-    NSNumericPadKeyMask         = 1 << 21,
-    NSHelpKeyMask               = 1 << 22,
-    NSFunctionKeyMask           = 1 << 23,
-    NSDeviceIndependentModifierFlagsMask    = 0xffff0000UL
+    NSEventModifierFlagCapsLock           = 1 << 16, // Set if Caps Lock key is pressed.
+    NSEventModifierFlagShift              = 1 << 17, // Set if Shift key is pressed.
+    NSEventModifierFlagControl            = 1 << 18, // Set if Control key is pressed.
+    NSEventModifierFlagOption             = 1 << 19, // Set if Option or Alternate key is pressed.
+    NSEventModifierFlagCommand            = 1 << 20, // Set if Command key is pressed.
+    NSEventModifierFlagNumericPad         = 1 << 21, // Set if any key in the numeric keypad is pressed.
+    NSEventModifierFlagHelp               = 1 << 22, // Set if the Help key is pressed.
+    NSEventModifierFlagFunction           = 1 << 23, // Set if any function key is pressed.
+    
+    // Used to retrieve only the device-independent modifier flags, allowing applications to mask off the device-dependent modifier flags, including event coalescing information.
+    NSEventModifierFlagDeviceIndependentFlagsMask    = 0xffff0000UL
 };
 
-/* pointer types for NSTabletProximity events or mouse events with subtype NSTabletProximityEventSubtype*/
+static const NSEventModifierFlags NSAlphaShiftKeyMask         API_DEPRECATED_WITH_REPLACEMENT("NSEventModifierFlagCapsLock", macosx(10.0, 10.12)) = NSEventModifierFlagCapsLock;
+static const NSEventModifierFlags NSShiftKeyMask              API_DEPRECATED_WITH_REPLACEMENT("NSEventModifierFlagShift", macosx(10.0, 10.12)) = NSEventModifierFlagShift;
+static const NSEventModifierFlags NSControlKeyMask            API_DEPRECATED_WITH_REPLACEMENT("NSEventModifierFlagControl", macosx(10.0, 10.12)) = NSEventModifierFlagControl;
+static const NSEventModifierFlags NSAlternateKeyMask          API_DEPRECATED_WITH_REPLACEMENT("NSEventModifierFlagOption", macosx(10.0, 10.12)) = NSEventModifierFlagOption;
+static const NSEventModifierFlags NSCommandKeyMask            API_DEPRECATED_WITH_REPLACEMENT("NSEventModifierFlagCommand", macosx(10.0, 10.12)) = NSEventModifierFlagCommand;
+static const NSEventModifierFlags NSNumericPadKeyMask         API_DEPRECATED_WITH_REPLACEMENT("NSEventModifierFlagNumericPad", macosx(10.0, 10.12)) = NSEventModifierFlagNumericPad;
+static const NSEventModifierFlags NSHelpKeyMask               API_DEPRECATED_WITH_REPLACEMENT("NSEventModifierFlagHelp", macosx(10.0, 10.12)) = NSEventModifierFlagHelp;
+static const NSEventModifierFlags NSFunctionKeyMask           API_DEPRECATED_WITH_REPLACEMENT("NSEventModifierFlagFunction", macosx(10.0, 10.12)) = NSEventModifierFlagFunction;
+static const NSEventModifierFlags NSDeviceIndependentModifierFlagsMask    API_DEPRECATED_WITH_REPLACEMENT("NSEventModifierFlagDeviceIndependentFlagsMask", macosx(10.0, 10.12)) = NSEventModifierFlagDeviceIndependentFlagsMask;
+
+/* pointer types for NSEventTypeTabletProximity events or mouse events with subtype NSEventSubtypeTabletProximity*/
 typedef NS_ENUM(NSUInteger, NSPointingDeviceType) {        
-    NSUnknownPointingDevice     = NX_TABLET_POINTER_UNKNOWN,
-    NSPenPointingDevice         = NX_TABLET_POINTER_PEN,
-    NSCursorPointingDevice      = NX_TABLET_POINTER_CURSOR,
-    NSEraserPointingDevice      = NX_TABLET_POINTER_ERASER
+    NSPointingDeviceTypeUnknown     = NX_TABLET_POINTER_UNKNOWN,
+    NSPointingDeviceTypePen         = NX_TABLET_POINTER_PEN,
+    NSPointingDeviceTypeCursor      = NX_TABLET_POINTER_CURSOR,
+    NSPointingDeviceTypeEraser      = NX_TABLET_POINTER_ERASER
 };
 
-/* button masks for NSTabletPoint events or mouse events with subtype NSTabletPointEventSubtype */
+static const NSPointingDeviceType NSUnknownPointingDevice     API_DEPRECATED_WITH_REPLACEMENT("NSPointingDeviceTypeUnknown", macosx(10.0, 10.12)) = NSPointingDeviceTypeUnknown;
+static const NSPointingDeviceType NSPenPointingDevice         API_DEPRECATED_WITH_REPLACEMENT("NSPointingDeviceTypePen", macosx(10.0, 10.12)) = NSPointingDeviceTypePen;
+static const NSPointingDeviceType NSCursorPointingDevice      API_DEPRECATED_WITH_REPLACEMENT("NSPointingDeviceTypeCursor", macosx(10.0, 10.12)) = NSPointingDeviceTypeCursor;
+static const NSPointingDeviceType NSEraserPointingDevice      API_DEPRECATED_WITH_REPLACEMENT("NSPointingDeviceTypeEraser", macosx(10.0, 10.12)) = NSPointingDeviceTypeEraser;
+
+/* button masks for NSEventTypeTabletPoint events or mouse events with subtype NSEventSubtypeTabletPoint */
 typedef NS_OPTIONS(NSUInteger, NSEventButtonMask) {
-    NSPenTipMask                = NX_TABLET_BUTTON_PENTIPMASK,
-    NSPenLowerSideMask          = NX_TABLET_BUTTON_PENLOWERSIDEMASK,
-    NSPenUpperSideMask          = NX_TABLET_BUTTON_PENUPPERSIDEMASK
+    NSEventButtonMaskPenTip                = NX_TABLET_BUTTON_PENTIPMASK,
+    NSEventButtonMaskPenLowerSide          = NX_TABLET_BUTTON_PENLOWERSIDEMASK,
+    NSEventButtonMaskPenUpperSide          = NX_TABLET_BUTTON_PENUPPERSIDEMASK
 };
 
+static const NSEventButtonMask NSPenTipMask                API_DEPRECATED_WITH_REPLACEMENT("NSEventButtonMaskPenTip", macosx(10.0, 10.12)) = NSEventButtonMaskPenTip;
+static const NSEventButtonMask NSPenLowerSideMask          API_DEPRECATED_WITH_REPLACEMENT("NSEventButtonMaskPenLowerSide", macosx(10.0, 10.12)) = NSEventButtonMaskPenLowerSide;
+static const NSEventButtonMask NSPenUpperSideMask          API_DEPRECATED_WITH_REPLACEMENT("NSEventButtonMaskPenUpperSide", macosx(10.0, 10.12)) = NSEventButtonMaskPenUpperSide;
+
 typedef NS_OPTIONS(NSUInteger, NSEventPhase) {
     NSEventPhaseNone        = 0, // event not associated with a phase.
     NSEventPhaseBegan       = 0x1 << 0,
@@ -162,24 +232,35 @@
 } NS_ENUM_AVAILABLE_MAC(10_7);
 
 typedef NS_ENUM(short, NSEventSubtype) {
-    /* event subtypes for NSAppKitDefined events */
-    NSWindowExposedEventType            = 0,
-    NSApplicationActivatedEventType     = 1,
-    NSApplicationDeactivatedEventType   = 2,
-    NSWindowMovedEventType              = 4,
-    NSScreenChangedEventType            = 8,
-    NSAWTEventType                      = 16,
+    /* event subtypes for NSEventTypeAppKitDefined events */
+    NSEventSubtypeWindowExposed            = 0,
+    NSEventSubtypeApplicationActivated     = 1,
+    NSEventSubtypeApplicationDeactivated   = 2,
+    NSEventSubtypeWindowMoved              = 4,
+    NSEventSubtypeScreenChanged            = 8,
     
-    /* event subtypes for NSSystemDefined events */
-    NSPowerOffEventType             = 1,
+    /* event subtypes for NSEventTypeSystemDefined events */
+    NSEventSubtypePowerOff             = 1,
     
     /* event subtypes for mouse events */
-    NSMouseEventSubtype             = NX_SUBTYPE_DEFAULT,
-    NSTabletPointEventSubtype       = NX_SUBTYPE_TABLET_POINT,
-    NSTabletProximityEventSubtype   = NX_SUBTYPE_TABLET_PROXIMITY,
-    NSTouchEventSubtype NS_ENUM_AVAILABLE_MAC(10_6)             = NX_SUBTYPE_MOUSE_TOUCH
+    NSEventSubtypeMouseEvent        = NX_SUBTYPE_DEFAULT,
+    NSEventSubtypeTabletPoint       = NX_SUBTYPE_TABLET_POINT,
+    NSEventSubtypeTabletProximity   = NX_SUBTYPE_TABLET_PROXIMITY,
+    NSEventSubtypeTouch  NS_ENUM_AVAILABLE_MAC(10_6)             = NX_SUBTYPE_MOUSE_TOUCH
 };
 
+static const NSEventSubtype NSWindowExposedEventType            API_DEPRECATED_WITH_REPLACEMENT("NSEventSubtypeWindowExposed", macosx(10.0, 10.12)) = NSEventSubtypeWindowExposed;
+static const NSEventSubtype NSApplicationActivatedEventType     API_DEPRECATED_WITH_REPLACEMENT("NSEventSubtypeApplicationActivated", macosx(10.0, 10.12)) = NSEventSubtypeApplicationActivated;
+static const NSEventSubtype NSApplicationDeactivatedEventType   API_DEPRECATED_WITH_REPLACEMENT("NSEventSubtypeApplicationDeactivated", macosx(10.0, 10.12)) = NSEventSubtypeApplicationDeactivated;
+static const NSEventSubtype NSWindowMovedEventType              API_DEPRECATED_WITH_REPLACEMENT("NSEventSubtypeWindowMoved", macosx(10.0, 10.12)) = NSEventSubtypeWindowMoved;
+static const NSEventSubtype NSScreenChangedEventType            API_DEPRECATED_WITH_REPLACEMENT("NSEventSubtypeScreenChanged", macosx(10.0, 10.12)) = NSEventSubtypeScreenChanged;
+static const NSEventSubtype NSAWTEventType                      NS_ENUM_DEPRECATED_MAC(10_10, 10_12, "This subtype no longer exists") = (NSEventSubtype)16;
+static const NSEventSubtype NSPowerOffEventType             API_DEPRECATED_WITH_REPLACEMENT("NSEventSubtypePowerOff", macosx(10.0, 10.12)) = NSEventSubtypePowerOff;
+static const NSEventSubtype NSMouseEventSubtype             API_DEPRECATED_WITH_REPLACEMENT("NSEventSubtypeMouseEvent", macosx(10.0, 10.12)) = NSEventSubtypeMouseEvent;
+static const NSEventSubtype NSTabletPointEventSubtype       API_DEPRECATED_WITH_REPLACEMENT("NSEventSubtypeTabletPoint", macosx(10.0, 10.12)) = NSEventSubtypeTabletPoint;
+static const NSEventSubtype NSTabletProximityEventSubtype   API_DEPRECATED_WITH_REPLACEMENT("NSEventSubtypeTabletProximity", macosx(10.0, 10.12)) = NSEventSubtypeTabletProximity;
+static const NSEventSubtype NSTouchEventSubtype             API_DEPRECATED_WITH_REPLACEMENT("NSEventSubtypeTouch", macosx(10.0, 10.12)) = NSEventSubtypeTouch;
+
 
 // NSPressureBehavior - The pressure gesture behavior that describes how a pressure gesture behaves and progresses
 // In general, pressure gestures begin when stage reaches 1 and end when stage reaches 0. This corresponds to the simultaneously generated mouse down/up events.
@@ -256,8 +337,8 @@
 #endif
         } mouse;
         struct {
-            NSString *keys;
-            NSString *unmodKeys;
+            __unsafe_unretained NSString *keys;
+            __unsafe_unretained NSString *unmodKeys;
             unsigned short keyCode;
             BOOL isARepeat;
 #if __LP64__
@@ -328,7 +409,7 @@
 @property (readonly) NSTimeInterval timestamp;
 @property (nullable, readonly, assign) NSWindow *window;
 @property (readonly) NSInteger windowNumber;
-@property (nullable, readonly, strong) NSGraphicsContext *context;
+@property (nullable, readonly, strong) NSGraphicsContext *context NS_DEPRECATED_MAC(10_0, 10_12, "This method always returns nil. If you need access to the current drawing context, use [NSGraphicsContext currentContext] inside of a draw operation.");
 
 /* these messages are valid for all mouse down/up/drag events */
 @property (readonly) NSInteger clickCount;
@@ -336,7 +417,7 @@
 /* these messages are valid for all mouse down/up/drag and enter/exit events */
 @property (readonly) NSInteger eventNumber;
 
-/* -pressure is valid for all mouse down/up/drag events, and is also valid for NSTabletPoint events on 10.4 or later and NSEventTypePressure on 10.10.3 or later */
+/* -pressure is valid for all mouse down/up/drag events, and is also valid for NSEventTypeTabletPoint events on 10.4 or later and NSEventTypePressure on 10.10.3 or later */
 @property (readonly) float pressure;
 /* -locationInWindow is valid for all mouse-related events */
 @property (readonly) NSPoint locationInWindow;
@@ -347,16 +428,16 @@
 @property (readonly) CGFloat deltaY;    
 @property (readonly) CGFloat deltaZ;    // 0 for most scroll wheel and mouse events
 
-/* This message is valid for NSScrollWheel events. A generic scroll wheel issues rather coarse scroll deltas. Some Apple mice and trackpads provide much more precise delta. This method determines the resolution of the scrollDeltaX and scrollDeltaY values.
+/* This message is valid for NSEventTypeScrollWheel events. A generic scroll wheel issues rather coarse scroll deltas. Some Apple mice and trackpads provide much more precise delta. This method determines the resolution of the scrollDeltaX and scrollDeltaY values.
 */
 @property (readonly) BOOL hasPreciseScrollingDeltas NS_AVAILABLE_MAC(10_7);
 
-/* The following two message are the preferred API for accessing NSScrollWheel deltas. When -hasPreciseScrollDeltas reutrns NO, multiply the returned value by line or row height. When -hasPreciseScrollDeltas returns YES, scroll by the returned value (in points). 
+/* The following two message are the preferred API for accessing NSEventTypeScrollWheel deltas. When -hasPreciseScrollDeltas reutrns NO, multiply the returned value by line or row height. When -hasPreciseScrollDeltas returns YES, scroll by the returned value (in points). 
 */
 @property (readonly) CGFloat scrollingDeltaX NS_AVAILABLE_MAC(10_7);
 @property (readonly) CGFloat scrollingDeltaY NS_AVAILABLE_MAC(10_7);
 
-/* This message is valid for NSScrollWheel events. With the Magic Mouse and some trackpads, the user can flick thier finger resulting in a stream of scroll events that dissipate over time. The location of these scroll wheel events changes as the user moves the cursor. AppKit latches these scroll wheel events to the view that is under the cursor when the flick occurs. A custom view can use this method to recognize these momentum scroll events and further route the event to the appropriate sub component.
+/* This message is valid for NSEventTypeScrollWheel events. With the Magic Mouse and some trackpads, the user can flick thier finger resulting in a stream of scroll events that dissipate over time. The location of these scroll wheel events changes as the user moves the cursor. AppKit latches these scroll wheel events to the view that is under the cursor when the flick occurs. A custom view can use this method to recognize these momentum scroll events and further route the event to the appropriate sub component.
 */
 @property (readonly) NSEventPhase momentumPhase NS_AVAILABLE_MAC(10_7);
 
@@ -412,13 +493,13 @@
 /* This message is valid for events of type NSEventTypeMagnify, on 10.5.2 or later */
 @property (readonly) CGFloat magnification NS_AVAILABLE_MAC(10_5);       // change in magnification.   This value should be added to the current scaling of an item to get the new scale factor.
 
-/* this message is valid for mouse events with subtype NSTabletPointEventSubtype or NSTabletProximityEventSubtype, and for NSTabletPoint and NSTabletProximity events */
+/* this message is valid for mouse events with subtype NSEventSubtypeTabletPoint or NSEventSubtypeTabletProximity, and for NSEventTypeTabletPoint and NSEventTypeTabletProximity events */
 @property (readonly) NSUInteger deviceID;
 
-/* this message is valid for valid for mouse events with subtype NSTabletPointEventSubtype, and for NSTabletPoint events.  On 10.5.2 or later, it is also valid for NSEventTypeRotate events. */
-@property (readonly) float rotation;       // In degrees.  For NSTabletPoint, this is rotation of the pen.  For NSEventTypeRotate, it is rotation on the track pad.
+/* this message is valid for valid for mouse events with subtype NSEventSubtypeTabletPoint, and for NSEventTypeTabletPoint events.  On 10.5.2 or later, it is also valid for NSEventTypeRotate events. */
+@property (readonly) float rotation;       // In degrees.  For NSEventTypeTabletPoint, this is rotation of the pen.  For NSEventTypeRotate, it is rotation on the track pad.
 
-/* these messages are valid for mouse events with subtype NSTabletPointEventSubtype, and for NSTabletPoint events */
+/* these messages are valid for mouse events with subtype NSEventSubtypeTabletPoint, and for NSEventTypeTabletPoint events */
 /* absolute x coordinate in tablet space at full tablet resolution */
 @property (readonly) NSInteger absoluteX; 
 /* absolute y coordinate in tablet space at full tablet resolution */
@@ -434,7 +515,7 @@
 /* NSArray of 3 vendor defined shorts */
 @property (readonly, strong) id vendorDefined;    
 
-/* these messages are valid for mouse events with subtype NSTabletProximityEventSubtype, and  for NSTabletProximity events */
+/* these messages are valid for mouse events with subtype NSEventSubtypeTabletProximity, and  for NSEventTypeTabletProximity events */
 /* vendor defined, typically USB vendor ID */
 @property (readonly) NSUInteger vendorID;
 /* vendor defined tablet ID */
@@ -460,7 +541,7 @@
 - (NSSet<NSTouch *> *)touchesMatchingPhase:(NSTouchPhase)phase inView:(nullable NSView *)view NS_AVAILABLE_MAC(10_6);
 
 /* The phase of a gesture scroll event. A gesture phrase are all the events that begin with a NSEventPhaseBegan and end with either a NSEventPhaseEnded or NSEventPhaseCancelled. All the gesture events are sent to the view under the cursor when the NSEventPhaseBegan occurred.  A gesture scroll event starts with a NSEventPhaseBegan phase and ends with a NSPhaseEnded. Legacy scroll wheel events (say from a Mighty Mouse) and momentum scroll wheel events have a phase of NSEventPhaseNone.
-    Valid for NSScrollWheel
+    Valid for NSEventTypeScrollWheel
 */
 @property (readonly) NSEventPhase phase NS_AVAILABLE_MAC(10_7);
 
@@ -502,10 +583,10 @@
 + (void)stopPeriodicEvents;
 
 /* apps will rarely create these objects */
-+ (nullable NSEvent *)mouseEventWithType:(NSEventType)type location:(NSPoint)location modifierFlags:(NSEventModifierFlags)flags timestamp:(NSTimeInterval)time windowNumber:(NSInteger)wNum context:(nullable NSGraphicsContext*)context eventNumber:(NSInteger)eNum clickCount:(NSInteger)cNum pressure:(float)pressure;
-+ (nullable NSEvent *)keyEventWithType:(NSEventType)type location:(NSPoint)location modifierFlags:(NSEventModifierFlags)flags timestamp:(NSTimeInterval)time windowNumber:(NSInteger)wNum context:(nullable NSGraphicsContext*)context characters:(NSString *)keys charactersIgnoringModifiers:(NSString *)ukeys isARepeat:(BOOL)flag keyCode:(unsigned short)code;
-+ (nullable NSEvent *)enterExitEventWithType:(NSEventType)type location:(NSPoint)location modifierFlags:(NSEventModifierFlags)flags timestamp:(NSTimeInterval)time windowNumber:(NSInteger)wNum context:(nullable NSGraphicsContext*)context eventNumber:(NSInteger)eNum trackingNumber:(NSInteger)tNum userData:(nullable void *)data;
-+ (nullable NSEvent *)otherEventWithType:(NSEventType)type location:(NSPoint)location modifierFlags:(NSEventModifierFlags)flags timestamp:(NSTimeInterval)time windowNumber:(NSInteger)wNum context:(nullable NSGraphicsContext*)context subtype:(short)subtype data1:(NSInteger)d1 data2:(NSInteger)d2;
++ (nullable NSEvent *)mouseEventWithType:(NSEventType)type location:(NSPoint)location modifierFlags:(NSEventModifierFlags)flags timestamp:(NSTimeInterval)time windowNumber:(NSInteger)wNum context:(nullable NSGraphicsContext* __unused)unusedPassNil eventNumber:(NSInteger)eNum clickCount:(NSInteger)cNum pressure:(float)pressure;
++ (nullable NSEvent *)keyEventWithType:(NSEventType)type location:(NSPoint)location modifierFlags:(NSEventModifierFlags)flags timestamp:(NSTimeInterval)time windowNumber:(NSInteger)wNum context:(nullable NSGraphicsContext* __unused)unusedPassNil characters:(NSString *)keys charactersIgnoringModifiers:(NSString *)ukeys isARepeat:(BOOL)flag keyCode:(unsigned short)code;
++ (nullable NSEvent *)enterExitEventWithType:(NSEventType)type location:(NSPoint)location modifierFlags:(NSEventModifierFlags)flags timestamp:(NSTimeInterval)time windowNumber:(NSInteger)wNum context:(nullable NSGraphicsContext* __unused)unusedPassNil eventNumber:(NSInteger)eNum trackingNumber:(NSInteger)tNum userData:(nullable void *)data;
++ (nullable NSEvent *)otherEventWithType:(NSEventType)type location:(NSPoint)location modifierFlags:(NSEventModifierFlags)flags timestamp:(NSTimeInterval)time windowNumber:(NSInteger)wNum context:(nullable NSGraphicsContext* __unused)unusedPassNil subtype:(short)subtype data1:(NSInteger)d1 data2:(NSInteger)d2;
 
 // global mouse coordinates
 + (NSPoint)mouseLocation;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFilePromiseProvider.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFilePromiseProvider.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFilePromiseProvider.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFilePromiseProvider.h	2016-06-03 05:13:45.000000000 +0200
@@ -0,0 +1,64 @@
+/*
+	NSFilePromiseProvider.h
+	Application Kit
+	Copyright (c) 2015-2016, Apple Inc.
+	All rights reserved.
+*/
+
+#import <Foundation/NSObject.h>
+#import <Foundation/NSArray.h>
+#import <Foundation/NSGeometry.h>
+#import <AppKit/AppKitDefines.h>
+#import <AppKit/NSPasteboard.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@protocol NSFilePromiseProviderDelegate;
+@class NSOperationQueue;
+
+NS_CLASS_AVAILABLE_MAC(10_12)
+@interface NSFilePromiseProvider : NSObject <NSPasteboardWriting> {
+@private
+    NSString *_fileType;
+    NSArray<NSString *> *_reservedA;
+    id <NSFilePromiseProviderDelegate> _delegate;
+    id _userInfo;
+    NSURL *_destinationURL;
+    struct {
+        unsigned int valid;
+        unsigned int reserved:31;
+    } _flags;
+    id _private __unused;
+}
+
+/* The UTI of the promised file type. An exception is thrown if the fileType does not conform to kUTTypeData or kUTTypeDirectory */
+@property(copy) NSString *fileType;
+
+/* Your object that is ultimately responsible for determining the final file name and writing the promised data to the destination. */
+@property(weak, nullable) id <NSFilePromiseProviderDelegate> delegate;
+
+/* When a simple string identifier is not enough. Store a pointer to an object that contains the source of the promised file data. */
+@property(strong, nullable) id userInfo;
+
+/* See fileType above for restrictions on the type of files to pass in */
+- (instancetype)initWithFileType:(NSString *)fileType delegate:(id <NSFilePromiseProviderDelegate>)delegate;
+
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
+@end
+
+
+@protocol NSFilePromiseProviderDelegate <NSObject>
+@required
+/* Return the base filename (not a full path) for this promise item. Do not start writing the file yet. */
+- (NSString *)filePromiseProvider:(NSFilePromiseProvider*)filePromiseProvider fileNameForDestination:(NSURL *)destinationURL;
+
+@optional
+/* Write the contents of this promise item to the provided URL and call completionHandler when done. NSFilePromiseReceiver automatically wraps this message with NSFileCoordinator when the promise destination is an NSFilePromiseReceiver. As such, the URL may be different than expected. Note: This request shall occur on the NSOperationQueue supplied by -promiseOperationQueue.
+ */
+- (void)filePromiseProvider:(NSFilePromiseProvider*)filePromiseProvider writePromiseToURL:(NSURL *)url completionHandler:(void (^)(NSError *errorOrNil))completionHandler;
+
+/* The operation queue that the write request will be issued from. If this method is not implemented, the mainOperationQueue is used. */
+- (NSOperationQueue *)promiseOperationQueueForFilePromiseProvider:(NSFilePromiseProvider*)filePromiseProvider;
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFilePromiseReceiver.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFilePromiseReceiver.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFilePromiseReceiver.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFilePromiseReceiver.h	2016-06-03 05:13:45.000000000 +0200
@@ -0,0 +1,61 @@
+/*
+	NSFilePromiseReceiver.h
+	Application Kit
+	Copyright (c) 2015-2016, Apple Inc.
+	All rights reserved.
+*/
+
+#import <Foundation/NSObject.h>
+#import <Foundation/NSArray.h>
+#import <Foundation/NSGeometry.h>
+#import <AppKit/AppKitDefines.h>
+#import <AppKit/NSPasteboard.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class NSOperationQueue;
+
+NS_CLASS_AVAILABLE_MAC(10_12)
+@interface NSFilePromiseReceiver : NSObject <NSPasteboardReading> {
+@private
+    NSPasteboard *_pasteboard;
+    NSPasteboardItem *_pasteboardItem;
+    NSArray<NSString*> *_fileTypes;
+    NSArray<NSString *> *_reservedA;
+    NSArray<NSString*> *_fileNames;
+    NSArray<NSURL*> *_fileURLs;
+    NSOperationQueue *_operationQueue;
+    NSInteger _promiseType;
+    void (^_readerBlock)(NSURL *, NSError * __nullable);
+    struct {
+        unsigned int usesFileCoordniation:1;
+        unsigned int registered:1;
+        unsigned int reserved:30;
+    } _flags;
+    id _private __unused;
+}
+
+/* A view must register what types it accepts via -registerForDraggedTypes:. Use this class method to get the file promise drag types that NSFilePromiseReceiver can accept, in order to register a view to accept promised files.
+ */
++ (NSArray<NSString *> *)readableDraggedTypes;
+
+/* The UTI of the file types promised (Note: The count of fileTypes should tell you the number of promised files, however, that is not guaranteed. Historically, some legacy file promisers only list each unique fileType once and write one or more files per type.
+ */
+@property(copy, readonly) NSArray<NSString*> *fileTypes;
+
+/* The file names of the promised files that are being written to the destination location. Note: This property returns an empty array until the file promise is called in via receivePromisedFilesAtDestination.
+ Note: This is an array, because legacy promises are an array of files on one pasteboard item.
+ */
+@property(copy, readonly) NSArray<NSString*> *fileNames;
+
+/* This effectively calls in the promises. Therefore, only call once you are accepting the file promise.
+ All file promisesReceiver's in a drag must specify the same destination location.
+ This is an array, because legacy promises are an array of files on one pasteboard item.
+ The reader block is called on the supplied operationQueue when the promised file is ready to be read. When the source is an NSFilePromiseProvider, the readerBlock call is wrapped in an NSFileCoordination read. Otherwise, a heuristic is used to determine when the promised file is ready to be read.
+ The options dictionary is ignored for now.
+ Note: Writing of the promised file may fail. When that occurs, the readerBlock is still called, but there may be nothing at the fileURL, or it may be a partial / corrupt file.
+ */
+- (void)receivePromisedFilesAtDestination:(NSURL *)destinationDir options:(NSDictionary *)options operationQueue:(NSOperationQueue *)operationQueue reader:(void(^)(NSURL *fileURL, NSError * __nullable errorOrNil))reader;
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFileWrapper.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFileWrapper.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFileWrapper.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFileWrapper.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSFileWrapper.h
         Application Kit
-        Copyright (c) 1995-2015, Apple Inc.
+        Copyright (c) 1995-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFileWrapperExtensions.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFileWrapperExtensions.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFileWrapperExtensions.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFileWrapperExtensions.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSFileWrapperExtensions.h
 	Application Kit
-	Copyright (c) 2002-2015, Apple Inc.
+	Copyright (c) 2002-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFont.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFont.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFont.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFont.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSFont.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -78,8 +78,8 @@
 */
 + (nullable NSFont *)userFontOfSize:(CGFloat)fontSize;	// Application font
 + (nullable NSFont *)userFixedPitchFontOfSize:(CGFloat)fontSize; // fixed-pitch font
-+ (void)setUserFont:(nullable NSFont *)aFont;	// set preference for Application font.
-+ (void)setUserFixedPitchFont:(nullable NSFont *)aFont; // set preference for fixed-pitch.
++ (void)setUserFont:(nullable NSFont *)font;	// set preference for Application font.
++ (void)setUserFixedPitchFont:(nullable NSFont *)font; // set preference for fixed-pitch.
 
 /* UI font settings
 */
@@ -120,7 +120,7 @@
 /********* Glyph coverage *********/
 @property (readonly) NSUInteger numberOfGlyphs;
 @property (readonly) NSStringEncoding mostCompatibleStringEncoding;
-- (NSGlyph)glyphWithName:(NSString *)aName;
+- (NSGlyph)glyphWithName:(NSString *)name;
 @property (readonly, strong) NSCharacterSet *coveredCharacterSet;
 
 /********* Font instance-wide metrics *********/
@@ -141,8 +141,8 @@
 @property (getter=isFixedPitch, readonly) BOOL fixedPitch;
 
 /********* Glyph metrics *********/
-- (NSRect)boundingRectForGlyph:(NSGlyph)aGlyph;
-- (NSSize)advancementForGlyph:(NSGlyph)ag;
+- (NSRect)boundingRectForGlyph:(NSGlyph)glyph;
+- (NSSize)advancementForGlyph:(NSGlyph)glyph;
 
 // bulk query
 - (void)getBoundingRects:(NSRectArray)bounds forGlyphs:(const NSGlyph *)glyphs count:(NSUInteger)glyphCount;
@@ -210,7 +210,7 @@
 - (CGFloat)widthOfString:(null_unspecified NSString *)string NS_DEPRECATED_MAC(10_0, 10_4); // This API never returns correct value. Use NSStringDrawing API instead.
 - (BOOL)isBaseFont NS_DEPRECATED_MAC(10_0, 10_4);
 - (null_unspecified NSDictionary *)afmDictionary NS_DEPRECATED_MAC(10_0, 10_4);
-- (BOOL)glyphIsEncoded:(NSGlyph)aGlyph NS_DEPRECATED_MAC(10_0, 10_4); // Can be deduced by aGlyph < [NSFont numberOfGlyphs] since only NSNativeShortGlyphPacking is supported.
+- (BOOL)glyphIsEncoded:(NSGlyph)glyph NS_DEPRECATED_MAC(10_0, 10_4); // Can be deduced by aGlyph < [NSFont numberOfGlyphs] since only NSNativeShortGlyphPacking is supported.
 - (CGFloat)defaultLineHeightForFont NS_DEPRECATED_MAC(10_0, 10_4); // Use -[NSLayoutManager defaultLineHeightForFont:] instead.
 + (null_unspecified NSArray *)preferredFontNames NS_DEPRECATED_MAC(10_0, 10_4); // NSFontCascadeListAttribute offers more powerful font substitution management
 + (void)setPreferredFontNames:(null_unspecified NSArray *)fontNameArray NS_DEPRECATED_MAC(10_0, 10_4);
@@ -219,11 +219,11 @@
 
 NS_ASSUME_NONNULL_BEGIN
 // The context-sensitive inter-glyph spacing is now performed at the typesetting stage.
-- (NSPoint)positionOfGlyph:(NSGlyph)curGlyph precededByGlyph:(NSGlyph)prevGlyph isNominal:(null_unspecified BOOL *)nominal NS_DEPRECATED_MAC(10_0, 10_4);
+- (NSPoint)positionOfGlyph:(NSGlyph)glyph precededByGlyph:(NSGlyph)prevGlyph isNominal:(null_unspecified BOOL *)nominal NS_DEPRECATED_MAC(10_0, 10_4);
 - (NSInteger)positionsForCompositeSequence:(null_unspecified NSGlyph *)someGlyphs numberOfGlyphs:(NSInteger)numGlyphs pointArray:(NSPointArray)points NS_DEPRECATED_MAC(10_0, 10_4);
-- (NSPoint)positionOfGlyph:(NSGlyph)curGlyph struckOverGlyph:(NSGlyph)prevGlyph metricsExist:(null_unspecified BOOL *)exist NS_DEPRECATED_MAC(10_0, 10_4);
-- (NSPoint)positionOfGlyph:(NSGlyph)aGlyph struckOverRect:(NSRect)aRect metricsExist:(null_unspecified BOOL *)exist NS_DEPRECATED_MAC(10_0, 10_4);
-- (NSPoint)positionOfGlyph:(NSGlyph)aGlyph forCharacter:(unichar)aChar struckOverRect:(NSRect)aRect NS_DEPRECATED_MAC(10_0, 10_4);
+- (NSPoint)positionOfGlyph:(NSGlyph)glyph struckOverGlyph:(NSGlyph)prevGlyph metricsExist:(null_unspecified BOOL *)exist NS_DEPRECATED_MAC(10_0, 10_4);
+- (NSPoint)positionOfGlyph:(NSGlyph)glyph struckOverRect:(NSRect)rect metricsExist:(null_unspecified BOOL *)exist NS_DEPRECATED_MAC(10_0, 10_4);
+- (NSPoint)positionOfGlyph:(NSGlyph)glyph forCharacter:(unichar)character struckOverRect:(NSRect)rect NS_DEPRECATED_MAC(10_0, 10_4);
 - (NSPoint)positionOfGlyph:(NSGlyph)thisGlyph withRelation:(NSGlyphRelation)rel toBaseGlyph:(NSGlyph)baseGlyph totalAdvancement:(NSSizePointer)adv metricsExist:(null_unspecified BOOL *)exist NS_DEPRECATED_MAC(10_0, 10_4);
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFontCollection.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFontCollection.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFontCollection.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFontCollection.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSFontCollection.h
 	Application Kit
-	Copyright (c) 2010-2015, Apple Inc.
+	Copyright (c) 2010-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFontDescriptor.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFontDescriptor.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFontDescriptor.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFontDescriptor.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSFontDescriptor.h
 	Application Kit
-	Copyright (c) 2003-2015, Apple Inc.
+	Copyright (c) 2003-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -77,7 +77,7 @@
 @property (nullable, readonly, copy) NSAffineTransform *matrix;
 @property (readonly) NSFontSymbolicTraits symbolicTraits;
 
-- (nullable id)objectForKey:(NSString *)anAttribute;
+- (nullable id)objectForKey:(NSString *)attribute;
 
 @property (readonly, copy) NSDictionary<NSString *, id> *fontAttributes;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFontManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFontManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFontManager.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFontManager.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSFontManager.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -61,7 +61,9 @@
 /*All instance variables are private*/
 @private
     NSFontPanel * _panel;
+#ifndef __OBJC2__
     unsigned int _fmReserved1;
+#endif
     SEL _action;
     id _actionOrigin;
     id _target;
@@ -72,11 +74,15 @@
         unsigned int senderTagMode:2;
 	unsigned int _RESERVED:12;
     } _fmFlags;
+#ifndef __OBJC2__
     unsigned short _fmReserved3;
+#endif
     id _delegate;
     id _collections;
+#ifndef __OBJC2__
     id _hiddenCollections;
     NSUInteger _fmReserved4;
+#endif
 }
 
 + (void)setFontPanelFactory:(nullable Class)factoryId;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFontPanel.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFontPanel.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFontPanel.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFontPanel.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSFontPanel.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -87,8 +87,11 @@
     id _fontEffectsBox;
     int _sizeStyle;
 
+    id _fontPanelToolbar;
+    id _fontPanelContentView;
+
 #if !__LP64__
-    id _fpUnused[72];
+    id _fpUnused[70];
 #endif /* !__LP64__ */
 }
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSForm.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSForm.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSForm.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSForm.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSForm.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -28,7 +28,7 @@
 - (NSFormCell *)addEntry:(NSString *)title;
 - (null_unspecified NSFormCell *)insertEntry:(NSString *)title atIndex:(NSInteger)index;
 - (void)removeEntryAtIndex:(NSInteger)index;
-- (NSInteger)indexOfCellWithTag:(NSInteger)aTag;
+- (NSInteger)indexOfCellWithTag:(NSInteger)tag;
 - (void)selectTextAtIndex:(NSInteger)index;
 - (void)setFrameSize:(NSSize)newSize;
 - (void)setTitleBaseWritingDirection:(NSWritingDirection)writingDirection;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFormCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFormCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFormCell.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFormCell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSFormCell.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -20,9 +20,11 @@
 #endif
 }
 
-- (instancetype)initTextCell:(nullable NSString *)aString;
+- (instancetype)initTextCell:(nullable NSString *)string NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
+- (instancetype)initImageCell:(nullable NSImage *)image NS_UNAVAILABLE;
 
-- (CGFloat)titleWidth:(NSSize)aSize;
+- (CGFloat)titleWidth:(NSSize)size;
 @property CGFloat titleWidth;
 @property (copy) NSString *title;
 @property (strong) NSFont *titleFont;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGestureRecognizer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGestureRecognizer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGestureRecognizer.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGestureRecognizer.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSGestureRecognizer.h
     Application Kit
-    Copyright (c) 2013-2015, Apple Inc.
+    Copyright (c) 2013-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -32,12 +32,12 @@
 @interface NSGestureRecognizer : NSObject <NSCoding> {
   @private
     NSMutableArray                   *_targets;
-    __weak id                        _target;
-    SEL                              _action;
+    id                                _target;
+    SEL                               _action;
     NSMutableArray                   *_delayedEvents;
-    __weak NSView                    *_view;
+    NSView                           *_view;
     NSEvent                          *_updateEvent;
-    __weak id <NSGestureRecognizerDelegate>  _delegate;
+    id <NSGestureRecognizerDelegate>  _delegate;
     NSMutableSet                     *_friends;
     NSGestureRecognizerState          _state;
     NSUInteger                        _gestureFlags;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGlyphGenerator.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGlyphGenerator.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGlyphGenerator.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGlyphGenerator.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSGlyphGenerator.h
         Application Kit
-        Copyright (c) 1993-2015, Apple Inc.
+        Copyright (c) 1993-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGlyphInfo.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGlyphInfo.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGlyphInfo.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGlyphInfo.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,6 +1,6 @@
 /*	
 	NSGlyphInfo.h
-	Copyright (c) 2002-2015, Apple Inc.
+	Copyright (c) 2002-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -23,13 +23,13 @@
 }
 
 // Returns an NSGlyphInfo object for the glyph name such as "copyright."
-+ (nullable NSGlyphInfo *)glyphInfoWithGlyphName:(NSString *)glyphName forFont:(NSFont *)font baseString:(NSString *)theString;
++ (nullable NSGlyphInfo *)glyphInfoWithGlyphName:(NSString *)glyphName forFont:(NSFont *)font baseString:(NSString *)string;
 
 // Returns an NSGlyphInfo object for the NSGlyph glyph
-+ (nullable NSGlyphInfo *)glyphInfoWithGlyph:(NSGlyph)glyph forFont:(NSFont *)font baseString:(NSString *)theString;
++ (nullable NSGlyphInfo *)glyphInfoWithGlyph:(NSGlyph)glyph forFont:(NSFont *)font baseString:(NSString *)string;
 
 // Returns an NSGlyphInfo object for the CID/RO
-+ (nullable NSGlyphInfo *)glyphInfoWithCharacterIdentifier:(NSUInteger)cid collection:(NSCharacterCollection)characterCollection baseString:(NSString *)theString;
++ (nullable NSGlyphInfo *)glyphInfoWithCharacterIdentifier:(NSUInteger)cid collection:(NSCharacterCollection)characterCollection baseString:(NSString *)string;
 
 // Returns the glyph name.  If the receiver is instantiated without glyph name, returns nil
 @property (nullable, readonly, copy) NSString *glyphName;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGradient.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGradient.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGradient.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGradient.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSGradient.h
 	Application Kit
-	Copyright (c) 2006-2015, Apple Inc.
+	Copyright (c) 2006-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -15,9 +15,7 @@
 
 @class NSBezierPath, NSColor, NSColorSpace;
 
-typedef NSUInteger NSGradientDrawingOptions;
-
-enum {
+typedef NS_OPTIONS(NSUInteger, NSGradientDrawingOptions) {
     NSGradientDrawsBeforeStartingLocation =   (1 << 0),
     NSGradientDrawsAfterEndingLocation =    (1 << 1),
 };
@@ -53,11 +51,11 @@
 @private
     NSArray *_colorArray;
     NSColorSpace *_colorSpace;
-    __strong void *_functionRef;
+    void *_functionRef;
     void *_componentArray;
-    void *_reserved1;
-    void *_reserved2;
-    void *_reserved3;
+    void *_reserved1 __unused;
+    void *_reserved2 __unused;
+    void *_reserved3 __unused;
 }
 
 
@@ -82,7 +80,9 @@
 
 /* Initializes a gradient by pairing the colors provided in the color array with the locations provided in the locations array.    Each location should be a CGFloat between 0.0 and 1.0.  The color array and location array should not be empty, and should contain the same number of items.  If no color is provided for 0.0 or 1.0, the created color gradient will use the color provided at the locations closest to 0.0 and 1.0 for those values.  This is the designated initializer.
 */
-- (nullable instancetype)initWithColors:(NSArray<NSColor *> *)colorArray atLocations:(nullable const CGFloat *)locations colorSpace:(NSColorSpace *)colorSpace;
+- (nullable instancetype)initWithColors:(NSArray<NSColor *> *)colorArray atLocations:(nullable const CGFloat *)locations colorSpace:(NSColorSpace *)colorSpace NS_DESIGNATED_INITIALIZER;
+
+- (instancetype)initWithCoder:(NSCoder *)decoder NS_DESIGNATED_INITIALIZER;
 
 
 /* DRAWING LINEAR GRADIENTS */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGraphics.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGraphics.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGraphics.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGraphics.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSGraphics.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -18,44 +18,78 @@
 typedef NS_ENUM(NSUInteger, NSCompositingOperation) {
     /* Porter-Duff compositing operations */
     /* http://www.w3.org/TR/2014/CR-compositing-1-20140220/#porterduffcompositingoperators */
-    NSCompositeClear,		
-    NSCompositeCopy,		
-    NSCompositeSourceOver,	
-    NSCompositeSourceIn,	
-    NSCompositeSourceOut,	
-    NSCompositeSourceAtop,	
-    NSCompositeDestinationOver,	
-    NSCompositeDestinationIn,	
-    NSCompositeDestinationOut,	
-    NSCompositeDestinationAtop,	
-    NSCompositeXOR,		
-    NSCompositePlusDarker,
-    NSCompositeHighlight	NS_DEPRECATED_MAC(10_0, 10_0, "Use NSCompositeSourceOver instead"),
-    NSCompositePlusLighter,
+    NSCompositingOperationClear,
+    NSCompositingOperationCopy,		
+    NSCompositingOperationSourceOver,	
+    NSCompositingOperationSourceIn,	
+    NSCompositingOperationSourceOut,	
+    NSCompositingOperationSourceAtop,	
+    NSCompositingOperationDestinationOver,	
+    NSCompositingOperationDestinationIn,	
+    NSCompositingOperationDestinationOut,	
+    NSCompositingOperationDestinationAtop,	
+    NSCompositingOperationXOR,		
+    NSCompositingOperationPlusDarker,
+    NSCompositingOperationHighlight NS_DEPRECATED_MAC(10_0, 10_0, "Use NSCompositingOperationSourceOver instead"),
+    NSCompositingOperationPlusLighter,
     
     /* Separable blend-modes */
     /* http://www.w3.org/TR/2014/CR-compositing-1-20140220/#blendingseparable */
-    NSCompositeMultiply		NS_AVAILABLE_MAC(10_10),
-    NSCompositeScreen		NS_AVAILABLE_MAC(10_10),
-    NSCompositeOverlay		NS_AVAILABLE_MAC(10_10),
-    NSCompositeDarken		NS_AVAILABLE_MAC(10_10),
-    NSCompositeLighten		NS_AVAILABLE_MAC(10_10),
-    NSCompositeColorDodge	NS_AVAILABLE_MAC(10_10),
-    NSCompositeColorBurn	NS_AVAILABLE_MAC(10_10),
-    NSCompositeSoftLight	NS_AVAILABLE_MAC(10_10),
-    NSCompositeHardLight	NS_AVAILABLE_MAC(10_10),
-    NSCompositeDifference	NS_AVAILABLE_MAC(10_10),
-    NSCompositeExclusion	NS_AVAILABLE_MAC(10_10),
+    NSCompositingOperationMultiply	NS_AVAILABLE_MAC(10_10),
+    NSCompositingOperationScreen	NS_AVAILABLE_MAC(10_10),
+    NSCompositingOperationOverlay	NS_AVAILABLE_MAC(10_10),
+    NSCompositingOperationDarken	NS_AVAILABLE_MAC(10_10),
+    NSCompositingOperationLighten	NS_AVAILABLE_MAC(10_10),
+    NSCompositingOperationColorDodge	NS_AVAILABLE_MAC(10_10),
+    NSCompositingOperationColorBurn	NS_AVAILABLE_MAC(10_10),
+    NSCompositingOperationSoftLight	NS_AVAILABLE_MAC(10_10),
+    NSCompositingOperationHardLight	NS_AVAILABLE_MAC(10_10),
+    NSCompositingOperationDifference	NS_AVAILABLE_MAC(10_10),
+    NSCompositingOperationExclusion	NS_AVAILABLE_MAC(10_10),
     
     /* Non-separable blend-modes */
     /* http://www.w3.org/TR/2014/CR-compositing-1-20140220/#blendingnonseparable */
-    NSCompositeHue		NS_AVAILABLE_MAC(10_10),
-    NSCompositeSaturation	NS_AVAILABLE_MAC(10_10),
-    NSCompositeColor		NS_AVAILABLE_MAC(10_10),
-    NSCompositeLuminosity	NS_AVAILABLE_MAC(10_10),
+    NSCompositingOperationHue		NS_AVAILABLE_MAC(10_10),
+    NSCompositingOperationSaturation	NS_AVAILABLE_MAC(10_10),
+    NSCompositingOperationColor		NS_AVAILABLE_MAC(10_10),
+    NSCompositingOperationLuminosity	NS_AVAILABLE_MAC(10_10),
 };
 
 
+static const NSCompositingOperation NSCompositeClear API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationClear", macosx(10.0, 10.12)) = NSCompositingOperationClear;
+static const NSCompositingOperation NSCompositeCopy API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationCopy", macosx(10.0, 10.12)) = NSCompositingOperationCopy;
+static const NSCompositingOperation NSCompositeSourceOver API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationSourceOver", macosx(10.0, 10.12)) = NSCompositingOperationSourceOver;
+static const NSCompositingOperation NSCompositeSourceIn API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationSourceIn", macosx(10.0, 10.12)) = NSCompositingOperationSourceIn;
+static const NSCompositingOperation NSCompositeSourceOut API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationSourceOut", macosx(10.0, 10.12)) = NSCompositingOperationSourceOut;
+static const NSCompositingOperation NSCompositeSourceAtop API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationSourceAtop", macosx(10.0, 10.12)) = NSCompositingOperationSourceAtop;
+static const NSCompositingOperation NSCompositeDestinationOver API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationDestinationOver", macosx(10.0, 10.12)) = NSCompositingOperationDestinationOver;
+static const NSCompositingOperation NSCompositeDestinationIn API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationDestinationIn", macosx(10.0, 10.12)) = NSCompositingOperationDestinationIn;
+static const NSCompositingOperation NSCompositeDestinationOut API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationDestinationOut", macosx(10.0, 10.12)) = NSCompositingOperationDestinationOut;
+static const NSCompositingOperation NSCompositeDestinationAtop API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationDestinationAtop", macosx(10.0, 10.12)) = NSCompositingOperationDestinationAtop;
+static const NSCompositingOperation NSCompositeXOR API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationXOR", macosx(10.0, 10.12)) = NSCompositingOperationXOR;
+static const NSCompositingOperation NSCompositePlusDarker API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationPlusDarker", macosx(10.0, 10.12)) = NSCompositingOperationPlusDarker;
+static const NSCompositingOperation NSCompositeHighlight NS_DEPRECATED_MAC(10_0, 10_0, "Use NSCompositingOperationHighlight instead") = NSCompositingOperationHighlight;
+static const NSCompositingOperation NSCompositePlusLighter API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationPlusLighter", macosx(10.0, 10.12)) = NSCompositingOperationPlusLighter;
+static const NSCompositingOperation NSCompositeMultiply	API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationMultiply", macosx(10.0, 10.12)) = NSCompositingOperationMultiply;
+static const NSCompositingOperation NSCompositeScreen API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationScreen", macosx(10.0, 10.12)) = NSCompositingOperationScreen;
+static const NSCompositingOperation NSCompositeOverlay API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationOverlay", macosx(10.0, 10.12)) = NSCompositingOperationOverlay;
+static const NSCompositingOperation NSCompositeDarken API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationDarken", macosx(10.0, 10.12)) = NSCompositingOperationDarken;
+static const NSCompositingOperation NSCompositeLighten API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationLighten", macosx(10.0, 10.12)) = NSCompositingOperationLighten;
+static const NSCompositingOperation NSCompositeColorDodge API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationColorDodge", macosx(10.0, 10.12)) = NSCompositingOperationColorDodge;
+static const NSCompositingOperation NSCompositeColorBurn API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationColorBurn", macosx(10.0, 10.12)) = NSCompositingOperationColorBurn;
+static const NSCompositingOperation NSCompositeSoftLight API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationSoftLight", macosx(10.0, 10.12)) = NSCompositingOperationSoftLight;
+static const NSCompositingOperation NSCompositeHardLight API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationHardLight", macosx(10.0, 10.12)) = NSCompositingOperationHardLight;
+static const NSCompositingOperation NSCompositeDifference API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationDifference", macosx(10.0, 10.12)) = NSCompositingOperationDifference;
+static const NSCompositingOperation NSCompositeExclusion API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationExclusion", macosx(10.0, 10.12)) = NSCompositingOperationExclusion;
+
+static const NSCompositingOperation NSCompositeHue API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationHue", macosx(10.0, 10.12)) = NSCompositingOperationHue;
+static const NSCompositingOperation NSCompositeSaturation API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationSaturation", macosx(10.0, 10.12)) = NSCompositingOperationSaturation;
+static const NSCompositingOperation NSCompositeColor API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationColor", macosx(10.0, 10.12)) = NSCompositingOperationColor;
+static const NSCompositingOperation NSCompositeLuminosity API_DEPRECATED_WITH_REPLACEMENT("NSCompositingOperationLuminosity", macosx(10.0, 10.12)) = NSCompositingOperationLuminosity;
+
+
+
+
 /* types of window backing store */
 typedef NS_ENUM(NSUInteger, NSBackingStoreType) {
     NSBackingStoreRetained	 = 0,
@@ -155,39 +189,39 @@
 
 /* Graphics functions
 */
-APPKIT_EXTERN void NSRectFill(NSRect aRect);
+APPKIT_EXTERN void NSRectFill(NSRect rect);
 APPKIT_EXTERN void NSRectFillList(const NSRect *rects, NSInteger count);
 APPKIT_EXTERN void NSRectFillListWithGrays(const NSRect *rects, const CGFloat *grays, NSInteger num);
 APPKIT_EXTERN void NSRectFillListWithColors(const NSRect *rects,  NSColor * const __nonnull * __nonnull colors, NSInteger num);
-APPKIT_EXTERN void NSRectFillUsingOperation(NSRect aRect, NSCompositingOperation op);
+APPKIT_EXTERN void NSRectFillUsingOperation(NSRect rect, NSCompositingOperation op);
 APPKIT_EXTERN void NSRectFillListUsingOperation(const NSRect *rects, NSInteger count, NSCompositingOperation op);
 APPKIT_EXTERN void NSRectFillListWithColorsUsingOperation(const NSRect *rects, NSColor * const __nonnull * __nonnull colors, NSInteger num, NSCompositingOperation op);
-APPKIT_EXTERN void NSFrameRect(NSRect aRect);
-APPKIT_EXTERN void NSFrameRectWithWidth(NSRect aRect, CGFloat frameWidth);
-APPKIT_EXTERN void NSFrameRectWithWidthUsingOperation(NSRect aRect, CGFloat frameWidth, NSCompositingOperation op);
-APPKIT_EXTERN void NSRectClip(NSRect aRect);
+APPKIT_EXTERN void NSFrameRect(NSRect rect);
+APPKIT_EXTERN void NSFrameRectWithWidth(NSRect rect, CGFloat frameWidth);
+APPKIT_EXTERN void NSFrameRectWithWidthUsingOperation(NSRect rect, CGFloat frameWidth, NSCompositingOperation op);
+APPKIT_EXTERN void NSRectClip(NSRect rect);
 APPKIT_EXTERN void NSRectClipList(const NSRect *rects, NSInteger count);
 APPKIT_EXTERN NSRect NSDrawTiledRects(NSRect boundsRect, NSRect clipRect, const NSRectEdge *sides, const CGFloat *grays, NSInteger count);
-APPKIT_EXTERN void NSDrawGrayBezel(NSRect aRect, NSRect clipRect);
-APPKIT_EXTERN void NSDrawGroove(NSRect aRect, NSRect clipRect);
-APPKIT_EXTERN void NSDrawWhiteBezel(NSRect aRect, NSRect clipRect);
-APPKIT_EXTERN void NSDrawButton(NSRect aRect, NSRect clipRect);
-APPKIT_EXTERN void NSEraseRect(NSRect aRect);
+APPKIT_EXTERN void NSDrawGrayBezel(NSRect rect, NSRect clipRect);
+APPKIT_EXTERN void NSDrawGroove(NSRect rect, NSRect clipRect);
+APPKIT_EXTERN void NSDrawWhiteBezel(NSRect rect, NSRect clipRect);
+APPKIT_EXTERN void NSDrawButton(NSRect rect, NSRect clipRect);
+APPKIT_EXTERN void NSEraseRect(NSRect rect);
 APPKIT_EXTERN NSColor * __nullable NSReadPixel(NSPoint passedPoint);
 APPKIT_EXTERN void NSDrawBitmap(NSRect rect, NSInteger width, NSInteger height, NSInteger bps, NSInteger spp, NSInteger bpp, NSInteger bpr, BOOL isPlanar, BOOL hasAlpha, NSString *colorSpaceName, const unsigned char *const __nullable data[5]);
 
-APPKIT_EXTERN void NSHighlightRect(NSRect aRect) NS_DEPRECATED_MAC(10_0, 10_0);
+APPKIT_EXTERN void NSHighlightRect(NSRect rect) NS_DEPRECATED_MAC(10_0, 10_0);
 APPKIT_EXTERN void NSBeep(void);
 
 /* gets performance stats about window server memory usage */
 APPKIT_EXTERN NSInteger NSGetWindowServerMemory(NSInteger context, NSInteger *virtualMemory, NSInteger *windowBackingMemory,   NSString * __nonnull * __nonnull windowDumpString); // Deprecated; doesn't return anything useful (as of 10.0)
 
 APPKIT_EXTERN NSRect NSDrawColorTiledRects(NSRect boundsRect, NSRect clipRect, const NSRectEdge *sides, NSColor * __nonnull * __nonnull colors, NSInteger count);
-APPKIT_EXTERN void NSDrawDarkBezel(NSRect aRect, NSRect clipRect);
-APPKIT_EXTERN void NSDrawLightBezel(NSRect aRect, NSRect clipRect);
-APPKIT_EXTERN void NSDottedFrameRect(NSRect aRect);
+APPKIT_EXTERN void NSDrawDarkBezel(NSRect rect, NSRect clipRect);
+APPKIT_EXTERN void NSDrawLightBezel(NSRect rect, NSRect clipRect);
+APPKIT_EXTERN void NSDottedFrameRect(NSRect rect);
 
-APPKIT_EXTERN void NSDrawWindowBackground(NSRect aRect);
+APPKIT_EXTERN void NSDrawWindowBackground(NSRect rect);
 APPKIT_EXTERN void NSSetFocusRingStyle(NSFocusRingPlacement placement);
 
 /* Disable and reenable screen updates.  
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGraphicsContext.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGraphicsContext.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGraphicsContext.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGraphicsContext.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSGraphicsContext.h
         Application Kit
-        Copyright (c) 1997-2015, Apple Inc.
+        Copyright (c) 1997-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGridView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGridView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGridView.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGridView.h	2016-06-03 05:13:45.000000000 +0200
@@ -0,0 +1,225 @@
+/*
+	NSGridView.h
+	Application Kit
+	Copyright (c) 2015-2016, Apple Inc.
+	All rights reserved.
+ */
+
+
+#import <AppKit/NSView.h>
+#import <AppKit/NSLayoutAnchor.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class NSLayoutConstraint, NSGridCell, NSGridColumn, NSGridRow;
+
+
+typedef NS_ENUM(NSInteger, NSGridCellPlacement) {
+    NSGridCellPlacementInherited = 0,
+    NSGridCellPlacementNone,
+    NSGridCellPlacementLeading,
+    NSGridCellPlacementTop = NSGridCellPlacementLeading,
+    
+    NSGridCellPlacementTrailing,
+    NSGridCellPlacementBottom = NSGridCellPlacementTrailing,
+    
+    NSGridCellPlacementCenter,
+    NSGridCellPlacementFill
+    
+} NS_ENUM_AVAILABLE_MAC(10_12);
+
+
+typedef NS_ENUM(NSInteger, NSGridRowAlignment) {
+    NSGridRowAlignmentInherited = 0,
+    NSGridRowAlignmentNone,
+    NSGridRowAlignmentFirstBaseline,
+    NSGridRowAlignmentLastBaseline
+} NS_ENUM_AVAILABLE_MAC(10_12);
+
+APPKIT_EXTERN const CGFloat NSGridViewSizeForContent NS_AVAILABLE_MAC(10_12); // Default value for row & column size, indicating it should automatically fit the content views.
+
+
+/*
+ NSGridView is a layout container for aligning views in spreadsheet-like rows & columns, indexed from the top left starting at 0.  Rows and columns are sized to fit their largest content (unless an explicit size has been set), but all cells in a given column will be the same width and all cells in a row will be the same height.
+
+ NSGridPlacement is used to specify the positioning of the contentView within the cell.  The content placement can be configured separately for the X & Y axes to align the content with either edge or to center it.  Placement properties on rows, columns, and cells default to 'inherited' so that the grid-level properties will effect all cells.  Content placement can be overridden for individual rows, columns, or cells by simply changing the appropriate property to a value other than 'inherited'.
+ */
+
+NS_CLASS_AVAILABLE_MAC(10_12)
+@interface NSGridView : NSView {
+@private
+    NSGridCellPlacement _xPlacement;
+    NSGridCellPlacement _yPlacement;
+    NSGridRowAlignment _rowAlignment;
+    CGFloat _rowSpacing;
+    CGFloat _colSpacing;
+    NSMutableArray *_columns;
+    NSMutableArray *_rows;
+    NSMapTable *_cellTable;
+    
+    id  _reserved __unused;
+    id  _reserved2 __unused;
+    id  _reserved3 __unused;
+}
+
+- (instancetype)initWithFrame:(NSRect)frameRect NS_DESIGNATED_INITIALIZER;
+- (nullable instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
+
++ (instancetype)gridViewWithNumberOfColumns:(NSInteger)columnCount rows:(NSInteger)rowCount; // Convenience initializer for gridview with specific dimensions.
++ (instancetype)gridViewWithViews:(NSArray<NSArray<NSView *> *> *)rows; // Convenience initializer for an autoreleased GridView large enough to hold the provided rows. Each element in 'rows' is an array of views for that row.
+
+@property (readonly) NSInteger numberOfRows;
+@property (readonly) NSInteger numberOfColumns;
+
+
+// Cells are arranged in rows and columns, which allow for configuration of content alignment on a row/column basis.
+- (NSGridRow *)rowAtIndex:(NSInteger)index;
+- (NSInteger)indexOfRow:(NSGridRow *)row; // Finds the index of the given row.  O(numberOfRows) time.
+- (NSGridColumn *)columnAtIndex:(NSInteger)index;
+- (NSInteger)indexOfColumn:(NSGridColumn *)column; // Finds the index of the given column.  O(numberOfColumns) time.
+- (NSGridCell*)cellAtColumnIndex:(NSInteger)columnIndex rowIndex:(NSInteger)rowIndex;
+- (nullable NSGridCell *)cellForView:(NSView*)view; // returns the cell from the receiver that contains the given view or one of its ancestors.
+
+// Rows & columns can be inserted & removed dynamically.  The grid will be enlarged to hold the specified views, if needed.
+- (NSGridRow *)addRowWithViews:(NSArray<NSView *> *)views;
+- (NSGridRow *)insertRowAtIndex:(NSInteger)index withViews:(NSArray<NSView *> *)views;
+- (void)moveRowAtIndex:(NSInteger)fromIndex toIndex:(NSInteger)toIndex;
+- (void)removeRowAtIndex:(NSInteger)index;
+
+- (NSGridColumn *)addColumnWithViews:(NSArray<NSView *> *)views;
+- (NSGridColumn *)insertColumnAtIndex:(NSInteger)index withViews:(NSArray<NSView *> *)views;
+- (void)moveColumnAtIndex:(NSInteger)fromIndex toIndex:(NSInteger)toIndex;
+- (void)removeColumnAtIndex:(NSInteger)index;
+
+
+// Grid-level layout properties will be used by cells that don't have the properties defined themselves or at the column/row level.  They default to bottom-leading placement, with no alignment.
+@property NSGridCellPlacement xPlacement;
+@property NSGridCellPlacement yPlacement;
+@property NSGridRowAlignment rowAlignment;
+
+// Grid-level property values for row & column spacing are added to the padding properties on rows & columns.  Defaults to 6pt.
+@property CGFloat rowSpacing;
+@property CGFloat columnSpacing;
+
+// Expands the cell at the top-leading corner of the given range to cover the entire area.  Other cells in the range become invalid: they will no longer maintain any layout, constraints, or content views.  Cell merging has no effect on the base cell coordinate system of the gridview, and cell references within a merged region will all refer to the single merged cell.  This is intended to be used to configure the grid geometry before installing views, but in the event that the cells being merged contain contentViews, only the top-leading will be kept.
+- (void)mergeCellsInHorizontalRange:(NSRange)hRange verticalRange:(NSRange)vRange;
+
+@end
+
+
+
+// NSGridRow represents a row of cells in the grid view, and allows content placement to be specified on a per-row basis.
+NS_CLASS_AVAILABLE_MAC(10_12)
+@interface NSGridRow : NSObject <NSCoding> {
+@private
+    NSGridView *_owningGridView;
+    NSMutableArray <NSGridCell*> *_cells;
+    NSLayoutYAxisAnchor* _top;
+    
+    id  _reserved __unused;
+    id  _reserved2 __unused;
+    id  _reserved3 __unused;
+    
+    NSGridCellPlacement _yPlacement;
+    NSGridRowAlignment _rowAlignment;
+
+    CGFloat _height;
+    CGFloat _topPadding;
+    CGFloat _bottomPadding;
+    BOOL _hidden;
+}
+
+@property (readonly,weak) NSGridView *gridView;
+@property (readonly) NSInteger numberOfCells;
+- (NSGridCell *)cellAtIndex:(NSInteger)index;
+
+
+// Row level placement properties will be used by cells whose Y-axis properties are set to 'inherited'.  These also default to 'inherited', falling back to the GridView level properties.
+@property NSGridCellPlacement yPlacement;
+@property NSGridRowAlignment rowAlignment;
+@property CGFloat height; // Height of this row, or NSGridViewSizeForContent (the default) to fit content automatically.
+@property CGFloat topPadding; // Padding is extra space between this row and an adjacent one.  Defaults to 0. Total inter-row-space is firstRow.bottomPadding + grid.rowSpacing + secondRow.topPadding
+@property CGFloat bottomPadding;
+
+@property (getter=isHidden) BOOL hidden; // Hidden rows/columns will collapse to 0 size and hide all their contentViews.
+- (void)mergeCellsInRange:(NSRange)range;
+
+@end
+
+
+
+// NSGridColumn represents a column of cells in the grid view, and allows content placement to be specified on a per-column basis.
+NS_CLASS_AVAILABLE_MAC(10_12)
+@interface NSGridColumn : NSObject <NSCoding> {
+@private
+    NSGridView *_owningGridView;
+    NSLayoutXAxisAnchor *_leading;
+    
+    id  _reserved __unused;
+    id  _reserved2 __unused;
+    id  _reserved3 __unused;
+    
+    NSGridCellPlacement _xPlacement;
+    CGFloat _width;
+    CGFloat _trailingPadding;
+    CGFloat _leadingPadding;
+    BOOL _hidden;
+}
+
+@property (readonly,weak) NSGridView *gridView;
+@property (readonly) NSInteger numberOfCells;
+- (NSGridCell *)cellAtIndex:(NSInteger)index;
+
+// Column level placement will be used by cells whose xPlacement is set to 'inherited'.  This also defaults to 'inherited', falling back to the NSGridView property.
+@property NSGridCellPlacement xPlacement;
+@property CGFloat width; // Width of this column, or NSGridViewSizeForContent (the default) to fit content automatically.
+@property CGFloat leadingPadding; // Padding is extra space between this column and an adjacent one.  Defaults to 0.  Total inter-column-space is firstColumn.trailingPadding + grid.columnSpacing + secondColumn.leadingPadding
+@property CGFloat trailingPadding;
+
+@property (getter=isHidden) BOOL hidden; // Hidden rows/columns will collapse to 0 size and hide all their contentViews.
+- (void)mergeCellsInRange:(NSRange)range;
+
+@end
+
+
+// NSGridCell represents a single cell in the grid.  The cell will maintain the necessary constraints for positioning out whichever contentView is set.
+NS_CLASS_AVAILABLE_MAC(10_12)
+@interface NSGridCell : NSObject <NSCoding> {
+@private
+    NSGridRow *_row;
+    NSGridColumn *_column;
+    NSView  *_contentView;
+    NSGridCell *_headOfMergedCell;
+    NSArray<NSLayoutConstraint*> *_customPlacementConstraints;
+    
+    id  _reserved __unused;
+    id  _reserved2 __unused;
+    id  _reserved3 __unused;
+    
+    NSGridCellPlacement _xPlacement;
+    NSGridCellPlacement _yPlacement;
+    NSGridRowAlignment _rowAlignment;
+}
+
+
+@property (strong,nullable) __kindof NSView *contentView; // The view whose placement will be managed by this cell.
+
+@property (class, readonly, strong) NSView *emptyContentView; // This view is used as a marker in NSGridView's "...WithViews:" methods to indicate a cell whose contentView should be nil.
+
+@property (readonly,weak) NSGridRow *row;
+@property (readonly,weak) NSGridColumn *column;
+
+// These properties control how the content view is placed in the cell.  Placement is configured independently for each axis.  Baseline alignment within a row is handled separately.  Properties set to the default value of 'inherited' will "fall back" to properties defined on the row/column, or to the GridView itself if needed.  Properties set to 'none' will cause the corresponding aspect of content layout to be left unmanaged by the grid view.  Handling of baseline alignment is special: all cells within a row that specify a rowAlignment (i.e., not "None") are considered to be 'aligned'.  The contentViews of such cells will be aligned by the specified baseline for each cell.  This creates the potential for unsatisfiable constraints in combination with the yPlacement properties on the aligned views.  Therefore, the entire baseline-aligned group is placed using the yPlacement of the first cell with a value other than NSGridCellPlaceNone.  The yPlacement properties of the remaining cells are overridden by their rowAlignment.
+
+@property NSGridCellPlacement xPlacement;
+@property NSGridCellPlacement yPlacement;
+@property NSGridRowAlignment rowAlignment;
+
+// Set these constraints to provide custom placement for the cell's content view.  NSGridView will activate the constraints when the cell is visible, and deactivate them when it is hidden.  Note that it is usually also necessary to set the xPlacement and/or yPlacement to 'Custom' in order to prevent NSGridView from adding its own placement constraints in one or both axes (which is likely to cause unsatisfiable constraints in combination with the custom ones).
+@property (copy) NSArray<NSLayoutConstraint *> *customPlacementConstraints;
+
+@end
+
+
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSHapticFeedback.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSHapticFeedback.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSHapticFeedback.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSHapticFeedback.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
-   NSHapticFeedback_Private.h
+   NSHapticFeedback.h
    Application Kit
-   Copyright (c) 2015, Apple Inc.
+   Copyright (c) 2015-2016, Apple Inc.
    All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSHelpManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSHelpManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSHelpManager.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSHelpManager.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSHelpManager.h
 	Application Kit
-	Copyright (c) 1995-2015, Apple Inc.
+	Copyright (c) 1995-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImage.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImage.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImage.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImage.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSImage.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -80,7 +80,7 @@
 
 + (nullable NSImage *)imageNamed:(NSString *)name;	/* If this finds & creates the image, only name is saved when archived */
 
-- (instancetype)initWithSize:(NSSize)aSize;
+- (instancetype)initWithSize:(NSSize)size;
 - (nullable instancetype)initWithData:(NSData *)data;			/* When archived, saves contents */
 - (nullable instancetype)initWithContentsOfFile:(NSString *)fileName;	/* When archived, saves contents */
 - (nullable instancetype)initWithContentsOfURL:(NSURL *)url;               /* When archived, saves contents */
@@ -115,7 +115,7 @@
 
 - (void)recache;
 @property (nullable, readonly, strong) NSData *TIFFRepresentation;
-- (nullable NSData *)TIFFRepresentationUsingCompression:(NSTIFFCompression)comp factor:(float)aFloat;
+- (nullable NSData *)TIFFRepresentationUsingCompression:(NSTIFFCompression)comp factor:(float)factor;
 
 @property (readonly, copy) NSArray<NSImageRep *> *representations;
 - (void)addRepresentations:(NSArray<NSImageRep *> *)imageReps;
@@ -222,11 +222,12 @@
 
 APPKIT_EXTERN NSString * const NSImageHintCTM NS_AVAILABLE_MAC(10_6); // value is NSAffineTransform
 APPKIT_EXTERN NSString * const NSImageHintInterpolation NS_AVAILABLE_MAC(10_6); // value is NSNumber with NSImageInterpolation enum value
+APPKIT_EXTERN NSString *const NSImageHintUserInterfaceLayoutDirection NS_AVAILABLE_MAC(10_12); // value is NSNumber with NSUserInterfaceLayoutDirection enum value
 
 @protocol NSImageDelegate <NSObject>
 @optional
 
-- (nullable NSImage *)imageDidNotDraw:(NSImage *)sender inRect:(NSRect)aRect;
+- (nullable NSImage *)imageDidNotDraw:(NSImage *)sender inRect:(NSRect)rect;
 
 - (void)image:(NSImage *)image willLoadRepresentation:(NSImageRep *)rep;
 - (void)image:(NSImage *)image didLoadRepresentationHeader:(NSImageRep *)rep;
@@ -250,8 +251,8 @@
 - (BOOL)isFlipped NS_DEPRECATED_MAC(10_0, 10_6);
 
 // these methods have surprising semantics.  Prefer to use the 'draw' methods (and note the new draw method taking respectContextIsFlipped as a parameter).  Please see the AppKit 10.6 release notes for exactly what's going on.
-- (void)dissolveToPoint:(NSPoint)point fraction:(CGFloat)aFloat NS_DEPRECATED_MAC(10_0, 10_6, "Use -drawAtPoint:... or -drawInRect:... methods instead");
-- (void)dissolveToPoint:(NSPoint)point fromRect:(NSRect)rect fraction:(CGFloat)aFloat NS_DEPRECATED_MAC(10_0, 10_6, "Use -drawAtPoint:... or -drawInRect:... methods instead");
+- (void)dissolveToPoint:(NSPoint)point fraction:(CGFloat)fraction NS_DEPRECATED_MAC(10_0, 10_6, "Use -drawAtPoint:... or -drawInRect:... methods instead");
+- (void)dissolveToPoint:(NSPoint)point fromRect:(NSRect)rect fraction:(CGFloat)fraction NS_DEPRECATED_MAC(10_0, 10_6, "Use -drawAtPoint:... or -drawInRect:... methods instead");
 - (void)compositeToPoint:(NSPoint)point operation:(NSCompositingOperation)op NS_DEPRECATED_MAC(10_0, 10_6, "Use -drawAtPoint:... or -drawInRect:... methods instead");
 - (void)compositeToPoint:(NSPoint)point fromRect:(NSRect)rect operation:(NSCompositingOperation)op NS_DEPRECATED_MAC(10_0, 10_6, "Use -drawAtPoint:... or -drawInRect:... methods instead");
 - (void)compositeToPoint:(NSPoint)point operation:(NSCompositingOperation)op fraction:(CGFloat)delta NS_DEPRECATED_MAC(10_0, 10_6, "Use -drawAtPoint:... or -drawInRect:... methods instead");
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImageCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImageCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImageCell.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImageCell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSImageCell.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImageRep.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImageRep.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImageRep.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImageRep.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSImageRep.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -11,6 +11,8 @@
 #import <Foundation/NSGeometry.h>
 #import <AppKit/AppKitDefines.h>
 #import <AppKit/NSGraphics.h>
+#import <AppKit/NSColorSpace.h>
+#import <AppKit/NSUserInterfaceLayout.h>
 #import <ApplicationServices/ApplicationServices.h>
 
 NS_ASSUME_NONNULL_BEGIN
@@ -23,6 +25,12 @@
     NSImageRepMatchesDevice = 0
 };
 
+typedef NS_ENUM(NSInteger, NSImageLayoutDirection) {
+    NSImageLayoutDirectionUnspecified = -1,
+    NSImageLayoutDirectionLeftToRight = 2,
+    NSImageLayoutDirectionRightToLeft = 3,
+} NS_AVAILABLE_MAC(10_12);
+
 @interface NSImageRep : NSObject <NSCopying, NSCoding> {
     /*All instance variables are private*/
     struct __repFlags {
@@ -34,7 +42,8 @@
         unsigned int keepCacheWindow:1 __attribute__((deprecated));
         unsigned int reserved:1;
         unsigned int bitsPerSample:8;
-	unsigned int gsaved:16;
+        unsigned int internalLayoutDirection:2;
+	unsigned int gsaved:14;
     } _repFlags;
     NSString *_colorSpaceName;
     NSSize _size;
@@ -61,6 +70,7 @@
 @property NSInteger bitsPerSample;
 @property NSInteger pixelsWide;
 @property NSInteger pixelsHigh;
+@property NSImageLayoutDirection layoutDirection NS_AVAILABLE_MAC(10_12); // Default: NSImageLayoutDirectionUnspecified
 
 /* The rest of the methods all deal with subclassers which can read/write data in files or pasteboards. 
 */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImageView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImageView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImageView.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImageView.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSImageView.h
     Application Kit
-    Copyright (c) 1994-2015, Apple Inc.
+    Copyright (c) 1994-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -39,6 +39,17 @@
 
 @end
 
+@interface NSImageView(NSImageViewConvenience)
+
+/*!
+ Creates a non-editable image view containing the provided image. The image is scaled proportionally down to fit the view, and is centered within the view.
+ @param image The image to display within the view.
+ @return An initialized image view.
+ */
++ (instancetype)imageViewWithImage:(NSImage *)image NS_AVAILABLE_MAC(10_12);
+
+@end
+
 NS_ASSUME_NONNULL_END
 
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSInputManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSInputManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSInputManager.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSInputManager.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSInputManager.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
  */
 
@@ -17,10 +17,10 @@
  */
 @protocol NSTextInput
 
-- (void) insertText:(null_unspecified id)aString NS_DEPRECATED_MAC(10_0, 10_6); // instead of keyDown: aString can be NSString or NSAttributedString
-- (void) doCommandBySelector:(null_unspecified SEL)aSelector NS_DEPRECATED_MAC(10_0, 10_6);
-	// setMarkedText: cannot take a nil first argument. aString can be NSString or NSAttributedString
-- (void) setMarkedText:(null_unspecified id)aString selectedRange:(NSRange)selRange NS_DEPRECATED_MAC(10_0, 10_6);
+- (void) insertText:(null_unspecified id)string NS_DEPRECATED_MAC(10_0, 10_6); // instead of keyDown: string can be NSString or NSAttributedString
+- (void) doCommandBySelector:(null_unspecified SEL)selector NS_DEPRECATED_MAC(10_0, 10_6);
+	// setMarkedText: cannot take a nil first argument. string can be NSString or NSAttributedString
+- (void) setMarkedText:(null_unspecified id)string selectedRange:(NSRange)selRange NS_DEPRECATED_MAC(10_0, 10_6);
 
 - (void) unmarkText NS_DEPRECATED_MAC(10_0, 10_6);
 - (BOOL) hasMarkedText NS_DEPRECATED_MAC(10_0, 10_6);
@@ -28,7 +28,7 @@
 
 /* Returns attributed string at the range.  This allows input mangers to query any range in backing-store.  May return nil.
 */
-- (null_unspecified NSAttributedString *) attributedSubstringFromRange:(NSRange)theRange NS_DEPRECATED_MAC(10_0, 10_6);
+- (null_unspecified NSAttributedString *) attributedSubstringFromRange:(NSRange)range NS_DEPRECATED_MAC(10_0, 10_6);
 
 /* This method returns the range for marked region.  If hasMarkedText == false, it'll return NSNotFound location & 0 length range.
 */
@@ -38,13 +38,13 @@
 */
 - (NSRange) selectedRange NS_DEPRECATED_MAC(10_0, 10_6);
 
-/* This method returns the first frame of rects for theRange in screen coordindate system.
+/* This method returns the first frame of rects for range in screen coordindate system.
 */
-- (NSRect) firstRectForCharacterRange:(NSRange)theRange NS_DEPRECATED_MAC(10_0, 10_6);
+- (NSRect) firstRectForCharacterRange:(NSRange)range NS_DEPRECATED_MAC(10_0, 10_6);
 
-/* This method returns the index for character that is nearest to thePoint.  thPoint is in screen coordinate system.
+/* This method returns the index for character that is nearest to point.  thPoint is in screen coordinate system.
 */
-- (NSUInteger)characterIndexForPoint:(NSPoint)thePoint NS_DEPRECATED_MAC(10_0, 10_6);
+- (NSUInteger)characterIndexForPoint:(NSPoint)point NS_DEPRECATED_MAC(10_0, 10_6);
 
 /* This method is the key to attribute extension.  We could add new attributes through this method. NSInputServer examines the return value of this method & constructs appropriate attributed string.
 */
@@ -72,7 +72,9 @@
     NSImage *_image;		// image for menu item
     unsigned int _flags;
     NSString *_keyBindingsName;	// path to the default bindings, if any
+#ifndef __OBJC2__
     int _reservedInputManager2;
+#endif
 }
 
 /* The "current input manager" is the one that is receiving input events at the time this method is called.  It may change out from under you, so don't cache the return value.
@@ -84,35 +86,35 @@
 + (void)cycleToNextInputLanguage:(nullable id)sender NS_DEPRECATED_MAC(10_0, 10_6);
 + (void)cycleToNextInputServerInLanguage:(nullable id)sender NS_DEPRECATED_MAC(10_0, 10_6);
 
-- (null_unspecified NSInputManager *) initWithName:(null_unspecified NSString *)inputServerName host:(null_unspecified NSString *)hostName NS_DEPRECATED_MAC(10_0, 10_6);
+- (null_unspecified NSInputManager *)initWithName:(null_unspecified NSString *)inputServerName host:(null_unspecified NSString *)hostName NS_DEPRECATED_MAC(10_0, 10_6);
 
-- (null_unspecified NSString *) localizedInputManagerName NS_DEPRECATED_MAC(10_0, 10_6);
+- (null_unspecified NSString *)localizedInputManagerName NS_DEPRECATED_MAC(10_0, 10_6);
 
 /* These messages are sent by Views that conform to the NSTextInput protocol TO the Current Input Manager when things happen via user or programmatic action.  E.g., when the mouse moves outside the marked range, send markedTextWillBeAbandoned:.  If the user selects some new text or moves the mouse within the marked region, send markedTextSelectionChanged:.  Not all input manager/server combinations will allow all changes, but abandoning of the marked region cannot be aborted.
 */ 
 
-- (void) markedTextAbandoned:(null_unspecified id)cli NS_DEPRECATED_MAC(10_0, 10_6); /* send after abandoning */
-- (void) markedTextSelectionChanged:(NSRange)newSel client:(null_unspecified id)cli NS_DEPRECATED_MAC(10_0, 10_6); /* send after changing */
+- (void)markedTextAbandoned:(null_unspecified id)cli NS_DEPRECATED_MAC(10_0, 10_6); /* send after abandoning */
+- (void)markedTextSelectionChanged:(NSRange)newSel client:(null_unspecified id)cli NS_DEPRECATED_MAC(10_0, 10_6); /* send after changing */
 
 /* This corresponds to a server method for input managers that demand to do their own interepretation of command keys as long as they're active.  This will typically be called by a key binder to find out whether it shouldn't just pass along strings.
 */
-- (BOOL) wantsToInterpretAllKeystrokes NS_DEPRECATED_MAC(10_0, 10_6);
+- (BOOL)wantsToInterpretAllKeystrokes NS_DEPRECATED_MAC(10_0, 10_6);
 
-- (null_unspecified NSString*) language NS_DEPRECATED_MAC(10_0, 10_6);
+- (null_unspecified NSString*)language NS_DEPRECATED_MAC(10_0, 10_6);
 
-- (null_unspecified NSImage *) image NS_DEPRECATED_MAC(10_0, 10_6);
+- (null_unspecified NSImage *)image NS_DEPRECATED_MAC(10_0, 10_6);
 
 - (null_unspecified NSInputServer *) server NS_DEPRECATED_MAC(10_0, 10_6);
 
 /* If corresponding input server wants to handle mouse events within marked region, this should return YES.  In that case, handleMouseEvent is sent. Otherwiese, mouse events are handled by first responder.
 */
-- (BOOL) wantsToHandleMouseEvents NS_DEPRECATED_MAC(10_0, 10_6);
+- (BOOL)wantsToHandleMouseEvents NS_DEPRECATED_MAC(10_0, 10_6);
 
-- (BOOL) handleMouseEvent:(null_unspecified NSEvent*)theMouseEvent NS_DEPRECATED_MAC(10_0, 10_6);
+- (BOOL)handleMouseEvent:(null_unspecified NSEvent*)mouseEvent NS_DEPRECATED_MAC(10_0, 10_6);
 
 /* This should return YES when the input method (language) prefers to delay text change notification 'till the input is actually committed.
 */
-- (BOOL) wantsToDelayTextChangeNotifications NS_DEPRECATED_MAC(10_0, 10_6);
+- (BOOL)wantsToDelayTextChangeNotifications NS_DEPRECATED_MAC(10_0, 10_6);
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSInputServer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSInputServer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSInputServer.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSInputServer.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSInputServer.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -15,8 +15,8 @@
 
 @protocol NSInputServiceProvider
 
-- (void) insertText:(null_unspecified id)aString client:(null_unspecified id)sender NS_DEPRECATED_MAC(10_0, 10_6);
-- (void) doCommandBySelector:(null_unspecified SEL)aSelector client:(null_unspecified id)sender NS_DEPRECATED_MAC(10_0, 10_6);
+- (void) insertText:(null_unspecified id)string client:(null_unspecified id)sender NS_DEPRECATED_MAC(10_0, 10_6);
+- (void) doCommandBySelector:(null_unspecified SEL)selector client:(null_unspecified id)sender NS_DEPRECATED_MAC(10_0, 10_6);
 - (void) markedTextAbandoned:(nullable id)sender NS_DEPRECATED_MAC(10_0, 10_6);
 - (void) markedTextSelectionChanged:(NSRange)newSel client:(null_unspecified id)sender NS_DEPRECATED_MAC(10_0, 10_6);
 - (void) terminate:(nullable id)sender NS_DEPRECATED_MAC(10_0, 10_6);
@@ -53,12 +53,12 @@
 
 @end
 
-/* These methods are sent to input servers that return YES to wantsToHandleMouseEvents.  thePoint is in screen coordinate.
+/* These methods are sent to input servers that return YES to wantsToHandleMouseEvents.  point is in screen coordinate.
 */
 @protocol NSInputServerMouseTracker
-- (BOOL) mouseDownOnCharacterIndex:(NSUInteger)theIndex atCoordinate:(NSPoint)thePoint withModifier:(NSUInteger)theFlags client:(null_unspecified id)sender NS_DEPRECATED_MAC(10_0, 10_6);
-- (BOOL) mouseDraggedOnCharacterIndex:(NSUInteger)theIndex atCoordinate:(NSPoint)thePoint withModifier:(NSUInteger)theFlags client:(null_unspecified id)sender NS_DEPRECATED_MAC(10_0, 10_6);
-- (void) mouseUpOnCharacterIndex:(NSUInteger)theIndex atCoordinate:(NSPoint)thePoint withModifier:(NSUInteger)theFlags client:(null_unspecified id)sender NS_DEPRECATED_MAC(10_0, 10_6);
+- (BOOL) mouseDownOnCharacterIndex:(NSUInteger)index atCoordinate:(NSPoint)point withModifier:(NSUInteger)flags client:(null_unspecified id)sender NS_DEPRECATED_MAC(10_0, 10_6);
+- (BOOL) mouseDraggedOnCharacterIndex:(NSUInteger)index atCoordinate:(NSPoint)point withModifier:(NSUInteger)flags client:(null_unspecified id)sender NS_DEPRECATED_MAC(10_0, 10_6);
+- (void) mouseUpOnCharacterIndex:(NSUInteger)index atCoordinate:(NSPoint)point withModifier:(NSUInteger)flags client:(null_unspecified id)sender NS_DEPRECATED_MAC(10_0, 10_6);
 @end
 
 NS_CLASS_DEPRECATED_MAC(10_0, 10_6)
@@ -67,7 +67,7 @@
     id _delegate;
 }
 
-- initWithDelegate:(null_unspecified id)aDelegate name:(null_unspecified NSString *)name NS_DEPRECATED_MAC(10_0, 10_6);
+- initWithDelegate:(null_unspecified id)delegate name:(null_unspecified NSString *)name NS_DEPRECATED_MAC(10_0, 10_6);
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSInterfaceStyle.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSInterfaceStyle.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSInterfaceStyle.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSInterfaceStyle.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSInterfaceStyle.h
         Application Kit
-        Copyright (c) 1995-2015, Apple Inc.
+        Copyright (c) 1995-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSItemProvider.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSItemProvider.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSItemProvider.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSItemProvider.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSItemProvider.h
 	Application Kit
-	Copyright (c) 2014-2015, Apple Inc.
+	Copyright (c) 2014-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSKeyValueBinding.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSKeyValueBinding.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSKeyValueBinding.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSKeyValueBinding.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSKeyValueBinding.h
 	Application Kit
-	Copyright (c) 2002-2015, Apple Inc.
+	Copyright (c) 2002-2016, Apple Inc.
 	All rights reserved.
  */
 
@@ -50,7 +50,7 @@
 - The default value shown in the options editor comes from the attribute description's defaultValue.*/
 
 
-- (NSArray<NSAttributeDescription *> *)optionDescriptionsForBinding:(NSString *)aBinding NS_AVAILABLE_MAC(10_5);
+- (NSArray<NSAttributeDescription *> *)optionDescriptionsForBinding:(NSString *)binding NS_AVAILABLE_MAC(10_5);
 
 
 @end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLayoutAnchor.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLayoutAnchor.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLayoutAnchor.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLayoutAnchor.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,15 +1,16 @@
 /*
  NSLayoutAnchor.h
  Application Kit
- Copyright (c) 2015, Apple Inc.
+ Copyright (c) 2015-2016, Apple Inc.
  All rights reserved.
  */
 
 #import <Foundation/NSGeometry.h>
 #import <Foundation/NSObject.h>
 
-@class NSLayoutConstraint;
+NS_ASSUME_NONNULL_BEGIN
 
+@class NSLayoutConstraint;
 
 /*
  An NSLayoutAnchor represents an edge or dimension of a layout item.  Its concrete subclasses allow concise creation of constraints.  The idea is that instead of invoking +[NSLayoutConstraint constraintWithItem: attribute: relatedBy: toItem: attribute: multiplier: constant:] directly, you can instead do something like this:
@@ -20,7 +21,7 @@
  
  */
 NS_CLASS_AVAILABLE(10_11, 9_0)
-@interface NSLayoutAnchor<AnchorType> : NSObject
+@interface NSLayoutAnchor<AnchorType> : NSObject <NSCopying, NSCoding>
 {
     @private
     id  _item;
@@ -78,4 +79,4 @@
 @end
 
 
-
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLayoutConstraint.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLayoutConstraint.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLayoutConstraint.h	2015-08-26 04:17:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLayoutConstraint.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSLayoutConstraint.h
 	Application Kit
-	Copyright (c) 2009-2015, Apple Inc.
+	Copyright (c) 2009-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -36,8 +36,8 @@
     NSLayoutAttributeHeight,
     NSLayoutAttributeCenterX,
     NSLayoutAttributeCenterY,
-    NSLayoutAttributeBaseline,
-    NSLayoutAttributeLastBaseline = NSLayoutAttributeBaseline,
+    NSLayoutAttributeLastBaseline,
+    NSLayoutAttributeBaseline NS_SWIFT_UNAVAILABLE("Use '.lastBaseline' instead") = NSLayoutAttributeLastBaseline,
     NSLayoutAttributeFirstBaseline NS_ENUM_AVAILABLE_MAC(10_11),
     
     NSLayoutAttributeNotAnAttribute = 0
@@ -53,7 +53,7 @@
     NSLayoutFormatAlignAllTrailing = (1 << NSLayoutAttributeTrailing),
     NSLayoutFormatAlignAllCenterX = (1 << NSLayoutAttributeCenterX),
     NSLayoutFormatAlignAllCenterY = (1 << NSLayoutAttributeCenterY),
-    NSLayoutFormatAlignAllBaseline = (1 << NSLayoutAttributeBaseline),
+    NSLayoutFormatAlignAllBaseline NS_SWIFT_UNAVAILABLE("Use '.alignAllLastBaseline' instead") = (1 << NSLayoutAttributeBaseline),
     NSLayoutFormatAlignAllLastBaseline = NSLayoutFormatAlignAllBaseline,
     NSLayoutFormatAlignAllFirstBaseline NS_ENUM_AVAILABLE_MAC(10_11) = (1 << NSLayoutAttributeFirstBaseline),
     
@@ -140,12 +140,13 @@
 
 /* Create constraints explicitly.  Constraints are of the form "view1.attr1 = view2.attr2 * multiplier + constant" 
  If your equation does not have a second view and attribute, use nil and NSLayoutAttributeNotAnAttribute.
+ Use of this method is not recommended. Constraints should be created using anchor objects on views and layout guides.
  */
 + (instancetype)constraintWithItem:(id)view1 attribute:(NSLayoutAttribute)attr1 relatedBy:(NSLayoutRelation)relation toItem:(nullable id)view2 attribute:(NSLayoutAttribute)attr2 multiplier:(CGFloat)multiplier constant:(CGFloat)c;
 
 /* If a constraint's priority level is less than NSLayoutPriorityRequired, then it is optional.  Higher priority constraints are met before lower priority constraints.
  Constraint satisfaction is not all or nothing.  If a constraint 'a == b' is optional, that means we will attempt to minimize 'abs(a-b)'.
- This property may only be modified as part of initial set up.  An exception will be thrown if it is set after a constraint has been added to a view.
+ This property may only be modified as part of initial set up or when optional.  After a constraint has been added to a view, an exception will be thrown if the priority is changed from/to NSLayoutPriorityRequired.
  */
 @property NSLayoutPriority priority;
 
@@ -156,12 +157,19 @@
 
 /* accessors
  firstItem.firstAttribute {==,<=,>=} secondItem.secondAttribute * multiplier + constant
+ Access to these properties is not recommended. Use the `firstAnchor` and `secondAnchor` properties instead.
  */
-@property (readonly, assign) id firstItem;
+@property (readonly, assign, nullable) id firstItem;
 @property (readonly) NSLayoutAttribute firstAttribute;
-@property (readonly) NSLayoutRelation relation;
 @property (nullable, readonly, assign) id secondItem;
 @property (readonly) NSLayoutAttribute secondAttribute;
+
+/* accessors
+ firstAnchor{==,<=,>=} secondAnchor * multiplier + constant
+ */
+@property (readonly, copy) NSLayoutAnchor *firstAnchor NS_AVAILABLE(10_12, 10_0);
+@property (readonly, copy, nullable) NSLayoutAnchor *secondAnchor NS_AVAILABLE(10_12, 10_0);
+@property (readonly) NSLayoutRelation relation;
 @property (readonly) CGFloat multiplier;
 
 /* Unlike the other properties, the constant may be modified after constraint creation.  Setting the constant on an existing constraint performs much better than removing the constraint and adding a new one that's just like the old but for having a new constant.
@@ -245,7 +253,7 @@
 
 @interface NSView (NSConstraintBasedLayoutCoreMethods) 
 - (void)updateConstraintsForSubtreeIfNeeded NS_AVAILABLE_MAC(10_7);
-- (void)updateConstraints NS_AVAILABLE_MAC(10_7);
+- (void)updateConstraints NS_AVAILABLE_MAC(10_7) NS_REQUIRES_SUPER;
 @property BOOL needsUpdateConstraints NS_AVAILABLE_MAC(10_7);
 
 - (void)layoutSubtreeIfNeeded NS_AVAILABLE_MAC(10_7);
@@ -313,7 +321,7 @@
  
  Note that not all views have an intrinsicContentSize.  A horizontal slider has an intrinsic height, but no intrinsic width - the slider artwork has no intrinsic best width.  A horizontal NSSlider returns (NSViewNoIntrinsicMetric, <slider height>) for intrinsicContentSize.  An NSBox returns (NSViewNoIntrinsicMetric, NSViewNoIntrinsicMetric).  The _intrinsic_ content size is concerned only with data that is in the view itself, not in other views.
  */
-APPKIT_EXTERN const CGFloat NSViewNoInstrinsicMetric; // Deprecated. Use NSViewNoIntrinsicMetric.
+APPKIT_EXTERN const CGFloat NSViewNoInstrinsicMetric NS_SWIFT_UNAVAILABLE("Use 'NSViewNoIntrinsicMetric' instead"); // Deprecated. Use NSViewNoIntrinsicMetric.
 APPKIT_EXTERN const CGFloat NSViewNoIntrinsicMetric NS_AVAILABLE_MAC(10_11); // -1
 
 @property (readonly) NSSize intrinsicContentSize NS_AVAILABLE_MAC(10_7);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLayoutGuide.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLayoutGuide.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLayoutGuide.h	2015-11-09 03:17:17.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLayoutGuide.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,11 +1,12 @@
 /*
 	NSLayoutGuide.h
 	Application Kit
-	Copyright (c) 2015, Apple Inc.
+	Copyright (c) 2015-2016, Apple Inc.
 	All rights reserved.
  */
 
 #import <AppKit/NSView.h>
+#import <AppKit/NSLayoutConstraint.h>
 #import <AppKit/NSLayoutAnchor.h>
 
 
@@ -36,13 +37,14 @@
     NSLayoutYAxisAnchor *_centerY;
     
     NSRect  _frame;
-    id  _reserved1;
-    id  _reserved2;
+    id _aux;
+    id  _reserved2 __unused;
+
     unsigned int    _shouldBeArchived:1;
     unsigned int    _weakHelper:1;
     unsigned int    _frameNeedsUpdate:1;
     unsigned int    _frameIsObserved:1;
-    unsigned int    _reservedFlags:28;
+    unsigned int    _reservedFlags:28 __unused;
 }
 
 
@@ -73,6 +75,12 @@
 @property (readonly, strong) NSLayoutXAxisAnchor *centerXAnchor;
 @property (readonly, strong) NSLayoutYAxisAnchor *centerYAnchor;
 
+
+// For debugging purposes:
+@property (readonly) BOOL hasAmbiguousLayout NS_AVAILABLE_MAC(10_12);
+- (NSArray<NSLayoutConstraint *> *)constraintsAffectingLayoutForOrientation:(NSLayoutConstraintOrientation)orientation NS_AVAILABLE_MAC(10_12);
+
+
 @end
 
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLayoutManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLayoutManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLayoutManager.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLayoutManager.h	2016-06-03 05:13:45.000000000 +0200
@@ -133,11 +133,11 @@
     NSTextView *_firstTextView;
     
     // Cache for rectangle arrays
-    __strong NSRect *_cachedRectArray;
+    NSRect *_cachedRectArray;
     NSUInteger _cachedRectArrayCapacity;
     
     // Cache for glyph strings
-    __strong char *_glyphBuffer;
+    char *_glyphBuffer;
     NSUInteger _glyphBufferSize;
     
     // Cache for faster glyph location lookup
@@ -286,9 +286,9 @@
 @property(readonly) NSUInteger numberOfGlyphs;
 
 // If non-contiguous layout is not enabled, these will cause generation of all glyphs up to and including glyphIndex.  The first CGGlyphAtIndex variant returns kCGFontIndexInvalid if the requested index is out of the range (0, numberOfGlyphs), and optionally returns a flag indicating whether the requested index is in range.  The second CGGlyphAtIndex variant raises a NSRangeError if the requested index is out of range.
-- (CGGlyph)CGGlyphAtIndex:(NSUInteger)glyphIndex isValidIndex:(nullable BOOL *)isValidIndex;
-- (CGGlyph)CGGlyphAtIndex:(NSUInteger)glyphIndex;
-- (BOOL)isValidGlyphIndex:(NSUInteger)glyphIndex;
+- (CGGlyph)CGGlyphAtIndex:(NSUInteger)glyphIndex isValidIndex:(nullable BOOL *)isValidIndex NS_AVAILABLE(10_11,7_0);
+- (CGGlyph)CGGlyphAtIndex:(NSUInteger)glyphIndex NS_AVAILABLE(10_11,7_0);
+- (BOOL)isValidGlyphIndex:(NSUInteger)glyphIndex NS_AVAILABLE(10_11,7_0);
 
 // If non-contiguous layout is not enabled, this will cause generation of all glyphs up to and including glyphIndex.  It will return the glyph property associated with the glyph at the specified index.
 - (NSGlyphProperty)propertyForGlyphAtIndex:(NSUInteger)glyphIndex NS_AVAILABLE(10_5, 7_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLevelIndicator.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLevelIndicator.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLevelIndicator.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLevelIndicator.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSLevelIndicatorCell.h
     Application Kit
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLevelIndicatorCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLevelIndicatorCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLevelIndicatorCell.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSLevelIndicatorCell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSLevelIndicatorCell.h
     Application Kit
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMagnificationGestureRecognizer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMagnificationGestureRecognizer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMagnificationGestureRecognizer.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMagnificationGestureRecognizer.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSMagnificationGestureRecognizer.h
     Application Kit
-    Copyright (c) 2013-2015, Apple Inc.
+    Copyright (c) 2013-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -15,10 +15,10 @@
 @private
     NSPoint _location;
     NSPoint _reserved1;
-    NSInteger _mflags;
+    NSInteger _mflags __unused;
     CGFloat _magnification;
+    id _reserved2;
 #ifndef __OBJC2__
-    NSInteger _reserved2;
     NSInteger _reserved3;
 #endif
 }
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMatrix.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMatrix.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMatrix.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMatrix.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSMatrix.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -120,8 +120,8 @@
 
 
 - (instancetype)initWithFrame:(NSRect)frameRect;
-- (instancetype)initWithFrame:(NSRect)frameRect mode:(NSMatrixMode)aMode prototype:(NSCell *)aCell numberOfRows:(NSInteger)rowsHigh numberOfColumns:(NSInteger)colsWide;
-- (instancetype)initWithFrame:(NSRect)frameRect mode:(NSMatrixMode)aMode cellClass:(nullable Class)factoryId numberOfRows:(NSInteger)rowsHigh numberOfColumns:(NSInteger)colsWide;
+- (instancetype)initWithFrame:(NSRect)frameRect mode:(NSMatrixMode)mode prototype:(NSCell *)cell numberOfRows:(NSInteger)rowsHigh numberOfColumns:(NSInteger)colsWide;
+- (instancetype)initWithFrame:(NSRect)frameRect mode:(NSMatrixMode)mode cellClass:(nullable Class)factoryId numberOfRows:(NSInteger)rowsHigh numberOfColumns:(NSInteger)colsWide;
 
 
 @property (assign) Class cellClass;
@@ -129,10 +129,10 @@
 - (NSCell *)makeCellAtRow:(NSInteger)row column:(NSInteger)col;
 @property NSMatrixMode mode;
 @property BOOL allowsEmptySelection;
-- (void)sendAction:(SEL)aSelector to:(id)anObject forAllCells:(BOOL)flag;
+- (void)sendAction:(SEL)selector to:(id)object forAllCells:(BOOL)flag;
 @property (readonly, copy) NSArray<NSCell *> *cells;
 - (void)sortUsingSelector:(SEL)comparator;
-- (void)sortUsingFunction:(NSInteger (*)(id, id, void * __nullable))compare context:(nullable void *)context;
+- (void)sortUsingFunction:(NSInteger (NS_NOESCAPE *)(id, id, void * __nullable))compare context:(nullable void *)context;
 @property (nullable, readonly, strong) __kindof NSCell *selectedCell;
 @property (readonly, copy) NSArray<__kindof NSCell *> *selectedCells;
 @property (readonly) NSInteger selectedRow;
@@ -143,7 +143,7 @@
 - (void)deselectAllCells;
 - (void)selectCellAtRow:(NSInteger)row column:(NSInteger)col;
 - (void)selectAll:(nullable id)sender;
-- (BOOL)selectCellWithTag:(NSInteger)anInt;
+- (BOOL)selectCellWithTag:(NSInteger)tag;
 @property NSSize cellSize;
 @property NSSize intercellSpacing;
 - (void)setScrollable:(BOOL)flag;
@@ -157,21 +157,21 @@
 @property (readonly) NSInteger numberOfColumns;
 - (nullable __kindof NSCell *)cellAtRow:(NSInteger)row column:(NSInteger)col;
 - (NSRect)cellFrameAtRow:(NSInteger)row column:(NSInteger)col;
-- (BOOL)getRow:(NSInteger *)row column:(NSInteger *)col ofCell:(NSCell *)aCell;
-- (BOOL)getRow:(NSInteger *)row column:(NSInteger *)col forPoint:(NSPoint)aPoint;
+- (BOOL)getRow:(NSInteger *)row column:(NSInteger *)col ofCell:(NSCell *)cell;
+- (BOOL)getRow:(NSInteger *)row column:(NSInteger *)col forPoint:(NSPoint)point;
 - (void)renewRows:(NSInteger)newRows columns:(NSInteger)newCols;
 - (void)putCell:(NSCell *)newCell atRow:(NSInteger)row column:(NSInteger)col;
 - (void)addRow;
 - (void)addRowWithCells:(NSArray<NSCell *> *)newCells;
 - (void)insertRow:(NSInteger)row;
-- (void)insertRow:(NSInteger)row withCells:(NSArray<NSCell *> *)newCells;
+- (void)insertRow:(NSInteger)row withCells:(nullable NSArray<NSCell *> *)newCells;
 - (void)removeRow:(NSInteger)row;
 - (void)addColumn;
 - (void)addColumnWithCells:(NSArray<NSCell *> *)newCells;
 - (void)insertColumn:(NSInteger)column;
-- (void)insertColumn:(NSInteger)column withCells:(NSArray<NSCell *> *)newCells;
+- (void)insertColumn:(NSInteger)column withCells:(nullable NSArray<NSCell *> *)newCells;
 - (void)removeColumn:(NSInteger)col;
-- (nullable __kindof NSCell *)cellWithTag:(NSInteger)anInt;
+- (nullable __kindof NSCell *)cellWithTag:(NSInteger)tag;
 @property (nullable) SEL doubleAction;
 @property BOOL autosizesCells;
 - (void)sizeToCells;
@@ -182,8 +182,8 @@
 @property (getter=isAutoscroll) BOOL autoscroll;
 - (void)scrollCellToVisibleAtRow:(NSInteger)row column:(NSInteger)col;
 @property (readonly) NSInteger mouseDownFlags;
-- (void)mouseDown:(NSEvent *)theEvent;
-- (BOOL)performKeyEquivalent:(NSEvent *)theEvent;
+- (void)mouseDown:(NSEvent *)event;
+- (BOOL)performKeyEquivalent:(NSEvent *)event;
 - (BOOL)sendAction;
 - (void)sendDoubleAction;
 @property (nullable, assign) id<NSMatrixDelegate> delegate;
@@ -194,7 +194,7 @@
 - (void)textDidChange:(NSNotification *)notification;
 - (void)selectText:(nullable id)sender;
 - (nullable __kindof NSCell *)selectTextAtRow:(NSInteger)row column:(NSInteger)col;
-- (BOOL)acceptsFirstMouse:(nullable NSEvent *)theEvent;
+- (BOOL)acceptsFirstMouse:(nullable NSEvent *)event;
 - (void)resetCursorRects;
 - (void)setToolTip:(nullable NSString *)toolTipString forCell:(NSCell *)cell;
 - (nullable NSString *)toolTipForCell:(NSCell *)cell;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMediaLibraryBrowserController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMediaLibraryBrowserController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMediaLibraryBrowserController.h	2015-08-26 04:17:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMediaLibraryBrowserController.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /* 
     NSMediaLibraryBrowserController.h
     Application Kit
-    Copyright (c) 2012-2015, Apple Inc.
+    Copyright (c) 2012-2016, Apple Inc.
     All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenu.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenu.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenu.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenu.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
  NSMenu.h
  Application Kit
- Copyright (c) 1996-2015, Apple Inc.
+ Copyright (c) 1996-2016, Apple Inc.
  All rights reserved.
 */
 
@@ -17,7 +17,7 @@
 @class NSMenu;
 @protocol NSMenuDelegate;
 
-@interface NSMenu : NSObject <NSCopying, NSCoding>
+@interface NSMenu : NSObject <NSCopying, NSCoding, NSUserInterfaceItemIdentification, NSAccessibilityElement, NSAccessibility>
 {
     /*All instance variables are private*/
     @private
@@ -45,14 +45,16 @@
         unsigned int noBottomPadding:1;
 	unsigned int hasNCStyle:1;
 	unsigned int delegateIsUnsafeUnretained:1;
-        unsigned int RESERVED:11;
+        unsigned int avoidUsingCache:1;
+        unsigned int RESERVED:10;
     } _mFlags;
     NSString *_uiid;
 }
 
 /* Designated initializer.  If this menu is used as a submenu of an item in the application's main menu, then the title is what appears in the menu bar.  Otherwise, the title is ignored.  Do not pass nil (an exception will result), but you may pass an empty string.
  */
-- (instancetype)initWithTitle:(NSString *)aTitle;
+- (instancetype)initWithTitle:(NSString *)title NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)decoder NS_DESIGNATED_INITIALIZER;
 
 /* Set and get the menu's title.  The titles of the submenus of the application's main menu items appear in the menu bar. */
 @property (copy) NSString *title;
@@ -87,10 +89,10 @@
 
 /* Inserts a new menu item with the given title, action, and key equivalent, at the given index.  The index must be at least zero and no more than the receiver's item count.  The title and key equivalent must not be nil (pass the empty string to indicate no key equivalent). This returns the new item.
  */
-- (nullable NSMenuItem *)insertItemWithTitle:(NSString *)aString action:(nullable SEL)aSelector keyEquivalent:(NSString *)charCode atIndex:(NSInteger)index;
+- (NSMenuItem *)insertItemWithTitle:(NSString *)string action:(nullable SEL)selector keyEquivalent:(NSString *)charCode atIndex:(NSInteger)index;
 
 /* Appends a new menu item with the given properties to the end of the menu. */
-- (nullable NSMenuItem *)addItemWithTitle:(NSString *)aString action:(nullable SEL)aSelector keyEquivalent:(NSString *)charCode;
+- (NSMenuItem *)addItemWithTitle:(NSString *)string action:(nullable SEL)selector keyEquivalent:(NSString *)charCode;
 
 /* Removes the item at the given index, which must be at least zero and less than the number of items.  All subsequent items will shift down one index. */
 - (void)removeItemAtIndex:(NSInteger)index;
@@ -98,8 +100,8 @@
 /* Removes the item from the menu.  If the item is nil, or is not present in the receiver, an exception will be raised. */
 - (void)removeItem:(NSMenuItem *)item;
 
-/* Same as [anItem setSubmenu:aMenu].  anItem may not be nil. */
-- (void)setSubmenu:(nullable NSMenu *)aMenu forItem:(NSMenuItem *)anItem;
+/* Same as [item setSubmenu:menu].  item may not be nil. */
+- (void)setSubmenu:(nullable NSMenu *)menu forItem:(NSMenuItem *)item;
 
 /* Removes all items.  This is more efficient than removing items one by one.  This does not post NSMenuDidRemoveItemNotification, for efficiency.
 */
@@ -118,14 +120,14 @@
 - (NSInteger)indexOfItem:(NSMenuItem *)item;
 
 /* Returns the first item in the menu that matches the given property, or -1 if no item in the menu matches. */
-- (NSInteger)indexOfItemWithTitle:(NSString *)aTitle;
-- (NSInteger)indexOfItemWithTag:(NSInteger)aTag;
+- (NSInteger)indexOfItemWithTitle:(NSString *)title;
+- (NSInteger)indexOfItemWithTag:(NSInteger)tag;
 - (NSInteger)indexOfItemWithRepresentedObject:(id)object;
 - (NSInteger)indexOfItemWithSubmenu:(nullable NSMenu *)submenu;
-- (NSInteger)indexOfItemWithTarget:(nullable id)target andAction:(SEL)actionSelector;
+- (NSInteger)indexOfItemWithTarget:(nullable id)target andAction:(nullable SEL)actionSelector;
 
 /* Returns the first item in the menu with the given property, or nil if no item in the menu matches. */
-- (nullable NSMenuItem *)itemWithTitle:(NSString *)aTitle;
+- (nullable NSMenuItem *)itemWithTitle:(NSString *)title;
 - (nullable NSMenuItem *)itemWithTag:(NSInteger)tag;
 
 /* Set and get whether the menu autoenables items.  If a menu autoenables items, then calls to -[NSMenuItem setEnabled:] are ignored, and the enabled state is computed via the NSMenuValidation informal protocol below.  Autoenabling is on by default. */
@@ -134,9 +136,9 @@
  /* If the receiver is set to autoenable items, then this triggers autovalidation of all menu items according to the NSMenuValidation informal protocol; otherwise this does nothing.  It is normally not necessary to call this; it will be called for you at the right time. */
 - (void)update;
   
-/* Attempts to perform the given key equivalent.  If the event is a key down event that matches the key equivalent of a menu item in the receiver or, recursively, any menu item in a submenu of the receiver, then this triggers that menu item's action and returns YES.  Otherwise, this returns NO.
+/* Attempts to perform the given key equivalent.  If the event is a key down event that matches the key equivalent of a menu item in the receiver or, recursively, any menu item in a submenu of the receiver, then this triggers that menu item's action (if the item is enabled) and returns YES.  Otherwise, this returns NO.
 */
-- (BOOL)performKeyEquivalent:(NSEvent *)theEvent;
+- (BOOL)performKeyEquivalent:(NSEvent *)event;
 
 /* This method is called when a menu item's enabled state, submenu, title, attributed title, image, key equivalent, key equivalent modifier mask, alternate status, indent, tooltip, view, or visibility (via isHidden) changes.  This method posts NSMenuDidChangeItemNotification.  Future properties will likely not call this method when they change, because posting a notification when a property changes is rather expensive.
  */
@@ -146,8 +148,8 @@
 */
 - (void)performActionForItemAtIndex:(NSInteger)index;
 
-/* Set and get the delegate for the menu.  See the NSMenuDelegate protocol for methods that the delegate may implement. */
-@property (nullable, assign) id<NSMenuDelegate> delegate;
+/* Set and get the delegate for the menu. The delegate is weakly referenced for zeroing-weak compatible objects on 10.9 and later. Otherwise the behavior of this property is 'assign'. See the NSMenuDelegate protocol for methods that the delegate may implement. */
+@property (nullable, weak) id<NSMenuDelegate> delegate;
 
 /* If called on the main menu, returns the height of the menu bar in pixels.  If called on any other menu, returns 0.
  */
@@ -262,12 +264,12 @@
 
 /* Returns the zone used to allocate NSMenu objects.  This is left in for compatibility and has returned NSDefaultMallocZone() since OS X 10.2.  It is not necessary to use this - menus can be allocated the usual way. */
 + (null_unspecified NSZone *)menuZone NS_DEPRECATED_MAC(10_0, 10_11);
-+ (void)setMenuZone:(null_unspecified NSZone *)aZone NS_DEPRECATED_MAC(10_0, 10_2);
++ (void)setMenuZone:(null_unspecified NSZone *)zone NS_DEPRECATED_MAC(10_0, 10_2);
 
 - (null_unspecified NSMenu *)attachedMenu NS_DEPRECATED_MAC(10_0, 10_2);
 - (BOOL)isAttached NS_DEPRECATED_MAC(10_0, 10_2);
 - (void)sizeToFit NS_DEPRECATED_MAC(10_0, 10_2);
-- (NSPoint)locationForSubmenu:(null_unspecified NSMenu *)aSubmenu NS_DEPRECATED_MAC(10_0, 10_2);
+- (NSPoint)locationForSubmenu:(null_unspecified NSMenu *)submenu NS_DEPRECATED_MAC(10_0, 10_2);
 
 /* In OS X 10.6 and later, the following methods no longer do anything useful. */
 @property BOOL menuChangedMessagesEnabled NS_DEPRECATED_MAC(10_0, 10_11);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenuItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenuItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenuItem.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenuItem.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSMenuItem.h
         Application Kit
-        Copyright (c) 1996-2015, Apple Inc.
+        Copyright (c) 1996-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -16,7 +16,7 @@
 @class NSMenu;
 @class NSImage, NSAttributedString, NSView;
 
-@interface NSMenuItem : NSObject <NSCopying, NSCoding, NSValidatedUserInterfaceItem>
+@interface NSMenuItem : NSObject <NSCopying, NSCoding, NSValidatedUserInterfaceItem, NSUserInterfaceItemIdentification, NSAccessibilityElement, NSAccessibility>
 {
     /*All instance variables are private*/
     @private
@@ -73,10 +73,12 @@
 
 + (NSMenuItem *)separatorItem;
 
-- (instancetype)initWithTitle:(NSString *)aString action:(nullable SEL)aSelector keyEquivalent:(NSString *)charCode;
+- (instancetype)initWithTitle:(NSString *)string action:(nullable SEL)selector keyEquivalent:(NSString *)charCode NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)decoder NS_DESIGNATED_INITIALIZER;
 
+/* Never call the set method directly it is there only for subclassers.
+ */
 @property (nullable, assign) NSMenu *menu;
-    // Never call the set method directly it is there only for subclassers.
 
 
 @property (readonly) BOOL hasSubmenu;
@@ -92,7 +94,7 @@
 @property (getter=isSeparatorItem, readonly) BOOL separatorItem;
 
 @property (copy) NSString *keyEquivalent;
-@property NSUInteger keyEquivalentModifierMask;
+@property NSEventModifierFlags keyEquivalentModifierMask;
 
 @property (readonly, copy) NSString *userKeyEquivalent;
 
@@ -102,7 +104,7 @@
 
 @property NSInteger state;
 @property (null_resettable, strong) NSImage *onStateImage; // checkmark by default
-@property (null_resettable, strong) NSImage *offStateImage; // none by default
+@property (nullable, strong) NSImage *offStateImage; // none by default
 @property (null_resettable, strong) NSImage *mixedStateImage; // horizontal line by default?
 
 @property (getter=isEnabled) BOOL enabled;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenuItemCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenuItemCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenuItemCell.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenuItemCell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSMenuItemCell.h
         Application Kit
-        Copyright (c) 1997-2015, Apple Inc.
+        Copyright (c) 1997-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -36,6 +36,9 @@
     } _micFlags;
 }
 
+- (instancetype)initTextCell:(NSString *)string NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
+
 @property (nullable, strong) NSMenuItem *menuItem;
 
 #if ! __LP64__
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenuView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenuView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenuView.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenuView.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSMenuView.h
         Application Kit
-        Copyright (c) 1997-2015, Apple Inc.
+        Copyright (c) 1997-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -100,7 +100,7 @@
 - (NSMenu *)attachedMenu;
 - (BOOL)isAttached;
 - (BOOL)isTornOff;
-- (NSPoint)locationForSubmenu:(NSMenu *)aSubmenu;
+- (NSPoint)locationForSubmenu:(NSMenu *)submenu;
 
 - (void)setWindowFrameForAttachingToRect:(NSRect)screenRect onScreen:(NSScreen *)screen preferredEdge:(NSRectEdge)edge popUpSelectedItem:(NSInteger)selectedItemIndex;
 - (void)detachSubmenu;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMovie.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMovie.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMovie.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMovie.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSMovie.h
         Application Kit
-        Copyright (c) 2000-2015, Apple Inc.
+        Copyright (c) 2000-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -26,12 +26,14 @@
   @private
     void*    _movie;
     NSURL*   _url;
+#ifndef __OBJC2__
     struct {
 	int dispose:1;
 	int reserved:31;
     } _movieFlags;
     long     _reserved1;
     long     _reserved2;
+#endif
 }
 
 #if !__LP64__
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMovieView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMovieView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMovieView.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMovieView.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,6 +1,6 @@
 /*
         NSMovieView.h
-        Copyright (c) 1998-2015, Apple Inc. All rights reserved.
+        Copyright (c) 1998-2016, Apple Inc. All rights reserved.
 */
 
 // Please note that NSMovie and NSMovieView are deprecated. NSMovieView does not exist in 64-bit.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNib.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNib.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNib.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNib.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSNib.h
 	Application Kit
-	Copyright (c) 2003-2015, Apple Inc.
+	Copyright (c) 2003-2016, Apple Inc.
 	All rights reserved.
 
 NSNib serves as a wrapper around a single InterfaceBuilder nib.  When an NSNib instance is created from a nib file, all of the data needed to instantiate the nib (the object graph as well as images and sounds that might be in the nib bundle) are read from the disk, however the nib is not instantiated until you call one of the instantiation methods.
@@ -34,7 +34,7 @@
         unsigned int _reserved:29;
     } _flags;
     NSString *_path;
-    id reserved2;
+    id reserved2 __unused;
 }
 
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNibConnector.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNibConnector.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNibConnector.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNibConnector.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSNibConnector.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -16,7 +16,7 @@
     id _destination;	/* The destination of the connection. */
     NSString *_label;	/* The label of the connection. */
 }
-@property (assign) id source;
+@property (nullable, assign) id source;
 @property (nullable, assign) id destination;
 @property (copy) NSString *label;
 - (void)replaceObject:(id)oldObject withObject:(id)newObject;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNibControlConnector.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNibControlConnector.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNibControlConnector.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNibControlConnector.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSNibControlConnector.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNibDeclarations.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNibDeclarations.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNibDeclarations.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNibDeclarations.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSNibDeclarations.h
         Application Kit
-        Copyright (c) 1996-2015, Apple Inc.
+        Copyright (c) 1996-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNibLoading.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNibLoading.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNibLoading.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNibLoading.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSNibLoading.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNibOutletConnector.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNibOutletConnector.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNibOutletConnector.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSNibOutletConnector.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSNibOutletConnector.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSObjectController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSObjectController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSObjectController.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSObjectController.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSObjectController.h
 	Application Kit
-	Copyright (c) 2002-2015, Apple Inc.
+	Copyright (c) 2002-2016, Apple Inc.
 	All rights reserved.
  */
 
@@ -16,7 +16,7 @@
 
 @interface NSObjectController : NSController {
 @private
-    void *_reserved3;
+    void *_reserved3 __unused;
     id _managedProxy;
     struct __objectControllerFlags {
         unsigned int _editable:1;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenGL.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenGL.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenGL.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenGL.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSOpenGL.h
         Application Kit
-        Copyright (c) 2000-2015, Apple Inc.
+        Copyright (c) 2000-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -52,7 +52,6 @@
 	NSOpenGLPFAAllRenderers       =   1,	/* choose from all available renderers          */
 	NSOpenGLPFATripleBuffer       =   3,	/* choose a triple buffered pixel format        */
 	NSOpenGLPFADoubleBuffer       =   5,	/* choose a double buffered pixel format        */
-	NSOpenGLPFAStereo             =   6,	/* stereo buffering supported                   */
 	NSOpenGLPFAAuxBuffers         =   7,	/* number of aux buffers                        */
 	NSOpenGLPFAColorSize          =   8,	/* number of color buffer bits                  */
 	NSOpenGLPFAAlphaSize          =  11,	/* number of alpha component bits               */
@@ -80,6 +79,7 @@
  	NSOpenGLPFAOpenGLProfile NS_ENUM_AVAILABLE_MAC(10_7)     =  99,	/* specify an OpenGL Profile to use             */
    
         /* The following attributes are deprecated. */
+	NSOpenGLPFAStereo NS_ENUM_DEPRECATED_MAC(10_0, 10_12)        =   6,
 	NSOpenGLPFAOffScreen NS_ENUM_DEPRECATED_MAC(10_0, 10_7)        =  53,
 	NSOpenGLPFAFullScreen NS_ENUM_DEPRECATED_MAC(10_0, 10_6)       =  54,
 	NSOpenGLPFASingleRenderer  NS_ENUM_DEPRECATED_MAC(10_0, 10_9)  =  71,
@@ -109,10 +109,10 @@
 {
 @private
     struct _CGLPixelFormatObject *_CGLPixelFormat;
-    void *_reserved1;
-    void *_reserved2;
-    void *_reserved3;
-    void *_reserved4;
+    void *_reserved1 __unused;
+    void *_reserved2 __unused;
+    void *_reserved3 __unused;
+    void *_reserved4 __unused;
 }
 
 - (nullable instancetype)initWithAttributes:(const NSOpenGLPixelFormatAttribute *)attribs;
@@ -140,8 +140,8 @@
 {
 @private
     struct _CGLPBufferObject *_CGLPBuffer;
-    void			*_reserved1;
-    void			*_reserved2;
+    void			*_reserved1 __unused;
+    void			*_reserved2 __unused;
 }
 
 /*
@@ -169,24 +169,24 @@
 
 /* Parameter names for NSOpenGLContext -setValues:forParameter: and -getValues:forParameter: */
 typedef NS_ENUM(NSInteger, NSOpenGLContextParameter) {
-    NSOpenGLCPSwapInterval           = 222, /* 1 param.  0 -> Don't sync, 1 -> Sync to vertical retrace     */
-    NSOpenGLCPSurfaceOrder           = 235, /* 1 param.  1 -> Above Window (default), -1 -> Below Window    */
-    NSOpenGLCPSurfaceOpacity         = 236, /* 1 param.  1-> Surface is opaque (default), 0 -> non-opaque   */
-    NSOpenGLCPSurfaceBackingSize     = 304, /* 2 params.  Width/height of surface backing size              */
-    NSOpenGLCPReclaimResources       = 308, /* 0 params.                                                    */
-    NSOpenGLCPCurrentRendererID      = 309, /* 1 param.   Retrieves the current renderer ID                 */
-    NSOpenGLCPGPUVertexProcessing    = 310, /* 1 param.   Currently processing vertices with GPU (get)      */
-    NSOpenGLCPGPUFragmentProcessing  = 311, /* 1 param.   Currently processing fragments with GPU (get)     */
-    NSOpenGLCPHasDrawable            = 314, /* 1 param.   Boolean returned if drawable is attached          */
-    NSOpenGLCPMPSwapsInFlight        = 315, /* 1 param.   Max number of swaps queued by the MP GL engine    */
+    NSOpenGLContextParameterSwapInterval           = 222, /* 1 param.  0 -> Don't sync, 1 -> Sync to vertical retrace     */
+    NSOpenGLContextParameterSurfaceOrder           = 235, /* 1 param.  1 -> Above Window (default), -1 -> Below Window    */
+    NSOpenGLContextParameterSurfaceOpacity         = 236, /* 1 param.  1-> Surface is opaque (default), 0 -> non-opaque   */
+    NSOpenGLContextParameterSurfaceBackingSize     = 304, /* 2 params.  Width/height of surface backing size              */
+    NSOpenGLContextParameterReclaimResources       = 308, /* 0 params.                                                    */
+    NSOpenGLContextParameterCurrentRendererID      = 309, /* 1 param.   Retrieves the current renderer ID                 */
+    NSOpenGLContextParameterGPUVertexProcessing    = 310, /* 1 param.   Currently processing vertices with GPU (get)      */
+    NSOpenGLContextParameterGPUFragmentProcessing  = 311, /* 1 param.   Currently processing fragments with GPU (get)     */
+    NSOpenGLContextParameterHasDrawable            = 314, /* 1 param.   Boolean returned if drawable is attached          */
+    NSOpenGLContextParameterMPSwapsInFlight        = 315, /* 1 param.   Max number of swaps queued by the MP GL engine    */
 
     /* The following parameters are obsolete and deprecated for new development. */
-    NSOpenGLCPSwapRectangle          = 200, /* 4 params.  Set or get the swap rectangle {x, y, w, h}        */
-    NSOpenGLCPSwapRectangleEnable    = 201, /* Enable or disable the swap rectangle                         */
-    NSOpenGLCPRasterizationEnable    = 221, /* Enable or disable all rasterization                          */
-    NSOpenGLCPStateValidation        = 301, /* Validate state for multi-screen functionality                */
-    NSOpenGLCPSurfaceSurfaceVolatile = 306, /* 1 param.   Surface volatile state                            */
-} ;
+    NSOpenGLContextParameterSwapRectangle          = 200, /* 4 params.  Set or get the swap rectangle {x, y, w, h}        */
+    NSOpenGLContextParameterSwapRectangleEnable    = 201, /* Enable or disable the swap rectangle                         */
+    NSOpenGLContextParameterRasterizationEnable    = 221, /* Enable or disable all rasterization                          */
+    NSOpenGLContextParameterStateValidation        = 301, /* Validate state for multi-screen functionality                */
+    NSOpenGLContextParameterSurfaceSurfaceVolatile = 306, /* 1 param.   Surface volatile state                            */
+};
 
 
 /*
@@ -197,7 +197,7 @@
 @interface NSOpenGLContext : NSObject <NSLocking>
 {
 @private
-	__weak NSView            *_view;
+    NSView *_view;
     struct _CGLContextObject *_CGLContext;
 }
 
@@ -271,4 +271,22 @@
 - (void)setTextureImageToPixelBuffer:(NSOpenGLPixelBuffer *)pixelBuffer colorBuffer:(GLenum)source NS_DEPRECATED_MAC(10_3, 10_7); /* Use IOSurface instead of NSOpenGLPixelBuffer on Mac OS 10.7 and newer. */
 @end
 
+
+static const NSOpenGLContextParameter NSOpenGLCPSwapInterval /*API_DEPRECATED_WITH_REPLACEMENT("NSOpenGLContextParameterSwapInterval", macosx(10.5, 10.12))*/ = NSOpenGLContextParameterSwapInterval;
+static const NSOpenGLContextParameter NSOpenGLCPSurfaceOrder /*API_DEPRECATED_WITH_REPLACEMENT("NSOpenGLContextParameterSurfaceOrder", macosx(10.0, 10.12))*/ = NSOpenGLContextParameterSurfaceOrder;
+static const NSOpenGLContextParameter NSOpenGLCPSurfaceOpacity /*API_DEPRECATED_WITH_REPLACEMENT("NSOpenGLContextParameterSurfaceOpacity", macosx(10.0, 10.12))*/ = NSOpenGLContextParameterSurfaceOpacity;
+static const NSOpenGLContextParameter NSOpenGLCPSurfaceBackingSize /*API_DEPRECATED_WITH_REPLACEMENT("NSOpenGLContextParameterSurfaceBackingSize", macosx(10.0, 10.12))*/ = NSOpenGLContextParameterSurfaceBackingSize;
+static const NSOpenGLContextParameter NSOpenGLCPReclaimResources /*API_DEPRECATED_WITH_REPLACEMENT("NSOpenGLContextParameterReclaimResources", macosx(10.0, 10.12))*/ = NSOpenGLContextParameterReclaimResources;
+static const NSOpenGLContextParameter NSOpenGLCPCurrentRendererID /*API_DEPRECATED_WITH_REPLACEMENT("NSOpenGLContextParameterCurrentRendererID", macosx(10.0, 10.12))*/ = NSOpenGLContextParameterCurrentRendererID;
+static const NSOpenGLContextParameter NSOpenGLCPGPUVertexProcessing /*API_DEPRECATED_WITH_REPLACEMENT("NSOpenGLContextParameterGPUVertexProcessing", macosx(10.0, 10.12))*/ = NSOpenGLContextParameterGPUVertexProcessing;
+static const NSOpenGLContextParameter NSOpenGLCPGPUFragmentProcessing /*API_DEPRECATED_WITH_REPLACEMENT("NSOpenGLContextParameterGPUFragmentProcessing", macosx(10.0, 10.12))*/ = NSOpenGLContextParameterGPUFragmentProcessing;
+static const NSOpenGLContextParameter NSOpenGLCPHasDrawable /*API_DEPRECATED_WITH_REPLACEMENT("NSOpenGLContextParameterHasDrawable", macosx(10.0, 10.12))*/ = NSOpenGLContextParameterHasDrawable;
+static const NSOpenGLContextParameter NSOpenGLCPMPSwapsInFlight /*API_DEPRECATED_WITH_REPLACEMENT("NSOpenGLContextParameterMPSwapsInFlight", macosx(10.0, 10.12))*/ = NSOpenGLContextParameterMPSwapsInFlight;
+
+static const NSOpenGLContextParameter NSOpenGLCPSwapRectangle /*API_DEPRECATED_WITH_REPLACEMENT("NSOpenGLContextParameterSwapRectangle", macosx(10.0, 10.12))*/ = NSOpenGLContextParameterSwapRectangle;
+static const NSOpenGLContextParameter NSOpenGLCPSwapRectangleEnable /*API_DEPRECATED_WITH_REPLACEMENT("NSOpenGLContextParameterSwapRectangleEnable", macosx(10.0, 10.12))*/ = NSOpenGLContextParameterSwapRectangleEnable;
+static const NSOpenGLContextParameter NSOpenGLCPRasterizationEnable /*API_DEPRECATED_WITH_REPLACEMENT("NSOpenGLContextParameterRasterizationEnable", macosx(10.0, 10.12))*/ = NSOpenGLContextParameterRasterizationEnable;
+static const NSOpenGLContextParameter NSOpenGLCPStateValidation /*API_DEPRECATED_WITH_REPLACEMENT("NSOpenGLContextParameterStateValidation", macosx(10.0, 10.12))*/ = NSOpenGLContextParameterStateValidation;
+static const NSOpenGLContextParameter NSOpenGLCPSurfaceSurfaceVolatile /*API_DEPRECATED_WITH_REPLACEMENT("NSOpenGLContextParameterSurfaceSurfaceVolatile", macosx(10.0, 10.12))*/ = NSOpenGLContextParameterSurfaceSurfaceVolatile;
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenGLLayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenGLLayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenGLLayer.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenGLLayer.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSOpenGLLayer.h
         Application Kit
-        Copyright (c) 2008-2015, Apple Inc.
+        Copyright (c) 2008-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -18,7 +18,7 @@
 @private
     NSOpenGLPixelFormat *_openGLPixelFormat;
     NSOpenGLContext *_openGLContext;
-    void *_reserved[5];
+    void *_reserved[5] __unused;
 }
 
 /* Provides access to the layer's associated view.  Subclasses shouldn't invoke -setView:, but can override it if desired to intercept the layer's association to, or dissociation from, a view.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenGLView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenGLView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenGLView.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenGLView.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSOpenGLView.h
         Application Kit
-        Copyright (c) 2000-2015, Apple Inc.
+        Copyright (c) 2000-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -15,9 +15,9 @@
   @private
     NSOpenGLContext*     _openGLContext;
     NSOpenGLPixelFormat* _pixelFormat;
-    NSInteger                _reserved1;
-    NSInteger                _reserved2;
-    NSInteger                _reserved3;
+    NSInteger                _reserved1 __unused;
+    NSInteger                _reserved2 __unused;
+    NSInteger                _reserved3 __unused;
 }
 
 + (NSOpenGLPixelFormat*)defaultPixelFormat;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenPanel.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenPanel.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenPanel.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenPanel.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSOpenPanel.h
     Application Kit
-    Copyright (c) 1994-2015, Apple Inc.
+    Copyright (c) 1994-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -15,8 +15,8 @@
 
 @interface NSOpenPanel : NSSavePanel {
 @private
-    char _reservedOpenPanel[4];
-    void *_privateOpenPanel;
+    char _reservedOpenPanel[4] __unused;
+    void *_privateOpenPanel __unused;
 }
 
 /* Creates a new instance of the NSOpenPanel. This class is not a singleton. 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOutlineView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOutlineView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOutlineView.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOutlineView.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSOutlineView.h
     Application Kit
-    Copyright (c) 1997-2015, Apple Inc.
+    Copyright (c) 1997-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -36,7 +36,7 @@
     unsigned int delegateWillDisplayOutlineCell:1;
     unsigned int subclassRowForItem:1;
     unsigned int selectionAdjustmentDisabled:1;
-    unsigned int unused:1;
+    unsigned int stronglyReferencesItems:1;
     unsigned int animateExpandAndCollapse:1;
     unsigned int delegateHeightOfRowByItem:1;
     unsigned int delayRowEntryFreeDisabled:1;
@@ -54,9 +54,9 @@
     unsigned int dontRedisplayOnFrameChange:1;
     unsigned int allowAutomaticAnimations:1;
     unsigned int dataSourceObjectValueByItem:1;
-    unsigned int allItemsLoaded:1;
+    unsigned int unused3:1;
 #else
-    unsigned int allItemsLoaded:1;
+    unsigned int unused3:1;
     unsigned int dataSourceObjectValueByItem:1;
     unsigned int allowAutomaticAnimations:1;
     unsigned int dontRedisplayOnFrameChange:1;
@@ -74,7 +74,7 @@
     unsigned int delayRowEntryFreeDisabled:1;
     unsigned int delegateHeightOfRowByItem:1;
     unsigned int animateExpandAndCollapse:1;
-    unsigned int unused:1;
+    unsigned int stronglyReferencesItems:1;
     unsigned int selectionAdjustmentDisabled:1;
     unsigned int subclassRowForItem:1;
     unsigned int delegateWillDisplayOutlineCell:1;
@@ -102,7 +102,7 @@
     NSInteger            _numberOfRows;    
     _NSOVRowEntry       *_rowEntryTree;
     NSMapTable          *_itemToEntryMap;
-    __strong CFMutableArrayRef _rowEntryArray;
+    CFMutableArrayRef    _rowEntryArray;
     NSInteger            _firstRowIndexDrawn;
     id                   _autoExpandTimerItem;
     NSTableColumn        *_outlineTableColumn;
@@ -115,7 +115,7 @@
     NSMutableArray       *_draggedItems;
     _OVFlags             _ovFlags;
     id                   _ovLock;
-    __strong long       *_indentArray;
+    long                *_indentArray;
     long                 _originalWidth;
     id                   _expandSet;
     id                   _expandSetToExpandItemsInto;
@@ -125,11 +125,9 @@
     id                   _ovReserved;
 }
 
-- (void)setDelegate:(nullable id <NSOutlineViewDelegate>)anObject;
-- (nullable id <NSOutlineViewDelegate>)delegate;
 
-- (void)setDataSource:(nullable id <NSOutlineViewDataSource>)aSource;
-- (nullable id <NSOutlineViewDataSource>)dataSource;
+@property (nullable, weak) id <NSOutlineViewDelegate> delegate;
+@property (nullable, weak) id <NSOutlineViewDataSource> dataSource;
 
 /* The 'outlineTableColumn' is the column that displays data in a hierarchical fashion, indented one identationlevel per level, decorated with indentation marker (disclosure triangle) on rows that are expandable. A nil 'outlineTableColumn' is silently ignored. On 10.5 and higher, this value is saved in encodeWithCoder: and restored in initWithCoder:.
 */
@@ -248,6 +246,10 @@
  */
 @property NSUserInterfaceLayoutDirection userInterfaceLayoutDirection NS_AVAILABLE_MAC(10_7);
 
+/* When YES, the NSOutlineView will retain and release the objects returned to it from the dataSource (outlineView:child:ofItem:). When NO, it only treats the objects as opaque items and assume the client has a retain on them. The default value is YES for applications linked on 10.12 and later, and NO for previous applications. This value is not encoded in the nib, and must be explicitly set to NO in code if one requires the legacy behavior and is linking on 10.12 and later. In general, this is required if the items themselves create a retain cycle.
+ */
+@property BOOL stronglyReferencesItems NS_AVAILABLE_MAC(10_12);
+
 @end
 
 #pragma mark -
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPDFImageRep.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPDFImageRep.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPDFImageRep.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPDFImageRep.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSPDFImageRep.h
         Application Kit
-        Copyright (c) 1999-2015, Apple Inc.
+        Copyright (c) 1999-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -13,8 +13,8 @@
 {
   @private
     NSData* _pdfData;
-    int     _reserved1;
-    int     _reserved2;
+    int     _reserved1 __unused;
+    int     _reserved2 __unused;
 
     id      _private;
 }
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPDFInfo.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPDFInfo.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPDFInfo.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPDFInfo.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSPDFInfo.h
         Application Kit
-        Copyright (c) 2013-2015, Apple Inc.
+        Copyright (c) 2013-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPDFPanel.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPDFPanel.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPDFPanel.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPDFPanel.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSPDFPanel.h
         Application Kit
-        Copyright (c) 2013-2015, Apple Inc.
+        Copyright (c) 2013-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPICTImageRep.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPICTImageRep.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPICTImageRep.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPICTImageRep.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSPICTImageRep.h
         Application Kit
-        Copyright (c) 1997-2015, Apple Inc.
+        Copyright (c) 1997-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPageController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPageController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPageController.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPageController.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
  NSPageController.h
  Application Kit
- Copyright (c) 2011-2015, Apple Inc.
+ Copyright (c) 2011-2016, Apple Inc.
  All rights reserved.
  */
 
@@ -115,13 +115,13 @@
 /* NOTE: The following 2 methods are only useful if you also implement the above two methods.
  */
 
-/* You only need to implement this if the view frame can differ between arrangedObjects. This method must return immediately. Avoid file, network or any potentially blocking or lengthy work to provide an answer. If this method is not implemented, all arrangedObjects are assumed to have the same frame as the current selectedViewController.view or the bounds of view when selectedViewController is nil.
+/* You only need to implement this if the view frame can differ between arrangedObjects. This method must return immediately. Avoid file, network or any potentially blocking or lengthy work to provide an answer. This method is called with a nil object to get the default frame size. If this method is not implemented, all arrangedObjects are assumed to have the same frame as the current selectedViewController.view or the bounds of view when selectedViewController is nil.
  */
-- (NSRect)pageController:(NSPageController *)pageController frameForObject:(id)object;
+- (NSRect)pageController:(NSPageController *)pageController frameForObject:(nullable id)object;
 
-/* Prepare the viewController and view for drawing. Setup data sources and perform layout. Note: this method is called on the main thread and should return immediately. The view will be asked to draw on a background thread and must support background drawing. If this method is not implemented, then viewController's representedObject is set to the representedObject.
+/* Prepare the viewController and view for drawing. Setup data sources and perform layout. Note: a nil object is passed for the purposes of caching a rendering of a default viewController. Note: this method is called on the main thread and should return immediately. The view will be asked to draw on a background thread and must support background drawing. If this method is not implemented, then viewController's representedObject is set to the representedObject.
  */
-- (void)pageController:(NSPageController *)pageController prepareViewController:(NSViewController *)viewController withObject:(id)object;
+- (void)pageController:(NSPageController *)pageController prepareViewController:(NSViewController *)viewController withObject:(nullable id)object;
 
 /* Note: You may find these useful regardless of which way you use NSPageController (History vs Custom).
  */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPageLayout.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPageLayout.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPageLayout.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPageLayout.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSPageLayout.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -22,7 +22,7 @@
     NSPrintInfo *_presentedPrintInfo;
     NSWindowController *_windowController;
 #if __LP64__
-    id _reserved[4];
+    id _reserved[4] __unused;
 #else
     unsigned char _compatibilityPadding[156];
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPanGestureRecognizer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPanGestureRecognizer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPanGestureRecognizer.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPanGestureRecognizer.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSPanGestureRecognizer.h
     Application Kit
-    Copyright (c) 2013-2015, Apple Inc.
+    Copyright (c) 2013-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -18,15 +18,14 @@
     NSUInteger _buttonMask;
     NSInteger _buttonCount;
     id _velocityFilter;
-    CGFloat private0;
-    CGFloat private1;
+    CGFloat private0 __unused;
+    CGFloat private1 __unused;
     struct __pgrFlags {
-        unsigned int    reserved:32;
-    } __pgrFlags;
+        unsigned int    reserved0:1;
+        unsigned int    reserved:31;
+    } __pgrFlags __unused;
     id _reserved0;
-#ifndef __OBJC2__
-    NSInteger _reserved1;
-#endif
+    id _reserved1 __unused;
 }
 
 /* bitfield of the button(s) required to recognize this click where bit 0 is the primary button, 1 is the secondary button, etc...
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPanel.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPanel.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPanel.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPanel.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,20 +1,12 @@
 /*
     NSPanel.h
     Application Kit
-    Copyright (c) 1994-2015, Apple Inc.
+    Copyright (c) 1994-2016, Apple Inc.
     All rights reserved.
 */
 
 #import <AppKit/NSWindow.h>
 
-// Panel specific styleMask options
-enum {
-    NSUtilityWindowMask			= 1 << 4,
-    NSDocModalWindowMask 		= 1 << 6,
-    NSNonactivatingPanelMask		= 1 << 7,           // specify a panel that does not activate owning application
-    NSHUDWindowMask NS_ENUM_AVAILABLE_MAC(10_6) = 1 << 13   // specify a heads up display panel
-};
-
 @interface NSPanel : NSWindow {
 
 }
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSParagraphStyle.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSParagraphStyle.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSParagraphStyle.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSParagraphStyle.h	2016-06-03 05:13:45.000000000 +0200
@@ -17,7 +17,7 @@
 // NSTextTab
 APPKIT_EXTERN NSString * NSTabColumnTerminatorsAttributeName NS_AVAILABLE(10_0, 7_0); // An attribute for NSTextTab options.  The value is NSCharacterSet.  The character set is used to determine the tab column terminating character.  The tab and newline characters are implied even if not included in the character set.
 
-NS_CLASS_AVAILABLE(10_0, 7_0) @interface NSTextTab : NSObject <NSCopying, NSCoding>
+NS_CLASS_AVAILABLE(10_0, 7_0) @interface NSTextTab : NSObject <NSCopying, NSCoding, NSSecureCoding>
 {
     /*All instance variables are private*/
     struct {
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPasteboard.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPasteboard.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPasteboard.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPasteboard.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSPasteboard.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -61,7 +61,7 @@
     NSMutableDictionary *_promiseTypeNamesByIdentifier;
     id			_support;	
     id			_pasteboardItems;
-    void *		_reserved[3];
+    void *		_reserved[3] __unused;
 }
 
 + (NSPasteboard *)generalPasteboard;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPasteboardItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPasteboardItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPasteboardItem.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPasteboardItem.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSPasteboardItem.h
 	Application Kit
-	Copyright (c) 2008-2015, Apple Inc.
+	Copyright (c) 2008-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -41,7 +41,7 @@
     NSUInteger	    _index;
     NSInteger	    _gen;
     id		    _auxObject;
-    void	    *_reserved;
+    void	    *_reserved __unused;
 }
 
 /* Returns an array of UTI strings of the data types supported by the receiver.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPathCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPathCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPathCell.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPathCell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSPathCell.h
     Application Kit
-    Copyright (c) 2005-2015, Apple Inc.
+    Copyright (c) 2005-2016, Apple Inc.
     All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPathComponentCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPathComponentCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPathComponentCell.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPathComponentCell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSPathComponentCell.h
     Application Kit
-    Copyright (c) 2006-2015, Apple Inc.
+    Copyright (c) 2006-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -36,7 +36,7 @@
         unsigned int isDropTarget:1;
         unsigned int reserved:27;
     } _flags; 
-    id _aux;
+    id _aux __unused;
 }
 
 /* See NSPathComponent.h for details on the image & URL properties.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPathControl.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPathControl.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPathControl.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPathControl.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSPathControl.h
     Application Kit
-    Copyright (c) 2005-2015, Apple Inc.
+    Copyright (c) 2005-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -43,7 +43,7 @@
 @private
     NSDragOperation _draggingSourceOperationMaskForLocal;
     NSDragOperation _draggingSourceOperationMaskForNonLocal;
-    NSInteger _reserved;
+    NSInteger _reserved __unused;
     id _delegate;
     id _pathAux;
 }
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPathControlItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPathControlItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPathControlItem.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPathControlItem.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
  NSPathControlItem.h
  Application Kit
- Copyright (c) 2013-2015, Apple Inc.
+ Copyright (c) 2013-2016, Apple Inc.
  All rights reserved.
  */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPersistentDocument.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPersistentDocument.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPersistentDocument.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPersistentDocument.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSPersistentDocument.h
 	Application Kit
-	Copyright (c) 2004-2015, Apple Inc.
+	Copyright (c) 2004-2016, Apple Inc.
 	All rights reserved.
  */
 
@@ -20,8 +20,8 @@
     id _store;
     uintptr_t _pDocFlags;
     id _relatedRequestURLs;
-    void *_reserved3;
-    void *_reserved4;
+    void *_reserved3 __unused;
+    void *_reserved4 __unused;
 }
 
 // Persistent documents always have a managed context (and a persistent store coordinator through that context).
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopUpButton.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopUpButton.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopUpButton.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopUpButton.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSPopUpButton.h
         Application Kit
-        Copyright (c) 1997-2015, Apple Inc.
+        Copyright (c) 1997-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -22,7 +22,7 @@
         unsigned int RESERVED:31;
     } _pbFlags;
 #if __LP64__
-    id _popupReserved;
+    id _popupReserved __unused;
 #endif
 }
 
@@ -69,7 +69,7 @@
 - (void)selectItemAtIndex:(NSInteger)index;
 - (void)selectItemWithTitle:(NSString *)title;
 - (BOOL)selectItemWithTag:(NSInteger)tag;
-- (void)setTitle:(NSString *)aString;
+- (void)setTitle:(NSString *)string;
 
 @property (nullable, readonly, strong) NSMenuItem *selectedItem;
 @property (readonly) NSInteger indexOfSelectedItem;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopUpButtonCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopUpButtonCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopUpButtonCell.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopUpButtonCell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSPopUpButtonCell.h
         Application Kit
-        Copyright (c) 1997-2015, Apple Inc.
+        Copyright (c) 1997-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -38,11 +38,12 @@
         unsigned int RESERVED:19;
     } _pbcFlags;
 #if __LP64__
-    id _popupReserved;
+    id _popupReserved __unused;
 #endif
 }
 
-- (instancetype)initTextCell:(NSString *)stringValue pullsDown:(BOOL)pullDown;
+- (instancetype)initTextCell:(NSString *)stringValue pullsDown:(BOOL)pullDown NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
 
 // Overrides behavior of NSCell.  This is the menu for the popup, not a context menu.  PopUpButtonCells do not have context menus.
 @property (nullable, strong) NSMenu *menu;
@@ -92,7 +93,7 @@
 - (void)selectItemAtIndex:(NSInteger)index;
 - (void)selectItemWithTitle:(NSString *)title;
 - (BOOL)selectItemWithTag:(NSInteger)tag;
-- (void)setTitle:(nullable NSString *)aString;
+- (void)setTitle:(nullable NSString *)string;
 
 @property (nullable, readonly, strong) NSMenuItem *selectedItem;
 @property (readonly) NSInteger indexOfSelectedItem;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopover.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopover.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopover.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopover.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSPopover.h
     Application Kit
-    Copyright (c) 2010-2015, Apple Inc.
+    Copyright (c) 2010-2016, Apple Inc.
     All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPredicateEditor.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPredicateEditor.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPredicateEditor.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPredicateEditor.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSPredicateEditor.h
 	Application Kit
-	Copyright (c) 2006-2015, Apple Inc.
+	Copyright (c) 2006-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPredicateEditorRowTemplate.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPredicateEditorRowTemplate.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPredicateEditorRowTemplate.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPredicateEditorRowTemplate.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSPredicateEditorRowTemplate.h
 	Application Kit
-	Copyright (c) 2006-2015, Apple Inc.
+	Copyright (c) 2006-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -32,7 +32,7 @@
 	unsigned reserved:30;
     } _ptFlags;
     
-    id _patternReserved;
+    id _patternReserved __unused;
 }
 
 /* returns a positive number if the template can represent the predicate, and zero if it cannot.  The highest match determines which template is responsible for displaying the predicate.  Developers can override this to determine which predicates their custom template handles.  By default, this returns values in the range [0., 1.]
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPressGestureRecognizer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPressGestureRecognizer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPressGestureRecognizer.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPressGestureRecognizer.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSPressGestureRecognizer.h
     Application Kit
-    Copyright (c) 2013-2015, Apple Inc.
+    Copyright (c) 2013-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -19,9 +19,7 @@
     CGFloat _allowableMovement;
     NSInteger _buttonCount;
     NSInteger _lcflags;
-#ifndef __OBJC2__
-    NSInteger _reserved1;
-#endif
+    id _reserved1;
 }
 
 /* bitfield of the button(s) required to recognize this click where bit 0 is the primary button, 1 is the secondary button, etc...
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPressureConfiguration.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPressureConfiguration.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPressureConfiguration.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPressureConfiguration.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSPressureConfiguration.h
     Application Kit
-    Copyright (c) 2013-2015, Apple Inc.
+    Copyright (c) 2013-2016, Apple Inc.
     All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPrintInfo.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPrintInfo.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPrintInfo.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPrintInfo.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSPrintInfo.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -91,7 +91,9 @@
 
 /* Given a dictionary that contains attribute entries, initialize. Attributes that are recognized by the NSPrintInfo class will be silently validated in the context of the printer selected by the attributes dictionary, or the default printer if the attributes dictionary selects no printer. Attributes that are not recognized by the NSPrintInfo class will be preserved, and returned in the dictionary returned by the -dictionary method, but otherwise ignored. This is the designated initializer for this class.
 */
-- (instancetype)initWithDictionary:(NSDictionary<NSString *, id> *)attributes;
+- (instancetype)initWithDictionary:(NSDictionary<NSString *, id> *)attributes NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)inDecoder NS_DESIGNATED_INITIALIZER;
+- (instancetype)init; // Convience method that calls through to initWithDictionary:nil
 
 /* Return a dictionary that contains attribute entries. This dictionary may contain attributes that were not specified in the dictionary originally passed to this object by -initWithDictionary. Changes to this dictionary will be reflected in the values returned by subsequent invocations of other of this class' methods.
 */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPrintOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPrintOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPrintOperation.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPrintOperation.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSPrintOperation.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPrintPanel.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPrintPanel.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPrintPanel.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPrintPanel.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSPrintPanel.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -83,7 +83,7 @@
     NSPrintInfo *_presentedPrintInfo;
     NSWindowController *_windowController;
 #if __LP64__
-    id _reserved[2];
+    id _reserved[2] __unused;
 #else
     unsigned char _compatibilityPadding[192];
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPrinter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPrinter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPrinter.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPrinter.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSPrinter.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -27,11 +27,11 @@
     NSString *_printerName;
     void *_printer;
     NSDictionary *_cachedDeviceDescription;
-    int _ppdCreationNum;
-    void *_ppdNodes;
-    void *_ppdPriv;
+    int _ppdCreationNum __unused;
+    void *_ppdNodes __unused;
+    void *_ppdPriv __unused;
 #if __LP64__
-    id _reserved[3];
+    id _reserved[3] __unused;
 #else
     unsigned char _compatibilityPadding[20];
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSProgressIndicator.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSProgressIndicator.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSProgressIndicator.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSProgressIndicator.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSProgressIndicator.h
         Application Kit
-        Copyright (c) 1997-2015, Apple Inc.
+        Copyright (c) 1997-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -61,7 +61,7 @@
     CGFloat     _drawingWidth;
 
     id		_roundColor;
-    id          _reserved;
+    id          _reserved __unused;
 
     volatile struct __progressIndicatorFlags {
         unsigned int isSpinning:1;
@@ -83,7 +83,7 @@
     } _progressIndicatorFlags;
 
     /* For future use */
-    id _NSProgressIndicatorReserved1;
+    id _NSProgressIndicatorReserved1 __unused;
 }
 
 	/* Options */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSQuickDrawView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSQuickDrawView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSQuickDrawView.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSQuickDrawView.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSQuickDrawView.h
         Application Kit
-        Copyright (c) 1999-2015, Apple Inc.
+        Copyright (c) 1999-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSResponder.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSResponder.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSResponder.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSResponder.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSResponder.h
         Application Kit
-        Copyright (c) 1994-2015, Apple Inc.
+        Copyright (c) 1994-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -24,27 +24,27 @@
 - (nullable instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
 
 @property (nullable, assign) NSResponder *nextResponder;
-- (BOOL)tryToPerform:(SEL)anAction with:(nullable id)anObject;
-- (BOOL)performKeyEquivalent:(NSEvent *)theEvent;
+- (BOOL)tryToPerform:(SEL)action with:(nullable id)object;
+- (BOOL)performKeyEquivalent:(NSEvent *)event;
 - (nullable id)validRequestorForSendType:(NSString *)sendType returnType:(NSString *)returnType;
-- (void)mouseDown:(NSEvent *)theEvent;
-- (void)rightMouseDown:(NSEvent *)theEvent;
-- (void)otherMouseDown:(NSEvent *)theEvent;
-- (void)mouseUp:(NSEvent *)theEvent;
-- (void)rightMouseUp:(NSEvent *)theEvent;
-- (void)otherMouseUp:(NSEvent *)theEvent;
-- (void)mouseMoved:(NSEvent *)theEvent;
-- (void)mouseDragged:(NSEvent *)theEvent;
-- (void)scrollWheel:(NSEvent *)theEvent;
-- (void)rightMouseDragged:(NSEvent *)theEvent;
-- (void)otherMouseDragged:(NSEvent *)theEvent;
-- (void)mouseEntered:(NSEvent *)theEvent;
-- (void)mouseExited:(NSEvent *)theEvent;
-- (void)keyDown:(NSEvent *)theEvent;
-- (void)keyUp:(NSEvent *)theEvent;
-- (void)flagsChanged:(NSEvent *)theEvent;
-- (void)tabletPoint:(NSEvent *)theEvent;
-- (void)tabletProximity:(NSEvent *)theEvent;
+- (void)mouseDown:(NSEvent *)event;
+- (void)rightMouseDown:(NSEvent *)event;
+- (void)otherMouseDown:(NSEvent *)event;
+- (void)mouseUp:(NSEvent *)event;
+- (void)rightMouseUp:(NSEvent *)event;
+- (void)otherMouseUp:(NSEvent *)event;
+- (void)mouseMoved:(NSEvent *)event;
+- (void)mouseDragged:(NSEvent *)event;
+- (void)scrollWheel:(NSEvent *)event;
+- (void)rightMouseDragged:(NSEvent *)event;
+- (void)otherMouseDragged:(NSEvent *)event;
+- (void)mouseEntered:(NSEvent *)event;
+- (void)mouseExited:(NSEvent *)event;
+- (void)keyDown:(NSEvent *)event;
+- (void)keyUp:(NSEvent *)event;
+- (void)flagsChanged:(NSEvent *)event;
+- (void)tabletPoint:(NSEvent *)event;
+- (void)tabletProximity:(NSEvent *)event;
 - (void)cursorUpdate:(NSEvent *)event NS_AVAILABLE_MAC(10_5);
 /* The following *WithEvent methods are available on 10.5.2 or later, and will be sent only on hardware capable of generating the corresponding NSEvent types 
 */
@@ -92,7 +92,7 @@
 
 - (void)helpRequested:(NSEvent *)eventPtr;
 
-- (BOOL)shouldBeTreatedAsInkEvent:(NSEvent *)theEvent;
+- (BOOL)shouldBeTreatedAsInkEvent:(NSEvent *)event;
 
 /* Some views process gesture scroll events to perform elastic scrolling. In some cases, you may want to track gesture scroll events like a swipe. (see -trackSwipeEventWithOptions:dampenAmountThresholdMin:max:usingHandler: in NSEvent.h) Implement this method and return YES in your swipe controller and views that perform elastic scrolling will forward gesture scroll events up the responder chain on the following condition: the content to be scrolled is already at the edge of the scrolled direction at the beginning of the scroll gesture. Otherwise, the view will perform elastic scrolling. Default implementation returns NO.
 */
@@ -116,7 +116,7 @@
 - (void)insertText:(id)insertString;
     // When key events have been passed off to the key binding mechanism through interpretKeyEvents:, they end up back in the view through either this method or the below doCommand... methods.  insertText: is used to pass through text that was not a command.
 
-- (void)doCommandBySelector:(SEL)aSelector;
+- (void)doCommandBySelector:(SEL)selector;
     // Performs the given selector if possible.
 
 /************************* Standard bindable commands *************************/
@@ -255,6 +255,7 @@
 /* Perform a Quick Look on the text cursor position, selection, or whatever is appropriate for your view. If there are no Quick Look items, then call [[self nextResponder] tryToPerform:_cmd with:sender]; to pass the request up the responder chain. Eventually AppKit will attempt to perform a dictionary look up. Also see quickLookWithEvent: above.
 */
 - (void)quickLookPreviewItems:(nullable id)sender NS_AVAILABLE_MAC(10_8);
+
 @end
 
 @interface NSResponder(NSUndoSupport)
@@ -277,7 +278,7 @@
 
     - (void)didPresentErrorWithRecovery:(BOOL)didRecover contextInfo:(void *)contextInfo;
 
-The default implementation of this method always invokes [self willPresentError:error] to give subclassers an opportunity to customize error presentation. It then forwards the message, passing the customized error, to the next responder or, if there is no next responder, NSApp. NSApplication's override of this method invokes [[NSAlert alertWithError:theErrorToPresent] beginSheetModalForWindow:window modalDelegate:self didEndSelector:selectorForAPrivateMethod contextInfo:privateContextInfo]. When the user has dismissed the alert, the error's recovery attempter is sent an -attemptRecoveryFromError:optionIndex:delegate:didRecoverSelector:contextInfo: message, if the error had recovery options and a recovery delegate.
+The default implementation of this method always invokes [self willPresentError:error] to give subclassers an opportunity to customize error presentation. It then forwards the message, passing the customized error, to the next responder or, if there is no next responder, NSApp. NSApplication's override of this method invokes [[NSAlert alertWithError:errorToPresent] beginSheetModalForWindow:window modalDelegate:self didEndSelector:selectorForAPrivateMethod contextInfo:privateContextInfo]. When the user has dismissed the alert, the error's recovery attempter is sent an -attemptRecoveryFromError:optionIndex:delegate:didRecoverSelector:contextInfo: message, if the error had recovery options and a recovery delegate.
 
 Errors for which ([[error domain] isEqualToString:NSCocoaErrorDomain] && [error code]==NSUserCancelledError) are a special case,  because they do not actually represent errors and should not be presented as such to the user. NSApplication's override of this method does not present an alert to the user for these kinds of errors. Instead it merely invokes the delegate specifying didRecover==NO.
 
@@ -322,11 +323,20 @@
 @end
 
 
+@interface NSResponder(NSWindowTabbing)
+
+/* For automatic window tabbing: This method can be implemented in the responder chain. It is automatically called for tabbed windows when the plus button is clicked, and the next window that is created and shown will be placed in a tab. This can be implemented in an NSDocumentController subclass, or somewhere in the responder chain starting at NSWindow (such as NSWindow, the window delegate, the windowController, the NSApp delegate, etc. A plus button on tabbed windows will only be shown if this method exists in the responder chain.
+ */
+- (IBAction)newWindowForTab:(nullable id)sender NS_AVAILABLE_MAC(10_12);
+
+@end
+
+
 @interface NSResponder(NSDeprecated)
 
 /* This method is deprecated in 10.8 and higher. Historically it has always returned NO and not done anything on MacOS.
  */
-- (BOOL)performMnemonic:(NSString *)theString NS_DEPRECATED_MAC(10_0, 10_8);
+- (BOOL)performMnemonic:(NSString *)string NS_DEPRECATED_MAC(10_0, 10_8);
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRotationGestureRecognizer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRotationGestureRecognizer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRotationGestureRecognizer.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRotationGestureRecognizer.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSRotationGestureRecognizer.h
     Application Kit
-    Copyright (c) 2013-2015, Apple Inc.
+    Copyright (c) 2013-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -15,7 +15,7 @@
 @private
     NSPoint _location;
     NSPoint _reserved1;
-    NSInteger _rflags;
+    NSInteger _rflags __unused;
     CGFloat _rotation;
 #ifndef __OBJC2__
     NSInteger _reserved2;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRuleEditor.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRuleEditor.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRuleEditor.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRuleEditor.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSRuleEditor.h
 	Application Kit
-	Copyright (c) 2006-2015, Apple Inc.
+	Copyright (c) 2006-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -68,7 +68,7 @@
     NSInteger _subviewIndexOfDropLine;
     id _dropLineView;
     NSViewAnimation *_currentAnimation;
-    id _unused1;
+    id _unused1 __unused;
     NSString *_stringsFileName;
     id _standardLocalizer;
     id _headerLocalizer;
@@ -96,9 +96,9 @@
     Class _rowClass;
     id _boundArrayOwner;
     NSString *_boundArrayKeyPath;
-    id _ruleReserved1;
+    id _ruleReserved1 __unused;
     NSInteger _lastRow;
-    id _ruleReserved2;
+    id _ruleReserved2 __unused;
 }
 
 /* -- Configuring NSRuleEditor -- */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRulerMarker.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRulerMarker.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRulerMarker.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRulerMarker.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSRulerMarker.h
         Application Kit
-        Copyright (c) 1994-2015, Apple Inc.
+        Copyright (c) 1994-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -32,47 +32,61 @@
 
 /**************************** Initialization ****************************/
 
-- (instancetype)initWithRulerView:(NSRulerView *)ruler markerLocation:(CGFloat)location image:(NSImage *)image imageOrigin:(NSPoint)imageOrigin;
-    // Designated initializer.  Location is expressed in the client view's bounds coordinates.  Location is the x position if the ruler is horizontal or the y position if the ruler is vertical.  The image will not be scaled or rotated.  The image origin indicates the point in the image that will be placed on the ruler's baseline at the given location and is expressed in the image's coordinate system.  NSRulerMarkers are movable but not removable by default.  A removable object should have its dimmed image set.
+/* Designated initializer.  Location is expressed in the client view's bounds coordinates.  Location is the x position if the ruler is horizontal or the y position if the ruler is vertical.  The image will not be scaled or rotated.  The image origin indicates the point in the image that will be placed on the ruler's baseline at the given location and is expressed in the image's coordinate system.  NSRulerMarkers are movable but not removable by default.  A removable object should have its dimmed image set.
+ */
+- (instancetype)initWithRulerView:(NSRulerView *)ruler markerLocation:(CGFloat)location image:(NSImage *)image imageOrigin:(NSPoint)imageOrigin NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
+- (instancetype)init NS_UNAVAILABLE;
 
 /*********************** Query/Set basic attributes ***********************/
 
+/* Returns the ruler.
+ */
 @property (readonly, assign) NSRulerView *ruler;
-    // Returns the ruler.
 
 
+/* The location is set by the -init... method and the -setLocation: method.  Location is an x position for horizontal rulers or a y position for vertical rulers.  It is expressed in the client view's coordinate system.
+ */
 @property CGFloat markerLocation;
-    // The location is set by the -init... method and the -setLocation: method.  Location is an x position for horizontal rulers or a y position for vertical rulers.  It is expressed in the client view's coordinate system.
 
+/* The image is what's drawn in the ruler.
+ */
 @property (strong) NSImage *image;
-    // The image is what's drawn in the ruler.
 
+/* The image is drawn such that the image origin is on the baseline of the ruler at the object's location.
+ */
 @property NSPoint imageOrigin;
-    // The image is drawn such that the image origin is on the baseline of the ruler at the object's location.
 
+/* Objects are movable, but not removable by default.  Movable means the ruler object can be dragged by the user.  Removable means it can be deleted by the user.
+ */
 @property (getter=isMovable) BOOL movable;
 @property (getter=isRemovable) BOOL removable;
-    // Objects are movable, but not removable by default.  Movable means the ruler object can be dragged by the user.  Removable means it can be deleted by the user.
 
+/* Returns YES if the ruler object is currently being dragged.
+ */
 @property (getter=isDragging, readonly) BOOL dragging;
-    // Returns YES if the ruler object is currently being dragged.
 
+/* The representedObject of an NSRulerMarker is purely for the client's use.  It must be able to copy itself.  A represented object should be some small object.  The text object uses NSStrings for most ruler objects or NSTextTab objects for tab stops.
+ */
 @property (nullable, strong) id<NSCopying> representedObject;
-    // The representedObject of an NSRulerMarker is purely for the client's use.  It must be able to copy itself.  A represented object should be some small object.  The text object uses NSStrings for most ruler objects or NSTextTab objects for tab stops.
 
 /************************** Ruler facilities **************************/
 
+/* Returns the rect that would be occupied by the object's image in the ruler's bounds coordinates.  This takes the flippedness of the ruler into account.
+ */
 @property (readonly) NSRect imageRectInRuler;
-    // Returns the rect that would be occupied by the object's image in the ruler's bounds coordinates.  This takes the flippedness of the ruler into account.
 
+/* Returns the height or width (depending on the ruler's orientation) required in the ruler to display the object.
+ */
 @property (readonly) CGFloat thicknessRequiredInRuler;
-    // Returns the height or width (depending on the ruler's orientation) required in the ruler to display the object.
 
+/* Draws the object at it's current location.  Only rect needs to be drawn.
+ */
 - (void)drawRect:(NSRect)rect;
-    // Draws the object at it's current location.  Only rect needs to be drawn.
 
+/* Handles the given mmouseDown event.  Performs a modal tracking loop until mouseUp allowing the object to be moved, if movable or removed, if removable.
+ */
 - (BOOL)trackMouse:(NSEvent *)mouseDownEvent adding:(BOOL)isAdding;
-    // Handles the given mmouseDown event.  Performs a modal tracking loop until mouseUp allowing the object to be moved, if movable or removed, if removable.
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRulerView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRulerView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRulerView.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRulerView.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,8 +1,8 @@
 /*
-        NSRulerView.h
-        Application Kit
-        Copyright (c) 1994-2015, Apple Inc.
-        All rights reserved.
+    NSRulerView.h
+    Application Kit
+    Copyright (c) 1994-2016, Apple Inc.
+    All rights reserved.
 */
 
 #import <Foundation/NSArray.h>
@@ -54,7 +54,9 @@
 
 /**************************** Initialization ****************************/
 
-- (instancetype)initWithScrollView:(nullable NSScrollView *)scrollView orientation:(NSRulerOrientation)orientation;
+- (instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
+
+- (instancetype)initWithScrollView:(nullable NSScrollView *)scrollView orientation:(NSRulerOrientation)orientation NS_DESIGNATED_INITIALIZER;
     // The designated initializer.  A ruler's size is controlled by its NSScrollView. initWithFrame: is overridden to call this.  The view is initialized with an unrealistically small default frame which will be reset in due time by the NSScrollView.
 
 /**************************** Basic setup ****************************/
@@ -161,8 +163,8 @@
     // This is sent to the existing client before it is replaced by the new client.  The existing client can catch this to clean up any cached state it keeps while it is the client of a ruler.
 
 // This additional mapping allows mapping between location and point for clients with rotated coordinate system (i.e. vertical text view)
-- (CGFloat)rulerView:(NSRulerView *)ruler locationForPoint:(NSPoint)aPoint NS_AVAILABLE_MAC(10_7);
-- (NSPoint)rulerView:(NSRulerView *)ruler pointForLocation:(CGFloat)aPoint NS_AVAILABLE_MAC(10_7);
+- (CGFloat)rulerView:(NSRulerView *)ruler locationForPoint:(NSPoint)point NS_AVAILABLE_MAC(10_7);
+- (NSPoint)rulerView:(NSRulerView *)ruler pointForLocation:(CGFloat)point NS_AVAILABLE_MAC(10_7);
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRunningApplication.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRunningApplication.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRunningApplication.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRunningApplication.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSRunningApplication.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -56,9 +56,9 @@
 NS_CLASS_AVAILABLE(10_6, NA)
 @interface NSRunningApplication : NSObject {
     @private
-    id _superReserved;
-    __strong void *_asn;
-    __strong void **_helpers;
+    id _superReserved __unused;
+    void *_asn;
+    void **_helpers;
     id _obsInfo;
     NSLock *_lock;
     NSString *_bundleID;
@@ -84,7 +84,7 @@
 	unsigned activationPolicy:3;
         unsigned reserved1:19;
     } _aflags;
-    id _appReserved;
+    id _appReserved __unused;
 }
 
 /* Indicates that the process is an exited application.  This is observable through KVO. */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSavePanel.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSavePanel.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSavePanel.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSavePanel.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSSavePanel.h
     Application Kit
-    Copyright (c) 1994-2015, Apple Inc.
+    Copyright (c) 1994-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -89,7 +89,7 @@
     NSSavePanelAuxiliary *_spAuxiliaryStorage;
     
 @private
-    char _unused:1;
+    char _unused:1 __unused;
 #if !__LP64__
     char _reserved[4];
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScreen.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScreen.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScreen.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScreen.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSScreen.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -44,12 +44,12 @@
 
 /* Convert to/from the device pixel aligned coordinates sytem of a display 
  */
-- (NSRect)convertRectToBacking:(NSRect)aRect NS_AVAILABLE_MAC(10_7);
-- (NSRect)convertRectFromBacking:(NSRect)aRect NS_AVAILABLE_MAC(10_7);
+- (NSRect)convertRectToBacking:(NSRect)rect NS_AVAILABLE_MAC(10_7);
+- (NSRect)convertRectFromBacking:(NSRect)rect NS_AVAILABLE_MAC(10_7);
 
 /* Uses NSIntegralRectWithOptions() to produce a pixel aligned rectangle on the target screen from the given input rectangle in global screen coordinates.
  */
-- (NSRect)backingAlignedRect:(NSRect)aRect options:(NSAlignmentOptions)options NS_AVAILABLE_MAC(10_7);
+- (NSRect)backingAlignedRect:(NSRect)rect options:(NSAlignmentOptions)options NS_AVAILABLE_MAC(10_7);
 
 /* Returns the scale factor representing the number of backing store pixels corresponding to each linear unit in screen space on this NSScreen. This method is provided for rare cases when the explicit scale factor is needed.  Please use -convert*ToBacking: methods whenever possible. 
  */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScrollView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScrollView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScrollView.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScrollView.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSScrollView.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 #import <Foundation/NSDate.h>
@@ -91,7 +91,7 @@
     NSView *    _cornerView;
     id          _ruler;
     _SFlags     _sFlags;
-    __strong void *_extraIvars;
+    id          _extraIvars;
     
     // new rulers
     NSRulerView *_horizontalRuler;
@@ -103,23 +103,23 @@
 
 /* Returns the NSScrollView frame size that yields the specified contentView frame size.  This method should be used in preference to the deprecated +frameSizeForContentSize:hasHorizontalScroller:hasVerticalScroller:borderType:, which makes assumptions about the scrollers' classes, control size, and style.  The "horizontalScrollerClass" parameter should specify the class of horizontal scroller to use if the NSScrollView will have a horizontal scroller, or Nil if it will not.  Likewise for the "verticalScrollerClass" parameter.
 */
-+ (NSSize)frameSizeForContentSize:(NSSize)cSize horizontalScrollerClass:(nullable Class)horizontalScrollerClass verticalScrollerClass:(nullable Class)verticalScrollerClass borderType:(NSBorderType)aType controlSize:(NSControlSize)controlSize scrollerStyle:(NSScrollerStyle)scrollerStyle NS_AVAILABLE_MAC(10_7);
++ (NSSize)frameSizeForContentSize:(NSSize)cSize horizontalScrollerClass:(nullable Class)horizontalScrollerClass verticalScrollerClass:(nullable Class)verticalScrollerClass borderType:(NSBorderType)type controlSize:(NSControlSize)controlSize scrollerStyle:(NSScrollerStyle)scrollerStyle NS_AVAILABLE_MAC(10_7);
 
 /* Returns the contentView frame size that yields the specified NSScrollView frame size.  This method should be used in preference to the deprecated +contentSizeForFrameSize:hasHorizontalScroller:hasVerticalScroller:borderType: method, which makes assumptions about the scrollers' classes, control size, and style.  The "horizontalScrollerClass" parameter should specify the class of horizontal scroller to use if the NSScrollView will have a horizontal scroller, or Nil if it will not.  Likewise for the "verticalScrollerClass" parameter.
 */
-+ (NSSize)contentSizeForFrameSize:(NSSize)fSize horizontalScrollerClass:(nullable Class)horizontalScrollerClass verticalScrollerClass:(nullable Class)verticalScrollerClass borderType:(NSBorderType)aType controlSize:(NSControlSize)controlSize scrollerStyle:(NSScrollerStyle)scrollerStyle NS_AVAILABLE_MAC(10_7);
++ (NSSize)contentSizeForFrameSize:(NSSize)fSize horizontalScrollerClass:(nullable Class)horizontalScrollerClass verticalScrollerClass:(nullable Class)verticalScrollerClass borderType:(NSBorderType)type controlSize:(NSControlSize)controlSize scrollerStyle:(NSScrollerStyle)scrollerStyle NS_AVAILABLE_MAC(10_7);
 
 /* Returns the NSScrollView frame size that yields the specified contentView frame size.  This method assumes scrollers of NSRegularControlSize, that are not subclassed in a way that affects their metrics (scrollerWidth), and also assumes that scrollers of the current [NSScroller preferredScrollerStyle] will be used, which may not be the case if conditions such as legacy scroller subclassing or presence of accessory views force fallback to NSScrollerStyleLegacy for a particular NSScrollView instance.  Since those assumptions will produce incorrect results for some cases, this method should be considered deprecated; use +frameSizeForContentSize:horizontalScrollerClass:verticalScrollerClass:borderType:controlSize:scrollerStyle:, which provides for full specification of the relevant parameters, instead.
 */
-+ (NSSize)frameSizeForContentSize:(NSSize)cSize hasHorizontalScroller:(BOOL)hFlag hasVerticalScroller:(BOOL)vFlag borderType:(NSBorderType)aType NS_DEPRECATED_MAC(10_0, 10_7, "Use +frameSizeForContentSize:horizontalScrollerClass:verticalScrollerClass:borderType:controlSize:scrollerStyle: instead");
++ (NSSize)frameSizeForContentSize:(NSSize)cSize hasHorizontalScroller:(BOOL)hFlag hasVerticalScroller:(BOOL)vFlag borderType:(NSBorderType)type NS_DEPRECATED_MAC(10_0, 10_7, "Use +frameSizeForContentSize:horizontalScrollerClass:verticalScrollerClass:borderType:controlSize:scrollerStyle: instead");
 
 /*Returns the contentView frame size that yields the specified NSScrollView frame size.  This method assumes scrollers of NSRegularControlSize, that are not subclassed in a way that affects their metrics (scrollerWidth), and also assumes that scrollers of the current [NSScroller preferredScrollerStyle] will be used, which may not be the case if conditions such as legacy scroller subclassing or presence of accessory views force fallback to NSScrollerStyleLegacy for a particular NSScrollView instance.  Since those assumptions will produce incorrect results for some cases, this method should be considered deprecated; use +contentSizeForFrameSize:horizontalScrollerClass:verticalScrollerClass:borderType:controlSize:scrollerStyle:, which provides for full specification of the relevant parameters, instead.
 */
-+ (NSSize)contentSizeForFrameSize:(NSSize)fSize hasHorizontalScroller:(BOOL)hFlag hasVerticalScroller:(BOOL)vFlag borderType:(NSBorderType)aType NS_DEPRECATED_MAC(10_0, 10_7, "+contentSizeForFrameSize:horizontalScrollerClass:verticalScrollerClass:borderType:controlSize:scrollerStyle: instead");
++ (NSSize)contentSizeForFrameSize:(NSSize)fSize hasHorizontalScroller:(BOOL)hFlag hasVerticalScroller:(BOOL)vFlag borderType:(NSBorderType)type NS_DEPRECATED_MAC(10_0, 10_7, "+contentSizeForFrameSize:horizontalScrollerClass:verticalScrollerClass:borderType:controlSize:scrollerStyle: instead");
 
 @property (readonly) NSRect documentVisibleRect;
 @property (readonly) NSSize contentSize;
-@property (nullable, assign) id /* NSView * */ documentView;
+@property (nullable, assign) __kindof NSView *documentView;
 @property (strong) NSClipView *contentView;
 @property (nullable, strong) NSCursor *documentCursor;
 @property NSBorderType borderType;
@@ -139,7 +139,7 @@
 @property BOOL scrollsDynamically;
 - (void)tile;
 - (void)reflectScrolledClipView:(NSClipView *)cView;
-- (void)scrollWheel:(NSEvent *)theEvent;
+- (void)scrollWheel:(NSEvent *)event;
 
 /* An NSScrollView's scrollerStyle determines the style of scrollers that it will use.  AppKit sets this property automatically at runtime, based on the user's "Show scroll bars" setting and (if relevant) the set of connected pointing devices and their configured scroll capabilities, as determined by [NSScroller preferredScrollerStyle].  Setting an NSScrollView's scrollerStyle sets the scrollerStyle of its horizontalScroller and verticalScroller to match the new value.  If the NSScrollView subsequently creates or is assigned a new horizontalScroller or verticalScroller, they will at that time be assigned the same scrollerStyle that was given to the NSScrollView.
 */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScroller.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScroller.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScroller.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScroller.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSScroller.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -144,9 +144,9 @@
 - (void)drawKnob;
 - (void)drawKnobSlotInRect:(NSRect)slotRect highlight:(BOOL)flag;
 - (void)highlight:(BOOL)flag;                                       // has no effect on 10.7
-- (NSScrollerPart)testPart:(NSPoint)thePoint;
-- (void)trackKnob:(NSEvent *)theEvent;
-- (void)trackScrollButtons:(NSEvent *)theEvent;                     // not invoked on 10.7
+- (NSScrollerPart)testPart:(NSPoint)point;
+- (void)trackKnob:(NSEvent *)event;
+- (void)trackScrollButtons:(NSEvent *)event;                     // not invoked on 10.7
 @property (readonly) NSScrollerPart hitPart;
 @property CGFloat knobProportion;
 - (void)setKnobProportion:(CGFloat)proportion NS_AVAILABLE_MAC(10_5);
@@ -156,7 +156,7 @@
 @interface NSScroller(NSDeprecated)
 /* A method that was deprecated in Mac OS 10.5. To maintain binary compatibility, AppKit will continue to invoke overrides of this method. Code that targets Mac OS 10.5 and later should use -setDoubleValue: and -setKnobProportion: instead, and eliminate any overrides of -setFloatValue:knobProportion:. Code that needs to remain compatible with Mac OS 10.4 and earlier should continue to use -setFloatValue:knobProportion:. 
 */
-- (void)setFloatValue:(float)aFloat knobProportion:(CGFloat)proportion NS_DEPRECATED_MAC(10_0, 10_5);
+- (void)setFloatValue:(float)value knobProportion:(CGFloat)proportion NS_DEPRECATED_MAC(10_0, 10_5);
 @end
 
 /* Posted when the preferred scroller style changes.  The notification object is private; disregard it.  Consult NSScroller's +preferredScrollerStyle method when this notification is received, or thereafter, to determine the new scroller style to use.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSearchField.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSearchField.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSearchField.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSearchField.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSSearchField.h
     Application Kit
-    Copyright (c) 2003-2015, Apple Inc.
+    Copyright (c) 2003-2016, Apple Inc.
     All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSearchFieldCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSearchFieldCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSearchFieldCell.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSearchFieldCell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSSearchFieldCell.h
 	Application Kit
-	Copyright (c) 2003-2015, Apple Inc.
+	Copyright (c) 2003-2016, Apple Inc.
 	All rights reserved.
  */
 
@@ -58,9 +58,14 @@
     unsigned int _reserved1;
     unsigned int _reserved2;
     unsigned int _reserved3;
-    unsigned int _reserved4;    
+    unsigned int _reserved4 __unused;
 }
 
+
+- (instancetype)initTextCell:(NSString *)string NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
+- (instancetype)initImageCell:(nullable NSImage *)image NS_UNAVAILABLE;
+
 @property (nullable, strong) NSButtonCell *searchButtonCell;
     // can modify, set or cancel search button.
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSecureTextField.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSecureTextField.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSecureTextField.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSecureTextField.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSSecureTextField.h
         Application Kit
-        Copyright (c) 1995-2015, Apple Inc.
+        Copyright (c) 1995-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -17,7 +17,7 @@
 /*All instance variables are private*/
     @private
     BOOL _echosBullets;
-    BOOL _csMode;
+    BOOL _csMode __unused;
 }
 
 @property BOOL echosBullets;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSegmentedCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSegmentedCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSegmentedCell.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSegmentedCell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSSegmentedCell.h
     Application Kit
-    Copyright (c) 2003-2015, Apple Inc.
+    Copyright (c) 2003-2016, Apple Inc.
     All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSegmentedControl.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSegmentedControl.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSegmentedControl.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSegmentedControl.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSSegmentedControl.h
 	Application Kit
-	Copyright (c) 2003-2015, Apple Inc.
+	Copyright (c) 2003-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -81,4 +81,28 @@
 
 @end
 
+@interface NSSegmentedControl (NSSegmentedControlConvenience)
+
+/*!
+ Creates a standard segmented control containing one segment for each of the provided labels.
+ @param labels An array of localized label strings to use for the control's segments.
+ @param trackingMode The selection mode for the control. The NSSegmentSwitchTracking enum describes the possible values and their effects.
+ @param target The target object that receives action messages from the control.
+ @param action The action message sent by the control.
+ @return An initialized segmented control.
+ */
++ (instancetype)segmentedControlWithLabels:(NSArray<NSString *> *)labels trackingMode:(NSSegmentSwitchTracking)trackingMode target:(nullable id)target action:(nullable SEL)action NS_AVAILABLE_MAC(10_12);
+
+/*!
+ Creates a standard segmented control containing one segment for each of the provided images. To ensure accessibility for this control, set the accessibilityDescription property on each of the provided images.
+ @param images An array of image objects to use for the control's segments.
+ @param trackingMode The selection mode for the control. The NSSegmentSwitchTracking enum describes the possible values and their effects.
+ @param target The target object that receives action messages from the control.
+ @param action The action message sent by the control.
+ @return An initialized segmented control.
+ */
++ (instancetype)segmentedControlWithImages:(NSArray<NSImage *> *)images trackingMode:(NSSegmentSwitchTracking)trackingMode target:(nullable id)target action:(nullable SEL)action NS_AVAILABLE_MAC(10_12);
+
+@end
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSShadow.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSShadow.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSShadow.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSShadow.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSShadow.h
         Application Kit
-	Copyright (c) 2002-2015, Apple Inc.
+	Copyright (c) 2002-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSharingService.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSharingService.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSharingService.h	2015-08-26 04:17:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSharingService.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,17 +1,19 @@
 /*
  NSSharingService.h
  Application Kit
- Copyright (c) 2011-2015, Apple Inc.
+ Copyright (c) 2011-2016, Apple Inc.
  All rights reserved.
  */
 
 #import <AppKit/AppKitDefines.h>
 #import <AppKit/NSPasteboard.h>
 #import <Foundation/NSGeometry.h>
+#import <Foundation/NSItemProvider.h>
 #import <Foundation/NSObject.h>
 #import <Foundation/NSArray.h>
 
 @class NSString, NSImage, NSView, NSError, NSWindow;
+@class CKShare, CKContainer;
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -41,6 +43,12 @@
 APPKIT_EXTERN NSString * const NSSharingServiceNamePostVideoOnYouku NS_AVAILABLE_MAC(10_8);
 APPKIT_EXTERN NSString * const NSSharingServiceNamePostVideoOnTudou NS_AVAILABLE_MAC(10_8);
 
+/* This service differs from other NSSharingServices in that it allows the user to establishes a persistent sharing session for the specified items with potentially many participants, instead of sending a copy of the items. You can invoke this service with an NSItemProvider that has registered a CKShare & CKContainer via either -registerCloudKitShare:container: or -registerCloudKitShareWithPreparationHandler:. (Registering other types on the same provider to enable other sharing services is allowed.)
+ 
+When performed, this service gives the user the opportunity to invite participants and start sharing. If the content is already shared it instead allows the user to view or modify participation or stop sharing. To detect changes the service makes to the CKShare, implement -sharingService:didSaveShare: and -sharingService:didStopSharing:.
+ */
+APPKIT_EXTERN NSString * const NSSharingServiceNameCloudSharing NS_AVAILABLE_MAC(10_12);
+
 
 @protocol NSSharingServiceDelegate;
 
@@ -131,12 +139,76 @@
 /* The following methods are invoked when the service is performed and the sharing window pops up, to present a transition between the original items and the sharing window.
  */
 - (NSRect)sharingService:(NSSharingService *)sharingService sourceFrameOnScreenForShareItem:(id)item;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_APPKIT_EPOCH) && SWIFT_SDK_OVERLAY_APPKIT_EPOCH >= 6)
+/* When non-nil, the image returned would be used for the transitioning animation. When nil, the transitioning animation is disabled.
+ */
+- (nullable NSImage *)sharingService:(NSSharingService *)sharingService transitionImageForShareItem:(id)item contentRect:(NSRect *)contentRect;
+#else
 - (NSImage *)sharingService:(NSSharingService *)sharingService transitionImageForShareItem:(id)item contentRect:(NSRect *)contentRect;
+#endif
 - (nullable NSWindow *)sharingService:(NSSharingService *)sharingService sourceWindowForShareItems:(NSArray *)items sharingContentScope:(NSSharingContentScope *)sharingContentScope;
 
+/* The following method is invoked when the service is performed and wants to display its contents in a popover. The delegate should return the view that will act as the anchor of the popover, along with the target rectangle within the bounds of that view and preferred edge of that rectangle for the popover to appear. The delegate may also return nil, indicating that there is no anchoring view currently available, in which case the service may attempt to display the service via some other means.
+ 
+ The service named NSSharingServiceNameCloudSharing prefers to display itself using a popover anchored to an "iCloud Sharing" or "Share" button. If no such button is available or visible, return nil.
+ */
+- (nullable NSView *)anchoringViewForSharingService:(NSSharingService *)sharingService showRelativeToRect:(NSRect *)positioningRect preferredEdge:(NSRectEdge *)preferredEdge;
+
 @end
 
 
+typedef NS_OPTIONS(NSUInteger, NSCloudKitSharingServiceOptions) {
+    NSCloudKitSharingServiceStandard = 0, // Allow the user to configure the share with the standard set of options
+    
+    NSCloudKitSharingServiceAllowPublic = 1 << 0, // The user is allowed to share publicly
+    NSCloudKitSharingServiceAllowPrivate = 1 << 1, // The user is allowed to share privately
+    
+    NSCloudKitSharingServiceAllowReadOnly = 1 << 4, // The user is allowed to grant participants read-only permissions
+    NSCloudKitSharingServiceAllowReadWrite = 1 << 5, // The user is allowed to grant participants read/write permissions.
+    
+} NS_ENUM_AVAILABLE_MAC(10_12);
+
+@protocol NSCloudSharingServiceDelegate <NSSharingServiceDelegate>
+@optional
+
+/* When an NSSharingServiceNameCloudSharing sharing service is dismissed it will invoke this method on the delegate, with an error if there was any. If the delegate implements this method, NSSharingServiceNameCloudSharing will not send -sharingService:didFailToShareItems:error: or -sharingService:didShareItems:.
+ */
+- (void)sharingService:(NSSharingService *)sharingService didCompleteForItems:(NSArray *)items error:(nullable NSError *)error;
+
+#if __OBJC2__
+
+/* The options returned by this method describe how the user is allowed to configure the share: whether the share is public or private, and whether participants have read-only or read/write permissions. If this method is not implemented, NSCloudKitSharingServiceStandard is assumed.
+ */
+- (NSCloudKitSharingServiceOptions)optionsForSharingService:(NSSharingService *)cloudKitSharingService shareProvider:(NSItemProvider *)provider;
+
+#endif
+
+/* When an NSSharingServiceNameCloudSharing sharing service successfully saves modifications to the CKShare, it will invoke this method on the delegate with the last-known state of the CKShare on the server.
+ */
+- (void)sharingService:(NSSharingService *)sharingService didSaveShare:(CKShare *)share;
+
+/* When an NSSharingServiceNameCloudSharing sharing service stops sharing it will delete the CKShare from the server, then invoke this method on the delegate with the last-known state of the CKShare.
+ */
+- (void)sharingService:(NSSharingService *)sharingService didStopSharing:(CKShare *)share;
+
+@end
+
+
+#if __OBJC2__
+
+@interface NSItemProvider (NSCloudKitSharing)
+
+/* Use this method when you want to share a collection of CKRecords but don't currently have a CKShare. When the preparationHandler is called, you should create a new CKShare with the appropriate root CKRecord. After ensuring the share and all records have been saved to the server, invoke the preparationCompletionHandler with either the resulting CKShare and its CKContainer, or an NSError if saving failed. Invoking the service with a CKShare registered with this method will prompt the user to start sharing.
+ */
+- (void)registerCloudKitShareWithPreparationHandler:(void (^_Nonnull)(void (^ _Nonnull preparationCompletionHandler)(CKShare * _Nullable, CKContainer * _Nullable, NSError * _Nullable)))preparationHandler NS_AVAILABLE_MAC(10_12);
+
+/* Use this method when you have a CKShare that is already saved to the server. Invoking the service with a CKShare registerd with this method will allow the owner to make modifications to the share settings, or will allow a participant to view the share settings.
+ */
+- (void)registerCloudKitShare:(CKShare *)share container:(CKContainer *)container NS_AVAILABLE_MAC(10_12);
+
+@end
+
+#endif
 
 
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSimpleHorizontalTypesetter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSimpleHorizontalTypesetter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSimpleHorizontalTypesetter.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSimpleHorizontalTypesetter.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,6 +1,6 @@
 /* 
     NSSimpleHorizontalTypesetter.h
-    Copyright (c) 1993-2015, Apple Inc.
+    Copyright (c) 1993-2016, Apple Inc.
     All rights reserved. 
  
     A concrete class to lay glyphs out in horizontal boxes.
@@ -228,9 +228,9 @@
 */
 - (void)typesetterLaidOneGlyph:(NSTypesetterGlyphInfo *)gl;
 
-/* If implemented by subclasses, this is called within "layoutGlyphsInHorizontalLineFragment:baseline:" after laying out each line fragment, immediately before "setLineFragmentRect:forGlyphRange:usedRect:" in the NSLayoutManager is called to record the used line fragment rectangles.  This is intended for subclasses to be able to affect e.g., linespacing globally.  The "used" rect is expected to be smaller than or equal to the "aRect".
+/* If implemented by subclasses, this is called within "layoutGlyphsInHorizontalLineFragment:baseline:" after laying out each line fragment, immediately before "setLineFragmentRect:forGlyphRange:usedRect:" in the NSLayoutManager is called to record the used line fragment rectangles.  This is intended for subclasses to be able to affect e.g., linespacing globally.  The "used" rect is expected to be smaller than or equal to the "rect".
 */
-- (void) willSetLineFragmentRect:(NSRect *)aRect forGlyphRange:(NSRange)aRange usedRect:(NSRect *)bRect;
+- (void) willSetLineFragmentRect:(NSRect *)rect forGlyphRange:(NSRange)range usedRect:(NSRect *)bRect;
 
 @end
 #endif /* __LP64__ || MAC_OS_X_VERSION_MIN_REQUIRED > MAC_OS_X_VERSION_10_4 */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSlider.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSlider.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSlider.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSlider.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSSlider.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -18,21 +18,13 @@
 @property double maxValue;
 @property double altIncrementValue;
 @property (readonly) CGFloat knobThickness;
-@property (getter=isVertical, readonly) NSInteger vertical;
-- (BOOL)acceptsFirstMouse:(nullable NSEvent *)theEvent;
+- (BOOL)acceptsFirstMouse:(nullable NSEvent *)event;
+@property (readwrite, getter=isVertical) BOOL vertical NS_AVAILABLE_MAC(10_12);
 
-/* These methods have never done anything, and are formally deprecated as of 10.9*/
-- (void)setTitleCell:(null_unspecified NSCell *)aCell NS_DEPRECATED_MAC(10_0, 10_9);
-- (null_unspecified id)titleCell NS_DEPRECATED_MAC(10_0, 10_9);
-- (void)setTitleColor:(null_unspecified NSColor *)newColor NS_DEPRECATED_MAC(10_0, 10_9);
-- (null_unspecified NSColor *)titleColor NS_DEPRECATED_MAC(10_0, 10_9);
-- (void)setTitleFont:(null_unspecified NSFont *)fontObj NS_DEPRECATED_MAC(10_0, 10_9);
-- (null_unspecified NSFont *)titleFont NS_DEPRECATED_MAC(10_0, 10_9);
-- (null_unspecified NSString *)title NS_DEPRECATED_MAC(10_0, 10_9);
-- (void)setTitle:(null_unspecified NSString *)aString NS_DEPRECATED_MAC(10_0, 10_9);
-- (void)setKnobThickness:(CGFloat)aFloat NS_DEPRECATED_MAC(10_0, 10_9);
-- (void)setImage:(null_unspecified NSImage *)backgroundImage NS_DEPRECATED_MAC(10_0, 10_9);
-- (null_unspecified NSImage *)image NS_DEPRECATED_MAC(10_0, 10_9);
+@end
+
+@interface NSSlider (NSSliderVerticalGetter)
+@property (readonly, getter=isVertical) BOOL vertical NS_AVAILABLE_MAC(10_0);
 @end
 
 @interface NSSlider(NSTickMarkSupport)
@@ -67,4 +59,43 @@
 
 @end
 
+@interface NSSlider(NSSliderConvenience)
+
+/*!
+ Creates a continuous horizontal slider over the range 0.0 to 1.0. The default value is 0.0.
+ @param target The target object that receives action messages from the control.
+ @param action The action message sent by the control.
+ @return An initialized slider control.
+ */
++ (instancetype)sliderWithTarget:(nullable id)target action:(nullable SEL)action NS_AVAILABLE_MAC(10_12);
+
+/*!
+ Creates a continuous horizontal slider that represents values over a specified range.
+ @param value The initial value displayed by the control.
+ @param minValue The minimum value represented by the control.
+ @param maxValue The maximum value represented by the control.
+ @param target The target object that receives action messages from the control.
+ @param action The action message sent by the control.
+ @return An initialized slider control.
+ */
++ (instancetype)sliderWithValue:(double)value minValue:(double)minValue maxValue:(double)maxValue target:(nullable id)target action:(nullable SEL)action NS_AVAILABLE_MAC(10_12);
+
+
+@end
+
+@interface NSSlider (NSSliderDeprecated)
+/* These methods have never done anything, and are formally deprecated as of 10.9*/
+- (void)setTitleCell:(null_unspecified NSCell *)cell NS_DEPRECATED_MAC(10_0, 10_9);
+- (null_unspecified id)titleCell NS_DEPRECATED_MAC(10_0, 10_9);
+- (void)setTitleColor:(null_unspecified NSColor *)newColor NS_DEPRECATED_MAC(10_0, 10_9);
+- (null_unspecified NSColor *)titleColor NS_DEPRECATED_MAC(10_0, 10_9);
+- (void)setTitleFont:(null_unspecified NSFont *)fontObj NS_DEPRECATED_MAC(10_0, 10_9);
+- (null_unspecified NSFont *)titleFont NS_DEPRECATED_MAC(10_0, 10_9);
+- (null_unspecified NSString *)title NS_DEPRECATED_MAC(10_0, 10_9);
+- (void)setTitle:(null_unspecified NSString *)string NS_DEPRECATED_MAC(10_0, 10_9);
+- (void)setKnobThickness:(CGFloat)thickness NS_DEPRECATED_MAC(10_0, 10_9);
+- (void)setImage:(null_unspecified NSImage *)backgroundImage NS_DEPRECATED_MAC(10_0, 10_9);
+- (null_unspecified NSImage *)image NS_DEPRECATED_MAC(10_0, 10_9);
+@end
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSliderCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSliderCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSliderCell.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSliderCell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,22 +1,21 @@
 /*
 	NSSliderCell.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
 #import <AppKit/NSActionCell.h>
 
 typedef NS_ENUM(NSUInteger, NSTickMarkPosition) {
-    NSTickMarkBelow = 0,
-    NSTickMarkAbove = 1,
-    NSTickMarkLeft  = NSTickMarkAbove,
-    NSTickMarkRight = NSTickMarkBelow
+    NSTickMarkPositionBelow = 0,
+    NSTickMarkPositionAbove = 1,
+    NSTickMarkPositionLeading = NSTickMarkPositionAbove,
+    NSTickMarkPositionTrailing = NSTickMarkPositionBelow
 };
-
 typedef NS_ENUM(NSUInteger, NSSliderType) {
-    NSLinearSlider   = 0,
-    NSCircularSlider = 1
+    NSSliderTypeLinear = 0,
+    NSSliderTypeCircular = 1,
 };
 
 @interface NSSliderCell : NSActionCell
@@ -34,7 +33,7 @@
     struct __sliderCellFlags {
         unsigned int weAreVertical:1;
         unsigned int weAreVerticalSet:1;
-        unsigned int reserved1:1;
+        unsigned int weHaveStickyOrientation:1;
         unsigned int isPressed:1;
         unsigned int allowsTickMarkValuesOnly:1;
         unsigned int tickMarkPosition:1;
@@ -55,27 +54,23 @@
 @property double altIncrementValue;
 
 @property NSSliderType sliderType;
-@property (getter=isVertical, readonly) NSInteger vertical;
+@property (readwrite, getter=isVertical) BOOL vertical NS_AVAILABLE_MAC(10_11);
 
 @property (readonly) NSRect trackRect;
 
 @property (readonly) CGFloat knobThickness;
+
 - (NSRect)knobRectFlipped:(BOOL)flipped;
+- (NSRect)barRectFlipped:(BOOL)flipped NS_AVAILABLE_MAC(10_9);
+
 - (void)drawKnob:(NSRect)knobRect;
 - (void)drawKnob;
-- (NSRect)barRectFlipped:(BOOL)flipped NS_AVAILABLE_MAC(10_9);
-- (void)drawBarInside:(NSRect)aRect flipped:(BOOL)flipped;
+- (void)drawBarInside:(NSRect)rect flipped:(BOOL)flipped;
 
-/* These methods have never done anything, and are formally deprecated as of 10.9*/
-- (void)setTitleColor:(NSColor *)newColor NS_DEPRECATED_MAC(10_0, 10_9);
-- (NSColor *)titleColor NS_DEPRECATED_MAC(10_0, 10_9);
-- (void)setTitleFont:(NSFont *)fontObj NS_DEPRECATED_MAC(10_0, 10_9);
-- (NSFont *)titleFont NS_DEPRECATED_MAC(10_0, 10_9);
-- (NSString *)title NS_DEPRECATED_MAC(10_0, 10_9);
-- (void)setTitle:(NSString *)aString NS_DEPRECATED_MAC(10_0, 10_9);
-- (void)setTitleCell:(NSCell *)aCell NS_DEPRECATED_MAC(10_0, 10_9);
-- (id)titleCell NS_DEPRECATED_MAC(10_0, 10_9);
-- (void)setKnobThickness:(CGFloat)aFloat NS_DEPRECATED_MAC(10_0, 10_9);
+@end
+
+@interface NSSliderCell (NSSliderCellVerticalGetter)
+@property (readonly, getter=isVertical) BOOL vertical NS_AVAILABLE_MAC(10_0);
 @end
 
 @interface NSSliderCell(NSTickMarkSupport)
@@ -111,3 +106,24 @@
 - (void)drawTickMarks NS_AVAILABLE_MAC(10_9);
 
 @end
+
+/* These methods have never done anything, and are formally deprecated as of 10.9 */
+@interface NSSliderCell (NSDeprecated)
+- (void)setTitleColor:(NSColor *)newColor NS_DEPRECATED_MAC(10_0, 10_9);
+- (NSColor *)titleColor NS_DEPRECATED_MAC(10_0, 10_9);
+- (void)setTitleFont:(NSFont *)fontObj NS_DEPRECATED_MAC(10_0, 10_9);
+- (NSFont *)titleFont NS_DEPRECATED_MAC(10_0, 10_9);
+- (NSString *)title NS_DEPRECATED_MAC(10_0, 10_9);
+- (void)setTitle:(NSString *)string NS_DEPRECATED_MAC(10_0, 10_9);
+- (void)setTitleCell:(NSCell *)cell NS_DEPRECATED_MAC(10_0, 10_9);
+- (id)titleCell NS_DEPRECATED_MAC(10_0, 10_9);
+- (void)setKnobThickness:(CGFloat)thickness NS_DEPRECATED_MAC(10_0, 10_9);
+@end
+
+static const NSTickMarkPosition NSTickMarkBelow API_DEPRECATED_WITH_REPLACEMENT("NSTickMarkPositionBelow", macosx(10.0, 10.12)) = NSTickMarkPositionBelow;
+static const NSTickMarkPosition NSTickMarkAbove API_DEPRECATED_WITH_REPLACEMENT("NSTickMarkPositionAbove", macosx(10.0, 10.12)) = NSTickMarkPositionAbove;
+static const NSTickMarkPosition NSTickMarkLeft API_DEPRECATED_WITH_REPLACEMENT("NSTickMarkPositionLeading", macosx(10.0, 10.12)) = NSTickMarkPositionLeading;
+static const NSTickMarkPosition NSTickMarkRight API_DEPRECATED_WITH_REPLACEMENT("NSTickMarkPositionTrailing", macosx(10.0, 10.12)) = NSTickMarkPositionTrailing;
+
+static const NSSliderType NSLinearSlider API_DEPRECATED_WITH_REPLACEMENT("NSSliderTypeLinear", macosx(10.0, 10.12)) = NSSliderTypeLinear;
+static const NSSliderType NSCircularSlider API_DEPRECATED_WITH_REPLACEMENT("NSSliderTypeCircular", macosx(10.0, 10.12)) = NSSliderTypeCircular;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSound.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSound.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSound.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSound.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSSound.h
 	Application Kit
-	Copyright (c) 1997-2015, Apple Inc.
+	Copyright (c) 1997-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -107,7 +107,7 @@
 @protocol NSSoundDelegate <NSObject>
 @optional
 
-- (void)sound:(NSSound *)sound didFinishPlaying:(BOOL)aBool;
+- (void)sound:(NSSound *)sound didFinishPlaying:(BOOL)flag;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpeechRecognizer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpeechRecognizer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpeechRecognizer.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpeechRecognizer.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSSpeechRecognizer.h
 	Application Kit
-	Copyright (c) 2003-2015, Apple Inc.
+	Copyright (c) 2003-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpeechSynthesizer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpeechSynthesizer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpeechSynthesizer.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpeechSynthesizer.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSSpeechSynthesizer.h
 	Application Kit
-	Copyright (c) 2003-2015, Apple Inc.
+	Copyright (c) 2003-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpellChecker.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpellChecker.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpellChecker.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpellChecker.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSSpellChecker.h
         Application Kit
-        Copyright (c) 1990-2015, Apple Inc.
+        Copyright (c) 1990-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -33,13 +33,19 @@
     id _guessesBrowser;
     id _wordField;
     id _languagePopUp;
+#ifndef __OBJC2__
     id _reserved1;
+#endif
     id _panel;
+#ifndef __OBJC2__
     id _reserved2;
+#endif
     id _correctButton;
     id _guessButton;
     id _ignoreButton;
+#ifndef __OBJC2__
     id _reserved3;
+#endif
     id _languagesBrowser;
     id _quotesBrowser;
     id _replacementsBrowser;
@@ -61,7 +67,9 @@
     } _scFlags;
     
     id _substitutionsPanel;
+#ifndef __OBJC2__
     id _reserved4;
+#endif
     id _learnButton;
     id _infoField;
     id _grammarControl;
@@ -104,6 +112,8 @@
 APPKIT_EXTERN NSString * NSTextCheckingDocumentTitleKey      NS_AVAILABLE_MAC(10_6);  // NSString, a title to be associated with the document
 APPKIT_EXTERN NSString * NSTextCheckingDocumentAuthorKey     NS_AVAILABLE_MAC(10_6);  // NSString, name of an author to be associated with the document
 APPKIT_EXTERN NSString * NSTextCheckingRegularExpressionsKey NS_AVAILABLE_MAC(10_7);  // NSArray of NSRegularExpressions to be matched in the text of the document
+APPKIT_EXTERN NSString * NSTextCheckingSelectedRangeKey      NS_AVAILABLE_MAC(10_12); // NSValue containing NSRange, should be the portion of the selected range intersecting the string being checked, or a zero-length range if there is an insertion point in or adjacent to the string being checked, or NSMakeRange(NSNotFound, 0) if the selection is entirely outside of the string being checked.
+
 
 /* Methods for obtaining the default values for NSTextCheckingQuotesKey and NSTextCheckingReplacementsKey. */
 - (NSArray<NSString *> *)userQuotesArrayForLanguage:(NSString *)language NS_AVAILABLE_MAC(10_6);
@@ -170,6 +180,9 @@
 
 - (void)dismissCorrectionIndicatorForView:(NSView *)view NS_AVAILABLE_MAC(10_7);
 
+/* In some cases the next typing should prevent a pending correction (if it is an @, for example).  This method allows clients to recognize these cases in a standardized way. */
+- (BOOL)preventsAutocorrectionBeforeString:(NSString *)string language:(nullable NSString *)language NS_AVAILABLE_MAC(10_12);
+
 
 /* Entries in the availableLanguages list are all available spellchecking languages in user preference order, as described in the spellchecker's info dictionary, usually language abbreviations such as en_US.  The userPreferredLanguages will be a subset of the availableLanguages, as selected by the user for use with spellchecking, in preference order.  If automaticallyIdentifiesLanguages is YES, then text checking will automatically use these as appropriate; otherwise, it will use the language set by setLanguage:.  The older checkSpellingOfString:... and checkGrammarOfString:... methods will use the language set by setLanguage:, if they are called with a nil language argument.  */
 @property (readonly, copy) NSArray<NSString *> *availableLanguages NS_AVAILABLE_MAC(10_5);
@@ -177,18 +190,20 @@
 @property BOOL automaticallyIdentifiesLanguages NS_AVAILABLE_MAC(10_6);
 
 /* Allows programmatic setting of the misspelled word field. */
-- (void)setWordFieldStringValue:(NSString *)aString;
+- (void)setWordFieldStringValue:(NSString *)string;
 
 /* These allow clients to programmatically instruct the spellchecker to learn and unlearn words, and to determine whether a word has been learned (and hence can potentially be unlearned). */
 - (void)learnWord:(NSString *)word;
 - (BOOL)hasLearnedWord:(NSString *)word NS_AVAILABLE_MAC(10_5);
 - (void)unlearnWord:(NSString *)word NS_AVAILABLE_MAC(10_5);
 
-/* These methods allow clients to determine the global user preference settings for automatic text replacement, spelling correction, quote substitution, and dash substitution.  Text views by default will follow these automatically, but clients may override that by programmatically setting the values on the text view.  These methods will be useful for non-text view clients and others who wish to keep track of the settings.  Notifications are available (see below) when the settings change. */
+/* These methods allow clients to determine the global user preference settings for automatic text replacement, spelling correction, quote substitution, dash substitution, autocapitalization, and double-space-to-period substitution.  Text views by default will follow these automatically, but clients may override that by programmatically setting the values on the text view.  These methods will be useful for non-text view clients and others who wish to keep track of the settings.  Notifications are available (see below) when the settings change. */
 + (BOOL)isAutomaticTextReplacementEnabled NS_AVAILABLE_MAC(10_7);
 + (BOOL)isAutomaticSpellingCorrectionEnabled NS_AVAILABLE_MAC(10_7);
 + (BOOL)isAutomaticQuoteSubstitutionEnabled NS_AVAILABLE_MAC(10_9);
 + (BOOL)isAutomaticDashSubstitutionEnabled NS_AVAILABLE_MAC(10_9);
++ (BOOL)isAutomaticCapitalizationEnabled NS_AVAILABLE_MAC(10_12);
++ (BOOL)isAutomaticPeriodSubstitutionEnabled NS_AVAILABLE_MAC(10_12);
 
 /* Use of the following methods is discouraged; ordinarily language identification should be allowed to take place automatically, or else a specific language should be passed in to the methods that take such an argument, if the language is known in advance.  -setLanguage: allows programmatic setting of the language to spell-check in, for compatibility use if other methods are called with no language specified.  -setLanguage: accepts any of the language formats used by NSBundle, and tries to find the closest match among the available languages.  If -setLanguage: has been called, then -language will return that match; otherwise, it will return Multilingual if there is more than one element in -userPreferredLanguages, or the one element in that array if there is only one.  */
 
@@ -198,10 +213,12 @@
 @end
 
 /* These notifications are made available via the default notification center when the global user preference settings mentioned above are changed. */
-APPKIT_EXTERN NSString * const NSSpellCheckerDidChangeAutomaticSpellingCorrectionNotification NS_AVAILABLE_MAC(10_7);
-APPKIT_EXTERN NSString * const NSSpellCheckerDidChangeAutomaticTextReplacementNotification NS_AVAILABLE_MAC(10_7);
-APPKIT_EXTERN NSString * const NSSpellCheckerDidChangeAutomaticQuoteSubstitutionNotification NS_AVAILABLE_MAC(10_9);
-APPKIT_EXTERN NSString * const NSSpellCheckerDidChangeAutomaticDashSubstitutionNotification NS_AVAILABLE_MAC(10_9);
+APPKIT_EXTERN NSNotificationName const NSSpellCheckerDidChangeAutomaticSpellingCorrectionNotification NS_AVAILABLE_MAC(10_7);
+APPKIT_EXTERN NSNotificationName const NSSpellCheckerDidChangeAutomaticTextReplacementNotification NS_AVAILABLE_MAC(10_7);
+APPKIT_EXTERN NSNotificationName const NSSpellCheckerDidChangeAutomaticQuoteSubstitutionNotification NS_AVAILABLE_MAC(10_9);
+APPKIT_EXTERN NSNotificationName const NSSpellCheckerDidChangeAutomaticDashSubstitutionNotification NS_AVAILABLE_MAC(10_9);
+APPKIT_EXTERN NSNotificationName const NSSpellCheckerDidChangeAutomaticCapitalizationNotification NS_AVAILABLE_MAC(10_12);
+APPKIT_EXTERN NSNotificationName const NSSpellCheckerDidChangeAutomaticPeriodSubstitutionNotification NS_AVAILABLE_MAC(10_12);
 
 
 @interface NSSpellChecker(NSDeprecated)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpellProtocol.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpellProtocol.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpellProtocol.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpellProtocol.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSSpellProtocol.h
         Application Kit
-        Copyright (c) 1990-2015, Apple Inc.
+        Copyright (c) 1990-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpellServer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpellServer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpellServer.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpellServer.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSSpellServer.h
         Application Kit
-        Copyright (c) 1990-2015, Apple Inc.
+        Copyright (c) 1990-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSplitView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSplitView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSplitView.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSplitView.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSSplitView.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -39,9 +39,10 @@
 @property (nullable, copy) NSString *autosaveName NS_AVAILABLE_MAC(10_5);
 
 
-/* Set or get the delegate of the split view. The delegate will be sent NSSplitViewDelegate messages to which it responds.
+/* Set or get the delegate of the split view. The delegate will be sent NSSplitViewDelegate messages to which it responds. 
+   For apps linked against 10.12, this property has zeroing weak memory semantics. When linked against an older SDK, or with objects that do not support zeroing weak references this falls back to having `assign` semantics.
 */
-@property (nullable, assign) id<NSSplitViewDelegate> delegate;
+@property (nullable, weak) id<NSSplitViewDelegate> delegate;
 
 /* Draw the divider between two of the split view's subviews. The rectangle describes the entire divider rectangle in the receiver's coordinates. You can override this method to change the appearance of dividers.
 */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSplitViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSplitViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSplitViewController.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSplitViewController.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,19 +1,18 @@
 /*
     NSSplitViewController.h
     Application Kit
-    Copyright (c) 2014-2015, Apple Inc.
+    Copyright (c) 2014-2016, Apple Inc.
     All rights reserved.
 */
 
-#import <Foundation/NSArray.h>
 #import <AppKit/NSViewController.h>
+#import <AppKit/NSSplitViewItem.h>
 #import <AppKit/AppKitDefines.h>
 #import <AppKit/NSSplitView.h>
 
-NS_ASSUME_NONNULL_BEGIN
-
-@class NSSplitViewItem;
+#import <Foundation/NSArray.h>
 
+NS_ASSUME_NONNULL_BEGIN
 
 /// This constant can be used with any sizing related \c NSSplitViewController properties to get the default system behavior.
 APPKIT_EXTERN const CGFloat NSSplitViewControllerAutomaticDimension NS_AVAILABLE_MAC(10_11);
@@ -31,9 +30,11 @@
 @private
     NSSplitView *_splitView;
     id _splitViewControllerPrivateData;
+#ifndef __OBJC2__
     struct {
         unsigned int _reserved:32;
     } _splitViewControllerFlags;
+#endif
 }
 
 /// The split view managed by the SplitViewController. This can be used to customize view properties such as the dividerStyle, vertical, and autosaveName. It is not guaranteed to be the same view as the receivers 'view' property. The default created splitView is vertical with a dividerStyle of \c NSSplitViewDividerStyleThin. To provide a custom NSSplitView, set the splitView property anytime before self.viewLoaded is YES.
@@ -93,112 +94,4 @@
 
 @end
 
-
-typedef NS_ENUM(NSInteger, NSSplitViewItemBehavior) {
-    NSSplitViewItemBehaviorDefault,
-    NSSplitViewItemBehaviorSidebar,
-    NSSplitViewItemBehaviorContentList
-} NS_AVAILABLE_MAC(10_11);
-
-typedef NS_ENUM(NSInteger, NSSplitViewItemCollapseBehavior) {
-    /// The item uses the default collapsing behavior for its set `behavior`. The default may change over time.
-    NSSplitViewItemCollapseBehaviorDefault,
-    /// The item prefers to keep the other panes at their current size and position on screen, potentially growing or shrinking the window in the direction to best preserve that. But it will break that preference in order to keep the window fully on screen or when in full screen.
-    NSSplitViewItemCollapseBehaviorPreferResizingSplitViewWithFixedSiblings,
-    /// The item prefers to resize the other split panes. This will be broken when uncollapsing if the item can't fully uncollapse before hitting the minimum size of the other panes or the window.
-    NSSplitViewItemCollapseBehaviorPreferResizingSiblingsWithFixedSplitView,
-    /// The item will collapse/uncollapse purely from a constraint animation, with a constraint priority of the item’s `holdingPriority`. This could result in a partial internal content resize and window resize, and has no implications for keeping the window on screen. External constraints can be used to tweak exactly how the animation affects item, sibling, and window size and positions.
-    NSSplitViewItemCollapseBehaviorUseConstraints
-} NS_AVAILABLE_MAC(10_11);
-
-
-/// This constant can be used with any sizing related \c NSSplitViewItem properties to unset their values.
-APPKIT_EXTERN const CGFloat NSSplitViewItemUnspecifiedDimension NS_AVAILABLE_MAC(10_11);
-
-/*!
- * NSSplitViewItem implements the items used in an NSSplitViewController.
- * The item describes a child ViewController's state in a SplitViewController, e.g. its collapsibility, holding priority and other metrics, and collapsed state.
- */
-NS_CLASS_AVAILABLE_MAC(10_10)
-@interface NSSplitViewItem : NSObject <NSAnimatablePropertyContainer, NSCoding> {
-@private
-    id _splitViewItemPrivateData;
-    struct {
-        unsigned int _collapsed:1;
-        unsigned int _canCollapse:1;
-        unsigned int _isOverlaid:1;
-        unsigned int _revealsOnEdgeHoverInFullscreen:1;
-        unsigned int _springLoaded:1;
-        unsigned int _reserved:27;
-    } _flags;
-}
-
-/*!
- * Creates an autoreleased SplitViewItem that represents the provided ViewController. All other properties are left at their default.
- * \param viewController The view controller used to set the viewController property
- * \return An autoreleased SplitViewItem.
- */
-+ (instancetype)splitViewItemWithViewController:(NSViewController *)viewController;
-
-/*!
- * Creates a split view item representing a sidebar for the provided ViewController.
- * Sidebars have standard system behavior, specifically:
- *  - Translucent material background
- *  - The ability to collapse/uncollapse on split view size changes
- *  - The ability to overlay at small split view sizes when in fullscreen
- *  - canCollapse is set to YES
- *  - minimumThickness and maximumThickness are set to the standard minimum and maximum sidebar size
- *  - preferredThicknessFraction is set to the standard fraction for sidebars (0.15)
- *  - springLoaded is set to YES
- * \param viewController The view controller used to set the viewController property
- * \return An autoreleased SplitViewItem that acts as a sidebar.
- */
-+ (instancetype)sidebarWithViewController:(NSViewController *)viewController NS_SWIFT_NAME(init(sidebarWithViewController:)) NS_AVAILABLE_MAC(10_11);
-
-/*!
- * Creates a split view item representing a content list for the provided ViewController, akin to Mail's message list, Note's note list.
- * Content lists have system standard defaults, specifically:
- *  - minimumThickness and maximumThickness are set to the system standard for content lists
- *  - automaticMaximumThickness is set to the system standard for content lists
- *  - preferredThicknessFraction is set to the standard fraction for content lists (0.28 when a neighbor sidebar is visible, 0.33 if not)
- * \param viewController The view controller used to set the viewController property
- * \return An autoreleased SplitViewItem that acts as a content list.
- */
-+ (instancetype)contentListWithViewController:(NSViewController *)viewController NS_SWIFT_NAME(init(contentListWithViewController:)) NS_AVAILABLE_MAC(10_11);
-
-/// The standard behavior type of the receiver. See initializers for descriptions of each behavior.
-@property (readonly) NSSplitViewItemBehavior behavior NS_AVAILABLE_MAC(10_11);
-
-/// The view controller represented by the SplitViewItem. An exception will be thrown if a new viewController is set while the receiving SplitViewItem is added to a SplitViewController.
-@property (strong) NSViewController *viewController;
-
-/// Whether or not the child ViewController corresponding to the SplitViewItem is collapsed in the SplitViewController. The default is \c NO. This can be set with the animator proxy to animate the collapse or uncollapse. The exact animation used can be customized by setting it in the -animations dictionary with a key of "collapsed". If this is set to YES before it is added to the SplitViewController, it will be initially collapsed and the SplitViewController will not cause the view to be loaded until it is uncollapsed. This is KVC/KVO compliant and will be updated if the value changes from user interaction.
-@property (getter=isCollapsed) BOOL collapsed;
-
-/// Whether or not the child view controller is collapsible from user interaction - whether by dragging or double clicking a divider. The default is \c NO.
-@property BOOL canCollapse;
-
-/// The resize behavior when the receiver toggles its `collapsed` state programmatically, both animatedly and not. Defaults to `.Default`.
-@property NSSplitViewItemCollapseBehavior collapseBehavior NS_AVAILABLE_MAC(10_11);
-
-/// A convenience to set the minimum thickness of the split view item -- width for "vertical" split views, height otherwise. If NSSplitViewItemUnspecifiedDimension, no minimum size is enforced by the SplitViewItem, although constraints in the contained view hierarchy might have constraints specify some minimum size on their own. Defaults to NSSplitViewItemUnspecifiedDimension.
-@property CGFloat minimumThickness NS_AVAILABLE_MAC(10_11);
-
-/// A convenience to set the maximum thickness of the split view item -- width for "vertical" split views, height otherwise. If NSSplitViewItemUnspecifiedDimension, no maximum size is enforced by the SplitViewItem, although constraints in the contained view hierarchy might have constraints specify some maximum size on their own. Defaults to NSSplitViewItemUnspecifiedDimension.
-@property CGFloat maximumThickness NS_AVAILABLE_MAC(10_11);
-
-/// The percentage of the contained NSSplitView that the NSSplitViewItem prefers to encompass. This is used when double-clicking on a neighbor divider to return to that standard ratio. As well as after entering fullscreen to determine the initial size of the receiver. Defaults to NSSplitViewItemUnspecifiedDimension, which means no resize will occur on double-clicks, and the absolute size is preserved when entering fullscreen.
-@property CGFloat preferredThicknessFraction NS_AVAILABLE_MAC(10_11);
-
-/// Sets the priority under which a SplitViewItem will hold its width (for a vertical split view) or height (for a horizontal split view). The view with the lowest priority will be the first to take on additional width if the split view grows or shrinks. The default is \c NSLayoutPriorityDefaultLow.
-@property NSLayoutPriority holdingPriority;
-
-/// The maximum thickness of the split view item when resizing due to automatic sizing, such as entering fullscreen with a set preferredThicknessFraction or proportional sizing. The user can still resize up to the absolute maximum size by dragging the divider or otherwise. If NSSplitViewItemUnspecifiedDimension, no automatic maximum is enforced. Defaults to NSSplitViewItemUnspecifiedDimension.
-@property CGFloat automaticMaximumThickness NS_AVAILABLE_MAC(10_11);
-
-/// If YES, the split view item can be temporarily uncollapsed during a drag by hovering or deep clicking on its neighboring divider. Defaults to NO.
-@property (getter=isSpringLoaded) BOOL springLoaded NS_AVAILABLE_MAC(10_11);
-
-@end
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSplitViewItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSplitViewItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSplitViewItem.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSplitViewItem.h	2016-06-03 05:13:45.000000000 +0200
@@ -0,0 +1,124 @@
+/*
+    NSSplitViewItem.h
+    Application Kit
+    Copyright (c) 2014-2016, Apple Inc.
+    All rights reserved.
+*/
+
+#import <AppKit/NSLayoutConstraint.h>
+#import <AppKit/AppKitDefines.h>
+#import <AppKit/NSAnimation.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class NSViewController;
+
+typedef NS_ENUM(NSInteger, NSSplitViewItemBehavior) {
+    NSSplitViewItemBehaviorDefault,
+    NSSplitViewItemBehaviorSidebar,
+    NSSplitViewItemBehaviorContentList
+} NS_AVAILABLE_MAC(10_11);
+
+typedef NS_ENUM(NSInteger, NSSplitViewItemCollapseBehavior) {
+    /// The item uses the default collapsing behavior for its set `behavior`. The default may change over time.
+    NSSplitViewItemCollapseBehaviorDefault,
+    /// The item prefers to keep the other panes at their current size and position on screen, potentially growing or shrinking the window in the direction to best preserve that. But it will break that preference in order to keep the window fully on screen or when in full screen.
+    NSSplitViewItemCollapseBehaviorPreferResizingSplitViewWithFixedSiblings,
+    /// The item prefers to resize the other split panes. This will be broken when uncollapsing if the item can't fully uncollapse before hitting the minimum size of the other panes or the window.
+    NSSplitViewItemCollapseBehaviorPreferResizingSiblingsWithFixedSplitView,
+    /// The item will collapse/uncollapse purely from a constraint animation, with a constraint priority of the item’s `holdingPriority`. This could result in a partial internal content resize and window resize, and has no implications for keeping the window on screen. External constraints can be used to tweak exactly how the animation affects item, sibling, and window size and positions.
+    NSSplitViewItemCollapseBehaviorUseConstraints
+} NS_AVAILABLE_MAC(10_11);
+
+
+/// This constant can be used with any sizing related \c NSSplitViewItem properties to unset their values.
+APPKIT_EXTERN const CGFloat NSSplitViewItemUnspecifiedDimension NS_AVAILABLE_MAC(10_11);
+
+/*!
+ * NSSplitViewItem implements the items used in an NSSplitViewController.
+ * The item describes a child ViewController's state in a SplitViewController, e.g. its collapsibility, holding priority and other metrics, and collapsed state.
+ */
+NS_CLASS_AVAILABLE_MAC(10_10)
+@interface NSSplitViewItem : NSObject <NSAnimatablePropertyContainer, NSCoding> {
+@private
+    id _splitViewItemPrivateData;
+    struct {
+        unsigned int _collapsed:1;
+        unsigned int _canCollapse:1;
+        unsigned int _isOverlaid:1;
+        unsigned int _revealsOnEdgeHoverInFullscreen:1;
+        unsigned int _springLoaded:1;
+        unsigned int _forceWithinWindowBlending:1;
+        unsigned int _reserved:26;
+    } _flags;
+}
+
+/*!
+ * Creates an autoreleased SplitViewItem that represents the provided ViewController. All other properties are left at their default.
+ * \param viewController The view controller used to set the viewController property
+ * \return An autoreleased SplitViewItem.
+ */
++ (instancetype)splitViewItemWithViewController:(NSViewController *)viewController;
+
+/*!
+ * Creates a split view item representing a sidebar for the provided ViewController.
+ * Sidebars have standard system behavior, specifically:
+ *  - Translucent material background
+ *  - The ability to collapse/uncollapse on split view size changes
+ *  - The ability to overlay at small split view sizes when in fullscreen
+ *  - canCollapse is set to YES
+ *  - minimumThickness and maximumThickness are set to the standard minimum and maximum sidebar size
+ *  - preferredThicknessFraction is set to the standard fraction for sidebars (0.15)
+ *  - springLoaded is set to YES
+ * \param viewController The view controller used to set the viewController property
+ * \return An autoreleased SplitViewItem that acts as a sidebar.
+ */
++ (instancetype)sidebarWithViewController:(NSViewController *)viewController NS_SWIFT_NAME(init(sidebarWithViewController:)) NS_AVAILABLE_MAC(10_11);
+
+/*!
+ * Creates a split view item representing a content list for the provided ViewController, akin to Mail's message list, Note's note list.
+ * Content lists have system standard defaults, specifically:
+ *  - minimumThickness and maximumThickness are set to the system standard for content lists
+ *  - automaticMaximumThickness is set to the system standard for content lists
+ *  - preferredThicknessFraction is set to the standard fraction for content lists (0.28 when a neighbor sidebar is visible, 0.33 if not)
+ * \param viewController The view controller used to set the viewController property
+ * \return An autoreleased SplitViewItem that acts as a content list.
+ */
++ (instancetype)contentListWithViewController:(NSViewController *)viewController NS_SWIFT_NAME(init(contentListWithViewController:)) NS_AVAILABLE_MAC(10_11);
+
+/// The standard behavior type of the receiver. See initializers for descriptions of each behavior.
+@property (readonly) NSSplitViewItemBehavior behavior NS_AVAILABLE_MAC(10_11);
+
+/// The view controller represented by the SplitViewItem. An exception will be thrown if a new viewController is set while the receiving SplitViewItem is added to a SplitViewController.
+@property (strong) NSViewController *viewController;
+
+/// Whether or not the child ViewController corresponding to the SplitViewItem is collapsed in the SplitViewController. The default is \c NO. This can be set with the animator proxy to animate the collapse or uncollapse. The exact animation used can be customized by setting it in the -animations dictionary with a key of "collapsed". If this is set to YES before it is added to the SplitViewController, it will be initially collapsed and the SplitViewController will not cause the view to be loaded until it is uncollapsed. This is KVC/KVO compliant and will be updated if the value changes from user interaction.
+@property (getter=isCollapsed) BOOL collapsed;
+
+/// Whether or not the child view controller is collapsible from user interaction - whether by dragging or double clicking a divider. The default is \c NO.
+@property BOOL canCollapse;
+
+/// The resize behavior when the receiver toggles its `collapsed` state programmatically, both animatedly and not. Defaults to `.Default`.
+@property NSSplitViewItemCollapseBehavior collapseBehavior NS_AVAILABLE_MAC(10_11);
+
+/// A convenience to set the minimum thickness of the split view item -- width for "vertical" split views, height otherwise. If NSSplitViewItemUnspecifiedDimension, no minimum size is enforced by the SplitViewItem, although constraints in the contained view hierarchy might have constraints specify some minimum size on their own. Defaults to NSSplitViewItemUnspecifiedDimension.
+@property CGFloat minimumThickness NS_AVAILABLE_MAC(10_11);
+
+/// A convenience to set the maximum thickness of the split view item -- width for "vertical" split views, height otherwise. If NSSplitViewItemUnspecifiedDimension, no maximum size is enforced by the SplitViewItem, although constraints in the contained view hierarchy might have constraints specify some maximum size on their own. Defaults to NSSplitViewItemUnspecifiedDimension.
+@property CGFloat maximumThickness NS_AVAILABLE_MAC(10_11);
+
+/// The percentage of the contained NSSplitView that the NSSplitViewItem prefers to encompass. This is used when double-clicking on a neighbor divider to return to that standard ratio. As well as after entering fullscreen to determine the initial size of the receiver. Defaults to NSSplitViewItemUnspecifiedDimension, which means no resize will occur on double-clicks, and the absolute size is preserved when entering fullscreen.
+@property CGFloat preferredThicknessFraction NS_AVAILABLE_MAC(10_11);
+
+/// Sets the priority under which a SplitViewItem will hold its width (for a vertical split view) or height (for a horizontal split view). The view with the lowest priority will be the first to take on additional width if the split view grows or shrinks. The default is \c NSLayoutPriorityDefaultLow.
+@property NSLayoutPriority holdingPriority;
+
+/// The maximum thickness of the split view item when resizing due to automatic sizing, such as entering fullscreen with a set preferredThicknessFraction or proportional sizing. The user can still resize up to the absolute maximum size by dragging the divider or otherwise. If NSSplitViewItemUnspecifiedDimension, no automatic maximum is enforced. Defaults to NSSplitViewItemUnspecifiedDimension.
+@property CGFloat automaticMaximumThickness NS_AVAILABLE_MAC(10_11);
+
+/// If YES, the split view item can be temporarily uncollapsed during a drag by hovering or deep clicking on its neighboring divider. Defaults to NO.
+@property (getter=isSpringLoaded) BOOL springLoaded NS_AVAILABLE_MAC(10_11);
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStackView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStackView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStackView.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStackView.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
  NSStackView.h
  Application Kit
- Copyright (c) 2012-2015, Apple Inc.
+ Copyright (c) 2012-2016, Apple Inc.
  All rights reserved.
  */
 
@@ -113,9 +113,9 @@
     NSLayoutPriority _verticalHuggingPriority;
     NSLayoutPriority _horizontalHuggingPriority;
     
-    BOOL _unused;
-    id _unused2;
-    id _unused3;
+    BOOL _unused __unused;
+    id _unused2 __unused;
+    id _unused3 __unused;
     
     id _private;
     
@@ -132,102 +132,36 @@
 #pragma mark General StackView Properties
 
 @property (nullable, assign) id<NSStackViewDelegate> delegate;
-@property NSUserInterfaceLayoutOrientation orientation; // Orientation of the StackView, defaults to NSUserInterfaceLayoutOrientationHorizontal
-@property NSLayoutAttribute alignment; // Describes how subviews are aligned within the StackView, defaults to NSLayoutAttributeCenterY for horizontal stacks, NSLayoutAttributeCenterX for vertical stacks. Setting NSLayoutAttributeNotAnAttribute will cause the internal alignment constraints to not be created, and could result in an ambiguous layout. Setting an inapplicable attribute for the set orientation will result in the alignment being ignored (similar to its handling with NSLayoutAttributeNotAnAttribute). The alignment constraints are established at a priority of NSLayoutPriorityDefaultLow and is therefore overridable on an individual view basis.
-@property NSEdgeInsets edgeInsets; // Default padding inside the StackView, around all of the subviews. Edge insets do not flip or rotate for changes to orientation or R2L languages.
 
+/// Orientation of the StackView, defaults to NSUserInterfaceLayoutOrientationHorizontal
+@property NSUserInterfaceLayoutOrientation orientation;
 
-#pragma mark Managing Views
+/// Describes how subviews are aligned within the StackView, defaults to `NSLayoutAttributeCenterY` for horizontal stacks, `NSLayoutAttributeCenterX` for vertical stacks. Setting `NSLayoutAttributeNotAnAttribute` will cause the internal alignment constraints to not be created, and could result in an ambiguous layout. Setting an inapplicable attribute for the set orientation will result in the alignment being ignored (similar to its handling with NSLayoutAttributeNotAnAttribute). The alignment constraints are established at a priority of `NSLayoutPriorityDefaultLow` and are overridable for individual views using external constraints.
+@property NSLayoutAttribute alignment;
 
-/*
- Adds the view to the given gravity area at the end of that gravity area.
- This method will update the StackView's layout, and could result in the StackView changing its size or views being detached / clipped.
- */
-- (void)addView:(NSView *)aView inGravity:(NSStackViewGravity)gravity;
-/*
- Adds the view to the given gravity area at the index within that gravity area.
- Index numbers & counts are specific to each gravity area, and are indexed based on the set userInterfaceLayoutDirection.
- (For a L2R layout, index 0 in the leading gravity is the furthest left index; for a R2L layout index 0 in the leading gravity is the furthest right index)
- This method will update the StackView's layout, and could result in the StackView changing its size or views being detached / clipped.
- An NSRangeException will be raised if the index is out of bounds
- */
-- (void)insertView:(NSView *)aView atIndex:(NSUInteger)index inGravity:(NSStackViewGravity)gravity;
-/*
- Will remove aView from the StackView.
- [aView removeFromSuperview] will have the same behavior in the case that aView is visible (not detached) from the StackView.
- In the case that aView had been detached, this method must be used to remove it from the StackView.
- aView must be managed by the StackView, an exception will be raised if not.
- */
-- (void)removeView:(NSView *)aView;
-
-- (NSArray<__kindof NSView *> *)viewsInGravity:(NSStackViewGravity)gravity; // Getters will return the views that are contained by the corresponding gravity area, regardless of detach-status.
-- (void)setViews:(NSArray<NSView *> *)views inGravity:(NSStackViewGravity)gravity; // Setters will update the views and the layout for that gravity area.
-
-/*
- Returns an array of all the views managed by this StackView, regardless of detach-status or gravity area.
- This is indexed in the order of indexing within the StackView. Detached views are indexed at the positions they would have been if they were still attached.
- */
-@property (readonly, copy) NSArray<__kindof NSView *> *views;
-@property (readonly, copy) NSArray<__kindof NSView *> *detachedViews; // Returns the list of all of the detached views, regardless of gravity area
-
-/// If YES, when a stacked view's `hidden` property is set to YES, the view will be detached from the stack and reattached when set to NO. Similarly, if the view has a lowered visibility priority and is detached from the stack view, it will be set as `hidden` rather than removed from the view hierarchy. Defaults to YES for apps linked on the 10.11 SDK or later.
-@property BOOL detachesHiddenViews NS_AVAILABLE_MAC(10_11);
-
-/*
- Sets and gets the visibility priorities for views in the StackView.
- When detaching a view, it will first detach views with the lowest visibility priority.
- If multiple views share the same lowest visibility priority, all of them will be dropped.
-
- Defaults to NSStackViewVisibilityPriorityMustHold.
- Setting the visibility priority to NSStackViewVisibilityPriorityNotVisible will force that view to be detached (regardless of available space).
- 
- aView must be managed by the StackView, an exception will be raised if not.
- */
-- (void)setVisibilityPriority:(NSStackViewVisibilityPriority)priority forView:(NSView *)aView;
-- (NSStackViewVisibilityPriority)visibilityPriorityForView:(NSView *)aView;
+/// Default padding inside the StackView, around all of the subviews.
+@property NSEdgeInsets edgeInsets;
 
+/// The spacing and sizing distribution of stacked views along the primary axis. Defaults to GravityAreas.
+@property NSStackViewDistribution distribution NS_AVAILABLE_MAC(10_11);
 
-#pragma mark Spacing & Layout
-
-/*
- Spacing within a StackView is managed completely by the StackView.
- However, extra layout constraints can be added in conjunction with the StackView to create a more customized layout.
- Below describes the constraints the StackView uses to space its internal views.
- Spacing between view gravities have constraints with the following constraints:
- - Length >= spacing @ NSLayoutPriorityRequired
- - Length == spacing @ huggingPriority
- Spacing between views (within a gravity) have the following constraints:
- - Length >= spacing @ NSLayoutPriorityRequired
- - Length == spacing @ MAX(NSLayoutPriorityDefaultHigh, huggingPriority)
- */
-@property CGFloat spacing; // Default (minimum) spacing between each view
+/// Default (minimum) spacing between each view
+@property CGFloat spacing;
 
 /*
  Set and get custom spacing after a view. This custom spacing is used instead of the default spacing set with the spacing property.
  This is saved across layout updates, until the view is removed from the StackView or the custom spacing is changed.
  A value of NSStackViewSpacingUseDefault signifies that the spacing is the default spacing set with the StackView property.
- aView must be managed by the StackView, an exception will be raised if not.
- */
-- (void)setCustomSpacing:(CGFloat)spacing afterView:(NSView *)aView;
-- (CGFloat)customSpacingAfterView:(NSView *)aView;
-
-/// The spacing and sizing distribution of stacked views along the primary axis. Defaults to GravityAreas.
-@property NSStackViewDistribution distribution NS_AVAILABLE_MAC(10_11);
-
-/*
- Priority at which the StackView will not clip its views, defaults to NSLayoutPriorityRequired
- Clipping begins from the right and bottom sides of the StackView.
+ `view` must be managed by the StackView, an exception will be raised if not.
  */
-- (NSLayoutPriority)clippingResistancePriorityForOrientation:(NSLayoutConstraintOrientation)orientation;
-- (void)setClippingResistancePriority:(NSLayoutPriority)clippingResistancePriority forOrientation:(NSLayoutConstraintOrientation)orientation;
+- (void)setCustomSpacing:(CGFloat)spacing afterView:(NSView *)view;
+- (CGFloat)customSpacingAfterView:(NSView *)view;
 
-// Priority at which the StackView wants its internal spacing to be as small as possible, defaults to NSLayoutPriorityDefaultLow
-- (NSLayoutPriority)huggingPriorityForOrientation:(NSLayoutConstraintOrientation)orientation;
-- (void)setHuggingPriority:(NSLayoutPriority)huggingPriority forOrientation:(NSLayoutConstraintOrientation)orientation;
+/// If YES, when a stacked view's `hidden` property is set to YES, the view will be detached from the stack and reattached when set to NO. Similarly, if the view has a lowered visibility priority and is detached from the stack view, it will be set as `hidden` rather than removed from the view hierarchy. Defaults to YES for apps linked on the 10.11 SDK or later.
+@property BOOL detachesHiddenViews NS_AVAILABLE_MAC(10_11);
 
-@end
 
-@interface NSStackView (NSStackViewArrangedSubviews)
+#pragma mark Arranged Subviews
 
 /// The list of views that are arranged in a stack by the receiver. They are a subset of \c -subviews, with potential difference in ordering.
 @property (readonly, copy) NSArray<__kindof NSView *> *arrangedSubviews NS_AVAILABLE_MAC(10_11);
@@ -250,8 +184,49 @@
  */
 - (void)removeArrangedSubview:(NSView *)view NS_AVAILABLE_MAC(10_11);
 
+/// The arrangedSubviews that are currently detached/hidden.
+@property (readonly, copy) NSArray<__kindof NSView *> *detachedViews;
+
+
+#pragma mark Custom Priorities
+
+/*
+ Sets and gets the visibility priorities for views in the StackView.
+ When detaching a view, it will first detach views with the lowest visibility priority.
+ If multiple views share the same lowest visibility priority, all of them will be dropped.
+
+ Defaults to `NSStackViewVisibilityPriorityMustHold`.
+ Setting the visibility priority to NSStackViewVisibilityPriorityNotVisible will force that view to be detached (regardless of available space), and will set the view to be hidden if `detachesHiddenViews` is set to `YES`.
+ 
+ `view` must be managed by the StackView, an exception will be raised if not.
+ */
+- (void)setVisibilityPriority:(NSStackViewVisibilityPriority)priority forView:(NSView *)view;
+- (NSStackViewVisibilityPriority)visibilityPriorityForView:(NSView *)view;
+
+/*
+ Priority at which the StackView will not clip its views, defaults to NSLayoutPriorityRequired
+ Clipping begins from the trailing and bottom sides of the StackView.
+ */
+- (NSLayoutPriority)clippingResistancePriorityForOrientation:(NSLayoutConstraintOrientation)orientation;
+- (void)setClippingResistancePriority:(NSLayoutPriority)clippingResistancePriority forOrientation:(NSLayoutConstraintOrientation)orientation;
+
+/* Priority at which the StackView wants its internal spacing to be as small as possible, defaults to NSLayoutPriorityDefaultLow
+ Spacing within a StackView is managed completely by the StackView.
+ However, extra layout constraints can be added in conjunction with the StackView to create a more customized layout.
+ Below describes the constraints the StackView uses to space its internal views.
+ Spacing between view gravities have constraints with the following constraints:
+ - Length >= spacing @ NSLayoutPriorityRequired
+ - Length == spacing @ huggingPriority
+ Spacing between views (within a gravity) have the following constraints:
+ - Length >= spacing @ NSLayoutPriorityRequired
+ - Length == spacing @ MAX(NSLayoutPriorityDefaultHigh, huggingPriority)
+ */
+- (NSLayoutPriority)huggingPriorityForOrientation:(NSLayoutConstraintOrientation)orientation;
+- (void)setHuggingPriority:(NSLayoutPriority)huggingPriority forOrientation:(NSLayoutConstraintOrientation)orientation;
+
 @end
 
+
 #pragma mark - NSStackViewDelegate
 @protocol NSStackViewDelegate <NSObject>
 @optional
@@ -264,6 +239,41 @@
 
 @end
 
+/* API that is intended for use when the `distribution` of the receiver is set to `NSStackViewDistributionGravityAreas`. */
+@interface NSStackView (NSStackViewGravityAreas)
+
+/*
+ Adds the view to the given gravity area at the end of that gravity area.
+ This method will update the StackView's layout, and could result in the StackView changing its size or views being detached / clipped.
+ */
+- (void)addView:(NSView *)view inGravity:(NSStackViewGravity)gravity;
+/*
+ Adds the view to the given gravity area at the index within that gravity area.
+ Index numbers & counts are specific to each gravity area, and are indexed based on the set userInterfaceLayoutDirection.
+ (For a L2R layout, index 0 in the leading gravity is the furthest left index; for a R2L layout index 0 in the leading gravity is the furthest right index)
+ This method will update the StackView's layout, and could result in the StackView changing its size or views being detached / clipped.
+ An NSRangeException will be raised if the index is out of bounds
+ */
+- (void)insertView:(NSView *)view atIndex:(NSUInteger)index inGravity:(NSStackViewGravity)gravity;
+/*
+ Will remove view from the StackView.
+ [view removeFromSuperview] will have the same behavior in the case that view is visible (not detached) from the StackView.
+ In the case that view had been detached, this method must be used to remove it from the StackView.
+ view must be managed by the StackView, an exception will be raised if not.
+ */
+- (void)removeView:(NSView *)view;
+
+- (NSArray<__kindof NSView *> *)viewsInGravity:(NSStackViewGravity)gravity; // Getters will return the views that are contained by the corresponding gravity area, regardless of detach-status.
+- (void)setViews:(NSArray<NSView *> *)views inGravity:(NSStackViewGravity)gravity; // Setters will update the views and the layout for that gravity area.
+
+/*
+ Returns an array of all the views managed by this StackView, regardless of detach-status or gravity area.
+ This is indexed in the order of indexing within the StackView. Detached views are indexed at the positions they would have been if they were still attached.
+ */
+@property (readonly, copy) NSArray<__kindof NSView *> *views;
+
+@end
+
 @interface NSStackView (NSStackViewDeprecated)
 /*
  Property describing whether or not all spacing between views should be equivalent. Defaults to NO.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStatusBar.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStatusBar.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStatusBar.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStatusBar.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSStatusBar.h
         Application Kit
-        Copyright (c) 1997-2015, Apple Inc.
+        Copyright (c) 1997-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -23,7 +23,7 @@
  @private
     id             _items;
     void           *_fReserved1;
-    void           *_fReserved2;
+    void           *_fReserved2 __unused;
     NSInteger      _registeredForNote;
 }
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStatusBarButton.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStatusBarButton.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStatusBarButton.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStatusBarButton.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSStatusBarButton.h
     Application Kit
-    Copyright (c) 1997-2015, Apple Inc.
+    Copyright (c) 1997-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -14,7 +14,7 @@
 NS_CLASS_AVAILABLE_MAC(10_10)
 @interface NSStatusBarButton : NSButton {
 @private
-    id _statusBarButtonPrivate;
+    id _statusBarButtonPrivate __unused;
 }
 
 /// When YES the status bar icon has a disabled/off appearance while still being functional, such as allowing selection and actions. Defaults to NO.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStatusItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStatusItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStatusItem.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStatusItem.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,11 +1,12 @@
 /*
     NSStatusItem.h
     Application Kit
-    Copyright (c) 1997-2015, Apple Inc.
+    Copyright (c) 1997-2016, Apple Inc.
     All rights reserved.
 */
 
 #import <Foundation/Foundation.h>
+#import <AppKit/NSEvent.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -17,45 +18,58 @@
 @class NSMenu;
 @class NSView;
 
+typedef NS_OPTIONS(NSUInteger, NSStatusItemBehavior) {
+    /* Allow the user to remove the item. By default, an item is not removable. To provide consistency with system status items, RemovalAllowed should be set if your application remains usable without the status item. It is the application's responsibility to allow the user to re-add the item. Upon removal, -visible is set to NO. This is observable through KVO.
+     */
+    NSStatusItemBehaviorRemovalAllowed = (1 << 1),
+    
+    /* The application terminates when the user removes the item. Implies NSStatusItemBehaviorRemovalAllowed.
+     */
+    NSStatusItemBehaviorTerminationOnRemoval = (1 << 2),
+} NS_ENUM_AVAILABLE_MAC(10_12);
+
 @interface NSStatusItem : NSObject {
  @private
     NSStatusBar* _fStatusBar;
-    CGFloat        _fLength;
+    CGFloat      _fLength;
     NSWindow*    _fWindow;
     NSView*      _fView;
     int          _fPriority;
-    struct {
-	unsigned int customView:1;
-	unsigned int highlightMode:1;
-	unsigned int hasAlternateImage:1;
-	unsigned int hidden:1;
-	unsigned int backgroundStyle:4;
-	unsigned int inAdjustLength:1;
-        unsigned int pendingReplicantDisplay:1;
-        unsigned int disableImageReplicationCount:4;
-        unsigned int updatingReplicant:1;
-        unsigned int didInactiveTemplateStyling:1;
-        unsigned int needsAdditionalReplicantUpdate:1;
-        unsigned int reserved:15;
-    }	 _fFlags;
+    NSUInteger   _fFlags;
     id		 _statusItemMenu;
     NSMutableDictionary *_replicants;
-    NSData *_subitemOffsets;
+    id _fReserved __unused;
     NSString *_displayIdentifier;
 }
 
-/// The status bar that the receiver is displayed in.
+/*  The status bar that the receiver is displayed in.
+ */
 @property (readonly, assign) NSStatusBar *statusBar;
 
-/// The amount of space in the status bar that should be allocated to the receiver. \c NSVariableStatusItemLength will adjust the length to the size of the status item's contents and \c NSSquareStatusItemLength will keep the length the same as the status bar's height.
+/*  The amount of space in the status bar that should be allocated to the receiver. \c NSVariableStatusItemLength will adjust the length to the size of the status item's contents and \c NSSquareStatusItemLength will keep the length the same as the status bar's height.
+ */
 @property CGFloat length;
 
-/// The drop down menu that is displayed when the status item is pressed or clicked.
+/*  The drop down menu that is displayed when the status item is pressed or clicked.
+ */
 @property (nullable, strong) NSMenu *menu;
 
-/// The button that is displayed in the status bar. This is created automatically on the creation of the StatusItem. Behavior customization for the button, such as image, target/action, tooltip, can be set with this property.
+/*  The button that is displayed in the status bar. This is created automatically on the creation of the StatusItem. Behavior customization for the button, such as image, target/action, tooltip, can be set with this property.
+ */
 @property (nullable, readonly, strong) NSStatusBarButton *button NS_AVAILABLE_MAC(10_10);
 
+/*  Specifies the behavior of the status item.
+ */
+@property (assign) NSStatusItemBehavior behavior NS_AVAILABLE_MAC(10_12);
+
+/*  Specifies if the status item is currently visible in the status bar, even if it is obscured by the application menu. Defaults to YES. Persisted based on the -autosaveName. This is observable through KVO.
+ */
+@property (assign, getter=isVisible) BOOL visible NS_AVAILABLE_MAC(10_12);
+
+/*  Specifies a unique name for persisting visibility information. If none is specified, one is automatically chosen. Apps with multiple status bar items should set an autosave after creation. Setting to nil resets the automatically chosen name and clears saved information.
+ */
+@property (null_resettable, copy) NSString *autosaveName NS_AVAILABLE_MAC(10_12);
+
 @end
 
 
@@ -76,7 +90,12 @@
 @property (getter=isEnabled) BOOL enabled;
 @property BOOL highlightMode;
 @property (nullable, copy) NSString *toolTip;
+
+#if __LP64__
+- (NSInteger)sendActionOn:(NSEventMask)mask;
+#else
 - (NSInteger)sendActionOn:(NSInteger)mask;
+#endif
 
 /*
  Custom views should not be set on a status item.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStepper.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStepper.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStepper.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStepper.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSStepper.h
         Application Kit
-        Copyright (c) 2000-2015, Apple Inc.
+        Copyright (c) 2000-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStepperCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStepperCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStepperCell.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStepperCell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSStepperCell.h
         Application Kit
-        Copyright (c) 2000-2015, Apple Inc.
+        Copyright (c) 2000-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStoryboard.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStoryboard.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStoryboard.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStoryboard.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSStoryboard.h
         Application Kit
-        Copyright (c) 2013-2015, Apple Inc.
+        Copyright (c) 2013-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStoryboardSegue.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStoryboardSegue.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStoryboardSegue.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStoryboardSegue.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSStoryboardSegue.h
         Application Kit
-        Copyright (c) 2013-2015, Apple Inc.
+        Copyright (c) 2013-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabView.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabView.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSTabView.h
         Application Kit
-        Copyright (c) 2000-2015, Apple Inc.
+        Copyright (c) 2000-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -41,7 +41,7 @@
 
     	/* Non-Persistent properties */
 
-    BOOL		_tabViewUnusedBOOL1;
+    BOOL		_tabViewUnusedBOOL1 __unused;
     
     BOOL		_drawsBackground;		// YES if we draw the background when borderless
     NSTabViewItem	*_pressedTabViewItem;		// using during tracking
@@ -76,7 +76,7 @@
         unsigned int reserved:19;
     } _flags;
     NSTabViewItem 	*_focusedTabViewItem;			
-    void		*_tabViewUnused2;
+    void		*_tabViewUnused2 __unused;
 }
 
 	/* Select */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabViewController.h	2015-08-26 04:17:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabViewController.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSTabViewController.h
     Application Kit
-    Copyright (c) 2014-2015, Apple Inc.
+    Copyright (c) 2014-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -43,7 +43,8 @@
     struct {
         unsigned int _changingSelection:1;
         unsigned int _addingInitialTabViewItems:1;
-        unsigned int __extra:30;
+        unsigned int _tabBarIsDrivingTabMove:1;
+        unsigned int __extra:29;
     } _tabViewControllerFlags;
 }
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabViewItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabViewItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabViewItem.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabViewItem.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSTabViewItem.h
     Application Kit
-    Copyright (c) 2000-2015, Apple Inc.
+    Copyright (c) 2000-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -56,9 +56,9 @@
 
 /* By default, NSTabViewItem creates a basic NSView for you automatically.
  */
-- (instancetype)initWithIdentifier:(id)identifier; // identifier is retained
+- (instancetype)initWithIdentifier:(nullable id)identifier; // identifier is retained
 
-@property (strong) id identifier;
+@property (strong, nullable) id identifier;
 @property (copy) NSColor *color;
 @property (copy) NSString *label;
 /// Get and set the image for this tab view item. The image may only be used in certain tab view styles and options.  The default value is nil.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableCellView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableCellView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableCellView.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableCellView.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSTableCellView.h
     Application Kit
-    Copyright (c) 2009-2015, Apple Inc.
+    Copyright (c) 2009-2016, Apple Inc.
     All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableColumn.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableColumn.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableColumn.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableColumn.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSTableColumn.h
     Application Kit
-    Copyright (c) 1995-2015, Apple Inc.
+    Copyright (c) 1995-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -45,7 +45,8 @@
 
 /* Designated initializer for NSTableColumns. Prior to 10.7, the parameter type was 'id', but it is now an 'NSString *'. See also -setIdentifier: and -identifier, and NSUserInterfaceItemIdentification.
  */
-- (instancetype)initWithIdentifier:(NSString *)identifier;
+- (instancetype)initWithIdentifier:(NSString *)identifier NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
 
 /* Gets and sets the string identifier associated with the NSTableColumn. 'identifier' will be copied. Prior to 10.7, the type was 'id', but was changed to 'NSString *' for NSUserInterfaceItemIdentification.
  */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableHeaderCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableHeaderCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableHeaderCell.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableHeaderCell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSTableHeaderCell.h
         Application Kit
-        Copyright (c) 1995-2015, Apple Inc.
+        Copyright (c) 1995-2016, Apple Inc.
         All rights reserved.
 */
 #import <AppKit/NSTextFieldCell.h>
@@ -18,7 +18,7 @@
 
 /* Returns the location to display the sorting indicator given the cellFrame.
 */
-- (NSRect)sortIndicatorRectForBounds:(NSRect)theRect;
+- (NSRect)sortIndicatorRectForBounds:(NSRect)rect;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableHeaderView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableHeaderView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableHeaderView.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableHeaderView.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSTableHeaderView.h
     Application Kit
-    Copyright (c) 1995-2015, Apple Inc.
+    Copyright (c) 1995-2016, Apple Inc.
     All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableRowView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableRowView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableRowView.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableRowView.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSTableRowView.h
     Application Kit
-    Copyright (c) 2008-2015, Apple Inc.
+    Copyright (c) 2008-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -18,7 +18,7 @@
 NS_CLASS_AVAILABLE(10_7, NA)
 @interface NSTableRowView : NSView <NSAccessibilityRow> {
 @private
-    NSView **_columnViews;
+    __unsafe_unretained NSView **_columnViews;
     NSInteger _columnCount;
     
     NSTableViewSelectionHighlightStyle _selectionHighlightStyle;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableView.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableView.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSTableView.h
     Application Kit
-    Copyright (c) 1995-2015, Apple Inc.
+    Copyright (c) 1995-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -165,6 +165,7 @@
     NSView              *_cornerView;
     NSMutableArray      *_tableColumns;
     NSCell              *_editingCell;
+    // NOTE: accessing the _delegate or _dataSource ivars directly is not supported! They are opaque objects, and may not represent the real delegate.
     id                  _delegate;
     id                  _dataSource;
     NSSize              _intercellSpacing;
@@ -195,13 +196,11 @@
 
 /* Get and set the dataSource. The dataSource can implement methods in the protocol NSTableViewDataSource. Some methods are required, unless bindings are used, in which case they are optional. The dataSource is a weak reference (non retained) in non garbage collected applications. Under garbage collected apps, it is a strong reference. The default value is 'nil'.
  */
-- (void)setDataSource:(nullable id <NSTableViewDataSource>)aSource;
-- (nullable id <NSTableViewDataSource>)dataSource;
+@property (nullable, weak) id <NSTableViewDataSource> dataSource;
 
 /* Get and set the delegate. The delegate can implement methods in the protocol NSTableViewDelegate. All delegate methods are optional. The delegate is a weak reference (non retained) in non garbage collected applications. Under garbage collected apps, it is a strong reference. The default value is 'nil'.
  */
-- (void)setDelegate:(nullable id <NSTableViewDelegate>)delegate;
-- (nullable id <NSTableViewDelegate>)delegate;
+@property (nullable, weak) id <NSTableViewDelegate> delegate;
 
 /* Get and set the headerView. Calling -setHeaderView:nil will remove the headerView. Calling -setHeaderView: may have the side effect of tiling the enclosingScrollView to accommodate the size change. The default value is a new NSTableHeaderView instance.
  */
@@ -336,7 +335,7 @@
 
 /* Support for little "indicator" images in table header cells.
 */
-- (void)setIndicatorImage:(nullable NSImage *)anImage inTableColumn:(NSTableColumn *)tableColumn;
+- (void)setIndicatorImage:(nullable NSImage *)image inTableColumn:(NSTableColumn *)tableColumn;
 - (nullable NSImage *)indicatorImageInTableColumn:(NSTableColumn *)tableColumn;
 
 /* Support for highlightable column header, for use with row selection.
@@ -473,14 +472,14 @@
 /* View Based TableView: This method attempts to make the view at 'column/row' the first responder, which will begin editing if the view supports editing.
    Cell Based TableView: This method edits the NSCell located at 'column/row' by calling the following NSCell method:
  
- - (void)editWithFrame:(NSRect)aRect inView:(NSView *)controlView editor:(NSText *)textObj delegate:(id)anObject event:(NSEvent *)theEvent;
+ - (void)editWithFrame:(NSRect)rect inView:(NSView *)controlView editor:(NSText *)textObj delegate:(id)delegate event:(NSEvent *)event;
  
  or, if 'select' is YES:
  
- - (void)selectWithFrame:(NSRect)aRect inView:(NSView *)controlView editor:(NSText *)textObj delegate:(id)anObject start:(NSInteger)selStart length:(NSInteger)selLength;
+ - (void)selectWithFrame:(NSRect)rect inView:(NSView *)controlView editor:(NSText *)textObj delegate:(id)delegate start:(NSInteger)selStart length:(NSInteger)selLength;
  
  */
-- (void)editColumn:(NSInteger)column row:(NSInteger)row withEvent:(nullable NSEvent *)theEvent select:(BOOL)select;
+- (void)editColumn:(NSInteger)column row:(NSInteger)row withEvent:(nullable NSEvent *)event select:(BOOL)select;
 
 /* View Based TableView: This method should not be subclassed or overridden for a "View Based TableView". Instead, row drawing customization can be done by subclassing NSTableRowView.
    Cell Based TableView: This method can be overriden to customize drawing for 'row'. 
@@ -524,7 +523,7 @@
 
 /* Enumerates all available NSTableRowViews. This includes all views in the -visibleRect, however, it may also include ones that are "in flight" due to animations or other various attributes of the table.
  */
-- (void)enumerateAvailableRowViewsUsingBlock:(void (^)(__kindof NSTableRowView *rowView, NSInteger row))handler NS_AVAILABLE_MAC(10_7);
+- (void)enumerateAvailableRowViewsUsingBlock:(void (NS_NOESCAPE ^)(__kindof NSTableRowView *rowView, NSInteger row))handler NS_AVAILABLE_MAC(10_7);
 
 /* View Based TableView: Group rows can optionally appear floating. Group rows are rows that the delegate responds YES to tableView:isGroupRow:. NSOutlineView will only float expandable group rows that are expanded. The default value is YES. This property is encoded and decoded in the nib.
  */
@@ -606,6 +605,10 @@
  */
 @property BOOL usesStaticContents NS_AVAILABLE_MAC(10_10);
 
+/* Get and set the user interface layout direction. When set to NSUserInterfaceLayoutDirectionRightToLeft, the TableView will flip the visual order of the table columns, while the logical order remains as it was. The default value is NSUserInterfaceLayoutDirectionLeftToRight. This method is available only on 10.12 and higher, and in previous releases it was hardcoded to always return NSUserInterfaceLayoutDirectionLeftToRight. However, NSOutlineView has had a separate implmentation since 10.7.
+ */
+@property NSUserInterfaceLayoutDirection userInterfaceLayoutDirection; // NS_AVAILABLE_MAC(10_12);
+
 @end
 
 #pragma mark -
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableViewRowAction.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableViewRowAction.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableViewRowAction.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableViewRowAction.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSTableViewRowAction.h
     Application Kit
-    Copyright (c) 2014-2015, Apple Inc.
+    Copyright (c) 2014-2016, Apple Inc.
     All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSText.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSText.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSText.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSText.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSText.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -73,7 +73,7 @@
 
 @property (nullable, copy) NSString *string;
 
-- (void)replaceCharactersInRange:(NSRange)range withString:(NSString *)aString;
+- (void)replaceCharactersInRange:(NSRange)range withString:(NSString *)string;
 - (void)replaceCharactersInRange:(NSRange)range withRTF:(NSData *)rtfData;
 - (void)replaceCharactersInRange:(NSRange)range withRTFD:(NSData *)rtfdData;
 
@@ -161,10 +161,10 @@
     NSTextWritingDirectionOverride NS_DEPRECATED_MAC(10_0, 10_11, "Use NSWritingDirectionOverride instead")      = (1 << 1)
 };
 
-static const NSTextAlignment NSLeftTextAlignment = NSTextAlignmentLeft;
-static const NSTextAlignment NSRightTextAlignment = NSTextAlignmentRight;
-static const NSTextAlignment NSCenterTextAlignment = NSTextAlignmentCenter;
-static const NSTextAlignment NSJustifiedTextAlignment = NSTextAlignmentJustified;
-static const NSTextAlignment NSNaturalTextAlignment = NSTextAlignmentNatural;
+static const NSTextAlignment NSLeftTextAlignment API_DEPRECATED_WITH_REPLACEMENT("NSTextAlignmentLeft", macosx(10.0, 10.12))  = NSTextAlignmentLeft;
+static const NSTextAlignment NSRightTextAlignment API_DEPRECATED_WITH_REPLACEMENT("NSTextAlignmentRight", macosx(10.0, 10.12))  = NSTextAlignmentRight;
+static const NSTextAlignment NSCenterTextAlignment API_DEPRECATED_WITH_REPLACEMENT("NSTextAlignmentCenter", macosx(10.0, 10.12))  = NSTextAlignmentCenter;
+static const NSTextAlignment NSJustifiedTextAlignment API_DEPRECATED_WITH_REPLACEMENT("NSTextAlignmentJustified", macosx(10.0, 10.12))  = NSTextAlignmentJustified;
+static const NSTextAlignment NSNaturalTextAlignment API_DEPRECATED_WITH_REPLACEMENT("NSTextAlignmentNatural", macosx(10.0, 10.12))  = NSTextAlignmentNatural;
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextAlternatives.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextAlternatives.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextAlternatives.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextAlternatives.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSTextAlternatives.h
 	Application Kit
-	Copyright (c) 2011-2015, Apple Inc.
+	Copyright (c) 2011-2016, Apple Inc.
 	All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextField.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextField.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextField.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextField.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSTextField.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -55,6 +55,39 @@
 
 @end
 
+@interface NSTextField(NSTextFieldConvenience)
+
+/*!
+ Creates a non-wrapping, non-editable, non-selectable text field that displays text in the default system font.
+ @param stringValue The title text to display in the field.
+ @return An initialized text field object.
+ */
++ (instancetype)labelWithString:(NSString *)stringValue NS_SWIFT_NAME(init(labelWithString:)) NS_AVAILABLE_MAC(10_12);
+
+/*!
+ Creates a wrapping, non-editable, selectable text field that displays text in the default system font.
+ @param stringValue The title text to display in the field.
+ @return An initialized text field object.
+ */
++ (instancetype)wrappingLabelWithString:(NSString *)stringValue NS_SWIFT_NAME(init(wrappingLabelWithString:)) NS_AVAILABLE_MAC(10_12);
+
+/*!
+ Creates a non-editable, selectable text field that displays attributed text.
+ The line break mode of this field is determined by the attributed string's NSParagraphStyle attribute.
+ @param attributedStringValue The attributed string to display in the field.
+ @return An initialized text field object.
+ */
++ (instancetype)labelWithAttributedString:(NSAttributedString *)attributedStringValue NS_SWIFT_NAME(init(labelWithAttributedString:)) NS_AVAILABLE_MAC(10_12);
+
+/*!
+ Creates a non-wrapping editable text field.
+ @param stringValue The initial contents of the text field, or nil for an initially empty text field.
+ @return An initialized text field object.
+ */
++ (instancetype)textFieldWithString:(nullable NSString *)stringValue NS_AVAILABLE_MAC(10_12);
+
+@end
+
 @interface NSTextField(NSTextFieldAttributedStringMethods)
 @property BOOL allowsEditingTextAttributes;
 @property BOOL importsGraphics;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextFieldCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextFieldCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextFieldCell.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextFieldCell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSTextFieldCell.h
     Application Kit
-    Copyright (c) 1994-2015, Apple Inc.
+    Copyright (c) 1994-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -39,10 +39,16 @@
         unsigned int thcHighlighted:1;
         unsigned int shouldNotClipToBounds:1;
         unsigned int allowsDefaultTightening:1;
-        unsigned int reservedTextFieldCell:9;
+        unsigned int enableCP:1;
+        unsigned int automaticCompletionDisabled:1;
+        unsigned int reservedTextFieldCell:7;
     } _tfFlags;
 }
 
+- (instancetype)initTextCell:(NSString *)string NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
+- (instancetype)initImageCell:(nullable NSImage *)image NS_UNAVAILABLE; // Use the designated initializer initTextCell:
+
 @property (nullable, copy) NSColor *backgroundColor;
 @property BOOL drawsBackground;
 @property (nullable, copy) NSColor *textColor;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextFinder.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextFinder.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextFinder.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextFinder.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSTextFinder.h
         Application Kit
-        Copyright (c) 2003-2015, Apple Inc.
+        Copyright (c) 2003-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -57,10 +57,11 @@
     BOOL _incrementalEnabled;
     BOOL _shouldDim;
     
-    id _private;
+    id _private __unused;
 }
 
-- (instancetype)init;
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)decoder NS_DESIGNATED_INITIALIZER;
 
 /* A text finder must be associated with an object which implements the NSTextFinderClient protocol for it to function. The client is responsible for providing the string to be searched, the location for the find bar, and methods which control feedback to the user about the search results. */
 @property (nullable, assign) IBOutlet id <NSTextFinderClient> client;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextInputClient.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextInputClient.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextInputClient.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextInputClient.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSTextInputClient.h
 	Application Kit
-	Copyright (c) 2006-2015, Apple Inc.
+	Copyright (c) 2006-2016, Apple Inc.
 	All rights reserved.
  */
 
@@ -16,17 +16,17 @@
 
 @protocol NSTextInputClient
 @required
-/* The receiver inserts aString replacing the content specified by replacementRange. aString can be either an NSString or NSAttributedString instance.
+/* The receiver inserts string replacing the content specified by replacementRange. string can be either an NSString or NSAttributedString instance.
 */
-- (void)insertText:(id)aString replacementRange:(NSRange)replacementRange;
+- (void)insertText:(id)string replacementRange:(NSRange)replacementRange;
 
-/* The receiver invokes the action specified by aSelector.
+/* The receiver invokes the action specified by selector.
 */
- - (void)doCommandBySelector:(SEL)aSelector;
+ - (void)doCommandBySelector:(SEL)selector;
  
-/* The receiver inserts aString replacing the content specified by replacementRange. aString can be either an NSString or NSAttributedString instance. selectedRange specifies the selection inside the string being inserted; hence, the location is relative to the beginning of aString. When aString is an NSString, the receiver is expected to render the marked text with distinguishing appearance (i.e. NSTextView renders with -markedTextAttributes).
+/* The receiver inserts string replacing the content specified by replacementRange. string can be either an NSString or NSAttributedString instance. selectedRange specifies the selection inside the string being inserted; hence, the location is relative to the beginning of string. When string is an NSString, the receiver is expected to render the marked text with distinguishing appearance (i.e. NSTextView renders with -markedTextAttributes).
 */
-- (void)setMarkedText:(id)aString selectedRange:(NSRange)selectedRange replacementRange:(NSRange)replacementRange;
+- (void)setMarkedText:(id)string selectedRange:(NSRange)selectedRange replacementRange:(NSRange)replacementRange;
 
 /* The receiver unmarks the marked text. If no marked text, the invocation of this method has no effect.
 */
@@ -44,30 +44,30 @@
 */
 - (BOOL)hasMarkedText;
 
-/* Returns attributed string specified by aRange. It may return nil. If non-nil return value and actualRange is non-NULL, it contains the actual range for the return value. The range can be adjusted from various reasons (i.e. adjust to grapheme cluster boundary, performance optimization, etc).
+/* Returns attributed string specified by range. It may return nil. If non-nil return value and actualRange is non-NULL, it contains the actual range for the return value. The range can be adjusted from various reasons (i.e. adjust to grapheme cluster boundary, performance optimization, etc).
 */
-- (nullable NSAttributedString *)attributedSubstringForProposedRange:(NSRange)aRange actualRange:(nullable NSRangePointer)actualRange;
+- (nullable NSAttributedString *)attributedSubstringForProposedRange:(NSRange)range actualRange:(nullable NSRangePointer)actualRange;
 
 /* Returns an array of attribute names recognized by the receiver.
 */
 - (NSArray<NSString *> *)validAttributesForMarkedText;
 
-/* Returns the first logical rectangular area for aRange. The return value is in the screen coordinate. The size value can be negative if the text flows to the left. If non-NULL, actuallRange contains the character range corresponding to the returned area.
+/* Returns the first logical rectangular area for range. The return value is in the screen coordinate. The size value can be negative if the text flows to the left. If non-NULL, actuallRange contains the character range corresponding to the returned area.
 */
-- (NSRect)firstRectForCharacterRange:(NSRange)aRange actualRange:(nullable NSRangePointer)actualRange;
+- (NSRect)firstRectForCharacterRange:(NSRange)range actualRange:(nullable NSRangePointer)actualRange;
 
-/* Returns the index for character that is nearest to aPoint. aPoint is in the screen coordinate system.
+/* Returns the index for character that is nearest to point. point is in the screen coordinate system.
 */
-- (NSUInteger)characterIndexForPoint:(NSPoint)aPoint;
+- (NSUInteger)characterIndexForPoint:(NSPoint)point;
 
 @optional
 /* Returns an attributed string representing the receiver's document content. An NSTextInputClient can implement this interface if can be done efficiently. The caller of this interface can random access arbitrary portions of the receiver's content more efficiently.
 */
 - (NSAttributedString *)attributedString;
 
-/* Returns the fraction of distance for aPoint from the left side of the character. This allows caller to perform precise selection handling.
+/* Returns the fraction of distance for point from the left side of the character. This allows caller to perform precise selection handling.
 */
-- (CGFloat)fractionOfDistanceThroughGlyphForPoint:(NSPoint)aPoint;
+- (CGFloat)fractionOfDistanceThroughGlyphForPoint:(NSPoint)point;
 
 /* Returns the baseline position relative to the origin of rectangle returned by -firstRectForCharacterRange:actualRange:. This information allows the caller to access finer-grained character position inside the NSTextInputClient document.
 */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextInputContext.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextInputContext.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextInputContext.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextInputContext.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSTextInputContext.h
 	Application Kit
-	Copyright (c) 2008-2015, Apple Inc.
+	Copyright (c) 2008-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -9,7 +9,6 @@
 #import <AppKit/AppKitDefines.h>
 #import <AppKit/NSTextInputClient.h>
 
-
 NS_ASSUME_NONNULL_BEGIN
 
 @class NSEvent;
@@ -29,7 +28,7 @@
 
     NSInteger _documentRefcon;
 
-    id _reserved[2];
+    id _reserved[2] __unused;
     id _auxiliary;
 
     struct {
@@ -63,7 +62,8 @@
 
 /* The designated initializer.
  */
-- (instancetype)initWithClient:(id <NSTextInputClient>)theClient;
+- (instancetype)initWithClient:(id <NSTextInputClient>)client NS_DESIGNATED_INITIALIZER;
+- (instancetype)init NS_UNAVAILABLE; // Use the designated initializer initWithClient:
 
 /**** Properties *****/
 /* Returns the owner of this input context. The owner, typically an NSView, retains its NSTextInputContext instance. NSTextInputContext doesn't retain its client.
@@ -88,13 +88,13 @@
 /**** Input source interface ****/
 /* Tells the Cocoa Text Input system to handle mouse/key events. Returns YES if the system consumed the event.
  */
-- (BOOL)handleEvent:(NSEvent *)theEvent;
+- (BOOL)handleEvent:(NSEvent *)event;
 
 /* Notifies the system to discard the current conversion session. The client should clear its marked range when sending this message.
  */
 - (void)discardMarkedText;
 
-/* Notifies the Cocoa Text Input system that the position information previously queried via methods like -firstRectForCharacterRange:actualRange: needs to be updated.
+/* Notifies the text input system that information related to character positions, including the document's visual coordinates, text selection, and document contents, has been modified. Text engines implementing the NSTextInputClient protocol should send this message whenever any of these changes occur, and -[NSTextInputContext handleEvent:] will not otherwise be called. -handleEvent: serves as an implicit notification that any of these changes could have occurred.
  */
 - (void)invalidateCharacterCoordinates;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextList.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextList.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextList.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextList.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,6 +1,6 @@
 /*
         NSTextList.h
-        Copyright (c) 2004-2015, Apple Inc.
+        Copyright (c) 2004-2016, Apple Inc.
         All rights reserved.
 
         Class to represent text lists.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextStorage.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextStorage.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextStorage.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextStorage.h	2016-06-03 05:13:45.000000000 +0200
@@ -126,7 +126,7 @@
 
 @interface NSObject (NSDeprecatedTextStorageDelegateInterface)
 - (void)textStorageWillProcessEditing:(NSNotification *)notification NS_DEPRECATED_MAC(10_0, 10_11, "Use -textStorage:willProcessEditing:range:changeInLength: instead.");
-- (void)textStorageDidProcessEditing:(NSNotification *)notification NS_DEPRECATED_MAC(10_0, 10_11, "Use -textStorage:DidProcessEditing:range:changeInLength: instead.");
+- (void)textStorageDidProcessEditing:(NSNotification *)notification NS_DEPRECATED_MAC(10_0, 10_11, "Use -textStorage:didProcessEditing:range:changeInLength: instead.");
 @end
 
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextStorageScripting.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextStorageScripting.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextStorageScripting.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextStorageScripting.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSTextStorageScripting.h
         AppKit Framework
-        Copyright (c) 1997-2015, Apple Inc.
+        Copyright (c) 1997-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextTable.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextTable.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextTable.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextTable.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,6 +1,6 @@
 /*
         NSTextTable.h
-        Copyright (c) 2004-2015, Apple Inc.
+        Copyright (c) 2004-2016, Apple Inc.
         All rights reserved.
 
         Classes to represent text tables and other text blocks.
@@ -67,7 +67,7 @@
     void *_blockSecondary;
 }
 
-- (instancetype)init;     // Designated initializer
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
 
 /* Content size */
 - (void)setValue:(CGFloat)val type:(NSTextBlockValueType)type forDimension:(NSTextBlockDimension)dimension;
@@ -114,7 +114,7 @@
     void *_tableBlockSecondary;
 }
 
-- (instancetype)initWithTable:(NSTextTable *)table startingRow:(NSInteger)row rowSpan:(NSInteger)rowSpan startingColumn:(NSInteger)col columnSpan:(NSInteger)colSpan;     // Designated initializer
+- (instancetype)initWithTable:(NSTextTable *)table startingRow:(NSInteger)row rowSpan:(NSInteger)rowSpan startingColumn:(NSInteger)col columnSpan:(NSInteger)colSpan NS_DESIGNATED_INITIALIZER;     // Designated initializer
 
 /* These methods determine the block's role in its enclosing table. */
 @property (readonly, strong) NSTextTable *table;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextView.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextView.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSTextView.h
         Application Kit
-        Copyright (c) 1994-2015, Apple Inc.
+        Copyright (c) 1994-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -178,7 +178,7 @@
 /************************* Vertical text support *************************/
 
 // Changes the receiver's layout orientation and invalidates the contents.  Unlike other NSTextView properties, this is not shared by sibling views.  It also rotates the bounds 90 degrees, swaps horizontal and vertical bits of the autoresizing mask, and reconfigures isHorizontallyResizable and isVerticallyResizable properties accordingly.  Also, if -enclosingScrollView returns non-nil, it reconfigures horizontal and vertical ruler views, horizontal and vertical scrollers, and the frame.
-- (void)setLayoutOrientation:(NSTextLayoutOrientation)theOrientation NS_AVAILABLE_MAC(10_7);
+- (void)setLayoutOrientation:(NSTextLayoutOrientation)orientation NS_AVAILABLE_MAC(10_7);
 
 // An action method that calls -setLayoutOrientation: with the sender's tag as the orientation.
 - (void)changeLayoutOrientation:(nullable id)sender NS_AVAILABLE_MAC(10_7);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTitlebarAccessoryViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTitlebarAccessoryViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTitlebarAccessoryViewController.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTitlebarAccessoryViewController.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSTitlebarAccessoryViewController.h
     Application Kit
-    Copyright (c) 2014-2015, Apple Inc.
+    Copyright (c) 2014-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -14,7 +14,7 @@
 
 /* For use with NSWindow's API addTitlebarAccessoryViewController:, etc. */
 NS_CLASS_AVAILABLE(10_10, NA)
-@interface NSTitlebarAccessoryViewController : NSViewController {
+@interface NSTitlebarAccessoryViewController : NSViewController <NSAnimationDelegate, NSAnimatablePropertyContainer> {
 @private
     NSLayoutAttribute _layoutAttribute;
     CGFloat _fullScreenMinHeight;
@@ -24,20 +24,22 @@
     BOOL _isToolbarAccessoryView;
     NSInteger _updateCount;
     
-    unsigned int _isInspectorBarView:1;
-    unsigned int _forceVisible:1;
+    unsigned int _hidden:1;
+    unsigned int _unusedTVC2:1 __unused;
     unsigned int _updatingFrame:1;
     unsigned int _registered:1;
-    unsigned int _reservedTVC:28;
-#if !__OBJC2__
-    id _reservedAVC;
-    id _reservedAVC2;
-#endif
+    unsigned int _reservedTVC:28 __unused;
+
+    id      _animationData;
+    CGFloat _visibleAmount; // For animating visibility
 }
 
 /* The layoutAttribute defaults to NSLayoutAttributeBottom, telling the window to place this view controller's view under the titlebar. NSLayoutAttributeRight is also supported, telling the window to place the view controller's view on the right side of the window. For applications linked on Mac OS 10.11 or later, NSLayoutAttributeLeft is also supported; placing the item on the left side of the window (adjacent and to the right of the close/minimize/maximize buttons). All other values are currently invalid and will assert.
  
     For applications linked on 10.11 and higher, a layoutAttribute== NSLayoutAttributeRight will no longer right indent toolbar items (previously it would leave a space), unless  the titleVisibility == NSWindowTitleHidden. 
+ 
+    For applications linked on 10.12 and higher, NSLayoutAttributeLeading and NSLayoutAttributeTrailing can also be used to specify an abstract position that automatically flips depending on the localized language.  For applications that do not link on 10.12, NSLayoutAttributeLeft will automatically flip to the Right when in a Right To Left language.
+ 
  */
 @property NSLayoutAttribute layoutAttribute;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTokenField.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTokenField.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTokenField.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTokenField.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSTokenField.h
 	Application Kit
-	Copyright (c) 2004-2015, Apple Inc.
+	Copyright (c) 2004-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -27,7 +27,7 @@
     id _reserved7;
 }
 
-- (void)setDelegate:(nullable id <NSTokenFieldDelegate>)anObject;
+- (void)setDelegate:(nullable id <NSTokenFieldDelegate>)delegate;
 - (nullable id <NSTokenFieldDelegate>)delegate;
 
 /* Sets the default token style used for each new token.  However, if the delegate implements tokenField:styleForRepresentedObject:, that return value will be used instead.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTokenFieldCell.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTokenFieldCell.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTokenFieldCell.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTokenFieldCell.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSTokenFieldCell.h
 	Application Kit
-	Copyright (c) 2004-2015, Apple Inc.
+	Copyright (c) 2004-2016, Apple Inc.
 	All rights reserved.
 
 */
@@ -39,7 +39,7 @@
     id _lastCell;
     NSRect _lastCellFrame;
     BOOL *_autoCompleteCancel;
-    id _reserved[6];
+    id _reserved[6] __unused;
     struct {
         unsigned int _style:4;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSToolbar.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSToolbar.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSToolbar.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSToolbar.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSToolbar.h
 	Application Kit
-	Copyright (c) 2000-2015, Apple Inc.
+	Copyright (c) 2000-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -35,10 +35,13 @@
     NSMutableArray *		_currentItemIdentifiers;
 
     NSView *_fullScreenAccessoryView;
-    id				_res2; 
+    struct {
+        unsigned int _hideBaselineOverride:1;
+        unsigned int _reserved:31;
+    } _tbFlags2;
     
     NSString *			_selectedItemIdentifier;
-    __strong void *		_metrics;
+    void *		_metrics;
 
     id				_delegate;
     NSWindow *			_logicalWindow;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSToolbarItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSToolbarItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSToolbarItem.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSToolbarItem.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSToolbarItem.h
 	Application Kit
-	Copyright (c) 2000-2015, Apple Inc.
+	Copyright (c) 2000-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -64,7 +64,7 @@
     NSSize		_minSize;
     NSSize		_maxSize;
 #if __LP64__
-    id			_toolbarItemReserved;
+    id			_toolbarItemReserved __unused;
 #endif
 }
 
@@ -147,7 +147,7 @@
 @interface NSObject (NSToolbarItemValidation)
 
 /* NSToolbarItemValidation extends the standard validation idea by introducing this new method which is sent to validators for each visible standard NSToolbarItem with a valid target/action pair.  Note: This message is sent from NSToolbarItem's validate method, however validate will not send this message for items that have custom views. */
-- (BOOL)validateToolbarItem:(NSToolbarItem *)theItem;
+- (BOOL)validateToolbarItem:(NSToolbarItem *)item;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSToolbarItemGroup.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSToolbarItemGroup.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSToolbarItemGroup.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSToolbarItemGroup.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSToolbarItemGroup.h
 	Application Kit
-	Copyright (c) 2000-2015, Apple Inc.
+	Copyright (c) 2000-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -22,7 +22,7 @@
       unsigned dirtiedLayout:1;
       unsigned reserved:31;
     } _giFlags;
-    id _giReserved;
+    id _giReserved __unused;
 }
 
 /* Set or get the array of subitems for the toolbar item.  By default, a NSToolbarItemGroup has an empty array of subitems.  You should call this to set the subitems before returning the item to the toolbar.  NSToolbarItemGroups may not contain other NSToolbarItemGroups as subitems.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTouch.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTouch.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTouch.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTouch.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSTouch.h
     Application Kit
-    Copyright (c) 2009-2015, Apple Inc.
+    Copyright (c) 2009-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -33,15 +33,12 @@
     NSInteger _index;
     id _identity;
     NSTouchPhase _phase;
-    NSPoint _normalizedPosition;
+    NSPoint _pos1;
     NSInteger _privateFlags;
     NSView *_view;
     id _reserved1;
-#if ! __LP64__
-    id _reserved2;
-    id _reserved3;
-    id _reserved4;
-#endif
+    NSPoint _pos0;
+    NSInteger _reserved4;
     id _device;
     NSSize  _deviceSize;
 #if ! __LP64__
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTrackingArea.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTrackingArea.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTrackingArea.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTrackingArea.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSTrackingArea.h
         Application Kit
-        Copyright (c) 2006-2015, Apple Inc.
+        Copyright (c) 2006-2016, Apple Inc.
         All rights reserved.
 */
 
@@ -41,7 +41,7 @@
 {
 @private
     NSRect _rect;
-    __weak id _owner;
+    id _owner;
     NSDictionary * _userInfo;
     NSTrackingAreaOptions _options;
     NSInteger _privateFlags;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTreeController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTreeController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTreeController.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTreeController.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSTreeController.h
 	Application Kit
-	Copyright (c) 2003-2015, Apple Inc.
+	Copyright (c) 2003-2016, Apple Inc.
 	All rights reserved.
  */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTreeNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTreeNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTreeNode.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTreeNode.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSTreeNode.h
 	AppKit
-	Copyright (c) 2007-2015, Apple Inc.
+	Copyright (c) 2007-2016, Apple Inc.
 	All rights reserved.
  */
 
@@ -16,7 +16,7 @@
 @interface NSTreeNode : NSObject {
     id _childNodesProxy;
     id _representedObject;
-    __strong void *_observationInfo;
+    void *_observationInfo;
     id _reserved2;
     NSMutableArray *_childNodes;
     NSTreeNode *_parentNode;//not retained
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTypesetter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTypesetter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTypesetter.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTypesetter.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,6 +1,6 @@
 /* 
 	NSTypesetter.h
-	Copyright (c) 1994-2015, Apple Inc.  All rights reserved. 
+	Copyright (c) 1994-2016, Apple Inc.  All rights reserved. 
 
 	An abstract class to lay glyphs out in horizontal or vertical boxes	
 */
@@ -130,7 +130,7 @@
 
 /* Factory methods */
 + (id)sharedSystemTypesetter;
-+ (id)sharedSystemTypesetterForBehavior:(NSTypesetterBehavior)theBehavior;
++ (id)sharedSystemTypesetterForBehavior:(NSTypesetterBehavior)behavior;
 + (NSTypesetterBehavior)defaultTypesetterBehavior;
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserActivity.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserActivity.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserActivity.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserActivity.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSUserActivity.h
     Application Kit
-    Copyright (c) 2014-2015, Apple Inc.
+    Copyright (c) 2014-2016, Apple Inc.
     All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserDefaultsController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserDefaultsController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserDefaultsController.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserDefaultsController.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSUserDefaultsController.h
 	Application Kit
-	Copyright (c) 2002-2015, Apple Inc.
+	Copyright (c) 2002-2016, Apple Inc.
 	All rights reserved.
  */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserInterfaceItemIdentification.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserInterfaceItemIdentification.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserInterfaceItemIdentification.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserInterfaceItemIdentification.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSUserInterfaceItemIdentification.h
     Application Kit
-    Copyright (c) 2006-2015, Apple Inc.
+    Copyright (c) 2006-2016, Apple Inc.
     All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserInterfaceItemSearching.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserInterfaceItemSearching.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserInterfaceItemSearching.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserInterfaceItemSearching.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSUserInterfaceItemSearching.h
     Application Kit
-    Copyright (c) 2008-2015, Apple Inc.
+    Copyright (c) 2008-2016, Apple Inc.
     All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserInterfaceLayout.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserInterfaceLayout.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserInterfaceLayout.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserInterfaceLayout.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSUserInterfaceLayout.h
     Application Kit
-    Copyright (c) 2015-2015, Apple Inc.
+    Copyright (c) 2015-2016, Apple Inc.
     All rights reserved.
  */
 
@@ -15,4 +15,4 @@
 typedef NS_ENUM(NSInteger, NSUserInterfaceLayoutOrientation) {
     NSUserInterfaceLayoutOrientationHorizontal = 0,
     NSUserInterfaceLayoutOrientationVertical = 1
-} NS_ENUM_AVAILABLE_MAC(10_9);
\ No newline at end of file
+} NS_ENUM_AVAILABLE_MAC(10_9);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserInterfaceValidation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserInterfaceValidation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserInterfaceValidation.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSUserInterfaceValidation.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSUserInterfaceValidation.h
 	Application Kit
-	Copyright (c) 1999-2015, Apple Inc.
+	Copyright (c) 1999-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -18,16 +18,16 @@
     i.e.
         @protocol NSValidatedToobarItem <NSValidatedUserInterfaceItem>
         - (NSImage *)image;
-        - (void)setImage:(NSImage *)theImage
+        - (void)setImage:(NSImage *)image
         - (NSString *)toolTip;
-        - (void)setToolTip:(NSString *)theToolTip;
+        - (void)setToolTip:(NSString *)toolTip;
         @end
 
  2) Declare validation method for validators
     You should declare your new selector that takes your object as the argument.
     i.e.
         @protocol NSToolbarItemValidations
-        - (BOOL)validateToolbarItem:(id <NSValidatedToobarItem>)theItem;
+        - (BOOL)validateToolbarItem:(id <NSValidatedToobarItem>)item;
         @end
 
  3) Implement your -update method
@@ -54,8 +54,8 @@
     i.e.
         @implementation NSTextView (NSToolbarValidation)
     
-        - (BOOL)validateToolbarItem:(id <NSValidatedToobarItem>)theItem {
-            BOOL returnValue = [self validateUserInterfaceItem:theItem];
+        - (BOOL)validateToolbarItem:(id <NSValidatedToobarItem>)item {
+            BOOL returnValue = [self validateUserInterfaceItem:item];
 
             // Your own validation
         
@@ -68,13 +68,13 @@
 NS_ASSUME_NONNULL_BEGIN
 
 @protocol NSValidatedUserInterfaceItem
-- (nullable SEL)action;
-- (NSInteger)tag;
+@property (readonly, nullable) SEL action;
+@property (readonly) NSInteger tag;
 @end
 
 /* Protocol implemented by validator objects */
 @protocol NSUserInterfaceValidations
-- (BOOL)validateUserInterfaceItem:(id <NSValidatedUserInterfaceItem>)anItem;
+- (BOOL)validateUserInterfaceItem:(id <NSValidatedUserInterfaceItem>)item;
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSView.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSView.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSView.h
     Application Kit
-    Copyright (c) 1994-2015, Apple Inc.
+    Copyright (c) 1994-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -155,21 +155,21 @@
 @property (nullable, readonly, assign) NSWindow *window;
 @property (nullable, readonly, assign) NSView *superview;
 @property (copy) NSArray<__kindof NSView *> *subviews;
-- (BOOL)isDescendantOf:(NSView *)aView;
-- (nullable NSView *)ancestorSharedWithView:(NSView *)aView;
+- (BOOL)isDescendantOf:(NSView *)view;
+- (nullable NSView *)ancestorSharedWithView:(NSView *)view;
 @property (nullable, readonly, assign) NSView *opaqueAncestor;
 @property (getter=isHidden) BOOL hidden;
 @property (getter=isHiddenOrHasHiddenAncestor, readonly) BOOL hiddenOrHasHiddenAncestor;
 
 - (void)getRectsBeingDrawn:(const NSRect * __nullable * __nullable)rects count:(nullable NSInteger *)count;
-- (BOOL)needsToDrawRect:(NSRect)aRect;
+- (BOOL)needsToDrawRect:(NSRect)rect;
 @property (readonly) BOOL wantsDefaultClipping;
 - (void)viewDidHide NS_AVAILABLE_MAC(10_5);
 - (void)viewDidUnhide NS_AVAILABLE_MAC(10_5);
 
-- (void)addSubview:(NSView *)aView;
-- (void)addSubview:(NSView *)aView positioned:(NSWindowOrderingMode)place relativeTo:(nullable NSView *)otherView;
-- (void)sortSubviewsUsingFunction:(NSComparisonResult (*)(__kindof NSView *, __kindof NSView *,  void * __nullable))compare context:(nullable void *)context;
+- (void)addSubview:(NSView *)view;
+- (void)addSubview:(NSView *)view positioned:(NSWindowOrderingMode)place relativeTo:(nullable NSView *)otherView;
+- (void)sortSubviewsUsingFunction:(NSComparisonResult (NS_NOESCAPE *)(__kindof NSView *, __kindof NSView *,  void * __nullable))compare context:(nullable void *)context;
 
 /* NOTE: In general, it is good practice to call 'super' for the viewWill* and viewDid* methods. Some AppKit subclasses, such as NSTableView, depend on this behavior, and calling super is required for things to work properly.
  */
@@ -215,35 +215,35 @@
  */
 @property (getter=isOpaque, readonly) BOOL opaque;
 
-- (NSPoint)convertPoint:(NSPoint)aPoint fromView:(nullable NSView *)aView;
-- (NSPoint)convertPoint:(NSPoint)aPoint toView:(nullable NSView *)aView;
-- (NSSize)convertSize:(NSSize)aSize fromView:(nullable NSView *)aView;
-- (NSSize)convertSize:(NSSize)aSize toView:(nullable NSView *)aView;
-- (NSRect)convertRect:(NSRect)aRect fromView:(nullable NSView *)aView;
-- (NSRect)convertRect:(NSRect)aRect toView:(nullable NSView *)aView;
+- (NSPoint)convertPoint:(NSPoint)point fromView:(nullable NSView *)view;
+- (NSPoint)convertPoint:(NSPoint)point toView:(nullable NSView *)view;
+- (NSSize)convertSize:(NSSize)size fromView:(nullable NSView *)view;
+- (NSSize)convertSize:(NSSize)size toView:(nullable NSView *)view;
+- (NSRect)convertRect:(NSRect)rect fromView:(nullable NSView *)view;
+- (NSRect)convertRect:(NSRect)rect toView:(nullable NSView *)view;
 
 /* Uses NSIntegralRectWithOptions() to produce a backing store pixel aligned rectangle from the given input rectangle in local view coordinates.
  */
-- (NSRect)backingAlignedRect:(NSRect)aRect options:(NSAlignmentOptions)options NS_AVAILABLE_MAC(10_7);
-- (NSRect)centerScanRect:(NSRect)aRect;
+- (NSRect)backingAlignedRect:(NSRect)rect options:(NSAlignmentOptions)options NS_AVAILABLE_MAC(10_7);
+- (NSRect)centerScanRect:(NSRect)rect;
 
 /* New methods for converting to and from backing store pixels */
 
-- (NSPoint)convertPointToBacking:(NSPoint)aPoint NS_AVAILABLE_MAC(10_7);
-- (NSPoint)convertPointFromBacking:(NSPoint)aPoint NS_AVAILABLE_MAC(10_7);
-- (NSSize)convertSizeToBacking:(NSSize)aSize NS_AVAILABLE_MAC(10_7);
-- (NSSize)convertSizeFromBacking:(NSSize)aSize NS_AVAILABLE_MAC(10_7);
-- (NSRect)convertRectToBacking:(NSRect)aRect NS_AVAILABLE_MAC(10_7);
-- (NSRect)convertRectFromBacking:(NSRect)aRect NS_AVAILABLE_MAC(10_7);
+- (NSPoint)convertPointToBacking:(NSPoint)point NS_AVAILABLE_MAC(10_7);
+- (NSPoint)convertPointFromBacking:(NSPoint)point NS_AVAILABLE_MAC(10_7);
+- (NSSize)convertSizeToBacking:(NSSize)size NS_AVAILABLE_MAC(10_7);
+- (NSSize)convertSizeFromBacking:(NSSize)size NS_AVAILABLE_MAC(10_7);
+- (NSRect)convertRectToBacking:(NSRect)rect NS_AVAILABLE_MAC(10_7);
+- (NSRect)convertRectFromBacking:(NSRect)rect NS_AVAILABLE_MAC(10_7);
 
 /* Use these methods to transform geometry between a view's interior (bounds) coordinate space and its layer's interior coordinate space.  The layer's space is virtual, and doesn't take into account the layer's contentsScale setting.  For conversion between view space and layer pixels, use -convert(Point/Size/Rect)(To/From)Backing: instead.
 */
-- (NSPoint)convertPointToLayer:(NSPoint)aPoint NS_AVAILABLE_MAC(10_7);
-- (NSPoint)convertPointFromLayer:(NSPoint)aPoint NS_AVAILABLE_MAC(10_7);
-- (NSSize)convertSizeToLayer:(NSSize)aSize NS_AVAILABLE_MAC(10_7);
-- (NSSize)convertSizeFromLayer:(NSSize)aSize NS_AVAILABLE_MAC(10_7);
-- (NSRect)convertRectToLayer:(NSRect)aRect NS_AVAILABLE_MAC(10_7);
-- (NSRect)convertRectFromLayer:(NSRect)aRect NS_AVAILABLE_MAC(10_7);
+- (NSPoint)convertPointToLayer:(NSPoint)point NS_AVAILABLE_MAC(10_7);
+- (NSPoint)convertPointFromLayer:(NSPoint)point NS_AVAILABLE_MAC(10_7);
+- (NSSize)convertSizeToLayer:(NSSize)size NS_AVAILABLE_MAC(10_7);
+- (NSSize)convertSizeFromLayer:(NSSize)size NS_AVAILABLE_MAC(10_7);
+- (NSRect)convertRectToLayer:(NSRect)rect NS_AVAILABLE_MAC(10_7);
+- (NSRect)convertRectFromLayer:(NSRect)rect NS_AVAILABLE_MAC(10_7);
 
 /* Reports whether AppKit may invoke the view's -drawRect: method on a background thread, where it would otherwise be invoked on the main thread.  Defaults to NO.
 */
@@ -269,26 +269,26 @@
 - (void)displayRectIgnoringOpacity:(NSRect)rect;
 - (void)displayIfNeededInRectIgnoringOpacity:(NSRect)rect;
 - (void)drawRect:(NSRect)dirtyRect;
-- (void)displayRectIgnoringOpacity:(NSRect)aRect inContext:(NSGraphicsContext *)context;
+- (void)displayRectIgnoringOpacity:(NSRect)rect inContext:(NSGraphicsContext *)context;
 
 - (nullable NSBitmapImageRep *)bitmapImageRepForCachingDisplayInRect:(NSRect)rect;
 - (void)cacheDisplayInRect:(NSRect)rect toBitmapImageRep:(NSBitmapImageRep *)bitmapImageRep;
 - (void)viewWillDraw NS_AVAILABLE_MAC(10_5);
 
-- (void)scrollPoint:(NSPoint)aPoint;
-- (BOOL)scrollRectToVisible:(NSRect)aRect;
-- (BOOL)autoscroll:(NSEvent *)theEvent;
+- (void)scrollPoint:(NSPoint)point;
+- (BOOL)scrollRectToVisible:(NSRect)rect;
+- (BOOL)autoscroll:(NSEvent *)event;
 - (NSRect)adjustScroll:(NSRect)newVisible;
-- (void)scrollRect:(NSRect)aRect by:(NSSize)delta;
+- (void)scrollRect:(NSRect)rect by:(NSSize)delta;
 - (void)translateRectsNeedingDisplayInRect:(NSRect)clipRect by:(NSSize)delta NS_AVAILABLE_MAC(10_5);
 
-- (nullable NSView *)hitTest:(NSPoint)aPoint;
-- (BOOL)mouse:(NSPoint)aPoint inRect:(NSRect)aRect;
-- (nullable __kindof NSView *)viewWithTag:(NSInteger)aTag;
+- (nullable NSView *)hitTest:(NSPoint)point;
+- (BOOL)mouse:(NSPoint)point inRect:(NSRect)rect;
+- (nullable __kindof NSView *)viewWithTag:(NSInteger)tag;
 @property (readonly) NSInteger tag;
-- (BOOL)performKeyEquivalent:(NSEvent *)theEvent;
-- (BOOL)acceptsFirstMouse:(nullable NSEvent *)theEvent;
-- (BOOL)shouldDelayWindowOrderingForEvent:(NSEvent *)theEvent;
+- (BOOL)performKeyEquivalent:(NSEvent *)event;
+- (BOOL)acceptsFirstMouse:(nullable NSEvent *)event;
+- (BOOL)shouldDelayWindowOrderingForEvent:(NSEvent *)event;
 @property (readonly) BOOL needsPanelToBecomeKey;
 @property (readonly) BOOL mouseDownCanMoveWindow;
 
@@ -300,12 +300,12 @@
 */
 @property BOOL wantsRestingTouches NS_AVAILABLE_MAC(10_6);
 
-- (void)addCursorRect:(NSRect)aRect cursor:(NSCursor *)anObj;
-- (void)removeCursorRect:(NSRect)aRect cursor:(NSCursor *)anObj;
+- (void)addCursorRect:(NSRect)rect cursor:(NSCursor *)object;
+- (void)removeCursorRect:(NSRect)rect cursor:(NSCursor *)object;
 - (void)discardCursorRects;
 - (void)resetCursorRects;
 
-- (NSTrackingRectTag)addTrackingRect:(NSRect)aRect owner:(id)anObject userData:(nullable void *)data assumeInside:(BOOL)flag;
+- (NSTrackingRectTag)addTrackingRect:(NSRect)rect owner:(id)owner userData:(nullable void *)data assumeInside:(BOOL)flag;
 - (void)removeTrackingRect:(NSTrackingRectTag)tag;
 
 - (CALayer *)makeBackingLayer NS_AVAILABLE_MAC(10_6);
@@ -384,7 +384,7 @@
 - (void)didCloseMenu:(NSMenu *)menu withEvent:(nullable NSEvent *)event NS_AVAILABLE_MAC(10_11);
 
 @property (nullable, copy) NSString *toolTip;
-- (NSToolTipTag)addToolTipRect:(NSRect)aRect owner:(id)anObject userData:(nullable void *)data;
+- (NSToolTipTag)addToolTipRect:(NSRect)rect owner:(id)owner userData:(nullable void *)data;
 - (void)removeToolTip:(NSToolTipTag)tag;
 - (void)removeAllToolTips;
 
@@ -501,7 +501,7 @@
 - (void)adjustPageWidthNew:(CGFloat *)newRight left:(CGFloat)oldLeft right:(CGFloat)oldRight limit:(CGFloat)rightLimit;
 - (void)adjustPageHeightNew:(CGFloat *)newBottom top:(CGFloat)oldTop bottom:(CGFloat)oldBottom limit:(CGFloat)bottomLimit;
 - (NSRect)rectForPage:(NSInteger)page;
-- (NSPoint)locationOfPrintRect:(NSRect)aRect;
+- (NSPoint)locationOfPrintRect:(NSRect)rect;
 - (void)drawPageBorderWithSize:(NSSize)borderSize;
 @property (readonly, copy) NSAttributedString *pageHeader;
 @property (readonly, copy) NSAttributedString *pageFooter;
@@ -515,7 +515,7 @@
 - (void)beginDocument;
 - (void)endDocument;
 
-- (void)beginPageInRect:(NSRect)aRect atPlacement:(NSPoint)location;
+- (void)beginPageInRect:(NSRect)rect atPlacement:(NSPoint)location;
 - (void)endPage;
 @end
 
@@ -529,8 +529,8 @@
 - (void)registerForDraggedTypes:(NSArray<NSString *> *)newTypes;
 - (void)unregisterDraggedTypes;
 
-- (BOOL)dragFile:(NSString *)filename fromRect:(NSRect)rect slideBack:(BOOL)aFlag event:(NSEvent *)event;
-- (BOOL)dragPromisedFilesOfTypes:(NSArray<NSString *> *)typeArray fromRect:(NSRect)rect source:(id)sourceObject slideBack:(BOOL)aFlag event:(NSEvent *)event;
+- (BOOL)dragFile:(NSString *)filename fromRect:(NSRect)rect slideBack:(BOOL)flag event:(NSEvent *)event;
+- (BOOL)dragPromisedFilesOfTypes:(NSArray<NSString *> *)typeArray fromRect:(NSRect)rect source:(id)sourceObject slideBack:(BOOL)flag event:(NSEvent *)event;
 @end
 
 @interface NSView (NSFullScreenMode) 
@@ -593,19 +593,19 @@
 
 /* This drag method as been deprecated in favor of beginDraggingSessionWithItems:event:source:
  */
-- (void)dragImage:(NSImage *)anImage at:(NSPoint)viewLocation offset:(NSSize)initialOffset event:(NSEvent *)event pasteboard:(NSPasteboard *)pboard source:(id)sourceObj slideBack:(BOOL)slideFlag NS_DEPRECATED_MAC(10_0, 10_7, "Use -beginDraggingSessionWithItems:event:source: instead");
+- (void)dragImage:(NSImage *)image at:(NSPoint)viewLocation offset:(NSSize)initialOffset event:(NSEvent *)event pasteboard:(NSPasteboard *)pboard source:(id)sourceObj slideBack:(BOOL)slideFlag NS_DEPRECATED_MAC(10_0, 10_7, "Use -beginDraggingSessionWithItems:event:source: instead");
 
 /* These methods are deprecated on 10.7 and later. */
-- (NSPoint)convertPointToBase:(NSPoint)aPoint NS_DEPRECATED_MAC(10_5, 10_7);
-- (NSPoint)convertPointFromBase:(NSPoint)aPoint NS_DEPRECATED_MAC(10_5, 10_7);
-- (NSSize)convertSizeToBase:(NSSize)aSize NS_DEPRECATED_MAC(10_5, 10_7);
-- (NSSize)convertSizeFromBase:(NSSize)aSize NS_DEPRECATED_MAC(10_5, 10_7);
-- (NSRect)convertRectToBase:(NSRect)aRect NS_DEPRECATED_MAC(10_5, 10_7);
-- (NSRect)convertRectFromBase:(NSRect)aRect NS_DEPRECATED_MAC(10_5, 10_7);
+- (NSPoint)convertPointToBase:(NSPoint)point NS_DEPRECATED_MAC(10_5, 10_7);
+- (NSPoint)convertPointFromBase:(NSPoint)point NS_DEPRECATED_MAC(10_5, 10_7);
+- (NSSize)convertSizeToBase:(NSSize)size NS_DEPRECATED_MAC(10_5, 10_7);
+- (NSSize)convertSizeFromBase:(NSSize)size NS_DEPRECATED_MAC(10_5, 10_7);
+- (NSRect)convertRectToBase:(NSRect)rect NS_DEPRECATED_MAC(10_5, 10_7);
+- (NSRect)convertRectFromBase:(NSRect)rect NS_DEPRECATED_MAC(10_5, 10_7);
 
 /* This method is deprecated in 10.8 and higher. On MacOS it has historically not done anything.
  */
-- (BOOL)performMnemonic:(NSString *)theString NS_DEPRECATED_MAC(10_0, 10_8);
+- (BOOL)performMnemonic:(NSString *)string NS_DEPRECATED_MAC(10_0, 10_8);
 
 /* shouldDrawColor is no longer used by AppKit.
  */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSViewController.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSViewController.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSViewController.h
 	Application Kit
-	Copyright (c) 2006-2015, Apple Inc.
+	Copyright (c) 2006-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -57,7 +57,7 @@
     unsigned int _viewIsAppearing:1;
     unsigned int _delayViewDidAppear:1;
     unsigned int _isContentViewController:1;
-    unsigned int _reserved:29;
+    unsigned int _reserved:29 __unused;
 }
 
 /* The designated initializer. The specified nib should typically have the class of the file's owner set to NSViewController, or a subclass of yours, with the "view" outlet connected to a view. If you pass in a nil nib name then -nibName will return nil. -loadView can be used to assign a view before -view is invoked. If you pass in a nil bundle then -nibBundle will return nil and -loadView will interpret it using the same rules as -[NSNib initWithNibNamed:bundle:].
@@ -160,7 +160,7 @@
 
 /* The view controllers that were presented by this view controller. In other words, 'self' displayed each of the items in the array. This is a one-to-many relationship.
 */
-@property (nullable, readonly, assign) NSArray<__kindof NSViewController *> *presentedViewControllers NS_AVAILABLE_MAC(10_10);
+@property (nullable, readonly) NSArray<__kindof NSViewController *> *presentedViewControllers NS_AVAILABLE_MAC(10_10);
 
 /* The view controller that presented this view controller (or its farthest ancestor). In other words, 'presentingViewController' is the one that displayed 'self' to screen.
 */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSVisualEffectView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSVisualEffectView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSVisualEffectView.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSVisualEffectView.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSVisualEffectView.h
     Application Kit
-    Copyright (c) 2014-2015, Apple Inc.
+    Copyright (c) 2014-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -17,6 +17,9 @@
     // Many of these colors are dynamic and depend on the current NSAppearance set on the view (or its parent view)
     NSVisualEffectMaterialAppearanceBased = 0, // Maps to Light or Dark, depending on the appearance set on the view
     NSVisualEffectMaterialTitlebar = 3, // Mainly designed to be used for NSVisualEffectBlendingModeWithinWindow
+    /* A special material for selection. The material will vary depending on the effectiveAppearance, active state, and emphasized state.
+     */
+    NSVisualEffectMaterialSelection = 4,
     NSVisualEffectMaterialMenu NS_ENUM_AVAILABLE_MAC(10_11) = 5,
     NSVisualEffectMaterialPopover NS_ENUM_AVAILABLE_MAC(10_11) = 6,
     NSVisualEffectMaterialSidebar NS_ENUM_AVAILABLE_MAC(10_11) = 7,
@@ -48,7 +51,7 @@
 NS_CLASS_AVAILABLE_MAC(10_10)
 @interface NSVisualEffectView : NSView {
 @private
-    __strong struct NSVisualEffectViewInternal *_NSVisualEffectViewInternal;
+    struct NSVisualEffectViewInternal *_NSVisualEffectViewInternal;
     
 #if !__LP64__
     uint8_t _reserved[48];
@@ -71,7 +74,7 @@
     unsigned int _appearsDarker:1;
     unsigned int _inheritsBlendGroup:1;
     unsigned int _registeredForFrameChanges:1;
-    unsigned int _reservedFlags:18;
+    unsigned int _reservedFlags:18 __unused;
 }
 
 /* The default value is NSVisualEffectMaterialAppearanceBased; the material is updated to be the correct material based on the appearance set on this view.
@@ -96,6 +99,10 @@
  */
 @property(nullable, retain) NSImage *maskImage;
 
+/* Some materials (currently only the Selection material) have a different look when the view is emphasized, meaning the view that is showing the selection has firstResponder status. The default value is NO.
+ */
+@property (getter=isEmphasized) BOOL emphasized NS_AVAILABLE_MAC(10_12);
+
 /* Some things this class overrides; it is required to call super if you subclass and override these.
  */
 - (void)viewDidMoveToWindow NS_REQUIRES_SUPER;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindow.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindow.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindow.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindow.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,8 +1,8 @@
 /*
-	NSWindow.h
-	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
-	All rights reserved.
+    NSWindow.h
+    Application Kit
+    Copyright (c) 1994-2016, Apple Inc.
+    All rights reserved.
 */
 
 #import <Foundation/NSArray.h>
@@ -21,39 +21,43 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-@class NSButton, NSButtonCell, NSColor, NSImage, NSPasteboard, NSScreen;
-@class NSNotification, NSText, NSView, NSMutableSet, NSSet, NSDate;
-@class NSToolbar, NSGraphicsContext, NSURL, NSColorSpace;
-@class NSDockTile, NSViewController, NSTitlebarAccessoryViewController;
+@class NSButton, NSButtonCell, NSColor, NSImage, NSPasteboard, NSScreen, NSNotification, NSText, NSView, NSMutableSet, NSSet, NSDate, NSToolbar, NSGraphicsContext, NSURL, NSColorSpace, NSDockTile, NSViewController, NSTitlebarAccessoryViewController, NSWindowAuxiliary, NSEvent, NSWindowController;
 
 @protocol NSWindowDelegate;
 
 #define NSAppKitVersionNumberWithCustomSheetPosition 686.0
 #define NSAppKitVersionNumberWithDeferredWindowDisplaySupport		1019.0
 
-enum {
-    NSBorderlessWindowMask = 0,
-    NSTitledWindowMask = 1 << 0,
-    NSClosableWindowMask = 1 << 1,
-    NSMiniaturizableWindowMask = 1 << 2,
-    NSResizableWindowMask	= 1 << 3,
+typedef NS_OPTIONS(NSUInteger, NSWindowStyleMask) {
+    NSWindowStyleMaskBorderless = 0,
+    NSWindowStyleMaskTitled = 1 << 0,
+    NSWindowStyleMaskClosable = 1 << 1,
+    NSWindowStyleMaskMiniaturizable = 1 << 2,
+    NSWindowStyleMaskResizable	= 1 << 3,
     
-/* Specifies a window with textured background. Textured windows generally don't draw a top border line under the titlebar/toolbar. To get that line, use the NSUnifiedTitleAndToolbarWindowMask mask.
- */
-    NSTexturedBackgroundWindowMask = 1 << 8,
+    /* Specifies a window with textured background. Textured windows generally don't draw a top border line under the titlebar/toolbar. To get that line, use the NSUnifiedTitleAndToolbarWindowMask mask.
+     */
+    NSWindowStyleMaskTexturedBackground = 1 << 8,
     
-/* Specifies a window whose titlebar and toolbar have a unified look - that is, a continuous background. Under the titlebar and toolbar a horizontal separator line will appear.
- */
-    NSUnifiedTitleAndToolbarWindowMask = 1 << 12,
+    /* Specifies a window whose titlebar and toolbar have a unified look - that is, a continuous background. Under the titlebar and toolbar a horizontal separator line will appear.
+     */
+    NSWindowStyleMaskUnifiedTitleAndToolbar = 1 << 12,
     
-/* When set, the window will appear full screen. This mask is automatically toggled when toggleFullScreen: is called.
- */
-    NSFullScreenWindowMask NS_ENUM_AVAILABLE_MAC(10_7) = 1 << 14,
+    /* When set, the window will appear full screen. This mask is automatically toggled when toggleFullScreen: is called.
+     */
+    NSWindowStyleMaskFullScreen NS_ENUM_AVAILABLE_MAC(10_7) = 1 << 14,
     
-/* If set, the contentView will consume the full size of the window; it can be combined with other window style masks, but is only respected for windows with a titlebar.
-    Utilizing this mask opts-in to layer-backing. Utilize the contentLayoutRect or auto-layout contentLayoutGuide to layout views underneath the titlebar/toolbar area.
- */
-    NSFullSizeContentViewWindowMask NS_ENUM_AVAILABLE_MAC(10_10) = 1 << 15
+    /* If set, the contentView will consume the full size of the window; it can be combined with other window style masks, but is only respected for windows with a titlebar.
+     Utilizing this mask opts-in to layer-backing. Utilize the contentLayoutRect or auto-layout contentLayoutGuide to layout views underneath the titlebar/toolbar area.
+     */
+    NSWindowStyleMaskFullSizeContentView NS_ENUM_AVAILABLE_MAC(10_10) = 1 << 15,
+    
+    /* The following are only applicable for NSPanel (or a subclass thereof)
+     */
+    NSWindowStyleMaskUtilityWindow			= 1 << 4,
+    NSWindowStyleMaskDocModalWindow 		= 1 << 6,
+    NSWindowStyleMaskNonactivatingPanel		= 1 << 7, // Specifies that a panel that does not activate the owning application
+    NSWindowStyleMaskHUDWindow NS_ENUM_AVAILABLE_MAC(10_6) = 1 << 13 // Specifies a heads up display panel
 };
 
 // Additional NSModalResponse values
@@ -96,9 +100,10 @@
     NSWindowCollectionBehaviorParticipatesInCycle NS_ENUM_AVAILABLE_MAC(10_6) = 1 << 5,     // default behavior if windowLevel == NSNormalWindowLevel
     NSWindowCollectionBehaviorIgnoresCycle NS_ENUM_AVAILABLE_MAC(10_6) = 1 << 6,            // default behavior if windowLevel != NSNormalWindowLevel
     
-    /* You may specify at most one of NSWindowCollectionBehaviorFullScreenPrimary or NSWindowCollectionBehaviorFullScreenAuxiliary. */
+    /* You may specify at most one of NSWindowCollectionBehaviorFullScreenPrimary, NSWindowCollectionBehaviorFullScreenAuxiliary, or NSWindowCollectionBehaviorFullScreenNone. */
     NSWindowCollectionBehaviorFullScreenPrimary NS_ENUM_AVAILABLE_MAC(10_7) = 1 << 7,       // the frontmost window with this collection behavior will be the fullscreen window.
     NSWindowCollectionBehaviorFullScreenAuxiliary NS_ENUM_AVAILABLE_MAC(10_7) = 1 << 8,     // windows with this collection behavior can be shown with the fullscreen window.
+    NSWindowCollectionBehaviorFullScreenNone NS_ENUM_AVAILABLE_MAC(10_7) = 1 << 9, // The window can not be made fullscreen when this bit is set
     
     /* 	You may specify at most one of NSWindowCollectionBehaviorFullScreenAllowsTiling or NSWindowCollectionBehaviorFullScreenDisallowsTiling, or an assertion will be raised.
      
@@ -158,21 +163,30 @@
     NSWindowToolbarButton,
     NSWindowDocumentIconButton,
     NSWindowDocumentVersionsButton NS_ENUM_AVAILABLE_MAC(10_7) = 6,
-    NSWindowFullScreenButton NS_ENUM_AVAILABLE_MAC(10_7)
+    NSWindowFullScreenButton NS_ENUM_DEPRECATED_MAC(10_7, 10_12, "The standard window button for NSWindowFullScreenButton is always nil; use NSWindowZoomButton instead"),
 };
 
 typedef NS_ENUM(NSInteger, NSWindowTitleVisibility) {
     /* The default mode has a normal window title and titlebar buttons. */
-    NSWindowTitleVisible  = 0,
+    NSWindowTitleVisible = 0,
     /* The always hidden mode hides the title and moves the toolbar up into the area previously occupied by the title. */
     NSWindowTitleHidden = 1,
 } NS_ENUM_AVAILABLE_MAC(10_10);
 
 #define NSEventDurationForever  DBL_MAX
 
-@class NSWindowAuxiliary;
-@class NSEvent;
-@class NSWindowController;
+typedef NS_ENUM(NSInteger, NSWindowUserTabbingPreference) {
+    NSWindowUserTabbingPreferenceManual,
+    NSWindowUserTabbingPreferenceAlways,
+    NSWindowUserTabbingPreferenceInFullScreen,
+} NS_ENUM_AVAILABLE_MAC(10_12);
+
+typedef NS_ENUM(NSInteger, NSWindowTabbingMode) {
+    NSWindowTabbingModeAutomatic, // The system automatically prefers to tab this window when appropriate
+    NSWindowTabbingModePreferred, // The window explicitly should prefer to tab when shown
+    NSWindowTabbingModeDisallowed // The window explicitly should not prefer to tab when shown
+}  NS_ENUM_AVAILABLE_MAC(10_12);
+
 
 @interface NSWindow : NSResponder <NSAnimatablePropertyContainer, NSUserInterfaceValidations, NSUserInterfaceItemIdentification, NSAppearanceCustomization, NSAccessibilityElement, NSAccessibility>
 {
@@ -193,7 +207,8 @@
     unsigned char	_postingDisabled;
     unsigned char	_styleMask;
     unsigned char	_flushDisabled;
-    unsigned char	_reservedWindow1;
+    unsigned char	_ignoreResignEvent:1;
+    unsigned char	_reservedWindow:7;
     void		*_cursorRects;
     void                *_trectTable;
     NSImage		*_miniIcon;
@@ -261,23 +276,25 @@
         unsigned int  makingFirstResponderForMouseDown:1;
         unsigned int  needsZoom:1;
         unsigned int  sentWindowNeedsDisplayMsg:1;
-        unsigned int  unused:2;
+        unsigned int  wasModalAtSometime:1;
+        unsigned int  windowWillBecomeFS:1;
     } _wFlags;
     id _defaultButtonCell;
     NSView *_initialFirstResponder;
     NSWindowAuxiliary *_auxiliaryStorage;
 }
 
-+ (NSRect)frameRectForContentRect:(NSRect)cRect styleMask:(NSUInteger)aStyle;
-+ (NSRect)contentRectForFrameRect:(NSRect)fRect styleMask:(NSUInteger)aStyle;
-+ (CGFloat)minFrameWidthWithTitle:(NSString *)aTitle styleMask:(NSUInteger)aStyle;
++ (NSRect)frameRectForContentRect:(NSRect)cRect styleMask:(NSWindowStyleMask)style;
++ (NSRect)contentRectForFrameRect:(NSRect)fRect styleMask:(NSWindowStyleMask)style;
++ (CGFloat)minFrameWidthWithTitle:(NSString *)title styleMask:(NSWindowStyleMask)style;
 + (NSWindowDepth)defaultDepthLimit;
 
 - (NSRect)frameRectForContentRect:(NSRect)contentRect;
 - (NSRect)contentRectForFrameRect:(NSRect)frameRect;
 
-- (instancetype)initWithContentRect:(NSRect)contentRect styleMask:(NSUInteger)aStyle backing:(NSBackingStoreType)bufferingType defer:(BOOL)flag;
-- (instancetype)initWithContentRect:(NSRect)contentRect styleMask:(NSUInteger)aStyle backing:(NSBackingStoreType)bufferingType defer:(BOOL)flag screen:(nullable NSScreen *)screen;
+- (instancetype)initWithContentRect:(NSRect)contentRect styleMask:(NSWindowStyleMask)style backing:(NSBackingStoreType)bufferingType defer:(BOOL)flag NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithContentRect:(NSRect)contentRect styleMask:(NSWindowStyleMask)style backing:(NSBackingStoreType)bufferingType defer:(BOOL)flag screen:(nullable NSScreen *)screen;
+- (instancetype)initWithCoder:(NSCoder *)coder NS_UNAVAILABLE; // Use initWithContentRect:. This method will throw an exception for coders that support allowsKeyedCoding, and is only available for compatability with non keyed coding.
 
 @property (copy) NSString *title;
 
@@ -316,26 +333,29 @@
 @property (nullable, strong) __kindof NSView *contentView;
 @property (nullable, assign) id<NSWindowDelegate> delegate;
 @property (readonly) NSInteger windowNumber;
-@property NSUInteger styleMask;
-/* Valid styleMask settings have the same restrictions as the styleMask passed to -initWithContentRect:styleMask:backing:defer:.  Some styleMask changes will cause the view hierarchy to be rebuilt, since there is a different subclass for the top level view of a borderless window than for the top level view of a titled window. */
-- (void)setStyleMask:(NSUInteger)styleMask NS_AVAILABLE_MAC(10_6);
-- (nullable NSText *)fieldEditor:(BOOL)createFlag forObject:(nullable id)anObject;
-- (void)endEditingFor:(nullable id)anObject;
+
+/* NOTE: The styleMask can only be set on OS 10.6 and later. Valid styleMask settings have the same restrictions as the styleMask passed to -initWithContentRect:styleMask:backing:defer:.  Some styleMask changes will cause the view hierarchy to be rebuilt, since there is a different subclass for the top level view of a borderless window than for the top level view of a titled window. */
+@property NSWindowStyleMask styleMask;
+
+- (nullable NSText *)fieldEditor:(BOOL)createFlag forObject:(nullable id)object;
+- (void)endEditingFor:(nullable id)object;
 
 - (NSRect)constrainFrameRect:(NSRect)frameRect toScreen:(nullable NSScreen *)screen;
 - (void)setFrame:(NSRect)frameRect display:(BOOL)flag;
-- (void)setContentSize:(NSSize)aSize;
-- (void)setFrameOrigin:(NSPoint)aPoint;
-- (void)setFrameTopLeftPoint:(NSPoint)aPoint;
+- (void)setContentSize:(NSSize)size;
+- (void)setFrameOrigin:(NSPoint)point;
+- (void)setFrameTopLeftPoint:(NSPoint)point;
 - (NSPoint)cascadeTopLeftFromPoint:(NSPoint)topLeftPoint;
 @property (readonly) NSRect frame;
 
-// smooth resize
-// subclasses can override animationResizeTime: to control the total time for the frame change.
-// newFrame is the rect passed into setFrame:display:animate:
+/*! Subclasses can override \c animationResizeTime: to control the total time for the frame change.
+ \c newFrame is the rect passed into \c setFrame:display:animate:
+ */
 - (NSTimeInterval)animationResizeTime:(NSRect)newFrame;
-// setFrame:display:animate: is equivalent to setFrame:display: if animateFlag is NO
-// If animationFlag is YES, this method will perform a smooth resize of the window, where the total time for the resize is specified by -animationResizeTime:
+
+/*! \c setFrame:display:animate: is equivalent to \c setFrame:display: if the \c animateFlag is NO.
+    If the \c animationFlag is YES, this method will perform a smooth resize of the window, where the total time for the resize is specified by \c -animationResizeTime:
+*/
 - (void)setFrame:(NSRect)frameRect display:(BOOL)displayFlag animate:(BOOL)animateFlag;
 
 @property (readonly) BOOL inLiveResize    NS_AVAILABLE_MAC(10_6);
@@ -363,12 +383,12 @@
 
 - (void)update;
 
-- (BOOL)makeFirstResponder:(nullable NSResponder *)aResponder;
+- (BOOL)makeFirstResponder:(nullable NSResponder *)responder;
 /* firstResponder is Key Value Observing (KVO) compliant. */
 @property (readonly, assign) NSResponder *firstResponder;
 
 @property (readonly) NSInteger resizeFlags;
-- (void)keyDown:(NSEvent *)theEvent;
+- (void)keyDown:(NSEvent *)event;
 - (void)close;
 @property (getter=isReleasedWhenClosed) BOOL releasedWhenClosed;
 - (void)miniaturize:(nullable id)sender;
@@ -376,7 +396,7 @@
 @property (getter=isZoomed, readonly) BOOL zoomed;
 - (void)zoom:(nullable id)sender;
 @property (getter=isMiniaturized, readonly) BOOL miniaturized;
-- (BOOL)tryToPerform:(SEL)anAction with:(nullable id)anObject;
+- (BOOL)tryToPerform:(SEL)action with:(nullable id)object;
 - (nullable id)validRequestorForSendType:(NSString *)sendType returnType:(NSString *)returnType;
 @property (null_resettable, copy) NSColor *backgroundColor;
 
@@ -430,15 +450,15 @@
 @property BOOL preventsApplicationTerminationWhenModal NS_AVAILABLE_MAC(10_6);
 
 /* New methods to convert window coordinates to screen coordinates */
-- (NSRect)convertRectToScreen:(NSRect)aRect NS_AVAILABLE_MAC(10_7);
-- (NSRect)convertRectFromScreen:(NSRect)aRect NS_AVAILABLE_MAC(10_7);
+- (NSRect)convertRectToScreen:(NSRect)rect NS_AVAILABLE_MAC(10_7);
+- (NSRect)convertRectFromScreen:(NSRect)rect NS_AVAILABLE_MAC(10_7);
 
 /* New methods to convert to/from a pixel integral backing store space */
-- (NSRect)convertRectToBacking:(NSRect)aRect NS_AVAILABLE_MAC(10_7);
-- (NSRect)convertRectFromBacking:(NSRect)aRect NS_AVAILABLE_MAC(10_7);
+- (NSRect)convertRectToBacking:(NSRect)rect NS_AVAILABLE_MAC(10_7);
+- (NSRect)convertRectFromBacking:(NSRect)rect NS_AVAILABLE_MAC(10_7);
 
 /* Use NSIntegralRectWithOptions() to produce a backing store pixel aligned rectangle from the given input rectangle in window coordinates. */
-- (NSRect)backingAlignedRect:(NSRect)aRect options:(NSAlignmentOptions)options NS_AVAILABLE_MAC(10_7);
+- (NSRect)backingAlignedRect:(NSRect)rect options:(NSAlignmentOptions)options NS_AVAILABLE_MAC(10_7);
 
 /* Returns the scale factor representing the number of backing store pixels corresponding to each linear unit in window space on this NSWindow. This method is provided for rare cases when the explicit scale factor is needed. Please use -convert*ToBacking: methods whenever possible. */
 @property (readonly) CGFloat backingScaleFactor NS_AVAILABLE_MAC(10_7); 
@@ -451,13 +471,6 @@
 - (NSData *)dataWithPDFInsideRect:(NSRect)rect;
 - (void)print:(nullable id)sender;
 
-- (void)disableCursorRects;
-- (void)enableCursorRects;
-- (void)discardCursorRects;
-@property (readonly) BOOL areCursorRectsEnabled;
-- (void)invalidateCursorRectsForView:(NSView *)aView;
-- (void)resetCursorRects;
-
 /*
  Default is NO. Set to YES to allow a window to display tooltips even when the application is in the background.  Note that, enabling tooltips in an inactive application will cause the app to do work any time the mouse passes over the window.  This can degrade system performance.
  Returns YES if this window displays tooltips even when the application is in the background.  To configure this setting you should call setAllowsToolTipsWhenApplicationIsInactive: instead of overriding -allowsToolTipsWhenApplicationIsInactive.
@@ -535,7 +548,7 @@
 + (void)removeFrameUsingName:(NSString *)name;
 
 
-- (void)cacheImageInRect:(NSRect)aRect;
+- (void)cacheImageInRect:(NSRect)rect;
 - (void)restoreCachedImage;
 - (void)discardCachedImage;
 
@@ -553,19 +566,7 @@
 @property NSSize minFullScreenContentSize NS_AVAILABLE_MAC(10_11);
 @property NSSize maxFullScreenContentSize NS_AVAILABLE_MAC(10_11);
 
-/* Tracks events matching the supplied mask with the supplied tracking handler until the tracking handler explicitly terminates tracking. Each event is removed from the event queue then passed to the tracking handler. If a matching event does not exist in the event queue, then the main thread blocks in the specified runloop mode until an event of the requested type is received or the timeout expires. If the timeout expires, the tracking handler is called with a nil event. A negative timeout is interpreted as 0. Use NSEventDurationForever to never timeout. Tracking continues until *stop is set to YES. Calls to -nextEventMatchingMask:… are allowed inside the trackingHandler block. This method returns once tracking is terminated.
- */
-- (void)trackEventsMatchingMask:(NSEventMask)mask timeout:(NSTimeInterval)timeout mode:(NSString *)mode handler:(void(^)(NSEvent *event, BOOL *stop))trackingHandler NS_AVAILABLE_MAC(10_10);
-- (nullable NSEvent *)nextEventMatchingMask:(NSUInteger)mask;
-- (nullable NSEvent *)nextEventMatchingMask:(NSUInteger)mask untilDate:(nullable NSDate *)expiration inMode:(NSString *)mode dequeue:(BOOL)deqFlag;
-- (void)discardEventsMatchingMask:(NSUInteger)mask beforeEvent:(nullable NSEvent *)lastEvent;
-- (void)postEvent:(NSEvent *)event atStart:(BOOL)flag;
-@property (nullable, readonly, strong) NSEvent *currentEvent;
-@property BOOL acceptsMouseMovedEvents;
-@property BOOL ignoresMouseEvents;
 @property (readonly, copy) NSDictionary<NSString *, id> *deviceDescription;
-- (void)sendEvent:(NSEvent *)theEvent;
-@property (readonly) NSPoint mouseLocationOutsideOfEventStream;
 
 @property (nullable, assign) __kindof NSWindowController *windowController;
 
@@ -592,7 +593,7 @@
 @property (nullable, readonly, strong) NSWindow *sheetParent NS_AVAILABLE_MAC(10_9);
 
 
-+ (nullable NSButton *)standardWindowButton:(NSWindowButton)b forStyleMask:(NSUInteger)styleMask;
++ (nullable NSButton *)standardWindowButton:(NSWindowButton)b forStyleMask:(NSWindowStyleMask)styleMask;
 - (nullable NSButton *)standardWindowButton:(NSWindowButton)b;
 
 - (void)addChildWindow:(NSWindow *)childWin ordered:(NSWindowOrderingMode)place;
@@ -625,7 +626,7 @@
 @property (readonly) NSWindowOcclusionState occlusionState NS_AVAILABLE_MAC(10_9);
 
 
-/* NSViewController Support */
+#pragma mark - NSViewController Support
 
 /* The main content view controller for the window. This provides the contentView of the window. Assigning this value will remove the existing contentView and will make the contentViewController.view the main contentView for the window. The default value is nil. The contentViewController only controls the contentView, and not the title of the window. The window title can easily be bound to the contentViewController with the following: [window bind:NSTitleBinding toObject:contentViewController withKeyPath:@"title" options:nil]. Setting the contentViewController will cause the window to resize based on the current size of the contentViewController. Autolayout should be used to restrict the size of the window. The value of the contentViewController is encoded in the NIB. Directly assigning a contentView will clear out the rootViewController.
  */
@@ -635,80 +636,127 @@
  */
 + (instancetype)windowWithContentViewController:(NSViewController *)contentViewController NS_AVAILABLE_MAC(10_10);
 
+#pragma mark - Window Dragging
+
 /* Call to start a drag (moving the window) in the Window Server process. In general, this can be done after a mouseDown event has come in and been examined by an application or view. The view may determine it wants to allow that portion of the window to start a window drag, and can hand off the work to the Window Server process by calling this method. This allows the window to participate in space switching, and other system features. Pass the original mouseDown event to the method. The method will return right away, and a mouseUp may not get sent.
  */
 - (void)performWindowDragWithEvent:(NSEvent *)event NS_AVAILABLE_MAC(10_11);
 
-@end
+#pragma mark - Keyboard UI support (Key View Loop)
 
-@interface NSWindow(NSKeyboardUI)
 @property (nullable, assign) NSView *initialFirstResponder;
 - (void)selectNextKeyView:(nullable id)sender;
 - (void)selectPreviousKeyView:(nullable id)sender;
-- (void)selectKeyViewFollowingView:(NSView *)aView;
-- (void)selectKeyViewPrecedingView:(NSView *)aView;
+- (void)selectKeyViewFollowingView:(NSView *)view;
+- (void)selectKeyViewPrecedingView:(NSView *)view;
 @property (readonly) NSSelectionDirection keyViewSelectionDirection;
 @property (nullable, retain) NSButtonCell *defaultButtonCell;
 - (void)disableKeyEquivalentForDefaultButtonCell;
 - (void)enableKeyEquivalentForDefaultButtonCell;
 @property BOOL autorecalculatesKeyViewLoop;
 - (void)recalculateKeyViewLoop;
-@end
 
-@interface NSWindow (NSToolbarSupport)
+#pragma mark - Toolbar Support
+
 @property (nullable, strong) NSToolbar *toolbar;
 - (void)toggleToolbarShown:(nullable id)sender;
 - (void)runToolbarCustomizationPalette:(nullable id)sender;
-@property BOOL showsToolbarButton;
-@end
+@property BOOL showsToolbarButton; // Does nothing in recent versions of the OS
 
-@interface NSWindow(NSDrag)
-- (void)dragImage:(NSImage *)anImage at:(NSPoint)baseLocation offset:(NSSize)initialOffset event:(NSEvent *)event pasteboard:(NSPasteboard *)pboard source:(id)sourceObj slideBack:(BOOL)slideFlag;
+#pragma mark - Automatic Window Tabbing
 
-- (void)registerForDraggedTypes:(NSArray<NSString *> *)newTypes;
-- (void)unregisterDraggedTypes;
-@end
+/* Allows automatic window tabbing when the value is YES. By default, this will be set to YES, but applications can explicitly opt out of all automatic tabbing by setting it to NO, and can still adoped explicit window tabbing, if desired. 
+ */
+@property (class) BOOL allowsAutomaticWindowTabbing NS_AVAILABLE_MAC(10_12);
 
-@interface NSWindow(NSCarbonExtensions)
+/* Returns the user's tabbing preference as set in System Preferences. This value should be queried anytime a new window is made to see if the user wants to automatically show it in tabs.
+ */
+@property (class, readonly) NSWindowUserTabbingPreference userTabbingPreference NS_AVAILABLE_MAC(10_12);
 
-/* Create an NSWindow for a Carbon window - windowRef must be a Carbon WindowRef - see MacWindows.h. This method can only be called on NSWindow, and not subclasses of NSWindow. On 10.11, it will throw an exception if this is done.
+/* Get and set the tabbing mode for this window. This should be set before a window is shown. The default value is NSWindowTabbingModeAutomatic. When the value is NSWindowTabbingModeAutomatic, the system will look at the userTabbingPreference and automatically tab windows together based on the tabbingIdentifier, when it is appropriate to do so.
  */
-- (nullable NSWindow *)initWithWindowRef:(void * /* WindowRef */)windowRef;
+@property NSWindowTabbingMode tabbingMode NS_AVAILABLE_MAC(10_12);
 
-/* return the Carbon WindowRef for this window, creating if necessary: - see MacWindows.h
+/* Windows with the same tabbingIdentifier will have the ability to be tabbed together when a window is being shown. This allows aggregation of similiar windows. By default, the tabbingIdentifier will be generated based on inherit window properties, such as the window class name, the delegate class name, the window controller class name, and some additional state. Windows can be explicilty made to group together by using the same tabbingIdentifier. 
  */
-@property (readonly) void * /* WindowRef */windowRef NS_RETURNS_INNER_POINTER;
-@end
+@property (copy) NSString *tabbingIdentifier NS_AVAILABLE_MAC(10_12);
 
-@interface NSWindow(NSDeprecated)
+/* Actions that can be called to perform various tabbed window behaviors. UI that is hooked up to these items can be automatically validated by calling NSWindow's validateUserInterfaceItem.
+ */
+- (IBAction)selectNextTab:(nullable id)sender NS_AVAILABLE_MAC(10_12);
+- (IBAction)selectPreviousTab:(nullable id)sender NS_AVAILABLE_MAC(10_12);
+- (IBAction)moveTabToNewWindow:(nullable id)sender NS_AVAILABLE_MAC(10_12);
+- (IBAction)mergeAllWindows:(nullable id)sender NS_AVAILABLE_MAC(10_12);
+- (IBAction)toggleTabBar:(nullable id)sender NS_AVAILABLE_MAC(10_12);
 
-+ (void)menuChanged:(NSMenu *)menu NS_DEPRECATED_MAC(10_0, 10_11, "This method does not do anything and should not be called.");
+/* Returns the entire group (stack) of windows that are all visually shown together in one virtual tabbed window and associated with this particular window. Operations can then be done on each window, as necessary. For instance, iterating over each window in the group and calling performClose: will close the entire stack. The result will be nil when the window is not tabbed at all (not showing a tab bar), and non-nil with at least one object when the tab bar is shown. The order of items in the array is the same order as the tabs visually shown (leading to trailing).
+ */
+@property (readonly, copy, nullable) NSArray<NSWindow *> *tabbedWindows NS_AVAILABLE_MAC(10_12);
 
-/* gState is unused and should not be called.
+/* Allows creating a group of tabbed windows, or adding a new window to an existing tabbed window group. The 'window' will be added to the receiver's tabbed window group, or create a group if needed. The tabbingIdentifier for the entire group should be the same for all the windows, otherwise an exception will be thrown. Use the ordered parameter with "NSWindowAbove" and "NSWindowBelow" to place the new window before or after the receiver's tab. Passing "NSWindowOut" will thrown an exception. Currently this method is not animatable, but that may change in the future.
  */
-- (NSInteger)gState NS_DEPRECATED_MAC(10_0, 10_10);
+- (void)addTabbedWindow:(NSWindow *)window ordered:(NSWindowOrderingMode)ordered NS_AVAILABLE_MAC(10_12);
 
-/* The base/screen conversion methods are deprecated in 10.7 and later. Please use convertRectToScreen: or convertRectFromScreen: instead.  */
-- (NSPoint)convertBaseToScreen:(NSPoint)aPoint NS_DEPRECATED_MAC(10_0, 10_7, "Use -convertRectToScreen: instead");
-- (NSPoint)convertScreenToBase:(NSPoint)aPoint NS_DEPRECATED_MAC(10_0, 10_7, "Use -convertRectFromScreen: instead");
+#pragma mark - Other
 
-/* -setCanBeVisibleOnAllSpaces: controls whether a window can be visible on all spaces (YES) or is associated with one space at a time (NO).  The default setting is NO.
+/* Retrieve the layout direction of the window titlebar: this includes the standard window buttons (close/minimize/maximize buttons) and the title for this window. In general, this will return "right to left" (RTL) if the primary system language is RTL. The layout direction may be RTL even in applications that do not have a RTL language localization. This value should be utilized if an application uses titlebarAppearsTransparent and places controls underneath the titlebar.
  */
--(BOOL)canBeVisibleOnAllSpaces NS_DEPRECATED_MAC(10_5, 10_5);
--(void)setCanBeVisibleOnAllSpaces:(BOOL)flag NS_DEPRECATED_MAC(10_5, 10_5);
+@property (readonly) NSUserInterfaceLayoutDirection windowTitlebarLayoutDirection NS_AVAILABLE_MAC(10_12);
 
-/* This method is deprecated and should not be used by applications targeting Mac OS X 10.7 or later.
- The implementation of this method will always return 1.0.  Please use -convertRectToBacking: and -backingScaleFactor instead.
+#pragma mark -
+
+@end
+
+@interface NSWindow(NSEvent)
+/* Tracks events matching the supplied mask with the supplied tracking handler until the tracking handler explicitly terminates tracking. Each event is removed from the event queue then passed to the tracking handler. If a matching event does not exist in the event queue, then the main thread blocks in the specified runloop mode until an event of the requested type is received or the timeout expires. If the timeout expires, the tracking handler is called with a nil event. A negative timeout is interpreted as 0. Use NSEventDurationForever to never timeout. Tracking continues until *stop is set to YES. Calls to -nextEventMatchingMask:… are allowed inside the trackingHandler block. This method returns once tracking is terminated.
  */
-- (CGFloat)userSpaceScaleFactor NS_DEPRECATED_MAC(10_4, 10_7, "Use -convertRectToBacking: and -backingScaleFactor instead");
+- (void)trackEventsMatchingMask:(NSEventMask)mask timeout:(NSTimeInterval)timeout mode:(NSString *)mode handler:(void(^)(NSEvent *event, BOOL *stop))trackingHandler NS_AVAILABLE_MAC(10_10);
+#if __LP64__
+- (nullable NSEvent *)nextEventMatchingMask:(NSEventMask)mask;
+- (nullable NSEvent *)nextEventMatchingMask:(NSEventMask)mask untilDate:(nullable NSDate *)expiration inMode:(NSString *)mode dequeue:(BOOL)deqFlag;
+- (void)discardEventsMatchingMask:(NSEventMask)mask beforeEvent:(nullable NSEvent *)lastEvent;
+#else
+- (nullable NSEvent *)nextEventMatchingMask:(NSUInteger)mask;
+- (nullable NSEvent *)nextEventMatchingMask:(NSUInteger)mask untilDate:(nullable NSDate *)expiration inMode:(NSString *)mode dequeue:(BOOL)deqFlag;
+- (void)discardEventsMatchingMask:(NSUInteger)mask beforeEvent:(nullable NSEvent *)lastEvent;
+#endif
 
-- (void)useOptimizedDrawing:(BOOL)flag NS_DEPRECATED_MAC(10_0, 10_10);
+- (void)postEvent:(NSEvent *)event atStart:(BOOL)flag;
+- (void)sendEvent:(NSEvent *)event;
+@property (nullable, readonly, strong) NSEvent *currentEvent;
+@property BOOL acceptsMouseMovedEvents;
+@property BOOL ignoresMouseEvents;
+@property (readonly) NSPoint mouseLocationOutsideOfEventStream;
+@end
 
-/* canStoreColor has not been needed or used in a while and is deprecated. */
-- (BOOL)canStoreColor NS_DEPRECATED_MAC(10_0, 10_10);
+@interface NSWindow(NSCursorRect)
+- (void)disableCursorRects;
+- (void)enableCursorRects;
+- (void)discardCursorRects;
+@property (readonly) BOOL areCursorRectsEnabled;
+- (void)invalidateCursorRectsForView:(NSView *)view;
+- (void)resetCursorRects;
+@end
+
+@interface NSWindow(NSDrag)
+- (void)dragImage:(NSImage *)image at:(NSPoint)baseLocation offset:(NSSize)initialOffset event:(NSEvent *)event pasteboard:(NSPasteboard *)pboard source:(id)sourceObj slideBack:(BOOL)slideFlag;
 
+- (void)registerForDraggedTypes:(NSArray<NSString *> *)newTypes;
+- (void)unregisterDraggedTypes;
 @end
 
+@interface NSWindow(NSCarbonExtensions)
+
+/* Create an NSWindow for a Carbon window - windowRef must be a Carbon WindowRef - see MacWindows.h. This method can only be called on NSWindow, and not subclasses of NSWindow. On 10.11, it will throw an exception if this is done.
+ */
+- (nullable NSWindow *)initWithWindowRef:(void * /* WindowRef */)windowRef;
+
+/* return the Carbon WindowRef for this window, creating if necessary: - see MacWindows.h
+ */
+@property (readonly) void * /* WindowRef */windowRef NS_RETURNS_INNER_POINTER;
+@end
+
+
 @protocol NSWindowDelegate <NSObject>
 @optional
 - (BOOL)windowShouldClose:(id)sender;
@@ -862,5 +910,51 @@
     NSUnscaledWindowMask		= 1 << 11
 } NS_ENUM_DEPRECATED_MAC(10_0, 10_9);
 
+@interface NSWindow(NSDeprecated)
+
++ (void)menuChanged:(NSMenu *)menu NS_DEPRECATED_MAC(10_0, 10_11, "This method does not do anything and should not be called.");
+
+/* gState is unused and should not be called.
+ */
+- (NSInteger)gState NS_DEPRECATED_MAC(10_0, 10_10, "This method is unused and should not be called.");
+
+/* The base/screen conversion methods are deprecated in 10.7 and later. Please use convertRectToScreen: or convertRectFromScreen: instead.  */
+- (NSPoint)convertBaseToScreen:(NSPoint)point NS_DEPRECATED_MAC(10_0, 10_7, "Use -convertRectToScreen: instead");
+- (NSPoint)convertScreenToBase:(NSPoint)point NS_DEPRECATED_MAC(10_0, 10_7, "Use -convertRectFromScreen: instead");
+
+/* -setCanBeVisibleOnAllSpaces: controls whether a window can be visible on all spaces (YES) or is associated with one space at a time (NO).  The default setting is NO.
+ */
+-(BOOL)canBeVisibleOnAllSpaces NS_DEPRECATED_MAC(10_5, 10_5);
+-(void)setCanBeVisibleOnAllSpaces:(BOOL)flag NS_DEPRECATED_MAC(10_5, 10_5);
+
+/* This method is deprecated and should not be used by applications targeting Mac OS X 10.7 or later.
+ The implementation of this method will always return 1.0.  Please use -convertRectToBacking: and -backingScaleFactor instead.
+ */
+- (CGFloat)userSpaceScaleFactor NS_DEPRECATED_MAC(10_4, 10_7, "Use -convertRectToBacking: and -backingScaleFactor instead");
+
+- (void)useOptimizedDrawing:(BOOL)flag NS_DEPRECATED_MAC(10_0, 10_10, "This method does not do nothing");
+
+/* canStoreColor has not been needed or used in a while and is deprecated. */
+- (BOOL)canStoreColor NS_DEPRECATED_MAC(10_0, 10_10, "This method does not do anything");
+
+@end
+
+/* Deprecated legacy style mask constants. Prefer to use NSWindowStyleMask values instead.
+ */
+static const NSWindowStyleMask NSBorderlessWindowMask API_DEPRECATED_WITH_REPLACEMENT("NSWindowStyleMaskBorderless", macosx(10.0, 10.12)) = NSWindowStyleMaskBorderless;
+static const NSWindowStyleMask NSTitledWindowMask API_DEPRECATED_WITH_REPLACEMENT("NSWindowStyleMaskTitled", macosx(10.0, 10.12)) = NSWindowStyleMaskTitled;
+static const NSWindowStyleMask NSClosableWindowMask API_DEPRECATED_WITH_REPLACEMENT("NSWindowStyleMaskClosable", macosx(10.0, 10.12)) = NSWindowStyleMaskClosable;
+static const NSWindowStyleMask NSMiniaturizableWindowMask API_DEPRECATED_WITH_REPLACEMENT("NSWindowStyleMaskMiniaturizable", macosx(10.0, 10.12)) = NSWindowStyleMaskMiniaturizable;
+static const NSWindowStyleMask NSResizableWindowMask API_DEPRECATED_WITH_REPLACEMENT("NSWindowStyleMaskResizable", macosx(10.0, 10.12)) = NSWindowStyleMaskResizable;
+static const NSWindowStyleMask NSTexturedBackgroundWindowMask API_DEPRECATED_WITH_REPLACEMENT("NSWindowStyleMaskTexturedBackground", macosx(10.0, 10.12)) = NSWindowStyleMaskTexturedBackground;
+static const NSWindowStyleMask NSUnifiedTitleAndToolbarWindowMask API_DEPRECATED_WITH_REPLACEMENT("NSWindowStyleMaskUnifiedTitleAndToolbar", macosx(10.0, 10.12)) = NSWindowStyleMaskUnifiedTitleAndToolbar;
+static const NSWindowStyleMask NSFullScreenWindowMask API_DEPRECATED_WITH_REPLACEMENT("NSWindowStyleMaskFullScreen", macosx(10.0, 10.12)) = NSWindowStyleMaskFullScreen;
+static const NSWindowStyleMask NSFullSizeContentViewWindowMask API_DEPRECATED_WITH_REPLACEMENT("NSWindowStyleMaskFullSizeContentView", macosx(10.0, 10.12)) = NSWindowStyleMaskFullSizeContentView;
+static const NSWindowStyleMask NSUtilityWindowMask API_DEPRECATED_WITH_REPLACEMENT("NSWindowStyleMaskUtilityWindow", macosx(10.0, 10.12)) = NSWindowStyleMaskUtilityWindow;
+static const NSWindowStyleMask NSDocModalWindowMask API_DEPRECATED_WITH_REPLACEMENT("NSWindowStyleMaskDocModalWindow", macosx(10.0, 10.12)) = NSWindowStyleMaskDocModalWindow;
+static const NSWindowStyleMask NSNonactivatingPanelMask API_DEPRECATED_WITH_REPLACEMENT("NSWindowStyleMaskNonactivatingPanel", macosx(10.0, 10.12)) = NSWindowStyleMaskNonactivatingPanel;
+static const NSWindowStyleMask NSHUDWindowMask API_DEPRECATED_WITH_REPLACEMENT("NSWindowStyleMaskHUDWindow", macosx(10.0, 10.12)) = NSWindowStyleMaskHUDWindow;
+
+
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindowController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindowController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindowController.h	2015-08-26 04:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindowController.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSWindowController.h
     Application Kit
-    Copyright (c) 1997-2015, Apple Inc.
+    Copyright (c) 1997-2016, Apple Inc.
     All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindowRestoration.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindowRestoration.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindowRestoration.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindowRestoration.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSWindowRestoration.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
  */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindowScripting.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindowScripting.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindowScripting.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindowScripting.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
         NSWindowScripting.h
         AppKit Framework
-        Copyright (c) 1997-2015, Apple Inc.
+        Copyright (c) 1997-2016, Apple Inc.
         All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWorkspace.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWorkspace.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWorkspace.h	2015-08-26 04:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWorkspace.h	2016-06-03 05:13:45.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	NSWorkspace.h
 	Application Kit
-	Copyright (c) 1994-2015, Apple Inc.
+	Copyright (c) 1994-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -354,7 +354,7 @@
 - (nullable NSArray *)launchedApplications NS_DEPRECATED_MAC(10_0, 10_7, "Use -[NSWorkspace runningApplications] instead.");
 
 /* Open a file with an animation.  This currently does the same thing as openFile: and its use is discouraged. */
-- (BOOL)openFile:(NSString *)fullPath fromImage:(nullable NSImage *)anImage at:(NSPoint)point inView:(nullable NSView *)aView NS_DEPRECATED_MAC(10_0, 10_11, "Use -[NSWorkspace openURL:] instead.");
+- (BOOL)openFile:(NSString *)fullPath fromImage:(nullable NSImage *)image at:(NSPoint)point inView:(nullable NSView *)view NS_DEPRECATED_MAC(10_0, 10_11, "Use -[NSWorkspace openURL:] instead.");
 
 
 /* Performs the given file operation, blocking until complete.  source should be the directory containing the file(s).  For operations that require a destination, such as Move and Copy, destination should be the destination directory; otherwise it should be nil.  files is an array of file names that are in the source directory.

```