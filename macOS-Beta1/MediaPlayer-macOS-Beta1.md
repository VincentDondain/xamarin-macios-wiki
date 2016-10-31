#MediaPlayer.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPContentItem.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPContentItem.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPContentItem.h	2016-09-23 00:57:35.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPContentItem.h	2016-10-25 03:34:26.000000000 +0200
@@ -16,7 +16,7 @@
 /// representation outside the client application. Examples of media items that a
 /// developer might want to represent include song files, streaming audio URLs,
 /// or radio stations.
-MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
+MP_API(ios(7.1), tvos(7.1), macos(10.12.2))
 @interface MPContentItem : NSObject
 
 /// Designated initializer. A unique identifier is required to identify the item
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPError.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPError.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPError.h	2016-09-23 00:57:35.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPError.h	2016-10-25 03:34:26.000000000 +0200
@@ -10,7 +10,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MP_EXTERN NSString * const MPErrorDomain NS_AVAILABLE(10_12_1, 9_3);
+MP_EXTERN NSString * const MPErrorDomain NS_AVAILABLE(10_12_2, 9_3);
 
 // error codes for the MPErrorDomain
 typedef NS_ENUM(NSInteger, MPErrorCode) {
@@ -20,6 +20,7 @@
     MPErrorNetworkConnectionFailed,                 // the device could not connect to the network
     MPErrorNotFound,                                // the id could not be found in the current storefront
     MPErrorNotSupported,                            // the request is not supported (ex: trying to add items to a smart playlist)
+    MPErrorCancelled NS_ENUM_AVAILABLE_IOS(10_1),   // the request was cancelled before it could complete
 } NS_ENUM_AVAILABLE_IOS(9_3);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaEntity.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaEntity.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaEntity.h	2016-09-23 00:57:35.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaEntity.h	2016-10-25 03:34:26.000000000 +0200
@@ -17,7 +17,7 @@
 // An MPMediaEntity represents an abstract member of an MPMediaLibrary.
 // Concrete subclasses are MPMediaItem and MPMediaItemCollection.
 
-MP_API_IOS_AVAILABLE_TVOS_PROHIBITED(4.2)
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(4.2, 10.12.2, 4.2)
 @interface MPMediaEntity : NSObject <NSSecureCoding>
 
 // Returns YES for properties which can be used to construct MPMediaPropertyPredicates.
@@ -36,7 +36,7 @@
 
 #pragma mark - Properties
 
-MP_EXTERN NSString * const MPMediaEntityPropertyPersistentID NS_AVAILABLE(10_12_1, 4_2);        // filterable
+MP_EXTERN NSString * const MPMediaEntityPropertyPersistentID NS_AVAILABLE(10_12_2, 4_2);        // filterable
 @property (nonatomic, readonly) MPMediaEntityPersistentID persistentID NS_AVAILABLE_IOS(7_0);
 
 @end
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaItem.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaItem.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaItem.h	2016-09-23 00:57:35.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaItem.h	2016-10-25 03:34:26.000000000 +0200
@@ -19,32 +19,32 @@
     MPMediaTypeMusic                                        = 1 << 0,
     MPMediaTypePodcast                                      = 1 << 1,
     MPMediaTypeAudioBook                                    = 1 << 2,
-    MPMediaTypeAudioITunesU NS_ENUM_AVAILABLE(10_12_1, 5_0) = 1 << 3,
+    MPMediaTypeAudioITunesU NS_ENUM_AVAILABLE(10_12_2, 5_0) = 1 << 3,
     MPMediaTypeAnyAudio                                     = 0x00ff,
     
     // video (available in iOS 5.0)
-    MPMediaTypeMovie        NS_ENUM_AVAILABLE(10_12_1, 5_0) = 1 << 8,
-    MPMediaTypeTVShow       NS_ENUM_AVAILABLE(10_12_1, 5_0) = 1 << 9,
-    MPMediaTypeVideoPodcast NS_ENUM_AVAILABLE(10_12_1, 5_0) = 1 << 10,
-    MPMediaTypeMusicVideo   NS_ENUM_AVAILABLE(10_12_1, 5_0) = 1 << 11,
-    MPMediaTypeVideoITunesU NS_ENUM_AVAILABLE(10_12_1, 5_0) = 1 << 12,
-    MPMediaTypeHomeVideo    NS_ENUM_AVAILABLE(10_12_1, 7_0) = 1 << 13,
-    MPMediaTypeAnyVideo     NS_ENUM_AVAILABLE(10_12_1, 5_0) = 0xff00,
+    MPMediaTypeMovie        NS_ENUM_AVAILABLE(10_12_2, 5_0) = 1 << 8,
+    MPMediaTypeTVShow       NS_ENUM_AVAILABLE(10_12_2, 5_0) = 1 << 9,
+    MPMediaTypeVideoPodcast NS_ENUM_AVAILABLE(10_12_2, 5_0) = 1 << 10,
+    MPMediaTypeMusicVideo   NS_ENUM_AVAILABLE(10_12_2, 5_0) = 1 << 11,
+    MPMediaTypeVideoITunesU NS_ENUM_AVAILABLE(10_12_2, 5_0) = 1 << 12,
+    MPMediaTypeHomeVideo    NS_ENUM_AVAILABLE(10_12_2, 7_0) = 1 << 13,
+    MPMediaTypeAnyVideo     NS_ENUM_AVAILABLE(10_12_2, 5_0) = 0xff00,
     
     MPMediaTypeAny                                     = ~0UL
