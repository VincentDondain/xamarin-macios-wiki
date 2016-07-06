#Security.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccessControl.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccessControl.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccessControl.h	2015-09-30 20:35:51.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccessControl.h	2016-05-24 06:55:31.000000000 +0200
@@ -46,7 +46,7 @@
 CFTypeID SecAccessControlGetTypeID(void)
 __OSX_AVAILABLE_STARTING(__MAC_10_10, __IPHONE_8_0);
 
-typedef CF_OPTIONS(CFIndex, SecAccessControlCreateFlags) {
+typedef CF_OPTIONS(CFOptionFlags, SecAccessControlCreateFlags) {
     kSecAccessControlUserPresence           = 1 << 0,                                 // User presence policy using Touch ID or Passcode. Touch ID does not have to be available or enrolled. Item is still accessible by Touch ID even if fingers are added or removed.
     kSecAccessControlTouchIDAny             CF_ENUM_AVAILABLE(NA, 9_0)    = 1 << 1,   // Constraint: Touch ID (any finger). Touch ID must be available and at least one finger must be enrolled. Item is still accessible by Touch ID even if fingers are added or removed.
     kSecAccessControlTouchIDCurrentSet      CF_ENUM_AVAILABLE(NA, 9_0)    = 1 << 3,   // Constraint: Touch ID from the set of currently enrolled fingers. Touch ID must be available and at least one finger must be enrolled. When fingers are added or removed, the item is invalidated.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecBase.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecBase.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecBase.h	2015-09-30 20:35:51.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecBase.h	2016-05-23 06:51:49.000000000 +0200
@@ -109,6 +109,7 @@
     errSecInteractionNotAllowed                 = -25308,  /* User interaction is not allowed. */
     errSecDecode                                = -26275,  /* Unable to decode the provided data. */
     errSecAuthFailed                            = -25293,  /* The user name or passphrase you entered is not correct. */
+    errSecVerifyFailed							= -67808,	/* A cryptographic verification failure has occurred. */
 };
 
 CF_IMPLICIT_BRIDGING_DISABLED
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecItem.h	2015-09-30 20:35:51.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecItem.h	2016-05-24 07:00:26.000000000 +0200
@@ -352,7 +352,8 @@
         kSecAttrLabel (which is intended to be human-readable). This attribute
         is used to look up a key programmatically; in particular, for keys of
         class kSecAttrKeyClassPublic and kSecAttrKeyClassPrivate, the value of
-        this attribute is the hash of the public key.
+        this attribute is the hash of the public key. This item is a type of CFDataRef.
+        Legacy keys may contain a UUID in this field as a CFStringRef.
     @constant kSecAttrIsPermanent Specifies a dictionary key whose value is a
         CFBooleanRef indicating whether the key in question will be stored
         permanently.
@@ -492,7 +493,7 @@
 extern const CFStringRef kSecAttrSyncViewHint
     __OSX_AVAILABLE_STARTING(__MAC_10_11, __IPHONE_9_0);
 extern const CFStringRef kSecAttrTokenID
-    __OSX_AVAILABLE_STARTING(__MAC_10_11, __IPHONE_9_0);
+    __OSX_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_9_0);
 
 /*!
     @enum kSecAttrAccessible Value Constants
@@ -710,12 +711,15 @@
 		in a dictionary. The kSecAttrKeyType constant is the key
 		and its value is one of the constants defined here.
     @constant kSecAttrKeyTypeRSA.
-    @constant kSecAttrKeyTypeEC.
+    @constant kSecAttrKeyTypeECSECPrimeRandom.
+    @constant kSecAttrKeyTypeEC This is legacy name for kSecAttrKeyTypeECSECPrimeRandom, new applications should not use it.
 */
 extern const CFStringRef kSecAttrKeyTypeRSA
     __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_2_0);
 extern const CFStringRef kSecAttrKeyTypeEC
     __OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_4_0);
+extern const CFStringRef kSecAttrKeyTypeECSECPrimeRandom
+    __OSX_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
 
 /*!
     @enum kSecAttrSynchronizable Value Constants
@@ -896,7 +900,7 @@
 extern const CFStringRef kSecUseOperationPrompt
     __OSX_AVAILABLE_STARTING(__MAC_10_10, __IPHONE_8_0);
 extern const CFStringRef kSecUseNoAuthenticationUI
-    __OSX_AVAILABLE_BUT_DEPRECATED_MSG(__MAC_10_10, __MAC_10_11, __IPHONE_8_0, __IPHONE_9_0, "Use a kSecAuthenticationUI instead.");
+    __OSX_AVAILABLE_BUT_DEPRECATED_MSG(__MAC_10_10, __MAC_10_11, __IPHONE_8_0, __IPHONE_9_0, "Use a kSecUseAuthenticationUI instead.");
 extern const CFStringRef kSecUseAuthenticationUI
     __OSX_AVAILABLE_STARTING(__MAC_10_11, __IPHONE_9_0);
 extern const CFStringRef kSecUseAuthenticationContext
@@ -938,7 +942,20 @@
          possible to import pregenerated keys to kSecAttrTokenIDSecureEnclave token.
 */
 extern const CFStringRef kSecAttrTokenIDSecureEnclave
-    __OSX_AVAILABLE_STARTING(__MAC_NA, __IPHONE_9_0);
+__OSX_AVAILABLE_STARTING(__MAC_NA, __IPHONE_9_0);
+
+/*!
+     @enum kSecAttrAccessGroup Value Constants
+     @constant kSecAttrAccessGroupToken Represents well-known access group
+         which contains items provided by external token (typically smart card).
+         This may be used as a value for kSecAttrAccessGroup attribute. Every
+         application has access to this access group so it is not needed to
+         explicitly list it in keychain-access-groups entitlement, but application
+         must explicitly state this access group in keychain queries in order to
+         be able to access items from external tokens.
+*/
+extern const CFStringRef kSecAttrAccessGroupToken
+    __OSX_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
 
 /*!
     @function SecItemCopyMatching
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecKey.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecKey.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecKey.h	2015-09-30 20:35:51.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecKey.h	2016-05-24 06:55:25.000000000 +0200
@@ -26,8 +26,6 @@
 	The functions provided in SecKey.h implement and manage a particular
     type of keychain item that represents a key.  A key can be stored in a
     keychain, but a key can also be a transient object.
-
-	You can use a key as a keychain item in most functions.
 */
 
 #ifndef _SECURITY_SECKEY_H_
@@ -35,6 +33,9 @@
 
 #include <Security/SecBase.h>
 #include <CoreFoundation/CFDictionary.h>
+#include <CoreFoundation/CFData.h>
+#include <CoreFoundation/CFSet.h>
+#include <CoreFoundation/CFError.h>
 #include <sys/types.h>
 
 __BEGIN_DECLS
@@ -155,8 +156,8 @@
       * kSecAttrCanUnwrap default true for private keys, false for public keys
 
 */
