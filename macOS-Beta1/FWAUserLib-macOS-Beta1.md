#FWAUserLib.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/FWAUserLib.framework/Headers/AppleFWAudioUserClientCommon.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/FWAUserLib.framework/Headers/AppleFWAudioUserClientCommon.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/FWAUserLib.framework/Headers/AppleFWAudioUserClientCommon.h	2015-08-23 01:26:09.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/FWAUserLib.framework/Headers/AppleFWAudioUserClientCommon.h	2016-05-11 16:08:39.000000000 +0200
@@ -14,14 +14,14 @@
 #ifndef _AppleFWAudioUserClientCommon_H
 #define _AppleFWAudioUserClientCommon_H
 
-#define CURRENT_DEVICE_STATUS_VERSION (0x00012000)
+#define CURRENT_DEVICE_STATUS_VERSION	(0x00012000)
 
 #define kNumInputClientBuffers			1
-#define kMIDIInputClientBufferSize 		(2 * 32)
-#define kMIDIInputRingBufferSize 		(8 * kMIDIInputClientBufferSize * kNumInputClientBuffers )
+#define kMIDIInputClientBufferSize		(2 * 32 )
+#define kMIDIInputRingBufferSize		(8 * kMIDIInputClientBufferSize * kNumInputClientBuffers )
 
 #define kNumOutputClientBuffers			1
-#define kMIDIOutputClientBufferSize 	(2 * 32)
+#define kMIDIOutputClientBufferSize		(2 * 32)
 #define kMIDIOutputRingBufferSize		(8 * kMIDIOutputClientBufferSize *  kNumOutputClientBuffers)
 
 #define kFWAStreamIdentSize 			(36)
@@ -32,7 +32,7 @@
 #define kMIDIPropertiesIsPrivateKey		"MIDIPropertyIsPrivate"
 #define kMIDIPropertiesIsEmbeddedKey	"MIDIPropertyIsEmbedded"
 
-#define kFWAGetCurrentClockSourcePlugKey	'clkp'
+#define kFWAGetCurrentClockSourcePlugKey 'clkp'
 
 #define kFWAMaxPropertyKeyLength (256)
 #define kFWAMaxPropertyValueLength (4096 - (kFWAMaxPropertyKeyLength + 8))
@@ -139,7 +139,7 @@
 
 // Moved to AppleFWAudioUserLib.cpp
 // update this with the version of the driver in xxxx.xxxx