-} NS_ENUM_AVAILABLE(10_12_1, 3_0) __TVOS_PROHIBITED;
+} MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(3.0, 10.12.2, 3.0);
 
 // An MPMediaItem represents a single piece of media in an MPMediaLibrary.
 // Media items have a unique identifier which persists across application launches.
 
-MP_API_IOS_AVAILABLE_TVOS_PROHIBITED(3.0)
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(3.0, 10.12.2, 3.0)
 @interface MPMediaItem : MPMediaEntity
 
 #pragma mark - Properties
 
 // Properties marked filterable can also be used to build MPMediaPropertyPredicates (see MPMediaQuery.h).
 
-MP_EXTERN NSString * const MPMediaItemPropertyPersistentID NS_AVAILABLE(10_12_1, 4_2);              // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyPersistentID NS_AVAILABLE(10_12_2, 4_2);              // filterable
 @property (nonatomic, readonly) MPMediaEntityPersistentID persistentID NS_AVAILABLE_IOS(5_0);
 
 MP_EXTERN NSString * const MPMediaItemPropertyMediaType;                                            // filterable
@@ -56,31 +56,31 @@
 MP_EXTERN NSString * const MPMediaItemPropertyAlbumTitle;                                           // filterable
 @property (nonatomic, readonly, nullable) NSString *albumTitle NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyAlbumPersistentID NS_AVAILABLE(10_12_1, 4_2);         // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyAlbumPersistentID NS_AVAILABLE(10_12_2, 4_2);         // filterable
 @property (nonatomic, readonly) MPMediaEntityPersistentID albumPersistentID NS_AVAILABLE_IOS(8_0);
 
 MP_EXTERN NSString * const MPMediaItemPropertyArtist;                                               // filterable
 @property (nonatomic, readonly, nullable) NSString *artist NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyArtistPersistentID NS_AVAILABLE(10_12_1, 4_2);        // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyArtistPersistentID NS_AVAILABLE(10_12_2, 4_2);        // filterable
 @property (nonatomic, readonly) MPMediaEntityPersistentID artistPersistentID NS_AVAILABLE_IOS(8_0);
 
 MP_EXTERN NSString * const MPMediaItemPropertyAlbumArtist;                                          // filterable
 @property (nonatomic, readonly, nullable) NSString *albumArtist NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyAlbumArtistPersistentID NS_AVAILABLE(10_12_1, 4_2);   // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyAlbumArtistPersistentID NS_AVAILABLE(10_12_2, 4_2);   // filterable
 @property (nonatomic, readonly) MPMediaEntityPersistentID albumArtistPersistentID NS_AVAILABLE_IOS(8_0);
 
 MP_EXTERN NSString * const MPMediaItemPropertyGenre;                                                // filterable
 @property (nonatomic, readonly, nullable) NSString *genre NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyGenrePersistentID NS_AVAILABLE(10_12_1, 4_2);         // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyGenrePersistentID NS_AVAILABLE(10_12_2, 4_2);         // filterable
 @property (nonatomic, readonly) MPMediaEntityPersistentID genrePersistentID NS_AVAILABLE_IOS(8_0);
 
 MP_EXTERN NSString * const MPMediaItemPropertyComposer;                                             // filterable
 @property (nonatomic, readonly, nullable) NSString *composer NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyComposerPersistentID NS_AVAILABLE(10_12_1, 4_2);      // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyComposerPersistentID NS_AVAILABLE(10_12_2, 4_2);      // filterable
 @property (nonatomic, readonly) MPMediaEntityPersistentID composerPersistentID NS_AVAILABLE_IOS(8_0);
 
 MP_EXTERN NSString * const MPMediaItemPropertyPlaybackDuration;
@@ -101,7 +101,7 @@
 MP_EXTERN NSString * const MPMediaItemPropertyArtwork;
 @property (nonatomic, readonly, nullable) MPMediaItemArtwork *artwork NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString *const MPMediaItemPropertyIsExplicit NS_AVAILABLE(10_12_1, 7_0);
+MP_EXTERN NSString *const MPMediaItemPropertyIsExplicit NS_AVAILABLE(10_12_2, 7_0);
 @property (nonatomic, readonly, getter = isExplicitItem) BOOL explicitItem NS_AVAILABLE_IOS(10_0);
 
 MP_EXTERN NSString * const MPMediaItemPropertyLyrics;
