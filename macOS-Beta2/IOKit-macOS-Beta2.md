#IOKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/IOKitKeys.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/IOKitKeys.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/IOKitKeys.h	2016-06-03 22:55:03.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/IOKitKeys.h	2016-06-29 00:56:02.000000000 +0200
@@ -133,6 +133,7 @@
 #define kIOMaximumSegmentByteCountWriteKey      "IOMaximumSegmentByteCountWrite"      // (OSNumber)
 #define kIOMinimumSegmentAlignmentByteCountKey  "IOMinimumSegmentAlignmentByteCount"  // (OSNumber)
 #define kIOMaximumSegmentAddressableBitCountKey "IOMaximumSegmentAddressableBitCount" // (OSNumber)
+#define kIOMinimumSaturationByteCountKey        "IOMinimumSaturationByteCount"        // (OSNumber)
 
 // properties found in services that wish to describe an icon
 //
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/graphics/IOGraphicsTypes.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/graphics/IOGraphicsTypes.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/graphics/IOGraphicsTypes.h	2016-06-03 23:08:18.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/graphics/IOGraphicsTypes.h	2016-06-29 01:09:10.000000000 +0200
@@ -31,7 +31,7 @@
 extern "C" {
 #endif
 
-#define IOGRAPHICSTYPES_REV     43
+#define IOGRAPHICSTYPES_REV     44
 
 typedef SInt32  IOIndex;
 typedef UInt32  IOSelect;
@@ -279,7 +279,10 @@
     kIOWSAA_Sleep               = 4,
     kIOWSAA_Hibernate           = kIOWSAA_Sleep,
     kIOWSAA_DriverOpen          = 5,    // Reserved
-    kIOWSAA_Transactional       = 0x10  // If this bit is present, transition is to/from transactional operation model.
+    kIOWSAA_Transactional       = 0x10,  // If this bit is present, transition is to/from transactional operation model.
+    // These attributes are internal
+    kIOWSAA_DeferStart          = 0x100,
+    kIOWSAA_DeferEnd            = 0x200
 };
 
 // values for kIOMirrorAttribute
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDKeys.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDKeys.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDKeys.h	2016-06-03 23:10:18.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDKeys.h	2016-06-29 01:11:16.000000000 +0200
@@ -420,11 +420,14 @@
  @defined Press count tracking keys
  @abstract Keys used to set the parameters for press count tracking
  @discussion CFBoolean value for kIOHIDKeyboardPressCountTrackingEnabledKey is used to turn on the feature or turn it off
+    CFArray value for kIOHIDKeyboardPressCountUsagePairsKey stores 32bit CFNumbers (UsagePage<<16)|Usage designating the keyboard events to process
+    If kIOHIDKeyboardPressCountUsagePairsKey is not set, all keyboard events will be processed
     kIOHIDKeyboardPressCountTriplePressTimeoutKey and kIOHIDKeybaordPressCountDoublePressTimeoutKey take CFNumberRef values
     The numbers represent the timeout values for determining the value kIOHIDEventFieldKeyboardPressCount
     kIOHIDKeyboardLongPressTimeoutKey value is used to determine the timeout for long presses
  */
 #define kIOHIDKeyboardPressCountTrackingEnabledKey      "PressCountTrackingEnabled"
+#define kIOHIDKeyboardPressCountUsagePairsKey           "PressCountUsagePairs"
 #define kIOHIDKeyboardPressCountTriplePressTimeoutKey   "PressCountTriplePressTimeout"
 #define kIOHIDKeyboardPressCountDoublePressTimeoutKey   "PressCountDoublePressTimeout"
 #define kIOHIDKeyboardLongPressTimeoutKey               "LongPressTimeout"
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/scsi/IOSCSIMultimediaCommandsDevice.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/scsi/IOSCSIMultimediaCommandsDevice.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/scsi/IOSCSIMultimediaCommandsDevice.h	2016-05-04 00:21:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/scsi/IOSCSIMultimediaCommandsDevice.h	2016-06-29 01:17:11.000000000 +0200
@@ -433,7 +433,7 @@
 												  const DVDKeyClass keyClass,
 												  const UInt32 lba,
 												  const UInt8 agid,
-												  const DVDKeyFormat keyFormat );
+												  const DVDKeyFormat keyFormat ) __attribute__ ((deprecated));
 												  
 	virtual IOReturn		SendKey				( IOMemoryDescriptor * buffer,
 												  const DVDKeyClass keyClass,
@@ -768,6 +768,17 @@
 								SCSICmdField2Byte 			ALLOCATION_LENGTH,
 								SCSICmdField2Bit 			AGID,
 								SCSICmdField6Bit 			KEY_FORMAT,
+								SCSICmdField1Byte 			CONTROL					) __attribute__ ((deprecated));
+
+
+	bool		REPORT_KEY_V3 (	SCSITaskIdentifier			request,
+								IOMemoryDescriptor *		dataBuffer,
+								SCSICmdField4Byte			LOGICAL_BLOCK_ADDRESS,
+								SCSICmdField1Byte			KEY_CLASS,
+								SCSICmdField2Byte 			ALLOCATION_LENGTH,
+								SCSICmdField1Byte			BLOCK_COUNT,
+								SCSICmdField2Bit 			AGID,
+								SCSICmdField6Bit 			KEY_FORMAT,
 								SCSICmdField1Byte 			CONTROL					);
 	
 	
@@ -793,10 +804,17 @@
 	
 	IOReturn	RequestIdle ( void );
 	
