#ScriptingBridge.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ScriptingBridge.framework/Headers/SBApplication.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ScriptingBridge.framework/Headers/SBApplication.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ScriptingBridge.framework/Headers/SBApplication.h	2016-07-08 11:12:39.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ScriptingBridge.framework/Headers/SBApplication.h	2016-07-23 04:16:11.000000000 +0200
@@ -58,7 +58,7 @@
 
 @protocol SBApplicationDelegate
 
-- (id) eventDidFail:(const AppleEvent *)event withError:(NSError *)error;
+- (nullable id) eventDidFail:(const AppleEvent *)event withError:(NSError *)error;
 	// The target application failed to handle the event.  If you return a result,
 	// it will become the result of the -sendEvent that failed.
 

```