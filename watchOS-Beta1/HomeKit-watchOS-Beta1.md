#HomeKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessory+Camera.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessory+Camera.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessory+Camera.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessory+Camera.h	2016-05-28 06:33:50.000000000 +0200
@@ -0,0 +1,31 @@
+//
+//  HMAccessory+Camera.h
+//  HomeKit
+//
+//  Copyright © 2015-2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <HomeKit/HMAccessory.h>
+
+@class HMCameraProfile;
+
+NS_ASSUME_NONNULL_BEGIN
+
+/*!
+ * @abstract Category implementing methods related to camera profile.
+ */
+@interface HMAccessory(Camera)
+
+/*!
+ * @brief Returns array of camera profiles implemented by the accessory.
+ *
+ * @discussion An accessory can contain one or more cameras. Each camera is represented as a 
+ *             an HMCameraProfile object. If the accessory does not contain a camera, this property
+ *             will be nil.
+ */
+@property(readonly, copy, nonatomic, nullable) NSArray<HMCameraProfile *> *cameraProfiles __IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessory.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessory.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessory.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessory.h	2016-05-28 06:33:50.000000000 +0200
@@ -22,7 +22,7 @@
  *             one relationship between a physical accessory and an object of this
  *             class. An accessory is composed of one or more services.
  */
-NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMAccessory : NSObject
 
 /*!
@@ -38,7 +38,7 @@
  *
  * @discussion Use uniqueIdentifier to obtain the identifier for this object.
  */
-@property(readonly, copy, nonatomic) NSUUID *identifier NS_DEPRECATED_IOS(8_0, 9_0) __WATCHOS_PROHIBITED;
+@property(readonly, copy, nonatomic) NSUUID *identifier NS_DEPRECATED_IOS(8_0, 9_0) __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief A unique identifier for the accessory.
@@ -70,7 +70,7 @@
  * @discussion Use uniqueIdentifiersForBridgedAccessories to obtain the identifiers for the
  *             bridged accessories.
  */
-@property(readonly, copy, nonatomic, nullable) NSArray<NSUUID *> *identifiersForBridgedAccessories NS_DEPRECATED_IOS(8_0, 9_0) __WATCHOS_PROHIBITED;
+@property(readonly, copy, nonatomic, nullable) NSArray<NSUUID *> *identifiersForBridgedAccessories NS_DEPRECATED_IOS(8_0, 9_0) __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief If this accessory is a bridge, this property is an array of NSUUID objects that,
@@ -118,7 +118,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)updateName:(NSString *)name completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)updateName:(NSString *)name completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief This method is used to have an accessory identify itself.
@@ -136,7 +136,7 @@
  * @brief This defines the protocol for a delegate to receive updates about
  *        different aspects of an accessory
  */
-NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @protocol HMAccessoryDelegate <NSObject>
 
 @optional
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryBrowser.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryBrowser.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryBrowser.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryBrowser.h	2016-05-28 06:33:50.000000000 +0200
@@ -16,7 +16,7 @@
  * @brief This class is used to discover new accessories in the home
  *        that have never been paired with and therefore not part of the home.
  */
-NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_PROHIBITED __TVOS_PROHIBITED
 @interface HMAccessoryBrowser : NSObject
 
 /*!
@@ -60,7 +60,7 @@
 /*!
  * @brief This delegate receives updates about new accessories in the home.
  */
-NS_AVAILABLE_IOS(8_0) __WATCHOS_PROHIBITED
+NS_AVAILABLE_IOS(8_0) __WATCHOS_PROHIBITED __TVOS_PROHIBITED
 @protocol HMAccessoryBrowserDelegate <NSObject>
 
 @optional
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryCategory.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryCategory.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryCategory.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryCategory.h	2016-05-28 06:33:50.000000000 +0200
@@ -13,7 +13,7 @@
 /*!
  * @brief This class is used to represent an accessory category.
  */
-NS_CLASS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMAccessoryCategory : NSObject
 
 /*!
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryCategoryTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryCategoryTypes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryCategoryTypes.h	2016-02-22 03:35:48.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryCategoryTypes.h	2016-05-28 06:33:50.000000000 +0200
@@ -17,79 +17,85 @@
 /*!
  * @brief Category type for Other.
  */
-HM_EXTERN NSString * const HMAccessoryCategoryTypeOther NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMAccessoryCategoryTypeOther NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Category type for Security System.
  */
-HM_EXTERN NSString * const HMAccessoryCategoryTypeSecuritySystem NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMAccessoryCategoryTypeSecuritySystem NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Category type for Bridge.
  */
-HM_EXTERN NSString * const HMAccessoryCategoryTypeBridge NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMAccessoryCategoryTypeBridge NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Category type for Door.
  */
-HM_EXTERN NSString * const HMAccessoryCategoryTypeDoor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMAccessoryCategoryTypeDoor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Category type for Door Lock.
  */
-HM_EXTERN NSString * const HMAccessoryCategoryTypeDoorLock NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMAccessoryCategoryTypeDoorLock NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Category type for Fan.
  */
-HM_EXTERN NSString * const HMAccessoryCategoryTypeFan NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMAccessoryCategoryTypeFan NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Category type for Garage Door Opener.
  */
-HM_EXTERN NSString * const HMAccessoryCategoryTypeGarageDoorOpener NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMAccessoryCategoryTypeGarageDoorOpener NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
+
+/*
+* @brief Category type for IP Camera.
+*/
+HM_EXTERN NSString * const HMAccessoryCategoryTypeIPCamera NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0);
 
 /*!
  * @brief Category type for Lightbulb.
  */
-HM_EXTERN NSString * const HMAccessoryCategoryTypeLightbulb NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMAccessoryCategoryTypeLightbulb NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Category type for Outlet.
  */
-HM_EXTERN NSString * const HMAccessoryCategoryTypeOutlet NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMAccessoryCategoryTypeOutlet NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Category type for Programmable Switch.
  */
-HM_EXTERN NSString * const HMAccessoryCategoryTypeProgrammableSwitch NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMAccessoryCategoryTypeProgrammableSwitch NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ * @brief Category type for Range Extender
+ */
+HM_EXTERN NSString * const HMAccessoryCategoryTypeRangeExtender NS_AVAILABLE_IOS(9_3) __WATCHOS_AVAILABLE(2_2);
 
 /*!
  * @brief Category type for Sensor.
  */
-HM_EXTERN NSString * const HMAccessoryCategoryTypeSensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMAccessoryCategoryTypeSensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Category type for Switch.
  */
-HM_EXTERN NSString * const HMAccessoryCategoryTypeSwitch NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMAccessoryCategoryTypeSwitch NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Category type for Thermostat.
  */
-HM_EXTERN NSString * const HMAccessoryCategoryTypeThermostat NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMAccessoryCategoryTypeThermostat NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Category type for Window.
  */
-HM_EXTERN NSString * const HMAccessoryCategoryTypeWindow NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMAccessoryCategoryTypeWindow NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Category type for Window Covering.
  */
-HM_EXTERN NSString * const HMAccessoryCategoryTypeWindowCovering NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMAccessoryCategoryTypeWindowCovering NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
-/*!
- * @brief Category type for Range Extender
- */
-HM_EXTERN NSString * const HMAccessoryCategoryTypeRangeExtender NS_AVAILABLE_IOS(9_3) __WATCHOS_AVAILABLE(2.2);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryProfile.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryProfile.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryProfile.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAccessoryProfile.h	2016-05-28 06:33:50.000000000 +0200
@@ -0,0 +1,40 @@
+//
+//  HMAccessoryProfile.h
+//  HomeKit
+//
+//  Copyright © 2015-2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+@class HMAccessory;
+@class HMService;
+
+NS_ASSUME_NONNULL_BEGIN
+
+/*!
+ * @abstract Represents a profile implemented by an accessory.
+ */
+__IOS_AVAILABLE(__IPHONE_10_0) __WATCHOS_AVAILABLE(__WATCHOS_3_0) __TVOS_AVAILABLE(__TVOS_10_0)
+@interface HMAccessoryProfile : NSObject
+
+- (instancetype)init NS_UNAVAILABLE;
+
+/*!
+ * @brief A unique identifier for the profile.
+ */
+@property(readonly, copy, nonatomic) NSUUID *uniqueIdentifier;
+
+/*!
+ * @brief Collection of services representing the profile.
+ */
+@property(readonly, strong, nonatomic) NSArray<HMService *> *services;
+
+/*!
+ * @brief Accessory implementing the profile.
+ */
+@property(readonly, weak, nonatomic) HMAccessory *accessory;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAction.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAction.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAction.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMAction.h	2016-05-28 06:33:50.000000000 +0200
@@ -10,7 +10,7 @@
 /*!
  * @brief This class is used to represent a generic action.
  */
-NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMAction : NSObject
 
 /*!
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMActionSet.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMActionSet.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMActionSet.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMActionSet.h	2016-05-26 07:47:38.000000000 +0200
@@ -15,7 +15,7 @@
  * @brief This class represents a collection of action objects that can be executed. 
  *        The order of execution of these actions is undefined.
  */             
-NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMActionSet : NSObject
 
 - (instancetype)init NS_UNAVAILABLE;
@@ -36,8 +36,9 @@
 @property(readonly, getter=isExecuting, nonatomic) BOOL executing;
 
 /*!
- * @brief Specifies the action set type - user-defined or one of the builtin types.
- *        Builtin action sets cannot be removed from the home.
+ * @brief Specifies the action set type - user-defined, trigger-owned or one of the builtin types.
+ *        Builtin action sets cannot be removed from the home. trigger-owned action sets cannot
+ *        be executed, renamed or associated with another trigger.
  */
 @property(readonly, copy, nonatomic) NSString *actionSetType NS_AVAILABLE_IOS(9_0);
 
@@ -47,6 +48,11 @@
 @property(readonly, copy, nonatomic) NSUUID *uniqueIdentifier NS_AVAILABLE_IOS(9_0);
 
 /*!
+ * @brief Specifies the last execution date for the action set.
+ */
+@property(readonly, copy, nonatomic) NSDate *lastExecutionDate NS_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+
+/*!
  * @brief This method is used to change the name of the action set.
  *
  * @param name New name for the action set.
@@ -55,7 +61,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)updateName:(NSString *)name completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)updateName:(NSString *)name completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Adds an action to the action set.
@@ -66,7 +72,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)addAction:(HMAction *)action completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)addAction:(HMAction *)action completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Removes an existing action from the action set.
@@ -77,35 +83,42 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)removeAction:(HMAction *)action completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
-
+- (void)removeAction:(HMAction *)action completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 @end
 
 /*!
- * @brief Builtin action set type for WakeUp
+ * @brief Builtin action set type for WakeUp.
  */
