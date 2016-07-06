#UIKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSAttributedString.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSAttributedString.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSAttributedString.h	2015-10-03 01:47:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSAttributedString.h	2016-06-03 06:16:40.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSLayoutAnchor.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSLayoutAnchor.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSLayoutAnchor.h	2015-10-03 01:47:14.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSLayoutAnchor.h	2016-06-03 05:02:46.000000000 +0200
@@ -3,9 +3,9 @@
 */
 
 #import <Foundation/Foundation.h>
+#import <UIKit/NSLayoutConstraint.h>
 
-@class NSLayoutConstraint, NSLayoutAnchor;
-
+NS_ASSUME_NONNULL_BEGIN
 
 /* An NSLayoutAnchor represents an edge or dimension of a layout item.  Its concrete 
  subclasses allow concise creation of constraints.  
@@ -75,3 +75,4 @@
 - (NSLayoutConstraint *)constraintGreaterThanOrEqualToAnchor:(NSLayoutDimension *)anchor multiplier:(CGFloat)m constant:(CGFloat)c;
 - (NSLayoutConstraint *)constraintLessThanOrEqualToAnchor:(NSLayoutDimension *)anchor multiplier:(CGFloat)m constant:(CGFloat)c;
 @end
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSLayoutConstraint.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSLayoutConstraint.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSLayoutConstraint.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSLayoutConstraint.h	2016-06-03 05:02:46.000000000 +0200
@@ -10,7 +10,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-@class NSArray, NSDictionary;
+@class NSArray, NSDictionary, NSLayoutAnchor;
 
 
 typedef NS_ENUM(NSInteger, NSLayoutRelation) {
@@ -30,8 +30,8 @@
     NSLayoutAttributeHeight,
     NSLayoutAttributeCenterX,
     NSLayoutAttributeCenterY,
-    NSLayoutAttributeBaseline,
-    NSLayoutAttributeLastBaseline = NSLayoutAttributeBaseline,
+    NSLayoutAttributeLastBaseline,
+    NSLayoutAttributeBaseline NS_SWIFT_UNAVAILABLE("Use 'lastBaseline' instead") = NSLayoutAttributeLastBaseline,
     NSLayoutAttributeFirstBaseline NS_ENUM_AVAILABLE_IOS(8_0),
     
     
@@ -56,8 +56,8 @@
     NSLayoutFormatAlignAllTrailing = (1 << NSLayoutAttributeTrailing),
     NSLayoutFormatAlignAllCenterX = (1 << NSLayoutAttributeCenterX),
     NSLayoutFormatAlignAllCenterY = (1 << NSLayoutAttributeCenterY),
-    NSLayoutFormatAlignAllBaseline = (1 << NSLayoutAttributeBaseline),
-    NSLayoutFormatAlignAllLastBaseline = NSLayoutFormatAlignAllBaseline,
+    NSLayoutFormatAlignAllLastBaseline = (1 << NSLayoutAttributeLastBaseline),
+    NSLayoutFormatAlignAllBaseline NS_SWIFT_UNAVAILABLE("Use 'alignAllLastBaseline' instead") = NSLayoutFormatAlignAllLastBaseline,
     NSLayoutFormatAlignAllFirstBaseline NS_ENUM_AVAILABLE_IOS(8_0) = (1 << NSLayoutAttributeFirstBaseline),
     
     NSLayoutFormatAlignmentMask = 0xFFFF,
@@ -98,7 +98,7 @@
 
 /* If a constraint's priority level is less than UILayoutPriorityRequired, then it is optional.  Higher priority constraints are met before lower priority constraints.
  Constraint satisfaction is not all or nothing.  If a constraint 'a == b' is optional, that means we will attempt to minimize 'abs(a-b)'.
- This property may only be modified as part of initial set up.  An exception will be thrown if it is set after a constraint has been added to a view.
+ This property may only be modified as part of initial set up or when optional.  After a constraint has been added to a view, an exception will be thrown if the priority is changed from/to NSLayoutPriorityRequired.
  */
 @property UILayoutPriority priority;
 
@@ -109,12 +109,19 @@
 
 /* accessors
  firstItem.firstAttribute {==,<=,>=} secondItem.secondAttribute * multiplier + constant
+ Access to these properties is not recommended. Use the `firstAnchor` and `secondAnchor` properties instead.
  */
 @property (readonly, assign) id firstItem;
 @property (readonly) NSLayoutAttribute firstAttribute;
-@property (readonly) NSLayoutRelation relation;
 @property (nullable, readonly, assign) id secondItem;
 @property (readonly) NSLayoutAttribute secondAttribute;
+
+/* accessors
+ firstAnchor{==,<=,>=} secondAnchor * multiplier + constant
+ */
+@property (readonly, copy) NSLayoutAnchor *firstAnchor NS_AVAILABLE(10_12, 10_0);
+@property (readonly, copy, nullable) NSLayoutAnchor *secondAnchor NS_AVAILABLE(10_12, 10_0);
+@property (readonly) NSLayoutRelation relation;
 @property (readonly) CGFloat multiplier;
 
 /* Unlike the other properties, the constant may be modified after constraint creation.  Setting the constant on an existing constraint performs much better than removing the constraint and adding a new one that's just like the old but for having a new constant.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSLayoutManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSLayoutManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSLayoutManager.h	2015-10-03 01:47:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSLayoutManager.h	2016-06-03 05:02:46.000000000 +0200
@@ -147,9 +147,9 @@
 @property(readonly, NS_NONATOMIC_IOSONLY) NSUInteger numberOfGlyphs;
 
 // If non-contiguous layout is not enabled, these will cause generation of all glyphs up to and including glyphIndex.  The first CGGlyphAtIndex variant returns kCGFontIndexInvalid if the requested index is out of the range (0, numberOfGlyphs), and optionally returns a flag indicating whether the requested index is in range.  The second CGGlyphAtIndex variant raises a NSRangeError if the requested index is out of range.
-- (CGGlyph)CGGlyphAtIndex:(NSUInteger)glyphIndex isValidIndex:(nullable BOOL *)isValidIndex;
-- (CGGlyph)CGGlyphAtIndex:(NSUInteger)glyphIndex;
-- (BOOL)isValidGlyphIndex:(NSUInteger)glyphIndex;
+- (CGGlyph)CGGlyphAtIndex:(NSUInteger)glyphIndex isValidIndex:(nullable BOOL *)isValidIndex NS_AVAILABLE(10_11,7_0);
+- (CGGlyph)CGGlyphAtIndex:(NSUInteger)glyphIndex NS_AVAILABLE(10_11,7_0);
+- (BOOL)isValidGlyphIndex:(NSUInteger)glyphIndex NS_AVAILABLE(10_11,7_0);
 
 // If non-contiguous layout is not enabled, this will cause generation of all glyphs up to and including glyphIndex.  It will return the glyph property associated with the glyph at the specified index.
 - (NSGlyphProperty)propertyForGlyphAtIndex:(NSUInteger)glyphIndex NS_AVAILABLE(10_5, 7_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSParagraphStyle.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSParagraphStyle.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSParagraphStyle.h	2015-10-03 01:47:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSParagraphStyle.h	2016-06-03 06:16:40.000000000 +0200
@@ -17,7 +17,7 @@
 // NSTextTab
 UIKIT_EXTERN NSString *const NSTabColumnTerminatorsAttributeName NS_AVAILABLE(10_0, 7_0); // An attribute for NSTextTab options.  The value is NSCharacterSet.  The character set is used to determine the tab column terminating character.  The tab and newline characters are implied even if not included in the character set.
 
-NS_CLASS_AVAILABLE(10_0, 7_0) @interface NSTextTab : NSObject <NSCopying, NSCoding>
+NS_CLASS_AVAILABLE(10_0, 7_0) @interface NSTextTab : NSObject <NSCopying, NSCoding, NSSecureCoding>
 
 + (NSCharacterSet *)columnTerminatorsForLocale:(nullable NSLocale *)aLocale NS_AVAILABLE(10_11, 7_0); // Returns the column terminators for locale. Passing nil returns an instance corresponding to +[NSLocale systemLocale]. For matching user's formatting preferences, pass +[NSLocale currentLocale]. Can be used as the value for NSTabColumnTerminatorsAttributeName to make a decimal tab stop.
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSTextContainer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSTextContainer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSTextContainer.h	2015-10-03 01:47:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSTextContainer.h	2016-06-03 05:02:19.000000000 +0200
@@ -18,7 +18,7 @@
 /**************************** Initialization ****************************/
 
 - (instancetype)initWithSize:(CGSize)size NS_DESIGNATED_INITIALIZER NS_AVAILABLE(10_11, 7_0);
-- (nullable instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
 
 
 /**************************** Layout ****************************/
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h	2016-05-23 08:16:41.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityConstants.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityConstants.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityConstants.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityConstants.h	2016-06-03 06:16:41.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityCustomRotor.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityCustomRotor.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityCustomRotor.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityCustomRotor.h	2016-06-03 05:02:46.000000000 +0200
@@ -0,0 +1,74 @@
+//
+//  UIAccessibilityCustomRotor.h
+//  UIKit
+//
+//  Copyright (c) 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <UIKit/UITextInput.h>
+
+/*
+ UIAccessibilityCustomRotor
+ 
+ Assistive technologies, like VoiceOver, use a context sensitive function to provide more power
+ and flexibility to perform actions and searches. This is called "The Rotor."
+ 
+ An element (or an element in the ancestor hierarchy) can expose an array of custom rotors
+ that a user can activate to search for other instances of like minded elements. This can also
+ be applied to ranges within elements.
+ 
+ As an example, in a magazine app, a custom rotor can be created to allow the user to find the next link or heading within an article.
+ Alternatively, in a document editor, the next misspelled word can be found by returning the next range that contains a misspelled word.
+ */
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class UIAccessibilityCustomRotor, UIAccessibilityCustomRotorItemResult, UIAccessibilityCustomRotorSearchPredicate;
+
+typedef NS_ENUM(NSInteger, UIAccessibilityCustomRotorDirection) {
+    UIAccessibilityCustomRotorDirectionPrevious NS_ENUM_AVAILABLE_IOS(10_0),
+    UIAccessibilityCustomRotorDirectionNext NS_ENUM_AVAILABLE_IOS(10_0),
+};
+
+typedef UIAccessibilityCustomRotorItemResult *_Nullable(^UIAccessibilityCustomRotorSearch)(UIAccessibilityCustomRotorSearchPredicate *predicate);
+
+// Create the array of UIAccessibilityCustomRotors and set it on the target element or ancestor element to which it applies.
+@interface NSObject (UIAccessibilityCustomRotor)
+@property (nonatomic, retain, nullable) NSArray<UIAccessibilityCustomRotor *> *accessibilityCustomRotors NS_AVAILABLE_IOS(10_0);
+@end
+
+// UIAccessibilityCustomRotorSearchPredicate is a container for search parameters.
+// It should be examined to determine the next matching UIAccessibilityCustomRotorItemResult.
+NS_CLASS_AVAILABLE_IOS(10_0) @interface UIAccessibilityCustomRotorSearchPredicate : NSObject
+@property (nonatomic, retain) UIAccessibilityCustomRotorItemResult *currentItem;
+@property (nonatomic) UIAccessibilityCustomRotorDirection searchDirection;
+@end
+
+NS_CLASS_AVAILABLE_IOS(10_0) @interface UIAccessibilityCustomRotor : NSObject
+
+- (instancetype)initWithName:(NSString *)name itemSearchBlock:(UIAccessibilityCustomRotorSearch)itemSearchBlock;
+
+// The localized name the assistive technology will use to describe the custom rotor.
+@property (nonatomic, copy) NSString *name;
+
+// A block that takes a UIAccessibilityCustomRotorItemResult and the search direction and returns the next/previous instance of that rotor item.
+// If the currentItem is nil, that implies the first/last item should be returned.
+@property (nonatomic, copy) UIAccessibilityCustomRotorSearch itemSearchBlock;
+
+@end
+
+NS_CLASS_AVAILABLE_IOS(10_0) @interface UIAccessibilityCustomRotorItemResult : NSObject
+
+- (instancetype)initWithTargetElement:(id<NSObject>)targetElement targetRange:(nullable UITextRange *)targetRange;
+
+// A UIAccessibilityCustomRotorItemResult references a real element that will be messaged for other accessibility properties.
+@property (nonatomic, weak) id<NSObject> targetElement;
+
+// Optionally, a target range can be used to search within an element (like a UITextView).
+// If targetRange is nil, the search should begin from the start/end of the element depending on the search direction.
+@property (nullable, nonatomic, retain) UITextRange *targetRange;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityElement.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityElement.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityElement.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityElement.h	2016-06-03 05:02:46.000000000 +0200
@@ -33,6 +33,10 @@
 @property (nonatomic, assign) CGRect accessibilityFrame;
 @property (nonatomic, assign) UIAccessibilityTraits accessibilityTraits;
 
+// When set, -[UIAccessibilityElement accessibilityFrame] will automatically adjust for the container's frame.
+// This can be useful when the element is a descendant of a scroll view, for instance.
+@property (nonatomic, assign) CGRect accessibilityFrameInContainerSpace NS_AVAILABLE_IOS(10_0);
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityZoom.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityZoom.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityZoom.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityZoom.h	2016-06-03 05:02:46.000000000 +0200
@@ -5,6 +5,9 @@
 //  Copyright (c) 2011-2015 Apple Inc. All rights reserved.
 //
 
+#import <Foundation/Foundation.h>
+#import <UIKit/UIView.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 /* 
@@ -21,6 +24,6 @@
  If your app uses multi-finger gestures that conflict with system Zoom gestures (by using three fingers), 
  calling this method will warn users of the conflict.
  */
-UIKIT_EXTERN void UIAccessibilityRegisterGestureConflictWithZoom() NS_AVAILABLE_IOS(5_0);
+UIKIT_EXTERN void UIAccessibilityRegisterGestureConflictWithZoom(void) NS_AVAILABLE_IOS(5_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIApplication.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIApplication.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIApplication.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIApplication.h	2016-06-03 05:02:46.000000000 +0200
@@ -70,13 +70,13 @@
     UIRemoteNotificationTypeSound   = 1 << 1,
     UIRemoteNotificationTypeAlert   = 1 << 2,
     UIRemoteNotificationTypeNewsstandContentAvailability = 1 << 3,
-} NS_ENUM_DEPRECATED_IOS(3_0, 8_0, "Use UIUserNotificationType for user notifications and registerForRemoteNotifications for receiving remote notifications instead.") __TVOS_PROHIBITED;
+} NS_ENUM_DEPRECATED_IOS(3_0, 8_0, "Use UserNotifications Framework's UNAuthorizationOptions for user notifications and registerForRemoteNotifications for receiving remote notifications instead.") __TVOS_PROHIBITED;
 
 typedef NS_ENUM(NSUInteger, UIBackgroundFetchResult) {
     UIBackgroundFetchResultNewData,
     UIBackgroundFetchResultNoData,
     UIBackgroundFetchResultFailed
-} NS_ENUM_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
+} NS_ENUM_AVAILABLE_IOS(7_0);
 
 typedef NS_ENUM(NSInteger, UIBackgroundRefreshStatus) {
     UIBackgroundRefreshStatusRestricted, //< unavailable on this system due to device configuration; the user cannot enable the feature
@@ -96,6 +96,7 @@
 UIKIT_EXTERN const NSTimeInterval UIApplicationBackgroundFetchIntervalMinimum NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
 UIKIT_EXTERN const NSTimeInterval UIApplicationBackgroundFetchIntervalNever NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
 
+@class CKShareMetadata;
 @class UIView, UIWindow;
 @class UIStatusBar, UIStatusBarWindow, UILocalNotification;
 @protocol UIApplicationDelegate;
@@ -104,7 +105,7 @@
 
 + (UIApplication *)sharedApplication NS_EXTENSION_UNAVAILABLE_IOS("Use view controller based solutions where appropriate instead.");
 
-@property(nullable, nonatomic,assign) id<UIApplicationDelegate> delegate;
+@property(nullable, nonatomic, assign) id<UIApplicationDelegate> delegate;
 
 - (void)beginIgnoringInteractionEvents NS_EXTENSION_UNAVAILABLE_IOS("");               // nested. set should be set during animations & transitions to ignore touch and other events
 - (void)endIgnoringInteractionEvents NS_EXTENSION_UNAVAILABLE_IOS("");
@@ -112,9 +113,15 @@
 
 @property(nonatomic,getter=isIdleTimerDisabled)       BOOL idleTimerDisabled;	  // default is NO
 
-- (BOOL)openURL:(NSURL*)url NS_EXTENSION_UNAVAILABLE_IOS("");
+- (BOOL)openURL:(NSURL*)url NS_DEPRECATED_IOS(2_0, 10_0, "Please use openURL:options:completionHandler: instead") NS_EXTENSION_UNAVAILABLE_IOS("");
 - (BOOL)canOpenURL:(NSURL *)url NS_AVAILABLE_IOS(3_0);
 
+// Options are specified in the section below for openURL options. An empty options dictionary will result in the same
+// behavior as the older openURL call, aside from the fact that this is asynchronous and calls the completion handler rather
+// than returning a result.
+// The completion handler is called on the main queue.
+- (void)openURL:(NSURL*)url options:(NSDictionary<NSString *, id> *)options completionHandler:(void (^ __nullable)(BOOL success))completion NS_AVAILABLE_IOS(10_0) NS_EXTENSION_UNAVAILABLE_IOS("");
+
 - (void)sendEvent:(UIEvent *)event;
 
 @property(nullable, nonatomic,readonly) UIWindow *keyWindow;
@@ -142,7 +149,7 @@
 @property(nonatomic,readonly) NSTimeInterval statusBarOrientationAnimationDuration __TVOS_PROHIBITED; // Returns the animation duration for the status bar during a 90 degree orientation change.  It should be doubled for a 180 degree orientation change.
 @property(nonatomic,readonly) CGRect statusBarFrame __TVOS_PROHIBITED; // returns CGRectZero if the status bar is hidden
 
-@property(nonatomic) NSInteger applicationIconBadgeNumber __TVOS_PROHIBITED;  // set to 0 to hide. default is 0. In iOS 8.0 and later, your application must register for user notifications using -[UIApplication registerUserNotificationSettings:] before being able to set the icon badge.
+@property(nonatomic) NSInteger applicationIconBadgeNumber;  // set to 0 to hide. default is 0. In iOS 8.0 and later, your application must register for user notifications using -[UIApplication registerUserNotificationSettings:] before being able to set the icon badge.
 
 @property(nonatomic) BOOL applicationSupportsShakeToEdit NS_AVAILABLE_IOS(3_0) __TVOS_PROHIBITED;
 
@@ -187,23 +194,23 @@
 // Returns YES if the application is currently registered for remote notifications, taking into account any systemwide settings; doesn't relate to connectivity.
 - (BOOL)isRegisteredForRemoteNotifications NS_AVAILABLE_IOS(8_0);
 
-- (void)registerForRemoteNotificationTypes:(UIRemoteNotificationType)types NS_DEPRECATED_IOS(3_0, 8_0, "Please use registerForRemoteNotifications and registerUserNotificationSettings: instead") __TVOS_PROHIBITED;
+- (void)registerForRemoteNotificationTypes:(UIRemoteNotificationType)types NS_DEPRECATED_IOS(3_0, 8_0, "Use -[UIApplication registerForRemoteNotifications] and UserNotifications Framework's -[UNUserNotificationCenter requestAuthorizationWithOptions:completionHandler:]") __TVOS_PROHIBITED;
 
 // Returns the enabled types, also taking into account any systemwide settings; doesn't relate to connectivity.
-- (UIRemoteNotificationType)enabledRemoteNotificationTypes NS_DEPRECATED_IOS(3_0, 8_0, "Please use -[UIApplication isRegisteredForRemoteNotifications], or -[UIApplication currentUserNotificationSettings] to retrieve user-enabled remote notification and user notification settings") __TVOS_PROHIBITED;
+- (UIRemoteNotificationType)enabledRemoteNotificationTypes NS_DEPRECATED_IOS(3_0, 8_0, "Use -[UIApplication isRegisteredForRemoteNotifications] and UserNotifications Framework's -[UNUserNotificationCenter getNotificationSettingsWithCompletionHandler:] to retrieve user-enabled remote notification and user notification settings") __TVOS_PROHIBITED;
 
 @end
 
 // In iOS 8.0 and later, your application must register for user notifications using -[UIApplication registerUserNotificationSettings:] before being able to schedule and present UILocalNotifications
 @interface UIApplication (UILocalNotifications)
 
-- (void)presentLocalNotificationNow:(UILocalNotification *)notification NS_AVAILABLE_IOS(4_0) __TVOS_PROHIBITED;
+- (void)presentLocalNotificationNow:(UILocalNotification *)notification NS_DEPRECATED_IOS(4_0, 10_0, "Use UserNotifications Framework's -[UNUserNotificationCenter addNotificationRequest:withCompletionHandler:]") __TVOS_PROHIBITED;
 
-- (void)scheduleLocalNotification:(UILocalNotification *)notification NS_AVAILABLE_IOS(4_0) __TVOS_PROHIBITED;  // copies notification
-- (void)cancelLocalNotification:(UILocalNotification *)notification NS_AVAILABLE_IOS(4_0) __TVOS_PROHIBITED;
-- (void)cancelAllLocalNotifications NS_AVAILABLE_IOS(4_0) __TVOS_PROHIBITED;
+- (void)scheduleLocalNotification:(UILocalNotification *)notification NS_DEPRECATED_IOS(4_0, 10_0, "Use UserNotifications Framework's -[UNUserNotificationCenter addNotificationRequest:withCompletionHandler:]") __TVOS_PROHIBITED;  // copies notification
+- (void)cancelLocalNotification:(UILocalNotification *)notification NS_DEPRECATED_IOS(4_0, 10_0, "Use UserNotifications Framework's -[UNUserNotificationCenter removePendingNotificationRequestsWithIdentifiers:]") __TVOS_PROHIBITED;
+- (void)cancelAllLocalNotifications NS_DEPRECATED_IOS(4_0, 10_0, "Use UserNotifications Framework's -[UNUserNotificationCenter removeAllPendingNotificationRequests]") __TVOS_PROHIBITED;
 
-@property(nullable,nonatomic,copy) NSArray<UILocalNotification *> *scheduledLocalNotifications NS_AVAILABLE_IOS(4_0) __TVOS_PROHIBITED;         // setter added in iOS 4.2
+@property(nullable,nonatomic,copy) NSArray<UILocalNotification *> *scheduledLocalNotifications NS_DEPRECATED_IOS(4_0, 10_0, "Use UserNotifications Framework's -[UNUserNotificationCenter getPendingNotificationRequestsWithCompletionHandler:]") __TVOS_PROHIBITED;
 
 @end
 
@@ -226,7 +233,7 @@
 @end
 
 @interface UIApplication (UINewsstand)
-- (void)setNewsstandIconImage:(nullable UIImage *)image NS_DEPRECATED_IOS(9_0, 9_0, "Newsstand apps now behave like normal apps on SpringBoard") __TVOS_PROHIBITED;
+- (void)setNewsstandIconImage:(nullable UIImage *)image NS_DEPRECATED_IOS(5_0, 9_0, "Newsstand apps now behave like normal apps on SpringBoard") __TVOS_PROHIBITED;
 @end
 
 @class UIApplicationShortcutItem;
@@ -286,26 +293,28 @@
 
 - (void)application:(UIApplication *)application didFailToRegisterForRemoteNotificationsWithError:(NSError *)error NS_AVAILABLE_IOS(3_0);
 
-- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo NS_AVAILABLE_IOS(3_0);
+- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo NS_DEPRECATED_IOS(3_0, 10_0, "Use UserNotifications Framework's -[UNUserNotificationCenterDelegate willPresentNotification:withCompletionHandler:] or -[UNUserNotificationCenterDelegate didReceiveNotificationResponse:withCompletionHandler:] for user visible notifications and -[UIApplicationDelegate application:didReceiveRemoteNotification:fetchCompletionHandler:] for silent remote notifications");
 
-- (void)application:(UIApplication *)application didReceiveLocalNotification:(UILocalNotification *)notification NS_AVAILABLE_IOS(4_0) __TVOS_PROHIBITED;
+- (void)application:(UIApplication *)application didReceiveLocalNotification:(UILocalNotification *)notification NS_DEPRECATED_IOS(4_0, 10_0, "Use UserNotifications Framework's -[UNUserNotificationCenterDelegate willPresentNotification:withCompletionHandler:] or -[UNUserNotificationCenterDelegate didReceiveNotificationResponse:withCompletionHandler:]") __TVOS_PROHIBITED;
 
 // Called when your app has been activated by the user selecting an action from a local notification.
 // A nil action identifier indicates the default action.
 // You should call the completion handler as soon as you've finished handling the action.
-- (void)application:(UIApplication *)application handleActionWithIdentifier:(nullable NSString *)identifier forLocalNotification:(UILocalNotification *)notification completionHandler:(void(^)())completionHandler NS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED;
-- (void)application:(UIApplication *)application handleActionWithIdentifier:(nullable NSString *)identifier forRemoteNotification:(NSDictionary *)userInfo withResponseInfo:(NSDictionary *)responseInfo completionHandler:(void(^)())completionHandler NS_AVAILABLE_IOS(9_0) __TVOS_PROHIBITED;
+- (void)application:(UIApplication *)application handleActionWithIdentifier:(nullable NSString *)identifier forLocalNotification:(UILocalNotification *)notification completionHandler:(void(^)())completionHandler NS_DEPRECATED_IOS(8_0, 10_0, "Use UserNotifications Framework's -[UNUserNotificationCenterDelegate didReceiveNotificationResponse:withCompletionHandler:]") __TVOS_PROHIBITED;
+
+- (void)application:(UIApplication *)application handleActionWithIdentifier:(nullable NSString *)identifier forRemoteNotification:(NSDictionary *)userInfo withResponseInfo:(NSDictionary *)responseInfo completionHandler:(void(^)())completionHandler NS_DEPRECATED_IOS(9_0, 10_0, "Use UserNotifications Framework's -[UNUserNotificationCenterDelegate didReceiveNotificationResponse:withCompletionHandler:]") __TVOS_PROHIBITED;
 
 // Called when your app has been activated by the user selecting an action from a remote notification.
 // A nil action identifier indicates the default action.
 // You should call the completion handler as soon as you've finished handling the action.
-- (void)application:(UIApplication *)application handleActionWithIdentifier:(nullable NSString *)identifier forRemoteNotification:(NSDictionary *)userInfo completionHandler:(void(^)())completionHandler NS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED;
-- (void)application:(UIApplication *)application handleActionWithIdentifier:(nullable NSString *)identifier forLocalNotification:(UILocalNotification *)notification withResponseInfo:(NSDictionary *)responseInfo completionHandler:(void(^)())completionHandler NS_AVAILABLE_IOS(9_0) __TVOS_PROHIBITED;
+- (void)application:(UIApplication *)application handleActionWithIdentifier:(nullable NSString *)identifier forRemoteNotification:(NSDictionary *)userInfo completionHandler:(void(^)())completionHandler NS_DEPRECATED_IOS(8_0, 10_0, "Use UserNotifications Framework's -[UNUserNotificationCenterDelegate didReceiveNotificationResponse:withCompletionHandler:]") __TVOS_PROHIBITED;
+
+- (void)application:(UIApplication *)application handleActionWithIdentifier:(nullable NSString *)identifier forLocalNotification:(UILocalNotification *)notification withResponseInfo:(NSDictionary *)responseInfo completionHandler:(void(^)())completionHandler NS_DEPRECATED_IOS(9_0, 10_0, "Use UserNotifications Framework's -[UNUserNotificationCenterDelegate didReceiveNotificationResponse:withCompletionHandler:]") __TVOS_PROHIBITED;
 
 /*! This delegate method offers an opportunity for applications with the "remote-notification" background mode to fetch appropriate new data in response to an incoming remote notification. You should call the fetchCompletionHandler as soon as you're finished performing that operation, so the system can accurately estimate its power and data cost.
  
  This method will be invoked even if the application was launched or resumed because of the remote notification. The respective delegate methods will be invoked first. Note that this behavior is in contrast to application:didReceiveRemoteNotification:, which is not called in those cases, and which will not be invoked if this method is implemented. !*/
-- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))completionHandler NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
+- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))completionHandler NS_AVAILABLE_IOS(7_0);
 
 /// Applications with the "fetch" background mode may be given opportunities to fetch updated content in the background or when it is convenient for the system. This method will be called in these situations. You should call the fetchCompletionHandler as soon as you're finished performing that operation, so the system can accurately estimate its power and data cost.
 - (void)application:(UIApplication *)application performFetchWithCompletionHandler:(void (^)(UIBackgroundFetchResult result))completionHandler NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
