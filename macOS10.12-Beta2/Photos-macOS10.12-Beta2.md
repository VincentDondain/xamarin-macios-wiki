#Photos.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Photos.framework/Headers/PHLivePhotoEditingContext.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Photos.framework/Headers/PHLivePhotoEditingContext.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Photos.framework/Headers/PHLivePhotoEditingContext.h	2016-06-02 04:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Photos.framework/Headers/PHLivePhotoEditingContext.h	2016-06-27 04:20:10.000000000 +0200
@@ -66,7 +66,7 @@
 - (void)saveLivePhotoToOutput:(PHContentEditingOutput *)output options:(nullable NSDictionary<PHLivePhotoEditingOption, id> *)options completionHandler:(void(^)(BOOL success, NSError * _Nullable error))handler;
 
 /// Cancel the current asynchronous operation
-/// This is implicitely called whenever prepare or save is called
+/// This is implicitly called whenever prepare or save is called
 /// A canceled operation will call its completion handler with an appropriate error code of PHLivePhotoEditingErrorCodeAborted
 - (void)cancel;
 

```