#NetworkExtension.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEFilterFlow.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEFilterFlow.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEFilterFlow.h	2015-10-03 00:30:41.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEFilterFlow.h	2016-05-21 08:21:25.000000000 +0200
@@ -1,5 +1,5 @@
 /*
- * Copyright (c) 2015 Apple Inc.
+ * Copyright (c) 2015, 2016 Apple Inc.
  * All rights reserved.
  */
 
@@ -74,13 +74,15 @@
 @interface NEFilterSocketFlow : NEFilterFlow <NSSecureCoding,NSCopying>
 /*!
  * @property remoteEndpoint
- * @discussion The flow's remote endpoint.
+ * @discussion The flow's remote endpoint. This endpoint object may be nil when [NEFilterDataProvider handleNewFlow:] is invoked and if so will be populated upon receiving network data.
+		In such a case, filtering on the flow may still be performed based on its socket type, socket family or socket protocol.
  */
 @property (readonly) NWEndpoint *remoteEndpoint NS_AVAILABLE(NA, 9_0);
 
 /*!
  * @property localEndpoint
- * @discussion The flow's local endpoint.
+ * @discussion The flow's local endpoint. This endpoint object may be nil when [NEFilterDataProvider handleNewFlow:] is invoked and if so will be populated upon receiving network data.
+		In such a case, filtering on the flow may still be performed based on its socket type, socket family or socket protocol.
  */
 @property (readonly) NWEndpoint *localEndpoint NS_AVAILABLE(NA, 9_0);
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEFilterManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEFilterManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEFilterManager.h	2015-10-03 00:30:41.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEFilterManager.h	2016-05-21 08:21:25.000000000 +0200
@@ -39,13 +39,13 @@
 	NEFilterManagerErrorConfigurationStale = 3,
 	/*! @const NEFilterManagerErrorConfigurationCannotBeRemoved The filter configuration cannot be removed. */
 	NEFilterManagerErrorConfigurationCannotBeRemoved = 4,
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} NS_ENUM_AVAILABLE(10_11, 8_0);
 
 /*! @const NEFilterErrorDomain The filter error domain */
-NEFILTER_EXPORT NSString * const NEFilterErrorDomain NS_AVAILABLE(10_10, 8_0);
+NEFILTER_EXPORT NSString * const NEFilterErrorDomain NS_AVAILABLE(10_11, 8_0);
 
 /*! @const NEFilterConfigurationDidChangeNotification Name of the NSNotification that is posted when the filter configuration changes. */
-NEFILTER_EXPORT NSString * const NEFilterConfigurationDidChangeNotification NS_AVAILABLE(10_10, 8_0);
+NEFILTER_EXPORT NSString * const NEFilterConfigurationDidChangeNotification NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @interface NEFilterManager
@@ -55,41 +55,41 @@
  *
  * Instances of this class are thread safe.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_11, 8_0)
 @interface NEFilterManager : NSObject
 
 /*!
  * @method sharedManager
  * @return The singleton NEFilterManager object for the calling process.
  */
-+ (NEFilterManager *)sharedManager NS_AVAILABLE(10_10, 8_0);
++ (NEFilterManager *)sharedManager NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @method loadFromPreferencesWithCompletionHandler:
  * @discussion This function loads the current filter configuration from the caller's filter preferences.
  * @param completionHandler A block that will be called when the load operation is completed. The NSError passed to this block will be nil if the load operation succeeded, non-nil otherwise.
  */
