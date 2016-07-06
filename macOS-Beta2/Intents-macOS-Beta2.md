#Intents.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/CLPlacemark+IntentsAdditions.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/CLPlacemark+IntentsAdditions.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/CLPlacemark+IntentsAdditions.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/CLPlacemark+IntentsAdditions.h	2016-06-28 04:49:12.000000000 +0200
@@ -6,16 +6,17 @@
 //
 
 #import <Foundation/Foundation.h>
-
 #import <CoreLocation/CLPlacemark.h>
 
+@class CNPostalAddress;
+
 NS_ASSUME_NONNULL_BEGIN
 
-@interface CLPlacemark (IntentsAdditions)
+@interface CLPlacemark (INIntentsAdditions)
 
-- (instancetype)initIntentPlacemarkWithLocation:(CLLocation *)location
-                              addressDictionary:(nullable NSDictionary<NSString *, id> *)addressDictionary
-NS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_AVAILABLE(3_0);
++ (instancetype)placemarkWithLocation:(CLLocation *)location
+                                 name:(nullable NSString *)name
+                        postalAddress:(nullable CNPostalAddress *)postalAddress API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx, watchos, tvos);
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h	2016-06-28 04:49:12.000000000 +0200
@@ -6,7 +6,6 @@
 //
 
 #import <Intents/INIntentResolutionResult.h>
-#import <Intents/INIntentResolutionResultUnsupportedReason.h>
 
 @class INDateComponentsRange;
 
@@ -26,10 +25,6 @@
 // This resolution result is to inform Siri that in order to continue, the app extension needs the date components range to be filled in greater detail. If this parameter is nil and the app extension wants to request a non-nil value, it should use +needsValue.
 + (instancetype)needsMoreDetailsForDateComponentsRange:(INDateComponentsRange *)dateComponentsRangeToComplete NS_SWIFT_NAME(needsMoreDetails(for:));
 
-// This resolution result is the same as +unsupportedWithReason:, but allows the app extension to provide alternate / suggested date components ranges.
-+ (instancetype)unsupportedWithReason:(INIntentResolutionResultUnsupportedReason)reason
-           alternativeDateComponentsRanges:(NSArray<INDateComponentsRange *> *)alternativeDateComponentsRanges NS_SWIFT_NAME(unsupported(with:alternativeDateComponentsRanges:));
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentErrors.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentErrors.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentErrors.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentErrors.h	2016-06-28 04:49:12.000000000 +0200
@@ -19,11 +19,13 @@
     INIntentErrorDeletingInteractionWithIdentifiers = 1903,
     INIntentErrorDeletingInteractionWithGroupIdentifier = 1904,
     
-    // Extension discovery
+    // Extension discovery / info plist validation
     INIntentErrorIntentSupportedByMultipleExtension = 2001,
     INIntentErrorRestrictedIntentsNotSupportedByExtension = 2002,
     INIntentErrorNoHandlerProvidedForIntent = 2003,
+    INIntentErrorInvalidIntentName = 2004,
     
     // Requests
     INIntentErrorRequestTimedOut = 3001,
+    
 };
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h	2016-06-28 04:49:12.000000000 +0200
@@ -7,8 +7,6 @@
 
 #import <Foundation/Foundation.h>
 
-#import <Intents/INIntentResolutionResultUnsupportedReason.h>
-
 NS_ASSUME_NONNULL_BEGIN
 
 @interface INIntentResolutionResult<ObjectType> : NSObject
@@ -22,8 +20,8 @@
 // This result is to tell Siri to continue whether or the user has provided a value for this parameter
 + (instancetype)notRequired NS_SWIFT_NAME(notRequired());
 