-OSStatus SecKeyGeneratePair(CFDictionaryRef parameters, SecKeyRef * __nullable CF_RETURNS_RETAINED publicKey,
-    SecKeyRef * __nullable CF_RETURNS_RETAINED privateKey) __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_2_0);
+OSStatus SecKeyGeneratePair(CFDictionaryRef parameters, SecKeyRef * _Nullable CF_RETURNS_RETAINED publicKey,
+    SecKeyRef * _Nullable CF_RETURNS_RETAINED privateKey) __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_2_0);
 
 
 /*!
@@ -293,7 +294,7 @@
 
 /*!
     @function SecKeyGetBlockSize
-    @abstract Decrypt a block of ciphertext. 
+    @abstract Returns size of the block for specified key, in bytes.
     @param key The key for which the block length is requested.
     @result The block length of the key in bytes.
     @discussion If for example key is an RSA key the value returned by 
@@ -302,6 +303,513 @@
 size_t SecKeyGetBlockSize(SecKeyRef key)
     __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_2_0);
 
+/*!
+ @function SecKeyCreateRandomKey
+ @abstract Generates a new public/private key pair.
+ @param parameters A dictionary containing one or more key-value pairs.
+	See the discussion sections below for a complete overview of options.
+ @param error On error, will be populated with an error object describing the failure.
+ See "Security Error Codes" (SecBase.h).
+ @return Newly generated private key.  To get associated public key, use SecKeyCopyPublicKey().
+ @discussion In order to generate a keypair the parameters dictionary must
+	at least contain the following keys:
+
+ * kSecAttrKeyType with a value being kSecAttrKeyTypeRSA or any other
+ kSecAttrKeyType defined in SecItem.h
+ * kSecAttrKeySizeInBits with a value being a CFNumberRef or CFStringRef
+ containing the requested key size in bits.  Example sizes for RSA
+ keys are: 512, 768, 1024, 2048.
+
+ The values below may be set either in the top-level dictionary or in a
+ dictionary that is the value of the kSecPrivateKeyAttrs or
+ kSecPublicKeyAttrs key in the top-level dictionary.  Setting these
+ attributes explicitly will override the defaults below.  See SecItem.h
+ for detailed information on these attributes including the types of
+ the values.
+
+ * kSecAttrLabel default NULL
+ * kSecAttrIsPermanent if this key is present and has a Boolean value of true,
+   the key or key pair will be added to the default keychain.
+ * kSecAttrTokenID if this key should be generated on specified token.  This
+   attribute can contain CFStringRef and can be present only in the top-level
+   parameters dictionary.
+ * kSecAttrApplicationTag default NULL
+ * kSecAttrEffectiveKeySize default NULL same as kSecAttrKeySizeInBits
+ * kSecAttrCanEncrypt default false for private keys, true for public keys
+ * kSecAttrCanDecrypt default true for private keys, false for public keys
+ * kSecAttrCanDerive default true
+ * kSecAttrCanSign default true for private keys, false for public keys
+ * kSecAttrCanVerify default false for private keys, true for public keys
+ * kSecAttrCanWrap default false for private keys, true for public keys
+ * kSecAttrCanUnwrap default true for private keys, false for public keys
+ */
+SecKeyRef _Nullable SecKeyCreateRandomKey(CFDictionaryRef parameters, CFErrorRef *error)
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+/*!
+	@function SecKeyCreateWithData
+	@abstract Create a SecKey from a well-defined external representation.
+	@param keyData CFData representing the key. The format of the data depends on the type of key being created.
+	@param attributes Dictionary containing attributes describing the key to be imported. The keys in this dictionary
+ 	are kSecAttr* constants from SecItem.h.  Mandatory attributes are:
+	 * kSecAttrKeyType
+	 * kSecAttrKeyClass
+	 * kSecAttrKeySizeInBits
+	@param error On error, will be populated with an error object describing the failure.
+ 	See "Security Error Codes" (SecBase.h).
+	@result A SecKey object representing the key, or NULL on failure.
+	@discussion This function does not add keys to any keychain, but the SecKey object it returns can be added
+ 	to keychain using the SecItemAdd function.
+	The requested data format depend on the type of key (kSecAttrKeyType) being created:
+	 * kSecAttrKeyTypeRSA               PKCS#1 format
+	 * kSecAttrKeyTypeECSECPrimeRandom  SEC1 format (www.secg.org)
+ */
+SecKeyRef _Nullable SecKeyCreateWithData(CFDataRef keyData, CFDictionaryRef attributes, CFErrorRef *error)
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+/*!
+	@function SecKeyCopyExternalRepresentation
+	@abstract Create an external representation for the given key suitable for the key's type.
+	@param key The key to be exported.
+	@param error On error, will be populated with an error object describing the failure.
+ 	See "Security Error Codes" (SecBase.h).
+	@result A CFData representing the key in a format suitable for that key type.
+	@discussion This function may fail if the key is not exportable (e.g., bound to a smart card or Secure Enclave).
+	The format in which the key will be exported depends on the type of key:
+	* kSecAttrKeyTypeRSA                 PKCS#1 format
+	* kSecAttrKeyTypeECSECPrimeRandom    SEC1 format (www.secg.org)
+ */
+CFDataRef _Nullable SecKeyCopyExternalRepresentation(SecKeyRef key, CFErrorRef *error)
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+/*!
+	@function SecKeyCopyAttributes
+	@abstract Retrieve keychain attributes of a key.
+	@param key The key whose attributes are to be retrieved.
+	@result Dictionary containing attributes of the key. The keys that populate this dictionary are defined
+ 	and discussed in SecItem.h.
+	@discussion The attributes provided by this function are:
+	* kSecAttrCanEncrypt
+	* kSecAttrCanDecrypt
+	* kSecAttrCanDerive
+	* kSecAttrCanSign
+	* kSecAttrCanVerify
+	* kSecAttrKeyClass
+	* kSecAttrKeyType
+	* kSecAttrKeySizeInBits
+	* kSecAttrTokenID
+	* kSecAttrApplicationLabel
+	Other values returned in that dictionary are RFU.
+ */
+CFDictionaryRef _Nullable SecKeyCopyAttributes(SecKeyRef key)
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+/*!
+	@function SecKeyCopyPublicKey
+	@abstract Retrieve the public key from a key pair or private key.
+	@param key The key from which to retrieve a public key.
+	@result The public key or NULL if public key is not available for specified key.
+	@discussion Fails if key does not contain a public key or no public key can be computed from it.
+ */
+SecKeyRef _Nullable SecKeyCopyPublicKey(SecKeyRef key)
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+/*!
+	@enum SecKeyAlgorithm
+	@abstract Available algorithms for performing cryptographic operations with SecKey object.  String representation
+	of constant can be used for logging or debugging purposes, because they contain human readable names of the algorithm.
+
+	@constant kSecKeyAlgorithmRSASignatureRaw
+	Raw RSA sign/verify operation, size of input data must be the same as value returned by SecKeyGetBlockSize().
+
+	@constant kSecKeyAlgorithmRSASignatureDigestPKCS1v15SHA1
+	RSA signature with PKCS#1 padding, input data must be SHA-1 generated digest.
+
+	@constant kSecKeyAlgorithmRSASignatureDigestPKCS1v15SHA224
+	RSA signature with PKCS#1 padding, input data must be SHA-224 generated digest.
+
+	@constant kSecKeyAlgorithmRSASignatureDigestPKCS1v15SHA256
+	RSA signature with PKCS#1 padding, input data must be SHA-256 generated digest.
+
+	@constant kSecKeyAlgorithmRSASignatureDigestPKCS1v15SHA384
+	RSA signature with PKCS#1 padding, input data must be SHA-384 generated digest.
+
+	@constant kSecKeyAlgorithmRSASignatureDigestPKCS1v15SHA512
+	RSA signature with PKCS#1 padding, input data must be SHA-512 generated digest.
+
+	@constant kSecKeyAlgorithmRSASignatureMessagePKCS1v15SHA1
+	RSA signature with PKCS#1 padding, SHA-1 digest is generated from input data of any size.
+
+	@constant kSecKeyAlgorithmRSASignatureMessagePKCS1v15SHA224
+	RSA signature with PKCS#1 padding, SHA-224 digest is generated from input data of any size.
+
+	@constant kSecKeyAlgorithmRSASignatureMessagePKCS1v15SHA256
+	RSA signature with PKCS#1 padding, SHA-256 digest is generated from input data of any size.
+
+	@constant kSecKeyAlgorithmRSASignatureMessagePKCS1v15SHA384
+	RSA signature with PKCS#1 padding, SHA-384 digest is generated from input data of any size.
+
+	@constant kSecKeyAlgorithmRSASignatureMessagePKCS1v15SHA512
+	RSA signature with PKCS#1 padding, SHA-512 digest is generated from input data of any size.
+
+	@constant kSecKeyAlgorithmECDSASignatureRFC4754
+	ECDSA algorithm, signature is concatenated r and s, big endian, data is message digest.
+
+	@constant kSecKeyAlgorithmECDSASignatureDigestX962
+	ECDSA algorithm, signature is in DER x9.62 encoding, input data is message digest.
+
+	@constant kSecKeyAlgorithmECDSASignatureDigestX962SHA1
+	ECDSA algorithm, signature is in DER x9.62 encoding, input data is message digest created by SHA1 algorithm.
+
+	@constant kSecKeyAlgorithmECDSASignatureDigestX962SHA1
+	ECDSA algorithm, signature is in DER x9.62 encoding, input data is message digest created by SHA224 algorithm.
+
+	@constant kSecKeyAlgorithmECDSASignatureDigestX962SHA1
+	ECDSA algorithm, signature is in DER x9.62 encoding, input data is message digest created by SHA256 algorithm.
+
+	@constant kSecKeyAlgorithmECDSASignatureDigestX962SHA1
+	ECDSA algorithm, signature is in DER x9.62 encoding, input data is message digest created by SHA384 algorithm.
+
+	@constant kSecKeyAlgorithmECDSASignatureDigestX962SHA1
+	ECDSA algorithm, signature is in DER x9.62 encoding, input data is message digest created by SHA512 algorithm.
+
+	@constant kSecKeyAlgorithmECDSASignatureMessageX962SHA1
+	ECDSA algorithm, signature is in DER x9.62 encoding, SHA-1 digest is generated from input data of any size.
+
+	@constant kSecKeyAlgorithmECDSASignatureMessageX962SHA224
+	ECDSA algorithm, signature is in DER x9.62 encoding, SHA-224 digest is generated from input data of any size.
+
+	@constant kSecKeyAlgorithmECDSASignatureMessageX962SHA256
+	ECDSA algorithm, signature is in DER x9.62 encoding, SHA-256 digest is generated from input data of any size.
+
+	@constant kSecKeyAlgorithmECDSASignatureMessageX962SHA384
+	ECDSA algorithm, signature is in DER x9.62 encoding, SHA-384 digest is generated from input data of any size.
+
+	@constant kSecKeyAlgorithmECDSASignatureMessageX962SHA512
+	ECDSA algorithm, signature is in DER x9.62 encoding, SHA-512 digest is generated from input data of any size.
+
+	@constant kSecKeyAlgorithmRSAEncryptionRaw
+	Raw RSA encryption or decryption, size of data must match RSA key modulus size.  Note that direct
+	use of this algorithm without padding is cryptographically very weak, it is important to always introduce
+	some kind of padding.  Input data size must be less or equal to the key block size and returned block has always
+	the same size as block size, as returned by SecKeyGetBlockSize().
+
+	@constant kSecKeyAlgorithmRSAEncryptionPKCS1
+	RSA encryption or decryption, data is padded using PKCS#1 padding scheme.  This algorithm should be used only for
+	backward compatibility with existing protocols and data. New implementations should choose cryptographically
+	stronger algorithm instead (see kSecKeyAlgorithmRSAEncryptionOAEP).  Input data must be at most
+ 	"key block size - 11" bytes long and returned block has always the same size as block size, as returned
+	by SecKeyGetBlockSize().
+
+	@constant kSecKeyAlgorithmRSAEncryptionOAEPSHA1
+	RSA encryption or decryption, data is padded using OAEP padding scheme internally using SHA1. Input data must be at most
+	"key block size - 42" bytes long and returned block has always the same size as block size, as returned
+	by SecKeyGetBlockSize().
+
+	@constant kSecKeyAlgorithmRSAEncryptionOAEPSHA224
+	RSA encryption or decryption, data is padded using OAEP padding scheme internally using SHA224. Input data must be at most
+	"key block size - 58" bytes long and returned block has always the same size as block size, as returned
+	by SecKeyGetBlockSize().
+
+	@constant kSecKeyAlgorithmRSAEncryptionOAEPSHA256
+	RSA encryption or decryption, data is padded using OAEP padding scheme internally using SHA256. Input data must be at most
+	"key block size - 66" bytes long and returned block has always the same size as block size, as returned
+	by SecKeyGetBlockSize().
+
+	@constant kSecKeyAlgorithmRSAEncryptionOAEPSHA384
+	RSA encryption or decryption, data is padded using OAEP padding scheme internally using SHA384. Input data must be at most
+	"key block size - 98" bytes long and returned block has always the same size as block size, as returned
+	by SecKeyGetBlockSize().
+
+	@constant kSecKeyAlgorithmRSAEncryptionOAEPSHA512
+	RSA encryption or decryption, data is padded using OAEP padding scheme internally using SHA512. Input data must be at most
+	"key block size - 130" bytes long and returned block has always the same size as block size, as returned
+	by SecKeyGetBlockSize().
+
+	@constant kSecKeyAlgorithmECDHKeyExchangeCofactor
+	Compute shared secret using ECDH cofactor algorithm, suitable only for kSecAttrKeyTypeECSECPrimeRandom keys.
+	This algorithm does not accept any parameters, length of output raw shared secret is given by the length of the key.
+
+	@constant kSecKeyAlgorithmECDHKeyExchangeCofactorX963SHA1
+	Compute shared secret using ECDH cofactor algorithm, suitable only for kSecAttrKeyTypeECSECPrimeRandom keys
+	and apply ANSI X9.63 KDF with SHA1 as hashing function.  Requires kSecKeyKeyExchangeParameterRequestedSize and allows
+	kSecKeyKeyExchangeParameterSharedInfo parameters to be used.
+
+	@constant kSecKeyAlgorithmECDHKeyExchangeCofactorX963SHA224
+	Compute shared secret using ECDH cofactor algorithm, suitable only for kSecAttrKeyTypeECSECPrimeRandom keys
+	and apply ANSI X9.63 KDF with SHA224 as hashing function.  Requires kSecKeyKeyExchangeParameterRequestedSize and allows
+	kSecKeyKeyExchangeParameterSharedInfo parameters to be used.
+
+	@constant kSecKeyAlgorithmECDHKeyExchangeCofactorX963SHA256
+	Compute shared secret using ECDH cofactor algorithm, suitable only for kSecAttrKeyTypeECSECPrimeRandom keys
+	and apply ANSI X9.63 KDF with SHA256 as hashing function.  Requires kSecKeyKeyExchangeParameterRequestedSize and allows
+	kSecKeyKeyExchangeParameterSharedInfo parameters to be used.
+
+	@constant kSecKeyAlgorithmECDHKeyExchangeCofactorX963SHA384
+	Compute shared secret using ECDH cofactor algorithm, suitable only for kSecAttrKeyTypeECSECPrimeRandom keys
+	and apply ANSI X9.63 KDF with SHA384 as hashing function.  Requires kSecKeyKeyExchangeParameterRequestedSize and allows
+	kSecKeyKeyExchangeParameterSharedInfo parameters to be used.
+
+	@constant kSecKeyAlgorithmECDHKeyExchangeCofactorX963SHA512
+	Compute shared secret using ECDH cofactor algorithm, suitable only for kSecAttrKeyTypeECSECPrimeRandom keys
+	and apply ANSI X9.63 KDF with SHA512 as hashing function.  Requires kSecKeyKeyExchangeParameterRequestedSize and allows
+	kSecKeyKeyExchangeParameterSharedInfo parameters to be used.
+
+	@constant kSecKeyAlgorithmECDHKeyExchangeStandard
+	Compute shared secret using ECDH algorithm without cofactor, suitable only for kSecAttrKeyTypeECSECPrimeRandom keys.
+	This algorithm does not accept any parameters, length of output raw shared secret is given by the length of the key.
+
+	@constant kSecKeyAlgorithmECDHKeyExchangeStandardX963SHA1
+	Compute shared secret using ECDH algorithm without cofactor, suitable only for kSecAttrKeyTypeECSECPrimeRandom keys
+	and apply ANSI X9.63 KDF with SHA1 as hashing function.  Requires kSecKeyKeyExchangeParameterRequestedSize and allows
+	kSecKeyKeyExchangeParameterSharedInfo parameters to be used.
+
+	@constant kSecKeyAlgorithmECDHKeyExchangeStandardX963SHA224
+	Compute shared secret using ECDH algorithm without cofactor, suitable only for kSecAttrKeyTypeECSECPrimeRandom keys
+	and apply ANSI X9.63 KDF with SHA224 as hashing function.  Requires kSecKeyKeyExchangeParameterRequestedSize and allows
+	kSecKeyKeyExchangeParameterSharedInfo parameters to be used.
+
+	@constant kSecKeyAlgorithmECDHKeyExchangeStandardX963SHA256
+	Compute shared secret using ECDH algorithm without cofactor, suitable only for kSecAttrKeyTypeECSECPrimeRandom keys
+	and apply ANSI X9.63 KDF with SHA256 as hashing function.  Requires kSecKeyKeyExchangeParameterRequestedSize and allows
+	kSecKeyKeyExchangeParameterSharedInfo parameters to be used.
+
+	@constant kSecKeyAlgorithmECDHKeyExchangeStandardX963SHA384
+	Compute shared secret using ECDH algorithm without cofactor, suitable only for kSecAttrKeyTypeECSECPrimeRandom keys
+	and apply ANSI X9.63 KDF with SHA384 as hashing function.  Requires kSecKeyKeyExchangeParameterRequestedSize and allows
+	kSecKeyKeyExchangeParameterSharedInfo parameters to be used.
+
+	@constant kSecKeyAlgorithmECDHKeyExchangeStandardX963SHA512
+	Compute shared secret using ECDH algorithm without cofactor, suitable only for kSecAttrKeyTypeECSECPrimeRandom keys
+	and apply ANSI X9.63 KDF with SHA512 as hashing function.  Requires kSecKeyKeyExchangeParameterRequestedSize and allows
+	kSecKeyKeyExchangeParameterSharedInfo parameters to be used.
+  */
+
+typedef CFStringRef SecKeyAlgorithm CF_STRING_ENUM
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSASignatureRaw
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSASignatureDigestPKCS1v15SHA1
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSASignatureDigestPKCS1v15SHA224
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSASignatureDigestPKCS1v15SHA256
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSASignatureDigestPKCS1v15SHA384
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSASignatureDigestPKCS1v15SHA512
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSASignatureMessagePKCS1v15SHA1
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSASignatureMessagePKCS1v15SHA224
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSASignatureMessagePKCS1v15SHA256
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSASignatureMessagePKCS1v15SHA384
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSASignatureMessagePKCS1v15SHA512
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDSASignatureRFC4754
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDSASignatureDigestX962
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDSASignatureDigestX962SHA1
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDSASignatureDigestX962SHA224
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDSASignatureDigestX962SHA256
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDSASignatureDigestX962SHA384
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDSASignatureDigestX962SHA512
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDSASignatureMessageX962SHA1
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDSASignatureMessageX962SHA224
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDSASignatureMessageX962SHA256
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDSASignatureMessageX962SHA384
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDSASignatureMessageX962SHA512
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSAEncryptionRaw
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSAEncryptionPKCS1
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSAEncryptionOAEPSHA1
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSAEncryptionOAEPSHA224
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSAEncryptionOAEPSHA256
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSAEncryptionOAEPSHA384
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmRSAEncryptionOAEPSHA512
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDHKeyExchangeStandard
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDHKeyExchangeStandardX963SHA1
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDHKeyExchangeStandardX963SHA224
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDHKeyExchangeStandardX963SHA256
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDHKeyExchangeStandardX963SHA384
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDHKeyExchangeStandardX963SHA512
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDHKeyExchangeCofactor
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDHKeyExchangeCofactorX963SHA1
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDHKeyExchangeCofactorX963SHA224
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDHKeyExchangeCofactorX963SHA256
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDHKeyExchangeCofactorX963SHA384
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyAlgorithm kSecKeyAlgorithmECDHKeyExchangeCofactorX963SHA512
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+/*!
+	@function SecKeyCreateSignature
+	@abstract Given a private key and data to sign, generate a digital signature.
+	@param key Private key with which to sign.
+	@param algorithm One of SecKeyAlgorithm constants suitable to generate signature with this key.
+	@param dataToSign The data to be signed, typically the digest of the actual data.
+	@param error On error, will be populated with an error object describing the failure.
+ 	See "Security Error Codes" (SecBase.h).
+	@result The signature over dataToSign represented as a CFData, or NULL on failure.
+	@discussion Computes digital signature using specified key over input data.  The operation algorithm
+	further defines the exact format of input data, operation to be performed and output signature.
+ */
+CFDataRef _Nullable SecKeyCreateSignature(SecKeyRef key, SecKeyAlgorithm algorithm, CFDataRef dataToSign,
+                                           CFErrorRef *error)
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+/*!
+	@function SecKeyVerifySignature
+	@abstract Given a public key, data which has been signed, and a signature, verify the signature.
+	@param key Public key with which to verify the signature.
+	@param algorithm One of SecKeyAlgorithm constants suitable to verify signature with this key.
+	@param signedData The data over which sig is being verified, typically the digest of the actual data.
+	@param signature The signature to verify.
+	@param error On error, will be populated with an error object describing the failure.
+ 	See "Security Error Codes" (SecBase.h).
+	@result True if the signature was valid, False otherwise.
+	@discussion Verifies digital signature operation using specified key and signed data.  The operation algorithm
+	further defines the exact format of input data, signature and operation to be performed.
+ */
+Boolean SecKeyVerifySignature(SecKeyRef key, SecKeyAlgorithm algorithm, CFDataRef signedData, CFDataRef signature, CFErrorRef *error)
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+/*!
+	@function SecKeyCreateEncryptedData
+	@abstract Encrypt a block of plaintext.
+	@param key Public key with which to encrypt the data.
+	@param algorithm One of SecKeyAlgorithm constants suitable to perform encryption with this key.
+	@param plaintext The data to encrypt. The length and format of the data must conform to chosen algorithm,
+	typically be less or equal to the value returned by SecKeyGetBlockSize().
+	@param error On error, will be populated with an error object describing the failure.
+ 	See "Security Error Codes" (SecBase.h).
+	@result The ciphertext represented as a CFData, or NULL on failure.
+	@discussion Encrypts plaintext data using specified key.  The exact type of the operation including the format
+	of input and output data is specified by encryption algorithm.
+ */
+CFDataRef _Nullable SecKeyCreateEncryptedData(SecKeyRef key, SecKeyAlgorithm algorithm, CFDataRef plaintext, CFErrorRef *error)
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+/*!
+	@function SecKeyCreateDecryptedData
+	@abstract Decrypt a block of ciphertext.
+	@param key Private key with which to decrypt the data.
+	@param algorithm One of SecKeyAlgorithm constants suitable to perform decryption with this key.
+	@param ciphertext The data to decrypt. The length and format of the data must conform to chosen algorithm,
+	typically be less or equal to the value returned by SecKeyGetBlockSize().
+	@param error On error, will be populated with an error object describing the failure.
+ 	See "Security Error Codes" (SecBase.h).
+	@result The plaintext represented as a CFData, or NULL on failure.
+	@discussion Decrypts ciphertext data using specified key.  The exact type of the operation including the format
+	of input and output data is specified by decryption algorithm.
+ */
+CFDataRef _Nullable SecKeyCreateDecryptedData(SecKeyRef key, SecKeyAlgorithm algorithm, CFDataRef ciphertext, CFErrorRef *error)
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+/*!
+	@enum SecKeyKeyExchangeParameter SecKey Key Exchange parameters
+	@constant kSecKeyKeyExchangeParameterRequestedSize Contains CFNumberRef with requested result size in bytes.
+	@constant kSecKeyKeyExchangeParameterSharedInfo Contains CFDataRef with additional shared info
+	for KDF (key derivation function).
+ */
+typedef CFStringRef SecKeyKeyExchangeParameter CF_STRING_ENUM
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyKeyExchangeParameter kSecKeyKeyExchangeParameterRequestedSize
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+extern const SecKeyKeyExchangeParameter kSecKeyKeyExchangeParameterSharedInfo
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+/*!
+	@function SecKeyCopyKeyExchangeResult
+	@abstract Perform Diffie-Hellman style of key exchange operation, optionally with additional key-derivation steps.
+	@param algorithm One of SecKeyAlgorithm constants suitable to perform this operation.
+	@param publicKey Remote party's public key.
+	@param parameters Dictionary with parameters, see SecKeyKeyExchangeParameter constants.  Used algorithm
+	determines the set of required and optional parameters to be used.
+	@param error Pointer to an error object on failure.
+	See "Security Error Codes" (SecBase.h).
+	@result Result of key exchange operation as a CFDataRef, or NULL on failure.
+ */
+CFDataRef _Nullable SecKeyCopyKeyExchangeResult(SecKeyRef privateKey, SecKeyAlgorithm algorithm, SecKeyRef publicKey, CFDictionaryRef parameters, CFErrorRef *error)
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+/*!
+	@enum SecKeyOperationType
+ 	@abstract Defines types of cryptographic operations available with SecKey instance.
+
+	@constant kSecKeyOperationTypeSign
+	Represents SecKeyCreateSignature()
+
+	@constant kSecKeyOperationTypeVerify
+	Represents SecKeyVerifySignature()
+
+	@constant kSecKeyOperationTypeEncrypt
+	Represents SecKeyCreateEncryptedData()
+
+	@constant kSecKeyOperationTypeDecrypt
+	Represents SecKeyCreateDecryptedData()
+
+	@constant kSecKeyOperationTypeKeyExchange
+	Represents SecKeyCopyKeyExchangeResult()
+ */
+typedef CF_ENUM(CFIndex, SecKeyOperationType) {
+    kSecKeyOperationTypeSign        = 0,
+    kSecKeyOperationTypeVerify      = 1,
+    kSecKeyOperationTypeEncrypt     = 2,
+    kSecKeyOperationTypeDecrypt     = 3,
+    kSecKeyOperationTypeKeyExchange = 4,
+} __OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
+/*!
+	@function SecKeyIsAlgorithmSupported
+	@abstract Checks whether key supports specified algorithm for specified operation.
+	@param key Key to query
+	@param operation Operation type for which the key is queried
+	@param algorithm Algorithm which is queried
+	@return True if key supports specified algorithm for specified operation, False otherwise.
+ */
+Boolean SecKeyIsAlgorithmSupported(SecKeyRef key, SecKeyOperationType operation, SecKeyAlgorithm algorithm)
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
 CF_IMPLICIT_BRIDGING_DISABLED
 CF_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecPolicy.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecPolicy.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecPolicy.h	2015-09-30 20:35:51.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecPolicy.h	2016-05-24 06:43:45.000000000 +0200
