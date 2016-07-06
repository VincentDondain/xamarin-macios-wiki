#CoreBluetooth.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBCentralManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBCentralManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBCentralManager.h	2015-09-30 20:41:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBCentralManager.h	2016-05-14 16:36:55.000000000 +0200
@@ -11,9 +11,10 @@
 #warning Please do not import this header file directly. Use <CoreBluetooth/CoreBluetooth.h> instead.
 #endif
 
-#import <CoreBluetooth/CBDefines.h>
 #import <CoreBluetooth/CBAdvertisementData.h>
 #import <CoreBluetooth/CBCentralManagerConstants.h>
+#import <CoreBluetooth/CBDefines.h>
+#import <CoreBluetooth/CBManager.h>
 #import <Foundation/Foundation.h>
 
 NS_ASSUME_NONNULL_BEGIN
@@ -32,13 +33,13 @@
  *
  */
 typedef NS_ENUM(NSInteger, CBCentralManagerState) {
-	CBCentralManagerStateUnknown = 0,
-	CBCentralManagerStateResetting,
-	CBCentralManagerStateUnsupported,
-	CBCentralManagerStateUnauthorized,
-	CBCentralManagerStatePoweredOff,
-	CBCentralManagerStatePoweredOn,
-};
+	CBCentralManagerStateUnknown = CBManagerStateUnknown,
+	CBCentralManagerStateResetting = CBManagerStateResetting,
+	CBCentralManagerStateUnsupported = CBManagerStateUnsupported,
+	CBCentralManagerStateUnauthorized = CBManagerStateUnauthorized,
+	CBCentralManagerStatePoweredOff = CBManagerStatePoweredOff,
+	CBCentralManagerStatePoweredOn = CBManagerStatePoweredOn,
+} NS_DEPRECATED(NA, NA, 5_0, 10_0, "Use CBManagerState instead");
 
 @protocol CBCentralManagerDelegate;
 @class CBUUID, CBPeripheral;
@@ -50,7 +51,7 @@
  *
  */
 NS_CLASS_AVAILABLE(10_7, 5_0)
-CB_EXTERN_CLASS @interface CBCentralManager : NSObject
+CB_EXTERN_CLASS @interface CBCentralManager : CBManager
 
 /*!
  *  @property delegate
@@ -58,16 +59,7 @@
  *  @discussion The delegate object that will receive central events.
  *
  */
-@property(assign, nonatomic, nullable) id<CBCentralManagerDelegate> delegate;
-
-/*!
- *  @property state
- *
- *  @discussion The current state of the central, initially set to <code>CBCentralManagerStateUnknown</code>. Updates are provided by required
- *              delegate method {@link centralManagerDidUpdateState:}.
- *
- */
-@property(readonly) CBCentralManagerState state;
+@property(nonatomic, weak, nullable) id<CBCentralManagerDelegate> delegate;
 
 /*!
  *  @property isAdvertising
@@ -75,7 +67,9 @@
  *  @discussion Whether or not the central is currently scanning.
  *
  */
-@property(readonly) BOOL isScanning NS_AVAILABLE(NA, 9_0);
+@property(nonatomic, assign, readonly) BOOL isScanning NS_AVAILABLE(NA, 9_0);
+
+- (instancetype)init;
 
 /*!
  *  @method initWithDelegate:queue:
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBManager.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBManager.h	2016-05-18 03:28:17.000000000 +0200
@@ -0,0 +1,49 @@
+/*
+ *	@file CBManager.h
+ *	@framework CoreBluetooth
+ *
+ *  @discussion Entry point to the central role.
+ *
+ *	@copyright 2016 Apple, Inc. All rights reserved.
+ */
+
+#import <CoreBluetooth/CBDefines.h>
+#import <Foundation/Foundation.h>
+
+NS_CLASS_AVAILABLE(N_A, 10_0)
+CB_EXTERN_CLASS @interface CBManager : NSObject
+
+- (instancetype)init NS_UNAVAILABLE;
+
+/*!
+ *  @enum CBManagerState
+ *
+ *  @discussion Represents the current state of a CBManager.
+ *
+ *  @constant CBManagerStateUnknown       State unknown, update imminent.
+ *  @constant CBManagerStateResetting     The connection with the system service was momentarily lost, update imminent.
+ *  @constant CBManagerStateUnsupported   The platform doesn't support the Bluetooth Low Energy Central/Client role.
+ *  @constant CBManagerStateUnauthorized  The application is not authorized to use the Bluetooth Low Energy role.
+ *  @constant CBManagerStatePoweredOff    Bluetooth is currently powered off.
+ *  @constant CBManagerStatePoweredOn     Bluetooth is currently powered on and available to use.
+ *
+ */
+typedef NS_ENUM(NSInteger, CBManagerState) {
+	CBManagerStateUnknown = 0,
+	CBManagerStateResetting,
+	CBManagerStateUnsupported,
+	CBManagerStateUnauthorized,
+	CBManagerStatePoweredOff,
+	CBManagerStatePoweredOn,
+} NS_ENUM_AVAILABLE(NA, 10_0);
+
+/*!
+ *  @property state
+ *
+ *  @discussion The current state of the manager, initially set to <code>CBManagerStateUnknown</code>.
+ *				Updates are provided by required delegate method {@link managerDidUpdateState:}.
+ *
+ */
+@property(nonatomic, assign, readonly) CBManagerState state;
+
+@end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBPeripheral.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBPeripheral.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBPeripheral.h	2015-09-30 20:41:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBPeripheral.h	2016-05-18 02:19:37.000000000 +0200
@@ -58,7 +58,7 @@
  *
  *  @discussion The delegate object that will receive peripheral events.
  */
