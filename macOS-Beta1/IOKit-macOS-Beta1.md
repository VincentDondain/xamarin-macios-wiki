#IOKit.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/graphics/IOGraphicsTypes.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/graphics/IOGraphicsTypes.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/graphics/IOGraphicsTypes.h	2016-10-08 04:23:33.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/graphics/IOGraphicsTypes.h	2016-10-24 00:21:33.000000000 +0200
@@ -282,7 +282,8 @@
     kIOWSAA_Transactional       = 0x10,  // If this bit is present, transition is to/from transactional operation model.
     // These attributes are internal
     kIOWSAA_DeferStart          = 0x100,
-    kIOWSAA_DeferEnd            = 0x200
+    kIOWSAA_DeferEnd            = 0x200,
+    kIOWSAA_Reserved            = 0xF0000000
 };
 
 // values for kIOMirrorAttribute
@@ -1327,6 +1328,8 @@
 #define kIODisplayMinValueKey           "min"
 #define kIODisplayMaxValueKey           "max"
 
+#define kIODisplayBrightnessProbeKey        "brightness-probe"
+#define kIODisplayLinearBrightnessProbeKey  "linear-brightness-probe"
 #define kIODisplayBrightnessKey             "brightness"
 #define kIODisplayLinearBrightnessKey       "linear-brightness"
 #define kIODisplayUsableLinearBrightnessKey "usable-linear-brightness"
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDManager.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDManager.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDManager.h	2016-09-28 04:25:53.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDManager.h	2016-10-22 03:00:41.000000000 +0200
@@ -260,7 +260,7 @@
 CF_EXPORT
 void IOHIDManagerRegisterDeviceMatchingCallback(
                                 IOHIDManagerRef                 manager,
-                                IOHIDDeviceCallback             callback,
+                                IOHIDDeviceCallback _Nullable   callback,
                                 void * _Nullable                context)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
@@ -276,7 +276,7 @@
 CF_EXPORT
 void IOHIDManagerRegisterDeviceRemovalCallback(
                                 IOHIDManagerRef                 manager,
-                                IOHIDDeviceCallback             callback,
+                                IOHIDDeviceCallback _Nullable   callback,
                                 void * _Nullable                context)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
@@ -290,9 +290,9 @@
 */
 CF_EXPORT
 void IOHIDManagerRegisterInputReportCallback( 
-                                    IOHIDManagerRef             manager,
-                                    IOHIDReportCallback         callback,
-                                    void * _Nullable            context)
+                                IOHIDManagerRef                 manager,
+                                IOHIDReportCallback _Nullable   callback,
+                                void * _Nullable                context)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
                                                                     
 /*! @function   IOHIDManagerRegisterInputValueCallback
@@ -308,7 +308,7 @@
 CF_EXPORT
 void IOHIDManagerRegisterInputValueCallback( 
                                 IOHIDManagerRef                 manager,
-                                IOHIDValueCallback              callback,
+                                IOHIDValueCallback _Nullable    callback,
                                 void * _Nullable                context)
 AVAILABLE_MAC_OS_X_VERSION_10_5_AND_LATER;
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/scsi/SCSICmds_INQUIRY_Definitions.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/scsi/SCSICmds_INQUIRY_Definitions.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/scsi/SCSICmds_INQUIRY_Definitions.h	2016-09-30 04:04:47.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/scsi/SCSICmds_INQUIRY_Definitions.h	2016-10-24 00:50:50.000000000 +0200
@@ -630,6 +630,7 @@
 */
 #define kIOPropertySCSIProductRevisionLevel			"Product Revision Level"
 
