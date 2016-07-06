#IOKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/DV/DVFamily.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/DV/DVFamily.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/DV/DVFamily.h	2015-08-23 03:47:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/DV/DVFamily.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,348 +0,0 @@
-/*
- * Copyright (c) 2009 Apple Inc. All rights reserved.
- *
- * @APPLE_LICENSE_HEADER_START@
- * 
- * This file contains Original Code and/or Modifications of Original Code
- * as defined in and that are subject to the Apple Public Source License
- * Version 2.0 (the 'License'). You may not use this file except in
- * compliance with the License. Please obtain a copy of the License at
- * http://www.opensource.apple.com/apsl/ and read it before using this
- * file.
- * 
- * The Original Code and all software distributed under the License are
- * distributed on an 'AS IS' basis, WITHOUT WARRANTY OF ANY KIND, EITHER
- * EXPRESS OR IMPLIED, AND APPLE HEREBY DISCLAIMS ALL SUCH WARRANTIES,
- * INCLUDING WITHOUT LIMITATION, ANY WARRANTIES OF MERCHANTABILITY,
- * FITNESS FOR A PARTICULAR PURPOSE, QUIET ENJOYMENT OR NON-INFRINGEMENT.
- * Please see the License for the specific language governing rights and
- * limitations under the License.
- * 
- * @APPLE_LICENSE_HEADER_END@
- */
-/*
-	File:		DVFamily.h
-
-	Copyright:	� 2001 by Apple Computer, Inc., all rights reserved.
-
-*/
-//
-//	DVFamily.h
-//
-
-#ifndef __DVFAMILY__
-#define __DVFAMILY__
-
-#include <IOKit/avc/IOFireWireAVCConsts.h>
-#ifdef __cplusplus
-extern "C" {
-#endif
-
-///////////////////////////////////////////////////////////////////////
-//
-// constants
-//
-///////////////////////////////////////////////////////////////////////
-
-enum 
-{
-	kInvalidDVDeviceID		= 0,
-	kEveryDVDeviceID		= 0xFFFFFFFF,
-	kInvalidDVConnectionID		= 0,
-        kInvalidDVDeviceRefNum		= 0,
-	kEveryDVDeviceRefNum		= 0xFFFFFFFF
-};
-
-enum
-{
-	kDVDisconnectedErr			= -14101,
-	kDVBadIDErr				= -14102,
-	kUnknownStandardErr			= -14103,
-	kAlreadyEnabledErr			= -14104,
-	kNotEnabledErr				= -14105,
-	kDVDeviceBusyErr			= -14106,
-        kDVNoNotificationsErr			= -14107
-};
-
-enum
-{
-	kUnknownStandard	= 0,
-	kNTSCStandard		= 1,
-	kPALStandard 		= 2
-};
-
-// DV events
-enum
-{
-	kInvalidDVDeviceEvent		= 0,
-	
-	kDVDeviceAdded				= 1 << 0,
-	kDVDeviceRemoved			= 1 << 1,
-	KDVDeviceInfoChanged		= 1 << 2,
-	
-	kDVIsochReadEnabled			= 1 << 3,
-	kDVIsochReadComplete		= 1 << 4,
-	kDVIsochReadDisabled	 	= 1 << 5,
-
-	kDVIsochWriteEnabled		= 1 << 6,
-	kDVIsochWriteComplete		= 1 << 7,
-	kDVIsochWriteDisabled		= 1 << 8,
-
-	kDVAVCEnabled				= 1 << 9,
-	kDVAVCDisabled				= 1 << 10,
-	kDVAVCTransactionComplete	= 1 << 11,
-
-	// Tempory new event for input. Goes away DVFamily is dead.
-	kDVInputEvent = 1 << 12,
-
-	kDVEveryEvent				= 0x00001fff
-};
-
-enum
-{
-	kDVGlobalEventConnectionID	= 0xffffffff,
-	kEventSpecificDataSize		= 16
-};
-
-///////////////////////////////////////////////////////////////////////
-//
-// types
-//
-///////////////////////////////////////////////////////////////////////
-
-// holds our device identification...
-typedef UInt32 DVDeviceID;			
-
-// holds our device connection identification...
-typedef UInt32 DVDeviceRefNum;
-
-typedef UInt32 DVClientID;
-
-// AVC
-enum {
-    kAVCSupportInquiryCommand       	= 0x02,
-    kAVCReportInquiryCommand        	= 0x03,
-
-    // Opcodes and parameters
-    kAVCWindOpcode                          = 0xc4,
-    kAVCWindHighSpeedRewind                 = 0x45,
-    kAVCWindStop                            = 0x60,
-    kAVCWindRewind                          = 0x65,
-    kAVCWindFastForward                     = 0x75,
-
-    kAVCPlayOpcode                          = 0xc3,
-    kAVCPlayNextFrame                       = 0x30,
-    kAVCPlaySlowest                         = 0x31,
-    kAVCPlaySlow6                           = 0x32, 
-    kAVCPlaySlow5                           = 0x33,
-    kAVCPlaySlow4                           = 0x34,
-    kAVCPlaySlow3                           = 0x35,
-    kAVCPlaySlow2                           = 0x36,
-    kAVCPlaySlow1                           = 0x37,
-    kAVCPlay1x                              = 0x38,
-    kAVCPlayFast1                           = 0x39, 
-    kAVCPlayFast2                           = 0x3a,
-    kAVCPlayFast3                           = 0x3b,
-    kAVCPlayFast4                           = 0x3c,
-    kAVCPlayFast5                           = 0x3d,
-    kAVCPlayFast6                           = 0x3e,
-    kAVCPlayFastest                         = 0x3f,
-    kAVCPlayPreviousFrame                   = 0x40,
-    kAVCPlayRevSlowest                      = 0x41,
-    kAVCPlayRevSlow6                        = 0x42,
-    kAVCPlayRevSlow5                        = 0x43,
-    kAVCPlayRevSlow4                        = 0x44,
-    kAVCPlayRevSlow3                        = 0x45,
-    kAVCPlayRevSlow2                        = 0x46,
-    kAVCPlayRevSlow1                        = 0x47,
-    kAVCPlayRev1x                           = 0x48,
-    kAVCPlayRevFast1                        = 0x49,
-    kAVCPlayRevFast2                        = 0x4a,
-    kAVCPlayRevFast3                        = 0x4b,
-    kAVCPlayRevFast4                        = 0x4c,
-    kAVCPlayRevFast5                        = 0x4d,
-    kAVCPlayRevFast6                        = 0x4e,
-    kAVCPlayRevFastest                      = 0x4f,
-    kAVCPlayForward                         = 0x75,
-    kAVCPlayForwardPause                    = 0x7d,
-    kAVCPlayReverse                         = 0x65,
-    kAVCPlayReversePause                    = 0x6d,
-
-    kAVCMediumOpcode                        = 0xc1,
-    kAVCMediumEject                         = 0x60,
-    kAVCMediumTrayOpen                      = 0x31,
-    kAVCMediumTrayClose                     = 0x32,
-
-    kAVCRecordOpcode                        = 0xc2,
-    kAVCRecVideoInsert                      = 0x31,
-    kAVCRecAudioInsert                      = 0x32,
-    kAVCRecAVInsert                         = 0x33,
-    kAVCRecSubcodeInsert                    = 0x34,
-    kAVCRecord                              = 0x75,
-    kAVCRecPause                            = 0x7d,
-    kAVCRecVideoInsertPause                 = 0x41,
-    kAVCRecAudioInsertPause                 = 0x42,
-    kAVCRecAVInsertPause                    = 0x43,
-    kAVCRecSubcodeInsertPause               = 0x44,
-
-    kAVCRecSpeedOpcode                      = 0xdb,
-    kAVCRecSpeedLowSpeed                    = 0x00,
-    kAVCRecSpeed32                          = 0x20, 
-    kAVCRecSpeedStandard                    = 0x6f,
-    kAVCRecSpeedHighSpeed                   = 0xfe,
-    kAVCRecSpeedDummyOperand                = 0x7f,
-
-    kAVCEditPresetOpcode                    = 0x45,
-    kAVCEditPreRollAndStandby               = 0x00,
-    kAVCEditVideoInsert                     = 0x21,
-    kAVCEditAudioInsert                     = 0x22,
-    kAVCEditAVInsert                        = 0x23,
-    kAVCEditSubcodeInsert                   = 0x24,
-    kAVCEditSyncRecord                      = 0x25,
-    kAVCEditSyncPlay                        = 0x35,
-    kAVCEditOtherMode                       = 0x60,
-    kAVCEditInPoint                         = 0x00,
-    kAVCEditOutPoint                        = 0x01,
-    kAVCEditPreRollTime                     = 0x02,
-    kAVCEditDummyOperand                    = 0xff,
-
-    kAVCPositionDummyOperand                = 0xff,
-
-    kAVCPositionTimeCodeOpcode              = 0x51,
-    kAVCPositionValueInquiry                = 0x71,
-
-    kAVCMechaModeInquiryOpcode              = 0xd0,
-    kAVCMechaModeDummyOperand               = 0x7f
-
-};
-
-typedef struct AVCCTSFrameStruct {
-        UInt8           cmdType_respCode;     // cmd type/resp onse code
-        UInt8           headerAddress;
-        UInt8           opcode;
-        UInt8           operand[5];
-} AVCCTSFrameStruct, *AVCCTSFrameStructPtr;
-
-// for sending AVC commands
-typedef struct AVCTransactionParamsStruct {
-	Ptr						commandBufferPtr;
-	UInt32					commandLength;
-	Ptr						responseBufferPtr;
-	UInt32					responseBufferSize;
-	void *		responseHandler;	// Obsolete
-} AVCTransactionParams, *AVCTransactionParamsPtr;
-
-///////////////////////////////////////////////////////////////////////
-//
-// DV Event Notification
-//
-
-typedef struct OpaqueRef	*DVNotificationID;
-
-typedef struct DVEventHeaderStruct {
-	DVDeviceID			deviceID;			// who it's from
-	DVNotificationID	notifID;
-	UInt32				theEvent;			// what the event was
-} DVEventHeader, *DVEventHeaderPtr;
-
-typedef struct DVEventRecordStruct {		// generalized form
-	DVEventHeader		eventHeader;
-	UInt8				eventData[kEventSpecificDataSize];
-} DVEventRecord, *DVEventRecordPtr;
-
-typedef struct DVConnectionEventStruct {
-	DVEventHeader		eventHeader;
-} DVConnectionEvent, *DVConnectionEventPtr;
-
-typedef struct DVIsochCompleteEventStruct {
-	DVEventHeader		eventHeader;
-	Ptr					pFrameBuffer;
-	unsigned long		bufferSize;
-	UInt32				fwCycleTime;
-} DVIsochCompleteEvent, *DVIsochCompleteEventPtr;
-
-typedef struct DVAVTransactionCompleteEventStruct {
-	DVEventHeader			eventHeader;
-	Ptr						commandBufferPtr;
-	UInt32					commandLength;
-	Ptr						responseBufferPtr;
-	UInt32					responseBufferSize;
-} DVAVCTransactionCompleteEvent, *DVAVCTransactionCompleteEventPtr;
-
-// DV notification proc
-typedef OSStatus (*DVNotifyProc)(DVEventRecordPtr event, void *userData );
-								
-///////////////////////////////////////////////////////////////////////
-//
-// external prototypes
-//
-///////////////////////////////////////////////////////////////////////
-
-///////////////////////////////////////////////////////////////////////
-//
-// general device management
-//
-UInt32 DVCountDevices( void );
-OSErr DVGetIndDevice( DVDeviceID * pDVDevice, UInt32 index );
-
-OSErr DVSetDeviceName( DVDeviceID deviceID, char * str );
-OSErr DVGetDeviceName( DVDeviceID deviceID, char * str );
-
-OSErr DVOpenDriver( DVDeviceID deviceID, DVDeviceRefNum *pRefNum );
-OSErr DVCloseDriver( DVDeviceRefNum refNum );
-
-//OSErr DVGetDeviceInfo( DVDeviceID deviceID, DVDeviceInfoPtr pInfo );
-//OSErr DVGetDeviceClock( DVDeviceID deviceID, Component *clock );
-
-///////////////////////////////////////////////////////////////////////
-//
-// DV event notification
-//
-// kEveryDVDeviceRefNum can be used as a wild card refNum, for notifications about all
-// devices - especially handy when there aren't any yet!
-//
-OSErr DVNewNotification( DVDeviceRefNum refNum, DVNotifyProc notifyProc,
-						void *userData, DVNotificationID *pNotifyID );
-	
-OSErr DVNotifyMeWhen( DVDeviceRefNum refNum, DVNotificationID notifyID, UInt32 events);
-OSErr DVCancelNotification( DVDeviceRefNum refNum, DVNotificationID notifyID );
-OSErr DVDisposeNotification( DVDeviceRefNum refNum, DVNotificationID notifyID );
-
-///////////////////////////////////////////////////////////////////////
-//
-// DV Isoch Read
-//
-OSErr DVEnableRead( DVDeviceRefNum refNum );
-OSErr DVDisableRead( DVDeviceRefNum refNum );
-OSErr DVReadFrame( DVDeviceRefNum refNum, Ptr *ppReadBuffer, UInt32 * pSize );
-OSErr DVReleaseFrame( DVDeviceRefNum refNum, Ptr pReadBuffer );
-
-///////////////////////////////////////////////////////////////////////
-//
-// DV Isoch Write
-//
-OSErr DVEnableWrite( DVDeviceRefNum refNum );
-OSErr DVDisableWrite( DVDeviceRefNum refNum );
-OSErr DVGetEmptyFrame( DVDeviceRefNum refNum, Ptr *ppEmptyFrameBuffer, UInt32 * pSize );
-OSErr DVWriteFrame( DVDeviceRefNum refNum, Ptr pWriteBuffer );
-OSErr DVSetWriteSignalMode( DVDeviceRefNum refNum, UInt8 mode);
-
-///////////////////////////////////////////////////////////////////////
-//
-// AVC transactions
-//
-OSErr DVDoAVCTransaction( DVDeviceRefNum refNum, AVCTransactionParamsPtr pParams );
-
-OSErr DVIsEnabled( DVDeviceRefNum refNum, Boolean *isEnabled);
-OSErr DVGetDeviceStandard( DVDeviceRefNum refNum, UInt32 * pStandard );
-
-
-
-
-#ifdef __cplusplus
-}
-#endif
-
-#endif __DVFAMILY__
-
-
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/IOBSD.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/IOBSD.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/IOBSD.h	2015-08-27 01:55:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/IOBSD.h	2016-06-03 22:55:03.000000000 +0200
@@ -32,6 +32,7 @@
  * bsd-related registry properties
  */
 
