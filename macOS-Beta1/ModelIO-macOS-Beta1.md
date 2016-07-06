#ModelIO.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLAsset.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLAsset.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLAsset.h	2015-08-23 03:50:33.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLAsset.h	2016-05-16 07:44:17.000000000 +0200
@@ -2,7 +2,7 @@
  @header MDLAsset.h
  @framework ModelIO
  @abstract Structures for representing contents of 3d model files
- @copyright Copyright © 2015 Apple, Inc. All rights reserved.
+ @copyright Copyright © 2016 Apple, Inc. All rights reserved.
  */
 
 #import <ModelIO/ModelIOExports.h>
@@ -12,12 +12,15 @@
 #import <Foundation/NSURL.h>
 #import <simd/simd.h>
 
+@class MDLLightProbe;
+@class MDLTexture;
+
 /*!
  @class MDLAsset
  
  @abstract An MDLAsset represents the contents of a model file.
  
-@discussion
+ @discussion
 
  Each asset contains a collection of hierarchies of objects, where each object 
  in the asset is the top level of a hierarchy. Objects include transforms, 
@@ -81,8 +84,15 @@
            vertexDescriptor:(nullable MDLVertexDescriptor*)vertexDescriptor
             bufferAllocator:(nullable id<MDLMeshBufferAllocator>)bufferAllocator;
 
+/*!
+ @method initWithBufferAllocator:
+ @abstract Initialize an empty MDLAsset with a buffer allocator to be used during
+           other operations.
+ */
+- (instancetype)initWithBufferAllocator:(nullable id<MDLMeshBufferAllocator>)bufferAllocator;
+
 /*! 
- @method initWithURL:vertexDescriptor:bufferAllocator:preserveTopology
+ @method initWithURL:vertexDescriptor:bufferAllocator:preserveTopology:error:
  @abstract Same as initWithURL:vertexDescriptor:bufferAllocator: except that
            if preserveTopology is YES, a topology buffer might be created on the
            submeshes.
@@ -95,7 +105,6 @@
              MDLGeometryTypeVariableTopology, and a faceTopologyBuffer will be
              created.
  */
-
 - (instancetype)initWithURL:(NSURL *)URL
            vertexDescriptor:(nullable MDLVertexDescriptor*)vertexDescriptor
             bufferAllocator:(nullable id<MDLMeshBufferAllocator>)bufferAllocator
@@ -109,6 +118,12 @@
  @return YES is returned if exporting proceeded successfully,
  */
 - (BOOL)exportAssetToURL:(NSURL *)URL;
+
+/*!
+ @method exportAssetToURL:error:
+ @abstract Export an asset to the specified URL.
+ @return YES is returned if exporting proceeded successfully,
+ */
 - (BOOL)exportAssetToURL:(NSURL *)URL error:(NSError * __nullable * __nullable)error;
 
 /*!
@@ -130,13 +145,23 @@
 + (BOOL)canExportFileExtension:(NSString *)extension;
 
 /*!
+ @method childObjectsOfClass:
+ @abstract Inspects an asset's hierarchy for objects of the specified class type
+ @return returns an NSArray of all objects in the asset matching the requested class
+ @discussion This can be used to get references to all MDLMesh objects, MDLLights,
+             etc. if objectClass is not a subclass of MDLObject, an exception will be
+             raised.
+ */
+- (NSArray<MDLObject*>*)childObjectsOfClass:(Class)objectClass;
+
+/*!
  @method boundingBoxAtTime:
  @abstract The bounds of the MDLAsset at the specified time
  */
 - (MDLAxisAlignedBoundingBox)boundingBoxAtTime:(NSTimeInterval)time;
 
 /*!
- @property bounds
+ @property boundingBox
  @abstract The bounds of the MDLAsset at the earliest time sample
  */
 @property (nonatomic, readonly) MDLAxisAlignedBoundingBox boundingBox;
@@ -153,7 +178,9 @@
  @property startTime
  @abstract Start time bracket of animation data
  @discussion If no animation data was specified by resource or resource incapable 
-             of specifying animation data, this value defaults to 0
+             of specifying animation data, this value defaults to 0. If startTime
+             was set explicitly, then the value of startTime will be the lesser
+             of the set value and the animated values.
  */
 @property (nonatomic, readwrite) NSTimeInterval startTime;
 
@@ -161,13 +188,15 @@
  @property endTime
  @abstract End time bracket of animation data
  @discussion If no animation data was specified by resource or resource incapable
-             of specifying animation data, this value defaults to 0
+             of specifying animation data, this value defaults to 0. If the
+             endTime was set explicitly, then the value of endTime will be the
+             greater of the set value and the animated values.
  */
 @property (nonatomic, readwrite) NSTimeInterval endTime;
 
 /*!
  @property URL
- @abstract  URL used to create the asset
+ @abstract URL used to create the asset
  @discussion If no animation data was specified by resource or resource incapable 
              of specifying animation data, this value defaults to 0
  */
@@ -181,7 +210,7 @@
 
 /*!
  @property vertexDescriptor
- @abstract  Vertex descriptor set upon asset initialization
+ @abstract Vertex descriptor set upon asset initialization
  @discussion Will be nil if there was no descriptor set
  */
 @property (nonatomic, readonly, retain, nullable) MDLVertexDescriptor *vertexDescriptor;
@@ -201,7 +230,8 @@
 - (void)removeObject:(MDLObject *)object;
 
 /*!
- The number of top level objects
+ @property count
+ @abstract The number of top level objects
  */
 @property (nonatomic, readonly) NSUInteger count;
 
@@ -219,4 +249,41 @@
 
 @end
 
+@protocol MDLLightProbeIrradianceDataSource <NSObject>
+/**
+ Bounding box of the source scene for which you are adding light probes.
+ */
+@property MDLAxisAlignedBoundingBox boundingBox;
+
+@optional
+/**
+ Spherical harmonics level used to calculate the spherical harmonics coefficients.
+ */
+@property NSUInteger sphericalHarmonicsLevel;
+
+/**
+ Given a position in the source scene, returns the spherical harmonics coefficients
+ at that point.
+ 
+ The data returned is an array of 32-bit floating-point values, containing three non-interleaved 
+ data sets corresponding to the red, green, and blue sets of coefficients. The array’s length is 
+ determined by the sphericalHarmonicsLevel property.
+ */
+-(NSData *)sphericalHarmonicsCoefficientsAtPosition:(vector_float3)position;
+@end
+
+/**
+ Given a light probe density, method places light probes in the scene according to the
+ passed in placement heuristic type. The higher the density, the greater the number of 
+ light probes placed in the scene.
+ 
+ Using the placement heuristic MDLProbePlacementUniformGrid places the light probes in the
+ scene as a uniform grid. The placement heuristic MDLProbePlacementIrradianceDistribution 
+ places the light probes in areas of greatest irradiance change. 
+ */
+@interface MDLAsset (MDLLightBaking)
++ (NSArray<MDLLightProbe *> *)placeLightProbesWithDensity:(float)value heuristic:(MDLProbePlacement)type
+                                usingIrradianceDataSource:(id<MDLLightProbeIrradianceDataSource>)dataSource;
+@end
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLCamera.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLCamera.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLCamera.h	2015-08-23 03:50:33.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLCamera.h	2016-05-16 07:44:17.000000000 +0200
@@ -97,6 +97,8 @@
  
  4. Geometry of the lens
  
+    This is a thin lens model.
+ 
     @property focalLength
  
     The default focal length is 50mm, corresponding to a field of view of 54 
@@ -226,6 +228,13 @@
 
  */
 
