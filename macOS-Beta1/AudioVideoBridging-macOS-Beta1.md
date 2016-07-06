#AudioVideoBridging.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AudioVideoBridging.framework/Headers/AVBEthernetInterface.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioVideoBridging.framework/Headers/AVBEthernetInterface.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AudioVideoBridging.framework/Headers/AVBEthernetInterface.h	2015-08-23 04:05:19.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioVideoBridging.framework/Headers/AVBEthernetInterface.h	2016-05-20 08:23:23.000000000 +0200
@@ -18,8 +18,10 @@
 NS_CLASS_AVAILABLE(10_8, NA)
 @interface AVBEthernetInterface : AVBInterface
 {
+#if AVB_LEGACY_OBJC_RUNTIME
 @private
-	io_object_t _notification;
+	void *_ethernetInterfaceImpl;
+#endif
 }
 
 @end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AudioVideoBridging.framework/Headers/AVBInterface.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioVideoBridging.framework/Headers/AVBInterface.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AudioVideoBridging.framework/Headers/AVBInterface.h	2015-08-23 04:05:19.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioVideoBridging.framework/Headers/AVBInterface.h	2016-05-20 08:23:23.000000000 +0200
@@ -12,20 +12,12 @@
 NS_ASSUME_NONNULL_BEGIN
 
 @class AVBMACAddress;
-@class AVBNetworkClient;
 
-@class AVBMVRP;
-@class AVBMSRPDomain;
-@class AVBMSRPListener;
-@class AVBMSRPTalker;
 @class AVB17221EntityDiscovery;
 
-@class TSgPTPClock;
-
 @class AVB17221AECPInterface;
 @class AVB17221ACMPInterface;
 
-@class AVB1722MAAP;
 
 @protocol AVBInterfaceDelegate;
 
@@ -39,54 +31,10 @@
 NS_CLASS_AVAILABLE(10_8, NA)
 @interface AVBInterface : NSObject
 {
-	@private
-	AVBNetworkClient *_networkClient;
-	
-	NSString *_interfaceName;
-	
-	AVBMVRP *_mvrp;
-	AVBMSRPDomain *_msrpDomain;
-	AVBMSRPListener *_msrpListener;
-	AVBMSRPTalker *_msrpTalker;
-	AVB17221EntityDiscovery *_entityDiscovery;
-	
-	TSgPTPClock *_timeSync;
-
-	AVB17221AECPInterface *_aecp;
-	AVB17221ACMPInterface *_acmp;
-	
-	AVB1722MAAP *_maap;
-	
-	AVBMACAddress *_macAddress;
-	
-	id<AVBInterfaceDelegate> _interfaceDelegate;
-	
-	dispatch_queue_t _networkClientCreationQueue;
-	dispatch_queue_t _mvrpCreationQueue;
-	dispatch_queue_t _msrpDomainCreationQueue;
-	dispatch_queue_t _msrpListenerCreationQueue;
-	dispatch_queue_t _msrpTalkerCreationQueue;
-	dispatch_queue_t _entityDiscoveryCreationQueue;
-	dispatch_queue_t _timeSyncCreationQueue;
-	dispatch_queue_t _aecpCreationQueue;
-	dispatch_queue_t _acmpCreationQueue;
-	dispatch_queue_t _maapCreationQueue;
-	
-	dispatch_queue_t _notificationQueue;
-	IONotificationPortRef _notificationPort;
-	
-	io_iterator_t _networkClientIterator;
-	io_iterator_t _mvrpIterator;
-	io_iterator_t _msrpDomainIterator;
-	io_iterator_t _msrpListenerIterator;
-	io_iterator_t _msrpTalkerIterator;
-	io_iterator_t _entityDiscoveryIterator;
-	io_iterator_t _timeSyncIterator;
-	io_iterator_t _aecpIterator;
-	io_iterator_t _acmpIterator;
-	io_iterator_t _maapIterator;
-	
-	NSMutableArray *_virtualEntities;
+#if AVB_LEGACY_OBJC_RUNTIME
+@private
+	void *_interfaceImpl;
+#endif
 }
 
 /*!
@@ -142,13 +90,15 @@
  */
 + (BOOL)isAVBCapableInterfaceNamed:(NSString *)anInterfaceName;
 
+- (instancetype)init NS_UNAVAILABLE;
+
 /*!
 	@method		initWithInterfaceName:
 	@abstract	This method initializes the receiver to work on the specified interface.
 	@param		anInterfaceName	The BSD name of the interface.
 	@result		The initialized receiver.
  */
-- (nullable instancetype)initWithInterfaceName:(NSString *)anInterfaceName;
+- (nullable instancetype)initWithInterfaceName:(NSString *)anInterfaceName NS_DESIGNATED_INITIALIZER;
 
 /*!
  @method		myGUID

```