#GameKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKAchievement.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKAchievement.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKAchievement.h	2016-05-21 09:29:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKAchievement.h	2016-06-29 05:49:46.000000000 +0200
@@ -13,7 +13,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 // GKAchievement represents a game achievement that the player has started or completely achieved.
-NS_CLASS_AVAILABLE(10_8, 4_1)
+NS_CLASS_AVAILABLE(10_8, 4_1) __WATCHOS_AVAILABLE(3_0)
 
 @interface GKAchievement : NSObject <NSCoding, NSSecureCoding>
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKAchievementDescription.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKAchievementDescription.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKAchievementDescription.h	2016-05-21 09:29:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKAchievementDescription.h	2016-06-29 05:49:46.000000000 +0200
@@ -11,7 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 // GKAchievementDescription is a full description of the achievement as defined before app submission in iTunes Connect.
-NS_CLASS_AVAILABLE(10_8, 4_1)
+NS_CLASS_AVAILABLE(10_8, 4_1) __WATCHOS_AVAILABLE(3_0)
 @interface GKAchievementDescription : NSObject <NSCoding, NSSecureCoding>
 
 // Asynchronously load all achievement descriptions
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKBasePlayer.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKBasePlayer.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKBasePlayer.h	2016-05-21 09:29:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKBasePlayer.h	2016-06-29 05:49:46.000000000 +0200
@@ -8,7 +8,7 @@
 #import <Foundation/Foundation.h>
 #import <GameKit/GKDefines.h>
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+NS_CLASS_AVAILABLE(10_12, 10_0) __WATCHOS_AVAILABLE(3_0)
 @interface GKBasePlayer : NSObject
 
 @property(readonly, nullable, retain, NS_NONATOMIC_IOSONLY) NSString *playerID;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKChallenge.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKChallenge.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKChallenge.h	2016-05-21 08:59:57.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKChallenge.h	2016-06-29 05:49:46.000000000 +0200
@@ -30,7 +30,7 @@
 };
 
 
-NS_CLASS_AVAILABLE(10_8, 6_0)
+NS_CLASS_AVAILABLE(10_8, 6_0) __WATCHOS_PROHIBITED
 @interface GKChallenge : NSObject <NSCoding, NSSecureCoding>
 
 // Query challenges for the current game issued to the local player -- equivalent GKChallenge objects are not guaranteed to be pointer equivalent across calls, but equal GKChallenge objects will have equal hashes
@@ -127,4 +127,4 @@
 #endif
 
 @end
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKEventListener.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKEventListener.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKEventListener.h	2016-05-21 09:29:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKEventListener.h	2016-06-29 05:49:46.000000000 +0200
@@ -16,24 +16,24 @@
 // Called when a player starts the game with the intent of playing a challenge, or intends to play a challenge after selecting it within the in-game Game Center UI.
 // player: The player who selected the challenge
 // challenge: The challenge which was selected
-- (void)player:(GKPlayer *)player wantsToPlayChallenge:(GKChallenge *)challenge NS_AVAILABLE(10_10, 7_0);
+- (void)player:(GKPlayer *)player wantsToPlayChallenge:(GKChallenge *)challenge NS_AVAILABLE(10_10, 7_0) __WATCHOS_PROHIBITED;
 
 // Called when a player has received a challenge, triggered by a push notification from the server. Received only while the game is running.
 // player: The player who received the challenge
 // challenge: The challenge which was received
-- (void)player:(GKPlayer *)player didReceiveChallenge:(GKChallenge *)challenge NS_AVAILABLE(10_10, 7_0);
+- (void)player:(GKPlayer *)player didReceiveChallenge:(GKChallenge *)challenge NS_AVAILABLE(10_10, 7_0) __WATCHOS_PROHIBITED;
 
 // Called when a player has completed a challenge, triggered while the game is running, or when the user has tapped a challenge notification banner while outside of the game.
 // player: The player who completed the challenge
 // challenge: The challenge which the player completed
 // friendPlayer: The friend who sent the challenge originally
-- (void)player:(GKPlayer *)player didCompleteChallenge:(GKChallenge *)challenge issuedByFriend:(GKPlayer *)friendPlayer NS_AVAILABLE(10_10, 7_0);
+- (void)player:(GKPlayer *)player didCompleteChallenge:(GKChallenge *)challenge issuedByFriend:(GKPlayer *)friendPlayer NS_AVAILABLE(10_10, 7_0) __WATCHOS_PROHIBITED;
 
 // Called when a player's friend has completed a challenge which the player sent to that friend. Triggered while the game is running, or when the user has tapped a challenge notification banner while outside of the game.
 // player: The player who sent the challenge originally
 // challenge: The challenge which the player created and sent
 // friendPlayer: The friend who completed the challenge
-- (void)player:(GKPlayer *)player issuedChallengeWasCompleted:(GKChallenge *)challenge byFriend:(GKPlayer *)friendPlayer NS_AVAILABLE(10_10, 7_0);
+- (void)player:(GKPlayer *)player issuedChallengeWasCompleted:(GKChallenge *)challenge byFriend:(GKPlayer *)friendPlayer NS_AVAILABLE(10_10, 7_0) __WATCHOS_PROHIBITED;
 
 @end
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSession.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSession.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSession.h	2016-05-28 06:34:38.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSession.h	2016-06-26 10:20:06.000000000 +0200
@@ -76,13 +76,10 @@
 - (void)sendData:(NSData *)data withTransportType:(GKTransportType)transport completionHandler:(void(^)(NSError *error))completionHandler;
 
 
-// Send a message to any players in the session. This uses an unreliable push mechanism. Message/data delivery is not guaranteed and may take some time to arrive.
+// Send a message to any players in the session. This uses an unreliable push mechanism. Message/data delivery is not guaranteed and may take some time to arrive. Receiving players may optionally have their application badged for this session.
 - (void)sendMessageWithLocalizedFormatKey:(NSString *)key arguments:(NSArray<NSString *> *)arguments data:(NSData *)data toPlayers:(NSArray<GKCloudPlayer *> *)players badgePlayers:(BOOL)badgePlayers completionHandler:(void(^)(NSError *error))completionHandler;
 
-// clear badged state for players
+// Clear application badge state for players for this session.
 - (void)clearBadgeForPlayers:(NSArray<GKCloudPlayer *> *)players completionHandler:(void(^)(NSError *error))completionHandler;
 
