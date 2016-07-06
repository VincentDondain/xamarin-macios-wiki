#Kernel.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/Availability.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/Availability.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/Availability.h	2016-05-11 14:53:19.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/Availability.h	2016-06-26 05:16:33.000000000 +0200
@@ -1,5 +1,5 @@
 /*
- * Copyright (c) 2007-2015 by Apple Inc.. All rights reserved.
+ * Copyright (c) 2007-2016 by Apple Inc.. All rights reserved.
  *
  * @APPLE_LICENSE_HEADER_START@
  * 
@@ -351,4 +351,55 @@
 #endif
 
 
+/*
+ Macros for defining which versions/platform a given symbol can be used.
+ 
+ @see http://clang.llvm.org/docs/AttributeReference.html#availability
+ */
+
+/*
+ * API Introductions
+ *
+ * Use to specify the release that a particular API became available.
+ *
+ * Platform names:
+ *   macosx, ios, tvos, watchos
+ *
+ * Examples:
+ *    __API_AVAILABLE(macosx(10.10))
+ *    __API_AVAILABLE(macosx(10.9), ios(10.0))
+ *    __API_AVAILABLE(macosx(10.4), ios(8.0), watchos(2.0), tvos(10.0))
+ */
+#define __API_AVAILABLE(...) __API_AVAILABLE_GET_MACRO(__VA_ARGS__,__API_AVAILABLE4, __API_AVAILABLE3, __API_AVAILABLE2, __API_AVAILABLE1)(__VA_ARGS__)
+
+
+/*
+ * API Deprecations
+ *
+ * Use to specify the release that a particular API became unavailable.
+ *
+ * Platform names:
+ *   macosx, ios, tvos, watchos
+ *
+ * Examples:
+ *
+ *    __API_DEPRECATED("No longer supported", macosx(10.4, 10.8))
+ *    __API_DEPRECATED("No longer supported", macosx(10.4, 10.8), ios(2.0, 3.0), watchos(2.0, 3.0), tvos(9.0, 10.0))
+ *
+ *    __API_DEPRECATED_WITH_REPLACEMENT("-setName:", tvos(10.0, 10.4), ios(9.0, 10.0))
+ *    __API_DEPRECATED_WITH_REPLACEMENT("SomeClassName", macosx(10.4, 10.6), watchos(2.0, 3.0))
+ */
+#define __API_DEPRECATED(...) __API_DEPRECATED_MSG_GET_MACRO(__VA_ARGS__,__API_DEPRECATED_MSG5,__API_DEPRECATED_MSG4,__API_DEPRECATED_MSG3,__API_DEPRECATED_MSG2,__API_DEPRECATED_MSG1)(__VA_ARGS__)
+#define __API_DEPRECATED_WITH_REPLACEMENT(...) __API_DEPRECATED_REP_GET_MACRO(__VA_ARGS__,__API_DEPRECATED_REP5,__API_DEPRECATED_REP4,__API_DEPRECATED_REP3,__API_DEPRECATED_REP2,__API_DEPRECATED_REP1)(__VA_ARGS__)
+
+/*
+ * API Unavailability
+ * Use to specify that an API is unavailable for a particular platform.
+ *
+ * Example:
+ *    __API_UNAVAILABLE(macosx)
+ *    __API_UNAVAILABLE(watchos, tvos)
+ */
+#define __API_UNAVAILABLE(...) __API_UNAVAILABLE_GET_MACRO(__VA_ARGS__,__API_UNAVAILABLE3,__API_UNAVAILABLE2,__API_UNAVAILABLE1)(__VA_ARGS__)
+
 #endif /* __AVAILABILITY__ */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityInternal.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityInternal.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityInternal.h	2016-05-11 14:53:08.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityInternal.h	2016-06-26 05:16:29.000000000 +0200
@@ -1,5 +1,5 @@
 /*
- * Copyright (c) 2007-2015 by Apple Inc.. All rights reserved.
+ * Copyright (c) 2007-2016 by Apple Inc.. All rights reserved.
  *
  * @APPLE_LICENSE_HEADER_START@
  * 
@@ -17323,4 +17323,90 @@
     #endif
 #endif
 
+/*
+ Macros for defining which versions/platform a given symbol can be used.
+ 
+ @see http://clang.llvm.org/docs/AttributeReference.html#availability
+ */
+
+/*
+ * API Introductions
+ *
+ * Use to specify the release that a particular API became available.
+ *
+ * Platform names:
+ *   macosx, ios, tvos, watchos
+ *
+ * Examples:
+ *    __API_AVAILABLE(macosx(10.10))
+ *    __API_AVAILABLE(macosx(10.9), ios(10.0))
+ *    __API_AVAILABLE(macosx(10.4), ios(8.0), watchos(2.0), tvos(10.0))
+ */
+#define __API_AVAILABLE_PLATFORM_macosx(x) macosx,introduced=x
+#define __API_AVAILABLE_PLATFORM_ios(x) ios,introduced=x
+#define __API_AVAILABLE_PLATFORM_watchos(x) watchos,introduced=x
+#define __API_AVAILABLE_PLATFORM_tvos(x) tvos,introduced=x
+
+#define __API_A(x) __attribute__((availability(__API_AVAILABLE_PLATFORM_##x)))
+#define __API_AVAILABLE1(x) __API_A(x)
+#define __API_AVAILABLE2(x,y) __API_A(x) __API_A(y)
+#define __API_AVAILABLE3(x,y,z)  __API_A(x) __API_A(y) __API_A(z)
+#define __API_AVAILABLE4(x,y,z,t) __API_A(x) __API_A(y) __API_A(z) __API_A(t)
+#define __API_AVAILABLE_GET_MACRO(_1,_2,_3,_4,NAME,...) NAME
+
+/*
+ * API Deprecations
+ *
+ * Use to specify the release that a particular API became unavailable.
+ *
+ * Platform names:
+ *   macosx, ios, tvos, watchos
+ *
+ * Examples:
+ *
+ *    __API_DEPRECATED("No longer supported", macosx(10.4, 10.8))
+ *    __API_DEPRECATED("No longer supported", macosx(10.4, 10.8), ios(2.0, 3.0), watchos(2.0, 3.0), tvos(9.0, 10.0))
+ *
+ *    __API_DEPRECATED_WITH_REPLACEMENT("-setName:", tvos(10.0, 10.4), ios(9.0, 10.0))
+ *    __API_DEPRECATED_WITH_REPLACEMENT("SomeClassName", macosx(10.4, 10.6), watchos(2.0, 3.0))
+ */
+#define __API_DEPRECATED_PLATFORM_macosx(x,y) macosx,introduced=x,deprecated=y
+#define __API_DEPRECATED_PLATFORM_ios(x,y) ios,introduced=x,deprecated=y
+#define __API_DEPRECATED_PLATFORM_watchos(x,y) watchos,introduced=x,deprecated=y
+#define __API_DEPRECATED_PLATFORM_tvos(x,y) tvos,introduced=x,deprecated=y
+
+#define __API_D(msg,x) __attribute__((availability(__API_DEPRECATED_PLATFORM_##x,message=msg)))
+#define __API_DEPRECATED_MSG2(msg,x) __API_D(msg,x)
+#define __API_DEPRECATED_MSG3(msg,x,y) __API_D(msg,x) __API_D(msg,y)
+#define __API_DEPRECATED_MSG4(msg,x,y,z) __API_DEPRECATED_MSG3(msg,x,y) __API_D(msg,z)
+#define __API_DEPRECATED_MSG5(msg,x,y,z,t) __API_DEPRECATED_MSG4(msg,x,y,z) __API_D(msg,t)
+#define __API_DEPRECATED_MSG_GET_MACRO(_1,_2,_3,_4,_5,NAME,...) NAME
+
+#define __API_R(rep,x) __attribute__((availability(__API_DEPRECATED_PLATFORM_##x,replacement=rep)))
+#define __API_DEPRECATED_REP2(rep,x) __API_R(rep,x)
+#define __API_DEPRECATED_REP3(rep,x,y) __API_R(rep,x) __API_R(rep,y)
+#define __API_DEPRECATED_REP4(rep,x,y,z)  __API_DEPRECATED_REP3(rep,x,y) __API_R(rep,z)
+#define __API_DEPRECATED_REP5(rep,x,y,z,t) __API_DEPRECATED_REP4(rep,x,y,z) __API_R(rep,t)
+#define __API_DEPRECATED_REP_GET_MACRO(_1,_2,_3,_4,_5,NAME,...) NAME
+
+/*
+ * API Unavailability
+ * Use to specify that an API is unavailable for a particular platform.
+ *
+ * Example:
+ *    __API_UNAVAILABLE(macosx)
+ *    __API_UNAVAILABLE(watchos, tvos)
+ */
+#define __API_UNAVAILABLE_PLATFORM_macosx macosx,unavailable
+#define __API_UNAVAILABLE_PLATFORM_ios ios,unavailable
+#define __API_UNAVAILABLE_PLATFORM_watchos watchos,unavailable
+#define __API_UNAVAILABLE_PLATFORM_tvos tvos,unavailable
+
+#define __API_U(x) __attribute__((availability(__API_UNAVAILABLE_PLATFORM_##x)))
+#define __API_UNAVAILABLE1(x) __API_U(x)
+#define __API_UNAVAILABLE2(x,y) __API_U(x) __API_U(y)
+#define __API_UNAVAILABLE3(x,y,z) __API_UNAVAILABLE2(x,y) __API_U(z)
+#define __API_UNAVAILABLE_GET_MACRO(_1,_2,_3,NAME,...) NAME
+
+
 #endif /* __AVAILABILITY_INTERNAL__ */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOKitKeys.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOKitKeys.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOKitKeys.h	2016-06-03 22:55:03.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOKitKeys.h	2016-06-29 00:56:02.000000000 +0200
@@ -133,6 +133,7 @@
 #define kIOMaximumSegmentByteCountWriteKey      "IOMaximumSegmentByteCountWrite"      // (OSNumber)
 #define kIOMinimumSegmentAlignmentByteCountKey  "IOMinimumSegmentAlignmentByteCount"  // (OSNumber)
 #define kIOMaximumSegmentAddressableBitCountKey "IOMaximumSegmentAddressableBitCount" // (OSNumber)
+#define kIOMinimumSaturationByteCountKey        "IOMinimumSaturationByteCount"        // (OSNumber)
 
 // properties found in services that wish to describe an icon
 //
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOMemoryDescriptor.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOMemoryDescriptor.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOMemoryDescriptor.h	2016-06-03 22:55:11.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOMemoryDescriptor.h	2016-06-29 00:56:08.000000000 +0200
@@ -69,6 +69,10 @@
 #define IODIRECTIONCOMPLETEWITHDATAVALIDDEFINED	1
      kIODirectionCompleteWithDataValid = 0x00000080,
 };
+
+
+
+
 #ifdef __LP64__
 typedef IOOptionBits IODirection;
 #endif /* __LP64__ */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IORegistryEntry.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IORegistryEntry.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IORegistryEntry.h	2016-06-03 22:55:11.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IORegistryEntry.h	2016-06-29 00:56:09.000000000 +0200
@@ -53,8 +53,9 @@
                                                void * context);
 
 enum {
-    kIORegistryIterateRecursively	= 0x00000001,
-    kIORegistryIterateParents		= 0x00000002
+    kIORegistryIterateRecursively   = 0x00000001,
+    kIORegistryIterateParents       = 0x00000002,
+    kIORegistryIterateFromUser      = 0x00000004
 };
 
 /*! @class IORegistryEntry : public OSObject
@@ -179,7 +180,13 @@
 
 private:
 #if __LP64__
+#if !CONFIG_EMBEDDED
+    virtual OSArray * getChildSetReferenceWithOptions( const IORegistryPlane * plane, IOOptionBits options = 0 ) const;
+    OSMetaClassDeclareReservedUsed(IORegistryEntry, 0);
+#else
     OSMetaClassDeclareReservedUnused(IORegistryEntry, 0);
+#endif
+
     OSMetaClassDeclareReservedUnused(IORegistryEntry, 1);
     OSMetaClassDeclareReservedUnused(IORegistryEntry, 2);
     OSMetaClassDeclareReservedUnused(IORegistryEntry, 3);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOUserClient.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOUserClient.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOUserClient.h	2016-06-03 22:55:13.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOUserClient.h	2016-06-29 00:56:11.000000000 +0200
@@ -173,7 +173,6 @@
     @abstract   Provides a basis for communication between client applications and I/O Kit objects.
 */
 
