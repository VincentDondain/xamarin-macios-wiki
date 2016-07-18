#GameKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKChallenge.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKChallenge.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKChallenge.h	2016-06-26 10:20:06.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKChallenge.h	2016-07-14 08:00:28.000000000 +0200
@@ -51,13 +51,13 @@
 
 @end
 
-NS_CLASS_AVAILABLE(10_8, 6_0)
+NS_CLASS_AVAILABLE(10_8, 6_0) __WATCHOS_PROHIBITED
 @interface GKScoreChallenge : GKChallenge
 
 @property (nonatomic, readonly, nullable, retain) GKScore *score; // The score to meet to satisfy this challenge
 @end
 
-NS_CLASS_AVAILABLE(10_8, 6_0)
+NS_CLASS_AVAILABLE(10_8, 6_0) __WATCHOS_PROHIBITED
 @interface GKAchievementChallenge : GKChallenge
 
 @property (nonatomic, readonly, nullable, retain) GKAchievement *achievement; // The achievement to achieve to satisfy this challenge
@@ -65,7 +65,7 @@
 
 
 // Use the following category methods to issue GKScoreChallenges and GKAchievementChallenges to an array of playerIDs. Players may not issue challenges to themselves nor to non-friends. Please see the GameKit reference documentation for further details on these methods.
-
+#if !TARGET_OS_WATCH
 @interface GKScore (GKChallenge)
 
 // Return a challenge compose view controller with pre-selected GKPlayers and a preformatted, player-editable message. Once this view controller is displayed, and the player sends or cancels sending the challenge, the completion handler will be called. This block contains the view controller, the reason why the handler was called, as well as which (if any) GKPlayers the challenge was sent to. Present modally from the top view controller. The completion handler should dismiss the view controller.
@@ -127,4 +127,5 @@
 #endif
 
 @end
+#endif
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKChallengeEventHandler.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKChallengeEventHandler.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKChallengeEventHandler.h	2016-06-29 07:15:36.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKChallengeEventHandler.h	2016-07-14 08:18:38.000000000 +0200
@@ -9,7 +9,7 @@
 #import <GameKit/GKChallenge.h>
 
 // GKChallengeEventHandler's delegate must implement the following protocol to be notified of challenge-related events. All of these methods are called on the main thread.
-NS_DEPRECATED(10_8, 10_10, 6_0, 7_0, "You should instead implement the GKChallengeListener protocol and register a listener with GKLocalPlayer.") 
+NS_DEPRECATED(10_8, 10_10, 6_0, 7_0, "You should instead implement the GKChallengeListener protocol and register a listener with GKLocalPlayer.") __WATCHOS_PROHIBITED 
 @protocol GKChallengeEventHandlerDelegate <NSObject>
 
 @optional
@@ -37,6 +37,7 @@
 
 @end
 
+#if !TARGET_OS_WATCH
 
 NS_CLASS_DEPRECATED(10_8, 10_10, 6_0, 7_0, "You should instead implement the GKChallengeListener protocol and register a listener with GKLocalPlayer.") 
 // A singleton object responsible for dispatching challenge-related events to its delegate
@@ -46,3 +47,4 @@
 
 @property (nonatomic, assign) id<GKChallengeEventHandlerDelegate> delegate NS_DEPRECATED(10_8, 10_10, 6_0, 7_0); // It is not safe to read or write this property on anything other than the main thread
 @end
+#endif
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKCloudPlayer.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKCloudPlayer.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKCloudPlayer.h	2016-06-29 07:15:36.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKCloudPlayer.h	2016-07-14 08:18:38.000000000 +0200
@@ -6,7 +6,7 @@
 //
 
 #import <GameKit/GKBasePlayer.h>
-
+NS_ASSUME_NONNULL_BEGIN
 @interface GKCloudPlayer : GKBasePlayer
 #if !__OBJC2__
 {
@@ -15,7 +15,8 @@
 }
 #endif
 