+typedef NS_ENUM(NSUInteger, MDLCameraProjection)
+{
+    MDLCameraProjectionPerspective = 0,
+    MDLCameraProjectionOrthographic = 1,
+};
+
+
 NS_CLASS_AVAILABLE(10_11, 9_0)
 MDL_EXPORT
 @interface MDLCamera : MDLObject
@@ -238,6 +247,10 @@
 @property (nonatomic, readonly) matrix_float4x4 projectionMatrix;
 
 /**
+ */
+@property (nonatomic, assign) MDLCameraProjection projection;
+
+/**
  Move the camera back and orient the camera so that a bounding box is framed 
  within the current field of view. Uses the Y axis as up.
  If setNearAndFar is YES, the near and far visibility distances will be set.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLLight.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLLight.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLLight.h	2015-08-23 03:50:33.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLLight.h	2016-05-18 04:40:09.000000000 +0200
@@ -56,13 +56,6 @@
  @property attenuationStartDistance. Within the attenuation start distance, the
            light is maximally bright.
  @property attenuationEndDistance. Beyond this distance, there is no light.
-
- @discussion A good formula to calculate falloff is
- 
-   falloff = clamp((1 - (distance/attenuationStartDistance)^4) ^2), 0, 1) / (distance^2 + 1)
- 
-   Note that adding one to distance in the denominator prevents numerical issues 
-   very close to the light's origin.
  */
 
 NS_CLASS_AVAILABLE(10_11, 9_0)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMaterial.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMaterial.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMaterial.h	2015-08-23 03:50:33.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMaterial.h	2016-05-18 04:40:08.000000000 +0200
@@ -218,7 +218,7 @@
 
 NS_CLASS_AVAILABLE(10_11, 9_0)
 MDL_EXPORT
-@interface MDLMaterialProperty : NSObject<MDLNamed>
+@interface MDLMaterialProperty : NSObject<MDLNamed, NSCopying>
 
 - (instancetype)init NS_UNAVAILABLE;
 
@@ -250,6 +250,60 @@
 @property (nonatomic, assign) vector_float3 float3Value;
 @property (nonatomic, assign) vector_float4 float4Value;
 @property (nonatomic, assign) matrix_float4x4 matrix4x4;
+@property (nonatomic, assign) float luminance;
+
+@end
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
+MDL_EXPORT
+@interface MDLMaterialPropertyConnection : NSObject<MDLNamed>
+
+- (instancetype)init NS_UNAVAILABLE;
+
+/** Connects the output to the input */
+- (instancetype)initWithOutput:(MDLMaterialProperty*)output
+                         input:(MDLMaterialProperty*)input;
+
+@property (nonatomic, weak, readonly) MDLMaterialProperty *output;
+@property (nonatomic, weak, readonly) MDLMaterialProperty *input;
+
+@end
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
+MDL_EXPORT
+@interface MDLMaterialPropertyNode : NSObject<MDLNamed>
+
+- (instancetype)init NS_UNAVAILABLE;
+
+- (instancetype)initWithInputs:(NSArray<MDLMaterialProperty*>*)inputs
+                       outputs:(NSArray<MDLMaterialProperty*>*)outputs
+            evaluationFunction:(void(^)(MDLMaterialPropertyNode*))function;
+
+@property (nonatomic, copy) void(^evaluationFunction)(MDLMaterialPropertyNode*);
+
+@property (nonatomic, readonly) NSArray<MDLMaterialProperty*> *inputs;
+@property (nonatomic, readonly) NSArray<MDLMaterialProperty*> *outputs;
+
+@end
+
+/**
+ @discussion inputs and outputs will contain all of the inputs and outputs
+             external to the graph, which are all the inputs and outputs not
+             internally connected to something
+ */
+NS_CLASS_AVAILABLE(10_12, 10_0)
+MDL_EXPORT
+@interface MDLMaterialPropertyGraph : MDLMaterialPropertyNode
+
+- (instancetype)init NS_UNAVAILABLE;
+
+- (instancetype)initWithNodes:(NSArray<MDLMaterialPropertyNode*>*)nodes
+                  connections:(NSArray<MDLMaterialPropertyConnection*>*)connections;
+
+- (void)evaluate;
+
+@property (nonatomic, readonly) NSArray<MDLMaterialPropertyNode*> *nodes;
+@property (nonatomic, readonly) NSArray<MDLMaterialPropertyConnection*> *connections;
 
 @end
 
@@ -297,6 +351,12 @@
 
 @end
 
+typedef NS_ENUM(NSUInteger, MDLMaterialFace) {
+    MDLMaterialFaceFront = 0,
+    MDLMaterialFaceBack,
+    MDLMaterialFaceDoubleSided
+};
+
 NS_CLASS_AVAILABLE(10_11, 9_0)
 MDL_EXPORT
 @interface MDLMaterial : NSObject<MDLNamed, NSFastEnumeration>
@@ -323,7 +383,9 @@
 - (nullable MDLMaterialProperty *)objectForKeyedSubscript:(NSString*)name;
 @property (nonatomic, readonly) NSUInteger count;
 
+// Default is MDLMaterialFaceFront
+@property (nonatomic) MDLMaterialFace materialFace;
+
 @end
 
 NS_ASSUME_NONNULL_END
-
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMesh.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMesh.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMesh.h	2015-08-23 03:50:33.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMesh.h	2016-05-16 07:44:17.000000000 +0200
@@ -24,10 +24,10 @@
 MDL_EXPORT
 @interface MDLVertexAttributeData : NSObject
 
-@property (nonatomic, retain) MDLMeshBufferMap *map;
-@property (nonatomic) void *dataStart;
-@property (nonatomic) NSUInteger stride;
-@property (nonatomic) MDLVertexFormat format;
+@property (nonatomic, retain, readonly) MDLMeshBufferMap *map;
+@property (nonatomic, readonly) void *dataStart;
+@property (nonatomic, readonly) NSUInteger stride;
+@property (nonatomic, readonly) MDLVertexFormat format;
 
 @end
 
@@ -43,14 +43,22 @@
 @interface MDLMesh : MDLObject
 
 /*!
+ @method initWithAllocator:
+ @abstract Initialize a mesh with an allocator
+ @return An empty mesh
+*/
+
+- (instancetype)initWithBufferAllocator:(nullable id<MDLMeshBufferAllocator>)bufferAllocator;
+
+/*!
  @method initWithVertexBuffer:vertexCount:descriptor:submeshes:
  @abstract Initialize object with a vertex buffer and a collection of submeshes
- @return Initialized mesh or nil if descriptor's layout array does not describe 
+ @return Initialized mesh or nil if descriptor's layout array does not describe
          a single buffer
  @param vertexBuffer MDLMeshBuffer object containing all vertex data for the mesh
  @param vertexCount Number of vertices in the vertexBuffer
  @param descriptor VertexDescriptor specifying how to interpret vertex data
- @param submeshes Array of submeshes with index buffers referencing vertex data 
+ @param submeshes Array of submeshes with index buffers referencing vertex data
         and/or materials to be applied to mesh
  */
 - (instancetype)initWithVertexBuffer:(id<MDLMeshBuffer>)vertexBuffer