@@ -110,28 +110,28 @@
 MP_EXTERN NSString * const MPMediaItemPropertyIsCompilation;                                       // filterable
 @property (nonatomic, readonly, getter = isCompilation) BOOL compilation NS_AVAILABLE_IOS(8_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyReleaseDate NS_AVAILABLE(10_12_1, 4_0);
+MP_EXTERN NSString * const MPMediaItemPropertyReleaseDate NS_AVAILABLE(10_12_2, 4_0);
 @property (nonatomic, readonly, nullable) NSDate *releaseDate NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyBeatsPerMinute NS_AVAILABLE(10_12_1, 4_0);
+MP_EXTERN NSString * const MPMediaItemPropertyBeatsPerMinute NS_AVAILABLE(10_12_2, 4_0);
 @property (nonatomic, readonly) NSUInteger beatsPerMinute NS_AVAILABLE_IOS(8_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyComments NS_AVAILABLE(10_12_1, 4_0);
+MP_EXTERN NSString * const MPMediaItemPropertyComments NS_AVAILABLE(10_12_2, 4_0);
 @property (nonatomic, readonly, nullable) NSString *comments NS_AVAILABLE_IOS(8_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyAssetURL NS_AVAILABLE(10_12_1, 4_0);
+MP_EXTERN NSString * const MPMediaItemPropertyAssetURL NS_AVAILABLE(10_12_2, 4_0);
 @property (nonatomic, readonly, nullable) NSURL *assetURL NS_AVAILABLE_IOS(8_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyIsCloudItem NS_AVAILABLE(10_12_1, 6_0);                // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyIsCloudItem NS_AVAILABLE(10_12_2, 6_0);                // filterable
 @property (nonatomic, readonly, getter = isCloudItem) BOOL cloudItem NS_AVAILABLE_IOS(8_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyHasProtectedAsset NS_AVAILABLE(10_12_1, 9_2);          // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyHasProtectedAsset NS_AVAILABLE(10_12_2, 9_2);          // filterable
 @property (nonatomic, readonly, getter = hasProtectedAsset) BOOL protectedAsset NS_AVAILABLE_IOS(9_2);
 
 MP_EXTERN NSString * const MPMediaItemPropertyPodcastTitle;                                          // filterable
 @property (nonatomic, readonly, nullable) NSString *podcastTitle NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyPodcastPersistentID NS_AVAILABLE(10_12_1, 4_2);        // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyPodcastPersistentID NS_AVAILABLE(10_12_2, 4_2);        // filterable
 @property (nonatomic, readonly) MPMediaEntityPersistentID podcastPersistentID NS_AVAILABLE_IOS(8_0);
 
 MP_EXTERN NSString * const MPMediaItemPropertyPlayCount;                                             // filterable
@@ -146,20 +146,20 @@
 MP_EXTERN NSString * const MPMediaItemPropertyLastPlayedDate;
 @property (nonatomic, readonly, nullable) NSDate *lastPlayedDate NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyUserGrouping NS_AVAILABLE(10_12_1, 4_0);
+MP_EXTERN NSString * const MPMediaItemPropertyUserGrouping NS_AVAILABLE(10_12_2, 4_0);
 @property (nonatomic, readonly, nullable) NSString *userGrouping NS_AVAILABLE_IOS(8_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyBookmarkTime NS_AVAILABLE(10_12_1, 6_0);
+MP_EXTERN NSString * const MPMediaItemPropertyBookmarkTime NS_AVAILABLE(10_12_2, 6_0);
 @property (nonatomic, readonly) NSTimeInterval bookmarkTime NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyDateAdded NS_AVAILABLE(10_12_1, 10_0);
+MP_EXTERN NSString * const MPMediaItemPropertyDateAdded NS_AVAILABLE(10_12_2, 10_0);
 @property (nonatomic, readonly) NSDate *dateAdded NS_AVAILABLE_IOS(10_0);
 
 @end
 
 //-----------------------------------------------------
 
-MP_API(ios(3.0), tvos(3.0), macos(10.12.1))
+MP_API(ios(3.0), tvos(3.0), macos(10.12.2))
 @interface MPMediaItemArtwork : NSObject
 
 #if TARGET_OS_IPHONE
@@ -171,10 +171,10 @@
 
 #else
 
-- (instancetype)initWithBoundsSize:(CGSize)boundsSize requestHandler:(NSImage *(^)(CGSize size))requestHandler NS_DESIGNATED_INITIALIZER NS_AVAILABLE_MAC(10_12_1);
+- (instancetype)initWithBoundsSize:(CGSize)boundsSize requestHandler:(NSImage *(^)(CGSize size))requestHandler NS_DESIGNATED_INITIALIZER NS_AVAILABLE_MAC(10_12_2);
 
 // Returns the artwork image for an item at a given size (in points).
-- (nullable NSImage *)imageWithSize:(CGSize)size NS_AVAILABLE_MAC(10_12_1);
+- (nullable NSImage *)imageWithSize:(CGSize)size NS_AVAILABLE_MAC(10_12_2);
 
 #endif
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPNowPlayingInfoCenter.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPNowPlayingInfoCenter.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPNowPlayingInfoCenter.h	2016-09-23 00:57:35.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPNowPlayingInfoCenter.h	2016-10-25 03:34:26.000000000 +0200
@@ -39,7 +39,7 @@
     MPNowPlayingInfoMediaTypeNone = 0,
     MPNowPlayingInfoMediaTypeAudio,
     MPNowPlayingInfoMediaTypeVideo,
-} NS_AVAILABLE(10_12_1, 10_0);
+} NS_AVAILABLE(10_12_2, 10_0);
 
 typedef NS_ENUM(NSUInteger, MPNowPlayingPlaybackState) {
     MPNowPlayingPlaybackStateUnknown = 0,
@@ -47,9 +47,9 @@
     MPNowPlayingPlaybackStatePaused,
     MPNowPlayingPlaybackStateStopped,
     MPNowPlayingPlaybackStateInterrupted
-} NS_AVAILABLE_MAC(10_12_1);
+} NS_AVAILABLE_MAC(10_12_2);
 
-MP_API(ios(5.0), tvos(5.0), macos(10.12.1))
+MP_API(ios(5.0), tvos(5.0), macos(10.12.2))
 @interface MPNowPlayingInfoCenter : NSObject
 
 /// Returns the default now playing info center.
@@ -65,7 +65,7 @@
 /// the application's audio session. This property must be set every time
 /// the app begins or halts playback, otherwise remote control functionality may
 /// not work as expected.
-@property (assign) MPNowPlayingPlaybackState playbackState NS_AVAILABLE_MAC(10_12_1);
+@property (assign) MPNowPlayingPlaybackState playbackState NS_AVAILABLE_MAC(10_12_2);
 
 @end
 
@@ -76,12 +76,12 @@
 // Note the elapsed time will be automatically extrapolated from the previously 
 // provided elapsed time and playback rate, so updating this property frequently
 // is not required (or recommended.)
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyElapsedPlaybackTime NS_AVAILABLE(10_12_1, 5_0); // NSNumber (double)
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyElapsedPlaybackTime NS_AVAILABLE(10_12_2, 5_0); // NSNumber (double)
 
 // The playback rate of the now playing item, with 1.0 representing normal 
 // playback. For example, 2.0 would represent playback at twice the normal rate.
 // If not specified, assumed to be 1.0.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyPlaybackRate NS_AVAILABLE(10_12_1, 5_0); // NSNumber (double)
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyPlaybackRate NS_AVAILABLE(10_12_2, 5_0); // NSNumber (double)
 
 // The "default" playback rate of the now playing item. You should set this
 // property if your app is playing a media item at a rate other than 1.0 in a
@@ -90,47 +90,47 @@
 // playback rate should also be 2.0. Conversely, if you are playing back content
 // at a normal rate (1.0) but the user is fast-forwarding your content at a rate
 // greater than 1.0, then the default playback rate should be set to 1.0.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyDefaultPlaybackRate NS_AVAILABLE(10_12_1, 8_0); // NSNumber (double)
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyDefaultPlaybackRate NS_AVAILABLE(10_12_2, 8_0); // NSNumber (double)
 
 // The index of the now playing item in the application's playback queue.
 // Note that the queue uses zero-based indexing, so the index of the first item 
 // would be 0 if the item should be displayed as "item 1 of 10".
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyPlaybackQueueIndex NS_AVAILABLE(10_12_1, 5_0); // NSNumber (NSUInteger)
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyPlaybackQueueIndex NS_AVAILABLE(10_12_2, 5_0); // NSNumber (NSUInteger)
 
 // The total number of items in the application's playback queue.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyPlaybackQueueCount NS_AVAILABLE(10_12_1, 5_0); // NSNumber (NSUInteger)
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyPlaybackQueueCount NS_AVAILABLE(10_12_2, 5_0); // NSNumber (NSUInteger)
 
 // The chapter currently being played. Note that this is zero-based.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyChapterNumber NS_AVAILABLE(10_12_1, 5_0); // NSNumber (NSUInteger)
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyChapterNumber NS_AVAILABLE(10_12_2, 5_0); // NSNumber (NSUInteger)
 
 // The total number of chapters in the now playing item.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyChapterCount NS_AVAILABLE(10_12_1, 5_0); // NSNumber (NSUInteger)
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyChapterCount NS_AVAILABLE(10_12_2, 5_0); // NSNumber (NSUInteger)
 
 // A boolean denoting whether the now playing item is a live stream.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyIsLiveStream NS_AVAILABLE(10_12_1, 10_0); // NSNumber (BOOL)
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyIsLiveStream NS_AVAILABLE(10_12_2, 10_0); // NSNumber (BOOL)
 
 // A list of available language option groups in the now playing item
 // Only one language option in a given group can be played at once.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyAvailableLanguageOptions NS_AVAILABLE(10_12_1, 9_0); // NSArrayRef of MPNowPlayingInfoLanguageOptionGroup
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyAvailableLanguageOptions NS_AVAILABLE(10_12_2, 9_0); // NSArrayRef of MPNowPlayingInfoLanguageOptionGroup
 
 // A list of currently active language options in the now playing item.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyCurrentLanguageOptions NS_AVAILABLE(10_12_1, 9_0); // NSArray of MPNowPlayingInfoLanguageOption
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyCurrentLanguageOptions NS_AVAILABLE(10_12_2, 9_0); // NSArray of MPNowPlayingInfoLanguageOption
 
 // An identifier that represents the collection to which the now playing item belongs.
 // This can refer to an artist, album, playlist, etc.
 // This can be used to ask the now playing app to resume playback of the collection.
-MP_EXTERN NSString *const MPNowPlayingInfoCollectionIdentifier NS_AVAILABLE(10_12_1, 9_3); // NSString
+MP_EXTERN NSString *const MPNowPlayingInfoCollectionIdentifier NS_AVAILABLE(10_12_2, 9_3); // NSString
 
 // An opaque identifier that uniquely represents the now playing item,
 // even across app relaunches. This can be in any format and is only used to
 // reference this item back to the now playing app.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyExternalContentIdentifier NS_AVAILABLE(10_12_1, 10_0); // NSString
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyExternalContentIdentifier NS_AVAILABLE(10_12_2, 10_0); // NSString
 
 // An optional opaque identifier that uniquely represents the profile that the
 // now playing item is being played from, even across app relauches.
 // This can be in any format and is only used to reference this profile back to
 // the now playing app.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyExternalUserProfileIdentifier NS_AVAILABLE(10_12_1, 10_0); // NSString
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyExternalUserProfileIdentifier NS_AVAILABLE(10_12_2, 10_0); // NSString
 
 // Represents the current playback progress of the now playing item.
 // 0.0 = not watched/listened/viewed, 1.0 = fully watched/listened/viewed
@@ -138,10 +138,10 @@
 // as it is used as a high level indicator as to how far along the user is.
 // For example, a movie may wish to set the now playing item as fully watched
 // when the credits begin to roll.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyPlaybackProgress NS_AVAILABLE(10_12_1, 10_0); // NSNumber (float)
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyPlaybackProgress NS_AVAILABLE(10_12_2, 10_0); // NSNumber (float)
 
 // Indicates the media type of the now playing item
 // This can be used to determine what kind of user interface the system displays.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyMediaType NS_AVAILABLE(10_12_1, 10_0); // NSNumber (MPNowPlayingInfoMediaType)
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyMediaType NS_AVAILABLE(10_12_2, 10_0); // NSNumber (MPNowPlayingInfoMediaType)
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPNowPlayingInfoLanguageOption.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPNowPlayingInfoLanguageOption.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPNowPlayingInfoLanguageOption.h	2016-09-23 00:57:35.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPNowPlayingInfoLanguageOption.h	2016-10-25 03:34:26.000000000 +0200
@@ -22,26 +22,26 @@
 // Common values used to to populate MPNowPlayingInfoLanguageOption's
 // characteristics property.
 // See the AVMediaSelectionOption documentation about Media Characteristics for more details.
-MP_EXTERN NSString *const MPLanguageOptionCharacteristicIsMainProgramContent NS_AVAILABLE(10_12_1, 9_0);
-MP_EXTERN NSString *const MPLanguageOptionCharacteristicIsAuxiliaryContent NS_AVAILABLE(10_12_1, 9_0);
-MP_EXTERN NSString *const MPLanguageOptionCharacteristicContainsOnlyForcedSubtitles NS_AVAILABLE(10_12_1, 9_0);
-MP_EXTERN NSString *const MPLanguageOptionCharacteristicTranscribesSpokenDialog NS_AVAILABLE(10_12_1, 9_0);
-MP_EXTERN NSString *const MPLanguageOptionCharacteristicDescribesMusicAndSound NS_AVAILABLE(10_12_1, 9_0);
-MP_EXTERN NSString *const MPLanguageOptionCharacteristicEasyToRead NS_AVAILABLE(10_12_1, 9_0);
-MP_EXTERN NSString *const MPLanguageOptionCharacteristicDescribesVideo NS_AVAILABLE(10_12_1, 9_0);
-MP_EXTERN NSString *const MPLanguageOptionCharacteristicLanguageTranslation NS_AVAILABLE(10_12_1, 9_0);
-MP_EXTERN NSString *const MPLanguageOptionCharacteristicDubbedTranslation NS_AVAILABLE(10_12_1, 9_0);
-MP_EXTERN NSString *const MPLanguageOptionCharacteristicVoiceOverTranslation NS_AVAILABLE(10_12_1, 9_0);
+MP_EXTERN NSString *const MPLanguageOptionCharacteristicIsMainProgramContent NS_AVAILABLE(10_12_2, 9_0);
+MP_EXTERN NSString *const MPLanguageOptionCharacteristicIsAuxiliaryContent NS_AVAILABLE(10_12_2, 9_0);
+MP_EXTERN NSString *const MPLanguageOptionCharacteristicContainsOnlyForcedSubtitles NS_AVAILABLE(10_12_2, 9_0);
+MP_EXTERN NSString *const MPLanguageOptionCharacteristicTranscribesSpokenDialog NS_AVAILABLE(10_12_2, 9_0);
+MP_EXTERN NSString *const MPLanguageOptionCharacteristicDescribesMusicAndSound NS_AVAILABLE(10_12_2, 9_0);
+MP_EXTERN NSString *const MPLanguageOptionCharacteristicEasyToRead NS_AVAILABLE(10_12_2, 9_0);
+MP_EXTERN NSString *const MPLanguageOptionCharacteristicDescribesVideo NS_AVAILABLE(10_12_2, 9_0);
+MP_EXTERN NSString *const MPLanguageOptionCharacteristicLanguageTranslation NS_AVAILABLE(10_12_2, 9_0);
+MP_EXTERN NSString *const MPLanguageOptionCharacteristicDubbedTranslation NS_AVAILABLE(10_12_2, 9_0);
+MP_EXTERN NSString *const MPLanguageOptionCharacteristicVoiceOverTranslation NS_AVAILABLE(10_12_2, 9_0);
 
 typedef NS_ENUM(NSUInteger, MPNowPlayingInfoLanguageOptionType) {
     MPNowPlayingInfoLanguageOptionTypeAudible,
     MPNowPlayingInfoLanguageOptionTypeLegible,
-} NS_ENUM_AVAILABLE(10_12_1, 9_0);
+} NS_ENUM_AVAILABLE(10_12_2, 9_0);
 
 // -----------------------------------------------------------------------------
 
 /// Represents a single language option option.
-MP_API(ios(9.0), tvos(9.0), macos(10.12.1))
+MP_API(ios(9.0), tvos(9.0), macos(10.12.2))
 @interface MPNowPlayingInfoLanguageOption : NSObject
 
 - (instancetype)initWithType:(MPNowPlayingInfoLanguageOptionType)languageOptionType
@@ -86,7 +86,7 @@
 
 // Represents a mutually exclusive group of language options.
 // Only one language option within a given group may be active at a time.
-MP_API(ios(9.0), tvos(9.0), macos(10.12.1))
+MP_API(ios(9.0), tvos(9.0), macos(10.12.2))
 @interface MPNowPlayingInfoLanguageOptionGroup : NSObject
 
 - (instancetype)initWithLanguageOptions:(NSArray<MPNowPlayingInfoLanguageOption *> *)languageOptions
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentManagerContext.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentManagerContext.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentManagerContext.h	2016-09-23 00:57:35.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentManagerContext.h	2016-10-25 03:34:26.000000000 +0200
@@ -11,7 +11,7 @@
 /// MPPlayableContentManagerContext represents the current state of
 /// the playable content endpoint. A context is retrievable from an instance
 /// of MPPlayableContentManager.
-MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(8.4, 10.12.1, 8.4)
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(8.4, 10.12.2, 8.4)
 @interface MPPlayableContentManagerContext : NSObject
 
 /// The number of items the content server will display when content limiting is enforced.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommand.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommand.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommand.h	2016-09-23 00:57:35.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommand.h	2016-10-25 03:34:26.000000000 +0200
@@ -25,13 +25,13 @@
     /// available that is required for this command. As an example, an
     /// application would return this error code if an "enable language option"
     /// command is received, but nothing is currently playing.
-    MPRemoteCommandHandlerStatusNoActionableNowPlayingItem NS_ENUM_AVAILABLE(10_12_1, 9_1) = 110,
+    MPRemoteCommandHandlerStatusNoActionableNowPlayingItem NS_ENUM_AVAILABLE(10_12_2, 9_1) = 110,
     
     /// The command could not be executed for another reason.
     MPRemoteCommandHandlerStatusCommandFailed = 200
-} NS_ENUM_AVAILABLE(10_12_1, 7_1);
+} NS_ENUM_AVAILABLE(10_12_2, 7_1);
 
-MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
+MP_API(ios(7.1), tvos(7.1), macos(10.12.2))
 @interface MPRemoteCommand : NSObject
 
 /// Whether a button (for example) should be enabled and tappable for this
@@ -59,7 +59,7 @@
 
 @end
 
-MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
+MP_API(ios(7.1), tvos(7.1), macos(10.12.2))
 @interface MPSkipIntervalCommand : MPRemoteCommand
 
 /// An array of NSNumbers (NSTimeIntervals) that contain preferred skip intervals.
@@ -67,7 +67,7 @@
 
 @end
 
-MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
+MP_API(ios(7.1), tvos(7.1), macos(10.12.2))
 @interface MPFeedbackCommand : MPRemoteCommand
 
 /// Whether the feedback command is in an "active" state. An example of when a
@@ -85,7 +85,7 @@
 
 @end
 
-MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
+MP_API(ios(7.1), tvos(7.1), macos(10.12.2))
 @interface MPRatingCommand : MPRemoteCommand
 
 /// Minimum rating for the command.
@@ -96,7 +96,7 @@
 
 @end
 
-MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
+MP_API(ios(7.1), tvos(7.1), macos(10.12.2))
 @interface MPChangePlaybackRateCommand : MPRemoteCommand
 
 /// An array of NSNumbers (floats) that contain supported playback rates that
