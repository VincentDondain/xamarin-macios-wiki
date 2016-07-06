#LocalAuthentication.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h	2016-05-26 07:42:49.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h	2016-06-29 07:12:15.000000000 +0200
@@ -183,8 +183,14 @@
     /// Access control will be used for key creation.
     LAAccessControlOperationCreateKey,
 
-    /// Access control will be used for accessing existing key.
-    LAAccessControlOperationUseKeySign
+    /// Access control will be used for sign operation with existing key.
+    LAAccessControlOperationUseKeySign,
+    
+    /// Access control will be used for data decryption using existing key.
+    LAAccessControlOperationUseKeyDecrypt NS_ENUM_AVAILABLE(10_12, 10_0),
+
+    /// Access control will be used for key exchange.
+    LAAccessControlOperationUseKeyKeyExchange NS_ENUM_AVAILABLE(10_12, 10_0),
 } NS_ENUM_AVAILABLE(10_11, 9_0) __WATCHOS_AVAILABLE(3.0) __TVOS_AVAILABLE(10.0);
 
 /// Evaluates access control object for the specified operation.
@@ -263,13 +269,16 @@
 ///              will reveal the fact database was changed between calls.
 @property (nonatomic, nullable, readonly) NSData *evaluatedPolicyDomainState NS_AVAILABLE(10_11, 9_0) __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
 
-/// Time interval for accepting a successful Touch ID unlock from the past.
+/// Time interval for accepting a successful Touch ID device unlock (on the lock screen) from the past.
 ///
 /// @discussion This property can be set with a time interval in seconds. If the device was successfully unlocked by
 ///             Touch ID within this time interval, then Touch ID authentication on this context will succeed
 ///             automatically and the reply block will be called without prompting user for Touch ID.
 ///
-///             The default value is 0, meaning that no previous TouchID authentication can be reused.
+///             The default value is 0, meaning that no previous TouchID unlock can be reused.
+///
+///             This property is meant only for reusing Touch ID matches from the device lock screen.
+///             It does not allow reusing previous Touch ID matches in application or between applications.
 ///
 ///             The maximum supported interval is 5 minutes and setting the value beyond 5 minutes does not increase
 ///             the accepted interval.

```