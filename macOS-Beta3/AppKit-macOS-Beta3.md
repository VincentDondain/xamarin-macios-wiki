#AppKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKit.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKit.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKit.h	2016-06-29 03:31:49.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKit.h	2016-07-11 05:26:54.000000000 +0200
@@ -230,3 +230,4 @@
 #import <AppKit/NSAlignmentFeedbackFilter.h>
 #import <AppKit/NSHapticFeedback.h>
 #import <AppKit/NSPressureConfiguration.h>
+#import <AppKit/AppKitLegacySwiftCompatibility.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitDefines.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitDefines.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitDefines.h	2016-06-29 03:31:49.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitDefines.h	2016-07-11 05:26:54.000000000 +0200
@@ -21,6 +21,8 @@
 #define AVAILABLE_MAC_OS_X_VERSION_10_7_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_7 DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER
 #endif
 
+#define APPKIT_SWIFT_SDK_EPOCH_AT_LEAST(__epoch__) (!defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_APPKIT_EPOCH) && SWIFT_SDK_OVERLAY_APPKIT_EPOCH >= __epoch__))
+
 //
 //  Platform specific defs for externs
 //
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitLegacySwiftCompatibility.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitLegacySwiftCompatibility.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitLegacySwiftCompatibility.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitLegacySwiftCompatibility.h	2016-07-11 05:26:54.000000000 +0200
@@ -0,0 +1,118 @@
+/*
+        AppKitLegacySwiftCompatibility.h
+        Application Kit
+        Copyright (c) 2016, Apple Inc.
+        All rights reserved.
+*/
+
+/* This header and its contents should only be used within AppKit headers. */
+
+#import <AppKit/NSImage.h>
+#import <AppKit/NSOpenGL.h>
+#import <AppKit/NSColor.h>
+#import <AppKit/NSColorSpace.h>
+
+
+NS_ASSUME_NONNULL_BEGIN
+
+#if !NS_IMAGE_DECLARES_DESIGNATED_INITIALIZERS
+
+@interface NSImage ()
+
+- (instancetype)initWithSize:(NSSize)size;
+
+@end
+
+#endif
+
+#if !NS_OPENGL_PIXEL_FORMAT_DECLARES_DESIGNATED_INITIALIZERS
+
+@interface NSOpenGLPixelFormat ()
+
+- (nullable NSOpenGLPixelFormat *)initWithCGLPixelFormatObj:(struct _CGLPixelFormatObject *)format NS_AVAILABLE_MAC(10_6);
+
+@end
+
+#endif
+
+#if !NSCOLOR_USE_CLASS_PROPERTIES
+// Older declarations for APIs that have been converted into class properties in 10.12
+@interface NSColor (NSColorLegacyDeclarationsForClassProperties)
++ (NSColor *)blackColor;
++ (NSColor *)darkGrayColor;
++ (NSColor *)lightGrayColor;
++ (NSColor *)whiteColor;
++ (NSColor *)grayColor;
++ (NSColor *)redColor;
++ (NSColor *)greenColor;
++ (NSColor *)blueColor;
++ (NSColor *)cyanColor;
++ (NSColor *)yellowColor;
++ (NSColor *)magentaColor;
++ (NSColor *)orangeColor;
++ (NSColor *)purpleColor;
++ (NSColor *)brownColor;
++ (NSColor *)clearColor;
++ (NSColor *)controlShadowColor;
++ (NSColor *)controlDarkShadowColor;
++ (NSColor *)controlColor;
++ (NSColor *)controlHighlightColor;
++ (NSColor *)controlLightHighlightColor;
++ (NSColor *)controlTextColor;
++ (NSColor *)controlBackgroundColor;
++ (NSColor *)selectedControlColor;
++ (NSColor *)secondarySelectedControlColor;
++ (NSColor *)selectedControlTextColor;
++ (NSColor *)disabledControlTextColor;
++ (NSColor *)textColor;
++ (NSColor *)textBackgroundColor;
++ (NSColor *)selectedTextColor;
++ (NSColor *)selectedTextBackgroundColor;
++ (NSColor *)gridColor;
++ (NSColor *)keyboardFocusIndicatorColor;
++ (NSColor *)windowBackgroundColor;
++ (NSColor *)underPageBackgroundColor NS_AVAILABLE_MAC(10_8);
++ (NSColor *)labelColor NS_AVAILABLE_MAC(10_10);
++ (NSColor *)secondaryLabelColor NS_AVAILABLE_MAC(10_10);
++ (NSColor *)tertiaryLabelColor NS_AVAILABLE_MAC(10_10);
++ (NSColor *)quaternaryLabelColor NS_AVAILABLE_MAC(10_10);
++ (NSColor *)scrollBarColor;
++ (NSColor *)knobColor;
++ (NSColor *)selectedKnobColor;
++ (NSColor *)windowFrameColor;
++ (NSColor *)windowFrameTextColor;
++ (NSColor *)selectedMenuItemColor;
++ (NSColor *)selectedMenuItemTextColor;
++ (NSColor *)highlightColor;
++ (NSColor *)shadowColor;
++ (NSColor *)headerColor;
++ (NSColor *)headerTextColor;
++ (NSColor *)alternateSelectedControlColor;
++ (NSColor *)alternateSelectedControlTextColor;
++ (NSArray<NSColor *> *)controlAlternatingRowBackgroundColors;
++ (NSControlTint)currentControlTint;
++ (void)setIgnoresAlpha:(BOOL)flag;
++ (BOOL)ignoresAlpha;
+@end
+#endif
+
+#if !NSCOLORSPACE_USE_CLASS_PROPERTIES
+// Older declarations for APIs that have been converted into class properties in 10.12
+@interface NSColorSpace (NSColorSpaceLegacyDeclarationsForClassProperties)
++ (NSColorSpace *)sRGBColorSpace NS_AVAILABLE_MAC(10_5);
++ (NSColorSpace *)genericGamma22GrayColorSpace NS_AVAILABLE_MAC(10_6);
++ (NSColorSpace *)extendedSRGBColorSpace NS_AVAILABLE_MAC(10_12);
++ (NSColorSpace *)extendedGenericGamma22GrayColorSpace NS_AVAILABLE_MAC(10_12);
++ (NSColorSpace *)displayP3ColorSpace NS_AVAILABLE_MAC(10_12);
++ (NSColorSpace *)adobeRGB1998ColorSpace NS_AVAILABLE_MAC(10_5);
++ (NSColorSpace *)genericRGBColorSpace;
++ (NSColorSpace *)genericGrayColorSpace;
++ (NSColorSpace *)genericCMYKColorSpace;
++ (NSColorSpace *)deviceRGBColorSpace;
++ (NSColorSpace *)deviceGrayColorSpace;
++ (NSColorSpace *)deviceCMYKColorSpace;
+@end
+#endif
+
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButton.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButton.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButton.h	2016-06-29 03:31:49.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButton.h	2016-07-11 05:26:54.000000000 +0200
@@ -20,10 +20,11 @@
 @property (nullable, strong) NSImage *image;
 @property (nullable, strong) NSImage *alternateImage;
 @property NSCellImagePosition imagePosition;