@@ -107,7 +107,7 @@
 
 /// Command for changing the current playback position in a now playing item.
 /// Sends out MPChangePlaybackPositionCommandEvents.
-MP_API(ios(9.0), tvos(9.0), macos(10.12.1))
+MP_API(ios(9.0), tvos(9.0), macos(10.12.2))
 @interface MPChangePlaybackPositionCommand : MPRemoteCommand
 
 @end
@@ -116,7 +116,7 @@
 /// update the system's current representation of your app's shuffle mode, set
 /// the currentShuffleType property on this command to the proper shuffle type
 /// value.
-MP_API(ios(8.0), tvos(8.0), macos(10.12.1))
+MP_API(ios(8.0), tvos(8.0), macos(10.12.2))
 @interface MPChangeShuffleModeCommand : MPRemoteCommand
 
 @property (nonatomic, assign) MPShuffleType currentShuffleType;
@@ -127,7 +127,7 @@
 /// update the system's current representation of your app's repeat mode, set
 /// the currentRepeatType property on this command to the proper repeat type
 /// value.
-MP_API(ios(8.0), tvos(8.0), macos(10.12.1))
+MP_API(ios(8.0), tvos(8.0), macos(10.12.2))
 @interface MPChangeRepeatModeCommand : MPRemoteCommand
 
 @property (nonatomic, assign) MPRepeatType currentRepeatType;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandCenter.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandCenter.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandCenter.h	2016-09-23 00:57:35.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandCenter.h	2016-10-25 03:34:26.000000000 +0200
