#AudioToolbox.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUAudioUnit.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUAudioUnit.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUAudioUnit.h	2016-05-11 16:31:22.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUAudioUnit.h	2016-06-26 06:32:16.000000000 +0200
@@ -494,7 +494,8 @@
 		
 		AUAudioUnit has an additional pseudo-property, "allParameterValues", on which KVO
 		notifications are issued in response to certain events where potentially all parameter
-		values are invalidated (e.g. selection of a preset or setting fullState).
+		values are invalidated. This includes changes to currentPreset, fullState, and
+		fullStateForDocument.
  
 		Subclassers should implement the parameterTree getter to expose parameters to hosts. They
 		should cache as much as possible and send KVO notifications on "parameterTree" when altering
@@ -745,6 +746,29 @@
 */
 @property (NS_NONATOMIC_IOSONLY, copy, nullable) NSString *contextName;
 
+/*!	@property	supportsMPE
+	@brief		Specifies whether an audio unit supports Multi-dimensional Polyphonic Expression.
+	@discussion
+		Bridged to the v2 property kAudioUnitProperty_SupportsMPE.
+*/
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
+
 @end
 
 // =================================================================================================
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUAudioUnitImplementation.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUAudioUnitImplementation.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUAudioUnitImplementation.h	2016-05-25 07:13:54.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUAudioUnitImplementation.h	2016-06-26 09:02:40.000000000 +0200
@@ -85,6 +85,12 @@
 	if the AU is implemented using AUAudioUnitV2Bridge.
 	See AudioComponent.h.
 
+Note that as of OS X version 10.12, the system has special support for installing both version 2
+(bundle-based) and version 3 (extension) implementations of the same audio unit. When two components
+are registered with the same type/subtype/manufacturer and version, normally the first one found
+is used. But if one is an audio unit extension and the other is not, then the audio unit extension's
+registration "wins", though if an app attempts to open it synchronously, with 
+AudioComponentInstanceNew, then the system will fall back to the version 2 implementation.
 */
 
 #if __OBJC2__
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUComponent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUComponent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUComponent.h	2016-05-11 16:31:22.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUComponent.h	2016-06-26 06:32:16.000000000 +0200
@@ -1423,6 +1423,34 @@
 												__OSX_AVAILABLE_STARTING(__MAC_10_0,__IPHONE_2_0);
 
 
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
 
 
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUParameters.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUParameters.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUParameters.h	2016-05-25 06:33:41.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AUParameters.h	2016-06-26 07:56:38.000000000 +0200
@@ -256,7 +256,9 @@
 		"LFO.rate.value" refers to that parameter's value.
 
 		An audio unit may choose to dynamically rearrange the tree. When doing so, it must
-		issue a KVO notification on the audio unit's parameterTree property.
+		issue a KVO notification on the audio unit's parameterTree property. The tree's elements are
+		mostly immutable (except for values and implementor hooks); the only way to modify them
+		is to publish a new tree.
 */
 NS_CLASS_AVAILABLE(10_11, 9_0)
 @interface AUParameterTree : AUParameterGroup <NSSecureCoding>
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AudioToolbox.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AudioToolbox.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AudioToolbox.h	2016-05-11 16:31:24.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AudioToolbox.h	2016-06-26 06:32:17.000000000 +0200
@@ -37,12 +37,9 @@
 		#include <AudioToolbox/AudioUnitUtilities.h>
 		#include <AudioToolbox/AUMIDIController.h>
 		#include <AudioToolbox/CoreAudioClock.h>
-		#ifdef __OBJC__
-			#import <AudioToolbox/AUCocoaUIView.h>
-		#endif
 
 	#ifdef __OBJC2__
-		// iOS, OS X 64-bit only
+		// iOS (all architectures), OS X 64-bit only
 		#import <AudioToolbox/AUAudioUnit.h>
 		#import <AudioToolbox/AUAudioUnitImplementation.h>
 		#import <AudioToolbox/AUParameters.h>
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AudioUnit.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AudioUnit.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AudioUnit.h	2016-05-11 16:31:24.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AudioUnit.h	2016-06-26 06:32:17.000000000 +0200
@@ -27,9 +27,6 @@
 	#endif
 
 		#include <AudioToolbox/AudioCodec.h>
-		#ifdef __OBJC__
-			#import <AudioToolbox/AUCocoaUIView.h>
-		#endif
 
 #else
 	#include <AudioComponent.h>
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AudioUnitProperties.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AudioUnitProperties.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AudioUnitProperties.h	2016-05-11 16:31:24.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AudioUnitProperties.h	2016-06-26 06:32:17.000000000 +0200
@@ -151,6 +151,7 @@
 						
 	@constant		kAudioUnitProperty_ParameterInfo
 						Scope:			Any
+						Element:		AudioUnitParameterID of the parameter being queried
 						Value Type:		AudioUnitParameterInfo
 						Access:			Read
 						
@@ -231,6 +232,7 @@
 	
 	@constant		kAudioUnitProperty_ParameterValueStrings
 						Scope:			Any
+						Element:		AudioUnitParameterID of the parameter being queried 
 						Value Type:		CFArrayRef
 						Access:			Read
 						
@@ -400,6 +402,7 @@
 	
 	@constant		kAudioUnitProperty_ParameterIDName
 						Scope:				any
+						Element:			AudioUnitParameterID of the parameter being queried
 						Value Type:			AudioUnitParameterIDName
 						Access:				read
 
@@ -749,6 +752,12 @@
 						parameters, via this property. The size of the array passed to
 						AudioUnitGetProperty controls the number of AudioUnitParameter values
 						returned.
+    @constant       kAudioUnitProperty_SupportsMPE
+                        Scope:          Global
+                        Value Type:     UInt32
+                        Access:         read
+                        
+                        Indicates whether an audio unit supports Multi-dimensional Polyphonic Expression.
 */
 CF_ENUM(AudioUnitPropertyID)
 {
@@ -793,6 +802,7 @@
 	kAudioUnitProperty_ClassInfoFromDocument		= 50,
 	kAudioUnitProperty_RequestViewController		= 56,
 	kAudioUnitProperty_ParametersForOverview		= 57,
+	kAudioUnitProperty_SupportsMPE					= 58,
 
 	kAudioUnitProperty_FastDispatch					= 5,
 	kAudioUnitProperty_SetExternalBuffer			= 15,
@@ -2101,12 +2111,12 @@
 						
 	@constant		kAudioOutputUnitProperty_ChannelMap
 	@discussion			Scope:			Input/Output
-						Value Type:		Array of UInt32
+						Value Type:		Array of SInt32
 						Access:			Read / Write
 
 						This will also work with AUConverter. This property is used to map input channels from an input (source) to a destination.
 						The number of channels represented in the channel map is the number of channels of the destination. The channel map entries
-						contain a channel number of the source that should be mapped to that destination channel. If -1 is specified, than that 
+						contain a channel number of the source that should be mapped to that destination channel. If -1 is specified, then that 
 						destination channel will not contain any channel from the source (so it will be silent)
 						
 	@constant		kAudioOutputUnitProperty_EnableIO

```