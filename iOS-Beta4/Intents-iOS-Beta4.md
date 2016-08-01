#Intents.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INBookRestaurantReservationIntent.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INBookRestaurantReservationIntent.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INBookRestaurantReservationIntent.h	2016-07-11 07:05:57.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INBookRestaurantReservationIntent.h	2016-07-25 07:26:52.000000000 +0200
@@ -13,16 +13,20 @@
 #import <Intents/INRestaurant.h>
 #import <Intents/INRestaurantOffer.h>
 #import <Intents/INRestaurantGuest.h>
-#import <Intents/INRestaurantMarketingPreferences.h>
+#import <Intents/INRestaurantResolutionResult.h>
+#import <Intents/INIntegerResolutionResult.h>
+#import <Intents/INRestaurantGuestResolutionResult.h>
+#import <Intents/INStringResolutionResult.h>
+#import <Intents/INDateComponentsResolutionResult.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INBookRestaurantReservationIntent : INIntent <NSCopying>
 
 @property (copy, NS_NONATOMIC_IOSONLY) INRestaurant *restaurant;
-@property (copy, nullable, NS_NONATOMIC_IOSONLY) INRestaurantMarketingPreferences *restaurantMarketingPreferences;
-@property (copy, NS_NONATOMIC_IOSONLY) NSDate *bookingDate;
+@property (copy, NS_NONATOMIC_IOSONLY) NSDateComponents *bookingDateComponents;
 @property (NS_NONATOMIC_IOSONLY) NSUInteger partySize;
 @property (copy, nullable, NS_NONATOMIC_IOSONLY) NSString *bookingIdentifier; // unique identifier supplied by vendor to this booking
 @property (copy, nullable, NS_NONATOMIC_IOSONLY) INRestaurantGuest *guest; // model object containing contact information
@@ -32,6 +36,9 @@
 @end
 
 @class INBookRestaurantReservationIntentResponse;
+
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INBookRestaurantReservationIntentHandling <NSObject>
 
 /*!
@@ -47,7 +54,7 @@
  
  */
 
-- (void)handleBookRestaurantReservation:(INBookRestaurantReservationIntent *)bookingIntent completion:(void (^)(INBookRestaurantReservationIntentResponse *response))completion  NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_SWIFT_NAME(handle(bookRestaurantReservation:completion:));
+- (void)handleBookRestaurantReservation:(INBookRestaurantReservationIntent *)intent completion:(void (^)(INBookRestaurantReservationIntentResponse *response))completion  NS_SWIFT_NAME(handle(bookRestaurantReservation:completion:));
 
 @optional
 
@@ -63,7 +70,7 @@
  
  */
 
-- (void)confirmBookRestaurantReservation:(INBookRestaurantReservationIntent *)bookingIntent completion:(void (^)(INBookRestaurantReservationIntentResponse *response))completion  NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_SWIFT_NAME(confirm(bookRestaurantReservation:completion:));
+- (void)confirmBookRestaurantReservation:(INBookRestaurantReservationIntent *)intent completion:(void (^)(INBookRestaurantReservationIntentResponse *response))completion  NS_SWIFT_NAME(confirm(bookRestaurantReservation:completion:));
 
 /*!
  @brief Resolution methods
@@ -77,11 +84,11 @@
  
  */
 
