#AppKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitLegacySwiftCompatibility.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitLegacySwiftCompatibility.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitLegacySwiftCompatibility.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitLegacySwiftCompatibility.h	2016-07-27 05:10:07.000000000 +0200
@@ -11,7 +11,8 @@
 #import <AppKit/NSOpenGL.h>
 #import <AppKit/NSColor.h>
 #import <AppKit/NSColorSpace.h>
-
+#import <AppKit/NSAppearance.h>
+#import <AppKit/NSWindow.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -114,5 +115,21 @@
 @end
 #endif
 
+#if !NS_APPEARANCE_DECLARES_DESIGNATED_INITIALIZERS
+
+@interface NSAppearance ()
+
+- (nullable instancetype)initWithAppearanceNamed:(NSString *)name bundle:(nullable NSBundle *)bundle;
+
+@end
+
+#endif
+
+#if !NSWINDOW_TRACK_EVENTS_DECLARES_NULLABILITY
+@interface NSWindow ()
+- (void)trackEventsMatchingMask:(NSEventMask)mask timeout:(NSTimeInterval)timeout mode:(NSRunLoopMode)mode handler:(void(^)(NSEvent *event, BOOL *stop))trackingHandler NS_AVAILABLE_MAC(10_10);
+@end
+#endif
+
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibility.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibility.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibility.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibility.h	2016-07-27 05:10:07.000000000 +0200
@@ -104,7 +104,7 @@
 @end
 
 /* Notification posted to the NSWorkspace notification center when any accessibility display options have changed. */
-APPKIT_EXTERN NSString * const NSWorkspaceAccessibilityDisplayOptionsDidChangeNotification NS_AVAILABLE_MAC(10_10);
+APPKIT_EXTERN NSNotificationName const NSWorkspaceAccessibilityDisplayOptionsDidChangeNotification NS_AVAILABLE_MAC(10_10);
 
 
 /*** Accessibility Related Methods ***/
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibilityConstants.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibilityConstants.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibilityConstants.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAccessibilityConstants.h	2016-07-27 05:10:07.000000000 +0200
@@ -12,7 +12,7 @@
 /*** Exception Constants ***/
 
 // name for accessibility exception - declared in NSErrors.h
-// APPKIT_EXTERN NSString *NSAccessibilityException;
+// APPKIT_EXTERN NSExceptionName NSAccessibilityException;
 
 /* userInfo key for error codes in accessibility exceptions
  */
@@ -511,7 +511,6 @@
 APPKIT_EXTERN NSString *const NSAccessibilityDescriptionListSubrole		NS_AVAILABLE_MAC(10_9);
 
 
-
 /* This function allows an accessibility notification to be posted with a user info dictionary.  The user info dictionary can be nil.  Valid contents of the user info dictionary are limited to classes which can be returned to an accessibility client.  That list currently includes NSString, NSNumber, NSArray, NSValues of points, ranges, sizes, rects, and valid NSAccessibility objects.  Most accessibility notifications do not require a user info dictionary.
  */
 APPKIT_EXTERN void NSAccessibilityPostNotificationWithUserInfo(id element, NSString *notification, NSDictionary *userInfo) NS_AVAILABLE_MAC(10_7);
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAnimation.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAnimation.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAnimation.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAnimation.h	2016-07-27 05:10:07.000000000 +0200
@@ -28,7 +28,7 @@
 
 typedef float NSAnimationProgress;
 