+#define kIOBSDKey      "IOBSD"     // (BSD subsystem resource)
 #define kIOBSDNameKey  "BSD Name"  // (an OSString)
 #define kIOBSDNamesKey "BSD Names" // (an OSDictionary of OSString's, for links)
 #define kIOBSDMajorKey "BSD Major" // (an OSNumber)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/IOKitKeys.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/IOKitKeys.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/IOKitKeys.h	2015-08-27 01:55:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/IOKitKeys.h	2016-06-03 22:55:03.000000000 +0200
@@ -55,6 +55,8 @@
 
 // registry ID number
 #define kIORegistryEntryIDKey		"IORegistryEntryID"
+// property name to get array of property names
+#define kIORegistryEntryPropertyKeysKey "IORegistryEntryPropertyKeys"
 
 // IOService class name
 #define kIOServiceClass			"IOService"
@@ -71,10 +73,12 @@
 #define kIOProviderClassKey		"IOProviderClass"
 #define kIONameMatchKey			"IONameMatch"
 #define kIOPropertyMatchKey		"IOPropertyMatch"
+#define kIOPropertyExistsMatchKey	"IOPropertyExistsMatch"
 #define kIOPathMatchKey			"IOPathMatch"
 #define kIOLocationMatchKey		"IOLocationMatch"
 #define kIOParentMatchKey		"IOParentMatch"
 #define kIOResourceMatchKey		"IOResourceMatch"
+#define kIOResourceMatchedKey		"IOResourceMatched"
 #define kIOMatchedServiceCountKey	"IOMatchedServiceCountMatch"
 
 #define kIONameMatchedKey		"IONameMatched"
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/IOReturn.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/IOReturn.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/IOReturn.h	2015-08-27 01:55:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/IOReturn.h	2016-06-03 22:55:04.000000000 +0200
@@ -72,6 +72,8 @@
 #define sub_iokit_sdio                    err_sub(0x174)
 #define sub_iokit_wlan                    err_sub(0x208)
 
+#define sub_iokit_appleembeddedsleepwakehandler  err_sub(0x209)
+
 #define sub_iokit_vendor_specific         err_sub(-2)
 #define sub_iokit_reserved                err_sub(-1)
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/audio/IOAudioTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/audio/IOAudioTypes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/audio/IOAudioTypes.h	2015-08-27 02:10:50.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/audio/IOAudioTypes.h	2016-06-03 23:11:37.000000000 +0200
@@ -105,7 +105,7 @@
 typedef struct _IOAudioEngineStatus {
     UInt32					fVersion;
     volatile UInt32			fCurrentLoopCount;
-    volatile AbsoluteTime                    fLastLoopTime;
+    volatile AbsoluteTime   fLastLoopTime;
     volatile UInt32			fEraseHeadSampleFrame;
 } IOAudioEngineStatus;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/graphics/IOGraphicsInterface.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/graphics/IOGraphicsInterface.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/graphics/IOGraphicsInterface.h	2015-08-27 02:09:19.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/graphics/IOGraphicsInterface.h	2016-06-03 23:08:18.000000000 +0200
@@ -35,6 +35,11 @@
 
 #include <IOKit/graphics/IOGraphicsInterfaceTypes.h>
 