-- (void)resolveRestaurantForBookRestaurantReservation:(INBookRestaurantReservationIntent *)bookingIntent completion:(void(^)(INIntentResolutionResult<INRestaurant *> *resolutionResult))completion NS_SWIFT_NAME(resolveRestaurant(for:completion:));
-- (void)resolveBookingDateForBookRestaurantReservation:(INBookRestaurantReservationIntent *)bookingIntent completion:(void(^)(INIntentResolutionResult<NSDate *> *resolutionResult))completion NS_SWIFT_NAME(resolveBookingDate(for:completion:));
-- (void)resolvePartySizeForBookRestaurantReservation:(INBookRestaurantReservationIntent *)bookingIntent completion:(void(^)(INIntentResolutionResult<NSNumber *> *resolutionResult))completion NS_SWIFT_NAME(resolvePartySize(for:completion:));
-- (void)resolveGuestForBookRestaurantReservation:(INBookRestaurantReservationIntent *)bookingIntent completion:(void(^)(INIntentResolutionResult<INRestaurantGuest *> *resolutionResult))completion NS_SWIFT_NAME(resolveGuest(for:completion:));
-- (void)resolveGuestProvidedSpecialRequestTextForBookRestaurantReservation:(INBookRestaurantReservationIntent *)bookingIntent completion:(void(^)(INIntentResolutionResult<NSString *> *resolutionResult))completion NS_SWIFT_NAME(resolveGuestProvidedSpecialRequestText(for:completion:));
+- (void)resolveRestaurantForBookRestaurantReservation:(INBookRestaurantReservationIntent *)intent withCompletion:(void(^)(INRestaurantResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveRestaurant(for:completion:));
+- (void)resolveBookingDateComponentsForBookRestaurantReservation:(INBookRestaurantReservationIntent *)intent withCompletion:(void(^)(INDateComponentsResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveBookingDateComponents(for:completion:));
+- (void)resolvePartySizeForBookRestaurantReservation:(INBookRestaurantReservationIntent *)intent withCompletion:(void(^)(INIntegerResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolvePartySize(for:completion:));
+- (void)resolveGuestForBookRestaurantReservation:(INBookRestaurantReservationIntent *)intent withCompletion:(void(^)(INRestaurantGuestResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveGuest(for:completion:));
+- (void)resolveGuestProvidedSpecialRequestTextForBookRestaurantReservation:(INBookRestaurantReservationIntent *)intent withCompletion:(void(^)(INStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveGuestProvidedSpecialRequestText(for:completion:));
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INBookRestaurantReservationIntentResponse.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INBookRestaurantReservationIntentResponse.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INBookRestaurantReservationIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INBookRestaurantReservationIntentResponse.h	2016-07-25 07:30:57.000000000 +0200
@@ -22,7 +22,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INBookRestaurantReservationIntentResponse : INIntentResponse
 
 - (instancetype)initWithCode:(INBookRestaurantReservationIntentCode)code userActivity:(nullable NSUserActivity *)userActivity;
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCallCapabilityOptionsResolutionResult.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCallCapabilityOptionsResolutionResult.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCallCapabilityOptionsResolutionResult.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCallCapabilityOptionsResolutionResult.h	1970-01-01 01:00:00.000000000 +0100
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
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmountResolutionResult.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmountResolutionResult.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmountResolutionResult.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmountResolutionResult.h	2016-07-25 07:30:57.000000000 +0200
@@ -23,9 +23,6 @@
 // This resolution result is to ask Siri to confirm if this is the currency amount with which the user wants to continue.
 + (instancetype)confirmationRequiredWithCurrencyAmountToConfirm:(nullable INCurrencyAmount *)currencyAmountToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
 
-// This resolution result is to inform Siri that in order to continue, the app extension needs the currency amount to be filled in greater detail. If this parameter is nil and the app extension wants to request a non-nil value, it should use +needsValue.
-+ (instancetype)needsMoreDetailsForCurrencyAmount:(INCurrencyAmount *)currencyAmountToComplete NS_SWIFT_NAME(needsMoreDetails(for:));
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h	2016-07-25 07:30:56.000000000 +0200
@@ -23,9 +23,6 @@
 // This resolution result is to ask Siri to confirm if this is the date components range with which the user wants to continue.
 + (instancetype)confirmationRequiredWithDateComponentsRangeToConfirm:(nullable INDateComponentsRange *)dateComponentsRangeToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
 
-// This resolution result is to inform Siri that in order to continue, the app extension needs the date components range to be filled in greater detail. If this parameter is nil and the app extension wants to request a non-nil value, it should use +needsValue.
-+ (instancetype)needsMoreDetailsForDateComponentsRange:(INDateComponentsRange *)dateComponentsRangeToComplete NS_SWIFT_NAME(needsMoreDetails(for:));
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsResolutionResult.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsResolutionResult.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsResolutionResult.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsResolutionResult.h	2016-07-25 07:30:57.000000000 +0200
@@ -0,0 +1,26 @@
+//
+//  INDateComponentsResolutionResult.m
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Intents/INIntentResolutionResult.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+API_AVAILABLE(ios(10.0))
+@interface INDateComponentsResolutionResult : INIntentResolutionResult
+
+// This resolution result is for when the app extension wants to tell Siri to proceed with a given dateComponents. The resolvedDateComponents need not be identical to the input dateComponents. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
++ (instancetype)successWithResolvedDateComponents:(NSDateComponents *)resolvedDateComponents NS_SWIFT_NAME(success(with:));
+
+// This resolution result is to ask Siri to disambiguate between the provided dateComponentss.
++ (instancetype)disambiguationWithDateComponentsToDisambiguate:(NSArray<NSDateComponents *> *)dateComponentsToDisambiguate NS_SWIFT_NAME(disambiguation(with:));
+
+// This resolution result is to ask Siri to confirm if this is the dateComponents with which the user wants to continue.
++ (instancetype)confirmationRequiredWithDateComponentsToConfirm:(nullable NSDateComponents *)dateComponentsToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingDefaultsIntent.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingDefaultsIntent.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingDefaultsIntent.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingDefaultsIntent.h	2016-07-25 07:30:57.000000000 +0200
@@ -11,10 +11,12 @@
 #import <Intents/INIntent.h>
 #import <Intents/INIntentResolutionResult.h>
 #import <Intents/INRestaurant.h>
+#import <Intents/INRestaurantResolutionResult.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INGetAvailableRestaurantReservationBookingDefaultsIntent : INIntent
 
 @property (copy, nullable, NS_NONATOMIC_IOSONLY) INRestaurant *restaurant; // an optional restaurant that the extension may or may not use to tailor reservation defaults
@@ -23,6 +25,8 @@
 
 @class INGetAvailableRestaurantReservationBookingDefaultsIntentResponse;
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INGetAvailableRestaurantReservationBookingDefaultsIntentHandling <NSObject>
 
 /*!
@@ -38,7 +42,7 @@
  
  */
 
-- (void)handleGetAvailableRestaurantReservationBookingDefaults:(INGetAvailableRestaurantReservationBookingDefaultsIntent *)bookingDefaultsIntent completion:(void (^)(INGetAvailableRestaurantReservationBookingDefaultsIntentResponse *response))completion NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_SWIFT_NAME(handle(getAvailableRestaurantReservationBookingDefaults:completion:));
+- (void)handleGetAvailableRestaurantReservationBookingDefaults:(INGetAvailableRestaurantReservationBookingDefaultsIntent *)intent completion:(void (^)(INGetAvailableRestaurantReservationBookingDefaultsIntentResponse *response))completion NS_SWIFT_NAME(handle(getAvailableRestaurantReservationBookingDefaults:completion:));
 
 @optional
 
@@ -54,7 +58,7 @@
  
  */
 
-- (void)confirmGetAvailableRestaurantReservationBookingDefaults:(INGetAvailableRestaurantReservationBookingDefaultsIntent *)bookingDefaultsIntent completion:(void (^)(INGetAvailableRestaurantReservationBookingDefaultsIntentResponse *response))completion NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_SWIFT_NAME(confirm(getAvailableRestaurantReservationBookingDefaults:completion:));
+- (void)confirmGetAvailableRestaurantReservationBookingDefaults:(INGetAvailableRestaurantReservationBookingDefaultsIntent *)intent completion:(void (^)(INGetAvailableRestaurantReservationBookingDefaultsIntentResponse *response))completion NS_SWIFT_NAME(confirm(getAvailableRestaurantReservationBookingDefaults:completion:));
 
 /*!
  @brief Resolution methods
@@ -68,7 +72,7 @@
  
  */
 
-- (void)resolveRestaurantForGetAvailableRestaurantReservationBookingDefaults:(INGetAvailableRestaurantReservationBookingDefaultsIntent *)bookingIntent completion:(void(^)(INIntentResolutionResult<INRestaurant *> *resolutionResult))completion NS_SWIFT_NAME(resolveRestaurant(for:completion:));
+- (void)resolveRestaurantForGetAvailableRestaurantReservationBookingDefaults:(INGetAvailableRestaurantReservationBookingDefaultsIntent *)intent withCompletion:(void(^)(INRestaurantResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveRestaurant(for:completion:));
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingDefaultsIntentResponse.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingDefaultsIntentResponse.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingDefaultsIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingDefaultsIntentResponse.h	2016-07-25 07:30:57.000000000 +0200
@@ -10,7 +10,6 @@
 
 #import <Intents/INIntentResponse.h>
 #import <Intents/INImage.h>
-#import <Intents/INRestaurantMarketingPreferences.h>
 
 typedef NS_ENUM(NSInteger, INGetAvailableRestaurantReservationBookingDefaultsIntentResponseCode) {
     INGetAvailableRestaurantReservationBookingDefaultsIntentResponseCodeSuccess,
@@ -20,7 +19,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INGetAvailableRestaurantReservationBookingDefaultsIntentResponse : INIntentResponse
 
 @property (readonly, NS_NONATOMIC_IOSONLY) NSUInteger defaultPartySize; // default party size for an available bookings request
@@ -28,7 +28,6 @@
 @property (nullable, NS_NONATOMIC_IOSONLY) NSNumber *maximumPartySize;
 @property (nullable, NS_NONATOMIC_IOSONLY) NSNumber *minimumPartySize;
 @property (copy, NS_NONATOMIC_IOSONLY) INImage *providerImage;
-@property (nullable, copy, NS_NONATOMIC_IOSONLY) INRestaurantMarketingPreferences *restaurantMarketingPreferences; // Optional means for allowing restaurant to express desire to communicate directly with the guest, given guest consent.
 
 - (instancetype)initWithDefaultPartySize:(NSUInteger)defaultPartySize defaultBookingDate:(NSDate *)defaultBookingDate code:(INGetAvailableRestaurantReservationBookingDefaultsIntentResponseCode)code userActivity:(nullable NSUserActivity *)userActivity NS_DESIGNATED_INITIALIZER;
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingsIntent.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingsIntent.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingsIntent.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingsIntent.h	2016-07-25 07:26:52.000000000 +0200
@@ -11,16 +11,20 @@
 #import <Intents/INIntent.h>
 #import <Intents/INIntentResolutionResult.h>
 #import <Intents/INRestaurant.h>
+#import <Intents/INRestaurantResolutionResult.h>
+#import <Intents/INIntegerResolutionResult.h>
+#import <Intents/INDateComponentsResolutionResult.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INGetAvailableRestaurantReservationBookingsIntent : INIntent <NSCopying>
 
 @property (copy, NS_NONATOMIC_IOSONLY) INRestaurant *restaurant;
 @property (NS_NONATOMIC_IOSONLY) NSUInteger partySize;
 
-@property (copy, nullable, NS_NONATOMIC_IOSONLY) NSDate *preferredBookingDate;
+@property (copy, nullable, NS_NONATOMIC_IOSONLY) NSDateComponents *preferredBookingDateComponents;
 
 @property (copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *maximumNumberOfResults; // if the caller has a preferred maximum number of results, one can optionally be specified. a nil here leaves it up to the extension
 
@@ -31,6 +35,8 @@
 
 @class INGetAvailableRestaurantReservationBookingsIntentResponse;
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INGetAvailableRestaurantReservationBookingsIntentHandling <NSObject>
 
 /*!
@@ -46,7 +52,7 @@
  
  */
 
-- (void)handleGetAvailableRestaurantReservationBookings:(INGetAvailableRestaurantReservationBookingsIntent *)showBookingsIntent completion:(void (^)(INGetAvailableRestaurantReservationBookingsIntentResponse *response))completion NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_SWIFT_NAME(handle(getAvailableRestaurantReservationBookings:completion:));
+- (void)handleGetAvailableRestaurantReservationBookings:(INGetAvailableRestaurantReservationBookingsIntent *)intent completion:(void (^)(INGetAvailableRestaurantReservationBookingsIntentResponse *response))completion NS_SWIFT_NAME(handle(getAvailableRestaurantReservationBookings:completion:));
 
 @optional
 
@@ -62,7 +68,7 @@
  
  */
 
-- (void)confirmGetAvailableRestaurantReservationBookings:(INGetAvailableRestaurantReservationBookingsIntent *)showBookingsIntent completion:(void (^)(INGetAvailableRestaurantReservationBookingsIntentResponse *response))completion NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_SWIFT_NAME(confirm(getAvailableRestaurantReservationBookings:completion:));
+- (void)confirmGetAvailableRestaurantReservationBookings:(INGetAvailableRestaurantReservationBookingsIntent *)intent completion:(void (^)(INGetAvailableRestaurantReservationBookingsIntentResponse *response))completion NS_SWIFT_NAME(confirm(getAvailableRestaurantReservationBookings:completion:));
 
 /*!
  @brief Resolution methods
@@ -76,9 +82,9 @@
  
  */
 
-- (void)resolveRestaurantForGetAvailableRestaurantReservationBookings:(INGetAvailableRestaurantReservationBookingsIntent *)showBookingsIntent completion:(void(^)(INIntentResolutionResult<INRestaurant *> *resolutionResult))completion NS_SWIFT_NAME(resolveRestaurant(for:completion:));
-- (void)resolvePartySizeForGetAvailableRestaurantReservationBookings:(INGetAvailableRestaurantReservationBookingsIntent *)showBookingsIntent completion:(void(^)(INIntentResolutionResult<NSNumber *> *resolutionResult))completion NS_SWIFT_NAME(resolvePartySize(for:completion:));
-- (void)resolvePreferredBookingDateForGetAvailableRestaurantReservationBookings:(INGetAvailableRestaurantReservationBookingsIntent *)showBookingsIntent completion:(void(^)(INIntentResolutionResult<NSDate *> *resolutionResult))completion NS_SWIFT_NAME(resolvePreferredBookingDate(for:completion:));
+- (void)resolveRestaurantForGetAvailableRestaurantReservationBookings:(INGetAvailableRestaurantReservationBookingsIntent *)intent withCompletion:(void(^)(INRestaurantResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveRestaurant(for:completion:));
+- (void)resolvePartySizeForGetAvailableRestaurantReservationBookings:(INGetAvailableRestaurantReservationBookingsIntent *)intent withCompletion:(void(^)(INIntegerResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolvePartySize(for:completion:));
+- (void)resolvePreferredBookingDateComponentsForGetAvailableRestaurantReservationBookings:(INGetAvailableRestaurantReservationBookingsIntent *)intent withCompletion:(void(^)(INDateComponentsResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolvePreferredBookingDateComponents(for:completion:));
 
 @end
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingsIntentResponse.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingsIntentResponse.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingsIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingsIntentResponse.h	2016-07-25 07:30:56.000000000 +0200
@@ -21,7 +21,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INGetAvailableRestaurantReservationBookingsIntentResponse : INIntentResponse
 
 - (instancetype)initWithAvailableBookings:(NSArray<INRestaurantReservationBooking *> *)availableBookings code:(INGetAvailableRestaurantReservationBookingsIntentCode)code userActivity:(nullable NSUserActivity *)userActivity NS_DESIGNATED_INITIALIZER;
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRestaurantGuestIntent.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRestaurantGuestIntent.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRestaurantGuestIntent.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRestaurantGuestIntent.h	2016-07-25 07:30:56.000000000 +0200
@@ -13,13 +13,16 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INGetRestaurantGuestIntent : INIntent
 
 @end
 
 @class INGetRestaurantGuestIntentResponse;
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INGetRestaurantGuestIntentHandling <NSObject>
 
 /*!
@@ -34,7 +37,7 @@
  @see  INGetRestaurantGuestIntentResponse
  
  */
-- (void)handleGetRestaurantGuest:(INGetRestaurantGuestIntent *)guestIntent completion:(void (^)(INGetRestaurantGuestIntentResponse *response))completion NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_SWIFT_NAME(handle(getRestaurantGuest:completion:));
+- (void)handleGetRestaurantGuest:(INGetRestaurantGuestIntent *)intent completion:(void (^)(INGetRestaurantGuestIntentResponse *response))completion NS_SWIFT_NAME(handle(getRestaurantGuest:completion:));
 
 @optional
 
@@ -50,7 +53,7 @@
  
  */
 
-- (void)confirmGetRestaurantGuest:(INGetRestaurantGuestIntent *)guestIntent completion:(void (^)(INGetRestaurantGuestIntentResponse *response))completion NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_SWIFT_NAME(confirm(getRestaurantGuest:completion:));
+- (void)confirmGetRestaurantGuest:(INGetRestaurantGuestIntent *)guestIntent completion:(void (^)(INGetRestaurantGuestIntentResponse *response))completion NS_SWIFT_NAME(confirm(getRestaurantGuest:completion:));
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRestaurantGuestIntentResponse.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRestaurantGuestIntentResponse.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRestaurantGuestIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRestaurantGuestIntentResponse.h	2016-07-25 07:30:56.000000000 +0200
@@ -19,7 +19,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INGetRestaurantGuestIntentResponse : INIntentResponse
 
 - (instancetype)initWithCode:(INGetRestaurantGuestIntentResponseCode)code userActivity:(nullable NSUserActivity *)userActivity NS_DESIGNATED_INITIALIZER;
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetUserCurrentRestaurantReservationBookingsIntent.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetUserCurrentRestaurantReservationBookingsIntent.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetUserCurrentRestaurantReservationBookingsIntent.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetUserCurrentRestaurantReservationBookingsIntent.h	2016-07-25 07:26:52.000000000 +0200
@@ -11,10 +11,12 @@
 #import <Intents/INIntent.h>
 #import <Intents/INIntentResolutionResult.h>
 #import <Intents/INRestaurant.h>
+#import <Intents/INRestaurantResolutionResult.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INGetUserCurrentRestaurantReservationBookingsIntent : INIntent <NSCopying>
 
 @property (copy, nullable, NS_NONATOMIC_IOSONLY) INRestaurant *restaurant; // optional filter to just reservations at restaurant
@@ -27,6 +29,8 @@
 
 @class INGetUserCurrentRestaurantReservationBookingsIntentResponse;
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INGetUserCurrentRestaurantReservationBookingsIntentHandling <NSObject>
 
 /*!
@@ -42,7 +46,7 @@
  
  */
 
-- (void)handleGetUserCurrentRestaurantReservationBookings:(INGetUserCurrentRestaurantReservationBookingsIntent *)showCurrentBookingsIntent completion:(void (^)(INGetUserCurrentRestaurantReservationBookingsIntentResponse *response))completion NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_SWIFT_NAME(handle(getUserCurrentRestaurantReservationBookings:completion:));
+- (void)handleGetUserCurrentRestaurantReservationBookings:(INGetUserCurrentRestaurantReservationBookingsIntent *)intent completion:(void (^)(INGetUserCurrentRestaurantReservationBookingsIntentResponse *response))completion NS_SWIFT_NAME(handle(getUserCurrentRestaurantReservationBookings:completion:));
 
 @optional
 
@@ -58,7 +62,7 @@
  
  */
 
-- (void)confirmGetUserCurrentRestaurantReservationBookings:(INGetUserCurrentRestaurantReservationBookingsIntent *)showCurrentBookingsIntent completion:(void (^)(INGetUserCurrentRestaurantReservationBookingsIntentResponse *response))completion NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_SWIFT_NAME(confirm(getUserCurrentRestaurantReservationBookings:completion:));
+- (void)confirmGetUserCurrentRestaurantReservationBookings:(INGetUserCurrentRestaurantReservationBookingsIntent *)intent completion:(void (^)(INGetUserCurrentRestaurantReservationBookingsIntentResponse *response))completion NS_SWIFT_NAME(confirm(getUserCurrentRestaurantReservationBookings:completion:));
 
 /*!
  @brief Resolution methods
@@ -72,7 +76,7 @@
  
  */
 
-- (void)resolveRestaurantForGetUserCurrentRestaurantReservationBookings:(INGetUserCurrentRestaurantReservationBookingsIntent *)showCurrentBookingsIntent completion:(void(^)(INIntentResolutionResult<INRestaurant *> *resolutionResult))completion NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_SWIFT_NAME(resolveRestaurant(for:completion:));;
+- (void)resolveRestaurantForGetUserCurrentRestaurantReservationBookings:(INGetUserCurrentRestaurantReservationBookingsIntent *)intent withCompletion:(void(^)(INRestaurantResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveRestaurant(for:completion:));
 
 @end
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetUserCurrentRestaurantReservationBookingsIntentResponse.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetUserCurrentRestaurantReservationBookingsIntentResponse.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetUserCurrentRestaurantReservationBookingsIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetUserCurrentRestaurantReservationBookingsIntentResponse.h	2016-07-25 07:30:57.000000000 +0200
@@ -20,7 +20,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INGetUserCurrentRestaurantReservationBookingsIntentResponse : INIntentResponse
 
 - (instancetype)initWithUserCurrentBookings:(NSArray<INRestaurantReservationUserBooking *> *)userCurrentBookings code:(INGetUserCurrentRestaurantReservationBookingsIntentResponseCode)code userActivity:(nullable NSUserActivity *)userActivity NS_DESIGNATED_INITIALIZER;
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h	2016-07-25 07:30:56.000000000 +0200
@@ -15,7 +15,6 @@
 - (instancetype)init NS_UNAVAILABLE;
 
 // This result is to tell Siri that the user must provide a non-nil value for this parameter in order to continue
-// If the current value of this parameter is already non-nil, but the app extension wants to request more details, it can indicate this using +resolutionResultNeedsMoreDetails
 + (instancetype)needsValue NS_SWIFT_NAME(needsValue());
 
 // This result is to tell Siri to continue whether or the user has provided a value for this parameter
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentRestaurantReservation.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentRestaurantReservation.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentRestaurantReservation.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentRestaurantReservation.h	2016-07-25 07:30:57.000000000 +0200
@@ -8,21 +8,20 @@
 //
 // http://mapsconnect.apple.com/info/extensions
 
-#import "INRestaurantGuest.h"
-#import "INTermsAndConditions.h"
-#import "INRestaurantGuestDisplayPreferences.h"
-#import "INRestaurantReservationBooking.h"
-#import "INRestaurantReservationUserBooking.h"
-#import "INBookRestaurantReservationIntent.h"
-#import "INGetAvailableRestaurantReservationBookingsIntent.h"
-#import "INGetUserCurrentRestaurantReservationBookingsIntent.h"
-#import "INGetAvailableRestaurantReservationBookingDefaultsIntent.h"
-#import "INBookRestaurantReservationIntentResponse.h"
-#import "INGetAvailableRestaurantReservationBookingsIntentResponse.h"
-#import "INGetUserCurrentRestaurantReservationBookingsIntentResponse.h"
-#import "INGetAvailableRestaurantReservationBookingDefaultsIntentResponse.h"
-#import "INRestaurant.h"
-#import "INRestaurantMarketingPreferences.h"
-#import "INRestaurantOffer.h"
-#import "INGetRestaurantGuestIntent.h"
-#import "INGetRestaurantGuestIntentResponse.h"
+#import <Intents/INRestaurantGuest.h>
+#import <Intents/INTermsAndConditions.h>
+#import <Intents/INRestaurantGuestDisplayPreferences.h>
+#import <Intents/INRestaurantReservationBooking.h>
+#import <Intents/INRestaurantReservationUserBooking.h>
+#import <Intents/INBookRestaurantReservationIntent.h>
+#import <Intents/INGetAvailableRestaurantReservationBookingsIntent.h>
+#import <Intents/INGetUserCurrentRestaurantReservationBookingsIntent.h>
+#import <Intents/INGetAvailableRestaurantReservationBookingDefaultsIntent.h>
+#import <Intents/INBookRestaurantReservationIntentResponse.h>
+#import <Intents/INGetAvailableRestaurantReservationBookingsIntentResponse.h>
+#import <Intents/INGetUserCurrentRestaurantReservationBookingsIntentResponse.h>
+#import <Intents/INGetAvailableRestaurantReservationBookingDefaultsIntentResponse.h>
+#import <Intents/INRestaurant.h>
+#import <Intents/INRestaurantOffer.h>
+#import <Intents/INGetRestaurantGuestIntent.h>
+#import <Intents/INGetRestaurantGuestIntentResponse.h>
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h	2016-07-25 07:30:57.000000000 +0200
@@ -17,7 +17,6 @@
     INIntentHandlingStatusSuccess,
     INIntentHandlingStatusFailure,
     INIntentHandlingStatusDeferredToApplication,
-    INIntentHandlingStatusDone = INIntentHandlingStatusSuccess, // Deprecated - please use 'Success' and 'Failure'.
 } API_AVAILABLE(macosx(10.12), ios(10.0));
 
 typedef NS_ENUM(NSInteger, INInteractionDirection) {
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INListRideOptionsIntentResponse.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INListRideOptionsIntentResponse.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INListRideOptionsIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INListRideOptionsIntentResponse.h	2016-07-25 07:30:57.000000000 +0200
@@ -42,8 +42,6 @@
 
 @property (readwrite, copy, nullable, NS_NONATOMIC_IOSONLY) NSArray<INPaymentMethod *> *paymentMethods;
 
-@property (readwrite, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *supportsApplePayForPayment NS_REFINED_FOR_SWIFT;
-
 @property (readwrite, copy, nullable, NS_NONATOMIC_IOSONLY) NSDate *expirationDate;
 
 @end
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentMethod.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentMethod.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentMethod.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentMethod.h	2016-07-25 07:30:57.000000000 +0200
@@ -34,6 +34,9 @@
 // An image that represents this payment method (e.g. the card's brand).
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INImage *icon;
 
+// This payment method represents Apple Pay. Its .type will be INPaymentMethodTypeApplePay. The .name, .identificationHint and .icon properties are not significant for this type of payment method.
++ (instancetype)applePayPaymentMethod;
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentMethodType.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentMethodType.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentMethodType.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentMethodType.h	2016-07-25 07:30:57.000000000 +0200
@@ -21,6 +21,7 @@
     INPaymentMethodTypeCredit,
     INPaymentMethodTypePrepaid,
     INPaymentMethodTypeStore,
+    INPaymentMethodTypeApplePay,
 };
 
 #endif // INPaymentMethodType_h
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentRecord.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentRecord.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentRecord.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentRecord.h	2016-07-25 07:30:57.000000000 +0200
@@ -26,7 +26,15 @@
                         currencyAmount:(nullable INCurrencyAmount *)currencyAmount
                          paymentMethod:(nullable INPaymentMethod *)paymentMethod
                                   note:(nullable NSString *)note
-                                status:(INPaymentStatus)status NS_DESIGNATED_INITIALIZER;
+                                status:(INPaymentStatus)status
+                             feeAmount:(nullable INCurrencyAmount *)feeAmount NS_DESIGNATED_INITIALIZER;
+
+- (nullable instancetype)initWithPayee:(nullable INPerson *)payee
+                                 payer:(nullable INPerson *)payer
+                        currencyAmount:(nullable INCurrencyAmount *)currencyAmount
+                         paymentMethod:(nullable INPaymentMethod *)paymentMethod
+                                  note:(nullable NSString *)note
+                                status:(INPaymentStatus)status;
 
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INPerson *payee;
 
@@ -43,6 +51,8 @@
 
 @property (readonly, assign, NS_NONATOMIC_IOSONLY) INPaymentStatus status;
 
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INCurrencyAmount *feeAmount;
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h	2016-07-25 07:30:57.000000000 +0200
@@ -23,9 +23,6 @@
 // This resolution result is to ask Siri to confirm if this is the person with which the user wants to continue.
 + (instancetype)confirmationRequiredWithPersonToConfirm:(nullable INPerson *)personToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
 
-// This resolution result is to inform Siri that in order to continue, the app extension needs the person to be filled in greater detail. If this parameter is nil and the app extension wants to request a non-nil value, it should use +needsValue.
-+ (instancetype)needsMoreDetailsForPerson:(INPerson *)personToComplete NS_SWIFT_NAME(needsMoreDetails(for:));
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPhotoAttributeOptionsResolutionResult.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPhotoAttributeOptionsResolutionResult.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPhotoAttributeOptionsResolutionResult.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPhotoAttributeOptionsResolutionResult.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,24 +0,0 @@
-//
-//  INPhotoAttributeOptionsResolutionResult.h
-//  Intents
-//
-//  Copyright © 2016 Apple. All rights reserved.
-//
-
-#import <Intents/INIntentResolutionResult.h>
-
-#import <Intents/INPhotoAttributeOptions.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-@interface INPhotoAttributeOptionsResolutionResult : INIntentResolutionResult
-
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
-+ (instancetype)successWithResolvedValue:(INPhotoAttributeOptions)resolvedValue NS_SWIFT_NAME(success(with:));
-
-// This resolution result is to ask Siri to confirm if this is the value with which the user wants to continue.
-+ (instancetype)confirmationRequiredWithValueToConfirm:(INPhotoAttributeOptions)valueToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h	2016-07-25 07:30:57.000000000 +0200
@@ -23,9 +23,6 @@
 // This resolution result is to ask Siri to confirm if this is the placemark with which the user wants to continue.
 + (instancetype)confirmationRequiredWithPlacemarkToConfirm:(nullable CLPlacemark *)placemarkToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
 
-// This resolution result is to inform Siri that in order to continue, the app extension needs the placemark to be filled in greater detail. If this parameter is nil and the app extension wants to request a non-nil value, it should use +needsValue.
-+ (instancetype)needsMoreDetailsForPlacemark:(CLPlacemark *)placemarkToComplete NS_SWIFT_NAME(needsMoreDetails(for:));
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestPaymentIntentResponse.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestPaymentIntentResponse.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestPaymentIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestPaymentIntentResponse.h	2016-07-25 07:30:56.000000000 +0200
@@ -16,6 +16,11 @@
     INRequestPaymentIntentResponseCodeSuccess,
     INRequestPaymentIntentResponseCodeFailure,
     INRequestPaymentIntentResponseCodeFailureRequiringAppLaunch,
+    INRequestPaymentIntentResponseCodeFailureCredentialsUnverified,
+    INRequestPaymentIntentResponseCodeFailurePaymentsAmountBelowMinimum,
+    INRequestPaymentIntentResponseCodeFailurePaymentsAmountAboveMaximum,
+    INRequestPaymentIntentResponseCodeFailurePaymentsCurrencyUnsupported,
+    INRequestPaymentIntentResponseCodeFailureNoBankAccount,
 } API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestRideIntent.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestRideIntent.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestRideIntent.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestRideIntent.h	2016-07-25 07:26:52.000000000 +0200
@@ -13,7 +13,7 @@
 @class INSpeakableString;
 @class INSpeakableStringResolutionResult;
 @class INIntegerResolutionResult;
-@class INBooleanResolutionResult;
+@class INPaymentMethod;
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -25,8 +25,7 @@
                        dropOffLocation:(nullable CLPlacemark *)dropOffLocation
                         rideOptionName:(nullable INSpeakableString *)rideOptionName
                              partySize:(nullable NSNumber *)partySize
-                     paymentMethodName:(nullable INSpeakableString *)paymentMethodName
-                usesApplePayForPayment:(nullable NSNumber *)usesApplePayForPayment NS_DESIGNATED_INITIALIZER NS_REFINED_FOR_SWIFT;
+                         paymentMethod:(nullable INPaymentMethod *)paymentMethod NS_DESIGNATED_INITIALIZER NS_REFINED_FOR_SWIFT;
 
 // Specifies the location to to begin the ride.
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) CLPlacemark *pickupLocation;
@@ -39,9 +38,7 @@
 // Defines the number of people in the party requesting the ride.
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *partySize NS_REFINED_FOR_SWIFT;
 
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INSpeakableString *paymentMethodName;
-
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *usesApplePayForPayment NS_REFINED_FOR_SWIFT;
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INPaymentMethod *paymentMethod;
 
 @end
 
@@ -115,12 +112,6 @@
 - (void)resolvePartySizeForRequestRide:(INRequestRideIntent *)intent
                         withCompletion:(void (^)(INIntegerResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolvePartySize(forRequestRide:with:));
 
-- (void)resolvePaymentMethodNameForRequestRide:(INRequestRideIntent *)intent
-                                withCompletion:(void (^)(INSpeakableStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolvePaymentMethodName(forRequestRide:with:));
-
-- (void)resolveUsesApplePayForPaymentForRequestRide:(INRequestRideIntent *)intent
-                                     withCompletion:(void (^)(INBooleanResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveUsesApplePayForPayment(forRequestRide:with:));
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurant.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurant.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurant.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurant.h	2016-07-25 07:30:57.000000000 +0200
@@ -13,7 +13,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INRestaurant : NSObject <NSSecureCoding, NSCopying>
 
 - (instancetype)initWithLocation:(CLLocation *)location name:(NSString *)name vendorIdentifier:(NSString *)vendorIdentifier restaurantIdentifier:(NSString *)restaurantIdentifier NS_DESIGNATED_INITIALIZER;
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuest.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuest.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuest.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuest.h	2016-07-25 07:30:57.000000000 +0200
@@ -12,7 +12,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INRestaurantGuest : INPerson
 
 - (instancetype)initWithNameComponents:(nullable NSPersonNameComponents *)nameComponents phoneNumber:(nullable NSString *)phoneNumber emailAddress:(nullable NSString *)emailAddress NS_DESIGNATED_INITIALIZER;
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuestDisplayPreferences.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuestDisplayPreferences.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuestDisplayPreferences.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuestDisplayPreferences.h	2016-07-25 07:30:57.000000000 +0200
@@ -8,7 +8,8 @@
 //
 // http://mapsconnect.apple.com/info/extensions
 
-NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INRestaurantGuestDisplayPreferences : NSObject <NSSecureCoding, NSCopying>
 
 @property (NS_NONATOMIC_IOSONLY) BOOL nameFieldFirstNameOptional; // indicates whether first name field is marked optional, defaults to NO
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuestResolutionResult.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuestResolutionResult.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuestResolutionResult.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuestResolutionResult.h	2016-07-25 07:30:57.000000000 +0200
@@ -0,0 +1,31 @@
+//
+//  INRestaurantGuestResolutionResult.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+//  This API requires you to work with Apple Maps before your application can use it. For information on how to get started, please go to MapsConnect.
+//
+//  http://mapsconnect.apple.com/info/extensions
+
+#import <Intents/INIntentResolutionResult.h>
+
+@class INRestaurantGuest;
+
+NS_ASSUME_NONNULL_BEGIN
+
+API_AVAILABLE(ios(10.0))
+@interface INRestaurantGuestResolutionResult : INIntentResolutionResult
+
+// This resolution result is for when the app extension wants to tell Siri to proceed with a given restaurant guest. The resolvedRestaurantGuest need not be identical to the input restaurant. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
++ (instancetype)successWithResolvedRestaurantGuest:(INRestaurantGuest *)resolvedRestaurantGuest NS_SWIFT_NAME(success(with:));
+
+// This resolution result is to ask Siri to disambiguate between the provided restaurant guests.
++ (instancetype)disambiguationWithRestaurantGuestsToDisambiguate:(NSArray<INRestaurantGuest *> *)restaurantGuestsToDisambiguate NS_SWIFT_NAME(disambiguation(with:));
+
+// This resolution result is to ask Siri to confirm if this is the restaurant guest with which the user wants to continue.
++ (instancetype)confirmationRequiredWithRestaurantGuestToConfirm:(nullable INRestaurantGuest *)restaurantGuestToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantMarketingPreferences.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantMarketingPreferences.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantMarketingPreferences.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantMarketingPreferences.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,37 +0,0 @@
-//
-//  INRestaurantMarketingPreferences.h
-//  Intents
-//
-//  Copyright © 2016 Apple. All rights reserved.
-//
-//  This API requires you to work with Apple Maps before your application can use it. For information on how to get started, please go to MapsConnect.
-//
-//  http://mapsconnect.apple.com/info/extensions
-
-#import <Foundation/Foundation.h>
-#import <Intents/INRestaurant.h>
-#import <Intents/INRestaurantGuest.h>
-
-typedef NS_ENUM(NSInteger, INRestaurantMarketingPreferencesContactMethod) {
-    INRestaurantMarketingPreferencesContactMethodUndefined = 0,
-    INRestaurantMarketingPreferencesContactMethodEmail
-};
-
-NS_ASSUME_NONNULL_BEGIN
-
-NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
-@interface INRestaurantMarketingPreferences : NSObject <NSSecureCoding, NSCopying>
-
-- (instancetype)init NS_UNAVAILABLE;
-
-- (instancetype)initWithContactMethod:(INRestaurantMarketingPreferencesContactMethod)contactMethod guestHasOptedInToMarketing:(BOOL)guestHasOptedInToMarketing  localizedDescriptionForMarketingEnabled:(NSString *)localizedDescriptionForMarketingEnabled localizedDescriptionForMarketingNotEnabled:(NSString * __nullable)localizedDescriptionForMarketingNotEnabled NS_DESIGNATED_INITIALIZER;
-
-@property (NS_NONATOMIC_IOSONLY, readonly) INRestaurantMarketingPreferencesContactMethod contactMethod;
-
-@property (NS_NONATOMIC_IOSONLY) BOOL guestHasOptedInToMarketing;
-
-@property (NS_NONATOMIC_IOSONLY, readonly) NSString *localizedDescriptionForMarketingEnabled; // A localized description of consequences, both legal and practical, of opting into receiving marketing from restaurant
-@property (NS_NONATOMIC_IOSONLY, nullable, readonly) NSString *localizedDescriptionForMarketingNotEnabled; // An optional localized description of practical consequences of not opting into receiving marketing from restaurant.
-
-@end
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantOffer.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantOffer.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantOffer.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantOffer.h	2016-07-25 07:30:57.000000000 +0200
@@ -12,7 +12,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INRestaurantOffer : NSObject <NSSecureCoding, NSCopying>
 
 @property (copy, NS_NONATOMIC_IOSONLY) NSString *offerTitleText;
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantReservationBooking.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantReservationBooking.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantReservationBooking.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantReservationBooking.h	2016-07-25 07:30:57.000000000 +0200
@@ -14,7 +14,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 // represents a booking at a restaurant during a given time for a given party size
 @interface INRestaurantReservationBooking : NSObject <NSSecureCoding, NSCopying>
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantReservationUserBooking.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantReservationUserBooking.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantReservationUserBooking.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantReservationUserBooking.h	2016-07-25 07:30:57.000000000 +0200
@@ -19,7 +19,8 @@
     INRestaurantReservationUserBookingStatusDenied
 };
 
-NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 NS_ASSUME_NONNULL_BEGIN
 @interface INRestaurantReservationUserBooking : INRestaurantReservationBooking <NSCopying>
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantResolutionResult.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantResolutionResult.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantResolutionResult.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantResolutionResult.h	2016-07-25 07:30:57.000000000 +0200
@@ -0,0 +1,31 @@
+//
+//  INRestaurantResolutionResult.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+//  This API requires you to work with Apple Maps before your application can use it. For information on how to get started, please go to MapsConnect.
+//
+//  http://mapsconnect.apple.com/info/extensions
+
+#import <Intents/INIntentResolutionResult.h>
+
+@class INRestaurant;
+
+NS_ASSUME_NONNULL_BEGIN
+
+API_AVAILABLE(ios(10.0))
+@interface INRestaurantResolutionResult : INIntentResolutionResult
+
+// This resolution result is for when the app extension wants to tell Siri to proceed with a given restaurant. The resolvedRestaurant need not be identical to the input restaurant. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
++ (instancetype)successWithResolvedRestaurant:(INRestaurant *)resolvedRestaurant NS_SWIFT_NAME(success(with:));
+
+// This resolution result is to ask Siri to disambiguate between the provided restaurants.
++ (instancetype)disambiguationWithRestaurantsToDisambiguate:(NSArray<INRestaurant *> *)restaurantsToDisambiguate NS_SWIFT_NAME(disambiguation(with:));
+
+// This resolution result is to ask Siri to confirm if this is the restaurant with which the user wants to continue.
++ (instancetype)confirmationRequiredWithRestaurantToConfirm:(nullable INRestaurant *)restaurantToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntent.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntent.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntent.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntent.h	2016-07-25 07:30:57.000000000 +0200
@@ -9,7 +9,6 @@
 #import <Intents/INIntentResolutionResult.h>
 
 @class INIntegerResolutionResult;
-@class INStringResolutionResult;
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -87,9 +86,6 @@
 - (void)resolveProfileNumberForSaveProfileInCar:(INSaveProfileInCarIntent *)intent
                                  withCompletion:(void (^)(INIntegerResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveProfileNumber(forSaveProfileInCar:with:));
 
-- (void)resolveProfileLabelForSaveProfileInCar:(INSaveProfileInCarIntent *)intent
-                                withCompletion:(void (^)(INStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveProfileLabel(forSaveProfileInCar:with:));
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h	2016-07-23 21:09:47.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h	2016-07-12 07:04:02.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h	2016-07-25 07:30:57.000000000 +0200
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
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntent.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntent.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntent.h	2016-07-11 07:05:57.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntent.h	2016-07-25 07:30:57.000000000 +0200
@@ -16,7 +16,6 @@
 @class CLPlacemark;
 @class INPlacemarkResolutionResult;
 @class INStringResolutionResult;
-@class INPhotoAttributeOptionsResolutionResult;
 @class INPerson;
 @class INPersonResolutionResult;
 
@@ -130,15 +129,6 @@
 - (void)resolveAlbumNameForSearchForPhotos:(INSearchForPhotosIntent *)intent
                             withCompletion:(void (^)(INStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveAlbumName(forSearchForPhotos:with:));
 
-- (void)resolveSearchTermsForSearchForPhotos:(INSearchForPhotosIntent *)intent
-                              withCompletion:(void (^)(NSArray<INStringResolutionResult *> *resolutionResults))completion NS_SWIFT_NAME(resolveSearchTerms(forSearchForPhotos:with:));
-
-- (void)resolveIncludedAttributesForSearchForPhotos:(INSearchForPhotosIntent *)intent
-                                     withCompletion:(void (^)(INPhotoAttributeOptionsResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveIncludedAttributes(forSearchForPhotos:with:));
-
-- (void)resolveExcludedAttributesForSearchForPhotos:(INSearchForPhotosIntent *)intent
-                                     withCompletion:(void (^)(INPhotoAttributeOptionsResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveExcludedAttributes(forSearchForPhotos:with:));
-
 - (void)resolvePeopleInPhotoForSearchForPhotos:(INSearchForPhotosIntent *)intent
                                 withCompletion:(void (^)(NSArray<INPersonResolutionResult *> *resolutionResults))completion NS_SWIFT_NAME(resolvePeopleInPhoto(forSearchForPhotos:with:));
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h	2016-07-25 07:26:52.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h	2016-07-25 07:30:57.000000000 +0200
@@ -14,6 +14,7 @@
     INSendMessageIntentResponseCodeSuccess,
     INSendMessageIntentResponseCodeFailure,
     INSendMessageIntentResponseCodeFailureRequiringAppLaunch,
+    INSendMessageIntentResponseCodeFailureMessageServiceNotAvailable,
 } API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendPaymentIntentResponse.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendPaymentIntentResponse.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendPaymentIntentResponse.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendPaymentIntentResponse.h	2016-07-25 07:30:57.000000000 +0200
@@ -16,6 +16,12 @@
     INSendPaymentIntentResponseCodeSuccess,
     INSendPaymentIntentResponseCodeFailure,
     INSendPaymentIntentResponseCodeFailureRequiringAppLaunch,
+    INSendPaymentIntentResponseCodeFailureCredentialsUnverified,
+    INSendPaymentIntentResponseCodeFailurePaymentsAmountBelowMinimum,
+    INSendPaymentIntentResponseCodeFailurePaymentsAmountAboveMaximum,
+    INSendPaymentIntentResponseCodeFailurePaymentsCurrencyUnsupported,
+    INSendPaymentIntentResponseCodeFailureInsufficientFunds,
+    INSendPaymentIntentResponseCodeFailureNoBankAccount,
 } API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntent.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntent.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntent.h	2016-07-11 07:05:57.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntent.h	2016-07-25 07:26:52.000000000 +0200
@@ -17,7 +17,6 @@
 @class INIntegerResolutionResult;
 @class INDoubleResolutionResult;
 @class INRelativeSettingResolutionResult;
-@class INTemperature;
 @class INTemperatureResolutionResult;
 @class INCarSeatResolutionResult;
 
@@ -35,7 +34,7 @@
                     fanSpeedIndex:(nullable NSNumber *)fanSpeedIndex
                fanSpeedPercentage:(nullable NSNumber *)fanSpeedPercentage
           relativeFanSpeedSetting:(INRelativeSetting)relativeFanSpeedSetting
-                      temperature:(nullable INTemperature *)temperature
+                      temperature:(nullable NSMeasurement<NSUnitTemperature *> *)temperature
        relativeTemperatureSetting:(INRelativeSetting)relativeTemperatureSetting
                       climateZone:(INCarSeat)climateZone NS_DESIGNATED_INITIALIZER NS_REFINED_FOR_SWIFT;
 
@@ -55,7 +54,7 @@
 
 @property (readonly, assign, NS_NONATOMIC_IOSONLY) INRelativeSetting relativeFanSpeedSetting;
 
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INTemperature *temperature;
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSMeasurement<NSUnitTemperature *> *temperature;
 
 @property (readonly, assign, NS_NONATOMIC_IOSONLY) INRelativeSetting relativeTemperatureSetting;
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntent.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntent.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntent.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntent.h	2016-07-25 07:30:57.000000000 +0200
@@ -9,7 +9,6 @@
 #import <Intents/INIntentResolutionResult.h>
 
 @class INIntegerResolutionResult;
-@class INStringResolutionResult;
 @class INBooleanResolutionResult;
 
 NS_ASSUME_NONNULL_BEGIN
@@ -91,9 +90,6 @@
 - (void)resolveProfileNumberForSetProfileInCar:(INSetProfileInCarIntent *)intent
                                 withCompletion:(void (^)(INIntegerResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveProfileNumber(forSetProfileInCar:with:));
 
-- (void)resolveProfileLabelForSetProfileInCar:(INSetProfileInCarIntent *)intent
-                               withCompletion:(void (^)(INStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveProfileLabel(forSetProfileInCar:with:));
-
 - (void)resolveDefaultProfileForSetProfileInCar:(INSetProfileInCarIntent *)intent
                                  withCompletion:(void (^)(INBooleanResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveDefaultProfile(forSetProfileInCar:with:));
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntent.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntent.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntent.h	2016-07-11 07:05:57.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntent.h	2016-07-25 07:26:52.000000000 +0200
@@ -16,7 +16,6 @@
 @class CLPlacemark;
 @class INPlacemarkResolutionResult;
 @class INStringResolutionResult;
-@class INPhotoAttributeOptionsResolutionResult;
 @class INPerson;
 @class INPersonResolutionResult;
 
@@ -130,15 +129,6 @@
 - (void)resolveAlbumNameForStartPhotoPlayback:(INStartPhotoPlaybackIntent *)intent
                                withCompletion:(void (^)(INStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveAlbumName(forStartPhotoPlayback:with:));
 
-- (void)resolveSearchTermsForStartPhotoPlayback:(INStartPhotoPlaybackIntent *)intent
-                                 withCompletion:(void (^)(NSArray<INStringResolutionResult *> *resolutionResults))completion NS_SWIFT_NAME(resolveSearchTerms(forStartPhotoPlayback:with:));
-
-- (void)resolveIncludedAttributesForStartPhotoPlayback:(INStartPhotoPlaybackIntent *)intent
-                                        withCompletion:(void (^)(INPhotoAttributeOptionsResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveIncludedAttributes(forStartPhotoPlayback:with:));
-
-- (void)resolveExcludedAttributesForStartPhotoPlayback:(INStartPhotoPlaybackIntent *)intent
-                                        withCompletion:(void (^)(INPhotoAttributeOptionsResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveExcludedAttributes(forStartPhotoPlayback:with:));
-
 - (void)resolvePeopleInPhotoForStartPhotoPlayback:(INStartPhotoPlaybackIntent *)intent
                                    withCompletion:(void (^)(NSArray<INPersonResolutionResult *> *resolutionResults))completion NS_SWIFT_NAME(resolvePeopleInPhoto(forStartPhotoPlayback:with:));
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperature.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperature.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperature.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperature.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,27 +0,0 @@
-//
-//  INTemperature.h
-//  Intents
-//
-//  Copyright © 2016 Apple. All rights reserved.
-//
-
-#import <Foundation/Foundation.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx)
-@interface INTemperature : NSObject <NSCopying, NSSecureCoding>
-
-- (instancetype)init NS_UNAVAILABLE;
-
-- (instancetype)initWithUnit:(NSUnitTemperature *)unit
-                       value:(NSNumber *)value NS_DESIGNATED_INITIALIZER NS_REFINED_FOR_SWIFT;
-
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSUnitTemperature *unit;
-
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *value NS_REFINED_FOR_SWIFT;
-
-@end
-
-NS_ASSUME_NONNULL_END
-
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureResolutionResult.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureResolutionResult.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureResolutionResult.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureResolutionResult.h	2016-07-25 07:30:57.000000000 +0200
@@ -15,16 +15,13 @@
 @interface INTemperatureResolutionResult : INIntentResolutionResult
 
 // This resolution result is for when the app extension wants to tell Siri to proceed with a given temperature. The resolvedTemperature need not be identical to the input temperature. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
-+ (instancetype)successWithResolvedTemperature:(INTemperature *)resolvedTemperature NS_SWIFT_NAME(success(with:));
++ (instancetype)successWithResolvedTemperature:(NSMeasurement<NSUnitTemperature *> *)resolvedTemperature NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to disambiguate between the provided temperatures.
-+ (instancetype)disambiguationWithTemperaturesToDisambiguate:(NSArray<INTemperature *> *)temperaturesToDisambiguate NS_SWIFT_NAME(disambiguation(with:));
++ (instancetype)disambiguationWithTemperaturesToDisambiguate:(NSArray<NSMeasurement<NSUnitTemperature *> *> *)temperaturesToDisambiguate NS_SWIFT_NAME(disambiguation(with:));
 
 // This resolution result is to ask Siri to confirm if this is the temperature with which the user wants to continue.
-+ (instancetype)confirmationRequiredWithTemperatureToConfirm:(nullable INTemperature *)temperatureToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
-
-// This resolution result is to inform Siri that in order to continue, the app extension needs the temperature to be filled in greater detail. If this parameter is nil and the app extension wants to request a non-nil value, it should use +needsValue.
-+ (instancetype)needsMoreDetailsForTemperature:(INTemperature *)temperatureToComplete NS_SWIFT_NAME(needsMoreDetails(for:));
++ (instancetype)confirmationRequiredWithTemperatureToConfirm:(nullable NSMeasurement<NSUnitTemperature *> *)temperatureToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
 
 @end
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTermsAndConditions.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTermsAndConditions.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTermsAndConditions.h	2016-07-11 07:06:19.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTermsAndConditions.h	2016-07-25 07:30:57.000000000 +0200
@@ -10,7 +10,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INTermsAndConditions : NSObject <NSSecureCoding, NSCopying>
 
 - (instancetype)initWithLocalizedTermsAndConditionsText:(NSString *)localizedTermsAndConditionsText privacyPolicyURL:(nullable NSURL*)privacyPolicyURL termsAndConditionsURL:(nullable NSURL *)termsAndConditionsURL NS_DESIGNATED_INITIALIZER;
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h	2016-07-11 07:05:57.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h	2016-07-25 07:30:57.000000000 +0200
@@ -43,7 +43,6 @@
 #import <Intents/INPaymentMethod.h>
 #import <Intents/INPaymentMethodType.h>
 #import <Intents/INPerson.h>
-#import <Intents/INTemperature.h>
 #import <Intents/INSpeakableString.h>
 
 // Common Resolution Results
@@ -57,6 +56,9 @@
 #import <Intents/INSpeakableStringResolutionResult.h>
 #import <Intents/INStringResolutionResult.h>
 #import <Intents/INTemperatureResolutionResult.h>
+#import <Intents/INDateComponentsResolutionResult.h>
+#import <Intents/INRestaurantResolutionResult.h>
+#import <Intents/INRestaurantGuestResolutionResult.h>
 
 // Calls Domain
 #import <Intents/INSearchCallHistoryIntent.h>
@@ -69,7 +71,6 @@
 #import <Intents/INCallRecordType.h>
 #import <Intents/INCallRecordTypeResolutionResult.h>
 #import <Intents/INCallCapabilityOptions.h>
-#import <Intents/INCallCapabilityOptionsResolutionResult.h>
 
 // CarPlay & Radio Domains
 #import <Intents/INSetAudioSourceInCarIntent.h>
@@ -132,7 +133,6 @@
 #import <Intents/INStartPhotoPlaybackIntentResponse.h>
 
 #import <Intents/INPhotoAttributeOptions.h>
-#import <Intents/INPhotoAttributeOptionsResolutionResult.h>
 
 // Ridesharing Domain
 #import <Intents/INListRideOptionsIntent.h>

```