+#ifndef __OPEN_SOURCE__
 
 /*!
 @enum INQUIRY Page Codes
@@ -649,6 +650,10 @@
 Page Code B1h.
 @constant kINQUIRY_PageB2_PageCode
 Page Code B2h.
+@constant kINQUIRY_PageC0_PageCode
+Page Code C0h.
+@constant kINQUIRY_PageC1_PageCode
+Page Code C1h.
 */
 enum
 {
@@ -658,8 +663,44 @@
 	kINQUIRY_Page89_PageCode				= 0x89,
 	kINQUIRY_PageB0_PageCode				= 0xB0,
 	kINQUIRY_PageB1_PageCode				= 0xB1,
-	kINQUIRY_PageB2_PageCode				= 0xB2
-};	
+	kINQUIRY_PageB2_PageCode				= 0xB2,
+	kINQUIRY_PageC0_PageCode				= 0xC0,
+	kINQUIRY_PageC1_PageCode				= 0xC1
+};
+
+#else
+
+/*!
+ @enum INQUIRY Page Codes
+ @discussion INQUIRY Page Codes to be used when EVPD is set in the
+ INQUIRY command.
+ @constant kINQUIRY_Page00_PageCode
+ Page Code 00h.
+ @constant kINQUIRY_Page80_PageCode
+ Page Code 80h.
+ @constant kINQUIRY_Page83_PageCode
+ Page Code 83h.
+ @constant kINQUIRY_Page89_PageCode
+ Page Code 89h.
+ @constant kINQUIRY_PageB0_PageCode
+ Page Code B0h.
+ @constant kINQUIRY_PageB1_PageCode
+ Page Code B1h.
+ @constant kINQUIRY_PageB2_PageCode
+ Page Code B2h.
+ */
+enum
+{
+    kINQUIRY_Page00_PageCode				= 0x00,
+    kINQUIRY_Page80_PageCode				= 0x80,
+    kINQUIRY_Page83_PageCode				= 0x83,
+    kINQUIRY_Page89_PageCode				= 0x89,
+    kINQUIRY_PageB0_PageCode				= 0xB0,
+    kINQUIRY_PageB1_PageCode				= 0xB1,
+    kINQUIRY_PageB2_PageCode				= 0xB2,
+};
+
+#endif /* __OPEN_SOURCE__ */
 
 
 /*!
@@ -1090,6 +1131,74 @@
 
 #pragma pack(pop)
 
+#ifndef __OPEN_SOURCE__
+
+#pragma pack(push, 1)
+
+enum
+{
+	kC0DataMaxStringLen = 32,
+};
+
+typedef struct  SCSICmd_INQUIRY_PageCx_Header
+{
+
+	UInt8		PERIPHERAL_DEVICE_TYPE; 	// 7-5 = Qualifier. 4-0 = Device type.
+	UInt8		PAGE_CODE;					// Must be equal to C0h or C1h
+	UInt8		RESERVED;
+	UInt8		PAGE_LENGTH;
+
+} SCSICmd_INQUIRY_PAGECx_Header;
+
+/*!
+ @struct SCSICmd_INQUIRY_PageC0_Data
+ @discussion INQUIRY Page C0h data as defined in Apple Target
+ Disk Mode specification. This is a vendor specific data structure.
+ This section contains all structures and definitions used by 
+ the INQUIRY command in response to a request for page C0h.
+ */
+
+typedef struct SCSICmd_INQUIRY_PageC0_Data
+{
+
+	SCSICmd_INQUIRY_PAGECx_Header	fHeader;
+	UInt8							fTdmPageVersion;
+	UInt8							fTdmProtocolVersion;
+	UInt8							fReserved1;
+	UInt8							fReserved2;
+	UInt8							fMacModelId[kC0DataMaxStringLen];
+	UInt8							fSerialNumber[kC0DataMaxStringLen];
+	UInt32							fMaxReadSize;
+	UInt32							fMaxWriteSize;
+	UInt32							fNativeBlockSize;
+	UInt64							fFeatures;
+	UInt64							fWorkArounds;
+
+} SCSICmd_INQUIRY_PageC0_Data;
+
+/*!
+ @struct SCSICmd_INQUIRY_PageC1_Data
+ @discussion INQUIRY Page C1h data as defined in Apple Target
+ Disk Mode specification. This is a vendor specific data structure.
+ This section contains all structures and definitions used by
+ the INQUIRY command in response to a request for page C1h.
+ */
+
+typedef struct SCSICmd_INQUIRY_PageC1_Data
+{
+
+	SCSICmd_INQUIRY_PAGECx_Header	fHeader;
+	UInt8							fTdmPowerRequirementsPageVersion;
+	UInt8							fReserved1;
+	UInt16							fReserved2;
+	UInt32							fPowerRequired;
+
+} SCSICmd_INQUIRY_PageC1_Data;
+
+#pragma pack(pop)
+
+#endif /* __OPEN_SOURCE__ */
+
 /*!
 @define kIOPropertySATVendorIdentification
 Vendor Identification of the SATL.

```