#Kernel.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IORegistryEntry.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IORegistryEntry.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IORegistryEntry.h	2016-06-29 00:56:09.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IORegistryEntry.h	2016-07-10 08:21:58.000000000 +0200
@@ -180,7 +180,7 @@
 
 private:
 #if __LP64__
-#if !CONFIG_EMBEDDED
+#if __x86_64__
     virtual OSArray * getChildSetReferenceWithOptions( const IORegistryPlane * plane, IOOptionBits options = 0 ) const;
     OSMetaClassDeclareReservedUsed(IORegistryEntry, 0);
 #else
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IOFramebuffer.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IOFramebuffer.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IOFramebuffer.h	2016-06-29 01:09:10.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IOFramebuffer.h	2016-07-10 08:40:09.000000000 +0200
@@ -29,6 +29,10 @@
 #include <IOKit/graphics/IOFramebufferShared.h>
 #include <IOKit/IOLib.h>
 
+
+#define IOFRAMEBUFFER_REV           2
+
+
 class IOFramebuffer;
 class IOBufferMemoryDescriptor;
 
@@ -135,6 +139,9 @@
 
     kIOFBNotifyWillNotify       = 80,
     kIOFBNotifyDidNotify        = 81,
+
+    kIOFBNotifyWSAAEnterDefer   = 90,
+    kIOFBNotifyWSAAExitDefer    = 91,
 };
 
 struct IOFramebufferNotificationNotify
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDUsageTables.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDUsageTables.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDUsageTables.h	2016-06-29 01:11:16.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDUsageTables.h	2016-07-10 08:58:23.000000000 +0200
@@ -94,7 +94,9 @@
     kHIDUsage_GD_Keyboard    = 0x06,    /* Application Collection */
     kHIDUsage_GD_Keypad    = 0x07,    /* Application Collection */
     kHIDUsage_GD_MultiAxisController    = 0x08,    /* Application Collection */
-    /* 0x09 - 0x2F Reserved */
+    kHIDUsage_GD_TabletPCSystemControls    = 0x09,    /* Application Collection */
+    kHIDUsage_GD_AssistiveControl    = 0x0A,    /* Application Collection */
+    /* 0x0B - 0x2F Reserved */
     kHIDUsage_GD_X    = 0x30,    /* Dynamic Value */
     kHIDUsage_GD_Y    = 0x31,    /* Dynamic Value */
     kHIDUsage_GD_Z    = 0x32,    /* Dynamic Value */
@@ -301,6 +303,7 @@
     kHIDUsage_Game_GunSafety    = 0x36,    /* On/Off Control */
     kHIDUsage_Game_GamepadFireOrJump    = 0x37,    /* Logical Collection */
     kHIDUsage_Game_GamepadTrigger    = 0x39,    /* Logical Collection */
+    kHIDUsage_Game_GamepadFormFitting    = 0x39,    /* Static Flag */
     /* 0x3A - 0xFFFF Reserved */
     kHIDUsage_Game_Reserved = 0xFFFF
 };
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDEventDriver.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDEventDriver.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDEventDriver.h	2016-06-29 01:11:16.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDEventDriver.h	2016-07-10 08:58:23.000000000 +0200
@@ -51,6 +51,7 @@
         
     UInt32                      _bootSupport;
     bool                        _multipleReports;
+    bool                        _authenticatedDevice;
     bool                        _reservedBool   __unused;
     UInt32                      _reservedUInt32 __unused;
     bool                        _reservedBool1  __unused;
@@ -83,6 +84,7 @@
             OSArray *           transducers;
             IOHIDElement *      touchCancelElement;
             bool                native;
+            bool                collectionDispatch;
         } digitizer;
         
         struct {
@@ -104,6 +106,7 @@
         
         struct {
             bool                extended;
+            bool                formFitting;
             OSArray *           elements;
             UInt32              capable;
             UInt32              sendingReportID;
@@ -137,7 +140,7 @@
             } shoulder;
 
         } gameController;
-        
+        UInt64  lastReportTime;
     };
     ExpansionData *             _reserved;
     
@@ -179,6 +182,7 @@
     void                    handleRelativeReport(AbsoluteTime timeStamp, UInt32 reportID);
     void                    handleGameControllerReport(AbsoluteTime timeStamp, UInt32 reportID);
     void                    handleMultiAxisPointerReport(AbsoluteTime timeStamp, UInt32 reportID);
+    void                    handleDigitizerCollectionReport(AbsoluteTime timeStamp, UInt32 reportID);
     void                    handleDigitizerReport(AbsoluteTime timeStamp, UInt32 reportID);
     IOHIDEvent*             handleDigitizerTransducerReport(DigitizerTransducer * transducer, AbsoluteTime timeStamp, UInt32 reportID);
     void                    handleScrollReport(AbsoluteTime timeStamp, UInt32 reportID);
@@ -189,6 +193,9 @@
     IOHIDEvent *            handleUnicodeGestureCandidateReport(EventElementCollection * candidate, AbsoluteTime timeStamp, UInt32 reportID);
     
     bool                    serializeCharacterGestureState(void * ref, OSSerialize * serializer);
+    bool                    conformTo (UInt32 usagePage, UInt32 usage);
+    IOHIDEvent*             createDigitizerTransducerEventForReport(DigitizerTransducer * transducer, AbsoluteTime timeStamp, UInt32 reportID);
+    bool                    serializeDebugState(void * ref, OSSerialize * serializer);
 
 protected:
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDParameter.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDParameter.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDParameter.h	2016-06-29 01:11:16.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDParameter.h	2016-07-10 08:58:23.000000000 +0200
@@ -335,7 +335,6 @@
     kIOHIDNumLockState              = 0x00000002,
     kIOHIDActivityUserIdle          = 0x00000003,
     kIOHIDActivityDisplayOn         = 0x00000004,
-    kIOHIDModifierFlags             = 0x00000005
 };
 
 #endif /* !_DEV_EVSIO_H */
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDUsageTables.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDUsageTables.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDUsageTables.h	2016-06-29 01:11:16.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDUsageTables.h	2016-07-10 08:58:23.000000000 +0200
@@ -94,7 +94,9 @@
     kHIDUsage_GD_Keyboard    = 0x06,    /* Application Collection */
     kHIDUsage_GD_Keypad    = 0x07,    /* Application Collection */
     kHIDUsage_GD_MultiAxisController    = 0x08,    /* Application Collection */
-    /* 0x09 - 0x2F Reserved */
+    kHIDUsage_GD_TabletPCSystemControls    = 0x09,    /* Application Collection */
+    kHIDUsage_GD_AssistiveControl    = 0x0A,    /* Application Collection */
+    /* 0x0B - 0x2F Reserved */
     kHIDUsage_GD_X    = 0x30,    /* Dynamic Value */
     kHIDUsage_GD_Y    = 0x31,    /* Dynamic Value */
     kHIDUsage_GD_Z    = 0x32,    /* Dynamic Value */
@@ -301,6 +303,7 @@
     kHIDUsage_Game_GunSafety    = 0x36,    /* On/Off Control */
     kHIDUsage_Game_GamepadFireOrJump    = 0x37,    /* Logical Collection */
     kHIDUsage_Game_GamepadTrigger    = 0x39,    /* Logical Collection */
+    kHIDUsage_Game_GamepadFormFitting    = 0x39,    /* Static Flag */
     /* 0x3A - 0xFFFF Reserved */
     kHIDUsage_Game_Reserved = 0xFFFF
 };
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IOBlockStorageDevice.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IOBlockStorageDevice.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IOBlockStorageDevice.h	2016-06-29 01:06:11.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IOBlockStorageDevice.h	2016-07-10 08:34:24.000000000 +0200
@@ -222,9 +222,9 @@
     virtual UInt32	doGetFormatCapacities(UInt64 * capacities,
                                             UInt32   capacitiesMaxCount) const	= 0;
 
-#ifdef __x86_64__
+#if TARGET_OS_OSX && defined(__x86_64__)
     virtual IOReturn	doLockUnlockMedia(bool doLock) __attribute__ ((deprecated));
-#endif /* __x86_64__ */
+#endif /* TARGET_OS_OSX && defined(__x86_64__) */
 
     virtual IOReturn	doSynchronizeCache(void) __attribute__ ((deprecated));
 
@@ -285,9 +285,9 @@
      */
     virtual IOReturn	reportEjectability(bool *isEjectable)	= 0;
 
-#ifdef __x86_64__
+#if TARGET_OS_OSX && defined(__x86_64__)
     virtual IOReturn	reportLockability(bool *isLockable) __attribute__ ((deprecated));
-#endif /* __x86_64__ */
+#endif /* TARGET_OS_OSX && defined(__x86_64__) */
 
     /*!
      * @function reportMaxValidBlock
@@ -316,10 +316,10 @@
      */
     virtual IOReturn	reportMediaState(bool *mediaPresent,bool *changedState = 0)	= 0;
     
-#ifdef __x86_64__
+#if TARGET_OS_OSX && defined(__x86_64__)
     virtual IOReturn	reportPollRequirements(bool *pollRequired,
                                             bool *pollIsExpensive) __attribute__ ((deprecated));
-#endif /* __x86_64__ */
+#endif /* TARGET_OS_OSX && defined(__x86_64__) */
     
     /*!
      * @function reportRemovability
@@ -404,9 +404,9 @@
      */
     virtual IOReturn	requestIdle(void);
 
-#ifdef __x86_64__
+#if TARGET_OS_OSX && defined(__x86_64__)
     virtual IOReturn doDiscard(UInt64 block, UInt64 nblks) __attribute__ ((deprecated));
-#endif /* __x86_64__ */
+#endif /* TARGET_OS_OSX && defined(__x86_64__) */
 
     /*!
      * @function doUnmap
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IOBlockStorageDriver.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IOBlockStorageDriver.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IOBlockStorageDriver.h	2016-06-29 01:06:11.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IOBlockStorageDriver.h	2016-07-10 08:34:24.000000000 +0200
@@ -679,11 +679,11 @@
 
     virtual bool handleStart(IOService * provider);
 
-#ifdef __x86_64__
+#if TARGET_OS_OSX && defined(__x86_64__)
     virtual bool handleYield(IOService *  provider,
                              IOOptionBits options  = 0,
                              void *       argument = 0) __attribute__ ((deprecated));
-#endif /* __x86_64__ */
+#endif /* TARGET_OS_OSX && defined(__x86_64__) */
 
     /*!
      * @function getMediaBlockSize
@@ -729,11 +729,11 @@
                               IOOptionBits options,
                               bool *       defer) APPLE_KEXT_OVERRIDE;
 
-#ifdef __x86_64__
+#if TARGET_OS_OSX && defined(__x86_64__)
     virtual bool yield(IOService *  provider,
                        IOOptionBits options  = 0,
                        void *       argument = 0) __attribute__ ((deprecated));
-#endif /* __x86_64__ */
+#endif /* TARGET_OS_OSX && defined(__x86_64__) */
 
     /*!
      * @function read
@@ -974,11 +974,11 @@
 
     virtual IOReturn formatMedia(UInt64 byteCapacity);
 
-#ifdef __x86_64__
+#if TARGET_OS_OSX && defined(__x86_64__)
     virtual IOReturn lockMedia(bool lock) __attribute__ ((deprecated));
 
     virtual IOReturn pollMedia() __attribute__ ((deprecated));
-#endif /* __x86_64__ */
+#endif /* TARGET_OS_OSX && defined(__x86_64__) */
 
     /*!
      * @function isMediaEjectable
@@ -1000,11 +1000,11 @@
 
     virtual bool isMediaRemovable() const;
 
-#ifdef __x86_64__
+#if TARGET_OS_OSX && defined(__x86_64__)
     virtual bool isMediaPollExpensive() const __attribute__ ((deprecated));
 
     virtual bool isMediaPollRequired() const __attribute__ ((deprecated));
-#endif /* __x86_64__ */
+#endif /* TARGET_OS_OSX && defined(__x86_64__) */
 
     /*!
      * @function isMediaWritable
@@ -1145,11 +1145,11 @@
                                          IOReturn status,
                                          UInt64   actualByteCount);
 
-#ifdef __x86_64__
+#if TARGET_OS_OSX && defined(__x86_64__)
     virtual void schedulePoller() __attribute__ ((deprecated));
 
     virtual void unschedulePoller() __attribute__ ((deprecated));
-#endif /* __x86_64__ */
+#endif /* TARGET_OS_OSX && defined(__x86_64__) */
 
     /*
      * This method is the power event handler for restarts and shutdowns.
@@ -1246,9 +1246,9 @@
      */
     virtual IOReturn	acceptNewMedia(void);
     
-#ifdef __x86_64__
+#if TARGET_OS_OSX && defined(__x86_64__)
     virtual UInt64	constrainByteCount(UInt64 requestedCount,bool isWrite) __attribute__ ((deprecated));
-#endif /* __x86_64__ */
+#endif /* TARGET_OS_OSX && defined(__x86_64__) */
 
     /*!
      * @function decommissionMedia
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IOStorage.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IOStorage.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IOStorage.h	2016-06-29 01:06:11.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IOStorage.h	2016-07-10 08:34:24.000000000 +0200
@@ -436,9 +436,9 @@
 
 public:
 
-#ifdef __x86_64__
+#if TARGET_OS_OSX && defined(__x86_64__)
     virtual bool attach(IOService * provider) APPLE_KEXT_OVERRIDE;
-#endif /* __x86_64__ */
+#endif /* TARGET_OS_OSX && defined(__x86_64__) */
 
     /*!
      * @function complete
@@ -535,9 +535,9 @@
                            IOStorageAttributes * attributes      = 0,
                            UInt64 *              actualByteCount = 0);
 
-#ifdef __x86_64__
+#if TARGET_OS_OSX && defined(__x86_64__)
     virtual IOReturn synchronizeCache(IOService * client) __attribute__ ((deprecated));
-#endif /* __x86_64__ */
+#endif /* TARGET_OS_OSX && defined(__x86_64__) */
 
     /*!
      * @function read
@@ -601,11 +601,11 @@
                        IOStorageAttributes * attributes,
                        IOStorageCompletion * completion) = 0;
 
-#ifdef __x86_64__
+#if TARGET_OS_OSX && defined(__x86_64__)
     virtual IOReturn discard(IOService * client,
                              UInt64      byteStart,
                              UInt64      byteCount) __attribute__ ((deprecated));
-#endif /* __x86_64__ */
+#endif /* TARGET_OS_OSX && defined(__x86_64__) */
 
     /*!
      * @function unmap
@@ -624,17 +624,17 @@
      * Returns the status of the operation.
      */
 
-#ifdef __x86_64__
+#if TARGET_OS_OSX && defined(__x86_64__)
     virtual IOReturn unmap(IOService *           client,
                            IOStorageExtent *     extents,
                            UInt32                extentsCount,
                            IOStorageUnmapOptions options = 0); /* 10.6.6 */
-#else /* !__x86_64__ */
+#else /* !TARGET_OS_OSX || !defined(__x86_64__) */
     virtual IOReturn unmap(IOService *           client,
                            IOStorageExtent *     extents,
                            UInt32                extentsCount,
                            IOStorageUnmapOptions options = 0) = 0;
-#endif /* !__x86_64__ */
+#endif /* !TARGET_OS_OSX || !defined(__x86_64__) */
 
     /*!
      * @function lockPhysicalExtents
@@ -721,17 +721,17 @@
      * Returns the status of the synchronization.
      */
 
-#ifdef __x86_64__
+#if TARGET_OS_OSX && defined(__x86_64__)
     virtual IOReturn synchronize(IOService *                 client,
                                  UInt64                      byteStart,
                                  UInt64                      byteCount,
                                  IOStorageSynchronizeOptions options = 0); /* 10.11.0 */
-#else /* !__x86_64__ */
+#else /* !TARGET_OS_OSX || !defined(__x86_64__) */
     virtual IOReturn synchronize(IOService *                 client,
                                  UInt64                      byteStart,
                                  UInt64                      byteCount,
                                  IOStorageSynchronizeOptions options = 0) = 0;
-#endif /* !__x86_64__ */
+#endif /* !TARGET_OS_OSX || !defined(__x86_64__) */
 
     /*!
      * @function getProvisionStatus
@@ -779,12 +779,12 @@
     OSMetaClassDeclareReservedUnused(IOStorage, 15);
 };
 
-#ifdef __x86_64__
+#if TARGET_OS_OSX && defined(__x86_64__)
 #ifdef KERNEL_PRIVATE
 #define _kIOStorageSynchronizeOption_super__synchronizeCache 0xFFFFFFFF
 #define _respondsTo_synchronizeCache ( IOStorage::_expansionData )
 #endif /* KERNEL_PRIVATE */
-#endif /* __x86_64__ */
+#endif /* TARGET_OS_OSX && defined(__x86_64__) */
 
 #endif /* __cplusplus */
 #endif /* KERNEL */
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostDevice.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostDevice.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostDevice.h	2016-06-29 01:13:25.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostDevice.h	2016-07-10 09:02:55.000000000 +0200
@@ -1,23 +1,213 @@
 /*
- * Copyright (c) 1998-2007 Apple Inc. All rights reserved.
+ * Copyright (c) 1998-2016 Apple Inc. All rights reserved.
  *
- * @APPLE_LICENSE_HEADER_START@
+ * @APPLE_OSREFERENCE_LICENSE_HEADER_START@
  *
- * The contents of this file constitute Original Code as defined in and
- * are subject to the Apple Public Source License Version 1.2 (the
- * "License").  You may not use this file except in compliance with the
- * License.  Please obtain a copy of the License at
- * http://www.apple.com/publicsource and read it before using this file.
+ * This file contains Original Code and/or Modifications of Original Code
+ * as defined in and that are subject to the Apple Public Source License
+ * Version 2.0 (the 'License'). You may not use this file except in
+ * compliance with the License. The rights granted to you under the License
+ * may not be used to create, or enable the creation or redistribution of,
+ * unlawful or unlicensed copies of an Apple operating system, or to
+ * circumvent, violate, or enable the circumvention or violation of, any
+ * terms of an Apple operating system software license agreement.
  *
- * This Original Code and all software distributed under the License are
- * distributed on an "AS IS" basis, WITHOUT WARRANTY OF ANY KIND, EITHER
+ * Please obtain a copy of the License at
+ * http://www.opensource.apple.com/apsl/ and read it before using this file.
+ *
+ * The Original Code and all software distributed under the License are
+ * distributed on an 'AS IS' basis, WITHOUT WARRANTY OF ANY KIND, EITHER
  * EXPRESS OR IMPLIED, AND APPLE HEREBY DISCLAIMS ALL SUCH WARRANTIES,
  * INCLUDING WITHOUT LIMITATION, ANY WARRANTIES OF MERCHANTABILITY,
  * FITNESS FOR A PARTICULAR PURPOSE, QUIET ENJOYMENT OR NON-INFRINGEMENT.
  * Please see the License for the specific language governing rights and
  * limitations under the License.
  *
- * @APPLE_LICENSE_HEADER_END@
+ * @APPLE_OSREFERENCE_LICENSE_HEADER_END@
+ */
+
+/*! 
+ @header     IOUSBHostDevice.h
+ @brief      IOUSBHostDevice is an IOService representing a USB device.
+ @discussion 
+ 
+ <h3>Session Management</h3>
+ 
+ A driver that has successfully matched on an IOUSBHostDevice is able to take ownership of the device by calling the <code>open</code> method defined by IOService on the IOUSBHostDevice.  Once <code>open</code> has completed successfully, the driver has an open session, and may use the deviceRequest interface to send control requests, and the setConfiguration interface to create or destroy child IOUSBHostInterface services.
+ 
+ When the driver is finished with control of the IOUSBHostDevice, it must call <code>close</code> to end its session.  Calling <code>close</code> will synchronously abort that session's outstanding IO on the control endpoint.  If the device is terminating for any reason, such as being unplugged, termination of the IOUSBHostDevice will be blocked until the driver calls <code>close</code>.  The willTerminate call into the driver is the recommended location to call <code>close</code>.
+ 
+ Drivers that match on an IOUSBHostInterface service do not need to open a session to the IOUSBHostDevice, as the IOUSBHostInterface will open a session to the IOUSBHostDevice on the driver's behalf.
+ 
+ <h3>deviceRequest Interface</h3>
+ 
+ The <code>deviceRequest</code> methods are used to send control requests to the device's default endpoint.  The <code>deviceRequest</code> methods may not be used for the following standard requests:
+ <ul>
+    <li>CLEAR_FEATURE ENDPOINT_HALT (USB 2.0 9.4.1) - Use <code>IOUSBHostPipe::clearStall</code> to send this request</li>
+    <li>SET_ADDRESS (USB 2.0 9.4.6)</li>
+    <li>SET_CONFIGURATION (USB 2.0 9.4.7) - Use <code>setConfiguration</code> to send this request</li>
+    <li>SET_INTERFACE (USB 2.0 9.4.10) - Use <code>IOUSBHostInterface::selectAlternateSetting</code> to send this request</li>
+ </ul>
+ 
+ <h3>IOUSBDevice Migration</h3>
+ 
+ IOUSBHostDevice serves as a replacement for IOUSBDevice.  Clients that previously matched on IOUSBDevice can use the following guide to convert to IOUSBHostDevice.
+ 
+ <code>virtual UInt16 IOUSBDevice::GetbcdUSB();</code><br>
+ Replacement: <code>USBToHost16(getDeviceDescriptor()->bcdUSB);</code>
+ 
+ <code>virtual UInt8 IOUSBDevice::GetDeviceClass();</code><br>
+ Replacement: <code>getDeviceDescriptor()->bDeviceClass;</code>
+ 
+ <code>virtual UInt8 IOUSBDevice::GetDeviceSubClass();</code><br>
+ Replacement: <code>getDeviceDescriptor()->bDeviceSubClass</code>
+ 
+ <code>virtual UInt8 IOUSBDevice::GetProtocol();</code><br>
+ Replacement: <code>getDeviceDescriptor()->bDeviceProtocol</code>
+ 
+ <code>virtual UInt8 IOUSBDevice::GetMaxPacketSize();</code><br>
+ Replacement: <code>getDeviceDescriptor->bMaxPacketSize0</code>
+ 
+ <code>virtual UInt16 IOUSBDevice::GetVendorID();</code><br>
+ Replacement: <code>USBToHost16(getDeviceDescriptor()->idVendor)</code>
+ 
+ <code>virtual UInt16 IOUSBDevice::GetProductID();</code><br>
+ Replacement: <code>USBToHost16(getDeviceDescriptor()->idProduct)</code>
+ 
+ <code>virtual UInt16 IOUSBDevice::GetDeviceRelease();</code><br>
+ Replacement: <code>USBToHost16(getDeviceDescriptor()->bcdDevice)</code>
+ 
+ <code>virtual UInt8 IOUSBDevice::GetNumConfigurations();</code><br>
+ Replacement: <code>getDeviceDescriptor()->bNumConfigurations</code>
+ 
+ <code>virtual UInt8 IOUSBDevice::GetManufacturerStringIndex();</code><br>
+ Replacement: <code>getDeviceDescriptor()->iManufacturer</code>
+ 
+ <code>virtual UInt8 IOUSBDevice::GetProductStringIndex();</code><br>
+ Replacement: <code>getDeviceDescriptor()->iProduct</code>
+ 
+ <code>virtual UInt8 IOUSBDevice::GetSerialNumberStringIndex();</code><br>
+ Replacement: <code>getDeviceDescriptor()->iSerialNumber</code>
+ 
+ <code>virtual IOReturn IOUSBDevice::FindNextInterfaceDescriptor(const IOUSBConfigurationDescriptor*, const IOUSBInterfaceDescriptor*, const IOUSBFindInterfaceRequest*, IOUSBInterfaceDescriptor**);</code><br>
+ Replacement:<br>
+ <pre>ConfigurationDescriptor* confDesc = getConfigurationDescriptor();
+InterfaceDescriptor* intDesc = NULL;
+while((intDesc = StandardUSB::getNextInterfaceDescriptor(confDesc, intDesc)) != NULL)
+{
+    if(intDesc->bInterfaceClass == kMyClass)
+    {
+        break;
+    }
+}</pre>
+ 
+ <code>virtual const IOUSBConfigurationDescriptor* IOUSBDevice::GetCachedConfigurationDescriptor(UInt8 configIndex);</code><br>
+ <code>virtual const IOUSBConfigurationDescriptor* IOUSBDevice::GetFullConfigurationDescriptor(UInt8 configIndex);</code><br>
+ Replacement: <code>getConfigurationDescriptor(configIndex)</code>
+ 
+ <code>virtual IOReturn IOUSBDevice::GetConfigurationDescriptor(UInt8 configValue, void* data, UInt32 len);</code><br>
+ Replacement: <code>getConfigurationDescriptorWithValue(configValue);</code>
+ 
+ <code>virtual IOUSBHostInterface* IOUSBDevice::FindNextInterface(IOUSBHostInterface*, IOUSBFindInterfaceRequest* request);</code><br>
+ <code>virtual OSIterator* IOUSBDevice::CreateInterfaceIterator(IOUSBFindInterfaceRequest* request);</code><br>
+ Replacement:<br>
+ <pre>OSIterator* iterator = _device->getChildIterator(gIOServicePlane);
+OSObject* candidate = NULL;
+while(iterator != NULL && (candidate = iterator->getNextObject()) != NULL)
+{
+    IOUSBHostInterface* interfaceCandidate = OSDynamicCast(IOUSBHostInterface, candidate);
+    if(   interfaceCandidate != NULL
+       && interfaceCandidate->getInterfaceDescriptor()->bInterfaceClass == kMyClass)
+    {
+        _interface = interfaceCandidate;
+        break;
+    }
+}
+OSSafeReleaseNULL(iterator);</pre>
+ 
+ <code>virtual IOReturn IOUSBDevice::SetConfiguration(IOService*, UInt8, bool);</code><br>
+ Replacement: <code>setConfiguration(configNumber, startMatchingInterfaces);</code>
+ 
+ <code>virtual UInt8 IOUSBDevice::GetSpeed();</code><br>
+ Replacement: <code>getSpeed();</code>
+ 
+ <code>virtual IOUSBController* IOUSBDevice::GetBus();</code><br>
+ Replacement: The controller cannot be directly accessed.  Use <code>getFrameNumber(...)</code> and <code>createIOBuffer(...)</code> instead.
+ 
+ <code>virtual UInt32 IOUSBDevice::GetBusPowerAvailable();</code><br>
+ Replacement: <code>allocateDownstreamBusCurrent(...);</code>
+ 
+ <code>virtual IOReturn IOUSBDevice::DeviceRequest(IOUSBDevRequest*, IOUSBCompletion*);<br>
+ virtual IOReturn IOUSBDevice::DeviceRequest(IOUSBDevRequestDesc*, IOUSBCompletion*);<br>
+ virtual IOReturn IOUSBDevice::DeviceRequest(IOUSBDevRequest*, UInt32, UInt32, IOUSBCompletion*);<br>
+ virtual IOReturn IOUSBDevice::DeviceRequest(IOUSBDevRequestDesc*, UInt32, UInt32, IOUSBCompletion*);<br></code>
+ Replacment: <code>deviceRequest(...);</code>
+ 
+ <code>virtual IOReturn IOUSBDevice::GetConfiguration(UInt8*);</code><br>
+ Replacment:
+ <pre>uint8_t configNumber  = 0;
+StandardUSB::DeviceRequest request;
+request.bmRequestType = makeDeviceRequestbmRequestType(kRequestDirectionIn, kRequestTypeStandard, kRequestRecipientDevice);
+request.bRequest      = kDeviceRequestGetConfiguration;
+request.wValue        = 0;
+request.wIndex        = 0;
+request.wLength       = sizeof(configNumber);
+ 
+uint32_t bytesTransferred = 0;
+ 
+deviceRequest(this, request, &configNumber, bytesTransferred, kUSBHostStandardRequestCompletionTimeout);</pre>
+ 
+ <code>virtual IOReturn IOUSBDevice::GetDeviceStatus(USBStatus*);</code><br>
+ Replacement:
+ <pre>uint16_t status       = 0;
+StandardUSB::DeviceRequest request;
+request.bmRequestType = makeDeviceRequestbmRequestType(kRequestDirectionIn, kRequestTypeStandard, kRequestRecipientDevice);
+request.bRequest      = kDeviceRequestGetStatus;
+request.wValue        = 0;
+request.wIndex        = 0;
+request.wLength       = sizeof(status);
+ 
+uint32_t bytesTransferred = 0;
+ 
+deviceRequest(this, request, &status, bytesTransferred, kUSBHostStandardRequestCompletionTimeout);</pre>
+ 
+ <code>virtual IOUSBPipe* IOUSBDevice::GetPipeZero();</code><br>
+ Replacement: The IOUSBHostPipe representing the default control endpoint is not accessible.  Use <code>deviceRequest(...)</code> and <code>abortDeviceRequests(...)</code> interfaces to interact with the default control endpoint.
+ 
+ <code>virtual IOReturn IOUSBDevice::GetStringDescriptor(UInt8, char*, int, UInt16);</code><br>
+ Replacement:
+ <pre>char stringBuffer[256] = { 0 };
+size_t stringLength = sizeof(stringBuffer);
+const StringDescriptor* stringDescriptor = getStringDescriptor(index);
+if(   stringDescriptor != NULL
+   && stringDescriptor->bLength > StandardUSB::kDescriptorSize)
+{
+   StandardUB::stringDescriptorToUTF8(stringDescriptor, stringBuffer, stringLength);
+}</pre>
+ 
+ <code>virtual const IOUSBDescriptorHeader* IOUSBDevice::FindNextDescriptor(const void*, UInt8);</code><br>
+ Replacement: <code>StandardUSB::getNextDescriptorWithType(getConfigurationDescriptor(), currentDescriptor, descriptorType);</code>
+ 
+ <code>virtual IOReturn IOUSBDevice::SuspendDevice(bool);</code><br>
+ Replacement: Power management should be done using the idling system described in IOUSBHostFamily.h.
+ 
+ <code>virtual IOReturn IOUSBDevice::ReEnumerateDevice(UInt32);</code><br>
+ Replacement: <code>reset();</code>
+ 
+ <code>virtual IOReturn IOUSBDevice::GetDeviceInformation(UInt32*);</code><br>
+ Replacement: <code>getPortStatus();</code>
+ 
+ <code>virtual UInt32 IOUSBDevice::RequestExtraPower(UInt32, UInt32);<br>
+ virtual IOReturn IOUSBDevice::ReturnExtraPower(UInt32, UInt32);</code><br>
+ Replacement: <code>allocateDownstreamBusCurrent(...);</code>
+ 
+ <code>virtual tUSBHostDeviceAddress IOUSBDevice::GetAddress(void);</code><br>
+ Replacement: <code>getAddress();</code>
+ 
+ <code>virtual IOReturn IOUSBDevice::ResetDevice();<br>
+ virtual UInt32 IOUSBDevice::GetExtraPowerAllocated(UInt32);<br>
+ void IOUSBDevice::SetBusPowerAvailable(UInt32);</code><br>
+ Replacement: none
  */
 
 #ifndef IOUSBHostFamily_IOUSBHostDevice_h
