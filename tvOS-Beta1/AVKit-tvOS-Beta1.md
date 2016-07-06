#AVKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposal.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposal.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposal.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposal.h	2016-06-02 07:09:49.000000000 +0200
@@ -0,0 +1,125 @@
+/*
+	File:  AVContentProposal.h
+	
+	Framework:  AVKit
+	
+	Copyright 2016 Apple Inc. All rights reserved.
+	
+ */
+
+#import <AVFoundation/AVFoundation.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class AVMetadataItem;
+@class AVPlayerViewController;
+@class UIImage;
+
+
+/*!
+	@class AVContentProposal
+	@abstract AVContentProposal describes content proposed to follow the current item (for example, the next episode of the same series).
+ */
+
+NS_CLASS_AVAILABLE_IOS(10_0)
+@interface AVContentProposal : NSObject <NSCopying>
+
+/*!
+	@property contentTimeForTransition
+	@abstract The time, within the bounds of the current playerItem, when the content proposal presentation should begin.
+	@discussion This commonly marks the beginning of the end credits in a television show or movie. For other content, this may be at the very end of the video. The default value,
+ kCMTimeIndefinite, indicates that the transition should occur at the very end of the playerItem; this is equivalent to using the duration of the asset.
+ */
+@property (nonatomic, readonly) CMTime contentTimeForTransition;
+
+/*!
+	@property automaticAcceptanceInterval
+	@abstract The interval between the time playback ends, and automatic acceptance of this content proposal.
+	@discussion The content proposal will display a countdown timer to reflect this value. Set this value to NAN to disable automatic acceptance, which is the default.
+ */
+@property (nonatomic, readwrite) NSTimeInterval automaticAcceptanceInterval;
+
+/*!
+	@property title
+	@abstract The title of the proposed content.
+ */
+@property (nonatomic, readonly, copy) NSString *title;
+
+/*!
+	@property previewImage
+	@abstract The (optional, but recommended) preview image for the proposed item (typically a frame from the proposed video, not poster artwork).
+ */
+@property (nonatomic, readonly, nullable) UIImage *previewImage;
+
+/*!
+	@property URL
+	@abstract The URL for the proposed content, or nil.
+	@discussion If the URL is nil, then the AVContentProposalDelegate must handle content proposal acceptance. 
+ */
+@property (nonatomic, readwrite, nullable) NSURL *URL;
+
+/*!
+	@property metadata
+	@abstract Optional additional metadata for the proposed item.
+	@discussion This can be used to specify season and episode numbers.
+ */
+@property (nonatomic, copy) NSArray<AVMetadataItem *> *metadata;
+
+/*!
+	@method initWithContentTimeForTransition:title:previewImage:
+	@parameter contentTimeForTransition
+		The time, within the bounds of the current playerItem, when the content proposal presentation should begin.
+	@parameter title
+		The title of the proposed content.
+	@parameter previewImage
+		The preview image for the proposed item.
+*/
+- (instancetype)initWithContentTimeForTransition:(CMTime)contentTimeForTransition title:(NSString *)title previewImage:(nullable UIImage *)previewImage NS_DESIGNATED_INITIALIZER;
+
+/* Use initWithContentTimeForTransition:title:previewImage: instead.
+ */
+- (instancetype)init NS_UNAVAILABLE;
+
+@end
+
+
+@protocol AVContentProposalDelegate /* AVPlayerViewControllerDelegate AVContentProposal extensions */
+@optional
+
+/*!
+	@method playerViewController:shouldPresentContentProposal:
+	@abstract Should return YES, if implemented, to allow presentation of the content proposal.
+	@discussion The delegate may wish to create a custom view controller when this is called.
+ */
+- (BOOL)playerViewController:(AVPlayerViewController *)playerViewController shouldPresentContentProposal:(AVContentProposal *)proposal NS_AVAILABLE_IOS(10_0);
+
+/*!
+	@method	playerViewController:didAcceptContentProposal:
+	@abstract The delegate should replace the current player item with the next item.
+	@description Clients must implement this method when setting the nextContentProposal property of AVPlayerViewController. The delegate should create a new AVPlayerItem and update the AVPlayer or AVQueuePlayer.
+ */
+- (void)playerViewController:(AVPlayerViewController *)playerViewController didAcceptContentProposal:(AVContentProposal *)proposal NS_AVAILABLE_IOS(10_0);
+
+/*!
+	@method	playerViewController:didRejectContentProposal:
+	@abstract The delegate should react to the user rejecting the content proposal, typically by dismissing the player view controller.
+	@description If the client does not implement this method, the player view controller will be dismissed.
+ */
+- (void)playerViewController:(AVPlayerViewController *)playerViewController didRejectContentProposal:(AVContentProposal *)proposal NS_AVAILABLE_IOS(10_0);
+
+@end
+
+
+@interface AVPlayerItem (AVContentProposal)
+
+/*!
+	@property nextContentProposal
+	@abstract The item proposed to follow the current content.
+	@description When null, no content will be proposed following this item. Only one item can have proposed "next" content at a time. Clients should also implement the AVPlayerViewControllerDelegate
+ method 'playerViewController:didAcceptProposal:'.
+ */
+@property (nonatomic, nullable) AVContentProposal *nextContentProposal NS_AVAILABLE_IOS(10_0);
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposalViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposalViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposalViewController.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposalViewController.h	2016-06-02 07:09:51.000000000 +0200
@@ -0,0 +1,85 @@
+/*
+	File:  AVContentProposalViewController
+	
+	Framework:  AVKit
+	
+	Copyright 2016 Apple Inc. All rights reserved.
+ */
+
+#import <AVKit/AVPlayerViewController.h>
+
+@class AVContentProposal;
+@class AVContentProposalViewController;
+
+NS_ASSUME_NONNULL_BEGIN
+
+typedef NS_ENUM(NSInteger, AVContentProposalAction) {
+	AVContentProposalActionAccept,
+	AVContentProposalActionReject,
+	AVContentProposalActionDefer
+};
+
+NS_CLASS_AVAILABLE_IOS(10_0)
+@interface AVContentProposalViewController : UIViewController
+
+/*!
+	@property contentProposal
+	@abstract The associated content proposal.
+	@discussion This property is set by the AVPlayerViewController; clients should normally not set this property.
+ */
+@property (nonatomic, readonly, nullable) AVContentProposal *contentProposal;
+
+/*!
+	@property playerViewController
+	@abstract The playerViewController presenting this content proposal.
+	@discussion This property will be set during presentation of the content proposal. It may be nil at other times.
+ */
+@property (nonatomic, readonly, weak, nullable) AVPlayerViewController *playerViewController;
+
+/*!
+	@property preferredPlayerViewFrame
+	@abstract Contains the desired frame of the player view during presentation of the content proposal.
+	@discussion By default, this returns the entire screen bounds, but custom view controllers may return a smaller rectangle, or CGRectZero to hide the player view completely.
+ */
+@property (nonatomic, readonly) CGRect preferredPlayerViewFrame;
+
+/*!
+	@property playerLayoutGuide
+	@abstract Contains a layer guide that tracks the size and location of the player view.
+	@discussion The view controller can constrain its views using the anchors of the playerLayoutGuide, which has the same size and position as the player view.
+ */
+@property (nonatomic, readonly) UILayoutGuide *playerLayoutGuide;
+
+/*!
+	@property dateOfAutomaticAcceptance
+	@abstract The date that this content proposal is scheduled to be automatically accepted.
+	@discussion When this value is nil, automatic acceptance is not scheduled. It is scheduled when the proposal is presented, and may be unscheduled if the user cancels automatic acceptance, manually accepts, or otherwise dismisses the proposal. During presentation, clients should set this property to nil to indicate that automatic acceptance has been canceled.
+ */
+@property (nonatomic, nullable) NSDate *dateOfAutomaticAcceptance;
+
+/*!
+	@method dismissContentProposalForAction:animated:completion:
+	@param	action
+			Indicates whether the user accepts or rejects the content proposal, or has deferred the decision.
+	@param	animated
+			YES if animation should be employed, NO if the presentation should be dismissed immediately.
+	@param	completion
+			An optional block that will be called when the proposal has been hidden.
+	@discussion The user is leaving the presentation. For action AVContentProposalActionDefer, the video will resume playing, or if it has ended, will replay from the beginning. For AVContentProposalActionAccept, the proposed content will begin to play; for AVContentProposalActionReject, the player view controller will be dismissed.
+ */
+- (void)dismissContentProposalForAction:(AVContentProposalAction)action animated:(BOOL)animated completion:(nullable void (^)(void))block;
+
+@end
+
+@interface AVPlayerViewController (AVContentProposalViewController)
+
+/*!
+	@property contentProposalViewController
+	@abstract The view controller responsible for the presentation of content proposals.
+	@discussion This should be set to a custom subclass of AVContentProposalViewController.
+ */
+@property (nonatomic, null_resettable) __kindof AVContentProposalViewController *contentProposalViewController NS_AVAILABLE_IOS(10_0);
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVKit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVKit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVKit.h	2015-10-10 07:17:42.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVKit.h	2016-06-02 07:09:51.000000000 +0200
@@ -3,7 +3,7 @@
 	
 	Framework:  AVKit
 	