-HM_EXTERN NSString * const HMActionSetTypeWakeUp NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMActionSetTypeWakeUp NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
- * @brief Type for builtin action set Sleep
+ * @brief Type for builtin action set Sleep.
  */
-HM_EXTERN NSString * const HMActionSetTypeSleep NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMActionSetTypeSleep NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
- * @brief Type for builtin action set HomeDeparture
+ * @brief Type for builtin action set HomeDeparture.
  */
-HM_EXTERN NSString * const HMActionSetTypeHomeDeparture NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMActionSetTypeHomeDeparture NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
- * @brief Type for builtin action set HomeArrival
+ * @brief Type for builtin action set HomeArrival.
  */
-HM_EXTERN NSString * const HMActionSetTypeHomeArrival NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMActionSetTypeHomeArrival NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
- * @brief Type for user-defined action sets
+ * @brief Type for user-defined action sets.
  */
-HM_EXTERN NSString * const HMActionSetTypeUserDefined NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMActionSetTypeUserDefined NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
+/*!
+ * @brief Type for trigger-owned action sets.
+ *
+ * @discussion An action set of this type is owned by a trigger and is not listed
+ *             as part of the home. An action set of this type cannot be executed,
+ *             renamed, or associated with a different trigger.
+ */
+HM_EXTERN NSString * const HMActionSetTypeTriggerOwned __IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraAudioControl.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraAudioControl.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraAudioControl.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraAudioControl.h	2016-05-28 06:33:50.000000000 +0200
@@ -0,0 +1,31 @@
+//
+//  HMCameraAudioControl.h
+//  HomeKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <HomeKit/HMCameraControl.h>
+
+@class HMCharacteristic;
+
+NS_ASSUME_NONNULL_BEGIN
+
+__IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0)
+@interface HMCameraAudioControl : HMCameraControl
+
+- (instancetype)init NS_UNAVAILABLE;
+
+/*!
+ * Characteristic corresponding to mute setting on the camera.
+ */
+@property(readonly, strong, nonatomic, nullable) HMCharacteristic *mute;
+
+/*!
+ * Characteristic corresponding to volume setting on the camera.
+ */
+@property(readonly, strong, nonatomic, nullable) HMCharacteristic *volume;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraControl.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraControl.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraControl.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraControl.h	2016-05-28 06:33:50.000000000 +0200
@@ -0,0 +1,20 @@
+//
+//  HMCameraControl.h
+//  HomeKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+/*!
+ * @abstract Represents a generic camera control.
+ */
+__IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0)
+@interface HMCameraControl : NSObject
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraDefines.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraDefines.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraDefines.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraDefines.h	2016-05-28 06:33:50.000000000 +0200
@@ -0,0 +1,59 @@
+//
+//  HMCameraDefines.h
+//  HomeKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+/*!
+ * @abstract This enumeration describes the different states of a camera stream.
+ */
+__IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0)
+typedef NS_ENUM(NSUInteger, HMCameraStreamState)
+{
+    /*!
+     * Start stream request is in progress.
+     */
+    HMCameraStreamStateStarting = 1,
+
+    /*!
+     * Streaming is in progress.
+     */
+    HMCameraStreamStateStreaming = 2,
+
+    /*!
+     * Stop stream request is in progress.
+     */
+    HMCameraStreamStateStopping = 3,
+
+    /*!
+     * No streaming is in progress.
+     */
+    HMCameraStreamStateNotStreaming = 4
+};
+
+/*!
+ * @abstract This enumeration describes the setting for audio on the recipient of the camera stream.
+ */
+__IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0)
+typedef NS_ENUM(NSUInteger, HMCameraAudioStreamSetting)
+{
+    /*!
+     * Muted for incoming and outgoing audio.
+     */
+    HMCameraAudioStreamSettingMuted = 1,
+
+    /*!
+     * Only incoming audio is allowed.
+     */
+    HMCameraAudioStreamSettingIncomingAudioAllowed = 2,
+
+    /*!
+     * Bidirectional audio is allowed.
+     */
+    HMCameraAudioStreamSettingBidirectionalAudioAllowed = 3,
+};
+
+
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraProfile.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraProfile.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraProfile.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraProfile.h	2016-05-28 06:33:50.000000000 +0200
@@ -0,0 +1,58 @@
+//
+//  HMCameraProfile.h
+//  HomeKit
+//
+//  Copyright © 2015 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <HomeKit/HMAccessoryProfile.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class HMCameraStreamControl;
+@class HMCameraSnapshotControl;
+@class HMCameraSettingsControl;
+@class HMCameraAudioControl;
+
+
+/*!
+ * @abstract Represents a camera profile the accessory implements.
+ *
+ * @discussion Provides an interface to interact with a Camera in an Accessory.
+ */
+__IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0)
+@interface HMCameraProfile : HMAccessoryProfile
+
+- (instancetype)init NS_UNAVAILABLE;
+
+/*!
+ * @brief Object that can be used to control the camera stream.
+ */
+@property(readonly, strong, nonatomic, nullable) HMCameraStreamControl *streamControl;
+
+/*!
+ * @brief Object that can be used to take image snapshots from the camera.
+ */
+@property(readonly, strong, nonatomic, nullable) HMCameraSnapshotControl *snapshotControl;
+
+/*!
+ * @brief Object that can be used to control the settings on the camera.
+ */
+@property(readonly, strong, nonatomic, nullable) HMCameraSettingsControl *settingsControl;
+
+/*!
+ * @brief Object that can be used to control the speaker settings on the camera.
+ */
+@property(readonly, strong, nonatomic, nullable) HMCameraAudioControl *speakerControl;
+
+/*!
+ * @brief Object that can be used to control the microphone settings on the camera.
+ */
+@property(readonly, strong, nonatomic, nullable) HMCameraAudioControl *microphoneControl;
+
+@end
+
+
+NS_ASSUME_NONNULL_END
+
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSettingsControl.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSettingsControl.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSettingsControl.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSettingsControl.h	2016-05-28 06:33:50.000000000 +0200
@@ -0,0 +1,69 @@
+//
+//  HMCameraSettingsControl.h
+//  HomeKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <HomeKit/HMCameraControl.h>
+
+@class HMCharacteristic;
+
+NS_ASSUME_NONNULL_BEGIN
+
+/*!
+ * @abstract This class can be used to control the settings on a camera.
+ */
+__IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0)
+@interface HMCameraSettingsControl : HMCameraControl
+
+- (instancetype)init NS_UNAVAILABLE;
+
+/*!
+ *  Characteristic corresponding to night vision setting on the camera.
+ */
+@property(readonly, strong, nonatomic, nullable) HMCharacteristic *nightVision;
+
+/*!
+ * Characteristic corresponding to current horizontal tilt setting on the camera.
+ */
+@property(readonly, strong, nonatomic, nullable) HMCharacteristic *currentHorizontalTilt;
+
+/*!
+ * Characteristic corresponding to target horizontal tilt setting on the camera.
+ */
+@property(readonly, strong, nonatomic, nullable) HMCharacteristic *targetHorizontalTilt;
+
+/*!
+ * Characteristic corresponding to current vertical tilt setting on the camera.
+ */
+@property(readonly, strong, nonatomic, nullable) HMCharacteristic *currentVerticalTilt;
+
+/*!
+ * Characteristic corresponding to target vertical tilt setting on the camera.
+ */
+@property(readonly, strong, nonatomic, nullable) HMCharacteristic *targetVerticalTilt;
+
+/*!
+ * Characteristic corresponding to optical zoom setting on the camera.
+ */
+@property(readonly, strong, nonatomic, nullable) HMCharacteristic *opticalZoom;
+
+/*!
+ * Characteristic corresponding to digital zoom setting on the camera.
+ */
+@property(readonly, strong, nonatomic, nullable) HMCharacteristic *digitalZoom;
+
+/*!
+ * Characteristic corresponding to image rotation setting on the camera.
+ */
+@property(readonly, strong, nonatomic, nullable) HMCharacteristic *imageRotation;
+
+/*!
+ * Characteristic corresponding to image mirroring setting on the camera.
+ */
+@property(readonly, strong, nonatomic, nullable) HMCharacteristic *imageMirroring;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshot.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshot.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshot.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshot.h	2016-05-28 06:33:50.000000000 +0200
@@ -0,0 +1,25 @@
+//
+//  HMCameraSnapshot.h
+//  HomeKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <HomeKit/HMCameraSource.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+/*!
+ * @abstract Represents a camera snapshot.
+ */
+@interface HMCameraSnapshot : HMCameraSource
+
+/*!
+ * @brief Time corresponding to the snapshot request.
+ */
+@property(readonly, copy, nonatomic) NSDate *captureDate;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshotControl.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshotControl.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshotControl.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshotControl.h	2016-05-28 06:33:50.000000000 +0200
@@ -0,0 +1,68 @@
+//
+//  HMCameraSnapshotControl.h
+//  HomeKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <HomeKit/HMCameraControl.h>
+
+#import <CoreGraphics/CoreGraphics.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class HMCameraSnapshot;
+@protocol HMCameraSnapshotControlDelegate;
+
+/*!
+ * @abstract This class can be used to take an image snapshot from a camera.
+ */
+__IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0)
+@interface HMCameraSnapshotControl : HMCameraControl
+
+/*!
+ * @brief Delegate that receives updates on the camera stream changes.
+ */
+@property(weak, nonatomic) id<HMCameraSnapshotControlDelegate> delegate;
+
+/*!
+ * @brief Represents the most recent snapshot taken from the camera.
+ */
+@property(readonly, strong, nonatomic, nullable) HMCameraSnapshot *mostRecentSnapshot;
+
+/*!
+ * @brief Takes an image snapshot.
+ *
+ * @param resolution Desired video resolution of the stream. This parameter is only a suggested resolution.
+ */
+- (void)takeSnapshot;
+
+@end
+
+
+/*!
+ * @brief This delegate receives updates on the camera stream.
+ */
+__IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0)
+@protocol HMCameraSnapshotControlDelegate <NSObject>
+
+@optional
+
+/*!
+ * @brief Informs the delegate that the snapshot was taken.
+ *
+ * @param cameraStreamControl Sender of this message.
+ *
+ * @param snapshot Snapshot will be valid if snapshot was successfully taken.
+ *
+ * @param error Error will be populated if the snapshot could not be taken.
+ */
+- (void)cameraSnapshotControl:(HMCameraSnapshotControl *)cameraSnapshotControl
+              didTakeSnapshot:(HMCameraSnapshot *__nullable)snapshot
+                        error:(NSError *__nullable)error;
+
+@end
+
+NS_ASSUME_NONNULL_END
+
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSource.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSource.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSource.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSource.h	2016-05-28 06:33:50.000000000 +0200
@@ -0,0 +1,20 @@
+//
+//  HMCameraSource.h
+//  HomeKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+/*!
+ * @brief Abstract class for source of data from a camera.
+ */
+__IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0)
+@interface HMCameraSource : NSObject
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraStream.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraStream.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraStream.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraStream.h	2016-05-28 06:33:50.000000000 +0200
@@ -0,0 +1,27 @@
+//
+//  HMCameraStream.h
+//  HomeKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <HomeKit/HMCameraSource.h>
+#import <HomeKit/HMCameraDefines.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+/*!
+ * @abstract Represents a camera stream.
+ */
+__IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0)
+@interface HMCameraStream : HMCameraSource
+
+/*!
+ * @brief Represents the audio setting for the current stream.
+ */
+@property(assign, nonatomic) HMCameraAudioStreamSetting audioStreamSetting;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraStreamControl.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraStreamControl.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraStreamControl.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraStreamControl.h	2016-05-28 06:33:50.000000000 +0200
@@ -0,0 +1,79 @@
+//
+//  HMCameraStreamControl.h
+//  HomeKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <HomeKit/HMCameraControl.h>
+#import <HomeKit/HMCameraDefines.h>
+
+#import <CoreGraphics/CoreGraphics.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@protocol HMCameraStreamControlDelegate;
+@class HMCameraStream;
+
+/*!
+ * @abstract This class can be used to control the stream from a camera.
+ */
+__IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0)
+@interface HMCameraStreamControl : HMCameraControl
+
+/*!
+ * @brief Delegate that receives updates on the camera stream changes.
+ */
+@property(weak, nonatomic) id<HMCameraStreamControlDelegate> delegate;
+
+/*!
+ * @brief Represents the current streaming state.
+ */
+@property(readonly, assign, nonatomic) HMCameraStreamState streamState;
+
+/*!
+ * @brief Represents the current camera stream.
+ */
+@property(readonly, strong, nonatomic, nullable) HMCameraStream *cameraStream;
+
+/*!
+ * @brief Starts the camera stream. 'currentCameraStream' will be updated upon 
+ *        successfully starting the stream.
+ */
+- (void)startStream;
+
+/*!
+ * @brief Stops the camera stream.
+ * */
+- (void)stopStream;
+
+@end
+
+/*!
+ * @brief This delegate receives updates on the camera stream.
+ */
+__IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0)
+@protocol HMCameraStreamControlDelegate <NSObject>
+
+@optional
+
+/*!
+ * @brief Informs the delegate that the stream has started.
+ *
+ * @param cameraStreamControl Sender of this message.
+ */
+- (void)cameraStreamControlDidStartStream:(HMCameraStreamControl *)cameraStreamControl;
+
+/*!
+ * @brief Informs the delegate that the stream has stopped.
+ *
+ * @param cameraStreamControl Sender of this message.
+ *
+ * @param error When stream stops because of an error, 'error' will be populated.
+ */
+- (void)cameraStreamControl:(HMCameraStreamControl *)cameraStreamControl didStopStreamWithError:(NSError *)error;
+
+@end
+
+NS_ASSUME_NONNULL_END
+
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraView.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraView.h	2016-05-28 06:33:50.000000000 +0200
@@ -0,0 +1,29 @@
+//
+//  HMCameraView.h
+//  HomeKit
+//
+//  Copyright © 2015 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+#import <UIKit/UIKit.h>
+
+@class HMCameraSource;
+
+NS_ASSUME_NONNULL_BEGIN
+
+/*!
+ * @abstract This view can render a camera source.
+ */
+__IOS_AVAILABLE(10_0) __WATCHOS_PROHIBITED __TVOS_AVAILABLE(10_0)
+@interface HMCameraView : UIView
+
+/*!
+ * @brief Represents the camera source.
+ */
+@property (strong, nonatomic, nullable) HMCameraSource *cameraSource;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristic.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristic.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristic.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristic.h	2016-05-23 08:18:22.000000000 +0200
@@ -16,7 +16,7 @@
 /*!
  * @brief Represent a characteristic on a service of an accessory.
  */
-NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMCharacteristic : NSObject
 
 /*!
@@ -114,7 +114,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)updateAuthorizationData:(nullable NSData *)data completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)updateAuthorizationData:(nullable NSData *)data completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicDefines.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicDefines.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicDefines.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicDefines.h	2016-05-28 06:33:50.000000000 +0200
@@ -24,7 +24,7 @@
     HMCharacteristicValueDoorStateOpening,
     HMCharacteristicValueDoorStateClosing,
     HMCharacteristicValueDoorStateStopped,
-} NS_ENUM_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+} NS_ENUM_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  @enum      HMCharacteristicValueHeatingCooling
@@ -39,7 +39,7 @@
     HMCharacteristicValueHeatingCoolingHeat,
     HMCharacteristicValueHeatingCoolingCool,
     HMCharacteristicValueHeatingCoolingAuto,
-} NS_ENUM_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+} NS_ENUM_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  @enum      HMCharacteristicValueRotationDirection
@@ -50,7 +50,7 @@
 typedef NS_ENUM(NSInteger, HMCharacteristicValueRotationDirection) {
     HMCharacteristicValueRotationDirectionClockwise = 0,
     HMCharacteristicValueRotationDirectionCounterClockwise,
-} NS_ENUM_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+} NS_ENUM_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  @enum      HMCharacteristicValueTemperatureUnit
@@ -61,7 +61,7 @@
 typedef NS_ENUM(NSInteger, HMCharacteristicValueTemperatureUnit) {
     HMCharacteristicValueTemperatureUnitCelsius = 0,
     HMCharacteristicValueTemperatureUnitFahrenheit,
-} NS_ENUM_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+} NS_ENUM_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  @enum      HMCharacteristicValueLockMechanismState
@@ -76,7 +76,7 @@
     HMCharacteristicValueLockMechanismStateSecured,
     HMCharacteristicValueLockMechanismStateJammed,
     HMCharacteristicValueLockMechanismStateUnknown,
-} NS_ENUM_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+} NS_ENUM_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  @enum      HMCharacteristicValueLockMechanismLastKnownAction
@@ -105,7 +105,7 @@
     HMCharacteristicValueLockMechanismLastKnownActionSecuredWithAutomaticSecureTimeout,
     HMCharacteristicValueLockMechanismLastKnownActionSecuredUsingPhysicalMovement,
     HMCharacteristicValueLockMechanismLastKnownActionUnsecuredUsingPhysicalMovement,
-} NS_ENUM_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+} NS_ENUM_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 
 /*!
@@ -117,7 +117,7 @@
 typedef NS_ENUM(NSInteger, HMCharacteristicValueAirParticulateSize) {
     HMCharacteristicValueAirParticulateSize2_5 = 0,
     HMCharacteristicValueAirParticulateSize10,
-} NS_ENUM_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+} NS_ENUM_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 
 /*!
@@ -137,7 +137,7 @@
     HMCharacteristicValueAirQualityFair,
     HMCharacteristicValueAirQualityInferior,
     HMCharacteristicValueAirQualityPoor,
-} NS_ENUM_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+} NS_ENUM_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 
 /*!
@@ -151,7 +151,7 @@
     HMCharacteristicValuePositionStateClosing = 0,
     HMCharacteristicValuePositionStateOpening,
     HMCharacteristicValuePositionStateStopped,
-} NS_ENUM_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+} NS_ENUM_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 
 /*!
@@ -169,7 +169,7 @@
     HMCharacteristicValueCurrentSecuritySystemStateNightArm,
     HMCharacteristicValueCurrentSecuritySystemStateDisarmed,
     HMCharacteristicValueCurrentSecuritySystemStateTriggered,
-} NS_ENUM_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+} NS_ENUM_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 
 /*!
@@ -185,4 +185,137 @@
     HMCharacteristicValueTargetSecuritySystemStateAwayArm,
     HMCharacteristicValueTargetSecuritySystemStateNightArm,
     HMCharacteristicValueTargetSecuritySystemStateDisarm,
-} NS_ENUM_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+} NS_ENUM_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ @enum      HMCharacteristicValueBatteryStatus
+
+ @constant  HMCharacteristicValueBatteryStatusNormal        Battery status is normal.
+ @constant  HMCharacteristicValueBatteryStatusLow           Battery status is low.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueBatteryStatus) {
+    HMCharacteristicValueBatteryStatusNormal = 0,
+    HMCharacteristicValueBatteryStatusLow,
+} NS_ENUM_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ @enum      HMCharacteristicValueJammedStatus
+
+ @constant  HMCharacteristicValueJammedStatusNone               Not Jammed.
+ @constant  HMCharacteristicValueJammedStatusJammed             Jammed.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueJammedStatus) {
+    HMCharacteristicValueJammedStatusNone = 0,
+    HMCharacteristicValueJammedStatusJammed,
+} NS_ENUM_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ @enum      HMCharacteristicValueTamperStatus
+
+ @constant  HMCharacteristicValueTamperStatusNone               Accessory is not tampered with.
+ @constant  HMCharacteristicValueTamperStatusTampered           Accessory is tampered with.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueTamperedStatus) {
+    HMCharacteristicValueTamperedStatusNone = 0,
+    HMCharacteristicValueTamperedStatusTampered,
+} NS_ENUM_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ @enum      HMCharacteristicValueLeakDetectionStatus
+
+ @constant  HMCharacteristicValueLeakDetectionStatusNone        Leak is not detected.
+ @constant  HMCharacteristicValueLeakDetectionStatusDetected    Leak is detected.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueLeakStatus) {
+    HMCharacteristicValueLeakStatusNone = 0,
+    HMCharacteristicValueLeakStatusDetected,
+} NS_ENUM_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ @enum      HMCharacteristicValueSmokeDetectionStatus
+
+ @constant  HMCharacteristicValueSmokeDetectionStatusNone       Smoke is not detected.
+ @constant  HMCharacteristicValueSmokeDetectionStatusDetected   Smoke is detected.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueSmokeDetectionStatus) {
+    HMCharacteristicValueSmokeDetectionStatusNone = 0,
+    HMCharacteristicValueSmokeDetectionStatusDetected,
+} NS_ENUM_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ @enum      HMCharacteristicValueChargingState
+
+ @constant  HMCharacteristicValueChargingStateNone              Charging is not in progress.
+ @constant  HMCharacteristicValueChargingStateInProgress        Charging is in progress.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueChargingState) {
+    HMCharacteristicValueChargingStateNone = 0,
+    HMCharacteristicValueChargingStateInProgress,
+} NS_ENUM_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+
+/*!
+ @enum      HMCharacteristicValueContactState
+
+ @constant  HMCharacteristicValueContactStateNone               Contact is not detected.
+ @constant  HMCharacteristicValueContactStateDetected           Contact is detected.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueContactState) {
+    HMCharacteristicValueContactStateNone = 0,
+    HMCharacteristicValueContactStateDetected,
+} NS_ENUM_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ @enum      HMCharacteristicValueStatusFault
+ 
+ @constant  HMCharacteristicValueStatusFaultNoFault               No Fault.
+ @constant  HMCharacteristicValueStatusFaultGeneralFault          General Fault.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueStatusFault) {
+    HMCharacteristicValueStatusFaultNoFault = 0,
+    HMCharacteristicValueStatusFaultGeneralFault,
+} NS_ENUM_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ @enum      HMCharacteristicValueCarbonMonoxideDetectionStatus
+
+ @constant  HMCharacteristicValueCarbonMonoxideDetectionStatusNotDetected       Carbon monoxide is not detected.
+ @constant  HMCharacteristicValueCarbonMonoxideDetectionStatusDetected          Carbon monoxide is detected.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueCarbonMonoxideDetectionStatus) {
+    HMCharacteristicValueCarbonMonoxideDetectionStatusNotDetected = 0,
+    HMCharacteristicValueCarbonMonoxideDetectionStatusDetected,
+} NS_ENUM_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ @enum      HMCharacteristicValueCarbonDioxideDetectionStatus
+
+ @constant  HMCharacteristicValueCarbonDioxideDetectionStatusNotDetected    Carbon dioxide is not detected.
+ @constant  HMCharacteristicValueCarbonDioxideDetectionStatusDetected       Carbon dioxide is detected.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueCarbonDioxideDetectionStatus) {
+    HMCharacteristicValueCarbonDioxideDetectionStatusNotDetected = 0,
+    HMCharacteristicValueCarbonDioxideDetectionStatusDetected,
+} NS_ENUM_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ @enum      HMCharacteristicValueOccupancyStatus
+
+ @constant  HMCharacteristicValueOccupancyStatusNotOccupied     Occupancy is not detected.
+ @constant  HMCharacteristicValueOccupancyStatusOccupied        Occupancy is detected.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueOccupancyStatus) {
+    HMCharacteristicValueOccupancyStatusNotOccupied = 0,
+    HMCharacteristicValueOccupancyStatusOccupied,
+} NS_ENUM_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ @enum      HMCharacteristicValueSecuritySystemAlarmType
+
+ @constant  HMCharacteristicValueSecuritySystemAlarmTypeNoAlarm     No alarm.
+ @constant  HMCharacteristicValueSecuritySystemAlarmTypeUnknown     Unknown alarm type.
+ */
+typedef NS_ENUM(NSInteger, HMCharacteristicValueSecuritySystemAlarmType) {
+    HMCharacteristicValueSecuritySystemAlarmTypeNoAlarm = 0,
+    HMCharacteristicValueSecuritySystemAlarmTypeUnknown,
+} NS_ENUM_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicEvent.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicEvent.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicEvent.h	2015-11-14 07:09:37.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicEvent.h	2016-05-28 06:33:50.000000000 +0200
@@ -14,7 +14,7 @@
  * @brief This class represents an event that is evaluated based on the value of a characteristic
  *        set to a particular value.
  */
