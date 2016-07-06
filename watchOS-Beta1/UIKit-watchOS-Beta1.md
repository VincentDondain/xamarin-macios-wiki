#UIKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSAttributedString.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSAttributedString.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSAttributedString.h	2015-08-13 07:58:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSAttributedString.h	2016-06-03 06:16:40.000000000 +0200
@@ -35,7 +35,7 @@
 UIKIT_EXTERN NSString * const NSObliquenessAttributeName NS_AVAILABLE(10_0, 7_0);         // NSNumber containing floating point value; skew to be applied to glyphs, default 0: no skew
 UIKIT_EXTERN NSString * const NSExpansionAttributeName NS_AVAILABLE(10_0, 7_0);           // NSNumber containing floating point value; log of expansion factor to be applied to glyphs, default 0: no expansion
 
-UIKIT_EXTERN NSString * const NSWritingDirectionAttributeName NS_AVAILABLE(10_6, 7_0);    // NSArray of NSNumbers representing the nested levels of writing direction overrides as defined by Unicode LRE, RLE, LRO, and RLO characters.  The control characters can be obtained by masking NSWritingDirection and NSTextWritingDirection values.  LRE: NSWritingDirectionLeftToRight|NSWritingDirectionEmbedding, RLE: NSWritingDirectionRightToLeft|NSWritingDirectionEmbedding, LRO: NSWritingDirectionLeftToRight|NSWritingDirectionOverride, RLO: NSWritingDirectionRightToLeft|NSWritingDirectionOverride,
+UIKIT_EXTERN NSString * const NSWritingDirectionAttributeName NS_AVAILABLE(10_6, 7_0);    // NSArray of NSNumbers representing the nested levels of writing direction overrides as defined by Unicode LRE, RLE, LRO, and RLO characters.  The control characters can be obtained by masking NSWritingDirection and NSWritingDirectionFormatType values.  LRE: NSWritingDirectionLeftToRight|NSWritingDirectionEmbedding, RLE: NSWritingDirectionRightToLeft|NSWritingDirectionEmbedding, LRO: NSWritingDirectionLeftToRight|NSWritingDirectionOverride, RLO: NSWritingDirectionRightToLeft|NSWritingDirectionOverride,
 
 UIKIT_EXTERN NSString * const NSVerticalGlyphFormAttributeName NS_AVAILABLE(10_7, 6_0);   // An NSNumber containing an integer value.  0 means horizontal text.  1 indicates vertical text.  If not specified, it could follow higher-level vertical orientation settings.  Currently on iOS, it's always horizontal.  The behavior for any other value is undefined.
 
@@ -122,7 +122,7 @@
 
 @interface NSAttributedString (NSAttributedStringDocumentFormats)
 // Methods initializing the receiver contents with an external document data.  options specify document attributes for interpreting the document contents.  NSDocumentTypeDocumentAttribute, NSCharacterEncodingDocumentAttribute, and NSDefaultAttributesDocumentAttribute are supported options key.  When they are not specified, these methods will examine the data and do their best to detect the appropriate attributes.  If dict is non-NULL, it will return a dictionary with various document-wide attributes accessible via NS...DocumentAttribute keys.
-- (nullable instancetype)initWithURL:(NSURL *)url options:(NSDictionary<NSString *, id> *)options documentAttributes:(NSDictionary<NSString *, id> * __nullable * __nullable)dict error:(NSError **)error NS_AVAILABLE(10_11, 9_0);
+- (nullable instancetype)initWithURL:(NSURL *)url options:(NSDictionary<NSString *, id> *)options documentAttributes:(NSDictionary<NSString *, id> * __nullable * __nullable)dict error:(NSError **)error NS_AVAILABLE(10_4, 9_0);
 - (nullable instancetype)initWithData:(NSData *)data options:(NSDictionary<NSString *, id> *)options documentAttributes:(NSDictionary<NSString *, id> * __nullable * __nullable)dict error:(NSError **)error NS_AVAILABLE(10_0, 7_0);
 
 // Generates an NSData object for the receiver contents in range.  It requires a document attributes dict specifying at least the NSDocumentTypeDocumentAttribute to determine the format to be written.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSParagraphStyle.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSParagraphStyle.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSParagraphStyle.h	2015-08-13 07:58:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSParagraphStyle.h	2016-06-03 06:16:40.000000000 +0200