+@property NSImageScaling imageScaling NS_AVAILABLE_MAC(10_5);
 @property BOOL imageHugsTitle API_AVAILABLE(macosx(10.12));
 
 - (void)setButtonType:(NSButtonType)type;
-@property NSInteger /* NSControlState */ state;
+@property NSInteger state;
 @property (getter=isBordered) BOOL bordered;
 @property (getter=isTransparent) BOOL transparent;
 - (void)setPeriodicDelay:(float)delay interval:(float)interval;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButtonCell.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButtonCell.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButtonCell.h	2016-06-29 03:31:49.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButtonCell.h	2016-07-11 05:26:54.000000000 +0200
@@ -71,9 +71,11 @@
     unsigned int        shouldNotHighlightOnPerformClick:1;
     unsigned int        leadingOrTrailing:1;
     unsigned int        alwaysRadioExclusive:1;
-    unsigned int        __reserved:2;
+    unsigned int        hasOverlayView:1;
+    unsigned int        __reserved:1;
 #else
-    unsigned int        __reserved:2;
+    unsigned int        __reserved:1;
+    unsigned int        hasOverlayView:1;
     unsigned int        alwaysRadioExclusive:1;
     unsigned int        leadingOrTrailing:1;
     unsigned int        shouldNotHighlightOnPerformClick:1;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCell.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCell.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCell.h	2016-06-29 03:31:49.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCell.h	2016-07-11 05:26:54.000000000 +0200
@@ -70,18 +70,11 @@
     NSScaleNone NS_ENUM_DEPRECATED_MAC(10_0, 10_10, "Use NSImageScaleNone instead")
 } NS_ENUM_AVAILABLE_MAC(10_5);
 
-typedef NS_ENUM(NSInteger, NSControlState) {
-    NSControlStateMixed = -1,
-    NSControlStateOff   =  0,
-    NSControlStateOn    =  1
-};
-typedef NSInteger NSCellStateValue; /* Use NSControlState instead */
-
-// These constants will be deprecated in a future release. Please migrate to the modern typed equivalents.
+typedef NSInteger NSCellStateValue;
 enum {
-    NSMixedState = NSControlStateMixed,
-    NSOffState   = NSControlStateOff,
-    NSOnState    = NSControlStateOn,
+    NSMixedState = -1,
+    NSOffState   =  0,
+    NSOnState    =  1,
 };
 
 /* NSButtonCell highlightsBy and showsStateBy mask */
@@ -186,7 +179,7 @@
 
 @property (nullable, assign) NSView *controlView; // Must be an NSControl subclass, non-control view subclasses not allowed!
 @property NSCellType type;
-@property NSInteger /* NSControlState */ state;
+@property NSInteger state;
 @property (nullable, weak) id target; // Target is weak for zeroing-weak compatible objects in apps linked on 10.10 or later. Otherwise the behavior of this property is 'assign'.
 @property (nullable) SEL action;
 @property NSInteger tag;
@@ -314,7 +307,7 @@
 
 @interface NSCell(NSCellMixedState)	/* allow button to have mixed state value*/
 @property BOOL allowsMixedState;
-@property (readonly) NSInteger /* NSControlState */ nextState;			/* get next state state in cycle */
+@property (readonly) NSInteger nextState;			/* get next state state in cycle */
 - (void)setNextState;			/* toggle/cycle through states */
 @end
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColor.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColor.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColor.h	2016-06-29 03:31:49.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColor.h	2016-07-11 05:26:54.000000000 +0200
@@ -43,6 +43,8 @@
 
 #define NSAppKitVersionNumberWithPatternColorLeakFix 641.0
 
+// By default class properties are enabled and available for Swift 3 and ObjC apps
+#define NSCOLOR_USE_CLASS_PROPERTIES APPKIT_SWIFT_SDK_EPOCH_AT_LEAST(2)
 
 
 @interface NSColor : NSObject <NSCopying, NSSecureCoding, NSPasteboardReading, NSPasteboardWriting>