-APPKIT_EXTERN NSString * NSAnimationProgressMarkNotification; // has single entry in user info dictionary
+APPKIT_EXTERN NSNotificationName NSAnimationProgressMarkNotification; // has single entry in user info dictionary
 APPKIT_EXTERN NSString * NSAnimationProgressMark; // NSNumber(float) with NSAnimationProgress
 
 @interface NSAnimation : NSObject <NSCopying, NSCoding> {
@@ -100,7 +100,7 @@
 - (void)clearStartAnimation;
 - (void)clearStopAnimation;
 
-@property (nullable, readonly, copy) NSArray<NSString *> *runLoopModesForAnimating;
+@property (nullable, readonly, copy) NSArray<NSRunLoopMode> *runLoopModesForAnimating;
 
 @end
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAppearance.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAppearance.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAppearance.h	2016-07-11 05:26:55.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSAppearance.h	2016-07-27 05:10:07.000000000 +0200
@@ -8,6 +8,8 @@
 #import <AppKit/AppKitDefines.h>
 #import <Foundation/NSObject.h>
 
+#define NS_APPEARANCE_DECLARES_DESIGNATED_INITIALIZERS APPKIT_SWIFT_SDK_EPOCH_AT_LEAST(2)
+
 NS_ASSUME_NONNULL_BEGIN
 
 @class NSString, NSBundle;
@@ -40,7 +42,10 @@
 /* Creates an NSAppearance by searching the specified bundle for a file with the specified name (without path extension).
     If bundle is nil, the main bundle is assumed.
  */
-- (nullable instancetype)initWithAppearanceNamed:(NSString *)name bundle:(nullable NSBundle *)bundle;
+#if NS_APPEARANCE_DECLARES_DESIGNATED_INITIALIZERS
+- (nullable instancetype)initWithAppearanceNamed:(NSString *)name bundle:(nullable NSBundle *)bundle NS_DESIGNATED_INITIALIZER;
+- (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
+#endif
 
 /* Query allowsVibrancy to see if the given appearance actually needs vibrant drawing. You may want to draw differently if the current apperance is vibrant.
  */
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSApplication.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSApplication.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSApplication.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSApplication.h	2016-07-27 05:10:07.000000000 +0200
@@ -63,8 +63,8 @@
 
 
 /* Modes passed to NSRunLoop */
-APPKIT_EXTERN NSString *NSModalPanelRunLoopMode;
-APPKIT_EXTERN NSString *NSEventTrackingRunLoopMode;
+APPKIT_EXTERN NSRunLoopMode NSModalPanelRunLoopMode;
+APPKIT_EXTERN NSRunLoopMode NSEventTrackingRunLoopMode;
 
 
 /* Pre-defined return values for -runModalFor: and -runModalSession:. The system also reserves all values below these. Other values can be used. */
@@ -277,10 +277,10 @@
 - (void)postEvent:(NSEvent *)event atStart:(BOOL)flag;
 @property (nullable, readonly, strong) NSEvent *currentEvent;
 #if __LP64__
-- (nullable NSEvent *)nextEventMatchingMask:(NSEventMask)mask untilDate:(nullable NSDate *)expiration inMode:(NSString *)mode dequeue:(BOOL)deqFlag;
+- (nullable NSEvent *)nextEventMatchingMask:(NSEventMask)mask untilDate:(nullable NSDate *)expiration inMode:(NSRunLoopMode)mode dequeue:(BOOL)deqFlag;
 - (void)discardEventsMatchingMask:(NSEventMask)mask beforeEvent:(nullable NSEvent *)lastEvent;
 #else
-- (nullable NSEvent *)nextEventMatchingMask:(NSUInteger)mask untilDate:(nullable NSDate *)expiration inMode:(NSString *)mode dequeue:(BOOL)deqFlag;
+- (nullable NSEvent *)nextEventMatchingMask:(NSUInteger)mask untilDate:(nullable NSDate *)expiration inMode:(NSRunLoopMode)mode dequeue:(BOOL)deqFlag;
 - (void)discardEventsMatchingMask:(NSUInteger)mask beforeEvent:(nullable NSEvent *)lastEvent;
 #endif
 @end
@@ -516,20 +516,20 @@
 APPKIT_EXTERN void NSUnregisterServicesProvider(NSString *name);
 
 /* Notifications */
-APPKIT_EXTERN NSString *NSApplicationDidBecomeActiveNotification;
-APPKIT_EXTERN NSString *NSApplicationDidHideNotification;
-APPKIT_EXTERN NSString *NSApplicationDidFinishLaunchingNotification;
-APPKIT_EXTERN NSString *NSApplicationDidResignActiveNotification;
-APPKIT_EXTERN NSString *NSApplicationDidUnhideNotification;
-APPKIT_EXTERN NSString *NSApplicationDidUpdateNotification;
-APPKIT_EXTERN NSString *NSApplicationWillBecomeActiveNotification;
-APPKIT_EXTERN NSString *NSApplicationWillHideNotification;
-APPKIT_EXTERN NSString *NSApplicationWillFinishLaunchingNotification;
-APPKIT_EXTERN NSString *NSApplicationWillResignActiveNotification;
-APPKIT_EXTERN NSString *NSApplicationWillUnhideNotification;
-APPKIT_EXTERN NSString *NSApplicationWillUpdateNotification;
-APPKIT_EXTERN NSString *NSApplicationWillTerminateNotification;
-APPKIT_EXTERN NSString *NSApplicationDidChangeScreenParametersNotification;
+APPKIT_EXTERN NSNotificationName NSApplicationDidBecomeActiveNotification;
+APPKIT_EXTERN NSNotificationName NSApplicationDidHideNotification;
+APPKIT_EXTERN NSNotificationName NSApplicationDidFinishLaunchingNotification;
+APPKIT_EXTERN NSNotificationName NSApplicationDidResignActiveNotification;
+APPKIT_EXTERN NSNotificationName NSApplicationDidUnhideNotification;
+APPKIT_EXTERN NSNotificationName NSApplicationDidUpdateNotification;
+APPKIT_EXTERN NSNotificationName NSApplicationWillBecomeActiveNotification;
+APPKIT_EXTERN NSNotificationName NSApplicationWillHideNotification;
+APPKIT_EXTERN NSNotificationName NSApplicationWillFinishLaunchingNotification;
+APPKIT_EXTERN NSNotificationName NSApplicationWillResignActiveNotification;
+APPKIT_EXTERN NSNotificationName NSApplicationWillUnhideNotification;
+APPKIT_EXTERN NSNotificationName NSApplicationWillUpdateNotification;
+APPKIT_EXTERN NSNotificationName NSApplicationWillTerminateNotification;
+APPKIT_EXTERN NSNotificationName NSApplicationDidChangeScreenParametersNotification;
 
 /* User info keys for NSApplicationDidFinishLaunchingNotification */
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBrowser.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBrowser.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBrowser.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSBrowser.h	2016-07-27 05:10:07.000000000 +0200
@@ -340,7 +340,7 @@
 
 /* The -object in the NSNotification is the browser whose column sizes need to be persisted. There is no userInfo.
  */
-APPKIT_EXTERN NSString * NSBrowserColumnConfigurationDidChangeNotification;
+APPKIT_EXTERN NSNotificationName NSBrowserColumnConfigurationDidChangeNotification;
 
 #pragma mark -
 #pragma mark **** Delegate methods ****
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCell.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCell.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCell.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCell.h	2016-07-27 05:10:07.000000000 +0200
@@ -311,7 +311,7 @@
 - (void)setNextState;			/* toggle/cycle through states */
 @end
 
-APPKIT_EXTERN NSString * NSControlTintDidChangeNotification; /* sent after user changes control tint preference */
+APPKIT_EXTERN NSNotificationName NSControlTintDidChangeNotification; /* sent after user changes control tint preference */
 
 /* Cell Hit testing support */
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionView.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionView.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionView.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionView.h	2016-07-27 05:10:07.000000000 +0200
@@ -224,7 +224,7 @@
 
 /* An optional, non-retained delegate object, that will have the opportunity to influence the CollectionView's drag-and-drop, selection, highlighting, and layout transitioning behaviors.  See the NSCollectionViewDelegate protocol, declared below, for the methods this delegate may implement.  Defaults to nil, which leaves the CollectionView to determine its own behaviors.
 */
-@property (nullable, assign) id<NSCollectionViewDelegate> delegate;
+@property (nullable, weak) id<NSCollectionViewDelegate> delegate;
 
 
 #pragma mark *** Decoration ***
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColor.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColor.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColor.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColor.h	2016-07-27 05:10:07.000000000 +0200
@@ -318,6 +318,6 @@
 
 @end
 
-APPKIT_EXTERN NSString * NSSystemColorsDidChangeNotification;
+APPKIT_EXTERN NSNotificationName NSSystemColorsDidChangeNotification;
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorList.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorList.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorList.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorList.h	2016-07-27 05:10:07.000000000 +0200
@@ -14,6 +14,7 @@
 
 #import <Foundation/NSObject.h>
 #import <Foundation/NSArray.h>
+#import <Foundation/NSNotification.h>
 #import <AppKit/AppKitDefines.h>
 #import <CoreFoundation/CFDictionary.h>
 
@@ -87,18 +88,24 @@
 */
 @property (getter=isEditable, readonly) BOOL editable;
 
-/* Use "nil" to save to the user's private colorlists directory. If the color list is named, this method will also insert the color list into availableColorLists.
+/* Save the color list using secure keyed archive format. Specify nil to save to the user's private colorlists directory (and also update availableColorLists), using the name of the color list.
+ */
+- (BOOL)writeToURL:(nullable NSURL *)url error:(NSError **)errPtr NS_AVAILABLE_MAC(10_11);
+
+/* Save the color list using unkeyed archive format. Specify nil to save to the user's private colorlists directory (and also update availableColorLists), using the name of the color list.
+ 
+   Use of the unkeyed archive format (and hence this API) is discouraged since it cannot represent some colors (including custom colorspace based ones) without loss. Use writeToURL:error: instead.
 */
 - (BOOL)writeToFile:(nullable NSString *)path;	
 
-/* If the color list is in the user's path, removes the corresponding file in user's private colorlists directory. Also removes the color list from availableColorLists. If there are no outstanding references to the color list this might deallocate the object as well.
+/* If the color list is in the user's private colorlists directory, removes the corresponding file and the color list from availableColorLists. If there are no outstanding references to the color list this might deallocate the object as well.
 */
 - (void)removeFile;
 
 @end
 
 /* Notifications */
-APPKIT_EXTERN NSString * NSColorListDidChangeNotification;
+APPKIT_EXTERN NSNotificationName NSColorListDidChangeNotification;
 
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorPanel.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorPanel.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorPanel.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorPanel.h	2016-07-27 05:10:07.000000000 +0200
@@ -105,7 +105,7 @@
 @end
 
 /* Notifications */
-APPKIT_EXTERN NSString * NSColorPanelColorDidChangeNotification;
+APPKIT_EXTERN NSNotificationName NSColorPanelColorDidChangeNotification;
 
 
 static const NSColorPanelMode NSNoModeColorPanel NS_AVAILABLE_MAC(10_5) /*API_DEPRECATED_WITH_REPLACEMENT("NSColorPanelModeNone", macosx(10.5, 10.12))*/ = NSColorPanelModeNone;
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSComboBox.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSComboBox.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSComboBox.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSComboBox.h	2016-07-27 05:10:07.000000000 +0200
@@ -10,10 +10,10 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-APPKIT_EXTERN NSString * NSComboBoxWillPopUpNotification;
-APPKIT_EXTERN NSString * NSComboBoxWillDismissNotification;
-APPKIT_EXTERN NSString * NSComboBoxSelectionDidChangeNotification;
-APPKIT_EXTERN NSString * NSComboBoxSelectionIsChangingNotification;
+APPKIT_EXTERN NSNotificationName NSComboBoxWillPopUpNotification;
+APPKIT_EXTERN NSNotificationName NSComboBoxWillDismissNotification;
+APPKIT_EXTERN NSNotificationName NSComboBoxSelectionDidChangeNotification;
+APPKIT_EXTERN NSNotificationName NSComboBoxSelectionIsChangingNotification;
 
 @class NSComboBox;
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSControl.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSControl.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSControl.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSControl.h	2016-07-27 05:10:07.000000000 +0200
@@ -144,9 +144,9 @@
 @end
 
                                                                     // userInfo keys:
-APPKIT_EXTERN NSString * NSControlTextDidBeginEditingNotification;	//	@"NSFieldEditor"
-APPKIT_EXTERN NSString * NSControlTextDidEndEditingNotification;	//	@"NSFieldEditor"
-APPKIT_EXTERN NSString * NSControlTextDidChangeNotification;		//	@"NSFieldEditor"
+APPKIT_EXTERN NSNotificationName NSControlTextDidBeginEditingNotification;	//	@"NSFieldEditor"
+APPKIT_EXTERN NSNotificationName NSControlTextDidEndEditingNotification;	//	@"NSFieldEditor"
+APPKIT_EXTERN NSNotificationName NSControlTextDidChangeNotification;		//	@"NSFieldEditor"
 
 
 @interface NSControl (NSDeprecated)
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDrawer.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDrawer.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDrawer.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDrawer.h	2016-07-27 05:10:07.000000000 +0200
@@ -103,10 +103,10 @@
 @end
 
 /* Notifications */
-APPKIT_EXTERN NSString * NSDrawerWillOpenNotification;
-APPKIT_EXTERN NSString * NSDrawerDidOpenNotification;
-APPKIT_EXTERN NSString * NSDrawerWillCloseNotification;
-APPKIT_EXTERN NSString * NSDrawerDidCloseNotification;
+APPKIT_EXTERN NSNotificationName NSDrawerWillOpenNotification;
+APPKIT_EXTERN NSNotificationName NSDrawerDidOpenNotification;
+APPKIT_EXTERN NSNotificationName NSDrawerWillCloseNotification;
+APPKIT_EXTERN NSNotificationName NSDrawerDidCloseNotification;
 
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSErrors.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSErrors.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSErrors.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSErrors.h	2016-07-27 05:10:07.000000000 +0200
@@ -13,41 +13,41 @@
 
 // The following strings are the names of exceptions the AppKit can raise
 
-APPKIT_EXTERN NSString *NSTextLineTooLongException;
-APPKIT_EXTERN NSString *NSTextNoSelectionException;
-APPKIT_EXTERN NSString *NSWordTablesWriteException;
-APPKIT_EXTERN NSString *NSWordTablesReadException;
-APPKIT_EXTERN NSString *NSTextReadException;
-APPKIT_EXTERN NSString *NSTextWriteException;
-APPKIT_EXTERN NSString *NSPasteboardCommunicationException;
-APPKIT_EXTERN NSString *NSPrintingCommunicationException;
-APPKIT_EXTERN NSString *NSAbortModalException;
-APPKIT_EXTERN NSString *NSAbortPrintingException;
-APPKIT_EXTERN NSString *NSIllegalSelectorException;
-APPKIT_EXTERN NSString *NSAppKitVirtualMemoryException;
-APPKIT_EXTERN NSString *NSBadRTFDirectiveException;
-APPKIT_EXTERN NSString *NSBadRTFFontTableException;
-APPKIT_EXTERN NSString *NSBadRTFStyleSheetException;
-APPKIT_EXTERN NSString *NSTypedStreamVersionException;
-APPKIT_EXTERN NSString *NSTIFFException;
-APPKIT_EXTERN NSString *NSPrintPackageException;
-APPKIT_EXTERN NSString *NSBadRTFColorTableException;
-APPKIT_EXTERN NSString *NSDraggingException;
-APPKIT_EXTERN NSString *NSColorListIOException;
-APPKIT_EXTERN NSString *NSColorListNotEditableException;
-APPKIT_EXTERN NSString *NSBadBitmapParametersException;
-APPKIT_EXTERN NSString *NSWindowServerCommunicationException;
-APPKIT_EXTERN NSString *NSFontUnavailableException;
-APPKIT_EXTERN NSString *NSPPDIncludeNotFoundException;
-APPKIT_EXTERN NSString *NSPPDParseException;
-APPKIT_EXTERN NSString *NSPPDIncludeStackOverflowException;
-APPKIT_EXTERN NSString *NSPPDIncludeStackUnderflowException;
-APPKIT_EXTERN NSString *NSRTFPropertyStackOverflowException;
-APPKIT_EXTERN NSString *NSAppKitIgnoredException;
-APPKIT_EXTERN NSString *NSBadComparisonException;
-APPKIT_EXTERN NSString *NSImageCacheException;
-APPKIT_EXTERN NSString *NSNibLoadingException;
-APPKIT_EXTERN NSString *NSBrowserIllegalDelegateException;
-APPKIT_EXTERN NSString *NSAccessibilityException NS_DEPRECATED_MAC(10_1, 10_11, "Exceptions are no longer appropriate for indicating errors in accessibility API. Unexpected values should be handled through appropriate type checking.");
+APPKIT_EXTERN NSExceptionName NSTextLineTooLongException;
+APPKIT_EXTERN NSExceptionName NSTextNoSelectionException;
+APPKIT_EXTERN NSExceptionName NSWordTablesWriteException;
+APPKIT_EXTERN NSExceptionName NSWordTablesReadException;
+APPKIT_EXTERN NSExceptionName NSTextReadException;
+APPKIT_EXTERN NSExceptionName NSTextWriteException;
+APPKIT_EXTERN NSExceptionName NSPasteboardCommunicationException;
+APPKIT_EXTERN NSExceptionName NSPrintingCommunicationException;
+APPKIT_EXTERN NSExceptionName NSAbortModalException;
+APPKIT_EXTERN NSExceptionName NSAbortPrintingException;
+APPKIT_EXTERN NSExceptionName NSIllegalSelectorException;
+APPKIT_EXTERN NSExceptionName NSAppKitVirtualMemoryException;
+APPKIT_EXTERN NSExceptionName NSBadRTFDirectiveException;
+APPKIT_EXTERN NSExceptionName NSBadRTFFontTableException;
+APPKIT_EXTERN NSExceptionName NSBadRTFStyleSheetException;
+APPKIT_EXTERN NSExceptionName NSTypedStreamVersionException;
+APPKIT_EXTERN NSExceptionName NSTIFFException;
+APPKIT_EXTERN NSExceptionName NSPrintPackageException;
+APPKIT_EXTERN NSExceptionName NSBadRTFColorTableException;
+APPKIT_EXTERN NSExceptionName NSDraggingException;
+APPKIT_EXTERN NSExceptionName NSColorListIOException;
+APPKIT_EXTERN NSExceptionName NSColorListNotEditableException;
+APPKIT_EXTERN NSExceptionName NSBadBitmapParametersException;
+APPKIT_EXTERN NSExceptionName NSWindowServerCommunicationException;
+APPKIT_EXTERN NSExceptionName NSFontUnavailableException;
+APPKIT_EXTERN NSExceptionName NSPPDIncludeNotFoundException;
+APPKIT_EXTERN NSExceptionName NSPPDParseException;
+APPKIT_EXTERN NSExceptionName NSPPDIncludeStackOverflowException;
+APPKIT_EXTERN NSExceptionName NSPPDIncludeStackUnderflowException;
+APPKIT_EXTERN NSExceptionName NSRTFPropertyStackOverflowException;
+APPKIT_EXTERN NSExceptionName NSAppKitIgnoredException;
+APPKIT_EXTERN NSExceptionName NSBadComparisonException;
+APPKIT_EXTERN NSExceptionName NSImageCacheException;
+APPKIT_EXTERN NSExceptionName NSNibLoadingException;
+APPKIT_EXTERN NSExceptionName NSBrowserIllegalDelegateException;
+APPKIT_EXTERN NSExceptionName NSAccessibilityException NS_DEPRECATED_MAC(10_1, 10_11, "Exceptions are no longer appropriate for indicating errors in accessibility API. Unexpected values should be handled through appropriate type checking.");
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFont.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFont.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFont.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFont.h	2016-07-27 05:10:07.000000000 +0200
@@ -57,7 +57,8 @@
         unsigned int _matrixIsIdentity:1;
         unsigned int _renderingMode:3;
         unsigned int _inInstanceCache:1;
-        unsigned int _reserved2:14;
+        unsigned int _appearanceSize:1;
+        unsigned int _reserved2:13;
     } _fFlags;
     id _private;
 }