-//FIXME: remove after we get <rdar://problem/24623538> Game Center needs a way of defining an XPC interface for daemons
-+ (void)acceptShareURL:(NSURL *)url handler:(void(^)(NSError *error))handler;
-
 @end
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionError.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionError.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionError.h	2016-05-21 09:29:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionError.h	2016-06-29 05:49:46.000000000 +0200
@@ -12,13 +12,16 @@
 typedef  NS_ENUM(NSInteger, GKGameSessionErrorCode) {
     GKGameSessionErrorUnknown = 1,
     GKGameSessionErrorNotAuthenticated = 2,
-    GKGameSessionErrorSessionOutOfDate = 3,
+    GKGameSessionErrorSessionConflict = 3,
     GKGameSessionErrorSessionNotShared = 4,
     GKGameSessionErrorConnectionCancelledByUser = 5,
-    GKGameSessionErrorCouldNotConnectToSession = 6,
+    GKGameSessionErrorConnectionFailed = 6,
     GKGameSessionErrorSessionHasMaxConnectedPlayers = 7,
     GKGameSessionErrorSendDataNotConnected = 8,
     GKGameSessionErrorSendDataNoRecipients = 9,
     GKGameSessionErrorSendDataNotReachable = 10,
-    GKGameSessionErrorSendRateLimitReached = 11
+    GKGameSessionErrorSendRateLimitReached = 11,
+    GKGameSessionErrorBadContainer = 12,
+    GKGameSessionErrorCloudQuotaExceeded = 13,
+    GKGameSessionErrorNetworkFailure = 14,
 };
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionEventListener.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionEventListener.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionEventListener.h	2016-05-21 09:29:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSessionEventListener.h	2016-06-29 05:49:46.000000000 +0200
@@ -16,8 +16,6 @@
 - (void)session:(GKGameSession *)session didReceiveData:(NSData *)data fromPlayer:(GKCloudPlayer *)player;
 - (void)session:(GKGameSession *)session didReceiveMessage:(NSString *)message withData:(NSData *)data fromPlayer:(GKCloudPlayer *)player;
 
-// A player has requested to play a session with the given other players. This could be initiated from an iMessage link or Siri, for example.
-- (void)player:(GKCloudPlayer *)player requestedSessionWithPlayers:(NSArray<GKCloudPlayer *> *)players;
 @end
 
 @interface GKGameSession (GKGameSessionEventListener)
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLeaderboard.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLeaderboard.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLeaderboard.h	2016-05-21 08:59:57.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLeaderboard.h	2016-06-29 05:49:46.000000000 +0200
@@ -25,7 +25,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 // GKLeaderboard represents the set of high scores for the current game, always including the local player's best score.
-NS_CLASS_AVAILABLE(10_8, 4_1)
+NS_CLASS_AVAILABLE(10_8, 4_1) __WATCHOS_AVAILABLE(3_0)
 @interface GKLeaderboard : NSObject
 
 @property(assign, NS_NONATOMIC_IOSONLY)            GKLeaderboardTimeScope      timeScope;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLeaderboardSet.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLeaderboardSet.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLeaderboardSet.h	2016-05-21 09:29:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLeaderboardSet.h	2016-06-29 05:49:46.000000000 +0200
@@ -13,7 +13,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 // GKLeaderboardSet represents the sets that leaderboards can be broken out into. 
-NS_CLASS_AVAILABLE(10_10, 7_0)
+NS_CLASS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0)
 @interface GKLeaderboardSet : NSObject <NSCoding, NSSecureCoding>
 
 @property(readonly, copy, NS_NONATOMIC_IOSONLY)    NSString                    *title;               // Localized set title.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLocalPlayer.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLocalPlayer.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLocalPlayer.h	2016-05-21 09:29:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKLocalPlayer.h	2016-06-29 05:49:46.000000000 +0200
@@ -21,7 +21,7 @@
 
 
 NS_ASSUME_NONNULL_BEGIN
-NS_CLASS_AVAILABLE(10_8, 4_1)
+NS_CLASS_AVAILABLE(10_8, 4_1) __WATCHOS_AVAILABLE(3_0)
 @interface GKLocalPlayer : GKPlayer
 
 // Obtain the primary GKLocalPlayer object.
@@ -39,25 +39,25 @@
 // 2. User credentials invalid
 // 3. User cancelled
 #if TARGET_OS_WATCH
-@property(atomic, nullable, copy) void(^authenticateHandler)(NSError * __nullable error);
+@property(atomic, nullable, copy) void(^authenticateHandler)(NSError * __nullable error) __WATCHOS_AVAILABLE(3_0);
 #elif TARGET_OS_IPHONE
 @property(nonatomic, nullable, copy) void(^authenticateHandler)(UIViewController * __nullable viewController, NSError * __nullable error) NS_AVAILABLE_IOS(6_0);
 #else
 @property(atomic, nullable, copy) void(^authenticateHandler)(NSViewController * __nullable viewController, NSError * __nullable error) NS_AVAILABLE_MAC(10_9);
 #endif
 
-// Asynchronously load the friends list as an array of GKPlayer. Calls completionHandler when finished. Error will be nil on success.
+// Asynchronously load the recent players list as an array of GKPlayer.  A recent player is someone that you have played a game with or is a legacy game center friend.  Calls completionHandler when finished. Error will be nil on success.
 // Possible reasons for error:
 // 1. Communications problem
 // 2. Unauthenticated player
-- (void)loadFriendPlayersWithCompletionHandler:(void(^__nullable)(NSArray<GKPlayer *> * __nullable friendPlayers, NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 8_0);
+- (void)loadRecentPlayersWithCompletionHandler:(void(^__nullable)(NSArray<GKPlayer *> * __nullable recentPlayers, NSError * __nullable error))completionHandler NS_AVAILABLE(10_11, 10_0) __WATCHOS_AVAILABLE(3_0);
 ;
 // Set the default leaderboard for the current game
 // Possible reasons for error:
 // 1. Communications problem
 // 2. Unauthenticated player
 // 3. Leaderboard not present
-- (void)setDefaultLeaderboardIdentifier:(NSString *)leaderboardIdentifier completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 7_0);
+- (void)setDefaultLeaderboardIdentifier:(NSString *)leaderboardIdentifier completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 
 // Load the default leaderboard identifier for the local player
