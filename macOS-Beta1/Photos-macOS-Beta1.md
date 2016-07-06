#Photos.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAdjustmentData.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAdjustmentData.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAdjustmentData.h	2015-08-24 08:23:02.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAdjustmentData.h	2016-06-02 04:02:46.000000000 +0200
@@ -22,4 +22,4 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Photos.framework/Headers/PHContentEditingInput.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Photos.framework/Headers/PHContentEditingInput.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Photos.framework/Headers/PHContentEditingInput.h	2015-08-24 08:23:02.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Photos.framework/Headers/PHContentEditingInput.h	2016-06-02 04:02:46.000000000 +0200
@@ -9,12 +9,14 @@
 #import <Photos/PhotosTypes.h>
 
 @class PHAdjustmentData;
+@class PHLivePhoto;
 @class AVAsset;
 @class CLLocation;
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE_MAC(10_11) @interface PHContentEditingInput : NSObject
+NS_CLASS_AVAILABLE(10_11, 8_0)
+@interface PHContentEditingInput : NSObject
 
 @property (readonly, assign) PHAssetMediaType mediaType;
 @property (readonly, assign) PHAssetMediaSubtype mediaSubtypes;
@@ -23,7 +25,7 @@
 @property (readonly, copy, nullable) NSString *uniformTypeIdentifier;
 
 // Adjustments to be applied onto the provided input image or video.
-@property (readonly, strong) PHAdjustmentData *adjustmentData;
+@property (readonly, strong, nullable) PHAdjustmentData *adjustmentData;
 
 // Input image:
 @property (readonly, strong, nullable) NSImage *displaySizeImage;
@@ -34,6 +36,9 @@
 @property (readonly, strong, nullable) AVAsset *avAsset NS_DEPRECATED_IOS(8_0, 9_0);
 @property (readonly, strong, nullable) AVAsset *audiovisualAsset NS_AVAILABLE(10_11, 9_0);
 
+// Input Live Photo:
+@property (readonly, strong, nullable) PHLivePhoto *livePhoto NS_AVAILABLE(10_12, 10_0);
+
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Photos.framework/Headers/PHContentEditingOutput.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Photos.framework/Headers/PHContentEditingOutput.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Photos.framework/Headers/PHContentEditingOutput.h	2015-08-24 08:23:02.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Photos.framework/Headers/PHContentEditingOutput.h	2016-06-02 04:02:46.000000000 +0200
@@ -11,7 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE_MAC(10_11) @interface PHContentEditingOutput : NSObject
+NS_CLASS_AVAILABLE(10_11, 8_0) @interface PHContentEditingOutput : NSObject
 
 - (instancetype)initWithContentEditingInput:(PHContentEditingInput *)contentEditingInput;
 
