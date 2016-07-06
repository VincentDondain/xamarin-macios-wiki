#CoreMIDI.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreMIDI.framework/Headers/MIDIServices.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreMIDI.framework/Headers/MIDIServices.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreMIDI.framework/Headers/MIDIServices.h	2015-08-23 01:22:31.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreMIDI.framework/Headers/MIDIServices.h	2016-05-16 05:34:35.000000000 +0200
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