+// <rdar://problem/23764215> IOGraphics: IOGraphicsInterface.h: "C" linkage not enforced.
+#ifdef __cplusplus
+extern "C" {
+#endif
+
 #define kIOGraphicsAcceleratorTypeID                    \
         (CFUUIDGetConstantUUIDWithBytes(NULL,           \
                                 0xAC, 0xCF, 0x00, 0x00, \
@@ -148,6 +153,11 @@
 IOReturn IOAccelFindAccelerator( io_service_t framebuffer,
                                  io_service_t * pAccelerator, UInt32 * pFramebufferIndex );
 
+
+#ifdef __cplusplus
+    }
+#endif
+
 /* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * */
 
 #endif /* !_IOKIT_IOGRAPHICSINTERFACE_H */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/graphics/IOGraphicsTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/graphics/IOGraphicsTypes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/graphics/IOGraphicsTypes.h	2015-08-27 02:09:19.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/graphics/IOGraphicsTypes.h	2016-06-03 23:08:18.000000000 +0200
@@ -31,7 +31,7 @@
 extern "C" {
 #endif
 
-#define IOGRAPHICSTYPES_REV     42
+#define IOGRAPHICSTYPES_REV     43
 
 typedef SInt32  IOIndex;
 typedef UInt32  IOSelect;
@@ -270,6 +270,18 @@
 	kIOFBDisplayPortTrainingAttribute   = 'dpta',
 };
 
+// values for kIOWindowServerActiveAttribute
+enum {
+    kIOWSAA_Unaccelerated       = 0,    // CPU rendering/access only, no GPU access
+    kIOWSAA_Accelerated         = 1,    // GPU rendering/access only, no CPU mappings
+    kIOWSAA_From_Accelerated    = 2,    // Transitioning from GPU to CPU
+    kIOWSAA_To_Accelerated      = 3,    // Transitioning from CPU to GPU
+    kIOWSAA_Sleep               = 4,
+    kIOWSAA_Hibernate           = kIOWSAA_Sleep,
+    kIOWSAA_DriverOpen          = 5,    // Reserved
+    kIOWSAA_Transactional       = 0x10  // If this bit is present, transition is to/from transactional operation model.
+};
+
 // values for kIOMirrorAttribute
 enum {
     kIOMirrorIsPrimary                  = 0x80000000,
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDBase.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDBase.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDBase.h	2015-08-23 00:59:23.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDBase.h	2016-05-21 06:36:20.000000000 +0200
@@ -28,20 +28,23 @@
 
 __BEGIN_DECLS
 
+CF_ASSUME_NONNULL_BEGIN
+CF_IMPLICIT_BRIDGING_ENABLED
+
 /*! @typedef IOHIDDeviceRef
 	This is the type of a reference to the IOHIDDevice.
 */
-typedef struct __IOHIDDevice * IOHIDDeviceRef;
+typedef struct CF_BRIDGED_TYPE(id) __IOHIDDevice * IOHIDDeviceRef;
 
 /*! @typedef IOHIDElementRef
 	This is the type of a reference to the IOHIDElement.
 */
-typedef struct __IOHIDElement * IOHIDElementRef;
+typedef struct CF_BRIDGED_TYPE(id) __IOHIDElement * IOHIDElementRef;
 
 /*! @typedef IOHIDValueRef
 	This is the type of a reference to the IOHIDValue.
 */
-typedef struct __IOHIDValue * IOHIDValueRef;
+typedef struct CF_BRIDGED_TYPE(id) __IOHIDValue * IOHIDValueRef;
 
 /*!
     @typedef    IOHIDTransactionDirectionType
@@ -49,11 +52,10 @@
     @constant   kIOHIDTransactionDirectionTypeInput Transaction direction used for requesting element values from a device. 
     @constant   kIOHIDTransactionDirectionTypeOutput Transaction direction used for dispatching element values to a device. 
 */
-enum {
+typedef CF_ENUM(uint32_t, IOHIDTransactionDirectionType) {
     kIOHIDTransactionDirectionTypeInput,
     kIOHIDTransactionDirectionTypeOutput
 };
-typedef uint32_t IOHIDTransactionDirectionType;
 
 /*!
     @enum       IOHIDTransactionOption
@@ -61,9 +63,7 @@
     @constant   kIOHIDTransactionOptionDefaultOutputValue Option to set the default element value to be used with an
                 IOHIDDeviceTransactionInterface of direction kIOHIDTransactionDirectionTypeOutput. 
 */
-enum {
-    kIOHIDTransactionOptionDefaultOutputValue = 0x0001
-};
+static const IOOptionBits kIOHIDTransactionOptionDefaultOutputValue = 0x0001;
 
 
 /*! @typedef IOHIDCallback
@@ -74,9 +74,9 @@
     @param sender Interface instance sending the completion routine.
 */
 typedef void (*IOHIDCallback)(
-                                    void *                  context, 
+                                    void * _Nullable        context,
                                     IOReturn                result, 
-                                    void *                  sender);
+                                    void * _Nullable        sender);
 
 /*! @typedef IOHIDReportCallback
     @discussion Type and arguments of callout C function that is used when a HID report completion routine is called.
@@ -89,9 +89,9 @@
     @param reportLength Size of the buffer received upon completion.
 */
 typedef void (*IOHIDReportCallback) (
-                                    void *                  context, 
+                                    void * _Nullable        context,
                                     IOReturn                result, 
-                                    void *                  sender, 
+                                    void * _Nullable        sender,
                                     IOHIDReportType         type, 
                                     uint32_t                reportID,
                                     uint8_t *               report, 
@@ -109,9 +109,9 @@
     @param timeStamp The time at which the report arrived.
 */
 typedef void (*IOHIDReportWithTimeStampCallback) (
-                                    void *                  context, 
+                                    void * _Nullable        context,
                                     IOReturn                result, 
-                                    void *                  sender, 
+                                    void * _Nullable        sender,
                                     IOHIDReportType         type, 
                                     uint32_t                reportID,
                                     uint8_t *               report, 
@@ -126,9 +126,9 @@
     @param value IOHIDValueRef containing the returned element value.
 */
 typedef void (*IOHIDValueCallback) ( 
-                                    void *                  context,
+                                    void * _Nullable        context,
                                     IOReturn                result, 
-                                    void *                  sender,
+                                    void * _Nullable        sender,
                                     IOHIDValueRef           value);
 
 /*! @typedef IOHIDValueMultipleCallback
@@ -139,9 +139,9 @@
     @param multiple CFDictionaryRef containing the returned element key value pairs.
 */
 typedef void (*IOHIDValueMultipleCallback) ( 
-                                    void *                  context,
+                                    void * _Nullable        context,
                                     IOReturn                result, 
-                                    void *                  sender,
+                                    void * _Nullable        sender,
                                     CFDictionaryRef         multiple);
 
 /*! @typedef IOHIDDeviceCallback
@@ -151,10 +151,14 @@
     @param device IOHIDDeviceRef containing the sending device.
 */
 typedef void (*IOHIDDeviceCallback) ( 
-                                    void *                  context,
+                                    void * _Nullable        context,
                                     IOReturn                result, 
-                                    void *                  sender,
+                                    void * _Nullable        sender,
                                     IOHIDDeviceRef          device);
 
+CF_IMPLICIT_BRIDGING_DISABLED
+CF_ASSUME_NONNULL_END
+
 __END_DECLS
+
 #endif /* _IOKIT_HID_IOHIDBASE_H_ */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDDevice.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDDevice.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDDevice.h	2015-08-23 00:59:23.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDDevice.h	2016-05-21 06:36:20.000000000 +0200
@@ -53,6 +53,9 @@
 
 __BEGIN_DECLS
 
+CF_ASSUME_NONNULL_BEGIN
+CF_IMPLICIT_BRIDGING_ENABLED
+
 /*!
 	@function   IOHIDDeviceGetTypeID
 	@abstract   Returns the type identifier of all IOHIDDevice instances.
@@ -71,8 +74,8 @@
     @result     Returns a new IOHIDDeviceRef.
 */
 CF_EXPORT
-IOHIDDeviceRef IOHIDDeviceCreate(
-                                CFAllocatorRef                  allocator, 
+IOHIDDeviceRef _Nullable IOHIDDeviceCreate(
+                                CFAllocatorRef _Nullable        allocator,
                                 io_service_t                    service)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
@@ -197,9 +200,9 @@
     @result     Returns CFArrayRef containing multiple IOHIDElement object.
 */
 CF_EXPORT 
-CFArrayRef IOHIDDeviceCopyMatchingElements(
+CFArrayRef _Nullable IOHIDDeviceCopyMatchingElements(
                                 IOHIDDeviceRef                  device, 
-                                CFDictionaryRef                 matching, 
+                                CFDictionaryRef _Nullable       matching,
                                 IOOptionBits                    options)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
@@ -247,8 +250,8 @@
 CF_EXPORT
 void IOHIDDeviceRegisterRemovalCallback( 
                                 IOHIDDeviceRef                  device, 
-                                IOHIDCallback                   callback, 
-                                void *                          context)
+                                IOHIDCallback _Nullable         callback,
+                                void * _Nullable                context)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*! @function   IOHIDDeviceRegisterInputValueCallback
@@ -265,9 +268,9 @@
 */
 CF_EXPORT
 void IOHIDDeviceRegisterInputValueCallback(
-                                IOHIDDeviceRef                  device, 
-                                IOHIDValueCallback              callback, 
-                                void *                          context)
+                                IOHIDDeviceRef                  device,
+                                IOHIDValueCallback _Nullable    callback,
+                                void * _Nullable                context)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*! @function   IOHIDDeviceRegisterInputReportCallback
@@ -288,8 +291,8 @@
                                 IOHIDDeviceRef                  device, 
                                 uint8_t *                       report, 
                                 CFIndex                         reportLength,
-                                IOHIDReportCallback             callback, 
-                                void *                          context)
+                                IOHIDReportCallback _Nullable   callback,
+                                void * _Nullable                context)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*! @function   IOHIDDeviceRegisterInputReportWithTimeStampCallback
@@ -310,8 +313,8 @@
                                 IOHIDDeviceRef                      device, 
                                 uint8_t *                           report, 
                                 CFIndex                             reportLength,
-                                IOHIDReportWithTimeStampCallback    callback, 
-                                void *                              context)
+                                IOHIDReportWithTimeStampCallback _Nullable  callback,
+                                void * _Nullable                    context)
 AVAILABLE_MAC_OS_X_VERSION_10_10_AND_LATER;
 
 /*! @function   IOHIDDeviceSetInputValueMatching
@@ -330,7 +333,7 @@
 CF_EXPORT
 void IOHIDDeviceSetInputValueMatching(
                                 IOHIDDeviceRef                  device, 
-                                CFDictionaryRef                 matching)
+                                CFDictionaryRef _Nullable       matching)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
                                 
 /*! @function   IOHIDDeviceSetInputValueMatchingMultiple
@@ -346,7 +349,7 @@
 CF_EXPORT
 void IOHIDDeviceSetInputValueMatchingMultiple(
                                 IOHIDDeviceRef                  device, 
-                                CFArrayRef                      multiple)
+                                CFArrayRef _Nullable            multiple)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
                                 
 /*! @function   IOHIDDeviceSetValue
@@ -408,8 +411,8 @@
                                 IOHIDElementRef                 element, 
                                 IOHIDValueRef                   value, 
                                 CFTimeInterval                  timeout,
-                                IOHIDValueCallback              callback, 
-                                void *                          context)
+                                IOHIDValueCallback _Nullable    callback,
+                                void * _Nullable                context)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*! @function   IOHIDDeviceSetValueMultipleWithCallback
@@ -432,8 +435,8 @@
                                 IOHIDDeviceRef                  device, 
                                 CFDictionaryRef                 multiple,
                                 CFTimeInterval                  timeout,
-                                IOHIDValueMultipleCallback      callback, 
-                                void *                          context)
+                                IOHIDValueMultipleCallback _Nullable    callback,
+                                void * _Nullable                context)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*! @function   IOHIDDeviceGetValue
@@ -452,7 +455,7 @@
 IOReturn IOHIDDeviceGetValue(
                                 IOHIDDeviceRef                  device, 
                                 IOHIDElementRef                 element, 
-                                IOHIDValueRef *                 pValue)
+                                IOHIDValueRef _Nonnull * _Nonnull   pValue)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*! @function   IOHIDDeviceCopyValueMultiple
@@ -472,7 +475,7 @@
 IOReturn IOHIDDeviceCopyValueMultiple(
                                 IOHIDDeviceRef                  device, 
                                 CFArrayRef                      elements, 
-                                CFDictionaryRef *               pMultiple)
+                                CFDictionaryRef _Nullable * _Nullable   pMultiple)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*! @function   IOHIDDeviceGetValueWithCallback
@@ -495,10 +498,10 @@
 IOReturn IOHIDDeviceGetValueWithCallback(
                                 IOHIDDeviceRef                  device, 
                                 IOHIDElementRef                 element, 
-                                IOHIDValueRef *                 pValue,
+                                IOHIDValueRef _Nonnull * _Nonnull    pValue,
                                 CFTimeInterval                  timeout,
-                                IOHIDValueCallback              callback, 
-                                void *                          context)
+                                IOHIDValueCallback _Nullable    callback,
+                                void * _Nullable                context)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 
@@ -519,13 +522,14 @@
     @result     Returns kIOReturnSuccess if successful.
 */
 CF_EXPORT
+
 IOReturn IOHIDDeviceCopyValueMultipleWithCallback(
                                 IOHIDDeviceRef                  device, 
                                 CFArrayRef                      elements, 
-                                CFDictionaryRef *               pMultiple,
+                                CFDictionaryRef _Nullable * _Nullable   pMultiple,
                                 CFTimeInterval                  timeout,
-                                IOHIDValueMultipleCallback      callback, 
-                                void *                          context)
+                                IOHIDValueMultipleCallback _Nullable    callback,
+                                void * _Nullable                context)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
                                 
 /*! @function   IOHIDDeviceSetReport
@@ -577,8 +581,8 @@
                                 const uint8_t *                 report,
                                 CFIndex                         reportLength,
                                 CFTimeInterval                  timeout,
-                                IOHIDReportCallback             callback,
-                                void *                          context)
+                                IOHIDReportCallback _Nullable   callback,
+                                void * _Nullable                context)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*! @function   IOHIDDeviceGetReport
@@ -641,7 +645,10 @@
                                 IOHIDReportCallback             callback,
                                 void *                          context)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
-                                
+
+CF_IMPLICIT_BRIDGING_DISABLED
+CF_ASSUME_NONNULL_END
+
 __END_DECLS
 
 #endif /* _IOKIT_HID_IOHIDDEVICE_USER_H */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDElement.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDElement.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDElement.h	2015-08-23 00:59:23.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDElement.h	2016-05-21 06:36:20.000000000 +0200
@@ -48,6 +48,10 @@
 
 __BEGIN_DECLS
 
+CF_ASSUME_NONNULL_BEGIN
+CF_IMPLICIT_BRIDGING_ENABLED
+
+
 /*!
 	@function   IOHIDElementGetTypeID
 	@abstract   Returns the type identifier of all IOHIDElement instances.
@@ -65,7 +69,7 @@
     @result     Returns a new IOHIDElementRef.
 */
 CF_EXPORT
-IOHIDElementRef IOHIDElementCreateWithDictionary(CFAllocatorRef allocator, CFDictionaryRef dictionary)
+IOHIDElementRef IOHIDElementCreateWithDictionary(CFAllocatorRef _Nullable allocator, CFDictionaryRef dictionary)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*!
@@ -86,7 +90,7 @@
     @result     Returns an IOHIDElementRef referencing the parent element.
 */
 CF_EXPORT
-IOHIDElementRef IOHIDElementGetParent(IOHIDElementRef element)
+IOHIDElementRef _Nullable IOHIDElementGetParent(IOHIDElementRef element)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*!
@@ -97,7 +101,7 @@
     @result     Returns an CFArrayRef containing element objects of type IOHIDElementRef.
 */
 CF_EXPORT
-CFArrayRef IOHIDElementGetChildren(IOHIDElementRef element)
+CFArrayRef _Nullable IOHIDElementGetChildren(IOHIDElementRef element)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*!
@@ -130,7 +134,7 @@
     @result     Returns a copy of the current attached elements.
 */
 CF_EXPORT
-CFArrayRef IOHIDElementCopyAttached(IOHIDElementRef element)
+CFArrayRef _Nullable IOHIDElementCopyAttached(IOHIDElementRef element)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*!
@@ -388,7 +392,7 @@
     @result     Returns the property.
 */
 CF_EXPORT
-CFTypeRef IOHIDElementGetProperty(IOHIDElementRef element, CFStringRef key)
+CFTypeRef _Nullable IOHIDElementGetProperty(IOHIDElementRef element, CFStringRef key)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*!
@@ -403,6 +407,8 @@
 Boolean IOHIDElementSetProperty(IOHIDElementRef element, CFStringRef key, CFTypeRef property)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
+CF_IMPLICIT_BRIDGING_DISABLED
+CF_ASSUME_NONNULL_END
 
 __END_DECLS
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDKeys.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDKeys.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDKeys.h	2016-02-27 07:31:03.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDKeys.h	2016-06-03 23:10:18.000000000 +0200
@@ -115,7 +115,7 @@
 #define kIOHIDTransportI2CValue                 "I2C"
 #define kIOHIDTransportSPIValue                 "SPI"
 #define kIOHIDTransportSerialValue              "Serial"
-#define kIOHIDTransportIAPValue                 "IAP"
+#define kIOHIDTransportIAPValue                 "iAP"
 #define kIOHIDTransportAirPlayValue             "AirPlay"
 #define kIOHIDTransportSPUValue                 "SPU"
 
@@ -407,7 +407,58 @@
  */
 #define kIOHIDSystemButtonPressedDuringDarkBoot     iokit_family_msg(sub_iokit_hidsystem, 7)
 
