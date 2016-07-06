#ImageIO.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageDestination.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageDestination.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageDestination.h	2015-08-23 02:35:40.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageDestination.h	2016-05-28 06:38:30.000000000 +0200
@@ -1,6 +1,6 @@
 /*
  * ImageIO - CGImageDestination.h
- * Copyright (c) 2004-2010 Apple Inc. All rights reserved.
+ * Copyright (c) 2004-2016 Apple Inc. All rights reserved.
  *
  */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageMetadata.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageMetadata.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageMetadata.h	2015-08-23 02:35:40.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageMetadata.h	2016-05-28 06:17:13.000000000 +0200
@@ -1,6 +1,8 @@
-// *****************************************************************************
-// CGImageMetadata.h
-// *****************************************************************************
+/*
+ * ImageIO - CGImageMetadata.h
+ * Copyright (c) 2004-2016 Apple Inc. All rights reserved.
+ *
+ */
 
 #ifndef CGIMAGEMETADATA_H_
 #define CGIMAGEMETADATA_H_
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageProperties.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageProperties.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageProperties.h	2015-08-23 02:35:40.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageProperties.h	2016-05-28 06:17:12.000000000 +0200
@@ -1,6 +1,6 @@
 /*
  * ImageIO - CGImageProperties.h
- * Copyright (c) 2004-2010 Apple Inc. All rights reserved.
+ * Copyright (c) 2004-2016 Apple Inc. All rights reserved.
  *
  */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageSource.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageSource.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageSource.h	2015-08-23 02:35:40.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageSource.h	2016-05-28 06:38:32.000000000 +0200
@@ -1,6 +1,6 @@
 /*
  * ImageIO - CGImageSource.h
- * Copyright (c) 2004-2010 Apple Inc. All rights reserved.
+ * Copyright (c) 2004-2016 Apple Inc. All rights reserved.
  *
  */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ImageIO.framework/Headers/ImageIO.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageIO.framework/Headers/ImageIO.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ImageIO.framework/Headers/ImageIO.h	2015-08-23 02:35:40.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageIO.framework/Headers/ImageIO.h	2016-05-28 05:15:43.000000000 +0200
@@ -1,6 +1,6 @@
 /*
  * ImageIO - ImageIO.h
- * Copyright (c) 2004-2010 Apple Inc. All rights reserved.
+ * Copyright (c) 2004-2016 Apple Inc. All rights reserved.
  *
  */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ImageIO.framework/Headers/ImageIOBase.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageIO.framework/Headers/ImageIOBase.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ImageIO.framework/Headers/ImageIOBase.h	2015-08-23 02:35:40.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ImageIO.framework/Headers/ImageIOBase.h	2016-05-28 05:15:43.000000000 +0200
@@ -1,6 +1,6 @@
 /*
  * ImageIO - ImageIOBase.h
- * Copyright (c) 2009-2010 Apple Inc. 
+ * Copyright (c) 2009-2016 Apple Inc. 
  * All rights reserved.
  *
  */

```