-- (void)loadFromPreferencesWithCompletionHandler:(void (^)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 8_0);
+- (void)loadFromPreferencesWithCompletionHandler:(void (^)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @method removeFromPreferencesWithCompletionHandler:
  * @discussion This function removes the filter configuration from the caller's filter preferences. If the filter is enabled, the filter becomes disabled.
  * @param completionHandler A block that will be called when the remove operation is completed. The NSError passed to this block will be nil if the remove operation succeeded, non-nil otherwise.
  */
-- (void)removeFromPreferencesWithCompletionHandler:(void (^)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 8_0);
+- (void)removeFromPreferencesWithCompletionHandler:(void (^)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @method saveToPreferencesWithCompletionHandler:
  * @discussion This function saves the filter configuration in the caller's filter preferences. If the filter is enabled, it will become active.
  * @param completionHandler A block that will be called when the save operation is completed. The NSError passed to this block will be nil if the save operation succeeded, non-nil otherwise.
  */
-- (void)saveToPreferencesWithCompletionHandler:(void (^)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 8_0);
+- (void)saveToPreferencesWithCompletionHandler:(void (^)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property localizedDescription
  * @discussion A string containing a description of the filter.
  */
-@property (copy, nullable) NSString *localizedDescription NS_AVAILABLE(10_10, 8_0);
+@property (copy, nullable) NSString *localizedDescription NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property providerConfiguration
@@ -101,7 +101,7 @@
  * @property enabled
  * @discussion Toggles the enabled status of the filter. Setting this property will disable filter configurations of other apps. This property will be set to NO when other filter configurations are enabled.
  */
-@property (getter=isEnabled) BOOL enabled NS_AVAILABLE(10_10, 8_0);
+@property (getter=isEnabled) BOOL enabled NS_AVAILABLE(10_11, 8_0);
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEOnDemandRule.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEOnDemandRule.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEOnDemandRule.h	2015-10-03 00:30:41.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEOnDemandRule.h	2016-05-21 06:45:11.000000000 +0200
@@ -33,7 +33,7 @@
 	NEOnDemandRuleActionEvaluateConnection = 3,
 	/*! @const NEOnDemandRuleActionIgnore Do not start the VPN connection, and leave the VPN connection in its current state */
 	NEOnDemandRuleActionIgnore = 4,
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} NS_ENUM_AVAILABLE(10_11, 8_0);
 
 /*!
  * @typedef NEOnDemandRuleInterfaceType
@@ -43,12 +43,12 @@
 	/*! @const NEOnDemandRuleInterfaceTypeAny */
 	NEOnDemandRuleInterfaceTypeAny NS_ENUM_AVAILABLE(10_11, 9_0) = 0,
 	/*! @const NEOnDemandRuleInterfaceTypeEthernet Wired Ethernet */
-	NEOnDemandRuleInterfaceTypeEthernet NS_ENUM_AVAILABLE(10_10, NA) = 1,
+	NEOnDemandRuleInterfaceTypeEthernet NS_ENUM_AVAILABLE(10_11, NA) = 1,
 	/*! @const NEOnDemandRuleInterfaceTypeWiFi WiFi */
-	NEOnDemandRuleInterfaceTypeWiFi NS_ENUM_AVAILABLE(10_10, 8_0) = 2,
+	NEOnDemandRuleInterfaceTypeWiFi NS_ENUM_AVAILABLE(10_11, 8_0) = 2,
 	/*! @const NEOnDemandRuleInterfaceTypeCellular Cellular */
 	NEOnDemandRuleInterfaceTypeCellular NS_ENUM_AVAILABLE(NA, 8_0) = 3,
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} NS_ENUM_AVAILABLE(10_11, 8_0);
 
 /*!
  * @interface NEOnDemandRule
@@ -58,44 +58,44 @@
  *
  * Instances of this class are thread safe.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_11, 8_0)
 @interface NEOnDemandRule : NSObject <NSSecureCoding,NSCopying>
 
 /*!
  * @property action
  * @discussion The rule's action
  */
-@property (readonly) NEOnDemandRuleAction action NS_AVAILABLE(10_10, 8_0);
+@property (readonly) NEOnDemandRuleAction action NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property DNSSearchDomainMatch
  * @discussion An array of NSString objects. If the current default search domain is equal to one of the strings in this array and all of the other conditions in the rule match, then the rule matches. If this property is nil (the default), then the current default search domain does not factor into the rule match.
  */
-@property (copy, nullable) NSArray<NSString *> *DNSSearchDomainMatch NS_AVAILABLE(10_10, 8_0);
+@property (copy, nullable) NSArray<NSString *> *DNSSearchDomainMatch NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property DNSServerAddressMatch
  * @discussion An array of DNS server IP addresses represented as NSString objects. If each of the current default DNS servers is equal to one of the strings in this array and all of the other conditions in the rule match, then the rule matches. If this property is nil (the default), then the default DNS servers do not factor into the rule match.
  */
-@property (copy, nullable) NSArray<NSString *> *DNSServerAddressMatch NS_AVAILABLE(10_10, 8_0);
+@property (copy, nullable) NSArray<NSString *> *DNSServerAddressMatch NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property interfaceTypeMatch
  * @discussion The type of interface that this rule matches. If the current primary network interface is of this type and all of the other conditions in the rule match, then the rule matches. If this property is 0 (the default), then the current primary interface type does not factor into the rule match.
  */
-@property NEOnDemandRuleInterfaceType interfaceTypeMatch NS_AVAILABLE(10_10, 8_0);
+@property NEOnDemandRuleInterfaceType interfaceTypeMatch NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property SSIDMatch
  * @discussion An array of NSString objects. If the Service Set Identifier (SSID) of the current primary connected network matches one of the strings in this array and all of the other conditions in the rule match, then the rule matches. If this property is nil (the default), then the current primary connected network SSID does not factor into the rule match.
  */
-@property (copy, nullable) NSArray<NSString *> *SSIDMatch NS_AVAILABLE(10_10, 8_0);
+@property (copy, nullable) NSArray<NSString *> *SSIDMatch NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property probeURL
  * @discussion An HTTP or HTTPS URL. If a request sent to this URL results in a HTTP 200 OK response and all of the other conditions in the rule match, then then rule matches. If this property is nil (the default), then an HTTP request does not factor into the rule match.
  */
-@property (copy, nullable) NSURL *probeURL NS_AVAILABLE(10_10, 8_0);
+@property (copy, nullable) NSURL *probeURL NS_AVAILABLE(10_11, 8_0);
 
 @end
 
@@ -107,7 +107,7 @@
  *
  * Instances of this class are thread safe.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_11, 8_0)
 @interface NEOnDemandRuleConnect : NEOnDemandRule
 @end
 
@@ -119,7 +119,7 @@
  *
  * Instances of this class are thread safe.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_11, 8_0)
 @interface NEOnDemandRuleDisconnect : NEOnDemandRule
 @end
 
@@ -131,7 +131,7 @@
  *
  * Instances of this class are thread safe.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_11, 8_0)
 @interface NEOnDemandRuleIgnore : NEOnDemandRule
 @end
 
@@ -143,14 +143,14 @@
  *
  * Instances of this class are thread safe.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_11, 8_0)
 @interface NEOnDemandRuleEvaluateConnection : NEOnDemandRule
 
 /*!
  * @property connectionRules
  * @discussion An array of NEEvaluateConnectionRule objects. Each NEEvaluateConnectionRule object is evaluated in order against the properties of the network connection being established.
  */
-@property (copy, nullable) NSArray<NEEvaluateConnectionRule *> *connectionRules NS_AVAILABLE(10_10, 8_0);
+@property (copy, nullable) NSArray<NEEvaluateConnectionRule *> *connectionRules NS_AVAILABLE(10_11, 8_0);
 
 @end
 
@@ -163,7 +163,7 @@
 	NEEvaluateConnectionRuleActionConnectIfNeeded = 1,
 	/*! @const NEEvaluateConnectionRuleActionNeverConnect Do not start the VPN connection */
 	NEEvaluateConnectionRuleActionNeverConnect = 2,
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} NS_ENUM_AVAILABLE(10_11, 8_0);
 
 /*!
  * @interface NEEvaluateConnectionRule
@@ -171,38 +171,38 @@
  *
  * Instances of this class are thread safe.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_11, 8_0)
 @interface NEEvaluateConnectionRule : NSObject <NSSecureCoding,NSCopying>
 
 /*!
  * @method initWithMatchDomains:andAction
  * @discussion Initialize an NEEvaluateConnectionRule instance with a list of destination host domains and an action
  */
-- (instancetype)initWithMatchDomains:(NSArray<NSString *> *)domains andAction:(NEEvaluateConnectionRuleAction)action NS_AVAILABLE(10_10, 8_0);
+- (instancetype)initWithMatchDomains:(NSArray<NSString *> *)domains andAction:(NEEvaluateConnectionRuleAction)action NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property action
  * @discussion The action to take if the properties of the network connection being established match the rule.
  */