-#define  kFWADeviceStatusCurrentVersion (CURRENT_DEVICE_STATUS_VERSION)
+#define kFWADeviceStatusCurrentVersion (0x00012000)
 
 typedef struct FWADeviceStatus
 {
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/FWAUserLib.framework/Headers/FWAUserLib.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/FWAUserLib.framework/Headers/FWAUserLib.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/FWAUserLib.framework/Headers/FWAUserLib.h	2015-08-23 01:26:09.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/FWAUserLib.framework/Headers/FWAUserLib.h	2016-05-11 16:08:39.000000000 +0200
@@ -5,7 +5,7 @@
  
      Version:   Mac OS X
  
-     Copyright � 2001-2013 Apple Computer, Inc. All rights reserved.
+     Copyright � 2001-2013 Apple Computer, Inc. All rights reserved.
  
      Bugs?:      For bug reports, consult the following page on
                  the World Wide Web:
@@ -23,37 +23,40 @@
 		&lt;FWAUserLib/AppleFWAudioUserLib.h&gt;
 */
 
+
 // <rdar://problem/11755857> Apply FWAUserLib framework headerdoc patch
 
 #include 	<IOKit/firewire/IOFireWireFamilyCommon.h>
 #include 	<FWAUserLib/AppleFWAudioUserClientCommon.h>
 
+#pragma clang arc_cf_code_audited begin
+
 /*! Opaque pointer to userland FWARefRec */
-typedef struct OpaqueFWARef				*FWARef;
+ typedef  struct  OpaqueFWARef 				* FWARef;
 
 /*! Opaque kernel pointer to AM824Channel */
-typedef struct OpaqueFWAIsochStreamRef	*FWAIsochStreamRef;
+typedef struct OpaqueFWAIsochStreamRef	* FWAIsochStreamRef;
 
 /*! Opaque kernel pointer to AppleLocalAudioDevice */
-typedef struct OpaqueFWADeviceRef		*FWADeviceRef;
+typedef struct OpaqueFWADeviceRef		* FWADeviceRef;
 
 /*! Opaque kernel pointer to AppleFWAudioEngineNub */
-typedef struct OpaqueFWAEngineRef		*FWAEngineRef;
+typedef struct OpaqueFWAEngineRef		* FWAEngineRef;
 
 /*! Opaque kernel pointer to AppleFWAudioStream. */
-typedef struct OpaqueFWAAudioStreamRef	*FWAAudioStreamRef;
+typedef struct OpaqueFWAAudioStreamRef	* FWAAudioStreamRef;
 
 /*! Opaque kernel pointer to AppleFWAudioMIDIStream. */
-typedef struct OpaqueFWAMIDIStreamRef	*FWAMIDIStreamRef;
+typedef struct OpaqueFWAMIDIStreamRef	* FWAMIDIStreamRef;
 
 /*! Opaque kernel pointer to AppleFWAudioMIDIPlug. */
-typedef struct OpaqueFWAMIDIPlugRef		*FWAMIDIPlugRef;
+typedef struct OpaqueFWAMIDIPlugRef		* FWAMIDIPlugRef;
 
 /*! Opaque kernel pointer to AppleFWAudioStream. */
-typedef struct OpaqueFWAAudioPlugRef	*FWAAudioPlugRef;
+typedef struct OpaqueFWAAudioPlugRef	* FWAAudioPlugRef;
 
 /*! Opaque kernel pointer to AppleFWAudioMIDIDeviceNub. */
-typedef struct OpaqueFWAMIDIDeviceNubRef *FWAMIDIDeviceNubRef;
+typedef struct OpaqueFWAMIDIDeviceNubRef * FWAMIDIDeviceNubRef;
 
 #if __cplusplus
 extern "C" {
@@ -77,7 +80,7 @@
 	 * @param deviceCount On input, pass in the size of the array; on output, deviceCount contains the number of nodeIDs returned in the array.
 	 * @result OSStatus
 	 */
-	OSStatus FWACountDevices( UInt16* deviceNodeIDArray,UInt16* deviceCount );
+	OSStatus FWACountDevices(  UInt16* deviceNodeIDArray, UInt16*  deviceCount  ) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAOpen
@@ -89,7 +92,7 @@
 	 * @param outRef On return, the FWARef for the device.
 	 * @result OSStatus
 	 */
-	OSStatus FWAOpen(UInt32 nodeID, FWARef* outRef );
+	OSStatus FWAOpen(UInt32 nodeID, FWARef  * outRef  ) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAOpenLocal
@@ -109,7 +112,7 @@
 	 * @param outRef On return, an FWARef that represents the FireWire audio service attached to the Macintosh local FireWire node.
 	 * @result OSStatus
 	 */
-	OSStatus FWAOpenLocal( FWARef* outRef );
+	OSStatus FWAOpenLocal( FWARef*  outRef ) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAClose
@@ -118,7 +121,7 @@
 	 * @param inRef The FWARef of the device to close.
 	 * @result OSStatus
 	 */     
-	OSStatus FWAClose( FWARef 	inRef );
+	OSStatus FWAClose( FWARef 	inRef ) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWARead
@@ -132,7 +135,7 @@
 	 * @param inDataPtr
 	 * @result OSStatus
 	 */
-	OSStatus FWARead( FWARef inRef, UInt8 inAddress, UInt8 inSubAddress, ByteCount	 inDataSize, void * inDataPtr );
+	OSStatus FWARead( FWARef inRef, UInt8 inAddress, UInt8 inSubAddress, ByteCount	 inDataSize, void * inDataPtr ) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAWrite
@@ -146,7 +149,7 @@
 	 * @param inDataPtr
 	 * @result OSStatus
 	 */
-	OSStatus FWAWrite( FWARef inRef, UInt8 inAddress, UInt8	 inSubAddress, ByteCount inDataSize,  const void *	inDataPtr );
+	OSStatus FWAWrite( FWARef inRef, UInt8 inAddress, UInt8	 inSubAddress, ByteCount inDataSize,  const void *	inDataPtr ) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 	// mLan support
@@ -161,7 +164,7 @@
 	 * @param outGeneration The current bus generation.
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetNodeID(FWARef inRef, UInt32 *outNodeID, UInt32 *outGeneration);
+	OSStatus FWAGetNodeID(FWARef  inRef, UInt32 *outNodeID, UInt32 * outGeneration) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetGUID
@@ -171,7 +174,7 @@
 	 * @param guid The address of a UInt64 to hold the device GUID.
 	 * @result OSStatus
 	 */     
-	OSStatus FWAGetGUID(FWARef inRef, UInt64 *guid);
+	OSStatus FWAGetGUID(FWARef inRef, UInt64 *guid) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetMacGUID
@@ -181,7 +184,7 @@
 	 * @param guid The address of a UInt64 to hold the Macintosh computer's GUID.
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetMacGUID(FWARef inRef, UInt64 *guid);
+	OSStatus FWAGetMacGUID(FWARef inRef, UInt64 *guid) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAReadQuadlet
@@ -192,7 +195,7 @@
 	 * @param outData A pointer to a UInt32 to hold the quadlet that was read.
 	 * @result OSStatus
 	 */
-	OSStatus FWAReadQuadlet(FWARef inRef, FWAddressPtr address, UInt32 *outData);
+	OSStatus FWAReadQuadlet(FWARef inRef, FWAddressPtr address, UInt32 *outData) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAReadBlock
@@ -204,7 +207,7 @@
 	 * @param outData A pointer to the data that was read.
 	 * @result OSStatus
 	 */
-	OSStatus FWAReadBlock(FWARef inRef, 	FWAddressPtr address, UInt32* size, UInt8 *outData);
+	OSStatus FWAReadBlock(FWARef inRef, 	FWAddressPtr address, UInt32* size, UInt8 *outData) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAExecuteAVC
@@ -217,7 +220,7 @@
 	 * @param responseSize A pointer to the size of the response.
 	 * @result OSStatus
 	 */
-	OSStatus FWAExecuteAVC(FWARef inRef, UInt8* cmd,UInt32 cmdSize,UInt8* response,UInt32* responseSize);
+	OSStatus FWAExecuteAVC(FWARef inRef, UInt8* cmd,UInt32 cmdSize,UInt8* response,UInt32* responseSize) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAWriteQuadlet
@@ -228,7 +231,7 @@
 	 * @param data The data to write.
 	 * @result OSStatus
 	 */
-	OSStatus FWAWriteQuadlet(FWARef inRef, FWAddressPtr address, UInt32 data);
+	OSStatus FWAWriteQuadlet(FWARef inRef, FWAddressPtr address, UInt32 data) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAWriteBlock
@@ -240,7 +243,7 @@
 	 * @param data A pointer to the data to write.
 	 * @result OSStatus
 	 */
-	OSStatus FWAWriteBlock(FWARef inRef, FWAddressPtr address, UInt32 size, const UInt8 *data);
+	OSStatus FWAWriteBlock(FWARef inRef, FWAddressPtr address, UInt32 size, const UInt8 *data) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWACreateMIDIStream
@@ -254,7 +257,7 @@
 	  * @param midiStreamRef On return, the reference to the MIDI stream to use in other MIDI functions.
 	 * @result OSStatus
 	 */
-	OSStatus FWACreateMIDIStream(FWARef inRef, UInt32 midiIO, UInt32 bufSizeInBytes, void * buf, UInt32 sequenceNum, UInt32 *midiStreamRef);
+	OSStatus FWACreateMIDIStream(FWARef inRef, UInt32 midiIO, UInt32 bufSizeInBytes, void * buf, UInt32 sequenceNum, UInt32 *midiStreamRef) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWADisposeMIDIStream
@@ -264,19 +267,19 @@
 	 * @param midiStreamRef The MIDI stream reference created with @link FWACreateMIDIStream FWACreateMIDIStream@/link.
 	 * @result OSStatus
 	 */
-	OSStatus FWADisposeMIDIStream(FWARef inRef, UInt32 midiStreamRef);
+	OSStatus FWADisposeMIDIStream(FWARef inRef, UInt32 midiStreamRef) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAWriteMIDIData
 	 * @abstract This function has been deprecated. Use @link FWAWriteMIDIDataAsync FWAWriteMIDIDataAsync@/link instead.
 	 */
-	OSStatus FWAWriteMIDIData(FWARef inRef,  UInt32 midiStreamRef, UInt32 writeMsgLength, UInt8 * buf);
+	OSStatus FWAWriteMIDIData(FWARef inRef,  UInt32 midiStreamRef, UInt32 writeMsgLength, UInt8 * buf) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAReadMIDIData
 	 * @abstract This function has been deprecated. Use @link FWAReadMIDIDataAsync FWAReadMIDIDataAsync@/link instead.
 	 */
-	OSStatus FWAReadMIDIData( FWARef inRef,  UInt32 midiStreamRef, FWAMIDIReadBuf *buf);
+	OSStatus FWAReadMIDIData( FWARef inRef,  UInt32 midiStreamRef, FWAMIDIReadBuf *buf) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 #pragma mark -- V2
@@ -292,7 +295,7 @@
 	 * @result OSStatus
 	 */
 
-	OSStatus FWAGetCycleTimeOffset(FWARef inRef, UInt32* cycleTimeOffset);
+	OSStatus FWAGetCycleTimeOffset(FWARef inRef, UInt32* cycleTimeOffset) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWASetCycleTimeOffset
@@ -302,7 +305,7 @@
 	 * @param cycleTimeOffset The cycle time offset in nanoseconds.
 	 * @result OSStatus
 	 */
-	OSStatus FWASetCycleTimeOffset(FWARef inRef, UInt32 cycleTimeOffset);
+	OSStatus FWASetCycleTimeOffset(FWARef inRef, UInt32 cycleTimeOffset) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetVendorID
@@ -313,7 +316,7 @@
 	 * @param vendorID On return, a pointer to the vendor ID of the device.
 	 * @result OSStatus
 	 */     
-	OSStatus FWAGetVendorID(FWARef inRef, UInt32 * vendorID);
+	OSStatus FWAGetVendorID(FWARef inRef, UInt32 * vendorID) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetDeviceName
@@ -324,7 +327,7 @@
 	 * @param name On return, a pointer to the device name.
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetDeviceName(FWARef inRef, char * name);
+	OSStatus FWAGetDeviceName(FWARef inRef, char * name) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetVendorName
@@ -335,7 +338,7 @@
 	 * @param name On return, a pointer to the device name.
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetVendorName(FWARef inRef, char * name);
+	OSStatus FWAGetVendorName(FWARef inRef, char * name) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAIsMIDICapable
@@ -345,7 +348,7 @@
 	 * @param supportsMIDI On return, a pointer to a Boolean value (TRUE if the device supports MIDI, FALSE if it does not).
 	 * @result OSStatus
 	 */
-	OSStatus FWAIsMIDICapable(FWARef inRef, bool* supportsMIDI);
+	OSStatus FWAIsMIDICapable(FWARef inRef, bool* supportsMIDI) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetNumMIDIInputPlugs
@@ -355,7 +358,7 @@
 	 * @param plugs On return, a pointer to the number of MIDI input plugs.
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetNumMIDIInputPlugs(FWARef inRef, UInt32* plugs);
+	OSStatus FWAGetNumMIDIInputPlugs(FWARef inRef, UInt32* plugs) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetNumMIDIOutputPlugs
@@ -365,7 +368,7 @@
 	 * @param plugs On return, a pointer to the number of MIDI output plugs.
 	 * @result OSStatus 
 	 */
-	OSStatus FWAGetNumMIDIOutputPlugs(FWARef inRef, UInt32* plugs);
+	OSStatus FWAGetNumMIDIOutputPlugs(FWARef inRef, UInt32* plugs) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWASetNumMIDIInputPlugs
@@ -375,7 +378,7 @@
 	 * @param plugs The number of input plugs.
 	 * @result OSStatus
 	 */
-	OSStatus FWASetNumMIDIInputPlugs(FWARef inRef, UInt32 plugs);
+	OSStatus FWASetNumMIDIInputPlugs(FWARef inRef, UInt32 plugs) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWASetNumMIDIOutputPlugs
@@ -385,7 +388,7 @@
 	 * @param plugs The number of output plugs.
 	 * @result OSStatus
 	 */
-	OSStatus FWASetNumMIDIOutputPlugs(FWARef inRef, UInt32 plugs);
+	OSStatus FWASetNumMIDIOutputPlugs(FWARef inRef, UInt32 plugs) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetNumAudioInputPlugs
@@ -395,7 +398,7 @@
 	 * @param plugs On return, a pointer to the number of audio input plugs.
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetNumAudioInputPlugs(FWARef inRef, UInt32* plugs);
+	OSStatus FWAGetNumAudioInputPlugs(FWARef inRef, UInt32* plugs) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetNumAudioOutputPlugs
@@ -405,7 +408,7 @@
 	 * @param plugs On return, a pointer to the number of audio output plugs.
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetNumAudioOutputPlugs(FWARef inRef, UInt32* plugs);
+	OSStatus FWAGetNumAudioOutputPlugs(FWARef inRef, UInt32* plugs) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWACreateAudioStream
@@ -417,7 +420,7 @@
 	 * @param sequenceNum
 	 * @result OSStatus
 	 */
-	OSStatus FWACreateAudioStream(FWARef inRef,UInt32 audioIO, UInt32 *audioStreamRef, UInt32 *sequenceNum);
+	OSStatus FWACreateAudioStream(FWARef inRef,UInt32 audioIO, UInt32 *audioStreamRef, UInt32 *sequenceNum) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 #pragma mark -- V3
@@ -432,7 +435,7 @@
 	 * @param audioStreamRef
 	 * @result OSStatus
 	 */
-	OSStatus FWADisposeAudioStream(FWARef inRef, UInt32 audioStreamRef);
+	OSStatus FWADisposeAudioStream(FWARef inRef, UInt32 audioStreamRef) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetDeviceSampleRate 
@@ -442,7 +445,7 @@
 	 * @param rate On return, a pointer to the current sample rate value.
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetDeviceSampleRate(FWARef inRef,UInt32* rate);
+	OSStatus FWAGetDeviceSampleRate(FWARef inRef,UInt32* rate) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetDeviceSendMode
@@ -452,7 +455,7 @@
 	 * @param mode On return, a pointer to the send mode (can be either IEC60958 or Raw audio).
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetDeviceSendMode(FWARef inRef,UInt32* mode);
+	OSStatus FWAGetDeviceSendMode(FWARef inRef,UInt32* mode) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetDeviceStatus
@@ -463,7 +466,7 @@
 	 * @param inSize The size of the status structure.
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetDeviceStatus( FWARef inRef, void *outData, UInt32 inSize);
+	OSStatus FWAGetDeviceStatus( FWARef inRef, void *outData, UInt32 inSize) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetDeviceStreamInfo
@@ -477,7 +480,7 @@
 	 * @param outputIsochChan The isochronous channel used for the output stream.
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetDeviceStreamInfo(FWARef inRef, UInt32 audioStreamRef, UInt32* numInput,UInt32* inputIsochChan, UInt32* numOutput,UInt32* outputIsochChan);
+	OSStatus FWAGetDeviceStreamInfo(FWARef inRef, UInt32 audioStreamRef, UInt32* numInput,UInt32* inputIsochChan, UInt32* numOutput,UInt32* outputIsochChan) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 	// Async methods added for MIDI
@@ -493,7 +496,7 @@
 	 * @param refcon User value that is returned when the event source is triggered.
 	 * @result OSStatus
 	 */
-	OSStatus FWAInitAEvntSource(FWARef inRef, CFRunLoopSourceRef *source, void * refcon);
+	OSStatus FWAInitAEvntSource(FWARef inRef, CFRunLoopSourceRef *source, void * refcon) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function CreateAsyncWakePort
@@ -503,7 +506,7 @@
 	 * @param notifyPort On return, a Mach port (mach_port_t) for notification.
 	 * @result OSStatus
 	 */
-	OSStatus CreateAsyncWakePort(FWARef inRef, mach_port_t *notifyPort);
+	OSStatus CreateAsyncWakePort(FWARef inRef, mach_port_t *notifyPort) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetAEvntSource
@@ -512,7 +515,7 @@
 	 * @param inRef The FWARef returned in @link FWAOpen FWAOpen@/link.
 	 * @result The run loop to pass in @link FWAInitAEvntSource FWAInitAEvntSource@/link.
 	 */
-	CFRunLoopSourceRef FWAGetAEvntSource(FWARef inRef);
+	CFRunLoopSourceRef FWAGetAEvntSource(FWARef inRef) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAWriteMIDIDataAsync
@@ -525,7 +528,7 @@
 	 * @param refCon User value that is returned when the notification is sent.
 	 * @result OSStatus
 	 */
-	OSStatus FWAWriteMIDIDataAsync(FWARef inRef, UInt32 midiStreamRef, UInt32 writeMsgLength, IOAsyncCallback1 callback, void * refCon);
+	OSStatus FWAWriteMIDIDataAsync(FWARef inRef, UInt32 midiStreamRef, UInt32 writeMsgLength, IOAsyncCallback1 callback, void * refCon) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAReadMIDIDataAsync
@@ -538,7 +541,7 @@
 	 * @param refCon User value that is returned when the notification is sent.
 	 * @result OSStatus
 	 */
-	OSStatus FWAReadMIDIDataAsync(FWARef inRef, UInt32 midiStreamRef, UInt32 readBufSize, IOAsyncCallback2 callback, void * refCon);
+	OSStatus FWAReadMIDIDataAsync(FWARef inRef, UInt32 midiStreamRef, UInt32 readBufSize, IOAsyncCallback2 callback, void * refCon) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 #pragma mark -- V4
@@ -558,7 +561,7 @@
 	 * @param update
 	 * @result Because this function is deprecated, the return value indicates it is unimplemented.
 	 */
-	OSStatus FWASetDeviceStreamInfo(FWARef inRef, UInt32 audioStreamRef, UInt32 numInput,UInt32 inputIsochChan, UInt32 numOutput,UInt32 outputIsochChan,bool update);
+	OSStatus FWASetDeviceStreamInfo(FWARef inRef, UInt32 audioStreamRef, UInt32 numInput,UInt32 inputIsochChan, UInt32 numOutput,UInt32 outputIsochChan,bool update) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 	
 	//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 #pragma mark -- V5
@@ -571,7 +574,7 @@
 	 * @param inRef The FWARef returned in @link FWAOpen FWAOpen@/link or in @link FWAOpenLocal FWAOpenLocal@/link.
 	 * @result OSStatus
 	 */     
-	OSStatus FWASyncUpDevice(FWARef inRef);
+	OSStatus FWASyncUpDevice(FWARef inRef) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetMaxSpeed
@@ -581,7 +584,7 @@
 	 * @param speed On return, a pointer to an IOFWSpeed that contains the speed.
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetMaxSpeed(FWARef inRef,IOFWSpeed* speed);
+	OSStatus FWAGetMaxSpeed(FWARef inRef,IOFWSpeed* speed) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetMaxIsochChannels
@@ -592,7 +595,7 @@
 	 * @param outChannels On return, a pointer to the number of isochronous output channels.
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetMaxIsochChannels(FWARef inRef, UInt32* inChannels, UInt32* outChannels);
+	OSStatus FWAGetMaxIsochChannels(FWARef inRef, UInt32* inChannels, UInt32* outChannels) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetMaxSequences
@@ -602,7 +605,7 @@
 	 * @param numSequences On return, a pointer to the number of sequences.
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetMaxSequences(FWARef inRef, UInt32* numSequences);
+	OSStatus FWAGetMaxSequences(FWARef inRef, UInt32* numSequences) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	 /*!
 	 * @function FWAGetSupportedSampleRates
@@ -613,7 +616,7 @@
 	 * @param count On input, a pointer to the number of sample rates the array can hold; on return, the actual number of sample rates returned.
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetSupportedSampleRates(FWARef inRef, UInt32* sampleRates, UInt32* count);
+	OSStatus FWAGetSupportedSampleRates(FWARef inRef, UInt32* sampleRates, UInt32* count) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetSupportedAudioTypes
@@ -624,7 +627,7 @@
 	 * @param count On input, a pointer to the number of audio types the array can hold; on return, the actual number of audio types returned.
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetSupportedAudioTypes(FWARef inRef, FWAudioType* audioTypes, UInt32* count);
+	OSStatus FWAGetSupportedAudioTypes(FWARef inRef, FWAudioType* audioTypes, UInt32* count) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetCurrentIsochStreamRefs
@@ -635,7 +638,7 @@
 	 * @param count On input, a pointer to the number of audio types the array can hold; on return, the actual number of audio types returned.
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetCurrentIsochStreamRefs(FWARef inRef, FWAIsochStreamRef* isochStreamRef, UInt32* count);
+	OSStatus FWAGetCurrentIsochStreamRefs(FWARef inRef, FWAIsochStreamRef* isochStreamRef, UInt32* count) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetIsochStreamState
@@ -646,7 +649,7 @@
 	 * @param state A pointer to an FWAStreamState that contains the current state (can be stopped, running, paused, or resumed).
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetIsochStreamState(FWARef inRef, FWAIsochStreamRef isochStreamRef,FWAStreamState* state);
+	OSStatus FWAGetIsochStreamState(FWARef inRef, FWAIsochStreamRef isochStreamRef,FWAStreamState* state) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetIsochStreamDirection
@@ -657,7 +660,7 @@
 	 * @param direction A pointer to an FWAStreamDirection that contains the current stream direction (can be out or in).
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetIsochStreamDirection(FWARef inRef, FWAIsochStreamRef isochStreamRef,FWAStreamDirection* direction);
+	OSStatus FWAGetIsochStreamDirection(FWARef inRef, FWAIsochStreamRef isochStreamRef,FWAStreamDirection* direction) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetIsochStreamChannelID
@@ -668,7 +671,7 @@
 	 * @param channelID On return, a pointer to the current isochronous stream channel ID.
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetIsochStreamChannelID(FWARef inRef, FWAIsochStreamRef isochStreamRef,UInt32* channelID);
+	OSStatus FWAGetIsochStreamChannelID(FWARef inRef, FWAIsochStreamRef isochStreamRef,UInt32* channelID) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWASetIsochStreamChannelID
@@ -679,7 +682,7 @@
 	 * @param channelID The value to which the isochronous stream channel ID should be set.
 	 * @result OSStatus
 	 */
-	OSStatus FWASetIsochStreamChannelID(FWARef inRef, FWAIsochStreamRef isochStreamRef,UInt32 channelID);
+	OSStatus FWASetIsochStreamChannelID(FWARef inRef, FWAIsochStreamRef isochStreamRef,UInt32 channelID) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetIsochStreamSampleRate
@@ -690,7 +693,7 @@
 	 * @param rate On return, a pointer to the isochronous stream sample rate.
 	 * @result OSStatus 
 	 */
-	OSStatus FWAGetIsochStreamSampleRate(FWARef inRef, FWAIsochStreamRef isochStreamRef,UInt32* rate);
+	OSStatus FWAGetIsochStreamSampleRate(FWARef inRef, FWAIsochStreamRef isochStreamRef,UInt32* rate) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWASetIsochStreamSampleRate
@@ -701,7 +704,7 @@
 	 * @param rate The sample rate to which the isochronous stream should be set.
 	 * @result OSStatus 
 	 */
-	OSStatus FWASetIsochStreamSampleRate(FWARef inRef, FWAIsochStreamRef isochStreamRef,UInt32 rate);
+	OSStatus FWASetIsochStreamSampleRate(FWARef inRef, FWAIsochStreamRef isochStreamRef,UInt32 rate) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetIsochStreamOutputSpeed
@@ -712,7 +715,7 @@
 	 * @param speed On return, a pointer to an IOFWSpeed that contains the speed.
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetIsochStreamOutputSpeed(FWARef inRef, FWAIsochStreamRef isochStreamRef,IOFWSpeed* speed);
+	OSStatus FWAGetIsochStreamOutputSpeed(FWARef inRef, FWAIsochStreamRef isochStreamRef,IOFWSpeed* speed) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWASetIsochStreamOutputSpeed
@@ -723,7 +726,7 @@
 	 * @param speed The speed to which the isochronous output stream should be set.
 	 * @result OSStatus
 	 */
-	OSStatus FWASetIsochStreamOutputSpeed(FWARef inRef, FWAIsochStreamRef isochStreamRef,IOFWSpeed speed);
+	OSStatus FWASetIsochStreamOutputSpeed(FWARef inRef, FWAIsochStreamRef isochStreamRef,IOFWSpeed speed) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetIsochStreamAudioType 
@@ -734,7 +737,7 @@
 	 * @param type On return, a pointer to an FWAudioType that contains the type (can be IEC60598, raw audio, or MIDI).
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetIsochStreamAudioType(FWARef inRef, FWAIsochStreamRef isochStreamRef, FWAudioType* type);
+	OSStatus FWAGetIsochStreamAudioType(FWARef inRef, FWAIsochStreamRef isochStreamRef, FWAudioType* type) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWASetIsochStreamAudioType 
@@ -745,7 +748,7 @@
 	 * @param type The audio type to which the isochronous stream should be set.
 	 * @result OSStatus
 	 */
-	OSStatus FWASetIsochStreamAudioType(FWARef inRef, FWAIsochStreamRef isochStreamRef, FWAudioType type);
+	OSStatus FWASetIsochStreamAudioType(FWARef inRef, FWAIsochStreamRef isochStreamRef, FWAudioType type) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWACreateIsochStream
@@ -760,7 +763,7 @@
 	 * @param isochStreamRef On return, an FWAIsochStreamRef representing this isochronous stream.
 	 * @result OSStatus
 	 */
-	OSStatus FWACreateIsochStream(FWARef inRef, UInt32 channelNumber,FWAStreamDirection direction,UInt32 numAudioChannels,UInt32 numMIDIChannels, FWAIsochStreamRef* isochStreamRef );
+	OSStatus FWACreateIsochStream(FWARef inRef, UInt32 channelNumber,FWAStreamDirection direction,UInt32 numAudioChannels,UInt32 numMIDIChannels, FWAIsochStreamRef* isochStreamRef ) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWADisposeIsochStream
@@ -770,7 +773,7 @@
 	 * @param isochStreamRef The FWAIsochStreamRef created with @link FWACreateIsochStream FWACreateIsochStream@/link.
 	 * @result OSStatus
 	 */
-	OSStatus FWADisposeIsochStream(FWARef inRef,FWAIsochStreamRef isochStreamRef );
+	OSStatus FWADisposeIsochStream(FWARef inRef,FWAIsochStreamRef isochStreamRef ) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAStartIsochStream
@@ -780,7 +783,7 @@
 	 * @param isochStreamRef The FWAIsochStreamRef created with @link FWACreateIsochStream FWACreateIsochStream@/link.
 	 * @result OSStatus
 	 */     
-	OSStatus FWAStartIsochStream(FWARef inRef, FWAIsochStreamRef isochStreamRef);
+	OSStatus FWAStartIsochStream(FWARef inRef, FWAIsochStreamRef isochStreamRef) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAStopIsochStream
@@ -790,7 +793,7 @@
 	 * @param isochStreamRef The FWAIsochStreamRef created with @link FWACreateIsochStream FWACreateIsochStream@/link.
 	 * @result OSStatus
 	 */
-	OSStatus FWAStopIsochStream(FWARef inRef,FWAIsochStreamRef isochStreamRef );
+	OSStatus FWAStopIsochStream(FWARef inRef,FWAIsochStreamRef isochStreamRef ) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetIsochStreamAudioSequenceCount
@@ -801,7 +804,7 @@
 	 * @param numAudioSequence On return, a pointer to the audio sequence count.
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetIsochStreamAudioSequenceCount(FWARef inRef, FWAIsochStreamRef isochStreamRef,UInt32* numAudioSequence);
+	OSStatus FWAGetIsochStreamAudioSequenceCount(FWARef inRef, FWAIsochStreamRef isochStreamRef,UInt32* numAudioSequence) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWASetIsochStreamAudioSequenceCount
@@ -812,7 +815,7 @@
 	 * @param numAudioSequence The number to which the isochronous stream audio sequence count should be set.
 	 * @result OSStatus
 	 */
-	OSStatus FWASetIsochStreamAudioSequenceCount(FWARef inRef, FWAIsochStreamRef isochStreamRef,UInt32 numAudioSequence);
+	OSStatus FWASetIsochStreamAudioSequenceCount(FWARef inRef, FWAIsochStreamRef isochStreamRef,UInt32 numAudioSequence) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetIsochStreamMIDISequenceCount
@@ -823,7 +826,7 @@
 	 * @param numMIDISequence On return, the sequence count of the MIDI stream.
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetIsochStreamMIDISequenceCount(FWARef inRef, FWAIsochStreamRef isochStreamRef,UInt32* numMIDISequence);
+	OSStatus FWAGetIsochStreamMIDISequenceCount(FWARef inRef, FWAIsochStreamRef isochStreamRef,UInt32* numMIDISequence) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWASetIsochStreamMIDISequenceCount
@@ -834,7 +837,7 @@
 	 * @param numMIDISequence The sequence count to which the MIDI stream should be set.
 	 * @result OSStatus
 	 */
-	OSStatus FWASetIsochStreamMIDISequenceCount(FWARef inRef, FWAIsochStreamRef isochStreamRef,UInt32 numMIDISequence);
+	OSStatus FWASetIsochStreamMIDISequenceCount(FWARef inRef, FWAIsochStreamRef isochStreamRef,UInt32 numMIDISequence) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 	
 	/*!
 	 * @function FWACreateFWAudioDevice
@@ -853,7 +856,7 @@
 	 * @param device On return, the FWADeviceRef representing the audio device.
 	 * @result OSStatus
 	 */
-	OSStatus FWACreateFWAudioDevice(FWARef inRef,const char * deviceName, UInt32 vendorID,const char* guid, FWADeviceRef* device);
+	OSStatus FWACreateFWAudioDevice(FWARef inRef,const char * deviceName, UInt32 vendorID,const char* guid, FWADeviceRef* device) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWADisposeFWAudioDevice
@@ -863,7 +866,7 @@
 	 * @param device The FWADeviceRef created with @link FWACreateFWAudioDevice FWACreateFWAudioDevice@/link.
 	 * @result OSStatus
 	 */
-	OSStatus FWADisposeFWAudioDevice(FWARef inRef,FWADeviceRef device);
+	OSStatus FWADisposeFWAudioDevice(FWARef inRef,FWADeviceRef device) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAStartFWAudioDevice
@@ -874,7 +877,7 @@
 	 * @param device The FWADeviceRef created with @link FWACreateFWAudioDevice FWACreateFWAudioDevice@/link.
 	 * @result OSStatus
 	 */
-	OSStatus FWAStartFWAudioDevice(FWARef inRef,FWADeviceRef device);
+	OSStatus FWAStartFWAudioDevice(FWARef inRef,FWADeviceRef device) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAStopFWAudioDevice
@@ -885,7 +888,7 @@
 	 * @param device The FWADeviceRef created with @link FWACreateFWAudioDevice FWACreateFWAudioDevice@/link.
 	 * @result OSStatus 
 	 */
-	OSStatus FWAStopFWAudioDevice(FWARef inRef,FWADeviceRef device);
+	OSStatus FWAStopFWAudioDevice(FWARef inRef,FWADeviceRef device) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWACreateFWAudioEngine
@@ -898,7 +901,7 @@
 	 * @param engine On return, the FWAEngineRef representing the audio engine.
 	 * @result OSStatus
 	 */
-	OSStatus FWACreateFWAudioEngine(FWARef inRef, FWADeviceRef owningDevice, bool hasInput, bool hasOutput, FWAEngineRef* engine);
+	OSStatus FWACreateFWAudioEngine(FWARef inRef, FWADeviceRef owningDevice, bool hasInput, bool hasOutput, FWAEngineRef* engine) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWADisposeFWAudioEngine
@@ -908,7 +911,7 @@
 	 * @param engine The FWAEngineRef created with @link FWACreateFWAudioEngine FWACreateFWAudioEngine@/link.
 	 * @result OSStatus
 	 */     
-	OSStatus FWADisposeFWAudioEngine(FWARef inRef, FWAEngineRef engine);
+	OSStatus FWADisposeFWAudioEngine(FWARef inRef, FWAEngineRef engine) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWACreateFWAudioStream
@@ -924,7 +927,7 @@
 	 * @param streamRef On return, the FWAAudioStreamRef representing this audio stream.
 	 * @result OSStatus
 	 */
-	OSStatus FWACreateFWAudioStream(FWARef inRef, FWAIsochStreamRef owningIsochStreamRef, UInt32 channelNumber,UInt32 direction,UInt32 numAudioChannels,char* streamName,UInt8* streamIdent, FWAAudioStreamRef* streamRef);
+	OSStatus FWACreateFWAudioStream(FWARef inRef, FWAIsochStreamRef owningIsochStreamRef, UInt32 channelNumber,UInt32 direction,UInt32 numAudioChannels,char* streamName,UInt8* streamIdent, FWAAudioStreamRef* streamRef) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWADisposeFWAudioStream
@@ -935,7 +938,7 @@
 	 * @result OSStatus
 	 */
 
-	OSStatus FWADisposeFWAudioStream(FWARef inRef, FWAAudioStreamRef streamRef );
+	OSStatus FWADisposeFWAudioStream(FWARef inRef, FWAAudioStreamRef streamRef ) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWACreateFWAudioMIDIStream
@@ -948,7 +951,7 @@
 	 * @param streamRef On return, the FWAMIDIStreamRef representing this MIDI stream.
 	 * @result OSStatus
 	 */
-	OSStatus FWACreateFWAudioMIDIStream(FWARef inRef, FWAIsochStreamRef owningIsochStreamRef, UInt32 sequenceNumber,UInt32 direction, FWAMIDIStreamRef* streamRef);
+	OSStatus FWACreateFWAudioMIDIStream(FWARef inRef, FWAIsochStreamRef owningIsochStreamRef, UInt32 sequenceNumber,UInt32 direction, FWAMIDIStreamRef* streamRef) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWADisposeFWAudioMIDIStream
@@ -958,7 +961,7 @@
 	 * @param streamRef The FWAMIDIStreamRef created with @link FWACreateFWAudioMIDIStream FWACreateFWAudioMIDIStream@/link.
 	 * @result OSStatus
 	 */
-	OSStatus FWADisposeFWAudioMIDIStream(FWARef inRef, FWAMIDIStreamRef streamRef );
+	OSStatus FWADisposeFWAudioMIDIStream(FWARef inRef, FWAMIDIStreamRef streamRef ) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWACreateFWAudioMIDIPlug
@@ -972,7 +975,7 @@
 	 * @param streamRef On return, the FWAMIDIPlugRef representing this MIDI plug.
 	 * @result OSStatus
 	 */
-	OSStatus FWACreateFWAudioMIDIPlug(FWARef inRef, FWAMIDIStreamRef owningMIDIStreamRef,UInt8 mpxID,char* plugName, UInt8* plugIdent, FWAMIDIPlugRef* streamRef);
+	OSStatus FWACreateFWAudioMIDIPlug(FWARef inRef, FWAMIDIStreamRef owningMIDIStreamRef,UInt8 mpxID,char* plugName, UInt8* plugIdent, FWAMIDIPlugRef* streamRef) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWADisposeFWAudioMIDIPlug
@@ -982,7 +985,7 @@
 	 * @param plugRef The FWAMIDIPlugRef created with @link FWACreateFWAudioMIDIPlug FWACreateFWAudioMIDIPlug @/link.
 	 * @result OSStatus
 	 */
-	OSStatus FWADisposeFWAudioMIDIPlug(FWARef inRef, FWAMIDIPlugRef plugRef );
+	OSStatus FWADisposeFWAudioMIDIPlug(FWARef inRef, FWAMIDIPlugRef plugRef ) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWAGetClockSource
@@ -993,7 +996,7 @@
 	 * @param sequence
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetClockSource(FWARef inRef, FWAIsochStreamRef *streamRef, UInt32 *sequence);
+	OSStatus FWAGetClockSource(FWARef inRef, FWAIsochStreamRef *streamRef, UInt32 *sequence) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*!
 	 * @function FWASetClockSource
@@ -1004,7 +1007,7 @@
 	 * @param sequence
 	 * @result OSStatus
 	 */
-	OSStatus FWASetClockSource(FWARef inRef, FWAIsochStreamRef streamRef,UInt32 sequence);
+	OSStatus FWASetClockSource(FWARef inRef, FWAIsochStreamRef streamRef,UInt32 sequence) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 #pragma mark -- V6
@@ -1022,7 +1025,7 @@
 	 * @param enable A Boolean value that indicates whether the AppleFWAudio_Disable property should be removed from or created in the I/O Registry.
 	 * @result OSStatus
 	 */
-	OSStatus FWASetAutoLoad(FWARef inRef, bool enable);
+	OSStatus FWASetAutoLoad(FWARef inRef, bool enable) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/* 
 	 * @function FWAGetProperty
@@ -1034,7 +1037,7 @@
 	 * @param size
 	 * @result OSStatus
 	 */
-	OSStatus FWAGetProperty(FWARef inRef, UInt32 propertyID, void * data,UInt32* size);
+	OSStatus FWAGetProperty(FWARef inRef, UInt32 propertyID, void * data,UInt32* size) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*
 	 * @function FWASetProperty
@@ -1046,7 +1049,7 @@
 	 * @param size
 	 * @result OSStatus
 	 */
-	OSStatus FWASetProperty(FWARef inRef, UInt32 propertyID, void * data,UInt32 size);
+	OSStatus FWASetProperty(FWARef inRef, UInt32 propertyID, void * data,UInt32 size) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 #pragma mark -- V7
@@ -1054,68 +1057,68 @@
 	/*! @group Version 7 */
 
 	/*! Description forthcoming. */
-	OSStatus FWASetPluginPath(FWARef inRef,FWAEngineRef engine,UInt32 vendorID, UInt32 modelID, const char* pluginPath);
+	OSStatus FWASetPluginPath(FWARef inRef,FWAEngineRef engine,UInt32 vendorID, UInt32 modelID, const char* pluginPath) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 	
 	/*! Description forthcoming. */
-	OSStatus FWACreateFWAudioPlug(FWARef inRef, FWAAudioStreamRef owningStream,UInt32 channelID,char* plugName, UInt8* plugIdent, FWAAudioPlugRef* streamRef);
+	OSStatus FWACreateFWAudioPlug(FWARef inRef, FWAAudioStreamRef owningStream,UInt32 channelID,char* plugName, UInt8* plugIdent, FWAAudioPlugRef* streamRef) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*! Description forthcoming. */
-	OSStatus FWADisposeFWAudioPlug(FWARef inRef, FWAAudioPlugRef plugRef );
+	OSStatus FWADisposeFWAudioPlug(FWARef inRef, FWAAudioPlugRef plugRef ) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 	
 	/*! Description forthcoming. */
-	OSStatus FWAGetFWAudioMIDIPlugChannel(FWARef inRef, FWAMIDIPlugRef streamRef,UInt32* channelID);
+	OSStatus FWAGetFWAudioMIDIPlugChannel(FWARef inRef, FWAMIDIPlugRef streamRef,UInt32* channelID) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*! Description forthcoming. */
-	OSStatus FWASetFWAudioMIDIPlugChannel(FWARef inRef, FWAMIDIPlugRef streamRef,UInt32 channelID);
+	OSStatus FWASetFWAudioMIDIPlugChannel(FWARef inRef, FWAMIDIPlugRef streamRef,UInt32 channelID) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*! Description forthcoming. */
-	OSStatus FWAGetFWAudioPlugChannel(FWARef inRef, FWAAudioPlugRef streamRef,UInt32* channelID);
+	OSStatus FWAGetFWAudioPlugChannel(FWARef inRef, FWAAudioPlugRef streamRef,UInt32* channelID) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*! Description forthcoming. */
-	OSStatus FWASetFWAudioPlugChannel(FWARef inRef, FWAAudioPlugRef streamRef,UInt32 channelID);
+	OSStatus FWASetFWAudioPlugChannel(FWARef inRef, FWAAudioPlugRef streamRef,UInt32 channelID) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*! Description forthcoming. */
-	OSStatus FWAGetIndexedFWAudioPlug(FWARef inRef,FWADeviceRef device, UInt32 index,UInt32 dir, FWAAudioPlugRef* plugRef);
+	OSStatus FWAGetIndexedFWAudioPlug(FWARef inRef,FWADeviceRef device, UInt32 index,UInt32 dir, FWAAudioPlugRef* plugRef) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*! Description forthcoming. */
-	OSStatus FWAGetIndexedFWAudioMIDIPlug(FWARef inRef, FWAMIDIDeviceNubRef device,UInt32 index,UInt32 dir,FWAMIDIPlugRef* plugRef);
+	OSStatus FWAGetIndexedFWAudioMIDIPlug(FWARef inRef, FWAMIDIDeviceNubRef device,UInt32 index,UInt32 dir,FWAMIDIPlugRef* plugRef) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 	
 	/*! Description forthcoming. */
-	OSStatus FWAAttachFWAudioStream(FWARef inRef, FWAAudioStreamRef streamRef,FWAIsochStreamRef isochChannel);
+	OSStatus FWAAttachFWAudioStream(FWARef inRef, FWAAudioStreamRef streamRef,FWAIsochStreamRef isochChannel) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*! Description forthcoming. */
-	OSStatus FWAAttachFWAudioMIDIStream(FWARef inRef, FWAMIDIStreamRef streamRef,FWAIsochStreamRef isochChannel);
+	OSStatus FWAAttachFWAudioMIDIStream(FWARef inRef, FWAMIDIStreamRef streamRef,FWAIsochStreamRef isochChannel) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*! Description forthcoming. */
-	OSStatus FWASetFWAudioPlugProperty(FWARef inRef, FWAAudioPlugRef plugRef,const char *keyname,const  char* keyvalue);
+	OSStatus FWASetFWAudioPlugProperty(FWARef inRef, FWAAudioPlugRef plugRef,const char *keyname,const  char* keyvalue) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*! Description forthcoming. */
-	OSStatus FWASetFWAudioMIDIPlugProperty(FWARef inRef,FWAMIDIPlugRef plugRef,const char *keyname,const  char* keyvalue);
+	OSStatus FWASetFWAudioMIDIPlugProperty(FWARef inRef,FWAMIDIPlugRef plugRef,const char *keyname,const  char* keyvalue) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*! Description forthcoming. */
-	OSStatus FWAOpenLocalWithInterface(UInt64 guid,UInt32 options, FWARef* outRef);
+	OSStatus FWAOpenLocalWithInterface(UInt64 guid,UInt32 options, FWARef* outRef) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*! Description forthcoming. */
-	OSStatus FWAOpenWithService(io_service_t ,UInt32 options, FWARef* outRef);
+	OSStatus FWAOpenWithService(io_service_t ,UInt32 options, FWARef* outRef) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*! Description forthcoming. */
-	OSStatus FWAGetSessionRef(FWARef inRef,IOFireWireSessionRef * sessionRef);
+	OSStatus FWAGetSessionRef(FWARef inRef,IOFireWireSessionRef * sessionRef) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*! Description forthcoming. */
-	OSStatus FWAReserveIsochSequences(FWARef inRef,FWAIsochStreamRef isochStream,FWAudioType type,UInt32 count);
+	OSStatus FWAReserveIsochSequences(FWARef inRef,FWAIsochStreamRef isochStream,FWAudioType type,UInt32 count) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 	
 	/*! Description forthcoming. */
-	OSStatus FWACreateFWAudioMIDIDeviceNub(FWARef inRef,FWADeviceRef owningDevice, const char * deviceName, UInt32 vendorID,const char* guid,const char* iconFilePath, UInt32 modelID, const char * editorPath, FWAMIDIDeviceNubRef* device);
+	OSStatus FWACreateFWAudioMIDIDeviceNub(FWARef inRef,FWADeviceRef owningDevice, const char * deviceName, UInt32 vendorID,const char* guid,const char* iconFilePath, UInt32 modelID, const char * editorPath, FWAMIDIDeviceNubRef* device) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*! Description forthcoming. */
-	OSStatus FWADisposeFWAudioMIDIDeviceNub(FWARef inRef,FWAMIDIDeviceNubRef device);
+	OSStatus FWADisposeFWAudioMIDIDeviceNub(FWARef inRef,FWAMIDIDeviceNubRef device) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*! Description forthcoming. */
-	OSStatus FWAMIDIDeviceNubAttachMIDIPlug(FWARef inRef, FWAMIDIDeviceNubRef midiDeviceNub,FWAMIDIPlugRef midiPlug);
+	OSStatus FWAMIDIDeviceNubAttachMIDIPlug(FWARef inRef, FWAMIDIDeviceNubRef midiDeviceNub,FWAMIDIPlugRef midiPlug) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
 
 	/*! Description forthcoming. */
-	OSStatus FWAMIDIDeviceNubDetachMIDIPlug(FWARef inRef, FWAMIDIPlugRef midiPlug);	
-
+	OSStatus FWAMIDIDeviceNubDetachMIDIPlug(FWARef inRef, FWAMIDIPlugRef midiPlug) AVAILABLE_MAC_OS_X_VERSION_10_4_AND_LATER_BUT_DEPRECATED_IN_MAC_OS_X_VERSION_10_12 ;
+#pragma clang arc_cf_code_audited end
 #if __cplusplus
 }
 #endif

```