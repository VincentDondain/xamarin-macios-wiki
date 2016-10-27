#Security.framework

``` diff
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccessControl.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccessControl.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccessControl.h	2016-09-26 22:04:01.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccessControl.h	2016-10-09 19:29:38.000000000 -0400
@@ -48,13 +48,13 @@
 
 typedef CF_OPTIONS(CFOptionFlags, SecAccessControlCreateFlags) {
     kSecAccessControlUserPresence           = 1 << 0,                                 // User presence policy using Touch ID or Passcode. Touch ID does not have to be available or enrolled. Item is still accessible by Touch ID even if fingers are added or removed.
-    kSecAccessControlTouchIDAny             CF_ENUM_AVAILABLE(NA, 9_0)    = 1u << 1,   // Constraint: Touch ID (any finger). Touch ID must be available and at least one finger must be enrolled. Item is still accessible by Touch ID even if fingers are added or removed.
-    kSecAccessControlTouchIDCurrentSet      CF_ENUM_AVAILABLE(NA, 9_0)    = 1u << 3,   // Constraint: Touch ID from the set of currently enrolled fingers. Touch ID must be available and at least one finger must be enrolled. When fingers are added or removed, the item is invalidated.
+    kSecAccessControlTouchIDAny             CF_ENUM_AVAILABLE(10_12, 9_0) = 1u << 1,   // Constraint: Touch ID (any finger). Touch ID must be available and at least one finger must be enrolled. Item is still accessible by Touch ID even if fingers are added or removed.
+    kSecAccessControlTouchIDCurrentSet      CF_ENUM_AVAILABLE(10_12, 9_0) = 1u << 3,   // Constraint: Touch ID from the set of currently enrolled fingers. Touch ID must be available and at least one finger must be enrolled. When fingers are added or removed, the item is invalidated.
     kSecAccessControlDevicePasscode         CF_ENUM_AVAILABLE(10_11, 9_0) = 1u << 4,   // Constraint: Device passcode
-    kSecAccessControlOr                     CF_ENUM_AVAILABLE(NA, 9_0)    = 1u << 14,  // Constraint logic operation: when using more than one constraint, at least one of them must be satisfied.
-    kSecAccessControlAnd                    CF_ENUM_AVAILABLE(NA, 9_0)    = 1u << 15,  // Constraint logic operation: when using more than one constraint, all must be satisfied.
-    kSecAccessControlPrivateKeyUsage        CF_ENUM_AVAILABLE(NA, 9_0)    = 1u << 30,  // Create access control for private key operations (i.e. sign operation)
-    kSecAccessControlApplicationPassword    CF_ENUM_AVAILABLE(NA, 9_0)    = 1u << 31,  // Security: Application provided password for data encryption key generation. This is not a constraint but additional item encryption mechanism.
+    kSecAccessControlOr                     CF_ENUM_AVAILABLE(10_12, 9_0) = 1u << 14,  // Constraint logic operation: when using more than one constraint, at least one of them must be satisfied.
+    kSecAccessControlAnd                    CF_ENUM_AVAILABLE(10_12, 9_0) = 1u << 15,  // Constraint logic operation: when using more than one constraint, all must be satisfied.
+    kSecAccessControlPrivateKeyUsage        CF_ENUM_AVAILABLE(10_12, 9_0) = 1u << 30,  // Create access control for private key operations (i.e. sign operation)
+    kSecAccessControlApplicationPassword    CF_ENUM_AVAILABLE(10_12, 9_0) = 1u << 31,  // Security: Application provided password for data encryption key generation. This is not a constraint but additional item encryption mechanism.
 } __OSX_AVAILABLE_STARTING(__MAC_10_10, __IPHONE_8_0);
 
 /*!
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecItem.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecItem.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecItem.h	2016-08-15 21:12:23.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecItem.h	2016-10-09 19:29:38.000000000 -0400
@@ -1015,6 +1015,22 @@
 	__OSX_AVAILABLE_STARTING(__MAC_10_11, __IPHONE_9_0);
 
 /*!
+     @enum kSecAttrTokenID Value Constants
+     @discussion Predefined item attribute constant used to get or set values
+         in a dictionary. The kSecAttrTokenID constant is the key and its value
+         can be kSecAttrTokenIDSecureEnclave.
+     @constant kSecAttrTokenIDSecureEnclave Specifies well-known identifier of the
+         token implemented using device's Secure Enclave. The only keychain items
+         supported by the Secure Enclave token are 256-bit elliptic curve keys
+         (kSecAttrKeyTypeEC).  Keys must be generated on the secure enclave using
+         SecKeyGenerateKeyPair call with kSecAttrTokenID set to
+         kSecAttrTokenIDSecureEnclave in the parameters dictionary, it is not
+         possible to import pregenerated keys to kSecAttrTokenIDSecureEnclave token.
+*/
+extern const CFStringRef kSecAttrTokenIDSecureEnclave
+    __OSX_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_9_0);
+
+/*!
      @enum kSecAttrAccessGroup Value Constants
      @constant kSecAttrAccessGroupToken Represents well-known access group
          which contains items provided by external token (typically smart card).

```