-@property (readonly) NEEvaluateConnectionRuleAction action NS_AVAILABLE(10_10, 8_0);
+@property (readonly) NEEvaluateConnectionRuleAction action NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property matchDomains
  * @discussion An array of NSString objects. If the host name of the destination of the network connection being established shares a suffix with one of the strings in this array, then the rule matches.
  */
-@property (readonly) NSArray<NSString *> *matchDomains NS_AVAILABLE(10_10, 8_0);
+@property (readonly) NSArray<NSString *> *matchDomains NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property useDNSServers
  * @discussion An array of NSString objects. If the rule matches the connection being established and the action is NEEvaluateConnectionRuleActionConnectIfNeeded, the DNS servers specified in this array are used to resolve the host name of the destination while evaluating connectivity to the destination. If the resolution fails for any reason, the VPN is started.
  */
-@property (copy, nullable) NSArray<NSString *> *useDNSServers NS_AVAILABLE(10_10, 8_0);
+@property (copy, nullable) NSArray<NSString *> *useDNSServers NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property probeURL
  * @discussion An HTTP or HTTPS URL. If the rule matches the connection being established and the action is NEEvaluateConnectionRuleActionConnectIfNeeded and a request sent to this URL results in a response with an HTTP response code other than 200, then the VPN is started.
  */
-@property (copy, nullable) NSURL *probeURL NS_AVAILABLE(10_10, 8_0);
+@property (copy, nullable) NSURL *probeURL NS_AVAILABLE(10_11, 8_0);
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEProvider.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEProvider.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEProvider.h	2015-10-03 00:30:41.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEProvider.h	2016-05-21 08:04:41.000000000 +0200
@@ -107,6 +107,14 @@
 - (NWUDPSession *)createUDPSessionToEndpoint:(NWEndpoint *)remoteEndpoint fromEndpoint:(nullable NWHostEndpoint *)localEndpoint NS_AVAILABLE(10_11, 9_0);
 
 /*!
+ * @method displayMessage:completionHandler:
+ * @discussion This method can be called by subclass implementations to display a message to the user.
+ * @param message The message to be displayed.
+ * @param completionHandler A block that is executed when the user acknowledges the message. If this method is called on a NEFilterDataProvider instance or the message cannot be displayed, then the completion handler block will be executed immediately with success parameter set to NO. If the message was successfully displayed to the user, then the completion handler block is executed with the success parameter set to YES when the user dismisses the message.
+ */
+- (void)displayMessage:(NSString *)message completionHandler:(void (^)(BOOL success))completionHandler NS_AVAILABLE(10_12, 10_0);
+
+/*!
  * @property defaultPath
  * @discussion The current default path for connections created by the provider. Use KVO to watch for network changes.
  */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEVPNConnection.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEVPNConnection.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEVPNConnection.h	2015-10-03 00:30:41.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEVPNConnection.h	2016-05-21 08:21:25.000000000 +0200
@@ -13,6 +13,8 @@
 #define NEVPN_EXPORT extern
 #endif
 
+@class NEVPNManager;
+
 /*!
  * @typedef NEVPNStatus
  * @abstract VPN status codes
@@ -30,15 +32,15 @@
     NEVPNStatusReasserting = 4,
     /*! @const NEVPNStatusDisconnecting The VPN is disconnecting. */
     NEVPNStatusDisconnecting = 5,
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} NS_ENUM_AVAILABLE(10_11, 8_0);
 
 /*! @const NEVPNStatusDidChangeNotification Name of the NSNotification that is posted when the VPN status changes. */
-NEVPN_EXPORT NSString * const NEVPNStatusDidChangeNotification NS_AVAILABLE(10_10, 8_0);
+NEVPN_EXPORT NSString * const NEVPNStatusDidChangeNotification NS_AVAILABLE(10_11, 8_0);
 
 /*! @const NEVPNConnectionStartOptionUsername Specify this key in the options dictionary passed to startVPNTunnelWithOptions:returningError: to override the username saved in the configuration. The value is a string */
 NEVPN_EXPORT NSString * const NEVPNConnectionStartOptionUsername NS_AVAILABLE(10_11, 9_0);
 
-/*! @const kNEVPNConnectioNEVPNConnectionStartOptionPasswordnOptionAuthPassword Specify this key in the options dictionary passed to startVPNTunnelWithOptions:returningError: to override the password saved in the configuration. The value is a string */
+/*! @const NEVPNConnectionStartOptionPassword Specify this key in the options dictionary passed to startVPNTunnelWithOptions:returningError: to override the password saved in the configuration. The value is a string */
 NEVPN_EXPORT NSString * const NEVPNConnectionStartOptionPassword NS_AVAILABLE(10_11, 9_0);
 
 /*!
@@ -47,7 +49,7 @@
  *
  * Instances of this class are thread safe.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_11, 8_0)
 @interface NEVPNConnection : NSObject
 
 /*!
@@ -58,7 +60,7 @@
  *    2. NEVPNErrorConfigurationDisabled
  * @return YES if the VPN tunnel was started successfully, NO if an error occurred.
  */
-- (BOOL)startVPNTunnelAndReturnError:(NSError **)error NS_AVAILABLE(10_10, 8_0);
+- (BOOL)startVPNTunnelAndReturnError:(NSError **)error NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @method startVPNTunnelWithOptions:andReturnError:
@@ -78,13 +80,13 @@
  * @method stopVPNTunnel:
  * @discussion This function is used to stop the VPN tunnel. The VPN tunnel disconnect process is started and this function returns immediately.
  */
-- (void)stopVPNTunnel NS_AVAILABLE(10_10, 8_0);
+- (void)stopVPNTunnel NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property status
  * @discussion The current status of the VPN.
  */
-@property (readonly) NEVPNStatus status NS_AVAILABLE(10_10, 8_0);
+@property (readonly) NEVPNStatus status NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property connectedDate
@@ -92,6 +94,12 @@
  */
 @property (readonly, nullable) NSDate *connectedDate NS_AVAILABLE(10_11, 9_0);
 
