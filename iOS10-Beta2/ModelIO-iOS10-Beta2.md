#ModelIO.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLAsset.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLAsset.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLAsset.h	2016-05-16 07:44:17.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLAsset.h	2016-06-26 08:24:46.000000000 +0200
@@ -20,11 +20,9 @@
  
  @abstract An MDLAsset represents the contents of a model file.
  
- @discussion
-
- Each asset contains a collection of hierarchies of objects, where each object 
- in the asset is the top level of a hierarchy. Objects include transforms, 
- lights, cameras, and meshes.
+ @discussion Each asset contains a collection of hierarchies of objects, where 
+             each object in the asset is the top level of a hierarchy. Objects 
+             include transforms, lights, cameras, and meshes.
  
  MDLAssets are typically instantiated from NSURLs that refer to a model resource.
 
@@ -117,7 +115,7 @@
  @abstract Export an asset to the specified URL.
  @return YES is returned if exporting proceeded successfully,
  */
-- (BOOL)exportAssetToURL:(NSURL *)URL;
+- (BOOL)exportAssetToURL:(NSURL *)URL NS_SWIFT_UNAVAILABLE("Use exportAssetToURL:error");
 
 /*!
  @method exportAssetToURL:error:
@@ -247,6 +245,15 @@
  */
 - (MDLObject *)objectAtIndex:(NSUInteger)index;
 
+/*!
+ @property masters
+ @abstract Master objects that can be instanced into the asset's object hierarchy
+ 
+ @see MDLObjectContainerComponent
+ */
+@property (nonatomic, retain) id<MDLObjectContainerComponent> masters;
+
+
 @end
 
 @protocol MDLLightProbeIrradianceDataSource <NSObject>
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLCamera.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLCamera.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLCamera.h	2016-05-16 07:44:17.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLCamera.h	2016-06-26 08:32:34.000000000 +0200
@@ -17,18 +17,15 @@
  
  @summary MDLCamera models a physically plausible camera.
  
- @discussion
-
- Note that values are represented as float in MDLCamera as it offers sufficient 
- precision, and because calculations will be identical on any processor 
+ @discussion Values are represented as float in MDLCamera as it offers sufficient 
+ precision, and because calculations will be identical on any processor
  architecture. This consistency is a requirement of the model.
 
  MDLCamera provides the a model of the parameters governing the physical process 
  of transforming a scene into an image.
 
- This process is modeled as a series of steps, each governed by physically 
- plausible properties.
- 
+ This process is modeled as a series of steps, each governed by the physical
+ properties of real world cameras.
  
  1. The position and orientation of the camera
     @see MDLObject transform property
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLLight.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLLight.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLLight.h	2016-05-18 04:40:09.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLLight.h	2016-06-26 09:18:51.000000000 +0200
@@ -36,11 +36,14 @@
 
 /** A utility function that returns the irradiance from the light at a given point.
     @discussion point is world space
+    @property colorSpace name, as defined in CGColorSpace.h. Default is 
+              kCGColorSpaceSRGB
   */
 - (CGColorRef)irradianceAtPoint:(vector_float3)point;
 - (CGColorRef)irradianceAtPoint:(vector_float3)point colorSpace:(CGColorSpaceRef)colorSpace;
 
 @property (nonatomic, readwrite) MDLLightType lightType;
+@property (nonatomic, copy, readwrite) NSString *colorSpace;
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMesh.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMesh.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMesh.h	2016-05-16 07:44:17.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMesh.h	2016-06-26 08:32:34.000000000 +0200
@@ -18,16 +18,18 @@
  @class MDLVertexAttributeData
  @abstract convenience object to quickly access vertex attribute data
  @discussion created by MDLMesh's vertexAttributeData selector
+             Setting values on this object has no effect on the
+             underlying objects.
  */
 
 NS_CLASS_AVAILABLE(10_11, 9_0)
 MDL_EXPORT
 @interface MDLVertexAttributeData : NSObject
 
-@property (nonatomic, retain, readonly) MDLMeshBufferMap *map;
-@property (nonatomic, readonly) void *dataStart;
-@property (nonatomic, readonly) NSUInteger stride;
-@property (nonatomic, readonly) MDLVertexFormat format;
+@property (nonatomic, retain) MDLMeshBufferMap *map;
+@property (nonatomic) void *dataStart;
+@property (nonatomic) NSUInteger stride;
+@property (nonatomic) MDLVertexFormat format;
 
 @end
 