@@ -19,7 +19,7 @@
 @class MPRemoteCommand;
 @class MPSkipIntervalCommand;
 
-MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
+MP_API(ios(7.1), tvos(7.1), macos(10.12.2))
 @interface MPRemoteCommandCenter : NSObject
 
 // Playback Commands
@@ -27,8 +27,8 @@
 @property (nonatomic, readonly) MPRemoteCommand *playCommand;
 @property (nonatomic, readonly) MPRemoteCommand *stopCommand;
 @property (nonatomic, readonly) MPRemoteCommand *togglePlayPauseCommand;
-@property (nonatomic, readonly) MPRemoteCommand *enableLanguageOptionCommand NS_AVAILABLE(10_12_1, 9_0);
-@property (nonatomic, readonly) MPRemoteCommand *disableLanguageOptionCommand NS_AVAILABLE(10_12_1, 9_0);
+@property (nonatomic, readonly) MPRemoteCommand *enableLanguageOptionCommand NS_AVAILABLE(10_12_2, 9_0);
+@property (nonatomic, readonly) MPRemoteCommand *disableLanguageOptionCommand NS_AVAILABLE(10_12_2, 9_0);
 @property (nonatomic, readonly) MPChangePlaybackRateCommand *changePlaybackRateCommand;
 @property (nonatomic, readonly) MPChangeRepeatModeCommand *changeRepeatModeCommand;
 @property (nonatomic, readonly) MPChangeShuffleModeCommand *changeShuffleModeCommand;