+/*!
+ * @property manager
+ * @discussion The NEVPNManager associated with this NEVPNConnection.
+ */
+@property (readonly) NEVPNManager *manager NS_AVAILABLE(10_12, 10_0);
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEVPNManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEVPNManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEVPNManager.h	2015-10-03 00:30:41.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEVPNManager.h	2016-05-21 08:04:41.000000000 +0200
@@ -49,13 +49,13 @@
     NEVPNErrorConfigurationReadWriteFailed = 5,
     /*! @const NEVPNErrorConfigurationUnknown An unknown configuration error occurred. */
     NEVPNErrorConfigurationUnknown = 6,
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} NS_ENUM_AVAILABLE(10_11, 8_0);
 
 /*! @const NEVPNErrorDomain The VPN error domain */
-NEVPN_EXPORT NSString * const NEVPNErrorDomain NS_AVAILABLE(10_10, 8_0);
+NEVPN_EXPORT NSString * const NEVPNErrorDomain NS_AVAILABLE(10_11, 8_0);
 
 /*! @const NEVPNConfigurationChangeNotification Name of the NSNotification that is posted when the VPN configuration changes. */
-NEVPN_EXPORT NSString * const NEVPNConfigurationChangeNotification NS_AVAILABLE(10_10, 8_0);
+NEVPN_EXPORT NSString * const NEVPNConfigurationChangeNotification NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @interface NEVPNManager
@@ -65,28 +65,28 @@
  *
  * Instances of this class are thread safe.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_11, 8_0)
 @interface NEVPNManager : NSObject
 
 /*!
  * @method sharedManager
  * @return The singleton NEVPNManager object for the calling process.
  */
-+ (NEVPNManager *)sharedManager NS_AVAILABLE(10_10, 8_0);
++ (NEVPNManager *)sharedManager NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @method loadFromPreferencesWithCompletionHandler:
  * @discussion This function loads the current VPN configuration from the caller's VPN preferences.
  * @param completionHandler A block that will be called on the main thread when the load operation is completed. The NSError passed to this block will be nil if the load operation succeeded, non-nil otherwise.
  */