@@ -175,11 +176,11 @@
 /********* Notifications *********/
 /* This notification is posted when the antialias threshold is changed by the user.
 */
-APPKIT_EXTERN NSString * NSAntialiasThresholdChangedNotification;
+APPKIT_EXTERN NSNotificationName NSAntialiasThresholdChangedNotification;
 
 /* This notification is posted when the available font set is modified as a result of activation/deactivation.
 */
-APPKIT_EXTERN NSString * NSFontSetChangedNotification;
+APPKIT_EXTERN NSNotificationName NSFontSetChangedNotification;
 
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFontCollection.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFontCollection.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFontCollection.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFontCollection.h	2016-07-27 05:10:07.000000000 +0200
@@ -153,7 +153,7 @@
  This notification is sent to the local notification center when a named, persistent collection is modified.
  User info key NSFontCollectionNotificationAction describes the nature of the change.
  */
-APPKIT_EXTERN NSString * const NSFontCollectionDidChangeNotification NS_AVAILABLE_MAC(10_7);
+APPKIT_EXTERN NSNotificationName const NSFontCollectionDidChangeNotification NS_AVAILABLE_MAC(10_7);
 
 // Notification user info dictionary keys
 APPKIT_EXTERN NSString * const NSFontCollectionActionKey NS_AVAILABLE_MAC(10_7);			// NSString: action taken
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSHelpManager.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSHelpManager.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSHelpManager.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSHelpManager.h	2016-07-27 05:10:07.000000000 +0200
@@ -50,8 +50,8 @@
 // Notifications for the activation/deactivation of the context help mode
 //
 
-APPKIT_EXTERN NSString * NSContextHelpModeDidActivateNotification;
-APPKIT_EXTERN NSString * NSContextHelpModeDidDeactivateNotification;
+APPKIT_EXTERN NSNotificationName NSContextHelpModeDidActivateNotification;
+APPKIT_EXTERN NSNotificationName NSContextHelpModeDidDeactivateNotification;
 
 //
 //  Conveniences for accessing Help.plist
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImageRep.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImageRep.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImageRep.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImageRep.h	2016-07-27 05:10:07.000000000 +0200
@@ -9,6 +9,7 @@
 #import <Foundation/NSArray.h>
 #import <Foundation/NSDictionary.h>
 #import <Foundation/NSGeometry.h>
+#import <Foundation/NSNotification.h>
 #import <AppKit/AppKitDefines.h>
 #import <AppKit/NSGraphics.h>
 #import <AppKit/NSColorSpace.h>
@@ -138,7 +139,7 @@
 
 /* Notifications */
 #define NSImageRepRegistryChangedNotification NSImageRepRegistryDidChangeNotification /* obsolete name */
-APPKIT_EXTERN NSString *NSImageRepRegistryDidChangeNotification;
+APPKIT_EXTERN NSNotificationName NSImageRepRegistryDidChangeNotification;
 
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenu.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenu.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenu.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenu.h	2016-07-27 05:10:07.000000000 +0200
@@ -239,16 +239,16 @@
 @property (readonly) NSMenuProperties propertiesToUpdate NS_AVAILABLE_MAC(10_6);
 @end
 
-APPKIT_EXTERN NSString *NSMenuWillSendActionNotification;
-APPKIT_EXTERN NSString *NSMenuDidSendActionNotification;
+APPKIT_EXTERN NSNotificationName NSMenuWillSendActionNotification;
+APPKIT_EXTERN NSNotificationName NSMenuDidSendActionNotification;
 
-APPKIT_EXTERN NSString *NSMenuDidAddItemNotification;
-APPKIT_EXTERN NSString *NSMenuDidRemoveItemNotification;
-APPKIT_EXTERN NSString *NSMenuDidChangeItemNotification;
+APPKIT_EXTERN NSNotificationName NSMenuDidAddItemNotification;
+APPKIT_EXTERN NSNotificationName NSMenuDidRemoveItemNotification;
+APPKIT_EXTERN NSNotificationName NSMenuDidChangeItemNotification;
 // All three of these have a user info key NSMenuItemIndex with a NSNumber value.
 
-APPKIT_EXTERN NSString *NSMenuDidBeginTrackingNotification;
-APPKIT_EXTERN NSString *NSMenuDidEndTrackingNotification;
+APPKIT_EXTERN NSNotificationName NSMenuDidBeginTrackingNotification;
+APPKIT_EXTERN NSNotificationName NSMenuDidEndTrackingNotification;
 
 // The remainder of this file contains deprecated methods
 @interface NSMenu (NSDeprecated)
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOutlineView.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOutlineView.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOutlineView.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOutlineView.h	2016-07-27 05:10:07.000000000 +0200
@@ -482,19 +482,19 @@
 
 /* Notifications
 */
