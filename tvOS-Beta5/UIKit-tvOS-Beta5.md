#UIKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIResponder.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIResponder.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIResponder.h	2016-07-28 04:43:52.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIResponder.h	2016-08-06 09:32:41.000000000 +0200
@@ -14,7 +14,26 @@
 @class UIPress;
 @class UIPressesEvent;
 
-NS_CLASS_AVAILABLE_IOS(2_0) @interface UIResponder : NSObject
+@protocol UIResponderStandardEditActions <NSObject>
+@optional
+- (void)cut:(nullable id)sender NS_AVAILABLE_IOS(3_0);
+- (void)copy:(nullable id)sender NS_AVAILABLE_IOS(3_0);
+- (void)paste:(nullable id)sender NS_AVAILABLE_IOS(3_0);
+- (void)select:(nullable id)sender NS_AVAILABLE_IOS(3_0);
+- (void)selectAll:(nullable id)sender NS_AVAILABLE_IOS(3_0);
+- (void)delete:(nullable id)sender NS_AVAILABLE_IOS(3_2);
+- (void)makeTextWritingDirectionLeftToRight:(nullable id)sender NS_AVAILABLE_IOS(5_0);
+- (void)makeTextWritingDirectionRightToLeft:(nullable id)sender NS_AVAILABLE_IOS(5_0);
+- (void)toggleBoldface:(nullable id)sender NS_AVAILABLE_IOS(6_0);
+- (void)toggleItalics:(nullable id)sender NS_AVAILABLE_IOS(6_0);
+- (void)toggleUnderline:(nullable id)sender NS_AVAILABLE_IOS(6_0);
+
+- (void)increaseSize:(nullable id)sender NS_AVAILABLE_IOS(7_0);
+- (void)decreaseSize:(nullable id)sender NS_AVAILABLE_IOS(7_0);
+
+@end
+
+NS_CLASS_AVAILABLE_IOS(2_0) @interface UIResponder : NSObject <UIResponderStandardEditActions>
 
 #if UIKIT_DEFINE_AS_PROPERTIES
 @property(nonatomic, readonly, nullable) UIResponder *nextResponder;
@@ -97,7 +116,7 @@
 @property (nonatomic,readonly) UIKeyModifierFlags modifierFlags;
 @property (nullable,nonatomic,copy) NSString *discoverabilityTitle NS_AVAILABLE_IOS(9_0);
 
-// The action for UIKeyCommands should accept a single (id)sender, as do the UIResponderStandardEditActions below
+// The action for UIKeyCommands should accept a single (id)sender, as do the UIResponderStandardEditActions above
 
 // Creates an key command that will _not_ be discoverable in the UI.
 + (UIKeyCommand *)keyCommandWithInput:(NSString *)input modifierFlags:(UIKeyModifierFlags)modifierFlags action:(SEL)action;
@@ -111,25 +130,6 @@
 @property (nullable,nonatomic,readonly) NSArray<UIKeyCommand *> *keyCommands NS_AVAILABLE_IOS(7_0); // returns an array of UIKeyCommand objects<
 @end
 
-@interface NSObject(UIResponderStandardEditActions)   // these methods are not implemented in NSObject
-
-- (void)cut:(nullable id)sender NS_AVAILABLE_IOS(3_0);
-- (void)copy:(nullable id)sender NS_AVAILABLE_IOS(3_0);
-- (void)paste:(nullable id)sender NS_AVAILABLE_IOS(3_0);
-- (void)select:(nullable id)sender NS_AVAILABLE_IOS(3_0);
-- (void)selectAll:(nullable id)sender NS_AVAILABLE_IOS(3_0);
-- (void)delete:(nullable id)sender NS_AVAILABLE_IOS(3_2);
-- (void)makeTextWritingDirectionLeftToRight:(nullable id)sender NS_AVAILABLE_IOS(5_0);
-- (void)makeTextWritingDirectionRightToLeft:(nullable id)sender NS_AVAILABLE_IOS(5_0);
-- (void)toggleBoldface:(nullable id)sender NS_AVAILABLE_IOS(6_0);
-- (void)toggleItalics:(nullable id)sender NS_AVAILABLE_IOS(6_0);
-- (void)toggleUnderline:(nullable id)sender NS_AVAILABLE_IOS(6_0);
-
-- (void)increaseSize:(nullable id)sender NS_AVAILABLE_IOS(7_0);
-- (void)decreaseSize:(nullable id)sender NS_AVAILABLE_IOS(7_0);
-
-@end
-
 @class UIInputViewController;
 @class UITextInputMode;
 @class UITextInputAssistantItem;
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextField.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextField.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextField.h	2016-07-28 04:43:52.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextField.h	2016-08-06 08:17:50.000000000 +0200
@@ -42,6 +42,11 @@
     UITextFieldViewModeAlways
 };
 
+typedef NS_ENUM(NSInteger, UITextFieldDidEndEditingReason) {
+    UITextFieldDidEndEditingReasonCommitted,
+    UITextFieldDidEndEditingReasonCancelled UIKIT_AVAILABLE_TVOS_ONLY(10_0)
+} NS_ENUM_AVAILABLE_IOS(10_0);
+
 NS_CLASS_AVAILABLE_IOS(2_0) @interface UITextField : UIControl <UITextInput, NSCoding, UIContentSizeCategoryAdjusting>
 
 @property(nullable, nonatomic,copy)   NSString               *text;                 // default is nil
@@ -115,6 +120,7 @@
 - (void)textFieldDidBeginEditing:(UITextField *)textField;           // became first responder
 - (BOOL)textFieldShouldEndEditing:(UITextField *)textField;          // return YES to allow editing to stop and to resign first responder status. NO to disallow the editing session to end
 - (void)textFieldDidEndEditing:(UITextField *)textField;             // may be called if forced even if shouldEndEditing returns NO (e.g. view removed from window) or endEditing:YES called
+- (void)textFieldDidEndEditing:(UITextField *)textField reason:(UITextFieldDidEndEditingReason)reason NS_AVAILABLE_IOS(10_0); // if implemented, called in place of textFieldDidEndEditing:
 
 - (BOOL)textField:(UITextField *)textField shouldChangeCharactersInRange:(NSRange)range replacementString:(NSString *)string;   // return NO to not change text
 
@@ -127,5 +133,7 @@
 UIKIT_EXTERN NSNotificationName const UITextFieldTextDidEndEditingNotification;
 UIKIT_EXTERN NSNotificationName const UITextFieldTextDidChangeNotification;
 
+UIKIT_EXTERN NSString *const UITextFieldDidEndEditingReasonKey NS_AVAILABLE_IOS(10_0);
+
 NS_ASSUME_NONNULL_END
 

```