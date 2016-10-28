diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButton.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButton.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButton.h	2016-08-11 21:43:44.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSButton.h	2016-10-10 22:25:11.000000000 -0400
@@ -37,6 +37,8 @@
 @property (getter=isSpringLoaded) BOOL springLoaded NS_AVAILABLE_MAC(10_10_3); // sends action on deep-press or extended hover while dragging. Defaults to NO.
 @property NSInteger maxAcceleratorLevel NS_AVAILABLE_MAC(10_10_3);	// Configures the maximum allowed level for an NSMultiLevelAcceleratorButton, allowed values range from [1,5]. Defaults to 2.
 
+@property (nullable, copy) NSColor *bezelColor NS_AVAILABLE_MAC(10_12_1); // The color of the button's bevel, in appearances that support it
+
 @end
 
 
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCandidateListTouchBarItem.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCandidateListTouchBarItem.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCandidateListTouchBarItem.h	1969-12-31 19:00:00.000000000 -0500
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCandidateListTouchBarItem.h	2016-10-10 22:25:11.000000000 -0400
@@ -0,0 +1,104 @@
+/*
+    NSCandidateListTouchBarItem.h
+    Application Kit
+    Copyright (c) 2016, Apple Inc.
+    All rights reserved.
+*/
+
+#import <AppKit/NSTouchBar.h>
+#import <AppKit/NSTouchBarItem.h>
+#import <AppKit/NSView.h>
+
+@protocol NSCandidateListTouchBarItemDelegate;
+@protocol NSTextInputClient;
+
+NS_ASSUME_NONNULL_BEGIN
+
+/* NSCandidateListTouchBarItem is a touch bar item that shows the word completion candidates for assisting users typing with text input capable views. In addition to candidates supplied by its client, the touch bar item can show candidates coming from the active input method. NSCandidateListTouchBarItem has two states: expanded and collapsed. When expanded, the item replaces any touch bar items occupying its location on the bar.
+*/
+
+#pragma mark NSCandidateListTouchBarItem
+NS_CLASS_AVAILABLE_MAC(10_12_1)
+@interface NSCandidateListTouchBarItem<CandidateType> : NSTouchBarItem
+#if !__OBJC2__
+{
+@private
+    id _candidateViewController;
+    NSString *_customizationLabel;
+    
+    NSViewController *_inputContextViewController;
+    
+    struct {
+        unsigned int _allowsIM:1;
+        unsigned int _collapsed:1;
+        unsigned int _isTextCompletionItem:1;
+        unsigned int _reserved:29;
+    } _clfbiFlags;
+    
+    void *_candidateListTouchBarItemReserved[4] __unused;
+}
+#endif
+
+#pragma mark Client
+// The client object for the receiver.
+@property (nullable, weak) NSView <NSTextInputClient> *client;
+
+@property (nullable, weak) id <NSCandidateListTouchBarItemDelegate> delegate;
+
+#pragma mark Appearance State
+// Controls the visible state of the receiver touch bar item. The default is YES.
+@property (getter=isCollapsed) BOOL collapsed;
+
+// When YES, the touch bar item is allowed to be collapsed. YES by default.
+@property BOOL allowsCollapsing;
+
+// Returns the state of its native candidate list visibility. When -collapsed=NO and not obscured by UI from the text input system, this property returns YES. KVO compliant. Clients should set candidates when YES.
+@property (readonly, getter=isCandidateListVisible) BOOL candidateListVisible;
+
+// Updates the candidate list visibility configuration based on the client's insertion point state. The client is expected to update the candidate list visibility configuration whenever its selection changes. When the selection length is 0 and the insertion cursor is visible, isVisible should be YES; otherwise, it should be NO. When -hasMarkedText is YES, it should be considered the cursor is visible.
+- (void)updateWithInsertionPointVisibility:(BOOL)isVisible;
+
+#pragma mark Input Method support
+// When YES, the touch bar item displays candidates from input methods when available instead of -candidates. YES by default.
+@property BOOL allowsTextInputContextCandidates;
+
+#pragma mark Candidates
+// A block function for converting a candidate object into an NSAttributedString that will be displayed in the candidate bar. nil by default. Not required for displaying NSString, NSAttributedString, and NSTextCheckingResult candidates. In absence of NSFontAttributeName and NSForegroundColorAttributeName in the returned string, the standard touch bar appearance font and color are used instead of Helvetica 12.0 and +[NSColor blackColor].
+@property (nullable, copy) NSAttributedString * (^attributedStringForCandidate)(CandidateType candidate, NSInteger index);
+
+// Returns an array of candidate objects previously set via -setCandidates:forSelectedRange:inString:view:.
+@property (readonly, copy) NSArray<CandidateType> *candidates;
+ 
+// Sets an array of candidate objects to be displayed in the candidate list bar item. The candidate objects are interpreted by -attributedStringForCandidate if the property is non-nil. NSCandidateListTouchBarItem can format NSString, NSAttributedString, and NSTextCheckingResult without the formatting block specified. The touch bar item will decide which candidates to place in the candidates array and in which order. The selectedRange and originalString arguments tell the context the list of candidates was originally derived from. For NSTextCheckingResult candidates, the selectedRange and originalString arguments should match those passed in to NSSpellChecker. The touch bar item will also arrange to display candidates near the selection in the view when appropriate.
+- (void)setCandidates:(NSArray<CandidateType> *)candidates forSelectedRange:(NSRange)selectedRange inString:(nullable NSString *)originalString;
+
+// The label displayed in the customization panel. The default is an empty string.
+@property (readwrite, copy, null_resettable) NSString *customizationLabel;
+@end
+
+#pragma mark NSCandidateListTouchBarItemDelegate
+@protocol NSCandidateListTouchBarItemDelegate <NSObject>
+@optional
+
+// Invoked when user touches down on a candidate in the bar.
+- (void)candidateListTouchBarItem:(NSCandidateListTouchBarItem *)anItem beginSelectingCandidateAtIndex:(NSInteger)index NS_AVAILABLE_MAC(10_12_1);
+
+// Invoked when user moves from touching one candidate in the bar to another.
+- (void)candidateListTouchBarItem:(NSCandidateListTouchBarItem *)anItem changeSelectionFromCandidateAtIndex:(NSInteger)previousIndex toIndex:(NSInteger)index NS_AVAILABLE_MAC(10_12_1);
+
+// Invoked when user stops touching candidates in the bar. If index==NSNotFound, user didn't select any candidate.
+- (void)candidateListTouchBarItem:(NSCandidateListTouchBarItem *)anItem endSelectingCandidateAtIndex:(NSInteger)index NS_AVAILABLE_MAC(10_12_1);
+
+// Invoked when -candidateListVisible changed the visibility state.
+- (void)candidateListTouchBarItem:(NSCandidateListTouchBarItem *)anItem changedCandidateListVisibility:(BOOL)isVisible NS_AVAILABLE_MAC(10_12_1);
+@end
+
+@interface NSView (NSCandidateListTouchBarItem)
+// Returns NSCandidateListTouchBarItem used by the receiver when the first responder. The default implementation just returns nil. NSTextInputContext uses the item returned from this method for showing the candidates from input methods.
+@property (nullable, readonly, strong) NSCandidateListTouchBarItem *candidateListTouchBarItem NS_AVAILABLE_MAC(10_12_1);
+@end
+
+// The standard touch bar item identifier for NSCandidateListTouchBarItem. -[NSView candidateListTouchBarItem] concrete overrides should be using this identifier for instantiating the touch bar item.
+APPKIT_EXTERN NSTouchBarItemIdentifier const NSTouchBarItemIdentifierCandidateList NS_AVAILABLE_MAC(10_12_1);
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSClickGestureRecognizer.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSClickGestureRecognizer.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSClickGestureRecognizer.h	2016-08-11 21:43:44.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSClickGestureRecognizer.h	2016-10-10 22:25:11.000000000 -0400
@@ -32,6 +32,7 @@
 /* the number of clicks required to match */
 @property NSInteger numberOfClicksRequired; // Defaults to 1
 
