#UIKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSParagraphStyle.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSParagraphStyle.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSParagraphStyle.h	2016-06-03 06:16:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSParagraphStyle.h	2016-06-27 07:03:36.000000000 +0200
@@ -43,7 +43,11 @@
 
 NS_CLASS_AVAILABLE(10_0, 6_0) @interface NSParagraphStyle : NSObject <NSCopying, NSMutableCopying, NSSecureCoding>
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) NSParagraphStyle *defaultParagraphStyle; // This class method returns a shared and cached NSParagraphStyle instance with the default style settings, with same value as the result of [[NSParagraphStyle alloc] init].
+#else
 + (NSParagraphStyle *)defaultParagraphStyle; // This class method returns a shared and cached NSParagraphStyle instance with the default style settings, with same value as the result of [[NSParagraphStyle alloc] init].
+#endif
 
 + (NSWritingDirection)defaultWritingDirectionForLanguage:(nullable NSString *)languageName;  // languageName is in ISO lang region format
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h	2016-05-23 08:16:41.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,435 +0,0 @@
-
-//
-//  UIAccessibility.h
-//  UIKit
-//
-//  Copyright (c) 2008-2015 Apple Inc. All rights reserved.
-//
-
-#import <CoreGraphics/CoreGraphics.h>
-#import <Foundation/Foundation.h>
-#import <UIKit/UIKitDefines.h>
-#import <UIKit/UIBezierPath.h>
-
-#import <UIKit/UIAccessibilityAdditions.h>
-#import <UIKit/UIAccessibilityConstants.h>
-#import <UIKit/UIAccessibilityCustomAction.h>
-#import <UIKit/UIAccessibilityCustomRotor.h>
-#import <UIKit/UIAccessibilityElement.h>
-#import <UIKit/UIAccessibilityIdentification.h>
-#import <UIKit/UIAccessibilityZoom.h>
-#import <UIKit/UIGuidedAccessRestrictions.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-/*
- UIAccessibility
- 
- UIAccessibility is implemented on all standard UIKit views and controls so
- that assistive applications can present them to users with disabilities.
- 
- Custom items in a user interface should override aspects of UIAccessibility
- to supply details where the default value is incomplete.
- 
- For example, a UIImageView subclass may need to override accessibilityLabel,
- but it does not need to override accessibilityFrame.
- 
- A completely custom subclass of UIView might need to override all of the
- UIAccessibility methods except accessibilityFrame.
- */
-
-@interface NSObject (UIAccessibility)
-
-/*
- Return YES if the receiver should be exposed as an accessibility element. 
- default == NO
- default on UIKit controls == YES 
- Setting the property to YES will cause the receiver to be visible to assistive applications. 
- */
-@property (nonatomic) BOOL isAccessibilityElement;
-
-/*
- Returns the localized label that represents the element. 
- If the element does not display text (an icon for example), this method
- should return text that best labels the element. For example: "Play" could be used for
- a button that is used to play music. "Play button" should not be used, since there is a trait
- that identifies the control is a button.
- default == nil
- default on UIKit controls == derived from the title
- Setting the property will change the label that is returned to the accessibility client. 
- */
-@property (nullable, nonatomic, copy) NSString *accessibilityLabel;
-
-/*
- Returns a localized string that describes the result of performing an action on the element, when the result is non-obvious.
- The hint should be a brief phrase.
- For example: "Purchases the item." or "Downloads the attachment."
- default == nil
- Setting the property will change the hint that is returned to the accessibility client. 
- */
-@property (nullable, nonatomic, copy) NSString *accessibilityHint;
-
-/*
- Returns a localized string that represents the value of the element, such as the value 
- of a slider or the text in a text field. Use only when the label of the element
- differs from a value. For example: A volume slider has a label of "Volume", but a value of "60%".
- default == nil
- default on UIKit controls == values for appropriate controls 
- Setting the property will change the value that is returned to the accessibility client.  
- */
-@property (nullable, nonatomic, copy) NSString *accessibilityValue;
-
-/*
- Returns a UIAccessibilityTraits mask that is the OR combination of
- all accessibility traits that best characterize the element.
- See UIAccessibilityConstants.h for a list of traits.
- When overriding this method, remember to combine your custom traits
- with [super accessibilityTraits].
- default == UIAccessibilityTraitNone
- default on UIKit controls == traits that best characterize individual controls. 
- Setting the property will change the traits that are returned to the accessibility client. 
- */
-@property (nonatomic) UIAccessibilityTraits accessibilityTraits;
-
-/*
- Returns the frame of the element in screen coordinates.
- default == CGRectZero
- default on UIViews == the frame of the view
- Setting the property will change the frame that is returned to the accessibility client. 
- */
-@property (nonatomic) CGRect accessibilityFrame;
-
-// The accessibilityFrame is expected to be in screen coordinates.
-// To help convert the frame to screen coordinates, use the following method.
-// The rect should exist in the view space of the UIView argument.
-UIKIT_EXTERN CGRect UIAccessibilityConvertFrameToScreenCoordinates(CGRect rect, UIView *view) NS_AVAILABLE_IOS(7_0);
-
-/*
- Returns the path of the element in screen coordinates.
- default == nil
- Setting the property, or overriding the method, will cause the assistive technology to prefer the path over the accessibility.
- frame when highlighting the element.
- */
-@property (nullable, nonatomic, copy) UIBezierPath *accessibilityPath NS_AVAILABLE_IOS(7_0);
-
-// The accessibilityPath is expected to be in screen coordinates.
-// To help convert the path to screen coordinates, use the following method.
-// The path should exist in the view space of the UIView argument.
-UIKIT_EXTERN UIBezierPath *UIAccessibilityConvertPathToScreenCoordinates(UIBezierPath *path, UIView *view) NS_AVAILABLE_IOS(7_0);
-
-/*
- Returns the activation point for an accessible element in screen coordinates.
- default == Mid-point of the accessibilityFrame.
- */
-@property (nonatomic) CGPoint accessibilityActivationPoint NS_AVAILABLE_IOS(5_0);
-
-/*
- Returns the language code that the element's label, value and hint should be spoken in. 
- If no language is set, the user's language is used.
- The format for the language code should follow Internet BCP 47 for language tags.
- For example, en-US specifies U.S. English.
- default == nil
- */
-@property (nullable, nonatomic, strong) NSString *accessibilityLanguage;
-
-/*
- Marks all the accessible elements contained within as hidden.
- default == NO
- */
-@property (nonatomic) BOOL accessibilityElementsHidden NS_AVAILABLE_IOS(5_0);
-
-/*
- Informs whether the receiving view should be considered modal by accessibility. If YES, then 
- elements outside this view will be ignored. Only elements inside this view will be exposed.
- default == NO
- */
-@property (nonatomic) BOOL accessibilityViewIsModal NS_AVAILABLE_IOS(5_0);
-
-/*
- Forces children elements to be grouped together regardless of their position on screen.
- For example, your app may show items that are meant to be grouped together in vertical columns. 
- By default, VoiceOver will navigate those items in horizontal rows. If shouldGroupAccessibilityChildren is set on
- a parent view of the items in the vertical column, VoiceOver will navigate the order correctly.
- default == NO
- */
-@property (nonatomic) BOOL shouldGroupAccessibilityChildren NS_AVAILABLE_IOS(6_0);
-
-/*
- Some assistive technologies allow the user to select a parent view or container to navigate its elements.
- This property allows an app to specify whether that behavior should apply to the receiver.
- Currently, this property only affects Switch Control, not VoiceOver or other assistive technologies.
- See UIAccessibilityConstants.h for the list of supported values.
- default == UIAccessibilityNavigationStyleAutomatic
- */
-@property (nonatomic) UIAccessibilityNavigationStyle accessibilityNavigationStyle NS_AVAILABLE_IOS(8_0);
-
-/*
- The elements considered to be the headers for this element. May be set on an instance of
- UIAccessibilityElement, a View or a View Controller. The accessibility container chain,
- and associated view controllers where appropriate, will be consulted.
- To avoid retain cycles, a weak copy of the elements will be held.
- */
-@property(nullable, nonatomic, copy) NSArray *accessibilityHeaderElements UIKIT_AVAILABLE_TVOS_ONLY(9_0);
-
-@end
-
-
-/*
- UIAccessibilityContainer
- 
- UIAccessibilityContainer methods can be overridden to vend individual elements
- that are managed by a single UIView.
- 
- For example, a single UIView might draw several items that (to an
- end user) have separate meaning and functionality.  It is important to vend
- each item as an individual accessibility element.
- 
- Sub-elements of a container that are not represented by concrete UIView
- instances (perhaps painted text or icons) can be represented using instances
- of UIAccessibilityElement class (see UIAccessibilityElement.h).
- 
- Accessibility containers MUST return NO to -isAccessibilityElement.
- */
-@interface NSObject (UIAccessibilityContainer)
-
-/*
- Returns the number of accessibility elements in the container.
- */
-- (NSInteger)accessibilityElementCount;
-
-/*
- Returns the accessibility element in order, based on index.
- default == nil 
- */
-- (nullable id)accessibilityElementAtIndex:(NSInteger)index;
-
-/*
- Returns the ordered index for an accessibility element
- default == NSNotFound 
- */
-- (NSInteger)indexOfAccessibilityElement:(id)element;
-
-// A list of container elements managed by the receiver.
-// This can be used as an alternative to implementing the dynamic methods.
-// default == nil
-@property (nullable, nonatomic, strong) NSArray *accessibilityElements NS_AVAILABLE_IOS(8_0);
-
-@end
-
-/*
- UIAccessibilityFocus
- 
- Assistive technologies, like VoiceOver, maintain a virtual focus on an element
- that allows the user to inspect an element without activating it.
- */
-@interface NSObject (UIAccessibilityFocus)
-
-// Override the following methods to know when an assistive technology has set or unset its virtual focus on the element. 
-- (void)accessibilityElementDidBecomeFocused NS_AVAILABLE_IOS(4_0);
-- (void)accessibilityElementDidLoseFocus NS_AVAILABLE_IOS(4_0);
-
-// Returns whether an assistive technology is focused on the element.
-- (BOOL)accessibilityElementIsFocused NS_AVAILABLE_IOS(4_0);
-
-// Returns a set of identifier keys indicating which technology is focused on this object
-- (nullable NSSet<NSString *> *)accessibilityAssistiveTechnologyFocusedIdentifiers NS_AVAILABLE_IOS(9_0);
-
-// Returns the element that is currently focused by an assistive technology.
-// default = nil.
-// Pass in a specific identifier (e.g. UIAccessibilityNotificationVoiceOverIdentifier) in order to choose the focused element for a specific product.
-// If no argument is used, the function will returned the element that was most recently focused.
-UIKIT_EXTERN __nullable id UIAccessibilityFocusedElement(NSString * __nullable assistiveTechnologyIdentifier) NS_AVAILABLE_IOS(9_0);
-
-@end
-
-/*
- UIAccessibilityAction
-
- An element should implement methods in this category if it supports the action.
- */
-@interface NSObject (UIAccessibilityAction)
-
-/*
- Implement accessibilityActivate on an element in order to handle the default action.
- For example, if a native control requires a swipe gesture, you may implement this method so that a
- VoiceOver user will perform a double-tap to activate the item.
- If your implementation successfully handles activate, return YES, otherwise return NO.
- default == NO
- */
-- (BOOL)accessibilityActivate NS_AVAILABLE_IOS(7_0);
-
-/* 
- If an element has the UIAccessibilityTraitAdjustable trait, it must also implement
- the following methods. Incrementing will adjust the element so that it increases its content,
- while decrementing decreases its content. For example, accessibilityIncrement will increase the value
- of a UISlider, and accessibilityDecrement will decrease the value.
- */   
-- (void)accessibilityIncrement NS_AVAILABLE_IOS(4_0);
-- (void)accessibilityDecrement NS_AVAILABLE_IOS(4_0);
-
-/*
- If the user interface requires a scrolling action (e.g. turning the page of a book), a view in the view 
- hierarchy should implement the following method. The return result indicates whether the action 
- succeeded for that direction. If the action failed, the method will be called on a view higher 
- in the hierarchy. If the action succeeds, UIAccessibilityPageScrolledNotification must be posted after
- the scrolling completes.
- default == NO
- */
-typedef NS_ENUM(NSInteger, UIAccessibilityScrollDirection) {
-    UIAccessibilityScrollDirectionRight = 1,
-    UIAccessibilityScrollDirectionLeft,
-    UIAccessibilityScrollDirectionUp,
-    UIAccessibilityScrollDirectionDown,
-    UIAccessibilityScrollDirectionNext NS_ENUM_AVAILABLE_IOS(5_0),
-    UIAccessibilityScrollDirectionPrevious NS_ENUM_AVAILABLE_IOS(5_0),
-};
-
-- (BOOL)accessibilityScroll:(UIAccessibilityScrollDirection)direction NS_AVAILABLE_IOS(4_2);
-
-/* 
- Implement accessibilityPerformEscape on an element or containing view to exit a modal or hierarchical interface view.
- For example, UIPopoverController implements accessibilityPerformEscape on it's root view, so that when
- called (as a result of a VoiceOver user action), it dismisses the popover.
- If your implementation successfully dismisses the current UI, return YES, otherwise return NO.
- default == NO
- */
-- (BOOL)accessibilityPerformEscape NS_AVAILABLE_IOS(5_0);
-
-/* 
- Implement accessibilityPerformMagicTap on an element, or the application, in order to provide a context-sensitive action.
- For example, a music player can implement this to start and stop playback, or a recording app could start and stop recording.
- Return YES to indicate that the action was handled.
- default == NO
- */
-- (BOOL)accessibilityPerformMagicTap NS_AVAILABLE_IOS(6_0);
-
-/*
- Return an array of UIAccessibilityCustomAction objects to make custom actions for an element accessible to an assistive technology.
- For example, a photo app might have a view that deletes its corresponding photo in response to a flick gesture.
- If the view returns a delete action from this property, VoiceOver and Switch Control users will be able to delete photos without performing the flick gesture.
- default == nil
- */
-@property (nullable, nonatomic, strong) NSArray <UIAccessibilityCustomAction *> *accessibilityCustomActions NS_AVAILABLE_IOS(8_0);
-@end
-
-/* 
- UIAccessibilityReadingContent
- 
- Implemented on an element that represents content meant to be read, like a book or periodical. 
- Use in conjuction with UIAccessibilityTraitCausesPageTurn to provide a continuous reading experience with VoiceOver.
- */
-@protocol UIAccessibilityReadingContent
-@required
-
-// Returns the line number given a point in the view's coordinate space.
-- (NSInteger)accessibilityLineNumberForPoint:(CGPoint)point NS_AVAILABLE_IOS(5_0);
-
-// Returns the content associated with a line number as a string.
-- (nullable NSString *)accessibilityContentForLineNumber:(NSInteger)lineNumber NS_AVAILABLE_IOS(5_0);
-
-// Returns the on-screen rectangle for a line number.
-- (CGRect)accessibilityFrameForLineNumber:(NSInteger)lineNumber NS_AVAILABLE_IOS(5_0);
-
-// Returns a string representing the text displayed on the current page.
-- (nullable NSString *)accessibilityPageContent NS_AVAILABLE_IOS(5_0);
-
-@end
-
-/*
- UIAccessibilityPostNotification
- 
- This function posts a notification to assistive applications.
- Some notifications specify a required or optional argument.
- Pass nil for the argument if the notification does not specify otherwise. 
- See UIAccessibilityConstants.h for a list of notifications.
- */
-UIKIT_EXTERN void UIAccessibilityPostNotification(UIAccessibilityNotifications notification, __nullable id argument);
-
-/* 
- Assistive Technology
- 
- Use UIAccessibilityIsVoiceOverRunning() to determine if VoiceOver is running.
- Listen for UIAccessibilityVoiceOverStatusChanged to know when VoiceOver starts or stops.
- */
-UIKIT_EXTERN BOOL UIAccessibilityIsVoiceOverRunning(void) NS_AVAILABLE_IOS(4_0);
-UIKIT_EXTERN NSString *const UIAccessibilityVoiceOverStatusChanged NS_AVAILABLE_IOS(4_0);
-
-// Returns whether system audio is mixed down from stereo to mono.
-UIKIT_EXTERN BOOL UIAccessibilityIsMonoAudioEnabled(void) NS_AVAILABLE_IOS(5_0);
-UIKIT_EXTERN NSString *const UIAccessibilityMonoAudioStatusDidChangeNotification NS_AVAILABLE_IOS(5_0);
-
-// Returns whether the system preference for closed captioning is enabled.
-UIKIT_EXTERN BOOL UIAccessibilityIsClosedCaptioningEnabled(void) NS_AVAILABLE_IOS(5_0);
-UIKIT_EXTERN NSString *const UIAccessibilityClosedCaptioningStatusDidChangeNotification NS_AVAILABLE_IOS(5_0);
-
-// Returns whether the system preference for invert colors is enabled.
-UIKIT_EXTERN BOOL UIAccessibilityIsInvertColorsEnabled(void) NS_AVAILABLE_IOS(6_0);
-UIKIT_EXTERN NSString *const UIAccessibilityInvertColorsStatusDidChangeNotification NS_AVAILABLE_IOS(6_0);
-
-// Returns whether the app is running under Guided Access mode.
-UIKIT_EXTERN BOOL UIAccessibilityIsGuidedAccessEnabled(void) NS_AVAILABLE_IOS(6_0);
-UIKIT_EXTERN NSString *const UIAccessibilityGuidedAccessStatusDidChangeNotification NS_AVAILABLE_IOS(6_0);
-
-// Returns whether the system preference for bold text is enabled
-UIKIT_EXTERN BOOL UIAccessibilityIsBoldTextEnabled(void) NS_AVAILABLE_IOS(8_0);
-UIKIT_EXTERN NSString *const UIAccessibilityBoldTextStatusDidChangeNotification NS_AVAILABLE_IOS(8_0);
-
-// Returns whether the system preference for grayscale is enabled
-UIKIT_EXTERN BOOL UIAccessibilityIsGrayscaleEnabled(void) NS_AVAILABLE_IOS(8_0);
-UIKIT_EXTERN NSString *const UIAccessibilityGrayscaleStatusDidChangeNotification NS_AVAILABLE_IOS(8_0);
-
-// Returns whether the system preference for reduce transparency is enabled
-UIKIT_EXTERN BOOL UIAccessibilityIsReduceTransparencyEnabled(void) NS_AVAILABLE_IOS(8_0);
-UIKIT_EXTERN NSString *const UIAccessibilityReduceTransparencyStatusDidChangeNotification NS_AVAILABLE_IOS(8_0);
-
-// Returns whether the system preference for reduce motion is enabled
-UIKIT_EXTERN BOOL UIAccessibilityIsReduceMotionEnabled(void) NS_AVAILABLE_IOS(8_0);
-UIKIT_EXTERN NSString *const UIAccessibilityReduceMotionStatusDidChangeNotification NS_AVAILABLE_IOS(8_0);
-
-// Returns whether the system preference for darker colors is enabled
-UIKIT_EXTERN BOOL UIAccessibilityDarkerSystemColorsEnabled(void) NS_AVAILABLE_IOS(8_0);
-UIKIT_EXTERN NSString *const UIAccessibilityDarkerSystemColorsStatusDidChangeNotification NS_AVAILABLE_IOS(8_0);
-
-/*
- Use UIAccessibilityIsSwitchControlRunning() to determine if Switch Control is running.
- Listen for UIAccessibilitySwitchControlStatusDidChangeNotification to know when Switch Control starts or stops.
-*/
-UIKIT_EXTERN BOOL UIAccessibilityIsSwitchControlRunning(void) NS_AVAILABLE_IOS(8_0);
-UIKIT_EXTERN NSString *const UIAccessibilitySwitchControlStatusDidChangeNotification NS_AVAILABLE_IOS(8_0);
-
-// Returns whether the system preference for Speak Selection is enabled
-UIKIT_EXTERN BOOL UIAccessibilityIsSpeakSelectionEnabled(void) NS_AVAILABLE_IOS(8_0);
-UIKIT_EXTERN NSString *const UIAccessibilitySpeakSelectionStatusDidChangeNotification NS_AVAILABLE_IOS(8_0);
-
-// Returns whether the system preference for Speak Screen is enabled
-UIKIT_EXTERN BOOL UIAccessibilityIsSpeakScreenEnabled(void) NS_AVAILABLE_IOS(8_0);
-UIKIT_EXTERN NSString *const UIAccessibilitySpeakScreenStatusDidChangeNotification NS_AVAILABLE_IOS(8_0);
-
-// Returns whether the system preference for Shake to Undo is enabled
-UIKIT_EXTERN BOOL UIAccessibilityIsShakeToUndoEnabled(void) NS_AVAILABLE_IOS(9_0);
-UIKIT_EXTERN NSString *const UIAccessibilityShakeToUndoDidChangeNotification NS_AVAILABLE_IOS(9_0);
-
-// Returns whether the system preference for AssistiveTouch is enabled
-UIKIT_EXTERN BOOL UIAccessibilityIsAssistiveTouchRunning(void) NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UIAccessibilityAssistiveTouchStatusDidChangeNotification NS_AVAILABLE_IOS(10_0);
-
-/*
- Use UIAccessibilityRequestGuidedAccessSession() to request this app be locked into or released
- from Single App mode. The request to lock this app into Single App mode will only succeed if the device is Supervised,
- and the app's bundle identifier has been whitelisted using Mobile Device Management. If you successfully request Single
- App mode, it is your responsibility to release the device by balancing this call.
- */
-UIKIT_EXTERN void UIAccessibilityRequestGuidedAccessSession(BOOL enable, void(^completionHandler)(BOOL didSucceed)) NS_AVAILABLE_IOS(7_0);
-
-typedef NS_OPTIONS(NSUInteger, UIAccessibilityHearingDeviceEar) {
-    UIAccessibilityHearingDeviceEarNone    = 0,
-    UIAccessibilityHearingDeviceEarLeft    = 1 << 1,
-    UIAccessibilityHearingDeviceEarRight   = 1 << 2,
-    UIAccessibilityHearingDeviceEarBoth    = UIAccessibilityHearingDeviceEarLeft | UIAccessibilityHearingDeviceEarRight,
-} NS_ENUM_AVAILABLE_IOS(10_0);
-
-// Returns the current pairing status of MFi hearing aids
-UIKIT_EXTERN UIAccessibilityHearingDeviceEar UIAccessibilityHearingDevicePairedEar(void) NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UIAccessibilityHearingDevicePairedEarDidChangeNotification NS_AVAILABLE_IOS(10_0);
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityCustomAction.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityCustomAction.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityCustomAction.h	2016-05-23 08:16:41.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityCustomAction.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,36 +0,0 @@
-//
-//  UIAccessibilityCustomAction.h
-//  UIKit
-//
-//  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
-//
-
-#import <Foundation/Foundation.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-NS_CLASS_AVAILABLE_IOS(8_0) @interface UIAccessibilityCustomAction : NSObject
-
-- (instancetype)initWithName:(NSString *)name target:(nullable id)target selector:(SEL)selector;
-
-/*
- A localized name that describes the action.
- */
-@property (nonatomic, copy) NSString *name;
-
-/*
- The object that will perform the action.
- */
-@property (nullable, nonatomic, weak) id target;
-
-/*
- The method that will be called on the target to perform the action.
- It must conform to one of the following signatures:
- - (BOOL)myPerformActionMethod;
- - (BOOL)myPerformActionMethod:(UIAccessibilityCustomAction *)action;
- */
-@property (nonatomic, assign) SEL selector;
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityIdentification.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityIdentification.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityIdentification.h	2016-05-23 08:16:41.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibilityIdentification.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,39 +0,0 @@
-//
-//  UIAccessibilityIdentification.h
-//  UIKit
-//
-//  Copyright 2010-2012 Apple Inc. All rights reserved.
-//
-
-#import <Foundation/Foundation.h>
-#import <UIKit/UIView.h>
-#import <UIKit/UIImage.h>
-#import <UIKit/UIBarItem.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-@protocol UIAccessibilityIdentification <NSObject>
-@required
-
-/*
- A string that identifies the user interface element.
- default == nil
-*/
-@property(nullable, nonatomic, copy) NSString *accessibilityIdentifier NS_AVAILABLE_IOS(5_0);
-
-@end
-
-@interface UIView (UIAccessibility) <UIAccessibilityIdentification>
-@end
-
-@interface UIBarItem (UIAccessibility) <UIAccessibilityIdentification>
-@end
-
-/*
- Defaults to the filename of the image, if available.
- The default identifier for a UIImageView will be the identifier of its UIImage.
- */
-@interface UIImage (UIAccessibility) <UIAccessibilityIdentification>
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIColor.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIColor.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIColor.h	2016-05-23 08:16:41.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIColor.h	2016-06-29 06:37:32.000000000 +0200
@@ -42,7 +42,24 @@
 
 // Some convenience methods to create colors.  These colors will be as calibrated as possible.
 // These colors are cached.
