#AppKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKit.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKit.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKit.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKit.h	2016-06-29 03:31:49.000000000 +0200
@@ -112,6 +112,7 @@
 #import <AppKit/NSSliderCell.h>
 #import <AppKit/NSSpellProtocol.h>
 #import <AppKit/NSStackView.h>
+#import <AppKit/NSGridView.h>
 #import <AppKit/NSText.h>
 #import <AppKit/NSTextField.h>
 #import <AppKit/NSTextFieldCell.h>
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
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButtonCell.h	2016-06-29 03:31:49.000000000 +0200
@@ -12,42 +12,32 @@
 @class NSAttributedString, NSFont, NSImage, NSSound;
 
 typedef NS_ENUM(NSUInteger, NSButtonType) {
-    NSMomentaryLightButton		= 0,	// was NSMomentaryPushButton
-    NSPushOnPushOffButton		= 1,
-    NSToggleButton			= 2,
-    NSSwitchButton			= 3,
-    NSRadioButton			= 4,
-    NSMomentaryChangeButton		= 5,
-    NSOnOffButton			= 6,
-    NSMomentaryPushInButton		= 7,	// was NSMomentaryLight
-    NSAcceleratorButton NS_ENUM_AVAILABLE_MAC(10_10_3)			= 8,
-    NSMultiLevelAcceleratorButton NS_ENUM_AVAILABLE_MAC(10_10_3)	= 9,
-    
-    /* These constants were accidentally reversed so that NSMomentaryPushButton lit and
-       NSMomentaryLight pushed. These names are now deprecated */
-    NSMomentaryPushButton NS_ENUM_DEPRECATED_MAC(10_0, 10_9)    = 0, // NSMomentaryLightButton should be used instead
-    NSMomentaryLight NS_ENUM_DEPRECATED_MAC(10_0, 10_9)         = 7 // NSMomentaryPushInButton should be used instead
+    NSButtonTypeMomentaryLight    = 0,
+    NSButtonTypePushOnPushOff     = 1,
+    NSButtonTypeToggle            = 2,
+    NSButtonTypeSwitch            = 3,
+    NSButtonTypeRadio             = 4,
+    NSButtonTypeMomentaryChange   = 5,
+    NSButtonTypeOnOff             = 6,
+    NSButtonTypeMomentaryPushIn   = 7,
+    NSButtonTypeAccelerator NS_ENUM_AVAILABLE_MAC(10_10_3) = 8,
+    NSButtonTypeMultiLevelAccelerator NS_ENUM_AVAILABLE_MAC(10_10_3) = 9,
 };
 
 typedef NS_ENUM(NSUInteger, NSBezelStyle) {
-    NSRoundedBezelStyle          = 1,
-    NSRegularSquareBezelStyle    = 2,
-    NSThickSquareBezelStyle      = 3,
-    NSThickerSquareBezelStyle    = 4,
-    NSDisclosureBezelStyle       = 5,
-    NSShadowlessSquareBezelStyle = 6,
-    NSCircularBezelStyle         = 7,
-    NSTexturedSquareBezelStyle   = 8,
-    NSHelpButtonBezelStyle       = 9,
-    NSSmallSquareBezelStyle       = 10,
-    NSTexturedRoundedBezelStyle   = 11,
-    NSRoundRectBezelStyle         = 12,
-    NSRecessedBezelStyle          = 13,
-    NSRoundedDisclosureBezelStyle = 14,
-    // The inline bezel style contains a solid round-rect border background. It can be used to create an "unread" indicator in an outline view, or another inline button in a tableview, such as a stop progress button in a download panel. Use text for an unread indicator, and a template image for other buttons.
-    NSInlineBezelStyle NS_ENUM_AVAILABLE_MAC(10_7) = 15,
-    
-    NSSmallIconButtonBezelStyle NS_ENUM_DEPRECATED_MAC(10_0, 10_0) = 2 // This bezel style is obsolete and should not be used.
+    NSBezelStyleRounded           = 1,
+    NSBezelStyleRegularSquare     = 2,
+    NSBezelStyleDisclosure        = 5,
+    NSBezelStyleShadowlessSquare  = 6,
+    NSBezelStyleCircular          = 7,
+    NSBezelStyleTexturedSquare    = 8,
+    NSBezelStyleHelpButton        = 9,
+    NSBezelStyleSmallSquare       = 10,
+    NSBezelStyleTexturedRounded   = 11,
+    NSBezelStyleRoundRect         = 12,
+    NSBezelStyleRecessed          = 13,
+    NSBezelStyleRoundedDisclosure = 14,
+    NSBezelStyleInline NS_ENUM_AVAILABLE_MAC(10_7) = 15,
 };
 
 typedef struct __BCFlags {
@@ -78,9 +68,15 @@
     unsigned int        isDrawingFocus:1;
     unsigned int        allowTitleTightening:1;
     unsigned int        imageHugsTitle:1;
-    unsigned int        __reserved:5;
+    unsigned int        shouldNotHighlightOnPerformClick:1;
+    unsigned int        leadingOrTrailing:1;
+    unsigned int        alwaysRadioExclusive:1;
+    unsigned int        __reserved:2;
 #else
-    unsigned int        __reserved:5;
+    unsigned int        __reserved:2;
+    unsigned int        alwaysRadioExclusive:1;
+    unsigned int        leadingOrTrailing:1;
+    unsigned int        shouldNotHighlightOnPerformClick:1;
     unsigned int        imageHugsTitle:1;
     unsigned int        allowTitleTightening:1;
     unsigned int        isDrawingFocus:1;
@@ -128,8 +124,7 @@
 #endif
 } _BCFlags2;
 