-
 class IOUserClient : public IOService
 {
     OSDeclareAbstractStructors(IOUserClient)
@@ -201,17 +200,7 @@
     bool reserve();
 
 private:
-    OSSet * mappings;
-    UInt8   sharedInstance;
-    UInt8   closed;
-    UInt8   __ipcFinal;
-    UInt8   __reservedA[1];
-    volatile SInt32 __ipc;
-#if __LP64__
-    void  * __reserved[7];
-#else
-    void  * __reserved[6];
-#endif
+    void  * __reserved[9];
 
 public:
    virtual IOReturn externalMethod( uint32_t selector, IOExternalMethodArguments * arguments,
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/bluetooth/Bluetooth.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/bluetooth/Bluetooth.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/bluetooth/Bluetooth.h	2016-06-07 01:24:20.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/bluetooth/Bluetooth.h	2016-06-29 00:57:40.000000000 +0200
@@ -1159,6 +1159,10 @@
 	uint8_t	data[8];
 };
 
+typedef struct BluetoothHCISupportedFeatures        BluetoothHCILESupportedFeatures;
+
+typedef struct BluetoothHCISupportedFeatures        BluetoothHCILEUsedFeatures;
+
 typedef uint8_t										BluetoothHCIPageNumber;
 typedef struct	BluetoothHCIExtendedFeaturesInfo	BluetoothHCIExtendedFeaturesInfo;
 struct BluetoothHCIExtendedFeaturesInfo
@@ -2337,6 +2341,13 @@
     uint16_t									supervisionTimeout;
 } __attribute__((packed));
         
+typedef struct  BluetoothHCIEventLEReadRemoteUsedFeaturesCompleteResults     BluetoothHCIEventLEReadRemoteUsedFeaturesCompleteResults;
+struct          BluetoothHCIEventLEReadRemoteUsedFeaturesCompleteResults
+{
+    BluetoothConnectionHandle					connectionHandle;
+    BluetoothHCISupportedFeatures				usedFeatures;
+} __attribute__((packed));
+
 typedef struct	BluetoothHCIEventDisconnectionCompleteResults		BluetoothHCIEventDisconnectionCompleteResults;
 struct			BluetoothHCIEventDisconnectionCompleteResults
 {
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IOGraphicsTypes.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IOGraphicsTypes.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IOGraphicsTypes.h	2016-06-03 23:08:18.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/graphics/IOGraphicsTypes.h	2016-06-29 01:09:10.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDKeys.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDKeys.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDKeys.h	2016-06-03 23:10:18.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDKeys.h	2016-06-29 01:11:16.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDEventService.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDEventService.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDEventService.h	2016-06-03 23:10:18.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDEventService.h	2016-06-29 01:11:16.000000000 +0200
@@ -338,7 +338,15 @@
                                 SInt32                      dy,
                                 UInt32                      buttonState,
                                 IOOptionBits                options = 0 );
-    
+
+    void                    dispatchRelativePointerEventWithFixed(
+                                AbsoluteTime                timeStamp,
+                                IOFixed                     dx,
+                                IOFixed                     dy,
+                                UInt32                      buttonState,
+                                IOOptionBits                options = 0 );
+
+  
     virtual void            dispatchAbsolutePointerEvent(
                                 AbsoluteTime                timeStamp,
                                 SInt32                      x,
@@ -358,6 +366,13 @@
                                 SInt32                      deltaAxis3,
                                 IOOptionBits                options = 0 );
 
+    void                    dispatchScrollWheelEventWithFixed(
+                                AbsoluteTime                timeStamp,
+                                IOFixed                     deltaAxis1,
+                                IOFixed                     deltaAxis2,
+                                IOFixed                     deltaAxis3,
+                                IOOptionBits                options = 0 );
+
     virtual void            dispatchTabletPointerEvent(
                                 AbsoluteTime                timeStamp,
                                 UInt32                      transducerID,
@@ -400,7 +415,14 @@
     virtual IOReturn        setSystemProperties( OSDictionary * properties );
     
     virtual IOReturn        setProperties( OSObject * properties );
-    
+  
+    virtual IOReturn        newUserClient(
+                              task_t owningTask,
+                              void * securityID,
+                              UInt32 type,
+                              OSDictionary * properties,
+                              IOUserClient ** handler );
+ 
 protected:
     OSMetaClassDeclareReservedUsed(IOHIDEventService,  0);
     virtual OSArray *       getDeviceUsagePairs();
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDSystem.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDSystem.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDSystem.h	2016-06-03 23:10:18.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDSystem.h	2016-06-29 01:11:16.000000000 +0200
@@ -147,6 +147,12 @@
 
     uint64_t lastEventTime;
     uint64_t lastUndimEvent;
+    
+    uint64_t lastSetCursorTime;
+    uint64_t lastShowCursorTime;
+    uint64_t lastHideCursorTime;
+    uint64_t lastChangeCursorTime;
+    uint64_t lastMoveCursorTime;
 
     IOService       *displayManager;	// points to display manager
     IOPMPowerFlags	displayState;
@@ -254,6 +260,7 @@
   void _setCursorPosition(bool external = false, bool proximityChange = false, OSObject * sender=0);
 
   static bool _idleTimeSerializerCallback(void * target, void * ref, OSSerialize *s);
+  static bool _cursorStateSerializerCallback(void * target, void * ref, OSSerialize *s);
   static bool _displaySerializerCallback(void * target, void * ref, OSSerialize *s);
 
   void createParameters( void );
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/scsi/IOBDServices.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/scsi/IOBDServices.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/scsi/IOBDServices.h	2016-06-03 23:14:33.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/scsi/IOBDServices.h	2016-06-29 01:17:11.000000000 +0200
@@ -158,6 +158,13 @@
 												  const DVDKeyClass keyClass,
 												  const UInt32 lba,
 												  const UInt8 agid,
+												  const DVDKeyFormat keyFormat ) APPLE_KEXT_OVERRIDE __attribute__ ((deprecated));
+
+	virtual IOReturn		reportKey			( IOMemoryDescriptor * buffer,
+												  const DVDKeyClass keyClass,
+												  const UInt32 lba,
+												  const UInt8 blockCount,
+												  const UInt8 agid,
 												  const DVDKeyFormat keyFormat ) APPLE_KEXT_OVERRIDE;
 												  
 	virtual IOReturn		sendKey				( IOMemoryDescriptor * buffer,
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/scsi/IODVDServices.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/scsi/IODVDServices.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/scsi/IODVDServices.h	2016-06-03 23:14:33.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/scsi/IODVDServices.h	2016-06-29 01:17:11.000000000 +0200
@@ -179,6 +179,13 @@
 												  const DVDKeyClass keyClass,
 												  const UInt32 lba,
 												  const UInt8 agid,
+												  const DVDKeyFormat keyFormat ) APPLE_KEXT_OVERRIDE __attribute__ ((deprecated));
+
+	virtual IOReturn		reportKey			( IOMemoryDescriptor * buffer,
+												  const DVDKeyClass keyClass,
+												  const UInt32 lba,
+												  const UInt8 blockCount,
+												  const UInt8 agid,
 												  const DVDKeyFormat keyFormat ) APPLE_KEXT_OVERRIDE;
 												  
 	virtual IOReturn		sendKey				( IOMemoryDescriptor * buffer,
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/scsi/IOSCSIMultimediaCommandsDevice.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/scsi/IOSCSIMultimediaCommandsDevice.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/scsi/IOSCSIMultimediaCommandsDevice.h	2016-05-04 00:21:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/scsi/IOSCSIMultimediaCommandsDevice.h	2016-06-29 01:17:11.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/serial/IOSerialStreamSync.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/serial/IOSerialStreamSync.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/serial/IOSerialStreamSync.h	2016-06-03 23:05:48.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/serial/IOSerialStreamSync.h	2016-06-29 01:06:46.000000000 +0200
@@ -249,7 +249,7 @@
 
     /*	Internal for IOSerialDriver only */
     virtual bool init(OSDictionary *dictionary = 0, void *refCon = 0);
-    virtual bool attach(IOService *provider);
+    virtual bool attach(IOService *provider) APPLE_KEXT_OVERRIDE;
     void *getRefCon() const { return fRefCon; }
 
 OSMetaClassDeclareReservedUnused(IOSerialStreamSync,  0);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IOBDMedia.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IOBDMedia.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IOBDMedia.h	2016-06-03 23:12:07.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IOBDMedia.h	2016-06-29 01:14:19.000000000 +0200
@@ -116,30 +116,22 @@
 
     virtual bool matchPropertyTable(OSDictionary * table, SInt32 * score);
 
-    /*!
-     * @function reportKey
-     * @discussion
+    /*
      * Issue an MMC REPORT KEY command.
-     * @param buffer
-     * Buffer for the data transfer.  The size of the buffer implies the size of
-     * the data transfer.
-     * @param keyClass
-     * As documented by MMC.
-     * @param address
-     * As documented by MMC.
-     * @param grantID
-     * As documented by MMC.
-     * @param format
-     * As documented by MMC.
-     * @result
-     * Returns the status of the data transfer.
+     * Obsoleted, replaced by this interface.
+     *     virtual IOReturn reportKey( IOMemoryDescriptor * buffer,
+     *                                 UInt8                keyClass,
+     *                                 UInt32               address,
+     *                                 UInt8                blockCount,
+     *                                 UInt8                grantID,
+     *                                 UInt8                format );
      */
 
     virtual IOReturn reportKey( IOMemoryDescriptor * buffer,
                                 UInt8                keyClass,
                                 UInt32               address,
                                 UInt8                grantID,
-                                UInt8                format );
+                                UInt8                format ) __attribute__ ((deprecated));
 
     /*!
      * @function sendKey
@@ -274,7 +266,35 @@
 
     virtual IOReturn splitTrack(UInt32 address);
 
-    OSMetaClassDeclareReservedUnused(IOBDMedia,  0);
+    /*!
+     * @function reportKey
+     * @discussion
+     * Issue an MMC REPORT KEY command.
+     * @param buffer
+     * Buffer for the data transfer.  The size of the buffer implies the size of
+     * the data transfer.
+     * @param keyClass
+     * As documented by MMC.
+     * @param address
+     * As documented by MMC.
+     * @param blockCount
+     * As documented by MMC.
+     * @param grantID
+     * As documented by MMC.
+     * @param format
+     * As documented by MMC.
+     * @result
+     * Returns the status of the data transfer.
+     */
+
+    virtual IOReturn reportKey( IOMemoryDescriptor * buffer,
+                                UInt8                keyClass,
+                                UInt32               address,
+                                UInt8                blockCount,
+                                UInt8                grantID,
+                                UInt8                format );
+
+    OSMetaClassDeclareReservedUsed(IOBDMedia,  0);		/* reportKey */
     OSMetaClassDeclareReservedUnused(IOBDMedia,  1);
     OSMetaClassDeclareReservedUnused(IOBDMedia,  2);
     OSMetaClassDeclareReservedUnused(IOBDMedia,  3);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IOBDMediaBSDClient.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IOBDMediaBSDClient.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IOBDMediaBSDClient.h	2016-06-03 23:12:07.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IOBDMediaBSDClient.h	2016-06-29 01:14:19.000000000 +0200
@@ -68,8 +68,9 @@
 {
     uint8_t  format;
     uint8_t  keyClass;
+    uint8_t  blockCount;
 
-    uint8_t  reserved0016[2];                      /* reserved, clear to zero */
+    uint8_t  reserved0024[1];                         /* reserved, clear to zero */
 
     uint32_t address;
     uint8_t  grantID;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IODVDBlockStorageDevice.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IODVDBlockStorageDevice.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IODVDBlockStorageDevice.h	2016-06-03 23:09:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IODVDBlockStorageDevice.h	2016-06-29 01:12:11.000000000 +0200
@@ -89,7 +89,7 @@
     /* New APIs for DVD */
 
     virtual IOReturn	reportKey(IOMemoryDescriptor *buffer,const DVDKeyClass keyClass,
-                                        const UInt32 lba,const UInt8 agid,const DVDKeyFormat keyFormat)	= 0;
+                                        const UInt32 lba,const UInt8 agid,const DVDKeyFormat keyFormat)	__attribute__ ((deprecated));
 
     virtual IOReturn	sendKey(IOMemoryDescriptor *buffer,const DVDKeyClass keyClass,
                                         const UInt8 agid,const DVDKeyFormat keyFormat)	= 0;
@@ -97,7 +97,11 @@
     virtual IOReturn	readDVDStructure(IOMemoryDescriptor *buffer,const DVDStructureFormat format,
                                         const UInt32 address,const UInt8 layer,const UInt8 agid)	= 0;
 
