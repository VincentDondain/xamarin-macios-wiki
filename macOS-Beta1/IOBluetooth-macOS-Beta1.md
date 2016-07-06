#IOBluetooth.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/Bluetooth.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/Bluetooth.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/Bluetooth.h	2015-08-27 01:19:37.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/Bluetooth.h	2016-06-07 01:24:20.000000000 +0200
@@ -302,10 +302,10 @@
 	kBluetoothDeviceNameMaxLength	= 248
 };
 
-typedef uint8_t		BluetoothDeviceName[ 256 ];		// Max 248 bytes of UTF-8 encoded Unicode.
-typedef uint16_t	BluetoothClockOffset;			// Bits 14-0 come from bits 16-2 of CLKslav-CLKmaster.
-typedef uint8_t		BluetoothRole;					// 
-typedef uint8_t		BluetoothAllowRoleSwitch;		// 0x00-0x01 valid, 0x02-0xFF reserved.
+typedef uint8_t		BluetoothDeviceName[ kBluetoothDeviceNameMaxLength ];		// Max 248 bytes of UTF-8 encoded Unicode.
+typedef uint16_t	BluetoothClockOffset;										// Bits 14-0 come from bits 16-2 of CLKslav-CLKmaster.
+typedef uint8_t		BluetoothRole;												//
+typedef uint8_t		BluetoothAllowRoleSwitch;									// 0x00-0x01 valid, 0x02-0xFF reserved.
 enum
 {
 	kBluetoothDontAllowRoleSwitch 	= 0x00, 
@@ -454,6 +454,13 @@
 	uint16_t	maxPDUPayloadSize;
 };
 
+typedef enum BluetoothL2CAPSegmentationAndReassembly {
+    kBluetoothL2CAPSegmentationAndReassemblyUnsegmentedSDU    =   0x00,
+    kBluetoothL2CAPSegmentationAndReassemblyStartOfSDU        =   0x01,
+    kBluetoothL2CAPSegmentationAndReassemblyEndOfSDU          =   0x02,
+    kBluetoothL2CAPSegmentationAndReassemblyContinuationOfSDU =   0x03
+} BluetoothL2CAPSegmentationAndReassembly;
+        
 enum
 {
 	kBluetoothL2CAPInfoTypeMaxConnectionlessMTUSize = 0x0001
@@ -472,11 +479,14 @@
 
 typedef enum
 {
-    kBluetoothL2CAPConnectionResultSuccessful				= 0x0000,
-    kBluetoothL2CAPConnectionResultPending					= 0x0001,
-    kBluetoothL2CAPConnectionResultRefusedPSMNotSupported	= 0x0002,
-    kBluetoothL2CAPConnectionResultRefusedSecurityBlock		= 0x0003,
-    kBluetoothL2CAPConnectionResultRefusedNoResources		= 0x0004,
+    kBluetoothL2CAPConnectionResultSuccessful						= 0x0000,
+    kBluetoothL2CAPConnectionResultPending							= 0x0001,
+    kBluetoothL2CAPConnectionResultRefusedPSMNotSupported			= 0x0002,
+    kBluetoothL2CAPConnectionResultRefusedSecurityBlock				= 0x0003,
+    kBluetoothL2CAPConnectionResultRefusedNoResources				= 0x0004,
+    kBluetoothL2CAPConnectionResultRefusedReserved					= 0x0005,
+    kBluetoothL2CAPConnectionResultRefusedInvalidSourceCID			= 0x0006,
+    kBluetoothL2CAPConnectionResultRefusedSourceCIDAlreadyAllocated	= 0x0007
 } BluetoothL2CAPConnectionResult;
 
 typedef enum 
@@ -558,24 +568,52 @@
     kBluetoothL2CAPQoSTypeGuaranteed	= 0x02,
 } BluetoothL2CAPQoSType;
 
