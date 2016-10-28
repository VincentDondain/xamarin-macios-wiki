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

