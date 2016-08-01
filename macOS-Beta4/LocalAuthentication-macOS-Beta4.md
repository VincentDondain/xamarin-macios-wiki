#LocalAuthentication.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h	2016-07-13 01:30:11.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/LocalAuthentication.framework/Headers/LAContext.h	2016-07-28 05:08:56.000000000 +0200
@@ -99,18 +99,16 @@
 /// @param policy Policy to be evaluated.
 ///
 /// @param reply Reply block that is executed when policy evaluation finishes.
+///              success Reply parameter that is YES if the policy has been evaluated successfully or
+///                      NO if the evaluation failed.
+///              error Reply parameter that is nil if the policy has been evaluated successfully, or it
+///                    contains error information about the evaluation failure.
 ///
 /// @param localizedReason Application reason for authentication. This string must be provided in correct
 ///                        localization and should be short and clear. It will be eventually displayed in
 ///                        the authentication dialog subtitle. A name of the calling application will be
 ///                        already displayed in title, so it should not be duplicated here.
 ///
-/// @param success Reply parameter that is YES if the policy has been evaluated successfully or NO if
-///                the evaluation failed.
-///
-/// @param error Reply parameter that is nil if the policy has been evaluated successfully, or it contains
-///              error information about the evaluation failure.
-///
 /// @warning localizedReason parameter is mandatory and the call will throw NSInvalidArgumentException if
 ///          nil or empty string is specified.
 ///
@@ -223,12 +221,10 @@
 ///                        already displayed in title, so it should not be duplicated here.
 ///
 /// @param reply Reply block that is executed when access control evaluation finishes.
-///
-/// @param success Reply parameter that is YES if the access control has been evaluated successfully or NO
-///                if the evaluation failed.
-///
-/// @param error Reply parameter that is nil if the access control has been evaluated successfully, or it
-///              contains error information about the evaluation failure.
+///              success Reply parameter that is YES if the access control has been evaluated successfully or
+///                      NO if the evaluation failed.
+///              error Reply parameter that is nil if the access control has been evaluated successfully, or
+///                    it contains error information about the evaluation failure.
 ///
 /// @warning localizedReason parameter is mandatory and the call will throw NSInvalidArgumentException if
 ///          nil or empty string is specified.

```