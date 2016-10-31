#MediaPlayer.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPContentItem.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPContentItem.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPContentItem.h	2016-08-11 06:42:45.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPContentItem.h	2016-10-24 06:54:14.000000000 +0200
@@ -16,7 +16,7 @@
 /// representation outside the client application. Examples of media items that a
 /// developer might want to represent include song files, streaming audio URLs,
 /// or radio stations.
-MP_EXTERN_CLASS_AVAILABLE(7_1)
+MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
 @interface MPContentItem : NSObject
 
 /// Designated initializer. A unique identifier is required to identify the item
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPError.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPError.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPError.h	2016-08-11 06:42:45.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPError.h	2016-10-24 06:54:13.000000000 +0200
@@ -10,7 +10,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MP_EXTERN NSString * const MPErrorDomain NS_AVAILABLE_IOS(9_3);
+MP_EXTERN NSString * const MPErrorDomain NS_AVAILABLE(10_12_1, 9_3);
 
 // error codes for the MPErrorDomain
 typedef NS_ENUM(NSInteger, MPErrorCode) {
@@ -20,6 +20,7 @@
     MPErrorNetworkConnectionFailed,                 // the device could not connect to the network
     MPErrorNotFound,                                // the id could not be found in the current storefront
     MPErrorNotSupported,                            // the request is not supported (ex: trying to add items to a smart playlist)
+    MPErrorCancelled NS_ENUM_AVAILABLE_IOS(10_1),   // the request was cancelled before it could complete
 } NS_ENUM_AVAILABLE_IOS(9_3);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaEntity.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaEntity.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaEntity.h	2016-08-11 06:42:45.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaEntity.h	2016-10-24 06:54:14.000000000 +0200
@@ -17,8 +17,7 @@
 // An MPMediaEntity represents an abstract member of an MPMediaLibrary.
 // Concrete subclasses are MPMediaItem and MPMediaItemCollection.
 
-MP_EXTERN_CLASS_AVAILABLE(4_2)
-__TVOS_PROHIBITED
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(4.2, 10.12.1, 4.2)
 @interface MPMediaEntity : NSObject <NSSecureCoding>
 
 // Returns YES for properties which can be used to construct MPMediaPropertyPredicates.
@@ -37,7 +36,7 @@
 
 #pragma mark - Properties
 
-MP_EXTERN NSString * const MPMediaEntityPropertyPersistentID NS_AVAILABLE_IOS(4_2);         // filterable
+MP_EXTERN NSString * const MPMediaEntityPropertyPersistentID NS_AVAILABLE(10_12_1, 4_2);        // filterable
 @property (nonatomic, readonly) MPMediaEntityPersistentID persistentID NS_AVAILABLE_IOS(7_0);
 
 @end
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaItem.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaItem.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaItem.h	2016-09-25 15:33:24.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaItem.h	2016-10-24 05:31:45.000000000 +0200
@@ -12,76 +12,75 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-@class UIImage, MPMediaItemArtwork;
+@class NSImage, UIImage, MPMediaItemArtwork;
 
 typedef NS_OPTIONS(NSUInteger, MPMediaType) {
     // audio
-    MPMediaTypeMusic                                   = 1 << 0,
-    MPMediaTypePodcast                                 = 1 << 1,
-    MPMediaTypeAudioBook                               = 1 << 2,
-    MPMediaTypeAudioITunesU NS_ENUM_AVAILABLE_IOS(5_0) = 1 << 3,
-    MPMediaTypeAnyAudio                                = 0x00ff,
+    MPMediaTypeMusic                                        = 1 << 0,
+    MPMediaTypePodcast                                      = 1 << 1,
+    MPMediaTypeAudioBook                                    = 1 << 2,
+    MPMediaTypeAudioITunesU NS_ENUM_AVAILABLE(10_12_1, 5_0) = 1 << 3,
+    MPMediaTypeAnyAudio                                     = 0x00ff,
     
     // video (available in iOS 5.0)
-    MPMediaTypeMovie        NS_ENUM_AVAILABLE_IOS(5_0) = 1 << 8,
-    MPMediaTypeTVShow       NS_ENUM_AVAILABLE_IOS(5_0) = 1 << 9,
-    MPMediaTypeVideoPodcast NS_ENUM_AVAILABLE_IOS(5_0) = 1 << 10,
-    MPMediaTypeMusicVideo   NS_ENUM_AVAILABLE_IOS(5_0) = 1 << 11,
-    MPMediaTypeVideoITunesU NS_ENUM_AVAILABLE_IOS(5_0) = 1 << 12,
-    MPMediaTypeHomeVideo    NS_ENUM_AVAILABLE_IOS(7_0) = 1 << 13,
-    MPMediaTypeAnyVideo     NS_ENUM_AVAILABLE_IOS(5_0) = 0xff00,
+    MPMediaTypeMovie        NS_ENUM_AVAILABLE(10_12_1, 5_0) = 1 << 8,
+    MPMediaTypeTVShow       NS_ENUM_AVAILABLE(10_12_1, 5_0) = 1 << 9,
+    MPMediaTypeVideoPodcast NS_ENUM_AVAILABLE(10_12_1, 5_0) = 1 << 10,
+    MPMediaTypeMusicVideo   NS_ENUM_AVAILABLE(10_12_1, 5_0) = 1 << 11,
+    MPMediaTypeVideoITunesU NS_ENUM_AVAILABLE(10_12_1, 5_0) = 1 << 12,
+    MPMediaTypeHomeVideo    NS_ENUM_AVAILABLE(10_12_1, 7_0) = 1 << 13,
+    MPMediaTypeAnyVideo     NS_ENUM_AVAILABLE(10_12_1, 5_0) = 0xff00,
     
     MPMediaTypeAny                                     = ~0UL
-} NS_ENUM_AVAILABLE_IOS(3_0) __TVOS_PROHIBITED;
+} MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(3.0, 10.12.1, 3.0);
 
 // An MPMediaItem represents a single piece of media in an MPMediaLibrary.
 // Media items have a unique identifier which persists across application launches.
 
-MP_EXTERN_CLASS_AVAILABLE(3_0)
-__TVOS_PROHIBITED
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(3.0, 10.12.1, 3.0)
 @interface MPMediaItem : MPMediaEntity
 
 #pragma mark - Properties
 
 // Properties marked filterable can also be used to build MPMediaPropertyPredicates (see MPMediaQuery.h).
 
