#Security.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/CSCommon.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/CSCommon.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/CSCommon.h	2016-05-26 06:38:47.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/CSCommon.h	2016-06-26 05:40:50.000000000 +0200
@@ -118,7 +118,9 @@
 	errSecCSNotAppLike =				-67002,	/* the code is valid but does not seem to be an app */
 	errSecCSBadDiskImageFormat =		-67001,	/* disk image format unrecognized, invalid, or unsuitable */
 	errSecCSUnsupportedDigestAlgorithm = -67000, /* signature digest algorithm(s) specified are not supported */
-	errSecCSInvalidAssociatedFileData =	-66999,	/* resource fork, finder information, or similar detritus not allowed */
+	errSecCSInvalidAssociatedFileData =	-66999,	/* resource fork, Finder information, or similar detritus not allowed */
+    errSecCSInvalidTeamIdentifier =     -66998, /* a Team Identifier string is invalid */
+    errSecCSBadTeamIdentifier =         -66997, /* a Team Identifier is wrong or inappropriate */
 };
 
 /*
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccessControl.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccessControl.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccessControl.h	2016-05-24 06:55:31.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccessControl.h	2016-06-26 08:40:19.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecKey.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecKey.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecKey.h	2016-05-26 06:38:47.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecKey.h	2016-06-26 05:40:50.000000000 +0200
@@ -721,6 +721,11 @@
 	@constant kSecKeyAlgorithmRSASignatureRaw
 	Raw RSA sign/verify operation, size of input data must be the same as value returned by SecKeyGetBlockSize().
 
+ 	@constant kSecKeyAlgorithmRSASignatureDigestPKCS1v15Raw
+ 	RSA sign/verify operation, assumes that input data is digest and OID and digest algorithm as specified in PKCS# v1.5.
+	This algorithm is typically not used directly, instead use algorithm with specified digest, like
+ 	kSecKeyAlgorithmRSASignatureDigestPKCS1v15SHA256.
+
 	@constant kSecKeyAlgorithmRSASignatureDigestPKCS1v15SHA1
 	RSA signature with PKCS#1 padding, input data must be SHA-1 generated digest.
 
@@ -803,27 +808,127 @@
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
@@ -890,6 +995,9 @@
 extern const SecKeyAlgorithm kSecKeyAlgorithmRSASignatureRaw
 __OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
 
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSASignatureDigestPKCS1v15Raw
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
 extern const SecKeyAlgorithm kSecKeyAlgorithmRSASignatureDigestPKCS1v15SHA1
 __OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
 extern const SecKeyAlgorithm kSecKeyAlgorithmRSASignatureDigestPKCS1v15SHA224
@@ -954,6 +1062,39 @@
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecPolicy.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecPolicy.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecPolicy.h	2016-05-26 06:38:47.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecPolicy.h	2016-06-26 05:40:50.000000000 +0200
@@ -165,7 +165,6 @@
  @result A policy object. The caller is responsible for calling CFRelease
  on this when it is no longer needed.
  */
-__nullable
 SecPolicyRef SecPolicyCreateBasicX509(void)
     __OSX_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_2_0);
 
@@ -179,7 +178,6 @@
  @result A policy object. The caller is responsible for calling CFRelease
  on this when it is no longer needed.
  */