@@ -73,8 +75,6 @@
  @return Initialized mesh or nil if descriptor's layout array is incompatible
          with vertexBuffers array
  @param vertexCount Number of vertices in vertexBuffers
- @param vertexBuffer An array of MDLMeshBuffer objects containing vertex data
-         for the mesh
  @param descriptor VertexDescriptor specifying how to interpret vertex data
  @param submeshes Array of submeshes with index buffers referencing vertex data
         and/or materials to be applied to mesh
@@ -180,13 +180,13 @@
 /*!
  @method addAttributeWithName:format:type:data:stride
  @abstract Create a new vertex attribute including an associated buffer with
- a copy of the supplied data, and update the vertex descriptor accordingly
+           a copy of the supplied data, and update the vertex descriptor accordingly
  @param name The name the attribute can be found by
  @param format Format of the data, such as MDLVertexFormatFloat3
  @param type The usage of the attribute, such as MDLVertexAttributePosition
  @param data Object containing the data to be used in the new vertex buffer
  @param stride The increment in bytes from the start of one data entry to
- the next.
+        the next.
  */
 -(void)addAttributeWithName:(NSString *)name
                      format:(MDLVertexFormat)format
@@ -195,6 +195,29 @@
                      stride:(NSInteger)stride;
 
 /*!
+ @method addAttributeWithName:format:type:data:stride:time
+ @abstract Create a new vertex attribute including an associated buffer with
+           a copy of the supplied data, and update the vertex descriptor accordingly
+ @param name The name the attribute can be found by
+ @param format Format of the data, such as MDLVertexFormatFloat3
+ @param type The usage of the attribute, such as MDLVertexAttributePosition
+ @param data Object containing the data to be used in the new vertex buffer
+ @param stride The increment in bytes from the start of one data entry to
+        the next.
+ @param time The time the attribute is to be invoked at.
+ @discussion Adding an attribute, such as position data, at multiple times will
+             result in attributes being created for each of those times.
+             Attributes corresponding to multiple times can be retrieved from
+             the vertex descriptor.
+ */
+-(void)addAttributeWithName:(NSString *)name
+                     format:(MDLVertexFormat)format
+                       type:(NSString *)type
+                       data:(NSData *)data
+                     stride:(NSInteger)stride
+                       time:(NSTimeInterval)time;
+
+/*!
  @method addNormalsWithAttributeNamed:creaseThreshold:
  @abstract Calculate and add vertex normal data
  @param attributeName Name of vertex normal attribute.  If nil, vertex normals
@@ -216,7 +239,7 @@
  @method addTangentBasisForTextureCoordinateAttributeNamed:tangentAttributeNamed:bitangentAttributeNamed
  @abstract Create tangent basis data
  @param textureCoordinateAttributeName texture coordinates to use in calculations
- @param tangentAttributeName Name of vertex tangent attribute.
+ @param tangentAttributeNamed Name of vertex tangent attribute.
  @param bitangentAttributeNamed Name of vertex bitangent attribute.
  @discussion Uses the attribute named MDLVertexAttributePosition and
              textureCoordinateAttributeName to calculate tangent and bitangent
@@ -224,7 +247,7 @@
              the new attributes if necessary.
  */
 - (void)addTangentBasisForTextureCoordinateAttributeNamed:(NSString*)textureCoordinateAttributeName
-                                    tangentAttributeNamed:(NSString *)tangentAttributeName
+                                    tangentAttributeNamed:(NSString *)tangentAttributeNamed
                                   bitangentAttributeNamed:(nullable NSString *)bitangentAttributeName;
 
 /*!
@@ -241,8 +264,8 @@
              tangent by B = (N x T) * T.w
  */
 - (void)addTangentBasisForTextureCoordinateAttributeNamed:(NSString*)textureCoordinateAttributeName
