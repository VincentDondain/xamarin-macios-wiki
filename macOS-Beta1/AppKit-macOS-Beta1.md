#AppKit.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopoverTouchBarItem.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopoverTouchBarItem.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopoverTouchBarItem.h	2016-10-13 01:14:44.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPopoverTouchBarItem.h	2016-10-24 09:19:26.000000000 +0200
@@ -86,4 +86,8 @@
 - (NSGestureRecognizer *)makeStandardActivatePopoverGestureRecognizer;
 @end
 
+@interface NSPopoverTouchBarItem (NSOldAPI)
+@property BOOL supportsPressAndHold /* NS_DEPRECATED_MAC(10_12_1, 10_12_1, "Use pressAndHoldTouchBar instead.") */;
+@end
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTouchBar.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTouchBar.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTouchBar.h	2016-10-13 01:14:44.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTouchBar.h	2016-10-24 09:19:26.000000000 +0200
@@ -205,4 +205,10 @@
 - (IBAction)toggleTouchBarCustomizationPalette:(nullable id)sender NS_AVAILABLE_MAC(10_12_1);
 @end
 
+@interface NSTouchBar (NSOldAPI)
+@property (copy) NSArray<NSTouchBarItemIdentifier> *customizationDefaultItemIdentifiers /* NS_DEPRECATED_WITH_REPLACEMENT_MAC("defultItemIdentifiers", 10_12_1, 10_12_1)*/ ;
+@property (copy) NSArray<NSTouchBarItemIdentifier> *itemIdentifiers /* NS_DEPRECATED_WITH_REPLACEMENT_MAC("defultItemIdentifiers", 10_12_1, 10_12_1)*/ ;
+@property (copy) NSSet<NSTouchBarItem *> *defaultItems /* NS_DEPRECATED_WITH_REPLACEMENT_MAC("templateItems", 10_12_1, 10_12_1) */ ;
+@end
+
 NS_ASSUME_NONNULL_END

```