@@ -65,14 +65,14 @@
 // 1. Communications problem
 // 2. Unauthenticated player
 // 3. Leaderboard not present
-- (void)loadDefaultLeaderboardIdentifierWithCompletionHandler:(void(^__nullable)(NSString * __nullable leaderboardIdentifier, NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 7_0);
+- (void)loadDefaultLeaderboardIdentifierWithCompletionHandler:(void(^__nullable)(NSString * __nullable leaderboardIdentifier, NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 
 // Generates a signature allowing 3rd party server to authenticate the GKLocalPlayer
 //Possible reasons for error:
 // 1. Communications problem
 // 2. Unauthenticated player
-- (void)generateIdentityVerificationSignatureWithCompletionHandler:(void (^__nullable)(NSURL * __nullable publicKeyUrl, NSData * __nullable signature, NSData * __nullable salt, uint64_t timestamp, NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 7_0);
+- (void)generateIdentityVerificationSignatureWithCompletionHandler:(void (^__nullable)(NSURL * __nullable publicKeyUrl, NSData * __nullable signature, NSData * __nullable salt, uint64_t timestamp, NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 @end
 
@@ -82,11 +82,11 @@
 @interface GKLocalPlayer (GKLocalPlayerEvents)
 
 // A single listener may be registered once. Registering multiple times results in undefined behavior. The registered listener will receive callbacks for any selector it responds to.
-- (void)registerListener:(id<GKLocalPlayerListener>)listener NS_AVAILABLE(10_10, 7_0);
+- (void)registerListener:(id<GKLocalPlayerListener>)listener NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
-- (void)unregisterListener:(id<GKLocalPlayerListener>)listener NS_AVAILABLE(10_10, 7_0);
+- (void)unregisterListener:(id<GKLocalPlayerListener>)listener NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
-- (void)unregisterAllListeners NS_AVAILABLE(10_10, 7_0);
+- (void)unregisterAllListeners NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 @end
 
@@ -97,10 +97,12 @@
 
 - (void)setDefaultLeaderboardCategoryID:(nullable NSString *)categoryID completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_DEPRECATED(10_8, 10_10, 6_0, 7_0,"Use setDefaultLeaderboardIdentifier:completionHandler: instead") __TVOS_UNAVAILABLE;
 - (void)loadDefaultLeaderboardCategoryIDWithCompletionHandler:(void(^__nullable)(NSString * __nullable categoryID, NSError * __nullable error))completionHandler NS_DEPRECATED(10_8, 10_10, 6_0, 7_0,"Use loadDefaultLeaderboardIdentifierWithCompletionHandler: instead") __TVOS_UNAVAILABLE;
-- (void)loadFriendsWithCompletionHandler:(void(^__nullable)(NSArray<NSString *> * __nullable friendIDs, NSError * __nullable error))completionHandler NS_DEPRECATED(10_8, 10_10, 4_1, 8_0, "use loadFriendPlayersWithCompletionHandler: instead") __TVOS_UNAVAILABLE;
+- (void)loadFriendsWithCompletionHandler:(void(^__nullable)(NSArray<NSString *> * __nullable friendIDs, NSError * __nullable error))completionHandler NS_DEPRECATED(10_8, 10_10, 4_1, 8_0, "use loadRecentPlayersWithCompletionHandler: instead") __TVOS_UNAVAILABLE;
 - (void)authenticateWithCompletionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_DEPRECATED(10_8, 10_8, 4_1, 6_0, "Set the authenticateHandler instead") __TVOS_UNAVAILABLE;
 
 @property(nonatomic, readonly, nullable, retain) NSArray<NSString *> *friends NS_DEPRECATED(10_8, 10_10, 4_1, 8_0, "use loadFriendPlayersWithCompletionHandler: instead") __TVOS_UNAVAILABLE; // Array of player identifiers of friends for the local player. Not valid until loadFriendsWithCompletionHandler: has completed.
 
+- (void)loadFriendPlayersWithCompletionHandler:(void(^__nullable)(NSArray<GKPlayer *> * __nullable friendPlayers, NSError * __nullable error))completionHandler NS_DEPRECATED(10_10, 10_11, 8_0, 10_0);
+
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatch.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatch.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatch.h	2016-05-21 08:59:57.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatch.h	2016-06-26 09:16:39.000000000 +0200
@@ -28,7 +28,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 // GKMatch represents an active networking sessions between players. It handles network communications and can report player connection status. All matches are created by a GKMatchmaker.
-NS_CLASS_AVAILABLE(10_8, 4_1)
+NS_CLASS_AVAILABLE(10_8, 4_1) __WATCHOS_PROHIBITED
 @interface GKMatch : NSObject
 
 @property(nonatomic, readonly) NSArray<GKPlayer *> *players NS_AVAILABLE(10_10, 8_0);    // GKPlayers in the match
@@ -87,4 +87,4 @@
 @property(nonatomic, readonly) NSArray<NSString *> *playerIDs NS_DEPRECATED(10_8, 10_10, 4_1, 8_0, "use players") __TVOS_UNAVAILABLE;   // NSStrings of player identifiers in the match
 
 @end
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatchmaker.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatchmaker.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatchmaker.h	2016-05-21 09:29:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKMatchmaker.h	2016-06-26 09:16:39.000000000 +0200
@@ -33,7 +33,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 // GKMatchRequest represents the parameters needed to create the match.
-NS_CLASS_AVAILABLE(10_8, 4_1)
+NS_CLASS_AVAILABLE(10_8, 4_1) __WATCHOS_AVAILABLE(3_0)
 @interface GKMatchRequest : NSObject
 
 @property(assign) NSUInteger minPlayers;     // Minimum number of players for the match
@@ -66,7 +66,7 @@
 
 
 // GKInvite represents an accepted game invite, it is used to create a GKMatchmakerViewController
-NS_CLASS_AVAILABLE(10_8, 4_1)
+NS_CLASS_AVAILABLE(10_8, 4_1) __WATCHOS_PROHIBITED
 @interface GKInvite : NSObject
 
 @property(readonly, retain, NS_NONATOMIC_IOSONLY) GKPlayer *sender NS_AVAILABLE(10_10, 8_0);
@@ -83,17 +83,17 @@
 @optional
 
 // player:didAcceptInvite: gets called when another player accepts the invite from the local player
-- (void)player:(GKPlayer *)player didAcceptInvite:(GKInvite *)invite NS_AVAILABLE(10_10, 7_0);
+- (void)player:(GKPlayer *)player didAcceptInvite:(GKInvite *)invite NS_AVAILABLE(10_10, 7_0) __WATCHOS_PROHIBITED;
 
 // didRequestMatchWithRecipients: gets called when the player chooses to play with another player from Game Center and it launches the game to start matchmaking
-- (void)player:(GKPlayer *)player didRequestMatchWithRecipients:(NSArray<GKPlayer *> *)recipientPlayers NS_AVAILABLE(10_10, 8_0);
+- (void)player:(GKPlayer *)player didRequestMatchWithRecipients:(NSArray<GKPlayer *> *)recipientPlayers NS_AVAILABLE(10_10, 8_0) __WATCHOS_PROHIBITED;
 - (void)player:(GKPlayer *)player didRequestMatchWithPlayers:(NSArray<NSString *> *)playerIDsToInvite NS_DEPRECATED_IOS(7_0, 8_0, "use player:didRequestMatchWithRecipients:") __TVOS_UNAVAILABLE;
 
 @end
 
 
 // GKMatchmaker is a singleton object to manage match creation from invites and auto-matching.
-NS_CLASS_AVAILABLE(10_8, 4_1)
+NS_CLASS_AVAILABLE(10_8, 4_1) __WATCHOS_PROHIBITED
 @interface GKMatchmaker : NSObject
 
 // The shared matchmaker
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKPlayer.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKPlayer.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKPlayer.h	2016-05-21 09:29:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKPlayer.h	2016-06-29 05:49:46.000000000 +0200
@@ -14,7 +14,7 @@
 @class GKGame;
 @class GKLocalPlayer;
 
-NS_CLASS_AVAILABLE(10_8, 4_1)
+NS_CLASS_AVAILABLE(10_8, 4_1) __WATCHOS_AVAILABLE(3_0)
 @interface GKPlayer : GKBasePlayer
 
 // Load the Game Center players for the playerIDs provided. Error will be nil on success.
@@ -27,13 +27,13 @@
 @property(readonly, nullable, retain, NS_NONATOMIC_IOSONLY)  NSString    *playerID;
 
 // This player's full name as displayed in the Game Center in-game UI. Use this when you need to display the player's name. The display name may be very long, so be sure to use appropriate string truncation API when drawing.
-@property(readonly, nullable, NS_NONATOMIC_IOSONLY)          NSString    *displayName NS_AVAILABLE(10_8, 6_0);
+@property(readonly, nullable, NS_NONATOMIC_IOSONLY)          NSString    *displayName NS_AVAILABLE(10_8, 6_0) __WATCHOS_AVAILABLE(3_0);
 
 // The alias property contains the player's nickname. When you need to display the name to the user, consider using displayName instead. The nickname is unique but not invariant: the player may change their nickname. The nickname may be very long, so be sure to use appropriate string truncation API when drawing.
 @property(readonly, copy, nullable, NS_NONATOMIC_IOSONLY)    NSString    *alias;
 
-+ (nonnull instancetype)anonymousGuestPlayerWithIdentifier:(nonnull NSString *)guestIdentifier NS_AVAILABLE(10_11, 9_0);
-@property(readonly, nullable, NS_NONATOMIC_IOSONLY) NSString *guestIdentifier NS_AVAILABLE(10_11, 9_0);
++ (nonnull instancetype)anonymousGuestPlayerWithIdentifier:(nonnull NSString *)guestIdentifier NS_AVAILABLE(10_11, 9_0) __WATCHOS_PROHIBITED;
+@property(readonly, nullable, NS_NONATOMIC_IOSONLY) NSString *guestIdentifier NS_AVAILABLE(10_11, 9_0) __WATCHOS_PROHIBITED;
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKSavedGame.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKSavedGame.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKSavedGame.h	2016-05-21 09:29:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKSavedGame.h	2016-06-29 05:49:46.000000000 +0200
@@ -9,7 +9,7 @@
 #import <GameKit/GKSavedGameListener.h>
 
 // Class representing a saved game for the local player, or a version of a saved game when in conflict
-NS_CLASS_AVAILABLE(10_10, 8_0) __TVOS_UNAVAILABLE
+NS_CLASS_AVAILABLE(10_10, 8_0) __WATCHOS_PROHIBITED __TVOS_UNAVAILABLE
 @interface GKSavedGame : NSObject <NSCopying>
 
 NS_ASSUME_NONNULL_BEGIN
@@ -43,4 +43,4 @@
 @end
 
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKSavedGameListener.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKSavedGameListener.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKSavedGameListener.h	2016-05-21 09:29:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKSavedGameListener.h	2016-06-29 05:49:46.000000000 +0200
@@ -9,7 +9,7 @@
 @class GKSavedGame;
 
 NS_ASSUME_NONNULL_BEGIN
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_10, 8_0) __WATCHOS_PROHIBITED
 @protocol GKSavedGameListener <NSObject>
 @optional
 
@@ -20,4 +20,4 @@
 - (void)player:(GKPlayer *)player hasConflictingSavedGames:(NSArray<GKSavedGame *> *)savedGames NS_AVAILABLE(10_10, 8_0) __TVOS_UNAVAILABLE;
 
 @end
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKScore.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKScore.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKScore.h	2016-05-21 09:29:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKScore.h	2016-06-29 05:49:46.000000000 +0200
@@ -15,38 +15,38 @@
 NS_ASSUME_NONNULL_BEGIN
 
 // GKScore represents a score in the leaderboards.
-NS_CLASS_AVAILABLE(10_8, 4_1)
+NS_CLASS_AVAILABLE(10_8, 4_1) __WATCHOS_AVAILABLE(3_0)
 @interface GKScore : NSObject <NSCoding, NSSecureCoding>
 
 // Initialize the score with the local player and current date.
 - (instancetype)initWithLeaderboardIdentifier:(NSString *)identifier;
 
 // Initialize the achievement for a specific player. Use to submit participant scores when ending a turn-based match.
-- (instancetype)initWithLeaderboardIdentifier:(NSString *)identifier player:(GKPlayer *)player NS_AVAILABLE(10_10, 8_0);
+- (instancetype)initWithLeaderboardIdentifier:(NSString *)identifier player:(GKPlayer *)player NS_AVAILABLE(10_10, 8_0) __WATCHOS_AVAILABLE(3_0);
 
 @property(assign, NS_NONATOMIC_IOSONLY)                     int64_t     value;              // The score value as a 64bit integer.
 @property(readonly, copy, nullable, NS_NONATOMIC_IOSONLY)   NSString    *formattedValue;    // The score formatted as a string, localized with a label
 
 // leaderboard identifier (required)
-@property(copy, NS_NONATOMIC_IOSONLY)               NSString    *leaderboardIdentifier NS_AVAILABLE(10_10, 7_0);
+@property(copy, NS_NONATOMIC_IOSONLY)               NSString    *leaderboardIdentifier NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 // optional additional context that allows a game to store and retrieve additional data associated with the store.  Default value of zero is returned if no value is set.
-@property(assign, NS_NONATOMIC_IOSONLY)                        uint64_t    context NS_AVAILABLE(10_8, 5_0);
+@property(assign, NS_NONATOMIC_IOSONLY)                        uint64_t    context NS_AVAILABLE(10_8, 5_0) __WATCHOS_AVAILABLE(3_0);
 
 @property(readonly, retain, NS_NONATOMIC_IOSONLY)   NSDate      *date;              // The date this score was recorded. A newly initialized, unsubmitted GKScore records the current date at init time.
-@property(readonly, retain, nullable, NS_NONATOMIC_IOSONLY)   GKPlayer    *player NS_AVAILABLE(10_10, 8_0);          // The player that recorded the score.
+@property(readonly, retain, nullable, NS_NONATOMIC_IOSONLY)   GKPlayer    *player NS_AVAILABLE(10_10, 8_0) __WATCHOS_AVAILABLE(3_0);          // The player that recorded the score.
 @property(readonly, assign, NS_NONATOMIC_IOSONLY)   NSInteger   rank;               // The rank of the player within the leaderboard, only valid when returned from GKLeaderboard
 
 // Convenience property to make the leaderboard associated with this GKScore, the default leaderboard for this player. Default value is false.
 // If true, reporting that score will make the category this score belongs to, the default leaderboard for this user
-@property(nonatomic, assign)                        BOOL        shouldSetDefaultLeaderboard     NS_AVAILABLE(10_8, 5_0);
+@property(nonatomic, assign)                        BOOL        shouldSetDefaultLeaderboard     NS_AVAILABLE(10_8, 5_0) __WATCHOS_AVAILABLE(3_0);
 
 // Report scores to the server. The value must be set, and date may be changed.
 // Possible reasons for error:
 // 1. Value not set
 // 2. Local player not authenticated
 // 3. Communications problem
-+ (void)reportScores:(NSArray<GKScore *> *)scores withCompletionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_8, 6_0);
++ (void)reportScores:(NSArray<GKScore *> *)scores withCompletionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_8, 6_0) __WATCHOS_AVAILABLE(3_0);
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKTurnBasedMatch.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKTurnBasedMatch.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKTurnBasedMatch.h	2016-05-21 09:29:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKTurnBasedMatch.h	2016-06-29 05:49:46.000000000 +0200
@@ -52,14 +52,14 @@
 // By default turn based events will badge your app.  To opt out of this add GKGameCenterBadgingDisabled  with a boolean value of YES to your info plist
 
 
-NS_CLASS_AVAILABLE(10_8, 5_0)
+NS_CLASS_AVAILABLE(10_8, 5_0) __WATCHOS_AVAILABLE(3_0)
 @interface GKTurnBasedParticipant : NSObject
 
-@property(readonly, nullable, retain, NS_NONATOMIC_IOSONLY) GKPlayer            *player NS_AVAILABLE(10_10, 8_0);
+@property(readonly, nullable, retain, NS_NONATOMIC_IOSONLY) GKPlayer            *player NS_AVAILABLE(10_10, 8_0) __WATCHOS_AVAILABLE(3_0);
 @property(readonly, nullable, copy, NS_NONATOMIC_IOSONLY) NSDate                *lastTurnDate;
 @property(readonly, NS_NONATOMIC_IOSONLY)       GKTurnBasedParticipantStatus    status;
 @property(assign, NS_NONATOMIC_IOSONLY)         GKTurnBasedMatchOutcome         matchOutcome;
-@property(readonly, nullable, copy, NS_NONATOMIC_IOSONLY) NSDate                *timeoutDate NS_AVAILABLE(10_8, 6_0);
+@property(readonly, nullable, copy, NS_NONATOMIC_IOSONLY) NSDate                *timeoutDate NS_AVAILABLE(10_8, 6_0) __WATCHOS_AVAILABLE(3_0);
 
 // Deprecated
 @property(readonly, nullable, copy, NS_NONATOMIC_IOSONLY) NSString              *playerID NS_DEPRECATED(10_8, 10_10, 5_0, 8_0, "use player") __TVOS_UNAVAILABLE;
@@ -71,7 +71,7 @@
 @optional
 
 // If Game Center initiates a match the developer should create a GKTurnBasedMatch from playersToInvite and present a GKTurnbasedMatchmakerViewController.
-- (void)player:(GKPlayer *)player didRequestMatchWithOtherPlayers:(NSArray<GKPlayer *> *)playersToInvite NS_AVAILABLE(10_10, 8_0);
+- (void)player:(GKPlayer *)player didRequestMatchWithOtherPlayers:(NSArray<GKPlayer *> *)playersToInvite NS_AVAILABLE(10_10, 8_0) __WATCHOS_PROHIBITED;
 
 // called when it becomes this player's turn.  It also gets called under the following conditions:
 //      the player's turn has a timeout and it is about to expire.
@@ -80,22 +80,22 @@
 //      turn was passed to another player
 //      another player saved the match data
 // Because of this the app needs to be prepared to handle this even while the player is taking a turn in an existing match.  The boolean indicates whether this event launched or brought to forground the app.
-- (void)player:(GKPlayer *)player receivedTurnEventForMatch:(GKTurnBasedMatch *)match didBecomeActive:(BOOL)didBecomeActive NS_AVAILABLE(10_10, 7_0);
+- (void)player:(GKPlayer *)player receivedTurnEventForMatch:(GKTurnBasedMatch *)match didBecomeActive:(BOOL)didBecomeActive NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 // called when the match has ended.
 - (void)player:(GKPlayer *)player matchEnded:(GKTurnBasedMatch *)match;
 
 // this is called when a player receives an exchange request from another player.
-- (void)player:(GKPlayer *)player receivedExchangeRequest:(GKTurnBasedExchange *)exchange forMatch:(GKTurnBasedMatch *)match NS_AVAILABLE(10_10, 7_0);
+- (void)player:(GKPlayer *)player receivedExchangeRequest:(GKTurnBasedExchange *)exchange forMatch:(GKTurnBasedMatch *)match NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 // this is called when an exchange is canceled by the sender.
-- (void)player:(GKPlayer *)player receivedExchangeCancellation:(GKTurnBasedExchange *)exchange forMatch:(GKTurnBasedMatch *)match NS_AVAILABLE(10_10, 7_0);
+- (void)player:(GKPlayer *)player receivedExchangeCancellation:(GKTurnBasedExchange *)exchange forMatch:(GKTurnBasedMatch *)match NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 // called when all players either respond or timeout responding to this request.  This is sent to both the turn holder and the initiator of the exchange
-- (void)player:(GKPlayer *)player receivedExchangeReplies:(NSArray<GKTurnBasedExchangeReply *> *)replies forCompletedExchange:(GKTurnBasedExchange *)exchange forMatch:(GKTurnBasedMatch *)match NS_AVAILABLE(10_10, 7_0);
+- (void)player:(GKPlayer *)player receivedExchangeReplies:(NSArray<GKTurnBasedExchangeReply *> *)replies forCompletedExchange:(GKTurnBasedExchange *)exchange forMatch:(GKTurnBasedMatch *)match NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 // Called when a player chooses to quit a match and that player has the current turn.  The developer should call participantQuitInTurnWithOutcome:nextParticipants:turnTimeout:matchData:completionHandler: on the match passing in appropriate values.  They can also update matchOutcome for other players as appropriate.
-- (void)player:(GKPlayer *)player wantsToQuitMatch:(GKTurnBasedMatch *)match NS_AVAILABLE(10_11, 9_0);
+- (void)player:(GKPlayer *)player wantsToQuitMatch:(GKTurnBasedMatch *)match NS_AVAILABLE(10_11, 9_0) __WATCHOS_AVAILABLE(3_0);
 
 // Deprecated
 - (void)player:(GKPlayer *)player didRequestMatchWithPlayers:(NSArray<NSString *> *)playerIDsToInvite NS_DEPRECATED_IOS(7_0, 8_0, "use didRequestMatchWithOtherPlayers") __TVOS_UNAVAILABLE;
@@ -104,11 +104,11 @@
 
 // Turn timeout constants
 
-extern NSTimeInterval        GKTurnTimeoutDefault NS_AVAILABLE(10_9, 6_0);    // use a default timeout of one week
-extern NSTimeInterval        GKTurnTimeoutNone NS_AVAILABLE(10_9, 6_0);
+extern NSTimeInterval        GKTurnTimeoutDefault NS_AVAILABLE(10_9, 6_0) __WATCHOS_AVAILABLE(3_0);    // use a default timeout of one week
+extern NSTimeInterval        GKTurnTimeoutNone NS_AVAILABLE(10_9, 6_0) __WATCHOS_AVAILABLE(3_0);
 
 
-NS_CLASS_AVAILABLE(10_8, 5_0)
+NS_CLASS_AVAILABLE(10_8, 5_0) __WATCHOS_AVAILABLE(3_0)
 @interface GKTurnBasedMatch : NSObject
 
 @property(readonly, nullable, retain, NS_NONATOMIC_IOSONLY)  NSString                           *matchID;
@@ -131,29 +131,29 @@
 // Notes: The localized message will be evaluated locally from these keys and sent across as well so that devices that do not have the game installed will see the message in the sender's localization
 //        The developer can access resulting string using the message property
 //        This is a similar concept to the way we handle localization for Push Notifications. See the "Local and Push Notification Programming Guide" for more details.
-- (void)setLocalizableMessageWithKey:(NSString*)key arguments:(nullable NSArray<NSString *> *)arguments NS_AVAILABLE(10_10, 7_0);
+- (void)setLocalizableMessageWithKey:(NSString*)key arguments:(nullable NSArray<NSString *> *)arguments NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 // returns the localizable message in the current locale. Setting this is equivalent to calling [self setLocalizableMessageWithKey:message arguments:nil]
 @property(readwrite, nullable, copy, NS_NONATOMIC_IOSONLY)   NSString                *message;
 
 
 // Returns the maximum size for the match data.
-@property(readonly, NS_NONATOMIC_IOSONLY)          NSUInteger              matchDataMaximumSize NS_AVAILABLE(10_8, 6_0);
+@property(readonly, NS_NONATOMIC_IOSONLY)          NSUInteger              matchDataMaximumSize NS_AVAILABLE(10_8, 6_0) __WATCHOS_AVAILABLE(3_0);
 
 // exchanges that are in progress on this match.  Once an exchange has completed and has been resolved by merging it into the match data by the current turn holder then it will be removed from this list
-@property(readonly, nullable, retain, NS_NONATOMIC_IOSONLY)  NSArray<GKTurnBasedExchange *>                 *exchanges NS_AVAILABLE(10_10, 7_0);
+@property(readonly, nullable, retain, NS_NONATOMIC_IOSONLY)  NSArray<GKTurnBasedExchange *>                 *exchanges NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 // returns the exchanges that currently await a reply from the local player
-@property(readonly, nullable, retain, NS_NONATOMIC_IOSONLY)  NSArray<GKTurnBasedExchange *>                 *activeExchanges NS_AVAILABLE(10_10, 7_0);
+@property(readonly, nullable, retain, NS_NONATOMIC_IOSONLY)  NSArray<GKTurnBasedExchange *>                 *activeExchanges NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 // returns the exchanges that have been completed and need to be merged by the local participant.  This will be nil unless the local participant is the current turn holder for this match
-@property(readonly, nullable, retain, NS_NONATOMIC_IOSONLY)  NSArray<GKTurnBasedExchange *>                 *completedExchanges NS_AVAILABLE(10_10, 7_0);
+@property(readonly, nullable, retain, NS_NONATOMIC_IOSONLY)  NSArray<GKTurnBasedExchange *>                 *completedExchanges NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 // maximum data allowed for exchange data
-@property(readonly, NS_NONATOMIC_IOSONLY)          NSUInteger              exchangeDataMaximumSize NS_AVAILABLE(10_10, 7_0);
+@property(readonly, NS_NONATOMIC_IOSONLY)          NSUInteger              exchangeDataMaximumSize NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 // limit of the number of exchanges that this player can have initiated at a given time
-@property(readonly, NS_NONATOMIC_IOSONLY)          NSUInteger              exchangeMaxInitiatedExchangesPerPlayer NS_AVAILABLE(10_10, 7_0);
+@property(readonly, NS_NONATOMIC_IOSONLY)          NSUInteger              exchangeMaxInitiatedExchangesPerPlayer NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 // Attempt to find a turn-based match for the specified request. Error will be nil on success.
 // Possible reasons for error:
@@ -165,19 +165,19 @@
 + (void)loadMatchesWithCompletionHandler:(void(^__nullable)(NSArray<GKTurnBasedMatch *> * __nullable matches, NSError * __nullable error))completionHandler;
 
 // load a match based on a previously known match ID
-+ (void)loadMatchWithID:(NSString *)matchID withCompletionHandler:(void(^__nullable)(GKTurnBasedMatch * __nullable match, NSError * __nullable error))completionHandler NS_AVAILABLE(10_8, 5_0);
++ (void)loadMatchWithID:(NSString *)matchID withCompletionHandler:(void(^__nullable)(GKTurnBasedMatch * __nullable match, NSError * __nullable error))completionHandler NS_AVAILABLE(10_8, 5_0) __WATCHOS_AVAILABLE(3_0);
 
 // Recreate a previously existing turn based match that ended. A new match with the same set of players will be returned by the completion handler. If multiple players do this then multiple new matches will be created. Error will be nil on success.
 // Possible reasons for error:
 // 1. Communications failure
 // 2. Unauthenticated player
-- (void)rematchWithCompletionHandler:(void(^__nullable)(GKTurnBasedMatch * __nullable match, NSError * __nullable error))completionHandler NS_AVAILABLE(10_9, 6_0);
+- (void)rematchWithCompletionHandler:(void(^__nullable)(GKTurnBasedMatch * __nullable match, NSError * __nullable error))completionHandler NS_AVAILABLE(10_9, 6_0) __WATCHOS_AVAILABLE(3_0);
 
 // If the local participant has status invited then accept the invite, otherwise returns an error
-- (void)acceptInviteWithCompletionHandler:(void(^__nullable)(GKTurnBasedMatch * __nullable match, NSError * __nullable error))completionHandler NS_AVAILABLE(10_8, 5_0);
+- (void)acceptInviteWithCompletionHandler:(void(^__nullable)(GKTurnBasedMatch * __nullable match, NSError * __nullable error))completionHandler NS_AVAILABLE(10_8, 5_0) __WATCHOS_AVAILABLE(3_0);
 
 // If the local participant has status invited then decline the invite, otherwise returns an error
-- (void)declineInviteWithCompletionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_8, 5_0);
+- (void)declineInviteWithCompletionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_8, 5_0) __WATCHOS_AVAILABLE(3_0);
 
 // Remove a declined or completed match (one with a matchOutcome set) from the player's list of matches. If using the GKTurnBasedMatchmakerViewController UI, this will remove it from the finished sessions.  The developer should not do this without user input.
 - (void)removeWithCompletionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler;
@@ -194,7 +194,7 @@
 - (void)endTurnWithNextParticipants:(NSArray<GKTurnBasedParticipant *> *)nextParticipants
                         turnTimeout:(NSTimeInterval)timeout
                           matchData:(NSData*)matchData
-                 completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_9, 6_0);
+                 completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_9, 6_0) __WATCHOS_AVAILABLE(3_0);
 
 
 // Ends the current player's turn by quitting the match.  The caller must indicate the next player and pass in updated matchData (if used).  All completed exchanges must be resolved or canceled before calling this.