-@interface NSButtonCell : NSActionCell
-{
+@interface NSButtonCell : NSActionCell {
     /*All instance variables are private*/
     NSString	       *_altContents;
     id			_sound;
@@ -172,18 +167,8 @@
 
 @end
 
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
 
-/* In 10.8 and higher, all the *Mnemonic* methods are deprecated. On MacOS they have typically not been used.
- */
-@interface NSButtonCell(NSKeyboardUI)
+// Deprecations
+
+typedef NS_ENUM(NSUInteger, NSGradientType) {
+    NSGradientNone          = 0,
+    NSGradientConcaveWeak   = 1,
+    NSGradientConcaveStrong = 2,
+    NSGradientConvexWeak    = 3,
+    NSGradientConvexStrong  = 4
+} NS_DEPRECATED_MAC(10_0, 10_12);
+
+// The following NSButtonType constants will be deprecated in a future release. Please migrate to the modern equivalents.
+static const NSButtonType NSMomentaryLightButton = NSButtonTypeMomentaryLight;
+static const NSButtonType NSPushOnPushOffButton = NSButtonTypePushOnPushOff;
+static const NSButtonType NSToggleButton = NSButtonTypeToggle;
+static const NSButtonType NSSwitchButton = NSButtonTypeSwitch;
+static const NSButtonType NSRadioButton = NSButtonTypeRadio;
+static const NSButtonType NSMomentaryChangeButton = NSButtonTypeMomentaryChange;
+static const NSButtonType NSOnOffButton = NSButtonTypeOnOff;
+static const NSButtonType NSMomentaryPushInButton = NSButtonTypeMomentaryPushIn;
+static const NSButtonType NSAcceleratorButton = NSButtonTypeAccelerator;
+static const NSButtonType NSMultiLevelAcceleratorButton = NSButtonTypeMultiLevelAccelerator;
+
+/* These constants were accidentally reversed so that NSMomentaryPushButton lit and NSMomentaryLight pushed. These names are now deprecated */
+static const NSButtonType NSMomentaryPushButton NS_ENUM_DEPRECATED_MAC(10_0, 10_9, "This constant is misnamed and has the same effect as NSButtonTypeMomentaryLight. Use that name instead, or switch to NSButtonTypeMomentaryPushIn.") = NSButtonTypeMomentaryLight;
+static const NSButtonType NSMomentaryLight NS_ENUM_DEPRECATED_MAC(10_0, 10_9, "This constant is misnamed and has the same effect as NSButtonTypeMomentaryPushIn. Use that name instead, or switch to NSButtonTypeMomentaryLight.") = NSButtonTypeMomentaryPushIn;
+
+// The following NSBezelStyle constants will be deprecated in a future release. Please migrate to the modern equivalents.
+static const NSBezelStyle NSRoundedBezelStyle = NSBezelStyleRounded;
+static const NSBezelStyle NSRegularSquareBezelStyle = NSBezelStyleRegularSquare;
+static const NSBezelStyle NSDisclosureBezelStyle = NSBezelStyleDisclosure;
+static const NSBezelStyle NSShadowlessSquareBezelStyle = NSBezelStyleShadowlessSquare;
+static const NSBezelStyle NSCircularBezelStyle = NSBezelStyleCircular;
+static const NSBezelStyle NSTexturedSquareBezelStyle = NSBezelStyleTexturedSquare;
+static const NSBezelStyle NSHelpButtonBezelStyle = NSBezelStyleHelpButton;
+static const NSBezelStyle NSSmallSquareBezelStyle = NSBezelStyleSmallSquare;
+static const NSBezelStyle NSTexturedRoundedBezelStyle = NSBezelStyleTexturedRounded;
+static const NSBezelStyle NSRoundRectBezelStyle = NSBezelStyleRoundRect;
+static const NSBezelStyle NSRecessedBezelStyle = NSBezelStyleRecessed;
+static const NSBezelStyle NSRoundedDisclosureBezelStyle = NSBezelStyleRoundedDisclosure;
+static const NSBezelStyle NSInlineBezelStyle = NSBezelStyleInline;
+
+static const NSBezelStyle NSSmallIconButtonBezelStyle NS_ENUM_DEPRECATED_MAC(10_0, 10_0, "This bezel style is obsolete and should not be used.") = (NSBezelStyle)2;
+static const NSBezelStyle NSThickSquareBezelStyle API_DEPRECATED_WITH_REPLACEMENT("NSBezelStyleRegularSquare", macosx(10.0, 10.12)) = (NSBezelStyle)3;
+static const NSBezelStyle NSThickerSquareBezelStyle API_DEPRECATED_WITH_REPLACEMENT("NSBezelStyleRegularSquare", macosx(10.0, 10.12)) = (NSBezelStyle)4;
+
+@interface NSButtonCell(NSDeprecated)
+
+@property NSGradientType gradientType NS_DEPRECATED_MAC(10_0, 10_12, "The gradientType property is unused, and setting it has no effect.");
 
-/* On 10.8, these two methods still will call setTitle: (or setAlternateTitle:) with the ampersand stripped from stringWithAmpersand, but does nothing else. Use setTitle directly.
- */
+// On 10.8, these two methods still will call setTitle: (or setAlternateTitle:) with the ampersand stripped from stringWithAmpersand, but does nothing else. Use setTitle directly.
 - (void)setTitleWithMnemonic:(null_unspecified NSString *)stringWithAmpersand NS_DEPRECATED_MAC(10_0, 10_8);
 - (void)setAlternateTitleWithMnemonic:(null_unspecified NSString *)stringWithAmpersand NS_DEPRECATED_MAC(10_0, 10_8);
 
-/* This method no longer does anything and should not be called.
- */
-- (void)setAlternateMnemonicLocation:(NSUInteger)location NS_DEPRECATED_MAC(10_0, 10_8);
+// This method no longer does anything and should not be called.
+- (void)setAlternateMnemonicLocation:(NSUInteger)location NS_DEPRECATED_MAC(10_0, 10_8, "This method is obsolete. Calling it has no effect.");
 
-/* On 10.8, alternateMnemonicLocation now always returns NSNotFound.
- */
+// On 10.8, alternateMnemonicLocation now always returns NSNotFound.
 - (NSUInteger)alternateMnemonicLocation NS_DEPRECATED_MAC(10_0, 10_8);
 
 - (null_unspecified NSString *)alternateMnemonic NS_DEPRECATED_MAC(10_0, 10_8);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCell.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCell.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCell.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCell.h	2016-06-29 03:31:49.000000000 +0200
@@ -47,13 +47,15 @@
 
 
 typedef NS_ENUM(NSUInteger, NSCellImagePosition) {
-    NSNoImage				= 0,
-    NSImageOnly				= 1,
-    NSImageLeft				= 2,
-    NSImageRight			= 3,
-    NSImageBelow			= 4,
-    NSImageAbove			= 5,
-    NSImageOverlaps			= 6
+    NSNoImage                           = 0,
+    NSImageOnly                         = 1,
+    NSImageLeft                         = 2,
+    NSImageRight                        = 3,
+    NSImageBelow                        = 4,
+    NSImageAbove                        = 5,
+    NSImageOverlaps                     = 6,
+    NSImageLeading  API_AVAILABLE(macosx(10.12)) = 7,
+    NSImageTrailing API_AVAILABLE(macosx(10.12)) = 8
 };
 
 
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
 
-/* ButtonCell highlightsBy and showsStateBy mask */
+/* NSButtonCell highlightsBy and showsStateBy mask */
 typedef NS_OPTIONS(NSUInteger, NSCellStyleMask) {
     NSNoCellMask			= 0,
     NSContentsCellMask			= 1,
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
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionView.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionView.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionView.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionView.h	2016-06-29 03:31:50.000000000 +0200
@@ -170,8 +170,9 @@
         unsigned int observingClipFrameChanges:1;
         unsigned int allowsSectionDrop:1;
         unsigned int backgroundViewScrollsWithContent:1;
+        unsigned int opensGaps:1;
         unsigned int visMode:1;
-        unsigned int reserved:12;
+        unsigned int reserved:11;
     } _cvFlags;
     id _delegate;
     NSMutableArray *_backgroundLayers;
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
@@ -44,10 +65,9 @@
 
 @property BOOL completes;
 
-- (nullable id <NSComboBoxDelegate>)delegate;
-- (void)setDelegate:(nullable id <NSComboBoxDelegate>)delegate;
+@property (nullable, assign) id<NSComboBoxDelegate> delegate;
 
-/* These two methods can only be used when usesDataSource is YES */
+/* The dataSource will only be used when usesDataSource is YES */
 @property (nullable, assign) id<NSComboBoxDataSource> dataSource;
 
 /* These methods can only be used when usesDataSource is NO */
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFilePromiseProvider.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFilePromiseProvider.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFilePromiseProvider.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFilePromiseProvider.h	2016-06-29 03:31:50.000000000 +0200
@@ -55,7 +55,7 @@
 @optional
 /* Write the contents of this promise item to the provided URL and call completionHandler when done. NSFilePromiseReceiver automatically wraps this message with NSFileCoordinator when the promise destination is an NSFilePromiseReceiver. As such, the URL may be different than expected. Note: This request shall occur on the NSOperationQueue supplied by -promiseOperationQueue.
  */
-- (void)filePromiseProvider:(NSFilePromiseProvider*)filePromiseProvider writePromiseToURL:(NSURL *)url completionHandler:(void (^)(NSError *errorOrNil))completionHandler;
+- (void)filePromiseProvider:(NSFilePromiseProvider*)filePromiseProvider writePromiseToURL:(NSURL *)url completionHandler:(void (^)(NSError * __nullable errorOrNil))completionHandler;
 
 /* The operation queue that the write request will be issued from. If this method is not implemented, the mainOperationQueue is used. */
 - (NSOperationQueue *)promiseOperationQueueForFilePromiseProvider:(NSFilePromiseProvider*)filePromiseProvider;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFilePromiseReceiver.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFilePromiseReceiver.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFilePromiseReceiver.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFilePromiseReceiver.h	2016-06-29 03:31:50.000000000 +0200
@@ -28,7 +28,7 @@
     NSInteger _promiseType;
     void (^_readerBlock)(NSURL *, NSError * __nullable);
     struct {
-        unsigned int usesFileCoordniation:1;
+        unsigned int usesFileCoordination:1;
         unsigned int registered:1;
         unsigned int reserved:30;
     } _flags;
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGridView.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGridView.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGridView.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGridView.h	2016-06-29 03:31:50.000000000 +0200
@@ -56,6 +56,7 @@
     NSMutableArray *_columns;
     NSMutableArray *_rows;
     NSMapTable *_cellTable;
+    NSInteger _currentConstraintGeneration;
     
     id  _reserved __unused;
     id  _reserved2 __unused;
@@ -122,6 +123,7 @@
     
     NSGridCellPlacement _yPlacement;
     NSGridRowAlignment _rowAlignment;
+    NSInteger _hasContentInGeneration;
 
     CGFloat _height;
     CGFloat _topPadding;
@@ -159,6 +161,7 @@
     id  _reserved2 __unused;
     id  _reserved3 __unused;
     
+    NSInteger _hasContentInGeneration;
     NSGridCellPlacement _xPlacement;
     CGFloat _width;
     CGFloat _trailingPadding;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImage.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImage.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImage.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImage.h	2016-06-29 03:31:49.000000000 +0200
@@ -317,12 +317,17 @@
 APPKIT_EXTERN NSString * const NSImageNameLockLockedTemplate NS_AVAILABLE_MAC(10_5);
 APPKIT_EXTERN NSString * const NSImageNameLockUnlockedTemplate NS_AVAILABLE_MAC(10_5);
 
-/* Use these images for "go forward" or "go back" functions, as seen in Safari's toolbar.  See also the right and left facing triangle images.
+/* Use these images for "go forward" or "go back" functions, as seen in Safari's toolbar.  These images will automatically mirror when the user interface layout direction is right to left.
  */
-APPKIT_EXTERN NSString * const NSImageNameGoRightTemplate NS_AVAILABLE_MAC(10_5); 
-APPKIT_EXTERN NSString * const NSImageNameGoLeftTemplate NS_AVAILABLE_MAC(10_5); 
+APPKIT_EXTERN NSString * const NSImageNameGoForwardTemplate NS_AVAILABLE_MAC(10_12);
+APPKIT_EXTERN NSString * const NSImageNameGoBackTemplate NS_AVAILABLE_MAC(10_12);
 
-/* Prefer the "GoLeft" and "GoRight" images for situations where they apply.  These generic triangles aren't endorsed for any particular use, but you can use them if you don't have any better art.
+/* These images are like GoForward and GoBack except that they always point in the specified direction regardless of layout direction.  See also the right and left facing triangle images.
+ */
+APPKIT_EXTERN NSString * const NSImageNameGoRightTemplate NS_AVAILABLE_MAC(10_5);
+APPKIT_EXTERN NSString * const NSImageNameGoLeftTemplate NS_AVAILABLE_MAC(10_5);
+
+/* Prefer the GoForward and GoBack or GoLeft and GoRight images for situations where they apply.  These generic triangles aren't endorsed for any particular use, but you can use them if you don't have any better art.
  */
 APPKIT_EXTERN NSString * const NSImageNameRightFacingTriangleTemplate NS_AVAILABLE_MAC(10_5);
 APPKIT_EXTERN NSString * const NSImageNameLeftFacingTriangleTemplate NS_AVAILABLE_MAC(10_5);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenuItem.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenuItem.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenuItem.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenuItem.h	2016-06-29 03:31:49.000000000 +0200
@@ -10,6 +10,7 @@
 #import <AppKit/AppKitDefines.h>
 #import <AppKit/NSUserInterfaceValidation.h>
 #import <AppKit/NSView.h>
+#import <AppKit/NSCell.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -102,7 +103,7 @@
 
 @property (nullable, strong) NSImage *image;
 
-@property NSInteger state;
+@property NSInteger /* NSControlState */ state;
 @property (null_resettable, strong) NSImage *onStateImage; // checkmark by default
 @property (nullable, strong) NSImage *offStateImage; // none by default
 @property (null_resettable, strong) NSImage *mixedStateImage; // horizontal line by default?
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenGLView.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenGLView.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenGLView.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenGLView.h	2016-06-29 03:31:49.000000000 +0200
@@ -51,7 +51,7 @@
 
 @interface NSView (NSExtendedDynamicRange)
 
-/* If any view on the screen has this enabled, the NSScreen which the OpenGL surface is on may have its maximumExtendedDynamicRangeColorComponentValue increased.  When composited by the Window Server, color values rendered by this OpenGL surface will be clamped to the NSScreen’s maximumExtendedDynamicRangeColorComponentValue rather than 1.0.
+/* When set to YES on a view with an attached OpenGL context, the NSScreen in which that views resides may have its maximumExtendedDynamicRangeColorComponentValue increased.  When composited by the Window Server, color values rendered by this OpenGL surface will be clamped to the NSScreen’s maximumExtendedDynamicRangeColorComponentValue rather than 1.0.
  */
 @property BOOL wantsExtendedDynamicRangeOpenGLSurface NS_AVAILABLE_MAC(10_11);
 
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSharingService.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSharingService.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSharingService.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSharingService.h	2016-06-29 03:31:50.000000000 +0200
@@ -139,7 +139,7 @@
 /* The following methods are invoked when the service is performed and the sharing window pops up, to present a transition between the original items and the sharing window.
  */
 - (NSRect)sharingService:(NSSharingService *)sharingService sourceFrameOnScreenForShareItem:(id)item;
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_APPKIT_EPOCH) && SWIFT_SDK_OVERLAY_APPKIT_EPOCH >= 6)
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_APPKIT_EPOCH) && SWIFT_SDK_OVERLAY_APPKIT_EPOCH >= 1)
 /* When non-nil, the image returned would be used for the transitioning animation. When nil, the transitioning animation is disabled.
  */
 - (nullable NSImage *)sharingService:(NSSharingService *)sharingService transitionImageForShareItem:(id)item contentRect:(NSRect *)contentRect;