-MP_EXTERN NSString * const MPMediaItemPropertyPersistentID NS_AVAILABLE_IOS(4_2);               // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyPersistentID NS_AVAILABLE(10_12_1, 4_2);              // filterable
 @property (nonatomic, readonly) MPMediaEntityPersistentID persistentID NS_AVAILABLE_IOS(5_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyMediaType;                                        // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyMediaType;                                            // filterable
 @property (nonatomic, readonly) MPMediaType mediaType NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyTitle;                                            // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyTitle;                                                // filterable
 @property (nonatomic, readonly, nullable) NSString *title NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyAlbumTitle;                                       // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyAlbumTitle;                                           // filterable
 @property (nonatomic, readonly, nullable) NSString *albumTitle NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyAlbumPersistentID NS_AVAILABLE_IOS(4_2);          // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyAlbumPersistentID NS_AVAILABLE(10_12_1, 4_2);         // filterable
 @property (nonatomic, readonly) MPMediaEntityPersistentID albumPersistentID NS_AVAILABLE_IOS(8_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyArtist;                                           // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyArtist;                                               // filterable
 @property (nonatomic, readonly, nullable) NSString *artist NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyArtistPersistentID NS_AVAILABLE_IOS(4_2);         // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyArtistPersistentID NS_AVAILABLE(10_12_1, 4_2);        // filterable
 @property (nonatomic, readonly) MPMediaEntityPersistentID artistPersistentID NS_AVAILABLE_IOS(8_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyAlbumArtist;                                      // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyAlbumArtist;                                          // filterable
 @property (nonatomic, readonly, nullable) NSString *albumArtist NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyAlbumArtistPersistentID NS_AVAILABLE_IOS(4_2);    // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyAlbumArtistPersistentID NS_AVAILABLE(10_12_1, 4_2);   // filterable
 @property (nonatomic, readonly) MPMediaEntityPersistentID albumArtistPersistentID NS_AVAILABLE_IOS(8_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyGenre;                                            // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyGenre;                                                // filterable
 @property (nonatomic, readonly, nullable) NSString *genre NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyGenrePersistentID NS_AVAILABLE_IOS(4_2);          // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyGenrePersistentID NS_AVAILABLE(10_12_1, 4_2);         // filterable
 @property (nonatomic, readonly) MPMediaEntityPersistentID genrePersistentID NS_AVAILABLE_IOS(8_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyComposer;                                         // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyComposer;                                             // filterable
 @property (nonatomic, readonly, nullable) NSString *composer NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyComposerPersistentID NS_AVAILABLE_IOS(4_2);       // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyComposerPersistentID NS_AVAILABLE(10_12_1, 4_2);      // filterable
 @property (nonatomic, readonly) MPMediaEntityPersistentID composerPersistentID NS_AVAILABLE_IOS(8_0);
 
 MP_EXTERN NSString * const MPMediaItemPropertyPlaybackDuration;
@@ -102,40 +101,40 @@
 MP_EXTERN NSString * const MPMediaItemPropertyArtwork;
 @property (nonatomic, readonly, nullable) MPMediaItemArtwork *artwork NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString *const MPMediaItemPropertyIsExplicit NS_AVAILABLE_IOS(7_0);
+MP_EXTERN NSString *const MPMediaItemPropertyIsExplicit NS_AVAILABLE(10_12_1, 7_0);
 @property (nonatomic, readonly, getter = isExplicitItem) BOOL explicitItem NS_AVAILABLE_IOS(10_0);
 
 MP_EXTERN NSString * const MPMediaItemPropertyLyrics;
 @property (nonatomic, readonly, nullable) NSString *lyrics NS_AVAILABLE_IOS(8_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyIsCompilation;                                    // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyIsCompilation;                                       // filterable
 @property (nonatomic, readonly, getter = isCompilation) BOOL compilation NS_AVAILABLE_IOS(8_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyReleaseDate NS_AVAILABLE_IOS(4_0);
+MP_EXTERN NSString * const MPMediaItemPropertyReleaseDate NS_AVAILABLE(10_12_1, 4_0);
 @property (nonatomic, readonly, nullable) NSDate *releaseDate NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyBeatsPerMinute NS_AVAILABLE_IOS(4_0);
+MP_EXTERN NSString * const MPMediaItemPropertyBeatsPerMinute NS_AVAILABLE(10_12_1, 4_0);
 @property (nonatomic, readonly) NSUInteger beatsPerMinute NS_AVAILABLE_IOS(8_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyComments NS_AVAILABLE_IOS(4_0);
+MP_EXTERN NSString * const MPMediaItemPropertyComments NS_AVAILABLE(10_12_1, 4_0);
 @property (nonatomic, readonly, nullable) NSString *comments NS_AVAILABLE_IOS(8_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyAssetURL NS_AVAILABLE_IOS(4_0);
+MP_EXTERN NSString * const MPMediaItemPropertyAssetURL NS_AVAILABLE(10_12_1, 4_0);
 @property (nonatomic, readonly, nullable) NSURL *assetURL NS_AVAILABLE_IOS(8_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyIsCloudItem NS_AVAILABLE_IOS(6_0);                // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyIsCloudItem NS_AVAILABLE(10_12_1, 6_0);                // filterable
 @property (nonatomic, readonly, getter = isCloudItem) BOOL cloudItem NS_AVAILABLE_IOS(8_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyHasProtectedAsset NS_AVAILABLE_IOS(9_2);          // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyHasProtectedAsset NS_AVAILABLE(10_12_1, 9_2);          // filterable
 @property (nonatomic, readonly, getter = hasProtectedAsset) BOOL protectedAsset NS_AVAILABLE_IOS(9_2);
 
-MP_EXTERN NSString * const MPMediaItemPropertyPodcastTitle;                                     // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyPodcastTitle;                                          // filterable
 @property (nonatomic, readonly, nullable) NSString *podcastTitle NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyPodcastPersistentID NS_AVAILABLE_IOS(4_2);        // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyPodcastPersistentID NS_AVAILABLE(10_12_1, 4_2);        // filterable
 @property (nonatomic, readonly) MPMediaEntityPersistentID podcastPersistentID NS_AVAILABLE_IOS(8_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyPlayCount;                                        // filterable
+MP_EXTERN NSString * const MPMediaItemPropertyPlayCount;                                             // filterable
 @property (nonatomic, readonly) NSUInteger playCount NS_AVAILABLE_IOS(7_0);
 
 MP_EXTERN NSString * const MPMediaItemPropertySkipCount;
@@ -147,31 +146,45 @@
 MP_EXTERN NSString * const MPMediaItemPropertyLastPlayedDate;
 @property (nonatomic, readonly, nullable) NSDate *lastPlayedDate NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyUserGrouping NS_AVAILABLE_IOS(4_0);
+MP_EXTERN NSString * const MPMediaItemPropertyUserGrouping NS_AVAILABLE(10_12_1, 4_0);
 @property (nonatomic, readonly, nullable) NSString *userGrouping NS_AVAILABLE_IOS(8_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyBookmarkTime NS_AVAILABLE_IOS(6_0);
+MP_EXTERN NSString * const MPMediaItemPropertyBookmarkTime NS_AVAILABLE(10_12_1, 6_0);
 @property (nonatomic, readonly) NSTimeInterval bookmarkTime NS_AVAILABLE_IOS(7_0);
 
-MP_EXTERN NSString * const MPMediaItemPropertyDateAdded NS_AVAILABLE_IOS(10_0);
+MP_EXTERN NSString * const MPMediaItemPropertyDateAdded NS_AVAILABLE(10_12_1, 10_0);
 @property (nonatomic, readonly) NSDate *dateAdded NS_AVAILABLE_IOS(10_0);
 
 @end
 
 //-----------------------------------------------------
 
-MP_EXTERN_CLASS_AVAILABLE(3_0)
+MP_API(ios(3.0), tvos(3.0), macos(10.12.1))
 @interface MPMediaItemArtwork : NSObject
 
+#if TARGET_OS_IPHONE
+
 - (instancetype)initWithBoundsSize:(CGSize)boundsSize requestHandler:(UIImage *(^)(CGSize size))requestHandler NS_DESIGNATED_INITIALIZER NS_AVAILABLE_IOS(10_0);
 
 // Returns the artwork image for an item at a given size (in points).
 - (nullable UIImage *)imageWithSize:(CGSize)size;
 
-@property (nonatomic, readonly) CGRect bounds; // The bounds of the full size image (in points).
+#else
+
+- (instancetype)initWithBoundsSize:(CGSize)boundsSize requestHandler:(NSImage *(^)(CGSize size))requestHandler NS_DESIGNATED_INITIALIZER NS_AVAILABLE_MAC(10_12_1);
+
+// Returns the artwork image for an item at a given size (in points).
+- (nullable NSImage *)imageWithSize:(CGSize)size NS_AVAILABLE_MAC(10_12_1);
 
+#endif
+
+@property (nonatomic, readonly) CGRect bounds; // The bounds of the full size image (in points).
 @property (nonatomic, readonly) CGRect imageCropRect NS_DEPRECATED_IOS(3_0, 10_0);
+
+#if TARGET_OS_IPHONE
 - (instancetype)initWithImage:(UIImage *)image NS_DEPRECATED_IOS(5_0, 10_0);
+#endif
+
 - (id)init NS_UNAVAILABLE;
 
 @end
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaItemCollection.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaItemCollection.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaItemCollection.h	2016-08-11 06:42:45.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaItemCollection.h	2016-10-24 06:54:13.000000000 +0200
@@ -13,8 +13,7 @@
 
 // An MPMediaItemCollection is a collection of related MPMediaItems in a media library.
 
-MP_EXTERN_CLASS_AVAILABLE(3_0)
-__TVOS_PROHIBITED
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(3.0, 10.12.1, 3.0)
 @interface MPMediaItemCollection : MPMediaEntity
 
 // Creates a media item collection by copying an array of MPMediaItems.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaLibrary.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaLibrary.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaLibrary.h	2016-08-11 06:42:45.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaLibrary.h	2016-10-24 06:54:13.000000000 +0200
@@ -30,8 +30,7 @@
     MPMediaLibraryAuthorizationStatusAuthorized,
 } NS_ENUM_AVAILABLE_IOS(9_3);
 
-MP_EXTERN_CLASS_AVAILABLE(3_0)
-__TVOS_PROHIBITED
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(3.0, 10.12.1, 3.0)
 @interface MPMediaLibrary : NSObject <NSSecureCoding>
 
 + (MPMediaLibrary *)defaultMediaLibrary;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaPickerController.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaPickerController.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaPickerController.h	2016-08-11 06:42:45.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaPickerController.h	2016-10-24 06:54:13.000000000 +0200
@@ -18,8 +18,7 @@
 // MPMediaPickerController is a UIViewController for visually selecting media items.
 // To display it, present it modally on an existing view controller.
 
-MP_EXTERN_CLASS_AVAILABLE(3_0)
-__TVOS_PROHIBITED
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(3.0, 10.12.1, 3.0)
 @interface MPMediaPickerController : UIViewController
 
 - (instancetype)initWithMediaTypes:(MPMediaType)mediaTypes NS_DESIGNATED_INITIALIZER;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaPlaylist.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaPlaylist.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaPlaylist.h	2016-08-11 06:42:45.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaPlaylist.h	2016-10-24 06:54:13.000000000 +0200
@@ -19,13 +19,12 @@
     MPMediaPlaylistAttributeOnTheGo = (1 << 0), // if set, the playlist was created on a device rather than synced from iTunes
     MPMediaPlaylistAttributeSmart   = (1 << 1),
     MPMediaPlaylistAttributeGenius  = (1 << 2)
-} NS_ENUM_AVAILABLE_IOS(3_0) __TVOS_PROHIBITED;
+} MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(3.0, 10.12.1, 3.0);
 
 // An MPMediaPlaylist is a collection of related MPMediaItems in an MPMediaLibrary.
 // Playlists have a unique identifier which persists across application launches.
 
-MP_EXTERN_CLASS_AVAILABLE(3_0)
-__TVOS_PROHIBITED
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(3.0, 10.12.1, 3.0)
 @interface MPMediaPlaylist : MPMediaItemCollection
 
 #pragma mark - Properties
@@ -57,8 +56,7 @@
 
 @end
 
-MP_EXTERN_CLASS_AVAILABLE(9_3)
-__TVOS_PROHIBITED
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(9.3, 10.12.1, 9.3)
 @interface MPMediaPlaylistCreationMetadata : NSObject
 
 - (id)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaQuery.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaQuery.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaQuery.h	2016-08-05 08:27:48.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaQuery.h	2016-10-24 06:38:13.000000000 +0200
@@ -24,12 +24,11 @@
     MPMediaGroupingGenre,
     MPMediaGroupingPlaylist,
     MPMediaGroupingPodcastTitle
-} NS_ENUM_AVAILABLE_IOS(3_0) __TVOS_PROHIBITED;
+} MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(3.0, 10.12.1, 3.0);
 
 // MPMediaQuery represents a collection of items or playlists determined by a chain of MPMediaPredicate objects.
 
-MP_EXTERN_CLASS_AVAILABLE(3_0)
-__TVOS_PROHIBITED
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(3.0, 10.12.1, 3.0)
 @interface MPMediaQuery : NSObject <NSSecureCoding, NSCopying>
 
 - (instancetype)initWithFilterPredicates:(nullable NSSet<MPMediaPredicate *> *)filterPredicates NS_DESIGNATED_INITIALIZER;
@@ -71,8 +70,7 @@
 // MPMediaPredicate is an abstract class that allows filtering media in an MPMediaQuery.
 // See the concrete subclass MPMediaPropertyPredicate for filtering options.
 
-MP_EXTERN_CLASS_AVAILABLE(3_0)
-__TVOS_PROHIBITED
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(3.0, 10.12.1, 3.0)
 @interface MPMediaPredicate : NSObject <NSSecureCoding> {}
 @end
 
@@ -83,10 +81,9 @@
 typedef NS_ENUM(NSInteger, MPMediaPredicateComparison) {
     MPMediaPredicateComparisonEqualTo,
     MPMediaPredicateComparisonContains
-} NS_ENUM_AVAILABLE_IOS(3_0) __TVOS_PROHIBITED;
+} MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(3.0, 10.12.1, 3.0);
 
-MP_EXTERN_CLASS_AVAILABLE(3_0)
-__TVOS_PROHIBITED
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(3.0, 10.12.1, 3.0)
 @interface MPMediaPropertyPredicate : MPMediaPredicate
 
 + (MPMediaPropertyPredicate *)predicateWithValue:(nullable id)value forProperty:(NSString *)property; // comparisonType is MPMediaPredicateComparisonEqualTo
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaQuerySection.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaQuerySection.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaQuerySection.h	2016-08-11 06:42:45.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaQuerySection.h	2016-10-24 06:54:14.000000000 +0200
@@ -12,8 +12,7 @@
 
 // An MPMediaQuerySection object represents a single section grouping for a query.
 
-MP_EXTERN_CLASS_AVAILABLE(4_2)
-__TVOS_PROHIBITED
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(4.2, 10.12.1, 4.2)
 @interface MPMediaQuerySection : NSObject <NSSecureCoding, NSCopying>
 
 // The localized title of the section grouping.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMoviePlayerController.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMoviePlayerController.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMoviePlayerController.h	2016-08-05 08:27:47.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMoviePlayerController.h	2016-10-24 05:31:44.000000000 +0200
@@ -6,6 +6,7 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <MediaPlayer/MediaPlayerDefines.h>
 #import <MediaPlayer/MPMediaPlayback.h>
 #import <UIKit/UIKit.h>
 
@@ -19,7 +20,7 @@
     MPMovieScalingModeAspectFit,  // Uniform scale until one dimension fits
     MPMovieScalingModeAspectFill, // Uniform scale until the movie fills the visible bounds. One dimension may have clipped contents
     MPMovieScalingModeFill        // Non-uniform scale. Both render dimensions will exactly match the visible bounds
-} NS_DEPRECATED_IOS(2_0, 9_0) __TVOS_PROHIBITED;
+} MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(2.0, 9.0, 10.12.1, 10.12.1, 2.0, 9.0);
 
 typedef NS_ENUM(NSInteger, MPMoviePlaybackState) {
     MPMoviePlaybackStateStopped,
@@ -28,19 +29,19 @@
     MPMoviePlaybackStateInterrupted,
     MPMoviePlaybackStateSeekingForward,
     MPMoviePlaybackStateSeekingBackward
-} NS_DEPRECATED_IOS(3_2, 9_0) __TVOS_PROHIBITED;
+} MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
 
 typedef NS_OPTIONS(NSUInteger, MPMovieLoadState) {
     MPMovieLoadStateUnknown        = 0,
     MPMovieLoadStatePlayable       = 1 << 0,
     MPMovieLoadStatePlaythroughOK  = 1 << 1, // Playback will be automatically started in this state when shouldAutoplay is YES
     MPMovieLoadStateStalled        = 1 << 2, // Playback will be automatically paused in this state, if started
-} NS_DEPRECATED_IOS(3_2, 9_0) __TVOS_PROHIBITED;
+} MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
 
 typedef NS_ENUM(NSInteger, MPMovieRepeatMode) {
     MPMovieRepeatModeNone,
     MPMovieRepeatModeOne
-} NS_DEPRECATED_IOS(3_2, 9_0) __TVOS_PROHIBITED;
+} MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
 
 typedef NS_ENUM(NSInteger, MPMovieControlStyle) {
     MPMovieControlStyleNone,       // No controls
@@ -48,13 +49,13 @@
     MPMovieControlStyleFullscreen, // Controls for fullscreen playback
     
     MPMovieControlStyleDefault = MPMovieControlStyleEmbedded
-} NS_DEPRECATED_IOS(3_2, 9_0) __TVOS_PROHIBITED;
+} MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
 
 typedef NS_ENUM(NSInteger, MPMovieFinishReason) {
     MPMovieFinishReasonPlaybackEnded,
     MPMovieFinishReasonPlaybackError,
     MPMovieFinishReasonUserExited
-} NS_DEPRECATED_IOS(3_2, 9_0) __TVOS_PROHIBITED;
+} MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
 
 // -----------------------------------------------------------------------------
 // Movie Property Types