-	Copyright 2015 Apple Inc. All rights reserved.
+	Copyright 2015-2016 Apple Inc. All rights reserved.
 	
 	To report bugs, go to:  http://developer.apple.com/bugreporter/
 	
@@ -11,7 +11,9 @@
 
 #import <AVKit/AVKitDefines.h>
 
+#import <AVKit/AVContentProposal.h>
+#import <AVKit/AVContentProposalViewController.h>
 #import <AVKit/AVInterstitialTimeRange.h>
 #import <AVKit/AVNavigationMarkersGroup.h>
-#import <AVKit/AVPlayerViewController.h>
 #import <AVKit/AVPlayerItem.h>
+#import <AVKit/AVPlayerViewController.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerViewController.h	2015-10-10 07:17:42.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerViewController.h	2016-06-02 07:09:49.000000000 +0200
@@ -94,6 +94,44 @@
 
 
 /*!
+	@constant	AVPlayerViewControllerSkippingBehaviorDefault
+	@abstract	The default skipping behavior.
+	@constant	AVPlayerViewControllerSkippingBehaviorSkipItem
+	@abstract	Skip to next/previous item (as in a playlist).
+ */
+typedef NS_ENUM(NSInteger, AVPlayerViewControllerSkippingBehavior) {
+	AVPlayerViewControllerSkippingBehaviorDefault = 0,
+	AVPlayerViewControllerSkippingBehaviorSkipItem
+};
+
+
+@interface AVPlayerViewController (AVPlayerViewControllerSkippingBehavior)
+
+/*
+	@property skippingBehavior
+	@abstract Specifies the behavior triggered by skipping gestures. AVPlayerViewControllerSkippingBehaviorDefault is the default value.
+	@discussion Use this property to override the default skipping behavior.
+ */
+@property (nonatomic) AVPlayerViewControllerSkippingBehavior skippingBehavior NS_AVAILABLE_IOS(10_0);
+
+/*
+	@property skipForwardEnabled
+	@abstract Indicates whether forward-skipping is available.
+	@discussion This property affects the appearance of the forward-skipping indicator. The behavior associated with forward-skipping is identified by the skippingBehavior property.
+ */
+@property (nonatomic, getter = isSkipForwardEnabled) BOOL skipForwardEnabled NS_AVAILABLE_IOS(10_0);
+
+/*
+	@property skipBackwardEnabled
+	@abstract Indicates whether backward-skipping is available.
+	@discussion This property affects the appearance of the backward-skipping indicator. The behavior associated with backward-skipping is identified by the skippingBehavior property.
+ */
+@property (nonatomic, getter = isSkipBackwardEnabled) BOOL skipBackwardEnabled NS_AVAILABLE_IOS(10_0);
+
+@end
+
+
+/*!
 	@protocol	AVPlayerViewControllerDelegate
 	@abstract	A protocol for delegates of AVPlayerViewController.
  */
