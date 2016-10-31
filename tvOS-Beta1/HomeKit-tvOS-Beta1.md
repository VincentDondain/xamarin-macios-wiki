#HomeKit.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryCategoryTypes.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryCategoryTypes.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryCategoryTypes.h	2016-08-13 07:16:38.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryCategoryTypes.h	2016-10-24 06:00:27.000000000 +0200
@@ -104,3 +104,27 @@
  */
 HM_EXTERN NSString * const HMAccessoryCategoryTypeWindowCovering NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
+/*!
+ * @brief Category type for Air Purifier.
+ */
+HM_EXTERN NSString * const HMAccessoryCategoryTypeAirPurifier NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Category type for Air Heater.
+ */
+HM_EXTERN NSString * const HMAccessoryCategoryTypeAirHeater NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Category type for Air Conditioner.
+ */
+HM_EXTERN NSString * const HMAccessoryCategoryTypeAirConditioner NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Category type for Air Humidifier.
+ */
+HM_EXTERN NSString * const HMAccessoryCategoryTypeAirHumidifier NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Category type for Air Dehumidifier.
+ */
+HM_EXTERN NSString * const HMAccessoryCategoryTypeAirDehumidifier NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshotControl.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshotControl.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshotControl.h	2016-08-13 07:16:38.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshotControl.h	2016-10-24 06:59:08.000000000 +0200
@@ -8,8 +8,6 @@
 #import <Foundation/Foundation.h>
 #import <HomeKit/HMCameraControl.h>
 
-#import <CoreGraphics/CoreGraphics.h>
-
 NS_ASSUME_NONNULL_BEGIN
 
 @class HMCameraSnapshot;
@@ -22,7 +20,7 @@
 @interface HMCameraSnapshotControl : HMCameraControl
 
 /*!
- * @brief Delegate that receives updates on the camera stream changes.
+ * @brief Delegate that receives updates on the camera snapshot changes.
  */
 @property(weak, nonatomic) id<HMCameraSnapshotControlDelegate> delegate;
 
@@ -33,8 +31,6 @@
 
 /*!
  * @brief Takes an image snapshot.
- *
- * @param resolution Desired video resolution of the stream. This parameter is only a suggested resolution.
  */
 - (void)takeSnapshot;
 
@@ -42,7 +38,7 @@
 
 
 /*!
- * @brief This delegate receives updates on the camera stream.
+ * @brief This delegate receives updates on the camera snapshot.
  */
 __IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0)
 @protocol HMCameraSnapshotControlDelegate <NSObject>
@@ -62,6 +58,13 @@
               didTakeSnapshot:(HMCameraSnapshot *__nullable)snapshot
                         error:(NSError *__nullable)error;
 
+/*!
+ * @brief Informs the delegate that the mostRecentSnapshot was updated.
+ *
+ * @param cameraStreamControl Sender of this message.
+ */
+- (void)cameraSnapshotControlDidUpdateMostRecentSnapshot:(HMCameraSnapshotControl *)cameraSnapshotControl;
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicDefines.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicDefines.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicDefines.h	2016-10-05 23:19:43.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicDefines.h	2016-10-24 06:00:27.000000000 +0200
@@ -247,10 +247,12 @@
 
  @constant  HMCharacteristicValueChargingStateNone              Charging is not in progress.
  @constant  HMCharacteristicValueChargingStateInProgress        Charging is in progress.
+ @constant  HMCharacteristicValueChargingStateNotChargeable     Charging is not supported.
  */
 typedef NS_ENUM(NSInteger, HMCharacteristicValueChargingState) {
     HMCharacteristicValueChargingStateNone = 0,
     HMCharacteristicValueChargingStateInProgress,
+    HMCharacteristicValueChargingStateNotChargeable NS_ENUM_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1),
 } NS_ENUM_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
 
 
@@ -319,3 +321,175 @@
     HMCharacteristicValueSecuritySystemAlarmTypeNoAlarm = 0,
     HMCharacteristicValueSecuritySystemAlarmTypeUnknown,
 } NS_ENUM_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ @enum      HMCharacteristicValueLockPhysicalControlsState