-@property(assign, nonatomic, nullable) id<CBPeripheralDelegate> delegate;
+@property(weak, nonatomic, nullable) id<CBPeripheralDelegate> delegate;
 
 /*!
  *  @property name
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBPeripheralManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBPeripheralManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBPeripheralManager.h	2015-09-30 20:41:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBPeripheralManager.h	2016-05-14 16:36:55.000000000 +0200
@@ -13,6 +13,7 @@
 
 #import <CoreBluetooth/CBDefines.h>
 #import <CoreBluetooth/CBError.h>
+#import <CoreBluetooth/CBManager.h>
 #import <CoreBluetooth/CBPeripheralManagerConstants.h>
 #import <Foundation/Foundation.h>
 
@@ -50,13 +51,13 @@
  *
  */
 typedef NS_ENUM(NSInteger, CBPeripheralManagerState) {
-	CBPeripheralManagerStateUnknown = 0,
-	CBPeripheralManagerStateResetting,
-	CBPeripheralManagerStateUnsupported,
-	CBPeripheralManagerStateUnauthorized,
-	CBPeripheralManagerStatePoweredOff,
-	CBPeripheralManagerStatePoweredOn,
-} NS_ENUM_AVAILABLE(NA, 6_0);
+	CBPeripheralManagerStateUnknown = CBManagerStateUnknown,
+	CBPeripheralManagerStateResetting = CBManagerStateResetting,
+	CBPeripheralManagerStateUnsupported = CBManagerStateUnsupported,
+	CBPeripheralManagerStateUnauthorized = CBManagerStateUnauthorized,
+	CBPeripheralManagerStatePoweredOff = CBManagerStatePoweredOff,
+	CBPeripheralManagerStatePoweredOn = CBManagerStatePoweredOn,
+} NS_DEPRECATED(NA, NA, 6_0, 10_0, "Use CBManagerState instead");
 
 /*!
  *  @enum CBPeripheralManagerConnectionLatency
@@ -74,7 +75,6 @@
 	CBPeripheralManagerConnectionLatencyHigh
 } NS_ENUM_AVAILABLE(NA, 6_0);
 
-
 @class CBCentral, CBService, CBMutableService, CBCharacteristic, CBMutableCharacteristic, CBATTRequest;
 @protocol CBPeripheralManagerDelegate;
 
@@ -95,7 +95,7 @@
  *
  */
 NS_CLASS_AVAILABLE(NA, 6_0)
-CB_EXTERN_CLASS @interface CBPeripheralManager : NSObject
+CB_EXTERN_CLASS @interface CBPeripheralManager : CBManager
 
 /*!
  *  @property delegate
@@ -103,16 +103,7 @@
  *  @discussion The delegate object that will receive peripheral events.
  *
  */
-@property(assign, nonatomic, nullable) id<CBPeripheralManagerDelegate> delegate;
-
-/*!
- *  @property state
- *
- *  @discussion The current state of the peripheral, initially set to <code>CBPeripheralManagerStateUnknown</code>. Updates are provided by required
- *              delegate method @link peripheralManagerDidUpdateState: @/link.
- *
- */
-@property(readonly) CBPeripheralManagerState state;
+@property(nonatomic, weak, nullable) id<CBPeripheralManagerDelegate> delegate;
 
 /*!
  *  @property isAdvertising
@@ -120,7 +111,7 @@
  *  @discussion Whether or not the peripheral is currently advertising data.
  *
  */
-@property(readonly) BOOL isAdvertising;
+@property(nonatomic, assign, readonly) BOOL isAdvertising;
 
 /*!
  *  @method authorizationStatus
@@ -134,6 +125,8 @@
  */
 + (CBPeripheralManagerAuthorizationStatus)authorizationStatus NS_AVAILABLE(NA, 7_0);
 
+- (instancetype)init;
+
 /*!
  *  @method initWithDelegate:queue:
  *
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBUUID.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBUUID.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBUUID.h	2015-09-30 20:41:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBUUID.h	2016-05-18 03:28:17.000000000 +0200
@@ -53,8 +53,11 @@
  *  @discussion The string representation of the UUID for the aggregate descriptor.
  */
 CB_EXTERN NSString * const CBUUIDCharacteristicAggregateFormatString;
-
-
+/*!
+ *  @const CBUUIDCharacteristicValidRangeString
+ *  @discussion Data representing the valid min/max values accepted for a characteristic.
+ */
+CB_EXTERN NSString * const CBUUIDCharacteristicValidRangeString;
 
 /*!
  * @class CBUUID

```