-- (void)loadFromPreferencesWithCompletionHandler:(void (^)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 8_0);
+- (void)loadFromPreferencesWithCompletionHandler:(void (^)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @method removeFromPreferencesWithCompletionHandler:
  * @discussion This function removes the VPN configuration from the caller's VPN preferences. If the VPN is enabled, has VPN On Demand enabled, and has VPN On Demand rules, the VPN is disabled and the VPN On Demand rules are de-activated.
  * @param completionHandler A block that will be called on the main thread when the remove operation is completed. The NSError passed to this block will be nil if the remove operation succeeded, non-nil otherwise.
  */
-- (void)removeFromPreferencesWithCompletionHandler:(nullable void (^)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 8_0);
+- (void)removeFromPreferencesWithCompletionHandler:(nullable void (^)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @method saveToPreferencesWithCompletionHandler:
@@ -94,7 +94,7 @@
  *
  * @param completionHandler A block that will be called on the main thread when the save operation is completed. The NSError passed to this block will be nil if the save operation succeeded, non-nil otherwise.
  */
-- (void)saveToPreferencesWithCompletionHandler:(nullable void (^)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 8_0);
+- (void)saveToPreferencesWithCompletionHandler:(nullable void (^)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_11, 8_0);
 
 #if !TARGET_OS_IPHONE && !TARGET_IPHONE_SIMULATOR
 /*!
@@ -102,32 +102,32 @@
  * @discussion This function sets an authorization object that can be used to obtain the authorization rights necessary to modify the system VPN configuration.
  * @param authorization The AuthorizationRef to use to obtain rights.
  */
-- (void)setAuthorization:(AuthorizationRef)authorization NS_AVAILABLE(10_10, NA);
+- (void)setAuthorization:(AuthorizationRef)authorization NS_AVAILABLE(10_11, NA);
 #endif
 
 /*!
  * @property onDemandRules
  * @discussion An array of NEOnDemandRule objects.
  */
-@property (copy, nullable) NSArray<NEOnDemandRule *> *onDemandRules NS_AVAILABLE(10_10, 8_0);
+@property (copy, nullable) NSArray<NEOnDemandRule *> *onDemandRules NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property onDemandEnabled
  * @discussion Toggles VPN On Demand.
  */
-@property (getter=isOnDemandEnabled) BOOL onDemandEnabled NS_AVAILABLE(10_10, 8_0);
+@property (getter=isOnDemandEnabled) BOOL onDemandEnabled NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property localizedDescription
  * @discussion A string containing a description of the VPN.
  */
-@property (copy, nullable) NSString *localizedDescription NS_AVAILABLE(10_10, 8_0);
+@property (copy, nullable) NSString *localizedDescription NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property protocol
  * @discussion An NEVPNProtocol object containing the protocol-specific portion of the VPN configuration.
  */
-@property (strong, nullable) NEVPNProtocol *protocol NS_DEPRECATED(10_10, 10_11, 8_0, 9_0, "Use protocolConfiguration instead");
+@property (strong, nullable) NEVPNProtocol *protocol NS_DEPRECATED(10_11, 10_11, 8_0, 9_0, "Use protocolConfiguration instead");
 
 /*!
  * @property protocolConfiguration
@@ -139,13 +139,13 @@
  * @property connection
  * @discussion The NEVPNConnection object used for controlling the VPN tunnel.
  */
-@property (readonly) NEVPNConnection *connection NS_AVAILABLE(10_10, 8_0);
+@property (readonly) NEVPNConnection *connection NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property enabled
  * @discussion Toggles the enabled status of the VPN. Setting this property will disable VPN configurations of other apps. This property will be set to NO  when other VPN configurations are enabled.
  */
-@property (getter=isEnabled) BOOL enabled NS_AVAILABLE(10_10, 8_0);
+@property (getter=isEnabled) BOOL enabled NS_AVAILABLE(10_11, 8_0);
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEVPNProtocol.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEVPNProtocol.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEVPNProtocol.h	2015-10-03 00:30:41.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEVPNProtocol.h	2016-05-21 08:21:25.000000000 +0200
@@ -21,32 +21,32 @@
  *
  * Instances of this class are thread safe.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_11, 8_0)
 @interface NEVPNProtocol : NSObject <NSCopying,NSSecureCoding>
 
 /*!
  * @property serverAddress
  * @discussion The VPN server. Depending on the protocol, may be an IP address, host name, or URL.
  */
-@property (copy, nullable) NSString *serverAddress NS_AVAILABLE(10_10, 8_0);
+@property (copy, nullable) NSString *serverAddress NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property username
  * @discussion The username component of the VPN authentication credential.
  */
-@property (copy, nullable) NSString *username NS_AVAILABLE(10_10, 8_0);
+@property (copy, nullable) NSString *username NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property passwordReference
  * @discussion The password component of the VPN authentication credential. The value is a persistent reference to a keychain item with the kSecClassGenericPassword class.
  */
-@property (copy, nullable) NSData *passwordReference NS_AVAILABLE(10_10, 8_0);
+@property (copy, nullable) NSData *passwordReference NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property identityReference
  * @discussion The certificate and private key component of the VPN authentication credential. The value is a persistent reference to a keychain item with the kSecClassIdentity class.
  */
-@property (copy, nullable) NSData *identityReference NS_AVAILABLE(10_10, 9_0);
+@property (copy, nullable) NSData *identityReference NS_AVAILABLE(10_11, 9_0);
 
 /*!
  * @property identityData
@@ -64,7 +64,7 @@
  * @property disconnectOnSleep
  * @discussion If YES, the VPN connection will be disconnected when the device goes to sleep. The default is NO.
  */
-@property BOOL disconnectOnSleep NS_AVAILABLE(10_10, 8_0);
+@property BOOL disconnectOnSleep NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property proxySettings
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEVPNProtocolIKEv2.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEVPNProtocolIKEv2.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEVPNProtocolIKEv2.h	2015-10-03 00:30:41.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEVPNProtocolIKEv2.h	2016-05-21 08:21:25.000000000 +0200
@@ -28,7 +28,7 @@
 	NEVPNIKEv2EncryptionAlgorithmAES128GCM NS_ENUM_AVAILABLE(10_11, 8_3) = 5,
 	/*! @const NEVPNIKEv2EncryptionAlgorithmAES256GCM Advanced Encryption Standard 256 bit (AES256GCM) */
 	NEVPNIKEv2EncryptionAlgorithmAES256GCM NS_ENUM_AVAILABLE(10_11, 8_3) = 6,
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} NS_ENUM_AVAILABLE(10_11, 8_0);
 
 /*!
  * @typedef NEVPNIKEv2IntegrityAlgorithm
@@ -45,7 +45,7 @@
 	NEVPNIKEv2IntegrityAlgorithmSHA384 = 4,
 	/*! @const NEVPNIKEv2IntegrityAlgorithmSHA512 SHA-2 512 bit */
 	NEVPNIKEv2IntegrityAlgorithmSHA512 = 5,
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} NS_ENUM_AVAILABLE(10_11, 8_0);
 
 /*!
  * @typedef NEVPNIKEv2DeadPeerDetectionRate
@@ -60,15 +60,15 @@
 	NEVPNIKEv2DeadPeerDetectionRateMedium = 2,
 	/*! @const NEVPNIKEv2DeadPeerDetectionRateHigh Run dead peer detection once every 1 minute. If the peer does not respond, retry 5 times at 1 second intervals before declaring the peer dead */
 	NEVPNIKEv2DeadPeerDetectionRateHigh = 3,
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} NS_ENUM_AVAILABLE(10_11, 8_0);
 
 /*!
  * @typedef NEVPNIKEv2DiffieHellmanGroup
  * @abstract IKEv2 Diffie Hellman groups
  */
 typedef NS_ENUM(NSInteger, NEVPNIKEv2DiffieHellmanGroup) {
-	/*! @const NEVPNIKEv2DiffieHellmanGroup0 Diffie Hellman group 0 */
-	NEVPNIKEv2DiffieHellmanGroup0 = 0,
+	/*! @const NEVPNIKEv2DiffieHellmanGroupInvalid Diffie Hellman group 0 is not a valid DH group*/
+	NEVPNIKEv2DiffieHellmanGroupInvalid = 0,
 	/*! @const NEVPNIKEv2DiffieHellmanGroup1 Diffie Hellman group 1 */
 	NEVPNIKEv2DiffieHellmanGroup1 = 1,
 	/*! @const NEVPNIKEv2DiffieHellmanGroup2 Diffie Hellman group 2 */
@@ -92,7 +92,7 @@
 	/*! @const NEVPNIKEv2DiffieHellmanGroup21 Diffie Hellman group 21 */
 	NEVPNIKEv2DiffieHellmanGroup21 = 21,
 	
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} NS_ENUM_AVAILABLE(10_11, 8_0);
 
 /*!
  * @typedef NEVPNIKEv2CertificateType
@@ -115,32 +115,32 @@
  *
  * Instances of this class are thread safe.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_11, 8_0)
 @interface NEVPNIKEv2SecurityAssociationParameters : NSObject <NSSecureCoding,NSCopying>
 
 /*!
  * @property encryptionAlgorithm
  * @discussion The algorithm used by the Security Association to encrypt and decrypt data. Default is NEVPNIKEv2EncryptionAlgorithm3DES.
  */
-@property NEVPNIKEv2EncryptionAlgorithm encryptionAlgorithm NS_AVAILABLE(10_10, 8_0);
+@property NEVPNIKEv2EncryptionAlgorithm encryptionAlgorithm NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property integrityAlgorithm
  * @discussion The algorithm used by the Security Association to verify the integrity of data. Default is NEVPNIKEv2IntegrityAlgorithmSHA96. The IKE psedo-random function algorithm will be inferred based on the integrity algorithm.
  */
-@property NEVPNIKEv2IntegrityAlgorithm integrityAlgorithm NS_AVAILABLE(10_10, 8_0);
+@property NEVPNIKEv2IntegrityAlgorithm integrityAlgorithm NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property diffieHellmanGroup
  * @discussion The Diffie Hellman group used by the Security Association. Default is NEVPNIKEv2DiffieHellmanGroup2.
  */
