#Photos.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAdjustmentData.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAdjustmentData.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAdjustmentData.h	2015-10-03 02:14:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAdjustmentData.h	2016-06-01 05:08:28.000000000 +0200
@@ -6,10 +6,11 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <Photos/PhotosDefines.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHAdjustmentData : NSObject
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHAdjustmentData : NSObject
 
 - (instancetype)initWithFormatIdentifier:(NSString *)formatIdentifier formatVersion:(NSString *)formatVersion data:(NSData *)data;
 
@@ -22,4 +23,4 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAsset.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAsset.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAsset.h	2015-10-03 02:14:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAsset.h	2016-06-01 05:08:28.000000000 +0200
@@ -9,17 +9,21 @@
 #import <Photos/PhotosTypes.h>
 #import <Photos/PHFetchResult.h>
 #import <Photos/PHPhotoLibrary.h>
+#import <Photos/PhotosDefines.h>
 
 #import <UIKit/UIImage.h>
 #import <ImageIO/ImageIO.h>
 #import <CoreLocation/CLLocation.h>
 
+
 @class PHFetchOptions;
 @class PHAssetCollection;
+@class PHPerson;
+@class PHFaceCollection;
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHAsset : PHObject
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHAsset : PHObject
 
 #pragma mark - Properties
 
@@ -45,7 +49,7 @@
 @property (nonatomic, assign, readonly) PHAssetBurstSelectionType burstSelectionTypes;
 @property (nonatomic, assign, readonly) BOOL representsBurst;
 
-@property (nonatomic, assign, readonly) PHAssetSourceType sourceType NS_AVAILABLE_IOS(9_0);
+@property (nonatomic, assign, readonly) PHAssetSourceType sourceType PHOTOS_AVAILABLE_IOS_TVOS(9_0, 10_0);
 
 #pragma mark - Capabilities
 
@@ -67,4 +71,4 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetChangeRequest.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetChangeRequest.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetChangeRequest.h	2015-10-03 02:14:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetChangeRequest.h	2016-06-01 05:08:28.000000000 +0200
@@ -9,6 +9,7 @@
 
 #import <Photos/PHAsset.h>
 #import <Photos/PHContentEditingOutput.h>
+#import <Photos/PhotosDefines.h>
 
 @class UIImage;
 @class CLLocation;
@@ -19,7 +20,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 // PHAssetChangeRequest can only be created or used within a -[PHPhotoLibrary performChanges:] or -[PHPhotoLibrary performChangesAndWait:] block.
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHAssetChangeRequest : NSObject
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHAssetChangeRequest : NSObject
 
 #pragma mark - Creating Assets
 
@@ -57,9 +58,9 @@
 @end
 
 
-typedef NSUInteger PHContentEditingInputRequestID NS_AVAILABLE_IOS(8_0);
+typedef NSUInteger PHContentEditingInputRequestID PHOTOS_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHContentEditingInputRequestOptions : NSObject
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHContentEditingInputRequestOptions : NSObject
 
 // Block to be provided by the client, used to determine if the given adjustment data can be handled (i.e. can be decoded and rendered).
 @property (nonatomic, copy) BOOL (^canHandleAdjustmentData)(PHAdjustmentData *adjustmentData);
@@ -74,15 +75,15 @@
 @interface PHAsset (PHContentEditingInput)
 
 // Completion and progress handlers are called on an arbitrary serial queue.
-- (PHContentEditingInputRequestID)requestContentEditingInputWithOptions:(nullable PHContentEditingInputRequestOptions *)options completionHandler:(void (^)(PHContentEditingInput *__nullable contentEditingInput, NSDictionary *info))completionHandler NS_AVAILABLE_IOS(8_0);
-- (void)cancelContentEditingInputRequest:(PHContentEditingInputRequestID)requestID NS_AVAILABLE_IOS(8_0);
+- (PHContentEditingInputRequestID)requestContentEditingInputWithOptions:(nullable PHContentEditingInputRequestOptions *)options completionHandler:(void (^)(PHContentEditingInput *__nullable contentEditingInput, NSDictionary *info))completionHandler PHOTOS_AVAILABLE_IOS_TVOS(8_0, 10_0);
+- (void)cancelContentEditingInputRequest:(PHContentEditingInputRequestID)requestID PHOTOS_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
 @end
 
 // Completion handler info dictionary keys
-extern NSString *const PHContentEditingInputResultIsInCloudKey NS_AVAILABLE_IOS(8_0);
-extern NSString *const PHContentEditingInputCancelledKey NS_AVAILABLE_IOS(8_0);
-extern NSString *const PHContentEditingInputErrorKey NS_AVAILABLE_IOS(8_0);
+extern NSString *const PHContentEditingInputResultIsInCloudKey PHOTOS_AVAILABLE_IOS_TVOS(8_0, 10_0);
+extern NSString *const PHContentEditingInputCancelledKey PHOTOS_AVAILABLE_IOS_TVOS(8_0, 10_0);
+extern NSString *const PHContentEditingInputErrorKey PHOTOS_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
 
 @interface PHContentEditingOutput (PHAssetChangeRequest)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetCollectionChangeRequest.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetCollectionChangeRequest.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetCollectionChangeRequest.h	2015-10-03 02:14:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetCollectionChangeRequest.h	2016-06-01 05:08:28.000000000 +0200
@@ -50,4 +50,4 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetCreationRequest.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetCreationRequest.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetCreationRequest.h	2015-10-03 02:14:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetCreationRequest.h	2016-06-01 05:08:28.000000000 +0200
@@ -7,12 +7,13 @@
 
 #import <Photos/PhotosTypes.h>
 #import <Photos/PHAssetChangeRequest.h>
+#import <Photos/PhotosDefines.h>
 
 #import <Foundation/Foundation.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE_IOS(9_0) @interface PHAssetResourceCreationOptions : NSObject <NSCopying>
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(9_0, 10_0) @interface PHAssetResourceCreationOptions : NSObject <NSCopying>
 
 // The filename for the resource. If not specified, one will be inferred from a fileURL if available, or else generated.
 @property (nonatomic, copy, nullable) NSString *originalFilename;