@@ -60,17 +68,17 @@
 
 /*!
  @method initWithVertexBuffer:vertexCount:descriptor:submeshes:
- @abstract Initialize object with an array of vertex buffers (Structure of 
+ @abstract Initialize object with an array of vertex buffers (Structure of
            Arrays) and a collection of submeshes
- @return Initialized mesh or nil if descriptor's layout array is incompatible 
+ @return Initialized mesh or nil if descriptor's layout array is incompatible
          with vertexBuffers array
  @param vertexCount Number of vertices in vertexBuffers
- @param vertexBuffer An array of MDLMeshBuffer objects containing vertex data 
+ @param vertexBuffer An array of MDLMeshBuffer objects containing vertex data
          for the mesh
  @param descriptor VertexDescriptor specifying how to interpret vertex data
- @param submeshes Array of submeshes with index buffers referencing vertex data 
+ @param submeshes Array of submeshes with index buffers referencing vertex data
         and/or materials to be applied to mesh
- @discussion Allows initialization with the layout of the vertexBuffers in a 
+ @discussion Allows initialization with the layout of the vertexBuffers in a
         structure-of-arrays form, in other words, non-interleaved vertex attributes
  */
 - (instancetype)initWithVertexBuffers:(NSArray<id<MDLMeshBuffer>> *)vertexBuffers
@@ -78,7 +86,6 @@
                            descriptor:(MDLVertexDescriptor *)descriptor
                             submeshes:(NSArray<MDLSubmesh*> *)submeshes;
 
-
 /*!
  @method vertexAttributeDataForAttributeNamed:
  @abstract convenience selector to get quick access to vertex attribute data
@@ -88,6 +95,20 @@
 - (nullable MDLVertexAttributeData*)vertexAttributeDataForAttributeNamed:(NSString*)name;
 
 /*!
+ @method vertexAttributeDataForAttributeNamed:asFormat
+ @abstract convenience selector to get quick access to vertex attribute data
+           reformatted to the requested format if necessary.
+ @discussion If the desired format has less elements than the source attribute
+             elements, excess elements will be discarded. If the desired format
+             has more elements than the source attribute, then the destination
+             elements will be set to zero.
+             The vertex buffer will remain mapped until the MDLVertexAttributeData
+             is freed.
+ */
+- (nullable MDLVertexAttributeData*)vertexAttributeDataForAttributeNamed:(NSString*)name
+                                                                asFormat:(MDLVertexFormat)format;
+
+/*!
  @property boundingBox
  @abstract Bounding box encompasing the mesh
  @discussion Calculated by iterating through MDLVertexAttributePosition to find
@@ -99,15 +120,15 @@
 /*!
  @property vertexDescriptor
  @abstract Immutable vertex descriptor for interpreting data in vertexBuffers
- @discussion Setting this applies the new layout in 'vertexBuffers' thus is a 
-             heavyweight operation as structured copies of almost all vertex 
-             buffer data could be made.  Additionally, if the new vertexDescriptor 
-             does not have an attribute in the original vertexDescriptor, that 
-             attribute will be deleted.  If the original vertexDescriptor does 
-             not have an attribute in the new vertexDescriptor, the data for the 
-             added attribute set as the added attribute's initializationValue 
+ @discussion Setting this applies the new layout in 'vertexBuffers' thus is a
+             heavyweight operation as structured copies of almost all vertex
+             buffer data could be made.  Additionally, if the new vertexDescriptor
+             does not have an attribute in the original vertexDescriptor, that
+             attribute will be deleted.  If the original vertexDescriptor does
+             not have an attribute in the new vertexDescriptor, the data for the
+             added attribute set as the added attribute's initializationValue
              property.
- 
+
              The allocator associated with each original meshbuffer is used to
              reallocate the corresponding resultant meshbuffer.
  */
@@ -116,11 +137,11 @@
 /*!
  @property vertexCount
  @abstract Number of vertices in the vertexBuffers
- @discussion The size of vertex data in each buffer can be compute by multiplying 
-             this value with the stride of the buffer in the vertexDescriptor's 
+ @discussion The size of vertex data in each buffer can be computed by multiplying
+             this value with the stride of the buffer in the vertexDescriptor's
              layout
  */
-@property (nonatomic, readonly) NSUInteger vertexCount;
+@property (nonatomic, readwrite) NSUInteger vertexCount;
 
 /*!
  @property vertexBuffers
@@ -131,10 +152,16 @@
 
 /*!
  @property submeshes
- @abstract Array of submeshes containing an indexbuffer referencing the vertex 
+ @abstract Array of submeshes containing an indexbuffer referencing the vertex
            data and material to be applied when the mesh is rendered
  */
-@property (nonatomic, readonly, retain) NSMutableArray<MDLSubmesh*> *submeshes;
+@property (nonatomic, copy, nullable) NSMutableArray<MDLSubmesh*> *submeshes;
+
+/*!
+ @property allocator
+ @abstract allocator used to allocate contained mesh buffers
+ */
+@property (nonatomic, readonly, retain) id<MDLMeshBufferAllocator> allocator;
 
 @end
 
@@ -151,17 +178,34 @@
                       format:(MDLVertexFormat)format;
 
 /*!
- @method addNormalsWithAttributeNamed:bufferIndex:
+ @method addAttributeWithName:format:type:data:stride
+ @abstract Create a new vertex attribute including an associated buffer with
+ a copy of the supplied data, and update the vertex descriptor accordingly
+ @param name The name the attribute can be found by
+ @param format Format of the data, such as MDLVertexFormatFloat3
+ @param type The usage of the attribute, such as MDLVertexAttributePosition
+ @param data Object containing the data to be used in the new vertex buffer
+ @param stride The increment in bytes from the start of one data entry to
+ the next.
+ */
+-(void)addAttributeWithName:(NSString *)name
+                     format:(MDLVertexFormat)format
+                       type:(NSString *)type
+                       data:(NSData *)data
+                     stride:(NSInteger)stride;
+
+/*!
+ @method addNormalsWithAttributeNamed:creaseThreshold:
  @abstract Calculate and add vertex normal data
- @param attributeName Name of vertex normal attribute.  If nil, vertex normals 
+ @param attributeName Name of vertex normal attribute.  If nil, vertex normals
         will be added with the MDLVertexAttributeNormal name string
- @param creaseThreshold Threshold of the dot product between the 2 triangles after which 
+ @param creaseThreshold Threshold of the dot product between the 2 triangles after which
                         their face normal will be smoothed out. Therefore, a threshold of 0 will
                         smooth everything and a threshold of 1 won't smooth anything.
  @discussion Uses the attribute named MDLVertexAttributePosition to calculate
-             vertex normals. If the mesh does not have an attribute with 
-             'attributeName', it will be added, otherwise the attribute name will 
-             be overwritten with vertex normal data. 'vertexDescriptor' will be 
+             vertex normals. If the mesh does not have an attribute with
+             'attributeName', it will be added, otherwise the attribute name will
+             be overwritten with vertex normal data. 'vertexDescriptor' will be
              updated to reflect the new attribute.
  */
 - (void)addNormalsWithAttributeNamed:(nullable NSString *)attributeName
@@ -176,7 +220,7 @@
  @param bitangentAttributeNamed Name of vertex bitangent attribute.
  @discussion Uses the attribute named MDLVertexAttributePosition and
              textureCoordinateAttributeName to calculate tangent and bitangent
-             attributes. The mesh's vertexDescriptor will be updated to reflect 
+             attributes. The mesh's vertexDescriptor will be updated to reflect
              the new attributes if necessary.
  */
 - (void)addTangentBasisForTextureCoordinateAttributeNamed:(NSString*)textureCoordinateAttributeName
@@ -190,10 +234,10 @@
  @param normalAttributeNamed normals to use in calculations
  @param tangentAttributeName Name of a four component vertex tangent attribute.
  @discussion Uses the attribute named MDLVertexAttributePosition and
-             textureCoordinateAttributeName and the specified normals to calculate 
-             tangent information. The mesh's vertexDescriptor will be updated to 
+             textureCoordinateAttributeName and the specified normals to calculate
+             tangent information. The mesh's vertexDescriptor will be updated to
              reflect the new attribute if necessary.