-// Retrieve a player instance representing the active iCloud account. Returns nil and an error if no iCloud is currently signed in.
-+ (void)getCurrentSignedInPlayer:(void(^)(GKCloudPlayer *player, NSError *error))handler;
+// Retrieve a player instance representing the active iCloud account for a given iCloud container. Returns nil and an error if the user is not signed in to iCloud or the container is invalid.
++ (void)getCurrentSignedInPlayerForContainer:(NSString * __nullable)containerName completionHandler:(void(^)(GKCloudPlayer *__nullable player, NSError * __nullable error))handler;
 
 @end
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKFriendRequestComposeViewController.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKFriendRequestComposeViewController.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKFriendRequestComposeViewController.h	2016-06-29 07:15:36.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKFriendRequestComposeViewController.h	2016-07-14 08:18:38.000000000 +0200
@@ -18,13 +18,13 @@
 // Standard view controller for sending friend requests to other players. Present modally from the top view controller.
 #if TARGET_OS_IPHONE
 NS_ASSUME_NONNULL_BEGIN
-NS_CLASS_AVAILABLE(10_8, 4_2) 
+NS_CLASS_DEPRECATED(10_8, 10_12, 4_2, 10_0) 
 @interface GKFriendRequestComposeViewController : UINavigationController
 @end
 #else
 #import <GameKit/GKDialogController.h>
 NS_ASSUME_NONNULL_BEGIN
-NS_CLASS_AVAILABLE(10_8, 4_2)
+NS_CLASS_DEPRECATED(10_8, 10_12, 4_2, 10_0)
 @interface GKFriendRequestComposeViewController : NSViewController <GKViewController> {
     id _remoteViewController;
     id<GKFriendRequestComposeViewControllerDelegate> _composeViewDelegateWeak;
@@ -54,6 +54,6 @@
 // Optional delegate
 @protocol GKFriendRequestComposeViewControllerDelegate
 // The compose view has finished
-- (void)friendRequestComposeViewControllerDidFinish:(GKFriendRequestComposeViewController *)viewController NS_AVAILABLE(10_8, 4_2) ;
+- (void)friendRequestComposeViewControllerDidFinish:(GKFriendRequestComposeViewController *)viewController NS_DEPRECATED(10_8, 10_12, 4_2, 10_0) ;
 @end
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSession.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSession.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSession.h	2016-06-26 10:20:06.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSession.h	2016-07-11 07:47:47.000000000 +0200
@@ -18,6 +18,8 @@
     GKTransportTypeReliable
 };
 