@@ -27,7 +28,7 @@
 
 
 // PHAssetCreationRequest can only be created or used within a -[PHPhotoLibrary performChanges:] or -[PHPhotoLibrary performChangesAndWait:] block.
-NS_CLASS_AVAILABLE_IOS(9_0) @interface PHAssetCreationRequest : PHAssetChangeRequest
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(9_0, 10_0) @interface PHAssetCreationRequest : PHAssetChangeRequest
 
 + (instancetype)creationRequestForAsset;
 
@@ -41,4 +42,4 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetResource.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetResource.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetResource.h	2015-10-03 02:14:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetResource.h	2016-06-01 05:08:28.000000000 +0200
@@ -6,13 +6,14 @@
 //
 
 #import <Photos/PhotosTypes.h>
+#import <Photos/PhotosDefines.h>
 
 @class PHAsset;
 @class PHLivePhoto;
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE_IOS(9_0) @interface PHAssetResource : NSObject
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(9_0, 10_0) @interface PHAssetResource : NSObject
 
 @property (nonatomic, assign, readonly) PHAssetResourceType type;
 @property (nonatomic, copy, readonly) NSString *assetLocalIdentifier;
@@ -22,8 +23,8 @@
 #pragma mark - Getting resources
 
 + (NSArray<PHAssetResource *> *)assetResourcesForAsset:(PHAsset *)asset;
-+ (NSArray<PHAssetResource *> *)assetResourcesForLivePhoto:(PHLivePhoto *)livePhoto NS_AVAILABLE_IOS(9_1);
++ (NSArray<PHAssetResource *> *)assetResourcesForLivePhoto:(PHLivePhoto *)livePhoto PHOTOS_AVAILABLE_IOS_TVOS(9_1, 10_0);
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetResourceManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetResourceManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetResourceManager.h	2015-10-03 02:14:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetResourceManager.h	2016-06-01 05:08:28.000000000 +0200
@@ -6,27 +6,28 @@
 //
 
 #import <Photos/PhotosTypes.h>
+#import <Photos/PhotosDefines.h>
 
 
 // Uniquely identify a resource data request
-typedef int32_t PHAssetResourceDataRequestID NS_AVAILABLE_IOS(9_0);
+typedef int32_t PHAssetResourceDataRequestID PHOTOS_AVAILABLE_IOS_TVOS(9_0, 10_0);
 static const PHAssetResourceDataRequestID PHInvalidAssetResourceDataRequestID = 0;
 
 // Progress handler, called in an arbitrary serial queue.
-typedef void (^PHAssetResourceProgressHandler)(double progress) NS_AVAILABLE_IOS(9_0);
+typedef void (^PHAssetResourceProgressHandler)(double progress) PHOTOS_AVAILABLE_IOS_TVOS(9_0, 10_0);
 
 @class PHAssetResource;
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE_IOS(9_0) @interface PHAssetResourceRequestOptions : NSObject <NSCopying>
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(9_0, 10_0) @interface PHAssetResourceRequestOptions : NSObject <NSCopying>
 
 @property (nonatomic, assign, getter=isNetworkAccessAllowed) BOOL networkAccessAllowed;
 @property (nonatomic, copy, nullable) PHAssetResourceProgressHandler progressHandler;
 
 @end
 
-NS_CLASS_AVAILABLE_IOS(9_0) @interface PHAssetResourceManager : NSObject
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(9_0, 10_0) @interface PHAssetResourceManager : NSObject
 
 + (PHAssetResourceManager *)defaultManager;
 
@@ -46,4 +47,4 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHChange.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHChange.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHChange.h	2015-10-03 02:14:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHChange.h	2016-06-01 05:08:28.000000000 +0200
@@ -6,6 +6,7 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <Photos/PhotosDefines.h>
 
 @class PHObject;
 @class PHObjectChangeDetails;
@@ -14,7 +15,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHChange : NSObject
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHChange : NSObject
 
 - (nullable PHObjectChangeDetails *)changeDetailsForObject:(PHObject *)object;
 - (nullable PHFetchResultChangeDetails *)changeDetailsForFetchResult:(PHFetchResult *)object;
@@ -23,7 +24,7 @@
 
 
 
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHObjectChangeDetails : NSObject
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHObjectChangeDetails : NSObject
 
 // the object in the state before this change (returns the object that was passed in to changeDetailsForObject:)
 @property (atomic, strong, readonly) __kindof PHObject *objectBeforeChanges;
@@ -41,7 +42,7 @@
 
 
 
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHFetchResultChangeDetails : NSObject
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHFetchResultChangeDetails : NSObject
 
 // fetch result with the state of the fetched objects before this change (returns the fetch result passed in to changeDetailsForFetchResult:)
 @property (atomic, strong, readonly) PHFetchResult *fetchResultBeforeChanges;
@@ -81,4 +82,4 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHCollection.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHCollection.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHCollection.h	2015-10-03 02:14:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHCollection.h	2016-06-01 05:08:28.000000000 +0200
@@ -8,13 +8,14 @@
 #import <Photos/PHObject.h>
 #import <Photos/PHFetchResult.h>
 #import <Photos/PhotosTypes.h>
+#import <Photos/PhotosDefines.h>
 
 @class PHAsset, PHCollectionList, PHFetchResult, PHFetchOptions;
 @class CLLocation;
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHCollection : PHObject
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHCollection : PHObject
 
 @property (nonatomic, assign, readonly) BOOL canContainAssets;
 @property (nonatomic, assign, readonly) BOOL canContainCollections;
@@ -33,7 +34,7 @@
 @end
 
 
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHAssetCollection : PHCollection
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHAssetCollection : PHCollection
 
 @property (nonatomic, assign, readonly) PHAssetCollectionType assetCollectionType;
 @property (nonatomic, assign, readonly) PHAssetCollectionSubtype assetCollectionSubtype;
@@ -50,7 +51,10 @@
 
 #pragma mark - Fetching asset collections
 
+// Fetch asset collections of a single type matching the provided local identifiers (type is inferred from the local identifiers)
 + (PHFetchResult<PHAssetCollection *> *)fetchAssetCollectionsWithLocalIdentifiers:(NSArray<NSString *> *)identifiers options:(nullable PHFetchOptions *)options;