@@ -63,22 +64,20 @@
     MPMovieMediaTypeMaskNone  = 0,
     MPMovieMediaTypeMaskVideo = 1 << 0,
     MPMovieMediaTypeMaskAudio = 1 << 1
-} NS_DEPRECATED_IOS(3_2, 9_0) __TVOS_PROHIBITED;
+} MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
 
 typedef NS_ENUM(NSInteger, MPMovieSourceType) {
     MPMovieSourceTypeUnknown,
     MPMovieSourceTypeFile,     // Local or progressively downloaded network content
     MPMovieSourceTypeStreaming // Live or on-demand streaming content
-} NS_DEPRECATED_IOS(3_2, 9_0) __TVOS_PROHIBITED;
+} MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
 
 // -----------------------------------------------------------------------------
 // Movie Player
 // 
 // See MPMediaPlayback.h for the playback methods.
 
-MP_EXTERN_CLASS_AVAILABLE(2_0)
-NS_DEPRECATED_IOS(2_0, 9_0, "Use AVPlayerViewController in AVKit.")
-__TVOS_PROHIBITED
+MP_API_IOS_DEPRECATED_WITH_REPLACEMENT_MACOS_TVOS_PROHIBITED("Use AVPlayerViewController in AVKit.", 2.0, 9.0, 10.12.1, 10.12.1, 2.0, 9.0)
 @interface MPMoviePlayerController : NSObject <MPMediaPlayback>
 
 - (instancetype)initWithContentURL:(NSURL *)url NS_DESIGNATED_INITIALIZER;
@@ -126,39 +125,39 @@
 @interface MPMoviePlayerController (MPMovieProperties)
 
 // The types of media in the movie, or MPMovieMediaTypeNone if not known.
-@property (nonatomic, readonly) MPMovieMediaTypeMask movieMediaTypes NS_DEPRECATED_IOS(2_0, 9_0, "Use AVPlayerViewController in AVKit.");
+@property (nonatomic, readonly) MPMovieMediaTypeMask movieMediaTypes MP_API_IOS_DEPRECATED_WITH_REPLACEMENT_MACOS_TVOS_PROHIBITED("Use AVPlayerViewController in AVKit.", 2.0, 9.0, 10.12.1, 10.12.1, 2.0, 9.0);
 
 // The playback type of the movie. Defaults to MPMovieSourceTypeUnknown.
 // Specifying a playback type before playing the movie can result in faster load times.
-@property (nonatomic) MPMovieSourceType movieSourceType NS_DEPRECATED_IOS(2_0, 9_0, "Use AVPlayerViewController in AVKit.")
+@property (nonatomic) MPMovieSourceType movieSourceType MP_API_IOS_DEPRECATED_WITH_REPLACEMENT_MACOS_TVOS_PROHIBITED("Use AVPlayerViewController in AVKit.", 2.0, 9.0, 10.12.1, 10.12.1, 2.0, 9.0)
 ;
 
 // The duration of the movie, or 0.0 if not known.
-@property (nonatomic, readonly) NSTimeInterval duration NS_DEPRECATED_IOS(2_0, 9_0, "Use AVPlayerViewController in AVKit.")
+@property (nonatomic, readonly) NSTimeInterval duration MP_API_IOS_DEPRECATED_WITH_REPLACEMENT_MACOS_TVOS_PROHIBITED("Use AVPlayerViewController in AVKit.", 2.0, 9.0, 10.12.1, 10.12.1, 2.0, 9.0)
 ;
 
 // The currently playable duration of the movie, for progressively downloaded network content.
-@property (nonatomic, readonly) NSTimeInterval playableDuration NS_DEPRECATED_IOS(2_0, 9_0, "Use AVPlayerViewController in AVKit.")
+@property (nonatomic, readonly) NSTimeInterval playableDuration MP_API_IOS_DEPRECATED_WITH_REPLACEMENT_MACOS_TVOS_PROHIBITED("Use AVPlayerViewController in AVKit.", 2.0, 9.0, 10.12.1, 10.12.1, 2.0, 9.0)
 ;
 
 // The natural size of the movie, or CGSizeZero if not known/applicable.
-@property (nonatomic, readonly) CGSize naturalSize NS_DEPRECATED_IOS(2_0, 9_0, "Use AVPlayerViewController in AVKit.")
+@property (nonatomic, readonly) CGSize naturalSize MP_API_IOS_DEPRECATED_WITH_REPLACEMENT_MACOS_TVOS_PROHIBITED("Use AVPlayerViewController in AVKit.", 2.0, 9.0, 10.12.1, 10.12.1, 2.0, 9.0)
 ;
 
 // The start time of movie playback. Defaults to NaN, indicating the natural start time of the movie.
-@property (nonatomic) NSTimeInterval initialPlaybackTime NS_DEPRECATED_IOS(2_0, 9_0, "Use AVPlayerViewController in AVKit.")
+@property (nonatomic) NSTimeInterval initialPlaybackTime MP_API_IOS_DEPRECATED_WITH_REPLACEMENT_MACOS_TVOS_PROHIBITED("Use AVPlayerViewController in AVKit.", 2.0, 9.0, 10.12.1, 10.12.1, 2.0, 9.0)
 ;
 
 // The end time of movie playback. Defaults to NaN, which indicates natural end time of the movie.
-@property (nonatomic) NSTimeInterval endPlaybackTime NS_DEPRECATED_IOS(2_0, 9_0, "Use AVPlayerViewController in AVKit.")
+@property (nonatomic) NSTimeInterval endPlaybackTime MP_API_IOS_DEPRECATED_WITH_REPLACEMENT_MACOS_TVOS_PROHIBITED("Use AVPlayerViewController in AVKit.", 2.0, 9.0, 10.12.1, 10.12.1, 2.0, 9.0)
 ;
 
 // Indicates whether the movie player allows AirPlay video playback. Defaults to YES on iOS 5.0 and later.
-@property (nonatomic) BOOL allowsAirPlay NS_DEPRECATED_IOS(4_3, 9_0, "Use AVPlayerViewController in AVKit.")
+@property (nonatomic) BOOL allowsAirPlay MP_API_IOS_DEPRECATED_WITH_REPLACEMENT_MACOS_TVOS_PROHIBITED("Use AVPlayerViewController in AVKit.", 4.3, 9.0, 10.12.1, 10.12.1, 4.3, 9.0)
 ;
 
 // Indicates whether the movie player is currently playing video via AirPlay.
-@property (nonatomic, readonly, getter=isAirPlayVideoActive) BOOL airPlayVideoActive NS_DEPRECATED_IOS(5_0, 9_0, "Use AVPlayerViewController in AVKit.")
+@property (nonatomic, readonly, getter=isAirPlayVideoActive) BOOL airPlayVideoActive MP_API_IOS_DEPRECATED_WITH_REPLACEMENT_MACOS_TVOS_PROHIBITED("Use AVPlayerViewController in AVKit.", 5.0, 9.0, 10.12.1, 10.12.1, 5.0, 9.0)
 ;
 
 @end
@@ -167,45 +166,45 @@
 // Movie Player Notifications
 
 // Posted when the scaling mode changes.
-MP_EXTERN NSString * const MPMoviePlayerScalingModeDidChangeNotification NS_DEPRECATED_IOS(2_0, 9_0);
+MP_EXTERN NSString * const MPMoviePlayerScalingModeDidChangeNotification MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(2.0, 9.0, 10.12.1, 10.12.1, 2.0, 9.0);
 
 // Posted when movie playback ends or a user exits playback.
-MP_EXTERN NSString * const MPMoviePlayerPlaybackDidFinishNotification NS_DEPRECATED_IOS(2_0, 9_0);
+MP_EXTERN NSString * const MPMoviePlayerPlaybackDidFinishNotification MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(2.0, 9.0, 10.12.1, 10.12.1, 2.0, 9.0);
 
-MP_EXTERN NSString * const MPMoviePlayerPlaybackDidFinishReasonUserInfoKey NS_DEPRECATED_IOS(3_2, 9_0); // NSNumber (MPMovieFinishReason)
+MP_EXTERN NSString * const MPMoviePlayerPlaybackDidFinishReasonUserInfoKey MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0); // NSNumber (MPMovieFinishReason)
 
 // Posted when the playback state changes, either programatically or by the user.
-MP_EXTERN NSString * const MPMoviePlayerPlaybackStateDidChangeNotification NS_DEPRECATED_IOS(3_2, 9_0);
+MP_EXTERN NSString * const MPMoviePlayerPlaybackStateDidChangeNotification MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
 
 // Posted when the network load state changes.
-MP_EXTERN NSString * const MPMoviePlayerLoadStateDidChangeNotification NS_DEPRECATED_IOS(3_2, 9_0);
+MP_EXTERN NSString * const MPMoviePlayerLoadStateDidChangeNotification MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
 
 // Posted when the currently playing movie changes.
-MP_EXTERN NSString * const MPMoviePlayerNowPlayingMovieDidChangeNotification NS_DEPRECATED_IOS(3_2, 9_0);
+MP_EXTERN NSString * const MPMoviePlayerNowPlayingMovieDidChangeNotification MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
 
 // Posted when the movie player enters or exits fullscreen mode.
