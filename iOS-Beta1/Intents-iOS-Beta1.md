#Intents.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/CLPlacemark+IntentsAdditions.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/CLPlacemark+IntentsAdditions.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/CLPlacemark+IntentsAdditions.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/CLPlacemark+IntentsAdditions.h	2016-10-22 02:34:38.000000000 +0200
@@ -16,7 +16,7 @@
 
 + (instancetype)placemarkWithLocation:(CLLocation *)location
                                  name:(nullable NSString *)name
-                        postalAddress:(nullable CNPostalAddress *)postalAddress API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx, watchos, tvos);
+                        postalAddress:(nullable CNPostalAddress *)postalAddress API_AVAILABLE(ios(10.0), watchos(3.1));
 
 @end
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INBookRestaurantReservationIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INBookRestaurantReservationIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INBookRestaurantReservationIntent.h	2016-09-28 09:40:42.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INBookRestaurantReservationIntent.h	2016-10-22 02:34:38.000000000 +0200
@@ -45,7 +45,7 @@
  @brief handling method
  
  @abstract Execute the task represented by the INBookRestaurantReservationIntent that's passed in
- @discussion This method are called to actually execute the intent, the app must return a response for this intent and an NSUserActivity capturing the state that the app must be restored to at the end of handling this intent
+ @discussion This method is called to actually execute the intent, the app must return a response for this intent and an NSUserActivity capturing the state that the app must be restored to at the end of handling this intent
  
  @param  bookingIntent The input intent
  @param  completion The response handling block to invoke with the response to handling the intent.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCallRecordTypeResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCallRecordTypeResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCallRecordTypeResolutionResult.h	2016-09-28 09:41:00.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCallRecordTypeResolutionResult.h	2016-10-22 02:34:37.000000000 +0200
@@ -13,7 +13,8 @@
 
 @interface INCallRecordTypeResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INCallRecordType. The resolvedValue can be different than the original INCallRecordType. This allows app extensions to apply business logic constraints.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedValue:(INCallRecordType)resolvedValue NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to confirm if this is the value with which the user wants to continue.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCancelWorkoutIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCancelWorkoutIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCancelWorkoutIntent.h	2016-09-28 09:41:00.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCancelWorkoutIntent.h	2016-10-22 02:34:37.000000000 +0200
@@ -17,6 +17,7 @@
 API_UNAVAILABLE(macosx)
 @interface INCancelWorkoutIntent : INIntent
 
+// Designated initializer. The `workoutName` can use `INWorkoutNameIdentifier` as its `identifier` parameter.
 - (instancetype)initWithWorkoutName:(nullable INSpeakableString *)workoutName NS_DESIGNATED_INITIALIZER;
 
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INSpeakableString *workoutName;
@@ -41,7 +42,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INCancelWorkoutIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  cancelWorkoutIntent The input intent
  @param  completion The response handling block takes a INCancelWorkoutIntentResponse containing the details of the result of having executed the intent
@@ -57,7 +58,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  cancelWorkoutIntent The input intent
  @param  completion The response block contains an INCancelWorkoutIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -72,7 +73,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  cancelWorkoutIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCarAirCirculationModeResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCarAirCirculationModeResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCarAirCirculationModeResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCarAirCirculationModeResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -13,7 +13,8 @@
 
 @interface INCarAirCirculationModeResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INCarAirCirculationMode. The resolvedValue can be different than the original INCarAirCirculationMode. This allows app extensions to apply business logic constraints.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedValue:(INCarAirCirculationMode)resolvedValue NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to confirm if this is the value with which the user wants to continue.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCarAudioSourceResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCarAudioSourceResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCarAudioSourceResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCarAudioSourceResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -13,7 +13,8 @@
 
 @interface INCarAudioSourceResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INCarAudioSource. The resolvedValue can be different than the original INCarAudioSource. This allows app extensions to apply business logic constraints.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedValue:(INCarAudioSource)resolvedValue NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to confirm if this is the value with which the user wants to continue.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCarDefrosterResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCarDefrosterResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCarDefrosterResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCarDefrosterResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -13,7 +13,8 @@
 
 @interface INCarDefrosterResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INCarDefroster. The resolvedValue can be different than the original INCarDefroster. This allows app extensions to apply business logic constraints.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedValue:(INCarDefroster)resolvedValue NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to confirm if this is the value with which the user wants to continue.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCarSeatResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCarSeatResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCarSeatResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCarSeatResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -13,7 +13,8 @@
 
 @interface INCarSeatResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INCarSeat. The resolvedValue can be different than the original INCarSeat. This allows app extensions to apply business logic constraints.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedValue:(INCarSeat)resolvedValue NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to confirm if this is the value with which the user wants to continue.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmount.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmount.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmount.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmount.h	2016-10-22 02:34:38.000000000 +0200
@@ -19,6 +19,7 @@
 
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSDecimalNumber *amount;
 
+// The ISO 4217 currency code that applies to the monetary amount.
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *currencyCode;
 
 @end
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmountResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmountResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmountResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INCurrencyAmountResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -14,7 +14,8 @@
 API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx)
 @interface INCurrencyAmountResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given currency amount. The resolvedCurrencyAmount need not be identical to the input currency amount. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INCurrencyAmount. The resolvedCurrencyAmount can be different than the original INCurrencyAmount. This allows app extension to apply business logic constraints. For example, the extension could round the amount to the nearest dollar.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedCurrencyAmount:(INCurrencyAmount *)resolvedCurrencyAmount NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to disambiguate between the provided currency amounts.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsRangeResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -14,7 +14,8 @@
 API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INDateComponentsRangeResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given date components range. The resolvedDateComponentsRange need not be identical to the input date components range. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INDateComponentsRange. The resolvedDateComponentsRange can be different than the original INDateComponentsRange. This allows app extensions to pick a suitable range.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedDateComponentsRange:(INDateComponentsRange *)resolvedDateComponentsRange NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to disambiguate between the provided date components ranges.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDateComponentsResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -12,7 +12,8 @@
 API_AVAILABLE(ios(10.0))
 @interface INDateComponentsResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given dateComponents. The resolvedDateComponents need not be identical to the input dateComponents. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given NSDateComponents. The resolvedDateComponents can be different than the original NSDateComponents. This allows app extensions to apply business logic constraints. For example, the extension could round the interval to the nearest day.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedDateComponents:(NSDateComponents *)resolvedDateComponents NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to disambiguate between the provided dateComponentss.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDomainHandling.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDomainHandling.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDomainHandling.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDomainHandling.h	2016-10-22 02:34:38.000000000 +0200
@@ -12,7 +12,7 @@
 @end
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(macosx, watchos)
 @protocol INCarPlayDomainHandling <INSetAudioSourceInCarIntentHandling, INSetClimateSettingsInCarIntentHandling, INSetDefrosterSettingsInCarIntentHandling, INSetSeatSettingsInCarIntentHandling, INSetProfileInCarIntentHandling, INSaveProfileInCarIntentHandling>
 @end
 