+
+// Fetch asset collections of a single type and subtype provided (use PHAssetCollectionSubtypeAny to match all subtypes)
 + (PHFetchResult<PHAssetCollection *> *)fetchAssetCollectionsWithType:(PHAssetCollectionType)type subtype:(PHAssetCollectionSubtype)subtype options:(nullable PHFetchOptions *)options;
 
 // Smart Albums are not supported, only Albums and Moments
@@ -76,7 +80,7 @@
 @end
 
 
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHCollectionList : PHCollection
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHCollectionList : PHCollection
 
 @property (nonatomic, assign, readonly) PHCollectionListType collectionListType;
 @property (nonatomic, assign, readonly) PHCollectionListSubtype collectionListSubtype;
@@ -92,7 +96,11 @@
 // A PHAssetCollectionTypeMoment will be contained by a PHCollectionListSubtypeMomentListCluster and a PHCollectionListSubtypeMomentListYear
 // Non-moment PHAssetCollections will only be contained by a single collection list
 + (PHFetchResult<PHCollectionList *> *)fetchCollectionListsContainingCollection:(PHCollection *)collection options:(nullable PHFetchOptions *)options;
+
+// Fetch collection lists of a single type matching the provided local identifiers (type is inferred from the local identifiers)
 + (PHFetchResult<PHCollectionList *> *)fetchCollectionListsWithLocalIdentifiers:(NSArray<NSString *> *)identifiers options:(nullable PHFetchOptions *)options;
+
+// Fetch asset collections of a single type and subtype provided (use PHCollectionListSubtypeAny to match all subtypes)
 + (PHFetchResult<PHCollectionList *> *)fetchCollectionListsWithType:(PHCollectionListType)collectionListType subtype:(PHCollectionListSubtype)subtype options:(nullable PHFetchOptions *)options;
 
 
@@ -110,4 +118,4 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHCollectionListChangeRequest.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHCollectionListChangeRequest.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHCollectionListChangeRequest.h	2015-10-03 02:14:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHCollectionListChangeRequest.h	2016-06-01 05:08:28.000000000 +0200
@@ -6,6 +6,7 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <Photos/PhotosDefines.h>
 
 @class PHFetchResult;
 @class PHCollection;
@@ -15,7 +16,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 // PHCollectionListChangeRequest can only be created or used within a -[PHPhotoLibrary performChanges:] or -[PHPhotoLibrary performChangesAndWait:] block.
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHCollectionListChangeRequest : NSObject
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHCollectionListChangeRequest : NSObject
 
 #pragma mark - Creating Collection Lists
 
@@ -54,4 +55,4 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHContentEditingInput.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHContentEditingInput.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHContentEditingInput.h	2015-10-03 02:14:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHContentEditingInput.h	2016-06-01 05:08:28.000000000 +0200
@@ -8,14 +8,16 @@
 #import <Foundation/Foundation.h>
 #import <UIKit/UIImage.h>
 #import <Photos/PhotosTypes.h>
+#import <Photos/PhotosDefines.h>
 
 @class PHAdjustmentData;
 @class AVAsset, AVAudioMix, AVVideoComposition;
 @class CLLocation;
+@class PHLivePhoto;
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHContentEditingInput : NSObject
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHContentEditingInput : NSObject
 
 @property (readonly, assign) PHAssetMediaType mediaType;
 @property (readonly, assign) PHAssetMediaSubtype mediaSubtypes;
@@ -24,7 +26,7 @@
 @property (readonly, copy, nullable) NSString *uniformTypeIdentifier;
 
 // Adjustments to be applied onto the provided input image or video.
-@property (readonly, strong) PHAdjustmentData *adjustmentData;
+@property (readonly, strong, nullable) PHAdjustmentData *adjustmentData;
 
 // Input image:
 @property (readonly, strong, nullable) UIImage *displaySizeImage;
@@ -33,8 +35,11 @@
 
 // Input video:
 @property (readonly, strong, nullable) AVAsset *avAsset NS_DEPRECATED_IOS(8_0, 9_0);
-@property (readonly, strong, nullable) AVAsset *audiovisualAsset NS_AVAILABLE(NA, 9_0);
+@property (readonly, strong, nullable) AVAsset *audiovisualAsset PHOTOS_AVAILABLE_IOS_TVOS_OSX(9_0, 10_0, NA);
+
+// Input Live Photo:
+@property (readonly, strong, nullable) PHLivePhoto *livePhoto NS_AVAILABLE_IOS(10_0);
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHContentEditingOutput.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHContentEditingOutput.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHContentEditingOutput.h	2015-10-03 02:14:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHContentEditingOutput.h	2016-06-01 05:08:28.000000000 +0200
@@ -6,12 +6,13 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <Photos/PhotosDefines.h>
 
 @class PHContentEditingInput, PHAdjustmentData;
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHContentEditingOutput : NSObject
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHContentEditingOutput : NSObject
 
 - (instancetype)initWithContentEditingInput:(PHContentEditingInput *)contentEditingInput;
 
@@ -22,4 +23,4 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHFetchOptions.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHFetchOptions.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHFetchOptions.h	2015-10-03 02:14:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHFetchOptions.h	2016-06-01 05:08:28.000000000 +0200
@@ -7,12 +7,13 @@
 
 #import <Foundation/Foundation.h>
 #import <Photos/PhotosTypes.h>
+#import <Photos/PhotosDefines.h>
 
 @class PHObject;
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHFetchOptions : NSObject <NSCopying>
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHFetchOptions : NSObject <NSCopying>
 
 // Some predicates / sorts may be suboptimal and we will log
 @property (nonatomic, strong, nullable) NSPredicate *predicate;
@@ -26,10 +27,10 @@
 
 // The asset source types included in the fetch results.  Defaults to PHAssetSourceTypeNone.
 // If set to PHAssetSourceTypeNone the asset source types included in the fetch results are inferred from the type of query performed (see PHAsset fetchAssetsWithOptions:)
-@property (nonatomic, assign) PHAssetSourceType includeAssetSourceTypes NS_AVAILABLE_IOS(9_0);
+@property (nonatomic, assign) PHAssetSourceType includeAssetSourceTypes PHOTOS_AVAILABLE_IOS_TVOS(9_0, 10_0);
 
 // Limits the maximum number of objects returned in the fetch result, a value of 0 means no limit.  Defaults to 0.