+
+ @constant  HMCharacteristicValueLockPhysicalControlsStateNotLocked     Physical controls not locked.
+ @constant  HMCharacteristicValueLockPhysicalControlsStateLocked        Physical controls locked.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueLockPhysicalControlsState) {
+    HMCharacteristicValueLockPhysicalControlsStateNotLocked = 0,
+    HMCharacteristicValueLockPhysicalControlsStateLocked,
+} NS_ENUM_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ @enum      HMCharacteristicValueCurrentAirPurifierState
+
+ @constant  HMCharacteristicValueCurrentAirPurifierStateInactive    Inactive.
+ @constant  HMCharacteristicValueCurrentAirPurifierStateIdle        Idle.
+ @constant  HMCharacteristicValueCurrentAirPurifierStateActive      Active.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueCurrentAirPurifierState) {
+    HMCharacteristicValueCurrentAirPurifierStateInactive = 0,
+    HMCharacteristicValueCurrentAirPurifierStateIdle,
+    HMCharacteristicValueCurrentAirPurifierStateActive,
+} NS_ENUM_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ @enum      HMCharacteristicValueTargetAirPurifierState
+
+ @constant  HMCharacteristicValueTargetAirPurifierStateManual       Air Purifier is in manual mode.
+ @constant  HMCharacteristicValueTargetAirPurifierStateAutomatic    Air Purifier is in automatic mode.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueTargetAirPurifierState) {
+    HMCharacteristicValueTargetAirPurifierStateManual = 0,
+    HMCharacteristicValueTargetAirPurifierStateAutomatic,
+} NS_ENUM_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ @enum      HMCharacteristicValueCurrentSlatState
+
+ @constant  HMCharacteristicValueCurrentSlatStateStationary         Slats are stationary.
+ @constant  HMCharacteristicValueCurrentSlatStateJammed             Slats are jammed.
+ @constant  HMCharacteristicValueCurrentSlatStateOscillating        Slats are oscillating.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueCurrentSlatState) {
+    HMCharacteristicValueCurrentSlatStateStationary = 0,
+    HMCharacteristicValueCurrentSlatStateJammed,
+    HMCharacteristicValueCurrentSlatStateOscillating,
+} NS_ENUM_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ @enum      HMCharacteristicValueSlatType
+
+ @constant  HMCharacteristicValueSlatTypeHorizontal          Slat type is horizontal.
+ @constant  HMCharacteristicValueSlatTypeVertical            Slat type is vertical.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueSlatType) {
+    HMCharacteristicValueSlatTypeHorizontal = 0,
+    HMCharacteristicValueSlatTypeVertical,
+} NS_ENUM_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ @enum      HMCharacteristicValueFilterChange
+
+ @constant  HMCharacteristicValueFilterChangeNotNeeded      Filter does not need to be changed.
+ @constant  HMCharacteristicValueFilterChangeNeeded         Filter needs to be changed.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueFilterChange) {
+    HMCharacteristicValueFilterChangeNotNeeded = 0,
+    HMCharacteristicValueFilterChangeNeeded,
+} NS_ENUM_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ @enum      HMCharacteristicValueCurrentFanState
+
+ @constant  HMCharacteristicValueCurrentFanStateInactive            Inactive.
+ @constant  HMCharacteristicValueCurrentFanStateIdle                Idle.
+ @constant  HMCharacteristicValueCurrentFanStateActive              Active.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueCurrentFanState) {
+    HMCharacteristicValueCurrentFanStateInactive = 0,
+    HMCharacteristicValueCurrentFanStateIdle,
+    HMCharacteristicValueCurrentFanStateActive,
+} NS_ENUM_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ @enum      HMCharacteristicValueTargetFanState
+
+ @constant  HMCharacteristicValueTargetFanStateManual       Fan is in manual mode.
+ @constant  HMCharacteristicValueTargetFanStateAutomatic    Fan is in automatic mode.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueTargetFanState) {
+    HMCharacteristicValueTargetFanStateManual = 0,
+    HMCharacteristicValueTargetFanStateAutomatic,
+} NS_ENUM_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ @enum      HMCharacteristicValueCurrentHeaterCoolerState
+
+ @constant  HMCharacteristicValueCurrentHeaterCoolerStateInactive   Inactive.
+ @constant  HMCharacteristicValueCurrentHeaterCoolerStateIdle       Idle.
+ @constant  HMCharacteristicValueCurrentHeaterCoolerStateHeating    Heating.
+ @constant  HMCharacteristicValueCurrentHeaterCoolerStateCooling    Cooling.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueCurrentHeaterCoolerState) {
+    HMCharacteristicValueCurrentHeaterCoolerStateInactive = 0,
+    HMCharacteristicValueCurrentHeaterCoolerStateIdle,
+    HMCharacteristicValueCurrentHeaterCoolerStateHeating,
+    HMCharacteristicValueCurrentHeaterCoolerStateCooling,
+} NS_ENUM_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ @enum      HMCharacteristicValueTargetHeaterCoolerState
+
+ @constant  HMCharacteristicValueTargetHeaterCoolerStateAutomatic       Automatic mode.
+ @constant  HMCharacteristicValueTargetHeaterCoolerStateHeat            Heat mode.
+ @constant  HMCharacteristicValueTargetHeaterCoolerStateCool            Cool mode.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueTargetHeaterCoolerState) {
+    HMCharacteristicValueTargetHeaterCoolerStateAutomatic = 0,
+    HMCharacteristicValueTargetHeaterCoolerStateHeat,
+    HMCharacteristicValueTargetHeaterCoolerStateCool,
+} NS_ENUM_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ @enum      HMCharacteristicValueCurrentHumidifierDehumidifierState
+
+ @constant  HMCharacteristicValueCurrentHumidifierDehumidifierStateInactive         Inactive.
+ @constant  HMCharacteristicValueCurrentHumidifierDehumidifierStateIdle             Idle.
+ @constant  HMCharacteristicValueCurrentHumidifierDehumidifierStateHumidifying      Humidifying.
+ @constant  HMCharacteristicValueCurrentHumidifierDehumidifierStateDehumidifying    Dehumidifying.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueCurrentHumidifierDehumidifierState) {
+    HMCharacteristicValueCurrentHumidifierDehumidifierStateInactive = 0,
+    HMCharacteristicValueCurrentHumidifierDehumidifierStateIdle,
+    HMCharacteristicValueCurrentHumidifierDehumidifierStateHumidifying,
+    HMCharacteristicValueCurrentHumidifierDehumidifierStateDehumidifying,
+} NS_ENUM_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ @enum      HMCharacteristicValueTargetHumidifierDehumidifierState
+
+ @constant  HMCharacteristicValueTargetHumidifierDehumidifierStateAutomatic             Automatic mode.
+ @constant  HMCharacteristicValueTargetHumidifierDehumidifierStateHumidify              Humidify mode.
+ @constant  HMCharacteristicValueTargetHumidifierDehumidifierStateDehumidify            Dehumidify mode.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueTargetHumidifierDehumidifierState) {
+    HMCharacteristicValueTargetHumidifierDehumidifierStateAutomatic = 0,
+    HMCharacteristicValueTargetHumidifierDehumidifierStateHumidify,
+    HMCharacteristicValueTargetHumidifierDehumidifierStateDehumidify,
+} NS_ENUM_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ @enum      HMCharacteristicValueSwingMode
+
+ @constant  HMCharacteristicValueSwingModeDisabled                  Swing mode is disabled.
+ @constant  HMCharacteristicValueSwingModeEnabled                   Swing mode is enabled.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueSwingMode) {
+    HMCharacteristicValueSwingModeDisabled = 0,
+    HMCharacteristicValueSwingModeEnabled,
+} NS_ENUM_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ @enum      HMCharacteristicValueActivationState
+
+ @constant  HMCharacteristicValueActivationStateInactive            Service is inactive.
+ @constant  HMCharacteristicValueActivationStateActive              Service is active.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueActivationState) {
+    HMCharacteristicValueActivationStateInactive = 0,
+    HMCharacteristicValueActivationStateActive,
+} NS_ENUM_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicTypes.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicTypes.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicTypes.h	2016-08-13 07:16:38.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicTypes.h	2016-10-24 06:59:08.000000000 +0200
@@ -505,4 +505,156 @@
  */
 HM_EXTERN NSString * const HMCharacteristicTypeImageMirroring NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
 