@@ -202,7 +202,7 @@
                         nextParticipants:(NSArray<GKTurnBasedParticipant *> *)nextParticipants
                              turnTimeout:(NSTimeInterval)timeout
                                matchData:(NSData*)matchData
-                       completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_9, 6_0);
+                       completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_9, 6_0) __WATCHOS_AVAILABLE(3_0);
 
 // Abandon the match when it is not the current participant's turn.  In this there is no update to matchData and no need to set nextParticipant.
 - (void)participantQuitOutOfTurnWithOutcome:(GKTurnBasedMatchOutcome)matchOutcome withCompletionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler;
@@ -211,15 +211,15 @@
 - (void)endMatchInTurnWithMatchData:(NSData*)matchData completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler;
 
 // This will end the match and submit scores and achievements for all participants. Scores should be submitted for all involved players, and multiple scores may be submitted for each to different leaderboards. Earned achievements may also be submitted for any participants. You must set each participant’s matchOutcome before calling this method. All completed exchanges must be resolved or canceled before calling this.
-- (void)endMatchInTurnWithMatchData:(NSData*)matchData scores:(nullable NSArray<GKScore *> *)scores achievements:(nullable NSArray<GKAchievement *> *)achievements completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 7_0);
+- (void)endMatchInTurnWithMatchData:(NSData*)matchData scores:(nullable NSArray<GKScore *> *)scores achievements:(nullable NSArray<GKAchievement *> *)achievements completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 // saves the matchData for the current turn without ending the turn.  If other players have the game running they will receive a handleTurnEventForMatch to indicate that the matchData has changed.  This is useful to initialize the game state for the first player when they take their turn or for updating the turn data due to the user taking an irreversible action within their turn.  All completed exchanges must be resolved or canceled before calling this. If you are using exchanges use saveMergedMatchData instead.  
-- (void)saveCurrentTurnWithMatchData:(NSData *)matchData completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_8, 6_0);
+- (void)saveCurrentTurnWithMatchData:(NSData *)matchData completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_8, 6_0) __WATCHOS_AVAILABLE(3_0);
 
 // saves the merged matchData for the current turn without ending the turn and mark the supplied exchanges as resolved meaning that the data has been merged into the match data. If other players have the game running they will receive a handleTurnEventForMatch to indicate that the matchData has changed.  It is required that all completed exchanges are resolved before ending a turn.  Otherwise calling endTurn, participantQuitInTurnWithOutCome or endMatchInTurn will return an error
 - (void)saveMergedMatchData:(NSData *)matchData
       withResolvedExchanges:(NSArray<GKTurnBasedExchange *> *)exchanges
