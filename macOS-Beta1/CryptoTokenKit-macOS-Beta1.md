#CryptoTokenKit.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKToken.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKToken.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKToken.h	2016-10-10 01:58:51.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKToken.h	2016-10-24 02:57:03.000000000 +0200
@@ -132,7 +132,7 @@
  @param operation Identifier of the operation.
  @param constraint Constraint to be satisfied by this authentication operation.
  @param error Error details (see TKError.h).
- @return authOperation Resulting context of the operation, which will be eventually finalized by receiving 'finishWithError:'.  The resulting 'authOperation' can be of any type based on TKTokenAuthOperation. For known types (e.g. TKTokenPasswordAuthOperation) the system will first fill in the context-specific properties (e.g. 'password') before triggering 'finishWithError:'.
+ @return authOperation Resulting context of the operation, which will be eventually finalized by receiving 'finishWithError:'.  The resulting 'authOperation' can be of any type based on TKTokenAuthOperation. For known types (e.g. TKTokenPasswordAuthOperation) the system will first fill in the context-specific properties (e.g. 'password') before triggering 'finishWithError:'. When no authentication is actually needed (typically because the session is already authenticated for requested constraint), return instance of TKTokenAuthOperation class instead of any specific subclass.
  */
 - (nullable TKTokenAuthOperation *)tokenSession:(TKTokenSession *)session beginAuthForOperation:(TKTokenOperation)operation constraint:(TKTokenOperationConstraint)constraint error:(NSError **)error;
 

```