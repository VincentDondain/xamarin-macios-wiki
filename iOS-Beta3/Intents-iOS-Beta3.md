#Intents.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INBookRestaurantReservationIntent.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INBookRestaurantReservationIntent.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INBookRestaurantReservationIntent.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INBookRestaurantReservationIntent.h	2016-07-11 07:05:57.000000000 +0200
@@ -13,6 +13,7 @@
 #import <Intents/INRestaurant.h>
 #import <Intents/INRestaurantOffer.h>
 #import <Intents/INRestaurantGuest.h>
+#import <Intents/INRestaurantMarketingPreferences.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -20,6 +21,7 @@
 @interface INBookRestaurantReservationIntent : INIntent <NSCopying>
 
 @property (copy, NS_NONATOMIC_IOSONLY) INRestaurant *restaurant;
+@property (copy, nullable, NS_NONATOMIC_IOSONLY) INRestaurantMarketingPreferences *restaurantMarketingPreferences;
 @property (copy, NS_NONATOMIC_IOSONLY) NSDate *bookingDate;
 @property (NS_NONATOMIC_IOSONLY) NSUInteger partySize;
 @property (copy, nullable, NS_NONATOMIC_IOSONLY) NSString *bookingIdentifier; // unique identifier supplied by vendor to this booking
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INBooleanResolutionResult.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INBooleanResolutionResult.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INBooleanResolutionResult.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INBooleanResolutionResult.h	2016-07-11 07:06:19.000000000 +0200
@@ -9,6 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx)
 @interface INBooleanResolutionResult : INIntentResolutionResult
 
 // This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCancelWorkoutIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCancelWorkoutIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCancelWorkoutIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCancelWorkoutIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -14,7 +14,7 @@
     INCancelWorkoutIntentResponseCodeFailure,
     INCancelWorkoutIntentResponseCodeFailureRequiringAppLaunch,
     INCancelWorkoutIntentResponseCodeFailureNoMatchingWorkout,
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INConditionalOperator.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INConditionalOperator.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INConditionalOperator.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INConditionalOperator.h	2016-07-11 07:06:19.000000000 +0200
@@ -14,6 +14,6 @@
     INConditionalOperatorAll = 0,
     INConditionalOperatorAny,
     INConditionalOperatorNone,
-};
+} API_AVAILABLE(macosx(10.12), ios(10.0));
 
 #endif // INConditionalOperator_h
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmount.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmount.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmount.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmount.h	2016-07-11 07:06:19.000000000 +0200
@@ -9,6 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx)
 @interface INCurrencyAmount : NSObject <NSCopying, NSSecureCoding>
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmountResolutionResult.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmountResolutionResult.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmountResolutionResult.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmountResolutionResult.h	2016-07-11 07:06:19.000000000 +0200
@@ -11,6 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx)
 @interface INCurrencyAmountResolutionResult : INIntentResolutionResult
 
 // This resolution result is for when the app extension wants to tell Siri to proceed with a given currency amount. The resolvedCurrencyAmount need not be identical to the input currency amount. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRange.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRange.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRange.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRange.h	2016-07-11 07:06:19.000000000 +0200
@@ -9,6 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INDateComponentsRange : NSObject <NSCopying, NSSecureCoding>
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h	2016-07-11 07:06:19.000000000 +0200
@@ -11,6 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INDateComponentsRangeResolutionResult : INIntentResolutionResult
 
 // This resolution result is for when the app extension wants to tell Siri to proceed with a given date components range. The resolvedDateComponentsRange need not be identical to the input date components range. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDomainHandling.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDomainHandling.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDomainHandling.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDomainHandling.h	2016-07-11 07:06:19.000000000 +0200
@@ -7,7 +7,7 @@
 
 #import <Intents/INIntents.h>
 
-API_AVAILABLE(macosx(10.12), ios(10.0))
+API_AVAILABLE(macosx(10.12),ios(10.0))
 @protocol INCallsDomainHandling <INStartAudioCallIntentHandling, INStartVideoCallIntentHandling, INSearchCallHistoryIntentHandling>
 @end
 
