#AVKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposal.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposal.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposal.h	2016-06-27 06:43:18.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposal.h	2016-07-14 06:26:07.000000000 +0200
@@ -17,61 +17,60 @@
 
 
 /*!
-	@class AVContentProposal
-	@abstract AVContentProposal describes content proposed to follow the current item (for example, the next episode of the same series).
+	@class		AVContentProposal
+	@abstract	AVContentProposal describes content proposed to follow the current item (for example, the next episode of the same series).
  */
 
 NS_CLASS_AVAILABLE_IOS(10_0)
 @interface AVContentProposal : NSObject <NSCopying>
 
 /*!
-	@property contentTimeForTransition
-	@abstract The time, within the bounds of the current playerItem, when the content proposal presentation should begin.
-	@discussion This commonly marks the beginning of the end credits in a television show or movie. For other content, this may be at the very end of the video. The default value,
- kCMTimeIndefinite, indicates that the transition should occur at the very end of the playerItem; this is equivalent to using the duration of the asset.
+	@property	contentTimeForTransition
+	@abstract	The time, within the bounds of the current playerItem, when the content proposal presentation should begin.
+	@discussion	This commonly marks the beginning of the end credits in a television show or movie. For other content, this may be at the very end of the video. The default value, kCMTimeIndefinite, indicates that the transition should occur at the very end of the playerItem; this is equivalent to using the duration of the asset.
  */
 @property (nonatomic, readonly) CMTime contentTimeForTransition;
 
 /*!
-	@property automaticAcceptanceInterval
-	@abstract The interval between the time playback ends, and automatic acceptance of this content proposal.
-	@discussion The content proposal will display a countdown timer to reflect this value. Set this value to NAN to disable automatic acceptance, which is the default.
+	@property	automaticAcceptanceInterval
+	@abstract	The interval between the time playback ends, and automatic acceptance of this content proposal.
+	@discussion	The content proposal will display a countdown timer to reflect this value. Set this value to NAN to disable automatic acceptance, which is the default.
  */
 @property (nonatomic, readwrite) NSTimeInterval automaticAcceptanceInterval;
 
 /*!
-	@property title
-	@abstract The title of the proposed content.
+	@property	title
+	@abstract	The title of the proposed content.
  */
 @property (nonatomic, readonly, copy) NSString *title;
 
 /*!
-	@property previewImage
-	@abstract The (optional, but recommended) preview image for the proposed item (typically a frame from the proposed video, not poster artwork).
+	@property	previewImage
+	@abstract	The (optional, but recommended) preview image for the proposed item (typically a frame from the proposed video, not poster artwork).
  */
 @property (nonatomic, readonly, nullable) UIImage *previewImage;
 
 /*!
-	@property URL
-	@abstract The URL for the proposed content, or nil.
-	@discussion If the URL is nil, then the AVContentProposalDelegate must handle content proposal acceptance. 
+	@property	URL
+	@abstract	The URL for the proposed content, or nil.
+	@discussion	If the URL is nil, then the AVContentProposalDelegate must handle content proposal acceptance.
  */
 @property (nonatomic, readwrite, nullable) NSURL *URL;
 
 /*!
-	@property metadata
-	@abstract Optional additional metadata for the proposed item.
-	@discussion This can be used to specify season and episode numbers.
+	@property	metadata
+	@abstract	Optional additional metadata for the proposed item.
+	@discussion	This can be used to specify season and episode numbers.
  */
 @property (nonatomic, copy) NSArray<AVMetadataItem *> *metadata;
 
 /*!
-	@method initWithContentTimeForTransition:title:previewImage:
-	@parameter contentTimeForTransition
+	@method		initWithContentTimeForTransition:title:previewImage:
+	@parameter	contentTimeForTransition
 		The time, within the bounds of the current playerItem, when the content proposal presentation should begin.
-	@parameter title
+	@parameter	title
 		The title of the proposed content.
-	@parameter previewImage
+	@parameter	previewImage
 		The preview image for the proposed item.
 */
 - (instancetype)initWithContentTimeForTransition:(CMTime)contentTimeForTransition title:(NSString *)title previewImage:(nullable UIImage *)previewImage NS_DESIGNATED_INITIALIZER;
@@ -83,33 +82,6 @@
 @end
 
 
