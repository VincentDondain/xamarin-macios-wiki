#AppKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSApplication.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSApplication.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSApplication.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSApplication.h	2016-06-29 03:31:49.000000000 +0200
@@ -390,7 +390,7 @@
  
  You should use the CKShareMetadata object's shareURL and containerIdentifier to schedule a CKAcceptSharesOperation, then start using the resulting CKShare and its associated record(s), which will appear in the CKContainer's shared database in a zone matching that of the record's owner.
 */
-- (void)application:(NSApplication *)application userAcceptedCloudKitShareWithMetadata:(CKShareMetadata *)metadata NS_AVAILABLE_MAC(10_12);
+- (void)application:(NSApplication *)application userDidAcceptCloudKitShareWithMetadata:(CKShareMetadata *)metadata NS_AVAILABLE_MAC(10_12);
 
 /* Notifications:
  */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButton.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButton.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButton.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButton.h	2016-06-29 03:31:49.000000000 +0200
@@ -20,8 +20,10 @@
 @property (nullable, strong) NSImage *image;
 @property (nullable, strong) NSImage *alternateImage;
 @property NSCellImagePosition imagePosition;
+@property BOOL imageHugsTitle API_AVAILABLE(macosx(10.12));
+
 - (void)setButtonType:(NSButtonType)type;
-@property NSInteger state;
+@property NSInteger /* NSControlState */ state;
 @property (getter=isBordered) BOOL bordered;
 @property (getter=isTransparent) BOOL transparent;
 - (void)setPeriodicDelay:(float)delay interval:(float)interval;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButtonCell.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButtonCell.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButtonCell.h	2016-06-03 05:13:45.000000000 +0200

-typedef NS_ENUM(NSUInteger, NSGradientType) {
-    NSGradientNone          = 0,
-    NSGradientConcaveWeak   = 1,
-    NSGradientConcaveStrong = 2,
-    NSGradientConvexWeak    = 3,
-    NSGradientConvexStrong  = 4
-} NS_DEPRECATED_MAC(10_0, 10_12);
-
 @interface NSButtonCell(NSButtonCellExtensions)
 
-@property NSGradientType gradientType NS_DEPRECATED_MAC(10_0, 10_12, "The gradientType property is unused, and setting it has no effect.");
-
 // When disabled, the image and text of an NSButtonCell are normally dimmed with gray.
 // Radio buttons and switches use (imageDimsWhenDisabled == NO) so only their text is dimmed.
 @property BOOL imageDimsWhenDisabled;
@@ -203,30 +188,70 @@
 @end
 
 @interface NSButtonCell(NSButtonCellBezelStyles)
-
 @property NSBezelStyle bezelStyle;
-
 @end
 
 @interface NSButtonCell (NSButtonCellSoundExtensions)
 @property (nullable, strong) NSSound *sound;
 @end
 

 
 
@@ -68,16 +70,21 @@
     NSScaleNone NS_ENUM_DEPRECATED_MAC(10_0, 10_10, "Use NSImageScaleNone instead")
 } NS_ENUM_AVAILABLE_MAC(10_5);
 
+typedef NS_ENUM(NSInteger, NSControlState) {
+    NSControlStateMixed = -1,
+    NSControlStateOff   =  0,
+    NSControlStateOn    =  1
+};
+typedef NSInteger NSCellStateValue; /* Use NSControlState instead */
 
+// These constants will be deprecated in a future release. Please migrate to the modern typed equivalents.
 enum {
-    NSMixedState = -1,
-    NSOffState   =  0,
-    NSOnState    =  1
+    NSMixedState = NSControlStateMixed,
+    NSOffState   = NSControlStateOff,
+    NSOnState    = NSControlStateOn,
 };
-typedef NSInteger NSCellStateValue;
-
@@ -179,7 +186,7 @@
 
 @property (nullable, assign) NSView *controlView; // Must be an NSControl subclass, non-control view subclasses not allowed!
 @property NSCellType type;
-@property NSInteger state;
+@property NSInteger /* NSControlState */ state;
 @property (nullable, weak) id target; // Target is weak for zeroing-weak compatible objects in apps linked on 10.10 or later. Otherwise the behavior of this property is 'assign'.
 @property (nullable) SEL action;
 @property NSInteger tag;
