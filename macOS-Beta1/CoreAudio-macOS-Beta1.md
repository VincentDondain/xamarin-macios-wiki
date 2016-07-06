#CoreAudio.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreAudio.framework/Headers/AudioHardware.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreAudio.framework/Headers/AudioHardware.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreAudio.framework/Headers/AudioHardware.h	2015-08-23 01:13:26.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreAudio.framework/Headers/AudioHardware.h	2016-05-14 06:00:35.000000000 +0200
@@ -520,6 +520,16 @@
                         property's data. Note that an error is not returned if the UID doesn't refer
                         to any AudioBoxes. Rather, this property will return kAudioObjectUnknown
                         as the value of the property.
+    @constant       kAudioHardwarePropertyClockDeviceList
+                        An array of AudioObjectIDs that represent all the AudioClockDevice objects 
+                        currently provided by the system.
+    @constant       kAudioHardwarePropertyTranslateUIDToClockDevice
+                        This property fetches the AudioObjectID that corresponds to the AudioClockDevice
+                        that has the given UID. The UID is passed in via the qualifier as a CFString
+                        while the AudioObjectID for the AudioClockDevice is returned to the caller
+                        as the property's data. Note that an error is not returned if the UID doesn't
+                        refer to any AudioClockDevice. Rather, this property will return 
+                        kAudioObjectUnknown as the value of the property.
     @constant       kAudioHardwarePropertyProcessIsMaster
                         A UInt32 where 1 means that the current process contains the master instance
                         of the HAL. The master instance of the HAL is the only instance in which
@@ -584,6 +594,8 @@
     kAudioHardwarePropertyTranslateBundleIDToTransportManager   = 'tmbi',
     kAudioHardwarePropertyBoxList                               = 'box#',
     kAudioHardwarePropertyTranslateUIDToBox                     = 'uidb',
+    kAudioHardwarePropertyClockDeviceList                       = 'clk#',
+    kAudioHardwarePropertyTranslateUIDToClockDevice             = 'uidc',
     kAudioHardwarePropertyProcessIsMaster                       = 'mast',
     kAudioHardwarePropertyIsInitingOrExiting                    = 'inot',
     kAudioHardwarePropertyUserIDChanged                         = 'euid',
@@ -940,6 +952,10 @@
     @constant       kAudioDevicePropertyActualSampleRate
                         A Float64 that indicates the current actual sample rate of the AudioDevice
                         as measured by its time stamps.
+    @constant       kAudioDevicePropertyClockDevice
+                        A CFString that contains the UID for the AudioClockDevice that is currently
+                        serving as the master time base of the device. The caller is responsible
+                        for releasing the returned CFObject.
 */
 CF_ENUM(AudioObjectPropertySelector)
 {
@@ -955,7 +971,8 @@
     kAudioDevicePropertyIOCycleUsage                    = 'ncyc',
     kAudioDevicePropertyStreamConfiguration             = 'slay',
     kAudioDevicePropertyIOProcStreamUsage               = 'suse',
-    kAudioDevicePropertyActualSampleRate                = 'asrt'
+    kAudioDevicePropertyActualSampleRate                = 'asrt',
+	kAudioDevicePropertyClockDevice						= 'apcd'
 };
 
 /*!
@@ -1514,6 +1531,16 @@
 #define kAudioAggregateDeviceMasterSubDeviceKey "master"
 
 /*!
+    @defined        kAudioAggregateDeviceClockDeviceKey
+    @discussion     The key used in a CFDictionary that describes the composition of an
+                    AudioAggregateDevice. The value for this key is a CFString that contains the
+                    UID for the clock device that is the master time source for the
+                    AudioAggregateDevice. If the aggregate device includes both a master audio
+                    device and a clock device, the clock device will control the master time base.
+*/
+#define kAudioAggregateDeviceClockDeviceKey "clock"
+
+/*!
     @defined        kAudioAggregateDeviceIsPrivateKey
     @discussion     The key used in a CFDictionary that describes the composition of an
                     AudioAggregateDevice. The value for this key is a CFNumber where a value of 0
@@ -1560,13 +1587,21 @@
                         A CFString that contains the UID for the AudioDevice that is currently
                         serving as the master time base of the aggregate device. The caller is
                         responsible for releasing the returned CFObject.
+    @constant       kAudioAggregateDevicePropertyClockDevice
+                        A CFString that contains the UID for the AudioClockDevice that is currently
+                        serving as the master time base of the aggregate device. If the aggregate
+                        device includes both a master audio device and a clock device, the clock
+                        device will control the master time base. Setting this property will enable
+                        drift correction for all subdevices in the aggregate device. The caller is
+                        responsible for releasing the returned CFObject.
 */
 CF_ENUM(AudioObjectPropertySelector)
 {
     kAudioAggregateDevicePropertyFullSubDeviceList      = 'grup',
     kAudioAggregateDevicePropertyActiveSubDeviceList    = 'agrp',
     kAudioAggregateDevicePropertyComposition            = 'acom',
-    kAudioAggregateDevicePropertyMasterSubDevice        = 'amst'
+    kAudioAggregateDevicePropertyMasterSubDevice        = 'amst',
+    kAudioAggregateDevicePropertyClockDevice            = 'apcd'
 };
 
 //==================================================================================================
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreAudio.framework/Headers/AudioHardwareBase.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreAudio.framework/Headers/AudioHardwareBase.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreAudio.framework/Headers/AudioHardwareBase.h	2015-08-23 01:13:26.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreAudio.framework/Headers/AudioHardwareBase.h	2016-05-14 06:00:35.000000000 +0200
@@ -383,14 +383,26 @@
                         property's data. Note that an error is not returned if the UID doesn't refer
                         to any AudioBoxes. Rather, this property will return kAudioObjectUnknown
                         as the value of the property.
