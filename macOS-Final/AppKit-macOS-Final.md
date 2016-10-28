#AppKit.framework

``` diff
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
