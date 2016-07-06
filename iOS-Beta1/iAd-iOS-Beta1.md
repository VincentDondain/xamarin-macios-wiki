#iAd.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/iAd.framework/Headers/ADBannerView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/iAd.framework/Headers/ADBannerView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/iAd.framework/Headers/ADBannerView.h	2016-02-20 01:15:57.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/iAd.framework/Headers/ADBannerView.h	2016-05-26 07:53:43.000000000 +0200
@@ -79,7 +79,7 @@
     ADErrorAssetLoadFailure = 8,
 #endif
 
-} NS_ENUM_AVAILABLE_IOS(4_0);
+} NS_ENUM_DEPRECATED_IOS(4_0, 10_0);
 
 /*!
  * @enum ADAdType
@@ -99,7 +99,7 @@
 typedef NS_ENUM(NSInteger, ADAdType) {
     ADAdTypeBanner,
     ADAdTypeMediumRectangle
-} NS_ENUM_AVAILABLE_IOS(6_0);
+} NS_ENUM_DEPRECATED_IOS(6_0, 10_0);
 
 @protocol ADBannerViewDelegate;
 
@@ -117,7 +117,7 @@
  * managing the banner view must be correctly configured to ensure banner action
  * presentation works correctly.
  */
-NS_CLASS_AVAILABLE_IOS(4_0) @interface ADBannerView : UIView
+NS_CLASS_DEPRECATED_IOS(4_0, 10_0) @interface ADBannerView : UIView
 
 /*!
  * @method initWithAdType:
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/iAd.framework/Headers/ADInterstitialAd.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/iAd.framework/Headers/ADInterstitialAd.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/iAd.framework/Headers/ADInterstitialAd.h	2015-10-03 02:30:33.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/iAd.framework/Headers/ADInterstitialAd.h	2016-05-26 07:53:43.000000000 +0200
@@ -33,7 +33,7 @@
  * Note that using interstitial ads on iPhones running iOS < 7.0 will cause an
  * exception to be thrown.
  */
-NS_CLASS_AVAILABLE_IOS(4_3) @interface ADInterstitialAd : NSObject
+NS_CLASS_DEPRECATED_IOS(4_3, 10_0) @interface ADInterstitialAd : NSObject
 
 /*!
  * @property delegate
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/iAd.framework/Headers/MPMoviePlayerController_iAdPreroll.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/iAd.framework/Headers/MPMoviePlayerController_iAdPreroll.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/iAd.framework/Headers/MPMoviePlayerController_iAdPreroll.h	2015-10-03 02:30:33.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/iAd.framework/Headers/MPMoviePlayerController_iAdPreroll.h	2016-05-26 07:53:43.000000000 +0200
@@ -5,6 +5,9 @@
 //  Copyright 2012 Apple, Inc. All rights reserved.
 //
 
+#import <TargetConditionals.h>
+
+#if TARGET_OS_IOS
 #import <MediaPlayer/MediaPlayer.h>
 
 /*!
@@ -61,3 +64,4 @@
 - (void)cancelPreroll NS_AVAILABLE_IOS(8_0);
 
 @end
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/iAd.framework/Headers/UIViewControlleriAdAdditions.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/iAd.framework/Headers/UIViewControlleriAdAdditions.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/iAd.framework/Headers/UIViewControlleriAdAdditions.h	2015-10-03 02:30:33.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/iAd.framework/Headers/UIViewControlleriAdAdditions.h	2016-05-25 05:44:54.000000000 +0200
@@ -30,7 +30,7 @@
     ADInterstitialPresentationPolicyNone = 0,
     ADInterstitialPresentationPolicyAutomatic,
     ADInterstitialPresentationPolicyManual
-}  NS_ENUM_AVAILABLE_IOS(7_0);
+}  NS_ENUM_DEPRECATED_IOS(7_0, 10_0);
 
 /*!
  * @category UIViewController (iAdAdditions)
@@ -57,7 +57,7 @@
  * view controller's interstitialPresentationPolicy is set to something other
  * than ADInterstitialPresentationPolicyNone.
  */