-    OSMetaClassDeclareReservedUnused(IODVDBlockStorageDevice,  0);
+    virtual IOReturn	reportKey(IOMemoryDescriptor *buffer,const DVDKeyClass keyClass,
+                                        const UInt32 lba,const UInt8 blockCount,
+                                        const UInt8 agid,const DVDKeyFormat keyFormat); /* 10.12.0 */
+
+    OSMetaClassDeclareReservedUsed(IODVDBlockStorageDevice,  0);        /* reportKey */
     OSMetaClassDeclareReservedUnused(IODVDBlockStorageDevice,  1);
     OSMetaClassDeclareReservedUnused(IODVDBlockStorageDevice,  2);
     OSMetaClassDeclareReservedUnused(IODVDBlockStorageDevice,  3);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IODVDBlockStorageDriver.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IODVDBlockStorageDriver.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IODVDBlockStorageDriver.h	2016-06-03 23:09:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IODVDBlockStorageDriver.h	2016-06-29 01:12:11.000000000 +0200
@@ -137,7 +137,7 @@
      * As documented by MtFuji. See DVDKeyFormat.
      */
     virtual IOReturn	reportKey(IOMemoryDescriptor *buffer,const DVDKeyClass keyClass,
-                                        const UInt32 lba,const UInt8 agid,const DVDKeyFormat keyFormat);
+                                        const UInt32 lba,const UInt8 agid,const DVDKeyFormat keyFormat) __attribute__ ((deprecated));
 
     /*
      * @function sendKey
@@ -179,7 +179,31 @@
     virtual IOReturn	readStructure(IOMemoryDescriptor *buffer,const DVDStructureFormat format,
                                         const UInt32 address,const UInt8 layer,const UInt8 agid);
 
-    OSMetaClassDeclareReservedUnused(IODVDBlockStorageDriver,  0);
+    /*
+     * @function reportKey
+     * @abstract
+     * Get key info from the DVD drive.
+     * @discussion
+     * This function handles the getting of key- and encryption-related data for the drive.
+     * @param buffer
+     * A buffer containing information, as documented in the specification
+     * "MtFuji Commands For Multimedia Devices."
+     * @param keyClass
+     * As documented by MtFuji. See DVDKeyClass.
+     * @param lba
+     * As documented by MtFuji.
+     * @param blockCount
+	 * As documented by MMC
+     * @param agid
+     * As documented by MtFuji.
+     * @param keyFormat
+     * As documented by MtFuji. See DVDKeyFormat.
+     */
+    virtual IOReturn	reportKey(IOMemoryDescriptor *buffer,const DVDKeyClass keyClass,
+										const UInt32 lba,const UInt8 blockCount,
+										const UInt8 agid,const DVDKeyFormat keyFormat);
+
+    OSMetaClassDeclareReservedUsed(IODVDBlockStorageDriver,  0);		/* reportKey */
     OSMetaClassDeclareReservedUnused(IODVDBlockStorageDriver,  1);
     OSMetaClassDeclareReservedUnused(IODVDBlockStorageDriver,  2);
     OSMetaClassDeclareReservedUnused(IODVDBlockStorageDriver,  3);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IODVDMedia.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IODVDMedia.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IODVDMedia.h	2016-06-03 23:09:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IODVDMedia.h	2016-06-29 01:12:11.000000000 +0200
@@ -166,31 +166,22 @@
 
     virtual bool matchPropertyTable(OSDictionary * table, SInt32 * score);
 
-    /*!
-     * @function reportKey
-     * @discussion
+    /*
      * Issue an MMC REPORT KEY command.
-     * @param buffer
-     * Buffer for the data transfer.  The size of the buffer implies the size of
-     * the data transfer.  Pass null for the kDVDKeyFormatAGID_Invalidate format
-     * case.
-     * @param keyClass
-     * As documented by MMC.
-     * @param address
-     * As documented by MMC.
-     * @param grantID
-     * As documented by MMC.
-     * @param format
-     * As documented by MMC.
-     * @result
-     * Returns the status of the data transfer.
+     * Obsoleted, replaced by this interface:
+     *    virtual IOReturn reportKey( IOMemoryDescriptor * buffer,
+     *                                UInt8                keyClass,
+     *                                UInt32               address,
+     *                                UInt8                blockCount,
+     *                                UInt8                grantID,
+     *                                UInt8                format );
      */
 
     virtual IOReturn reportKey( IOMemoryDescriptor * buffer,
                                 const DVDKeyClass    keyClass,
                                 const UInt32         address,
                                 const UInt8          grantID,
-                                const DVDKeyFormat   format );
+                                const DVDKeyFormat   format ) __attribute__ ((deprecated));
 
     /*!
      * @function sendKey
@@ -308,7 +299,35 @@
                                     DVDRZoneInfoAddressType addressType,
                                     UInt16 *                actualByteCount );
 
-    OSMetaClassDeclareReservedUnused(IODVDMedia,  0);
+    /*!
+     * @function reportKey
+     * @discussion
+     * Issue an MMC REPORT KEY command.
+     * @param buffer
+     * Buffer for the data transfer.  The size of the buffer implies the size of
+     * the data transfer.
+     * @param keyClass
+     * As documented by MMC.
+     * @param address
+     * As documented by MMC.
+     * @param blockCount
+     * As documented by MMC.
+     * @param grantID
+     * As documented by MMC.
+     * @param format
+     * As documented by MMC.
+     * @result
+     * Returns the status of the data transfer.
+     */
+
+    virtual IOReturn reportKey( IOMemoryDescriptor * buffer,
+                                UInt8                keyClass,
+                                UInt32               address,
+                                UInt8                blockCount,
+                                UInt8                grantID,
+                                UInt8                format );
+
+    OSMetaClassDeclareReservedUsed(IODVDMedia,  0);         /* reportKey */
     OSMetaClassDeclareReservedUnused(IODVDMedia,  1);
     OSMetaClassDeclareReservedUnused(IODVDMedia,  2);
     OSMetaClassDeclareReservedUnused(IODVDMedia,  3);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IODVDMediaBSDClient.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IODVDMediaBSDClient.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IODVDMediaBSDClient.h	2016-06-03 23:09:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/storage/IODVDMediaBSDClient.h	2016-06-29 01:12:11.000000000 +0200
@@ -69,8 +69,9 @@
 {
     uint8_t  format;
     uint8_t  keyClass;
+    uint8_t  blockCount;
 
-    uint8_t  reserved0016[2];                      /* reserved, clear to zero */
+    uint8_t  reserved0024[1];                      /* reserved, clear to zero */
 
     uint32_t address;
     uint8_t  grantID;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostDevice.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostDevice.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostDevice.h	2016-06-07 01:20:47.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostDevice.h	2016-06-29 01:13:25.000000000 +0200
@@ -54,6 +54,8 @@
 class AppleUSBHostPort;
 class AppleUSBHostDescriptorCache;
 class AppleUSBHostResources;
+class IOSimpleReporter;
+class IOStateReporter;
 
 /*!
     @class IOUSBHostDevice
@@ -151,7 +153,7 @@
     
     virtual IOReturn message(UInt32 type, IOService* provider,  void* argument = 0);
 
-    virtual const char* stringFromReturn(IOReturn rtn);
+    virtual const char* stringFromReturn(IOReturn code);
 
     virtual bool setProperty(const OSSymbol* aKey, OSObject*   anObject);
     virtual bool setProperty(const OSString* aKey, OSObject*   anObject);
@@ -162,6 +164,9 @@
     virtual bool setProperty(const char* aKey, unsigned long long aValue, unsigned int aNumberOfBits);
     virtual bool setProperty(const char* aKey, void*      	      bytes,  unsigned int length);
 
+    virtual IOReturn configureReport(IOReportChannelList* channels, IOReportConfigureAction action, void* result, void* destination);
+    virtual IOReturn updateReport(IOReportChannelList*channels, IOReportUpdateAction action, void* result, void* destination);
+
 protected:
     virtual IOReturn terminateGated(IOOptionBits options = 0);
     
@@ -972,6 +977,9 @@
 
     struct tExpansionData
     {
+        OSSet*              _reports;
+        IOStateReporter*    _powerStateReport;
+        IOSimpleReporter*   _idlePolicyReport;
     };
 
     tExpansionData* _expansionData;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostFamily.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostFamily.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostFamily.h	2016-06-07 01:20:47.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostFamily.h	2016-06-29 01:13:25.000000000 +0200
@@ -326,6 +326,7 @@
 #define kUSBHostBillboardDevicePropertyAlternateModeStringIndex "iAlternateModeString"
 #define kUSBHostBillboardDevicePropertyAlternateModeString      "AlternateModeString"
 #define kUSBHostBillboardDevicePropertyAddtionalInfoURLIndex    "iAddtionalInfoURL"
+#define kUSBHostBillboardDevicePropertyAddtionalInfoURL         "AddtionalInfoURL"
 
 #if TARGET_OS_EMBEDDED
 #define kUSBHostInterfacePropertyStringIndex                    "iInterface"
@@ -372,13 +373,14 @@
 
 #pragma mark APCI enumerations
 
-// UPC definitions from ACPI Rev 4.0
+// ACPI 5.0a Table 9-227: UPC Return Package Values
 typedef enum
 {
     kUSBHostPortNotConnectable = 0,                 // Port is not connectable
     kUSBHostPortConnectable    = 1                  // Port is connectable either user visible or invisible
 } tUSBHostPortConnectable;
 
+// ACPI 5.0a Table 9-227: UPC Return Package Values
 typedef enum
 {
     kUSBHostConnectorTypeA              = 0x00,
@@ -389,6 +391,7 @@
     kUSBHostConnectorTypeUSB3MicroB     = 0x05,
     kUSBHostConnectorTypeUSB3MicroAB    = 0x06,
     kUSBHostConnectorTypeUSB3PowerB     = 0x07,
+    kUSBHostConnectorTypeUSBTypeC       = 0x09,
     kUSBHostConnectorTypeUnknown        = 0xFE,
     kUSBHostConnectorTypeProprietary    = 0xFF
 } tUSBHostConnectorType;
@@ -420,7 +423,15 @@
 #define kRDYForGPIOTest                                 "RDYG"
 #define kReconfiguredCount                              "RCFG"
 #define kUSBPlatformProperties                          "USBX"
+#define kUSBTypeCCableDetectACPIMethod                  "MODU"
 
+// connection types returned by MODU method
+typedef enum
+{
+    kUSBTypeCCableTypeNone              = 0,
+    kUSBTypeCCableTypeUSB               = 1,
+    kUSBTypeCCableTypeError             = 0xFF
+} tUSBCTypeCableType;
 
 #endif
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostInterface.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostInterface.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostInterface.h	2016-06-07 01:20:47.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostInterface.h	2016-06-29 01:13:25.000000000 +0200
@@ -36,6 +36,8 @@
 #include <IOKit/usb/IOUSBHostFamily.h>
 #include <IOKit/usb/IOUSBHostDevice.h>
 
+class IOSimpleReporter;
+
 /*!
  * @class IOUSBHostInterface
  *
@@ -87,7 +89,10 @@
     
     virtual IOReturn    message(UInt32 type, IOService* provider,  void* argument = 0);
 
-    virtual const char* stringFromReturn(IOReturn rtn);
+    virtual IOReturn configureReport(IOReportChannelList* channels, IOReportConfigureAction action, void* result, void* destination);
+    virtual IOReturn updateReport(IOReportChannelList*channels, IOReportUpdateAction action, void* result, void* destination);
+
+    virtual const char* stringFromReturn(IOReturn code);
     
 protected:
     virtual IOReturn openGated(IOService* forClient, IOOptionBits options, void* arg);
@@ -502,6 +507,9 @@
 protected:
     struct tExpansionData
     {
+        IOLock*             _reportLock;
+        OSSet*              _reports;
+        IOSimpleReporter*   _idlePolicyReport;
     };
     tExpansionData* _expansionData;
     
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/StandardUSB.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/StandardUSB.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/StandardUSB.h	2016-06-07 01:20:47.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/StandardUSB.h	2016-06-29 01:13:25.000000000 +0200
@@ -483,9 +483,9 @@
     // USB Billboard 3.1.6.2: Billboard Capability Descriptor
     struct BillboardAlternateModeCapability
     {
-        uint16_t wSVID;
-        uint8_t  bAlternateMode;
-        uint8_t  iAlternateModeString;
+        uint16_t  wSVID;
+        uint32_t  bAlternateMode;
+        uint8_t   iAlternateModeString;
     };
 
 #ifdef __cplusplus
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/USB.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/USB.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/USB.h	2016-06-07 01:22:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/USB.h	2016-06-29 01:16:54.000000000 +0200
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
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/i386/cpuid.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/i386/cpuid.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/i386/cpuid.h	2016-06-03 22:54:56.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/i386/cpuid.h	2016-06-29 00:55:52.000000000 +0200
@@ -193,8 +193,6 @@
 #define CPUID_MWAIT_EXTENSION	_Bit(0)	/* enumeration of WMAIT extensions */
 #define CPUID_MWAIT_BREAK	_Bit(1)	/* interrupts are break events	   */
 
-#define CPUID_MODEL_YONAH		0x0E
-#define CPUID_MODEL_MEROM		0x0F
 #define CPUID_MODEL_PENRYN		0x17
 #define CPUID_MODEL_NEHALEM		0x1A
 #define CPUID_MODEL_FIELDS		0x1E	/* Lynnfield, Clarksfield */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/i386/proc_reg.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/i386/proc_reg.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/i386/proc_reg.h	2016-06-03 22:54:56.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/i386/proc_reg.h	2016-06-29 00:55:52.000000000 +0200
@@ -613,4 +613,9 @@
 #define MSR_IA32_KERNEL_GS_BASE			0xC0000102
 #define MSR_IA32_TSC_AUX			0xC0000103
 
+#define HV_VMX_EPTP_MEMORY_TYPE_UC  		0x0
+#define HV_VMX_EPTP_MEMORY_TYPE_WB		0x6
+#define HV_VMX_EPTP_WALK_LENGTH(wl)    		(0ULL | ((((wl) - 1) & 0x7) << 3))
+#define HV_VMX_EPTP_ENABLE_AD_FLAGS    		(1ULL << 6)
+
 #endif	/* _I386_PROC_REG_H_ */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/bits.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/bits.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/bits.h	2016-06-03 22:55:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/bits.h	2016-06-29 00:55:59.000000000 +0200
@@ -31,6 +31,8 @@
 #ifndef __BITS_H__
 #define __BITS_H__
 
+typedef unsigned int			uint;
+
 #define BIT(b)				(1ULL << (b))
 
 #define mask(width)			(BIT(width) - 1)
@@ -130,7 +132,8 @@
 }
 
 