-@property (nonatomic, assign, readwrite) NSUInteger fetchLimit NS_AVAILABLE_IOS(9_0);
+@property (nonatomic, assign, readwrite) NSUInteger fetchLimit PHOTOS_AVAILABLE_IOS_TVOS(9_0, 10_0);
 
 // Whether the owner of this object is interested in incremental change details for the results of this fetch (see PHChange)
 // Defaults to YES
@@ -37,4 +38,4 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHFetchResult.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHFetchResult.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHFetchResult.h	2015-10-03 02:14:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHFetchResult.h	2016-06-01 05:08:28.000000000 +0200
@@ -7,12 +7,13 @@
 
 #import <Foundation/Foundation.h>
 #import <Photos/PhotosTypes.h>
+#import <Photos/PhotosDefines.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
 // Accessing fetched results (fetches objects from the backing store in chunks on demand rather than all at once)
 // Fetched objects will be kept in a cache and purged under memory pressure
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHFetchResult<ObjectType> : NSObject <NSCopying, NSFastEnumeration>
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHFetchResult<ObjectType> : NSObject <NSCopying, NSFastEnumeration>
 
 @property (readonly) NSUInteger count;
 - (ObjectType)objectAtIndex:(NSUInteger)index;
@@ -36,4 +37,4 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHImageManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHImageManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHImageManager.h	2015-10-03 02:14:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHImageManager.h	2016-05-27 07:17:26.000000000 +0200
@@ -8,6 +8,7 @@
 #import <AVFoundation/AVFoundation.h>
 #import <UIKit/UIKit.h>
 #import <Photos/PhotosTypes.h>
+#import <Photos/PhotosDefines.h>
 
 @class PHAsset;
 @class PHLivePhoto;
@@ -20,24 +21,24 @@
     PHImageRequestOptionsVersionCurrent = 0, // version with edits (aka adjustments) rendered or unadjusted version if there is no edits
     PHImageRequestOptionsVersionUnadjusted, // original version without any adjustments
     PHImageRequestOptionsVersionOriginal // original version, in the case of a combined format the highest fidelity format will be returned (e.g. RAW for a RAW+JPG source image)
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} PHOTOS_ENUM_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
 typedef NS_ENUM(NSInteger, PHImageRequestOptionsDeliveryMode) {
     PHImageRequestOptionsDeliveryModeOpportunistic = 0, // client may get several image results when the call is asynchronous or will get one result when the call is synchronous
     PHImageRequestOptionsDeliveryModeHighQualityFormat = 1, // client will get one result only and it will be as asked or better than asked (sync requests are automatically processed this way regardless of the specified mode)
     PHImageRequestOptionsDeliveryModeFastFormat = 2 // client will get one result only and it may be degraded
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} PHOTOS_ENUM_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
 typedef NS_ENUM(NSInteger, PHImageRequestOptionsResizeMode) {
     PHImageRequestOptionsResizeModeNone = 0, // no resize
     PHImageRequestOptionsResizeModeFast, // use targetSize as a hint for optimal decoding when the source image is a compressed format (i.e. subsampling), the delivered image may be larger than targetSize
     PHImageRequestOptionsResizeModeExact, // same as above but also guarantees the delivered image is exactly targetSize (must be set when a normalizedCropRect is specified)
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} PHOTOS_ENUM_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
 // Progress handler, called in an arbitrary serial queue. Only called when the data is not available locally and is retrieved from iCloud.
-typedef void (^ PHAssetImageProgressHandler)(double progress, NSError *__nullable error, BOOL *stop, NSDictionary *__nullable info) NS_AVAILABLE_IOS(8_0);
+typedef void (^ PHAssetImageProgressHandler)(double progress, NSError *__nullable error, BOOL *stop, NSDictionary *__nullable info) PHOTOS_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHImageRequestOptions : NSObject <NSCopying>
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHImageRequestOptions : NSObject <NSCopying>
 
 @property (nonatomic, assign) PHImageRequestOptionsVersion version; // version
 @property (nonatomic, assign) PHImageRequestOptionsDeliveryMode deliveryMode; // delivery mode. Defaults to PHImageRequestOptionsDeliveryModeOpportunistic
@@ -50,8 +51,9 @@
 @end
 
 
-NS_CLASS_AVAILABLE_IOS(9_1) @interface PHLivePhotoRequestOptions : NSObject <NSCopying>
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(9_1, 10_0) @interface PHLivePhotoRequestOptions : NSObject <NSCopying>
 
+@property (nonatomic, assign) PHImageRequestOptionsVersion version; // version
 @property (nonatomic, assign) PHImageRequestOptionsDeliveryMode deliveryMode;
 @property (nonatomic, assign, getter=isNetworkAccessAllowed) BOOL networkAccessAllowed;
 @property (nonatomic, copy, nullable) PHAssetImageProgressHandler progressHandler;
@@ -64,19 +66,19 @@
 typedef NS_ENUM(NSInteger, PHVideoRequestOptionsVersion) {
     PHVideoRequestOptionsVersionCurrent = 0, // version with edits (aka adjustments) rendered or unadjusted version if there is no edits
     PHVideoRequestOptionsVersionOriginal // original version
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} PHOTOS_ENUM_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
 typedef NS_ENUM(NSInteger, PHVideoRequestOptionsDeliveryMode) { // only apply with PHVideoRequestOptionsVersionCurrent
     PHVideoRequestOptionsDeliveryModeAutomatic = 0, // let us pick the quality (typ. PHVideoRequestOptionsDeliveryModeMediumQualityFormat for streamed AVPlayerItem or AVAsset, or PHVideoRequestOptionsDeliveryModeHighQualityFormat for AVAssetExportSession)
     PHVideoRequestOptionsDeliveryModeHighQualityFormat = 1, // best quality
     PHVideoRequestOptionsDeliveryModeMediumQualityFormat = 2, // medium quality (typ. 720p MP4), currently only supported for AVPlayerItem or AVAsset when streaming from iCloud (will systematically default to PHVideoRequestOptionsDeliveryModeHighQualityFormat if locally available)
     PHVideoRequestOptionsDeliveryModeFastFormat = 3 // fastest available (typ. 360p MP4), currently only supported for AVPlayerItem or AVAsset when streaming from iCloud (will systematically default to PHVideoRequestOptionsDeliveryModeHighQualityFormat if locally available)
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} PHOTOS_ENUM_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
 // Progress handler, called in an arbitrary serial queue: only called when the data is not available locally and is retrieved from iCloud