@@ -44,7 +44,7 @@
 // Seek Commands
 @property (nonatomic, readonly) MPRemoteCommand *seekForwardCommand;
 @property (nonatomic, readonly) MPRemoteCommand *seekBackwardCommand;
-@property (nonatomic, readonly) MPChangePlaybackPositionCommand *changePlaybackPositionCommand NS_AVAILABLE(10_12_1, 9_1);
+@property (nonatomic, readonly) MPChangePlaybackPositionCommand *changePlaybackPositionCommand NS_AVAILABLE(10_12_2, 9_1);
 
 // Rating Command
 @property (nonatomic, readonly) MPRatingCommand *ratingCommand;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandEvent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandEvent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandEvent.h	2016-09-23 00:57:35.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandEvent.h	2016-10-25 03:34:26.000000000 +0200
@@ -14,7 +14,7 @@
 
 @class MPRemoteCommand;
 
-MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
+MP_API(ios(7.1), tvos(7.1), macos(10.12.2))
 @interface MPRemoteCommandEvent : NSObject
 
 /// The command that sent the event.
@@ -25,7 +25,7 @@
 
 @end
 
-MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
+MP_API(ios(7.1), tvos(7.1), macos(10.12.2))
 @interface MPSkipIntervalCommandEvent : MPRemoteCommandEvent
 
 /// The chosen interval for this skip command event.
@@ -36,9 +36,9 @@
 typedef NS_ENUM(NSUInteger, MPSeekCommandEventType) {
     MPSeekCommandEventTypeBeginSeeking,
     MPSeekCommandEventTypeEndSeeking
-} NS_ENUM_AVAILABLE(10_12_1, 7_1);
+} NS_ENUM_AVAILABLE(10_12_2, 7_1);
 
-MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
+MP_API(ios(7.1), tvos(7.1), macos(10.12.2))
 @interface MPSeekCommandEvent : MPRemoteCommandEvent
 
 /// The type of seek command event, which specifies whether an external player
@@ -47,7 +47,7 @@
 
 @end
 
-MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
+MP_API(ios(7.1), tvos(7.1), macos(10.12.2))
 @interface MPRatingCommandEvent : MPRemoteCommandEvent
 
 /// The chosen rating for this command event. This value will be within the
@@ -56,7 +56,7 @@
 
 @end
 
-MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
+MP_API(ios(7.1), tvos(7.1), macos(10.12.2))
 @interface MPChangePlaybackRateCommandEvent : MPRemoteCommandEvent
 
 /// The chosen playback rate for this command event. This value will be equal
@@ -66,7 +66,7 @@
 
 @end
 
-MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
+MP_API(ios(7.1), tvos(7.1), macos(10.12.2))
 @interface MPFeedbackCommandEvent : MPRemoteCommandEvent
 
 /// Whether the command event is a negative operation. For example, the command
@@ -82,7 +82,7 @@
 
 @end
 
-MP_API(ios(9.0), tvos(9.0), macos(10.12.1))
+MP_API(ios(9.0), tvos(9.0), macos(10.12.2))
 @interface MPChangeLanguageOptionCommandEvent : MPRemoteCommandEvent
 
 /// The requested language option to change.
@@ -96,7 +96,7 @@
 
 @end
 
-MP_API(ios(8.0), tvos(8.0), macos(10.12.1))
+MP_API(ios(8.0), tvos(8.0), macos(10.12.2))
 @interface MPChangePlaybackPositionCommandEvent : MPRemoteCommandEvent
 
 /// The desired playback position to use when setting the current time of the player.
@@ -104,7 +104,7 @@
 
 @end
 
-MP_API(ios(8.0), tvos(8.0), macos(10.12.1))
+MP_API(ios(8.0), tvos(8.0), macos(10.12.2))
 @interface MPChangeShuffleModeCommandEvent : MPRemoteCommandEvent
 
 /// The desired shuffle type to use when fulfilling the request.
@@ -115,7 +115,7 @@
 
 @end
 
-MP_API(ios(8.0), tvos(8.0), macos(10.12.1))
+MP_API(ios(8.0), tvos(8.0), macos(10.12.2))
 @interface MPChangeRepeatModeCommandEvent : MPRemoteCommandEvent
 
 /// The desired repeat type to use when fulfilling the request.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteControlTypes.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteControlTypes.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteControlTypes.h	2016-09-23 00:57:35.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteControlTypes.h	2016-10-25 03:34:26.000000000 +0200
@@ -12,16 +12,16 @@
     MPShuffleTypeOff,           /// Nothing is shuffled during playback.
     MPShuffleTypeItems,         /// Individual items are shuffled during playback.
     MPShuffleTypeCollections,   /// Collections (e.g. albums) are shuffled during playback.
