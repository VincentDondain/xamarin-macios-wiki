#OpenGLES.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/OpenGLES.framework/Headers/EAGLDrawable.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/OpenGLES.framework/Headers/EAGLDrawable.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/OpenGLES.framework/Headers/EAGLDrawable.h	2015-10-02 23:48:50.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/OpenGLES.framework/Headers/EAGLDrawable.h	2016-05-14 17:00:29.000000000 +0200
@@ -53,6 +53,9 @@
 /* Request the native window system display the OpenGL ES renderbuffer bound to <target> */
 - (BOOL)presentRenderbuffer:(NSUInteger)target;
 
+/* Request the native window system display the OpenGL ES renderbuffer bound to <target> at specified time */
+- (BOOL)presentRenderbuffer:(NSUInteger)target atTime:(CFTimeInterval)presentationTime;
+
 @end /* EAGLDrawable protocol */
 
 

```