-+ (UIColor *)blackColor;      // 0.0 white 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) UIColor *blackColor;      // 0.0 white
+@property(class, nonatomic, readonly) UIColor *darkGrayColor;   // 0.333 white
+@property(class, nonatomic, readonly) UIColor *lightGrayColor;  // 0.667 white
+@property(class, nonatomic, readonly) UIColor *whiteColor;      // 1.0 white
+@property(class, nonatomic, readonly) UIColor *grayColor;       // 0.5 white
+@property(class, nonatomic, readonly) UIColor *redColor;        // 1.0, 0.0, 0.0 RGB
+@property(class, nonatomic, readonly) UIColor *greenColor;      // 0.0, 1.0, 0.0 RGB
+@property(class, nonatomic, readonly) UIColor *blueColor;       // 0.0, 0.0, 1.0 RGB
+@property(class, nonatomic, readonly) UIColor *cyanColor;       // 0.0, 1.0, 1.0 RGB
+@property(class, nonatomic, readonly) UIColor *yellowColor;     // 1.0, 1.0, 0.0 RGB
+@property(class, nonatomic, readonly) UIColor *magentaColor;    // 1.0, 0.0, 1.0 RGB
+@property(class, nonatomic, readonly) UIColor *orangeColor;     // 1.0, 0.5, 0.0 RGB
+@property(class, nonatomic, readonly) UIColor *purpleColor;     // 0.5, 0.0, 0.5 RGB
+@property(class, nonatomic, readonly) UIColor *brownColor;      // 0.6, 0.4, 0.2 RGB
+@property(class, nonatomic, readonly) UIColor *clearColor;      // 0.0 white, 0.0 alpha
+#else
++ (UIColor *)blackColor;      // 0.0 white
 + (UIColor *)darkGrayColor;   // 0.333 white 
 + (UIColor *)lightGrayColor;  // 0.667 white 
 + (UIColor *)whiteColor;      // 1.0 white 