-+ (void)prepareInterstitialAds NS_AVAILABLE_IOS(7_0);
++ (void)prepareInterstitialAds NS_DEPRECATED_IOS(7_0, 10_0);
 
 /*!
  * @property interstitialPresentationPolicy
@@ -68,7 +68,7 @@
  * -requestInterstitialAdPresentation. By default the policy is "None", so to be
  * able to present an interstitial it must be changed to either "Automatic" or "Manual".
  */
-@property (nonatomic, assign) ADInterstitialPresentationPolicy interstitialPresentationPolicy NS_AVAILABLE_IOS(7_0);
+@property (nonatomic, assign) ADInterstitialPresentationPolicy interstitialPresentationPolicy NS_DEPRECATED_IOS(7_0, 10_0);
 
 /*!
  * @property canDisplayBannerAds
@@ -83,7 +83,7 @@
  *
  * @seealso originalContentView
  */
-@property (nonatomic, assign) BOOL canDisplayBannerAds NS_AVAILABLE_IOS(7_0);
+@property (nonatomic, assign) BOOL canDisplayBannerAds NS_DEPRECATED_IOS(7_0, 10_0);
 
 /*!
  * @property originalContentView
@@ -95,7 +95,7 @@
  * disabled, the view controller's content view will remain embedded - that operation
  * will not be reversed.
  */
-@property (nonatomic, retain, readonly) UIView *originalContentView NS_AVAILABLE_IOS(7_0);
+@property (nonatomic, retain, readonly) UIView *originalContentView NS_DEPRECATED_IOS(7_0, 10_0);
 
 /*!
  * @property presentingFullScreenAd
@@ -104,7 +104,7 @@
  * Can be used to query the controller to determine if it is presenting a full screen
  * ad, which may be an interstitial or the iAd shown when the user taps a banner.
  */
-@property (nonatomic, readonly, getter=isPresentingFullScreenAd) BOOL presentingFullScreenAd NS_AVAILABLE_IOS(7_0);
+@property (nonatomic, readonly, getter=isPresentingFullScreenAd) BOOL presentingFullScreenAd NS_DEPRECATED_IOS(7_0, 10_0);
 
 /*!
  * @property displayingBannerAd
@@ -112,7 +112,7 @@
  * @discussion
  * Can be used to query the controller to determine if it is displaying a banner ad.
  */
-@property (nonatomic, readonly, getter=isDisplayingBannerAd) BOOL displayingBannerAd NS_AVAILABLE_IOS(7_0);
+@property (nonatomic, readonly, getter=isDisplayingBannerAd) BOOL displayingBannerAd NS_DEPRECATED_IOS(7_0, 10_0);
 
 /*!
  * @method requestInterstitialAdPresentation
@@ -126,7 +126,7 @@
  * manage significant state changes, such as game levels. Returns YES if an interstitial
  * will be presented.
  */
-- (BOOL)requestInterstitialAdPresentation NS_AVAILABLE_IOS(7_0);
+- (BOOL)requestInterstitialAdPresentation NS_DEPRECATED_IOS(7_0, 10_0);
 
 /*!
  * @method shouldPresentInterstitialAd
@@ -141,6 +141,6 @@
  * state. The method will be invoked when the framework is about to present an interstitial
  * ad in the ADInterstitialPresentationPolicyAutomatic configuration.
  */
-@property (NS_NONATOMIC_IOSONLY, readonly) BOOL shouldPresentInterstitialAd NS_AVAILABLE_IOS(7_0);
+@property (NS_NONATOMIC_IOSONLY, readonly) BOOL shouldPresentInterstitialAd NS_DEPRECATED_IOS(7_0, 10_0);
 
 @end

```