@@ -17,7 +17,7 @@
 // NSTextTab
 UIKIT_EXTERN NSString *const NSTabColumnTerminatorsAttributeName NS_AVAILABLE(10_0, 7_0); // An attribute for NSTextTab options.  The value is NSCharacterSet.  The character set is used to determine the tab column terminating character.  The tab and newline characters are implied even if not included in the character set.
 
-NS_CLASS_AVAILABLE(10_0, 7_0) @interface NSTextTab : NSObject <NSCopying, NSCoding>
+NS_CLASS_AVAILABLE(10_0, 7_0) @interface NSTextTab : NSObject <NSCopying, NSCoding, NSSecureCoding>
 
 + (NSCharacterSet *)columnTerminatorsForLocale:(nullable NSLocale *)aLocale NS_AVAILABLE(10_11, 7_0); // Returns the column terminators for locale. Passing nil returns an instance corresponding to +[NSLocale systemLocale]. For matching user's formatting preferences, pass +[NSLocale currentLocale]. Can be used as the value for NSTabColumnTerminatorsAttributeName to make a decimal tab stop.
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h	2016-02-20 03:44:05.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h	2016-05-23 08:16:41.000000000 +0200
@@ -1,3 +1,4 @@
+
 //
 //  UIAccessibility.h
 //  UIKit
@@ -13,6 +14,7 @@
 #import <UIKit/UIAccessibilityAdditions.h>
 #import <UIKit/UIAccessibilityConstants.h>
 #import <UIKit/UIAccessibilityCustomAction.h>
+#import <UIKit/UIAccessibilityCustomRotor.h>
 #import <UIKit/UIAccessibilityElement.h>
 #import <UIKit/UIAccessibilityIdentification.h>
 #import <UIKit/UIAccessibilityZoom.h>
@@ -349,64 +351,68 @@
  Use UIAccessibilityIsVoiceOverRunning() to determine if VoiceOver is running.
  Listen for UIAccessibilityVoiceOverStatusChanged to know when VoiceOver starts or stops.
  */
-UIKIT_EXTERN BOOL UIAccessibilityIsVoiceOverRunning() NS_AVAILABLE_IOS(4_0);
+UIKIT_EXTERN BOOL UIAccessibilityIsVoiceOverRunning(void) NS_AVAILABLE_IOS(4_0);
 UIKIT_EXTERN NSString *const UIAccessibilityVoiceOverStatusChanged NS_AVAILABLE_IOS(4_0);
 
 // Returns whether system audio is mixed down from stereo to mono.
-UIKIT_EXTERN BOOL UIAccessibilityIsMonoAudioEnabled() NS_AVAILABLE_IOS(5_0);
+UIKIT_EXTERN BOOL UIAccessibilityIsMonoAudioEnabled(void) NS_AVAILABLE_IOS(5_0);
 UIKIT_EXTERN NSString *const UIAccessibilityMonoAudioStatusDidChangeNotification NS_AVAILABLE_IOS(5_0);
 
 // Returns whether the system preference for closed captioning is enabled.
-UIKIT_EXTERN BOOL UIAccessibilityIsClosedCaptioningEnabled() NS_AVAILABLE_IOS(5_0);
+UIKIT_EXTERN BOOL UIAccessibilityIsClosedCaptioningEnabled(void) NS_AVAILABLE_IOS(5_0);
 UIKIT_EXTERN NSString *const UIAccessibilityClosedCaptioningStatusDidChangeNotification NS_AVAILABLE_IOS(5_0);
 
 // Returns whether the system preference for invert colors is enabled.
-UIKIT_EXTERN BOOL UIAccessibilityIsInvertColorsEnabled() NS_AVAILABLE_IOS(6_0);
+UIKIT_EXTERN BOOL UIAccessibilityIsInvertColorsEnabled(void) NS_AVAILABLE_IOS(6_0);
 UIKIT_EXTERN NSString *const UIAccessibilityInvertColorsStatusDidChangeNotification NS_AVAILABLE_IOS(6_0);
 
 // Returns whether the app is running under Guided Access mode.
-UIKIT_EXTERN BOOL UIAccessibilityIsGuidedAccessEnabled() NS_AVAILABLE_IOS(6_0);
+UIKIT_EXTERN BOOL UIAccessibilityIsGuidedAccessEnabled(void) NS_AVAILABLE_IOS(6_0);
 UIKIT_EXTERN NSString *const UIAccessibilityGuidedAccessStatusDidChangeNotification NS_AVAILABLE_IOS(6_0);
 
 // Returns whether the system preference for bold text is enabled
