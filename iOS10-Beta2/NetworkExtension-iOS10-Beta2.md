#NetworkExtension.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEAppProxyFlow.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEAppProxyFlow.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEAppProxyFlow.h	2016-05-21 06:45:11.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEAppProxyFlow.h	2016-06-26 08:39:47.000000000 +0200
@@ -94,26 +94,5 @@
 
 @end
 
-/*!
- * @interface NEFlowMetaData
- * @discussion The NEFlowMetaData class declares the programmatic interface for an object that contains extra information about a flow.
- */
-NS_CLASS_AVAILABLE(10_11, 9_0)
-@interface NEFlowMetaData : NSObject
-
-/*!
- * @property sourceAppUniqueIdentifier
- * @discussion A blob of bytes that uniquely identifies the source app binary of the flow. This value is unique across multiple versions of the same app.
- */
-@property (readonly) NSData *sourceAppUniqueIdentifier NS_AVAILABLE(10_11, 9_0);
-
-/*!
- * @property sourceAppSigningIdentifier
- * @discussion A string containing the signing identifier (almost always equivalent to the bundle identifier) of the source app of the flow.
- */
-@property (readonly) NSString *sourceAppSigningIdentifier NS_AVAILABLE(10_11, 9_0);
-
-@end
-
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEFilterFlow.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEFilterFlow.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEFilterFlow.h	2016-05-21 08:21:25.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEFilterFlow.h	2016-06-26 09:04:35.000000000 +0200
@@ -77,14 +77,14 @@
  * @discussion The flow's remote endpoint. This endpoint object may be nil when [NEFilterDataProvider handleNewFlow:] is invoked and if so will be populated upon receiving network data.
 		In such a case, filtering on the flow may still be performed based on its socket type, socket family or socket protocol.
  */
-@property (readonly) NWEndpoint *remoteEndpoint NS_AVAILABLE(NA, 9_0);
+@property (readonly, nullable) NWEndpoint *remoteEndpoint NS_AVAILABLE(NA, 9_0);
 
 /*!
  * @property localEndpoint
  * @discussion The flow's local endpoint. This endpoint object may be nil when [NEFilterDataProvider handleNewFlow:] is invoked and if so will be populated upon receiving network data.
 		In such a case, filtering on the flow may still be performed based on its socket type, socket family or socket protocol.
  */