@@ -97,76 +99,79 @@
 + (nullable NSColor *)colorWithCatalogName:(NSString *)listName colorName:(NSString *)colorName;
 
 
+#if NSCOLOR_USE_CLASS_PROPERTIES
 /* Some convenience methods to create colors in the calibrated color spaces...
-*/
-+ (NSColor *)blackColor;	/* 0.0 white */
-+ (NSColor *)darkGrayColor;	/* 0.333 white */
-+ (NSColor *)lightGrayColor;	/* 0.667 white */
-+ (NSColor *)whiteColor;	/* 1.0 white */
-+ (NSColor *)grayColor;		/* 0.5 white */
-+ (NSColor *)redColor;		/* 1.0, 0.0, 0.0 RGB */
-+ (NSColor *)greenColor;	/* 0.0, 1.0, 0.0 RGB */
-+ (NSColor *)blueColor;		/* 0.0, 0.0, 1.0 RGB */
-+ (NSColor *)cyanColor;		/* 0.0, 1.0, 1.0 RGB */
-+ (NSColor *)yellowColor;	/* 1.0, 1.0, 0.0 RGB */
-+ (NSColor *)magentaColor;	/* 1.0, 0.0, 1.0 RGB */
-+ (NSColor *)orangeColor;	/* 1.0, 0.5, 0.0 RGB */
-+ (NSColor *)purpleColor;	/* 0.5, 0.0, 0.5 RGB */
-+ (NSColor *)brownColor;	/* 0.6, 0.4, 0.2 RGB */
-+ (NSColor *)clearColor;	/* 0.0 white, 0.0 alpha */
-
-+ (NSColor *)controlShadowColor;		// Dark border for controls
-+ (NSColor *)controlDarkShadowColor;		// Darker border for controls
-+ (NSColor *)controlColor;			// Control face and old window background color
-+ (NSColor *)controlHighlightColor;		// Light border for controls
-+ (NSColor *)controlLightHighlightColor;	// Lighter border for controls
-+ (NSColor *)controlTextColor;			// Text on controls
-+ (NSColor *)controlBackgroundColor;		// Background of large controls (browser, tableview, clipview, ...)
-+ (NSColor *)selectedControlColor;		// Control face for selected controls
-+ (NSColor *)secondarySelectedControlColor;	// Color for selected controls when control is not active (that is, not focused)
-+ (NSColor *)selectedControlTextColor;		// Text on selected controls
-+ (NSColor *)disabledControlTextColor;		// Text on disabled controls
-+ (NSColor *)textColor;				// Document text
-+ (NSColor *)textBackgroundColor;		// Document text background
-+ (NSColor *)selectedTextColor;			// Selected document text
-+ (NSColor *)selectedTextBackgroundColor;	// Selected document text background
-+ (NSColor *)gridColor;				// Grids in controls
-+ (NSColor *)keyboardFocusIndicatorColor;// Keyboard focus ring around controls
-+ (NSColor *)windowBackgroundColor;		// Background fill for window contents
-+ (NSColor *)underPageBackgroundColor NS_AVAILABLE_MAC(10_8);   // Background areas revealed behind views
-
-+ (NSColor *)labelColor NS_AVAILABLE_MAC(10_10);            // Text color for static text and related elements
-+ (NSColor *)secondaryLabelColor NS_AVAILABLE_MAC(10_10);   // Text color for secondary static text and related elements
-+ (NSColor *)tertiaryLabelColor NS_AVAILABLE_MAC(10_10);    // Text color for disabled static text and related elements
-+ (NSColor *)quaternaryLabelColor NS_AVAILABLE_MAC(10_10);  // Text color for large secondary or disabled static text, separators, large glyphs/icons, etc
-
-+ (NSColor *)scrollBarColor;			// Scroll bar slot color
-+ (NSColor *)knobColor;     			// Knob face color for controls
-+ (NSColor *)selectedKnobColor;       		// Knob face color for selected controls
-
-+ (NSColor *)windowFrameColor;			// Window frames
-+ (NSColor *)windowFrameTextColor;		// Text on window frames
-
-+ (NSColor *)selectedMenuItemColor;		// Highlight color for menus
-+ (NSColor *)selectedMenuItemTextColor;		// Highlight color for menu text
-
-+ (NSColor *)highlightColor;     	     	// Highlight color for UI elements (this is abstract and defines the color all highlights tend toward)
-+ (NSColor *)shadowColor;     			// Shadow color for UI elements (this is abstract and defines the color all shadows tend toward)
+ */
+@property (class, strong, readonly) NSColor *blackColor;        /* 0.0 white */
+@property (class, strong, readonly) NSColor *darkGrayColor;     /* 0.333 white */
+@property (class, strong, readonly) NSColor *lightGrayColor;    /* 0.667 white */
+@property (class, strong, readonly) NSColor *whiteColor;        /* 1.0 white */
+@property (class, strong, readonly) NSColor *grayColor;         /* 0.5 white */
+@property (class, strong, readonly) NSColor *redColor;          /* 1.0, 0.0, 0.0 RGB */
+@property (class, strong, readonly) NSColor *greenColor;        /* 0.0, 1.0, 0.0 RGB */
+@property (class, strong, readonly) NSColor *blueColor;         /* 0.0, 0.0, 1.0 RGB */
+@property (class, strong, readonly) NSColor *cyanColor;         /* 0.0, 1.0, 1.0 RGB */
+@property (class, strong, readonly) NSColor *yellowColor;       /* 1.0, 1.0, 0.0 RGB */
+@property (class, strong, readonly) NSColor *magentaColor;      /* 1.0, 0.0, 1.0 RGB */
+@property (class, strong, readonly) NSColor *orangeColor;       /* 1.0, 0.5, 0.0 RGB */
+@property (class, strong, readonly) NSColor *purpleColor;       /* 0.5, 0.0, 0.5 RGB */
+@property (class, strong, readonly) NSColor *brownColor;        /* 0.6, 0.4, 0.2 RGB */
+@property (class, strong, readonly) NSColor *clearColor;        /* 0.0 white, 0.0 alpha */
+
+@property (class, strong, readonly) NSColor *controlShadowColor;            // Dark border for controls
+@property (class, strong, readonly) NSColor *controlDarkShadowColor;        // Darker border for controls
+@property (class, strong, readonly) NSColor *controlColor;                  // Control face and old window background color
+@property (class, strong, readonly) NSColor *controlHighlightColor;         // Light border for controls
+@property (class, strong, readonly) NSColor *controlLightHighlightColor;    // Lighter border for controls
+@property (class, strong, readonly) NSColor *controlTextColor;              // Text on controls
+@property (class, strong, readonly) NSColor *controlBackgroundColor;        // Background of large controls (browser, tableview, clipview, ...)
+@property (class, strong, readonly) NSColor *selectedControlColor;          // Control face for selected controls
+@property (class, strong, readonly) NSColor *secondarySelectedControlColor; // Color for selected controls when control is not active (that is, not focused)
+@property (class, strong, readonly) NSColor *selectedControlTextColor;      // Text on selected controls
+@property (class, strong, readonly) NSColor *disabledControlTextColor;      // Text on disabled controls
+@property (class, strong, readonly) NSColor *textColor;                     // Document text
+@property (class, strong, readonly) NSColor *textBackgroundColor;           // Document text background
+@property (class, strong, readonly) NSColor *selectedTextColor;             // Selected document text
+@property (class, strong, readonly) NSColor *selectedTextBackgroundColor;   // Selected document text background
+@property (class, strong, readonly) NSColor *gridColor;                     // Grids in controls
+@property (class, strong, readonly) NSColor *keyboardFocusIndicatorColor;   // Keyboard focus ring around controls
+@property (class, strong, readonly) NSColor *windowBackgroundColor;         // Background fill for window contents
+@property (class, strong, readonly) NSColor *underPageBackgroundColor NS_AVAILABLE_MAC(10_8); // Background areas revealed behind views
+
+@property (class, strong, readonly) NSColor *labelColor NS_AVAILABLE_MAC(10_10);              // Text color for static text and related elements
+@property (class, strong, readonly) NSColor *secondaryLabelColor NS_AVAILABLE_MAC(10_10);     // Text color for secondary static text and related elements
+@property (class, strong, readonly) NSColor *tertiaryLabelColor NS_AVAILABLE_MAC(10_10);      // Text color for disabled static text and related elements
+@property (class, strong, readonly) NSColor *quaternaryLabelColor NS_AVAILABLE_MAC(10_10);    // Text color for large secondary or disabled static text, separators, large glyphs/icons, etc
+
+@property (class, strong, readonly) NSColor *scrollBarColor;                // Scroll bar slot color
+@property (class, strong, readonly) NSColor *knobColor;                     // Knob face color for controls
+@property (class, strong, readonly) NSColor *selectedKnobColor;             // Knob face color for selected controls
+
+@property (class, strong, readonly) NSColor *windowFrameColor;              // Window frames
+@property (class, strong, readonly) NSColor *windowFrameTextColor;          // Text on window frames
+
+@property (class, strong, readonly) NSColor *selectedMenuItemColor;         // Highlight color for menus
+@property (class, strong, readonly) NSColor *selectedMenuItemTextColor;     // Highlight color for menu text
+
+@property (class, strong, readonly) NSColor *highlightColor;                // Highlight color for UI elements (this is abstract and defines the color all highlights tend toward)
+@property (class, strong, readonly) NSColor *shadowColor;                   // Shadow color for UI elements (this is abstract and defines the color all shadows tend toward)
+
+@property (class, strong, readonly) NSColor *headerColor;                   // Background color for header cells in Table/OutlineView
+@property (class, strong, readonly) NSColor *headerTextColor;               // Text color for header cells in Table/OutlineView
 