-             Note that the bitangent can be calculated from the normal and 
+             Note that the bitangent can be calculated from the normal and
              tangent by B = (N x T) * T.w
  */
 - (void)addTangentBasisForTextureCoordinateAttributeNamed:(NSString*)textureCoordinateAttributeName
@@ -201,14 +245,50 @@
                                     tangentAttributeNamed:(NSString *)tangentAttributeName;
 
 /*!
+ @method addTextureCoordinatesForAttributeNamed:textureCoordinateAttributeName
+ @abstract Creates texture coordinates by unwrapping the mesh
+ @param textureCoordinateAttributeName texture coordinates to modify or create
+ @discussion Uses the attribute named MDLVertexAttributePosition and if available,
+             the attribute named MDLVertexAttributeNormal to calculate texture coordinates
+ */
+- (void)addUnwrappedTextureCoordinatesForAttributeNamed:(NSString*)textureCoordinateAttributeName;
+
+/*!
  @method makeVerticesUnique:
  @abstract Deindexes the vertex array
- @discussion If any vertices are shared on multiple faces, duplicate those 
-             vertices so faces do not share vertices. The vertex buffer and index 
+ @discussion If any vertices are shared on multiple faces, duplicate those
+             vertices so faces do not share vertices. The vertex buffer and index
              buffers on submeshes may grow to accomadate any vertices added.
  */
 - (void)makeVerticesUnique;
 
+/*!
+ @method replaceAttributeNamed:withData
+ @abstract replace existing attribute data with new attribute data retaining
+ the format of the replacement data.
+ @discussion If the specified attribute does not already exist, it will be
+ created.
+ */
+- (void)replaceAttributeNamed:(NSString*)name
+                     withData:(nonnull MDLVertexAttributeData*)newData;
+
+/*!
+ @method updateAttributeNamed:withData
+ @abstract update existing attribute data with new attribute data retaining
+ the format of the exisitng data.
+ @discussion If the specified attribute does not already exist, it will be
+ created with the same format as the newData.
+ */
+- (void)updateAttributeNamed:(NSString*)name
+                    withData:(nonnull MDLVertexAttributeData*)newData;
+
+/*! 
+ @method removeAttributeNamed:
+ @abstract remove an attribute
+ @discussion if the named attribute does not exist, nothing happens.
+ */
+- (void)removeAttributeNamed:(NSString*)name;
+
 
 @end
 
@@ -217,25 +297,26 @@
 @interface MDLMesh (Generators)
 
 /*!
- @method newBoxWithDimensions:segments:inwardNormals:geometryType:allocator:
+ @method initBoxMeshWithExtent:segments:inwardNormals:geometryType:allocator:
  @abstract Factory method for generating a mesh with a cube shape
  @return MDLMesh box with desired attributes
- @param dimensions Width, height, and depth of the box
+ @param extent size of the box in each dimension
  @param segments Number of slices in each dimension
  @param inwardNormals Generated Normal point inward
  @param geometryType Can be MDLGeometryTypeLines, MDLGeometryTypeQuads, or MDLGeometryTypeTriangles
- @param allocator A mesh buffer allocator used to allocate memory to back buffers 
+ @param allocator A mesh buffer allocator used to allocate memory to back buffers
         for the returned mesh.  If nil, a default allocator will be used
- @discussion Assembled with triangle or quad primitives.  Specifying inward 
-             normals is useful for generating a skybox. The center of the box 
+ @discussion Assembled with triangle or quad primitives.  Specifying inward
+             normals is useful for generating a skybox. The center of the box
              is at(0, 0, 0).
              Will raise an exception if an unsupported geometry type is passed in.
  */
-+ (instancetype)newBoxWithDimensions:(vector_float3)dimensions
-                            segments:(vector_uint3)segments
-                        geometryType:(MDLGeometryType)geometryType
-                       inwardNormals:(BOOL)inwardNormals
-                           allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
+- (instancetype)initBoxWithExtent:(vector_float3)extent
+                             segments:(vector_uint3)segments
+                        inwardNormals:(BOOL)inwardNormals
+                         geometryType:(MDLGeometryType)geometryType
+                            allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
+
 
 /*!
  @method newEllipsoidWithRadii:radialSegments:verticalSegments:inwardNormals:hemisphere:allocator:
@@ -244,13 +325,13 @@
  @param radii Width, height, and depth of ellipsoid.
  @param radialSegments Number of pie slices :)
  @param verticalSegments Number of slices in the vertical direction
- @param geometryType Must be MDLGeometryTypeTriangles
- @param inwardNormals If true, generated normals will face inwards. Useful for 
+ @param geometryType Must be MDLGeometryTypeTriangles or MDLGeometryTypeLines
+ @param inwardNormals If true, generated normals will face inwards. Useful for
         generating a skydome.
  @param geometryType Must be  Must be MDLGeometryTypeTriangles
  @param hemisphere If true, only top half of ellipsoid will be generated. The
         actual nubmer of vertical slices will be half of 'vertical' segments
- @param allocator A mesh buffer allocator used to allocate memory to back buffers 
+ @param allocator A mesh buffer allocator used to allocate memory to back buffers
         for the returned mesh.  If nil, a default allocator will be used
  @discussion Specifying inward normals and hemisphere is useful for generating a skydome.
              Specifying equal X, Y, and Z radii will generate a sphere.
@@ -258,13 +339,17 @@
              Will raise an exception if radialSegments is < 3, verticalSegments is < 2,
              or an unsupported geometry type is passed in.
  */
-+ (instancetype)newEllipsoidWithRadii:(vector_float3)radii
-                       radialSegments:(NSUInteger)radialSegments
-                     verticalSegments:(NSUInteger)verticalSegments
-                         geometryType:(MDLGeometryType)geometryType
-                        inwardNormals:(BOOL)inwardNormals
-                           hemisphere:(BOOL)hemisphere
-                            allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
+- (instancetype)initSphereWithExtent:(vector_float3)extent
+                            segments:(vector_uint2)segments
+                       inwardNormals:(BOOL)inwardNormals
+                        geometryType:(MDLGeometryType)geometryType
+                           allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
+- (instancetype)initHemisphereWithExtent:(vector_float3)extent
+                                segments:(vector_uint2)segments
+                           inwardNormals:(BOOL)inwardNormals
+                                     cap:(BOOL)cap
+                            geometryType:(MDLGeometryType)geometryType
+                               allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
 
 /*!
  @method newCylinderWithHeight:
@@ -274,15 +359,15 @@
  @param radii Radii of cylinder in X and Z directions.
  @param radialSegments Number of pie slices :)
  @param verticalSegments Number of slices along Y axis
- @param geometryType Must be MDLGeometryTypeTriangles
+ @param geometryType Must be MDLGeometryTypeTriangles or MDLGeometryTypeLines
  @param inwardNormals Normals point toward center of cylinder
- @param allocator A mesh buffer allocator used to allocate memory to back buffers 
+ @param allocator A mesh buffer allocator used to allocate memory to back buffers
         for the returned mesh.  If nil, a default allocator will be used
  @discussion Center of cylinder at (0, 0, 0) with a top at +Y and bottom at -Y.
              Specifying equal X and Z radia will generate a true cylinder.
              Specifying a height of 0.0 and verticalSegments of 0 will generate
              a disc.
-             Will raise and exceiption radialSegments is < 3 or an unsupported
+             Will raise an exception if radialSegments is < 3 or if an unsupported
              geometry type is passed in.
              Generated texture coordinates are laid out as follows:
                                                       ___
@@ -297,12 +382,51 @@
                  Texture for base of cylinder  ---> [     ]
                                                      \___/   <- T texcoord = 1.0
  */
