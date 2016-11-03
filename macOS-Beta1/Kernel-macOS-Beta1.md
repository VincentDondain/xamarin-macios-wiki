#Kernel.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOWorkLoop.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOWorkLoop.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOWorkLoop.h	2016-09-30 03:22:00.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOWorkLoop.h	2016-10-23 23:48:33.000000000 +0200
@@ -143,9 +143,6 @@
     struct ExpansionData {
 	IOOptionBits options;
 	IOEventSource *passiveEventChain;
-#if DEBUG
-	void * allocationBacktrace[16];
-#endif /* DEBUG */
 #if IOKITSTATS
 	struct IOWorkLoopCounter *counter;
 #else
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/bluetooth/BluetoothAssignedNumbers.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/bluetooth/BluetoothAssignedNumbers.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/bluetooth/BluetoothAssignedNumbers.h	2016-10-08 04:49:44.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/bluetooth/BluetoothAssignedNumbers.h	2016-10-24 00:26:16.000000000 +0200
@@ -659,7 +659,7 @@
 
 // HCI Versions
 
-enum BluetoothHCIVersions
+typedef enum BluetoothHCIVersions
 {
 	kBluetoothHCIVersionCoreSpecification1_0b												=	0x00,
 	kBluetoothHCIVersionCoreSpecification1_1												=	0x01,
@@ -670,12 +670,12 @@
 	kBluetoothHCIVersionCoreSpecification4_0												=	0x06,
     kBluetoothHCIVersionCoreSpecification4_1												=	0x07,
     kBluetoothHCIVersionCoreSpecification4_2												=	0x08
-};
+} BluetoothHCIVersions;
 
 
 // LMP Versions
 
-enum BluetoothLMPVersions
+typedef enum BluetoothLMPVersions
 {
 	kBluetoothLMPVersionCoreSpecification1_0b												=	0x00,
 	kBluetoothLMPVersionCoreSpecification1_1												=	0x01,
@@ -686,7 +686,7 @@
 	kBluetoothLMPVersionCoreSpecification4_0												=	0x06,
 	kBluetoothLMPVersionCoreSpecification4_1												=	0x07,
     kBluetoothLMPVersionCoreSpecification4_2												=	0x08
-};
+} BluetoothLMPVersions;
 
 #ifdef	__cplusplus
 	}
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IODisplay.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IODisplay.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IODisplay.h	2016-10-08 04:23:33.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IODisplay.h	2016-10-24 00:21:33.000000000 +0200
@@ -33,6 +33,8 @@
 extern const OSSymbol * gIODisplayMinValueKey;
 extern const OSSymbol * gIODisplayMaxValueKey;
 
+extern const OSSymbol * gIODisplayBrightnessProbeKey;
+extern const OSSymbol * gIODisplayLinearBrightnessProbeKey;
 extern const OSSymbol * gIODisplayContrastKey;
 extern const OSSymbol * gIODisplayBrightnessKey;
 extern const OSSymbol * gIODisplayLinearBrightnessKey;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IOGraphicsTypes.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IOGraphicsTypes.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IOGraphicsTypes.h	2016-10-08 04:23:33.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IOGraphicsTypes.h	2016-10-24 00:21:33.000000000 +0200
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
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDEventService.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDEventService.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDEventService.h	2016-10-06 05:59:49.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDEventService.h	2016-10-24 00:28:50.000000000 +0200
@@ -70,13 +70,6 @@
     kHIDDispatchOptionKeyboardNoRepeat                  = (1<<0)
 };
 
-enum
-{
-    kHIDShutdownDebugModeStackshots = 1,
-    kHIDShutdownDebugModePanic,
-    kHIDShutdownDebugModeDisabled
-};
-
 
 class IOHIDEventService;
 class   IOHIDPointing;
@@ -152,10 +145,6 @@
                 IOTimerEventSource *    nmiTimer;
                 UInt32                  stackshotHeld;
                 IOTimerEventSource *    stackshotTimer;
-                UInt32                  shutdownDebugMode;
-                UInt32                  shutdownDebugKeyMask;
-                UInt32                  shutdownDebugDelay;
-                IOTimerEventSource *    shutdownDebugTimer;
             } debug;
             bool                    swapISO;
 #else
@@ -226,12 +215,6 @@
     void                    debuggerTimerCallback(IOTimerEventSource *sender);
 
     void                    stackshotTimerCallback(IOTimerEventSource *sender);