-#define BITMAP_SIZE(n)	(size_t)((((uint)(n) + 63) >> 6) << 3)	/* Round to 64bit bitmap_t, then convert to bytes */
+#define BITMAP_LEN(n)	(((uint)(n) + 63) >> 6)		/* Round to 64bit bitmap_t */
+#define BITMAP_SIZE(n)	(size_t)(BITMAP_LEN(n) << 3)		/* Round to 64bit bitmap_t, then convert to bytes */
 #define bitmap_bit(n)	bits(n, 5, 0)
 #define bitmap_index(n)	bits(n, 63, 6)
 
@@ -167,12 +170,24 @@
 inline static void
 bitmap_set(bitmap_t *map, uint n)
 {
-	atomic_bit_set(&map[bitmap_index(n)], bitmap_bit(n));
+	bit_set(map[bitmap_index(n)], bitmap_bit(n));
 }
 
 inline static void
 bitmap_clear(bitmap_t *map, uint n)
 {
+	bit_clear(map[bitmap_index(n)], bitmap_bit(n));
+}
+
+inline static void
+atomic_bitmap_set(bitmap_t *map, uint n)
+{
+	atomic_bit_set(&map[bitmap_index(n)], bitmap_bit(n));
+}
+
+inline static void
+atomic_bitmap_clear(bitmap_t *map, uint n)
+{
 	atomic_bit_clear(&map[bitmap_index(n)], bitmap_bit(n));
 }
 
@@ -270,6 +285,8 @@
 
 #if DEVELOPMENT || DEBUG
 
+#ifdef XNU_TEST_BITMAP
+
 extern void dump_bitmap_next(bitmap_t *map, uint nbits);
 extern void dump_bitmap_lsb(bitmap_t *map, uint nbits);
 extern void test_bitmap(void);
@@ -329,3 +346,5 @@
 #endif
 
 #endif
+
+#endif
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/clock.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/clock.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/clock.h	2016-06-03 22:55:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/clock.h	2016-06-29 00:55:59.000000000 +0200
@@ -117,9 +117,21 @@
 							uint64_t		nanoseconds,
 							uint64_t		*result);
 
+/*
+ * Absolute <-> Continuous Time conversion routines
+ *
+ * It is the caller's responsibility to ensure that these functions are
+ * synchronized with respect to updates to the continuous timebase.  The
+ * returned value is only valid until the next update to the continuous
+ * timebase.
+ *
+ * If the value to be returned by continuoustime_to_absolutetime would be
+ * negative, zero is returned.  This occurs when the provided continuous time
+ * is less the amount of the time the system spent asleep and /must/ be
+ * handled.
+ */
 extern uint64_t			absolutetime_to_continuoustime(
 							uint64_t		abstime);
-
 extern uint64_t			continuoustime_to_absolutetime(
 							uint64_t		conttime);
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/kcdata.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/kcdata.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/kcdata.h	2016-06-03 22:55:03.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/kcdata.h	2016-06-29 00:55:57.000000000 +0200
@@ -438,7 +438,6 @@
 #define STACKSHOT_KCCONTAINER_THREAD 0x904u
 #define STACKSHOT_KCTYPE_TASK_SNAPSHOT 0x905u         /* task_snapshot_v2 */
 #define STACKSHOT_KCTYPE_THREAD_SNAPSHOT 0x906u       /* thread_snapshot_v2, thread_snapshot_v3 */
-#define STASKSHOT_KCTYPE_DONATING_PIDS 0x907u         /* todo: remove once all callers move to the correct spelling below */
 #define STACKSHOT_KCTYPE_DONATING_PIDS 0x907u         /* int[] */
 #define STACKSHOT_KCTYPE_SHAREDCACHE_LOADINFO 0x908u  /* same as KCDATA_TYPE_LIBRARY_LOADINFO64 */
 #define STACKSHOT_KCTYPE_THREAD_NAME 0x909u           /* char[] */
@@ -464,6 +463,7 @@
 #define STACKSHOT_KCTYPE_CPU_TIMES 0x919u             /* struct stackshot_cpu_times */
 #define STACKSHOT_KCTYPE_STACKSHOT_DURATION 0x91au    /* struct stackshot_duration */
 #define STACKSHOT_KCTYPE_STACKSHOT_FAULT_STATS 0x91bu /* struct stackshot_fault_stats */
+#define STACKSHOT_KCTYPE_KERNELCACHE_LOADINFO  0x91cu /* kernelcache UUID -- same as KCDATA_TYPE_LIBRARY_LOADINFO64 */
 
 struct stack_snapshot_frame32 {
 	uint32_t lr;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/kern_cdata.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/kern_cdata.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/kern_cdata.h	2016-06-03 22:55:03.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/kern_cdata.h	2016-06-29 00:55:57.000000000 +0200
@@ -57,4 +57,14 @@
 
 
 
+typedef void * kcdata_descriptor_t;
+
+
+uint32_t kcdata_estimate_required_buffer_size(uint32_t num_items, uint32_t payload_size);
+uint64_t kcdata_memory_get_used_bytes(kcdata_descriptor_t kcd);
+kern_return_t kcdata_memcpy(kcdata_descriptor_t data, mach_vm_address_t dst_addr, void * src_addr, uint32_t size);
+kern_return_t kcdata_get_memory_addr(kcdata_descriptor_t data, uint32_t type, uint32_t size, mach_vm_address_t * user_addr);
+kern_return_t kcdata_get_memory_addr_for_array(
+    kcdata_descriptor_t data, uint32_t type_of_element, uint32_t size_of_element, uint32_t count, mach_vm_address_t * user_addr);
+
 #endif /* _KERN_CDATA_H_ */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/c++/OSKext.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/c++/OSKext.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/c++/OSKext.h	2016-06-03 22:55:00.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/c++/OSKext.h	2016-06-29 00:55:57.000000000 +0200
@@ -211,9 +211,13 @@
         OSData   * booterData);
 
     static OSKext * withPrelinkedInfoDict(
-        OSDictionary * infoDict);
+        OSDictionary * infoDict,
+        bool doCoalesedSlides);
     virtual bool initWithPrelinkedInfoDict(
-        OSDictionary * infoDict);
+        OSDictionary * infoDict,
+        bool doCoalesedSlides);
+
+    static void setAllVMAttributes(void);
 
     static OSKext * withMkext2Info(
         OSDictionary * anInfoDict,
@@ -303,7 +307,7 @@
     static void recordIdentifierRequest(
         OSString * kextIdentifier);
 
-    virtual OSReturn slidePrelinkedExecutable(void);
+    virtual OSReturn slidePrelinkedExecutable(bool doCoalesedSlides);
     virtual OSReturn loadExecutable(void);
     virtual void     jettisonLinkeditSegment(void);
     virtual void     jettisonDATASegmentPadding(void);
@@ -354,6 +358,7 @@
     static  OSDictionary * copyLoadedKextInfoByUUID(
         OSArray * kextIdentifiers = NULL,
         OSArray * keys = NULL);
+    static OSData * copyKextUUIDForAddress(OSNumber *address = NULL);
     virtual OSDictionary * copyInfo(OSArray * keys = NULL);
 
    /* Logging to user space.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/c++/OSString.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/c++/OSString.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/c++/OSString.h	2016-06-03 22:55:01.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/libkern/c++/OSString.h	2016-06-29 00:55:58.000000000 +0200
@@ -260,7 +260,6 @@
     */
     virtual bool initWithCStringNoCopy(const char * cString);
 
-    bool initWithStringOfLength(const char *cString, size_t inlength);
 
    /*!
     * @function free
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/dyld_kernel.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/dyld_kernel.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/dyld_kernel.h	2016-06-03 22:55:18.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/dyld_kernel.h	2016-06-29 00:56:16.000000000 +0200
@@ -29,8 +29,10 @@
 #ifndef _MACH_DYLIB_INFO_H_
 #define _MACH_DYLIB_INFO_H_
 
+#include <mach/boolean.h>
 #include <sys/_types.h>
 #include <sys/_types/_fsid_t.h>
+#include <sys/_types/_u_int8_t.h>
 #include <sys/_types/_u_int32_t.h>
 #include <sys/_types/_fsobj_id_t.h>
 #include <sys/_types/_uuid_t.h>
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/mach_time.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/mach_time.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/mach_time.h	2016-06-03 22:55:19.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/mach_time.h	2016-06-29 00:56:17.000000000 +0200
@@ -48,11 +48,17 @@
 __OSX_AVAILABLE_STARTING(__MAC_10_9, __IPHONE_8_0)
 uint64_t			mach_approximate_time(void);
 
-__OSX_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0) 
-__TVOS_AVAILABLE(__TVOS_10_0) 
+/*
+ * like mach_absolute_time, but advances during sleep
+ */
+__OSX_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0)
+__TVOS_AVAILABLE(__TVOS_10_0)
 __WATCHOS_AVAILABLE(__WATCHOS_3_0)
 uint64_t			mach_continuous_time(void);
 
+/*
+ * like mach_approximate_time, but advances during sleep
+ */
 __OSX_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0)
 __TVOS_AVAILABLE(__TVOS_10_0)
 __WATCHOS_AVAILABLE(__WATCHOS_3_0)
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/mach_voucher_types.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/mach_voucher_types.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/mach_voucher_types.h	2016-06-03 22:55:19.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/mach_voucher_types.h	2016-06-29 00:56:17.000000000 +0200
@@ -170,6 +170,9 @@
 typedef mach_msg_type_number_t mach_voucher_attr_raw_recipe_size_t;
 typedef mach_msg_type_number_t mach_voucher_attr_raw_recipe_array_size_t;
 
