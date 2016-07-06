#LocalAuthentication.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h	2015-10-03 04:22:14.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h	2016-05-26 07:42:49.000000000 +0200
@@ -18,7 +18,8 @@
     ///             policy evaluation will fail. If Touch ID is locked out, passcode is required as
     ///             the first step to unlock the Touch ID.
     ///
-    ///             Touch ID authentication dialog contains a cancel button and a fallback button with
+    ///             Touch ID authentication dialog contains a cancel button with default title "Cancel"
+    ///             which can be customized using localizedCancelTitle property and a fallback button with
     ///             default title "Enter Password" which can be customized using localizedFallbackTitle
     ///             property. Fallback button is initially hidden and shows up after first unsuccessful
     ///             Touch ID attempt. Tapping cancel button or fallback button causes evaluatePolicy call
@@ -26,7 +27,7 @@
     ///
     ///             Biometric authentication will get locked after 5 unsuccessful attempts. After that,
     ///             users have to unlock it by entering passcode.
-    LAPolicyDeviceOwnerAuthenticationWithBiometrics NS_ENUM_AVAILABLE(NA, 8_0) = kLAPolicyDeviceOwnerAuthenticationWithBiometrics,
+    LAPolicyDeviceOwnerAuthenticationWithBiometrics NS_ENUM_AVAILABLE(NA, 8_0) __WATCHOS_AVAILABLE(3.0) __TVOS_AVAILABLE(10.0) = kLAPolicyDeviceOwnerAuthenticationWithBiometrics,
 
     /// Device owner was authenticated by Touch ID or device passcode.
     ///
@@ -43,17 +44,17 @@
     ///             increased backoff delay.
     LAPolicyDeviceOwnerAuthentication NS_ENUM_AVAILABLE(10_11, 9_0) = kLAPolicyDeviceOwnerAuthentication
 
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} NS_ENUM_AVAILABLE(10_10, 8_0) __WATCHOS_AVAILABLE(3.0) __TVOS_AVAILABLE(10.0);
 
 /// The maximum value for LAContext touchIDAuthenticationAllowableReuseDuration property.
-extern const NSTimeInterval LATouchIDAuthenticationMaximumAllowableReuseDuration NS_AVAILABLE_IOS(9_0);
+extern const NSTimeInterval LATouchIDAuthenticationMaximumAllowableReuseDuration NS_AVAILABLE(NA, 9_0) __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
 
 /// Class that represents an authentication context.
 ///
 /// @discussion This context can be used for evaluating policies.
 ///
 /// @see LAPolicy
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_10, 8_0) __WATCHOS_AVAILABLE(3.0) __TVOS_AVAILABLE(10.0)
 @interface LAContext : NSObject
 
 /// Determines if a particular policy can be evaluated.
@@ -145,8 +146,8 @@
     ///             LocalAuthentication will not show password entry user interface.
     ///             When entered from the LocalAuthentication user interface, the password is stored as
     ///             UTF-8 encoded string.
-    LACredentialTypeApplicationPassword = 0,
-} NS_ENUM_AVAILABLE(10_11, 9_0);
+    LACredentialTypeApplicationPassword __TVOS_UNAVAILABLE = 0,
+} NS_ENUM_AVAILABLE(10_11, 9_0) __WATCHOS_AVAILABLE(3.0) __TVOS_AVAILABLE(10.0);
 
 /// Sets a credential to this context.
 ///
@@ -161,7 +162,7 @@
 /// @return YES if the credential was set successfully, NO otherwise.
 ///
 - (BOOL)setCredential:(nullable NSData *)credential
-                type:(LACredentialType)type NS_AVAILABLE(10_11, 9_0);
+                 type:(LACredentialType)type NS_AVAILABLE(10_11, 9_0) __WATCHOS_AVAILABLE(3.0) __TVOS_UNAVAILABLE;
 
 /// Reveals if credential was set with this context.
 ///
@@ -169,7 +170,7 @@
 ///
 /// @return YES on success, NO otherwise.
 ///
-- (BOOL)isCredentialSet:(LACredentialType)type NS_AVAILABLE(10_11, 9_0);
+- (BOOL)isCredentialSet:(LACredentialType)type NS_AVAILABLE(10_11, 9_0) __WATCHOS_AVAILABLE(3.0) __TVOS_UNAVAILABLE;
 
 typedef NS_ENUM(NSInteger, LAAccessControlOperation)
 {
@@ -184,7 +185,7 @@
 
     /// Access control will be used for accessing existing key.
     LAAccessControlOperationUseKeySign
-} NS_ENUM_AVAILABLE(10_11, 9_0);
+} NS_ENUM_AVAILABLE(10_11, 9_0) __WATCHOS_AVAILABLE(3.0) __TVOS_AVAILABLE(10.0);
 
 /// Evaluates access control object for the specified operation.
 ///
@@ -229,13 +230,18 @@
                     operation:(LAAccessControlOperation)operation
               localizedReason:(NSString *)localizedReason
                         reply:(void(^)(BOOL success, NSError * __nullable error))reply
