#PassKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentMethod.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentMethod.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentMethod.h	2016-06-28 06:15:58.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentMethod.h	2016-07-10 13:14:00.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentRequest.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentRequest.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentRequest.h	2016-06-28 08:26:53.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPaymentRequest.h	2016-07-11 07:57:39.000000000 +0200
@@ -5,6 +5,7 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <PassKit/PKConstants.h>
 
 #if TARGET_OS_IOS
 #import <AddressBook/ABRecord.h>

```