+#define MACH_VOUCHER_ATTR_MAX_RAW_RECIPE_ARRAY_SIZE   5120
+#define MACH_VOUCHER_TRAP_STACK_LIMIT                 256
+
 #pragma pack()
 
 /*
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/machine/sdt.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/machine/sdt.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/machine/sdt.h	2016-06-03 22:55:01.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/machine/sdt.h	2016-06-29 00:55:59.000000000 +0200
@@ -217,6 +217,16 @@
     type3, arg3, type4, arg4, type5, arg5)						\
 	DTRACE_PROBE5(__sdt_, name, arg1, arg2, arg3, arg4, arg5);
 
+#define	DTRACE_MEMORYSTATUS2(name, type1, arg1, type2, arg2)		\
+	DTRACE_PROBE2(__sdt_, name, arg1, arg2);
+
+#define	DTRACE_MEMORYSTATUS3(name, type1, arg1, type2, arg2, type3, arg3)		\
+	DTRACE_PROBE3(__sdt_, name, arg1, arg2, arg3);
+
+#define	DTRACE_MEMORYSTATUS6(name, type1, arg1, type2, arg2, 			\
+    type3, arg3, type4, arg4, type5, arg5, type6, arg6)	\
+	DTRACE_PROBE6(__vminfo_, name, arg1, arg2, arg3, arg4, arg5, arg6)
+
 #define	DTRACE_TMR3(name, type1, arg1, type2, arg2, type3, arg3)		\
 	DTRACE_PROBE3(__sdt_, name, arg1, arg2, arg3);
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/machine.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/machine.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/machine.h	2016-06-03 22:55:19.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/machine.h	2016-06-29 00:56:17.000000000 +0200
@@ -341,8 +341,6 @@
 #define CPUFAMILY_POWERPC_G4		0x77c184ae
 #define CPUFAMILY_POWERPC_G5		0xed76d8aa
 #define CPUFAMILY_INTEL_6_13		0xaa33392b
-#define CPUFAMILY_INTEL_YONAH		0x73d67300
-#define CPUFAMILY_INTEL_MEROM		0x426f69ef
 #define CPUFAMILY_INTEL_PENRYN		0x78ea4fbc
 #define CPUFAMILY_INTEL_NEHALEM		0x6b5a4cd2
 #define CPUFAMILY_INTEL_WESTMERE	0x573b5eec
@@ -364,13 +362,8 @@
 #define CPUFAMILY_ARM_TWISTER		0x92fb37c8
 
 /* The following synonyms are deprecated: */
-#define CPUFAMILY_INTEL_6_14	CPUFAMILY_INTEL_YONAH
-#define CPUFAMILY_INTEL_6_15	CPUFAMILY_INTEL_MEROM
 #define CPUFAMILY_INTEL_6_23	CPUFAMILY_INTEL_PENRYN
 #define CPUFAMILY_INTEL_6_26	CPUFAMILY_INTEL_NEHALEM
 
-#define CPUFAMILY_INTEL_CORE	CPUFAMILY_INTEL_YONAH
-#define CPUFAMILY_INTEL_CORE2	CPUFAMILY_INTEL_MEROM
-
 
 #endif	/* _MACH_MACHINE_H_ */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/task.defs /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/task.defs
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/task.defs	2016-06-03 22:55:25.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/task.defs	2016-06-29 00:56:23.000000000 +0200
@@ -474,7 +474,9 @@
 
 routine task_register_dyld_shared_cache_image_info(
         task                :task_t;
-        dyld_cache_image    :dyld_kernel_image_info_t);
+        dyld_cache_image    :dyld_kernel_image_info_t;
+        no_cache            :boolean_t;
+        private_cache       :boolean_t);
 
 routine task_register_dyld_set_dyld_state(
         task           :task_t;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/task.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/task.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/task.h	2016-06-03 22:55:26.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/mach/task.h	2016-06-29 00:56:25.000000000 +0200
@@ -707,7 +707,9 @@
 kern_return_t task_register_dyld_shared_cache_image_info
 (
 	task_t task,
-	dyld_kernel_image_info_t dyld_cache_image
+	dyld_kernel_image_info_t dyld_cache_image,
+	boolean_t no_cache,
+	boolean_t private_cache
 );
 
 /* Routine task_register_dyld_set_dyld_state */
@@ -1393,6 +1395,8 @@
 		mach_msg_header_t Head;
 		NDR_record_t NDR;
 		dyld_kernel_image_info_t dyld_cache_image;
+		boolean_t no_cache;
+		boolean_t private_cache;
 	} __Request__task_register_dyld_shared_cache_image_info_t __attribute__((unused));
 #ifdef  __MigPackStructs
 #pragma pack()
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/net/ethernet.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/net/ethernet.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/net/ethernet.h	2016-06-03 22:55:07.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/net/ethernet.h	2016-06-29 00:56:09.000000000 +0200
@@ -105,6 +105,7 @@
 #define ETHERTYPE_IPV6		0x86dd	/* IPv6 */
 #define ETHERTYPE_PAE		0x888e  /* EAPOL PAE/802.1x */
 #define ETHERTYPE_RSN_PREAUTH	0x88c7  /* 802.11i / RSN Pre-Authentication */
+#define ETHERTYPE_PTP		0x88f7  /* IEEE 1588 Precision Time Protocol */
 #define	ETHERTYPE_LOOPBACK	0x9000	/* used to test interfaces */
 /* XXX - add more useful types here */
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/net/if_arp.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/net/if_arp.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/net/if_arp.h	2016-05-04 00:21:26.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/net/if_arp.h	2016-06-29 00:56:09.000000000 +0200
@@ -1,5 +1,5 @@
 /*
- * Copyright (c) 2000-2012 Apple Inc. All rights reserved.
+ * Copyright (c) 2000-2016 Apple Inc. All rights reserved.
  *
  * @APPLE_OSREFERENCE_LICENSE_HEADER_START@
  * 
@@ -143,6 +143,7 @@
 	/* General statistics */
 	uint32_t inuse;		/* # of ARP entries in routing table */
 	uint32_t txurequests;	/* # of ARP requests sent (unicast) */
+	uint32_t held;		/* # of packets held waiting for a reply */
 };
 
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/net/if_utun.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/net/if_utun.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/net/if_utun.h	2016-06-03 22:55:09.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/net/if_utun.h	2016-06-29 00:56:11.000000000 +0200
@@ -43,8 +43,7 @@
 #define UTUN_OPT_IFNAME							2
 #define UTUN_OPT_EXT_IFDATA_STATS				3	/* get|set (type int) */
 #define UTUN_OPT_INC_IFDATA_STATS_IN			4	/* set to increment stat counters (type struct utun_stats_param) */ 
-#define UTUN_OPT_INC_IFDATA_STATS_OUT			5	/* set to increment stat counters (type struct utun_stats_param) */ 
-
+#define UTUN_OPT_INC_IFDATA_STATS_OUT			5	/* set to increment stat counters (type struct utun_stats_param) */
 
 #define UTUN_OPT_SET_DELEGATE_INTERFACE			15      /* set the delegate interface (char[]) */
 #define UTUN_OPT_MAX_PENDING_PACKETS			16      /* the number of packets that can be waiting to be read
@@ -56,7 +55,7 @@
  */
 #define	UTUN_FLAGS_NO_OUTPUT		0x0001
 #define UTUN_FLAGS_NO_INPUT			0x0002
-
+#define UTUN_FLAGS_ENABLE_PROC_UUID	0x0004
 
 /*
  * utun stats parameter structure
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/pexpert/i386/boot.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/pexpert/i386/boot.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/pexpert/i386/boot.h	2016-05-04 00:21:26.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/pexpert/i386/boot.h	2016-06-29 00:55:52.000000000 +0200
@@ -80,7 +80,7 @@
  * Video information.. 
  */
 
-struct Boot_Video {
+struct Boot_VideoV1 {
 	uint32_t	v_baseAddr;	/* Base address of video memory */
 	uint32_t	v_display;	/* Display Code (if Applicable */
 	uint32_t	v_rowBytes;	/* Number of bytes per pixel row */
@@ -88,7 +88,17 @@
 	uint32_t	v_height;	/* Height */
 	uint32_t	v_depth;	/* Pixel Depth */
 };
+typedef struct Boot_VideoV1	Boot_VideoV1;
 
+struct Boot_Video {
+	uint32_t	v_display;	/* Display Code (if Applicable */
+	uint32_t	v_rowBytes;	/* Number of bytes per pixel row */
+	uint32_t	v_width;	/* Width */
+	uint32_t	v_height;	/* Height */
+	uint32_t	v_depth;	/* Pixel Depth */
+	uint32_t	v_resv[7];	/* Reserved */
+	uint64_t	v_baseAddr;	/* Base address of video memory */
+};
 typedef struct Boot_Video	Boot_Video;
 
 /* Values for v_display */
@@ -147,7 +157,7 @@
     uint32_t    MemoryMapDescriptorSize;
     uint32_t    MemoryMapDescriptorVersion;
 
-    Boot_Video	Video;		/* Video Information */
+    Boot_VideoV1 VideoV1;	/* Video Information */
 
     uint32_t    deviceTreeP;	  /* Physical address of flattened device tree */
     uint32_t    deviceTreeLength; /* Length of flattened tree */
@@ -179,7 +189,8 @@
     uint32_t    boot_SMC_plimit;
     uint16_t    bootProgressMeterStart;
     uint16_t    bootProgressMeterEnd;
-    uint32_t    __reserved4[726];
+    Boot_Video	Video;		/* Video Information */
+    uint32_t    __reserved4[712];
 
 } boot_args;
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/pexpert/pexpert.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/pexpert/pexpert.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/pexpert/pexpert.h	2016-06-03 22:55:00.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/pexpert/pexpert.h	2016-06-29 00:55:56.000000000 +0200
@@ -71,6 +71,8 @@
 
 extern uint8_t gPlatformECID[8];
 
+extern uint32_t gPlatformMemoryID;
+
 unsigned int PE_init_taproot(vm_offset_t *taddr);
 
 extern void (*PE_kputc)(char c);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/disk.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/disk.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/disk.h	2016-06-03 22:55:48.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/disk.h	2016-06-29 00:56:49.000000000 +0200
@@ -72,6 +72,7 @@
  * DKIOCGETCOMMANDPOOLSIZE               get device's queue depth
  *
  * DKIOCGETPROVISIONSTATUS               get device's block provision status
+ * DKIOCGETIOMINSATURATIONBYTECOUNT      get minimum byte count to saturate storage bandwidth
  */
 
 #define DK_FEATURE_BARRIER                    0x00000002
@@ -257,6 +258,7 @@
 #define DKIOCSETTIER                          _IOW('d', 85, dk_set_tier_t)
 #define DKIOCGETENCRYPTIONTYPE                _IOR('d', 86, uint32_t)
 #define DKIOCISLOWPOWERMODE                   _IOR('d', 87, uint32_t)
+#define DKIOCGETIOMINSATURATIONBYTECOUNT      _IOR('d', 88, uint32_t)
 
 
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h	2016-06-03 22:55:50.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h	2016-06-29 00:56:50.000000000 +0200
@@ -1,5 +1,5 @@
 /*
- * Copyright (c) 2000-2014 Apple Inc. All rights reserved.
+ * Copyright (c) 2000-2016 Apple Inc. All rights reserved.
  *
  * @APPLE_OSREFERENCE_LICENSE_HEADER_START@
  *
@@ -26,10 +26,8 @@
  * @APPLE_OSREFERENCE_LICENSE_HEADER_END@
  */
 
-/* 	Copyright (c) 1997 Apple Computer, Inc.  All rights reserved.
- *
- * kdebug.h -   kernel_debug definitions
- *
+/*
+ * kdebug.h - kernel_debug definitions
  */
 
 #ifndef BSD_SYS_KDEBUG_H
@@ -65,7 +63,7 @@
  * The eventid is a hierarchical ID, indicating which components an event is
  * referring to.  The debugid includes an eventid and two function qualifier
  * bits, to determine the structural significance of an event (whether it
- * starts or ends a series of grouped events).
+ * starts or ends an interval).
  */
 
 #define KDBG_CLASS_MASK   (0xff000000)
@@ -85,7 +83,6 @@
 #define KDBG_CODE_OFFSET (2)
 #define KDBG_CODE_MAX    (0x3fff)
 
-
 #define KDBG_EVENTID_MASK (0xfffffffc)
 #define KDBG_FUNC_MASK    (0x00000003)
 
@@ -108,44 +105,48 @@
 #define KDBG_EXTRACT_CODE(Debugid) \
         ((uint16_t)(((Debugid) & KDBG_CODE_MASK) >> KDBG_CODE_OFFSET))
 
+/* function qualifiers  */
+#define DBG_FUNC_START 1
+#define DBG_FUNC_END   2
+#define DBG_FUNC_NONE  0
+
+/*
+ * Definitions to support IOP tracing.
+ */
 
-/* The Function qualifiers  */
-#define DBG_FUNC_START		1
-#define DBG_FUNC_END		2
-#define DBG_FUNC_NONE		0
 
 /* The Kernel Debug Classes  */