@@ -36,6 +36,7 @@
 @end
 
 API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INPhotosDomainHandling <INSearchForPhotosIntentHandling, INStartPhotoPlaybackIntentHandling>
 @end
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDoubleResolutionResult.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDoubleResolutionResult.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDoubleResolutionResult.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDoubleResolutionResult.h	2016-07-11 07:06:19.000000000 +0200
@@ -9,6 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx)
 @interface INDoubleResolutionResult : INIntentResolutionResult
 
 // This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INEndWorkoutIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INEndWorkoutIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INEndWorkoutIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INEndWorkoutIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -14,7 +14,7 @@
     INEndWorkoutIntentResponseCodeFailure,
     INEndWorkoutIntentResponseCodeFailureRequiringAppLaunch,
     INEndWorkoutIntentResponseCodeFailureNoMatchingWorkout,
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INExtension.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INExtension.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INExtension.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INExtension.h	2016-07-11 07:06:19.000000000 +0200
@@ -4,19 +4,12 @@
 //  Copyright © 2015 Apple Inc. All rights reserved.
 //
 
-#import <Foundation/NSExtensionRequestHandling.h>
+#import <Foundation/Foundation.h>
 
-@class INIntent;
+#import <Intents/INIntentHandlerProviding.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
-@protocol INIntentHandlerProviding <NSObject>
-
-// Override this function to provide classes other than the extension's principal class to handle a given intent
-- (nullable id)handlerForIntent:(INIntent *)intent;
-
-@end
-
 @interface INExtension : NSObject <INIntentHandlerProviding>
 @end
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingDefaultsIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingDefaultsIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingDefaultsIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingDefaultsIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -10,6 +10,7 @@
 
 #import <Intents/INIntentResponse.h>
 #import <Intents/INImage.h>
+#import <Intents/INRestaurantMarketingPreferences.h>
 
 typedef NS_ENUM(NSInteger, INGetAvailableRestaurantReservationBookingDefaultsIntentResponseCode) {
     INGetAvailableRestaurantReservationBookingDefaultsIntentResponseCodeSuccess,
@@ -27,6 +28,7 @@
 @property (nullable, NS_NONATOMIC_IOSONLY) NSNumber *maximumPartySize;
 @property (nullable, NS_NONATOMIC_IOSONLY) NSNumber *minimumPartySize;
 @property (copy, NS_NONATOMIC_IOSONLY) INImage *providerImage;
+@property (nullable, copy, NS_NONATOMIC_IOSONLY) INRestaurantMarketingPreferences *restaurantMarketingPreferences; // Optional means for allowing restaurant to express desire to communicate directly with the guest, given guest consent.
 
 - (instancetype)initWithDefaultPartySize:(NSUInteger)defaultPartySize defaultBookingDate:(NSDate *)defaultBookingDate code:(INGetAvailableRestaurantReservationBookingDefaultsIntentResponseCode)code userActivity:(nullable NSUserActivity *)userActivity NS_DESIGNATED_INITIALIZER;
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRideStatusIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRideStatusIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRideStatusIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRideStatusIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -18,7 +18,7 @@
     INGetRideStatusIntentResponseCodeFailureRequiringAppLaunch,
     INGetRideStatusIntentResponseCodeFailureRequiringAppLaunchMustVerifyCredentials,
     INGetRideStatusIntentResponseCodeFailureRequiringAppLaunchServiceTemporarilyUnavailable,
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INImage.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INImage.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INImage.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INImage.h	2016-07-11 07:06:19.000000000 +0200
@@ -11,6 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INImage : NSObject <NSCopying, NSSecureCoding>
 
 + (instancetype)imageNamed:(NSString *)name;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntegerResolutionResult.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntegerResolutionResult.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntegerResolutionResult.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntegerResolutionResult.h	2016-07-11 07:06:19.000000000 +0200
@@ -9,6 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx)
 @interface INIntegerResolutionResult : INIntentResolutionResult
 
 // This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntent.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntent.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntent.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntent.h	2016-07-11 07:06:19.000000000 +0200
@@ -9,6 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INIntent : NSObject <NSCopying, NSSecureCoding>
 
 // Returns the identifier of the receiver.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentErrors.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentErrors.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentErrors.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentErrors.h	2016-07-11 07:06:19.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentHandlerProviding.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentHandlerProviding.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentHandlerProviding.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentHandlerProviding.h	2016-07-11 07:06:19.000000000 +0200
@@ -0,0 +1,21 @@
+//
+//  INIntentHandlerProviding.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+@class INIntent;
+
+NS_ASSUME_NONNULL_BEGIN
+
+@protocol INIntentHandlerProviding <NSObject>
+
+// Override this function to provide classes other than the extension's principal class to handle a given intent
+- (nullable id)handlerForIntent:(INIntent *)intent;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentIdentifiers.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentIdentifiers.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentIdentifiers.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentIdentifiers.h	2016-07-11 07:06:19.000000000 +0200
@@ -10,70 +10,76 @@
 #import <Intents/IntentsDefines.h>
 
 // Identifier for INStartAudioCallIntent class.