+typedef enum {
+    kBluetoothL2CAPSupervisoryFuctionTypeReceiverReady			= 0x0,
+    kBluetoothL2CAPSupervisoryFuctionTypeReject					= 0x1,
+    kBluetoothL2CAPSupervisoryFuctionTypeReceiverNotReady		= 0x2,
+    kBluetoothL2CAPSupervisoryFuctionTypeSelectiveReject		= 0x3
+} BluetoothL2CAPSupervisoryFuctionType;
+        
+enum {
+	kBluetoothLETXTimeMin			= 0x0148,   // 328 us / 41 octets / 27 (0x1B) byte PDU
+	kBluetoothLETXTimeDefault		= 0x0148,   // 328 us
+	kBluetoothLETXTimeMax			= 0x0848,   // 2120 us / 265 octets / 251 (0xFB) byte PDU
+	kBluetoothLETXOctetsMin			= 0x001b,   // 27 bytes pre-LE DPLE size
+	kBluetoothLETXOctetsDefault		= 0x001b,   // 27 bytes
+	kBluetoothLETXOctetsMax			= 0x00fb,   // 251 bytes 4.2 LE DPLE feature
+};
+
 enum
 {
-	kBluetoothL2CAPMTULowEnergyDefault			= 0x001b,	// 27 bytes
-	kBluetoothL2CAPMTUMinimum					= 0x0030,	// 48 bytes
-	kBluetoothL2CAPMTUDefault					= 0x03F9,	// 11.10.08 - dropped back to 1017 from 1021 (don't aggravate the 3DH5 problem between CSR<->BRCM just yet)
+//	kBluetoothL2CAPMTULowEnergyDefault			= 0x0080,								// 128 bytes - DPLE feature
+	kBluetoothL2CAPMTULowEnergyDefault			= kBluetoothLETXOctetsMin,				// 27 bytes
+	kBluetoothL2CAPMTULowEnergyMax              = kBluetoothLETXOctetsMax,				// 251 bytes
+	kBluetoothL2CAPMTUMinimum					= 0x0030,								// 48 bytes
+	kBluetoothL2CAPMTUDefault					= 0x03F9,								// 11.10.08 - dropped back to 1017 from 1021 (don't aggravate the 3DH5 problem between CSR<->BRCM just yet)
 	kBluetoothL2CAPMTUMaximum					= 0xffff,	
 	kBluetoothL2CAPMTUStart						= 0x7fff,
-	kBluetoothL2CAPMTUSIG						= 0x0030,	// 48 bytes
+	kBluetoothL2CAPMTUSIG						= 0x0030,								// 48 bytes
 	kBluetoothL2CAPFlushTimeoutDefault			= kBluetoothL2CAPFlushTimeoutForever,	// 0xffff
 	kBluetoothL2CAPQoSFlagsDefault				= 0,
-	kBluetoothL2CAPQoSTypeDefault				= kBluetoothL2CAPQoSTypeBestEffort,	// 0x01
+	kBluetoothL2CAPQoSTypeDefault				= kBluetoothL2CAPQoSTypeBestEffort,		// 0x01
 	kBluetoothL2CAPQoSTokenRateDefault			= 0x00000000,
 	kBluetoothL2CAPQoSTokenBucketSizeDefault	= 0x00000000,
 	kBluetoothL2CAPQoSPeakBandwidthDefault		= 0x00000000,
 	kBluetoothL2CAPQoSLatencyDefault			= 0xffffffff,
 	kBluetoothL2CAPQoSDelayVariationDefault		= 0xffffffff
 };
-		
+
+enum {
+    kBluetoothLEMaxTXTimeMin = 0x0148,
+    kBluetoothLEMaxTXTimeDefault = kBluetoothL2CAPMTULowEnergyDefault,
+    kBluetoothLEMaxTXTimeMax = 0x0848,
+    kBluetoothLEMaxTXOctetsMin              = 0x001b,	// 27 bytes
+    kBluetoothLEMaxTXOctetsDefault			= 0x0080,	// 128 bytes - DPLE feature
+    kBluetoothLEMaxTXOctetsMax              = 0x00fb,	// 251 bytes - DPLE feature
+};
+        
+
 #pragma mark === LE Security Manager ===
 
 #define kBluetoothLESMPTimeout 30		
@@ -779,7 +817,7 @@
 
 // Commands
 		
-typedef uint8_t		BluetoothHCICommandOpCodeGroup;
+typedef uint8_t         BluetoothHCICommandOpCodeGroup;
 typedef uint16_t		BluetoothHCICommandOpCodeCommand;
 typedef uint16_t		BluetoothHCICommandOpCode;
 typedef	uint32_t		BluetoothHCIVendorCommandSelector;
@@ -1129,7 +1167,22 @@
 	BluetoothHCIPageNumber	maxPage;
 	uint8_t					data[8];
 };