@@ -57,6 +74,7 @@
 + (UIColor *)purpleColor;     // 0.5, 0.0, 0.5 RGB 
 + (UIColor *)brownColor;      // 0.6, 0.4, 0.2 RGB 
 + (UIColor *)clearColor;      // 0.0 white, 0.0 alpha 
+#endif
 
 // Set the color: Sets the fill and stroke colors in the current drawing context. Should be implemented by subclassers.
 - (void)set;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h	2016-05-23 08:16:41.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h	2016-06-27 07:06:58.000000000 +0200
@@ -25,7 +25,11 @@
 + (nullable UIFont *)fontWithName:(NSString *)fontName size:(CGFloat)fontSize;
 
 // Returns an array of font family names for all installed fonts
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) NSArray<NSString *> *familyNames;
+#else
 + (NSArray<NSString *> *)familyNames;
+#endif
 
 // Returns an array of font names for the specified family name
 + (NSArray<NSString *> *)fontNamesForFamilyName:(NSString *)familyName;
@@ -63,7 +67,11 @@
 + (UIFont *)fontWithDescriptor:(UIFontDescriptor *)descriptor size:(CGFloat)pointSize NS_AVAILABLE_IOS(7_0);
 
 // Returns a font descriptor which describes the font.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) UIFontDescriptor *fontDescriptor NS_AVAILABLE_IOS(7_0);