-                                     normalAttributeNamed:(NSString*)normalAttributeName
-                                    tangentAttributeNamed:(NSString *)tangentAttributeName;
+                                     normalAttributeNamed:(NSString*)normalAttributeNamed
+                                    tangentAttributeNamed:(NSString *)tangentAttributeNamed;
 
 /*!
  @method addTextureCoordinatesForAttributeNamed:textureCoordinateAttributeName
@@ -319,17 +342,12 @@
 
 
 /*!
- @method newEllipsoidWithRadii:radialSegments:verticalSegments:inwardNormals:hemisphere:allocator:
+ @method initSphereWithExtent:segments:inwardNormals:geometryType:allocator
  @abstract Factory method for generating a mesh with an ellipsoid shape
  @return MDLMesh epllipsoid with desired attributes
- @param radii Width, height, and depth of ellipsoid.
- @param radialSegments Number of pie slices :)
- @param verticalSegments Number of slices in the vertical direction
  @param geometryType Must be MDLGeometryTypeTriangles or MDLGeometryTypeLines
  @param inwardNormals If true, generated normals will face inwards. Useful for
         generating a skydome.
- @param geometryType Must be  Must be MDLGeometryTypeTriangles
- @param hemisphere If true, only top half of ellipsoid will be generated. The
         actual nubmer of vertical slices will be half of 'vertical' segments
  @param allocator A mesh buffer allocator used to allocate memory to back buffers
         for the returned mesh.  If nil, a default allocator will be used
@@ -352,13 +370,9 @@
                                allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
 
 /*!
- @method newCylinderWithHeight:
+ @method initCylinderWithExtent:segments:inwardNormals:topCap:bottomCap:geometryType:allocator
  @abstract Factory method for generating a mesh with a cylindrical shape
  @return MDLMesh cylinder with desired attributes
- @param height Height of cylindoid.
- @param radii Radii of cylinder in X and Z directions.
- @param radialSegments Number of pie slices :)
- @param verticalSegments Number of slices along Y axis
  @param geometryType Must be MDLGeometryTypeTriangles or MDLGeometryTypeLines
  @param inwardNormals Normals point toward center of cylinder
  @param allocator A mesh buffer allocator used to allocate memory to back buffers
@@ -391,15 +405,11 @@
                              allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
 
 /*!
- @method newCapsuleWithHeight:
+ @method initCapsuleWithExtent:cylinderSegments:hemisphereSegments:inwardNormals:geometryType:allocator
  @abstract Factory method for generating a mesh with a capsule shape; a cylinder
            with hemispheres for caps.
  @return MDLMesh capsule with desired attributes
- @param height Height of cylindoid.
- @param radii Radii of cylinder in X and Z directions.
- @param radialSegments Number of pie slices :)
- @param verticalSegments Number of slices along Y axis
- @param hemisphereSegments Number of slices through hemisphere caps along Y axis 
+ @param hemisphereSegments Number of slices through hemisphere caps along Y axis
  @param geometryType Must be MDLGeometryTypeTriangles or MDLGeometryTypeLines
  @param inwardNormals Normals point toward center of cylinder
  @param allocator A mesh buffer allocator used to allocate memory to back buffers
@@ -430,14 +440,9 @@
                             allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
 
 /*!
- @method newEllipticalConeWithHeight:radii:radialSegments:verticalSegments:inwardNormals:allocator:
+ @method initConeWithExtent:segments:inwardNormals:cap:geometryType:allocator
  @abstract Factory method for generating a mesh with an ellipticalCone shape.
  @return MDLMesh cone with desired attributes
- @param height Height of ellipticalCone from point to base.
- @param radii Radii of base in X and Z directions.  Values of vector should be
-        equal to create a true cone.
- @param radialSegments Number of pie slices :)
- @param verticalSegments Number of slices along Y axis
  @param geometryType Must be MDLGeometryTypeTriangles or MDLGeometryTypeLines
  @param inwardNormals Normals point toward center of ellipticalCone
  @param allocator A mesh buffer allocator used to allocate memory to back buffers
@@ -464,7 +469,7 @@
                          allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
 
 /*!
- @method newPlaneWithDimensions:segments:geometryType:allocator:
+ @method initPlaneWithExtent:segments:geometryType:allocator
  @abstract Factory method for generating a mesh with an planar shape
  @return MDLMesh plane with desired attributes
  @param extent extent of the plane
@@ -481,10 +486,9 @@
                           allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
 
 /*!
- @method newIcosahedronWithRadius:inwardNormals:allocator:
+ @method initIcosahedronWithExtent:inwardNormals:geometryType:allocator
  @abstract Factory method for generating a mesh icosahedron
  @return MDLMesh icosahedron with desired attributes
- @param radius Distance from the center to the outermost point of the mesh
  @param inwardNormals Generated normals will face towards the center of the mesh
  @param allocator A mesh buffer allocator used to allocate memory to back buffers
         for the returned mesh.  If nil, a default allocator will be used
@@ -496,7 +500,7 @@
                                 allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
 
 /*!
- @method newSubdividedMesh:subdivisionLevels:allocator:
+ @method initMeshBySubdividingMesh:submeshIndex:subdivisionLevels:allocator
  @abstract Factory method that generates a subdivided mesh from a source mesh
  @param mesh Mesh from which to generate a subdivided mesh
  @param submeshIndex Index of submesh in Mesh's submesh array from which to
@@ -555,20 +559,6 @@
 
 @end
 
-/*!
- @interface MDLAnimationRig
- @abstract Animation control rig for use when vertex attributes of joint indices
-           and weights exist.
- */
-
-@interface MDLMesh (MDLAnimationRig)
-
-@property (readonly, nonatomic) NSUInteger controlNodeCount;
-- (MDLObject *) controlNodeForIndex:(NSUInteger)index;
-- (matrix_float4x4) inverseBasePoseForIndex:(NSUInteger)index;
-
-@end
-
 
 @interface MDLMesh (MDLLightBaking)
 
