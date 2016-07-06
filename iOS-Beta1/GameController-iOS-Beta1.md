#GameController.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCController.h	2015-10-03 02:19:26.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCController.h	2016-05-04 00:21:22.000000000 +0200
@@ -35,6 +35,44 @@
 GAMECONTROLLER_EXTERN NSString *const GCControllerDidDisconnectNotification;
 
 /**
+ A view controller subclass that allows fine grained control of the user interface system's handling
+ of game controller events. Set an instance of this class as your root view controller if you intend
+ to use GCController APIs for handling game controllers.
+ */
+#if TARGET_OS_IPHONE || TARGET_OS_TV
+NS_CLASS_AVAILABLE(10_11, 9_0)
+@interface GCEventViewController : UIViewController
+#else
+NS_CLASS_AVAILABLE(10_11, 9_0)
+@interface GCEventViewController : NSViewController
+#endif
+
+/**
+ Controllers can be used to control the general UIKit user interface and for many views that is
+ the default behavior. By using a controller event view controller you get fine grained control
+ over whether the controller events go trough the UIEvent & UIResponder chain, or if they are
+ decoupled from the UI and all incoming data is served via GCController.
+
+ Defaults to NO - suppressing UIEvents from game controllers and presenting them via the GCController
+ API whilst this controller's view or any of it's subviews are the first responders. If you are not
+ using any UIView components or UIEvents in your application you should leave this as NO and process
+ your game controller events via the normal GCController API.
+ 
+ If set to YES the controller input will start flowing through UIEvent and the UIResponder
+ chain will be used. This gives you fine grained control over the event handling of the
+ controlled view and its subviews. You should stop using GCController instances and the corresponding
+ profiles if you no longer need to read input from them.
+ 
+ Note that unlike UIView.userInteractionEnabled this only controls the flow of game controller events.
+ 
+ @see GCController
+ @see UIView.userInteractionEnabled
+ */
+@property (nonatomic, assign) BOOL controllerUserInteractionEnabled;
+
+@end
+
+/**
  This is the player index that a connected controller will have if it has never been assigned a player index on the current system.
  Controllers retain the player index they have been assigned between game sessions, so if you wish to unset the player index of a
  controller set it back to this value.
@@ -84,9 +122,9 @@
  @see GCMotion.valueChangedHandler
  */
 #if defined(OS_OBJECT_USE_OBJC) && OS_OBJECT_USE_OBJC==1
-@property (retain) dispatch_queue_t handlerQueue NS_AVAILABLE(10_11, 9_0);
+@property (retain) dispatch_queue_t handlerQueue;
 #else
-@property (assign) dispatch_queue_t handlerQueue NS_AVAILABLE(10_11, 9_0);
+@property (assign) dispatch_queue_t handlerQueue;
 #endif
 
 /**
@@ -103,15 +141,13 @@
 @property (nonatomic, readonly, getter = isAttachedToDevice) BOOL attachedToDevice;
 
 /**
- A player index for the controller, defaults to GCControllerPlayerIndexUnset, unless the controller previously had
- a player index assigned to it on the current user's system.
+ A player index for the controller, defaults to GCControllerPlayerIndexUnset.
  
  This can be set both for the application to keep track of controllers and as a signal to make a controller display a player
  index on a set of LEDs or some other mechanism.
  
- A controller is not guranteed to have a visual display of the playerIndex, but the API will keep track of the playerIndex
- for a controller while connected and in between being disconnected and connected again. Thus playerIndex persists for a controller
- with regards to a system. This makes it useful for persisting player-controller assignments across game sessions.
+ A controller is not guranteed to have a visual display of the playerIndex, playerIndex does not persist for a controller
+ with regards to a system.
  
  Negative values less than GCControllerPlayerIndexUnset will just map back to GCControllerPlayerIndexUnset when read back.
  */
@@ -134,6 +170,7 @@
  @see motion
  */
 @property (nonatomic, retain, readonly, nullable) GCGamepad *gamepad;
+@property (nonatomic, retain, readonly, nullable) GCMicroGamepad *microGamepad;
 @property (nonatomic, retain, readonly, nullable) GCExtendedGamepad *extendedGamepad;
 
 /**
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCGamepad.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCGamepad.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCGamepad.h	2015-10-03 02:19:26.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCGamepad.h	2016-05-25 05:37:07.000000000 +0200
@@ -20,6 +20,7 @@
  A profile maps the hardware notion of a controller into a logical controller. One that a developer can design for
  and depend on, no matter the underlying hardware.
  */