-+ (NSColor *)headerColor;			// Background color for header cells in Table/OutlineView
-+ (NSColor *)headerTextColor;			// Text color for header cells in Table/OutlineView
+@property (class, strong, readonly) NSColor *alternateSelectedControlColor;      // Similar to selectedControlColor; for use in lists and tables
+@property (class, strong, readonly) NSColor *alternateSelectedControlTextColor;  // Similar to selectedControlTextColor; see alternateSelectedControlColor
 
-+ (NSColor *)alternateSelectedControlColor;	// Similar to selectedControlColor; for use in lists and tables 
-+ (NSColor *)alternateSelectedControlTextColor;		// Similar to selectedControlTextColor; see alternateSelectedControlColor
+@property (class, strong, readonly) NSArray<NSColor *> *controlAlternatingRowBackgroundColors;  // Standard colors for alternating colored rows in tables and lists (for instance, light blue/white; don't assume just two colors)
 
-+ (NSArray<NSColor *> *)controlAlternatingRowBackgroundColors;	// Standard colors for alternating colored rows in tables and lists (for instance, light blue/white; don't assume just two colors)
+@property (class, readonly) NSControlTint currentControlTint;   // returns current system control tint
 
-- (nullable NSColor *)highlightWithLevel:(CGFloat)val;	// val = 0 => receiver, val = 1 => highlightColor
-- (nullable NSColor *)shadowWithLevel:(CGFloat)val;	// val = 0 => receiver, val = 1 => shadowColor
+#endif
 
 + (NSColor *)colorForControlTint:(NSControlTint)controlTint;	// pass in valid tint to get rough color matching. returns default if invalid tint
 
