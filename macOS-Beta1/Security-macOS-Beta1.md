#Security.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/Authorization.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/Authorization.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/Authorization.h	2015-08-23 01:04:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/Authorization.h	2016-05-26 06:38:47.000000000 +0200
@@ -158,7 +158,7 @@
 typedef struct {
 	AuthorizationString name;
 	size_t valueLength;
-	void *value;
+	void * __nullable value;
 	UInt32 flags;
 } AuthorizationItem;
 
@@ -172,7 +172,7 @@
 */
 typedef struct {
 	UInt32 count;
-	AuthorizationItem *items;
+	AuthorizationItem * __nullable items;
 } AuthorizationItemSet;
 
 
@@ -188,9 +188,7 @@
 	SECURITY NOTE: Applications should take care to not disclose the AuthorizationExternalForm to
 	potential attackers since it would authorize rights to them.
 */
-enum {
-	kAuthorizationExternalFormLength = 32
-};
+static const size_t kAuthorizationExternalFormLength = 32;
 
 typedef struct {
 	char bytes[kAuthorizationExternalFormLength];
@@ -342,7 +340,6 @@
 	
     @param authorization (input) The authorization object on which this operation is performed.
     @param tag (input/optional) An optional string tag specifing which sideband information should be returned.  When NULL is specified all available information is returned.
-    @param flags (input) options specified by the AuthorizationFlags enum.  set all unused bits to zero to allow for future expansion.
     @param info (output) A pointer to a newly allocated AuthorizationInfoSet in which the requested sideband infomation is returned (info should be deallocated by calling AuthorizationFreeItemSet() when it is no longer needed).
 
     @result errAuthorizationSuccess 0 No error.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/AuthorizationPlugin.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/AuthorizationPlugin.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/AuthorizationPlugin.h	2015-08-23 01:04:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/AuthorizationPlugin.h	2016-05-26 06:38:47.000000000 +0200
@@ -214,8 +214,8 @@
     /* Read value from context.  AuthorizationValue does not own data. */
     OSStatus (*GetContextValue)(AuthorizationEngineRef inEngine,
         AuthorizationString inKey,
-        AuthorizationContextFlags *outContextFlags,
-        const AuthorizationValue * __nullable * __nonnull outValue);
+        AuthorizationContextFlags * __nullable outContextFlags,
+        const AuthorizationValue * __nullable * __nullable outValue);
 
     /* Write value to context.  AuthorizationValue and data are copied. */
     OSStatus (*SetContextValue)(AuthorizationEngineRef inEngine,
@@ -226,7 +226,7 @@
     /* Read value from hints. AuthorizationValue does not own data. */
     OSStatus (*GetHintValue)(AuthorizationEngineRef inEngine,
         AuthorizationString inKey,
-        const AuthorizationValue * __nullable * __nonnull outValue);
+        const AuthorizationValue * __nullable * __nullable outValue);
 
     /* Write value to hints.  AuthorizationValue and data are copied. */
     OSStatus (*SetHintValue)(AuthorizationEngineRef inEngine,
@@ -239,12 +239,12 @@
 
     /* Read SessionId. */
     OSStatus (*GetSessionId)(AuthorizationEngineRef inEngine,
-        AuthorizationSessionId __nullable * __nonnull outSessionId);
+        AuthorizationSessionId __nullable * __nullable outSessionId);
 
     /* Read value from hints. AuthorizationValue does not own data. */
     OSStatus (*GetImmutableHintValue)(AuthorizationEngineRef inEngine,
         AuthorizationString inKey,
-        const AuthorizationValue * __nullable * __nonnull outValue);
+        const AuthorizationValue * __nullable * __nullable outValue);
 
 } AuthorizationCallbacks;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/CSCommon.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/CSCommon.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/CSCommon.h	2016-02-24 07:36:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/CSCommon.h	2016-05-26 06:38:47.000000000 +0200
@@ -118,6 +118,7 @@
 	errSecCSNotAppLike =				-67002,	/* the code is valid but does not seem to be an app */
 	errSecCSBadDiskImageFormat =		-67001,	/* disk image format unrecognized, invalid, or unsuitable */
 	errSecCSUnsupportedDigestAlgorithm = -67000, /* signature digest algorithm(s) specified are not supported */
+	errSecCSInvalidAssociatedFileData =	-66999,	/* resource fork, finder information, or similar detritus not allowed */
 };
 
 /*
@@ -135,6 +136,7 @@
 extern const CFStringRef kSecCFErrorResourceAdded;	/* CFURLRef: unsealed resource found */
 extern const CFStringRef kSecCFErrorResourceAltered; /* CFURLRef: modified resource found */
 extern const CFStringRef kSecCFErrorResourceMissing; /* CFURLRef: sealed (non-optional) resource missing */
+extern const CFStringRef kSecCFErrorResourceSideband; /* CFURLRef: sealed resource has invalid sideband data (resource fork, etc.) */
 extern const CFStringRef kSecCFErrorInfoPlist;		/* CFTypeRef: Info.plist dictionary or component thereof found invalid */
 extern const CFStringRef kSecCFErrorGuestAttributes; /* CFTypeRef: Guest attribute set of element not accepted */
 extern const CFStringRef kSecCFErrorRequirementSyntax; /* CFStringRef: compilation error for Requirement source */
@@ -200,11 +202,12 @@
 typedef CF_OPTIONS(uint32_t, SecCSFlags) {
     kSecCSDefaultFlags = 0,					/* no particular flags (default behavior) */
 	
-    kSecCSConsiderExpiration = 1 << 31,		/* consider expired certificates invalid */
+    kSecCSConsiderExpiration = 1U << 31,		/* consider expired certificates invalid */
     kSecCSEnforceRevocationChecks = 1 << 30,	/* force revocation checks regardless of preference settings */
     kSecCSNoNetworkAccess = 1 << 29,            /* do not use the network, cancels "kSecCSEnforceRevocationChecks"  */
 	kSecCSReportProgress = 1 << 28,			/* make progress report call-backs when configured */
     kSecCSCheckTrustedAnchors = 1 << 27, /* build certificate chain to system trust anchors, not to any self-signed certificate */
+	kSecCSQuickCheck = 1 << 26,		/* (internal) */
 };
 
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccess.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccess.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccess.h	2016-02-24 07:36:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccess.h	2016-05-26 06:38:47.000000000 +0200
@@ -135,7 +135,7 @@
 	@param owner A pointer to a CSSM access control list owner.
 	@param aclCount An unsigned 32-bit integer representing the number of items in the access control list.
 	@param acls A pointer to the access control list.
-	@param On return, a pointer to the new access reference.
+	@param accessRef On return, a pointer to the new access reference.
 	@result A result code.  See "Security Error Codes" (SecBase.h).
 	@discussion For 10.7 and later please use the SecAccessCreateWithOwnerAndACL API
 */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccessControl.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccessControl.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccessControl.h	2015-08-23 01:04:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecAccessControl.h	2016-05-24 06:55:31.000000000 +0200
@@ -46,7 +46,7 @@
 CFTypeID SecAccessControlGetTypeID(void)
 __OSX_AVAILABLE_STARTING(__MAC_10_10, __IPHONE_8_0);
 