+NS_CLASS_DEPRECATED(10_9, 10_12, 7_0, 10_0)
 GAMECONTROLLER_EXPORT
 @interface GCGamepad : NSObject
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCMicroGamepad.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCMicroGamepad.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCMicroGamepad.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCMicroGamepad.h	2016-05-27 07:08:34.000000000 +0200
@@ -0,0 +1,102 @@
+//
+//  GCMicroGamepad.h
+//  GameController
+//
+//  Copyright (c) 2014 Apple Inc. All rights reserved.
+//
+
+#import <GameController/GameController.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class GCController;
+@class GCMicroGamepadSnapshot;
+
+/**
+ Micro Gamepad profile.
+ 
+ All controller profiles provide a base level of information about the controller they belong to.
+ 
+ A profile maps the hardware notion of a controller into a logical controller. One that a developer can design for
+ and depend on, no matter the underlying hardware.
+ */
+NS_CLASS_AVAILABLE(10_11, 9_0)
+@interface GCMicroGamepad : NSObject
+
+/**
+ A profile keeps a reference to the controller that this profile is mapping input from.
+ */
+#if !__has_feature(objc_arc)
+@property (nonatomic, readonly, assign) GCController *controller;
+#else
+@property (nonatomic, readonly, weak) GCController *controller;
+#endif
+
+/**
+ Set this block if you want to be notified when a value on a element changed. If multiple elements have changed this block will be called
+ for each element that changed. As elements in a collection, such as the axis in a dpad, tend to change at the same time and thus
+ will only call this once with the collection as the element.
+ 
+ @param gamepad this gamepad that is being used to map the raw input data into logical values on controller elements such as the dpad or the buttons.
+ @param element the element that has been modified.
+ */
+typedef void (^GCMicroGamepadValueChangedHandler)(GCMicroGamepad *gamepad, GCControllerElement *element);
+@property (nonatomic, copy, nullable) GCMicroGamepadValueChangedHandler valueChangedHandler;
+
+/**
+ Polls the state vector of the controller and saves it to a snapshot. The snapshot is stored in a device independent
+ format that can be serialized and used at a later date. This is useful for features such as quality assurance,
+ save game or replay functionality among many.
+ 
+ If your application is heavily multithreaded this may also be useful to guarantee atomicity of input handling as
+ a snapshot will not change based on user input once it is taken.
+ 
+ @see GCMicroGamepadSnapshot
+ */
+- (GCMicroGamepadSnapshot *)saveSnapshot;
+
+/**
+ Optionally analog in the Micro profile. All the elements of this directional input are either analog or digital.
+ */
+@property (nonatomic, readonly, retain) GCControllerDirectionPad *dpad;
+
+/**
+ The Micro profile has two buttons that are optionally analog in the Micro profile.
+ Button A is the primary action button, it indicates affirmative action and should be used to advance in menus
+ or perform the primary action in gameplay.
+ */
+@property (nonatomic, readonly, retain) GCControllerButtonInput *buttonA;
+
+/**
+ Button X is the secondary action button, it indicates an alternate affirmative action and should be used to perform
+ a secondary action. If there is no secondary action it should be used as equivalent to buttonA.
+ 
+ Unlike on other profiles there is no negative button on this profile. Instead the GCController's pause handler should be
+ used to present menu content or to retreat in a menu flow.
+ @see buttonA
+ @see GCController.controllerPausedHandler
+ */
+@property (nonatomic, readonly, retain) GCControllerButtonInput *buttonX;
+
+/**
+ The Micro profile can use the raw position values of the touchpad on the remote as D-pad values, or it can create a virtual dpad centered around the first conact point with the surface.
+ 
+ If NO; a smaller sliding window is created around the initial touch point and subsequent movement is relative to that center. Movement outside the window will slide the window with it to re-center it. This is great for surfaces where there is no clear sense of a middle and drift over time is an issue.
+ 
+ If YES; the absolute values are used and any drift will have to managed manually either through user traning or by a developer using the dpad.
+ 
+ The default value for this property is NO, meaing a sliding window is used for the dpad.
+ */
+@property (nonatomic, assign) BOOL reportsAbsoluteDpadValues;
+
+/**
+ Allows the Micro profile to monitor the orientation of the controller, if the controller is positioned in landscape orientation, D-pad input values will be transposed 90 degrees to match the new orientation.
+ 
+ The default value for this property is NO.
+ */
+@property (nonatomic, assign) BOOL allowsRotation;
+
+@end
+
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCMicroGamepadSnapshot.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCMicroGamepadSnapshot.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCMicroGamepadSnapshot.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCMicroGamepadSnapshot.h	2016-05-25 05:37:07.000000000 +0200
@@ -0,0 +1,66 @@
+//
+//  GCMicroGamepadSnapshot.h
+//  GameController
+//
+//  Copyright (c) 2014 Apple Inc. All rights reserved.
+//
+
+#import <GameController/GameController.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+/**
+ A GCMicroGamepadSnapshot snapshot is a concrete GCMicroGamepad implementation. It can be used directly in an
+ application to implement controller input replays. It is also returned as the result of polling
+ a controller.
+ 
+ The current snapshotData is readily available to access as NSData. A developer can serialize this to any
+ destination necessary using the NSData API.
+ 
+ The data contains some version of a GCMicroGamepadSnapShotData structure.
+ 
+ @see -[GCMicroGamepad saveSnapshot]
+ */
+GAMECONTROLLER_EXPORT
+@interface GCMicroGamepadSnapshot : GCMicroGamepad
+@property (atomic, copy) NSData *snapshotData;
+
+- (instancetype)initWithSnapshotData:(NSData *)data;
+- (instancetype)initWithController:(GCController *)controller snapshotData:(NSData *)data;
+
+@end
+
+#pragma pack(push, 1)
+typedef struct {
+    // Standard information
+    uint16_t version; //0x0100
+    uint16_t size;    //sizeof(GCMicroGamepadSnapShotDataV100) or larger
+    
+    // Standard gamepad data
+    // Axes in the range [-1.0, 1.0]
+    float dpadX;
+    float dpadY;
+    
+    // Buttons in the range [0.0, 1.0]
+    float buttonA;
+    float buttonX;
+    
+} GCMicroGamepadSnapShotDataV100;
+#pragma pack(pop)
+
+/**Fills out a v100 snapshot from any compatible NSData source
+ 
+ @return NO if data is nil, snapshotData is nil or the contents of data does not contain a compatible snapshot. YES for all other cases.
+ */
+GAMECONTROLLER_EXPORT
+BOOL GCMicroGamepadSnapShotDataV100FromNSData(GCMicroGamepadSnapShotDataV100 *__nullable snapshotData, NSData *__nullable data);
+
+/**Creates an NSData object from a v100 snapshot.
+ If the version and size is not set in the snapshot the data will automatically have version 0x100 and sizeof(GCMicroGamepadSnapShotDataV100) set as the values implicitly.
+ 
+ @return nil if the snapshot is NULL, otherwise an NSData instance compatible with GCGamepadSnapshot.snapshotData
+ */
+GAMECONTROLLER_EXPORT
+NSData *__nullable NSDataFromGCMicroGamepadSnapShotDataV100(GCMicroGamepadSnapShotDataV100 *__nullable snapshotData);
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCMotion.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCMotion.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCMotion.h	2015-10-03 02:19:26.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCMotion.h	2016-05-25 05:21:23.000000000 +0200
@@ -134,13 +134,19 @@
 
 /**
  The current attitude of the controller.
+ 
+ @note Remotes can not determine a stable attitude so the values will be (0,0,0,1) at all times.
+ @see GCMicroGamepad
  */
-@property (nonatomic, assign, readonly) GCQuaternion attitude;
+@property (nonatomic, assign, readonly) GCQuaternion attitude __TVOS_UNAVAILABLE;
 
 /**
  The current rotation rate of the controller.
+ 
+ @note Remotes can not determine a stable rotation rate so the values will be (0,0,0) at all times.
+ @see GCMicroGamepad
  */
-@property (nonatomic, assign, readonly) GCRotationRate rotationRate;
+@property (nonatomic, assign, readonly) GCRotationRate rotationRate __TVOS_UNAVAILABLE;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GameController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GameController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GameController.h	2015-10-03 02:19:26.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GameController.h	2016-05-25 05:37:07.000000000 +0200
@@ -34,4 +34,7 @@
 #import <GameController/GCExtendedGamepad.h>
 #import <GameController/GCExtendedGamepadSnapshot.h>
 
+#import <GameController/GCMicroGamepad.h>
+#import <GameController/GCMicroGamepadSnapshot.h>
+
 #import <GameController/GCController.h>

```