-+ (NSControlTint)currentControlTint;	// returns current system control tint
+- (nullable NSColor *)highlightWithLevel:(CGFloat)val;	// val = 0 => receiver, val = 1 => highlightColor
+- (nullable NSColor *)shadowWithLevel:(CGFloat)val;	// val = 0 => receiver, val = 1 => shadowColor
 
 
 /* Set the color: Sets the fill and stroke colors in the current drawing context. If the color doesn't know about alpha, it's set to 1.0. Should be implemented by subclassers.
@@ -290,8 +295,9 @@
 
 This method provides a global approach to removing alpha which might not always be appropriate. Applications which need to import alpha sometimes should set this flag to NO and explicitly make colors opaque in cases where it matters to them.
 */
-+ (void)setIgnoresAlpha:(BOOL)flag;
-+ (BOOL)ignoresAlpha;
+#if NSCOLOR_USE_CLASS_PROPERTIES
+@property (class) BOOL ignoresAlpha;
+#endif
 
 @end
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorSpace.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorSpace.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorSpace.h	2016-06-29 03:31:49.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorSpace.h	2016-07-11 05:26:54.000000000 +0200
@@ -15,6 +15,8 @@
 
 @class NSData;
 
+// By default class properties are enabled and available for Swift 3 and ObjC apps
+#define NSCOLORSPACE_USE_CLASS_PROPERTIES APPKIT_SWIFT_SDK_EPOCH_AT_LEAST(2)
 
 
 typedef NS_ENUM(NSInteger, NSColorSpaceModel) {
@@ -64,22 +66,24 @@
 @property (readonly) NSColorSpaceModel colorSpaceModel;
 @property (nullable, readonly, copy) NSString *localizedName;	// Will return nil if no localized name
 
-+ (NSColorSpace *)sRGBColorSpace  NS_AVAILABLE_MAC(10_5);
-+ (NSColorSpace *)genericGamma22GrayColorSpace  NS_AVAILABLE_MAC(10_6);             // The grayscale color space with gamma 2.2, compatible with sRGB
-
-+ (NSColorSpace *)extendedSRGBColorSpace  NS_AVAILABLE_MAC(10_12);                  // sRGB compatible color space that allows specifying components beyond the range of [0.0, 1.0]
-+ (NSColorSpace *)extendedGenericGamma22GrayColorSpace  NS_AVAILABLE_MAC(10_12);    // sRGB compatible gray color space that allows specifying components beyond the range of [0.0, 1.0]
-
-+ (NSColorSpace *)displayP3ColorSpace  NS_AVAILABLE_MAC(10_12);     // Standard DCI-P3 primaries, a D65 white point, and the same gamma curve as the sRGB IEC61966-2.1 color space
-
-+ (NSColorSpace *)adobeRGB1998ColorSpace  NS_AVAILABLE_MAC(10_5);
-
-+ (NSColorSpace *)genericRGBColorSpace;		// NSColorSpace corresponding to Cocoa color space name NSCalibratedRGBColorSpace
-+ (NSColorSpace *)genericGrayColorSpace;	// NSColorSpace corresponding to Cocoa color space name NSCalibratedWhiteColorSpace
-+ (NSColorSpace *)genericCMYKColorSpace;
-+ (NSColorSpace *)deviceRGBColorSpace;		// NSColorSpace corresponding to Cocoa color space name NSDeviceRGBColorSpace
-+ (NSColorSpace *)deviceGrayColorSpace;		// NSColorSpace corresponding to Cocoa color space name NSDeviceWhiteColorSpace
-+ (NSColorSpace *)deviceCMYKColorSpace;		// NSColorSpace corresponding to Cocoa color space name NSDeviceCMYKColorSpace
+#if NSCOLORSPACE_USE_CLASS_PROPERTIES
+@property (class, strong, readonly) NSColorSpace *sRGBColorSpace NS_AVAILABLE_MAC(10_5);
+@property (class, strong, readonly) NSColorSpace *genericGamma22GrayColorSpace NS_AVAILABLE_MAC(10_6);             // The grayscale color space with gamma 2.2, compatible with sRGB
+
+@property (class, strong, readonly) NSColorSpace *extendedSRGBColorSpace NS_AVAILABLE_MAC(10_12);                  // sRGB compatible color space that allows specifying components beyond the range of [0.0, 1.0]
+@property (class, strong, readonly) NSColorSpace *extendedGenericGamma22GrayColorSpace NS_AVAILABLE_MAC(10_12);    // sRGB compatible gray color space that allows specifying components beyond the range of [0.0, 1.0]
+
+@property (class, strong, readonly) NSColorSpace *displayP3ColorSpace NS_AVAILABLE_MAC(10_12);     // Standard DCI-P3 primaries, a D65 white point, and the same gamma curve as the sRGB IEC61966-2.1 color space
+
+@property (class, strong, readonly) NSColorSpace *adobeRGB1998ColorSpace NS_AVAILABLE_MAC(10_5);
+
+@property (class, strong, readonly) NSColorSpace *genericRGBColorSpace;		// NSColorSpace corresponding to Cocoa color space name NSCalibratedRGBColorSpace
+@property (class, strong, readonly) NSColorSpace *genericGrayColorSpace;	// NSColorSpace corresponding to Cocoa color space name NSCalibratedWhiteColorSpace
+@property (class, strong, readonly) NSColorSpace *genericCMYKColorSpace;
+@property (class, strong, readonly) NSColorSpace *deviceRGBColorSpace;		// NSColorSpace corresponding to Cocoa color space name NSDeviceRGBColorSpace
+@property (class, strong, readonly) NSColorSpace *deviceGrayColorSpace;		// NSColorSpace corresponding to Cocoa color space name NSDeviceWhiteColorSpace
+@property (class, strong, readonly) NSColorSpace *deviceCMYKColorSpace;		// NSColorSpace corresponding to Cocoa color space name NSDeviceCMYKColorSpace
+#endif
 
 /* Return the list of color spaces available on the system that are displayed by the color panel, in the order they are displayed in the color panel. Doesn't return arbitrary color spaces which may have been created on the fly, or spaces without user displayable names. Pass model==NSUnknownColorSpaceModel to get all color spaces. Empty array is returned if no color spaces are available for the specified model.
 */
@@ -89,14 +93,15 @@
 
 
 static const NSColorSpaceModel NSUnknownColorSpaceModel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorSpaceModelUnknown", macosx(10.0, 10.12))*/ = NSColorSpaceModelUnknown;
-static const NSColorSpaceModel NSGrayColorSpaceModel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorSpaceModelGray", macosx(10.0, 10.12))*/ = NSColorSpaceModelGray;
-static const NSColorSpaceModel NSRGBColorSpaceModel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorSpaceModelRGB", macosx(10.0, 10.12))*/ = NSColorSpaceModelRGB;
-static const NSColorSpaceModel NSCMYKColorSpaceModel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorSpaceModelCMYK", macosx(10.0, 10.12))*/ = NSColorSpaceModelCMYK;
-static const NSColorSpaceModel NSLABColorSpaceModel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorSpaceModelLAB", macosx(10.0, 10.12))*/ = NSColorSpaceModelLAB;
+static const NSColorSpaceModel NSGrayColorSpaceModel    /*API_DEPRECATED_WITH_REPLACEMENT("NSColorSpaceModelGray", macosx(10.0, 10.12))*/ = NSColorSpaceModelGray;
+static const NSColorSpaceModel NSRGBColorSpaceModel     /*API_DEPRECATED_WITH_REPLACEMENT("NSColorSpaceModelRGB", macosx(10.0, 10.12))*/ = NSColorSpaceModelRGB;
+static const NSColorSpaceModel NSCMYKColorSpaceModel    /*API_DEPRECATED_WITH_REPLACEMENT("NSColorSpaceModelCMYK", macosx(10.0, 10.12))*/ = NSColorSpaceModelCMYK;
+static const NSColorSpaceModel NSLABColorSpaceModel     /*API_DEPRECATED_WITH_REPLACEMENT("NSColorSpaceModelLAB", macosx(10.0, 10.12))*/ = NSColorSpaceModelLAB;
 static const NSColorSpaceModel NSDeviceNColorSpaceModel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorSpaceModelDeviceN", macosx(10.0, 10.12))*/ = NSColorSpaceModelDeviceN;
 static const NSColorSpaceModel NSIndexedColorSpaceModel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorSpaceModelIndexed", macosx(10.0, 10.12))*/ = NSColorSpaceModelIndexed;
 static const NSColorSpaceModel NSPatternColorSpaceModel /*API_DEPRECATED_WITH_REPLACEMENT("NSColorSpaceModelPatterned", macosx(10.0, 10.12))*/ = NSColorSpaceModelPatterned;
 
+
 NS_ASSUME_NONNULL_END
 
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDocument.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDocument.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDocument.h	2016-06-29 03:31:49.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDocument.h	2016-07-11 05:26:54.000000000 +0200
@@ -470,6 +470,14 @@
 */
 - (IBAction)browseDocumentVersions:(nullable id)sender NS_AVAILABLE_MAC(10_8);
 
+/* Whether the receiver is currently displaying the Versions browser. KVO-compliant.
+*/
+@property (getter=isBrowsingVersions, readonly) BOOL browsingVersions NS_AVAILABLE_MAC(10_12);
+
+/* If the receiver is currently displaying the Versions browser, cleanly stop browsing versions (which includes waiting for any animations to complete). Then invoke the completion handler on the main thread.
+*/
+- (void)stopBrowsingVersionsWithCompletionHandler:(void (^ _Nullable)(void))completionHandler NS_AVAILABLE_MAC(10_12);
+
 /* Return YES if the receiving subclass of NSDocument supports Mac OS 10.8 autosaving of drafts, NO otherwise. The default implementation of this method returns YES for applications linked on or after Mac OS 10.8. You can override it and return YES to declare your NSDocument subclass' ability to do Mac OS 10.8 autosaving of drafts. You can also override it and return NO to opt out of this behavior after linking with 10.8. You should not invoke this method to find out whether autosaving of a draft will be done. Instances of subclasses that return YES from this method should be ready to properly handle save operations with NSAutosaveAsOperation.
 
 AppKit invokes this method at a variety of times. For example, when -updateChangeCount is called with NSChangeDone (without NSChangeDiscardable), NSDocument will the next autosave to use NSAutosaveAsOperation and return the document into a draft.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGraphics.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGraphics.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGraphics.h	2016-06-29 03:31:49.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGraphics.h	2016-07-11 05:26:54.000000000 +0200
@@ -179,8 +179,8 @@
 /* Approximate color gamut for use by NSScreen and NSWindow
  */
 typedef NS_ENUM(NSInteger, NSDisplayGamut) {
-    NSDisplayGamutSRGB = 1,
-    NSDisplayGamutP3
+    NSDisplayGamutSRGB NS_SWIFT_NAME(sRGB) = 1,
+    NSDisplayGamutP3 NS_SWIFT_NAME(p3)
 } NS_ENUM_AVAILABLE_MAC(10_12);
 
 /* Keys for deviceDescription dictionaries.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImage.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImage.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImage.h	2016-06-29 03:31:49.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImage.h	2016-07-11 05:26:54.000000000 +0200
@@ -16,6 +16,8 @@
 #import <AppKit/NSLayoutConstraint.h>
 #import <ApplicationServices/ApplicationServices.h>
 
+#define NS_IMAGE_DECLARES_DESIGNATED_INITIALIZERS APPKIT_SWIFT_SDK_EPOCH_AT_LEAST(2)
+
 NS_ASSUME_NONNULL_BEGIN
 
 @class NSColor, NSImageRep, NSGraphicsContext, NSURL;
@@ -80,7 +82,11 @@
 
 + (nullable NSImage *)imageNamed:(NSString *)name;	/* If this finds & creates the image, only name is saved when archived */
 
-- (instancetype)initWithSize:(NSSize)size;
+#if NS_IMAGE_DECLARES_DESIGNATED_INITIALIZERS
+- (instancetype)initWithSize:(NSSize)size NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
+#endif
+
 - (nullable instancetype)initWithData:(NSData *)data;			/* When archived, saves contents */
 - (nullable instancetype)initWithContentsOfFile:(NSString *)fileName;	/* When archived, saves contents */
 - (nullable instancetype)initWithContentsOfURL:(NSURL *)url;               /* When archived, saves contents */
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenuItem.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenuItem.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenuItem.h	2016-06-29 03:31:49.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSMenuItem.h	2016-07-11 05:26:54.000000000 +0200
@@ -103,7 +103,7 @@
 
 @property (nullable, strong) NSImage *image;
 
-@property NSInteger /* NSControlState */ state;
+@property NSInteger state;
 @property (null_resettable, strong) NSImage *onStateImage; // checkmark by default
 @property (nullable, strong) NSImage *offStateImage; // none by default
 @property (null_resettable, strong) NSImage *mixedStateImage; // horizontal line by default?
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenGL.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenGL.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenGL.h	2016-06-29 03:31:49.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSOpenGL.h	2016-07-11 05:26:54.000000000 +0200
@@ -5,9 +5,12 @@
         All rights reserved.
 */
 
+#import <AppKit/AppKitDefines.h>
 #import <Foundation/Foundation.h>
 #import <OpenGL/gltypes.h>
 
+#define NS_OPENGL_PIXEL_FORMAT_DECLARES_DESIGNATED_INITIALIZERS APPKIT_SWIFT_SDK_EPOCH_AT_LEAST(2)
+
 NS_ASSUME_NONNULL_BEGIN
 
 @class NSData, NSView, NSScreen;
@@ -115,9 +118,11 @@
     void *_reserved4 __unused;
 }
 