-// This result is for informing Siri that this value is unsupported due to the specified reason, Siri may use this reason to craft an appropriate response dialog
-+ (instancetype)unsupportedWithReason:(INIntentResolutionResultUnsupportedReason)reason NS_SWIFT_NAME(unsupported(with:));
+// This result is for informing Siri that this value is unsupported
++ (instancetype)unsupported NS_SWIFT_NAME(unsupported());
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResultUnsupportedReason.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResultUnsupportedReason.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResultUnsupportedReason.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResultUnsupportedReason.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,23 +0,0 @@
-//
-//  INIntentResolutionResultUnsupportedReason.h
-//  Intents
-//
-//  Copyright © 2016 Apple. All rights reserved.
-//
-
-#ifndef INIntentResolutionResultUnsupportedReason_h
-#define INIntentResolutionResultUnsupportedReason_h
-
-#import <Foundation/Foundation.h>
-
-#import <Intents/IntentsDefines.h>
-
-typedef NS_ENUM(NSInteger, INIntentResolutionResultUnsupportedReason) {
-    INIntentResolutionResultUnsupportedReasonUnknown = 0,
-    INIntentResolutionResultUnsupportedReasonNone,
-    INIntentResolutionResultUnsupportedReasonNotNow,
-    INIntentResolutionResultUnsupportedReasonNotHere,
-    INIntentResolutionResultUnsupportedReasonConflictWithOtherFields,
-};
-
-#endif // INIntentResolutionResultUnsupportedReason_h
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h	2016-06-28 04:49:12.000000000 +0200
@@ -14,7 +14,10 @@
     INIntentHandlingStatusUnspecified = 0,
     INIntentHandlingStatusReady,
     INIntentHandlingStatusInProgress,
