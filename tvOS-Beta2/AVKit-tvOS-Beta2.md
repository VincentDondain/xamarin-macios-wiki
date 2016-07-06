#AVKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposal.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposal.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposal.h	2016-06-02 07:09:49.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposal.h	2016-06-27 06:43:18.000000000 +0200
@@ -3,7 +3,7 @@
 	
 	Framework:  AVKit
 	
-	Copyright 2016 Apple Inc. All rights reserved.
+	Copyright © 2016 Apple Inc. All rights reserved.
 	
  */
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposalViewController.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposalViewController.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposalViewController.h	2016-06-02 07:09:51.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVContentProposalViewController.h	2016-06-27 06:42:47.000000000 +0200
@@ -3,7 +3,7 @@
 	
 	Framework:  AVKit
 	
-	Copyright 2016 Apple Inc. All rights reserved.
+	Copyright © 2016 Apple Inc. All rights reserved.
  */
 
 #import <AVKit/AVPlayerViewController.h>
@@ -76,7 +76,7 @@
 /*!
 	@property contentProposalViewController
 	@abstract The view controller responsible for the presentation of content proposals.
-	@discussion This should be set to a custom subclass of AVContentProposalViewController.
+	@discussion This can be set to a custom subclass of AVContentProposalViewController. Setting it to nil will restore the default view controller, which provides a standard content proposal presentation.
  */
 @property (nonatomic, null_resettable) __kindof AVContentProposalViewController *contentProposalViewController NS_AVAILABLE_IOS(10_0);
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVInterstitialTimeRange.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVInterstitialTimeRange.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVInterstitialTimeRange.h	2016-06-02 07:09:51.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVInterstitialTimeRange.h	2016-06-27 06:42:47.000000000 +0200
@@ -3,7 +3,7 @@
 	
 	Framework:  AVKit
 	
-	Copyright 2015 Apple Inc. All rights reserved.
+	Copyright © 2015-2016 Apple Inc. All rights reserved.
 	
  */
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVKit.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVKit.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVKit.h	2016-06-02 07:09:51.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVKit.h	2016-06-27 06:42:47.000000000 +0200
@@ -3,7 +3,7 @@
 	
 	Framework:  AVKit
 	
-	Copyright 2015-2016 Apple Inc. All rights reserved.
+	Copyright © 2015-2016 Apple Inc. All rights reserved.
 	
 	To report bugs, go to:  http://developer.apple.com/bugreporter/
 	
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVKitDefines.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVKitDefines.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVKitDefines.h	2016-06-02 07:09:51.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVKitDefines.h	2016-06-27 06:42:47.000000000 +0200
@@ -3,7 +3,7 @@
 	
 	Framework:  AVKit
 	
-	Copyright 2014-2015 Apple Inc. All rights reserved.
+	Copyright © 2014-2016 Apple Inc. All rights reserved.
 	
  */
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVNavigationMarkersGroup.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVNavigationMarkersGroup.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVNavigationMarkersGroup.h	2016-06-02 07:09:51.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVNavigationMarkersGroup.h	2016-06-27 06:42:47.000000000 +0200
@@ -3,7 +3,7 @@
 	
 	Framework:  AVKit
 	
-	Copyright 2015 Apple Inc. All rights reserved.
+	Copyright © 2015-2016 Apple Inc. All rights reserved.
 	
  */
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerItem.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerItem.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerItem.h	2016-06-02 07:09:51.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerItem.h	2016-06-27 06:42:47.000000000 +0200
@@ -3,7 +3,7 @@
 	
 	Framework:  AVKit
 	
-	Copyright 2015 Apple Inc. All rights reserved.
+	Copyright © 2015-2016 Apple Inc. All rights reserved.
 	
  */
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerViewController.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerViewController.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerViewController.h	2016-06-02 07:09:49.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerViewController.h	2016-06-27 06:43:18.000000000 +0200
@@ -3,7 +3,7 @@
 	
 	Framework:  AVKit
 	
-	Copyright 2015 Apple Inc. All rights reserved.
+	Copyright © 2015-2016 Apple Inc. All rights reserved.
  */
 
 #import <CoreMedia/CoreMedia.h>

```