@@ -1,5 +1,5 @@
 /*
- * Copyright (c) 2002-2010,2012-2014 Apple Inc. All Rights Reserved.
+ * Copyright (c) 2002-2016 Apple Inc. All Rights Reserved.
  *
  * @APPLE_LICENSE_HEADER_START@
  * 
@@ -46,6 +46,7 @@
 	@constant kSecPolicyAppleSSL
 	@constant kSecPolicyAppleSMIME
 	@constant kSecPolicyAppleEAP
+	@constant kSecPolicyAppleiChat
 	@constant kSecPolicyAppleIPsec
 	@constant kSecPolicyApplePKINITClient
 	@constant kSecPolicyApplePKINITServer
@@ -54,6 +55,8 @@
 	@constant kSecPolicyAppleIDValidation
 	@constant kSecPolicyAppleTimeStamping
 	@constant kSecPolicyAppleRevocation
+	@constant kSecPolicyApplePassbookSigning
+	@constant kSecPolicyApplePayIssuerEncryption
 */
 extern const CFStringRef kSecPolicyAppleX509Basic
     __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_7_0);
@@ -65,6 +68,10 @@
     __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_7_0);
 extern const CFStringRef kSecPolicyAppleIPsec
     __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_7_0);
+#if TARGET_OS_MAC && !TARGET_OS_IPHONE
+extern const CFStringRef kSecPolicyAppleiChat
+    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7, __MAC_10_9, __IPHONE_NA, __IPHONE_NA);
+#endif
 extern const CFStringRef kSecPolicyApplePKINITClient
     __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
 extern const CFStringRef kSecPolicyApplePKINITServer
