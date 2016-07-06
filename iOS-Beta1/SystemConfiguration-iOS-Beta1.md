#SystemConfiguration.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/CaptiveNetwork.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/CaptiveNetwork.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/CaptiveNetwork.h	2015-10-02 23:28:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/CaptiveNetwork.h	2016-05-23 06:45:52.000000000 +0200
@@ -1,5 +1,5 @@
 /*
- * Copyright (c) 2009-2015 Apple Inc. All rights reserved.
+ * Copyright (c) 2009-2016 Apple Inc. All rights reserved.
  *
  * @APPLE_LICENSE_HEADER_START@
  * 
@@ -51,22 +51,8 @@
 		These APIs are treated as advisory only.
 		There is no guarantee or contract that the operating system
 		will take the intended action.
-
-	@note IMPORTANT: This API is deprecated starting in iOS 9.
-		For captive network applications, this has been completely
-		replaced by <NetworkExtension/NEHotspotHelper.h>.
-		For other applications, there is no direct replacement.
-		Please file a bug describing your use of this API so that
-		we can consider your requirements as this situation evolves.
  */
 
-#define CN_DEPRECATION_NOTICE						\
-    "For captive network applications, this has been completely "	\
-    "replaced by <NetworkExtension/NEHotspotHelper.h>. "		\
-    "For other applications, there is no direct replacement. "		\
-    "Please file a bug describing your use of this API to that "	\
-    "we can consider your requirements as this situation evolves."
-
 __BEGIN_DECLS
 
 /*!
@@ -129,37 +115,25 @@
 	 You MUST release the returned value.
  */
 CFArrayRef __nullable
-CNCopySupportedInterfaces	(void)
-    __OSX_AVAILABLE_BUT_DEPRECATED_MSG(__MAC_10_8, __MAC_NA,
-				       __IPHONE_4_1, __IPHONE_9_0,
-				       CN_DEPRECATION_NOTICE);
+CNCopySupportedInterfaces	(void)			__OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_4_1);
 
 /*!
  @constant kCNNetworkInfoKeySSIDData
  @discussion NetworkInfo Dictionary key for SSID in CFData format
  */
-extern const CFStringRef kCNNetworkInfoKeySSIDData
-    __OSX_AVAILABLE_BUT_DEPRECATED_MSG(__MAC_NA, __MAC_NA,
-				       __IPHONE_4_1, __IPHONE_9_0,
-				       CN_DEPRECATION_NOTICE);
+extern const CFStringRef kCNNetworkInfoKeySSIDData	__OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_4_1);
 
 /*!
  @constant kCNNetworkInfoKeySSID
  @discussion NetworkInfo Dictionary key for SSID in CFString format
  */
-extern const CFStringRef kCNNetworkInfoKeySSID
-    __OSX_AVAILABLE_BUT_DEPRECATED_MSG(__MAC_NA, __MAC_NA,
-				       __IPHONE_4_1, __IPHONE_9_0,
-				       CN_DEPRECATION_NOTICE);
+extern const CFStringRef kCNNetworkInfoKeySSID		__OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_4_1);
 
 /*!
  @constant kCNNetworkInfoKeyBSSID
  @discussion NetworkInfo Dictionary key for BSSID in CFString format
  */
-extern const CFStringRef kCNNetworkInfoKeyBSSID
-    __OSX_AVAILABLE_BUT_DEPRECATED_MSG(__MAC_NA, __MAC_NA,
-				       __IPHONE_4_1, __IPHONE_9_0,
-				       CN_DEPRECATION_NOTICE);
+extern const CFStringRef kCNNetworkInfoKeyBSSID		__OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_4_1);
 
 /*!
  @function CNCopyCurrentNetworkInfo
@@ -181,10 +155,7 @@
 	 You MUST release the returned value.
  */
 CFDictionaryRef __nullable
