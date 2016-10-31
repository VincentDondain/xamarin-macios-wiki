#Intents.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/CLPlacemark+IntentsAdditions.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/CLPlacemark+IntentsAdditions.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/CLPlacemark+IntentsAdditions.h	2016-07-31 15:18:11.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/CLPlacemark+IntentsAdditions.h	2016-10-24 05:25:49.000000000 +0200
@@ -16,7 +16,7 @@
 
 + (instancetype)placemarkWithLocation:(CLLocation *)location
                                  name:(nullable NSString *)name
-                        postalAddress:(nullable CNPostalAddress *)postalAddress API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx, watchos, tvos);
+                        postalAddress:(nullable CNPostalAddress *)postalAddress API_AVAILABLE(ios(10.0), watchos(3.1));
 
 @end
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INCallRecordTypeResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INCallRecordTypeResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INCallRecordTypeResolutionResult.h	2016-07-31 15:18:11.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INCallRecordTypeResolutionResult.h	2016-10-24 05:25:49.000000000 +0200
@@ -13,7 +13,8 @@
 
 @interface INCallRecordTypeResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INCallRecordType. The resolvedValue can be different than the original INCallRecordType. This allows app extensions to apply business logic constraints.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedValue:(INCallRecordType)resolvedValue NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to confirm if this is the value with which the user wants to continue.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h	2016-07-31 15:18:11.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h	2016-10-24 05:25:49.000000000 +0200
@@ -14,7 +14,8 @@
 API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INDateComponentsRangeResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given date components range. The resolvedDateComponentsRange need not be identical to the input date components range. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INDateComponentsRange. The resolvedDateComponentsRange can be different than the original INDateComponentsRange. This allows app extensions to pick a suitable range.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedDateComponentsRange:(INDateComponentsRange *)resolvedDateComponentsRange NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to disambiguate between the provided date components ranges.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageAttributeOptionsResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageAttributeOptionsResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageAttributeOptionsResolutionResult.h	2016-07-31 15:18:11.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageAttributeOptionsResolutionResult.h	2016-10-24 05:25:49.000000000 +0200
@@ -13,7 +13,8 @@
 
 @interface INMessageAttributeOptionsResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INMessageAttributeOptions. The resolvedValue can be different than the original INMessageAttributeOptions. This allows app extensions to apply business logic constraints.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedValue:(INMessageAttributeOptions)resolvedValue NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to confirm if this is the value with which the user wants to continue.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h	2016-07-31 15:18:11.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h	2016-10-24 05:25:49.000000000 +0200
@@ -7,6 +7,8 @@
 
 #import <Foundation/Foundation.h>
 
+#import <Intents/INPersonRelationship.h>
+
 @class INImage;
 @class INPersonHandle;
 
@@ -18,14 +20,11 @@
 - (instancetype)init NS_UNAVAILABLE;
 
 - (instancetype)initWithPersonHandle:(INPersonHandle *)personHandle
-                nameComponents:(nullable NSPersonNameComponents *)nameComponents
-                   displayName:(nullable NSString *)displayName
-                         image:(nullable INImage *)image
-             contactIdentifier:(nullable NSString *)contactIdentifier
-              customIdentifier:(nullable NSString *)customIdentifier NS_DESIGNATED_INITIALIZER;
-
-// The identity of the person in the application (e.g. email address, phone number, user handle, etc.)
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *handle  NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use personHandle instead");
+                      nameComponents:(nullable NSPersonNameComponents *)nameComponents
+                         displayName:(nullable NSString *)displayName
+                               image:(nullable INImage *)image
+                   contactIdentifier:(nullable NSString *)contactIdentifier
+                    customIdentifier:(nullable NSString *)customIdentifier NS_DESIGNATED_INITIALIZER;
 
 // The identity of the person in the application
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INPersonHandle *personHandle;
@@ -45,25 +44,8 @@
 // This property can be set to the app's identifier for this person
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *customIdentifier;
 
