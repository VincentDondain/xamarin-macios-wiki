#GameKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKAchievement.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKAchievement.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKAchievement.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKAchievement.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKAchievement.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
@@ -49,7 +49,7 @@
 @property(assign, NS_NONATOMIC_IOSONLY) BOOL showsCompletionBanner NS_AVAILABLE(10_8, 5_0);             // A banner will be momentarily displayed after reporting a completed achievement
 
 // The identifier of the player that earned the achievement.
-@property(readonly, retain, NS_NONATOMIC_IOSONLY) GKPlayer *player NS_AVAILABLE(10_10, 8_0);
+@property(readonly, retain, nullable, NS_NONATOMIC_IOSONLY) GKPlayer *player NS_AVAILABLE(10_10, 8_0);
 
 @end
 
@@ -61,4 +61,4 @@
 @property(readonly, copy, NS_NONATOMIC_IOSONLY) NSString *playerID NS_DEPRECATED_IOS(7_0, 8_0, "use player") ;
 
 @end
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKAchievementDescription.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKAchievementDescription.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKAchievementDescription.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKAchievementDescription.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKAchievementDescription.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKAchievementViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKAchievementViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKAchievementViewController.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKAchievementViewController.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKAchievementViewController.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 #if TARGET_OS_IPHONE
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKBasePlayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKBasePlayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKBasePlayer.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKBasePlayer.h	2016-05-25 08:40:16.000000000 +0200
@@ -0,0 +1,19 @@
+//
+//  GKBasePlayer.h
+//  Game Center
+//
+//  Copyright 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <GameKit/GKDefines.h>
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface GKBasePlayer : NSObject
+
+@property(readonly, nullable, retain, NS_NONATOMIC_IOSONLY) NSString *playerID;
+
+// This player's full name as displayed in the Game Center in-game UI. Use this when you need to display the player's name. The display name may be very long, so be sure to use appropriate string truncation API when drawing.
+@property(readonly, nullable, NS_NONATOMIC_IOSONLY) NSString *displayName;
+
+@end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKChallenge.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKChallenge.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKChallenge.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKChallenge.h	2016-05-21 12:19:14.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKChallenge.h
 //  Game Center
 //
-//  Copyright 2012-2015 Apple Inc. All rights reserved.
+//  Copyright 2012-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKChallengeEventHandler.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKChallengeEventHandler.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKChallengeEventHandler.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKChallengeEventHandler.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKChallengeEventHandler.h
 //  Game Center
 //
-//  Copyright 2012-2015 Apple Inc. All rights reserved.
+//  Copyright 2012-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKCloudPlayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKCloudPlayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKCloudPlayer.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKCloudPlayer.h	2016-05-25 08:40:16.000000000 +0200
@@ -0,0 +1,21 @@
+//
+//  GKCloudPlayer.h
+//  Game Center
+//
+//  Copyright 2012-2016 Apple Inc. All rights reserved.
+//
+
+#import <GameKit/GKBasePlayer.h>
+
+@interface GKCloudPlayer : GKBasePlayer
+#if !__OBJC2__
+{
+    NSString *_identifier;
+    NSString *_name;
+}
+#endif
+
+// Retrieve a player instance representing the active iCloud account. Returns nil and an error if no iCloud is currently signed in.
++ (void)getCurrentSignedInPlayer:(void(^)(GKCloudPlayer *player, NSError *error))handler;
+
+@end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKDefines.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKDefines.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKDefines.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKDefines.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKDefines.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 #ifndef GK_EXTERN
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKError.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKError.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKError.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKError.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKError.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
@@ -37,6 +37,8 @@
     GKErrorTurnBasedInvalidState                = 24,
     GKErrorInvitationsDisabled                  = 25,
     GKErrorPlayerPhotoFailure                   = 26,
-    GKErrorUbiquityContainerUnavailable         = 27
+    GKErrorUbiquityContainerUnavailable         = 27,
+    GKErrorMatchNotConnected                    = 28,
+    GKErrorGameSessionRequestInvalid            = 29
 };
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKEventListener.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKEventListener.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKEventListener.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKEventListener.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKEventListener.h
 //  Game Center
 //
-//  Copyright 2012-2015 Apple Inc. All rights reserved.
+//  Copyright 2012-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKFriendRequestComposeViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKFriendRequestComposeViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKFriendRequestComposeViewController.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKFriendRequestComposeViewController.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKFriendRequestComposeViewController.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 #if TARGET_OS_IPHONE
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameCenterViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameCenterViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameCenterViewController.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameCenterViewController.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKGameCenterViewController.h
 //  Game Center
 //
