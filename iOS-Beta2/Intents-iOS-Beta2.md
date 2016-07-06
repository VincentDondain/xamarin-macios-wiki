#Intents.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/CLPlacemark+IntentsAdditions.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/CLPlacemark+IntentsAdditions.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/CLPlacemark+IntentsAdditions.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/CLPlacemark+IntentsAdditions.h	2016-06-26 09:15:29.000000000 +0200
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
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCancelWorkoutIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCancelWorkoutIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCancelWorkoutIntent.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCancelWorkoutIntent.h	2016-06-26 09:15:29.000000000 +0200
@@ -8,15 +8,18 @@
 #import <Intents/INIntent.h>
 #import <Intents/INIntentResolutionResult.h>
 
-@class INStringResolutionResult;
+@class INSpeakableString;
+@class INSpeakableStringResolutionResult;
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INCancelWorkoutIntent : INIntent
 
-- (instancetype)initWithWorkoutName:(nullable NSString *)workoutName NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithWorkoutName:(nullable INSpeakableString *)workoutName NS_DESIGNATED_INITIALIZER;
 
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *workoutName;
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INSpeakableString *workoutName;
 
 @end
 
@@ -28,6 +31,8 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INCancelWorkoutIntentHandling <NSObject>
 
 @required
@@ -77,7 +82,7 @@
  */
 
 - (void)resolveWorkoutNameForCancelWorkout:(INCancelWorkoutIntent *)intent