+    @constant       kAudioPlugInPropertyClockDeviceList
+                        An array of AudioObjectIDs that represent all the AudioClockDevice objects
+                        currently provided by the plug-in.
+    @constant       kAudioPlugInPropertyTranslateUIDToClockDevice
+                        This property fetches the AudioObjectID that corresponds to the 
+                        AudioClockDevice that has the given UID. The UID is passed in via the 
+                        qualifier as a CFString while the AudioObjectID for the AudioClockDevice is 
+                        returned to the caller as the property's data. Note that an error is not 
+                        returned if the UID doesn't refer to any AudioClockDevices. Rather, this 
+                        property will return kAudioObjectUnknown as the value of the property.
 */
 CF_ENUM(AudioObjectPropertySelector)
 {
-    kAudioPlugInPropertyBundleID                = 'piid',
-    kAudioPlugInPropertyDeviceList              = 'dev#',
-    kAudioPlugInPropertyTranslateUIDToDevice    = 'uidd',
-    kAudioPlugInPropertyBoxList                 = 'box#',
-    kAudioPlugInPropertyTranslateUIDToBox       = 'uidb'
+    kAudioPlugInPropertyBundleID                  = 'piid',
+    kAudioPlugInPropertyDeviceList                = 'dev#',
+    kAudioPlugInPropertyTranslateUIDToDevice      = 'uidd',
+    kAudioPlugInPropertyBoxList                   = 'box#',
+    kAudioPlugInPropertyTranslateUIDToBox         = 'uidb',
+    kAudioPlugInPropertyClockDeviceList           = 'clk#',
+    kAudioPlugInPropertyTranslateUIDToClockDevice = 'uidc'
 };
 
 //==================================================================================================
@@ -503,6 +515,10 @@
                         An array of AudioObjectIDs that represent all the AudioDevice objects that
                         came out of the given AudioBox. Note that until a box is enabled, this list
                         will be empty.
+    @constant       kAudioBoxPropertyClockDeviceList
+                        An array of AudioObjectIDs that represent all the AudioClockDevice objects
+                        that came out of the given AudioBox. Note that until a box is enabled, this 
+                        list will be empty.
 */
 CF_ENUM(AudioObjectPropertySelector)
 {
@@ -514,7 +530,8 @@
     kAudioBoxPropertyIsProtected        = 'bpro',
     kAudioBoxPropertyAcquired           = 'bxon',
     kAudioBoxPropertyAcquisitionFailed  = 'bxof',
-    kAudioBoxPropertyDeviceList         = 'bdv#'
+    kAudioBoxPropertyDeviceList         = 'bdv#',
+    kAudioBoxPropertyClockDeviceList    = 'bcl#'
 };
 
 //==================================================================================================