-
-#if TARGET_OS_IPHONE
-    void                    forcedShutdownDebugTimerCallback(IOTimerEventSource *sender);
-    void                    forcedShutdownDebugInit();
-  
-#endif
 #endif
     
     void                    multiAxisTimerCallback(IOTimerEventSource *sender);
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDUtility.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDUtility.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDUtility.h	2016-10-06 05:59:49.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDUtility.h	2016-10-24 00:28:50.000000000 +0200
@@ -67,6 +67,14 @@
       }
       return result;
     }
+    bool isTopRow () const {
+        bool result = false;
+        if ((usagePage() == kHIDPage_KeyboardOrKeypad) &&
+            (((usage() >= kHIDUsage_Keyboard1) && (usage() <= kHIDUsage_Keyboard0)) || (usage() == kHIDUsage_KeyboardHyphen) || (usage() == kHIDUsage_KeyboardDeleteOrBackspace))) {
+            result = true;
+        }
+        return result;
+    }
 };
 
 struct KeyAttribute {
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/scsi/SCSICmds_INQUIRY_Definitions.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/scsi/SCSICmds_INQUIRY_Definitions.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/scsi/SCSICmds_INQUIRY_Definitions.h	2016-09-30 04:04:47.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/scsi/SCSICmds_INQUIRY_Definitions.h	2016-10-24 00:50:50.000000000 +0200
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
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/c++/OSData.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/c++/OSData.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/c++/OSData.h	2016-09-30 03:21:47.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/c++/OSData.h	2016-10-23 23:48:22.000000000 +0200
@@ -734,6 +734,7 @@
 private:
     virtual void setDeallocFunction(DeallocFunction func);
     OSMetaClassDeclareReservedUsed(OSData, 0);
+    bool isSerializable(void);
 
 private:
     OSMetaClassDeclareReservedUnused(OSData, 1);
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/mach_time.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/mach_time.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/mach_time.h	2016-09-30 03:22:05.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/mach_time.h	2016-10-23 23:48:40.000000000 +0200
@@ -51,17 +51,13 @@
 /*
  * like mach_absolute_time, but advances during sleep
  */
-__OSX_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0)
-__TVOS_AVAILABLE(__TVOS_10_0)
-__WATCHOS_AVAILABLE(__WATCHOS_3_0)
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0)
 uint64_t			mach_continuous_time(void);
 
 /*
  * like mach_approximate_time, but advances during sleep
  */
-__OSX_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0)
-__TVOS_AVAILABLE(__TVOS_10_0)
-__WATCHOS_AVAILABLE(__WATCHOS_3_0)
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0)
 uint64_t			mach_continuous_approximate_time(void);
 
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/vm_statistics.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/vm_statistics.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/vm_statistics.h	2016-09-30 03:22:08.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/vm_statistics.h	2016-10-23 23:48:44.000000000 +0200
@@ -436,8 +436,6 @@
 /* DHMM data */
 #define VM_MEMORY_DHMM 84
 
-/* memory needed for DFR related actions */
-#define VM_MEMORY_DFR 85
 
 /* memory allocated by SceneKit.framework */
 #define VM_MEMORY_SCENEKIT 86
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_policy.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_policy.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_policy.h	2016-09-30 03:21:46.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_policy.h	2016-10-23 23:48:22.000000000 +0200
@@ -6589,7 +6589,7 @@
 struct mac_policy_conf {
 	const char		*mpc_name;		/** policy name */
 	const char		*mpc_fullname;		/** full name */
-	const char		**mpc_labelnames;	/** managed label namespaces */
+	char const * const *mpc_labelnames;	/** managed label namespaces */
 	unsigned int		 mpc_labelname_count;	/** number of managed label namespaces */
 	struct mac_policy_ops	*mpc_ops;		/** operation vector */
 	int			 mpc_loadtime_flags;	/** load time flags */
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h	2016-09-30 03:22:38.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h	2016-10-23 23:49:17.000000000 +0200
@@ -559,6 +559,7 @@
 #define DKIO_NOCACHE	0x80
 #define DKIO_TIER_MASK	0xF00
 #define DKIO_TIER_SHIFT	8
+#define DKIO_TIER_UPGRADE 0x1000
 
 /* Kernel Debug Sub Classes for Applications (DBG_APPS) */
 #define DBG_APP_LOGINWINDOW     0x03
```