-CNCopyCurrentNetworkInfo	(CFStringRef interfaceName)
-    __OSX_AVAILABLE_BUT_DEPRECATED_MSG(__MAC_NA, __MAC_NA,
-				       __IPHONE_4_1, __IPHONE_9_0,
-				       CN_DEPRECATION_NOTICE);
+CNCopyCurrentNetworkInfo	(CFStringRef interfaceName)	__OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_4_1);
 
 __END_DECLS
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/SCNetwork.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/SCNetwork.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/SCNetwork.h	2015-10-02 23:28:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/SCNetwork.h	2016-05-23 06:27:05.000000000 +0200
@@ -125,8 +125,8 @@
 		Note: this API has been deprecated but you can
 		      get equivalent results with :
 <pre>
-	SCNetworkReachabiltyRef   target;
-	SCNetworkReachabiltyFlags flags = 0;
+	SCNetworkReachabilityRef   target;
+	SCNetworkReachabilityFlags flags = 0;
 	Boolean                   ok;
 
 	target = SCNetworkReachabilityCreateWithAddress(NULL, address);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/SCNetworkConfiguration.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/SCNetworkConfiguration.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/SCNetworkConfiguration.h	2015-10-02 23:28:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/SCNetworkConfiguration.h	2016-05-23 06:45:52.000000000 +0200
@@ -1,5 +1,5 @@
 /*
- * Copyright (c) 2004-2011, 2015 Apple Inc. All rights reserved.
+ * Copyright (c) 2004-2011, 2015, 2016 Apple Inc. All rights reserved.
  *
  * @APPLE_LICENSE_HEADER_START@
  * 
@@ -123,7 +123,7 @@
 /*!
 	@const kSCNetworkInterfaceTypePPTP
  */
-extern const CFStringRef kSCNetworkInterfaceTypePPTP						__OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_NA);
+extern const CFStringRef kSCNetworkInterfaceTypePPTP						__OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_4,__MAC_10_12,__IPHONE_NA,__IPHONE_NA);
 
 /*!
 	@const kSCNetworkInterfaceTypeSerial
@@ -238,11 +238,6 @@
 /* network "protocol" types */
 
 /*!
-	@const kSCNetworkProtocolTypeAppleTalk
- */
-extern const CFStringRef kSCNetworkProtocolTypeAppleTalk					__OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_4,__MAC_10_6,__IPHONE_NA,__IPHONE_NA);
-
-/*!
 	@const kSCNetworkProtocolTypeDNS
  */
 extern const CFStringRef kSCNetworkProtocolTypeDNS						__OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_NA);