+NS_ASSUME_NONNULL_BEGIN
+
 @interface GKGameSession : NSObject
 #if !__OBJC2__
 {
@@ -43,43 +45,45 @@
 @property (nonatomic, readonly) NSArray<GKCloudPlayer *> *badgedPlayers;
 
 // Create a new session with the given title and maximum number of connected players. (You may pass 0 to use the system limit of 16 players.)
-+ (void)createSessionInContainer:(NSString *)containerName withTitle:(NSString *)title maxConnectedPlayers:(NSInteger)maxPlayers completionHandler:(void(^)(GKGameSession *session, NSError *error))completionHandler;
++ (void)createSessionInContainer:(NSString * __nullable)containerName withTitle:(NSString *)title maxConnectedPlayers:(NSInteger)maxPlayers completionHandler:(void(^)(GKGameSession * __nullable session, NSError * __nullable error))completionHandler;
 
 // Load all sessions involving the current user.
-+ (void)loadSessionsInContainer:(NSString *)containerName completionHandler:(void(^)(NSArray<GKGameSession *> *sessions, NSError *error))completionHandler;
++ (void)loadSessionsInContainer:(NSString * __nullable)containerName completionHandler:(void(^)(NSArray<GKGameSession *> * __nullable sessions, NSError * __nullable error))completionHandler;
 
 // Load a specific session.
-+ (void)loadSessionWithIdentifier:(NSString *)identifier completionHandler:(void(^)(GKGameSession *session, NSError *error))completionHandler;
++ (void)loadSessionWithIdentifier:(NSString *)identifier completionHandler:(void(^)(GKGameSession * __nullable session, NSError * __nullable error))completionHandler;
 
 // Remove a session. If called by the owner this deletes the session from the server.
-+ (void)removeSessionWithIdentifier:(NSString *)identifier completionHandler:(void(^)(NSError *error))completionHandler;
++ (void)removeSessionWithIdentifier:(NSString *)identifier completionHandler:(void(^)(NSError * __nullable error))completionHandler;
 
 
 // Get the URL needed to share this session.
-- (void)getShareURLWithCompletionHandler:(void(^)(NSURL *url, NSError *error))completionHandler;
+- (void)getShareURLWithCompletionHandler:(void(^)(NSURL * __nullable url, NSError * __nullable error))completionHandler;
 
 // Load associated persistent data. The session's lastModifiedDate and lastModifiedPlayer will be updated upon completion.
-- (void)loadDataWithCompletionHandler:(void(^)(NSData *data, NSError *error))completionHandler;
+- (void)loadDataWithCompletionHandler:(void(^)(NSData * __nullable data, NSError * __nullable error))completionHandler;
 
 // Save new/updated persistent data. Data size is limited to 512K. The session's lastModifiedDate and lastModifiedPlayer will be updated upon completion.
 // If a version conflict is detected the handler will include the version currently on the server and an error. In this case the data has not been saved. To resolve the conflict a client would call this method again, presumably after merging data or giving the user a choice on how to resolve the conflict. (Note that when calling again it is possible to get a new conflict, if another device has since written a new version.)
-- (void)saveData:(NSData *)data completionHandler:(void(^)(NSData *conflictingData, NSError *error))completionHandler;
+- (void)saveData:(NSData *)data completionHandler:(void(^)(NSData * __nullable conflictingData, NSError * __nullable error))completionHandler;
 
 
 // Set your connection state. May fail if you attempt to connect but the connected player limit has already been reached or there are network problems. The session's lastModifiedDate and lastModifiedPlayer will be updated upon completion.
-- (void)setConnectionState:(GKConnectionState)state completionHandler:(void(^)(NSError *error))completionHandler;
+- (void)setConnectionState:(GKConnectionState)state completionHandler:(void(^)(NSError * __nullable error))completionHandler;
 
 // Get the players with the given connection state.
 - (NSArray<GKCloudPlayer *> *)playersWithConnectionState:(GKConnectionState)state;
 
 // Send data to all connected players.
-- (void)sendData:(NSData *)data withTransportType:(GKTransportType)transport completionHandler:(void(^)(NSError *error))completionHandler;
+- (void)sendData:(NSData *)data withTransportType:(GKTransportType)transport completionHandler:(void(^)(NSError * __nullable error))completionHandler;
 
 
 // Send a message to any players in the session. This uses an unreliable push mechanism. Message/data delivery is not guaranteed and may take some time to arrive. Receiving players may optionally have their application badged for this session.
-- (void)sendMessageWithLocalizedFormatKey:(NSString *)key arguments:(NSArray<NSString *> *)arguments data:(NSData *)data toPlayers:(NSArray<GKCloudPlayer *> *)players badgePlayers:(BOOL)badgePlayers completionHandler:(void(^)(NSError *error))completionHandler;
+- (void)sendMessageWithLocalizedFormatKey:(NSString *)key arguments:(NSArray<NSString *> *)arguments data:(NSData * __nullable)data toPlayers:(NSArray<GKCloudPlayer *> *)players badgePlayers:(BOOL)badgePlayers completionHandler:(void(^)(NSError * __nullable error))completionHandler;
 
 // Clear application badge state for players for this session.
-- (void)clearBadgeForPlayers:(NSArray<GKCloudPlayer *> *)players completionHandler:(void(^)(NSError *error))completionHandler;
+- (void)clearBadgeForPlayers:(NSArray<GKCloudPlayer *> *)players completionHandler:(void(^)(NSError * __nullable error))completionHandler;
 
 @end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionError.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionError.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionError.h	2016-06-29 07:15:36.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionError.h	2016-07-14 08:18:38.000000000 +0200
@@ -24,4 +24,6 @@
     GKGameSessionErrorBadContainer = 12,
     GKGameSessionErrorCloudQuotaExceeded = 13,
     GKGameSessionErrorNetworkFailure = 14,
+    GKGameSessionErrorCloudDriveDisabled = 15,
+    GKGameSessionErrorInvalidSession = 16,
 };
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionEventListener.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionEventListener.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionEventListener.h	2016-06-29 07:15:36.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionEventListener.h	2016-07-14 08:18:38.000000000 +0200
@@ -6,6 +6,7 @@
 //
 
 #import "GKGameSession.h"