@@ -150,7 +150,7 @@
 
 /* The following method is invoked when the service is performed and wants to display its contents in a popover. The delegate should return the view that will act as the anchor of the popover, along with the target rectangle within the bounds of that view and preferred edge of that rectangle for the popover to appear. The delegate may also return nil, indicating that there is no anchoring view currently available, in which case the service may attempt to display the service via some other means.
  
- The service named NSSharingServiceNameCloudSharing prefers to display itself using a popover anchored to an "iCloud Sharing" or "Share" button. If no such button is available or visible, return nil.
+ The service named NSSharingServiceNameCloudSharing prefers to display itself using a popover anchored to an "Add People" or "Share" button. If no such button is available or visible, return nil.
  */
 - (nullable NSView *)anchoringViewForSharingService:(NSSharingService *)sharingService showRelativeToRect:(NSRect *)positioningRect preferredEdge:(NSRectEdge *)preferredEdge;
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSliderCell.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSliderCell.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSliderCell.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSliderCell.h	2016-06-29 03:31:49.000000000 +0200
@@ -43,7 +43,8 @@
         unsigned int snappedToPreviousValue:1;
         unsigned int snappedToDefaultValue:1;
         unsigned int snappingAllowed:1;
-        unsigned int reserved2:19;
+        unsigned int collapseOnResize:1;
+        unsigned int reserved2:18;
     } _scFlags;
 }
 
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
@@ -35,7 +50,11 @@
     id	_tabViewItems;                          	// array of NSTabViewItem
     NSTabViewItem	*_selectedTabViewItem;		// nil only if _tabViewItems is empty
     NSFont		*_font;				// font use to display the tab label
