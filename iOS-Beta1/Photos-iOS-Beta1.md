#Photos.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHPhotoLibrary.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHPhotoLibrary.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHPhotoLibrary.h	2016-09-30 07:24:24.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHPhotoLibrary.h	2016-10-25 05:19:39.000000000 +0200
@@ -46,7 +46,8 @@
 // Nesting change requests will throw an exception
 - (void)performChanges:(dispatch_block_t)changeBlock completionHandler:(nullable void(^)(BOOL success, NSError *__nullable error))completionHandler;
 - (BOOL)performChangesAndWait:(dispatch_block_t)changeBlock error:(NSError *__autoreleasing *)error;
-
+- (void)performCancellableChanges:(void(^)(BOOL *cancel))cancellableChangeBlock completionHandler:(nullable void(^)(BOOL success, NSError *__nullable error))completionHandler;
+- (BOOL)performCancellableChangesAndWait:(void(^)(BOOL *cancel))cancellableChangeBlock error:(NSError *__autoreleasing *)error;
 
 #pragma mark - Change Handling
 

```