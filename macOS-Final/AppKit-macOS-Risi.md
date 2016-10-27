diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextField.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextField.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextField.h	2016-08-11 21:43:44.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextField.h	2016-10-10 22:25:11.000000000 -0400
@@ -55,6 +55,14 @@
 
 @end
 
+#pragma mark NSTextField Touch Bar Item Properties
+@interface NSTextField (NSTouchBar)
+
+@property (getter=isAutomaticTextCompletionEnabled) BOOL automaticTextCompletionEnabled NS_AVAILABLE_MAC(10_12_1);
+@property BOOL allowsCharacterPickerTouchBarItem NS_AVAILABLE_MAC(10_12_1);
+
+@end
+
 @interface NSTextField(NSTextFieldConvenience)
 
 /*!
@@ -94,6 +102,12 @@
 @end
 
 @protocol NSTextFieldDelegate <NSControlTextEditingDelegate>
+@optional
+- (nullable NSArray *)textField:(NSTextField *)textField textView:(NSTextView *)textView candidatesForSelectedRange:(NSRange)selectedRange NS_AVAILABLE_MAC(10_12_1);
+
+- (NSArray<NSTextCheckingResult *> *)textField:(NSTextField *)textField textView:(NSTextView *)textView candidates:(NSArray<NSTextCheckingResult *> *)candidates forSelectedRange:(NSRange)selectedRange NS_AVAILABLE_MAC(10_12_1);
+
+- (BOOL)textField:(NSTextField *)textField textView:(NSTextView *)textView shouldSelectCandidateAtIndex:(NSUInteger)index NS_AVAILABLE_MAC(10_12_1);
 @end
 
 @interface NSTextField(NSDeprecated)
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextView.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextView.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextView.h	2016-08-11 21:43:44.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTextView.h	2016-10-10 22:25:11.000000000 -0400
@@ -456,6 +458,33 @@
 
 @end
 
+
+#pragma mark NSTouchBar support
+/* NSTextView provides support for text formatting and inputting touch bar items. -[NSTextView makeTouchBar] instantiates an NSTouchBar configured based on settings such as -automaticTextCompletionEnabled and -richText. NSTextView conforms to NSTouchBarDelegate and supplies touch bar items via -touchBar:makeItemForIdentifier:.
+ */
+@interface NSTextView (NSTextView_TouchBar) <NSCandidateListTouchBarItemDelegate, NSTouchBarDelegate>
+
+// Enables automatic completion touch bar item. YES by default. When YES, NSTextView displays the candidates for the text selection in its NSCandidateListTouchBarItem returned from -candidateListTouchBarItem. Invokes -updateTouchBarItemIdentifiers.
+@property (getter=isAutomaticTextCompletionEnabled) BOOL automaticTextCompletionEnabled NS_AVAILABLE_MAC(10_12_1);
+- (IBAction)toggleAutomaticTextCompletion:(nullable id)sender NS_AVAILABLE_MAC(10_12_1);
+
+// When Yes, NSTouchBarItemIdentifierCharacterPicker is included in -[NSTouchBar itemIdentifiers] for its touch bar. Default is YES. Invokes -updateTouchBarItemIdentifiers.
+@property BOOL allowsCharacterPickerTouchBarItem NS_AVAILABLE_MAC(10_12_1);
+
+// This message should be sent whenever a property affecting touch bar item states is changed. It updates -itemIdentifiers for its touch bar.
+- (void)updateTouchBarItemIdentifiers NS_AVAILABLE_MAC(10_12_1);
+
+// Updates state of text formatting touch bar items such as NSTouchBarItemIdentifierTextStyle and NSTouchBarItemIdentifierTextAlignment for the receiver based on the current selection.
+- (void)updateTextTouchBarItems NS_AVAILABLE_MAC(10_12_1);
+
+// Updates the candidates for -candidateListTouchBarItem.
+- (void)updateCandidates NS_AVAILABLE_MAC(10_12_1);
+
+// -[NSTextView candidateListTouchBarItem] returns an NSCandidateTouchBarItem instance owned by the receiver. The touch bar item is instantiated in -[NSTextView touchBar:makeItemForIdentifier:] with NSTouchBarItemIdentifierCandidateLit.
+@property (nullable, readonly, strong) NSCandidateListTouchBarItem *candidateListTouchBarItem NS_AVAILABLE_MAC(10_12_1);
+@end
+
+
 @interface NSTextView (NSDeprecated)
 
 // toggleBaseWritingDirection: will be deprecated in favor of the new NSResponder methods makeBaseWritingDirectionNatural:, makeBaseWritingDirectionLeftToRight:, and makeBaseWritingDirectionRightToLeft:, which NSTextView now implements.