-    NSTabViewType	_tabViewType;
+    struct __NSTabViewTypeFlags {
+        unsigned int tabViewBorderType:3;
+        unsigned int tabPosition:5;
+        unsigned int reserved:24;
+    } _typeFlags;
     BOOL		_allowTruncatedLabels;
     id                  _delegate;
 
@@ -75,7 +94,8 @@
         unsigned int ownedByTabViewController:1;
         unsigned int reserved:19;
     } _flags;
-    NSTabViewItem 	*_focusedTabViewItem;			
+    NSTabViewItem 	*_focusedTabViewItem;
+
     void		*_tabViewUnused2 __unused;
 }
 
@@ -83,7 +103,7 @@
 
 - (void)selectTabViewItem:(nullable NSTabViewItem *)tabViewItem;
 - (void)selectTabViewItemAtIndex:(NSInteger)index;				// May raise an NSRangeException
-- (void)selectTabViewItemWithIdentifier:(id)identifier;			// May raise an NSRangeException if identifier not found
+- (void)selectTabViewItemWithIdentifier:(id)identifier;                         // May raise an NSRangeException if identifier not found
 - (void)takeSelectedTabViewItemFromSender:(nullable id)sender;			// May raise an NSRangeException
 
 	/* Navigation */
@@ -95,12 +115,14 @@
 
 	/* Getters */
 