@@ -307,7 +314,7 @@
 
 @interface NSCell(NSCellMixedState)	/* allow button to have mixed state value*/
 @property BOOL allowsMixedState;
-@property (readonly) NSInteger nextState;			/* get next state state in cycle */
+@property (readonly) NSInteger /* NSControlState */ nextState;			/* get next state state in cycle */
 - (void)setNextState;			/* toggle/cycle through states */
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSComboBox.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSComboBox.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSComboBox.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSComboBox.h	2016-06-29 03:31:49.000000000 +0200
@@ -15,7 +15,28 @@
 APPKIT_EXTERN NSString * NSComboBoxSelectionDidChangeNotification;
 APPKIT_EXTERN NSString * NSComboBoxSelectionIsChangingNotification;
 
-@protocol NSComboBoxDelegate, NSComboBoxDataSource;
+@class NSComboBox;
+
+@protocol NSComboBoxDataSource <NSObject>
+@optional
+/* These two methods are required when not using bindings */
+- (NSInteger)numberOfItemsInComboBox:(NSComboBox *)comboBox;
+- (nullable id)comboBox:(NSComboBox *)comboBox objectValueForItemAtIndex:(NSInteger)index;
+
+- (NSUInteger)comboBox:(NSComboBox *)comboBox indexOfItemWithStringValue:(NSString *)string;
+- (nullable NSString *)comboBox:(NSComboBox *)comboBox completedString:(NSString *)string;
+@end
+
+@protocol NSComboBoxDelegate <NSTextFieldDelegate>
+@optional
+
+/* Notifications */
+- (void)comboBoxWillPopUp:(NSNotification *)notification;
+- (void)comboBoxWillDismiss:(NSNotification *)notification;
+- (void)comboBoxSelectionDidChange:(NSNotification *)notification;
+- (void)comboBoxSelectionIsChanging:(NSNotification *)notification;
+
+@end
 
 @interface NSComboBox : NSTextField {
     /*All instance variables are private*/
@@ -65,25 +85,4 @@
 
 @end
 
-@protocol NSComboBoxDataSource <NSObject>
-@optional
-/* These two methods are required when not using bindings */
-- (NSInteger)numberOfItemsInComboBox:(NSComboBox *)comboBox;
-- (nullable id)comboBox:(NSComboBox *)comboBox objectValueForItemAtIndex:(NSInteger)index;
-
-- (NSUInteger)comboBox:(NSComboBox *)comboBox indexOfItemWithStringValue:(NSString *)string;
-- (nullable NSString *)comboBox:(NSComboBox *)comboBox completedString:(NSString *)string;
-@end
-
-@protocol NSComboBoxDelegate <NSTextFieldDelegate>
-@optional
-
-/* Notifications */
-- (void)comboBoxWillPopUp:(NSNotification *)notification;
-- (void)comboBoxWillDismiss:(NSNotification *)notification;
-- (void)comboBoxSelectionDidChange:(NSNotification *)notification;
-- (void)comboBoxSelectionIsChanging:(NSNotification *)notification;
-
-@end
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGraphics.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGraphics.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGraphics.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGraphics.h	2016-06-29 03:31:49.000000000 +0200
@@ -176,6 +176,12 @@
 APPKIT_EXTERN const CGFloat NSDarkGray;
 APPKIT_EXTERN const CGFloat NSBlack;
 
+/* Approximate color gamut for use by NSScreen and NSWindow
+ */
+typedef NS_ENUM(NSInteger, NSDisplayGamut) {
+    NSDisplayGamutSRGB = 1,
+    NSDisplayGamutP3
+} NS_ENUM_AVAILABLE_MAC(10_12);
 
 /* Keys for deviceDescription dictionaries.
 */

diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScreen.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScreen.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScreen.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScreen.h	2016-06-29 03:31:49.000000000 +0200
@@ -42,6 +42,10 @@
 
 @property (readonly) const NSWindowDepth *supportedWindowDepths NS_RETURNS_INNER_POINTER; /* 0 terminated */
 
+/* canRepresentDisplayGamut: returns YES if the colorSpace of the receiving screen is capable of representing the given display gamut
+ */
+- (BOOL)canRepresentDisplayGamut:(NSDisplayGamut)displayGamut  NS_AVAILABLE_MAC(10_12);
+
 /* Convert to/from the device pixel aligned coordinates sytem of a display 
  */
 - (NSRect)convertRectToBacking:(NSRect)rect NS_AVAILABLE_MAC(10_7);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabView.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabView.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabView.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabView.h	2016-06-29 03:31:49.000000000 +0200
@@ -17,6 +17,7 @@
 
 #define NSAppKitVersionNumberWithDirectionalTabs 631.0
 
+// Use tabPosition and tabViewBorderType instead
 typedef NS_ENUM(NSUInteger, NSTabViewType) {
     NSTopTabsBezelBorder	= 0,			// the default
     NSLeftTabsBezelBorder	= 1,
@@ -27,6 +28,20 @@
     NSNoTabsNoBorder		= 6
 };
 
+typedef NS_ENUM(NSUInteger, NSTabPosition) {
+    NSTabPositionNone                  = 0,
+    NSTabPositionTop                   = 1,
+    NSTabPositionLeft                  = 2,
+    NSTabPositionBottom                = 3,
+    NSTabPositionRight                 = 4
+} NS_AVAILABLE_MAC(10_12);
+
+typedef NS_ENUM(NSUInteger, NSTabViewBorderType) {
+    NSTabViewBorderTypeNone            = 0,
+    NSTabViewBorderTypeLine            = 1,
+    NSTabViewBorderTypeBezel           = 2
+} NS_AVAILABLE_MAC(10_12);
+
 @interface NSTabView : NSView
 {
 @private
@@ -95,12 +115,14 @@
 
 	/* Getters */
 
+@property NSTabPosition tabPosition;
+@property NSTabViewBorderType tabViewBorderType;                                // This will only be respected if NSTabPosition is NSTabPositionNone.
 @property (readonly, copy) NSArray<__kindof NSTabViewItem *> *tabViewItems;
 @property BOOL allowsTruncatedLabels;
 @property BOOL drawsBackground;  						// only relevant for borderless tab view type
 @property NSControlTint controlTint;
 @property NSControlSize controlSize;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTitlebarAccessoryViewController.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTitlebarAccessoryViewController.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTitlebarAccessoryViewController.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTitlebarAccessoryViewController.h	2016-06-29 03:31:50.000000000 +0200
@@ -53,6 +53,9 @@
 */
 @property CGFloat fullScreenMinHeight;
 
+/* Indicates whether the accessory view is actually visible in the window. When set, this property will collapse the accessory view to 0 height (animatable) but NOT remove it from the window. That way, you can easily show and hide it without difficulty. Set through the animator object to animate it. */
+@property (getter=isHidden) BOOL hidden NS_AVAILABLE_MAC(10_12);
+
 - (void)viewWillAppear NS_REQUIRES_SUPER;
 - (void)viewDidAppear NS_REQUIRES_SUPER;
 - (void)viewDidDisappear NS_REQUIRES_SUPER;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindow.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindow.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindow.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindow.h	2016-06-29 03:31:50.000000000 +0200
@@ -608,6 +608,10 @@
 
 @property (nullable, strong) NSColorSpace *colorSpace NS_AVAILABLE_MAC(10_6);
 
+/* canRepresentDisplayGamut: returns YES if the colorSpace of the receiving window, and the colorSpace of the screen containing that window, are capable of representing the given display gamut
+*/
+- (BOOL)canRepresentDisplayGamut:(NSDisplayGamut)displayGamut  NS_AVAILABLE_MAC(10_12);
+
 /* windowNumbersWithOptions: returns an autoreleased array of NSNumbers containing windowNumbers for all visible windows satisfying options.  If no options are specified, only visible windows belonging to the calling application and on the active space are included.  If options include NSWindowNumberListAllApplications, visible windows belonging to all applications are included.  If options include NSWindowNumberListAllSpaces, visible windows on all spaces are included.  Windows on the active space are returned in z-order.  
    Examples: 
       To get an array of windowNumbers visible on the current space and belonging to the calling application:  

```