@@ -79,6 +86,8 @@
     __OSX_AVAILABLE_STARTING(__MAC_10_8, __IPHONE_7_0);
 extern const CFStringRef kSecPolicyAppleRevocation
     __OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_7_0);
+extern const CFStringRef kSecPolicyApplePassbookSigning
+    __OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_7_0);
 extern const CFStringRef kSecPolicyApplePayIssuerEncryption
     __OSX_AVAILABLE_STARTING(__MAC_10_11, __IPHONE_9_0);
 
@@ -93,20 +102,26 @@
         Additional policy values which your code can optionally set:
             kSecPolicyName      (name which must be matched)
             kSecPolicyClient    (evaluate for client, rather than server)
-            kSecPolicyRevocationFlags (only valid for a revocation policy)
+            kSecPolicyRevocationFlags   (only valid for a revocation policy)
+            kSecPolicyTeamIdentifier    (only valid for a Passbook signing policy)
 
     @constant kSecPolicyOid Specifies the policy OID (value is a CFStringRef)
     @constant kSecPolicyName Specifies a CFStringRef (or CFArrayRef of same)
         containing a name which must be matched in the certificate to satisfy
         this policy. For SSL/TLS, EAP, and IPSec policies, this specifies the
         server name which must match the common name of the certificate.