-NS_CLASS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMCharacteristicEvent<TriggerValueType : id<NSCopying>> : HMEvent
 
 - (instancetype)init NS_UNAVAILABLE;
@@ -32,7 +32,7 @@
  * @return Instance object representing the characteristic event.
  */
 - (instancetype)initWithCharacteristic:(HMCharacteristic *)characteristic
-                          triggerValue:(nullable TriggerValueType)triggerValue __WATCHOS_PROHIBITED;
+                          triggerValue:(nullable TriggerValueType)triggerValue __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief The characteristic associated with the event.
@@ -56,7 +56,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)updateTriggerValue:(nullable TriggerValueType)triggerValue completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)updateTriggerValue:(nullable TriggerValueType)triggerValue completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicMetadata.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicMetadata.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicMetadata.h	2016-02-22 03:35:48.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicMetadata.h	2016-05-28 06:33:50.000000000 +0200
@@ -15,7 +15,7 @@
  *		  further information about a characteristic’s value, which can be used
  * 		  for presentation purposes.
  */
-NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMCharacteristicMetadata : NSObject
 
 /*!
@@ -53,6 +53,11 @@
  */
 @property(readonly, copy, nonatomic, nullable) NSString *manufacturerDescription;
 
+/*!
+ * @brief The subset of valid values supported by the characteristic when the format is unsigned integral type.
+ */
+@property(readonly, copy, nonatomic, nullable) NSArray<NSNumber *> *validValues NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);;
+
 @end
 
 /*!
@@ -64,84 +69,84 @@
  *
  * @discussion The value is an NSNumber containing the boolean value.
  */
-HM_EXTERN NSString * const HMCharacteristicMetadataFormatBool NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicMetadataFormatBool NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Describes that the value format is an integer.
  *
  * @discussion The value is an NSNumber containing a signed 32-bit integer with a range [-2147483648, 2147483647].
  */
-HM_EXTERN NSString * const HMCharacteristicMetadataFormatInt NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicMetadataFormatInt NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Describes that the value format is a float.
  *
  * @discussion The value is an NSNumber containing a 32-bit float.
  */
-HM_EXTERN NSString * const HMCharacteristicMetadataFormatFloat NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicMetadataFormatFloat NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Describes that the value format is a string.
  *
  * @discussion The value is an NSString.
  */
-HM_EXTERN NSString * const HMCharacteristicMetadataFormatString NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicMetadataFormatString NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Describes that the value format is an array.
  *
  * @discussion The value is an NSArray.
  */
-HM_EXTERN NSString * const HMCharacteristicMetadataFormatArray NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicMetadataFormatArray NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Describes that the value format is a dictionary.
  *
  * @discussion The value is an NSDictionary.
  */
-HM_EXTERN NSString * const HMCharacteristicMetadataFormatDictionary NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicMetadataFormatDictionary NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Describes that the value format is an unsigned 8-bit integer.
  *
  * @discussion The value is an NSNumber containing an unsigned 8-bit integer with a range [0, 255].
  */
-HM_EXTERN NSString * const HMCharacteristicMetadataFormatUInt8 NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicMetadataFormatUInt8 NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Describes that the value format is an unsigned 16-bit integer.
  *
  * @discussion The value is an NSNumber containing an unsigned 16-bit integer with a range [0, 65535].
  */
-HM_EXTERN NSString * const HMCharacteristicMetadataFormatUInt16 NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicMetadataFormatUInt16 NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Describes that the value format is an unsigned 32-bit integer.
  *
  * @discussion The value is an NSNumber containing an unsigned 32-bit integer with a range [0, 4294967295].
  */
-HM_EXTERN NSString * const HMCharacteristicMetadataFormatUInt32 NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicMetadataFormatUInt32 NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Describes that the value format is an unsigned 64-bit integer.
  *
  * @discussion The value is an NSNumber containing an unsigned 64-bit integer with a range [0, 18446744073709551615].
  */
-HM_EXTERN NSString * const HMCharacteristicMetadataFormatUInt64 NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicMetadataFormatUInt64 NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Describes that the value format is a data blob.
  *
  * @discussion The value is an NSData containing the bytes of data.
  */
-HM_EXTERN NSString * const HMCharacteristicMetadataFormatData NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicMetadataFormatData NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Describes that the value format is a TLV8.
  *
  * @discussion The value is an NSData containing a set of one or more TLV8's, which are packed type-length-value items with an 8-bit type, 8-bit length, and N-byte value.
  */
-HM_EXTERN NSString * const HMCharacteristicMetadataFormatTLV8 NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicMetadataFormatTLV8 NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 
 /*!
@@ -151,32 +156,42 @@
 /*!
  * @brief Describes that the unit of the characteristic is in Celsius.
  */
-HM_EXTERN NSString * const HMCharacteristicMetadataUnitsCelsius NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicMetadataUnitsCelsius NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Describes that the unit of the characteristic is in Fahrenheit.
  */
-HM_EXTERN NSString * const HMCharacteristicMetadataUnitsFahrenheit NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicMetadataUnitsFahrenheit NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Describes that the unit of the characteristic is a percentage.
  */
-HM_EXTERN NSString * const HMCharacteristicMetadataUnitsPercentage NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicMetadataUnitsPercentage NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
- * @brief Describes that the unit of the characteristic is an arc degree.
+ * @brief Describes that the unit of the characteristic is arc degree.
  */
-HM_EXTERN NSString * const HMCharacteristicMetadataUnitsArcDegree NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicMetadataUnitsArcDegree NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
- * @brief Describes that the unit of the characteristic is in seconds.
+ * @brief Describes that the unit of the characteristic is seconds.
  */
-HM_EXTERN NSString * const HMCharacteristicMetadataUnitsSeconds NS_AVAILABLE_IOS(8_3) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicMetadataUnitsSeconds NS_AVAILABLE_IOS(8_3) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Describes that the unit of the characteristic is Lux (illuminance).
  */