-MP_EXTERN NSString * const MPMoviePlayerWillEnterFullscreenNotification NS_DEPRECATED_IOS(3_2, 9_0);
-MP_EXTERN NSString * const MPMoviePlayerDidEnterFullscreenNotification NS_DEPRECATED_IOS(3_2, 9_0);
-MP_EXTERN NSString * const MPMoviePlayerWillExitFullscreenNotification NS_DEPRECATED_IOS(3_2, 9_0);
-MP_EXTERN NSString * const MPMoviePlayerDidExitFullscreenNotification NS_DEPRECATED_IOS(3_2, 9_0);
-MP_EXTERN NSString * const MPMoviePlayerFullscreenAnimationDurationUserInfoKey NS_DEPRECATED_IOS(3_2, 9_0); // NSNumber of double (NSTimeInterval)
-MP_EXTERN NSString * const MPMoviePlayerFullscreenAnimationCurveUserInfoKey NS_DEPRECATED_IOS(3_2, 9_0);     // NSNumber of NSUInteger (UIViewAnimationCurve)
+MP_EXTERN NSString * const MPMoviePlayerWillEnterFullscreenNotification MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
+MP_EXTERN NSString * const MPMoviePlayerDidEnterFullscreenNotification MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
+MP_EXTERN NSString * const MPMoviePlayerWillExitFullscreenNotification MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
+MP_EXTERN NSString * const MPMoviePlayerDidExitFullscreenNotification MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
+MP_EXTERN NSString * const MPMoviePlayerFullscreenAnimationDurationUserInfoKey MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0); // NSNumber of double (NSTimeInterval)
+MP_EXTERN NSString * const MPMoviePlayerFullscreenAnimationCurveUserInfoKey MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);     // NSNumber of NSUInteger (UIViewAnimationCurve)
 
 // Posted when the movie player begins or ends playing video via AirPlay.
-MP_EXTERN NSString * const MPMoviePlayerIsAirPlayVideoActiveDidChangeNotification NS_DEPRECATED_IOS(5_0, 9_0);
+MP_EXTERN NSString * const MPMoviePlayerIsAirPlayVideoActiveDidChangeNotification MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(5.0, 9.0, 10.12.1, 10.12.1, 5.0, 9.0);
 
 // Posted when the ready for display state changes.
-MP_EXTERN NSString * const MPMoviePlayerReadyForDisplayDidChangeNotification NS_DEPRECATED_IOS(6_0, 9_0);
+MP_EXTERN NSString * const MPMoviePlayerReadyForDisplayDidChangeNotification MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(6.0, 9.0, 10.12.1, 10.12.1, 6.0, 9.0);
 
 // -----------------------------------------------------------------------------
 // Movie Property Notifications
 
 // Calling -prepareToPlay on the movie player will begin determining movie properties asynchronously.
 // These notifications are posted when the associated movie property becomes available.
-MP_EXTERN NSString * const MPMovieMediaTypesAvailableNotification NS_DEPRECATED_IOS(3_2, 9_0);
-MP_EXTERN NSString * const MPMovieSourceTypeAvailableNotification NS_DEPRECATED_IOS(3_2, 9_0); // Posted if the movieSourceType is MPMovieSourceTypeUnknown when preparing for playback.
-MP_EXTERN NSString * const MPMovieDurationAvailableNotification NS_DEPRECATED_IOS(3_2, 9_0);
-MP_EXTERN NSString * const MPMovieNaturalSizeAvailableNotification NS_DEPRECATED_IOS(3_2, 9_0);
+MP_EXTERN NSString * const MPMovieMediaTypesAvailableNotification MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
+MP_EXTERN NSString * const MPMovieSourceTypeAvailableNotification MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0); // Posted if the movieSourceType is MPMovieSourceTypeUnknown when preparing for playback.
+MP_EXTERN NSString * const MPMovieDurationAvailableNotification MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
+MP_EXTERN NSString * const MPMovieNaturalSizeAvailableNotification MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
 
 // -----------------------------------------------------------------------------
 // Thumbnails
@@ -213,28 +212,28 @@
 typedef NS_ENUM(NSInteger, MPMovieTimeOption) {
     MPMovieTimeOptionNearestKeyFrame,
     MPMovieTimeOptionExact
-} NS_DEPRECATED_IOS(3_2, 9_0) __TVOS_PROHIBITED;
+} MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
 
 @interface MPMoviePlayerController (MPMoviePlayerThumbnailGeneration)
 
 // Returns a thumbnail at the given time.
 // Deprecated.  Use -requestThumbnailImagesAtTimes:timeOption: / MPMoviePlayerThumbnailImageRequestDidFinishNotification instead.
-- (UIImage *)thumbnailImageAtTime:(NSTimeInterval)playbackTime timeOption:(MPMovieTimeOption)option NS_DEPRECATED_IOS(3_2, 7_0);
+- (UIImage *)thumbnailImageAtTime:(NSTimeInterval)playbackTime timeOption:(MPMovieTimeOption)option MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 7.0, 10.12.1, 10.12.1, 3.2, 7.0);
 
 // Asynchronously request thumbnails for one or more times, provided as an array of NSNumbers (double).
 // Posts MPMoviePlayerThumbnailImageRequestDidFinishNotification on completion.
-- (void)requestThumbnailImagesAtTimes:(NSArray *)playbackTimes timeOption:(MPMovieTimeOption)option NS_DEPRECATED_IOS(3_2, 9_0);
+- (void)requestThumbnailImagesAtTimes:(NSArray *)playbackTimes timeOption:(MPMovieTimeOption)option MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
 
 // Cancels all pending asynchronous thumbnail requests.
-- (void)cancelAllThumbnailImageRequests NS_DEPRECATED_IOS(3_2, 9_0);
+- (void)cancelAllThumbnailImageRequests MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
 
 @end
 
 // Posted when each thumbnail image request is completed.
-MP_EXTERN NSString * const MPMoviePlayerThumbnailImageRequestDidFinishNotification NS_DEPRECATED_IOS(3_2, 9_0);
-MP_EXTERN NSString * const MPMoviePlayerThumbnailImageKey NS_DEPRECATED_IOS(3_2, 9_0); // UIImage, may be nil if an error occurred.
-MP_EXTERN NSString * const MPMoviePlayerThumbnailTimeKey NS_DEPRECATED_IOS(3_2, 9_0);  // NSNumber (double)
-MP_EXTERN NSString * const MPMoviePlayerThumbnailErrorKey NS_DEPRECATED_IOS(3_2, 9_0); // NSError
+MP_EXTERN NSString * const MPMoviePlayerThumbnailImageRequestDidFinishNotification MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
+MP_EXTERN NSString * const MPMoviePlayerThumbnailImageKey MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0); // UIImage, may be nil if an error occurred.
+MP_EXTERN NSString * const MPMoviePlayerThumbnailTimeKey MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0); // NSNumber (double)
+MP_EXTERN NSString * const MPMoviePlayerThumbnailErrorKey MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0); // NSError
 
 // -----------------------------------------------------------------------------
 // Timed Metadata
@@ -242,13 +241,11 @@
 @interface MPMoviePlayerController (MPMoviePlayerTimedMetadataAdditions)
 
 // Returns an array of the most recent MPTimedMetadata objects provided by the media stream.
-@property (nonatomic, readonly) NSArray *timedMetadata NS_DEPRECATED_IOS(4_0, 9_0);
+@property (nonatomic, readonly) NSArray *timedMetadata MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(4.0, 9.0, 10.12.1, 10.12.1, 4.0, 9.0);
 
 @end
 
-MP_EXTERN_CLASS_AVAILABLE(4_0)
-NS_DEPRECATED_IOS(4_0, 9_0)
-__TVOS_PROHIBITED
+MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(4.0, 9.0, 10.12.1, 10.12.1, 4.0, 9.0)
 @interface MPTimedMetadata : NSObject
 
 // A key which identifies a piece of timed metadata.
@@ -269,25 +266,25 @@
 @end
 
 // Posted when new timed metadata arrives.
-MP_EXTERN NSString * const MPMoviePlayerTimedMetadataUpdatedNotification NS_DEPRECATED_IOS(4_0, 9_0);
-MP_EXTERN NSString * const MPMoviePlayerTimedMetadataUserInfoKey NS_DEPRECATED_IOS(4_0, 9_0);       // NSDictionary of the most recent MPTimedMetadata objects.
+MP_EXTERN NSString * const MPMoviePlayerTimedMetadataUpdatedNotification MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(4.0, 9.0, 10.12.1, 10.12.1, 4.0, 9.0);
+MP_EXTERN NSString * const MPMoviePlayerTimedMetadataUserInfoKey MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(4.0, 9.0, 10.12.1, 10.12.1, 4.0, 9.0);       // NSDictionary of the most recent MPTimedMetadata objects.
 
 // Additional dictionary keys for use with the 'allMetadata' property. All keys are optional.
-MP_EXTERN NSString * const MPMoviePlayerTimedMetadataKeyName NS_DEPRECATED_IOS(4_0, 9_0);           // NSString
-MP_EXTERN NSString * const MPMoviePlayerTimedMetadataKeyInfo NS_DEPRECATED_IOS(4_0, 9_0);           // NSString
-MP_EXTERN NSString * const MPMoviePlayerTimedMetadataKeyMIMEType NS_DEPRECATED_IOS(4_0, 9_0);       // NSString
-MP_EXTERN NSString * const MPMoviePlayerTimedMetadataKeyDataType NS_DEPRECATED_IOS(4_0, 9_0);       // NSString
-MP_EXTERN NSString * const MPMoviePlayerTimedMetadataKeyLanguageCode NS_DEPRECATED_IOS(4_0, 9_0);   // NSString (ISO 639-2)
+MP_EXTERN NSString * const MPMoviePlayerTimedMetadataKeyName MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(4.0, 9.0, 10.12.1, 10.12.1, 4.0, 9.0);           // NSString
+MP_EXTERN NSString * const MPMoviePlayerTimedMetadataKeyInfo MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(4.0, 9.0, 10.12.1, 10.12.1, 4.0, 9.0);           // NSString
+MP_EXTERN NSString * const MPMoviePlayerTimedMetadataKeyMIMEType MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(4.0, 9.0, 10.12.1, 10.12.1, 4.0, 9.0);       // NSString
+MP_EXTERN NSString * const MPMoviePlayerTimedMetadataKeyDataType MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(4.0, 9.0, 10.12.1, 10.12.1, 4.0, 9.0);       // NSString
+MP_EXTERN NSString * const MPMoviePlayerTimedMetadataKeyLanguageCode MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(4.0, 9.0, 10.12.1, 10.12.1, 4.0, 9.0);   // NSString (ISO 639-2)
 
 // -----------------------------------------------------------------------------
 
 @interface MPMoviePlayerController (MPMovieLogging)
 
 // Returns an object that represents a snapshot of the network access log. Can be nil.
-@property (nonatomic, readonly) MPMovieAccessLog *accessLog NS_DEPRECATED_IOS(4_3, 9_0);
+@property (nonatomic, readonly) MPMovieAccessLog *accessLog MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(4.3, 9.0, 10.12.1, 10.12.1, 4.3, 9.0);
 
 // Returns an object that represents a snapshot of the error log. Can be nil.
-@property (nonatomic, readonly) MPMovieErrorLog *errorLog NS_DEPRECATED_IOS(4_3, 9_0);
+@property (nonatomic, readonly) MPMovieErrorLog *errorLog MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(4.3, 9.0, 10.12.1, 10.12.1, 4.3, 9.0);
 
 @end
 
@@ -295,9 +292,7 @@
 // An MPMovieAccessLog accumulates key metrics about network playback and presents them as a collection of MPMovieAccessLogEvent instances.
 // Each MPMovieAccessLogEvent instance collates the data that relates to each uninterrupted period of playback.
 
-MP_EXTERN_CLASS_AVAILABLE(4_3)
-NS_DEPRECATED_IOS(4_3, 9_0)
-__TVOS_PROHIBITED
+MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(4.3, 9.0, 10.12.1, 10.12.1, 4.3, 9.0)
 @interface MPMovieAccessLog : NSObject <NSCopying>
 
 // Returns the webserver access log into a textual format that conforms to the W3C Extended Log File Format for web server log files.
