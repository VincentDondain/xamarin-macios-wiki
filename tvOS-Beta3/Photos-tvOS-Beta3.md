#Photos.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetCollectionChangeRequest.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetCollectionChangeRequest.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetCollectionChangeRequest.h	2016-06-27 06:45:24.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHAssetCollectionChangeRequest.h	2016-07-11 07:40:27.000000000 +0200
@@ -6,8 +6,9 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <Photos/PHFetchResult.h>
 
-@class PHFetchResult;
+@class PHAsset;
 @class PHAssetCollection;
 @class PHObjectPlaceholder;
 
@@ -35,7 +36,7 @@
 + (nullable instancetype)changeRequestForAssetCollection:(PHAssetCollection *)assetCollection;
 
 // to add, remove or rearrange assets in a collection, passing in the fetched assets in that collection will ensure that the asset positions are tracked correctly in the case that the collection has been externally edited after the fetch, but before this change is applied
-+ (nullable instancetype)changeRequestForAssetCollection:(PHAssetCollection *)assetCollection assets:(PHFetchResult *)assets;
++ (nullable instancetype)changeRequestForAssetCollection:(PHAssetCollection *)assetCollection assets:(PHFetchResult<PHAsset *> *)assets;
 
 @property (nonatomic, strong, readwrite) NSString *title;
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHChange.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHChange.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHChange.h	2016-06-27 06:45:24.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHChange.h	2016-07-11 07:40:27.000000000 +0200
@@ -7,11 +7,11 @@
 
 #import <Foundation/Foundation.h>
 #import <Photos/PhotosDefines.h>
+#import <Photos/PHFetchResult.h>
 
 @class PHObject;
 @class PHObjectChangeDetails;
 @class PHFetchResultChangeDetails;
-@class PHFetchResult;
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -24,13 +24,13 @@
 
 
 
-PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHObjectChangeDetails : NSObject
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHObjectChangeDetails<ObjectType: PHObject *> : NSObject
 
 // the object in the state before this change (returns the object that was passed in to changeDetailsForObject:)
-@property (atomic, strong, readonly) __kindof PHObject *objectBeforeChanges;
+@property (atomic, strong, readonly) __kindof ObjectType objectBeforeChanges;
 
 // the object in the state after this change
-@property (atomic, strong, readonly, nullable) __kindof PHObject *objectAfterChanges;
+@property (atomic, strong, readonly, nullable) __kindof ObjectType objectAfterChanges;
 
 // YES if the image or video content for this object has been changed
 @property (atomic, readonly) BOOL assetContentChanged;
@@ -42,13 +42,13 @@
 
 
 
-PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHFetchResultChangeDetails : NSObject
+PHOTOS_CLASS_AVAILABLE_IOS_TVOS(8_0, 10_0) @interface PHFetchResultChangeDetails<ObjectType: PHObject *> : NSObject
 
 // fetch result with the state of the fetched objects before this change (returns the fetch result passed in to changeDetailsForFetchResult:)
-@property (atomic, strong, readonly) PHFetchResult *fetchResultBeforeChanges;
+@property (atomic, strong, readonly) PHFetchResult<ObjectType> *fetchResultBeforeChanges;
 
 // fetch result with the state of the fetched objects after this change
-@property (atomic, strong, readonly) PHFetchResult *fetchResultAfterChanges;
+@property (atomic, strong, readonly) PHFetchResult<ObjectType> *fetchResultAfterChanges;
 
 // YES if the changes to this fetch result are described by the removed/inserted/changed details.
 // NO indicates that the scope of changes were too large and UI clients should do a full reload, incremental changes could not be provided
@@ -57,17 +57,17 @@
 // The indexes of the removed items, relative to the 'before' state of the fetch result
 // returns nil if hasIncrementalChanges is NO
 @property (atomic, strong, readonly, nullable) NSIndexSet *removedIndexes;
-@property (atomic, strong, readonly) NSArray<__kindof PHObject *> *removedObjects;
+@property (atomic, strong, readonly) NSArray<ObjectType> *removedObjects;
 
 // The indexes of the inserted items, relative to the 'before' state of the fetch result after applying the removedIndexes
 // returns nil if hasIncrementalChanges is NO
 @property (atomic, strong, readonly, nullable) NSIndexSet *insertedIndexes;
-@property (atomic, strong, readonly) NSArray<__kindof PHObject *> *insertedObjects;
+@property (atomic, strong, readonly) NSArray<ObjectType> *insertedObjects;
 
 // The indexes of the updated items, relative to the 'after' state of the fetch result
 // returns nil if hasIncrementalChanges is NO
 @property (atomic, strong, readonly, nullable) NSIndexSet *changedIndexes;
-@property (atomic, strong, readonly) NSArray<__kindof PHObject *> *changedObjects;
+@property (atomic, strong, readonly) NSArray<ObjectType> *changedObjects;
 
 // Enumerates the indexes of the moved items, relative to the 'before' state of the fetch result after applying the removedIndexes and insertedIndexes
 - (void)enumerateMovesWithBlock:(void(^)(NSUInteger fromIndex, NSUInteger toIndex))handler;
@@ -78,7 +78,7 @@
 
 
 // Provides a "diff" between 2 PHFetchResult objects.
-+ (instancetype)changeDetailsFromFetchResult:(PHFetchResult *)fromResult toFetchResult:(PHFetchResult *)toResult changedObjects:(NSArray<PHObject *> *)changedObjects;
++ (instancetype)changeDetailsFromFetchResult:(PHFetchResult<ObjectType> *)fromResult toFetchResult:(PHFetchResult<ObjectType> *)toResult changedObjects:(NSArray<ObjectType> *)changedObjects;
 
 @end
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHCollectionListChangeRequest.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHCollectionListChangeRequest.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHCollectionListChangeRequest.h	2016-06-27 06:45:24.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/Photos.framework/Headers/PHCollectionListChangeRequest.h	2016-07-11 07:40:27.000000000 +0200
@@ -7,8 +7,8 @@
 
 #import <Foundation/Foundation.h>
 #import <Photos/PhotosDefines.h>
+#import <Photos/PHFetchResult.h>
 
-@class PHFetchResult;
 @class PHCollection;
 @class PHCollectionList;
 @class PHObjectPlaceholder;
@@ -37,7 +37,7 @@
 + (nullable instancetype)changeRequestForCollectionList:(PHCollectionList *)collectionList;
 
 // to add, remove or rearrange child collections in a collection list, passing in the fetched collections in that collection list will ensure that the child collection positions are tracked correctly in the case that the collection list has been externally edited after the fetch, but before this change is applied
-+ (nullable instancetype)changeRequestForCollectionList:(PHCollectionList *)collectionList childCollections:(PHFetchResult *)childCollections;
++ (nullable instancetype)changeRequestForCollectionList:(PHCollectionList *)collectionList childCollections:(PHFetchResult<__kindof PHCollection *> *)childCollections;
 
 @property (nonatomic, strong, readwrite) NSString *title;
 

```