-@property (readonly) NWEndpoint *localEndpoint NS_AVAILABLE(NA, 9_0);
+@property (readonly, nullable) NWEndpoint *localEndpoint NS_AVAILABLE(NA, 9_0);
 
 /*!
  *	@property socketFamily
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEFlowMetaData.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEFlowMetaData.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEFlowMetaData.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEFlowMetaData.h	2016-06-26 09:04:35.000000000 +0200
@@ -0,0 +1,33 @@
+/*
+ * Copyright (c) 2016 Apple Inc.
+ * All rights reserved.
+ */
+
+#ifndef __NE_INDIRECT__
+#error "Please import the NetworkExtension module instead of this file directly."
+#endif
+
+NS_ASSUME_NONNULL_BEGIN
+
+/*!
+ * @interface NEFlowMetaData
+ * @discussion The NEFlowMetaData class declares the programmatic interface for an object that contains extra information about a flow.
+ */
+NS_CLASS_AVAILABLE(10_11, 9_0)
+@interface NEFlowMetaData : NSObject <NSCopying,NSSecureCoding>
+
+/*!
+ * @property sourceAppUniqueIdentifier
+ * @discussion A blob of bytes that uniquely identifies the source app binary of the flow. This value is unique across multiple versions of the same app.
+ */
+@property (readonly) NSData *sourceAppUniqueIdentifier NS_AVAILABLE(10_11, 9_0);
+
+/*!
+ * @property sourceAppSigningIdentifier
+ * @discussion A string containing the signing identifier (almost always equivalent to the bundle identifier) of the source app of the flow.
+ */
+@property (readonly) NSString *sourceAppSigningIdentifier NS_AVAILABLE(10_11, 9_0);
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEPacket.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEPacket.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEPacket.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEPacket.h	2016-06-26 09:04:35.000000000 +0200
@@ -0,0 +1,60 @@
+/*
+ * Copyright (c) 2016 Apple Inc.
+ * All rights reserved.
+ */
+
+#ifndef __NE_INDIRECT__
+#error "Please import the NetworkExtension module instead of this file directly."
+#endif
+
+#import <netinet/in.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class NEFlowMetaData;
+
+/*!
+ * @interface NEPacket
+ * @discussion An NEPacket object represents the data, protocol family, and metadata associated with an IP packet. 
+ *	These packets are used to read and write on an NEPacketTunnelFlow.
+ *
+ * NEPacket is part of NetworkExtension.framework
+ *
+ * Instances of this class are thread safe.
+ */
+__attribute__((visibility("default")))
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NEPacket : NSObject <NSCopying,NSSecureCoding>
+
+/*!
+ * @method initWithData:protocolFamily:
+ * @discussion Initializes a new NEPacket object with data and protocol family.
+ * @param data The content of the packet.
+ * @param protocolFamily The protocol family of the packet (such as AF_INET or AF_INET6).
+ */
+- (instancetype)initWithData:(NSData *)data
+			  protocolFamily:(sa_family_t)protocolFamily API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+/*!
+ * @property data
+ * @discussion The data content of the packet.
+ */
+@property (readonly, copy) NSData *data API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+/*!
+ * @property protocolFamily
+ * @discussion The protocol family of the packet (such as AF_INET or AF_INET6).
+ */
+@property (readonly) sa_family_t protocolFamily API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+/*!
+ * @property metadata
+ * @discussion Metadata about the source application and flow for this packet.
+ *	This property will only be non-nil when the routing method for the NEPacketTunnelProvider
+ *	is NETunnelProviderRoutingMethodSourceApplication.
+ */
+@property (readonly, nullable) NEFlowMetaData *metadata API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEPacketTunnelFlow.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEPacketTunnelFlow.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEPacketTunnelFlow.h	2016-05-21 08:21:25.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEPacketTunnelFlow.h	2016-06-26 09:04:35.000000000 +0200
@@ -9,6 +9,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+@class NEPacket;
+
 /*!
  * @file NEPacketTunnelFlow.h
  * @discussion This file declares the NEPacketTunnelFlow API. The NEPacketTunnelFlow is used by NEPacketTunnelProvider implementations to tunnel IP packets.
@@ -40,6 +42,20 @@
  */
 - (BOOL)writePackets:(NSArray<NSData *> *)packets withProtocols:(NSArray<NSNumber *> *)protocols NS_AVAILABLE(10_11, 9_0);
 
+/*!
+ * @method readPacketObjectsWithCompletionHandler:
+ * @discussion Read available IP packets from the flow.
+ * @param completionHandler A block that will be executed to handle the packets. This block takes an array of NEPacket objects. If after handling the packets the caller wants to read more packets then the caller must call this method again.
+ */
+- (void)readPacketObjectsWithCompletionHandler:(void (^)(NSArray<NEPacket *> *packets))completionHandler NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ * @method writePacketObjects:
+ * @discussion Write multiple IP packets to the flow.
+ * @param packets An array of NEPacket objects, each containing packet data and protocol family to be written.
+ */
+- (BOOL)writePacketObjects:(NSArray<NEPacket *> *)packets NS_AVAILABLE(10_12, 10_0);
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NetworkExtension.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NetworkExtension.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NetworkExtension.h	2016-05-21 08:21:25.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NetworkExtension.h	2016-06-26 09:04:35.000000000 +0200
@@ -22,12 +22,14 @@
 #import <NetworkExtension/NEFilterManager.h>
 #import <NetworkExtension/NEFilterProvider.h>
 #import <NetworkExtension/NEFilterProviderConfiguration.h>
+#import <NetworkExtension/NEFlowMetaData.h>
 #if TARGET_OS_IPHONE
 #import <NetworkExtension/NEHotspotHelper.h>
 #endif
 #import <NetworkExtension/NEIPv4Settings.h>
 #import <NetworkExtension/NEIPv6Settings.h>
 #import <NetworkExtension/NEOnDemandRule.h>
+#import <NetworkExtension/NEPacket.h>
 #import <NetworkExtension/NEPacketTunnelFlow.h>
 #import <NetworkExtension/NEPacketTunnelNetworkSettings.h>
 #import <NetworkExtension/NEPacketTunnelProvider.h>

```