+/*!
+ @defined IOHIDKeyboard Keys
+ @abstract Keys that represent parameters of keyboards.
+ @discussion Legacy IOHIDKeyboard keys, formerly in IOHIDPrivateKeys. See IOHIDServiceKeys.h for the new keys.
+ */
+#define kIOHIDKeyboardCapsLockDelay         "CapsLockDelay"
+#define kIOHIDKeyboardCapsLockDelayOverride "CapsLockDelayOverride"
+#define kIOHIDKeyboardEjectDelay            "EjectDelay"
+
+/*!
+ @defined Press count tracking keys
+ @abstract Keys used to set the parameters for press count tracking
+ @discussion CFBoolean value for kIOHIDKeyboardPressCountTrackingEnabledKey is used to turn on the feature or turn it off
+    kIOHIDKeyboardPressCountTriplePressTimeoutKey and kIOHIDKeybaordPressCountDoublePressTimeoutKey take CFNumberRef values
+    The numbers represent the timeout values for determining the value kIOHIDEventFieldKeyboardPressCount
+    kIOHIDKeyboardLongPressTimeoutKey value is used to determine the timeout for long presses
+ */
+#define kIOHIDKeyboardPressCountTrackingEnabledKey      "PressCountTrackingEnabled"
+#define kIOHIDKeyboardPressCountTriplePressTimeoutKey   "PressCountTriplePressTimeout"
+#define kIOHIDKeyboardPressCountDoublePressTimeoutKey   "PressCountDoublePressTimeout"
+#define kIOHIDKeyboardLongPressTimeoutKey               "LongPressTimeout"
+
+/*!
+ @defined Tap count tracking keys
+ @abstract Keys used to set the parameters for tap count tracking
+ @discussion CFBoolean value for kIOHIDBiometricTapTrackingEnabledKey is used to turn on the feature or turn it off
+ kIOHIDBiometricDoubleTapTimeoutKey and kIOHIDBiometricTripleTapTimeoutKey take CFNumberRef values
+ The numbers represent the timeout values for determining the value kIOHIDEventFieldBiometricTapCount
+ */
+#define kIOHIDBiometricTapTrackingEnabledKey            "TapTrackingEnabled"
+#define kIOHIDBiometricDoubleTapTimeoutKey              "DoubleTapTimeout"
+#define kIOHIDBiometricTripleTapTimeoutKey              "TripleTapTimeout"
+
+/*!
+    @defined kFnFunctionUsageMapKey
+    @abstract top row key remapping for consumer usages
+    @discussion string of comma separated uint64_t value representing (usagePage<<32) | usage pairs
+ 
+ */
+#define kFnFunctionUsageMapKey      "FnFunctionUsageMap"
+
+/*!
+    @defined kFnKeyboardUsageMapKey
+    @abstract top row key reampping for consumer usages
+    @discussion string of comma separated uint64_t value representing (usagePage<<32) | usage pairs
+ 
+ */
+#define kFnKeyboardUsageMapKey      "FnKeyboardUsageMap"
+
+#define kNumLockKeyboardUsageMapKey "NumLockKeyboardUsageMap"
 
+#define kKeyboardUsageMapKey        "KeyboardUsageMap"
 
 __END_DECLS
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDManager.h	2015-08-23 00:59:23.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDManager.h	2016-05-21 06:36:20.000000000 +0200
@@ -53,6 +53,9 @@
 
 __BEGIN_DECLS
 
+CF_ASSUME_NONNULL_BEGIN
+CF_IMPLICIT_BRIDGING_ENABLED
+
 /*!
  @enum IOHIDManagerOptions
  @abstract Various options that can be supplied to IOHIDManager functions.
@@ -64,17 +67,17 @@
  @const kIOHIDManagerOptionDoNotSaveProperties This constant can be supplied to @link IOHIDManagerCreate @/link when you want to 
  use the persistent property store but do not want to add to it.
  */
-typedef enum {
+typedef CF_OPTIONS(uint32_t, IOHIDManagerOptions) {
     kIOHIDManagerOptionNone = 0x0,
     kIOHIDManagerOptionUsePersistentProperties = 0x1,
     kIOHIDManagerOptionDoNotLoadProperties = 0x2,
     kIOHIDManagerOptionDoNotSaveProperties = 0x4,
-} IOHIDManagerOptions;
+};
 
 /*! @typedef IOHIDManagerRef
 	@abstract This is the type of a reference to the IOHIDManager.
 */
-typedef struct __IOHIDManager * IOHIDManagerRef;
+typedef struct CF_BRIDGED_TYPE(id) __IOHIDManager * IOHIDManagerRef;
 
 /*!
 	@function   IOHIDManagerGetTypeID
@@ -97,7 +100,7 @@
 */
 CF_EXPORT 
 IOHIDManagerRef IOHIDManagerCreate(     
-                                CFAllocatorRef                  allocator,
+                                CFAllocatorRef _Nullable        allocator,
                                 IOOptionBits                    options)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
                                 
@@ -142,7 +145,7 @@
     @result     Returns CFTypeRef containing the property.
 */
 CF_EXPORT
-CFTypeRef IOHIDManagerGetProperty(
+CFTypeRef _Nullable IOHIDManagerGetProperty(
                                 IOHIDManagerRef                 manager,
                                 CFStringRef                     key)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
@@ -218,7 +221,7 @@
 CF_EXPORT
 void IOHIDManagerSetDeviceMatching(
                                 IOHIDManagerRef                 manager,
-                                CFDictionaryRef                 matching)
+                                CFDictionaryRef _Nullable       matching)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
                                 
 /*! @function   IOHIDManagerSetDeviceMatchingMultiple
@@ -233,7 +236,7 @@
 CF_EXPORT
 void IOHIDManagerSetDeviceMatchingMultiple(
                                 IOHIDManagerRef                 manager,
-                                CFArrayRef                      multiple)
+                                CFArrayRef _Nullable            multiple)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
                                 
 /*! @function   IOHIDManagerCopyDevices
@@ -242,7 +245,7 @@
     @result     CFSetRef containing IOHIDDeviceRefs.
 */
 CF_EXPORT
-CFSetRef IOHIDManagerCopyDevices(
+CFSetRef _Nullable IOHIDManagerCopyDevices(
                                 IOHIDManagerRef                 manager)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
@@ -258,7 +261,7 @@
 void IOHIDManagerRegisterDeviceMatchingCallback(
                                 IOHIDManagerRef                 manager,
                                 IOHIDDeviceCallback             callback,
-                                void *                          context)
+                                void * _Nullable                context)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*! @function   IOHIDManagerRegisterDeviceRemovalCallback
@@ -274,7 +277,7 @@
 void IOHIDManagerRegisterDeviceRemovalCallback(
                                 IOHIDManagerRef                 manager,
                                 IOHIDDeviceCallback             callback,
-                                void *                          context)
+                                void * _Nullable                context)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*! @function   IOHIDManagerRegisterInputReportCallback
@@ -289,7 +292,7 @@
 void IOHIDManagerRegisterInputReportCallback( 
                                     IOHIDManagerRef             manager,
                                     IOHIDReportCallback         callback,
-                                    void *                      context)
+                                    void * _Nullable            context)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
                                                                     
 /*! @function   IOHIDManagerRegisterInputValueCallback
@@ -306,7 +309,7 @@
 void IOHIDManagerRegisterInputValueCallback( 
                                 IOHIDManagerRef                 manager,
                                 IOHIDValueCallback              callback,
-                                void *                          context)
+                                void * _Nullable                context)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*! @function   IOHIDManagerSetInputValueMatching
@@ -325,7 +328,7 @@
 CF_EXPORT
 void IOHIDManagerSetInputValueMatching(
                                 IOHIDManagerRef                 manager,
-                                CFDictionaryRef                 matching)
+                                CFDictionaryRef _Nullable       matching)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*! @function   IOHIDManagerSetInputValueMatchingMultiple
@@ -342,7 +345,7 @@
 CF_EXPORT
 void IOHIDManagerSetInputValueMatchingMultiple(
                                                IOHIDManagerRef                 manager,
-                                               CFArrayRef                      multiple)
+                                               CFArrayRef _Nullable            multiple)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*!
@@ -365,6 +368,8 @@
 AVAILABLE_MAC_OS_X_VERSION_10_6_AND_LATER;
 
 
+CF_IMPLICIT_BRIDGING_DISABLED
+CF_ASSUME_NONNULL_END
 
 __END_DECLS
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDQueue.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDQueue.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDQueue.h	2015-08-23 00:59:23.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDQueue.h	2016-05-21 06:36:20.000000000 +0200
@@ -58,10 +58,13 @@
 
 __BEGIN_DECLS
 
+CF_ASSUME_NONNULL_BEGIN
+CF_IMPLICIT_BRIDGING_ENABLED
+
 /*! @typedef IOHIDQueueRef
 	This is the type of a reference to the IOHIDQueue.
 */
-typedef struct __IOHIDQueue * IOHIDQueueRef;
+typedef struct CF_BRIDGED_TYPE(id) __IOHIDQueue * IOHIDQueueRef;
 
 /*!
 	@function   IOHIDQueueGetTypeID
@@ -83,8 +86,8 @@
     @result     Returns a new IOHIDQueueRef.
 */
 CF_EXPORT
-IOHIDQueueRef IOHIDQueueCreate(
-                                CFAllocatorRef                  allocator, 
+IOHIDQueueRef _Nullable IOHIDQueueCreate(
+                                CFAllocatorRef _Nullable        allocator,
                                 IOHIDDeviceRef                  device,
                                 CFIndex                         depth,
                                 IOOptionBits                    options)
@@ -232,7 +235,7 @@
 void IOHIDQueueRegisterValueAvailableCallback(
                                 IOHIDQueueRef                   queue,
                                 IOHIDCallback                   callback,
-                                void *                          context)
+                                void * _Nullable                context)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*! 
@@ -269,6 +272,9 @@
                                 CFTimeInterval                  timeout)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
+CF_IMPLICIT_BRIDGING_DISABLED
+CF_ASSUME_NONNULL_END
+
 __END_DECLS
 
 #endif /* _IOKIT_HID_IOHIDQUEUE_USER_H */
\ No newline at end of file
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDTransaction.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDTransaction.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDTransaction.h	2015-08-23 00:59:23.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDTransaction.h	2016-05-21 06:36:20.000000000 +0200
@@ -49,10 +49,13 @@
 
 __BEGIN_DECLS
 
+CF_ASSUME_NONNULL_BEGIN
+CF_IMPLICIT_BRIDGING_ENABLED
+
 /*! @typedef IOHIDTransactionRef
 	This is the type of a reference to the IOHIDTransaction.
 */
-typedef struct __IOHIDTransaction * IOHIDTransactionRef;
+typedef struct CF_BRIDGED_TYPE(id) __IOHIDTransaction * IOHIDTransactionRef;
 
 /*!
 	@function   IOHIDTransactionGetTypeID
@@ -75,8 +78,8 @@
     @result     Returns a new IOHIDTransactionRef.
 */
 CF_EXPORT
-IOHIDTransactionRef IOHIDTransactionCreate(
-                                CFAllocatorRef                  allocator, 
+IOHIDTransactionRef _Nullable IOHIDTransactionCreate(
+                                CFAllocatorRef _Nullable        allocator,
                                 IOHIDDeviceRef                  device,
                                 IOHIDTransactionDirectionType   direction,
                                 IOOptionBits                    options)
@@ -233,7 +236,7 @@
     @result     Returns IOHIDValueRef for the given element.
 */
 CF_EXPORT
-IOHIDValueRef IOHIDTransactionGetValue(
+IOHIDValueRef _Nullable IOHIDTransactionGetValue(
                                 IOHIDTransactionRef             transaction,
                                 IOHIDElementRef                 element,
                                 IOOptionBits                    options)
@@ -282,8 +285,8 @@
 IOReturn IOHIDTransactionCommitWithCallback(
                                 IOHIDTransactionRef             transaction,
                                 CFTimeInterval                  timeout, 
-                                IOHIDCallback                   callback, 
-                                void *                          context)
+                                IOHIDCallback _Nullable         callback,
+                                void * _Nullable                context)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*! 
@@ -297,7 +300,11 @@
 void IOHIDTransactionClear(
                                 IOHIDTransactionRef             transaction)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
-                                
+
+
+CF_IMPLICIT_BRIDGING_DISABLED
+CF_ASSUME_NONNULL_END
+
 __END_DECLS
 
 #endif /* _IOKIT_HID_IOHIDTRANSACTION_USER_H */
\ No newline at end of file
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDUsageTables.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDUsageTables.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDUsageTables.h	2015-11-11 08:21:27.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDUsageTables.h	2016-06-03 23:10:18.000000000 +0200
@@ -576,6 +576,15 @@
     kHIDUsage_LED_GenericIndicator    = 0x4B,    /* On/Off Control */
     kHIDUsage_LED_SystemSuspend    = 0x4C,    /* On/Off Control */
     kHIDUsage_LED_ExternalPowerConnected    = 0x4D,    /* On/Off Control */
+    kHIDUsage_LED_PlayerIndicator   = 0x4E, /* Collection Logical */
+    kHIDUsage_LED_Player1   = 0x4F,  /* Selector */
+    kHIDUsage_LED_Player2   = 0x50,  /* Selector */
+    kHIDUsage_LED_Player3   = 0x51,  /* Selector */
+    kHIDUsage_LED_Player4   = 0x52,  /* Selector */
+    kHIDUsage_LED_Player5   = 0x53,  /* Selector */
+    kHIDUsage_LED_Player6   = 0x54,  /* Selector */
+    kHIDUsage_LED_Player7   = 0x55,  /* Selector */
+    kHIDUsage_LED_Player8   = 0x56,  /* Selector */
     /* 0x4E - 0xFFFF Reserved */
     kHIDUsage_LED_Reserved = 0xFFFF
 };
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDValue.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDValue.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDValue.h	2015-08-23 00:59:23.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDValue.h	2016-05-21 06:36:20.000000000 +0200
@@ -49,6 +49,9 @@
 
 __BEGIN_DECLS
 