+#if NS_OPENGL_PIXEL_FORMAT_DECLARES_DESIGNATED_INITIALIZERS
+- (nullable NSOpenGLPixelFormat *)initWithCGLPixelFormatObj:(struct _CGLPixelFormatObject *)format NS_AVAILABLE_MAC(10_6) NS_DESIGNATED_INITIALIZER;
+#endif
 - (nullable instancetype)initWithAttributes:(const NSOpenGLPixelFormatAttribute *)attribs;
 - (nullable id)initWithData:(null_unspecified NSData*)attribs NS_DEPRECATED_MAC(10_0, 10_6, "Use -initWithAttributes: instead");
-- (nullable NSOpenGLPixelFormat *)initWithCGLPixelFormatObj:(struct _CGLPixelFormatObject *)format NS_AVAILABLE_MAC(10_6);
 
 - (null_unspecified NSData*)attributes NS_DEPRECATED_MAC(10_0, 10_6);
 - (void)setAttributes:(null_unspecified NSData*)attribs NS_DEPRECATED_MAC(10_0, 10_6);
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSharingService.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSharingService.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSharingService.h	2016-06-29 03:31:50.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSharingService.h	2016-07-11 05:26:55.000000000 +0200
@@ -12,6 +12,8 @@
 #import <Foundation/NSObject.h>
 #import <Foundation/NSArray.h>
 