@@ -58,19 +248,9 @@
 class IOStateReporter;
 
 /*!
-    @class IOUSBHostDevice
-    @abstract The IOService object representing a device on the USB bus.
-    @discussion This class provides functionality to configure a device and to create
-        IOUSBHostInterface objects to represent the interfaces of the device.
- */
-
-/*!
- * @class IOUSBHostDevice
- *
- * @brief The IOService object representing a device on the USB bus.
- *
- * @discussion  This class provides functionality to configure a device and to create IOUSBHostInterface objects to 
- * represent the interfaces of the device.
+ * @class       IOUSBHostDevice
+ * @brief       The IOService object representing a USB device
+ * @discussion  This class provides functionality to send control requests to the default control endpoint, as well as create IOUSBHostInterface objects to represent the interfaces contained in the selected configuration.  Function drivers should not subclass IOUSBHostDevice.
  */
 class IOUSBHostDevice : public IOService
 {
@@ -86,13 +266,12 @@
 
 public:
     /*!
-     * @brief Powerstates supported by an IOUSBHostDevice
-     *
-     * @constant kPowerStateOff The device has been powered off and is likely in the process of terminating
-     * @constant kPowerStateSuspended The device is suspended.  All I/O has been paused and the bus will be
-     * suspended once its AppleUSBHostPort power parent enters the suspend state.
-     * @constant kPowerStateOn The device is powered on and I/O is possible.
-     * @constant kPowerStateCount Number of possible power states 
+     * @namespace   IOUSBHostDevice
+     * @brief       Powerstates supported by an IOUSBHostDevice
+     * @constant    kPowerStateOff The device has been powered off and will be terminated.
+     * @constant    kPowerStateSuspended The device is suspended.  All I/O has been paused and the bus will be suspended once its AppleUSBHostPort power parent enters the suspend state.
+     * @constant    kPowerStateOn The device is powered on and I/O is possible.
+     * @constant    kPowerStateCount Number of possible power states.
      */
     enum tPowerState
     {
@@ -102,16 +281,13 @@
         kPowerStateCount
     };
 
-    /*!
-     * @brief Factory method for creating an IOUSBHostDevice object
-     *
-     * @param controller Controller to which the USB device is attached
-     *
-     * @param speed Speed at which the device enumerated
-     *
-     * @param address Address that was assigned during enumeration
-     *
-     * @return Pointer to an IOUSBHostDevice object is successful
+    /*
+     * @brief       Factory method for creating an IOUSBHostDevice object
+     * @discussion  This method should not be called by function drivers.  IOUSBHostDevice objects are created by AppleUSBHostPort services when a device is connected.
+     * @param       controller Controller to which the USB device is attached
+     * @param       speed Speed at which the device enumerated
+     * @param       address tUSBHostDeviceAddress that has been allocated by the controller
+     * @return      Pointer to an IOUSBHostDevice object if successful, otherwise NULL
      */
     static IOUSBHostDevice* withController(AppleUSBHostController* controller, UInt8 speed, tUSBHostDeviceAddress address);
 
@@ -132,6 +308,10 @@
     
 #pragma mark IOService overrides
 public:
+    /*!
+     * @functiongroup   IOService overrides
+     * @discussion      For a discussion of proper usage for <code>open</code> and <code>close</code>, see the discussion of "Session Management" above.
+     */
 
     virtual bool attach(IOService* provider);
     virtual bool start(IOService* provider);
@@ -145,9 +325,24 @@
 
     virtual IOReturn setProperties(OSObject* properties);
 
+    /*!
+     * @brief       Open a session to the IOUSBHostDevice
+     * @discussion  This method opens a session to an IOUSBHostDevice.  It will acquire the service's workloop lock.  Child IOUSBHostInterfaces may open simultaneous sessions, but only one other service may open a session.
+     * @param       forClient The IOService that is opening a session.
+     * @param       options See IOService.h
+     * @param       arg See IOService.h
+     * @return      bool true if the session could be opened, otherwise false.
+     */
     virtual bool open(IOService* forClient, IOOptionBits options = 0, void* arg = 0);
     virtual bool handleOpen(IOService* forClient, IOOptionBits options, void* arg);
     virtual bool handleIsOpen(const IOService* forClient) const;
+    
+    /*!
+     * @brief       Close a session to the IOUSBHostDevice
+     * @discussion  This method closes an open session to an IOUSBHostDevice.  It will acquire the service's workloop lock, abort any IO associated with the specified client, and may call commandSleep to allow processing of aborted control requests before returning.
+     * @param       forClient The IOService that is closing its session.  Any IO associated with the specified client will be aborted.
+     * @param       options See IOService.h
+     */
     virtual void close(IOService* forClient, IOOptionBits options = 0);
     virtual void handleClose(IOService* forClient, IOOptionBits options);
     
@@ -197,12 +392,9 @@
 #pragma mark Power management
 public:
     /*!
-     * @methodgroup Power management
-     *
-     * @discussion The following mthods should be considered private and should not be called by client drivers.
-     * In general the below methods are overriden IOService power methods used internally to implement idling
-     * and maintain proper device state.
+     * @functiongroup Power management
      */
+
     virtual void          registerPowerService();
     virtual IOReturn      addPowerChild(IOService* theChild);
     virtual IOReturn      removePowerChild(IOPowerConnection* theChild);
@@ -214,26 +406,14 @@
     virtual IOReturn      forcePower(tPowerState powerState, bool clamp, uint32_t timeoutMs = 0);
     
     /*!
-     * @brief Allocate bus current in addition to the bMaxPower value specified by the configuration descriptor
-     *
-     * @discussion Some hosts are able to source more than the standard-defined bus current to attached devices, or
-     * may use less current than defined in the bMaxPower field of the configuration descriptor.
-     *
-     * Devices can use this interface to request more or less bus current.  The parameters passed in are abolute values
-     * of current required for operation in kPowerStateOn and kPowerStateSuspended IOUSBHostDevice power levels, and
-     * override the bMaxPower field in the configuration descriptor.  For example, if bMaxPower indicates the device
-     * requires 500mA to operate, then a request for 1000mA will double the allocated power for the device.
-     *
-     * A setConfiguration(0) call to unconfigure the device will reset these overrides.
-     *
-     * The parameters are passed by reference, and may be modified by the software stack before being returned.
-     * If more bus current is being requested than is available, the value may be reduced to stay within system limits.
-     *
-     * @param wakeUnits The number of extra mA requested when the device is in kPowerStateOn
-     *
-     * @param sleepUnits The number of extra mA requested when the device is in kPowerStateSuspended
-     *
-     * @return IOReturn kIOReturnSuccess if the device's allocation amounts were updated
+     * @brief       Allocate bus current that does not match the bMaxPower value specified by the device's configuration descriptor
+     * @discussion 
+     * Devices can use this interface to request more or less bus current than what is specified in the selected configuration descriptor's bMaxPower field.  The parameters passed in are abolute values of current required for operation in kPowerStateOn and kPowerStateSuspended IOUSBHostDevice power levels, and override the bMaxPower field in the configuration descriptor.  For example, if bMaxPower indicates the device requires 500mA to operate, then a request for 1000mA will double the allocated power for the device.
+     * A setConfiguration call to select a different configuration or unconfigure the device will reset the bus current allocations.
+     * The parameters are passed by reference, and may be modified before being returned.  If more bus current is being requested than is available, the values may be reduced to stay within system limits.
+     * @param       wakeUnits As input, the number of mA requested when the device is in kPowerStateOn.  As output, the number of mA allocated to the device in kPowerStateOn.
+     * @param       sleepUnits As input, the number of mA requested when the device is in kPowerStateSuspended.  As output, the number of mA allocated to the device in kPowerStateSuspended.
+     * @return      IOReturn kIOReturnSuccess if the device's allocation amounts were updated, otherwise an error code
      */
     virtual IOReturn allocateDownstreamBusCurrent(uint32_t& wakeUnits, uint32_t& sleepUnits);
     
@@ -242,6 +422,9 @@
         kIdleAssertionInhibit = 0,
         kIdleAssertionPermit
     };
+    /*!
+     * @brief       This method should be considered private and should not be called by function drivers.
+     */
     virtual IOReturn idleAssertion(IOService* forService, tIdleAssertion assertion);
 
     // Public pad slots for power management
@@ -300,52 +483,31 @@
 
 #pragma mark Descriptors
 public:
+    /*! @functiongroup Descriptors */
+
     /*!
-     * @brief Store the provided descriptor in the set of cached descriptors.
-     *
-     * @discussion This method will store the provided descriptor in the set of caced descriptors.  Internally,
-     * the cache is an OSDictionary containing OSSets indexted by the bDescriptorType field.  There can only be
-     * one cached descriptor in the set with identical <code>bDescriptorType</code>, <code>index</code>, and 
-     * <code>languageID</code>.  The descriptor is copied into the cache.
-     *
-     * @param descriptor Pointer to the descriptor to cache
-     *
-     * @param length Length of the descriptor, if 0 the length will be extracted from the descriptor itself.
-     *
-     * @param index Descriptor index value.  Low byte of <code>wValue</code> of the SET_DESCRIPTOR control request described
-     * in section 9.4.8 of the USB 2.0 specification.
-     *
-     * @param languageID Descriptor language ID.  <code>wIndex</code> of the SET_DESCRIPTOR control request described in 
-     * section 9.4.8 of the USB 2.0 specification.
-     *
-     * @return IOReturn result code
+     * @brief       Store the provided descriptor in the set of cached descriptors.
+     * @discussion  This method will store a descriptor in a set of cached descriptors.  If a descriptor with an identical <code>bDescriptorType</code>, <code>index</code>, and <code>languageID</code> already exists in the cache, it will be replaced.  The provided descriptor is copied, and may be discarded after being stored in the cache.  Future descriptor fetch calls such as getDescriptor will return the cached value.  Future GET_DESCRIPTOR control requests (USB 2.0 9.4.3) will also return the cached descriptor.  SET_DESCRIPTOR control requests (USB 2.0 9.4.8) will remove the cached descriptor.
+     * @param       descriptor Pointer to the descriptor to cache
+     * @param       length Length of the descriptor, or 0 the descriptor's bLength field should be used.
+     * @param       index Descriptor index value.  Low byte of <code>wValue</code> of the SET_DESCRIPTOR control request (USB 2.0 9.4.8).
+     * @param       languageID Descriptor language ID.  <code>wIndex</code> of the SET_DESCRIPTOR control request (USB 2.0 9.4.8).
+     * @return      IOReturn result code
      */
     virtual IOReturn cacheDescriptor(const StandardUSB::Descriptor* descriptor, uint16_t length = 0, uint8_t index = 0, uint16_t languageID = 0);
     
     /*!
-     * @brief Search the cache for the descriptor
-     *
-     * @discussion This method will search the descriptor cache for the descriptor that matches the input arguments.  If
-     * the descriptor is not in the cache, a device request will be issued to retrieve the descriptor from the USB device.
-     * If the device request is successful, the resulting descriptor will be added to the cache.
-     *
-     * @param type <bDescriptorType> of the descriptor to find.
-     *
-     * @param length Reference to a uint16_t which will be updated with the length of the descriptor.  As input, used as 
-     * <code>wLength</code> when fetching variable-length configuration or BOS descriptors, or when fetching nonstandard
-     * descriptor types.
-     *
-     * @param index Descriptor index value.  Low byte of <code>wValue</code> of the GET_DESCRIPTOR control request described
-     * in section 9.4.3 of the USB 2.0 specification.
-     *
-     * @param languageID Descriptor language ID.  <code>wIndex</code> of the GET_DESCRIPTOR control request described in
-     * section 9.4.3 of the USB 2.0 specification.
-     *
-     * @param requestType tDeviceRequestType to be used for the GET_DESCRIPTOR control request
-     *
-     * @param requestRecipient tDeviceRequestRecipient to be used for the GET_DESCRIPTOR control request
-     *
-     * @return Pointer to the descriptor if found.
+     * @brief       Retrieve a descriptor from the cache or the device
+     * @discussion  
+     * This method will search the descriptor cache for the descriptor that matches the input arguments.  If the descriptor is not in the cache, a GET_DESCRIPTOR control request (USB 2.0 9.4.3) will be issued to retrieve the descriptor from the device.  If the device request is successful, the retrieved descriptor will be added to the cache.
+     * This method will acquire the service's workloop lock, and may call commandSleep to perform the GET_DESCRIPTOR control request.
+     * @param       type <code>bDescriptorType</code> of the descriptor to find.
+     * @param       length Reference to a uint16_t which will be updated with the length of the descriptor.  As input, used as <code>wLength</code> when fetching variable-length configuration or BOS descriptors, or when fetching nonstandard descriptor types.
+     * @param       index Descriptor index value.  Low byte of <code>wValue</code> of the SET_DESCRIPTOR control request (USB 2.0 9.4.8).
+     * @param       languageID Descriptor language ID.  <code>wIndex</code> of the SET_DESCRIPTOR control request (USB 2.0 9.4.8).
+     * @param       requestType tDeviceRequestType to be used for a GET_DESCRIPTOR control request.
+     * @param       requestRecipient tDeviceRequestRecipient to be used for a GET_DESCRIPTOR control request.
+     * @return      Pointer to the cached descriptor if found, otherwise NULL.
      */
     virtual const StandardUSB::Descriptor* getDescriptor(uint8_t type,
                                                          uint16_t& length,
@@ -354,76 +516,49 @@
                                                          tDeviceRequestType requestType = kRequestTypeStandard,
                                                          tDeviceRequestRecipient requestRecipient = kRequestRecipientDevice);
     
-    // Retrieve and cache the entire length of standard descriptor types
-    // TODO: We are handing out pointers to cached descriptors, which could theoretically be invalidated
-    // TODO: We might want to make it so cached descriptors can't be replaced or removed by anyone but us
-    /*!
-     * @brief Return the device descriptor
-     *
-     * @discussion This method is simply a convenience method to retrieve the device descriptor.  Internally this method
-     * simply calls @link getDescriptor @/link.
-     *
-     * @return Pointer to the device descriptor if found.
+    /*!
+     * @brief       Return the device descriptor
+     * @discussion  This method uses getDescriptor to retrieve the device descriptor.
+     * @return      Pointer to the device descriptor.
      */
     virtual const StandardUSB::DeviceDescriptor* getDeviceDescriptor();
 
     /*!
-     * @brief Return the configuration descriptor with the specified index
-     *
-     * @discussion This method is simply a convenience method to retrieve the configuration descriptor.  Internally this method
-     * simply calls @link getDescriptor @/link.
-     *
-     * @param index  Descriptor index value.  Low byte of <code>wValue</code> of the GET_DESCRIPTOR control request described
-     * in section 9.4.3 of the USB 2.0 specification.
-     *
-     * @return Pointer to the configuration descriptor if found
+     * @brief       Return the configuration descriptor with the specified index
+     * @discussion  This method uses getDescriptor to retrieve a configuration descriptor.
+     * @param       index Descriptor index value
+     * @return      Pointer to the configuration descriptor if found
      */
     virtual const StandardUSB::ConfigurationDescriptor* getConfigurationDescriptor(uint8_t index);
 
     /*!
-     * @brief Return the configuration descriptor with the specified <code>bConfigurationValue</code>
-     *
-     * @discussion This method will iterate through all configuration descriptors by index looking for the one whose
-     * <code>bConfigurationValue</code> matches the input value.
-     *
-     * @param bConfigurationValue Value to match
-     *
-     * @return Pointer to the configuration descriptor if found
+     * @brief       Return the configuration descriptor with the specified <code>bConfigurationValue</code>
+     * @discussion  This method uses getDescriptor to search for a configuration descriptor with a specific <code>bConfigurationValue</code> field.
+     * @param       bConfigurationValue Value to match
+     * @return      Pointer to the configuration descriptor if found
      */
     virtual const StandardUSB::ConfigurationDescriptor* getConfigurationDescriptorWithValue(uint8_t bConfigurationValue);
     
     /*!
-     * @brief Return the currently selected configuration descriptor
-     *
-     * @discussion This method will return the configuration descriptor currently selected by a successful setConfiguration call
-     *
-     * @return Pointer to the configuration descriptor if found, or NULL if the device is not configured
+     * @brief       Return the currently selected configuration descriptor
+     * @discussion  This method uses getDescriptor to return the configuration descriptor currently selected after a successful setConfiguration call
+     * @return      Pointer to the configuration descriptor if found, or NULL if the device is not configured
      */
     virtual const StandardUSB::ConfigurationDescriptor* getConfigurationDescriptor();
 
     /*!
-     * @brief Return the capability descriptors of the device
-     *
-     * @discussion This method will attempt to return the Binary Device Object Store descriptors described in section
-     * 9.6.2 of the USB 3.1 specification.
-     *
-     * @return Pointer to the BOS descriptor if found
+     * @brief       Return the capability descriptors of the device
+     * @discussion  This method uses getDescriptor to return the device's BOS descriptors
+     * @return      Pointer to the BOS descriptor if found, otherwise NULL
      */
     virtual const StandardUSB::BOSDescriptor* getCapabilityDescriptors();
 
     /*!
-     * @brief Return a string descriptor from the device
-     *
-     * @discussion This method is simply a convenience method to retieve the desired string descriptor.  Internally this method
-     * simply calls @link getDescriptor @/link.
-     *
-     * @param index  Descriptor index value.  Low byte of <code>wValue</code> of the GET_DESCRIPTOR control request described
-     * in section 9.4.3 of the USB 2.0 specification.
-     *
-     * @param languageID  Descriptor language ID.  <code>wIndex</code> of the GET_DESCRIPTOR control request described in 
-     * section 9.4.3 of the USB 2.0 specification.
-     *
-     * @return Pointer to the descriptor if found
+     * @brief       Return a string descriptor from the device
+     * @discussion  This method uses getDescriptor to return a string descriptor.
+     * @param       index Descriptor index value.  Low byte of <code>wValue</code> of the SET_DESCRIPTOR control request (USB 2.0 9.4.8).
+     * @param       languageID Descriptor language ID.  <code>wIndex</code> of the SET_DESCRIPTOR control request (USB 2.0 9.4.8).     *
+     * @return      Pointer to the descriptor if found
      */
     virtual const StandardUSB::StringDescriptor* getStringDescriptor(uint8_t index, uint16_t languageID = StandardUSB::kLanguageIDEnglishUS);
 
@@ -469,166 +604,58 @@
     
 #pragma mark Configuration, interface, and pipe management
 public:
+    /*! @functiongroup Configuration, interface, and pipe management */
+    
     /*!
-     * @brief Select a new configuration for the device
-     *
-     * @discussion This method will select a new configuration for a device.  If the device was previously configured all
-     * child interfaces will be terminated prior to setting the new configuration.  This method will send the SET_CONFIGURATION
-     * request to the device as described by section 9.4.7 of the USB 2.0 specification.
-     *
-     * @param bConfigurationValue Configuration to select
-     *
-     * @param matchInterfaces If true, any interfaces within the new configuration will be registered for matching.
-     *
-     * @return IOReturn result code
+     * @brief       Select a new configuration for the device
+     * @discussion
+     * This method will select a new configuration for a device.  If the device was previously configured all child interfaces will be terminated prior to setting the new configuration.  This method will send the SET_CONFIGURATION control request (USB 2.0 9.4.7) to the device.
+     * This method will acquire the service's workloop lock, and may call commandSleep to perform the SET_CONFIGURATION control request.
+     * @param       bConfigurationValue Configuration to select
+     * @param       matchInterfaces If true, any interfaces within the new configuration will be registered for matching.
+     * @return      IOReturn result code
      */
     virtual IOReturn setConfiguration(uint8_t bConfigurationValue, bool matchInterfaces = true);
     
     /*!
-     * @brief Factory method to create IOUSBHostPipe objects
-     *
-     * @param descriptor Endpoint descriptor for this pipe (used to decide direction, bandwidth requirements, etc).
-     *
-     * @param companionDescriptor Companion descriptor for the endpint
-     *
-     * @param interface Interface to which the endpoint belongs
-     *
-     * @return Pointer to the newly created IOUSBHostPipe object
+     * @brief       The following method should be considered private and should not be called by function drivers.
+     * @discussion  Drivers should use <code>IOUSBHostInterface::copyPipe</code> to retrieve handles to IOUSBHostPipe objects.
      */
     virtual IOUSBHostPipe* createPipe(const StandardUSB::EndpointDescriptor* descriptor, const StandardUSB::SuperSpeedEndpointCompanionDescriptor* companionDescriptor, IOUSBHostInterface* interface);
 
     /*!
-     * @brief Issue an aynchronous setup request on the default control pipe
-     *
-     * @discussion This method will issue an asynchronous control request on the defaul pipe.
-     *
-     * <pre>
-     * @textblock
-     * The following request types are reserved and cannot be made as generic control requests, the appropriate API call should be used instead.
-     *
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientDevice), kDeviceRequestSetAddress � reserved, this request cannot be sent by drivers.
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientDevice), kDeviceRequestSetConfiguration � see setConfiguration().
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientInterface), kDeviceRequestSetInterface � see IOUSBHostInterface::selectAlternateSetting().
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientEndpoint), kRequestRecipientEndpoint � see IOUSBHostPipe::clearStall().
-     *
-     * @/textblock
-     * </pre>
-     *
-     * @param forClient The object issuing the request (generally the <code>this</code> pointer).
-     *
-     * @param request Reference to a valid StandardUSB::DeviceRequest object.  This will be copied and can therefore be stack-allocated.
-     *
-     * @param dataBuffer Pointer to the memory to be used for the I/O.
-     *
-     * @param completion Pointer to a valid, non NULL, IOUSBHostCompletion object.  This will be copied and can therefore be stack-allocated.
-     *
-     * @param completionTimeoutMs Time-out of the request in milliseconds.  If 0, the request will never time-out.
-     *
-     * @return IOReturn result code
+     * @brief       Enqueue a request on the default control endpoint
+     * @discussion  This method will enqueue an asynchronous request on the default control endpoint.  If successful, the provided completion routine will be called to report the status of the completed IO.
+     * @param       forClient The service with an open session issuing the request.
+     * @param       request Reference to a valid StandardUSB::DeviceRequest structure.  The structure is copied and can therefore be stack-allocated.
+     * @param       dataBuffer A void* or IOMemoryDescriptor* defining the memory to use for the request's data phase.
+     * @param       completion Pointer to a IOUSBHostCompletion structure.  This will be copied and can therefore be stack-allocated.
+     * @param       completionTimeoutMs Timeout of the request in milliseconds.  If 0, the request will never timeout.
+     * @return      kIOReuturnSuccess if the completion will be called in the future, otherwise error
      */
     virtual IOReturn deviceRequest(IOService* forClient, StandardUSB::DeviceRequest& request, void* dataBuffer, IOUSBHostCompletion* completion, uint32_t completionTimeoutMs = kUSBHostDefaultControlCompletionTimeoutMS);
-
-    /*!
-     * @brief Issue an aynchronous setup request on the default control pipe
-     *
-     * @discussion This method will issue an asynchronous control request on the defaul pipe.
-     * <pre>
-     * @textblock
-     * The following request types are reserved and cannot be made as generic control requests, the appropriate API call should be used instead.
-     *
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientDevice), kDeviceRequestSetAddress � reserved, this request cannot be sent by drivers.
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientDevice), kDeviceRequestSetConfiguration � see setConfiguration().
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientInterface), kDeviceRequestSetInterface � see IOUSBHostInterface::selectAlternateSetting().
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientEndpoint), kRequestRecipientEndpoint � see IOUSBHostPipe::clearStall().
-     *
-     * @/textblock
-     * </pre>
-     *
-     * @param forClient The object issuing the request (generally the <code>this</code> pointer).
-     *
-     * @param request Reference to a valid StandardUSB::DeviceRequest object.  This will be copied and can therefore be stack-allocated.
-     *
-     * @param dataBuffer Pointer to an IOMemoryDescriptor for the memory to be used for the I/O.
-     *
-     * @param completion Pointer to a valid, non NULL, IOUSBHostCompletion object.  This will be copied and can therefore be stack-allocated.
-     *
-     * @param completionTimeoutMs Time-out of the request in milliseconds.  If 0, the request will never time-out.
-     *
-     * @return IOReturn result code
-     */
     virtual IOReturn deviceRequest(IOService* forClient, StandardUSB::DeviceRequest& request, IOMemoryDescriptor* dataBuffer, IOUSBHostCompletion* completion, uint32_t completionTimeoutMs = kUSBHostDefaultControlCompletionTimeoutMS);
     
     /*!
-     * @brief Issue a synchronous setup request on the default control pipe.
-     *
-     * <pre>
-     * @textblock
-     * The following request types are reserved and cannot be made as generic control requests, the appropriate API call should be used instead.
-     *
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientDevice), kDeviceRequestSetAddress � reserved, this request cannot be sent by drivers.
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientDevice), kDeviceRequestSetConfiguration � see setConfiguration().
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientInterface), kDeviceRequestSetInterface � see IOUSBHostInterface::selectAlternateSetting().
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientEndpoint), kRequestRecipientEndpoint � see IOUSBHostPipe::clearStall().
-     *
-     * @/textblock
-     * </pre>
-     *
-     * @param forClient The object issuing the request (generally the <code>this</code> pointer).
-     *
-     * @param request Reference to a valid StandardUSB::DeviceRequest object.  This will be copied and can therefore be stack-allocated.
-     *
-     * @param dataBuffer Pointer to the memory to be used for the I/O.
-     *
-     * @param bytesTransferred Reference which will be updated with the bytes transferred during the request.
-     *
-     * @param completionTimeoutMs Time-out of the request in milliseconds.  If 0, the request will never time-out.
-     *
-     * @return IOReturn result code
+     * @brief       Send a request on the default control endpoint
+     * @discussion  This method will send a synchronous request on the default control endpoint, and will not return until the request is complete.  This method will acquire the service's workloop lock, and will call commandSleep to send the control request.
+     * @param       forClient The service with an open session issuing the request.
+     * @param       request Reference to a valid StandardUSB::DeviceRequest structure.
+     * @param       dataBuffer A void* or IOMemoryDescriptor* defining the memory to use for the request's data phase.
+     * @param       bytesTransferred A uint32_t reference which will be updated with the byte count of the completed data phase.
+     * @param       completionTimeoutMs Timeout of the request in milliseconds.  If 0, the request will never timeout.
+     * @return      IOReturn value indicating the result of the IO request
      */
     virtual IOReturn deviceRequest(IOService* forClient, StandardUSB::DeviceRequest& request, void* dataBuffer, uint32_t& bytesTransferred, uint32_t completionTimeoutMs = kUSBHostDefaultControlCompletionTimeoutMS);
-
-    /*!
-     * @brief Issue a synchronous setup request on the default control pipe.
-     *
-     * <pre>
-     * @textblock
-     * The following request types are reserved and cannot be made as generic control requests, the appropriate API call should be used instead.
-     *
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientDevice), kDeviceRequestSetAddress � reserved, this request cannot be sent by drivers.
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientDevice), kDeviceRequestSetConfiguration � see setConfiguration().
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientInterface), kDeviceRequestSetInterface � see IOUSBHostInterface::selectAlternateSetting().
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientEndpoint), kRequestRecipientEndpoint � see IOUSBHostPipe::clearStall().
-     *
-     * @/textblock
-     * </pre>
-     *
-     * @param forClient The object issuing the request (generally the <code>this</code> pointer).
-     *
-     * @param request Reference to a valid StandardUSB::DeviceRequest object.  This will be copied and can therefore be stack-allocated.
-     *
-     * @param dataBuffer Pointer to an IOMemoryDescriptor for the memory to be used for the I/O.
-     *
-     * @param bytesTransferred Reference which will be updated with the bytes transferred during the request.
-     *
-     * @param completionTimeoutMs Time-out of the request in milliseconds.  If 0, the request will never time-out.
-     *
-     * @return IOReturn result code
-     */
     virtual IOReturn deviceRequest(IOService* forClient, StandardUSB::DeviceRequest& request, IOMemoryDescriptor* dataBuffer, uint32_t& bytesTransferred, uint32_t completionTimeoutMs = kUSBHostDefaultControlCompletionTimeoutMS);
 
     /*!
-     * @brief Abort device requests made via the @link deviceRequest @\link methods by <code>forClient</code>
-     *
-     * @discussion This method will abort any requests made via the @link deviceRequest @\link methods.  It will not abort
-     * requests made through other interface objects.
-     *
-     * @param forClient Client which issued the requests
-     *
-     * @param options IOUSBHostIOSource::tAbortOptions
-     *
-     * @param withError IOReturn error value to return with the requests.
-     *
-     * @return IOReturn result code
+     * @brief       Abort device requests made via the @link deviceRequest @/link methods by <code>forClient</code>
+     * @discussion  This method will abort any requests associated with a specific client made via the @link deviceRequest @/link methods.  It will not abort requests made by other clients.
+     * @param       forClient Client which issued the requests
+     * @param       options IOUSBHostIOSource::tAbortOptions
+     * @param       withError IOReturn error value to return with the requests.  The default value of kIOReturnAborted should be used.
+     * @return      IOReturn result code
      */
     virtual IOReturn abortDeviceRequests(IOService* forClient = NULL, IOOptionBits options = IOUSBHostIOSource::kAbortAsynchronous, IOReturn withError = kIOReturnAborted);
     
@@ -677,69 +704,48 @@
 
 #pragma mark Miscellaneous
 public:
+    /*! @functiongroup Provider and state accessors */
+
     /*!
-     * @brief Return the device's address
-     *
-     * @return Current address of the device
+     * @brief   Retrieve the device's address
+     * @return  Current address of the device
      */
     virtual tUSBHostDeviceAddress getAddress() const;
     
     /*!
-     * @brief Return the device's speed
-     *
-     * @return The enumerated speed of the device:
-     * @constant kUSBHostConnectionSpeedLow
-     * @constant kUSBHostConnectionSpeedFull
-     * @constant kUSBHostConnectionSpeedHigh
-     * @constant kUSBHostConnectionSpeedSuper
-     * @constant kUSBHostConnectionSpeedSuperPlus
+     * @brief       Retrieve the device's operational speed
+     * @return      tInternalUSBHostConnectionSpeed
      */
     virtual uint8_t getSpeed() const;
     
     /*!
-     * @brief Return the current frame number of the USB bus
-     *
-     * @description This method will return the current frame number of the USB bus.  This is most useful for
-     * scheduling future isochronous requests.
-     *
-     * @param theTime If not NULL, this will be updated with the current system time
-     *
-     * @return The current frame number
+     * @brief       Return the current frame number of the USB controller
+     * @description This method will return the current frame number of the USB controller, omitting microframe.  This is most useful for scheduling future isochronous requests.
+     * @param       theTime If not NULL, this will be updated with the current system time
+     * @return      The current frame number
      */
     virtual uint64_t getFrameNumber(AbsoluteTime* theTime = NULL);
     
     /*!
-     * @brief Reset and re-emerate the device
-     *
-     * @discussion This function will reset and re-enumerate the USB device.  The current IOUSBHostDevice object and all
-     * of its children will be terminated.  A new IOUSBHostDevice object will be created and registered if the reset
-     * is successful and the previous object has finished terminating.  This function may not be called from the port
-     * workloop thread.
-     *
-     * @return IOReturn result code
+     * @brief       Terminate the device and attempt to reenumerate it
+     * @discussion  This function will reset and attempt to reenumerate the USB device.  The current IOUSBHostDevice object and all of its children will be terminated.  A new IOUSBHostDevice object will be created and registered if the reset is successful and the previous object has finished terminating.  This function may not be called from the port workloop thread.
+     * @return      IOReturn result code
      */
     virtual IOReturn reset();
     
     /*!
-     * @brief Return the current port status
-     *
-     * @discussion This method will return the current port status as a logical OR of bits described by @link tUSBHostPortStatus @\link
-     *
-     * @return port status
+     * @brief       Return the current port status
+     * @discussion  This method will return the current port status as described by @link tUSBHostPortStatus @/link
+     * @return      port status
      */
     virtual uint32_t getPortStatus();
     
     /*!
-     * @brief Allocate a buffer to be used for I/O
-     *
-     * @discussion The underlying host controller hardware may have alignment and fragmentation restrictions.  This
-     * method will return a buffer which is guaranteed to meet the restrictions the host controller may have.
-     *
-     * @param options kIODirectionOut, kIODirectionIn to set the direction of the I/O transfer.
-     *
-     * @param capacity Size of the buffer to allocate
-     *
-     * @return Pointer to the newly allocated memory descriptor or NULL
+     * @brief       Allocate a buffer to be used for I/O
+     * @discussion  This method will allocate an IOBufferMemoryDescriptor optimized for use by the underlying controller hardware.  A buffer allocated by this method will not be bounced to perform DMA operations.
+     * @param       options kIODirectionOut, kIODirectionIn to set the direction of the I/O transfer.
+     * @param       capacity Size of the buffer to allocate
+     * @return      Pointer to an IOBufferMemoryDescriptor if successful, otherwise NULL
      */
     virtual IOBufferMemoryDescriptor* createIOBuffer(IOOptionBits options, mach_vm_size_t capacity);
 
@@ -768,185 +774,6 @@
     OSMetaClassDeclareReservedUnused(IOUSBHostDevice, 98);
     OSMetaClassDeclareReservedUnused(IOUSBHostDevice, 99);
 
-public:
-    // Removed legacy methods
-    
-    // virtual UInt16 GetbcdUSB() __attribute__((deprecated));
-    // Replacement: USBToHost16(getDeviceDescriptor()->bcdUSB);
-    
-    // virtual UInt8  GetDeviceClass() __attribute__((deprecated));
-    // Replacement: getDeviceDescriptor()->bDeviceClass;
-    
-    // virtual UInt8  GetDeviceSubClass() __attribute__((deprecated));
-    // Replacement: getDeviceDescriptor()->bDeviceSubClass
-    
-    // virtual UInt8  GetProtocol() __attribute__((deprecated));
-    // Replacement: getDeviceDescriptor()->bDeviceProtocol
-    
-    // virtual UInt8  GetMaxPacketSize() __attribute__((deprecated));
-    // Replacement: getDeviceDescriptor->bMaxPacketSize0
-    
-    // virtual UInt16 GetVendorID() __attribute__((deprecated));
-    // Replacement: USBToHost16(getDeviceDescriptor()->idVendor)
-    
-    // virtual UInt16 GetProductID() __attribute__((deprecated));
-    // Replacement: USBToHost16(getDeviceDescriptor()->idProduct)
-    
-    // virtual UInt16 GetDeviceRelease() __attribute__((deprecated));
-    // Replacement: USBToHost16(getDeviceDescriptor()->bcdDevice)
-
-    // virtual UInt8  GetNumConfigurations() __attribute__((deprecated));
-    // Replacement: getDeviceDescriptor()->bNumConfigurations
-    
-    // virtual UInt8  GetManufacturerStringIndex() __attribute__((deprecated));
-    // Replacement: getDeviceDescriptor()->iManufacturer
-    
-    // virtual UInt8  GetProductStringIndex() __attribute__((deprecated));
-    // Replacement: getDeviceDescriptor()->iProduct
-
-    // virtual UInt8  GetSerialNumberStringIndex() __attribute__((deprecated));
-    // Replacement: getDeviceDescriptor()->iSerialNumber
-    
-    // virtual IOReturn FindNextInterfaceDescriptor(const IOUSBConfigurationDescriptor* configDescIn,
-    //                                              const IOUSBInterfaceDescriptor*     intfDesc,
-    //                                              const IOUSBFindInterfaceRequest*    request,
-    //                                              IOUSBInterfaceDescriptor**          descOut) __attribute__((deprecated));
-    // Replacement:
-    // ConfigurationDescriptor* confDesc = getConfigurationDescriptor(1);
-    // InterfaceDescriptor* intDesc = NULL;
-    // while((intDesc = getNextInterfaceDescriptor(confDesc, intDesc)) != NULL)
-    // {
-    //     if(intDesc->bInterfaceClass == kMyClass)
-    //     {
-    //         break;
-    //     }
-    // }
-    
-    // virtual const IOUSBConfigurationDescriptor* GetCachedConfigurationDescriptor(UInt8 configIndex) __attribute__((deprecated));
-    // virtual const IOUSBConfigurationDescriptor* GetFullConfigurationDescriptor(UInt8 configIndex) __attribute__((deprecated));
-    // Replacement: getConfigurationDescriptor(configIndex)
-    
-    // virtual IOReturn GetConfigurationDescriptor(UInt8 configValue, void* data, UInt32 len) __attribute__((deprecated));
-    // Replacement: getConfigurationDescriptorWithValue(configValue)
-
-
-    // virtual IOUSBHostInterface* FindNextInterface(IOUSBHostInterface*        current,
-    //                                               IOUSBFindInterfaceRequest* request) __attribute__((deprecated));
-    // virtual OSIterator* CreateInterfaceIterator(IOUSBFindInterfaceRequest* request) __attribute__((deprecated));
-    // Replacement:
-    // OSIterator* iterator = _device->getChildIterator(gIOServicePlane);
-    // OSObject* candidate = NULL;
-    // while(iterator != NULL && (candidate = iterator->getNextObject()) != NULL)
-    // {
-    //     IOUSBHostInterface* interfaceCandidate = OSDynamicCast(IOUSBHostInterface, candidate);
-    //     if(   interfaceCandidate != NULL
-    //        && interfaceCandidate->getInterfaceDescriptor()->bInterfaceClass == kUSBHubClass)
-    //     {
-    //         _interface = interfaceCandidate;
-    //         break;
-    //     }
-    // }
-    // OSSafeReleaseNULL(iterator);
-    
-    // virtual IOReturn SetConfiguration(IOService* forClient, UInt8 configNumber, bool startMatchingInterfaces = true) __attribute__((deprecated));
-    // Replacement: setConfiguration(configNumber, startMatchingInterfaces)
-
-    // No longer supported.
-    // Use getSpeed instead.
-    // virtual UInt8 GetSpeed(void) __attribute__((deprecated));
-
-    // virtual AppleUSBHostController* GetBus(void) __attribute__((deprecated));
-    // Use getFrameNumber and createIOBuffer instead.
-
-    // No longer supported.
-    // Use allocateDownstreamBusCurrent instead.
-    // virtual UInt32 GetBusPowerAvailable(void) __attribute__((deprecated));
-
-    // virtual IOReturn DeviceRequest(IOUSBDevRequest* request,
-    //                                IOUSBCompletion* completion = 0) __attribute__((deprecated));
-    // virtual IOReturn DeviceRequest(IOUSBDevRequestDesc* request,
-    //                                IOUSBCompletion*     completion = 0) __attribute__((deprecated));
-    // virtual IOReturn DeviceRequest(IOUSBDevRequest* request,
-    //                                UInt32           noDataTimeout,
-    //                                UInt32           completionTimeout,
-    //                                IOUSBCompletion* completion = 0) __attribute__((deprecated));
-    // virtual IOReturn DeviceRequest(IOUSBDevRequestDesc* request,
-    //                                UInt32               noDataTimeout,
-    //                                UInt32               completionTimeout,
-    //                                IOUSBCompletion*     completion = 0) __attribute__((deprecated));
-    // Replacment:
-    // deviceRequest(...)
-    
-    // virtual IOReturn GetConfiguration(UInt8* configNumber) __attribute__((deprecated));
-    // Replacment:
-    // uint8_t configNumber  = 0;
-    // StandardUSB::DeviceRequest request;
-    // request.bmRequestType = makeDeviceRequestbmRequestType(kRequestDirectionIn, kRequestTypeStandard, kRequestRecipientDevice);
-    // request.bRequest      = kDeviceRequestGetConfiguration;
-    // request.wValue        = 0;
-    // request.wIndex        = 0;
-    // request.wLength       = sizeof(configNumber);
-    //
-    // uint32_t bytesTransferred = 0;
-    //    
-    // deviceRequest(this, request, &configNumber, bytesTransferred, kUSBHostStandardRequestCompletionTimeout);
-    
-    // virtual IOReturn GetDeviceStatus(USBStatus* status) __attribute__((deprecated));
-    // Replacement:
-    // uint16_t status       = 0;
-    // StandardUSB::DeviceRequest request;
-    // request.bmRequestType = makeDeviceRequestbmRequestType(kRequestDirectionIn, kRequestTypeStandard, kRequestRecipientDevice);
-    // request.bRequest      = kDeviceRequestGetStatus;
-    // request.wValue        = 0;
-    // request.wIndex        = 0;
-    // request.wLength       = sizeof(status);
-    //
-    // uint32_t bytesTransferred = 0;
-    //
-    // deviceRequest(this, request, &status, bytesTransferred, kUSBHostStandardRequestCompletionTimeout);
-    
-    // virtual IOUSBHostPipe* GetPipeZero() __attribute__((deprecated));
-    // virtual IOUSBHostPipe* getPipeZero() __attribute__((deprecated));
-    // Replacement: none.  Use deviceRequest(...) and abortDeviceRequests(...) interfaces to interact with the default endpoint
-
-    // virtual IOReturn GetStringDescriptor(UInt8 index, char* buf, int maxLen, UInt16 lang = 0x409) __attribute__((deprecated));
-    // Replacement: getStringDescriptor(index, languageID)
-    // Use sys/utfconv.h to extract UTF strings from string descriptors:
-    // char stringBuffer[256] = { 0 };
-    // size_t utf8len = 0;
-    // const StringDescriptor* stringDescriptor = getStringDescriptor(index);
-    // if(   stringDescriptor != NULL
-    //    && stringDescriptor->bLength > StandardUSB::kDescriptorSize)
-    // {
-    //     utf8_encodestr(reinterpret_cast<const u_int16_t*>(stringDescriptor->bString), stringDescriptor->bLength - kDescriptorSize,
-    //                    reinterpret_cast<u_int8_t*>(stringBuffer), &utf8len, sizeof(stringBuffer), '/', UTF_LITTLE_ENDIAN);
-    // }
-
-    // virtual const IOUSBDescriptorHeader* FindNextDescriptor(const void* cur, UInt8 descType) __attribute__((deprecated));
-    // Replacement: StandardUSB::getNextDescriptor(getConfigurationDescriptor(currentConfig), cur, descType)
-
-    // virtual IOReturn SuspendDevice(bool suspend) __attribute__((deprecated));
-    // Replacement: forcePower(kPowerStateSuspended, false) or forcePower(kPowerStateOn, false)
-
-    // virtual IOReturn ReEnumerateDevice(UInt32 options) __attribute__((deprecated));
-    // Replacement: reset()
-
-    // virtual IOReturn GetDeviceInformation(UInt32* info) __attribute__((deprecated));
-    // Replacement: getPortStatus()
-
-    // virtual UInt32 RequestExtraPower(UInt32 type, UInt32 requestedPower) __attribute__((deprecated));
-    // virtual IOReturn ReturnExtraPower(UInt32 type, UInt32 returnedPower) __attribute__((deprecated));
-    // TODO: Replacement
-
-    // virtual tUSBHostDeviceAddress GetAddress(void) __attribute__((deprecated));
-    // Replacement: getAddress()
-    
-    // virtual IOReturn ResetDevice() __attribute__((deprecated));
-    // virtual UInt32 GetExtraPowerAllocated(UInt32 type) __attribute__((deprecated));
-    // virtual void ForceIdlePolicy(UInt32 deviceIdleTimeout, UInt32 ioIdleTimeout) __attribute__((deprecated));
-    // void SetBusPowerAvailable(UInt32 newPower) __attribute__((deprecated));
-    // Replacement: none
-
 protected:
     enum
     {
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostFamily.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostFamily.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostFamily.h	2016-06-29 01:13:25.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostFamily.h	2016-07-10 09:02:55.000000000 +0200
@@ -1,10 +1,103 @@
-//
-//  IOUSBHostFamily.h
-//  IOUSBHostFamily
-//
-//  Created by Dan Wilson on 1/14/15.
-//
-//
+/*
+ * Copyright (c) 1998-2016 Apple Inc. All rights reserved.
+ *
+ * @APPLE_OSREFERENCE_LICENSE_HEADER_START@
+ *
+ * This file contains Original Code and/or Modifications of Original Code
+ * as defined in and that are subject to the Apple Public Source License
+ * Version 2.0 (the 'License'). You may not use this file except in
+ * compliance with the License. The rights granted to you under the License
+ * may not be used to create, or enable the creation or redistribution of,
+ * unlawful or unlicensed copies of an Apple operating system, or to
+ * circumvent, violate, or enable the circumvention or violation of, any
+ * terms of an Apple operating system software license agreement.
+ *
+ * Please obtain a copy of the License at
+ * http://www.opensource.apple.com/apsl/ and read it before using this file.
+ *
+ * The Original Code and all software distributed under the License are
+ * distributed on an 'AS IS' basis, WITHOUT WARRANTY OF ANY KIND, EITHER
+ * EXPRESS OR IMPLIED, AND APPLE HEREBY DISCLAIMS ALL SUCH WARRANTIES,
+ * INCLUDING WITHOUT LIMITATION, ANY WARRANTIES OF MERCHANTABILITY,
+ * FITNESS FOR A PARTICULAR PURPOSE, QUIET ENJOYMENT OR NON-INFRINGEMENT.
+ * Please see the License for the specific language governing rights and
+ * limitations under the License.
+ *
+ * @APPLE_OSREFERENCE_LICENSE_HEADER_END@
+ */
+
+/*! 
+ @header     IOUSBHostFamily.h
+ @brief      IOUSBHostFamily provides support for discovering, enumerating, and communicating with USB devices.
+ @discussion Starting with Mac OS X El Capitan, IOUSBHostFamily serves as a replacement for IOUSBFamily.
+ 
+ <h3>Architecture</h3>
+
+ USB host controller hardware is managed by AppleUSBHostController subclasses such as AppleUSBXHCI and AppleUSBEHCI.  Each AppleUSBHostController is the parent to one or more AppleUSBHostPort services, and each AppleUSBHostPort is able to enumerate a single IOUSBHostDevice service.  IOUSBHostDevice is the parent to zero or more IOUSBHostInterface services, and IOUSBHostInterface provides access to zero or more IOUSBHostPipe objects.  USB 3.0 and newer streaming-capable IOUSBHostPipe objects can generate one or more IOUSBHostStream objects.
+ 
+ AppleUSBHostPort services provide a workloop that is dedicated for use by the port, its enumerated device, and any attached drivers.  As such, drivers should not create or manage their own workloops.
+ 
+ IOUSBHostDevice and IOUSBHostInterface services can be matched on and controlled by third-party drivers, and are documented in IOUSBHostDevice.h and IOUSBHostInterface.h.  IOUSBHostPipe and IOUSBHostStream services share a common IOUSBHostIOSource base class, and are documented in IOUSBHostIOSource.h, IOUSBHostPipe.h, and IOUSBHostStream.h.  AppleUSBHostController and AppleUSBHostPort should be considered opaque classes.
+ 
+ <h3>Matching</h3>
+ 
+ IOUSBHostDevice and IOUSBHostInterface matching uses the same properties as the deprecated IOUSBDevice and IOUSBInterface classes.  See <a href="https://developer.apple.com/library/mac/qa/qa1076/_index.html">QA1076: Tips on USB driver matching for Mac OS X</a> for additional information.
+
+ <h3>Power management</h3>
+
+ IOUSBHostFamily supports more advanced power management capabilities, including pausing IO, and automatic suspend of idle devices.  All of this functionality is guided by idle policies set on IOUSBHostInterface services and IOUSBHostPipe objects.  The idle policy functionality allows most drivers to ignore suspend or resume events on the bus, and makes it unnecessary for them to actively participate in power management.
+
+ <h4>Idle suspend</h4>
+
+ By default, interfaces and pipes do not enable an idle policy, and the device will remain in the active (not suspended) state as long as the host machine is awake.  To enable idle suspend, the driver controlling an IOUSBHostInterface must enable an idle policy with the <code>IOUSBHostInterface::setIdlePolicy</code> API.  In the simple case of a device with only a single interface, when the interface's endpoints have no IO requests pending, the system will wait the time specified in the setIdlePolicy call, and then electrically suspend the device.  A new IO request during the wait period will cancel the suspend, and a new IO request after the device has suspended will immediately resume the device and initiate the IO.
+ 
+ In the more complex case of a device with multiple interfaces, a consensus idle policy must be calculated by finding the largest idle policy for all interfaces, excluding those which have not been opened by a driver.
+ 
+ Selection of an idle policy depends on the individual device, and should factor in resume latency tolerance.  The recommended idle policy for an interface is 50ms or larger.
+ 
+ Idle suspend is disabled if a driver is the power child of the IOUSBHostDevice and resides in a power state with an input power requirement that does not include <code>kIOPMLowPower</code>.
+
+ <h4>Pausing IO</h4>
+ 
+ A more advanced approach to idle suspend allows the device to suspend while transfers are still pending.  This is particularly useful for interfaces with interrupt IN endpoints that always have an IO pending, and otherwise would not idle suspend.  To enable IO pause, endpoints that would otherwise keep the device in the active state must enable an idle policy with the <code>IOUSBHostPipe::setIdlePolicy</code> API.  When an IOUSBHostPipe with an idle policy begins servicing a new IO, but does not complete it within the wait time specified in the idle policy, the IOUSBHostPipe is now considered idle and will not keep the device in the active state.  Idle endpoints are still serviced on the bus, and the IOUSBHostPipe is capable of moving data even when idle.  When all endpoints in the device have no pending IO requests or are idle, the idle suspend wait period begins as described above.
+
+ If the idle suspend period elapses without any new IO requests that would cancel the suspend, IOUSBHostFamily will pause the transfers on the bus and suspend the device.  IO requests are not aborted or returned to the driver when paused in this manner.
+ 
+ After resuming the device due to a remote wake or a new IO request, the pending IO requests are resumed on the bus, and data movement can continue.  If a large transfer is interrupted by a suspend, IOUSBHostFamily will combine the packets from before and after the suspend and return them as a single transfer result.  Note that not all firmware supports a mid-transfer suspend/resume, and pausing IO should only be enabled for devices that have been tested for this use case.
+ 
+ Control and isochronous IOUSBHostPipe objects never enable an idle policy, and pending IO on these endpoints will always prevent idle suspend.
+ 
+ Selection of an idle policy depends on the individual endpoint, and should factor in resume latency tolerance and expected data transfer frequency.  The recommended idle policy for IN-direction bulk and interrupt endpoints is 50ms or larger.  Firmware must be capable of handling a mid-transfer suspend/resume, and should issue a remote wake when data is available to be read.  Enabling an idle policy for OUT-direction bulk or interrupt endpoints is not generally recommended, but if enabled, firmware should have the ability to issue a remote wake when there is space in its endpoint buffer for additional data.
+
+ <h4>System power state changes</h4>
+ 
+ For devices that idle suspend, it may be necessary to perform IO as the system enters the sleep state, for example to enable wake-on-LAN for an Ethernet controller.  Drivers that wish to perform this type of IO should call <code>IOService::registerInterestedDriver</code> on the PM root to be notified of system-level changes.  During the <code>powerStateWillChangeTo</code> notification with a capability flag including <code>kIOPMSleepCapability</code>, the driver can initiate an IO request and resume the device.  Once the driver acknowledges this <code>powerStateWillChangeTo</code> notification, the device may not be able to raise its power state until the system wakes.  Attempting an IO request from other PM root <code>powerStateWillChangeTo</code> and <code>powerStateDidChangeTo</code> notifications may result in a deadlock waiting for a power state change.
+
+ <h3>Comparison to IOUSBFamily</h3>
+ 
+ Developers already familiar with IOUSBFamily can take advantage of new capabilities in IOUSBHostFamily that can simplify driver development and maintenace.
+ 
+ <h4>Workloops</h4>
+ 
+ IOUSBFamily provided a workloop for each controller, and all downstream devices shared that workloop.  By contrast, each AppleUSBHostPort creates a workloop dedicated for its attached device, which significantly reduces lock contention and improves responsiveness for drivers attached to IOUSBHostDevice or IOUSBHostInterface services.  Because the workloop is not shared across many unrelated services, driver developers are discouraged from creating an additional workloop.
+ 
+ <h4>Synchronous IO from completion callbacks</h4>
+ 
+ IOUSBFamily did not permit synchronous IO to be executed from a completion callback, but this restriction has been removed in IOUSBHostFamily.  Driver developers can now issue a sequence of synchronous commands in a completion routine without chaining thread calls or using complex state machines.
+ 
+ <h4>IO bookkeeping</h4>
+ 
+ IOUSBHostFamily now tracks all outstanding IOs for an endpoint, and offers more predictable behavior when aborting transfers or terminating services.  In most cases, driver developers no longer need to track the number of outstanding IOs, and can terminate their services with more determinism.
+
+ <h3>Driver Recommendations</h3>
+ 
+ <ul>
+    <li>Do not create a separate workloop</li>
+    <li>If joining the power plane, reside in a <code>kIOPMLowPower</code> state to enable idle suspend</li>
+    <li>If supporting pausing IO, only enable an idle policy on bulk or interrupt IN endpoints</li>
+    <li>If interested in system power state changes, call <code>registerInterestedDriver</code> on the PM root</li>
+ </ul>
+*/
 
 #ifndef IOUSBHostFamily_IOUSBHostFamily_h
 #define IOUSBHostFamily_IOUSBHostFamily_h
@@ -85,6 +178,7 @@
 };
 
 /*!
+ * @enum tInternalUSBHostConnectionSpeed
  * @brief Connection speeds used internally by IOUSBHostFamily
  */
 enum
@@ -97,46 +191,39 @@
     kUSBHostConnectionSpeedCount        = 5
 };
 
-/*!
- @define IOUSBHostFamily message codes
- @discussion Messages specific to the IOUSBHostFamily
- */
-
-// The two most significant bits of the error and message code are used to indicate a USB subgroup.
-#define iokit_usblegacy_group    (0 << StandardUSBBitRangePhase(12, 13))
-#define iokit_usbhost_group      (1 << StandardUSBBitRangePhase(12, 13))
 #define iokit_usb_codemask       StandardUSBBitRange(0, 11)
-
+#define iokit_usbhost_group      (1 << StandardUSBBitRangePhase(12, 13))
+#define iokit_usblegacy_group    (0 << StandardUSBBitRangePhase(12, 13))
+#define iokit_usbhost_err(message) ((IOReturn)(iokit_family_err(sub_iokit_usb, iokit_usbhost_group | (message & iokit_usb_codemask))))
 #define iokit_usbhost_msg(message) ((uint32_t)(iokit_family_msg(sub_iokit_usb, iokit_usbhost_group | (message & iokit_usb_codemask))))
 #define	iokit_usblegacy_err_msg(message)     ((uint32_t)(sys_iokit | sub_iokit_usb | message))
 
+/*!
+ @definedblock  IOUSBHostFamily message codes
+ @discussion    Messages passed between USB services using the <code>IOService::message</code> API.
+ */
 #define kUSBHostMessageConfigurationSet               iokit_usbhost_msg(0x00)       // 0xe0005000  IOUSBHostDevice -> clients upon a setConfiguration call.
 #define kUSBHostMessageRenegotiateCurrent             iokit_usbhost_msg(0x01)       // 0xe0005001  Request clients to renegotiate bus current allocations
 
-#define kUSBHostMessageUpdateIdlePolicy               iokit_usbhost_msg(0x100)      // 0xe0005100  Internal use only.  IOUSBHostInterface -> IOUSBHostDevice to update its idle policy.
-#define kUSBHostMessageRemoteWake                     iokit_usbhost_msg(0x101)      // 0xe0005101  Internal use only.  AppleUSBHostPort -> IOUSBHostDevice upon a remote wake event.
-#define kUSBHostMessageDeviceSuspend                  iokit_usbhost_msg(0x102)      // 0xe0005102  Internal use only.  IOUSBHostDevice -> clients upon a suspend event.
-#define kUSBHostMessageDeviceResume                   iokit_usbhost_msg(0x103)      // 0xe0005103  Internal use only.  IOUSBHostDevice -> clients upon a resume event.
-#define kUSBHostMessagePortsCreated                   iokit_usbhost_msg(0x104)      // 0xe0005104  Internal use only.  AppleUSBHostController and AppleUSBHub -> clients after all ports have been created.
+#define kUSBHostMessageUpdateIdlePolicy               iokit_usbhost_msg(0x100)      // 0xe0005100  Apple Internal use only.  IOUSBHostInterface -> IOUSBHostDevice to update its idle policy.
+#define kUSBHostMessageRemoteWake                     iokit_usbhost_msg(0x101)      // 0xe0005101  Apple Internal use only.  AppleUSBHostPort -> IOUSBHostDevice upon a remote wake event.
+#define kUSBHostMessageDeviceSuspend                  iokit_usbhost_msg(0x102)      // 0xe0005102  Apple Internal use only.  IOUSBHostDevice -> clients upon a suspend event.
+#define kUSBHostMessageDeviceResume                   iokit_usbhost_msg(0x103)      // 0xe0005103  Apple Internal use only.  IOUSBHostDevice -> clients upon a resume event.
+#define kUSBHostMessagePortsCreated                   iokit_usbhost_msg(0x104)      // 0xe0005104  Apple Internal use only.  AppleUSBHostController and AppleUSBHub -> clients after all ports have been created.
 #define kUSBHostMessageDeviceConnected                iokit_usbhost_msg(0x105)      // 0xe0005105  Apple Internal use only.  AppleUSBRemovablePort -> clients after a connect.
 #define kUSBHostMessageDeviceDisconnected             iokit_usbhost_msg(0x106)      // 0xe0005106  Apple Internal use only.  AppleUSBRemovablePort -> clients after a disconnect.
 #define kUSBHostMessageControllerPoweredOn            iokit_usbhost_msg(0x107)      // 0xe0005107  Apple Internal use only.  AppleEmbeddedUSBXHCIFL1100 -> FL1100Boot after a stable power state is reached.
 #define kUSBHostMessageNonInterruptIsochFrame         iokit_usbhost_msg(0x108)      // 0xe0005108  Apple Internal use only. 
 
 // User Message Support
-#define kUSBHostMessageOvercurrentCondition           iokit_usblegacy_err_msg(0x13) // 0xe0004013  Message sent to the clients of the device's hub parent, when a device causes an overcurrent condition.  The message argument contains the locationID of the device
-#define kUSBHostMessageNotEnoughPower                 iokit_usblegacy_err_msg(0x14) // 0xe0004014  Message sent to the clients of the device's hub parent, when a device causes an low power notice to be displayed.  The message argument contains the locationID of the device
-#define kUSBHostMessageEndpointCountExceeded          iokit_usblegacy_err_msg(0x19) // 0xe0004019  Message sent to a device when endpoints cannot be created because the USB controller ran out of resources
-#define kUSBHostMessageDeviceCountExceeded            iokit_usblegacy_err_msg(0x1a) // 0xe000401a  Message sent by a hub when a device cannot be enumerated because the USB controller ran out of resources
-#define kUSBHostMessageUnsupportedConfiguration       iokit_usblegacy_err_msg(0x1c) // 0xe000401c  Message sent to the clients of the device when a device is not supported in the current configuration.  The message argument contains the locationID of the device
-#define kUSBHostMessageHubCountExceeded               iokit_usblegacy_err_msg(0x1d) // 0xe000401d  Message sent when a 6th hub was plugged in and was not enumerated, as the USB spec only support 5 hubs in a chain
-#define kUSBHostMessageTDMLowBattery                  iokit_usblegacy_err_msg(0x1e) // 0xe000401e  Message sent when when an attached TDM system battery is running low.
-
-/*!
- @defined IOUSBHostFamily error codes
- @discussion  Errors specific to the IOUSBHostFamily.  Note that the iokit_usb_err(x) translates to 0xe0004xxx, where xxx is the value in parenthesis as a hex number.
- */
-#define iokit_usbhost_err(message) ((IOReturn)(iokit_family_err(sub_iokit_usb, iokit_usbhost_group | (message & iokit_usb_codemask))))
+#define kUSBHostMessageOvercurrentCondition           iokit_usblegacy_err_msg(0x13) // 0xe0004013  Apple Internal use only.  Message sent to the clients of the device's hub parent, when a device causes an overcurrent condition.  The message argument contains the locationID of the device
+#define kUSBHostMessageNotEnoughPower                 iokit_usblegacy_err_msg(0x14) // 0xe0004014  Apple Internal use only.  Message sent to the clients of the device's hub parent, when a device causes an low power notice to be displayed.  The message argument contains the locationID of the device
+#define kUSBHostMessageEndpointCountExceeded          iokit_usblegacy_err_msg(0x19) // 0xe0004019  Apple Internal use only.  Message sent to a device when endpoints cannot be created because the USB controller ran out of resources
+#define kUSBHostMessageDeviceCountExceeded            iokit_usblegacy_err_msg(0x1a) // 0xe000401a  Apple Internal use only.  Message sent by a hub when a device cannot be enumerated because the USB controller ran out of resources
+#define kUSBHostMessageUnsupportedConfiguration       iokit_usblegacy_err_msg(0x1c) // 0xe000401c  Apple Internal use only.  Message sent to the clients of the device when a device is not supported in the current configuration.  The message argument contains the locationID of the device
+#define kUSBHostMessageHubCountExceeded               iokit_usblegacy_err_msg(0x1d) // 0xe000401d  Apple Internal use only.  Message sent when a 6th hub was plugged in and was not enumerated, as the USB spec only support 5 hubs in a chain
+#define kUSBHostMessageTDMLowBattery                  iokit_usblegacy_err_msg(0x1e) // 0xe000401e  Apple Internal use only.  Message sent when when an attached TDM system battery is running low.
+/*! @/definedblock */
 
 #define kUSBHostReturnPipeStalled   iokit_usbhost_err(0x0)  // 0xe0005000  Pipe has issued a STALL handshake.  Use clearStall to clear this condition.
 #define kUSBHostReturnNoPower       iokit_usbhost_err(0x1)  // 0xe0005001  A setConfiguration call was not able to succeed because all configurations require more power than is available.