-@property (nullable, readonly, strong) NSTabViewItem *selectedTabViewItem;					// return nil if none are selected
-@property (strong) NSFont *font;							// returns font used for all tab labels.
-@property NSTabViewType tabViewType;
+@property (nullable, readonly, strong) NSTabViewItem *selectedTabViewItem;	// return nil if none are selected
+@property (strong) NSFont *font;						// returns font used for all tab labels.
+@property NSTabViewType tabViewType;                                            // Use tabPosition and tabViewBorderType instead. Setting this will also set the tabPosition and tabViewBorderType. Setting tabPosition or tabViewBorderType will affect tabViewType
+@property NSTabPosition tabPosition;
+@property NSTabViewBorderType tabViewBorderType;                                // This will only be respected if NSTabPosition is NSTabPositionNone.
 @property (readonly, copy) NSArray<__kindof NSTabViewItem *> *tabViewItems;
 @property BOOL allowsTruncatedLabels;
-@property (readonly) NSSize minimumSize;							// returns the minimum size of the tab view
+@property (readonly) NSSize minimumSize;					// returns the minimum size of the tab view
 @property BOOL drawsBackground;  						// only relevant for borderless tab view type
 @property NSControlTint controlTint;
 @property NSControlSize controlSize;
@@ -108,7 +130,7 @@
 	/* Add/Remove tabs */
 
 - (void)addTabViewItem:(NSTabViewItem *)tabViewItem;				// Add tab at the end.
