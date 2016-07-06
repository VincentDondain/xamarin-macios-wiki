#AudioToolbox.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUAudioUnit.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUAudioUnit.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUAudioUnit.h	2016-05-25 07:13:54.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUAudioUnit.h	2016-06-26 07:56:00.000000000 +0200
@@ -753,7 +753,23 @@
 	@discussion
 		Bridged to the v2 property kAudioUnitProperty_SupportsMPE.
 */
-@property (NS_NONATOMIC_IOSONLY, readonly) BOOL supportsMPE;
+@property (NS_NONATOMIC_IOSONLY, readonly) BOOL supportsMPE NS_AVAILABLE(10_12, 10_0);
+
+/*!	@property	channelMap
+	@brief		Specify a mapping of input channels to output channels.
+	@discussion
+		Converter and input/output audio units may support re-ordering or splitting of input
+		channels to output channels. The number of channels in the channel map is the number of
+		channels of the destination (output format). The channel map entries contain a channel
+		number of the source channel that should be mapped to that destination channel. If -1 is
+		specified, then that destination channel will not contain any channel from the source (so it
+		will be silent).
+		
+		If the property value is nil, then the audio unit does not support this property.
+ 
+		Bridged to the v2 property kAudioOutputUnitProperty_ChannelMap.
+*/
+@property (NS_NONATOMIC_IOSONLY, copy, nullable) NSArray<NSNumber *> *channelMap NS_AVAILABLE(10_12, 10_0);
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUComponent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUComponent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUComponent.h	2016-05-25 06:33:41.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUComponent.h	2016-06-26 07:56:38.000000000 +0200
@@ -1604,6 +1604,34 @@
                                                 __OSX_AVAILABLE_STARTING(__MAC_NA, __IPHONE_7_0);
 #endif // TARGET_OS_IPHONE
 
+/*!
+	@function		AudioUnitExtensionSetComponentList
+	@abstract		Allows the implementor of an audio unit extension to dynamically modify the
+					list of component registrations for the extension.
+	@param			extensionIdentifier
+						The bundle ID of the audio unit extension.
+	@param			audioComponentInfo
+						An array of dictionaries, one for each component, in the same format as
+						described in AudioComponent.h for the Info.plist key "AudioComponents".
+    @result         An OSStatus result code.
+*/
+extern void
+AudioUnitExtensionSetComponentList(CFStringRef extensionIdentifier, CFArrayRef audioComponentInfo)
+                                                __OSX_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+
+/*!
+	@function		AudioUnitExtensionCopyComponentList
+	@abstract		Allows the implementor of an audio unit extension to dynamically modify the
+					list of component registrations for the extension.
+	@param			extensionIdentifier
+						The bundle ID of the audio unit extension.
+	@result			An array of dictionaries, one for each component, in the same format as
+					described in AudioComponent.h for the Info.plist key "AudioComponents".
+					The caller should release this value when done with it.
+*/
+extern CFArrayRef
+AudioUnitExtensionCopyComponentList(CFStringRef extensionIdentifier)
+                                                __OSX_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
 
 
 
```