+#define NS_SHARING_SERVICE_DELEGATE_TRANSITION_IMAGE_FOR_SHARE_ITEM_DECLARES_NULLABILITY (1)
+
 @class NSString, NSImage, NSView, NSError, NSWindow;
 @class CKShare, CKContainer;
 
@@ -139,7 +141,7 @@
 /* The following methods are invoked when the service is performed and the sharing window pops up, to present a transition between the original items and the sharing window.
  */
 - (NSRect)sharingService:(NSSharingService *)sharingService sourceFrameOnScreenForShareItem:(id)item;
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_APPKIT_EPOCH) && SWIFT_SDK_OVERLAY_APPKIT_EPOCH >= 1)
+#if NS_SHARING_SERVICE_DELEGATE_TRANSITION_IMAGE_FOR_SHARE_ITEM_DECLARES_NULLABILITY
 /* When non-nil, the image returned would be used for the transitioning animation. When nil, the transitioning animation is disabled.
  */
 - (nullable NSImage *)sharingService:(NSSharingService *)sharingService transitionImageForShareItem:(id)item contentRect:(NSRect *)contentRect;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableViewRowAction.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableViewRowAction.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableViewRowAction.h	2016-06-29 03:31:49.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableViewRowAction.h	2016-07-11 05:26:54.000000000 +0200