-INTENTS_EXTERN NSString *const INStartAudioCallIntentIdentifier;
+INTENTS_EXTERN NSString *const INStartAudioCallIntentIdentifier API_AVAILABLE(macosx(10.12), ios(10.0));
 
 // Identifier for INStartVideoCallIntent class.
-INTENTS_EXTERN NSString *const INStartVideoCallIntentIdentifier;
+INTENTS_EXTERN NSString *const INStartVideoCallIntentIdentifier API_AVAILABLE(macosx(10.12), ios(10.0));
 
 // Identifier for INSearchCallHistoryIntent class.
-INTENTS_EXTERN NSString *const INSearchCallHistoryIntentIdentifier;
+INTENTS_EXTERN NSString *const INSearchCallHistoryIntentIdentifier API_AVAILABLE(macosx(10.12), ios(10.0));
 
 // Identifier for INSetAudioSourceInCarIntent class.
-INTENTS_EXTERN NSString *const INSetAudioSourceInCarIntentIdentifier;
+INTENTS_EXTERN NSString *const INSetAudioSourceInCarIntentIdentifier API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 // Identifier for INSetClimateSettingsInCarIntent class.
-INTENTS_EXTERN NSString *const INSetClimateSettingsInCarIntentIdentifier;
+INTENTS_EXTERN NSString *const INSetClimateSettingsInCarIntentIdentifier API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 // Identifier for INSetDefrosterSettingsInCarIntent class.
-INTENTS_EXTERN NSString *const INSetDefrosterSettingsInCarIntentIdentifier;
+INTENTS_EXTERN NSString *const INSetDefrosterSettingsInCarIntentIdentifier API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
-// Identifier for INSetSeatTemperatureInCarIntent class.
-INTENTS_EXTERN NSString *const INSetSeatTemperatureInCarIntentIdentifier;
+// Identifier for INSetSeatSettingsInCarIntent class.
+INTENTS_EXTERN NSString *const INSetSeatSettingsInCarIntentIdentifier API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
+
+// Identifier for INSetProfileInCarIntent class.
+INTENTS_EXTERN NSString *const INSetProfileInCarIntentIdentifier API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
+
+// Identifier for INSaveProfileInCarIntent class.
+INTENTS_EXTERN NSString *const INSaveProfileInCarIntentIdentifier API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 // Identifier for INStartWorkoutIntent class.
-INTENTS_EXTERN NSString *const INStartWorkoutIntentIdentifier;
+INTENTS_EXTERN NSString *const INStartWorkoutIntentIdentifier API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 // Identifier for INPauseWorkoutIntent class.
-INTENTS_EXTERN NSString *const INPauseWorkoutIntentIdentifier;
+INTENTS_EXTERN NSString *const INPauseWorkoutIntentIdentifier API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 // Identifier for INEndWorkoutIntent class.
-INTENTS_EXTERN NSString *const INEndWorkoutIntentIdentifier;
+INTENTS_EXTERN NSString *const INEndWorkoutIntentIdentifier API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 // Identifier for INCancelWorkoutIntent class.
-INTENTS_EXTERN NSString *const INCancelWorkoutIntentIdentifier;
+INTENTS_EXTERN NSString *const INCancelWorkoutIntentIdentifier API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 // Identifier for INResumeWorkoutIntent class.
-INTENTS_EXTERN NSString *const INResumeWorkoutIntentIdentifier;
+INTENTS_EXTERN NSString *const INResumeWorkoutIntentIdentifier API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 // Identifier for INSetRadioStationIntent class.
-INTENTS_EXTERN NSString *const INSetRadioStationIntentIdentifier;
+INTENTS_EXTERN NSString *const INSetRadioStationIntentIdentifier API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 // Identifier for INSendMessageIntent class.
-INTENTS_EXTERN NSString *const INSendMessageIntentIdentifier;
+INTENTS_EXTERN NSString *const INSendMessageIntentIdentifier API_AVAILABLE(macosx(10.12), ios(10.0));
 
 // Identifier for INSearchForMessagesIntent class.
-INTENTS_EXTERN NSString *const INSearchForMessagesIntentIdentifier;
+INTENTS_EXTERN NSString *const INSearchForMessagesIntentIdentifier API_AVAILABLE(macosx(10.12), ios(10.0));
 
 // Identifier for INSetMessageAttributeIntent class.