+@property NSInteger numberOfTouchesRequired NS_AVAILABLE_MAC(10_12_1);
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColor.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColor.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColor.h	2016-08-11 21:43:44.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColor.h	2016-10-10 22:25:11.000000000 -0400
@@ -166,7 +166,9 @@
 
 @property (class, readonly) NSControlTint currentControlTint;   // returns current system control tint
 
-#endif
+#endif // NSCOLOR_USE_CLASS_PROPERTIES
+
+@property (class, strong, readonly) NSColor *scrubberTexturedBackgroundColor NS_AVAILABLE_MAC(10_12_1); // Patterned background color for use in NSScrubber
 
 + (NSColor *)colorForControlTint:(NSControlTint)controlTint;	// pass in valid tint to get rough color matching. returns default if invalid tint
 
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorPickerTouchBarItem.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorPickerTouchBarItem.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorPickerTouchBarItem.h	1969-12-31 19:00:00.000000000 -0500
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorPickerTouchBarItem.h	2016-10-10 22:25:11.000000000 -0400
@@ -0,0 +1,68 @@
+/*
+ NSColorPickerTouchBarItem.h
+ Application Kit
+ Copyright (c) 2016-2016, Apple Inc.
+ All rights reserved.
+*/
+
+#import <AppKit/NSTouchBarItem.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class NSViewController, NSColor, NSImage, NSString, NSColorList;
+
+NS_CLASS_AVAILABLE_MAC(10_12_1)
+@interface NSColorPickerTouchBarItem : NSTouchBarItem {
+@private
+    id _overlay;
+    NSString *_customizationLabel;
+    NSColor *_color;
+    __weak id _target;
+    SEL _action;
+    NSInteger _mode;
+    NSView *_view;
+    NSString *_buttonTitle;
+    NSImage *_buttonImage;
+    NSColorList *_colorList;
+    id _autounbinder;
+    id _colorPickerReserved __unused;
+    signed char _showsAlpha:1;
+    signed char _supportsPressAndHoldVariants:1;
+    signed char _enabled:1;
+#if !__OBJC2__
+    unsigned int _colorPickerTouchBarItemReservedFlags:29 __unused;
+    void *_colorPickerTouchBarItemReserved[3] __unused;
+#endif /* !__OBJC2__ */
+}
+
+/// Creates a bar item containing a button with the standard color picker icon that invokes the color picker.
++ (instancetype)colorPickerWithIdentifier:(NSTouchBarItemIdentifier)identifier;
+/// Creates a bar item containing a button with the standard text color picker icon that invokes the color picker. Should be used when the item is used for picking text colors.
++ (instancetype)textColorPickerWithIdentifier:(NSTouchBarItemIdentifier)identifier;
+/// Creates a bar item containing a button with the standard stroke color picker icon that invokes the color picker. Should be used when the item is used for picking stroke colors.
++ (instancetype)strokeColorPickerWithIdentifier:(NSTouchBarItemIdentifier)identifier;
+
+/// Creates a bar item containing a button with the provided image that invokes the color picker.
++ (instancetype)colorPickerWithIdentifier:(NSTouchBarItemIdentifier)identifier buttonImage:(NSImage *)image;
+
+/// The selected color of the picker.
+@property (copy) NSColor *color;
+
+/// Whether or not the picker should allow picking a color with non-1.0 alpha. Defaults to `!NSColor.ignoresAlpha`.
+@property BOOL showsAlpha;
+
+/// The color list displayed in the list color picker. Defaults to the standard system color list. Setting a custom color list will disable the additional tints/shades that appear on long-press.
+@property (strong, null_resettable) NSColorList *colorList;
+
+/// The localized string labelling this item during user customization. The default value is the localized string of "Color Picker".
+@property (readwrite, copy, null_resettable) NSString *customizationLabel;
+
+@property (weak, nullable) id target;
+@property (nullable) SEL action;
+
+/// Enables or disabled the color picker. If it is currently being shown in a popover, it will be dismissed.
+@property (getter=isEnabled) BOOL enabled;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCustomTouchBarItem.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCustomTouchBarItem.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCustomTouchBarItem.h	1969-12-31 19:00:00.000000000 -0500
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCustomTouchBarItem.h	2016-10-10 22:25:11.000000000 -0400
@@ -0,0 +1,46 @@
+/*
+ NSCustomTouchBarItem.h
+ Application Kit
+ Copyright (c) 2015-2016, Apple Inc.
+ All rights reserved.
+*/
+
+#import <AppKit/NSTouchBarItem.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+NS_CLASS_AVAILABLE_MAC(10_12_1)
+@interface NSCustomTouchBarItem : NSTouchBarItem {
+@private
+    NSView *_view;
+    NSViewController *_viewController;
+    NSString *_customizationLabel;
+    NSInteger _preferredPopoverTransposerPriority;
+    Class _preferredPopoverTransposerClass;
+#if !__OBJC2__
+    void *_customTouchBarItemReserved[4] __unused;
+#endif /* !__OBJC2__ */
+}
+
+/*
+    A view to be displayed in the touch bar in the location corresponding to this item. 
+    By default, the getter for this property will return this item's view controller's view. If this property is set explicitly, the view controller will be set to nil.
+    This property is archived.
+*/
+@property (readwrite, strong) __kindof NSView *view;
+
+/*
+    A view controller whose view is to be displayed in the touch bar in the location corresponding to this item.
+    By default, this property is nil. When set, this item's view property will automatically return the view associated with this view controller.
+    This property is archived.
+*/
+@property (readwrite, strong, nullable) __kindof NSViewController *viewController;
+
+/*
+    The localized string labelling this item during user customization. The default value is the empty string. This property is archived.
+*/
+@property (readwrite, copy, null_resettable) NSString *customizationLabel;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSEvent.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSEvent.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSEvent.h	2016-08-11 21:43:44.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSEvent.h	2016-10-10 22:25:11.000000000 -0400
@@ -57,7 +57,8 @@
     NSEventTypeQuickLook NS_ENUM_AVAILABLE_MAC(10_8) = 33,
     
 #if __LP64__