@@ -227,8 +314,8 @@
 };
 
 /*!
- @enum Default control request timeout values in milliseconds
- @discussion default values used for data and completion timeouts.
+ @enum tUSBHostDefaultControlRequestTimeout
+ @brief Default control request timeout values in milliseconds
  */
 enum
 {
@@ -363,6 +450,7 @@
 #define kUSBHostControllerPropertyFullSpeedCompanion            "kUSBFullSpeedCompanion"                // OSBoolean false to disable full-speed companion controller
 #define kUSBHostControllerPropertyHighSpeedCompanion            "kUSBHighSpeedCompanion"                // OSBoolean false to disable high-speed companion controller
 #define kUSBHostControllerPropertySuperSpeedCompanion           "kUSBSuperSpeedCompanion"               // OSBoolean false to disable superspeed companion controller
+#define kUSBHostControllerPropertyRevision                      "Revision"                              // OSData    Major/minor revision number of controller
 
 #define kUSBHostPortPropertyExternalDeviceResetController       "kUSBHostPortExternalDeviceResetController"
 #define kUSBHostPortPropertyExternalDevicePowerController       "kUSBHostPortExternalDevicePowerController"
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostHIDDevice.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostHIDDevice.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostHIDDevice.h	2016-06-29 01:13:52.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostHIDDevice.h	2016-07-10 09:03:26.000000000 +0200
@@ -99,6 +99,8 @@
 
 #define kUSBHID_IoIdleTimeout "I/O Idle Timeout"
 
+#define kUSBHostHIDDevicePropertyIdlePolicy "kUSBHIDDeviceIdlePolicy"
+
 /*!
  @typedef IOUSBHostHIDDescriptor
  @discussion USB HID Descriptor.  See the USB HID Specification at <a href="http://www.usb.org"TARGET="_blank">http://www.usb.org</a>.  (This structure
@@ -213,6 +215,20 @@
     virtual void stop (IOService *provider);
     
     virtual void free (void);
+
+    virtual bool setProperty(const OSSymbol* aKey, OSObject* anObject);
+
+    virtual bool setProperty(const OSString* aKey, OSObject* anObject);
+
+    virtual bool setProperty(const char* aKey, OSObject* anObject);
+
+    virtual bool setProperty(const char* aKey, const char * aString);
+
+    virtual bool setProperty(const char* aKey, bool aBoolean);
+
+    virtual bool setProperty(const char* aKey, unsigned long long aValue, unsigned int aNumberOfBits);
+
+    virtual bool setProperty(const char* aKey, void* bytes, unsigned int length);
     
     
     // IOHIDDevice Methods
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostIOSource.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostIOSource.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostIOSource.h	2016-06-29 01:13:25.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostIOSource.h	2016-07-10 09:02:55.000000000 +0200
@@ -1,15 +1,34 @@
-//
-//  IOUSBHostIOSource.h
-//  IOUSBHostFamily
-//
-//  Created by Dan Wilson on 2/17/14.
-//
-//
+/*
+ * Copyright (c) 1998-2016 Apple Inc. All rights reserved.
+ *
+ * @APPLE_OSREFERENCE_LICENSE_HEADER_START@
+ *
+ * This file contains Original Code and/or Modifications of Original Code
+ * as defined in and that are subject to the Apple Public Source License
+ * Version 2.0 (the 'License'). You may not use this file except in
+ * compliance with the License. The rights granted to you under the License
+ * may not be used to create, or enable the creation or redistribution of,
+ * unlawful or unlicensed copies of an Apple operating system, or to
+ * circumvent, violate, or enable the circumvention or violation of, any
+ * terms of an Apple operating system software license agreement.
+ *
+ * Please obtain a copy of the License at
+ * http://www.opensource.apple.com/apsl/ and read it before using this file.
+ *
+ * The Original Code and all software distributed under the License are
+ * distributed on an 'AS IS' basis, WITHOUT WARRANTY OF ANY KIND, EITHER
+ * EXPRESS OR IMPLIED, AND APPLE HEREBY DISCLAIMS ALL SUCH WARRANTIES,
+ * INCLUDING WITHOUT LIMITATION, ANY WARRANTIES OF MERCHANTABILITY,
+ * FITNESS FOR A PARTICULAR PURPOSE, QUIET ENJOYMENT OR NON-INFRINGEMENT.
+ * Please see the License for the specific language governing rights and
+ * limitations under the License.
+ *
+ * @APPLE_OSREFERENCE_LICENSE_HEADER_END@
+ */
 
 /*!
- * @header IOUSBHostIOSource.h
- *
- * @brief Provides IOUSBHostIOSource API
+ @header     IOUSBHostIOSource.h
+ @brief      IOUSBHostIOSource is the base class for objects that perform USB IO.
  */
 
 #ifndef IOUSBHostFamily_IOUSBHostIOSource_h
@@ -26,6 +45,14 @@
 class AppleUSBHostRequestPool;
 
 typedef void (*IOUSBHostCompletionAction)(void* owner, void* parameter, IOReturn status, uint32_t bytesTransferred);
+
+/*!
+ * @struct      IOUSBHostCompletion
+ * @discussion  Struture describing the completion callback for an asynchronous bulk, control, or interrupt IO operation
+ * @field       owner Pointer to an object that owns the transfer.  May be used as <code>this</code> for an action passed via OSMemberFunctionCast.
+ * @field       action IOUSBHostCompletionAction to run when the IO request completes.
+ * @field       parameter Pointer to be used as context within the completion action.
+ */
 struct IOUSBHostCompletion
 {
     void* owner;
@@ -34,15 +61,12 @@
 };
 
 /*!
- * @typedef IOUSBHostIsochronousFrame
- * @discussion Structure representing a single frame in an isochronous transfer.
- * @param status Completion status for this individual frame.  IOUSBHostFamily will initialize this to kIOReturnInvalid
- * and will update the field with a valid status code upon completion of the frame.
- * @param requestCount The number of bytes requested to transfer for this frame.  This field must be initialized by the caller
- * before this structure is submitted to IOUSBHostFamily.
- * @param completeCount The number of bytes actually transferred for this frame.  IOUSBHostFamily will update this field
- * upon completion of the frame.
- * @param timeStamp The observed AbsoluteTime for this frame's completion.
+ * @struct      IOUSBHostIsochronousFrame
+ * @discussion  Structure representing a single frame in an isochronous transfer.
+ * @field       status Completion status for this individual frame.  IOUSBHostFamily will initialize this to kIOReturnInvalid and will update the field with a valid status code upon completion of the frame.
+ * @field       requestCount The number of bytes requested to transfer for this frame.  This field must be initialized by the caller before this structure is submitted to IOUSBHostFamily.
+ * @field       completeCount The number of bytes actually transferred for this frame.  IOUSBHostFamily will update this field upon completion of the frame.
+ * @field       timeStamp The observed AbsoluteTime for this frame's completion.  Note that interrupt latency and system load may result in more than one frame completing with the same timestamp.
  */
 struct IOUSBHostIsochronousFrame
 {
@@ -53,6 +77,14 @@
 };
 
 typedef void (*IOUSBHostIsochronousCompletionAction)(void* owner, void* parameter, IOReturn status, IOUSBHostIsochronousFrame* frameList);
+
+/*!
+ * @struct      IOUSBHostIsochronousCompletion
+ * @discussion  Struture describing the completion callback for an asynchronous isochronous operation
+ * @field       owner Pointer to an object that owns the transfer.  May be used as <code>this</code> for an action passed via OSMemberFunctionCast.
+ * @field       action IOUSBHostIsochronousCompletionAction to run when the IO request completes.
+ * @field       parameter Pointer to be used as context within the completion action.
+ */
 struct IOUSBHostIsochronousCompletion
 {
     void* owner;
@@ -61,11 +93,9 @@
 };
 
 /*!
- * @class IOUSBHostIOSource
- *
- * @brief IOUSBHostIOSource object
- *
- * @discussion Provides the base class API for controlling pipe policy and performing I/O.
+ * @class       IOUSBHostIOSource
+ * @brief       The base class for objects that perform USB IO.
+ * @discussion  This class provides functionality to transfer data across USB.  Function drivers should not subclass IOUSBHostIOSource.
  */
 class IOUSBHostIOSource : public OSObject
 {
@@ -101,12 +131,13 @@
     
 public:
     /*!
-     * @brief Return value for <code>getState()</code>
-     *
-     * @constant kStateReady The I/O source is idle and fully-functional.
-     * @constant kStateRunningCompletions The I/O source is currently running completions.
-     * @constant kStateAborting The I/O source is currently aborting all requests.
-     * @constant kStateInactive The I/O source has been closed.
+     * @enum        tState
+     * @namespace   IOUSBHostIOSource
+     * @brief       Return value for <code>getState()</code>
+     * @constant    kStateReady The I/O source is idle and fully-functional.
+     * @constant    kStateRunningCompletions The I/O source is currently running completions.
+     * @constant    kStateAborting The I/O source is currently aborting all requests.
+     * @constant    kStateInactive The I/O source has been closed.
      */
     enum tState
     {
@@ -118,17 +149,16 @@
     };
 
     /*!
-     * @brief Returns the current state of the I/O source.
-     *
-     * @return @link tState @/link
+     * @brief   Returns the current state of the I/O source.
+     * @return  @link tState @/link
      */
     virtual tState getState();
 
     /*!
-     * @brief Options for <code>abort()</code>
-     *
-     * @constant kAbortAsynchronous the abort should occur asynchronously.
-     * @constant kAbortSynchronous the abort should occur synchronously.
+     * @enum        tAbortOptions
+     * @brief       Options for <code>abort()</code>
+     * @constant    kAbortAsynchronous abort() should return immediately without waiting for the aborted IO to complete
+     * @constant    kAbortSynchronous abort() should not return until the aborted IO has completed
      */
     enum tAbortOptions
     {
@@ -137,20 +167,12 @@
     };
 
     /*!
-     * @brief Abort pending I/O requests.
-     *
-     * @discussion This method will abort all pending I/O requests.  If <code>options</code> is  <code>kAbortSynchronous</code>
-     * this method will block any new requests that are not submitted from one of the aborted request's callback until the abort
-     * completes.
-     *
-     * @param options Whether the abort operation should be synchronous or not.
-     *
-     * @param withError Error code which will be passed to any request which hasn't successfully completed.
-     *
-     * @param forClient Service for which to abort requests.  If NULL, all requests will be aborted.  Only control endpoints can
-     * specify a non-NULL value.
-     *
-     * @return IOReturn result code
+     * @brief       Abort pending I/O requests.
+     * @discussion  This method will abort all pending I/O requests.  If <code>options</code> includes <code>kAbortSynchronous</code>, this method will block any new IO requests unless they are submitted from an aborted IO's completion routine.
+     * @param       options tAbortOptions
+     * @param       withError IOReturn error value to return with the requests.  The default value of kIOReturnAborted should be used.
+     * @param       forClient Service for which to abort requests.  If NULL, all requests will be aborted.  Only control endpoints can specify a non-NULL value.
+     * @return      IOReturn result code
      */
     virtual IOReturn abort(IOOptionBits options = kAbortAsynchronous, IOReturn withError = kIOReturnAborted, IOService* forClient = NULL);
     
@@ -214,43 +236,24 @@
 #pragma mark IO
 public:
     /*!
-     * @brief Issue an asynchronous I/O request on the source.
-     *
-     * @discussion This method is used to issue an asynchronous I/O request on a bulk or interrupt pipe.
-     *
-     * See IOUSBHostPipe::io and IOUSBHostStream::io for object-specific interface notes.
-     *
-     * @param dataBuffer Pointer to a valid memory descriptor to use as the backing store for the I/O.
-     *
-     * @param dataBufferLength Length of the request.  Must be >= <code>dataBuffer->getLength()</code>
-     *
-     * @param completion Pointer to a valid, non NULL, IOUSBHostCompletion object.  This will be copied and can therefore be stack-allocated.
-     *
-     * @param completionTimeoutMs Timeout of the request in milliseconds.  If 0, the request will never timeout.
-     * Must be 0 for interrupt pipes and streams.
-     *
-     * @return IOReturn result code
+     * @brief       Enqueue an IO request on the source
+     * @discussion  This method is used to issue an asynchronous I/O request on a bulk or interrupt pipe.  See IOUSBHostPipe::io and IOUSBHostStream::io for object-specific interface notes.
+     * @param       dataBuffer IOMemoryDescriptor pointer containing the buffer to use for the transfer
+     * @param       dataBufferLength Length of the request.  Must be <= <code>dataBuffer->getLength()</code>
+     * @param       completion Pointer to a IOUSBHostCompletion structure.  This will be copied and can therefore be stack-allocated.
+     * @param       completionTimeoutMs Timeout of the request in milliseconds.  If 0, the request will never timeout.  Must be 0 for interrupt pipes and streams.
+     * @return      kIOReuturnSuccess if the completion will be called in the future, otherwise error
      */
     virtual IOReturn io(IOMemoryDescriptor* dataBuffer, uint32_t dataBufferLength, IOUSBHostCompletion* completion, uint32_t completionTimeoutMs = 0);
     
     /*!
-     * @brief Issue a synchronous I/O request on the source.
-     *
-     * @discussion This method is used to issue a synchronous I/O request on a bulk or interrupt pipe.  Although this
-     * is a synchronous call, it is permitted to be called from the completion callback of an asynchronous request.
-     *
-     * See IOUSBHostPipe::io and IOUSBHostStream::io for object-specific interface notes.
-     *
-     * @param dataBuffer Pointer to the memory to be used for the I/O.
-     *
-     * @param dataBufferLength Length of the request.  Must be >= the amount of memory allocated to <code>dataBuffer</code>
-     *
-     * @param bytesTransferred Reference which will be updated with the bytes transferred during the request.
-     *
-     * @param completionTimeoutMs Timeout of the request in milliseconds.  If 0, the request will never timeout.
-     * Must be 0 for interrupt pipes and streams.
-     *
-     * @return IOReturn result code
+     * @brief       Perform an IO request on the source
+     * @discussion  This method will send a synchronous request on the IO source, and will not return until the request is complete.  This method will acquire the service's workloop lock, and will call commandSleep to send the request.  See IOUSBHostPipe::io and IOUSBHostStream::io for object-specific interface notes.
+     * @param       dataBuffer IOMemoryDescriptor pointer containing the buffer to use for the transfer
+     * @param       dataBufferLength Length of the request.  Must be <= <code>dataBuffer->getLength()</code>
+     * @param       bytesTransferred uint32_t reference which will be updated with the bytes transferred during the request
+     * @param       completionTimeoutMs Timeout of the request in milliseconds.  If 0, the request will never timeout.  Must be 0 for interrupt pipes and streams.
+     * @return      IOReturn value indicating the result of the IO request
      */
     virtual IOReturn io(IOMemoryDescriptor* dataBuffer, uint32_t dataBufferLength, uint32_t& bytesTransferred, uint32_t completionTimeoutMs = 0);
     
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostInterface.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostInterface.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostInterface.h	2016-06-29 01:13:25.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostInterface.h	2016-07-10 09:02:55.000000000 +0200
@@ -1,14 +1,19 @@
 /*
- * Copyright (c) 1998-2007 Apple Inc. All rights reserved.
+ * Copyright (c) 1998-2016 Apple Inc. All rights reserved.
  *
- * @APPLE_LICENSE_HEADER_START@
+ * @APPLE_OSREFERENCE_LICENSE_HEADER_START@
  *
  * This file contains Original Code and/or Modifications of Original Code
  * as defined in and that are subject to the Apple Public Source License
  * Version 2.0 (the 'License'). You may not use this file except in
- * compliance with the License. Please obtain a copy of the License at
- * http://www.opensource.apple.com/apsl/ and read it before using this
- * file.
+ * compliance with the License. The rights granted to you under the License
+ * may not be used to create, or enable the creation or redistribution of,
+ * unlawful or unlicensed copies of an Apple operating system, or to
+ * circumvent, violate, or enable the circumvention or violation of, any
+ * terms of an Apple operating system software license agreement.
+ *
+ * Please obtain a copy of the License at
+ * http://www.opensource.apple.com/apsl/ and read it before using this file.
  *
  * The Original Code and all software distributed under the License are
  * distributed on an 'AS IS' basis, WITHOUT WARRANTY OF ANY KIND, EITHER
@@ -18,13 +23,130 @@
  * Please see the License for the specific language governing rights and
  * limitations under the License.
  *
- * @APPLE_LICENSE_HEADER_END@
+ * @APPLE_OSREFERENCE_LICENSE_HEADER_END@
  */
 
 /*!
- * @header IOUSBHostInterface.h
- *
- * @brief Provides IOUSBHostInterface API
+ @header     IOUSBHostInterface.h
+ @brief      IOUSBHostInterface is an IOService representing a USB interface.
+ @discussion
+ 
+ <h3>Session Management</h3>
+ 
+ A driver that has successfully matched on an IOUSBHostInterface is able to take ownership of the interface by calling the <code>open</code> method defined by IOService on the IOUSBHostInterface.  Once <code>open</code> has completed successfully, the driver has an open session, and may use the deviceRequest interface to send control requests, the selectAlternateSetting interface to change the endpoints and behavior of the interface.
+ 
+ When the driver is finished with control of the IOUSBHostInterface, it must call <code>close</code> to end its session.  Calling <code>close</code> will synchronously abort that session's outstanding IO on the control endpoint.  If the interface is terminating for any reason, such as the device being unplugged, termination of the IOUSBHostInterface will be blocked until the driver calls <code>close</code>.  The willTerminate call into the driver is the recommended location to call <code>close</code>.
+ 
+ <h3>deviceRequest Interface</h3>
+ 
+ The <code>deviceRequest</code> methods are used to send control requests to the device's default endpoint.  The <code>deviceRequest</code> methods may not be used for the following standard requests:
+ <ul>
+    <li>CLEAR_FEATURE ENDPOINT_HALT (USB 2.0 9.4.1) - Use <code>IOUSBHostPipe::clearStall</code> to send this request</li>
+    <li>SET_ADDRESS (USB 2.0 9.4.6)</li>
+    <li>SET_CONFIGURATION (USB 2.0 9.4.7) - Use <code>setConfiguration</code> to send this request</li>
+    <li>SET_INTERFACE (USB 2.0 9.4.10) - Use <code>IOUSBHostInterface::selectAlternateSetting</code> to send this request</li>
+ </ul>
+ 
+ <h3>IOUSBInterface Migration</h3>
+ 
+ IOUSBHostInterface serves as a replacement for IOUSBInterface.  Clients that previously matched on IOUSBInterface can use the following guide to convert to IOUSBHostInterface.
+ 
+ <code>virtual const IOUSBInterfaceDescriptor* IOUSBInterface::FindNextAltInterface(const IOUSBInterfaceDescriptor*, IOUSBFindInterfaceRequest*);</code><br>
+ Replacement: <code>StandardUSB::getNextInterfaceDescriptor(...);</code>
+ 
+ <code>virtual IOUSBPipe* IOUSBInterface::FindNextPipe(IOUSBHostPipe*, IOUSBFindEndpointRequest*);<br>
+ virtual IOUSBPipe* IOUSBInterface::FindNextPipe(IOUSBHostPipe*, IOUSBFindEndpointRequest*, bool);</code><br>
+ Replacement: 
+ <pre>const EndpointDescriptor* endpointCandidate = NULL;
+IOUSBHostPipe* foundPipe = NULL;
+while((endpointCandidate = StandardUSB::getNextAssociatedDescriptorWithType(getConfigurationDescriptor(), getInterfaceDescriptor(), endpointCandidate, kDescriptorTypeEndpoint)) != NULL)
+{
+   if(endpointCandidate->bEndpointAddress == desiredAddress>)
+   {
+       foundPipe = copyPipe(StandardUSB::getEndpointAddress(endpointCandidate));
+       break;
+   }
+}</pre>
+ 
+ <code>virtual const IOUSBDescriptorHeader* IOUSBInterface::FindNextAssociatedDescriptor(const void*, UInt8);</code><br>
+ Replacement: <code>StandardUSB::getNextAssociatedDescriptorWithType(getConfigurationDescriptor(), getInterfaceDescriptor(), currentDescriptor, type);</code>
+ 
+ <code>virtual IOReturn IOUSBInterface::SetAlternateInterface(IOService*, UInt16);
+ Replacement: <code>selectAlternateSetting(...);</code>
+ 
+ <code>virtual IOUSBHostPipe* IOUSBInterface::GetPipeObj(UInt8);<br>
+ virtual IOUSBHostPipe* IOUSBInterface::GetPipeObjRetain(UInt8);</code><br>
+ Replacement: <code>copyPipe(endpointAddress);</code><br>
+ Note that <code>copyPipe</code> behaves like <code>GetPipeObjRetain</code>, and the returned pipe must be released by the caller during termination.
+ 
+ <code>virtual UInt8 IOUSBInterface::GetConfigValue();</code><br>
+ Replacement: <code>getConfigurationDescriptor()->bConfigurationValue;</code>
+ 
+ <code>virtual IOUSBHostDevice* IOUSBInterface::GetDevice();</code><br>
+ Replacement: 
+ <pre>// Function drivers should not assume the immediate provider of an IOUSBHostInterface is an IOUSBHostDevice.
+IOService* deviceCandidate = getProvider();
+IOUSBHostDevice* device = NULL;
+while(deviceCandidate != NULL)
+{
+    device = OSDynamicCast(IOUSBHostDevice, deviceCandidate);
+    if(device != NULL)
+    {
+        break;
+    }
+ 
+    deviceCandidate = deviceCandidate->getProvider();
+}</pre>
+
+ <code>virtual UInt8 IOUSBInterface::GetInterfaceNumber();</code><br>
+ Replacement: <code>getInterfaceDescriptor()->bInterfaceNumber;</code>
+ 
+ <code>virtual UInt8 IOUSBInterface::GetAlternateSetting();</code><br>
+ Replacement: <code>getInterfaceDescriptor()->bAlternateSetting;</code>
+ 
+ <code>virtual UInt8 IOUSBInterface::GetNumEndpoints();</code><br>
+ Replacement: <code>getInterfaceDescriptor()->bNumEndpoints;</code>
+ 
+ <code>virtual UInt8 IOUSBInterface::GetInterfaceClass();</code><br>
+ Replacement: <code>getInterfaceDescriptor()->bInterfaceClass;</code>
+ 
+ <code>virtual UInt8 IOUSBInterface::GetInterfaceSubClass();</code><br>
+ Replacement: <code>getInterfaceDescriptor()->bInterfaceSubClass;</code>
+
+ <code>virtual UInt8 IOUSBInterface::GetInterfaceProtocol();</code><br>
+ Replacement: <code>getInterfaceDescriptor()->bInterfaceProtocol;</code>
+
+ <code>virtual UInt8 IOUSBInterface::GetInterfaceStringIndex();</code><br>
+ Replacement: <code>getInterfaceDescriptor()->iInterface;</code>
+ 
+ <code>virtual IOReturn IOUSBInterface::DeviceRequest(IOUSBDevRequest* request, IOUSBCompletion* completion = 0);<br>
+ virtual IOReturn IOUSBInterface::DeviceRequest(IOUSBDevRequestDesc* request, IOUSBCompletion* completion = 0);</code><br>
+ Replacement: <code>deviceRequest(...)</code>
+ 
+ <code>virtual IOReturn IOUSBInterface::GetEndpointProperties(UInt8 alternateSetting, UInt8 endpointNumber, UInt8 direction, UInt8* transferType, UInt16* maxPacketSize, UInt8* interval);<br>
+ virtual IOReturn GetEndpointPropertiesV3(IOUSBEndpointProperties*);</code><br>
+ Replacement: Use <code>StandardUSB::getEndpoint*</code> methods to retrieve endpoint properties.
+
+ <code>virtual IOReturn RememberStreams();</code><br>
+ Replacement: none
+
+ <code>virtual IOReturn RecreateStreams();</code><br>
+ Replacement: none
+
+ <code>virtual void UnlinkPipes();</code><br>
+ Replacement: none
+
+ <code>virtual void ReopenPipes();</code><br>
+ Replacement: none
+
+ <code>virtual IOReturn GetInterfaceStatus(USBStatus*);</code><br>
+ Replacement: Use <code>deviceRequest(...)</code> to manually craft the control request.
+
+ <code>virtual IOReturn SetFunctionSuspendFeature(UInt8);</code><br>
+ Replacement: It is not recommended for function drivers to send this request.
+
+ <code>virtual IOReturn EnableRemoteWake(bool);</code><br>
+ Replacement: Use <code>deviceRequest(...)</code> to manually craft the control request.  <code>IOUSBHostDevice::setConfiguration</code> will automatically enable remote wake if the descriptors indicate it is supported.
  */
 
 #ifndef IOUSBHostFamily_IOUSBHostInterface_h
@@ -39,18 +161,22 @@
 class IOSimpleReporter;
 
 /*!
- * @class IOUSBHostInterface
- *
- * @abstract The object representing an interface of a device on the USB bus.
- *
- * @discussion This class provides functionality to find the pipes of an interface and to read the descriptors associated
- * with an interface. When an interface is open()ed,  all its pipes are created.
+ * @class       IOUSBHostInterface
+ * @brief       The IOService object representing a USB interface
+ * @discussion  This class provides functionality to send control requests to the default control endpoint, as well as create IOUSBHostPipe objects to transfer data.  Function drivers should not subclass IOUSBHostInterface.
  */
 class IOUSBHostInterface : public IOService
 {
     OSDeclareDefaultStructors(IOUSBHostInterface)
 
 public:
+    /*
+     * @brief       Factory method for creating an IOUSBHostInterface object
+     * @discussion  This method should not be called by function drivers.  To create an IOUSBHostInterface, use IOUSBHostDevice::setConfiguration(...)
+     * @param       configurationDescriptor Descriptor for the configuration this interface belongs to
+     * @param       interfaceDescriptor Descriptor for this interface's default alt setting
+     * @return      Pointer to an IOUSBHostInterface object if successful, otherwise NULL
+     */
     static IOUSBHostInterface* withDescriptors(const StandardUSB::ConfigurationDescriptor* configurationDescriptor, const StandardUSB::InterfaceDescriptor* interfaceDescriptor);
 
 protected:
@@ -70,6 +196,7 @@
 
 #pragma mark IOService overrides
 public:
+    // The following methods, with the notable exception of <code>open</code> and <code>close</code> should be considered private and should not be called by function drivers.  For a discussion of proper usage for <code>open</code> and <code>close</code>, see the discussion of "Session Management" above.
     virtual bool        attach(IOService* provider);
     virtual bool        start(IOService* provider);
     virtual bool        terminate(IOOptionBits options = 0);
@@ -84,7 +211,25 @@
     {
         kOpenOptionsSelectAlternateInterface = StandardUSBBit(16)
     };
+
+    /*! @functiongroup IOService overrides */
+
+    /*!
+     * @brief       Open a session to the IOUSBHostInterface
+     * @discussion  This method opens a session to an IOUSBHostInterface.  It will acquire the service's workloop lock.  Only one service may open a session at a time.
+     * @param       forClient The IOService that is opening a session.
+     * @param       options See IOService.h, <code>kOpenOptionsSelectAlternateInterface</code> in the options mask will immediately select the alternate setting passed by value through the <code>arg</code> parameter
+     * @param       arg See IOService.h, or the value of the alt setting to use if <code>kOpenOptionsSelectAlternateInterface</code> is included in the options mask
+     * @return      bool true if the session could be opened, otherwise false.
+     */
     virtual bool        open(IOService* forClient, IOOptionBits options = 0, void* arg = 0);
+    
+    /*!
+     * @brief       Close a session to the IOUSBHostInterface
+     * @discussion  This method closes an open session to an IOUSBHostInterface.  It will acquire the service's workloop lock, abort any IO for the interface and its endpoints, and may call commandSleep to allow processing of aborted IO before returning.
+     * @param       forClient The IOService that is closing its session.
+     * @param       options See IOService.h
+     */
     virtual void        close(IOService* forClient, IOOptionBits options = 0);
     
     virtual IOReturn    message(UInt32 type, IOService* provider,  void* argument = 0);
@@ -93,7 +238,7 @@
     virtual IOReturn updateReport(IOReportChannelList*channels, IOReportUpdateAction action, void* result, void* destination);
 
     virtual const char* stringFromReturn(IOReturn code);
-    
+
 protected:
     virtual IOReturn openGated(IOService* forClient, IOOptionBits options, void* arg);
     virtual IOReturn closeGated(IOService* forClient, IOOptionBits options);
@@ -116,21 +261,19 @@
 
 #pragma mark Power management
 public:
+    /*! @functiongroup Power management */
+
     /*!
-     * @brief Sets the desired idle policy for the device
-     *
-     * @discussion TODO talk about device idleness, largest deviceIdleTimeout wins etc
-     *
-     * @param deviceIdleTimeout The amount of time, in milliseconds, after all pipes are idle to wait before suspending the device.
-     *
-     * @return IOReturn result code
+     * @brief       Sets the desired idle suspend timeout for the interface
+     * @discussion  Once the interface is considered idle, it will defer electrical suspend of the device for the specified duration.  For a more complete discussion of idle policies, refer to "Idle suspend" in IOUSBHostFamily.h.
+     * @param       deviceIdleTimeout The amount of time, in milliseconds, after all pipes are idle to wait before suspending the device.
+     * @return     IOReturn result code
      */
     virtual IOReturn setIdlePolicy(uint32_t deviceIdleTimeout);
     
     /*!
-     * @brief Returns the current device idle timeout.  See @link IOUSBHostInterface::setIdlePolicy @/link
-     *
-     * @return The amount of time, in milliseconds, after all pipes are idle to wait before suspending the device,
+     * @brief       Retrieve the current idle suspend timeout.  See @link setIdlePolicy @/link
+     * @return      The amount of time, in milliseconds, after all pipes are idle to wait before suspending the device,
      */
     virtual uint32_t getIdlePolicy();
     
@@ -164,32 +307,26 @@
     
 #pragma mark Descriptors
 public:
+    /*! @functiongroup Descriptors */
+
     /*!
-     * @brief Return the configuration descriptor in which this interface is defined
-     *
-     * @return Pointer to the configuration descriptor
+     * @brief       Retrieve the configuration descriptor in which this interface is defined
+     * @return      ConfigurationDescriptor pointer
      */
     virtual const StandardUSB::ConfigurationDescriptor* getConfigurationDescriptor();
     
     /*!
-     * @brief Return the interface descriptor associated with this interface
-     *
-     * @return Pointer to the interface descriptor for this interface
+     * @brief       Retrieve the interface descriptor associated with this interface
+     * @return      InterfaceDescriptor pointer
      */
     virtual const StandardUSB::InterfaceDescriptor* getInterfaceDescriptor();
     
     /*!
-     * @brief Return a string descriptor from the device
-     *
-     * @discussion This method is simply a convenience method to retieve the desired string descriptor.
-     *
-     * @param index  Descriptor index value.  Low byte of <code>wValue</code> of the GET_DESCRIPTOR control request described
-     * in section 9.4.3 of the USB 2.0 specification.
-     *
-     * @param languageID  Descriptor language ID.  <code>wIndex</code> of the GET_DESCRIPTOR control request described in
-     * section 9.4.3 of the USB 2.0 specification.
-     *
-     * @return Pointer to the descriptor if found
+     * @brief       Return a string descriptor from the device
+     * @discussion  This method uses IOUSBHostDevice::getDescriptor to return a string descriptor.
+     * @param       index Descriptor index value.  Low byte of <code>wValue</code> of the SET_DESCRIPTOR control request (USB 2.0 9.4.8).
+     * @param       languageID Descriptor language ID.  <code>wIndex</code> of the SET_DESCRIPTOR control request (USB 2.0 9.4.8).     *
+     * @return      Pointer to the descriptor if found
      */
     virtual const StandardUSB::StringDescriptor* getStringDescriptor(uint8_t index, uint16_t languageID = StandardUSB::kLanguageIDEnglishUS);
     
@@ -222,155 +359,54 @@
     
 #pragma mark Alternate setting and pipe management
 public:
+    /*! @functiongroup Alternate setting and pipe management */
+
     /*!
-     * @brief Select an alternate setting for this interface
-     *
-     * @discussion This method is used to select an alternate setting for the interface.  All open pipes will be closed and
-     * the new alternate setting will be selected via SET_INTERFACE control request (see section 9.4.10 of the USB 2.0
-     * specification).  If the alternate setting was successfully selected, the interface will be re-registered for matching
-     *
-     * @param bAlternateSetting Alternate interface number to activate
-     *
-     * @return IOReturn result code
+     * @brief       Select an alternate setting for this interface
+     * @discussion  This method is used to select an alternate setting for the interface.  All pending IO on the interface's pipes will be aborted, and the open pipes will be closed.  The new alternate setting will be selected via SET_INTERFACE control request (USB 2.0 9.4.10).
+     * @param       bAlternateSetting Alternate interface number to activate
+     * @return      IOReturn result code
      */
     virtual IOReturn selectAlternateSetting(uint8_t bAlternateSetting);
     
     /*!
-     * @brief Return the pipe whose <code>bEndpointAddress</code> matches <code>address</code>
-     *
-     * @discussion This method will return the pipe whose <code>bEndpointAddress</code> matches <code>address</code>.  If
-     * the pipe doesn't exist yet, but is part of the interface, it will first be created.  This method returns a
-     * <code>retain()</code>ed object that must be <code>release()</code>ed by the caller.
-     *
-     * @param address Address of the pipe
-     *
-     * @return Pointer to a retain()ed IOUSBHostPipe object or NULL
+     * @brief       Return the pipe whose <code>bEndpointAddress</code> matches <code>address</code>
+     * @discussion  This method will return the pipe whose <code>bEndpointAddress</code> matches <code>address</code>.  If the pipe doesn't exist yet, but is part of the interface, it will first be created.  The caller must release the IOUSBHostPipe when finished using it.
+     * @param       address Address of the pipe
+     * @return      Pointer to a retain()ed IOUSBHostPipe object or NULL
      */
     virtual IOUSBHostPipe* copyPipe(uint8_t address);
     
     /*!
-     * @brief Issue an aynchronous setup request on the default control pipe
-     *
-     * @discussion This method will issue an asynchronous control request on the defaul pipe.
-     *
-     * <pre>
-     * @textblock
-     * The following request types are reserved and cannot be made as generic control requests, the appropriate API call should be used instead.
-     *
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientDevice), kDeviceRequestSetAddress � reserved, this request cannot be sent by drivers.
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientDevice), kDeviceRequestSetConfiguration � see setConfiguration().
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientInterface), kDeviceRequestSetInterface � see IOUSBHostInterface::selectAlternateSetting().
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientEndpoint), kRequestRecipientEndpoint � see IOUSBHostPipe::clearStall().
-     *
-     * @/textblock
-     * </pre>
-     *
-     * @param request Reference to a valid StandardUSB::DeviceRequest object.  This will be copied and can therefore be stack-allocated.
-     *
-     * @param dataBuffer Pointer to the memory to be used for the I/O.
-     *
-     * @param completion Pointer to a valid, non NULL, IOUSBHostCompletion object.  This will be copied and can therefore be stack-allocated.
-     *
-     * @param completionTimeoutMs Time-out of the request in milliseconds.  If 0, the request will never time-out.
-     *
-     * @return IOReturn result code
+     * @brief       Enqueue a request on the default control endpoint
+     * @discussion  This method will enqueue an asynchronous request on the default control endpoint.  If successful, the provided completion routine will be called to report the status of the completed IO.
+     * @param       request Reference to a valid StandardUSB::DeviceRequest structure.  The structure is copied and can therefore be stack-allocated.
+     * @param       dataBuffer A void* or IOMemoryDescriptor* defining the memory to use for the request's data phase.
+     * @param       completion Pointer to a IOUSBHostCompletion structure.  This will be copied and can therefore be stack-allocated.
+     * @param       completionTimeoutMs Timeout of the request in milliseconds.  If 0, the request will never timeout.
+     * @return      kIOReuturnSuccess if the completion will be called in the future, otherwise error
      */
     virtual IOReturn deviceRequest(StandardUSB::DeviceRequest& request, void* dataBuffer, IOUSBHostCompletion* completion, uint32_t completionTimeoutMs = kUSBHostDefaultControlCompletionTimeoutMS);
-    
-    /*!
-     * @brief Issue an aynchronous setup request on the default control pipe
-     *
-     * @discussion This method will issue an asynchronous control request on the defaul pipe.
-     *
-     * <pre>
-     * @textblock
-     * The following request types are reserved and cannot be made as generic control requests, the appropriate API call should be used instead.
-     *
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientDevice), kDeviceRequestSetAddress � reserved, this request cannot be sent by drivers.
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientDevice), kDeviceRequestSetConfiguration � see setConfiguration().
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientInterface), kDeviceRequestSetInterface � see IOUSBHostInterface::selectAlternateSetting().
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientEndpoint), kRequestRecipientEndpoint � see IOUSBHostPipe::clearStall().
-     *
-     * @/textblock
-     * </pre>
-     *
-     * @param request Reference to a valid StandardUSB::DeviceRequest object.  This will be copied and can therefore be stack-allocated.
-     *
-     * @param dataBuffer Pointer to an IOMemoryDescriptor for the memory to be used for the I/O.
-     *
-     * @param completion Pointer to a valid, non NULL, IOUSBHostCompletion object.  This will be copied and can therefore be stack-allocated.
-     *
-     * @param completionTimeoutMs Time-out of the request in milliseconds.  If 0, the request will never time-out.
-     *
-     * @return IOReturn result code
-     */
     virtual IOReturn deviceRequest(StandardUSB::DeviceRequest& request, IOMemoryDescriptor* dataBuffer, IOUSBHostCompletion* completion, uint32_t completionTimeoutMs = kUSBHostDefaultControlCompletionTimeoutMS);
     
     /*!
-     * @brief Issue a synchronous setup request on the default control pipe.
-     *
-     * <pre>
-     * @textblock
-     * The following request types are reserved and cannot be made as generic control requests, the appropriate API call should be used instead.
-     *
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientDevice), kDeviceRequestSetAddress � reserved, this request cannot be sent by drivers.
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientDevice), kDeviceRequestSetConfiguration � see setConfiguration().
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientInterface), kDeviceRequestSetInterface � see IOUSBHostInterface::selectAlternateSetting().
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientEndpoint), kRequestRecipientEndpoint � see IOUSBHostPipe::clearStall().
-     *
-     * @/textblock
-     * </pre>
-     *
-     * @param request Reference to a valid StandardUSB::DeviceRequest object.  This will be copied and can therefore be stack-allocated.
-     *
-     * @param dataBuffer Pointer to the memory to be used for the I/O.
-     *
-     * @param bytesTransferred Reference which will be updated with the bytes transferred during the request.
-     *
-     * @param completionTimeoutMs Time-out of the request in milliseconds.  If 0, the request will never time-out.
-     *
-     * @return IOReturn result code
+     * @brief       Send a request on the default control endpoint
+     * @discussion  This method will send a synchronous request on the default control endpoint, and will not return until the request is complete.  This method will acquire the service's workloop lock, and will call commandSleep to send the control request.
+     * @param       request Reference to a valid StandardUSB::DeviceRequest structure.
+     * @param       dataBuffer A void* or IOMemoryDescriptor* defining the memory to use for the request's data phase.
+     * @param       bytesTransferred A uint32_t reference which will be updated with the byte count of the completed data phase.
+     * @param       completionTimeoutMs Timeout of the request in milliseconds.  If 0, the request will never timeout.
+     * @return      IOReturn value indicating the result of the IO request
      */
     virtual IOReturn deviceRequest(StandardUSB::DeviceRequest& request, void* dataBuffer, uint32_t& bytesTransferred, uint32_t completionTimeoutMs = kUSBHostDefaultControlCompletionTimeoutMS);
-    
-    /*!
-     * @brief Issue a synchronous setup request on the default control pipe.
-     *
-     * <pre>
-     * @textblock
-     * The following request types are reserved and cannot be made as generic control requests, the appropriate API call should be used instead.
-     *
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientDevice), kDeviceRequestSetAddress � reserved, this request cannot be sent by drivers.
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientDevice), kDeviceRequestSetConfiguration � see setConfiguration().
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientInterface), kDeviceRequestSetInterface � see IOUSBHostInterface::selectAlternateSetting().
-     *    (kRequestDirectionOut, kRequestTypeStandard, kRequestRecipientEndpoint), kRequestRecipientEndpoint � see IOUSBHostPipe::clearStall().
-     *
-     * @/textblock
-     * </pre>
-     *
-     * @param request Reference to a valid StandardUSB::DeviceRequest object.  This will be copied and can therefore be stack-allocated.
-     *
-     * @param dataBuffer Pointer to an IOMemoryDescriptor for the memory to be used for the I/O.
-     *
-     * @param bytesTransferred Reference which will be updated with the bytes transferred during the request.
-     *
-     * @param completionTimeoutMs Time-out of the request in milliseconds.  If 0, the request will never time-out.
-     *
-     * @return IOReturn result code
-     */
     virtual IOReturn deviceRequest(StandardUSB::DeviceRequest& request, IOMemoryDescriptor* dataBuffer, uint32_t& bytesTransferred, uint32_t completionTimeoutMs = kUSBHostDefaultControlCompletionTimeoutMS);
     
     /*!
-     * @brief Abort any requests made via the @link deviceRequest @\link methods
-     *
-     * @discussion This method will abort any requests made via the @link deviceRequest @\link methods.  It will not abort
-     * requests made through other interface objects.
-     *
-     * @param options IOUSBHostIOSource::tAbortOptions
-     *
-     * @param withError IOReturn error value to return with the requests.
-     *
-     * @return IOReturn result code
+     * @brief       Abort device requests made via the @link deviceRequest @/link methods by <code>forClient</code>
+     * @discussion  This method will abort any requests associated with a specific client made via the @link deviceRequest @/link methods.  It will not abort requests made by other clients.
+     * @param       options IOUSBHostIOSource::tAbortOptions
+     * @param       withError IOReturn error value to return with the requests.  The default value of kIOReturnAborted should be used.
+     * @return      IOReturn result code
      */
     IOReturn abortDeviceRequests(IOOptionBits options = IOUSBHostIOSource::kAbortAsynchronous, IOReturn withError = kIOReturnAborted);
     
@@ -437,45 +473,35 @@
 
 #pragma mark Miscellaneous
 public:
+    /*! @functiongroup Provider access */
+
     /*!
-     * @brief Return the parent/provider IOUSBHostDevice object of this interface.
-     *
-     * @return Pointer to the parent/provider IOUSBHostDevice object.
+     * @brief       Return the parent/provider IOUSBHostDevice object of this interface.
+     * @return      IOUSBHostDevice pointer
      */
     virtual IOUSBHostDevice* getDevice() const;
     
     /*!
-     * @brief Return the current frame number of the USB bus
-     *
-     * @description This method will return the current frame number of the USB bus.  This is most useful for
-     * scheduling future isochronous requests.
-     *
-     * @param theTime If not NULL, this will be updated with the current system time
-     *
-     * @return The current frame number
+     * @brief       Return the current frame number of the USB controller
+     * @description This method will return the current frame number of the USB controller, omitting microframe.  This is most useful for scheduling future isochronous requests.
+     * @param       theTime If not NULL, this will be updated with the current system time
+     * @return      The current frame number
      */
     virtual uint64_t getFrameNumber(AbsoluteTime* theTime = NULL) const;
     
     /*!
-     * @brief Return the current port status
-     *
-     * @discussion This method will return the current port status as a logical OR of bits described be @link USBDeviceInformationBits @\link
-     *
-     * @return port status
+     * @brief       Return the current port status
+     * @discussion  Combination of tUSBHostPortStatus values
+     * @return      port status
      */
     virtual uint32_t getPortStatus() const;
 
     /*!
-     * @brief Allocate a buffer to be used for I/O
-     *
-     * @discussion The underlying host controller hardware may have alignment and fragmentation restrictions.  This
-     * method will return a buffer which is guaranteed to meet the restrictions the host controller may have.
-     *
-     * @param options kIODirectionOut, kIODirectionIn to set the direction of the I/O transfer.
-     *
-     * @param capacity Size of the buffer to allocate
-     *
-     * @return Pointer to the newly allocated memory descriptor or NULL
+     * @brief       Allocate a buffer to be used for I/O
+     * @discussion  This method will allocate an IOBufferMemoryDescriptor optimized for use by the underlying controller hardware.  A buffer allocated by this method will not be bounced to perform DMA operations.
+     * @param       options kIODirectionOut, kIODirectionIn to set the direction of the I/O transfer.
+     * @param       capacity Size of the buffer to allocate
+     * @return      Pointer to an IOBufferMemoryDescriptor if successful, otherwise NULL
      */
     virtual IOBufferMemoryDescriptor* createIOBuffer(IOOptionBits options, mach_vm_size_t capacity);
     
@@ -512,59 +538,6 @@
         IOSimpleReporter*   _idlePolicyReport;
     };
     tExpansionData* _expansionData;
-    
-#pragma mark Deprecated
-public:
-    
-    // virtual const IOUSBInterfaceDescriptor* FindNextAltInterface(const IOUSBInterfaceDescriptor* current,
-    //                                                              IOUSBFindInterfaceRequest*      request) __attribute__((deprecated));
-    // Replacement: StandardUSB::getNextInterfaceDescriptor
-
-    // virtual IOUSBHostPipe* FindNextPipe(IOUSBHostPipe* current, IOUSBFindEndpointRequest* request) __attribute__((deprecated));
-    // virtual IOUSBHostPipe* FindNextPipe(IOUSBHostPipe* current, IOUSBFindEndpointRequest* request, bool withRetain) __attribute__((deprecated));
-    // Replacement: getInterfaceDescriptor and StandardUSB::getNextAssociatedDescriptorWithType to find an endpoint descriptor,
-    // then use copyPipe to retrieve the pipe object
-
-    // virtual const IOUSBDescriptorHeader* FindNextAssociatedDescriptor(const void* current, UInt8 type) __attribute__((deprecated));
-    // Replacement: getInterfaceDescriptor and StandardUSB::getNextAssociatedDescriptorWithType
-
-    // virtual IOReturn SetAlternateInterface(IOService* forClient, UInt16 alternateSetting) __attribute__((deprecated));
-    // Replacement: selectAlternateSetting
-
-    // virtual IOUSBHostPipe* GetPipeObj(UInt8 index) __attribute__((deprecated));
-    // virtual IOUSBHostPipe* GetPipeObjRetain(UInt8 index) __attribute__((deprecated));
-    // Replacement: copyPipe
-
-    // virtual UInt8 GetConfigValue() __attribute__((deprecated));
-    // Replacement: getConfigurationDescriptor
-
-    // Deprecated.  Use getProvider
-    // virtual IOUSBHostDevice* GetDevice() __attribute__((deprecated));
-
-    // virtual UInt8 GetInterfaceNumber() __attribute__((deprecated));
-    // virtual UInt8 GetAlternateSetting() __attribute__((deprecated));
-    // virtual UInt8 GetNumEndpoints() __attribute__((deprecated));
-    // virtual UInt8 GetInterfaceClass() __attribute__((deprecated));
-    // virtual UInt8 GetInterfaceSubClass() __attribute__((deprecated));
-    // virtual UInt8 GetInterfaceProtocol() __attribute__((deprecated));
-    // virtual UInt8 GetInterfaceStringIndex() __attribute__((deprecated));
-    // Replacement: getInterfaceDescriptor
-
-    // virtual IOReturn DeviceRequest(IOUSBDevRequest* request, IOUSBCompletion* completion = 0) __attribute__((deprecated));
-    // virtual IOReturn DeviceRequest(IOUSBDevRequestDesc* request, IOUSBCompletion* completion = 0) __attribute__((deprecated));
-    // Replacement: deviceRequest
-
-    // virtual IOReturn GetEndpointProperties(UInt8 alternateSetting, UInt8 endpointNumber, UInt8 direction, UInt8* transferType, UInt16* maxPacketSize, UInt8* interval) __attribute__((deprecated));
-    // Replacement: StandardUSB::getEndpoint*
-
-    // virtual IOReturn SetIdlePolicy(UInt32 deviceIdleTimeout, UInt32 ioIdleTimeout) __attribute__((deprecated));
-    // Replacement: setIdlePolicy and IOUSBHostPope::setIdlePolicy
-
-    // virtual void GetIdlePolicy(UInt32& deviceIdleTimeout, UInt32& ioIdleTimeout) __attribute__((deprecated));
-    // Replacement: getIdlePolicy and IOUSBHostPipe::getIdlePolicy
-
-    // IOBufferMemoryDescriptor* CreateIOBuffer(IOOptionBits options, mach_vm_size_t capacity) __attribute__((deprecated));
-    // Replacement: createIOBuffer
 };
 
 #endif // IOUSBHostFamily_IOUSBHostInterface_h
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostPipe.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostPipe.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostPipe.h	2016-06-29 01:13:25.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostPipe.h	2016-07-10 09:02:55.000000000 +0200
@@ -1,30 +1,119 @@
 /*
- * Copyright (c) 1998-2006 Apple Computer, Inc. All rights reserved.
+ * Copyright (c) 1998-2016 Apple Inc. All rights reserved.
  *
- * @APPLE_LICENSE_HEADER_START@
+ * @APPLE_OSREFERENCE_LICENSE_HEADER_START@
  *
- * The contents of this file constitute Original Code as defined in and
- * are subject to the Apple Public Source License Version 1.2 (the
- * "License").  You may not use this file except in compliance with the
- * License.  Please obtain a copy of the License at
- * http://www.apple.com/publicsource and read it before using this file.
+ * This file contains Original Code and/or Modifications of Original Code
+ * as defined in and that are subject to the Apple Public Source License
+ * Version 2.0 (the 'License'). You may not use this file except in
+ * compliance with the License. The rights granted to you under the License
+ * may not be used to create, or enable the creation or redistribution of,
+ * unlawful or unlicensed copies of an Apple operating system, or to
+ * circumvent, violate, or enable the circumvention or violation of, any
+ * terms of an Apple operating system software license agreement.
  *
- * This Original Code and all software distributed under the License are
- * distributed on an "AS IS" basis, WITHOUT WARRANTY OF ANY KIND, EITHER
+ * Please obtain a copy of the License at
+ * http://www.opensource.apple.com/apsl/ and read it before using this file.
+ *
+ * The Original Code and all software distributed under the License are
+ * distributed on an 'AS IS' basis, WITHOUT WARRANTY OF ANY KIND, EITHER
  * EXPRESS OR IMPLIED, AND APPLE HEREBY DISCLAIMS ALL SUCH WARRANTIES,
  * INCLUDING WITHOUT LIMITATION, ANY WARRANTIES OF MERCHANTABILITY,
  * FITNESS FOR A PARTICULAR PURPOSE, QUIET ENJOYMENT OR NON-INFRINGEMENT.
  * Please see the License for the specific language governing rights and
  * limitations under the License.
  *
- * @APPLE_LICENSE_HEADER_END@
+ * @APPLE_OSREFERENCE_LICENSE_HEADER_END@
  */
 
 /*!
- * @header IOUSBHostPipe.h
- *
- * @brief Provides IOUSBHostPipe API
+ @header     IOUSBHostPipe.h
+ @brief      IOUSBHostPipe is an object representing a USB endpoint.
+ @discussion
+ 
+ <h3>IOUSBPipe Migration</h3>
+ 
+ IOUSBHostPipe serves as a replacement for IOUSBPipe.  Clients that previously used an IOUSBPipe can use the following guide to convert to IOUSBHostPipe.
+ 
+ <code>virtual IOReturn IOUSBPipe::Abort(IOOptionBits, IOReturn);</code><br>
+ Replacement: <code>abort(...);</code>
+ 
+ <code>virtual IOReturn IOUSBPipe::Reset();<br>
+ virtual IOReturn IOUSBPipe::ClearStall();</code><br>
+ Replacement: <code>clearStall(false)</code>
+ 
+ <code>virtual IOReturn IOUSBPipe::ClearPipeStall(bool);</code><br>
+ Replacement: <code>clearStall(...);</code>
+ 
+ <code>virtual IOReturn IOUSBPipe::Read(IOMemoryDescriptor*, IOUSBCompletion*, UInt32*);<br>
+ virtual IOReturn IOUSBPipe::Read(IOMemoryDescriptor*, UInt32, UInt32, IOUSBCompletion*, UInt32*);<br>
+ virtual IOReturn IOUSBPipe::Read(IOMemoryDescriptor*, UInt32, UInt32, IOByteCount, IOUSBCompletion*, UInt32*);<br>
+ virtual IOReturn IOUSBPipe::Read(IOMemoryDescriptor*, UInt32, UInt32, IOByteCount, IOUSBCompletionWithTimeStamp*, UInt32*);<br>
+ virtual IOReturn IOUSBPipe::Write(IOMemoryDescriptor*, UInt32, UInt32, IOUSBCompletion*);<br>
+ virtual IOReturn IOUSBPipe::Write(IOMemoryDescriptor*, UInt32, UInt32, IOByteCount, IOUSBCompletion*);<br>
+ virtual IOReturn IOUSBPipe::Write(IOMemoryDescriptor*, IOUSBCompletion*);<br>
+ virtual IOReturn IOUSBPipe::Read(IOMemoryDescriptor*, UInt64, UInt32, IOUSBIsocFrame*, IOUSBIsocCompletion*);<br>
+ virtual IOReturn IOUSBPipe::Read(IOMemoryDescriptor*, UInt64, UInt32, IOUSBLowLatencyIsocFrame*, IOUSBLowLatencyIsocCompletion*, UInt32);<br>
+ virtual IOReturn IOUSBPipe::Write(IOMemoryDescriptor*, UInt64, UInt32, IOUSBIsocFrame*, IOUSBIsocCompletion*);<br>
+ virtual IOReturn IOUSBPipe::Write(IOMemoryDescriptor*, UInt64, UInt32, IOUSBLowLatencyIsocFrame*, IOUSBLowLatencyIsocCompletion*, UInt32);</code><br>
+ Replacement: <code>io(...);</code>
+ 
+ <code>virtual IOReturn IOUSBPipe::ControlRequest(IOUSBDevRequestDesc*, IOUSBCompletion*, UInt32, UInt32);<br>
+ virtual IOReturn IOUSBPipe::ControlRequest(IOUSBDevRequest*, IOUSBCompletion*);<br>
+ virtual IOReturn IOUSBPipe::ControlRequest(IOUSBDevRequestDesc*, UInt32, UInt32, IOUSBCompletion*);<br>
+ virtual IOReturn IOUSBPipe::ControlRequest(IOUSBDevRequest*, UInt32, UInt32, IOUSBCompletion*);</code><br>
+ Replacement: <code>controlRequest(...);</code>
+ 
+ <code>virtual const IOUSBController::Endpoint* IOUSBPipe::GetEndpoint();<br>
+ virtual UInt8 IOUSBPipe::GetDirection();<br>
+ virtual UInt8 IOUSBPipe::GetType();<br>
+ virtual UInt8 IOUSBPipe::GetEndpointNumber();<br>
+ virtual UInt16 IOUSBPipe::GetMaxPacketSize();<br>
+ virtual UInt8 IOUSBPipe::GetInterval();</code><br>
+ Replacement: Use <code>getEndpointDescriptor()</code>, <code>getSuperSpeedEndpointCompanionDescriptor()</code>, and <code>getDescriptors()</code> with <code>StandardUSB::getEndpoint*</code> methods to retrieve endpoint characteristics
+ 
+ <code>virtual tUSBHostDeviceAddress IOUSBPipe::GetAddress();</code><br>
+ Replacement: <code>getDeviceAddress();</code>
+ 
+ <code>virtual UInt8 IOUSBPipe::GetSpeed();</code><br>
+ Replacement: <code>getSpeed();</code>
+ 
+ <code>virtual IOReturn IOUSBPipe::GetPipeStatus();</code><br>
+ Replacement: If an endpoint is halted, new IO requests will be rejected with an appropriate error until the condition is cleared.
+ 
+ <code>virtual IOReturn IOUSBPipe::SetPipePolicy(UInt16 maxPacketSize, UInt8 maxInterval);</code><br>
+ Replacement: <code>adjustPipe(...);</code>
+ 
+ <h3>IOUSBPipeV2 Migration</h3>
+ 
+ IOUSBPipeV2 implemented interfaces for USB 3.0 streaming endpoint support.  IOUSBHostPipe provides interfaces to enable or disable streaming, and IOUSBHostStream provides interfaces to perform streaming IO.
+ 
+ <code>virtual IOReturn IOUSBPipeV2::CreateStreams(UInt32);</code><br>
+ Replacement: <code>enableStreams();</code> and <code>disableStreams();</code>
+
+ <code>virtual IOReturn IOUSBPipeV2::Read(UInt32, IOMemoryDescriptor*, UInt32, UInt32, IOByteCount, IOUSBCompletion*, IOByteCount*);<br>
+ virtual IOReturn IOUSBPipeV2::Write(UInt32, IOMemoryDescriptor*, UInt32, UInt32, IOByteCount, IOUSBCompletion*);<br>
+ virtual IOReturn IOUSBPipeV2::Abort(UInt32, IOOptionBits, IOReturn);</code><br>
+ Replacement: Use <code>copyStream</code> and IOUSBHostStream interfaces to perform IO to a streaming endpoint.
+ 
+ <code>virtual UInt32 IOUSBPipeV2::GetConfiguredStreams();</code><br>
+ Replacement: none
+ 
+ <code>virtual UInt32 IOUSBPipeV2::SupportsStreams();</code><br>
+ Replacement: <code>StandardUSB::getEndpointMaxStreams(...);</code>
+ 
+ <code>virtual const IOUSBSuperSpeedEndpointCompanionDescriptor* IOUSBPipeV2::GetSuperSpeedEndpointCompanionDescriptor();</code><br>
+ Replacement: <code>getSuperSpeedEndpointCompanionDescriptor(...);</code>
+
+ <code>virtual UInt8 IOUSBPipeV2::GetMult();</code><br>
+ Replacement: <code>StandardUSB::getEndpointMult(...);</code>
+ Refer to documentation for this method, as it may not return the same values as <code>IOUSBPipeV2::GetMult()</code>.
+
+ <code>virtual UInt8 IOUSBPipeV2::GetMaxBurst();<br>
+ virtual UInt16 IOUSBPipeV2::GetBytesPerInterval();</code><br>
+ Replacement: <code>StandardUSB::getEndpointBurstSize(...)</code> or <code>StandardUSB::getEndpointBurstSize32(...)</code>.  Refer to documentation for the replacement methods, as they may not return the same values as <code>IOUSBPipeV2::GetMaxBurst()</code> or <code>IOUSBPipeV2::GetBytesPerInterval;</code>
  */
+
 #ifndef IOUSBHostFamily_IOUSBHostPipe_h
 #define IOUSBHostFamily_IOUSBHostPipe_h
 
@@ -40,11 +129,9 @@
 class AppleUSBHostController;
 
 /*!
- * @class IOUSBHostPipe
- *
- * @brief IOUSBHostPipe object
- *
- * @discussion Provides the API for controlling pipe policy and performing I/O.
+ * @class       IOUSBHostPipe
+ * @brief       The OSObject representing a USB endpoint
+ * @discussion  This class provides functionality to transfer data across USB.  Function drivers should not subclass IOUSBHostPipe.
  */
 class IOUSBHostPipe : public IOUSBHostIOSource
 {
@@ -57,15 +144,9 @@
 
 public:
     /*!
-     * @struct StandardUSBDescriptors
-     *
-     * @brief Encapsulates descriptors for a single endpoint
-     * 
-     * @discussion The StandardUSBDescriptors struct is used to intialize and adjust pipes in the system.  The bcdUSB member
-     * must be initialized to the USB revision supported by the device.  Acceptable values are 0x0110, 0x0200, 0x0300, 0x0310.
-     * The descriptor member must always be initialized with a pointer to a valid endpoint descriptor.  The ssCompanionDescriptor
-     * and sspCompanionDescriptor members may be required for bcdUSB versions 0x0300 and greater, depending on operating speed
-     * and values set in the descriptors.  See USB 3.1 � 9.5 for more information on when these descriptors may be required.
+     * @struct      StandardUSBDescriptors
+     * @brief       Encapsulates descriptors for a single endpoint
+     * @discussion  The StandardUSBDescriptors struct is used to intialize and adjust pipes in the system.  The bcdUSB member must be initialized to the USB revision supported by the device.  Acceptable values are 0x0110, 0x0200, 0x0300, 0x0310.  The descriptor member must always be initialized with a pointer to a valid endpoint descriptor.  The ssCompanionDescriptor and sspCompanionDescriptor members may be required for bcdUSB versions 0x0300 and greater, depending on device operating speed and values set in the descriptors.  See USB 3.1 � 9.5 for more information on when these descriptors may be required.
      */
     struct StandardUSBDescriptors
     {
@@ -75,21 +156,46 @@
         const StandardUSB::SuperSpeedPlusIsochronousEndpointCompanionDescriptor*    sspCompanionDescriptor;
     };
     
-    static IOUSBHostPipe* withDescriptorsAndOwners(const StandardUSB::EndpointDescriptor* descriptor, const StandardUSB::SuperSpeedEndpointCompanionDescriptor* companionDescriptor,
-                                                   AppleUSBHostController* controller, IOUSBHostDevice* device, IOUSBHostInterface* interface, UInt8 speed, tUSBHostDeviceAddress address);
+    /*
+     * @brief       Factory method for creating an IOUSBHostPipe object
+     * @discussion  This method should not be called by function drivers.  To create an IOUSBHostPipe, use IOUSBHostInterface::copyPipe(...)
+     * @param       descriptor EndpointDescriptor for the endpoint
+     * @param       companionDescriptor SuperSpeedEndpointCompanionDescriptor for the endpoint, or NULL
+     * @param       controller AppleUSBHostController to which the USB endpoint is associated
+     * @param       device IOUSBHostDevice to which this endpoint belongs, or NULL
+     * @param       interface IOUSBHostInterface to which this endpoint belongs, or NULL
+     * @param       speed Operational speed of the device
+     * @param       address tUSBHostDeviceAddress that has been allocated by the controller
+     * @return      Pointer to an IOUSBHostPipe object if successful, otherwise NULL
+     */
+    static IOUSBHostPipe* withDescriptorsAndOwners(const StandardUSB::EndpointDescriptor* descriptor,
+                                                   const StandardUSB::SuperSpeedEndpointCompanionDescriptor* companionDescriptor,
+                                                   AppleUSBHostController* controller,
+                                                   IOUSBHostDevice* device,
+                                                   IOUSBHostInterface* interface,
+                                                   UInt8 speed,
+                                                   tUSBHostDeviceAddress address);
 
 protected:
-    virtual bool initWithDescriptorsAndOwners(const StandardUSB::EndpointDescriptor* descriptor, const StandardUSB::SuperSpeedEndpointCompanionDescriptor* companionDescriptor,
-                                              AppleUSBHostController* controller, IOUSBHostDevice* device, IOUSBHostInterface* interface, UInt8 speed, tUSBHostDeviceAddress address);
+    virtual bool initWithDescriptorsAndOwners(const StandardUSB::EndpointDescriptor* descriptor,
+                                              const StandardUSB::SuperSpeedEndpointCompanionDescriptor* companionDescriptor,
+                                              AppleUSBHostController* controller,
+                                              IOUSBHostDevice* device,
+                                              IOUSBHostInterface* interface,
+                                              UInt8 speed,
+                                              tUSBHostDeviceAddress address);
 
 #pragma mark IOUSBHostIOSource overrides
 public:
     virtual void free();
-    
+
+    /*! @functiongroup IO 
+     *  @discussion All I/O calls will synchronize with the workloop.  Furthermore, all completion callbacks will also synchronize with the workloop.  Therefore, when using the asynchronous I/O methods it is most performant to make subsequent calls from completion callback as the workloop lock will already be owned.
+     */
+
     /*!
-     * @brief Abort pending I/O requests.
-     *
-     * @discussion See IOUSBHostIOSource::abort for documentation
+     * @brief       Abort pending I/O requests.
+     * @discussion  See IOUSBHostIOSource::abort for documentation
      */
     virtual IOReturn abort(IOOptionBits options = kAbortAsynchronous, IOReturn withError = kIOReturnAborted, IOService* forClient = NULL);
     
@@ -118,16 +224,15 @@
 #pragma mark Descriptors and policies
 public:
     /*!
-     * @methodgroup Descriptors and Policies
+     * @functiongroup Descriptors
      */
     
     /*!
-     * @brief Options for <code>getEndpointDescriptor()</code> and <code>getSuperSpeedEndpointCompanionDescriptor()</code>
+     * @brief Options for <code>getEndpointDescriptor</code>, <code>getSuperSpeedEndpointCompanionDescriptor</code>, and <code>getDescriptors</code>
      *
      * @discussion
-     * @constant kGetEndpointDescriptorOriginal - Original descriptor as returned as part of the configuration descriptor.
-     * @constant kGetEndpointDescriptorCurrentPolicy - Descriptor controlling the current endpoint policy.  This may differ from
-     * kGetEndpointDescriptorOriginal if <code>adjustPipe()</code> has been called.
+     * @constant kGetEndpointDescriptorOriginal - Original descriptor used when creating the pipe
+     * @constant kGetEndpointDescriptorCurrentPolicy - Descriptor controlling the current endpoint policy, including changes made via the <code>adjustPolicy</code> method.
      */
     enum tGetEndpointDescriptorOptions
     {
@@ -136,104 +241,72 @@
     };
     
     /*!
-     * @brief This method will return an endpoint descriptor associated with the pipe.
-     *
-     * @param type The desired endpoint descriptor type to return.  See @link //apple_ref/cpp/tag/IOUSBHostPipe/tGetEndpointDescriptorOptions
-     * IOUSBHostPipe::tGetEndpointDescriptorOptions @/link for more details.
-     *
-     * @return If successful a pointer to the endpoint descriptor is returned.  Otherwise, NULL is returned.
+     * @brief   Retrieve the EndpointDescriptor associated with this object
+     * @param   type tGetEndpointDescriptorOptions indicating which descriptor to retrieve
+     * @return  EndpointDescriptor pointer if successful, otherwise NULL
      */
     virtual const StandardUSB::EndpointDescriptor* getEndpointDescriptor(tGetEndpointDescriptorOptions type = kGetEndpointDescriptorCurrentPolicy);
     
     /*!
-     * @brief This method will return the Super-Speed endpoint companion descriptor associated with the pipe.
-     *
-     * @param type The desired endpoint descriptor type to return. See @link //apple_ref/cpp/tag/IOUSBHostPipe/tGetEndpointDescriptorOptions
-     * IOUSBHostPipe::tGetEndpointDescriptorOptions @/link for more details.
-     *
-     * @return If successful a pointer to the companion descriptor is returned.  Otherwise, NULL is returned.
+     * @brief   Retrieve the SuperSpeedEndpointCompanionDescriptor associated with this object
+     * @param   type tGetEndpointDescriptorOptions indicating which descriptor to retrieve
+     * @return  SuperSpeedEndpointCompanionDescriptor pointer if successful, otherwise NULL
      */
     virtual const StandardUSB::SuperSpeedEndpointCompanionDescriptor* getSuperSpeedEndpointCompanionDescriptor(tGetEndpointDescriptorOptions type = kGetEndpointDescriptorCurrentPolicy);
-    
+
+    /*! @functiongroup Policies */
     /*!
-     * @brief This method is used to change the amount of bandwidth currently allocated to the pipe.
-     *
-     * @discussion This method is only valid for interrupt and isochronous endpoints.  There is only a finite amount of
-     * bandwith available for interrupt and isochronous endpoints on the USB bus TODO
-     *
-     * @param endpointDescriptor Pointer to an endpoint descriptor describing the bandwidth request
-     *
-     * @param companionDescriptor Pointer to a companion descriptor describing the bandwidth request
-     *
-     * @return IOReturn result code
+     * @brief       Adjust behavior of periodic endpoints to consume a different amount of bus bandwidth
+     * @discussion  Periodic (interrupt and isochronous) endpoints reserve bus bandwidth when they are created, which takes into account max packet size, burst size, and the endpoint service interval.  If a function driver knows the endpoint will not use all of the allocated bandwidth, the <code>adjustPolicy</code> method may be used to reduce the bandwidth reserved for the endpoint.  The original endpoint descriptors should be copied and modified to adjust max packet size, mult, burst, and interval, and then passed to <code>adjustPolicy</code>.  The altered descriptors must pass <code>StandardUSB::validateEndpointDescriptor(...)</code> for policy changes to be processed.
+     * @param       endpointDescriptor Pointer to an EndpointDescriptor describing the new endpoint policy
+     * @param       companionDescriptor Pointer to a SuperSpeedEndpointCompanionDescriptor describing the bandwidth request
+     * @return      IOReturn result code
      */
     virtual IOReturn adjustPipe(const StandardUSB::EndpointDescriptor* endpointDescriptor, const StandardUSB::SuperSpeedEndpointCompanionDescriptor* companionDescriptor);
     
     /*!
-     * @brief Set the idle policy of the pipe
-     *
-     * @discussion TODO Detailed discussion about idling.  This method is only valid for interrupt and bulk endpoints.
-     *
-     * @param idleTimeoutMs The time, in milliseconds, after which if no I/O has completed the IOUSBHostPipe is consider idle.
-     *
-     * @return IOReturn result code
+     * @brief       Sets the desired idle timeout for the pipe
+     * @discussion  When a bulk or interrupt pipe is actively servicing an IO request, it will be considered "busy" for idleTimeoutMs.  For a more complete discussion of idle policies, refer to "Pausing IO" in IOUSBHostFamily.h.
+     * @param       idleTimeoutMs The amount of time, in milliseconds, before an active transfer is considered idle.  If 0 the pipe will not be considered idle if there is an IO request enqueued.
+     * @return      IOReturn result code
      */
     virtual IOReturn setIdlePolicy(uint32_t idleTimeoutMs);
     
     /*!
-     * @brief Get the idle policy of the pipe
-     *
-     * @discussion This method is only valid for interrupt and bulk endpoints.
-     *
-     * @return The current idle timeout in milliseconds
+     * @brief       Retrieve the current idle timeout for the pipe
+     * @return      Current idle timeout in milliseconds
      */
     virtual uint32_t getIdlePolicy();
-    
+
+    /*! @functiongroup IO */
     /*!
-     * @brief Clear the halt condition of the pipe.
-     *
-     * @discussion This method will abort all pending I/O, clear the halted condition, and reset the data toggle for the pipe.
-     * In general, this must be done after a non-control I/O call returns or completes with an error condition.  This method
-     * will also clear the transaction translator if this is a 'split' pipe as described in section 11.17.5 of the 
-     * USB 2.0 specification.
+     * @brief       Clear the halt condition of the pipe.
+     * @discussion  When a bulk or interrupt USB endpoint encounters any IO error other than a timeout, it transitions to a Halted state which must be cleared to perform additional IO on the endpoint.  This method will clear the halted condition for the endpoint, including sending a CLEAR_TT_BUFFER control request  (USB 2.0 11.24.2.3) to an intermediate hub if required.  All pending IO on the endpoint will be aborted, and the data toggle for the endpoint will also be reset.  To keep the device's data toggle synchronized with the host's data toggle, it is recommended that the withRequest parameter is always set to true, which causes the <code>clearStall</code> call to send a CLEAR_FEATURE ENDPOINT_HALT (USB 2.0 9.4.1) command to the device.  clearStall is not required for control endpoints.
+     * @param       withRequest If true a CLEAR_FEATURE ENDPOINT_HALT (USB 2.0 9.4.1) will be sent to the device.
      *
-     * @param withRequest If true the USB device request: CLEAR_FEATURE::ENDPOINT_HALT for this endnpoint request will be
-     * issued on the default pipe.  See section 9.4.1 of the USB 2.0 specification for more details.
-     *
-     * @return IOReturn result code
+     * @return      IOReturn result code
      */
     virtual IOReturn clearStall(bool withRequest);
     
     // Public pad slots for descriptors and policies
+    /*! @functiongroup Policies */
+    OSMetaClassDeclareReservedUsed(IOUSBHostPipe, 10);
     /*!
-     * @brief This method is used to change the amount of bandwidth currently allocated to the pipe.
-     *
-     * @discussion This method is only valid for interrupt and isochronous endpoints.  The standard USB descriptors used
-     * as parameters define the max packet size and bInterval to use for the new endpoint policy.
-     *
-     * @param descriptors Pointer to an endpoint descriptor structure describing the bandwidth request.  See documentation for StandardUSBDescriptors
-     * for more information on proper intialization of the structure.
-     *
-     * @return IOReturn result code
+     * @brief       Adjust behavior of periodic endpoints to consume a different amount of bus bandwidth
+     * @discussion  Periodic (interrupt and isochronous) endpoints reserve bus bandwidth when they are created, which takes into account max packet size, burst size, and the endpoint service interval.  If a function driver knows the endpoint will not use all of the allocated bandwidth, the <code>adjustPolicy</code> method may be used to reduce the bandwidth reserved for the endpoint.  The original endpoint descriptors should be copied and modified to adjust max packet size, mult, burst, and interval, and then passed to <code>adjustPolicy</code>.  The altered descriptors must pass <code>StandardUSB::validateEndpointDescriptor(...)</code> for policy changes to be processed.
+     * @param       descriptors Pointer to a StandardUSBDescriptors structure describing the new endpoint policy
+     * @return      IOReturn result code
      */
-    OSMetaClassDeclareReservedUsed(IOUSBHostPipe, 10);
     virtual IOReturn adjustPipe(StandardUSBDescriptors* descriptors);
 
+    /*! @functiongroup Descriptors */
+    OSMetaClassDeclareReservedUsed(IOUSBHostPipe, 11);
     /*!
-     * @brief This method is used to retrieve standard USB descriptors for the pipe
-     *
-     * @discussion This method will return an @link //apple_ref/cpp/tag/IOUSBHostPipe/StandardUSBDescriptors IOUSBHostPipe::StandardUSBDescriptors @/link
-     * populated with pointers to the descriptor set specified by the <code>type</code> parameter.
-     *
-     * @param descriptors A pointer to an @link //apple_ref/cpp/tag/IOUSBHostPipe/StandardUSBDescriptors IOUSBHostPipe::StandardUSBDescriptors @/link struct
-     * that will be populated with descriptor pointers
-     *
-     * @param type The desired endpoint descriptor type to return.  See @link //apple_ref/cpp/tag/IOUSBHostPipe/tGetEndpointDescriptorOptions
-     * IOUSBHostPipe::tGetEndpointDescriptorOptions @/link for more details.
-     *
-     * @return IOReturn result code
+     * @brief   Retrieve the descriptors associated with this object
+     * @param   descriptors StandardUSBDescriptors pointer to populate
+     * @param   type tGetEndpointDescriptorOptions indicating which descriptors to retrieve
+     * @return  IOReturn result
      */
-    OSMetaClassDeclareReservedUsed(IOUSBHostPipe, 11);
     virtual IOReturn getDescriptors(StandardUSBDescriptors* descriptors, tGetEndpointDescriptorOptions type = kGetEndpointDescriptorCurrentPolicy);
 
     OSMetaClassDeclareReservedUnused(IOUSBHostPipe, 12);
@@ -285,140 +358,31 @@
 
 #pragma mark Control requests
 public:
+    /*! @functiongroup IO */
     /*!
-     * @methodgroup Control Requests
-     */
-    
-    /*!
-     * @brief Issue an asynchronous control request on the pipe.
-     *
-     * @discussion This method will issue an asynchronous control request on the pipe.  A trivial example is provided below:
-     *
-     * <pre>
-     * @textblock
-     * uint8_t                    dataBuffer[4];
-     * IOReturn                   result;
-     * StandardUSB::DeviceRequest request;
-     * IOUSBHostCompletion        completion;
-     *
-     * request.bmRequestType = makeDeviceRequestbmRequestType(kRequestDirectionIn, kRequestTypeClass, kRequestRecipientInterface);
-     * request.bRequest      = 0x12;
-     * request.wValue        = 0x3456;
-     * request.wIndex        = 0x7890;
-     * request.wLength       = sizeof(uint32_t);
-     *
-     * completion.owner     = this;
-     * completion.action    = OSMemberFunctionCast(IOUSBHostCompletionAction, this, &MyDriver::controlRequestComplete);
-     * completion.parameter = NULL;
-     *
-     * result = _controlPipe->controlRequest(this, request, &dataBuffer, &completion, 1000);<br>
-     *
-     * ...
-     *
-     * void MyDriver::controlRequestComplete(void* parameter, IOReturn status, uint32_t bytesTransferred)
-     * {
-     *     if(status == kIOReturnSuccess)
-     *     {
-     *         IOLog("received %u bytes\n", bytesTransferred);
-     *     }
-     *
-     * @/textblock
-     * </pre>
-     *
-     * @param forClient The object issuing the request (generally the <code>this</code> pointer).
-     *
-     * @param request Reference to a valid StandardUSB::DeviceRequest object.  This will be copied and can therefore be stack-allocated.
-     *
-     * @param dataBuffer Pointer to the memory to be used for the I/O.
-     *
-     * @param completion Pointer to a valid, non NULL, IOUSBHostCompletion object.  This will be copied and can therefore be stack-allocated.
-     *
-     * @param completionTimeoutMs Time-out of the request in milliseconds.  If 0, the request will never time-out.
-     *
-     * @return IOReturn result code
+     * @brief       Enqueue a request on a control endpoint
+     * @discussion  This method will enqueue an asynchronous request on a control endpoint.  If successful, the provided completion routine will be called to report the status of the completed IO.
+     * @param       forClient The service issuing the request.
+     * @param       request Reference to a valid StandardUSB::DeviceRequest structure.  The structure is copied and can therefore be stack-allocated.
+     * @param       dataBuffer A void* or IOMemoryDescriptor* defining the memory to use for the request's data phase.
+     * @param       completion Pointer to a IOUSBHostCompletion structure.  This will be copied and can therefore be stack-allocated.
+     * @param       completionTimeoutMs Timeout of the request in milliseconds.  If 0, the request will never timeout.
+     * @return      kIOReuturnSuccess if the completion will be called in the future, otherwise error
      */
     virtual IOReturn controlRequest(IOService* forClient, StandardUSB::DeviceRequest& request, void* dataBuffer, IOUSBHostCompletion* completion, uint32_t completionTimeoutMs);
-    
-    /*!
-     * @brief Issue an asynchronous control request on the pipe.
-     *
-     * @discussion This method will issue an asynchronous control request on the pipe.  This method differs from
-     * @link //apple_ref/cpp/instm/IOUSBHostPipe/controlRequest/IOReturn/(IOService*,StandardUSB::DeviceRequest%26,void*,IOUSBHostCompletion*,uint32_t) @/link
-     * in that it takes an IOMemoryDescriptor instead of a void * for <code>dataBuffer</code>.
-     *
-     * @param forClient The object issuing the request (generally the <code>this</code> pointer).
-     *
-     * @param request Reference to a valid StandardUSB::DeviceRequest object.  This will be copied and can therefore be stack-allocated.
-     *
-     * @param dataBuffer Pointer to an IOMemoryDescriptor for the memory to be used for the I/O.
-     *
-     * @param completion Pointer to a valid, non NULL, IOUSBHostCompletion object.  This will be copied and can therefore be stack-allocated.
-     *
-     * @param completionTimeoutMs Time-out of the request in milliseconds.  If 0, the request will never time-out.
-     *
-     * @return IOReturn result code
-     */
     virtual IOReturn controlRequest(IOService* forClient, StandardUSB::DeviceRequest& request, IOMemoryDescriptor* dataBuffer, IOUSBHostCompletion* completion, uint32_t completionTimeoutMs);
     
     /*!
-     * @brief Issue a synchronous control request on the pipe.
-     *
-     * @discussion This method will issue a synchronous control request on the pipe. A trivial example is provided below:
-     *
-     * <pre>
-     * @textblock
-     * uint8_t                    dataBuffer[4];
-     * uint32_t                   bytesTransferred;
-     * IOReturn                   result;
-     * StandardUSB::DeviceRequest request;
-     *
-     * request.bmRequestType = makeDeviceRequestbmRequestType(kRequestDirectionIn, kRequestTypeClass, kRequestRecipientInterface);
-     * request.bRequest      = 0x12;
-     * request.wValue        = 0x3456;
-     * request.wIndex        = 0x7890;
-     * request.wLength       = sizeof(uint32_t);
-     *
-     * result = _controlPipe->controlRequest(this, request, &dataBuffer, bytesTransferred, 1000);
-     * if(result == kIOReturnSuccess)
-     * {
-     *     IOLog("received %u bytes\n", bytesTransferred);
-     * }
-     * @/textblock
-     * </pre>
-     *
-     * @param forClient The object issuing the request (generally the <code>this</code> pointer).
-     *
-     * @param request Reference to a valid StandardUSB::DeviceRequest object.  This will be copied and can therefore be stack-allocated.
-     *
-     * @param dataBuffer Pointer to the memory to be used for the I/O.
-     *
-     * @param bytesTransferred Reference which will be updated with the bytes transferred during the request.
-     *
-     * @param completionTimeoutMs Time-out of the request in milliseconds.  If 0, the request will never time-out.
-     *
-     * @return IOReturn result code
+     * @brief       Send a request on a control endpoint
+     * @discussion  This method will send a synchronous request on a control endpoint, and will not return until the request is complete.  This method will acquire the owning device's workloop lock, and will call commandSleep to send the control request.
+     * @param       forClient The service issuing the request.
+     * @param       request Reference to a valid StandardUSB::DeviceRequest structure.
+     * @param       dataBuffer A void* or IOMemoryDescriptor* defining the memory to use for the request's data phase.
+     * @param       bytesTransferred A uint32_t reference which will be updated with the byte count of the completed data phase.
+     * @param       completionTimeoutMs Timeout of the request in milliseconds.  If 0, the request will never timeout.
+     * @return      IOReturn value indicating the result of the IO request
      */
     virtual IOReturn controlRequest(IOService* forClient, StandardUSB::DeviceRequest& request, void* dataBuffer, uint32_t& bytesTransferred, uint32_t completionTimeoutMs);
-    
-    /*!
-     * @brief Issue a synchronous control request on the pipe.
-     *
-     * @discussion This method will issue a synchronous control request on the pipe.  This method differs from
-     * @link //apple_ref/cpp/instm/IOUSBHostPipe/controlRequest/IOReturn/(IOService*,StandardUSB::DeviceRequest%26,void*,uint32_t%26,uint32_t) @/link
-     * in that it takes an IOMemoryDescriptor instead of a void * for <code>dataBuffer</code>.
-     *
-     * @param forClient The object issuing the request (generally the <code>this</code> pointer).
-     *
-     * @param request Reference to a valid StandardUSB::DeviceRequest object.  This will be copied and can therefore be stack-allocated.
-     *
-     * @param dataBuffer Pointer to an IOMemoryDescriptor for the memory to be used for the I/O.
-     *
-     * @param bytesTransferred Reference which will be updated with the bytes transferred during the request.
-     *
-     * @param completionTimeoutMs Time-out of the request in milliseconds.  If 0, the request will never time-out.
-     *
-     * @return IOReturn result code
-     */
     virtual IOReturn controlRequest(IOService* forClient, StandardUSB::DeviceRequest& request, IOMemoryDescriptor* dataBuffer, uint32_t& bytesTransferred, uint32_t completionTimeoutMs);
 
     // Public pad slots for control requests
@@ -463,55 +427,33 @@
 #pragma mark IO
 public:
     /*!
-     * @methodgroup I/O
-     *
-     * @discussion All I/O calls will synchronize with the workloop.  Furthermore, all completion callbacks will also
-     * synchronize with the workloop.  Therefore, when using the asynchronous I/O methods it is most performant to make
-     * subsequent calls from completion callback as the workloop lock will already be owned.
+     * @functiongroup IO
      */
     
     /*!
-     * @brief Issue an asynchronous I/O request
-     *
-     * @discussion See IOUSBHostIOSource::io for documentation
-
-     * @param completionTimeoutMs Must be 0 for interrupt endpoints.
+     * @brief       Enqueue a request on a bulk or interrupt endpoint
+     * @discussion  See IOUSBHostIOSource::io for documentation
+     * @param       completionTimeoutMs Must be 0 for interrupt endpoints.
      */
     virtual IOReturn io(IOMemoryDescriptor* dataBuffer, uint32_t dataBufferLength, IOUSBHostCompletion* completion, uint32_t completionTimeoutMs = 0);
     
     /*!
-     * @brief Issue a synchronous I/O request
-     *
-     * @discussion See IOUSBHostIOSource::io for documentation
-     *
-     * @param completionTimeoutMs Must be 0 for interrupt endpoints.
+     * @brief       Perform a request on a bulk or interrupt endpoint
+     * @discussion  See IOUSBHostIOSource::io for documentation
+     * @param       completionTimeoutMs Must be 0 for interrupt endpoints.
      */
     virtual IOReturn io(IOMemoryDescriptor* dataBuffer, uint32_t dataBufferLength, uint32_t& bytesTransferred, uint32_t completionTimeoutMs = 0);
     
     /*!
-     * @brief Issue an I/O request to an isochronous pipe.
-     *
-     * @discussion This method is used to issue isochronout I/O requests.  To ensure minimal latency the
-     * IOUSBHostIsochronousFrame::status and IOUSBHostIsochronousFrame::completeCount fields of <code>frameList</code> are
-     * updated at interrupt time.  In the case of an asynchronous call, this allows software to peek at the frame list and
-     * detect completed frames prior to receiving the completion callback.
-     *
-     * @param dataBuffer Pointer to a valid memory descriptor to be used as the backing store for the I/O.
-     *
-     * @param frameList Pointer to the frame list describing the request.  See <link>IOUSBHostIsochronousFrame</link> for
-     * information regarding structure initialization requirements and usage.
-     *
-     * @param frameListCount Number of elements in <code>frameList</code>.
-     *
-     * @param firstFrameNumber Frame number which this request should begin on.  The current frame number can be queried via
-     * <code>IOUSHostDevice::getFrameNumber()</code> or <code>IOUSBHostInterface::getFrameNumber()</code> .  If 0, the request
-     * will be enqueued on the next available frame.
-     *
-     * @param completion To create a synchronous I/O request, this parameter must be NULL.  For an asynchronous request this
-     * paramater must be properly filled out prior to calling this method.  If not NULL, this parameter will be copied and
-     * can therefore be stack-allocated.
-     *
-     * @return IOReturn result code
+     * @brief       Enqueue or perform a request on an isochronous endpoint
+     * @discussion  
+     * This method is used to issue isochronous requests.  The caller allocates and initializes an array of IOUSBHostIsochronousFrame structures, which is used to describe the frames that will be transferred.  See @link IOUSBHostIsochronousFrame @/link for information regarding structure initialization requirements and usage.
+     * @param       dataBuffer Pointer to a valid memory descriptor to be used as the backing store for the I/O.
+     * @param       frameList Pointer first element in an IOUSBHostIsochronousFrame array.  The array must contain at least frameListCount elements.
+     * @param       frameListCount Number of elements in <code>frameList</code>.
+     * @param       firstFrameNumber Frame number which this request should begin on.  The current frame number can be queried via <code>IOUSHostDevice::getFrameNumber()</code> or <code>IOUSBHostInterface::getFrameNumber()</code>.  If 0, the transfer will start on the next available frame (XHCI only).
+     * @param       completion To create a synchronous I/O request, this parameter must be NULL.  For an asynchronous request this paramater must be properly filled out prior to calling this method.  If not NULL, this parameter will be copied and can therefore be stack-allocated.
+     * @return      IOReturn result code
      */
     virtual IOReturn io(IOMemoryDescriptor* dataBuffer, IOUSBHostIsochronousFrame* frameList, uint32_t frameListCount, uint64_t firstFrameNumber = 0, IOUSBHostIsochronousCompletion* completion = NULL);
     
@@ -545,45 +487,29 @@
 #pragma mark Streams
 public:
     /*!
-     * @methodgroup Streams
+     * @functiongroup Streams
+     * @discussion IOUSBHostPipe defines interfaces to enable and disable streams for an endpoint, and to create IOUSBHostStream objects.  See IOUSBHostStream.h for additional documentation.
      */
     
     /*!
-     * @brief Enable streams for the IOUSBHostPipe
-     * 
-     * @discussion This method changes the operational mode of the IOUSBHostPipe to allow streaming endpoint
-     * transfers, and must be called before copyStream will return any IOUSBHostStream objects.
-     *
-     * @return IOReturn result code.  An error will be returned if the pipe, device, or underlying host
-     * controller does not support streams.
+     * @brief       Enable streams for the IOUSBHostPipe
+     * @discussion  This method changes the operational mode of the IOUSBHostPipe to allow streaming endpoint transfers, and must be called before copyStream will return any IOUSBHostStream objects.
+     * @return      IOReturn result code.  An error will be returned if the pipe, device, or underlying host controller does not support streams.
      */
     virtual IOReturn enableStreams();
     
     /*!
-     * @brief Disable streams for the IOUSBHostPipe
-     *
-     * @discussion This method changes the operational mode of the IOUSBHostPipe to disable streaming endpoint
-     * transfers.  Calling this method will synchronously abort any outstanding calls on existing IOUSBHostStream
-     * objects, and therefore all stream contexts should first be set as non-active on the device via an out-of-band
-     * (class-defined) mechanism.
-     *
-     * @return IOReturn result code.  An error will be returned if streams were not enabled for this IOUSBHostPipe.
+     * @brief       Disable streams for the IOUSBHostPipe
+     * @discussion  This method changes the operational mode of the IOUSBHostPipe to disable streaming endpoint transfers.  Calling this method will synchronously abort any outstanding calls on existing IOUSBHostStream objects, and therefore all stream contexts should first be set as non-active on the device via an out-of-band (class-defined) mechanism (USB 3.1 8.12.1.4).
+     * @return      IOReturn result code.  An error will be returned if streams were not enabled for this IOUSBHostPipe.
      */
     virtual IOReturn disableStreams();
     
     /*!
-     * @brief Return the stream associated with <code>streamID</code>
-     *
-     * @discussion This method will return the stream associated with <code>streamID</code>.  If the stream
-     * doesn't exist yet it will be created.  This method returns a <code>retain()</code>ed object that must
-     * be <code>release()</code>ed by the caller.  <code>IOUSBHostPipe::enableStreams</code> must be called before
-     * this method will return a stream object.
-     *
-     * @param streamID Stream ID in the range of 1 to <code>max</code>, where <code>max</code> can be retrieved
-     * by calling <code>StandardUSB::getEndpointMaxStreams</code> with the endpoint descriptors.
-     *
-     * @return Pointer to a retain()ed IOUSBHostStream object or NULL.  NULL may be returned if either the device
-     * or the underlying host controller do not support that stream ID.
+     * @brief       Return the stream associated with <code>streamID</code>
+     * @discussion  This method will return the stream associated with <code>streamID</code>.  If the stream doesn't exist yet it will be created.  The caller must release the IOUSBHostStream when finished using it.  <code>IOUSBHostPipe::enableStreams</code> must be called before this method will return a stream object.
+     * @param       streamID Stream ID in the range of 1 to <code>max</code>, where <code>max</code> can be retrieved by calling <code>StandardUSB::getEndpointMaxStreams</code> with the endpoint descriptors.
+     * @return      Pointer to a retain()ed IOUSBHostStream object or NULL.  NULL may be returned if either the device or the underlying host controller do not support that stream ID.
      */
     virtual IOUSBHostStream* copyStream(uint32_t streamID);
     
@@ -624,8 +550,18 @@
     
 #pragma mark Miscellaneous
 public:
+    /*! @functiongroup Provider interfaces */
+
+    /*!
+     * @brief       Retrieve the device's operational speed
+     * @return      tInternalUSBHostConnectionSpeed
+     */
     virtual uint8_t getSpeed() const;
     
+    /*!
+     * @brief   Retrieve the device's address
+     * @return  Current address of the device
+     */
     virtual tUSBHostDeviceAddress getDeviceAddress() const;
     
     // Public pad slots for miscellaneous
@@ -663,142 +599,17 @@
 public:
     enum tPipeAbortOptions
     {
-        kIOUSBPipeAbortAsync = 0,
-        kIOUSBPipeAbortSync  = 1
+        kIOUSBPipeAbortAsync = IOUSBHostIOSource::kAbortAsynchronous,
+        kIOUSBPipeAbortSync  = IOUSBHostIOSource::kAbortSynchronous
     };
 
     enum tUSBPipeState
     {
-        kUSBPipeStateReady,
-        kUSBPipeStateRunningCompletions,
-        kUSBPipeStateAborting,
-        kUSBPipeStateInactive
+        kUSBPipeStateReady              = IOUSBHostIOSource::kStateReady,
+        kUSBPipeStateRunningCompletions = IOUSBHostIOSource::kStateRunningCompletions,
+        kUSBPipeStateAborting           = IOUSBHostIOSource::kStateAborting,
+        kUSBPipeStateInactive           = IOUSBHostIOSource::kStateInactive
     };
-    
-    // IOUSBHostPipe::tUSBPipeState GetPipeState() __attribute__((deprecated));
-    // Replacement: getState
-
-    // virtual IOReturn Abort(IOOptionBits options = kIOUSBPipeAbortAsync, IOReturn withError = kIOReturnAborted) __attribute__((deprecated));
-    // Replacement: abort
-
-    // virtual IOReturn Reset(void) __attribute__((deprecated));
-    // virtual IOReturn ClearStall(void) __attribute__((deprecated));
-    // Replacement: clearStall(false)
-
-    // virtual IOReturn ClearPipeStall(bool withDeviceRequest = false) __attribute__((deprecated));
-    // Replacement: clearStall
-
-    // virtual IOReturn Read(IOMemoryDescriptor* buffer,
-    //                       IOUSBCompletion*    completion = 0,
-    //                       UInt32*             bytesRead = 0) __attribute__((deprecated));
-    // virtual IOReturn Read(IOMemoryDescriptor* buffer,
-    //                       UInt64 frameStart, UInt32 numFrames, IOUSBIsocFrame* frameList,
-    //                       IOUSBIsocCompletion* completion = 0) __attribute__((deprecated));
-    // virtual IOReturn Read(IOMemoryDescriptor* buffer,
-    //                       UInt32              noDataTimeout,
-    //                       UInt32              completionTimeout,
-    //                       IOUSBCompletion*    completion = 0,
-    //                       UInt32*             bytesRead = 0) __attribute__((deprecated));
-    // virtual IOReturn Read(IOMemoryDescriptor* buffer,
-    //                       UInt64 frameStart, UInt32 numFrames, IOUSBLowLatencyIsocFrame* frameList,
-    //                       IOUSBLowLatencyIsocCompletion*       completion = 0, UInt32 updateFrequency = 0) __attribute__((deprecated));
-    // virtual IOReturn Read(IOMemoryDescriptor* buffer,
-    //                       UInt32              noDataTimeout,
-    //                       UInt32              completionTimeout,
-    //                       IOByteCount         reqCount,
-    //                       IOUSBCompletion*    completion = 0,
-    //                       UInt32*             bytesRead = 0) __attribute__((deprecated));
-    // virtual IOReturn Read(IOMemoryDescriptor*           buffer,
-    //                       UInt32                        noDataTimeout,
-    //                       UInt32                        completionTimeout,
-    //                       IOByteCount                   reqCount,
-    //                       IOUSBCompletionWithTimeStamp* completion = 0,
-    //                       UInt32*                       bytesRead = 0) __attribute__((deprecated));
-    // virtual IOReturn Write(IOMemoryDescriptor* buffer,
-    //                        IOUSBCompletion*    completion = 0) __attribute__((deprecated));
-    // virtual IOReturn Write(IOMemoryDescriptor* buffer,
-    //                        UInt64 frameStart, UInt32 numFrames, IOUSBIsocFrame* frameList,
-    //                        IOUSBIsocCompletion* completion = 0) __attribute__((deprecated));
-    // virtual IOReturn Write(IOMemoryDescriptor* buffer,
-    //                        UInt32              noDataTimeout,
-    //                        UInt32              completionTimeout,
-    //                        IOUSBCompletion*    completion = 0) __attribute__((deprecated));
-    // virtual IOReturn Write(IOMemoryDescriptor* buffer,
-    //                        UInt32              noDataTimeout,
-    //                        UInt32              completionTimeout,
-    //                        IOByteCount         reqCount,
-    //                        IOUSBCompletion*    completion = 0) __attribute__((deprecated));
-    // virtual IOReturn Write(IOMemoryDescriptor* buffer,
-    //                        UInt64 frameStart, UInt32 numFrames, IOUSBLowLatencyIsocFrame* frameList,
-    //                        IOUSBLowLatencyIsocCompletion* completion = 0, UInt32 updateFrequency = 0) __attribute__((deprecated));
-    // Replacement: io
-
-    // virtual IOReturn ControlRequest(IOUSBDevRequestDesc* request, IOUSBCompletion* completion = NULL,
-    //                                 UInt32 noDataTimeout = kUSBHostDefaultControlNoDataTimeoutMS, UInt32 completionTimeout = kUSBHostDefaultControlCompletionTimeoutMS) __attribute__((deprecated));
-    // virtual IOReturn ControlRequest(IOUSBDevRequest* request, IOUSBCompletion* completion = NULL) __attribute__((deprecated));
-    // virtual IOReturn ControlRequest(IOUSBDevRequestDesc* request, UInt32 noDataTimeout, UInt32 completionTimeout, IOUSBCompletion* completion = 0) __attribute__((deprecated));
-    // virtual IOReturn ControlRequest(IOUSBDevRequest* request, UInt32 noDataTimeout, UInt32 completionTimeout, IOUSBCompletion* completion = 0) __attribute__((deprecated));
-    // Replacement: controlRequest
-
-    // virtual const AppleUSBHostController::Endpoint* GetEndpoint() __attribute__((deprecated));
-    // virtual const StandardUSB::EndpointDescriptor* GetEndpointDescriptor(tGetEndpointDescriptorOptions type = kGetEndpointDescriptorOriginal) __attribute__((deprecated));
-    // virtual const StandardUSB::SuperSpeedEndpointCompanionDescriptor* GetEndpointCompanionDescriptor(tGetEndpointDescriptorOptions type = kGetEndpointDescriptorOriginal) __attribute__((deprecated));
-    // virtual UInt8 GetDirection() __attribute__((deprecated));
-    // virtual UInt8 GetType() __attribute__((deprecated));
-    // virtual UInt8            GetEndpointNumber() __attribute__((deprecated));
-    // virtual UInt16           GetMaxPacketSize() __attribute__((deprecated));
-    // virtual UInt16           GetBurstSize() __attribute__((deprecated));
-    // virtual UInt8            GetInterval() __attribute__((deprecated));
-    // Replacement: getEndpointDescriptor and getEndpointCompanionDescriptor
-
-    // virtual tUSBHostDeviceAddress GetAddress() __attribute__((deprecated));
-    // Replacement: getDeviceAddress
-    
-    // virtual UInt8            GetSpeed() __attribute__((deprecated));
-    // Replacement: getSpeed
-    
-    // virtual IOReturn GetPipeStatus(void) __attribute__((deprecated));
-    // Replacement: none
-
-    // virtual IOReturn SetPipePolicy(UInt16 maxPacketSize, UInt8 maxInterval) __attribute__((deprecated));
-    // Replacement: adjustPipe
-
-    // virtual void OverrideIdlePolicy(bool override, UInt32 ioIdleTimeout = 0) __attribute__((deprecated));
-    // Replacement: setIdlePolicy
-
-    // virtual void GetIdlePolicy(UInt32& ioIdleTimeout) __attribute__((deprecated));
-    // Replacement: setIdlePolicy
-
-    // virtual IOReturn Read(UInt32              streamID,
-    //                       IOMemoryDescriptor* buffer,
-    //                       UInt32              noDataTimeout,
-    //                       UInt32              completionTimeout,
-    //                       IOByteCount         reqCount,
-    //                       IOUSBCompletion*    completion = 0,
-    //                       IOByteCount*        bytesRead = 0) __attribute__((deprecated));
-    // virtual IOReturn Write(UInt32              streamID,
-    //                        IOMemoryDescriptor* buffer,
-    //                        UInt32              noDataTimeout,
-    //                        UInt32              completionTimeout,
-    //                        IOByteCount         reqCount,
-    //                        IOUSBCompletion*    completion = 0) __attribute__((deprecated));
-    // virtual IOReturn Abort(UInt32 streamID, IOOptionBits options, IOReturn withError) __attribute__((deprecated));
-    // virtual UInt32 GetConfiguredStreams(void) __attribute__((deprecated));
-    // Replacement: copyStream and IOUSBHostStream interfaces
-
-    // virtual UInt32 SupportsStreams(void) __attribute__((deprecated));
-    // Replacement: StandardUSB::getEndpointMaxStreams
-
-    // virtual IOReturn CreateStreams(UInt32 maxStreams) __attribute__((deprecated));
-    // Replacement: enableStreams
-    
-    // virtual const StandardUSB::SuperSpeedEndpointCompanionDescriptor* GetSuperSpeedEndpointCompanionDescriptor(tGetEndpointDescriptorOptions type = kGetEndpointDescriptorOriginal) __attribute__((deprecated));
-    // Replacement: getSuperSpeedEndpointCompanionDescriptor
-
-    // virtual UInt8 GetMaxBurst() __attribute__((deprecated));
-    // virtual UInt8 GetMult() __attribute__((deprecated));
-    // virtual UInt16 GetBytesPerInterval() __attribute__((deprecated));
-    // Replacement: StandardUSB::getEndpoint*
 };
 
 #endif // IOUSBHostFamily_IOUSBHostPipe_h
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostStream.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostStream.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostStream.h	2016-06-29 01:13:25.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostStream.h	2016-07-10 09:02:55.000000000 +0200
@@ -1,10 +1,35 @@
-//
-//  IOUSBHostStream.h
-//  IOUSBHostFamily
-//
-//  Created by Dan Wilson on 2/13/14.
-//
-//
+/*
+ * Copyright (c) 1998-2016 Apple Inc. All rights reserved.
+ *
+ * @APPLE_OSREFERENCE_LICENSE_HEADER_START@
+ *
+ * This file contains Original Code and/or Modifications of Original Code
+ * as defined in and that are subject to the Apple Public Source License
+ * Version 2.0 (the 'License'). You may not use this file except in
+ * compliance with the License. The rights granted to you under the License
+ * may not be used to create, or enable the creation or redistribution of,
+ * unlawful or unlicensed copies of an Apple operating system, or to
+ * circumvent, violate, or enable the circumvention or violation of, any
+ * terms of an Apple operating system software license agreement.
+ *
+ * Please obtain a copy of the License at
+ * http://www.opensource.apple.com/apsl/ and read it before using this file.
+ *
+ * The Original Code and all software distributed under the License are
+ * distributed on an 'AS IS' basis, WITHOUT WARRANTY OF ANY KIND, EITHER
+ * EXPRESS OR IMPLIED, AND APPLE HEREBY DISCLAIMS ALL SUCH WARRANTIES,
+ * INCLUDING WITHOUT LIMITATION, ANY WARRANTIES OF MERCHANTABILITY,
+ * FITNESS FOR A PARTICULAR PURPOSE, QUIET ENJOYMENT OR NON-INFRINGEMENT.
+ * Please see the License for the specific language governing rights and
+ * limitations under the License.
+ *
+ * @APPLE_OSREFERENCE_LICENSE_HEADER_END@
+ */
+
+/*!
+ @header     IOUSBHostStream.h
+ @brief      IOUSBHostStream is an object representing an individual stream within a streaming endpoint.
+ */
 
 #ifndef IOUSBHostFamily_IOUSBHostStream_h
 #define IOUSBHostFamily_IOUSBHostStream_h
@@ -14,6 +39,11 @@
 
 class IOUSBHostPipe;
 
+/*!
+ * @class       IOUSBHostStream
+ * @brief       The OSObject representing an individual stream within a USB endpoint
+ * @discussion  This class provides functionality to transfer data across USB.  Function drivers should not subclass IOUSBHostStream.
+ */
 class IOUSBHostStream : public IOUSBHostIOSource
 {
     OSDeclareDefaultStructors(IOUSBHostStream)
@@ -21,39 +51,48 @@
     friend class IOUSBHostPipe;
 
 public:
+    /*!
+     * @brief       Factory method for creating an IOUSBHostStream object
+     * @discussion  This method should not be called by function drivers.  To create an IOUSBHostStream, use IOUSBHostPipe::copyStream(...)
+     * @param       controller AppleUSBHostController to which the USB endpoint is associated
+     * @param       device IOUSBHostDevice to which this endpoint belongs
+     * @param       pipe IOUSBHostPipe to which this stream belongs
+     * @param       streamID The stream ID for this instance
+     * @return      Pointer to an IOUSBHostStream object if successful, otherwise NULL
+     */
     IOUSBHostStream* withOwnersAndStreamID(AppleUSBHostController* controller, IOUSBHostDevice* device, IOUSBHostPipe* pipe, uint32_t streamID);
 
     virtual void free();
     
     /*!
-     * @brief Abort pending I/O requests
-     *
-     * @discussion See IOUSBHostIOSource::abort for documentation
-     * 
-     * A stream context must be set as non-active on the device via an out-of-band (class-defined) mechanism before this method is called.
-     * A non-active stream will not be selected by the device to become the current stream on the endpoint.
+     * @brief       Abort pending I/O requests.
+     * @discussion  See IOUSBHostIOSource::abort for documentation.  A stream context must be set as non-active on the device via an out-of-band (class-defined) mechanism before this method is called (USB 3.1 8.12.1.4).  A non-active stream will not be selected by the device to become the current stream on the endpoint.
      */
     virtual IOReturn abort(IOOptionBits options = kAbortAsynchronous, IOReturn withError = kIOReturnAborted, IOService* forClient = NULL);
 
+    /*!
+     * @brief       Retrieve the IOUSBHostPipe to which this stream belongs
+     * @return      IOUSBHostPipe pointer
+     */
     virtual IOUSBHostPipe* getPipe() const { return _pipe; }
 
+    /*!
+     * @brief       Retrieve the sream ID for this instance
+     * @return      Stream ID
+     */
     virtual uint32_t getStreamID() const { return _streamID; }
     
-    /*!
-     * @brief Issue an asynchronous I/O request
-     *
-     * @discussion See IOUSBHostIOSource::io for documentation
-     *
-     * @param completionTimeoutMs Must be 0 for streams
+     /*!
+     * @brief       Enqueue a request on a stream
+     * @discussion  See IOUSBHostIOSource::io for documentation
+     * @param       completionTimeoutMs Must be 0 for streams.
      */
     virtual IOReturn io(IOMemoryDescriptor* dataBuffer, uint32_t dataBufferLength, IOUSBHostCompletion* completion, uint32_t completionTimeoutMs = 0);
     
     /*!
-     * @brief Issue a synchronous I/O request
-     *
-     * @discussion See IOUSBHostIOSource::io for documentation
-     *
-     * @param completionTimeoutMs Must be 0 for streams
+     * @brief       Perform a request on a stream
+     * @discussion  See IOUSBHostIOSource::io for documentation
+     * @param       completionTimeoutMs Must be 0 for streams.
      */
     virtual IOReturn io(IOMemoryDescriptor* dataBuffer, uint32_t dataBufferLength, uint32_t& bytesTransferred, uint32_t completionTimeoutMs = 0);
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/StandardUSB.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/StandardUSB.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/StandardUSB.h	2016-06-29 01:13:25.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/StandardUSB.h	2016-07-10 09:02:55.000000000 +0200
@@ -1,17 +1,41 @@
-//
-//  StandardUSB.h
-//  IOUSBHostFamily
-//
-//  Created by Dan Wilson on 12/11/13.
-//
-//
+/*
+ * Copyright (c) 1998-2016 Apple Inc. All rights reserved.
+ *
+ * @APPLE_OSREFERENCE_LICENSE_HEADER_START@
+ *
+ * This file contains Original Code and/or Modifications of Original Code
+ * as defined in and that are subject to the Apple Public Source License
+ * Version 2.0 (the 'License'). You may not use this file except in
+ * compliance with the License. The rights granted to you under the License
+ * may not be used to create, or enable the creation or redistribution of,
+ * unlawful or unlicensed copies of an Apple operating system, or to
+ * circumvent, violate, or enable the circumvention or violation of, any
+ * terms of an Apple operating system software license agreement.
+ *
+ * Please obtain a copy of the License at
+ * http://www.opensource.apple.com/apsl/ and read it before using this file.
+ *
+ * The Original Code and all software distributed under the License are
+ * distributed on an 'AS IS' basis, WITHOUT WARRANTY OF ANY KIND, EITHER
+ * EXPRESS OR IMPLIED, AND APPLE HEREBY DISCLAIMS ALL SUCH WARRANTIES,
+ * INCLUDING WITHOUT LIMITATION, ANY WARRANTIES OF MERCHANTABILITY,
+ * FITNESS FOR A PARTICULAR PURPOSE, QUIET ENJOYMENT OR NON-INFRINGEMENT.
+ * Please see the License for the specific language governing rights and
+ * limitations under the License.
+ *
+ * @APPLE_OSREFERENCE_LICENSE_HEADER_END@
+ */
+
+/*! @header     StandardUSB.h
+    @brief      StandardUSB defines structures and constants to reflect the USB specification
+ */
 
 #ifndef IOUSBHostFamily_StandardUSB_h
 #define IOUSBHostFamily_StandardUSB_h
 
 #include <IOKit/IOTypes.h>
-#include <libkern/OSByteOrder.h>
 #include <IOKit/IOReturn.h>
+#include <libkern/OSByteOrder.h>
 
 #pragma mark Platform endianness and bitmask macros
 
@@ -38,8 +62,11 @@
 #endif // __cplusplus
     
 #pragma mark Descriptor definitions
-    // USB 2.0 Table 9-5
-    // USB 3.0 Table 9-6
+    /*!
+     * @enum        tDescriptorType
+     * @namespace   StandardUSB
+     * @brief       Descriptor types defined by USB 2.0 Table 9-5 and USB 3.0 Table 9-6
+     */
     enum tDescriptorType
     {
         kDescriptorTypeDevice = 1,
@@ -62,7 +89,12 @@
     };
     
     typedef enum tDescriptorType tDescriptorType;
-    
+
+    /*!
+     * @enum        tDescriptorSize
+     * @namespace   StandardUSB
+     * @brief       Size in bytes for descriptor structures
+     */
     enum tDescriptorSize
     {
         kDescriptorSize = 2,
@@ -89,8 +121,13 @@
     };
     
     typedef enum tDescriptorSize tDescriptorSize;
-    
-    // USB 2.0 9.5: Descriptors
+
+    /*!
+     * @struct      Descriptor
+     * @namespace   StandardUSB
+     * @brief       Base descriptor defined by USB 2.0 9.5
+     * @discussion  StandardUSB.h declares structs to represent a variety of USB standard descriptors.  Each of thes structs is derived from the Descriptor base struct, and can therefore be passed to methods accepting a Descriptor pointer without explicit casting.  For the C language, each struct is defined independently to include the bLength and bDescriptorType fields expected for all USB descriptors.
+     */
     struct Descriptor
     {
         uint8_t bLength;
@@ -646,54 +683,340 @@
     
 #ifdef __cplusplus
 #pragma mark Descriptor list parsing
+    /*!
+     * @brief       Get the next descriptor in a configuration descriptor
+     * @discussion  This method will advance currentDescriptor by its bLength, and validate that the new descriptor fits withing the bounds of configurationDescriptor.  Using NULL for currentDescriptor will return the first descriptor after the configuration descriptor.
+     * @param       configurationDescriptor Configuration descriptor that contains the descriptors to iterate through
+     * @param       currentDescriptor A descriptor pointer within the bounds of configurationDescriptor, or NULL
+     * @return      Descriptor pointer, or NULL if no descriptor can be returned
+     */
     const Descriptor* getNextDescriptor(const ConfigurationDescriptor* configurationDescriptor, const Descriptor* currentDescriptor);
+
+    /*!
+     * @brief       Find the next descriptor matching a given type within a configuration descriptor
+     * @discussion  This method uses getNextDescriptor, and further validates that the returned descriptor's bDescriptorType field matches the type parameter.
+     * @param       configurationDescriptor Configuration descriptor that contains the descriptors to iterate through
+     * @param       currentDescriptor A descriptor pointer within the bounds of configurationDescriptor, or NULL
+     * @param       type tDescriptorType representing the descriptor type to find
+     * @return      Descriptor pointer, or NULL if no matching descriptor can be found
+     */
     const Descriptor* getNextDescriptorWithType(const ConfigurationDescriptor* configurationDescriptor, const Descriptor* currentDescriptor, const uint8_t type);
+
+    /*!
+     * @brief       Get the next descriptor in a configuration descriptor that belongs to another container descriptor
+     * @discussion  This method uses getNextDescriptor, but will return NULL if another descriptor is found whose bDescriptorType field matches the value used for parentDescriptor's bDescriptorType.  Using NULL for currentDescriptor will return the first descriptor after parentDescriptor.
+     * @param       configurationDescriptor Configuration descriptor that contains the descriptors to iterate through
+     * @param       parentDescriptor A descriptor pointer within the bounds of configurationDescriptor
+     * @param       currentDescriptor A descriptor pointer within the bounds of configurationDescriptor, or NULL
+     * @return      Descriptor pointer, or NULL if no descriptor can be returned
+     */
     const Descriptor* getNextAssociatedDescriptor(const ConfigurationDescriptor* configurationDescriptor, const Descriptor* parentDescriptor, const Descriptor* currentDescriptor);
+
+    /*!
+     * @brief       Find the next descriptor matching a given type within a configuration descriptor that belongs to another container descriptor
+     * @discussion  This method uses getNextAssociatedDescriptor, and further validates that the returned descriptor's bDescriptorType field matches the type passed parameter.
+     * @param       configurationDescriptor Configuration descriptor that contains the descriptors to iterate through
+     * @param       parentDescriptor A descriptor pointer within the bounds of configurationDescriptor
+     * @param       currentDescriptor A descriptor pointer within the bounds of configurationDescriptor, or NULL
+     * @param       type tDescriptorType representing the descriptor type to find
+     * @return      Descriptor pointer, or NULL if no matching descriptor can be found
+     */
     const Descriptor* getNextAssociatedDescriptorWithType(const ConfigurationDescriptor* configurationDescriptor, const Descriptor* parentDescriptor, const Descriptor* currentDescriptor, const uint8_t type);
+
+    /*!
+     * @brief       Find the next interface association descriptor in a configuration descriptor
+     * @discussion  This method uses getNextDescriptorWithType to fetch the next interface association descriptor
+     * @param       configurationDescriptor Configuration descriptor that contains the descriptors to iterate through
+     * @param       currentDescriptor A descriptor pointer within the bounds of configurationDescriptor, or NULL
+     * @return      InterfaceAssociationDescriptor pointer, or NULL if no matching descriptor can be found
+     */
     const InterfaceAssociationDescriptor* getNextInterfaceAssociationDescriptor(const ConfigurationDescriptor* configurationDescriptor, const Descriptor* currentDescriptor);
+    
+    /*!
+     * @brief       Find the next interface descriptor in a configuration descriptor
+     * @discussion  This method uses getNextDescriptorWithType to fetch the next interface descriptor
+     * @param       configurationDescriptor Configuration descriptor that contains the descriptors to iterate through
+     * @param       currentDescriptor A descriptor pointer within the bounds of configurationDescriptor, or NULL
+     * @return      InterfaceDescriptor pointer, or NULL if no matching descriptor can be found
+     */
     const InterfaceDescriptor* getNextInterfaceDescriptor(const ConfigurationDescriptor* configurationDescriptor, const Descriptor* currentDescriptor);
+        
+    /*!
+     * @brief       Find the next endpoint descriptor associated with an interface descriptor
+     * @discussion  This method uses getNextAssociatedDescriptorWithType to fetch the next endpoint descriptor associated with a specific interface descriptor
+     * @param       configurationDescriptor Configuration descriptor that contains the descriptors to iterate through
+     * @param       interfaceDescriptor An interface descriptor within the bounds of configurationDescriptor
+     * @param       currentDescriptor A descriptor pointer within the bounds of configurationDescriptor, or NULL
+     * @return      EndpointDescriptor pointer, or NULL if no matching descriptor can be found
+     */
     const EndpointDescriptor* getNextEndpointDescriptor(const ConfigurationDescriptor* configurationDescriptor, const InterfaceDescriptor* interfaceDescriptor, const Descriptor* currentDescriptor);
     
+    /*!
+     * @brief       Get the next device capability descriptor in a BOS descriptor
+     * @discussion  This method will advance currentDescriptor by its bLength, and validate that the new descriptor fits withing the bounds of bosDescriptor.  Using NULL for currentDescriptor will return the first descriptor after the BOS descriptor.
+     * @param       bosDescriptor BOS descriptor that contains the descriptors to iterate through
+     * @param       currentDescriptor A descriptor pointer within the bounds of bosDescriptor, or NULL
+     * @return      DeviceCapabilityDescriptor pointer, or NULL if no descriptor can be returned
+     */
     const DeviceCapabilityDescriptor* getNextCapabilityDescriptor(const BOSDescriptor* bosDescriptor, const DeviceCapabilityDescriptor* currentDescriptor);
+    
+    /*!
+     * @brief       Find the next descriptor matching a given type within a BOS descriptor
+     * @discussion  This method uses getNextCapabilityDescriptor, and further validates that the returned descriptor's bDevCapabilityType field matches the type parameter.
+     * @param       bosDescriptor BOS descriptor that contains the descriptors to iterate through
+     * @param       currentDescriptor A descriptor pointer within the bounds of bosDescriptor, or NULL
+     * @param       type tDeviceCapabilityType representing the descriptor type to find
+     * @return      DeviceCapabilityDescriptor pointer, or NULL if no matching descriptor can be found
+     */
     const DeviceCapabilityDescriptor* getNextCapabilityDescriptorWithType(const BOSDescriptor* bosDescriptor, const DeviceCapabilityDescriptor* currentDescriptor, const uint8_t type);
+        
+    /*!
+     * @brief       Find the first USB20ExtensionCapabilityDescriptor in a BOS descriptor
+     * @discussion  This method uses getNextCapabilityDescriptorWithType to fetch the first USB20ExtensionCapabilityDescriptor
+     * @param       bosDescriptor BOS descriptor that contains the descriptors to iterate through
+     * @return      USB20ExtensionCapabilityDescriptor pointer, or NULL if no matching descriptor can be found
+     */
     const USB20ExtensionCapabilityDescriptor* getUSB20ExtensionDeviceCapabilityDescriptor(const BOSDescriptor* bosDescriptor);
+
+    /*!
+     * @brief       Find the first SuperSpeedUSBDeviceCapabilityDescriptor in a BOS descriptor
+     * @discussion  This method uses getNextCapabilityDescriptorWithType to fetch the first SuperSpeedUSBDeviceCapabilityDescriptor
+     * @param       bosDescriptor BOS descriptor that contains the descriptors to iterate through
+     * @return      SuperSpeedUSBDeviceCapabilityDescriptor pointer, or NULL if no matching descriptor can be found
+     */
     const SuperSpeedUSBDeviceCapabilityDescriptor* getSuperSpeedDeviceCapabilityDescriptor(const BOSDescriptor* bosDescriptor);
+
+    /*!
+     * @brief       Find the first SuperSpeedPlusUSBDeviceCapabilityDescriptor in a BOS descriptor
+     * @discussion  This method uses getNextCapabilityDescriptorWithType to fetch the first SuperSpeedPlusUSBDeviceCapabilityDescriptor
+     * @param       bosDescriptor BOS descriptor that contains the descriptors to iterate through
+     * @return      SuperSpeedPlusUSBDeviceCapabilityDescriptor pointer, or NULL if no matching descriptor can be found
+     */
     const SuperSpeedPlusUSBDeviceCapabilityDescriptor* getSuperSpeedPlusDeviceCapabilityDescriptor(const BOSDescriptor* bosDescriptor);
+
+    /*!
+     * @brief       Find the first ContainerIDCapabilityDescriptor in a BOS descriptor
+     * @discussion  This method uses getNextCapabilityDescriptorWithType to fetch the first ContainerIDCapabilityDescriptor
+     * @param       bosDescriptor BOS descriptor that contains the descriptors to iterate through
+     * @return      ContainerIDCapabilityDescriptor pointer, or NULL if no matching descriptor can be found
+     */
     const ContainerIDCapabilityDescriptor* getContainerIDDescriptor(const BOSDescriptor* bosDescriptor);
+        
+    /*!
+     * @brief       Find the first BillboardCapabilityDescriptor in a BOS descriptor
+     * @discussion  This method uses getNextCapabilityDescriptorWithType to fetch the first BillboardCapabilityDescriptor
+     * @param       bosDescriptor BOS descriptor that contains the descriptors to iterate through
+     * @return      BillboardCapabilityDescriptor pointer, or NULL if no matching descriptor can be found
+     */
     const BillboardCapabilityDescriptor* getBillboardDescriptor(const BOSDescriptor* bosDescriptor);
 
 #pragma mark Device descriptor parsing
+    /*!
+     * @brief       Validate the contents of a device descriptor
+     * @discussion  This method parses a device descriptor and validates its contents.  If repairable validation errors are encountered, the descriptor passed in may be modified.
+     * @param       usbDeviceSpeed The operational speed of the device
+     * @param       descriptor The descriptor to validate
+     * @return      bool true if the descriptor passed validation, false if it did not
+     */
     bool validateDeviceDescriptor(uint32_t usbDeviceSpeed, const DeviceDescriptor* descriptor);
     
 #pragma mark Endpoint descriptor parsing
+    /*!
+     * @brief       Extract the direction of an endpoint from an endpoint descriptor
+     * @discussion  This method parses an endpoint descriptor to determine its transfer direction
+     * @param       descriptor The descriptor to parse
+     * @return      tEndpointDirection indicating the direction found.  Control endpoints return tEndpointDirection.
+     */
     uint8_t getEndpointDirection(const EndpointDescriptor* descriptor);
+        
+    /*!
+     * @brief       Extract the direction and number of an endpoint from an endpoint descriptor
+     * @discussion  This method parses an endpoint descriptor to determine its address
+     * @param       descriptor The descriptor to parse
+     * @return      uint8_t representing direction and endpoint number
+     */
     uint8_t getEndpointAddress(const EndpointDescriptor* descriptor);
+    
+    /*!
+     * @brief       Extract the number of an endpoint from an endpoint descriptor
+     * @discussion  This method parses an endpoint descriptor to determine its number, excluding direction
+     * @param       descriptor The descriptor to parse
+     * @return      uint8_t representing endpoint number
+     */
     uint8_t getEndpointNumber(const EndpointDescriptor* descriptor);
+        
+    /*!
+     * @brief       Extract the type of an endpoint from an endpoint descriptor
+     * @discussion  This method parses an endpoint descriptor to determine its type
+     * @param       descriptor The descriptor to parse
+     * @return      tEndpointType indicating the type found.
+     */
     uint8_t getEndpointType(const EndpointDescriptor* descriptor);
+        
+    /*!
+     * @brief       Validate the max packet size of an endpoint descriptor
+     * @discussion  This method parses an endpoint descriptor and validates the max packet size.  If repairable validation errors are encountered, the descriptor passed in may be modified.
+     * @param       usbDeviceSpeed The operational speed of the device
+     * @param       descriptor The descriptor to validate
+     * @return      bool true if the descriptor passed validation, false if it did not
+     */
     bool validateEndpointMaxPacketSize(uint32_t usbDeviceSpeed, const EndpointDescriptor* descriptor);
+        
+    /*!
+     * @brief       Extract the max packet size from an endpoint descriptor
+     * @discussion  This method parses an endpoint descriptor to determine its max packet size, which does not take into account mult or burst factors.
+     * @param       usbDeviceSpeed The operational speed of the device
+     * @param       descriptor The descriptor to parse
+     * @return      uint16_t The max packet size in bytes
+     */
     uint16_t getEndpointMaxPacketSize(uint32_t usbDeviceSpeed, const EndpointDescriptor* descriptor);
+        
+    /*!
+     * @brief       Validate the burst size of endpoint descriptors
+     * @discussion  This method parses endpoint descriptors and validates the burst size.  If repairable validation errors are encountered, the descriptors passed in may be modified.
+     * @param       usbDeviceSpeed The operational speed of the device
+     * @param       descriptor The EndpointDescriptor to validate
+     * @param       companionDescriptor The SuperSpeedEndpointCompanionDescriptor to validate, or NULL
+     * @return      bool true if the descriptor passed validation, false if it did not
+     */
     bool validateEndpointBurstSize(uint32_t usbDeviceSpeed, const EndpointDescriptor* descriptor, const SuperSpeedEndpointCompanionDescriptor* companionDescriptor);
+        
+    /*!
+     * @brief       Validate the burst size of endpoint descriptors
+     * @discussion  This method parses endpoint descriptors and validates the burst size.  If repairable validation errors are encountered, the descriptors passed in may be modified.
+     * @param       usbDeviceSpeed The operational speed of the device
+     * @param       descriptor The EndpointDescriptor to validate
+     * @param       companionDescriptor The SuperSpeedEndpointCompanionDescriptor to validate, or NULL
+     * @param       sspCompanionDescriptor The SuperSpeedPlusIsochronousEndpointCompanionDescriptor to validate, or NULL
+     * @return      bool true if the descriptor passed validation, false if it did not
+     */
     bool validateEndpointBurstSize(uint32_t usbDeviceSpeed,
                                    const EndpointDescriptor* descriptor,
                                    const SuperSpeedEndpointCompanionDescriptor* companionDescriptor,
                                    const SuperSpeedPlusIsochronousEndpointCompanionDescriptor* sspCompanionDescriptor);
+    
+    /*!
+     * @brief       Extract the burst size from endpoint descriptors
+     * @discussion  This method parses endpoint descriptors to determine burst size, which includes mult and burst factors as applicable.
+     * @param       usbDeviceSpeed The operational speed of the device
+     * @param       descriptor The EndpointDescriptor to parse
+     * @param       companionDescriptor The SuperSpeedEndpointCompanionDescriptor to parse, or NULL
+     * @return      uint16_t The burst size in bytes
+     */
     uint16_t getEndpointBurstSize(uint32_t usbDeviceSpeed, const EndpointDescriptor* descriptor, const SuperSpeedEndpointCompanionDescriptor* companionDescriptor);
+        
+    /*!
+     * @brief       Extract the burst size from endpoint descriptors
+     * @discussion  This method parses endpoint descriptors to determine burst size, which includes mult and burst factors as applicable.  SuperSpeed Plus isochronous endpoints will return the dwBytesPerInterval field from the SuperSpeedPlusIsochronousEndpointCompanionDescriptor parameter.
+     * @param       usbDeviceSpeed The operational speed of the device
+     * @param       descriptor The EndpointDescriptor to parse
+     * @param       companionDescriptor The SuperSpeedEndpointCompanionDescriptor to parse, or NULL
+     * @param       sspCompanionDescriptor The SuperSpeedPlusIsochronousEndpointCompanionDescriptor to parse, or NULL
+     * @return      uint32_t The burst size in bytes
+     */
     uint32_t getEndpointBurstSize32(uint32_t usbDeviceSpeed,
                                     const EndpointDescriptor* descriptor,
                                     const SuperSpeedEndpointCompanionDescriptor* companionDescriptor = NULL,
                                     const SuperSpeedPlusIsochronousEndpointCompanionDescriptor* sspCompanionDescriptor = NULL);
+        
+    /*!
+     * @brief       Extract the mult count from endpoint descriptors
+     * @discussion  This method parses endpoint descriptors to determine mult
+     * @param       usbDeviceSpeed The operational speed of the device
+     * @param       descriptor The EndpointDescriptor to parse
+     * @param       companionDescriptor The SuperSpeedEndpointCompanionDescriptor to parse, or NULL
+     * @param       sspCompanionDescriptor The SuperSpeedPlusIsochronousEndpointCompanionDescriptor to parse, or NULL
+     * @return      uint8_t The mult count
+     */
     uint8_t getEndpointMult(uint32_t usbDeviceSpeed,
                             const EndpointDescriptor* descriptor,
                             const SuperSpeedEndpointCompanionDescriptor* companionDescriptor = NULL,
                             const SuperSpeedPlusIsochronousEndpointCompanionDescriptor* sspCompanionDescriptor = NULL);
+        
+    /*!
+     * @brief       Validate the interval of an endpoint descriptor
+     * @discussion  This method parses an endpoint descriptor and validates the interval.  If repairable validation errors are encountered, the descriptor passed in may be modified.
+     * @param       usbDeviceSpeed The operational speed of the device
+     * @param       descriptor The EndpointDescriptor to validate
+     * @return      bool true if the descriptor passed validation, false if it did not
+     */
     bool validateEndpointInterval(uint32_t usbDeviceSpeed, const EndpointDescriptor* descriptor);
+        
+    /*!
+     * @brief       Extract the interval of an endpoint descriptor
+     * @discussion  This method parses an endpoint descriptor and returns the service interval as n in (2^(n-1)) microframes
+     * @param       usbDeviceSpeed The operational speed of the device
+     * @param       descriptor The EndpointDescriptor to parse
+     * @return      uint32_t Encoded endpoint interval
+     */
     uint32_t getEndpointIntervalEncodedMicroframes(uint32_t usbDeviceSpeed, const EndpointDescriptor* descriptor);
+
+    /*!
+     * @brief       Extract the interval of an endpoint descriptor
+     * @discussion  This method parses an endpoint descriptor and returns the service interval in microframes
+     * @param       usbDeviceSpeed The operational speed of the device
+     * @param       descriptor The EndpointDescriptor to parse
+     * @return      uint32_t Endpoint interval in microframes
+     */
     uint32_t getEndpointIntervalMicroframes(uint32_t usbDeviceSpeed, const EndpointDescriptor* descriptor);
+        
+    /*!
+     * @brief       Extract the interval of an endpoint descriptor
+     * @discussion  This method parses an endpoint descriptor and returns the service interval in frames
+     * @param       usbDeviceSpeed The operational speed of the device
+     * @param       descriptor The EndpointDescriptor to parse
+     * @return      uint32_t Endpoint interval in frames
+     */
     uint32_t getEndpointIntervalFrames(uint32_t usbDeviceSpeed, const EndpointDescriptor* descriptor);
+        
+    /*!
+     * @brief       Extract the number of streams supported by an endpoint
+     * @discussion  This method parses endpoint descriptors and returns the number of streams supported as n in (2^n)
+     * @param       usbDeviceSpeed The operational speed of the device
+     * @param       descriptor The EndpointDescriptor to parse
+     * @param       companionDescriptor The SuperSpeedEndpointCompanionDescriptor to parse
+     * @return      uint32_t Encoded number of streams
+     */
     uint32_t getEndpointMaxStreamsEncoded(uint32_t usbDeviceSpeed, const EndpointDescriptor* descriptor, const SuperSpeedEndpointCompanionDescriptor* companionDescriptor);
+
+    /*!
+     * @brief       Extract the number of streams supported by an endpoint
+     * @discussion  This method parses endpoint descriptors and returns the number of streams supported
+     * @param       usbDeviceSpeed The operational speed of the device
+     * @param       descriptor The EndpointDescriptor to parse
+     * @param       companionDescriptor The SuperSpeedEndpointCompanionDescriptor to parse
+     * @return      uint32_t Number of streams
+     */
     uint32_t getEndpointMaxStreams(uint32_t usbDeviceSpeed, const EndpointDescriptor* descriptor, const SuperSpeedEndpointCompanionDescriptor* companionDescriptor);
+        
+    /*!
+     * @brief       Extract the maximum bus current required by a configuration descriptor
+     * @discussion  This method parses a configuration descriptor and returns the number of milliamps required to power the device
+     * @param       usbDeviceSpeed The operational speed of the device
+     * @param       descriptor The ConfigurationDescriptor to parse
+     * @return      uint32_t milliamps required
+     */
     uint32_t getConfigurationMaxPowerMilliAmps(uint32_t usbDeviceSpeed, const ConfigurationDescriptor* descriptor);
+        
+    /*!
+     * @brief       Validate the contents of an endpoint descriptor
+     * @discussion  This method parses an endpoint descriptor and validates its contents.  If repairable validation errors are encountered, the descriptor passed in may be modified.
+     * @param       usbDeviceSpeed The operational speed of the device
+     * @param       descriptor The EndpointDescriptor to validate
+     * @param       companionDescriptor The SuperSpeedEndpointCompanionDescriptor to validate, or NULL
+     * @return      bool true if the descriptor passed validation, false if it did not
+     */
     bool validateEndpointDescriptor(uint32_t usbDeviceSpeed, const EndpointDescriptor* descriptor, const SuperSpeedEndpointCompanionDescriptor* companionDescriptor);
+        
+    /*!
+     * @brief       Validate the contents of an endpoint descriptor
+     * @discussion  This method parses an endpoint descriptor and validates its contents.  If repairable validation errors are encountered, the descriptor passed in may be modified.
+     * @param       usbDeviceSpeed The operational speed of the device
+     * @param       descriptor The EndpointDescriptor to validate
+     * @param       companionDescriptor The SuperSpeedEndpointCompanionDescriptor to validate, or NULL
+     * @param       sspCompanionDescriptor The SuperSpeedPlusIsochronousEndpointCompanionDescriptor to validate, or NULL
+     * @return      bool true if the descriptor passed validation, false if it did not
+     */
     bool validateEndpointDescriptor(uint32_t usbDeviceSpeed,
                                     const EndpointDescriptor* descriptor,
                                     const SuperSpeedEndpointCompanionDescriptor* companionDescriptor,
@@ -701,22 +1024,22 @@
     
 #pragma mark String descriptor parsing
     /*!
-     * @brief Convert a USB string descriptor to a UTF8 character string
-     *
-     * @discussion This method uses utf8_encodestr with appropriate options to convert a USB string descriptor to a UTF8 string.
-     *
-     * @param stringDescriptor Descriptor to convert
-     *
-     * @param stringBuffer Buffer to write the UTF8 string to
-     *
-     * @param length Reference to size_t.  As input it is the size stringBuffer.  As output it is the number of character written to stringBuffer.
-     *
-     * @return IOReturn result code.  kIOReturnSuccess if any portion of the string could be converted and placed in stringBuffer.  kIOReturnError if the
-     * string descriptor contains characters that cannot be converted to UTF8
+     * @brief       Convert a USB string descriptor to a UTF8 character string
+     * @discussion  This method uses utf8_encodestr with appropriate options to convert a USB string descriptor to a UTF8 string.
+     * @param       stringDescriptor Descriptor to convert
+     * @param       stringBuffer Buffer to write the UTF8 string to
+     * @param       length Reference to size_t.  As input it is the size stringBuffer.  As output it is the number of character written to stringBuffer.
+     * @return      IOReturn result code.  kIOReturnSuccess if any portion of the string could be converted and placed in stringBuffer.  kIOReturnError if the string descriptor cannot be converted to UTF8.
      */
     IOReturn stringDescriptorToUTF8(const StringDescriptor* stringDescriptor, char* stringBuffer, size_t& length);
     
 #pragma mark Capability descriptor parsing
+    /*!
+     * @brief       Validate the contents of a BOS descriptor
+     * @discussion  This method parses a BOS descriptor and validates its contents, as well as the contents of its associated device capability descriptors.  If repairable validation errors are encountered, the descriptor passed in may be modified.
+     * @param       bosDescriptor The BOSDescriptor to validate
+     * @return      bool true if the descriptor passed validation, false if it did not
+     */
     bool validateDeviceCapabilityDescriptors(const BOSDescriptor* bosDescriptor);
         
 #endif // __cplusplus
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/backtrace.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/backtrace.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/backtrace.h	2016-06-29 00:55:59.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/backtrace.h	2016-07-10 08:22:00.000000000 +0200
@@ -29,6 +29,7 @@
 #ifndef BACKTRACE_H
 #define BACKTRACE_H
 
+#include <stdbool.h>
 #include <stdint.h>
 #include <sys/cdefs.h>
 
@@ -46,9 +47,43 @@
  * up to max_frames return addresses in bt.  Returns the number of return
  * addresses stored.
  */
-uint32_t backtrace_fp(uintptr_t *bt, uint32_t max_frames, void *start_fp)
+uint32_t backtrace_frame(uintptr_t *bt, uint32_t max_frames, void *start_frame)
 	__attribute__((noinline,not_tail_called));
 
+/*
+ * Backtrace the kernel stack of the context that was interrupted, storing up
+ * to max_frames return addresses in bt.  Returns 0 on success, and non-zero
+ * otherwise.  On success, the number of frames written is stored at the value
+ * pointed to by frames_out.
+ *
+ * Must be called from interrupt context.
+ */
+uint32_t backtrace_interrupted(uintptr_t *bt, uint32_t max_frames);
+
+/*
+ * Backtrace the user stack of the current thread, storing up to max_frames
+ * return addresses in bt.  Returns 0 on success, and non-zero otherwise.  On
+ * success, the number of frames written is stored at the value pointed to by
+ * frames_out and the value pointed to by user_64_out is set true if the user
+ * space thread was running in 64-bit mode, and false otherwise.
+ *
+ * Must not be called from interrupt context or with interrupts disabled.
+ */
+int backtrace_user(uintptr_t *bt, uint32_t max_frames, uint32_t *frames_out,
+	bool *user_64_out);
+
+/*
+ * Backtrace the user stack of the given thread, storing up to max_frames return
+ * addresses in bt.  Returns 0 on success, and non-zero otherwise.  On success,
+ * the number of frames written is stored at the value pointed to by frames_out
+ * and the value pointed to by user_64_out is set true if the user space thread
+ * was running in 64-bit mode, and false otherwise.
+ *
+ * Must not be called from interrupt context or with interrupts disabled.
+ */
+int backtrace_thread_user(void *thread, uintptr_t *bt, uint32_t max_frames,
+	uint32_t *frames_out, bool *user_64_out);
+
 __END_DECLS
 
 #endif /* !defined(BACKTRACE_H) */
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/bits.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/bits.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/bits.h	2016-06-29 00:55:59.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/bits.h	2016-07-10 08:22:01.000000000 +0200
@@ -283,68 +283,4 @@
 	return -1;
 }
 
-#if DEVELOPMENT || DEBUG
-
-#ifdef XNU_TEST_BITMAP
-
-extern void dump_bitmap_next(bitmap_t *map, uint nbits);
-extern void dump_bitmap_lsb(bitmap_t *map, uint nbits);
-extern void test_bitmap(void);
-
-void
-dump_bitmap_next(bitmap_t *map, uint nbits)
-{
-	for (int i = bitmap_first(map, nbits); i >= 0; i = bitmap_next(map, i)) {
-		printf(" %d", i);
-	}
-	printf("\n");
-}
-
-void
-dump_bitmap_lsb(bitmap_t *map, uint nbits)
-{
-	for (int i = bitmap_lsb_first(map, nbits); i >= 0; i = bitmap_lsb_next(map, nbits, i)) {
-		printf(" %d", i);
-	}
-	printf("\n");
-}
-
-void
-test_bitmap(void)
-{
-	uint start = 60;
-	for (uint nbits = start; nbits <= 192; nbits++) {
-		bitmap_t *map = bitmap_alloc(nbits);
-
-		for (uint i = 0; i < nbits; i++) {
-			bitmap_set(map, i);
-		}
-
-		int expected_result = nbits - 1;
-		for (int i = bitmap_first(map, nbits); i >= 0; i = bitmap_next(map, i)) {
-			assert(i == expected_result);
-			expected_result--;
-		}
-		assert(expected_result == -1);
-
-		expected_result = 0;
-		for (int i = bitmap_lsb_first(map, nbits); i >= 0; i = bitmap_lsb_next(map, nbits, i)) {
-			assert(i == expected_result);
-			expected_result++;
-		}
-		assert(expected_result == (int)nbits);
-
-		for (uint i = 0; i < nbits; i++) {
-			bitmap_clear(map, i);
-		}
-		assert(bitmap_first(map, nbits) == -1);
-		assert(bitmap_lsb_first(map, nbits) == -1);
-
-		bitmap_free(map, nbits);
-	}
-}
-#endif
-
-#endif
-
 #endif
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/kcdata.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/kcdata.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/kcdata.h	2016-06-29 00:55:57.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/kcdata.h	2016-07-10 08:22:00.000000000 +0200
@@ -417,9 +417,13 @@
 #define KCDATA_BUFFER_BEGIN_DELTA_STACKSHOT 0xDE17A59Au /* owner: sys/stackshot.h */
                                                         /* type-range: 0x940 - 0x9ff */
 #define KCDATA_BUFFER_BEGIN_OS_REASON 0x53A20900u       /* owner: sys/reason.h */
-                                                        /* type-range: 0x1000-103f */
-
-/* next type range number available 0x1040 */
+                                                        /* type-range: 0x1000-0x103f */
+#define KCDATA_BUFFER_BEGIN_XNUPOST_CONFIG 0x1e21c09fu  /* owner: osfmk/tests/kernel_tests.c */
+                                                        /* type-range: 0x1040-0x105f */
+
+/* next type range number available 0x1060 */
+/**************** definitions for XNUPOST *********************/
+#define XNUPOST_KCTYPE_TESTCONFIG		0x1040
 
 /**************** definitions for stackshot *********************/
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/dyld_kernel.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/dyld_kernel.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/dyld_kernel.h	2016-06-29 00:56:16.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/dyld_kernel.h	2016-07-10 08:22:05.000000000 +0200
@@ -30,9 +30,8 @@
 #define _MACH_DYLIB_INFO_H_
 
 #include <mach/boolean.h>
-#include <sys/_types.h>
+#include <stdint.h>
 #include <sys/_types/_fsid_t.h>
-#include <sys/_types/_u_int8_t.h>
 #include <sys/_types/_u_int32_t.h>
 #include <sys/_types/_fsobj_id_t.h>
 #include <sys/_types/_uuid_t.h>
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach-o/loader.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach-o/loader.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach-o/loader.h	2016-06-29 00:55:54.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach-o/loader.h	2016-07-10 08:21:45.000000000 +0200
@@ -300,6 +300,7 @@
 #define	LC_ENCRYPTION_INFO_64 0x2C /* 64-bit encrypted segment information */
 #define LC_LINKER_OPTION 0x2D /* linker options in MH_OBJECT files */
 #define LC_LINKER_OPTIMIZATION_HINT 0x2E /* optimization hints in MH_OBJECT files */
+#define LC_VERSION_MIN_TVOS 0x2F /* build for AppleTV min OS version */
 #define LC_VERSION_MIN_WATCHOS 0x30 /* build for Watch min OS version */
 
 /*
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/netinet/ip_var.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/netinet/ip_var.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/netinet/ip_var.h	2016-06-29 00:56:06.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/netinet/ip_var.h	2016-07-10 08:21:55.000000000 +0200
@@ -126,6 +126,7 @@
 	u_int32_t ips_rxc_chainsz_gt2;	/* rx chain size greater than 2 */
 	u_int32_t ips_rxc_chainsz_gt4;  /* rx chain size greater than 4 */
 	u_int32_t ips_rxc_notlist;	/* count of pkts through ip_input */
+	u_int32_t ips_raw_sappend_fail;	/* sock append failed */
 
 };
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/netinet6/in6_var.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/netinet6/in6_var.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/netinet6/in6_var.h	2016-06-29 00:56:02.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/netinet6/in6_var.h	2016-07-10 08:21:53.000000000 +0200
@@ -469,6 +469,9 @@
 /* do not input/output */
 #define	IN6_IFF_NOTREADY	(IN6_IFF_TENTATIVE|IN6_IFF_DUPLICATED)
 
+/* SLAAC/DHCPv6 address */
+#define IN6_IFF_NOTMANUAL	(IN6_IFF_AUTOCONF|IN6_IFF_DYNAMIC)
+
 #define	IN6_ARE_SCOPE_CMP(a, b)		((a) - (b))
 #define	IN6_ARE_SCOPE_EQUAL(a, b)	((a) == (b))
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/netinet6/nd6.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/netinet6/nd6.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/netinet6/nd6.h	2016-06-29 00:56:03.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/netinet6/nd6.h	2016-07-10 08:21:53.000000000 +0200
@@ -135,6 +135,7 @@
 #define	NDDRF_INSTALLED	0x1	/* installed in the routing table */
 #define	NDDRF_IFSCOPE	0x2	/* installed as a scoped route */
 #define	NDDRF_STATIC	0x4	/* for internal use only */
+#define	NDDRF_MAPPED	0x8	/* Default router addr is mapped to a different one for routing */
 
 struct	in6_defrouter {
 	struct	sockaddr_in6 rtaddr;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/proc.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/proc.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/proc.h	2016-06-29 00:56:51.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/proc.h	2016-07-10 08:22:39.000000000 +0200
@@ -2,7 +2,7 @@
  * Copyright (c) 2000-2016 Apple Computer, Inc. All rights reserved.
  *
  * @APPLE_OSREFERENCE_LICENSE_HEADER_START@
- * 
+ *
  * This file contains Original Code and/or Modifications of Original Code
  * as defined in and that are subject to the Apple Public Source License
  * Version 2.0 (the 'License'). You may not use this file except in
@@ -11,10 +11,10 @@
  * unlawful or unlicensed copies of an Apple operating system, or to
  * circumvent, violate, or enable the circumvention or violation of, any
  * terms of an Apple operating system software license agreement.
- * 
+ *
  * Please obtain a copy of the License at
  * http://www.opensource.apple.com/apsl/ and read it before using this file.
- * 
+ *
  * The Original Code and all software distributed under the License are
  * distributed on an 'AS IS' basis, WITHOUT WARRANTY OF ANY KIND, EITHER
  * EXPRESS OR IMPLIED, AND APPLE HEREBY DISCLAIMS ALL SUCH WARRANTIES,
@@ -22,7 +22,7 @@
  * FITNESS FOR A PARTICULAR PURPOSE, QUIET ENJOYMENT OR NON-INFRINGEMENT.
  * Please see the License for the specific language governing rights and
  * limitations under the License.
- * 
+ *
  * @APPLE_OSREFERENCE_LICENSE_HEADER_END@
  */
 /* Copyright (c) 1995, 1997 Apple Computer, Inc. All Rights Reserved */
@@ -106,9 +106,9 @@
 extern int proc_issignal(int pid, sigset_t mask);
 /* this routine returns 1 if the pid1 is inferior of pid2 */
 extern int proc_isinferior(int pid1, int pid2);
-/* this routine copies the process's name of the executable to the passed in buffer. It 
- * is always null terminated. The size of the buffer is to be passed in as well. This 
- * routine is to be used typically for debugging 
+/* this routine copies the process's name of the executable to the passed in buffer. It
+ * is always null terminated. The size of the buffer is to be passed in as well. This
+ * routine is to be used typically for debugging
  */
 void proc_name(int pid, char * buf, int size);
 /* This routine is simillar to proc_name except it returns for current process */
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h	2016-06-29 00:56:55.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h	2016-07-10 08:22:42.000000000 +0200
@@ -29,7 +29,7 @@
  * System call switch table.
  *
  * DO NOT EDIT-- this file is automatically generated.
- * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3757.0.0.0.1/bsd/kern/syscalls.master
+ * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3777.0.0.0.1/bsd/kern/syscalls.master
  */
 
 #ifndef _SYS_SYSCALL_H_
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h	2016-06-29 00:56:55.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h	2016-07-10 08:22:42.000000000 +0200
@@ -29,7 +29,7 @@
  * System call switch table.
  *
  * DO NOT EDIT-- this file is automatically generated.
- * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3757.0.0.0.1/bsd/kern/syscalls.master
+ * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3777.0.0.0.1/bsd/kern/syscalls.master
  */
 
 #ifndef _SYS_SYSPROTO_H_
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vBasicOps.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vBasicOps.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vBasicOps.h	2016-06-29 01:09:47.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vBasicOps.h	2016-07-10 08:37:00.000000000 +0200
@@ -3,7 +3,7 @@
  
      Contains:   Basic Algebraic Operations for AltiVec
  
-     Version:    vecLib-599.0
+     Version:    vecLib-600.0
  
      Copyright:  Copyright (c) 1999-2016 by Apple Inc. All rights reserved.
  
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vDSP.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vDSP.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vDSP.h	2016-06-29 01:09:47.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vDSP.h	2016-07-10 08:37:00.000000000 +0200
@@ -3,7 +3,7 @@
 
     Contains:   AltiVec DSP Interfaces
 
-    Version:    vecLib-599.0
+    Version:    vecLib-600.0
 
     Copyright:  Copyright (c) 2000-2016 by Apple Inc. All rights reserved.
 
@@ -244,7 +244,7 @@
     vDSP_Version0 is a major version number.
     vDSP_Version1 is a minor version number.
 */
-#define vDSP_Version0   599
+#define vDSP_Version0   600
 #define vDSP_Version1   0
 
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vForce.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vForce.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vForce.h	2016-06-29 01:09:47.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vForce.h	2016-07-10 08:37:00.000000000 +0200
@@ -1,5 +1,5 @@
 /*
-vForce.h (from vecLib-599.0)
+vForce.h (from vecLib-600.0)
 Copyright (c) 1999-2016 by Apple Inc. All rights reserved.
 
 @APPLE_LICENSE_HEADER_START@
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vecLib.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vecLib.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vecLib.h	2016-06-29 01:09:47.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vecLib.h	2016-07-10 08:37:00.000000000 +0200
@@ -3,7 +3,7 @@
  
      Contains:   Master include for vecLib framework
  
-     Version:    vecLib-599.0
+     Version:    vecLib-600.0
  
      Copyright:  Copyright (c) 2000-2016 by Apple Inc. All rights reserved.
  
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vecLibTypes.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vecLibTypes.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vecLibTypes.h	2016-06-29 01:09:47.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vecLibTypes.h	2016-07-10 08:37:00.000000000 +0200
@@ -3,7 +3,7 @@
  
      Contains:   Master include for vecLib framework
  
-     Version:    vecLib-599.0
+     Version:    vecLib-600.0
  
      Copyright:  Copyright (c) 2000-2016 by Apple Inc. All rights reserved.
  

```