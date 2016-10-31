#CoreBluetooth.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBPeripheral.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBPeripheral.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBPeripheral.h	2016-07-30 23:46:36.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBPeripheral.h	2016-10-15 02:49:54.000000000 +0200
@@ -67,6 +67,7 @@
 	NSMutableDictionary			*_attributes;
 	BOOL						 _isPaired;
 	BOOL						 _isConnectedToSystem;
+    NSInteger                    role;
 }
 
 /*!

```