-+ (instancetype)newCylinderWithHeight:(float)height
-                                radii:(vector_float2)radii
-                       radialSegments:(NSUInteger)radialSegments
-                     verticalSegments:(NSUInteger)verticalSegments
-                         geometryType:(MDLGeometryType)geometryType
+- (instancetype)initCylinderWithExtent:(vector_float3)extent
+                              segments:(vector_uint2)segments
+                         inwardNormals:(BOOL)inwardNormals
+                                topCap:(BOOL)topCap
+                             bottomCap:(BOOL)bottomCap
+                          geometryType:(MDLGeometryType)geometryType
+                             allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
+
+/*!
+ @method newCapsuleWithHeight:
+ @abstract Factory method for generating a mesh with a capsule shape; a cylinder
+           with hemispheres for caps.
+ @return MDLMesh capsule with desired attributes
+ @param height Height of cylindoid.
+ @param radii Radii of cylinder in X and Z directions.
+ @param radialSegments Number of pie slices :)
+ @param verticalSegments Number of slices along Y axis
+ @param hemisphereSegments Number of slices through hemisphere caps along Y axis 
+ @param geometryType Must be MDLGeometryTypeTriangles or MDLGeometryTypeLines
+ @param inwardNormals Normals point toward center of cylinder
+ @param allocator A mesh buffer allocator used to allocate memory to back buffers
+        for the returned mesh.  If nil, a default allocator will be used
+ @discussion Center of cylinder at (0, 0, 0) with a top at +Y and bottom at -Y.
+             Specifying equal X and Z radia will generate a true cylinder.
+             Specifying a height of 0.0 and verticalSegments of 0 will generate
+             a sphere. Height controls the size of the cylinder, the full height
+             of the capsule will also incorporate the hemisphere caps.
+            Will raise an exception if radialSegments is < 3 or if an unsupported
+            geometry type is passed in.
+            Generated texture coordinates are laid out as follows:
+                                      ___
+                                     /   \   <- T texcoord = 0.0
+ Texture for top of cylinder   ---> [-----]
+                                    [     ]  <- T texcoord = 0.3333
+                                    [     ]
+ Texture for sides of cylinder ---> [     ]
+                                    [_____]  <- T texcoord = 0.6666
+ Texture for base of cylinder  ---> [     ]
+                                     \___/   <- T texcoord = 1.0
+*/
+- (instancetype)initCapsuleWithExtent:(vector_float3)extent
+                     cylinderSegments:(vector_uint2)segments
+                   hemisphereSegments:(int)hemisphereSegments
                         inwardNormals:(BOOL)inwardNormals
+                         geometryType:(MDLGeometryType)geometryType
                             allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
 
 /*!
@@ -310,17 +434,17 @@
  @abstract Factory method for generating a mesh with an ellipticalCone shape.
  @return MDLMesh cone with desired attributes
  @param height Height of ellipticalCone from point to base.
- @param radii Radii of base in X and Z directions.  Values of vector should be 
+ @param radii Radii of base in X and Z directions.  Values of vector should be
         equal to create a true cone.
  @param radialSegments Number of pie slices :)
  @param verticalSegments Number of slices along Y axis
- @param geometryType Must be MDLGeometryTypeTriangles
+ @param geometryType Must be MDLGeometryTypeTriangles or MDLGeometryTypeLines
  @param inwardNormals Normals point toward center of ellipticalCone
- @param allocator A mesh buffer allocator used to allocate memory to back buffers 
+ @param allocator A mesh buffer allocator used to allocate memory to back buffers
         for the returned mesh.  If nil, a default allocator will be used
- @discussion Point of cone at (0, 0, 0) while base of cone is -Y. 
-             Will raise an exception if radialSegments is < 3, verticalSegments is < 1,
-             or an unsupported geometry type is passed in.
+ @discussion Point of cone at (0, 0, 0) while base of cone is -Y.
+             Will raise an exception if radialSegments is < 3, or verticalSegments is < 1,
+             or if an unsupported geometry type is passed in.
              Generated texture coordinates are laid out as follows:
                                                  _____
                                                 [     ]  <- T texcoord = 0.0
@@ -332,32 +456,29 @@
                  Texture for base of cone  ---> [     ]
                                                  \___/   <- T texcoord = 1.0
  */
-+ (instancetype)newEllipticalConeWithHeight:(float)height
-                                      radii:(vector_float2)radii
-                             radialSegments:(NSUInteger)radialSegments
-                           verticalSegments:(NSUInteger)verticalSegments
-                               geometryType:(MDLGeometryType)geometryType
-                              inwardNormals:(BOOL)inwardNormals
-                                  allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
+- (instancetype)initConeWithExtent:(vector_float3)extent
+                          segments:(vector_uint2)segments
+                     inwardNormals:(BOOL)inwardNormals
+                               cap:(BOOL)cap
+                      geometryType:(MDLGeometryType)geometryType
+                         allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
 
 /*!
  @method newPlaneWithDimensions:segments:geometryType:allocator:
  @abstract Factory method for generating a mesh with an planar shape
  @return MDLMesh plane with desired attributes
- @param dimensions Dimensions of the plane in X and Z directions.
+ @param extent extent of the plane
  @param segments Number of segements in the X and Y dimensions
  @param geometryType Can be MDLGeometryTypeLines, MDLGeometryTypeQuads, or MDLGeometryTypeTriangles
- @param allocator A mesh buffer allocator used to allocate memory to back buffers 
+ @param allocator A mesh buffer allocator used to allocate memory to back buffers
         for the returned mesh.  If nil, a default allocator will be used
- @discussion Assembled with triangle or quad primitives. Creates a plane along 
-             the X/Z axis. Center of plane at (0, 0, 0). All normals point up,
-             towards positive Y
+ @discussion Creates a plane spanning the greatest dimensions of extent.
              Will raise an exception if an unsupported geometry type is passed in.
  */
-+ (instancetype)newPlaneWithDimensions:(vector_float2)dimensions
-                              segments:(vector_uint2)segments
-                          geometryType:(MDLGeometryType)geometryType
-                             allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
+- (instancetype)initPlaneWithExtent:(vector_float3)extent
+                           segments:(vector_uint2)segments
+                       geometryType:(MDLGeometryType)geometryType
+                          allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
 
 /*!
  @method newIcosahedronWithRadius:inwardNormals:allocator:
@@ -365,14 +486,14 @@
  @return MDLMesh icosahedron with desired attributes
  @param radius Distance from the center to the outermost point of the mesh
  @param inwardNormals Generated normals will face towards the center of the mesh
- @param allocator A mesh buffer allocator used to allocate memory to back buffers 
+ @param allocator A mesh buffer allocator used to allocate memory to back buffers
         for the returned mesh.  If nil, a default allocator will be used
  @discussion  Creates an icosahedron with center at (0, 0, 0).
  */
-+ (instancetype)newIcosahedronWithRadius:(float)radius
-                           inwardNormals:(BOOL)inwardNormals
-                               allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
-
+- (instancetype)initIcosahedronWithExtent:(vector_float3)extent
+                            inwardNormals:(BOOL)inwardNormals
+                             geometryType:(MDLGeometryType)geometryType
+                                allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
 
 /*!
  @method newSubdividedMesh:subdivisionLevels:allocator:
@@ -381,39 +502,91 @@
  @param submeshIndex Index of submesh in Mesh's submesh array from which to
         generate a subdivided mesh
  @param subdivisionLevels The number of levels to subdivide mesh
- @discussion Subdivision levels over four are likely to generate more triangles 
-             than can be reasonably displayed. Index and vertex data will use 
-             the same allocator used for the source mesh. Loading an asset 
+ @discussion Subdivision levels over four are likely to generate more triangles
+             than can be reasonably displayed. Index and vertex data will use
+             the same allocator used for the source mesh. Loading an asset
              using the topology preservation flag set to YES will result in the
              best subdivision results.
- @return Returns a mesh subdividied to index level, unless subdivision is 
-         impossible.  Only triangle and quadrilateral meshes can be subdivided.
+ @return Returns a mesh subdivided to index level, unless subdivision is
+         impossible.
  */