-typedef void (^PHAssetVideoProgressHandler)(double progress, NSError *__nullable error, BOOL *stop, NSDictionary *__nullable info) NS_AVAILABLE_IOS(8_0);
+typedef void (^PHAssetVideoProgressHandler)(double progress, NSError *__nullable error, BOOL *stop, NSDictionary *__nullable info) PHOTOS_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHVideoRequestOptions : NSObject
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHVideoRequestOptions : NSObject
 
 @property (nonatomic, assign, getter=isNetworkAccessAllowed) BOOL networkAccessAllowed;
 @property (nonatomic, assign) PHVideoRequestOptionsVersion version;
@@ -90,22 +92,22 @@
 #pragma mark - PHImageManager - Fetching
 
 // Uniquely identify a cancellable async request
-typedef int32_t PHImageRequestID NS_AVAILABLE_IOS(8_0);
+typedef int32_t PHImageRequestID PHOTOS_AVAILABLE_IOS_TVOS(8_0, 10_0);
 static const PHImageRequestID PHInvalidImageRequestID = 0;
 
 // Size to pass when requesting the original image or the largest rendered image available (resizeMode will be ignored)
-extern CGSize const PHImageManagerMaximumSize NS_AVAILABLE_IOS(8_0);
+extern CGSize const PHImageManagerMaximumSize PHOTOS_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
 // Result's handler info dictionary keys
-extern NSString *const PHImageResultIsInCloudKey NS_AVAILABLE_IOS(8_0); // key (NSNumber): result is in iCloud, meaning a new request will need to get issued (with networkAccessAllowed set) to get the result
-extern NSString *const PHImageResultIsDegradedKey NS_AVAILABLE_IOS(8_0); // key (NSNumber): result  is a degraded image (only with async requests), meaning other images will be sent unless the request is cancelled in the meanwhile (note that the other request may fail if, for example, data is not available locally and networkAccessAllowed was not specified)
-extern NSString *const PHImageResultRequestIDKey NS_AVAILABLE_IOS(8_0); // key (NSNumber): Request ID of the request for this result
-extern NSString *const PHImageCancelledKey NS_AVAILABLE_IOS(8_0); // key (NSNumber): result is not available because the request was cancelled
-extern NSString *const PHImageErrorKey NS_AVAILABLE_IOS(8_0); // key (NSError): NSFileManager or iCloud Photo Library errors
+extern NSString *const PHImageResultIsInCloudKey PHOTOS_AVAILABLE_IOS_TVOS(8_0, 10_0); // key (NSNumber): result is in iCloud, meaning a new request will need to get issued (with networkAccessAllowed set) to get the result
+extern NSString *const PHImageResultIsDegradedKey PHOTOS_AVAILABLE_IOS_TVOS(8_0, 10_0); // key (NSNumber): result  is a degraded image (only with async requests), meaning other images will be sent unless the request is cancelled in the meanwhile (note that the other request may fail if, for example, data is not available locally and networkAccessAllowed was not specified)
+extern NSString *const PHImageResultRequestIDKey PHOTOS_AVAILABLE_IOS_TVOS(8_0, 10_0); // key (NSNumber): Request ID of the request for this result
+extern NSString *const PHImageCancelledKey PHOTOS_AVAILABLE_IOS_TVOS(8_0, 10_0); // key (NSNumber): result is not available because the request was cancelled
+extern NSString *const PHImageErrorKey PHOTOS_AVAILABLE_IOS_TVOS(8_0, 10_0); // key (NSError): NSFileManager or iCloud Photo Library errors
 
 
 // Note that all sizes are in pixels
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHImageManager : NSObject
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHImageManager : NSObject
 
 + (PHImageManager *)defaultManager;
 
@@ -136,7 +138,7 @@
 #pragma mark - Live Photo
 
 /// Requests a live photo representation of the asset. With PHImageRequestOptionsDeliveryModeOpportunistic (or if no options are specified), the resultHandler block may be called more than once (the first call may occur before the method returns). The PHImageResultIsDegradedKey key in the result handler's info parameter indicates when a temporary low-quality live photo is provided.
-- (PHImageRequestID)requestLivePhotoForAsset:(PHAsset *)asset targetSize:(CGSize)targetSize contentMode:(PHImageContentMode)contentMode options:(nullable PHLivePhotoRequestOptions *)options resultHandler:(void (^)(PHLivePhoto *__nullable livePhoto, NSDictionary *__nullable info))resultHandler NS_AVAILABLE_IOS(9_1);
+- (PHImageRequestID)requestLivePhotoForAsset:(PHAsset *)asset targetSize:(CGSize)targetSize contentMode:(PHImageContentMode)contentMode options:(nullable PHLivePhotoRequestOptions *)options resultHandler:(void (^)(PHLivePhoto *__nullable livePhoto, NSDictionary *__nullable info))resultHandler PHOTOS_AVAILABLE_IOS_TVOS(9_1, 10_0);
 
 
 #pragma mark - Video
@@ -155,7 +157,7 @@
 
 #pragma mark - PHCachingImageManager - Preheating
 
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHCachingImageManager : PHImageManager
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHCachingImageManager : PHImageManager
 
 // During fast scrolling clients should set this to improve responsiveness
 @property (nonatomic, assign) BOOL allowsCachingHighQualityImages; // Defaults to YES
@@ -169,4 +171,4 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHLivePhoto.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHLivePhoto.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHLivePhoto.h	2015-10-03 02:14:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHLivePhoto.h	2016-06-01 05:08:28.000000000 +0200
@@ -8,20 +8,22 @@
 #import <Foundation/Foundation.h>
 #import <UIKit/UIKit.h>
 
+#import <Photos/PhotosDefines.h>
+
 #import "PhotosTypes.h"
 
 NS_ASSUME_NONNULL_BEGIN
 