-__nullable
 SecPolicyRef SecPolicyCreateSSL(Boolean server, CFStringRef __nullable hostname)
     __OSX_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_2_0);
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecTranslocate.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecTranslocate.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecTranslocate.h	2016-05-26 06:38:48.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecTranslocate.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,219 +0,0 @@
-/*
- * Copyright (c) 2016 Apple Inc. All Rights Reserved.
- *
- * @APPLE_LICENSE_HEADER_START@
- *
- * This file contains Original Code and/or Modifications of Original Code
- * as defined in and that are subject to the Apple Public Source License
- * Version 2.0 (the 'License'). You may not use this file except in
- * compliance with the License. Please obtain a copy of the License at
- * http://www.opensource.apple.com/apsl/ and read it before using this
- * file.
- *
- * The Original Code and all software distributed under the License are
- * distributed on an 'AS IS' basis, WITHOUT WARRANTY OF ANY KIND, EITHER
- * EXPRESS OR IMPLIED, AND APPLE HEREBY DISCLAIMS ALL SUCH WARRANTIES,
- * INCLUDING WITHOUT LIMITATION, ANY WARRANTIES OF MERCHANTABILITY,
- * FITNESS FOR A PARTICULAR PURPOSE, QUIET ENJOYMENT OR NON-INFRINGEMENT.
- * Please see the License for the specific language governing rights and
- * limitations under the License.
- *
- * @APPLE_LICENSE_HEADER_END@
- */
-
-#ifndef H_LIBSECURITY_TRANSLOCATE
-#define H_LIBSECURITY_TRANSLOCATE
-
-#include <CoreFoundation/CoreFoundation.h>
-
-CF_ASSUME_NONNULL_BEGIN
-
-#ifdef __cplusplus
-extern "C" {
-#endif
-
-/*!
-    @function SecTranslocateStartListening
-
-    @abstract Initialize the SecTranslocate Library as the XPC Server, Disk Arbitration Listener, and Launch Services Notification listener
-
-    @param error On error will be populated with an error object describing the failure (a posix domain error such as EINVAL)
-
-    @result True on success False on failure
- */
-Boolean SecTranslocateStartListening(CFErrorRef* __nullable error)
-__OSX_AVAILABLE(10.12);
-
-/*!
- @function SecTranslocateStartListeningWithOptions
-
- @abstract Initialize the SecTranslocate Library as the XPC Server, Disk Arbitration Listener, and Launch Services Notification listener
-
- @param option (currently unused) A dictionary of options that could impact server startup
- @param outError On error will be populated with an error object describing the failure (a posix domain error such as EINVAL)
-
- @result True on success False on failure
- */
-Boolean SecTranslocateStartListeningWithOptions(CFDictionaryRef options, CFErrorRef * __nullable outError)
-__OSX_AVAILABLE(10.12);
-
-/*!
-    @function SecTranslocateCreateSecureDirectoryForURL
- 
-    @abstract Create a CFURL pointing to a translocated location from which to access the directory specified by pathToTranslocate.
-
-    @param pathToTranslocate URL of the directory to be accessed from a translocated location.
-    @param destinationPath URL where the directory of interest should be translocated, or NULL for a random UUID location
-    @param error On error will be populated with an error object describing the failure (a posix domain error such as EINVAL)
-
-    @result A CFURL pointing to the translocated location of the directory.
-
-    @discussion 
-        Calls to this function and SecTranslocateDeleteSecureDirectory are serialized to ensure only one call to either
-        is operating at a time.
-        Translocations will be created in the calling users's DARWIN_USER_TEMPDIR/AppTranslocation/<UUID>
- 
-        pathToTranslocated is expected to be of the form /some/dir/myApp.app
-        destinationPath is expected to be of the form /<DARWIN_USER_TEMPDIR>/AppTranslocation/<DIR>/d/myApp.app
-        
-        Resulting translocations are of the form /<DARWIN_USER_TEMPDIR>/AppTranslocation/<DIR>/d/myApp.app
-            <DIR> will be a UUID if destinationPath isn't specified.
- 
-        If pathToTranslocate is in a quarantined mountpoint, the quarantine attributes will be propagated to the
-            translocated location.
- 
-        pathToTranslocate will cause a failure if it doesn't resolve to a path that exists, or it exceeds MAXPATHLEN
- 
-        destinationPath will cause a failure if
-            1. it doesn't match the app (last directory) specified by path to translocate
-            2. it differs from an already existing mount location for pathToTranslocate
-            3. It isn't in the user's current temp dir
-            4. someone created a file with the same name as the provided path
-            5. It doesn't match the form /<DARWIN_USER_TEMPDIR>/AppTranslocation/<DIR>/d/myApp.app
-
-        pathToTranslocate is returned if it should not be translocated based on policy. It is retained if so it can be treated as a copy.
-
-        This function can be run from any process. If the process is not the xpc server, then an xpc call is made.
- */
-CFURLRef __nullable SecTranslocateCreateSecureDirectoryForURL (CFURLRef pathToTranslocate, CFURLRef __nullable destinationPath, CFErrorRef* __nullable error)
-__OSX_AVAILABLE(10.12);
-
-/*!
-    @function SecTranslocateAppLaunchCheckin
-
-    @abstract Register that a translocated pid is running
-
-    @param pid the pid to register
-
-    @discussion this function will log if there is a problem. The actual work is either sent to the server via xpc, or dispatched async.
-
-        This function can be run from any process. If the process is not the xpc server, then an xpc call is made.
- */
-void SecTranslocateAppLaunchCheckin(pid_t pid)
-__OSX_AVAILABLE(10.12);
-
-/*!
-    @function SecTranslocateURLShouldRunTranslocated
-
-    @abstract Implements policy to decide whether the entity defined by path should be run translocated
-
-    @param path URL to the entity in question
-
-    @param shouldTranslocate true if the path should be translocated, false otherwise
-
-    @param error On error will be populated with an error object describing the failure (a posix domain error such as EINVAL)
-
-    @result true on success, false on failure (on failure error is set if provided). shouldTranslocate gives the answer
-
-    @discussion The policy is as follows:
-        1. If path is already on a nullfs mountpoint - no translocation
-        2. No quarantine attributes - no translocation
-        3. If QTN_FLAG_DO_NOT_TRANSLOCATE is set or QTN_FLAG_TRANSLOCATE is not set - no translocations
-        4. Otherwise, if QTN_FLAG_TRANSLOCATE is set - translocation
-
-        This function can be called from any process or thread.
- */
-Boolean SecTranslocateURLShouldRunTranslocated(CFURLRef path, bool* shouldTranslocate, CFErrorRef* __nullable error)
-__OSX_AVAILABLE(10.12);
-
-/*!
-    @function SecTranslocateIsTranslocatedURL
-
-    @abstract indicates whether the provided path is an original path or a translocated path (for the calling user)
-
-    @param path path to check
-
-    @param isTranslocated true if the path is translocated, false otherwise
-
-    @param error On error will be populated with an error object describing the failure (a posix domain error such as EINVAL)
-
-    @result true on success, false on failure (on failure error is set if provided). isTranslocated gives the answer
-
-    @discussion will return
-        1. false and EPERM if the caller doesn't have read access to the path
-        2. false and ENOENT if the path doesn't exist
-        3. false and ENINVAL if the parameters are broken
-        4. true and isTranslocated = true if the path is on a nullfs mount and in the user's app translocation directory
-        5. true and isTranslocated = false if the path is not on a nullfs mount or not in the user's app translocation directory
-
-        If path is a symlink, the results will reflect whatever the symlink actually points to.
-
-        This function can be called from any process or thread.
-*/
-Boolean SecTranslocateIsTranslocatedURL(CFURLRef path, bool* isTranslocated, CFErrorRef* __nullable error)
-__OSX_AVAILABLE(10.12);
-
-/*!
-    @function SecTranslocateCreateOriginalPathForURL
-
-    @abstract finds the original path to a file given a translocated path
-
-    @param translocatedPath the path to look up
-
-    @param error On error will be populated with an error object describing the failure (a posix domain error such as EINVAL)
-
-    @result A valid, existant path, or NULL on error
-
-    @discussion will return
-        1. NULL and EPERM if the caller doesn't have read access to the path
-        2. NULL and ENOENT if the path doesn't exist
-        3. NULL and ENINVAL if the parameters are broken
-        4. A retained copy of translocatedPath if it isn't translocated
-        5. The real path to original untranslocated file/directory.
-
-        If translocatedPath is a symlink, the results will reflect whatever the symlink actually points to.
-
-        This function can be called from any process or thread.
-*/
-CFURLRef __nullable SecTranslocateCreateOriginalPathForURL(CFURLRef translocatedPath, CFErrorRef* __nullable error)
-__OSX_AVAILABLE(10.12);
-
-/*!
- @function SecTranslocateDeleteSecureDirectory
- 
- @abstract Unmount the translocated directory structure and delete the mount point directory.
- 
- @param translocatedPath a CFURL pointing to a translocated location.
- 
- @param error On error will be populated with an error object describing the failure (a posix domain error such as EINVAL).
- 
- @result true on success, false on error.
- 
- @discussion This function will make sure that the translocatedPath belongs to the calling user before unmounting.
-    After an unmount, this function will iterate through all the directories in the user's AppJail directory and delete any that aren't currently mounted on.
-    This function can only be called from the XPC Server. An error will be returned if this is called from any other process.
- 
- @note This function will be removed before Fuji GM. (unmounting will be internal to the library only)
- 
- */
-Boolean SecTranslocateDeleteSecureDirectory(CFURLRef translocatedPath, CFErrorRef* __nullable error)
-__OSX_AVAILABLE(10.12);
-
-    
-#ifdef __cplusplus
-}
-#endif
-
-CF_ASSUME_NONNULL_END
-
-#endif /* H_LIBSECURITY_TRANSLOCATE */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecTrust.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecTrust.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecTrust.h	2016-05-26 06:38:47.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecTrust.h	2016-06-26 05:40:50.000000000 +0200
@@ -447,8 +447,9 @@
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
@@ -465,7 +466,7 @@
     of the wireless network for which this cert is needed, the account for which
     this cert should be considered valid, and so on.
  */
