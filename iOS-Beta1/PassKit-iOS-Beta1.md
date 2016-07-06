#PassKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKAddPassButton.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKAddPassButton.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKAddPassButton.h	2015-10-03 02:33:49.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKAddPassButton.h	2016-06-05 05:30:27.000000000 +0200
@@ -4,6 +4,8 @@
 //
 //  Copyright © 2015 Apple, Inc. All rights reserved.
 //
+#if TARGET_OS_IPHONE
+
 #import <UIKit/UIKit.h>
 
 NS_ASSUME_NONNULL_BEGIN
@@ -25,4 +27,6 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
+
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKAddPassesViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKAddPassesViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKAddPassesViewController.h	2015-10-03 02:33:49.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKAddPassesViewController.h	2016-06-05 05:30:27.000000000 +0200
@@ -5,6 +5,8 @@
 //  Copyright (c) 2011 Apple, Inc. All rights reserved.
 //
 
+#if TARGET_OS_IPHONE
+
 #import <UIKit/UIKit.h>
 
 @class PKPass;
@@ -17,7 +19,7 @@
 -(void)addPassesViewControllerDidFinish:(PKAddPassesViewController *)controller; // delegate should dismiss presentation
 @end
 
-NS_CLASS_AVAILABLE(NA, 6_0)
+NS_CLASS_AVAILABLE_IOS(6_0)
 @interface PKAddPassesViewController : UIViewController
 
 /* controller should be presented with -presentViewController:animated:completion:
@@ -32,3 +34,5 @@
 @end
 
 NS_ASSUME_NONNULL_END
+
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKAddPaymentPassViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKAddPaymentPassViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKAddPaymentPassViewController.h	2015-10-03 02:33:49.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKAddPaymentPassViewController.h	2016-06-05 05:30:27.000000000 +0200
@@ -4,6 +4,9 @@
 //
 //  Copyright © 2015 Apple, Inc. All rights reserved.
 //
+
+#if TARGET_OS_IPHONE
+
 #import <UIKit/UIKit.h>
 NS_ASSUME_NONNULL_BEGIN
 
@@ -89,4 +92,6 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
+
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKConstants.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKConstants.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKConstants.h	2015-11-14 01:44:26.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKConstants.h	2016-06-05 05:30:27.000000000 +0200
@@ -7,13 +7,32 @@
 
 #import <Foundation/Foundation.h>
 
+#ifndef PKCONSTANTS_H
+#define PKCONSTANTS_H
+
 extern NSString * const PKEncryptionSchemeECC_V2 NS_AVAILABLE_IOS(9_0);
+extern NSString * const PKEncryptionSchemeRSA_V2 NS_AVAILABLE_IOS(10_0);
+
+extern NSString * const PKPaymentNetworkAmex NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(3.0);
+extern NSString * const PKPaymentNetworkChinaUnionPay NS_AVAILABLE_IOS(9_2) __WATCHOS_AVAILABLE(3.0);
+extern NSString * const PKPaymentNetworkDiscover NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(3.0);
+extern NSString * const PKPaymentNetworkInterac NS_AVAILABLE_IOS(9_2) __WATCHOS_AVAILABLE(3.0);
+extern NSString * const PKPaymentNetworkMasterCard NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(3.0);
+extern NSString * const PKPaymentNetworkPrivateLabel NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(3.0);
+extern NSString * const PKPaymentNetworkVisa NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(3.0);
+
+typedef NS_ENUM(NSInteger, PKPaymentAuthorizationStatus) {
+    PKPaymentAuthorizationStatusSuccess, // Merchant auth'd (or expects to auth) the transaction successfully.
+    PKPaymentAuthorizationStatusFailure, // Merchant failed to auth the transaction.
+
+    PKPaymentAuthorizationStatusInvalidBillingPostalAddress,  // Merchant refuses service to this billing address.
+    PKPaymentAuthorizationStatusInvalidShippingPostalAddress, // Merchant refuses service to this shipping address.
+    PKPaymentAuthorizationStatusInvalidShippingContact,       // Supplied contact information is insufficient.
+
+    PKPaymentAuthorizationStatusPINRequired NS_ENUM_AVAILABLE_IOS(9_2),  // Transaction requires PIN entry.
+    PKPaymentAuthorizationStatusPINIncorrect NS_ENUM_AVAILABLE_IOS(9_2), // PIN was not entered correctly, retry.
+    PKPaymentAuthorizationStatusPINLockout NS_ENUM_AVAILABLE_IOS(9_2)    // PIN retry limit exceeded.
 
-extern NSString * const PKPaymentNetworkAmex NS_AVAILABLE(NA, 8_0);
-extern NSString * const PKPaymentNetworkChinaUnionPay NS_AVAILABLE(NA, 9_2);
-extern NSString * const PKPaymentNetworkDiscover NS_AVAILABLE(NA, 9_0);
-extern NSString * const PKPaymentNetworkInterac NS_AVAILABLE(NA, 9_2);
-extern NSString * const PKPaymentNetworkMasterCard NS_AVAILABLE(NA, 8_0);
-extern NSString * const PKPaymentNetworkPrivateLabel NS_AVAILABLE(NA, 9_0);
-extern NSString * const PKPaymentNetworkVisa NS_AVAILABLE(NA, 8_0);
+} NS_ENUM_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(3.0);
 
+#endif // PKCONSTANTS_H
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKContact.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKContact.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKContact.h	2015-11-14 01:44:26.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKContact.h	2016-06-05 05:30:27.000000000 +0200
@@ -7,14 +7,14 @@
 #import <Foundation/Foundation.h>
 #import <Contacts/Contacts.h>
 
-NS_CLASS_AVAILABLE(NA, 9_0)
+NS_CLASS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(3.0)
 @interface PKContact : NSObject
 
-@property (nonatomic, retain, nullable) NSPersonNameComponents *name;
+@property (nonatomic, strong, nullable) NSPersonNameComponents *name;
 
-@property (nonatomic, retain, nullable) CNPostalAddress *postalAddress;
-@property (nonatomic, retain, nullable) NSString        *emailAddress;
-@property (nonatomic, retain, nullable) CNPhoneNumber   *phoneNumber;
+@property (nonatomic, strong, nullable) CNPostalAddress *postalAddress;
+@property (nonatomic, strong, nullable) NSString        *emailAddress;
+@property (nonatomic, strong, nullable) CNPhoneNumber   *phoneNumber;
 
 // CNPostalAddress does not support a distinct sublocality field. Some regions require a distinct sublocality,
 // and the Apple Pay sheet will prompt users to input it. Access the sublocality value here.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKError.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKError.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKError.h	2015-10-03 02:33:49.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKError.h	2016-06-05 05:30:27.000000000 +0200
@@ -17,6 +17,6 @@
     PKUnsupportedVersionError,
     PKInvalidSignature,
     PKNotEntitledError
-} NS_ENUM_AVAILABLE_IOS(6_0);
+} NS_AVAILABLE_IOS(6_0);
 
-#endif
+#endif // __PKERROR_H
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKObject.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKObject.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKObject.h	2015-10-03 02:33:49.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKObject.h	2016-06-05 05:30:27.000000000 +0200
@@ -15,4 +15,4 @@
 
 @end
 
-#endif
+#endif // __PKOBJECT_H
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPass.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPass.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPass.h	2015-10-03 02:33:49.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPass.h	2016-06-05 05:30:27.000000000 +0200
@@ -13,40 +13,46 @@
 typedef NS_ENUM(NSUInteger, PKPassType) {
     PKPassTypeBarcode,
     PKPassTypePayment,
-    PKPassTypeAny = ~0
+    PKPassTypeAny = ~(NSUInteger)0
 } NS_ENUM_AVAILABLE_IOS(8_0);
 
 @class PKPaymentPass;
+
+#if TARGET_OS_IPHONE
 @class UIImage;
+#endif
 
 NS_ASSUME_NONNULL_BEGIN
 @interface PKPass : PKObject
 
 - (instancetype)initWithData:(NSData *)data error:(NSError **)error;
 
-@property (nonatomic,assign,readonly) PKPassType                passType NS_AVAILABLE_IOS(8_0);
-@property (nonatomic,assign,readonly,nullable) PKPaymentPass    *paymentPass NS_AVAILABLE_IOS(8_0);
+@property (nonatomic, assign, readonly) PKPassType           passType NS_AVAILABLE_IOS(8_0);
+@property (nonatomic, readonly, nullable) PKPaymentPass      *paymentPass NS_AVAILABLE_IOS(8_0);
+
+@property (nonatomic, copy, readonly) NSString               *serialNumber;
+@property (nonatomic, copy, readonly) NSString               *passTypeIdentifier;
+@property (nonatomic, copy, readonly,nullable) NSURL         *webServiceURL;
+@property (nonatomic, copy, readonly,nullable) NSString      *authenticationToken;
 
-@property (nonatomic,copy,readonly) NSString                *serialNumber;
-@property (nonatomic,copy,readonly) NSString                *passTypeIdentifier;
-@property (nonatomic,copy,readonly,nullable) NSURL          *webServiceURL;
-@property (nonatomic,copy,readonly,nullable) NSString       *authenticationToken;
-
-@property (nonatomic,copy,readonly) UIImage                 *icon __WATCHOS_PROHIBITED;
-@property (nonatomic,copy,readonly) NSString                *localizedName; // e.g. "Boarding Pass"
-@property (nonatomic,copy,readonly) NSString                *localizedDescription; // e.g. "SFO -> LHR"
-@property (nonatomic,copy,readonly) NSString                *organizationName; // e.g. "Great Airways"
-@property (nonatomic,copy,readonly,nullable) NSDate         *relevantDate; // may be useful for sorting
-@property (nonatomic,copy,readonly,nullable) NSDictionary   *userInfo NS_AVAILABLE_IOS(7_0);
+#if TARGET_OS_IPHONE
+@property (nonatomic, copy, readonly) UIImage                *icon __WATCHOS_PROHIBITED;
+#endif
+
+@property (nonatomic, copy, readonly) NSString               *localizedName; // e.g. "Boarding Pass"
+@property (nonatomic, copy, readonly) NSString               *localizedDescription; // e.g. "SFO -> LHR"
+@property (nonatomic, copy, readonly) NSString               *organizationName; // e.g. "Great Airways"
+@property (nonatomic, copy, readonly, nullable) NSDate       *relevantDate; // may be useful for sorting
+@property (nonatomic, copy, readonly, nullable) NSDictionary *userInfo NS_AVAILABLE_IOS(7_0);
 
-@property (nonatomic,copy,readonly) NSURL *passURL; // open to view pass in Passbook.app
+@property (nonatomic, copy, readonly, nullable) NSURL *passURL; // open to view pass in Wallet app
 
-@property (nonatomic,assign,readonly,getter=isRemotePass)   BOOL        remotePass NS_AVAILABLE_IOS(9_0);
-@property (nonatomic,copy,readonly)                         NSString    *deviceName NS_AVAILABLE_IOS(9_0);
+@property (nonatomic, assign, readonly, getter=isRemotePass)   BOOL       remotePass NS_AVAILABLE_IOS(9_0);
+@property (nonatomic, copy, readonly)                          NSString   *deviceName NS_AVAILABLE_IOS(9_0);
 
 - (nullable id)localizedValueForFieldKey:(NSString *)key; // IBOutlet-like; allows access to field data from pass file format
 
 @end
 NS_ASSUME_NONNULL_END
 
-#endif
+#endif // __PKPASS_H
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPassLibrary.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPassLibrary.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPassLibrary.h	2015-10-03 02:33:49.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPassLibrary.h	2016-06-05 05:29:56.000000000 +0200
@@ -74,6 +74,9 @@
 // Opens the card setup flow (in Wallet on iPhone, Settings on iPad). Use this to direct a user to card setup directly from your app.
 - (void)openPaymentSetup __WATCHOS_PROHIBITED NS_AVAILABLE_IOS(8_3);
 
+// Presents the pass for use above the current application. The pass must already be in the pass library for this to have effect.
+- (void)presentPaymentPass:(PKPaymentPass *)pass __WATCHOS_PROHIBITED NS_AVAILABLE_IOS(10_0);
+
 // Returns YES if either the current device or an attached device both supports adding payment passes and does not already contain
 // a payment pass with the supplied primary account identifier.
 - (BOOL)canAddPaymentPassWithPrimaryAccountIdentifier:(NSString *)primaryAccountIdentifier NS_AVAILABLE_IOS(9_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPayment.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPayment.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPayment.h	2015-10-03 02:33:49.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPayment.h	2016-06-05 05:30:27.000000000 +0200
@@ -4,7 +4,9 @@
 //  Copyright (c) 2014 Apple, Inc. All rights reserved.
 //
 
+#if TARGET_OS_IOS
 #import <AddressBook/ABRecord.h>
+#endif // TARGET_OS_IOS
 #import <PassKit/PKPaymentToken.h>
 
 @class PKShippingMethod;
@@ -14,29 +16,35 @@
 // have a PKPaymentToken which contains a payment credential encrypted to the merchant
 // identifier specified in the request, and when requested, the user's shipping address
 // and chosen shipping method.
-NS_CLASS_AVAILABLE(NA, 8_0)
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(3.0)
 @interface PKPayment : NSObject
 
 // A PKPaymentToken which contains an encrypted payment credential.
-@property (nonatomic, readonly, nonnull) PKPaymentToken *token;
+@property (nonatomic, strong, readonly, nonnull) PKPaymentToken *token;
 
 // The full billing address that the user selected for this transaction.  Fields are
 // constrained to those specified in the requiredBillingAddressFields property of the original
 // PKPaymentRequest object.  This property is only set when the application has set
 // the requiredBillingAddressFields property of the PKPaymentRequest.
-@property (nonatomic, readonly, nullable) ABRecordRef billingAddress NS_DEPRECATED_IOS(8_0, 9_0, "Use billingContact instead");
-@property (nonatomic, readonly, nullable) PKContact *billingContact NS_AVAILABLE_IOS(9_0);
+@property (nonatomic, strong, readonly, nullable) PKContact *billingContact NS_AVAILABLE_IOS(9_0);
+
+#if TARGET_OS_IOS
+@property (nonatomic, assign, readonly, nullable) ABRecordRef billingAddress NS_DEPRECATED_IOS(8_0, 9_0, "Use billingContact instead") __WATCHOS_PROHIBITED;
+#endif // TARGET_OS_IOS
 
 // The full shipping address that the user selected for this transaction.  Fields are
 // constrained to those specified in the requiredShippingAddressFields property of the original
 // PKPaymentRequest object.  This property is only set when the application has set
 // the requiredShippingAddressFields property of the PKPaymentRequest.
-@property (nonatomic, readonly, nullable) ABRecordRef shippingAddress NS_DEPRECATED_IOS(8_0, 9_0, "Use shippingContact instead");;
-@property (nonatomic, readonly, nullable) PKContact *shippingContact NS_AVAILABLE_IOS(9_0);
+@property (nonatomic, strong, readonly, nullable) PKContact *shippingContact NS_AVAILABLE_IOS(9_0);
+
+#if TARGET_OS_IOS
+@property (nonatomic, assign, readonly, nullable) ABRecordRef shippingAddress NS_DEPRECATED_IOS(8_0, 9_0, "Use shippingContact instead") __WATCHOS_PROHIBITED;
+#endif // TARGET_OS_IOS
 
 // The shipping method that the user chose.  This property is only set when the
 // application has set the shippingMethods property of the PKPaymentRequest.
-@property (nonatomic, readonly, nullable) PKShippingMethod *shippingMethod;
+@property (nonatomic, strong, readonly, nullable) PKShippingMethod *shippingMethod;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentAuthorizationController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentAuthorizationController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentAuthorizationController.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentAuthorizationController.h	2016-05-24 07:24:59.000000000 +0200
@@ -0,0 +1,122 @@
+//
+//  PKPaymentAuthorizationController.h
+//  PassKit
+//
+//  Copyright © 2015 Apple, Inc. All rights reserved.
+//
+#if TARGET_OS_IPHONE
+
+#import <PassKit/PKConstants.h>
+#import <PassKit/PKPaymentRequest.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class PKPayment;
+@class PKContact;
+@class PKPaymentMethod;
+@class PKShippingMethod;
+@class PKPaymentSummaryItem;
+@class PKPaymentAuthorizationController;
+
+@protocol PKPaymentAuthorizationControllerDelegate <NSObject>
+
+@required
+
+// Sent to the delegate after the user has acted on the payment request.  The application
+// should inspect the payment to determine whether the payment request was authorized.
+//
+// If the application requested a shipping contact then the full contact is now part of the payment.
+//
+// The delegate must call completion with an appropriate authorization status, as may be determined
+// by submitting the payment credential to a processing gateway for payment authorization.
+- (void)paymentAuthorizationController:(PKPaymentAuthorizationController *)controller
+                   didAuthorizePayment:(PKPayment *)payment
+                            completion:(void (^)(PKPaymentAuthorizationStatus status))completion;
+
+
+// Sent to the delegate when payment authorization is finished.  This may occur when
+// the user cancels the request, or after the PKPaymentAuthorizationStatus parameter of the
+// paymentAuthorizationController:didAuthorizePayment:completion: has been shown to the user.
+//
+// The delegate is responsible for dismissing and releasing the controller in this method.
+- (void)paymentAuthorizationControllerDidFinish:(PKPaymentAuthorizationController *)controller;
+
+@optional
+
+
+// Sent to the delegate before the payment is authorized, but after the user has authenticated using
+// the side button. Optional.
+- (void)paymentAuthorizationControllerWillAuthorizePayment:(PKPaymentAuthorizationController *)controller;
+
+
+// Sent when the user has selected a new shipping method.  The delegate should determine
+// shipping costs based on the shipping method and either the shipping address contact in the original
+// PKPaymentRequest or the contact provided by the last call to paymentAuthorizationController:
+// didSelectShippingContact:completion:.
+//
+// The delegate must invoke the completion block with an updated array of PKPaymentSummaryItem objects.
+//
+// The delegate will receive no further callbacks except paymentAuthorizationControllerDidFinish:
+// until it has invoked the completion block.
+- (void)paymentAuthorizationController:(PKPaymentAuthorizationController *)controller
+               didSelectShippingMethod:(PKShippingMethod *)shippingMethod
+                            completion:(void (^)(PKPaymentAuthorizationStatus status, NSArray<PKPaymentSummaryItem *> *summaryItems))completion;
+
+- (void)paymentAuthorizationController:(PKPaymentAuthorizationController *)controller
+              didSelectShippingContact:(PKContact *)contact
+                            completion:(void (^)(PKPaymentAuthorizationStatus status, NSArray<PKShippingMethod *> *shippingMethods,
+                                                 NSArray<PKPaymentSummaryItem *> *summaryItems))completion;
+
+// Sent when the user has selected a new payment card.  Use this delegate callback if you need to
+// update the summary items in response to the card type changing (for example, applying credit card surcharges)
+//
+// The delegate will receive no further callbacks except paymentAuthorizationControllerDidFinish:
+// until it has invoked the completion block.
+- (void)paymentAuthorizationController:(PKPaymentAuthorizationController *)controller
+                didSelectPaymentMethod:(PKPaymentMethod *)paymentMethod
+                            completion:(void (^)(NSArray<PKPaymentSummaryItem *> *summaryItems))completion;
+
+@end
+
+// PKPaymentAuthorizationController prompts the user to authorize a PKPaymentRequest, funding the
+// payment amount with a valid payment card.
+__WATCHOS_AVAILABLE(3.0) __IOS_AVAILABLE(10.0)
+@interface PKPaymentAuthorizationController : NSObject
+
+// Determine whether this device can process payment requests.
+// YES if the device is generally capable of making in-app payments.
+// NO if the device cannot make in-app payments or if the user is restricted from authorizing payments.
++ (BOOL)canMakePayments;
+
+// Determine whether this device can process payment requests using specific payment network brands.
+// Your application should confirm that the user can make payments before attempting to authorize a payment.
+// Your application may also want to alter its appearance or behavior when the user is not allowed
+// to make payments.
+// YES if the user can authorize payments on this device using one of the payment networks supported
+// by the merchant.
+// NO if the user cannot authorize payments on these networks or if the user is restricted from
+// authorizing payments.
++ (BOOL)canMakePaymentsUsingNetworks:(NSArray<NSString *> *)supportedNetworks;
+
+// Determine whether this device can process payments using the specified networks and capabilities bitmask
+// See +canMakePaymentsUsingNetworks:
++ (BOOL)canMakePaymentsUsingNetworks:(NSArray<NSString *> *)supportedNetworks capabilities:(PKMerchantCapability)capabilties;
+
+// The controller's delegate.
+@property (nonatomic, weak, nullable) id<PKPaymentAuthorizationControllerDelegate> delegate;
+
+// Initialize the controller with a payment request.
+- (instancetype)initWithPaymentRequest:(PKPaymentRequest *)request NS_DESIGNATED_INITIALIZER;
+
+// Presents the Apple Pay UI modally over your app. You are responsible for dismissal
+- (void)presentWithCompletion:(void(^)(BOOL success))completion;
+
+// Dismisses the Apple Pay UI. Call this when you receive the paymentAuthorizationControllerDidFinish delegate
+// callback, or otherwise wish a dismissal to occur
+- (void)dismissWithCompletion:(nullable void(^)(void))completion;
+
+@end
+
+NS_ASSUME_NONNULL_END
+
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentAuthorizationViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentAuthorizationViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentAuthorizationViewController.h	2015-11-14 01:44:26.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentAuthorizationViewController.h	2016-06-05 05:30:27.000000000 +0200
@@ -4,9 +4,17 @@
 //
 //  Copyright (c) 2014 Apple, Inc. All rights reserved.
 //
+#if !TARGET_OS_WATCH && !TARGET_OS_TV
 
+#if TARGET_OS_IPHONE
 #import <UIKit/UIKit.h>
 #import <AddressBook/ABRecord.h>
+#else
+#import <AppKit/AppKit.h>
+#import <AddressBook/ABAddressBookC.h>
+#endif
+
+#import <PassKit/PKConstants.h>
 #import <PassKit/PKPaymentRequest.h>
 
 NS_ASSUME_NONNULL_BEGIN
@@ -18,20 +26,6 @@
 @class PKPaymentSummaryItem;
 @class PKPaymentAuthorizationViewController;
 
-typedef NS_ENUM(NSInteger, PKPaymentAuthorizationStatus) {
-    PKPaymentAuthorizationStatusSuccess, // Merchant auth'd (or expects to auth) the transaction successfully.
-    PKPaymentAuthorizationStatusFailure, // Merchant failed to auth the transaction.
-    
-    PKPaymentAuthorizationStatusInvalidBillingPostalAddress,  // Merchant refuses service to this billing address.
-    PKPaymentAuthorizationStatusInvalidShippingPostalAddress, // Merchant refuses service to this shipping address.
-    PKPaymentAuthorizationStatusInvalidShippingContact,       // Supplied contact information is insufficient.
-    
-    PKPaymentAuthorizationStatusPINRequired NS_ENUM_AVAILABLE(NA, 9_2),  // Transaction requires PIN entry.
-    PKPaymentAuthorizationStatusPINIncorrect NS_ENUM_AVAILABLE(NA, 9_2), // PIN was not entered correctly, retry.
-    PKPaymentAuthorizationStatusPINLockout NS_ENUM_AVAILABLE(NA, 9_2)    // PIN retry limit exceeded.
-    
-} NS_ENUM_AVAILABLE(NA, 8_0);
-
 @protocol PKPaymentAuthorizationViewControllerDelegate <NSObject>
 
 @required
@@ -105,8 +99,13 @@
 
 // PKPaymentAuthorizationViewController prompts the user to authorize a PKPaymentRequest, funding the
 // payment amount with a valid payment card.
-NS_CLASS_AVAILABLE(NA, 8_0)
+#if TARGET_OS_IPHONE
+NS_CLASS_AVAILABLE_IOS(8_0)
 @interface PKPaymentAuthorizationViewController : UIViewController
+#else
+NS_CLASS_AVAILABLE_MAC(10_12)
+@interface PKPaymentAuthorizationViewController : NSViewController
+#endif
 
 // Determine whether this device can process payment requests.
 // YES if the device is generally capable of making in-app payments.
@@ -137,4 +136,6 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
+
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentButton.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentButton.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentButton.h	2015-10-03 02:33:49.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentButton.h	2016-06-05 05:30:27.000000000 +0200
@@ -3,6 +3,9 @@
 //
 //  Copyright © 2014 Apple, Inc. All rights reserved.
 //
+
+#if TARGET_OS_IPHONE
+
 #import <UIKit/UIKit.h>
 
 NS_ASSUME_NONNULL_BEGIN
@@ -16,13 +19,14 @@
 typedef NS_ENUM(NSInteger, PKPaymentButtonType) {
     PKPaymentButtonTypePlain = 0,
     PKPaymentButtonTypeBuy,
-    PKPaymentButtonTypeSetUp NS_ENUM_AVAILABLE_IOS(9_0)
+    PKPaymentButtonTypeSetUp NS_ENUM_AVAILABLE_IOS(9_0),
+    PKPaymentButtonTypeInStore NS_ENUM_AVAILABLE_IOS(10_0)
 } NS_ENUM_AVAILABLE_IOS(8_3);
 
 // PKPaymentButton vends a number of Apple Pay related buttons for use inside of your app
 // These buttons can be used to prompt the user to pay with Apple Pay, or set up cards for payment
 // Refer to the Apple Pay developer documentation for more information on how to use this class
-NS_CLASS_AVAILABLE(NA, 8_3) @interface PKPaymentButton : UIButton
+NS_CLASS_AVAILABLE_IOS(8_3) @interface PKPaymentButton : UIButton
 
 + (instancetype)buttonWithType:(PKPaymentButtonType)buttonType style:(PKPaymentButtonStyle)buttonStyle;
 
@@ -30,4 +34,6 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
+
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentMethod.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentMethod.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentMethod.h	2015-10-03 02:33:49.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentMethod.h	2016-06-05 05:30:27.000000000 +0200
@@ -12,7 +12,7 @@
 @class PKPaymentPass;
 
 NS_ASSUME_NONNULL_BEGIN
-NS_CLASS_AVAILABLE(NA, 9_0)
+NS_CLASS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(3.0)
 @interface PKPaymentMethod : NSObject
 
 typedef NS_OPTIONS(NSUInteger, PKPaymentMethodType) {
@@ -21,23 +21,23 @@
     PKPaymentMethodTypeCredit,
     PKPaymentMethodTypePrepaid,
     PKPaymentMethodTypeStore,
-} NS_ENUM_AVAILABLE(NA, 9_0);
+} NS_ENUM_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(3.0);
 
 // A string describing the instrument that's suitable for display
-@property (nonatomic, readonly, nullable) NSString *displayName;
+@property (nonatomic, copy, readonly, nullable) NSString *displayName;
 
 // The payment network that backs the instrument. Suitable for display.
-@property (nonatomic, readonly, nullable) NSString *network;
+@property (nonatomic, copy, readonly, nullable) NSString *network;
 
 // The underlying instrument type (Credit, Debit, etc)
 @property (nonatomic, readonly) PKPaymentMethodType type;
 
 // The payment pass - will only be provided if your app is entitled to view the pass in question
-@property (nonatomic, readonly, nullable) PKPaymentPass *paymentPass;
+@property (nonatomic, copy, readonly, nullable) PKPaymentPass *paymentPass;
 
 @end
 
 NS_ASSUME_NONNULL_END
 
-#endif
+#endif // End __PKPAYMENTMETHOD_H
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentPass.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentPass.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentPass.h	2015-10-03 02:33:49.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentPass.h	2016-06-05 05:30:27.000000000 +0200
@@ -24,13 +24,13 @@
 NS_CLASS_AVAILABLE_IOS(8_0)
 @interface PKPaymentPass : PKPass
 
-@property (nonatomic,copy,readonly) NSString                      *primaryAccountIdentifier;
-@property (nonatomic,copy,readonly) NSString                      *primaryAccountNumberSuffix;
-@property (readonly)                NSString                      *deviceAccountIdentifier;
-@property (readonly)                NSString                      *deviceAccountNumberSuffix;
-@property (nonatomic, readonly)     PKPaymentPassActivationState  activationState;
+@property (nonatomic, copy, readonly) NSString *primaryAccountIdentifier;
+@property (nonatomic, copy, readonly) NSString *primaryAccountNumberSuffix;
+@property (weak, readonly) NSString *deviceAccountIdentifier;
+@property (weak, readonly) NSString *deviceAccountNumberSuffix;
+@property (nonatomic, readonly) PKPaymentPassActivationState activationState;
 
 @end
 NS_ASSUME_NONNULL_END
 
-#endif
+#endif // End __PKPAYMENTPASS_H
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentRequest.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentRequest.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentRequest.h	2015-10-03 02:33:49.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentRequest.h	2016-05-24 07:26:38.000000000 +0200
@@ -5,46 +5,52 @@
 //
 
 #import <Foundation/Foundation.h>
+
+#if TARGET_OS_IOS
 #import <AddressBook/ABRecord.h>
+#endif // TARGET_OS_IOS
+
+#ifndef __PKPAYMENTREQUEST_H__
+#define __PKPAYMENTREQUEST_H__
 
 @class PKContact;
 
 NS_ASSUME_NONNULL_BEGIN
 
 typedef NS_OPTIONS(NSUInteger, PKMerchantCapability) {
-    PKMerchantCapability3DS                                 = 1UL << 0,   // Merchant supports 3DS
-    PKMerchantCapabilityEMV                                 = 1UL << 1,   // Merchant supports EMV
-    PKMerchantCapabilityCredit NS_ENUM_AVAILABLE_IOS(9_0)   = 1UL << 2,   // Merchant supports credit
-    PKMerchantCapabilityDebit  NS_ENUM_AVAILABLE_IOS(9_0)   = 1UL << 3    // Merchant supports debit
-} NS_ENUM_AVAILABLE(NA, 8_0);
+    PKMerchantCapability3DS                                  = 1UL << 0,   // Merchant supports 3DS
+    PKMerchantCapabilityEMV                                  = 1UL << 1,   // Merchant supports EMV
+    PKMerchantCapabilityCredit NS_ENUM_AVAILABLE_IOS(9_0) = 1UL << 2,   // Merchant supports credit
+    PKMerchantCapabilityDebit  NS_ENUM_AVAILABLE_IOS(9_0) = 1UL << 3    // Merchant supports debit
+} NS_ENUM_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(3.0);
 
 typedef NS_OPTIONS(NSUInteger, PKAddressField) {
-    PKAddressFieldNone                              = 0UL,      // No address fields required.
-    PKAddressFieldPostalAddress                     = 1UL << 0, // Full street address including name, street, city, state/province, postal code, country.
-    PKAddressFieldPhone                             = 1UL << 1,
-    PKAddressFieldEmail                             = 1UL << 2,
-    PKAddressFieldName NS_ENUM_AVAILABLE_IOS(8_3)   = 1UL << 3,
-    PKAddressFieldAll                               = (PKAddressFieldPostalAddress|PKAddressFieldPhone|PKAddressFieldEmail|PKAddressFieldName)
-} NS_ENUM_AVAILABLE(NA, 8_0);
+    PKAddressFieldNone                               = 0UL,      // No address fields required.
+    PKAddressFieldPostalAddress                      = 1UL << 0, // Full street address including name, street, city, state/province, postal code, country.
+    PKAddressFieldPhone                              = 1UL << 1,
+    PKAddressFieldEmail                              = 1UL << 2,
+    PKAddressFieldName NS_ENUM_AVAILABLE_IOS(8_3) = 1UL << 3,
+    PKAddressFieldAll                                = (PKAddressFieldPostalAddress|PKAddressFieldPhone|PKAddressFieldEmail|PKAddressFieldName)
+} NS_ENUM_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(3.0);
 
 typedef NS_ENUM(NSUInteger, PKShippingType) {
     PKShippingTypeShipping,
     PKShippingTypeDelivery,
     PKShippingTypeStorePickup,
     PKShippingTypeServicePickup
-} NS_ENUM_AVAILABLE(NA, 8_3);
+} NS_ENUM_AVAILABLE_IOS(8_3) __WATCHOS_AVAILABLE(3.0);
 
 typedef NS_ENUM(NSUInteger, PKPaymentSummaryItemType) {
     PKPaymentSummaryItemTypeFinal,      // The payment summary item's amount is known to be correct
     PKPaymentSummaryItemTypePending     // The payment summary item's amount is estimated or unknown - e.g, a taxi fare
-} NS_ENUM_AVAILABLE(NA, 9_0);
+} NS_ENUM_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(3.0);
 
 // PKPaymentSummaryItem Defines a line-item for a payment such as tax, shipping, or discount.
-NS_CLASS_AVAILABLE(NA, 8_0)
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(3.0)
 @interface PKPaymentSummaryItem : NSObject
 
 + (instancetype)summaryItemWithLabel:(NSString *)label amount:(NSDecimalNumber *)amount;
-+ (instancetype)summaryItemWithLabel:(NSString *)label amount:(NSDecimalNumber *)amount type:(PKPaymentSummaryItemType)type NS_AVAILABLE(NA, 9_0);
++ (instancetype)summaryItemWithLabel:(NSString *)label amount:(NSDecimalNumber *)amount type:(PKPaymentSummaryItemType)type NS_AVAILABLE_IOS(9_0);
 
 // A short localized description of the item, e.g. "Tax" or "Gift Card".
 @property (nonatomic, copy) NSString *label;
@@ -55,12 +61,12 @@
 
 // Defaults to PKPaymentSummaryItemTypeFinal
 // Set to PKPaymentSummaryItemTypePending if the amount of the item is not known at this time
-@property (nonatomic, assign) PKPaymentSummaryItemType type NS_AVAILABLE(NA, 9_0);
+@property (nonatomic, assign) PKPaymentSummaryItemType type NS_AVAILABLE_IOS(9_0);
 
 @end
 
 // Defines a shipping method for delivering physical goods.
-NS_CLASS_AVAILABLE(NA, 8_0)
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(3.0)
 @interface PKShippingMethod : PKPaymentSummaryItem
 
 // Application-defined unique identifier for this shipping method.  The application will receive this
@@ -76,9 +82,12 @@
 // PKPaymentRequest defines an application's request to produce a payment instrument for the
 // purchase of goods and services. It encapsulates information about the selling party's payment
 // processing capabilities, an amount to pay, and the currency code.
-NS_CLASS_AVAILABLE(NA, 8_0)
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(3.0)
 @interface PKPaymentRequest : NSObject
 
+// The payment networks and platforms supported for in-app payment
++ (NSArray<NSString *> *)availableNetworks NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3.0);
+
 // Identifies the merchant, as previously agreed with Apple.  Must match one of the merchant
 // identifiers in the application's entitlement.
 @property (nonatomic, copy) NSString *merchantIdentifier;
@@ -105,16 +114,22 @@
 @property (nonatomic, assign) PKAddressField requiredBillingAddressFields;
 
 // If the merchant already has a billing address on file, set it here.
-@property (nonatomic, assign, nullable) ABRecordRef billingAddress NS_DEPRECATED_IOS(8_0, 9_0, "Use billingContact instead");
-@property (nonatomic, retain, nullable) PKContact *billingContact NS_AVAILABLE_IOS(9_0);
+@property (nonatomic, strong, nullable) PKContact *billingContact NS_AVAILABLE_IOS(9_0);
+
+#if TARGET_OS_IOS
+@property (nonatomic, assign, nullable) ABRecordRef billingAddress __WATCHOS_PROHIBITED NS_DEPRECATED_IOS(8_0, 9_0, "Use billingContact instead");
+#endif
 
 // Indicates which shipping address fields the merchant requires in order to process a transaction.
 // The default is PKAddressFieldNone.
 @property (nonatomic, assign) PKAddressField requiredShippingAddressFields;
 
 // If the merchant already has a shipping address on file, set it here.
-@property (nonatomic, assign, nullable) ABRecordRef shippingAddress NS_DEPRECATED_IOS(8_0, 9_0, "Use shippingContact instead");
-@property (nonatomic, retain, nullable) PKContact *shippingContact NS_AVAILABLE_IOS(9_0);
+@property (nonatomic, strong, nullable) PKContact *shippingContact NS_AVAILABLE_IOS(9_0);
+
+#if TARGET_OS_IOS
+@property (nonatomic, assign, nullable) ABRecordRef shippingAddress __WATCHOS_PROHIBITED NS_DEPRECATED_IOS(8_0, 9_0, "Use shippingContact instead");
+#endif
 
 // Shipping methods supported by the merchant.
 @property (nonatomic, copy, nullable) NSArray<PKShippingMethod *> *shippingMethods;
@@ -130,3 +145,5 @@
 @end
 
 NS_ASSUME_NONNULL_END
+
+#endif // __PKPAYMENTREQUEST_H__
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentToken.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentToken.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentToken.h	2015-10-03 02:33:49.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentToken.h	2016-06-05 05:30:27.000000000 +0200
@@ -10,28 +10,28 @@
 
 // Contains the user's payment credentials, encrypted to the merchant.
 NS_ASSUME_NONNULL_BEGIN
-NS_CLASS_AVAILABLE(NA, 8_0)
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(3.0)
 @interface PKPaymentToken : NSObject
 
 // Describes the properties of the underlying payment instrument selected to fund the payment
-@property (nonatomic, readonly) PKPaymentMethod *paymentMethod NS_AVAILABLE_IOS(9_0);
+@property (nonatomic, strong, readonly) PKPaymentMethod *paymentMethod NS_AVAILABLE_IOS(9_0);
 
 // A string that describes the payment instrument the user has selected to fund the payment.
 // Suitable for display, e.g. "Amex 1234".
-@property (nonatomic, readonly) NSString *paymentInstrumentName NS_DEPRECATED_IOS(8_0, 9_0, "Use paymentMethod instead");
+@property (nonatomic, copy, readonly) NSString *paymentInstrumentName NS_DEPRECATED_IOS(8_0, 9_0, "Use paymentMethod instead") __WATCHOS_PROHIBITED;
 
 // Payment network for the card that funds the payment.
-@property (nonatomic, readonly) NSString *paymentNetwork NS_DEPRECATED_IOS(8_0, 9_0, "Use paymentMethod instead");
+@property (nonatomic, copy, readonly) NSString *paymentNetwork NS_DEPRECATED_IOS(8_0, 9_0, "Use paymentMethod instead") __WATCHOS_PROHIBITED;
 
 // A string that describes a globally unique identifier for this transaction that can be used
 // for receipt purposes.
-@property (nonatomic, readonly) NSString *transactionIdentifier;
+@property (nonatomic, copy, readonly) NSString *transactionIdentifier;
 
 // UTF-8 encoded JSON dictionary of encrypted payment data.  Ready for transmission to
 // merchant's e-commerce backend for decryption and submission to a payment processor's
 // gateway.
-@property (nonatomic, readonly) NSData *paymentData;
+@property (nonatomic, copy, readonly) NSData *paymentData;
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PassKit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PassKit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PassKit.h	2015-10-03 02:33:49.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PassKit.h	2016-06-05 05:30:27.000000000 +0200
@@ -12,12 +12,6 @@
 #import <PassKit/PKError.h>
 #import <PassKit/PKPassLibrary.h>
 #import <PassKit/PKContact.h>
-#if __has_include(<PassKit/PKAddPassesViewController.h>)
-#import <PassKit/PKAddPassesViewController.h>
-#endif
-#if __has_include(<PassKit/PKAddPaymentPassViewController.h>)
-#import <PassKit/PKAddPaymentPassViewController.h>
-#endif
 #if __has_include(<PassKit/PKPaymentRequest.h>)
 #import <PassKit/PKPaymentRequest.h>
 #endif
@@ -30,12 +24,23 @@
 #if __has_include(<PassKit/PKPaymentToken.h>)
 #import <PassKit/PKPaymentToken.h>
 #endif
+#if TARGET_OS_IPHONE || TARGET_OS_OSX
 #if __has_include(<PassKit/PKPaymentAuthorizationViewController.h>)
 #import <PassKit/PKPaymentAuthorizationViewController.h>
 #endif
+#if __has_include(<PassKit/PKPaymentAuthorizationController.h>)
+#import <PassKit/PKPaymentAuthorizationController.h>
+#endif
 #if __has_include(<PassKit/PKAddPassButton.h>)
 #import <PassKit/PKAddPassButton.h>
 #endif
 #if __has_include(<PassKit/PKPaymentButton.h>)
 #import <PassKit/PKPaymentButton.h>
 #endif
+#if __has_include(<PassKit/PKAddPassesViewController.h>)
+#import <PassKit/PKAddPassesViewController.h>
+#endif
+#if __has_include(<PassKit/PKAddPaymentPassViewController.h>)
+#import <PassKit/PKAddPaymentPassViewController.h>
+#endif
+#endif // TARGET_OS_IPHONE

```