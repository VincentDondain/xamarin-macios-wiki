#LocalAuthentication.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h	2016-05-26 07:42:49.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h	2016-06-29 07:12:15.000000000 +0200
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
```