-HM_EXTERN NSString * const HMCharacteristicMetadataUnitsLux NS_AVAILABLE_IOS(9_3) __WATCHOS_AVAILABLE(2.2);
+HM_EXTERN NSString * const HMCharacteristicMetadataUnitsLux NS_AVAILABLE_IOS(9_3) __WATCHOS_AVAILABLE(2_2) __TVOS_AVAILABLE(10_0);
+
+/*!
+ * @brief Describes that the unit of the characteristic is parts per million.
+ */
+HM_EXTERN NSString * const HMCharacteristicMetadataUnitsPartsPerMillion __IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ * @brief Describes that the unit of the characteristic is micrograms per cubic meter.
+ */
+HM_EXTERN NSString * const HMCharacteristicMetadataUnitsMicrogramsPerCubicMeter __IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
 
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicTypes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicTypes.h	2016-02-22 03:52:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicTypes.h	2016-05-26 07:14:11.000000000 +0200
@@ -15,22 +15,22 @@
  *        event connection provides unidirectional communication from the
  *        accessory to the controller.
  */
-HM_EXTERN NSString * const HMCharacteristicPropertySupportsEventNotification NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicPropertySupportsEventNotification NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief This constant specifies that the characteristic is readable.
  */
-HM_EXTERN NSString * const HMCharacteristicPropertyReadable NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicPropertyReadable NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief This constant specifies that the characteristic is writable.
  */
-HM_EXTERN NSString * const HMCharacteristicPropertyWritable NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicPropertyWritable NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief This constant specifies that the characteristic should be hidden from the user.
  */
-HM_EXTERN NSString * const HMCharacteristicPropertyHidden NS_AVAILABLE_IOS(9_3) __WATCHOS_AVAILABLE(2.2);
+HM_EXTERN NSString * const HMCharacteristicPropertyHidden NS_AVAILABLE_IOS(9_3) __WATCHOS_AVAILABLE(2_2) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @group Accessory Service Characteristic Types
@@ -41,391 +41,391 @@
 /*!
  * @brief Characteristic type for power state. The value of the characteristic is a boolean.
  */
-HM_EXTERN NSString * const HMCharacteristicTypePowerState NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypePowerState NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for hue. The value of the characteristic is a float value in arc degrees.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeHue NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeHue NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for saturation. The value of the characteristic is a float value in percent.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeSaturation NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeSaturation NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for brightness. The value of the characteristic is an int value in percent.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeBrightness NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeBrightness NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for temperature units. The value of the characteristic is one of the values
  *        defined for HMCharacteristicValueTemperatureUnit.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeTemperatureUnits NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeTemperatureUnits NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for current temperature. The value of the characteristic is a float value in Celsius.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeCurrentTemperature NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeCurrentTemperature NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for target temperature. The value of the characteristic is a float value in Celsius.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeTargetTemperature NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeTargetTemperature NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for heating/cooling mode. The value of the characteristic is one of the values
  *        defined for HMCharacteristicValueHeatingCooling and indicates the current heating/cooling mode.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeCurrentHeatingCooling NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeCurrentHeatingCooling NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for target heating/cooling mode. The value of the characteristic is one of the values
  *        defined for HMCharacteristicValueHeatingCooling and indicates the target heating/cooling mode.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeTargetHeatingCooling NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeTargetHeatingCooling NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for cooling threshold temperature. The value of the characteristic is a float value in Celsius.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeCoolingThreshold NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeCoolingThreshold NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for heating threshold temperature. The value of the characteristic is a float value in Celsius.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeHeatingThreshold NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeHeatingThreshold NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for current relative humidity. The value of the characteristic is a float value in percent.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeCurrentRelativeHumidity NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeCurrentRelativeHumidity NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for target relative humidity. The value of the characteristic is a float value in percent.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeTargetRelativeHumidity NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeTargetRelativeHumidity NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for current door state. The value of the characteristic is one of the values
  *        defined for HMCharacteristicValueDoorState and indicates the current door state.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeCurrentDoorState NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeCurrentDoorState NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for target door state. The value of the characteristic is one of the values
  *        defined for HMCharacteristicValueDoorState and indicates the target door state.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeTargetDoorState NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeTargetDoorState NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for obstruction detected. The value of the characteristic is a boolean value.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeObstructionDetected NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeObstructionDetected NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for name. The value of the characteristic is a string.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeName NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeName NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for manufacturer. The value of the characteristic is a string.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeManufacturer NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeManufacturer NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for model. The value of the characteristic is a string.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeModel NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeModel NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for serial number. The value of the characteristic is a string.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeSerialNumber NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeSerialNumber NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for identify. The characteristic is write-only that takes a boolean.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeIdentify NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeIdentify NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for rotation direction. The value of the characteristic is one of the values
  *        defined for HMCharacteristicValueRotationDirection and indicates the fan rotation direction.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeRotationDirection NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeRotationDirection NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for rotation speed. The value of the characteristic is a float representing
  *        the percentage of maximum speed.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeRotationSpeed NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeRotationSpeed NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for outlet in use. The value of the characteristic is a boolean, which is true
  *        if the outlet is in use.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeOutletInUse NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeOutletInUse NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for version. The value of the characteristic is a string.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeVersion NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeVersion NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for logs. The value of the characteristic is TLV8 data wrapped in an NSData.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeLogs NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeLogs NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for audio feedback. The value of the characteristic is a boolean.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeAudioFeedback NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeAudioFeedback NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for admin only access. The value of the characteristic is a boolean.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeAdminOnlyAccess NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeAdminOnlyAccess NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for Security System Alarm Type. The value of the characteristic is a uint8.
  *        indicating the type of alarm triggered by a security system service. This characteristic has a value
  *        of 1 when the alarm type is not known and a value of 0 indicates that the alarm conditions are cleared.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeSecuritySystemAlarmType NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeSecuritySystemAlarmType NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for motion detected. The value of the characteristic is a boolean.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeMotionDetected NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeMotionDetected NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for current lock mechanism state. The value of the characteristic is one of the values
  *        defined for HMCharacteristicValueLockMechanismState.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeCurrentLockMechanismState NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeCurrentLockMechanismState NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for target lock mechanism state. The value of the characteristic is either
  *        HMCharacteristicValueLockMechanismStateUnsecured, or HMCharacteristicValueLockMechanismStateSecured,
  *        as defined by HMCharacteristicValueLockMechanismState.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeTargetLockMechanismState NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeTargetLockMechanismState NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for the last known action for a lock mechanism. The value of the characteristic is one of the values
  *        defined for HMCharacteristicValueLockMechanismLastKnownAction.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeLockMechanismLastKnownAction NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeLockMechanismLastKnownAction NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for the control point for lock management. The characteristic is write-only that takes TLV8 data wrapped in an NSData.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeLockManagementControlPoint NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeLockManagementControlPoint NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for the auto secure timeout for lock management. The value of the characteristic is an unsigned 
           32-bit integer representing the number of seconds.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeLockManagementAutoSecureTimeout NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeLockManagementAutoSecureTimeout NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for density of air-particulate matter. The value of the characteristic is
- *        in units of micrograms/m^2.
+ *        in units of micrograms/m^3.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeAirParticulateDensity NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeAirParticulateDensity NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for size of air-particulate matter. The value of the characteristic is
  *        one of the values defined for HMCharacteristicValueAirParticulateSize.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeAirParticulateSize NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeAirParticulateSize NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for air quality. The value of the characteristic is
  *        one of the values defined for HMCharacteristicValueAirQuality.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeAirQuality NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeAirQuality NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for battery level. The value of the characteristic is an uint8
  *        value in percent.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeBatteryLevel NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeBatteryLevel NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for carbon dioxide detected. The value of the characteristic is a uint8 value.
  *        A value of 0 indicates carbon dioxide levels are normal.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeCarbonDioxideDetected NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeCarbonDioxideDetected NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for carbon dioxide level.
  *        The value of the characteristic is a float value in units of ppm.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeCarbonDioxideLevel NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeCarbonDioxideLevel NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for carbon dioxide peak level.
  *        The value of the characteristic is a float value in units of ppm.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeCarbonDioxidePeakLevel NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeCarbonDioxidePeakLevel NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for carbon monoxide detected. The value of the characteristic is a uint8 value.
  *        A value of 0 indicates carbon monoxide levels are normal.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeCarbonMonoxideDetected NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeCarbonMonoxideDetected NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for carbon monoxide level.
  *        The value of the characteristic is a float value in units of ppm.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeCarbonMonoxideLevel NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeCarbonMonoxideLevel NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for carbon monoxide peak level.
  *        The value of the characteristic is a float value in units of ppm.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeCarbonMonoxidePeakLevel NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeCarbonMonoxidePeakLevel NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for Charging state. The value of the characteristic is a uint8.
  *        A value of 1 indicates charging is in progress.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeChargingState NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeChargingState NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for Contact sensor state. The value of the characteristic is a uint8 value.
  *        A value of 0 indicates that contact is detected; a value of 1 indicates no contact is detected.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeContactState NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeContactState NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for current horizontal tilt angle. The value is a float representing the angle in arc degrees.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeCurrentHorizontalTilt NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeCurrentHorizontalTilt NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for current light level. The value of the characteristic in units of lux.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeCurrentLightLevel NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeCurrentLightLevel NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for current position of a door/window. The value of the characteristic is an
  *        uint8 value in percent.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeCurrentPosition NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeCurrentPosition NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for current security system state. The value of the characteristic is one of
  *        the values defined for HMCharacteristicValueCurrentSecuritySystemState.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeCurrentSecuritySystemState NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeCurrentSecuritySystemState NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for current vertical tilt angle. The value is a float representing the angle in arc degrees.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeCurrentVerticalTilt NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeCurrentVerticalTilt NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for firmware version. The value of the characteristic is a string value
  *        describing the firmware version of the accessory.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeFirmwareVersion NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeFirmwareVersion NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for hardware version. The value of the characteristic is a string value
  *        describing the hardware version of the accessory.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeHardwareVersion NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeHardwareVersion NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for Hold Position. The value of the characteristic is a boolean
  *        indicating that the current position should be held/maintained.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeHoldPosition NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeHoldPosition NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for programmable switch input event. The value of the characteristic is an int
  *        that can change based on the type of programmable switch. For a binary programmable switch, a value of 0
  *        indicates OFF (and 1 indicates ON). For a slider programmable switch, the value indicates the level.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeInputEvent NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeInputEvent NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for leak detected. The value of the characteristic is a uint8 value.
  *        A value of 0 indicates no leak is detected; a value of 1 indicates that a leak is detected.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeLeakDetected NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeLeakDetected NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for Occupancy Detected. The value of the characteristic is a uint8 value.
  *        A value of 0 indicates no occupancy is detected; a value of 1 indicates that occupancy is detected.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeOccupancyDetected NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeOccupancyDetected NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for programmable switch output state. This value is to be used for presentation
  *        purposes. For a binary programmable switch, a value of 1 can be used to present a state of ON.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeOutputState NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeOutputState NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for Position state. The value of the characteristic is one of the
  *        one of the values defined for HMCharacteristicValuePositionState.
  */
