#PassKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKAddPaymentPassViewController.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKAddPaymentPassViewController.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKAddPaymentPassViewController.h	2016-06-29 07:17:01.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKAddPaymentPassViewController.h	2016-07-11 07:57:39.000000000 +0200
@@ -8,6 +8,7 @@
 #if TARGET_OS_IPHONE
 
 #import <UIKit/UIKit.h>
+#import <PassKit/PKConstants.h>
 NS_ASSUME_NONNULL_BEGIN
 
 @class PKAddPaymentPassViewController, PKPaymentPass;
@@ -25,9 +26,9 @@
  *  PKEncryptionSchemeECC_V2:
  *      ephemeralPublicKey
  */
-- (nullable instancetype)initWithEncryptionScheme:(NSString *)encryptionScheme NS_DESIGNATED_INITIALIZER;
+- (nullable instancetype)initWithEncryptionScheme:(PKEncryptionScheme)encryptionScheme NS_DESIGNATED_INITIALIZER;
 
-@property (nonatomic, copy, readonly) NSString *encryptionScheme;
+@property (nonatomic, copy, readonly) PKEncryptionScheme encryptionScheme;
 
 /* Display Properties:
  *  At least one of cardholder name or primary account suffix must be supplied.
@@ -43,7 +44,7 @@
 
 /* Filters introduction page to a specific network - does not function as a restriction.
  */
-@property (nonatomic, copy, nullable) NSString *paymentNetwork;
+@property (nonatomic, copy, nullable) PKPaymentNetwork paymentNetwork;
 
 @end
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentMethod.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentMethod.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentMethod.h	2016-06-29 07:17:01.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentMethod.h	2016-07-11 07:57:39.000000000 +0200
@@ -8,6 +8,7 @@
 #define __PKPAYMENTMETHOD_H
 
 #import <Foundation/Foundation.h>
+#import <PassKit/PKConstants.h>
 
 @class PKPaymentPass;
 
@@ -15,7 +16,7 @@
 NS_CLASS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(3.0)
 @interface PKPaymentMethod : NSObject
 
-typedef NS_OPTIONS(NSUInteger, PKPaymentMethodType) {
+typedef NS_ENUM(NSUInteger, PKPaymentMethodType) {
     PKPaymentMethodTypeUnknown = 0,
     PKPaymentMethodTypeDebit,
     PKPaymentMethodTypeCredit,
@@ -27,7 +28,7 @@
 @property (nonatomic, copy, readonly, nullable) NSString *displayName;
 
 // The payment network that backs the instrument. Suitable for display.
-@property (nonatomic, copy, readonly, nullable) NSString *network;
+@property (nonatomic, copy, readonly, nullable) PKPaymentNetwork network;
 
 // The underlying instrument type (Credit, Debit, etc)
 @property (nonatomic, readonly) PKPaymentMethodType type;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentRequest.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentRequest.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentRequest.h	2016-06-28 08:26:53.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentRequest.h	2016-07-11 07:57:39.000000000 +0200
@@ -5,6 +5,7 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <PassKit/PKConstants.h>
 
 #if TARGET_OS_IOS
 #import <AddressBook/ABRecord.h>

```