-        For S/MIME, this specifies the RFC822 email address.
+        For S/MIME, this specifies the RFC822 email address. For Passbook
+        signing, this specifies the pass signer.
     @constant kSecPolicyClient Specifies a CFBooleanRef value that indicates
         this evaluation should be for a client certificate. If not set (or
         false), the policy evaluates the certificate as a server certificate.
     @constant kSecPolicyRevocationFlags Specifies a CFNumberRef that holds a
         kCFNumberCFIndexType bitmask value. See "Revocation Policy Constants"
         for a description of individual bits in this value.
+    @constant kSecPolicyTeamIdentifier Specifies a CFStringRef containing a
+        team identifier which must be matched in the certificate to satisfy
+        this policy. For the Passbook signing policy, this string must match
+        the Organizational Unit field of the certificate subject.
  */
 extern const CFStringRef kSecPolicyOid
 	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_7_0);
@@ -116,6 +131,8 @@
 	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_7_0);
 extern const CFStringRef kSecPolicyRevocationFlags
 	__OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_7_0);
+extern const CFStringRef kSecPolicyTeamIdentifier
+    __OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_7_0);
 
 
 /*!
@@ -137,6 +154,7 @@
     @discussion This function returns the properties for a policy, as set by the
     policy's construction function or by a prior call to SecPolicySetProperties.
 */