-HM_EXTERN NSString * const HMCharacteristicTypePositionState NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypePositionState NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for Smoke Detected. The value of the characteristic is a uint8 value.
- *        A value of 0 indicates no leak is detected; a value of 1 indicates that a leak is detected.
+ *        A value of 0 indicates no smoke is detected; a value of 1 indicates that smoke is detected.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeSmokeDetected NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeSmokeDetected NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for software version. The value of the characteristic is a string value
  *        describing the software version of the accessory.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeSoftwareVersion NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeSoftwareVersion NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type to indicate status of a service is active. The value of the characteristic is a boolean.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeStatusActive NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeStatusActive NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type to indicate status of a service is fault. The value of the characteristic is a uint8 value.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeStatusFault NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeStatusFault NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type to indicate status of a service is jammed. The value of the characteristic is a uint8 value.
  *        A value of 0 indicates that the service is not jammed; a value of 1 indicates that the service is jammed.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeStatusJammed NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeStatusJammed NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type to indicate status of a service is low battery. The value of the characteristic is a uint8 value.
  *        A value of 0 indicates battery level is normal; a value of 1 indicates that battery level is low.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeStatusLowBattery NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeStatusLowBattery NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type to indicate status of a service is tampered. The value of the characteristic is a uint8 value.
  *        A value of 0 indicates no tampering has been detected; a value of 1 indicates that a tampering has been detected.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeStatusTampered NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeStatusTampered NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for target horizontal tilt angle. The value is a float representing the angle in arc degrees.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeTargetHorizontalTilt NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeTargetHorizontalTilt NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for target security system state. The value of the characteristic is one of
  *        the values defined for HMCharacteristicValueTargetSecuritySystemState.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeTargetSecuritySystemState NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeTargetSecuritySystemState NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for target position of a door/window. The value of the characteristic is an
@@ -433,11 +433,71 @@
  *        indicates most shade. For blinds, a value of 0 indicates most light is allowed in and 100
  *        indicates least light is allowed.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeTargetPosition NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeTargetPosition NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Characteristic type for target vertical tilt angle. The value is a float representing the angle in arc degrees.
  */
-HM_EXTERN NSString * const HMCharacteristicTypeTargetVerticalTilt NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicTypeTargetVerticalTilt NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ * @brief Characteristic type for streaming status. The value is a tlv8 data.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeStreamingStatus NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ * @brief Characteristic type for supported video stream configuration. The value is a tlv8 data.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeSupportedVideoStreamConfiguration NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ * @brief Characteristic type for supported audio stream configuration. The value is a tlv8 data.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeSupportedAudioStreamConfiguration NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ * @brief Characteristic type for supported RTP stream configuration. The value is a tlv8 data.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeSupportedRTPConfiguration NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ * @brief Characteristic type for selected stream configuration. The value is a tlv8 data.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeSelectedStreamConfiguration NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ * @brief Characteristic type for image snapshot control point. The value is a tlv8 data.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeVolume NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ * @brief Characteristic type for mute control. The value is boolean.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeMute NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ * @brief Characteristic type for camera night vision. The value is boolean.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeNightVision NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ * @brief Characteristic type for camera optical zoom. The value is float.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeOpticalZoom NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ * @brief Characteristic type for camera digital zoom. The value is float.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeDigitalZoom NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ * @brief Characteristic type for camera image rotation. The value is float with valid values: 0, 90, 180 and 270
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeImageRotation NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ * @brief Characteristic type for image mirroring. The value is boolean.
+ */
+HM_EXTERN NSString * const HMCharacteristicTypeImageMirroring NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicWriteAction.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicWriteAction.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicWriteAction.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCharacteristicWriteAction.h	2016-05-28 06:33:50.000000000 +0200
@@ -14,7 +14,7 @@
  * @brief This class is used to represent an entry in an action set that writes a specific
  *        value to a characteristic.
  */
-NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMCharacteristicWriteAction<TargetValueType : id<NSCopying>> : HMAction
 
 - (instancetype)init NS_UNAVAILABLE;
@@ -29,7 +29,7 @@
  * @return Instance object representing the characteristic write action.
  */
 - (instancetype)initWithCharacteristic:(HMCharacteristic *)characteristic
-                           targetValue:(TargetValueType)targetValue NS_DESIGNATED_INITIALIZER __WATCHOS_PROHIBITED;
+                           targetValue:(TargetValueType)targetValue NS_DESIGNATED_INITIALIZER __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief The characteristic associated with the action.
@@ -50,7 +50,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)updateTargetValue:(TargetValueType)targetValue completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)updateTargetValue:(TargetValueType)targetValue completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMError.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMError.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMError.h	2016-02-22 03:52:43.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMError.h	2016-05-28 06:33:50.000000000 +0200
@@ -101,6 +101,6 @@
     HMErrorCodeLocationForHomeDisabled                 NS_ENUM_AVAILABLE_IOS(9_0) = 84,
     HMErrorCodeNotAuthorizedForLocationServices        NS_ENUM_AVAILABLE_IOS(9_0) = 85,
     HMErrorCodeReferToUserManual                       NS_ENUM_AVAILABLE_IOS(9_3) = 86,
-} NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+} NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMEvent.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMEvent.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMEvent.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMEvent.h	2016-05-28 06:33:50.000000000 +0200
@@ -10,7 +10,7 @@
 /*!
  * @brief This class is used to represent a generic HomeKit event.
  */
-NS_CLASS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMEvent : NSObject
 
 /*!
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMEventTrigger.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMEventTrigger.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMEventTrigger.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMEventTrigger.h	2016-05-23 07:54:39.000000000 +0200
@@ -1,7 +1,9 @@
+//
 // HMEventTrigger.h
 // HomeKit
 //
 // Copyright (c) 2015 Apple Inc. All rights reserved.
+//
 
 #import <Foundation/Foundation.h>
 #import <HomeKit/HMTrigger.h>
@@ -17,24 +19,14 @@
  */
 
 /*!
- * @brief Event corresponding to sunrise
- */
-HM_EXTERN NSString * const HMSignificantEventSunrise NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
-
-/*!
- * @brief Event corresponding to sunset
- */
-HM_EXTERN NSString * const HMSignificantEventSunset NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
-
-/*!
  * @brief Specifies the key path for a characteristic in a NSPredicate
  */
-HM_EXTERN NSString * const HMCharacteristicKeyPath NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicKeyPath NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Specifies the key path for a characteristic value in a NSPredicate
  */
-HM_EXTERN NSString * const HMCharacteristicValueKeyPath NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMCharacteristicValueKeyPath NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 
 /*!
@@ -42,7 +34,7 @@
  *
  * @discussion This class represents a trigger that is based on events.
  */
-NS_CLASS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMEventTrigger : HMTrigger
 
 - (instancetype)init NS_UNAVAILABLE;
@@ -62,7 +54,7 @@
  */
 - (instancetype)initWithName:(NSString *)name
                       events:(NSArray<HMEvent *> *)events
-                   predicate:(nullable NSPredicate *)predicate NS_DESIGNATED_INITIALIZER __WATCHOS_PROHIBITED;
+                   predicate:(nullable NSPredicate *)predicate __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief The events associated with the trigger.
@@ -155,7 +147,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)addEvent:(HMEvent *)event completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)addEvent:(HMEvent *)event completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Removes the specified event from the event trigger.
@@ -166,7 +158,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)removeEvent:(HMEvent *)event completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)removeEvent:(HMEvent *)event completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief This method replaces the predicate used to evaluate execution of the action sets associated with the trigger.
@@ -177,7 +169,7 @@
  *                   The NSError provides more information on the status of the request,
  *                   error will be nil on success. 
  */
-- (void)updatePredicate:(nullable NSPredicate *)predicate completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)updatePredicate:(nullable NSPredicate *)predicate completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMHome.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMHome.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMHome.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMHome.h	2016-05-23 08:18:22.000000000 +0200
@@ -29,7 +29,7 @@
  *             all the rooms, zones, service groups, users, triggers, and action sets in
  *             the home.
  */
-NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMHome : NSObject
 
 - (instancetype)init NS_UNAVAILABLE;
@@ -63,7 +63,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)updateName:(NSString *)name completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)updateName:(NSString *)name completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 @end
 
@@ -84,7 +84,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)addAccessory:(HMAccessory *)accessory completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)addAccessory:(HMAccessory *)accessory completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Removes an accessory from the home.
@@ -95,7 +95,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)removeAccessory:(HMAccessory *)accessory completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)removeAccessory:(HMAccessory *)accessory completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Assigns a new room for the accessory.
@@ -111,7 +111,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)assignAccessory:(HMAccessory *)accessory toRoom:(HMRoom *)room completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)assignAccessory:(HMAccessory *)accessory toRoom:(HMRoom *)room completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Queries all services that match the specified types.
@@ -136,7 +136,17 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)unblockAccessory:(HMAccessory *)accessory completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)unblockAccessory:(HMAccessory *)accessory completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
+
+/*!
+ * @brief Find nearby accessories and add them to the home. During this process, each of the accessories added
+ *        to the home is assigned to a room and its services are configured.
+ *
+ * @param completion Block that is invoked once the request is processed.
+ *                   The NSError provides more information on the status of the request, error
+ *                   will be nil on success.
+ */
+- (void)addAndSetupAccessoriesWithCompletionHandler:(void (^)(NSError * __nullable error))completion __IOS_AVAILABLE(10_0) __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 @end
 
