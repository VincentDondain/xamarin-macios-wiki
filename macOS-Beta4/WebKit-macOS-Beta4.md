#WebKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebViewConfiguration.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebViewConfiguration.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebViewConfiguration.h	2016-07-11 08:37:12.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebViewConfiguration.h	2016-07-25 08:15:52.000000000 +0200
@@ -182,6 +182,12 @@
  */
 @property (nonatomic) WKDataDetectorTypes dataDetectorTypes API_AVAILABLE(ios(10.0));
 
+/*! @abstract A Boolean value indicating whether the WKWebView should always allow scaling of the web page, regardless of author intent.
+ @discussion This will override the user-scalable property.
+ The default value is NO.
+ */
+@property (nonatomic) BOOL ignoresViewportScaleLimits API_AVAILABLE(ios(10.0));
+
 #else
 
 /*! @abstract The directionality of user interface elements.
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/WebKit.framework/Headers/WebKitErrors.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/WebKit.framework/Headers/WebKitErrors.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/WebKit.framework/Headers/WebKitErrors.h	2016-07-11 08:37:13.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/WebKit.framework/Headers/WebKitErrors.h	2016-07-24 00:08:47.000000000 +0200
@@ -1,5 +1,5 @@
 /*
- * Copyright (C) 2003 Apple Inc.  All rights reserved.
+ * Copyright (C) 2003-2016 Apple Inc. All rights reserved.
  *
  * Redistribution and use in source and binary forms, with or without
  * modification, are permitted provided that the following conditions

```