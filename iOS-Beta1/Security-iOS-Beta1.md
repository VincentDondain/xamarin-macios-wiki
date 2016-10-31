#Security.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecureTransport.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecureTransport.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecureTransport.h	2016-10-01 08:53:48.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Security.framework/Headers/SecureTransport.h	2016-10-24 06:31:25.000000000 +0200
@@ -311,26 +311,30 @@
  * Predefined TLS configurations constants
  */
 
-/* Default configuration - currently same as kSSLSessionConfig_standard */
+/* Default configuration (has 3DES, no RC4) */
 extern const CFStringRef kSSLSessionConfig_default;
 /* ATS v1 Config: TLS v1.2, only PFS ciphersuites */
 extern const CFStringRef kSSLSessionConfig_ATSv1;
 /* ATS v1 Config without PFS: TLS v1.2, include non PFS ciphersuites */
 extern const CFStringRef kSSLSessionConfig_ATSv1_noPFS;
-/* TLS v1.2 to TLS v1.0, with default ciphersuites (no RC4) */
+/* TLS v1.2 to TLS v1.0, with default ciphersuites (no 3DES, no RC4) */
 extern const CFStringRef kSSLSessionConfig_standard;
-/* TLS v1.2 to TLS v1.0, with defaults ciphersuites + RC4 */
+/* TLS v1.2 to TLS v1.0, with default ciphersuites + RC4 + 3DES */
 extern const CFStringRef kSSLSessionConfig_RC4_fallback;
-/* TLS v1.0 only, with defaults ciphersuites + fallback SCSV */
+/* TLS v1.0 only, with default ciphersuites + fallback SCSV */
 extern const CFStringRef kSSLSessionConfig_TLSv1_fallback;
-/* TLS v1.0, with defaults ciphersuites + RC4 + fallback SCSV */
+/* TLS v1.0, with default ciphersuites + RC4 + 3DES + fallback SCSV */
 extern const CFStringRef kSSLSessionConfig_TLSv1_RC4_fallback;
 /* TLS v1.2 to TLS v1.0, defaults + RC4 + DHE ciphersuites */
 extern const CFStringRef kSSLSessionConfig_legacy;
-/* TLS v1.2 to TLS v1.0, defaults + RC4 + DHE ciphersuites */
+/* TLS v1.2 to TLS v1.0, default + RC4 + DHE ciphersuites */
 extern const CFStringRef kSSLSessionConfig_legacy_DHE;
 /* TLS v1.2, anonymous ciphersuites only */
 extern const CFStringRef kSSLSessionConfig_anonymous;
+/* TLS v1.2 to TLS v1.0, has 3DES, no RC4 */
+extern const CFStringRef kSSLSessionConfig_3DES_fallback;
+/* TLS v1.0, with default ciphersuites + 3DES, no RC4 */
+extern const CFStringRef kSSLSessionConfig_TLSv1_3DES_fallback;
 
 
 /******************

```