-UIKIT_EXTERN BOOL UIAccessibilityIsBoldTextEnabled() NS_AVAILABLE_IOS(8_0);
+UIKIT_EXTERN BOOL UIAccessibilityIsBoldTextEnabled(void) NS_AVAILABLE_IOS(8_0);
 UIKIT_EXTERN NSString *const UIAccessibilityBoldTextStatusDidChangeNotification NS_AVAILABLE_IOS(8_0);
 
 // Returns whether the system preference for grayscale is enabled
-UIKIT_EXTERN BOOL UIAccessibilityIsGrayscaleEnabled() NS_AVAILABLE_IOS(8_0);
+UIKIT_EXTERN BOOL UIAccessibilityIsGrayscaleEnabled(void) NS_AVAILABLE_IOS(8_0);
 UIKIT_EXTERN NSString *const UIAccessibilityGrayscaleStatusDidChangeNotification NS_AVAILABLE_IOS(8_0);
 
 // Returns whether the system preference for reduce transparency is enabled
-UIKIT_EXTERN BOOL UIAccessibilityIsReduceTransparencyEnabled() NS_AVAILABLE_IOS(8_0);
+UIKIT_EXTERN BOOL UIAccessibilityIsReduceTransparencyEnabled(void) NS_AVAILABLE_IOS(8_0);
 UIKIT_EXTERN NSString *const UIAccessibilityReduceTransparencyStatusDidChangeNotification NS_AVAILABLE_IOS(8_0);
 
 // Returns whether the system preference for reduce motion is enabled
-UIKIT_EXTERN BOOL UIAccessibilityIsReduceMotionEnabled() NS_AVAILABLE_IOS(8_0);
+UIKIT_EXTERN BOOL UIAccessibilityIsReduceMotionEnabled(void) NS_AVAILABLE_IOS(8_0);
 UIKIT_EXTERN NSString *const UIAccessibilityReduceMotionStatusDidChangeNotification NS_AVAILABLE_IOS(8_0);
 
 // Returns whether the system preference for darker colors is enabled
-UIKIT_EXTERN BOOL UIAccessibilityDarkerSystemColorsEnabled() NS_AVAILABLE_IOS(8_0);
+UIKIT_EXTERN BOOL UIAccessibilityDarkerSystemColorsEnabled(void) NS_AVAILABLE_IOS(8_0);
 UIKIT_EXTERN NSString *const UIAccessibilityDarkerSystemColorsStatusDidChangeNotification NS_AVAILABLE_IOS(8_0);
 
 /*
  Use UIAccessibilityIsSwitchControlRunning() to determine if Switch Control is running.
  Listen for UIAccessibilitySwitchControlStatusDidChangeNotification to know when Switch Control starts or stops.
 */
-UIKIT_EXTERN BOOL UIAccessibilityIsSwitchControlRunning() NS_AVAILABLE_IOS(8_0);
+UIKIT_EXTERN BOOL UIAccessibilityIsSwitchControlRunning(void) NS_AVAILABLE_IOS(8_0);
 UIKIT_EXTERN NSString *const UIAccessibilitySwitchControlStatusDidChangeNotification NS_AVAILABLE_IOS(8_0);
 
 // Returns whether the system preference for Speak Selection is enabled
-UIKIT_EXTERN BOOL UIAccessibilityIsSpeakSelectionEnabled() NS_AVAILABLE_IOS(8_0);
+UIKIT_EXTERN BOOL UIAccessibilityIsSpeakSelectionEnabled(void) NS_AVAILABLE_IOS(8_0);
 UIKIT_EXTERN NSString *const UIAccessibilitySpeakSelectionStatusDidChangeNotification NS_AVAILABLE_IOS(8_0);
 
 // Returns whether the system preference for Speak Screen is enabled
-UIKIT_EXTERN BOOL UIAccessibilityIsSpeakScreenEnabled() NS_AVAILABLE_IOS(8_0);
+UIKIT_EXTERN BOOL UIAccessibilityIsSpeakScreenEnabled(void) NS_AVAILABLE_IOS(8_0);
 UIKIT_EXTERN NSString *const UIAccessibilitySpeakScreenStatusDidChangeNotification NS_AVAILABLE_IOS(8_0);
 
 // Returns whether the system preference for Shake to Undo is enabled