@@ -135,6 +173,19 @@
 - (void)playerViewController:(AVPlayerViewController *)playerViewController willResumePlaybackAfterUserNavigatedFromTime:(CMTime)oldTime toTime:(CMTime)targetTime;
 
 /*!
+	@method		playerViewController:timeToSeekAfterUserNavigatedFromTime:toTime:
+	@param		playerViewController
+				The player view controller.
+	@param		oldTime
+				The playback time before the user began navigating.
+	@param		targetTime
+				The playback time selected by the user.
+	@abstract	The delegate can implement this method to be notified when the user has skipped, scrubbed, or otherwise navigated to a new time, and wants to resume playback at the target time.
+	@discussion	This delegate method is delivered for (and only for) user-initiated changes to the playback time. If the user skips/scrubs several times before resuming playback, this method is only called once. This method should not be used to disable scrubbing; use the requiresLinearPlayback property of the AVPlayerViewController instead.
+ */
+- (CMTime)playerViewController:(AVPlayerViewController *)playerViewController timeToSeekAfterUserNavigatedFromTime:(CMTime)oldTime toTime:(CMTime)targetTime NS_AVAILABLE_IOS(10_0);
+
+/*!
 	@method		playerViewController:didSelectMediaSelectionOption:inMediaSelectionGroup:
 	@param		playerViewController
 				The player view controller.
@@ -158,6 +209,22 @@
  */
 - (void)playerViewController:(AVPlayerViewController *)playerViewController didSelectExternalSubtitleOptionLanguage:(NSString *)language NS_SWIFT_UNAVAILABLE("External subtitle options are not supported");
 
+/*
+	@method		skipToNextItemForPlayerViewController:
+	@param		playerViewController
+				The player view controller.
+	@discussion	Clients that request non-default skipping behavior should implement this method. The delegate should update the playerViewController’s player to play the next player item.
+ */
+- (void)skipToNextItemForPlayerViewController:(AVPlayerViewController *)playerViewController NS_AVAILABLE_IOS(10_0);
+
+/*
+	@method		skipToPreviousItemForPlayerViewController:
+	@param		playerViewController
+				The player view controller.
+	@discussion	The delegate should update the playerViewController’s player to play the previous player item.
+ */
+- (void)skipToPreviousItemForPlayerViewController:(AVPlayerViewController *)playerViewController NS_AVAILABLE_IOS(10_0);
+
 @end
 
 NS_ASSUME_NONNULL_END

```