-typedef CF_OPTIONS(CFIndex, SecAccessControlCreateFlags) {
+typedef CF_OPTIONS(CFOptionFlags, SecAccessControlCreateFlags) {
     kSecAccessControlUserPresence           = 1 << 0,                                 // User presence policy using Touch ID or Passcode. Touch ID does not have to be available or enrolled. Item is still accessible by Touch ID even if fingers are added or removed.
     kSecAccessControlTouchIDAny             CF_ENUM_AVAILABLE(NA, 9_0)    = 1 << 1,   // Constraint: Touch ID (any finger). Touch ID must be available and at least one finger must be enrolled. Item is still accessible by Touch ID even if fingers are added or removed.
     kSecAccessControlTouchIDCurrentSet      CF_ENUM_AVAILABLE(NA, 9_0)    = 1 << 3,   // Constraint: Touch ID from the set of currently enrolled fingers. Touch ID must be available and at least one finger must be enrolled. When fingers are added or removed, the item is invalidated.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecAsn1Types.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecAsn1Types.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecAsn1Types.h	2015-11-03 22:23:19.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecAsn1Types.h	2016-05-26 06:38:48.000000000 +0200
@@ -44,6 +44,10 @@
 #include <stdint.h>
 
 #include <TargetConditionals.h>
+
+#pragma clang diagnostic push
+#pragma clang diagnostic ignored "-Wdeprecated-declarations"
+
 #if TARGET_OS_EMBEDDED || TARGET_IPHONE_SIMULATOR
 /* @@@ We need something that tells us which platform we are building
    for that let's us distinguish if we are doing an emulator build. */
@@ -244,4 +248,6 @@
 
 CF_ASSUME_NONNULL_END
 
+#pragma clang diagnostic pop
+
 #endif /* _SEC_ASN1_TYPES_H_ */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecCertificate.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecCertificate.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecCertificate.h	2015-08-23 01:04:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecCertificate.h	2016-05-26 06:38:47.000000000 +0200
@@ -31,6 +31,8 @@
 #ifndef _SECURITY_SECCERTIFICATE_H_
 #define _SECURITY_SECCERTIFICATE_H_
 
+#define _SECURITY_VERSION_GREATER_THAN_57610_
+
 #include <CoreFoundation/CFBase.h>
 #include <CoreFoundation/CFArray.h>
 #include <CoreFoundation/CFData.h>
@@ -102,7 +104,7 @@
 	@function SecCertificateCreateWithData
 	@abstract Create a certificate reference given its DER representation as a CFData.
     @param allocator CFAllocator to allocate the certificate data. Pass NULL to use the default allocator.
-    @param certificate DER encoded X.509 certificate.
+    @param data DER encoded X.509 certificate.
 	@result On return, a reference to the certificate. Returns NULL if the passed-in data is not a valid DER-encoded X.509 certificate.
 */
 __nullable
@@ -308,6 +310,39 @@
 	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
 
 /*!
+ @typedef SecKeyUsage
+ @abstract Flags to indicate key usages in the KeyUsage extension of a certificate
+ @constant kSecKeyUsageUnspecified No KeyUsage extension in certificate.
+ @constant kSecKeyUsageDigitalSignature DigitalSignature bit set in KeyUsage extension.
+ @constant kSecKeyUsageNonRepudiation NonRepudiation bit set in KeyUsage extension.
+ @constant kSecKeyUsageContentCommitment ContentCommitment bit set in KeyUsage extension.
+ @constant kSecKeyUsageKeyEncipherment KeyEncipherment bit set in KeyUsage extension.
+ @constant kSecKeyUsageDataEncipherment DataEncipherment bit set in KeyUsage extension.
+ @constant kSecKeyUsageKeyAgreement KeyAgreement bit set in KeyUsage extension.
+ @constant kSecKeyUsageKeyCertSign KeyCertSign bit set in KeyUsage extension.
+ @constant kSecKeyUsageCRLSign CRLSign bit set in KeyUsage extension.
+ @constant kSecKeyUsageEncipherOnly EncipherOnly bit set in KeyUsage extension.
+ @constant kSecKeyUsageDecipherOnly DecipherOnly bit set in KeyUsage extension.
+ @constant kSecKeyUsageCritical KeyUsage extension is marked critical.
+ @constant kSecKeyUsageAll For masking purposes, all SecKeyUsage values.
+ */
+typedef CF_OPTIONS(uint32_t, SecKeyUsage) {
+    kSecKeyUsageUnspecified      = 0,
+    kSecKeyUsageDigitalSignature = 1 << 0,
+    kSecKeyUsageNonRepudiation   = 1 << 1,
+    kSecKeyUsageContentCommitment= 1 << 1,
+    kSecKeyUsageKeyEncipherment  = 1 << 2,
+    kSecKeyUsageDataEncipherment = 1 << 3,
+    kSecKeyUsageKeyAgreement     = 1 << 4,
+    kSecKeyUsageKeyCertSign      = 1 << 5,
+    kSecKeyUsageCRLSign          = 1 << 6,
+    kSecKeyUsageEncipherOnly     = 1 << 7,
+    kSecKeyUsageDecipherOnly     = 1 << 8,
+    kSecKeyUsageCritical         = 1 << 31,
+    kSecKeyUsageAll              = 0x7FFFFFFF
+};
+
+/*!
  @enum kSecPropertyKey
  @abstract Constants used to access dictionary entries returned by SecCertificateCopyValues
  @constant kSecPropertyKeyType The type of the entry
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecCode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecCode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecCode.h	2016-02-24 07:36:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecCode.h	2016-05-26 06:38:47.000000000 +0200
@@ -111,7 +111,7 @@
 	and is the ultimate authority on the its dynamic validity and status.
 	The host relationship is securely established (absent reported errors).
 	
-	@param code A valid SecCode object reference representing code running
+	@param guest A valid SecCode object reference representing code running
 	on the system.
 	@param flags Optional flags. Pass kSecCSDefaultFlags for standard behavior.
 	@param host On successful return, a SecCode object reference identifying
@@ -121,6 +121,16 @@
 */
 OSStatus SecCodeCopyHost(SecCodeRef guest, SecCSFlags flags, SecCodeRef * __nonnull CF_RETURNS_RETAINED host);
 
+extern const CFStringRef kSecGuestAttributeCanonical;
+extern const CFStringRef kSecGuestAttributeHash;
+extern const CFStringRef kSecGuestAttributeMachPort;
+extern const CFStringRef kSecGuestAttributePid;
+extern const CFStringRef kSecGuestAttributeAudit;
+extern const CFStringRef kSecGuestAttributeDynamicCode;
+extern const CFStringRef kSecGuestAttributeDynamicCodeInfoPlist;
+extern const CFStringRef kSecGuestAttributeArchitecture;
+extern const CFStringRef kSecGuestAttributeSubarchitecture;
+
 /*!
 	@function SecCodeCopyGuestWithAttributes
 	This is the omnibus API function for obtaining dynamic code references.
@@ -175,14 +185,6 @@
 	@error errSecCSMultipleGuests The attributes specified do not uniquely identify
 	a guest (the specification is ambiguous).
 */
-extern const CFStringRef kSecGuestAttributeCanonical;
-extern const CFStringRef kSecGuestAttributeHash;
-extern const CFStringRef kSecGuestAttributeMachPort;
-extern const CFStringRef kSecGuestAttributePid;
-extern const CFStringRef kSecGuestAttributeDynamicCode;
-extern const CFStringRef kSecGuestAttributeDynamicCodeInfoPlist;
-extern const CFStringRef kSecGuestAttributeArchitecture;
-extern const CFStringRef kSecGuestAttributeSubarchitecture;
 
 OSStatus SecCodeCopyGuestWithAttributes(SecCodeRef __nullable host,
 	CFDictionaryRef __nullable attributes,	SecCSFlags flags, SecCodeRef * __nonnull CF_RETURNS_RETAINED guest);
@@ -206,6 +208,30 @@
 	@param requirement An optional code requirement specifying additional conditions
 	the code object must satisfy to be considered valid. If NULL, no additional
 	requirements are imposed.
+	@result If validation passes, errSecSuccess. If validation fails, an OSStatus value
+	documented in CSCommon.h or certain other Security framework headers.
+*/
+OSStatus SecCodeCheckValidity(SecCodeRef code, SecCSFlags flags,
+	SecRequirementRef __nullable requirement);
+
+/*!
+	@function SecCodeCheckValidityWifErrors
+	Performs dynamic validation of the given SecCode object. The call obtains and
+	verifies the signature on the code object. It checks the validity of only those
+	sealed components required to establish identity. It checks the SecCode's
+	dynamic validity status as reported by its host. It ensures that the SecCode's
+	host is in turn valid. Finally, it validates the code against a SecRequirement
+	if one is given. The call succeeds if all these conditions are satisfactory.
+	It fails otherwise.
+
+	This call is secure against attempts to modify the file system source of the
+	SecCode.
+
+	@param code The code object to be validated.
+	@param flags Optional flags. Pass kSecCSDefaultFlags for standard behavior.
+	@param requirement An optional code requirement specifying additional conditions
+	the code object must satisfy to be considered valid. If NULL, no additional
+	requirements are imposed.
 	@param errors An optional pointer to a CFErrorRef variable. If the call fails
 	(and something other than errSecSuccess is returned), and this argument is non-NULL,
 	a CFErrorRef is stored there further describing the nature and circumstances
@@ -213,9 +239,6 @@
 	@result If validation passes, errSecSuccess. If validation fails, an OSStatus value
 	documented in CSCommon.h or certain other Security framework headers.
 */
-OSStatus SecCodeCheckValidity(SecCodeRef code, SecCSFlags flags,
-	SecRequirementRef __nullable requirement);
-
 OSStatus SecCodeCheckValidityWithErrors(SecCodeRef code, SecCSFlags flags,
 	SecRequirementRef __nullable requirement, CFErrorRef *errors);
 
@@ -226,10 +249,7 @@
 	code object can be found. For single files, the URL points to that file.
 	For bundles, it points to the directory containing the entire bundle.
 	
-	This returns the same URL as the kSecCodeInfoMainExecutable key returned
-	by SecCodeCopySigningInformation.
-
-	@param code The Code or StaticCode object to be located. For a Code
+	@param staticCode The Code or StaticCode object to be located. For a Code
 		argument, its StaticCode is processed as per SecCodeCopyStaticCode.
 	@param flags Optional flags. Pass kSecCSDefaultFlags for standard behavior.
 	@param path On successful return, contains a CFURL identifying the location
@@ -340,10 +360,12 @@
 	@constant kSecCodeInfoFormat A CFString characterizing the type and format of
 		the code. Suitable for display to a (knowledeable) user.
 	@constant kSecCodeInfoDigestAlgorithm A CFNumber indicating the kind of cryptographic
-		hash function actually used to establish integrity of the signature.
+		hash function chosen to establish integrity of the signature on this system, which
+        is the best supported algorithm from kSecCodeInfoDigestAlgorithms.
 	@constant kSecCodeInfoDigestAlgorithms A CFArray of CFNumbers indicating the kinds of
  		cryptographic hash functions available within the signature. The ordering of those items
- 		has no significance.
+ 		has no significance in terms of priority, but determines the order in which
+        the hashes appear in kSecCodeInfoCdHashes.
  	@constant kSecCodeInfoPlatformIdentifier If this code was signed as part of an operating
  		system release, this value identifies that release.
 	@constant kSecCodeInfoIdentifier A CFString with the actual signing identifier
@@ -391,6 +413,11 @@
 		remains stable across (developer-approved) updates.
 		The algorithm used may change from time to time. However, for any existing signature,
  		the value is stable.
+	@constant kSecCodeInfoCdHashes An array containing the values of the kSecCodeInfoUnique
+        binary identifier for every digest algorithm supported in the signature, in the same
+        order as in the kSecCodeInfoDigestAlgorithms array. The kSecCodeInfoUnique value
+        will be contained in this array, and be the one corresponding to the
+        kSecCodeInfoDigestAlgorithm value.
  */
 CF_ENUM(uint32_t) {
 	kSecCSInternalInformation = 1 << 0,
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecDigestTransform.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecDigestTransform.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecDigestTransform.h	2015-08-23 01:04:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecDigestTransform.h	2016-05-26 06:38:47.000000000 +0200
@@ -93,7 +93,7 @@
 /*!
 	@constant kSecDigestLengthAttribute
 		Used with SecTransformGetAttribute to query the length attribute.
-		Returns a CFNumberRef that contains the length.
+		Returns a CFNumberRef that contains the length in bytes.
  */
 extern const CFStringRef kSecDigestLengthAttribute;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecIdentity.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecIdentity.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecIdentity.h	2015-08-23 01:04:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecIdentity.h	2016-05-26 06:38:47.000000000 +0200
@@ -107,8 +107,7 @@
     @param name A string containing a URI, RFC822 email address, DNS hostname, or other name which uniquely identifies the service requiring an identity.
     @param keyUsage A CFArrayRef value, containing items defined in SecItem.h  Pass NULL to ignore this parameter. (kSecAttrCanEncrypt, kSecAttrCanDecrypt, kSecAttrCanDerive, kSecAttrCanSign, kSecAttrCanVerify, kSecAttrCanWrap, kSecAttrCanUnwrap)
     @param validIssuers (optional) An array of CFDataRef instances whose contents are the subject names of allowable issuers, as returned by a call to SSLCopyDistinguishedNames (SecureTransport.h). Pass NULL if any issuer is allowed.
-    @param identity On return, a reference to the preferred identity, or NULL if none was found. You are responsible for releasing this reference by calling the CFRelease function.
-    @result An identity or NULL. if the preferred identity has not been set. Your code should then typically perform a search for possible identities using the SecItem APIs.
+    @result An identity or NULL, if the preferred identity has not been set. Your code should then typically perform a search for possible identities using the SecItem APIs.
     @discussion If a preferred identity has not been set for the supplied name, the returned identity reference will be NULL. Your code should then perform a search for possible identities, using the SecItemCopyMatching API.
 */
 __nullable
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecItem.h	2015-08-23 01:04:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecItem.h	2016-05-26 06:38:48.000000000 +0200
@@ -517,6 +517,8 @@
 	__OSX_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_2_0);
 extern const CFStringRef kSecAttrCanUnwrap
 	__OSX_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_2_0);
+extern const CFStringRef kSecAttrTokenID
+    __OSX_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_9_0);
 
 /*!
     @enum kSecAttrAccessible Value Constants
@@ -742,6 +744,7 @@
 	 @constant kSecAttrKeyTypeCAST
      @constant kSecAttrKeyTypeECDSA (deprecated; use kSecAttrKeyTypeEC instead.)
      @constant kSecAttrKeyTypeEC
+     @constant kSecAttrKeyTypeECSECPrimeRandom
 */
 extern const CFStringRef kSecAttrKeyTypeRSA
 	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_2_0);