-typedef int32_t PHLivePhotoRequestID NS_AVAILABLE_IOS(9_1);
+typedef int32_t PHLivePhotoRequestID PHOTOS_AVAILABLE_IOS_TVOS(9_1, 10_0);
 static const PHLivePhotoRequestID PHLivePhotoRequestIDInvalid = 0;
 
 /// These keys may be found in the info dictionary delivered to a live photo request result handler block.
-extern NSString * const PHLivePhotoInfoErrorKey NS_AVAILABLE_IOS(9_1); // key : NSError decribing an error that has occurred while creating the live photo
-extern NSString * const PHLivePhotoInfoIsDegradedKey NS_AVAILABLE_IOS(9_1); // key : NSNumber containing a BOOL, YES whenever the deivered live photo object does not contain all content required for full playback.
-extern NSString * const PHLivePhotoInfoCancelledKey NS_AVAILABLE_IOS(9_1); // key : NSNumber containing a BOOL, YES when the result handler is being called after the request has been cancelled.
+extern NSString * const PHLivePhotoInfoErrorKey PHOTOS_AVAILABLE_IOS_TVOS(9_1, 10_0); // key : NSError decribing an error that has occurred while creating the live photo
+extern NSString * const PHLivePhotoInfoIsDegradedKey PHOTOS_AVAILABLE_IOS_TVOS(9_1, 10_0); // key : NSNumber containing a BOOL, YES whenever the deivered live photo object does not contain all content required for full playback.
+extern NSString * const PHLivePhotoInfoCancelledKey PHOTOS_AVAILABLE_IOS_TVOS(9_1, 10_0); // key : NSNumber containing a BOOL, YES when the result handler is being called after the request has been cancelled.
 
 
-NS_CLASS_AVAILABLE_IOS(9_1)
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(9_1, 10_0)
 @interface PHLivePhoto : NSObject <NSCopying, NSSecureCoding>
 
 /// The dimensions of the live photo measured in pixels.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHLivePhotoEditingContext.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHLivePhotoEditingContext.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHLivePhotoEditingContext.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHLivePhotoEditingContext.h	2016-06-01 05:07:14.000000000 +0200
@@ -0,0 +1,116 @@
+//
+//  PHLivePhotoEditingContext.h
+//  Photos
+//
+//  Copyright (c) 2016 Apple Inc. All rights reserved.
+//
+
+#import <Photos/PHLivePhoto.h>
+#import <CoreImage/CIImage.h>
+#import <CoreMedia/CMTime.h>
+#import <ImageIO/CGImageProperties.h>
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
+NS_AVAILABLE(12_0, 10_0)
+@interface PHLivePhotoEditingContext : NSObject
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
+// ------------------------------------------------------------------------
+// Editable properties
+// ------------------------------------------------------------------------
+
+/// A block that can be set to process each frame of the live photo
+/// Note that the context uses a copy of the processor block during processing
+@property (nullable, copy) PHLivePhotoFrameProcessingBlock frameProcessor;
+
+/// Specify the audio volume of the edited live photo
+/// Must be between 0.0 and 1.0
+/// Default to 1.0
+@property float audioVolume;
+
+// The orientation of the live photo
+@property (readonly) CGImagePropertyOrientation orientation;
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
+/// This is implicitly called whenever prepare or save is called
+/// A canceled operation will call its completion handler with an appropriate error code
+- (void)cancel;
+
+@end
+
+/// The type of frame in the Live Photo
+typedef NS_ENUM(NSInteger, PHLivePhotoFrameType) {
+    /// Indicates the still image
+    PHLivePhotoFrameTypePhoto,
+    
+    /// Indicates a video frame
+    PHLivePhotoFrameTypeVideo,
+} NS_ENUM_AVAILABLE(10_12, 10_0);
+
+/// Protocol that describes a single frame of a live photo
+@protocol PHLivePhotoFrame
+
+/// Input image for the frame
+@property (readonly) CIImage *image;
+
+/// The time of the frame relative to the beginning of the live photo
+@property (readonly) CMTime time;
+
+/// The type of frame
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
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHObject.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHObject.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHObject.h	2015-10-03 02:14:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHObject.h	2016-06-01 05:08:28.000000000 +0200
@@ -6,13 +6,14 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <Photos/PhotosDefines.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
 @class PHPhotoLibrary;
 
 
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHObject : NSObject <NSCopying>
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHObject : NSObject <NSCopying>
 
 // Returns an identifier which persistently identifies the object on a given device
 @property (nonatomic, copy, readonly) NSString *localIdentifier;
@@ -20,7 +21,7 @@
 @end
 
 // PHObjectPlaceholder represents a model object future , vended by change requests when creating a model object.  PHObjectPlaceholder is a read-only object and may be used as a proxy for the real object that will be created both inside and outside of the change block.  Will compare isEqual: to the fetched model object after the change block is performed.
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHObjectPlaceholder : PHObject
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHObjectPlaceholder : PHObject
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHPhotoLibrary.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHPhotoLibrary.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHPhotoLibrary.h	2015-10-03 02:14:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHPhotoLibrary.h	2016-06-01 05:08:28.000000000 +0200
@@ -6,6 +6,7 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <Photos/PhotosDefines.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -18,10 +19,10 @@
                                             //   such as parental controls being in place.
     PHAuthorizationStatusDenied,            // User has explicitly denied this application access to photos data.
     PHAuthorizationStatusAuthorized         // User has authorized this application to access photos data.
-} NS_AVAILABLE_IOS(8_0);
+} PHOTOS_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
 
-NS_CLASS_AVAILABLE_IOS(8_0) @protocol PHPhotoLibraryChangeObserver <NSObject>
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @protocol PHPhotoLibraryChangeObserver <NSObject>
 // This callback is invoked on an arbitrary serial queue. If you need this to be handled on a specific queue, you should redispatch appropriately
 - (void)photoLibraryDidChange:(PHChange *)changeInstance;
 
@@ -32,7 +33,7 @@
  @abstract     A PHPhotoLibrary provides access to the metadata and image data for the photos, videos and related content in the user's photo library, including content from the Camera Roll, iCloud Shared, Photo Stream, imported, and synced from iTunes.
  @discussion   ...
  */
-NS_CLASS_AVAILABLE_IOS(8_0) @interface PHPhotoLibrary : NSObject
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHPhotoLibrary : NSObject
 
 + (PHPhotoLibrary *)sharedPhotoLibrary;
 