-    NSEventTypePressure NS_ENUM_AVAILABLE_MAC(10_10_3) = 34
+    NSEventTypePressure NS_ENUM_AVAILABLE_MAC(10_10_3) = 34,
+    NSEventTypeDirectTouch NS_ENUM_AVAILABLE_MAC(10_10) = 37,
 #endif
 };
 
@@ -124,6 +125,7 @@
      */
     NSEventMaskSmartMagnify NS_ENUM_AVAILABLE_MAC(10_8) = 1ULL << NSEventTypeSmartMagnify,
     NSEventMaskPressure NS_ENUM_AVAILABLE_MAC(10_10_3) = 1ULL << NSEventTypePressure,
+    NSEventMaskDirectTouch NS_ENUM_AVAILABLE_MAC(10_12_1) = 1ULL << NSEventTypeDirectTouch,
 #endif
     
     NSEventMaskAny              = NSUIntegerMax,
@@ -540,6 +542,16 @@
 
 - (NSSet<NSTouch *> *)touchesMatchingPhase:(NSTouchPhase)phase inView:(nullable NSView *)view NS_AVAILABLE_MAC(10_6);
 
+/* Only valid for NSEventTypeGesture events. Equivalent to [event touchesMatchingPhase:NSTouchPhaseAny inView:nil] */
+- (NSSet <NSTouch *> *)allTouches NS_AVAILABLE_MAC(10_12);
+
+/* Only valid for NSEventTypeGesture events. Equivalent to [event touchesMatchingPhase:NSTouchPhaseAny inView:view] */
+- (NSSet <NSTouch *> *)touchesForView:(NSView *)view NS_AVAILABLE_MAC(10_12);
+
+/* An array of auxiliary NSTouch’s for the touch events that did not get delivered for a given main touch. This also includes an auxiliary version of the main touch itself. Only valid for NSEventTypeDirectTouch events.
+*/
+- (NSArray <NSTouch *> *)coalescedTouchesForTouch:(NSTouch *)touch NS_AVAILABLE_MAC(10_12_1);
+
 /* The phase of a gesture scroll event. A gesture phrase are all the events that begin with a NSEventPhaseBegan and end with either a NSEventPhaseEnded or NSEventPhaseCancelled. All the gesture events are sent to the view under the cursor when the NSEventPhaseBegan occurred.  A gesture scroll event starts with a NSEventPhaseBegan phase and ends with a NSPhaseEnded. Legacy scroll wheel events (say from a Mighty Mouse) and momentum scroll wheel events have a phase of NSEventPhaseNone.
     Valid for NSEventTypeScrollWheel
 */
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGestureRecognizer.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGestureRecognizer.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGestureRecognizer.h	2016-08-11 21:43:44.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGestureRecognizer.h	2016-10-10 22:25:11.000000000 -0400
@@ -7,11 +7,12 @@
 
 #import <Foundation/Foundation.h>
 #import <CoreGraphics/CoreGraphics.h>