-                            withCompletion:(void (^)(INStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveWorkoutName(forCancelWorkout:with:));
+                            withCompletion:(void (^)(INSpeakableStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveWorkoutName(forCancelWorkout:with:));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCancelWorkoutIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCancelWorkoutIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCancelWorkoutIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCancelWorkoutIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -9,8 +9,8 @@
 
 typedef NS_ENUM(NSInteger, INCancelWorkoutIntentResponseCode) {
     INCancelWorkoutIntentResponseCodeUnspecified = 0,
-    INCancelWorkoutIntentResponseCodeInProgress,
-    INCancelWorkoutIntentResponseCodeSuccess,
+    INCancelWorkoutIntentResponseCodeReady,
+    INCancelWorkoutIntentResponseCodeContinueInApp,
     INCancelWorkoutIntentResponseCodeFailure,
     INCancelWorkoutIntentResponseCodeFailureRequiringAppLaunch,
     INCancelWorkoutIntentResponseCodeFailureNoMatchingWorkout,
@@ -18,6 +18,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INCancelWorkoutIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCarSeat.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCarSeat.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCarSeat.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCarSeat.h	2016-06-26 09:15:29.000000000 +0200
@@ -22,6 +22,9 @@
     INCarSeatRearLeft,
     INCarSeatRearRight,
     INCarSeatRear,
+    INCarSeatThirdRowLeft,
+    INCarSeatThirdRowRight,
+    INCarSeatThirdRow,
 };
 
 #endif // INCarSeat_h
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmount.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmount.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmount.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmount.h	2016-06-26 09:15:29.000000000 +0200
@@ -16,9 +16,9 @@
 - (instancetype)initWithAmount:(NSDecimalNumber *)amount
                   currencyCode:(NSString *)currencyCode NS_DESIGNATED_INITIALIZER;
 
-@property (readonly, copy, NS_NONATOMIC_IOSONLY) NSDecimalNumber *amount;
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSDecimalNumber *amount;
 
-@property (readonly, copy, NS_NONATOMIC_IOSONLY) NSString *currencyCode;
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *currencyCode;
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmountResolutionResult.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmountResolutionResult.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmountResolutionResult.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmountResolutionResult.h	2016-06-26 09:15:29.000000000 +0200
@@ -6,7 +6,6 @@
 //
 
 #import <Intents/INIntentResolutionResult.h>
-#import <Intents/INIntentResolutionResultUnsupportedReason.h>
 
 @class INCurrencyAmount;
 
@@ -26,10 +25,6 @@
 // This resolution result is to inform Siri that in order to continue, the app extension needs the currency amount to be filled in greater detail. If this parameter is nil and the app extension wants to request a non-nil value, it should use +needsValue.
 + (instancetype)needsMoreDetailsForCurrencyAmount:(INCurrencyAmount *)currencyAmountToComplete NS_SWIFT_NAME(needsMoreDetails(for:));
 
-// This resolution result is the same as +unsupportedWithReason:, but allows the app extension to provide alternate / suggested currency amounts.
-+ (instancetype)unsupportedWithReason:(INIntentResolutionResultUnsupportedReason)reason
-           alternativeCurrencyAmounts:(NSArray<INCurrencyAmount *> *)alternativeCurrencyAmounts NS_SWIFT_NAME(unsupported(with:alternativeCurrencyAmounts:));
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h	2016-06-26 09:15:29.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDomainHandling.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDomainHandling.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDomainHandling.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDomainHandling.h	2016-06-26 09:15:29.000000000 +0200
@@ -7,27 +7,39 @@
 
 #import <Intents/INIntents.h>
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @protocol INCallsDomainHandling <INStartAudioCallIntentHandling, INStartVideoCallIntentHandling, INSearchCallHistoryIntentHandling>
 @end
 
-@protocol INCarPlayDomainHandling <INSetAudioSourceInCarIntentHandling, INSetClimateSettingsInCarIntentHandling, INSetDefrosterSettingsInCarIntentHandling, INSetSeatTemperatureInCarIntentHandling>
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
+@protocol INCarPlayDomainHandling <INSetAudioSourceInCarIntentHandling, INSetClimateSettingsInCarIntentHandling, INSetDefrosterSettingsInCarIntentHandling, INSetSeatSettingsInCarIntentHandling, INSetProfileInCarIntentHandling, INSaveProfileInCarIntentHandling>
 @end
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INWorkoutsDomainHandling <INStartWorkoutIntentHandling, INPauseWorkoutIntentHandling, INEndWorkoutIntentHandling, INCancelWorkoutIntentHandling, INResumeWorkoutIntentHandling>
 @end
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INRadioDomainHandling <INSetRadioStationIntentHandling>
 @end
 
-@protocol INMessagesDomainHandling <INSendMessageIntentHandling, INSearchForMessagesIntentHandling>
+API_AVAILABLE(macosx(10.12), ios(10.0))
+@protocol INMessagesDomainHandling <INSendMessageIntentHandling, INSearchForMessagesIntentHandling, INSetMessageAttributeIntentHandling>
 @end
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INPaymentsDomainHandling <INSendPaymentIntentHandling, INRequestPaymentIntentHandling>
 @end
 
+API_AVAILABLE(ios(10.0))
 @protocol INPhotosDomainHandling <INSearchForPhotosIntentHandling, INStartPhotoPlaybackIntentHandling>
 @end
 
-NS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_AVAILABLE(3_0)
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INRidesharingDomainHandling <INListRideOptionsIntentHandling, INRequestRideIntentHandling, INGetRideStatusIntentHandling>
 @end
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INEndWorkoutIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INEndWorkoutIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INEndWorkoutIntent.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INEndWorkoutIntent.h	2016-06-26 09:15:29.000000000 +0200
@@ -8,15 +8,18 @@
 #import <Intents/INIntent.h>
 #import <Intents/INIntentResolutionResult.h>
 
-@class INStringResolutionResult;
+@class INSpeakableString;
+@class INSpeakableStringResolutionResult;
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INEndWorkoutIntent : INIntent
 
-- (instancetype)initWithWorkoutName:(nullable NSString *)workoutName NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithWorkoutName:(nullable INSpeakableString *)workoutName NS_DESIGNATED_INITIALIZER;
 
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *workoutName;
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INSpeakableString *workoutName;
 
 @end
 
@@ -28,6 +31,8 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INEndWorkoutIntentHandling <NSObject>
 
 @required
@@ -77,7 +82,7 @@
  */
 
 - (void)resolveWorkoutNameForEndWorkout:(INEndWorkoutIntent *)intent
-                         withCompletion:(void (^)(INStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveWorkoutName(forEndWorkout:with:));
+                         withCompletion:(void (^)(INSpeakableStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveWorkoutName(forEndWorkout:with:));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INEndWorkoutIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INEndWorkoutIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INEndWorkoutIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INEndWorkoutIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -9,8 +9,8 @@
 
 typedef NS_ENUM(NSInteger, INEndWorkoutIntentResponseCode) {
     INEndWorkoutIntentResponseCodeUnspecified = 0,
-    INEndWorkoutIntentResponseCodeInProgress,
-    INEndWorkoutIntentResponseCodeSuccess,
+    INEndWorkoutIntentResponseCodeReady,
+    INEndWorkoutIntentResponseCodeContinueInApp,
     INEndWorkoutIntentResponseCodeFailure,
     INEndWorkoutIntentResponseCodeFailureRequiringAppLaunch,
     INEndWorkoutIntentResponseCodeFailureNoMatchingWorkout,
@@ -18,6 +18,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INEndWorkoutIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingDefaultsIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingDefaultsIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingDefaultsIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingDefaultsIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -11,9 +11,10 @@
 #import <Intents/INIntentResponse.h>
 #import <Intents/INImage.h>
 
-typedef NS_ENUM(NSInteger, INGetAvailableRestaurantReservationBookingDefaultsIntentCode) {
-    INGetAvailableRestaurantReservationBookingDefaultsIntentCodeSuccess,
-    INGetAvailableRestaurantReservationBookingDefaultsIntentCodeFailure
+typedef NS_ENUM(NSInteger, INGetAvailableRestaurantReservationBookingDefaultsIntentResponseCode) {
+    INGetAvailableRestaurantReservationBookingDefaultsIntentResponseCodeSuccess,
+    INGetAvailableRestaurantReservationBookingDefaultsIntentResponseCodeFailure,
+    INGetAvailableRestaurantReservationBookingDefaultsIntentResponseCodeUnspecified
 };
 
 NS_ASSUME_NONNULL_BEGIN
@@ -21,14 +22,15 @@
 NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
 @interface INGetAvailableRestaurantReservationBookingDefaultsIntentResponse : INIntentResponse
 
-@property (NS_NONATOMIC_IOSONLY) NSUInteger defaultPartySize; // default party size for an available bookings request
-@property (copy, NS_NONATOMIC_IOSONLY) NSDate *defaultBookingDate; // default booking time for an available bookings request
-@property (NS_NONATOMIC_IOSONLY) NSNumber *maximumPartySize;
+@property (readonly, NS_NONATOMIC_IOSONLY) NSUInteger defaultPartySize; // default party size for an available bookings request
+@property (readonly, copy, NS_NONATOMIC_IOSONLY) NSDate *defaultBookingDate; // default booking time for an available bookings request
+@property (nullable, NS_NONATOMIC_IOSONLY) NSNumber *maximumPartySize;
+@property (nullable, NS_NONATOMIC_IOSONLY) NSNumber *minimumPartySize;
 @property (copy, NS_NONATOMIC_IOSONLY) INImage *providerImage;
 
-- (instancetype)initWithCode:(INGetAvailableRestaurantReservationBookingDefaultsIntentCode)code userActivity:(nullable NSUserActivity *)userActivity NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithDefaultPartySize:(NSUInteger)defaultPartySize defaultBookingDate:(NSDate *)defaultBookingDate code:(INGetAvailableRestaurantReservationBookingDefaultsIntentResponseCode)code userActivity:(nullable NSUserActivity *)userActivity NS_DESIGNATED_INITIALIZER;
 
-@property (readonly, NS_NONATOMIC_IOSONLY) INGetAvailableRestaurantReservationBookingDefaultsIntentCode code;
+@property (readonly, NS_NONATOMIC_IOSONLY) INGetAvailableRestaurantReservationBookingDefaultsIntentResponseCode code;
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingsIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingsIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingsIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingsIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -10,11 +10,13 @@
 
 #import <Intents/INIntentResponse.h>
 #import <Intents/INRestaurantReservationBooking.h>
+#import <Intents/INTermsAndConditions.h>
 
 typedef NS_ENUM(NSInteger, INGetAvailableRestaurantReservationBookingsIntentCode) {
     INGetAvailableRestaurantReservationBookingsIntentCodeSuccess,
     INGetAvailableRestaurantReservationBookingsIntentCodeFailure,
-    INGetAvailableRestaurantReservationBookingsIntentCodeFailureRequestUnsatisfiable
+    INGetAvailableRestaurantReservationBookingsIntentCodeFailureRequestUnsatisfiable,
+    INGetAvailableRestaurantReservationBookingsIntentCodeFailureRequestUnspecified
 };
 
 NS_ASSUME_NONNULL_BEGIN
@@ -22,12 +24,14 @@
 NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
 @interface INGetAvailableRestaurantReservationBookingsIntentResponse : INIntentResponse
 
-- (instancetype)initWithCode:(INGetAvailableRestaurantReservationBookingsIntentCode)code userActivity:(nullable NSUserActivity *)userActivity NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithAvailableBookings:(NSArray<INRestaurantReservationBooking *> *)availableBookings code:(INGetAvailableRestaurantReservationBookingsIntentCode)code userActivity:(nullable NSUserActivity *)userActivity NS_DESIGNATED_INITIALIZER;
 
 @property (readonly, NS_NONATOMIC_IOSONLY) INGetAvailableRestaurantReservationBookingsIntentCode code;
 
-@property (copy, nullable, NS_NONATOMIC_IOSONLY) NSString *localizedBookingAdvisementText; // an optional string to be displayed in UI that allows the vendor to detail things like specials or incentives
-@property (copy, NS_NONATOMIC_IOSONLY) NSArray<INRestaurantReservationBooking *> *availableBookings;
+@property (copy, nullable, NS_NONATOMIC_IOSONLY) NSString *localizedRestaurantDescriptionText; // An optional string to be displayed in UI that allows the vendor to specify details or history about the restaurant.
+@property (copy, nullable, NS_NONATOMIC_IOSONLY) NSString *localizedBookingAdvisementText; // An optional string to be displayed in UI that allows the vendor to detail things like specials or incentives.
+@property (copy, nullable, NS_NONATOMIC_IOSONLY) INTermsAndConditions *termsAndConditions; // An optional object allowing the vendor to display terms of use for its service
+@property (readonly, NS_NONATOMIC_IOSONLY) NSArray<INRestaurantReservationBooking *> *availableBookings;
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRestaurantGuestIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRestaurantGuestIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRestaurantGuestIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRestaurantGuestIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -10,17 +10,24 @@
 
 #import <Intents/Intents.h>
 #import <Intents/INRestaurantGuest.h>
+#import <Intents/INRestaurantGuestDisplayPreferences.h>
+
+typedef NS_ENUM(NSInteger, INGetRestaurantGuestIntentResponseCode) {
+    INGetRestaurantGuestIntentResponseCodeSuccess,
+    INGetRestaurantGuestIntentResponseCodeFailure,
+};
 
 NS_ASSUME_NONNULL_BEGIN
 
 NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
 @interface INGetRestaurantGuestIntentResponse : INIntentResponse
 
-- (instancetype)initWithCode:(NSInteger)code userActivity:(nullable NSUserActivity *)userActivity NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCode:(INGetRestaurantGuestIntentResponseCode)code userActivity:(nullable NSUserActivity *)userActivity NS_DESIGNATED_INITIALIZER;
 
 @property (copy, nullable, NS_NONATOMIC_IOSONLY) INRestaurantGuest *guest;
+@property (copy, nullable, NS_NONATOMIC_IOSONLY) INRestaurantGuestDisplayPreferences *guestDisplayPreferences;
 
-@property (readonly, NS_NONATOMIC_IOSONLY) NSInteger code;
+@property (readonly, NS_NONATOMIC_IOSONLY) INGetRestaurantGuestIntentResponseCode code;
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRideStatusIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRideStatusIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRideStatusIntent.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRideStatusIntent.h	2016-06-26 09:15:29.000000000 +0200
@@ -10,6 +10,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INGetRideStatusIntent : INIntent
 
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
@@ -26,6 +28,8 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INGetRideStatusIntentHandling <NSObject>
 
 @required
@@ -81,6 +85,8 @@
 
 @end
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INGetRideStatusIntentResponseObserver <NSObject>
 
 - (void)getRideStatusResponseDidUpdate:(INGetRideStatusIntentResponse *)response NS_SWIFT_NAME(didUpdate(getRideStatus:));
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRideStatusIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRideStatusIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRideStatusIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRideStatusIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -11,6 +11,7 @@
 
 typedef NS_ENUM(NSInteger, INGetRideStatusIntentResponseCode) {
     INGetRideStatusIntentResponseCodeUnspecified = 0,
+    INGetRideStatusIntentResponseCodeReady,
     INGetRideStatusIntentResponseCodeInProgress,
     INGetRideStatusIntentResponseCodeSuccess,
     INGetRideStatusIntentResponseCodeFailure,
@@ -21,8 +22,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 10_0)
-__TVOS_PROHIBITED __WATCHOS_AVAILABLE(3_0)
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INGetRideStatusIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetUserCurrentRestaurantReservationBookingsIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetUserCurrentRestaurantReservationBookingsIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetUserCurrentRestaurantReservationBookingsIntent.h	2016-05-25 06:33:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetUserCurrentRestaurantReservationBookingsIntent.h	2016-06-26 09:15:29.000000000 +0200
@@ -20,6 +20,9 @@
 @property (copy, nullable, NS_NONATOMIC_IOSONLY) INRestaurant *restaurant; // optional filter to just reservations at restaurant
 @property (copy, nullable, NS_NONATOMIC_IOSONLY) NSString *reservationIdentifier; // optional filter to reservation with exact ID
 
+@property (copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *maximumNumberOfResults; // if the caller has a preferred maximum number of results, one can optionally be specified. a nil here leaves it up to the extension
+@property (copy, nullable, NS_NONATOMIC_IOSONLY) NSDate *earliestBookingDateForResults; // specifies the earliest booking date desired for results, including dates in the past
+
 @end
 
 @class INGetUserCurrentRestaurantReservationBookingsIntentResponse;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetUserCurrentRestaurantReservationBookingsIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetUserCurrentRestaurantReservationBookingsIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetUserCurrentRestaurantReservationBookingsIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetUserCurrentRestaurantReservationBookingsIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -11,10 +11,11 @@
 #import <Intents/INIntentResponse.h>
 #import <Intents/INRestaurantReservationUserBooking.h>
 
-typedef NS_ENUM(NSInteger, INGetUserCurrentRestaurantReservationBookingsIntentCode) {
-    INGetUserCurrentRestaurantReservationBookingsIntentCodeSuccess,
-    INGetUserCurrentRestaurantReservationBookingsIntentCodeFailure,
-    INGetUserCurrentRestaurantReservationBookingsIntentCodeFailureRequestUnsatisfiable
+typedef NS_ENUM(NSInteger, INGetUserCurrentRestaurantReservationBookingsIntentResponseCode) {
+    INGetUserCurrentRestaurantReservationBookingsIntentResponseCodeSuccess,
+    INGetUserCurrentRestaurantReservationBookingsIntentResponseCodeFailure,
+    INGetUserCurrentRestaurantReservationBookingsIntentResponseCodeFailureRequestUnsatisfiable,
+    INGetUserCurrentRestaurantReservationBookingsIntentResponseCodeUnspecified
 };
 
 NS_ASSUME_NONNULL_BEGIN
@@ -22,9 +23,9 @@
 NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
 @interface INGetUserCurrentRestaurantReservationBookingsIntentResponse : INIntentResponse
 
-- (instancetype)initWithCode:(INGetUserCurrentRestaurantReservationBookingsIntentCode)code userActivity:(nullable NSUserActivity *)userActivity NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithUserCurrentBookings:(NSArray<INRestaurantReservationUserBooking *> *)userCurrentBookings code:(INGetUserCurrentRestaurantReservationBookingsIntentResponseCode)code userActivity:(nullable NSUserActivity *)userActivity NS_DESIGNATED_INITIALIZER;
 
-@property (readonly, NS_NONATOMIC_IOSONLY) INGetUserCurrentRestaurantReservationBookingsIntentCode code;
+@property (readonly, NS_NONATOMIC_IOSONLY) INGetUserCurrentRestaurantReservationBookingsIntentResponseCode code;
 
 @property (copy, NS_NONATOMIC_IOSONLY) NSArray<INRestaurantReservationUserBooking *> *userCurrentBookings;
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentErrors.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentErrors.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentErrors.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentErrors.h	2016-06-26 09:15:29.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResult.h	2016-06-26 09:15:29.000000000 +0200
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
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResultUnsupportedReason.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResultUnsupportedReason.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResultUnsupportedReason.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResolutionResultUnsupportedReason.h	1970-01-01 01:00:00.000000000 +0100
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResponses.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResponses.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResponses.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentResponses.h	2016-06-26 09:15:29.000000000 +0200
@@ -14,7 +14,9 @@
 #import <Intents/INSetAudioSourceInCarIntentResponse.h>
 #import <Intents/INSetClimateSettingsInCarIntentResponse.h>
 #import <Intents/INSetDefrosterSettingsInCarIntentResponse.h>
-#import <Intents/INSetSeatTemperatureInCarIntentResponse.h>
+#import <Intents/INSetSeatSettingsInCarIntentResponse.h>
+#import <Intents/INSetProfileInCarIntentResponse.h>
+#import <Intents/INSaveProfileInCarIntentResponse.h>
 
 // Messages Intent Responses
 #import <Intents/INSendMessageIntentResponse.h>
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentRestaurantReservation.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentRestaurantReservation.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentRestaurantReservation.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntentRestaurantReservation.h	2016-06-26 09:15:29.000000000 +0200
@@ -9,6 +9,8 @@
 // http://mapsconnect.apple.com/info/extensions
 
 #import "INRestaurantGuest.h"
+#import "INTermsAndConditions.h"
+#import "INRestaurantGuestDisplayPreferences.h"
 #import "INRestaurantReservationBooking.h"
 #import "INRestaurantReservationUserBooking.h"
 #import "INBookRestaurantReservationIntent.h"
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntents.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntents.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntents.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntents.h	2016-06-26 09:15:29.000000000 +0200
@@ -14,7 +14,9 @@
 #import <Intents/INSetAudioSourceInCarIntent.h>
 #import <Intents/INSetClimateSettingsInCarIntent.h>
 #import <Intents/INSetDefrosterSettingsInCarIntent.h>
-#import <Intents/INSetSeatTemperatureInCarIntent.h>
+#import <Intents/INSetSeatSettingsInCarIntent.h>
+#import <Intents/INSetProfileInCarIntent.h>
+#import <Intents/INSaveProfileInCarIntent.h>
 
 // Messages Intents
 #import <Intents/INSendMessageIntent.h>
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INInteraction.h	2016-06-26 09:15:29.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INListRideOptionsIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INListRideOptionsIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INListRideOptionsIntent.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INListRideOptionsIntent.h	2016-06-26 09:14:37.000000000 +0200
@@ -13,6 +13,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INListRideOptionsIntent : INIntent
 
 - (instancetype)initWithPickupLocation:(nullable CLPlacemark *)pickupLocation
@@ -32,6 +34,8 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INListRideOptionsIntentHandling <NSObject>
 
 @required
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INListRideOptionsIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INListRideOptionsIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INListRideOptionsIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INListRideOptionsIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -12,6 +12,7 @@
 
 typedef NS_ENUM(NSInteger, INListRideOptionsIntentResponseCode) {
     INListRideOptionsIntentResponseCodeUnspecified = 0,
+    INListRideOptionsIntentResponseCodeReady,
     INListRideOptionsIntentResponseCodeInProgress,
     INListRideOptionsIntentResponseCodeSuccess,
     INListRideOptionsIntentResponseCodeFailure,
@@ -19,12 +20,13 @@
     INListRideOptionsIntentResponseCodeFailureRequiringAppLaunchMustVerifyCredentials,
     INListRideOptionsIntentResponseCodeFailureRequiringAppLaunchNoServiceInArea,
     INListRideOptionsIntentResponseCodeFailureRequiringAppLaunchServiceTemporarilyUnavailable,
+    INListRideOptionsIntentResponseCodeFailureRequiringAppLaunchPreviousRideNeedsCompletion,
 };
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 10_0)
-__TVOS_PROHIBITED __WATCHOS_AVAILABLE(3_0)
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INListRideOptionsIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageAttribute.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageAttribute.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageAttribute.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageAttribute.h	2016-06-26 09:15:29.000000000 +0200
@@ -5,13 +5,19 @@
 //  Copyright © 2016 Apple. All rights reserved.
 //
 
+#ifndef INMessageAttribute_h
+#define INMessageAttribute_h
+
 #import <Foundation/Foundation.h>
 
 #import <Intents/IntentsDefines.h>
 
-typedef NSString *INMessageAttribute NS_STRING_ENUM;
+typedef NS_ENUM(NSInteger, INMessageAttribute) {
+    INMessageAttributeUnknown = 0,
+    INMessageAttributeRead,
+    INMessageAttributeUnread,
+    INMessageAttributeFlagged,
+    INMessageAttributeUnflagged,
+};
 
-INTENTS_EXTERN INMessageAttribute const INMessageAttributeRead NS_SWIFT_NAME(INMessageAttribute.read);
-INTENTS_EXTERN INMessageAttribute const INMessageAttributeUnread NS_SWIFT_NAME(INMessageAttribute.unread);
-INTENTS_EXTERN INMessageAttribute const INMessageAttributeFlagged NS_SWIFT_NAME(INMessageAttribute.flagged);
-INTENTS_EXTERN INMessageAttribute const INMessageAttributeUnflagged NS_SWIFT_NAME(INMessageAttribute.unflagged);
+#endif // INMessageAttribute_h
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageAttributeResolutionResult.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageAttributeResolutionResult.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageAttributeResolutionResult.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageAttributeResolutionResult.h	2016-06-26 09:15:29.000000000 +0200
@@ -13,11 +13,10 @@
 
 @interface INMessageAttributeResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value.
-// If the app extension wants to continue with a 'nil' value, it must use +resolutionResultNotRequired
+// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
 + (instancetype)successWithResolvedValue:(INMessageAttribute)resolvedValue NS_SWIFT_NAME(success(with:));
 
-// This resolution result is to ask Siri to confirm if this is the value with which the user wants to continue
+// This resolution result is to ask Siri to confirm if this is the value with which the user wants to continue.
 + (instancetype)confirmationRequiredWithValueToConfirm:(INMessageAttribute)valueToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
 
 @end
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageService.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageService.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageService.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageService.h	1970-01-01 01:00:00.000000000 +0100
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPauseWorkoutIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPauseWorkoutIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPauseWorkoutIntent.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPauseWorkoutIntent.h	2016-06-26 09:15:29.000000000 +0200
@@ -8,15 +8,18 @@
 #import <Intents/INIntent.h>
 #import <Intents/INIntentResolutionResult.h>
 
-@class INStringResolutionResult;
+@class INSpeakableString;
+@class INSpeakableStringResolutionResult;
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INPauseWorkoutIntent : INIntent
 
-- (instancetype)initWithWorkoutName:(nullable NSString *)workoutName NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithWorkoutName:(nullable INSpeakableString *)workoutName NS_DESIGNATED_INITIALIZER;
 
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *workoutName;
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INSpeakableString *workoutName;
 
 @end
 
@@ -28,6 +31,8 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INPauseWorkoutIntentHandling <NSObject>
 
 @required
@@ -77,7 +82,7 @@
  */
 
 - (void)resolveWorkoutNameForPauseWorkout:(INPauseWorkoutIntent *)intent
-                           withCompletion:(void (^)(INStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveWorkoutName(forPauseWorkout:with:));
+                           withCompletion:(void (^)(INSpeakableStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveWorkoutName(forPauseWorkout:with:));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPauseWorkoutIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPauseWorkoutIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPauseWorkoutIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPauseWorkoutIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -9,8 +9,8 @@
 
 typedef NS_ENUM(NSInteger, INPauseWorkoutIntentResponseCode) {
     INPauseWorkoutIntentResponseCodeUnspecified = 0,
-    INPauseWorkoutIntentResponseCodeInProgress,
-    INPauseWorkoutIntentResponseCodeSuccess,
+    INPauseWorkoutIntentResponseCodeReady,
+    INPauseWorkoutIntentResponseCodeContinueInApp,
     INPauseWorkoutIntentResponseCodeFailure,
     INPauseWorkoutIntentResponseCodeFailureRequiringAppLaunch,
     INPauseWorkoutIntentResponseCodeFailureNoMatchingWorkout,
@@ -18,6 +18,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INPauseWorkoutIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentMethodResolutionResult.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentMethodResolutionResult.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentMethodResolutionResult.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentMethodResolutionResult.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,35 +0,0 @@
-//
-//  INPaymentMethodResolutionResult.h
-//  Intents
-//
-//  Copyright © 2016 Apple. All rights reserved.
-//
-
-#import <Intents/INIntentResolutionResult.h>
-#import <Intents/INIntentResolutionResultUnsupportedReason.h>
-
-@class INPaymentMethod;
-
-NS_ASSUME_NONNULL_BEGIN
-
-@interface INPaymentMethodResolutionResult : INIntentResolutionResult
-
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given payment method. The resolvedPaymentMethod need not be identical to the input payment method. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
-+ (instancetype)successWithResolvedPaymentMethod:(INPaymentMethod *)resolvedPaymentMethod NS_SWIFT_NAME(success(with:));
-
-// This resolution result is to ask Siri to disambiguate between the provided payment methods.
-+ (instancetype)disambiguationWithPaymentMethodsToDisambiguate:(NSArray<INPaymentMethod *> *)paymentMethodsToDisambiguate NS_SWIFT_NAME(disambiguation(with:));
-
-// This resolution result is to ask Siri to confirm if this is the payment method with which the user wants to continue.
-+ (instancetype)confirmationRequiredWithPaymentMethodToConfirm:(nullable INPaymentMethod *)paymentMethodToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
-
-// This resolution result is to inform Siri that in order to continue, the app extension needs the payment method to be filled in greater detail. If this parameter is nil and the app extension wants to request a non-nil value, it should use +needsValue.
-+ (instancetype)needsMoreDetailsForPaymentMethod:(INPaymentMethod *)paymentMethodToComplete NS_SWIFT_NAME(needsMoreDetails(for:));
-
-// This resolution result is the same as +unsupportedWithReason:, but allows the app extension to provide alternate / suggested payment methods.
-+ (instancetype)unsupportedWithReason:(INIntentResolutionResultUnsupportedReason)reason
-            alternativePaymentMethods:(NSArray<INPaymentMethod *> *)alternativePaymentMethods NS_SWIFT_NAME(unsupported(with:alternativePaymentMethods:));
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentStatus.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentStatus.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentStatus.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPaymentStatus.h	2016-06-26 09:15:29.000000000 +0200
@@ -16,7 +16,7 @@
     INPaymentStatusUnknown = 0,
     INPaymentStatusPending,
     INPaymentStatusCompleted,
-    INPaymentStatusCancelled,
+    INPaymentStatusCanceled,
     INPaymentStatusFailed,
 };
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson+SiriAdditions.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson+SiriAdditions.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson+SiriAdditions.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson+SiriAdditions.h	2016-06-26 09:15:29.000000000 +0200
@@ -0,0 +1,18 @@
+//
+//  INPerson+SiriAdditions.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Intents/INPerson.h>
+
+#import <Intents/INSpeakable.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@interface INPerson (SiriAdditions) <INSpeakable>
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h	2016-06-28 04:49:12.000000000 +0200
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
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h	2016-06-26 09:15:29.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h	2016-06-26 09:15:29.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h	2016-06-26 09:15:29.000000000 +0200
@@ -6,7 +6,6 @@
 //
 
 #import <Intents/INIntentResolutionResult.h>
-#import <Intents/INIntentResolutionResultUnsupportedReason.h>
 
 @class CLPlacemark;
 
@@ -26,10 +25,6 @@
 // This resolution result is to inform Siri that in order to continue, the app extension needs the placemark to be filled in greater detail. If this parameter is nil and the app extension wants to request a non-nil value, it should use +needsValue.
 + (instancetype)needsMoreDetailsForPlacemark:(CLPlacemark *)placemarkToComplete NS_SWIFT_NAME(needsMoreDetails(for:));
 
-// This resolution result is the same as +unsupportedWithReason:, but allows the app extension to provide alternate / suggested placemarks.
-+ (instancetype)unsupportedWithReason:(INIntentResolutionResultUnsupportedReason)reason
-           alternativePlacemarks:(NSArray<CLPlacemark *> *)alternativePlacemarks NS_SWIFT_NAME(unsupported(with:alternativePlacemarks:));
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestPaymentIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestPaymentIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestPaymentIntent.h	2016-05-25 06:33:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestPaymentIntent.h	2016-06-26 09:14:37.000000000 +0200
@@ -13,17 +13,16 @@
 @class INCurrencyAmount;
 @class INCurrencyAmountResolutionResult;
 @class INStringResolutionResult;
-@class INPaymentMethod;
-@class INPaymentMethodResolutionResult;
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INRequestPaymentIntent : INIntent
 
 - (instancetype)initWithPayer:(nullable INPerson *)payer
                currencyAmount:(nullable INCurrencyAmount *)currencyAmount
-                         note:(nullable NSString *)note
-                paymentMethod:(nullable INPaymentMethod *)paymentMethod NS_DESIGNATED_INITIALIZER;
+                         note:(nullable NSString *)note NS_DESIGNATED_INITIALIZER;
 
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INPerson *payer;
 
@@ -31,8 +30,6 @@
 
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *note;
 
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INPaymentMethod *paymentMethod;
-
 @end
 
 @class INRequestPaymentIntentResponse;
@@ -43,6 +40,8 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INRequestPaymentIntentHandling <NSObject>
 
 @required
@@ -100,9 +99,6 @@
 - (void)resolveNoteForRequestPayment:(INRequestPaymentIntent *)intent
                       withCompletion:(void (^)(INStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveNote(forRequestPayment:with:));
 
-- (void)resolvePaymentMethodForRequestPayment:(INRequestPaymentIntent *)intent
-                               withCompletion:(void (^)(INPaymentMethodResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolvePaymentMethod(forRequestPayment:with:));
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestPaymentIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestPaymentIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestPaymentIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestPaymentIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -11,6 +11,7 @@
 
 typedef NS_ENUM(NSInteger, INRequestPaymentIntentResponseCode) {
     INRequestPaymentIntentResponseCodeUnspecified = 0,
+    INRequestPaymentIntentResponseCodeReady,
     INRequestPaymentIntentResponseCodeInProgress,
     INRequestPaymentIntentResponseCodeSuccess,
     INRequestPaymentIntentResponseCodeFailure,
@@ -19,6 +20,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INRequestPaymentIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestRideIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestRideIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestRideIntent.h	2016-05-25 06:33:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestRideIntent.h	2016-06-26 09:14:37.000000000 +0200
@@ -10,19 +10,22 @@
 
 @class CLPlacemark;
 @class INPlacemarkResolutionResult;
-@class INStringResolutionResult;
+@class INSpeakableString;
+@class INSpeakableStringResolutionResult;
 @class INIntegerResolutionResult;
 @class INBooleanResolutionResult;
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INRequestRideIntent : INIntent
 
 - (instancetype)initWithPickupLocation:(nullable CLPlacemark *)pickupLocation
                        dropOffLocation:(nullable CLPlacemark *)dropOffLocation
-                        rideOptionName:(nullable NSString *)rideOptionName
+                        rideOptionName:(nullable INSpeakableString *)rideOptionName
                              partySize:(nullable NSNumber *)partySize
-                     paymentMethodName:(nullable NSString *)paymentMethodName
+                     paymentMethodName:(nullable INSpeakableString *)paymentMethodName
                 usesApplePayForPayment:(nullable NSNumber *)usesApplePayForPayment NS_DESIGNATED_INITIALIZER NS_REFINED_FOR_SWIFT;
 
 // Specifies the location to to begin the ride.
@@ -31,12 +34,12 @@
 // Specifies where the ride should end.
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) CLPlacemark *dropOffLocation;
 
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *rideOptionName;
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INSpeakableString *rideOptionName;
 
 // Defines the number of people in the party requesting the ride.
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *partySize NS_REFINED_FOR_SWIFT;
 
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *paymentMethodName;
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INSpeakableString *paymentMethodName;
 
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *usesApplePayForPayment NS_REFINED_FOR_SWIFT;
 
@@ -50,6 +53,8 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INRequestRideIntentHandling <NSObject>
 
 @required
@@ -105,13 +110,13 @@
                               withCompletion:(void (^)(INPlacemarkResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveDropOffLocation(forRequestRide:with:));
 
 - (void)resolveRideOptionNameForRequestRide:(INRequestRideIntent *)intent
-                             withCompletion:(void (^)(INStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveRideOptionName(forRequestRide:with:));
+                             withCompletion:(void (^)(INSpeakableStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveRideOptionName(forRequestRide:with:));
 
 - (void)resolvePartySizeForRequestRide:(INRequestRideIntent *)intent
                         withCompletion:(void (^)(INIntegerResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolvePartySize(forRequestRide:with:));
 
 - (void)resolvePaymentMethodNameForRequestRide:(INRequestRideIntent *)intent
-                                withCompletion:(void (^)(INStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolvePaymentMethodName(forRequestRide:with:));
+                                withCompletion:(void (^)(INSpeakableStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolvePaymentMethodName(forRequestRide:with:));
 
 - (void)resolveUsesApplePayForPaymentForRequestRide:(INRequestRideIntent *)intent
                                      withCompletion:(void (^)(INBooleanResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveUsesApplePayForPayment(forRequestRide:with:));
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestRideIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestRideIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestRideIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestRideIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -11,6 +11,7 @@
 
 typedef NS_ENUM(NSInteger, INRequestRideIntentResponseCode) {
     INRequestRideIntentResponseCodeUnspecified = 0,
+    INRequestRideIntentResponseCodeReady,
     INRequestRideIntentResponseCodeInProgress,
     INRequestRideIntentResponseCodeSuccess,
     INRequestRideIntentResponseCodeFailure,
@@ -18,12 +19,13 @@
     INRequestRideIntentResponseCodeFailureRequiringAppLaunchMustVerifyCredentials,
     INRequestRideIntentResponseCodeFailureRequiringAppLaunchNoServiceInArea,
     INRequestRideIntentResponseCodeFailureRequiringAppLaunchServiceTemporarilyUnavailable,
+    INRequestRideIntentResponseCodeFailureRequiringAppLaunchPreviousRideNeedsCompletion,
 };
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 10_0)
-__TVOS_PROHIBITED __WATCHOS_AVAILABLE(3_0)
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INRequestRideIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurant.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurant.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurant.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurant.h	2016-06-26 09:15:29.000000000 +0200
@@ -16,9 +16,10 @@
 NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
 @interface INRestaurant : NSObject <NSSecureCoding, NSCopying>
 
+- (instancetype)initWithLocation:(CLLocation *)location name:(NSString *)name vendorIdentifier:(NSString *)vendorIdentifier restaurantIdentifier:(NSString *)restaurantIdentifier NS_DESIGNATED_INITIALIZER;
+
 @property (copy, NS_NONATOMIC_IOSONLY) CLLocation *location;
 @property (copy, NS_NONATOMIC_IOSONLY) NSString *name;
-
 @property (copy, NS_NONATOMIC_IOSONLY) NSString *vendorIdentifier; // provider's vendor identifier
 @property (copy, NS_NONATOMIC_IOSONLY) NSString *restaurantIdentifier; // vendor specific restaurant identifier. should match what Maps is ingesting through its data pipeline for the vendor.
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuest.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuest.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuest.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuest.h	2016-06-26 09:15:29.000000000 +0200
@@ -15,6 +15,8 @@
 NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
 @interface INRestaurantGuest : INPerson
 
+- (instancetype)initWithNameComponents:(nullable NSPersonNameComponents *)nameComponents phoneNumber:(nullable NSString *)phoneNumber emailAddress:(nullable NSString *)emailAddress NS_DESIGNATED_INITIALIZER;
+
 @property (copy, nullable, NS_NONATOMIC_IOSONLY) NSString *phoneNumber;
 @property (copy, nullable, NS_NONATOMIC_IOSONLY) NSString *emailAddress;
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuestDisplayPreferences.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuestDisplayPreferences.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuestDisplayPreferences.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuestDisplayPreferences.h	2016-06-26 09:15:29.000000000 +0200
@@ -0,0 +1,25 @@
+//
+//  INRestaurantGuestDisplayPreferences.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+// This API requires you to work with Apple Maps before your application can use it. For information on how to get started, please go to MapsConnect.
+//
+// http://mapsconnect.apple.com/info/extensions
+
+NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+@interface INRestaurantGuestDisplayPreferences : NSObject <NSSecureCoding, NSCopying>
+
+@property (NS_NONATOMIC_IOSONLY) BOOL nameFieldFirstNameOptional; // indicates whether first name field is marked optional, defaults to NO
+@property (NS_NONATOMIC_IOSONLY) BOOL nameFieldLastNameOptional; // indicates whether last name field is marked optional, defaults to NO
+
+@property (NS_NONATOMIC_IOSONLY) BOOL nameFieldShouldBeDisplayed; // indicates whether name input field should be displayed, defaults to YES
+@property (NS_NONATOMIC_IOSONLY) BOOL emailAddressFieldShouldBeDisplayed; // indicates whether email address input field should be displayed, defaults to YES
+@property (NS_NONATOMIC_IOSONLY) BOOL phoneNumberFieldShouldBeDisplayed; // indicates whether phone number field should be displayed, defaults to YES
+
+@property (NS_NONATOMIC_IOSONLY) BOOL nameEditable; // indicates whether the name field should be user editable, defaults to YES
+@property (NS_NONATOMIC_IOSONLY) BOOL emailAddressEditable; // indicates whether the email address field should be user editable, defaults to YES
+@property (NS_NONATOMIC_IOSONLY) BOOL phoneNumberEditable; // indicates whether the phone number field should be user editable, defaults to YES
+
+@end
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantReservationBooking.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantReservationBooking.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantReservationBooking.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantReservationBooking.h	2016-06-26 09:15:29.000000000 +0200
@@ -18,17 +18,19 @@
 // represents a booking at a restaurant during a given time for a given party size
 @interface INRestaurantReservationBooking : NSObject <NSSecureCoding, NSCopying>
 
+- (instancetype)initWithRestaurant:(INRestaurant *)restaurant bookingDate:(NSDate *)bookingDate partySize:(NSUInteger)partySize bookingIdentifier:(NSString *)bookingIdentifier NS_DESIGNATED_INITIALIZER;
+
 @property (copy, NS_NONATOMIC_IOSONLY) INRestaurant *restaurant;
-@property (copy, nullable, NS_NONATOMIC_IOSONLY) NSString *bookingDescription; // nullable string describing the booking
+@property (copy, nullable, NS_NONATOMIC_IOSONLY) NSString *bookingDescription; // A nullable string describing the booking
 @property (copy, NS_NONATOMIC_IOSONLY) NSDate *bookingDate;
 @property (NS_NONATOMIC_IOSONLY) NSUInteger partySize;
-@property (copy, NS_NONATOMIC_IOSONLY) NSString *bookingIdentifier; // vendor specific identifier that refers to this booking
-@property (getter = isBookingAvailable, NS_NONATOMIC_IOSONLY) BOOL bookingAvailable; // allows extension to mark specific timeslots as having been filled
+@property (copy, NS_NONATOMIC_IOSONLY) NSString *bookingIdentifier; // A vendor specific identifier that refers to this booking.
+@property (getter = isBookingAvailable, NS_NONATOMIC_IOSONLY) BOOL bookingAvailable; // Boolean indicating whether timeslot is available for booking. Defaults to YES.
 @property (copy, nullable, NS_NONATOMIC_IOSONLY) NSArray <INRestaurantOffer *> *offers;
-@property (NS_NONATOMIC_IOSONLY) BOOL requiresManualRequest; // restaurant must be contacted by phone before confirmation is given
-@property (NS_NONATOMIC_IOSONLY) BOOL requiresEmailAddress; // email address required to book
-@property (NS_NONATOMIC_IOSONLY) BOOL requiresName; // name required to book
-@property (NS_NONATOMIC_IOSONLY) BOOL requiresPhoneNumber; // phone number required to book
+@property (NS_NONATOMIC_IOSONLY) BOOL requiresManualRequest; // YES means restaurant must be contacted by phone before confirmation is given. Defaults to NO.
+@property (NS_NONATOMIC_IOSONLY) BOOL requiresEmailAddress; // YES means an email address is required to book. Defaults to NO.
+@property (NS_NONATOMIC_IOSONLY) BOOL requiresName; // YES means a name is required to book. Defaults to NO.
+@property (NS_NONATOMIC_IOSONLY) BOOL requiresPhoneNumber; // YES means a phone number required to book. Defaults to NO.
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantReservationUserBooking.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantReservationUserBooking.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantReservationUserBooking.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantReservationUserBooking.h	2016-06-26 09:15:29.000000000 +0200
@@ -11,6 +11,7 @@
 #import <Intents/INIntent.h>
 #import <Intents/INRestaurantReservationBooking.h>
 #import <Intents/INRestaurantGuest.h>
+#import <Intents/INRestaurantOffer.h>
 
 typedef NS_ENUM (NSUInteger, INRestaurantReservationUserBookingStatus) {
     INRestaurantReservationUserBookingStatusPending,
@@ -22,9 +23,14 @@
 NS_ASSUME_NONNULL_BEGIN
 @interface INRestaurantReservationUserBooking : INRestaurantReservationBooking <NSCopying>
 
+- (instancetype)initWithRestaurant:(INRestaurant *)restaurant bookingDate:(NSDate *)bookingDate partySize:(NSUInteger)partySize bookingIdentifier:(NSString *)bookingIdentifier guest:(INRestaurantGuest *)guest status:(INRestaurantReservationUserBookingStatus)status dateStatusModified:(NSDate *)dateStatusModified;
+
 @property (copy, NS_NONATOMIC_IOSONLY) INRestaurantGuest *guest;
 @property (copy, nullable, NS_NONATOMIC_IOSONLY) NSString *advisementText; // a string representing restaurant specific information related to the reservation: things like late policies, parking instructions, or specials
+@property (copy, nullable, NS_NONATOMIC_IOSONLY) INRestaurantOffer *selectedOffer; // an offer, if any, attached to the booking
+@property (copy, nullable, NS_NONATOMIC_IOSONLY) NSString *guestProvidedSpecialRequestText; // any user-specified special request text submitted with the reservation
 @property (NS_NONATOMIC_IOSONLY) INRestaurantReservationUserBookingStatus status; // an enum indicating whether a booking was denied, pending, or confirmed
+@property (NS_NONATOMIC_IOSONLY) NSDate *dateStatusModified; // date indicating when the status was updated to its current value
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INResumeWorkoutIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INResumeWorkoutIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INResumeWorkoutIntent.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INResumeWorkoutIntent.h	2016-06-26 09:15:29.000000000 +0200
@@ -8,15 +8,18 @@
 #import <Intents/INIntent.h>
 #import <Intents/INIntentResolutionResult.h>
 
-@class INStringResolutionResult;
+@class INSpeakableString;
+@class INSpeakableStringResolutionResult;
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INResumeWorkoutIntent : INIntent
 
-- (instancetype)initWithWorkoutName:(nullable NSString *)workoutName NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithWorkoutName:(nullable INSpeakableString *)workoutName NS_DESIGNATED_INITIALIZER;
 
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *workoutName;
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INSpeakableString *workoutName;
 
 @end
 
@@ -28,6 +31,8 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INResumeWorkoutIntentHandling <NSObject>
 
 @required
@@ -77,7 +82,7 @@
  */
 
 - (void)resolveWorkoutNameForResumeWorkout:(INResumeWorkoutIntent *)intent
-                            withCompletion:(void (^)(INStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveWorkoutName(forResumeWorkout:with:));
+                            withCompletion:(void (^)(INSpeakableStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveWorkoutName(forResumeWorkout:with:));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INResumeWorkoutIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INResumeWorkoutIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INResumeWorkoutIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INResumeWorkoutIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -9,8 +9,8 @@
 
 typedef NS_ENUM(NSInteger, INResumeWorkoutIntentResponseCode) {
     INResumeWorkoutIntentResponseCodeUnspecified = 0,
-    INResumeWorkoutIntentResponseCodeInProgress,
-    INResumeWorkoutIntentResponseCodeSuccess,
+    INResumeWorkoutIntentResponseCodeReady,
+    INResumeWorkoutIntentResponseCodeContinueInApp,
     INResumeWorkoutIntentResponseCodeFailure,
     INResumeWorkoutIntentResponseCodeFailureRequiringAppLaunch,
     INResumeWorkoutIntentResponseCodeFailureNoMatchingWorkout,
@@ -18,6 +18,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INResumeWorkoutIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideCompletionStatus.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideCompletionStatus.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideCompletionStatus.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideCompletionStatus.h	2016-06-26 09:15:29.000000000 +0200
@@ -0,0 +1,58 @@
+//
+//  INRideCompletionStatus.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+@class INCurrencyAmount;
+
+NS_ASSUME_NONNULL_BEGIN
+
+NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+@interface INRideCompletionStatus: NSObject <NSCopying, NSSecureCoding>
+
+- (instancetype)init NS_UNAVAILABLE;
+
+// The ride completed.
++ (instancetype)completed;
+
+// The ride completed. The fare in the provided amount was successfully paid; this amount may be displayed to the user.
++ (instancetype)completedWithSettledPaymentAmount:(INCurrencyAmount *)settledPaymentAmount NS_SWIFT_NAME(completed(settled:));
+
+// The ride completed but there is a payment outstanding that the user needs to settle in the application.
+// The .completionUserActivity should be set, and will be continued in your application to perform payment tasks.
++ (instancetype)completedWithOutstandingPaymentAmount:(INCurrencyAmount *)outstandingPaymentAmount NS_SWIFT_NAME(completed(outstanding:));
+
+// The ride was canceled by the service (e.g. because the driver asked to cancel)
++ (instancetype)canceledByService;
+
+// The ride was canceled by the user (e.g. by doing so through your application)
++ (instancetype)canceledByUser;
+
+// The ride was canceled by the service because the passenger was not present for pickup and the vehicle maximum wait time elapsed.
++ (instancetype)canceledMissedPickup;
+
+// If this property is set, UI may be shown to the user to complete post-ride tasks (e.g. for feedback or settling outstanding payment). Acting on that UI will continue this activity in your application.
+@property (readwrite, strong, nullable, NS_NONATOMIC_IOSONLY) NSUserActivity *completionUserActivity;
+
+// YES if the ride was completed.
+@property (readonly, NS_NONATOMIC_IOSONLY, getter=isCompleted) BOOL completed;
+
+// YES if the ride was canceled.
+@property (readonly, NS_NONATOMIC_IOSONLY, getter=isCanceled) BOOL canceled;
+
+// YES if the user missed the pickup. This is only YES if .canceled is YES.
+@property (readonly, NS_NONATOMIC_IOSONLY, getter=isMissedPickup) BOOL missedPickup;
+
+// The payment amount, if any.
+@property (readonly, strong, nullable, NS_NONATOMIC_IOSONLY) INCurrencyAmount *paymentAmount;
+
+// Whether the payment is outstanding (YES) or settled (NO).
+@property (readonly, NS_NONATOMIC_IOSONLY, getter=isOutstanding) BOOL outstanding;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideDriver.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideDriver.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideDriver.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideDriver.h	2016-06-26 09:15:29.000000000 +0200
@@ -8,22 +8,30 @@
 #import <Intents/INPerson.h>
 
 @class INImage;
+@class INPersonHandle;
 
 NS_ASSUME_NONNULL_BEGIN
 
 @interface INRideDriver : INPerson <NSCopying, NSSecureCoding>
 
-- (instancetype)initWithHandle:(NSString *)handle
+- (instancetype)initWithPersonHandle:(INPersonHandle *)personHandle
+                nameComponents:(nullable NSPersonNameComponents *)nameComponents
                    displayName:(nullable NSString *)displayName
                          image:(nullable INImage *)image
                         rating:(nullable NSString *)rating
                    phoneNumber:(nullable NSString *)phoneNumber NS_DESIGNATED_INITIALIZER;
 
 - (instancetype)initWithHandle:(NSString *)handle
+                   displayName:(nullable NSString *)displayName
+                         image:(nullable INImage *)image
+                        rating:(nullable NSString *)rating
+                   phoneNumber:(nullable NSString *)phoneNumber NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use the designated initializer instead");
+
+- (instancetype)initWithHandle:(NSString *)handle
                 nameComponents:(NSPersonNameComponents *)nameComponents
                          image:(nullable INImage *)image
                         rating:(nullable NSString *)rating
-                   phoneNumber:(nullable NSString *)phoneNumber NS_DESIGNATED_INITIALIZER;
+                   phoneNumber:(nullable NSString *)phoneNumber NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use the designated initializer instead");
 
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *rating;
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideOption.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideOption.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideOption.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideOption.h	2016-06-26 09:15:29.000000000 +0200
@@ -29,6 +29,7 @@
 @property (readwrite, copy, NS_NONATOMIC_IOSONLY) NSDate *estimatedPickupDate; // used for providing an ETA to the user.
 
 @property (readwrite, copy, nullable, NS_NONATOMIC_IOSONLY) INPriceRange *priceRange; // The indicative range of prices for this option.
+@property (readwrite, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *usesMeteredFare; // If @YES, the fare will be metered by the driver, and price range information will be noted as unavailable.
 
 @property (readwrite, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *disclaimerMessage; // A message that includes warnings or disclaimers shown to the user before they confirm the request. For example: "This ride may make multiple stops", or "This ride may be shared with other passengers".
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRidePhase.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRidePhase.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRidePhase.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRidePhase.h	2016-06-26 09:15:29.000000000 +0200
@@ -18,7 +18,8 @@
     INRidePhaseConfirmed,
     INRidePhaseOngoing,
     INRidePhaseCompleted,
-    INRidePhaseCanceled,
+    INRidePhaseApproachingPickup,
+    INRidePhasePickup,
 };
 
 #endif // INRidePhase_h
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideStatus.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideStatus.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideStatus.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideStatus.h	2016-06-26 09:15:29.000000000 +0200
@@ -13,6 +13,7 @@
 @class INRideVehicle;
 @class INRideDriver;
 @class INRideOption;
+@class INRideCompletionStatus;
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -22,6 +23,10 @@
 @property (readwrite, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *rideIdentifier;
 
 @property (readwrite, assign, NS_NONATOMIC_IOSONLY) INRidePhase phase;
+
+// This property should be set if the phase is INRidePhaseCompleted.
+@property (readwrite, copy, nullable, NS_NONATOMIC_IOSONLY) INRideCompletionStatus *completionStatus;
+
 @property (readwrite, copy, nullable, NS_NONATOMIC_IOSONLY) INRideVehicle *vehicle;
 @property (readwrite, copy, nullable, NS_NONATOMIC_IOSONLY) INRideDriver *driver;
 
@@ -36,6 +41,10 @@
 
 @property (readwrite, strong, nullable, NS_NONATOMIC_IOSONLY) NSUserActivity *userActivityForCancelingInApplication; // If set, and the ride hasn't completed or been canceled yet, the system may open the containing application and request continuation of this activity to request that the ride be canceled. It is appropriate to show confirmation UI to the user when this happens.
 
+// These actions may be available for the user to choose during the ride.
+// When shown, the .title of each activity will presented to the user. Selecting an activity will open your application to continue it.
+@property (readwrite, copy, nullable, NS_NONATOMIC_IOSONLY) NSArray<NSUserActivity *> *additionalActionActivities;
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntent.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntent.h	2016-06-26 09:14:37.000000000 +0200
@@ -0,0 +1,95 @@
+//
+//  INSaveProfileInCarIntent.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Intents/INIntent.h>
+#import <Intents/INIntentResolutionResult.h>
+
+@class INIntegerResolutionResult;
+@class INStringResolutionResult;
+
+NS_ASSUME_NONNULL_BEGIN
+
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
+@interface INSaveProfileInCarIntent : INIntent
+
+- (instancetype)initWithProfileNumber:(nullable NSNumber *)profileNumber
+                         profileLabel:(nullable NSString *)profileLabel NS_DESIGNATED_INITIALIZER NS_REFINED_FOR_SWIFT;
+
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *profileNumber NS_REFINED_FOR_SWIFT;
+
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *profileLabel;
+
+@end
+
+@class INSaveProfileInCarIntentResponse;
+
+/*!
+ @brief Protocol to declare support for handling an INSaveProfileInCarIntent 
+ @abstract By implementing this protocol, a class can provide logic for resolving, confirming and handling the intent.
+ @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
+ */
+
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
+@protocol INSaveProfileInCarIntentHandling <NSObject>
+
+@required
+
+/*!
+ @brief handling method
+
+ @abstract Execute the task represented by the INSaveProfileInCarIntent that's passed in
+ @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+
+ @param  saveProfileInCarIntent The input intent
+ @param  completion The response handling block takes a INSaveProfileInCarIntentResponse containing the details of the result of having executed the intent
+
+ @see  INSaveProfileInCarIntentResponse
+ */
+
+- (void)handleSaveProfileInCar:(INSaveProfileInCarIntent *)intent
+                    completion:(void (^)(INSaveProfileInCarIntentResponse *response))completion NS_SWIFT_NAME(handle(saveProfileInCar:completion:));
+
+@optional
+
+/*!
+ @brief Confirmation method
+ @abstract Validate that this intent is ready for the next step (i.e. handling)
+ @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+
+ @param  saveProfileInCarIntent The input intent
+ @param  completion The response block contains an INSaveProfileInCarIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
+
+ @see INSaveProfileInCarIntentResponse
+
+ */
+
+- (void)confirmSaveProfileInCar:(INSaveProfileInCarIntent *)intent
+                     completion:(void (^)(INSaveProfileInCarIntentResponse *response))completion NS_SWIFT_NAME(confirm(saveProfileInCar:completion:));
+
+/*!
+ @brief Resolution methods
+ @abstract Determine if this intent is ready for the next step (confirmation)
+ @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+
+ @param  saveProfileInCarIntent The input intent
+ @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
+
+ @see INIntentResolutionResult
+
+ */
+
+- (void)resolveProfileNumberForSaveProfileInCar:(INSaveProfileInCarIntent *)intent
+                                 withCompletion:(void (^)(INIntegerResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveProfileNumber(forSaveProfileInCar:with:));
+
+- (void)resolveProfileLabelForSaveProfileInCar:(INSaveProfileInCarIntent *)intent
+                                withCompletion:(void (^)(INStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveProfileLabel(forSaveProfileInCar:with:));
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntentResponse.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -0,0 +1,36 @@
+//
+//  INSaveProfileInCarIntentResponse.h
+//  Intents
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Intents/INIntentResponse.h>
+
+typedef NS_ENUM(NSInteger, INSaveProfileInCarIntentResponseCode) {
+    INSaveProfileInCarIntentResponseCodeUnspecified = 0,
+    INSaveProfileInCarIntentResponseCodeReady,
+    INSaveProfileInCarIntentResponseCodeInProgress,
+    INSaveProfileInCarIntentResponseCodeSuccess,
+    INSaveProfileInCarIntentResponseCodeFailure,
+    INSaveProfileInCarIntentResponseCodeFailureRequiringAppLaunch,
+};
+
+NS_ASSUME_NONNULL_BEGIN
+
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
+@interface INSaveProfileInCarIntentResponse : INIntentResponse
+
+- (id)init NS_UNAVAILABLE;
+
+// The app extension has the option of capturing its private state as an NSUserActivity and returning it as the 'currentActivity'.
+// If the the app is launched, an NSUserActivity will be passed in with the private state.  The NSUserActivity may also be used to query the app's UI extension (if provided) for a view controller representing the current intent handling state.
+// In the case of app launch, the NSUserActivity will have its activityType set to the name of the intent. This intent object will also be available in the NSUserActivity.interaction property.
+- (instancetype)initWithCode:(INSaveProfileInCarIntentResponseCode)code userActivity:(nullable NSUserActivity *)userActivity NS_DESIGNATED_INITIALIZER;
+
+@property (readonly, NS_NONATOMIC_IOSONLY) INSaveProfileInCarIntentResponseCode code;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h	2016-06-26 09:15:29.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h	2016-06-26 09:15:29.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntent.h	2016-05-25 06:33:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntent.h	2016-06-26 09:15:29.000000000 +0200
@@ -22,6 +22,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
 @interface INSearchForPhotosIntent : INIntent
 
 - (instancetype)initWithDateCreated:(nullable INDateComponentsRange *)dateCreated
@@ -69,6 +70,7 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(ios(10.0))
 @protocol INSearchForPhotosIntentHandling <NSObject>
 
 @required
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -9,14 +9,15 @@
 
 typedef NS_ENUM(NSInteger, INSearchForPhotosIntentResponseCode) {
     INSearchForPhotosIntentResponseCodeUnspecified = 0,
-    INSearchForPhotosIntentResponseCodeInProgress,
-    INSearchForPhotosIntentResponseCodeSuccess,
+    INSearchForPhotosIntentResponseCodeReady,
+    INSearchForPhotosIntentResponseCodeContinueInApp,
     INSearchForPhotosIntentResponseCodeFailure,
     INSearchForPhotosIntentResponseCodeFailureRequiringAppLaunch,
 };
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
 @interface INSearchForPhotosIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h	2016-05-25 03:39:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h	2016-06-26 09:14:37.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendPaymentIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendPaymentIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendPaymentIntent.h	2016-05-25 06:33:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendPaymentIntent.h	2016-06-26 09:14:37.000000000 +0200
@@ -13,17 +13,16 @@
 @class INCurrencyAmount;
 @class INCurrencyAmountResolutionResult;
 @class INStringResolutionResult;
-@class INPaymentMethod;
-@class INPaymentMethodResolutionResult;
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INSendPaymentIntent : INIntent
 
 - (instancetype)initWithPayee:(nullable INPerson *)payee
                currencyAmount:(nullable INCurrencyAmount *)currencyAmount
-                         note:(nullable NSString *)note
-                paymentMethod:(nullable INPaymentMethod *)paymentMethod NS_DESIGNATED_INITIALIZER;
+                         note:(nullable NSString *)note NS_DESIGNATED_INITIALIZER;
 
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INPerson *payee;
 
@@ -31,8 +30,6 @@
 
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *note;
 
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INPaymentMethod *paymentMethod;
-
 @end
 
 @class INSendPaymentIntentResponse;
@@ -43,6 +40,8 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INSendPaymentIntentHandling <NSObject>
 
 @required
@@ -100,9 +99,6 @@
 - (void)resolveNoteForSendPayment:(INSendPaymentIntent *)intent
                    withCompletion:(void (^)(INStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveNote(forSendPayment:with:));
 
-- (void)resolvePaymentMethodForSendPayment:(INSendPaymentIntent *)intent
-                            withCompletion:(void (^)(INPaymentMethodResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolvePaymentMethod(forSendPayment:with:));
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendPaymentIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendPaymentIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendPaymentIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendPaymentIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -11,6 +11,7 @@
 
 typedef NS_ENUM(NSInteger, INSendPaymentIntentResponseCode) {
     INSendPaymentIntentResponseCodeUnspecified = 0,
+    INSendPaymentIntentResponseCodeReady,
     INSendPaymentIntentResponseCodeInProgress,
     INSendPaymentIntentResponseCodeSuccess,
     INSendPaymentIntentResponseCodeFailure,
@@ -19,6 +20,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INSendPaymentIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetAudioSourceInCarIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetAudioSourceInCarIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetAudioSourceInCarIntent.h	2016-05-25 06:33:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetAudioSourceInCarIntent.h	2016-06-26 09:14:37.000000000 +0200
@@ -16,6 +16,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INSetAudioSourceInCarIntent : INIntent
 
 - (instancetype)initWithAudioSource:(INCarAudioSource)audioSource
@@ -35,6 +37,8 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INSetAudioSourceInCarIntentHandling <NSObject>
 
 @required
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetAudioSourceInCarIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetAudioSourceInCarIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetAudioSourceInCarIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetAudioSourceInCarIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -9,6 +9,7 @@
 
 typedef NS_ENUM(NSInteger, INSetAudioSourceInCarIntentResponseCode) {
     INSetAudioSourceInCarIntentResponseCodeUnspecified = 0,
+    INSetAudioSourceInCarIntentResponseCodeReady,
     INSetAudioSourceInCarIntentResponseCodeInProgress,
     INSetAudioSourceInCarIntentResponseCodeSuccess,
     INSetAudioSourceInCarIntentResponseCodeFailure,
@@ -17,6 +18,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INSetAudioSourceInCarIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntent.h	2016-05-25 06:33:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntent.h	2016-06-26 09:15:29.000000000 +0200
@@ -9,18 +9,22 @@
 #import <Intents/INIntentResolutionResult.h>
 
 #import <Intents/INCarAirCirculationMode.h>
+#import <Intents/INCarSeat.h>
 #import <Intents/INRelativeSetting.h>
-#import <Intents/INTemperatureUnit.h>
 
 @class INBooleanResolutionResult;
 @class INCarAirCirculationModeResolutionResult;
 @class INIntegerResolutionResult;
 @class INDoubleResolutionResult;
 @class INRelativeSettingResolutionResult;
-@class INTemperatureUnitResolutionResult;
+@class INTemperature;
+@class INTemperatureResolutionResult;
+@class INCarSeatResolutionResult;
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INSetClimateSettingsInCarIntent : INIntent
 
 - (instancetype)initWithEnableFan:(nullable NSNumber *)enableFan
@@ -31,9 +35,9 @@
                     fanSpeedIndex:(nullable NSNumber *)fanSpeedIndex
                fanSpeedPercentage:(nullable NSNumber *)fanSpeedPercentage
           relativeFanSpeedSetting:(INRelativeSetting)relativeFanSpeedSetting
-                  temperatureUnit:(INTemperatureUnit)temperatureUnit
-                      temperature:(nullable NSNumber *)temperature
-       relativeTemperatureSetting:(INRelativeSetting)relativeTemperatureSetting NS_DESIGNATED_INITIALIZER NS_REFINED_FOR_SWIFT;
+                      temperature:(nullable INTemperature *)temperature
+       relativeTemperatureSetting:(INRelativeSetting)relativeTemperatureSetting
+                      climateZone:(INCarSeat)climateZone NS_DESIGNATED_INITIALIZER NS_REFINED_FOR_SWIFT;
 
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *enableFan NS_REFINED_FOR_SWIFT;
 
@@ -51,12 +55,12 @@
 
 @property (readonly, assign, NS_NONATOMIC_IOSONLY) INRelativeSetting relativeFanSpeedSetting;
 
-@property (readonly, assign, NS_NONATOMIC_IOSONLY) INTemperatureUnit temperatureUnit;
-
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *temperature NS_REFINED_FOR_SWIFT;
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INTemperature *temperature;
 
 @property (readonly, assign, NS_NONATOMIC_IOSONLY) INRelativeSetting relativeTemperatureSetting;
 
+@property (readonly, assign, NS_NONATOMIC_IOSONLY) INCarSeat climateZone;
+
 @end
 
 @class INSetClimateSettingsInCarIntentResponse;
@@ -67,6 +71,8 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INSetClimateSettingsInCarIntentHandling <NSObject>
 
 @required
@@ -139,15 +145,15 @@
 - (void)resolveRelativeFanSpeedSettingForSetClimateSettingsInCar:(INSetClimateSettingsInCarIntent *)intent
                                                   withCompletion:(void (^)(INRelativeSettingResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveRelativeFanSpeedSetting(forSetClimateSettingsInCar:with:));
 
-- (void)resolveTemperatureUnitForSetClimateSettingsInCar:(INSetClimateSettingsInCarIntent *)intent
-                                          withCompletion:(void (^)(INTemperatureUnitResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveTemperatureUnit(forSetClimateSettingsInCar:with:));
-
 - (void)resolveTemperatureForSetClimateSettingsInCar:(INSetClimateSettingsInCarIntent *)intent
-                                      withCompletion:(void (^)(INDoubleResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveTemperature(forSetClimateSettingsInCar:with:));
+                                      withCompletion:(void (^)(INTemperatureResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveTemperature(forSetClimateSettingsInCar:with:));
 
 - (void)resolveRelativeTemperatureSettingForSetClimateSettingsInCar:(INSetClimateSettingsInCarIntent *)intent
                                                      withCompletion:(void (^)(INRelativeSettingResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveRelativeTemperatureSetting(forSetClimateSettingsInCar:with:));
 
+- (void)resolveClimateZoneForSetClimateSettingsInCar:(INSetClimateSettingsInCarIntent *)intent
+                                      withCompletion:(void (^)(INCarSeatResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveClimateZone(forSetClimateSettingsInCar:with:));
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -9,6 +9,7 @@
 
 typedef NS_ENUM(NSInteger, INSetClimateSettingsInCarIntentResponseCode) {
     INSetClimateSettingsInCarIntentResponseCodeUnspecified = 0,
+    INSetClimateSettingsInCarIntentResponseCodeReady,
     INSetClimateSettingsInCarIntentResponseCodeInProgress,
     INSetClimateSettingsInCarIntentResponseCodeSuccess,
     INSetClimateSettingsInCarIntentResponseCodeFailure,
@@ -17,6 +18,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INSetClimateSettingsInCarIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetDefrosterSettingsInCarIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetDefrosterSettingsInCarIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetDefrosterSettingsInCarIntent.h	2016-05-25 06:33:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetDefrosterSettingsInCarIntent.h	2016-06-26 09:15:29.000000000 +0200
@@ -15,6 +15,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INSetDefrosterSettingsInCarIntent : INIntent
 
 - (instancetype)initWithEnable:(nullable NSNumber *)enable
@@ -34,6 +36,8 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INSetDefrosterSettingsInCarIntentHandling <NSObject>
 
 @required
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetDefrosterSettingsInCarIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetDefrosterSettingsInCarIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetDefrosterSettingsInCarIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetDefrosterSettingsInCarIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -9,6 +9,7 @@
 
 typedef NS_ENUM(NSInteger, INSetDefrosterSettingsInCarIntentResponseCode) {
     INSetDefrosterSettingsInCarIntentResponseCodeUnspecified = 0,
+    INSetDefrosterSettingsInCarIntentResponseCodeReady,
     INSetDefrosterSettingsInCarIntentResponseCodeInProgress,
     INSetDefrosterSettingsInCarIntentResponseCodeSuccess,
     INSetDefrosterSettingsInCarIntentResponseCodeFailure,
@@ -17,6 +18,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INSetDefrosterSettingsInCarIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetMessageAttributeIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetMessageAttributeIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetMessageAttributeIntent.h	2016-05-25 06:33:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetMessageAttributeIntent.h	2016-06-26 09:15:29.000000000 +0200
@@ -10,19 +10,20 @@
 
 #import <Intents/INMessageAttribute.h>
 
-@class INMessageAttributeResolutionResult;
 @class INStringResolutionResult;
+@class INMessageAttributeResolutionResult;
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INSetMessageAttributeIntent : INIntent
 
 - (instancetype)initWithIdentifiers:(nullable NSArray<NSString *> *)identifiers
-                          attribute:(nullable INMessageAttribute)attribute NS_DESIGNATED_INITIALIZER;
+                          attribute:(INMessageAttribute)attribute NS_DESIGNATED_INITIALIZER;
 
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSArray<NSString *> *identifiers;
 
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INMessageAttribute attribute;
+@property (readonly, assign, NS_NONATOMIC_IOSONLY) INMessageAttribute attribute;
 
 @end
 
@@ -34,6 +35,7 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @protocol INSetMessageAttributeIntentHandling <NSObject>
 
 @required
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetMessageAttributeIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetMessageAttributeIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetMessageAttributeIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetMessageAttributeIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -9,15 +9,18 @@
 
 typedef NS_ENUM(NSInteger, INSetMessageAttributeIntentResponseCode) {
     INSetMessageAttributeIntentResponseCodeUnspecified = 0,
+    INSetMessageAttributeIntentResponseCodeReady,
     INSetMessageAttributeIntentResponseCodeInProgress,
     INSetMessageAttributeIntentResponseCodeSuccess,
     INSetMessageAttributeIntentResponseCodeFailure,
     INSetMessageAttributeIntentResponseCodeFailureRequiringAppLaunch,
     INSetMessageAttributeIntentResponseCodeFailureMessageNotFound,
+    INSetMessageAttributeIntentResponseCodeFailureMessageAttributeNotSet,
 };
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INSetMessageAttributeIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntent.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntent.h	2016-06-26 09:14:37.000000000 +0200
@@ -0,0 +1,102 @@
+//
+//  INSetProfileInCarIntent.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Intents/INIntent.h>
+#import <Intents/INIntentResolutionResult.h>
+
+@class INIntegerResolutionResult;
+@class INStringResolutionResult;
+@class INBooleanResolutionResult;
+
+NS_ASSUME_NONNULL_BEGIN
+
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
+@interface INSetProfileInCarIntent : INIntent
+
+- (instancetype)initWithProfileNumber:(nullable NSNumber *)profileNumber
+                         profileLabel:(nullable NSString *)profileLabel
+                       defaultProfile:(nullable NSNumber *)defaultProfile NS_DESIGNATED_INITIALIZER NS_REFINED_FOR_SWIFT;
+
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *profileNumber NS_REFINED_FOR_SWIFT;
+
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *profileLabel;
+
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *defaultProfile NS_REFINED_FOR_SWIFT;
+
+@end
+
+@class INSetProfileInCarIntentResponse;
+
+/*!
+ @brief Protocol to declare support for handling an INSetProfileInCarIntent 
+ @abstract By implementing this protocol, a class can provide logic for resolving, confirming and handling the intent.
+ @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
+ */
+
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
+@protocol INSetProfileInCarIntentHandling <NSObject>
+
+@required
+
+/*!
+ @brief handling method
+
+ @abstract Execute the task represented by the INSetProfileInCarIntent that's passed in
+ @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+
+ @param  setProfileInCarIntent The input intent
+ @param  completion The response handling block takes a INSetProfileInCarIntentResponse containing the details of the result of having executed the intent
+
+ @see  INSetProfileInCarIntentResponse
+ */
+
+- (void)handleSetProfileInCar:(INSetProfileInCarIntent *)intent
+                   completion:(void (^)(INSetProfileInCarIntentResponse *response))completion NS_SWIFT_NAME(handle(setProfileInCar:completion:));
+
+@optional
+
+/*!
+ @brief Confirmation method
+ @abstract Validate that this intent is ready for the next step (i.e. handling)
+ @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+
+ @param  setProfileInCarIntent The input intent
+ @param  completion The response block contains an INSetProfileInCarIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
+
+ @see INSetProfileInCarIntentResponse
+
+ */
+
+- (void)confirmSetProfileInCar:(INSetProfileInCarIntent *)intent
+                    completion:(void (^)(INSetProfileInCarIntentResponse *response))completion NS_SWIFT_NAME(confirm(setProfileInCar:completion:));
+
+/*!
+ @brief Resolution methods
+ @abstract Determine if this intent is ready for the next step (confirmation)
+ @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+
+ @param  setProfileInCarIntent The input intent
+ @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
+
+ @see INIntentResolutionResult
+
+ */
+
+- (void)resolveProfileNumberForSetProfileInCar:(INSetProfileInCarIntent *)intent
+                                withCompletion:(void (^)(INIntegerResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveProfileNumber(forSetProfileInCar:with:));
+
+- (void)resolveProfileLabelForSetProfileInCar:(INSetProfileInCarIntent *)intent
+                               withCompletion:(void (^)(INStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveProfileLabel(forSetProfileInCar:with:));
+
+- (void)resolveDefaultProfileForSetProfileInCar:(INSetProfileInCarIntent *)intent
+                                 withCompletion:(void (^)(INBooleanResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveDefaultProfile(forSetProfileInCar:with:));
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntentResponse.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -0,0 +1,36 @@
+//
+//  INSetProfileInCarIntentResponse.h
+//  Intents
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Intents/INIntentResponse.h>
+
+typedef NS_ENUM(NSInteger, INSetProfileInCarIntentResponseCode) {
+    INSetProfileInCarIntentResponseCodeUnspecified = 0,
+    INSetProfileInCarIntentResponseCodeReady,
+    INSetProfileInCarIntentResponseCodeInProgress,
+    INSetProfileInCarIntentResponseCodeSuccess,
+    INSetProfileInCarIntentResponseCodeFailure,
+    INSetProfileInCarIntentResponseCodeFailureRequiringAppLaunch,
+};
+
+NS_ASSUME_NONNULL_BEGIN
+
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
+@interface INSetProfileInCarIntentResponse : INIntentResponse
+
+- (id)init NS_UNAVAILABLE;
+
+// The app extension has the option of capturing its private state as an NSUserActivity and returning it as the 'currentActivity'.
+// If the the app is launched, an NSUserActivity will be passed in with the private state.  The NSUserActivity may also be used to query the app's UI extension (if provided) for a view controller representing the current intent handling state.
+// In the case of app launch, the NSUserActivity will have its activityType set to the name of the intent. This intent object will also be available in the NSUserActivity.interaction property.
+- (instancetype)initWithCode:(INSetProfileInCarIntentResponseCode)code userActivity:(nullable NSUserActivity *)userActivity NS_DESIGNATED_INITIALIZER;
+
+@property (readonly, NS_NONATOMIC_IOSONLY) INSetProfileInCarIntentResponseCode code;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetRadioStationIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetRadioStationIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetRadioStationIntent.h	2016-05-25 06:33:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetRadioStationIntent.h	2016-06-26 09:14:37.000000000 +0200
@@ -17,6 +17,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INSetRadioStationIntent : INIntent
 
 - (instancetype)initWithRadioType:(INRadioType)radioType
@@ -45,6 +47,8 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INSetRadioStationIntentHandling <NSObject>
 
 @required
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetRadioStationIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetRadioStationIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetRadioStationIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetRadioStationIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -9,6 +9,7 @@
 
 typedef NS_ENUM(NSInteger, INSetRadioStationIntentResponseCode) {
     INSetRadioStationIntentResponseCodeUnspecified = 0,
+    INSetRadioStationIntentResponseCodeReady,
     INSetRadioStationIntentResponseCodeInProgress,
     INSetRadioStationIntentResponseCodeSuccess,
     INSetRadioStationIntentResponseCodeFailure,
@@ -18,6 +19,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INSetRadioStationIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatSettingsInCarIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatSettingsInCarIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatSettingsInCarIntent.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatSettingsInCarIntent.h	2016-06-26 09:15:29.000000000 +0200
@@ -0,0 +1,124 @@
+//
+//  INSetSeatSettingsInCarIntent.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Intents/INIntent.h>
+#import <Intents/INIntentResolutionResult.h>
+
+#import <Intents/INCarSeat.h>
+#import <Intents/INRelativeSetting.h>
+
+@class INBooleanResolutionResult;
+@class INCarSeatResolutionResult;
+@class INIntegerResolutionResult;
+@class INRelativeSettingResolutionResult;
+
+NS_ASSUME_NONNULL_BEGIN
+
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
+@interface INSetSeatSettingsInCarIntent : INIntent
+
+- (instancetype)initWithEnableHeating:(nullable NSNumber *)enableHeating
+                        enableCooling:(nullable NSNumber *)enableCooling
+                        enableMassage:(nullable NSNumber *)enableMassage
+                                 seat:(INCarSeat)seat
+                                level:(nullable NSNumber *)level
+                 relativeLevelSetting:(INRelativeSetting)relativeLevelSetting NS_DESIGNATED_INITIALIZER NS_REFINED_FOR_SWIFT;
+
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *enableHeating NS_REFINED_FOR_SWIFT;
+
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *enableCooling NS_REFINED_FOR_SWIFT;
+
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *enableMassage NS_REFINED_FOR_SWIFT;
+
+@property (readonly, assign, NS_NONATOMIC_IOSONLY) INCarSeat seat;
+
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *level NS_REFINED_FOR_SWIFT;
+
+@property (readonly, assign, NS_NONATOMIC_IOSONLY) INRelativeSetting relativeLevelSetting;
+
+@end
+
+@class INSetSeatSettingsInCarIntentResponse;
+
+/*!
+ @brief Protocol to declare support for handling an INSetSeatSettingsInCarIntent 
+ @abstract By implementing this protocol, a class can provide logic for resolving, confirming and handling the intent.
+ @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
+ */
+
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
+@protocol INSetSeatSettingsInCarIntentHandling <NSObject>
+
+@required
+
+/*!
+ @brief handling method
+
+ @abstract Execute the task represented by the INSetSeatSettingsInCarIntent that's passed in
+ @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+
+ @param  setSeatSettingsInCarIntent The input intent
+ @param  completion The response handling block takes a INSetSeatSettingsInCarIntentResponse containing the details of the result of having executed the intent
+
+ @see  INSetSeatSettingsInCarIntentResponse
+ */
+
+- (void)handleSetSeatSettingsInCar:(INSetSeatSettingsInCarIntent *)intent
+                        completion:(void (^)(INSetSeatSettingsInCarIntentResponse *response))completion NS_SWIFT_NAME(handle(setSeatSettingsInCar:completion:));
+
+@optional
+
+/*!
+ @brief Confirmation method
+ @abstract Validate that this intent is ready for the next step (i.e. handling)
+ @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+
+ @param  setSeatSettingsInCarIntent The input intent
+ @param  completion The response block contains an INSetSeatSettingsInCarIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
+
+ @see INSetSeatSettingsInCarIntentResponse
+
+ */
+
+- (void)confirmSetSeatSettingsInCar:(INSetSeatSettingsInCarIntent *)intent
+                         completion:(void (^)(INSetSeatSettingsInCarIntentResponse *response))completion NS_SWIFT_NAME(confirm(setSeatSettingsInCar:completion:));
+
+/*!
+ @brief Resolution methods
+ @abstract Determine if this intent is ready for the next step (confirmation)
+ @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+
+ @param  setSeatSettingsInCarIntent The input intent
+ @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
+
+ @see INIntentResolutionResult
+
+ */
+
+- (void)resolveEnableHeatingForSetSeatSettingsInCar:(INSetSeatSettingsInCarIntent *)intent
+                                     withCompletion:(void (^)(INBooleanResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveEnableHeating(forSetSeatSettingsInCar:with:));
+
+- (void)resolveEnableCoolingForSetSeatSettingsInCar:(INSetSeatSettingsInCarIntent *)intent
+                                     withCompletion:(void (^)(INBooleanResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveEnableCooling(forSetSeatSettingsInCar:with:));
+
+- (void)resolveEnableMassageForSetSeatSettingsInCar:(INSetSeatSettingsInCarIntent *)intent
+                                     withCompletion:(void (^)(INBooleanResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveEnableMassage(forSetSeatSettingsInCar:with:));
+
+- (void)resolveSeatForSetSeatSettingsInCar:(INSetSeatSettingsInCarIntent *)intent
+                            withCompletion:(void (^)(INCarSeatResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveSeat(forSetSeatSettingsInCar:with:));
+
+- (void)resolveLevelForSetSeatSettingsInCar:(INSetSeatSettingsInCarIntent *)intent
+                             withCompletion:(void (^)(INIntegerResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveLevel(forSetSeatSettingsInCar:with:));
+
+- (void)resolveRelativeLevelSettingForSetSeatSettingsInCar:(INSetSeatSettingsInCarIntent *)intent
+                                            withCompletion:(void (^)(INRelativeSettingResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveRelativeLevelSetting(forSetSeatSettingsInCar:with:));
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatSettingsInCarIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatSettingsInCarIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatSettingsInCarIntentResponse.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatSettingsInCarIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -0,0 +1,36 @@
+//
+//  INSetSeatSettingsInCarIntentResponse.h
+//  Intents
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Intents/INIntentResponse.h>
+
+typedef NS_ENUM(NSInteger, INSetSeatSettingsInCarIntentResponseCode) {
+    INSetSeatSettingsInCarIntentResponseCodeUnspecified = 0,
+    INSetSeatSettingsInCarIntentResponseCodeReady,
+    INSetSeatSettingsInCarIntentResponseCodeInProgress,
+    INSetSeatSettingsInCarIntentResponseCodeSuccess,
+    INSetSeatSettingsInCarIntentResponseCodeFailure,
+    INSetSeatSettingsInCarIntentResponseCodeFailureRequiringAppLaunch,
+};
+
+NS_ASSUME_NONNULL_BEGIN
+
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
+@interface INSetSeatSettingsInCarIntentResponse : INIntentResponse
+
+- (id)init NS_UNAVAILABLE;
+
+// The app extension has the option of capturing its private state as an NSUserActivity and returning it as the 'currentActivity'.
+// If the the app is launched, an NSUserActivity will be passed in with the private state.  The NSUserActivity may also be used to query the app's UI extension (if provided) for a view controller representing the current intent handling state.
+// In the case of app launch, the NSUserActivity will have its activityType set to the name of the intent. This intent object will also be available in the NSUserActivity.interaction property.
+- (instancetype)initWithCode:(INSetSeatSettingsInCarIntentResponseCode)code userActivity:(nullable NSUserActivity *)userActivity NS_DESIGNATED_INITIALIZER;
+
+@property (readonly, NS_NONATOMIC_IOSONLY) INSetSeatSettingsInCarIntentResponseCode code;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatTemperatureInCarIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatTemperatureInCarIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatTemperatureInCarIntent.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatTemperatureInCarIntent.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,116 +0,0 @@
-//
-//  INSetSeatTemperatureInCarIntent.h
-//  Intents
-//
-//  Copyright © 2016 Apple. All rights reserved.
-//
-
-#import <Intents/INIntent.h>
-#import <Intents/INIntentResolutionResult.h>
-
-#import <Intents/INCarSeat.h>
-#import <Intents/INRelativeSetting.h>
-#import <Intents/INTemperatureMode.h>
-
-@class INBooleanResolutionResult;
-@class INCarSeatResolutionResult;
-@class INTemperatureModeResolutionResult;
-@class INIntegerResolutionResult;
-@class INRelativeSettingResolutionResult;
-
-NS_ASSUME_NONNULL_BEGIN
-
-@interface INSetSeatTemperatureInCarIntent : INIntent
-
-- (instancetype)initWithEnable:(nullable NSNumber *)enable
-                          seat:(INCarSeat)seat
-               temperatureMode:(INTemperatureMode)temperatureMode
-                         level:(nullable NSNumber *)level
-          relativeLevelSetting:(INRelativeSetting)relativeLevelSetting NS_DESIGNATED_INITIALIZER NS_REFINED_FOR_SWIFT;
-
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *enable NS_REFINED_FOR_SWIFT;
-
-@property (readonly, assign, NS_NONATOMIC_IOSONLY) INCarSeat seat;
-
-@property (readonly, assign, NS_NONATOMIC_IOSONLY) INTemperatureMode temperatureMode;
-
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *level NS_REFINED_FOR_SWIFT;
-
-@property (readonly, assign, NS_NONATOMIC_IOSONLY) INRelativeSetting relativeLevelSetting;
-
-@end
-
-@class INSetSeatTemperatureInCarIntentResponse;
-
-/*!
- @brief Protocol to declare support for handling an INSetSeatTemperatureInCarIntent 
- @abstract By implementing this protocol, a class can provide logic for resolving, confirming and handling the intent.
- @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
- */
-
-@protocol INSetSeatTemperatureInCarIntentHandling <NSObject>
-
-@required
-
-/*!
- @brief handling method
-
- @abstract Execute the task represented by the INSetSeatTemperatureInCarIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
-
- @param  setSeatTemperatureInCarIntent The input intent
- @param  completion The response handling block takes a INSetSeatTemperatureInCarIntentResponse containing the details of the result of having executed the intent
-
- @see  INSetSeatTemperatureInCarIntentResponse
- */
-
-- (void)handleSetSeatTemperatureInCar:(INSetSeatTemperatureInCarIntent *)intent
-                           completion:(void (^)(INSetSeatTemperatureInCarIntentResponse *response))completion NS_SWIFT_NAME(handle(setSeatTemperatureInCar:completion:));
-
-@optional
-
-/*!
- @brief Confirmation method
- @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
-
- @param  setSeatTemperatureInCarIntent The input intent
- @param  completion The response block contains an INSetSeatTemperatureInCarIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
-
- @see INSetSeatTemperatureInCarIntentResponse
-
- */
-
-- (void)confirmSetSeatTemperatureInCar:(INSetSeatTemperatureInCarIntent *)intent
-                            completion:(void (^)(INSetSeatTemperatureInCarIntentResponse *response))completion NS_SWIFT_NAME(confirm(setSeatTemperatureInCar:completion:));
-
-/*!
- @brief Resolution methods
- @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
-
- @param  setSeatTemperatureInCarIntent The input intent
- @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
-
- @see INIntentResolutionResult
-
- */
-
-- (void)resolveEnableForSetSeatTemperatureInCar:(INSetSeatTemperatureInCarIntent *)intent
-                                 withCompletion:(void (^)(INBooleanResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveEnable(forSetSeatTemperatureInCar:with:));
-
-- (void)resolveSeatForSetSeatTemperatureInCar:(INSetSeatTemperatureInCarIntent *)intent
-                               withCompletion:(void (^)(INCarSeatResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveSeat(forSetSeatTemperatureInCar:with:));
-
-- (void)resolveTemperatureModeForSetSeatTemperatureInCar:(INSetSeatTemperatureInCarIntent *)intent
-                                          withCompletion:(void (^)(INTemperatureModeResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveTemperatureMode(forSetSeatTemperatureInCar:with:));
-
-- (void)resolveLevelForSetSeatTemperatureInCar:(INSetSeatTemperatureInCarIntent *)intent
-                                withCompletion:(void (^)(INIntegerResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveLevel(forSetSeatTemperatureInCar:with:));
-
-- (void)resolveRelativeLevelSettingForSetSeatTemperatureInCar:(INSetSeatTemperatureInCarIntent *)intent
-                                               withCompletion:(void (^)(INRelativeSettingResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveRelativeLevelSetting(forSetSeatTemperatureInCar:with:));
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatTemperatureInCarIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatTemperatureInCarIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatTemperatureInCarIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatTemperatureInCarIntentResponse.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,33 +0,0 @@
-//
-//  INSetSeatTemperatureInCarIntentResponse.h
-//  Intents
-//
-//  Copyright © 2016 Apple Inc. All rights reserved.
-//
-
-#import <Intents/INIntentResponse.h>
-
-typedef NS_ENUM(NSInteger, INSetSeatTemperatureInCarIntentResponseCode) {
-    INSetSeatTemperatureInCarIntentResponseCodeUnspecified = 0,
-    INSetSeatTemperatureInCarIntentResponseCodeInProgress,
-    INSetSeatTemperatureInCarIntentResponseCodeSuccess,
-    INSetSeatTemperatureInCarIntentResponseCodeFailure,
-    INSetSeatTemperatureInCarIntentResponseCodeFailureRequiringAppLaunch,
-};
-
-NS_ASSUME_NONNULL_BEGIN
-
-@interface INSetSeatTemperatureInCarIntentResponse : INIntentResponse
-
-- (id)init NS_UNAVAILABLE;
-
-// The app extension has the option of capturing its private state as an NSUserActivity and returning it as the 'currentActivity'.
-// If the the app is launched, an NSUserActivity will be passed in with the private state.  The NSUserActivity may also be used to query the app's UI extension (if provided) for a view controller representing the current intent handling state.
-// In the case of app launch, the NSUserActivity will have its activityType set to the name of the intent. This intent object will also be available in the NSUserActivity.interaction property.
-- (instancetype)initWithCode:(INSetSeatTemperatureInCarIntentResponseCode)code userActivity:(nullable NSUserActivity *)userActivity NS_DESIGNATED_INITIALIZER;
-
-@property (readonly, NS_NONATOMIC_IOSONLY) INSetSeatTemperatureInCarIntentResponseCode code;
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakable.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakable.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakable.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakable.h	2016-06-26 09:15:29.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h	2016-06-26 09:15:29.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h	2016-06-26 09:15:29.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntent.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntent.h	2016-06-26 09:15:29.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntent.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntent.h	2016-06-26 09:15:29.000000000 +0200
@@ -22,6 +22,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
 @interface INStartPhotoPlaybackIntent : INIntent
 
 - (instancetype)initWithDateCreated:(nullable INDateComponentsRange *)dateCreated
@@ -69,6 +70,7 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(ios(10.0))
 @protocol INStartPhotoPlaybackIntentHandling <NSObject>
 
 @required
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -9,14 +9,15 @@
 
 typedef NS_ENUM(NSInteger, INStartPhotoPlaybackIntentResponseCode) {
     INStartPhotoPlaybackIntentResponseCodeUnspecified = 0,
-    INStartPhotoPlaybackIntentResponseCodeInProgress,
-    INStartPhotoPlaybackIntentResponseCodeSuccess,
+    INStartPhotoPlaybackIntentResponseCodeReady,
+    INStartPhotoPlaybackIntentResponseCodeContinueInApp,
     INStartPhotoPlaybackIntentResponseCodeFailure,
     INStartPhotoPlaybackIntentResponseCodeFailureRequiringAppLaunch,
 };
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
 @interface INStartPhotoPlaybackIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntent.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntent.h	2016-06-26 09:15:29.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartWorkoutIntent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartWorkoutIntent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartWorkoutIntent.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartWorkoutIntent.h	2016-06-26 09:15:29.000000000 +0200
@@ -11,7 +11,8 @@
 #import <Intents/INWorkoutGoalUnitType.h>
 #import <Intents/INWorkoutLocationType.h>
 
-@class INStringResolutionResult;
+@class INSpeakableString;
+@class INSpeakableStringResolutionResult;
 @class INDoubleResolutionResult;
 @class INWorkoutGoalUnitTypeResolutionResult;
 @class INWorkoutLocationTypeResolutionResult;
@@ -19,15 +20,17 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INStartWorkoutIntent : INIntent
 
-- (instancetype)initWithWorkoutName:(nullable NSString *)workoutName
+- (instancetype)initWithWorkoutName:(nullable INSpeakableString *)workoutName
                           goalValue:(nullable NSNumber *)goalValue
                 workoutGoalUnitType:(INWorkoutGoalUnitType)workoutGoalUnitType
                 workoutLocationType:(INWorkoutLocationType)workoutLocationType
                         isOpenEnded:(nullable NSNumber *)isOpenEnded NS_DESIGNATED_INITIALIZER NS_REFINED_FOR_SWIFT;
 
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *workoutName;
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INSpeakableString *workoutName;
 
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *goalValue NS_REFINED_FOR_SWIFT;
 
@@ -47,6 +50,8 @@
  @discussion The minimum requirement for an implementing class is that it should be able to handle the intent. The resolution and confirmation methods are optional. The handling method is always called last, after resolving and confirming the intent.
  */
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @protocol INStartWorkoutIntentHandling <NSObject>
 
 @required
@@ -96,7 +101,7 @@
  */
 
 - (void)resolveWorkoutNameForStartWorkout:(INStartWorkoutIntent *)intent
-                           withCompletion:(void (^)(INStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveWorkoutName(forStartWorkout:with:));
+                           withCompletion:(void (^)(INSpeakableStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveWorkoutName(forStartWorkout:with:));
 
 - (void)resolveGoalValueForStartWorkout:(INStartWorkoutIntent *)intent
                          withCompletion:(void (^)(INDoubleResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveGoalValue(forStartWorkout:with:));
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartWorkoutIntentResponse.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartWorkoutIntentResponse.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartWorkoutIntentResponse.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartWorkoutIntentResponse.h	2016-06-26 09:15:29.000000000 +0200
@@ -9,8 +9,8 @@
 
 typedef NS_ENUM(NSInteger, INStartWorkoutIntentResponseCode) {
     INStartWorkoutIntentResponseCodeUnspecified = 0,
-    INStartWorkoutIntentResponseCodeInProgress,
-    INStartWorkoutIntentResponseCodeSuccess,
+    INStartWorkoutIntentResponseCodeReady,
+    INStartWorkoutIntentResponseCodeContinueInApp,
     INStartWorkoutIntentResponseCodeFailure,
     INStartWorkoutIntentResponseCodeFailureRequiringAppLaunch,
     INStartWorkoutIntentResponseCodeFailureOngoingWorkout,
@@ -19,6 +19,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+API_AVAILABLE(ios(10.0))
+API_UNAVAILABLE(macosx)
 @interface INStartWorkoutIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h	2016-06-26 09:15:29.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperature.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperature.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperature.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperature.h	2016-06-26 09:15:29.000000000 +0200
@@ -0,0 +1,26 @@
+//
+//  INTemperature.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@interface INTemperature : NSObject <NSCopying, NSSecureCoding>
+
+- (instancetype)init NS_UNAVAILABLE;
+
+- (instancetype)initWithUnit:(NSUnitTemperature *)unit
+                       value:(NSNumber *)value NS_DESIGNATED_INITIALIZER NS_REFINED_FOR_SWIFT;
+
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSUnitTemperature *unit;
+
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *value NS_REFINED_FOR_SWIFT;
+
+@end
+
+NS_ASSUME_NONNULL_END
+
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureMode.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureMode.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureMode.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureMode.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,21 +0,0 @@
-//
-//  INTemperatureMode.h
-//  Intents
-//
-//  Copyright © 2016 Apple. All rights reserved.
-//
-
-#ifndef INTemperatureMode_h
-#define INTemperatureMode_h
-
-#import <Foundation/Foundation.h>
-
-#import <Intents/IntentsDefines.h>
-
-typedef NS_ENUM(NSInteger, INTemperatureMode) {
-    INTemperatureModeUnknown = 0,
-    INTemperatureModeHeating,
-    INTemperatureModeCooling,
-};
-
-#endif // INTemperatureMode_h
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureModeResolutionResult.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureModeResolutionResult.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureModeResolutionResult.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureModeResolutionResult.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,24 +0,0 @@
-//
-//  INTemperatureModeResolutionResult.h
-//  Intents
-//
-//  Copyright © 2016 Apple. All rights reserved.
-//
-
-#import <Intents/INIntentResolutionResult.h>
-
-#import <Intents/INTemperatureMode.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-@interface INTemperatureModeResolutionResult : INIntentResolutionResult
-
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
-+ (instancetype)successWithResolvedValue:(INTemperatureMode)resolvedValue NS_SWIFT_NAME(success(with:));
-
-// This resolution result is to ask Siri to confirm if this is the value with which the user wants to continue.
-+ (instancetype)confirmationRequiredWithValueToConfirm:(INTemperatureMode)valueToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureResolutionResult.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureResolutionResult.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureResolutionResult.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureResolutionResult.h	2016-06-26 09:15:29.000000000 +0200
@@ -0,0 +1,30 @@
+//
+//  INTemperatureResolutionResult.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Intents/INIntentResolutionResult.h>
+
+@class INTemperature;
+
+NS_ASSUME_NONNULL_BEGIN
+
+@interface INTemperatureResolutionResult : INIntentResolutionResult
+
+// This resolution result is for when the app extension wants to tell Siri to proceed with a given temperature. The resolvedTemperature need not be identical to the input temperature. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
++ (instancetype)successWithResolvedTemperature:(INTemperature *)resolvedTemperature NS_SWIFT_NAME(success(with:));
+
+// This resolution result is to ask Siri to disambiguate between the provided temperatures.
++ (instancetype)disambiguationWithTemperaturesToDisambiguate:(NSArray<INTemperature *> *)temperaturesToDisambiguate NS_SWIFT_NAME(disambiguation(with:));
+
+// This resolution result is to ask Siri to confirm if this is the temperature with which the user wants to continue.
++ (instancetype)confirmationRequiredWithTemperatureToConfirm:(nullable INTemperature *)temperatureToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
+
+// This resolution result is to inform Siri that in order to continue, the app extension needs the temperature to be filled in greater detail. If this parameter is nil and the app extension wants to request a non-nil value, it should use +needsValue.
++ (instancetype)needsMoreDetailsForTemperature:(INTemperature *)temperatureToComplete NS_SWIFT_NAME(needsMoreDetails(for:));
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureUnit.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureUnit.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureUnit.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureUnit.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,21 +0,0 @@
-//
-//  INTemperatureUnit.h
-//  Intents
-//
-//  Copyright © 2016 Apple. All rights reserved.
-//
-
-#ifndef INTemperatureUnit_h
-#define INTemperatureUnit_h
-
-#import <Foundation/Foundation.h>
-
-#import <Intents/IntentsDefines.h>
-
-typedef NS_ENUM(NSInteger, INTemperatureUnit) {
-    INTemperatureUnitUnknown = 0,
-    INTemperatureUnitCelsius,
-    INTemperatureUnitFahrenheit,
-};
-
-#endif // INTemperatureUnit_h
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureUnitResolutionResult.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureUnitResolutionResult.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureUnitResolutionResult.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureUnitResolutionResult.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,24 +0,0 @@
-//
-//  INTemperatureUnitResolutionResult.h
-//  Intents
-//
-//  Copyright © 2016 Apple. All rights reserved.
-//
-
-#import <Intents/INIntentResolutionResult.h>
-
-#import <Intents/INTemperatureUnit.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-@interface INTemperatureUnitResolutionResult : INIntentResolutionResult
-
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
-+ (instancetype)successWithResolvedValue:(INTemperatureUnit)resolvedValue NS_SWIFT_NAME(success(with:));
-
-// This resolution result is to ask Siri to confirm if this is the value with which the user wants to continue.
-+ (instancetype)confirmationRequiredWithValueToConfirm:(INTemperatureUnit)valueToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTermsAndConditions.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTermsAndConditions.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTermsAndConditions.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTermsAndConditions.h	2016-06-26 09:15:29.000000000 +0200
@@ -0,0 +1,23 @@
+//
+//  INTermsAndConditions.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+// This API requires you to work with Apple Maps before your application can use it. For information on how to get started, please go to MapsConnect.
+//
+// http://mapsconnect.apple.com/info/extensions
+
+NS_ASSUME_NONNULL_BEGIN
+
+NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+@interface INTermsAndConditions : NSObject <NSSecureCoding, NSCopying>
+
+- (instancetype)initWithLocalizedTermsAndConditionsText:(NSString *)localizedTermsAndConditionsText privacyPolicyURL:(nullable NSURL*)privacyPolicyURL termsAndConditionsURL:(nullable NSURL *)termsAndConditionsURL NS_DESIGNATED_INITIALIZER;
+
+@property (readonly, NS_NONATOMIC_IOSONLY) NSString *localizedTermsAndConditionsText; // A string that contains a summary of the vendor's terms and conditions.
+@property (readonly, nullable, NS_NONATOMIC_IOSONLY) NSURL *privacyPolicyURL; // An optional URL that links to the vendor's privacy policy.
+@property (readonly, nullable, NS_NONATOMIC_IOSONLY) NSURL *termsAndConditionsURL; // An optional URL that links to the vendor's full terms and conditions.
+
+@end
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INVocabulary.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INVocabulary.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INVocabulary.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INVocabulary.h	2016-06-26 09:15:29.000000000 +0200
@@ -9,22 +9,26 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-
 typedef NS_ENUM(NSInteger, INVocabularyStringType) {
-    /// The name of a contact as a person will say it, for example “Jon Smith”, “Apple Inc”.
+    /// The name of a contact as a person will say it, for example “Jon Smith”, “Apple”.
     INVocabularyStringTypeContactName = 1,
 
     /// The name of a group of contacts as a person will say it, for example "Tahoe Trip".
     INVocabularyStringTypeContactGroupName,
 
-    /// A user-defined keyword associated with an image or images, for example "food", "Vacation"
+    /// A keyword associated with an image or images, for example "food", "Vacation".
     INVocabularyStringTypePhotoTag = 100,
 
-    /// The name a user has given to a collection of photographs, for example "WWDC 2015 Karaoke"
+    /// The name for a photograph album, for example "WWDC 2015 Karaoke".
+    /// You may find that INVocabularyStringTypePhotoTag is a better match for concepts that are similar to, but not exactly, albums.
     INVocabularyStringTypePhotoAlbumName,
 
     /// The name a user has created for a workout, for example  “Half Marathon”, “Kettlebell exercise”
     INVocabularyStringTypeWorkoutActivityName = 200,
+
+    /// The name of a vehicle configuration profile, for example "Roadtrip", "Rally", "Good Weather".
+    /// For use by automaker apps that are enabled to work with CarPlay <https://developer.apple.com/carplay/>.
+    INVocabularyStringTypeCarProfileName = 300,
 };
 
 @interface INVocabulary : NSObject
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h	2016-05-25 06:28:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h	2016-06-26 09:14:37.000000000 +0200
@@ -23,9 +23,9 @@
 #import <Intents/INIntentIdentifiers.h>
 #import <Intents/INIntentResponse.h>
 #import <Intents/INIntentResolutionResult.h>
-#import <Intents/INIntentResolutionResultUnsupportedReason.h>
 #import <Intents/INDomainHandling.h>
 #import <Intents/INInteraction.h>
+#import <Intents/INSpeakable.h>
 
 // Intents & Intent Responses
 #import <Intents/INIntents.h>
@@ -35,12 +35,15 @@
 #import <Intents/INExtension.h>
 
 // Common Types
+#import <Intents/INPersonHandle.h>
 #import <Intents/INCurrencyAmount.h>
 #import <Intents/INDateComponentsRange.h>
 #import <Intents/INImage.h>
 #import <Intents/INPaymentMethod.h>
 #import <Intents/INPaymentMethodType.h>
 #import <Intents/INPerson.h>
+#import <Intents/INTemperature.h>
+#import <Intents/INSpeakableString.h>
 
 // Common Resolution Results
 #import <Intents/INBooleanResolutionResult.h>
@@ -48,10 +51,11 @@
 #import <Intents/INDateComponentsRangeResolutionResult.h>
 #import <Intents/INDoubleResolutionResult.h>
 #import <Intents/INIntegerResolutionResult.h>
-#import <Intents/INPaymentMethodResolutionResult.h>
 #import <Intents/INPersonResolutionResult.h>
 #import <Intents/INPlacemarkResolutionResult.h>
+#import <Intents/INSpeakableStringResolutionResult.h>
 #import <Intents/INStringResolutionResult.h>
+#import <Intents/INTemperatureResolutionResult.h>
 
 // Calls Domain
 #import <Intents/INSearchCallHistoryIntent.h>
@@ -73,8 +77,12 @@
 #import <Intents/INSetClimateSettingsInCarIntentResponse.h>
 #import <Intents/INSetDefrosterSettingsInCarIntent.h>
 #import <Intents/INSetDefrosterSettingsInCarIntentResponse.h>
-#import <Intents/INSetSeatTemperatureInCarIntent.h>
-#import <Intents/INSetSeatTemperatureInCarIntentResponse.h>
+#import <Intents/INSetSeatSettingsInCarIntent.h>
+#import <Intents/INSetSeatSettingsInCarIntentResponse.h>
+#import <Intents/INSetProfileInCarIntent.h>
+#import <Intents/INSetProfileInCarIntentResponse.h>
+#import <Intents/INSaveProfileInCarIntent.h>
+#import <Intents/INSaveProfileInCarIntentResponse.h>
 #import <Intents/INSetRadioStationIntent.h>
 #import <Intents/INSetRadioStationIntentResponse.h>
 
@@ -92,10 +100,6 @@
 #import <Intents/INRelativeReferenceResolutionResult.h>
 #import <Intents/INRelativeSetting.h>
 #import <Intents/INRelativeSettingResolutionResult.h>
-#import <Intents/INTemperatureMode.h>
-#import <Intents/INTemperatureModeResolutionResult.h>
-#import <Intents/INTemperatureUnit.h>
-#import <Intents/INTemperatureUnitResolutionResult.h>
 
 // Messages Domain
 #import <Intents/INSearchForMessagesIntent.h>
@@ -110,7 +114,6 @@
 #import <Intents/INMessageAttributeResolutionResult.h>
 #import <Intents/INMessageAttributeOptions.h>
 #import <Intents/INMessageAttributeOptionsResolutionResult.h>
-#import <Intents/INMessageService.h>
 
 // Payments Domain
 #import <Intents/INSendPaymentIntent.h>
@@ -146,6 +149,7 @@
 #import <Intents/INRideVehicle.h>
 #import <Intents/INRideFareLineItem.h>
 #import <Intents/INRidePartySizeOption.h>
+#import <Intents/INRideCompletionStatus.h>
 
 // Workouts Domain
 #import <Intents/INStartWorkoutIntent.h>
@@ -175,3 +179,4 @@
 #import <Intents/INPreferences.h>
 #import <Intents/CLPlacemark+IntentsAdditions.h>
 #import <Intents/NSUserActivity+IntentsAdditions.h>
+#import <Intents/INPerson+SiriAdditions.h>

```