@@ -54,4 +55,4 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/Photos.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/Photos.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/Photos.h	2015-10-03 02:14:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/Photos.h	2016-06-01 05:08:28.000000000 +0200
@@ -25,6 +25,7 @@
 #import <Photos/PHAssetCreationRequest.h>
 #import <Photos/PHAssetCollectionChangeRequest.h>
 #import <Photos/PHCollectionListChangeRequest.h>
+#import <Photos/PHLivePhotoEditingContext.h>
 
 #import <Photos/PHImageManager.h>
 
@@ -35,4 +36,6 @@
 #import <Photos/PHContentEditingInput.h>
 #import <Photos/PHContentEditingOutput.h>
 
+#import <Photos/PhotosDefines.h>
+
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PhotosDefines.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PhotosDefines.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PhotosDefines.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PhotosDefines.h	2016-06-01 05:08:28.000000000 +0200
@@ -0,0 +1,37 @@
+//
+//  PhotosDefines.h
+//  PhotoKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Availability.h>
+
+#ifdef __cplusplus
+#define PHOTOS_EXTERN            extern "C" __attribute__((visibility ("default")))
+#else
+#define PHOTOS_EXTERN	        extern __attribute__((visibility ("default")))
+#endif
+
+#define PHOTOS_STATIC_INLINE	static inline
+
+#define PHOTOS_AVAILABLE_IOS_ONLY(vers)                 __IOS_AVAILABLE(vers) __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE
+#define PHOTOS_AVAILABLE_WATCHOS_ONLY(vers)             __IOS_UNAVAILABLE __WATCHOS_AVAILABLE(vers) __TVOS_UNAVAILABLE
+#define PHOTOS_AVAILABLE_TVOS_ONLY(vers)                __IOS_UNAVAILABLE __WATCHOS_UNAVAILABLE __TVOS_AVAILABLE(vers)
+#define PHOTOS_AVAILABLE_IOS_TVOS(_ios, _tvos)          __IOS_AVAILABLE(_ios) __TVOS_AVAILABLE(_tvos)
+#define PHOTOS_AVAILABLE_IOS_TVOS_OSX(_ios, _tvos, _osx)            __IOS_AVAILABLE(_ios) __TVOS_AVAILABLE(_tvos) __OSX_AVAILABLE(_osx)
+#define PHOTOS_AVAILABLE_IOS_WATCHOS_TVOS(_ios, _watchos, _tvos)    __IOS_AVAILABLE(_ios) __WATCHOS_AVAILABLE(_watchos) __TVOS_AVAILABLE(_tvos)
+
+#define PHOTOS_CLASS_AVAILABLE_IOS_ONLY(vers)           PHOTOS_EXTERN __IOS_AVAILABLE(vers) __WATCHOS_UNAVAILABLE __TVOS_UNAVAILABLE
+#define PHOTOS_CLASS_AVAILABLE_WATCHOS_ONLY(vers)       PHOTOS_EXTERN __IOS_UNAVAILABLE __WATCHOS_AVAILABLE(vers) __TVOS_UNAVAILABLE
+#define PHOTOS_CLASS_AVAILABLE_TVOS_ONLY(vers)          PHOTOS_EXTERN __IOS_UNAVAILABLE __WATCHOS_UNAVAILABLE __TVOS_AVAILABLE(vers)
+#define PHOTOS_CLASS_AVAILABLE_IOS_TVOS(_ios, _tvos)    PHOTOS_EXTERN __IOS_AVAILABLE(_ios) __TVOS_AVAILABLE(_tvos)
+#define PHOTOS_CLASS_AVAILABLE_IOS_TVOS_OSX(_ios, _tvos, _osx)          PHOTOS_EXTERN __IOS_AVAILABLE(_ios) __TVOS_AVAILABLE(_tvos) __OSX_AVAILABLE(_osx)
+#define PHOTOS_CLASS_AVAILABLE_IOS_WATCHOS_TVOS(_ios, _watchos, _tvos)  PHOTOS_EXTERN __IOS_AVAILABLE(_ios) __WATCHOS_AVAILABLE(_watchos) __TVOS_AVAILABLE(_tvos)
+
+#define PHOTOS_ENUM_AVAILABLE_IOS_ONLY(vers)            PHOTOS_AVAILABLE_IOS_ONLY(vers)
+#define PHOTOS_ENUM_AVAILABLE_WATCHOS_ONLY(vers)        PHOTOS_AVAILABLE_WATCHOS_ONLY(vers)
+#define PHOTOS_ENUM_AVAILABLE_TVOS_ONLY(vers)           PHOTOS_AVAILABLE_TVOS_ONLY(vers)
+#define PHOTOS_ENUM_AVAILABLE_IOS_TVOS(_ios, _tvos)     PHOTOS_AVAILABLE_IOS_TVOS(_ios, _tvos)
+#define PHOTOS_ENUM_AVAILABLE_IOS_TVOS_OSX(_ios, _tvos, _osx)          PHOTOS_AVAILABLE_IOS_TVOS_OSX(_ios, _tvos, _osx)
+#define PHOTOS_ENUM_AVAILABLE_IOS_WATCHOS_TVOS(_ios, _watchos, _tvos)  PHOTOS_AVAILABLE_IOS_WATCHOS_TVOS(_ios, _watchos, _tvos)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PhotosTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PhotosTypes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PhotosTypes.h	2015-10-03 02:14:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PhotosTypes.h	2016-06-01 05:08:28.000000000 +0200
@@ -8,19 +8,21 @@
 #ifndef Photos_PhotosTypes_h
 #define Photos_PhotosTypes_h
 
+#import <Photos/PhotosDefines.h>
+
 #pragma mark - PHCollectionListTypes
 
 typedef NS_ENUM(NSInteger, PHImageContentMode) {
     PHImageContentModeAspectFit = 0,
     PHImageContentModeAspectFill = 1,
     PHImageContentModeDefault = PHImageContentModeAspectFit
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} PHOTOS_ENUM_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
 typedef NS_ENUM(NSInteger, PHCollectionListType) {
     PHCollectionListTypeMomentList    = 1,
     PHCollectionListTypeFolder        = 2,
     PHCollectionListTypeSmartFolder   = 3,
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} PHOTOS_ENUM_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
 typedef NS_ENUM(NSInteger, PHCollectionListSubtype) {
     
@@ -37,7 +39,7 @@
     
     // Used for fetching if you don't care about the exact subtype
     PHCollectionListSubtypeAny = NSIntegerMax
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} PHOTOS_ENUM_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
 #pragma mark - PHCollection types
 