@@ -763,6 +766,8 @@
 	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
 extern const CFStringRef kSecAttrKeyTypeEC
 	__OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_4_0);
+extern const CFStringRef kSecAttrKeyTypeECSECPrimeRandom
+    __OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_4_0);
 
 /*!
 	 @enum kSecAttrPRF Value Constants
@@ -1010,6 +1015,19 @@
 	__OSX_AVAILABLE_STARTING(__MAC_10_11, __IPHONE_9_0);
 
 /*!
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
+
+/*!
 	 @function SecItemCopyMatching
 	 @abstract Returns one or more items which match a search query.
 	 @param query A dictionary containing an item class specification and
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecKey.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecKey.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecKey.h	2015-08-23 01:04:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecKey.h	2016-05-26 06:38:47.000000000 +0200
@@ -39,6 +39,7 @@
 #include <Security/cssmtype.h>
 #include <CoreFoundation/CFBase.h>
 #include <CoreFoundation/CFDictionary.h>
+#include <CoreFoundation/CFSet.h>
 #include <sys/types.h>
 
 #if defined(__cplusplus)
@@ -264,7 +265,7 @@
 	@discussion This API is deprecated for 10.7. Please use the SecKeyGeneratePair API instead.
 */
 OSStatus SecKeyCreatePair(
-        SecKeychainRef __nullable keychainRef,
+        SecKeychainRef _Nullable keychainRef,
         CSSM_ALGORITHMS algorithm,
         uint32 keySizeInBits,
         CSSM_CC_HANDLE contextHandle,
@@ -272,9 +273,9 @@
         uint32 publicKeyAttr,
         CSSM_KEYUSE privateKeyUsage,
         uint32 privateKeyAttr,
-        SecAccessRef __nullable initialAccess,
-        SecKeyRef* __nullable CF_RETURNS_RETAINED publicKey,
-        SecKeyRef* __nullable CF_RETURNS_RETAINED privateKey)
+        SecAccessRef _Nullable initialAccess,
+        SecKeyRef* _Nullable CF_RETURNS_RETAINED publicKey,
+        SecKeyRef* _Nullable CF_RETURNS_RETAINED privateKey)
 		DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER;
 
 /*!
@@ -292,14 +293,14 @@
 	@discussion This API is deprecated for 10.7.  Please use the SecKeyGenerateSymmetric API instead.
 */
 OSStatus SecKeyGenerate(
-        SecKeychainRef __nullable keychainRef,
+        SecKeychainRef _Nullable keychainRef,
         CSSM_ALGORITHMS algorithm,
         uint32 keySizeInBits,
         CSSM_CC_HANDLE contextHandle,
         CSSM_KEYUSE keyUsage,
         uint32 keyAttr,
-        SecAccessRef __nullable initialAccess,
-        SecKeyRef* __nullable CF_RETURNS_RETAINED keyRef)
+        SecAccessRef _Nullable initialAccess,
+        SecKeyRef* _Nullable CF_RETURNS_RETAINED keyRef)
 		DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER;
 
 /*!
@@ -310,7 +311,7 @@
     @result A result code. See "Security Error Codes" (SecBase.h).
     @discussion  The CSSM_KEY is valid until the key item reference is released. This API is deprecated in 10.7. Its use should no longer be needed.
 */
-OSStatus SecKeyGetCSSMKey(SecKeyRef key, const CSSM_KEY * __nullable * __nonnull cssmKey)
+OSStatus SecKeyGetCSSMKey(SecKeyRef key, const CSSM_KEY * _Nullable * __nonnull cssmKey)
 	DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER;;
 
 /*!
@@ -337,7 +338,7 @@
         SecKeyRef keyRef,
         CSSM_ACL_AUTHORIZATION_TAG operation,
         SecCredentialType credentialType,
-        const CSSM_ACCESS_CREDENTIALS * __nullable * __nonnull outCredentials)
+        const CSSM_ACCESS_CREDENTIALS * _Nullable * __nonnull outCredentials)
 		DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER;
 
 /*!
@@ -378,7 +379,7 @@
  * kSecAttrLabel (a user-visible label whose value is a CFStringRef,
  e.g. "My App's Encryption Key")
  * kSecAttrApplicationLabel (a label defined by your application, whose
- value is a CFStringRef and which can be used to find this key in a
+ value is a CFDataRef and which can be used to find this key in a
  subsequent call to SecItemCopyMatching, e.g. "ID-1234567890-9876-0151")
 
  To specify the generated key's access control settings, set this key:
@@ -393,7 +394,7 @@
  * kSecAttrCanUnwrap (defaults to true if not explicitly specified)
 
 */
-__nullable
+_Nullable
 SecKeyRef SecKeyGenerateSymmetric(CFDictionaryRef parameters, CFErrorRef *error)
 	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
 
@@ -422,7 +423,7 @@
  * kSecAttrCanUnwrap (defaults to true if not explicitly specified)
 
 */
-__nullable
+_Nullable
 SecKeyRef SecKeyCreateFromData(CFDictionaryRef parameters,
 	CFDataRef keyData, CFErrorRef *error)
 	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
@@ -467,7 +468,7 @@
 
 */
 OSStatus SecKeyGeneratePair(CFDictionaryRef parameters,
-	SecKeyRef * __nullable CF_RETURNS_RETAINED publicKey, SecKeyRef * __nullable CF_RETURNS_RETAINED privateKey)
+	SecKeyRef * _Nullable CF_RETURNS_RETAINED publicKey, SecKeyRef * _Nullable CF_RETURNS_RETAINED privateKey)
 	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_2_0);
 
 /*!
@@ -488,7 +489,6 @@
  @param parameters A dictionary containing one or more key-value pairs.
  @param deliveryQueue A dispatch queue to be used to deliver the results.
  @param result A callback function to result when the operation has completed.
- @result On success the function returns NULL.
 
  @discussion In order to generate a keypair the parameters dictionary must
  at least contain the following keys:
@@ -555,7 +555,7 @@
  error parameter contains the reason.
 
 */
-__nullable
+_Nullable
 SecKeyRef SecKeyDeriveFromPassword(CFStringRef password,
 	CFDictionaryRef parameters, CFErrorRef *error)
 	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
@@ -576,7 +576,7 @@
  * kSecSalt	- a CFData for the salt value for the encrypt.
 
 */
-__nullable
+_Nullable
 CFDataRef SecKeyWrapSymmetric(SecKeyRef keyToWrap,
 	SecKeyRef wrappingKey, CFDictionaryRef parameters, CFErrorRef *error)
 	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
@@ -597,11 +597,519 @@
  * kSecSalt	- a CFData for the salt value for the decrypt.
 
 */
-__nullable
-SecKeyRef SecKeyUnwrapSymmetric(CFDataRef __nullable * __nonnull keyToUnwrap,
+_Nullable
+SecKeyRef SecKeyUnwrapSymmetric(CFDataRef _Nullable * __nonnull keyToUnwrap,
 	SecKeyRef unwrappingKey, CFDictionaryRef parameters, CFErrorRef *error)
 	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
 
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
+CFDataRef _Nullable SecKeyCreateSignature(SecKeyRef key, SecKeyAlgorithm algorithm, CFDataRef dataToSign, CFErrorRef *error)
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
+CFDataRef _Nullable SecKeyCreateEncryptedData(SecKeyRef key, SecKeyAlgorithm algorithm, CFDataRef plaintext,
+                                               CFErrorRef *error)
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
+CFDataRef _Nullable SecKeyCreateDecryptedData(SecKeyRef key, SecKeyAlgorithm algorithm, CFDataRef ciphertext,
+                                               CFErrorRef *error)
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecKeychain.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecKeychain.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecKeychain.h	2015-08-23 01:04:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecKeychain.h	2016-05-26 06:38:47.000000000 +0200
@@ -416,7 +416,7 @@
 	@function SecKeychainGetPath
 	@abstract Get the path of the specified keychain.
     @param keychain A reference to a keychain.
-    @param ioPathLength On input, a pointer to the size or the buffer pointed to by pathName. On return, the size of the buffer without the zero termination.
+    @param ioPathLength On input, a pointer to the size of the buffer pointed to by pathName. On return, the size of the buffer without the zero termination.
 	@param pathName On return, the POSIX path to the keychain.
     @result A result code.  See "Security Error Codes" (SecBase.h).
 */
@@ -603,7 +603,7 @@
 	@function SecKeychainCopyAccess
 	@abstract Retrieves the access for a keychain. 
 	@param keychain A reference to the keychain from which to copy the access.
-    @param accessRef On return, a pointer to the access reference.
+    @param access On return, a pointer to the access reference.
     @result A result code.  See "Security Error Codes" (SecBase.h).
 */
 OSStatus SecKeychainCopyAccess(SecKeychainRef __nullable keychain, SecAccessRef * __nonnull CF_RETURNS_RETAINED access);
@@ -612,7 +612,7 @@
 	@function SecKeychainSetAccess
 	@abstract Sets the access for a keychain.
     @param keychain A reference to the keychain for which to set the access.
-    @param accessRef An access reference.
+    @param access An access reference.
     @result A result code.  See "Security Error Codes" (SecBase.h).
 */
 OSStatus SecKeychainSetAccess(SecKeychainRef __nullable keychain, SecAccessRef access);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecKeychainItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecKeychainItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecKeychainItem.h	2015-08-23 01:04:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecKeychainItem.h	2016-05-26 06:38:47.000000000 +0200
@@ -259,7 +259,7 @@
     @result A result code. See "Security Error Codes" (SecBase.h).
 */
 OSStatus SecKeychainItemCreateCopy(SecKeychainItemRef itemRef, SecKeychainRef __nullable destKeychainRef,
-	SecAccessRef initialAccess, SecKeychainItemRef * __nonnull CF_RETURNS_RETAINED itemCopy);
+	SecAccessRef __nullable initialAccess, SecKeychainItemRef * __nonnull CF_RETURNS_RETAINED itemCopy);
 
 /*!
     @function SecKeychainItemCreatePersistentReference
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecPolicy.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecPolicy.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecPolicy.h	2015-08-23 01:04:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecPolicy.h	2016-05-26 06:38:47.000000000 +0200
@@ -1,15 +1,15 @@
 /*
- * Copyright (c) 2002-2014 Apple Inc. All Rights Reserved.
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
 
@@ -25,7 +25,7 @@
 	@header SecPolicy
 	The functions provided in SecPolicy.h provide an interface to various
 	X.509 certificate trust policies.
-*/
+ */
 
 #ifndef _SECURITY_SECPOLICY_H_
 #define _SECURITY_SECPOLICY_H_