-		
+
+        
+enum BluetoothLEFeatureBits
+{
+    kBluetoothLEFeatureLEEncryption                         = (1 << 0L),
+    kBluetoothLEFeatureConnectionParamsRequestProcedure     = (1 << 1L),
+    kBluetoothLEFeatureExtendedRejectIndication             = (1 << 2L),
+    kBluetoothLEFeatureSlaveInitiatedFeaturesExchange       = (1 << 3L),
+    kBluetoothLEFeatureLEPing                               = (1 << 4L),
+    kBluetoothLEFeatureLEDataPacketLengthExtension          = (1 << 5L),
+    kBluetoothLEFeatureLLPrivacy                            = (1 << 6L),
+    kBluetoothLEFeatureExtendedScannerFilterPolicies        = (1 << 7L),
+    
+    // Three other bytes are RFU
+};
+
 enum BluetoothFeatureBits
 {
 	// Byte 0 of the support features data structure.
@@ -1314,6 +1367,64 @@
 	uint8_t		retransmissionEffort;
 	uint16_t		packetType;
 };
+// Add for EnhancedSetup
+typedef struct BluetoothHCIEnhancedSetupSynchronousConnectionParams	BluetoothHCIEnhancedSetupSynchronousConnectionParams;
+struct BluetoothHCIEnhancedSetupSynchronousConnectionParams
+{
+    uint32_t		transmitBandwidth;
+    uint32_t		receiveBandwidth;
+    uint64_t        transmitCodingFormat;
+    uint64_t        receiveCodingFormat;
+    uint8_t         transmitCodecFrameSize;
+    uint8_t         receiveCodecFrameSize;
+    uint16_t        inputBandwidth;
+    uint16_t        outputBandwidth;
+    uint64_t        inputCodingFormat;
+    uint64_t        outputCodingFormat;
+    uint16_t        inputCodedDataSize;
+    uint16_t        outputCodedDataSize;
+    uint8_t         inputPCMDataFormat;
+    uint8_t         outputPCMDataFormat;
+    uint8_t         inputPCMSamplePayloadMSBPosition;
+    uint8_t         outputPCMSamplePayloadMSBPosition;
+    uint8_t         inputDataPath;
+    uint8_t         outputDataPath;
+    uint8_t         inputTransportUnitSize;
+    uint8_t         outputTransportUnitSize;
+    uint16_t		maxLatency;
+    uint16_t		voiceSetting;
+    uint8_t		retransmissionEffort;
+    uint16_t		packetType;
+};
+// Add for EnhancedAccept
+typedef struct BluetoothHCIEnhancedAcceptSynchronousConnectionRequestParams	BluetoothHCIEnhancedAcceptSynchronousConnectionRequestParams;
+struct BluetoothHCIEnhancedAcceptSynchronousConnectionRequestParams
+{
+    uint32_t		transmitBandwidth;
+    uint32_t		receiveBandwidth;
+    uint64_t        transmitCodingFormat;
+    uint64_t        receiveCodingFormat;
+    uint8_t         transmitCodecFrameSize;
+    uint8_t         receiveCodecFrameSize;
+    uint16_t        inputBandwidth;
+    uint16_t        outputBandwidth;
+    uint64_t        inputCodingFormat;
+    uint64_t        outputCodingFormat;
+    uint16_t        inputCodedDataSize;
+    uint16_t        outputCodedDataSize;
+    uint8_t         inputPCMDataFormat;
+    uint8_t         outputPCMDataFormat;
+    uint8_t         inputPCMSamplePayloadMSBPosition;
+    uint8_t         outputPCMSamplePayloadMSBPosition;
+    uint8_t         inputDataPath;
+    uint8_t         outputDataPath;
+    uint8_t         inputTransportUnitSize;
+    uint8_t         outputTransportUnitSize;
+    uint16_t		maxLatency;
+    uint16_t		voiceSetting;
+    uint8_t		retransmissionEffort;
+    uint16_t		packetType;
+};
 
 typedef uint8_t	BluetoothHCILoopbackMode;
 enum
@@ -1903,6 +2014,24 @@
 typedef uint8_t		BluetoothHCISupportedIAC;
 typedef uint32_t	BluetoothHCITransmitBandwidth;
 typedef uint32_t	BluetoothHCIReceiveBandwidth;