@@ -151,7 +161,7 @@
 /*!
  * @brief Array of HMUser objects that represent all users associated with the home.
  */
-@property(readonly, copy, nonatomic) NSArray<HMUser *> *users NS_DEPRECATED_IOS(8_0, 9_0) __WATCHOS_PROHIBITED;
+@property(readonly, copy, nonatomic) NSArray<HMUser *> *users NS_DEPRECATED_IOS(8_0, 9_0) __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Presents a view controller to manage users of the home.
@@ -164,7 +174,7 @@
  *                   will be nil on success. If the user does not have administrator privileges the error code will be set to
  *                   HMErrorCodeInsufficientPrivileges.
  */
-- (void)manageUsersWithCompletionHandler:(void (^)(NSError * __nullable error))completion NS_AVAILABLE_IOS(9_0) __WATCHOS_PROHIBITED;
+- (void)manageUsersWithCompletionHandler:(void (^)(NSError * __nullable error))completion NS_AVAILABLE_IOS(9_0) __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Adds a user to the home.
@@ -175,7 +185,7 @@
  *                   will be nil on success. The userInfo dictionary will contain the HMUserFailedAccessoriesKey which provides
  *                   more details on the accessories that failed to add the user.
  */
-- (void)addUserWithCompletionHandler:(void (^)(HMUser * __nullable user, NSError * __nullable error))completion NS_DEPRECATED_IOS(8_0, 9_0) __WATCHOS_PROHIBITED;
+- (void)addUserWithCompletionHandler:(void (^)(HMUser * __nullable user, NSError * __nullable error))completion NS_DEPRECATED_IOS(8_0, 9_0) __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Removes a user from the home.
@@ -187,7 +197,7 @@
  *                   will be nil on success. The userInfo dictionary will contain the HMUserFailedAccessoriesKey which provides
  *                   more details on the accessories that failed to remove the user.
  */
-- (void)removeUser:(HMUser *)user completionHandler:(void (^)(NSError * __nullable error))completion NS_DEPRECATED_IOS(8_0, 9_0) __WATCHOS_PROHIBITED;
+- (void)removeUser:(HMUser *)user completionHandler:(void (^)(NSError * __nullable error))completion NS_DEPRECATED_IOS(8_0, 9_0) __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Retrieve the access level of the user associated with the home.
@@ -214,7 +224,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)addRoomWithName:(NSString *)roomName completionHandler:(void (^)(HMRoom * __nullable room, NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)addRoomWithName:(NSString *)roomName completionHandler:(void (^)(HMRoom * __nullable room, NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Removes a room from the home. 
@@ -229,7 +239,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)removeRoom:(HMRoom *)room completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)removeRoom:(HMRoom *)room completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief This method returns a room that represents the entire home. This can be used to assign a room
@@ -259,7 +269,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)addZoneWithName:(NSString *)zoneName completionHandler:(void (^)(HMZone * __nullable zone, NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)addZoneWithName:(NSString *)zoneName completionHandler:(void (^)(HMZone * __nullable zone, NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Removes a zone from the home.
@@ -270,7 +280,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)removeZone:(HMZone *)zone completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)removeZone:(HMZone *)zone completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 @end
 
@@ -292,7 +302,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)addServiceGroupWithName:(NSString *)serviceGroupName completionHandler:(void (^)(HMServiceGroup * __nullable group, NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)addServiceGroupWithName:(NSString *)serviceGroupName completionHandler:(void (^)(HMServiceGroup * __nullable group, NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Removes a service group from the home.
@@ -303,7 +313,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)removeServiceGroup:(HMServiceGroup *)group completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)removeServiceGroup:(HMServiceGroup *)group completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 @end
 
@@ -325,7 +335,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)addActionSetWithName:(NSString *)actionSetName completionHandler:(void (^)(HMActionSet * __nullable actionSet, NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)addActionSetWithName:(NSString *)actionSetName completionHandler:(void (^)(HMActionSet * __nullable actionSet, NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Removes an existing action set from the home.
@@ -336,7 +346,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)removeActionSet:(HMActionSet *)actionSet completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)removeActionSet:(HMActionSet *)actionSet completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Executes all the actions within an action set.
@@ -384,7 +394,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)addTrigger:(HMTrigger *)trigger completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)addTrigger:(HMTrigger *)trigger completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Removes a trigger from the home. If the trigger is active, they are automatically deactivated.
@@ -395,7 +405,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)removeTrigger:(HMTrigger *)trigger completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)removeTrigger:(HMTrigger *)trigger completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 @end
 
@@ -404,7 +414,7 @@
  * @brief This delegate receives update on the various accessories, action sets, groups and triggers 
  *        managed in the home.
  */
-NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @protocol HMHomeDelegate <NSObject>
 
 @optional
@@ -697,6 +707,6 @@
  *             corresponding to the dictionary key is an NSError that provides more details on the
  *             underlying error for that accessory.
  */
-HM_EXTERN NSString * const HMUserFailedAccessoriesKey NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMUserFailedAccessoriesKey NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMHomeAccessControl.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMHomeAccessControl.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMHomeAccessControl.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMHomeAccessControl.h	2016-05-28 06:33:50.000000000 +0200
@@ -10,7 +10,7 @@
 /*!
  * @brief Represents the access control of a user associated with a home.
  */
-NS_CLASS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMHomeAccessControl : NSObject
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMHomeManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMHomeManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMHomeManager.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMHomeManager.h	2016-05-25 04:59:53.000000000 +0200
@@ -17,7 +17,7 @@
  *
  * @discussion This class is responsible for managing a collection of homes. 
  */
-NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMHomeManager : NSObject
 
 /*!
@@ -48,7 +48,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)updatePrimaryHome:(HMHome *)home completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)updatePrimaryHome:(HMHome *)home completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Adds a new home to the collection.
@@ -60,7 +60,7 @@
  *                   will be nil on success.
  *
  */
-- (void)addHomeWithName:(NSString *)homeName completionHandler:(void (^)(HMHome * __nullable home, NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)addHomeWithName:(NSString *)homeName completionHandler:(void (^)(HMHome * __nullable home, NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Removes an existing home from the collection.
@@ -71,14 +71,14 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)removeHome:(HMHome *)home completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)removeHome:(HMHome *)home completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 @end
 
 /*!
  * @brief This delegate receives updates on homes being managed via the home manager.
  */
-NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @protocol HMHomeManagerDelegate <NSObject>
 
 @optional
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMLocationEvent.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMLocationEvent.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMLocationEvent.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMLocationEvent.h	2016-05-28 06:33:50.000000000 +0200
@@ -16,7 +16,7 @@
  * @brief This class represents an event that is evaluated based on entry to and/or
  *        exit from a Region
  */
-NS_CLASS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMLocationEvent : HMEvent
 
 - (instancetype)init NS_UNAVAILABLE;
@@ -28,7 +28,7 @@
  *
  * @return Instance object representing the location event.
  */
-- (instancetype)initWithRegion:(CLRegion *)region __WATCHOS_PROHIBITED;
+- (instancetype)initWithRegion:(CLRegion *)region __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Region on which events are triggered based on the properties notifyOnEntry and notifyOnExit.
@@ -45,7 +45,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)updateRegion:(CLRegion *)region completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)updateRegion:(CLRegion *)region completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMRoom.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMRoom.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMRoom.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMRoom.h	2016-05-28 06:33:50.000000000 +0200
@@ -12,7 +12,7 @@
 /*!
  * @brief This class describes a room in the home.
  */
-NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMRoom : NSObject
 
 - (instancetype)init NS_UNAVAILABLE;
@@ -42,7 +42,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)updateName:(NSString *)name completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)updateName:(NSString *)name completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMService.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMService.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMService.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMService.h	2016-05-25 04:59:53.000000000 +0200
@@ -19,7 +19,7 @@
  *             A service is composed of one or more characteristics that can be 
  *             modified.
  */
-NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMService : NSObject
 
 /*!
@@ -73,6 +73,21 @@
 @property(readonly, getter=isUserInteractive, nonatomic) BOOL userInteractive NS_AVAILABLE_IOS(9_0);
 
 /*!
+ * @brief Indicates if this services is the primary service.
+ *
+ * @discussion Applications should use this property to show the primary service on the accessory.
+ */
+@property(readonly, getter=isPrimaryService, nonatomic) BOOL primaryService NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ * @brief Array of HMService objects that represents all the services that the service links to.
+ *  
+ * @discussion Applications should use this property to show logical grouping of services on the accessory.
+ *             linkedServices will be nil when the service does not link to any other services.
+ */
+@property(readonly, copy, nonatomic) NSArray<HMService *> * __nullable linkedServices NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+
+/*!
  * @brief This method is used to change the name of the service.
  *
  * @param name New name for the service.
@@ -83,7 +98,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)updateName:(NSString *)name completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)updateName:(NSString *)name completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief This method is used to set up the service type of the device connected to a switch or an outlet.
@@ -98,7 +113,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)updateAssociatedServiceType:(nullable NSString *)serviceType completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)updateAssociatedServiceType:(nullable NSString *)serviceType completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMServiceGroup.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMServiceGroup.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMServiceGroup.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMServiceGroup.h	2016-05-28 06:33:50.000000000 +0200
@@ -16,7 +16,7 @@
  *             This allows for association of a set of accessory services into a group.
  *             Eg. A collection of lights can be grouped as the "Desk Lamps" service group.
  */
-NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMServiceGroup : NSObject
 
 - (instancetype)init NS_UNAVAILABLE;
@@ -45,7 +45,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)updateName:(NSString *)name completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)updateName:(NSString *)name completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Adds an service to this service group. The service and the group must be part of the same
@@ -58,7 +58,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)addService:(HMService *)service completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)addService:(HMService *)service completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Removes an service from this service group.
@@ -69,7 +69,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)removeService:(HMService *)service completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)removeService:(HMService *)service completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMServiceTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMServiceTypes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMServiceTypes.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMServiceTypes.h	2016-05-23 08:18:23.000000000 +0200
@@ -18,136 +18,141 @@
 /*!
  * @brief Service type for lightbulb.
  */
-HM_EXTERN NSString * const HMServiceTypeLightbulb NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeLightbulb NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for switch.
  */
-HM_EXTERN NSString * const HMServiceTypeSwitch NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeSwitch NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for thermostat.
  */