@@ -22,7 +22,7 @@
 @end
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(macosx, watchos)
 @protocol INRadioDomainHandling <INSetRadioStationIntentHandling>
 @end
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDoubleResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDoubleResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDoubleResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INDoubleResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -12,7 +12,8 @@
 API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx)
 @interface INDoubleResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given number. The resolvedValue can be different than the original number. This allows app extensions to apply business logic constraints. For example, the extension could precisely control rounding the value.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedValue:(double)resolvedValue NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to confirm if this is the double value with which the user wants to continue.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INEndWorkoutIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INEndWorkoutIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INEndWorkoutIntent.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INEndWorkoutIntent.h	2016-10-22 02:34:37.000000000 +0200
@@ -17,6 +17,7 @@
 API_UNAVAILABLE(macosx)
 @interface INEndWorkoutIntent : INIntent
 
+// Designated initializer. The `workoutName` can use `INWorkoutNameIdentifier` as its `identifier` parameter.
 - (instancetype)initWithWorkoutName:(nullable INSpeakableString *)workoutName NS_DESIGNATED_INITIALIZER;
 
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INSpeakableString *workoutName;
@@ -41,7 +42,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INEndWorkoutIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  endWorkoutIntent The input intent
  @param  completion The response handling block takes a INEndWorkoutIntentResponse containing the details of the result of having executed the intent
@@ -57,7 +58,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  endWorkoutIntent The input intent
  @param  completion The response block contains an INEndWorkoutIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -72,7 +73,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  endWorkoutIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingDefaultsIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingDefaultsIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingDefaultsIntent.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingDefaultsIntent.h	2016-10-22 02:34:38.000000000 +0200
@@ -33,7 +33,7 @@
  @brief handling method
  
  @abstract Execute the task represented by the INGetAvailableRestaurantReservationBookingDefaultsIntent that's passed in
- @discussion This method are called to actually execute the intent, the app must return a response for this intent and an NSUserActivity capturing the state that the app must be restored to at the end of handling this intent
+ @discussion This method is called to actually execute the intent, the app must return a response for this intent and an NSUserActivity capturing the state that the app must be restored to at the end of handling this intent
  
  @param  bookingDefaultsIntent The input intent
  @param  completion The response handling block to invoke with the response to handling the intent.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingsIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingsIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingsIntent.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetAvailableRestaurantReservationBookingsIntent.h	2016-10-22 02:34:38.000000000 +0200
@@ -43,7 +43,7 @@
  @brief handling method
  
  @abstract Execute the task represented by the INGetAvailableRestaurantReservationBookingsIntent that's passed in
- @discussion This method are called to actually execute the intent, the app must return a response for this intent and an NSUserActivity capturing the state that the app must be restored to at the end of handling this intent
+ @discussion This method is called to actually execute the intent, the app must return a response for this intent and an NSUserActivity capturing the state that the app must be restored to at the end of handling this intent
  
  @param  showBookingsIntent The input intent
  @param  completion The response handling block to invoke with the response to handling the intent.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRestaurantGuestIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRestaurantGuestIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRestaurantGuestIntent.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRestaurantGuestIntent.h	2016-10-22 02:34:38.000000000 +0200
@@ -29,7 +29,7 @@
  @brief handling method
  
  @abstract Execute the task represented by the INGetRestaurantGuestIntent that's passed in
- @discussion This method are called to actually execute the intent, the app must return a response for this intent and an NSUserActivity capturing the state that the app must be restored to at the end of handling this intent
+ @discussion This method is called to actually execute the intent, the app must return a response for this intent and an NSUserActivity capturing the state that the app must be restored to at the end of handling this intent
  
  @param  guestIntent The input intent
  @param  completion The response handling block to invoke with the response to handling the intent.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRideStatusIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRideStatusIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRideStatusIntent.h	2016-09-28 09:41:00.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetRideStatusIntent.h	2016-10-22 02:34:37.000000000 +0200
@@ -38,7 +38,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INGetRideStatusIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  getRideStatusIntent The input intent
  @param  completion The response handling block takes a INGetRideStatusIntentResponse containing the details of the result of having executed the intent
@@ -59,7 +59,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  getRideStatusIntent The input intent
  @param  completion The response block contains an INGetRideStatusIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -74,7 +74,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  getRideStatusIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetUserCurrentRestaurantReservationBookingsIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetUserCurrentRestaurantReservationBookingsIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetUserCurrentRestaurantReservationBookingsIntent.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INGetUserCurrentRestaurantReservationBookingsIntent.h	2016-10-22 02:34:38.000000000 +0200
@@ -37,7 +37,7 @@
  @brief handling method
  
  @abstract Execute the task represented by the INGetUserCurrentRestaurantReservationBookingsIntent that's passed in
- @discussion This method are called to actually execute the intent, the app must return a response for this intent and an NSUserActivity capturing the state that the app must be restored to at the end of handling this intent
+ @discussion This method is called to actually execute the intent, the app must return a response for this intent and an NSUserActivity capturing the state that the app must be restored to at the end of handling this intent
  
  @param  showCurrentBookingsIntent The input intent
  @param  completion The response handling block to invoke with the response to handling the intent.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntegerResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntegerResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntegerResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INIntegerResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -12,7 +12,8 @@
 API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx)
 @interface INIntegerResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given integer. The resolvedValue can be different than the original integer. This allows app extensions to apply business logic constraints. For example, the extension could constrain the value to some maximum.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedValue:(NSInteger)resolvedValue NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to confirm if this is the integer value with which the user wants to continue.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INListRideOptionsIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INListRideOptionsIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INListRideOptionsIntent.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INListRideOptionsIntent.h	2016-10-22 02:34:38.000000000 +0200
@@ -44,7 +44,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INListRideOptionsIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  listRideOptionsIntent The input intent
  @param  completion The response handling block takes a INListRideOptionsIntentResponse containing the details of the result of having executed the intent
@@ -60,7 +60,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  listRideOptionsIntent The input intent
  @param  completion The response block contains an INListRideOptionsIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -75,7 +75,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  listRideOptionsIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageAttributeOptionsResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageAttributeOptionsResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageAttributeOptionsResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageAttributeOptionsResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -13,7 +13,8 @@
 
 @interface INMessageAttributeOptionsResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INMessageAttributeOptions. The resolvedValue can be different than the original INMessageAttributeOptions. This allows app extensions to apply business logic constraints.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedValue:(INMessageAttributeOptions)resolvedValue NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to confirm if this is the value with which the user wants to continue.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageAttributeResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageAttributeResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageAttributeResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INMessageAttributeResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -13,7 +13,8 @@
 
 @interface INMessageAttributeResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INMessageAttribute. The resolvedValue can be different than the original INMessageAttribute. This allows app extensions to apply business logic constraints.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedValue:(INMessageAttribute)resolvedValue NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to confirm if this is the value with which the user wants to continue.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPauseWorkoutIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPauseWorkoutIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPauseWorkoutIntent.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPauseWorkoutIntent.h	2016-10-22 02:34:38.000000000 +0200
