#Kernel.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IORegistryEntry.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IORegistryEntry.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IORegistryEntry.h	2016-07-10 08:21:58.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IORegistryEntry.h	2016-07-27 03:31:19.000000000 +0200
@@ -55,7 +55,6 @@
 enum {
     kIORegistryIterateRecursively   = 0x00000001,
     kIORegistryIterateParents       = 0x00000002,
-    kIORegistryIterateFromUser      = 0x00000004
 };
 
 /*! @class IORegistryEntry : public OSObject
@@ -180,13 +179,7 @@
 
 private:
 #if __LP64__
-#if __x86_64__
-    virtual OSArray * getChildSetReferenceWithOptions( const IORegistryPlane * plane, IOOptionBits options = 0 ) const;
-    OSMetaClassDeclareReservedUsed(IORegistryEntry, 0);
-#else
     OSMetaClassDeclareReservedUnused(IORegistryEntry, 0);
-#endif
-
     OSMetaClassDeclareReservedUnused(IORegistryEntry, 1);
     OSMetaClassDeclareReservedUnused(IORegistryEntry, 2);
     OSMetaClassDeclareReservedUnused(IORegistryEntry, 3);
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOReportMacros.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOReportMacros.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOReportMacros.h	2016-07-10 08:21:58.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/IOReportMacros.h	2016-07-27 03:31:20.000000000 +0200
@@ -30,6 +30,7 @@
 #define _IOREPORT_MACROS_H_
 
 #include "IOReportTypes.h"
+#include <string.h>
 
 #ifdef __cplusplus
 extern "C" {
@@ -74,16 +75,17 @@
  * IOReportCategories categories - categories of this channel
  *
  * If the buffer is not of sufficient size, the macro calls IOREPORT_ABORT().
- * If that returns, the buffer is filled with 0xbadcafe.
+ * If that returns, the buffer is left full of '&'.
  */
 
-#define SIMPLEREPORT_INIT(buffer, bufSize, providerID, channelID, cats)  \
+#define SIMPLEREPORT_INIT(buf, bufSize, providerID, channelID, cats)  \
 do {  \
-    IOReportElement     *__elem = (IOReportElement *)(buffer);  \
+    memset((buf), '&', (bufSize));  \
+    IOReportElement     *__elem = (IOReportElement *)(buf);  \
     IOSimpleReportValues *__vals;  \
     if ((bufSize) >= SIMPLEREPORT_BUFSIZE) {  \
-        __elem->channel_id = (channelID);  \
         __elem->provider_id = (providerID);  \
+        __elem->channel_id = (channelID);  \
         __elem->channel_type.report_format = kIOReportFormatSimple;  \
         __elem->channel_type.reserved = 0;  \
         __elem->channel_type.categories = (cats);  \
@@ -95,7 +97,6 @@
     }  \
     else {  \
         IOREPORT_ABORT("bufSize is smaller than the required size\n");  \
-        __POLLUTE_BUF((buffer), (bufSize));  \
     }  \
 } while(0)
 
@@ -225,10 +226,11 @@
  * IOReportCategories categories - categories of this channel
  *
  * If the buffer is not of sufficient size, the macro invokes IOREPORT_ABORT.
- * If that returns, the buffer is filled with 0xbadcafe.
+ * If that returns, the buffer is left full of '&'.
  */
 #define STATEREPORT_INIT(nstates, buf, bufSize, providerID, channelID, cats) \
 do {  \
+    memset((buf), '&', (bufSize));  \
     IOStateReportInfo *__info = (IOStateReportInfo *)(buf);  \
     IOStateReportValues *__rep;  \
     IOReportElement     *__elem;  \
@@ -236,8 +238,8 @@
         for (unsigned __no = 0; __no < (nstates); __no++) {  \
             __elem =  &(__info->elem[__no]);  \
             __rep = (IOStateReportValues *) &(__elem->values);  \
-            __elem->channel_id = (channelID);  \
             __elem->provider_id = (providerID);  \
+            __elem->channel_id = (channelID);  \
             __elem->channel_type.report_format = kIOReportFormatState;  \
             __elem->channel_type.reserved = 0;  \
             __elem->channel_type.categories = (cats);  \
@@ -247,13 +249,13 @@
             __rep->state_id = __no;  \
             __rep->intransitions = 0;  \
             __rep->upticks = 0;  \
+            __rep->last_intransition = 0;  \
         }  \
         __info->curr_state = 0;  \
         __info->update_ts = 0;  \
     }  \
     else {  \
         IOREPORT_ABORT("bufSize is smaller than the required size\n");  \
-        __POLLUTE_BUF((buf), (bufSize));  \
     }  \
 } while(0)
 
@@ -408,12 +410,13 @@
  *            uint64_t channelID   - ID of this channel, see IOREPORT_MAKEID()
  * IOReportCategories categories   - categories of this channel
  *
