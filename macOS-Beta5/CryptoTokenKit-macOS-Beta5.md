#CryptoTokenKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKSmartCard.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKSmartCard.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKSmartCard.h	2016-07-27 04:20:30.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKSmartCard.h	2016-08-06 06:08:51.000000000 +0200
@@ -18,7 +18,7 @@
 
 /// Global pool of smart card reader slots.
 /// Note that defaultManager instance is accessible only if the calling application has 'com.apple.security.smartcard' entitlement set to Boolean:YES.  If the calling application does not have this entitlement, defaultManager is always set to nil.
-+ (nullable instancetype)defaultManager;
+@property (class, nullable, readonly) TKSmartCardSlotManager *defaultManager;
 
 /// Array of currently known slots in the system.  Slots are identified by NSString name instances.  Use KVO to be notified about slots arrivals and removals.
 @property (readonly) NSArray<NSString *> *slotNames;
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKTLVRecord.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKTLVRecord.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKTLVRecord.h	2016-07-27 04:20:30.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKTLVRecord.h	2016-08-06 06:08:51.000000000 +0200
@@ -72,6 +72,7 @@
 /// TKSimpleTLVRecord implements Simple-TLV encoding according to ISO7816-4.
 /// Tag is number in range <1..254> encoded as single byte, length is either single byte specifying length 0-254
 /// or 3 bytes encoded as 0xff followed by 2 bytes of big-endian encoded number.
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
 @interface TKSimpleTLVRecord : TKTLVRecord
 
 /// Creates TLV record with specified tag and value.

```