-- (void)insertTabViewItem:(NSTabViewItem *)tabViewItem atIndex:(NSInteger)index;	// May raise an NSRangeException
+- (void)insertTabViewItem:(NSTabViewItem *)tabViewItem atIndex:(NSInteger)index;// May raise an NSRangeException
 - (void)removeTabViewItem:(NSTabViewItem *)tabViewItem;				// tabViewItem must be an existing tabViewItem
 
 	/* Delegate */
@@ -121,13 +143,13 @@
 
 	/* Geometry */
 
-@property (readonly) NSRect contentRect;							// Return the rect available for a "page". 
+@property (readonly) NSRect contentRect;					// Return the rect available for a "page".
 
 	/* Query */
 
 @property (readonly) NSInteger numberOfTabViewItems;
 - (NSInteger)indexOfTabViewItem:(NSTabViewItem *)tabViewItem;			// NSNotFound if not found
-- (NSTabViewItem *)tabViewItemAtIndex:(NSInteger)index;			// May raise an NSRangeException	
+- (NSTabViewItem *)tabViewItemAtIndex:(NSInteger)index;                         // May raise an NSRangeException	
 - (NSInteger)indexOfTabViewItemWithIdentifier:(id)identifier;			// NSNotFound if not found
 
 @end
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableView.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableView.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableView.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableView.h	2016-06-29 03:31:49.000000000 +0200
@@ -111,7 +111,7 @@
     
     /* The table will use a row height specified for a small/medium or large table.
      It is required that all sizes be fully tested and supported if NSTableViewRowSizeStyleCustom is not used.
-     Some standard Aqua metrics may be applied to cells based on the current size. */
+     Some standard Aqua metrics may be applied to cells based on the current size. Specifically, the metrics will be applied to the NSTableCellView's textField and imageView outlets. Don't use these and add your own outlets if you wish to control the metrics yourself. */
     NSTableViewRowSizeStyleSmall = 1,
     NSTableViewRowSizeStyleMedium = 2,
     NSTableViewRowSizeStyleLarge = 3,
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableViewRowAction.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableViewRowAction.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableViewRowAction.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableViewRowAction.h	2016-06-29 03:31:49.000000000 +0200
@@ -27,8 +27,8 @@
     NSColor *_backgroundColor;
 #ifndef __OBJC2__
     unsigned int _flags:32;
