#GameKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKCloudPlayer.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKCloudPlayer.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKCloudPlayer.h	2016-07-25 08:50:20.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKCloudPlayer.h	2016-08-06 09:57:16.000000000 +0200
@@ -2,11 +2,13 @@
 //  GKCloudPlayer.h
 //  Game Center
 //
-//  Copyright 2012-2016 Apple Inc. All rights reserved.
+//  Copyright 2016 Apple Inc. All rights reserved.
 //
 
 #import <GameKit/GKBasePlayer.h>
 NS_ASSUME_NONNULL_BEGIN
+NS_CLASS_AVAILABLE(10_12, 10_0) __WATCHOS_PROHIBITED
+
 @interface GKCloudPlayer : GKBasePlayer
 #if !__OBJC2__
 {
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSession.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSession.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSession.h	2016-07-23 02:15:44.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSession.h	2016-08-06 09:48:20.000000000 +0200
@@ -19,6 +19,7 @@
 };
 
 NS_ASSUME_NONNULL_BEGIN
+NS_CLASS_AVAILABLE(10_12, 10_0) __WATCHOS_PROHIBITED
 
 @interface GKGameSession : NSObject
 #if !__OBJC2__
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionEventListener.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionEventListener.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionEventListener.h	2016-07-25 08:50:20.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionEventListener.h	2016-08-06 09:57:16.000000000 +0200
@@ -10,18 +10,18 @@
 
 @protocol GKGameSessionEventListener <NSObject>
 @optional
-- (void)session:(GKGameSession *)session didAddPlayer:(GKCloudPlayer *)player;
-- (void)session:(GKGameSession *)session didRemovePlayer:(GKCloudPlayer *)player;
-- (void)session:(GKGameSession *)session player:(GKCloudPlayer *)player didChangeConnectionState:(GKConnectionState)newState;
-- (void)session:(GKGameSession *)session player:(GKCloudPlayer *)player didSaveData:(NSData *)data;
-- (void)session:(GKGameSession *)session didReceiveData:(NSData *)data fromPlayer:(GKCloudPlayer *)player;
-- (void)session:(GKGameSession *)session didReceiveMessage:(NSString *)message withData:(NSData *)data fromPlayer:(GKCloudPlayer *)player;
+- (void)session:(GKGameSession *)session didAddPlayer:(GKCloudPlayer *)player NS_AVAILABLE(10_12, 10_0) __WATCHOS_PROHIBITED;
+- (void)session:(GKGameSession *)session didRemovePlayer:(GKCloudPlayer *)player NS_AVAILABLE(10_12, 10_0) __WATCHOS_PROHIBITED;
+- (void)session:(GKGameSession *)session player:(GKCloudPlayer *)player didChangeConnectionState:(GKConnectionState)newState NS_AVAILABLE(10_12, 10_0) __WATCHOS_PROHIBITED;
+- (void)session:(GKGameSession *)session player:(GKCloudPlayer *)player didSaveData:(NSData *)data NS_AVAILABLE(10_12, 10_0) __WATCHOS_PROHIBITED;
+- (void)session:(GKGameSession *)session didReceiveData:(NSData *)data fromPlayer:(GKCloudPlayer *)player NS_AVAILABLE(10_12, 10_0) __WATCHOS_PROHIBITED;
+- (void)session:(GKGameSession *)session didReceiveMessage:(NSString *)message withData:(NSData *)data fromPlayer:(GKCloudPlayer *)player NS_AVAILABLE(10_12, 10_0) __WATCHOS_PROHIBITED;
 
 @end
 
 @interface GKGameSession (GKGameSessionEventListener)
-+ (void)addEventListener:(NSObject<GKGameSessionEventListener> *)listener;
-+ (void)removeEventListener:(NSObject<GKGameSessionEventListener> *)listener;
++ (void)addEventListener:(NSObject<GKGameSessionEventListener> *)listener NS_SWIFT_NAME(add(listener:)) NS_AVAILABLE(10_12, 10_0) __WATCHOS_PROHIBITED;
++ (void)removeEventListener:(NSObject<GKGameSessionEventListener> *)listener NS_SWIFT_NAME(remove(listener:)) NS_AVAILABLE(10_12, 10_0) __WATCHOS_PROHIBITED;
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionSharingViewController.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionSharingViewController.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionSharingViewController.h	2016-07-25 08:50:20.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionSharingViewController.h	2016-08-06 09:57:16.000000000 +0200
@@ -1,9 +1,8 @@
 //
 //  GKGameSessionSharingViewController.h
-//  GameCenterUI
+//  Game Center
 //
-//  Created by Alan Berfield on 2/20/16.
-//  Copyright © 2016 Apple Inc. All rights reserved.
+//  Copyright 2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>

```