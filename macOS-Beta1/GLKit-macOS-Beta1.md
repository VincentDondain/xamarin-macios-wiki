#GLKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKMathUtils.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKMathUtils.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKMathUtils.h	2015-08-27 04:21:11.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKMathUtils.h	2016-06-03 05:29:35.000000000 +0200
@@ -26,7 +26,7 @@
 GLK_INLINE float GLKMathRadiansToDegrees(float radians) { return radians * (180 / M_PI); };
     
 GLKVector3 GLKMathProject(GLKVector3 object, GLKMatrix4 model, GLKMatrix4 projection, int *viewport);
-GLKVector3 GLKMathUnproject(GLKVector3 window, GLKMatrix4 model, GLKMatrix4 projection, int *viewport, bool *success);
+GLKVector3 GLKMathUnproject(GLKVector3 window, GLKMatrix4 model, GLKMatrix4 projection, int *viewport, bool  * __nullable success);
 
 #ifdef __OBJC__
 NSString * NSStringFromGLKMatrix2(GLKMatrix2 matrix);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKMatrix3.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKMatrix3.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKMatrix3.h	2015-08-27 04:21:11.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKMatrix3.h	2016-06-03 05:29:35.000000000 +0200
@@ -101,7 +101,7 @@
 
 GLK_INLINE GLKVector3 GLKMatrix3MultiplyVector3(GLKMatrix3 matrixLeft, GLKVector3 vectorRight);
 
-GLK_INLINE void GLKMatrix3MultiplyVector3Array(GLKMatrix3 matrix, GLKVector3 *vectors, size_t vectorCount);
+GLK_INLINE void GLKMatrix3MultiplyVector3Array(GLKMatrix3 matrix, GLKVector3 *__nonnull vectors, size_t vectorCount);
 
 #pragma mark -
 #pragma mark Implementations
@@ -483,7 +483,7 @@
     return v;
 }
 
-GLK_INLINE void GLKMatrix3MultiplyVector3Array(GLKMatrix3 matrix, GLKVector3 *vectors, size_t vectorCount)
+GLK_INLINE void GLKMatrix3MultiplyVector3Array(GLKMatrix3 matrix, GLKVector3 *__nonnull vectors, size_t vectorCount)
 {
     int i;
     for (i=0; i < vectorCount; i++)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKMatrix4.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKMatrix4.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKMatrix4.h	2015-08-27 04:21:11.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKMatrix4.h	2016-06-03 05:29:35.000000000 +0200
@@ -13,6 +13,7 @@
 #include <math.h>
 
 
+
 #include <GLKit/GLKMathTypes.h>
 #include <GLKit/GLKVector3.h>
 #include <GLKit/GLKVector4.h>
@@ -142,8 +143,8 @@
     
 GLK_INLINE GLKMatrix4 GLKMatrix4Transpose(GLKMatrix4 matrix);
     
-GLKMatrix4 GLKMatrix4Invert(GLKMatrix4 matrix, bool *isInvertible);
-GLKMatrix4 GLKMatrix4InvertAndTranspose(GLKMatrix4 matrix, bool *isInvertible);
+GLKMatrix4 GLKMatrix4Invert(GLKMatrix4 matrix, bool * __nullable isInvertible);
+GLKMatrix4 GLKMatrix4InvertAndTranspose(GLKMatrix4 matrix, bool * __nullable isInvertible);
 
 GLK_INLINE GLKMatrix4 GLKMatrix4Multiply(GLKMatrix4 matrixLeft, GLKMatrix4 matrixRight);
 
@@ -191,19 +192,19 @@
 /*
  Assumes 0 in the w component.
  */
-GLK_INLINE void GLKMatrix4MultiplyVector3Array(GLKMatrix4 matrix, GLKVector3 *vectors, size_t vectorCount);
+GLK_INLINE void GLKMatrix4MultiplyVector3Array(GLKMatrix4 matrix, GLKVector3 *__nonnull vectors, size_t vectorCount);
 /*
  Assumes 1 in the w component.
  */
-GLK_INLINE void GLKMatrix4MultiplyVector3ArrayWithTranslation(GLKMatrix4 matrix, GLKVector3 *vectors, size_t vectorCount);
+GLK_INLINE void GLKMatrix4MultiplyVector3ArrayWithTranslation(GLKMatrix4 matrix, GLKVector3 *__nonnull vectors, size_t vectorCount);
 /*
  Assumes 1 in the w component and divides the resulting vector by w before returning.
  */
-GLK_INLINE void GLKMatrix4MultiplyAndProjectVector3Array(GLKMatrix4 matrix, GLKVector3 *vectors, size_t vectorCount);
+GLK_INLINE void GLKMatrix4MultiplyAndProjectVector3Array(GLKMatrix4 matrix, GLKVector3 *__nonnull vectors, size_t vectorCount);
     
 GLK_INLINE GLKVector4 GLKMatrix4MultiplyVector4(GLKMatrix4 matrixLeft, GLKVector4 vectorRight);
 
-GLK_INLINE void GLKMatrix4MultiplyVector4Array(GLKMatrix4 matrix, GLKVector4 *vectors, size_t vectorCount);
+GLK_INLINE void GLKMatrix4MultiplyVector4Array(GLKMatrix4 matrix, GLKVector4 *__nonnull vectors, size_t vectorCount);
 
 #pragma mark -
 #pragma mark Implementations
@@ -834,21 +835,21 @@
     return GLKVector3MultiplyScalar(GLKVector3Make(v4.v[0], v4.v[1], v4.v[2]), 1.0f / v4.v[3]);
 }
 