+typedef uint64_t    BluetoothHCITransmitCodingFormat;
+typedef uint64_t    BluetoothHCIReceiveCodingFormat;
+typedef uint16_t    BluetoothHCITransmitCodecFrameSize;
+typedef uint16_t    BluetoothHCIReceiveCodecFrameSize;
+typedef uint32_t    BluetoothHCIInputBandwidth;
+typedef uint32_t    BluetoothHCIOutputBandwidth;
+typedef uint64_t    BluetoothHCIInputCodingFormat;
+typedef uint64_t    BluetoothHCIOutputCodingFormat;
+typedef uint16_t    BluetoothHCIInputCodedDataSize;
+typedef uint16_t    BluetoothHCIOutputCodedDataSize;
+typedef uint8_t     BluetoothHCIInputPCMDataFormat;
+typedef uint8_t     BluetoothHCIOutputPCMDataFormat;
+typedef uint8_t     BluetoothHCIInputPCMSamplePayloadMSBPosition;
+typedef uint8_t     BluetoothHCIOutputPCMSamplePayloadMSBPosition;
+typedef uint8_t     BluetoothHCIInputDataPath;
+typedef uint8_t     BluetoothHCIOutputDataPath;
+typedef uint8_t     BluetoothHCIInputTransportUnitSize;
+typedef uint8_t     BluetoothHCIOutputTransportUnitSize;
 typedef uint16_t	BluetoothHCIMaxLatency;
 typedef uint8_t		BluetoothHCIRetransmissionEffort;		
 enum BluetoothHCIRetransmissionEffortTypes
@@ -1936,6 +2065,35 @@
 	BluetoothPacketType					packetType;
 };
 
+typedef struct	BluetoothEnhancedSynchronousConnectionInfo		BluetoothEnhancedSynchronousConnectionInfo;
+struct	BluetoothEnhancedSynchronousConnectionInfo
+{
+    BluetoothHCITransmitBandwidth                   transmitBandWidth;
+    BluetoothHCIReceiveBandwidth                    receiveBandWidth;
+    BluetoothHCITransmitCodingFormat                transmitCodingFormat;
+    BluetoothHCIReceiveCodingFormat                 receiveCodingFormat;
+    BluetoothHCITransmitCodecFrameSize              transmitCodecFrameSize;
+    BluetoothHCIReceiveCodecFrameSize               receiveCodecFrameSize;
+    BluetoothHCIInputBandwidth                      inputBandwidth;
+    BluetoothHCIOutputBandwidth                     outputBandwidth;
+    BluetoothHCIInputCodingFormat                   inputCodingFormat;
+    BluetoothHCIOutputCodingFormat                  outputCodingFormat;
+    BluetoothHCIInputCodedDataSize                  inputCodedDataSize;
+    BluetoothHCIOutputCodedDataSize                 outputCodedDataSize;
+    BluetoothHCIInputPCMDataFormat                  inputPCMDataFormat;
+    BluetoothHCIOutputPCMDataFormat                 outputPCMDataFormat;
+    BluetoothHCIInputPCMSamplePayloadMSBPosition    inputPCMSampelPayloadMSBPosition;
+    BluetoothHCIOutputPCMSamplePayloadMSBPosition   outputPCMSampelPayloadMSBPosition;
+    BluetoothHCIInputDataPath                       inputDataPath;
+    BluetoothHCIOutputDataPath                      outputDataPath;
+    BluetoothHCIInputTransportUnitSize              inputTransportUnitSize;
+    BluetoothHCIOutputTransportUnitSize             outputTransportUnitSize;
+    BluetoothHCIMaxLatency                          maxLatency;
+    BluetoothHCIVoiceSetting                        voiceSetting;
+    BluetoothHCIRetransmissionEffort                retransmissionEffort;
+    BluetoothPacketType                             packetType;
+};
+        
 typedef struct	BluetoothHCIEventSynchronousConnectionCompleteResults 	BluetoothHCIEventSynchronousConnectionCompleteResults;
 struct			BluetoothHCIEventSynchronousConnectionCompleteResults
 {
@@ -2032,6 +2190,12 @@
 		kBluetoothHCISubEventLEConnectionUpdateComplete					= 0x03,
 		kBluetoothHCISubEventLEReadRemoteUsedFeaturesComplete			= 0x04,
 		kBluetoothHCISubEventLELongTermKeyRequest						= 0x05,
+    	kBluetoothHCISubEventLERemoteConnectionParameterRequest			= 0x06,
+    	kBluetoothHCISubEventLEDataLengthChange							= 0x07,
+    	kBluetoothHCISubEventLEReadLocalP256PublicKeyComplete			= 0x08,
+    	kBluetoothHCISubEventLEGenerateDHKeyComplete					= 0x09,
+    	kBluetoothHCISubEventLEEnhancedConnectionComplete				= 0x0A,
+    	kBluetoothHCISubEventLEDirectAdvertisingReport					= 0x0B,
 	
 	// [v3.0]
 	
@@ -2480,8 +2644,9 @@
 	kBluetoothHCIErrorConnectionTerminatedDueToMICFailure				= 0x3D,
 	kBluetoothHCIErrorConnectionFailedToBeEstablished                   = 0x3E,
 	kBluetoothHCIErrorMACConnectionFailed                               = 0x3F,
-	
-	kBluetoothHCIErrorMax												= 0x3F
+    kBluetoothHCIErrorCoarseClockAdjustmentRejected                     = 0x40,
+    
+    kBluetoothHCIErrorMax												= 0x40
 };
 
 #if 0
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/BluetoothAssignedNumbers.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/BluetoothAssignedNumbers.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/BluetoothAssignedNumbers.h	2016-02-27 07:04:10.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/BluetoothAssignedNumbers.h	2016-06-07 01:20:44.000000000 +0200
@@ -390,6 +390,8 @@
     
 	// Range 0x1001-0xFFFF dynamically assigned.
     kBluetoothL2CAPPSMDynamicStart				= 0x1001,