@@ -17,6 +17,7 @@
 API_UNAVAILABLE(macosx)
 @interface INPauseWorkoutIntent : INIntent
 
+// Designated initializer. The `workoutName` can use `INWorkoutNameIdentifier` as its `identifier` parameter.
 - (instancetype)initWithWorkoutName:(nullable INSpeakableString *)workoutName NS_DESIGNATED_INITIALIZER;
 
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INSpeakableString *workoutName;
@@ -41,7 +42,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INPauseWorkoutIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  pauseWorkoutIntent The input intent
  @param  completion The response handling block takes a INPauseWorkoutIntentResponse containing the details of the result of having executed the intent
@@ -57,7 +58,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  pauseWorkoutIntent The input intent
  @param  completion The response block contains an INPauseWorkoutIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -72,7 +73,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  pauseWorkoutIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h	2016-07-31 15:18:11.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson.h	2016-10-22 02:34:38.000000000 +0200
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
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h	2016-09-28 09:41:00.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandle.h	2016-10-22 02:34:37.000000000 +0200
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
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandleLabel.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandleLabel.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandleLabel.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonHandleLabel.h	2016-10-22 02:34:38.000000000 +0200
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
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonRelationship.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonRelationship.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonRelationship.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonRelationship.h	2016-10-22 02:34:37.000000000 +0200
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
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPersonResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -14,7 +14,8 @@
 API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INPersonResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given person. The resolvedPerson need not be identical to the input person. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INPerson. The resolvedPerson can be different than the original INPerson. This allows app extensions to add and correct attributes of the INPerson. For example, an extension may add a nickname from the app.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedPerson:(INPerson *)resolvedPerson NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to disambiguate between the provided people.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson_Deprecated.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson_Deprecated.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson_Deprecated.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPerson_Deprecated.h	2016-10-22 02:34:38.000000000 +0200
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
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INPlacemarkResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -14,7 +14,9 @@
 API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INPlacemarkResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given placemark. The resolvedPlacemark need not be identical to the input placemark. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given CLPlacemark. The resolvedPlacemark can be different than the original CLPlacemark. This allows app extensions to dynamically fill-in details about the CLPlacemark, as appropriate. To make a new CLPlacemark, see <Intents/CLPlacemark+IntentsAdditions.h>. 
+// Use +notRequired to continue with a 'nil' value.
+
 + (instancetype)successWithResolvedPlacemark:(CLPlacemark *)resolvedPlacemark NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to disambiguate between the provided placemarks.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRadioTypeResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRadioTypeResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRadioTypeResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRadioTypeResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -13,7 +13,8 @@
 
 @interface INRadioTypeResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INRadioType. The resolvedValue can be different than the original INRadioType. This allows app extensions to apply business logic constraints.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedValue:(INRadioType)resolvedValue NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to confirm if this is the value with which the user wants to continue.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRelativeReferenceResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRelativeReferenceResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRelativeReferenceResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRelativeReferenceResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -13,7 +13,8 @@
 
 @interface INRelativeReferenceResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INRelativeReference. The resolvedValue can be different than the original INRelativeReference. This allows app extensions to apply business logic constraints.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedValue:(INRelativeReference)resolvedValue NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to confirm if this is the value with which the user wants to continue.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRelativeSettingResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRelativeSettingResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRelativeSettingResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRelativeSettingResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -13,7 +13,8 @@
 
 @interface INRelativeSettingResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INRelativeSetting. The resolvedValue can be different than the original INRelativeSetting. This allows app extensions to apply business logic constraints.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedValue:(INRelativeSetting)resolvedValue NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to confirm if this is the value with which the user wants to continue.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestPaymentIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestPaymentIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestPaymentIntent.h	2016-09-28 09:40:42.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestPaymentIntent.h	2016-10-22 02:34:38.000000000 +0200
@@ -50,7 +50,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INRequestPaymentIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  requestPaymentIntent The input intent
  @param  completion The response handling block takes a INRequestPaymentIntentResponse containing the details of the result of having executed the intent
@@ -66,7 +66,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  requestPaymentIntent The input intent
  @param  completion The response block contains an INRequestPaymentIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -81,7 +81,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  requestPaymentIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestRideIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestRideIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestRideIntent.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRequestRideIntent.h	2016-10-22 02:51:11.000000000 +0200
@@ -60,7 +60,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INRequestRideIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  requestRideIntent The input intent
  @param  completion The response handling block takes a INRequestRideIntentResponse containing the details of the result of having executed the intent
@@ -76,7 +76,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  requestRideIntent The input intent
  @param  completion The response block contains an INRequestRideIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -91,7 +91,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  requestRideIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuestResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuestResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuestResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantGuestResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -17,13 +17,10 @@
 API_AVAILABLE(ios(10.0))
 @interface INRestaurantGuestResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given restaurant guest. The resolvedRestaurantGuest need not be identical to the input restaurant. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
 + (instancetype)successWithResolvedRestaurantGuest:(INRestaurantGuest *)resolvedRestaurantGuest NS_SWIFT_NAME(success(with:));
 
-// This resolution result is to ask Siri to disambiguate between the provided restaurant guests.
 + (instancetype)disambiguationWithRestaurantGuestsToDisambiguate:(NSArray<INRestaurantGuest *> *)restaurantGuestsToDisambiguate NS_SWIFT_NAME(disambiguation(with:));
 
-// This resolution result is to ask Siri to confirm if this is the restaurant guest with which the user wants to continue.
 + (instancetype)confirmationRequiredWithRestaurantGuestToConfirm:(nullable INRestaurantGuest *)restaurantGuestToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
 
 @end
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRestaurantResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -17,13 +17,10 @@
 API_AVAILABLE(ios(10.0))
 @interface INRestaurantResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given restaurant. The resolvedRestaurant need not be identical to the input restaurant. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
 + (instancetype)successWithResolvedRestaurant:(INRestaurant *)resolvedRestaurant NS_SWIFT_NAME(success(with:));
 
-// This resolution result is to ask Siri to disambiguate between the provided restaurants.
 + (instancetype)disambiguationWithRestaurantsToDisambiguate:(NSArray<INRestaurant *> *)restaurantsToDisambiguate NS_SWIFT_NAME(disambiguation(with:));
 
-// This resolution result is to ask Siri to confirm if this is the restaurant with which the user wants to continue.
 + (instancetype)confirmationRequiredWithRestaurantToConfirm:(nullable INRestaurant *)restaurantToConfirm NS_SWIFT_NAME(confirmationRequired(with:));
 
 @end
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INResumeWorkoutIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INResumeWorkoutIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INResumeWorkoutIntent.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INResumeWorkoutIntent.h	2016-10-22 02:34:38.000000000 +0200
@@ -17,6 +17,7 @@
 API_UNAVAILABLE(macosx)
 @interface INResumeWorkoutIntent : INIntent
 