-UIKIT_EXTERN BOOL UIAccessibilityIsShakeToUndoEnabled() NS_AVAILABLE_IOS(9_0);
+UIKIT_EXTERN BOOL UIAccessibilityIsShakeToUndoEnabled(void) NS_AVAILABLE_IOS(9_0);
 UIKIT_EXTERN NSString *const UIAccessibilityShakeToUndoDidChangeNotification NS_AVAILABLE_IOS(9_0);
 
+// Returns whether the system preference for AssistiveTouch is enabled
+UIKIT_EXTERN BOOL UIAccessibilityIsAssistiveTouchRunning(void) NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UIAccessibilityAssistiveTouchStatusDidChangeNotification NS_AVAILABLE_IOS(10_0);
+
 /*
  Use UIAccessibilityRequestGuidedAccessSession() to request this app be locked into or released
  from Single App mode. The request to lock this app into Single App mode will only succeed if the device is Supervised,
@@ -415,4 +421,15 @@
  */
 UIKIT_EXTERN void UIAccessibilityRequestGuidedAccessSession(BOOL enable, void(^completionHandler)(BOOL didSucceed)) NS_AVAILABLE_IOS(7_0);
 
+typedef NS_OPTIONS(NSUInteger, UIAccessibilityHearingDeviceEar) {
+    UIAccessibilityHearingDeviceEarNone    = 0,
+    UIAccessibilityHearingDeviceEarLeft    = 1 << 1,
+    UIAccessibilityHearingDeviceEarRight   = 1 << 2,
+    UIAccessibilityHearingDeviceEarBoth    = UIAccessibilityHearingDeviceEarLeft | UIAccessibilityHearingDeviceEarRight,
+} NS_ENUM_AVAILABLE_IOS(10_0);
+
+// Returns the current pairing status of MFi hearing aids
+UIKIT_EXTERN UIAccessibilityHearingDeviceEar UIAccessibilityHearingDevicePairedEar(void) NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UIAccessibilityHearingDevicePairedEarDidChangeNotification NS_AVAILABLE_IOS(10_0);
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityConstants.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityConstants.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityConstants.h	2016-03-01 05:10:04.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityConstants.h	2016-06-03 06:16:41.000000000 +0200
@@ -99,6 +99,12 @@
 UIKIT_EXTERN UIAccessibilityTraits UIAccessibilityTraitCausesPageTurn NS_AVAILABLE_IOS(5_0);
 
 /*
+ Used when a view or accessibility container represents an ordered list of tabs.
+ The object with this trait should return NO for isAccessibilityElement.
+ */
+UIKIT_EXTERN UIAccessibilityTraits UIAccessibilityTraitTabBar NS_AVAILABLE_IOS(10_0);
+
+/*
  Accessibility Notifications
  
  UIKit posts notifications for standard events as appropriate, however the
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIColor.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIColor.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIColor.h	2016-02-20 03:44:05.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIColor.h	2016-05-23 08:16:41.000000000 +0200
@@ -22,6 +22,7 @@
 + (UIColor *)colorWithWhite:(CGFloat)white alpha:(CGFloat)alpha;
 + (UIColor *)colorWithHue:(CGFloat)hue saturation:(CGFloat)saturation brightness:(CGFloat)brightness alpha:(CGFloat)alpha;
 + (UIColor *)colorWithRed:(CGFloat)red green:(CGFloat)green blue:(CGFloat)blue alpha:(CGFloat)alpha;
++ (UIColor *)colorWithDisplayP3Red:(CGFloat)displayP3Red green:(CGFloat)green blue:(CGFloat)blue alpha:(CGFloat)alpha NS_AVAILABLE_IOS(10_0);
 + (UIColor *)colorWithCGColor:(CGColorRef)cgColor;
 + (UIColor *)colorWithPatternImage:(UIImage *)image;
 #if __has_include(<CoreImage/CoreImage.h>)
@@ -32,6 +33,7 @@
 - (UIColor *)initWithWhite:(CGFloat)white alpha:(CGFloat)alpha;
 - (UIColor *)initWithHue:(CGFloat)hue saturation:(CGFloat)saturation brightness:(CGFloat)brightness alpha:(CGFloat)alpha;
 - (UIColor *)initWithRed:(CGFloat)red green:(CGFloat)green blue:(CGFloat)blue alpha:(CGFloat)alpha;
+- (UIColor *)initWithDisplayP3Red:(CGFloat)displayP3Red green:(CGFloat)green blue:(CGFloat)blue alpha:(CGFloat)alpha NS_AVAILABLE_IOS(10_0);
 - (UIColor *)initWithCGColor:(CGColorRef)cgColor;
 - (UIColor *)initWithPatternImage:(UIImage*)image;
 #if __has_include(<CoreImage/CoreImage.h>)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h	2016-02-20 03:44:05.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h	2016-05-23 08:16:41.000000000 +0200
@@ -10,12 +10,16 @@
 #import <UIKit/UIKitDefines.h>
 #import <UIKit/UIFontDescriptor.h>
 
+@class UITraitCollection;
+
 NS_ASSUME_NONNULL_BEGIN
 
 NS_CLASS_AVAILABLE_IOS(2_0) @interface UIFont : NSObject <NSCopying>
 
 // Returns an instance of the font associated with the text style and scaled appropriately for the user's selected content size category. See UIFontDescriptor.h for the complete list.
 + (UIFont *)preferredFontForTextStyle:(NSString *)style NS_AVAILABLE_IOS(7_0);
+// Returns an instance of the font associated with the text style and scaled appropriately for the content size category defined in the trait collection.
++ (UIFont *)preferredFontForTextStyle:(NSString *)style compatibleWithTraitCollection:(nullable UITraitCollection *)traitCollection NS_AVAILABLE_IOS(10_0);
 
 // Returns a font using CSS name matching semantics.
 + (nullable UIFont *)fontWithName:(NSString *)fontName size:(CGFloat)fontSize;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h	2016-03-01 05:10:03.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h	2016-06-03 06:16:40.000000000 +0200
@@ -47,7 +47,7 @@
 
 typedef NSUInteger UIFontDescriptorClass;
 
-@class NSMutableDictionary, NSDictionary, NSArray, NSSet;
+@class NSMutableDictionary, NSDictionary, NSArray, NSSet, UITraitCollection;
 
 NS_CLASS_AVAILABLE_IOS(7_0) @interface UIFontDescriptor : NSObject <NSCopying, NSSecureCoding>
 
@@ -75,15 +75,20 @@
 
 // Returns a font descriptor containing the text style and containing the user's selected content size category.
 + (UIFontDescriptor *)preferredFontDescriptorWithTextStyle:(NSString *)style;
+// Returns a font descriptor containing the text style and containing the content size category defined in the trait collection.
++ (UIFontDescriptor *)preferredFontDescriptorWithTextStyle:(NSString *)style compatibleWithTraitCollection:(nullable UITraitCollection *)traitCollection NS_AVAILABLE_IOS(10_0);
 
 - (instancetype)initWithFontAttributes:(NSDictionary<NSString *, id> *)attributes NS_DESIGNATED_INITIALIZER;
 
 - (UIFontDescriptor *)fontDescriptorByAddingAttributes:(NSDictionary<NSString *, id> *)attributes; // the new attributes take precedence over the existing ones in the receiver
-- (UIFontDescriptor *)fontDescriptorWithSymbolicTraits:(UIFontDescriptorSymbolicTraits)symbolicTraits;
 - (UIFontDescriptor *)fontDescriptorWithSize:(CGFloat)newPointSize;
 - (UIFontDescriptor *)fontDescriptorWithMatrix:(CGAffineTransform)matrix;
 - (UIFontDescriptor *)fontDescriptorWithFace:(NSString *)newFace;
 - (UIFontDescriptor *)fontDescriptorWithFamily:(NSString *)newFamily;
+
+- (nullable UIFontDescriptor *)fontDescriptorWithSymbolicTraits:(UIFontDescriptorSymbolicTraits)symbolicTraits; // Returns a new font descriptor reference in the same family with the given symbolic traits, or nil if none found in the system.
+
+
 @end
 
 // Predefined font attributes not defined in NSAttributedString.h
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphics.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphics.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphics.h	2016-02-20 03:44:05.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphics.h	2016-05-23 08:16:41.000000000 +0200
@@ -27,9 +27,11 @@
 
 // UIImage context
 
+// The following methods will only return a 8-bit per channel context in the DeviceRGB color space.
+// Any new bitmap drawing code is encouraged to use UIGraphicsImageRenderer in leiu of this API.
 UIKIT_EXTERN void     UIGraphicsBeginImageContext(CGSize size);
 UIKIT_EXTERN void     UIGraphicsBeginImageContextWithOptions(CGSize size, BOOL opaque, CGFloat scale) NS_AVAILABLE_IOS(4_0);
-UIKIT_EXTERN UIImage* __null_unspecified UIGraphicsGetImageFromCurrentImageContext(void);
+UIKIT_EXTERN UIImage* __nullable UIGraphicsGetImageFromCurrentImageContext(void);
 UIKIT_EXTERN void     UIGraphicsEndImageContext(void); 
 
 // PDF context
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImage.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImage.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImage.h	2016-02-20 03:44:02.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImage.h	2016-05-23 08:16:41.000000000 +0200
@@ -20,6 +20,10 @@
 @class UITraitCollection, UIImageAsset;
 #endif
 
+#if __has_include(<UIKit/UIGraphicsImageRenderer.h>)
+@class UIGraphicsImageRendererFormat;
+#endif
+
 typedef NS_ENUM(NSInteger, UIImageOrientation) {
     UIImageOrientationUp,            // default orientation
     UIImageOrientationDown,          // 180 deg rotation
@@ -123,6 +127,11 @@
 - (UIImage *)imageWithRenderingMode:(UIImageRenderingMode)renderingMode NS_AVAILABLE_IOS(7_0);
 @property(nonatomic, readonly) UIImageRenderingMode renderingMode NS_AVAILABLE_IOS(7_0);
 
+#if __has_include(<UIKit/UIGraphicsImageRenderer.h>)
+// Returns an optimal UIGraphicsImageRendererFormat instance for this image, maintaining pixel format and color space.
+@property (nonatomic, readonly) UIGraphicsImageRendererFormat *imageRendererFormat NS_AVAILABLE_IOS(10_0);
+#endif
+
 #if __has_include(<UIKit/UITraitCollection.h>)
 @property (nonatomic, readonly, copy) UITraitCollection *traitCollection NS_AVAILABLE_IOS(8_0); // describes the image in terms of its traits
 @property (nullable, nonatomic, readonly) UIImageAsset *imageAsset NS_AVAILABLE_IOS(8_0); // The asset is not encoded along with the image. Returns nil if the image is not CGImage based.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h	2016-02-20 03:44:02.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h	2016-06-03 05:02:19.000000000 +0200
@@ -44,7 +44,8 @@
 
 #import <UIKit/UIColor.h>
 
-#if __has_include(<UIKit/UIControl.h>)
+#if __has_include(<UIKit/UIContentSizeCategoryAdjusting.h>)
+#import <UIKit/UIContentSizeCategoryAdjusting.h>
 #import <UIKit/UIControl.h>
 #import <UIKit/UIDataDetectors.h>
 #import <UIKit/UIDatePicker.h>
@@ -54,6 +55,7 @@
 #import <UIKit/UIDocumentPickerViewController.h>
 #import <UIKit/UIDocumentMenuViewController.h>
 #import <UIKit/UIDocumentPickerExtensionViewController.h>
+#import <UIKit/UICloudSharingController.h>
 #import <UIKit/NSFileProviderExtension.h>
 #import <UIKit/UIVisualEffectView.h>
 #import <UIKit/UIEvent.h>
@@ -70,6 +72,12 @@
 #import <UIKit/UIGraphics.h>
 #import <UIKit/UIImage.h>
 
+#if __has_include(<UIKit/UIGraphicsRenderer.h>)
+#import <UIKit/UIGraphicsRenderer.h>
+#import <UIKit/UIGraphicsImageRenderer.h>
+#import <UIKit/UIGraphicsPDFRenderer.h>
+#endif
+
 #if __has_include(<UIKit/UIImageAsset.h>)
 #import <UIKit/UIImageAsset.h>
 #import <UIKit/NSDataAsset.h>
@@ -89,6 +97,7 @@
 #import <UIKit/UIApplicationShortcutItem.h>
 #import <UIKit/UIUserNotificationSettings.h>
 #import <UIKit/UIFocus.h>
+#import <UIKit/UIFocusGuide.h>
 #import <UIKit/UIFocusAnimationCoordinator.h>
 #import <UIKit/UILocalizedIndexedCollation.h>
 #import <UIKit/UILongPressGestureRecognizer.h>
@@ -121,6 +130,7 @@
 #import <UIKit/UIProgressView.h>
 #import <UIKit/UIReferenceLibraryViewController.h>
 #import <UIKit/UIRefreshControl.h>
+#import <UIKit/UIRefreshControlHosting.h>
 #import <UIKit/UIResponder.h>
 #import <UIKit/UIRotationGestureRecognizer.h>
 #import <UIKit/UIScreen.h>
@@ -191,6 +201,7 @@
 #import <UIKit/UIViewControllerTransitioning.h>
 #import <UIKit/UIViewControllerTransitionCoordinator.h>
 #import <UIKit/UIPresentationController.h>
+#import <UIKit/UIPreviewInteraction.h>
 #import <UIKit/UIPopoverPresentationController.h>
 #import <UIKit/UIDynamicAnimator.h>
 #import <UIKit/UIDynamicBehavior.h>
@@ -203,3 +214,7 @@
 #import <UIKit/UICollisionBehavior.h>
 #import <UIKit/UIRegion.h>
 #endif
+
+#if __has_include(<UIKit/UIViewPropertyAnimator.h>)
+#import <UIKit/UIViewPropertyAnimator.h>
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h	2016-02-20 03:44:05.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h	2016-05-23 08:16:41.000000000 +0200
@@ -21,6 +21,8 @@
 #define UIKIT_AVAILABLE_IOS_TVOS(_ios, _tvos) __IOS_AVAILABLE(_ios) __WATCHOS_UNAVAILABLE __TVOS_AVAILABLE(_tvos)
 #define UIKIT_AVAILABLE_IOS_WATCHOS_TVOS(_ios, _watchos, _tvos) __IOS_AVAILABLE(_ios) __WATCHOS_AVAILABLE(_watchos) __TVOS_AVAILABLE(_tvos)
 
+#define UIKIT_CLASS_AVAILABLE_IOS_ONLY(vers) UIKIT_EXTERN __IOS_AVAILABLE(vers) __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE
+#define UIKIT_CLASS_AVAILABLE_WATCHOS_ONLY(vers) UIKIT_EXTERN __IOS_UNAVAILABLE __WATCHOS_AVAILABLE(vers) __TVOS_UNAVAILABLE
 #define UIKIT_CLASS_AVAILABLE_TVOS_ONLY(vers) UIKIT_EXTERN __IOS_UNAVAILABLE __WATCHOS_UNAVAILABLE __TVOS_AVAILABLE(vers)
 #define UIKIT_CLASS_AVAILABLE_IOS_TVOS(_ios, _tvos) UIKIT_EXTERN __IOS_AVAILABLE(_ios) __WATCHOS_UNAVAILABLE __TVOS_AVAILABLE(_tvos)
 #define UIKIT_CLASS_AVAILABLE_IOS_WATCHOS_TVOS(_ios, _watchos, _tvos) UIKIT_EXTERN __IOS_AVAILABLE(_ios) __WATCHOS_AVAILABLE(_watchos) __TVOS_AVAILABLE(_tvos)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILocalNotification.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILocalNotification.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILocalNotification.h	2016-02-20 03:44:05.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILocalNotification.h	2016-05-23 08:16:41.000000000 +0200
@@ -13,7 +13,8 @@
 @class CLRegion;
 
 // In iOS 8.0 and later, your application must register for user notifications using -[UIApplication registerUserNotificationSettings:] before being able to schedule and present UILocalNotifications
-NS_CLASS_AVAILABLE_IOS(4_0) __TVOS_PROHIBITED @interface UILocalNotification : NSObject<NSCopying, NSCoding>       // added in iOS 4.0
+NS_CLASS_DEPRECATED_IOS(4_0, 10_0, "Use UserNotifications Framework's UNNotificationRequest") __TVOS_PROHIBITED
+@interface UILocalNotification : NSObject<NSCopying, NSCoding>
 
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
 - (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
@@ -57,6 +58,6 @@
 @end
 
 
-UIKIT_EXTERN NSString *const UILocalNotificationDefaultSoundName NS_AVAILABLE_IOS(4_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN NSString *const UILocalNotificationDefaultSoundName NS_DEPRECATED_IOS(4_0, 10_0, "Use UserNotifications Framework's +[UNNotificationSound defaultSound]") __TVOS_PROHIBITED;
 
 NS_ASSUME_NONNULL_END

```