-    id _reserved;
 #endif
+    NSImage *_image;
 }
 
 + (instancetype)rowActionWithStyle:(NSTableViewRowActionStyle)style title:(NSString *)title handler:(void (^)(NSTableViewRowAction *action, NSInteger row))handler;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextField.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextField.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextField.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextField.h	2016-06-29 03:31:49.000000000 +0200
@@ -72,7 +72,7 @@
 + (instancetype)wrappingLabelWithString:(NSString *)stringValue NS_SWIFT_NAME(init(wrappingLabelWithString:)) NS_AVAILABLE_MAC(10_12);
 
 /*!
- Creates a non-editable, selectable text field that displays attributed text.
+ Creates a non-editable, non-selectable text field that displays attributed text.
  The line break mode of this field is determined by the attributed string's NSParagraphStyle attribute.
  @param attributedStringValue The attributed string to display in the field.
  @return An initialized text field object.
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSViewController.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSViewController.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSViewController.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSViewController.h	2016-06-29 03:31:50.000000000 +0200
@@ -57,7 +57,8 @@
     unsigned int _viewIsAppearing:1;
     unsigned int _delayViewDidAppear:1;
     unsigned int _isContentViewController:1;
-    unsigned int _reserved:29 __unused;
+    unsigned int _shouldDirtyLayoutOnSizeChanges:1;
+    unsigned int _reserved:28 __unused;
 }
 
 /* The designated initializer. The specified nib should typically have the class of the file's owner set to NSViewController, or a subclass of yours, with the "view" outlet connected to a view. If you pass in a nil nib name then -nibName will return nil. -loadView can be used to assign a view before -view is invoked. If you pass in a nil bundle then -nibBundle will return nil and -loadView will interpret it using the same rules as -[NSNib initWithNibNamed:bundle:].
@@ -154,7 +155,7 @@
 */
 - (void)dismissViewController:(NSViewController *)viewController NS_AVAILABLE_MAC(10_10);
 
-/* Dismisses the ViewController.  If the presenter is a ViewController, it will be sent a -dismissViewController: message with this ViewController as the parameter.  Does nothing if the receiver is not currently presented.
+/* Dismisses the receiver.  If the receiver’s presenter is an NSViewController, it will be sent a -dismissViewController: message with this receiver as the parameter.  Does nothing if the receiver is not currently presented.
 */
 - (IBAction)dismissController:(nullable id)sender NS_AVAILABLE_MAC(10_10);
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSVisualEffectView.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSVisualEffectView.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSVisualEffectView.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSVisualEffectView.h	2016-06-29 03:31:50.000000000 +0200
@@ -54,11 +54,13 @@
     struct NSVisualEffectViewInternal *_NSVisualEffectViewInternal;
     
 #if !__LP64__
-    uint8_t _reserved[48];
+    uint8_t _reserved[40];
 #endif
     CALayer *_darkenLayer;
     CALayer *_maskLayer;
     CALayer *_clearCopyLayer;
+    CALayer *_backdropLayer;
+    CALayer *_backdropLayerForMask;
     
     unsigned int _dirty:1;
     unsigned int _hasMask:1;
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