-INTENTS_EXTERN NSString *const INSetMessageAttributeIntentIdentifier;
+INTENTS_EXTERN NSString *const INSetMessageAttributeIntentIdentifier API_AVAILABLE(macosx(10.12), ios(10.0));
 
 // Identifier for INSendPaymentIntent class.
-INTENTS_EXTERN NSString *const INSendPaymentIntentIdentifier;
+INTENTS_EXTERN NSString *const INSendPaymentIntentIdentifier API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 // Identifier for INRequestPaymentIntent class.
-INTENTS_EXTERN NSString *const INRequestPaymentIntentIdentifier;
+INTENTS_EXTERN NSString *const INRequestPaymentIntentIdentifier API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 // Identifier for INSearchForPhotosIntent class.
-INTENTS_EXTERN NSString *const INSearchForPhotosIntentIdentifier;
+INTENTS_EXTERN NSString *const INSearchForPhotosIntentIdentifier API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 // Identifier for INStartPhotoPlaybackIntent class.
-INTENTS_EXTERN NSString *const INStartPhotoPlaybackIntentIdentifier;
+INTENTS_EXTERN NSString *const INStartPhotoPlaybackIntentIdentifier API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 // Identifier for INListRideOptionsIntent class.
-INTENTS_EXTERN NSString *const INListRideOptionsIntentIdentifier;
+INTENTS_EXTERN NSString *const INListRideOptionsIntentIdentifier API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 // Identifier for INRequestRideIntent class.
-INTENTS_EXTERN NSString *const INRequestRideIntentIdentifier;
+INTENTS_EXTERN NSString *const INRequestRideIntentIdentifier API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 // Identifier for INGetRideStatusIntent class.
-INTENTS_EXTERN NSString *const INGetRideStatusIntentIdentifier;
+INTENTS_EXTERN NSString *const INGetRideStatusIntentIdentifier API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h	2016-07-11 07:06:19.000000000 +0200
@@ -9,6 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INIntentResolutionResult<ObjectType> : NSObject
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -9,6 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INIntentResponse : NSObject <NSCopying, NSSecureCoding>
 
 // This user activity will be used to launch the containing application when host application finds appropriate or when users request so.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentRestaurantReservation.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentRestaurantReservation.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentRestaurantReservation.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentRestaurantReservation.h	2016-07-11 07:06:19.000000000 +0200
@@ -22,6 +22,7 @@
 #import "INGetUserCurrentRestaurantReservationBookingsIntentResponse.h"
 #import "INGetAvailableRestaurantReservationBookingDefaultsIntentResponse.h"
 #import "INRestaurant.h"
+#import "INRestaurantMarketingPreferences.h"
 #import "INRestaurantOffer.h"
 #import "INGetRestaurantGuestIntent.h"
 #import "INGetRestaurantGuestIntentResponse.h"
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h	2016-07-11 07:06:19.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INListRideOptionsIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INListRideOptionsIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INListRideOptionsIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INListRideOptionsIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -21,7 +21,7 @@
     INListRideOptionsIntentResponseCodeFailureRequiringAppLaunchNoServiceInArea,
     INListRideOptionsIntentResponseCodeFailureRequiringAppLaunchServiceTemporarilyUnavailable,
     INListRideOptionsIntentResponseCodeFailureRequiringAppLaunchPreviousRideNeedsCompletion,
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessage.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessage.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessage.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessage.h	2016-07-11 07:06:19.000000000 +0200
@@ -11,6 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INMessage : NSObject <NSCopying, NSSecureCoding>
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPauseWorkoutIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPauseWorkoutIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPauseWorkoutIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPauseWorkoutIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -14,7 +14,7 @@
     INPauseWorkoutIntentResponseCodeFailure,
     INPauseWorkoutIntentResponseCodeFailureRequiringAppLaunch,
     INPauseWorkoutIntentResponseCodeFailureNoMatchingWorkout,
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentMethod.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentMethod.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentMethod.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentMethod.h	2016-07-11 07:06:19.000000000 +0200
@@ -13,19 +13,24 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx)
 @interface INPaymentMethod : NSObject <NSCopying, NSSecureCoding>
 
 - (instancetype)init NS_UNAVAILABLE;
 
 - (instancetype)initWithType:(INPaymentMethodType)type
                         name:(nullable NSString *)name