+#else
 - (UIFontDescriptor *)fontDescriptor NS_AVAILABLE_IOS(7_0);
+#endif
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h	2016-06-03 06:16:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h	2016-06-27 06:29:56.000000000 +0200
@@ -62,7 +62,11 @@
 
 - (nullable id)objectForKey:(NSString *)anAttribute;
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) NSDictionary<NSString *, id> *fontAttributes;
+#else
 - (NSDictionary<NSString *, id> *)fontAttributes;
+#endif
 
 // Instance conversion
 // Returns "normalized" font descriptors matching the receiver. mandatoryKeys is an NSSet instance containing keys that are required to be identical in order to be matched. mandatoryKeys can be nil.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGeometry.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGeometry.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGeometry.h	2016-05-23 07:49:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGeometry.h	2016-06-27 07:06:58.000000000 +0200
@@ -55,8 +55,13 @@
     return offset1.horizontal == offset2.horizontal && offset1.vertical == offset2.vertical;
 }
 
+#if UIKIT_REMOVE_ZERO_FROM_SWIFT
+UIKIT_EXTERN const UIEdgeInsets UIEdgeInsetsZero NS_SWIFT_UNAVAILABLE("Use UIEdgeInsets.zero instead");
+UIKIT_EXTERN const UIOffset UIOffsetZero NS_SWIFT_UNAVAILABLE("Use UIOffset.zero instead");
+#else
 UIKIT_EXTERN const UIEdgeInsets UIEdgeInsetsZero;
 UIKIT_EXTERN const UIOffset UIOffsetZero;