+	// AACP
+	kBluetoothL2CAPPSMAACP						= 0x1001,
 	kBluetoothL2CAPPSMD2D						= 0x100F,
     kBluetoothL2CAPPSMDynamicEnd				= 0xFFFF,
     
@@ -637,6 +639,17 @@
     kBluetoothHCIExtendedInquiryResponseDataTypePublicTargetAddress                         =   0x17,
     kBluetoothHCIExtendedInquiryResponseDataTypeRandomTargetAddress                         =   0x18,
     kBluetoothHCIExtendedInquiryResponseDataTypeAppearance                                  =   0x19,
+    kBluetoothHCIExtendedInquiryResponseDataTypeAdvertisingInterval							=	0x1A,
+    kBluetoothHCIExtendedInquiryResponseDataTypeLEBluetoothDeviceAddress					=	0x1B,
+    kBluetoothHCIExtendedInquiryResponseDataTypeLERole										=	0x1C,
+    kBluetoothHCIExtendedInquiryResponseDataTypeSimplePairingHash							=	0x1D,
+    kBluetoothHCIExtendedInquiryResponseDataTypeSimplePairingRandomizer						=	0x1E,
+    kBluetoothHCIExtendedInquiryResponseDataTypeServiceSolicitation32BitUUIDs				=	0x1F,
+    kBluetoothHCIExtendedInquiryResponseDataTypeServiceData32BitUUID						=	0x20,
+    kBluetoothHCIExtendedInquiryResponseDataTypeServiceData128BitUUID						=	0x21,
+    kBluetoothHCIExtendedInquiryResponseDataTypeSecureConnectionsConfirmationValue			=	0x22,
+    kBluetoothHCIExtendedInquiryResponseDataTypeSecureConnectionsRandomValue				=	0x23,
+    kBluetoothHCIExtendedInquiryResponseDataType3DInformationData							=	0x3D,
 	kBluetoothHCIExtendedInquiryResponseDataTypeManufacturerSpecificData					=	0xFF
 };
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/IOBluetooth.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/IOBluetooth.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/IOBluetooth.h	2015-08-27 01:19:37.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/IOBluetooth.h	2016-06-07 01:20:44.000000000 +0200
@@ -58,8 +58,6 @@
 		#import <IOBluetooth/objc/IOBluetoothHandsFreeAudioGateway.h>
 		#import <IOBluetooth/objc/IOBluetoothHandsFree.h>
 		#import <IOBluetooth/objc/IOBluetoothHandsFreeDevice.h>
-
-        #import <CoreBluetooth/CoreBluetooth.h>
 	#if defined(__cplusplus)
 	}
 	#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/objc/IOBluetoothHandsFree.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/objc/IOBluetoothHandsFree.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/objc/IOBluetoothHandsFree.h	2016-02-27 07:04:10.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/objc/IOBluetoothHandsFree.h	2016-06-07 01:20:44.000000000 +0200