+          identificationHint:(nullable NSString *)identificationHint
                         icon:(nullable INImage *)icon NS_DESIGNATED_INITIALIZER;
 
 @property (readonly, assign, NS_NONATOMIC_IOSONLY) INPaymentMethodType type;
 
-// The name of this payment method, e.g. "Flyover Rewards (···· 1259)".
+// The name of this payment method, e.g. "Flyover Rewards".
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *name;
 
+// The identification hint for this payment method, e.g. "(···· 1259)"
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *identificationHint;
+
 // An image that represents this payment method (e.g. the card's brand).
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INImage *icon;
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentRecord.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentRecord.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentRecord.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentRecord.h	2016-07-11 07:06:19.000000000 +0200
@@ -16,6 +16,7 @@
 @class INPaymentMethod;
 @class INPerson;
 
+API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx)
 @interface INPaymentRecord : NSObject <NSCopying, NSSecureCoding>
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson+SiriAdditions.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson+SiriAdditions.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson+SiriAdditions.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson+SiriAdditions.h	2016-07-11 07:06:19.000000000 +0200
@@ -12,7 +12,6 @@
 NS_ASSUME_NONNULL_BEGIN
 
 @interface INPerson (SiriAdditions) <INSpeakable>
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h	2016-06-28 04:49:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h	2016-07-11 07:06:19.000000000 +0200
@@ -12,6 +12,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INPerson : NSObject <NSCopying, NSSecureCoding>
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h	2016-07-11 07:06:19.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h	2016-07-11 07:06:19.000000000 +0200
@@ -11,6 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INPersonResolutionResult : INIntentResolutionResult
 
 // This resolution result is for when the app extension wants to tell Siri to proceed with a given person. The resolvedPerson need not be identical to the input person. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h	2016-07-11 07:06:19.000000000 +0200
@@ -11,6 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INPlacemarkResolutionResult : INIntentResolutionResult
 
 // This resolution result is for when the app extension wants to tell Siri to proceed with a given placemark. The resolvedPlacemark need not be identical to the input placemark. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPreferences.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPreferences.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPreferences.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPreferences.h	2016-07-11 07:06:19.000000000 +0200
@@ -9,6 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx)
 @interface INPreferences : NSObject
 
 + (INSiriAuthorizationStatus)siriAuthorizationStatus;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPriceRange.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPriceRange.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPriceRange.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPriceRange.h	2016-07-11 07:06:19.000000000 +0200
@@ -9,6 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx)
 @interface INPriceRange : NSObject <NSCopying, NSSecureCoding>
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestPaymentIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestPaymentIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestPaymentIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestPaymentIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -16,7 +16,7 @@
     INRequestPaymentIntentResponseCodeSuccess,
     INRequestPaymentIntentResponseCodeFailure,
     INRequestPaymentIntentResponseCodeFailureRequiringAppLaunch,
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestRideIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestRideIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestRideIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestRideIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -20,7 +20,7 @@
     INRequestRideIntentResponseCodeFailureRequiringAppLaunchNoServiceInArea,
     INRequestRideIntentResponseCodeFailureRequiringAppLaunchServiceTemporarilyUnavailable,
     INRequestRideIntentResponseCodeFailureRequiringAppLaunchPreviousRideNeedsCompletion,
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantMarketingPreferences.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantMarketingPreferences.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantMarketingPreferences.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantMarketingPreferences.h	2016-07-11 07:06:19.000000000 +0200
@@ -0,0 +1,37 @@
+//
+//  INRestaurantMarketingPreferences.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+//  This API requires you to work with Apple Maps before your application can use it. For information on how to get started, please go to MapsConnect.
+//
+//  http://mapsconnect.apple.com/info/extensions
+
+#import <Foundation/Foundation.h>
+#import <Intents/INRestaurant.h>
+#import <Intents/INRestaurantGuest.h>
+
+typedef NS_ENUM(NSInteger, INRestaurantMarketingPreferencesContactMethod) {
+    INRestaurantMarketingPreferencesContactMethodUndefined = 0,
+    INRestaurantMarketingPreferencesContactMethodEmail
+};
+
+NS_ASSUME_NONNULL_BEGIN
+
+NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+@interface INRestaurantMarketingPreferences : NSObject <NSSecureCoding, NSCopying>
+
+- (instancetype)init NS_UNAVAILABLE;
+
+- (instancetype)initWithContactMethod:(INRestaurantMarketingPreferencesContactMethod)contactMethod guestHasOptedInToMarketing:(BOOL)guestHasOptedInToMarketing  localizedDescriptionForMarketingEnabled:(NSString *)localizedDescriptionForMarketingEnabled localizedDescriptionForMarketingNotEnabled:(NSString * __nullable)localizedDescriptionForMarketingNotEnabled NS_DESIGNATED_INITIALIZER;
+
+@property (NS_NONATOMIC_IOSONLY, readonly) INRestaurantMarketingPreferencesContactMethod contactMethod;
+
+@property (NS_NONATOMIC_IOSONLY) BOOL guestHasOptedInToMarketing;
+
+@property (NS_NONATOMIC_IOSONLY, readonly) NSString *localizedDescriptionForMarketingEnabled; // A localized description of consequences, both legal and practical, of opting into receiving marketing from restaurant
+@property (NS_NONATOMIC_IOSONLY, nullable, readonly) NSString *localizedDescriptionForMarketingNotEnabled; // An optional localized description of practical consequences of not opting into receiving marketing from restaurant.
+
+@end
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INResumeWorkoutIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INResumeWorkoutIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INResumeWorkoutIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INResumeWorkoutIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -14,7 +14,7 @@
     INResumeWorkoutIntentResponseCodeFailure,
     INResumeWorkoutIntentResponseCodeFailureRequiringAppLaunch,
     INResumeWorkoutIntentResponseCodeFailureNoMatchingWorkout,
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideOption.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideOption.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideOption.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideOption.h	2016-07-11 07:06:19.000000000 +0200
@@ -25,7 +25,7 @@
 - (nullable instancetype)initWithCoder:(NSCoder *)decoder NS_DESIGNATED_INITIALIZER;
 
 @property (readwrite, copy, NS_NONATOMIC_IOSONLY) NSString *name; // a name for the ride option.