@@ -716,6 +733,81 @@
 
 //==================================================================================================
 #pragma mark -
+#pragma mark AudioClockDevice Constants
+    
+/*!
+    @enum           AudioClockDevice Class Constants
+    @abstract       Various constants related to the AudioClockDevice class.
+    @constant       kAudioClockDeviceClassID
+                        The AudioClassID that identifies the AudioClockDevice class.
+*/
+CF_ENUM(AudioObjectPropertySelector)
+{
+    kAudioClockDeviceClassID    = 'aclk'
+};
+    
+    //==================================================================================================
+#pragma mark AudioClockDevice Properties
+    
+/*!
+    @enum           AudioClockDevice Properties
+    @abstract       AudioObjectPropertySelector values provided by the AudioClockDevice class.
+    @discussion     The AudioClockDevice class is a subclass of the AudioObject class. The class has just
+                    the global scope, kAudioObjectPropertyScopeGlobal, and only a master element.
+    @constant       kAudioClockDevicePropertyDeviceUID
+                        A CFString that contains a persistent identifier for the AudioClockDevice.
+                        An AudioClockDevice's UID is persistent across boots. The content of the UID
+                        string is a black box and may contain information that is unique to a
+                        particular instance of an clock's hardware or unique to the CPU. Therefore
+                        they are not suitable for passing between CPUs or for identifying similar
+                        models of hardware. The caller is responsible for releasing the returned
+                        CFObject.
+    @constant       kAudioClockDevicePropertyTransportType
+                        A UInt32 whose value indicates how the AudioClockDevice is connected to the
+                        CPU. Constants for some of the values for this property can be found in the
+                        enum in the AudioDevice Constants section of this file.
+    @constant       kAudioClockDevicePropertyClockDomain
+                        A UInt32 whose value indicates the clock domain to which this
+                        AudioClockDevice belongs. AudioClockDevices and AudioDevices that have the
+                        same value for this property are able to be synchronized in hardware.
+                        However, a value of 0 indicates that the clock domain for the device is
+                        unspecified and should be assumed to be separate from every other device's
+                        clock domain, even if they have the value of 0 as their clock domain as well.
+    @constant       kAudioClockDevicePropertyDeviceIsAlive
+                        A UInt32 where a value of 1 means the device is ready and available and 0
+                        means the device is usable and will most likely go away shortly.
+    @constant       kAudioClockDevicePropertyDeviceIsRunning
+                        A UInt32 where a value of 0 means the AudioClockDevice is not providing
+                        times and a value of 1 means that it is. Note that the notification for this
+                        property is usually sent from the AudioClockDevice's IO thread.
+    @constant       kAudioClockDevicePropertyLatency
+                        A UInt32 containing the number of frames of latency in the AudioClockDevice.
+    @constant       kAudioClockDevicePropertyControlList
+                        An array of AudioObjectIDs that represent the AudioControls of the
+                        AudioClockDevice. Note that if a notification is received for this property,
+                        any cached AudioObjectIDs for the device become invalid and need to be
+                        re-fetched.
+    @constant       kAudioClockDevicePropertyNominalSampleRate
+                        A Float64 that indicates the current nominal sample rate of the
+                        AudioClockDevice.
+    @constant       kAudioClockDevicePropertyAvailableNominalSampleRates
+                        An array of AudioValueRange structs that indicates the valid ranges for the
+                        nominal sample rate of the AudioClockDevice.
+*/
+CF_ENUM(AudioObjectPropertySelector)
+{
+    kAudioClockDevicePropertyDeviceUID                   = 'cuid',
+    kAudioClockDevicePropertyTransportType               = 'tran',
+    kAudioClockDevicePropertyClockDomain                 = 'clkd',
+    kAudioClockDevicePropertyDeviceIsAlive               = 'livn',
+    kAudioClockDevicePropertyDeviceIsRunning             = 'goin',
+    kAudioClockDevicePropertyLatency                     = 'ltnc',
+    kAudioClockDevicePropertyControlList                 = 'ctrl',
+    kAudioClockDevicePropertyNominalSampleRate           = 'nsrt',
+    kAudioClockDevicePropertyAvailableNominalSampleRates = 'nsr#'
+};
+//==================================================================================================
+#pragma mark -
 #pragma mark AudioEndPointDevice Constants
 
 /*!
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreAudio.framework/Headers/AudioServerPlugIn.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreAudio.framework/Headers/AudioServerPlugIn.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreAudio.framework/Headers/AudioServerPlugIn.h	2015-08-23 01:13:26.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreAudio.framework/Headers/AudioServerPlugIn.h	2016-05-14 06:00:35.000000000 +0200
@@ -27,9 +27,9 @@
     An AudioServerPlugIn can provide the host with information that describes the conditions that
     must be met to load the plug-in. This is done through plug-in bundle's info.plist in a key named
     "AudioServerPlugIn_LoadingConditions". The value of this key is a dictionary whose keys describe
-    the loading conditions for the plug-in. Currently, only the key named "IOService Matching" whose
-    value is an array of matching dictionaries. The host will load the plug-in if any of these
-    matching dictionaries match an IOService.
+    the loading conditions for the plug-in. Currently, the only defined key is named
+    "IOService Matching" whose value is an array of IOService matching dictionaries. The host will
+	load the plug-in if any of these matching dictionaries match an IOService.
     
     An AudioServerPlugIn operates in a limited environment. First and foremost, an AudioServerPlugIn
     may not make any calls to the client HAL API in the CoreAudio.framework. This will result in
@@ -58,7 +58,7 @@
     
     An AudioServerPlugIn provides the same property-based object model as the HAL's client
     framework. The basic objects and properties are defined in <CoreAudio/AudioHardwareBase.h> and
-    are supplemented with properties decleared here. The plug-in is responsible for defining the
+    are supplemented with properties declared here. The plug-in is responsible for defining the
     AudioObjectIDs to be used as handles for the AudioObjects the plug-in provides. However, the
     AudioObjectID for the one and only AudioPlugIn object must be kAudioObjectPlugInObject.
     
@@ -145,11 +145,11 @@
     @field          mSelector
                         The AudioObjectPropertySelector of the custom property.
     @field          mPropertyDataType
-                        A UInt32 whose value inidicates the data type of the data of the custom
+                        A UInt32 whose value indicates the data type of the data of the custom
                         property. Constants for this value are defined in the Basic Constants
                         section.
     @field          mQualifierDataType
-                        A UInt32 whose value inidicates the data type of the data of the custom
+                        A UInt32 whose value indicates the data type of the data of the custom
                         property. Constants for this value are defined in the Basic Constants
                         section.
 */