@@ -367,6 +376,10 @@
 
 // This is called on the main thread when a user activity managed by UIKit has been updated. You can use this as a last chance to add additional data to the userActivity.
 - (void)application:(UIApplication *)application didUpdateUserActivity:(NSUserActivity *)userActivity NS_AVAILABLE_IOS(8_0);
+
+#pragma mark -- CloudKit Sharing Invitation Handling --
+- (void) application:(UIApplication *)application userAcceptedCloudKitShareWithMetadata:(CKShareMetadata *)cloudKitShareMetadata NS_AVAILABLE_IOS(10_0);
+
 @end
 
 @interface UIApplication(UIApplicationDeprecated)
@@ -416,7 +429,7 @@
 UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsURLKey                   NS_AVAILABLE_IOS(3_0); // userInfo contains NSURL with launch URL
 UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsSourceApplicationKey     NS_AVAILABLE_IOS(3_0); // userInfo contains NSString with launch app bundle ID
 UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsRemoteNotificationKey    NS_AVAILABLE_IOS(3_0) __TVOS_PROHIBITED; // userInfo contains NSDictionary with payload
-UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsLocalNotificationKey     NS_AVAILABLE_IOS(4_0) __TVOS_PROHIBITED; // userInfo contains a UILocalNotification
+UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsLocalNotificationKey     NS_DEPRECATED_IOS(4_0, 10_0, "Use UserNotifications Framework's -[UNUserNotificationCenterDelegate didReceiveNotificationResponse:withCompletionHandler:]") __TVOS_PROHIBITED; // userInfo contains a UILocalNotification
 UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsAnnotationKey            NS_AVAILABLE_IOS(3_2); // userInfo contains object with annotation property list
 UIKIT_EXTERN NSString *const UIApplicationProtectedDataWillBecomeUnavailable    NS_AVAILABLE_IOS(4_0);
 UIKIT_EXTERN NSString *const UIApplicationProtectedDataDidBecomeAvailable       NS_AVAILABLE_IOS(4_0);
@@ -429,6 +442,7 @@
 // Key in options dict passed to application:[will | did]FinishLaunchingWithOptions and info for UIApplicationDidFinishLaunchingNotification
 UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsUserActivityDictionaryKey    NS_AVAILABLE_IOS(8_0); // Sub-Dictionary present in launch options when user activity is present
 UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsUserActivityTypeKey          NS_AVAILABLE_IOS(8_0); // Key in user activity dictionary for the activity type
+UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsCloudKitShareMetadataKey NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED; // The presence of this key indicates that the app was launched in order to handle a CloudKit sharing invitation. The value of this key is a CKShareMetadata object.
 
 UIKIT_EXTERN NSString *const UIApplicationOpenSettingsURLString NS_AVAILABLE_IOS(8_0);
 
@@ -438,6 +452,7 @@
 UIKIT_EXTERN NSString *const UIApplicationOpenURLOptionsOpenInPlaceKey NS_AVAILABLE_IOS(9_0);   // value is a bool NSNumber, set to YES if the file needs to be copied before use
 
 // Content size category constants
+UIKIT_EXTERN NSString *const UIContentSizeCategoryUnspecified NS_AVAILABLE_IOS(10_0);
 UIKIT_EXTERN NSString *const UIContentSizeCategoryExtraSmall NS_AVAILABLE_IOS(7_0);
 UIKIT_EXTERN NSString *const UIContentSizeCategorySmall NS_AVAILABLE_IOS(7_0);
 UIKIT_EXTERN NSString *const UIContentSizeCategoryMedium NS_AVAILABLE_IOS(7_0);
@@ -463,4 +478,10 @@
 // Extension point identifier constants
 UIKIT_EXTERN NSString *const UIApplicationKeyboardExtensionPointIdentifier NS_AVAILABLE_IOS(8_0);
 