@@ -533,6 +562,20 @@
 
 - (nullable NSUndoManager *)undoManagerForTextView:(NSTextView *)view;
 
+
+// Delegate only. Invoked from -updateTouchBarItemIdentifiers before setting the item identifiers for textView's touch bar.
+- (NSArray<NSTouchBarItemIdentifier> *)textView:(NSTextView *)textView shouldUpdateTouchBarItemIdentifiers:(NSArray<NSTouchBarItemIdentifier> *)identifiers NS_AVAILABLE_MAC(10_12_1);
+
+// Delegate only. Provides customized list of candidates to textView.candidateListTouchBarItem. Invoked from -updateCandidates. NSTextView uses the candidates returned from this method and suppress its built-in candidate generation. Returning nil from this delegate method allows NSTextView to query candidates from NSSpellChecker.
+- (nullable NSArray *)textView:(NSTextView *)textView candidatesForSelectedRange:(NSRange)selectedRange NS_AVAILABLE_MAC(10_12_1);
+
+// Delegate only. Allows customizing the candidate list queried from NSSpellChecker.
+- (NSArray<NSTextCheckingResult *> *)textView:(NSTextView *)textView candidates:(NSArray<NSTextCheckingResult *> *)candidates forSelectedRange:(NSRange)selectedRange NS_AVAILABLE_MAC(10_12_1);
+
+// Delegate only. Notifies the delegate that the user selected the candidate at index in -[NSCandidateListTouchBarItem candidates] for textView.candidateListTouchBarItem. When no candidate selected, index is NSNotFound. Returning YES allows textView to insert the candidate into the text storage if it's NSString, NSAttributedString, or NSTextCheckingResult.
+- (BOOL)textView:(NSTextView *)textView shouldSelectCandidateAtIndex:(NSUInteger)index NS_AVAILABLE_MAC(10_12_1);
+
+
 // The following delegate-only methods are deprecated in favor of the more verbose ones above.
 - (BOOL)textView:(NSTextView *)textView clickedOnLink:(null_unspecified id)link NS_DEPRECATED_MAC(10_0, 10_6, "Use -textView:clickedOnLink:atIndex: instead");
 - (void)textView:(NSTextView *)textView clickedOnCell:(null_unspecified id <NSTextAttachmentCell>)cell inRect:(NSRect)cellFrame NS_DEPRECATED_MAC(10_0, 10_6, "Use -textView:clickedOnCell:inRect:atIndex: instead");
@@ -541,6 +584,29 @@
 
 @end
 