+CF_ASSUME_NONNULL_BEGIN
+CF_IMPLICIT_BRIDGING_ENABLED
+
 /*!
 	@function   IOHIDValueGetTypeID
 	@abstract   Returns the type identifier of all IOHIDValue instances.
@@ -71,7 +74,7 @@
     @result     Returns a reference to a new IOHIDValueRef.
 */
 CF_EXPORT
-IOHIDValueRef IOHIDValueCreateWithIntegerValue(CFAllocatorRef allocator, IOHIDElementRef element, uint64_t timeStamp, CFIndex value)
+IOHIDValueRef IOHIDValueCreateWithIntegerValue(CFAllocatorRef _Nullable allocator, IOHIDElementRef element, uint64_t timeStamp, CFIndex value)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*!
@@ -89,7 +92,7 @@
     @result     Returns a reference to a new IOHIDValueRef.
 */
 CF_EXPORT
-IOHIDValueRef IOHIDValueCreateWithBytes(CFAllocatorRef allocator, IOHIDElementRef element, uint64_t timeStamp, const uint8_t * bytes, CFIndex length)
+IOHIDValueRef _Nullable IOHIDValueCreateWithBytes(CFAllocatorRef _Nullable allocator, IOHIDElementRef element, uint64_t timeStamp, const uint8_t * bytes, CFIndex length)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*!
@@ -107,7 +110,7 @@
     @result     Returns a reference to a new IOHIDValueRef.
 */
 CF_EXPORT
-IOHIDValueRef IOHIDValueCreateWithBytesNoCopy(CFAllocatorRef allocator, IOHIDElementRef element, uint64_t timeStamp, const uint8_t * bytes, CFIndex length)
+IOHIDValueRef _Nullable IOHIDValueCreateWithBytesNoCopy(CFAllocatorRef _Nullable allocator, IOHIDElementRef element, uint64_t timeStamp, const uint8_t * bytes, CFIndex length)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
 /*!
@@ -184,6 +187,9 @@
 double_t IOHIDValueGetScaledValue(IOHIDValueRef value, IOHIDValueScaleType type)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
+CF_IMPLICIT_BRIDGING_DISABLED
+CF_ASSUME_NONNULL_END
+
 __END_DECLS
 
 #endif /* _IOKIT_HID_IOHIDELEMENTEVENT_H */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDParameter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDParameter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDParameter.h	2015-08-27 02:05:39.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDParameter.h	2016-06-03 23:10:18.000000000 +0200
@@ -70,6 +70,9 @@
 #define kIOHIDKeyboardCapsLockDoesLockKey       "HIDKeyboardCapsLockDoesLock"
 #define kIOHIDKeyboardSupportsF12EjectKey       "HIDKeyboardSupportsF12Eject"
 #define kIOHIDKeyboardSupportedModifiersKey     "HIDKeyboardSupportedModifiers"
+#define kIOHIDKeyboardGlobalModifiersKey        "HIDKeyboardGlobalModifiers"
+#define kIOHIDServiceUseGlobalModifiersKey      "HIDServiceUseGlobalModifiers"
+
 
 #define kIOHIDPointerResolutionKey		"HIDPointerResolution"
 #define kIOHIDResetPointerKey			"HIDResetPointer"
@@ -136,6 +139,10 @@
 // shift keys in sequence will toggle sticky keys on or off
 #define kIOHIDStickyKeysShiftTogglesKey	"HIDStickyKeysShiftToggles"
 
+//
+//
+#define kIOHIDMouseClickNotification    "HIDClickNotification"
+
 // if kIOHIDMouseKeysOptionTogglesKey is 1, then a sequence of five
 // option keys in sequence will toggle mouse keys on or off
 #define kIOHIDMouseKeysOptionTogglesKey	"HIDMouseKeysOptionToggles"
@@ -328,6 +335,7 @@
     kIOHIDNumLockState              = 0x00000002,
     kIOHIDActivityUserIdle          = 0x00000003,
     kIOHIDActivityDisplayOn         = 0x00000004,
+    kIOHIDModifierFlags             = 0x00000005
 };
 
 #endif /* !_DEV_EVSIO_H */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOLLEvent.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOLLEvent.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOLLEvent.h	2015-08-27 02:05:39.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOLLEvent.h	2016-06-03 23:10:18.000000000 +0200
@@ -188,6 +188,10 @@
 #define NX_SUBTYPE_SLEEP_EVENT				11
 #define NX_SUBTYPE_RESTART_EVENT			12
 #define NX_SUBTYPE_SHUTDOWN_EVENT			13
+#define NX_SUBTYPE_MENU               16
+#define NX_SUBTYPE_ACCESSIBILITY      17
+
+
 
 #define NX_SUBTYPE_STICKYKEYS_ON			100
 #define NX_SUBTYPE_STICKYKEYS_OFF			101
@@ -522,6 +526,7 @@
     UInt64              service_id __attribute__ ((packed)); /* service id */
     SInt32              ext_pid;    /* external pid */
 } NXEvent, *NXEventPtr;
+
 #endif
 
 /* The current version number of the NXEvent structure. */
@@ -559,5 +564,20 @@
                             NX_TABLETPOINTERMASK | NX_TABLETPROXIMITYMASK \
                         )
 
+
+#define  NX_EVENT_EXTENSION_LOCATION_INVALID            0x1
+#define  NX_EVENT_EXTENSION_LOCATION_TYPE_FLOAT         0x2
+#define  NX_EVENT_EXTENSION_LOCATION_DEVICE_SCALED      0x4
+#define  NX_EVENT_EXTENSION_MOUSE_DELTA_TYPE_FLOAT      0x8
+
+typedef struct _NXEventExtension {
+    UInt32              flags;
+} NXEventExtension;
+
+typedef struct _NXEventExt {
+    NXEvent             payload;
+    NXEventExtension    extension;
+} NXEventExt;
+
 #endif /* !_DEV_EVENT_H */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/ev_keymap.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/ev_keymap.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/ev_keymap.h	2015-08-27 02:05:39.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/ev_keymap.h	2016-06-03 23:10:18.000000000 +0200
@@ -85,6 +85,8 @@
 #define NX_NUM_SCANNED_SPECIALKEYS	24 /* First 24 special keys are */
 					  /* actively scanned in kernel */
 
+#define NX_KEYTYPE_MENU		25
+
 /* Mask of special keys that are posted as events */
 
 #define NX_SPECIALKEY_POST_MASK		\
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/iokitmig.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/iokitmig.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/iokitmig.h	2015-08-23 01:00:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/iokitmig.h	2016-05-21 06:37:17.000000000 +0200
@@ -14,6 +14,29 @@
 #include <mach/message.h>
 #include <mach/mig_errors.h>
 #include <mach/port.h>
+	
+/* BEGIN MIG_STRNCPY_ZEROFILL CODE */
+
+#if defined(__has_include)
+#if __has_include(<mach/mig_strncpy_zerofill_support.h>)
+#ifndef USING_MIG_STRNCPY_ZEROFILL
+#define USING_MIG_STRNCPY_ZEROFILL
+#endif
+#ifndef __MIG_STRNCPY_ZEROFILL_FORWARD_TYPE_DECLS__
+#define __MIG_STRNCPY_ZEROFILL_FORWARD_TYPE_DECLS__
+#ifdef __cplusplus
+extern "C" {
+#endif
+	extern int mig_strncpy_zerofill(char *dest, const char *src, int len) __attribute__((weak_import));
+#ifdef __cplusplus
+}
+#endif
+#endif /* __MIG_STRNCPY_ZEROFILL_FORWARD_TYPE_DECLS__ */
+#endif /* __has_include(<mach/mig_strncpy_zerofill_support.h>) */
+#endif /* __has_include */
+	
+/* END MIG_STRNCPY_ZEROFILL CODE */
+
 
 #ifdef AUTOTEST
 #ifndef FUNCTION_PTR_T
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/network/IONetworkController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/network/IONetworkController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/network/IONetworkController.h	2015-08-27 02:09:01.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/network/IONetworkController.h	2016-06-03 23:05:42.000000000 +0200
@@ -217,16 +217,22 @@
     @constant kIONetworkFeatureTransmitCompletionStatus Set this bit to
         advertise the capability to report per-packet transmit completion status.
         See <code>IONetworkInterface::reportTransmitCompletionStatus</code>.
+    @constant kIONetworkFeatureHWTimeStamp Set this bit to advertise
+         the capability to compute per-packet timestamp in hardware.
+    @constant kIONetworkFeatureHWTimeStamp Set this bit to advertise
+        the capability to compute per-packet timestamp in software.
 */
 
 enum {
-    kIONetworkFeatureNoBSDWait                  = 0x01,
-    kIONetworkFeatureHardwareVlan               = 0x02,
-    kIONetworkFeatureSoftwareVlan               = 0x04,
-    kIONetworkFeatureMultiPages                 = 0x08,
-    kIONetworkFeatureTSOIPv4                    = 0x10,
-    kIONetworkFeatureTSOIPv6                    = 0x20,
-    kIONetworkFeatureTransmitCompletionStatus   = 0x40
+    kIONetworkFeatureNoBSDWait                  = 0x001,
+    kIONetworkFeatureHardwareVlan               = 0x002,
+    kIONetworkFeatureSoftwareVlan               = 0x004,
+    kIONetworkFeatureMultiPages                 = 0x008,
+    kIONetworkFeatureTSOIPv4                    = 0x010,
+    kIONetworkFeatureTSOIPv6                    = 0x020,
+    kIONetworkFeatureTransmitCompletionStatus   = 0x040,
+    kIONetworkFeatureHWTimeStamp                = 0x080,
+    kIONetworkFeatureSWTimeStamp                = 0x100
 };
 
 #endif /* !_IONETWORKCONTROLLER_H */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/ps/IOPSKeys.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/ps/IOPSKeys.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/ps/IOPSKeys.h	2015-08-23 00:59:23.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/ps/IOPSKeys.h	2016-05-21 06:36:20.000000000 +0200
@@ -266,13 +266,12 @@
 /*!
  * @define      kIOPSPowerSourceIDKey
  *
- * @abstract    CFNumber key uniquely identifying a UPS attached to the system.
+ * @abstract    CFNumber key uniquely identifying the power source.
  *
  * @discussion
  *              <ul>
- *              <li> Apple UPS power sources will publish this key.
- *              <li> Callers should not set this key; OS X power management will publish this key for UPS's.
- *              <li> Type CFNumber, kCFNumberIntType, uniquely identifying an attached UPS.
+ *              <li> Callers should not set this key; OS X power management will publish this key for all power sources
+ *              <li> Type CFNumber, kCFNumberIntType, uniquely identifying the power source
  *              </ul>
  */
  
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/pwr_mgt/IOPM.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/pwr_mgt/IOPM.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/pwr_mgt/IOPM.h	2015-08-27 01:55:11.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/pwr_mgt/IOPM.h	2016-06-03 22:55:01.000000000 +0200
@@ -612,6 +612,7 @@
 #define kIOPMPSAdapterDetailsAmperageKey	    "Amperage"
 #define kIOPMPSAdapterDetailsDescriptionKey	    "Description"
 #define kIOPMPSAdapterDetailsPMUConfigurationKey    "PMUConfiguration"
+#define kIOPMPSAdapterDetailsVoltage            "AdapterVoltage"
 
 // Battery's time remaining estimate is invalid this long (seconds) after a wake
 #define kIOPMPSInvalidWakeSecondsKey           "BatteryInvalidWakeSeconds"
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/pwr_mgt/IOPMLib.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/pwr_mgt/IOPMLib.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/pwr_mgt/IOPMLib.h	2015-08-23 00:59:23.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/pwr_mgt/IOPMLib.h	2016-05-21 06:36:20.000000000 +0200
@@ -204,7 +204,7 @@
     @param notificationID A copy of the notification ID which came as part of the power state change notification being acknowledged.
     @result             Returns kIOReturnSuccess or an error condition if request failed.
 */