+// Designated initializer. The `workoutName` can use `INWorkoutNameIdentifier` as its `identifier` parameter.
 - (instancetype)initWithWorkoutName:(nullable INSpeakableString *)workoutName NS_DESIGNATED_INITIALIZER;
 
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) INSpeakableString *workoutName;
@@ -41,7 +42,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INResumeWorkoutIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  resumeWorkoutIntent The input intent
  @param  completion The response handling block takes a INResumeWorkoutIntentResponse containing the details of the result of having executed the intent
@@ -57,7 +58,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  resumeWorkoutIntent The input intent
  @param  completion The response block contains an INResumeWorkoutIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -72,7 +73,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  resumeWorkoutIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideCompletionStatus.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideCompletionStatus.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideCompletionStatus.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideCompletionStatus.h	2016-10-22 02:34:38.000000000 +0200
@@ -11,7 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.1))
 @interface INRideCompletionStatus: NSObject <NSCopying, NSSecureCoding>
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideDriver.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideDriver.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideDriver.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideDriver.h	2016-10-22 02:34:38.000000000 +0200
@@ -14,29 +14,15 @@
 
 @interface INRideDriver : INPerson <NSCopying, NSSecureCoding>
 
-- (instancetype)initWithPersonHandle:(INPersonHandle *)personHandle
-                nameComponents:(nullable NSPersonNameComponents *)nameComponents
-                   displayName:(nullable NSString *)displayName
-                         image:(nullable INImage *)image
-                        rating:(nullable NSString *)rating
-                   phoneNumber:(nullable NSString *)phoneNumber NS_DESIGNATED_INITIALIZER;
-
-- (instancetype)initWithHandle:(NSString *)handle
-                   displayName:(nullable NSString *)displayName
-                         image:(nullable INImage *)image
-                        rating:(nullable NSString *)rating
-                   phoneNumber:(nullable NSString *)phoneNumber NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use the designated initializer instead");
-
-- (instancetype)initWithHandle:(NSString *)handle
-                nameComponents:(NSPersonNameComponents *)nameComponents
-                         image:(nullable INImage *)image
-                        rating:(nullable NSString *)rating
-                   phoneNumber:(nullable NSString *)phoneNumber NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use the designated initializer instead");
-
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *rating;
-
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *phoneNumber;
 
-@end
+- (instancetype)initWithPhoneNumber:(NSString *)phoneNumber
+                     nameComponents:(nullable NSPersonNameComponents *)nameComponents
+                        displayName:(nullable NSString *)displayName
+                              image:(nullable INImage *)image
+                             rating:(nullable NSString *)rating NS_DESIGNATED_INITIALIZER;
 
+@end
+ 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideDriver_Deprecated.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideDriver_Deprecated.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideDriver_Deprecated.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INRideDriver_Deprecated.h	2016-10-22 02:34:38.000000000 +0200
@@ -0,0 +1,35 @@
+//
+//  INRideDriver_Deprecated.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Intents/INRideDriver.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@interface INRideDriver (Deprecated)
+
+- (instancetype)initWithPersonHandle:(INPersonHandle *)personHandle
+                      nameComponents:(nullable NSPersonNameComponents *)nameComponents
+                         displayName:(nullable NSString *)displayName
+                               image:(nullable INImage *)image
+                              rating:(nullable NSString *)rating
+                         phoneNumber:(nullable NSString *)phoneNumber API_DEPRECATED("Use the designated initializer instead", ios(10.0, 10.2));
+
+- (instancetype)initWithHandle:(NSString *)handle
+                   displayName:(nullable NSString *)displayName
+                         image:(nullable INImage *)image
+                        rating:(nullable NSString *)rating
+                   phoneNumber:(nullable NSString *)phoneNumber API_DEPRECATED("Use the designated initializer instead", ios(10.0, 10.0));
+
+- (instancetype)initWithHandle:(NSString *)handle
+                nameComponents:(NSPersonNameComponents *)nameComponents
+                         image:(nullable INImage *)image
+                        rating:(nullable NSString *)rating
+                   phoneNumber:(nullable NSString *)phoneNumber API_DEPRECATED("Use the designated initializer instead", ios(10.0, 10.0));
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntent.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntent.h	2016-10-22 02:34:38.000000000 +0200
@@ -9,19 +9,20 @@
 #import <Intents/INIntentResolutionResult.h>
 
 @class INIntegerResolutionResult;
+@class INStringResolutionResult;
 
 NS_ASSUME_NONNULL_BEGIN
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @interface INSaveProfileInCarIntent : INIntent
 
 - (instancetype)initWithProfileNumber:(nullable NSNumber *)profileNumber
-                         profileLabel:(nullable NSString *)profileLabel NS_DESIGNATED_INITIALIZER NS_REFINED_FOR_SWIFT;
+                          profileName:(nullable NSString *)profileName NS_DESIGNATED_INITIALIZER NS_REFINED_FOR_SWIFT;
 
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *profileNumber NS_REFINED_FOR_SWIFT;
 
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *profileLabel;
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *profileName;
 
 @end
 
@@ -34,7 +35,7 @@
  */
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @protocol INSaveProfileInCarIntentHandling <NSObject>
 
 @required
@@ -43,7 +44,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INSaveProfileInCarIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  saveProfileInCarIntent The input intent
  @param  completion The response handling block takes a INSaveProfileInCarIntentResponse containing the details of the result of having executed the intent
@@ -59,7 +60,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  saveProfileInCarIntent The input intent
  @param  completion The response block contains an INSaveProfileInCarIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -74,7 +75,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  saveProfileInCarIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