-#define DBG_MACH		1
-#define DBG_NETWORK		2
-#define DBG_FSYSTEM		3
-#define DBG_BSD			4
-#define DBG_IOKIT		5
-#define DBG_DRIVERS		6
-#define DBG_TRACE           	7
-#define DBG_DLIL	        8
-#define DBG_WORKQUEUE		9
-#define DBG_CORESTORAGE		10
-#define DBG_CG         		11
-#define DBG_MISC		20
-#define DBG_SECURITY		30
-#define DBG_DYLD           	31
-#define DBG_QT              	32
-#define DBG_APPS            	33
-#define DBG_LAUNCHD         	34
-#define DBG_PERF                37
-#define DBG_IMPORTANCE          38
-#define DBG_BANK                40
-#define DBG_XPC                 41
-#define DBG_ATM                 42
-#define DBG_ARIADNE             43
-#define DBG_DAEMON              44
-#define DBG_ENERGYTRACE         45
-#define DBG_DISPATCH            46
-#define DBG_IMG                 49
-#define DBG_UMALLOC		51
+#define DBG_MACH        1
+#define DBG_NETWORK     2
+#define DBG_FSYSTEM     3
+#define DBG_BSD         4
+#define DBG_IOKIT       5
+#define DBG_DRIVERS     6
+#define DBG_TRACE       7
+#define DBG_DLIL        8
+#define DBG_WORKQUEUE   9
+#define DBG_CORESTORAGE 10
+#define DBG_CG          11
+#define DBG_MISC        20
+#define DBG_SECURITY    30
+#define DBG_DYLD        31
+#define DBG_QT          32
+#define DBG_APPS        33
+#define DBG_LAUNCHD     34
+#define DBG_PERF        37
+#define DBG_IMPORTANCE  38
+#define DBG_BANK        40
+#define DBG_XPC         41
+#define DBG_ATM         42
+#define DBG_ARIADNE     43
+#define DBG_DAEMON      44
+#define DBG_ENERGYTRACE 45
+#define DBG_DISPATCH    46
+#define DBG_IMG         49
+#define DBG_UMALLOC     51
 
 
-#define DBG_MIG			255
+#define DBG_MIG         255
 
 
 
@@ -441,7 +442,8 @@
 #define DBG_JOURNAL   5       /* journaling operations */
 #define DBG_IOCTL     6       /* ioctl to the disk */
 #define DBG_BOOTCACHE 7       /* bootcache operations */
-#define DBG_HFS       8       /* HFS-specific events; see bsd/hfs/hfs_kdebug.h */
+#define DBG_HFS       8       /* HFS-specific events; see the hfs project */
+#define DBG_APFS      0xA     /* APFS-specific events; see the apfs project */
 #define DBG_EXFAT     0xE     /* ExFAT-specific events; see the exfat project */
 #define DBG_MSDOS     0xF     /* FAT-specific events; see the msdosfs project */
 #define DBG_ACFS      0x10    /* Xsan-specific events; see the XsanFS project */
@@ -461,12 +463,13 @@
 #define DBG_HFS_UPDATE_SKIPPED	 0x80
 
 /* The Kernel Debug Sub Classes for BSD */
-#define DBG_BSD_PROC		0x01	/* process/signals related */
-#define DBG_BSD_MEMSTAT		0x02	/* memorystatus / jetsam operations */
-#define	DBG_BSD_EXCP_SC		0x0C	/* System Calls */
-#define	DBG_BSD_AIO		0x0D	/* aio (POSIX async IO) */
-#define DBG_BSD_SC_EXTENDED_INFO 0x0E	/* System Calls, extended info */
-#define DBG_BSD_SC_EXTENDED_INFO2 0x0F	/* System Calls, extended info */
+#define DBG_BSD_PROC              0x01 /* process/signals related */
+#define DBG_BSD_MEMSTAT           0x02 /* memorystatus / jetsam operations */
+#define DBG_BSD_EXCP_SC           0x0C /* System Calls */
+#define DBG_BSD_AIO               0x0D /* aio (POSIX async IO) */
+#define DBG_BSD_SC_EXTENDED_INFO  0x0E /* System Calls, extended info */
+#define DBG_BSD_SC_EXTENDED_INFO2 0x0F /* System Calls, extended info */
+#define DBG_BSD_KDEBUG_TEST       0xFF /* for testing kdebug */
 
 
 /* The Codes for BSD subcode class DBG_BSD_PROC */
@@ -524,7 +527,24 @@
 #define	DBG_BUFFER	0x20
 
 /* The Kernel Debug Sub Classes for DBG_DYLD */
-#define DBG_DYLD_STRING   5
+#define DBG_DYLD_UUID (5)
+
+/* Kernel Debug codes for the DBG_DYLD_UUID subclass */
+#define DBG_DYLD_UUID_MAP_A             (0)
+#define DBG_DYLD_UUID_MAP_B             (1)
+#define DBG_DYLD_UUID_MAP_32_A          (2)
+#define DBG_DYLD_UUID_MAP_32_B          (3)
+#define DBG_DYLD_UUID_MAP_32_C          (4)
+#define DBG_DYLD_UUID_UNMAP_A           (5)
+#define DBG_DYLD_UUID_UNMAP_B           (6)
+#define DBG_DYLD_UUID_UNMAP_32_A        (7)
+#define DBG_DYLD_UUID_UNMAP_32_B        (8)
+#define DBG_DYLD_UUID_UNMAP_32_C        (9)
+#define DBG_DYLD_UUID_SHARED_CACHE_A    (10)
+#define DBG_DYLD_UUID_SHARED_CACHE_B    (11)
+#define DBG_DYLD_UUID_SHARED_CACHE_32_A (12)
+#define DBG_DYLD_UUID_SHARED_CACHE_32_B (13)
+#define DBG_DYLD_UUID_SHARED_CACHE_32_C (14)
 
 /* The Kernel Debug modifiers for the DBG_DKRW sub class */
 #define DKIO_DONE 	0x01
@@ -662,44 +682,53 @@
 /* Kernel Debug Macros for specific daemons */
 #define COREDUETDBG_CODE(code) DAEMONDBG_CODE(DBG_DAEMON_COREDUET, code)
 
-/*   Usage:
-* kernel_debug((KDBG_CODE(DBG_NETWORK, DNET_PROTOCOL, 51) | DBG_FUNC_START),
-*	offset, 0, 0, 0,0)
-*
-* For ex,
-*
-* #include <sys/kdebug.h>
-*
-* #define DBG_NETIPINIT NETDBG_CODE(DBG_NETIP,1)
-*
-*
-* void
-* ip_init()
-* {
-*	register struct protosw *pr;
-*	register int i;
-*
-*	KERNEL_DEBUG(DBG_NETIPINIT | DBG_FUNC_START, 0,0,0,0,0)
-* 	--------
-*	KERNEL_DEBUG(DBG_NETIPINIT, 0,0,0,0,0)
-* 	--------
-*	KERNEL_DEBUG(DBG_NETIPINIT | DBG_FUNC_END, 0,0,0,0,0)
-* }
-*
+/*
+ * To use kdebug in the kernel:
+ *
+ * #include <sys/kdebug.h>
+ *
+ * #define DBG_NETIPINIT NETDBG_CODE(DBG_NETIP, 1)
+ *
+ * void
+ * ip_init(void)
+ * {
+ *     KDBG(DBG_NETIPINIT | DBG_FUNC_START, 1, 2, 3, 4);
+ *     ...
+ *     KDBG(DBG_NETIPINIT);
+ *     ...
+ *     KDBG(DBG_NETIPINIT | DBG_FUNC_END);
+ * }
+ */
 
-*/
 
 extern unsigned int kdebug_enable;
-#define KDEBUG_ENABLE_TRACE   0x1
-#define KDEBUG_ENABLE_ENTROPY 0x2 /* obsolete */
-#define KDEBUG_ENABLE_CHUD    0x4 /* obsolete */
-#define KDEBUG_ENABLE_PPT     0x8
-#define KDEBUG_ENABLE_SERIAL 0x10
 
 /*
- * Infer the supported kernel debug event level from config option.
- * Use (KDEBUG_LEVEL >= KDEBUG_LEVEL_STANDARD) as a guard to protect
- * unaudited debug code.
+ * Bits used by kdebug_enable.  These control which events are traced at
+ * runtime.
+ */
+#define KDEBUG_ENABLE_TRACE   (1U << 0)
+#define KDEBUG_ENABLE_ENTROPY (1U << 1) /* obsolete */
+#define KDEBUG_ENABLE_CHUD    (1U << 2) /* obsolete */
+#define KDEBUG_ENABLE_PPT     (1U << 3)
+#define KDEBUG_ENABLE_SERIAL  (1U << 4)
+
+#define KDEBUG_TRACE (KDEBUG_ENABLE_TRACE)
+
+/*
+ * Specify KDEBUG_PPT to indicate that the event belongs to the limited PPT set.
+ * PPT is deprecated -- use a typefilter and the PPTDBG class instead.
+ */
+#define KDEBUG_PPT    (KDEBUG_ENABLE_PPT)
+#define KDEBUG_COMMON (KDEBUG_ENABLE_TRACE | KDEBUG_ENABLE_PPT)
+
+/*
+ * The kernel debug configuration level.  These values control which events are
+ * compiled in under different build configurations.
+ *
+ * Infer the supported kernel debug event level from config option.  Use
+ * (KDEBUG_LEVEL >= KDEBUG_LEVEL_STANDARD) as a guard to protect unaudited debug
+ * code.
  */
 #define KDEBUG_LEVEL_NONE     0
 #define KDEBUG_LEVEL_IST      1
@@ -715,65 +744,165 @@
 #define KDEBUG_LEVEL KDEBUG_LEVEL_FULL
 #else
 #define KDEBUG_LEVEL KDEBUG_LEVEL_STANDARD
-/* Currently, all other kernel configurations (development, etc)
-   build with KDEBUG_LEVEL_STANDARD.  As a result, KERNEL_DEBUG_CONSTANT*()
-   are on by default but KERNEL_DEBUG*() are not.
-*/
+/*
+ * Currently, all other kernel configurations (development, etc) build with
+ * KDEBUG_LEVEL_STANDARD.  As a result, KERNEL_DEBUG_CONSTANT*() are on by
+ * default but KERNEL_DEBUG*() are not.
+ */
 #endif
 
+#define KDBG_IMPROBABLE
+
+/*
+ * KERNEL_DEBUG_CONSTANT_FILTERED events are omitted from tracing unless they
+ * are explicitly requested in the typefilter.  They are not emitted when
+ * tracing without a typefilter.
+ */
 #if (KDEBUG_LEVEL >= KDEBUG_LEVEL_STANDARD)
-#define KERNEL_DEBUG_CONSTANT(x,a,b,c,d,e)				\
-do {									\
-	if (kdebug_enable & ~KDEBUG_ENABLE_PPT)						\
-        kernel_debug(x,(uintptr_t)a,(uintptr_t)b,(uintptr_t)c,		\
-		       (uintptr_t)d,(uintptr_t)e);			\
-} while(0)
+#define KERNEL_DEBUG_CONSTANT_FILTERED(x, a, b, c, d, ...)             \
+	do {                                                               \
+		if (KDBG_IMPROBABLE(kdebug_enable & ~KDEBUG_ENABLE_PPT)) {     \
+			kernel_debug_filtered((x), (uintptr_t)(a), (uintptr_t)(b), \
+				(uintptr_t)(c), (uintptr_t)(d));                       \
+		}                                                              \
+	} while (0)
+#else /* (KDEBUG_LEVEL >= KDEBUG_LEVEL_STANDARD) */
+#define KERNEL_DEBUG_CONSTANT_FILTERED(type, x, a, b, c, d, ...) do {} while (0)
+#endif /* (KDEBUG_LEVEL >= KDEBUG_LEVEL_STANDARD) */
 
-#define KERNEL_DEBUG_CONSTANT1(x,a,b,c,d,e)				\
-do {									\
-	if (kdebug_enable & ~KDEBUG_ENABLE_PPT)						\
-        kernel_debug1(x,(uintptr_t)a,(uintptr_t)b,(uintptr_t)c,		\
-			(uintptr_t)d,(uintptr_t)e);			\
-} while(0)
+#if (KDEBUG_LEVEL >= KDEBUG_LEVEL_STANDARD)
+#define KERNEL_DEBUG_CONSTANT(x, a, b, c, d, e)                               \
+	do {                                                                      \
+		if (KDBG_IMPROBABLE(kdebug_enable & ~KDEBUG_ENABLE_PPT)) {            \
+			kernel_debug((x), (uintptr_t)(a), (uintptr_t)(b), (uintptr_t)(c), \
+				(uintptr_t)(d),(uintptr_t)(e));                               \
+		}                                                                     \
+	} while (0)
 