@@ -447,7 +442,7 @@
  */
 Boolean
 SCNetworkInterfaceSetConfiguration		(SCNetworkInterfaceRef		interface,
-						 CFDictionaryRef		config)		__OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_NA);
+						 CFDictionaryRef __nullable	config)		__OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_NA);
 
 /*!
 	@function SCNetworkInterfaceSetExtendedConfiguration
@@ -459,7 +454,7 @@
 Boolean
 SCNetworkInterfaceSetExtendedConfiguration	(SCNetworkInterfaceRef		interface,
 						 CFStringRef			extendedType,
-						 CFDictionaryRef		config)		__OSX_AVAILABLE_STARTING(__MAC_10_5,__IPHONE_NA);
+						 CFDictionaryRef __nullable	config)		__OSX_AVAILABLE_STARTING(__MAC_10_5,__IPHONE_NA);
 
 #pragma mark -
 
@@ -907,7 +902,7 @@
  */
 Boolean
 SCNetworkProtocolSetConfiguration		(SCNetworkProtocolRef		protocol,
-						 CFDictionaryRef		config)		__OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_NA);
+						 CFDictionaryRef __nullable	config)		__OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_NA);
 
 /*!
 	@function SCNetworkProtocolSetEnabled
@@ -1107,7 +1102,7 @@
  */
 Boolean
 SCNetworkServiceSetName				(SCNetworkServiceRef		service,
-						 CFStringRef			name)		__OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_NA);
+						 CFStringRef __nullable		name)		__OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_NA);
 
 
 /* --------------------------------------------------------------------------------
@@ -1285,7 +1280,7 @@
  */
 Boolean
 SCNetworkSetSetName				(SCNetworkSetRef		set,
-						 CFStringRef			name)		__OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_NA);
+						 CFStringRef __nullable		name)		__OSX_AVAILABLE_STARTING(__MAC_10_4,__IPHONE_NA);
 
 /*!
 	@function SCNetworkSetSetServiceOrder
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/SCNetworkReachability.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/SCNetworkReachability.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/SCNetworkReachability.h	2015-10-02 23:28:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/SCNetworkReachability.h	2016-05-23 06:27:05.000000000 +0200
@@ -1,15 +1,15 @@
 /*
- * Copyright (c) 2003-2005, 2008-2010, 2015 Apple Inc. All rights reserved.
+ * Copyright (c) 2003-2005, 2008-2010, 2015-2016 Apple Inc. All rights reserved.
  *
  * @APPLE_LICENSE_HEADER_START@
- * 
+ *
  * This file contains Original Code and/or Modifications of Original Code
  * as defined in and that are subject to the Apple Public Source License
  * Version 2.0 (the 'License'). You may not use this file except in
  * compliance with the License. Please obtain a copy of the License at
  * http://www.opensource.apple.com/apsl/ and read it before using this
  * file.
- * 
+ *
  * The Original Code and all software distributed under the License are
  * distributed on an 'AS IS' basis, WITHOUT WARRANTY OF ANY KIND, EITHER
  * EXPRESS OR IMPLIED, AND APPLE HEREBY DISCLAIMS ALL SUCH WARRANTIES,
@@ -17,7 +17,7 @@
  * FITNESS FOR A PARTICULAR PURPOSE, QUIET ENJOYMENT OR NON-INFRINGEMENT.
  * Please see the License for the specific language governing rights and
  * limitations under the License.
- * 
+ *
  * @APPLE_LICENSE_HEADER_END@
  */
 
@@ -49,6 +49,22 @@
 		computer.
 		Note that reachability does <i>not</i> guarantee that the data
 		packet will actually be received by the host.
+ 
+		When reachability is used without scheduling updates on a runloop
+		or dispatch queue, the system will not generate DNS traffic and
+		will be optimistic about its reply - it will assume that the target
+		is reachable if there is a default route but a DNS query is
+		needed to learn the address. When scheduled, the first callback
+		will behave like an unscheduled call but subsequent calls will
+		leverage DNS results.
+ 
+		When used on IPv6-only (NAT64+DNS64) networks, reachability checks
+		for IPv4 address literals (either a struct sockaddr_in * or textual
+		representations such as "192.0.2.1") will automatically give the
+		result for the corresponding synthesized IPv6 address.
+		On those networks, creating a CFSocketStream or NSURLSession
+		to that address will send packets but trying to connect using
+		BSD socket APIs will fail.
  */
 
 /*!
@@ -323,12 +339,13 @@
 
 /*!
 	@function SCNetworkReachabilitySetDispatchQueue
-	@discussion Schedules callbacks for the given target on the given
+	@discussion Schedule or unschedule callbacks for the given target on the given
 		dispatch queue.
 	@param target The address or name that is set up for asynchronous
 		notifications.  Must be non-NULL.
-	@param queue A libdispatch queue to run the callback on. Pass NULL to disable notifications, and release queue.
-	@result Returns TRUE if the target is unscheduled successfully;
+	@param queue A libdispatch queue to run the callback on. 
+		Pass NULL to unschedule callbacks.
+	@result Returns TRUE if the target is scheduled or unscheduled successfully;
 		FALSE otherwise.
  */
 Boolean
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/SCPreferencesSetSpecific.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/SCPreferencesSetSpecific.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/SCPreferencesSetSpecific.h	2015-10-02 23:28:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/SCPreferencesSetSpecific.h	2016-05-23 06:27:23.000000000 +0200
@@ -65,7 +65,7 @@
 Boolean
 SCPreferencesSetComputerName		(
 					SCPreferencesRef	prefs,
-					CFStringRef		name,
+					CFStringRef __nullable	name,
 					CFStringEncoding	nameEncoding
 					)			__OSX_AVAILABLE_STARTING(__MAC_10_1,__IPHONE_NA);
 