@@ -34,9 +34,7 @@
 #include <CoreFoundation/CFDictionary.h>
 #include <Security/SecBase.h>
 
-#if defined(__cplusplus)
-extern "C" {
-#endif
+__BEGIN_DECLS
 
 CF_ASSUME_NONNULL_BEGIN
 CF_IMPLICIT_BRIDGING_ENABLED
@@ -48,8 +46,8 @@
 	@constant kSecPolicyAppleSSL
 	@constant kSecPolicyAppleSMIME
 	@constant kSecPolicyAppleEAP
-	@constant kSecPolicyAppleIPsec
 	@constant kSecPolicyAppleiChat
+	@constant kSecPolicyAppleIPsec
 	@constant kSecPolicyApplePKINITClient
 	@constant kSecPolicyApplePKINITServer
 	@constant kSecPolicyAppleCodeSigning
@@ -58,8 +56,8 @@
 	@constant kSecPolicyAppleTimeStamping
 	@constant kSecPolicyAppleRevocation
 	@constant kSecPolicyApplePassbookSigning
-    @constant kSecPolicyApplePayIssuerEncryption
-*/
+	@constant kSecPolicyApplePayIssuerEncryption
+ */
 extern const CFStringRef kSecPolicyAppleX509Basic
     __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_7_0);
 extern const CFStringRef kSecPolicyAppleSSL
@@ -70,8 +68,10 @@
     __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_7_0);
 extern const CFStringRef kSecPolicyAppleIPsec
     __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_7_0);
+#if TARGET_OS_MAC && !TARGET_OS_IPHONE
 extern const CFStringRef kSecPolicyAppleiChat
     __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7, __MAC_10_9, __IPHONE_NA, __IPHONE_NA);
+#endif
 extern const CFStringRef kSecPolicyApplePKINITClient
     __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
 extern const CFStringRef kSecPolicyApplePKINITServer
@@ -91,11 +91,10 @@
 extern const CFStringRef kSecPolicyApplePayIssuerEncryption
     __OSX_AVAILABLE_STARTING(__MAC_10_11, __IPHONE_9_0);
 
-
 /*!
     @enum Policy Value Constants
     @abstract Predefined property key constants used to get or set values in
-        a dictionary for a policy instance.
+    a dictionary for a policy instance.
     @discussion
         All policies will have the following read-only value:
             kSecPolicyOid       (the policy object identifier)
@@ -104,14 +103,16 @@
             kSecPolicyName      (name which must be matched)
             kSecPolicyClient    (evaluate for client, rather than server)
             kSecPolicyRevocationFlags (only valid for a revocation policy)
+            kSecPolicyRevocationFlags   (only valid for a revocation policy)
+            kSecPolicyTeamIdentifier    (only valid for a Passbook signing policy)
 
     @constant kSecPolicyOid Specifies the policy OID (value is a CFStringRef)
     @constant kSecPolicyName Specifies a CFStringRef (or CFArrayRef of same)
         containing a name which must be matched in the certificate to satisfy
         this policy. For SSL/TLS, EAP, and IPSec policies, this specifies the
         server name which must match the common name of the certificate.
-        For S/MIME, this specifies the RFC822 email address.
-        For Passbook signing, this specifies the pass signer.
+        For S/MIME, this specifies the RFC822 email address. For Passbook
+        signing, this specifies the pass signer.
     @constant kSecPolicyClient Specifies a CFBooleanRef value that indicates
         this evaluation should be for a client certificate. If not set (or
         false), the policy evaluates the certificate as a server certificate.
@@ -124,60 +125,63 @@
         the Organizational Unit field of the certificate subject.
  */
 extern const CFStringRef kSecPolicyOid
-	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_7_0);
+    __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_7_0);
 extern const CFStringRef kSecPolicyName
-	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_7_0);
+    __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_7_0);
 extern const CFStringRef kSecPolicyClient
-	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_7_0);
+    __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_7_0);
 extern const CFStringRef kSecPolicyRevocationFlags
-	__OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_7_0);
+    __OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_7_0);
 extern const CFStringRef kSecPolicyTeamIdentifier
-	__OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_7_0);
+    __OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_7_0);
 
 
 /*!
-    @function SecPolicyGetTypeID
-    @abstract Returns the type identifier of SecPolicy instances.
-    @result The CFTypeID of SecPolicy instances.
-*/
+ @function SecPolicyGetTypeID
+ @abstract Returns the type identifier of SecPolicy instances.
+ @result The CFTypeID of SecPolicy instances.
+ */
 CFTypeID SecPolicyGetTypeID(void)
-	__OSX_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
+    __OSX_AVAILABLE_STARTING(__MAC_10_3, __IPHONE_2_0);
 
 /*!
-    @function SecPolicyCopyProperties
-    @abstract Returns a dictionary of this policy's properties.
-    @param policyRef A policy reference.
-    @result A properties dictionary. See "Policy Value Constants" for a list
-    of currently defined property keys. It is the caller's responsibility to
-    CFRelease this reference when it is no longer needed.
-    @result A result code. See "Security Error Codes" (SecBase.h).
-    @discussion This function returns the properties for a policy, as set by the
-    policy's construction function or by a prior call to SecPolicySetProperties.
-*/
+ @function SecPolicyCopyProperties
+ @abstract Returns a dictionary of this policy's properties.
+ @param policyRef A policy reference.
+ @result A properties dictionary. See "Policy Value Constants" for a list
+ of currently defined property keys. It is the caller's responsibility to
+ CFRelease this reference when it is no longer needed.
+ @result A result code. See "Security Error Codes" (SecBase.h).
+ @discussion This function returns the properties for a policy, as set by the
+ policy's construction function or by a prior call to SecPolicySetProperties.
+ */
+__nullable
 CFDictionaryRef SecPolicyCopyProperties(SecPolicyRef policyRef)
-	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_7_0);
+    __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_7_0);
 
 /*!
-    @function SecPolicyCreateBasicX509
-    @abstract Returns a policy object for the default X.509 policy.
-    @result A policy object. The caller is responsible for calling CFRelease
-    on this when it is no longer needed.
-*/
+ @function SecPolicyCreateBasicX509
+ @abstract Returns a policy object for the default X.509 policy.
+ @result A policy object. The caller is responsible for calling CFRelease
+ on this when it is no longer needed.
+ */
+__nullable
 SecPolicyRef SecPolicyCreateBasicX509(void)
-	__OSX_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_2_0);
+    __OSX_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_2_0);
 
 /*!
-    @function SecPolicyCreateSSL
-    @abstract Returns a policy object for evaluating SSL certificate chains.
-    @param server Passing true for this parameter creates a policy for SSL
-    server certificates.
-    @param hostname (Optional) If present, the policy will require the specified
-    hostname to match the hostname in the leaf certificate.
-    @result A policy object. The caller is responsible for calling CFRelease
-    on this when it is no longer needed.
-*/
+ @function SecPolicyCreateSSL
+ @abstract Returns a policy object for evaluating SSL certificate chains.
+ @param server Passing true for this parameter creates a policy for SSL
+ server certificates.
+ @param hostname (Optional) If present, the policy will require the specified
+ hostname to match the hostname in the leaf certificate.
+ @result A policy object. The caller is responsible for calling CFRelease
+ on this when it is no longer needed.
+ */
+__nullable
 SecPolicyRef SecPolicyCreateSSL(Boolean server, CFStringRef __nullable hostname)
-	__OSX_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_2_0);
+    __OSX_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_2_0);
 
 /*!
 	@enum Revocation Policy Constants
@@ -200,14 +204,14 @@
 	OCSP or CRL may be used, depending on the method(s) specified in the
 	certificate and the value of kSecRevocationPreferCRL.
  */