@@ -576,7 +566,7 @@
  @method generateAmbientOcclusionTextureWithSize:
  @abstract Creates an Ambient Occlusion texture, returns true upon success, false
            upon failure
- @param size  Texture Size in which to bake the ambient occlusion
+ @param textureSize Texture Size in which to bake the ambient occlusion
  @param raysPerSample Number of rays to be sent out of every texture texel against
         the object for potential occlusion.
  @param attenuationFactor Float between 0 to 1 that defines how to attenuate the
@@ -601,7 +591,7 @@
  @method generateAmbientOcclusionTextureWithQuality:
  @abstract Creates an Ambient Occlusion texture, returns true upon success, false
            upon failure
- @param quality Float between 0 and 1 that defines quality of the bake process.
+ @param bakeQuality Float between 0 and 1 that defines quality of the bake process.
         0 is of lower quality but bakes faster and uses less memory, where 1 is
         of higher quality.
  @param attenuationFactor Float between 0 to 1 that defines how to attenuate the
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMeshBuffer.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMeshBuffer.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMeshBuffer.h	2016-05-04 00:21:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMeshBuffer.h	2016-06-26 08:21:25.000000000 +0200
@@ -225,7 +225,6 @@
  @return An object conforming to the MDLMeshBuffer protocol.  Returns nil the 
          buffer could not be allocated in the zone given.
  @param zone Zone from which to allocate the memory
- @param data Values with which to fill the buffer
  @param type Type of data to be stored in this buffer
  @discussion An implementing MDLMeshBufferAllocator object may increase the size 
              of the zone if the buffer could not be allocated with the current 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLObject.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLObject.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLObject.h	2016-05-16 08:40:26.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLObject.h	2016-06-26 08:32:34.000000000 +0200
@@ -46,6 +46,21 @@
 @property (nonatomic, weak, nullable) MDLObject* parent;
 
 /*!
+ @property instance
+ @abstract Instance object
+ @discussion nil, unless this object refers to master data to be instanced. The
+             master data object can be any MDLObject that does not have a parent.
+             If an MDLAsset has been created from a data file, any master objects
+             parsed from that file will be found in the masters property.
+             A typical use of a master and instance might be to have one master
+             chair MDLObject, and instance six chairs around a table. The
+             transform of each chair would be found on the parent MDLObject, but
+             the various items making up the chair would be found in the master
+             object.
+ */
+@property (nonatomic, nullable, retain) MDLObject* instance;
+
+/*!
  @property path
  @abstract a string representing a path to the object
  @discussion a path is of the form /path/to/object where the path is formed by
@@ -57,14 +72,14 @@
 @property (nonatomic, readonly) NSString* path;
 
 /*!
+ @abstract Return the object at the specified path, or nil if none exists there
+ */
+- (MDLObject*)objectAtPath:(NSString*)path;
+
+/*!
  @property transform
  @abstract Short hand property for the MDLTransformComponent.
- @discussion 
- 
- The default value is nil
-
- Getter is equivalent to "-[componentConformingToProtocol:@protocol(MDLTransformComponent)]"
- Setter is equivalent to "-[setComponent:forProtocol:@protocol(MDLTransformComponent)]"
+ @discussion The default value is nil
  
  @see MDLTransformComponent
  */