+
+#pragma mark Touch Bar Item Identifiers
+/* Standard Touch Bar Item Identifiers */
+// A touch bar item identifier for a control selecting special characters (i.e. Emoji). -[NSTouchBar itemForIdentifier:] recognizes the identifier.
+APPKIT_EXTERN NSTouchBarItemIdentifier const NSTouchBarItemIdentifierCharacterPicker NS_AVAILABLE_MAC(10_12_1);
+
+/* Identifiers recognized by -[NSTextView touchBar:makeItemForIdentifier:] */
+// A touch bar item identifier for a control selecting the text color.
+APPKIT_EXTERN NSTouchBarItemIdentifier const NSTouchBarItemIdentifierTextColorPicker NS_AVAILABLE_MAC(10_12_1);
+
+// A touch bar item identifier for a control selecting the text style.
+APPKIT_EXTERN NSTouchBarItemIdentifier const NSTouchBarItemIdentifierTextStyle NS_AVAILABLE_MAC(10_12_1);
+
+// A touch bar item identifier for a control selecting the text alignment. -[NSTextView touchBarItemForIdentifier:] returns an NSPopoverTouchBarItem.
+APPKIT_EXTERN NSTouchBarItemIdentifier const NSTouchBarItemIdentifierTextAlignment NS_AVAILABLE_MAC(10_12_1);
+
+// A touch bar item identifier for a control inserting the text list style. -[NSTextView touchBarItemForIdentifier:] returns an NSPopoverTouchBarItem.
+APPKIT_EXTERN NSTouchBarItemIdentifier const NSTouchBarItemIdentifierTextList NS_AVAILABLE_MAC(10_12_1);
+
+// A touch bar item identifier for a group of text format controls.
+APPKIT_EXTERN NSTouchBarItemIdentifier const NSTouchBarItemIdentifierTextFormat NS_AVAILABLE_MAC(10_12_1);
+
+
 // NSOldNotifyingTextView -> the old view, NSNewNotifyingTextView -> the new view.  The text view delegate is not automatically registered to receive this notification because the text machinery will automatically switch over the delegate to observe the new first text view as the first text view changes.
 APPKIT_EXTERN NSNotificationName NSTextViewWillChangeNotifyingTextViewNotification;
 
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTouch.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTouch.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTouch.h	2016-08-11 21:43:44.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTouch.h	2016-10-10 22:25:11.000000000 -0400
@@ -24,6 +24,17 @@
     NSTouchPhaseAny             = NSUIntegerMax
 } NS_ENUM_AVAILABLE_MAC(10_7);
 
+typedef NS_ENUM(NSInteger, NSTouchType) {
+    NSTouchTypeDirect,      // A direct touch from a finger (on a screen)
+    NSTouchTypeIndirect,      // An indirect touch (not a screen)
+} NS_ENUM_AVAILABLE_MAC(10_12_1);
+
+typedef NS_OPTIONS(NSUInteger, NSTouchTypeMask) {
+    NSTouchTypeMaskDirect      = (1 <<  NSTouchTypeDirect),      // A direct touch from a finger (on a screen)
+    NSTouchTypeMaskIndirect    = (1 <<  NSTouchTypeIndirect),      // An indirect touch (not a screen)
+} NS_ENUM_AVAILABLE_MAC(10_12_1);
+
+NS_INLINE NSTouchTypeMask NSTouchTypeMaskFromType(NSTouchType type) { return (1 << type); }
 
 /* Unlike the iPhone, NSTouch objects do not persist for the life of the touch.
 */
@@ -66,5 +77,14 @@
 
 @end
 