-    INIntentHandlingStatusDone,
+    INIntentHandlingStatusSuccess,
+    INIntentHandlingStatusFailure,
+    INIntentHandlingStatusDeferredToApplication,
+    INIntentHandlingStatusDone = INIntentHandlingStatusSuccess, // Deprecated - please use 'Success' and 'Failure'.
 } NS_ENUM_AVAILABLE(10_12, 10_0);
 
 typedef NS_ENUM(NSInteger, INInteractionDirection) {
@@ -37,23 +40,23 @@
 - (instancetype)initWithIntent:(INIntent *)intent response:(nullable INIntentResponse *)response NS_DESIGNATED_INITIALIZER;
 
 // donate this interaction to the system
-- (void)donateInteractionWithCompletion:(void(^_Nullable)(NSError * _Nullable error))completion;
+- (void)donateInteractionWithCompletion:(void(^_Nullable)(NSError * _Nullable error))completion NS_SWIFT_NAME(donate(completion:));
 
 // delete all the interactions ever donated by the calling app
-+ (void)deleteAllInteractionsWithCompletion:(void (^_Nullable)(NSError * _Nullable error))completion;
++ (void)deleteAllInteractionsWithCompletion:(void (^_Nullable)(NSError * _Nullable error))completion NS_SWIFT_NAME(deleteAll(completion:));
 
 // delete the interactions with the specified identifiers that were donated by this app
-+ (void)deleteInteractionsWithIdentifiers:(nonnull NSArray<NSString *> *)identifiers completion:(void(^_Nullable)(NSError * _Nullable error))completion;
++ (void)deleteInteractionsWithIdentifiers:(nonnull NSArray<NSString *> *)identifiers completion:(void(^_Nullable)(NSError * _Nullable error))completion NS_SWIFT_NAME(delete(with:completion:));
 
 // delete this app's interactions with the specified group identifier
-+ (void)deleteInteractionsWithGroupIdentifier:(nonnull NSString *)groupIdentifier completion:(void(^_Nullable)(NSError * _Nullable error))completion;
++ (void)deleteInteractionsWithGroupIdentifier:(nonnull NSString *)groupIdentifier completion:(void(^_Nullable)(NSError * _Nullable error))completion NS_SWIFT_NAME(delete(with:completion:));
 
 @property (readonly, copy, NS_NONATOMIC_IOSONLY) INIntent *intent;
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INIntentResponse *intentResponse;
 
 // Indicates the state of execution of the intent
 // This is consistent with the response state of the intentResponse, if specified
-@property (assign, NS_NONATOMIC_IOSONLY) INIntentHandlingStatus intentHandlingStatus;
+@property (readonly, NS_NONATOMIC_IOSONLY) INIntentHandlingStatus intentHandlingStatus;
 
 // Indicates the direction of the interaction
 @property (assign, NS_NONATOMIC_IOSONLY) INInteractionDirection direction;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageService.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageService.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageService.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageService.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,32 +0,0 @@
-//
-//  INMessageService.h
-//  Intents
-//
-//  Copyright © 2016 Apple. All rights reserved.
-//
-
-#import <Foundation/Foundation.h>
-
-#import <Intents/IntentsDefines.h>
-
-typedef NSString * INMessageServiceName NS_EXTENSIBLE_STRING_ENUM;
-
-INTENTS_EXTERN INMessageServiceName const INMessageServiceNameiMessage NS_SWIFT_NAME(INMessageServiceName.iMessage);
-INTENTS_EXTERN INMessageServiceName const INMessageServiceNameSMS;
-INTENTS_EXTERN INMessageServiceName const INMessageServiceNameJabber;
-INTENTS_EXTERN INMessageServiceName const INMessageServiceNameAIM;
-INTENTS_EXTERN INMessageServiceName const INMessageServiceNameFacebook NS_SWIFT_NAME(INMessageServiceName.Facebook);
-INTENTS_EXTERN INMessageServiceName const INMessageServiceNameGaduGadu NS_SWIFT_NAME(INMessageServiceName.GaduGadu);
-INTENTS_EXTERN INMessageServiceName const INMessageServiceNameHangouts NS_SWIFT_NAME(INMessageServiceName.Hangouts);
-INTENTS_EXTERN INMessageServiceName const INMessageServiceNameICQ NS_SWIFT_NAME(INMessageServiceName.ICQ);
-INTENTS_EXTERN INMessageServiceName const INMessageServiceNameKakaoTalk NS_SWIFT_NAME(INMessageServiceName.KakaoTalk);
-INTENTS_EXTERN INMessageServiceName const INMessageServiceNameKik NS_SWIFT_NAME(INMessageServiceName.Kik);
-INTENTS_EXTERN INMessageServiceName const INMessageServiceNameLINE;
-INTENTS_EXTERN INMessageServiceName const INMessageServiceNameMSN;
-INTENTS_EXTERN INMessageServiceName const INMessageServiceNameQQ;
-INTENTS_EXTERN INMessageServiceName const INMessageServiceNameSkype NS_SWIFT_NAME(INMessageServiceName.Skype);
-INTENTS_EXTERN INMessageServiceName const INMessageServiceNameSnapchat NS_SWIFT_NAME(INMessageServiceName.Snapchat);
-INTENTS_EXTERN INMessageServiceName const INMessageServiceNameTwitter NS_SWIFT_NAME(INMessageServiceName.Twitter);
-INTENTS_EXTERN INMessageServiceName const INMessageServiceNameWeChat NS_SWIFT_NAME(INMessageServiceName.WeChat);
-INTENTS_EXTERN INMessageServiceName const INMessageServiceNameWhatsApp NS_SWIFT_NAME(INMessageServiceName.WhatsApp);
-INTENTS_EXTERN INMessageServiceName const INMessageServiceNameYahoo NS_SWIFT_NAME(INMessageServiceName.Yahoo);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h	2016-06-28 04:49:12.000000000 +0200
@@ -8,6 +8,7 @@
 #import <Foundation/Foundation.h>
 
 @class INImage;
+@class INPersonHandle;
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -15,14 +16,18 @@
 
 - (instancetype)init NS_UNAVAILABLE;
 
-- (instancetype)initWithHandle:(NSString *)handle
+- (instancetype)initWithPersonHandle:(INPersonHandle *)personHandle
                 nameComponents:(nullable NSPersonNameComponents *)nameComponents
                    displayName:(nullable NSString *)displayName
                          image:(nullable INImage *)image
-             contactIdentifier:(nullable NSString *)contactIdentifier NS_DESIGNATED_INITIALIZER;
+             contactIdentifier:(nullable NSString *)contactIdentifier
+              customIdentifier:(nullable NSString *)customIdentifier NS_DESIGNATED_INITIALIZER;
 
 // The identity of the person in the application (e.g. email address, phone number, user handle, etc.)
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *handle;
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *handle  NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use personHandle instead");
+
+// The identity of the person in the application
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INPersonHandle *personHandle;
 
 // Returns the person's name components if this was initialized with them
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSPersonNameComponents *nameComponents;
@@ -33,10 +38,12 @@
 // Returns an image for the person.
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INImage *image;
 
-// Reference to this person, if present in the Contacts database
-// During intent resolution, an app extension can use this property to set a custom indentifier
+// Reference to this person, if present in the system's Contacts store
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *contactIdentifier;
 
+// This property can be set to the app's identifier for this person
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *customIdentifier;
+
 @end
 
 @interface INPerson (INPersonCreation)
@@ -44,12 +51,42 @@
 //  This is the preferred convenience initializer if the app knows the name components of the person (e.g. given name, family name, etc).
 - (instancetype)initWithHandle:(NSString *)handle
                 nameComponents:(NSPersonNameComponents *)nameComponents
-             contactIdentifier:(nullable NSString *)contactIdentifier;
+             contactIdentifier:(nullable NSString *)contactIdentifier NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use the designated initializer instead");
 
 // Use this convenience initializer if the person's name is unknown
 - (instancetype)initWithHandle:(NSString *)handle
                    displayName:(nullable NSString *)displayName
-             contactIdentifier:(nullable NSString *)contactIdentifier;
+             contactIdentifier:(nullable NSString *)contactIdentifier NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use the designated initializer instead");
+
+- (instancetype)initWithHandle:(NSString *)handle
+                nameComponents:(nullable NSPersonNameComponents *)nameComponents
+                   displayName:(nullable NSString *)displayName
+                         image:(nullable INImage *)image
+             contactIdentifier:(nullable NSString *)contactIdentifier NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use the designated initializer instead");
+
+@end
+
+typedef NS_ENUM(NSInteger, INPersonSuggestionType) {
+    INPersonSuggestionTypeSocialProfile = 1,
+    INPersonSuggestionTypeInstantMessageAddress
+};
+
+@interface INPerson (INInteraction)
+
+// If your application has other representations for the person's handle, you can supply it for INInteraction donation
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSArray<INPersonHandle *> *aliases;
+
+// What Contact property this INInteraction donation should be suggested as when this person is matched to a contact in the system's Contacts store.
+@property (readonly, NS_NONATOMIC_IOSONLY) INPersonSuggestionType suggestionType;
+
+- (instancetype)initWithPersonHandle:(INPersonHandle *)personHandle
+                nameComponents:(nullable NSPersonNameComponents *)nameComponents
+                   displayName:(nullable NSString *)displayName
+                         image:(nullable INImage *)image
+             contactIdentifier:(nullable NSString *)contactIdentifier
+              customIdentifier:(nullable NSString *)customIdentifier
+                       aliases:(nullable NSArray<INPersonHandle *> *)aliases
+                suggestionType:(INPersonSuggestionType)suggestionType;
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h	2016-06-28 04:49:12.000000000 +0200
@@ -0,0 +1,28 @@
+//
+//  INPersonHandle.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+typedef NS_ENUM(NSInteger, INPersonHandleType) {
+    INPersonHandleTypeUnknown = 0,
+    INPersonHandleTypeEmailAddress,
+    INPersonHandleTypePhoneNumber,
+};
+
+NS_ASSUME_NONNULL_BEGIN
+
+@interface INPersonHandle : NSObject <NSCopying, NSSecureCoding>
+
+@property (readonly, copy, NS_NONATOMIC_IOSONLY) NSString *value;
+@property (readonly, NS_NONATOMIC_IOSONLY) INPersonHandleType type;
+
+- (instancetype)init NS_UNAVAILABLE;
+- (instancetype)initWithValue:(NSString *)value type:(INPersonHandleType)type NS_DESIGNATED_INITIALIZER;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h	2016-06-28 04:49:12.000000000 +0200
@@ -6,7 +6,6 @@
 //
 
 #import <Intents/INIntentResolutionResult.h>
