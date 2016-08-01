#Intents.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INCallCapabilityOptionsResolutionResult.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INCallCapabilityOptionsResolutionResult.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INCallCapabilityOptionsResolutionResult.h	2016-07-12 07:04:02.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INCallCapabilityOptionsResolutionResult.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,24 +0,0 @@
-//
-//  INCallCapabilityOptionsResolutionResult.h
-//  Intents
-//
-//  Copyright © 2016 Apple. All rights reserved.
-//
-
-#import <Intents/INIntentResolutionResult.h>
-
-#import <Intents/INCallCapabilityOptions.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-@interface INCallCapabilityOptionsResolutionResult : INIntentResolutionResult
-
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
-+ (instancetype)successWithResolvedValue:(INCallCapabilityOptions)resolvedValue NS_SWIFT_NAME(success(with:));
-
-// This resolution result is to ask Siri to confirm if this is the value with which the user wants to continue.
-+ (instancetype)confirmationRequiredWithValueToConfirm:(INCallCapabilityOptions)valueToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h	2016-07-12 07:04:02.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h	2016-07-23 21:09:47.000000000 +0200
@@ -23,9 +23,6 @@
 // This resolution result is to ask Siri to confirm if this is the date components range with which the user wants to continue.
 + (instancetype)confirmationRequiredWithDateComponentsRangeToConfirm:(nullable INDateComponentsRange *)dateComponentsRangeToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
 
-// This resolution result is to inform Siri that in order to continue, the app extension needs the date components range to be filled in greater detail. If this parameter is nil and the app extension wants to request a non-nil value, it should use +needsValue.
-+ (instancetype)needsMoreDetailsForDateComponentsRange:(INDateComponentsRange *)dateComponentsRangeToComplete NS_SWIFT_NAME(needsMoreDetails(for:));
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h	2016-07-12 07:04:02.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h	2016-07-23 21:09:47.000000000 +0200
@@ -15,7 +15,6 @@
 - (instancetype)init NS_UNAVAILABLE;
 
 // This result is to tell Siri that the user must provide a non-nil value for this parameter in order to continue
-// If the current value of this parameter is already non-nil, but the app extension wants to request more details, it can indicate this using +resolutionResultNeedsMoreDetails
 + (instancetype)needsValue NS_SWIFT_NAME(needsValue());
 
 // This result is to tell Siri to continue whether or the user has provided a value for this parameter
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h	2016-07-12 07:04:02.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h	2016-07-23 21:09:47.000000000 +0200
@@ -17,7 +17,6 @@
     INIntentHandlingStatusSuccess,
     INIntentHandlingStatusFailure,
     INIntentHandlingStatusDeferredToApplication,
