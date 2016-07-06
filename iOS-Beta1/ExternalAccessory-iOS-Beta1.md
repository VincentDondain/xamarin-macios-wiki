#ExternalAccessory.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ExternalAccessory.framework/Headers/EAWiFiUnconfiguredAccessoryBrowser.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ExternalAccessory.framework/Headers/EAWiFiUnconfiguredAccessoryBrowser.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ExternalAccessory.framework/Headers/EAWiFiUnconfiguredAccessoryBrowser.h	2015-10-03 02:21:02.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ExternalAccessory.framework/Headers/EAWiFiUnconfiguredAccessoryBrowser.h	2016-05-25 05:19:30.000000000 +0200
@@ -104,7 +104,7 @@
  * @return Instance object
  *
  */
-- (instancetype)initWithDelegate:(nullable id<EAWiFiUnconfiguredAccessoryBrowserDelegate>)delegate queue:(nullable dispatch_queue_t)queue NS_DESIGNATED_INITIALIZER NS_AVAILABLE(NA, 8_0);
+- (instancetype)initWithDelegate:(nullable id<EAWiFiUnconfiguredAccessoryBrowserDelegate>)delegate queue:(nullable dispatch_queue_t)queue __IOS_AVAILABLE(8.0) __OSX_UNAVAILABLE __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
 
 /*!
  * @brief Start the search for unconfigured accessories
@@ -116,13 +116,13 @@
  * @param predicate The desired filter for unconfigured accessory results conforming to the EAWiFiUnconfiguredAccessory protocol.
  *
  */
-- (void)startSearchingForUnconfiguredAccessoriesMatchingPredicate:(nullable NSPredicate *)predicate NS_AVAILABLE(NA, 8_0);
+- (void)startSearchingForUnconfiguredAccessoriesMatchingPredicate:(nullable NSPredicate *)predicate __IOS_AVAILABLE(8.0) __OSX_UNAVAILABLE __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
 
 /*!
  * @brief Stop the search for unconfigured MFi Wireless Accessory Configuration accessories
  *
  */
-- (void)stopSearchingForUnconfiguredAccessories NS_AVAILABLE(NA, 8_0);
+- (void)stopSearchingForUnconfiguredAccessories __IOS_AVAILABLE(8.0) __OSX_UNAVAILABLE __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
 
 /*!
  * @brief Begin the configuration process for the chosen accessory
@@ -136,7 +136,7 @@
  * @param viewController The UIViewController that will host the Apple guided setup UI in the host application.
  *
  */
-- (void)configureAccessory:(EAWiFiUnconfiguredAccessory *)accessory withConfigurationUIOnViewController:(UIViewController *)viewController NS_AVAILABLE(NA, 8_0);
+- (void)configureAccessory:(EAWiFiUnconfiguredAccessory *)accessory withConfigurationUIOnViewController:(UIViewController *)viewController __IOS_AVAILABLE(8.0) __OSX_UNAVAILABLE __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
 
 @end
 
@@ -162,7 +162,7 @@
  *  @param state   The current state of the EAWiFiUnconfiguredAccessoryBrowser.
  *
  */
-- (void)accessoryBrowser:(EAWiFiUnconfiguredAccessoryBrowser *)browser didUpdateState:(EAWiFiUnconfiguredAccessoryBrowserState)state NS_AVAILABLE(NA, 8_0);
+- (void)accessoryBrowser:(EAWiFiUnconfiguredAccessoryBrowser *)browser didUpdateState:(EAWiFiUnconfiguredAccessoryBrowserState)state __IOS_AVAILABLE(8.0) __OSX_UNAVAILABLE __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
 
 /*!
  *  @method accessoryBrowser:didFindUnconfiguredAccessories:
@@ -174,7 +174,7 @@
  *  @param accessories The set of EAWiFiUnconfiguredAccessory objects that have been found since the last update.
  *
  */
-- (void)accessoryBrowser:(EAWiFiUnconfiguredAccessoryBrowser *)browser didFindUnconfiguredAccessories:(NSSet<EAWiFiUnconfiguredAccessory *> *)accessories NS_AVAILABLE(NA, 8_0);
+- (void)accessoryBrowser:(EAWiFiUnconfiguredAccessoryBrowser *)browser didFindUnconfiguredAccessories:(NSSet<EAWiFiUnconfiguredAccessory *> *)accessories __IOS_AVAILABLE(8.0) __OSX_UNAVAILABLE __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
 
 /*!
  *  @method accessoryBrowser:didRemoveUnconfiguredAccessories:
@@ -186,10 +186,10 @@
  *  @param accessories The set of EAWiFiUnconfiguredAccessory objects that have been removed from the scan results since the last update.
  *
  */
-- (void)accessoryBrowser:(EAWiFiUnconfiguredAccessoryBrowser *)browser didRemoveUnconfiguredAccessories:(NSSet<EAWiFiUnconfiguredAccessory *> *)accessories NS_AVAILABLE(NA, 8_0);
+- (void)accessoryBrowser:(EAWiFiUnconfiguredAccessoryBrowser *)browser didRemoveUnconfiguredAccessories:(NSSet<EAWiFiUnconfiguredAccessory *> *)accessories __IOS_AVAILABLE(8.0) __OSX_UNAVAILABLE __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
 
 /*!
- *  @method accessoryBrowser:didFinishConfiguringAccessory:withError:
+ *  @method accessoryBrowser:didFinishConfiguringAccessory:withStatus:
  *
  *  @discussion Invoked whenever the EAWiFiUnconfiguredAccessoryBrowser has completed configuring the selected EAWiFiUnconfiguredAccessory.
  *
@@ -198,7 +198,7 @@
  *  @param status    The status of the configuration process that has completed.
  *
  */
-- (void)accessoryBrowser:(EAWiFiUnconfiguredAccessoryBrowser *)browser didFinishConfiguringAccessory:(EAWiFiUnconfiguredAccessory *)accessory withStatus:(EAWiFiUnconfiguredAccessoryConfigurationStatus)status NS_AVAILABLE(NA, 8_0);
+- (void)accessoryBrowser:(EAWiFiUnconfiguredAccessoryBrowser *)browser didFinishConfiguringAccessory:(EAWiFiUnconfiguredAccessory *)accessory withStatus:(EAWiFiUnconfiguredAccessoryConfigurationStatus)status __IOS_AVAILABLE(8.0) __OSX_UNAVAILABLE __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE;
 
 @end
 

```