-HM_EXTERN NSString * const HMServiceTypeThermostat NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeThermostat NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for garage door opener.
  */
-HM_EXTERN NSString * const HMServiceTypeGarageDoorOpener NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeGarageDoorOpener NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for accessory information.
  */
-HM_EXTERN NSString * const HMServiceTypeAccessoryInformation NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeAccessoryInformation NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for fan.
  */
-HM_EXTERN NSString * const HMServiceTypeFan NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeFan NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for outlet.
  */
-HM_EXTERN NSString * const HMServiceTypeOutlet NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeOutlet NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for lock mechanism.
  */
-HM_EXTERN NSString * const HMServiceTypeLockMechanism NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeLockMechanism NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for lock management.
  */
-HM_EXTERN NSString * const HMServiceTypeLockManagement NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeLockManagement NS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for air quality sensor.
  */
-HM_EXTERN NSString * const HMServiceTypeAirQualitySensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeAirQualitySensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for battery.
  */
-HM_EXTERN NSString * const HMServiceTypeBattery NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeBattery NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for carbon dioxide sensor.
  */
-HM_EXTERN NSString * const HMServiceTypeCarbonDioxideSensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeCarbonDioxideSensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for carbon monoxide sensor.
  */
-HM_EXTERN NSString * const HMServiceTypeCarbonMonoxideSensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeCarbonMonoxideSensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for contact sensor.
  */
-HM_EXTERN NSString * const HMServiceTypeContactSensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeContactSensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for door.
  */
-HM_EXTERN NSString * const HMServiceTypeDoor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeDoor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for humidity sensor.
  */
-HM_EXTERN NSString * const HMServiceTypeHumiditySensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeHumiditySensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for leak sensor.
  */
-HM_EXTERN NSString * const HMServiceTypeLeakSensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeLeakSensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for light sensor.
  */
-HM_EXTERN NSString * const HMServiceTypeLightSensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeLightSensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for motion sensor.
  */
-HM_EXTERN NSString * const HMServiceTypeMotionSensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeMotionSensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for occupancy sensor.
  */
-HM_EXTERN NSString * const HMServiceTypeOccupancySensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeOccupancySensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for security system.
  */
-HM_EXTERN NSString * const HMServiceTypeSecuritySystem NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeSecuritySystem NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for stateful programmable switch.
  */
-HM_EXTERN NSString * const HMServiceTypeStatefulProgrammableSwitch NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeStatefulProgrammableSwitch NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for stateless programmable switch.
  */
-HM_EXTERN NSString * const HMServiceTypeStatelessProgrammableSwitch NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeStatelessProgrammableSwitch NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for smoke sensor.
  */
-HM_EXTERN NSString * const HMServiceTypeSmokeSensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeSmokeSensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for temperature sensor.
  */
-HM_EXTERN NSString * const HMServiceTypeTemperatureSensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeTemperatureSensor NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for window.
  */
-HM_EXTERN NSString * const HMServiceTypeWindow NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeWindow NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
 
 /*!
  * @brief Service type for window covering.
  */
-HM_EXTERN NSString * const HMServiceTypeWindowCovering NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0);
+HM_EXTERN NSString * const HMServiceTypeWindowCovering NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
+
+HM_EXTERN NSString * const HMServiceTypeCameraRTPStreamManagement NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+HM_EXTERN NSString * const HMServiceTypeCameraControl NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+HM_EXTERN NSString * const HMServiceTypeMicrophone NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
+HM_EXTERN NSString * const HMServiceTypeSpeaker NS_AVAILABLE_IOS(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMSignificantEvents.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMSignificantEvents.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMSignificantEvents.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMSignificantEvents.h	2016-05-28 06:33:50.000000000 +0200
@@ -0,0 +1,25 @@
+//
+//  HMSignificantEvents.h
+//  HomeKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <HomeKit/HMDefines.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+/*!
+ * @brief Event corresponding to sunrise
+ */
+HM_EXTERN NSString * const HMSignificantEventSunrise NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
+
+/*!
+ * @brief Event corresponding to sunset
+ */
+HM_EXTERN NSString * const HMSignificantEventSunset NS_AVAILABLE_IOS(9_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0);
+
+NS_ASSUME_NONNULL_END
+
+
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMTimerTrigger.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMTimerTrigger.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMTimerTrigger.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMTimerTrigger.h	2016-05-23 07:54:39.000000000 +0200
@@ -13,7 +13,7 @@
  *
  * @discussion This class represents a trigger that is based on timers.
  */
-NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMTimerTrigger : HMTrigger
 
 - (instancetype)init NS_UNAVAILABLE;
@@ -48,7 +48,8 @@
                     fireDate:(NSDate *)fireDate
                     timeZone:(nullable NSTimeZone *)timeZone
                   recurrence:(nullable NSDateComponents *)recurrence
-          recurrenceCalendar:(nullable NSCalendar *)recurrenceCalendar NS_DESIGNATED_INITIALIZER __WATCHOS_PROHIBITED;
+          recurrenceCalendar:(nullable NSCalendar *)recurrenceCalendar NS_DESIGNATED_INITIALIZER __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
+
 
 /*!
  * @brief Specifies when, in an absolute time, the trigger should fire the first time.
@@ -98,7 +99,7 @@
  *                   error will be nil on success. HMErrorCodeDateMustBeOnSpecifiedBoundaries will
  *                   be returned if the fireDate includes a seconds value other than 0.
  */
-- (void)updateFireDate:(NSDate *)fireDate completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)updateFireDate:(NSDate *)fireDate completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief This method is used to change the time zone of the fire date of a timer trigger.
@@ -110,7 +111,7 @@
  *                   The NSError provides more information on the status of the request,
  *                   error will be nil on success.
  */
-- (void)updateTimeZone:(nullable NSTimeZone *)timeZone completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)updateTimeZone:(nullable NSTimeZone *)timeZone completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief This method is used to change the recurrence interval for a timer trigger.
@@ -129,7 +130,8 @@
  *                   HMErrorCodeRecurrenceTooLarge is returned if the recurrence interval is
  *                   greater than 5 weeks. *                   error will be nil on success.
  */
-- (void)updateRecurrence:(nullable NSDateComponents *)recurrence completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)updateRecurrence:(nullable NSDateComponents *)recurrence
+       completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMTrigger.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMTrigger.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMTrigger.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMTrigger.h	2016-05-28 06:33:50.000000000 +0200
@@ -16,7 +16,7 @@
  * @discussion This class describes a trigger which is an event that can
  *             be used to execute one or more action sets when the event fires.
  */
-NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMTrigger : NSObject
 
 - (instancetype)init NS_UNAVAILABLE;
@@ -57,7 +57,7 @@
  * @param completion Block that is invoked once the request is processed.
  *                   The NSError provides more information on the status of the request.
  */
-- (void)updateName:(NSString *)name completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)updateName:(NSString *)name completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Registers an action set to be executed when the trigger is fired.
@@ -68,7 +68,7 @@
  * @param completion Block that is invoked once the request is processed. 
  *                   The NSError provides more information on the status of the request.
  */
-- (void)addActionSet:(HMActionSet *)actionSet completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)addActionSet:(HMActionSet *)actionSet completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief De-registers an action set from the trigger.
@@ -78,7 +78,7 @@
  * @param completion Block that is invoked once the request is processed. 
  *                   The NSError provides more information on the status of the request.
  */
-- (void)removeActionSet:(HMActionSet *)actionSet completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)removeActionSet:(HMActionSet *)actionSet completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Enables or disables the trigger. 
@@ -95,7 +95,7 @@
  * @param completion Block that is invoked once the request is processed. 
  *                   The NSError provides more information on the status of the request.
  */
-- (void)enable:(BOOL)enable completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)enable:(BOOL)enable completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMUser.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMUser.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMUser.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMUser.h	2016-05-28 06:33:50.000000000 +0200
@@ -14,7 +14,7 @@
 /*!
  * @brief This class describes a user in the home.
  */
-NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMUser : NSObject
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMZone.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMZone.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMZone.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMZone.h	2016-05-28 06:33:50.000000000 +0200
@@ -17,7 +17,7 @@
  *             Eg. "Living Room" and "Kitchen" rooms can be grouped together
  *             in the "Downstairs" zone.
  */
-NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(__WATCHOS_2_0)
+NS_CLASS_AVAILABLE_IOS(8_0) __WATCHOS_AVAILABLE(2_0) __TVOS_AVAILABLE(10_0)
 @interface HMZone : NSObject
 
 - (instancetype)init NS_UNAVAILABLE;
@@ -46,7 +46,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)updateName:(NSString *)name completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)updateName:(NSString *)name completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Adds a room to a zone.
@@ -60,7 +60,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)addRoom:(HMRoom *)room completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)addRoom:(HMRoom *)room completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 /*!
  * @brief Removes a room from the zone.
@@ -71,7 +71,7 @@
  *                   The NSError provides more information on the status of the request, error
  *                   will be nil on success.
  */
-- (void)removeRoom:(HMRoom *)room completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED;
+- (void)removeRoom:(HMRoom *)room completionHandler:(void (^)(NSError * __nullable error))completion __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HomeKit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HomeKit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HomeKit.h	2015-08-14 08:30:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HomeKit.h	2016-05-28 06:33:50.000000000 +0200
@@ -27,3 +27,22 @@
 #import <HomeKit/HMLocationEvent.h>
 #import <HomeKit/HMEventTrigger.h>
 #import <HomeKit/HMError.h>
+#import <HomeKit/HMAccessoryProfile.h>
+#import <HomeKit/HMSignificantEvents.h>
+
+#if __has_include(<UIKit/UIView.h>)
+#import <HomeKit/HMCameraView.h>
+#endif
+#import <HomeKit/HMAccessory+Camera.h>
+#import <HomeKit/HMCameraProfile.h>
+#import <HomeKit/HMCameraControl.h>
+
+#import <HomeKit/HMCameraStreamControl.h>
+#import <HomeKit/HMCameraStream.h>
+
+#import <HomeKit/HMCameraSnapshotControl.h>
+#import <HomeKit/HMCameraSnapshot.h>
+
+#import <HomeKit/HMCameraSettingsControl.h>
+#import <HomeKit/HMCameraAudioControl.h>
+

```