-#define KERNEL_DEBUG_EARLY(x,a,b,c,d)					\
-do {									\
-        kernel_debug_early((uint32_t)x,  (uintptr_t)a, (uintptr_t)b,	\
-		           (uintptr_t)c, (uintptr_t)d);			\
-} while(0)
+/*
+ * DO NOT USE THIS MACRO -- it breaks fundamental assumptions about ktrace and
+ * is only meant to be used by the pthread kext and other points in the kernel
+ * where the thread ID must be provided explicitly.
+ */
+#define KERNEL_DEBUG_CONSTANT1(x, a, b, c, d, e)                               \
+	do {                                                                       \
+		if (KDBG_IMPROBABLE(kdebug_enable & ~KDEBUG_ENABLE_PPT)) {             \
+			kernel_debug1((x), (uintptr_t)(a), (uintptr_t)(b), (uintptr_t)(c), \
+			(uintptr_t)(d), (uintptr_t)(e));                                   \
+		}                                                                      \
+	} while (0)
+
+#define KERNEL_DEBUG_EARLY(x, a, b, c, d)                                 \
+	do {                                                                  \
+		kernel_debug_early((uint32_t)(x), (uintptr_t)(a), (uintptr_t)(b), \
+			(uintptr_t)(c), (uintptr_t)(d));                              \
+	} while (0)
 #else /* (KDEBUG_LEVEL >= KDEBUG_LEVEL_STANDARD) */
-#define KERNEL_DEBUG_CONSTANT(x,a,b,c,d,e) do { } while(0)
-#define KERNEL_DEBUG_CONSTANT1(x,a,b,c,d,e) do { } while(0)
-#define KERNEL_DEBUG_EARLY(x,a,b,c,d) do { } while(0)
+#define KERNEL_DEBUG_CONSTANT(x, a, b, c, d, e) do {} while (0)
+#define KERNEL_DEBUG_CONSTANT1(x, a, b, c, d, e) do {} while (0)
+#define KERNEL_DEBUG_EARLY(x, a, b, c, d) do {} while (0)
 #endif /* (KDEBUG_LEVEL >= KDEBUG_LEVEL_STANDARD) */
 
+/*
+ * KERNEL_DEBUG_CONSTANT_IST (in-system trace) events provide an audited subset
+ * of tracepoints for userland system tracing tools.  This tracing level was
+ * created by 8857227 to protect fairplayd and other PT_DENY_ATTACH processes.
+ * It has two effects: only KERNEL_DEBUG_CONSTANT_IST() traces are emitted and
+ * any PT_DENY_ATTACH processes will only emit basic traces as defined by the
+ * kernel_debug_filter() routine.
+ */
+#define KERNEL_DEBUG_CONSTANT_RELEASE(x, a, b, c, d, e) \
+	KERNEL_DEBUG_CONSTANT_IST(~KDEBUG_ENABLE_PPT, x, a, b, c, d, 0)
+
+#if (KDEBUG_LEVEL >= KDEBUG_LEVEL_IST)
+#define KERNEL_DEBUG_CONSTANT_IST(type, x, a, b, c, d, e)                     \
+	do {                                                                      \
+		if (KDBG_IMPROBABLE(kdebug_enable & (type))) {                        \
+			kernel_debug((x), (uintptr_t)(a), (uintptr_t)(b), (uintptr_t)(c), \
+				(uintptr_t)(d), (uintptr_t)(e));                              \
+		}                                                                     \
+	} while (0)
+#else /* (KDEBUG_LEVEL >= KDEBUG_LEVEL_IST) */
+#define KERNEL_DEBUG_CONSTANT_IST(type, x, a, b, c, d, e) do {} while (0)
+#endif /* (KDEBUG_LEVEL >= KDEBUG_LEVEL_IST) */
+
+#if NO_KDEBUG
+#define __kdebug_constant_only __unused
+#endif
 
 /*
- * Specify KDEBUG_PPT to indicate that the event belongs to the
- * limited PPT set.
+ * KERNEL_DEBUG events are only traced for DEBUG kernels.
  */
-#define KDEBUG_COMMON (KDEBUG_ENABLE_TRACE | KDEBUG_ENABLE_PPT)
-#define KDEBUG_TRACE  (KDEBUG_ENABLE_TRACE)
-#define KDEBUG_PPT    (KDEBUG_ENABLE_PPT)
+#define KERNEL_DEBUG_CONSTANT_DEBUG(x, a, b, c, d, e) \
+	KERNEL_DEBUG(x, a, b, c, d, e)
+
+#if (KDEBUG_LEVEL >= KDEBUG_LEVEL_FULL)
+#define __kdebug_only
+
+#define KERNEL_DEBUG(x, a, b, c, d, e)                                  \
+	do {                                                                \
+		if (KDBG_IMPROBABLE(kdebug_enable & ~KDEBUG_ENABLE_PPT)) {      \
+			kernel_debug((uint32_t)(x), (uintptr_t)(a), (uintptr_t)(b), \
+				(uintptr_t)(c), (uintptr_t)(d), (uintptr_t)(e));        \
+		}                                                               \
+	} while (0)
 
 /*
-   KERNEL_DEBUG_CONSTANT_IST events provide an audited subset of
-   tracepoints for userland system tracing tools.  This tracing level was
-   created by 8857227 to protect fairplayd and other PT_DENY_ATTACH
-   processes.  It has two effects: only KERNEL_DEBUG_CONSTANT_IST() traces
-   are emitted and any PT_DENY_ATTACH processes will only emit basic
-   traces as defined by the kernel_debug_filter() routine.
+ * DO NOT USE THIS MACRO -- see warning above for KERNEL_DEBUG_CONSTANT1.
  */
-#if (KDEBUG_LEVEL >= KDEBUG_LEVEL_IST)
-#define KERNEL_DEBUG_CONSTANT_IST(type,x,a,b,c,d,e)			\
-do {									\
-	if (kdebug_enable & type)					\
-        kernel_debug(x,(uintptr_t)a,(uintptr_t)b,(uintptr_t)c,		\
-			(uintptr_t)d,(uintptr_t)e);			\
-} while(0)
+#define KERNEL_DEBUG1(x, a, b, c, d, e)                                  \
+	do {                                                                 \
+		if (KDBG_IMPROBABLE(kdebug_enable & ~KDEBUG_ENABLE_PPT)) {       \
+			kernel_debug1((uint32_t)(x), (uintptr_t)(a), (uintptr_t)(b), \
+				(uintptr_t)(c), (uintptr_t)(d), (uintptr_t)(e));         \
+		}                                                                \
+	} while (0)
+
+#else /* (KDEBUG_LEVEL >= KDEBUG_LEVEL_FULL) */
+#define __kdebug_only __unused
+
+#define KERNEL_DEBUG(x,a,b,c,d,e) do {} while (0)
+#define KERNEL_DEBUG1(x,a,b,c,d,e) do {} while (0)
+#endif /* (KDEBUG_LEVEL >= KDEBUG_LEVEL_FULL) */
+
 
+extern void kernel_debug(
+		uint32_t  debugid,
+		uintptr_t arg1,
+		uintptr_t arg2,
+		uintptr_t arg3,
+		uintptr_t arg4,
+		uintptr_t arg5);
+
+extern void kernel_debug1(
+		uint32_t  debugid,
+		uintptr_t arg1,
+		uintptr_t arg2,
+		uintptr_t arg3,
+		uintptr_t arg4,
+		uintptr_t arg5);
+
+extern void kernel_debug_filtered(
+		uint32_t  debugid,
+		uintptr_t arg1,
+		uintptr_t arg2,
+		uintptr_t arg3,
+		uintptr_t arg4);
+
+extern void kernel_debug_early(
+		uint32_t  debugid,
+		uintptr_t arg1,
+		uintptr_t arg2,
+		uintptr_t arg3,
+		uintptr_t arg4);
+
+/*
+ * EnergyTracing macros.
+ */
+
+#if (KDEBUG_LEVEL >= KDEBUG_LEVEL_IST)
 // whether to bother calculating EnergyTracing inputs
-// could chnage in future to see if DBG_ENERGYTRACE is active
+// could change in future to see if DBG_ENERGYTRACE is active
 #define ENTR_SHOULDTRACE kdebug_enable
 // encode logical EnergyTracing into 32/64 KDebug trace
 #define ENTR_KDTRACE(component, opcode, lifespan, id, quality, value) 	\
@@ -817,7 +946,6 @@
 
 #else /* (KDEBUG_LEVEL >= KDEBUG_LEVEL_IST) */
 
-#define KERNEL_DEBUG_CONSTANT_IST(type,x,a,b,c,d,e) do { } while(0)
 #define ENTR_SHOULDTRACE FALSE
 #define ENTR_KDTRACE(component, opcode, lifespan, id, quality, value) 	\
 				    do {} while (0)
@@ -827,58 +955,10 @@
 
 #endif /* (KDEBUG_LEVEL >= KDEBUG_LEVEL_IST) */
 
-#if NO_KDEBUG
-#define __kdebug_constant_only __unused
-#endif
-
-extern void kernel_debug(
-		uint32_t  debugid,
-		uintptr_t arg1,
-		uintptr_t arg2,
-		uintptr_t arg3,
-		uintptr_t arg4,
-		uintptr_t arg5);
-
-extern void kernel_debug1(
-		uint32_t  debugid,
-		uintptr_t arg1,
-		uintptr_t arg2,
-		uintptr_t arg3,
-		uintptr_t arg4,
-		uintptr_t arg5);
-
-extern void kernel_debug_early(
-		uint32_t  debugid,
-		uintptr_t arg1,
-		uintptr_t arg2,
-		uintptr_t arg3,
-		uintptr_t arg4);
-
 
-#if (KDEBUG_LEVEL >= KDEBUG_LEVEL_FULL)
-#define KERNEL_DEBUG(x,a,b,c,d,e)					\
-do {									\
-	if (kdebug_enable & ~KDEBUG_ENABLE_PPT)				\
-        kernel_debug((uint32_t)x,  (uintptr_t)a, (uintptr_t)b,		\
-		     (uintptr_t)c, (uintptr_t)d, (uintptr_t)e);		\
-} while(0)
-
-#define KERNEL_DEBUG1(x,a,b,c,d,e)					\
-do {									\
-	if (kdebug_enable & ~KDEBUG_ENABLE_PPT)				\
-        kernel_debug1((uint32_t)x,  (uintptr_t)a, (uintptr_t)b,		\
-		      (uintptr_t)c, (uintptr_t)d, (uintptr_t)e);	\
-} while(0)
-
-#else /* (KDEBUG_LEVEL >= KDEBUG_LEVEL_FULL) */
-
-#define KERNEL_DEBUG(x,a,b,c,d,e) do {} while (0)
-#define KERNEL_DEBUG1(x,a,b,c,d,e) do {} while (0)
-
-#define __kdebug_only __unused
-#endif /* (KDEBUG_LEVEL >= KDEBUG_LEVEL_FULL) */
-
-// KDEBUG COMMPAGE BITs
+/*
+ * Bits set in the comm page for kdebug.
+ */
 #define KDEBUG_COMMPAGE_ENABLE_TRACE      0x1
 #define KDEBUG_COMMPAGE_ENABLE_TYPEFILTER 0x2 /* Forced to false if ENABLE_TRACE is 0 */
 
@@ -917,5 +997,4 @@
 __END_DECLS
 
 
-
 #endif /* !BSD_SYS_KDEBUG_H */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebugevents.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebugevents.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebugevents.h	2016-06-03 22:55:54.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebugevents.h	2016-06-29 00:56:55.000000000 +0200
@@ -132,9 +132,9 @@
         {0x10c010c, "MSC_kern_invalid_#67"},
         {0x10c0110, "MSC_kern_invalid_#68"},
         {0x10c0114, "MSC_kern_invalid_#69"},
-        {0x10c0118, "MSC_kern_invalid_#70"},
+        {0x10c0118, "MSC_host_create_mach_voucher_trap"},
         {0x10c011c, "MSC_kern_invalid_#71"},
-        {0x10c0120, "MSC_kern_invalid_#72"},
+        {0x10c0120, "MSC_mach_voucher_extract_attr_recipe_trap"},
         {0x10c0124, "MSC_kern_invalid_#73"},
         {0x10c0128, "MSC_kern_invalid_#74"},
         {0x10c012c, "MSC_kern_invalid_#75"},
@@ -1225,7 +1225,7 @@
         {0x40c05a8, "BSC_kqueue"},
         {0x40c05ac, "BSC_kevent"},
         {0x40c05b0, "BSC_lchown"},
-        {0x40c05b4, "BSC_stack_snapshot"},
+        {0x40c05b4, "BSC_obs_stack_snapshot"},
         {0x40c05b8, "BSC_bsdthread_register"},
         {0x40c05bc, "BSC_workq_open"},
         {0x40c05c0, "BSC_workq_kernreturn"},
@@ -1462,8 +1462,8 @@
         {0x50700e4, "PM_UserActiveState"},
         {0x50700e8, "PM_AppResponseDelay"},
         {0x50700ec, "PM_DriverResponseDelay"},