-IOReturn IOAllowPowerChange ( io_connect_t kernelPort, long notificationID )
+IOReturn IOAllowPowerChange ( io_connect_t kernelPort, intptr_t notificationID )
                             AVAILABLE_MAC_OS_X_VERSION_10_0_AND_LATER;
 
 /*! @function IOCancelPowerChange
@@ -220,7 +220,7 @@
     @param notificationID A copy of the notification ID which came as part of the power state change notification being acknowledged.
     @result Returns kIOReturnSuccess or an error condition if request failed.
  */
-IOReturn IOCancelPowerChange ( io_connect_t kernelPort, long notificationID )
+IOReturn IOCancelPowerChange ( io_connect_t kernelPort, intptr_t notificationID )
                             AVAILABLE_MAC_OS_X_VERSION_10_0_AND_LATER;
 
 /*!
@@ -458,7 +458,7 @@
  *	                    Caller must specify this argument.
  *
  * @param Details 	    A CFString value to correspond to key <code>@link kIOPMAssertionDetailsKey@/link</code>.
- *	                    Caller my pass NULL, but it helps power users and administrators identify the
+ *	                    Caller may pass NULL, but it helps power users and administrators identify the
  *                      reasons for this assertion.
  *
  * @param HumanReadableReason
@@ -481,8 +481,8 @@
  * @result              kIOReturnSuccess, or another IOKit return code on error.
  */
 IOReturn	IOPMAssertionCreateWithDescription(
-                                           CFStringRef  AssertionType, 
-                                           CFStringRef  Name, 
+                                           CFStringRef  AssertionType,
+                                           CFStringRef  Name,
                                            CFStringRef  Details,
                                            CFStringRef  HumanReadableReason,
                                            CFStringRef  LocalizationBundlePath,
@@ -490,7 +490,7 @@
                                            CFStringRef  TimeoutAction,
                                            IOPMAssertionID  *AssertionID)
 __OSX_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_4_3);
-    
+
 
 
 /*!
@@ -500,21 +500,22 @@
  * @param AssertionProperties   Dictionary providing the properties of the assertion that need to be created.
  * @param AssertionID           (Output) On successful return, contains a unique reference to a PM assertion.
  *
- * @discussion          
- *      Create a new PM assertion - the caller must specify the type of assertion, initial level, and its 
+ * @discussion
+ *      Create a new PM assertion - the caller must specify the type of assertion, initial level, and its
  *      properties as @link IOPMAssertionDictionaryKeys@/link keys in the <code>AssertionProperties</code> dictionary.
- *      The following keys are recommend and/or required to be specified in the AssertionProperties 
+ *      The following keys are recommend and/or required to be specified in the AssertionProperties
  *      dictionary argument.
  *      <ul>
  *          <li> REQUIRED: <code>kIOPMAssertionTypeKey</code> define the assertion type.
  *
- *          <li> REQUIRED: <code>kIOPMAssertionValueKey</code> define an inital value.
- *
  *          <li> REQUIRED: <code>kIOPMAssertionNameKey</code> Caller must describe the name for the activity that
- *               requires the change in behavior provided by the assertion. 
+ *               requires the change in behavior provided by the assertion.
+ *
+ *          <li> OPTIONAL: <code>kIOPMAssertionLevelKey</code> define an inital value. If not set, assertion is
+ *               turned on after creation.
  *
  *          <li> OPTIONAL: <code>kIOPMAssertionDetailsKey</code> Caller may describe context-specific data about the
- *               assertion. 
+ *               assertion.
  *
  *          <li> OPTIONAL: <code>kIOPMAssertionHumanReadableReasonKey</code> Caller may describe the reason for creating the assertion
  *              in a localizable CFString. This should be a human readable phrase that describes the actions the
@@ -539,13 +540,13 @@
 /*!
  * @function            IOPMAssertionDeclareUserActivity
  *
- * @abstract            Declares that the user is active on the system. 
+ * @abstract            Declares that the user is active on the system.
  *
- * @discussion          This causes the display to power on and postpone display sleep, 
- *                      up to the user's display sleep Energy Saver settings. 
+ * @discussion          This causes the display to power on and postpone display sleep,
+ *                      up to the user's display sleep Energy Saver settings.
  *
  *                      If you need to hold the display awake for a longer period and you know
- *                      how long you'd like to hold it, consider taking assertion 
+ *                      how long you'd like to hold it, consider taking assertion
  *                      <code>@link kIOPMAssertPreventUserIdleDisplaySleep @/link</code> using
  *                      <code>@link IOPMAssertionCreateWithDescription @/link</code> API instead.
  *
@@ -679,7 +680,7 @@
  * @discussion          Only the process that created an assertion may change its properties.
  * @param theAssertion  The <code>@link IOPMAssertionID@/link</code> of the assertion to modify.
  * @param theProperty   The CFString key, from <code>@link IOPMAssertionDictionaryKeys@/link</code> to modify.
- * @param theValue      The property to set. It must be a CFNumber or CFString, as specified by the property key named in whichProperty.
+ * @param theValue      The property to set. The value must match the CF type expected for the specified key.
  * @result              Returns <code>@link kIOReturnNotPriviliged@/link</code> if the caller doesn't 
  *                          have permission to modify this assertion.
  *                      Returns <code>@link kIOReturnNotFound@/link</code> if PM can't locate this assertion.
@@ -757,9 +758,6 @@
  *
  * @abstract            The simplest API to create a power assertion.
  *
- * @deprecated          IOPMAssertionCreate is deprecated in favor of <code>@link IOPMAssertionCreateWithProperties@/link</code>.
- *                      Please use that version of this API instead.
- *
  * @discussion          No special privileges are necessary to make this call - any process may
  *                      activate a power assertion. Caller must specify an AssertionName - NULL is not
  *                      a valid input.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/scsi/SCSICmds_INQUIRY_Definitions.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/scsi/SCSICmds_INQUIRY_Definitions.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/scsi/SCSICmds_INQUIRY_Definitions.h	2015-08-27 04:10:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/scsi/SCSICmds_INQUIRY_Definitions.h	2016-06-03 23:14:33.000000000 +0200
@@ -643,6 +643,12 @@
 Page Code 83h.
 @constant kINQUIRY_Page89_PageCode
 Page Code 89h.
+@constant kINQUIRY_PageB0_PageCode
+Page Code B0h.
+@constant kINQUIRY_PageB1_PageCode
+Page Code B1h.
+@constant kINQUIRY_PageB2_PageCode
+Page Code B2h.
 */
 enum
 {
@@ -650,7 +656,9 @@
 	kINQUIRY_Page80_PageCode				= 0x80,
 	kINQUIRY_Page83_PageCode				= 0x83,
 	kINQUIRY_Page89_PageCode				= 0x89,
-	kINQUIRY_PageB1_PageCode				= 0xB1
+	kINQUIRY_PageB0_PageCode				= 0xB0,
+	kINQUIRY_PageB1_PageCode				= 0xB1,
+	kINQUIRY_PageB2_PageCode				= 0xB2
 };	
 
 
@@ -977,7 +985,7 @@
 /*!
 @struct SCSICmd_INQUIRY_Page89_Data
 @discussion INQUIRY Page 89h data as defined in the SAT 1.0
-specification. This section contians all structures and
+specification. This section contains all structures and
 definitions used by the INQUIRY command in response to a request
 for page 89h - ATA information VPD Page.
 */
@@ -996,11 +1004,44 @@
 	UInt8		IDENTIFY_DATA[512];
 } SCSICmd_INQUIRY_Page89_Data;
 
+#pragma pack(push, 1)
+
+/*!
+ @struct SCSICmd_INQUIRY_PageB0_Data
+ @discussion INQUIRY Page B0h data as defined in the SBC
+ specification. This section contains all structures and
+ definitions used by the INQUIRY command in response to a request
+ for page B0h - Block Limits VPD Page.
+ */
+typedef struct SCSICmd_INQUIRY_PageB0_Data
+{
+	UInt8 		PERIPHERAL_DEVICE_TYPE;					// 7-5 = Qualifier. 4-0 = Device type.
+	UInt8 		PAGE_CODE;								// Must be equal to B0h
+	UInt16 		PAGE_LENGTH;							// Must be equal to 3Ch
+	UInt8 		WSNZ;									// 0 = WSNZ, 7-1 = Reserved.
+	UInt8 		MAXIMUM_COMPARE_AND_WRITE_LENGTH;
+	UInt16 		OPTIMAL_TRANSFER_LENGTH_GRANULARITY;
+	UInt32		MAXIMUM_TRANSFER_LENGTH;
+	UInt32 		OPTIMAL_TRANSFER_LENGTH;
+	UInt32 		MAXIMUM_PREFETCH_LENGTH;
+	UInt32 		MAXIMUM_UNMAP_LBA_COUNT;
+	UInt32 		MAXIMUM_UNMAP_BLOCK_DESCRIPTOR_COUNT;
+	UInt32 		OPTIMAL_UNMAP_GRANULARITY;
+	UInt32 		UNMAP_GRANULARITY_ALIGNMENT;
+	UInt64 		MAXIMUM_WRITE_SAME_LENGTH;
+	UInt32		MAXIMUM_ATOMIC_TRANSFER_LENGTH;
+	UInt32		ATOMIC_ALIGNMENT;
+	UInt32		ATOMIC_TRANSFER_LENGTH_GRANULARITY;
+	UInt32		MAXIMUM_ATOMIC_TRANSFER_LENGTH_WITH_ATOMIC_BOUNDARY;
+	UInt32		MAXIMUM_ATOMIC_BOUNDARY_SIZE;
+} SCSICmd_INQUIRY_PageB0_Data;
+
+#pragma pack(pop)
 
 /*!
 @struct SCSICmd_INQUIRY_PageB1_Data
 @discussion INQUIRY Page B1h data as defined in the SBC 
-specification. This section contians all structures and
+specification. This section contains all structures and
 definitions used by the INQUIRY command in response to a request
 for page B1h - Block Device Characteristics VPD Page.
 */
@@ -1019,6 +1060,35 @@
 	kINQUIRY_PageB1_Page_Length	= 0x3C
 };
 