+@interface NSTouch (NSTouchBar)
+/* A touch can only be one type at a time */
+@property(readonly) NSTouchType type NS_AVAILABLE_MAC(10_12_1);
+
+/* These two methods are only valid for Direct touches. A nil view means the touch location in the root container of touch. */
+- (NSPoint)locationInView:(nullable NSView *)view NS_AVAILABLE_MAC(10_12_1);
+- (NSPoint)previousLocationInView:(nullable NSView *)view NS_AVAILABLE_MAC(10_12_1);
+@end
+
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTouchBar.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTouchBar.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTouchBar.h	1969-12-31 19:00:00.000000000 -0500
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTouchBar.h	2016-10-12 19:14:44.000000000 -0400
@@ -0,0 +1,208 @@
+/*
+ NSTouchBar.h
+ Application Kit
+ Copyright (c) 2015-2016, Apple Inc.
+ All rights reserved.
+*/
+
+#import <AppKit/NSResponder.h>
+#import <AppKit/NSApplication.h>
+#import <AppKit/NSTouchBarItem.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+typedef NSString * NSTouchBarCustomizationIdentifier NS_EXTENSIBLE_STRING_ENUM;
+
+@protocol NSTouchBarDelegate, NSTouchBarProvider;
+
+NS_CLASS_AVAILABLE_MAC(10_12_1)
+@interface NSTouchBar : NSObject <NSCoding> {
+@private
+    id _configuration;
+
+    NSTouchBarItemIdentifier _principalItemIdentifier;
+    
+    NSSet<NSTouchBarItem *> *_templateItems;
+    
+    id <NSTouchBarDelegate> _delegate;
+    
+    NSCache *_itemCache;
+    
+    NSInteger _visibilityCount;
+    
+    unsigned _isBuildingItems:1;
+    
+    unsigned _suppressesLessFocusedTouchBars:1;
+    unsigned _suppressesMoreFocusedTouchBars:1;
+    unsigned _suppressedByLessFocusedTouchBars:1;
+    unsigned _suppressedByMoreFocusedTouchBars:1;
+    
+    id _fbReserved;
+#if !__OBJC2__
+    void *_touchBarReserved[4] __unused;
+#endif /* !__OBJC2__ */
+}
+
+/* 
+    -init is a designated initializer.
+*/
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
+
+/* 
+    -initWithCoder: is also a designated initializer.
+*/
+- (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
+
+/* 
+    A string uniquely identifying this bar for customization purposes. All bars with this identifier will have their items coordinated automatically during customization or instantiation.
+
+    Touch bars lacking a customizationIdentifier are not customizable.
+    
+    This property is archived.
+*/
+@property (copy, nullable) NSTouchBarCustomizationIdentifier customizationIdentifier;
+
+/*
+    The items that are presented in the customization palette for the user to add to the touch bar. These items will be presented to the user in the order specified in this array.
+
+    This property is archived.
+*/
+@property (copy) NSArray<NSTouchBarItemIdentifier> *customizationAllowedItemIdentifiers;
+
+/*
+    Some items are too important to be removed. The corresponding item identifiers should be listed here. During customization the user will be prevented from removing these items from the touch bar.
+    
+    This property is archived.
+*/
+@property (copy) NSArray<NSTouchBarItemIdentifier> *customizationRequiredItemIdentifiers;
+
+/*
+    An array of identifiers specifying the items in this touch bar. When constructing the instantiated items array, the identifiers in this array will be fed through the -itemForIdentifier: method.
+    Item identifiers should be globally unique, excepting NSTouchBarItemIdentifierFixedSpaceSmall, NSTouchBarItemIdentifierFixedSpaceLarge, NSTouchBarItemIdentifierFlexibleSpace, and NSTouchBarItemIdentifierOtherItemsProxy.
+    
+    This array also corresponds to the item ordering for the receiver in the “default set” in the customization palette.
+ 
+    This property is archived.
+*/
+@property (copy) NSArray<NSTouchBarItemIdentifier> *defaultItemIdentifiers;
+
+/*
+    The resolved array of item identifiers. If the bar has not been customized this will match the defaultItemIdentifiers.
+    
+    This property is not archived.
+*/
+@property (copy, readonly) NSArray<NSTouchBarItemIdentifier> *itemIdentifiers;
+
+/*
+    Specifying a principal item identifier communicates that the item with that identifier has special significance to this touch bar. Currently, that item will be placed in the center of the resolved touch row. Note that multiple visible bars may each specify a principal item identifier - but only one of them can have the request honored.
+    
+    This property is archived.
+*/
+@property (copy, nullable) NSTouchBarItemIdentifier principalItemIdentifier;
+
+/*
+    Items in this set are the first step in resolving instantiated items from their identifiers. If an item identifier is specified in the itemIdentifiers array, and an item with that identifier is in this set, it will be added to the items array in the corresponding location.
+ 
+    This property is archived.
+*/
+@property (copy) NSSet<NSTouchBarItem *> *templateItems;
+
+/*
+    The touch bar delegate. The touch bar delegate can dynamically create items.
+    
+    This property is conditionally archived (see -encodeConditionalObject:forKey:.)
+*/
+@property (nullable, weak) id <NSTouchBarDelegate> delegate;
+
+/*
+ Returns an instantiated NSTouchBarItem for the given identifier. Items are resolved from the following locations, in order:
+ * items already in the instantiated items array
+ * items in the defaultTouchBarItems set
+ * items returned from the delegate's -touchBar:makeItemForIdentifier: method
+ * some special identifiers are handled automatically
+ NSTouchBarItemIdentifierFixedSpaceSmall -> NSTouchBar will automatically create a standard small space
+ NSTouchBarItemIdentifierFixedSpaceLarge -> NSTouchBar will automatically create a standard large space
+ NSTouchBarItemIdentifierFlexibleSpace -> NSTouchBar will automatically create a standard flexible space
+ NSTouchBarItemIdentifierOtherItemsProxy -> NSTouchBar will automatically create a special item that acts as a proxy for the items of touch bars closer to the first responder.
+ */
+- (nullable __kindof NSTouchBarItem *)itemForIdentifier:(NSTouchBarItemIdentifier)identifier;
+
+/*
+    When YES, the touch bar is attached to an eligible touch bar provider, and its items are displayable, assuming adequate space.
+    This property is key value observable.
+*/
+@property (readonly, getter=isVisible) BOOL visible;
+
+@end
+
+@protocol NSTouchBarDelegate <NSObject>
+@optional
+/*
+    When constructing the items array, this delegate method will be invoked to construct a touch bar item if that item cannot be found in the defaultItems set.
+*/
+- (nullable NSTouchBarItem *)touchBar:(NSTouchBar *)touchBar makeItemForIdentifier:(NSTouchBarItemIdentifier)identifier;
+@end
+
+/*
+    Touch bars are discovered by searching certain well known components of the application for objects that conform to the NSTouchBarProvider protocol.
+    
+    Some specific objects in a process are searched to discover NSTouchBar providers. In order, these objects are:
+    * the application delegate
+    * the application object itself
+    * the main window’s window controller
+    * the main window’s delegate
+    * the main window itself
+    * the main window’s first responder
+    * the key window’s window controller
+    * the key window’s delegate
+    * the key window itself
+    * the key window’s first responder
+
+    If any of these objects are an NSResponder or a subclass of NSResponder, the responder chain anchored at that object is also searched.
+
+    For example in a complicated, but otherwise standard application, that chain might look like this.
+
+    * Application delegate
+    * Application
+    * key window controller
+    * key window delegate
+    * key window
+    * view controller (closest to root of window)
+    * view (closest to root of window)
+    * intermediate view controllers and views
+    * key window’s first responder’s view controller
+    * key window’s first responder
+
+    Touch bars can be nested by including the special NSTouchBarItemIdentifierOtherItemsProxy item identifier. This allows more broadly scoped touch bars (closer to the app delegate) to also display the contents of more narrowly scoped touch bars (closer to the first responder.) If a touch bar omits the special NSTouchBarItemIdentifierOtherItemsProxy item identifier, it will be hidden if a more narrowly scoped touch bar is provided.
+*/
+@protocol NSTouchBarProvider <NSObject>
+@required
+/*
+    The basic method for providing a touch bar. AppKit will key value observe this property, if for some reason you wish to replace a live touch bar wholesale.
+    Note that many subclasses of NSResponder already implement this method and conform to this protocol.
+*/
+@property (strong, readonly, nullable) NSTouchBar *touchBar NS_AVAILABLE_MAC(10_12_1);
+@end
+
+@interface NSResponder (NSTouchBarProvider) <NSTouchBarProvider>
+/*
+    The touch bar object associated with this responder. If no touch bar is explicitly set, NSResponder will send -makeTouchBar to itself to create the default touch bar for this responder. This property is archived.
+*/
+@property (strong, readwrite, nullable) NSTouchBar *touchBar NS_AVAILABLE_MAC(10_12_1);
+
+/*
+    Subclasses should over-ride this method to create and configure the default touch bar for this responder.
+*/
+- (nullable NSTouchBar *)makeTouchBar NS_AVAILABLE_MAC(10_12_1);
+@end
+
+
+@interface NSApplication (NSTouchBarCustomization)
+/// Whether or not a menu item to customize the touch bar can be automatically added to the main menu. It will only actually be added when a touch bar hardware or simulator is present. Defaults to NO. Setting this property to YES is the recommended way to add the customization menu item. But if non-standard placement of the menu item is needed, creating a menu item with an action of `toggleTouchBarCustomizationPalette:` can be used instead.
+@property (getter=isAutomaticCustomizeTouchBarMenuItemEnabled) BOOL automaticCustomizeTouchBarMenuItemEnabled NS_AVAILABLE_MAC(10_12_1);
+
+/// Show or dismiss the customization palette for the currently displayed touch bars. NSApplication validates this selector against whether the current touch bars are customizable and, if configured on a menu item, will standardize and localize the title. If the current system does not have touch bar support, the menu item will be automatically hidden.
+- (IBAction)toggleTouchBarCustomizationPalette:(nullable id)sender NS_AVAILABLE_MAC(10_12_1);
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTouchBarItem.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTouchBarItem.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTouchBarItem.h	1969-12-31 19:00:00.000000000 -0500
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTouchBarItem.h	2016-10-10 22:25:11.000000000 -0400
@@ -0,0 +1,107 @@
+/*
+ NSTouchBarItem.h
+ Application Kit
+ Copyright (c) 2015-2016, Apple Inc.
+ All rights reserved.
+*/
+
+#import <AppKit/AppKitDefines.h>
+
+#import <Foundation/Foundation.h>
+
+typedef NSString * NSTouchBarItemIdentifier NS_EXTENSIBLE_STRING_ENUM;
+
+@class NSTouchBar, NSViewController, NSView, NSImage, NSGestureRecognizer;
+@class NSString;
+
+NS_ASSUME_NONNULL_BEGIN
+
+typedef float NSTouchBarItemPriority _NS_TYPED_EXTENSIBLE_ENUM NS_AVAILABLE_MAC(10_12_1);
+
+static const NSTouchBarItemPriority NSTouchBarItemPriorityHigh NS_AVAILABLE_MAC(10_12_1) = 1000;
+static const NSTouchBarItemPriority NSTouchBarItemPriorityNormal NS_AVAILABLE_MAC(10_12_1) = 0;
+static const NSTouchBarItemPriority NSTouchBarItemPriorityLow NS_AVAILABLE_MAC(10_12_1) = -1000;
+
+
+NS_CLASS_AVAILABLE_MAC(10_12_1)
+@interface NSTouchBarItem : NSObject <NSCoding> {
+@private
+    NSTouchBarItemIdentifier _identifier;
+    NSTouchBarItemPriority _visibilityPriority;
+    NSInteger _visibilityCount;
+    NSMapTable<NSTouchBar *, NSNumber *> *_touchBars;
+
+#if !__OBJC2__
+    void *_touchBarItemReserved[4] __unused;
+#endif /* !__OBJC2__ */
+}
+
+/*
+    The designated initializer. This instantiates a new touch bar item with the specified initializer.
+*/
+- (instancetype)initWithIdentifier:(NSTouchBarItemIdentifier)identifier NS_DESIGNATED_INITIALIZER;
+
+/*
+    Items can be archived and unarchived using NSCoder, as noted by conformance to the NSCoding protocol.
+*/
+- (nullable instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
+
+/*
+    Items must be instantiated with an identifier. Use -initWithIdentifier instead of -init.
+*/
+- (instancetype)init NS_UNAVAILABLE;
+
+/*
+    The identifier of this item. Apart from spaces, item identifiers should be globally unique.
+*/
+@property (readonly, copy) NSTouchBarItemIdentifier identifier;
+
+/*
+    If there are more items in the touch bar than can be displayed, some will be hidden. Items with high visibility priority will be hidden after items with low visibility priority.
+*/
+@property NSTouchBarItemPriority visibilityPriority;
+
+/*
+    Intended for subclassing. By default, this method returns this item's view controller's view.
+*/
+@property (readonly, nullable) NSView *view;
+
+/*
+    Intended for subclassing. By default, this method returns nil.
+*/
+@property (readonly, nullable) NSViewController *viewController;
+
+/*
+    The user visible string identifying this item during customization. By default this method returns the empty string.
+*/
+@property (readonly, copy) NSString *customizationLabel;
+
+/*
+    When YES, this item is attached to a visible touch bar, and is being displayed. Note that some types of items are never considered visible, for example spaces, other items proxys, and groups.
+    This property is key value observable.
+*/
+@property (readonly, getter=isVisible) BOOL visible;
+@end
+
+/*
+    The identifier of an item appropriate for use as a small space in the touch bar. Generally, you can use this identifier in a touch bar's itemIdentifiers array, and it will instantiate that space for you.
+*/
+APPKIT_EXTERN NSTouchBarItemIdentifier const NSTouchBarItemIdentifierFixedSpaceSmall NS_AVAILABLE_MAC(10_12_1);
+
+/*
+    The identifier of an item appropriate for use as a large space in the touch bar. Generally, you can use this identifier in a touch bar's itemIdentifiers array, and it will instantiate that space for you.
+*/
+APPKIT_EXTERN NSTouchBarItemIdentifier const NSTouchBarItemIdentifierFixedSpaceLarge NS_AVAILABLE_MAC(10_12_1);
+
+/*
+    The identifier of an item appropriate for use as a flexible space in the touch bar. Generally, you can use this identifier in a touch bar's itemIdentifiers array, and it will instantiate that space for you.
+*/
+APPKIT_EXTERN NSTouchBarItemIdentifier const NSTouchBarItemIdentifierFlexibleSpace NS_AVAILABLE_MAC(10_12_1);
+
+/*
+    The identifier of the special "other items proxy." Generally, you can use this identifier in a touch bar's itemIdentifiers array, and a special proxy item will be instantiated for you. When the touch bar containing this item is visible, touch bars provided by items closer to the first responder will be nested inside the space denoted for this item. Space items on either side of this item will be automatically massaged to handle cases where the touch bar containing this identifier is itself the bar closest to the first responder (or closer bars are empty.)
+    Note that a touch bar lacking this item identifier will be replaced in its entirety by touch bars closer to the first responder.
+*/
+APPKIT_EXTERN NSTouchBarItemIdentifier const NSTouchBarItemIdentifierOtherItemsProxy NS_AVAILABLE_MAC(10_12_1);
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSView.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSView.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSView.h	2016-08-11 21:43:44.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSView.h	2016-10-10 22:25:11.000000000 -0400
@@ -292,9 +293,8 @@
 @property (readonly) BOOL needsPanelToBecomeKey;
 @property (readonly) BOOL mouseDownCanMoveWindow;
 
-/* By default, views do not accept touch events
-*/
-@property BOOL acceptsTouchEvents NS_AVAILABLE_MAC(10_6);
+/* Deprecated in favor of allowedTouchTypes. Return YES if allowedTouchTypes includes NSTouchTypeMaskIndirect */
+@property BOOL acceptsTouchEvents NS_DEPRECATED_MAC(10_6, 10_12_1);
 
 /* In some cases, the user may rest a thumb or other touch on the device. By default, these touches are not delivered and are not included in the event's set of touches. Touches may transition in and out of resting at any time. Unless the view wants restingTouches, began / ended events are simlulated as touches transition from resting to active and vice versa.
 */
@@ -589,6 +589,11 @@
 - (void)removeGestureRecognizer:(NSGestureRecognizer *)gestureRecognizer NS_AVAILABLE_MAC(10_10);
 @end
 
+@interface NSView (NSTouchBar)
+/* Defaults to NSTouchTypeDirect if linked on or after 10_12, 0 otherwise */
+@property NSTouchTypeMask allowedTouchTypes NS_AVAILABLE_MAC(10_12_1);
+@end
+
 @interface NSView(NSDeprecated)
 
 /* This drag method as been deprecated in favor of beginDraggingSessionWithItems:event:source:
