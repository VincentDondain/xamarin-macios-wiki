#IOKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/IOKitLib.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/IOKitLib.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/IOKitLib.h	2016-07-09 07:06:55.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/IOKitLib.h	2016-07-25 06:39:38.000000000 +0200
@@ -391,7 +391,7 @@
     @discussion This is the preferred method of finding IOService objects currently registered by IOKit (that is, objects that have had their registerService() methods invoked). To find IOService objects that aren't yet registered, use an iterator as created by IORegistryEntryCreateIterator(). IOServiceAddMatchingNotification can also supply this information and install a notification of new IOServices. The matching information used in the matching dictionary may vary depending on the class of service being looked up.
     @param masterPort The master port obtained from IOMasterPort(). Pass kIOMasterPortDefault to look up the default master port.
     @param matching A CF dictionary containing matching information, of which one reference is always consumed by this function (Note prior to the Tiger release there was a small chance that the dictionary might not be released if there was an error attempting to serialize the dictionary). IOKitLib can construct matching dictionaries for common criteria with helper functions such as IOServiceMatching, IOServiceNameMatching, IOBSDNameMatching.
-    @param existing An iterator handle is returned on success, and should be released by the caller when the iteration is finished.
+    @param existing An iterator handle, or NULL, is returned on success, and should be released by the caller when the iteration is finished. If NULL is returned, the iteration was successful but found no matching services.
     @result A kern_return_t error code. */
 
 kern_return_t
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDKeys.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDKeys.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDKeys.h	2016-07-10 08:58:23.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDKeys.h	2016-07-27 03:48:35.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDProperties.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDProperties.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDProperties.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDProperties.h	2016-07-27 03:48:35.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDEventSystemClient.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDEventSystemClient.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDEventSystemClient.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDEventSystemClient.h	2016-07-25 06:39:38.000000000 +0200
@@ -0,0 +1,118 @@
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
+#ifndef IOHIDEventSystemClient_h
+#define IOHIDEventSystemClient_h
+
+#include <CoreFoundation/CoreFoundation.h>
+
+__BEGIN_DECLS
+CF_ASSUME_NONNULL_BEGIN
+CF_IMPLICIT_BRIDGING_ENABLED
+
+/*!
+    @header IOHIDEventSystemClient
+    
+    IOHIDEventSystemClient serves as a client that can be used
+    for reading/writing specific properties of the HID event system, as
+    well as getting services of the HID event system. A list of accessible
+    properties can be found in <code>IOKit/hid/IOHIDProperties.h</code>.
+ 
+    @seealso IOKit/hidsystem/IOHIDServiceClient.h
+ */
+
+typedef struct CF_BRIDGED_TYPE(id) __IOHIDEventSystemClient * IOHIDEventSystemClientRef;
+
+/*!
+ * @function    IOHIDEventSystemClientCreateSimpleClient
+ *
+ * @abstract    Creates a client of the HID event system that has to ability to read/write certain
+ *              properties.
+ *
+ * @discussion  Certain properties have the ability to be set/read by clients, see
+ *              <code>IOHIDProperties.h</code> for a list of these properties.
+ *
+ * @param       allocator a custom allocator reference to be used for allocation of the result.
+ *
+ * @result      Returns a <code>IOHIDEventSystemClientRef</code> on success.
+ *              Caller should CFRelease the client when they are finished with it, or keep a
+ *              reference to the client if multiple properties need to be set/read.
+ */
+IOHIDEventSystemClientRef IOHIDEventSystemClientCreateSimpleClient(CFAllocatorRef _Nullable allocator);
+
+/*!
+ * @function    IOHIDEventSystemClientSetProperty
+ *
+ * @abstract    Sets a property on the HID event system.
+ *
+ * @param       client the HID client that created via <code>IOHIDEventSystemClientCreateSimpleClient()</code>.
+ *
+ * @param       key the property key to set. A list of keys can be found in <code>HIDProperties.h</code>.
+ *
+ * @param       property the value to set the property.
+ *
+ * @result      Returns true on success.
+ */
+Boolean IOHIDEventSystemClientSetProperty(IOHIDEventSystemClientRef client, CFStringRef key, CFTypeRef property);
+
+/*!
+ * @function    IOHIDEventSystemClientCopyProperty
+ *
+ * @abstract    Copies a property from the HID event system.
+ *
+ * @param       client the HID client created via <code>IOHIDEventSystemClientCreateSimpleClient()</code>.
+ *
+ * @param       key the property key to copy. A list of keys can be found in <code>HIDProperties.h</code>.
+ *
+ * @result      Returns a CFTypeRef of the property to be copied on success, otherwise NULL.
+ *              Caller is responsible for calling CFRelease on the property.
+ */
+CFTypeRef _Nullable IOHIDEventSystemClientCopyProperty(IOHIDEventSystemClientRef client, CFStringRef key);
+
+/*!
+ * @function    IOHIDEventSystemClientGetTypeID
+ *
+ * @result      Returns the CFTypeID of the <code>IOHIDEventSystemClient</code> class.
+ */
+CFTypeID IOHIDEventSystemClientGetTypeID(void);
+
+/*!
+ * @function    IOHIDEventSystemClientCopyServices
+ *
+ * @abstract    Copies all services available to the client.
+ *
+ * @discussion  Useful for seeing services that are available. Clients can further probe
+ *              the services with the APIs available in <code>IOHIDServiceClient.h</code>.
+ *
+ * @param       client the HID client that created via <code>IOHIDEventSystemClientCreateSimpleClient()</code>.
+ *
+ * @result      On success, returns a CFArrayRef of <code>IOHIDServiceClientRefs</code> that are
+ *              available to the client. Caller is responsible for releasing the array.
+ */
+CFArrayRef _Nullable IOHIDEventSystemClientCopyServices(IOHIDEventSystemClientRef client);
+
+CF_IMPLICIT_BRIDGING_DISABLED
+CF_ASSUME_NONNULL_END
+__END_DECLS
+
+#endif /* IOHIDEventSystemClient_h */
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDLib.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDLib.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDLib.h	2016-05-04 00:21:23.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDLib.h	2016-07-25 06:39:38.000000000 +0200
@@ -72,45 +72,39 @@
 
 extern kern_return_t
 IOHIDGetButtonEventNum( io_connect_t connect,
-	NXMouseButton button, int * eventNum );
+	NXMouseButton button, int * eventNum ) __deprecated;
 
 extern kern_return_t
-IOHIDSetCursorBounds( io_connect_t connect, const IOGBounds * bounds );
+IOHIDGetScrollAcceleration( io_connect_t handle, double * acceleration ) __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12, __IPHONE_NA, __IPHONE_NA);
 
 extern kern_return_t
-IOHIDSetOnScreenCursorBounds( io_connect_t connect, const IOGPoint * point, const IOGBounds * bounds );
+IOHIDSetScrollAcceleration( io_connect_t handle, double acceleration ) __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12, __IPHONE_NA, __IPHONE_NA);
 
 extern kern_return_t
-IOHIDGetScrollAcceleration( io_connect_t handle, double * acceleration );
+IOHIDGetMouseAcceleration( io_connect_t handle, double * acceleration ) __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12, __IPHONE_NA, __IPHONE_NA);
 
 extern kern_return_t
-IOHIDSetScrollAcceleration( io_connect_t handle, double acceleration );
-
-extern kern_return_t
-IOHIDGetMouseAcceleration( io_connect_t handle, double * acceleration );
-
-extern kern_return_t
-IOHIDSetMouseAcceleration( io_connect_t handle, double acceleration );
+IOHIDSetMouseAcceleration( io_connect_t handle, double acceleration ) __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12, __IPHONE_NA, __IPHONE_NA);
 
 extern kern_return_t
 IOHIDGetMouseButtonMode( io_connect_t handle, int * mode );
 
 extern kern_return_t
-IOHIDSetMouseButtonMode( io_connect_t handle, int mode );
+IOHIDSetMouseButtonMode( io_connect_t handle, int mode ) __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12, __IPHONE_NA, __IPHONE_NA);
 
 extern kern_return_t
-IOHIDGetAccelerationWithKey( io_connect_t handle, CFStringRef key, double * acceleration );
+IOHIDGetAccelerationWithKey( io_connect_t handle, CFStringRef key, double * acceleration ) __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12, __IPHONE_NA, __IPHONE_NA);
 
 extern kern_return_t
-IOHIDSetAccelerationWithKey( io_connect_t handle, CFStringRef key, double acceleration );
+IOHIDSetAccelerationWithKey( io_connect_t handle, CFStringRef key, double acceleration ) __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12, __IPHONE_NA, __IPHONE_NA);
 
 extern kern_return_t
 IOHIDGetParameter( io_connect_t handle, CFStringRef key, IOByteCount maxSize, 
-		void * bytes, IOByteCount * actualSize );
+		void * bytes, IOByteCount * actualSize ) __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12, __IPHONE_2_0, __IPHONE_10_0);
 
 extern kern_return_t
 IOHIDSetParameter( io_connect_t handle, CFStringRef key, 
-		const void * bytes, IOByteCount size );
+		const void * bytes, IOByteCount size ) __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12, __IPHONE_NA, __IPHONE_NA);
 
 extern kern_return_t
 IOHIDCopyCFTypeParameter( io_connect_t handle, CFStringRef key,
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDParameter.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDParameter.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDParameter.h	2016-07-10 08:58:23.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDParameter.h	2016-07-27 03:48:35.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDServiceClient.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDServiceClient.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDServiceClient.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDServiceClient.h	2016-07-25 06:39:38.000000000 +0200
@@ -0,0 +1,106 @@
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
+#ifndef IOHIDServiceClient_h
+#define IOHIDServiceClient_h
+
+#include <CoreFoundation/CoreFoundation.h>
+
+__BEGIN_DECLS
+CF_ASSUME_NONNULL_BEGIN
+CF_IMPLICIT_BRIDGING_ENABLED
+
+/*!
+    @header IOHIDServiceClient
+    
+    IOHIDServiceClient serves as a client to the HID event system
+    services. Users are able to copy/set specific properties (defined in
+    <code>IOKit/hid/IOHIDProperties.h</code>), and gather more information
+    about the services available in the HID event system.
+ */
+
+typedef struct CF_BRIDGED_TYPE(id) __IOHIDServiceClient * IOHIDServiceClientRef;
+
+/*!
+ * @function    IOHIDServiceClientSetProperty
+ *
+ * @abstract    Sets a property on the HID service.
+ *
+ * @param       service the HID service to set the property on.
+ *
+ * @param       key the property key to set. A list of keys can be found in <code>HIDProperties.h</code>.
+ *
+ * @param       property the value to set the property.
+ *
+ * @result      Returns true on success.
+ */
+Boolean IOHIDServiceClientSetProperty(IOHIDServiceClientRef service, CFStringRef key, CFTypeRef property);
+
+/*!
+ * @function    IOHIDServiceClientCopyProperty
+ *
+ * @abstract    Copies a property from the HID service.
+ *
+ * @param       service the HID service to copy the property from.
+ *
+ * @param       key the property key to copy. A list of keys can be found in <code>HIDProperties.h</code>.
+ *
+ * @result      Returns a CFTypeRef of the property to be copied on success, otherwise NULL.
+ *              Caller is responsible for calling CFRelease on the property.
+ */
+CFTypeRef _Nullable IOHIDServiceClientCopyProperty(IOHIDServiceClientRef service, CFStringRef key);
+
+/*!
+ * @function    IOHIDServiceClientGetTypeID
+ *
+ * @result      Returns the CFTypeID of the <code>IOHIDServiceClient</code> class.
+ */
+CFTypeID IOHIDServiceClientGetTypeID(void);
+
+/*!
+ * @function    IOHIDServiceClientGetRegistryID
+ *
+ * @param       service the HID service to get the registry ID for.
+ *
+ * @result      Returns a CFTypeRef containing the registry ID for the service.
+ */
+CFTypeRef IOHIDServiceClientGetRegistryID(IOHIDServiceClientRef service);
+
+/*!
+ * @function    IOHIDServiceClientConformsTo
+ *
+ * @abstract    Determines if a HID service conforms to a specific usage page and usage.
+ *
+ * @param       usagePage A usage page defined in <code>IOHIDUsageTables.h</code>.
+ *
+ * @param       usage A usage defined in <code>IOHIDUsageTables.h</code>.
+ *
+ * @result      Returns true if the service conforms to the provided usage page and usage.
+ */
+boolean_t IOHIDServiceClientConformsTo(IOHIDServiceClientRef service, uint32_t usagePage, uint32_t usage);
+
+CF_IMPLICIT_BRIDGING_DISABLED
+CF_ASSUME_NONNULL_END
+__END_DECLS
+
+#endif /* IOHIDServiceClient_h */
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/event_status_driver.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/event_status_driver.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/event_status_driver.h	2016-07-09 07:06:55.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/event_status_driver.h	2016-07-25 06:39:38.000000000 +0200
@@ -41,6 +41,7 @@
 #include <IOKit/hidsystem/IOLLEvent.h>
 #include <IOKit/hidsystem/IOHIDTypes.h>
 #include <AvailabilityMacros.h> 
+#include <IOKit/IOKitLib.h>
 
 /*
  * Event System Handle:
@@ -52,27 +53,27 @@
 typedef mach_port_t NXEventHandle;
 
 /* Open and Close */
-NXEventHandle NXOpenEventStatus(void);
-void NXCloseEventStatus(NXEventHandle handle);
+NXEventHandle NXOpenEventStatus(void) __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12, __IPHONE_NA, __IPHONE_NA);
+void NXCloseEventStatus(NXEventHandle handle) __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12, __IPHONE_NA, __IPHONE_NA);
 
 /* Status */
 extern NXEventSystemInfoType NXEventSystemInfo(NXEventHandle handle,
 				char *flavor,
 				int *evs_info,
-				unsigned int *evs_info_cnt);
+				unsigned int *evs_info_cnt) __deprecated;
 /* Keyboard */
-extern void NXSetKeyRepeatInterval(NXEventHandle handle, double seconds);
-extern double NXKeyRepeatInterval(NXEventHandle handle);
-extern void NXSetKeyRepeatThreshold(NXEventHandle handle, double threshold);
-extern double NXKeyRepeatThreshold(NXEventHandle handle);
-extern void NXResetKeyboard(NXEventHandle handle);
+extern void NXSetKeyRepeatInterval(NXEventHandle handle, double seconds) __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12, __IPHONE_NA, __IPHONE_NA);
+extern double NXKeyRepeatInterval(NXEventHandle handle) __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12, __IPHONE_NA, __IPHONE_NA);
+extern void NXSetKeyRepeatThreshold(NXEventHandle handle, double threshold) __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12, __IPHONE_NA, __IPHONE_NA);
+extern double NXKeyRepeatThreshold(NXEventHandle handle) __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12, __IPHONE_NA, __IPHONE_NA);
+extern void NXResetKeyboard(NXEventHandle handle) __deprecated;
 
 /* Mouse */
-extern void NXSetClickTime(NXEventHandle handle, double seconds);
-extern double NXClickTime(NXEventHandle handle);
-extern void NXSetClickSpace(NXEventHandle handle, _NXSize_ *area);
-extern void NXGetClickSpace(NXEventHandle handle, _NXSize_ *area);
-extern void NXResetMouse(NXEventHandle handle);
+extern void NXSetClickTime(NXEventHandle handle, double seconds)__OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12, __IPHONE_NA, __IPHONE_NA);
+extern double NXClickTime(NXEventHandle handle) __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12, __IPHONE_NA, __IPHONE_NA);
+extern void NXSetClickSpace(NXEventHandle handle, _NXSize_ *area) __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12, __IPHONE_NA, __IPHONE_NA);
+extern void NXGetClickSpace(NXEventHandle handle, _NXSize_ *area) __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_0, __MAC_10_12, __IPHONE_NA, __IPHONE_NA);
+extern void NXResetMouse(NXEventHandle handle) __deprecated;
 
 /*
 * The following functions have been removed.

```