-enum {
-	kSecRevocationOCSPMethod = (1 << 0),
-	kSecRevocationCRLMethod = (1 << 1),
-	kSecRevocationPreferCRL = (1 << 2),
-	kSecRevocationRequirePositiveResponse = (1 << 3),
-	kSecRevocationNetworkAccessDisabled = (1 << 4),
-	kSecRevocationUseAnyAvailableMethod = (kSecRevocationOCSPMethod |
-		kSecRevocationCRLMethod)
+CF_ENUM(CFOptionFlags) {
+    kSecRevocationOCSPMethod = (1 << 0),
+    kSecRevocationCRLMethod = (1 << 1),
+    kSecRevocationPreferCRL = (1 << 2),
+    kSecRevocationRequirePositiveResponse = (1 << 3),
+    kSecRevocationNetworkAccessDisabled = (1 << 4),
+    kSecRevocationUseAnyAvailableMethod = (kSecRevocationOCSPMethod |
+                                           kSecRevocationCRLMethod)
 };
 
 /*!
@@ -222,9 +226,10 @@
 	create a revocation policy yourself unless you wish to override default
 	system behavior (e.g. to force a particular method, or to disable
 	revocation checking entirely.)
-*/
+ */
+__nullable
 SecPolicyRef SecPolicyCreateRevocation(CFOptionFlags revocationFlags)
-	__OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_7_0);
+    __OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_7_0);
 
 /*!
 	@function SecPolicyCreateWithProperties
@@ -236,11 +241,11 @@
 	Constants" for a list of currently defined property keys.
 	@result The returned policy reference, or NULL if the policy could not be
 	created.
-*/
+ */
 __nullable
 SecPolicyRef SecPolicyCreateWithProperties(CFTypeRef policyIdentifier,
-	CFDictionaryRef __nullable properties)
-	__OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_7_0);
+                                           CFDictionaryRef __nullable properties)
+    __OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_7_0);
 
 CF_IMPLICIT_BRIDGING_DISABLED
 CF_ASSUME_NONNULL_END
@@ -310,23 +315,23 @@
         have a key usage that permits it to be used for decryption only.
  */
 extern const CFStringRef kSecPolicyKU_DigitalSignature
-	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
+    __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
 extern const CFStringRef kSecPolicyKU_NonRepudiation
-	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
+    __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
 extern const CFStringRef kSecPolicyKU_KeyEncipherment
-	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
+    __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
 extern const CFStringRef kSecPolicyKU_DataEncipherment
-	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
+    __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
 extern const CFStringRef kSecPolicyKU_KeyAgreement
-	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
+    __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
 extern const CFStringRef kSecPolicyKU_KeyCertSign
-	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
+    __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
 extern const CFStringRef kSecPolicyKU_CRLSign
-	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
+    __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
 extern const CFStringRef kSecPolicyKU_EncipherOnly
-	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
+    __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
 extern const CFStringRef kSecPolicyKU_DecipherOnly
-	__OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
+    __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
 
 /*!
 	@function SecPolicyCreateWithOID
@@ -339,10 +344,10 @@
 	@discussion This function is deprecated in Mac OS X 10.9 and later;
 	use SecPolicyCreateWithProperties (or a more specific policy creation
 	function) instead.
-*/
+ */
 __nullable
 SecPolicyRef SecPolicyCreateWithOID(CFTypeRef policyOID)
-	__OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7, __MAC_10_9, __IPHONE_NA, __IPHONE_NA);
+    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7, __MAC_10_9, __IPHONE_NA, __IPHONE_NA);
 
 /*!
 	@function SecPolicyGetOID
@@ -352,9 +357,9 @@
 	@result A result code. See "Security Error Codes" (SecBase.h).
 	@discussion This function is deprecated in Mac OS X 10.7 and later;
 	use SecPolicyCopyProperties instead.
-*/
+ */
 OSStatus SecPolicyGetOID(SecPolicyRef policyRef, CSSM_OID *oid)
-	__OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_2, __MAC_10_7, __IPHONE_NA, __IPHONE_NA);
+    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_2, __MAC_10_7, __IPHONE_NA, __IPHONE_NA);
 
 /*!
 	@function SecPolicyGetValue
@@ -364,9 +369,9 @@
 	@result A result code. See "Security Error Codes" (SecBase.h).
 	@discussion This function is deprecated in Mac OS X 10.7 and later;
 	use SecPolicyCopyProperties instead.
-*/
+ */
 OSStatus SecPolicyGetValue(SecPolicyRef policyRef, CSSM_DATA *value)
-	__OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_2, __MAC_10_7, __IPHONE_NA, __IPHONE_NA);
+    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_2, __MAC_10_7, __IPHONE_NA, __IPHONE_NA);
 
 /*!
 	@function SecPolicySetValue
@@ -379,9 +384,9 @@
 	instances should be considered read-only; in cases where your code would
 	consider changing properties of a policy, it should instead create a new
 	policy instance with the desired properties.
-*/
+ */
 OSStatus SecPolicySetValue(SecPolicyRef policyRef, const CSSM_DATA *value)
-	__OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_2, __MAC_10_7, __IPHONE_NA, __IPHONE_NA);
+    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_2, __MAC_10_7, __IPHONE_NA, __IPHONE_NA);
 
 /*!
 	@function SecPolicySetProperties
@@ -396,10 +401,10 @@
 	instances should be considered read-only; in cases where your code would
 	consider changing properties of a policy, it should instead create a new
 	policy instance with the desired properties.
-*/
+ */
 OSStatus SecPolicySetProperties(SecPolicyRef policyRef,
-	CFDictionaryRef properties)
-	__OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7, __MAC_10_9, __IPHONE_NA, __IPHONE_NA);
+                                CFDictionaryRef properties)
+    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_7, __MAC_10_9, __IPHONE_NA, __IPHONE_NA);
 
 /*!
 	@function SecPolicyGetTPHandle
@@ -408,17 +413,15 @@
 	@param tpHandle On return, a pointer to a value of type CSSM_TP_HANDLE.
 	@result A result code. See "Security Error Codes" (SecBase.h).
 	@discussion This function is deprecated in Mac OS X 10.7 and later.
-*/
+ */
 OSStatus SecPolicyGetTPHandle(SecPolicyRef policyRef, CSSM_TP_HANDLE *tpHandle)
-	__OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_2, __MAC_10_7, __IPHONE_NA, __IPHONE_NA);
+    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_2, __MAC_10_7, __IPHONE_NA, __IPHONE_NA);
 
 CF_IMPLICIT_BRIDGING_DISABLED
 CF_ASSUME_NONNULL_END
-    
+
 #endif /* TARGET_OS_MAC && !TARGET_OS_IPHONE */
 
-#if defined(__cplusplus)
-}
-#endif
+__END_DECLS
 
 #endif /* !_SECURITY_SECPOLICY_H_ */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecRandom.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecRandom.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecRandom.h	2015-08-23 01:04:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecRandom.h	2016-05-26 06:38:47.000000000 +0200
@@ -55,10 +55,12 @@
 /*!
 	@function SecRandomCopyBytes
 	@abstract Return count random bytes in *bytes, allocated by the caller.
+        It is critical to check the return value for error
 	@result Return 0 on success or -1 if something went wrong, check errno
     to find out the real error.
 */
 int SecRandomCopyBytes(SecRandomRef __nullable rnd, size_t count, uint8_t *bytes)
+    __attribute__ ((warn_unused_result))
     __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_2_0);
 
 CF_IMPLICIT_BRIDGING_DISABLED
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecRequirement.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecRequirement.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecRequirement.h	2015-08-23 01:04:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecRequirement.h	2016-05-26 06:38:47.000000000 +0200
@@ -81,10 +81,6 @@
 	@param flags Optional flags. Pass kSecCSDefaultFlags for standard behavior.
 	@param requirement On successful return, contains a reference to a SecRequirement
 	object that implements the conditions described in text.
-	@param errors An optional pointer to a CFErrorRef variable. If the call fails
-	(and something other than errSecSuccess is returned), and this argument is non-NULL,
-	a CFErrorRef is stored there further describing the nature and circumstances
-	of the failure. The caller must CFRelease() this error object when done with it.
 	@result Upon success, errSecSuccess. Upon error, an OSStatus value documented in
 	CSCommon.h or certain other Security framework headers.
 */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecStaticCode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecStaticCode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecStaticCode.h	2016-02-24 07:36:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecStaticCode.h	2016-05-26 06:38:47.000000000 +0200
@@ -71,12 +71,42 @@
 	may cause the bundle to be misconstrued. If you expect to submit such paths,
 	first clean them with realpath(3) or equivalent.
 	@param flags Optional flags. Pass kSecCSDefaultFlags for standard behavior.
-	@param attributes A CFDictionary containing additional attributes of the code sought.
 	@param staticCode On successful return, contains a reference to the StaticCode object
 	representing the code at path. Unchanged on error.
 	@result Upon success, errSecSuccess. Upon error, an OSStatus value documented in
 	CSCommon.h or certain other Security framework headers.
+*/
+OSStatus SecStaticCodeCreateWithPath(CFURLRef path, SecCSFlags flags, SecStaticCodeRef * __nonnull CF_RETURNS_RETAINED staticCode);
+
+extern const CFStringRef kSecCodeAttributeArchitecture;
+extern const CFStringRef kSecCodeAttributeSubarchitecture;
+extern const CFStringRef kSecCodeAttributeUniversalFileOffset;
+extern const CFStringRef kSecCodeAttributeBundleVersion;
+
+/*!
+	@function SecStaticCodeCreateWithPathAndAttributes
+	Given a path to a file system object, create a SecStaticCode object representing
+	the code at that location, if possible. Such a SecStaticCode is not inherently
+	linked to running code in the system.
 	
+	It is possible to create a SecStaticCode object from an unsigned code object.
+	Most uses of such an object will return the errSecCSUnsigned error. However,
+	SecCodeCopyPath and SecCodeCopySigningInformation can be safely applied to such objects.
+
+	@param path A path to a location in the file system. Only file:// URLs are
+	currently supported. For bundles, pass a URL to the root directory of the
+	bundle. For single files, pass a URL to the file. If you pass a URL to the
+	main executable of a bundle, the bundle as a whole will be generally recognized.
+	Caution: Paths containing embedded // or /../ within a bundle's directory
+	may cause the bundle to be misconstrued. If you expect to submit such paths,
+	first clean them with realpath(3) or equivalent.
+	@param flags Optional flags. Pass kSecCSDefaultFlags for standard behavior.
+	@param attributes A CFDictionary containing additional attributes of the code sought.
+	@param staticCode On successful return, contains a reference to the StaticCode object
+	representing the code at path. Unchanged on error.
+	@result Upon success, errSecSuccess. Upon error, an OSStatus value documented in
+	CSCommon.h or certain other Security framework headers.
+
 	@constant kSecCodeAttributeArchitecture Specifies the Mach-O architecture of code desired.
 	This can be a CFString containing a canonical architecture name ("i386" etc.), or a CFNumber
 	specifying an architecture numerically (see mach/machine.h). This key is ignored if the code
@@ -88,13 +118,6 @@
 	if the code is not in Mach-O form.
 	@constant kSecCodeAttributeUniversalFileOffset The offset of a Mach-O specific slice of a universal Mach-O file.
 */