@@ -315,9 +310,7 @@
 // -----------------------------------------------------------------------------
 // An MPMovieErrorLog provides data to identify if, and when, network resource playback failures occured.
 
-MP_EXTERN_CLASS_AVAILABLE(4_3)
-NS_DEPRECATED_IOS(4_3, 9_0)
-__TVOS_PROHIBITED
+MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(4.3, 9.0, 10.12.1, 10.12.1, 4.3, 9.0)
 @interface MPMovieErrorLog : NSObject <NSCopying>
 
 // Returns the webserver error log into a textual format that conforms to the W3C Extended Log File Format for web server log files.
@@ -335,9 +328,7 @@
 // -----------------------------------------------------------------------------
 // An MPMovieAccessLogEvent repesents a single access log entry.
 
-MP_EXTERN_CLASS_AVAILABLE(4_3)
-NS_DEPRECATED_IOS(4_3, 9_0)
-__TVOS_PROHIBITED
+MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(4.3, 9.0, 10.12.1, 10.12.1, 4.3, 9.0)
 @interface MPMovieAccessLogEvent : NSObject <NSCopying>
 
 // A count of media segments downloaded from the server to this client.
@@ -387,9 +378,7 @@
 // -----------------------------------------------------------------------------
 // An MPMovieErrorLogEvent repesents a single error log entry.
 
-MP_EXTERN_CLASS_AVAILABLE(4_3)
-NS_DEPRECATED_IOS(4_3, 9_0)
-__TVOS_PROHIBITED
+MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(4.3, 9.0, 10.12.1, 10.12.1, 4.3, 9.0)
 @interface MPMovieErrorLogEvent : NSObject <NSCopying>
 
 // The date and time when the error occured.
@@ -423,6 +412,6 @@
 
 // Indicates if the movie player should inherit the application's audio session instead of creating a new session (which would interrupt the application's session).
 // Defaults to YES. Setting this property during playback will not take effect until playback is stopped and started again.
-@property (nonatomic) BOOL useApplicationAudioSession NS_DEPRECATED_IOS(3_2, 6_0);
+@property (nonatomic) BOOL useApplicationAudioSession MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(3.2, 6.0, 10.12.1, 10.12.1, 3.2, 6.0);
 
 @end
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMoviePlayerViewController.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMoviePlayerViewController.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMoviePlayerViewController.h	2016-08-11 06:42:45.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMoviePlayerViewController.h	2016-10-24 06:54:13.000000000 +0200
@@ -11,9 +11,7 @@
 
 @class MPMoviePlayerController;
 
-MP_EXTERN_CLASS_AVAILABLE(3_2)
-NS_DEPRECATED_IOS(3_2, 9_0, "Use AVPlayerViewController in AVKit.")
-__TVOS_PROHIBITED
+MP_API_IOS_DEPRECATED_WITH_REPLACEMENT_MACOS_TVOS_PROHIBITED("Use AVPlayerViewController in AVKit.", 3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0)
 @interface MPMoviePlayerViewController : UIViewController
 
 - (instancetype)initWithContentURL:(NSURL *)contentURL NS_DESIGNATED_INITIALIZER;
@@ -28,7 +26,7 @@
 
 @interface UIViewController (MPMoviePlayerViewController)
 
-- (void)presentMoviePlayerViewControllerAnimated:(MPMoviePlayerViewController *)moviePlayerViewController NS_DEPRECATED_IOS(3_2, 9_0, "Use AVPlayerViewController in AVKit.") __TVOS_PROHIBITED;
-- (void)dismissMoviePlayerViewControllerAnimated NS_DEPRECATED_IOS(3_2, 9_0, "Use AVPlayerViewController in AVKit.") __TVOS_PROHIBITED;
+- (void)presentMoviePlayerViewControllerAnimated:(MPMoviePlayerViewController *)moviePlayerViewController MP_API_IOS_DEPRECATED_WITH_REPLACEMENT_MACOS_TVOS_PROHIBITED("Use AVPlayerViewController in AVKit.", 3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
+- (void)dismissMoviePlayerViewControllerAnimated MP_API_IOS_DEPRECATED_WITH_REPLACEMENT_MACOS_TVOS_PROHIBITED("Use AVPlayerViewController in AVKit.", 3.2, 9.0, 10.12.1, 10.12.1, 3.2, 9.0);
 
 @end
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMusicPlayerController.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMusicPlayerController.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMusicPlayerController.h	2016-05-04 00:21:21.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMusicPlayerController.h	2016-10-24 06:38:13.000000000 +0200
@@ -11,11 +11,10 @@
 #import <MediaPlayer/MPMediaItem.h>
 #import <MediaPlayer/MPMediaQuery.h>
 #import <MediaPlayer/MPMediaPlayback.h>
+#import <MediaPlayer/MPMusicPlayerQueueDescriptor.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
-@class MPMediaItem, MPMediaQuery, MPMusicPlayerControllerInternal;
-
 typedef NS_ENUM(NSInteger, MPMusicPlaybackState) {
     MPMusicPlaybackStateStopped,
     MPMusicPlaybackStatePlaying,
@@ -23,25 +22,24 @@
     MPMusicPlaybackStateInterrupted,
     MPMusicPlaybackStateSeekingForward,
     MPMusicPlaybackStateSeekingBackward
-} __TVOS_PROHIBITED;
+} MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(3.0, 10.12.1, 3.0);
 
 typedef NS_ENUM(NSInteger, MPMusicRepeatMode) {
     MPMusicRepeatModeDefault, // the user's preference for repeat mode
     MPMusicRepeatModeNone,
     MPMusicRepeatModeOne,
     MPMusicRepeatModeAll
-} __TVOS_PROHIBITED;
+} MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(3.0, 10.12.1, 3.0);
 
 typedef NS_ENUM(NSInteger, MPMusicShuffleMode) {
     MPMusicShuffleModeDefault, // the user's preference for shuffle mode
     MPMusicShuffleModeOff,
     MPMusicShuffleModeSongs,
     MPMusicShuffleModeAlbums
-} __TVOS_PROHIBITED;
+} MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(3.0, 10.12.1, 3.0);
 
 // MPMusicPlayerController allows playback of MPMediaItems through the Music application.
-MP_EXTERN_CLASS_AVAILABLE(3_0)
-__TVOS_PROHIBITED
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(3.0, 10.12.1, 3.0)
 @interface MPMusicPlayerController : NSObject <MPMediaPlayback>
 
 /// Playing media items with the applicationMusicPlayer will restore the user's Music state after the application quits.
@@ -83,6 +81,13 @@
 - (void)setQueueWithQuery:(MPMediaQuery *)query;
 - (void)setQueueWithItemCollection:(MPMediaItemCollection *)itemCollection;
 - (void)setQueueWithStoreIDs:(NSArray<NSString *> *)storeIDs NS_AVAILABLE_IOS(9_3);
+- (void)setQueueWithDescriptor:(MPMusicPlayerQueueDescriptor *)descriptor NS_AVAILABLE_IOS(10_1);
+
+// The completion handler will be called when the first item from the queue is buffered and ready to play.
+// If a first item has been specified using MPMusicPlayerQueueDescriptor, the error will be non-nil if the specified item cannot be prepared for playback.
+// If a first item is not specified, the error will be non-nil if an item cannot be prepared for playback.
+// Errors will be in MPErrorDomain.
+- (void)prepareToPlayWithCompletionHandler:(void (^)(NSError *_Nullable error))completionHandler NS_AVAILABLE_IOS(10_1);
 
 // Skips to the next item in the queue. If already at the last item, this will end playback.
 - (void)skipToNextItem;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMusicPlayerQueueDescriptor.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMusicPlayerQueueDescriptor.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMusicPlayerQueueDescriptor.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMusicPlayerQueueDescriptor.h	2016-10-24 06:54:13.000000000 +0200
@@ -0,0 +1,48 @@
+//
+//  MPMusicPlayerQueueDescriptor.h
+//  MediaPlayerFramework
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <MediaPlayer/MediaPlayerDefines.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class MPMediaItem, MPMediaItemCollection, MPMediaQuery;
+
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(10.1, 10.12.1, 10.1)
+@interface MPMusicPlayerQueueDescriptor : NSObject<NSSecureCoding>
+
+@end
+
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(10.1, 10.12.1, 10.1)
+@interface MPMusicPlayerMediaItemQueueDescriptor : MPMusicPlayerQueueDescriptor
+
+- (instancetype)initWithQuery:(MPMediaQuery *)query;
+- (instancetype)initWithItemCollection:(MPMediaItemCollection *)itemCollection;
+
+@property (nonatomic, copy, readonly) MPMediaQuery *query;
+@property (nonatomic, strong, readonly) MPMediaItemCollection *itemCollection;
+@property (nonatomic, strong, nullable) MPMediaItem *startItem;
+
+- (void)setStartTime:(NSTimeInterval)startTime forItem:(MPMediaItem *)mediaItem;
+- (void)setEndTime:(NSTimeInterval)endTime forItem:(MPMediaItem *)mediaItem;
+
+@end
+
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(10.1, 10.12.1, 10.1)
+@interface MPMusicPlayerStoreQueueDescriptor : MPMusicPlayerQueueDescriptor
+
+- (instancetype)initWithStoreIDs:(NSArray<NSString *> *)storeIDs;
+
+@property (nonatomic, copy, nullable) NSArray<NSString *> *storeIDs;
+@property (nonatomic, copy, nullable) NSString *startItemID;
+
+- (void)setStartTime:(NSTimeInterval)startTime forItemWithStoreID:(NSString *)storeID;
+- (void)setEndTime:(NSTimeInterval)endTime forItemWithStoreID:(NSString *)storeID;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPNowPlayingInfoCenter.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPNowPlayingInfoCenter.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPNowPlayingInfoCenter.h	2016-08-05 08:27:48.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPNowPlayingInfoCenter.h	2016-10-24 05:31:45.000000000 +0200
@@ -39,19 +39,34 @@
     MPNowPlayingInfoMediaTypeNone = 0,
     MPNowPlayingInfoMediaTypeAudio,
     MPNowPlayingInfoMediaTypeVideo,
-} NS_AVAILABLE_IOS(10_0);
+} NS_AVAILABLE(10_12_1, 10_0);
 
-MP_EXTERN_CLASS_AVAILABLE(5_0)
+typedef NS_ENUM(NSUInteger, MPNowPlayingPlaybackState) {
+    MPNowPlayingPlaybackStateUnknown = 0,
+    MPNowPlayingPlaybackStatePlaying,
+    MPNowPlayingPlaybackStatePaused,
+    MPNowPlayingPlaybackStateStopped,
+    MPNowPlayingPlaybackStateInterrupted
+} NS_AVAILABLE_MAC(10_12_1);
+
+MP_API(ios(5.0), tvos(5.0), macos(10.12.1))
 @interface MPNowPlayingInfoCenter : NSObject
 
-// Returns the default now playing info center.
-// The default center holds now playing info about the current application.
+/// Returns the default now playing info center.
+/// The default center holds now playing info about the current application.
 + (MPNowPlayingInfoCenter *)defaultCenter;
 
-// The current now playing info for the center.
-// Setting the info to nil will clear it.
+/// The current now playing info for the center.
+/// Setting the info to nil will clear it.
 @property (copy, nullable) NSDictionary<NSString *, id> *nowPlayingInfo;
 
+/// The current playback state of the app.
+/// This only applies on macOS, where playback state cannot be determined by
+/// the application's audio session. This property must be set every time
+/// the app begins or halts playback, otherwise remote control functionality may
+/// not work as expected.
+@property (assign) MPNowPlayingPlaybackState playbackState NS_AVAILABLE_MAC(10_12_1);
+
 @end
 
 // -----------------------------------------------------------------------------