+- (instancetype)initMeshBySubdividingMesh:(MDLMesh*)mesh
+                             submeshIndex:(int)submeshIndex
+                        subdivisionLevels:(unsigned int)subdivisionLevels
+                                allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
+
+
++ (instancetype)newBoxWithDimensions:(vector_float3)dimensions
+                            segments:(vector_uint3)segments
+                        geometryType:(MDLGeometryType)geometryType
+                       inwardNormals:(BOOL)inwardNormals
+                           allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
++ (instancetype)newEllipsoidWithRadii:(vector_float3)radii
+                       radialSegments:(NSUInteger)radialSegments
+                     verticalSegments:(NSUInteger)verticalSegments
+                         geometryType:(MDLGeometryType)geometryType
+                        inwardNormals:(BOOL)inwardNormals
+                           hemisphere:(BOOL)hemisphere
+                            allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
++ (instancetype)newCylinderWithHeight:(float)height
+                                radii:(vector_float2)radii
+                       radialSegments:(NSUInteger)radialSegments
+                     verticalSegments:(NSUInteger)verticalSegments
+                         geometryType:(MDLGeometryType)geometryType
+                        inwardNormals:(BOOL)inwardNormals
+                            allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
++ (instancetype)newEllipticalConeWithHeight:(float)height
+                                      radii:(vector_float2)radii
+                             radialSegments:(NSUInteger)radialSegments
+                           verticalSegments:(NSUInteger)verticalSegments
+                               geometryType:(MDLGeometryType)geometryType
+                              inwardNormals:(BOOL)inwardNormals
+                                  allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
++ (instancetype)newPlaneWithDimensions:(vector_float2)dimensions
+                              segments:(vector_uint2)segments
+                          geometryType:(MDLGeometryType)geometryType
+                             allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
++ (instancetype)newIcosahedronWithRadius:(float)radius
+                           inwardNormals:(BOOL)inwardNormals
+                               allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
 + (nullable instancetype)newSubdividedMesh:(MDLMesh*)mesh
                               submeshIndex:(NSUInteger)submeshIndex
                          subdivisionLevels:(NSUInteger)subdivisionLevels;
 
 @end
 
+/*!
+ @interface MDLAnimationRig
+ @abstract Animation control rig for use when vertex attributes of joint indices
+           and weights exist.
+ */
+
+@interface MDLMesh (MDLAnimationRig)
+
+@property (readonly, nonatomic) NSUInteger controlNodeCount;
+- (MDLObject *) controlNodeForIndex:(NSUInteger)index;
+- (matrix_float4x4) inverseBasePoseForIndex:(NSUInteger)index;
+
+@end
 
 
 @interface MDLMesh (MDLLightBaking)
 
 /*!
  @method generateAmbientOcclusionTextureWithSize:
- @abstract Creates an Ambient Occlusion texture, returns true upon success, false 
+ @abstract Creates an Ambient Occlusion texture, returns true upon success, false
            upon failure
  @param size  Texture Size in which to bake the ambient occlusion
  @param raysPerSample Number of rays to be sent out of every texture texel against
         the object for potential occlusion.
- @param attenuationFactor Float between 0 to 1 that defines how to attenuate the 
-        AO value. 0 doesn't change it, and at 1, all AO values are white except 
+ @param attenuationFactor Float between 0 to 1 that defines how to attenuate the
+        AO value. 0 doesn't change it, and at 1, all AO values are white except
         if they are originally completely black. Quadratic attenuation in between.
  @param objectsToConsider NSArray of MDLMeshes containing the objects to raytrace against
- @param vertexAttributeName NSString of the MDLVertexAttribute where the vertex 
-        texture UVs will be stored. Creates it if it doesn't exist, otherwise 
+ @param vertexAttributeName NSString of the MDLVertexAttribute where the vertex
+        texture UVs will be stored. Creates it if it doesn't exist, otherwise
         overwrites current values.
- @param materialPropertyName NSString of the MDLMaterialProperty that will store 
+ @param materialPropertyName NSString of the MDLMaterialProperty that will store
         the texture in the Mesh.
  @result Success or failure of the baking process.
  */
@@ -429,17 +602,17 @@
  @abstract Creates an Ambient Occlusion texture, returns true upon success, false
            upon failure
  @param quality Float between 0 and 1 that defines quality of the bake process.
-        0 is of lower quality but bakes faster and uses less memory, where 1 is 
+        0 is of lower quality but bakes faster and uses less memory, where 1 is
         of higher quality.
- @param attenuationFactor Float between 0 to 1 that defines how to attenuate the 
-        AO value. 0 doesn't change it, and at 1, all AO values are white except 
+ @param attenuationFactor Float between 0 to 1 that defines how to attenuate the
+        AO value. 0 doesn't change it, and at 1, all AO values are white except
         if they are originally completely black. Quadratic attenuation in between.
- @param objectsToConsider NSArray of MDLMeshes containing the objects to raytrace 
+ @param objectsToConsider NSArray of MDLMeshes containing the objects to raytrace
         against
- @param vertexAttributeName NSString of the MDLVertexAttribute where the vertex 
-        texture UVs will be stored. Creates it if it doesn't exist, otherwise 
+ @param vertexAttributeName NSString of the MDLVertexAttribute where the vertex
+        texture UVs will be stored. Creates it if it doesn't exist, otherwise
         overwrites current values.
- @param materialPropertyName NSString of the MDLMaterialProperty that will store 
+ @param materialPropertyName NSString of the MDLMaterialProperty that will store
         the texture in the Mesh.
  @result Success or failure of the baking process.
   */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLObject.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLObject.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLObject.h	2015-08-23 03:50:33.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLObject.h	2016-05-16 05:38:40.000000000 +0200
@@ -46,6 +46,17 @@
 @property (nonatomic, weak, nullable) MDLObject* parent;
 
 /*!
+ @property path
+ @abstract a string representing a path to the object
+ @discussion a path is of the form /path/to/object where the path is formed by
+             concatenating the names of the objects up the parent chain.
+             Requesting a path will force any unnamed objects to became uniquely
+             named. Any characters outside of [A-Z][a-z][0-9][:-_.] will be
+             forced to underscore.
+ */
+@property (nonatomic, readonly) NSString* path;
+
+/*!
  @property transform
  @abstract Short hand property for the MDLTransformComponent.
  @discussion 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLSubmesh.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLSubmesh.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLSubmesh.h	2015-08-23 03:50:33.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLSubmesh.h	2016-05-16 07:44:17.000000000 +0200
@@ -160,6 +160,8 @@
  */
 @property (nonatomic, readonly, retain) id<MDLMeshBuffer> indexBuffer;
 
