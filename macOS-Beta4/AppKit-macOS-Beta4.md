#AppKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitLegacySwiftCompatibility.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitLegacySwiftCompatibility.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitLegacySwiftCompatibility.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/AppKitLegacySwiftCompatibility.h	2016-07-27 05:10:07.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionView.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionView.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionView.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSCollectionView.h	2016-07-27 05:10:07.000000000 +0200
@@ -224,7 +224,7 @@
 
 /* An optional, non-retained delegate object, that will have the opportunity to influence the CollectionView's drag-and-drop, selection, highlighting, and layout transitioning behaviors.  See the NSCollectionViewDelegate protocol, declared below, for the methods this delegate may implement.  Defaults to nil, which leaves the CollectionView to determine its own behaviors.
 */
-@property (nullable, assign) id<NSCollectionViewDelegate> delegate;
+@property (nullable, weak) id<NSCollectionViewDelegate> delegate;
 
 
 #pragma mark *** Decoration ***

diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorList.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorList.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorList.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSColorList.h	2016-07-27 05:10:07.000000000 +0200
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
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStackView.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStackView.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStackView.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSStackView.h	2016-07-27 05:10:07.000000000 +0200
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

	/* These constants are deprecated in favor of their NSTextFinder equivalents. */
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
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindow.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindow.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindow.h	2016-07-11 05:26:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindow.h	2016-07-27 05:10:07.000000000 +0200
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
```
