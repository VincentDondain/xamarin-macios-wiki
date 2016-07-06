#CoreBluetooth.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBPeripheral.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBPeripheral.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBPeripheral.h	2016-05-11 15:54:22.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreBluetooth.framework/Headers/CBPeripheral.h	2016-06-26 06:00:02.000000000 +0200
@@ -190,6 +190,15 @@
 - (void)readValueForCharacteristic:(CBCharacteristic *)characteristic;
 
 /*!
+ *  @method		maximumWriteValueLengthForType:
+ *
+ *  @discussion	The maximum amount of data, in bytes, that can be sent to a characteristic in a single write type.
+ *
+ *  @see		writeValue:forCharacteristic:type:
+ */
+- (NSUInteger)maximumWriteValueLengthForType:(CBCharacteristicWriteType)type NS_AVAILABLE(10_12, 9_0);
+
+/*!
  *  @method writeValue:forCharacteristic:type:
  *
  *  @param data				The value to write.
@@ -418,4 +427,4 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END

```