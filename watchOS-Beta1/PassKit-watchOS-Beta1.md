#PassKit.framework

``` diff
diff -ruN /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKConstants.h /Applications/Xcode81.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKConstants.h
--- /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKConstants.h	2016-08-06 10:50:37.000000000 +0200
+++ /Applications/Xcode81.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKConstants.h	2016-09-15 07:27:39.000000000 +0200
@@ -23,6 +23,8 @@
 extern PKPaymentNetwork const PKPaymentNetworkMasterCard NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(3.0);
 extern PKPaymentNetwork const PKPaymentNetworkPrivateLabel NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(3.0);
 extern PKPaymentNetwork const PKPaymentNetworkVisa NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(3.0);
+extern PKPaymentNetwork const PKPaymentNetworkJCB NS_AVAILABLE_IOS(10_1) __WATCHOS_AVAILABLE(3.1);
+extern PKPaymentNetwork const PKPaymentNetworkSuica NS_AVAILABLE_IOS(10_1) __WATCHOS_AVAILABLE(3.1);
 
 typedef NS_ENUM(NSInteger, PKPaymentAuthorizationStatus) {
     PKPaymentAuthorizationStatusSuccess, // Merchant auth'd (or expects to auth) the transaction successfully.
@@ -38,4 +40,17 @@
 
 } NS_ENUM_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(3.0);
 
+typedef NS_ENUM(NSInteger, PKPaymentButtonStyle) {
+    PKPaymentButtonStyleWhite = 0,
+    PKPaymentButtonStyleWhiteOutline,
+    PKPaymentButtonStyleBlack
+} NS_ENUM_AVAILABLE_IOS(8_3);
+
+typedef NS_ENUM(NSInteger, PKPaymentButtonType) {
+    PKPaymentButtonTypePlain = 0,
+    PKPaymentButtonTypeBuy,
+    PKPaymentButtonTypeSetUp NS_ENUM_AVAILABLE_IOS(9_0),
+    PKPaymentButtonTypeInStore NS_ENUM_AVAILABLE_IOS(10_0)
+} NS_ENUM_AVAILABLE_IOS(8_3);
+
 #endif // PKCONSTANTS_H
diff -ruN /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKLabeledValue.h /Applications/Xcode81.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKLabeledValue.h
--- /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKLabeledValue.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode81.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKLabeledValue.h	2016-09-15 07:27:39.000000000 +0200
@@ -0,0 +1,21 @@
+//
+//  PKLabeledValue.h
+//  PassKit
+//
+//  Copyright © 2016 Apple, Inc. All rights reserved.
+//
+#import <Foundation/Foundation.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+NS_CLASS_AVAILABLE_IOS(10_1) @interface PKLabeledValue : NSObject
+
+- (instancetype)initWithLabel:(NSString *)label
+                        value:(NSString *)value NS_DESIGNATED_INITIALIZER;
+
+@property (nonatomic, copy, readonly) NSString *label;
+@property (nonatomic, copy, readonly) NSString *value;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPassLibrary.h /Applications/Xcode81.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPassLibrary.h
--- /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPassLibrary.h	2016-08-11 07:56:54.000000000 +0200
+++ /Applications/Xcode81.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPassLibrary.h	2016-09-15 07:26:46.000000000 +0200
@@ -81,6 +81,9 @@
 // a payment pass with the supplied primary account identifier.
 - (BOOL)canAddPaymentPassWithPrimaryAccountIdentifier:(NSString *)primaryAccountIdentifier NS_AVAILABLE_IOS(9_0);
 
+// If the library can add Felica passes, this method will return YES. Otherwise, NO will be returned.
+- (BOOL)canAddFelicaPass NS_AVAILABLE_IOS(10_1);
+
 // These methods may be utilized to activate a payment pass that is provisioned but currently in the inactive state, by providing
 // either a cryptographic OTP, or an activation code.
 - (void)activatePaymentPass:(PKPaymentPass *)paymentPass withActivationData:(NSData *)activationData completion:(nullable void(^)(BOOL success, NSError* error))completion __WATCHOS_PROHIBITED NS_AVAILABLE_IOS(8_0);
diff -ruN /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKSuicaPassProperties.h /Applications/Xcode81.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKSuicaPassProperties.h
--- /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKSuicaPassProperties.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode81.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKSuicaPassProperties.h	2016-09-15 07:27:39.000000000 +0200
@@ -0,0 +1,33 @@
+//
+//  PKSuicaPassProperties.h
+//  PassKit
+//
+//  Copyright (c) 2016 Apple, Inc. All rights reserved.
+//
+//
+
+#import <Foundation/Foundation.h>
+
+@class PKPass;
+
+NS_ASSUME_NONNULL_BEGIN
+
+NS_CLASS_AVAILABLE_IOS(10_1) __WATCHOS_AVAILABLE(3.1)
+@interface PKSuicaPassProperties : NSObject
+
+/// Properties for a given pass, or nil if the pass doesn’t support the set of properties being requested
++ (nullable instancetype)passPropertiesForPass:(PKPass *)pass;
+
+@property (nonatomic, copy, readonly) NSDecimalNumber *transitBalance;
+@property (nonatomic, copy, readonly) NSString *transitBalanceCurrencyCode;
+
+@property (nonatomic, assign, readonly, getter=isInStation) BOOL inStation;
+/// Note: isInShinkansenStation is not a subset of isInStation.
+@property (nonatomic, assign, readonly, getter=isInShinkansenStation) BOOL inShinkansenStation;
+
+@property (nonatomic, assign, readonly, getter=isGreenCarTicketUsed) BOOL greenCarTicketUsed;
+@property (nonatomic, assign, readonly, getter=isBlacklisted) BOOL blacklisted;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PassKit.h /Applications/Xcode81.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PassKit.h
--- /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PassKit.h	2016-08-06 10:50:38.000000000 +0200
+++ /Applications/Xcode81.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PassKit.h	2016-09-15 07:27:39.000000000 +0200
@@ -11,7 +11,13 @@
 #import <PassKit/PKPaymentPass.h>
 #import <PassKit/PKError.h>
 #import <PassKit/PKPassLibrary.h>
+#if __has_include(<PassKit/PKLabeledValue.h>)
+#import <PassKit/PKLabeledValue.h>
+#endif
 #import <PassKit/PKContact.h>
+#if __has_include(<PassKit/PKSuicaPassProperties.h>)
+#import <PassKit/PKSuicaPassProperties.h>
+#endif
 #if __has_include(<PassKit/PKPaymentRequest.h>)
 #import <PassKit/PKPaymentRequest.h>
 #endif

```