@@ -14,7 +14,7 @@
 /*!
  @header
  @abstract	Hands free superclass. Superclass of IOBluetoothHandsFreeDevice or IOBluetoothHandsFreeAudioGateway.
- 			Contains the common code used to support the Bluetoooth hands free profile.
+ Contains the common code used to support the Bluetoooth hands free profile.
  @copyright	(c) 2010 by Apple Inc. All rights reserved.
  */
 
@@ -126,23 +126,23 @@
  @class IOBluetoothHandsFree
  @abstract Hands free profile class.
  @discussion Superclass of IOBluetoothHandsFreeDevice and IOBluetoothHandsFreeAudioGateway classes.
-			 Contains the common code used to support the bluetoooth hands free profile.
+ Contains the common code used to support the bluetoooth hands free profile.
  @coclass IOBluetoothHandsFreeDevice
  @coclass IOBluetoothHandsFreeAudioGateway
  */
 NS_CLASS_AVAILABLE(10_7, NA)
 @interface IOBluetoothHandsFree : NSObject {
-    IOBluetoothRFCOMMChannel *		_rfcommChannel;
+	IOBluetoothRFCOMMChannel *		_rfcommChannel;
 	IOBluetoothUserNotification *	_rfcommChannelNotification;
-    
+	
 	uint32_t						_supportedFeatures;
 	
 	void *							_reserved1;
-    
+	
 	float							_previousInputVolume;
 	float							_previousOutputVolume;
 	BOOL							_previousOutputMuted;
-    
+	
 	IOBluetoothDevice *				_device;
 	BluetoothRFCOMMChannelID		_deviceRFCOMMChannelID;
 	uint32_t						_deviceSupportedFeatures;
@@ -153,10 +153,10 @@
 	int								_handsFreeState;
 	IOBluetoothSMSMode				_SMSMode;
 	BOOL							_SMSEnabled;
-    
-    BOOL							_connectSCOAfterSLCConnected;
-
-    IOBluetoothHandsFreeExpansion *	_reserved;
+	
+	BOOL							_connectSCOAfterSLCConnected;
+	
+	IOBluetoothHandsFreeExpansion *	_reserved;
 }
 
 
@@ -324,7 +324,7 @@
  @method		connect
  @abstract		Connect to the device
  @discussion	Connects to the device and sets up a service level connection (RFCOMM channel).
- 				Delegate methods will be called once the connection is complete or a failure occurs.
+ Delegate methods will be called once the connection is complete or a failure occurs.
  */
 - (void)connect NS_AVAILABLE_MAC(10_7);
 
@@ -332,7 +332,7 @@
  @method		disconnect
  @abstract		Disconnect from the device
  @discussion	Disconnects from the device, closes the SCO and service level connection if they are connected.
- 				Delegate methods will be called once the disconnection is complete.
+ Delegate methods will be called once the disconnection is complete.
  */
 - (void)disconnect NS_AVAILABLE_MAC(10_7);
 
@@ -348,7 +348,7 @@
  @method		connectSCO
  @abstract		Open a SCO connection with the device
  @discussion	Opens a SCO connection with the device. The device must already have a service level connection or this will return immediately.
- 				Delegate methods will be called once the connection is complete of a failure occurs.
+ Delegate methods will be called once the connection is complete of a failure occurs.
  */
 - (void)connectSCO NS_AVAILABLE_MAC(10_7);
 
@@ -356,7 +356,7 @@
  @method		disconnectSCO
  @abstract		Disconnect the SCO connection with the device
  @discussion	Disconnects the SCO connection with the device (if one exists).
- 				Delegate methods will be called once the disconnection is complete.
+ Delegate methods will be called once the disconnection is complete.
  */
 - (void)disconnectSCO NS_AVAILABLE_MAC(10_7);
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/objc/IOBluetoothHandsFreeAudioGateway.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/objc/IOBluetoothHandsFreeAudioGateway.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/objc/IOBluetoothHandsFreeAudioGateway.h	2015-08-27 01:19:37.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/objc/IOBluetoothHandsFreeAudioGateway.h	2016-06-07 01:20:44.000000000 +0200
@@ -16,7 +16,7 @@
 @interface IOBluetoothHandsFreeAudioGateway : IOBluetoothHandsFree {
 	BOOL				_indicatorMode;
 	BOOL				_indicatorEventReporting;
-    
+	BOOL				_isSiriActive;
     IOBluetoothHandsFreeAudioGatewayExpansion *	_expansion;
 }
 

```