@@ -198,7 +198,7 @@
                         whenever the IO thread resynchronizes with the hardware.
     @field          mNominalIOBufferFrameSize
                         The number of sample frames that will nominally be read/written in the new
-                        IO cycle. Note that the actual IO bufers that get read/written might be a
+                        IO cycle. Note that the actual IO buffers that get read/written might be a
                         different size depending on whether or not any drift compensation is being
                         applied by the Host.
     @field          mInputTime
@@ -262,7 +262,7 @@
 
 /*!
     @enum           Custom Property Data Types
-    @abstract       The set of data types the Host knows how to marshall between the server and the
+    @abstract       The set of data types the Host knows how to marshal between the server and the
                     client. These are the only types supported for custom properties. See
                     AudioServerPlugInCustomPropertyInfo for more information.
     @constant       kAudioServerPlugInCustomPropertyDataTypeNone
@@ -294,7 +294,7 @@
                         This operation transfers the input data from the device's ring buffer to the
                         provided buffer in the stream's native format. Note that this operation
                         always happens in-place in the main buffer passed to DoIOOperation(). It is
-                        required that this operation be implmemented if the AudioDevice has input
+                        required that this operation be implemented if the AudioDevice has input
                         streams.
     @constant       kAudioServerPlugInIOOperationConvertInput
                         This operation converts the input data from its native format to the
@@ -474,7 +474,7 @@
         @param          inKey
                             A CFStringRef that contains the name of the key whose data is to be
                             fetched. Note that the Host will make sure that the keys for one plug-in
-                            do not collide with the keys for othe plug-ins.
+                            do not collide with the keys for other plug-ins.
         @param          outData
                             The data associated with the named storage key in the form of
                             CFPropertyList. The caller is responsible for releasing the returned
@@ -497,7 +497,7 @@
         @param          inKey
                             A CFStringRef that contains the name of the key whose data is to be
                             written. Note that the Host will make sure that the keys for one plug-in
-                            do not collide with the keys for othe plug-ins.
+                            do not collide with the keys for other plug-ins.
         @param          inData
                             A CFPropertyListRef containing the data to associate with the key.
         @result         An OSStatus indicating success or failure.
@@ -515,7 +515,7 @@
         @param          inKey
                             A CFStringRef that contains the name of the key to be deleted. Note that
                             the Host will make sure that the keys for one plug-in do not collide
-                            with the keys for othe plug-ins.
+                            with the keys for other plug-ins.
         @result         An OSStatus indicating success or failure.
     */
     OSStatus