@@ -61,12 +76,12 @@
 // Note the elapsed time will be automatically extrapolated from the previously 
 // provided elapsed time and playback rate, so updating this property frequently
 // is not required (or recommended.)
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyElapsedPlaybackTime NS_AVAILABLE_IOS(5_0); // NSNumber (double)
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyElapsedPlaybackTime NS_AVAILABLE(10_12_1, 5_0); // NSNumber (double)
 
 // The playback rate of the now playing item, with 1.0 representing normal 
 // playback. For example, 2.0 would represent playback at twice the normal rate.
 // If not specified, assumed to be 1.0.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyPlaybackRate NS_AVAILABLE_IOS(5_0); // NSNumber (double)
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyPlaybackRate NS_AVAILABLE(10_12_1, 5_0); // NSNumber (double)
 
 // The "default" playback rate of the now playing item. You should set this
 // property if your app is playing a media item at a rate other than 1.0 in a
@@ -75,47 +90,47 @@
 // playback rate should also be 2.0. Conversely, if you are playing back content
 // at a normal rate (1.0) but the user is fast-forwarding your content at a rate
 // greater than 1.0, then the default playback rate should be set to 1.0.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyDefaultPlaybackRate NS_AVAILABLE_IOS(8_0); // NSNumber (double)
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyDefaultPlaybackRate NS_AVAILABLE(10_12_1, 8_0); // NSNumber (double)
 
 // The index of the now playing item in the application's playback queue.
 // Note that the queue uses zero-based indexing, so the index of the first item 
 // would be 0 if the item should be displayed as "item 1 of 10".
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyPlaybackQueueIndex NS_AVAILABLE_IOS(5_0); // NSNumber (NSUInteger)
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyPlaybackQueueIndex NS_AVAILABLE(10_12_1, 5_0); // NSNumber (NSUInteger)
 
 // The total number of items in the application's playback queue.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyPlaybackQueueCount NS_AVAILABLE_IOS(5_0); // NSNumber (NSUInteger)
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyPlaybackQueueCount NS_AVAILABLE(10_12_1, 5_0); // NSNumber (NSUInteger)
 
 // The chapter currently being played. Note that this is zero-based.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyChapterNumber NS_AVAILABLE_IOS(5_0); // NSNumber (NSUInteger)
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyChapterNumber NS_AVAILABLE(10_12_1, 5_0); // NSNumber (NSUInteger)
 
 // The total number of chapters in the now playing item.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyChapterCount NS_AVAILABLE_IOS(5_0); // NSNumber (NSUInteger)
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyChapterCount NS_AVAILABLE(10_12_1, 5_0); // NSNumber (NSUInteger)
 
 // A boolean denoting whether the now playing item is a live stream.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyIsLiveStream NS_AVAILABLE_IOS(10_0); // NSNumber (BOOL)
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyIsLiveStream NS_AVAILABLE(10_12_1, 10_0); // NSNumber (BOOL)
 
 // A list of available language option groups in the now playing item
 // Only one language option in a given group can be played at once.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyAvailableLanguageOptions NS_AVAILABLE_IOS(9_0); // NSArrayRef of MPNowPlayingInfoLanguageOptionGroup
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyAvailableLanguageOptions NS_AVAILABLE(10_12_1, 9_0); // NSArrayRef of MPNowPlayingInfoLanguageOptionGroup
 
 // A list of currently active language options in the now playing item.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyCurrentLanguageOptions NS_AVAILABLE_IOS(9_0); // NSArray of MPNowPlayingInfoLanguageOption
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyCurrentLanguageOptions NS_AVAILABLE(10_12_1, 9_0); // NSArray of MPNowPlayingInfoLanguageOption
 
 // An identifier that represents the collection to which the now playing item belongs.
 // This can refer to an artist, album, playlist, etc.
 // This can be used to ask the now playing app to resume playback of the collection.
-MP_EXTERN NSString *const MPNowPlayingInfoCollectionIdentifier NS_AVAILABLE_IOS(9_3); // NSString
+MP_EXTERN NSString *const MPNowPlayingInfoCollectionIdentifier NS_AVAILABLE(10_12_1, 9_3); // NSString
 
 // An opaque identifier that uniquely represents the now playing item,
 // even across app relaunches. This can be in any format and is only used to
 // reference this item back to the now playing app.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyExternalContentIdentifier NS_AVAILABLE_IOS(10_0); // NSString
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyExternalContentIdentifier NS_AVAILABLE(10_12_1, 10_0); // NSString
 
 // An optional opaque identifier that uniquely represents the profile that the
 // now playing item is being played from, even across app relauches.
 // This can be in any format and is only used to reference this profile back to
 // the now playing app.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyExternalUserProfileIdentifier NS_AVAILABLE_IOS(10_0); // NSString
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyExternalUserProfileIdentifier NS_AVAILABLE(10_12_1, 10_0); // NSString
 
 // Represents the current playback progress of the now playing item.
 // 0.0 = not watched/listened/viewed, 1.0 = fully watched/listened/viewed
@@ -123,11 +138,10 @@
 // as it is used as a high level indicator as to how far along the user is.
 // For example, a movie may wish to set the now playing item as fully watched
 // when the credits begin to roll.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyPlaybackProgress NS_AVAILABLE_IOS(10_0); // NSNumber (float)
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyPlaybackProgress NS_AVAILABLE(10_12_1, 10_0); // NSNumber (float)
 
 // Indicates the media type of the now playing item
 // This can be used to determine what kind of user interface the system displays.
-MP_EXTERN NSString *const MPNowPlayingInfoPropertyMediaType NS_AVAILABLE_IOS(10_0); // NSNumber (MPNowPlayingInfoMediaType)
-
+MP_EXTERN NSString *const MPNowPlayingInfoPropertyMediaType NS_AVAILABLE(10_12_1, 10_0); // NSNumber (MPNowPlayingInfoMediaType)
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPNowPlayingInfoLanguageOption.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPNowPlayingInfoLanguageOption.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPNowPlayingInfoLanguageOption.h	2016-05-04 00:21:26.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPNowPlayingInfoLanguageOption.h	2016-10-24 06:54:13.000000000 +0200
@@ -22,26 +22,26 @@
 // Common values used to to populate MPNowPlayingInfoLanguageOption's
 // characteristics property.
 // See the AVMediaSelectionOption documentation about Media Characteristics for more details.
-MP_EXTERN NSString *const MPLanguageOptionCharacteristicIsMainProgramContent NS_AVAILABLE_IOS(9_0);
-MP_EXTERN NSString *const MPLanguageOptionCharacteristicIsAuxiliaryContent NS_AVAILABLE_IOS(9_0);
-MP_EXTERN NSString *const MPLanguageOptionCharacteristicContainsOnlyForcedSubtitles NS_AVAILABLE_IOS(9_0);
-MP_EXTERN NSString *const MPLanguageOptionCharacteristicTranscribesSpokenDialog NS_AVAILABLE_IOS(9_0);
-MP_EXTERN NSString *const MPLanguageOptionCharacteristicDescribesMusicAndSound NS_AVAILABLE_IOS(9_0);
-MP_EXTERN NSString *const MPLanguageOptionCharacteristicEasyToRead NS_AVAILABLE_IOS(9_0);
-MP_EXTERN NSString *const MPLanguageOptionCharacteristicDescribesVideo NS_AVAILABLE_IOS(9_0);
-MP_EXTERN NSString *const MPLanguageOptionCharacteristicLanguageTranslation NS_AVAILABLE_IOS(9_0);
-MP_EXTERN NSString *const MPLanguageOptionCharacteristicDubbedTranslation NS_AVAILABLE_IOS(9_0);
-MP_EXTERN NSString *const MPLanguageOptionCharacteristicVoiceOverTranslation NS_AVAILABLE_IOS(9_0);
+MP_EXTERN NSString *const MPLanguageOptionCharacteristicIsMainProgramContent NS_AVAILABLE(10_12_1, 9_0);
+MP_EXTERN NSString *const MPLanguageOptionCharacteristicIsAuxiliaryContent NS_AVAILABLE(10_12_1, 9_0);
+MP_EXTERN NSString *const MPLanguageOptionCharacteristicContainsOnlyForcedSubtitles NS_AVAILABLE(10_12_1, 9_0);
+MP_EXTERN NSString *const MPLanguageOptionCharacteristicTranscribesSpokenDialog NS_AVAILABLE(10_12_1, 9_0);
+MP_EXTERN NSString *const MPLanguageOptionCharacteristicDescribesMusicAndSound NS_AVAILABLE(10_12_1, 9_0);
+MP_EXTERN NSString *const MPLanguageOptionCharacteristicEasyToRead NS_AVAILABLE(10_12_1, 9_0);
+MP_EXTERN NSString *const MPLanguageOptionCharacteristicDescribesVideo NS_AVAILABLE(10_12_1, 9_0);
+MP_EXTERN NSString *const MPLanguageOptionCharacteristicLanguageTranslation NS_AVAILABLE(10_12_1, 9_0);
+MP_EXTERN NSString *const MPLanguageOptionCharacteristicDubbedTranslation NS_AVAILABLE(10_12_1, 9_0);
+MP_EXTERN NSString *const MPLanguageOptionCharacteristicVoiceOverTranslation NS_AVAILABLE(10_12_1, 9_0);
 
 typedef NS_ENUM(NSUInteger, MPNowPlayingInfoLanguageOptionType) {
     MPNowPlayingInfoLanguageOptionTypeAudible,
     MPNowPlayingInfoLanguageOptionTypeLegible,
-} NS_ENUM_AVAILABLE_IOS(9_0);
+} NS_ENUM_AVAILABLE(10_12_1, 9_0);
 
 // -----------------------------------------------------------------------------
 
 /// Represents a single language option option.
-MP_EXTERN_CLASS_AVAILABLE(9_0)
+MP_API(ios(9.0), tvos(9.0), macos(10.12.1))
 @interface MPNowPlayingInfoLanguageOption : NSObject
 
 - (instancetype)initWithType:(MPNowPlayingInfoLanguageOptionType)languageOptionType
@@ -86,7 +86,7 @@
 
 // Represents a mutually exclusive group of language options.
 // Only one language option within a given group may be active at a time.
-MP_EXTERN_CLASS_AVAILABLE(9_0)
+MP_API(ios(9.0), tvos(9.0), macos(10.12.1))
 @interface MPNowPlayingInfoLanguageOptionGroup : NSObject
 
 - (instancetype)initWithLanguageOptions:(NSArray<MPNowPlayingInfoLanguageOption *> *)languageOptions
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentDataSource.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentDataSource.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentDataSource.h	2016-08-11 06:42:45.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentDataSource.h	2016-10-24 06:54:13.000000000 +0200
@@ -17,7 +17,7 @@
 /// Data sources are responsible for providing metadata about your media to these
 /// systems in a meaningful way, so that features like user interfaces and play
 /// queues can be setup automatically.
-__TVOS_PROHIBITED
+MP_API_IOS_AVAILABLE_TVOS_PROHIBITED(7.1, 10.12.1, 7.1)
 @protocol MPPlayableContentDataSource <NSObject>
 @optional
 
@@ -41,7 +41,7 @@
 /// to be retrieved.
 /// Client applications should always call the completion handler after loading
 /// has finished, if this method is implemented.
