#OpenGLES.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/OpenGLES.framework/Headers/EAGLDrawable.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/OpenGLES.framework/Headers/EAGLDrawable.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/OpenGLES.framework/Headers/EAGLDrawable.h	2015-09-30 20:56:29.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/OpenGLES.framework/Headers/EAGLDrawable.h	2016-05-18 03:55:47.000000000 +0200
@@ -53,6 +53,9 @@
 /* Request the native window system display the OpenGL ES renderbuffer bound to <target> */
 - (BOOL)presentRenderbuffer:(NSUInteger)target;
 
+/* Request the native window system display the OpenGL ES renderbuffer bound to <target> at specified time */
+- (BOOL)presentRenderbuffer:(NSUInteger)target atTime:(CFTimeInterval)presentationTime;
+
 @end /* EAGLDrawable protocol */
 
 

```