@@ -86,6 +87,9 @@
 - (void)resolveProfileNumberForSaveProfileInCar:(INSaveProfileInCarIntent *)intent
                                  withCompletion:(void (^)(INIntegerResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveProfileNumber(forSaveProfileInCar:with:));
 
+- (void)resolveProfileNameForSaveProfileInCar:(INSaveProfileInCarIntent *)intent
+                               withCompletion:(void (^)(INStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveProfileName(forSaveProfileInCar:with:));
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntentResponse.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntentResponse.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntentResponse.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntentResponse.h	2016-10-22 02:34:38.000000000 +0200
@@ -14,12 +14,12 @@
     INSaveProfileInCarIntentResponseCodeSuccess,
     INSaveProfileInCarIntentResponseCodeFailure,
     INSaveProfileInCarIntentResponseCodeFailureRequiringAppLaunch,
-} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(watchos, macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @interface INSaveProfileInCarIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntent_Deprecated.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntent_Deprecated.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntent_Deprecated.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSaveProfileInCarIntent_Deprecated.h	2016-10-22 02:34:38.000000000 +0200
@@ -0,0 +1,26 @@
+//
+//  INSaveProfileInCarIntent+INSaveProfileInCarIntent_Deprecated.h
+//  Intents
+//
+//  Created by Yifeng Gui on 8/30/16.
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#if (defined(TARGET_OS_WATCH) && !TARGET_OS_WATCH)
+
+#import <Intents/INSaveProfileInCarIntent.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@interface INSaveProfileInCarIntent (Deprecated)
+
+- (instancetype)initWithProfileNumber:(nullable NSNumber *)profileNumber
+                         profileLabel:(nullable NSString *)profileLabel API_DEPRECATED("Use `-initWithProfileNumber:profileName:` method instead.", ios(10.0, 10.2)) API_UNAVAILABLE(watchos) NS_REFINED_FOR_SWIFT;
+
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *profileLabel API_DEPRECATED("Use `profileName` property instead.", ios(10.0, 10.2)) API_UNAVAILABLE(watchos);
+
+@end
+
+NS_ASSUME_NONNULL_END
+
+#endif
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h	2016-09-28 09:41:00.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntent.h	2016-10-22 02:34:37.000000000 +0200
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
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchCallHistoryIntentResponse.h	2016-10-22 02:34:38.000000000 +0200
@@ -13,6 +13,7 @@
     INSearchCallHistoryIntentResponseCodeContinueInApp,
     INSearchCallHistoryIntentResponseCodeFailure,
     INSearchCallHistoryIntentResponseCodeFailureRequiringAppLaunch,
+    INSearchCallHistoryIntentResponseCodeFailureAppConfigurationRequired,
 } API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h	2016-10-22 02:51:11.000000000 +0200
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
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntent.h	2016-09-28 09:40:42.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntent.h	2016-10-22 02:51:11.000000000 +0200
@@ -80,7 +80,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INSearchForPhotosIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  searchForPhotosIntent The input intent
  @param  completion The response handling block takes a INSearchForPhotosIntentResponse containing the details of the result of having executed the intent
@@ -96,7 +96,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  searchForPhotosIntent The input intent
  @param  completion The response block contains an INSearchForPhotosIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -111,7 +111,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  searchForPhotosIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntentResponse.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntentResponse.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntentResponse.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForPhotosIntentResponse.h	2016-10-22 02:34:38.000000000 +0200
@@ -13,6 +13,7 @@
     INSearchForPhotosIntentResponseCodeContinueInApp,
     INSearchForPhotosIntentResponseCodeFailure,
     INSearchForPhotosIntentResponseCodeFailureRequiringAppLaunch,
+    INSearchForPhotosIntentResponseCodeFailureAppConfigurationRequired,
 } API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h	2016-09-28 09:40:42.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendMessageIntent.h	2016-10-22 02:34:38.000000000 +0200
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
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendPaymentIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendPaymentIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendPaymentIntent.h	2016-09-28 09:40:42.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSendPaymentIntent.h	2016-10-22 02:51:11.000000000 +0200
@@ -50,7 +50,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INSendPaymentIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  sendPaymentIntent The input intent
  @param  completion The response handling block takes a INSendPaymentIntentResponse containing the details of the result of having executed the intent
@@ -66,7 +66,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  sendPaymentIntent The input intent
  @param  completion The response block contains an INSendPaymentIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -81,7 +81,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  sendPaymentIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetAudioSourceInCarIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetAudioSourceInCarIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetAudioSourceInCarIntent.h	2016-09-28 09:40:42.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetAudioSourceInCarIntent.h	2016-10-22 02:34:38.000000000 +0200
@@ -17,7 +17,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @interface INSetAudioSourceInCarIntent : INIntent
 
 - (instancetype)initWithAudioSource:(INCarAudioSource)audioSource
@@ -38,7 +38,7 @@
  */
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @protocol INSetAudioSourceInCarIntentHandling <NSObject>
 
 @required
@@ -47,7 +47,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INSetAudioSourceInCarIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  setAudioSourceInCarIntent The input intent
  @param  completion The response handling block takes a INSetAudioSourceInCarIntentResponse containing the details of the result of having executed the intent
@@ -63,7 +63,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  setAudioSourceInCarIntent The input intent
  @param  completion The response block contains an INSetAudioSourceInCarIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -78,7 +78,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  setAudioSourceInCarIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetAudioSourceInCarIntentResponse.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetAudioSourceInCarIntentResponse.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetAudioSourceInCarIntentResponse.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetAudioSourceInCarIntentResponse.h	2016-10-22 02:34:38.000000000 +0200
@@ -14,12 +14,12 @@
     INSetAudioSourceInCarIntentResponseCodeSuccess,
     INSetAudioSourceInCarIntentResponseCodeFailure,
     INSetAudioSourceInCarIntentResponseCodeFailureRequiringAppLaunch,
-} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(watchos, macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @interface INSetAudioSourceInCarIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntent.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntent.h	2016-10-22 02:51:11.000000000 +0200
@@ -23,7 +23,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @interface INSetClimateSettingsInCarIntent : INIntent
 
 - (instancetype)initWithEnableFan:(nullable NSNumber *)enableFan
@@ -71,7 +71,7 @@
  */
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @protocol INSetClimateSettingsInCarIntentHandling <NSObject>
 
 @required
@@ -80,7 +80,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INSetClimateSettingsInCarIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  setClimateSettingsInCarIntent The input intent
  @param  completion The response handling block takes a INSetClimateSettingsInCarIntentResponse containing the details of the result of having executed the intent
@@ -96,7 +96,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  setClimateSettingsInCarIntent The input intent
  @param  completion The response block contains an INSetClimateSettingsInCarIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -111,7 +111,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  setClimateSettingsInCarIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntentResponse.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntentResponse.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntentResponse.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetClimateSettingsInCarIntentResponse.h	2016-10-22 02:34:38.000000000 +0200
@@ -14,12 +14,12 @@
     INSetClimateSettingsInCarIntentResponseCodeSuccess,
     INSetClimateSettingsInCarIntentResponseCodeFailure,
     INSetClimateSettingsInCarIntentResponseCodeFailureRequiringAppLaunch,
-} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(watchos, macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @interface INSetClimateSettingsInCarIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetDefrosterSettingsInCarIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetDefrosterSettingsInCarIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetDefrosterSettingsInCarIntent.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetDefrosterSettingsInCarIntent.h	2016-10-22 02:51:10.000000000 +0200
@@ -16,7 +16,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @interface INSetDefrosterSettingsInCarIntent : INIntent
 
 - (instancetype)initWithEnable:(nullable NSNumber *)enable
@@ -37,7 +37,7 @@
  */
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @protocol INSetDefrosterSettingsInCarIntentHandling <NSObject>
 
 @required
@@ -46,7 +46,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INSetDefrosterSettingsInCarIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  setDefrosterSettingsInCarIntent The input intent
  @param  completion The response handling block takes a INSetDefrosterSettingsInCarIntentResponse containing the details of the result of having executed the intent
@@ -62,7 +62,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  setDefrosterSettingsInCarIntent The input intent
  @param  completion The response block contains an INSetDefrosterSettingsInCarIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -77,7 +77,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  setDefrosterSettingsInCarIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetDefrosterSettingsInCarIntentResponse.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetDefrosterSettingsInCarIntentResponse.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetDefrosterSettingsInCarIntentResponse.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetDefrosterSettingsInCarIntentResponse.h	2016-10-22 02:34:38.000000000 +0200
@@ -14,12 +14,12 @@
     INSetDefrosterSettingsInCarIntentResponseCodeSuccess,
     INSetDefrosterSettingsInCarIntentResponseCodeFailure,
     INSetDefrosterSettingsInCarIntentResponseCodeFailureRequiringAppLaunch,
-} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(watchos, macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @interface INSetDefrosterSettingsInCarIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetMessageAttributeIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetMessageAttributeIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetMessageAttributeIntent.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetMessageAttributeIntent.h	2016-10-22 02:34:38.000000000 +0200
@@ -44,7 +44,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INSetMessageAttributeIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  setMessageAttributeIntent The input intent
  @param  completion The response handling block takes a INSetMessageAttributeIntentResponse containing the details of the result of having executed the intent
@@ -60,7 +60,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  setMessageAttributeIntent The input intent
  @param  completion The response block contains an INSetMessageAttributeIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -75,7 +75,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  setMessageAttributeIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntent.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntent.h	2016-10-22 02:34:38.000000000 +0200
@@ -9,21 +9,22 @@
 #import <Intents/INIntentResolutionResult.h>
 
 @class INIntegerResolutionResult;
+@class INStringResolutionResult;
 @class INBooleanResolutionResult;
 
 NS_ASSUME_NONNULL_BEGIN
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @interface INSetProfileInCarIntent : INIntent
 
 - (instancetype)initWithProfileNumber:(nullable NSNumber *)profileNumber
-                         profileLabel:(nullable NSString *)profileLabel
+                          profileName:(nullable NSString *)profileName
                        defaultProfile:(nullable NSNumber *)defaultProfile NS_DESIGNATED_INITIALIZER NS_REFINED_FOR_SWIFT;
 
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *profileNumber NS_REFINED_FOR_SWIFT;
 
-@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *profileLabel;
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *profileName;
 
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSNumber *defaultProfile NS_REFINED_FOR_SWIFT;
 
@@ -38,7 +39,7 @@
  */
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @protocol INSetProfileInCarIntentHandling <NSObject>
 
 @required
@@ -47,7 +48,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INSetProfileInCarIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  setProfileInCarIntent The input intent
  @param  completion The response handling block takes a INSetProfileInCarIntentResponse containing the details of the result of having executed the intent
@@ -63,7 +64,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  setProfileInCarIntent The input intent
  @param  completion The response block contains an INSetProfileInCarIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -78,7 +79,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  setProfileInCarIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
@@ -90,6 +91,9 @@
 - (void)resolveProfileNumberForSetProfileInCar:(INSetProfileInCarIntent *)intent
                                 withCompletion:(void (^)(INIntegerResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveProfileNumber(forSetProfileInCar:with:));
 
+- (void)resolveProfileNameForSetProfileInCar:(INSetProfileInCarIntent *)intent
+                              withCompletion:(void (^)(INStringResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveProfileName(forSetProfileInCar:with:));
+
 - (void)resolveDefaultProfileForSetProfileInCar:(INSetProfileInCarIntent *)intent
                                  withCompletion:(void (^)(INBooleanResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveDefaultProfile(forSetProfileInCar:with:));
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntentResponse.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntentResponse.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntentResponse.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntentResponse.h	2016-10-22 02:34:38.000000000 +0200
@@ -14,12 +14,12 @@
     INSetProfileInCarIntentResponseCodeSuccess,
     INSetProfileInCarIntentResponseCodeFailure,
     INSetProfileInCarIntentResponseCodeFailureRequiringAppLaunch,
-} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(watchos, macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @interface INSetProfileInCarIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntent_Deprecated.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntent_Deprecated.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntent_Deprecated.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetProfileInCarIntent_Deprecated.h	2016-10-22 02:34:38.000000000 +0200
@@ -0,0 +1,26 @@
+//
+//  INSetProfileInCarIntent_Deprecated.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#if (defined(TARGET_OS_WATCH) && !TARGET_OS_WATCH)
+
+#import <Intents/INSetProfileInCarIntent.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@interface INSetProfileInCarIntent (Deprecated)
+
+- (instancetype)initWithProfileNumber:(nullable NSNumber *)profileNumber
+                         profileLabel:(nullable NSString *)profileLabel
+                       defaultProfile:(nullable NSNumber *)defaultProfile API_DEPRECATED("Use `-initWithProfileNumber:profileName:defaultProfile:` method instead.", ios(10.0, 10.2)) API_UNAVAILABLE(watchos) NS_REFINED_FOR_SWIFT;
+
+@property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSString *profileLabel API_DEPRECATED("Use `profileName` property instead.", ios(10.0, 10.2)) API_UNAVAILABLE(watchos);
+
+@end
+
+NS_ASSUME_NONNULL_END
+
+#endif
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetRadioStationIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetRadioStationIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetRadioStationIntent.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetRadioStationIntent.h	2016-10-22 02:51:11.000000000 +0200
@@ -18,7 +18,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @interface INSetRadioStationIntent : INIntent
 
 - (instancetype)initWithRadioType:(INRadioType)radioType
@@ -48,7 +48,7 @@
  */
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @protocol INSetRadioStationIntentHandling <NSObject>
 
 @required
@@ -57,7 +57,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INSetRadioStationIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  setRadioStationIntent The input intent
  @param  completion The response handling block takes a INSetRadioStationIntentResponse containing the details of the result of having executed the intent
@@ -73,7 +73,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  setRadioStationIntent The input intent
  @param  completion The response block contains an INSetRadioStationIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -88,7 +88,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  setRadioStationIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetRadioStationIntentResponse.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetRadioStationIntentResponse.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetRadioStationIntentResponse.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetRadioStationIntentResponse.h	2016-10-22 02:34:38.000000000 +0200
@@ -15,12 +15,12 @@
     INSetRadioStationIntentResponseCodeFailure,
     INSetRadioStationIntentResponseCodeFailureRequiringAppLaunch,
     INSetRadioStationIntentResponseCodeFailureNotSubscribed,
-} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(watchos, macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @interface INSetRadioStationIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatSettingsInCarIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatSettingsInCarIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatSettingsInCarIntent.h	2016-09-28 09:40:42.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatSettingsInCarIntent.h	2016-10-22 02:51:11.000000000 +0200
@@ -19,7 +19,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @interface INSetSeatSettingsInCarIntent : INIntent
 
 - (instancetype)initWithEnableHeating:(nullable NSNumber *)enableHeating
@@ -52,7 +52,7 @@
  */
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @protocol INSetSeatSettingsInCarIntentHandling <NSObject>
 
 @required
@@ -61,7 +61,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INSetSeatSettingsInCarIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  setSeatSettingsInCarIntent The input intent
  @param  completion The response handling block takes a INSetSeatSettingsInCarIntentResponse containing the details of the result of having executed the intent
@@ -77,7 +77,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  setSeatSettingsInCarIntent The input intent
  @param  completion The response block contains an INSetSeatSettingsInCarIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -92,7 +92,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  setSeatSettingsInCarIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatSettingsInCarIntentResponse.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatSettingsInCarIntentResponse.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatSettingsInCarIntentResponse.h	2016-09-28 09:41:00.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetSeatSettingsInCarIntentResponse.h	2016-10-22 02:34:37.000000000 +0200
@@ -14,12 +14,12 @@
     INSetSeatSettingsInCarIntentResponseCodeSuccess,
     INSetSeatSettingsInCarIntentResponseCodeFailure,
     INSetSeatSettingsInCarIntentResponseCodeFailureRequiringAppLaunch,
-} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(watchos, macosx);
 
 NS_ASSUME_NONNULL_BEGIN
 
 API_AVAILABLE(ios(10.0))
-API_UNAVAILABLE(macosx)
+API_UNAVAILABLE(watchos, macosx)
 @interface INSetSeatSettingsInCarIntentResponse : INIntentResponse
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableString.h	2016-10-22 02:34:38.000000000 +0200
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
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSpeakableStringResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -14,7 +14,8 @@
 API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INSpeakableStringResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given string. The resolvedString need not be identical to the input string. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INSpeakableString. The resolvedString can be different than the original INSpeakableString. This allows app extensions to add a pronunciationHint, or otherwise tweak the string.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedString:(INSpeakableString *)resolvedString NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to disambiguate between the provided strings.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntent.h	2016-09-28 09:41:00.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntent.h	2016-10-22 02:34:37.000000000 +0200
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
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartAudioCallIntentResponse.h	2016-10-22 02:34:38.000000000 +0200
@@ -13,6 +13,8 @@
     INStartAudioCallIntentResponseCodeContinueInApp,
     INStartAudioCallIntentResponseCodeFailure,
     INStartAudioCallIntentResponseCodeFailureRequiringAppLaunch,
+    INStartAudioCallIntentResponseCodeFailureAppConfigurationRequired,
+    INStartAudioCallIntentResponseCodeFailureCallingServiceNotAvailable,
 } API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntent.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntent.h	2016-10-22 02:51:11.000000000 +0200
@@ -80,7 +80,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INStartPhotoPlaybackIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  startPhotoPlaybackIntent The input intent
  @param  completion The response handling block takes a INStartPhotoPlaybackIntentResponse containing the details of the result of having executed the intent
@@ -96,7 +96,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  startPhotoPlaybackIntent The input intent
  @param  completion The response block contains an INStartPhotoPlaybackIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -111,7 +111,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  startPhotoPlaybackIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntentResponse.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntentResponse.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntentResponse.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartPhotoPlaybackIntentResponse.h	2016-10-22 02:34:38.000000000 +0200
@@ -13,6 +13,7 @@
     INStartPhotoPlaybackIntentResponseCodeContinueInApp,
     INStartPhotoPlaybackIntentResponseCodeFailure,
     INStartPhotoPlaybackIntentResponseCodeFailureRequiringAppLaunch,
+    INStartPhotoPlaybackIntentResponseCodeFailureAppConfigurationRequired,
 } API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 NS_ASSUME_NONNULL_BEGIN
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntent.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntent.h	2016-10-22 02:34:38.000000000 +0200
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
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartVideoCallIntentResponse.h	2016-10-22 02:34:38.000000000 +0200
@@ -13,6 +13,8 @@
     INStartVideoCallIntentResponseCodeContinueInApp,
     INStartVideoCallIntentResponseCodeFailure,
     INStartVideoCallIntentResponseCodeFailureRequiringAppLaunch,
+    INStartVideoCallIntentResponseCodeFailureAppConfigurationRequired,
+    INStartVideoCallIntentResponseCodeFailureCallingServiceNotAvailable,
 } API_AVAILABLE(macosx(10.12), ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartWorkoutIntent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartWorkoutIntent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartWorkoutIntent.h	2016-09-28 09:40:42.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStartWorkoutIntent.h	2016-10-22 02:51:11.000000000 +0200
@@ -24,6 +24,7 @@
 API_UNAVAILABLE(macosx)
 @interface INStartWorkoutIntent : INIntent
 
+// Designated initializer. The `workoutName` can use `INWorkoutNameIdentifier` as its `identifier` parameter.
 - (instancetype)initWithWorkoutName:(nullable INSpeakableString *)workoutName
                           goalValue:(nullable NSNumber *)goalValue
                 workoutGoalUnitType:(INWorkoutGoalUnitType)workoutGoalUnitType
@@ -60,7 +61,7 @@
  @brief handling method
 
  @abstract Execute the task represented by the INStartWorkoutIntent that's passed in
- @discussion This method is called to actually execute the intent. The app must return a response for this intent.
+ @discussion Called to actually execute the intent. The app must return a response for this intent.
 
  @param  startWorkoutIntent The input intent
  @param  completion The response handling block takes a INStartWorkoutIntentResponse containing the details of the result of having executed the intent
@@ -76,7 +77,7 @@
 /*!
  @brief Confirmation method
  @abstract Validate that this intent is ready for the next step (i.e. handling)
- @discussion These methods are called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
+ @discussion Called prior to asking the app to handle the intent. The app should return a response object that contains additional information about the intent, which may be relevant for the system to show the user prior to handling. If unimplemented, the system will assume the intent is valid following resolution, and will assume there is no additional information relevant to this intent.
 
  @param  startWorkoutIntent The input intent
  @param  completion The response block contains an INStartWorkoutIntentResponse containing additional details about the intent that may be relevant for the system to show the user prior to handling.
@@ -91,7 +92,7 @@
 /*!
  @brief Resolution methods
  @abstract Determine if this intent is ready for the next step (confirmation)
- @discussion These methods are called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
+ @discussion Called to make sure the app extension is capable of handling this intent in its current form. This method is for validating if the intent needs any further fleshing out.
 
  @param  startWorkoutIntent The input intent
  @param  completion The response block contains an INIntentResolutionResult for the parameter being resolved
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INStringResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -12,7 +12,8 @@
 API_AVAILABLE(macosx(10.12), ios(10.0))
 @interface INStringResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given string. The resolvedString need not be identical to the input string. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given string. The resolvedString can be different than the original string. This allows app extensions to apply business logic constraints to the string.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedString:(NSString *)resolvedString NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to disambiguate between the provided strings.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INTemperatureResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -14,7 +14,8 @@
 API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx)
 @interface INTemperatureResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given temperature. The resolvedTemperature need not be identical to the input temperature. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given temperature. The resolvedTemperature can be different than the original temperature. This allows app extensions to apply business logic constraints to the temperature. For example, constraining it to a maximum or minimum value.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedTemperature:(NSMeasurement<NSUnitTemperature *> *)resolvedTemperature NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to disambiguate between the provided temperatures.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INWorkoutGoalUnitTypeResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INWorkoutGoalUnitTypeResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INWorkoutGoalUnitTypeResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INWorkoutGoalUnitTypeResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -13,7 +13,8 @@
 
 @interface INWorkoutGoalUnitTypeResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INWorkoutGoalUnitType. The resolvedValue can be different than the original INWorkoutGoalUnitType. This allows app extensions to apply business logic constraints.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedValue:(INWorkoutGoalUnitType)resolvedValue NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to confirm if this is the value with which the user wants to continue.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INWorkoutLocationTypeResolutionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INWorkoutLocationTypeResolutionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INWorkoutLocationTypeResolutionResult.h	2016-09-28 09:41:01.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INWorkoutLocationTypeResolutionResult.h	2016-10-22 02:34:38.000000000 +0200
@@ -13,7 +13,8 @@
 
 @interface INWorkoutLocationTypeResolutionResult : INIntentResolutionResult
 
-// This resolution result is for when the app extension wants to tell Siri to proceed with a given value. The resolvedValue need not be identical to the input value. If the app extension wants to continue with a 'nil' value, it must use +notRequired.
+// This resolution result is for when the app extension wants to tell Siri to proceed, with a given INWorkoutLocationType. The resolvedValue can be different than the original INWorkoutLocationType. This allows app extensions to apply business logic constraints.
+// Use +notRequired to continue with a 'nil' value.
 + (instancetype)successWithResolvedValue:(INWorkoutLocationType)resolvedValue NS_SWIFT_NAME(success(with:));
 
 // This resolution result is to ask Siri to confirm if this is the value with which the user wants to continue.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INWorkoutNameIdentifier.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INWorkoutNameIdentifier.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INWorkoutNameIdentifier.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INWorkoutNameIdentifier.h	2016-10-22 02:34:38.000000000 +0200
@@ -0,0 +1,31 @@
+//
+//  INWorkoutNameIdentifier.h
+//  Intents
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+#import <Intents/IntentsDefines.h>
+
+typedef NSString *INWorkoutNameIdentifier NS_STRING_ENUM;
+
+INTENTS_EXTERN INWorkoutNameIdentifier const INWorkoutNameIdentifierRun NS_SWIFT_NAME(INWorkoutNameIdentifier.run);
+INTENTS_EXTERN INWorkoutNameIdentifier const INWorkoutNameIdentifierSit NS_SWIFT_NAME(INWorkoutNameIdentifier.sit);
+INTENTS_EXTERN INWorkoutNameIdentifier const INWorkoutNameIdentifierSteps NS_SWIFT_NAME(INWorkoutNameIdentifier.steps);
+INTENTS_EXTERN INWorkoutNameIdentifier const INWorkoutNameIdentifierStand NS_SWIFT_NAME(INWorkoutNameIdentifier.stand);
+INTENTS_EXTERN INWorkoutNameIdentifier const INWorkoutNameIdentifierMove NS_SWIFT_NAME(INWorkoutNameIdentifier.move);
+INTENTS_EXTERN INWorkoutNameIdentifier const INWorkoutNameIdentifierWalk NS_SWIFT_NAME(INWorkoutNameIdentifier.walk);
+INTENTS_EXTERN INWorkoutNameIdentifier const INWorkoutNameIdentifierYoga NS_SWIFT_NAME(INWorkoutNameIdentifier.yoga);
+INTENTS_EXTERN INWorkoutNameIdentifier const INWorkoutNameIdentifierDance NS_SWIFT_NAME(INWorkoutNameIdentifier.dance);
+INTENTS_EXTERN INWorkoutNameIdentifier const INWorkoutNameIdentifierCrosstraining NS_SWIFT_NAME(INWorkoutNameIdentifier.crosstraining);
+INTENTS_EXTERN INWorkoutNameIdentifier const INWorkoutNameIdentifierElliptical NS_SWIFT_NAME(INWorkoutNameIdentifier.elliptical);
+INTENTS_EXTERN INWorkoutNameIdentifier const INWorkoutNameIdentifierRower NS_SWIFT_NAME(INWorkoutNameIdentifier.rower);
+INTENTS_EXTERN INWorkoutNameIdentifier const INWorkoutNameIdentifierCycle NS_SWIFT_NAME(INWorkoutNameIdentifier.cycle);
+INTENTS_EXTERN INWorkoutNameIdentifier const INWorkoutNameIdentifierStairs NS_SWIFT_NAME(INWorkoutNameIdentifier.stairs);
+INTENTS_EXTERN INWorkoutNameIdentifier const INWorkoutNameIdentifierOther NS_SWIFT_NAME(INWorkoutNameIdentifier.other);
+INTENTS_EXTERN INWorkoutNameIdentifier const INWorkoutNameIdentifierIndoorrun NS_SWIFT_NAME(INWorkoutNameIdentifier.indoorrun);
+INTENTS_EXTERN INWorkoutNameIdentifier const INWorkoutNameIdentifierIndoorcycle NS_SWIFT_NAME(INWorkoutNameIdentifier.indoorcycle);
+INTENTS_EXTERN INWorkoutNameIdentifier const INWorkoutNameIdentifierIndoorwalk NS_SWIFT_NAME(INWorkoutNameIdentifier.indoorwalk);
+INTENTS_EXTERN INWorkoutNameIdentifier const INWorkoutNameIdentifierExercise NS_SWIFT_NAME(INWorkoutNameIdentifier.exercise);
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h	2016-09-28 09:40:42.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/Intents.h	2016-10-22 02:51:11.000000000 +0200
@@ -44,6 +44,8 @@
 #import <Intents/INPaymentMethodType.h>
 #import <Intents/INPerson.h>
 #import <Intents/INSpeakableString.h>
+#import <Intents/INPersonHandleLabel.h>
+#import <Intents/INPersonRelationship.h>
 
 // Common Resolution Results
 #import <Intents/INBooleanResolutionResult.h>
@@ -168,6 +170,7 @@
 #import <Intents/INWorkoutGoalUnitTypeResolutionResult.h>
 #import <Intents/INWorkoutLocationType.h>
 #import <Intents/INWorkoutLocationTypeResolutionResult.h>
+#import <Intents/INWorkoutNameIdentifier.h>
 
 // Restaurant Booking
 #import <Intents/INIntentRestaurantReservation.h>
@@ -181,3 +184,9 @@
 #import <Intents/CLPlacemark+IntentsAdditions.h>
 #import <Intents/NSUserActivity+IntentsAdditions.h>
 #import <Intents/INPerson+SiriAdditions.h>
+
+// Deprecated
+#import <Intents/INPerson_Deprecated.h>
+#import <Intents/INRideDriver_Deprecated.h>
+#import <Intents/INSaveProfileInCarIntent_Deprecated.h>
+#import <Intents/INSetProfileInCarIntent_Deprecated.h>

```