- * If the buffer is not of sufficient size, the macro invokes IOREPORT_ABORT()
- * and, if that returns, fills the buffer with 0xbadcafe.
+ * If the buffer is not of sufficient size, the macro invokes IOREPORT_ABORT().
+ * If that returns, the buffer is left full of '&'.
  */
 
 #define SIMPLEARRAY_INIT(nValues, buf, bufSize, providerID, channelID, cats) \
 do {  \
+    memset((buf), '&', (bufSize));  \
     IOSimpleArrayReportValues *__rep;  \
     IOReportElement     *__elem;  \
     uint32_t            __nElems = (((nValues) / IOR_VALUES_PER_ELEMENT) + \
@@ -422,8 +425,8 @@
         for (unsigned __no = 0; __no < __nElems; __no++) {  \
             __elem =  &(((IOReportElement *)(buf))[__no]);  \
             __rep = (IOSimpleArrayReportValues *) &(__elem->values);  \
-            __elem->channel_id = (channelID);  \
             __elem->provider_id = (providerID);  \
+            __elem->channel_id = (channelID);  \
             __elem->channel_type.report_format = kIOReportFormatSimpleArray;  \
             __elem->channel_type.reserved = 0;  \
             __elem->channel_type.categories = (cats);  \
@@ -438,7 +441,6 @@
     }  \
     else {  \
         IOREPORT_ABORT("bufSize is smaller than the required size\n");  \
-        __POLLUTE_BUF((buf), (bufSize));  \
     }  \
 } while(0)
 
@@ -584,10 +586,11 @@
  * IOReportCategories categories - categories of this channel
  *
  * If the buffer is not of sufficient size, the macro invokes IOREPORT_ABORT.
- * If that returns, the buffer is filled with 0xbadcafe.
+ * If that returns, the buffer is left full of '&'.
  */
 #define HISTREPORT_INIT(nbuckets, bktSize, buf, bufSize, providerID, channelID, cats) \
 do {  \
+    memset((buf), '&', (bufSize));  \
     IOHistReportInfo   *__info = (IOHistReportInfo *)(buf);  \
     IOReportElement         *__elem;  \
     IOHistogramReportValues *__rep;  \
@@ -596,20 +599,19 @@
         for (unsigned __no = 0; __no < (nbuckets); __no++) {  \
             __elem =  &(__info->elem[__no]);  \
             __rep = (IOHistogramReportValues *) &(__elem->values);  \
-            __elem->channel_id = (channelID);  \
             __elem->provider_id = (providerID);  \
+            __elem->channel_id = (channelID);  \
             __elem->channel_type.report_format = kIOReportFormatHistogram;  \
             __elem->channel_type.reserved = 0;  \
             __elem->channel_type.categories = (cats);  \
             __elem->channel_type.nelements = (nbuckets);  \
             __elem->channel_type.element_idx = __no;  \
             __elem->timestamp = 0;  \
-            bzero(__rep, sizeof(IOHistogramReportValues)); \
+            memset(__rep, '\0', sizeof(IOHistogramReportValues)); \
         }  \
     }  \
     else {  \
         IOREPORT_ABORT("bufSize is smaller than the required size\n");  \
-        __POLLUTE_BUF((buf), (bufSize));  \
     }  \
 } while (0)
 
@@ -696,17 +698,6 @@
 #define HISTREPORT_GETCHTYPE(hist_buf)  \
     (*(uint64_t*)&(((IOHistReportInfo *)(hist_buf))->elem[0].channel_type))
 
-
-
-/* generic utilities */
-
-    #define __POLLUTE_BUF(buf, bufSize)  \
-    do {  \
-        int __cnt = (bufSize)/sizeof(uint32_t);  \
-        while (--__cnt >= 0)  \
-            ((uint32_t*)(buf))[__cnt] = 0xbadcafe;  \
-    } while (0)
-
 #ifdef __cplusplus
 }
 #endif
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDKeys.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDKeys.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDKeys.h	2016-07-10 08:58:23.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDKeys.h	2016-07-27 03:48:35.000000000 +0200
@@ -29,6 +29,7 @@
 #include <IOKit/hidsystem/IOHIDParameter.h>
 #include <IOKit/IOReturn.h>
 #include <IOKit/IOMessage.h>
+#include <IOKit/hid/IOHIDProperties.h>
 
 __BEGIN_DECLS
 
@@ -413,7 +414,6 @@
  @discussion Legacy IOHIDKeyboard keys, formerly in IOHIDPrivateKeys. See IOHIDServiceKeys.h for the new keys.
  */
 #define kIOHIDKeyboardCapsLockDelay         "CapsLockDelay"
-#define kIOHIDKeyboardCapsLockDelayOverride "CapsLockDelayOverride"
 #define kIOHIDKeyboardEjectDelay            "EjectDelay"
 
 /*!
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDProperties.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDProperties.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDProperties.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hid/IOHIDProperties.h	2016-07-27 03:48:35.000000000 +0200
@@ -0,0 +1,124 @@
+/*
+ * Copyright (c) 2016 Apple Computer, Inc. All rights reserved.
+ *
+ * @APPLE_LICENSE_HEADER_START@
+ *
+ * This file contains Original Code and/or Modifications of Original Code
+ * as defined in and that are subject to the Apple Public Source License
+ * Version 2.0 (the 'License'). You may not use this file except in
+ * compliance with the License. Please obtain a copy of the License at
+ * http://www.opensource.apple.com/apsl/ and read it before using this
+ * file.
+ *
+ * The Original Code and all software distributed under the License are
+ * distributed on an 'AS IS' basis, WITHOUT WARRANTY OF ANY KIND, EITHER
+ * EXPRESS OR IMPLIED, AND APPLE HEREBY DISCLAIMS ALL SUCH WARRANTIES,
+ * INCLUDING WITHOUT LIMITATION, ANY WARRANTIES OF MERCHANTABILITY,
+ * FITNESS FOR A PARTICULAR PURPOSE, QUIET ENJOYMENT OR NON-INFRINGEMENT.
+ * Please see the License for the specific language governing rights and
+ * limitations under the License.
+ *
+ * @APPLE_LICENSE_HEADER_END@
+ */
+
+#ifndef IOHIDProperties_h
+#define IOHIDProperties_h
+
+/*!
+ * @define      kIOHIDPointerAccelerationKey
+ *
+ * @abstract    CFNumber that contains the pointer acceleration value.
+ */
+#define kIOHIDPointerAccelerationKey                "HIDPointerAcceleration"
+
+/*!
+ * @define      kIOHIDPointerAccelerationTypeKey
+ *
+ * @abstract    CFString containing the type of acceleration for pointer.
+ *              Supported types are:
+ *                  <code>kIOHIDPointerAccelerationKey</code>
+ *                  <code>kIOHIDMouseScrollAccelerationKey</code>
+ *                  <code>kIOHIDTrackpadAccelerationType</code>
+ */
+#define kIOHIDPointerAccelerationTypeKey            "HIDPointerAccelerationType"
+
+/*!
+ * @define      kIOHIDMouseScrollAccelerationKey
+ *
+ * @abstract    CFNumber that contains the mouse scroll acceleration value.
+ */
+#define kIOHIDMouseScrollAccelerationKey            "HIDMouseScrollAcceleration"
+
+/*!
+ * @define      kIOHIDMouseAccelerationType
+ *
+ * @abstract    CFNumber that contains the mouse acceleration value.
+ */
+#define kIOHIDMouseAccelerationType                 "HIDMouseAcceleration"
+#define kIOHIDMouseAccelerationTypeKey              kIOHIDMouseAccelerationType
+
+/*!
+ * @define      kIOHIDScrollAccelerationKey
+ *
+ * @abstract    CFNumber that contains the scroll acceleration value.
+ */
+#define kIOHIDScrollAccelerationKey                 "HIDScrollAcceleration"
+
+/*!
+ * @define      kIOHIDScrollAccelerationTypeKey
+ *
+ * @abstract    CFString containing the type of acceleration for scroll.
+ *              Supported types are:
+ *                  <code>kIOHIDMouseScrollAccelerationKey</code>
+ *                  <code>kIOHIDTrackpadScrollAccelerationKey</code>
+ */
+#define kIOHIDScrollAccelerationTypeKey             "HIDScrollAccelerationType"
+
+/*!
+ * @define      kIOHIDPointerButtonMode
+ *
+ * @abstract    CFNumber containing the current pointer button mode.
+ *              See IOHIDButtonModes enumerator for possible modes.
+ */
+#define kIOHIDPointerButtonMode                     "HIDPointerButtonMode"
+#define kIOHIDPointerButtonModeKey                  kIOHIDPointerButtonMode
+
+/*!
+ * @define      kIOHIDUserUsageMapKey
+ *
+ * @abstract    CFArray of dictionaries that contain user defined key mappings.
+ */
+#define kIOHIDUserUsageMapKey                       "UserKeyMapping"
+
+/*!
+ * @define      kIOHIDKeyboardCapsLockDelayOverride
+ *
+ * @abstract    CFNumber containing the delay (in ms) before the caps lock key is activated.
+ */
+#define kIOHIDKeyboardCapsLockDelayOverride         "CapsLockDelayOverride"
+#define kIOHIDKeyboardCapsLockDelayOverrideKey      kIOHIDKeyboardCapsLockDelayOverride
+
+/*!
+ * @define      kIOHIDServiceEjectDelayKey
+ *
+ * @abstract    CFNumber containing the delay (in ms) before the eject key is activated.
+ */
+#define kIOHIDServiceEjectDelayKey                  "EjectDelay"
+
+/*!
+ * @define      kIOHIDServiceInitialKeyRepeatDelayKey
+ *
+ * @abstract    CFNumber containing the delay (in ns) before the initial key repeat.
+ *              If value is 0, there are no repeats.
+ */
+#define kIOHIDServiceInitialKeyRepeatDelayKey       "HIDInitialKeyRepeat"
+
+/*!
+ * @define      kIOHIDServiceKeyRepeatDelayKey
+ *
+ * @abstract    CFNumber containing the delay (in ns) for subsequent key repeats.
+ *              If value is 0, there are no repeats (including initial).
+ */
+#define kIOHIDServiceKeyRepeatDelayKey              "HIDKeyRepeat"
+
+#endif /* IOHIDProperties_h */
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDParameter.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDParameter.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDParameter.h	2016-07-10 08:58:23.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidsystem/IOHIDParameter.h	2016-07-27 03:48:35.000000000 +0200
@@ -39,6 +39,7 @@
 /* Public type definitions. */
 #include <IOKit/hidsystem/IOHIDTypes.h>
 #include <IOKit/hidsystem/IOLLEvent.h>
+#include <IOKit/hid/IOHIDProperties.h>
 
 /*
  * Identify this driver as one that uses the new driverkit and messaging API
@@ -71,7 +72,11 @@
 #define kIOHIDKeyboardSupportsF12EjectKey       "HIDKeyboardSupportsF12Eject"
 #define kIOHIDKeyboardSupportedModifiersKey     "HIDKeyboardSupportedModifiers"
 #define kIOHIDKeyboardGlobalModifiersKey        "HIDKeyboardGlobalModifiers"
-#define kIOHIDServiceUseGlobalModifiersKey      "HIDServiceUseGlobalModifiers"
+
+//read only property that specify usage of clobal modifiers
+// Bit[0] -  Report modifiers to the service by setting kIOHIDKeyboardGlobalModifiersKey  with global modifiers
+// Bit[1] -  Update/translate events from service taking global modifiers state in consideration
+#define kIOHIDServiceGlobalModifiersUsageKey     "HIDServiceGlobalModifiersUsage"
 
 
 #define kIOHIDPointerResolutionKey		"HIDPointerResolution"
@@ -79,19 +84,14 @@
 #define kIOHIDPointerConvertAbsoluteKey	"HIDPointerConvertAbsolute"
 #define kIOHIDPointerContactToMoveKey	"HIDPointerContactToMove"
 #define kIOHIDPointerPressureToClickKey	"HIDPointerPressureToClick"
-#define kIOHIDPointerButtonMode			"HIDPointerButtonMode"
 #define kIOHIDPointerButtonCountKey	"HIDPointerButtonCount"
 
-#define kIOHIDPointerAccelerationKey	"HIDPointerAcceleration"
 #define kIOHIDPointerAccelerationSettingsKey	"HIDPointerAccelerationSettings"
-#define kIOHIDPointerAccelerationTypeKey	"HIDPointerAccelerationType"
 #define kIOHIDPointerAccelerationTableKey  "HIDPointerAccelerationTable"
 
 #define kIOHIDScrollResetKey			"HIDScrollReset"
 #define kIOHIDScrollResolutionKey		"HIDScrollResolution"
 #define kIOHIDScrollReportRateKey       "HIDScrollReportRate"
-#define kIOHIDScrollAccelerationKey		"HIDScrollAcceleration"
-#define kIOHIDScrollAccelerationTypeKey     "HIDScrollAccelerationType"
 #define kIOHIDScrollAccelerationTableKey	"HIDScrollAccelerationTable"
 
 #define kIOHIDScrollResolutionXKey		"HIDScrollResolutionX"
@@ -107,10 +107,8 @@
 #define kIOHIDScrollZoomModifierMaskKey "HIDScrollZoomModifierMask"
 
 #define kIOHIDTrackpadScrollAccelerationKey "HIDTrackpadScrollAcceleration"
-#define kIOHIDMouseScrollAccelerationKey   "HIDMouseScrollAcceleration"
 
 #define kIOHIDTrackpadAccelerationType	"HIDTrackpadAcceleration"
-#define kIOHIDMouseAccelerationType		"HIDMouseAcceleration"
 
 #define kIOHIDClickTimeKey				"HIDClickTime"
 #define kIOHIDClickSpaceKey				"HIDClickSpace"
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/bits.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/bits.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/bits.h	2016-07-10 08:22:01.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/kern/bits.h	2016-07-27 03:31:17.000000000 +0200
@@ -1,8 +1,8 @@
 /*
- * Copyright (c) 2015 Apple Inc. All rights reserved.
+ * Copyright (c) 2015-2016 Apple Inc. All rights reserved.
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
  *
  * Bit manipulation functions
@@ -31,6 +31,10 @@
 #ifndef __BITS_H__
 #define __BITS_H__
 
+#include <kern/kalloc.h>
+#include <stdbool.h>
+#include <stdint.h>
+
 typedef unsigned int			uint;
 
 #define BIT(b)				(1ULL << (b))
@@ -119,16 +123,21 @@
 
 typedef _Atomic uint64_t		bitmap_t;
 
-inline static void
-atomic_bit_set(bitmap_t *map, int n)
+
+inline static bool
+atomic_bit_set(bitmap_t *map, int n, int mem_order)
 {
-	__c11_atomic_fetch_or((_Atomic bitmap_t *)map, BIT(n), __ATOMIC_SEQ_CST);
+	bitmap_t prev;
+	prev = __c11_atomic_fetch_or(map, BIT(n), mem_order);
+	return bit_test(prev, n);
 }
 
-inline static void
-atomic_bit_clear(bitmap_t *map, int n)
+inline static bool
+atomic_bit_clear(bitmap_t *map, int n, int mem_order)
 {
-	__c11_atomic_fetch_and((_Atomic bitmap_t *)map, ~BIT(n), __ATOMIC_SEQ_CST);
+	bitmap_t prev;
+	prev = __c11_atomic_fetch_and(map, ~BIT(n), mem_order);
+	return bit_test(prev, n);
 }
 
 
@@ -179,16 +188,16 @@
 	bit_clear(map[bitmap_index(n)], bitmap_bit(n));
 }
 
-inline static void
-atomic_bitmap_set(bitmap_t *map, uint n)
+inline static bool
+atomic_bitmap_set(bitmap_t *map, uint n, int mem_order)
 {
-	atomic_bit_set(&map[bitmap_index(n)], bitmap_bit(n));
+	return atomic_bit_set(&map[bitmap_index(n)], bitmap_bit(n), mem_order);
 }
 
-inline static void
-atomic_bitmap_clear(bitmap_t *map, uint n)
+inline static bool
+atomic_bitmap_clear(bitmap_t *map, uint n, int mem_order)
 {
-	atomic_bit_clear(&map[bitmap_index(n)], bitmap_bit(n));
+	return atomic_bit_clear(&map[bitmap_index(n)], bitmap_bit(n), mem_order);
 }
 
 inline static bool
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/net/net_kev.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/net/net_kev.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/net/net_kev.h	2016-07-10 08:21:59.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/net/net_kev.h	2016-07-27 03:31:20.000000000 +0200
@@ -29,6 +29,8 @@
 #ifndef _NET_NETKEV_H_
 #define _NET_NETKEV_H_
 
+#if !defined(_POSIX_C_SOURCE) || defined(_DARWIN_C_SOURCE)
+
 /* Kernel event subclass identifiers for KEV_NETWORK_CLASS */
 #define	KEV_INET_SUBCLASS	1 	/* inet subclass */
 /* KEV_INET_SUBCLASS event codes */
@@ -90,4 +92,7 @@
 #define	KEV_INET6_NEW_RTADV_ADDR        5 /* Autoconf address has appeared */
 #define	KEV_INET6_DEFROUTER             6 /* Default router detected */
 
+
+#endif /* (!_POSIX_C_SOURCE || _DARWIN_C_SOURCE) */
+
 #endif /* _NET_NETKEV_H_ */
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/netinet/tcp_var.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/netinet/tcp_var.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/netinet/tcp_var.h	2016-07-10 08:21:56.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/netinet/tcp_var.h	2016-07-27 03:31:16.000000000 +0200
@@ -407,6 +407,8 @@
 	u_int32_t	tcps_mss_to_default;	/* Change MSS to default using link status report */
 	u_int32_t	tcps_mss_to_medium;	/* Change MSS to medium using link status report */
 	u_int32_t	tcps_mss_to_low;	/* Change MSS to low using link status report */
+	u_int32_t	tcps_ecn_fallback_droprst; /* ECN fallback caused by connection drop due to RST */
+	u_int32_t	tcps_ecn_fallback_droprxmt; /* ECN fallback due to drop after multiple retransmits */
 };
 
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_framework.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_framework.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_framework.h	2016-07-10 08:21:47.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_framework.h	2016-07-27 03:31:05.000000000 +0200
@@ -2,7 +2,7 @@
  * Copyright (c) 2007 Apple Inc. All rights reserved.
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
 /*-
@@ -377,7 +377,7 @@
 	    struct socket *so);
 int	mac_socket_check_listen(kauth_cred_t cred, struct socket *so);
 int	mac_socket_check_receive(kauth_cred_t cred, struct socket *so);
-int	mac_socket_check_received(kauth_cred_t cred, struct socket *so, 
+int	mac_socket_check_received(kauth_cred_t cred, struct socket *so,
 	    struct sockaddr *saddr);
 int     mac_socket_check_select(kauth_cred_t cred, struct socket *so,
 	    int which);
@@ -558,11 +558,20 @@
 	    const char *name);
 int	mac_vnode_notify_create(vfs_context_t ctx, struct mount *mp,
 	    struct vnode *dvp, struct vnode *vp, struct componentname *cnp);
-void	mac_vnode_notify_rename(vfs_context_t ctx, struct vnode *vp,
+void	mac_vnode_notify_deleteextattr(vfs_context_t ctx, struct vnode *vp, const char *name);
+void	mac_vnode_notify_link(vfs_context_t ctx, struct vnode *vp,
 	    struct vnode *dvp, struct componentname *cnp);
 void	mac_vnode_notify_open(vfs_context_t ctx, struct vnode *vp, int acc_flags);
-void	mac_vnode_notify_link(vfs_context_t ctx, struct vnode *vp,
-			      struct vnode *dvp, struct componentname *cnp);
+void	mac_vnode_notify_rename(vfs_context_t ctx, struct vnode *vp,
+	    struct vnode *dvp, struct componentname *cnp);
+void	mac_vnode_notify_setacl(vfs_context_t ctx, struct vnode *vp, struct kauth_acl *acl);
+void	mac_vnode_notify_setattrlist(vfs_context_t ctx, struct vnode *vp, struct attrlist *alist);
+void	mac_vnode_notify_setextattr(vfs_context_t ctx, struct vnode *vp, const char *name, struct uio *uio);
+void	mac_vnode_notify_setflags(vfs_context_t ctx, struct vnode *vp, u_long flags);
+void	mac_vnode_notify_setmode(vfs_context_t ctx, struct vnode *vp, mode_t mode);
+void	mac_vnode_notify_setowner(vfs_context_t ctx, struct vnode *vp, uid_t uid, gid_t gid);
+void	mac_vnode_notify_setutimes(vfs_context_t ctx, struct vnode *vp, struct timespec atime, struct timespec mtime);
+void	mac_vnode_notify_truncate(vfs_context_t ctx, kauth_cred_t file_cred, struct vnode *vp);
 int	mac_vnode_find_sigs(struct proc *p, struct vnode *vp, off_t offsetInMacho);
 int	vnode_label(struct mount *mp, struct vnode *dvp, struct vnode *vp,
 	    struct componentname *cnp, int flags, vfs_context_t ctx);
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_policy.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_policy.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_policy.h	2016-07-10 08:21:47.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_policy.h	2016-07-27 03:31:06.000000000 +0200
@@ -5773,6 +5773,158 @@
 );
 
 /**
+  @brief Inform MAC policies that an extended attribute has been removed from a vnode
+  @param cred Subject credential
+  @param vp Object node
+  @param label Policy label for vp
+  @param name Extended attribute name
+
+  Inform MAC policies that an extended attribute has been removed from a vnode.
+*/
+typedef void mpo_vnode_notify_deleteextattr_t(
+	kauth_cred_t cred,
+	struct vnode *vp,
+	struct label *label,
+	const char *name
+);
+
+
+/**
+  @brief Inform MAC policies that an ACL has been set on a vnode
+  @param cred Subject credential
+  @param vp Object node
+  @param label Policy label for vp
+  @param acl ACL structure pointer
+
+  Inform MAC policies that an ACL has been set on a vnode.
+*/
+typedef void mpo_vnode_notify_setacl_t(
+	kauth_cred_t cred,
+	struct vnode *vp,
+	struct label *label,
+	struct kauth_acl *acl
+);
+
+/**
+  @brief Inform MAC policies that an attributes have been set on a vnode
+  @param cred Subject credential
+  @param vp Object vnode
+  @param label Policy label for vp
+  @param alist List of attributes to set
+
+  Inform MAC policies that an attributes have been set on a vnode.
+*/
+typedef void mpo_vnode_notify_setattrlist_t(
+	kauth_cred_t cred,
+	struct vnode *vp,
+	struct label *label,
+	struct attrlist *alist
+);
+
+/**
+  @brief Inform MAC policies that an extended attribute has been set on a vnode
+  @param cred Subject credential
+  @param vp Object vnode
+  @param label Policy label for vp
+  @param name Extended attribute name
+  @param uio I/O structure pointer
+
+  Inform MAC policies that an extended attribute has been set on a vnode.
+*/
+typedef void mpo_vnode_notify_setextattr_t(
+	kauth_cred_t cred,
+	struct vnode *vp,
+	struct label *label,
+	const char *name,
+	struct uio *uio
+);
+
+/**
+  @brief Inform MAC policies that flags have been set on a vnode
+  @param cred Subject credential
+  @param vp Object vnode
+  @param label Policy label for vp
+  @param flags File flags; see chflags(2)
+
+  Inform MAC policies that flags have been set on a vnode.
+*/
+typedef void mpo_vnode_notify_setflags_t(
+	kauth_cred_t cred,
+	struct vnode *vp,
+	struct label *label,
+	u_long flags
+);
+
+/**
+  @brief Inform MAC policies that a new mode has been set on a vnode
+  @param cred Subject credential
+  @param vp Object vnode
+  @param label Policy label for vp
+  @param mode File mode; see chmod(2)
+
+  Inform MAC policies that a new mode has been set on a vnode.
+*/
+typedef void mpo_vnode_notify_setmode_t(
+	kauth_cred_t cred,
+	struct vnode *vp,
+	struct label *label,
+	mode_t mode
+);
+
+/**
+  @brief Inform MAC policies that new uid/gid have been set on a vnode
+  @param cred Subject credential
+  @param vp Object vnode
+  @param label Policy label for vp
+  @param uid User ID
+  @param gid Group ID
+
+  Inform MAC policies that new uid/gid have been set on a vnode.
+*/
+typedef void mpo_vnode_notify_setowner_t(
+	kauth_cred_t cred,
+	struct vnode *vp,
+	struct label *label,
+	uid_t uid,
+	gid_t gid
+);
+
+/**
+  @brief Inform MAC policies that new timestamps have been set on a vnode
+  @param cred Subject credential
+  @param vp Object vnode
+  @param label Policy label for vp
+  @param atime Access time; see utimes(2)
+  @param mtime Modification time; see utimes(2)
+
+  Inform MAC policies that new timestamps have been set on a vnode.
+*/
+typedef void mpo_vnode_notify_setutimes_t(
+	kauth_cred_t cred,
+	struct vnode *vp,
+	struct label *label,
+	struct timespec atime,
+	struct timespec mtime
+);
+
+/**
+  @brief Inform MAC policies that a vnode has been truncated
+  @param cred Subject credential
+  @param file_cred Credential associated with the struct fileproc
+  @param vp Object vnode
+  @param label Policy label for vp
+
+  Inform MAC policies that a vnode has been truncated.
+*/
+typedef void mpo_vnode_notify_truncate_t(
+	kauth_cred_t cred,
+	kauth_cred_t file_cred,
+	struct vnode *vp,
+	struct label *label
+);
+
+
+/**
   @brief Inform MAC policies that a pty slave has been granted
   @param p Responsible process
   @param tp tty data structure
@@ -5911,7 +6063,7 @@
  * Please note that this should be kept in sync with the check assumptions
  * policy in bsd/kern/policy_check.c (policy_ops struct).
  */