-    INIntentHandlingStatusDone = INIntentHandlingStatusSuccess, // Deprecated - please use 'Success' and 'Failure'.
 } API_AVAILABLE(macosx(10.12), ios(10.0));
 
 typedef NS_ENUM(NSInteger, INInteractionDirection) {
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h	2016-07-12 07:04:02.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h	2016-07-23 21:09:47.000000000 +0200
@@ -23,9 +23,6 @@
 // This resolution result is to ask Siri to confirm if this is the person with which the user wants to continue.
 + (instancetype)confirmationRequiredWithPersonToConfirm:(nullable INPerson *)personToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
 
-// This resolution result is to inform Siri that in order to continue, the app extension needs the person to be filled in greater detail. If this parameter is nil and the app extension wants to request a non-nil value, it should use +needsValue.
-+ (instancetype)needsMoreDetailsForPerson:(INPerson *)personToComplete NS_SWIFT_NAME(needsMoreDetails(for:));
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h	2016-07-12 07:04:02.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h	2016-07-23 21:09:47.000000000 +0200
@@ -23,9 +23,6 @@
 // This resolution result is to ask Siri to confirm if this is the placemark with which the user wants to continue.
 + (instancetype)confirmationRequiredWithPlacemarkToConfirm:(nullable CLPlacemark *)placemarkToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
 
-// This resolution result is to inform Siri that in order to continue, the app extension needs the placemark to be filled in greater detail. If this parameter is nil and the app extension wants to request a non-nil value, it should use +needsValue.
-+ (instancetype)needsMoreDetailsForPlacemark:(CLPlacemark *)placemarkToComplete NS_SWIFT_NAME(needsMoreDetails(for:));
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h	2016-07-23 21:09:47.000000000 +0200
@@ -16,7 +16,6 @@
 @class INDateComponentsRangeResolutionResult;
 @class INPerson;
 @class INPersonResolutionResult;
-@class INCallCapabilityOptionsResolutionResult;
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -106,9 +105,6 @@
 - (void)resolveRecipientForSearchCallHistory:(INSearchCallHistoryIntent *)intent
                               withCompletion:(void (^)(INPersonResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveRecipient(forSearchCallHistory:with:));
 
-- (void)resolveCallCapabilitiesForSearchCallHistory:(INSearchCallHistoryIntent *)intent
-                                     withCompletion:(void (^)(INCallCapabilityOptionsResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveCallCapabilities(forSearchCallHistory:with:));
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h	2016-07-12 07:04:02.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h	2016-07-25 07:30:57.000000000 +0200
@@ -13,10 +13,10 @@
 
 @class INPerson;
 @class INPersonResolutionResult;
-@class INStringResolutionResult;
 @class INMessageAttributeOptionsResolutionResult;
 @class INDateComponentsRange;
 @class INDateComponentsRangeResolutionResult;
+@class INStringResolutionResult;
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -130,9 +130,6 @@
 - (void)resolveSendersForSearchForMessages:(INSearchForMessagesIntent *)intent
                             withCompletion:(void (^)(NSArray<INPersonResolutionResult *> *resolutionResults))completion NS_SWIFT_NAME(resolveSenders(forSearchForMessages:with:));
 
-- (void)resolveSearchTermsForSearchForMessages:(INSearchForMessagesIntent *)intent
-                                withCompletion:(void (^)(NSArray<INStringResolutionResult *> *resolutionResults))completion NS_SWIFT_NAME(resolveSearchTerms(forSearchForMessages:with:));
-
 - (void)resolveAttributesForSearchForMessages:(INSearchForMessagesIntent *)intent
                                withCompletion:(void (^)(INMessageAttributeOptionsResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveAttributes(forSearchForMessages:with:));
 
@@ -142,9 +139,6 @@
 - (void)resolveIdentifiersForSearchForMessages:(INSearchForMessagesIntent *)intent
                                 withCompletion:(void (^)(NSArray<INStringResolutionResult *> *resolutionResults))completion NS_SWIFT_NAME(resolveIdentifiers(forSearchForMessages:with:));
 
-- (void)resolveNotificationIdentifiersForSearchForMessages:(INSearchForMessagesIntent *)intent
-                                            withCompletion:(void (^)(NSArray<INStringResolutionResult *> *resolutionResults))completion NS_SWIFT_NAME(resolveNotificationIdentifiers(forSearchForMessages:with:));
-
 - (void)resolveGroupNamesForSearchForMessages:(INSearchForMessagesIntent *)intent
                                withCompletion:(void (^)(NSArray<INStringResolutionResult *> *resolutionResults))completion NS_SWIFT_NAME(resolveGroupNames(forSearchForMessages:with:));
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h	2016-07-25 07:26:52.000000000 +0200
@@ -105,12 +105,6 @@
 - (void)resolveGroupNameForSendMessage:(INSendMessageIntent *)intent
                         withCompletion:(void (^)(INStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveGroupName(forSendMessage:with:));
 
-- (void)resolveServiceNameForSendMessage:(INSendMessageIntent *)intent
-                          withCompletion:(void (^)(INStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveServiceName(forSendMessage:with:));
-
-- (void)resolveSenderForSendMessage:(INSendMessageIntent *)intent
-                     withCompletion:(void (^)(INPersonResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveSender(forSendMessage:with:));
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h	2016-07-12 07:04:02.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h	2016-07-23 21:09:47.000000000 +0200
@@ -14,6 +14,7 @@
     INSendMessageIntentResponseCodeSuccess,
     INSendMessageIntentResponseCodeFailure,
     INSendMessageIntentResponseCodeFailureRequiringAppLaunch,
+    INSendMessageIntentResponseCodeFailureMessageServiceNotAvailable,
 } API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h	2016-07-12 07:04:02.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h	2016-07-23 21:09:47.000000000 +0200
@@ -50,7 +50,6 @@
 #import <Intents/INCallRecordType.h>
 #import <Intents/INCallRecordTypeResolutionResult.h>
 #import <Intents/INCallCapabilityOptions.h>
-#import <Intents/INCallCapabilityOptionsResolutionResult.h>
 
 // Messages Domain
 #import <Intents/INSendMessageIntent.h>

```