+#endif
 
 UIKIT_EXTERN NSString *NSStringFromCGPoint(CGPoint point);
 UIKIT_EXTERN NSString *NSStringFromCGVector(CGVector vector);
@@ -84,6 +89,15 @@
 + (NSValue *)valueWithUIEdgeInsets:(UIEdgeInsets)insets;
 + (NSValue *)valueWithUIOffset:(UIOffset)insets NS_AVAILABLE_IOS(5_0);
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) CGPoint CGPointValue;
+@property(nonatomic, readonly) CGVector CGVectorValue;
+@property(nonatomic, readonly) CGSize CGSizeValue;
+@property(nonatomic, readonly) CGRect CGRectValue;
+@property(nonatomic, readonly) CGAffineTransform CGAffineTransformValue;
+@property(nonatomic, readonly) UIEdgeInsets UIEdgeInsetsValue;
+@property(nonatomic, readonly) UIOffset UIOffsetValue NS_AVAILABLE_IOS(5_0);
+#else
 - (CGPoint)CGPointValue;
 - (CGVector)CGVectorValue;
 - (CGSize)CGSizeValue;
@@ -91,6 +105,7 @@
 - (CGAffineTransform)CGAffineTransformValue;
 - (UIEdgeInsets)UIEdgeInsetsValue;
 - (UIOffset)UIOffsetValue NS_AVAILABLE_IOS(5_0);