-@end
-
-@interface INPerson (INPersonCreation)
-
-//  This is the preferred convenience initializer if the app knows the name components of the person (e.g. given name, family name, etc).
-- (instancetype)initWithHandle:(NSString *)handle
-                nameComponents:(NSPersonNameComponents *)nameComponents
-             contactIdentifier:(nullable NSString *)contactIdentifier NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use the designated initializer instead");
-
-// Use this convenience initializer if the person's name is unknown
-- (instancetype)initWithHandle:(NSString *)handle
-                   displayName:(nullable NSString *)displayName
-             contactIdentifier:(nullable NSString *)contactIdentifier NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use the designated initializer instead");
-
-- (instancetype)initWithHandle:(NSString *)handle
-                nameComponents:(nullable NSPersonNameComponents *)nameComponents
-                   displayName:(nullable NSString *)displayName
-                         image:(nullable INImage *)image
-             contactIdentifier:(nullable NSString *)contactIdentifier NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use the designated initializer instead");
+// This person's relationship to the user
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INPersonRelationship relationship;
 
 @end
 
@@ -81,13 +63,13 @@
 @property (readonly, NS_NONATOMIC_IOSONLY) INPersonSuggestionType suggestionType;
 
 - (instancetype)initWithPersonHandle:(INPersonHandle *)personHandle
-                nameComponents:(nullable NSPersonNameComponents *)nameComponents
-                   displayName:(nullable NSString *)displayName
-                         image:(nullable INImage *)image
-             contactIdentifier:(nullable NSString *)contactIdentifier
-              customIdentifier:(nullable NSString *)customIdentifier
-                       aliases:(nullable NSArray<INPersonHandle *> *)aliases
-                suggestionType:(INPersonSuggestionType)suggestionType;
+                      nameComponents:(nullable NSPersonNameComponents *)nameComponents
+                         displayName:(nullable NSString *)displayName
+                               image:(nullable INImage *)image
+                   contactIdentifier:(nullable NSString *)contactIdentifier
+                    customIdentifier:(nullable NSString *)customIdentifier
+                             aliases:(nullable NSArray<INPersonHandle *> *)aliases
+                      suggestionType:(INPersonSuggestionType)suggestionType;
 
 @end
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h	2016-07-31 15:18:11.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h	2016-10-24 05:25:49.000000000 +0200
@@ -7,6 +7,8 @@
 
 #import <Foundation/Foundation.h>
 
