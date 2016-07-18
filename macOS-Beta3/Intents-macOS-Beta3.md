#Intents.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INConditionalOperator.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INConditionalOperator.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INConditionalOperator.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INConditionalOperator.h	2016-07-12 07:04:02.000000000 +0200
@@ -14,6 +14,6 @@
     INConditionalOperatorAll = 0,
     INConditionalOperatorAny,
     INConditionalOperatorNone,
-};
+} API_AVAILABLE(macosx(10.12), ios(10.0));
 
 #endif // INConditionalOperator_h
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRange.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRange.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRange.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRange.h	2016-07-12 07:04:02.000000000 +0200
@@ -9,6 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INDateComponentsRange : NSObject <NSCopying, NSSecureCoding>
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h	2016-07-12 07:04:02.000000000 +0200
@@ -11,6 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INDateComponentsRangeResolutionResult : INIntentResolutionResult
 
 // This resolution result is for when the app extension wants to tell Siri to proceed with a given date components range. The resolvedDateComponentsRange need not be identical to the input date components range. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INImage.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INImage.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INImage.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INImage.h	2016-07-12 07:04:02.000000000 +0200
@@ -11,6 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INImage : NSObject <NSCopying, NSSecureCoding>
 
 + (instancetype)imageNamed:(NSString *)name;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntent.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntent.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntent.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntent.h	2016-07-12 07:04:02.000000000 +0200
@@ -9,6 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INIntent : NSObject <NSCopying, NSSecureCoding>
 
 // Returns the identifier of the receiver.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentErrors.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentErrors.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentErrors.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentErrors.h	2016-07-12 07:04:02.000000000 +0200
@@ -9,12 +9,12 @@
 
 #import <Intents/IntentsDefines.h>
 
-INTENTS_EXTERN NSString * const INIntentErrorDomain;
+INTENTS_EXTERN NSString * const INIntentErrorDomain API_AVAILABLE(macosx(10.12), ios(10.0));
 
 typedef NS_ENUM(NSInteger, INIntentErrorCode) {
     // Interactions
     INIntentErrorInteractionOperationNotSupported = 1900,
-    INIntentErrorAddingInteraction = 1901,
+    INIntentErrorDonatingInteraction = 1901,
     INIntentErrorDeletingAllInteractions = 1902,
     INIntentErrorDeletingInteractionWithIdentifiers = 1903,
     INIntentErrorDeletingInteractionWithGroupIdentifier = 1904,
@@ -28,4 +28,6 @@
     // Requests
     INIntentErrorRequestTimedOut = 3001,
     
-};
+    // User Vocabulary Sync
+    INIntentErrorInvalidUserVocabularyFileLocation = 4000,
+} API_AVAILABLE(macosx(10.12), ios(10.0));
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h	2016-07-12 07:04:02.000000000 +0200
@@ -9,6 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INIntentResolutionResult<ObjectType> : NSObject
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResponse.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResponse.h	2016-07-12 07:04:02.000000000 +0200
@@ -9,6 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INIntentResponse : NSObject <NSCopying, NSSecureCoding>
 
 // This user activity will be used to launch the containing application when host application finds appropriate or when users request so.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h	2016-07-12 07:04:02.000000000 +0200
@@ -18,13 +18,13 @@
     INIntentHandlingStatusFailure,
     INIntentHandlingStatusDeferredToApplication,
     INIntentHandlingStatusDone = INIntentHandlingStatusSuccess, // Deprecated - please use 'Success' and 'Failure'.
-} NS_ENUM_AVAILABLE(10_12, 10_0);
+} API_AVAILABLE(macosx(10.12), ios(10.0));
 
 typedef NS_ENUM(NSInteger, INInteractionDirection) {
     INInteractionDirectionUnspecified = 0,
     INInteractionDirectionOutgoing,
     INInteractionDirectionIncoming,
-} NS_ENUM_AVAILABLE(10_12, 10_0);
+} API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -34,6 +34,7 @@
  The system may also launch the app with an NSUserActivity containing an INInteraction such that the app can perform the action if it chooses.
 */
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INInteraction : NSObject <NSSecureCoding, NSCopying>
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessage.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessage.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessage.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessage.h	2016-07-12 07:04:02.000000000 +0200
@@ -11,6 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INMessage : NSObject <NSCopying, NSSecureCoding>
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h	2016-07-11 07:06:19.000000000 +0200
@@ -12,6 +12,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INPerson : NSObject <NSCopying, NSSecureCoding>
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h	2016-07-12 07:04:02.000000000 +0200
@@ -11,10 +11,11 @@
     INPersonHandleTypeUnknown = 0,
     INPersonHandleTypeEmailAddress,
     INPersonHandleTypePhoneNumber,
-};
+} API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INPersonHandle : NSObject <NSCopying, NSSecureCoding>
 
 @property (readonly, copy, NS_NONATOMIC_IOSONLY) NSString *value;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h	2016-07-12 07:04:02.000000000 +0200