+#pragma pack(push, 1)
+
+/*!
+ @struct SCSICmd_INQUIRY_PageB2_Data
+ @discussion INQUIRY Page B2h data as defined in the SBC
+ specification. This section contains all structures and
+ definitions used by the INQUIRY command in response to a request
+ for page B2h - Logical Block Provisioning VPD Page.
+ */
+typedef struct SCSICmd_INQUIRY_PageB2_Data
+{
+	UInt8 		PERIPHERAL_DEVICE_TYPE;			// 7-5 = Qualifier. 4-0 = Device type.
+	UInt8 		PAGE_CODE;						// Must be equal to B2h.
+	UInt16 		PAGE_LENGTH;					// Must be n-3.
+	UInt8 		THRESHOLD_EXPONENT;
+	UInt8 		LBP_FLAGS;						// 7 = LBPU, 6 = LBPWS, 5 = LBPWS10,
+												// 4-2 = LBPRZ, 1 = ANC_SUP, 0 = DP.
+	UInt8 		MINIMUM_PERCENTAGE;				// 7-3 = MINIMUM PERCENTAGE,
+												// 2-0 = PROVISIONING TYPE.
+	UInt8		THRESHOLD_PERCENTAGE;
+} SCSICmd_INQUIRY_PageB2_Data;
+
+typedef struct SCSICmd_INQUIRY_PageB2_Provisioning_Group_Descriptor
+{
+	UInt8	DESIGNATION_DESCRIPTOR[20];
+	UInt8	RESERVED[18];
+} SCSICmd_INQUIRY_PageB2_Provisioning_Group_Descriptor;
+
+#pragma pack(pop)
 
 /*!
 @define kIOPropertySATVendorIdentification
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/scsi/SCSICommandOperationCodes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/scsi/SCSICommandOperationCodes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/scsi/SCSICommandOperationCodes.h	2015-08-27 04:10:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/scsi/SCSICommandOperationCodes.h	2016-06-03 23:14:33.000000000 +0200
@@ -170,7 +170,7 @@
     kSCSICmd_REPAIR_TRACK                   = 0x58,
     kSCSICmd_REPORT_DEVICE_IDENTIFIER    	= 0xA3,
     kSCSICmd_REPORT_KEY                     = 0xA4,
-    kSCSICmd_REPORT_LUNS                    = 0xA0, 
+    kSCSICmd_REPORT_LUNS                    = 0xA0,
     kSCSICmd_REQUEST_SENSE                  = 0x03,
     kSCSICmd_RESERVE_6                      = 0x16,
     kSCSICmd_RESERVE_10                     = 0x56,
@@ -207,7 +207,8 @@
     kSCSICmd_SYNCHRONIZE_CACHE              = 0x35,
     kSCSICmd_SYNCHRONIZE_CACHE_16           = 0x91,
     kSCSICmd_TEST_UNIT_READY                = 0x00,
-	kSCSICmd_UPDATE_BLOCK					= 0x3D,
+    kSCSICmd_UPDATE_BLOCK					= 0x3D,
+    kSCSICmd_UNMAP                          = 0x42,
     kSCSICmd_VERIFY_10                      = 0x2F,
     kSCSICmd_VERIFY_12                      = 0xAF,
     kSCSICmd_VERIFY_16                      = 0x8F,
@@ -254,6 +255,7 @@
 	kSCSIServiceAction_REPORT_ALIASES								= 0x0B,
 	kSCSIServiceAction_REPORT_DEVICE_IDENTIFIER						= 0x05,
 	kSCSIServiceAction_REPORT_PRIORITY								= 0x0E,
+	kSCSIServiceAction_REPORT_PROVISIONING_INITIALIZATION_PATTERN   = 0x1D,
 	kSCSIServiceAction_REPORT_SUPPORTED_OPERATION_CODES				= 0x0C,
 	kSCSIServiceAction_REPORT_SUPPORTED_TASK_MANAGEMENT_FUNCTIONS	= 0x0D,
 	kSCSIServiceAction_REPORT_TARGET_PORT_GROUPS					= 0x0A
@@ -271,8 +273,9 @@
 /* Service Action Definitions for the SERVICE ACTION IN (9Eh) command */
 enum
 {
+	kSCSIServiceAction_GET_LBA_STATUS       = 0x12,
 	kSCSIServiceAction_READ_CAPACITY_16		= 0x10,
-	kSCSIServiceAction_READ_LONG_16			= 0x11	
+	kSCSIServiceAction_READ_LONG_16			= 0x11,
 };
 
 /* Service Action Definitions for the SERVICE ACTION OUT (9Fh) command */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/usb/IOUSBLib.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/usb/IOUSBLib.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/usb/IOUSBLib.h	2015-08-27 02:12:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/usb/IOUSBLib.h	2016-06-07 01:22:45.000000000 +0200
@@ -921,7 +921,39 @@
 0x17, 0xF9, 0xE5, 0x9C, 0xB0, 0xA1, 0x40, 0x1D,                                                 \
 0x9A, 0xC0, 0x8D, 0xE2, 0x7A, 0xC6, 0x04, 0x7E)
 
+// 33A85DB0-0C3B-4328-8F02-FDA81B117F4C
+/*!
+ @defined kIOUSBInterfaceInterfaceID800
+ @discussion This UUID constant is used to obtain an interface interface corresponding to
+ an IOUSBInterface user client in the kernel. The type of this device interface is
+ kIOUSBInterfaceInterfaceID800. This device interface is obtained after the device interface
+ for the service itself has been obtained.
+
+ <b>Note:</b> The kIOUSBInterfaceInterfaceID800 is returned only by version 900.4.1 or above of
+ the IOUSBFamily. This version of IOUSBFamily shipped with Mac OS X version 10.12.  If your software
+ is running on a version of Mac OS X prior to 10.12 you will need to use the UUID kIOUSBInterfaceInterfaceID,
+ kIOUSBInterfaceInterfaceID182, kIOUSBInterfaceInterfaceID183, kIOUSBInterfaceInterfaceID190, kIOUSBInterfaceInterfaceID192,
+ kIOUSBInterfaceInterfaceID197, kIOUSBInterfaceInterfaceID220, kIOUSBInterfaceInterfaceID245, kIOUSBInterfaceInterfaceID300,
+ kIOUSBInterfaceInterfaceID500, kIOUSBInterfaceInterfaceID550 , kIOUSBInterfaceInterfaceID650 or kIOUSBInterfaceInterfaceID700 and you will not have access to some functions.
+
+ Example:
+ <pre>
+ @textblock
+ IOCFPluginInterface             **iodev; 	// obtained earlier
+
+ IOUSBInterfaceInterface800      **intf;     // fetching this now
+ IOReturn                        err;
+
+ err = (*iodev)->QueryInterface(iodev,
+ CFUUIDGetUUIDBytes(kIOUSBInterfaceInterfaceID800),
+ (LPVoid)&intf);
+ @/textblock
+ </pre>
+ */
 
+#define kIOUSBInterfaceInterfaceID800 CFUUIDGetConstantUUIDWithBytes(kCFAllocatorSystemDefault, \
+0x33, 0xA8, 0x5D, 0xB0, 0x0C, 0x3B, 0x43, 0x28,                                                 \
+0x8F, 0x02, 0xFD, 0xA8, 0x1B, 0x11, 0x7F, 0x4C)
 
 /*!
  @interface IOUSBDeviceInterface
@@ -4129,6 +4161,120 @@
 	
 } IOUSBInterfaceInterface700;
 
+/*!
+ @interface IOUSBInterfaceInterface800
+ @abstract   The object you use to access a USB interface interface from user space, returned by the IOUSBFamily
+ version 8.0.0 and above.
+ @discussion The functions listed here include all of the functions defined for the IOUSBInterfaceInterface,
+ IOUSBInterfaceInterface182, IOUSBInterfaceInterface183, IOUSBInterfaceInterface190, IOUSBInterfaceInterface192,
+ IOUSBInterfaceInterface197, IOUSBInterfaceInterface220, IOUSBInterfaceInterface245, IOUSBInterfaceInterface300,
+ IOUSBInterfaceInterface500, IOUSBInterfaceInterface550 and IOUSBInterfaceInterface650, IOUSBInterfaceInterface700 as well as some new functions that are available on
+ Mac OS X version 10.11 and later.
+ @super IOUSBInterfaceInterface700
+ */
+
+typedef struct IOUSBInterfaceStruct800 {
+    IUNKNOWN_C_GUTS;
+    IOReturn (*CreateInterfaceAsyncEventSource)(void *self, CFRunLoopSourceRef *source);
+    CFRunLoopSourceRef (*GetInterfaceAsyncEventSource)(void *self);
+    IOReturn (*CreateInterfaceAsyncPort)(void *self, mach_port_t *port);
+    mach_port_t (*GetInterfaceAsyncPort)(void *self);
+    IOReturn (*USBInterfaceOpen)(void *self);
+    IOReturn (*USBInterfaceClose)(void *self);
+    IOReturn (*GetInterfaceClass)(void *self, UInt8 *intfClass);
+    IOReturn (*GetInterfaceSubClass)(void *self, UInt8 *intfSubClass);
+    IOReturn (*GetInterfaceProtocol)(void *self, UInt8 *intfProtocol);
+    IOReturn (*GetDeviceVendor)(void *self, UInt16 *devVendor);
+    IOReturn (*GetDeviceProduct)(void *self, UInt16 *devProduct);
+    IOReturn (*GetDeviceReleaseNumber)(void *self, UInt16 *devRelNum);
+    IOReturn (*GetConfigurationValue)(void *self, UInt8 *configVal);
+    IOReturn (*GetInterfaceNumber)(void *self, UInt8 *intfNumber);
+    IOReturn (*GetAlternateSetting)(void *self, UInt8 *intfAltSetting);
+    IOReturn (*GetNumEndpoints)(void *self, UInt8 *intfNumEndpoints);
+    IOReturn (*GetLocationID)(void *self, UInt32 *locationID);
+    IOReturn (*GetDevice)(void *self, io_service_t *device);
+    IOReturn (*SetAlternateInterface)(void *self, UInt8 alternateSetting);
+    IOReturn (*GetBusFrameNumber)(void *self, UInt64 *frame, AbsoluteTime *atTime);
+    IOReturn (*ControlRequest)(void *self, UInt8 pipeRef, IOUSBDevRequest *req);
+    IOReturn (*ControlRequestAsync)(void *self, UInt8 pipeRef, IOUSBDevRequest *req, IOAsyncCallback1 callback, void *refCon);
+    IOReturn (*GetPipeProperties)(void *self, UInt8 pipeRef, UInt8 *direction, UInt8 *number, UInt8 *transferType, UInt16 *maxPacketSize, UInt8 *interval);
+    IOReturn (*GetPipeStatus)(void *self, UInt8 pipeRef);
+    IOReturn (*AbortPipe)(void *self, UInt8 pipeRef);
+    IOReturn (*ResetPipe)(void *self, UInt8 pipeRef);
+    IOReturn (*ClearPipeStall)(void *self, UInt8 pipeRef);
+    IOReturn (*ReadPipe)(void *self, UInt8 pipeRef, void *buf, UInt32 *size);
+    IOReturn (*WritePipe)(void *self, UInt8 pipeRef, void *buf, UInt32 size);
+    IOReturn (*ReadPipeAsync)(void *self, UInt8 pipeRef, void *buf, UInt32 size, IOAsyncCallback1 callback, void *refcon);
+    IOReturn (*WritePipeAsync)(void *self, UInt8 pipeRef, void *buf, UInt32 size, IOAsyncCallback1 callback, void *refcon);
+    IOReturn (*ReadIsochPipeAsync)(void *self, UInt8 pipeRef, void *buf, UInt64 frameStart, UInt32 numFrames, IOUSBIsocFrame *frameList,
+                                   IOAsyncCallback1 callback, void *refcon);
+    IOReturn (*WriteIsochPipeAsync)(void *self, UInt8 pipeRef, void *buf, UInt64 frameStart, UInt32 numFrames, IOUSBIsocFrame *frameList,
+                                    IOAsyncCallback1 callback, void *refcon);
+    IOReturn (*ControlRequestTO)(void *self, UInt8 pipeRef, IOUSBDevRequestTO *req);
+    IOReturn (*ControlRequestAsyncTO)(void *self, UInt8 pipeRef, IOUSBDevRequestTO *req, IOAsyncCallback1 callback, void *refCon);
+    IOReturn (*ReadPipeTO)(void *self, UInt8 pipeRef, void *buf, UInt32 *size, UInt32 noDataTimeout, UInt32 completionTimeout);
+    IOReturn (*WritePipeTO)(void *self, UInt8 pipeRef, void *buf, UInt32 size, UInt32 noDataTimeout, UInt32 completionTimeout);
+    IOReturn (*ReadPipeAsyncTO)(void *self, UInt8 pipeRef, void *buf, UInt32 size, UInt32 noDataTimeout, UInt32 completionTimeout, IOAsyncCallback1 callback, void *refcon);
+    IOReturn (*WritePipeAsyncTO)(void *self, UInt8 pipeRef, void *buf, UInt32 size, UInt32 noDataTimeout, UInt32 completionTimeout, IOAsyncCallback1 callback, void *refcon);
+    IOReturn (*USBInterfaceGetStringIndex)(void *self, UInt8 *si);
+    IOReturn (*USBInterfaceOpenSeize)(void *self);
+    IOReturn (*ClearPipeStallBothEnds)(void *self, UInt8 pipeRef);
+    IOReturn (*SetPipePolicy)(void *self, UInt8 pipeRef, UInt16 maxPacketSize, UInt8 maxInterval);
+    IOReturn (*GetBandwidthAvailable)(void *self, UInt32 *bandwidth);
+    IOReturn (*GetEndpointProperties)(void *self, UInt8 alternateSetting, UInt8 endpointNumber, UInt8 direction, UInt8 *transferType, UInt16 *maxPacketSize, UInt8 *interval);
+    IOReturn (*LowLatencyReadIsochPipeAsync)(void *self, UInt8 pipeRef, void *buf, UInt64 frameStart, UInt32 numFrames, UInt32 updateFrequency, IOUSBLowLatencyIsocFrame *frameList,
+                                             IOAsyncCallback1 callback, void *refcon);
+    IOReturn (*LowLatencyWriteIsochPipeAsync)(void *self, UInt8 pipeRef, void *buf, UInt64 frameStart, UInt32 numFrames, UInt32 updateFrequency, IOUSBLowLatencyIsocFrame *frameList,
+                                              IOAsyncCallback1 callback, void *refcon);
+    IOReturn (*LowLatencyCreateBuffer)(void * self, void **buffer, IOByteCount size, UInt32 bufferType);
+    IOReturn (*LowLatencyDestroyBuffer) (void * self, void * buffer );
+    IOReturn (*GetBusMicroFrameNumber)(void *self, UInt64 *microFrame, AbsoluteTime *atTime);
+    IOReturn (*GetFrameListTime)(void *self, UInt32 *microsecondsInFrame);
+    IOReturn (*GetIOUSBLibVersion)(void *self, NumVersion *ioUSBLibVersion, NumVersion *usbFamilyVersion);
+    IOUSBDescriptorHeader * (*FindNextAssociatedDescriptor)(void *self, const void *currentDescriptor, UInt8 descriptorType);
+    IOUSBDescriptorHeader * (*FindNextAltInterface)(void *self, const void *current, IOUSBFindInterfaceRequest *request);
+    IOReturn (*GetBusFrameNumberWithTime)(void *self, UInt64 *frame, AbsoluteTime *atTime);
+    IOReturn (*GetPipePropertiesV2)(void *self, UInt8 pipeRef, UInt8 *direction, UInt8 *number, UInt8 *transferType, UInt16 *maxPacketSize, UInt8 *interval, UInt8 *maxBurst, UInt8 *mult, UInt16 *bytesPerInterval);
+    IOReturn (*GetPipePropertiesV3)(void *self, UInt8 pipeRef, IOUSBEndpointProperties *properties);
+    IOReturn (*GetEndpointPropertiesV3)(void *self, IOUSBEndpointProperties *properties);
+    IOReturn (*SupportsStreams)(void *self, UInt8 pipeRef, UInt32 *supportsStreams);
+    IOReturn (*CreateStreams)(void *self, UInt8 pipeRef, UInt32 streamID);
+    IOReturn (*GetConfiguredStreams)(void *self, UInt8 pipeRef, UInt32 *configuredStreams);
+    IOReturn (*ReadStreamsPipeTO)(void *self, UInt8 pipeRef, UInt32 streamID, void *buf, UInt32 *size, UInt32 noDataTimeout, UInt32 completionTimeout);
+    IOReturn (*WriteStreamsPipeTO)(void *self, UInt8 pipeRef, UInt32 streamID, void *buf, UInt32 size, UInt32 noDataTimeout, UInt32 completionTimeout);
+    IOReturn (*ReadStreamsPipeAsyncTO)(void *self, UInt8 pipeRef, UInt32 streamID, void *buf, UInt32 size, UInt32 noDataTimeout, UInt32 completionTimeout, IOAsyncCallback1 callback, void *refcon);
+    IOReturn (*WriteStreamsPipeAsyncTO)(void *self, UInt8 pipeRef, UInt32 streamID, void *buf, UInt32 size, UInt32 noDataTimeout, UInt32 completionTimeout, IOAsyncCallback1 callback, void *refcon);
+    IOReturn (*AbortStreamsPipe)(void *self, UInt8 pipeRef, UInt32 streamID);
+    IOReturn (*RegisterForNotification)(void * self, UInt64 notificationMask, IOAsyncCallback2 callback, void *refCon, UInt64 *pRegistrationToken);
+    IOReturn (*UnregisterNotification)(void *self, UInt64 registrationToken);
+    IOReturn (*AcknowledgeNotification)(void *self, UInt64 notificationToken);
+    IOReturn (*RegisterDriver)(void *self);
+
+    /*!
+     @function SetDeviceIdlePolicy
+     @abstract   Define an idling policy for the interface.
+     @discussion This method is called to enforce an an idle policy for the device. Note, the device does not have to be open to use this function.
+     @availability This function is only available with IOUSBInterfaceInterface800 and above.
+     @param      self Pointer to the IOUSBInterfaceInterface.
+     @param      deviceIdleTimeout The amount of time in ms a device is idle before it can be suspended.  Use 0 to prevent suspending an idle device.
+     @result     Returns kIOReturnSuccess if successful, kIOReturnNoDevice if there is no connection to an IOService, kIOReturnUnsupported is the bus doesn't support this function.
+     */
+    IOReturn (*SetDeviceIdlePolicy)(void* self, UInt32 deviceIdleTimeout);
+
+    /*!
+     @function SetPipeIdlePolicy
+     @abstract   Define an idling policy for the interface.
+     @discussion This method is called to enforce an an idle policy for the pipes. Note, the device does not have to be open to use this function.
+     @availability This function is only available with IOUSBInterfaceInterface800 and above.
+     @param      self Pointer to the IOUSBInterfaceInterface.
+     @param      pipeRef Index for the desired pipe (1 - GetNumEndpoints).
+     @param      ioIdleTimeout The amount of time in ms an IO is pending before it allows the device to be considered idle.  Use 0 to prevent idling the device while the IO is in progress, regardless of how long it takes.
+     @result     Returns kIOReturnSuccess if successful, kIOReturnNoDevice if there is no connection to an IOService, kIOReturnUnsupported is the bus doesn't support this function.
+     */
+    IOReturn (*SetPipeIdlePolicy)(void* self, UInt8 pipeRef, UInt32 ioIdleTimeout);
+
+} IOUSBInterfaceInterface800;
+
 #define kIOUSBDeviceClassName		"IOUSBDevice"
 #define kIOUSBInterfaceClassName	"IOUSBInterface"
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/usb/IOUSBUserClient.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/usb/IOUSBUserClient.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/usb/IOUSBUserClient.h	2015-08-27 02:12:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/usb/IOUSBUserClient.h	2016-06-07 01:22:45.000000000 +0200
@@ -95,6 +95,8 @@
     kUSBInterfaceUserClientUnregisterNotification,
     kUSBInterfaceUserClientAcknowledgeNotification,
     kUSBInterfaceUserClientRegisterDriver,