+#import <Intents/INPersonHandleLabel.h>
+
 typedef NS_ENUM(NSInteger, INPersonHandleType) {
     INPersonHandleTypeUnknown = 0,
     INPersonHandleTypeEmailAddress,
@@ -20,9 +22,11 @@
 
 @property (readonly, copy, NS_NONATOMIC_IOSONLY) NSString *value;
 @property (readonly, NS_NONATOMIC_IOSONLY) INPersonHandleType type;
+@property (readonly, nullable, NS_NONATOMIC_IOSONLY) INPersonHandleLabel label;
 
 - (instancetype)init NS_UNAVAILABLE;
-- (instancetype)initWithValue:(NSString *)value type:(INPersonHandleType)type NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithValue:(NSString *)value type:(INPersonHandleType)type label:(nullable INPersonHandleLabel)label NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithValue:(NSString *)value type:(INPersonHandleType)type;
 
 @end
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandleLabel.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandleLabel.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandleLabel.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandleLabel.h	2016-10-24 05:25:49.000000000 +0200
@@ -0,0 +1,22 @@
+//
+//  INPersonHandleLabel.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+#import <Intents/IntentsDefines.h>
+
+typedef NSString *INPersonHandleLabel NS_EXTENSIBLE_STRING_ENUM;
+
+INTENTS_EXTERN INPersonHandleLabel const INPersonHandleLabelHome NS_SWIFT_NAME(INPersonHandleLabel.home);
+INTENTS_EXTERN INPersonHandleLabel const INPersonHandleLabelWork NS_SWIFT_NAME(INPersonHandleLabel.work);
+INTENTS_EXTERN INPersonHandleLabel const INPersonHandleLabeliPhone NS_SWIFT_NAME(INPersonHandleLabel.iPhone);
+INTENTS_EXTERN INPersonHandleLabel const INPersonHandleLabelMobile NS_SWIFT_NAME(INPersonHandleLabel.mobile);
+INTENTS_EXTERN INPersonHandleLabel const INPersonHandleLabelMain NS_SWIFT_NAME(INPersonHandleLabel.main);
+INTENTS_EXTERN INPersonHandleLabel const INPersonHandleLabelHomeFax NS_SWIFT_NAME(INPersonHandleLabel.homeFax);
+INTENTS_EXTERN INPersonHandleLabel const INPersonHandleLabelWorkFax NS_SWIFT_NAME(INPersonHandleLabel.workFax);
+INTENTS_EXTERN INPersonHandleLabel const INPersonHandleLabelPager NS_SWIFT_NAME(INPersonHandleLabel.pager);
+INTENTS_EXTERN INPersonHandleLabel const INPersonHandleLabelOther NS_SWIFT_NAME(INPersonHandleLabel.other);
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonRelationship.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonRelationship.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonRelationship.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonRelationship.h	2016-10-24 05:25:49.000000000 +0200
@@ -0,0 +1,24 @@
+//
+//  INPersonRelationship.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+#import <Intents/IntentsDefines.h>
+
+typedef NSString *INPersonRelationship NS_EXTENSIBLE_STRING_ENUM;
+
+INTENTS_EXTERN INPersonRelationship const INPersonRelationshipFather NS_SWIFT_NAME(INPersonRelationship.father);
+INTENTS_EXTERN INPersonRelationship const INPersonRelationshipMother NS_SWIFT_NAME(INPersonRelationship.mother);
+INTENTS_EXTERN INPersonRelationship const INPersonRelationshipParent NS_SWIFT_NAME(INPersonRelationship.parent);
+INTENTS_EXTERN INPersonRelationship const INPersonRelationshipBrother NS_SWIFT_NAME(INPersonRelationship.brother);
+INTENTS_EXTERN INPersonRelationship const INPersonRelationshipSister NS_SWIFT_NAME(INPersonRelationship.sister);
+INTENTS_EXTERN INPersonRelationship const INPersonRelationshipChild NS_SWIFT_NAME(INPersonRelationship.child);
+INTENTS_EXTERN INPersonRelationship const INPersonRelationshipFriend NS_SWIFT_NAME(INPersonRelationship.friend);
+INTENTS_EXTERN INPersonRelationship const INPersonRelationshipSpouse NS_SWIFT_NAME(INPersonRelationship.spouse);
+INTENTS_EXTERN INPersonRelationship const INPersonRelationshipPartner NS_SWIFT_NAME(INPersonRelationship.partner);
+INTENTS_EXTERN INPersonRelationship const INPersonRelationshipAssistant NS_SWIFT_NAME(INPersonRelationship.assistant);
+INTENTS_EXTERN INPersonRelationship const INPersonRelationshipManager NS_SWIFT_NAME(INPersonRelationship.manager);
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h	2016-07-31 15:18:11.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h	2016-10-24 05:25:49.000000000 +0200
@@ -14,7 +14,8 @@
 API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INPersonResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given person. The resolvedPerson need not be identical to the input person. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INPerson. The resolvedPerson can be different than the original INPerson. This allows app extensions to add and correct attributes of the INPerson. For example, an extension may add a nickname from the app.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedPerson:(INPerson *)resolvedPerson NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to disambiguate between the provided people.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson_Deprecated.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson_Deprecated.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson_Deprecated.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson_Deprecated.h	2016-10-24 05:25:49.000000000 +0200
@@ -0,0 +1,38 @@
+//
+//  INPerson_Deprecated.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Intents/INPerson.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@interface INPerson (Deprecated)
+
+// The identity of the person in the application (e.g. email address, phone number, user handle, etc.)
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *handle  API_DEPRECATED("Use personHandle instead", ios(10.0, 10.0), macosx(10.12, 10.12));
+
+//  This is the preferred convenience initializer if the app knows the name components of the person (e.g. given name, family name, etc).
+- (instancetype)initWithHandle:(NSString *)handle
+                nameComponents:(NSPersonNameComponents *)nameComponents
+             contactIdentifier:(nullable NSString *)contactIdentifier API_DEPRECATED("Use the designated initializer instead", ios(10.0, 10.0), macosx(10.12, 10.12));
+
+// Use this convenience initializer if the person's name is unknown
+- (instancetype)initWithHandle:(NSString *)handle
+                   displayName:(nullable NSString *)displayName
+             contactIdentifier:(nullable NSString *)contactIdentifier API_DEPRECATED("Use the designated initializer instead", ios(10.0, 10.0), macosx(10.12, 10.12));
+
+- (instancetype)initWithHandle:(NSString *)handle
+                nameComponents:(nullable NSPersonNameComponents *)nameComponents
+                   displayName:(nullable NSString *)displayName
+                         image:(nullable INImage *)image
+             contactIdentifier:(nullable NSString *)contactIdentifier API_DEPRECATED("Use the designated initializer instead", ios(10.0, 10.0), macosx(10.12, 10.12));
+
+
+
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h	2016-07-31 15:18:11.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h	2016-10-24 05:25:49.000000000 +0200
@@ -14,7 +14,9 @@
 API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INPlacemarkResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given placemark. The resolvedPlacemark need not be identical to the input placemark. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given CLPlacemark. The resolvedPlacemark can be different than the original CLPlacemark. This allows app extensions to dynamically fill-in details about the CLPlacemark, as appropriate. To make a new CLPlacemark, see <Intents/CLPlacemark+IntentsAdditions.h>. 
+// Use +notRequired to continue with a 'nil' value.
+
 + (instancetype)successWithResolvedPlacemark:(CLPlacemark *)resolvedPlacemark NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to disambiguate between the provided placemarks.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h	2016-09-28 09:41:00.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h	2016-10-22 02:34:37.000000000 +0200
@@ -56,7 +56,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INSearchCallHistoryIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  searchCallHistoryIntent The input intent
  @param  completion The response handling block takes a INSearchCallHistoryIntentResponse containing the details of the result of having executed the intent
@@ -72,7 +72,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  searchCallHistoryIntent The input intent
  @param  completion The response block contains an INSearchCallHistoryIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -87,7 +87,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  searchCallHistoryIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h	2016-07-31 15:18:11.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h	2016-10-24 05:25:49.000000000 +0200
@@ -13,6 +13,7 @@
     INSearchCallHistoryIntentResponseCodeContinueInApp,
     INSearchCallHistoryIntentResponseCodeFailure,
     INSearchCallHistoryIntentResponseCodeFailureRequiringAppLaunch,
+    INSearchCallHistoryIntentResponseCodeFailureAppConfigurationRequired,
 } API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h	2016-10-22 02:51:11.000000000 +0200