-extern const CFStringRef kSecCodeAttributeArchitecture;
-extern const CFStringRef kSecCodeAttributeSubarchitecture;
-extern const CFStringRef kSecCodeAttributeUniversalFileOffset;
-extern const CFStringRef kSecCodeAttributeBundleVersion;
-
-OSStatus SecStaticCodeCreateWithPath(CFURLRef path, SecCSFlags flags, SecStaticCodeRef * __nonnull CF_RETURNS_RETAINED staticCode);
-
 OSStatus SecStaticCodeCreateWithPathAndAttributes(CFURLRef path, SecCSFlags flags, CFDictionaryRef attributes,
 	SecStaticCodeRef * __nonnull CF_RETURNS_RETAINED staticCode);
 
@@ -152,6 +175,7 @@
 	kSecCSCheckGatekeeperArchitectures = (1 << 6) | kSecCSCheckAllArchitectures,
 	kSecCSRestrictSymlinks = 1 << 7,
 	kSecCSRestrictToAppLike = 1 << 8,
+	kSecCSRestrictSidebandData = 1 << 9,
 };
 
 OSStatus SecStaticCodeCheckValidity(SecStaticCodeRef staticCode, SecCSFlags flags,
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecTask.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecTask.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecTask.h	2015-08-23 01:04:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecTask.h	2016-05-26 06:38:47.000000000 +0200
@@ -103,6 +103,21 @@
 __nullable
 CFDictionaryRef SecTaskCopyValuesForEntitlements(SecTaskRef task, CFArrayRef entitlements, CFErrorRef *error);
 
+
+   
+/*!
+    @function SecTaskCopySigningIdentifier
+    @abstract Return the value of the codesigning identifier.
+    @param task A previously created SecTask object
+    @param error On a NULL return, this will contain a CFError describing
+    the problem.  This argument may be NULL if the caller is not interested in
+    detailed errors. The caller must CFRelease the returned value.
+ */
+
+__nullable
+CFStringRef
+SecTaskCopySigningIdentifier(SecTaskRef task, CFErrorRef *error);
+
 CF_IMPLICIT_BRIDGING_DISABLED
 CF_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecTranslocate.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecTranslocate.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecTranslocate.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecTranslocate.h	2016-05-26 06:38:48.000000000 +0200
@@ -0,0 +1,219 @@
+/*
+ * Copyright (c) 2016 Apple Inc. All Rights Reserved.
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
+#ifndef H_LIBSECURITY_TRANSLOCATE
+#define H_LIBSECURITY_TRANSLOCATE
+
+#include <CoreFoundation/CoreFoundation.h>
+
+CF_ASSUME_NONNULL_BEGIN
+
+#ifdef __cplusplus
+extern "C" {
+#endif
+
+/*!
+    @function SecTranslocateStartListening
+
+    @abstract Initialize the SecTranslocate Library as the XPC Server, Disk Arbitration Listener, and Launch Services Notification listener
+
+    @param error On error will be populated with an error object describing the failure (a posix domain error such as EINVAL)
+
+    @result True on success False on failure
+ */
+Boolean SecTranslocateStartListening(CFErrorRef* __nullable error)
+__OSX_AVAILABLE(10.12);
+
+/*!
+ @function SecTranslocateStartListeningWithOptions
+
+ @abstract Initialize the SecTranslocate Library as the XPC Server, Disk Arbitration Listener, and Launch Services Notification listener
+
+ @param option (currently unused) A dictionary of options that could impact server startup
+ @param outError On error will be populated with an error object describing the failure (a posix domain error such as EINVAL)
+
+ @result True on success False on failure
+ */
+Boolean SecTranslocateStartListeningWithOptions(CFDictionaryRef options, CFErrorRef * __nullable outError)
+__OSX_AVAILABLE(10.12);
+
+/*!
+    @function SecTranslocateCreateSecureDirectoryForURL
+ 
+    @abstract Create a CFURL pointing to a translocated location from which to access the directory specified by pathToTranslocate.
+
+    @param pathToTranslocate URL of the directory to be accessed from a translocated location.
+    @param destinationPath URL where the directory of interest should be translocated, or NULL for a random UUID location
+    @param error On error will be populated with an error object describing the failure (a posix domain error such as EINVAL)
+
+    @result A CFURL pointing to the translocated location of the directory.
+
+    @discussion 
+        Calls to this function and SecTranslocateDeleteSecureDirectory are serialized to ensure only one call to either
+        is operating at a time.
+        Translocations will be created in the calling users's DARWIN_USER_TEMPDIR/AppTranslocation/<UUID>
+ 
+        pathToTranslocated is expected to be of the form /some/dir/myApp.app
+        destinationPath is expected to be of the form /<DARWIN_USER_TEMPDIR>/AppTranslocation/<DIR>/d/myApp.app
+        
+        Resulting translocations are of the form /<DARWIN_USER_TEMPDIR>/AppTranslocation/<DIR>/d/myApp.app
+            <DIR> will be a UUID if destinationPath isn't specified.
+ 
+        If pathToTranslocate is in a quarantined mountpoint, the quarantine attributes will be propagated to the
+            translocated location.
+ 
+        pathToTranslocate will cause a failure if it doesn't resolve to a path that exists, or it exceeds MAXPATHLEN
+ 
+        destinationPath will cause a failure if
+            1. it doesn't match the app (last directory) specified by path to translocate
+            2. it differs from an already existing mount location for pathToTranslocate
+            3. It isn't in the user's current temp dir
+            4. someone created a file with the same name as the provided path
+            5. It doesn't match the form /<DARWIN_USER_TEMPDIR>/AppTranslocation/<DIR>/d/myApp.app
+
+        pathToTranslocate is returned if it should not be translocated based on policy. It is retained if so it can be treated as a copy.
+
+        This function can be run from any process. If the process is not the xpc server, then an xpc call is made.
+ */
+CFURLRef __nullable SecTranslocateCreateSecureDirectoryForURL (CFURLRef pathToTranslocate, CFURLRef __nullable destinationPath, CFErrorRef* __nullable error)
+__OSX_AVAILABLE(10.12);
+
+/*!
+    @function SecTranslocateAppLaunchCheckin
+
+    @abstract Register that a translocated pid is running
+
+    @param pid the pid to register
+
+    @discussion this function will log if there is a problem. The actual work is either sent to the server via xpc, or dispatched async.
+
+        This function can be run from any process. If the process is not the xpc server, then an xpc call is made.
+ */
+void SecTranslocateAppLaunchCheckin(pid_t pid)
+__OSX_AVAILABLE(10.12);
+
+/*!
+    @function SecTranslocateURLShouldRunTranslocated
+
+    @abstract Implements policy to decide whether the entity defined by path should be run translocated
+
+    @param path URL to the entity in question
+
+    @param shouldTranslocate true if the path should be translocated, false otherwise
+
+    @param error On error will be populated with an error object describing the failure (a posix domain error such as EINVAL)
+
+    @result true on success, false on failure (on failure error is set if provided). shouldTranslocate gives the answer
+
+    @discussion The policy is as follows:
+        1. If path is already on a nullfs mountpoint - no translocation
+        2. No quarantine attributes - no translocation
+        3. If QTN_FLAG_DO_NOT_TRANSLOCATE is set or QTN_FLAG_TRANSLOCATE is not set - no translocations
+        4. Otherwise, if QTN_FLAG_TRANSLOCATE is set - translocation
+
+        This function can be called from any process or thread.
+ */
+Boolean SecTranslocateURLShouldRunTranslocated(CFURLRef path, bool* shouldTranslocate, CFErrorRef* __nullable error)
+__OSX_AVAILABLE(10.12);
+
+/*!
+    @function SecTranslocateIsTranslocatedURL
+
+    @abstract indicates whether the provided path is an original path or a translocated path (for the calling user)
+
+    @param path path to check
+
+    @param isTranslocated true if the path is translocated, false otherwise
+
+    @param error On error will be populated with an error object describing the failure (a posix domain error such as EINVAL)
+
+    @result true on success, false on failure (on failure error is set if provided). isTranslocated gives the answer
+
+    @discussion will return
+        1. false and EPERM if the caller doesn't have read access to the path
+        2. false and ENOENT if the path doesn't exist
+        3. false and ENINVAL if the parameters are broken
+        4. true and isTranslocated = true if the path is on a nullfs mount and in the user's app translocation directory
+        5. true and isTranslocated = false if the path is not on a nullfs mount or not in the user's app translocation directory
+
+        If path is a symlink, the results will reflect whatever the symlink actually points to.
+
+        This function can be called from any process or thread.
+*/
+Boolean SecTranslocateIsTranslocatedURL(CFURLRef path, bool* isTranslocated, CFErrorRef* __nullable error)
+__OSX_AVAILABLE(10.12);
+
+/*!
+    @function SecTranslocateCreateOriginalPathForURL
+
+    @abstract finds the original path to a file given a translocated path
+
+    @param translocatedPath the path to look up
+
+    @param error On error will be populated with an error object describing the failure (a posix domain error such as EINVAL)
+
+    @result A valid, existant path, or NULL on error
+
+    @discussion will return
+        1. NULL and EPERM if the caller doesn't have read access to the path
+        2. NULL and ENOENT if the path doesn't exist
+        3. NULL and ENINVAL if the parameters are broken
+        4. A retained copy of translocatedPath if it isn't translocated
+        5. The real path to original untranslocated file/directory.
+
+        If translocatedPath is a symlink, the results will reflect whatever the symlink actually points to.
+
+        This function can be called from any process or thread.
+*/
+CFURLRef __nullable SecTranslocateCreateOriginalPathForURL(CFURLRef translocatedPath, CFErrorRef* __nullable error)
+__OSX_AVAILABLE(10.12);
+
+/*!
+ @function SecTranslocateDeleteSecureDirectory
+ 
+ @abstract Unmount the translocated directory structure and delete the mount point directory.
+ 
+ @param translocatedPath a CFURL pointing to a translocated location.
+ 
+ @param error On error will be populated with an error object describing the failure (a posix domain error such as EINVAL).
+ 
+ @result true on success, false on error.
+ 
+ @discussion This function will make sure that the translocatedPath belongs to the calling user before unmounting.
+    After an unmount, this function will iterate through all the directories in the user's AppJail directory and delete any that aren't currently mounted on.
+    This function can only be called from the XPC Server. An error will be returned if this is called from any other process.
+ 
+ @note This function will be removed before Fuji GM. (unmounting will be internal to the library only)
+ 
+ */
+Boolean SecTranslocateDeleteSecureDirectory(CFURLRef translocatedPath, CFErrorRef* __nullable error)
+__OSX_AVAILABLE(10.12);
+
+    
+#ifdef __cplusplus
+}
+#endif
+
+CF_ASSUME_NONNULL_END
+
+#endif /* H_LIBSECURITY_TRANSLOCATE */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecTrust.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecTrust.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecTrust.h	2015-08-23 01:04:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecTrust.h	2016-05-26 06:38:47.000000000 +0200
@@ -1,15 +1,15 @@
 /*
- * Copyright (c) 2002-2014 Apple Inc. All Rights Reserved.
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
 
@@ -34,9 +34,7 @@
 #include <CoreFoundation/CoreFoundation.h>
 #include <AvailabilityMacros.h>
 
-#if defined(__cplusplus)
-extern "C" {
-#endif
+__BEGIN_DECLS
 
 CF_ASSUME_NONNULL_BEGIN
 CF_IMPLICIT_BRIDGING_ENABLED
@@ -82,17 +80,15 @@
     of trust evaluation. This value may be returned by the SecTrustEvaluate
     function but not stored as part of the user trust settings.
  */
