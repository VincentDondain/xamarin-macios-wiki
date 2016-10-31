#IOBluetooth.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/BluetoothAssignedNumbers.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/BluetoothAssignedNumbers.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/BluetoothAssignedNumbers.h	2016-10-08 04:49:44.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOBluetooth.framework/Headers/BluetoothAssignedNumbers.h	2016-10-24 00:26:16.000000000 +0200
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

```