-GLK_INLINE void GLKMatrix4MultiplyVector3Array(GLKMatrix4 matrix, GLKVector3 *vectors, size_t vectorCount)
+GLK_INLINE void GLKMatrix4MultiplyVector3Array(GLKMatrix4 matrix, GLKVector3 *__nonnull vectors, size_t vectorCount)
 {
     int i;
     for (i=0; i < vectorCount; i++)
         vectors[i] = GLKMatrix4MultiplyVector3(matrix, vectors[i]);
 }
 
-GLK_INLINE void GLKMatrix4MultiplyVector3ArrayWithTranslation(GLKMatrix4 matrix, GLKVector3 *vectors, size_t vectorCount)
+GLK_INLINE void GLKMatrix4MultiplyVector3ArrayWithTranslation(GLKMatrix4 matrix, GLKVector3 *__nonnull vectors, size_t vectorCount)
 {
     int i;
     for (i=0; i < vectorCount; i++)
         vectors[i] = GLKMatrix4MultiplyVector3WithTranslation(matrix, vectors[i]);
 }
     
-GLK_INLINE void GLKMatrix4MultiplyAndProjectVector3Array(GLKMatrix4 matrix, GLKVector3 *vectors, size_t vectorCount)
+GLK_INLINE void GLKMatrix4MultiplyAndProjectVector3Array(GLKMatrix4 matrix, GLKVector3 *__nonnull vectors, size_t vectorCount)
 {
     int i;
     for (i=0; i < vectorCount; i++)
@@ -877,7 +878,7 @@
 #endif
 }
 