-
-typedef uint32_t SecTrustResultType;
-enum {
-    kSecTrustResultInvalid = 0,
-    kSecTrustResultProceed = 1,
-    kSecTrustResultConfirm CF_ENUM_DEPRECATED(10_0, 10_9, NA, NA) = 2,
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
@@ -150,6 +146,12 @@
         value of kCFBooleanTrue. The value will be a CFDateRef representing
         the earliest date at which the revocation info for one of the
         certificates in this chain might change.
+    @constant kSecTrustCertificateTransparency
+        This key will be present and have a value of kCFBooleanTrue
+        if this chain is CT qualified.
+    @constant kSecTrustCertificateTransparencyWhiteList
+        This key will be present and have a value of kCFBooleanTrue
+        if this chain is EV, not CT qualified, but included of the CT WhiteList.
  */
 extern const CFStringRef kSecTrustEvaluationDate
     __OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_7_0);
@@ -163,6 +165,10 @@
     __OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_7_0);
 extern const CFStringRef kSecTrustRevocationValidUntilDate
     __OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_7_0);
+extern const CFStringRef kSecTrustCertificateTransparency
+    __OSX_AVAILABLE_STARTING(__MAC_10_11, __IPHONE_9_0);
+extern const CFStringRef kSecTrustCertificateTransparencyWhiteList
+    __OSX_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
 
 #ifdef __BLOCKS__
 /*!
@@ -318,7 +324,7 @@
 /*!
     @function SecTrustGetVerifyTime
     @abstract Returns the verify time.
-    4
+    @param trust A reference to the trust object being verified.
     @result A CFAbsoluteTime value representing the time at which certificates
     should be checked for validity.
     @discussion This function retrieves the verification time for the given
@@ -625,7 +631,7 @@
     for the evaluation, use SecTrustGetTrustResult.
  */
 OSStatus SecTrustGetResult(SecTrustRef trustRef, SecTrustResultType * __nullable result,
-    CFArrayRef * __nonnull CF_RETURNS_RETAINED certChain, CSSM_TP_APPLE_EVIDENCE_INFO * __nullable * __nonnull statusChain)
+    CFArrayRef * __nullable CF_RETURNS_RETAINED certChain, CSSM_TP_APPLE_EVIDENCE_INFO * __nullable * __nullable statusChain)
     __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_2, __MAC_10_7, __IPHONE_NA, __IPHONE_NA);
 
 /*!
@@ -693,8 +699,6 @@
 
 #endif /* TARGET_OS_MAC && !TARGET_OS_IPHONE */
 
-#if defined(__cplusplus)
-}
-#endif
+__END_DECLS
 
 #endif /* !_SECURITY_SECTRUST_H_ */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecTrustSettings.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecTrustSettings.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecTrustSettings.h	2015-08-23 01:04:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecTrustSettings.h	2016-05-26 06:38:48.000000000 +0200
@@ -1,5 +1,5 @@
 /*
- * Copyright (c) 2006,2011,2014 Apple Inc. All Rights Reserved.
+ * Copyright (c) 2006,2011,2014-2015 Apple Inc. All Rights Reserved.
  * 
  * @APPLE_LICENSE_HEADER_START@
  * 
@@ -230,7 +230,7 @@
  * SecTrustSettingsResult for that default Trust Setting (if not 
  * kSecTrustSettingsResultUnspecified) will apply. 
  *
- * This can be used e.g. by a system administrator to explicilty distrust all 
+ * This can be used e.g. by a system administrator to explicitly distrust all
  * of the root certs in the (immutable) system domain for a specific policy. 
  *
  * This const is passed as the 'SecCertificateRef certRef' argument to 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecureTransport.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecureTransport.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecureTransport.h	2015-11-03 22:23:18.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecureTransport.h	2016-05-24 07:00:20.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecurityFeatures.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecurityFeatures.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/SecurityFeatures.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/SecurityFeatures.h	2016-05-26 06:43:00.000000000 +0200
@@ -0,0 +1,35 @@
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
+#define SECURITY_LEGACY_CSSM 1
+#define SECURITY_LEGACY_SECURE_TRANSPORT 1
+
+#endif /* SECURITY_SECURITY_FEATURES_H */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/certextensions.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/certextensions.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/certextensions.h	2015-08-23 01:04:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/certextensions.h	2016-05-26 06:38:48.000000000 +0200
@@ -28,6 +28,9 @@
 
 #include <Security/cssmtype.h>
 
+#pragma clang diagnostic push
+#pragma clang diagnostic ignored "-Wdeprecated-declarations"
+
 /***
  *** Structs for declaring extension-specific data. 
  ***/
@@ -637,4 +640,6 @@
 	CSSM_BOOL				critical;
 } CE_DataAndType DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER;
 
+#pragma clang diagnostic pop
+
 #endif	/* _CERT_EXTENSIONS_H_ */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/cssmaci.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmaci.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/cssmaci.h	2015-08-23 01:04:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmaci.h	2016-05-26 06:38:48.000000000 +0200
@@ -32,6 +32,9 @@
 extern "C" {
 #endif
 
+#pragma clang diagnostic push
+#pragma clang diagnostic ignored "-Wdeprecated-declarations"
+
 typedef struct cssm_spi_ac_funcs {
     CSSM_RETURN (CSSMACI *AuthCompute)
         (CSSM_AC_HANDLE ACHandle,
@@ -53,6 +56,8 @@
          void **OutputParams);
 } CSSM_SPI_AC_FUNCS DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER, *CSSM_SPI_AC_FUNCS_PTR DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER;
 
+#pragma clang diagnostic pop
+
 #ifdef __cplusplus
 }
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/cssmapple.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmapple.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/cssmapple.h	2016-02-24 07:36:42.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmapple.h	2016-05-26 06:38:48.000000000 +0200
@@ -37,6 +37,9 @@
 extern "C" {
 #endif
 
+#pragma clang diagnostic push
+#pragma clang diagnostic ignored "-Wdeprecated-declarations"
+
 /* Guids for standard Apple addin modules. */
 
 /* CSSM itself: {87191ca0-0fc9-11d4-849a-000502b52122} */
@@ -389,6 +392,12 @@
 
     // Make a backup of this database in a new file
     CSSM_APPLEFILEDL_MAKE_BACKUP,
+
+    // Make a copy of this database
+    CSSM_APPLEFILEDL_MAKE_COPY,
+
+    // Delete this database
+    CSSM_APPLEFILEDL_DELETE_FILE,
 };
 
 /* UNLOCK_REFERRAL "type" attribute values */
@@ -701,6 +710,10 @@
     CSSM_APPLE_PRIVATE_CSPDL_CODE_21 = 21,
     CSSM_APPLE_PRIVATE_CSPDL_CODE_22 = 22,
     CSSM_APPLE_PRIVATE_CSPDL_CODE_23 = 23,
+    CSSM_APPLE_PRIVATE_CSPDL_CODE_24 = 24,
+    CSSM_APPLE_PRIVATE_CSPDL_CODE_25 = 25,
+    CSSM_APPLE_PRIVATE_CSPDL_CODE_26 = 26,
+    CSSM_APPLE_PRIVATE_CSPDL_CODE_27 = 27,
 
 	/* Given a CSSM_KEY_PTR in any format, obtain the SHA-1 hash of the
 	 * associated key blob.
@@ -1177,6 +1190,8 @@
 #define errSecErrnoBase			100000
 #define errSecErrnoLimit		100255
 
+#pragma clang diagnostic pop
+
 #ifdef	__cplusplus
 }
 #endif	// __cplusplus
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/cssmcli.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmcli.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/cssmcli.h	2015-08-23 01:04:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmcli.h	2016-05-26 06:38:48.000000000 +0200
@@ -32,6 +32,9 @@
 extern "C" {
 #endif
 
+#pragma clang diagnostic push
+#pragma clang diagnostic ignored "-Wdeprecated-declarations"
+
 typedef struct cssm_spi_cl_funcs {
     CSSM_RETURN (CSSMCLI *CertCreateTemplate)
         (CSSM_CL_HANDLE CLHandle,
@@ -235,6 +238,8 @@
          void **OutputParams);
 } CSSM_SPI_CL_FUNCS DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER, *CSSM_SPI_CL_FUNCS_PTR DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER;
 
+#pragma clang diagnostic pop
+
 #ifdef __cplusplus
 }
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/cssmcspi.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmcspi.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/cssmcspi.h	2015-08-23 01:04:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmcspi.h	2016-05-26 06:38:48.000000000 +0200
@@ -33,6 +33,9 @@
 extern "C" {
 #endif
 
+#pragma clang diagnostic push
+#pragma clang diagnostic ignored "-Wdeprecated-declarations"
+
 typedef struct cssm_spi_csp_funcs {
     CSSM_RETURN (CSSMCSPI *EventNotify)
         (CSSM_CSP_HANDLE CSPHandle,
@@ -360,6 +363,8 @@
          const CSSM_ACL_OWNER_PROTOTYPE *NewOwner);
 } CSSM_SPI_CSP_FUNCS DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER, *CSSM_SPI_CSP_FUNCS_PTR DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER;
 
+#pragma clang diagnostic pop
+
 #ifdef __cplusplus
 }
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/cssmdli.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmdli.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/cssmdli.h	2015-08-23 01:04:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmdli.h	2016-05-26 06:38:48.000000000 +0200
@@ -32,6 +32,9 @@
 extern "C" {
 #endif
 
+#pragma clang diagnostic push
+#pragma clang diagnostic ignored "-Wdeprecated-declarations"
+
 typedef struct cssm_spi_dl_funcs {
     CSSM_RETURN (CSSMDLI *DbOpen)
         (CSSM_DL_HANDLE DLHandle,
@@ -144,6 +147,8 @@
          void **OutputParams);
 } CSSM_SPI_DL_FUNCS DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER, *CSSM_SPI_DL_FUNCS_PTR DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER;
 
+#pragma clang diagnostic pop
+
 #ifdef __cplusplus
 }
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/cssmkrapi.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmkrapi.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/cssmkrapi.h	2015-08-23 01:04:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmkrapi.h	2016-05-26 06:38:48.000000000 +0200
@@ -32,6 +32,9 @@
 extern "C" {
 #endif
 
+#pragma clang diagnostic push
+#pragma clang diagnostic ignored "-Wdeprecated-declarations"
+
 typedef uint32 CSSM_KRSP_HANDLE; /* Key Recovery Service Provider Handle */
 
 typedef struct cssm_kr_name {
@@ -236,6 +239,8 @@
                      void **OutputParams)
 		DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER;
 
