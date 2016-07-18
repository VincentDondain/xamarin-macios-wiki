#CoreBluetooth.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBCentralManager.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBCentralManager.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBCentralManager.h	2016-06-25 00:18:58.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBCentralManager.h	2016-07-10 12:03:55.000000000 +0200
@@ -62,7 +62,7 @@
 @property(nonatomic, weak, nullable) id<CBCentralManagerDelegate> delegate;
 
 /*!
- *  @property isAdvertising
+ *  @property isScanning
  *
  *  @discussion Whether or not the central is currently scanning.
  *

```