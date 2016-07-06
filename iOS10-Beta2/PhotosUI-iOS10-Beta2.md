#PhotosUI.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHContentEditingController.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHContentEditingController.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHContentEditingController.h	2016-06-01 05:16:03.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PhotosUI.framework/Headers/PHContentEditingController.h	2016-06-28 08:43:14.000000000 +0200
@@ -23,7 +23,7 @@
 - (void)startContentEditingWithInput:(PHContentEditingInput *)contentEditingInput placeholderImage:(UIImage *)placeholderImage;
 
 // Called when the user finishes the editing session. The receiver should prevent the user from editing the asset further. Also, it should create the editing output and call the completion handler. The completion handler returns after the output has been consumed, so it is safe to perform clean up after it returns. The completion handler can (and should best) be called on a background queue.
-- (void)finishContentEditingWithCompletionHandler:(void (^)(PHContentEditingOutput *))completionHandler;
+- (void)finishContentEditingWithCompletionHandler:(void (^)(PHContentEditingOutput * _Nullable))completionHandler;
 
 // Called if the user cancels the editing session. (Can be called while the receiver is producing the editing output.)
 - (void)cancelContentEditing;

```