+#pragma clang diagnostic pop
+
 #ifdef __cplusplus
 }
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/cssmkrspi.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmkrspi.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/cssmkrspi.h	2015-08-23 01:04:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmkrspi.h	2016-05-26 06:38:48.000000000 +0200
@@ -32,6 +32,9 @@
 extern "C" {
 #endif
 
+#pragma clang diagnostic push
+#pragma clang diagnostic ignored "-Wdeprecated-declarations"
+
 /* Data types for Key Recovery SPI */
 
 typedef struct cssm_spi_kr_funcs {
@@ -104,6 +107,8 @@
          void **OutputParams);
 } CSSM_SPI_KR_FUNCS DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER, *CSSM_SPI_KR_FUNCS_PTR DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER;
 
+#pragma clang diagnostic pop
+
 #ifdef __cplusplus
 }
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/cssmspi.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmspi.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/cssmspi.h	2015-08-23 01:04:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmspi.h	2016-05-26 06:38:48.000000000 +0200
@@ -32,6 +32,9 @@
 extern "C" {
 #endif
 
+#pragma clang diagnostic push
+#pragma clang diagnostic ignored "-Wdeprecated-declarations"
+
 typedef CSSM_RETURN (CSSMAPI *CSSM_SPI_ModuleEventHandler)
     (const CSSM_GUID *ModuleGuid,
      void *CssmNotifyCallbackCtx,
@@ -124,6 +127,7 @@
 CSSM_SPI_ModuleDetach (CSSM_MODULE_HANDLE ModuleHandle)
 	DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER;
 
+#pragma clang diagnostic pop
 
 #ifdef __cplusplus
 }
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/cssmtpi.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmtpi.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/cssmtpi.h	2015-08-23 01:04:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmtpi.h	2016-05-26 06:38:48.000000000 +0200
@@ -32,6 +32,9 @@
 extern "C" {
 #endif
 
+#pragma clang diagnostic push
+#pragma clang diagnostic ignored "-Wdeprecated-declarations"
+
 typedef struct cssm_spi_tp_funcs {
     CSSM_RETURN (CSSMTPI *SubmitCredRequest)
         (CSSM_TP_HANDLE TPHandle,
@@ -195,6 +198,8 @@
          void **OutputParams);
 } CSSM_SPI_TP_FUNCS DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER, *CSSM_SPI_TP_FUNCS_PTR DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER;
 
+#pragma clang diagnostic pop
+
 #ifdef __cplusplus
 }
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/cssmtype.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmtype.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/cssmtype.h	2015-08-23 01:04:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/cssmtype.h	2016-05-26 06:38:48.000000000 +0200
@@ -38,6 +38,9 @@
 extern "C" {
 #endif
 
+#pragma clang diagnostic push
+#pragma clang diagnostic ignored "-Wdeprecated-declarations"
+
 /* Handle types. */
 	
 typedef CSSM_INTPTR CSSM_HANDLE, *CSSM_HANDLE_PTR;
@@ -2073,6 +2076,8 @@
     CSSM_DB_INDEXED_DATA_LOCATION IndexedDataLocation;
 } CSSM_DB_SCHEMA_INDEX_INFO DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER, *CSSM_DB_SCHEMA_INDEX_INFO_PTR DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER;
 
+#pragma clang diagnostic pop
+
 #ifdef __cplusplus
 }
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/emmspi.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/emmspi.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/emmspi.h	2015-08-23 01:04:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/emmspi.h	2016-05-26 06:38:48.000000000 +0200
@@ -32,6 +32,9 @@
 extern "C" {
 #endif
 
+#pragma clang diagnostic push
+#pragma clang diagnostic ignored "-Wdeprecated-declarations"
+
 typedef struct cssm_state_funcs {
     CSSM_RETURN (CSSMAPI *cssm_GetAttachFunctions)
         (CSSM_MODULE_HANDLE hAddIn,
@@ -87,6 +90,8 @@
                            CSSM_MANAGER_REGISTRATION_INFO_PTR FunctionTable)
 						DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER;
 
+#pragma clang diagnostic pop
+
 #ifdef __cplusplus
 }
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/emmtype.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/emmtype.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/emmtype.h	2015-08-23 01:04:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/emmtype.h	2016-05-26 06:38:48.000000000 +0200
@@ -32,6 +32,9 @@
 extern "C" {
 #endif
 
+#pragma clang diagnostic push
+#pragma clang diagnostic ignored "-Wdeprecated-declarations"
+
 #define CSSM_HINT_CALLBACK (1)
 
 typedef uint32 CSSM_MANAGER_EVENT_TYPES;
@@ -46,6 +49,8 @@
     CSSM_DATA EventData;
 } CSSM_MANAGER_EVENT_NOTIFICATION DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER, *CSSM_MANAGER_EVENT_NOTIFICATION_PTR DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER;
 
+#pragma clang diagnostic pop
+
 #ifdef __cplusplus
 }
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/mds.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/mds.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/mds.h	2015-08-23 01:04:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/mds.h	2016-05-26 06:38:47.000000000 +0200
@@ -33,6 +33,9 @@
 extern "C" {
 #endif
 
+#pragma clang diagnostic push
+#pragma clang diagnostic ignored "-Wdeprecated-declarations"
+
 typedef CSSM_DL_HANDLE MDS_HANDLE;
 
 typedef CSSM_DL_DB_HANDLE MDS_DB_HANDLE;
@@ -146,6 +149,8 @@
 MDS_Uninstall (MDS_HANDLE MdsHandle)
 	DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER;
 
+#pragma clang diagnostic pop
+
 #ifdef __cplusplus
 }
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/oids.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/oids.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/oids.h	2015-11-03 22:23:18.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/oids.h	2016-05-26 06:38:47.000000000 +0200
@@ -1,5 +1,5 @@
 /*
- * Copyright (c) 2005-2009,2011-2015 Apple Inc. All Rights Reserved.
+ * Copyright (c) 2005-2009,2011-2016 Apple Inc. All Rights Reserved.
  *
  * @APPLE_LICENSE_HEADER_START@
  *
@@ -33,9 +33,7 @@
 #include <stdint.h>
 #include <string.h>
 
-#ifdef __cplusplus
-extern "C" {
-#endif
+__BEGIN_DECLS
 
 /*
  * Basic data types
@@ -82,7 +80,11 @@
     oidSha224,          /* OID_NIST_HASHALG 4 */
     oidFee,             /* APPLE_ALG_OID 1 */
     oidMd5Fee,          /* APPLE_ALG_OID 3 */
-    oidSha1Fee;         /* APPLE_ALG_OID 4 */
+    oidSha1Fee,         /* APPLE_ALG_OID 4 */
+    oidEcPrime192v1,    /* OID_EC_CURVE 1 prime192v1/secp192r1/ansiX9p192r1*/
+    oidEcPrime256v1,    /* OID_EC_CURVE 7 prime256v1/secp256r1*/
+    oidAnsip384r1,      /* OID_CERTICOM_EC_CURVE 34 ansip384r1/secp384r1*/
+    oidAnsip521r1;      /* OID_CERTICOM_EC_CURVE 35 ansip521r1/secp521r1*/
 
 /* Standard X.509 Cert and CRL extensions. */
 extern const DERItem
@@ -145,8 +147,6 @@
     oidGoogleEmbeddedSignedCertificateTimestamp,
     oidGoogleOCSPSignedCertificateTimestamp;
 
-#ifdef __cplusplus
-}
-#endif
+__END_DECLS
 
 #endif	/* _LIB_DER_OIDS_H_ */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/x509defs.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/x509defs.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Security.framework/Headers/x509defs.h	2015-08-23 01:04:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Security.framework/Headers/x509defs.h	2016-05-26 06:38:48.000000000 +0200
@@ -32,6 +32,9 @@
 extern "C" {
 #endif
 
+#pragma clang diagnostic push
+#pragma clang diagnostic ignored "-Wdeprecated-declarations"
+
 typedef uint8 CSSM_BER_TAG;
 #define BER_TAG_UNKNOWN 0
 #define BER_TAG_BOOLEAN 1
@@ -223,6 +226,8 @@
     CSSM_X509_SIGNATURE signature;
 } CSSM_X509_SIGNED_CRL DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER, *CSSM_X509_SIGNED_CRL_PTR DEPRECATED_IN_MAC_OS_X_VERSION_10_7_AND_LATER;
 
+#pragma clang diagnostic pop
+
 #ifdef __cplusplus
 }
 #endif

```