+#endif
 
 @end
     
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImage.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImage.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImage.h	2016-05-23 08:16:41.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImage.h	2016-06-27 07:06:58.000000000 +0200
@@ -137,9 +137,14 @@
 @property (nullable, nonatomic, readonly) UIImageAsset *imageAsset NS_AVAILABLE_IOS(8_0); // The asset is not encoded along with the image. Returns nil if the image is not CGImage based.
 #endif
 
+// Creates a version of this image that, when assigned to a UIImageView’s image property, draws its underlying image contents horizontally mirrored when running under a right-to-left language. Affects the flipsForRightToLeftLayoutDirection property; does not affect the imageOrientation property.
+// This method cannot be used to create a left-to-right version of a right-to-left source image, and will be deprecated in a future release. New code should instead use -imageWithHorizontallyFlippedOrientation to construct a UIImageAsset.
 - (UIImage *)imageFlippedForRightToLeftLayoutDirection NS_AVAILABLE_IOS(9_0);
 @property (nonatomic, readonly) BOOL flipsForRightToLeftLayoutDirection NS_AVAILABLE_IOS(9_0);
 
+// Creates a version of this image with an imageOrientation property that is horizontally mirrored from this image’s. Does not affect the flipsForRightToLeftLayoutDirection property.
+- (UIImage *)imageWithHorizontallyFlippedOrientation NS_AVAILABLE_IOS(10_0);
+
 @end
 
 @interface UIImage(UIImageDeprecated)
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h	2016-06-03 05:02:19.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h	2016-06-27 07:06:58.000000000 +0200
@@ -130,7 +130,6 @@
 #import <UIKit/UIProgressView.h>
 #import <UIKit/UIReferenceLibraryViewController.h>
 #import <UIKit/UIRefreshControl.h>