-#import <Intents/INIntentResolutionResultUnsupportedReason.h>
 
 @class INPerson;
 
@@ -26,10 +25,6 @@
 // This resolution result is to inform Siri that in order to continue, the app extension needs the person to be filled in greater detail. If this parameter is nil and the app extension wants to request a non-nil value, it should use +needsValue.
 + (instancetype)needsMoreDetailsForPerson:(INPerson *)personToComplete NS_SWIFT_NAME(needsMoreDetails(for:));
 
-// This resolution result is the same as +unsupportedWithReason:, but allows the app extension to provide alternate / suggested people.
-+ (instancetype)unsupportedWithReason:(INIntentResolutionResultUnsupportedReason)reason
-                    alternativePeople:(NSArray<INPerson *> *)alternativePeople NS_SWIFT_NAME(unsupported(with:alternativePeople:));
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h	2016-06-26 09:15:29.000000000 +0200
@@ -20,6 +20,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INSearchCallHistoryIntent : INIntent
 
 - (instancetype)initWithCallType:(INCallRecordType)callType
@@ -47,6 +48,7 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @protocol INSearchCallHistoryIntentHandling <NSObject>
 
 @required
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h	2016-06-28 04:49:12.000000000 +0200
@@ -9,14 +9,15 @@
 
 typedef NS_ENUM(NSInteger, INSearchCallHistoryIntentResponseCode) {
     INSearchCallHistoryIntentResponseCodeUnspecified = 0,
-    INSearchCallHistoryIntentResponseCodeInProgress,
-    INSearchCallHistoryIntentResponseCodeSuccess,
+    INSearchCallHistoryIntentResponseCodeReady,
+    INSearchCallHistoryIntentResponseCodeContinueInApp,
     INSearchCallHistoryIntentResponseCodeFailure,
     INSearchCallHistoryIntentResponseCodeFailureRequiringAppLaunch,
 };
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INSearchCallHistoryIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h	2016-06-26 09:15:29.000000000 +0200
@@ -20,6 +20,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INSearchForMessagesIntent : INIntent
 
 - (instancetype)initWithRecipients:(nullable NSArray<INPerson *> *)recipients
