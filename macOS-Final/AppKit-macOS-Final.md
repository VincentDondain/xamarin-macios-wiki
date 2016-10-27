#AppKit.framework

``` diff
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
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImageView.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImageView.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImageView.h	2016-08-11 21:43:44.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSImageView.h	2016-10-10 22:25:11.000000000 -0400
@@ -11,10 +11,11 @@
 NS_ASSUME_NONNULL_BEGIN
 
 @interface NSImageView : NSControl <NSAccessibilityImage> {
-    /*All instance variables are private*/
+    /* All instance variables are private */
     struct __IVFlags {
         unsigned int _hasImageView:1;
-        unsigned int _unused:25;
+        unsigned int _usesCachedImage:1;
+        unsigned int _unused:24;
         unsigned int _rejectsMultiFileDrops:1;
         unsigned int _compatibleScalingAndAlignment:1;
         unsigned int _reserved:1;
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPanGestureRecognizer.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPanGestureRecognizer.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPanGestureRecognizer.h	2016-08-11 21:43:44.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPanGestureRecognizer.h	2016-10-10 22:25:11.000000000 -0400
@@ -42,4 +42,8 @@
 
 @end
 
+@interface NSPanGestureRecognizer (NSTouchBar)
+@property NSInteger numberOfTouchesRequired NS_AVAILABLE_MAC(10_12_1);
+@end
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopoverTouchBarItem.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopoverTouchBarItem.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopoverTouchBarItem.h	1969-12-31 19:00:00.000000000 -0500
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopoverTouchBarItem.h	2016-10-12 19:14:44.000000000 -0400
@@ -0,0 +1,89 @@
+/*
+ NSPopoverTouchBarItem.h
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
+@interface NSPopoverTouchBarItem : NSTouchBarItem {
+@private
+    NSTouchBar *_popoverTouchBar;
+    NSTouchBar *_pressAndHoldTouchBar;
+    
+    id _overlay;
+    
+    NSString *_customizationLabel;
+    
+    NSView *_collapsedRepresentation;
+    
+    NSImage *_collapsedRepresentationImage;
+    NSString *_collapsedRepresentationLabel;
+    
+    unsigned _showsCloseButton:1;
+    unsigned _showsControlStrip:1;
+    unsigned _collapsedRepresentationChevronBehavior:2;
+#if !__OBJC2__
+    unsigned _popoverTouchBarItemReservedFlags: 28 __unused;
+    void *_popoverTouchBarItemReserved[3] __unused;
+#endif /* !__OBJC2__ */
+}
+
+/*
+    The touch bar displayed when this item is "popped." By default this is an empty touch bar that cannot be customized. This property is archived.
+*/
+@property (strong) NSTouchBar *popoverTouchBar;
+
+/*
+    The localized string labelling this item during user customization. The default value is the empty string. This property is archived.
+*/
+@property (readwrite, copy, null_resettable) NSString *customizationLabel;
+
+/*
+    The view displayed when the item is in its hosted touch bar. By default, this is an NSButton whose target is this popover item, whose action is showPopover:, and whose image and title are bound to this item's collapsedRepresentationImage and collapsedRepresentationLabel respectively. This property is archived.
+*/
+@property (strong) __kindof NSView *collapsedRepresentation;
+
+/*
+    The image displayed by the button used by default for the default collapsed representation. If the collapsedRepresentation button has been replaced by a different view, this property may not have any effect. This property is archived.
+*/
+@property (strong, nullable) NSImage *collapsedRepresentationImage;
+
+/*
+    The localized string displayed by the button used by default for the default collapsed representation. If the collapsedRepresentation button has been replaced by a different view, this property may not have any effect. This property is archived.
+*/
+@property (strong) NSString *collapsedRepresentationLabel;
+
+/*
+    A touchbar to be used exclusively for press-and-hold popovers. This touch bar can be the same as the one used for "popoverTouchBar" property, but does not have to be. When non-nil this touch bar will be displayed while the user holds their finger down on the collapsed representation and released when the user raises their finger. This tracking behavior is automatic, but popovers with custom collapsed representations will still need to send -showPopover: to start tracking.
+
+    This property is archived.
+*/
+@property (strong, nullable) NSTouchBar *pressAndHoldTouchBar;
+
+/*
+    When YES, automatically displays a close button in the popover. When NO it is the responsibility of the client to dismiss the popover.
+*/
+@property BOOL showsCloseButton;
+
+/*
+    Replaces the main touch bar with this item's popover touch bar. If this item is not visible, this method will have no effect. If this item ceases to be visible, the popover touch bar will automatically be ordered out.
+*/
+- (void)showPopover:(nullable id)sender;
+
+/*
+    This method will restore the previously visible main touch bar. This method can be invoked explicitly to order out a popover if interacting with an item inside it should close it.
+*/
+- (void)dismissPopover:(nullable id)sender;
+
+/* 
+    Returns a new gesture recognizer, already wired up to send this popover -showPopover:. It is the callers responsibility to attach this GR to a custom collapsedRepresentation view 
+*/
+- (NSGestureRecognizer *)makeStandardActivatePopoverGestureRecognizer;
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPressGestureRecognizer.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPressGestureRecognizer.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPressGestureRecognizer.h	2016-08-11 21:43:44.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPressGestureRecognizer.h	2016-10-10 22:25:11.000000000 -0400
@@ -34,6 +34,7 @@
 */
 @property CGFloat allowableMovement; // in screen points. Defaults to double-click distance
 
+@property NSInteger numberOfTouchesRequired NS_AVAILABLE_MAC(10_12_1);
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScrubber.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScrubber.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScrubber.h	1969-12-31 19:00:00.000000000 -0500
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScrubber.h	2016-10-10 22:25:11.000000000 -0400
@@ -0,0 +1,228 @@
+/*
+ NSScrubber.h
+ Application Kit
+ Copyright (c) 2016, Apple Inc.
+ All rights reserved.
+ */
+
+#import <AppKit/NSControl.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class NSScrubber, NSScrubberItemView, NSScrubberSelectionView, NSScrubberLayout, NSPanGestureRecognizer, NSPressGestureRecognizer, NSButton, NSNib;
+
+#pragma mark Data Source & Delegate Protocols
+
+@protocol NSScrubberDataSource <NSObject>
+@required
+- (NSInteger)numberOfItemsForScrubber:(NSScrubber *)scrubber NS_AVAILABLE_MAC(10_12_1);
+- (__kindof NSScrubberItemView *)scrubber:(NSScrubber *)scrubber viewForItemAtIndex:(NSInteger)index NS_AVAILABLE_MAC(10_12_1);
+@end
+
+@protocol NSScrubberDelegate <NSObject>
+@optional
+- (void)scrubber:(NSScrubber *)scrubber didSelectItemAtIndex:(NSInteger)selectedIndex NS_AVAILABLE_MAC(10_12_1);
+- (void)scrubber:(NSScrubber *)scrubber didHighlightItemAtIndex:(NSInteger)highlightedIndex NS_AVAILABLE_MAC(10_12_1);
+- (void)scrubber:(NSScrubber *)scrubber didChangeVisibleRange:(NSRange)visibleRange NS_AVAILABLE_MAC(10_12_1);
+
+- (void)didBeginInteractingWithScrubber:(NSScrubber *)scrubber NS_AVAILABLE_MAC(10_12_1);
+- (void)didFinishInteractingWithScrubber:(NSScrubber *)scrubber NS_AVAILABLE_MAC(10_12_1);
+- (void)didCancelInteractingWithScrubber:(NSScrubber *)scrubber NS_AVAILABLE_MAC(10_12_1);
+@end
+
+#pragma mark - Associated Types
+
+/*!
+ * @typedef NSScrubberMode
+ * @discussion Determines the interaction mode for a NSScrubber control.
+ *
+ * @const NSScrubberModeFixed Panning over the control does not scroll, but instead highlights the element under the user’s finger. The highlighted element is selected the end of the gesture. If the gesture begins on top of the selected element, or if the @c continuous property is set to @c YES, the selection is changed immediately as the user pans.
+ * @const NSScrubberModeFree  Panning over the control freely scrolls the scrubber content. Items are selected by tapping or pressing them without panning. If the @c continuous property is set to @c YES, the control automatically selects items as they scroll under the axis specified by the @c itemAlignment property; if @c itemAlignment is @c NSScrubberAlignmentNone, it is interpreted as @c NSScrubberAlignmentCenter for this purpose.
+ */
+typedef NS_ENUM(NSInteger, NSScrubberMode) {
+    NSScrubberModeFixed = 0,
+    NSScrubberModeFree
+} NS_ENUM_AVAILABLE_MAC(10_12_1);
+
+/*!
+ * @typedef NSScrubberAlignment
+ * @discussion NSScrubberAlignment specifies the preferred alignment of elements within the control.
+ *
+ * @const NSScrubberAlignmentNone      Specifies no preference for item alignment.
+ * @const NSScrubberAlignmentLeading   Specifies that an item will be leading-aligned within the control.
+ * @const NSScrubberAlignmentTrailing  Specifies that an item will be trailing-aligned within the control.
+ * @const NSScrubberAlignmentCenter    Specifies that an item will be center-aligned within the control.
+ */
+typedef NS_ENUM(NSInteger, NSScrubberAlignment) {
+    NSScrubberAlignmentNone = 0,
+    NSScrubberAlignmentLeading,
+    NSScrubberAlignmentTrailing,
+    NSScrubberAlignmentCenter
+} NS_ENUM_AVAILABLE_MAC(10_12_1);
+
+/*!
+ * @class NSScrubberSelectionStyle
+ * @abstract @c NSScrubberSelectionStyle is an abstract class that provides decorative accessory views for selected and highlighted items within a NSScrubber control. Class properties provide convenient access to built-in styles. For a completely custom style, subclassers can override @c -makeSelectionView to create and configure arbitrary @c NSScrubberSelectionView subclasses.
+ *
+ */
+NS_CLASS_AVAILABLE_MAC(10_12_1)
+@interface NSScrubberSelectionStyle : NSObject <NSCoding>
+
+#pragma mark Built-in Styles
+
+@property (class, strong, readonly) NSScrubberSelectionStyle *outlineOverlayStyle;
+@property (class, strong, readonly) NSScrubberSelectionStyle *roundedBackgroundStyle;
+
+#pragma mark Initialization & View Creation
+
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
+
+- (nullable __kindof NSScrubberSelectionView *)makeSelectionView;
+
+@end
+
+#pragma mark - Scrubber Control
+
+/*!
+ * @class NSScrubber
+ * @abstract @c NSScrubber is a control designed for the Touch Bar environment. 
+ *
+ * @c NSScrubber arranges a finite number of "items" (represented by views of type @c NSScrubberItemView ) according to a layout object (see @c NSScrubberLayout ), and provides several methods for navigating and selecting those items.
+ *
+ * Clients provide data to @c NSScrubber via a data source object (see the @c NSScrubberDataSource protocol) and react to user interaction via a delegate object (see the @c NSScrubberDelegate protocol).
+ *
+ */
+NS_CLASS_AVAILABLE_MAC(10_12_1)
+@interface NSScrubber : NSView {
+@private
+    id _delegate;
+    id _dataSource;
+    id _tx;
+
+    NSScrollView *_scrollView;
+    NSView *_translationView;
+    NSPanGestureRecognizer   *_scrubGestureRecognizer;
+    NSPanGestureRecognizer   *_scrollGestureRecognizer;
+    NSPressGestureRecognizer *_pressGestureRecognizer;
+    
+    NSButton *_arrowLeft;
+    NSButton *_arrowRight;
+    
+    NSView  *_backgroundView;
+    NSColor *_backgroundColor;
+    
+    NSScrubberAlignment _itemAlignment;
+    NSScrubberMode _mode;
+    
+    id _autoscrollLink;
+    NSPoint _autoscrollEffectivePoint;
+    CGFloat _autoscrollRatio;
+    CGFloat _autoscrollVelocity;
+    NSTimeInterval _autoscrollBasis;
+    
+    unsigned int _isInteracting:1;
+    unsigned int _isMovingSelection:1;
+    unsigned int _continuous:1;
+    unsigned int _ignoresTouches:1;
+    unsigned int _trackingChangedItem:1;
+    unsigned int _setFloating:1;
+    unsigned int _reservedFlags:26 __unused;
+    
+#ifndef __OBJC2__
+    id _reserved __unused;
+#endif
+}
+
+#pragma mark Properties
+
+@property (weak, nullable) id<NSScrubberDataSource> dataSource;
+@property (weak, nullable) id<NSScrubberDelegate> delegate;
+@property (strong) __kindof NSScrubberLayout *scrubberLayout;
+
+/// Returns the number of items represented by the scrubber control.
+@property (readonly) NSInteger numberOfItems;
+
+/// The index of the currently highlighted item within the control. If there is no highlighted item, the value of this property is (-1).
+@property (readonly) NSInteger highlightedIndex;
+
+/// The index of the selected item within the control. If there is no selected item, the value of this property is (-1). Setting this property through the animator proxy will animate the selection change. Programmatic selection changes do not trigger delegate callbacks.
+@property NSInteger selectedIndex;
+
+/// Describes the interaction mode for the scrubber control. See the @c NSScrubberMode enumeration for a list of possible values. The default value is @c NSScrubberModeFixed.
+@property NSScrubberMode mode;
+
+/// If the value of @c itemAlignment is not @c NSScrubberAlignmentNone, the scrubber will ensure that some item rests at the preferred alignment within the control following a scrolling or paging interaction. The default value is @c NSScrubberAlignmentNone.
+@property NSScrubberAlignment itemAlignment;
+
+/// When @c continuous is @c YES, panning over the control in @c NSScrubberModeFixed will immediately select the item under the user's finger, and scrolling in @c NSScrubberModeFree will continuously select items as they pass through the current @c itemAlignment. The default is @c NO.
+@property (getter=isContinuous) BOOL continuous;
+
+/// When @c floatsSelectionViews is @c YES, the selection decorations provided by @c selectionBackgroundStyle and @c selectionOverlayStyle will smoothly float between selected items, rather than animating their entrance/exit in-place. The default is @c NO.
+@property BOOL floatsSelectionViews;
+
+/// Specifies a style of decoration to place behind items that are selected and/or highlighted. The default value is @c nil, indicating no built-in background decoration.
+@property (strong, nullable) NSScrubberSelectionStyle *selectionBackgroundStyle;
+
+/// Specifies a style of decoration to place above items that are selected and/or highlighted. The default value is @c nil, indicating no built-in overlay decoration.
+@property (strong, nullable) NSScrubberSelectionStyle *selectionOverlayStyle;
+
+/// If @c showsArrowButtons is @c YES, the control provides leading and trailing arrow buttons. Tapping an arrow button moves the selection index by one element; pressing and holding repeatedly moves the selection. The default is @c NO.
+@property BOOL showsArrowButtons;
+
+/// If @c showsAdditionalContentIndicators is @c YES, the control will draw a fade effect to indicate that there is additional unscrolled content. The default is @c NO.
+@property BOOL showsAdditionalContentIndicators;
+
+/// If set, @c backgroundColor is displayed behind the scrubber content. The background color is suppressed if the scrubber is assigned a non-nil @c backgroundView. The default value is @c nil.
+@property (copy, nullable) NSColor *backgroundColor;
+
+/// If non-nil, the @c backgroundView is displayed below the scrubber content. The view's layout is managed by @c NSScrubber to match the content area. If this property is non-nil, the @c backgroundColor property has no effect. The default value is @c nil.
+@property (strong, nullable) NSView *backgroundView;
+
+#pragma mark Initialization
+
+- (instancetype)initWithFrame:(NSRect)frameRect NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
+
+#pragma mark Data Manipulation
+
+/// Invalidate all data within the scrubber control, triggering a reload of all content, and clearing the current selection.
+- (void)reloadData;
+
+/// Updates inside the @c performSequentialBatchUpdates block are processed and displayed all at once, including insertion, removal, moving, reloading items, and changing the selected index. Changes are performed iteratively using the same semantics as @c NSMutableArray. NSScrubber expects its dataSource to reflect the changes made inside @c -performSequentialBatchUpdates: immediately after the @c updateBlock finishes executing.
+- (void)performSequentialBatchUpdates:(void(NS_NOESCAPE ^)(void))updateBlock;
+
+/// Inserts new items at the specified indexes. NSScrubber will request views for each new index from the @c dataSource. This method uses the same semantics as @c NSMutableArray; each index in the set specifies the destination index after all previous insertions have occurred. Therefore, an NSIndexSet of [1,2,3] will result in three new contiguous items.
+- (void)insertItemsAtIndexes:(NSIndexSet *)indexes;
+
+/// Removes the items at the specified indexes. This method uses the same semantics as @c NSMutableArray.
+- (void)removeItemsAtIndexes:(NSIndexSet *)indexes;
+
+/// Reloads the items at the specified indexes. NSScrubber will request new views for each item and smoothly crossfade between them before discarding the original views.
+- (void)reloadItemsAtIndexes:(NSIndexSet *)indexes;
+
+/// Moves an item from one index to another. @c oldIndex refers to the item's index prior to the movement, whereas @c newIndex refers to the item's final location.
+- (void)moveItemAtIndex:(NSInteger)oldIndex toIndex:(NSInteger)newIndex;
+
+#pragma mark Interaction
+
+/// Scrolls an item to a given alignment within the control. If @c NSScrubberAlignmentNone is provided, then the control scrolls the minimum amount necessary to make the item visible. Scrolling is animated if called on the animator proxy.
+- (void)scrollItemAtIndex:(NSInteger)index toAlignment:(NSScrubberAlignment)alignment;
+
+/// Returns the @c NSScrubberItemView for the given index, if one currently exists; returns @c nil otherwise.
+- (nullable __kindof NSScrubberItemView *)itemViewForItemAtIndex:(NSInteger)index;
+
+#pragma mark Item Reuse Queue
+
+/// Registers a @c NSScrubberItemView class to be instantiated for the given @c itemIdentifier. Raises an exception if @c itemViewClass is not a subclass of @c NSScrubberItemView. Passing @c nil for @c itemViewClass removes a previous registration. Registrations made through this method do not persist through NSCoding.
+- (void)registerClass:(nullable Class)itemViewClass forItemIdentifier:(NSString *)itemIdentifier;
+
+/// Register a nib to be instantiated for the given @c itemIdentifier. The nib must contain a top-level object which is a subclass of NSScrubberItemView; otherwise, @c -makeItemWithIdentifier: may return @c nil for this identifier. Passing @c nil for @c nib removes a previous registration.
+- (void)registerNib:(nullable NSNib *)nib forItemIdentifier:(NSString *)itemIdentifier;
+
+/// Creates or reuses a @c NSScrubberItemView corresponding to the provided @c itemIdentifier. @c NSScrubber searches, in order: the reuse queue, the list of registered classes, and then the list of registered nibs. If the reuse queue is empty, and there is no Class or Interface Builder archive registered for the @c itemIdentifier, this method returns @c nil.
+- (nullable __kindof NSScrubberItemView *)makeItemWithIdentifier:(NSString *)itemIdentifier owner:(nullable id)owner;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScrubberItemView.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScrubberItemView.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScrubberItemView.h	1969-12-31 19:00:00.000000000 -0500
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScrubberItemView.h	2016-10-10 22:25:11.000000000 -0400
@@ -0,0 +1,116 @@
+/*
+ NSScrubberItemView.h
+ Application Kit
+ Copyright (c) 2016, Apple Inc.
+ All rights reserved.
+ */
+
+#import <AppKit/NSImageCell.h>
+#import <AppKit/NSView.h>
+#import <os/lock.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class NSScrubberLayoutAttributes, NSTextField, NSImageView;
+
+#pragma mark - Arranged View
+
+NS_CLASS_AVAILABLE_MAC(10_12_1)
+@interface NSScrubberArrangedView : NSView {
+@private
+    os_unfair_lock _flagLock;
+    unsigned int _selected:1;
+    unsigned int _highlighted:1;
+#if !__OBJC2__
+    unsigned int _reservedArrangedViewFlags:30 __unused;
+    void *_arrangedViewReserved[3] __unused;
+#endif
+}
+
+@property (getter=isSelected)    BOOL selected;
+@property (getter=isHighlighted) BOOL highlighted;
+
+- (void)applyLayoutAttributes:(__kindof NSScrubberLayoutAttributes *)layoutAttributes NS_REQUIRES_SUPER;
+
+@end
+
+#pragma mark - Selection View
+
+/*!
+ @class NSScrubberSelectionView
+ @abstract The base view class for all selection decorations used by the @c NSScrubber control.
+ */
+NS_CLASS_AVAILABLE_MAC(10_12_1)
+@interface NSScrubberSelectionView : NSScrubberArrangedView {
+#if !__OBJC2__
+    void *_selectionViewReserved[4] __unused;
+#endif
+}
+@end
+
+#pragma mark - Item Views
+
+/*!
+ @class NSScrubberItemView
+ @abstract The base view class that is arranged by a @c NSScrubber control.
+ */
+NS_CLASS_AVAILABLE_MAC(10_12_1)
+@interface NSScrubberItemView : NSScrubberArrangedView {
+@private
+    id _background;
+    id _foreground;
+    id _maskOne;
+    id _maskTwo;
+    unsigned int _edge:2;
+#if !__OBJC2__
+    unsigned int _scrubberItemViewReservedFlags:30 __unused;
+    void *_scrubberItemViewReserved[3] __unused;
+#endif
+}
+
+@end
+
+#pragma mark Text Item
+
+/*!
+ @class NSScrubberTextItemView
+ @abstract A simple @c NSScrubberItemView for displaying text. The -fittingSize method can be used to measure the smallest size for the view which fits the title without truncating.
+ */
+NS_CLASS_AVAILABLE_MAC(10_12_1)
+@interface NSScrubberTextItemView : NSScrubberItemView {
+@private
+    NSTextField *_textField;
+#if !__OBJC2__
+    void *_scrubberTextItemViewReserved[4] __unused;
+#endif
+}
+
+@property (strong, readonly) NSTextField *textField;
+@property (copy) NSString *title;
+
+@end
+
+#pragma mark Image Item
+
+/*!
+ @class NSScrubberTextItemView
+ @abstract A simple @c NSScrubberItemView for displaying an image. 
+ @discussion If the provided image is larger than the view's frame, it is scaled proportionally to fill the entire frame. The cropped portion of the image is determined by the @c imageAlignment property.
+ */
+NS_CLASS_AVAILABLE_MAC(10_12_1)
+@interface NSScrubberImageItemView : NSScrubberItemView {
+@private
+    NSImageView *_imageView;
+    NSImageAlignment _alignment;
+#if !__OBJC2__
+    void *_scrubberImageItemViewReserved[4] __unused;
+#endif
+}
+
+@property (strong, readonly) NSImageView *imageView;
+@property (copy) NSImage *image;
+@property NSImageAlignment imageAlignment;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScrubberLayout.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScrubberLayout.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScrubberLayout.h	1969-12-31 19:00:00.000000000 -0500
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSScrubberLayout.h	2016-10-10 22:25:11.000000000 -0400
@@ -0,0 +1,157 @@
+/*
+ NSScrubberLayout.h
+ Application Kit
+ Copyright (c) 2016, Apple Inc.
+ All rights reserved.
+ */
+
+#import <Foundation/NSGeometry.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class NSScrubber, NSScrubberFlowLayout, NSIndexSet;
+@protocol NSScrubberDelegate;
+
+#pragma mark - Layout Attributes
+
+/*!
+ @class NSScrubberLayoutAttributes
+ @abstract @c NSScrubberLayoutAttributes describes the layout of a single @c NSScrubber item.
+ @discussion @c NSScrubberLayout objects transact in terms of @c NSScrubberLayoutAttributes. @c NSScrubberLayoutAttributes can be subclassed if a layout object wants to include more layout information than the base implementation provides. Subclasses of @c NSScrubberLayoutAttributes must implement @c isEqual:, @c hash, and the @c NSCopying protocol.
+ */
+NS_CLASS_AVAILABLE_MAC(10_12_1)
+@interface NSScrubberLayoutAttributes : NSObject <NSCopying> {
+@private
+    NSInteger _itemIndex;
+    NSRect _frame;
+    CGFloat _alpha;
+#ifndef __OBJC2__
+    id _reserved[3] __unused;
+#endif
+}
+
+@property NSInteger itemIndex;
+@property NSRect frame;
+@property CGFloat alpha;
+
++ (instancetype)layoutAttributesForItemAtIndex:(NSInteger)index;
+
+@end
+
+#pragma mark - Base Layout Object
+
+/*!
+ @class NSScrubberLayout
+ @abstract @c NSScrubberLayout is an abstract class that describes the layout of items within a @c NSScrubber control.
+ */
+NS_CLASS_AVAILABLE_MAC(10_12_1)
+@interface NSScrubberLayout : NSObject <NSCoding> {
+@private
+    id _private;
+    unsigned int _dirty:1;
+    unsigned int _unprepared:1;
+    unsigned int _reservedFlags:30 __unused;
+}
+
+#pragma mark Base Implementation
+/* 
+ The following properties and methods are provided by the base implementation
+ */
+
+/// Specifies a class for describing layout attributes. By default, this is @c NSScrubberLayoutAttributes, but subclasses may override this method to use a custom subclass of @c NSScrubberLayoutAttributes.
++ (Class)layoutAttributesClass;
+
+/// The NSScrubber control that this layout is assigned to, or @c nil if the receiver is not assigned to a scrubber.
+@property (weak, nullable, readonly) NSScrubber *scrubber;
+
+/// The currently visible rectangle, in the coordinate space of the scrubber content. Returns @c NSZeroRect if the receiver is not assigned to a scrubber.
+@property (readonly) NSRect visibleRect;
+
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
+
+/// Signals that layout has been invalidated and the NSScrubber should run a fresh layout pass. Subclasses may define more granular invalidation methods suitable for their own data structures, but those methods should always call up to -invalidateLayout.
+- (void)invalidateLayout NS_REQUIRES_SUPER;
+
+#pragma mark Subclassing Hooks
+/* 
+ The following methods should be implemented by subclasses.
+ */
+
+/// Following any invalidation in layout, @c NSScrubber will call @c prepareLayout on its layout object prior to requesting any other layout information. Subclasses should use this method to perform upfront calculations and caching. The base implementation of this method does nothing.
+- (void)prepareLayout;
+
+/// Returns the content size for all elements within the scrubber. The base implementation returns @c NSZeroSize.
+- (NSSize)scrubberContentSize;
+
+/// Returns the layout attributes for a single item within the scrubber. The base implementation returns @c nil.
+- (nullable __kindof NSScrubberLayoutAttributes *)layoutAttributesForItemAtIndex:(NSInteger)index;
+
+/// Returns the set of layout attributes for all items within the provided rectangle. The base implementation returns an empty set.
+- (NSSet<__kindof NSScrubberLayoutAttributes *> *)layoutAttributesForItemsInRect:(NSRect)rect;
+
+/// If @c YES, the scrubber will invalidate its layout when the selection changes. The default value is @c NO. Subclasses should return @c YES if the selection index affects the item layout.
+- (BOOL)shouldInvalidateLayoutForSelectionChange;
+
+/// If @c YES, the scrubber will invalidate its layout when an item is highlighted. The default value is @c NO. Subclasses should return @c YES if the highlight state affects the item layout.
+- (BOOL)shouldInvalidateLayoutForHighlightChange;
+
+/// If @c YES, the scrubber will invalidate its layout in response to a change in the visible region. The default value is @c NO. Subclasses which rely on the size or origin of the visible region should return @c YES.
+- (BOOL)shouldInvalidateLayoutForChangeFromVisibleRect:(NSRect)fromVisibleRect toVisibleRect:(NSRect)toVisibleRect;
+
+/// If @c YES, the layout object will automatically have its inputs and outputs mirrored in right-to-left interfaces. The default value is @c YES. Subclasses that wish to handle RTL layout manually should return @c NO.
+- (BOOL)automaticallyMirrorsInRightToLeftLayout;
+
+@end
+
+#pragma mark - Flow Layout
+
+@protocol NSScrubberFlowLayoutDelegate <NSScrubberDelegate>
+@optional
+- (NSSize)scrubber:(NSScrubber *)scrubber layout:(NSScrubberFlowLayout *)layout sizeForItemAtIndex:(NSInteger)itemIndex;
+@end
+
+/*!
+ @class NSScrubberFlowLayout
+ @abstract @c NSScrubberFlowLayout is a concrete layout object that arranges items end-to-end in a linear strip. It supports a fixed inter-item spacing and both fixed- and variable-sized items.
+ @discussion If the associated scrubber's @c delegate conforms to @c NSScrubberFlowLayoutDelegate, and it implements the @c scrubber:layout:sizeForItemAtIndex: method, @c NSScrubberFlowLayout will obtain the item size from the delegate. If the delegate does not implement that method, or if the method returns @c NSZeroSize, it will fall back to using the layout's @c itemSize property. By default, NSScrubberFlowLayout does not invalidate its layout on selection change, highlight change, or visible rectangle change.
+ */
+NS_CLASS_AVAILABLE_MAC(10_12_1)
+@interface NSScrubberFlowLayout : NSScrubberLayout {
+@private
+    id _support;
+    CGFloat _itemSpacing;
+    NSSize _itemSize;
+}
+
+/// The amount of horizontal spacing between items in points. The default value is 0.0.
+@property CGFloat itemSpacing;
+
+/// The frame size for each item, if not provided by the scrubber's delegate. The default value is { 50.0, 30.0 }.
+@property NSSize itemSize;
+
+- (void)invalidateLayoutForItemsAtIndexes:(NSIndexSet *)invalidItemIndexes;
+
+@end
+
+#pragma mark - Proportional Layout
+
+/*!
+ @class NSScrubberProportionalLayout
+ @abstract @c NSScrubberProportionalLayout is a concrete layout object that sizes each item to some fraction of the scrubber's visible size.
+ */
+NS_CLASS_AVAILABLE_MAC(10_12_1)
+@interface NSScrubberProportionalLayout : NSScrubberLayout {
+@private
+    NSInteger _numberOfVisibleItems;
+}
+
+/// The number of items that should fit within the scrubber's viewport at once.
+@property NSInteger numberOfVisibleItems;
+
+- (instancetype)initWithNumberOfVisibleItems:(NSInteger)numberOfVisibleItems NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSegmentedControl.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSegmentedControl.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSegmentedControl.h	2016-08-11 21:43:44.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSegmentedControl.h	2016-10-10 22:25:11.000000000 -0400
@@ -79,6 +79,8 @@
  */
 @property (readonly) double doubleValueForSelectedSegment NS_AVAILABLE_MAC(10_10_3);
 
+@property (nullable, copy) NSColor *selectedSegmentBezelColor NS_AVAILABLE_MAC(10_12_1); // The color of the selected segment's bevel, in appearances that support it
+
 @end
 
 @interface NSSegmentedControl (NSSegmentedControlConvenience)
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSharingServicePickerTouchBarItem.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSharingServicePickerTouchBarItem.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSharingServicePickerTouchBarItem.h	1969-12-31 19:00:00.000000000 -0500
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSharingServicePickerTouchBarItem.h	2016-10-10 22:25:11.000000000 -0400
@@ -0,0 +1,49 @@
+/*
+    NSSharingServicePickerTouchBarItem.h
+    Application Kit
+    Copyright (c) 2016, Apple Inc.
+    All rights reserved.
+*/
+
+#import <AppKit/NSTouchBarItem.h>
+#import <AppKit/NSSharingService.h>
+
+@protocol NSSharingServicePickerTouchBarItemDelegate;
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class NSTouchBarSharingServicePickerViewController, NSPopoverTouchBarItem;
+
+NS_CLASS_AVAILABLE_MAC(10_12_1)
+@interface NSSharingServicePickerTouchBarItem : NSTouchBarItem {
+@private
+    __kindof NSPopoverTouchBarItem *_internalPopoverItem;
+    __weak NSTouchBarSharingServicePickerViewController *_pickerViewController;
+    NSString *_customizationLabel;
+    __weak id<NSSharingServicePickerTouchBarItemDelegate> _delegate;
+
+#if !__OBJC2__
+    void *_sharingServicePickerTouchBarItemReserved[4] __unused;
+#endif
+}
+
+@property (weak) id<NSSharingServicePickerTouchBarItemDelegate> delegate;
+
+/* Enables or disabled the sharing button; if the popover is shown, it will first be closed.
+ */
+@property (getter=isEnabled) BOOL enabled;
+
+/* Get/set the button title and image. By default, the button title is an empty string, and the button image is a share picker image. */
+@property (copy) NSString *buttonTitle;
+@property (nullable, retain) NSImage *buttonImage;
+
+@end
+
+@protocol NSSharingServicePickerTouchBarItemDelegate <NSSharingServicePickerDelegate>
+@required
+/* Return the items that represent the objects to be shared. They must conform to the <NSPasteboardWriting> protocol or be an NSItemProvider. (e.g. NSString, NSImage, NSURL, etc.). */
+- (NSArray *)itemsForSharingServicePickerTouchBarItem:(NSSharingServicePickerTouchBarItem *)pickerTouchBarItem;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSlider.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSlider.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSlider.h	2016-08-11 21:43:44.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSlider.h	2016-10-10 22:25:11.000000000 -0400
@@ -21,6 +21,8 @@
 - (BOOL)acceptsFirstMouse:(nullable NSEvent *)event;
 @property (readwrite, getter=isVertical) BOOL vertical NS_AVAILABLE_MAC(10_12);
 
+@property (nullable, copy) NSColor *trackFillColor NS_AVAILABLE_MAC(10_12_1); // The color of the filled portion of the track, in appearances that support it
+
 @end
 
 @interface NSSlider (NSSliderVerticalGetter)
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSliderAccessory.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSliderAccessory.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSliderAccessory.h	1969-12-31 19:00:00.000000000 -0500
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSliderAccessory.h	2016-10-10 22:25:11.000000000 -0400
@@ -0,0 +1,65 @@
+/*
+    NSSliderAccessory.h
+    Application Kit
+    Copyright (c) 2016-2016, Apple Inc.
+    All rights reserved.
+ */
+
+#import <AppKit/NSAccessibility.h>
+#import <Foundation/Foundation.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class NSSlider, NSSliderAccessoryBehavior, NSImage;
+
+NS_CLASS_AVAILABLE_MAC(10_12)
+@interface NSSliderAccessory : NSObject <NSCoding, NSAccessibility, NSAccessibilityElement> {
+@private
+    id _content;
+    id _container;
+    NSSliderAccessoryBehavior *_behavior;
+    signed char _enabled: 1;
+
+#if !__OBJC2__
+    unsigned int _sliderAccessoryReservedFlags: 31 __unused;
+    void *_sliderAccessoryReserved[3] __unused;
+#endif /* !__OBJC2__ */
+}
+
+/// Creates an image-based accessory
++ (NSSliderAccessory *)accessoryWithImage:(NSImage *)image;
+
+/// The effect on interaction with the accessory. Defaults to `automaticBehavior`
+@property (copy) NSSliderAccessoryBehavior *behavior;
+
+/// Whether or not the accessory is interactive and draws with an enabled appearance. Defaults to YES.
+@property (getter=isEnabled) BOOL enabled;
+
+@end
+
+
+NS_CLASS_AVAILABLE_MAC(10_12)
+@interface NSSliderAccessoryBehavior : NSObject <NSCoding, NSCopying>
+
+/// The behavior is automatically picked to be the system standard for the slider's current context, e.g. touch bars have `.valueStep` behavior.
+@property (class, readonly, copy) NSSliderAccessoryBehavior *automaticBehavior  NS_SWIFT_NAME(automatic);
+
+/// The value of the slider moves towards the associated value for the accessory with by a delta of the slider's `altIncrementValue`.
+@property (class, readonly, copy) NSSliderAccessoryBehavior *valueStepBehavior NS_SWIFT_NAME(valueStep);
+
+/// The value of the slider is reset to the associated value for the accessory.
+@property (class, readonly, copy) NSSliderAccessoryBehavior *valueResetBehavior NS_SWIFT_NAME(valueReset);
+
+/// The action is sent to the target on interaction. The optional first parameter is an NSSliderAccessory.
++ (NSSliderAccessoryBehavior *)behaviorWithTarget:(nullable id)target action:(SEL)action;
+
+/// The handler block is invoked on interaction. This variant is not codable and will assert in `-encodeWithCoder:`.
++ (NSSliderAccessoryBehavior *)behaviorWithHandler:(void(^)(NSSliderAccessory *))handler;
+
+
+/// Override point for custom subclasses to handle interaction.
+- (void)handleAction:(NSSliderAccessory *)sender;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSliderTouchBarItem.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSliderTouchBarItem.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSliderTouchBarItem.h	1969-12-31 19:00:00.000000000 -0500
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSliderTouchBarItem.h	2016-10-10 22:25:11.000000000 -0400
@@ -0,0 +1,57 @@
+/*
+ NSSliderTouchBarItem.h
+ Application Kit
+ Copyright (c) 2016-2016, Apple Inc.
+ All rights reserved.
+ */
+
+#import <AppKit/NSTouchBarItem.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class NSSliderAccessory, NSSlider;
+
+typedef CGFloat NSSliderAccessoryWidth _NS_TYPED_EXTENSIBLE_ENUM NS_AVAILABLE_MAC(10_12_1);
+/// The default width for slider accessories.
+APPKIT_EXTERN const NSSliderAccessoryWidth NSSliderAccessoryWidthDefault NS_AVAILABLE_MAC(10_12_1);
+/// The standard "wide" width for slider accessories.
+APPKIT_EXTERN const NSSliderAccessoryWidth NSSliderAccessoryWidthWide NS_AVAILABLE_MAC(10_12_1);
+
+NS_CLASS_AVAILABLE_MAC(10_12_1)
+@interface NSSliderTouchBarItem : NSTouchBarItem {
+@private
+    __kindof NSView *_view;
+    id _autounbinder;
+    __weak id _target;
+    SEL _action;
+    NSString *_customizationLabel;
+
+#if !__OBJC2__
+    void *_sliderTouchBarItemReserved[4] __unused;
+#endif /* !__OBJC2__ */
+}
+
+/// The slider displayed by the bar item. It is automatically created, but can be set to a custom subclass. doubleValue, minValue, maxValue, etc can all be read and set through the slider.
+@property (strong) NSSlider *slider;
+
+/// The text label displayed along with the slider. If set to nil, the label will not have space reserved in the item.
+@property (nullable, copy) NSString *label;
+
+/// The accessory that appears on the end of the slider with the minimum value
+@property (strong, nullable) NSSliderAccessory *minimumValueAccessory;
+/// The accessory that appears on the end of the slider with the maximum value
+@property (strong, nullable) NSSliderAccessory *maximumValueAccessory;
+/// The width of the value accessories. Defaults to `.default`, but can be set to `.wide` or a custom value.
+@property NSSliderAccessoryWidth valueAccessoryWidth;
+
+/// The target of the item, notified when the slider or accessories receive user interaction.
+@property (weak, nullable) id target;
+/// The action of the item, called when the slider or accessories receive user interaction.
+@property (nullable) SEL action;
+
+/// The localized string labelling this item during user customization. The default value is empty string.
+@property (readwrite, copy, null_resettable) NSString *customizationLabel;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpellChecker.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpellChecker.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpellChecker.h	2016-08-11 21:43:44.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSSpellChecker.h	2016-10-10 22:25:11.000000000 -0400
@@ -99,6 +99,9 @@
 /* Requests unified text checking in the background.  The return value is a monotonically increasing sequence number that can be used to keep track of requests in flight.  The completion handler will be called (in an arbitrary context) when results are available, with the sequence number and results.  The arguments and results are otherwise the same as for the previous method. */
 - (NSInteger)requestCheckingOfString:(NSString *)stringToCheck range:(NSRange)range types:(NSTextCheckingTypes)checkingTypes options:(nullable NSDictionary<NSString *, id> *)options inSpellDocumentWithTag:(NSInteger)tag completionHandler:(void (^ __nullable)(NSInteger sequenceNumber, NSArray<NSTextCheckingResult *> *results, NSOrthography *orthography, NSInteger wordCount))completionHandler NS_AVAILABLE_MAC(10_6);
 
+/* Requests candidate generation in the background.  The return value is a monotonically increasing sequence number that can be used to keep track of requests in flight.  The completion handler will be called (in an arbitrary context) when results are available, with the sequence number and results. */
+- (NSInteger)requestCandidatesForSelectedRange:(NSRange)selectedRange inString:(NSString *)stringToCheck types:(NSTextCheckingTypes)checkingTypes options:(nullable NSDictionary<NSString *, id> *)options inSpellDocumentWithTag:(NSInteger)tag completionHandler:(void (^ __nullable)(NSInteger sequenceNumber, NSArray<NSTextCheckingResult *> *candidates))completionHandler NS_AVAILABLE_MAC(10_12_1);
+
 /* Provides a menu containing contextual menu items suitable for certain kinds of detected results (notably date/time/address results).  The options dictionary allows clients to pass in information associated with the document.  */
 - (nullable NSMenu *)menuForResult:(NSTextCheckingResult *)result string:(NSString *)checkedString options:(nullable NSDictionary<NSString *, id> *)options atLocation:(NSPoint)location inView:(NSView *)view NS_AVAILABLE_MAC(10_6);
 
@@ -183,6 +186,8 @@
 /* In some cases the next typing should prevent a pending correction (if it is an @, for example).  This method allows clients to recognize these cases in a standardized way. */
 - (BOOL)preventsAutocorrectionBeforeString:(NSString *)string language:(nullable NSString *)language NS_AVAILABLE_MAC(10_12);
 
+/* In some cases the space automatically inserted after an accepted candidate should be deleted when the next text is typed (e.g. if it is a period or comma).  This method allows clients to recognize these cases in a standardized way. */
+- (BOOL)deletesAutospaceBetweenString:(NSString *)precedingString andString:(NSString *)followingString language:(nullable NSString *)language NS_AVAILABLE_MAC(10_12_1);
 
 /* Entries in the availableLanguages list are all available spellchecking languages in user preference order, as described in the spellchecker's info dictionary, usually language abbreviations such as en_US.  The userPreferredLanguages will be a subset of the availableLanguages, as selected by the user for use with spellchecking, in preference order.  If automaticallyIdentifiesLanguages is YES, then text checking will automatically use these as appropriate; otherwise, it will use the language set by setLanguage:.  The older checkSpellingOfString:... and checkGrammarOfString:... methods will use the language set by setLanguage:, if they are called with a nil language argument.  */
 @property (readonly, copy) NSArray<NSString *> *availableLanguages NS_AVAILABLE_MAC(10_5);
@@ -204,6 +209,7 @@
 + (BOOL)isAutomaticDashSubstitutionEnabled NS_AVAILABLE_MAC(10_9);
 + (BOOL)isAutomaticCapitalizationEnabled NS_AVAILABLE_MAC(10_12);
 + (BOOL)isAutomaticPeriodSubstitutionEnabled NS_AVAILABLE_MAC(10_12);
++ (BOOL)isAutomaticTextCompletionEnabled NS_AVAILABLE_MAC(10_12_1);
 
 /* Use of the following methods is discouraged; ordinarily language identification should be allowed to take place automatically, or else a specific language should be passed in to the methods that take such an argument, if the language is known in advance.  -setLanguage: allows programmatic setting of the language to spell-check in, for compatibility use if other methods are called with no language specified.  -setLanguage: accepts any of the language formats used by NSBundle, and tries to find the closest match among the available languages.  If -setLanguage: has been called, then -language will return that match; otherwise, it will return Multilingual if there is more than one element in -userPreferredLanguages, or the one element in that array if there is only one.  */
 
@@ -219,6 +225,7 @@
 APPKIT_EXTERN NSNotificationName const NSSpellCheckerDidChangeAutomaticDashSubstitutionNotification NS_AVAILABLE_MAC(10_9);
 APPKIT_EXTERN NSNotificationName const NSSpellCheckerDidChangeAutomaticCapitalizationNotification NS_AVAILABLE_MAC(10_12);
 APPKIT_EXTERN NSNotificationName const NSSpellCheckerDidChangeAutomaticPeriodSubstitutionNotification NS_AVAILABLE_MAC(10_12);
+APPKIT_EXTERN NSNotificationName const NSSpellCheckerDidChangeAutomaticTextCompletionNotification NS_AVAILABLE_MAC(10_12_1);
 
 
 @interface NSSpellChecker(NSDeprecated)
