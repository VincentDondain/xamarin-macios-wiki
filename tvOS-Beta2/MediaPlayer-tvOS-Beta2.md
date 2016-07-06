#MediaPlayer.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPContentItem.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPContentItem.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPContentItem.h	2016-05-28 06:47:30.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPContentItem.h	2016-06-29 05:40:59.000000000 +0200
@@ -50,8 +50,15 @@
 /// Represents whether this content item is explicit content
 @property (nonatomic, assign, getter = isExplicitContent) BOOL explicitContent NS_AVAILABLE_IOS(10_0);
 
+/// Represents whether the content item is a container that may contain other
+/// content items, e.g. an album or a playlist.
 @property (nonatomic, assign, getter = isContainer) BOOL container;
 
+/// Represents whether the content item is actionable from a playback
+/// perspective. Albums are playable, for example, because selecting an album
+/// for playback means the app should play each song in the album in order. An
+/// example of a content item that may not be playable is a genre, since an app
+/// experience typically doesn't involve selecting an entire genre for playback.
 @property (nonatomic, assign, getter = isPlayable) BOOL playable;
 
 @end
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommand.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommand.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommand.h	2016-05-28 06:47:29.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommand.h	2016-06-27 06:38:03.000000000 +0200
@@ -54,6 +54,9 @@
 /// Returns an opaque object to act as the target.
 - (id)addTargetWithHandler:(MPRemoteCommandHandlerStatus(^)(MPRemoteCommandEvent *event))handler;
 
+/// Private constructor.
+- (instancetype)init NS_UNAVAILABLE;
+
 @end
 
 MP_EXTERN_CLASS_AVAILABLE(7_1)
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandCenter.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandCenter.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandCenter.h	2016-05-28 06:47:29.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandCenter.h	2016-06-29 05:40:59.000000000 +0200
@@ -27,8 +27,8 @@
 @property (nonatomic, readonly) MPRemoteCommand *playCommand;
 @property (nonatomic, readonly) MPRemoteCommand *stopCommand;
 @property (nonatomic, readonly) MPRemoteCommand *togglePlayPauseCommand;
-@property (nonatomic, readonly) MPRemoteCommand *enableLanguageOptionCommand;
-@property (nonatomic, readonly) MPRemoteCommand *disableLanguageOptionCommand;
+@property (nonatomic, readonly) MPRemoteCommand *enableLanguageOptionCommand NS_AVAILABLE_IOS(9_0);
+@property (nonatomic, readonly) MPRemoteCommand *disableLanguageOptionCommand NS_AVAILABLE_IOS(9_0);
 @property (nonatomic, readonly) MPChangePlaybackRateCommand *changePlaybackRateCommand;
 @property (nonatomic, readonly) MPChangeRepeatModeCommand *changeRepeatModeCommand;
 @property (nonatomic, readonly) MPChangeShuffleModeCommand *changeShuffleModeCommand;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandEvent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandEvent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandEvent.h	2016-05-28 06:47:29.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandEvent.h	2016-06-27 06:38:03.000000000 +0200
@@ -110,6 +110,9 @@
 /// The desired shuffle type to use when fulfilling the request.
 @property (nonatomic, readonly) MPShuffleType shuffleType;
 
+/// Whether or not the selection should be preserved between playback sessions
+@property (nonatomic, readonly) BOOL preservesShuffleMode;
+
 @end
 
 MP_EXTERN_CLASS_AVAILABLE(8_0)
@@ -118,6 +121,9 @@
 /// The desired repeat type to use when fulfilling the request.
 @property (nonatomic, readonly) MPRepeatType repeatType;
 
+/// Whether or not the selection should be preserved between playback sessions
+@property (nonatomic, readonly) BOOL preservesRepeatMode;
+
 @end
 
 NS_ASSUME_NONNULL_END

```