-@protocol AVContentProposalDelegate /* AVPlayerViewControllerDelegate AVContentProposal extensions */
-@optional
-
-/*!
-	@method playerViewController:shouldPresentContentProposal:
-	@abstract Should return YES, if implemented, to allow presentation of the content proposal.
-	@discussion The delegate may wish to create a custom view controller when this is called.
- */
-- (BOOL)playerViewController:(AVPlayerViewController *)playerViewController shouldPresentContentProposal:(AVContentProposal *)proposal NS_AVAILABLE_IOS(10_0);
-
-/*!
-	@method	playerViewController:didAcceptContentProposal:
-	@abstract The delegate should replace the current player item with the next item.
-	@description Clients must implement this method when setting the nextContentProposal property of AVPlayerViewController. The delegate should create a new AVPlayerItem and update the AVPlayer or AVQueuePlayer.
- */
-- (void)playerViewController:(AVPlayerViewController *)playerViewController didAcceptContentProposal:(AVContentProposal *)proposal NS_AVAILABLE_IOS(10_0);
-
-/*!
-	@method	playerViewController:didRejectContentProposal:
-	@abstract The delegate should react to the user rejecting the content proposal, typically by dismissing the player view controller.
-	@description If the client does not implement this method, the player view controller will be dismissed.
- */
-- (void)playerViewController:(AVPlayerViewController *)playerViewController didRejectContentProposal:(AVContentProposal *)proposal NS_AVAILABLE_IOS(10_0);
-
-@end
-
-
 @interface AVPlayerItem (AVContentProposal)
 
 /*!
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerViewController.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerViewController.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerViewController.h	2016-06-27 06:43:18.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerViewController.h	2016-07-14 06:25:44.000000000 +0200
@@ -11,6 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+@class AVContentProposal;
 @class AVPlayer;
 @class AVMediaSelectionOption;
 @class AVMediaSelectionGroup;
@@ -209,7 +210,7 @@
  */
 - (void)playerViewController:(AVPlayerViewController *)playerViewController didSelectExternalSubtitleOptionLanguage:(NSString *)language NS_SWIFT_UNAVAILABLE("External subtitle options are not supported");
 
-/*
+/*!
 	@method		skipToNextItemForPlayerViewController:
 	@param		playerViewController
 				The player view controller.
@@ -217,7 +218,7 @@
  */
 - (void)skipToNextItemForPlayerViewController:(AVPlayerViewController *)playerViewController NS_AVAILABLE_IOS(10_0);
 
-/*
+/*!
 	@method		skipToPreviousItemForPlayerViewController:
 	@param		playerViewController
 				The player view controller.
@@ -225,6 +226,27 @@
  */
 - (void)skipToPreviousItemForPlayerViewController:(AVPlayerViewController *)playerViewController NS_AVAILABLE_IOS(10_0);
 
+/*!
+	@method		playerViewController:shouldPresentContentProposal:
+	@abstract	Should return YES, if implemented, to allow presentation of the content proposal.
+	@discussion	The delegate may wish to create a custom view controller when this is called.
+ */
+- (BOOL)playerViewController:(AVPlayerViewController *)playerViewController shouldPresentContentProposal:(AVContentProposal *)proposal NS_AVAILABLE_IOS(10_0);
+
+/*!
+	@method		playerViewController:didAcceptContentProposal:
+	@abstract	The delegate should replace the current player item with the next item.
+	@discussion	Clients must implement this method when setting the nextContentProposal property of AVPlayerViewController. The delegate should create a new AVPlayerItem and update the AVPlayer or AVQueuePlayer.
+ */
+- (void)playerViewController:(AVPlayerViewController *)playerViewController didAcceptContentProposal:(AVContentProposal *)proposal NS_AVAILABLE_IOS(10_0);
+
+/*!
+	@method		playerViewController:didRejectContentProposal:
+	@abstract	The delegate should react to the user rejecting the content proposal, typically by dismissing the player view controller.
+	@discussion	If the client does not implement this method, the player view controller will be dismissed.
+ */
+- (void)playerViewController:(AVPlayerViewController *)playerViewController didRejectContentProposal:(AVContentProposal *)proposal NS_AVAILABLE_IOS(10_0);
+
 @end
 
 NS_ASSUME_NONNULL_END

```