+NS_ASSUME_NONNULL_BEGIN
 
 @protocol GKGameSessionEventListener <NSObject>
 @optional
@@ -22,3 +23,6 @@
 + (void)addEventListener:(NSObject<GKGameSessionEventListener> *)listener;
 + (void)removeEventListener:(NSObject<GKGameSessionEventListener> *)listener;
 @end
+
+NS_ASSUME_NONNULL_END
+
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionSharingViewController.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionSharingViewController.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionSharingViewController.h	2016-06-29 07:15:36.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionSharingViewController.h	2016-07-14 08:18:38.000000000 +0200
@@ -26,7 +26,7 @@
 
 
 @protocol GKGameSessionSharingViewControllerDelegate <NSObject>
-- (void)sharingViewController:(GKGameSessionSharingViewController *)viewController didFinishWithError:(NSError *)error;
+- (void)sharingViewController:(GKGameSessionSharingViewController *)viewController didFinishWithError:(NSError * __nullable)error;
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLocalPlayer.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLocalPlayer.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLocalPlayer.h	2016-06-26 12:27:07.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLocalPlayer.h	2016-07-14 08:00:28.000000000 +0200
@@ -76,8 +76,13 @@
 
 @end
 
+#if TARGET_OS_WATCH
+@protocol GKLocalPlayerListener <GKChallengeListener, GKInviteEventListener, GKTurnBasedEventListener>
+@end
+#else
 @protocol GKLocalPlayerListener <GKChallengeListener, GKInviteEventListener, GKTurnBasedEventListener, GKSavedGameListener>
 @end
+#endif
 
 @interface GKLocalPlayer (GKLocalPlayerEvents)
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatch.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatch.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatch.h	2016-06-26 10:20:06.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatch.h	2016-07-14 08:00:28.000000000 +0200
@@ -59,6 +59,7 @@
 
 @end
 
+__WATCHOS_PROHIBITED
 @protocol GKMatchDelegate <NSObject>
 @optional
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKSavedGame.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKSavedGame.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKSavedGame.h	2016-06-29 07:15:36.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKSavedGame.h	2016-07-14 08:18:38.000000000 +0200
@@ -23,7 +23,7 @@
 
 @end
 
-
+#if !TARGET_OS_WATCH
 @interface GKLocalPlayer (GKSavedGame) <GKSavedGameListener>
 
 // Asynchronously fetch saved games. The handler is called with an array of GKSavedGame objects or an error.
@@ -41,6 +41,6 @@
 - (void)resolveConflictingSavedGames:(NSArray<GKSavedGame *> *)conflictingSavedGames withData:(NSData *)data completionHandler:(void(^__nullable)(NSArray<GKSavedGame *> * __nullable savedGames, NSError * __nullable error))handler NS_AVAILABLE(10_10, 8_0) ;
 
 @end
-
+#endif
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GameKit.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GameKit.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GameKit.h	2016-06-29 07:15:36.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GameKit.h	2016-07-14 08:18:38.000000000 +0200
@@ -59,26 +59,3 @@
 #import <GameKit/GKTurnBasedMatchmakerViewController.h>
 #import <GameKit/GKVoiceChat.h>
 #import <GameKit/GKVoiceChatService.h>
-//
-//  GameKit.h
-//  Game Center
-//
-//  Copyright 2010-2016 Apple Inc. All rights reserved.
-//
-
-#import <TargetConditionals.h>
-#import <simd/simd.h>
-
-#import <UIKit/UIKit.h>
-
-#if !TARGET_OS_SIMULATOR
-#import <Metal/Metal.h>
-#import <MetalKit/MetalKit.h>
-#endif
-
-#import <SpriteKit/SpriteKit.h>
-#import <SceneKit/SceneKit.h>
-#import <GameplayKit/GameplayKit.h>
-#import <GameController/GameController.h>
-#import <ModelIO/ModelIO.h>
-#import <ReplayKit/ReplayKit.h>

```