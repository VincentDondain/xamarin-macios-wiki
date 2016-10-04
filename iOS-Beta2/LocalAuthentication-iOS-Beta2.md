#LocalAuthentication.framework

``` diff
diff -ruN /Applications/Xcode8.1-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h /Applications/Xcode8.1-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h
--- /Applications/Xcode8.1-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h	2016-09-15 01:35:49.000000000 +0200
+++ /Applications/Xcode8.1-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h	2016-09-30 07:12:32.000000000 +0200
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

```