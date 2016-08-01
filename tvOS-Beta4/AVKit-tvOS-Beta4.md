#AVKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposalViewController.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposalViewController.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposalViewController.h	2016-07-14 06:26:07.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposalViewController.h	2016-07-23 00:52:26.000000000 +0200
@@ -76,7 +76,7 @@
 /*!
 	@property contentProposalViewController
 	@abstract The view controller responsible for the presentation of content proposals.
-	@discussion This can be set to a custom subclass of AVContentProposalViewController. Setting it to nil will restore the default view controller, which provides a standard content proposal presentation.
+	@discussion This should be set to a custom subclass of AVContentProposalViewController.
  */
 @property (nonatomic, null_resettable) __kindof AVContentProposalViewController *contentProposalViewController NS_AVAILABLE_IOS(10_0);
 

```