+	/* 10.12.0 */
+	virtual IOReturn		ReportKey			( IOMemoryDescriptor * buffer,
+												  const DVDKeyClass keyClass,
+												  const UInt32 lba,
+												  const UInt8 blockCount,
+												  const UInt8 agid,
+												  const DVDKeyFormat keyFormat );
+
 private:
 	
 	// Space reserved for future expansion.
-    OSMetaClassDeclareReservedUnused ( IOSCSIMultimediaCommandsDevice, 	8 );
     OSMetaClassDeclareReservedUnused ( IOSCSIMultimediaCommandsDevice, 	9 );
     OSMetaClassDeclareReservedUnused ( IOSCSIMultimediaCommandsDevice, 10 );
     OSMetaClassDeclareReservedUnused ( IOSCSIMultimediaCommandsDevice, 11 );
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/storage/IOBDMediaBSDClient.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/storage/IOBDMediaBSDClient.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/storage/IOBDMediaBSDClient.h	2016-06-03 23:12:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/storage/IOBDMediaBSDClient.h	2016-06-29 01:14:19.000000000 +0200
@@ -68,8 +68,9 @@
 {
     uint8_t  format;
     uint8_t  keyClass;
+    uint8_t  blockCount;
 
-    uint8_t  reserved0016[2];                      /* reserved, clear to zero */
+    uint8_t  reserved0024[1];                         /* reserved, clear to zero */
 
     uint32_t address;
     uint8_t  grantID;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/storage/IODVDMediaBSDClient.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/storage/IODVDMediaBSDClient.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/storage/IODVDMediaBSDClient.h	2016-05-04 00:21:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/storage/IODVDMediaBSDClient.h	2016-06-29 01:12:11.000000000 +0200
@@ -69,8 +69,9 @@
 {
     uint8_t  format;
     uint8_t  keyClass;
+    uint8_t  blockCount;
 
-    uint8_t  reserved0016[2];                      /* reserved, clear to zero */
+    uint8_t  reserved0024[1];                      /* reserved, clear to zero */
 
     uint32_t address;
     uint8_t  grantID;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/usb/USB.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/usb/USB.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/usb/USB.h	2016-06-07 01:22:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/usb/USB.h	2016-06-29 01:16:54.000000000 +0200
@@ -377,7 +377,7 @@
 @discussion  Errors specific to the IOUSBFamily.  Note that the iokit_usb_err(x) translates to 0xe0004xxx, where xxx is the value in parenthesis as a hex number.
 */
 
-#define	iokit_usb_err(return)								(sys_iokit|sub_iokit_usb|return)
+#define	iokit_usb_err(return)								(IOReturn)(sys_iokit|sub_iokit_usb|return)
 #define kIOUSBUnknownPipeErr								iokit_usb_err(0x61)									// 0xe0004061  Pipe ref not recognized
 #define kIOUSBTooManyPipesErr								iokit_usb_err(0x60)									// 0xe0004060  Too many pipes
 #define kIOUSBNoAsyncPortErr								iokit_usb_err(0x5f)									// 0xe000405f  no async port
@@ -462,11 +462,12 @@
 #define kIOUSBMessageDeviceCountExceeded			iokit_usb_msg(0x1a)		// 0xe000401a  Message sent by a hub when a device cannot be enumerated because the USB controller ran out of resources
 #define kIOUSBMessageHubPortDeviceDisconnected      iokit_usb_msg(0x1b)		// 0xe000401b  Message sent by a built-in hub when a device was disconnected
 #define kIOUSBMessageUnsupportedConfiguration		iokit_usb_msg(0x1c)     // 0xe000401c  Message sent to the clients of the device when a device is not supported in the current configuration.  The message argument contains the locationID of the device
-#define kIOUSBMessageHubCountExceeded               iokit_usb_err(0x1d)     // 0xe000401d  Message sent when a 6th hub was plugged in and was not enumerated, as the USB spec only support 5 hubs in a chain
-#define kIOUSBMessageTDMLowBattery                  iokit_usb_err(0x1e)     // 0xe000401e  Message sent when when an attached TDM system battery is running low.
-#define kIOUSBMessageLegacySuspendDevice            iokit_usb_err(0x1f)     // 0xe000401f  Message sent to legacy interfaces when SuspedDevice() is called .
-#define kIOUSBMessageLegacyResetDevice              iokit_usb_err(0x20)     // 0xe0004020  Message sent to legacy interfaces when ResetDevice() is called .
-#define kIOUSBMessageLegacyReEnumerateDevice        iokit_usb_err(0x21)     // 0xe0004021  Message sent to legacy interfaces when ReEnumerateDevice() is called .
+#define kIOUSBMessageHubCountExceeded               iokit_usb_msg(0x1d)     // 0xe000401d  Message sent when a 6th hub was plugged in and was not enumerated, as the USB spec only support 5 hubs in a chain
+#define kIOUSBMessageTDMLowBattery                  iokit_usb_msg(0x1e)     // 0xe000401e  Message sent when when an attached TDM system battery is running low.
+#define kIOUSBMessageLegacySuspendDevice            iokit_usb_msg(0x1f)     // 0xe000401f  Message sent to legacy interfaces when SuspedDevice() is called .
+#define kIOUSBMessageLegacyResetDevice              iokit_usb_msg(0x20)     // 0xe0004020  Message sent to legacy interfaces when ResetDevice() is called .
+#define kIOUSBMessageLegacyReEnumerateDevice        iokit_usb_msg(0x21)     // 0xe0004021  Message sent to legacy interfaces when ReEnumerateDevice() is called .
+#define kIOUSBMessageConfigurationSet               iokit_usb_msg(0x22)     // 0xe0004022  Message sent upon a SetConfiguration call 
     
 /*! @/defineblock */
 

```