-#define MAC_POLICY_OPS_VERSION 43 /* inc when new reserved slots are taken */
+#define MAC_POLICY_OPS_VERSION 44 /* inc when new reserved slots are taken */
 struct mac_policy_ops {
 	mpo_audit_check_postselect_t		*mpo_audit_check_postselect;
 	mpo_audit_check_preselect_t		*mpo_audit_check_preselect;
@@ -5987,14 +6139,14 @@
 	mpo_ipq_label_update_t			*mpo_ipq_label_update;
 
 	mpo_file_check_library_validation_t     *mpo_file_check_library_validation;
-	mpo_reserved_hook_t                     *mpo_reserved2;
-	mpo_reserved_hook_t                     *mpo_reserved3;
-	mpo_reserved_hook_t                     *mpo_reserved4;
-	mpo_reserved_hook_t                     *mpo_reserved5;
-	mpo_reserved_hook_t                     *mpo_reserved6;
-	mpo_reserved_hook_t                     *mpo_reserved7;
-	mpo_reserved_hook_t                     *mpo_reserved8;
-	mpo_reserved_hook_t                     *mpo_reserved9;
+	mpo_vnode_notify_setacl_t               *mpo_vnode_notify_setacl;
+	mpo_vnode_notify_setattrlist_t          *mpo_vnode_notify_setattrlist;
+	mpo_vnode_notify_setextattr_t           *mpo_vnode_notify_setextattr;
+	mpo_vnode_notify_setflags_t             *mpo_vnode_notify_setflags;
+	mpo_vnode_notify_setmode_t              *mpo_vnode_notify_setmode;
+	mpo_vnode_notify_setowner_t             *mpo_vnode_notify_setowner;
+	mpo_vnode_notify_setutimes_t            *mpo_vnode_notify_setutimes;
+	mpo_vnode_notify_truncate_t             *mpo_vnode_notify_truncate;
 
 	mpo_mbuf_label_associate_bpfdesc_t	*mpo_mbuf_label_associate_bpfdesc;
 	mpo_mbuf_label_associate_ifnet_t	*mpo_mbuf_label_associate_ifnet;
@@ -6271,7 +6423,7 @@
 
 	mpo_vnode_check_setacl_t		*mpo_vnode_check_setacl;
 
-	mpo_reserved_hook_t			*mpo_reserved33;
+	mpo_vnode_notify_deleteextattr_t        *mpo_vnode_notify_deleteextattr;
 
 	mpo_system_check_kas_info_t		*mpo_system_check_kas_info;
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h	2016-07-10 08:22:38.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h	2016-07-27 03:31:59.000000000 +0200
@@ -435,15 +435,16 @@
 #define DBG_DLIL_IF_FLT 5       /* DLIL Interface FIlter */
 
 /* The Kernel Debug Sub Classes for File System (DBG_FSYSTEM) */
-#define DBG_FSRW      1       /* reads and writes to the filesystem */
-#define DBG_DKRW      2       /* reads and writes to the disk */
-#define DBG_FSVN      3       /* vnode operations (inc. locking/unlocking) */
-#define DBG_FSLOOOKUP 4       /* namei and other lookup-related operations */
-#define DBG_JOURNAL   5       /* journaling operations */
-#define DBG_IOCTL     6       /* ioctl to the disk */
-#define DBG_BOOTCACHE 7       /* bootcache operations */
-#define DBG_HFS       8       /* HFS-specific events; see the hfs project */
-#define DBG_APFS      0xA     /* APFS-specific events; see the apfs project */
+#define DBG_FSRW      0x1     /* reads and writes to the filesystem */
+#define DBG_DKRW      0x2     /* reads and writes to the disk */
+#define DBG_FSVN      0x3     /* vnode operations (inc. locking/unlocking) */
+#define DBG_FSLOOOKUP 0x4     /* namei and other lookup-related operations */
+#define DBG_JOURNAL   0x5     /* journaling operations */
+#define DBG_IOCTL     0x6     /* ioctl to the disk */
+#define DBG_BOOTCACHE 0x7     /* bootcache operations */
+#define DBG_HFS       0x8     /* HFS-specific events; see the hfs project */
+#define DBG_APFS      0x9     /* APFS-specific events; see the apfs project */
+#define DBG_SMB       0xA     /* SMB-specific events; see the smb project */
 #define DBG_EXFAT     0xE     /* ExFAT-specific events; see the exfat project */
 #define DBG_MSDOS     0xF     /* FAT-specific events; see the msdosfs project */
 #define DBG_ACFS      0x10    /* Xsan-specific events; see the XsanFS project */
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h	2016-07-10 08:22:42.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h	2016-07-27 03:32:03.000000000 +0200
@@ -29,7 +29,7 @@
  * System call switch table.
  *
  * DO NOT EDIT-- this file is automatically generated.
- * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3777.0.0.0.1/bsd/kern/syscalls.master
+ * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3789.1.4.1.1/bsd/kern/syscalls.master
  */
 
 #ifndef _SYS_SYSCALL_H_
@@ -403,7 +403,6 @@
 #define	SYS_kevent         363
 #define	SYS_lchown         364
 			/* 365  old stack_snapshot */
-#define	SYS_stack_snapshot 365
 #define	SYS_bsdthread_register 366
 #define	SYS_workq_open     367
 #define	SYS_workq_kernreturn 368
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h	2016-07-10 08:22:42.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h	2016-07-27 03:32:04.000000000 +0200
@@ -29,7 +29,7 @@
  * System call switch table.
  *
  * DO NOT EDIT-- this file is automatically generated.
- * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3777.0.0.0.1/bsd/kern/syscalls.master
+ * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3789.1.4.1.1/bsd/kern/syscalls.master
  */
 
 #ifndef _SYS_SYSPROTO_H_
@@ -407,6 +407,7 @@
 struct gettimeofday_args {
 	char tp_l_[PADL_(user_addr_t)]; user_addr_t tp; char tp_r_[PADR_(user_addr_t)];
 	char tzp_l_[PADL_(user_addr_t)]; user_addr_t tzp; char tzp_r_[PADR_(user_addr_t)];
+	char mach_absolute_time_l_[PADL_(user_addr_t)]; user_addr_t mach_absolute_time; char mach_absolute_time_r_[PADR_(user_addr_t)];
 };
 struct getrusage_args {
 	char who_l_[PADL_(int)]; int who; char who_r_[PADR_(int)];
@@ -1452,16 +1453,6 @@
 	char owner_l_[PADL_(uid_t)]; uid_t owner; char owner_r_[PADR_(uid_t)];
 	char group_l_[PADL_(gid_t)]; gid_t group; char group_r_[PADR_(gid_t)];
 };
-#if CONFIG_EMBEDDED
-#else
-struct stack_snapshot_args {
-	char pid_l_[PADL_(pid_t)]; pid_t pid; char pid_r_[PADR_(pid_t)];
-	char tracebuf_l_[PADL_(user_addr_t)]; user_addr_t tracebuf; char tracebuf_r_[PADR_(user_addr_t)];
-	char tracebuf_size_l_[PADL_(uint32_t)]; uint32_t tracebuf_size; char tracebuf_size_r_[PADR_(uint32_t)];
-	char flags_l_[PADL_(uint32_t)]; uint32_t flags; char flags_r_[PADR_(uint32_t)];
-	char dispatch_offset_l_[PADL_(uint32_t)]; uint32_t dispatch_offset; char dispatch_offset_r_[PADR_(uint32_t)];
-};
-#endif
 #if CONFIG_WORKQUEUE
 struct bsdthread_register_args {
 	char threadstart_l_[PADL_(user_addr_t)]; user_addr_t threadstart; char threadstart_r_[PADR_(user_addr_t)];
@@ -2585,10 +2576,6 @@
 int kqueue(struct proc *, struct kqueue_args *, int *);
 int kevent(struct proc *, struct kevent_args *, int *);
 int lchown(struct proc *, struct lchown_args *, int *);
-#if CONFIG_EMBEDDED
-#else
-int stack_snapshot(struct proc *, struct stack_snapshot_args *, int *);
-#endif
 #if CONFIG_WORKQUEUE
 int bsdthread_register(struct proc *, struct bsdthread_register_args *, int *);
 int workq_open(struct proc *, struct workq_open_args *, int *);
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/vnode.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/vnode.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/vnode.h	2016-07-10 08:22:41.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/vnode.h	2016-07-27 03:32:02.000000000 +0200
@@ -447,7 +447,8 @@
 #define	VA_UTIMES_NULL		0x010000	/* utimes argument was NULL */
 #define VA_EXCLUSIVE		0x020000	/* exclusive create request */
 #define VA_NOINHERIT		0x040000	/* Don't inherit ACLs from parent */
-#define VA_NOAUTH		0x080000	
+#define VA_NOAUTH		0x080000
+#define VA_64BITOBJIDS		0x100000	/* fileid/linkid/parentid are 64 bit */
 
 /*
  *  Modes.  Some values same as Ixxx entries from inode.h for now.

```