-- (void)contentItemForIdentifier:(NSString *)identifier completionHandler:(void(^)(MPContentItem *__nullable, NSError * __nullable))completionHandler NS_AVAILABLE_IOS(10_0);
+- (void)contentItemForIdentifier:(NSString *)identifier completionHandler:(void(^)(MPContentItem *__nullable, NSError * __nullable))completionHandler MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(10.0, 10.12.1, 10.0);
 
 @required
 /// Returns the number of child nodes at the specified index path. In a virtual
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentDelegate.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentDelegate.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentDelegate.h	2016-08-11 06:42:45.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentDelegate.h	2016-10-24 06:54:13.000000000 +0200
@@ -6,6 +6,7 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <MediaPlayer/MediaPlayerDefines.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -17,14 +18,14 @@
 /// MPPlayableContentDataSource) and selects a content item to play. If the media
 /// player decides that it wants to play the item, it will ask the application's
 /// content delegate to initiate playback.
-__TVOS_PROHIBITED
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(7.1, 10.12.1, 7.1)
 @protocol MPPlayableContentDelegate <NSObject>
 @optional
 
 /// This method is called when a media player interface wants to play a requested
 /// content item. The application should call the completion handler with an
 /// appropriate error if there was an error beginning playback for the item.
-- (void)playableContentManager:(MPPlayableContentManager *)contentManager initiatePlaybackOfContentItemAtIndexPath:(NSIndexPath *)indexPath completionHandler:(void(^)(NSError * __nullable))completionHandler NS_AVAILABLE_IOS(7_1);
+- (void)playableContentManager:(MPPlayableContentManager *)contentManager initiatePlaybackOfContentItemAtIndexPath:(NSIndexPath *)indexPath completionHandler:(void(^)(NSError * __nullable))completionHandler MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(7.1, 10.12.1, 7.1);
 
 
 /// This method is called when a media player interface wants the now playing
@@ -44,10 +45,10 @@
 /// anything it deems appropriate.
 /// The app should call the provided completion handler once it is ready to play
 /// something.
-- (void)playableContentManager:(MPPlayableContentManager *)contentManager initializePlaybackQueueWithContentItems:(nullable NSArray *)contentItems completionHandler:(void(^)(NSError * __nullable))completionHandler NS_AVAILABLE_IOS(9_3);
+- (void)playableContentManager:(MPPlayableContentManager *)contentManager initializePlaybackQueueWithContentItems:(nullable NSArray *)contentItems completionHandler:(void(^)(NSError * __nullable))completionHandler MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(9.3, 10.12.1, 9.3);
 
 /// This method is called when the content server notifies the manager that the current context has changed.
-- (void)playableContentManager:(MPPlayableContentManager *)contentManager didUpdateContext:(MPPlayableContentManagerContext *)context NS_AVAILABLE_IOS(8_4);
+- (void)playableContentManager:(MPPlayableContentManager *)contentManager didUpdateContext:(MPPlayableContentManagerContext *)context MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(8.4, 10.12.1, 8.4);
 
 @end
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentManager.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentManager.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentManager.h	2016-08-11 06:42:45.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentManager.h	2016-10-24 06:54:13.000000000 +0200
@@ -17,8 +17,7 @@
 /// provides the content manager with a data source, which allows the media player
 /// to browse the media content offered by the application, as well as a delegate,
 /// which allows the media player to relay non-media remote playback commands to the application.
-MP_EXTERN_CLASS_AVAILABLE(7_1)
-__TVOS_PROHIBITED
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(7.1, 10.12.1, 7.1)
 @interface MPPlayableContentManager : NSObject
 
 @property (nonatomic, weak, nullable) id<MPPlayableContentDataSource> dataSource;
@@ -26,7 +25,7 @@
 @property (nonatomic, readonly) MPPlayableContentManagerContext *context NS_AVAILABLE_IOS(8_4);
 
 /// Tells the content manager which MPBrowsableContentItems are currently playing based on their identifiers.
-@property (nonatomic, strong) NSArray<NSString *> *nowPlayingIdentifiers NS_AVAILABLE_IOS(10_0);
+@property (nonatomic, strong) NSArray<NSString *> *nowPlayingIdentifiers NS_AVAILABLE(10_12_1, 10_0);
 
 /// Returns the application's instance of the content manager.
 + (instancetype)sharedContentManager;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentManagerContext.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentManagerContext.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentManagerContext.h	2016-08-11 06:42:45.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPPlayableContentManagerContext.h	2016-10-24 06:54:13.000000000 +0200
@@ -8,12 +8,10 @@
 #import <Foundation/Foundation.h>
 #import <MediaPlayer/MediaPlayerDefines.h>
 
-
 /// MPPlayableContentManagerContext represents the current state of
 /// the playable content endpoint. A context is retrievable from an instance
 /// of MPPlayableContentManager.
-MP_EXTERN_CLASS_AVAILABLE(8_4)
-__TVOS_PROHIBITED
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(8.4, 10.12.1, 8.4)
 @interface MPPlayableContentManagerContext : NSObject
 
 /// The number of items the content server will display when content limiting is enforced.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommand.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommand.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommand.h	2016-08-11 06:42:45.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommand.h	2016-10-24 05:31:45.000000000 +0200
@@ -25,13 +25,13 @@
     /// available that is required for this command. As an example, an
     /// application would return this error code if an "enable language option"
     /// command is received, but nothing is currently playing.
-    MPRemoteCommandHandlerStatusNoActionableNowPlayingItem NS_ENUM_AVAILABLE_IOS(9_1) = 110,
+    MPRemoteCommandHandlerStatusNoActionableNowPlayingItem NS_ENUM_AVAILABLE(10_12_1, 9_1) = 110,
     
     /// The command could not be executed for another reason.
     MPRemoteCommandHandlerStatusCommandFailed = 200
-} NS_ENUM_AVAILABLE_IOS(7_1);
+} NS_ENUM_AVAILABLE(10_12_1, 7_1);
 
-MP_EXTERN_CLASS_AVAILABLE(7_1)
+MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
 @interface MPRemoteCommand : NSObject
 
 /// Whether a button (for example) should be enabled and tappable for this
@@ -59,7 +59,7 @@
 
 @end
 
-MP_EXTERN_CLASS_AVAILABLE(7_1)
+MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
 @interface MPSkipIntervalCommand : MPRemoteCommand
 
 /// An array of NSNumbers (NSTimeIntervals) that contain preferred skip intervals.
@@ -67,7 +67,7 @@
 
 @end
 
-MP_EXTERN_CLASS_AVAILABLE(7_1)
+MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
 @interface MPFeedbackCommand : MPRemoteCommand
 
 /// Whether the feedback command is in an "active" state. An example of when a
@@ -85,7 +85,7 @@
 
 @end
 
-MP_EXTERN_CLASS_AVAILABLE(7_1)
+MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
 @interface MPRatingCommand : MPRemoteCommand
 
 /// Minimum rating for the command.
@@ -96,7 +96,7 @@
 
 @end
 
-MP_EXTERN_CLASS_AVAILABLE(7_1)
+MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
 @interface MPChangePlaybackRateCommand : MPRemoteCommand
 
 /// An array of NSNumbers (floats) that contain supported playback rates that
@@ -107,7 +107,7 @@
 
 /// Command for changing the current playback position in a now playing item.
 /// Sends out MPChangePlaybackPositionCommandEvents.
-MP_EXTERN_CLASS_AVAILABLE(9_0)
+MP_API(ios(9.0), tvos(9.0), macos(10.12.1))
 @interface MPChangePlaybackPositionCommand : MPRemoteCommand
 
 @end
@@ -116,7 +116,7 @@
 /// update the system's current representation of your app's shuffle mode, set
 /// the currentShuffleType property on this command to the proper shuffle type
 /// value.
-MP_EXTERN_CLASS_AVAILABLE(8_0)
+MP_API(ios(8.0), tvos(8.0), macos(10.12.1))
 @interface MPChangeShuffleModeCommand : MPRemoteCommand
 
 @property (nonatomic, assign) MPShuffleType currentShuffleType;
@@ -127,7 +127,7 @@
 /// update the system's current representation of your app's repeat mode, set
 /// the currentRepeatType property on this command to the proper repeat type
 /// value.
-MP_EXTERN_CLASS_AVAILABLE(8_0)
+MP_API(ios(8.0), tvos(8.0), macos(10.12.1))
 @interface MPChangeRepeatModeCommand : MPRemoteCommand
 
 @property (nonatomic, assign) MPRepeatType currentRepeatType;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandCenter.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandCenter.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandCenter.h	2016-08-11 06:42:45.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandCenter.h	2016-10-24 06:54:14.000000000 +0200
@@ -19,7 +19,7 @@
 @class MPRemoteCommand;
 @class MPSkipIntervalCommand;
 
-MP_EXTERN_CLASS_AVAILABLE(7_1)
+MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
 @interface MPRemoteCommandCenter : NSObject
 
 // Playback Commands
@@ -27,8 +27,8 @@
 @property (nonatomic, readonly) MPRemoteCommand *playCommand;
 @property (nonatomic, readonly) MPRemoteCommand *stopCommand;
 @property (nonatomic, readonly) MPRemoteCommand *togglePlayPauseCommand;
-@property (nonatomic, readonly) MPRemoteCommand *enableLanguageOptionCommand NS_AVAILABLE_IOS(9_0);
-@property (nonatomic, readonly) MPRemoteCommand *disableLanguageOptionCommand NS_AVAILABLE_IOS(9_0);
+@property (nonatomic, readonly) MPRemoteCommand *enableLanguageOptionCommand NS_AVAILABLE(10_12_1, 9_0);
+@property (nonatomic, readonly) MPRemoteCommand *disableLanguageOptionCommand NS_AVAILABLE(10_12_1, 9_0);
 @property (nonatomic, readonly) MPChangePlaybackRateCommand *changePlaybackRateCommand;
 @property (nonatomic, readonly) MPChangeRepeatModeCommand *changeRepeatModeCommand;
 @property (nonatomic, readonly) MPChangeShuffleModeCommand *changeShuffleModeCommand;
@@ -44,7 +44,7 @@
 // Seek Commands
 @property (nonatomic, readonly) MPRemoteCommand *seekForwardCommand;
 @property (nonatomic, readonly) MPRemoteCommand *seekBackwardCommand;
-@property (nonatomic, readonly) MPChangePlaybackPositionCommand *changePlaybackPositionCommand NS_AVAILABLE_IOS(9_1);
+@property (nonatomic, readonly) MPChangePlaybackPositionCommand *changePlaybackPositionCommand NS_AVAILABLE(10_12_1, 9_1);
 
 // Rating Command
 @property (nonatomic, readonly) MPRatingCommand *ratingCommand;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandEvent.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandEvent.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandEvent.h	2016-09-30 07:27:06.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteCommandEvent.h	2016-10-24 06:38:13.000000000 +0200
@@ -14,7 +14,7 @@
 
 @class MPRemoteCommand;
 
-MP_EXTERN_CLASS_AVAILABLE(7_1)
+MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
 @interface MPRemoteCommandEvent : NSObject
 
 /// The command that sent the event.
@@ -25,7 +25,7 @@
 
 @end
 
-MP_EXTERN_CLASS_AVAILABLE(7_1)
+MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
 @interface MPSkipIntervalCommandEvent : MPRemoteCommandEvent
 
 /// The chosen interval for this skip command event.
@@ -36,9 +36,9 @@
 typedef NS_ENUM(NSUInteger, MPSeekCommandEventType) {
     MPSeekCommandEventTypeBeginSeeking,
     MPSeekCommandEventTypeEndSeeking
-} NS_ENUM_AVAILABLE_IOS(7_1);
+} NS_ENUM_AVAILABLE(10_12_1, 7_1);
 