+__nullable
 CFDictionaryRef SecPolicyCopyProperties(SecPolicyRef policyRef)
 	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_7_0);
 
@@ -146,6 +164,7 @@
     @result A policy object. The caller is responsible for calling CFRelease
     on this when it is no longer needed.
 */
+__nullable
 SecPolicyRef SecPolicyCreateBasicX509(void)
 	__OSX_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_2_0);
 
@@ -159,6 +178,7 @@
     @result A policy object. The caller is responsible for calling CFRelease
     on this when it is no longer needed.
 */
+__nullable
 SecPolicyRef SecPolicyCreateSSL(Boolean server, CFStringRef __nullable hostname)
 	__OSX_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_2_0);
 
@@ -206,6 +226,7 @@
 	system behavior (e.g. to force a particular method, or to disable
 	revocation checking entirely.)
 */
+__nullable
 SecPolicyRef SecPolicyCreateRevocation(CFOptionFlags revocationFlags)
 	__OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_7_0);
 
@@ -220,6 +241,7 @@
 	@result The returned policy reference, or NULL if the policy could not be
 	created.
 */
+__nullable
 SecPolicyRef SecPolicyCreateWithProperties(CFTypeRef policyIdentifier,
 	CFDictionaryRef __nullable properties)
 	__OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_7_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecRandom.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecRandom.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecRandom.h	2015-09-30 20:35:51.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecRandom.h	2016-05-24 06:39:30.000000000 +0200
@@ -53,10 +53,12 @@
 /*!
 	@function SecRandomCopyBytes
 	@abstract Return count random bytes in *bytes, allocated by the caller.
+         It is critical to check the return value for error
 	@result Return 0 on success or -1 if something went wrong, check errno
     to find out the real error.
 */
 int SecRandomCopyBytes(SecRandomRef __nullable rnd, size_t count, uint8_t *bytes)
+    __attribute__ ((warn_unused_result))
     __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_2_0);
 
 CF_IMPLICIT_BRIDGING_DISABLED
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecSharedCredential.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecSharedCredential.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecSharedCredential.h	2015-09-30 20:35:51.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecSharedCredential.h	2016-05-23 06:50:45.000000000 +0200
@@ -1,15 +1,15 @@
 /*
- * Copyright (c) 2014 Apple Inc. All Rights Reserved.
+ * Copyright (c) 2014-2016 Apple Inc. All Rights Reserved.
  *
  * @APPLE_LICENSE_HEADER_START@
- * 
+ *
  * This file contains Original Code and/or Modifications of Original Code
  * as defined in and that are subject to the Apple Public Source License
  * Version 2.0 (the 'License'). You may not use this file except in
  * compliance with the License. Please obtain a copy of the License at
  * http://www.opensource.apple.com/apsl/ and read it before using this
  * file.
- * 
+ *
  * The Original Code and all software distributed under the License are
  * distributed on an 'AS IS' basis, WITHOUT WARRANTY OF ANY KIND, EITHER
  * EXPRESS OR IMPLIED, AND APPLE HEREBY DISCLAIMS ALL SUCH WARRANTIES,
@@ -17,7 +17,7 @@
  * FITNESS FOR A PARTICULAR PURPOSE, QUIET ENJOYMENT OR NON-INFRINGEMENT.
  * Please see the License for the specific language governing rights and
  * limitations under the License.
- * 
+ *
  * @APPLE_LICENSE_HEADER_END@
  */
 
@@ -53,7 +53,7 @@
         that contains a password.
 */
 extern const CFStringRef kSecSharedPassword
-    __OSX_AVAILABLE_STARTING(__MAC_NA, __IPHONE_8_0) __WATCHOS_UNAVAILABLE;
+    __OSX_AVAILABLE_STARTING(__MAC_NA, __IPHONE_8_0) __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
 
 /*!
  @function SecAddSharedWebCredential
@@ -68,7 +68,7 @@
  */
 void SecAddSharedWebCredential(CFStringRef fqdn, CFStringRef account, CFStringRef __nullable password,
     void (^completionHandler)(CFErrorRef __nullable error))