-//  Copyright 2012-2015 Apple Inc. All rights reserved.
+//  Copyright 2012-2016 Apple Inc. All rights reserved.
 //
 
 #import <GameKit/GKLeaderboard.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSession.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSession.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSession.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSession.h	2016-05-28 06:34:38.000000000 +0200
@@ -0,0 +1,88 @@
+//
+//  GKGameSession.h
+//  Game Center
+//
+//  Copyright 2016 Apple Inc. All rights reserved.
+//
+
+#import <GameKit/GKDefines.h>
+@class GKCloudPlayer;
+
+typedef NS_ENUM(NSInteger, GKConnectionState) {
+    GKConnectionStateNotConnected,
+    GKConnectionStateConnected
+};
+
+typedef NS_ENUM(NSInteger, GKTransportType) {
+    GKTransportTypeUnreliable,
+    GKTransportTypeReliable
+};
+
+@interface GKGameSession : NSObject
+#if !__OBJC2__
+{
+    NSString *_identifier;
+    NSString *_title;
+    GKCloudPlayer *_owner;
+    NSArray<GKCloudPlayer *> *_players;
+    NSDate *_lastModifiedDate;
+    GKCloudPlayer *_lastModifiedPlayer;
+    NSString *_serverChangeTag;
+    NSInteger _maxNumberOfConnectedPlayers;
+    NSMutableDictionary<NSString*, NSArray<NSNumber*> *> *_playerStates;
+}
+#endif
+
+@property (nonatomic, readonly) NSString *identifier;
+@property (nonatomic, readonly) NSString *title;
+@property (nonatomic, readonly) GKCloudPlayer *owner;
+@property (nonatomic, readonly) NSArray<GKCloudPlayer *> *players;
+@property (nonatomic, readonly) NSDate *lastModifiedDate;
+@property (nonatomic, readonly) GKCloudPlayer *lastModifiedPlayer;
+@property (nonatomic, readonly) NSInteger maxNumberOfConnectedPlayers;
+@property (nonatomic, readonly) NSArray<GKCloudPlayer *> *badgedPlayers;
+
+// Create a new session with the given title and maximum number of connected players. (You may pass 0 to use the system limit of 16 players.)
++ (void)createSessionInContainer:(NSString *)containerName withTitle:(NSString *)title maxConnectedPlayers:(NSInteger)maxPlayers completionHandler:(void(^)(GKGameSession *session, NSError *error))completionHandler;
+
+// Load all sessions involving the current user.
++ (void)loadSessionsInContainer:(NSString *)containerName completionHandler:(void(^)(NSArray<GKGameSession *> *sessions, NSError *error))completionHandler;
+
+// Load a specific session.
++ (void)loadSessionWithIdentifier:(NSString *)identifier completionHandler:(void(^)(GKGameSession *session, NSError *error))completionHandler;
+
+// Remove a session. If called by the owner this deletes the session from the server.
++ (void)removeSessionWithIdentifier:(NSString *)identifier completionHandler:(void(^)(NSError *error))completionHandler;
+
+
+// Get the URL needed to share this session.
+- (void)getShareURLWithCompletionHandler:(void(^)(NSURL *url, NSError *error))completionHandler;
+
+// Load associated persistent data. The session's lastModifiedDate and lastModifiedPlayer will be updated upon completion.
+- (void)loadDataWithCompletionHandler:(void(^)(NSData *data, NSError *error))completionHandler;
+
+// Save new/updated persistent data. Data size is limited to 512K. The session's lastModifiedDate and lastModifiedPlayer will be updated upon completion.
+// If a version conflict is detected the handler will include the version currently on the server and an error. In this case the data has not been saved. To resolve the conflict a client would call this method again, presumably after merging data or giving the user a choice on how to resolve the conflict. (Note that when calling again it is possible to get a new conflict, if another device has since written a new version.)
+- (void)saveData:(NSData *)data completionHandler:(void(^)(NSData *conflictingData, NSError *error))completionHandler;
+
+
+// Set your connection state. May fail if you attempt to connect but the connected player limit has already been reached or there are network problems. The session's lastModifiedDate and lastModifiedPlayer will be updated upon completion.
+- (void)setConnectionState:(GKConnectionState)state completionHandler:(void(^)(NSError *error))completionHandler;
+
+// Get the players with the given connection state.
+- (NSArray<GKCloudPlayer *> *)playersWithConnectionState:(GKConnectionState)state;
+
+// Send data to all connected players.
+- (void)sendData:(NSData *)data withTransportType:(GKTransportType)transport completionHandler:(void(^)(NSError *error))completionHandler;
+
+
+// Send a message to any players in the session. This uses an unreliable push mechanism. Message/data delivery is not guaranteed and may take some time to arrive.
+- (void)sendMessageWithLocalizedFormatKey:(NSString *)key arguments:(NSArray<NSString *> *)arguments data:(NSData *)data toPlayers:(NSArray<GKCloudPlayer *> *)players badgePlayers:(BOOL)badgePlayers completionHandler:(void(^)(NSError *error))completionHandler;
+
+// clear badged state for players
+- (void)clearBadgeForPlayers:(NSArray<GKCloudPlayer *> *)players completionHandler:(void(^)(NSError *error))completionHandler;
+
+//FIXME: remove after we get <rdar://problem/24623538> Game Center needs a way of defining an XPC interface for daemons
++ (void)acceptShareURL:(NSURL *)url handler:(void(^)(NSError *error))handler;
+
+@end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionError.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionError.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionError.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionError.h	2016-05-25 08:40:16.000000000 +0200
@@ -0,0 +1,24 @@
+//
+//  GKGameSessionError.h
+//  Game Center
+//
+//  Copyright 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+extern NSString * __nonnull GKGameSessionErrorDomain;
+
+typedef  NS_ENUM(NSInteger, GKGameSessionErrorCode) {
+    GKGameSessionErrorUnknown = 1,
+    GKGameSessionErrorNotAuthenticated = 2,
+    GKGameSessionErrorSessionOutOfDate = 3,
+    GKGameSessionErrorSessionNotShared = 4,
+    GKGameSessionErrorConnectionCancelledByUser = 5,
+    GKGameSessionErrorCouldNotConnectToSession = 6,
+    GKGameSessionErrorSessionHasMaxConnectedPlayers = 7,
+    GKGameSessionErrorSendDataNotConnected = 8,
+    GKGameSessionErrorSendDataNoRecipients = 9,
+    GKGameSessionErrorSendDataNotReachable = 10,
+    GKGameSessionErrorSendRateLimitReached = 11
+};
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionEventListener.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionEventListener.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionEventListener.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionEventListener.h	2016-05-25 08:40:16.000000000 +0200
@@ -0,0 +1,26 @@
+//
+//  GKGameSessionEventListener.h
+//  Game Center
+//
+//  Copyright 2016 Apple Inc. All rights reserved.
+//
+
+#import "GKGameSession.h"
+
+@protocol GKGameSessionEventListener <NSObject>
+@optional
+- (void)session:(GKGameSession *)session didAddPlayer:(GKCloudPlayer *)player;
+- (void)session:(GKGameSession *)session didRemovePlayer:(GKCloudPlayer *)player;
+- (void)session:(GKGameSession *)session player:(GKCloudPlayer *)player didChangeConnectionState:(GKConnectionState)newState;
+- (void)session:(GKGameSession *)session player:(GKCloudPlayer *)player didSaveData:(NSData *)data;
+- (void)session:(GKGameSession *)session didReceiveData:(NSData *)data fromPlayer:(GKCloudPlayer *)player;
+- (void)session:(GKGameSession *)session didReceiveMessage:(NSString *)message withData:(NSData *)data fromPlayer:(GKCloudPlayer *)player;
+
+// A player has requested to play a session with the given other players. This could be initiated from an iMessage link or Siri, for example.
+- (void)player:(GKCloudPlayer *)player requestedSessionWithPlayers:(NSArray<GKCloudPlayer *> *)players;
+@end
+
+@interface GKGameSession (GKGameSessionEventListener)
++ (void)addEventListener:(NSObject<GKGameSessionEventListener> *)listener;
++ (void)removeEventListener:(NSObject<GKGameSessionEventListener> *)listener;
+@end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionSharingViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionSharingViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionSharingViewController.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionSharingViewController.h	2016-05-25 08:40:16.000000000 +0200
@@ -0,0 +1,35 @@
+//
+//  GKGameSessionSharingViewController.h
+//  GameCenterUI
+//
+//  Created by Alan Berfield on 2/20/16.
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+#if TARGET_OS_TV
+
+@class GKGameSession;
+@protocol GKGameSessionSharingViewControllerDelegate;
+
+
+NS_ASSUME_NONNULL_BEGIN
+
+@interface GKGameSessionSharingViewController : UIViewController
+@property (nonatomic, readonly, strong) GKGameSession *session;
+@property (nonatomic, weak, nullable) id<GKGameSessionSharingViewControllerDelegate> delegate;
+
+- (instancetype)initWithSession:(GKGameSession *)session;
+
+@end
+
+
+@protocol GKGameSessionSharingViewControllerDelegate <NSObject>
+- (void)sharingViewController:(GKGameSessionSharingViewController *)viewController didFinishWithError:(NSError *)error;
+@end
+
+NS_ASSUME_NONNULL_END
+
+
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLeaderboard.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLeaderboard.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLeaderboard.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLeaderboard.h	2016-05-25 07:35:30.000000000 +0200
@@ -2,10 +2,11 @@
 //  GKLeaderboard.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
