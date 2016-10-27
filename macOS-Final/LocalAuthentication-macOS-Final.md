#LocalAuthentication.framework

``` diff
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h	2016-08-12 23:13:29.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h	2016-10-09 19:47:29.000000000 -0400
@@ -27,7 +27,7 @@
     ///
     ///             Biometric authentication will get locked after 5 unsuccessful attempts. After that,
     ///             users have to unlock it by entering passcode.
-    LAPolicyDeviceOwnerAuthenticationWithBiometrics NS_ENUM_AVAILABLE(NA, 8_0) __WATCHOS_AVAILABLE(3.0) __TVOS_AVAILABLE(10.0) = kLAPolicyDeviceOwnerAuthenticationWithBiometrics,
+    LAPolicyDeviceOwnerAuthenticationWithBiometrics NS_ENUM_AVAILABLE(10_12, 8_0) __WATCHOS_AVAILABLE(3.0) __TVOS_AVAILABLE(10.0) = kLAPolicyDeviceOwnerAuthenticationWithBiometrics,
 
     /// Device owner was authenticated by Touch ID or device passcode.
     ///
@@ -47,7 +47,7 @@
 } NS_ENUM_AVAILABLE(10_10, 8_0) __WATCHOS_AVAILABLE(3.0) __TVOS_AVAILABLE(10.0);
 
 /// The maximum value for LAContext touchIDAuthenticationAllowableReuseDuration property.
-extern const NSTimeInterval LATouchIDAuthenticationMaximumAllowableReuseDuration NS_AVAILABLE(NA, 9_0) __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
+extern const NSTimeInterval LATouchIDAuthenticationMaximumAllowableReuseDuration NS_AVAILABLE(10_12, 9_0) __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
 
 /// Class that represents an authentication context.
 ///
@@ -106,8 +106,8 @@
 ///
 /// @param localizedReason Application reason for authentication. This string must be provided in correct
 ///                        localization and should be short and clear. It will be eventually displayed in
-///                        the authentication dialog subtitle. A name of the calling application will be
-///                        already displayed in title, so it should not be duplicated here.
+///                        the authentication dialog. A name of the calling application will be already
+///                        displayed in title, so it should not be duplicated here.
 ///
 /// @warning localizedReason parameter is mandatory and the call will throw NSInvalidArgumentException if
 ///          nil or empty string is specified.
@@ -217,8 +217,8 @@
 ///
 /// @param localizedReason Application reason for authentication. This string must be provided in correct
 ///                        localization and should be short and clear. It will be eventually displayed in
-///                        the authentication dialog subtitle. A name of the calling application will be
-///                        already displayed in title, so it should not be duplicated here.
+///                        the authentication dialog. A name of the calling application will be already
+///                        displayed in title, so it should not be duplicated here.
 ///
 /// @param reply Reply block that is executed when access control evaluation finishes.
 ///              success Reply parameter that is YES if the access control has been evaluated successfully or
@@ -282,7 +282,7 @@
 ///             the accepted interval.
 ///
 /// @see LATouchIDAuthenticationMaximumAllowableReuseDuration
-@property (nonatomic) NSTimeInterval touchIDAuthenticationAllowableReuseDuration NS_AVAILABLE(NA, 9_0) __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
+@property (nonatomic) NSTimeInterval touchIDAuthenticationAllowableReuseDuration NS_AVAILABLE(10_12, 9_0) __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
 
 @end
 

```