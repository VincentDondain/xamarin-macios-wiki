#CoreMIDI.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMIDI.framework/Headers/MIDIServices.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMIDI.framework/Headers/MIDIServices.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMIDI.framework/Headers/MIDIServices.h	2015-10-03 01:52:03.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMIDI.framework/Headers/MIDIServices.h	2016-05-16 05:34:35.000000000 +0200
@@ -1969,8 +1969,8 @@
 */
 extern OSStatus
 MIDIObjectFindByUniqueID(	MIDIUniqueID 		inUniqueID,
-							MIDIObjectRef *		outObject,
-							MIDIObjectType *	outObjectType)
+							MIDIObjectRef * __nullable outObject,
+							MIDIObjectType * __nullable outObjectType)
 							
 															__OSX_AVAILABLE_STARTING(__MAC_10_2, __IPHONE_4_2);
 

```