@@ -22,4 +22,4 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Photos.framework/Headers/PHLivePhoto.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Photos.framework/Headers/PHLivePhoto.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Photos.framework/Headers/PHLivePhoto.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Photos.framework/Headers/PHLivePhoto.h	2016-06-02 04:02:46.000000000 +0200
@@ -0,0 +1,26 @@
+//
+//  PHLivePhoto.h
+//  Photos
+//
+//  Copyright © 2015 Apple, Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+/*!
+ @class PHLivePhoto
+ @abstract Encapsulate the information needed to display a live photo in a PHLivePhotoView
+ */
+
+NS_CLASS_AVAILABLE(10_12, 9_1) @interface PHLivePhoto : NSObject
+
+- (instancetype)init NS_UNAVAILABLE;
+
+/// The dimensions of the live photo measured in pixels.
+@property (readonly, nonatomic) CGSize size;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Photos.framework/Headers/PHLivePhotoEditingContext.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Photos.framework/Headers/PHLivePhotoEditingContext.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Photos.framework/Headers/PHLivePhotoEditingContext.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Photos.framework/Headers/PHLivePhotoEditingContext.h	2016-06-02 04:02:46.000000000 +0200
@@ -0,0 +1,126 @@
+//
+//  Copyright © 2016 Apple, Inc. All rights reserved.
+//
+
+#import <Photos/PHLivePhoto.h>
+#import <CoreImage/CIImage.h>
+#import <CoreMedia/CMTime.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@protocol PHLivePhotoFrame;
+@class PHContentEditingInput;
+@class PHContentEditingOutput;
+
+/// A block callback for processing frames of a live photo, including the still image
+typedef CIImage * _Nullable (^PHLivePhotoFrameProcessingBlock)(id <PHLivePhotoFrame> _Nonnull frame, NSError * _Nullable * _Nonnull error);
+
+typedef NSString * const PHLivePhotoEditingOption NS_STRING_ENUM;
+
+NS_CLASS_AVAILABLE(10_12, 10_0) @interface PHLivePhotoEditingContext : NSObject
+
+/// Initializer from the specified live photo input
+/// Return nil if the specified input is not for a live photo
+- (nullable instancetype)initWithLivePhotoEditingInput:(PHContentEditingInput *)livePhotoInput NS_DESIGNATED_INITIALIZER;
+- (instancetype)init NS_UNAVAILABLE;
+
+// ------------------------------------------------------------------------
+// Read-only properties
+// ------------------------------------------------------------------------
+
+/// The original full-size image from the input live photo
+@property (readonly) CIImage *fullSizeImage;
+
+/// The duration of the live photo
+@property (readonly) CMTime duration;
+
+/// The time of the still image within the live photo
+@property (readonly) CMTime photoTime;
+
+// The orientation of the live photo
+@property (readonly) CGImagePropertyOrientation orientation;
+
+// ------------------------------------------------------------------------
+// Editable properties
+// ------------------------------------------------------------------------
+
+/// A block that can be set to process each frame of the live photo
+/// Note that the context uses a copy of the processor block during processing
+@property (nullable, copy) PHLivePhotoFrameProcessingBlock frameProcessor;
+
+/// Specify the volume gain of the live photo
+/// Must be between 0.0 and 1.0
+/// Default to 1.0
+@property float audioVolume;
+
+// ------------------------------------------------------------------------
+// Processing
+// ------------------------------------------------------------------------
+
+/// Asynchronously generate a new live photo suitable for playback in a PHLivePhotoView of the specified target size
+/// The options dictionary can contain additional options, see below
+- (void)prepareLivePhotoForPlaybackWithTargetSize:(CGSize)targetSize options:(nullable NSDictionary<PHLivePhotoEditingOption, id> *)options completionHandler:(void(^)(PHLivePhoto * _Nullable livePhoto, NSError * _Nullable error))handler;
+
+/// Asynchronously process and save the edited live photo to the specified content editing output
+/// Options dictionary should be nil, reserved for future expansion
+- (void)saveLivePhotoToOutput:(PHContentEditingOutput *)output options:(nullable NSDictionary<PHLivePhotoEditingOption, id> *)options completionHandler:(void(^)(BOOL success, NSError * _Nullable error))handler;
+
+/// Cancel the current asynchronous operation
+/// This is implicitely called whenever prepare or save is called
+/// A canceled operation will call its completion handler with an appropriate error code of PHLivePhotoEditingErrorCodeAborted
+- (void)cancel;
+
+@end
+
+/// Type of frames in a Live Photo
+typedef NS_ENUM(NSInteger, PHLivePhotoFrameType)
+{
+    /// Indicate the still image
+    PHLivePhotoFrameTypePhoto,
+    
+    /// Indicate a video frame
+    PHLivePhotoFrameTypeVideo,
+} NS_ENUM_AVAILABLE(10_12, 10_0);
+
+/// Protocol that describes a single frame of a live photo
+NS_CLASS_AVAILABLE(10_12, 10_0) @protocol PHLivePhotoFrame <NSObject>
+
+/// Input image for the frame
+@property (readonly) CIImage *image;
+
+/// The time of the frame relative to the beginning of the live photo
+@property (readonly) CMTime time;
+
+/// The type of frame (photo or video)
+@property (nonatomic, readonly) PHLivePhotoFrameType type;
+
+/// The scale of the frame relative to the full-size image
+@property (readonly) CGFloat renderScale;
+
+@end
+
+// ------------------------------------------------------------------------
+// Options that can be set during processing
+// ------------------------------------------------------------------------
+
+/// Indicates whether processing should happen at playback time
+/// If set to NO (the default) the live photo will always be rendered before playback
+/// If set to YES, the editing context might still choose to render first for performance reasons
+/// This option is ignored by the saveLivePhotoToOutput method
+extern PHLivePhotoEditingOption PHLivePhotoShouldRenderAtPlaybackTime NS_AVAILABLE(10_12, 10_0);
+
+// ------------------------------------------------------------------------
+// Errors
+// ------------------------------------------------------------------------
+
+/// The error domain for all Live Photo Editing errors
+extern NSString * const PHLivePhotoEditingErrorDomain NS_AVAILABLE(10_12, 10_0);
+
+/// Error code for Live Photo Editing errors
+typedef NS_ENUM(NSInteger, PHLivePhotoEditingErrorCode)
+{
+    PHLivePhotoEditingErrorCodeUnknown,
+    PHLivePhotoEditingErrorCodeAborted,
+} NS_AVAILABLE(10_12, 10_0);
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Photos.framework/Headers/Photos.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Photos.framework/Headers/Photos.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Photos.framework/Headers/Photos.h	2015-08-24 08:23:02.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Photos.framework/Headers/Photos.h	2016-06-02 04:02:46.000000000 +0200
@@ -11,3 +11,5 @@
 #import <Photos/PHContentEditingInput.h>
 #import <Photos/PHContentEditingOutput.h>
 #import <Photos/PHAdjustmentData.h>
