#Security.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccessControl.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccessControl.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccessControl.h	2016-05-24 06:55:31.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccessControl.h	2016-06-26 08:40:19.000000000 +0200
@@ -48,13 +48,13 @@
 
 typedef CF_OPTIONS(CFOptionFlags, SecAccessControlCreateFlags) {
     kSecAccessControlUserPresence           = 1 << 0,                                 // User presence policy using Touch ID or Passcode. Touch ID does not have to be available or enrolled. Item is still accessible by Touch ID even if fingers are added or removed.
-    kSecAccessControlTouchIDAny             CF_ENUM_AVAILABLE(NA, 9_0)    = 1 << 1,   // Constraint: Touch ID (any finger). Touch ID must be available and at least one finger must be enrolled. Item is still accessible by Touch ID even if fingers are added or removed.
-    kSecAccessControlTouchIDCurrentSet      CF_ENUM_AVAILABLE(NA, 9_0)    = 1 << 3,   // Constraint: Touch ID from the set of currently enrolled fingers. Touch ID must be available and at least one finger must be enrolled. When fingers are added or removed, the item is invalidated.
-    kSecAccessControlDevicePasscode         CF_ENUM_AVAILABLE(10_11, 9_0) = 1 << 4,   // Constraint: Device passcode
-    kSecAccessControlOr                     CF_ENUM_AVAILABLE(NA, 9_0)    = 1 << 14,  // Constraint logic operation: when using more than one constraint, at least one of them must be satisfied.
-    kSecAccessControlAnd                    CF_ENUM_AVAILABLE(NA, 9_0)    = 1 << 15,  // Constraint logic operation: when using more than one constraint, all must be satisfied.
-    kSecAccessControlPrivateKeyUsage        CF_ENUM_AVAILABLE(NA, 9_0)    = 1 << 30,  // Create access control for private key operations (i.e. sign operation)
-    kSecAccessControlApplicationPassword    CF_ENUM_AVAILABLE(NA, 9_0)    = 1 << 31,  // Security: Application provided password for data encryption key generation. This is not a constraint but additional item encryption mechanism.
+    kSecAccessControlTouchIDAny             CF_ENUM_AVAILABLE(NA, 9_0)    = 1u << 1,   // Constraint: Touch ID (any finger). Touch ID must be available and at least one finger must be enrolled. Item is still accessible by Touch ID even if fingers are added or removed.
+    kSecAccessControlTouchIDCurrentSet      CF_ENUM_AVAILABLE(NA, 9_0)    = 1u << 3,   // Constraint: Touch ID from the set of currently enrolled fingers. Touch ID must be available and at least one finger must be enrolled. When fingers are added or removed, the item is invalidated.
+    kSecAccessControlDevicePasscode         CF_ENUM_AVAILABLE(10_11, 9_0) = 1u << 4,   // Constraint: Device passcode
+    kSecAccessControlOr                     CF_ENUM_AVAILABLE(NA, 9_0)    = 1u << 14,  // Constraint logic operation: when using more than one constraint, at least one of them must be satisfied.
+    kSecAccessControlAnd                    CF_ENUM_AVAILABLE(NA, 9_0)    = 1u << 15,  // Constraint logic operation: when using more than one constraint, all must be satisfied.
+    kSecAccessControlPrivateKeyUsage        CF_ENUM_AVAILABLE(NA, 9_0)    = 1u << 30,  // Create access control for private key operations (i.e. sign operation)
+    kSecAccessControlApplicationPassword    CF_ENUM_AVAILABLE(NA, 9_0)    = 1u << 31,  // Security: Application provided password for data encryption key generation. This is not a constraint but additional item encryption mechanism.
 } __OSX_AVAILABLE_STARTING(__MAC_10_10, __IPHONE_8_0);
 
 /*!
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecKey.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecKey.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecKey.h	2016-05-24 06:55:25.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecKey.h	2016-06-26 07:35:40.000000000 +0200
@@ -422,6 +422,11 @@
 	@constant kSecKeyAlgorithmRSASignatureRaw
 	Raw RSA sign/verify operation, size of input data must be the same as value returned by SecKeyGetBlockSize().
 
+ 	@constant kSecKeyAlgorithmRSASignatureDigestPKCS1v15Raw
+ 	RSA sign/verify operation, assumes that input data is digest and OID and digest algorithm as specified in PKCS# v1.5.
+	This algorithm is typically not used directly, instead use algorithm with specified digest, like
+ 	kSecKeyAlgorithmRSASignatureDigestPKCS1v15SHA256.
+
 	@constant kSecKeyAlgorithmRSASignatureDigestPKCS1v15SHA1
 	RSA signature with PKCS#1 padding, input data must be SHA-1 generated digest.
 
@@ -504,27 +509,127 @@
 	@constant kSecKeyAlgorithmRSAEncryptionOAEPSHA1
 	RSA encryption or decryption, data is padded using OAEP padding scheme internally using SHA1. Input data must be at most
 	"key block size - 42" bytes long and returned block has always the same size as block size, as returned
-	by SecKeyGetBlockSize().
+	by SecKeyGetBlockSize().  Use kSecKeyAlgorithmRSAEncryptionOAEPSHA1AESGCM to be able to encrypt and decrypt arbitrary long data.
 
 	@constant kSecKeyAlgorithmRSAEncryptionOAEPSHA224
 	RSA encryption or decryption, data is padded using OAEP padding scheme internally using SHA224. Input data must be at most
 	"key block size - 58" bytes long and returned block has always the same size as block size, as returned
-	by SecKeyGetBlockSize().
+	by SecKeyGetBlockSize().  Use kSecKeyAlgorithmRSAEncryptionOAEPSHA224AESGCM to be able to encrypt and decrypt arbitrary long data.
 
 	@constant kSecKeyAlgorithmRSAEncryptionOAEPSHA256
 	RSA encryption or decryption, data is padded using OAEP padding scheme internally using SHA256. Input data must be at most
 	"key block size - 66" bytes long and returned block has always the same size as block size, as returned
-	by SecKeyGetBlockSize().
+	by SecKeyGetBlockSize().  Use kSecKeyAlgorithmRSAEncryptionOAEPSHA256AESGCM to be able to encrypt and decrypt arbitrary long data.
 
 	@constant kSecKeyAlgorithmRSAEncryptionOAEPSHA384
 	RSA encryption or decryption, data is padded using OAEP padding scheme internally using SHA384. Input data must be at most
 	"key block size - 98" bytes long and returned block has always the same size as block size, as returned
-	by SecKeyGetBlockSize().
+	by SecKeyGetBlockSize().  Use kSecKeyAlgorithmRSAEncryptionOAEPSHA384AESGCM to be able to encrypt and decrypt arbitrary long data.
 
 	@constant kSecKeyAlgorithmRSAEncryptionOAEPSHA512
 	RSA encryption or decryption, data is padded using OAEP padding scheme internally using SHA512. Input data must be at most
 	"key block size - 130" bytes long and returned block has always the same size as block size, as returned
-	by SecKeyGetBlockSize().
+	by SecKeyGetBlockSize().  Use kSecKeyAlgorithmRSAEncryptionOAEPSHA512AESGCM to be able to encrypt and decrypt arbitrary long data.
+
+	@constant kSecKeyAlgorithmRSAEncryptionOAEPSHA1AESGCM
+ 	Randomly generated AES session key is encrypted by RSA with OAEP padding.  User data are encrypted using session key in GCM
+ 	mode with all-zero 16 bytes long IV (initialization vector).  Finally 16 byte AES-GCM tag is appended to ciphertext.
+	256bit AES key is used if RSA key is 4096bit or bigger, otherwise 128bit AES key is used.  Raw public key data is used
+ 	as authentication data for AES-GCM encryption.
+
+	@constant kSecKeyAlgorithmRSAEncryptionOAEPSHA224AESGCM
+ 	Randomly generated AES session key is encrypted by RSA with OAEP padding.  User data are encrypted using session key in GCM
+ 	mode with all-zero 16 bytes long IV (initialization vector).  Finally 16 byte AES-GCM tag is appended to ciphertext.
+	256bit AES key is used if RSA key is 4096bit or bigger, otherwise 128bit AES key is used.  Raw public key data is used
+ 	as authentication data for AES-GCM encryption.
+
+	@constant kSecKeyAlgorithmRSAEncryptionOAEPSHA256AESGCM
+ 	Randomly generated AES session key is encrypted by RSA with OAEP padding.  User data are encrypted using session key in GCM
+ 	mode with all-zero 16 bytes long IV (initialization vector).  Finally 16 byte AES-GCM tag is appended to ciphertext.
+	256bit AES key is used if RSA key is 4096bit or bigger, otherwise 128bit AES key is used.  Raw public key data is used
+ 	as authentication data for AES-GCM encryption.
+
+	@constant kSecKeyAlgorithmRSAEncryptionOAEPSHA384AESGCM
+ 	Randomly generated AES session key is encrypted by RSA with OAEP padding.  User data are encrypted using session key in GCM
+ 	mode with all-zero 16 bytes long IV (initialization vector).  Finally 16 byte AES-GCM tag is appended to ciphertext.
+	256bit AES key is used if RSA key is 4096bit or bigger, otherwise 128bit AES key is used.  Raw public key data is used
+ 	as authentication data for AES-GCM encryption.
+
+	@constant kSecKeyAlgorithmRSAEncryptionOAEPSHA512AESGCM
+ 	Randomly generated AES session key is encrypted by RSA with OAEP padding.  User data are encrypted using session key in GCM
+ 	mode with all-zero 16 bytes long IV (initialization vector).  Finally 16 byte AES-GCM tag is appended to ciphertext.
+	256bit AES key is used if RSA key is 4096bit or bigger, otherwise 128bit AES key is used.  Raw public key data is used
+ 	as authentication data for AES-GCM encryption.
+
+ 	@constant kSecKeyAlgorithmECIESEncryptionStandardX963SHA1AESGCM
+	ECIES encryption or decryption.  This algorithm does not limit the size of the message to be encrypted or decrypted.
+	Encryption is done using AES-GCM with key negotiated by kSecKeyAlgorithmECDHKeyExchangeStandardX963SHA1.  AES Key size
+	is 128bit for EC keys <=256bit and 256bit for bigger EC keys.  Ephemeral public key data is used as sharedInfo for KDF,
+	and static public key data is used as authenticationData for AES-GCM processing.  AES-GCM uses 16 bytes long TAG and
+ 	all-zero 16 byte long IV (initialization vector).
+
+ 	@constant kSecKeyAlgorithmECIESEncryptionStandardX963SHA224AESGCM
+	ECIES encryption or decryption.  This algorithm does not limit the size of the message to be encrypted or decrypted.
+	Encryption is done using AES-GCM with key negotiated by kSecKeyAlgorithmECDHKeyExchangeStandardX963SHA1.  AES Key size
+	is 128bit for EC keys <=256bit and 256bit for bigger EC keys.  Ephemeral public key data is used as sharedInfo for KDF,
+	and static public key data is used as authenticationData for AES-GCM processing.  AES-GCM uses 16 bytes long TAG and
+ 	all-zero 16 byte long IV (initialization vector).
+
+ 	@constant kSecKeyAlgorithmECIESEncryptionStandardX963SHA256AESGCM
+	ECIES encryption or decryption.  This algorithm does not limit the size of the message to be encrypted or decrypted.
+	Encryption is done using AES-GCM with key negotiated by kSecKeyAlgorithmECDHKeyExchangeStandardX963SHA1.  AES Key size
+	is 128bit for EC keys <=256bit and 256bit for bigger EC keys.  Ephemeral public key data is used as sharedInfo for KDF,
+	and static public key data is used as authenticationData for AES-GCM processing.  AES-GCM uses 16 bytes long TAG and
+ 	all-zero 16 byte long IV (initialization vector).
+
+ 	@constant kSecKeyAlgorithmECIESEncryptionStandardX963SHA384AESGCM
+	ECIES encryption or decryption.  This algorithm does not limit the size of the message to be encrypted or decrypted.
+	Encryption is done using AES-GCM with key negotiated by kSecKeyAlgorithmECDHKeyExchangeStandardX963SHA1.  AES Key size
+	is 128bit for EC keys <=256bit and 256bit for bigger EC keys.  Ephemeral public key data is used as sharedInfo for KDF,
+	and static public key data is used as authenticationData for AES-GCM processing.  AES-GCM uses 16 bytes long TAG and
+ 	all-zero 16 byte long IV (initialization vector).
+
+ 	@constant kSecKeyAlgorithmECIESEncryptionStandardX963SHA512AESGCM
+	ECIES encryption or decryption.  This algorithm does not limit the size of the message to be encrypted or decrypted.
+	Encryption is done using AES-GCM with key negotiated by kSecKeyAlgorithmECDHKeyExchangeStandardX963SHA1.  AES Key size
+	is 128bit for EC keys <=256bit and 256bit for bigger EC keys.  Ephemeral public key data is used as sharedInfo for KDF,
+	and static public key data is used as authenticationData for AES-GCM processing.  AES-GCM uses 16 bytes long TAG and
+ 	all-zero 16 byte long IV (initialization vector).
+
+ 	@constant kSecKeyAlgorithmECIESEncryptionCofactorX963SHA1AESGCM
+	ECIES encryption or decryption.  This algorithm does not limit the size of the message to be encrypted or decrypted.
+	Encryption is done using AES-GCM with key negotiated by kSecKeyAlgorithmECDHKeyExchangeCofactorX963SHA1.  AES Key size
+	is 128bit for EC keys <=256bit and 256bit for bigger EC keys.  Ephemeral public key data is used as sharedInfo for KDF,
+	and static public key data is used as authenticationData for AES-GCM processing.  AES-GCM uses 16 bytes long TAG and
+ 	all-zero 16 byte long IV (initialization vector).
+
+ 	@constant kSecKeyAlgorithmECIESEncryptionCofactorX963SHA224AESGCM
+	ECIES encryption or decryption.  This algorithm does not limit the size of the message to be encrypted or decrypted.
+	Encryption is done using AES-GCM with key negotiated by kSecKeyAlgorithmECDHKeyExchangeCofactorX963SHA1.  AES Key size
+	is 128bit for EC keys <=256bit and 256bit for bigger EC keys.  Ephemeral public key data is used as sharedInfo for KDF,
+	and static public key data is used as authenticationData for AES-GCM processing.  AES-GCM uses 16 bytes long TAG and
+ 	all-zero 16 byte long IV (initialization vector).
+
+ 	@constant kSecKeyAlgorithmECIESEncryptionCofactorX963SHA256AESGCM
+	ECIES encryption or decryption.  This algorithm does not limit the size of the message to be encrypted or decrypted.
+	Encryption is done using AES-GCM with key negotiated by kSecKeyAlgorithmECDHKeyExchangeCofactorX963SHA1.  AES Key size
+	is 128bit for EC keys <=256bit and 256bit for bigger EC keys.  Ephemeral public key data is used as sharedInfo for KDF,
+	and static public key data is used as authenticationData for AES-GCM processing.  AES-GCM uses 16 bytes long TAG and
+ 	all-zero 16 byte long IV (initialization vector).
+
+ 	@constant kSecKeyAlgorithmECIESEncryptionCofactorX963SHA384AESGCM
+	ECIES encryption or decryption.  This algorithm does not limit the size of the message to be encrypted or decrypted.
+	Encryption is done using AES-GCM with key negotiated by kSecKeyAlgorithmECDHKeyExchangeCofactorX963SHA1.  AES Key size
+	is 128bit for EC keys <=256bit and 256bit for bigger EC keys.  Ephemeral public key data is used as sharedInfo for KDF,
+	and static public key data is used as authenticationData for AES-GCM processing.  AES-GCM uses 16 bytes long TAG and
+ 	all-zero 16 byte long IV (initialization vector).
+
+ 	@constant kSecKeyAlgorithmECIESEncryptionCofactorX963SHA512AESGCM
+	ECIES encryption or decryption.  This algorithm does not limit the size of the message to be encrypted or decrypted.
+	Encryption is done using AES-GCM with key negotiated by kSecKeyAlgorithmECDHKeyExchangeCofactorX963SHA1.  AES Key size
+	is 128bit for EC keys <=256bit and 256bit for bigger EC keys.  Ephemeral public key data is used as sharedInfo for KDF,
+	and static public key data is used as authenticationData for AES-GCM processing.  AES-GCM uses 16 bytes long TAG and
+ 	all-zero 16 byte long IV (initialization vector).
 
 	@constant kSecKeyAlgorithmECDHKeyExchangeCofactor
 	Compute shared secret using ECDH cofactor algorithm, suitable only for kSecAttrKeyTypeECSECPrimeRandom keys.
@@ -591,6 +696,9 @@
 extern const SecKeyAlgorithm kSecKeyAlgorithmRSASignatureRaw
 __OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
 
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSASignatureDigestPKCS1v15Raw
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
 extern const SecKeyAlgorithm kSecKeyAlgorithmRSASignatureDigestPKCS1v15SHA1
 __OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
 extern const SecKeyAlgorithm kSecKeyAlgorithmRSASignatureDigestPKCS1v15SHA224
@@ -655,6 +763,39 @@
 extern const SecKeyAlgorithm kSecKeyAlgorithmRSAEncryptionOAEPSHA512
 __OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
 
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSAEncryptionOAEPSHA1AESGCM
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSAEncryptionOAEPSHA224AESGCM
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSAEncryptionOAEPSHA256AESGCM
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSAEncryptionOAEPSHA384AESGCM
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSAEncryptionOAEPSHA512AESGCM
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+extern const SecKeyAlgorithm kSecKeyAlgorithmECIESEncryptionStandardX963SHA1AESGCM
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECIESEncryptionStandardX963SHA224AESGCM
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECIESEncryptionStandardX963SHA256AESGCM
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECIESEncryptionStandardX963SHA384AESGCM
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECIESEncryptionStandardX963SHA512AESGCM
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+extern const SecKeyAlgorithm kSecKeyAlgorithmECIESEncryptionCofactorX963SHA1AESGCM
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECIESEncryptionCofactorX963SHA224AESGCM
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECIESEncryptionCofactorX963SHA256AESGCM
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECIESEncryptionCofactorX963SHA384AESGCM
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECIESEncryptionCofactorX963SHA512AESGCM
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
 extern const SecKeyAlgorithm kSecKeyAlgorithmECDHKeyExchangeStandard
 __OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
 extern const SecKeyAlgorithm kSecKeyAlgorithmECDHKeyExchangeStandardX963SHA1
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecPolicy.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecPolicy.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecPolicy.h	2016-05-24 06:43:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecPolicy.h	2016-06-26 07:28:51.000000000 +0200
@@ -164,7 +164,6 @@
     @result A policy object. The caller is responsible for calling CFRelease
     on this when it is no longer needed.
 */