-@property (readwrite, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *subtitle; // a message associated with the option, shown as a subtitle under the title, which may include additional information or branding text. For example: "Shared ride" or "Operates 10am-10pm only".
+
 @property (readwrite, copy, NS_NONATOMIC_IOSONLY) NSDate *estimatedPickupDate; // used for providing an ETA to the user.
 
 @property (readwrite, copy, nullable, NS_NONATOMIC_IOSONLY) INPriceRange *priceRange; // The indicative range of prices for this option.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideStatus.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideStatus.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideStatus.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideStatus.h	2016-07-11 07:06:19.000000000 +0200
@@ -33,6 +33,10 @@
 @property (readwrite, copy, nullable, NS_NONATOMIC_IOSONLY) NSDate *estimatedPickupDate;
 @property (readwrite, copy, nullable, NS_NONATOMIC_IOSONLY) NSDate *estimatedDropOffDate;
 
+// This is the date after arrival at the pickup location after which the ride may stop waiting for the passenger to be picked up.
+// The passenger is expected to arrive at pickup before this date.
+@property (readwrite, copy, nullable, NS_NONATOMIC_IOSONLY) NSDate *estimatedPickupEndDate;
+
 @property (readwrite, copy, nullable, NS_NONATOMIC_IOSONLY) CLPlacemark *pickupLocation;
 @property (readwrite, copy, nullable, NS_NONATOMIC_IOSONLY) NSArray<CLPlacemark *> *waypoints;
 @property (readwrite, copy, nullable, NS_NONATOMIC_IOSONLY) CLPlacemark *dropOffLocation;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -14,7 +14,7 @@
     INSaveProfileInCarIntentResponseCodeSuccess,
     INSaveProfileInCarIntentResponseCodeFailure,
     INSaveProfileInCarIntentResponseCodeFailureRequiringAppLaunch,
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -13,7 +13,7 @@
     INSearchCallHistoryIntentResponseCodeContinueInApp,
     INSearchCallHistoryIntentResponseCodeFailure,
     INSearchCallHistoryIntentResponseCodeFailureRequiringAppLaunch,
-};
+} API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -17,7 +17,7 @@
     INSearchForMessagesIntentResponseCodeFailure,
     INSearchForMessagesIntentResponseCodeFailureRequiringAppLaunch,
     INSearchForMessagesIntentResponseCodeFailureMessageServiceNotAvailable,
-};
+} API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntent.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntent.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntent.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntent.h	2016-07-11 07:05:57.000000000 +0200
@@ -23,6 +23,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INSearchForPhotosIntent : INIntent
 
 - (instancetype)initWithDateCreated:(nullable INDateComponentsRange *)dateCreated