+#import <Photos/PHLivePhoto.h>
+#import <Photos/PHLivePhotoEditingContext.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Photos.framework/Headers/PhotosTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Photos.framework/Headers/PhotosTypes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Photos.framework/Headers/PhotosTypes.h	2015-08-24 08:23:02.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Photos.framework/Headers/PhotosTypes.h	2016-06-02 04:02:46.000000000 +0200
@@ -5,12 +5,105 @@
 //  Copyright (c) 2014 Apple Inc. All rights reserved.
 //
 
+#ifndef Photos_PhotosTypes_h
+#define Photos_PhotosTypes_h
+
+#pragma mark - PHCollectionListTypes
+
+typedef NS_ENUM(NSInteger, PHImageContentMode) {
+    PHImageContentModeAspectFit = 0,
+    PHImageContentModeAspectFill = 1,
+    PHImageContentModeDefault = PHImageContentModeAspectFit
+} NS_ENUM_AVAILABLE(10_11, 8_0);
+
+typedef NS_ENUM(NSInteger, PHCollectionListType) {
+    PHCollectionListTypeMomentList    = 1,
+    PHCollectionListTypeFolder        = 2,
+    PHCollectionListTypeSmartFolder   = 3,
+} NS_ENUM_AVAILABLE(10_11, 8_0);
+
+typedef NS_ENUM(NSInteger, PHCollectionListSubtype) {
+    
+    // PHCollectionListTypeMomentList subtypes
+    PHCollectionListSubtypeMomentListCluster    = 1,
+    PHCollectionListSubtypeMomentListYear       = 2,
+    
+    // PHCollectionListTypeFolder subtypes
+    PHCollectionListSubtypeRegularFolder        = 100,
+    
+    // PHCollectionListTypeSmartFolder subtypes
+    PHCollectionListSubtypeSmartFolderEvents    = 200,
+    PHCollectionListSubtypeSmartFolderFaces     = 201,
+    
+    // Used for fetching if you don't care about the exact subtype
+    PHCollectionListSubtypeAny = NSIntegerMax
+} NS_ENUM_AVAILABLE(10_11, 8_0);
+
+#pragma mark - PHCollection types
+
+typedef NS_ENUM(NSInteger, PHCollectionEditOperation) {
+    PHCollectionEditOperationDeleteContent    = 1, // Delete things it contains
+    PHCollectionEditOperationRemoveContent    = 2, // Remove things it contains, they're not deleted from the library
+    PHCollectionEditOperationAddContent       = 3, // Add things from other collection
+    PHCollectionEditOperationCreateContent    = 4, // Create new things, or duplicate them from others in the same container
+    PHCollectionEditOperationRearrangeContent = 5, // Change the order of things
+    PHCollectionEditOperationDelete           = 6, // Deleting of the container, not the content
+    PHCollectionEditOperationRename           = 7, // Renaming of the container, not the content
+} NS_AVAILABLE(10_11, 8_0);
+
+#pragma mark - PHAssetCollection types
+
+typedef NS_ENUM(NSInteger, PHAssetCollectionType) {
+    PHAssetCollectionTypeAlbum      = 1,
+    PHAssetCollectionTypeSmartAlbum = 2,
+    PHAssetCollectionTypeMoment     = 3,
+} NS_ENUM_AVAILABLE(10_11, 8_0);
+
+typedef NS_ENUM(NSInteger, PHAssetCollectionSubtype) {
+    
+    // PHAssetCollectionTypeAlbum regular subtypes
+    PHAssetCollectionSubtypeAlbumRegular         = 2,
+    PHAssetCollectionSubtypeAlbumSyncedEvent     = 3,
+    PHAssetCollectionSubtypeAlbumSyncedFaces     = 4,
+    PHAssetCollectionSubtypeAlbumSyncedAlbum     = 5,
+    PHAssetCollectionSubtypeAlbumImported        = 6,
+    
+    // PHAssetCollectionTypeAlbum shared subtypes
+    PHAssetCollectionSubtypeAlbumMyPhotoStream   = 100,
+    PHAssetCollectionSubtypeAlbumCloudShared     = 101,
+    
+    // PHAssetCollectionTypeSmartAlbum subtypes
+    PHAssetCollectionSubtypeSmartAlbumGeneric    = 200,
+    PHAssetCollectionSubtypeSmartAlbumPanoramas  = 201,
+    PHAssetCollectionSubtypeSmartAlbumVideos     = 202,
+    PHAssetCollectionSubtypeSmartAlbumFavorites  = 203,
+    PHAssetCollectionSubtypeSmartAlbumTimelapses = 204,
+    PHAssetCollectionSubtypeSmartAlbumAllHidden  = 205,
+    PHAssetCollectionSubtypeSmartAlbumRecentlyAdded = 206,
+    PHAssetCollectionSubtypeSmartAlbumBursts     = 207,
+    PHAssetCollectionSubtypeSmartAlbumSlomoVideos = 208,
+    PHAssetCollectionSubtypeSmartAlbumUserLibrary = 209,
+    PHAssetCollectionSubtypeSmartAlbumSelfPortraits NS_AVAILABLE(10_11, 9_0) = 210,
+    PHAssetCollectionSubtypeSmartAlbumScreenshots NS_AVAILABLE(10_11, 9_0) = 211,
+    
+    // Used for fetching, if you don't care about the exact subtype
+    PHAssetCollectionSubtypeAny = NSIntegerMax
+} NS_ENUM_AVAILABLE(10_11, 8_0);
+
+#pragma mark - PHAsset types
+
+typedef NS_ENUM(NSInteger, PHAssetEditOperation) {
+    PHAssetEditOperationDelete     = 1,
+    PHAssetEditOperationContent    = 2,
+    PHAssetEditOperationProperties = 3,
+} NS_AVAILABLE(10_11, 8_0);
+
 typedef NS_ENUM(NSInteger, PHAssetMediaType) {
-	PHAssetMediaTypeUnknown = 0,
-	PHAssetMediaTypeImage,
-	PHAssetMediaTypeVideo,
-	PHAssetMediaTypeAudio,
-} NS_ENUM_AVAILABLE_MAC(10_11);
+    PHAssetMediaTypeUnknown = 0,
+    PHAssetMediaTypeImage   = 1,
+    PHAssetMediaTypeVideo   = 2,
+    PHAssetMediaTypeAudio   = 3,
+} NS_ENUM_AVAILABLE(10_11, 8_0);
 
 typedef NS_OPTIONS(NSUInteger, PHAssetMediaSubtype) {
     PHAssetMediaSubtypeNone               = 0,
@@ -18,11 +111,38 @@
     // Photo subtypes
     PHAssetMediaSubtypePhotoPanorama      = (1UL << 0),
     PHAssetMediaSubtypePhotoHDR           = (1UL << 1),
-	PHAssetMediaSubtypePhotoScreenshot    = (1UL << 2),
+    PHAssetMediaSubtypePhotoScreenshot NS_AVAILABLE(10_11, 9_0) = (1UL << 2),
+    PHAssetMediaSubtypePhotoLive NS_AVAILABLE(10_11, 9_1) = (1UL << 3),
     
     // Video subtypes
     PHAssetMediaSubtypeVideoStreamed      = (1UL << 16),
     PHAssetMediaSubtypeVideoHighFrameRate = (1UL << 17),
     PHAssetMediaSubtypeVideoTimelapse     = (1UL << 18),
-} NS_ENUM_AVAILABLE_MAC(10_11);
+} NS_AVAILABLE(10_11, 8_0);
+
+typedef NS_OPTIONS(NSUInteger, PHAssetBurstSelectionType) {
+    PHAssetBurstSelectionTypeNone     = 0,
+    PHAssetBurstSelectionTypeAutoPick = (1UL << 0),
+    PHAssetBurstSelectionTypeUserPick = (1UL << 1),
+} NS_AVAILABLE(10_11, 8_0);
+
+typedef NS_OPTIONS(NSUInteger, PHAssetSourceType) {
+    PHAssetSourceTypeNone            = 0,
+    PHAssetSourceTypeUserLibrary     = (1UL << 0),
+    PHAssetSourceTypeCloudShared     = (1UL << 1),
+    PHAssetSourceTypeiTunesSynced    = (1UL << 2),
+} NS_AVAILABLE(10_11, 9_0);
+
+typedef NS_ENUM(NSInteger, PHAssetResourceType) {
+    PHAssetResourceTypePhoto                                = 1,
+    PHAssetResourceTypeVideo                                = 2,
+    PHAssetResourceTypeAudio                                = 3,
+    PHAssetResourceTypeAlternatePhoto                       = 4,
+    PHAssetResourceTypeFullSizePhoto                        = 5,
+    PHAssetResourceTypeFullSizeVideo                        = 6,
+    PHAssetResourceTypeAdjustmentData                       = 7,
+    PHAssetResourceTypeAdjustmentBasePhoto                  = 8,
+    PHAssetResourceTypePairedVideo NS_AVAILABLE(10_11,9_1)  = 9,
+} NS_ENUM_AVAILABLE(10_11, 9_0);
 
+#endif

```