-MP_EXTERN_CLASS_AVAILABLE(7_1)
+MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
 @interface MPSeekCommandEvent : MPRemoteCommandEvent
 
 /// The type of seek command event, which specifies whether an external player
@@ -47,7 +47,7 @@
 
 @end
 
-MP_EXTERN_CLASS_AVAILABLE(7_1)
+MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
 @interface MPRatingCommandEvent : MPRemoteCommandEvent
 
 /// The chosen rating for this command event. This value will be within the
@@ -56,7 +56,7 @@
 
 @end
 
-MP_EXTERN_CLASS_AVAILABLE(7_1)
+MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
 @interface MPChangePlaybackRateCommandEvent : MPRemoteCommandEvent
 
 /// The chosen playback rate for this command event. This value will be equal
@@ -66,7 +66,7 @@
 
 @end
 
-MP_EXTERN_CLASS_AVAILABLE(7_1)
+MP_API(ios(7.1), tvos(7.1), macos(10.12.1))
 @interface MPFeedbackCommandEvent : MPRemoteCommandEvent
 
 /// Whether the command event is a negative operation. For example, the command
@@ -82,7 +82,7 @@
 
 @end
 
-MP_EXTERN_CLASS_AVAILABLE(9_0)
+MP_API(ios(9.0), tvos(9.0), macos(10.12.1))
 @interface MPChangeLanguageOptionCommandEvent : MPRemoteCommandEvent
 
 /// The requested language option to change.
@@ -96,7 +96,7 @@
 
 @end
 
-MP_EXTERN_CLASS_AVAILABLE(8_0)
+MP_API(ios(8.0), tvos(8.0), macos(10.12.1))
 @interface MPChangePlaybackPositionCommandEvent : MPRemoteCommandEvent
 
 /// The desired playback position to use when setting the current time of the player.
@@ -104,7 +104,7 @@
 
 @end
 
-MP_EXTERN_CLASS_AVAILABLE(8_0)
+MP_API(ios(8.0), tvos(8.0), macos(10.12.1))
 @interface MPChangeShuffleModeCommandEvent : MPRemoteCommandEvent
 
 /// The desired shuffle type to use when fulfilling the request.
@@ -115,7 +115,7 @@
 
 @end
 
-MP_EXTERN_CLASS_AVAILABLE(8_0)
+MP_API(ios(8.0), tvos(8.0), macos(10.12.1))
 @interface MPChangeRepeatModeCommandEvent : MPRemoteCommandEvent
 
 /// The desired repeat type to use when fulfilling the request.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteControlTypes.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteControlTypes.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteControlTypes.h	2016-08-11 06:42:45.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPRemoteControlTypes.h	2016-10-24 06:54:13.000000000 +0200
@@ -12,16 +12,16 @@
     MPShuffleTypeOff,           /// Nothing is shuffled during playback.
     MPShuffleTypeItems,         /// Individual items are shuffled during playback.
     MPShuffleTypeCollections,   /// Collections (e.g. albums) are shuffled during playback.
-} NS_ENUM_AVAILABLE_IOS(3_0);
+} NS_ENUM_AVAILABLE(10_12_1, 3_0);
 
 typedef NS_ENUM(NSInteger, MPRepeatType) {
     MPRepeatTypeOff,    /// Nothing is repeated during playback.
     MPRepeatTypeOne,    /// Repeat a single item indefinitely.
     MPRepeatTypeAll,    /// Repeat the current container or playlist indefinitely.
-} NS_ENUM_AVAILABLE_IOS(3_0);
+} NS_ENUM_AVAILABLE(10_12_1, 3_0);
 
 typedef NS_ENUM(NSInteger, MPChangeLanguageOptionSetting) {
     MPChangeLanguageOptionSettingNone, /// No Language Option Change
     MPChangeLanguageOptionSettingNowPlayingItemOnly, /// The Language Option change applies only the the now playing item
     MPChangeLanguageOptionSettingPermanent /// The Language Option change should apply to all future playback
-} NS_ENUM_AVAILABLE_IOS(9_4);
+} NS_ENUM_AVAILABLE(10_12_1, 9_4);
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPVolumeView.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPVolumeView.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPVolumeView.h	2016-08-11 06:42:45.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPVolumeView.h	2016-10-24 06:54:13.000000000 +0200
@@ -11,8 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MP_EXTERN_CLASS_AVAILABLE(2_0)
-__TVOS_PROHIBITED
+MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(2.0, 10.12.1, 2.0)
 @interface MPVolumeView : UIView <NSCoding>
 
 @property (nonatomic) BOOL showsVolumeSlider NS_AVAILABLE_IOS(4_2); // Default is YES.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayer.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayer.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayer.h	2016-08-11 06:42:45.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayer.h	2016-10-24 06:54:13.000000000 +0200
@@ -6,9 +6,9 @@
 //
 
 #import <MediaPlayer/MediaPlayerDefines.h>
-#import <MediaPlayer/MPContentItem.h>
-#import <MediaPlayer/MPError.h>
-#import <MediaPlayer/MPMediaItem.h>
+#import <TargetConditionals.h>
+
+#if TARGET_OS_IPHONE
 #import <MediaPlayer/MPMediaItemCollection.h>
 #import <MediaPlayer/MPMediaLibrary.h>
 #import <MediaPlayer/MPMediaPickerController.h>
@@ -18,15 +18,22 @@
 #import <MediaPlayer/MPMoviePlayerController.h>
 #import <MediaPlayer/MPMoviePlayerViewController.h>
 #import <MediaPlayer/MPMusicPlayerController.h>
-#import <MediaPlayer/MPNowPlayingInfoCenter.h>
-#import <MediaPlayer/MPNowPlayingInfoLanguageOption.h>
+#import <MediaPlayer/MPMusicPlayerQueueDescriptor.h>
 #import <MediaPlayer/MPPlayableContentDataSource.h>
 #import <MediaPlayer/MPPlayableContentDelegate.h>
 #import <MediaPlayer/MPPlayableContentManager.h>
 #import <MediaPlayer/MPPlayableContentManagerContext.h>
+#import <MediaPlayer/MPVolumeSettings.h>
+#import <MediaPlayer/MPVolumeView.h>
+#endif
+
+#import <MediaPlayer/AVFoundation+MPNowPlayingInfoLanguageOptionAdditions.h>
+#import <MediaPlayer/MPContentItem.h>
+#import <MediaPlayer/MPError.h>
+#import <MediaPlayer/MPMediaItem.h>
+#import <MediaPlayer/MPNowPlayingInfoCenter.h>
+#import <MediaPlayer/MPNowPlayingInfoLanguageOption.h>
 #import <MediaPlayer/MPRemoteCommand.h>
 #import <MediaPlayer/MPRemoteCommandCenter.h>
 #import <MediaPlayer/MPRemoteCommandEvent.h>
 #import <MediaPlayer/MPRemoteControlTypes.h>
-#import <MediaPlayer/MPVolumeSettings.h>
-#import <MediaPlayer/MPVolumeView.h>
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayerDefines.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayerDefines.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayerDefines.h	2016-08-11 06:42:45.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MediaPlayerDefines.h	2016-10-24 06:54:13.000000000 +0200
@@ -11,5 +11,31 @@
 #define MP_EXTERN     extern __attribute__((visibility ("default")))
 #endif
 
-#define MP_EXTERN_CLASS                    __attribute__((visibility("default")))
-#define MP_EXTERN_CLASS_AVAILABLE(version) __attribute__((visibility("default"))) NS_CLASS_AVAILABLE(NA, version)
+#define MP_EXTERN_CLASS                       __attribute__((visibility("default")))
+#define MP_EXTERN_CLASS_AVAILABLE(version)    __attribute__((visibility("default"))) NS_CLASS_AVAILABLE(NA, version)
+#define MP_EXTERN_CLASS_AVAILABLE_X(ios, mac) __attribute__((visibility("default"))) NS_CLASS_AVAILABLE(mac, ios)
+
+#define MP_API __attribute__((visibility("default"))) __API_AVAILABLE
+#define MP_DEPRECATED __attribute__((visibility("default"))) __API_DEPRECATED
+#define MP_DEPRECATED_WITH_REPLACEMENT __attribute__((visibility("default"))) __API_DEPRECATED_WITH_REPLACEMENT
+#define MP_UNAVAILABLE __attribute__((visibility("default"))) __API_UNAVAILABLE
+
+#if __has_include(<AvailabilityProhibitedInternal.h>)
+#define MP_API_IOS_AVAILABLE_TVOS_PROHIBITED(iosver, macosver, tvosver) MP_API(ios(iosver), tvos(tvosver), macos(macosver)) __TVOS_PROHIBITED
+#define MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(iosver, macosver, tvosver) MP_API(ios(iosver), tvos(tvosver), macos(macosver)) __TVOS_PROHIBITED
+#define MP_API_IOS_DEPRECATED_TVOS_PROHIBITED(iosintro, iosdep, macosintro, macosdep, tvosintro, tvosdep) \
+    MP_DEPRECATED("No longer supported", ios(iosintro, iosdep), tvos(tvosintro, tvosdep), macos(macosintro, macosdep)) __TVOS_PROHIBITED
+#define MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(iosintro, iosdep, macosintro, macosdep, tvosintro, tvosdep) \
+    MP_DEPRECATED("No longer supported", ios(iosintro, iosdep), tvos(tvosintro, tvosdep), macos(macosintro, macosdep)) __TVOS_PROHIBITED
+#define MP_API_IOS_DEPRECATED_WITH_REPLACEMENT_MACOS_TVOS_PROHIBITED(replacement, iosintro, iosdep, macosintro, macosdep, tvosintro, tvosdep) \
+    MP_DEPRECATED_WITH_REPLACEMENT(replacement, ios(iosintro, iosdep), tvos(tvosintro, tvosdep), macos(macosintro, macosdep)) __TVOS_PROHIBITED
+#else
+#define MP_API_IOS_AVAILABLE_TVOS_PROHIBITED(iosver, macosver, tvosver) MP_API(ios(iosver), macos(macosver)) __TVOS_PROHIBITED
+#define MP_API_IOS_AVAILABLE_MACOS_TVOS_PROHIBITED(iosver, macosver, tvosver) MP_API(ios(iosver)) __TVOS_PROHIBITED __OS_AVAILABILITY(macosx,unavailable)
+#define MP_API_IOS_DEPRECATED_TVOS_PROHIBITED(iosintro, iosdep, macosintro, macosdep, tvosintro, tvosdep) \
+    MP_DEPRECATED("No longer supported", ios(iosintro, iosdep), macos(macosintro, macosdep)) __TVOS_PROHIBITED
+#define MP_API_IOS_DEPRECATED_MACOS_TVOS_PROHIBITED(iosintro, iosdep, macosintro, macosdep, tvosintro, tvosdep) \
+    MP_DEPRECATED("No longer supported", ios(iosintro, iosdep)) __TVOS_PROHIBITED __OS_AVAILABILITY(macosx,unavailable)
+#define MP_API_IOS_DEPRECATED_WITH_REPLACEMENT_MACOS_TVOS_PROHIBITED(replacement, iosintro, iosdep, macosintro, macosdep, tvosintro, tvosdep) \
+    MP_DEPRECATED_WITH_REPLACEMENT(replacement, ios(iosintro, iosdep)) __TVOS_PROHIBITED __OS_AVAILABILITY(macosx,unavailable)
+#endif

```