-GLK_INLINE void GLKMatrix4MultiplyVector4Array(GLKMatrix4 matrix, GLKVector4 *vectors, size_t vectorCount)
+GLK_INLINE void GLKMatrix4MultiplyVector4Array(GLKMatrix4 matrix, GLKVector4 *__nonnull vectors, size_t vectorCount)
 {
     int i;
     for (i=0; i < vectorCount; i++)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKQuaternion.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKQuaternion.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKQuaternion.h	2015-08-27 04:21:11.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKQuaternion.h	2016-06-03 05:29:35.000000000 +0200
@@ -76,13 +76,13 @@
 GLK_INLINE GLKQuaternion GLKQuaternionNormalize(GLKQuaternion quaternion);
 
 GLK_INLINE GLKVector3 GLKQuaternionRotateVector3(GLKQuaternion quaternion, GLKVector3 vector);
-void GLKQuaternionRotateVector3Array(GLKQuaternion quaternion, GLKVector3 *vectors, size_t vectorCount);
+void GLKQuaternionRotateVector3Array(GLKQuaternion quaternion, GLKVector3 *__nonnull vectors, size_t vectorCount);
     
 /*
  The fourth component of the vector is ignored when calculating the rotation.
  */
 GLK_INLINE GLKVector4 GLKQuaternionRotateVector4(GLKQuaternion quaternion, GLKVector4 vector);
-void GLKQuaternionRotateVector4Array(GLKQuaternion quaternion, GLKVector4 *vectors, size_t vectorCount);
+void GLKQuaternionRotateVector4Array(GLKQuaternion quaternion, GLKVector4 *__nonnull vectors, size_t vectorCount);
     
 #pragma mark -
 #pragma mark Implementations
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKTextureLoader.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKTextureLoader.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKTextureLoader.h	2015-08-27 04:21:11.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKTextureLoader.h	2016-05-21 09:05:55.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKVector2.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKVector2.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKVector2.h	2015-08-27 04:21:11.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKVector2.h	2016-06-03 05:29:35.000000000 +0200
@@ -256,110 +256,56 @@
    
 GLK_INLINE bool GLKVector2AllEqualToVector2(GLKVector2 vectorLeft, GLKVector2 vectorRight)
 {
-#if defined(__ARM_NEON_)
-    float32x2_t v1 = *(float32x2_t *)&vectorLeft;
-    float32x2_t v2 = *(float32x2_t *)&vectorRight;
-    uint32x2_t vCmp = vceq_f32(v1, v2);
-    uint32x2_t vAnd = vand_u32(vCmp, vext_u32(vCmp, vCmp, 1));
-    vAnd = vand_u32(vAnd, vdup_n_u32(1));
-    return (bool)vget_lane_u32(vAnd, 0);
-#else
     bool compare = false;
     if (vectorLeft.v[0] == vectorRight.v[0] &&
         vectorLeft.v[1] == vectorRight.v[1])
         compare = true;
     return compare;
-#endif
 }
 
 GLK_INLINE bool GLKVector2AllEqualToScalar(GLKVector2 vector, float value)
 {
-#if defined(__ARM_NEON_)
-    float32x2_t v1 = *(float32x2_t *)&vector;
-    float32x2_t v2 = vdup_n_f32(value);
-    uint32x2_t vCmp = vceq_f32(v1, v2);
-    uint32x2_t vAnd = vand_u32(vCmp, vext_u32(vCmp, vCmp, 1));
-    vAnd = vand_u32(vAnd, vdup_n_u32(1));
-    return (bool)vget_lane_u32(vAnd, 0);
-#else
     bool compare = false;
     if (vector.v[0] == value &&
         vector.v[1] == value)
         compare = true;
     return compare;
-#endif
 }
 
 GLK_INLINE bool GLKVector2AllGreaterThanVector2(GLKVector2 vectorLeft, GLKVector2 vectorRight)
 {
-#if defined(__ARM_NEON_)
-    float32x2_t v1 = *(float32x2_t *)&vectorLeft;
-    float32x2_t v2 = *(float32x2_t *)&vectorRight;
-    uint32x2_t vCmp = vcgt_f32(v1, v2);
-    uint32x2_t vAnd = vand_u32(vCmp, vext_u32(vCmp, vCmp, 1));
-    vAnd = vand_u32(vAnd, vdup_n_u32(1));
-    return (bool)vget_lane_u32(vAnd, 0);
-#else
     bool compare = false;
     if (vectorLeft.v[0] > vectorRight.v[0] &&
         vectorLeft.v[1] > vectorRight.v[1])
         compare = true;
     return compare;
-#endif
 }
 
 GLK_INLINE bool GLKVector2AllGreaterThanScalar(GLKVector2 vector, float value)
 {
-#if defined(__ARM_NEON_)
-    float32x2_t v1 = *(float32x2_t *)&vector;
-    float32x2_t v2 = vdup_n_f32(value);
-    uint32x2_t vCmp = vcgt_f32(v1, v2);
-    uint32x2_t vAnd = vand_u32(vCmp, vext_u32(vCmp, vCmp, 1));
-    vAnd = vand_u32(vAnd, vdup_n_u32(1));
-    return (bool)vget_lane_u32(vAnd, 0);
-#else
     bool compare = false;
     if (vector.v[0] > value &&
         vector.v[1] > value)
         compare = true;
     return compare;
-#endif
 }
 
 GLK_INLINE bool GLKVector2AllGreaterThanOrEqualToVector2(GLKVector2 vectorLeft, GLKVector2 vectorRight)
 {
-#if defined(__ARM_NEON_)
-    float32x2_t v1 = *(float32x2_t *)&vectorLeft;
-    float32x2_t v2 = *(float32x2_t *)&vectorRight;
-    uint32x2_t vCmp = vcge_f32(v1, v2);
-    uint32x2_t vAnd = vand_u32(vCmp, vext_u32(vCmp, vCmp, 1));
-    vAnd = vand_u32(vAnd, vdup_n_u32(1));
-    return (bool)vget_lane_u32(vAnd, 0);
-#else
     bool compare = false;
     if (vectorLeft.v[0] >= vectorRight.v[0] &&
         vectorLeft.v[1] >= vectorRight.v[1])
         compare = true;
     return compare;
-#endif
 }
 
 GLK_INLINE bool GLKVector2AllGreaterThanOrEqualToScalar(GLKVector2 vector, float value)
 {
-#if defined(__ARM_NEON_)
-    float32x2_t v1 = *(float32x2_t *)&vector;
-    float32x2_t v2 = vdup_n_f32(value);
-    uint32x2_t vCmp = vcge_f32(v1, v2);
-    uint32x2_t vAnd = vand_u32(vCmp, vext_u32(vCmp, vCmp, 1));
-    vAnd = vand_u32(vAnd, vdup_n_u32(1));
-    return (bool)vget_lane_u32(vAnd, 0);
-#else
     bool compare = false;
     if (vector.v[0] >= value &&
         vector.v[1] >= value)
         compare = true;
     return compare;
-#endif
 }
     
 GLK_INLINE GLKVector2 GLKVector2Normalize(GLKVector2 vector)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKVector4.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKVector4.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKVector4.h	2015-08-27 04:21:11.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/GLKit.framework/Headers/GLKVector4.h	2016-06-03 05:29:35.000000000 +0200
@@ -281,15 +281,7 @@
    
 GLK_INLINE bool GLKVector4AllEqualToVector4(GLKVector4 vectorLeft, GLKVector4 vectorRight)
 {
-#if defined(__ARM_NEON_)
-    float32x4_t v1 = *(float32x4_t *)&vectorLeft;
-    float32x4_t v2 = *(float32x4_t *)&vectorRight;
-    uint32x4_t vCmp = vceqq_f32(v1, v2);
-    uint32x2_t vAnd = vand_u32(vget_low_u32(vCmp), vget_high_u32(vCmp));
-    vAnd = vand_u32(vAnd, vext_u32(vAnd, vAnd, 1));
-    vAnd = vand_u32(vAnd, vdup_n_u32(1));
-    return (bool)vget_lane_u32(vAnd, 0);
-#elif defined(GLK_SSE3_INTRINSICS)
+#if   defined(GLK_SSE3_INTRINSICS)
     return _mm_movemask_ps(_mm_cmpeq_ps(_mm_load_ps(&vectorLeft.v[0]), _mm_load_ps(&vectorRight.v[0]))) == 0xF;
 #else
     bool compare = false;
@@ -304,15 +296,7 @@
 
 GLK_INLINE bool GLKVector4AllEqualToScalar(GLKVector4 vector, float value)
 {
-#if defined(__ARM_NEON_)
-    float32x4_t v1 = *(float32x4_t *)&vector;
-    float32x4_t v2 = vdupq_n_f32(value);
-    uint32x4_t vCmp = vceqq_f32(v1, v2);
-    uint32x2_t vAnd = vand_u32(vget_low_u32(vCmp), vget_high_u32(vCmp));
-    vAnd = vand_u32(vAnd, vext_u32(vAnd, vAnd, 1));
-    vAnd = vand_u32(vAnd, vdup_n_u32(1));
-    return (bool)vget_lane_u32(vAnd, 0);
-#elif defined(GLK_SSE3_INTRINSICS)
+#if   defined(GLK_SSE3_INTRINSICS)
     return _mm_movemask_ps(_mm_cmpeq_ps(_mm_load_ps(&vector.v[0]), _mm_set1_ps(value))) == 0xF;
 #else
     bool compare = false;
@@ -327,15 +311,7 @@
 
 GLK_INLINE bool GLKVector4AllGreaterThanVector4(GLKVector4 vectorLeft, GLKVector4 vectorRight)
 {
-#if defined(__ARM_NEON_)
-    float32x4_t v1 = *(float32x4_t *)&vectorLeft;
-    float32x4_t v2 = *(float32x4_t *)&vectorRight;
-    uint32x4_t vCmp = vcgtq_f32(v1, v2);
-    uint32x2_t vAnd = vand_u32(vget_low_u32(vCmp), vget_high_u32(vCmp));
-    vAnd = vand_u32(vAnd, vext_u32(vAnd, vAnd, 1));
-    vAnd = vand_u32(vAnd, vdup_n_u32(1));
-    return (bool)vget_lane_u32(vAnd, 0);
-#elif defined(GLK_SSE3_INTRINSICS)
+#if   defined(GLK_SSE3_INTRINSICS)
     return _mm_movemask_ps(_mm_cmpgt_ps(_mm_load_ps(&vectorLeft.v[0]), _mm_load_ps(&vectorRight.v[0]))) == 0xF;
 #else
     bool compare = false;
@@ -350,15 +326,7 @@
     
 GLK_INLINE bool GLKVector4AllGreaterThanScalar(GLKVector4 vector, float value)
 {
-#if defined(__ARM_NEON_)
-    float32x4_t v1 = *(float32x4_t *)&vector;
-    float32x4_t v2 = vdupq_n_f32(value);
-    uint32x4_t vCmp = vcgtq_f32(v1, v2);
-    uint32x2_t vAnd = vand_u32(vget_low_u32(vCmp), vget_high_u32(vCmp));
-    vAnd = vand_u32(vAnd, vext_u32(vAnd, vAnd, 1));
-    vAnd = vand_u32(vAnd, vdup_n_u32(1));
-    return (bool)vget_lane_u32(vAnd, 0);
-#elif defined(GLK_SSE3_INTRINSICS)
+#if   defined(GLK_SSE3_INTRINSICS)
     return _mm_movemask_ps(_mm_cmpgt_ps(_mm_load_ps(&vector.v[0]), _mm_set1_ps(value))) == 0xF;
 #else
     bool compare = false;
@@ -373,15 +341,7 @@
 
 GLK_INLINE bool GLKVector4AllGreaterThanOrEqualToVector4(GLKVector4 vectorLeft, GLKVector4 vectorRight)
 {
-#if defined(__ARM_NEON_)
-    float32x4_t v1 = *(float32x4_t *)&vectorLeft;
-    float32x4_t v2 = *(float32x4_t *)&vectorRight;
-    uint32x4_t vCmp = vcgeq_f32(v1, v2);
-    uint32x2_t vAnd = vand_u32(vget_low_u32(vCmp), vget_high_u32(vCmp));
-    vAnd = vand_u32(vAnd, vext_u32(vAnd, vAnd, 1));
-    vAnd = vand_u32(vAnd, vdup_n_u32(1));
-    return (bool)vget_lane_u32(vAnd, 0);
-#elif defined(GLK_SSE3_INTRINSICS)
+#if   defined(GLK_SSE3_INTRINSICS)
     return _mm_movemask_ps(_mm_cmpge_ps(_mm_load_ps(&vectorLeft.v[0]), _mm_load_ps(&vectorRight.v[0]))) == 0xF;
 #else
     bool compare = false;
@@ -396,15 +356,7 @@
 
 GLK_INLINE bool GLKVector4AllGreaterThanOrEqualToScalar(GLKVector4 vector, float value)
 {
-#if defined(__ARM_NEON_)
-    float32x4_t v1 = *(float32x4_t *)&vector;
-    float32x4_t v2 = vdupq_n_f32(value);
-    uint32x4_t vCmp = vcgeq_f32(v1, v2);
-    uint32x2_t vAnd = vand_u32(vget_low_u32(vCmp), vget_high_u32(vCmp));
-    vAnd = vand_u32(vAnd, vext_u32(vAnd, vAnd, 1));
-    vAnd = vand_u32(vAnd, vdup_n_u32(1));
-    return (bool)vget_lane_u32(vAnd, 0);
-#elif defined(GLK_SSE3_INTRINSICS)
+#if   defined(GLK_SSE3_INTRINSICS)
     return _mm_movemask_ps(_mm_cmpge_ps(_mm_load_ps(&vector.v[0]), _mm_set1_ps(value))) == 0xF;
 #else
     bool compare = false;

```