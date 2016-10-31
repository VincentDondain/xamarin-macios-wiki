#ModelIO.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMaterial.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMaterial.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMaterial.h	2016-07-31 02:19:10.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMaterial.h	2016-10-23 09:49:56.000000000 +0200
@@ -366,7 +366,11 @@
 - (void)setProperty:(MDLMaterialProperty*)property;
 - (void)removeProperty:(MDLMaterialProperty*)property;
 - (nullable MDLMaterialProperty*)propertyNamed:(NSString*)name;
+// Returns the first occurence of the property that matches the semantic.
+// Not recommended to use when there are multiple properties with same semantic.
 - (nullable MDLMaterialProperty*)propertyWithSemantic:(MDLMaterialSemantic)semantic;
+// Returns the complete list of properties that match the semantic (e.g. Kd & Kd_map)
+- (NSArray<MDLMaterialProperty *> *)propertiesWithSemantic:(MDLMaterialSemantic)semantic;
 - (void)removeAllProperties;
 
 @property (nonatomic, readonly, retain) MDLScatteringFunction *scatteringFunction;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMesh.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMesh.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMesh.h	2016-07-28 23:26:19.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMesh.h	2016-10-23 10:43:26.000000000 +0200
@@ -148,7 +148,7 @@
  @abstract Array of buffers containing vertex data
  @discussion The vertex buffers in this array are indexed by the vertex descriptor.
  */
-@property (nonatomic, readonly, retain) NSArray<id<MDLMeshBuffer>> *vertexBuffers;
+@property (nonatomic, readwrite, retain) NSArray<id<MDLMeshBuffer>> *vertexBuffers;
 
 /*!
  @property submeshes
@@ -434,7 +434,7 @@
 */
 - (instancetype)initCapsuleWithExtent:(vector_float3)extent
                      cylinderSegments:(vector_uint2)segments
-                   hemisphereSegments:(int)hemisphereSegments
+                   hemisphereSegments:(uint32_t)hemisphereSegments
                         inwardNormals:(BOOL)inwardNormals
                          geometryType:(MDLGeometryType)geometryType
                             allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
@@ -539,6 +539,14 @@
                          geometryType:(MDLGeometryType)geometryType
                         inwardNormals:(BOOL)inwardNormals
                             allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
++ (instancetype)newCapsuleWithHeight:(float)height
+                               radii:(vector_float2)radii
+                      radialSegments:(NSUInteger)radialSegments
+                    verticalSegments:(NSUInteger)verticalSegments
+                  hemisphereSegments:(NSUInteger)hemisphereSegments
+                        geometryType:(MDLGeometryType)geometryType
+                       inwardNormals:(BOOL)inwardNormals
+                           allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
 + (instancetype)newEllipticalConeWithHeight:(float)height
                                       radii:(vector_float2)radii
                              radialSegments:(NSUInteger)radialSegments
@@ -552,6 +560,10 @@
                              allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
 + (instancetype)newIcosahedronWithRadius:(float)radius
                            inwardNormals:(BOOL)inwardNormals
+                            geometryType:(MDLGeometryType)geometryType
+                               allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
++ (instancetype)newIcosahedronWithRadius:(float)radius
+                           inwardNormals:(BOOL)inwardNormals
                                allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
 + (nullable instancetype)newSubdividedMesh:(MDLMesh*)mesh
                               submeshIndex:(NSUInteger)submeshIndex
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLObject.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLObject.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLObject.h	2016-09-24 02:51:26.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLObject.h	2016-10-23 09:23:13.000000000 +0200
@@ -76,6 +76,13 @@
  */
 - (MDLObject*)objectAtPath:(NSString*)path;
 
+
+- (void)enumerateChildObjectsOfClass:(Class)objectClass
+                                root:(MDLObject*)root
+                          usingBlock:( void(^)(MDLObject* object, BOOL *stop))block
+                         stopPointer:(BOOL *)stopPointer;
+
+
 /*!
  @property transform
  @abstract Short hand property for the MDLTransformComponent.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLSubmesh.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLSubmesh.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLSubmesh.h	2016-09-24 03:12:04.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLSubmesh.h	2016-10-23 09:23:13.000000000 +0200
@@ -12,10 +12,18 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+@class MDLSubmesh;
+
 NS_CLASS_AVAILABLE(10_11, 9_0)
 MDL_EXPORT
 @interface MDLSubmeshTopology : NSObject
 
+/*! 
+ @method initWithSubmesh:
+ @abstract create a topology object corresponding to the topology in the submesh
+ */
+- (instancetype) initWithSubmesh:(MDLSubmesh*)submesh;
+
 /*!
  @property faceTopologyBuffer
  @abstract A buffer of 8 bit unsigned integer values, where each entry corresponds
@@ -196,7 +204,7 @@
              A submesh of type MDLGeometryTypeVariableTopology with no topology
              data is an empty submesh.
 */
-@property (nonatomic, readonly, retain, nullable) MDLSubmeshTopology *topology;
+@property (nonatomic, retain, nullable) MDLSubmeshTopology *topology;
 
 /*!
  @property name
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTexture.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTexture.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTexture.h	2016-07-28 23:26:19.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTexture.h	2016-10-23 09:49:56.000000000 +0200
@@ -338,6 +338,15 @@
                               channelEncoding:(MDLTextureChannelEncoding)channelEncoding
                                     grayscale:(BOOL)grayscale;
 
+/**
+ Create a texture containing cellular noise. 
+ 
+ @param frequency How large the cells will be
+ */
+- (instancetype)initCellularNoiseWithFrequency:(float)frequency
+                                          name:(nullable NSString*)name
+                             textureDimensions:(vector_int2)textureDimensions
+                               channelEncoding:(MDLTextureChannelEncoding)channelEncoding;
 
 @end
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLVoxelArray.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLVoxelArray.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLVoxelArray.h	2016-07-28 23:26:19.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLVoxelArray.h	2016-10-23 09:23:13.000000000 +0200
@@ -87,7 +87,7 @@
                     divisions:(int)divisions
                interiorShells:(int)interiorShells
                exteriorShells:(int)exteriorShells
-                  patchRadius:(float)patchRadius NS_DEPRECATED(10_11, 10_12, NA, NA);
+                  patchRadius:(float)patchRadius;
 
 /**
  Initialize a voxel grid from an MDLAsset and dilate the resulting voxels by

```