@@ -84,7 +84,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INSearchForMessagesIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  searchForMessagesIntent The input intent
  @param  completion The response handling block takes a INSearchForMessagesIntentResponse containing the details of the result of having executed the intent
@@ -100,7 +100,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  searchForMessagesIntent The input intent
  @param  completion The response block contains an INSearchForMessagesIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -115,7 +115,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  searchForMessagesIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h	2016-09-28 09:40:42.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h	2016-10-22 02:34:38.000000000 +0200
@@ -56,7 +56,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INSendMessageIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  sendMessageIntent The input intent
  @param  completion The response handling block takes a INSendMessageIntentResponse containing the details of the result of having executed the intent
@@ -72,7 +72,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  sendMessageIntent The input intent
  @param  completion The response block contains an INSendMessageIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -87,7 +87,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  sendMessageIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h	2016-07-31 15:18:11.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h	2016-10-24 05:25:49.000000000 +0200
@@ -15,9 +15,12 @@
 @interface INSpeakableString : NSObject <INSpeakable>
 
 - (instancetype)init NS_UNAVAILABLE;
+
 - (instancetype)initWithIdentifier:(NSString *)identifier
-                   spokenPhrase:(NSString *)spokenPhrase
-                   pronunciationHint:(nullable NSString *)pronunciationHint NS_DESIGNATED_INITIALIZER;
+                      spokenPhrase:(NSString *)spokenPhrase
+                 pronunciationHint:(nullable NSString *)pronunciationHint NS_DESIGNATED_INITIALIZER;
+
+- (instancetype)initWithSpokenPhrase:(NSString *)spokenPhrase;
 
 @end
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h	2016-07-31 15:18:11.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h	2016-10-24 05:25:49.000000000 +0200
@@ -14,7 +14,8 @@
 API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INSpeakableStringResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given string. The resolvedString need not be identical to the input string. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INSpeakableString. The resolvedString can be different than the original INSpeakableString. This allows app extensions to add a pronunciationHint, or otherwise tweak the string.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedString:(INSpeakableString *)resolvedString NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to disambiguate between the provided strings.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntent.h	2016-07-31 15:18:11.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntent.h	2016-10-24 05:25:49.000000000 +0200