@@ -87,7 +87,7 @@
 Boolean
 SCPreferencesSetLocalHostName		(
 					SCPreferencesRef	prefs,
-					CFStringRef		name
+					CFStringRef __nullable	name
 					)			__OSX_AVAILABLE_STARTING(__MAC_10_2,__IPHONE_NA);
 
 __END_DECLS
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/SCSchemaDefinitions.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/SCSchemaDefinitions.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/SCSchemaDefinitions.h	2015-10-02 23:28:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SystemConfiguration.framework/Headers/SCSchemaDefinitions.h	2016-05-23 06:27:23.000000000 +0200
@@ -1,5 +1,5 @@
 /*
- * Copyright (c) 2000-2015 Apple Inc. All rights reserved.
+ * Copyright (c) 2000-2016 Apple Inc. All rights reserved.
  *
  * @APPLE_LICENSE_HEADER_START@
  *
@@ -326,10 +326,6 @@
  *
  *   * RESERVED FOR FUTURE USE *
  *
- * kSCEntNetPPTP Entity Keys
- *
- *   * RESERVED FOR FUTURE USE *
- *
  * kSCEntNetL2TP Entity Keys
  *
  *   kSCPropNetL2TPIPSecSharedSecret                    "IPSecSharedSecret"            CFString
@@ -570,13 +566,6 @@
 #define kSCEntNetAirPort kSCEntNetAirPort
 
 /*!
-  @const kSCEntNetAppleTalk
-  @discussion Value is a CFDictionary
- */
-extern const CFStringRef kSCEntNetAppleTalk                                 __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_6,__IPHONE_NA,__IPHONE_NA);
-#define kSCEntNetAppleTalk kSCEntNetAppleTalk
-
-/*!
   @const kSCEntNetDHCP
   @discussion Value is a CFDictionary
  */
@@ -654,13 +643,6 @@
 #define kSCEntNetModem kSCEntNetModem
 
 /*!
-  @const kSCEntNetNetInfo
-  @discussion Value is a CFDictionary
- */
-extern const CFStringRef kSCEntNetNetInfo                                   __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_5,__IPHONE_NA,__IPHONE_NA);
-#define kSCEntNetNetInfo kSCEntNetNetInfo
-
-/*!
   @const kSCEntNetPPP
   @discussion Value is a CFDictionary
  */
@@ -685,7 +667,7 @@
   @const kSCEntNetPPTP
   @discussion Value is a CFDictionary
  */