@@ -49,7 +51,7 @@
     PHCollectionEditOperationRearrangeContent = 5, // Change the order of things
     PHCollectionEditOperationDelete           = 6, // Deleting of the container, not the content
     PHCollectionEditOperationRename           = 7, // Renaming of the container, not the content
-} NS_AVAILABLE_IOS(8_0);
+} PHOTOS_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
 #pragma mark - PHAssetCollection types
 
@@ -57,7 +59,7 @@
     PHAssetCollectionTypeAlbum      = 1,
     PHAssetCollectionTypeSmartAlbum = 2,
     PHAssetCollectionTypeMoment     = 3,
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} PHOTOS_ENUM_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
 typedef NS_ENUM(NSInteger, PHAssetCollectionSubtype) {
     
@@ -83,12 +85,12 @@
     PHAssetCollectionSubtypeSmartAlbumBursts     = 207,
     PHAssetCollectionSubtypeSmartAlbumSlomoVideos = 208,
     PHAssetCollectionSubtypeSmartAlbumUserLibrary = 209,
-    PHAssetCollectionSubtypeSmartAlbumSelfPortraits NS_AVAILABLE_IOS(9_0) = 210,
-    PHAssetCollectionSubtypeSmartAlbumScreenshots NS_AVAILABLE_IOS(9_0) = 211,
+    PHAssetCollectionSubtypeSmartAlbumSelfPortraits PHOTOS_AVAILABLE_IOS_TVOS(9_0, 10_0) = 210,
+    PHAssetCollectionSubtypeSmartAlbumScreenshots PHOTOS_AVAILABLE_IOS_TVOS(9_0, 10_0) = 211,
     
     // Used for fetching, if you don't care about the exact subtype
     PHAssetCollectionSubtypeAny = NSIntegerMax
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} PHOTOS_ENUM_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
 #pragma mark - PHAsset types
 
@@ -96,14 +98,14 @@
     PHAssetEditOperationDelete     = 1,
     PHAssetEditOperationContent    = 2,
     PHAssetEditOperationProperties = 3,
-} NS_AVAILABLE_IOS(8_0);
+} PHOTOS_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
 typedef NS_ENUM(NSInteger, PHAssetMediaType) {
     PHAssetMediaTypeUnknown = 0,
     PHAssetMediaTypeImage   = 1,
     PHAssetMediaTypeVideo   = 2,
     PHAssetMediaTypeAudio   = 3,
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} PHOTOS_ENUM_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
 typedef NS_OPTIONS(NSUInteger, PHAssetMediaSubtype) {
     PHAssetMediaSubtypeNone               = 0,
@@ -111,28 +113,27 @@
     // Photo subtypes
     PHAssetMediaSubtypePhotoPanorama      = (1UL << 0),
     PHAssetMediaSubtypePhotoHDR           = (1UL << 1),
-    PHAssetMediaSubtypePhotoScreenshot NS_AVAILABLE_IOS(9_0) = (1UL << 2),
-    PHAssetMediaSubtypePhotoLive NS_AVAILABLE_IOS(9_1) = (1UL << 3),
+    PHAssetMediaSubtypePhotoScreenshot PHOTOS_AVAILABLE_IOS_TVOS(9_0, 10_0) = (1UL << 2),
+    PHAssetMediaSubtypePhotoLive PHOTOS_AVAILABLE_IOS_TVOS(9_1, 10_0) = (1UL << 3),
 
-    
     // Video subtypes
     PHAssetMediaSubtypeVideoStreamed      = (1UL << 16),
     PHAssetMediaSubtypeVideoHighFrameRate = (1UL << 17),
     PHAssetMediaSubtypeVideoTimelapse     = (1UL << 18),
-} NS_AVAILABLE_IOS(8_0);
+} PHOTOS_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
 typedef NS_OPTIONS(NSUInteger, PHAssetBurstSelectionType) {
     PHAssetBurstSelectionTypeNone     = 0,
     PHAssetBurstSelectionTypeAutoPick = (1UL << 0),
     PHAssetBurstSelectionTypeUserPick = (1UL << 1),
-} NS_AVAILABLE_IOS(8_0);
+} PHOTOS_AVAILABLE_IOS_TVOS(8_0, 10_0);
 
 typedef NS_OPTIONS(NSUInteger, PHAssetSourceType) {
     PHAssetSourceTypeNone            = 0,
     PHAssetSourceTypeUserLibrary     = (1UL << 0),
     PHAssetSourceTypeCloudShared     = (1UL << 1),
     PHAssetSourceTypeiTunesSynced    = (1UL << 2),
-} NS_AVAILABLE_IOS(9_0);
+} PHOTOS_AVAILABLE_IOS_TVOS(9_0, 10_0);
 
 typedef NS_ENUM(NSInteger, PHAssetResourceType) {
     PHAssetResourceTypePhoto                             = 1,
@@ -143,7 +144,9 @@
     PHAssetResourceTypeFullSizeVideo                     = 6,
     PHAssetResourceTypeAdjustmentData                    = 7,
     PHAssetResourceTypeAdjustmentBasePhoto               = 8,
-    PHAssetResourceTypePairedVideo NS_AVAILABLE_IOS(9_1) = 9,
-} NS_ENUM_AVAILABLE_IOS(9_0);
+    PHAssetResourceTypePairedVideo PHOTOS_AVAILABLE_IOS_TVOS(9_1, 10_0) = 9,
+    PHAssetResourceTypeFullSizePairedVideo PHOTOS_AVAILABLE_IOS_TVOS(10_0, 10_0) = 10,
+    PHAssetResourceTypeAdjustmentBasePairedVideo PHOTOS_AVAILABLE_IOS_TVOS(10_0, 10_0) = 11,
+} PHOTOS_ENUM_AVAILABLE_IOS_TVOS(9_0, 10_0);
 
 #endif

```