@@ -71,6 +72,7 @@
  */
 
 API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INSearchForPhotosIntentHandling <NSObject>
 
 @required
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -13,11 +13,12 @@
     INSearchForPhotosIntentResponseCodeContinueInApp,
     INSearchForPhotosIntentResponseCodeFailure,
     INSearchForPhotosIntentResponseCodeFailureRequiringAppLaunch,
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
 API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INSearchForPhotosIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -14,7 +14,7 @@
     INSendMessageIntentResponseCodeSuccess,
     INSendMessageIntentResponseCodeFailure,
     INSendMessageIntentResponseCodeFailureRequiringAppLaunch,
-};
+} API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendPaymentIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendPaymentIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendPaymentIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendPaymentIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -16,7 +16,7 @@
     INSendPaymentIntentResponseCodeSuccess,
     INSendPaymentIntentResponseCodeFailure,
     INSendPaymentIntentResponseCodeFailureRequiringAppLaunch,
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetAudioSourceInCarIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetAudioSourceInCarIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetAudioSourceInCarIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetAudioSourceInCarIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -14,7 +14,7 @@
     INSetAudioSourceInCarIntentResponseCodeSuccess,
     INSetAudioSourceInCarIntentResponseCodeFailure,
     INSetAudioSourceInCarIntentResponseCodeFailureRequiringAppLaunch,
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -14,7 +14,7 @@
     INSetClimateSettingsInCarIntentResponseCodeSuccess,
     INSetClimateSettingsInCarIntentResponseCodeFailure,
     INSetClimateSettingsInCarIntentResponseCodeFailureRequiringAppLaunch,
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetDefrosterSettingsInCarIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetDefrosterSettingsInCarIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetDefrosterSettingsInCarIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetDefrosterSettingsInCarIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -14,7 +14,7 @@
     INSetDefrosterSettingsInCarIntentResponseCodeSuccess,
     INSetDefrosterSettingsInCarIntentResponseCodeFailure,
     INSetDefrosterSettingsInCarIntentResponseCodeFailureRequiringAppLaunch,
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetMessageAttributeIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetMessageAttributeIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetMessageAttributeIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetMessageAttributeIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -16,7 +16,7 @@
     INSetMessageAttributeIntentResponseCodeFailureRequiringAppLaunch,
     INSetMessageAttributeIntentResponseCodeFailureMessageNotFound,
     INSetMessageAttributeIntentResponseCodeFailureMessageAttributeNotSet,
-};
+} API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -14,7 +14,7 @@
     INSetProfileInCarIntentResponseCodeSuccess,
     INSetProfileInCarIntentResponseCodeFailure,
     INSetProfileInCarIntentResponseCodeFailureRequiringAppLaunch,
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetRadioStationIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetRadioStationIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetRadioStationIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetRadioStationIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -15,7 +15,7 @@
     INSetRadioStationIntentResponseCodeFailure,
     INSetRadioStationIntentResponseCodeFailureRequiringAppLaunch,
     INSetRadioStationIntentResponseCodeFailureNotSubscribed,
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatSettingsInCarIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatSettingsInCarIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatSettingsInCarIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatSettingsInCarIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -14,7 +14,7 @@
     INSetSeatSettingsInCarIntentResponseCodeSuccess,
     INSetSeatSettingsInCarIntentResponseCodeFailure,
     INSetSeatSettingsInCarIntentResponseCodeFailureRequiringAppLaunch,
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSiriAuthorizationStatus.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSiriAuthorizationStatus.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSiriAuthorizationStatus.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSiriAuthorizationStatus.h	2016-07-11 07:06:19.000000000 +0200
@@ -30,6 +30,6 @@
     
     // User has authorized this application to use Siri services.
     INSiriAuthorizationStatusAuthorized
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 #endif /* INSiriAuthorizationStatus_h */
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h	2016-07-11 07:06:19.000000000 +0200
@@ -11,6 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INSpeakableString : NSObject <INSpeakable>
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h	2016-07-11 07:06:19.000000000 +0200
@@ -11,6 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INSpeakableStringResolutionResult : INIntentResolutionResult
 
 // This resolution result is for when the app extension wants to tell Siri to proceed with a given string. The resolvedString need not be identical to the input string. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -13,7 +13,7 @@
     INStartAudioCallIntentResponseCodeContinueInApp,
     INStartAudioCallIntentResponseCodeFailure,
     INStartAudioCallIntentResponseCodeFailureRequiringAppLaunch,