+    kUSBInterfaceUserClientSetDeviceIdlePolicy,
+    kUSBInterfaceUserClientSetPipeIdlePolicy,
     kIOUSBLibInterfaceUserClientNumCommands
 };
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/usb/USB.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/usb/USB.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/usb/USB.h	2015-08-27 02:12:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/usb/USB.h	2016-06-07 01:22:45.000000000 +0200
@@ -609,6 +609,43 @@
 	};
 	typedef struct IOUSBDeviceCapabilityContainerID		IOUSBDeviceCapabilityContainerID;
 	typedef IOUSBDeviceCapabilityContainerID *			IOUSBDeviceCapabilityContainerIDPtr;
+
+    /*!
+     @typedef IOUSBDeviceCapabilityBillboardAltConfig
+     @discussion Device Capability Billboard Alternate Setting Info
+     */
+    struct IOUSBDeviceCapabilityBillboardAltConfig {
+        UInt16          wSVID;
+        UInt8           bAltenateMode;
+        UInt8           iAlternateModeString;
+    };
+
+    typedef struct IOUSBDeviceCapabilityBillboardAltConfig		IOUSBDeviceCapabilityBillboardAltConfig;
+    typedef IOUSBDeviceCapabilityBillboardAltConfig *			IOUSBDeviceCapabilityBillboardAltConfigPtr;
+
+    /*!
+     @typedef IOUSBDeviceCapabilityBillboard
+     @discussion Device Capability Billboard
+     */
+    struct IOUSBDeviceCapabilityBillboard {
+        UInt8                                           bLength;
+        UInt8                                           bDescriptorType;
+        UInt8                                           bDevCapabilityType;
+        UInt8                                           iAdditionalInfoURL;
+        UInt8                                           bNumberOfAlternateModes;
+        UInt8                                           bPreferredAlternateMode;
+        UInt16                                          vCONNPower;
+        UInt8                                           bmConfigured[32];
+        UInt16                                          bcdVersion;
+        UInt8                                           bAdditionalFailureInfo;
+        UInt8                                           bReserved;
+        IOUSBDeviceCapabilityBillboardAltConfig         pAltConfigurations[];
+    };
+
+    typedef struct IOUSBDeviceCapabilityBillboard		IOUSBDeviceCapabilityBillboard;
+    typedef IOUSBDeviceCapabilityBillboard *			IOUSBDeviceCapabilityBillboardPtr;
+
+
 #pragma options align=reset
 	
 /*!
@@ -1134,17 +1171,19 @@
 	/*!
 	 @enum USBDeviceSpeed
 	 @discussion Returns the speed of a particular USB device. 
-	 @constant	kUSBDeviceSpeedLow	The device is a low speed device.
-	 @constant	kUSBDeviceSpeedFull	The device is a full speed device.
-	 @constant	kUSBDeviceSpeedHigh	The device is a high speed device.
-	 @constant	kUSBDeviceSpeedSuper  The device is a SuperSpeed device
+	 @constant	kUSBDeviceSpeedLow        The device is a low speed device.
+	 @constant	kUSBDeviceSpeedFull       The device is a full speed device.
+	 @constant	kUSBDeviceSpeedHigh       The device is a high speed device.
+	 @constant	kUSBDeviceSpeedSuper      The device is a SuperSpeed (Gen 1) 5Gbps device
+     @constant	kUSBDeviceSpeedSuperGen2  The device is a SuperSpeed Plus (Gen 2) 10Gbps device
 	 */
 enum {
-        kUSBDeviceSpeedLow		= 0,
-        kUSBDeviceSpeedFull		= 1,
-		kUSBDeviceSpeedHigh		= 2,
-		kUSBDeviceSpeedSuper	= 3
-        };
+        kUSBDeviceSpeedLow          = 0,
+        kUSBDeviceSpeedFull         = 1,
+		kUSBDeviceSpeedHigh         = 2,
+		kUSBDeviceSpeedSuper        = 3,
+        kUSBDeviceSpeedSuperPlus	= 4
+};
 
 /*!
     @enum MicrosecondsInFrame
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/usb/USBSpec.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/usb/USBSpec.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOKit.framework/Headers/usb/USBSpec.h	2015-11-11 08:28:57.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/usb/USBSpec.h	2016-06-07 01:22:45.000000000 +0200
@@ -21,7 +21,6 @@
  * @APPLE_LICENSE_HEADER_END@
  */
 
-
 /*
  * Constants that both OS9 and OSX want to define, and whose values are
  * specified by the USB Standard.
@@ -149,7 +148,8 @@
 		kUSBDeviceCapabilityWirelessUSB		= 1,
 		kUSBDeviceCapabilityUSB20Extension	= 2,
 		kUSBDeviceCapabilitySuperSpeedUSB	= 3,
-		kUSBDeviceCapabilityContainerID		= 4
+		kUSBDeviceCapabilityContainerID		= 4,
+        kUSBDeviceCapabilityBillboard       = 13
 };
 
     /*!
@@ -480,7 +480,41 @@
 		kUSBSuperSpeedSupportsHS	=	2,		// Value of wSpeedSupported indicating that the device supports high speed
 		kUSBSuperSpeedSupportsSS	=	3,		// Value of wSpeedSupported indicating that the device supports 5 Gbps
 	};
-		
+
+    /*!
+     @enum USB Device Billboard Capability Vconn Power constants
+     @discussion Power needed by the adapter for full functionality
+     */
+    enum {
+        kUSBBillboardVConn1Watt     =   0,
+        kUSBBillboardVConn1P5Watt   =   1,
+        kUSBBillboardVConn2Watt     =   2,
+        kUSBBillboardVConn3Watt     =   3,
+        kUSBBillboardVConn4Watt     =   4,
+        kUSBBillboardVConn5Watt     =   5,
+        kUSBBillboardVConn6Watt     =   6,
+        kUSBBillboardVConnReserved  =   7
+    };
+    /*!
+     @defineblock USB Billboard Capability Descriptor Constant
+     @define	kUSBBillboardVConnNoPowerReq	bit position for No Power Required, VConn b2:0 are ignored when this bit is set
+     */
+
+#define kUSBBillboardVConnNoPowerReq    15
+
+    /*! @/defineblock */
+
+    /*!
+     @enum USB Device Billboard Capability bmConfigured constants
+     @ A bit pair signifying the state of Alternate Modes
+     */
+    enum {
+        kUSBBillboardUnspecifiedError     =   0,
+        kUSBBillboardConfigNotAttempted   =   1,
+        kUSBBillboardConfigUnsuccessful   =   2,
+        kUSBBillboardAltModeConfigSuccess =   3
+    };
+
 	/*!
 	 @defineblock USB Descriptor and IORegistry constants
 	 @discussion 	Various constants used to describe the fields in the various USB Device Descriptors and IORegistry names used for some of those fields 

```