-APPKIT_EXTERN NSString * NSOutlineViewSelectionDidChangeNotification;
-APPKIT_EXTERN NSString * NSOutlineViewColumnDidMoveNotification;                                // @"NSOldColumn", @"NSNewColumn"
-APPKIT_EXTERN NSString * NSOutlineViewColumnDidResizeNotification;                // @"NSTableColumn", @"NSOldWidth"
-APPKIT_EXTERN NSString * NSOutlineViewSelectionIsChangingNotification;
+APPKIT_EXTERN NSNotificationName NSOutlineViewSelectionDidChangeNotification;
+APPKIT_EXTERN NSNotificationName NSOutlineViewColumnDidMoveNotification;                                // @"NSOldColumn", @"NSNewColumn"
+APPKIT_EXTERN NSNotificationName NSOutlineViewColumnDidResizeNotification;                // @"NSTableColumn", @"NSOldWidth"
+APPKIT_EXTERN NSNotificationName NSOutlineViewSelectionIsChangingNotification;
 
 
 /* Note for the following NSOutlineViewItem*Notifications:
    The 'userInfo' dictionary in the notification will have an @"NSObject" key where the value is the changed (id)item.
 */
-APPKIT_EXTERN NSString * NSOutlineViewItemWillExpandNotification;
-APPKIT_EXTERN NSString * NSOutlineViewItemDidExpandNotification;
-APPKIT_EXTERN NSString * NSOutlineViewItemWillCollapseNotification;
-APPKIT_EXTERN NSString * NSOutlineViewItemDidCollapseNotification;
+APPKIT_EXTERN NSNotificationName NSOutlineViewItemWillExpandNotification;
+APPKIT_EXTERN NSNotificationName NSOutlineViewItemDidExpandNotification;
+APPKIT_EXTERN NSNotificationName NSOutlineViewItemWillCollapseNotification;
+APPKIT_EXTERN NSNotificationName NSOutlineViewItemDidCollapseNotification;
 
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopUpButton.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopUpButton.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopUpButton.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopUpButton.h	2016-07-27 05:10:07.000000000 +0200
@@ -84,6 +84,6 @@
 @end
 
 /* Notifications */
-APPKIT_EXTERN NSString * NSPopUpButtonWillPopUpNotification;
+APPKIT_EXTERN NSNotificationName NSPopUpButtonWillPopUpNotification;
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopUpButtonCell.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopUpButtonCell.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopUpButtonCell.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopUpButtonCell.h	2016-07-27 05:10:07.000000000 +0200
@@ -116,6 +116,6 @@
 
 
 /* Notifications */
-APPKIT_EXTERN NSString * NSPopUpButtonCellWillPopUpNotification;
+APPKIT_EXTERN NSNotificationName NSPopUpButtonCellWillPopUpNotification;
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopover.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopover.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopover.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopover.h	2016-07-27 05:10:07.000000000 +0200
@@ -59,7 +59,7 @@
 #endif
 @private
     id _bindingAdaptor;
-    id <NSPopoverDelegate> _delegate;
+    id _delegate;
     id _visualRepresentation;
     NSView *_positioningView;
     NSViewController *_contentViewController;
@@ -117,7 +117,7 @@
 
 /*  The delegate of the popover. The delegate is not retained. 
  */
-@property(nullable, assign) IBOutlet id <NSPopoverDelegate> delegate;
+@property(nullable, weak) IBOutlet id <NSPopoverDelegate> delegate;
 
 #if MAC_OS_X_VERSION_MIN_REQUIRED >= MAC_OS_X_VERSION_10_10
 
@@ -205,19 +205,19 @@
 
 /*  Sent before the popover is shown. 
  */
-APPKIT_EXTERN NSString * const NSPopoverWillShowNotification NS_AVAILABLE_MAC(10_7);
+APPKIT_EXTERN NSNotificationName const NSPopoverWillShowNotification NS_AVAILABLE_MAC(10_7);
 
 /*  Sent after the popover has finished animating onscreen. 
  */
-APPKIT_EXTERN NSString * const NSPopoverDidShowNotification NS_AVAILABLE_MAC(10_7);
+APPKIT_EXTERN NSNotificationName const NSPopoverDidShowNotification NS_AVAILABLE_MAC(10_7);
 
 /*  Sent before the popover is closed. The userInfo key NSPopoverCloseReasonKey specifies the reason for closing.  It can currently be either NSPopoverCloseReasonStandard or NSPopoverCloseReasonDetachToWindow, although more reasons for closing may be added in the future. 
  */
-APPKIT_EXTERN NSString * const NSPopoverWillCloseNotification NS_AVAILABLE_MAC(10_7);
+APPKIT_EXTERN NSNotificationName const NSPopoverWillCloseNotification NS_AVAILABLE_MAC(10_7);
 
 /*  Sent after the popover has finished animating offscreen.  This notification has the same user info keys as NSPopoverWillCloseNotification. 
  */
-APPKIT_EXTERN NSString * const NSPopoverDidCloseNotification NS_AVAILABLE_MAC(10_7);
+APPKIT_EXTERN NSNotificationName const NSPopoverDidCloseNotification NS_AVAILABLE_MAC(10_7);
 
 #pragma mark -
 #pragma mark Delegate Methods
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPrintOperation.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPrintOperation.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPrintOperation.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPrintOperation.h	2016-07-27 05:10:07.000000000 +0200
@@ -35,7 +35,7 @@
 
 /* An exception that may be thrown by the factory methods described below.
 */
-APPKIT_EXTERN NSString * NSPrintOperationExistsException;
+APPKIT_EXTERN NSExceptionName NSPrintOperationExistsException;
 
 @interface NSPrintOperation : NSObject {
 }
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRuleEditor.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRuleEditor.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRuleEditor.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSRuleEditor.h	2016-07-27 05:10:07.000000000 +0200
@@ -246,7 +246,7 @@
 
 /* Posted to the default notification center whenever the view's rows change.
  * The object is the NSRuleEditor; there is no userInfo */
-APPKIT_EXTERN NSString * const NSRuleEditorRowsDidChangeNotification;
+APPKIT_EXTERN NSNotificationName const NSRuleEditorRowsDidChangeNotification;
 
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScreen.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScreen.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScreen.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScreen.h	2016-07-27 05:10:07.000000000 +0200
@@ -9,6 +9,7 @@
 #import <Foundation/NSArray.h>
 #import <Foundation/NSDictionary.h>
 #import <Foundation/NSGeometry.h>
+#import <Foundation/NSNotification.h>
 #import <AppKit/NSGraphics.h>
 
 NS_ASSUME_NONNULL_BEGIN
@@ -63,7 +64,7 @@
 
 
 /* Notifications */
-APPKIT_EXTERN NSString * const NSScreenColorSpaceDidChangeNotification NS_AVAILABLE_MAC(10_6);  // the notification object is the screen whose profile has changed
+APPKIT_EXTERN NSNotificationName const NSScreenColorSpaceDidChangeNotification NS_AVAILABLE_MAC(10_6);  // the notification object is the screen whose profile has changed
 
 
 @interface NSScreen (NSExtendedDynamicRange)
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScrollView.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScrollView.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScrollView.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScrollView.h	2016-07-27 05:10:07.000000000 +0200
@@ -209,27 +209,27 @@
 
 /* This notification is sent at the beginning of a magnify gesture. The notification object is the scroll view performing the magnification.
 */
-APPKIT_EXTERN NSString * const NSScrollViewWillStartLiveMagnifyNotification NS_AVAILABLE_MAC(10_8);
+APPKIT_EXTERN NSNotificationName const NSScrollViewWillStartLiveMagnifyNotification NS_AVAILABLE_MAC(10_8);
 
 /* This notification is sent at the end of magnify gesture. The notification object is the scroll view view performing the magnification.
 */
-APPKIT_EXTERN NSString * const NSScrollViewDidEndLiveMagnifyNotification NS_AVAILABLE_MAC(10_8);
+APPKIT_EXTERN NSNotificationName const NSScrollViewDidEndLiveMagnifyNotification NS_AVAILABLE_MAC(10_8);
 
 /* This notification is sent on the main thread at the beginning of user initiated live scroll tracking (gesture scroll or scroller tracking, e.g. thumb dragging).
  The notification object is the scroll view performing the scroll.
 */
-APPKIT_EXTERN NSString * const NSScrollViewWillStartLiveScrollNotification NS_AVAILABLE_MAC(10_9);
+APPKIT_EXTERN NSNotificationName const NSScrollViewWillStartLiveScrollNotification NS_AVAILABLE_MAC(10_9);
 
 /* This notification is sent on the main thread after changing the clipview bounds origin due to a user initiated event.
  Not all user initiated scrolls are bracketed by a willStart/didEnd notification pair (legacy mice).
  The notification object is the scroll view performing the scroll.
 */
-APPKIT_EXTERN NSString * const NSScrollViewDidLiveScrollNotification NS_AVAILABLE_MAC(10_9);
+APPKIT_EXTERN NSNotificationName const NSScrollViewDidLiveScrollNotification NS_AVAILABLE_MAC(10_9);
 
 /* This notification is sent on the main thread at the end of live scroll tracking.
  The notification object is the scroll view performing the scroll.
 */
-APPKIT_EXTERN NSString * const NSScrollViewDidEndLiveScrollNotification NS_AVAILABLE_MAC(10_9);
+APPKIT_EXTERN NSNotificationName const NSScrollViewDidEndLiveScrollNotification NS_AVAILABLE_MAC(10_9);
 
 
 @interface NSScrollView(NSRulerSupport)
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScroller.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScroller.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScroller.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScroller.h	2016-07-27 05:10:07.000000000 +0200
@@ -161,6 +161,6 @@
 
 /* Posted when the preferred scroller style changes.  The notification object is private; disregard it.  Consult NSScroller's +preferredScrollerStyle method when this notification is received, or thereafter, to determine the new scroller style to use.
 */