+#import <AppKit/NSTouch.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
 @protocol NSGestureRecognizerDelegate;
-@class NSView, NSEvent, NSPressureConfiguration;
+@class NSView, NSEvent, NSPressureConfiguration, NSTouch;
 
 NS_ENUM_AVAILABLE_MAC(10_10)
 typedef NS_ENUM(NSInteger, NSGestureRecognizerState) {
@@ -93,6 +94,10 @@
 
 @end
 
+@interface NSGestureRecognizer (NSTouchBar)
+/* Currently, only NSTouchTypeDirect is supported. Defaults to 0 */
+@property NSTouchTypeMask allowedTouchTypes NS_AVAILABLE_MAC(10_12_1);
+@end
 
 @protocol NSGestureRecognizerDelegate <NSObject>
 @optional
@@ -119,6 +124,9 @@
 - (BOOL)gestureRecognizer:(NSGestureRecognizer *)gestureRecognizer shouldRequireFailureOfGestureRecognizer:(NSGestureRecognizer *)otherGestureRecognizer;
 - (BOOL)gestureRecognizer:(NSGestureRecognizer *)gestureRecognizer shouldBeRequiredToFailByGestureRecognizer:(NSGestureRecognizer *)otherGestureRecognizer;
 
+/* called before touchesBegan:withEvent: is called on the gesture recognizer for a new touch. return NO to prevent the gesture recognizer from seeing this touch
+ */
+- (BOOL)gestureRecognizer:(NSGestureRecognizer *)gestureRecognizer shouldReceiveTouch:(NSTouch *)touch NS_AVAILABLE_MAC(10_12_1);
 @end
 
 // the extensions in this header are to be used only by subclasses of NSGestureRecognizer
@@ -165,7 +173,10 @@
 - (void)magnifyWithEvent:(NSEvent *)event;
 - (void)rotateWithEvent:(NSEvent *)event;
 - (void)pressureChangeWithEvent:(NSEvent *)event NS_AVAILABLE_MAC(10_10_3);
-
+- (void)touchesBeganWithEvent:(NSEvent *)event NS_AVAILABLE_MAC(10_12_1);
+- (void)touchesMovedWithEvent:(NSEvent *)event NS_AVAILABLE_MAC(10_12_1);
+- (void)touchesEndedWithEvent:(NSEvent *)event NS_AVAILABLE_MAC(10_12_1);
+- (void)touchesCancelledWithEvent:(NSEvent *)event NS_AVAILABLE_MAC(10_12_1);
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGroupTouchBarItem.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGroupTouchBarItem.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGroupTouchBarItem.h	1969-12-31 19:00:00.000000000 -0500
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSGroupTouchBarItem.h	2016-10-10 22:25:11.000000000 -0400
@@ -0,0 +1,41 @@
+/*
+ NSGroupTouchBarItem.h
+ Application Kit
+ Copyright (c) 2015-2016, Apple Inc.
+ All rights reserved.
+*/
+
+#import <AppKit/NSTouchBarItem.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+NS_CLASS_AVAILABLE_MAC(10_12_1)
+@interface NSGroupTouchBarItem : NSTouchBarItem {
+@private
+    NSTouchBar *_groupTouchBar;
+    NSString *_customizationLabel;
+#if !__OBJC2__
+    void *_groupTouchBarItemReserved[4] __unused;
+#endif /* !__OBJC2__ */
+}
+
+/*
+    Returns an autoreleased NSGroupTouchBarItem with a groupTouchBar built from the given items array. Customization is not enabled by default when creating a NSGroupTouchBarItem this way.
+*/
++ (NSGroupTouchBarItem *)groupItemWithIdentifier:(NSTouchBarItemIdentifier)identifier items:(NSArray<NSTouchBarItem *> *)items;
+
+/*
+    A touch bar, presented seamlessly as part of the touch bar this item is hosted in.
+    This touch bar may have its own principal item, and can be customized (or not) per the normal touch bar customization rules.
+    By default this is an empty touch bar that cannot be customized. This property is archived.
+*/
+@property (strong) NSTouchBar *groupTouchBar;
+
+/*
+    The localized string labelling this item during user customization. The default value is the empty string. This property is archived.
+*/
+@property (readwrite, copy, null_resettable) NSString *customizationLabel;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImage.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImage.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImage.h	2016-08-11 21:43:44.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImage.h	2016-10-10 22:25:11.000000000 -0400
@@ -228,7 +228,7 @@
 
 APPKIT_EXTERN NSString * const NSImageHintCTM NS_AVAILABLE_MAC(10_6); // value is NSAffineTransform
 APPKIT_EXTERN NSString * const NSImageHintInterpolation NS_AVAILABLE_MAC(10_6); // value is NSNumber with NSImageInterpolation enum value
-APPKIT_EXTERN NSString *const NSImageHintUserInterfaceLayoutDirection NS_AVAILABLE_MAC(10_12); // value is NSNumber with NSUserInterfaceLayoutDirection enum value
+APPKIT_EXTERN NSString * const NSImageHintUserInterfaceLayoutDirection NS_AVAILABLE_MAC(10_12); // value is NSNumber with NSUserInterfaceLayoutDirection enum value
 
 @protocol NSImageDelegate <NSObject>
 @optional
@@ -292,8 +292,7 @@
  
  Some images also contain the word "Freestanding".  This indicates that an image is appropriate for use as a borderless button - it doesn't need any extra bezel artwork behind it.  For example, Safari uses NSImageNameStopProgressTemplate as the stop button in a button on its toolbar, while it uses NSImageNameStopProgressFreestandingTemplate in the downloads window where it appears inline with a progress indicator.
   
- The string value of each symbol is the same as the constant name without the "ImageName" part.  For example, NSImageNameBonjour is @"NSBonjour".  This is documented so that images can be used by name in Interface Builder.     
- 
+ The string value of each symbol is the same as the constant name without the "ImageName" part.  For example, NSImageNameBonjour is @"NSBonjour".  This is documented so that images can be used by name in Interface Builder.
  */
 APPKIT_EXTERN NSString * const NSImageNameQuickLookTemplate NS_AVAILABLE_MAC(10_5);
 APPKIT_EXTERN NSString * const NSImageNameBluetoothTemplate NS_AVAILABLE_MAC(10_5);
@@ -402,7 +401,88 @@
 APPKIT_EXTERN NSString * const NSImageNameStatusPartiallyAvailable NS_AVAILABLE_MAC(10_6);
 APPKIT_EXTERN NSString * const NSImageNameStatusUnavailable NS_AVAILABLE_MAC(10_6);
 APPKIT_EXTERN NSString * const NSImageNameStatusNone NS_AVAILABLE_MAC(10_6);
-
 APPKIT_EXTERN NSString * const NSImageNameShareTemplate NS_AVAILABLE_MAC(10_8);
 
+/* These images are appropriate for use only in Touch Bar items.
+ */
+APPKIT_EXTERN NSString * const NSImageNameTouchBarAddDetailTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarAddTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarAlarmTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarAudioInputMuteTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarAudioInputTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarAudioOutputMuteTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarAudioOutputVolumeHighTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarAudioOutputVolumeLowTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarAudioOutputVolumeMediumTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarAudioOutputVolumeOffTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarBookmarksTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarColorPickerFill NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarColorPickerFont NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarColorPickerStroke NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarCommunicationAudioTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarCommunicationVideoTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarComposeTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarDeleteTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarDownloadTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarEnterFullScreenTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarExitFullScreenTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarFastForwardTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarFolderCopyToTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarFolderMoveToTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarFolderTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarGetInfoTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarGoBackTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarGoDownTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarGoForwardTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarGoUpTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarHistoryTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarIconViewTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarListViewTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarMailTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarNewFolderTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarNewMessageTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarOpenInBrowserTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarPauseTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarPlayheadTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarPlayPauseTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarPlayTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarQuickLookTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarRecordStartTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarRecordStopTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarRefreshTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarRewindTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarRotateLeftTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarRotateRightTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarSearchTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarShareTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarSidebarTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarSkipAhead15SecondsTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarSkipAhead30SecondsTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarSkipAheadTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarSkipBack15SecondsTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarSkipBack30SecondsTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarSkipBackTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarSkipToEndTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarSkipToStartTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarSlideshowTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarTagIconTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarTextBoldTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarTextBoxTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarTextCenterAlignTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarTextItalicTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarTextJustifiedAlignTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarTextLeftAlignTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarTextListTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarTextRightAlignTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarTextStrikethroughTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarTextUnderlineTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarUserAddTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarUserGroupTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarUserTemplate NS_AVAILABLE_MAC(10_12_1);
+
+/* If you have a volume indicator, use NSImageNameTouchBarAudioOutputVolume{Off,Low,Medium,High}Template, which align the speaker correctly.  For volume controls, use NSImageNameTouchBarVolume{Down,Up}Template.
+ */
+APPKIT_EXTERN NSString * const NSImageNameTouchBarVolumeDownTemplate NS_AVAILABLE_MAC(10_12_1);
+APPKIT_EXTERN NSString * const NSImageNameTouchBarVolumeUpTemplate NS_AVAILABLE_MAC(10_12_1);
+
 NS_ASSUME_NONNULL_END

