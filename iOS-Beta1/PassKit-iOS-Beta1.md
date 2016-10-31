#PassKit.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPassLibrary.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPassLibrary.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPassLibrary.h	2016-10-06 08:46:25.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PassKit.framework/Headers/PKPassLibrary.h	2016-10-24 06:10:30.000000000 +0200
@@ -82,7 +82,7 @@
 - (BOOL)canAddPaymentPassWithPrimaryAccountIdentifier:(NSString *)primaryAccountIdentifier NS_AVAILABLE_IOS(9_0);
 
 // If the library can add Felica passes, this method will return YES. Otherwise, NO will be returned.
-- (BOOL)canAddFelicaPass NS_AVAILABLE_IOS(10_1);
+- (BOOL)canAddFelicaPass NS_AVAILABLE_IOS(10_1) __WATCHOS_AVAILABLE(3.1);
 
 // These methods may be utilized to activate a payment pass that is provisioned but currently in the inactive state, by providing
 // either a cryptographic OTP, or an activation code.

```