-@property NEVPNIKEv2DiffieHellmanGroup diffieHellmanGroup NS_AVAILABLE(10_10, 8_0);
+@property NEVPNIKEv2DiffieHellmanGroup diffieHellmanGroup NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property lifetimeMinutes
  * @discussion The life time of the Security Association, in minutes. Default is 60 for IKE Security Associations, and 30 for Child Security Associations. Before the lifetime is reached, IKEv2 will attempt to rekey the Security Association to maintain the connection.
  */
-@property int32_t lifetimeMinutes NS_AVAILABLE(10_10, 8_0);
+@property int32_t lifetimeMinutes NS_AVAILABLE(10_11, 8_0);
 
 @end
 
@@ -151,26 +151,26 @@
  * Instances of this class use IKE version 2 for key negotiation.
  * Instances of this class are thread safe.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_11, 8_0)
 @interface NEVPNProtocolIKEv2 : NEVPNProtocolIPSec
 
 /*!
  * @property deadPeerDetectionRate
  * @discussion How frequently the IKEv2 client will run the dead peer detection algorithm.  Default is NEVPNIKEv2DeadPeerDetectionRateMedium.
  */
-@property NEVPNIKEv2DeadPeerDetectionRate deadPeerDetectionRate NS_AVAILABLE(10_10, 8_0);
+@property NEVPNIKEv2DeadPeerDetectionRate deadPeerDetectionRate NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property serverCertificateIssuerCommonName
  * @discussion A string containing the Subject Common Name field of the Certificate Authority certificate that issued the IKEv2 server's certificate.
  */
-@property (copy, nullable) NSString *serverCertificateIssuerCommonName NS_AVAILABLE(10_10, 8_0);
+@property (copy, nullable) NSString *serverCertificateIssuerCommonName NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property serverCertificateCommonName
  * @discussion A string containing the value to verify in the IKEv2 server certificate's Subject Common Name field.
  */
-@property (copy, nullable) NSString *serverCertificateCommonName NS_AVAILABLE(10_10, 8_0);
+@property (copy, nullable) NSString *serverCertificateCommonName NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property certificateType
@@ -188,13 +188,13 @@
  * @property IKESecurityAssociationParameters
  * @discussion Parameters for the IKE SA
  */
-@property (readonly) NEVPNIKEv2SecurityAssociationParameters *IKESecurityAssociationParameters NS_AVAILABLE(10_10, 8_0);
+@property (readonly) NEVPNIKEv2SecurityAssociationParameters *IKESecurityAssociationParameters NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property childSecurityAssociationParameters
  * @discussion Parameters for the child SA
  */
-@property (readonly) NEVPNIKEv2SecurityAssociationParameters *childSecurityAssociationParameters NS_AVAILABLE(10_10, 8_0);
+@property (readonly) NEVPNIKEv2SecurityAssociationParameters *childSecurityAssociationParameters NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property disableMOBIKE
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEVPNProtocolIPSec.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEVPNProtocolIPSec.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEVPNProtocolIPSec.h	2015-10-03 00:30:41.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NEVPNProtocolIPSec.h	2016-05-21 08:21:25.000000000 +0200
@@ -22,7 +22,7 @@
 	NEVPNIKEAuthenticationMethodCertificate = 1,
 	/*! @const NEVPNIKEAuthenticationMethodSharedSecret Use a shared secret as the authentication credential */
 	NEVPNIKEAuthenticationMethodSharedSecret = 2,
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} NS_ENUM_AVAILABLE(10_11, 8_0);
 
 /*!
  * @interface NEVPNProtocolIPSec
@@ -30,14 +30,14 @@
  *
  * Instances of this class use IKE version 1 for key negotiation.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_11, 8_0)
 @interface NEVPNProtocolIPSec : NEVPNProtocol
 
 /*!
  * @property authenticationMethod
  * @discussion The method used to authenticate with the IPSec server. Note that if this property is set to NEVPNIKEAuthenticationMethodNone, extended authentication will still be negotiated if useExtendedAuthentication is set to YES.
  */
-@property NEVPNIKEAuthenticationMethod authenticationMethod NS_AVAILABLE(10_10, 8_0);
+@property NEVPNIKEAuthenticationMethod authenticationMethod NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property useExtendedAuthentication
@@ -45,25 +45,25 @@
  *   For IKE version 1, when this flag is set X-Auth authentication will be negotiated as part of the IKE session, using the username and password properties as the credential.
  *   For IKE version 2, when this flag is set EAP authentication will be negotiated as part of the IKE session, using the username, password, and/or identity properties as the credential depending on which EAP method the server requires.
  */
-@property BOOL useExtendedAuthentication NS_AVAILABLE(10_10, 8_0);
+@property BOOL useExtendedAuthentication NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property sharedSecretReference
  * @discussion A persistent reference to a keychain item of class kSecClassGenericPassword containing the IKE shared secret.
  */
-@property (copy, nullable) NSData *sharedSecretReference NS_AVAILABLE(10_10, 8_0);
+@property (copy, nullable) NSData *sharedSecretReference NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property localIdentifier
  * @discussion A string identifying the local IPSec endpoint for authentication purposes.
  */
-@property (copy, nullable) NSString *localIdentifier NS_AVAILABLE(10_10, 8_0);
+@property (copy, nullable) NSString *localIdentifier NS_AVAILABLE(10_11, 8_0);
 
 /*!
  * @property remoteIdentifier
  * @discussion A string identifying the remote IPSec endpoint for authentication purposes.
  */
-@property (copy, nullable) NSString *remoteIdentifier NS_AVAILABLE(10_10, 8_0);
+@property (copy, nullable) NSString *remoteIdentifier NS_AVAILABLE(10_11, 8_0);
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWBonjourServiceEndpoint.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWBonjourServiceEndpoint.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWBonjourServiceEndpoint.h	2015-10-03 00:30:41.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWBonjourServiceEndpoint.h	2016-05-21 08:21:25.000000000 +0200
@@ -1,23 +1,25 @@
 //
-//  NWBonjourService.h
+//  NWBonjourServiceEndpoint.h
 //  Network
 //
-//  Copyright (c) 2014, 2015 Apple. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
 #ifndef __NE_INDIRECT__
 #error "Please import the NetworkExtension module instead of this file directly."
-#endif
+#endif // __NE_INDIRECT__
+
+#ifndef __NWBonjourServiceEndpoint_h_
+#define __NWBonjourServiceEndpoint_h_
 