-APPKIT_EXTERN NSString * const NSPreferredScrollerStyleDidChangeNotification NS_AVAILABLE_MAC(10_7);
+APPKIT_EXTERN NSNotificationName const NSPreferredScrollerStyleDidChangeNotification NS_AVAILABLE_MAC(10_7);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSliderCell.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSliderCell.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSliderCell.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSliderCell.h	2016-07-27 05:10:07.000000000 +0200
@@ -44,7 +44,8 @@
         unsigned int snappedToDefaultValue:1;
         unsigned int snappingAllowed:1;
         unsigned int collapseOnResize:1;
-        unsigned int reserved2:18;
+        unsigned int startedOnAccessory:1;
+        unsigned int reserved2:17;
     } _scFlags;
 }
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSplitView.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSplitView.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSplitView.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSplitView.h	2016-07-27 05:10:07.000000000 +0200
@@ -189,11 +189,11 @@
 
 /* A notification that is posted to the default notification center by NSSplitView when a split view is about to resize its subviews either as a result of its own resizing or during the dragging of one of its dividers by the user. Starting in Mac OS 10.5, if the notification is being sent because the user is dragging a divider, the notification's user info dictionary contains an entry whose key is @"NSSplitViewDividerIndex" and whose value is an NSInteger-wrapping NSNumber that is the index of the divider being dragged.
 */
-APPKIT_EXTERN NSString * NSSplitViewWillResizeSubviewsNotification;
+APPKIT_EXTERN NSNotificationName NSSplitViewWillResizeSubviewsNotification;
 
 /* A notification that is posted to the default notification center by NSSplitView when a split view has just resized its subviews either as a result of its own resizing or during the dragging of one of its dividers by the user. Starting in Mac OS 10.5, if the notification is being sent because the user is dragging a divider, the notification's user info dictionary contains an entry whose key is @"NSSplitViewDividerIndex" and whose value is an NSInteger-wrapping NSNumber that is the index of the divider being dragged.
 */