+- (id<MDLMeshBuffer>)indexBufferAsIndexType:(MDLIndexBitDepth)indexType;
+
 /*!
  @property indexCount
  @abstract Number of indices in the indexBuffer
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTexture.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTexture.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTexture.h	2015-08-23 03:50:33.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTexture.h	2016-05-16 05:38:40.000000000 +0200
@@ -73,6 +73,8 @@
 MDL_EXPORT
 @interface MDLTexture : NSObject<MDLNamed>
 
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
+
 /**
  Creates a texture from a source in the main bundle named in a manner matching
   name.
@@ -138,6 +140,15 @@
 @property (nonatomic, readonly) MDLTextureChannelEncoding channelEncoding;
 @property (nonatomic) BOOL isCube;
 
+/**
+ hasAlphaValues
+ @summary
+ Can be overridden. If not overridden, hasAlpha will be NO if the texture does not
+ have an alpha channel. It wil be YES if the texture has an alpha channel and
+ there is at least one non-opaque texel in it.
+ */
+@property (nonatomic) BOOL hasAlphaValues;
+
 @end
 
 /** 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTransform.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTransform.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTransform.h	2015-08-23 03:50:33.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTransform.h	2016-05-18 04:40:09.000000000 +0200
@@ -30,11 +30,17 @@
 /** The matrix, at minimumTime */
 @property (nonatomic, assign) matrix_float4x4 matrix;
 
-/** If no animation data is present, minimumTime and maximumTime will be zero
- */
+/** if YES, this transform is intended to be in global space, not parent space */
+@property (nonatomic, assign) BOOL resetsTransform;
+
+/** If no animation data is present, minimumTime and maximumTime will be zero */
 @property (nonatomic, readonly) NSTimeInterval minimumTime;
 @property (nonatomic, readonly) NSTimeInterval maximumTime;
 
+/** An array of sample times for which a key has been stored
+    If no animation data is present, the array will contain a single value of zero */
+@property (nonatomic, readonly, copy) NSArray<NSNumber*> *keyTimes;
+
 @optional
 - (void)setLocalTransform:(matrix_float4x4)transform forTime:(NSTimeInterval)time;
 
@@ -70,10 +76,12 @@
 
 NS_CLASS_AVAILABLE(10_11, 9_0)
 MDL_EXPORT
-@interface MDLTransform : NSObject <MDLTransformComponent>
+@interface MDLTransform : NSObject <NSCopying, MDLTransformComponent>
 
 - (instancetype)initWithIdentity NS_DESIGNATED_INITIALIZER;
 - (instancetype)initWithTransformComponent:(id<MDLTransformComponent>)component;
+- (instancetype)initWithTransformComponent:(id<MDLTransformComponent>)component
+                           resetsTransform:(BOOL)resetsTransform;
 
 /**
  Initialization with a matrix assumes the matrix is an invertible, homogeneous 
@@ -81,6 +89,7 @@
  with a non-affine matrix will yield those of the identity transform.
  */
 - (instancetype)initWithMatrix:(matrix_float4x4)matrix;
+- (instancetype)initWithMatrix:(matrix_float4x4)matrix resetsTransform:(BOOL)resetsTransform;
 
 /**
  Set all transform components to identity
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTypes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTypes.h	2015-08-23 03:50:33.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTypes.h	2016-05-16 05:38:40.000000000 +0200
@@ -25,6 +25,12 @@
 /* Stereolithography file format, file extension STL, UTI public.standard-tesselated-geometry-format */
 MDL_EXPORT NSString * __nonnull const kUTTypeStereolithography NS_AVAILABLE(10_11, 9_0);
 
+/* Universal Scene Description file format, file extension USDA or USDB, UTI com.pixar.universal-scene-description */
+MDL_EXPORT NSString * __nonnull const kUTTypeUniversalSceneDescription NS_AVAILABLE(10_12, 10_0);
+
+/* MDLTexture can export OpenEXR files. The correct file format extension is EXR, and
+   the UTI is com.ilm.openexr-image */
+
 NS_ASSUME_NONNULL_BEGIN
 typedef NS_ENUM(NSUInteger, MDLIndexBitDepth)
 {
@@ -51,6 +57,11 @@
     MDLGeometryKindQuads
 };
 
+typedef NS_ENUM(NSInteger, MDLProbePlacement) {
+    MDLProbePlacementUniformGrid = 0,
+    MDLProbePlacementIrradianceDistribution
+};
+
 NS_CLASS_AVAILABLE(10_11, 9_0)
 MDL_EXPORT
 @protocol MDLNamed
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLVertexDescriptor.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLVertexDescriptor.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLVertexDescriptor.h	2015-08-23 03:50:33.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLVertexDescriptor.h	2016-05-16 05:38:40.000000000 +0200
@@ -282,10 +282,16 @@
  */
 - (void)addOrReplaceAttribute:(nonnull MDLVertexAttribute*)attribute;
 
+/*!
+ @method removeAttributeNamed:
+ @abstract Remove the named attribute if it exists
+ */
+- (void)removeAttributeNamed:(NSString*)name;
+
 /*! 
  @property attributes
  @abstract An array of MDLVertexAttribute objects
- @discussion An array describing the current attribute state of vertex buffers in an
+ @discussion ay describing the current attribute state of vertex buffers in an
              MDLMesh mesh
  */
 @property (nonatomic, retain) NSMutableArray<MDLVertexAttribute*> *attributes;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLVoxelArray.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLVoxelArray.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLVoxelArray.h	2015-08-23 03:50:33.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLVoxelArray.h	2016-05-18 04:40:08.000000000 +0200
@@ -14,7 +14,7 @@
 
 #import <ModelIO/MDLTypes.h>
 #import <ModelIO/MDLMeshBuffer.h>
-#import <Foundation/Foundation.h>
+#import <ModelIO/MDLObject.h>
 #import <simd/simd.h>
 
 NS_ASSUME_NONNULL_BEGIN
@@ -51,16 +51,34 @@
 
 NS_CLASS_AVAILABLE(10_11, 9_0)
 MDL_EXPORT
-@interface MDLVoxelArray : NSObject
+@interface MDLVoxelArray : MDLObject
+
+/**
+ Initialize a voxel grid from an MDLAsset. Attempts to create a closed volume
+ model by applying "patches" of radius patchRadius to any holes found in the
+ orginal mesh. Choose a patch radius that will be large enough to fill in the largest
+ hole in the model.
+ */
+- (instancetype)initWithAsset:(MDLAsset*)asset divisions:(int)divisions patchRadius:(float)patchRadius;
+
+/**
+ Initialize a voxel grid from an NSData containing an array of MDLVoxelIndex values.
+ 
+ @param boundingBox The bounds defining the extent of the volume model in Cartesian space
+ @param voxelExtent The extent of a single voxel
+ */
+- (instancetype)initWithData:(NSData*)voxelData
+                 boundingBox:(MDLAxisAlignedBoundingBox)boundingBox
+                 voxelExtent:(float)voxelExtent;
 
 /**
  Initialize a voxel grid from an MDLAsset and dilate the resulting voxels by
- a number of interior and exterior shells. 
+ a number of interior and exterior shells.
  Routine will attempt to create a closed volume model by applying patches of
  a given radius to any holes it may find in the asset.
  
- @param divisions The number of divisions to divide the vertical extent of the 
-        model by.
+ @param divisions The number of divisions to divide the vertical extent of the
+ model by.
  @param interiorShells The number of shells to compute inside the surface shell
  @param exteriorShells The number of shells to compute outside the surface shell
  @param patchRadius The radius of the largest model mending patch in world space units
@@ -69,7 +87,7 @@
                     divisions:(int)divisions
                interiorShells:(int)interiorShells
                exteriorShells:(int)exteriorShells
-                  patchRadius:(float)patchRadius;
+                  patchRadius:(float)patchRadius NS_DEPRECATED(10_11, 10_12, NA, NA);
 
 /**
  Initialize a voxel grid from an MDLAsset and dilate the resulting voxels by
@@ -87,42 +105,53 @@
                     divisions:(int)divisions
               interiorNBWidth:(float)interiorNBWidth
               exteriorNBWidth:(float)exteriorNBWidth
-                  patchRadius:(float)patchRadius;
-
+                  patchRadius:(float)patchRadius NS_DEPRECATED(10_11, 10_12, NA, NA);
 
 /**
- Initialize a voxel grid from an NSData containing an array of MDLVoxelIndex values.
- 
- @param boundingBox The bounds defining the extent of the volume model in Cartesian space
- @param voxelExtent The extent of a single voxel
+ The number of voxels in the grid
  */