-NS_ASSUME_NONNULL_BEGIN
 
-@class NWEndpoint;
+NS_ASSUME_NONNULL_BEGIN
 
 /*!
  * @interface NWBonjourServiceEndpoint
- * @discussion NWBonjourServiceEndpoint is a subclass of NWEndpoint. It represents an endpoint 
- *		backed by a Bonjour service, specified with a name, type, and domain. For example, the 
- *		Bonjour service MyMusicStudio._music._tcp.local. has the name "MyMusicStudio", 
+ * @discussion NWBonjourServiceEndpoint is a subclass of NWEndpoint. It represents an endpoint
+ *		backed by a Bonjour service, specified with a name, type, and domain. For example, the
+ *		Bonjour service MyMusicStudio._music._tcp.local. has the name "MyMusicStudio",
  *		the type "_music._tcp", and the domain "local".
  */
 NS_CLASS_AVAILABLE(10_11, 9_0)
@@ -55,3 +57,5 @@
 @end
 
 NS_ASSUME_NONNULL_END
+
+#endif // __NWBonjourServiceEndpoint_h_
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWEndpoint.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWEndpoint.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWEndpoint.h	2015-10-03 00:30:41.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWEndpoint.h	2016-05-21 08:21:25.000000000 +0200
@@ -2,12 +2,16 @@
 //  NWEndpoint
 //  Network
 //
-//  Copyright (c) 2014, 2015 Apple. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
 #ifndef __NE_INDIRECT__
 #error "Please import the NetworkExtension module instead of this file directly."
-#endif
+#endif // __NE_INDIRECT__
+
+#ifndef __NWEndpoint_h_
+#define __NWEndpoint_h_
+
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -16,8 +20,10 @@
  * @discussion NWEndpoint is a generic class to represent network endpoints, such as a port on a remote server.
  */
 NS_CLASS_AVAILABLE(10_11, 9_0)
-@interface NWEndpoint : NSObject
+@interface NWEndpoint : NSObject <NSSecureCoding, NSCopying>
 
 @end
 
 NS_ASSUME_NONNULL_END
+
+#endif // __NWEndpoint_h_
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWHostEndpoint.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWHostEndpoint.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWHostEndpoint.h	2015-10-03 00:30:41.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWHostEndpoint.h	2016-05-21 08:21:25.000000000 +0200
@@ -2,20 +2,22 @@
 //  NWHostEndpoint.h
 //  Network
 //
-//  Copyright (c) 2014, 2015 Apple. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
 #ifndef __NE_INDIRECT__
 #error "Please import the NetworkExtension module instead of this file directly."
-#endif
+#endif // __NE_INDIRECT__
+
+#ifndef __NWHostEndpoint_h_
+#define __NWHostEndpoint_h_
 
-NS_ASSUME_NONNULL_BEGIN
 
-@class NWEndpoint;
+NS_ASSUME_NONNULL_BEGIN
 
 /*!
  * @interface NWHostEndpoint
- * @discussion NWHostEndpoint is a subclass of NWEndpoint. It represents an endpoint backed by a 
+ * @discussion NWHostEndpoint is a subclass of NWEndpoint. It represents an endpoint backed by a
  *		hostname and port. Note that a hostname string may be an IP or IPv6 address.
  */
 NS_CLASS_AVAILABLE(10_11, 9_0)
@@ -45,3 +47,5 @@
 @end
 
 NS_ASSUME_NONNULL_END
+
+#endif // __NWHostEndpoint_h_
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWPath.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWPath.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWPath.h	2015-10-03 00:30:41.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWPath.h	2016-05-21 08:21:25.000000000 +0200
@@ -2,12 +2,16 @@
 //  NWPath.h
 //  Network
 //
-//  Copyright (c) 2014, 2015 Apple. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
 #ifndef __NE_INDIRECT__
 #error "Please import the NetworkExtension module instead of this file directly."
-#endif
+#endif // __NE_INDIRECT__
+
+#ifndef __NWPath_h_
+#define __NWPath_h_
+
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -29,8 +33,8 @@
 
 /*!
  * @interface NWPath
- * @discussion A network path, represented with NWPath, expresses the viability status and 
- *		properties of the path that a networking connection will take on the device. For example, 
+ * @discussion A network path, represented with NWPath, expresses the viability status and
+ *		properties of the path that a networking connection will take on the device. For example,
  *		if the path status is NWPathStatusSatisfied, then a connection could use that path.
  */
 NS_CLASS_AVAILABLE(10_11, 9_0)
@@ -58,3 +62,5 @@
 @end
 
 NS_ASSUME_NONNULL_END
+
+#endif // __NWPath_h_
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWTCPConnection.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWTCPConnection.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWTCPConnection.h	2015-10-03 00:30:41.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWTCPConnection.h	2016-05-21 06:45:11.000000000 +0200
@@ -2,20 +2,20 @@
 //  NWTCPConnection.h
 //  Network
 //
-//  Copyright (c) 2014, 2015 Apple. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
 #ifndef __NE_INDIRECT__
 #error "Please import the NetworkExtension module instead of this file directly."
-#endif
+#endif // __NE_INDIRECT__
+
+#ifndef __NWTCPConnection_h_
+#define __NWTCPConnection_h_
 
 #import <Security/Security.h>
 
-NS_ASSUME_NONNULL_BEGIN
 
-@class NWEndpoint;
-@class NWPath;
-@class NWTCPConnection;
+NS_ASSUME_NONNULL_BEGIN
 
 /*!
  * @typedef NWTCPConnectionState
@@ -162,7 +162,7 @@
  * @param length The exact number of bytes the caller wants to read
  * @param completion The completion handler to be invoked when there is data to read or an error occurred
  */
-- (void)readLength:(NSUInteger)length completionHandler:(void (^)(NSData * __nullable data, NSError * __nullable error))completion NS_AVAILABLE(10_11, 9_0);
+- (void)readLength:(NSUInteger)length completionHandler:(void (^)(NSData *data, NSError * __nullable error))completion NS_AVAILABLE(10_11, 9_0);
 
 /*!
  * @method readMinimumLength:maximumLength:completionHandler:
@@ -189,7 +189,7 @@
  * @param maximum The maximum number of bytes the caller wants to read
  * @param completion The completion handler to be invoked when there is data to read or an error occurred
  */