@@ -534,7 +534,7 @@
                         the Host gives the device clearance to do so by invoking the plug-in's
                         PerformDeviceConfigurationChange() routine. Note that the call to
                         PerformDeviceConfigurationChange() may be deferred to another thread at the
-                        descretion of the host.
+                        discretion of the host.
                         The sorts of changes that must go through this mechanism are anything that
                         affects either the structure of the device or IO. This includes, but is not
                         limited to, changing stream layout, adding/removing controls, changing the
@@ -632,7 +632,7 @@
                             The plug-in to initialize.
         @param          inHost
                             An AudioServerPlugInHostInterface struct that the plug-in is to use for
-                            communication with the Host. The Host guarantees that the strorage
+                            communication with the Host. The Host guarantees that the storage
                             pointed to by inHost will remain valid for the lifetime of the plug-in.
         @result         An OSStatus indicating success or failure.
     */
@@ -1001,7 +1001,7 @@
         @abstract       Asks the plug-in whether or not the device will perform the given phase of
                         the IO cycle for a particular device.
         @discussion     As part of starting IO, the Host will ask the plug-in whether or not the
-                        device in question will perform the givne IO operation. This method is not
+                        device in question will perform the given IO operation. This method is not
                         called during the IO cycle. A device is allowed to do different sets of
                         operations for different clients.
         @param          inDriver
@@ -1064,7 +1064,7 @@
 
     /*!
         @method         DoIOOperation
-        @abstract       Tells the device to perfrom an IO operation for a particular stream.
+        @abstract       Tells the device to perform an IO operation for a particular stream.
         @param          inDriver
                             The plug-in that owns the device.
         @param          inDeviceObjectID
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreAudio.framework/Headers/CoreAudioTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreAudio.framework/Headers/CoreAudioTypes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreAudio.framework/Headers/CoreAudioTypes.h	2015-08-23 01:13:26.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreAudio.framework/Headers/CoreAudioTypes.h	2016-05-27 06:51:23.000000000 +0200
@@ -177,12 +177,11 @@
     UInt32      mNumberBuffers;
     AudioBuffer mBuffers[1]; // this is a variable length array of mNumberBuffers elements
     
-#if defined(__cplusplus) && CA_STRICT
+#if defined(__cplusplus) && defined(CA_STRICT) && CA_STRICT
 public:
     AudioBufferList() {}
 private:
-    //  Copying and assigning a variable length struct is problematic so turn their use into a
-    //  compile time error for eacy spotting.
+    //  Copying and assigning a variable length struct is problematic; generate a compile error.
     AudioBufferList(const AudioBufferList&);
     AudioBufferList&    operator=(const AudioBufferList&);
 #endif
@@ -1309,7 +1308,7 @@
     AudioChannelLayout() {}
 private:
     //  Copying and assigning a variable length struct is problematic so turn their use into a
-    //  compile time error for eacy spotting.
+    //  compile time error for easy spotting.
     AudioChannelLayout(const AudioChannelLayout&);
     AudioChannelLayout&         operator=(const AudioChannelLayout&);
 #endif

```