+#pragma mark -- openURL options --
+
+// Option for openURL:options:CompletionHandler: only open URL if it is a valid universal link with an application configured to open it
+// If there is no application configured, or the user disabled using it to open the link, completion handler called with NO
+UIKIT_EXTERN NSString *const UIApplicationOpenURLOptionUniversalLinksOnly;
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICloudSharingController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICloudSharingController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICloudSharingController.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICloudSharingController.h	2016-06-03 05:02:46.000000000 +0200
@@ -0,0 +1,66 @@
+//
+//  UICloudSharingController.h
+//  UIKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <UIKit/UIKit.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class UICloudSharingController, CKShare, CKContainer;
+
+typedef NS_OPTIONS(NSUInteger, UICloudSharingPermissionOptions) {
+    // Choose one or none of the following
+    UICloudSharingPermissionPublicOnly = 1 << 0,    // The user is only allowed to share publicly
+    UICloudSharingPermissionPrivateOnly = 1 << 1,   // The user is only allowed to share privately
+
+    // Choose one or none of the following
+    UICloudSharingPermissionReadOnly = 1 << 2,  // The user is only allowed to grant participants read-only permissions
+    UICloudSharingPermissionReadWrite = 1 << 3, // The user is only allowed to grant participants read/write permissions
+};
+
+@protocol UICloudSharingControllerDelegate <NSObject>
+
+- (void)cloudSharingController:(UICloudSharingController *)csc failedToSaveShareWithError:(NSError *)error;
+
+@optional
+- (void)cloudSharingControllerDidSaveShare:(UICloudSharingController *)csc;
+- (void)cloudSharingControllerDidStopSharing:(UICloudSharingController *)csc;
+
+@end
+
+NS_CLASS_AVAILABLE_IOS(10_0) @interface UICloudSharingController : UIViewController
+
+- (instancetype)initWithNibName:(nullable NSString *)nibNameOrNil bundle:(nullable NSBundle *)nibBundleOrNil NS_UNAVAILABLE;
+- (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_UNAVAILABLE;
+
+/* Use this initializer when you want to share a set of CKRecords but haven't yet saved a CKShare.
+ The passed-in, not-yet-saved share can have keys such as the title or thumbnail set.
+ The preparation handler is called when it is time to save the share to the server.
+ After ensuring the share and record have been saved to the server, invoke the preparationCompletionHandler
+ with either the resulting CKShare, or an NSError if saving failed.
+ */
+- (instancetype)initWithShare:(CKShare *)share preparationHandler:(void (^)(UICloudSharingController *controller, void (^preparationCompletionHandler)(CKShare * _Nullable, CKContainer * _Nullable, NSError * _Nullable)))preparationHandler;
+
+/* Use this initializer when you already have an active CKShare that was set up previously.
+ */
+- (instancetype)initWithShare:(CKShare *)share container:(CKContainer *)container;
+
+@property (nonatomic, weak) id<UICloudSharingControllerDelegate> delegate;
+@property (nonatomic, readonly, strong, nullable) CKShare *share;
+
+/* Restrict the sharing invitation UI to specific types of share permissions. If set, only the specified combinations of permissions are selectable.
+ */
+@property (nonatomic) UICloudSharingPermissionOptions availablePermissions;
+
+/* Returns an activity item source for use with UIActivityViewController.
+ If the activity is selected, delegate methods will be called for the original instance of
+ the sharing controller.
+ */
+- (id <UIActivityItemSource>)activityItemSource;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionView.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionView.h	2016-06-03 05:02:20.000000000 +0200
@@ -51,7 +51,7 @@
 - (NSInteger)collectionView:(UICollectionView *)collectionView numberOfItemsInSection:(NSInteger)section;
 
 // The cell that is returned must be retrieved from a call to -dequeueReusableCellWithReuseIdentifier:forIndexPath:
-- (UICollectionViewCell *)collectionView:(UICollectionView *)collectionView cellForItemAtIndexPath:(NSIndexPath *)indexPath;
+- (__kindof UICollectionViewCell *)collectionView:(UICollectionView *)collectionView cellForItemAtIndexPath:(NSIndexPath *)indexPath;
 
 @optional
 
@@ -65,6 +65,18 @@
 
 @end
 
+@protocol UICollectionViewDataSourcePrefetching <NSObject>
+@required
+// indexPaths are ordered ascending by geometric distance from the collection view
+- (void)collectionView:(UICollectionView *)collectionView prefetchItemsAtIndexPaths:(NSArray<NSIndexPath *> *)indexPaths NS_AVAILABLE_IOS(10_0);
+
+@optional
+// indexPaths that previously were considered as candidates for pre-fetching, but were not actually used; may be a subset of the previous call to -collectionView:prefetchItemsAtIndexPaths:
+- (void)collectionView:(UICollectionView *)collectionView cancelPrefetchingForItemsAtIndexPaths:(NSArray<NSIndexPath *> *)indexPaths  NS_AVAILABLE_IOS(10_0);
+
+@end
+
+
 @protocol UICollectionViewDelegate <UIScrollViewDelegate>
 @optional
 
@@ -121,6 +133,10 @@
 @property (nonatomic, strong) UICollectionViewLayout *collectionViewLayout;
 @property (nonatomic, weak, nullable) id <UICollectionViewDelegate> delegate;
 @property (nonatomic, weak, nullable) id <UICollectionViewDataSource> dataSource;
+
+@property (nonatomic, weak, nullable) id<UICollectionViewDataSourcePrefetching> prefetchDataSource NS_AVAILABLE_IOS(10_0);
+@property (nonatomic, getter=isPrefetchingEnabled) BOOL prefetchingEnabled NS_AVAILABLE_IOS(10_0);
+
 @property (nonatomic, strong, nullable) UIView *backgroundView; // will be automatically resized to track the size of the collection view and placed behind all cells and supplementary views.
 
 // For each reuse identifier that the collection view will use, register either a class or a nib from which to instantiate a cell.
@@ -167,7 +183,7 @@
 - (NSArray<__kindof UICollectionViewCell *> *)visibleCells;
 - (NSArray<NSIndexPath *> *)indexPathsForVisibleItems;
 
-- (UICollectionReusableView *)supplementaryViewForElementKind:(NSString *)elementKind atIndexPath:(NSIndexPath *)indexPath NS_AVAILABLE_IOS(9_0);
+- (nullable UICollectionReusableView *)supplementaryViewForElementKind:(NSString *)elementKind atIndexPath:(NSIndexPath *)indexPath NS_AVAILABLE_IOS(9_0);
 - (NSArray<UICollectionReusableView *> *)visibleSupplementaryViewsOfKind:(NSString *)elementKind NS_AVAILABLE_IOS(9_0);
 - (NSArray<NSIndexPath *> *)indexPathsForVisibleSupplementaryElementsOfKind:(NSString *)elementKind NS_AVAILABLE_IOS(9_0);
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewFlowLayout.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewFlowLayout.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewFlowLayout.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewFlowLayout.h	2016-06-03 05:02:46.000000000 +0200
@@ -14,6 +14,7 @@
 
 UIKIT_EXTERN NSString *const UICollectionElementKindSectionHeader NS_AVAILABLE_IOS(6_0);
 UIKIT_EXTERN NSString *const UICollectionElementKindSectionFooter NS_AVAILABLE_IOS(6_0);
+UIKIT_EXTERN const CGSize UICollectionViewFlowLayoutAutomaticSize  NS_AVAILABLE_IOS(10_0);
 
 typedef NS_ENUM(NSInteger, UICollectionViewScrollDirection) {
     UICollectionViewScrollDirectionVertical,
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewTransitionLayout.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewTransitionLayout.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewTransitionLayout.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewTransitionLayout.h	2016-06-03 05:02:47.000000000 +0200
@@ -5,7 +5,7 @@
 //  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
 //
 
-#import <UIKit/UIKit.h>
+#import <UIKit/UICollectionViewLayout.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIColor.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIColor.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIColor.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIColor.h	2016-05-23 08:16:41.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIContentSizeCategoryAdjusting.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIContentSizeCategoryAdjusting.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIContentSizeCategoryAdjusting.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIContentSizeCategoryAdjusting.h	2016-06-03 05:02:46.000000000 +0200
@@ -0,0 +1,23 @@
+//
+//  UIContentSizeCategoryAdjusting.h
+//  UIKit
+//
+//  Copyright (c) 2016-2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <UIKit/UIKitDefines.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+NS_CLASS_AVAILABLE_IOS(10_0) @protocol UIContentSizeCategoryAdjusting <NSObject>
+
+/*
+ Indicates whether the corresponding element should automatically update its font when the device’s UIContentSizeCategory is changed.
+ For this property to take effect, the element’s font must be a font vended using +preferredFontForTextStyle: or +preferredFontForTextStyle:compatibleWithTraitCollection: with a valid UIFontTextStyle.
+ */
+@property (nonatomic) BOOL adjustsFontForContentSizeCategory;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDataDetectors.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDataDetectors.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDataDetectors.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDataDetectors.h	2016-06-03 05:02:46.000000000 +0200
@@ -2,17 +2,20 @@
 //  UIDataDetectors.h
 //  UIKit
 //
-//  Copyright (c) 2009-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2009-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
 
 typedef NS_OPTIONS(NSUInteger, UIDataDetectorTypes) {
-    UIDataDetectorTypePhoneNumber                              = 1 << 0,          // Phone number detection
-    UIDataDetectorTypeLink                                     = 1 << 1,          // URL detection
-    UIDataDetectorTypeAddress NS_ENUM_AVAILABLE_IOS(4_0)       = 1 << 2,          // Street address detection
-    UIDataDetectorTypeCalendarEvent NS_ENUM_AVAILABLE_IOS(4_0) = 1 << 3,          // Event detection
+    UIDataDetectorTypePhoneNumber                                        = 1 << 0, // Phone number detection
+    UIDataDetectorTypeLink                                               = 1 << 1, // URL detection
+    UIDataDetectorTypeAddress NS_ENUM_AVAILABLE_IOS(4_0)                 = 1 << 2, // Street address detection
+    UIDataDetectorTypeCalendarEvent NS_ENUM_AVAILABLE_IOS(4_0)           = 1 << 3, // Event detection
+    UIDataDetectorTypeShipmentTrackingNumber NS_ENUM_AVAILABLE_IOS(10_0) = 1 << 4, // Shipment tracking number detection
+    UIDataDetectorTypeFlightNumber NS_ENUM_AVAILABLE_IOS(10_0)           = 1 << 5, // Flight number detection
+    UIDataDetectorTypeLookupSuggestion NS_ENUM_AVAILABLE_IOS(10_0)       = 1 << 6, // Information users may want to look up
 
-    UIDataDetectorTypeNone          = 0,               // No detection at all
-    UIDataDetectorTypeAll           = NSUIntegerMax    // All types
+    UIDataDetectorTypeNone          = 0,               // Disable detection
+    UIDataDetectorTypeAll           = NSUIntegerMax    // Enable all types, including types that may be added later
 } __TVOS_PROHIBITED;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDocument.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDocument.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDocument.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDocument.h	2016-06-03 05:02:20.000000000 +0200
@@ -25,7 +25,7 @@
 typedef NS_OPTIONS(NSUInteger, UIDocumentState) {
     UIDocumentStateNormal            = 0,
     UIDocumentStateClosed            = 1 << 0, // The document has either not been successfully opened, or has been since closed. Document properties may not be valid.
-    UIDocumentStateInConflict        = 1 << 1, // Conflicts exist for the document's fileURL. They can be accessed through +[NSFileVersion otherVersionsOfItemAtURL:].
+    UIDocumentStateInConflict        = 1 << 1, // Conflicts exist for the document's fileURL. They can be accessed through +[NSFileVersion unresolvedConflictVersionsOfItemAtURL:].
     UIDocumentStateSavingError       = 1 << 2, // An error has occurred that prevents the document from saving.
     UIDocumentStateEditingDisabled   = 1 << 3, // Set before calling -disableEditing. The document is is busy and it is not currently safe to allow user edits. -enableEditing will be called when it becomes safe to edit again.
     UIDocumentStateProgressAvailable = 1 << 4  // Set if the document is busy loading or saving. Progress is valid while this is set.
@@ -52,6 +52,8 @@
 
 @property (readonly) UIDocumentState documentState __TVOS_PROHIBITED;
 
+@property (readonly, nullable) NSProgress *progress NS_AVAILABLE_IOS(9_0) __TVOS_PROHIBITED; // The download or upload progress of a document. Valid while UIDocumentStateProgressAvailable is set.
+
 #pragma mark *** Opening and Closing ***
 
 // Subclassing this method without calling super should be avoided. Subclassers who don't call super must use NSFileCoordinator for coordinated reading themselves.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFocus.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFocus.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFocus.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFocus.h	2016-06-03 06:16:42.000000000 +0200
@@ -6,12 +6,13 @@
 //
 
 #import <Foundation/Foundation.h>
-#import <UIKit/UILayoutGuide.h>
+#import <UIKit/UIFocusGuide.h>
 #import <UIKit/UIFocusAnimationCoordinator.h>
 
-@class UIView;
+@class UIView, UIFocusUpdateContext;
 
 typedef NS_OPTIONS(NSUInteger, UIFocusHeading) {
+    UIFocusHeadingNone          = 0,
     UIFocusHeadingUp            = 1 << 0,
     UIFocusHeadingDown          = 1 << 1,
     UIFocusHeadingLeft          = 1 << 2,
@@ -23,50 +24,63 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-/// UIFocusUpdateContexts provide information relevant to a specific focus update from one view to another. They are ephemeral objects that are usually discarded after the update is finished.
-NS_CLASS_AVAILABLE_IOS(9_0) @interface UIFocusUpdateContext : NSObject
-
-/// The view that was focused before the update. May be nil if no view was focused, such as when setting initial focus.
-@property (nonatomic, weak, readonly, nullable) UIView *previouslyFocusedView;
-
-/// The view that will be focused after the update. May be nil if no view will be focused.
-@property (nonatomic, weak, readonly, nullable) UIView *nextFocusedView;
-
-/// The focus heading in which the update is occuring.
-@property (nonatomic, assign, readonly) UIFocusHeading focusHeading;
-
-@end
-
-
-/// UIFocusEnvironments represent branches of the view hierarchy participating in the focus system.
+/// Objects conforming to UIFocusEnvironment influence and respond to focus behavior within a specific area of the screen that they control.
 NS_CLASS_AVAILABLE_IOS(9_0) @protocol UIFocusEnvironment <NSObject>
 
-/// The preferred focused view is the view that will be focused when focus is updated programmatically. This includes setting initial focus and forcing updates via -updateFocusIfNeeded. May be self in the case of UIView instances.
-@property (nonatomic, weak, readonly, nullable) UIView *preferredFocusedView;
+/// The preferred focus environments define where to search for the default focused item in an environment, such as when focus updates programmatically.
+/// Starting from the target environment, each preferred focus environment is recursively searched in the order of the array until an eligible, focusable item is found.
+/// Preferred focus environments can include focusable and non-focusable items, in addition to non-item environments. Returning an empty array is equivalent to returning an array containing only 'self'.
+@property (nonatomic, copy, readonly) NSArray<id<UIFocusEnvironment>> *preferredFocusEnvironments;
 
-/// Marks this environment as needing a focus update, which if accepted will reset focus to the preferred focused view on the next update cycle. If this environment does not currently contain the focused view, then calling this method has no effect. If a parent of this environment is also requesting focus, then that parent's preferred focused view is used instead.
+/// Marks this environment as needing a focus update, which if accepted will attempt to reset focus to this environment, or one of its preferred focus environments, on the next update cycle. If this environment does not currently contain the focused item, then calling this method has no effect. If a parent of this environment is also requesting focus, then this environment's request is rejected in favor of the parent's.
 - (void)setNeedsFocusUpdate;
 
-/// Forces focus to be updated immediately. If there is an environment that has requested a focus update via -setNeedsFocusUpdate, and the request was accepted, then focus will be updated to that environment's preferred focused view.
+/// Forces focus to be updated immediately. If there is an environment that has requested a focus update via -setNeedsFocusUpdate, and the request was accepted, then focus will be updated to that environment or one of its preferred focus environments.
 - (void)updateFocusIfNeeded;
 
 /// Asks whether the system should allow a focus update to occur.
 - (BOOL)shouldUpdateFocusInContext:(UIFocusUpdateContext *)context;
 
-/// Called when the screen’s focusedView has been updated to a new view. Use the animation coordinator to schedule focus-related animations in response to the update.
+/// Called when the screen’s focused item has been updated to a new item. Use the animation coordinator to schedule focus-related animations in response to the update.
 - (void)didUpdateFocusInContext:(UIFocusUpdateContext *)context withAnimationCoordinator:(UIFocusAnimationCoordinator *)coordinator;
 
+@optional
+
+@property (nonatomic, weak, readonly, nullable) UIView *preferredFocusedView NS_DEPRECATED_IOS(9_0, 10_0, "Use -preferredFocusEnvironments instead.");
+
+@end
+
+
+/// Objects conforming to UIFocusItem are considered capable of participating in focus. Only UIFocusItems can ever be focused.
+/// NOTE: This protocol is not currently meant to be conformed to by third-party classes.
+NS_CLASS_AVAILABLE_IOS(10_0) @protocol UIFocusItem <UIFocusEnvironment>
+
+/// Indicates whether or not this item is currently allowed to become focused.
+/// Returning NO restricts the item from being focusable, even if it is visible in the user interface. For example, UIControls return NO if they are disabled.
+- (BOOL)canBecomeFocused;
+
 @end
 
 
-/// UIFocusGuides are UILayoutGuide subclasses that participate in the focus system from within their owning view. A UIFocusGuide may be used to expose non-view areas as focusable.
-NS_CLASS_AVAILABLE_IOS(9_0) @interface UIFocusGuide : UILayoutGuide
+/// UIFocusUpdateContexts provide information relevant to a specific focus update from one view to another. They are ephemeral objects that are usually discarded after the update is finished.
+NS_CLASS_AVAILABLE_IOS(9_0) @interface UIFocusUpdateContext : NSObject
+
+/// The item that was focused before the update, i.e. where focus is updating from. May be nil if no item was focused, such as when focus is initially set.
+@property (nonatomic, weak, readonly, nullable) id<UIFocusItem> previouslyFocusedItem NS_AVAILABLE_IOS(10_0);
+
+/// The item that is focused after the update, i.e. where focus is updating to. May be nil if no item is being focused, meaning focus is being lost.
+@property (nonatomic, weak, readonly, nullable) id<UIFocusItem> nextFocusedItem NS_AVAILABLE_IOS(10_0);
+
+/// The view that was focused before the update. May be nil if no view was focused, such as when setting initial focus.
+/// If previouslyFocusedItem is not a view, this returns that item's containing view, otherwise they are equal.
+@property (nonatomic, weak, readonly, nullable) UIView *previouslyFocusedView;
 
-/// If disabled, UIFocusGuides are ignored by the focus engine, but still participate in layout. Modifying this flag allows you to conditionally enable or disable certain focus behaviors. YES by default.
-@property (nonatomic, getter=isEnabled) BOOL enabled;
+/// The view that will be focused after the update. May be nil if no view will be focused.
+/// If nextFocusedItem is not a view, this returns that item's containing view, otherwise they are equal.
+@property (nonatomic, weak, readonly, nullable) UIView *nextFocusedView;
 
-/// Setting a preferred focused view marks this guide's layoutFrame as focusable, and if focused, redirects focus to its preferred focused view. If nil, this guide is effectively disabled.
-@property (nonatomic, weak, nullable) UIView *preferredFocusedView;
+/// The focus heading in which the update is occuring.
+@property (nonatomic, assign, readonly) UIFocusHeading focusHeading;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFocusGuide.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFocusGuide.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFocusGuide.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFocusGuide.h	2016-06-03 05:02:46.000000000 +0200
@@ -0,0 +1,29 @@
+//
+//  UIFocusGuide.h
+//  UIKit
+//
+//  Copyright © 2015 Apple Inc. All rights reserved.
+//
+
+#import <UIKit/UILayoutGuide.h>
+
+@protocol UIFocusEnvironment;
+
+NS_ASSUME_NONNULL_BEGIN
+
+/// UIFocusGuides are UILayoutGuide subclasses that participate in the focus system from within their owning view. A UIFocusGuide may be used to expose non-view areas as focusable.
+NS_CLASS_AVAILABLE_IOS(9_0) @interface UIFocusGuide : UILayoutGuide
+
+/// If disabled, UIFocusGuides are ignored by the focus engine, but still participate in layout. Modifying this flag allows you to conditionally enable or disable certain focus behaviors. YES by default.
+@property (nonatomic, getter=isEnabled) BOOL enabled;
+
+/// Setting preferredFocusEnvironments to a non-empty array marks this guide's layoutFrame as focusable. If empty, this guide is effectively disabled.
+/// If focused, the guide attempts to redirect focus to each environment in the array, in order, stopping when a focusable item in an environment has been found.
+@property (nonatomic, copy, null_resettable) NSArray<id<UIFocusEnvironment>> *preferredFocusEnvironments NS_AVAILABLE_IOS(10_0);
+
+/// Setting a preferred focused view marks this guide's layoutFrame as focusable, and if focused, redirects focus to its preferred focused view. If nil, this guide is effectively disabled.
+@property (nonatomic, weak, nullable) UIView *preferredFocusedView NS_DEPRECATED_IOS(9_0, 10_0, "Use -preferredFocusEnvironments instead.");
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h	2016-06-03 05:02:46.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h	2016-06-03 06:16:40.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGestureRecognizer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGestureRecognizer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGestureRecognizer.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGestureRecognizer.h	2016-06-03 05:02:46.000000000 +0200
@@ -54,6 +54,11 @@
 @property(nonatomic, copy) NSArray<NSNumber *> *allowedTouchTypes NS_AVAILABLE_IOS(9_0); // Array of UITouchType's as NSNumbers.
 @property(nonatomic, copy) NSArray<NSNumber *> *allowedPressTypes NS_AVAILABLE_IOS(9_0); // Array of UIPressTypes as NSNumbers.
 
+// Indicates whether the gesture recognizer will consider touches of different touch types simultaneously.
+// If NO, it receives all touches that match its allowedTouchTypes.
+// If YES, once it receives a touch of a certain type, it will ignore new touches of other types, until it is reset to UIGestureRecognizerStatePossible.
+@property (nonatomic) BOOL requiresExclusiveTouchType NS_AVAILABLE_IOS(9_2); // defaults to YES
+
 // create a relationship with another gesture recognizer that will prevent this gesture's actions from being called until otherGestureRecognizer transitions to UIGestureRecognizerStateFailed
 // if otherGestureRecognizer transitions to UIGestureRecognizerStateRecognized or UIGestureRecognizerStateBegan then this recognizer will instead transition to UIGestureRecognizerStateFailed
 // example usage: a single tap may require a double tap to fail
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGestureRecognizerSubclass.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGestureRecognizerSubclass.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGestureRecognizerSubclass.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGestureRecognizerSubclass.h	2016-06-03 05:02:46.000000000 +0200
@@ -48,7 +48,7 @@
 - (void)touchesMoved:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event;
 - (void)touchesEnded:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event;
 - (void)touchesCancelled:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event;
-- (void)touchesEstimatedPropertiesUpdated:(NSSet * _Nonnull)touches NS_AVAILABLE_IOS(9_1);
+- (void)touchesEstimatedPropertiesUpdated:(NSSet<UITouch *> *)touches NS_AVAILABLE_IOS(9_1);
 
 - (void)pressesBegan:(NSSet<UIPress *> *)presses withEvent:(UIPressesEvent *)event NS_AVAILABLE_IOS(9_0);
 - (void)pressesChanged:(NSSet<UIPress *> *)presses withEvent:(UIPressesEvent *)event NS_AVAILABLE_IOS(9_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphics.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphics.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphics.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphics.h	2016-06-03 05:02:46.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphicsImageRenderer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphicsImageRenderer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphicsImageRenderer.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphicsImageRenderer.h	2016-06-03 05:02:46.000000000 +0200
@@ -0,0 +1,42 @@
+//
+//  UIGraphicsImageRenderer.h
+//  UIKit
+//
+//  Copyright (c) 2016 Apple Inc. All rights reserved.
+//
+
+#import <UIKit/UIGraphicsRenderer.h>
+#import <UIKit/UIImage.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class UIGraphicsImageRendererContext;
+
+typedef void (^UIGraphicsImageDrawingActions)(UIGraphicsImageRendererContext *rendererContext) NS_AVAILABLE_IOS(10_0);
+
+
+NS_CLASS_AVAILABLE_IOS(10_0) @interface UIGraphicsImageRendererFormat : UIGraphicsRendererFormat
+@property (nonatomic) CGFloat scale; // display scale of the context. defaults to mainScreen scale.
+@property (nonatomic) BOOL opaque; // indicates the bitmap context will draw fully opaque. defaults to NO.
+@property (nonatomic) BOOL prefersExtendedRange; // indicates the bitmap context should draw into a context capable of rendering extended color images. Defaults to NO on hardware that does not support deep color, YES on hardware that does.
+@end
+
+NS_CLASS_AVAILABLE_IOS(10_0) @interface UIGraphicsImageRendererContext : UIGraphicsRendererContext
+@property (nonatomic, readonly) UIImage *currentImage; // Returns a UIImage representing the current state of the renderer's CGContext
+@end
+
+NS_CLASS_AVAILABLE_IOS(10_0) @interface UIGraphicsImageRenderer : UIGraphicsRenderer
+- (instancetype)initWithSize:(CGSize)size;
+- (instancetype)initWithSize:(CGSize)size format:(UIGraphicsImageRendererFormat *)format NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithBounds:(CGRect)bounds format:(UIGraphicsImageRendererFormat *)format NS_DESIGNATED_INITIALIZER;
+
+// Returns a UIImage rendered with the contents of the CGContext after the imageRenderBlock executes.
+// If the options provided to the renderer contain a rect with a zero width or height size, this will return an empty UIImage.
+- (UIImage *)imageWithActions:(NS_NOESCAPE UIGraphicsImageDrawingActions)actions;
+
+// These return compressed image data with the contents of the image drawn in the renderer block.
+- (NSData *)PNGDataWithActions:(NS_NOESCAPE UIGraphicsImageDrawingActions)actions;
+- (NSData *)JPEGDataWithCompressionQuality:(CGFloat)compressionQuality actions:(NS_NOESCAPE UIGraphicsImageDrawingActions)actions;
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphicsPDFRenderer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphicsPDFRenderer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphicsPDFRenderer.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphicsPDFRenderer.h	2016-06-03 05:02:46.000000000 +0200
@@ -0,0 +1,38 @@
+//
+//  UIGraphicsPDFRenderer.h
+//  UIKit
+//
+//  Copyright (c) 2016 Apple Inc. All rights reserved.
+//
+
+#import <UIKit/UIGraphicsRenderer.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class UIGraphicsPDFRendererContext;
+
+typedef void (^UIGraphicsPDFDrawingActions)(UIGraphicsPDFRendererContext *rendererContext) NS_AVAILABLE_IOS(10_0);
+
+NS_CLASS_AVAILABLE_IOS(10_0) @interface UIGraphicsPDFRendererFormat : UIGraphicsRendererFormat
+@property (nonatomic, copy) NSDictionary<NSString *, id> *documentInfo;
+@end
+
+NS_CLASS_AVAILABLE_IOS(10_0) @interface UIGraphicsPDFRendererContext : UIGraphicsRendererContext
+@property (nonatomic, readonly) CGRect pdfContextBounds;
+
+- (void)beginPage;
+- (void)beginPageWithBounds:(CGRect)bounds pageInfo:(NSDictionary<NSString *, id> *)pageInfo;
+
+- (void)setURL:(NSURL *)url forRect:(CGRect)rect;
+- (void)addDestinationWithName:(NSString *)name atPoint:(CGPoint)point;
+- (void)setDestinationWithName:(NSString *)name forRect:(CGRect)rect;
+@end
+
+NS_CLASS_AVAILABLE_IOS(10_0) @interface UIGraphicsPDFRenderer : UIGraphicsRenderer
+- (instancetype)initWithBounds:(CGRect)bounds format:(UIGraphicsPDFRendererFormat *)format NS_DESIGNATED_INITIALIZER;
+
+- (BOOL)writePDFToURL:(NSURL *)url withActions:(NS_NOESCAPE UIGraphicsPDFDrawingActions)actions error:(NSError **)error;
+- (NSData *)PDFDataWithActions:(NS_NOESCAPE UIGraphicsPDFDrawingActions)actions;
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphicsRenderer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphicsRenderer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphicsRenderer.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphicsRenderer.h	2016-06-03 05:02:46.000000000 +0200
@@ -0,0 +1,59 @@
+//
+//  UIGraphicsRenderer.h
+//  UIKit
+//
+//  Copyright (c) 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <CoreGraphics/CoreGraphics.h>
+#import <UIKit/UIView.h>
+
+
+NS_ASSUME_NONNULL_BEGIN
+
+/*
+ UIGraphicsRendererFormat is an object that describes the particular properties of the
+ context created by its associated renderer class.
+ */
+NS_CLASS_AVAILABLE_IOS(10_0) @interface UIGraphicsRendererFormat : NSObject <NSCopying>
+// returns a default configured format object, best suited for the current device.
++ (instancetype)defaultFormat;
+
+// returns the bounds for drawing into the owning UIGraphicsRendererContext.
+@property (nonatomic, readonly) CGRect bounds;
+@end
+
+/*
+ A UIGraphicsRendererContext provides primative drawing routines not provided through other
+ UIKit classes (UIImage, UIBezierPath, etc) in addition to providing access to the underlying
+ CGContextRef.
+ */
+NS_CLASS_AVAILABLE_IOS(10_0) @interface UIGraphicsRendererContext : NSObject
+@property (nonatomic, readonly) CGContextRef CGContext;
+@property (nonatomic, readonly) __kindof UIGraphicsRendererFormat *format;
+
+- (void)fillRect:(CGRect)rect;
+- (void)fillRect:(CGRect)rect blendMode:(CGBlendMode)blendMode;
+
+- (void)strokeRect:(CGRect)rect;
+- (void)strokeRect:(CGRect)rect blendMode:(CGBlendMode)blendMode;
+
+- (void)clipToRect:(CGRect)rect;
+@end
+
+/*
+ An abstract base class for creating graphics renderers. Do not use this class directly.
+ */
+NS_CLASS_AVAILABLE_IOS(10_0) @interface UIGraphicsRenderer : NSObject
+// Creates a new UIGraphicsRenderer instance with the provides bounds and format, or a defaultFormat if none is provided.
+// The format instance is copied by the initializer, and the provided instance may be immediately reused
+// for creating other renderer instances with the same or different bounds.
+- (instancetype)initWithBounds:(CGRect)bounds;
+- (instancetype)initWithBounds:(CGRect)bounds format:(UIGraphicsRendererFormat *)format NS_DESIGNATED_INITIALIZER;
+
+@property (nonatomic, readonly) __kindof UIGraphicsRendererFormat *format; // The renderer format used to create this renderer instance. returned by copy.
+@property (nonatomic, readonly) BOOL allowsImageOutput; // If YES, this renderer may be used to generate CGImageRefs.
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphicsRendererSubclass.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphicsRendererSubclass.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphicsRendererSubclass.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGraphicsRendererSubclass.h	2016-06-03 05:02:46.000000000 +0200
@@ -0,0 +1,34 @@
+//
+//  UIGraphicsRendererSubclass.h
+//  UIKit
+//
+//  Copyright (c) 2016 Apple Inc. All rights reserved.
+//
+
+#import <UIKit/UIGraphicsRenderer.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+typedef void (^UIGraphicsDrawingActions)(__kindof UIGraphicsRendererContext *rendererContext) NS_AVAILABLE_IOS(10_0);
+
+/*
+ To create a subclass of UIGraphicsRenderer, you must include this header in your implimentation and override at least the following methods:
+    + (Class)rendererContextClass
+    + (nullable CGContextRef)contextWithFormat:(UIGraphicsRendererFormat *)format
+ */
+@interface UIGraphicsRenderer (UIGraphicsRendererProtected)
+// The Class of your UIGraphicsRendererContext subclass
++ (Class)rendererContextClass NS_AVAILABLE_IOS(10_0);
+
+// Override this to create a context with a custom format
++ (nullable CGContextRef)contextWithFormat:(UIGraphicsRendererFormat *)format CF_RETURNS_RETAINED NS_AVAILABLE_IOS(10_0);
+
+// Override this to provide a CGContext created by a renderer with a custom initial configuration
++ (void)prepareCGContext:(CGContextRef)context withRendererContext:(UIGraphicsRendererContext *)rendererContext NS_AVAILABLE_IOS(10_0);
+
+// Invokes the drawingActions with a context generated by +contextWithFormat:, captured in an instance of +rendererContextClass, after prepreation by +prepareCGContext:withRendererContext:
+// This method is not intended to be overridden.
+- (BOOL)runDrawingActions:(NS_NOESCAPE UIGraphicsDrawingActions)drawingActions completionActions:(nullable NS_NOESCAPE UIGraphicsDrawingActions)completionActions error:(NSError **)error NS_AVAILABLE_IOS(10_0);
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImage.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImage.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImage.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImage.h	2016-05-23 08:16:41.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImageAsset.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImageAsset.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImageAsset.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImageAsset.h	2016-06-03 05:02:46.000000000 +0200
@@ -17,7 +17,7 @@
 - (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
 
 - (UIImage *)imageWithTraitCollection:(UITraitCollection *)traitCollection; // Images returned hold a strong reference to the asset that created them
-- (void)registerImage:(UIImage *)image withTraitCollection:(UITraitCollection *)traitCollection;
+- (void)registerImage:(UIImage *)image withTraitCollection:(UITraitCollection *)traitCollection; // Adds a new variation to this image asset that is appropriate for the provided traits. Any traits not exposed by asset catalogs (such as forceTouchCapability) are ignored.
 - (void)unregisterImageWithTraitCollection:(UITraitCollection *)traitCollection; // removes only those images added with registerImage:withTraitCollection:
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIInputView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIInputView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIInputView.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIInputView.h	2016-06-03 05:02:46.000000000 +0200
@@ -5,7 +5,7 @@
 //  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
 //
 
-#import <UIKit/UIKit.h>
+#import <UIKit/UIView.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIInputViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIInputViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIInputViewController.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIInputViewController.h	2016-06-03 05:02:46.000000000 +0200
@@ -5,7 +5,8 @@
 //  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
 //
 
-#import <UIKit/UIKit.h>
+#import <Foundation/Foundation.h>
+#import <UIKit/UIViewController.h>
 #import <UIKit/UIInputView.h>
 #import <UIKit/UITextInput.h>
 
@@ -18,6 +19,10 @@
 @property (nullable, nonatomic, readonly) NSString *documentContextBeforeInput;
 @property (nullable, nonatomic, readonly) NSString *documentContextAfterInput;
 
+// An app can store UITextInputMode in its document context, when user switches to the document, the host will pass the inputMode as documentInputMode to the UIInputViewController,
+// which can switch to the inputMode and set primaryLanguage if it supports it.
+@property (nullable, nonatomic, readonly) UITextInputMode *documentInputMode NS_AVAILABLE_IOS(10_0);
+
 - (void)adjustTextPositionByCharacterOffset:(NSInteger)offset;
 
 @end
@@ -35,6 +40,11 @@
 - (void)dismissKeyboard;
 - (void)advanceToNextInputMode;
 
+// Launch inputMode list above the view when long pressing or swiping up from the view,
+// Advance to nextInputMode when short tapping on the view.
+// Example: [KeyboardButton addTarget:self action:@selector(handleInputModeListFromView:withEvent:) forControlEvents:UIControlEventAllTouchEvents].
+- (void)handleInputModeListFromView:(nonnull UIView *)view withEvent:(nonnull UIEvent *)event NS_AVAILABLE_IOS(10_0);
+
 // This will not provide a complete repository of a language's vocabulary.
 // It is solely intended to supplement existing lexicons.
 - (void)requestSupplementaryLexiconWithCompletion:(void (^)(UILexicon *))completionHandler;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIInterface.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIInterface.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIInterface.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIInterface.h	2016-06-03 05:02:46.000000000 +0200
@@ -28,6 +28,31 @@
     UIUserInterfaceSizeClassRegular     = 2,
 } NS_ENUM_AVAILABLE_IOS(8_0);
 
+typedef NS_ENUM(NSInteger, UIUserInterfaceStyle) {
+    UIUserInterfaceStyleUnspecified,
+    UIUserInterfaceStyleLight,
+    UIUserInterfaceStyleDark,
+} __TVOS_AVAILABLE(10_0) __IOS_PROHIBITED __WATCHOS_PROHIBITED;
+
+typedef NS_ENUM(NSInteger, UIUserInterfaceLayoutDirection) {
+    UIUserInterfaceLayoutDirectionLeftToRight,
+    UIUserInterfaceLayoutDirectionRightToLeft,
+} NS_ENUM_AVAILABLE_IOS(5_0);
+
+// These values are only used for the layout direction trait, which informs but does not completely dictate the layout direction of views. To determine the effective layout direction of a view, consult the UIView.effectiveUserInterfaceLayoutDirection property, whose values are members of the UIUserInterfaceLayoutDirection enum.
+typedef NS_ENUM(NSInteger, UITraitEnvironmentLayoutDirection) {
+    UITraitEnvironmentLayoutDirectionUnspecified = -1,
+    UITraitEnvironmentLayoutDirectionLeftToRight = UIUserInterfaceLayoutDirectionLeftToRight,
+    UITraitEnvironmentLayoutDirectionRightToLeft = UIUserInterfaceLayoutDirectionRightToLeft,
+} NS_ENUM_AVAILABLE_IOS(10_0);
+
+typedef NS_ENUM(NSInteger, UIDisplayGamut) {
+    UIDisplayGamutUnspecified = -1,
+    UIDisplayGamutSRGB,
+    UIDisplayGamutP3
+} NS_ENUM_AVAILABLE_IOS(10_0);
+
+
 // System colors
 
 @interface UIColor (UIColorSystemColors)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h	2016-06-03 05:02:19.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h	2016-06-03 05:02:46.000000000 +0200
@@ -21,6 +21,8 @@
 #define UIKIT_AVAILABLE_IOS_TVOS(_ios, _tvos) __IOS_AVAILABLE(_ios) __WATCHOS_UNAVAILABLE __TVOS_AVAILABLE(_tvos)
 #define UIKIT_AVAILABLE_IOS_WATCHOS_TVOS(_ios, _watchos, _tvos) __IOS_AVAILABLE(_ios) __WATCHOS_AVAILABLE(_watchos) __TVOS_AVAILABLE(_tvos)
 
+#define UIKIT_CLASS_AVAILABLE_IOS_ONLY(vers) UIKIT_EXTERN __IOS_AVAILABLE(vers) __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE
+#define UIKIT_CLASS_AVAILABLE_WATCHOS_ONLY(vers) UIKIT_EXTERN __IOS_UNAVAILABLE __WATCHOS_AVAILABLE(vers) __TVOS_UNAVAILABLE
 #define UIKIT_CLASS_AVAILABLE_TVOS_ONLY(vers) UIKIT_EXTERN __IOS_UNAVAILABLE __WATCHOS_UNAVAILABLE __TVOS_AVAILABLE(vers)
 #define UIKIT_CLASS_AVAILABLE_IOS_TVOS(_ios, _tvos) UIKIT_EXTERN __IOS_AVAILABLE(_ios) __WATCHOS_UNAVAILABLE __TVOS_AVAILABLE(_tvos)
 #define UIKIT_CLASS_AVAILABLE_IOS_WATCHOS_TVOS(_ios, _watchos, _tvos) UIKIT_EXTERN __IOS_AVAILABLE(_ios) __WATCHOS_AVAILABLE(_watchos) __TVOS_AVAILABLE(_tvos)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILabel.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILabel.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILabel.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILabel.h	2016-06-03 06:16:40.000000000 +0200
@@ -10,19 +10,20 @@
 #import <UIKit/UIView.h>
 #import <UIKit/UIStringDrawing.h>
 #import <UIKit/UIKitDefines.h>
+#import <UIKit/UIContentSizeCategoryAdjusting.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
 @class UIColor, UIFont;
 
-NS_CLASS_AVAILABLE_IOS(2_0) @interface UILabel : UIView <NSCoding>
+NS_CLASS_AVAILABLE_IOS(2_0) @interface UILabel : UIView <NSCoding, UIContentSizeCategoryAdjusting>
 
 @property(nullable, nonatomic,copy)   NSString           *text;            // default is nil
 @property(null_resettable, nonatomic,strong) UIFont      *font;            // default is nil (system font 17 plain)
 @property(null_resettable, nonatomic,strong) UIColor     *textColor;       // default is nil (text draws black)
 @property(nullable, nonatomic,strong) UIColor            *shadowColor;     // default is nil (no shadow)
 @property(nonatomic)        CGSize             shadowOffset;    // default is CGSizeMake(0, -1) -- a top shadow
-@property(nonatomic)        NSTextAlignment    textAlignment;   // default is NSTextAlignmentLeft
+@property(nonatomic)        NSTextAlignment    textAlignment;   // default is NSTextAlignmentNatural (before iOS 9, the default was NSTextAlignmentLeft)
 @property(nonatomic)        NSLineBreakMode    lineBreakMode;   // default is NSLineBreakByTruncatingTail. used for single and multiple lines of text
 
 // the underlying attributed string drawn by the label, if set, the label ignores the properties above.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILexicon.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILexicon.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILexicon.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILexicon.h	2016-06-03 05:02:46.000000000 +0200
@@ -5,7 +5,7 @@
 //  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
 //
 
-#import <UIKit/UIKit.h>
+#import <Foundation/Foundation.h>
 
 
 NS_ASSUME_NONNULL_BEGIN
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILocalNotification.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILocalNotification.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILocalNotification.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UILocalNotification.h	2016-06-03 05:02:46.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINavigationBar.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINavigationBar.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINavigationBar.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINavigationBar.h	2016-06-03 06:16:41.000000000 +0200
@@ -22,7 +22,7 @@
 
 NS_CLASS_AVAILABLE_IOS(2_0) @interface UINavigationBar : UIView <NSCoding, UIBarPositioning> 
 
-@property(nonatomic,assign) UIBarStyle barStyle __TVOS_PROHIBITED;
+@property(nonatomic,assign) UIBarStyle barStyle UI_APPEARANCE_SELECTOR __TVOS_PROHIBITED;
 @property(nullable,nonatomic,weak) id<UINavigationBarDelegate> delegate;
 
 /*
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINavigationController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINavigationController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINavigationController.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINavigationController.h	2016-06-03 06:16:41.000000000 +0200
@@ -37,7 +37,7 @@
 
 UIKIT_EXTERN const CGFloat UINavigationControllerHideShowBarDuration;
 
-@class UIView, UINavigationBar, UINavigationItem, UIToolbar, UILayoutContainerView;
+@class UIView, UINavigationBar, UINavigationItem, UIToolbar;
 @protocol UINavigationControllerDelegate;
 
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINibLoading.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINibLoading.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINibLoading.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UINibLoading.h	2016-06-03 05:02:46.000000000 +0200
@@ -8,15 +8,19 @@
 #import <Foundation/Foundation.h>
 #import <UIKit/UIKitDefines.h>
 
+NS_ASSUME_NONNULL_BEGIN
+
 UIKIT_EXTERN NSString * const UINibExternalObjects NS_AVAILABLE_IOS(3_0);
 
 @interface NSBundle(UINibLoadingAdditions)
-- (NSArray *)loadNibNamed:(NSString *)name owner:(id)owner options:(NSDictionary *)options;
+- (NSArray *)loadNibNamed:(NSString *)name owner:(nullable id)owner options:(nullable NSDictionary *)options;
 @end
 
 @interface NSObject(UINibLoadingAdditions)
-- (void)awakeFromNib;
+- (void)awakeFromNib NS_REQUIRES_SUPER;
 - (void)prepareForInterfaceBuilder NS_AVAILABLE_IOS(8_0);
 @end
 
 UIKIT_EXTERN NSString * const UINibProxiedObjectsKey NS_DEPRECATED_IOS(2_0, 3_0) __TVOS_PROHIBITED;
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPanGestureRecognizer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPanGestureRecognizer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPanGestureRecognizer.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPanGestureRecognizer.h	2016-06-03 05:02:46.000000000 +0200
@@ -22,7 +22,7 @@
 - (CGPoint)translationInView:(nullable UIView *)view;                        // translation in the coordinate system of the specified view
 - (void)setTranslation:(CGPoint)translation inView:(nullable UIView *)view;
 
-- (CGPoint)velocityInView:(nullable UIView *)view;                           // velocity of the pan in pixels/second in the coordinate system of the specified view
+- (CGPoint)velocityInView:(nullable UIView *)view;                           // velocity of the pan in points/second in the coordinate system of the specified view
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPasteboard.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPasteboard.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPasteboard.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPasteboard.h	2016-06-03 05:02:46.000000000 +0200
@@ -10,16 +10,12 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-UIKIT_EXTERN NSString *const UIPasteboardNameGeneral __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIPasteboardNameFind __TVOS_PROHIBITED;
+UIKIT_EXTERN NSString *const UIPasteboardNameGeneral __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+UIKIT_EXTERN NSString *const UIPasteboardNameFind __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_DEPRECATED_IOS(3_0, 10_0, "The Find pasteboard is no longer available.");
 
 @class UIColor, UIImage;
 
-NS_CLASS_AVAILABLE_IOS(3_0) __TVOS_PROHIBITED @interface UIPasteboard : NSObject
-{
-  @private
-    NSString * __nullable _name;
-}
+NS_CLASS_AVAILABLE_IOS(3_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED @interface UIPasteboard : NSObject
 
 + (UIPasteboard *)generalPasteboard;
 + (nullable UIPasteboard *)pasteboardWithName:(NSString *)pasteboardName create:(BOOL)create;
@@ -29,7 +25,8 @@
 
 + (void)removePasteboardWithName:(NSString *)pasteboardName;
 
-@property(getter=isPersistent,nonatomic) BOOL persistent;
+@property(readonly,getter=isPersistent,nonatomic) BOOL persistent;
+- (void)setPersistent:(BOOL)persistent NS_DEPRECATED_IOS(3_0, 10_0, "Do not set persistence on pasteboards. This property is set automatically.");
 @property(readonly,nonatomic) NSInteger changeCount;
 
 // First item
@@ -46,50 +43,63 @@
 // Multiple items
 
 @property(readonly,nonatomic) NSInteger numberOfItems;
-- (nullable NSArray *)pasteboardTypesForItemSet:(nullable NSIndexSet*)itemSet;
+- (nullable NSArray<NSArray<NSString *> *> *)pasteboardTypesForItemSet:(nullable NSIndexSet*)itemSet;
 
 - (BOOL)containsPasteboardTypes:(NSArray<NSString *> *)pasteboardTypes inItemSet:(nullable NSIndexSet *)itemSet;
-- (nullable NSIndexSet *)itemSetWithPasteboardTypes:(NSArray *)pasteboardTypes;
+- (nullable NSIndexSet *)itemSetWithPasteboardTypes:(NSArray<NSString *> *)pasteboardTypes;
 - (nullable NSArray *)valuesForPasteboardType:(NSString *)pasteboardType inItemSet:(nullable NSIndexSet *)itemSet;
 - (nullable NSArray *)dataForPasteboardType:(NSString *)pasteboardType inItemSet:(nullable NSIndexSet *)itemSet;
 
 // Direct access
 
-@property(nonatomic,copy) NSArray *items;
+@property(nonatomic,copy) NSArray<NSDictionary<NSString *, id> *> *items;
 - (void)addItems:(NSArray<NSDictionary<NSString *, id> *> *)items;
 
-@end
-
-// Notification
+typedef NSString * UIPasteboardOption NS_EXTENSIBLE_STRING_ENUM NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UIPasteboardOption const UIPasteboardOptionExpirationDate __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_AVAILABLE_IOS(10_0) NS_SWIFT_NAME(UIPasteboardOption.expirationDate); // Value: NSDate.
+UIKIT_EXTERN UIPasteboardOption const UIPasteboardOptionLocalOnly __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_AVAILABLE_IOS(10_0) NS_SWIFT_NAME(UIPasteboardOption.localOnly); // Value: NSNumber, boolean.
 
-UIKIT_EXTERN NSString *const UIPasteboardChangedNotification __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIPasteboardChangedTypesAddedKey __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIPasteboardChangedTypesRemovedKey __TVOS_PROHIBITED;
+- (void)setItems:(NSArray<NSDictionary<NSString *, id> *> *)items options:(NSDictionary<UIPasteboardOption, id> *)options NS_AVAILABLE_IOS(10_0);
 
-UIKIT_EXTERN NSString *const UIPasteboardRemovedNotification __TVOS_PROHIBITED;
+@property(nullable,nonatomic,copy) NSString *string __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+@property(nullable,nonatomic,copy) NSArray<NSString *> *strings __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
-// Extensions
+@property(nullable,nonatomic,copy) NSURL *URL __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+@property(nullable,nonatomic,copy) NSArray<NSURL *> *URLs __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
-UIKIT_EXTERN NSArray<NSString *> *UIPasteboardTypeListString __TVOS_PROHIBITED;
-UIKIT_EXTERN NSArray<NSString *> *UIPasteboardTypeListURL __TVOS_PROHIBITED;
-UIKIT_EXTERN NSArray<NSString *> *UIPasteboardTypeListImage __TVOS_PROHIBITED;
-UIKIT_EXTERN NSArray<NSString *> *UIPasteboardTypeListColor __TVOS_PROHIBITED;
+@property(nullable,nonatomic,copy) UIImage *image __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+@property(nullable,nonatomic,copy) NSArray<UIImage *> *images __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
-@interface UIPasteboard(UIPasteboardDataExtensions)
+@property(nullable,nonatomic,copy) UIColor *color __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+@property(nullable,nonatomic,copy) NSArray<UIColor *> *colors __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
-@property(nullable,nonatomic,copy) NSString *string __TVOS_PROHIBITED;
-@property(nullable,nonatomic,copy) NSArray<NSString *> *strings __TVOS_PROHIBITED;
+// Queries
 
-@property(nullable,nonatomic,copy) NSURL *URL __TVOS_PROHIBITED;
-@property(nullable,nonatomic,copy) NSArray<NSURL *> *URLs __TVOS_PROHIBITED;
+@property (nonatomic, readonly) BOOL hasStrings __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_AVAILABLE_IOS(10_0);
+@property (nonatomic, readonly) BOOL hasURLs __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_AVAILABLE_IOS(10_0);
+@property (nonatomic, readonly) BOOL hasImages __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_AVAILABLE_IOS(10_0);
+@property (nonatomic, readonly) BOOL hasColors __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_AVAILABLE_IOS(10_0);
 
-@property(nullable,nonatomic,copy) UIImage *image __TVOS_PROHIBITED;
-@property(nullable,nonatomic,copy) NSArray<UIImage *> *images __TVOS_PROHIBITED;
+@end
 
-@property(nullable,nonatomic,copy) UIColor *color __TVOS_PROHIBITED;
-@property(nullable,nonatomic,copy) NSArray<UIColor *> *colors __TVOS_PROHIBITED;
+// Notification
 
-@end
+UIKIT_EXTERN NSString *const UIPasteboardChangedNotification __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+UIKIT_EXTERN NSString *const UIPasteboardChangedTypesAddedKey __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+UIKIT_EXTERN NSString *const UIPasteboardChangedTypesRemovedKey __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+
+UIKIT_EXTERN NSString *const UIPasteboardRemovedNotification __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+
+// Types
+
+UIKIT_EXTERN NSArray<NSString *> *UIPasteboardTypeListString __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+UIKIT_EXTERN NSArray<NSString *> *UIPasteboardTypeListURL __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+UIKIT_EXTERN NSArray<NSString *> *UIPasteboardTypeListImage __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+UIKIT_EXTERN NSArray<NSString *> *UIPasteboardTypeListColor __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+
+// Use the following type in setItems: or setItems:options: to automatically insert appropriate UTIs for supported types.
+// Supported types are: NSString, NSURL, UIImage, UIColor, NSAttributedString.
+UIKIT_EXTERN NSString * const UIPasteboardTypeAutomatic __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_AVAILABLE_IOS(10_0);
 
 NS_ASSUME_NONNULL_END
     
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPickerView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPickerView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPickerView.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPickerView.h	2016-06-03 05:02:46.000000000 +0200
@@ -8,14 +8,13 @@
 #import <Foundation/Foundation.h>
 #import <CoreGraphics/CoreGraphics.h>
 #import <UIKit/UIView.h>
-#import <UIKit/UITableView.h>
 #import <UIKit/UIKitDefines.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
 @protocol UIPickerViewDataSource, UIPickerViewDelegate;
 
-NS_CLASS_AVAILABLE_IOS(2_0) __TVOS_PROHIBITED @interface UIPickerView : UIView <NSCoding, UITableViewDataSource>
+NS_CLASS_AVAILABLE_IOS(2_0) __TVOS_PROHIBITED @interface UIPickerView : UIView <NSCoding>
 
 @property(nullable,nonatomic,weak) id<UIPickerViewDataSource> dataSource;                // default is nil. weak reference
 @property(nullable,nonatomic,weak) id<UIPickerViewDelegate>   delegate;                  // default is nil. weak reference
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverPresentationController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverPresentationController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverPresentationController.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverPresentationController.h	2016-06-03 05:02:46.000000000 +0200
@@ -5,8 +5,6 @@
 //  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
 //
 
-#import <UIKit/UIKit.h>
-
 #import <UIKit/UIPresentationController.h>
 #import <UIKit/UIPopoverSupport.h>
 #import <UIKit/UIPopoverBackgroundView.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverSupport.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverSupport.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverSupport.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverSupport.h	2016-06-03 05:02:46.000000000 +0200
@@ -5,6 +5,8 @@
 //  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
 //
 
+#import <UIKit/UIViewController.h>
+
 typedef NS_OPTIONS(NSUInteger, UIPopoverArrowDirection) {
     UIPopoverArrowDirectionUp = 1UL << 0,
     UIPopoverArrowDirectionDown = 1UL << 1,
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPresentationController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPresentationController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPresentationController.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPresentationController.h	2016-06-03 05:02:46.000000000 +0200
@@ -51,7 +51,8 @@
 
 @property(nullable, nonatomic, weak) id <UIAdaptivePresentationControllerDelegate> delegate;
 
-- (instancetype)initWithPresentedViewController:(UIViewController *)presentedViewController presentingViewController:(UIViewController *)presentingViewController;
+- (instancetype)initWithPresentedViewController:(UIViewController *)presentedViewController presentingViewController:(nullable UIViewController *)presentingViewController NS_DESIGNATED_INITIALIZER;
+- (instancetype)init NS_UNAVAILABLE;
 
 // By default this implementation defers to the delegate, if one exists, or returns the current presentation style. UIFormSheetPresentationController, and
 // UIPopoverPresentationController override this implementation to return UIModalPresentationStyleFullscreen if the delegate does not provide an
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPressesEvent.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPressesEvent.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPressesEvent.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPressesEvent.h	2016-06-03 05:02:46.000000000 +0200
@@ -5,7 +5,9 @@
 //  Copyright (c) 2005-2015 Apple Inc. All rights reserved.
 //
 
-#import <UIKit/UIKit.h>
+#import <UIKit/UIEvent.h>
+#import <UIKit/UIPress.h>
+#import <UIKit/UIGestureRecognizer.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPreviewInteraction.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPreviewInteraction.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPreviewInteraction.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPreviewInteraction.h	2016-06-03 05:02:46.000000000 +0200
@@ -0,0 +1,44 @@
+//
+//  UIPreviewInteraction.h
+//  UIKit
+//
+//  Copyright (c) 2015-2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <UIKit/UIKitDefines.h>
+#import <UIKit/UIView.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@protocol UIPreviewInteractionDelegate;
+
+UIKIT_CLASS_AVAILABLE_IOS_ONLY(10_0) @interface UIPreviewInteraction : NSObject
+
+- (instancetype)initWithView:(UIView *)view NS_DESIGNATED_INITIALIZER;
+@property (nonatomic, readonly, weak) UIView *view;
+
+- (instancetype)init NS_UNAVAILABLE;
+
+@property (nonatomic, nullable, weak) id <UIPreviewInteractionDelegate> delegate;
+
+- (CGPoint)locationInCoordinateSpace:(nullable id <UICoordinateSpace>)coordinateSpace; // returns the current location of the touch that started the interaction
+- (void)cancelInteraction;
+
+@end
+
+@protocol UIPreviewInteractionDelegate <NSObject>
+
+- (void)previewInteraction:(UIPreviewInteraction *)previewInteraction didUpdatePreviewTransition:(CGFloat)transitionProgress ended:(BOOL)ended UIKIT_AVAILABLE_IOS_ONLY(10_0); // transitionProgress ranges from 0 to 1
+- (void)previewInteractionDidCancel:(UIPreviewInteraction *)previewInteraction UIKIT_AVAILABLE_IOS_ONLY(10_0);
+
+@optional
+
+- (BOOL)previewInteractionShouldBegin:(UIPreviewInteraction *)previewInteraction UIKIT_AVAILABLE_IOS_ONLY(10_0);
+
+// If implemented, a preview interaction will also trigger haptic feedback when detecting a commit (pop). The provided transitionProgress ranges from 0 to 1.
+- (void)previewInteraction:(UIPreviewInteraction *)previewInteraction didUpdateCommitTransition:(CGFloat)transitionProgress ended:(BOOL)ended UIKIT_AVAILABLE_IOS_ONLY(10_0);
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintFormatter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintFormatter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintFormatter.h	2015-10-03 01:47:14.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintFormatter.h	2016-06-03 05:02:46.000000000 +0200
@@ -24,7 +24,9 @@
 
 @property(nonatomic) CGFloat      maximumContentHeight __TVOS_PROHIBITED;      // default is 0.0. limits content to width
 @property(nonatomic) CGFloat      maximumContentWidth __TVOS_PROHIBITED;       // default is 0.0. limits content to height
-@property(nonatomic) UIEdgeInsets contentInsets __TVOS_PROHIBITED;             // default is UIEdgeInsetsZero. from edge of printableRect. applies to whole content. bottom inset unused
+@property(nonatomic) UIEdgeInsets contentInsets NS_DEPRECATED_IOS(4_2,10_0, "Use perPageContentInsets instead.") __TVOS_PROHIBITED;
+                                                                               // default is UIEdgeInsetsZero. from edge of printableRect. applies to whole content. bottom inset unused
+                                                                               // Deprecated in favor of perPageContentInsets which produces better output
 @property(nonatomic) UIEdgeInsets perPageContentInsets __TVOS_PROHIBITED;      // default is UIEdgeInsetsZero from edge of the page.  applies to content on each page (each edge applies to each page)
 
 @property(nonatomic)          NSInteger startPage __TVOS_PROHIBITED;           // default is NSNotFound
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintInfo.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintInfo.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintInfo.h	2015-10-03 01:47:14.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintInfo.h	2016-06-03 05:02:46.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIPrintInfo.h
 //  UIKit
 //
-//  Copyright 2010-2012 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
@@ -36,13 +36,12 @@
 + (UIPrintInfo *)printInfo;
 + (UIPrintInfo *)printInfoWithDictionary:(nullable NSDictionary *)dictionary;
 
-- (NSDictionary *)dictionaryRepresentation;
-
 @property(nullable,nonatomic,copy)     NSString                *printerID;         // default is nil. set after user selects printer
 @property(nonatomic,copy)     NSString                *jobName;           // default is application name
 @property(nonatomic)          UIPrintInfoOutputType    outputType;        // default is UIPrintInfoOutputGeneral
 @property(nonatomic)          UIPrintInfoOrientation   orientation;       // default is UIPrintInfoOrientationPortrait
 @property(nonatomic)          UIPrintInfoDuplex        duplex;            // default is based on document type (none for photo, long edge for other)
+@property(nonatomic,readonly)   NSDictionary *dictionaryRepresentation;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintInteractionController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintInteractionController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintInteractionController.h	2015-10-03 01:47:14.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintInteractionController.h	2016-06-03 05:02:46.000000000 +0200
@@ -40,7 +40,7 @@
 
 @property(nullable,nonatomic,strong) UIPrintInfo                             *printInfo;      // changes to printInfo ignored while printing. default is nil
 @property(nullable,nonatomic,weak)   id<UIPrintInteractionControllerDelegate> delegate;       // not retained. default is nil
-@property(nonatomic)        BOOL                                     showsPageRange; // default is NO.
+@property(nonatomic)        BOOL                                     showsPageRange NS_DEPRECATED_IOS(4_2,10_0, "Pages can be removed from the print preview, so page range is always shown.");
 @property(nonatomic)        BOOL                                     showsNumberOfCopies NS_AVAILABLE_IOS(7_0); // default is YES.
 @property(nonatomic)        BOOL                                     showsPaperSelectionForLoadedPapers NS_AVAILABLE_IOS(8_0); // default is NO.  Paper selection for loaded papers is always shown for UIPrintInfoOutputPhoto and UIPrintInfoOutputPhotoGrayscale
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintPageRenderer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintPageRenderer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintPageRenderer.h	2015-10-03 01:47:14.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintPageRenderer.h	2016-06-03 05:02:46.000000000 +0200
@@ -2,7 +2,7 @@
 //  UIPrintPageRenderer.h
 //  UIKit
 //
-//  Copyright 2010-2012 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
@@ -21,11 +21,12 @@
 @property(nonatomic,readonly) CGRect paperRect;      // complete paper rect. origin is (0,0)
 @property(nonatomic,readonly) CGRect printableRect;  // imageable area inside paper rect
 
+@property(nonatomic,readonly) NSInteger numberOfPages;  // override point. page count. default is maximum page count needed for all formatters or 0
+
 @property(nullable,nonatomic,copy) NSArray<UIPrintFormatter *> *printFormatters;
 - (nullable NSArray<UIPrintFormatter *> *)printFormattersForPageAtIndex:(NSInteger)pageIndex;
 - (void)addPrintFormatter:(UIPrintFormatter *)formatter startingAtPageAtIndex:(NSInteger)pageIndex;
 
-- (NSInteger)numberOfPages;                        // override point. called to get page count. default returns maximum page count needed for all formatters or 0
 - (void)prepareForDrawingPages:(NSRange)range;     // override point. default does nothing. called before requesting a set of pages to draw
 
 - (void)drawPageAtIndex:(NSInteger)pageIndex inRect:(CGRect)printableRect;                         // override point. may be called from non-main thread.  calls the various draw methods below.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIRefreshControlHosting.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIRefreshControlHosting.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIRefreshControlHosting.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIRefreshControlHosting.h	2016-06-03 05:02:46.000000000 +0200
@@ -0,0 +1,17 @@
+//
+//  UIRefreshControlHosting.h
+//  UIKit
+//
+//  Copyright 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+@class UIRefreshControl;
+
+NS_CLASS_AVAILABLE_IOS(10_0) @protocol UIRefreshControlHosting <NSObject>
+
+@property (nonatomic, strong, nullable) UIRefreshControl *refreshControl __TVOS_PROHIBITED;
+
+@end
+
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIResponder.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIResponder.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIResponder.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIResponder.h	2016-06-03 06:16:40.000000000 +0200
@@ -34,8 +34,8 @@
 - (void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(nullable UIEvent *)event;
 - (void)touchesMoved:(NSSet<UITouch *> *)touches withEvent:(nullable UIEvent *)event;
 - (void)touchesEnded:(NSSet<UITouch *> *)touches withEvent:(nullable UIEvent *)event;
-- (void)touchesCancelled:(nullable NSSet<UITouch *> *)touches withEvent:(nullable UIEvent *)event;
-- (void)touchesEstimatedPropertiesUpdated:(NSSet * _Nonnull)touches NS_AVAILABLE_IOS(9_1);
+- (void)touchesCancelled:(NSSet<UITouch *> *)touches withEvent:(nullable UIEvent *)event;
+- (void)touchesEstimatedPropertiesUpdated:(NSSet<UITouch *> *)touches NS_AVAILABLE_IOS(9_1);
 
 // Generally, all responders which do custom press handling should override all four of these methods.
 // Your responder will receive either pressesEnded:withEvent or pressesCancelled:withEvent: for each
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScreen.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScreen.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScreen.h	2016-03-03 06:15:08.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScreen.h	2016-06-03 06:16:41.000000000 +0200
@@ -64,7 +64,8 @@
 
 - (nullable CADisplayLink *)displayLinkWithTarget:(id)target selector:(SEL)sel NS_AVAILABLE_IOS(4_0);
 
-@property (nullable, nonatomic, weak, readonly) UIView *focusedView NS_AVAILABLE_IOS(9_0);
+@property (nullable, nonatomic, weak, readonly) id<UIFocusItem> focusedItem NS_AVAILABLE_IOS(10_0);
+@property (nullable, nonatomic, weak, readonly) UIView *focusedView NS_AVAILABLE_IOS(9_0); // If focusedItem is not a view, this returns that item's containing view. Otherwise they are equal.
 @property (readonly, nonatomic) BOOL supportsFocus NS_AVAILABLE_IOS(9_0);
 
 @property(nonatomic,readonly) CGRect applicationFrame NS_DEPRECATED_IOS(2_0, 9_0, "Use -[UIScreen bounds]") __TVOS_PROHIBITED;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScrollView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScrollView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScrollView.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScrollView.h	2016-06-03 05:02:19.000000000 +0200
@@ -9,6 +9,7 @@
 #import <CoreGraphics/CoreGraphics.h>
 #import <UIKit/UIView.h>
 #import <UIKit/UIGeometry.h>
+#import <UIKit/UIRefreshControlHosting.h>
 #import <UIKit/UIKitDefines.h>
 
 NS_ASSUME_NONNULL_BEGIN
@@ -31,7 +32,7 @@
 @class UIEvent, UIImageView, UIPanGestureRecognizer, UIPinchGestureRecognizer;
 @protocol UIScrollViewDelegate;
 
-NS_CLASS_AVAILABLE_IOS(2_0) @interface UIScrollView : UIView <NSCoding>
+NS_CLASS_AVAILABLE_IOS(2_0) @interface UIScrollView : UIView <NSCoding, UIRefreshControlHosting>
 
 @property(nonatomic)         CGPoint                      contentOffset;                  // default CGPointZero
 @property(nonatomic)         CGSize                       contentSize;                    // default CGSizeZero
@@ -104,6 +105,8 @@
 
 // Use these accessors to configure the scroll view's built-in gesture recognizers.
 // Do not change the gestures' delegates or override the getters for these properties.
+
+// Change `panGestureRecognizer.allowedTouchTypes` to limit scrolling to a particular set of touch types.
 @property(nonatomic, readonly) UIPanGestureRecognizer *panGestureRecognizer NS_AVAILABLE_IOS(5_0);
 // `pinchGestureRecognizer` will return nil when zooming is disabled.
 @property(nullable, nonatomic, readonly) UIPinchGestureRecognizer *pinchGestureRecognizer NS_AVAILABLE_IOS(5_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchContainerViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchContainerViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchContainerViewController.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchContainerViewController.h	2016-06-03 05:02:46.000000000 +0200
@@ -5,7 +5,7 @@
 //  Copyright © 2015 Apple Inc. All rights reserved.
 //
 
-#import <UIKit/UIKit.h>
+#import <UIKit/UIViewController.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchController.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchController.h	2016-06-03 05:02:46.000000000 +0200
@@ -5,9 +5,9 @@
 //  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
 //
 
-#import <UIKit/UIKit.h>
 #import <UIKit/UIPresentationController.h>
 #import <UIKit/UIViewControllerTransitioning.h>
+#import <UIKit/UISearchBar.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchDisplayController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchDisplayController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchDisplayController.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISearchDisplayController.h	2016-06-03 05:02:19.000000000 +0200
@@ -10,6 +10,7 @@
 #import <UIKit/UIKitDefines.h>
 #import <UIKit/UILabel.h>
 #import <UIKit/UITableView.h>
+#import <UIKit/UINavigationBar.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISlider.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISlider.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISlider.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISlider.h	2016-06-03 05:02:46.000000000 +0200
@@ -9,7 +9,6 @@
 #import <CoreGraphics/CoreGraphics.h>
 #import <UIKit/UIControl.h>
 #import <UIKit/UIKitDefines.h>
-#import <QuartzCore/QuartzCore.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISplitViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISplitViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISplitViewController.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISplitViewController.h	2016-06-03 06:16:42.000000000 +0200
@@ -5,7 +5,7 @@
 //  Copyright (c) 2009-2015 Apple Inc. All rights reserved.
 //
 
-#import <UIKit/UIKit.h>
+#import <UIKit/UIViewController.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIStoryboardSegue.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIStoryboardSegue.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIStoryboardSegue.h	2015-10-03 01:47:14.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIStoryboardSegue.h	2016-06-03 05:02:46.000000000 +0200
@@ -31,7 +31,7 @@
 @end
 
 /// Encapsulates the source of a prospective unwind segue.
-/// You do not create instances of this class directly. Instead, UIKit creates an instance of this class and sends -destinationViewControllerForUnwindSource: to each ancestor of the sourceViewController until one returns a non-null result or the chain is exhausted.
+/// You do not create instances of this class directly. Instead, UIKit creates an instance of this class and sends -allowedChildViewControllersForUnwindingFromSource: to each ancestor of the sourceViewController until it finds a view controller which returns YES from -canPerformUnwindSegueAction:fromViewController:withSender:.
 NS_CLASS_AVAILABLE_IOS(9_0) @interface UIStoryboardUnwindSegueSource : NSObject
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBar.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBar.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBar.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBar.h	2016-06-03 05:02:46.000000000 +0200
@@ -23,9 +23,9 @@
 
 NS_CLASS_AVAILABLE_IOS(2_0) @interface UITabBar : UIView
 
-@property(nullable,nonatomic,assign) id<UITabBarDelegate> delegate;     // weak reference. default is nil
-@property(nullable,nonatomic,copy) NSArray<UITabBarItem *> *items;        // get/set visible UITabBarItems. default is nil. changes not animated. shown in order
-@property(nullable,nonatomic,assign) UITabBarItem *selectedItem; // will show feedback based on mode. default is nil
+@property(nullable, nonatomic, weak) id<UITabBarDelegate> delegate;     // weak reference. default is nil
+@property(nullable, nonatomic, copy) NSArray<UITabBarItem *> *items;        // get/set visible UITabBarItems. default is nil. changes not animated. shown in order
+@property(nullable, nonatomic, weak) UITabBarItem *selectedItem; // will show feedback based on mode. default is nil
 
 - (void)setItems:(nullable NSArray<UITabBarItem *> *)items animated:(BOOL)animated;   // will fade in or out or reorder and adjust spacing
 
@@ -40,8 +40,10 @@
  and behaves as described for the tintColor property added to UIView.
  To tint the bar's background, please use -barTintColor.
  */
-@property(null_resettable, nonatomic,strong) UIColor *tintColor NS_AVAILABLE_IOS(5_0);
-@property(nullable, nonatomic,strong) UIColor *barTintColor NS_AVAILABLE_IOS(7_0) UI_APPEARANCE_SELECTOR;  // default is nil
+@property(null_resettable, nonatomic, strong) UIColor *tintColor NS_AVAILABLE_IOS(5_0);
+@property(nullable, nonatomic, strong) UIColor *barTintColor NS_AVAILABLE_IOS(7_0) UI_APPEARANCE_SELECTOR;  // default is nil
+/// Unselected items in this tab bar will be tinted with this color. Setting this value to nil indicates that UITabBar should use its default value instead.
+@property (nonatomic, readwrite, copy, nullable) UIColor *unselectedItemTintColor NS_AVAILABLE_IOS(10_0) UI_APPEARANCE_SELECTOR;
 
 /* selectedImageTintColor will be applied to the gradient image used when creating the
  selected image. Default is nil and will result in the system bright blue for selected
@@ -51,19 +53,19 @@
  Deprecated in iOS 8.0. On iOS 7.0 and later the selected image takes its color from the
  inherited tintColor of the UITabBar, which may be set separately if necessary.
  */
-@property(nullable,nonatomic,strong) UIColor *selectedImageTintColor NS_DEPRECATED_IOS(5_0,8_0,"Use tintColor") UI_APPEARANCE_SELECTOR __TVOS_PROHIBITED;
+@property(nullable, nonatomic, strong) UIColor *selectedImageTintColor NS_DEPRECATED_IOS(5_0,8_0,"Use tintColor") UI_APPEARANCE_SELECTOR __TVOS_PROHIBITED;
 
 /* The background image will be tiled to fit, even if it was not created via the UIImage resizableImage methods.
  */
-@property(nullable, nonatomic,strong) UIImage *backgroundImage NS_AVAILABLE_IOS(5_0) UI_APPEARANCE_SELECTOR;
+@property(nullable, nonatomic, strong) UIImage *backgroundImage NS_AVAILABLE_IOS(5_0) UI_APPEARANCE_SELECTOR;
 
 /* The selection indicator image is drawn on top of the tab bar, behind the bar item icon.
  */
-@property(nullable, nonatomic,strong) UIImage *selectionIndicatorImage NS_AVAILABLE_IOS(5_0) UI_APPEARANCE_SELECTOR; 
+@property(nullable, nonatomic, strong) UIImage *selectionIndicatorImage NS_AVAILABLE_IOS(5_0) UI_APPEARANCE_SELECTOR;
 
 /* Default is nil. When non-nil, a custom shadow image to show instead of the default shadow image. For a custom shadow to be shown, a custom background image must also be set with -setBackgroundImage: (if the default background image is used, the default shadow image will be used).
  */
-@property(nullable, nonatomic,strong) UIImage *shadowImage NS_AVAILABLE_IOS(6_0) UI_APPEARANCE_SELECTOR;
+@property(nullable, nonatomic, strong) UIImage *shadowImage NS_AVAILABLE_IOS(6_0) UI_APPEARANCE_SELECTOR;
 
 /*
  Default is UITabBarItemPositioningAutomatic. The tab bar items fill horizontally
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBarController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBarController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBarController.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBarController.h	2016-06-03 06:16:41.000000000 +0200
@@ -11,6 +11,11 @@
 #import <UIKit/UIKitDefines.h>
 #import <UIKit/UITabBar.h>
 
+NS_ASSUME_NONNULL_BEGIN
+
+@class UIView, UIImage, UINavigationController, UITabBarItem;
+@protocol UITabBarControllerDelegate;
+
 /*!
  UITabBarController manages a button bar and transition view, for an application with multiple top-level modes.
  
@@ -23,11 +28,6 @@
  UITabBarController is rotatable if all of its view controllers are rotatable.
  */
 
-NS_ASSUME_NONNULL_BEGIN
-
-@class UIView, UIImage, UINavigationController, UITabBarItem;
-@protocol UITabBarControllerDelegate;
-
 NS_CLASS_AVAILABLE_IOS(2_0) @interface UITabBarController : UIViewController <UITabBarDelegate, NSCoding>
 
 @property(nullable, nonatomic,copy) NSArray<__kindof UIViewController *> *viewControllers;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBarItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBarItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBarItem.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBarItem.h	2016-06-03 05:02:46.000000000 +0200
@@ -57,6 +57,15 @@
  */
 @property (nonatomic, readwrite, assign) UIOffset titlePositionAdjustment NS_AVAILABLE_IOS(5_0) UI_APPEARANCE_SELECTOR;
 
+/// If this item displays a badge, this color will be used for the badge's background. If set to nil, the default background color will be used instead.
+@property (nonatomic, readwrite, copy, nullable) UIColor *badgeColor NS_AVAILABLE_IOS(10_0) UI_APPEARANCE_SELECTOR;
+
+/// Provide text attributes to use to draw the badge text for the given singular control state (Normal, Disabled, Focused, Selected, or Highlighted). Default values will be supplied for keys that are not provided by this dictionary. See NSAttributedString.h for details on what keys are available.
+- (void)setBadgeTextAttributes:(nullable NSDictionary<NSString *,id> *)textAttributes forState:(UIControlState)state NS_AVAILABLE_IOS(10_0) UI_APPEARANCE_SELECTOR;
+
+/// Returns attributes previously set via -setBadgeTextAttributes:forState:.
+- (nullable NSDictionary<NSString *,id> *)badgeTextAttributesForState:(UIControlState)state NS_AVAILABLE_IOS(10_0) UI_APPEARANCE_SELECTOR;
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableView.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableView.h	2016-06-03 05:02:19.000000000 +0200
@@ -48,6 +48,7 @@
 @class UITableView;
 @class UINib;
 @protocol UITableViewDataSource;
+@protocol UITableViewDataSourcePrefetching;
 @class UILongPressGestureRecognizer;
 @class UITableViewHeaderFooterView;
 @class UIRefreshControl;
@@ -181,6 +182,7 @@
 @property (nonatomic, readonly) UITableViewStyle style;
 @property (nonatomic, weak, nullable) id <UITableViewDataSource> dataSource;
 @property (nonatomic, weak, nullable) id <UITableViewDelegate> delegate;
+@property (nonatomic, weak) id<UITableViewDataSourcePrefetching> prefetchDataSource NS_AVAILABLE_IOS(10_0);
 @property (nonatomic) CGFloat rowHeight;             // will return the default value if unset
 @property (nonatomic) CGFloat sectionHeaderHeight;   // will return the default value if unset
 @property (nonatomic) CGFloat sectionFooterHeight;   // will return the default value if unset
@@ -337,6 +339,25 @@
 
 @end
 
+
+// _______________________________________________________________________________________________________________
+// this protocol can provide information about cells before they are displayed on screen.
+
+@protocol UITableViewDataSourcePrefetching <NSObject>
+
+@required
+
+// indexPaths are ordered ascending by geometric distance from the table view
+- (void)tableView:(UITableView *)tableView prefetchRowsAtIndexPaths:(NSArray<NSIndexPath *> *)indexPaths;
+
+@optional
+
+// indexPaths that previously were considered as candidates for pre-fetching, but were not actually used; may be a subset of the previous call to -tableView:prefetchRowsAtIndexPaths:
+- (void)tableView:(UITableView *)tableView cancelPrefetchingForRowsAtIndexPaths:(NSArray<NSIndexPath *> *)indexPaths;
+
+@end
+
+
 //_______________________________________________________________________________________________________________
 
 // This category provides convenience methods to make it easier to use an NSIndexPath to represent a section and row
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableViewController.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableViewController.h	2016-06-03 05:02:46.000000000 +0200
@@ -7,6 +7,7 @@
 #import <Foundation/Foundation.h>
 #import <UIKit/UIViewController.h>
 #import <UIKit/UITableView.h>
+#import <UIKit/UIRefreshControlHosting.h>
 #import <UIKit/UIKitDefines.h>
 
 // Creates a table view with the correct dimensions and autoresizing, setting the datasource and delegate to self.
@@ -16,7 +17,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE_IOS(2_0) @interface UITableViewController : UIViewController <UITableViewDelegate, UITableViewDataSource>
+NS_CLASS_AVAILABLE_IOS(2_0) @interface UITableViewController : UIViewController <UITableViewDelegate, UITableViewDataSource, UIRefreshControlHosting>
 
 - (instancetype)initWithStyle:(UITableViewStyle)style NS_DESIGNATED_INITIALIZER;
 - (instancetype)initWithNibName:(nullable NSString *)nibNameOrNil bundle:(nullable NSBundle *)nibBundleOrNil NS_DESIGNATED_INITIALIZER;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextChecker.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextChecker.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextChecker.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextChecker.h	2016-06-03 05:02:46.000000000 +0200
@@ -19,15 +19,15 @@
 - (NSRange)rangeOfMisspelledWordInString:(NSString *)stringToCheck range:(NSRange)range startingAt:(NSInteger)startingOffset wrap:(BOOL)wrapFlag language:(NSString *)language;
 
 /* Returns an array of strings, in the order in which they should be presented, representing guesses for words that might have been intended in place of the misspelled word at the given range in the given string. */
-- (nullable NSArray *)guessesForWordRange:(NSRange)range inString:(NSString *)string language:(NSString *)language;
+- (nullable NSArray<NSString *> *)guessesForWordRange:(NSRange)range inString:(NSString *)string language:(NSString *)language;
 
 /* Returns an array of strings, in the order in which they should be presented, representing complete words that the user might be trying to type when starting by typing the partial word at the given range in the given string. */
-- (nullable NSArray *)completionsForPartialWordRange:(NSRange)range inString:(nullable NSString *)string language:(NSString *)language;
+- (nullable NSArray<NSString *> *)completionsForPartialWordRange:(NSRange)range inString:(NSString *)string language:(NSString *)language;
 
 /* Methods for dealing with ignored words. */
 - (void)ignoreWord:(NSString *)wordToIgnore;
-- (nullable NSArray *)ignoredWords;
-- (void)setIgnoredWords:(nullable NSArray *)words;
+- (nullable NSArray<NSString *> *)ignoredWords;
+- (void)setIgnoredWords:(nullable NSArray<NSString *> *)words;
 
 /* These allow clients to programmatically instruct the checker to learn and unlearn words, and to determine whether a word has been learned (and hence can potentially be unlearned). */
 + (void)learnWord:(NSString *)word;
@@ -35,7 +35,7 @@
 + (void)unlearnWord:(NSString *)word;
 
 /* Entries in the availableLanguages list are all available spellchecking languages in user preference order, usually language abbreviations such as en_US. */
-+ (NSArray *)availableLanguages;
++ (NSArray<NSString *> *)availableLanguages;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextField.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextField.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextField.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextField.h	2016-06-03 06:16:41.000000000 +0200
@@ -12,6 +12,7 @@
 #import <UIKit/UIFont.h>
 #import <UIKit/UIStringDrawing.h>
 #import <UIKit/UITextInput.h>
+#import <UIKit/UIContentSizeCategoryAdjusting.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -41,7 +42,7 @@
     UITextFieldViewModeAlways
 };
 
-NS_CLASS_AVAILABLE_IOS(2_0) @interface UITextField : UIControl <UITextInput, NSCoding> 
+NS_CLASS_AVAILABLE_IOS(2_0) @interface UITextField : UIControl <UITextInput, NSCoding, UIContentSizeCategoryAdjusting>
 
 @property(nullable, nonatomic,copy)   NSString               *text;                 // default is nil
 @property(nullable, nonatomic,copy)   NSAttributedString     *attributedText NS_AVAILABLE_IOS(6_0); // default is nil
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInput.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInput.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInput.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInput.h	2016-06-03 05:02:46.000000000 +0200
@@ -278,8 +278,8 @@
 @property (nullable, nonatomic, readonly, strong) NSString *primaryLanguage; // The primary language, if any, of the input mode.  A BCP 47 language identifier such as en-US
 
 // To query the UITextInputMode, refer to the UIResponder method -textInputMode.
-+ (nullable UITextInputMode *)currentInputMode NS_DEPRECATED_IOS(4_2, 7_0)  __TVOS_PROHIBITED;; // The current input mode.  Nil if unset.
-+ (NSArray<NSString *> *)activeInputModes; // The activate input modes.
++ (nullable UITextInputMode *)currentInputMode NS_DEPRECATED_IOS(4_2, 7_0)  __TVOS_PROHIBITED; // The current input mode.  Nil if unset.
++ (NSArray<UITextInputMode *> *)activeInputModes; // The active input modes.
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInputTraits.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInputTraits.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInputTraits.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInputTraits.h	2016-06-03 06:16:41.000000000 +0200
@@ -59,16 +59,17 @@
 //
 typedef NS_ENUM(NSInteger, UIKeyboardType) {
     UIKeyboardTypeDefault,                // Default type for the current input method.
-    UIKeyboardTypeASCIICapable,           // Displays a keyboard which can enter ASCII characters, non-ASCII keyboards remain active
+    UIKeyboardTypeASCIICapable,           // Displays a keyboard which can enter ASCII characters
     UIKeyboardTypeNumbersAndPunctuation,  // Numbers and assorted punctuation.
     UIKeyboardTypeURL,                    // A type optimized for URL entry (shows . / .com prominently).
-    UIKeyboardTypeNumberPad,              // A number pad (0-9). Suitable for PIN entry.
+    UIKeyboardTypeNumberPad,              // A number pad with locale-appropriate digits (0-9, ۰-۹, ०-९, etc.). Suitable for PIN entry.
     UIKeyboardTypePhonePad,               // A phone pad (1-9, *, 0, #, with letters under the numbers).
     UIKeyboardTypeNamePhonePad,           // A type optimized for entering a person's name or phone number.
     UIKeyboardTypeEmailAddress,           // A type optimized for multiple email address entry (shows space @ . prominently).
     UIKeyboardTypeDecimalPad NS_ENUM_AVAILABLE_IOS(4_1),   // A number pad with a decimal point.
     UIKeyboardTypeTwitter NS_ENUM_AVAILABLE_IOS(5_0),      // A type optimized for twitter text entry (easy access to @ #)
     UIKeyboardTypeWebSearch NS_ENUM_AVAILABLE_IOS(7_0),    // A default keyboard type with URL-oriented addition (shows space . prominently).
+    UIKeyboardTypeASCIICapableNumberPad NS_ENUM_AVAILABLE_IOS(10_0), // A number pad (0-9) that will always be ASCII digits.
 
     UIKeyboardTypeAlphabet = UIKeyboardTypeASCIICapable, // Deprecated
 
@@ -132,5 +133,32 @@
 @property(nonatomic) BOOL enablesReturnKeyAutomatically;                  // default is NO (when YES, will automatically disable return key when text widget has zero-length contents, and will automatically enable when text widget has non-zero-length contents)
 @property(nonatomic,getter=isSecureTextEntry) BOOL secureTextEntry;       // default is NO
 
+// The textContentType property is to provide the keyboard with extra information about the semantic intent of the text document.
+@property(nonatomic,copy) NSString *textContentType NS_AVAILABLE_IOS(10_0); // default is nil
+
 @end
 
+UIKIT_EXTERN NSString *const UITextContentTypeName                      NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeNamePrefix                NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeGivenName                 NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeMiddleName                NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeFamilyName                NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeNameSuffix                NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeNickname                  NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeJobTitle                  NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeOrganizationName          NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeLocation                  NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeFullStreetAddress         NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeStreetAddressLine1        NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeStreetAddressLine2        NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeAddressCity               NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeAddressState              NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeAddressCityAndState       NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeSublocality               NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeCountryName               NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypePostalCode                NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeTelephoneNumber           NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeEmailAddress              NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeURL                       NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN NSString *const UITextContentTypeCreditCardNumber          NS_AVAILABLE_IOS(10_0);
+
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInteraction.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInteraction.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInteraction.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInteraction.h	2016-06-03 05:02:46.000000000 +0200
@@ -0,0 +1,12 @@
+//
+//  UITextInteraction.h
+//  UIKit
+//
+//  Copyright (c) 2016-2016 Apple Inc. All rights reserved.
+//
+
+typedef NS_ENUM(NSInteger, UITextItemInteraction) {
+    UITextItemInteractionInvokeDefaultAction,
+    UITextItemInteractionPresentActions,
+    UITextItemInteractionPreview,
+} NS_ENUM_AVAILABLE_IOS(10_0);
\ No newline at end of file
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextView.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextView.h	2016-06-03 06:16:40.000000000 +0200
@@ -12,6 +12,8 @@
 #import <UIKit/UITextInput.h>
 #import <UIKit/UIKitDefines.h>
 #import <UIKit/UIDataDetectors.h>
+#import <UIKit/UITextInteraction.h>
+#import <UIKit/UIContentSizeCategoryAdjusting.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -32,12 +34,15 @@
 
 - (void)textViewDidChangeSelection:(UITextView *)textView;
 
-- (BOOL)textView:(UITextView *)textView shouldInteractWithURL:(NSURL *)URL inRange:(NSRange)characterRange NS_AVAILABLE_IOS(7_0);
-- (BOOL)textView:(UITextView *)textView shouldInteractWithTextAttachment:(NSTextAttachment *)textAttachment inRange:(NSRange)characterRange NS_AVAILABLE_IOS(7_0);
+- (BOOL)textView:(UITextView *)textView shouldInteractWithURL:(NSURL *)URL inRange:(NSRange)characterRange interaction:(UITextItemInteraction)interaction NS_AVAILABLE_IOS(10_0);
+- (BOOL)textView:(UITextView *)textView shouldInteractWithTextAttachment:(NSTextAttachment *)textAttachment inRange:(NSRange)characterRange interaction:(UITextItemInteraction)interaction NS_AVAILABLE_IOS(10_0);
+
+- (BOOL)textView:(UITextView *)textView shouldInteractWithURL:(NSURL *)URL inRange:(NSRange)characterRange NS_DEPRECATED_IOS(7_0, 10_0, "Use textView:shouldInteractWithURL:inRange:forInteractionType: instead");
+- (BOOL)textView:(UITextView *)textView shouldInteractWithTextAttachment:(NSTextAttachment *)textAttachment inRange:(NSRange)characterRange NS_DEPRECATED_IOS(7_0, 10_0, "Use textView:shouldInteractWithTextAttachment:inRange:forInteractionType: instead");
 
 @end
 
-NS_CLASS_AVAILABLE_IOS(2_0) @interface UITextView : UIScrollView <UITextInput>
+NS_CLASS_AVAILABLE_IOS(2_0) @interface UITextView : UIScrollView <UITextInput, UIContentSizeCategoryAdjusting>
 
 @property(nullable,nonatomic,weak) id<UITextViewDelegate> delegate;
 @property(null_resettable,nonatomic,copy) NSString *text;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITimingCurveProvider.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITimingCurveProvider.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITimingCurveProvider.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITimingCurveProvider.h	2016-06-03 05:02:46.000000000 +0200
@@ -0,0 +1,29 @@
+//
+//  UITimingCurveProvider.h
+//  UIKit
+//
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+typedef NS_ENUM(NSInteger, UITimingCurveType) {
+    UITimingCurveTypeBuiltin,
+    UITimingCurveTypeCubic,
+    UITimingCurveTypeSpring,
+    UITimingCurveTypeComposed,        
+} NS_ENUM_AVAILABLE_IOS(10_0);
+
+@class UICubicTimingParameters, UISpringTimingParameters;
+
+NS_ASSUME_NONNULL_BEGIN
+
+@protocol UITimingCurveProvider <NSCoding, NSCopying>
+
+@property(nonatomic, readonly) UITimingCurveType timingCurveType;
+@property(nullable, nonatomic, readonly) UICubicTimingParameters *cubicTimingParameters;
+@property(nullable, nonatomic, readonly) UISpringTimingParameters *springTimingParameters;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITimingParameters.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITimingParameters.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITimingParameters.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITimingParameters.h	2016-06-03 05:02:46.000000000 +0200
@@ -0,0 +1,60 @@
+//
+//  UITimingParameters.h
+//  UIKit
+//
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <UIKit/UITimingCurveProvider.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+NS_CLASS_AVAILABLE_IOS(10_0) @interface UICubicTimingParameters : NSObject  <UITimingCurveProvider>
+
+@property(nonatomic, readonly) UIViewAnimationCurve animationCurve;
+@property(nonatomic, readonly) CGPoint controlPoint1;
+@property(nonatomic, readonly) CGPoint controlPoint2;
+
+- (instancetype)init NS_DESIGNATED_INITIALIZER; // initializes with the default CA timing curve
+- (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithAnimationCurve:(UIViewAnimationCurve)curve NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithControlPoint1:(CGPoint)point1 controlPoint2:(CGPoint)point2 NS_DESIGNATED_INITIALIZER;
+
+@end
+
+
+NS_CLASS_AVAILABLE_IOS(10_0) @interface UISpringTimingParameters : NSObject  <UITimingCurveProvider>
+
+@property(nonatomic, readonly) CGVector initialVelocity;
+
+- (instancetype)init NS_DESIGNATED_INITIALIZER; // Initializes with the default system spring parameters
+
+- (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
+
+// Performs `animations` using a timing curve described by the motion of a
+// spring. When `dampingRatio` is 1, the animation will smoothly decelerate to
+// its final model values without oscillating. Damping ratios less than 1 will
+// oscillate more and more before coming to a complete stop. You can use the
+// initial spring velocity to specify how fast the object at the end of the
+// simulated spring was moving before it was attached. It's a unit coordinate
+// system, where 1 is defined as travelling the total animation distance in a
+// second. So if you're changing an object's position by 200pt in this
+// animation, and you want the animation to behave as if the object was moving
+// at 100pt/s before the animation started, you'd pass 0.5. You'll typically
+// want to pass 0 for the velocity. Velocity is specified as a vector for the
+// convenience of animating position changes. For 1-dimensional properties
+// the x-coordinate of the velocity vector is used.
+- (instancetype)initWithDampingRatio:(CGFloat)ratio initialVelocity:(CGVector)velocity NS_DESIGNATED_INITIALIZER;
+
+// Similiar to initWithDampingRatio:initialVelocity: except this allows you to specify the spring constants for the underlying
+// CASpringAnimation directly. The duration is computed assuming a small settling oscillation.
+- (instancetype)initWithMass:(CGFloat)mass stiffness:(CGFloat)stiffness damping:(CGFloat)damping initialVelocity:(CGVector)velocity NS_DESIGNATED_INITIALIZER;
+
+// Equivalent to initWithDampingRatio:initialVelocity: where the velocity is the zero-vector.
+- (instancetype)initWithDampingRatio:(CGFloat)ratio;
+
+@end
+
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIToolbar.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIToolbar.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIToolbar.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIToolbar.h	2016-06-03 05:02:46.000000000 +0200
@@ -20,8 +20,8 @@
 
 NS_CLASS_AVAILABLE_IOS(2_0) __TVOS_PROHIBITED @interface UIToolbar : UIView <UIBarPositioning>
 
-@property(nonatomic) UIBarStyle barStyle __TVOS_PROHIBITED; // default is UIBarStyleDefault (blue)
-@property(nullable,nonatomic,copy) NSArray<UIBarButtonItem *> *items; // get/set visible UIBarButtonItem. default is nil. changes not animated. shown in order
+@property(nonatomic) UIBarStyle barStyle UI_APPEARANCE_SELECTOR __TVOS_PROHIBITED; // default is UIBarStyleDefault (blue)
+@property(nullable, nonatomic, copy) NSArray<UIBarButtonItem *> *items; // get/set visible UIBarButtonItem. default is nil. changes not animated. shown in order
 
 /*
  New behavior on iOS 7.
@@ -44,8 +44,8 @@
  and behaves as described for the tintColor property added to UIView.
  To tint the bar's background, please use -barTintColor.
  */
-@property(null_resettable, nonatomic,strong) UIColor *tintColor;
-@property(nullable, nonatomic,strong) UIColor *barTintColor NS_AVAILABLE_IOS(7_0) UI_APPEARANCE_SELECTOR;  // default is nil
+@property(null_resettable, nonatomic, strong) UIColor *tintColor;
+@property(nullable, nonatomic, strong) UIColor *barTintColor NS_AVAILABLE_IOS(7_0) UI_APPEARANCE_SELECTOR;  // default is nil
 
 /* Use these methods to set and access custom background images for toolbars.
       Default is nil. When non-nil the image will be used instead of the system image for toolbars in the
@@ -65,7 +65,7 @@
 - (void)setShadowImage:(nullable UIImage *)shadowImage forToolbarPosition:(UIBarPosition)topOrBottom NS_AVAILABLE_IOS(6_0) UI_APPEARANCE_SELECTOR;
 - (nullable UIImage *)shadowImageForToolbarPosition:(UIBarPosition)topOrBottom NS_AVAILABLE_IOS(6_0) UI_APPEARANCE_SELECTOR;
 
-@property(nullable, nonatomic,assign) id<UIToolbarDelegate> delegate NS_AVAILABLE_IOS(7_0); // You may not set the delegate when the toolbar is managed by a UINavigationController.
+@property(nullable, nonatomic, weak) id<UIToolbarDelegate> delegate NS_AVAILABLE_IOS(7_0); // You may not set the delegate when the toolbar is managed by a UINavigationController.
 @end
 
 __TVOS_PROHIBITED
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITraitCollection.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITraitCollection.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITraitCollection.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITraitCollection.h	2016-06-03 05:02:46.000000000 +0200
@@ -30,6 +30,12 @@
 + (UITraitCollection *)traitCollectionWithUserInterfaceIdiom:(UIUserInterfaceIdiom)idiom;
 @property (nonatomic, readonly) UIUserInterfaceIdiom userInterfaceIdiom; // unspecified: UIUserInterfaceIdiomUnspecified
 
++ (UITraitCollection *)traitCollectionWithUserInterfaceStyle:(UIUserInterfaceStyle)userInterfaceStyle __TVOS_AVAILABLE(10_0) __WATCHOS_PROHIBITED __IOS_PROHIBITED;
+@property (nonatomic, readonly) UIUserInterfaceStyle userInterfaceStyle __TVOS_AVAILABLE(10_0) __WATCHOS_PROHIBITED __IOS_PROHIBITED; // unspecified: UIUserInterfaceStyleUnspecified
+
++ (UITraitCollection *)traitCollectionWithLayoutDirection:(UITraitEnvironmentLayoutDirection)layoutDirection;
+@property (nonatomic, readonly) UITraitEnvironmentLayoutDirection layoutDirection; // unspecified: UITraitEnvironmentLayoutDirectionUnspecified
+
 + (UITraitCollection *)traitCollectionWithDisplayScale:(CGFloat)scale;
 @property (nonatomic, readonly) CGFloat displayScale; // unspecified: 0.0
 
@@ -42,6 +48,12 @@
 + (UITraitCollection *)traitCollectionWithForceTouchCapability:(UIForceTouchCapability)capability NS_AVAILABLE_IOS(9_0);
 @property (nonatomic, readonly) UIForceTouchCapability forceTouchCapability NS_AVAILABLE_IOS(9_0); // unspecified: UIForceTouchCapabilityUnknown
 
++ (UITraitCollection *)traitCollectionWithPreferredContentSizeCategory:(NSString *)preferredContentSizeCategory NS_AVAILABLE_IOS(10_0);
+@property (nonatomic, copy, readonly) NSString *preferredContentSizeCategory NS_AVAILABLE_IOS(10_0); // unspecified: UIContentSizeCategoryUnspecified
+
++ (UITraitCollection *)traitCollectionWithDisplayGamut:(UIDisplayGamut)displayGamut NS_AVAILABLE_IOS(10_0);
+@property (nonatomic, readonly) UIDisplayGamut displayGamut NS_AVAILABLE_IOS(10_0); // unspecified: UIDisplayGamutUnspecified
+
 @end
 
 /*! Trait environments expose a trait collection that describes their environment. */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIUserNotificationSettings.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIUserNotificationSettings.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIUserNotificationSettings.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIUserNotificationSettings.h	2016-06-03 05:02:46.000000000 +0200
@@ -18,28 +18,28 @@
     UIUserNotificationTypeBadge   = 1 << 0, // the application may badge its icon upon a notification being received
     UIUserNotificationTypeSound   = 1 << 1, // the application may play a sound upon a notification being received
     UIUserNotificationTypeAlert   = 1 << 2, // the application may display an alert upon a notification being received
-} NS_ENUM_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED;
+} NS_ENUM_DEPRECATED_IOS(8_0, 10_0, "Use UserNotifications Framework's UNAuthorizationOptions") __TVOS_PROHIBITED;
 
 typedef NS_ENUM(NSUInteger, UIUserNotificationActionBehavior) {
     UIUserNotificationActionBehaviorDefault,        // the default action behavior
     UIUserNotificationActionBehaviorTextInput       // system provided action behavior, allows text input from the user
-} NS_ENUM_AVAILABLE_IOS(9_0) __TVOS_PROHIBITED;
+} NS_ENUM_DEPRECATED_IOS(9_0, 10_0, "Use UserNotifications Framework's UNNotificationAction or UNTextInputNotificationAction") __TVOS_PROHIBITED;
 
 typedef NS_ENUM(NSUInteger, UIUserNotificationActivationMode) {
     UIUserNotificationActivationModeForeground, // activates the application in the foreground
     UIUserNotificationActivationModeBackground  // activates the application in the background, unless it's already in the foreground
-} NS_ENUM_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED;
+} NS_ENUM_DEPRECATED_IOS(8_0, 10_0, "Use UserNotifications Framework's UNNotificationActionOptions") __TVOS_PROHIBITED;
 
 typedef NS_ENUM(NSUInteger, UIUserNotificationActionContext) {
     UIUserNotificationActionContextDefault,  // the default context of a notification action
     UIUserNotificationActionContextMinimal   // the context of a notification action when space is limited
-} NS_ENUM_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED;
+} NS_ENUM_DEPRECATED_IOS(8_0, 10_0, "Use UserNotifications Framework's -[UNNotificationCategory actions] or -[UNNotificationCategory minimalActions]") __TVOS_PROHIBITED;
 
-UIKIT_EXTERN NSString *const UIUserNotificationTextInputActionButtonTitleKey NS_AVAILABLE_IOS(9_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN NSString *const UIUserNotificationTextInputActionButtonTitleKey NS_DEPRECATED_IOS(9_0, 10_0, "Use UserNotifications Framework's -[UNTextInputNotificationAction textInputButtonTitle]") __TVOS_PROHIBITED;
 
-UIKIT_EXTERN NSString *const UIUserNotificationActionResponseTypedTextKey NS_AVAILABLE_IOS(9_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN NSString *const UIUserNotificationActionResponseTypedTextKey NS_DEPRECATED_IOS(9_0, 10_0, "Use UserNotifications Framework's -[UNTextInputNotificationResponse userText]") __TVOS_PROHIBITED;
 
-NS_CLASS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED
+NS_CLASS_DEPRECATED_IOS(8_0, 10_0, "Use UserNotifications Framework's UNNotificationSettings") __TVOS_PROHIBITED
 @interface UIUserNotificationSettings : NSObject
 
 // categories may be nil or an empty set if custom user notification actions will not be used
@@ -53,21 +53,21 @@
 
 @end
 
-NS_CLASS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED
+NS_CLASS_DEPRECATED_IOS(8_0, 10_0, "Use UserNotifications Framework's UNNotificationCategory") __TVOS_PROHIBITED
 @interface UIUserNotificationCategory : NSObject <NSCopying, NSMutableCopying, NSSecureCoding>
 
 - (instancetype)init NS_DESIGNATED_INITIALIZER __TVOS_PROHIBITED;
 - (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER __TVOS_PROHIBITED;
 
 // The category identifier passed in a UILocalNotification or a remote notification payload
-@property (nullable,nonatomic, copy, readonly) NSString *identifier __TVOS_PROHIBITED;
+@property (nullable, nonatomic, copy, readonly) NSString *identifier __TVOS_PROHIBITED;
 
 // UIUserNotificationActions in the order to be displayed for the specified context
 - (nullable NSArray<UIUserNotificationAction *> *)actionsForContext:(UIUserNotificationActionContext)context __TVOS_PROHIBITED;
 
 @end
 
-NS_CLASS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED
+NS_CLASS_DEPRECATED_IOS(8_0, 10_0, "Use UserNotifications Framework's UNNotificationCategory") __TVOS_PROHIBITED
 @interface UIMutableUserNotificationCategory : UIUserNotificationCategory
 
 // The category identifier passed in a UILocalNotification or a remote notification payload
@@ -78,7 +78,7 @@
 
 @end
 
-NS_CLASS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED
+NS_CLASS_DEPRECATED_IOS(8_0, 10_0, "Use UserNotifications Framework's UNNotificationAction") __TVOS_PROHIBITED
 @interface UIUserNotificationAction : NSObject <NSCopying, NSMutableCopying, NSSecureCoding>
 
 - (instancetype)init NS_DESIGNATED_INITIALIZER __TVOS_PROHIBITED;
@@ -107,7 +107,7 @@
 
 @end
 
-NS_CLASS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED
+NS_CLASS_DEPRECATED_IOS(8_0, 10_0, "Use UserNotifications Framework's UNNotificationAction") __TVOS_PROHIBITED
 @interface UIMutableUserNotificationAction : UIUserNotificationAction
 
 // The unique identifier for this action.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIView.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIView.h	2016-06-03 05:02:19.000000000 +0200
@@ -6,6 +6,7 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <QuartzCore/QuartzCore.h>
 #import <UIKit/UIResponder.h>
 #import <UIKit/UIInterface.h>
 #import <UIKit/UIKitDefines.h>
@@ -21,7 +22,7 @@
     UIViewAnimationCurveEaseInOut,         // slow at beginning and end
     UIViewAnimationCurveEaseIn,            // slow at beginning
     UIViewAnimationCurveEaseOut,           // slow at end
-    UIViewAnimationCurveLinear
+    UIViewAnimationCurveLinear,
 };
 
 typedef NS_ENUM(NSInteger, UIViewContentMode) {
@@ -120,11 +121,6 @@
     UISemanticContentAttributeForceRightToLeft
 } NS_ENUM_AVAILABLE_IOS(9_0);
 
-typedef NS_ENUM(NSInteger, UIUserInterfaceLayoutDirection) {
-    UIUserInterfaceLayoutDirectionLeftToRight,
-    UIUserInterfaceLayoutDirectionRightToLeft,
-} NS_ENUM_AVAILABLE_IOS(5_0);
-
 @protocol UICoordinateSpace <NSObject>
 
 - (CGPoint)convertPoint:(CGPoint)point toCoordinateSpace:(id <UICoordinateSpace>)coordinateSpace NS_AVAILABLE_IOS(8_0);
@@ -138,7 +134,7 @@
 
 @class UIBezierPath, UIEvent, UIWindow, UIViewController, UIColor, UIGestureRecognizer, UIMotionEffect, CALayer, UILayoutGuide;
 
-NS_CLASS_AVAILABLE_IOS(2_0) @interface UIView : UIResponder <NSCoding, UIAppearance, UIAppearanceContainer, UIDynamicItem, UITraitEnvironment, UICoordinateSpace, UIFocusEnvironment>
+NS_CLASS_AVAILABLE_IOS(2_0) @interface UIView : UIResponder <NSCoding, UIAppearance, UIAppearanceContainer, UIDynamicItem, UITraitEnvironment, UICoordinateSpace, UIFocusItem, CALayerDelegate>
 
 + (Class)layerClass;                        // default is [CALayer class]. Used when creating the underlying layer for the view.
 
@@ -152,8 +148,17 @@
 - (BOOL)canBecomeFocused NS_AVAILABLE_IOS(9_0); // NO by default
 @property (readonly, nonatomic, getter=isFocused) BOOL focused NS_AVAILABLE_IOS(9_0);
 
-+ (UIUserInterfaceLayoutDirection)userInterfaceLayoutDirectionForSemanticContentAttribute:(UISemanticContentAttribute)attribute NS_AVAILABLE_IOS(9_0);
 @property (nonatomic) UISemanticContentAttribute semanticContentAttribute NS_AVAILABLE_IOS(9_0);
+
+// This method returns the layout direction implied by the provided semantic content attribute relative to the application-wide layout direction (as returned by UIApplication.sharedApplication.userInterfaceLayoutDirection).
++ (UIUserInterfaceLayoutDirection)userInterfaceLayoutDirectionForSemanticContentAttribute:(UISemanticContentAttribute)attribute NS_AVAILABLE_IOS(9_0);
+
+// This method returns the layout direction implied by the provided semantic content attribute relative to the provided layout direction. For example, when provided a layout direction of RightToLeft and a semantic content attribute of Playback, this method returns LeftToRight. Layout and drawing code can use this method to determine how to arrange elements, but might find it easier to query the container view’s effectiveUserInterfaceLayoutDirection property instead.
++ (UIUserInterfaceLayoutDirection)userInterfaceLayoutDirectionForSemanticContentAttribute:(UISemanticContentAttribute)semanticContentAttribute relativeToLayoutDirection:(UIUserInterfaceLayoutDirection)layoutDirection NS_AVAILABLE_IOS(10_0);
+
+// Returns the user interface layout direction appropriate for arranging the immediate content of this view. Always consult the effectiveUserInterfaceLayoutDirection of the view whose immediate content is being arranged or drawn. Do not assume that the value propagates through the view’s subtree.
+@property (readonly, nonatomic) UIUserInterfaceLayoutDirection effectiveUserInterfaceLayoutDirection NS_AVAILABLE_IOS(10_0);
+
 @end
 
 @interface UIView(UIViewGeometry)
@@ -299,7 +304,7 @@
 
 + (void)setAnimationsEnabled:(BOOL)enabled;                         // ignore any attribute changes while set.
 + (BOOL)areAnimationsEnabled;
-+ (void)performWithoutAnimation:(void (^)(void))actionsWithoutAnimation NS_AVAILABLE_IOS(7_0);
++ (void)performWithoutAnimation:(void (NS_NOESCAPE ^)(void))actionsWithoutAnimation NS_AVAILABLE_IOS(7_0);
 
 + (NSTimeInterval)inheritedAnimationDuration NS_AVAILABLE_IOS(9_0);
 
@@ -402,7 +407,7 @@
 
 @interface UIView (UIConstraintBasedLayoutCoreMethods) 
 - (void)updateConstraintsIfNeeded NS_AVAILABLE_IOS(6_0); // Updates the constraints from the bottom up for the view hierarchy rooted at the receiver. UIWindow's implementation creates a layout engine if necessary first.
-- (void)updateConstraints NS_AVAILABLE_IOS(6_0); // Override this to adjust your special constraints during a constraints update pass
+- (void)updateConstraints NS_AVAILABLE_IOS(6_0) NS_REQUIRES_SUPER; // Override this to adjust your special constraints during a constraints update pass
 - (BOOL)needsUpdateConstraints NS_AVAILABLE_IOS(6_0);
 - (void)setNeedsUpdateConstraints NS_AVAILABLE_IOS(6_0);
 @end
@@ -560,6 +565,22 @@
 - (void)exerciseAmbiguityInLayout NS_AVAILABLE_IOS(6_0); 
 @end
 
+/* Everything in this section should be used in debugging only, never in shipping code.  These methods may not exist in the future - no promises.
+ */
+@interface UILayoutGuide (UIConstraintBasedLayoutDebugging)
+
+/* This returns a list of all the constraints that are affecting the current location of the receiver.  The constraints do not necessarily involve the receiver, they may affect the frame indirectly.
+ Pass UILayoutConstraintAxisHorizontal for the constraints affecting [self center].x and CGRectGetWidth([self bounds]), and UILayoutConstraintAxisVertical for the constraints affecting[self center].y and CGRectGetHeight([self bounds]).
+ */
+- (NSArray<__kindof NSLayoutConstraint *> *)constraintsAffectingLayoutForAxis:(UILayoutConstraintAxis)axis NS_AVAILABLE_IOS(10_0);
+
+/* If there aren't enough constraints in the system to uniquely determine layout, we say the layout is ambiguous.  For example, if the only constraint in the system was x = y + 100, then there are lots of different possible values for x and y.  This situation is not automatically detected by UIKit, due to performance considerations and details of the algorithm used for layout.
+ The symptom of ambiguity is that views sometimes jump from place to place, or possibly are just in the wrong place.
+ -hasAmbiguousLayout runs a check for whether there is another center and bounds the receiver could have that could also satisfy the constraints.
+ */
+- (BOOL)hasAmbiguousLayout NS_AVAILABLE_IOS(10_0);
+@end
+
 @interface UIView (UIStateRestoration)
 @property (nullable, nonatomic, copy) NSString *restorationIdentifier NS_AVAILABLE_IOS(6_0);
 - (void) encodeRestorableStateWithCoder:(NSCoder *)coder NS_AVAILABLE_IOS(6_0);
@@ -581,8 +602,8 @@
 
 * Creating snapshots from existing snapshots (as a method to duplicate, crop or create a resizable variant) is supported. In cases where many snapshots are needed, creating a snapshot from a common superview and making subsequent snapshots from it can be more performant. Please keep in mind that if 'afterUpdates' is YES, the original snapshot is committed and any changes made to it, not the view originally snapshotted, will be included.
  */
-- (UIView *)snapshotViewAfterScreenUpdates:(BOOL)afterUpdates NS_AVAILABLE_IOS(7_0);
-- (UIView *)resizableSnapshotViewFromRect:(CGRect)rect afterScreenUpdates:(BOOL)afterUpdates withCapInsets:(UIEdgeInsets)capInsets NS_AVAILABLE_IOS(7_0);  // Resizable snapshots will default to stretching the center
+- (nullable UIView *)snapshotViewAfterScreenUpdates:(BOOL)afterUpdates NS_AVAILABLE_IOS(7_0);
+- (nullable UIView *)resizableSnapshotViewFromRect:(CGRect)rect afterScreenUpdates:(BOOL)afterUpdates withCapInsets:(UIEdgeInsets)capInsets NS_AVAILABLE_IOS(7_0);  // Resizable snapshots will default to stretching the center
 // Use this method to render a snapshot of the view hierarchy into the current context. Returns NO if the snapshot is missing image data, YES if the snapshot is complete. Calling this method from layoutSubviews while the current transaction is committing will capture what is currently displayed regardless if afterUpdates is YES.
 - (BOOL)drawViewHierarchyInRect:(CGRect)rect afterScreenUpdates:(BOOL)afterUpdates NS_AVAILABLE_IOS(7_0);
 @end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewAnimating.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewAnimating.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewAnimating.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewAnimating.h	2016-06-03 05:02:46.000000000 +0200
@@ -0,0 +1,81 @@
+//
+//  UIViewAnimating.h
+//  UIKit
+//
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
+//
+
+
+#import <Foundation/Foundation.h>
+
+typedef NS_ENUM(NSInteger, UIViewAnimatingState)
+{
+    UIViewAnimatingStateInactive, // The animation is not executing.
+    UIViewAnimatingStateActive,   // The animation is executing.
+    UIViewAnimatingStateStopped,  // The animation has been stopped and has not transitioned to inactive.
+} NS_ENUM_AVAILABLE_IOS(10_0) ;
+
+typedef NS_ENUM(NSInteger, UIViewAnimatingPosition) {
+    UIViewAnimatingPositionEnd,
+    UIViewAnimatingPositionStart,
+    UIViewAnimatingPositionCurrent,
+} NS_ENUM_AVAILABLE_IOS(10_0);
+
+
+NS_ASSUME_NONNULL_BEGIN
+
+@protocol UIViewAnimating <NSObject>
+
+@property(nonatomic, readonly) UIViewAnimatingState state;
+
+// Running indicates that the animation is running either in the forward or the reversed direction.
+// The state of a running animation is always active.
+@property(nonatomic, readonly, getter=isRunning) BOOL running;
+
+// Reversed indicates that the animation is running in the reversed direction when running is YES.
+// If running is NO, it indicates that it will run in the reversed direction when it is started.
+@property(nonatomic, getter=isReversed) BOOL reversed;
+
+// fractionComplete values are typically between 0 and 1. Some adopters may choose to give
+// meaning to values less than zero and greater than 1 to facilitate over and
+// undershooting.  The setter is usually a nop when the animation is
+// running. Adopters are free to change this if it makes sense. An adopter
+// may also choose to only return a meaningful result for this property if it 
+// is read while the animation is not running.
+@property(nonatomic) CGFloat fractionComplete;  
+
+// Starts the animation either from an inactive state, or if the animation has been paused.
+- (void)startAnimation;
+
+// Pauses an active, running animation, or start the animation as paused. This is different
+// than stopping an animation.
+- (void)pauseAnimation;
+
+// Stops the animation.  The values of a view's animated property values are
+// updated to correspond to the values that were last rendered. If
+// withoutFinishing == YES, then the animator immediately becomes
+// inactive. Otherwise it enters the stopped state and it is incumbent on the
+// client to explicitly finish the animation by calling finishAnimationAtPosition:. Note
+// when an animation finishes naturally this method is not called.
+- (void)stopAnimation:(BOOL) withoutFinishing;
+
+// This method may only be called if the animator is in the stopped state.
+// The finalPosition argument should indicate the final values of the animated properties.
+- (void)finishAnimationAtPosition:(UIViewAnimatingPosition)finalPosition;
+
+@end
+
+@protocol UITimingCurveProvider;
+
+@protocol UIViewImplicitlyAnimating <UIViewAnimating>
+
+@optional
+
+- (void)addAnimations:(void (^)(void))animation delayFactor:(CGFloat)delayFactor;
+- (void)addAnimations:(void (^)(void))animation;
+- (void)addCompletion:(void (^)(UIViewAnimatingPosition finalPosition))completion;
+- (void)continueAnimationWithTimingParameters:(nullable id <UITimingCurveProvider>)parameters durationFactor:(CGFloat)durationFactor;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewController.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewController.h	2016-06-03 05:02:19.000000000 +0200
@@ -186,6 +186,9 @@
 // A controller that defines the presentation context can also specify the modal transition style if this property is true.
 @property(nonatomic,assign) BOOL providesPresentationContextTransitionStyle NS_AVAILABLE_IOS(5_0);
 
+// If YES, when this view controller becomes visible and focusable, focus will be automatically restored to the item that was last focused. For example, when an item in this view controller is focused, and then another view controller is presented and dismissed, the original item will become focused again. Defaults to YES.
+@property (nonatomic) BOOL restoresFocusAfterTransition NS_AVAILABLE_IOS(10_0);
+
 /*
   These four methods can be used in a view controller's appearance callbacks to determine if it is being
   presented, dismissed, or added or removed as a child view controller. For example, a view controller can
@@ -338,7 +341,7 @@
   Removes the the receiver from its parent's children controllers array. If this method is overridden then
   the super implementation must be called.
 */
-- (void) removeFromParentViewController NS_AVAILABLE_IOS(5_0);
+- (void)removeFromParentViewController NS_AVAILABLE_IOS(5_0);
 
 /*
   This method can be used to transition between sibling child view controllers. The receiver of this method is
@@ -399,8 +402,8 @@
   addChildViewController: will call [child willMoveToParentViewController:self] before adding the
   child. However, it will not call didMoveToParentViewController:. It is expected that a container view
   controller subclass will make this call after a transition to the new child has completed or, in the
-  case of no transition, immediately after the call to addChildViewController:. Similarly
-  removeFromParentViewController: does not call [self willMoveToParentViewController:nil] before removing the
+  case of no transition, immediately after the call to addChildViewController:. Similarly,
+  removeFromParentViewController does not call [self willMoveToParentViewController:nil] before removing the
   child. This is also the responsibilty of the container subclass. Container subclasses will typically define
   a method that transitions to a new child by first calling addChildViewController:, then executing a
   transition which will add the new child's view into the view hierarchy of its parent, and finally will call
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitionCoordinator.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitionCoordinator.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitionCoordinator.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitionCoordinator.h	2016-06-03 05:02:46.000000000 +0200
@@ -24,9 +24,12 @@
 // or dismissal.
 - (UIModalPresentationStyle)presentationStyle;
 
-// initiallyInteractive can only be YES if isAnimated is YES. It never changes during the course of a transition. This indicates whether the transition
-// was initiated as an interactive transition. If this is no, isInteractive can not be YES.
+/// initiallyInteractive indicates whether the transition was initiated as an interactive transition.
+/// It never changes during the course of a transition.
+/// It can only be YES if isAnimated is YES.
+///If it is NO, then isInteractive can only be YES if isInterruptible is YES
 - (BOOL)initiallyInteractive;
+@property(nonatomic,readonly) BOOL isInterruptible NS_AVAILABLE_IOS(10_0);
 
 // Interactive transitions have non-interactive segments. For example, they all complete non-interactively. Some interactive transitions may have
 // intermediate segments that are not interactive.
@@ -101,7 +104,13 @@
 // appearing will receive a viewWillDisappear: call, and the view controller
 // that was disappearing will receive a viewWillAppear: call.  This handler is
 // invoked BEFORE the "will" method calls are made.
-- (void)notifyWhenInteractionEndsUsingBlock: (void (^)(id <UIViewControllerTransitionCoordinatorContext>context))handler;
+- (void)notifyWhenInteractionEndsUsingBlock: (void (^)(id <UIViewControllerTransitionCoordinatorContext>context))handler NS_DEPRECATED_IOS(7_0, 10_0,"Use notifyWhenInteractionChangesUsingBlock");
+
+// This method behavior is identical to the method above. On 10.0, however, the behavior has
+// changed slightly to account for the fact that transitions can be interruptible. For interruptible transitions
+// The block may be called multiple times. It is called each time the transition moves from an interactive to a 
+// non-interactive state and vice-versa. The block is now also retained until the transition has completed.
+- (void)notifyWhenInteractionChangesUsingBlock: (void (^)(id <UIViewControllerTransitionCoordinatorContext>context))handler NS_AVAILABLE_IOS(10_0);
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitioning.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitioning.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitioning.h	2015-11-03 03:37:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitioning.h	2016-06-03 06:16:40.000000000 +0200
@@ -8,6 +8,8 @@
 #import <Foundation/Foundation.h>
 #import <UIKit/UIViewController.h>
 #import <UIKit/UIViewControllerTransitionCoordinator.h>
+#import <UIKit/UIViewAnimating.h>
+#import <UIKit/UITimingParameters.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -31,12 +33,12 @@
 // then the system automatically invokes the animator's animateTransition:
 // method.
 //
-// The system queries the view controller's transitionDelegate or the the
+// The system queries the view controller's transitioningDelegate or the
 // navigation controller's delegate to determine if an animator or interaction
-// controller should be used in a transition. The transitionDelegate is a new
+// controller should be used in a transition. The transitioningDelegate is a new
 // propery on UIViewController and conforms to the
 // UIViewControllerTransitioningDelegate protocol defined below. The navigation
-// controller likewise has been agumented with a couple of new delegate methods.
+// controller likewise has been augmented with a couple of new delegate methods.
 //
 // The UIViewControllerContextTransitioning protocol can be adopted by custom
 // container controllers.  It is purposely general to cover more complex
@@ -53,34 +55,45 @@
 // within the containerView specified by the context. For interactive
 // transitions the context's updateInteractiveTransition:,
 // finishInteractiveTransition or cancelInteractiveTransition should be called
-// as the interactive animation proceeds. A concrete interaction controller
-// class, UIPercentDrivenInteractiveTransition, is provided below to
-// interactive; drive CA transitions defined by an animator.
+// as the interactive animation proceeds. The UIPercentDrivenInteractiveTransition
+// class provides an implementation of the UIViewControllerInteractiveTransitioning
+// protocol that can be used to interactively drive any UIView property animations
+// that are created by an animator.
+
 
 @protocol UIViewControllerContextTransitioning <NSObject>
 
 // The view in which the animated transition should take place.
-- (nullable UIView *)containerView;
+- (UIView *)containerView;
 
 // Most of the time this is YES. For custom transitions that use the new UIModalPresentationCustom
 // presentation type we will invoke the animateTransition: even though the transition should not be
 // animated. This allows the custom transition to add or remove subviews to the container view. 
 - (BOOL)isAnimated;
 
+// The next two values can change if the animating transition is interruptible.
 - (BOOL)isInteractive; // This indicates whether the transition is currently interactive.
-
 - (BOOL)transitionWasCancelled;
 
 - (UIModalPresentationStyle)presentationStyle;
 
-// It only makes sense to call these from an interaction controller that
-// conforms to the UIViewControllerInteractiveTransitioning protocol and was
-// vended to the system by a container view controller's delegate or, in the case
-// of a present or dismiss, the transitioningDelegate.
+// An interaction controller that conforms to the
+// UIViewControllerInteractiveTransitioning protocol (which is vended by a
+// container view controller's delegate or, in the case of a presentation, the
+// transitioningDelegate) should call these methods as the interactive
+// transition is scrubbed and then either cancelled or completed. Note that if
+// the animator is interruptible, then calling finishInteractiveTransition: and
+// cancelInteractiveTransition: are indications that if the transition is not
+// interrupted again it will finish naturally or be cancelled.
+
 - (void)updateInteractiveTransition:(CGFloat)percentComplete;
 - (void)finishInteractiveTransition;
 - (void)cancelInteractiveTransition;
 
+// This should be called if the transition animation is interruptible and it 
+// is being paused.
+- (void)pauseInteractiveTransition NS_AVAILABLE_IOS(10_0);
+
 // This must be called whenever a transition completes (or is cancelled.)
 // Typically this is called by the object conforming to the
 // UIViewControllerAnimatedTransitioning protocol that was vended by the transitioning
@@ -117,15 +130,25 @@
 
 @protocol UIViewControllerAnimatedTransitioning <NSObject>
 
-// This is used for percent driven interactive transitions, as well as for container controllers that have companion animations that might need to
-// synchronize with the main animation. 
+// This is used for percent driven interactive transitions, as well as for
+// container controllers that have companion animations that might need to
+// synchronize with the main animation.
 - (NSTimeInterval)transitionDuration:(nullable id <UIViewControllerContextTransitioning>)transitionContext;
 // This method can only  be a nop if the transition is interactive and not a percentDriven interactive transition.
 - (void)animateTransition:(id <UIViewControllerContextTransitioning>)transitionContext;
 
-
 @optional
 
+/// A conforming object implements this method if the transition it creates can
+/// be interrupted. For example, it could return an instance of a
+/// UIViewPropertyAnimator. It is expected that this method will return the same
+/// instance for the life of a transition. An interruptibleAnimator should only
+/// be created if the transitionContext is not nil. If the transitionContext is
+/// nil, then this method should return the previously created
+/// interruptibleAnimator if the transition is still in flight, or nil if it is
+/// not.
+- (nullable id <UIViewImplicitlyAnimating>) interruptibleAnimatorForTransition:(nullable id <UIViewControllerContextTransitioning>)transitionContext NS_AVAILABLE_IOS(10_0);
+
 // This is a convenience and if implemented will be invoked by the system when the transition context's completeTransition: method is invoked.
 - (void)animationEnded:(BOOL) transitionCompleted;
 
@@ -139,6 +162,13 @@
 - (CGFloat)completionSpeed;
 - (UIViewAnimationCurve)completionCurve;
 
+/// In 10.0, if an object conforming to UIViewControllerAnimatedTransitioning is
+/// known to be interruptible, it is possible to start it as if it was not
+/// interactive and then interrupt the transition and interact with it. In this
+/// case, implement this method and return NO. If an interactor does not
+/// implement this method, YES is assumed.
+@property (nonatomic, readonly) BOOL wantsInteractiveStart NS_AVAILABLE_IOS(10_0);
+
 @end
 
 @class UIPresentationController;
@@ -154,32 +184,47 @@
 
 - (nullable id <UIViewControllerInteractiveTransitioning>)interactionControllerForDismissal:(id <UIViewControllerAnimatedTransitioning>)animator;
 
-- (nullable UIPresentationController *)presentationControllerForPresentedViewController:(UIViewController *)presented presentingViewController:(UIViewController *)presenting sourceViewController:(UIViewController *)source NS_AVAILABLE_IOS(8_0);
+- (nullable UIPresentationController *)presentationControllerForPresentedViewController:(UIViewController *)presented presentingViewController:(nullable UIViewController *)presenting sourceViewController:(UIViewController *)source NS_AVAILABLE_IOS(8_0);
 
 @end
 
 NS_CLASS_AVAILABLE_IOS(7_0) @interface UIPercentDrivenInteractiveTransition : NSObject <UIViewControllerInteractiveTransitioning>
 
-// This is the non-interactive duration that was returned when the
-// animators transitionDuration: method was called when the transition started.
+/// This is the non-interactive duration that was returned when the
+/// animators transitionDuration: method was called when the transition started.
 @property (readonly) CGFloat duration;
 
-// The last percentComplete value specified by updateInteractiveTransition:
+/// The last percentComplete value specified by updateInteractiveTransition:
 @property (readonly) CGFloat percentComplete;
 
-// completionSpeed defaults to 1.0 which corresponds to a completion duration of
-// (1 - percentComplete)*duration.  It must be greater than 0.0. The actual
-// completion is inversely proportional to the completionSpeed.  This can be set
-// before cancelInteractiveTransition or finishInteractiveTransition is called
-// in order to speed up or slow down the non interactive part of the
-// transition.
+/// completionSpeed defaults to 1.0 which corresponds to a completion duration of
+/// (1 - percentComplete)*duration.  It must be greater than 0.0. The actual
+/// completion is inversely proportional to the completionSpeed.  This can be set
+/// before cancelInteractiveTransition or finishInteractiveTransition is called
+/// in order to speed up or slow down the non interactive part of the
+/// transition.
 @property (nonatomic,assign) CGFloat completionSpeed;
 
-// When the interactive part of the transition has completed, this property can
-// be set to indicate a different animation curve. It defaults to UIViewAnimationCurveEaseInOut.
-// Note that during the interactive portion of the animation the timing curve is linear. 
+/// When the interactive part of the transition has completed, this property can
+/// be set to indicate a different animation curve. It defaults to UIViewAnimationCurveEaseInOut.
+/// Note that during the interactive portion of the animation the timing curve is linear. 
 @property (nonatomic,assign) UIViewAnimationCurve completionCurve;
 
+/// For an interruptible animator, one can specify a different timing curve provider to use when the
+/// transition is continued. This property is ignored if the animated transitioning object does not
+/// vend an interruptible animator.
+@property (nullable, nonatomic, strong)id <UITimingCurveProvider> timingCurve NS_AVAILABLE_IOS(10_0);
+
+/// Set this to NO in order to start an interruptible transition non
+/// interactively. By default this is YES, which is consistent with the behavior
+/// before 10.0.
+@property (nonatomic) BOOL wantsInteractiveStart NS_AVAILABLE_IOS(10_0);
+
+/// Use this method to pause a running interruptible animator. This will ensure that all blocks
+/// provided by a transition coordinator's notifyWhenInteractionChangesUsingBlock: method
+/// are executed when a transition moves in and out of an interactive mode.
+- (void)pauseInteractiveTransition NS_AVAILABLE_IOS(10_0);
+
 // These methods should be called by the gesture recognizer or some other logic
 // to drive the interaction. This style of interaction controller should only be
 // used with an animator that implements a CA style transition in the animator's
@@ -187,8 +232,8 @@
 // specified, the animateTransition: method must ensure to call the
 // UIViewControllerTransitionParameters completeTransition: method. The other
 // interactive methods on UIViewControllerContextTransitioning should NOT be
-// called.
-
+// called. If there is an interruptible animator, these methods will either scrub or continue 
+// the transition in the forward or reverse directions.
 - (void)updateInteractiveTransition:(CGFloat)percentComplete;
 - (void)cancelInteractiveTransition;
 - (void)finishInteractiveTransition;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewPropertyAnimator.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewPropertyAnimator.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewPropertyAnimator.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewPropertyAnimator.h	2016-06-03 05:02:46.000000000 +0200
@@ -0,0 +1,75 @@
+//
+//  UIViewPropertyAnimator.h
+//  UIKit
+//
+//  Copyright (c) 2005-2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <UIKit/UIViewAnimating.h>
+#import <UIKit/UITimingParameters.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+NS_CLASS_AVAILABLE_IOS(10_0) @interface UIViewPropertyAnimator : NSObject <UIViewImplicitlyAnimating, NSCopying>
+
+@property(nullable, nonatomic, copy, readonly) id <UITimingCurveProvider> timingParameters;
+
+@property(nonatomic, readonly) NSTimeInterval duration;
+
+/// Defaults to YES. Raises if set on an active animator.
+@property(nonatomic, getter=isUserInteractionEnabled) BOOL userInteractionEnabled;
+
+/// Defaults to YES. Raises if set on an active animator.
+@property(nonatomic, getter=isInterruptible) BOOL interruptible;
+
+- (instancetype)initWithDuration:(NSTimeInterval)duration timingParameters:(id <UITimingCurveProvider>)parameters NS_DESIGNATED_INITIALIZER;
+
+// All convenience initializers return an animator which is not running.
+- (instancetype)initWithDuration:(NSTimeInterval)duration curve:(UIViewAnimationCurve)curve animations:(void (^ __nullable)(void))animations;
+- (instancetype)initWithDuration:(NSTimeInterval)duration controlPoint1: (CGPoint)point1 controlPoint2:(CGPoint)point2  animations:(void (^)(void))animations;
+- (instancetype)initWithDuration:(NSTimeInterval)duration dampingRatio:(CGFloat)ratio animations:(void (^ __nullable)(void))animations;
+
+/// @abstract This method provides compatibility with the old style [UIView
+/// animationWithDuration:...]  method. It is also useful for controlling
+/// how animations options are inherited.
+/// @discussion Creates a UIViewPropertyAnimator, sets the duration, options, etc. And starts the
+/// animation with the associated animation and completion blocks. The animator
+/// returned is interruptible only if it is not called from within the execution
+/// block of another animation (animator or legacy). Note that if it is called
+/// within the execution block of another animation it will inherit the duration
+/// and other characteristics of that animation UNLESS the appropriate override
+/// options have been specified. Also note that if is called within the execution
+/// block of another propertyAnimator that is interruptible, the implicit
+/// animations defined by this call will be tracked by the outer
+/// propertyAnimator.
++ (instancetype)runningPropertyAnimatorWithDuration:(NSTimeInterval)duration
+                                              delay:(NSTimeInterval)delay
+                                            options:(UIViewAnimationOptions)options
+                                         animations:(void (^ __nullable)(void))animations
+                                         completion:(void (^ __nullable)(UIViewAnimatingPosition finalPosition))completion;
+
+/// Animatable view properties that are set by the animation block will be
+/// animated to their new values. The animations will commence at delayFactor *
+/// animator.duration seconds into the animation. The duration of the animation
+/// will be (1 - delayFactor) * animator.duration seconds.
+- (void)addAnimations:(void (^)(void))animation delayFactor:(CGFloat)delayFactor;
+
+/// Animatable view properties that are set by the animation block will be
+/// animated to their new values.
+- (void)addAnimations:(void (^)(void))animation;
+
+- (void)addCompletion:(void (^)(UIViewAnimatingPosition finalPosition))completion;
+
+/// Provides a means to continue an animation in either the forward or reversed
+/// directions with new timing parameters and duration.  The durationFactor is in
+/// terms of a unit duration defined by the originally specified duration of the
+/// animator. It is used to specify the remaining time for the animation. When
+/// called, it behaves as if the animation was started from its current position
+/// with a new duration and timing parameters.
+- (void)continueAnimationWithTimingParameters:(nullable id <UITimingCurveProvider>)parameters durationFactor:(CGFloat)durationFactor;
+
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIVisualEffectView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIVisualEffectView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIVisualEffectView.h	2015-11-03 03:37:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIVisualEffectView.h	2016-06-03 06:16:42.000000000 +0200
@@ -5,7 +5,7 @@
 //  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
 //
 
-#import <UIKit/UIKit.h>
+#import <UIKit/UIView.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -23,7 +23,9 @@
 typedef NS_ENUM(NSInteger, UIBlurEffectStyle) {
     UIBlurEffectStyleExtraLight,
     UIBlurEffectStyleLight,
-    UIBlurEffectStyleDark
+    UIBlurEffectStyleDark,
+    UIBlurEffectStyleRegular NS_ENUM_AVAILABLE_IOS(10_0) = 4, // Adapts to user interface style
+    UIBlurEffectStyleProminent NS_ENUM_AVAILABLE_IOS(10_0) = 5, // Adapts to user interface style
 } NS_ENUM_AVAILABLE_IOS(8_0);
 
 NS_CLASS_AVAILABLE_IOS(8_0) @interface UIVisualEffect : NSObject <NSCopying, NSSecureCoding> @end

```