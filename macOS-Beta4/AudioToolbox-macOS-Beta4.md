#AudioToolbox.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUComponent.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUComponent.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUComponent.h	2016-07-09 08:26:29.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUComponent.h	2016-07-25 08:05:18.000000000 +0200
@@ -1423,34 +1423,6 @@
 												__OSX_AVAILABLE_STARTING(__MAC_10_0,__IPHONE_2_0);
 
 
-/*!
-	@function		AudioUnitExtensionSetComponentList
-	@abstract		Allows the implementor of an audio unit extension to dynamically modify the
-					list of component registrations for the extension.
-	@param			extensionIdentifier
-						The bundle ID of the audio unit extension.
-	@param			audioComponentInfo
-						An array of dictionaries, one for each component, in the same format as
-						described in AudioComponent.h for the Info.plist key "AudioComponents".
-    @result         An OSStatus result code.
-*/
-extern void
-AudioUnitExtensionSetComponentList(CFStringRef extensionIdentifier, CFArrayRef audioComponentInfo)
-                                                __OSX_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
-
-/*!
-	@function		AudioUnitExtensionCopyComponentList
-	@abstract		Allows the implementor of an audio unit extension to dynamically modify the
-					list of component registrations for the extension.
-	@param			extensionIdentifier
-						The bundle ID of the audio unit extension.
-	@result			An array of dictionaries, one for each component, in the same format as
-					described in AudioComponent.h for the Info.plist key "AudioComponents".
-					The caller should release this value when done with it.
-*/
-extern CFArrayRef
-AudioUnitExtensionCopyComponentList(CFStringRef extensionIdentifier)
-                                                __OSX_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
 
 
 

```