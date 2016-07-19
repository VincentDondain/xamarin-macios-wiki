#AppKit.framework

``` diff
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
 @property (getter=isBordered) BOOL bordered;
 @property (getter=isTransparent) BOOL transparent;
 - (void)setPeriodicDelay:(float)delay interval:(float)interval;
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
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableViewRowAction.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableViewRowAction.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableViewRowAction.h	2016-06-29 03:31:49.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTableViewRowAction.h	2016-07-11 05:26:54.000000000 +0200
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

-
-- (void)setDelegate:(nullable id <NSTokenFieldDelegate>)delegate;
-- (nullable id <NSTokenFieldDelegate>)delegate;

@@ -80,4 +53,32 @@
 
 @end
 
+
+@interface NSTokenField : NSTextField {    

+
+/* For apps linked against 10.12, this property has zeroing weak memory semantics. When linked against an older SDK, or with objects that do not support zeroing weak references this falls back to having `assign` semantics. */
+@property (nullable, assign) id<NSTokenFieldDelegate> delegate;
+
```
