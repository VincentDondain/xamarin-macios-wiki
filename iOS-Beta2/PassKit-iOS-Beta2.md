#PassKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKConstants.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKConstants.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKConstants.h	2016-06-05 05:30:27.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKConstants.h	2016-06-29 07:17:01.000000000 +0200
@@ -10,16 +10,19 @@
 #ifndef PKCONSTANTS_H
 #define PKCONSTANTS_H
 
-extern NSString * const PKEncryptionSchemeECC_V2 NS_AVAILABLE_IOS(9_0);
-extern NSString * const PKEncryptionSchemeRSA_V2 NS_AVAILABLE_IOS(10_0);
 
-extern NSString * const PKPaymentNetworkAmex NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(3.0);
-extern NSString * const PKPaymentNetworkChinaUnionPay NS_AVAILABLE_IOS(9_2) __WATCHOS_AVAILABLE(3.0);
-extern NSString * const PKPaymentNetworkDiscover NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(3.0);
-extern NSString * const PKPaymentNetworkInterac NS_AVAILABLE_IOS(9_2) __WATCHOS_AVAILABLE(3.0);
-extern NSString * const PKPaymentNetworkMasterCard NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(3.0);
-extern NSString * const PKPaymentNetworkPrivateLabel NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(3.0);
-extern NSString * const PKPaymentNetworkVisa NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(3.0);
+typedef NSString * PKEncryptionScheme NS_STRING_ENUM;
+extern PKEncryptionScheme const PKEncryptionSchemeECC_V2 NS_AVAILABLE_IOS(9_0);
+extern PKEncryptionScheme const PKEncryptionSchemeRSA_V2 NS_AVAILABLE_IOS(10_0);
+
+typedef NSString * PKPaymentNetwork NS_EXTENSIBLE_STRING_ENUM;
+extern PKPaymentNetwork const PKPaymentNetworkAmex NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(3.0);
+extern PKPaymentNetwork const PKPaymentNetworkChinaUnionPay NS_AVAILABLE_IOS(9_2) __WATCHOS_AVAILABLE(3.0);
+extern PKPaymentNetwork const PKPaymentNetworkDiscover NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(3.0);
+extern PKPaymentNetwork const PKPaymentNetworkInterac NS_AVAILABLE_IOS(9_2) __WATCHOS_AVAILABLE(3.0);
+extern PKPaymentNetwork const PKPaymentNetworkMasterCard NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(3.0);
+extern PKPaymentNetwork const PKPaymentNetworkPrivateLabel NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(3.0);
+extern PKPaymentNetwork const PKPaymentNetworkVisa NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(3.0);
 
 typedef NS_ENUM(NSInteger, PKPaymentAuthorizationStatus) {
     PKPaymentAuthorizationStatusSuccess, // Merchant auth'd (or expects to auth) the transaction successfully.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPassLibrary.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPassLibrary.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPassLibrary.h	2016-06-05 05:29:56.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPassLibrary.h	2016-06-28 06:15:58.000000000 +0200
@@ -89,19 +89,21 @@
 
 // This notification is issued by a library instance, with that instance as the sender.  If there are no instantiated library objects,
 // no notifications. There are no guarantees about what thread or queue these come in on.
-extern NSString * const PKPassLibraryDidChangeNotification NS_AVAILABLE_IOS(6_0);
-extern NSString * const PKPassLibraryRemotePaymentPassesDidChangeNotification NS_AVAILABLE_IOS(9_0);
+typedef NSString * PKPassLibraryNotificationName NS_EXTENSIBLE_STRING_ENUM;
+extern PKPassLibraryNotificationName const PKPassLibraryDidChangeNotification NS_AVAILABLE_IOS(6_0);
+extern PKPassLibraryNotificationName const PKPassLibraryRemotePaymentPassesDidChangeNotification NS_AVAILABLE_IOS(9_0);
 
 // Entries in user info dictionary for PKPassLibraryDidChangeNotification.
 // - PKPassLibraryAddedPassesUserInfoKey is the key for an array of passes
 // - PKPassLibraryReplacementPassesUserInfoKey is the key for an array of passes
 // - PKPassLibraryRemovedPassInfosUserInfoKey is the key for an array of dictionaries, each of which has keys
 //   PKPassLibraryPassTypeIdentifierUserInfoKey and PKPassLibrarySerialNumberUserInfoKey mapping to strings.
-extern NSString *const PKPassLibraryAddedPassesUserInfoKey NS_AVAILABLE_IOS(6_0);
-extern NSString *const PKPassLibraryReplacementPassesUserInfoKey NS_AVAILABLE_IOS(6_0);
-extern NSString *const PKPassLibraryRemovedPassInfosUserInfoKey NS_AVAILABLE_IOS(6_0);
+typedef NSString * PKPassLibraryNotificationKey NS_STRING_ENUM;
+extern PKPassLibraryNotificationKey const PKPassLibraryAddedPassesUserInfoKey NS_AVAILABLE_IOS(6_0);
+extern PKPassLibraryNotificationKey const PKPassLibraryReplacementPassesUserInfoKey NS_AVAILABLE_IOS(6_0);
+extern PKPassLibraryNotificationKey const PKPassLibraryRemovedPassInfosUserInfoKey NS_AVAILABLE_IOS(6_0);
 
-extern NSString *const PKPassLibraryPassTypeIdentifierUserInfoKey NS_AVAILABLE_IOS(6_0);
-extern NSString *const PKPassLibrarySerialNumberUserInfoKey NS_AVAILABLE_IOS(6_0);
+extern PKPassLibraryNotificationKey const PKPassLibraryPassTypeIdentifierUserInfoKey NS_AVAILABLE_IOS(6_0);
+extern PKPassLibraryNotificationKey const PKPassLibrarySerialNumberUserInfoKey NS_AVAILABLE_IOS(6_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentAuthorizationController.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentAuthorizationController.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentAuthorizationController.h	2016-05-24 07:24:59.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentAuthorizationController.h	2016-06-28 06:15:58.000000000 +0200
@@ -96,11 +96,11 @@
 // by the merchant.
 // NO if the user cannot authorize payments on these networks or if the user is restricted from
 // authorizing payments.
-+ (BOOL)canMakePaymentsUsingNetworks:(NSArray<NSString *> *)supportedNetworks;
++ (BOOL)canMakePaymentsUsingNetworks:(NSArray<PKPaymentNetwork> *)supportedNetworks;
 
 // Determine whether this device can process payments using the specified networks and capabilities bitmask
 // See +canMakePaymentsUsingNetworks:
-+ (BOOL)canMakePaymentsUsingNetworks:(NSArray<NSString *> *)supportedNetworks capabilities:(PKMerchantCapability)capabilties;
++ (BOOL)canMakePaymentsUsingNetworks:(NSArray<PKPaymentNetwork> *)supportedNetworks capabilities:(PKMerchantCapability)capabilties;
 
 // The controller's delegate.
 @property (nonatomic, weak, nullable) id<PKPaymentAuthorizationControllerDelegate> delegate;
@@ -109,7 +109,7 @@
 - (instancetype)initWithPaymentRequest:(PKPaymentRequest *)request NS_DESIGNATED_INITIALIZER;
 
 // Presents the Apple Pay UI modally over your app. You are responsible for dismissal
-- (void)presentWithCompletion:(void(^)(BOOL success))completion;
+- (void)presentWithCompletion:(nullable void(^)(BOOL success))completion;
 
 // Dismisses the Apple Pay UI. Call this when you receive the paymentAuthorizationControllerDidFinish delegate
 // callback, or otherwise wish a dismissal to occur
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentAuthorizationViewController.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentAuthorizationViewController.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentAuthorizationViewController.h	2016-06-05 05:30:27.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentAuthorizationViewController.h	2016-06-29 07:17:01.000000000 +0200
@@ -120,11 +120,11 @@
 // by the merchant.
 // NO if the user cannot authorize payments on these networks or if the user is restricted from
 // authorizing payments.
-+ (BOOL)canMakePaymentsUsingNetworks:(NSArray<NSString *> *)supportedNetworks;
++ (BOOL)canMakePaymentsUsingNetworks:(NSArray<PKPaymentNetwork> *)supportedNetworks;
 
 // Determine whether this device can process payments using the specified networks and capabilities bitmask
 // See -canMakePaymentsUsingNetworks:
-+ (BOOL)canMakePaymentsUsingNetworks:(NSArray<NSString *> *)supportedNetworks capabilities:(PKMerchantCapability)capabilties NS_AVAILABLE_IOS(9_0);
++ (BOOL)canMakePaymentsUsingNetworks:(NSArray<PKPaymentNetwork> *)supportedNetworks capabilities:(PKMerchantCapability)capabilties NS_AVAILABLE_IOS(9_0);
 
 // The view controller's delegate.
 @property (nonatomic, assign, nullable) id<PKPaymentAuthorizationViewControllerDelegate> delegate;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentMethod.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentMethod.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentMethod.h	2016-06-05 05:30:27.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentMethod.h	2016-06-29 07:17:01.000000000 +0200
@@ -20,7 +20,7 @@
     PKPaymentMethodTypeDebit,
     PKPaymentMethodTypeCredit,
     PKPaymentMethodTypePrepaid,
-    PKPaymentMethodTypeStore,
+    PKPaymentMethodTypeStore
 } NS_ENUM_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(3.0);
 
 // A string describing the instrument that's suitable for display
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentRequest.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentRequest.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentRequest.h	2016-05-24 07:26:38.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentRequest.h	2016-06-28 08:26:53.000000000 +0200
@@ -10,6 +10,8 @@
 #import <AddressBook/ABRecord.h>
 #endif // TARGET_OS_IOS
 
+#import <PassKit/PKConstants.h>
+
 #ifndef __PKPAYMENTREQUEST_H__
 #define __PKPAYMENTREQUEST_H__
 
@@ -86,7 +88,7 @@
 @interface PKPaymentRequest : NSObject
 
 // The payment networks and platforms supported for in-app payment
-+ (NSArray<NSString *> *)availableNetworks NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3.0);
++ (NSArray<PKPaymentNetwork> *)availableNetworks NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3.0);
 
 // Identifies the merchant, as previously agreed with Apple.  Must match one of the merchant
 // identifiers in the application's entitlement.
@@ -97,7 +99,7 @@
 
 // The payment networks supported by the merchant, for example @[ PKPaymentNetworkVisa,
 // PKPaymentNetworkMasterCard ].  This property constrains payment cards that may fund the payment.
-@property (nonatomic, copy) NSArray<NSString *> *supportedNetworks;
+@property (nonatomic, copy) NSArray<PKPaymentNetwork> *supportedNetworks;
 
 // The payment processing capabilities of the merchant.
 @property (nonatomic, assign) PKMerchantCapability merchantCapabilities;

```