+/*!
+ * @brief Characteristic type for active status. The value is boolean.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeActive NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for air purifier current state. The value is
+ *        one of the value defined for HMCharacteristicValueCurrentAirPurifierState.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeCurrentAirPurifierState NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for current fan state. The value is
+ *        one of the values defined for HMCharacteristicValueCurrentFanState.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeCurrentFanState NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for heater/cooler current state. The value is
+ *        one of the values defined for HMCharacteristicValueCurrentHeaterCoolerState.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeCurrentHeaterCoolerState NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for humidifier/dehumidifier current state. The value is
+ *        one of the values defined for HMCharacteristicValueCurrentHumidifierDehumidifierState.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeCurrentHumidifierDehumidifierState NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for current slat state. The value is
+ *        one of the values defined for HMCharacteristicValueCurrentSlatState.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeCurrentSlatState NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for water level. The value is in percentage units.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeWaterLevel NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for filter change indication. The value is
+ *        one of the values defined for HMCharacteristicValueFilterChange.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeFilterChangeIndication NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for filter life level. The value is in percentage units.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeFilterLifeLevel NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for resetting filter change indication. The characteristic
+ *        is write-only that takes a boolean value of 1.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeFilterResetChangeIndication NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for locking physical controls. The value is
+ *        one of the values defined for HMCharacteristicValueLockPhysicalControlsState.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeLockPhysicalControls NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for swing mode. The value is
+ *        one of the values defined for HMCharacteristicValueSwingMode.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeSwingMode NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for target heater/cooler state. The value is
+ *        one of the values defined for HMCharacteristicValueTargetHeaterCoolerState.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeTargetHeaterCoolerState NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for target humidifier/dehumidifier state. The value
+ *        is one of the values defined for HMCharacteristicValueTargetHumidifierDehumidifierState.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeTargetHumidifierDehumidifierState NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for target fan state. The value is
+ *        one of the values defined for HMCharacteristicValueTargetFanState.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeTargetFanState NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for slat type. The value is
+ *        one of the values defined for HMCharacteristicValueSlatType.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeSlatType NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for current tilt angle. The value is a float representing the angle in arc degrees.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeCurrentTilt NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for target tilt angle. The value is a float representing the angle in arc degrees.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeTargetTilt NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for density of ozone. The value of the characteristic is
+ *        in units of micrograms/m^3.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeOzoneDensity NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for density of nitrogen dioxide. The value of the characteristic is
+ *        in units of micrograms/m^3.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeNitrogenDioxideDensity NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for density of suplhur dioxide. The value of the characteristic is
+ *        in units of micrograms/m^3.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeSuplhurDioxideDensity NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for density of air-particulate matter of size 2.5 micrograms. The
+ *        value of the characteristic is in units of micrograms/m^3.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypePM2_5Density NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for density of air-particulate matter of size 10 micrograms. The
+ *        value of the characteristic is in units of micrograms/m^3.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypePM10Density NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for density of volatile organic compounds. The value of the
+ *        characteristic is in units of micrograms/m^3.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeVolatileOrganicCompoundDensity NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for dehumidifier threshold. The value of the characteristic is
+ *        a float value in percent.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeDehumidifierThreshold NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Characteristic type for humidifier threshold. The value of the characteristic is
+ *        a float value in percent.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeHumidifierThreshold NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMError.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMError.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMError.h	2016-09-28 09:45:09.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMError.h	2016-10-24 06:59:08.000000000 +0200
@@ -104,6 +104,7 @@
     HMErrorCodeInvalidOrMissingAuthorizationData       NS_ENUM_AVAILABLE_IOS(10) = 87,
     HMErrorCodeBridgedAccessoryNotReachable            NS_ENUM_AVAILABLE_IOS(10) = 88,
     HMErrorCodeNotAuthorizedForMicrophoneAccess        NS_ENUM_AVAILABLE_IOS(10) = 89,
+    HMErrorCodeIncompatibleNetwork                     NS_ENUM_AVAILABLE_IOS(10_2) = 90,
 } NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMServiceTypes.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMServiceTypes.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMServiceTypes.h	2016-10-01 08:50:41.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMServiceTypes.h	2016-10-23 09:20:42.000000000 +0200
@@ -175,4 +175,34 @@
  */
 HM_EXTERN NSString * const HMServiceTypeSpeaker NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
 
+/*!
+ * @brief Service type for air purifier.
+ */
+HM_EXTERN NSString * const HMServiceTypeAirPurifier NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Service type for ventilation fan.
+ */
+HM_EXTERN NSString * const HMServiceTypeVentilationFan NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Service type for filter maintenance.
+ */
+HM_EXTERN NSString * const HMServiceTypeFilterMaintenance NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Service type for heater/cooler.
+ */
+HM_EXTERN NSString * const HMServiceTypeHeaterCooler NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Service type for humidifier/dehumidifier.
+ */
+HM_EXTERN NSString * const HMServiceTypeHumidifierDehumidifier NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
+/*!
+ * @brief Service type for slat(s).
+ */
+HM_EXTERN NSString * const HMServiceTypeSlat NS_AVAILABLE_IOS(10_2) __WATCHOS_AVAILABLE(3_1_1) __TVOS_AVAILABLE(10_1);
+
 NS_ASSUME_NONNULL_END

```