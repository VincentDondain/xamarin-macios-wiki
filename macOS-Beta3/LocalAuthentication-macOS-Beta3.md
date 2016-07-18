#LocalAuthentication.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h	2016-06-29 07:12:15.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h	2016-07-13 01:30:11.000000000 +0200
@@ -267,6 +267,8 @@
 ///              data will change. Nature of such database changes cannot be determined
 ///              but comparing data of evaluatedPolicyDomainState after different evaluatePolicy
 ///              will reveal the fact database was changed between calls.
+/// @warning Please note that the value returned by this property can also change between OS versions even if
+///          there was no change of the enrolled fingerprints.
 @property (nonatomic, nullable, readonly) NSData *evaluatedPolicyDomainState NS_AVAILABLE(10_11, 9_0) __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
 
 /// Time interval for accepting a successful Touch ID device unlock (on the lock screen) from the past.

```