#CoreWLAN.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreWLAN.framework/Headers/CWNetworkProfile.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreWLAN.framework/Headers/CWNetworkProfile.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreWLAN.framework/Headers/CWNetworkProfile.h	2015-08-23 01:25:42.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreWLAN.framework/Headers/CWNetworkProfile.h	2016-05-26 02:10:12.000000000 +0200
@@ -60,6 +60,8 @@
     NSInteger       _roamingProfileType;
     
     BOOL            _isPersonalHotspot;
+    
+    NSArray         *_bssidList;
 }
 
 /*!
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreWLAN.framework/Headers/CWWiFiClient.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreWLAN.framework/Headers/CWWiFiClient.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreWLAN.framework/Headers/CWWiFiClient.h	2015-08-23 01:25:42.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreWLAN.framework/Headers/CWWiFiClient.h	2016-05-26 02:10:12.000000000 +0200
@@ -111,6 +111,39 @@
  * The name of the Wi-Fi interface.
  *
  * @abstract
+ * Invoked when any state of WiFi virtual interface changes.
+ *
+ * @discussion
+ * Use -[CWWiFiClient startMonitoringEventWithType:error:] with the CWEventTypeVirtualInterfaceStateChanged event type
+ * to register for virtual interface state changed notifications.
+ */
+- (void)virtualInterfaceStateChangedForWiFiInterfaceWithName:(NSString *)interfaceName;
+
+/*!
+ * @method
+ *
+ * @param interfaceName
+ * The name of the Wi-Fi interface.
+ *
+ * @param rangingData
+ * Dictionary containing distance measurement data.
+ *
+ * @abstract
+ * Invoked when WiFi ranging measurement completed.
+ *
+ * @discussion
+ * Use -[CWWiFiClient startMonitoringEventWithType:error:] with the CWEventTypeRangingReportEvent event type
+ * to register for ranging event notifications.
+ */
+- (void)rangingReportEventForWiFiInterfaceWithName:(NSString *)interfaceName data:(NSArray *)rangingData error:(NSError *)err;
+
+/*!
+ * @method
+ *
+ * @param interfaceName
+ * The name of the Wi-Fi interface.
+ *
+ * @abstract
  * Invoked when the Wi-Fi link state changes.
  *
  * @discussion
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreWLAN.framework/Headers/CoreWLANTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreWLAN.framework/Headers/CoreWLANTypes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CoreWLAN.framework/Headers/CoreWLANTypes.h	2015-08-23 01:25:42.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreWLAN.framework/Headers/CoreWLANTypes.h	2016-05-26 02:10:12.000000000 +0200
@@ -402,6 +402,9 @@
  * @constant CWEventTypeCountryCodeDidChange
  * Posted when the adopted country code of any Wi-Fi interface changes.
  *
+ * @constant CWEventTypeVirtualInterfaceStateChanged
+ * Posted when any state of any Wi-Fi virtual interface changes.
+ *
  * @constant CWEventTypeLinkDidChange 
  * Posted when the link state for any Wi-Fi interface changes.
  *
@@ -414,6 +417,9 @@
  * @constant CWEventTypeScanCacheUpdated
  * Posted when the scan cache of any Wi-Fi interface is updated with new scan results.
  *
+ * @constant CWEventTypeRangingEvent
+ * Posted when WiFi ranging measurement completed.
+ *
  * @constant CWEventTypeUnknown
  * Unknown event type.
  */
@@ -428,6 +434,8 @@
     CWEventTypeLinkQualityDidChange     = 6,
     CWEventTypeModeDidChange            = 7,
     CWEventTypeScanCacheUpdated         = 8,
+    CWEventTypeVirtualInterfaceStateChanged = 9,
+    CWEventTypeRangingReportEvent       = 10,
     CWEventTypeUnknown                  = NSIntegerMax,
 } NS_ENUM_AVAILABLE_MAC(10_10);
 

```