-- (instancetype)initWithData:(NSData*)voxelData
-                 boundingBox:(MDLAxisAlignedBoundingBox)boundingBox
-                 voxelExtent:(float)voxelExtent;
+@property (nonatomic, readonly) NSUInteger count;
 
 /**
- Create a mesh from the voxel grid
+ The extent of the voxel grid in index space
  */
-- (nullable MDLMesh*)meshUsingAllocator:(nullable id<MDLMeshBufferAllocator>)allocator;
+@property (nonatomic, readonly) MDLVoxelIndexExtent voxelIndexExtent;
 
 /**
  Determine if a sample exists at the specified index
- @discussion the allowAny parameters can be used to wildcard any dimensions. This 
-             is useful to perform queries such as determining if any voxel 
-             exists on the XY plane at a certain Z, or if any voxel exists at 
-             any X, Y, Z, or a particular shell, and so on.
+ @discussion the allowAny parameters can be used to wildcard any dimensions. This
+ is useful to perform queries such as determining if any voxel
+ exists on the XY plane at a certain Z, or if any voxel exists at
+ any X, Y, Z, or a particular shell, and so on.
  */
 - (BOOL)voxelExistsAtIndex:(MDLVoxelIndex)index
                  allowAnyX:(BOOL)allowAnyX allowAnyY:(BOOL)allowAnyY allowAnyZ:(BOOL)allowAnyZ
              allowAnyShell:(BOOL)allowAnyShell;
 
 /**
+ Returns an NSData containing the indices of all voxels found in the extent
+ */
+- (nullable NSData *)voxelsWithinExtent:(MDLVoxelIndexExtent)extent;
+
+/**
+ Returns an NSData containing the indices of all voxels in the voxel grid
+ */
+- (nullable NSData *)voxelIndices;
+
+/**
  Set a sample at the specified index
  @discussion the extent, bounds, and shell properties may be modified
  */
 - (void)setVoxelAtIndex:(MDLVoxelIndex)index;
 
 /**
+ Set voxels corresponding to a mesh.
+ Routine will attempt to create a closed volume model by applying "patches" of
+ a given radius to any holes it may find in the mesh.
+ */
+- (void)setVoxelsForMesh:(nonnull MDLMesh*)mesh divisions:(int)divisions patchRadius:(float)patchRadius;
+
+/**
  Set voxels corresponding to a mesh
  Routine will attempt to create a closed volume model by applying "patches" of
  a given radius to any holes it may find in the mesh.
@@ -137,7 +166,7 @@
                divisions:(int)divisions
           interiorShells:(int)interiorShells
           exteriorShells:(int)exteriorShells
-             patchRadius:(float)patchRadius;
+             patchRadius:(float)patchRadius NS_DEPRECATED(10_11, 10_12, NA, NA);
 
 
 /**
@@ -155,25 +184,21 @@
                divisions:(int)divisions
          interiorNBWidth:(float)interiorNBWidth
          exteriorNBWidth:(float)exteriorNBWidth
-             patchRadius:(float)patchRadius;
-
+             patchRadius:(float)patchRadius NS_DEPRECATED(10_11, 10_12, NA, NA);
 
 /**
- Returns an NSData containing the indices of all voxels found in the extent
- */
-- (nullable NSData *)voxelsWithinExtent:(MDLVoxelIndexExtent)extent;
-
-/**
- Returns an NSData containing the indices of all voxels in the voxel grid
+ Union modifies the voxel grid to be the merger with the supplied voxel grid.
+ It is assumed that the spatial voxel extent of one voxel in the supplied grid is the same as that of the voxel grid.
+ Note that the shell level data will be cleared.
  */
-- (nullable NSData *)voxelIndices;
+- (void)unionWithVoxels:(MDLVoxelArray*)voxels;
 
 /**
- Union modifies the voxel grid to be the merger with the supplied voxel grid.
+ Intersection modifies the voxel grid so that only voxels that are also in the supplied voxel grid are retained.
  It is assumed that the spatial voxel extent of one voxel in the supplied grid is the same as that of the voxel grid.
  Note that the shell level data will be cleared.
  */
-- (void)unionWithVoxels:(MDLVoxelArray*)voxels;
+- (void)intersectWithVoxels:(MDLVoxelArray*)voxels;
 
 /**
  Difference modifies the voxel grid so that voxels also in the supplied voxel grid are removed.
@@ -183,11 +208,9 @@
 - (void)differenceWithVoxels:(MDLVoxelArray*)voxels;
 
 /**
- Intersection modifies the voxel grid so that only voxels that are also in the supplied voxel grid are retained.
- It is assumed that the spatial voxel extent of one voxel in the supplied grid is the same as that of the voxel grid.
- Note that the shell level data will be cleared.
+ The extent of the voxel grid in Cartesian space
  */
-- (void)intersectWithVoxels:(MDLVoxelArray*)voxels;
+@property (nonatomic, readonly) MDLAxisAlignedBoundingBox boundingBox;
 
 /**
  Return the voxel index corresponding to a point in space
@@ -205,19 +228,49 @@
 - (MDLAxisAlignedBoundingBox)voxelBoundingBoxAtIndex:(MDLVoxelIndex)index;
 
 /**
- The number of voxels in the grid
+ Converts volume grid into a signed shell field by surrounding the surface voxels, which have shell 
+ level values of zero, by an inner layer of voxels with shell level values of negative one and an 
+ outer layer of voxels with shell level values of positive one.
+ 
+ The volume model must be closed in order to generate a signed shell field.
  */
-@property (nonatomic, readonly) NSUInteger count;
+- (void)convertToSignedShellField;
 
 /**
- The extent of the voxel grid in index space
+ Returns whether or not the volume grid is in a valid signed shell field form.
+ 
+ This property will be set to YES after calling generateSignedShellField. All other 
+ methods that modify the voxel grid will cause this property to be set to NO. Setting
+ shellFieldInteriorThickness and shellFieldExteriorThickness will not affect the value
+ of this property.
  */
-@property (nonatomic, readonly) MDLVoxelIndexExtent voxelIndexExtent;
+@property (nonatomic, readonly) BOOL isValidSignedShellField;
 
 /**
- The extent of the voxel grid in Cartesian space
+ If voxel grid is in a valid signed shell field form, sets the interior thickness to the desired width,
+ as measured from the model surface. If the voxel grid is not in a valid signed shell field form, the
+ value of this property is zero.
  */
-@property (nonatomic, readonly) MDLAxisAlignedBoundingBox boundingBox;
+@property (nonatomic) float shellFieldInteriorThickness;
+
+/**
+ If voxel grid is in a valid signed shell field form, sets the exterior thickness to the desired width,
+ as measured from the model surface. If the voxel grid is not in a valid signed shell field form, the
+ value of this property is zero.
+ */
+@property (nonatomic) float shellFieldExteriorThickness;
+
+/**
+ Creates a coarse mesh from the voxel grid
+ */
+- (nullable MDLMesh*)coarseMesh;
+- (nullable MDLMesh*)coarseMeshUsingAllocator:(nullable id<MDLMeshBufferAllocator>)allocator;
+
+/**
+ Creates a smooth mesh from the voxel grid
+ */
+- (nullable MDLMesh*)meshUsingAllocator:(nullable id<MDLMeshBufferAllocator>)allocator;
+
 
 @end
 

```