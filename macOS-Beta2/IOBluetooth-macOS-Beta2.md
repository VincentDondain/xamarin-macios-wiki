#IOBluetooth.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/Bluetooth.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/Bluetooth.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/Bluetooth.h	2016-06-07 01:24:20.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/Bluetooth.h	2016-06-29 00:57:40.000000000 +0200
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
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/objc/IOBluetoothHandsFreeAudioGateway.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/objc/IOBluetoothHandsFreeAudioGateway.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/objc/IOBluetoothHandsFreeAudioGateway.h	2016-06-07 01:20:44.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/objc/IOBluetoothHandsFreeAudioGateway.h	2016-06-29 00:57:40.000000000 +0200
@@ -16,7 +16,6 @@
 @interface IOBluetoothHandsFreeAudioGateway : IOBluetoothHandsFree {
 	BOOL				_indicatorMode;
 	BOOL				_indicatorEventReporting;
-	BOOL				_isSiriActive;
     IOBluetoothHandsFreeAudioGatewayExpansion *	_expansion;
 }
 
@@ -94,4 +93,4 @@
  */
 - (void)handsFree:(IOBluetoothHandsFreeAudioGateway *)device redial:(NSNumber *)redial NS_AVAILABLE_MAC(10_7);
 
-@end
\ No newline at end of file
+@end

```