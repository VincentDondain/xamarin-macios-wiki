#GLKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKTextureLoader.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKTextureLoader.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKTextureLoader.h	2015-09-30 23:23:34.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKTextureLoader.h	2016-05-21 09:05:55.000000000 +0200
@@ -124,7 +124,8 @@
     GLKTextureLoaderErrorReorientationFailure = 15,
     GLKTextureLoaderErrorAlphaPremultiplicationFailure = 16,
     GLKTextureLoaderErrorInvalidEAGLContext = 17,
-    GLKTextureLoaderErrorIncompatibleFormatSRGB = 18
+    GLKTextureLoaderErrorIncompatibleFormatSRGB = 18,
+    GLKTextureLoaderErrorUnsupportedTextureTarget = 19,
 } NS_ENUM_AVAILABLE(10_8, 5_0);
 
 #pragma mark -
@@ -162,18 +163,24 @@
     GLenum                      target;
     GLuint                      width;
     GLuint                      height;
+    GLuint                      depth;
     GLKTextureInfoAlphaState    alphaState;
     GLKTextureInfoOrigin        textureOrigin;
     BOOL                        containsMipmaps;
+    GLuint                      mimapLevelCount;
+    GLuint                      arrayLength;
 }
 
 @property (readonly) GLuint                     name;
 @property (readonly) GLenum                     target;
 @property (readonly) GLuint                     width;
 @property (readonly) GLuint                     height;
+@property (readonly) GLuint                     depth;
 @property (readonly) GLKTextureInfoAlphaState   alphaState;
 @property (readonly) GLKTextureInfoOrigin       textureOrigin;
 @property (readonly) BOOL                       containsMipmaps;
+@property (readonly) GLuint                     mimapLevelCount;
+@property (readonly) GLuint                     arrayLength;
 
 @end
 
@@ -205,6 +212,17 @@
                                                 error:(NSError * __nullable * __nullable)outError;           /* Error description. */
 
 /*
+ Synchronously load a named texture asset from a given bundled into an OpenGL texture
+ Returns the generated texture object when the operation is complete, or the operation terminates with an error (returning nil).
+ Returned error can be queried via 'error', which is nil otherwise.
+ */
++ (nullable GLKTextureInfo *)textureWithName:(NSString *)name                                       /* The asset name */
+                                 scaleFactor:(CGFloat)scaleFactor                                   /* scale factor of asset to be retrieved */
+                                      bundle:(nullable NSBundle*)bundle                             /* The bundle where the named texture is located */
+                                     options:(nullable NSDictionary<NSString*, NSNumber*> *)options /* Options that control how the image is loaded. */
+                                       error:(NSError * __nullable * __nullable)outError;           /* Error description. */
+
+/*
  Synchronously create a texture from data residing in memory.
  Returns the generated texture object when the operation is complete, or the operation terminates with an error (returning nil).
  Returned error can be queried via 'error', which is nil otherwise.
@@ -278,6 +296,17 @@
                completionHandler:(GLKTextureLoaderCallback)block;                       /* Block to be invoked on the above dispatch queue. */
 
 /*
+ Asynchronously load a named texture asset from a given bundled into an OpenGL texture
+ Invokes the block on the provided queue when the operation is complete. If queue is NULL, the main queue will be used.
+ */
+- (void)textureWithName:(NSString *)name                                       /* The asset name */
+            scaleFactor:(CGFloat)scaleFactor                                   /* scale factor of asset to be retrieved */
+                 bundle:(nullable NSBundle*)bundle                             /* The bundle where the named texture is located */
+                options:(nullable NSDictionary<NSString*, NSNumber*> *)options /* Options that control how the image is loaded. */
+                  queue:(nullable dispatch_queue_t)queue                       /* Dispatch queue, or NULL to use the main queue. */
+      completionHandler:(GLKTextureLoaderCallback)block;                       /* Block to be invoked on the above dispatch queue. */
+
+/*
  Asynchronously create a texture from data residing in memory.
  Invokes the block on the provided queue when the operation is complete. If queue is NULL, the main queue will be used.
  */

```