-                        NS_AVAILABLE(10_11, 9_0);
+                        NS_AVAILABLE(10_11, 9_0) __WATCHOS_AVAILABLE(3.0) __TVOS_UNAVAILABLE;
 
 /// Fallback button title.
 /// @discussion Allows fallback button title customization. A default title "Enter Password" is used when
 ///             this property is left nil. If set to empty string, the button will be hidden.
 @property (nonatomic, nullable, copy) NSString *localizedFallbackTitle;
 
+/// Cancel button title.
+/// @discussion Allows cancel button title customization. A default title "Cancel" is used when
+///             this property is left nil or is set to empty string.
+@property (nonatomic, nullable, copy) NSString *localizedCancelTitle NS_AVAILABLE(10_12, 10_0);
+
 /// Allows setting the limit for the number of failures during biometric authentication.
 ///
 /// @discussion When the specified limit is exceeded, evaluation of LAPolicyDeviceOwnerAuthenticationWithBiometrics
@@ -244,7 +250,7 @@
 ///
 /// @warning Please note that setting this property with high values does not prevent biometry lockout after 5
 ///          wrong attempts.
-@property (nonatomic, nullable) NSNumber *maxBiometryFailures NS_DEPRECATED_IOS(8_3, 9_0);
+@property (nonatomic, nullable) NSNumber *maxBiometryFailures NS_DEPRECATED_IOS(8_3, 9_0) __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
 
 /// Contains policy domain state.
 ///
@@ -255,7 +261,7 @@
 ///              data will change. Nature of such database changes cannot be determined
 ///              but comparing data of evaluatedPolicyDomainState after different evaluatePolicy
 ///              will reveal the fact database was changed between calls.
-@property (nonatomic, nullable, readonly) NSData *evaluatedPolicyDomainState NS_AVAILABLE(10_11, 9_0);
+@property (nonatomic, nullable, readonly) NSData *evaluatedPolicyDomainState NS_AVAILABLE(10_11, 9_0) __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
 
 /// Time interval for accepting a successful Touch ID unlock from the past.
 ///
@@ -269,7 +275,7 @@
 ///             the accepted interval.
 ///
 /// @see LATouchIDAuthenticationMaximumAllowableReuseDuration
-@property (nonatomic) NSTimeInterval touchIDAuthenticationAllowableReuseDuration NS_AVAILABLE_IOS(9_0);
+@property (nonatomic) NSTimeInterval touchIDAuthenticationAllowableReuseDuration NS_AVAILABLE(NA, 9_0) __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAError.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAError.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAError.h	2015-11-14 01:24:10.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAError.h	2016-05-26 07:42:49.000000000 +0200
@@ -29,12 +29,12 @@
     LAErrorTouchIDNotAvailable  = kLAErrorTouchIDNotAvailable,
     
     /// Authentication could not start, because Touch ID has no enrolled fingers.
-    LAErrorTouchIDNotEnrolled   = kLAErrorTouchIDNotEnrolled,
+    LAErrorTouchIDNotEnrolled = kLAErrorTouchIDNotEnrolled,
 
     /// Authentication was not successful, because there were too many failed Touch ID attempts and
     /// Touch ID is now locked. Passcode is required to unlock Touch ID, e.g. evaluating
     /// LAPolicyDeviceOwnerAuthenticationWithBiometrics will ask for passcode as a prerequisite.
-    LAErrorTouchIDLockout   NS_ENUM_AVAILABLE(10_11, 9_0) = kLAErrorTouchIDLockout,
+    LAErrorTouchIDLockout   NS_ENUM_AVAILABLE(10_11, 9_0) __WATCHOS_AVAILABLE(3.0) __TVOS_AVAILABLE(10.0) = kLAErrorTouchIDLockout,
 
     /// Authentication was canceled by application (e.g. invalidate was called while
     /// authentication was in progress).
@@ -42,7 +42,8 @@
 
     /// LAContext passed to this call has been previously invalidated.
     LAErrorInvalidContext   NS_ENUM_AVAILABLE(10_11, 9_0) = kLAErrorInvalidContext
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} NS_ENUM_AVAILABLE(10_10, 8_0) __WATCHOS_AVAILABLE(3.0) __TVOS_AVAILABLE(10.0);
 
 /// LocalAuthentication error domain.
-extern NSString *const __nonnull LAErrorDomain NS_AVAILABLE(10_10, 8_3);
+extern NSString *const __nonnull LAErrorDomain
+NS_AVAILABLE(10_10, 8_3) __WATCHOS_AVAILABLE(3.0) __TVOS_AVAILABLE(10.0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAPublicDefines.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAPublicDefines.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAPublicDefines.h	2015-10-03 04:22:14.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAPublicDefines.h	2016-05-26 07:42:49.000000000 +0200
@@ -16,6 +16,11 @@
 #define kLAOptionUserFallback                               1
 #define kLAOptionAuthenticationReason                       2
 
+// Credential types
+#define kLACredentialTypePasscode                          -1
+#define kLACredentialTypePassphrase                        -2
+#define kLACredentialCTKPIN                                -3
+
 // Error codes
 #define kLAErrorAuthenticationFailed                       -1
 #define kLAErrorUserCancel                                 -2

```