-          completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 7_0);
+          completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 // Send an exchange request to one or more participants.  Each recipient will receive a push notification using supplied localizable message.  If any of the participants have an inactive status (GKTurnBasedParticipantStatusDone) then this will return an error.  completionHandler gets passed the updated exchange with identifier, sender and recipients set
 - (void)sendExchangeToParticipants:(NSArray<GKTurnBasedParticipant *> *)participants
@@ -227,13 +227,13 @@
              localizableMessageKey:(NSString *)key
                          arguments:(NSArray<NSString *> *)arguments
                            timeout:(NSTimeInterval)timeout
-                 completionHandler:(void(^__nullable)(GKTurnBasedExchange *exchange, NSError *error))completionHandler NS_AVAILABLE(10_10, 7_0);
+                 completionHandler:(void(^__nullable)(GKTurnBasedExchange *exchange, NSError *error))completionHandler NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 // Send a reminder to one or more participants.  Each recipient will receive a push notification using supplied localizable message.  This allows a game to send reminders that a turn or exchange request needs action.  On the receiver side this will generate a turn event for the match.
 - (void)sendReminderToParticipants:(NSArray<GKTurnBasedParticipant *> *)participants
              localizableMessageKey:(NSString *)key
                          arguments:(NSArray<NSString *> *)arguments