-__nullable
 SecPolicyRef SecPolicyCreateBasicX509(void)
 	__OSX_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_2_0);
 
@@ -178,7 +177,6 @@
     @result A policy object. The caller is responsible for calling CFRelease
     on this when it is no longer needed.
 */
-__nullable
 SecPolicyRef SecPolicyCreateSSL(Boolean server, CFStringRef __nullable hostname)
 	__OSX_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_2_0);
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecTrust.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecTrust.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecTrust.h	2016-05-23 06:50:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecTrust.h	2016-06-26 08:34:59.000000000 +0200
@@ -448,8 +448,9 @@
     @abstract Set a trust cookie to be used for evaluating this certificate chain.
     @param trust A reference to a trust object.
     @param exceptions An exceptions cookie as returned by a call to
-    SecTrustCopyExceptions() in the past.
-    @result Upon calling SecTrustEvaluate(), any failures that where present at the
+    SecTrustCopyExceptions() in the past.  You may pass NULL to clear any
+    exceptions which have been previously set on this trust reference.
+    @result Upon calling SecTrustEvaluate(), any failures that were present at the
     time the exceptions object was created are ignored, and instead of returning
     kSecTrustResultRecoverableTrustFailure, kSecTrustResultProceed will be returned
     (if the certificate for which exceptions was created matches the current leaf
@@ -466,7 +467,7 @@
     of the wireless network for which this cert is needed, the account for which
     this cert should be considered valid, and so on.
  */
-bool SecTrustSetExceptions(SecTrustRef trust, CFDataRef exceptions)
+bool SecTrustSetExceptions(SecTrustRef trust, CFDataRef __nullable exceptions)
     __OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_4_0);
 
 /*!
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecureTransport.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecureTransport.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecureTransport.h	2016-05-24 07:00:20.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecureTransport.h	2016-06-26 07:34:08.000000000 +0200
@@ -329,6 +329,8 @@
 extern const CFStringRef kSSLSessionConfig_legacy;
 /* TLS v1.2 to TLS v1.0, defaults + RC4 + DHE ciphersuites */
 extern const CFStringRef kSSLSessionConfig_legacy_DHE;