-};
+} API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntent.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntent.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntent.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntent.h	2016-07-11 07:05:57.000000000 +0200
@@ -23,6 +23,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INStartPhotoPlaybackIntent : INIntent
 
 - (instancetype)initWithDateCreated:(nullable INDateComponentsRange *)dateCreated
@@ -71,6 +72,7 @@
  */
 
 API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INStartPhotoPlaybackIntentHandling <NSObject>
 
 @required
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -13,11 +13,12 @@
     INStartPhotoPlaybackIntentResponseCodeContinueInApp,
     INStartPhotoPlaybackIntentResponseCodeFailure,
     INStartPhotoPlaybackIntentResponseCodeFailureRequiringAppLaunch,
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
 API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INStartPhotoPlaybackIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -13,7 +13,7 @@
     INStartVideoCallIntentResponseCodeContinueInApp,
     INStartVideoCallIntentResponseCodeFailure,
     INStartVideoCallIntentResponseCodeFailureRequiringAppLaunch,
-};
+} API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartWorkoutIntentResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartWorkoutIntentResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartWorkoutIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartWorkoutIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
@@ -15,7 +15,7 @@
     INStartWorkoutIntentResponseCodeFailureRequiringAppLaunch,
     INStartWorkoutIntentResponseCodeFailureOngoingWorkout,
     INStartWorkoutIntentResponseCodeFailureNoMatchingWorkout,
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h	2016-07-11 07:06:19.000000000 +0200
@@ -9,6 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INStringResolutionResult : INIntentResolutionResult
 
 // This resolution result is for when the app extension wants to tell Siri to proceed with a given string. The resolvedString need not be identical to the input string. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperature.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperature.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperature.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperature.h	2016-07-11 07:06:19.000000000 +0200
@@ -9,6 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx)
 @interface INTemperature : NSObject <NSCopying, NSSecureCoding>
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureResolutionResult.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureResolutionResult.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureResolutionResult.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureResolutionResult.h	2016-07-11 07:06:19.000000000 +0200
@@ -11,6 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx)
 @interface INTemperatureResolutionResult : INIntentResolutionResult
 
 // This resolution result is for when the app extension wants to tell Siri to proceed with a given temperature. The resolvedTemperature need not be identical to the input temperature. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INVocabulary.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INVocabulary.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INVocabulary.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INVocabulary.h	2016-07-11 07:06:19.000000000 +0200
@@ -31,6 +31,7 @@
     INVocabularyStringTypeCarProfileName = 300,
 };
 
+API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx, watchos, tvos)
 @interface INVocabulary : NSObject
 
 + (instancetype)sharedVocabulary;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INWorkoutGoalUnitType.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INWorkoutGoalUnitType.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INWorkoutGoalUnitType.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INWorkoutGoalUnitType.h	2016-07-11 07:06:19.000000000 +0200
@@ -18,7 +18,7 @@
     INWorkoutGoalUnitTypeMeter,
     INWorkoutGoalUnitTypeFoot,
     INWorkoutGoalUnitTypeMile,
-    INWorkoutGoalUnitTypeYards,
+    INWorkoutGoalUnitTypeYard,
     INWorkoutGoalUnitTypeSecond,
     INWorkoutGoalUnitTypeMinute,
     INWorkoutGoalUnitTypeHour,
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h	2016-06-26 09:14:37.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h	2016-07-11 07:05:57.000000000 +0200
@@ -20,6 +20,7 @@
 // Base
 #import <Intents/INIntent.h>
 #import <Intents/INIntentErrors.h>
+#import <Intents/INIntentHandlerProviding.h>
 #import <Intents/INIntentIdentifiers.h>
 #import <Intents/INIntentResponse.h>
 #import <Intents/INIntentResolutionResult.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/NSUserActivity+IntentsAdditions.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/NSUserActivity+IntentsAdditions.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/NSUserActivity+IntentsAdditions.h	2016-06-26 09:15:29.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/NSUserActivity+IntentsAdditions.h	2016-07-11 07:06:19.000000000 +0200
@@ -13,7 +13,7 @@
 
 @interface NSUserActivity (IntentsAdditions)
 
-@property (readonly, nullable, NS_NONATOMIC_IOSONLY) INInteraction *interaction;
+@property (readonly, nullable, NS_NONATOMIC_IOSONLY) INInteraction *interaction API_AVAILABLE(macosx(10.12), ios(10.0));
 
 @end
 

```