-    __OSX_AVAILABLE_STARTING(__MAC_NA, __IPHONE_8_0) __WATCHOS_UNAVAILABLE;
+    __OSX_AVAILABLE_STARTING(__MAC_NA, __IPHONE_8_0) __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
 
 /*!
  @function SecRequestSharedWebCredential
@@ -90,7 +90,7 @@
  */
 void SecRequestSharedWebCredential(CFStringRef __nullable fqdn, CFStringRef __nullable account,
     void (^completionHandler)(CFArrayRef __nullable credentials, CFErrorRef __nullable error))
-    __OSX_AVAILABLE_STARTING(__MAC_NA, __IPHONE_8_0) __WATCHOS_UNAVAILABLE;
+    __OSX_AVAILABLE_STARTING(__MAC_NA, __IPHONE_8_0) __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
 
 /*!
  @function SecCreateSharedWebCredentialPassword
@@ -99,7 +99,7 @@
 */
 __nullable
 CFStringRef SecCreateSharedWebCredentialPassword(void)
-__OSX_AVAILABLE_STARTING(__MAC_NA, __IPHONE_8_0) __WATCHOS_UNAVAILABLE;
+    __OSX_AVAILABLE_STARTING(__MAC_NA, __IPHONE_8_0) __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
 
 
 #endif /* __BLOCKS__ */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecTrust.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecTrust.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecTrust.h	2015-09-30 20:35:51.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecTrust.h	2016-05-23 06:50:45.000000000 +0200
@@ -1,15 +1,15 @@
 /*
- * Copyright (c) 2002-2010,2012-2014 Apple Inc. All Rights Reserved.
+ * Copyright (c) 2002-2016 Apple Inc. All Rights Reserved.
  *
  * @APPLE_LICENSE_HEADER_START@
- * 
+ *
  * This file contains Original Code and/or Modifications of Original Code
  * as defined in and that are subject to the Apple Public Source License
  * Version 2.0 (the 'License'). You may not use this file except in
  * compliance with the License. Please obtain a copy of the License at
  * http://www.opensource.apple.com/apsl/ and read it before using this
  * file.
- * 
+ *
  * The Original Code and all software distributed under the License are
  * distributed on an 'AS IS' basis, WITHOUT WARRANTY OF ANY KIND, EITHER
  * EXPRESS OR IMPLIED, AND APPLE HEREBY DISCLAIMS ALL SUCH WARRANTIES,
@@ -17,7 +17,7 @@
  * FITNESS FOR A PARTICULAR PURPOSE, QUIET ENJOYMENT OR NON-INFRINGEMENT.
  * Please see the License for the specific language governing rights and
  * limitations under the License.
- * 
+ *
  * @APPLE_LICENSE_HEADER_END@
  */
 
@@ -80,16 +80,15 @@
     of trust evaluation. This value may be returned by the SecTrustEvaluate
     function but not stored as part of the user trust settings.
  */
-typedef uint32_t SecTrustResultType;
-enum {
-    kSecTrustResultInvalid = 0,
-    kSecTrustResultProceed = 1,
-    kSecTrustResultConfirm SEC_DEPRECATED_ATTRIBUTE = 2,
-    kSecTrustResultDeny = 3,
-    kSecTrustResultUnspecified = 4,
-    kSecTrustResultRecoverableTrustFailure = 5,
-    kSecTrustResultFatalTrustFailure = 6,
-    kSecTrustResultOtherError = 7
+typedef CF_ENUM(uint32_t, SecTrustResultType) {
+    kSecTrustResultInvalid  CF_ENUM_AVAILABLE(10_3, 2_0) = 0,
+    kSecTrustResultProceed  CF_ENUM_AVAILABLE(10_3, 2_0) = 1,
+    kSecTrustResultConfirm  CF_ENUM_DEPRECATED(10_3, 10_9, 2_0, 7_0) = 2,
+    kSecTrustResultDeny  CF_ENUM_AVAILABLE(10_3, 2_0) = 3,
+    kSecTrustResultUnspecified  CF_ENUM_AVAILABLE(10_3, 2_0) = 4,
+    kSecTrustResultRecoverableTrustFailure  CF_ENUM_AVAILABLE(10_3, 2_0) = 5,
+    kSecTrustResultFatalTrustFailure  CF_ENUM_AVAILABLE(10_3, 2_0) = 6,
+    kSecTrustResultOtherError  CF_ENUM_AVAILABLE(10_3, 2_0) = 7
 };
 
 /*!
@@ -150,6 +149,9 @@
     @constant kSecTrustCertificateTransparency
         This key will be present and have a value of kCFBooleanTrue
         if this chain is CT qualified.
+    @constant kSecTrustCertificateTransparencyWhiteList
+        This key will be present and have a value of kCFBooleanTrue
+        if this chain is EV, not CT qualified, but included of the CT WhiteList.
 
  */
 extern const CFStringRef kSecTrustEvaluationDate
@@ -165,7 +167,9 @@
 extern const CFStringRef kSecTrustRevocationValidUntilDate
     __OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_7_0);
 extern const CFStringRef kSecTrustCertificateTransparency
-__OSX_AVAILABLE_STARTING(__MAC_10_11, __IPHONE_9_0);
+    __OSX_AVAILABLE_STARTING(__MAC_10_11, __IPHONE_9_0);
+extern const CFStringRef kSecTrustCertificateTransparencyWhiteList
+    __OSX_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
 
 #ifdef __BLOCKS__
 /*!
@@ -551,8 +555,7 @@
     @constant kSecTrustOptionImplicitAnchors Properly self-signed certs are
     treated as anchors implicitly.
  */
-typedef uint32_t SecTrustOptionFlags;
-enum {
+typedef CF_OPTIONS(uint32_t, SecTrustOptionFlags) {
     kSecTrustOptionAllowExpired       = 0x00000001,
     kSecTrustOptionLeafIsCA           = 0x00000002,
     kSecTrustOptionFetchIssuerFromNet = 0x00000004,
@@ -628,7 +631,7 @@
     for the evaluation, use SecTrustGetTrustResult.
  */
 OSStatus SecTrustGetResult(SecTrustRef trustRef, SecTrustResultType * __nullable result,
-    CFArrayRef * __nonnull CF_RETURNS_RETAINED certChain, CSSM_TP_APPLE_EVIDENCE_INFO * __nullable * __nonnull statusChain)
+    CFArrayRef * __nullable CF_RETURNS_RETAINED certChain, CSSM_TP_APPLE_EVIDENCE_INFO * __nullable * __nullable statusChain)
     __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_2, __MAC_10_7, __IPHONE_NA, __IPHONE_NA);
 
 /*!
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecureTransport.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecureTransport.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecureTransport.h	2015-11-03 03:23:37.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecureTransport.h	2016-05-24 07:00:20.000000000 +0200
@@ -1,5 +1,5 @@
 /*
- * Copyright (c) 1999-2002,2005-2014 Apple Inc. All Rights Reserved.
+ * Copyright (c) 1999-2002,2005-2016 Apple Inc. All Rights Reserved.
  *
  * @APPLE_LICENSE_HEADER_START@
  * 
@@ -147,6 +147,10 @@
      * Set this option to break from a client hello in order to check for SNI
      */
     kSSLSessionOptionBreakOnClientHello = 7,