-} NS_ENUM_AVAILABLE(10_12_1, 3_0);
+} NS_ENUM_AVAILABLE(10_12_2, 3_0);
 
 typedef NS_ENUM(NSInteger, MPRepeatType) {
     MPRepeatTypeOff,    /// Nothing is repeated during playback.
     MPRepeatTypeOne,    /// Repeat a single item indefinitely.
     MPRepeatTypeAll,    /// Repeat the current container or playlist indefinitely.
-} NS_ENUM_AVAILABLE(10_12_1, 3_0);
+} NS_ENUM_AVAILABLE(10_12_2, 3_0);
 
 typedef NS_ENUM(NSInteger, MPChangeLanguageOptionSetting) {
     MPChangeLanguageOptionSettingNone, /// No Language Option Change
     MPChangeLanguageOptionSettingNowPlayingItemOnly, /// The Language Option change applies only the the now playing item
     MPChangeLanguageOptionSettingPermanent /// The Language Option change should apply to all future playback
-} NS_ENUM_AVAILABLE(10_12_1, 3_0);
+} NS_ENUM_AVAILABLE(10_12_2, 9_4);
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayer.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayer.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayer.h	2016-09-23 00:57:35.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayer.h	2016-10-25 03:34:26.000000000 +0200
@@ -6,6 +6,7 @@
 //
 
 #import <MediaPlayer/MediaPlayerDefines.h>
+#import <TargetConditionals.h>
 
 #if TARGET_OS_IPHONE
 #import <MediaPlayer/MPMediaItemCollection.h>
@@ -17,6 +18,7 @@
 #import <MediaPlayer/MPMoviePlayerController.h>
 #import <MediaPlayer/MPMoviePlayerViewController.h>
 #import <MediaPlayer/MPMusicPlayerController.h>
+#import <MediaPlayer/MPMusicPlayerQueueDescriptor.h>
 #import <MediaPlayer/MPPlayableContentDataSource.h>
 #import <MediaPlayer/MPPlayableContentDelegate.h>
 #import <MediaPlayer/MPPlayableContentManager.h>
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayerDefines.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayerDefines.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayerDefines.h	2016-09-23 00:57:35.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayerDefines.h	2016-10-25 03:34:26.000000000 +0200
@@ -21,9 +21,21 @@
 #define MP_UNAVAILABLE __attribute__((visibility("default"))) __API_UNAVAILABLE
 
 #if __has_include(<AvailabilityProhibitedInternal.h>)
-#define MP_API_IOS_AVAILABLE_TVOS_PROHIBITED(ver) MP_API(ios(ver), tvos(ver))
-#define MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(iosver, macosver, tvosver) MP_API(ios(iosver), tvos(tvosver), macos(macosver))
+#define MP_API_IOS_AVAILABLE_TVOS_PROHIBITED(iosver, macosver, tvosver) MP_API(ios(iosver), tvos(tvosver), macos(macosver)) __TVOS_PROHIBITED
+#define MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(iosver, macosver, tvosver) MP_API(ios(iosver), tvos(tvosver), macos(macosver)) __TVOS_PROHIBITED
+#define MP_API_IOS_DEPRECATED_TVOS_PROHIBITED(iosintro, iosdep, macosintro, macosdep, tvosintro, tvosdep) \
+    MP_DEPRECATED("No longer supported", ios(iosintro, iosdep), tvos(tvosintro, tvosdep), macos(macosintro, macosdep)) __TVOS_PROHIBITED
+#define MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(iosintro, iosdep, macosintro, macosdep, tvosintro, tvosdep) \
+    MP_DEPRECATED("No longer supported", ios(iosintro, iosdep), tvos(tvosintro, tvosdep), macos(macosintro, macosdep)) __TVOS_PROHIBITED
+#define MP_API_IOS_DEPRECATED_WITH_REPLACEMENT_MACOS_TVOS_PROHIBITED(replacement, iosintro, iosdep, macosintro, macosdep, tvosintro, tvosdep) \
+    MP_DEPRECATED_WITH_REPLACEMENT(replacement, ios(iosintro, iosdep), tvos(tvosintro, tvosdep), macos(macosintro, macosdep)) __TVOS_PROHIBITED
 #else
-#define MP_API_IOS_AVAILABLE_TVOS_PROHIBITED(ver) MP_API(ios(ver))
-#define MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(iosver, macosver, tvosver) MP_API(ios(iosver), tvos(tvosver))
+#define MP_API_IOS_AVAILABLE_TVOS_PROHIBITED(iosver, macosver, tvosver) MP_API(ios(iosver), macos(macosver)) __TVOS_PROHIBITED
+#define MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(iosver, macosver, tvosver) MP_API(ios(iosver)) __TVOS_PROHIBITED __OS_AVAILABILITY(macosx,unavailable)
+#define MP_API_IOS_DEPRECATED_TVOS_PROHIBITED(iosintro, iosdep, macosintro, macosdep, tvosintro, tvosdep) \
+    MP_DEPRECATED("No longer supported", ios(iosintro, iosdep), macos(macosintro, macosdep)) __TVOS_PROHIBITED
+#define MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(iosintro, iosdep, macosintro, macosdep, tvosintro, tvosdep) \
+    MP_DEPRECATED("No longer supported", ios(iosintro, iosdep)) __TVOS_PROHIBITED __OS_AVAILABILITY(macosx,unavailable)
+#define MP_API_IOS_DEPRECATED_WITH_REPLACEMENT_MACOS_TVOS_PROHIBITED(replacement, iosintro, iosdep, macosintro, macosdep, tvosintro, tvosdep) \
+    MP_DEPRECATED_WITH_REPLACEMENT(replacement, ios(iosintro, iosdep)) __TVOS_PROHIBITED __OS_AVAILABILITY(macosx,unavailable)
 #endif

```