@@ -40,7 +40,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INStartAudioCallIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  startAudioCallIntent The input intent
  @param  completion The response handling block takes a INStartAudioCallIntentResponse containing the details of the result of having executed the intent
@@ -56,7 +56,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  startAudioCallIntent The input intent
  @param  completion The response block contains an INStartAudioCallIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -71,7 +71,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  startAudioCallIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h	2016-07-31 15:18:11.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h	2016-10-24 05:25:49.000000000 +0200
@@ -13,6 +13,8 @@
     INStartAudioCallIntentResponseCodeContinueInApp,
     INStartAudioCallIntentResponseCodeFailure,
     INStartAudioCallIntentResponseCodeFailureRequiringAppLaunch,
+    INStartAudioCallIntentResponseCodeFailureAppConfigurationRequired,
+    INStartAudioCallIntentResponseCodeFailureCallingServiceNotAvailable,
 } API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntent.h	2016-07-31 15:18:11.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntent.h	2016-10-24 05:25:49.000000000 +0200
@@ -40,7 +40,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INStartVideoCallIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  startVideoCallIntent The input intent
  @param  completion The response handling block takes a INStartVideoCallIntentResponse containing the details of the result of having executed the intent
@@ -56,7 +56,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  startVideoCallIntent The input intent
  @param  completion The response block contains an INStartVideoCallIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -71,7 +71,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  startVideoCallIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h	2016-07-31 15:18:11.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h	2016-10-24 05:25:49.000000000 +0200
@@ -13,6 +13,8 @@
     INStartVideoCallIntentResponseCodeContinueInApp,
     INStartVideoCallIntentResponseCodeFailure,
     INStartVideoCallIntentResponseCodeFailureRequiringAppLaunch,
+    INStartVideoCallIntentResponseCodeFailureAppConfigurationRequired,
+    INStartVideoCallIntentResponseCodeFailureCallingServiceNotAvailable,
 } API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h	2016-07-31 15:18:11.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h	2016-10-24 05:25:49.000000000 +0200
@@ -12,7 +12,8 @@
 API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INStringResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given string. The resolvedString need not be identical to the input string. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given string. The resolvedString can be different than the original string. This allows app extensions to apply business logic constraints to the string.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedString:(NSString *)resolvedString NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to disambiguate between the provided strings.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h	2016-07-31 15:18:11.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h	2016-10-24 05:25:49.000000000 +0200
@@ -31,6 +31,8 @@
 #import <Intents/INImage.h>
 #import <Intents/INPerson.h>
 #import <Intents/INSpeakableString.h>
+#import <Intents/INPersonHandleLabel.h>
+#import <Intents/INPersonRelationship.h>
 
 // Common Resolution Results
 #import <Intents/INDateComponentsRangeResolutionResult.h>
@@ -64,3 +66,6 @@
 // Utilities
 #import <Intents/CLPlacemark+IntentsAdditions.h>
 #import <Intents/NSUserActivity+IntentsAdditions.h>
+
+// Deprecated
+#import <Intents/INPerson_Deprecated.h>

```