-extern const CFStringRef kSCEntNetPPTP                                      __OSX_AVAILABLE_STARTING(__MAC_10_3,__IPHONE_NA);
+extern const CFStringRef kSCEntNetPPTP                                      __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_3,__MAC_10_12,__IPHONE_NA,__IPHONE_NA);
 #define kSCEntNetPPTP kSCEntNetPPTP
 
 /*!
@@ -846,91 +828,6 @@
 #define kSCValNetAirPortAuthPasswordEncryptionKeychain kSCValNetAirPortAuthPasswordEncryptionKeychain
 
 /*!
-  @group kSCEntNetAppleTalk Entity Keys
- */
-
-/*!
-  @const kSCPropNetAppleTalkComputerName
-  @discussion Value is a CFString
- */
-extern const CFStringRef kSCPropNetAppleTalkComputerName                    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_6,__IPHONE_NA,__IPHONE_NA);
-#define kSCPropNetAppleTalkComputerName kSCPropNetAppleTalkComputerName
-
-/*!
-  @const kSCPropNetAppleTalkComputerNameEncoding
-  @discussion Value is a CFNumber
- */
-extern const CFStringRef kSCPropNetAppleTalkComputerNameEncoding            __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_6,__IPHONE_NA,__IPHONE_NA);
-#define kSCPropNetAppleTalkComputerNameEncoding kSCPropNetAppleTalkComputerNameEncoding
-
-/*!
-  @const kSCPropNetAppleTalkConfigMethod
-  @discussion Value is a CFString
- */
-extern const CFStringRef kSCPropNetAppleTalkConfigMethod                    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_6,__IPHONE_NA,__IPHONE_NA);
-#define kSCPropNetAppleTalkConfigMethod kSCPropNetAppleTalkConfigMethod
-
-/*!
-  @const kSCPropNetAppleTalkDefaultZone
-  @discussion Value is a CFString
- */
-extern const CFStringRef kSCPropNetAppleTalkDefaultZone                     __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_6,__IPHONE_NA,__IPHONE_NA);
-#define kSCPropNetAppleTalkDefaultZone kSCPropNetAppleTalkDefaultZone
-
-/*!
-  @const kSCPropNetAppleTalkNetworkID
-  @discussion Value is a CFNumber
- */
-extern const CFStringRef kSCPropNetAppleTalkNetworkID                       __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_6,__IPHONE_NA,__IPHONE_NA);
-#define kSCPropNetAppleTalkNetworkID kSCPropNetAppleTalkNetworkID
-
-/*!
-  @const kSCPropNetAppleTalkNetworkRange
-  @discussion Value is a CFArray[CFNumber]
- */
-extern const CFStringRef kSCPropNetAppleTalkNetworkRange                    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_2,__MAC_10_6,__IPHONE_NA,__IPHONE_NA);
-#define kSCPropNetAppleTalkNetworkRange kSCPropNetAppleTalkNetworkRange
-
-/*!
-  @const kSCPropNetAppleTalkNodeID
-  @discussion Value is a CFNumber
- */
-extern const CFStringRef kSCPropNetAppleTalkNodeID                          __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_6,__IPHONE_NA,__IPHONE_NA);
-#define kSCPropNetAppleTalkNodeID kSCPropNetAppleTalkNodeID
-
-/*!
-  @const kSCPropNetAppleTalkSeedNetworkRange
-  @discussion Value is a CFArray[CFNumber]
- */
-extern const CFStringRef kSCPropNetAppleTalkSeedNetworkRange                __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_6,__IPHONE_NA,__IPHONE_NA);
-#define kSCPropNetAppleTalkSeedNetworkRange kSCPropNetAppleTalkSeedNetworkRange
-
-/*!
-  @const kSCPropNetAppleTalkSeedZones
-  @discussion Value is a CFArray[CFString]
- */
-extern const CFStringRef kSCPropNetAppleTalkSeedZones                       __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_6,__IPHONE_NA,__IPHONE_NA);
-#define kSCPropNetAppleTalkSeedZones kSCPropNetAppleTalkSeedZones
-
-/*!
-  @const kSCValNetAppleTalkConfigMethodNode
- */
-extern const CFStringRef kSCValNetAppleTalkConfigMethodNode                 __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_6,__IPHONE_NA,__IPHONE_NA);
-#define kSCValNetAppleTalkConfigMethodNode kSCValNetAppleTalkConfigMethodNode
-
-/*!
-  @const kSCValNetAppleTalkConfigMethodRouter
- */
-extern const CFStringRef kSCValNetAppleTalkConfigMethodRouter               __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_6,__IPHONE_NA,__IPHONE_NA);
-#define kSCValNetAppleTalkConfigMethodRouter kSCValNetAppleTalkConfigMethodRouter
-
-/*!
-  @const kSCValNetAppleTalkConfigMethodSeedRouter
- */
-extern const CFStringRef kSCValNetAppleTalkConfigMethodSeedRouter           __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_6,__IPHONE_NA,__IPHONE_NA);
-#define kSCValNetAppleTalkConfigMethodSeedRouter kSCValNetAppleTalkConfigMethodSeedRouter
-
-/*!
   @group kSCEntNetDNS Entity Keys
  */
 
@@ -1117,7 +1014,7 @@
 /*!
   @const kSCValNetInterfaceSubTypePPTP
  */