+#import <os/lock.h>
 
 typedef NS_ENUM(NSInteger, GKLeaderboardTimeScope) {
     GKLeaderboardTimeScopeToday = 0,
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLeaderboardSet.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLeaderboardSet.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLeaderboardSet.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLeaderboardSet.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKLeaderboardSet.h
 //  Game Center
 //
-//  Copyright 2012-2015 Apple Inc. All rights reserved.
+//  Copyright 2012-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLeaderboardViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLeaderboardViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLeaderboardViewController.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLeaderboardViewController.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKLeaderboardViewController.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 #import <GameKit/GKLeaderboard.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLocalPlayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLocalPlayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLocalPlayer.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLocalPlayer.h	2016-05-25 07:35:30.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKLocalPlayer.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
@@ -38,7 +38,9 @@
 // 1. Communications problem
 // 2. User credentials invalid
 // 3. User cancelled
-#if TARGET_OS_IPHONE
+#if TARGET_OS_WATCH
+@property(atomic, nullable, copy) void(^authenticateHandler)(NSError * __nullable error);
+#elif TARGET_OS_IPHONE
 @property(nonatomic, nullable, copy) void(^authenticateHandler)(UIViewController * __nullable viewController, NSError * __nullable error) NS_AVAILABLE_IOS(6_0);
 #else
 @property(atomic, nullable, copy) void(^authenticateHandler)(NSViewController * __nullable viewController, NSError * __nullable error) NS_AVAILABLE_MAC(10_9);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatch.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatch.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatch.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatch.h	2016-05-21 12:19:14.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKMatch.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatchmaker.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatchmaker.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatchmaker.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatchmaker.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKMatchmaker.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 #include <Foundation/Foundation.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatchmakerViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatchmakerViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatchmakerViewController.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatchmakerViewController.h	2016-05-25 07:35:30.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKMatchmakerViewController.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 @class GKMatchRequest, GKInvite, GKMatch, GKPlayer;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKNotificationBanner.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKNotificationBanner.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKNotificationBanner.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKNotificationBanner.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKNotificationBanner.h
 //  Game Center
 //
-//  Copyright 2012-2015 Apple Inc. All rights reserved.
+//  Copyright 2012-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKPeerPickerController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKPeerPickerController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKPeerPickerController.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKPeerPickerController.h	2016-05-25 07:35:30.000000000 +0200
@@ -30,6 +30,8 @@
 
 @optional
 
+#pragma clang diagnostic push
+#pragma clang diagnostic ignored "-Wdeprecated-declarations"
 /* Notifies delegate that a connection type was chosen by the user.
  */
 - (void)peerPickerController:(GKPeerPickerController *)picker didSelectConnectionType:(GKPeerPickerConnectionType)type ;
@@ -38,8 +40,7 @@
  
  You should return a valid GKSession object for use by the picker. If this method is not implemented or returns 'nil', a default GKSession is created on the delegate's behalf.
  */
-#pragma clang diagnostic push
-#pragma clang diagnostic ignored "-Wdeprecated-declarations"
+
 - (GKSession *)peerPickerController:(GKPeerPickerController *)picker sessionForConnectionType:(GKPeerPickerConnectionType)type ;
 
 /* Notifies delegate that the peer was connected to a GKSession.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKPlayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKPlayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKPlayer.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKPlayer.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,10 +2,11 @@
 //  GKPlayer.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
+#import <GameKit/GKBasePlayer.h>
 #import <GameKit/GKDefines.h>
 #import <GameKit/GKError.h>
 
@@ -14,7 +15,7 @@
 @class GKLocalPlayer;
 
 NS_CLASS_AVAILABLE(10_8, 4_1)
-@interface GKPlayer : NSObject
+@interface GKPlayer : GKBasePlayer
 
 // Load the Game Center players for the playerIDs provided. Error will be nil on success.
 // Possible reasons for error:
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKSavedGame.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKSavedGame.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKSavedGame.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKSavedGame.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKSavedGame.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 #import <GameKit/GKLocalPlayer.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKSavedGameListener.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKSavedGameListener.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKSavedGameListener.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKSavedGameListener.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKSavedGameListener.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 @class GKPlayer;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKScore.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKScore.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKScore.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKScore.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKScore.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
@@ -34,7 +34,7 @@
 @property(assign, NS_NONATOMIC_IOSONLY)                        uint64_t    context NS_AVAILABLE(10_8, 5_0);
 
 @property(readonly, retain, NS_NONATOMIC_IOSONLY)   NSDate      *date;              // The date this score was recorded. A newly initialized, unsubmitted GKScore records the current date at init time.
-@property(readonly, retain, NS_NONATOMIC_IOSONLY)   GKPlayer    *player NS_AVAILABLE(10_10, 8_0);          // The player that recorded the score.
+@property(readonly, retain, nullable, NS_NONATOMIC_IOSONLY)   GKPlayer    *player NS_AVAILABLE(10_10, 8_0);          // The player that recorded the score.
 @property(readonly, assign, NS_NONATOMIC_IOSONLY)   NSInteger   rank;               // The rank of the player within the leaderboard, only valid when returned from GKLeaderboard
 
 // Convenience property to make the leaderboard associated with this GKScore, the default leaderboard for this player. Default value is false.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKTurnBasedMatch.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKTurnBasedMatch.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKTurnBasedMatch.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKTurnBasedMatch.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKTurnBasedMatch.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 #import <GameKit/GKPlayer.h>
@@ -298,7 +298,7 @@
 NS_DEPRECATED(10_8, 10_10, 5_0, 7_0, "Use registerListener on GKLocalPlayer with an object that implements the GKTurnBasedEventListener protocol") 
 @protocol  GKTurnBasedEventHandlerDelegate
 
-- (void)handleInviteFromGameCenter:(NSArray<GKPlayer *> *)playersToInvite NS_DEPRECATED(10_8, 10_10, 5_0, 7_0);
+- (void)handleInviteFromGameCenter:(NSArray<NSString *> *)playersToInvite NS_DEPRECATED(10_8, 10_10, 5_0, 7_0);
 - (void)handleTurnEventForMatch:(GKTurnBasedMatch *)match didBecomeActive:(BOOL)didBecomeActive NS_DEPRECATED(10_9, 10_10, 6_0, 7_0);
 
 @optional
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKTurnBasedMatchmakerViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKTurnBasedMatchmakerViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKTurnBasedMatchmakerViewController.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKTurnBasedMatchmakerViewController.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKTurnBasedMatchmakerViewController.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 @protocol GKTurnBasedMatchmakerViewControllerDelegate;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKVoiceChat.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKVoiceChat.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKVoiceChat.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKVoiceChat.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,7 +2,7 @@
 //  GKVoiceChat.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GameKit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GameKit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GameKit.h	2015-10-03 02:32:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GameKit.h	2016-05-25 08:40:16.000000000 +0200
@@ -2,19 +2,42 @@
 //  GameKit.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
+#import <TargetConditionals.h>
+#import <simd/simd.h>
+
+#import <UIKit/UIKit.h>
+
+#if !TARGET_OS_SIMULATOR
+#import <Metal/Metal.h>
+#import <MetalKit/MetalKit.h>
+#endif
+
+#import <SpriteKit/SpriteKit.h>
+#import <SceneKit/SceneKit.h>
+#import <GameplayKit/GameplayKit.h>
+#import <GameController/GameController.h>
+#import <ModelIO/ModelIO.h>
+#import <ReplayKit/ReplayKit.h>
+
 #import <GameKit/GKDefines.h>
 #import <GameKit/GKAchievement.h>
 #import <GameKit/GKAchievementDescription.h>
 #import <GameKit/GKAchievementViewController.h>
+#import <GameKit/GKBasePlayer.h>
 #import <GameKit/GKChallenge.h>
 #import <GameKit/GKChallengeEventHandler.h>
+#import <GameKit/GKCloudPlayer.h>
 #import <GameKit/GKError.h>
 #import <GameKit/GKEventListener.h>
 #import <GameKit/GKFriendRequestComposeViewController.h>
 #import <GameKit/GKGameCenterViewController.h>
+#import <GameKit/GKGameSession.h>
+#import <GameKit/GKGameSessionError.h>
+#import <GameKit/GKGameSessionEventListener.h>
+#import <GameKit/GKGameSessionSharingViewController.h>
 #import <GameKit/GKLeaderboard.h>
 #import <GameKit/GKLeaderboardSet.h>
 #import <GameKit/GKLeaderboardViewController.h>
@@ -40,7 +63,7 @@
 //  GameKit.h
 //  Game Center
 //
-//  Copyright 2010-2015 Apple Inc. All rights reserved.
+//  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
 #import <TargetConditionals.h>

```