+    /*
+     * Set this option to Allow renegotations. False by default.
+     */
+    kSSLSessionOptionAllowRenegotiation = 8,
 
 };
 
@@ -171,13 +175,13 @@
 	/*
 	 * Server side: We asked for a cert, client sent one, we validated
 	 *				it OK. App can inspect the cert via
-	 *				SSLGetPeerCertificates().
+	 *				SSLCopyPeerCertificates().
 	 * Client side: server asked for one, we sent it.
 	 */
 	kSSLClientCertSent,
 	/*
 	 * Client sent a cert but failed validation. Server side only.
-	 * Server app can inspect the cert via SSLGetPeerCertificates().
+	 * Server app can inspect the cert via SSLCopyPeerCertificates().
 	 */
 	kSSLClientCertRejected
 } ;
@@ -303,6 +307,29 @@
     kSSLDatagramType
 };
 
+/*
+ * Predefined TLS configurations constants
+ */
+
+/* Default configuration - currently same as kSSLSessionConfig_standard */
+extern const CFStringRef kSSLSessionConfig_default;
+/* ATS v1 Config: TLS v1.2, only PFS ciphersuites */
+extern const CFStringRef kSSLSessionConfig_ATSv1;
+/* ATS v1 Config without PFS: TLS v1.2, include non PFS ciphersuites */
+extern const CFStringRef kSSLSessionConfig_ATSv1_noPFS;
+/* TLS v1.2 to TLS v1.0, with default ciphersuites (no RC4) */
+extern const CFStringRef kSSLSessionConfig_standard;
+/* TLS v1.2 to TLS v1.0, with defaults ciphersuites + RC4 */
+extern const CFStringRef kSSLSessionConfig_RC4_fallback;
+/* TLS v1.0 only, with defaults ciphersuites + fallback SCSV */
+extern const CFStringRef kSSLSessionConfig_TLSv1_fallback;
+/* TLS v1.0, with defaults ciphersuites + RC4 + fallback SCSV */
+extern const CFStringRef kSSLSessionConfig_TLSv1_RC4_fallback;
+/* TLS v1.2 to TLS v1.0, defaults + RC4 + DHE ciphersuites */
+extern const CFStringRef kSSLSessionConfig_legacy;
+/* TLS v1.2 to TLS v1.0, defaults + RC4 + DHE ciphersuites */
+extern const CFStringRef kSSLSessionConfig_legacy_DHE;
+
 
 /******************
  *** Public API ***
@@ -410,6 +437,19 @@
 							 SSLWriteFunc		writeFunc)
 	__OSX_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_5_0);
 
+
+/*
+ * Set a predefined configuration for the SSL Session
+ *
+ * This currently affect enabled protocol versions,
+ * enabled ciphersuites, and the kSSLSessionOptionFallback
+ * session option.
+ */
+OSStatus
+SSLSetSessionConfig(SSLContextRef context,
+                    CFStringRef config)
+    __OSX_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+
 /*
  * Set the minimum SSL protocol version allowed. Optional.
  * The default is the lower supported protocol.
@@ -444,13 +484,13 @@
  *
  * This can only be called when no session is active.
  *
- * For TLS contexts, legal values for minVersion are :
+ * For TLS contexts, legal values for maxVersion are :
  *		kSSLProtocol3
  * 		kTLSProtocol1
  * 		kTLSProtocol11
  * 		kTLSProtocol12
  *
- * For DTLS contexts, legal values for minVersion are :
+ * For DTLS contexts, legal values for maxVersion are :
  *      kDTLSProtocol1
  */
 OSStatus
@@ -719,19 +759,6 @@
 	__OSX_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_5_0);
 
 
-/* Deprecated, does nothing */
-typedef CF_ENUM(int, SSLSessionStrengthPolicy)
-{
-    kSSLSessionStrengthPolicyDefault,
-    kSSLSessionStrengthPolicyATSv1,
-    kSSLSessionStrengthPolicyATSv1_noPFS,
-};
-
-OSStatus
-SSLSetSessionStrengthPolicy(SSLContextRef context,
-                            SSLSessionStrengthPolicy policyStrength);
-
-
 #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
 /*
  * Enable/disable peer certificate chain validation. Default is enabled.
@@ -1299,6 +1326,17 @@
 	__OSX_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_5_0);
 
 /*
+ * Server Only: Request renegotation.
+ * This will return an error if the server is already renegotiating, or if the session is closed.
+ * After this return without error, the application should call SSLHandshake() and/or SSLRead() as
+ * for the original handshake.
+ */
+OSStatus
+SSLReHandshake				(SSLContextRef		context)
+    __OSX_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+
+
+/*
  * Normal application-level read/write. On both of these, a errSSLWouldBlock
  * return and a partially completed transfer - or even zero bytes transferred -
  * are NOT mutually exclusive.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/Security.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/Security.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/Security.h	2015-09-30 20:35:51.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/Security.h	2016-05-24 06:39:30.000000000 +0200
@@ -32,4 +32,6 @@
 #include <Security/SecRandom.h>
 #include <Security/SecSharedCredential.h>
 #include <Security/SecTrust.h>
-
+#if !TARGET_OS_IPHONE
+#include <Security/AuthSession.h>
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecurityFeatures.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecurityFeatures.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecurityFeatures.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecurityFeatures.h	2016-05-24 06:39:30.000000000 +0200
@@ -0,0 +1,32 @@
+/*
+ * Copyright (c) 2015 Apple Inc. All Rights Reserved.
+ *
+ * @APPLE_LICENSE_HEADER_START@
+ *
+ * This file contains Original Code and/or Modifications of Original Code
+ * as defined in and that are subject to the Apple Public Source License
+ * Version 2.0 (the 'License'). You may not use this file except in
+ * compliance with the License. Please obtain a copy of the License at
+ * http://www.opensource.apple.com/apsl/ and read it before using this
+ * file.
+ *
+ * The Original Code and all software distributed under the License are
+ * distributed on an 'AS IS' basis, WITHOUT WARRANTY OF ANY KIND, EITHER
+ * EXPRESS OR IMPLIED, AND APPLE HEREBY DISCLAIMS ALL SUCH WARRANTIES,
+ * INCLUDING WITHOUT LIMITATION, ANY WARRANTIES OF MERCHANTABILITY,
+ * FITNESS FOR A PARTICULAR PURPOSE, QUIET ENJOYMENT OR NON-INFRINGEMENT.
+ * Please see the License for the specific language governing rights and
+ * limitations under the License.
+ *
+ * @APPLE_LICENSE_HEADER_END@
+ */
+
+/*
+ * What features are enabled for this platform, used so that
+ * header files can be shared between the the different platforms
+ */
+
+#ifndef SECURITY_SECURITY_FEATURES_H
+#define SECURITY_SECURITY_FEATURES_H 1
+
+#endif /* SECURITY_SECURITY_FEATURES_H */

```