@@ -11,6 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INPersonResolutionResult : INIntentResolutionResult
 
 // This resolution result is for when the app extension wants to tell Siri to proceed with a given person. The resolvedPerson need not be identical to the input person. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h	2016-07-12 07:04:02.000000000 +0200
@@ -0,0 +1,31 @@
+//
+//  INPlacemarkResolutionResult.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Intents/INIntentResolutionResult.h>
+
+@class CLPlacemark;
+
+NS_ASSUME_NONNULL_BEGIN
+
+API_AVAILABLE(macosx(10.12), ios(10.0))
+@interface INPlacemarkResolutionResult : INIntentResolutionResult
+
+// This resolution result is for when the app extension wants to tell Siri to proceed with a given placemark. The resolvedPlacemark need not be identical to the input placemark. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
++ (instancetype)successWithResolvedPlacemark:(CLPlacemark *)resolvedPlacemark NS_SWIFT_NAME(success(with:));
+
+// This resolution result is to ask Siri to disambiguate between the provided placemarks.
++ (instancetype)disambiguationWithPlacemarksToDisambiguate:(NSArray<CLPlacemark *> *)placemarksToDisambiguate NS_SWIFT_NAME(disambiguation(with:));
+
+// This resolution result is to ask Siri to confirm if this is the placemark with which the user wants to continue.
++ (instancetype)confirmationRequiredWithPlacemarkToConfirm:(nullable CLPlacemark *)placemarkToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
+
+// This resolution result is to inform Siri that in order to continue, the app extension needs the placemark to be filled in greater detail. If this parameter is nil and the app extension wants to request a non-nil value, it should use +needsValue.
++ (instancetype)needsMoreDetailsForPlacemark:(CLPlacemark *)placemarkToComplete NS_SWIFT_NAME(needsMoreDetails(for:));
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h	2016-07-12 07:04:02.000000000 +0200
@@ -13,7 +13,7 @@
     INSearchCallHistoryIntentResponseCodeContinueInApp,
     INSearchCallHistoryIntentResponseCodeFailure,
     INSearchCallHistoryIntentResponseCodeFailureRequiringAppLaunch,
-};
+} API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntentResponse.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntentResponse.h	2016-07-12 07:04:02.000000000 +0200
@@ -17,7 +17,7 @@
     INSearchForMessagesIntentResponseCodeFailure,
     INSearchForMessagesIntentResponseCodeFailureRequiringAppLaunch,
     INSearchForMessagesIntentResponseCodeFailureMessageServiceNotAvailable,
-};
+} API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h	2016-07-12 07:04:02.000000000 +0200
@@ -14,7 +14,7 @@
     INSendMessageIntentResponseCodeSuccess,
     INSendMessageIntentResponseCodeFailure,
     INSendMessageIntentResponseCodeFailureRequiringAppLaunch,
-};
+} API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h	2016-07-12 07:04:02.000000000 +0200
@@ -11,6 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INSpeakableString : NSObject <INSpeakable>
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h	2016-07-12 07:04:02.000000000 +0200
@@ -11,6 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INSpeakableStringResolutionResult : INIntentResolutionResult
 
 // This resolution result is for when the app extension wants to tell Siri to proceed with a given string. The resolvedString need not be identical to the input string. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h	2016-07-12 07:04:02.000000000 +0200
@@ -13,7 +13,7 @@
     INStartAudioCallIntentResponseCodeContinueInApp,
     INStartAudioCallIntentResponseCodeFailure,
     INStartAudioCallIntentResponseCodeFailureRequiringAppLaunch,
-};
+} API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h	2016-07-12 07:04:02.000000000 +0200
@@ -13,7 +13,7 @@
     INStartVideoCallIntentResponseCodeContinueInApp,
     INStartVideoCallIntentResponseCodeFailure,
     INStartVideoCallIntentResponseCodeFailureRequiringAppLaunch,
-};
+} API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h	2016-07-12 07:04:02.000000000 +0200
@@ -9,6 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INStringResolutionResult : INIntentResolutionResult
 
 // This resolution result is for when the app extension wants to tell Siri to proceed with a given string. The resolvedString need not be identical to the input string. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h	2016-07-12 07:04:02.000000000 +0200
@@ -35,6 +35,7 @@
 // Common Resolution Results
 #import <Intents/INDateComponentsRangeResolutionResult.h>
 #import <Intents/INPersonResolutionResult.h>
+#import <Intents/INPlacemarkResolutionResult.h>
 #import <Intents/INSpeakableStringResolutionResult.h>
 #import <Intents/INStringResolutionResult.h>
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/NSUserActivity+IntentsAdditions.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/NSUserActivity+IntentsAdditions.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/NSUserActivity+IntentsAdditions.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/NSUserActivity+IntentsAdditions.h	2016-07-12 07:04:02.000000000 +0200
@@ -13,7 +13,7 @@
 
 @interface NSUserActivity (IntentsAdditions)
 
-@property (readonly, nullable, NS_NONATOMIC_IOSONLY) INInteraction *interaction;
+@property (readonly, nullable, NS_NONATOMIC_IOSONLY) INInteraction *interaction API_AVAILABLE(macosx(10.12), ios(10.0));
 
 @end
 

```