-extern const CFStringRef kSCValNetInterfaceSubTypePPTP                      __OSX_AVAILABLE_STARTING(__MAC_10_2,__IPHONE_NA);
+extern const CFStringRef kSCValNetInterfaceSubTypePPTP                      __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_2,__MAC_10_12,__IPHONE_NA,__IPHONE_NA);
 #define kSCValNetInterfaceSubTypePPTP kSCValNetInterfaceSubTypePPTP
 
 /*!
@@ -1619,62 +1516,6 @@
 #define kSCValNetModemDialModeWaitForDialTone kSCValNetModemDialModeWaitForDialTone
 
 /*!
-  @group kSCEntNetNetInfo Entity Keys
- */
-
-/*!
-  @const kSCPropNetNetInfoBindingMethods
-  @discussion Value is a CFString
- */
-extern const CFStringRef kSCPropNetNetInfoBindingMethods                    __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_5,__IPHONE_NA,__IPHONE_NA);
-#define kSCPropNetNetInfoBindingMethods kSCPropNetNetInfoBindingMethods
-
-/*!
-  @const kSCPropNetNetInfoServerAddresses
-  @discussion Value is a CFArray[CFString]
- */
-extern const CFStringRef kSCPropNetNetInfoServerAddresses                   __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_5,__IPHONE_NA,__IPHONE_NA);
-#define kSCPropNetNetInfoServerAddresses kSCPropNetNetInfoServerAddresses
-
-/*!
-  @const kSCPropNetNetInfoServerTags
-  @discussion Value is a CFArray[CFString]
- */
-extern const CFStringRef kSCPropNetNetInfoServerTags                        __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_5,__IPHONE_NA,__IPHONE_NA);
-#define kSCPropNetNetInfoServerTags kSCPropNetNetInfoServerTags
-
-/*!
-  @const kSCPropNetNetInfoBroadcastServerTag
-  @discussion Value is a CFString
- */
-extern const CFStringRef kSCPropNetNetInfoBroadcastServerTag                __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_5,__IPHONE_NA,__IPHONE_NA);
-#define kSCPropNetNetInfoBroadcastServerTag kSCPropNetNetInfoBroadcastServerTag
-
-/*!
-  @const kSCValNetNetInfoBindingMethodsBroadcast
- */
-extern const CFStringRef kSCValNetNetInfoBindingMethodsBroadcast            __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_5,__IPHONE_NA,__IPHONE_NA);
-#define kSCValNetNetInfoBindingMethodsBroadcast kSCValNetNetInfoBindingMethodsBroadcast
-
-/*!
-  @const kSCValNetNetInfoBindingMethodsDHCP
- */
-extern const CFStringRef kSCValNetNetInfoBindingMethodsDHCP                 __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_5,__IPHONE_NA,__IPHONE_NA);
-#define kSCValNetNetInfoBindingMethodsDHCP kSCValNetNetInfoBindingMethodsDHCP
-
-/*!
-  @const kSCValNetNetInfoBindingMethodsManual
- */
-extern const CFStringRef kSCValNetNetInfoBindingMethodsManual               __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_5,__IPHONE_NA,__IPHONE_NA);
-#define kSCValNetNetInfoBindingMethodsManual kSCValNetNetInfoBindingMethodsManual
-
-/*!
-  @const kSCValNetNetInfoDefaultServerTag
- */
-extern const CFStringRef kSCValNetNetInfoDefaultServerTag                   __OSX_AVAILABLE_BUT_DEPRECATED(__MAC_10_1,__MAC_10_5,__IPHONE_NA,__IPHONE_NA);
-#define kSCValNetNetInfoDefaultServerTag kSCValNetNetInfoDefaultServerTag
-
-/*!
   @group kSCEntNetPPP Entity Keys
  */
 
@@ -2091,10 +1932,6 @@
  */
 
 /*!
-  @group kSCEntNetPPTP Entity Keys
- */
-
-/*!
   @group kSCEntNetL2TP Entity Keys
  */
 

```