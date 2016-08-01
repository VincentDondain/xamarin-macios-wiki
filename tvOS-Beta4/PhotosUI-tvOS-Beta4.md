#PhotosUI.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PhotosUI.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PhotosUI.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PhotosUI.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PhotosUI.h	2016-07-28 06:03:39.000000000 +0200
@@ -0,0 +1,18 @@
+//
+//  PhotosUI.h
+//  PhotosUI
+//
+//  Copyright (c) 2014 Apple Inc. All rights reserved.
+//
+
+#ifndef PhotosUI_PhotosUI_h
+#define PhotosUI_PhotosUI_h
+
+#import <TargetConditionals.h>
+
+#if !TARGET_OS_TV
+#import <PhotosUI/PHContentEditingController.h>
+#endif
+#import <PhotosUI/PHLivePhotoView.h>
+
+#endif

```