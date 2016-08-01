#UIKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h	2016-07-11 07:32:59.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h	2016-07-28 05:06:41.000000000 +0200
@@ -17,9 +17,9 @@
 NS_CLASS_AVAILABLE_IOS(2_0) @interface UIFont : NSObject <NSCopying>
 
 // Returns an instance of the font associated with the text style and scaled appropriately for the user's selected content size category. See UIFontDescriptor.h for the complete list.
-+ (UIFont *)preferredFontForTextStyle:(NSString *)style NS_AVAILABLE_IOS(7_0);
++ (UIFont *)preferredFontForTextStyle:(UIFontTextStyle)style NS_AVAILABLE_IOS(7_0);
 // Returns an instance of the font associated with the text style and scaled appropriately for the content size category defined in the trait collection.
-+ (UIFont *)preferredFontForTextStyle:(NSString *)style compatibleWithTraitCollection:(nullable UITraitCollection *)traitCollection NS_AVAILABLE_IOS(10_0);
++ (UIFont *)preferredFontForTextStyle:(UIFontTextStyle)style compatibleWithTraitCollection:(nullable UITraitCollection *)traitCollection NS_AVAILABLE_IOS(10_0);
 
 // Returns a font using CSS name matching semantics.
 + (nullable UIFont *)fontWithName:(NSString *)fontName size:(CGFloat)fontSize;
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h	2016-07-11 07:32:59.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h	2016-07-28 04:43:52.000000000 +0200
@@ -46,6 +46,11 @@
 } NS_ENUM_AVAILABLE_IOS(7_0);
 
 typedef NSUInteger UIFontDescriptorClass;
+#if UIKIT_STRING_ENUMS
+typedef NSString * UIFontTextStyle NS_EXTENSIBLE_STRING_ENUM;
+#else
+typedef NSString * UIFontTextStyle;
+#endif
 
 @class NSMutableDictionary, NSDictionary, NSArray, NSSet, UITraitCollection;
 
@@ -78,9 +83,9 @@
 + (UIFontDescriptor *)fontDescriptorWithName:(NSString *)fontName matrix:(CGAffineTransform)matrix;
 
 // Returns a font descriptor containing the text style and containing the user's selected content size category.
-+ (UIFontDescriptor *)preferredFontDescriptorWithTextStyle:(NSString *)style;
++ (UIFontDescriptor *)preferredFontDescriptorWithTextStyle:(UIFontTextStyle)style;
 // Returns a font descriptor containing the text style and containing the content size category defined in the trait collection.
-+ (UIFontDescriptor *)preferredFontDescriptorWithTextStyle:(NSString *)style compatibleWithTraitCollection:(nullable UITraitCollection *)traitCollection NS_AVAILABLE_IOS(10_0);
++ (UIFontDescriptor *)preferredFontDescriptorWithTextStyle:(UIFontTextStyle)style compatibleWithTraitCollection:(nullable UITraitCollection *)traitCollection NS_AVAILABLE_IOS(10_0);
 
 - (instancetype)initWithFontAttributes:(NSDictionary<NSString *, id> *)attributes NS_DESIGNATED_INITIALIZER;
 
@@ -146,16 +151,16 @@
 UIKIT_EXTERN NSString *const UIFontFeatureSelectorIdentifierKey NS_AVAILABLE_IOS(7_0);
 
 // Font text styles, semantic descriptions of the intended use for a font returned by +[UIFont preferredFontForTextStyle:]
-UIKIT_EXTERN NSString *const UIFontTextStyleTitle1 NS_AVAILABLE_IOS(9_0);
-UIKIT_EXTERN NSString *const UIFontTextStyleTitle2 NS_AVAILABLE_IOS(9_0);
-UIKIT_EXTERN NSString *const UIFontTextStyleTitle3 NS_AVAILABLE_IOS(9_0);
-UIKIT_EXTERN NSString *const UIFontTextStyleHeadline NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UIFontTextStyleSubheadline NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UIFontTextStyleBody NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UIFontTextStyleCallout NS_AVAILABLE_IOS(9_0);
-UIKIT_EXTERN NSString *const UIFontTextStyleFootnote NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UIFontTextStyleCaption1 NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UIFontTextStyleCaption2 NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIFontTextStyle const UIFontTextStyleTitle1 NS_AVAILABLE_IOS(9_0);
+UIKIT_EXTERN UIFontTextStyle const UIFontTextStyleTitle2 NS_AVAILABLE_IOS(9_0);
+UIKIT_EXTERN UIFontTextStyle const UIFontTextStyleTitle3 NS_AVAILABLE_IOS(9_0);
+UIKIT_EXTERN UIFontTextStyle const UIFontTextStyleHeadline NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIFontTextStyle const UIFontTextStyleSubheadline NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIFontTextStyle const UIFontTextStyleBody NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIFontTextStyle const UIFontTextStyleCallout NS_AVAILABLE_IOS(9_0);
+UIKIT_EXTERN UIFontTextStyle const UIFontTextStyleFootnote NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIFontTextStyle const UIFontTextStyleCaption1 NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIFontTextStyle const UIFontTextStyleCaption2 NS_AVAILABLE_IOS(7_0);
 
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h	2016-07-11 07:25:47.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h	2016-07-28 05:06:41.000000000 +0200
@@ -218,3 +218,4 @@
 #if __has_include(<UIKit/UIViewPropertyAnimator.h>)
 #import <UIKit/UIViewPropertyAnimator.h>
 #endif
+
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h	2016-07-11 07:32:59.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h	2016-07-28 05:06:41.000000000 +0200
@@ -29,3 +29,4 @@
 
 #define UIKIT_DEFINE_AS_PROPERTIES (!defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_UIKIT_EPOCH) && SWIFT_SDK_OVERLAY_UIKIT_EPOCH >= 1))
 #define UIKIT_REMOVE_ZERO_FROM_SWIFT (!defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_UIKIT_EPOCH) && SWIFT_SDK_OVERLAY_UIKIT_EPOCH >= 1))
+#define UIKIT_STRING_ENUMS ((defined(SWIFT_SDK_OVERLAY_UIKIT_EPOCH) && SWIFT_SDK_OVERLAY_UIKIT_EPOCH >= 2))

```