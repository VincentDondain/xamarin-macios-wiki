#AVKit.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerItem.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerItem.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerItem.h	2016-08-11 06:50:28.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerItem.h	2016-10-25 07:42:41.000000000 +0200
@@ -18,6 +18,26 @@
 @class AVMetadataItem;
 @class AVNavigationMarkersGroup;
 
+
+/*!
+ @constant AVKitMetadataIdentifierExternalContentIdentifier
+ @abstract AVKit will publish the value of this metadata item to MPNowPlayingInfoPropertyExternalContentIdentifier.
+ */
+AVKIT_EXTERN NSString *const AVKitMetadataIdentifierExternalContentIdentifier NS_AVAILABLE_IOS(10_1);
+
+/*!
+ @constant AVKitMetadataIdentifierExternalUserProfileIdentifier
+ @abstract AVKit will publish the value of this metadata item to MPNowPlayingInfoPropertyExternalUserProfileIdentifier.
+ */
+AVKIT_EXTERN NSString *const AVKitMetadataIdentifierExternalUserProfileIdentifier NS_AVAILABLE_IOS(10_1);
+
+/*!
+ @constant AVKitMetadataIdentifierPlaybackProgress
+ @abstract AVKit will publish the value of this metadata item to MPNowPlayingInfoPropertyPlaybackProgress.
+ */
+AVKIT_EXTERN NSString *const AVKitMetadataIdentifierPlaybackProgress NS_AVAILABLE_IOS(10_1);
+
+
 @interface AVPlayerItem (AVPlayerViewControllerAdditions)
 
 /*!
@@ -30,12 +50,16 @@
 /*!
 	@property	externalMetadata
 	@abstract	Supplements metadata contained in the asset.
-	@discussion This property is for display purposes only. All keys defined in AVMetadataIdentifiers.h are valid. The full set of presentable metadata varies by release and platform. The following are displayed on TVOS:
+	@discussion This property is for display purposes, and will also be published as Now Playing Info. All keys defined in AVMetadataIdentifiers.h are valid. The full set of presentable metadata varies by release. The following are displayed on tvOS:
 		 AVMetadataCommonIdentifierTitle
 		 AVMetadataCommonIdentifierDescription
 		 AVMetadataIdentifieriTunesMetadataContentRating
 		 AVMetadataIdentifierQuickTimeMetadataGenre
 	 Values are normally strings. Poster artwork can be provided with AVMetadataCommonIdentifierArtwork.
+	 The following are not displayed, but will be published through Now Playing Info:
+		 AVKitMetadataIdentifierExternalContentIdentifier
+		 AVKitMetadataIdentifierExternalProfileIdentifier
+		 AVKitMetadataIdentifierPlaybackProgress
  */
 @property (nonatomic, copy) NSArray<AVMetadataItem *> *externalMetadata;
 

```