+/* TLS v1.2, anonymous ciphersuites only */
+extern const CFStringRef kSSLSessionConfig_anonymous;
 
 
 /******************
@@ -616,7 +618,7 @@
  */
 OSStatus
 SSLSetCertificate			(SSLContextRef		context,
-							 CFArrayRef			certRefs)
+							 CFArrayRef			_Nullable certRefs)
 	__OSX_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_5_0);
 
 /*
@@ -669,6 +671,25 @@
 							 size_t				*peerNameLen)	// IN/OUT
 	__OSX_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_5_0);
 
+
+/*
+ * Determine the buffer size needed for SSLCopyRequestedPeerNameLength().
+ */
+OSStatus
+SSLCopyRequestedPeerName    (SSLContextRef      context,
+                             char               *peerName,
+                             size_t             *peerNameLen)
+    __OSX_AVAILABLE_STARTING(__MAC_10_11, __IPHONE_9_0);
+
+/*
+ * Server Only: obtain the hostname specified by the client in the ServerName extension (SNI)
+ */
+OSStatus
+SSLCopyRequestedPeerNameLength  (SSLContextRef  ctx,
+                                 size_t         *peerNameLen)
+    __OSX_AVAILABLE_STARTING(__MAC_10_11, __IPHONE_9_0);
+
+
 /*
  * Specify the Datagram TLS Hello Cookie.
  * This is to be called for server side only and is optional.

```