-bool SecTrustSetExceptions(SecTrustRef trust, CFDataRef exceptions)
+bool SecTrustSetExceptions(SecTrustRef trust, CFDataRef __nullable exceptions)
     __OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_4_0);
 
 /*!
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecureTransport.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecureTransport.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecureTransport.h	2016-05-24 07:00:20.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecureTransport.h	2016-06-26 07:34:08.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmapple.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmapple.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmapple.h	2016-05-26 06:38:48.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmapple.h	2016-06-26 05:40:50.000000000 +0200
@@ -962,7 +962,7 @@
 	CSSM_TP_ACTION_REQUIRE_CRL_PER_CERT 	= 0x00000001,
 	// enable fetch from network
 	CSSM_TP_ACTION_FETCH_CRL_FROM_NET 		= 0x00000002,
-	// if set and positive OCSP verify for given cert, no further revocation
+	// if set and positive CRL verify for given cert, no further revocation
 	// checking need be done on that cert
 	CSSM_TP_ACTION_CRL_SUFFICIENT			= 0x00000004,
 	// require CRL verification for certs which claim a CRL provider
@@ -1164,6 +1164,7 @@
  * (included here for lack of a better place)
  */
 #define kKeychainSuffix			".keychain"
+#define kKeychainDbSuffix       ".keychain-db"
 #define kSystemKeychainName		"System.keychain"
 #define kSystemKeychainDir		"/Library/Keychains/"
 #define kSystemUnlockFile		"/var/db/SystemKey"

```