@@ -73,17 +88,21 @@
 /*!
  @property children
  @abstract Short hand property for the MDLObjectContainerComponent.
- @discussion
-  The default value is nil
- 
- Getter is equivalent to "-[componentConformingToProtocol:@protocol(MDLObjectContainerComponent)]"
- Setter is equivalent to "-[setComponent:forProtocol:@protocol(MDLObjectContainerComponent)]"
+ @discussion The default value is nil
  
  @see MDLObjectContainerComponent
  */
 @property (nonatomic, retain) id<MDLObjectContainerComponent> children;
 
 /*!
+ @property hidden
+ @abstract Visibility of the node
+ @discussion default is NO
+ */
+
+@property (nonatomic) BOOL hidden;
+
+/*!
  @method addChild:
  @abstract Short hand for adding a child to the current container component and 
            setting the parent to this object.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTexture.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTexture.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTexture.h	2016-05-16 05:38:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTexture.h	2016-06-26 08:21:25.000000000 +0200
@@ -99,7 +99,8 @@
     orientation and demosaiced in all other instances.
  */
 + (nullable instancetype)textureCubeWithImagesNamed:(NSArray<NSString *> *)names;
-+ (nullable instancetype)textureCubeWithImagesNamed:(NSArray<NSString *> *)names bundle:(nullable NSBundle*)bundleOrNil;
++ (nullable instancetype)textureCubeWithImagesNamed:(NSArray<NSString *> *)names
+                                             bundle:(nullable NSBundle*)bundleOrNil;
 
 + (instancetype)irradianceTextureCubeWithTexture:(MDLTexture*)texture
                                             name:(nullable NSString*)name
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTypes.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTypes.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTypes.h	2016-05-16 08:40:26.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTypes.h	2016-06-26 09:39:44.000000000 +0200
@@ -28,9 +28,6 @@
 /* Universal Scene Description file format, file extension USDA or USDB, UTI com.pixar.universal-scene-description */
 MDL_EXPORT NSString * __nonnull const kUTTypeUniversalSceneDescription NS_AVAILABLE(10_12, 10_0);
 
-/* MDLTexture can export OpenEXR files. The correct file format extension is EXR, and
-   the UTI is com.ilm.openexr-image */
-
 NS_ASSUME_NONNULL_BEGIN
 typedef NS_ENUM(NSUInteger, MDLIndexBitDepth)
 {
@@ -49,12 +46,7 @@
     MDLGeometryTypeTriangles,
     MDLGeometryTypeTriangleStrips,
     MDLGeometryTypeQuads,
-    MDLGeometryTypeVariableTopology,
-    MDLGeometryKindPoints = 0,        // Legacy enumerations
-    MDLGeometryKindLines,
-    MDLGeometryKindTriangles,
-    MDLGeometryKindTriangleStrips,
-    MDLGeometryKindQuads
+    MDLGeometryTypeVariableTopology
 };
 
 typedef NS_ENUM(NSInteger, MDLProbePlacement) {
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLVertexDescriptor.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLVertexDescriptor.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLVertexDescriptor.h	2016-05-16 05:38:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLVertexDescriptor.h	2016-06-26 09:39:44.000000000 +0200
@@ -171,6 +171,8 @@
 MDL_EXPORT
 @interface MDLVertexBufferLayout : NSObject <NSCopying>
 
+- (instancetype) initWithStride:(NSUInteger) stride;
+
 /*!
  @property stride
  @abstract stride in bytes of each vertex element of in the buffer
@@ -228,6 +230,13 @@
 @property (nonatomic, readwrite) NSUInteger bufferIndex;
 
 /*!
+ @property time
+ @abstract the time the attribute is intended for.
+ @discussion morph targets would store their times here
+ */
+@property (nonatomic, readwrite) NSTimeInterval time;
+
+/*!
  @property initializationValue
  @abstract Value to initialize the attribute to in the vertex buffer if no values
  @discussion This values of this vector will be set in attribute in the vertex
@@ -246,9 +255,7 @@
 /*!
  @class MDLVertexDescriptor
  @abstract Describes the layout of vertex buffers in MDLMesh objects
- @discussion 
- 
- This object is a property of MDLMesh describing the current state of
+ @discussion This object is a property of MDLMesh describing the current state of
  attributes and buffer layouts of the vertex buffers in the mesh. This must be 
  immutable otherwise even small changes could cause the buffers to be out of sync 
  with the layout described here.
@@ -277,7 +284,7 @@
 
 /*!
  @method addOrReplaceAttribute:
- @abstract Replace any attribute with the same name, or add it if it does not
+ @abstract Replace any attribute with the same name and time, or add it if it does not
            already exist.
  */
 - (void)addOrReplaceAttribute:(nonnull MDLVertexAttribute*)attribute;

```