-                 completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 7_0);
+                 completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
                  
 // deprecated methods
 - (void)endTurnWithNextParticipant:(GKTurnBasedParticipant *)nextParticipant matchData:(NSData*)matchData completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_DEPRECATED(10_8, 10_9, 5_0, 6_0, "Use endTurnWithNextParticipants:... instead") __TVOS_UNAVAILABLE;
@@ -251,15 +251,15 @@
     GKTurnBasedExchangeStatusComplete = 2,
     GKTurnBasedExchangeStatusResolved = 3,
     GKTurnBasedExchangeStatusCanceled = 4
-}  NS_ENUM_AVAILABLE(10_10, 7_0);
+}  NS_ENUM_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 // Exchange timeout constants
 
-extern NSTimeInterval        GKExchangeTimeoutDefault NS_AVAILABLE(10_10, 7_0);    // use a default timeout of one day
-extern NSTimeInterval        GKExchangeTimeoutNone NS_AVAILABLE(10_10, 7_0);
+extern NSTimeInterval        GKExchangeTimeoutDefault NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);    // use a default timeout of one day
+extern NSTimeInterval        GKExchangeTimeoutNone NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 
-NS_CLASS_AVAILABLE(10_10,7_0)
+NS_CLASS_AVAILABLE(10_10,7_0) __WATCHOS_AVAILABLE(3_0)
 @interface  GKTurnBasedExchange : NSObject
 
 @property (readonly, nullable, NS_NONATOMIC_IOSONLY)     NSString                            *exchangeID;         // persistent identifier used to refer to this exchange.
