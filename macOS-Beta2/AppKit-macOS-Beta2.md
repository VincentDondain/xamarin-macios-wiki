#AppKit.framework

``` diff
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabView.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabView.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabView.h	2016-06-03 05:13:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSTabView.h	2016-06-29 03:31:49.000000000 +0200
@@ -17,6 +17,7 @@
 
 
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
@@ -95,12 +115,14 @@
 
 	/* Getters */
 
+@property NSTabPosition tabPosition;
+@property NSTabViewBorderType tabViewBorderType;                                // This will only be respected if NSTabPosition is NSTabPositionNone.
 @property (readonly, copy) NSArray<__kindof NSTabViewItem *> *tabViewItems;
 @property BOOL allowsTruncatedLabels;
 @property BOOL drawsBackground;  						// only relevant for borderless tab view type
 @property NSControlTint controlTint;
 @property NSControlSize controlSize;
```