@@ -9,7 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-@class NSColor, NSButton;
+@class NSColor, NSButton, NSImage;
 
 typedef NS_ENUM(NSInteger, NSTableViewRowActionStyle) {
     NSTableViewRowActionStyleRegular,
@@ -37,6 +37,10 @@
 @property (copy) NSString *title;
 @property (null_resettable, copy) NSColor *backgroundColor; // The default background color is dependent on style. Generally this is red for destructive actions, and blue for others.
 
+/* Prefer using an image over text for the row action button
+ */
+@property (nullable, strong) NSImage *image API_AVAILABLE(macosx(10.12));
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTokenField.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTokenField.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTokenField.h	2016-06-29 03:31:49.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTokenField.h	2016-07-11 05:26:54.000000000 +0200
@@ -12,43 +12,16 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-@protocol NSTokenFieldDelegate;
+@class NSTokenField;
 
 
-@interface NSTokenField : NSTextField {    
-    BOOL _reserved1;
-    BOOL _reserved2;
-    BOOL _reserved3;
-    BOOL _reserved4;
-
-    NSTrackingRectTag  _trackingRectTag;
-    id _reserved5;
-    id _reserved6;
-    id _reserved7;
-}
-
-- (void)setDelegate:(nullable id <NSTokenFieldDelegate>)delegate;
-- (nullable id <NSTokenFieldDelegate>)delegate;
-
-/* Sets the default token style used for each new token.  However, if the delegate implements tokenField:styleForRepresentedObject:, that return value will be used instead.
-*/
-@property NSTokenStyle tokenStyle;
-
-@property NSTimeInterval completionDelay;
-+ (NSTimeInterval)defaultCompletionDelay;
-
-@property (null_resettable, copy) NSCharacterSet *tokenizingCharacterSet;
-+ (NSCharacterSet *)defaultTokenizingCharacterSet;
-
-@end
-
 @protocol NSTokenFieldDelegate <NSTextFieldDelegate>
 
 @optional
 
 // Each element in the array should be an NSString or an array of NSStrings.
 // substring is the partial string that is being completed.  tokenIndex is the index of the token being completed.
-// selectedIndex allows you to return by reference an index specifying which of the completions should be selected initially. 
+// selectedIndex allows you to return by reference an index specifying which of the completions should be selected initially.
 // The default behavior is not to have any completions.
 - (nullable NSArray *)tokenField:(NSTokenField *)tokenField completionsForSubstring:(NSString *)substring indexOfToken:(NSInteger)tokenIndex indexOfSelectedItem:(nullable NSInteger *)selectedIndex;
 
@@ -63,7 +36,7 @@
 - (nullable NSString *)tokenField:(NSTokenField *)tokenField editingStringForRepresentedObject:(id)representedObject;
 - (id)tokenField:(NSTokenField *)tokenField representedObjectForEditingString: (NSString *)editingString;
 
-// We put the string on the pasteboard before calling this delegate method. 
+// We put the string on the pasteboard before calling this delegate method.
 // By default, we write the NSStringPboardType as well as an array of NSStrings.
 - (BOOL)tokenField:(NSTokenField *)tokenField writeRepresentedObjects:(NSArray *)objects toPasteboard:(NSPasteboard *)pboard;
 
@@ -72,7 +45,7 @@
 
 // By default the tokens have no menu.
 - (nullable NSMenu *)tokenField:(NSTokenField *)tokenField menuForRepresentedObject:(id)representedObject;
-- (BOOL)tokenField:(NSTokenField *)tokenField hasMenuForRepresentedObject:(id)representedObject; 
+- (BOOL)tokenField:(NSTokenField *)tokenField hasMenuForRepresentedObject:(id)representedObject;
 
 // This method allows you to change the style for individual tokens as well as have mixed text and tokens.
 - (NSTokenStyle)tokenField:(NSTokenField *)tokenField styleForRepresentedObject:(id)representedObject;
@@ -80,4 +53,32 @@
 
 @end
 
+
+@interface NSTokenField : NSTextField {    
+    BOOL _reserved1;
+    BOOL _reserved2;
+    BOOL _reserved3;
+    BOOL _reserved4;
+
+    NSTrackingRectTag  _trackingRectTag;
+    id _reserved5;
+    id _reserved6;
+    id _reserved7;
+}
+
+/* For apps linked against 10.12, this property has zeroing weak memory semantics. When linked against an older SDK, or with objects that do not support zeroing weak references this falls back to having `assign` semantics. */
+@property (nullable, assign) id<NSTokenFieldDelegate> delegate;
+
+/* Sets the default token style used for each new token.  However, if the delegate implements tokenField:styleForRepresentedObject:, that return value will be used instead.
+*/
+@property NSTokenStyle tokenStyle;
+
+@property NSTimeInterval completionDelay;
++ (NSTimeInterval)defaultCompletionDelay;
+
+@property (null_resettable, copy) NSCharacterSet *tokenizingCharacterSet;
++ (NSCharacterSet *)defaultTokenizingCharacterSet;
+
+@end
+
 NS_ASSUME_NONNULL_END

```