@@ -74,6 +75,7 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @protocol INSearchForMessagesIntentHandling <NSObject>
 
 @required
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntentResponse.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntentResponse.h	2016-06-28 04:49:12.000000000 +0200
@@ -11,14 +11,17 @@
 
 typedef NS_ENUM(NSInteger, INSearchForMessagesIntentResponseCode) {
     INSearchForMessagesIntentResponseCodeUnspecified = 0,
+    INSearchForMessagesIntentResponseCodeReady,
     INSearchForMessagesIntentResponseCodeInProgress,
     INSearchForMessagesIntentResponseCodeSuccess,
     INSearchForMessagesIntentResponseCodeFailure,
     INSearchForMessagesIntentResponseCodeFailureRequiringAppLaunch,
+    INSearchForMessagesIntentResponseCodeFailureMessageServiceNotAvailable,
 };
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INSearchForMessagesIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h	2016-06-26 09:14:37.000000000 +0200
@@ -14,6 +14,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INSendMessageIntent : INIntent
 
 - (instancetype)initWithRecipients:(nullable NSArray<INPerson *> *)recipients
@@ -46,6 +47,7 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @protocol INSendMessageIntentHandling <NSObject>
 
 @required
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h	2016-06-28 04:49:12.000000000 +0200
@@ -9,6 +9,7 @@
 
 typedef NS_ENUM(NSInteger, INSendMessageIntentResponseCode) {
     INSendMessageIntentResponseCodeUnspecified = 0,
+    INSendMessageIntentResponseCodeReady,
     INSendMessageIntentResponseCodeInProgress,
     INSendMessageIntentResponseCodeSuccess,
     INSendMessageIntentResponseCodeFailure,
@@ -17,6 +18,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INSendMessageIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakable.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakable.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakable.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakable.h	2016-06-28 04:49:12.000000000 +0200
@@ -0,0 +1,16 @@
+//
+//  INSpeakable.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+@protocol INSpeakable <NSObject>
+
+@property (readonly, nullable, NS_NONATOMIC_IOSONLY) NSString *spokenPhrase;
+@property (readonly, nullable, NS_NONATOMIC_IOSONLY) NSString *pronunciationHint;
+@property (readonly, nullable, NS_NONATOMIC_IOSONLY) NSString *identifier;
+
+@end
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h	2016-06-28 04:49:12.000000000 +0200
@@ -0,0 +1,24 @@
+//
+//  INSpeakableString.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+#import <Intents/INSpeakable.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@interface INSpeakableString : NSObject <INSpeakable>
+
+- (instancetype)init NS_UNAVAILABLE;
+- (instancetype)initWithIdentifier:(NSString *)identifier
+                   spokenPhrase:(NSString *)spokenPhrase
+                   pronunciationHint:(nullable NSString *)pronunciationHint NS_DESIGNATED_INITIALIZER;
+
+@end
+
+NS_ASSUME_NONNULL_END
+
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h	2016-06-28 04:49:12.000000000 +0200
@@ -0,0 +1,27 @@
+//
+//  INSpeakableStringResolutionResult.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Intents/INIntentResolutionResult.h>
+
+@class INSpeakableString;
+
+NS_ASSUME_NONNULL_BEGIN
+
+@interface INSpeakableStringResolutionResult : INIntentResolutionResult
+
+// This resolution result is for when the app extension wants to tell Siri to proceed with a given string. The resolvedString need not be identical to the input string. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
++ (instancetype)successWithResolvedString:(INSpeakableString *)resolvedString NS_SWIFT_NAME(success(with:));
+
+// This resolution result is to ask Siri to disambiguate between the provided strings.
++ (instancetype)disambiguationWithStringsToDisambiguate:(NSArray<INSpeakableString *> *)stringsToDisambiguate NS_SWIFT_NAME(disambiguation(with:));
+
+// This resolution result is to ask Siri to confirm if this is the string with which the user wants to continue.
++ (instancetype)confirmationRequiredWithStringToConfirm:(nullable INSpeakableString *)stringToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntent.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntent.h	2016-06-28 04:49:12.000000000 +0200
@@ -13,6 +13,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INStartAudioCallIntent : INIntent
 
 - (instancetype)initWithContacts:(nullable NSArray<INPerson *> *)contacts NS_DESIGNATED_INITIALIZER;
@@ -30,6 +31,7 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @protocol INStartAudioCallIntentHandling <NSObject>
 
 @required
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h	2016-06-28 04:49:12.000000000 +0200
@@ -9,14 +9,15 @@
 
 typedef NS_ENUM(NSInteger, INStartAudioCallIntentResponseCode) {
     INStartAudioCallIntentResponseCodeUnspecified = 0,
-    INStartAudioCallIntentResponseCodeInProgress,
-    INStartAudioCallIntentResponseCodeSuccess,
+    INStartAudioCallIntentResponseCodeReady,
+    INStartAudioCallIntentResponseCodeContinueInApp,
     INStartAudioCallIntentResponseCodeFailure,
     INStartAudioCallIntentResponseCodeFailureRequiringAppLaunch,
 };
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INStartAudioCallIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntent.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntent.h	2016-06-28 04:49:12.000000000 +0200
@@ -13,6 +13,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INStartVideoCallIntent : INIntent
 
 - (instancetype)initWithContacts:(nullable NSArray<INPerson *> *)contacts NS_DESIGNATED_INITIALIZER;
@@ -30,6 +31,7 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @protocol INStartVideoCallIntentHandling <NSObject>
 
 @required
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h	2016-06-28 04:49:12.000000000 +0200
@@ -9,14 +9,15 @@
 
 typedef NS_ENUM(NSInteger, INStartVideoCallIntentResponseCode) {
     INStartVideoCallIntentResponseCodeUnspecified = 0,
-    INStartVideoCallIntentResponseCodeInProgress,
-    INStartVideoCallIntentResponseCodeSuccess,
+    INStartVideoCallIntentResponseCodeReady,
+    INStartVideoCallIntentResponseCodeContinueInApp,
     INStartVideoCallIntentResponseCodeFailure,
     INStartVideoCallIntentResponseCodeFailureRequiringAppLaunch,
 };
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INStartVideoCallIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h	2016-06-28 04:49:12.000000000 +0200
@@ -6,7 +6,6 @@
 //
 
 #import <Intents/INIntentResolutionResult.h>
-#import <Intents/INIntentResolutionResultUnsupportedReason.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -21,10 +20,6 @@
 // This resolution result is to ask Siri to confirm if this is the string with which the user wants to continue.
 + (instancetype)confirmationRequiredWithStringToConfirm:(nullable NSString *)stringToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
 
-// This resolution result is the same as +unsupportedWithReason:, but allows the app extension to provide alternate / suggested strings.
-+ (instancetype)unsupportedWithReason:(INIntentResolutionResultUnsupportedReason)reason
-                   alternativeStrings:(NSArray<NSString *> *)alternativeStrings NS_SWIFT_NAME(unsupported(with:alternativeStrings:));
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h	2016-06-28 04:49:12.000000000 +0200
@@ -22,17 +22,20 @@
 #import <Intents/INIntentErrors.h>
 #import <Intents/INIntentResponse.h>
 #import <Intents/INIntentResolutionResult.h>
-#import <Intents/INIntentResolutionResultUnsupportedReason.h>
 #import <Intents/INInteraction.h>
+#import <Intents/INSpeakable.h>
 
 // Common Types
+#import <Intents/INPersonHandle.h>
 #import <Intents/INDateComponentsRange.h>
 #import <Intents/INImage.h>
 #import <Intents/INPerson.h>
+#import <Intents/INSpeakableString.h>
 
 // Common Resolution Results
 #import <Intents/INDateComponentsRangeResolutionResult.h>
 #import <Intents/INPersonResolutionResult.h>
+#import <Intents/INSpeakableStringResolutionResult.h>
 #import <Intents/INStringResolutionResult.h>
 
 // Calls Domain
@@ -57,7 +60,6 @@
 #import <Intents/INMessage.h>
 #import <Intents/INMessageAttributeOptions.h>
 #import <Intents/INMessageAttributeOptionsResolutionResult.h>
-#import <Intents/INMessageService.h>
 
 // Utilities
 #import <Intents/CLPlacemark+IntentsAdditions.h>

```