-- (void)readMinimumLength:(NSUInteger)minimum maximumLength:(NSUInteger)maximum completionHandler:(void (^)(NSData * __nullable data, NSError * __nullable error))completion NS_AVAILABLE(10_11, 9_0);
+- (void)readMinimumLength:(NSUInteger)minimum maximumLength:(NSUInteger)maximum completionHandler:(void (^)(NSData *data, NSError * __nullable error))completion NS_AVAILABLE(10_11, 9_0);
 
 /*!
  * @method write:completionHandler:
@@ -280,3 +280,5 @@
 @end
 
 NS_ASSUME_NONNULL_END
+
+#endif // __NWTCPConnection_h_
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWTLSParameters.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWTLSParameters.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWTLSParameters.h	2015-10-03 00:30:41.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWTLSParameters.h	2016-05-21 08:21:25.000000000 +0200
@@ -1,13 +1,17 @@
 //
-//  NWUDPSession.h
-//  Network
+//  NWTLSParameters.h
+//  NetworkExtension
 //
-//  Copyright (c) 2015 Apple. All rights reserved.
+//  Copyright (c) 2015-2016 Apple. All rights reserved.
 //
 
 #ifndef __NE_INDIRECT__
 #error "Please import the NetworkExtension module instead of this file directly."
-#endif
+#endif // __NE_INDIRECT__
+
+#ifndef __NWTLSParameters_h_
+#define __NWTLSParameters_h_
+
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -46,3 +50,5 @@
 @end
 
 NS_ASSUME_NONNULL_END
+
+#endif // __NWTLSParameters_h_
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWUDPSession.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWUDPSession.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWUDPSession.h	2015-10-03 00:30:41.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWUDPSession.h	2016-05-21 08:21:25.000000000 +0200
@@ -2,17 +2,19 @@
 //  NWUDPSession.h
 //  Network
 //
-//  Copyright (c) 2014, 2015 Apple. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
 #ifndef __NE_INDIRECT__
 #error "Please import the NetworkExtension module instead of this file directly."
-#endif
+#endif // __NE_INDIRECT__
 
-NS_ASSUME_NONNULL_BEGIN
 
-@class NWEndpoint;
-@class NWPath;
+#ifndef __NWUDPSession_h_
+#define __NWUDPSession_h_
+
+
+NS_ASSUME_NONNULL_BEGIN
 
 /*!
  * @typedef NWUDPSessionState
@@ -50,7 +52,7 @@
  * @discussion This convenience initializer can be used to create a new session based on the
  *		original session's endpoint and parameters.
  *
- *		The application should create an NWUDPSession and watch the "hasBetterPath" property. 
+ *		The application should create an NWUDPSession and watch the "hasBetterPath" property.
  *		When this property is YES, it should call initWithUpgradeForSession: to create a new
  *		session, with the goal to start transferring data on the new better path as soon as
  *		possible to reduce power and potentially monetary cost. When the new "upgrade" session
@@ -65,9 +67,9 @@
 
 /*!
  * @property state
- * @discussion The current state of the UDP session. If the state is NWUDPSessionStateReady, 
+ * @discussion The current state of the UDP session. If the state is NWUDPSessionStateReady,
  *		then the connection is eligible for reading and writing. The state will be
- *		NWUDPSessionStateFailed if the endpoint could not be resolved, or all endpoints have been 
+ *		NWUDPSessionStateFailed if the endpoint could not be resolved, or all endpoints have been
  *		rejected. Use KVO to watch for changes.
  */
 @property (readonly) NWUDPSessionState state NS_AVAILABLE(10_11, 9_0);
@@ -86,14 +88,14 @@
 
 /*!
  * @property viable
- * @discussion YES if the connection can read and write data, NO otherwise. 
+ * @discussion YES if the connection can read and write data, NO otherwise.
  *		Use KVO to watch this property.
  */
 @property (readonly, getter=isViable) BOOL viable NS_AVAILABLE(10_11, 9_0);
 
 /*!
  * @property hasBetterPath
- * @discussion YES if there is another path available that is preferred over the currentPath. 
+ * @discussion YES if there is another path available that is preferred over the currentPath.
  *		To take advantage of this path, create a new UDPSession. Use KVO to watch for changes.
  */
 @property (readonly) BOOL hasBetterPath NS_AVAILABLE(10_11, 9_0);
@@ -106,7 +108,7 @@
 
 /*!
  * @method tryNextResolvedEndpoint
- * @discussion Mark the current value of resolvedEndpoint as unusable, and try to switch to the 
+ * @discussion Mark the current value of resolvedEndpoint as unusable, and try to switch to the
  *		next available endpoint. This should be used when the caller has attempted to communicate
  *		with the current resolvedEndpoint, and the caller has determined that it is unusable. If
  *		there are no other resolved endpoints, the session will move to the failed state.
@@ -117,7 +119,7 @@
  * @property maximumDatagramLength
  * @discussion The maximum size of a datagram to be written currently. If a datagram is written
  *		with a longer length, the datagram may be fragmented or encounter an error. Note that this
- *		value is not guaranteed to be the maximum datagram length for end-to-end communication 
+ *		value is not guaranteed to be the maximum datagram length for end-to-end communication
  *		across the network. Use KVO to watch for changes.
  */
 @property (readonly) NSUInteger maximumDatagramLength NS_AVAILABLE(10_11, 9_0);
@@ -129,7 +131,7 @@
  * @param handler A handler called when datagrams have been read, or when an error has occurred.
  * @param minDatagrams The maximum number of datagrams to send to the handler.
  */
-- (void)setReadHandler:(void (^)(NSArray<NSData *> * __nullable datagrams, NSError * __nullable error))handler
+- (void)setReadHandler:(void (^)(NSArray<NSData *> *datagrams, NSError * __nullable error))handler
 		  maxDatagrams:(NSUInteger)maxDatagrams NS_AVAILABLE(10_11, 9_0);
 
 /*!
@@ -162,3 +164,5 @@
 @end
 
 NS_ASSUME_NONNULL_END
+
+#endif // __NWUDPSession_h_

```