@@ -275,21 +275,21 @@
 @property (readonly, nullable, NS_NONATOMIC_IOSONLY)     NSArray<GKTurnBasedExchangeReply *> *replies;            // Array of GKTurnBasedExchangeReply.
 
 // cancel an exchange. It is possible to cancel an exchange that is active or complete. Each recipient will receive a push notification using supplied localizable message. Returns an error if the exchange has already been canceled.
-- (void)cancelWithLocalizableMessageKey:(NSString *)key arguments:(NSArray<NSString *> *)arguments completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 7_0);
+- (void)cancelWithLocalizableMessageKey:(NSString *)key arguments:(NSArray<NSString *> *)arguments completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 // reply to an exchange. The sender will receive a push notification using supplied localizable message. Returns an error if the exchange has already been canceled.
-- (void)replyWithLocalizableMessageKey:(NSString *)key arguments:(NSArray<NSString *> *)arguments data:(NSData *)data completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 7_0);
+- (void)replyWithLocalizableMessageKey:(NSString *)key arguments:(NSArray<NSString *> *)arguments data:(NSData *)data completionHandler:(void(^__nullable)(NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 7_0) __WATCHOS_AVAILABLE(3_0);
 
 @end
 
     
-NS_CLASS_AVAILABLE(10_10,7_0)
+NS_CLASS_AVAILABLE(10_10,7_0) __WATCHOS_AVAILABLE(3_0)
 @interface GKTurnBasedExchangeReply  : NSObject
 
 @property (readonly, nullable, NS_NONATOMIC_IOSONLY)          GKTurnBasedParticipant         *recipient;          // the recipient who this reply is from
 @property (readonly, nullable, NS_NONATOMIC_IOSONLY)          NSString                       *message;            // localized message for the push notification generated by the reply of this exchange
 @property (readonly, nullable, NS_NONATOMIC_IOSONLY)          NSData                         *data;               // data sent by the replying recipient
-@property (readonly, nullable, NS_NONATOMIC_IOSONLY)          NSDate                         *replyDate NS_AVAILABLE(10_10, 8_0); // send date for the exchange.
+@property (readonly, nullable, NS_NONATOMIC_IOSONLY)          NSDate                         *replyDate NS_AVAILABLE(10_10, 8_0) __WATCHOS_AVAILABLE(3_0); // send date for the exchange.
 @end
 
 // deprecated
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKVoiceChat.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKVoiceChat.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKVoiceChat.h	2016-05-21 09:29:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKVoiceChat.h	2016-06-29 05:49:46.000000000 +0200
@@ -20,7 +20,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 // GKVoiceChat represents an instance of a named voice communications channel
-NS_CLASS_AVAILABLE(10_8, 4_1)
+NS_CLASS_AVAILABLE(10_8, 4_1) __WATCHOS_PROHIBITED
 @interface GKVoiceChat : NSObject
 
 - (void)start;  // start receiving audio from the chat
@@ -48,4 +48,4 @@
 - (void)setMute:(BOOL)isMuted forPlayer:(NSString *)playerID NS_DEPRECATED(10_8, 10_10, 5_0, 8_0, "use setPlayer:muted:") __TVOS_UNAVAILABLE;
 
 @end
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END

```