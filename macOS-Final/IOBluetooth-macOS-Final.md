#IOBluetooth.framework

``` diff
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/Bluetooth.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/Bluetooth.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/Bluetooth.h	2016-08-17 21:39:57.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/Bluetooth.h	2016-10-07 22:35:28.000000000 -0400
@@ -365,7 +365,8 @@
 	kBluetoothL2CAPChannelReservedStart			= 0x0007,
     kBluetoothL2CAPChannelLEAP					= 0x002A,
     kBluetoothL2CAPChannelLEAS					= 0x002B,
-	kBluetoothL2CAPChannelMagnet				= 0x003A, // Magnet
+    kBluetoothL2CAPChannelMagicPairing			= 0x0030,
+	kBluetoothL2CAPChannelMagnet				= 0x003A,
     kBluetoothL2CAPChannelReservedEnd			= 0x003F,
     
     // Range 0x0040 to 0xFFFF are dynamically allocated.
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/BluetoothAssignedNumbers.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/BluetoothAssignedNumbers.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/BluetoothAssignedNumbers.h	2016-08-17 21:39:57.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/BluetoothAssignedNumbers.h	2016-10-07 22:49:44.000000000 -0400
@@ -649,6 +649,9 @@
     kBluetoothHCIExtendedInquiryResponseDataTypeServiceData128BitUUID						=	0x21,
     kBluetoothHCIExtendedInquiryResponseDataTypeSecureConnectionsConfirmationValue			=	0x22,
     kBluetoothHCIExtendedInquiryResponseDataTypeSecureConnectionsRandomValue				=	0x23,
+    kBluetoothHCIExtendedInquiryResponseDataTypeURI											=	0x24,
+    kBluetoothHCIExtendedInquiryResponseDataTypeIndoorPositioning							=	0x25,
+    kBluetoothHCIExtendedInquiryResponseDataTypeTransportDiscoveryData						=	0x26,
     kBluetoothHCIExtendedInquiryResponseDataType3DInformationData							=	0x3D,
 	kBluetoothHCIExtendedInquiryResponseDataTypeManufacturerSpecificData					=	0xFF
 };

```