-#import <UIKit/UIRefreshControlHosting.h>
 #import <UIKit/UIResponder.h>
 #import <UIKit/UIRotationGestureRecognizer.h>
 #import <UIKit/UIScreen.h>
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h	2016-05-23 08:16:41.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h	2016-06-27 07:06:58.000000000 +0200
@@ -26,3 +26,6 @@
 #define UIKIT_CLASS_AVAILABLE_TVOS_ONLY(vers) UIKIT_EXTERN __IOS_UNAVAILABLE __WATCHOS_UNAVAILABLE __TVOS_AVAILABLE(vers)
 #define UIKIT_CLASS_AVAILABLE_IOS_TVOS(_ios, _tvos) UIKIT_EXTERN __IOS_AVAILABLE(_ios) __WATCHOS_UNAVAILABLE __TVOS_AVAILABLE(_tvos)
 #define UIKIT_CLASS_AVAILABLE_IOS_WATCHOS_TVOS(_ios, _watchos, _tvos) UIKIT_EXTERN __IOS_AVAILABLE(_ios) __WATCHOS_AVAILABLE(_watchos) __TVOS_AVAILABLE(_tvos)
+
+#define UIKIT_DEFINE_AS_PROPERTIES (!defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_UIKIT_EPOCH) && SWIFT_SDK_OVERLAY_UIKIT_EPOCH >= 1))
+#define UIKIT_REMOVE_ZERO_FROM_SWIFT (!defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_UIKIT_EPOCH) && SWIFT_SDK_OVERLAY_UIKIT_EPOCH >= 1))

```