-        {0x50700ec, "PM_PCIDevChangeDone"},
         {0x50700f0, "PM_PCIDevChangeStart"},
+        {0x50700f4, "PM_PCIDevChangeDone"},
         {0x5080004, "IOSERVICE_BUSY"},
         {0x5080008, "IOSERVICE_NONBUSY"},
         {0x508000c, "IOSERVICE_MODULESTALL"},
@@ -1926,6 +1926,21 @@
         {0x1f040010, "DYLD_map_bundle_image"},
         {0x1f040014, "DYLD_load_dependent_libraries"},
         {0x1f040018, "DYLD_notify_prebinding_agent"},
+        {0x1f050000, "DYLD_uuid_map_a"},
+        {0x1f050004, "DYLD_uuid_map_b"},
+        {0x1f050008, "DYLD_uuid_map_32_a"},
+        {0x1f05000c, "DYLD_uuid_map_32_b"},
+        {0x1f050010, "DYLD_uuid_map_32_c"},
+        {0x1f050014, "DYLD_uuid_unmap_a"},
+        {0x1f050018, "DYLD_uuid_unmap_b"},
+        {0x1f05001c, "DYLD_uuid_unmap_32_a"},
+        {0x1f050020, "DYLD_uuid_unmap_32_b"},
+        {0x1f050024, "DYLD_uuid_unmap_32_c"},
+        {0x1f050028, "DYLD_uuid_shared_cache_a"},
+        {0x1f05002c, "DYLD_uuid_shared_cache_b"},
+        {0x1f050030, "DYLD_uuid_shared_cache_32_a"},
+        {0x1f050034, "DYLD_uuid_shared_cache_32_b"},
+        {0x1f050038, "DYLD_uuid_shared_cache_32_c"},
         {0x1ff10000, "SCROLL_BEGIN_obs"},
         {0x1ff10100, "SCROLL_END_obs"},
         {0x1ff20000, "BOOT_BEGIN_obs"},
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/socket.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/socket.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/socket.h	2016-06-03 22:55:51.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/socket.h	2016-06-29 00:56:52.000000000 +0200
@@ -276,31 +276,11 @@
 
 #define	SO_NETSVC_MARKING_LEVEL	0x1119	/* Get QoS marking in effect for socket */
 
-/*
- * NETSVC_MRKNG_UNKNOWN
- *
- * The outgoing network interface is not known
- */
-#define	NETSVC_MRKNG_UNKNOWN		0
-/*
- * NETSVC_MRKNG_LVL_L2
- *
- * Default marking at layer 2 (for example Wi=Fi WMM)
- */
-#define	NETSVC_MRKNG_LVL_L2		1
-/*
- * NETSVC_MRKNG_LVL_ALL_L3L2
- *
- * Layer 3 DSCP marking and layer 2 marking for all Network Service Types
- */
-#define	NETSVC_MRKNG_LVL_L3L2_ALL	2
-/*
- * NETSVC_MRKNG_LVL_BK_L3L2
- *
- * The system policy limits layer 3 DSCP marking and layer 2 marking
- * to background Network Service Types
- */
-#define	NETSVC_MRKNG_LVL_L3L2_BK	3
+#define	NETSVC_MRKNG_UNKNOWN		0	/* The outgoing network interface is not known */
+#define	NETSVC_MRKNG_LVL_L2		1	/* Default marking at layer 2 (for example Wi-Fi WMM) */
+#define	NETSVC_MRKNG_LVL_L3L2_ALL	2	/* Layer 3 DSCP marking and layer 2 marking for all Network Service Types */
+#define	NETSVC_MRKNG_LVL_L3L2_BK	3	/* The system policy limits layer 3 DSCP marking and layer 2 marking
+						 * to background Network Service Types */
 
 typedef __uint32_t sae_associd_t;
 #define	SAE_ASSOCID_ANY	0
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h	2016-06-03 22:55:54.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h	2016-06-29 00:56:55.000000000 +0200
@@ -29,7 +29,7 @@
  * System call switch table.
  *
  * DO NOT EDIT-- this file is automatically generated.
- * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3705.0.0.1.10/bsd/kern/syscalls.master
+ * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3757.0.0.0.1/bsd/kern/syscalls.master
  */
 
 #ifndef _SYS_SYSCALL_H_
@@ -402,6 +402,7 @@
 #define	SYS_kqueue         362
 #define	SYS_kevent         363
 #define	SYS_lchown         364
+			/* 365  old stack_snapshot */
 #define	SYS_stack_snapshot 365
 #define	SYS_bsdthread_register 366
 #define	SYS_workq_open     367
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysctl.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysctl.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysctl.h	2016-06-03 22:55:52.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysctl.h	2016-06-29 00:56:52.000000000 +0200
@@ -540,32 +540,33 @@
 #define KERN_TFP_POLICY_DEFAULT 	2	/* Default  Mode: related ones allowed and upcall authentication */
 
 /* KERN_KDEBUG types */
-#define KERN_KDEFLAGS		1
-#define KERN_KDDFLAGS		2
-#define KERN_KDENABLE		3
-#define KERN_KDSETBUF		4
-#define KERN_KDGETBUF		5
-#define KERN_KDSETUP		6
-#define KERN_KDREMOVE		7
-#define KERN_KDSETREG		8
-#define KERN_KDGETREG		9
-#define KERN_KDREADTR		10
-#define KERN_KDPIDTR		11
-#define KERN_KDTHRMAP           12
+#define KERN_KDEFLAGS         1
+#define KERN_KDDFLAGS         2
+#define KERN_KDENABLE         3
+#define KERN_KDSETBUF         4
+#define KERN_KDGETBUF         5
+#define KERN_KDSETUP          6
+#define KERN_KDREMOVE         7
+#define KERN_KDSETREG         8
+#define KERN_KDGETREG         9
+#define KERN_KDREADTR         10
+#define KERN_KDPIDTR          11
+#define KERN_KDTHRMAP         12
 /* Don't use 13 as it is overloaded with KERN_VNODE */
-#define KERN_KDPIDEX            14
-#define KERN_KDSETRTCDEC        15 /* obsolete */
-#define KERN_KDGETENTROPY       16 /* obsolete */
-#define KERN_KDWRITETR		17
-#define KERN_KDWRITEMAP		18
-/* 19 - 20 unused */
-#define KERN_KDREADCURTHRMAP	21
-#define KERN_KDSET_TYPEFILTER   22
-#define KERN_KDBUFWAIT		23
-#define KERN_KDCPUMAP		24
+#define KERN_KDPIDEX          14
+#define KERN_KDSETRTCDEC      15 /* obsolete */
+#define KERN_KDGETENTROPY     16 /* obsolete */
+#define KERN_KDWRITETR        17
+#define KERN_KDWRITEMAP       18
+#define KERN_KDTEST           19
+/* 20 unused */
+#define KERN_KDREADCURTHRMAP  21
+#define KERN_KDSET_TYPEFILTER 22
+#define KERN_KDBUFWAIT        23
+#define KERN_KDCPUMAP         24
 /* 25 - 26 unused */
-#define KERN_KDWRITEMAP_V3	27
-#define KERN_KDWRITETR_V3	28
+#define KERN_KDWRITEMAP_V3    27
+#define KERN_KDWRITETR_V3     28
 
 #define CTL_KERN_NAMES { \
 	{ 0, 0 }, \
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h	2016-06-03 22:55:54.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h	2016-06-29 00:56:55.000000000 +0200
@@ -29,7 +29,7 @@
  * System call switch table.
  *
  * DO NOT EDIT-- this file is automatically generated.
- * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3705.0.0.1.10/bsd/kern/syscalls.master
+ * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3757.0.0.0.1/bsd/kern/syscalls.master
  */
 
 #ifndef _SYS_SYSPROTO_H_
@@ -1452,6 +1452,8 @@
 	char owner_l_[PADL_(uid_t)]; uid_t owner; char owner_r_[PADR_(uid_t)];
 	char group_l_[PADL_(gid_t)]; gid_t group; char group_r_[PADR_(gid_t)];
 };
+#if CONFIG_EMBEDDED
+#else
 struct stack_snapshot_args {
 	char pid_l_[PADL_(pid_t)]; pid_t pid; char pid_r_[PADR_(pid_t)];
 	char tracebuf_l_[PADL_(user_addr_t)]; user_addr_t tracebuf; char tracebuf_r_[PADR_(user_addr_t)];
@@ -1459,6 +1461,7 @@
 	char flags_l_[PADL_(uint32_t)]; uint32_t flags; char flags_r_[PADR_(uint32_t)];
 	char dispatch_offset_l_[PADL_(uint32_t)]; uint32_t dispatch_offset; char dispatch_offset_r_[PADR_(uint32_t)];
 };
+#endif
 #if CONFIG_WORKQUEUE
 struct bsdthread_register_args {
 	char threadstart_l_[PADL_(user_addr_t)]; user_addr_t threadstart; char threadstart_r_[PADR_(user_addr_t)];
@@ -2582,7 +2585,10 @@
 int kqueue(struct proc *, struct kqueue_args *, int *);
 int kevent(struct proc *, struct kevent_args *, int *);
 int lchown(struct proc *, struct lchown_args *, int *);
+#if CONFIG_EMBEDDED
+#else
 int stack_snapshot(struct proc *, struct stack_snapshot_args *, int *);
+#endif
 #if CONFIG_WORKQUEUE
 int bsdthread_register(struct proc *, struct bsdthread_register_args *, int *);
 int workq_open(struct proc *, struct workq_open_args *, int *);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/uuid/uuid.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/uuid/uuid.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/uuid/uuid.h	2016-06-03 22:55:11.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/uuid/uuid.h	2016-06-29 00:56:07.000000000 +0200
@@ -46,6 +46,8 @@
 #define UUID_DEFINE(name,u0,u1,u2,u3,u4,u5,u6,u7,u8,u9,u10,u11,u12,u13,u14,u15) \
 	static const uuid_t name __attribute__ ((unused)) = {u0,u1,u2,u3,u4,u5,u6,u7,u8,u9,u10,u11,u12,u13,u14,u15}
 
+UUID_DEFINE(UUID_NULL, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0);
+
 #ifdef __cplusplus
 extern "C" {
 #endif
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vBasicOps.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vBasicOps.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vBasicOps.h	2016-06-03 23:09:20.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vBasicOps.h	2016-06-29 01:09:47.000000000 +0200
@@ -3,7 +3,7 @@
  
      Contains:   Basic Algebraic Operations for AltiVec
  
-     Version:    vecLib-595.0
+     Version:    vecLib-599.0
  
      Copyright:  Copyright (c) 1999-2016 by Apple Inc. All rights reserved.
  
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vDSP.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vDSP.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vDSP.h	2016-06-03 23:09:20.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vDSP.h	2016-06-29 01:09:47.000000000 +0200
@@ -3,7 +3,7 @@
 
     Contains:   AltiVec DSP Interfaces
 
-    Version:    vecLib-595.0
+    Version:    vecLib-599.0
 
     Copyright:  Copyright (c) 2000-2016 by Apple Inc. All rights reserved.
 
@@ -244,7 +244,7 @@
     vDSP_Version0 is a major version number.
     vDSP_Version1 is a minor version number.
 */
-#define vDSP_Version0   595
+#define vDSP_Version0   599
 #define vDSP_Version1   0
 
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vForce.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vForce.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vForce.h	2016-06-03 23:09:20.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vForce.h	2016-06-29 01:09:47.000000000 +0200
@@ -1,5 +1,5 @@
 /*
-vForce.h (from vecLib-595.0)
+vForce.h (from vecLib-599.0)
 Copyright (c) 1999-2016 by Apple Inc. All rights reserved.
 
 @APPLE_LICENSE_HEADER_START@
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vecLib.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vecLib.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vecLib.h	2016-06-03 23:09:20.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vecLib.h	2016-06-29 01:09:47.000000000 +0200
@@ -3,7 +3,7 @@
  
      Contains:   Master include for vecLib framework
  
-     Version:    vecLib-595.0
+     Version:    vecLib-599.0
  
      Copyright:  Copyright (c) 2000-2016 by Apple Inc. All rights reserved.
  
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vecLibTypes.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vecLibTypes.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vecLibTypes.h	2016-06-03 23:09:20.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/vecLib/vecLibTypes.h	2016-06-29 01:09:47.000000000 +0200
@@ -3,7 +3,7 @@
  
      Contains:   Master include for vecLib framework
  
-     Version:    vecLib-595.0
+     Version:    vecLib-599.0
  
      Copyright:  Copyright (c) 2000-2016 by Apple Inc. All rights reserved.
  

```