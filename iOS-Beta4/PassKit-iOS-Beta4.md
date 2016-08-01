#PassKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKConstants.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKConstants.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKConstants.h	2016-07-11 07:57:39.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKConstants.h	2016-07-28 05:29:39.000000000 +0200
@@ -28,9 +28,9 @@
     PKPaymentAuthorizationStatusSuccess, // Merchant auth'd (or expects to auth) the transaction successfully.
     PKPaymentAuthorizationStatusFailure, // Merchant failed to auth the transaction.
 
-    PKPaymentAuthorizationStatusInvalidBillingPostalAddress,  // Merchant refuses service to this billing address.
-    PKPaymentAuthorizationStatusInvalidShippingPostalAddress, // Merchant refuses service to this shipping address.
-    PKPaymentAuthorizationStatusInvalidShippingContact,       // Supplied contact information is insufficient.
+    PKPaymentAuthorizationStatusInvalidBillingPostalAddress,  // Supplied billing address is insufficient or otherwise invalid
+    PKPaymentAuthorizationStatusInvalidShippingPostalAddress, // Supplied postal address is insufficient or otherwise invalid
+    PKPaymentAuthorizationStatusInvalidShippingContact,       // Supplied contact information is insufficient or otherwise invalid
 
     PKPaymentAuthorizationStatusPINRequired NS_ENUM_AVAILABLE_IOS(9_2),  // Transaction requires PIN entry.
     PKPaymentAuthorizationStatusPINIncorrect NS_ENUM_AVAILABLE_IOS(9_2), // PIN was not entered correctly, retry.
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentMethod.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentMethod.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentMethod.h	2016-07-11 07:57:39.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentMethod.h	2016-07-28 05:29:39.000000000 +0200
@@ -25,9 +25,11 @@
 } NS_ENUM_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(3.0);
 
 // A string describing the instrument that's suitable for display
+// This property will be nil prior to the user authorizing the payment
 @property (nonatomic, copy, readonly, nullable) NSString *displayName;
 
 // The payment network that backs the instrument. Suitable for display.
+// This property will be nil prior to the user authorizing the payment
 @property (nonatomic, copy, readonly, nullable) PKPaymentNetwork network;
 
 // The underlying instrument type (Credit, Debit, etc)

```