-APPKIT_EXTERN NSString * NSSplitViewDidResizeSubviewsNotification;
+APPKIT_EXTERN NSNotificationName NSSplitViewDidResizeSubviewsNotification;
 
 
 @interface NSSplitView (NSDeprecated)
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStackView.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStackView.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStackView.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStackView.h	2016-07-27 05:10:07.000000000 +0200
@@ -101,7 +101,7 @@
 NS_CLASS_AVAILABLE(10_9, NA)
 @interface NSStackView : NSView {
 @private
-    id<NSStackViewDelegate> _delegate;
+    id _delegate;
     
     NSUserInterfaceLayoutOrientation _orientation;
     NSInteger _alignment;
@@ -131,7 +131,7 @@
 
 #pragma mark General StackView Properties
 
-@property (nullable, assign) id<NSStackViewDelegate> delegate;
+@property (nullable, weak) id<NSStackViewDelegate> delegate;
 
 /// Orientation of the StackView, defaults to NSUserInterfaceLayoutOrientationHorizontal
 @property NSUserInterfaceLayoutOrientation orientation;
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabView.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabView.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabView.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabView.h	2016-07-27 05:10:07.000000000 +0200
@@ -118,8 +118,8 @@
 @property (nullable, readonly, strong) NSTabViewItem *selectedTabViewItem;	// return nil if none are selected
 @property (strong) NSFont *font;						// returns font used for all tab labels.
 @property NSTabViewType tabViewType;                                            // Use tabPosition and tabViewBorderType instead. Setting this will also set the tabPosition and tabViewBorderType. Setting tabPosition or tabViewBorderType will affect tabViewType
-@property NSTabPosition tabPosition;
-@property NSTabViewBorderType tabViewBorderType;                                // This will only be respected if NSTabPosition is NSTabPositionNone.
+@property NSTabPosition tabPosition NS_AVAILABLE_MAC(10_12);
+@property NSTabViewBorderType tabViewBorderType NS_AVAILABLE_MAC(10_12);        // This will only be respected if NSTabPosition is NSTabPositionNone.
 @property (readonly, copy) NSArray<__kindof NSTabViewItem *> *tabViewItems;
 @property BOOL allowsTruncatedLabels;
 @property (readonly) NSSize minimumSize;					// returns the minimum size of the tab view
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableView.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableView.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableView.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableView.h	2016-07-27 05:10:07.000000000 +0200
@@ -749,10 +749,10 @@
 
 @end
 
-APPKIT_EXTERN NSString * NSTableViewSelectionDidChangeNotification;
-APPKIT_EXTERN NSString * NSTableViewColumnDidMoveNotification;       // @"NSOldColumn", @"NSNewColumn"
-APPKIT_EXTERN NSString * NSTableViewColumnDidResizeNotification;     // @"NSTableColumn", @"NSOldWidth"
-APPKIT_EXTERN NSString * NSTableViewSelectionIsChangingNotification;
+APPKIT_EXTERN NSNotificationName NSTableViewSelectionDidChangeNotification;
+APPKIT_EXTERN NSNotificationName NSTableViewColumnDidMoveNotification;       // @"NSOldColumn", @"NSNewColumn"
+APPKIT_EXTERN NSNotificationName NSTableViewColumnDidResizeNotification;     // @"NSTableColumn", @"NSOldWidth"
+APPKIT_EXTERN NSNotificationName NSTableViewSelectionIsChangingNotification;
 
 // The NSTableViewRowViewKey is the key that View Based TableView uses to identify the NIB containing the template row view. You can specify a custom row view (without any code) by associating this key with the appropriate NIB name in IB.
 APPKIT_EXTERN NSString * const NSTableViewRowViewKey NS_AVAILABLE_MAC(10_7); // @"NSTableViewRowViewKey"
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSText.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSText.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSText.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSText.h	2016-07-27 05:10:07.000000000 +0200
@@ -149,9 +149,9 @@
 @end
 
 /* Notifications */
-APPKIT_EXTERN NSString * NSTextDidBeginEditingNotification;
-APPKIT_EXTERN NSString * NSTextDidEndEditingNotification;    // userInfo key:  @"NSTextMovement"
-APPKIT_EXTERN NSString * NSTextDidChangeNotification;
+APPKIT_EXTERN NSNotificationName NSTextDidBeginEditingNotification;
+APPKIT_EXTERN NSNotificationName NSTextDidEndEditingNotification;    // userInfo key:  @"NSTextMovement"
+APPKIT_EXTERN NSNotificationName NSTextDidChangeNotification;
 
 
 /* Deprecated */
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextAlternatives.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextAlternatives.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextAlternatives.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextAlternatives.h	2016-07-27 05:10:07.000000000 +0200
@@ -7,6 +7,7 @@
 
 #import <Foundation/NSObject.h>
 #import <Foundation/NSArray.h>
+#import <Foundation/NSNotification.h>
 #import <AppKit/AppKitDefines.h>
 
 NS_ASSUME_NONNULL_BEGIN
@@ -30,6 +31,6 @@
 
 @end
 
-APPKIT_EXTERN NSString * NSTextAlternativesSelectedAlternativeStringNotification NS_AVAILABLE_MAC(10_8); // @"NSAlternativeString"
+APPKIT_EXTERN NSNotificationName NSTextAlternativesSelectedAlternativeStringNotification NS_AVAILABLE_MAC(10_8); // @"NSAlternativeString"
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextContainer.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextContainer.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextContainer.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextContainer.h	2016-07-27 05:10:07.000000000 +0200
@@ -84,7 +84,11 @@
 @property BOOL heightTracksTextView;
 
 // Set/get the view which the container is drawn in.  Having a view is optional.
+#if MAC_OS_X_VERSION_MIN_REQUIRED < MAC_OS_X_VERSION_10_12
 @property (nullable, strong) NSTextView *textView;
+#else
+@property (nullable, weak) NSTextView *textView;
+#endif
 @end
 
 /**************************** Deprecated ****************************/
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextInputContext.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextInputContext.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextInputContext.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextInputContext.h	2016-07-27 05:10:07.000000000 +0200
@@ -8,6 +8,7 @@
 #import <Foundation/NSArray.h>
 #import <AppKit/AppKitDefines.h>
 #import <AppKit/NSTextInputClient.h>
+#import <Foundation/NSNotification.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -121,7 +122,7 @@
 /**** Notifications ****/
 /* Notified whenever the selected text input source changes.
  */
-APPKIT_EXTERN NSString * NSTextInputContextKeyboardSelectionDidChangeNotification NS_AVAILABLE_MAC(10_6);
+APPKIT_EXTERN NSNotificationName NSTextInputContextKeyboardSelectionDidChangeNotification NS_AVAILABLE_MAC(10_6);
 
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextStorage.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextStorage.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextStorage.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextStorage.h	2016-07-27 05:10:07.000000000 +0200
@@ -117,8 +117,8 @@
 
 /**** Notifications ****/
 
-APPKIT_EXTERN NSString *  NSTextStorageWillProcessEditingNotification NS_AVAILABLE(10_0, 7_0);
-APPKIT_EXTERN NSString *  NSTextStorageDidProcessEditingNotification NS_AVAILABLE(10_0, 7_0);
+APPKIT_EXTERN NSNotificationName NSTextStorageWillProcessEditingNotification NS_AVAILABLE(10_0, 7_0);
+APPKIT_EXTERN NSNotificationName NSTextStorageDidProcessEditingNotification NS_AVAILABLE(10_0, 7_0);
 
 /**** Deprecations ****/
 // NSTextStorageEditedOptions is deprecated along with -[NSLayoutManager textStorage:edited:range:changeInLength:invalidatedRange:. Use NSTextStorageEditActions.
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextView.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextView.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextView.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextView.h	2016-07-27 05:10:07.000000000 +0200
@@ -54,7 +54,9 @@
 */
 APPKIT_EXTERN NSString * NSAllRomanInputSourcesLocaleIdentifier NS_AVAILABLE_MAC(10_5);
 
+#if MAC_OS_X_VERSION_MIN_REQUIRED < MAC_OS_X_VERSION_10_12
 NS_AUTOMATED_REFCOUNT_WEAK_UNAVAILABLE
+#endif
 @interface NSTextView : NSText <NSUserInterfaceValidations, NSTextInputClient, NSTextLayoutOrientationProvider, NSDraggingSource, NSTextInput, NSAccessibilityNavigableStaticText>
 
 /**************************** Initializing ****************************/
@@ -188,6 +190,10 @@
 // Here point is in view coordinates, and the return value is a character index appropriate for placing a zero-length selection for an insertion point associated with the mouse at the given point.  The NSTextInput method characterIndexForPoint: is not suitable for this role.
 - (NSUInteger)characterIndexForInsertionAtPoint:(NSPoint)point NS_AVAILABLE_MAC(10_5);
 
+/**************************** Ownership policy ****************************/
+// Returns whether instances of the class operate in the object ownership policy introduced with macOS Sierra and later. When YES, the new object owner policy is used. Under the policy, each text view strongly retains its text storage and its text container weakly references the view. Also, the text views are compatible with __weak storage. The default is YES.
+@property(readonly, class) BOOL stronglyReferencesTextStorage NS_AVAILABLE_MAC(10_12);
+
 @end
 
 @interface NSTextView (NSCompletion)
@@ -536,12 +542,12 @@
 @end
 
 // NSOldNotifyingTextView -> the old view, NSNewNotifyingTextView -> the new view.  The text view delegate is not automatically registered to receive this notification because the text machinery will automatically switch over the delegate to observe the new first text view as the first text view changes.
-APPKIT_EXTERN NSString * NSTextViewWillChangeNotifyingTextViewNotification;
+APPKIT_EXTERN NSNotificationName NSTextViewWillChangeNotifyingTextViewNotification;
 
 // NSOldSelectedCharacterRange -> NSValue with old range.
-APPKIT_EXTERN NSString * NSTextViewDidChangeSelectionNotification;
+APPKIT_EXTERN NSNotificationName NSTextViewDidChangeSelectionNotification;
 
-APPKIT_EXTERN NSString * NSTextViewDidChangeTypingAttributesNotification;
+APPKIT_EXTERN NSNotificationName NSTextViewDidChangeTypingAttributesNotification;
 
 
 /* These constants are deprecated in favor of their NSTextFinder equivalents. */
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSToolbar.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSToolbar.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSToolbar.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSToolbar.h	2016-07-27 05:10:07.000000000 +0200
@@ -186,8 +186,8 @@
 @end
 
 /* Notifications */
-APPKIT_EXTERN NSString * NSToolbarWillAddItemNotification;
-APPKIT_EXTERN NSString * NSToolbarDidRemoveItemNotification;
+APPKIT_EXTERN NSNotificationName NSToolbarWillAddItemNotification;
+APPKIT_EXTERN NSNotificationName NSToolbarDidRemoveItemNotification;
 
 
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSToolbarItem.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSToolbarItem.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSToolbarItem.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSToolbarItem.h	2016-07-27 05:10:07.000000000 +0200
@@ -12,7 +12,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-@class NSToolbarItemViewer, NSMenuItem, NSView, NSImage;
+@class NSToolbarItemViewer, NSMenuItem, NSView, NSImage, CKShare;
 
 @interface NSToolbarItem : NSObject <NSCopying, NSValidatedUserInterfaceItem> {
 @private
@@ -151,6 +151,13 @@
 
 @end
 
+@protocol NSCloudSharingValidation <NSObject>
+
+/* NSToolbarItems created with NSToolbarCloudSharingItemIdentifier use this method for further validation after sending `-validateToolbarItem:` or `-validateUserInterfaceItem:`. The validator for the item's action should return the current CKShare corresponding to the selected item, if any. The state of the item will be changed reflect the state of the CKShare. */
+- (nullable CKShare *)cloudShareForUserInterfaceItem:(id <NSValidatedUserInterfaceItem>)item;
+
+@end
+
 
 /* standard toolbar item identifiers */
 
@@ -163,5 +170,8 @@
 APPKIT_EXTERN NSString * NSToolbarCustomizeToolbarItemIdentifier;  // Puts the current toolbar into customize mode.
 APPKIT_EXTERN NSString * NSToolbarPrintItemIdentifier;             // Sends printDocument: to firstResponder, but you can change this in toolbarWillAddItem: if you need to do so.
 APPKIT_EXTERN NSString * NSToolbarToggleSidebarItemIdentifier NS_AVAILABLE_MAC(10_11);  // A standard toolbar item identifier for sidebars. It sends -toggleSidebar: to the firstResponder.
+APPKIT_EXTERN NSString * NSToolbarCloudSharingItemIdentifier API_AVAILABLE(macosx(10.12)); // A standard toolbar item identifier for cloud sharing via NSSharingServiceNameCloudSharing. It validates itself and modifies its appearance by using the NSCloudSharingValidation protocol. It sends -performCloudSharing: to the firstResponder.
+
+
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSView.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSView.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSView.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSView.h	2016-07-27 05:10:07.000000000 +0200
@@ -626,20 +626,20 @@
 
 /* Sent when the frame changes for a view. This is only sent if postsFrameChangedNotifications is set to YES.
  */
-APPKIT_EXTERN NSString *NSViewFrameDidChangeNotification;
-APPKIT_EXTERN NSString *NSViewFocusDidChangeNotification;
+APPKIT_EXTERN NSNotificationName NSViewFrameDidChangeNotification;
+APPKIT_EXTERN NSNotificationName NSViewFocusDidChangeNotification;
 
 /* This notification is sent whenever the views bounds change and the frame does not.  That is, it is sent whenever the view's bounds are translated, scaled or rotated, but NOT when the bounds change as a result of, for example, setFrameSize:.
  */
-APPKIT_EXTERN NSString *NSViewBoundsDidChangeNotification;
+APPKIT_EXTERN NSNotificationName NSViewBoundsDidChangeNotification;
 
 /* This notification is sent whenever an NSView that has an attached NSSurface changes size or changes screens (thus potentially changing graphics hardware drivers.)
  */
-APPKIT_EXTERN NSString *NSViewGlobalFrameDidChangeNotification;
+APPKIT_EXTERN NSNotificationName NSViewGlobalFrameDidChangeNotification;
     
 /* This notification is sent whenever tracking areas should be recalculated for the view.  It is sent after the view receives -updateTrackingAreas.
  */
-APPKIT_EXTERN NSString *NSViewDidUpdateTrackingAreasNotification NS_AVAILABLE_MAC(10_5);
+APPKIT_EXTERN NSNotificationName NSViewDidUpdateTrackingAreasNotification NS_AVAILABLE_MAC(10_5);
 
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindow.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindow.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindow.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindow.h	2016-07-27 05:10:07.000000000 +0200
@@ -19,6 +19,8 @@
 #import <AppKit/NSAnimation.h>
 #import <AppKit/NSAppearance.h>
 
+#define NSWINDOW_TRACK_EVENTS_DECLARES_NULLABILITY APPKIT_SWIFT_SDK_EPOCH_AT_LEAST(3)
+
 NS_ASSUME_NONNULL_BEGIN
 
 @class NSButton, NSButtonCell, NSColor, NSImage, NSPasteboard, NSScreen, NSNotification, NSText, NSView, NSMutableSet, NSSet, NSDate, NSToolbar, NSGraphicsContext, NSURL, NSColorSpace, NSDockTile, NSViewController, NSTitlebarAccessoryViewController, NSWindowAuxiliary, NSEvent, NSWindowController;
@@ -714,14 +716,16 @@
 @interface NSWindow(NSEvent)
 /* Tracks events matching the supplied mask with the supplied tracking handler until the tracking handler explicitly terminates tracking. Each event is removed from the event queue then passed to the tracking handler. If a matching event does not exist in the event queue, then the main thread blocks in the specified runloop mode until an event of the requested type is received or the timeout expires. If the timeout expires, the tracking handler is called with a nil event. A negative timeout is interpreted as 0. Use NSEventDurationForever to never timeout. Tracking continues until *stop is set to YES. Calls to -nextEventMatchingMask:… are allowed inside the trackingHandler block. This method returns once tracking is terminated.
  */
-- (void)trackEventsMatchingMask:(NSEventMask)mask timeout:(NSTimeInterval)timeout mode:(NSString *)mode handler:(void(^)(NSEvent *event, BOOL *stop))trackingHandler NS_AVAILABLE_MAC(10_10);
+#if NSWINDOW_TRACK_EVENTS_DECLARES_NULLABILITY
+- (void)trackEventsMatchingMask:(NSEventMask)mask timeout:(NSTimeInterval)timeout mode:(NSString *)mode handler:(void(NS_NOESCAPE ^)(NSEvent *__nullable event, BOOL *stop))trackingHandler NS_AVAILABLE_MAC(10_10);
+#endif
 #if __LP64__
 - (nullable NSEvent *)nextEventMatchingMask:(NSEventMask)mask;
-- (nullable NSEvent *)nextEventMatchingMask:(NSEventMask)mask untilDate:(nullable NSDate *)expiration inMode:(NSString *)mode dequeue:(BOOL)deqFlag;
+- (nullable NSEvent *)nextEventMatchingMask:(NSEventMask)mask untilDate:(nullable NSDate *)expiration inMode:(NSRunLoopMode)mode dequeue:(BOOL)deqFlag;
 - (void)discardEventsMatchingMask:(NSEventMask)mask beforeEvent:(nullable NSEvent *)lastEvent;
 #else
 - (nullable NSEvent *)nextEventMatchingMask:(NSUInteger)mask;
-- (nullable NSEvent *)nextEventMatchingMask:(NSUInteger)mask untilDate:(nullable NSDate *)expiration inMode:(NSString *)mode dequeue:(BOOL)deqFlag;
+- (nullable NSEvent *)nextEventMatchingMask:(NSUInteger)mask untilDate:(nullable NSDate *)expiration inMode:(NSRunLoopMode)mode dequeue:(BOOL)deqFlag;
 - (void)discardEventsMatchingMask:(NSUInteger)mask beforeEvent:(nullable NSEvent *)lastEvent;
 #endif
 
@@ -864,26 +868,26 @@
 
 
 /* Notifications */
-APPKIT_EXTERN NSString *NSWindowDidBecomeKeyNotification;
-APPKIT_EXTERN NSString *NSWindowDidBecomeMainNotification;
-APPKIT_EXTERN NSString *NSWindowDidChangeScreenNotification;
-APPKIT_EXTERN NSString *NSWindowDidDeminiaturizeNotification;
-APPKIT_EXTERN NSString *NSWindowDidExposeNotification;			// userInfo key:  @"NSExposedRect"
-APPKIT_EXTERN NSString *NSWindowDidMiniaturizeNotification;
-APPKIT_EXTERN NSString *NSWindowDidMoveNotification;
-APPKIT_EXTERN NSString *NSWindowDidResignKeyNotification;
-APPKIT_EXTERN NSString *NSWindowDidResignMainNotification;
-APPKIT_EXTERN NSString *NSWindowDidResizeNotification;
-APPKIT_EXTERN NSString *NSWindowDidUpdateNotification;
-APPKIT_EXTERN NSString *NSWindowWillCloseNotification;
-APPKIT_EXTERN NSString *NSWindowWillMiniaturizeNotification;
-APPKIT_EXTERN NSString *NSWindowWillMoveNotification;
-APPKIT_EXTERN NSString *NSWindowWillBeginSheetNotification;
-APPKIT_EXTERN NSString *NSWindowDidEndSheetNotification;
+APPKIT_EXTERN NSNotificationName NSWindowDidBecomeKeyNotification;
+APPKIT_EXTERN NSNotificationName NSWindowDidBecomeMainNotification;
+APPKIT_EXTERN NSNotificationName NSWindowDidChangeScreenNotification;
+APPKIT_EXTERN NSNotificationName NSWindowDidDeminiaturizeNotification;
+APPKIT_EXTERN NSNotificationName NSWindowDidExposeNotification;			// userInfo key:  @"NSExposedRect"
+APPKIT_EXTERN NSNotificationName NSWindowDidMiniaturizeNotification;
+APPKIT_EXTERN NSNotificationName NSWindowDidMoveNotification;
+APPKIT_EXTERN NSNotificationName NSWindowDidResignKeyNotification;
+APPKIT_EXTERN NSNotificationName NSWindowDidResignMainNotification;
+APPKIT_EXTERN NSNotificationName NSWindowDidResizeNotification;
+APPKIT_EXTERN NSNotificationName NSWindowDidUpdateNotification;
+APPKIT_EXTERN NSNotificationName NSWindowWillCloseNotification;
+APPKIT_EXTERN NSNotificationName NSWindowWillMiniaturizeNotification;
+APPKIT_EXTERN NSNotificationName NSWindowWillMoveNotification;
+APPKIT_EXTERN NSNotificationName NSWindowWillBeginSheetNotification;
+APPKIT_EXTERN NSNotificationName NSWindowDidEndSheetNotification;
 
 /* NSWindowDidChangeBackingPropertiesNotification is posted on 10.7.3 and later, when a window's backingScaleFactor and/or its colorSpace changes.  When running on a system version where this new notification is available, applications should use it instead of NSWindowDidChangeScreenProfileNotification to watch for changes to either of these backing store properties.  Many applications won't have any need to watch for this notification, but those that perform sophisticated color handling or manually manage their own caches of window-resolution-and/or/colorspace-appropriate bitmapped images will find this notification useful, as a prompt to invalidate their caches or schedule other reassessment for the new resolution and/or color space as needed.  The notification's userInfo dictionary specifies the window's previous backingScaleFactor and colorSpace.  You can compare these with the window's new backingScaleFactor and colorSpace at the time of the notification, to determine which of these two properties (potentially both) changed.
 */
-APPKIT_EXTERN NSString * const NSWindowDidChangeBackingPropertiesNotification NS_AVAILABLE_MAC(10_7); // added in 10.7.3; userInfo keys: NSBackingPropertyOldScaleFactorKey, NSBackingPropertyOldColorSpaceKey
+APPKIT_EXTERN NSNotificationName const NSWindowDidChangeBackingPropertiesNotification NS_AVAILABLE_MAC(10_7); // added in 10.7.3; userInfo keys: NSBackingPropertyOldScaleFactorKey, NSBackingPropertyOldColorSpaceKey
 
 APPKIT_EXTERN NSString * const NSBackingPropertyOldScaleFactorKey NS_AVAILABLE_MAC(10_7); // added in 10.7.3; an NSNumber
 APPKIT_EXTERN NSString * const NSBackingPropertyOldColorSpaceKey NS_AVAILABLE_MAC(10_7);  // added in 10.7.3; an NSColorSpace
@@ -891,22 +895,22 @@
 
 /* NSWindowDidChangeScreenProfileNotification is posted when a window's display's color profile changes, or when the window moves to a display that has a different color profile.  When running on 10.7.3 or later, this notification is still posted for compatibility, but modern applications should instead watch for NSWindowDidChangeBackingPropertiesNotification, which is posted for both color space and resolution changes, and facilitates handling both in a single update and redisplay pass.
 */
-APPKIT_EXTERN NSString *NSWindowDidChangeScreenProfileNotification;
+APPKIT_EXTERN NSNotificationName NSWindowDidChangeScreenProfileNotification;
 
 /* NSWindowWillStartLiveResizeNotification is sent when the user starts a live resize operation via a mouseDown in the resize corner.  The notification will be sent before the window size is changed.  Note that this notification is sent once for a sequence of window resize operations */
-APPKIT_EXTERN NSString * const NSWindowWillStartLiveResizeNotification  NS_AVAILABLE_MAC(10_6);
+APPKIT_EXTERN NSNotificationName const NSWindowWillStartLiveResizeNotification  NS_AVAILABLE_MAC(10_6);
 /* NSWindowDidEndLiveResizeNotification is sent after the user ends a live resize operation via a mouseUp in the resize corner.  The notification will be sent after the final window size change.    Note that this notification is sent once for a sequence of window resize operations */
-APPKIT_EXTERN NSString * const NSWindowDidEndLiveResizeNotification  NS_AVAILABLE_MAC(10_6);
-APPKIT_EXTERN NSString * const NSWindowWillEnterFullScreenNotification NS_AVAILABLE_MAC(10_7);
-APPKIT_EXTERN NSString * const NSWindowDidEnterFullScreenNotification NS_AVAILABLE_MAC(10_7);
-APPKIT_EXTERN NSString * const NSWindowWillExitFullScreenNotification NS_AVAILABLE_MAC(10_7);
-APPKIT_EXTERN NSString * const NSWindowDidExitFullScreenNotification NS_AVAILABLE_MAC(10_7);
-APPKIT_EXTERN NSString * const NSWindowWillEnterVersionBrowserNotification NS_AVAILABLE_MAC(10_7);
-APPKIT_EXTERN NSString * const NSWindowDidEnterVersionBrowserNotification NS_AVAILABLE_MAC(10_7);
-APPKIT_EXTERN NSString * const NSWindowWillExitVersionBrowserNotification NS_AVAILABLE_MAC(10_7);
-APPKIT_EXTERN NSString * const NSWindowDidExitVersionBrowserNotification NS_AVAILABLE_MAC(10_7);
+APPKIT_EXTERN NSNotificationName const NSWindowDidEndLiveResizeNotification  NS_AVAILABLE_MAC(10_6);
+APPKIT_EXTERN NSNotificationName const NSWindowWillEnterFullScreenNotification NS_AVAILABLE_MAC(10_7);
+APPKIT_EXTERN NSNotificationName const NSWindowDidEnterFullScreenNotification NS_AVAILABLE_MAC(10_7);
+APPKIT_EXTERN NSNotificationName const NSWindowWillExitFullScreenNotification NS_AVAILABLE_MAC(10_7);
+APPKIT_EXTERN NSNotificationName const NSWindowDidExitFullScreenNotification NS_AVAILABLE_MAC(10_7);
+APPKIT_EXTERN NSNotificationName const NSWindowWillEnterVersionBrowserNotification NS_AVAILABLE_MAC(10_7);
+APPKIT_EXTERN NSNotificationName const NSWindowDidEnterVersionBrowserNotification NS_AVAILABLE_MAC(10_7);
+APPKIT_EXTERN NSNotificationName const NSWindowWillExitVersionBrowserNotification NS_AVAILABLE_MAC(10_7);
+APPKIT_EXTERN NSNotificationName const NSWindowDidExitVersionBrowserNotification NS_AVAILABLE_MAC(10_7);
 /* Upon receiving this notification, you can query the NSWindow for its current occlusion state. Note that this only notifies about changes in the state of the occlusion, not when the occlusion region changes. You can use this notification to increase responsiveness and save power, by halting any expensive calculations that the user can not see. */
-APPKIT_EXTERN NSString * const NSWindowDidChangeOcclusionStateNotification NS_AVAILABLE_MAC(10_9);
+APPKIT_EXTERN NSNotificationName const NSWindowDidChangeOcclusionStateNotification NS_AVAILABLE_MAC(10_9);
 
 /* NSUnscaledWindowMask is deprecated and has no effect. The scale factor for a window backing store is dynamic and dependent on the screen it is placed on.
  */
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindowRestoration.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindowRestoration.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindowRestoration.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindowRestoration.h	2016-07-27 05:10:07.000000000 +0200
@@ -46,7 +46,7 @@
 
 /* NSApplicationDidFinishRestoringWindowsNotification is posted when the application is finished restoring windows, that is, when all the completion handlers from restoreWindowWithIdentifier:state:completionHandler: have been called.  This is always posted after NSApplicationWillFinishLaunching, but may be posted before or after NSApplicationDidFinishLaunching, depending on whether clients copy the completion handlers and invoke them later.  If there were no windows to restore, then this notification is still posted at the corresponding point in app launch (between NSApplicationWillFinishLaunchingNotification and NSApplicationDidFinishLaunchingNotification).  The object is NSApplication, and there is no user info.
  */
-APPKIT_EXTERN NSString * const NSApplicationDidFinishRestoringWindowsNotification NS_AVAILABLE_MAC(10_7);
+APPKIT_EXTERN NSNotificationName const NSApplicationDidFinishRestoringWindowsNotification NS_AVAILABLE_MAC(10_7);
 
 
 @interface NSWindow (NSUserInterfaceRestoration)
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWorkspace.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWorkspace.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWorkspace.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWorkspace.h	2016-07-27 05:10:07.000000000 +0200
@@ -254,13 +254,13 @@
  */
 APPKIT_EXTERN NSString * const NSWorkspaceApplicationKey NS_AVAILABLE_MAC(10_6);
 
-APPKIT_EXTERN NSString * NSWorkspaceWillLaunchApplicationNotification;	//	see above
-APPKIT_EXTERN NSString * NSWorkspaceDidLaunchApplicationNotification;	//	see above
-APPKIT_EXTERN NSString * NSWorkspaceDidTerminateApplicationNotification;	//	see above
-APPKIT_EXTERN NSString * const NSWorkspaceDidHideApplicationNotification NS_AVAILABLE_MAC(10_6);
-APPKIT_EXTERN NSString * const NSWorkspaceDidUnhideApplicationNotification NS_AVAILABLE_MAC(10_6);
-APPKIT_EXTERN NSString * const NSWorkspaceDidActivateApplicationNotification NS_AVAILABLE_MAC(10_6);
-APPKIT_EXTERN NSString * const NSWorkspaceDidDeactivateApplicationNotification NS_AVAILABLE_MAC(10_6);
+APPKIT_EXTERN NSNotificationName NSWorkspaceWillLaunchApplicationNotification;	//	see above
+APPKIT_EXTERN NSNotificationName NSWorkspaceDidLaunchApplicationNotification;	//	see above
+APPKIT_EXTERN NSNotificationName NSWorkspaceDidTerminateApplicationNotification;	//	see above
+APPKIT_EXTERN NSNotificationName const NSWorkspaceDidHideApplicationNotification NS_AVAILABLE_MAC(10_6);
+APPKIT_EXTERN NSNotificationName const NSWorkspaceDidUnhideApplicationNotification NS_AVAILABLE_MAC(10_6);
+APPKIT_EXTERN NSNotificationName const NSWorkspaceDidActivateApplicationNotification NS_AVAILABLE_MAC(10_6);
+APPKIT_EXTERN NSNotificationName const NSWorkspaceDidDeactivateApplicationNotification NS_AVAILABLE_MAC(10_6);
 
 
 /* Volume notifications */
@@ -275,36 +275,36 @@
 APPKIT_EXTERN NSString * const NSWorkspaceVolumeOldLocalizedNameKey NS_AVAILABLE_MAC(10_6); //NSString containing the old user-visible name of the volume
 APPKIT_EXTERN NSString * const NSWorkspaceVolumeOldURLKey NS_AVAILABLE_MAC(10_6);  //NSURL containing the old mount path of the volume
 
-APPKIT_EXTERN NSString * NSWorkspaceDidMountNotification;		//	@"NSDevicePath"
-APPKIT_EXTERN NSString * NSWorkspaceDidUnmountNotification;		//	@"NSDevicePath"
-APPKIT_EXTERN NSString * NSWorkspaceWillUnmountNotification;		//	@"NSDevicePath"
+APPKIT_EXTERN NSNotificationName NSWorkspaceDidMountNotification;		//	@"NSDevicePath"
+APPKIT_EXTERN NSNotificationName NSWorkspaceDidUnmountNotification;		//	@"NSDevicePath"
+APPKIT_EXTERN NSNotificationName NSWorkspaceWillUnmountNotification;		//	@"NSDevicePath"
 
 /* NSWorkspaceDidRenameVolumeNotification is posted when a volume changes its name and/or mount path.  These typically change simultaneously, in which case only one notification is posted.
  */
-APPKIT_EXTERN NSString * const NSWorkspaceDidRenameVolumeNotification NS_AVAILABLE_MAC(10_6);
+APPKIT_EXTERN NSNotificationName const NSWorkspaceDidRenameVolumeNotification NS_AVAILABLE_MAC(10_6);
 
 
 /* Power notifications */
-APPKIT_EXTERN NSString * const NSWorkspaceWillPowerOffNotification;
+APPKIT_EXTERN NSNotificationName const NSWorkspaceWillPowerOffNotification;
 
-APPKIT_EXTERN NSString * NSWorkspaceWillSleepNotification;
-APPKIT_EXTERN NSString * NSWorkspaceDidWakeNotification;
+APPKIT_EXTERN NSNotificationName NSWorkspaceWillSleepNotification;
+APPKIT_EXTERN NSNotificationName NSWorkspaceDidWakeNotification;
 
-APPKIT_EXTERN NSString * const NSWorkspaceScreensDidSleepNotification	NS_AVAILABLE_MAC(10_6);
-APPKIT_EXTERN NSString * const NSWorkspaceScreensDidWakeNotification	NS_AVAILABLE_MAC(10_6);
+APPKIT_EXTERN NSNotificationName const NSWorkspaceScreensDidSleepNotification	NS_AVAILABLE_MAC(10_6);
+APPKIT_EXTERN NSNotificationName const NSWorkspaceScreensDidWakeNotification	NS_AVAILABLE_MAC(10_6);
 
 /* Session notifications */
-APPKIT_EXTERN NSString * NSWorkspaceSessionDidBecomeActiveNotification;
-APPKIT_EXTERN NSString * NSWorkspaceSessionDidResignActiveNotification;
+APPKIT_EXTERN NSNotificationName NSWorkspaceSessionDidBecomeActiveNotification;
+APPKIT_EXTERN NSNotificationName NSWorkspaceSessionDidResignActiveNotification;
 
 
 /* Miscellaneous notifications */
 
 /* NSWorkspaceDidChangeFileLabelsNotification is posted when the user changes a file label color name or the color itself.  The notification object is always NSWorkspace, and there is no user info.
  */
-APPKIT_EXTERN NSString * const NSWorkspaceDidChangeFileLabelsNotification NS_AVAILABLE_MAC(10_6);
+APPKIT_EXTERN NSNotificationName const NSWorkspaceDidChangeFileLabelsNotification NS_AVAILABLE_MAC(10_6);
 
-APPKIT_EXTERN NSString * const NSWorkspaceActiveSpaceDidChangeNotification NS_AVAILABLE_MAC(10_6);
+APPKIT_EXTERN NSNotificationName const NSWorkspaceActiveSpaceDidChangeNotification NS_AVAILABLE_MAC(10_6);
 
 
 /* The following keys can be used in the configuration dictionary of the launchApplicationAtURL:, openURL:, and openURL:withApplicationAtURL: methods.  Each key is optional, and if omitted, default behavior is applied. */
@@ -377,7 +377,7 @@
 APPKIT_EXTERN NSString * NSWorkspaceRecycleOperation NS_DEPRECATED_MAC(10_0, 10_11, "Use -[NSWorkspace recycleURLs:completionHandler:] instead.");
 APPKIT_EXTERN NSString * NSWorkspaceDuplicateOperation NS_DEPRECATED_MAC(10_0, 10_11, "Use -[NSWorkspace duplicateURLs:completionHandler:] instead.");
 
-APPKIT_EXTERN NSString * NSWorkspaceDidPerformFileOperationNotification NS_DEPRECATED_MAC(10_0, 10_11);	//	@"NSOperationNumber"
+APPKIT_EXTERN NSNotificationName NSWorkspaceDidPerformFileOperationNotification NS_DEPRECATED_MAC(10_0, 10_11);	//	@"NSOperationNumber"
 
 APPKIT_EXTERN NSString * NSPlainFileType NS_DEPRECATED_MAC(10_0, 10_6);
 APPKIT_EXTERN NSString * NSDirectoryFileType NS_DEPRECATED_MAC(10_0, 10_6);

```