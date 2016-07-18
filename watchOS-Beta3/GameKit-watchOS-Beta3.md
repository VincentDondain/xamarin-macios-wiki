#GameKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKCloudPlayer.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKCloudPlayer.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKCloudPlayer.h	2016-06-29 06:14:31.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKCloudPlayer.h	2016-07-11 07:47:47.000000000 +0200
@@ -15,8 +15,8 @@
 }
 #endif
 
-// Retrieve a player instance representing the active iCloud account. Returns nil and an error if no iCloud is currently signed in.
-+ (void)getCurrentSignedInPlayer:(void(^)(GKCloudPlayer *__nullable player, NSError * __nullable error))handler;
+// Retrieve a player instance representing the active iCloud account for a given iCloud container. Returns nil and an error if the user is not signed in to iCloud or the container is invalid.
++ (void)getCurrentSignedInPlayerForContainer:(NSString * __nullable)containerName completionHandler:(void(^)(GKCloudPlayer *__nullable player, NSError * __nullable error))handler;
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GameKit.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GameKit.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GameKit.h	2016-06-29 06:14:31.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GameKit.h	2016-07-11 07:47:47.000000000 +0200
@@ -5,6 +5,12 @@
 //  Copyright 2010-2016 Apple Inc. All rights reserved.
 //
 
+#import <TargetConditionals.h>
+#import <simd/simd.h>
+
+#import <SpriteKit/SpriteKit.h>
+#import <SceneKit/SceneKit.h>
+
 #import <GameKit/GKDefines.h>
 #import <GameKit/GKAchievement.h>
 #import <GameKit/GKAchievementDescription.h>

```