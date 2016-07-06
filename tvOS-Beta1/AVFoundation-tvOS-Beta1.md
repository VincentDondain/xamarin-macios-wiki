#AVFoundation.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h	2015-09-30 23:17:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h	2016-05-25 07:22:12.000000000 +0200
@@ -431,6 +431,14 @@
  */
 AVF_EXPORT NSString *const AVURLAssetHTTPCookiesKey NS_AVAILABLE_IOS(8_0);
 
+/*
+ @constant		AVURLAssetAllowsCellularAccessKey
+ @abstract		Indicates whether network requests on behalf of this asset are allowed to use the cellular interface.
+ @discussion
+ 	Default is YES.
+*/
+AVF_EXPORT NSString *const AVURLAssetAllowsCellularAccessKey NS_AVAILABLE_IOS(10_0);
+
 /*!
   @class		AVURLAsset
 
@@ -519,6 +527,17 @@
 
 @end
 
+@class AVAssetCache;
+
+@interface AVURLAsset (AVURLAssetCache)
+
+/*!
+ @property	assetCache
+ @abstract	Provides access to an instance of AVAssetCache to use for inspection of locally cached media data. Will be nil if an asset has not been configured to store or access media data from disk.
+*/
+@property (nonatomic, readonly, nullable) AVAssetCache *assetCache NS_AVAILABLE(10_12, 10_0);
+
+@end
 
 @interface AVURLAsset (AVAssetCompositionUtility )
 
@@ -589,8 +608,8 @@
 
 /*!
   @property		associatedWithFragmentMinder
-  @abstract		Indicates whether an AVAsset that supports fragment minding is currently associated with an AVAssetFragmentMinder.
-  @discussion	AVAssets that support fragment minding post change notifications only while associated with an AVAssetFragmentMinder.
+  @abstract		Indicates whether an AVAsset that supports fragment minding is currently associated with a fragment minder, e.g. an instance of AVFragmentedAssetMinder.
+  @discussion	AVAssets that support fragment minding post change notifications only while associated with a fragment minder.
 */
 @property (nonatomic, readonly, getter=isAssociatedWithFragmentMinder) BOOL associatedWithFragmentMinder NS_AVAILABLE_MAC(10_11);
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetCache.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetCache.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetCache.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetCache.h	2016-05-25 07:19:40.000000000 +0200
@@ -0,0 +1,51 @@
+/*
+	File:  AVAssetCache.h
+ 
+	Framework:  AVFoundation
+ 
+	Copyright 2016 Apple Inc. All rights reserved.
+ 
+*/
+
+#import <AVFoundation/AVBase.h>
+#import <Foundation/Foundation.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class AVMediaSelectionGroup;
+@class AVMediaSelectionOption;
+
+/*!
+	@class		AVAssetCache
+
+	@abstract
+		AVAssetCache is a class vended by an AVAsset used for the inspection of locally available media data.
+
+	@discussion
+		AVAssetCaches are vended by AVURLAsset's assetCache property.
+
+*/
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface AVAssetCache : NSObject
+
+/*
+	@property	playableOffline
+	@abstract
+		Returns YES if a complete rendition of an AVAsset is available to be played without a network connection.
+	@discussion
+		An answer of YES does not indicate that any given media selection is available for offline playback. To determine if a specific media selection is available offline, see mediaSelectionOptionsInMediaSelectionGroup:.
+*/
+@property (nonatomic, readonly, getter=isPlayableOffline) BOOL playableOffline;
+
+/*
+	@method		mediaSelectionOptionsInMediaSelectionGroup:
+	@abstract
+		Returns an array of AVMediaSelectionOptions in an AVMediaSelectionGroup that are available for offline operations, e.g. playback.
+*/
+- (NSArray<AVMediaSelectionOption *> *)mediaSelectionOptionsInMediaSelectionGroup:(AVMediaSelectionGroup *)mediaSelectionGroup;
+
+AV_INIT_UNAVAILABLE
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetDownloadTask.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetDownloadTask.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetDownloadTask.h	2015-09-30 23:17:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetDownloadTask.h	2016-05-25 07:22:12.000000000 +0200
@@ -15,7 +15,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-// Keys for options dictionary for use with -[AVAssetDownloadURLSession assetDownloadTaskWithURLAsset:destinationURL:options:]
+// Keys for options dictionary for use with -[AVAssetDownloadURLSession assetDownloadTaskWithURLAsset:assetTitle:assetArtworkData:options:]
 
 /*!
  @constant		AVAssetDownloadTaskMinimumRequiredMediaBitrateKey
@@ -39,7 +39,7 @@
  @discussion	Should be created with -[AVAssetDownloadURLSession assetDownloadTaskWithURLAsset:destinationURL:options:]. To utilize local data for playback for downloads that are in-progress, re-use the URLAsset supplied in initialization. An AVAssetDownloadTask may be instantiated with a destinationURL pointing to an existing asset on disk, for the purpose of completing or augmenting a downloaded asset.
 */
 
-NS_CLASS_AVAILABLE_IOS(9_0)
+NS_CLASS_AVAILABLE_IOS(9_0) __TVOS_PROHIBITED
 @interface AVAssetDownloadTask : NSURLSessionTask
 
 /*!
@@ -53,7 +53,7 @@
  @abstract		The file URL supplied to the download task upon initialization.
  @discussion	This URL may have been appended with the appropriate extension for the asset.
 */
-@property (nonatomic, readonly) NSURL *destinationURL;
+@property (nonatomic, readonly) NSURL *destinationURL NS_DEPRECATED_IOS(9_0, 10_0);
 
 /*!
  @property		options
@@ -69,6 +69,7 @@
 @property (nonatomic, readonly) NSArray<NSValue *> *loadedTimeRanges;
 
 // NSURLRequest and NSURLResponse objects are not available for AVAssetDownloadTask
+AV_INIT_UNAVAILABLE
 @property (readonly, copy) NSURLRequest *originalRequest NS_UNAVAILABLE;
 @property (readonly, copy) NSURLRequest *currentRequest NS_UNAVAILABLE;
 @property (readonly, copy) NSURLResponse *response NS_UNAVAILABLE;
@@ -81,8 +82,21 @@
  @abstract		Delegate method to implement when adopting AVAssetDownloadTask.
 */
 
+__TVOS_PROHIBITED
 @protocol AVAssetDownloadDelegate <NSURLSessionTaskDelegate>
 @optional
+/*!
+ @method		URLSession:assetDownloadTask:didFinishDownloadingToURL:
+ @abstract		Sent when a download task that has completed a download.
+ @discussion	Unlike NSURLSessionDownloadDelegate, the delegate should NOT move the file from this directory after it has been called. Downloaded assets must remain at the system provided URL. URLSession:task:didCompleteWithError: will still be called.
+ @param			session
+				The session the asset download task is on.
+ @param			assetDownloadTask
+				The AVAssetDownloadTask whose downloaded completed.
+ @param			location
+				The location the asset has been downloaded to.
+*/
+- (void)URLSession:(NSURLSession *)session assetDownloadTask:(AVAssetDownloadTask *)assetDownloadTask didFinishDownloadingToURL:(NSURL *)location NS_AVAILABLE_IOS(10_0);
 
 /*!
  @method		URLSession:assetDownloadTask:didLoadTimeRange:totalTimeRangesLoaded:timeRangeExpectedToLoad:
@@ -119,7 +133,7 @@
  @class			AVAssetDownloadURLSession
  @abstract		A subclass of NSURLSession to support AVAssetDownloadTask.
 */
-NS_CLASS_AVAILABLE_IOS(9_0)
+NS_CLASS_AVAILABLE_IOS(9_0) __TVOS_PROHIBITED
 @interface AVAssetDownloadURLSession : NSURLSession
 
 /*!
@@ -145,9 +159,25 @@
  @param			options
 				See AVAssetDownloadTask*Key above. Configures non-default behavior for the download task. Using this parameter is required for downloading non-default media selections for HLS assets.
 */
-- (nullable AVAssetDownloadTask *)assetDownloadTaskWithURLAsset:(AVURLAsset *)URLAsset destinationURL:(NSURL *)destinationURL options:(nullable NSDictionary<NSString *, id> *)options;
+- (nullable AVAssetDownloadTask *)assetDownloadTaskWithURLAsset:(AVURLAsset *)URLAsset destinationURL:(NSURL *)destinationURL options:(nullable NSDictionary<NSString *, id> *)options NS_DEPRECATED_IOS(9_0, 10_0);
+
+/*!
+ @method		assetDownloadTaskWithURLAsset:assetTitle:assetArtworkData:options:
+ @abstract		Creates and initializes an AVAssetDownloadTask to be used with this AVAssetDownloadURLSession.
+ @discussion	This method may return nil if the URLSession has been invalidated.
+ @param			URLAsset
+				The AVURLAsset to download locally.
+ @param			assetTitle
+				A human readable title for this asset, expected to be as suitable as possible for the user's preferred languages. Will show up in the usage pane of the settings app.
+ @param			assetArtworkData
+				Artwork data for this asset. Optional. Will show up in the usage pane of the settings app.
+ @param			options
+				See AVAssetDownloadTask*Key above. Configures non-default behavior for the download task. Using this parameter is required for downloading non-default media selections for HLS assets.
+*/
+- (nullable AVAssetDownloadTask *)assetDownloadTaskWithURLAsset:(AVURLAsset *)URLAsset assetTitle:(NSString *)title assetArtworkData:(nullable NSData *)artworkData options:(nullable NSDictionary<NSString *, id> *)options NS_AVAILABLE_IOS(10_0);
 
 // only AVAssetDownloadTasks can be created with AVAssetDownloadURLSession
+AV_INIT_UNAVAILABLE
 + (NSURLSession *)sharedSession NS_UNAVAILABLE;
 + (NSURLSession *)sessionWithConfiguration:(NSURLSessionConfiguration *)configuration NS_UNAVAILABLE;
 + (NSURLSession *)sessionWithConfiguration:(NSURLSessionConfiguration *)configuration delegate:(nullable id <NSURLSessionDelegate>)delegate delegateQueue:(nullable NSOperationQueue *)queue NS_UNAVAILABLE;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetImageGenerator.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetImageGenerator.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetImageGenerator.h	2015-09-30 23:17:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetImageGenerator.h	2016-05-25 07:19:40.000000000 +0200
@@ -3,7 +3,7 @@
 
 	Framework:  AVFoundation
  
-	Copyright 2010-2015 Apple Inc. All rights reserved.
+	Copyright 2010-2016 Apple Inc. All rights reserved.
 
 */
 
@@ -34,18 +34,24 @@
 /*!
 	@constant		AVAssetImageGeneratorApertureModeCleanAperture
 	@abstract		Both pixel aspect ratio and clean aperture will be applied.
+	@discussion
+		An image's clean aperture is a region of video free from transition artifacts caused by the encoding of the signal.
 */
 AVF_EXPORT NSString *const AVAssetImageGeneratorApertureModeCleanAperture NS_AVAILABLE(10_7, 4_0);
 
 /*!
 	@constant		AVAssetImageGeneratorApertureModeProductionAperture
 	@abstract		Only pixel aspect ratio will be applied.
+	@discussion
+		The image is not cropped to the clean aperture region, but it is scaled according to the pixel aspect ratio. Use this option when you want to see all the pixels in your video, including the edges.
 */
 AVF_EXPORT NSString *const AVAssetImageGeneratorApertureModeProductionAperture NS_AVAILABLE(10_7, 4_0);
 
 /*!
 	@constant		AVAssetImageGeneratorApertureModeEncodedPixels
 	@abstract		Neither pixel aspect ratio nor clean aperture will be applied.
+	@discussion
+		The image is not cropped to the clean aperture region and is not scaled according to the pixel aspect ratio. The encoded dimensions of the image description are displayed.
 */
 AVF_EXPORT NSString *const AVAssetImageGeneratorApertureModeEncodedPixels NS_AVAILABLE(10_7, 4_0);
 
@@ -146,10 +152,10 @@
 	@result			A CGImageRef.
 	@discussion		Returns the CGImage synchronously. Ownership follows the Create Rule.
 */
-- (nullable CGImageRef)copyCGImageAtTime:(CMTime)requestedTime actualTime:(nullable CMTime *)actualTime error:(NSError * __nullable * __nullable)outError CF_RETURNS_RETAINED;
+- (nullable CGImageRef)copyCGImageAtTime:(CMTime)requestedTime actualTime:(nullable CMTime *)actualTime error:(NSError * _Nullable * _Nullable)outError CF_RETURNS_RETAINED;
 
 /* error object indicates the reason for failure if the result is AVAssetImageGeneratorFailed */
-typedef void (^AVAssetImageGeneratorCompletionHandler)(CMTime requestedTime, CGImageRef __nullable image, CMTime actualTime, AVAssetImageGeneratorResult result, NSError * __nullable error);
+typedef void (^AVAssetImageGeneratorCompletionHandler)(CMTime requestedTime, CGImageRef _Nullable image, CMTime actualTime, AVAssetImageGeneratorResult result, NSError * _Nullable error);
 
 /*!
 	@method			generateCGImagesAsynchronouslyForTimes:completionHandler:
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetReader.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetReader.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetReader.h	2015-09-30 23:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetReader.h	2016-05-25 07:19:40.000000000 +0200
@@ -3,7 +3,7 @@
 
 	Framework:  AVFoundation
  
-	Copyright 2010-2015 Apple Inc. All rights reserved.
+	Copyright 2010-2016 Apple Inc. All rights reserved.
 
 */
 
@@ -78,7 +78,7 @@
  @discussion
 	If the specified asset belongs to a mutable subclass of AVAsset, AVMutableComposition or AVMutableMovie, the results of any asset reading operation are undefined if you mutate the asset after invoking -startReading.
  */
-+ (nullable instancetype)assetReaderWithAsset:(AVAsset *)asset error:(NSError * __nullable * __nullable)outError;
++ (nullable instancetype)assetReaderWithAsset:(AVAsset *)asset error:(NSError * _Nullable * _Nullable)outError;
 
 /*!
  @method initWithAsset:error:
@@ -94,7 +94,7 @@
  @discussion
 	If the specified asset belongs to a mutable subclass of AVAsset, AVMutableComposition or AVMutableMovie, the results of any asset reading operation are undefined if you mutate the asset after invoking -startReading.
  */
-- (nullable instancetype)initWithAsset:(AVAsset *)asset error:(NSError * __nullable * __nullable)outError NS_DESIGNATED_INITIALIZER;
+- (nullable instancetype)initWithAsset:(AVAsset *)asset error:(NSError * _Nullable * _Nullable)outError NS_DESIGNATED_INITIALIZER;
 
 /*!
  @property asset
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetReaderOutput.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetReaderOutput.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetReaderOutput.h	2015-09-30 23:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetReaderOutput.h	2016-05-25 07:22:12.000000000 +0200
@@ -541,7 +541,6 @@
 
 @end
 
-
 @class AVAssetReaderSampleReferenceOutputInternal;
 
 /*!
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetResourceLoader.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetResourceLoader.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetResourceLoader.h	2015-09-30 23:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetResourceLoader.h	2016-05-25 07:19:41.000000000 +0200
@@ -3,7 +3,7 @@
 
 	Framework:  AVFoundation
  
-	Copyright 2010-2015 Apple Inc. All rights reserved.
+	Copyright 2010-2016 Apple Inc. All rights reserved.
 
 */
 
@@ -373,7 +373,7 @@
  				If obtaining the streaming content key request fails, will be set to an instance of NSError describing the failure.
  @result		The key request data that must be transmitted to the key vendor to obtain the content key.
 */
-- (nullable NSData *)streamingContentKeyRequestDataForApp:(NSData *)appIdentifier contentIdentifier:(NSData *)contentIdentifier options:(nullable NSDictionary<NSString *, id> *)options error:(NSError * __nullable * __nullable)outError;
+- (nullable NSData *)streamingContentKeyRequestDataForApp:(NSData *)appIdentifier contentIdentifier:(NSData *)contentIdentifier options:(nullable NSDictionary<NSString *, id> *)options error:(NSError * _Nullable * _Nullable)outError;
 
 /*! 
  @method 		persistentContentKeyFromKeyVendorResponse:options:error:
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetTrack.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetTrack.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetTrack.h	2015-09-30 23:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetTrack.h	2016-05-25 07:19:41.000000000 +0200
@@ -3,7 +3,7 @@
 
 	Framework:  AVFoundation
  
-	Copyright 2010-2015 Apple Inc. All rights reserved.
+	Copyright 2010-2016 Apple Inc. All rights reserved.
 
 */
 
@@ -101,11 +101,11 @@
 
 /* indicates the language associated with the track, as an ISO 639-2/T language code;
    may be nil if no language is indicated */
-@property (nonatomic, readonly) NSString *languageCode;
+@property (nonatomic, readonly, nullable) NSString *languageCode;
 
 /* indicates the language tag associated with the track, as an IETF BCP 47 (RFC 4646) language identifier;
    may be nil if no language tag is indicated */
-@property (nonatomic, readonly) NSString *extendedLanguageTag;
+@property (nonatomic, readonly, nullable) NSString *extendedLanguageTag;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetWriter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetWriter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetWriter.h	2015-09-30 23:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetWriter.h	2016-05-24 07:21:19.000000000 +0200
@@ -3,7 +3,7 @@
 
 	Framework:  AVFoundation
  
-	Copyright 2010-2015 Apple Inc. All rights reserved.
+	Copyright 2010-2016 Apple Inc. All rights reserved.
 
 */
 
@@ -84,7 +84,7 @@
 	
 	UTIs for container formats that can be written are declared in AVMediaFormat.h.
  */
-+ (nullable instancetype)assetWriterWithURL:(NSURL *)outputURL fileType:(NSString *)outputFileType error:(NSError * __nullable * __nullable)outError;
++ (nullable instancetype)assetWriterWithURL:(NSURL *)outputURL fileType:(NSString *)outputFileType error:(NSError * _Nullable * _Nullable)outError;
 
 /*!
  @method initWithURL:fileType:error:
@@ -105,7 +105,7 @@
 	
 	UTIs for container formats that can be written are declared in AVMediaFormat.h.
  */
-- (nullable instancetype)initWithURL:(NSURL *)outputURL fileType:(NSString *)outputFileType error:(NSError * __nullable * __nullable)outError NS_DESIGNATED_INITIALIZER;
+- (nullable instancetype)initWithURL:(NSURL *)outputURL fileType:(NSString *)outputFileType error:(NSError * _Nullable * _Nullable)outError NS_DESIGNATED_INITIALIZER;
 
 /*!
  @property outputURL
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsynchronousKeyValueLoading.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsynchronousKeyValueLoading.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsynchronousKeyValueLoading.h	2015-09-30 23:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsynchronousKeyValueLoading.h	2016-05-25 07:22:13.000000000 +0200
@@ -3,7 +3,7 @@
  
     Framework:  AVFoundation
  
-	Copyright 2010-2015 Apple Inc. All rights reserved.
+	Copyright 2010-2016 Apple Inc. All rights reserved.
  
  */
 
@@ -53,7 +53,7 @@
       
     The sole exception to this general rule is in usage on Mac OS X on the desktop, where it may be acceptable to block in cases in which the client is preparing objects for use on background threads or in operation queues. On iOS, values should always be loaded asynchronously prior to calling getters for the values, in any usage scenario.
 */
-- (AVKeyValueStatus)statusOfValueForKey:(NSString *)key error:(NSError * __nullable * __nullable)outError;
+- (AVKeyValueStatus)statusOfValueForKey:(NSString *)key error:(NSError * _Nullable * _Nullable)outError;
 
 /*!
   @method		loadValuesAsynchronouslyForKeys:completionHandler:
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioBuffer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioBuffer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioBuffer.h	2015-09-30 23:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioBuffer.h	2016-05-25 07:19:41.000000000 +0200
@@ -1,214 +1,9 @@
 /*
-	File:		AVAudioBuffer.h
-	Framework:	AVFoundation
+	File:           AVAudioBuffer.h
+	Framework:      AVFoundation
 	
-	Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioTypes.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-@class AVAudioFormat;
-
-/*!
-	@class AVAudioBuffer
-	@abstract A buffer of audio data, with a format.
-	@discussion
-		AVAudioBuffer represents a buffer of audio data and its format.
-*/
-
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioBuffer : NSObject <NSCopying, NSMutableCopying> {
-@protected
-	void *_impl;
-}
-
-/*!
-	@property format
-	@abstract The format of the audio in the buffer.
-*/
-@property (nonatomic, readonly) AVAudioFormat *format;
-
-/*!	@property audioBufferList
-	@abstract The buffer's underlying AudioBufferList.
-	@discussion
-		For compatibility with lower-level CoreAudio and AudioToolbox API's, this method accesses
-		the buffer implementation's internal AudioBufferList. The buffer list structure must
-		not be modified, though you may modify buffer contents.
-		
-		The mDataByteSize fields of this AudioBufferList express the buffer's current frameLength.
-*/
-@property (nonatomic, readonly) const AudioBufferList *audioBufferList;
-
-/*!	@property mutableAudioBufferList
-	@abstract A mutable version of the buffer's underlying AudioBufferList.
-	@discussion
-		Some lower-level CoreAudio and AudioToolbox API's require a mutable AudioBufferList,
-		for example, AudioConverterConvertComplexBuffer.
-		
-		The mDataByteSize fields of this AudioBufferList express the buffer's current frameCapacity.
-		If they are altered, you should modify the buffer's frameLength to match.
-*/
-@property (nonatomic, readonly) AudioBufferList *mutableAudioBufferList;
-
-@end
-
-// -------------------------------------------------------------------------------------------------
-
-/*!
-	@class AVAudioPCMBuffer
-	@abstract A subclass of AVAudioBuffer for use with PCM audio formats.
-	@discussion
-		AVAudioPCMBuffer provides a number of methods useful for manipulating buffers of
-		audio in PCM format.
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioPCMBuffer : AVAudioBuffer
-
-/*!	@method initWithPCMFormat:frameCapacity:
-	@abstract Initialize a buffer that is to contain PCM audio samples.
-	@param format
-		The format of the PCM audio to be contained in the buffer.
-	@param frameCapacity
-		The capacity of the buffer in PCM sample frames.
-	@discussion
-		An exception is raised if the format is not PCM.
-*/
-- (instancetype)initWithPCMFormat:(AVAudioFormat *)format frameCapacity:(AVAudioFrameCount)frameCapacity NS_DESIGNATED_INITIALIZER;
-
-/*! @property frameCapacity
-	@abstract
-		The buffer's capacity, in audio sample frames.
-*/
-@property (nonatomic, readonly) AVAudioFrameCount frameCapacity;
-
-/*!	@property frameLength
-	@abstract The current number of valid sample frames in the buffer.
-	@discussion
-		You may modify the length of the buffer as part of an operation that modifies its contents.
-		The length must be less than or equal to the frameCapacity. Modifying frameLength will update
-		the mDataByteSize in each of the underlying AudioBufferList's AudioBuffer's correspondingly,
-		and vice versa. Note that in the case of deinterleaved formats, mDataByteSize will refers
-		the size of one channel's worth of audio samples.
-*/
-@property (nonatomic) AVAudioFrameCount frameLength;
-
-/*!	@property stride
-	@abstract The buffer's number of interleaved channels.
-	@discussion
-		Useful in conjunction with floatChannelData etc.
-*/
-@property (nonatomic, readonly) NSUInteger stride;
-
-/*! @property floatChannelData
-	@abstract Access the buffer's float audio samples.
-	@discussion
-		floatChannelData returns pointers to the buffer's audio samples if the buffer's format is
-		32-bit float, or nil if it is another format.
-	
-		The returned pointer is to format.channelCount pointers to float. Each of these pointers
-		is to "frameLength" valid samples, which are spaced by "stride" samples.
-		
-		If format.interleaved is false (as with the standard deinterleaved float format), then 
-		the pointers will be to separate chunks of memory. "stride" is 1.
-		
-		If format.interleaved is true, then the pointers will refer into the same chunk of interleaved
-		samples, each offset by 1 frame. "stride" is the number of interleaved channels.
-*/
-@property (nonatomic, readonly) float * __nonnull const * __nullable floatChannelData;
-
-/*!	@property int16ChannelData
-	@abstract Access the buffer's int16_t audio samples.
-	@discussion
-		int16ChannelData returns the buffer's audio samples if the buffer's format has 2-byte
-		integer samples, or nil if it is another format.
-		
-		See the discussion of floatChannelData.
-*/
-@property (nonatomic, readonly) int16_t * __nonnull const * __nullable int16ChannelData;
-
-/*!	@property int32ChannelData
-	@abstract Access the buffer's int32_t audio samples.
-	@discussion
-		int32ChannelData returns the buffer's audio samples if the buffer's format has 4-byte
-		integer samples, or nil if it is another format.
-		
-		See the discussion of floatChannelData.
-*/
-@property (nonatomic, readonly) int32_t * __nonnull const * __nullable int32ChannelData;
-
-@end
-
-
-// -------------------------------------------------------------------------------------------------
-
-/*!
-	@class AVAudioCompressedBuffer
-	@abstract A subclass of AVAudioBuffer for use with compressed audio formats.
-*/
-NS_CLASS_AVAILABLE(10_11, 9_0)
-@interface AVAudioCompressedBuffer : AVAudioBuffer
-
-/*!	@method initWithFormat:packetCapacity:maximumPacketSize:
-	@abstract Initialize a buffer that is to contain compressed audio data. 
-	@param format
-		The format of the audio to be contained in the buffer.
-	@param packetCapacity
-		The capacity of the buffer in packets.
-	@param maximumPacketSize
-		The maximum size in bytes of a compressed packet. 
-		The maximum packet size can be obtained from the maximumOutputPacketSize property of an AVAudioConverter configured for encoding this format.
-	@discussion
-		An exception is raised if the format is PCM.
-*/
-- (instancetype)initWithFormat:(AVAudioFormat *)format packetCapacity:(AVAudioPacketCount)packetCapacity maximumPacketSize:(NSInteger)maximumPacketSize;
-
-/*!	@method initWithFormat:packetCapacity:
-	@abstract Initialize a buffer that is to contain constant bytes per packet compressed audio data.
-	@param format
-		The format of the audio to be contained in the buffer.
-	@param packetCapacity
-		The capacity of the buffer in packets.
-	@discussion
-		This fails if the format is PCM or if the format has variable bytes per packet (format.streamDescription->mBytesPerPacket == 0).
-*/
-- (instancetype)initWithFormat:(AVAudioFormat *)format packetCapacity:(AVAudioPacketCount)packetCapacity;
-
-/*! @property packetCapacity
-	@abstract
-		The number of compressed packets the buffer can contain.
-*/
-@property (nonatomic, readonly) AVAudioPacketCount packetCapacity;
-
-/*!	@property packetCount
-	@abstract The current number of compressed packets in the buffer.
-	@discussion
-		You may modify the packet length as part of an operation that modifies its contents.
-		The packet length must be less than or equal to the packetCapacity.
-*/
-@property (nonatomic) AVAudioPacketCount packetCount;
-
-/*!	@property maximumPacketSize
-	@abstract The maximum size of a compressed packet in bytes.
-*/
-@property (nonatomic, readonly) NSInteger maximumPacketSize;
-
-/*! @property data
-	@abstract Access the buffer's data bytes.
-*/
-@property (nonatomic, readonly) void *data;
-
-/*! @property packetDescriptions
-	@abstract Access the buffer's array of packet descriptions, if any.
-	@discussion
-		If the format has constant bytes per packet (format.streamDescription->mBytesPerPacket != 0), then this will return nil.
-*/
-@property (nonatomic, readonly, nullable) AudioStreamPacketDescription *packetDescriptions;
-
-@end
-
-NS_ASSUME_NONNULL_END
-
-// -------------------------------------------------------------------------------------------------
+#import <AVFAudio/AVAudioBuffer.h>
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioChannelLayout.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioChannelLayout.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioChannelLayout.h	2015-09-30 23:17:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioChannelLayout.h	2016-05-25 07:19:41.000000000 +0200
@@ -1,81 +1,9 @@
 /*
-	File:		AVAudioChannelLayout.h
-	Framework:	AVFoundation
+	File:           AVAudioChannelLayout.h
+	Framework:      AVFoundation
 	
-	Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioTypes.h>
-#import <CoreAudio/CoreAudioTypes.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-/*!
-	@class AVAudioChannelLayout
-	@abstract A description of the roles of a set of audio channels.
-	@discussion
-		This object is a thin wrapper for the AudioChannelLayout structure, described
-		in <CoreAudio/CoreAudioTypes.h>.
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioChannelLayout : NSObject <NSSecureCoding> {
-@private
-	AudioChannelLayoutTag _layoutTag;
-	AudioChannelLayout * _layout;
-	void *_reserved;
-}
-
-
-/*!	@method initWithLayoutTag:
-	@abstract Initialize from a layout tag.
-	@param layoutTag
-		The tag.
-*/
-- (instancetype)initWithLayoutTag:(AudioChannelLayoutTag)layoutTag;
-
-/*!	@method initWithLayout:
-	@abstract Initialize from an AudioChannelLayout.
-	@param layout
-		The AudioChannelLayout.
-	@discussion
-		If the provided layout's tag is kAudioChannelLayoutTag_UseChannelDescriptions, this
-		initializer attempts to convert it to a more specific tag.
-*/
-- (instancetype)initWithLayout:(const AudioChannelLayout *)layout NS_DESIGNATED_INITIALIZER;
-
-/*!	@method isEqual:
-	@abstract Determine whether another AVAudioChannelLayout is exactly equal to this layout.
-	@param object
-		The AVAudioChannelLayout to compare against.
-	@discussion
-		The underlying AudioChannelLayoutTag and AudioChannelLayout are compared for equality.
-*/
-- (BOOL)isEqual:(id)object;
-
-/*!	@method layoutWithLayoutTag:
-	@abstract Create from a layout tag.
-*/
-+ (instancetype)layoutWithLayoutTag:(AudioChannelLayoutTag)layoutTag;
-
-/*!	@method layoutWithLayout:
-	@abstract Create from an AudioChannelLayout
-*/
-+ (instancetype)layoutWithLayout:(const AudioChannelLayout *)layout;
-
-/*!	@property layoutTag
-	@abstract The layout's tag. */
-@property (nonatomic, readonly) AudioChannelLayoutTag layoutTag;
-
-/*!	@property layout
-	@abstract The underlying AudioChannelLayout. */
-@property (nonatomic, readonly) const AudioChannelLayout *layout;
-
-/*! @property channelCount
-	@abstract The number of channels of audio data.
-*/
-@property (nonatomic, readonly) AVAudioChannelCount channelCount;
-
-@end
-
-NS_ASSUME_NONNULL_END
+#import <AVFAudio/AVAudioChannelLayout.h>
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioConnectionPoint.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioConnectionPoint.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioConnectionPoint.h	2015-09-30 23:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioConnectionPoint.h	2016-05-25 07:19:41.000000000 +0200
@@ -1,52 +1,9 @@
 /*
-	File:		AVAudioConnectionPoint.h
-	Framework:	AVFoundation
+	File:           AVAudioConnectionPoint.h
+	Framework:      AVFoundation
 	
-	Copyright (c) 2015 Apple Inc. All Rights Reserved.
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioTypes.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-@class AVAudioNode;
-
-/*! @class AVAudioConnectionPoint
-	@abstract A representation of either a source or destination connection point in AVAudioEngine.
-	@discussion
-		AVAudioConnectionPoint describes either a source or destination connection point (node, bus)
-		in AVAudioEngine's graph.
-	
-		Instances of this class are immutable.
-*/
-NS_CLASS_AVAILABLE(10_11, 9_0)
-@interface AVAudioConnectionPoint : NSObject {
-@private
-	AVAudioNode *_node;
-	AVAudioNodeBus _bus;
-	void *_reserved;
-}
-
-/*! @method initWithNode:bus:
-	@abstract Create a connection point object.
-	@param node the source or destination node
-	@param bus the output or input bus on the node
-	@discussion
-		If the node is nil, this method fails (returns nil).
-*/
-- (instancetype)initWithNode:(AVAudioNode *)node bus:(AVAudioNodeBus)bus NS_DESIGNATED_INITIALIZER;
-
-/*!	@property node
-	@abstract Returns the node in the connection point.
-*/
-@property (nonatomic, readonly, weak) AVAudioNode *node;
-
-/*!	@property bus
-	@abstract Returns the bus on the node in the connection point.
-*/
-@property (nonatomic, readonly) AVAudioNodeBus bus;
-
-@end
-
-NS_ASSUME_NONNULL_END
+#import <AVFAudio/AVAudioConnectionPoint.h>
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioConverter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioConverter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioConverter.h	2015-09-30 23:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioConverter.h	2016-05-25 07:19:41.000000000 +0200
@@ -1,318 +1,9 @@
 /*
-	File:		AVAudioConverter.h
-	Framework:	AVFoundation
+	File:           AVAudioConverter.h
+	Framework:      AVFoundation
 	
-	Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioTypes.h>
-#import <AVFoundation/AVAudioFormat.h>
-#import <AVFoundation/AVAudioBuffer.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-/*! @enum AVAudioConverterPrimeMethod
-    @abstract values for the primeMethod property. See further discussion under AVAudioConverterPrimeInfo.
-     
-        AVAudioConverterPrimeMethod_Pre
-            Primes with leading + trailing input frames.
-     
-        AVAudioConverterPrimeMethod_Normal
-			Only primes with trailing (zero latency). Leading frames are assumed to be silence.
-     
-        AVAudioConverterPrimeMethod_None
-			Acts in "latency" mode. Both leading and trailing frames assumed to be silence.
-*/
-typedef NS_ENUM(NSInteger, AVAudioConverterPrimeMethod) {
-    AVAudioConverterPrimeMethod_Pre       = 0,
-    AVAudioConverterPrimeMethod_Normal    = 1,
-    AVAudioConverterPrimeMethod_None      = 2
-};
-
-/*!
-    @struct     AVAudioConverterPrimeInfo
-    @abstract   This struct is the value of the primeInfo property and specifies priming information.
-    
-    @field      leadingFrames
-        Specifies the number of leading (previous) input frames, relative to the normal/desired
-        start input frame, required by the converter to perform a high quality conversion. If
-        using AVAudioConverterPrimeMethod_Pre, the client should "pre-seek" the input stream provided
-        through the input proc by leadingFrames. If no frames are available previous to the
-        desired input start frame (because, for example, the desired start frame is at the very
-        beginning of available audio), then provide "leadingFrames" worth of initial zero frames
-        in the input proc.  Do not "pre-seek" in the default case of
-        AVAudioConverterPrimeMethod_Normal or when using AVAudioConverterPrimeMethod_None.
-
-    @field      trailingFrames
-        Specifies the number of trailing input frames (past the normal/expected end input frame)
-        required by the converter to perform a high quality conversion.  The client should be
-        prepared to provide this number of additional input frames except when using
-        AVAudioConverterPrimeMethod_None. If no more frames of input are available in the input stream
-        (because, for example, the desired end frame is at the end of an audio file), then zero
-        (silent) trailing frames will be synthesized for the client.
-            
-    @discussion
-        When using convertToBuffer:error:withInputFromBlock: (either a single call or a series of calls), some
-        conversions, particularly involving sample-rate conversion, ideally require a certain
-        number of input frames previous to the normal start input frame and beyond the end of
-        the last expected input frame in order to yield high-quality results.
-        
-        These are expressed in the leadingFrames and trailingFrames members of the structure.
-        
-        The very first call to convertToBuffer:error:withInputFromBlock:, or first call after
-        reset, will request additional input frames beyond those normally
-        expected in the input proc callback to fulfill this first AudioConverterFillComplexBuffer()
-        request. The number of additional frames requested, depending on the prime method, will
-        be approximately:
-
-        <pre>
-            AVAudioConverterPrimeMethod_Pre       leadingFrames + trailingFrames
-            AVAudioConverterPrimeMethod_Normal    trailingFrames
-            AVAudioConverterPrimeMethod_None      0
-        </pre>
-
-        Thus, in effect, the first input proc callback(s) may provide not only the leading
-        frames, but also may "read ahead" by an additional number of trailing frames depending
-        on the prime method.
-
-        AVAudioConverterPrimeMethod_None is useful in a real-time application processing live input,
-        in which case trailingFrames (relative to input sample rate) of through latency will be
-        seen at the beginning of the output of the AudioConverter.  In other real-time
-        applications such as DAW systems, it may be possible to provide these initial extra
-        audio frames since they are stored on disk or in memory somewhere and
-        AVAudioConverterPrimeMethod_Pre may be preferable.  The default method is
-        AVAudioConverterPrimeMethod_Normal, which requires no pre-seeking of the input stream and
-        generates no latency at the output.
-*/
-typedef struct AVAudioConverterPrimeInfo {
-    AVAudioFrameCount      leadingFrames;
-    AVAudioFrameCount      trailingFrames;
-} AVAudioConverterPrimeInfo;
-
-
-/*! @enum AVAudioConverterInputStatus
-    @abstract You must return one of these codes from your AVAudioConverterInputBlock.
-     
-        AVAudioConverterInputStatus_HaveData
-            This is the normal case where you supply data to the converter.
-     
-        AVAudioConverterInputStatus_NoDataNow
-			If you are out of data for now, set *ioNumberOfPackets = 0 and return AVAudioConverterInputStatus_NoDataNow and the 
-			conversion routine will return as much output as could be converted with the input already supplied.
-     
-        AVAudioConverterInputStatus_EndOfStream
-			If you are at the end of stream, set *ioNumberOfPackets = 0 and return AVAudioConverterInputStatus_EndOfStream.
-*/
-typedef NS_ENUM(NSInteger, AVAudioConverterInputStatus) {
-	AVAudioConverterInputStatus_HaveData    = 0,
-	AVAudioConverterInputStatus_NoDataNow   = 1,
-	AVAudioConverterInputStatus_EndOfStream = 2
-}  NS_ENUM_AVAILABLE(10_11, 9_0);
-
-/*! @enum AVAudioConverterOutputStatus
-    @abstract These values are returned from convertToBuffer:error:withInputFromBlock:
-
-		AVAudioConverterOutputStatus_HaveData
-			All of the requested data was returned.
-
-		AVAudioConverterOutputStatus_InputRanDry
-			Not enough input was available to satisfy the request at the current time. The output buffer contains as much as could be converted.
-			
-		AVAudioConverterOutputStatus_EndOfStream
-			The end of stream has been reached. No data was returned.
-		
-		AVAudioConverterOutputStatus_Error
-			An error occurred.
-*/
-typedef NS_ENUM(NSInteger, AVAudioConverterOutputStatus) {
-	AVAudioConverterOutputStatus_HaveData          = 0,
-	AVAudioConverterOutputStatus_InputRanDry       = 1,
-	AVAudioConverterOutputStatus_EndOfStream       = 2,
-	AVAudioConverterOutputStatus_Error             = 3
-}  NS_ENUM_AVAILABLE(10_11, 9_0);
-
-/*! @typedef AVAudioConverterInputBlock
-    @abstract A block which will be called by convertToBuffer:error:withInputFromBlock: to get input data as needed. 
-	@param  inNumberOfPackets
-		This will be the number of packets required to complete the request.
-		You may supply more or less that this amount. If less, then the input block will get called again.
-	@param outStatus
-		The block must set the appropriate AVAudioConverterInputStatus enum value.
-		If you have supplied data, set outStatus to AVAudioConverterInputStatus_HaveData and return an AVAudioBuffer.
-		If you are out of data for now, set outStatus to AVAudioConverterInputStatus_NoDataNow and return nil, and the
-		conversion routine will return as much output as could be converted with the input already supplied.
-		If you are at the end of stream, set outStatus to AVAudioConverterInputStatus_EndOfStream, and return nil.
-	@return
-		An AVAudioBuffer containing data to be converted, or nil if at end of stream or no data is available.
-		The data in the returned buffer must not be cleared or re-filled until the input block is called again or the conversion has finished.
-	@discussion
-		convertToBuffer:error:withInputFromBlock: will return as much output as could be converted with the input already supplied.
-*/
-typedef AVAudioBuffer * __nullable (^AVAudioConverterInputBlock)(AVAudioPacketCount inNumberOfPackets, AVAudioConverterInputStatus* outStatus);
-
-/*!
-	@class AVAudioConverter
-	@abstract
-		AVAudioConverter converts streams of audio between various formats.
-	@discussion
-*/
-NS_CLASS_AVAILABLE(10_11, 9_0)
-@interface AVAudioConverter : NSObject {
-@private
-	void *_impl;
-}
-
-/*!	@method initFromFormat:toFormat:
-	@abstract Initialize from input and output formats.
-	@param fromFormat 
-		The input format.
-	@param toFormat 
-		The output format.
-*/
-- (instancetype)initFromFormat:(AVAudioFormat *)fromFormat toFormat:(AVAudioFormat *)toFormat;
-
-
-/*! @method reset
-    @abstract Resets the converter so that a new stream may be converted.
-*/
-- (void)reset;
-
-/*! @property inputFormat
-    @abstract The format of the input audio stream. (NB. AVAudioFormat includes the channel layout)
-*/
-@property (nonatomic, readonly) AVAudioFormat *inputFormat;
-
-/*! @property outputFormat
-    @abstract The format of the output audio stream. (NB. AVAudioFormat includes the channel layout)
-*/
-@property (nonatomic, readonly) AVAudioFormat *outputFormat;
-
-/*! @property channelMap
-    @abstract An array of integers indicating from which input to derive each output.
-	@discussion 
-		The array has size equal to the number of output channels. Each element's value is
-		the input channel number, starting with zero, that is to be copied to that output. A negative value means 
-		that the output channel will have no source and will be silent.
-		Setting a channel map overrides channel mapping due to any channel layouts in the input and output formats that may have been supplied.
-*/
-@property (nonatomic, retain) NSArray<NSNumber *> *channelMap;
-
-/*! @property magicCookie
-    @abstract Decoders require some data in the form of a magicCookie in order to decode properly. Encoders will produce a magicCookie.
-*/
-@property (nonatomic, retain, nullable) NSData *magicCookie;
-
-/*! @property downmix
-    @abstract If YES and channel remapping is necessary, then channels will be mixed as appropriate instead of remapped. Default value is NO.
-*/
-@property (nonatomic) BOOL downmix;
-
-/*! @property dither
-    @abstract Setting YES will turn on dither, if dither makes sense in given the current formats and settings. Default value is NO.
-*/
-@property (nonatomic) BOOL dither;
-
-/*! @property sampleRateConverterQuality
-    @abstract An AVAudioQuality value as defined in AVAudioSettings.h.
-*/
-@property (nonatomic) NSInteger sampleRateConverterQuality;
-
-/*! @property sampleRateConverterAlgorithm
-    @abstract An AVSampleRateConverterAlgorithmKey value as defined in AVAudioSettings.h.
-*/
-@property (nonatomic, retain) NSString *sampleRateConverterAlgorithm;
-
-/*! @property primeMethod
-    @abstract Indicates the priming method to be used by the sample rate converter or decoder.
-*/
-@property (nonatomic) AVAudioConverterPrimeMethod primeMethod;
-
-/*! @property primeInfo
-    @abstract Indicates the the number of priming frames .
-*/
-@property (nonatomic) AVAudioConverterPrimeInfo primeInfo;
-
-
-/*! @method convertToBuffer:fromBuffer:error:
-    @abstract Perform a simple conversion. That is, a conversion which does not involve codecs or sample rate conversion.
-	@param inputBuffer 
-		The input buffer.
-	@param outputBuffer 
-		The output buffer.
-	@param outError 
-		An error if the conversion fails.
-	@return 
-		YES is returned on success, NO when an error has occurred.
-	@discussion 
-		The output buffer's frameCapacity should be at least at large as the inputBuffer's frameLength.
-		If the conversion involves a codec or sample rate conversion, you instead must use
-		convertToBuffer:error:withInputFromBlock:.
-*/
-- (BOOL)convertToBuffer:(AVAudioPCMBuffer *)outputBuffer fromBuffer:(const AVAudioPCMBuffer *)inputBuffer error:(NSError **)outError;
-
-/*! @method convertToBuffer:error:withInputFromBlock:
-    @abstract Perform any supported conversion. 
-	@param inputBlock
-		A block which will be called to get input data as needed. See description for AVAudioConverterInputBlock.
-	@param outputBuffer 
-		The output buffer.
-	@param outError 
-		An error if the conversion fails.
-	@return 
-		An AVAudioConverterOutputStatus is returned.
-	@discussion 
-		It attempts to fill the buffer to its capacity. On return, the buffer's length indicates the number of 
-		sample frames successfully converted.
-*/
-- (AVAudioConverterOutputStatus)convertToBuffer:(AVAudioBuffer *)outputBuffer error:(NSError **)outError withInputFromBlock:(AVAudioConverterInputBlock)inputBlock;
-
-@end
-
-
-@interface AVAudioConverter (Encoding)
-
-/*! @property bitRate
-    @abstract bitRate in bits per second. Only applies when encoding.
-*/
-@property (nonatomic) NSInteger bitRate;
-
-/*! @property bitRateStrategy
-    @abstract When encoding, an AVEncoderBitRateStrategyKey value constant as defined in AVAudioSettings.h. Returns nil if not encoding.
-*/
-@property (nonatomic, retain, nullable) NSString *bitRateStrategy;
-
-/*! @property maximumOutputPacketSize
-    @abstract When encoding it is useful to know how large a packet can be in order to allocate a buffer to receive the output.
-*/
-@property (nonatomic, readonly) NSInteger maximumOutputPacketSize;
-
-/*! @property availableEncodeBitRates
-    @abstract When encoding, an NSArray of NSNumber of all bit rates provided by the codec. Returns nil if not encoding.
-*/
-@property (nonatomic, readonly, nullable) NSArray<NSNumber *> *availableEncodeBitRates;
-
-/*! @property applicableEncodeBitRates
-    @abstract When encoding, an NSArray of NSNumber of bit rates that can be applied based on the current formats and settings. Returns nil if not encoding.
-*/
-@property (nonatomic, readonly, nullable) NSArray<NSNumber *> *applicableEncodeBitRates;
-
-/*! @property availableEncodeSampleRates
-    @abstract When encoding, an NSArray of NSNumber of all output sample rates provided by the codec. Returns nil if not encoding.
-*/
-@property (nonatomic, readonly, nullable) NSArray<NSNumber *> *availableEncodeSampleRates;
-
-/*! @property applicableEncodeSampleRates
-    @abstract When encoding, an NSArray of NSNumber of output sample rates that can be applied based on the current formats and settings. Returns nil if not encoding.
-*/
-@property (nonatomic, readonly, nullable) NSArray<NSNumber *> *applicableEncodeSampleRates;
-
-/*! @property availableEncodeChannelLayoutTags
-    @abstract When encoding, an NSArray of NSNumber of all output channel layout tags provided by the codec. Returns nil if not encoding.
-*/
-@property (nonatomic, readonly, nullable) NSArray<NSNumber *> *availableEncodeChannelLayoutTags;
-
-@end
-
-
-NS_ASSUME_NONNULL_END
+#import <AVFAudio/AVAudioConverter.h>
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioEngine.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioEngine.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioEngine.h	2015-09-30 23:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioEngine.h	2016-05-25 07:19:41.000000000 +0200
@@ -1,328 +1,9 @@
 /*
-	File:		AVAudioEngine.h
-	Framework:	AVFoundation
+	File:           AVAudioEngine.h
+	Framework:      AVFoundation
 	
-	Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioTypes.h>
-#import <AudioToolbox/MusicPlayer.h>
-#import <AVFoundation/AVAudioConnectionPoint.h>
+#import <AVFAudio/AVAudioEngine.h>
 
-NS_ASSUME_NONNULL_BEGIN
-
-@class AVAudioFormat, AVAudioNode, AVAudioInputNode, AVAudioOutputNode, AVAudioMixerNode;
-
-/*!
-	@class AVAudioEngine
-	@discussion
-		An AVAudioEngine contains a group of connected AVAudioNodes ("nodes"), each of which performs
-		an audio signal generation, processing, or input/output task.
-		
-		Nodes are created separately and attached to the engine.
-
-		The engine supports dynamic connection, disconnection and removal of nodes while running,
-		with only minor limitations:
-		- all dynamic reconnections must occur upstream of a mixer
-		- while removals of effects will normally result in the automatic connection of the adjacent
-			nodes, removal of a node which has differing input vs. output channel counts, or which
-			is a mixer, is likely to result in a broken graph.
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioEngine : NSObject {
-@private
-	void *_impl;
-}
-
-/*! @method init
-	@abstract
-		Initialize a new engine.
-*/
-- (instancetype)init;
-
-/*!	@method attachNode:
-	@abstract
-		Take ownership of a new node.
-	@param node
-		The node to be attached to the engine.
-	@discussion
-		To support the instantiation of arbitrary AVAudioNode subclasses, instances are created
-		externally to the engine, but are not usable until they are attached to the engine via
-		this method. Thus the idiom, without ARC, is:
-
-<pre>
-// when building engine:
-AVAudioNode *_player;	// member of controller class (for example)
-...
-_player = [[AVAudioPlayerNode alloc] init];
-[engine attachNode: _player];
-...
-// when destroying engine (without ARC)
-[_player release];
-</pre>
-*/
-- (void)attachNode:(AVAudioNode *)node;
-
-/*!	@method detachNode:
-	@abstract
-		Detach a node previously attached to the engine.
-	@discussion
-		If necessary, the engine will safely disconnect the node before detaching it.
-*/
-- (void)detachNode:(AVAudioNode *)node;
-
-/*! @method connect:to:fromBus:toBus:format:
-	@abstract
-		Establish a connection between two nodes.
-	@param node1 the source node
-	@param node2 the destination node
-	@param bus1 the output bus on the source node
-	@param bus2 the input bus on the destination node
-	@param format if non-nil, the format of the source node's output bus is set to this
-		format. In all cases, the format of the destination node's input bus is set to
-		match that of the source node's output bus.
-	@discussion
-		Nodes have input and output buses (AVAudioNodeBus). Use this method to establish
-		one-to-one connections betweeen nodes. Connections made using this method are always
-		one-to-one, never one-to-many or many-to-one.
-	
-		Note that any pre-existing connection(s) involving the source's output bus or the
-		destination's input bus will be broken.
-*/
-- (void)connect:(AVAudioNode *)node1 to:(AVAudioNode *)node2 fromBus:(AVAudioNodeBus)bus1 toBus:(AVAudioNodeBus)bus2 format:(AVAudioFormat * __nullable)format;
-
-/*!	@method connect:to:format:
-	@abstract
-		Establish a connection between two nodes
-	@discussion
-		This calls connect:to:fromBus:toBus:format: using bus 0 on the source node,
-		and bus 0 on the destination node, except in the case of a destination which is a mixer,
-		in which case the destination is the mixer's nextAvailableInputBus.
-*/
-- (void)connect:(AVAudioNode *)node1 to:(AVAudioNode *)node2 format:(AVAudioFormat * __nullable)format;
-
-/*! @method connect:toConnectionPoints:fromBus:format:
-	@abstract
-		Establish connections between a source node and multiple destination nodes.
-	@param sourceNode the source node
-	@param destNodes an array of AVAudioConnectionPoint objects specifying destination 
-		nodes and busses
-	@param sourceBus the output bus on source node
-	@param format if non-nil, the format of the source node's output bus is set to this
-		format. In all cases, the format of the destination nodes' input bus is set to
-		match that of the source node's output bus
-	@discussion
-		Use this method to establish connections from a source node to multiple destination nodes.
-		Connections made using this method are either one-to-one (when a single destination
-		connection is specified) or one-to-many (when multiple connections are specified), but 
-		never many-to-one.
-
-		To incrementally add a new connection to a source node, use this method with an array
-		of AVAudioConnectionPoint objects comprising of pre-existing connections (obtained from
-		`outputConnectionPointsForNode:outputBus:`) and the new connection.
- 
-		Note that any pre-existing connection involving the destination's input bus will be 
-		broken. And, any pre-existing connection on source node which is not a part of the
-		specified destination connection array will also be broken.
-
-		Also note that when the output of a node is split into multiple paths, all the paths
-		must render at the same rate until they reach a common mixer.
-		In other words, starting from the split node until the common mixer node where all split 
-		paths terminate, you cannot have:
-			- any AVAudioUnitTimeEffect
-			- any sample rate conversion
-*/
-- (void)connect:(AVAudioNode *)sourceNode toConnectionPoints:(NSArray<AVAudioConnectionPoint *> *)destNodes fromBus:(AVAudioNodeBus)sourceBus format:(AVAudioFormat * __nullable)format NS_AVAILABLE(10_11, 9_0);
-
-/*! @method disconnectNodeInput:bus:
-	@abstract
-		Remove a connection between two nodes.
-	@param node the node whose input is to be disconnected
-	@param bus the destination's input bus to disconnect
-*/
-- (void)disconnectNodeInput:(AVAudioNode *)node bus:(AVAudioNodeBus)bus;
-
-/*!	@method disconnectNodeInput:
-	@abstract
-		Remove a connection between two nodes.
-	@param node the node whose inputs are to be disconnected
-	@discussion
-		Connections are broken on each of the node's input busses.
-*/
-- (void)disconnectNodeInput:(AVAudioNode *)node;
-
-/*! @method disconnectNodeOutput:bus:
-	@abstract
-		Remove a connection between two nodes.
-	@param node the node whose output is to be disconnected
-	@param bus the source's output bus to disconnect
-*/
-- (void)disconnectNodeOutput:(AVAudioNode *)node bus:(AVAudioNodeBus)bus;
-
-/*!	@method disconnectNodeOutput:
-	@abstract
-		Remove a connection between two nodes.
-	@param node the node whose outputs are to be disconnected
-	@discussion
-		Connections are broken on each of the node's output busses.
-*/
-- (void)disconnectNodeOutput:(AVAudioNode *)node;
-
-/*!	@method prepare
-	@abstract
-		Prepare the engine for starting.
-	@discussion
-		This method preallocates many of the resources the engine requires in order to start.
-		It can be used to be able to start more responsively.
-*/
-- (void)prepare;
-
-/*! @method startAndReturnError:
-	@abstract
-		Start the engine.
-	@return
-		YES for success
-	@discussion
-		Calls prepare if it has not already been called since stop.
-	
-		Starts the audio hardware via the AVAudioInputNode and/or AVAudioOutputNode instances in
-		the engine. Audio begins flowing through the engine.
-	
-		Reasons for potential failure include:
-		
-		1. There is problem in the structure of the graph. Input can't be routed to output or to a
-			recording tap through converter type nodes.
-		2. An AVAudioSession error.
-		3. The driver failed to start the hardware.
-*/
-- (BOOL)startAndReturnError:(NSError **)outError;
-
-/*!	@method pause
-	@abstract
-		Pause the engine.
-	@discussion
-		Stops the flow of audio through the engine, but does not deallocate the resources allocated
-		by prepare. Resume the engine by invoking start again.
-*/
-- (void)pause;
-
-/*!	@method reset
-	@abstract reset
-		Reset all of the nodes in the engine.
-	@discussion
-		This will reset all of the nodes in the engine. This is useful, for example, for silencing
-		reverb and delay tails.
-*/
-- (void)reset;
-
-/*! @method stop
-	@abstract
-		Stop the engine. Releases the resources allocated by prepare.
-*/
-- (void)stop;
-
-/*! @method inputConnectionPointForNode:inputBus:
-	@abstract 
-		Get connection information on a node's input bus.
-	@param node the node whose input connection is being queried.
-	@param bus the node's input bus on which the connection is being queried.
-	@return	
-		An AVAudioConnectionPoint object with connection information on the node's
-		specified input bus.
-	@discussion
-		Connections are always one-to-one or one-to-many, never many-to-one.
- 
-		Returns nil if there is no connection on the node's specified input bus.
-*/
-- (AVAudioConnectionPoint * __nullable)inputConnectionPointForNode:(AVAudioNode *)node inputBus:(AVAudioNodeBus)bus NS_AVAILABLE(10_11, 9_0);
-
-/*! @method outputConnectionPointsForNode:outputBus:
-	@abstract
-		Get connection information on a node's output bus.
-	@param node the node whose output connections are being queried.
-	@param bus the node's output bus on which connections are being queried.
-	@return
-		An array of AVAudioConnectionPoint objects with connection information on the node's
-		specified output bus.
-	@discussion
-		Connections are always one-to-one or one-to-many, never many-to-one.
- 
-		Returns an empty array if there are no connections on the node's specified output bus.
-*/
-- (NSArray<AVAudioConnectionPoint *> *)outputConnectionPointsForNode:(AVAudioNode *)node outputBus:(AVAudioNodeBus)bus NS_AVAILABLE(10_11, 9_0);
-
-/*! @property musicSequence
-	@abstract
-		The MusicSequence previously attached to the engine (if any).
- */
-@property (nonatomic, nullable) MusicSequence musicSequence;
-
-/*! @property outputNode
-	@abstract
-		The engine's singleton output node.
-	@discussion
-		Audio output is performed via an output node. The engine creates a singleton on demand when
-		this property is first accessed. Connect another node to the input of the output node, or obtain
-		a mixer that is connected there by default, using the "mainMixerNode" property.
- 
-		The AVAudioSesssion category and/or availability of hardware determine whether an app can
-		perform output. Check the output format of output node (i.e. hardware format) for non-zero
-		sample rate and channel count to see if output is enabled.
-*/
-@property (readonly, nonatomic) AVAudioOutputNode *outputNode;
-
-/*! @property inputNode
-	@abstract
-		The engine's singleton input node.
-	@discussion
-		Audio input is performed via an input node. The engine creates a singleton on demand when
-		this property is first accessed. To receive input, connect another node from the output of 
-		the input node, or create a recording tap on it.
- 
-		The AVAudioSesssion category and/or availability of hardware determine whether an app can
-		perform input. Check for non-nil input node and its input format (i.e. hardware format) for non-zero
-		sample rate and channel count to see if input is enabled.
-*/
-
-@property (readonly, nonatomic, nullable) AVAudioInputNode *inputNode __TVOS_UNAVAILABLE;
-
-
-/*! @property mainMixerNode
-	@abstract
-		The engine's optional singleton main mixer node.
-	@discussion
-		The engine will construct a singleton main mixer and connect it to the outputNode on demand,
-		when this property is first accessed. You can then connect additional nodes to the mixer.
-		
-		By default, the mixer's output format (sample rate and channel count) will track the format 
-		of the output node. You may however make the connection explicitly with a different format.
-*/
-@property (readonly, nonatomic) AVAudioMixerNode *mainMixerNode;
-
-/*! @property running
-	@abstract
-		The engine's running state.
-*/
-@property (readonly, nonatomic, getter=isRunning) BOOL running;
-
-@end
-
-/*!	@constant AVAudioEngineConfigurationChangeNotification
-	@abstract
-		A notification generated on engine configuration changes.
-	@discussion
-		Register for this notification on your engine instances, as follows:
-		
-		[[NSNotificationCenter defaultCenter] addObserver: myObject 
-			 selector:    @selector(handleInterruption:)
-			 name:        AVAudioEngineConfigurationChangeNotification
-			 object:      engine];
-
-		When the engine's I/O unit observes a change to the audio input or output hardware's
-		channel count or sample rate, the engine stops, uninitializes itself, and issues this 
-		notification.	
-*/
-AVF_EXPORT
-NSString *const AVAudioEngineConfigurationChangeNotification NS_AVAILABLE(10_10, 8_0);
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioEnvironmentNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioEnvironmentNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioEnvironmentNode.h	2015-09-30 23:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioEnvironmentNode.h	2016-05-25 07:19:41.000000000 +0200
@@ -1,263 +1,9 @@
 /*
-    File:       AVAudioEnvironmentNode.h
-    Framework:	AVFoundation
- 
-    Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	File:           AVAudioEnvironmentNode.h
+	Framework:      AVFoundation
+	
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioNode.h>
-#import <AVFoundation/AVAudioUnitReverb.h>
-#import <AVFoundation/AVAudioUnitEQ.h>
-#import <AVFoundation/AVAudioMixing.h>
+#import <AVFAudio/AVAudioEnvironmentNode.h>
 
-NS_ASSUME_NONNULL_BEGIN
-
-/*! @enum AVAudioEnvironmentDistanceAttenuationModel
-    @abstract Types of distance attenuation models
-    @discussion
-        Distance attenuation is the natural attenuation of sound when traveling from the source to 
-        the listener. The different attenuation models listed below describe the drop-off in gain as 
-        the source moves away from the listener.
-     
-        AVAudioEnvironmentDistanceAttenuationModelExponential
-            distanceGain = (distance / referenceDistance) ^ (-rolloffFactor)
-     
-        AVAudioEnvironmentDistanceAttenuationModelInverse
-            distanceGain = referenceDistance /  (referenceDistance + rolloffFactor *
-                                                (distance – referenceDistance))
-     
-        AVAudioEnvironmentDistanceAttenuationModelLinear
-            distanceGain = (1 – rolloffFactor * (distance – referenceDistance) /
-                                                (maximumDistance – referenceDistance))
-     
-        With all the distance models, if the formula can not be evaluated then the source will not 
-        be attenuated. For example, if a linear model is being used with referenceDistance equal 
-        to maximumDistance, then the gain equation will have a divide-by-zero error in it. In this case,
-        there is no attenuation for that source.
-     
-        All the values for distance are specified in meters.
-*/
-typedef NS_ENUM(NSInteger, AVAudioEnvironmentDistanceAttenuationModel) {
-    AVAudioEnvironmentDistanceAttenuationModelExponential   = 1,
-    AVAudioEnvironmentDistanceAttenuationModelInverse       = 2,
-    AVAudioEnvironmentDistanceAttenuationModelLinear        = 3
-} NS_ENUM_AVAILABLE(10_10, 8_0);
-
-
-/*! @class AVAudioEnvironmentDistanceAttenuationParameters
-    @abstract Parameters specifying the amount of distance attenuation
-    @discussion
-        A standalone instance of AVAudioEnvironmentDistanceAttenuationParameters cannot be created. 
-        Only an instance vended out by a source object (e.g. AVAudioEnvironmentNode) can be used.
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioEnvironmentDistanceAttenuationParameters : NSObject {
-@private
-	void *_impl;
-}
-
-/*! @property distanceAttenuationModel
-    @abstract Type of distance attenuation model
-    @discussion
-        Default:    AVAudioEnvironmentDistanceAttenuationModelInverse
-*/
-@property (nonatomic) AVAudioEnvironmentDistanceAttenuationModel distanceAttenuationModel;
-
-/*! @property referenceDistance
-    @abstract The minimum distance at which attenuation is applied
-    @discussion
-        Default:    1.0 meter
-        Models:     AVAudioEnvironmentDistanceAttenuationModelInverse,
-                    AVAudioEnvironmentDistanceAttenuationModelLinear
-*/
-@property (nonatomic) float referenceDistance;
-
-/*! @property maximumDistance
-    @abstract The distance beyond which no further attenuation is applied
-    @discussion
-        Default:    100000.0 meters
-        Models:     AVAudioEnvironmentDistanceAttenuationModelLinear
-*/
-@property (nonatomic) float maximumDistance;
-
-/*! @property rolloffFactor
-    @abstract Determines the attenuation curve
-    @discussion
-        A higher value results in a steeper attenuation curve.
-        The rolloff factor should be a value greater than 0.
-        Default:    1.0
-        Models:     AVAudioEnvironmentDistanceAttenuationModelExponential
-                    AVAudioEnvironmentDistanceAttenuationModelInverse
-                    AVAudioEnvironmentDistanceAttenuationModelLinear
-*/
-@property (nonatomic) float rolloffFactor;
-
-@end
-
-
-/*! @class AVAudioEnvironmentReverbParameters
-    @abstract Parameters used to control the reverb in AVAudioEnvironmentNode
-    @discussion
-        Reverberation can be used to simulate the acoustic characteristics of an environment.
-        AVAudioEnvironmentNode has a built in reverb that describes the space that the listener 
-        is in.
- 
-        The reverb also has a single filter that sits at the end of the chain. This filter is useful 
-        to shape the overall sound of the reverb. For instance, one of the reverb presets can be 
-        selected to simulate the general space and then the filter can be used to brighten or darken 
-        the overall sound.
- 
-        A standalone instance of AVAudioEnvironmentReverbParameters cannot be created.
-        Only an instance vended out by a source object (e.g. AVAudioEnvironmentNode) can be used.
-*/
-
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioEnvironmentReverbParameters : NSObject {
-@private
-	void *_impl;
-}
-
-/*! @property enable
-    @abstract Turns on/off the reverb
-    @discussion
-        Default:    NO
-*/
-@property (nonatomic) BOOL enable;
-
-/*! @property level
-    @abstract Controls the master level of the reverb
-    @discussion
-        Range:      -40 to 40 dB
-        Default:    0.0
-*/
-@property (nonatomic) float level;
-
-/*! @property filterParameters
-    @abstract filter that applies to the output of the reverb
-*/
-@property (nonatomic, readonly) AVAudioUnitEQFilterParameters *filterParameters;
-
-/*! @method loadFactoryReverbPreset:
-    @abstract Load one of the reverb's factory presets
-    @param preset
-        Reverb preset to be set.
-    @discussion
-        Loading a factory reverb preset changes the sound of the reverb. This works independently
-        of the filter which follows the reverb in the signal chain.
-*/
-- (void)loadFactoryReverbPreset:(AVAudioUnitReverbPreset)preset;
-
-@end
-
-
-/*!
-    @class AVAudioEnvironmentNode
-    @abstract Mixer node that simulates a 3D environment
-    @discussion
-        AVAudioEnvironmentNode is a mixer node that simulates a 3D audio environment. Any node that 
-        conforms to the AVAudioMixing protocol (e.g. AVAudioPlayerNode) can act as a source in this
-        environment.
- 
-        The environment has an implicit "listener". By controlling the listener's position and
-        orientation, the application controls the way the user experiences the virtual world. 
-        In addition, this node also defines properties for distance attenuation and reverberation 
-        that help characterize the environment.
- 
-        It is important to note that only inputs with a mono channel connection format to the 
-        environment node are spatialized. If the input is stereo, the audio is passed through 
-        without being spatialized. Currently inputs with connection formats of more than 2 channels 
-        are not supported.
- 
-        In order to set the environment node’s output to a multichannel format, use an AVAudioFormat 
-        having one of the following AudioChannelLayoutTags.
- 
-        kAudioChannelLayoutTag_AudioUnit_4
-        kAudioChannelLayoutTag_AudioUnit_5_0;
-        kAudioChannelLayoutTag_AudioUnit_6_0;
-        kAudioChannelLayoutTag_AudioUnit_7_0;
-        kAudioChannelLayoutTag_AudioUnit_7_0_Front;
-        kAudioChannelLayoutTag_AudioUnit_8;
-*/
-
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioEnvironmentNode : AVAudioNode <AVAudioMixing>
-
-/*! @property outputVolume
-	@abstract The mixer's output volume.
-	@discussion
-        This accesses the mixer's output volume (0.0-1.0, inclusive).
-*/
-@property (nonatomic) float outputVolume;
-
-/*! @property nextAvailableInputBus
-    @abstract Find an unused input bus
-    @discussion
-        This will find and return the first input bus to which no other node is connected.
-*/
-@property (nonatomic, readonly) AVAudioNodeBus nextAvailableInputBus;
-
-/*! @property listenerPosition
-    @abstract Sets the listener's position in the 3D environment
-    @discussion
-        The coordinates are specified in meters.
-        Default:
-            The default poistion of the listener is at the origin.
-            x: 0.0
-            y: 0.0
-            z: 0.0
-*/
-@property (nonatomic) AVAudio3DPoint listenerPosition;
-
-/*! @property listenerVectorOrientation
-    @abstract The listener's orientation in the environment
-    @discussion
-    Changing listenerVectorOrientation will result in a corresponding change in listenerAngularOrientation.
-        Default:
-            The default orientation is with the listener looking directly along the negative Z axis.
-            forward: (0, 0, -1)
-            up:      (0, 1, 0)
-*/
-@property (nonatomic) AVAudio3DVectorOrientation listenerVectorOrientation;
-
-/*! @property listenerAngularOrientation
-    @abstract The listener's orientation in the environment
-    @discussion
-    Changing listenerAngularOrientation will result in a corresponding change in listenerVectorOrientation.
-        All angles are specified in degrees.
-        Default:
-            The default orientation is with the listener looking directly along the negative Z axis.
-            yaw: 0.0
-            pitch: 0.0
-            roll: 0.0
-*/
-@property (nonatomic) AVAudio3DAngularOrientation listenerAngularOrientation;
-
-/*! @property distanceAttenuationParameters
-    @abstract The distance attenuation parameters for the environment
-*/
-@property (nonatomic, readonly) AVAudioEnvironmentDistanceAttenuationParameters *distanceAttenuationParameters;
-
-/*! @property reverbParameters
-    @abstract The reverb parameters for the environment
-*/
-@property (nonatomic, readonly) AVAudioEnvironmentReverbParameters *reverbParameters;
-
-/*! @property applicableRenderingAlgorithms
-    @abstract Returns an array of AVAudio3DMixingRenderingAlgorithm values based on the current output format
-    @discussion
-        AVAudioEnvironmentNode supports several rendering algorithms per input bus which are defined 
-        in <AVFoundation/AVAudioMixing.h>.
- 
-        Depending on the current output format of the environment node, this method returns 
-        an immutable array of the applicable rendering algorithms. This is important when the
-        environment node has been configured to a multichannel output format because only a subset
-        of the available rendering algorithms are designed to render to all of the channels.
-        
-        This information should be retrieved after a successful connection to the destination node 
-        via the engine's connect method.
-*/
-@property (nonatomic, readonly) NSArray<NSNumber *> *applicableRenderingAlgorithms;
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioFile.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioFile.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioFile.h	2015-09-30 23:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioFile.h	2016-05-25 07:19:41.000000000 +0200
@@ -1,167 +1,9 @@
 /*
-	File:		AVAudioFile.h
-	Framework:	AVFoundation
+	File:           AVAudioFile.h
+	Framework:      AVFoundation
 	
-	Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioTypes.h>
-#import <AVFoundation/AVAudioFormat.h>
+#import <AVFAudio/AVAudioFile.h>
 
-NS_ASSUME_NONNULL_BEGIN
-
-@class NSURL;
-@class AVAudioPCMBuffer;
-
-/*!
-	@class AVAudioFile
-	@abstract
-		AVAudioFile represents an audio file opened for reading or writing.
-	@discussion
-		Regardless of the file's actual format, reading and writing the file is done via 
-		`AVAudioPCMBuffer` objects, containing samples in an `AVAudioCommonFormat`,
-		referred to as the file's "processing format." Conversions are performed to and from
-		the file's actual format.
-		
-		Reads and writes are always sequential, but random access is possible by setting the
-		framePosition property.
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioFile : NSObject {
-@private
-	void *_impl;
-}
-/*! @method initForReading:error:
-	@abstract Open a file for reading.
-	@param fileURL
-		the file to open
-	@param outError
-		on exit, if an error occurs, a description of the error
-	@discussion
-		This opens the file for reading using the standard format (deinterleaved floating point).
-*/
-- (nullable instancetype)initForReading:(NSURL *)fileURL error:(NSError **)outError;
-
-/*!	@method initForReading:commonFormat:interleaved:error:
-	@abstract Open a file for reading, using a specified processing format.
-	@param fileURL
-		the file to open
-	@param format
-		the processing format to use when reading from the file
-	@param interleaved
-		whether to use an interleaved processing format
-	@param outError
-		on exit, if an error occurs, a description of the error
-*/
-- (nullable instancetype)initForReading:(NSURL *)fileURL commonFormat:(AVAudioCommonFormat)format interleaved:(BOOL)interleaved error:(NSError **)outError;
-
-/*! @method initForWriting:settings:error:
-	@abstract Open a file for writing.
-	@param fileURL
-		the path at which to create the file
-	@param settings
-		the format of the file to create (See `AVAudioRecorder`.)
-	@param outError
-		on exit, if an error occurs, a description of the error
-	@discussion
-		The file type to create is inferred from the file extension. Will overwrite a file at the
-		specified URL if a file exists.
-
-		This opens the file for writing using the standard format (deinterleaved floating point).
-*/
-- (nullable instancetype)initForWriting:(NSURL *)fileURL settings:(NSDictionary<NSString *, id> *)settings error:(NSError **)outError;
-
-/*! @method initForWriting:settings:commonFormat:interleaved:error:
-	@abstract Open a file for writing.
-	@param fileURL
-		the path at which to create the file
-	@param settings
-		the format of the file to create (See `AVAudioRecorder`.)
-	@param format
-		the processing format to use when writing to the file
-	@param interleaved
-		whether to use an interleaved processing format
-	@param outError
-		on exit, if an error occurs, a description of the error
-	@discussion
-		The file type to create is inferred from the file extension. Will overwrite a file at the
-		specified URL if a file exists.
-*/
-- (nullable instancetype)initForWriting:(NSURL *)fileURL settings:(NSDictionary<NSString *, id> *)settings commonFormat:(AVAudioCommonFormat)format interleaved:(BOOL)interleaved error:(NSError **)outError;
-
-/*! @method readIntoBuffer:error:
-	@abstract Read an entire buffer.
-	@param buffer
-		The buffer into which to read from the file. Its format must match the file's
-		processing format.
-	@param outError
-		on exit, if an error occurs, a description of the error
-	@return
-		YES for success.
-	@discussion
-		Reading sequentially from framePosition, attempts to fill the buffer to its capacity. On
-		return, the buffer's length indicates the number of sample frames successfully read.
-*/
-- (BOOL)readIntoBuffer:(AVAudioPCMBuffer *)buffer error:(NSError **)outError;
-
-/*! @method readIntoBuffer:frameCount:error:
-	@abstract Read a portion of a buffer.
-	@param frames
-		The number of frames to read.
-	@param buffer
-		The buffer into which to read from the file. Its format must match the file's
-		processing format.
-	@param outError
-		on exit, if an error occurs, a description of the error
-	@return
-		YES for success.
-	@discussion
-		Like `readIntoBuffer:error:`, but can be used to read fewer frames than buffer.frameCapacity.
-*/
-- (BOOL)readIntoBuffer:(AVAudioPCMBuffer *)buffer frameCount:(AVAudioFrameCount)frames error:(NSError **)outError;
-
-/*! @method writeFromBuffer:error:
-	@abstract Write a buffer.
-	@param buffer
-		The buffer from which to write to the file. Its format must match the file's
-		processing format.
-	@param outError
-		on exit, if an error occurs, a description of the error
-	@return
-		YES for success.
-	@discussion
-		Writes sequentially. The buffer's frameLength signifies how much of the buffer is to be written.
-*/
-- (BOOL)writeFromBuffer:(const AVAudioPCMBuffer *)buffer error:(NSError **)outError;
-
-/*!	@property url
-	@abstract The URL the file is reading or writing.
-*/
-@property (nonatomic, readonly) NSURL *url;
-
-/*! @property fileFormat
-	@abstract The on-disk format of the file.
-*/
-@property (nonatomic, readonly) AVAudioFormat *fileFormat;
-
-/*! @property processingFormat
-	@abstract The processing format of the file.
-*/
-@property (nonatomic, readonly) AVAudioFormat *processingFormat;
-
-/*! @property length
-	@abstract The number of sample frames in the file.
-	@discussion
-		 Note: this can be expensive to compute for the first time.
-*/
-@property (nonatomic, readonly) AVAudioFramePosition length;
-
-/*! @property framePosition
-	@abstract The position in the file at which the next read or write will occur.
-	@discussion
-		Set framePosition to perform a seek before a read or write. A read or write operation advances the frame position by the number of frames read or written.
-*/
-@property (nonatomic) AVAudioFramePosition framePosition;
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioFormat.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioFormat.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioFormat.h	2015-09-30 23:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioFormat.h	2016-05-25 07:19:41.000000000 +0200
@@ -1,209 +1,9 @@
 /*
-	File:		AVAudioFormat.h
-	Framework:	AVFoundation
+	File:           AVAudioFormat.h
+	Framework:      AVFoundation
 	
-	Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioTypes.h>
-#import <AVFoundation/AVAudioChannelLayout.h>
-#import <CoreMedia/CMFormatDescription.h>
+#import <AVFAudio/AVAudioFormat.h>
 
-NS_ASSUME_NONNULL_BEGIN
-
-/*!	
-	@enum		AVAudioCommonFormat
-	@constant	AVAudioOtherFormat
-					A format other than one of the common ones below.
-	@constant	AVAudioPCMFormatFloat32
-					Native-endian floats (this is the standard format).
-	@constant	AVAudioPCMFormatFloat64
-					Native-endian doubles.
-	@constant	AVAudioPCMFormatInt16
-					Signed 16-bit native-endian integers.
-	@constant	AVAudioPCMFormatInt32
-					Signed 32-bit native-endian integers.
-*/
-typedef NS_ENUM(NSUInteger, AVAudioCommonFormat) {
-	AVAudioOtherFormat = 0,
-	AVAudioPCMFormatFloat32 = 1,
-	AVAudioPCMFormatFloat64 = 2,
-	AVAudioPCMFormatInt16 = 3,
-	AVAudioPCMFormatInt32 = 4
-} NS_ENUM_AVAILABLE(10_10, 8_0);
-
-
-/*! @class AVAudioFormat
-	@abstract A representation of an audio format.
-	@discussion
-		AVAudioFormat wraps a Core Audio AudioStreamBasicDescription struct, with convenience
-		initializers and accessors for common formats, including Core Audio's standard deinterleaved
-		32-bit floating point.
-	
-		Instances of this class are immutable.
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioFormat : NSObject <NSSecureCoding> {
-@private
-	AudioStreamBasicDescription _asbd;
-	AVAudioChannelLayout *_layout;
-	AVAudioCommonFormat _commonFormat;
-	void * _reserved;
-}
-
-
-/*! @method initWithStreamDescription:
-	@abstract Initialize from an AudioStreamBasicDescription.
-	@param asbd
-		the AudioStreamBasicDescription
-	@discussion
-		If the format specifies more than 2 channels, this method fails (returns nil).
-*/
-- (instancetype)initWithStreamDescription:(const AudioStreamBasicDescription *)asbd;
-
-/*! @method initWithStreamDescription:channelLayout:
-	@abstract Initialize from an AudioStreamBasicDescription and optional channel layout.
-	@param asbd
-		the AudioStreamBasicDescription
-	@param layout
-		the channel layout. Can be nil only if asbd specifies 1 or 2 channels.
-	@discussion
-		If the format specifies more than 2 channels, this method fails (returns nil) unless layout
-		is non-nil.
-*/
-- (instancetype)initWithStreamDescription:(const AudioStreamBasicDescription *)asbd channelLayout:(AVAudioChannelLayout * __nullable)layout;
-
-/*! @method initStandardFormatWithSampleRate:channels:
-	@abstract Initialize to deinterleaved float with the specified sample rate and channel count.
-	@param sampleRate
-		the sample rate
-	@param channels
-		the channel count
-	@discussion
-		If the format specifies more than 2 channels, this method fails (returns nil).
-*/
-- (instancetype)initStandardFormatWithSampleRate:(double)sampleRate channels:(AVAudioChannelCount)channels;
-
-/*! @method initStandardFormatWithSampleRate:channelLayout:
-	@abstract Initialize to deinterleaved float with the specified sample rate and channel layout.
-	@param sampleRate
-		the sample rate
-	@param layout
-		the channel layout. must not be nil.
-*/
-- (instancetype)initStandardFormatWithSampleRate:(double)sampleRate channelLayout:(AVAudioChannelLayout *)layout;
-
-/*! @method initWithCommonFormat:sampleRate:channels:interleaved:
-	@abstract Initialize to float with the specified sample rate, channel count and interleavedness.
-	@param format
-		the common format type
-	@param sampleRate
-		the sample rate
-	@param channels
-		the channel count
-	@param interleaved
-		true if interleaved
-	@discussion
-		If the format specifies more than 2 channels, this method fails (returns nil).
-*/
-- (instancetype)initWithCommonFormat:(AVAudioCommonFormat)format sampleRate:(double)sampleRate channels:(AVAudioChannelCount)channels interleaved:(BOOL)interleaved;
-
-/*! @method initWithCommonFormat:sampleRate:interleaved:channelLayout:
-	@abstract Initialize to float with the specified sample rate, channel layout and interleavedness.
-	@param format
-		the common format type
-	@param sampleRate
-		the sample rate
-	@param interleaved
-		true if interleaved
-	@param layout
-		the channel layout. must not be nil.
-*/
-- (instancetype)initWithCommonFormat:(AVAudioCommonFormat)format sampleRate:(double)sampleRate interleaved:(BOOL)interleaved channelLayout:(AVAudioChannelLayout *)layout;
-
-/*! @method initWithSettings:
-	@abstract Initialize using a settings dictionary.
-	@discussion
-		See AVAudioSettings.h. Note that many settings dictionary elements pertain to encoder
-		settings, not the basic format, and will be ignored.
-*/
-- (instancetype)initWithSettings:(NSDictionary<NSString *, id> *)settings;
-
-/*!
- 	@method initWithCMAudioFormatDescription:
- 	@abstract initialize from a CMAudioFormatDescriptionRef.
- 	@param formatDescription
- 		the CMAudioFormatDescriptionRef.
- 	@discussion
- 		If formatDescription is invalid, this method fails (returns nil).
- */
-- (instancetype)initWithCMAudioFormatDescription:(CMAudioFormatDescriptionRef)formatDescription NS_AVAILABLE(10_11, 9_0);
-
-
-/*!	@method isEqual:
-	@abstract Determine whether another format is functionally equivalent.
-	@param object
-		the format to compare against
-	@discussion
-		For PCM, interleavedness is ignored for mono. Differences in the AudioStreamBasicDescription
-		alignment and packedness are ignored when they are not significant (e.g. with 1 channel, 2
-		bytes per frame and 16 bits per channel, neither alignment, the format is implicitly packed
-		and can be interpreted as either high- or low-aligned.)
-		For AVAudioChannelLayout, a layout with standard mono/stereo tag is considered to be 
-		equivalent to a nil layout. Otherwise, the layouts are compared for equality.
-*/
-- (BOOL)isEqual:(id)object;
-
-/*!	@property standard
-	@abstract Describes whether the format is deinterleaved native-endian float.
-*/
-@property (nonatomic, readonly, getter=isStandard) BOOL standard;
-
-/*!	@property commonFormat
-	@abstract An `AVAudioCommonFormat` identifying the format
-*/
-@property (nonatomic, readonly) AVAudioCommonFormat commonFormat;
-
-/*! @property channelCount
-	@abstract The number of channels of audio data.
-*/
-@property (nonatomic, readonly) AVAudioChannelCount channelCount;
-
-/*! @property sampleRate
-	@abstract A sampling rate in Hertz.
-*/
-@property (nonatomic, readonly) double sampleRate;
-
-/*!	@property interleaved
-	@abstract Describes whether the samples are interleaved.
-	@discussion
-		For non-PCM formats, the value is undefined.
-*/
-@property (nonatomic, readonly, getter=isInterleaved) BOOL interleaved;
-
-/*!	@property streamDescription
-	@abstract Returns the AudioStreamBasicDescription, for use with lower-level audio API's.
-*/
-@property (nonatomic, readonly) const AudioStreamBasicDescription *streamDescription;
-
-/*!	@property channelLayout
-	@abstract The underlying AVAudioChannelLayout, if any.
-	@discussion
-		Only formats with more than 2 channels are required to have channel layouts.
-*/
-@property (nonatomic, readonly, nullable) const AVAudioChannelLayout *channelLayout;
-
-/*!	@property settings
-	@abstract Returns the format represented as a dictionary with keys from AVAudioSettings.h.
-*/
-@property (nonatomic, readonly) NSDictionary<NSString *, id> *settings;
-
-/*!
-	 @property formatDescription
-	 @abstract Converts to a CMAudioFormatDescriptionRef, for use with Core Media API's.
- */
-@property (nonatomic, readonly) CMAudioFormatDescriptionRef formatDescription NS_AVAILABLE(10_11, 9_0);
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioIONode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioIONode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioIONode.h	2015-09-30 23:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioIONode.h	2016-05-25 07:19:41.000000000 +0200
@@ -1,62 +1,9 @@
 /*
-	File:		AVAudioIONode.h
-	Framework:	AVFoundation
+	File:           AVAudioIONode.h
+	Framework:      AVFoundation
 	
-	Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioNode.h>
-#import <AVFoundation/AVAudioMixing.h>
-#import <AudioUnit/AudioUnit.h>
+#import <AVFAudio/AVAudioIONode.h>
 
-/*!	@class AVAudioIONode
-	@abstract Base class for a node that connects to the system's audio input or output.
-	@discussion
-		On OS X, AVAudioInputNode and AVAudioOutputNode communicate with the system's default
-		input and output devices. On iOS, they communicate with the devices appropriate to
-		the app's AVAudioSession category and other configuration, also considering the user's
-		actions such as connecting/disconnecting external devices.
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioIONode : AVAudioNode
-
-/*!	@property presentationLatency
-	@abstract The presentation, or hardware, latency.
-	@discussion
-		This corresponds to kAudioDevicePropertyLatency and kAudioStreamPropertyLatency.
-		See <CoreAudio/AudioHardwareBase.h>.
-*/
-@property (nonatomic, readonly) NSTimeInterval presentationLatency;
-
-/*!	@property audioUnit
-	@abstract The node's underlying AudioUnit, if any.
-	@discussion
-		This is only necessary for certain advanced usages.
-*/
-@property (nonatomic, readonly, nullable) AudioUnit audioUnit;
-@end
-
-
-/*! @class AVAudioInputNode
-	@abstract A node that connects to the system's audio input.
-	@discussion
-		This node has one element. The format of the input scope reflects the audio hardware sample
-		rate and channel count. The format of the output scope is initially the same as that of the
-		input, but you may set it to a different format, in which case the node will convert.
-*/
-
-
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioInputNode : AVAudioIONode <AVAudioMixing>
-@end
-
-/*! @class AVAudioOutputNode
-	@abstract A node that connects to the system's audio input.
-	@discussion
-		This node has one element. The format of the output scope reflects the audio hardware sample
-		rate and channel count. The format of the input scope is initially the same as that of the
-		output, but you may set it to a different format, in which case the node will convert.
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioOutputNode : AVAudioIONode
-@end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioMixerNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioMixerNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioMixerNode.h	2015-09-30 23:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioMixerNode.h	2016-05-25 07:19:42.000000000 +0200
@@ -1,41 +1,9 @@
 /*
-	File:		AVAudioMixerNode.h
-	Framework:	AVFoundation
+	File:           AVAudioMixerNode.h
+	Framework:      AVFoundation
 	
-	Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioNode.h>
-#import <AVFoundation/AVAudioMixing.h>
+#import <AVFAudio/AVAudioMixerNode.h>
 
-NS_ASSUME_NONNULL_BEGIN
-
-/*! @class AVAudioMixerNode
-	@abstract A node that mixes its inputs to a single output.
-	@discussion
-		Mixers may have any number of inputs.
-	
-		The mixer accepts input at any sample rate and efficiently combines sample rate
-		conversions. It also accepts any channel count and will correctly upmix or downmix
-		to the output channel count.
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioMixerNode : AVAudioNode <AVAudioMixing>
-
-/*! @property outputVolume
-	@abstract The mixer's output volume.
-	@discussion
-		This accesses the mixer's output volume (0.0-1.0, inclusive).
-*/
-@property (nonatomic) float outputVolume;
-
-/*! @property nextAvailableInputBus
-	@abstract Find an unused input bus.
-	@discussion
-		This will find and return the first input bus to which no other node is connected.
-*/
-@property (nonatomic, readonly) AVAudioNodeBus nextAvailableInputBus;
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioMixing.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioMixing.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioMixing.h	2015-09-30 23:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioMixing.h	2016-05-25 07:19:42.000000000 +0200
@@ -1,245 +1,9 @@
 /*
-    File:       AVAudioMixing.h
-    Framework:	AVFoundation
- 
-    Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	File:           AVAudioMixing.h
+	Framework:      AVFoundation
+	
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioTypes.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-@class AVAudioNode, AVAudioConnectionPoint, AVAudioMixingDestination;
-@protocol AVAudioStereoMixing;
-@protocol AVAudio3DMixing;
-
-/*! @protocol   AVAudioMixing
-    @abstract   Protocol that defines properties applicable to the input bus of a mixer
-                node
-    @discussion
-        Nodes that conforms to the AVAudioMixing protocol can talk to a mixer node downstream,
-        specifically of type AVAudioMixerNode or AVAudioEnvironmentNode. The properties defined 
-        by this protocol apply to the respective input bus of the mixer node that the source node is 
-        connected to. Note that effect nodes cannot talk to their downstream mixer.
-
-		Properties can be set either on the source node, or directly on individual mixer connections.
-		Source node properties are:
-		- applied to all existing mixer connections when set
-		- applied to new mixer connections
-		- preserved upon disconnection from mixers
-		- not affected by connections/disconnections to/from mixers
-		- not affected by any direct changes to properties on individual mixer connections
-
-		Individual mixer connection properties, when set, will override any values previously derived 
-		from the corresponding source node properties. However, if a source node property is 
-		subsequently set, it will override the corresponding property value of all individual mixer 
-		connections.
-		Unlike source node properties, individual mixer connection properties are not preserved upon
-		disconnection (see `AVAudioMixing(destinationForMixer:bus:)` and `AVAudioMixingDestination`).
-
-		Source nodes that are connected to a mixer downstream can be disconnected from
-		one mixer and connected to another mixer with source node's mixing settings intact.
-		For example, an AVAudioPlayerNode that is being used in a gaming scenario can set up its 
-		3D mixing settings and then move from one environment to another.
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@protocol AVAudioMixing <AVAudioStereoMixing, AVAudio3DMixing>
-
-/*! @method destinationForMixer:bus:
-	@abstract Returns the AVAudioMixingDestination object corresponding to specified mixer node and
-		its input bus
-	@discussion
-		When a source node is connected to multiple mixers downstream, setting AVAudioMixing 
-		properties directly on the source node will apply the change to all the mixers downstream. 
-		If you want to set/get properties on a specific mixer, use this method to get the 
-		corresponding AVAudioMixingDestination and set/get properties on it. 
- 
-		Note:
-		- Properties set on individual AVAudioMixingDestination instances will not reflect at the
-			source node level.
-
-		- AVAudioMixingDestination reference returned by this method could become invalid when
-			there is any disconnection between the source and the mixer node. Hence this reference
-			should not be retained and should be fetched every time you want to set/get properties 
-			on a specific mixer.
- 
-		If the source node is not connected to the specified mixer/input bus, this method
-		returns nil.
-		Calling this on an AVAudioMixingDestination instance returns self if the specified
-		mixer/input bus match its connection point, otherwise returns nil.
-*/
-- (nullable AVAudioMixingDestination *)destinationForMixer:(AVAudioNode *)mixer bus:(AVAudioNodeBus)bus NS_AVAILABLE(10_11, 9_0);
-
-/*! @property volume
-    @abstract Set a bus's input volume
-    @discussion
-        Range:      0.0 -> 1.0
-        Default:    1.0
-        Mixers:     AVAudioMixerNode, AVAudioEnvironmentNode
-*/
-@property (nonatomic) float volume;
-
-@end
-
-
-/*! @protocol   AVAudioStereoMixing
-    @abstract   Protocol that defines stereo mixing properties
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@protocol AVAudioStereoMixing <NSObject>
-
-/*! @property pan
-    @abstract Set a bus's stereo pan
-    @discussion
-        Range:      -1.0 -> 1.0
-        Default:    0.0
-        Mixer:      AVAudioMixerNode
-*/
-@property (nonatomic) float pan;
-
-@end
-
-
-/*! @enum AVAudio3DMixingRenderingAlgorithm
-    @abstract   Types of rendering algorithms available per input bus of the environment node
-    @discussion
-        The rendering algorithms differ in terms of quality and cpu cost. 
-        AVAudio3DMixingRenderingAlgorithmEqualPowerPanning is the simplest panning algorithm and also 
-        the least expensive computationally.
- 
-        With the exception of AVAudio3DMixingRenderingAlgorithmSoundField, while the mixer is
-        rendering to multi channel hardware, audio data will only be rendered to channels 1 & 2.
- 
-        AVAudio3DMixingRenderingAlgorithmEqualPowerPanning
-            EqualPowerPanning merely pans the data of the mixer bus into a stereo field. This 
-            algorithm is analogous to the pan knob found on a mixing board channel strip. 
- 
-        AVAudio3DMixingRenderingAlgorithmSphericalHead
-            SphericalHead is designed to emulate 3 dimensional space in headphones by simulating 
-            inter-aural time delays and other spatial cues. SphericalHead is slightly less CPU 
-            intensive than the HRTF algorithm.
- 
-        AVAudio3DMixingRenderingAlgorithmHRTF
-            HRTF (Head Related Transfer Function) is a high quality algorithm using filtering to 
-            emulate 3 dimensional space in headphones. HRTF is a cpu intensive algorithm.
- 
-        AVAudio3DMixingRenderingAlgorithmSoundField
-            SoundField is designed for rendering to multi channel hardware. The mixer takes data 
-            being rendered with SoundField and distributes it amongst all the output channels with 
-            a weighting toward the location in which the sound derives. It is very effective for 
-            ambient sounds, which may derive from a specific location in space, yet should be heard 
-            through the listener's entire space.
- 
-        AVAudio3DMixingRenderingAlgorithmStereoPassThrough
-            StereoPassThrough should be used when no localization is desired for the source data. 
-            Setting this algorithm tells the mixer to take mono/stereo input and pass it directly to 
-            channels 1 & 2 without localization.
- 
-*/
-typedef NS_ENUM(NSInteger, AVAudio3DMixingRenderingAlgorithm) {
-    AVAudio3DMixingRenderingAlgorithmEqualPowerPanning      = 0,
-    AVAudio3DMixingRenderingAlgorithmSphericalHead          = 1,
-    AVAudio3DMixingRenderingAlgorithmHRTF                   = 2,
-    AVAudio3DMixingRenderingAlgorithmSoundField             = 3,
-    AVAudio3DMixingRenderingAlgorithmStereoPassThrough      = 5
-} NS_ENUM_AVAILABLE(10_10, 8_0);
-
-
-/*! @protocol   AVAudio3DMixing
-    @abstract   Protocol that defines 3D mixing properties
-*/
-@protocol AVAudio3DMixing <NSObject>
-
-/*! @property renderingAlgorithm
-    @abstract Type of rendering algorithm used
-    @discussion
-        Depending on the current output format of the AVAudioEnvironmentNode, only a subset of the 
-        rendering algorithms may be supported. An array of valid rendering algorithms can be 
-        retrieved by calling applicableRenderingAlgorithms on AVAudioEnvironmentNode.
- 
-        Default:    AVAudio3DMixingRenderingAlgorithmEqualPowerPanning
-        Mixer:      AVAudioEnvironmentNode
-*/
-@property (nonatomic) AVAudio3DMixingRenderingAlgorithm renderingAlgorithm;
-
-/*! @property rate
-    @abstract Changes the playback rate of the input signal
-    @discussion
-        A value of 2.0 results in the output audio playing one octave higher.
-        A value of 0.5, results in the output audio playing one octave lower.
-     
-        Range:      0.5 -> 2.0
-        Default:    1.0
-        Mixer:      AVAudioEnvironmentNode
-*/
-@property (nonatomic) float rate;
-
-/*! @property reverbBlend
-    @abstract Controls the blend of dry and reverb processed audio
-    @discussion
-        This property controls the amount of the source's audio that will be processed by the reverb 
-        in AVAudioEnvironmentNode. A value of 0.5 will result in an equal blend of dry and processed 
-        (wet) audio.
- 
-        Range:      0.0 (completely dry) -> 1.0 (completely wet)
-        Default:    0.0
-        Mixer:      AVAudioEnvironmentNode
-*/
-@property (nonatomic) float reverbBlend;
-
-/*! @property obstruction
-    @abstract Simulates filtering of the direct path of sound due to an obstacle
-    @discussion
-        Only the direct path of sound between the source and listener is blocked.
- 
-        Range:      -100.0 -> 0.0 dB
-        Default:    0.0
-        Mixer:      AVAudioEnvironmentNode
-*/
-@property (nonatomic) float obstruction;
-
-/*! @property occlusion
-    @abstract Simulates filtering of the direct and reverb paths of sound due to an obstacle
-    @discussion
-        Both the direct and reverb paths of sound between the source and listener are blocked.
- 
-        Range:      -100.0 -> 0.0 dB
-        Default:    0.0
-        Mixer:      AVAudioEnvironmentNode
-*/
-@property (nonatomic) float occlusion;
-
-/*! @property position
-    @abstract The location of the source in the 3D environment
-    @discussion
-        The coordinates are specified in meters.
- 
-        Mixer:      AVAudioEnvironmentNode
-*/
-@property (nonatomic) AVAudio3DPoint position;
-
-@end
-
-/*! @class AVAudioMixingDestination
-	@abstract An object representing a connection to a mixer node from a node that
-		conforms to AVAudioMixing protocol
-	@discussion
-		A standalone instance of AVAudioMixingDestination cannot be created.
-		Only an instance vended by a source node (e.g. AVAudioPlayerNode) can be used
-		(see `AVAudioMixing`).
-*/
-NS_CLASS_AVAILABLE(10_11, 9_0)
-@interface AVAudioMixingDestination : NSObject <AVAudioMixing> {
-@private
-	void *_impl;
-}
-
-/*! @property connectionPoint
-	@abstract Returns the underlying mixer connection point
-*/
-@property (nonatomic, readonly) AVAudioConnectionPoint *connectionPoint;
-
-@end
-
-NS_ASSUME_NONNULL_END
+#import <AVFAudio/AVAudioMixing.h>
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioNode.h	2015-09-30 23:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioNode.h	2016-05-25 07:19:42.000000000 +0200
@@ -1,140 +1,9 @@
 /*
-	File:		AVAudioNode.h
-	Framework:	AVFoundation
+	File:           AVAudioNode.h
+	Framework:      AVFoundation
 	
-	Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioTypes.h>
+#import <AVFAudio/AVAudioNode.h>
 
-NS_ASSUME_NONNULL_BEGIN
-
-@class AVAudioEngine, AVAudioFormat, AVAudioInputNode, AVAudioMixerNode, AVAudioOutputNode, AVAudioPCMBuffer, AVAudioTime;
-
-/*!	@typedef AVAudioNodeTapBlock
-	@abstract A block that receives copies of the output of an AVAudioNode.
-	@param buffer
-		a buffer of audio captured from the output of an AVAudioNode
-	@param when
-		the time at which the buffer was captured
-	@discussion
-		CAUTION: This callback may be invoked on a thread other than the main thread.
-*/
-typedef void (^AVAudioNodeTapBlock)(AVAudioPCMBuffer *buffer, AVAudioTime *when);
-
-/*!
-	@class AVAudioNode
-	@abstract Base class for an audio generation, processing, or I/O block.
-	@discussion
-		`AVAudioEngine` objects contain instances of various AVAudioNode subclasses. This
-		base class provides certain common functionality.
-		
-		Nodes have input and output busses, which can be thought of as connection points.
-		For example, an effect typically has one input bus and one output bus. A mixer
-		typically has multiple input busses and one output bus.
-		
-		Busses have formats, expressed in terms of sample rate and channel count. When making
-		connections between nodes, often the format must match exactly. There are exceptions
-		(e.g. `AVAudioMixerNode` and `AVAudioOutputNode`).
-
-		Nodes do not currently provide useful functionality until attached to an engine.
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioNode : NSObject {
-@protected
-	void *_impl;
-}
-/*! @method reset
-	@abstract Clear a unit's previous processing state.
-*/
-- (void)reset;
-
-/*! @method inputFormatForBus:
-	@abstract Obtain an input bus's format.
-*/
-- (AVAudioFormat *)inputFormatForBus:(AVAudioNodeBus)bus;
-
-/*! @method outputFormatForBus:
-	@abstract Obtain an output bus's format.
-*/
-- (AVAudioFormat *)outputFormatForBus:(AVAudioNodeBus)bus;
-
-/*!	@method nameForInputBus:
-	@abstract Return the name of an input bus.
-*/
-- (NSString *)nameForInputBus:(AVAudioNodeBus)bus;
-
-/*!	@method nameForOutputBus:
-	@abstract Return the name of an output bus.
-*/
-- (NSString *)nameForOutputBus:(AVAudioNodeBus)bus;
-
-/*! @method installTapOnBus:bufferSize:format:block:
-	@abstract Create a "tap" to record/monitor/observe the output of the node.
-	@param bus
-		the node output bus to which to attach the tap
-	@param bufferSize
-		the requested size of the incoming buffers. The implementation may choose another size.
-	@param format
-		If non-nil, attempts to apply this as the format of the specified output bus. This should
-		only be done when attaching to an output bus which is not connected to another node; an
-		error will result otherwise.
-		The tap and connection formats (if non-nil) on the specified bus should be identical. 
-		Otherwise, the latter operation will override any previously set format.
-		Note that for AVAudioOutputNode, tap format must be specified as nil.
-	@param tapBlock
-		a block to be called with audio buffers
-	
-	@discussion
-		Only one tap may be installed on any bus. Taps may be safely installed and removed while
-		the engine is running.
-		
-		E.g. to capture audio from input node:
-<pre>
-AVAudioEngine *engine = [[AVAudioEngine alloc] init];
-AVAudioInputNode *input = [engine inputNode];
-AVAudioFormat *format = [input outputFormatForBus: 0];
-[input installTapOnBus: 0 bufferSize: 8192 format: format block: ^(AVAudioPCMBuffer *buf, AVAudioTime *when) {
-// ‘buf' contains audio captured from input node at time 'when'
-}];
-....
-// start engine
-</pre>
-*/
-- (void)installTapOnBus:(AVAudioNodeBus)bus bufferSize:(AVAudioFrameCount)bufferSize format:(AVAudioFormat * __nullable)format block:(AVAudioNodeTapBlock)tapBlock;
-
-/*!	@method removeTapOnBus:
-	@abstract Destroy a tap.
-	@param bus
-		the node output bus whose tap is to be destroyed
-	@return
-		YES for success.
-*/
-- (void)removeTapOnBus:(AVAudioNodeBus)bus;
-
-/*!	@property engine
-	@abstract The engine to which the node is attached (or nil).
-*/
-@property (nonatomic, readonly, nullable) AVAudioEngine *engine;
-
-/*! @property numberOfInputs
-	@abstract The node's number of input busses.
-*/
-@property (nonatomic, readonly) NSUInteger numberOfInputs;
-
-/*! @property numberOfOutputs
-	@abstract The node's number of output busses.
-*/
-@property (nonatomic, readonly) NSUInteger numberOfOutputs;
-
-/*! @property lastRenderTime
-	@abstract Obtain the time for which the node most recently rendered.
-	@discussion
-		Will return nil if the engine is not running or if the node is not connected to an input or
-		output node.
-*/
-@property (nonatomic, readonly, nullable) AVAudioTime *lastRenderTime;
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioPlayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioPlayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioPlayer.h	2015-09-30 23:17:58.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioPlayer.h	2016-05-25 07:19:42.000000000 +0200
@@ -1,133 +1,9 @@
 /*
-	File:  AVAudioPlayer.h
+	File:           AVAudioPlayer.h
+	Framework:      AVFoundation
 	
-	Framework:  AVFoundation
-
-	Copyright 2008-2015 Apple Inc. All rights reserved.
-*/
-
-#import <AVFoundation/AVBase.h>
-#import <Foundation/Foundation.h>
-#import <AVFoundation/AVAudioSettings.h>
-#import <AudioToolbox/AudioFile.h>
-#import <Availability.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-@class NSData, NSURL, NSError;
-@class AVAudioSessionChannelDescription;
-@protocol AVAudioPlayerDelegate;
-
-NS_CLASS_AVAILABLE(10_7, 2_2)
-@interface AVAudioPlayer : NSObject {
-@private
-	id _impl;
-}
-
-/* For all of these init calls, if a return value of nil is given you can check outError to see what the problem was.
- If not nil, then the object is usable for playing
-*/
-
-/* all data must be in the form of an audio file understood by CoreAudio */
-- (nullable instancetype)initWithContentsOfURL:(NSURL *)url error:(NSError **)outError;
-- (nullable instancetype)initWithData:(NSData *)data error:(NSError **)outError;
-
-/* The file type hint is a constant defined in AVMediaFormat.h whose value is a UTI for a file format. e.g. AVFileTypeAIFF. */
-/* Sometimes the type of a file cannot be determined from the data, or it is actually corrupt. The file type hint tells the parser what kind of data to look for so that files which are not self identifying or possibly even corrupt can be successfully parsed. */
-- (nullable instancetype)initWithContentsOfURL:(NSURL *)url fileTypeHint:(NSString * __nullable)utiString error:(NSError **)outError NS_AVAILABLE(10_9, 7_0);
-- (nullable instancetype)initWithData:(NSData *)data fileTypeHint:(NSString * __nullable)utiString error:(NSError **)outError NS_AVAILABLE(10_9, 7_0);
-
-/* transport control */
-/* methods that return BOOL return YES on success and NO on failure. */
-- (BOOL)prepareToPlay;	/* get ready to play the sound. happens automatically on play. */
-- (BOOL)play;			/* sound is played asynchronously. */
-- (BOOL)playAtTime:(NSTimeInterval)time NS_AVAILABLE(10_7, 4_0); /* play a sound some time in the future. time is an absolute time based on and greater than deviceCurrentTime. */
-- (void)pause;			/* pauses playback, but remains ready to play. */
-- (void)stop;			/* stops playback. no longer ready to play. */
-
-/* properties */
-
-@property(readonly, getter=isPlaying) BOOL playing; /* is it playing or not? */
-
-@property(readonly) NSUInteger numberOfChannels;
-@property(readonly) NSTimeInterval duration; /* the duration of the sound. */
-
-/* the delegate will be sent messages from the AVAudioPlayerDelegate protocol */ 
-@property(assign, nullable) id<AVAudioPlayerDelegate> delegate;
-
-/* one of these properties will be non-nil based on the init... method used */
-@property(readonly, nullable) NSURL *url; /* returns nil if object was not created with a URL */
-@property(readonly, nullable) NSData *data; /* returns nil if object was not created with a data object */
-
-@property float pan NS_AVAILABLE(10_7, 4_0); /* set panning. -1.0 is left, 0.0 is center, 1.0 is right. */
-@property float volume; /* The volume for the sound. The nominal range is from 0.0 to 1.0. */
-
-@property BOOL enableRate NS_AVAILABLE(10_8, 5_0); /* You must set enableRate to YES for the rate property to take effect. You must set this before calling prepareToPlay. */
-@property float rate NS_AVAILABLE(10_8, 5_0); /* See enableRate. The playback rate for the sound. 1.0 is normal, 0.5 is half speed, 2.0 is double speed. */
-
-
-/*  If the sound is playing, currentTime is the offset into the sound of the current playback position.  
-If the sound is not playing, currentTime is the offset into the sound where playing would start. */
-@property NSTimeInterval currentTime;
-
-/* returns the current time associated with the output device */
-@property(readonly) NSTimeInterval deviceCurrentTime NS_AVAILABLE(10_7, 4_0);
-
-/* "numberOfLoops" is the number of times that the sound will return to the beginning upon reaching the end. 
-A value of zero means to play the sound just once.
-A value of one will result in playing the sound twice, and so on..
-Any negative number will loop indefinitely until stopped.
+	Copyright 2016 Apple Inc. All rights reserved.
 */
-@property NSInteger numberOfLoops;
-
-/* settings */
-@property(readonly) NSDictionary<NSString *, id> *settings NS_AVAILABLE(10_7, 4_0); /* returns a settings dictionary with keys as described in AVAudioSettings.h */
-
-/* metering */
-
-@property(getter=isMeteringEnabled) BOOL meteringEnabled; /* turns level metering on or off. default is off. */
-
-- (void)updateMeters; /* call to refresh meter values */
-
-- (float)peakPowerForChannel:(NSUInteger)channelNumber; /* returns peak power in decibels for a given channel */
-- (float)averagePowerForChannel:(NSUInteger)channelNumber; /* returns average power in decibels for a given channel */
-
-#if TARGET_OS_IPHONE
-/* The channels property lets you assign the output to play to specific channels as described by AVAudioSession's channels property */
-/* This property is nil valued until set. */
-/* The array must have the same number of channels as returned by the numberOfChannels property. */
-@property(nonatomic, copy, nullable) NSArray<NSNumber *> *channelAssignments NS_AVAILABLE(10_9, 7_0); /* Array of AVAudioSessionChannelDescription objects */
-#endif
-
-@end
-
-/* A protocol for delegates of AVAudioPlayer */
-@protocol AVAudioPlayerDelegate <NSObject>
-@optional 
-/* audioPlayerDidFinishPlaying:successfully: is called when a sound has finished playing. This method is NOT called if the player is stopped due to an interruption. */
-- (void)audioPlayerDidFinishPlaying:(AVAudioPlayer *)player successfully:(BOOL)flag;
-
-/* if an error occurs while decoding it will be reported to the delegate. */
-- (void)audioPlayerDecodeErrorDidOccur:(AVAudioPlayer *)player error:(NSError * __nullable)error;
-
-#if TARGET_OS_IPHONE
-
-/* AVAudioPlayer INTERRUPTION NOTIFICATIONS ARE DEPRECATED - Use AVAudioSession instead. */
-
-/* audioPlayerBeginInterruption: is called when the audio session has been interrupted while the player was playing. The player will have been paused. */
-- (void)audioPlayerBeginInterruption:(AVAudioPlayer *)player NS_DEPRECATED_IOS(2_2, 8_0);
-
-/* audioPlayerEndInterruption:withOptions: is called when the audio session interruption has ended and this player had been interrupted while playing. */
-/* Currently the only flag is AVAudioSessionInterruptionFlags_ShouldResume. */
-- (void)audioPlayerEndInterruption:(AVAudioPlayer *)player withOptions:(NSUInteger)flags NS_DEPRECATED_IOS(6_0, 8_0);
-
-- (void)audioPlayerEndInterruption:(AVAudioPlayer *)player withFlags:(NSUInteger)flags NS_DEPRECATED_IOS(4_0, 6_0);
-
-/* audioPlayerEndInterruption: is called when the preferred method, audioPlayerEndInterruption:withFlags:, is not implemented. */
-- (void)audioPlayerEndInterruption:(AVAudioPlayer *)player NS_DEPRECATED_IOS(2_2, 6_0);
-
-#endif // TARGET_OS_IPHONE
 
-@end
+#import <AVFAudio/AVAudioPlayer.h>
 
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioPlayerNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioPlayerNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioPlayerNode.h	2015-09-30 23:17:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioPlayerNode.h	2016-05-25 07:19:42.000000000 +0200
@@ -1,239 +1,9 @@
 /*
-	File:		AVAudioPlayerNode.h
-	Framework:	AVFoundation
+	File:           AVAudioPlayerNode.h
+	Framework:      AVFoundation
 	
-	Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioNode.h>
-#import <AVFoundation/AVAudioFile.h>
-#import <AVFoundation/AVAudioMixing.h>
+#import <AVFAudio/AVAudioPlayerNode.h>
 
-NS_ASSUME_NONNULL_BEGIN
-
-@class AVAudioTime;
-
-/*!
-	@enum AVAudioPlayerNodeBufferOptions
-	@abstract	Options controlling buffer scheduling.
-	
-	@constant	AVAudioPlayerNodeBufferLoops
-					The buffer loops indefinitely.
-	@constant	AVAudioPlayerNodeBufferInterrupts
-					The buffer interrupts any buffer already playing.
-	@constant	AVAudioPlayerNodeBufferInterruptsAtLoop
-					The buffer interrupts any buffer already playing, at its loop point.
-*/
-typedef NS_OPTIONS(NSUInteger, AVAudioPlayerNodeBufferOptions) {
-    AVAudioPlayerNodeBufferLoops			= 1UL << 0,		// 0x01
-	AVAudioPlayerNodeBufferInterrupts		= 1UL << 1,		// 0x02
-	AVAudioPlayerNodeBufferInterruptsAtLoop	= 1UL << 2		// 0x04
-} NS_AVAILABLE(10_10, 8_0);
-
-/*!
-	@class AVAudioPlayerNode
-	@abstract Play buffers or segments of audio files.
-	@discussion
-		AVAudioPlayerNode supports scheduling the playback of `AVAudioBuffer` instances,
-		or segments of audio files opened via `AVAudioFile`. Buffers and segments may be
-		scheduled at specific points in time, or to play immediately following preceding segments.
-	
-		FORMATS
-		
-		Normally, you will want to configure the node's output format with the same number of
-		channels as are in the files and buffers to be played. Otherwise, channels will be dropped
-		or added as required. It is usually better to use an `AVAudioMixerNode` to
-		do this.
-	
-		Similarly, when playing file segments, the node will sample rate convert if necessary, but
-		it is often preferable to configure the node's output sample rate to match that of the file(s)
-		and use a mixer to perform the rate conversion.
-		
-		When playing buffers, there is an implicit assumption that the buffers are at the same
-		sample rate as the node's output format.
-		
-		TIMELINES
-	
-		The usual `AVAudioNode` sample times (as observed by `lastRenderTime`)
-		have an arbitrary zero point. AVAudioPlayerNode superimposes a second "player timeline" on
-		top of this, to reflect when the player was started, and intervals during which it was
-		paused. The methods `nodeTimeForPlayerTime:` and `playerTimeForNodeTime:`
-		convert between the two.
-
-		This class' `stop` method unschedules all previously scheduled buffers and
-		file segments, and returns the player timeline to sample time 0.
-
-		TIMESTAMPS
-		
-		The "schedule" methods all take an `AVAudioTime` "when" parameter. This is
-		interpreted as follows:
-		
-		1. nil:
-			- if there have been previous commands, the new one is played immediately following the
-				last one.
-			- otherwise, if the node is playing, the event is played in the very near future.
-			- otherwise, the command is played at sample time 0.
-		2. sample time:
-			- relative to the node's start time (which begins at 0 when the node is started).
-		3. host time:
-			- ignored unless sample time not valid.
-		
-		ERRORS
-		
-		The "schedule" methods can fail if:
-		
-		1. a buffer's channel count does not match that of the node's output format.
-		2. a file can't be accessed.
-		3. an AVAudioTime specifies neither a valid sample time or host time.
-		4. a segment's start frame or frame count is negative.
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioPlayerNode : AVAudioNode <AVAudioMixing>
-
-/*! @method scheduleBuffer:completionHandler:
-	@abstract Schedule playing samples from an AVAudioBuffer.
-	@param buffer
-		the buffer to play
-	@param completionHandler
-		called after the buffer has completely played or the player is stopped. may be nil.
-	@discussion
-		Schedules the buffer to be played following any previously scheduled commands.
-*/
-- (void)scheduleBuffer:(AVAudioPCMBuffer *)buffer completionHandler:(AVAudioNodeCompletionHandler __nullable)completionHandler;
-
-/*! @method scheduleBuffer:atTime:options:completionHandler:
-	@abstract Schedule playing samples from an AVAudioBuffer.
-	@param buffer
-		the buffer to play
-	@param when 
-		the time at which to play the buffer. see the discussion of timestamps, above.
-	@param options
-		options for looping, interrupting other buffers, etc.
-	@param completionHandler
-		called after the buffer has completely played or the player is stopped. may be nil.
-	@discussion
-*/
-- (void)scheduleBuffer:(AVAudioPCMBuffer *)buffer atTime:(AVAudioTime * __nullable)when options:(AVAudioPlayerNodeBufferOptions)options completionHandler:(AVAudioNodeCompletionHandler __nullable)completionHandler;
-
-/*! @method scheduleFile:atTime:completionHandler:
-	@abstract Schedule playing of an entire audio file.
-	@param file
-		the file to play
-	@param when 
-		the time at which to play the file. see the discussion of timestamps, above.
-	@param completionHandler
-		called after the file has completely played or the player is stopped. may be nil.
-*/
-- (void)scheduleFile:(AVAudioFile *)file atTime:(AVAudioTime * __nullable)when completionHandler:(AVAudioNodeCompletionHandler __nullable)completionHandler;
-
-/*! @method scheduleSegment:startingFrame:frameCount:atTime:completionHandler:
-	@abstract Schedule playing a segment of an audio file.
-	@param file
-		the file to play
-	@param startFrame
-		the starting frame position in the stream
-	@param numberFrames
-		the number of frames to play
-	@param when
-		the time at which to play the region. see the discussion of timestamps, above.
-	@param completionHandler
-		called after the segment has completely played or the player is stopped. may be nil.
-*/
-- (void)scheduleSegment:(AVAudioFile *)file startingFrame:(AVAudioFramePosition)startFrame frameCount:(AVAudioFrameCount)numberFrames atTime:(AVAudioTime * __nullable)when completionHandler:(AVAudioNodeCompletionHandler __nullable)completionHandler;
-
-/*!	@method stop
-	@abstract Clear all of the node's previously scheduled events and stop playback.
-	@discussion
-		All of the node's previously scheduled events are cleared, including any that are in the
-		middle of playing. The node's sample time (and therefore the times to which new events are 
-		to be scheduled) is reset to 0, and will not proceed until the node is started again (via
-		play or playAtTime).
-*/
-- (void)stop;
-
-/*! @method prepareWithFrameCount:
-	@abstract Prepares previously scheduled file regions or buffers for playback.
-	@param frameCount
-		The number of sample frames of data to be prepared before returning.
-	@discussion
-*/		
-- (void)prepareWithFrameCount:(AVAudioFrameCount)frameCount;
-
-/*!	@method play
-	@abstract Start or resume playback immediately.
-	@discussion
-		equivalent to playAtTime:nil
-*/
-- (void)play;
-
-/*!	@method playAtTime:
-	@abstract Start or resume playback at a specific time.
-	@param when
-		the node time at which to start or resume playback. nil signifies "now".
-	@discussion
-		This node is initially paused. Requests to play buffers or file segments are enqueued, and
-		any necessary decoding begins immediately. Playback does not begin, however, until the player
-		has started playing, via this method.
- 
-		E.g. To start a player X seconds in future:
-<pre>
-// start engine and player
-NSError *nsErr = nil;
-[_engine startAndReturnError:&nsErr];
-if (!nsErr) {
-	const float kStartDelayTime = 0.5; // sec
-	AVAudioFormat *outputFormat = [_player outputFormatForBus:0];
-	AVAudioFramePosition startSampleTime = _player.lastRenderTime.sampleTime + kStartDelayTime * outputFormat.sampleRate;
-	AVAudioTime *startTime = [AVAudioTime timeWithSampleTime:startSampleTime atRate:outputFormat.sampleRate];
-	[_player playAtTime:startTime];
-}
-</pre>
-*/
-- (void)playAtTime:(AVAudioTime * __nullable)when;
-
-/*! @method pause
-	@abstract Pause playback.
-	@discussion
-		The player's sample time does not advance while the node is paused.
-*/
-- (void)pause;
-
-/*!	@method nodeTimeForPlayerTime:
-	@abstract
-		Convert from player time to node time.
-	@param playerTime
-		a time relative to the player's start time
-	@return
-		a node time
-	@discussion
-		This method and its inverse `playerTimeForNodeTime:` are discussed in the
-		introduction to this class.
-	
-		If the player is not playing when this method is called, nil is returned.
-*/
-- (AVAudioTime * __nullable)nodeTimeForPlayerTime:(AVAudioTime *)playerTime;
-
-/*!	@method playerTimeForNodeTime:
-	@abstract
-		Convert from node time to player time.
-	@param nodeTime
-		a node time
-	@return
-		a time relative to the player's start time
-	@discussion
-		This method and its inverse `nodeTimeForPlayerTime:` are discussed in the
-		introduction to this class.
-	
-		If the player is not playing when this method is called, nil is returned.
-*/
-- (AVAudioTime * __nullable)playerTimeForNodeTime:(AVAudioTime *)nodeTime;
-
-/*!	@property playing
-	@abstract Indicates whether or not the player is playing.
-*/
-@property(nonatomic, readonly, getter=isPlaying) BOOL playing;
-
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioRecorder.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioRecorder.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioRecorder.h	2015-09-30 23:17:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioRecorder.h	2016-05-25 07:19:42.000000000 +0200
@@ -1,109 +1,9 @@
 /*
-	File:  AVAudioRecorder.h
+	File:           AVAudioRecorder.h
+	Framework:      AVFoundation
 	
-	Framework:  AVFoundation
-
-	Copyright 2008-2015 Apple Inc. All rights reserved.
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVBase.h>
-#import <Foundation/Foundation.h>
-#import <AVFoundation/AVAudioSettings.h>
-#import <Availability.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-@protocol AVAudioRecorderDelegate;
-@class NSURL, NSError;
-
-
-NS_CLASS_AVAILABLE(10_7, 3_0) __TVOS_UNAVAILABLE
-@interface AVAudioRecorder : NSObject {
-@private
-    void *_impl;
-}
-
-
-/* The file type to record is inferred from the file extension. Will overwrite a file at the specified url if a file exists */
-- (nullable instancetype)initWithURL:(NSURL *)url settings:(NSDictionary<NSString *, id> *)settings error:(NSError **)outError;
-
-/* transport control */
-/* methods that return BOOL return YES on success and NO on failure. */
-- (BOOL)prepareToRecord; /* creates the file and gets ready to record. happens automatically on record. */
-- (BOOL)record; /* start or resume recording to file. */
-- (BOOL)recordAtTime:(NSTimeInterval)time NS_AVAILABLE_IOS(6_0); /* start recording at specified time in the future. time is an absolute time based on and greater than deviceCurrentTime. */
-- (BOOL)recordForDuration:(NSTimeInterval) duration; /* record a file of a specified duration. the recorder will stop when it has recorded this length of audio */
-- (BOOL)recordAtTime:(NSTimeInterval)time forDuration:(NSTimeInterval) duration NS_AVAILABLE_IOS(6_0); /* record a file of a specified duration starting at specified time. time is an absolute time based on and greater than deviceCurrentTime. */
-- (void)pause; /* pause recording */
-- (void)stop; /* stops recording. closes the file. */
-
-- (BOOL)deleteRecording; /* delete the recorded file. recorder must be stopped. returns NO on failure. */
-
-/* properties */
-
-@property(readonly, getter=isRecording) BOOL recording; /* is it recording or not? */
-
-@property(readonly) NSURL *url; /* URL of the recorded file */
-
-/* these settings are fully valid only when prepareToRecord has been called */
-@property(readonly) NSDictionary<NSString *, id> *settings;
-
-/* the delegate will be sent messages from the AVAudioRecorderDelegate protocol */ 
-@property(assign, nullable) id<AVAudioRecorderDelegate> delegate;
-
-/* get the current time of the recording - only valid while recording */
-@property(readonly) NSTimeInterval currentTime;
-/* get the device current time - always valid */
-@property(readonly) NSTimeInterval deviceCurrentTime NS_AVAILABLE_IOS(6_0);
-
-/* metering */
-
-@property(getter=isMeteringEnabled) BOOL meteringEnabled; /* turns level metering on or off. default is off. */
-
-- (void)updateMeters; /* call to refresh meter values */
-
-- (float)peakPowerForChannel:(NSUInteger)channelNumber; /* returns peak power in decibels for a given channel */
-- (float)averagePowerForChannel:(NSUInteger)channelNumber; /* returns average power in decibels for a given channel */
-
-#if TARGET_OS_IPHONE
-/* The channels property lets you assign the output to record specific channels as described by AVAudioSession's channels property */
-/* This property is nil valued until set. */
-/* The array must have the same number of channels as returned by the numberOfChannels property. */
-@property(nonatomic, copy, nullable) NSArray<NSNumber *> *channelAssignments NS_AVAILABLE(10_9, 7_0); /* Array of AVAudioSessionChannelDescription objects */
-#endif
-
-@end
-
-
-/* A protocol for delegates of AVAudioRecorder */
-__TVOS_UNAVAILABLE
-@protocol AVAudioRecorderDelegate <NSObject>
-@optional 
-
-/* audioRecorderDidFinishRecording:successfully: is called when a recording has been finished or stopped. This method is NOT called if the recorder is stopped due to an interruption. */
-- (void)audioRecorderDidFinishRecording:(AVAudioRecorder *)recorder successfully:(BOOL)flag;
-
-/* if an error occurs while encoding it will be reported to the delegate. */
-- (void)audioRecorderEncodeErrorDidOccur:(AVAudioRecorder *)recorder error:(NSError * __nullable)error;
-
-#if TARGET_OS_IPHONE
-
-/* AVAudioRecorder INTERRUPTION NOTIFICATIONS ARE DEPRECATED - Use AVAudioSession instead. */
-
-/* audioRecorderBeginInterruption: is called when the audio session has been interrupted while the recorder was recording. The recorded file will be closed. */
-- (void)audioRecorderBeginInterruption:(AVAudioRecorder *)recorder NS_DEPRECATED_IOS(2_2, 8_0);
-
-/* audioRecorderEndInterruption:withOptions: is called when the audio session interruption has ended and this recorder had been interrupted while recording. */
-/* Currently the only flag is AVAudioSessionInterruptionFlags_ShouldResume. */
-- (void)audioRecorderEndInterruption:(AVAudioRecorder *)recorder withOptions:(NSUInteger)flags NS_DEPRECATED_IOS(6_0, 8_0);
-
-- (void)audioRecorderEndInterruption:(AVAudioRecorder *)recorder withFlags:(NSUInteger)flags NS_DEPRECATED_IOS(4_0, 6_0);
-
-/* audioRecorderEndInterruption: is called when the preferred method, audioRecorderEndInterruption:withFlags:, is not implemented. */
-- (void)audioRecorderEndInterruption:(AVAudioRecorder *)recorder NS_DEPRECATED_IOS(2_2, 6_0);
-
-#endif // TARGET_OS_IPHONE
-
-@end
+#import <AVFAudio/AVAudioRecorder.h>
 
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioSequencer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioSequencer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioSequencer.h	2015-09-30 23:17:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioSequencer.h	2016-05-25 07:19:42.000000000 +0200
@@ -1,371 +1,9 @@
 /*
-	File:		AVAudioSequencer.h
-	Framework:	AVFoundation
-
-	Copyright (c) 2015 Apple Inc. All Rights Reserved.
-*/
-
-#import <Foundation/Foundation.h>
-#import <AudioToolbox/MusicPlayer.h>
-
-#if __has_include(<CoreMIDI/MIDIServices.h>)
-	#import <CoreMIDI/MIDIServices.h>
-#endif
-
-NS_ASSUME_NONNULL_BEGIN
-
-@class AVAudioUnit;
-@class AVAudioTime;
-@class AVAudioEngine;
-@class AVMusicTrack;
-@class AVMusicTrackEventIterator;
-@class AVAudioSequencer;
-
-/*!	@typedef AVMusicTimeStamp
-	@abstract A fractional number of beats
+	File:           AVAudioSequencer.h
+	Framework:      AVFoundation
 	
-	@discussion
- 		This is used for all sequencer timeline-related methods.  The relationship between this
- 		value and time in seconds is determined by the sequence's tempo.
- */
-
-typedef Float64 AVMusicTimeStamp;
-
-/*! @typedef AVMusicSequenceLoadOptions
- 	@abstract Determines whether data on different MIDI channels is mapped to multiple tracks, or if the tracks are preserved as-is.
- 	@discussion
-		If AVMusicSequenceLoadSMF_ChannelsToTracks is set, the loaded MIDI Sequence will contain a tempo track,
-		one track for each MIDI channel that is found in the SMF, and one track for SysEx and/or MetaEvents (this will
- 		be the last track in the sequence).
- 		If AVMusicSequenceLoadSMF_PreserveTracks is set, the loadad MIDI Sequence will contain one track for each track
- 		that is found in the SMF, plus a tempo track (if not found in the SMF).
-*/
-
-typedef NS_OPTIONS(NSUInteger, AVMusicSequenceLoadOptions) {
-	AVMusicSequenceLoadSMF_PreserveTracks		= 0,				// 0x00
-	AVMusicSequenceLoadSMF_ChannelsToTracks		= (1UL << 0)		// 0x01
-} NS_AVAILABLE(10_11, 9_0);
-
-/*! @typedef AVBeatRange
- 	@abstract Used to describe a specific time range within an AVMusicTrack.
-*/
-
-typedef struct _AVBeatRange {
-	AVMusicTimeStamp start;
-	AVMusicTimeStamp length;
-} AVBeatRange;
-
-NS_INLINE AVBeatRange AVMakeBeatRange(AVMusicTimeStamp startBeat, AVMusicTimeStamp lengthInBeats) {
-	AVBeatRange r;
-	r.start = startBeat;
-	r.length = lengthInBeats;
-	return r;
-}
-
-/*! @class AVAudioSequencer
-    @abstract A collection of MIDI events organized into AVMusicTracks, plus a player to play back the events.
- */
-
-NS_CLASS_AVAILABLE(10_11, 9_0)
-@interface AVAudioSequencer : NSObject {
-@protected
-	void *_impl;
-}
-
-/*! @method init
-	@abstract
-		Initialize a new sequencer, which will not be connected to an audio engine.
- 	@discussion
- 		This is used to create a sequencer whose tracks will only send events to external MIDI endpoints.
- */
-- (instancetype)init	__TVOS_UNAVAILABLE;
-
-/*! @method initWithAudioEngine:
-	@abstract
-		Initialize a new sequencer, handing it the audio engine.
-*/
-- (instancetype)initWithAudioEngine:(AVAudioEngine *)engine;
-
-/*! @method loadFromURL:options:error:
-	@abstract Load the file referenced by the URL and add the events to the sequence
- 	@param fileURL
- 	@param options
- 		determines how the file's contents are mapped to tracks inside the sequence
-	@param outError
-*/
-- (BOOL)loadFromURL:(NSURL *)fileURL options:(AVMusicSequenceLoadOptions)options error:(NSError **)outError;
-
-/*! @method loadFromData:options:error:
-	@abstract Parse the data and add the its events to the sequence
-	@param data
-	@param options
- 		determines how the contents are mapped to tracks inside the sequence
-	@param outError
-*/
-- (BOOL)loadFromData:(NSData *)data options:(AVMusicSequenceLoadOptions)options error:(NSError **)outError;
-
-/*! @method writeToURL:SMPTEResolution:replaceExisting:error:
-	@abstract Create and write a MIDI file from the events in the sequence
- 	@param fileURL
- 		the path for the file to be created
-	@param resolution
-		the relationship between "tick" and quarter note for saving to a Standard MIDI File - pass in
-		zero to use default - this will be the value that is currently set on the tempo track
-	@param replace
-		if the file already exists, YES will cause it to be overwritten with the new data.
-		Otherwise the call will fail with a permission error.
-	@param outError
-	@discussion
-		Only MIDI events are written when writing to the MIDI file. MIDI files are normally beat
- 		based, but can also have a SMPTE (or real-time rather than beat time) representation.
- 		The relationship between "tick" and quarter note for saving to Standard MIDI File
-		- pass in zero to use default - this will be the value that is currently set on the tempo track
- */
-- (BOOL)writeToURL:(NSURL *)fileURL SMPTEResolution:(NSInteger)resolution replaceExisting:(BOOL)replace error:(NSError **)outError;
-
-/*!	@method dataWithSMPTEResolution:error:
- 	@abstract Return a data object containing the events from the sequence
- 	@discussion
- 		All details regarding the SMPTE resolution apply here as well.
- 		The returned NSData lifetime is controlled by the client.
-*/
-- (NSData *)dataWithSMPTEResolution:(NSInteger)SMPTEResolution error:(NSError **)outError;
-
-/*!	@method secondsForBeats:
-	@abstract Get the time in seconds for the given beat position (timestamp) in the track
-*/
-- (NSTimeInterval)secondsForBeats:(AVMusicTimeStamp)beats;
-
-/*!	@method beatsForSeconds:
-	@abstract Get the beat position (timestamp) for the given time in the track
-*/
-- (AVMusicTimeStamp)beatsForSeconds:(NSTimeInterval)seconds;
-
-/* properties */
-
-/*!	@property tracks
-	@abstract An NSArray containing all the tracks in the sequence
-	@discussion
-		Track indices count from 0, and do not include the tempo track.
- */
-@property (nonatomic, readonly) NSArray<AVMusicTrack *> *tracks;
-
-/*!	@property tempoTrack
-	@abstract The tempo track
-	 @discussion
-		 Each sequence has a single tempo track. All tempo events are placed into this track (as well
-		 as other appropriate events (for instance, the time signature from a MIDI file). The tempo
-		 track can be edited and iterated upon as any other track. Non-tempo events in a tempo track
-		 are ignored.
-*/
-@property (nonatomic, readonly) AVMusicTrack *tempoTrack;
-
-/*!	@property userInfo
- 	@abstract A dictionary containing meta-data derived from a sequence
- 	@discussion
- 		The dictionary can contain one or more of the kAFInfoDictionary_* keys
-		specified in <AudioToolbox/AudioFile.h>
-*/
-@property (nonatomic, readonly) NSDictionary<NSString *, id> *userInfo;
-
-@end
-
-@interface AVAudioSequencer(AVAudioSequencer_Player)
-
-/*! @property currentPositionInSeconds
-	@abstract The current playback position in seconds
-	@discussion
-		Setting this positions the sequencer's player to the specified time.  This can be set while
-		the player is playing, in which case playback will resume at the new position.
- */
-@property(nonatomic) NSTimeInterval currentPositionInSeconds;
-
-/*! @property currentPositionInBeats
-	@abstract The current playback position in beats
-	@discussion
-		Setting this positions the sequencer's player to the specified beat.  This can be set while
-		the player is playing, in which case playback will resume at the new position.
- */
-@property(nonatomic) NSTimeInterval currentPositionInBeats;
-
-
-/*! @property playing
-	@abstract Indicates whether or not the sequencer's player is playing
-	@discussion
-		Returns TRUE if the sequencer's player has been started and not stopped. It may have
-		"played" past the end of the events in the sequence, but it is still considered to be
-		playing (and its time value increasing) until it is explicitly stopped.
- */
-@property(nonatomic, readonly, getter=isPlaying) BOOL playing;
-
-/*! @property rate
-	@abstract The playback rate of the sequencer's player
-	@discussion
-		1.0 is normal playback rate.  Rate must be > 0.0.
- */
-@property (nonatomic) float rate;
-
-/*!	@method hostTimeForBeats:error:
-	@abstract Returns the host time that will be (or was) played at the specified beat.
-    @discussion
-		This call is only valid if the player is playing and will return 0 with an error if the
-		player is not playing or if the starting position of the player (its "starting beat") was 
-		after the specified beat.  The method uses the sequence's tempo map to translate a beat
-		time from the starting time and beat of the player.
-*/
-- (UInt64)hostTimeForBeats:(AVMusicTimeStamp)inBeats error:(NSError **)outError;
-
-/*!	@method beatsForHostTime:error:
-	@abstract Returns the beat that will be (or was) played at the specified host time.
-    @discussion
-		This call is only valid if the player is playing and will return 0 with an error if the
-		player is not playing or if the starting time of the player was after the specified host
-		time.  The method uses the sequence's tempo map to retrieve a beat time from the starting
-		and specified host time.
-*/
-- (AVMusicTimeStamp)beatsForHostTime:(UInt64)inHostTime error:(NSError **)outError;
-
-/*! @method prepareToPlay
-	@abstract Get ready to play the sequence by prerolling all events
-	@discussion
-		Happens automatically on play if it has not already been called, but may produce a delay in startup.
- */
-- (void)prepareToPlay;
-
-/*!	@method	startAndReturnError:
-	@abstract	Start the sequencer's player
-	@discussion
-		If the AVAudioSequencer has not been prerolled, it will pre-roll itself and then start.
-*/
-- (BOOL)startAndReturnError:(NSError **)outError;
-
-/*!	@method	stop
-	@abstract	Stop the sequencer's player
-	@discussion
- 		Stopping the player leaves it in an un-prerolled state, but stores the playback position so that
- 		a subsequent call to startAndReturnError will resume where it left off.
- 		This action will not stop an associated audio engine.
-*/
-- (void)stop;
-
-@end
-
-
-/*! @class AVMusicTrack
-    @abstract A collection of music events which will be sent to a given destination, and which can be 
- 				offset, muted, etc. independently of events in other tracks.
- */
-NS_CLASS_AVAILABLE(10_11, 9_0)
-@interface AVMusicTrack : NSObject {
-@protected
-	void *_impl;
-}
-
-/* properties */
-
-/*!	@property destinationAudioUnit
-	@abstract The AVAudioUnit which will receive the track's events
-	@discussion
-		This is mutually exclusive with setting a destination MIDIEndpoint.  The AU must already
-		be attached to an audio engine, and the track must be part of the AVAudioSequencer
-		associated with that engine. When playing, the track will send its events to that AVAudioUnit.
-		The destination AU cannot be changed while the track's sequence is playing.
- */
-@property (nonatomic, retain, nullable) AVAudioUnit *destinationAudioUnit;
-
-/*!	@property destinationMIDIEndpoint
-	@abstract Set the track's target to the specified MIDI endpoint
-	@discussion
-		This is mutually exclusive with setting a destination audio unit.  Setting this will remove the
- 		track's reference to an AVAudioUnit destination.  When played, the track will send its events to the MIDI
- 		Endpoint.  See also MIDIDestinationCreate.  The endpoint cannot be changed while the track's sequence is playing.
- */
-#if (TARGET_OS_MAC && !TARGET_OS_IPHONE) || TARGET_OS_IOS
-@property (nonatomic) MIDIEndpointRef destinationMIDIEndpoint;
-#endif
-
-/*!	@property loopRange
- 	@abstract The timestamp range in beats for the loop
- 	@discussion
-		The loop is set by specifying its beat range.
-*/
-@property (nonatomic) AVBeatRange loopRange;
-
-/*!	@property loopingEnabled
-	@abstract Determines whether or not the track is looped.
-	@discussion
-		If loopRange has not been set, the full track will be looped.
-*/
-@property (nonatomic,getter=isLoopingEnabled) BOOL loopingEnabled;
-
-typedef NS_ENUM(NSInteger, AVMusicTrackLoopCount) {
-	AVMusicTrackLoopCountForever		= -1
-} NS_ENUM_AVAILABLE(10_10, 8_0);
-
-/*!	@property numberOfLoops
- 	@abstract The number of times that the track's loop will repeat
- 	@discussion
- 		If set to AVMusicTrackLoopCountForever, the track will loop forever.
- 		Otherwise, legal values start with 1.
-*/
-@property (nonatomic) NSInteger numberOfLoops;
-
-/*! @property offsetTime
-    @abstract Offset the track's start time to the specified time in beats
- 	@discussion
-        By default this value is zero.
-*/
-@property (nonatomic) AVMusicTimeStamp offsetTime;
-
-/*! @property muted
-    @abstract Whether the track is muted
-*/
-@property (nonatomic,getter=isMuted) BOOL muted;
-
-/*! @property soloed
-    @abstract Whether the track is soloed
-*/
-@property (nonatomic,getter=isSoloed) BOOL soloed;
-
-/*! @property lengthInBeats
-    @abstract The total duration of the track in beats
-    @discussion
-		This will return the beat of the last event in the track plus any additional time that may be
-		needed for fading out of ending notes or round a loop point to musical bar, etc.  If this
-		has not been set by the user, the track length will always be adjusted to the end of the
-		last active event in a track and is adjusted dynamically as events are added or removed.
-
-		The property will return the maximum of the user-set track length, or the calculated length.
-*/
-@property (nonatomic) AVMusicTimeStamp lengthInBeats;
-
-/*! @property lengthInSeconds
-    @abstract The total duration of the track in seconds
-    @discussion
-		This will return time of the last event in the track plus any additional time that may be
-		needed for fading out of ending notes or round a loop point to musical bar, etc.  If this
-		has not been set by the user, the track length will always be adjusted to the end of the
-		last active event in a track and is adjusted dynamically as events are added or removed.
- 
- The property will return the maximum of the user-set track length, or the calculated length.
- */
-@property (nonatomic) NSTimeInterval lengthInSeconds;
-
-
-/*! @property timeResolution
-    @abstract The time resolution value for the sequence, in ticks (pulses) per quarter note (PPQN)
-    @discussion
-		If a MIDI file was used to construct the containing sequence, the resolution will be what
-		was in the file. If you want to keep a time resolution when writing a new file, you can
-		retrieve this value and then specify it when calling -[AVAudioSequencer
-		writeToFile:flags:withResolution]. It has no direct bearing on the rendering or notion of
-		time of the sequence itself, just its representation in MIDI files. By default this is set
-		to either 480 if the sequence was created manually, or a value based on what was in a MIDI
-		file if the sequence was created from a MIDI file.
-		This can only be retrieved from the tempo track.
+	Copyright 2016 Apple Inc. All rights reserved.
 */
-@property (nonatomic, readonly) NSUInteger timeResolution;
 
-@end
+#import <AVFAudio/AVAudioSequencer.h>
 
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioSession.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioSession.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioSession.h	2015-09-30 23:17:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioSession.h	2016-05-25 07:19:42.000000000 +0200
@@ -1,797 +1,9 @@
 /*
-	File:  AVAudioSession.h
+	File:           AVAudioSession.h
+	Framework:      AVFoundation
 	
-	Framework:  AVFoundation
-	
-	Copyright 2009-2015 Apple Inc. All rights reserved.
-	
-*/
-
-#import <AVFoundation/AVBase.h>
-#import <Foundation/NSObject.h>
-#import <Foundation/NSArray.h>
-#import <Foundation/NSDate.h>	/* for NSTimeInterval */
-#import <AvailabilityMacros.h>
-#import <CoreAudio/CoreAudioTypes.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-/* This protocol is available with iPhone 3.0 or later */
-@protocol AVAudioSessionDelegate;
-@class NSError, NSString, NSNumber;
-@class AVAudioSessionChannelDescription, AVAudioSessionPortDescription, AVAudioSessionRouteDescription, AVAudioSessionDataSourceDescription;
-
-/*
- Notes on terminology used in this API.
- Some of the property names and class names in AVAudioSession differ from
- the names used in the 'C' language Audio Session API.  In this API, an audio 
- "route" is made up of zero or more input "ports" and zero or more ouput "ports". 
- If the current audio category does not support inputs, the route will consist purely of 
- outputs.  Conversely, if the category does not support output, the route will
- consist purely of inputs.  Categories that support simultaneous input and output
- will have both inputs and outputs in the route.  
- 
- A "port" refers to a single input or output within an audio route.  Examples of 
- ports include built-in speaker, wired microphone, or Bluetooth A2DP output.
-*/
-
-
-#pragma mark -- enumerations --
-
-/* For use with AVAudioSessionInterruptionNotification */
-typedef NS_OPTIONS(NSUInteger, AVAudioSessionInterruptionOptions)
-{
-	AVAudioSessionInterruptionOptionShouldResume = 1
-} NS_AVAILABLE_IOS(6_0);
-
-/*  options for use when calling setActive:withOptions:error: 
-AVAudioSessionSetActiveOptionNotifyOthersOnDeactivation -- 
-Notify an interrupted app that the interruption has ended and it may resume playback. Only valid on 
-session deactivation. */
-typedef NS_OPTIONS(NSUInteger, AVAudioSessionSetActiveOptions)
-{
-	AVAudioSessionSetActiveOptionNotifyOthersOnDeactivation = 1
-} NS_AVAILABLE_IOS(6_0);
-
-/* values to use for setting overrideOutputAudioPort property
-AVAudioSessionPortOverrideNone -- 
-No override.  Return audio routing to the default state for the current audio category.
-AVAudioSessionPortOverrideSpeaker -- 
-Route audio output to speaker.  Use this override with AVAudioSessionCategoryPlayAndRecord, which by 
-default routes the output to the receiver. */
-typedef NS_ENUM(NSUInteger, AVAudioSessionPortOverride)
-{
-	AVAudioSessionPortOverrideNone    = 0,
-	AVAudioSessionPortOverrideSpeaker __TVOS_PROHIBITED = 'spkr'
-} NS_AVAILABLE_IOS(6_0) ;
-
-/* values for AVAudioSessionRouteChangeReasonKey in AVAudioSessionRouteChangeNotification userInfo dictionary
- AVAudioSessionRouteChangeReasonUnknown
-	The reason is unknown.
- AVAudioSessionRouteChangeReasonNewDeviceAvailable
-	A new device became available (e.g. headphones have been plugged in).
- AVAudioSessionRouteChangeReasonOldDeviceUnavailable
-	The old device became unavailable (e.g. headphones have been unplugged).
- AVAudioSessionRouteChangeReasonCategoryChange
-	The audio category has changed (e.g. AVAudioSessionCategoryPlayback has been changed to AVAudioSessionCategoryPlayAndRecord).
- AVAudioSessionRouteChangeReasonOverride
-	The route has been overridden (e.g. category is AVAudioSessionCategoryPlayAndRecord and the output 
-	has been changed from the receiver, which is the default, to the speaker).
- AVAudioSessionRouteChangeReasonWakeFromSleep
-	The device woke from sleep.
- AVAudioSessionRouteChangeReasonNoSuitableRouteForCategory
-	Returned when there is no route for the current category (for instance, the category is AVAudioSessionCategoryRecord
-	but no input device is available).
- AVAudioSessionRouteChangeReasonRouteConfigurationChange
-	Indicates that the set of input and/our output ports has not changed, but some aspect of their
-	configuration has changed.  For example, a port's selected data source has changed.
-*/
-typedef NS_ENUM(NSUInteger, AVAudioSessionRouteChangeReason)
-{
-	AVAudioSessionRouteChangeReasonUnknown = 0,
-	AVAudioSessionRouteChangeReasonNewDeviceAvailable = 1,
-	AVAudioSessionRouteChangeReasonOldDeviceUnavailable = 2,
-	AVAudioSessionRouteChangeReasonCategoryChange = 3,
-	AVAudioSessionRouteChangeReasonOverride = 4,
-	AVAudioSessionRouteChangeReasonWakeFromSleep = 6,
-	AVAudioSessionRouteChangeReasonNoSuitableRouteForCategory = 7,
-	AVAudioSessionRouteChangeReasonRouteConfigurationChange NS_ENUM_AVAILABLE_IOS(7_0) = 8
-} NS_AVAILABLE_IOS(6_0);
-
-/* values for setCategory:withOptions:error:
-AVAudioSessionCategoryOptionMixWithOthers -- 
-	This allows an application to set whether or not other active audio apps will be interrupted or mixed with
-	when your app's audio session goes active. The typical cases are:
-	 (1) AVAudioSessionCategoryPlayAndRecord or AVAudioSessionCategoryMultiRoute
-		 this will default to false, but can be set to true. This would allow other applications to play in the background
-		 while an app had both audio input and output enabled
-	 (2) AVAudioSessionCategoryPlayback
-		 this will default to false, but can be set to true. This would allow other applications to play in the background,
-		 but an app will still be able to play regardless of the setting of the ringer switch
-	 (3) Other categories
-		 this defaults to false and cannot be changed (that is, the mix with others setting of these categories
-		 cannot be overridden. An application must be prepared for setting this property to fail as behaviour 
-		 may change in future releases. If an application changes their category, they should reassert the 
-		 option (it is not sticky across category changes).
- 
-AVAudioSessionCategoryOptionDuckOthers -- 
-	This allows an application to set whether or not other active audio apps will be ducked when when your app's audio
-	session goes active. An example of this is the Nike app, which provides periodic updates to its user (it reduces the
-	volume of any music currently being played while it provides its status). This defaults to off. Note that the other
-	audio will be ducked for as long as the current session is active. You will need to deactivate your audio
-	session when you want full volume playback of the other audio. 
-    If your category is AVAudioSessionCategoryPlayback, AVAudioSessionCategoryPlayAndRecord, or 
-	AVAudioSessionCategoryMultiRoute, by default the audio session will be non-mixable and non-ducking. 
-	Setting this option will also make your category mixable with others (AVAudioSessionCategoryOptionMixWithOthers
-	will be set).
- 
-AVAudioSessionCategoryOptionAllowBluetooth --
-	This allows an application to change the default behaviour of some audio session categories with regards to showing
-	bluetooth devices as available routes. The current category behavior is:
-	 (1) AVAudioSessionCategoryPlayAndRecord
-		 this will default to false, but can be set to true. This will allow a paired bluetooth device to show up as
-		 an available route for input, while playing through the category-appropriate output
-	 (2) AVAudioSessionCategoryRecord
-		 this will default to false, but can be set to true. This will allow a paired bluetooth device to show up
-		 as an available route for input
-	 (3) Other categories
-		 this defaults to false and cannot be changed (that is, enabling bluetooth for input in these categories is
-		 not allowed)
-		 An application must be prepared for setting this option to fail as behaviour may change in future releases.
-		 If an application changes their category or mode, they should reassert the override (it is not sticky
-		 across category and mode changes).
- 
-AVAudioSessionCategoryOptionDefaultToSpeaker --
-	This allows an application to change the default behaviour of some audio session categories with regards to
-	the audio route. The current category behavior is:
-	 (1) AVAudioSessionCategoryPlayAndRecord category
-		 this will default to false, but can be set to true. this will route to Speaker (instead of Receiver)
-		 when no other audio route is connected.
-	 (2) Other categories
-		 this defaults to false and cannot be changed (that is, the default to speaker setting of these
-		 categories cannot be overridden
-		 An application must be prepared for setting this property to fail as behaviour may change in future releases.
-		 If an application changes their category, they should reassert the override (it is not sticky across
-		 category and mode changes). 
- 
-AVAudioSessionCategoryOptionInterruptSpokenAudioAndMixWithOthers --
-	If another app's audio session mode is set to AVAudioSessionModeSpokenAudio (podcast playback in the background for example),
-	then that other app's audio will be interrupted when the current application's audio session goes active. An example of this
-	is a navigation app that provides navigation prompts to its user (it pauses any spoken audio currently being played while it
-	plays the prompt). This defaults to off. Note that the other app's audio will be paused for as long as the current session is
-	active. You will need to deactivate your audio session to allow the other audio to resume playback.
-	Setting this option will also make your category mixable with others (AVAudioSessionCategoryOptionMixWithOthers
-	will be set).  If you want other non-spoken audio apps to duck their audio when your app's session goes active, also set
-	AVAudioSessionCategoryOptionDuckOthers.
- */
-typedef NS_OPTIONS(NSUInteger, AVAudioSessionCategoryOptions)
-{
-	/* MixWithOthers is only valid with AVAudioSessionCategoryPlayAndRecord, AVAudioSessionCategoryPlayback, and  AVAudioSessionCategoryMultiRoute */
-	AVAudioSessionCategoryOptionMixWithOthers			= 0x1,
-	/* DuckOthers is only valid with AVAudioSessionCategoryPlayAndRecord, AVAudioSessionCategoryPlayback, and AVAudioSessionCategoryMultiRoute */
-	AVAudioSessionCategoryOptionDuckOthers				= 0x2,
-	/* AllowBluetooth is only valid with AVAudioSessionCategoryRecord and AVAudioSessionCategoryPlayAndRecord */
-	AVAudioSessionCategoryOptionAllowBluetooth	__TVOS_PROHIBITED		= 0x4,
-	/* DefaultToSpeaker is only valid with AVAudioSessionCategoryPlayAndRecord */
-	AVAudioSessionCategoryOptionDefaultToSpeaker __TVOS_PROHIBITED		= 0x8,
-	/* InterruptSpokenAudioAndMixWithOthers is only valid with AVAudioSessionCategoryPlayAndRecord, AVAudioSessionCategoryPlayback, and AVAudioSessionCategoryMultiRoute */
-	AVAudioSessionCategoryOptionInterruptSpokenAudioAndMixWithOthers NS_AVAILABLE_IOS(9_0) 	= 0x11
-} NS_AVAILABLE_IOS(6_0);
-
-typedef NS_ENUM(NSUInteger, AVAudioSessionInterruptionType)
-{
-	AVAudioSessionInterruptionTypeBegan = 1,  /* the system has interrupted your audio session */
-	AVAudioSessionInterruptionTypeEnded = 0,  /* the interruption has ended */
-} NS_AVAILABLE_IOS(6_0);
-
-/* Used in AVAudioSessionSilenceSecondaryAudioHintNotification to indicate whether optional secondary audio muting should begin or end */
-typedef NS_ENUM(NSUInteger, AVAudioSessionSilenceSecondaryAudioHintType)
-{
-	AVAudioSessionSilenceSecondaryAudioHintTypeBegin = 1,  /* the system is indicating that another application's primary audio has started */
-	AVAudioSessionSilenceSecondaryAudioHintTypeEnd = 0,    /* the system is indicating that another application's primary audio has stopped */
-} NS_AVAILABLE_IOS(8_0);
-
-/*!
-	@enum AVAudioSessionRecordPermission values
-	@abstract   These are the values returned by recordPermission.
-	@constant   AVAudioSessionRecordPermissionUndetermined
-		The user has not yet been asked for permission.
-	@constant   AVAudioSessionRecordPermissionDenied
- 		The user has been asked and has denied permission.
-	@constant   AVAudioSessionRecordPermissionGranted
- 		The user has been asked and has granted permission.
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-typedef NS_OPTIONS(NSUInteger, AVAudioSessionRecordPermission)
-{
-	AVAudioSessionRecordPermissionUndetermined		= 'undt',
-	AVAudioSessionRecordPermissionDenied			= 'deny',
-	AVAudioSessionRecordPermissionGranted			= 'grnt'
-} NS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED;
-
-/*!
-	@enum AVAudioSession error codes
-	@abstract   These are the error codes returned from the AVAudioSession API.
-	@constant   AVAudioSessionErrorCodeNone
-		Operation succeeded.
-	@constant   AVAudioSessionErrorCodeMediaServicesFailed
-		The app attempted to use the audio session during or after a Media Services failure.  App should
- 		wait for a AVAudioSessionMediaServicesWereResetNotification and then rebuild all its state.
-	@constant	AVAudioSessionErrorCodeIsBusy
- 		The app attempted to set its audio session inactive, but it is still actively playing and/or recording.
- 	@constant	AVAudioSessionErrorCodeIncompatibleCategory
- 		The app tried to perform an operation on a session but its category does not support it.
- 		For instance, if the app calls setPreferredInputNumberOfChannels: while in a playback-only category.
-	@constant	AVAudioSessionErrorCodeCannotInterruptOthers
-		The app's audio session is non-mixable and trying to go active while in the background.
- 		This is allowed only when the app is the NowPlaying app.
-	@constant	AVAudioSessionErrorCodeMissingEntitlement
-		The app does not have the required entitlements to perform an operation.
-	@constant	AVAudioSessionErrorCodeSiriIsRecording
- 		The app tried to do something with the audio session that is not allowed while Siri is recording.
- 	@constant	AVAudioSessionErrorCodeCannotStartPlaying
-		The app is not allowed to start recording and/or playing, usually because of a lack of audio key in
- 		its Info.plist.  This could also happen if the app has this key but uses a category that can't record 
- 		and/or play in the background (AVAudioSessionCategoryAmbient, AVAudioSessionCategorySoloAmbient, etc.).
-	@constant	AVAudioSessionErrorCodeCannotStartRecording
-		The app is not allowed to start recording, usually because it is starting a mixable recording from the
- 		background and is not an Inter-App Audio app.
-	@constant	AVAudioSessionErrorCodeBadParam
- 		An illegal value was used for a property.
-	@constant	AVAudioSessionErrorInsufficientPriority
- 		The app was not allowed to set the audio category because another app (Phone, etc.) is controlling it.
-	@constant	AVAudioSessionErrorCodeResourceNotAvailable
-		The operation failed because the device does not have sufficient hardware resources to complete the action. 
-		For example, the operation requires audio input hardware, but the device has no audio input available.
-	@constant	AVAudioSessionErrorCodeUnspecified
- 		An unspecified error has occurred.
-*/
-
-typedef NS_ENUM(NSInteger, AVAudioSessionErrorCode)
-{
-	AVAudioSessionErrorCodeNone							=  0,
-	AVAudioSessionErrorCodeMediaServicesFailed			= 'msrv',			/* 0x6D737276, 1836282486	*/
-	AVAudioSessionErrorCodeIsBusy						= '!act',			/* 0x21616374, 560030580	*/
-	AVAudioSessionErrorCodeIncompatibleCategory			= '!cat',			/* 0x21636174, 560161140	*/
-	AVAudioSessionErrorCodeCannotInterruptOthers		= '!int',			/* 0x21696E74, 560557684	*/
-	AVAudioSessionErrorCodeMissingEntitlement			= 'ent?',			/* 0x656E743F, 1701737535	*/
-	AVAudioSessionErrorCodeSiriIsRecording				= 'siri',			/* 0x73697269, 1936290409	*/
-	AVAudioSessionErrorCodeCannotStartPlaying			= '!pla',			/* 0x21706C61, 561015905	*/
-	AVAudioSessionErrorCodeCannotStartRecording			= '!rec',			/* 0x21726563, 561145187	*/
-	AVAudioSessionErrorCodeBadParam						= -50,
-	AVAudioSessionErrorInsufficientPriority				= '!pri',			/* 0x21707269, 561017449	*/
-	AVAudioSessionErrorCodeResourceNotAvailable			= '!res',			/* 0x21726573, 561145203	*/
-	AVAudioSessionErrorCodeUnspecified					= 'what'			/* 0x77686174, 2003329396	*/
-} NS_AVAILABLE_IOS(7_0);
-
-#pragma mark -- AVAudioSession interface --
-NS_CLASS_AVAILABLE(NA, 3_0)
-@interface AVAudioSession : NSObject {
-@private
-    void * _impl;
-}
-
- /* returns singleton instance */
-+ (AVAudioSession*)sharedInstance;
-
-/* Set the session active or inactive. Note that activating an audio session is a synchronous (blocking) operation.
- Therefore, we recommend that applications not activate their session from a thread where a long blocking operation will be problematic.
- Note that this method will throw an exception in apps linked on or after iOS 8 if the session is set inactive while it has running or 
- paused I/O (e.g. audio queues, players, recorders, converters, remote I/Os, etc.).
-*/
-- (BOOL)setActive:(BOOL)active error:(NSError **)outError;
-- (BOOL)setActive:(BOOL)active withOptions:(AVAudioSessionSetActiveOptions)options error:(NSError **)outError NS_AVAILABLE_IOS(6_0);
-
-// Get the list of categories available on the device.  Certain categories may be unavailable on particular devices.  For example,
-// AVAudioSessionCategoryRecord will not be available on devices that have no support for audio input.
-@property(readonly) NSArray<NSString *> *availableCategories NS_AVAILABLE_IOS(9_0);
-
-/* set session category */
-- (BOOL)setCategory:(NSString *)category error:(NSError **)outError;
-/* set session category with options */
-- (BOOL)setCategory:(NSString *)category withOptions:(AVAudioSessionCategoryOptions)options error:(NSError **)outError NS_AVAILABLE_IOS(6_0);
-
-/* get session category. Examples: AVAudioSessionCategoryRecord, AVAudioSessionCategoryPlayAndRecord, etc. */
-@property(readonly) NSString *category;
-
-/* Returns an enum indicating whether the user has granted or denied permission to record, or has not been asked */
-- (AVAudioSessionRecordPermission)recordPermission NS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED;
-
-/* Checks to see if calling process has permission to record audio.  The 'response' block will be called
- immediately if permission has already been granted or denied.  Otherwise, it presents a dialog to notify
- the user and allow them to choose, and calls the block once the UI has been dismissed.  'granted'
- indicates whether permission has been granted.
- */
-typedef void (^PermissionBlock)(BOOL granted);
-
-- (void)requestRecordPermission:(PermissionBlock)response NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
-
-/* get the current set of AVAudioSessionCategoryOptions */
-@property(readonly) AVAudioSessionCategoryOptions categoryOptions NS_AVAILABLE_IOS(6_0);
-
-// Modes modify the audio category in order to introduce behavior that is tailored to the specific
-// use of audio within an application. Examples:  AVAudioSessionModeVideoRecording, AVAudioSessionModeVoiceChat,
-// AVAudioSessionModeMeasurement, etc.
-
-// Get the list of modes available on the device.  Certain modes may be unavailable on particular devices.  For example,
-// AVAudioSessionModeVideoRecording will not be available on devices that have no support for recording video.
-@property(readonly) NSArray<NSString *> *availableModes NS_AVAILABLE_IOS(9_0);
-
-- (BOOL)setMode:(NSString *)mode error:(NSError **)outError NS_AVAILABLE_IOS(5_0); /* set session mode */
-@property(readonly) NSString *mode NS_AVAILABLE_IOS(5_0); /* get session mode */
-
-- (BOOL)overrideOutputAudioPort:(AVAudioSessionPortOverride)portOverride  error:(NSError **)outError NS_AVAILABLE_IOS(6_0);
-
-/* Will be true when another application is playing audio.
-Note: As of iOS 8.0, Apple recommends that most applications use secondaryAudioShouldBeSilencedHint instead of this property.
-The otherAudioPlaying property will be true if any other audio (including audio from an app using AVAudioSessionCategoryAmbient)
-is playing, whereas the secondaryAudioShouldBeSilencedHint property is more restrictive in its consideration of whether 
-primary audio from another application is playing.  
-*/
-@property(readonly, getter=isOtherAudioPlaying) BOOL otherAudioPlaying  NS_AVAILABLE_IOS(6_0);
-
-/* Will be true when another application with a non-mixable audio session is playing audio.  Applications may use
-this property as a hint to silence audio that is secondary to the functionality of the application. For example, a game app
-using AVAudioSessionCategoryAmbient may use this property to decide to mute its soundtrack while leaving its sound effects unmuted.
-Note: This property is closely related to AVAudioSessionSilenceSecondaryAudioHintNotification.
-*/
-@property(readonly) BOOL secondaryAudioShouldBeSilencedHint  NS_AVAILABLE_IOS(8_0);
-
-/* A description of the current route, consisting of zero or more input ports and zero or more output ports */
-@property(readonly) AVAudioSessionRouteDescription *currentRoute NS_AVAILABLE_IOS(6_0);
-
-
-/* Select a preferred input port for audio routing. If the input port is already part of the current audio route, this will have no effect.
-   Otherwise, selecting an input port for routing will initiate a route change to use the preferred input port, provided that the application's
-   session controls audio routing. Setting a nil value will clear the preference. */
-- (BOOL)setPreferredInput:(nullable AVAudioSessionPortDescription *)inPort error:(NSError **)outError NS_AVAILABLE_IOS(7_0);
-@property(readonly, nullable) AVAudioSessionPortDescription * preferredInput NS_AVAILABLE_IOS(7_0); /* Get the preferred input port.  Will be nil if no preference has been set */
-
-/* Get the set of input ports that are available for routing. Note that this property only applies to the session's current category and mode.
-   For example, if the session's current category is AVAudioSessionCategoryPlayback, there will be no available inputs.  */
-@property(readonly, nullable) NSArray<AVAudioSessionPortDescription *> * availableInputs NS_AVAILABLE_IOS(7_0);
-
-@end
-
-
-/* AVAudioSessionHardwareConfiguration manages the set of properties that reflect the current state of
- audio hardware in the current route.  Applications whose functionality depends on these properties should
- reevaluate them any time the route changes. */
-@interface AVAudioSession (AVAudioSessionHardwareConfiguration)
-
-/* Get and set preferred values for hardware properties.  Note: that there are corresponding read-only
- properties that describe the actual values for sample rate, I/O buffer duration, etc. */
-
-	/* The preferred hardware sample rate for the session. The actual sample rate may be different. */
-- (BOOL)setPreferredSampleRate:(double)sampleRate  error:(NSError **)outError NS_AVAILABLE_IOS(6_0);
-@property(readonly) double preferredSampleRate NS_AVAILABLE_IOS(6_0);
-
-	/* The preferred hardware IO buffer duration in seconds. The actual IO buffer duration may be different.  */
-- (BOOL)setPreferredIOBufferDuration:(NSTimeInterval)duration error:(NSError **)outError;
-@property(readonly) NSTimeInterval preferredIOBufferDuration;
-
-	/* Sets the number of input channels that the app would prefer for the current route */
-- (BOOL)setPreferredInputNumberOfChannels:(NSInteger)count error:(NSError **)outError NS_AVAILABLE_IOS(7_0);
-@property(readonly) NSInteger preferredInputNumberOfChannels NS_AVAILABLE_IOS(7_0);
-
-	/* Sets the number of output channels that the app would prefer for the current route */
-- (BOOL)setPreferredOutputNumberOfChannels:(NSInteger)count error:(NSError **)outError NS_AVAILABLE_IOS(7_0);
-@property(readonly) NSInteger preferredOutputNumberOfChannels NS_AVAILABLE_IOS(7_0);
-
-
-/* Returns the largest number of audio input channels available for the current route */
-@property (readonly) NSInteger	maximumInputNumberOfChannels NS_AVAILABLE_IOS(7_0);
-
-/* Returns the largest number of audio output channels available for the current route */
-@property (readonly) NSInteger	maximumOutputNumberOfChannels NS_AVAILABLE_IOS(7_0);
-
-/* A value defined over the range [0.0, 1.0], with 0.0 corresponding to the lowest analog
-gain setting and 1.0 corresponding to the highest analog gain setting.  Attempting to set values
-outside of the defined range will result in the value being "clamped" to a valid input.  This is
-a global input gain setting that applies to the current input source for the entire system.
-When no applications are using the input gain control, the system will restore the default input
-gain setting for the input source.  Note that some audio accessories, such as USB devices, may
-not have a default value.  This property is only valid if inputGainSettable
-is true.  Note: inputGain is key-value observable */
-- (BOOL)setInputGain:(float)gain  error:(NSError **)outError NS_AVAILABLE_IOS(6_0);
-@property(readonly) float inputGain NS_AVAILABLE_IOS(6_0); /* value in range [0.0, 1.0] */
-
-/* True when audio input gain is available.  Some input ports may not provide the ability to set the
-input gain, so check this value before attempting to set input gain. */
-@property(readonly, getter=isInputGainSettable) BOOL inputGainSettable  NS_AVAILABLE_IOS(6_0);
-
-/* True if input hardware is available. */
-@property(readonly, getter=isInputAvailable) BOOL inputAvailable  NS_AVAILABLE_IOS(6_0);
-
-/* DataSource methods are for use with routes that support input or output data source selection.
-If the attached accessory supports data source selection, the data source properties/methods provide for discovery and 
-selection of input and/or output data sources. Note that the properties and methods for data source selection below are
-equivalent to the properties and methods on AVAudioSessionPortDescription. The methods below only apply to the currently 
-routed ports. */
-
-/* Key-value observable. */
-@property(readonly, nullable) NSArray<AVAudioSessionDataSourceDescription *> * inputDataSources NS_AVAILABLE_IOS(6_0);
-
-/* Get and set the currently selected data source.  Will be nil if no data sources are available.
-Setting a nil value will clear the data source preference. */
-@property(readonly, nullable) AVAudioSessionDataSourceDescription *inputDataSource NS_AVAILABLE_IOS(6_0);
-- (BOOL)setInputDataSource:(nullable AVAudioSessionDataSourceDescription *)dataSource error:(NSError **)outError NS_AVAILABLE_IOS(6_0);
-
-/* Key-value observable. */
-@property(readonly, nullable) NSArray<AVAudioSessionDataSourceDescription *> * outputDataSources NS_AVAILABLE_IOS(6_0);
-
-/* Get and set currently selected data source.  Will be nil if no data sources are available. 
-Setting a nil value will clear the data source preference. */
-@property(readonly, nullable) AVAudioSessionDataSourceDescription *outputDataSource NS_AVAILABLE_IOS(6_0);
-- (BOOL)setOutputDataSource:(nullable AVAudioSessionDataSourceDescription *)dataSource error:(NSError **)outError NS_AVAILABLE_IOS(6_0);
-
-
-/* Current values for hardware properties.  Note that most of these properties have corresponding methods 
-for getting and setting preferred values.  Input- and output-specific properties will generate an error if they are 
-queried if the audio session category does not support them.  Each of these will return 0 (or 0.0) if there is an error.  */
-
-	/* The current hardware sample rate */
-@property(readonly) double sampleRate NS_AVAILABLE_IOS(6_0);
-
-	/* The current number of hardware input channels. Is key-value observable */
-@property(readonly) NSInteger inputNumberOfChannels NS_AVAILABLE_IOS(6_0);
-
-	/* The current number of hardware output channels. Is key-value observable */
-@property(readonly) NSInteger outputNumberOfChannels NS_AVAILABLE_IOS(6_0);
-
-	/* The current output volume. Is key-value observable */
-@property(readonly) float outputVolume  NS_AVAILABLE_IOS(6_0); /* value in range [0.0, 1.0] */
-
-	/* The current hardware input latency in seconds. */
-@property(readonly) NSTimeInterval inputLatency  NS_AVAILABLE_IOS(6_0);
-
-	/* The current hardware output latency in seconds. */
-@property(readonly) NSTimeInterval outputLatency  NS_AVAILABLE_IOS(6_0);
-
-	/* The current hardware IO buffer duration in seconds. */
-@property(readonly) NSTimeInterval IOBufferDuration  NS_AVAILABLE_IOS(6_0);
-
-@end
-
-@interface AVAudioSession (AVAudioSessionDeprecated)
-
-/* The delegate property is deprecated. Instead, you should register for the NSNotifications named below. */
-/* For example: 
- [[NSNotificationCenter defaultCenter] addObserver: myObject 
- selector:    @selector(handleInterruption:) 
- name:        AVAudioSessionInterruptionNotification 
- object:      [AVAudioSession sharedInstance]]; 
- */
-@property(assign, nullable) id<AVAudioSessionDelegate> delegate NS_DEPRECATED_IOS(4_0, 6_0) __TVOS_PROHIBITED;
-
-
-- (BOOL)setActive:(BOOL)active withFlags:(NSInteger)flags error:(NSError **)outError NS_DEPRECATED_IOS(4_0, 6_0) __TVOS_PROHIBITED;
-
-@property(readonly) BOOL inputIsAvailable NS_DEPRECATED_IOS(3_0, 6_0) __TVOS_PROHIBITED; /* is input hardware available or not? */
-
-/* deprecated.  Use the corresponding properties without "Hardware" in their names. */
-@property(readonly) double currentHardwareSampleRate NS_DEPRECATED_IOS(3_0, 6_0) __TVOS_PROHIBITED;
-@property(readonly) NSInteger currentHardwareInputNumberOfChannels NS_DEPRECATED_IOS(3_0, 6_0) __TVOS_PROHIBITED;
-@property(readonly) NSInteger currentHardwareOutputNumberOfChannels NS_DEPRECATED_IOS(3_0, 6_0) __TVOS_PROHIBITED;
-- (BOOL)setPreferredHardwareSampleRate:(double)sampleRate error:(NSError **)outError NS_DEPRECATED_IOS(3_0, 6_0) __TVOS_PROHIBITED;
-@property(readonly) double preferredHardwareSampleRate NS_DEPRECATED_IOS(3_0, 6_0) __TVOS_PROHIBITED;
-
-@end
-
-#pragma mark -- Names for NSNotifications --
-
-/* Registered listeners will be notified when the system has interrupted the audio session and when
- the interruption has ended.  Check the notification's userInfo dictionary for the interruption type -- either begin or end.
- In the case of an end interruption notification, check the userInfo dictionary for AVAudioSessionInterruptionOptions that
- indicate whether audio playback should resume.
- */
-AVF_EXPORT NSString *const AVAudioSessionInterruptionNotification NS_AVAILABLE_IOS(6_0);
-
-/* Registered listeners will be notified when a route change has occurred.  Check the notification's userInfo dictionary for the
- route change reason and for a description of the previous audio route.
- */
-AVF_EXPORT NSString *const AVAudioSessionRouteChangeNotification NS_AVAILABLE_IOS(6_0);
-
-/* Registered listeners will be notified if the media server is killed.  In the event that the server is killed,
- take appropriate steps to handle requests that come in before the server resets.  See Technical Q&A QA1749.
- */
-AVF_EXPORT NSString *const AVAudioSessionMediaServicesWereLostNotification NS_AVAILABLE_IOS(7_0);
-
-/* Registered listeners will be notified when the media server restarts.  In the event that the server restarts,
- take appropriate steps to re-initialize any audio objects used by your application.  See Technical Q&A QA1749.
- */
-AVF_EXPORT NSString *const AVAudioSessionMediaServicesWereResetNotification NS_AVAILABLE_IOS(6_0);
-
-/* Registered listeners that are currently in the foreground and have active audio sessions will be notified 
- when primary audio from other applications starts and stops.  Check the notification's userInfo dictionary 
- for the notification type -- either begin or end.
- Foreground applications may use this notification as a hint to enable or disable audio that is secondary
- to the functionality of the application. For more information, see the related property secondaryAudioShouldBeSilencedHint.
-*/
-AVF_EXPORT NSString *const AVAudioSessionSilenceSecondaryAudioHintNotification NS_AVAILABLE_IOS(8_0);
-
-#pragma mark -- Keys for NSNotification userInfo dictionaries --
-
-/* keys for AVAudioSessionInterruptionNotification */
-	/* value is an NSNumber representing an AVAudioSessionInterruptionType */
-AVF_EXPORT NSString *const AVAudioSessionInterruptionTypeKey NS_AVAILABLE_IOS(6_0);
-	/* Only present for end interruption events.  Value is of type AVAudioSessionInterruptionOptions.*/
-AVF_EXPORT NSString *const AVAudioSessionInterruptionOptionKey NS_AVAILABLE_IOS(6_0);
-	
-/* keys for AVAudioSessionRouteChangeNotification */
-	/* value is an NSNumber representing an AVAudioSessionRouteChangeReason */
-AVF_EXPORT NSString *const AVAudioSessionRouteChangeReasonKey NS_AVAILABLE_IOS(6_0);
-	/* value is AVAudioSessionRouteDescription * */
-AVF_EXPORT NSString *const AVAudioSessionRouteChangePreviousRouteKey NS_AVAILABLE_IOS(6_0);
-
-/* keys for AVAudioSessionSilenceSecondaryAudioHintNotification */
-/* value is an NSNumber representing an AVAudioSessionSilenceSecondaryAudioHintType */
-AVF_EXPORT NSString *const AVAudioSessionSilenceSecondaryAudioHintTypeKey NS_AVAILABLE_IOS(8_0);
-
-#pragma mark -- Values for the category property --
-
-/*  Use this category for background sounds such as rain, car engine noise, etc.  
- Mixes with other music. */
-AVF_EXPORT NSString *const AVAudioSessionCategoryAmbient;
-	
-/*  Use this category for background sounds.  Other music will stop playing. */
-AVF_EXPORT NSString *const AVAudioSessionCategorySoloAmbient;
-
-/* Use this category for music tracks.*/
-AVF_EXPORT NSString *const AVAudioSessionCategoryPlayback;
-
-/*  Use this category when recording audio. */
-AVF_EXPORT NSString *const AVAudioSessionCategoryRecord;
-
-/*  Use this category when recording and playing back audio. */
-AVF_EXPORT NSString *const AVAudioSessionCategoryPlayAndRecord;
-
-/*  Use this category when using a hardware codec or signal processor while
- not playing or recording audio. */
-AVF_EXPORT NSString *const AVAudioSessionCategoryAudioProcessing __TVOS_PROHIBITED;
-
-/*  Use this category to customize the usage of available audio accessories and built-in audio hardware.
- For example, this category provides an application with the ability to use an available USB output 
- and headphone output simultaneously for separate, distinct streams of audio data. Use of 
- this category by an application requires a more detailed knowledge of, and interaction with, 
- the capabilities of the available audio routes.  May be used for input, output, or both.
- Note that not all output types and output combinations are eligible for multi-route.  Input is limited
- to the last-in input port. Eligible inputs consist of the following:
-	AVAudioSessionPortUSBAudio, AVAudioSessionPortHeadsetMic, and AVAudioSessionPortBuiltInMic.  
- Eligible outputs consist of the following: 
-	AVAudioSessionPortUSBAudio, AVAudioSessionPortLineOut, AVAudioSessionPortHeadphones, AVAudioSessionPortHDMI, 
-	and AVAudioSessionPortBuiltInSpeaker.  
- Note that AVAudioSessionPortBuiltInSpeaker is only allowed to be used when there are no other eligible 
- outputs connected.  */
-AVF_EXPORT NSString *const AVAudioSessionCategoryMultiRoute NS_AVAILABLE_IOS(6_0);
-
-#pragma mark -- Values for the mode property --
-
-/*!
-@abstract      Modes modify the audio category in order to introduce behavior that is tailored to the specific
-use of audio within an application.  Available in iOS 5.0 and greater.
- */
-
-/* The default mode */
-AVF_EXPORT NSString *const AVAudioSessionModeDefault NS_AVAILABLE_IOS(5_0);
-
-/* Only valid with AVAudioSessionCategoryPlayAndRecord.  Appropriate for Voice over IP
-(VoIP) applications.  Reduces the number of allowable audio routes to be only those
-that are appropriate for VoIP applications and may engage appropriate system-supplied
-signal processing.  Has the side effect of setting AVAudioSessionCategoryOptionAllowBluetooth */
-AVF_EXPORT NSString *const AVAudioSessionModeVoiceChat NS_AVAILABLE_IOS(5_0);
-
-/* Set by Game Kit on behalf of an application that uses a GKVoiceChat object; valid
- only with the AVAudioSessionCategoryPlayAndRecord category.
- Do not set this mode directly. If you need similar behavior and are not using
- a GKVoiceChat object, use AVAudioSessionModeVoiceChat instead. */
-AVF_EXPORT NSString *const AVAudioSessionModeGameChat NS_AVAILABLE_IOS(5_0);
-
-/* Only valid with AVAudioSessionCategoryPlayAndRecord or AVAudioSessionCategoryRecord.
- Modifies the audio routing options and may engage appropriate system-supplied signal processing. */
-AVF_EXPORT NSString *const AVAudioSessionModeVideoRecording NS_AVAILABLE_IOS(5_0);
-
-/* Appropriate for applications that wish to minimize the effect of system-supplied signal
-processing for input and/or output audio signals. */
-AVF_EXPORT NSString *const AVAudioSessionModeMeasurement NS_AVAILABLE_IOS(5_0);
-
-/* Engages appropriate output signal processing for movie playback scenarios.  Currently
-only applied during playback over built-in speaker. */
-AVF_EXPORT NSString *const AVAudioSessionModeMoviePlayback NS_AVAILABLE_IOS(6_0);
-
-/* Only valid with kAudioSessionCategory_PlayAndRecord. Reduces the number of allowable audio
-routes to be only those that are appropriate for video chat applications. May engage appropriate
-system-supplied signal processing.  Has the side effect of setting
-AVAudioSessionCategoryOptionAllowBluetooth and AVAudioSessionCategoryOptionDefaultToSpeaker. */
-AVF_EXPORT NSString *const AVAudioSessionModeVideoChat NS_AVAILABLE_IOS(7_0);
-
-/* Appropriate for applications which play spoken audio and wish to be paused (via audio session interruption) rather than ducked
-if another app (such as a navigation app) plays a spoken audio prompt.  Examples of apps that would use this are podcast players and
-audio books.  For more information, see the related category option AVAudioSessionCategoryOptionInterruptSpokenAudioAndMixWithOthers. */
-AVF_EXPORT NSString *const AVAudioSessionModeSpokenAudio NS_AVAILABLE_IOS(9_0);
-
-#pragma mark -- constants for port types --
-
-/* input port types */
-AVF_EXPORT NSString *const AVAudioSessionPortLineIn       NS_AVAILABLE_IOS(6_0); /* Line level input on a dock connector */
-AVF_EXPORT NSString *const AVAudioSessionPortBuiltInMic   NS_AVAILABLE_IOS(6_0); /* Built-in microphone on an iOS device */
-AVF_EXPORT NSString *const AVAudioSessionPortHeadsetMic   NS_AVAILABLE_IOS(6_0); /* Microphone on a wired headset.  Headset refers to an
-																				   accessory that has headphone outputs paired with a
-																				   microphone. */
-
-/* output port types */
-AVF_EXPORT NSString *const AVAudioSessionPortLineOut          NS_AVAILABLE_IOS(6_0); /* Line level output on a dock connector */
-AVF_EXPORT NSString *const AVAudioSessionPortHeadphones       NS_AVAILABLE_IOS(6_0); /* Headphone or headset output */
-AVF_EXPORT NSString *const AVAudioSessionPortBluetoothA2DP    NS_AVAILABLE_IOS(6_0); /* Output on a Bluetooth A2DP device */
-AVF_EXPORT NSString *const AVAudioSessionPortBuiltInReceiver  NS_AVAILABLE_IOS(6_0); /* The speaker you hold to your ear when on a phone call */
-AVF_EXPORT NSString *const AVAudioSessionPortBuiltInSpeaker   NS_AVAILABLE_IOS(6_0); /* Built-in speaker on an iOS device */
-AVF_EXPORT NSString *const AVAudioSessionPortHDMI             NS_AVAILABLE_IOS(6_0); /* Output via High-Definition Multimedia Interface */
-AVF_EXPORT NSString *const AVAudioSessionPortAirPlay          NS_AVAILABLE_IOS(6_0); /* Output on a remote Air Play device */
-AVF_EXPORT NSString *const AVAudioSessionPortBluetoothLE	  NS_AVAILABLE_IOS(7_0); /* Output on a Bluetooth Low Energy device */
-
-/* port types that refer to either input or output */
-AVF_EXPORT NSString *const AVAudioSessionPortBluetoothHFP NS_AVAILABLE_IOS(6_0); /* Input or output on a Bluetooth Hands-Free Profile device */
-AVF_EXPORT NSString *const AVAudioSessionPortUSBAudio     NS_AVAILABLE_IOS(6_0); /* Input or output on a Universal Serial Bus device */
-AVF_EXPORT NSString *const AVAudioSessionPortCarAudio     NS_AVAILABLE_IOS(7_0); /* Input or output via Car Audio */
-
-#pragma mark -- constants for data source locations, orientations, polar patterns, and channel roles --
-
-/* The following represent the location of a data source on an iOS device. */
-AVF_EXPORT NSString *const AVAudioSessionLocationUpper					NS_AVAILABLE_IOS(7_0);
-AVF_EXPORT NSString *const AVAudioSessionLocationLower					NS_AVAILABLE_IOS(7_0);
-
-/* The following represent the orientation or directionality of a data source on an iOS device. */
-AVF_EXPORT NSString *const AVAudioSessionOrientationTop					NS_AVAILABLE_IOS(7_0);
-AVF_EXPORT NSString *const AVAudioSessionOrientationBottom				NS_AVAILABLE_IOS(7_0);
-AVF_EXPORT NSString *const AVAudioSessionOrientationFront				NS_AVAILABLE_IOS(7_0);
-AVF_EXPORT NSString *const AVAudioSessionOrientationBack				NS_AVAILABLE_IOS(7_0);
-AVF_EXPORT NSString *const AVAudioSessionOrientationLeft				NS_AVAILABLE_IOS(8_0);
-AVF_EXPORT NSString *const AVAudioSessionOrientationRight				NS_AVAILABLE_IOS(8_0);
-
-/* The following represent the possible polar patterns for a data source on an iOS device. */
-AVF_EXPORT NSString *const AVAudioSessionPolarPatternOmnidirectional	NS_AVAILABLE_IOS(7_0);
-AVF_EXPORT NSString *const AVAudioSessionPolarPatternCardioid			NS_AVAILABLE_IOS(7_0);
-AVF_EXPORT NSString *const AVAudioSessionPolarPatternSubcardioid		NS_AVAILABLE_IOS(7_0);
-
-#pragma mark -- helper class interfaces --
-
-/* 
- AVAudioSessionChannelDescription objects provide information about a port's audio channels.
- AudioQueues, AURemoteIO and AUVoiceIO instances can be assigned to communicate with specific 
- hardware channels by setting an array of <port UID, channel index> pairs.
- */
-NS_CLASS_AVAILABLE(NA, 6_0)
-@interface AVAudioSessionChannelDescription : NSObject {
-@private
-    void *_impl;
-}
-
-@property(readonly) NSString *			channelName;
-@property(readonly) NSString *			owningPortUID;  /* the unique identifier (UID) for the channel's owning port */
-@property(readonly) NSUInteger			channelNumber;  /* the index of this channel in its owning port's array of channels */
-@property(readonly) AudioChannelLabel	channelLabel;	/* description of the physical location of this channel.   */
-
-@end
-
-NS_CLASS_AVAILABLE(NA, 6_0)
-@interface AVAudioSessionPortDescription : NSObject {
-@private
-    void * _impl;
-}
-
-/* Value is one of the AVAudioSessionPort constants declared above. */
-@property(readonly) NSString *portType;
-
-/* A descriptive name for the port */
-@property(readonly) NSString *portName;
-
-/* A system-assigned unique identifier for the port */
-@property(readonly) NSString *UID;
-
-@property(readonly, nullable) NSArray<AVAudioSessionChannelDescription *> *	channels;
-
-/* Will be nil if there are no selectable data sources. */
-@property(readonly, nullable) NSArray<AVAudioSessionDataSourceDescription *> *	dataSources NS_AVAILABLE_IOS(7_0);
-
-/* Will be nil if there are no selectable data sources. In all other cases, this
- property reflects the currently selected data source.*/
-@property(readonly, nullable) AVAudioSessionDataSourceDescription *selectedDataSource NS_AVAILABLE_IOS(7_0);
-
-/* This property reflects the application's preferred data source for the Port.
- Will be nil if there are no selectable data sources or if no preference has been set.*/
-@property(readonly, nullable) AVAudioSessionDataSourceDescription *preferredDataSource NS_AVAILABLE_IOS(7_0);
-
-/* Select the preferred data source for this port. The input dataSource parameter must be one of the dataSources exposed by 
-the dataSources property. Setting a nil value will clear the preference.
-Note: if the port is part of the active audio route, changing the data source will likely
-result in a route reconfiguration.  If the port is not part of the active route, selecting a new data source will
-not result in an immediate route reconfiguration.  Use AVAudioSession's setPreferredInput:error: method to activate the port. */
-- (BOOL)setPreferredDataSource:(nullable AVAudioSessionDataSourceDescription *)dataSource error:(NSError **)outError NS_AVAILABLE_IOS(7_0);
-
-@end
-
-NS_CLASS_AVAILABLE(NA, 6_0)
-@interface AVAudioSessionRouteDescription : NSObject {
-@private
-    void * _impl;
-}
-
-@property(readonly) NSArray<AVAudioSessionPortDescription *> * inputs;
-
-@property(readonly) NSArray<AVAudioSessionPortDescription *> * outputs;
-@end
-
-NS_CLASS_AVAILABLE(NA, 6_0)
-@interface AVAudioSessionDataSourceDescription : NSObject {
-@private
-    void * _impl;
-}
-
-/* system-assigned ID for the data source */
-@property(readonly) NSNumber *dataSourceID;
-
-/* human-readable name for the data source */
-@property(readonly) NSString *dataSourceName;
-
-/* Location and orientation can be used to distinguish between multiple data sources belonging to a single port.  For example, in the case of a port of type AVAudioSessionPortBuiltInMic, one can
-   use these properties to differentiate between an upper/front-facing microphone and a lower/bottom-facing microphone. */
-
-/* Describes the general location of a data source. Will be nil for data sources for which the location is not known. */
-@property(readonly, nullable) NSString *	location NS_AVAILABLE_IOS(7_0);
-
-/* Describes the orientation of a data source.  Will be nil for data sources for which the orientation is not known. */
-@property(readonly, nullable) NSString *	orientation NS_AVAILABLE_IOS(7_0);
-
-/* Array of one or more NSStrings describing the supported polar patterns for a data source.  Will be nil for data sources that have no selectable patterns. */
-@property(readonly, nullable) NSArray<NSString *> *	supportedPolarPatterns NS_AVAILABLE_IOS(7_0);
-
-/* Describes the currently selected polar pattern.  Will be nil for data sources that have no selectable patterns. */
-@property(readonly, nullable) NSString *	selectedPolarPattern NS_AVAILABLE_IOS(7_0);
-
-/* Describes the preferred polar pattern.  Will be nil for data sources that have no selectable patterns or if no preference has been set. */
-@property(readonly, nullable) NSString *	preferredPolarPattern NS_AVAILABLE_IOS(7_0);
-
-/* Select the desired polar pattern from the set of available patterns. Setting a nil value will clear the preference.
-   Note: if the owning port and data source are part of the active audio route,
-   changing the polar pattern will likely result in a route reconfiguration. If the owning port and data source are not part of the active route,
-   selecting a polar pattern will not result in an immediate route reconfiguration.  Use AVAudioSession's setPreferredInput:error: method
-   to activate the port. Use setPreferredDataSource:error: to active the data source on the port. */
-- (BOOL)setPreferredPolarPattern:(nullable NSString *)pattern error:(NSError **)outError NS_AVAILABLE_IOS(7_0);
-
-@end
-
-
-#pragma mark -- AVAudioSessionDelegate protocol --
-/* The AVAudioSessionDelegate protocol is deprecated. Instead you should register for notifications. */
-__TVOS_PROHIBITED
-@protocol AVAudioSessionDelegate <NSObject>
-@optional 
-
-- (void)beginInterruption; /* something has caused your audio session to be interrupted */
-
-/* the interruption is over */
-- (void)endInterruptionWithFlags:(NSUInteger)flags NS_AVAILABLE_IOS(4_0); /* Currently the only flag is AVAudioSessionInterruptionFlags_ShouldResume. */
-		
-- (void)endInterruption; /* endInterruptionWithFlags: will be called instead if implemented. */
-
-/* notification for input become available or unavailable */
-- (void)inputIsAvailableChanged:(BOOL)isInputAvailable;
-
-@end
-
-
-#pragma mark -- Deprecated enumerations --
-
-/* Deprecated in iOS 6.0.  Use AVAudioSessionInterruptionOptions instead.
- Flags passed to you when endInterruptionWithFlags: is called on the delegate */
-enum {
-	AVAudioSessionInterruptionFlags_ShouldResume = 1
-} NS_DEPRECATED_IOS(4_0, 6_0) __TVOS_PROHIBITED;
-
-/* Deprecated in iOS 6.0.  Use AVAudioSessionSetActiveOptions instead.
- flags for use when calling setActive:withFlags:error: */
-enum {	
-	AVAudioSessionSetActiveFlags_NotifyOthersOnDeactivation = 1
-} NS_DEPRECATED_IOS(4_0, 6_0) __TVOS_PROHIBITED;
+#import <AVFAudio/AVAudioSession.h>
 
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioSettings.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioSettings.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioSettings.h	2015-09-30 23:17:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioSettings.h	2016-05-25 07:19:42.000000000 +0200
@@ -1,67 +1,9 @@
 /*
-	File:  AVAudioSettings.h
+	File:           AVAudioSettings.h
+	Framework:      AVFoundation
 	
-	Framework:  AVFoundation
-	
-	Copyright 2008-2013 Apple Inc. All rights reserved.
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVBase.h>
-#import <Foundation/NSObject.h>
-#import <Availability.h>
-
-/* This file's methods are available with iPhone 3.0 or later */
-
-/* property keys - values for all keys defined below are NSNumbers */
-
-/* keys for all formats */
-AVF_EXPORT NSString *const AVFormatIDKey;								/* value is an integer (format ID) from CoreAudioTypes.h */
-AVF_EXPORT NSString *const AVSampleRateKey;								/* value is floating point in Hertz */
-AVF_EXPORT NSString *const AVNumberOfChannelsKey;						/* value is an integer */
-
-/* linear PCM keys */
-AVF_EXPORT NSString *const AVLinearPCMBitDepthKey;						/* value is an integer, one of: 8, 16, 24, 32 */
-AVF_EXPORT NSString *const AVLinearPCMIsBigEndianKey;					/* value is a BOOL */
-AVF_EXPORT NSString *const AVLinearPCMIsFloatKey;						/* value is a BOOL */
-
-AVF_EXPORT NSString *const AVLinearPCMIsNonInterleaved                  NS_AVAILABLE(10_7, 4_0);   /* value is a BOOL */
-#define AVLinearPCMIsNonInterleavedKey AVLinearPCMIsNonInterleaved
-
-/* encoder property keys */
-AVF_EXPORT NSString *const AVEncoderAudioQualityKey;					/* value is an integer from enum AVAudioQuality */
-AVF_EXPORT NSString *const AVEncoderAudioQualityForVBRKey               NS_AVAILABLE(10_9, 7_0); /* value is an integer from enum AVAudioQuality. only relevant for AVAudioBitRateStrategy_Variable */
-
-	/* only one of AVEncoderBitRateKey and AVEncoderBitRatePerChannelKey should be provided. */
-AVF_EXPORT NSString *const AVEncoderBitRateKey;           				/* value is an integer. */
-AVF_EXPORT NSString *const AVEncoderBitRatePerChannelKey                NS_AVAILABLE(10_7, 4_0); /* value is an integer */
-AVF_EXPORT NSString *const AVEncoderBitRateStrategyKey                  NS_AVAILABLE(10_9, 7_0); /* value is an AVAudioBitRateStrategy constant. see below. */
-AVF_EXPORT NSString *const AVEncoderBitDepthHintKey;					/* value is an integer from 8 to 32 */
-
-/* sample rate converter property keys */
-AVF_EXPORT NSString *const AVSampleRateConverterAlgorithmKey NS_AVAILABLE(10_9, 7_0); /* value is an AVSampleRateConverterAlgorithm constant. see below. */
-AVF_EXPORT NSString *const AVSampleRateConverterAudioQualityKey;		/* value is an integer from enum AVAudioQuality */
-
-/* channel layout */
-AVF_EXPORT NSString *const AVChannelLayoutKey NS_AVAILABLE(10_7, 4_0);	/* value is an NSData containing an AudioChannelLayout */
-
-
-/* property values */
-
-/* values for AVEncoderBitRateStrategyKey */
-AVF_EXPORT NSString *const AVAudioBitRateStrategy_Constant              NS_AVAILABLE(10_9, 7_0);
-AVF_EXPORT NSString *const AVAudioBitRateStrategy_LongTermAverage       NS_AVAILABLE(10_9, 7_0);
-AVF_EXPORT NSString *const AVAudioBitRateStrategy_VariableConstrained   NS_AVAILABLE(10_9, 7_0);
-AVF_EXPORT NSString *const AVAudioBitRateStrategy_Variable              NS_AVAILABLE(10_9, 7_0);
-
-/* values for AVSampleRateConverterAlgorithmKey */
-AVF_EXPORT NSString *const AVSampleRateConverterAlgorithm_Normal        NS_AVAILABLE(10_9, 7_0);
-AVF_EXPORT NSString *const AVSampleRateConverterAlgorithm_Mastering     NS_AVAILABLE(10_9, 7_0);
-
-typedef NS_ENUM(NSInteger, AVAudioQuality) {
-	AVAudioQualityMin    = 0,
-	AVAudioQualityLow    = 0x20,
-	AVAudioQualityMedium = 0x40,
-	AVAudioQualityHigh   = 0x60,
-	AVAudioQualityMax    = 0x7F
-};
+#import <AVFAudio/AVAudioSettings.h>
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioTime.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioTime.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioTime.h	2015-09-30 23:17:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioTime.h	2016-05-25 07:19:42.000000000 +0200
@@ -1,142 +1,9 @@
 /*
-	File:		AVAudioTime.h
-	Framework:	AVFoundation
+	File:           AVAudioTime.h
+	Framework:      AVFoundation
 	
-	Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioTypes.h>
+#import <AVFAudio/AVAudioTime.h>
 
-NS_ASSUME_NONNULL_BEGIN
-
-/*!
-	@class AVAudioTime
-	@abstract Represent a moment in time.
-	@discussion
-		AVAudioTime is used in AVAudioEngine to represent time. Instances are immutable.
-		
-		A single moment in time may be represented in two different ways:
-		1. mach_absolute_time(), the system's basic clock. Commonly referred to as "host time."
-		2. audio samples at a particular sample rate
-		
-		A single AVAudioTime instance may contain either or both representations; it might
-		represent only a sample time, only a host time, or both.
-		
-Rationale for using host time:
-[a] internally we are using AudioTimeStamp, which uses host time, and it seems silly to divide
-[b] it is consistent with a standard system timing service
-[c] we do provide conveniences to convert between host ticks and seconds (host time divided by
-	frequency) so client code wanting to do what should be straightforward time computations can at 
-	least not be cluttered by ugly multiplications and divisions by the host clock frequency.
-*/
-
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioTime : NSObject {
-@private
-	AudioTimeStamp _ats;
-	double _sampleRate;
-	void *_reserved;
-}
-
-/*!	@method initWithAudioTimeStamp:sampleRate:
-*/
-- (instancetype)initWithAudioTimeStamp: (const AudioTimeStamp *)ts sampleRate: (double)sampleRate;
-
-/*! @method initWithHostTime:
-*/
-- (instancetype)initWithHostTime:(uint64_t)hostTime;
-
-/*! @method initWithSampleTime:atRate:
-*/
-- (instancetype)initWithSampleTime:(AVAudioFramePosition)sampleTime atRate:(double)sampleRate;
-
-/*! @method initWithHostTime:sampleTime:atRate:
-*/
-- (instancetype)initWithHostTime:(uint64_t)hostTime sampleTime:(AVAudioFramePosition)sampleTime atRate:(double)sampleRate;
-
-/*! @method timeWithAudioTimeStamp:sampleRate:
-*/
-+ (instancetype)timeWithAudioTimeStamp: (const AudioTimeStamp *)ts sampleRate: (double)sampleRate;
-
-/*! @method timeWithHostTime:
-*/
-+ (instancetype)timeWithHostTime:(uint64_t)hostTime;
-
-/*! @method timeWithSampleTime:atRate:
-*/
-+ (instancetype)timeWithSampleTime:(AVAudioFramePosition)sampleTime atRate:(double)sampleRate;
-
-/*! @method timeWithHostTime:sampleTime:atRate:
-*/
-+ (instancetype)timeWithHostTime:(uint64_t)hostTime sampleTime:(AVAudioFramePosition)sampleTime atRate:(double)sampleRate;
-
-/*!	@method hostTimeForSeconds:
-	@abstract Convert seconds to host time.
-*/
-+ (uint64_t)hostTimeForSeconds:(NSTimeInterval)seconds;
-
-/*!	@method secondsForHostTime:
-	@abstract Convert host time to seconds.
-*/
-+ (NSTimeInterval)secondsForHostTime:(uint64_t)hostTime;
-
-/*!	@method extrapolateTimeFromAnchor:
-	@abstract Converts between host and sample time.
-	@param anchorTime
-		An AVAudioTime with a more complete AudioTimeStamp than that of the receiver (self).
-	@return
-		the extrapolated time
-	@discussion
-		If anchorTime is an AVAudioTime where both host time and sample time are valid,
-		and self is another timestamp where only one of the two is valid, this method
-		returns a new AVAudioTime copied from self and where any additional valid fields provided by
-		the anchor are also valid.
-
-<pre>
-// time0 has a valid audio sample representation, but no host time representation.
-AVAudioTime *time0 = [AVAudioTime timeWithSampleTime: 0.0 atRate: 44100.0];
-// anchor has a valid host time representation and sample time representation.
-AVAudioTime *anchor = [player playerTimeForNodeTime: player.lastRenderTime];
-// fill in valid host time representation
-AVAudioTime *fullTime0 = [time0 extrapolateTimeFromAnchor: anchor];
-</pre>
-*/
-- (AVAudioTime *)extrapolateTimeFromAnchor:(AVAudioTime *)anchorTime;
-
-
-/*! @property hostTimeValid
-	@abstract Whether the hostTime property is valid.
-*/
-@property (nonatomic, readonly, getter=isHostTimeValid) BOOL hostTimeValid;
-
-/*! @property hostTime
-	@abstract The host time.
-*/
-@property (nonatomic, readonly) uint64_t hostTime;
-
-/*! @property sampleTimeValid
-	@abstract Whether the sampleTime and sampleRate properties are valid.
-*/
-@property (nonatomic, readonly, getter=isSampleTimeValid) BOOL sampleTimeValid;
-
-/*!	@property sampleTime
-	@abstract The time as a number of audio samples, as tracked by the current audio device.
-*/
-@property (nonatomic, readonly) AVAudioFramePosition sampleTime;
-
-/*!	@property sampleRate
-	@abstract The sample rate at which sampleTime is being expressed.
-*/
-@property (nonatomic, readonly) double sampleRate;
-
-/*! @property audioTimeStamp
-	@abstract The time expressed as an AudioTimeStamp structure.
-	@discussion
-		This may be useful for compatibility with lower-level CoreAudio and AudioToolbox API's.
-*/
-@property (readonly, nonatomic) AudioTimeStamp audioTimeStamp;
-
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioTypes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioTypes.h	2015-09-30 23:17:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioTypes.h	2016-05-25 07:19:42.000000000 +0200
@@ -1,178 +1,9 @@
 /*
-	File:		AVAudioTypes.h
-	Framework:	AVFoundation
+	File:           AVAudioTypes.h
+	Framework:      AVFoundation
 	
-	Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#ifndef __AVAudioTypes_h__
-#define __AVAudioTypes_h__
-
-#import <Foundation/Foundation.h>
-#import <AVFoundation/AVBase.h>
-#import <CoreAudio/CoreAudioTypes.h>
-
-/*! @typedef AVAudioFramePosition
-	@abstract A position in an audio file or stream.
-*/
-typedef int64_t		AVAudioFramePosition;
-
-/*!	@typedef AVAudioFrameCount
-	@abstract A number of audio sample frames.
-	
-	@discussion
-		Rationale: making this a potentially larger-than-32-bit type like NSUInteger would open the
-		door to a large set of runtime failures due to underlying implementations' use of UInt32.
-		
-		TODO: Remove rationales.
-*/
-typedef uint32_t	AVAudioFrameCount;
-
-/*!	@typedef AVAudioPacketCount
-	@abstract A number of packets of compressed audio data.
-	
-	@discussion
-		Rationale: making this a potentially larger-than-32-bit type like NSUInteger would open the
-		door to a large set of runtime failures due to underlying implementations' use of UInt32.
-		
-		TODO: Remove rationales.
-*/
-typedef uint32_t	AVAudioPacketCount;
-
-/*!	@typedef AVAudioChannelCount
-	@abstract A number of audio channels.
-	
-	@discussion
-		Rationale: making this a potentially larger-than-32-bit type like NSUInteger would open the
-		door to a large set of runtime failures due to underlying implementations' use of UInt32.
-*/
-typedef uint32_t	AVAudioChannelCount;
-
-/*! @typedef AVAudioNodeCompletionHandler
-	@abstract Generic callback handler.
-	@discussion
-		Various AVAudioEngine objects issue callbacks to generic blocks of this type. In general
-		the callback arrives on a non-main thread and it is the client's responsibility to handle it
-		in a thread-safe manner.
-*/
-typedef void (^AVAudioNodeCompletionHandler)(void);
-
-/*!	@typedef AVAudioNodeBus
-	@abstract The index of a bus on an AVAudioNode.
-	@discussion
-		@link AVAudioNode @/link objects potentially have multiple input and/or output busses.
-		AVAudioNodeBus represents a bus as a zero-based index.
-*/
-typedef NSUInteger AVAudioNodeBus;
-
-
-
-/*=============================================================================*/
-/*!	@struct AVAudio3DPoint
-    @abstract Struct representing a point in 3D space
-    @discussion
-        This struct is used by classes dealing with 3D audio such as `AVAudioMixing`
-        and `AVAudioEnvironmentNode` and represents a point in 3D space.
-*/
-struct AVAudio3DPoint {
-    float x;
-    float y;
-    float z;
-};
-typedef struct AVAudio3DPoint AVAudio3DPoint;
-
-/*!	@method AVAudioMake3DPoint
-    @abstract Creates and returns an AVAudio3DPoint object
-*/
-NS_INLINE AVAudio3DPoint AVAudioMake3DPoint(float x, float y, float z) {
-    AVAudio3DPoint p;
-    p.x = x;
-    p.y = y;
-    p.z = z;
-    return p;
-}
-
-/*!	@typedef AVAudio3DVector
-    @abstract Struct representing a vector in 3D space
-    @discussion
-        This struct is used by classes dealing with 3D audio such as @link AVAudioMixing @/link
-        and @link AVAudioEnvironmentNode @/link and represents a vector in 3D space.
-*/
-typedef struct AVAudio3DPoint AVAudio3DVector;
-
-/*!	@method AVAudio3DVector
-    @abstract Creates and returns an AVAudio3DVector object
-*/
-NS_INLINE AVAudio3DVector AVAudioMake3DVector(float x, float y, float z) {
-    AVAudio3DVector v;
-    v.x = x;
-    v.y = y;
-    v.z = z;
-    return v;
-}
-
-/*!	@struct AVAudio3DVectorOrientation
-    @abstract Struct representing the orientation of the listener in 3D space
-    @discussion
-        Two orthogonal vectors describe the orientation of the listener. The forward
-        vector points in the direction that the listener is facing. The up vector is orthogonal
-        to the forward vector and points upwards from the listener's head.
-*/
-struct AVAudio3DVectorOrientation {
-    AVAudio3DVector forward;
-    AVAudio3DVector up;
-};
-typedef struct AVAudio3DVectorOrientation AVAudio3DVectorOrientation;
-
-/*!	@method AVAudioMake3DVectorOrientation
-    @abstract Creates and returns an AVAudio3DVectorOrientation object
-*/
-NS_INLINE AVAudio3DVectorOrientation AVAudioMake3DVectorOrientation(AVAudio3DVector forward, AVAudio3DVector up) {
-    AVAudio3DVectorOrientation o;
-    o.forward = forward;
-    o.up = up;
-    return o;
-}
-
-/*!	@struct AVAudio3DAngularOrientation
-    @abstract Struct representing the orientation of the listener in 3D space
-    @discussion
-        Three angles describe the orientation of a listener's head - yaw, pitch and roll.
- 
-        Yaw describes the side to side movement of the listener's head.
-        The yaw axis is perpendicular to the plane of the listener's ears with its origin at the 
-        center of the listener's head and directed towards the bottom of the listener's head. A 
-        positive yaw is in the clockwise direction going from 0 to 180 degrees. A negative yaw is in 
-        the counter-clockwise direction going from 0 to -180 degrees.
- 
-        Pitch describes the up-down movement of the listener's head.
-        The pitch axis is perpendicular to the yaw axis and is parallel to the plane of the 
-        listener's ears with its origin at the center of the listener's head and directed towards 
-        the right ear. A positive pitch is the upwards direction going from 0 to 180 degrees. A 
-        negative pitch is in the downwards direction going from 0 to -180 degrees.
- 
-        Roll describes the tilt of the listener's head.
-        The roll axis is perpendicular to the other two axes with its origin at the center of the 
-        listener's head and is directed towards the listener's nose. A positive roll is to the right 
-        going from 0 to 180 degrees. A negative roll is to the left going from 0 to -180 degrees.
-*/
-struct AVAudio3DAngularOrientation {
-    float yaw;
-    float pitch;
-    float roll;
-};
-typedef struct AVAudio3DAngularOrientation AVAudio3DAngularOrientation;
-
-/*!	@method AVAudioMake3DAngularOrientation
-    @abstract Creates and returns an AVAudio3DAngularOrientation object
-*/
-NS_INLINE AVAudio3DAngularOrientation AVAudioMake3DAngularOrientation(float yaw, float pitch, float roll) {
-    AVAudio3DAngularOrientation o;
-    o.yaw = yaw;
-    o.pitch = pitch;
-    o.roll = roll;
-    return o;
-}
-
-#endif // __AVAudioTypes_h__
+#import <AVFAudio/AVAudioTypes.h>
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnit.h	2015-09-30 23:17:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnit.h	2016-05-25 07:19:42.000000000 +0200
@@ -1,105 +1,9 @@
 /*
-    File:       AVAudioUnit.h
-    Framework:  AVFoundation
-    
-    Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	File:           AVAudioUnit.h
+	Framework:      AVFoundation
+	
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioNode.h>
-#import <AudioUnit/AudioUnit.h>
+#import <AVFAudio/AVAudioUnit.h>
 
-NS_ASSUME_NONNULL_BEGIN
-
-#if __OBJC2__
-@class AUAudioUnit;
-#endif // __OBJC2__
-
-/*! @class AVAudioUnit
-    @abstract An AVAudioNode implemented by an audio unit.
-    @discussion
-        An AVAudioUnit is an AVAudioNode implemented by an audio unit. Depending on the type of
-        the audio unit, audio is processed either in real-time or non real-time.
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioUnit : AVAudioNode
-
-/*!	@method	instantiateWithComponentDescription:options:completionHandler:
-	@abstract Asynchronously create an instance of an audio unit component, wrapped in an AVAudioUnit.
-	@param audioComponentDescription
-		The component to instantiate.
-	@param options
-		Instantiation options.
-	@param completionHandler
-		Called in an arbitrary thread/queue context when instantiation is complete. The client
-		should retain the provided AVAudioUnit.
-	@discussion
-		Components whose flags include kAudioComponentFlag_RequiresAsyncInstantiation must be 
-		instantiated asynchronously, via this method if they are to be used with AVAudioEngine.
-		See the discussion of this flag in AudioUnit/AudioComponent.h.
-		
-		The returned AVAudioUnit instance normally will be of a subclass (AVAudioUnitEffect,
-		AVAudioUnitGenerator, AVAudioUnitMIDIInstrument, or AVAudioUnitTimeEffect), selected
-		according to the component's type.
-*/
-+ (void)instantiateWithComponentDescription:(AudioComponentDescription)audioComponentDescription options:(AudioComponentInstantiationOptions)options completionHandler:(void (^)(__kindof AVAudioUnit * __nullable audioUnit, NSError * __nullable error))completionHandler NS_AVAILABLE(10_11, 9_0);
-
-/*! @method loadAudioUnitPresetAtURL:error:
-    @abstract Load an audio unit preset.
-    @param url
-        NSURL of the .aupreset file.
-	@param outError
-    @discussion
-        If the .aupreset file cannot be successfully loaded, an error is returned.
-*/
-- (BOOL)loadAudioUnitPresetAtURL:(NSURL *)url error:(NSError **)outError;
-
-/*! @property audioComponentDescription
-    @abstract AudioComponentDescription of the underlying audio unit.
-*/
-@property (nonatomic, readonly) AudioComponentDescription audioComponentDescription;
-
-/*! @property audioUnit
-    @abstract Reference to the underlying audio unit.
-    @discussion
-        A reference to the underlying audio unit is provided so that parameters that are not
-        exposed by AVAudioUnit subclasses can be modified using the AudioUnit C API.
- 
-        No operations that may conflict with state maintained by the engine should be performed
-        directly on the audio unit. These include changing initialization state, stream formats,
-        channel layouts or connections to other audio units.
-*/
-@property (nonatomic, readonly) AudioUnit audioUnit;
-
-#if __OBJC2__
-/*! @property AUAudioUnit
-    @abstract An AUAudioUnit wrapping or underlying the implementation's AudioUnit.
-    @discussion
-        This provides an AUAudioUnit which either wraps or underlies the implementation's
-        AudioUnit, depending on how that audio unit is packaged. Applications can interact with this
-        AUAudioUnit to control custom properties, select presets, change parameters, etc.
- 
-        As with the audioUnit property, no operations that may conflict with state maintained by the
-        engine should be performed directly on the audio unit. These include changing initialization
-        state, stream formats, channel layouts or connections to other audio units.
-*/
-@property (nonatomic, readonly) AUAudioUnit *AUAudioUnit NS_AVAILABLE(10_11, 9_0);
-#endif // __OBJC2__
-
-/*! @property name
-    @abstract Name of the audio unit.
-*/
-@property (nonatomic, readonly) NSString *name;
-
-/*! @property manufacturerName
-    @abstract Manufacturer name of the audio unit.
-*/
-@property (nonatomic, readonly) NSString *manufacturerName;
-
-/*! @property version
-    @abstract Version number of the audio unit.
-*/
-@property (nonatomic, readonly) NSUInteger version;
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitComponent.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitComponent.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitComponent.h	2015-09-30 23:17:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitComponent.h	2016-05-25 07:19:42.000000000 +0200
@@ -1,238 +1,9 @@
 /*
- File:		AVAudioUnitComponent.h
- Framework:	AVFoundation
- 
- Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
- */
+	File:           AVAudioUnitComponent.h
+	Framework:      AVFoundation
+	
+	Copyright 2016 Apple Inc. All rights reserved.
+*/
 
-#import <AVFoundation/AVAudioTypes.h>
-#import <AudioUnit/AudioComponent.h>
-#import <AudioUnit/AUComponent.h>
+#import <AVFAudio/AVAudioUnitComponent.h>
 
-NS_ASSUME_NONNULL_BEGIN
-
-// Standard Audio Unit Types
-AVF_EXPORT NSString * const AVAudioUnitTypeOutput				NS_AVAILABLE(10_10, 9_0);
-AVF_EXPORT NSString * const AVAudioUnitTypeMusicDevice			NS_AVAILABLE(10_10, 9_0);
-AVF_EXPORT NSString * const AVAudioUnitTypeMusicEffect			NS_AVAILABLE(10_10, 9_0);
-AVF_EXPORT NSString * const AVAudioUnitTypeFormatConverter		NS_AVAILABLE(10_10, 9_0);
-AVF_EXPORT NSString * const AVAudioUnitTypeEffect				NS_AVAILABLE(10_10, 9_0);
-AVF_EXPORT NSString * const AVAudioUnitTypeMixer				NS_AVAILABLE(10_10, 9_0);
-AVF_EXPORT NSString * const AVAudioUnitTypePanner				NS_AVAILABLE(10_10, 9_0);
-AVF_EXPORT NSString * const AVAudioUnitTypeGenerator			NS_AVAILABLE(10_10, 9_0);
-AVF_EXPORT NSString * const AVAudioUnitTypeOfflineEffect		NS_AVAILABLE(10_10, 9_0);
-AVF_EXPORT NSString * const AVAudioUnitTypeMIDIProcessor		NS_AVAILABLE(10_10, 9_0);
-
-// Standard Audio Unit Manufacturers
-AVF_EXPORT NSString * const AVAudioUnitManufacturerNameApple	NS_AVAILABLE(10_10, 9_0);
-
-#pragma mark AVAudioUnitComponent
-
-/*!
- @class AVAudioUnitComponent
- @discussion
-	 AVAudioUnitComponent provides details about an audio unit such as type, subtype, manufacturer, 
-	 location etc. User tags can be added to the AVAudioUnitComponent which can be queried later
- 	 for display.
- */
-
-NS_CLASS_AVAILABLE(10_10, 9_0)
-@interface AVAudioUnitComponent : NSObject
-{
-	void *_impl;
-}
-/*! @property name
-	@abstract the name of an audio component
- */
-@property (nonatomic, readonly) NSString		*name;
-
-/*! @property typeName
-	@abstract standard audio component types returned as strings
- */
-@property (nonatomic, readonly) NSString		*typeName;
-
-/*! @property typeName
-	@abstract localized string of typeName for display
- */
-@property (nonatomic, readonly) NSString		*localizedTypeName;
-
-/*! @property manufacturerName
-	@abstract the manufacturer name, extracted from the manufacturer key defined in Info.plist dictionary
- */
-@property (nonatomic, readonly) NSString		*manufacturerName;
-
-/*! @property version
-	@abstract version number comprised of a hexadecimal number with major, minor, dot-release format: 0xMMMMmmDD
- */
-@property (nonatomic, readonly) NSUInteger	version;
-
-/*! @property versionString
-	@abstract version number as string
- */
-@property (nonatomic, readonly) NSString		*versionString;
-
-/*! @property componentURL
-	@abstract URL representing location of component
- */
-@property (nonatomic, readonly, nullable) NSURL		*componentURL NS_DEPRECATED(10_10, 10_11, NA, NA);
-
-/*! @property availableArchitectures
-	@abstract NSArray of NSNumbers each of which corresponds to one of the constants in Mach-O Architecture in NSBundle Class Reference
- */
-@property (nonatomic, readonly) NSArray<NSNumber *>		*availableArchitectures NS_AVAILABLE(10_10, NA);
-
-/*! @property sandboxSafe
-	@abstract On OSX, YES if the AudioComponent can be loaded into a sandboxed process otherwise NO.
-			  On iOS, this is always YES.
- */
-@property (nonatomic, readonly, getter=isSandboxSafe) BOOL		sandboxSafe;
-
-/*! @property hasMIDIInput
-	@abstract YES if AudioComponent has midi input, otherwise NO
- */
-@property (nonatomic, readonly) BOOL		hasMIDIInput;
-
-/*! @property hasMIDIOutput
-	@abstract YES if AudioComponent has midi output, otherwise NO
- */
-@property (nonatomic, readonly) BOOL		hasMIDIOutput;
-
-/*! @property audioComponent
-	@abstract the audioComponent that can be used in AudioComponent APIs.
- */
-@property (nonatomic, readonly) AudioComponent	audioComponent;
-
-/*! @property userTagNames
-	@abstract User tags represent the tags from the current user.
- */
-@property (copy) NSArray<NSString *>		*userTagNames NS_AVAILABLE(10_10, NA);
-
-/*! @property allTagNames
-	@abstract represent the tags from the current user and the system tags defined by AudioComponent.
- */
-@property (nonatomic, readonly) NSArray<NSString *>		*allTagNames;
-
-/*! @property audioComponentDescription
-	@abstract description of the audio component that can be used in AudioComponent APIs.
- */
-@property (nonatomic, readonly) AudioComponentDescription	audioComponentDescription;
-
-/*! @property iconURL
-	@abstract A URL that will specify the location of an icon file that can be used when presenting UI
- for this audio component.
- */
-@property (nonatomic, readonly, nullable) NSURL		*iconURL NS_AVAILABLE(10_10, NA);
-
-#if !TARGET_OS_IPHONE
-/*! @property icon
-	@abstract An icon representing the component.
-    @discussion
-        For a component originating in an app extension, the returned icon will be that of the
-        application containing the extension.
-        
-        For components loaded from bundles, the icon will be that of the bundle.
- */
-@property (nonatomic, readonly, nullable) NSImage *icon NS_AVAILABLE(10_11, NA);
-#endif
-
-/*! @property passesAUVal
-	@abstract YES if the AudioComponent has passed the AU validation tests, otherwise NO
- */
-@property (nonatomic, readonly) BOOL		passesAUVal NS_AVAILABLE(10_10, NA);
-
-/*! @property hasCustomView
-	@abstract YES if the AudioComponent provides custom view, otherwise NO
- */
-@property (nonatomic, readonly) BOOL		hasCustomView NS_AVAILABLE(10_10, NA);
-
-/*! @property configurationDictionary
-	@abstract A NSDictionary that contains information describing the capabilities of the AudioComponent.
-	The specific information depends on the type and the keys are defined in AudioUnitProperties.h
- */
-@property (nonatomic, readonly) NSDictionary<NSString *, id>		*configurationDictionary NS_AVAILABLE(10_10, NA);
-
-/*! @property supportsNumberInputChannels: outputChannels:
-	@abstract returns YES if the AudioComponent supports the input/output channel configuration
- */
-- (BOOL)supportsNumberInputChannels:(NSInteger)numInputChannels outputChannels:(NSInteger)numOutputChannels NS_AVAILABLE(10_10, NA);
-
-@end
-
-
-#pragma mark AVAudioUnitComponentManager
-
-/* The notification object is an AVAudioUnitComponent object */
-AVF_EXPORT NSString * const AVAudioUnitComponentTagsDidChangeNotification NS_AVAILABLE(10_10, 9_0);
-
-/*!
- @class AVAudioUnitComponentManager
- @discussion 
- 		AVAudioUnitComponentManager is a singleton object that provides an easy way to find
- 		audio components that are registered with the system. It provides methods to search and
- 		query various information about the audio components without opening them.
- 
- 		Currently audio components that are audio units can only be searched.
- 
- 		The class also supports predefined system tags and arbitrary user tags. Each audio unit can be 
- 		tagged as part of its definition. Refer to AudioComponent.h for more details. AudioUnit Hosts
- 		such as Logic or GarageBand can present groupings of audio units based on the tags.
- 
- 		Searching for audio units can be done in various ways
- 			- using a NSPredicate that contains search strings for tags or descriptions
- 			- using a block to match on custom criteria 
-			- using an AudioComponentDescription
- */
-
-NS_CLASS_AVAILABLE(10_10, 9_0)
-@interface AVAudioUnitComponentManager : NSObject
-{
-	void *_impl;
-}
-
-/*! @discussion 
- 		returns all tags associated with the current user as well as all system tags defined by 
-		the audio unit(s).
- */
-@property (nonatomic, readonly) NSArray<NSString *>		*tagNames;
-
-/*! @discussion
-		returns the localized standard system tags defined by the audio unit(s).
- */
-
-@property (nonatomic, readonly) NSArray<NSString *>		*standardLocalizedTagNames;
-
-/* returns singleton instance of AVAudioUnitComponentManager */
-+ (instancetype)sharedAudioUnitComponentManager;
-
-/*!
- @method componentsMatchingPredicate:
- @abstract	returns an array of AVAudioUnitComponent objects that match the search predicate.
- @discussion
- 		AudioComponent's information or tags can be used to build a search criteria. 
- 		For example, "typeName CONTAINS 'Effect'" or tags IN {'Sampler', 'MIDI'}"
- */
-- (NSArray<AVAudioUnitComponent *> *)componentsMatchingPredicate:(NSPredicate *)predicate;
-
-/*!
- @method componentsPassingTest:
- @abstract	returns an array of AVAudioUnitComponent objects that pass the user provided block method.
- @discussion
-		For each AudioComponent found by the manager, the block method will be called. If the return
- 		value is YES then the AudioComponent is added to the resulting array else it will excluded. 
- 		This gives more control to the block provider to filter out the components returned.
- */
-- (NSArray<AVAudioUnitComponent *> *)componentsPassingTest:(BOOL(^)(AVAudioUnitComponent *comp, BOOL *stop))testHandler;
-
-/*!
- @method componentsMatchingDescription:
- @abstract	returns an array of AVAudioUnitComponent objects that match the description.
- @discussion
- 		This method provides a mechanism to search for AudioComponents using AudioComponentDescription
-		structure. The type, subtype and manufacturer fields are used to search for audio units. A 
- 		value of 0 for any of these fields is a wildcard and returns the first match found.
- */
-- (NSArray<AVAudioUnitComponent *> *)componentsMatchingDescription:(AudioComponentDescription)desc;
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitDelay.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitDelay.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitDelay.h	2015-09-30 23:17:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitDelay.h	2016-05-25 07:19:42.000000000 +0200
@@ -1,62 +1,9 @@
 /*
-    File:		AVAudioUnitDelay.h
-    Framework:	AVFoundation
- 
-    Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	File:           AVAudioUnitDelay.h
+	Framework:      AVFoundation
+	
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioUnitEffect.h>
+#import <AVFAudio/AVAudioUnitDelay.h>
 
-NS_ASSUME_NONNULL_BEGIN
-
-/*! @class AVAudioUnitDelay
-    @abstract an AVAudioUnitEffect that implements a delay effect
-    @discussion
-        A delay unit delays the input signal by the specified time interval
-        and then blends it with the input signal. The amount of high frequency
-        roll-off can also be controlled in order to simulate the effect of
-        a tape delay.
- 
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioUnitDelay : AVAudioUnitEffect
-
-/*! @property delayTime
-    Time taken by the delayed input signal to reach the output
-    @abstract
-    Range:      0 -> 2
-    Default:    1
-    Unit:       Seconds
- */
-@property (nonatomic) NSTimeInterval delayTime;
-
-/*! @property feedback
-    @abstract
-    Amount of the output signal fed back into the delay line
-    Range:      -100 -> 100
-    Default:    50
-    Unit:       Percent
-*/
-@property (nonatomic) float feedback;
-
-/*! @property lowPassCutoff
-    @abstract
-    Cutoff frequency above which high frequency content is rolled off
-    Range:      10 -> (samplerate/2)
-    Default:    15000
-    Unit:       Hertz
-*/
-@property (nonatomic) float lowPassCutoff;
-
-/*! @property wetDryMix
-    @abstract
-    Blend of the wet and dry signals
-    Range:      0 (all dry) -> 100 (all wet)
-    Default:    100
-    Unit:       Percent
-*/
-@property (nonatomic) float wetDryMix;
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitDistortion.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitDistortion.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitDistortion.h	2015-09-30 23:18:00.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitDistortion.h	2016-05-25 07:19:42.000000000 +0200
@@ -1,71 +1,9 @@
 /*
-    File:		AVAudioUnitDistortion.h
-    Framework:	AVFoundation
- 
-    Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	File:           AVAudioUnitDistortion.h
+	Framework:      AVFoundation
+	
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioUnitEffect.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-typedef NS_ENUM(NSInteger, AVAudioUnitDistortionPreset) {
-    AVAudioUnitDistortionPresetDrumsBitBrush           = 0,
-    AVAudioUnitDistortionPresetDrumsBufferBeats        = 1,
-    AVAudioUnitDistortionPresetDrumsLoFi               = 2,
-    AVAudioUnitDistortionPresetMultiBrokenSpeaker      = 3,
-    AVAudioUnitDistortionPresetMultiCellphoneConcert   = 4,
-    AVAudioUnitDistortionPresetMultiDecimated1         = 5,
-    AVAudioUnitDistortionPresetMultiDecimated2         = 6,
-    AVAudioUnitDistortionPresetMultiDecimated3         = 7,
-    AVAudioUnitDistortionPresetMultiDecimated4         = 8,
-    AVAudioUnitDistortionPresetMultiDistortedFunk      = 9,
-    AVAudioUnitDistortionPresetMultiDistortedCubed     = 10,
-    AVAudioUnitDistortionPresetMultiDistortedSquared   = 11,
-    AVAudioUnitDistortionPresetMultiEcho1              = 12,
-    AVAudioUnitDistortionPresetMultiEcho2              = 13,
-    AVAudioUnitDistortionPresetMultiEchoTight1         = 14,
-    AVAudioUnitDistortionPresetMultiEchoTight2         = 15,
-    AVAudioUnitDistortionPresetMultiEverythingIsBroken = 16,
-    AVAudioUnitDistortionPresetSpeechAlienChatter      = 17,
-    AVAudioUnitDistortionPresetSpeechCosmicInterference = 18,
-    AVAudioUnitDistortionPresetSpeechGoldenPi          = 19,
-    AVAudioUnitDistortionPresetSpeechRadioTower        = 20,
-    AVAudioUnitDistortionPresetSpeechWaves             = 21
-} NS_ENUM_AVAILABLE(10_10, 8_0);
-
-/*! @class AVAudioUnitDistortion
-    @abstract An AVAudioUnitEffect that implements a multi-stage distortion effect.
- 
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioUnitDistortion : AVAudioUnitEffect
-
-/*! @method loadFactoryPreset:
-    @abstract Load a distortion preset.
-    Default:    AVAudioUnitDistortionPresetDrumsBitBrush
-*/
--(void)loadFactoryPreset:(AVAudioUnitDistortionPreset)preset;
-
-/*! @property preGain
-    @abstract
-    Gain applied to the signal before being distorted
-    Range:      -80 -> 20
-    Default:    -6
-    Unit:       dB
-*/
-@property (nonatomic) float preGain;
-
-/*! @property wetDryMix
-    @abstract
-    Blend of the distorted and dry signals
-    Range:      0 (all dry) -> 100 (all distorted)
-    Default:    50
-    Unit:       Percent
-*/
-@property (nonatomic) float wetDryMix;
-
-@end
-
-NS_ASSUME_NONNULL_END
+#import <AVFAudio/AVAudioUnitDistortion.h>
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitEQ.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitEQ.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitEQ.h	2015-09-30 23:18:00.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitEQ.h	2016-05-25 07:19:42.000000000 +0200
@@ -1,164 +1,9 @@
 /*
-    File:		AVAudioUnitEQ.h
-    Framework:	AVFoundation
- 
-    Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
- */
-
-#import <AVFoundation/AVAudioUnitEffect.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-/*! @enum AVAudioUnitEQFilterType
-    @abstract Filter types available to use with AVAudioUnitEQ.
-    @discussion
-        Depending on the filter type, a combination of one or all of the filter parameters defined 
-        in AVAudioUnitEQFilterParameters are used to set the filter.
-     
-        AVAudioUnitEQFilterTypeParametric
-            Parametric filter based on Butterworth analog prototype.
-            Required parameters: frequency (center), bandwidth, gain
-     
-        AVAudioUnitEQFilterTypeLowPass
-            Simple Butterworth 2nd order low pass filter
-            Required parameters: frequency (-3 dB cutoff at specified frequency)
-        
-        AVAudioUnitEQFilterTypeHighPass
-            Simple Butterworth 2nd order high pass filter
-            Required parameters: frequency (-3 dB cutoff at specified frequency)
-     
-        AVAudioUnitEQFilterTypeResonantLowPass
-            Low pass filter with resonance support (via bandwidth parameter)
-            Required parameters: frequency (-3 dB cutoff at specified frequency), bandwidth
-     
-        AVAudioUnitEQFilterTypeResonantHighPass
-            High pass filter with resonance support (via bandwidth parameter)
-            Required parameters: frequency (-3 dB cutoff at specified frequency), bandwidth
-     
-        AVAudioUnitEQFilterTypeBandPass
-            Band pass filter
-            Required parameters: frequency (center), bandwidth
-     
-        AVAudioUnitEQFilterTypeBandStop
-            Band stop filter (aka "notch filter")
-            Required parameters: frequency (center), bandwidth
-     
-        AVAudioUnitEQFilterTypeLowShelf
-            Low shelf filter
-            Required parameters: frequency (center), gain
-     
-        AVAudioUnitEQFilterTypeHighShelf
-            High shelf filter
-            Required parameters: frequency (center), gain
-     
-        AVAudioUnitEQFilterTypeResonantLowShelf
-            Low shelf filter with resonance support (via bandwidth parameter)
-            Required parameters: frequency (center), bandwidth, gain
-     
-        AVAudioUnitEQFilterTypeResonantHighShelf
-            High shelf filter with resonance support (via bandwidth parameter)
-            Required parameters: frequency (center), bandwidth, gain
- 
-*/
-typedef NS_ENUM(NSInteger, AVAudioUnitEQFilterType) {
-    AVAudioUnitEQFilterTypeParametric        = 0,
-    AVAudioUnitEQFilterTypeLowPass           = 1,
-    AVAudioUnitEQFilterTypeHighPass          = 2,
-    AVAudioUnitEQFilterTypeResonantLowPass   = 3,
-    AVAudioUnitEQFilterTypeResonantHighPass  = 4,
-    AVAudioUnitEQFilterTypeBandPass          = 5,
-    AVAudioUnitEQFilterTypeBandStop          = 6,
-    AVAudioUnitEQFilterTypeLowShelf          = 7,
-    AVAudioUnitEQFilterTypeHighShelf         = 8,
-    AVAudioUnitEQFilterTypeResonantLowShelf  = 9,
-    AVAudioUnitEQFilterTypeResonantHighShelf = 10,
-} NS_ENUM_AVAILABLE(10_10, 8_0);
-
-
-/*! @class AVAudioUnitEQFilterParameters
-    @abstract Filter parameters used by AVAudioUnitEQ.
-    @discussion
-        A standalone instance of AVAudioUnitEQFilterParameters cannot be created. Only an instance
-        vended out by a source object (e.g. AVAudioUnitEQ) can be used.
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioUnitEQFilterParameters : NSObject {
-@private
-	void *_impl;
-}
-
-/*! @property filterType
-    @abstract AVAudioUnitEQFilterType
-    @discussion
-    Default:    AVAudioUnitEQFilterTypeParametric
-*/
-@property (nonatomic) AVAudioUnitEQFilterType filterType;
-
-/*! @property frequency
-    @abstract Frequency in Hertz.
-    @discussion
-    Range:      20 -> (SampleRate/2)
-    Unit:       Hertz
-*/
-@property (nonatomic) float frequency;
-
-/*! @property bandwidth
-    @abstract Bandwidth in octaves.
-    @discussion
-    Range:      0.05 -> 5.0
-    Unit:       Octaves
-*/
-@property (nonatomic) float bandwidth;
-
-/*! @property gain
-    @abstract Gain in dB.
-    @discussion
-    Range:      -96 -> 24
-    Default:    0
-    Unit:       dB
-*/
-@property (nonatomic) float gain;
-
-/*! @property bypass
-    @abstract bypass state of band.
-    @discussion
-    Default:    YES
-*/
-@property (nonatomic) BOOL bypass;
-
-@end
-
-
-/*! @class AVAudioUnitEQ
-    @abstract An AVAudioUnitEffect that implements a Multi-Band Equalizer.
- 
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioUnitEQ : AVAudioUnitEffect
-
-/*! @method initWithNumberOfBands:
-    @abstract Initialize the EQ with number of bands.
-    @param numberOfBands
-        The number of bands created by the EQ.
-*/
-- (instancetype)initWithNumberOfBands:(NSUInteger)numberOfBands;
-
-/*! @property bands
-    @abstract Array of AVAudioUnitEQFilterParameters objects.
-    @discussion
-        The number of elements in the array is equal to the number of bands.
-*/
-@property (nonatomic, readonly) NSArray<AVAudioUnitEQFilterParameters *> *bands;
-
-/*! @property globalGain
-    @abstract Overall gain adjustment applied to the signal.
-    @discussion
-        Range:     -96 -> 24
-        Default:   0
-        Unit:      dB
+	File:           AVAudioUnitEQ.h
+	Framework:      AVFoundation
+	
+	Copyright 2016 Apple Inc. All rights reserved.
 */
-@property (nonatomic) float globalGain;
 
-@end
+#import <AVFAudio/AVAudioUnitEQ.h>
 
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitEffect.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitEffect.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitEffect.h	2015-09-30 23:18:00.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitEffect.h	2016-05-25 07:19:42.000000000 +0200
@@ -1,51 +1,9 @@
 /*
-    File:		AVAudioUnitEffect.h
-    Framework:	AVFoundation
- 
-    Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	File:           AVAudioUnitEffect.h
+	Framework:      AVFoundation
+	
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioUnit.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-/*! @class AVAudioUnitEffect
-    @abstract an AVAudioUnit that processes audio in real-time
-    @discussion
-    An AVAudioUnitEffect represents an audio unit of type kAudioUnitType_Effect,
-    kAudioUnitType_MusicEffect, kAudioUnitType_Panner, kAudioUnitType_RemoteEffect or 
-    kAudioUnitType_RemoteMusicEffect.
-
-    These effects run in real-time and process some x number of audio input 
-    samples to produce x number of audio output samples. A delay unit is an 
-    example of an effect unit.
- 
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioUnitEffect : AVAudioUnit
-
-/*! @method initWithAudioComponentDescription:
-    @abstract Create an AVAudioUnitEffect object.
-    
-    @param audioComponentDescription
-    @abstract AudioComponentDescription of the audio unit to be instantiated.
-    @discussion
-    The componentType must be one of these types
-    kAudioUnitType_Effect
-    kAudioUnitType_MusicEffect
-    kAudioUnitType_Panner
-    kAudioUnitType_RemoteEffect
-    kAudioUnitType_RemoteMusicEffect
-
-*/
-- (instancetype)initWithAudioComponentDescription:(AudioComponentDescription)audioComponentDescription;
-
-/*! @property bypass
-    @abstract Bypass state of the audio unit.
-*/
-@property (nonatomic) BOOL bypass;
-
-@end
-
-NS_ASSUME_NONNULL_END
+#import <AVFAudio/AVAudioUnitEffect.h>
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitGenerator.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitGenerator.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitGenerator.h	2015-09-30 23:18:00.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitGenerator.h	2016-05-25 07:19:43.000000000 +0200
@@ -1,41 +1,9 @@
 /*
-    File:		AVAudioUnitGenerator.h
-    Framework:	AVFoundation
- 
-    Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
- */
-
-#import <AVFoundation/AVAudioUnit.h>
-#import <AVFoundation/AVAudioMixing.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-/*! @class AVAudioUnitGenerator
-    @abstract an AVAudioUnit that generates audio output
-    @discussion
-    An AVAudioUnitGenerator represents an audio unit of type kAudioUnitType_Generator or
-	kAudioUnitType_RemoteGenerator.
-    A generator will have no audio input, but will just produce audio output.
-    A tone generator is an example of this. 
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioUnitGenerator : AVAudioUnit <AVAudioMixing>
-
-/*! @method initWithAudioComponentDescription:
-    @abstract Create an AVAudioUnitGenerator object.
-    
-    @param audioComponentDescription
-    @abstract AudioComponentDescription of the audio unit to be instantiated.
-    @discussion
-    The componentType must be kAudioUnitType_Generator or kAudioUnitType_RemoteGenerator
-*/
-- (instancetype)initWithAudioComponentDescription:(AudioComponentDescription)audioComponentDescription;
-
-/*! @property bypass
-    @abstract Bypass state of the audio unit.
+	File:           AVAudioUnitGenerator.h
+	Framework:      AVFoundation
+	
+	Copyright 2016 Apple Inc. All rights reserved.
 */
-@property (nonatomic) BOOL bypass;
 
-@end
+#import <AVFAudio/AVAudioUnitGenerator.h>
 
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitMIDIInstrument.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitMIDIInstrument.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitMIDIInstrument.h	2015-09-30 23:18:00.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitMIDIInstrument.h	2016-05-25 07:19:43.000000000 +0200
@@ -1,175 +1,9 @@
 /*
-	File:		AVAudioUnitMIDIInstrument.h
-	Framework:	AVFoundation
+	File:           AVAudioUnitMIDIInstrument.h
+	Framework:      AVFoundation
 	
-	Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioUnit.h>
-#import <AVFoundation/AVAudioMixing.h>
+#import <AVFAudio/AVAudioUnitMIDIInstrument.h>
 
-#if defined(__MAC_OS_X_VERSION_MIN_REQUIRED) && __MAC_OS_X_VERSION_MIN_REQUIRED >= 101100
-	#define AVAudioUnitMIDIInstrument_MixingConformance <AVAudioMixing>
-#elif defined(__IPHONE_OS_VERSION_MIN_REQUIRED) && __IPHONE_OS_VERSION_MIN_REQUIRED >= 90000
-	#define AVAudioUnitMIDIInstrument_MixingConformance <AVAudioMixing>
-#else
-	#define AVAudioUnitMIDIInstrument_MixingConformance
-#endif
-
-
-NS_ASSUME_NONNULL_BEGIN
-
-/*!
- @class AVAudioUnitMIDIInstrument
- @abstract Base class for sample synthesizers.
- @discussion
-    This base class represents audio units of type kAudioUnitType_MusicDevice or kAudioUnitType_RemoteInstrument. This can be used in a chain
-    that processes realtime input (live) and has general concept of music events i.e. notes.
- */
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioUnitMIDIInstrument : AVAudioUnit AVAudioUnitMIDIInstrument_MixingConformance
-
-/*! @method initWithAudioComponentDescription:
- @abstract initialize the node with the component description
- @param description
-    audio component description structure that describes the audio component of type kAudioUnitType_MusicDevice
-    or kAudioUnitType_RemoteInstrument.
- */
-- (instancetype)initWithAudioComponentDescription:(AudioComponentDescription)description;
-
-/*! @method startNote:withVelocity:onChannel:
- @abstract sends a MIDI Note On event to the instrument
- @param note
-    the note number (key) to play.
-    Range: 0 -> 127
- @param velocity
-    specifies the volume with which the note is played.
-    Range: 0 -> 127
- @param channel
-    the channel number to which the event is sent.
- */
-- (void)startNote:(uint8_t)note withVelocity:(uint8_t)velocity onChannel:(uint8_t)channel;
-
-/*! @method stopNote:onChannel:
- @abstract sends a MIDI Note Off event to the instrument
- @param note
-    the note number (key) to stop
-    Range: 0 -> 127
- @param channel
-    the channel number to which the event is sent. 
-
- */
-- (void)stopNote:(uint8_t)note onChannel:(uint8_t)channel;
-
-/*! @method sendController:withValue:onChannel:
- @abstract send a MIDI controller event to the instrument.
- @param controller
-    a standard MIDI controller number. 
-    Range: 0 -> 127
- @param  value
-    value for the controller. 
-    Range: 0 -> 127
- @param channel
-    the channel number to which the event is sent. 
- 
- */
-- (void)sendController:(uint8_t)controller withValue:(uint8_t)value onChannel:(uint8_t)channel;
-
-/*! @method sendPitchBend:onChannel:
- @abstract sends MIDI Pitch Bend event to the instrument.
- @param pitchbend
-    value of the pitchbend
-    Range: 0 -> 16383
- @param channel
-    the channel number to which the pitch bend message is sent
- 
- */
-- (void)sendPitchBend:(uint16_t)pitchbend onChannel:(uint8_t)channel;
-
-/*! @method sendPressure:onChannel:
- @abstract sends MIDI channel pressure event to the instrument.
- @param pressure 
-    value of the pressure.
-    Range: 0 -> 127
- @param channel
-    the channel number to which the event is sent. 
-
- */
-- (void)sendPressure:(uint8_t)pressure onChannel:(uint8_t)channel;
-
-/*! @method sendPressureForKey:withValue:onChannel:
- @abstract sends MIDI Polyphonic key pressure event to the instrument
- @param key
-    the key (note) number to which the pressure event applies
-    Range: 0 -> 127
- @param value
-    value of the pressure
-    Range: 0 -> 127
- @param channel
-    channel number to which the event is sent. 
-
- */
-- (void)sendPressureForKey:(uint8_t)key withValue:(uint8_t)value onChannel:(uint8_t)channel;
-
-/*! @method sendProgramChange:onChannel:
- @abstract sends MIDI Program Change event to the instrument
- @param program
-    the program number.
-    Range: 0 -> 127
- @param channel
-    channel number to which the event is sent.
- @discussion
-    the instrument will be loaded from the bank that has been previous set by MIDI Bank Select
-    controller messages (0 and 31). If none has been set, bank 0 will be used. 
- */
-- (void)sendProgramChange:(uint8_t)program onChannel:(uint8_t)channel;
-
-/*! @method sendProgramChange:bankMSB:bankLSB:onChannel:
- @abstract sends a MIDI Program Change and Bank Select events to the instrument
- @param program
-    specifies the program (preset) number within the bank to load.
-    Range: 0 -> 127
- @param bankMSB
-    specifies the most significant byte value for the bank to select.
-    Range: 0 -> 127
- @param bankLSB
-    specifies the least significant byte value for the bank to select.
-    Range: 0 -> 127
- @param channel
-    channel number to which the events are sent.
- @discussion
- 
- */
-- (void)sendProgramChange:(uint8_t)program bankMSB:(uint8_t)bankMSB bankLSB:(uint8_t)bankLSB onChannel:(uint8_t)channel;
-
-/*! @method sendMIDIEvent:data1:data2:
- @abstract sends a MIDI event which contains two data bytes to the instrument.
- @param midiStatus
-    the STATUS value of the MIDI event
- @param data1
-    the first data byte of the MIDI event
- @param data2
-    the second data byte of the MIDI event.
-  */
-- (void)sendMIDIEvent:(uint8_t)midiStatus data1:(uint8_t)data1 data2:(uint8_t)data2;
-
-/*! @method sendMIDIEvent:data1:
- @abstract sends a MIDI event which contains one data byte to the instrument.
- @param midiStatus
-    the STATUS value of the MIDI event
- @param data1
-    the first data byte of the MIDI event
- */
-- (void)sendMIDIEvent:(uint8_t)midiStatus data1:(uint8_t)data1;
-
-/*! @method sendMIDISysExEvent:
- @abstract sends a MIDI System Exclusive event to the instrument.
- @param midiData
-    a NSData object containing the complete SysEx data including start(F0) and termination(F7) bytes.
- 
- */
-- (void)sendMIDISysExEvent:(NSData *)midiData;
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitReverb.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitReverb.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitReverb.h	2015-09-30 23:18:00.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitReverb.h	2016-05-25 07:19:43.000000000 +0200
@@ -1,55 +1,9 @@
 /*
-    File:		AVAudioUnitReverb.h
-    Framework:	AVFoundation
- 
-    Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
- */
-
-#import <AVFoundation/AVAudioUnitEffect.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-typedef NS_ENUM(NSInteger, AVAudioUnitReverbPreset) {
-    AVAudioUnitReverbPresetSmallRoom       = 0,
-    AVAudioUnitReverbPresetMediumRoom      = 1,
-    AVAudioUnitReverbPresetLargeRoom       = 2,
-    AVAudioUnitReverbPresetMediumHall      = 3,
-    AVAudioUnitReverbPresetLargeHall       = 4,
-    AVAudioUnitReverbPresetPlate           = 5,
-    AVAudioUnitReverbPresetMediumChamber   = 6,
-    AVAudioUnitReverbPresetLargeChamber    = 7,
-    AVAudioUnitReverbPresetCathedral       = 8,
-    AVAudioUnitReverbPresetLargeRoom2      = 9,
-    AVAudioUnitReverbPresetMediumHall2     = 10,
-    AVAudioUnitReverbPresetMediumHall3     = 11,
-    AVAudioUnitReverbPresetLargeHall2      = 12
-} NS_ENUM_AVAILABLE(10_10, 8_0);
-
-/*! @class AVAudioUnitReverb
-    @abstract an AVAudioUnitEffect that implements a reverb
-    @discussion
-        A reverb simulates the acoustic characteristics of a particular environment.
-        Use the different presets to simulate a particular space and blend it in with
-        the original signal using the wetDryMix parameter.
- 
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioUnitReverb : AVAudioUnitEffect
-
-/*! @method loadFactoryPreset:
-    @abstract load a reverb preset
-    Default:    AVAudioUnitReverbPresetMediumHall
-*/
-- (void)loadFactoryPreset:(AVAudioUnitReverbPreset)preset;
-
-/*! @property wetDryMix
-    @abstract
-    Blend of the wet and dry signals
-    Range:      0 (all dry) -> 100 (all wet)
-    Unit:       Percent
+	File:           AVAudioUnitReverb.h
+	Framework:      AVFoundation
+	
+	Copyright 2016 Apple Inc. All rights reserved.
 */
-@property (nonatomic) float wetDryMix;
 
-@end
+#import <AVFAudio/AVAudioUnitReverb.h>
 
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitSampler.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitSampler.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitSampler.h	2015-09-30 23:18:00.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitSampler.h	2016-05-25 07:19:43.000000000 +0200
@@ -1,103 +1,9 @@
 /*
-	File:		AVAudioUnitSampler.h
-	Framework:	AVFoundation
+	File:           AVAudioUnitSampler.h
+	Framework:      AVFoundation
 	
-	Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioUnitMIDIInstrument.h>
+#import <AVFAudio/AVAudioUnitSampler.h>
 
-NS_ASSUME_NONNULL_BEGIN
-
-/*!
- @class AVAudioUnitSampler
- @abstract Apple's sampler audio unit.
- @discussion
-    An AVAudioUnit for Apple's Sampler Audio Unit. The sampler can be configured by loading
-    instruments from different types of files such as an aupreset, a DLS or SF2 sound bank,
-    an EXS24 instrument, a single audio file, or an array of audio files.
-
-    The output is a single stereo bus. 
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioUnitSampler : AVAudioUnitMIDIInstrument
-
-/*! @method loadSoundBankInstrumentAtURL:program:bankMSB:bankLSB:error:
-	@abstract loads a specific instrument from the specified sound bank
-	@param bankURL
-		URL for a Soundbank file. The file can be either a DLS bank (.dls) or a SoundFont bank (.sf2).
-	@param program
-		program number for the instrument to load
-	@param bankMSB
-		MSB for the bank number for the instrument to load.  This is usually 0x79 for melodic
-		instruments and 0x78 for percussion instruments.
-	@param bankLSB
-		LSB for the bank number for the instrument to load.  This is often 0, and represents the "bank variation".
-	@param outError
-    	the status of the operation
-	@discussion
- 		This method reads from file and allocates memory, so it should not be called on a real time thread.
- */
-- (BOOL)loadSoundBankInstrumentAtURL:(NSURL *)bankURL program:(uint8_t)program bankMSB:(uint8_t)bankMSB bankLSB:(uint8_t)bankLSB error:(NSError **)outError;
-
-/*! @method loadInstrumentAtURL:error:
-	@abstract configures the sampler by loading the specified preset file.
-	@param instrumentURL
-    	URL to the preset file or audio file
-	@param outError
-		the status of the operation
-	@discussion
-		The file can be of one of the following types: Logic/GarageBand EXS24 instrument,
-		the Sampler AU's native aupreset, or an audio file (eg. .caf, .aiff, .wav, .mp3).
-	 
-		If an audio file URL is loaded, it will become the sole sample in a new default instrument.
-		Any information contained in the file regarding its keyboard placement (e.g. root key,
-		key range) will be used.
-		This method reads from file and allocates memory, so it should not be called on a real time thread.
- 
- */
-- (BOOL)loadInstrumentAtURL:(NSURL *)instrumentURL error:(NSError **)outError;
-
-/*! @method loadAudioFilesAtURLs:error:
-	@abstract configures the sampler by loading a set of audio files.
-	@param audioFiles
-		array of URLs for audio files to be loaded
-	@param outError
-		the status of the operation
-	@discussion
-		The audio files are loaded into a new default instrument with each audio file placed
-		into its own sampler zone. Any information contained in the audio file regarding
-		their placement on the keyboard (e.g. root key, key range) will be used.
-		This method reads from file and allocates memory, so it should not be called on a real time thread.
- 
- */
-- (BOOL)loadAudioFilesAtURLs:(NSArray<NSURL *> *)audioFiles error:(NSError **)outError;
-
-/*! @property stereoPan
-	@abstract
-		adjusts the pan for all the notes played.
-		Range:     -1 -> +1
-		Default:   0
- */
-@property (nonatomic) float     stereoPan;
-
-/*! @property masterGain
-	@abstract
-    	adjusts the gain of all the notes played
-		Range:     -90.0 -> +12 db
-		Default: 0 db
- */
-@property (nonatomic) float     masterGain;
-
-/*! @property globalTuning
-	@abstract
-		adjusts the tuning of all the notes played.
-		Range:     -2400 -> +2400 cents
-		Default:   0
- */
-@property (nonatomic) float     globalTuning;
-
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitTimeEffect.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitTimeEffect.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitTimeEffect.h	2015-09-30 23:18:00.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitTimeEffect.h	2016-05-25 07:19:43.000000000 +0200
@@ -1,40 +1,9 @@
 /*
-    File:		AVAudioUnitTimeEffect.h
-    Framework:	AVFoundation
- 
-    Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
- */
-
-#import <AVFoundation/AVAudioUnit.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-/*! @class AVAudioUnitTimeEffect
-    @abstract an AVAudioUnit that processes audio in non real-time
-    @discussion
-    An AVAudioUnitTimeEffect represents an audio unit of type aufc.
-    These effects do not process audio in real-time. The varispeed
-    unit is an example of a time effect unit.
- 
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioUnitTimeEffect : AVAudioUnit
-
-/*! @method initWithAudioComponentDescription:
-    @abstract create an AVAudioUnitTimeEffect object
-    
-    @param audioComponentDescription
-    @abstract AudioComponentDescription of the audio unit to be initialized
-    @discussion 
-    The componentType must be kAudioUnitType_FormatConverter
-*/
-- (instancetype)initWithAudioComponentDescription:(AudioComponentDescription)audioComponentDescription;
-
-/*! @property bypass
-    @abstract bypass state of the audio unit
+	File:           AVAudioUnitTimeEffect.h
+	Framework:      AVFoundation
+	
+	Copyright 2016 Apple Inc. All rights reserved.
 */
-@property (nonatomic) BOOL bypass;
 
-@end
+#import <AVFAudio/AVAudioUnitTimeEffect.h>
 
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitTimePitch.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitTimePitch.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitTimePitch.h	2015-09-30 23:18:00.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitTimePitch.h	2016-05-25 07:19:43.000000000 +0200
@@ -1,56 +1,9 @@
 /*
-    File:		AVAudioUnitTimePitch.h
-    Framework:	AVFoundation
- 
-    Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	File:           AVAudioUnitTimePitch.h
+	Framework:      AVFoundation
+	
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <AVFoundation/AVAudioUnitTimeEffect.h>
+#import <AVFAudio/AVAudioUnitTimePitch.h>
 
-NS_ASSUME_NONNULL_BEGIN
-
-/*! @class AVAudioUnitTimePitch
-    @abstract an AVAudioUnitTimeEffect that provides good quality time stretching and pitch shifting
-    @discussion
-        In this time effect, the playback rate and pitch parameters function independently of each other
- 
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioUnitTimePitch : AVAudioUnitTimeEffect
-
-/*! @property rate
-    @abstract playback rate of the input signal
- 
-    Range:      1/32 -> 32.0
-    Default:    1.0
-    Unit:       Generic
-*/
-@property (nonatomic) float rate;
-
-/*! @property pitch
-    @abstract amount by which the input signal is pitch shifted
-    @discussion
-              1 octave  = 1200 cents
-    1 musical semitone  = 100 cents
- 
-    Range:      -2400 -> 2400
-    Default:    1.0
-    Unit:       Cents
-*/
-@property (nonatomic) float pitch;
-
-/*! @property overlap
-    @abstract amount of overlap between segments of the input audio signal
-    @discussion
-    A higher value results in fewer artifacts in the output signal.
-    This parameter also impacts the amount of CPU used.
- 
-    Range:      3.0 -> 32.0
-    Default:    8.0
-    Unit:       Generic
-*/
-@property (nonatomic) float overlap;
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitVarispeed.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitVarispeed.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitVarispeed.h	2015-09-30 23:18:00.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitVarispeed.h	2016-05-25 07:19:43.000000000 +0200
@@ -1,41 +1,9 @@
 /*
-    File:		AVAudioUnitVarispeed.h
-    Framework:	AVFoundation
- 
-    Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
- */
-
-#import <AVFoundation/AVAudioUnitTimeEffect.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-/*! @class AVAudioUnitVarispeed
-    @abstract an AVAudioUnitTimeEffect that can be used to control the playback rate 
-*/
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVAudioUnitVarispeed : AVAudioUnitTimeEffect
-
-/*! @property rate
-    @abstract controls the playback rate of the audio signal
-    @discussion
-    Since this unit resamples the input signal, changing the playback rate also changes the pitch.
-    
-    i.e. changing the rate to 2.0 results in the output audio playing one octave higher.
-    Similarly changing the rate to 0.5, results in the output audio playing one octave lower.
- 
-    The playback rate and pitch can be calculated as
-                  rate  = pow(2, cents/1200.0)
-        pitch in cents  = 1200.0 * log2(rate)
-    
-    Where,    1 octave  = 1200 cents
-    1 musical semitone  = 100 cents
- 
-    Range:      0.25 -> 4.0
-    Default:    1.0
-    Unit:       Generic
+	File:           AVAudioUnitVarispeed.h
+	Framework:      AVFoundation
+	
+	Copyright 2016 Apple Inc. All rights reserved.
 */
-@property (nonatomic) float rate;
 
-@end
+#import <AVFAudio/AVAudioUnitVarispeed.h>
 
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVBase.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVBase.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVBase.h	2015-09-30 23:18:00.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVBase.h	2016-05-24 07:21:24.000000000 +0200
@@ -42,7 +42,20 @@
 	#define AV_PARAMETERIZED_TYPE(TYPENAME, TYPEBOUNDS) TYPEBOUNDS
 #endif
 
+// Pre-10.12
+#ifndef __NSi_10_12
+	#define __NSi_10_12 introduced=10.12
+#endif
+
+#ifndef __NSd_10_12
+	#define __NSd_10_12 ,deprecated=10.12
+#endif
+
 // Pre-10.11
+#ifndef __NSi_10_11_3
+	#define __NSi_10_11_3 introduced=10.11.3
+#endif
+
 #ifndef __NSi_10_11
 	#define __NSi_10_11 introduced=10.11
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureAudioDataOutput.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureAudioDataOutput.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureAudioDataOutput.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureAudioDataOutput.h	2016-05-25 07:19:43.000000000 +0200
@@ -0,0 +1,138 @@
+/*
+    File:  AVCaptureAudioDataOutput.h
+ 	
+ 	Framework:  AVFoundation
+ 
+	Copyright 2010-2016 Apple Inc. All rights reserved.
+*/
+
+#import <AVFoundation/AVCaptureOutput.h>
+#import <CoreMedia/CMSampleBuffer.h>
+
+#pragma mark - AVCaptureAudioDataOutput
+
+@class AVCaptureAudioDataOutputInternal;
+@protocol AVCaptureAudioDataOutputSampleBufferDelegate;
+
+/*!
+ @class AVCaptureAudioDataOutput
+ @abstract
+    AVCaptureAudioDataOutput is a concrete subclass of AVCaptureOutput that can be used to process uncompressed or compressed samples from the audio being captured.
+ 
+ @discussion
+    Instances of AVCaptureAudioDataOutput produce audio sample buffers suitable for processing using other media APIs. Applications can access the sample buffers with the captureOutput:didOutputSampleBuffer:fromConnection: delegate method.
+ */
+NS_CLASS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED
+@interface AVCaptureAudioDataOutput : AVCaptureOutput 
+{
+@private
+	AVCaptureAudioDataOutputInternal *_internal;
+}
+
+/*!
+ @method setSampleBufferDelegate:queue:
+ @abstract
+    Sets the receiver's delegate that will accept captured buffers and dispatch queue on which the delegate will be called.
+
+ @param sampleBufferDelegate
+    An object conforming to the AVCaptureAudioDataOutputSampleBufferDelegate protocol that will receive sample buffers after they are captured.
+ @param sampleBufferCallbackQueue
+    A dispatch queue on which all sample buffer delegate methods will be called.
+
+ @discussion
+    When a new audio sample buffer is captured it will be vended to the sample buffer delegate using the captureOutput:didOutputSampleBuffer:fromConnection: delegate method. All delegate methods will be called on the specified dispatch queue. If the queue is blocked when new samples are captured, those samples will be automatically dropped when they become sufficiently late. This allows clients to process existing samples on the same queue without having to manage the potential memory usage increases that would otherwise occur when that processing is unable to keep up with the rate of incoming samples.
+
+    Clients that need to minimize the chances of samples being dropped should specify a queue on which a sufficiently small amount of processing is being done outside of receiving sample buffers. However, if such clients migrate extra processing to another queue, they are responsible for ensuring that memory usage does not grow without bound from samples that have not been processed.
+
+    A serial dispatch queue must be used to guarantee that audio samples will be delivered in order. The sampleBufferCallbackQueue parameter may not be NULL, except when setting sampleBufferDelegate to nil.
+ */
+- (void)setSampleBufferDelegate:(id<AVCaptureAudioDataOutputSampleBufferDelegate>)sampleBufferDelegate queue:(dispatch_queue_t)sampleBufferCallbackQueue;
+
+/*!
+ @property sampleBufferDelegate
+ @abstract
+    The receiver's delegate.
+
+ @discussion
+    The value of this property is an object conforming to the AVCaptureAudioDataOutputSampleBufferDelegate protocol that will receive sample buffers after they are captured. The delegate is set using the setSampleBufferDelegate:queue: method.
+ */
+@property(nonatomic, readonly) id<AVCaptureAudioDataOutputSampleBufferDelegate> sampleBufferDelegate;
+
+/*!
+ @property sampleBufferCallbackQueue
+ @abstract
+    The dispatch queue on which all sample buffer delegate methods will be called.
+
+ @discussion
+    The value of this property is a dispatch_queue_t. The queue is set using the setSampleBufferDelegate:queue: method.
+ */
+@property(nonatomic, readonly) dispatch_queue_t sampleBufferCallbackQueue;
+
+#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
+
+/*!
+ @property audioSettings
+ @abstract
+    Specifies the settings used to decode or re-encode audio before it is output by the receiver.
+
+ @discussion
+    The value of this property is an NSDictionary containing values for audio settings keys defined  in AVAudioSettings.h. When audioSettings is set to nil, the AVCaptureAudioDataOutput vends samples in their device native format.
+ */
+@property(nonatomic, copy) NSDictionary *audioSettings NS_AVAILABLE(10_7, NA);
+
+#endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
+
+/*!
+ @method recommendedAudioSettingsForAssetWriterWithOutputFileType:
+ @abstract
+    Specifies the recommended settings for use with an AVAssetWriterInput.
+
+ @param outputFileType
+    Specifies the UTI of the file type to be written (see AVMediaFormat.h for a list of file format UTIs).
+ 
+ @return
+    A fully populated dictionary of keys and values that are compatible with AVAssetWriter.
+ 
+ @discussion
+    The value of this property is an NSDictionary containing values for compression settings keys defined in AVAudioSettings.h. This dictionary is suitable for use as the "outputSettings" parameter when creating an AVAssetWriterInput, such as,
+
+       [AVAssetWriterInput assetWriterInputWithMediaType:AVMediaTypeAudio outputSettings:outputSettings sourceFormatHint:hint];
+    
+    The dictionary returned contains all necessary keys and values needed by AVAssetWriter (see AVAssetWriterInput.h, -initWithMediaType:outputSettings: for a more in depth discussion). For QuickTime movie and ISO files, the recommended audio settings will always produce output comparable to that of AVCaptureMovieFileOutput.
+
+    Note that the dictionary of settings is dependent on the current configuration of the receiver's AVCaptureSession and its inputs. The settings dictionary may change if the session's configuration changes. As such, you should configure your session first, then query the recommended audio settings.
+ */
+- (NSDictionary *)recommendedAudioSettingsForAssetWriterWithOutputFileType:(NSString *)outputFileType NS_AVAILABLE_IOS(7_0);
+
+@end
+
+/*!
+ @protocol AVCaptureAudioDataOutputSampleBufferDelegate
+ @abstract
+    Defines an interface for delegates of AVCaptureAudioDataOutput to receive captured audio sample buffers.
+ */
+__TVOS_PROHIBITED
+@protocol AVCaptureAudioDataOutputSampleBufferDelegate <NSObject>
+
+@optional
+
+/*!
+ @method captureOutput:didOutputSampleBuffer:fromConnection:
+ @abstract
+    Called whenever an AVCaptureAudioDataOutput instance outputs a new audio sample buffer.
+
+ @param captureOutput
+    The AVCaptureAudioDataOutput instance that output the samples.
+ @param sampleBuffer
+    A CMSampleBuffer object containing the audio samples and additional information about them, such as their format and presentation time.
+ @param connection
+    The AVCaptureConnection from which the audio was received.
+
+ @discussion
+    Delegates receive this message whenever the output captures and outputs new audio samples, decoding or re-encoding as specified by the audioSettings property. Delegates can use the provided sample buffer in conjunction with other APIs for further processing. This method will be called on the dispatch queue specified by the output's sampleBufferCallbackQueue property. This method is called periodically, so it must be efficient to prevent capture performance problems, including dropped audio samples.
+
+    Clients that need to reference the CMSampleBuffer object outside of the scope of this method must CFRetain it and then CFRelease it when they are finished with it.
+ */
+- (void)captureOutput:(AVCaptureOutput *)captureOutput didOutputSampleBuffer:(CMSampleBufferRef)sampleBuffer fromConnection:(AVCaptureConnection *)connection;
+
+@end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureAudioPreviewOutput.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureAudioPreviewOutput.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureAudioPreviewOutput.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureAudioPreviewOutput.h	2016-05-25 07:19:43.000000000 +0200
@@ -0,0 +1,55 @@
+/*
+    File:  AVCaptureAudioPreviewOutput.h
+ 	
+ 	Framework:  AVFoundation
+ 
+	Copyright 2010-2016 Apple Inc. All rights reserved.
+*/
+
+#import <AVFoundation/AVCaptureOutput.h>
+
+
+#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
+
+#pragma mark - AVCaptureAudioPreviewOutput
+
+@class AVCaptureAudioPreviewOutputInternal;
+
+/*!
+ @class AVCaptureAudioPreviewOutput
+ @abstract
+    AVCaptureAudioPreviewOutput is a concrete subclass of AVCaptureOutput that can be used to preview the audio being captured.
+ 
+ @discussion
+    Instances of AVCaptureAudioPreviewOutput have an associated Core Audio output device that can be used to play audio being captured by the capture session. The unique ID of a Core Audio device can be obtained from its kAudioDevicePropertyDeviceUID property.
+ */
+NS_CLASS_AVAILABLE(10_7, NA) __TVOS_PROHIBITED
+@interface AVCaptureAudioPreviewOutput : AVCaptureOutput 
+{
+@private
+	AVCaptureAudioPreviewOutputInternal *_internal;
+}
+
+/*!
+ @property outputDeviceUniqueID
+ @abstract
+    Specifies the unique ID of the Core Audio output device being used to play preview audio.
+
+ @discussion
+    The value of this property is an NSString containing the unique ID of the Core Audio device to be used for output, or nil if the default system output should be used.
+ */
+@property(nonatomic, copy) NSString *outputDeviceUniqueID;
+
+/*!
+ @property volume
+ @abstract
+    Specifies the preview volume of the output.
+
+ @discussion
+    The value of this property is the preview volume of the receiver, where 1.0 is the maximum volume and 0.0 is muted. 
+ */
+@property(nonatomic) float volume;
+
+@end
+
+#endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureDevice.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureDevice.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureDevice.h	2015-09-30 23:18:01.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureDevice.h	2016-05-25 07:19:43.000000000 +0200
@@ -24,7 +24,7 @@
 
  @discussion
     The notification object is an AVCaptureDevice instance representing the device that became available.
-*/
+ */
 AVF_EXPORT NSString *const AVCaptureDeviceWasConnectedNotification NS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED;
 
 /*!
@@ -34,21 +34,17 @@
 
  @discussion
     The notification object is an AVCaptureDevice instance representing the device that became unavailable.
-*/
+ */
 AVF_EXPORT NSString *const AVCaptureDeviceWasDisconnectedNotification NS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED;
 
 /*!
  @constant  AVCaptureDeviceSubjectAreaDidChangeNotification
  @abstract
-	Posted when the instance of AVCaptureDevice has detected a substantial change
-	to the video subject area.
+    Posted when the instance of AVCaptureDevice has detected a substantial change to the video subject area.
  
  @discussion
-	Clients may observe the AVCaptureDeviceSubjectAreaDidChangeNotification to know
-	when an instance of AVCaptureDevice has detected a substantial change
-	to the video subject area.  This notification is only sent if you first set
-	subjectAreaChangeMonitoringEnabled to YES.
- */
+    Clients may observe the AVCaptureDeviceSubjectAreaDidChangeNotification to know when an instance of AVCaptureDevice has detected a substantial change to the video subject area. This notification is only sent if you first set subjectAreaChangeMonitoringEnabled to YES.
+  */
 AVF_EXPORT NSString *const AVCaptureDeviceSubjectAreaDidChangeNotification NS_AVAILABLE_IOS(5_0) __TVOS_PROHIBITED;
 
 @class AVCaptureDeviceFormat;
@@ -63,15 +59,10 @@
     An AVCaptureDevice represents a physical device that provides realtime input media data, such as video and audio.
 
  @discussion
-    Each instance of AVCaptureDevice corresponds to a device, such as a camera or microphone. Instances of
-    AVCaptureDevice cannot be created directly. An array of all currently available devices can also be obtained using
-    the devices class method. Devices can provide one or more streams of a given media type. Applications can search
-    for devices that provide media of a specific type using the devicesWithMediaType: and defaultDeviceWithMediaType:
-    class methods.
-
-    Instances of AVCaptureDevice can be used to provide media data to an AVCaptureSession by creating an
-    AVCaptureDeviceInput with the device and adding that to the capture session.
-*/
+    Each instance of AVCaptureDevice corresponds to a device, such as a camera or microphone. Instances of AVCaptureDevice cannot be created directly. An array of all currently available devices can also be obtained using the devices class method. Devices can provide one or more streams of a given media type. Applications can search for devices that provide media of a specific type using the devicesWithMediaType: and defaultDeviceWithMediaType: class methods.
+
+    Instances of AVCaptureDevice can be used to provide media data to an AVCaptureSession by creating an AVCaptureDeviceInput with the device and adding that to the capture session.
+ */
 NS_CLASS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED
 @interface AVCaptureDevice : NSObject
 {
@@ -88,11 +79,8 @@
     An NSArray of AVCaptureDevice instances for each available device.
 
  @discussion
-    This method returns an array of AVCaptureDevice instances for input devices currently connected and available for
-    capture. The returned array contains all devices that are available at the time the method is called. Applications
-    should observe AVCaptureDeviceWasConnectedNotification and AVCaptureDeviceWasDisconnectedNotification to be notified
-    when the list of available devices has changed.
-*/
+    This method returns an array of AVCaptureDevice instances for input devices currently connected and available for capture. The returned array contains all devices that are available at the time the method is called. Applications should observe AVCaptureDeviceWasConnectedNotification and AVCaptureDeviceWasDisconnectedNotification to be notified when the list of available devices has changed.
+ */
 + (NSArray *)devices;
 
 /*!
@@ -106,12 +94,8 @@
     An NSArray of AVCaptureDevice instances for each available device.
 
  @discussion
-    This method returns an array of AVCaptureDevice instances for input devices currently connected and available for
-    capture that provide media of the given type. Media type constants are defined in AVMediaFormat.h. The returned
-    array contains all devices that are available at the time the method is called. Applications should observe
-    AVCaptureDeviceWasConnectedNotification and AVCaptureDeviceWasDisconnectedNotification to be notified when the list
-    of available devices has changed.
-*/
+    This method returns an array of AVCaptureDevice instances for input devices currently connected and available for capture that provide media of the given type. Media type constants are defined in AVMediaFormat.h. The returned array contains all devices that are available at the time the method is called. Applications should observe AVCaptureDeviceWasConnectedNotification and AVCaptureDeviceWasDisconnectedNotification to be notified when the list of available devices has changed.
+ */
 + (NSArray *)devicesWithMediaType:(NSString *)mediaType;
 
 /*!
@@ -125,10 +109,8 @@
     The default device with the given media type, or nil if no device with that media type exists.
 
  @discussion
-    This method returns the default device of the given media type currently available on the system. For example, for
-    AVMediaTypeVideo, this method will return the built in camera that is primarily used for capture and recording.
-    Media type constants are defined in AVMediaFormat.h.
-*/
+    This method returns the default device of the given media type currently available on the system. For example, for AVMediaTypeVideo, this method will return the built in camera that is primarily used for capture and recording. Media type constants are defined in AVMediaFormat.h.
+ */
 + (AVCaptureDevice *)defaultDeviceWithMediaType:(NSString *)mediaType;
 
 /*!
@@ -142,10 +124,8 @@
     An AVCaptureDevice instance with the given unique ID, or nil if no device with that unique ID is available.
 
  @discussion
-    Every available capture device has a unique ID that persists on one system across device connections and
-    disconnections, application restarts, and reboots of the system itself. This method can be used to recall or track
-    the status of a specific device whose unique ID has previously been saved.
-*/
+    Every available capture device has a unique ID that persists on one system across device connections and disconnections, application restarts, and reboots of the system itself. This method can be used to recall or track the status of a specific device whose unique ID has previously been saved.
+ */
 + (AVCaptureDevice *)deviceWithUniqueID:(NSString *)deviceUniqueID;
 
 /*!
@@ -154,10 +134,8 @@
     An ID unique to the model of device corresponding to the receiver.
 
  @discussion
-    Every available capture device has a unique ID that persists on one system across device connections and
-    disconnections, application restarts, and reboots of the system itself. Applications can store the value returned by
-    this property to recall or track the status of a specific device in the future.
-*/
+    Every available capture device has a unique ID that persists on one system across device connections and disconnections, application restarts, and reboots of the system itself. Applications can store the value returned by this property to recall or track the status of a specific device in the future.
+ */
 @property(nonatomic, readonly) NSString *uniqueID;
 
 /*!
@@ -166,10 +144,8 @@
     The model ID of the receiver.
 
  @discussion
-    The value of this property is an identifier unique to all devices of the same model. The value is persistent across
-    device connections and disconnections, and across different systems. For example, the model ID of the camera built
-    in to two identical iPhone models will be the same even though they are different physical devices.
-*/
+    The value of this property is an identifier unique to all devices of the same model. The value is persistent across device connections and disconnections, and across different systems. For example, the model ID of the camera built in to two identical iPhone models will be the same even though they are different physical devices.
+ */
 @property(nonatomic, readonly) NSString *modelID;
 
 /*!
@@ -179,7 +155,7 @@
  
  @discussion
     This property can be used for displaying the name of a capture device in a user interface.
-*/
+ */
 @property(nonatomic, readonly) NSString *localizedName;
 
 #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
@@ -190,9 +166,8 @@
     The human-readable manufacturer name for the receiver.
 
  @discussion
-    This property can be used to identify capture devices from a particular manufacturer.  All Apple devices return "Apple Inc.".
-    Devices from third party manufacturers may return an empty string.
-*/
+    This property can be used to identify capture devices from a particular manufacturer. All Apple devices return "Apple Inc.". Devices from third party manufacturers may return an empty string.
+ */
 @property(nonatomic, readonly) NSString *manufacturer NS_AVAILABLE(10_9, NA);
 
 /*!
@@ -201,9 +176,8 @@
     The transport type of the receiver (e.g. USB, PCI, etc).
 
  @discussion
-    This property can be used to discover the transport type of a capture device.  Transport types
-    are defined in <IOKit/audio/IOAudioTypes.h> as kIOAudioDeviceTransportType*.
-*/
+    This property can be used to discover the transport type of a capture device. Transport types are defined in <IOKit/audio/IOAudioTypes.h> as kIOAudioDeviceTransportType*.
+ */
 @property(nonatomic, readonly) int32_t transportType NS_AVAILABLE(10_7, NA);
 
 #endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
@@ -220,7 +194,7 @@
  
  @discussion
     Media type constants are defined in AVMediaFormat.h.
-*/
+ */
 - (BOOL)hasMediaType:(NSString *)mediaType;
 
 
@@ -235,11 +209,8 @@
     A BOOL indicating whether the device was successfully locked for configuration.
 
  @discussion
-    In order to set hardware properties on an AVCaptureDevice, such as focusMode and exposureMode, clients must first
-    acquire a lock on the device.  Clients should only hold the device lock if they require settable device properties
-    to remain unchanged.  Holding the device lock unnecessarily may degrade capture quality in other applications
-    sharing the device.
-*/
+    In order to set hardware properties on an AVCaptureDevice, such as focusMode and exposureMode, clients must first acquire a lock on the device. Clients should only hold the device lock if they require settable device properties to remain unchanged. Holding the device lock unnecessarily may degrade capture quality in other applications sharing the device.
+ */
 - (BOOL)lockForConfiguration:(NSError **)outError;
 
 /*!
@@ -248,9 +219,8 @@
     Release exclusive control over device hardware properties.
 
  @discussion
-    This method should be called to match an invocation of lockForConfiguration: when an application no longer needs to
-    keep device hardware properties from changing automatically.
-*/
+    This method should be called to match an invocation of lockForConfiguration: when an application no longer needs to keep device hardware properties from changing automatically.
+ */
 - (void)unlockForConfiguration;
 
 /*!
@@ -264,10 +234,8 @@
     YES if the receiver can be used with the given preset, NO otherwise.
 
  @discussion
-    An AVCaptureSession instance can be associated with a preset that configures its inputs and outputs to fulfill common
-    use cases. This method can be used to determine if the receiver can be used in a capture session with the given
-    preset. Presets are defined in AVCaptureSession.h.
-*/
+    An AVCaptureSession instance can be associated with a preset that configures its inputs and outputs to fulfill common use cases. This method can be used to determine if the receiver can be used in a capture session with the given preset. Presets are defined in AVCaptureSession.h.
+ */
 - (BOOL)supportsAVCaptureSessionPreset:(NSString *)preset;
 
 /*!
@@ -276,12 +244,8 @@
     Indicates whether the device is connected and available to the system.
 
  @discussion
-    The value of this property is a BOOL indicating whether the device represented by the receiver is connected and
-    available for use as a capture device. Clients can key value observe the value of this property to be notified when
-    a device is no longer available. When the value of this property becomes NO for a given instance, it will not become
-    YES again. If the same physical device again becomes available to the system, it will be represented using a new
-    instance of AVCaptureDevice.
-*/
+    The value of this property is a BOOL indicating whether the device represented by the receiver is connected and available for use as a capture device. Clients can key value observe the value of this property to be notified when a device is no longer available. When the value of this property becomes NO for a given instance, it will not become YES again. If the same physical device again becomes available to the system, it will be represented using a new instance of AVCaptureDevice.
+ */
 @property(nonatomic, readonly, getter=isConnected) BOOL connected;
 
 #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
@@ -292,10 +256,8 @@
     Indicates whether the device is in use by another application.
 
  @discussion
-    The value of this property is a BOOL indicating whether the device represented by the receiver is
-    in use by another application. Clients can key value observe the value of this property to be notified when
-    another app starts or stops using this device.
-*/
+    The value of this property is a BOOL indicating whether the device represented by the receiver is in use by another application. Clients can key value observe the value of this property to be notified when another app starts or stops using this device.
+ */
 @property(nonatomic, readonly, getter=isInUseByAnotherApplication) BOOL inUseByAnotherApplication NS_AVAILABLE(10_7, NA);
 
 /*!
@@ -304,12 +266,8 @@
     Indicates whether the device is suspended.
 
  @discussion
-    The value of this property is a BOOL indicating whether the device represented by the receiver is
-    currently suspended.  Some devices disallow data capture due to a feature on the device.
-    For example, isSuspended returns YES for the external iSight when its privacy iris is closed, or 
-    for the internal iSight on a notebook when the notebook's display is closed.  Clients can key value 
-    observe the value of this property to be notified when the device becomes suspended or unsuspended.
-*/
+    The value of this property is a BOOL indicating whether the device represented by the receiver is currently suspended. Some devices disallow data capture due to a feature on the device. For example, isSuspended returns YES for the external iSight when its privacy iris is closed, or for the internal iSight on a notebook when the notebook's display is closed. Clients can key value observe the value of this property to be notified when the device becomes suspended or unsuspended.
+ */
 @property(nonatomic, readonly, getter=isSuspended) BOOL suspended NS_AVAILABLE(10_7, NA);
 
 /*!
@@ -318,10 +276,8 @@
     An array of AVCaptureDevice objects physically linked to the receiver.
 
  @discussion
-    The value of this property is an array of AVCaptureDevice objects that are a part of the same physical 
-    device as the receiver.  For example, for the external iSight camera, linkedDevices returns an array 
-    containing an AVCaptureDevice for the external iSight microphone.
-*/
+    The value of this property is an array of AVCaptureDevice objects that are a part of the same physical device as the receiver. For example, for the external iSight camera, linkedDevices returns an array containing an AVCaptureDevice for the external iSight microphone.
+ */
 @property(nonatomic, readonly) NSArray *linkedDevices NS_AVAILABLE(10_7, NA);
 
 #endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
@@ -332,10 +288,8 @@
     An array of AVCaptureDeviceFormat objects supported by the receiver.
 
  @discussion
-    This property can be used to enumerate the formats natively supported by the receiver.  The
-    capture device's activeFormat property may be set to one of the formats in this array.  Clients 
-    can observe automatic changes to the receiver's formats by key value observing this property.
-*/
+    This property can be used to enumerate the formats natively supported by the receiver. The capture device's activeFormat property may be set to one of the formats in this array. Clients can observe automatic changes to the receiver's formats by key value observing this property.
+ */
 @property(nonatomic, readonly) NSArray *formats NS_AVAILABLE(10_7, 7_0);
 
 /*!
@@ -344,34 +298,23 @@
     The currently active format of the receiver.
 
  @discussion
-    This property can be used to get or set the currently active device format.
-    -setActiveFormat: throws an NSInvalidArgumentException if set to a format not present in the formats
-    array.  -setActiveFormat: throws an NSGenericException if called without first obtaining exclusive
-    access to the receiver using lockForConfiguration:.  Clients can observe automatic changes to the 
-    receiver's activeFormat by key value observing this property.
- 
-    On iOS, use of AVCaptureDevice's setActiveFormat: and AVCaptureSession's setSessionPreset: are mutually
-    exclusive.  If you set a capture device's active format, the session to which it is attached changes its
-    preset to AVCaptureSessionPresetInputPriority.  Likewise if you set the AVCaptureSession's sessionPreset
-    property, the session assumes control of its input devices, and configures their activeFormat appropriately.
-    Note that audio devices do not expose any user-configurable formats on iOS.  To configure audio input on
-    iOS, you should use the AVAudioSession APIs instead (see AVAudioSession.h).
+    This property can be used to get or set the currently active device format. -setActiveFormat: throws an NSInvalidArgumentException if set to a format not present in the formats array. -setActiveFormat: throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:. Clients can observe automatic changes to the receiver's activeFormat by key value observing this property.
+ 
+    On iOS, use of AVCaptureDevice's setActiveFormat: and AVCaptureSession's setSessionPreset: are mutually exclusive. If you set a capture device's active format, the session to which it is attached changes its preset to AVCaptureSessionPresetInputPriority. Likewise if you set the AVCaptureSession's sessionPreset property, the session assumes control of its input devices, and configures their activeFormat appropriately. Note that audio devices do not expose any user-configurable formats on iOS. To configure audio input on iOS, you should use the AVAudioSession APIs instead (see AVAudioSession.h).
     
-    The activeFormat, activeVideoMinFrameDuration, and activeVideoMaxFrameDuration properties may be set simultaneously
-    by using AVCaptureSession's begin/commitConfiguration methods:
+    The activeFormat, activeVideoMinFrameDuration, and activeVideoMaxFrameDuration properties may be set simultaneously by using AVCaptureSession's begin/commitConfiguration methods:
  
     [session beginConfiguration]; // the session to which the receiver's AVCaptureDeviceInput is added.
     if ( [device lockForConfiguration:&error] ) {
         [device setActiveFormat:newFormat];
         [device setActiveVideoMinFrameDuration:newMinDuration];
         [device setActiveVideoMaxFrameDuration:newMaxDuration];
-	    [device unlockForConfiguration];
+        [device unlockForConfiguration];
     }
     [session commitConfiguration]; // The new format and frame rates are applied together in commitConfiguration
  
-	Note that when configuring a session to use an active format intended for high resolution still photography and applying one or more of the
-	following operations to an AVCaptureVideoDataOutput, the system may not meet the target framerate: zoom, orientation changes, format conversion.
-*/
+    Note that when configuring a session to use an active format intended for high resolution still photography and applying one or more of the following operations to an AVCaptureVideoDataOutput, the system may not meet the target framerate: zoom, orientation changes, format conversion.
+ */
 @property(nonatomic, retain) AVCaptureDeviceFormat *activeFormat NS_AVAILABLE(10_7, 7_0);
 
 /*!
@@ -380,25 +323,15 @@
     A property indicating the receiver's current active minimum frame duration (the reciprocal of its max frame rate).
 
  @discussion
-    An AVCaptureDevice's activeVideoMinFrameDuration property is the reciprocal of its active
-    maximum frame rate.  To limit the max frame rate of the capture device, clients may
-    set this property to a value supported by the receiver's activeFormat (see AVCaptureDeviceFormat's 
-    videoSupportedFrameRateRanges property).  Clients may set this property's value to kCMTimeInvalid to
-    return activeVideoMinFrameDuration to its default value for the given activeFormat.
-    -setActiveVideoMinFrameDuration: throws an NSInvalidArgumentException if set to an unsupported value.  
-    -setActiveVideoMinFrameDuration: throws an NSGenericException if called without first obtaining exclusive 
-    access to the receiver using lockForConfiguration:.  Clients can observe automatic changes to the receiver's 
-    activeVideoMinFrameDuration by key value observing this property.
+    An AVCaptureDevice's activeVideoMinFrameDuration property is the reciprocal of its active maximum frame rate. To limit the max frame rate of the capture device, clients may set this property to a value supported by the receiver's activeFormat (see AVCaptureDeviceFormat's videoSupportedFrameRateRanges property). Clients may set this property's value to kCMTimeInvalid to return activeVideoMinFrameDuration to its default value for the given activeFormat. -setActiveVideoMinFrameDuration: throws an NSInvalidArgumentException if set to an unsupported value. -setActiveVideoMinFrameDuration: throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:. Clients can observe automatic changes to the receiver's activeVideoMinFrameDuration by key value observing this property.
  
     On iOS, the receiver's activeVideoMinFrameDuration resets to its default value under the following conditions:
-	    - The receiver's activeFormat changes
+        - The receiver's activeFormat changes
         - The receiver's AVCaptureDeviceInput's session's sessionPreset changes
         - The receiver's AVCaptureDeviceInput is added to a session
  
-    When exposureMode is AVCaptureExposureModeCustom, setting the activeVideoMinFrameDuration affects max frame
-    rate, but not exposureDuration. You may use setExposureModeCustomWithDuration:ISO:completionHandler:
-    to set a shorter exposureDuration than your activeVideoMinFrameDuration, if desired.
-*/
+    When exposureMode is AVCaptureExposureModeCustom, setting the activeVideoMinFrameDuration affects max frame rate, but not exposureDuration. You may use setExposureModeCustomWithDuration:ISO:completionHandler: to set a shorter exposureDuration than your activeVideoMinFrameDuration, if desired.
+ */
 @property(nonatomic) CMTime activeVideoMinFrameDuration NS_AVAILABLE(10_7, 7_0);
 
 /*!
@@ -407,30 +340,15 @@
     A property indicating the receiver's current active maximum frame duration (the reciprocal of its min frame rate).
 
  @discussion
-    An AVCaptureDevice's activeVideoMaxFrameDuration property is the reciprocal of its active
-    minimum frame rate.  To limit the min frame rate of the capture device, clients may
-    set this property to a value supported by the receiver's activeFormat (see AVCaptureDeviceFormat's 
-    videoSupportedFrameRateRanges property).  Clients may set this property's value to kCMTimeInvalid to
-    return activeVideoMaxFrameDuration to its default value for the given activeFormat.
-    -setActiveVideoMaxFrameDuration: throws an NSInvalidArgumentException if set to an unsupported value.  
-    -setActiveVideoMaxFrameDuration: throws an NSGenericException if called without first obtaining exclusive 
-    access to the receiver using lockForConfiguration:.  Clients can observe automatic changes to the receiver's 
-    activeVideoMaxFrameDuration by key value observing this property.
+    An AVCaptureDevice's activeVideoMaxFrameDuration property is the reciprocal of its active minimum frame rate. To limit the min frame rate of the capture device, clients may set this property to a value supported by the receiver's activeFormat (see AVCaptureDeviceFormat's videoSupportedFrameRateRanges property). Clients may set this property's value to kCMTimeInvalid to return activeVideoMaxFrameDuration to its default value for the given activeFormat. -setActiveVideoMaxFrameDuration: throws an NSInvalidArgumentException if set to an unsupported value. -setActiveVideoMaxFrameDuration: throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:. Clients can observe automatic changes to the receiver's activeVideoMaxFrameDuration by key value observing this property.
  
     On iOS, the receiver's activeVideoMaxFrameDuration resets to its default value under the following conditions:
-	    - The receiver's activeFormat changes
+        - The receiver's activeFormat changes
         - The receiver's AVCaptureDeviceInput's session's sessionPreset changes
         - The receiver's AVCaptureDeviceInput is added to a session
  
-    When exposureMode is AVCaptureExposureModeCustom, frame rate and exposure duration are interrelated.
-    If you call setExposureModeCustomWithDuration:ISO:completionHandler: with an exposureDuration longer 
-    than the current activeVideoMaxFrameDuration, the activeVideoMaxFrameDuration will be lengthened to
-    accommodate the longer exposure time.  Setting a shorter exposure duration does not automatically
-    change the activeVideoMinFrameDuration or activeVideoMaxFrameDuration. To explicitly increase the
-    frame rate in custom exposure mode, you must set the activeVideoMaxFrameDuration to a shorter value.
-    If your new max frame duration is shorter than the current exposureDuration, the exposureDuration will
-    shorten as well to accommodate the new frame rate.
-*/
+    When exposureMode is AVCaptureExposureModeCustom, frame rate and exposure duration are interrelated. If you call setExposureModeCustomWithDuration:ISO:completionHandler: with an exposureDuration longer than the current activeVideoMaxFrameDuration, the activeVideoMaxFrameDuration will be lengthened to accommodate the longer exposure time. Setting a shorter exposure duration does not automatically change the activeVideoMinFrameDuration or activeVideoMaxFrameDuration. To explicitly increase the frame rate in custom exposure mode, you must set the activeVideoMaxFrameDuration to a shorter value. If your new max frame duration is shorter than the current exposureDuration, the exposureDuration will shorten as well to accommodate the new frame rate.
+ */
 @property(nonatomic) CMTime activeVideoMaxFrameDuration NS_AVAILABLE(10_9, 7_0);
 
 #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
@@ -441,11 +359,8 @@
     An array of AVCaptureDeviceInputSource objects supported by the receiver.
  
  @discussion
-    Some devices can capture data from one of multiple data sources (different input jacks on the same 
-    audio device, for example).  For devices with multiple possible data sources, inputSources can be 
-    used to enumerate the possible choices. Clients can observe automatic changes to the receiver's 
-    inputSources by key value observing this property.
-*/
+    Some devices can capture data from one of multiple data sources (different input jacks on the same audio device, for example). For devices with multiple possible data sources, inputSources can be used to enumerate the possible choices. Clients can observe automatic changes to the receiver's inputSources by key value observing this property.
+ */
 @property(nonatomic, readonly) NSArray *inputSources NS_AVAILABLE(10_7, NA);
 
 /*!
@@ -454,12 +369,8 @@
     The currently active input source of the receiver.
 
  @discussion
-    This property can be used to get or set the currently active device input source.
-    -setActiveInputSource: throws an NSInvalidArgumentException if set to a value not present in the
-    inputSources array.  -setActiveInputSource: throws an NSGenericException if called without first 
-    obtaining exclusive access to the receiver using lockForConfiguration:.  Clients can observe automatic  
-    changes to the receiver's activeInputSource by key value observing this property.
-*/
+    This property can be used to get or set the currently active device input source. -setActiveInputSource: throws an NSInvalidArgumentException if set to a value not present in the inputSources array. -setActiveInputSource: throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:. Clients can observe automatic changes to the receiver's activeInputSource by key value observing this property.
+ */
 @property(nonatomic, retain) AVCaptureDeviceInputSource *activeInputSource NS_AVAILABLE(10_7, NA);
 
 #endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
@@ -478,7 +389,7 @@
     Indicates that the device is physically located on the back of the system hardware.
  @constant AVCaptureDevicePositionFront
     Indicates that the device is physically located on the front of the system hardware.
-*/
+ */
 typedef NS_ENUM(NSInteger, AVCaptureDevicePosition) {
 	AVCaptureDevicePositionUnspecified         = 0,
 	AVCaptureDevicePositionBack                = 1,
@@ -493,9 +404,8 @@
     Indicates the physical position of an AVCaptureDevice's hardware on the system.
 
  @discussion
-    The value of this property is an AVCaptureDevicePosition indicating where the receiver's device is physically
-    located on the system hardware.
-*/
+    The value of this property is an AVCaptureDevicePosition indicating where the receiver's device is physically located on the system hardware.
+ */
 @property(nonatomic, readonly) AVCaptureDevicePosition position;
 
 @end
@@ -511,7 +421,7 @@
     Indicates that the flash should always be on.
  @constant AVCaptureFlashModeAuto
     Indicates that the flash should be used automatically depending on ambient light conditions.
-*/
+ */
 typedef NS_ENUM(NSInteger, AVCaptureFlashMode) {
 	AVCaptureFlashModeOff  = 0,
 	AVCaptureFlashModeOn   = 1,
@@ -526,9 +436,8 @@
     Indicates whether the receiver has a flash.
 
  @discussion
-    The value of this property is a BOOL indicating whether the receiver has a flash. The receiver's flashMode property
-    can only be set when this property returns YES.
-*/
+    The value of this property is a BOOL indicating whether the receiver has a flash. The receiver's flashMode property can only be set when this property returns YES.
+ */
 @property(nonatomic, readonly) BOOL hasFlash;
 
 /*!
@@ -537,10 +446,8 @@
     Indicates whether the receiver's flash is currently available for use.
  
  @discussion
-    The value of this property is a BOOL indicating whether the receiver's flash is 
-    currently available. The flash may become unavailable if, for example, the device
-    overheats and needs to cool off. This property is key-value observable.
-*/
+    The value of this property is a BOOL indicating whether the receiver's flash is currently available. The flash may become unavailable if, for example, the device overheats and needs to cool off. This property is key-value observable.
+ */
 @property(nonatomic, readonly, getter=isFlashAvailable) BOOL flashAvailable NS_AVAILABLE_IOS(5_0);
 
 /*!
@@ -549,14 +456,9 @@
     Indicates whether the receiver's flash is currently active.
  
  @discussion
-    The value of this property is a BOOL indicating whether the receiver's flash is 
-    currently active. When the flash is active, it will flash if a still image is
-    captured. When a still image is captured with the flash active, exposure and
-    white balance settings are overridden for the still. This is true even when
-    using AVCaptureExposureModeCustom and/or AVCaptureWhiteBalanceModeLocked.
-    This property is key-value observable.
-*/
-@property(nonatomic, readonly, getter=isFlashActive) BOOL flashActive NS_AVAILABLE_IOS(5_0);
+    The value of this property is a BOOL indicating whether the receiver's flash is currently active. When the flash is active, it will flash if a still image is captured. When a still image is captured with the flash active, exposure and white balance settings are overridden for the still. This is true even when using AVCaptureExposureModeCustom and/or AVCaptureWhiteBalanceModeLocked. This property is key-value observable.
+ */
+@property(nonatomic, readonly, getter=isFlashActive) BOOL flashActive NS_DEPRECATED_IOS(5_0, 10_0, "Use AVCapturePhotoOutput's -isFlashScene instead.");
 
 /*!
  @method isFlashModeSupported:
@@ -570,8 +472,8 @@
 
  @discussion
     The receiver's flashMode property can only be set to a certain mode if this method returns YES for that mode.
-*/
-- (BOOL)isFlashModeSupported:(AVCaptureFlashMode)flashMode;
+ */
+- (BOOL)isFlashModeSupported:(AVCaptureFlashMode)flashMode NS_DEPRECATED(10_7, NA, 4_0, 10_0, "Use AVCapturePhotoOutput's -supportedFlashModes instead.");
 
 /*!
  @property flashMode
@@ -579,13 +481,11 @@
     Indicates current mode of the receiver's flash, if it has one.
 
  @discussion
-    The value of this property is an AVCaptureFlashMode that determines the mode of the 
-    receiver's flash, if it has one.  -setFlashMode: throws an NSInvalidArgumentException
-    if set to an unsupported value (see -isFlashModeSupported:).  -setFlashMode: throws an NSGenericException 
-    if called without first obtaining exclusive access to the receiver using lockForConfiguration:.
-    Clients can observe automatic changes to the receiver's flashMode by key value observing this property.
-*/
-@property(nonatomic) AVCaptureFlashMode flashMode;
+    The value of this property is an AVCaptureFlashMode that determines the mode of the receiver's flash, if it has one. -setFlashMode: throws an NSInvalidArgumentException if set to an unsupported value (see -isFlashModeSupported:). -setFlashMode: throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:. Clients can observe automatic changes to the receiver's flashMode by key value observing this property.
+ 
+    When using AVCapturePhotoOutput, AVCaptureDevice's flashMode property is ignored. You specify flashMode on a per photo basis by setting the AVCapturePhotoSettings.flashMode property.
+ */
+@property(nonatomic) AVCaptureFlashMode flashMode NS_DEPRECATED(10_7, NA, 4_0, 10_0, "Use AVCapturePhotoSettings.flashMode instead.");
 
 @end
 
@@ -600,7 +500,7 @@
     Indicates that the torch should always be on.
  @constant AVCaptureTorchModeAuto
     Indicates that the torch should be used automatically depending on ambient light conditions.
-*/
+ */
 typedef NS_ENUM(NSInteger, AVCaptureTorchMode) {
 	AVCaptureTorchModeOff  = 0,
 	AVCaptureTorchModeOn   = 1,
@@ -608,11 +508,9 @@
 } NS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED;
 
 /*!
-  @constant AVCaptureMaxAvailableTorchLevel
-    A special value that may be passed to -setTorchModeWithLevel:error: to set the torch to the
-    maximum level currently available. Under thermal duress, the maximum available torch level
-    may be less than 1.0.
-*/
+ @constant AVCaptureMaxAvailableTorchLevel
+    A special value that may be passed to -setTorchModeWithLevel:error: to set the torch to the maximum level currently available. Under thermal duress, the maximum available torch level may be less than 1.0.
+ */
 extern const float AVCaptureMaxAvailableTorchLevel;
 
 @interface AVCaptureDevice (AVCaptureDeviceTorch)
@@ -623,9 +521,8 @@
     Indicates whether the receiver has a torch.
 
  @discussion
-    The value of this property is a BOOL indicating whether the receiver has a torch. The receiver's torchMode property
-    can only be set when this property returns YES.
-*/
+    The value of this property is a BOOL indicating whether the receiver has a torch. The receiver's torchMode property can only be set when this property returns YES.
+ */
 @property(nonatomic, readonly) BOOL hasTorch;
 
 /*!
@@ -634,10 +531,8 @@
     Indicates whether the receiver's torch is currently available for use.
  
  @discussion
-    The value of this property is a BOOL indicating whether the receiver's torch is 
-    currently available. The torch may become unavailable if, for example, the device
-    overheats and needs to cool off. This property is key-value observable.
-*/
+    The value of this property is a BOOL indicating whether the receiver's torch is currently available. The torch may become unavailable if, for example, the device overheats and needs to cool off. This property is key-value observable.
+ */
 @property(nonatomic, readonly, getter=isTorchAvailable) BOOL torchAvailable NS_AVAILABLE_IOS(5_0);
 
 /*!
@@ -646,11 +541,8 @@
     Indicates whether the receiver's torch is currently active.
  
  @discussion
-    The value of this property is a BOOL indicating whether the receiver's torch is 
-    currently active. If the current torchMode is AVCaptureTorchModeAuto and isTorchActive
-    is YES, the torch will illuminate once a recording starts (see AVCaptureOutput.h 
-    -startRecordingToOutputFileURL:recordingDelegate:). This property is key-value observable.
-*/
+    The value of this property is a BOOL indicating whether the receiver's torch is currently active. If the current torchMode is AVCaptureTorchModeAuto and isTorchActive is YES, the torch will illuminate once a recording starts (see AVCaptureOutput.h -startRecordingToOutputFileURL:recordingDelegate:). This property is key-value observable.
+ */
 @property(nonatomic, readonly, getter=isTorchActive) BOOL torchActive NS_AVAILABLE_IOS(6_0);
 
 /*!
@@ -659,9 +551,8 @@
     Indicates the receiver's current torch brightness level as a floating point value.
 
  @discussion
-    The value of this property is a float indicating the receiver's torch level 
-    from 0.0 (off) -> 1.0 (full). This property is key-value observable.
-*/
+    The value of this property is a float indicating the receiver's torch level from 0.0 (off) -> 1.0 (full). This property is key-value observable.
+ */
 @property(nonatomic, readonly) float torchLevel NS_AVAILABLE_IOS(5_0);
 
 /*!
@@ -676,7 +567,7 @@
 
  @discussion
     The receiver's torchMode property can only be set to a certain mode if this method returns YES for that mode.
-*/
+ */
 - (BOOL)isTorchModeSupported:(AVCaptureTorchMode)torchMode;
 
 /*!
@@ -685,12 +576,8 @@
     Indicates current mode of the receiver's torch, if it has one.
 
  @discussion
-    The value of this property is an AVCaptureTorchMode that determines the mode of the 
-    receiver's torch, if it has one.  -setTorchMode: throws an NSInvalidArgumentException
-    if set to an unsupported value (see -isTorchModeSupported:).  -setTorchMode: throws an NSGenericException 
-    if called without first obtaining exclusive access to the receiver using lockForConfiguration:.
-    Clients can observe automatic changes to the receiver's torchMode by key value observing this property.
-*/
+    The value of this property is an AVCaptureTorchMode that determines the mode of the receiver's torch, if it has one. -setTorchMode: throws an NSInvalidArgumentException if set to an unsupported value (see -isTorchModeSupported:). -setTorchMode: throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:. Clients can observe automatic changes to the receiver's torchMode by key value observing this property.
+ */
 @property(nonatomic) AVCaptureTorchMode torchMode;
 
 /*!
@@ -699,15 +586,8 @@
     Sets the current mode of the receiver's torch to AVCaptureTorchModeOn at the specified level.
 
  @discussion
-    This method sets the torch mode to AVCaptureTorchModeOn at a specified level.  torchLevel must be 
-    a value between 0 and 1, or the special value AVCaptureMaxAvailableTorchLevel.  The specified value
-    may not be available if the iOS device is too hot. This method throws an NSInvalidArgumentException
-    if set to an unsupported level. If the specified level is valid, but unavailable, the method returns
-    NO with AVErrorTorchLevelUnavailable.  -setTorchModeOnWithLevel:error: throws an NSGenericException 
-    if called without first obtaining exclusive access to the receiver using lockForConfiguration:.
-    Clients can observe automatic changes to the receiver's torchMode by key value observing the torchMode 
-    property.
-*/
+    This method sets the torch mode to AVCaptureTorchModeOn at a specified level. torchLevel must be a value between 0 and 1, or the special value AVCaptureMaxAvailableTorchLevel. The specified value may not be available if the iOS device is too hot. This method throws an NSInvalidArgumentException if set to an unsupported level. If the specified level is valid, but unavailable, the method returns NO with AVErrorTorchLevelUnavailable. -setTorchModeOnWithLevel:error: throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:. Clients can observe automatic changes to the receiver's torchMode by key value observing the torchMode property.
+ */
 - (BOOL)setTorchModeOnWithLevel:(float)torchLevel error:(NSError **)outError NS_AVAILABLE_IOS(6_0);
 
 @end
@@ -723,7 +603,7 @@
     Indicates that the device should autofocus once and then change the focus mode to AVCaptureFocusModeLocked.
  @constant AVCaptureFocusModeContinuousAutoFocus
     Indicates that the device should automatically focus when needed.
-*/
+ */
 typedef NS_ENUM(NSInteger, AVCaptureFocusMode) {
 	AVCaptureFocusModeLocked              = 0,
 	AVCaptureFocusModeAutoFocus           = 1,
@@ -733,15 +613,15 @@
 /*!
  @enum AVCaptureAutoFocusRangeRestriction
  @abstract
-	Constants indicating the restriction of the receiver's autofocus system to a particular range of focus scan, if it supports range restrictions.
+    Constants indicating the restriction of the receiver's autofocus system to a particular range of focus scan, if it supports range restrictions.
  
  @constant AVCaptureAutoFocusRangeRestrictionNone
-	Indicates that the autofocus system should not restrict the focus range.
+    Indicates that the autofocus system should not restrict the focus range.
  @constant AVCaptureAutoFocusRangeRestrictionNear
-	Indicates that the autofocus system should restrict the focus range for subject matter that is near to the camera.
+    Indicates that the autofocus system should restrict the focus range for subject matter that is near to the camera.
  @constant AVCaptureAutoFocusRangeRestrictionFar
-	Indicates that the autofocus system should restrict the focus range for subject matter that is far from the camera.
-*/
+    Indicates that the autofocus system should restrict the focus range for subject matter that is far from the camera.
+ */
 typedef NS_ENUM(NSInteger, AVCaptureAutoFocusRangeRestriction) {
 	AVCaptureAutoFocusRangeRestrictionNone = 0,
 	AVCaptureAutoFocusRangeRestrictionNear = 1,
@@ -762,7 +642,7 @@
 
  @discussion
     The receiver's focusMode property can only be set to a certain mode if this method returns YES for that mode.
-*/
+ */
 - (BOOL)isFocusModeSupported:(AVCaptureFocusMode)focusMode;
 
 /*!
@@ -771,12 +651,8 @@
     Indicates current focus mode of the receiver, if it has one.
 
  @discussion
-    The value of this property is an AVCaptureFocusMode that determines the receiver's focus mode, if it has one.
-    -setFocusMode: throws an NSInvalidArgumentException if set to an unsupported value (see -isFocusModeSupported:).  
-    -setFocusMode: throws an NSGenericException if called without first obtaining exclusive access to the receiver 
-    using lockForConfiguration:.  Clients can observe automatic changes to the receiver's focusMode by key value 
-    observing this property.
-*/
+    The value of this property is an AVCaptureFocusMode that determines the receiver's focus mode, if it has one. -setFocusMode: throws an NSInvalidArgumentException if set to an unsupported value (see -isFocusModeSupported:). -setFocusMode: throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:. Clients can observe automatic changes to the receiver's focusMode by key value observing this property.
+ */
 @property(nonatomic) AVCaptureFocusMode focusMode;
 
 /*!
@@ -786,7 +662,7 @@
 
  @discussion
     The receiver's focusPointOfInterest property can only be set if this property returns YES.
-*/
+ */
 @property(nonatomic, readonly, getter=isFocusPointOfInterestSupported) BOOL focusPointOfInterestSupported;
 
 /*!
@@ -795,15 +671,8 @@
     Indicates current focus point of interest of the receiver, if it has one.
 
  @discussion
-    The value of this property is a CGPoint that determines the receiver's focus point of interest, if it has one. A
-    value of (0,0) indicates that the camera should focus on the top left corner of the image, while a value of (1,1)
-    indicates that it should focus on the bottom right. The default value is (0.5,0.5).  -setFocusPointOfInterest:
-    throws an NSInvalidArgumentException if isFocusPointOfInterestSupported returns NO.  -setFocusPointOfInterest: throws 
-    an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:.  
-    Clients can observe automatic changes to the receiver's focusPointOfInterest by key value observing this property.  Note that
-    setting focusPointOfInterest alone does not initiate a focus operation.  After setting focusPointOfInterest, call
-    -setFocusMode: to apply the new point of interest.
-*/
+    The value of this property is a CGPoint that determines the receiver's focus point of interest, if it has one. A value of (0,0) indicates that the camera should focus on the top left corner of the image, while a value of (1,1) indicates that it should focus on the bottom right. The default value is (0.5,0.5). -setFocusPointOfInterest: throws an NSInvalidArgumentException if isFocusPointOfInterestSupported returns NO. -setFocusPointOfInterest: throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:. Clients can observe automatic changes to the receiver's focusPointOfInterest by key value observing this property. Note that setting focusPointOfInterest alone does not initiate a focus operation. After setting focusPointOfInterest, call -setFocusMode: to apply the new point of interest.
+ */
 @property(nonatomic) CGPoint focusPointOfInterest;
 
 /*!
@@ -812,66 +681,49 @@
     Indicates whether the receiver is currently performing a focus scan to adjust focus.
 
  @discussion
-    The value of this property is a BOOL indicating whether the receiver's camera focus is being automatically
-    adjusted by means of a focus scan, because its focus mode is AVCaptureFocusModeAutoFocus or
-	AVCaptureFocusModeContinuousAutoFocus.
-    Clients can observe the value of this property to determine whether the camera's focus is stable.
-	@seealso lensPosition
-	@seealso AVCaptureAutoFocusSystem
-*/
+    The value of this property is a BOOL indicating whether the receiver's camera focus is being automatically adjusted by means of a focus scan, because its focus mode is AVCaptureFocusModeAutoFocus or AVCaptureFocusModeContinuousAutoFocus. Clients can observe the value of this property to determine whether the camera's focus is stable.
+ @seealso lensPosition
+ @seealso AVCaptureAutoFocusSystem
+ */
 @property(nonatomic, readonly, getter=isAdjustingFocus) BOOL adjustingFocus;
 
 /*!
  @property autoFocusRangeRestrictionSupported
  @abstract
-	Indicates whether the receiver supports autofocus range restrictions.
+    Indicates whether the receiver supports autofocus range restrictions.
  
  @discussion
-	The receiver's autoFocusRangeRestriction property can only be set if this property returns YES.
+    The receiver's autoFocusRangeRestriction property can only be set if this property returns YES.
  */
 @property(nonatomic, readonly, getter=isAutoFocusRangeRestrictionSupported) BOOL autoFocusRangeRestrictionSupported NS_AVAILABLE_IOS(7_0);
 
 /*!
  @property autoFocusRangeRestriction
  @abstract
-	Indicates current restriction of the receiver's autofocus system to a particular range of focus scan, if it supports range restrictions.
+    Indicates current restriction of the receiver's autofocus system to a particular range of focus scan, if it supports range restrictions.
  
  @discussion
-	The value of this property is an AVCaptureAutoFocusRangeRestriction indicating how the autofocus system
-	should limit its focus scan.  The default value is AVCaptureAutoFocusRangeRestrictionNone.
-	-setAutoFocusRangeRestriction: throws an NSInvalidArgumentException if isAutoFocusRangeRestrictionSupported
-	returns NO.  -setAutoFocusRangeRestriction: throws an NSGenericException if called without first obtaining exclusive
-	access to the receiver using lockForConfiguration:.  This property only has an effect when the focusMode property is
-	set to AVCaptureFocusModeAutoFocus or AVCaptureFocusModeContinuousAutoFocus.  Note that setting autoFocusRangeRestriction 
-	alone does not initiate a focus operation.  After setting autoFocusRangeRestriction, call -setFocusMode: to apply the new restriction.
+    The value of this property is an AVCaptureAutoFocusRangeRestriction indicating how the autofocus system should limit its focus scan. The default value is AVCaptureAutoFocusRangeRestrictionNone. -setAutoFocusRangeRestriction: throws an NSInvalidArgumentException if isAutoFocusRangeRestrictionSupported returns NO. -setAutoFocusRangeRestriction: throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:. This property only has an effect when the focusMode property is set to AVCaptureFocusModeAutoFocus or AVCaptureFocusModeContinuousAutoFocus. Note that setting autoFocusRangeRestriction alone does not initiate a focus operation. After setting autoFocusRangeRestriction, call -setFocusMode: to apply the new restriction.
  */
 @property(nonatomic) AVCaptureAutoFocusRangeRestriction autoFocusRangeRestriction NS_AVAILABLE_IOS(7_0);
 
 /*!
  @property smoothAutoFocusSupported
  @abstract
-	Indicates whether the receiver supports smooth autofocus.
+    Indicates whether the receiver supports smooth autofocus.
  
  @discussion
-	The receiver's smoothAutoFocusEnabled property can only be set if this property returns YES.
+    The receiver's smoothAutoFocusEnabled property can only be set if this property returns YES.
  */
 @property(nonatomic, readonly, getter=isSmoothAutoFocusSupported) BOOL smoothAutoFocusSupported NS_AVAILABLE_IOS(7_0);
 
 /*!
  @property smoothAutoFocusEnabled
  @abstract
-	Indicates whether the receiver should use smooth autofocus.
+    Indicates whether the receiver should use smooth autofocus.
  
  @discussion
-	On a receiver where -isSmoothAutoFocusSupported returns YES and smoothAutoFocusEnabled is set to YES,
-	a smooth autofocus will be engaged when the focus mode is set to AVCaptureFocusModeAutoFocus or
-	AVCaptureFocusModeContinuousAutoFocus.  Enabling smooth autofocus is appropriate for movie recording.
-	Smooth autofocus is slower and less visually invasive. Disabling smooth autofocus is more appropriate
-	for video processing where a fast autofocus is necessary.  The default value is NO.
-	Setting this property throws an NSInvalidArgumentException if -isSmoothAutoFocusSupported returns NO.
-	The receiver must be locked for configuration using lockForConfiguration: before clients can set this method,
-	otherwise an NSGenericException is thrown. Note that setting smoothAutoFocusEnabled alone does not initiate a
-	focus operation.  After setting smoothAutoFocusEnabled, call -setFocusMode: to apply the new smooth autofocus mode.
+    On a receiver where -isSmoothAutoFocusSupported returns YES and smoothAutoFocusEnabled is set to YES, a smooth autofocus will be engaged when the focus mode is set to AVCaptureFocusModeAutoFocus or AVCaptureFocusModeContinuousAutoFocus. Enabling smooth autofocus is appropriate for movie recording. Smooth autofocus is slower and less visually invasive. Disabling smooth autofocus is more appropriate for video processing where a fast autofocus is necessary. The default value is NO. Setting this property throws an NSInvalidArgumentException if -isSmoothAutoFocusSupported returns NO. The receiver must be locked for configuration using lockForConfiguration: before clients can set this method, otherwise an NSGenericException is thrown. Note that setting smoothAutoFocusEnabled alone does not initiate a focus operation. After setting smoothAutoFocusEnabled, call -setFocusMode: to apply the new smooth autofocus mode.
  */
 @property(nonatomic, getter=isSmoothAutoFocusEnabled) BOOL smoothAutoFocusEnabled NS_AVAILABLE_IOS(7_0);
 
@@ -881,21 +733,14 @@
     Indicates the focus position of the lens.
  
  @discussion
-    The range of possible positions is 0.0 to 1.0, with 0.0 being the shortest distance at which the lens can focus and
-    1.0 the furthest. Note that 1.0 does not represent focus at infinity. The default value is 1.0.
-    Note that a given lens position value does not correspond to an exact physical distance, nor does it represent a
-    consistent focus distance from device to device. This property is key-value observable. It can be read at any time, 
-    regardless of focus mode, but can only be set via setFocusModeLockedWithLensPosition:completionHandler:.
-*/
+    The range of possible positions is 0.0 to 1.0, with 0.0 being the shortest distance at which the lens can focus and 1.0 the furthest. Note that 1.0 does not represent focus at infinity. The default value is 1.0. Note that a given lens position value does not correspond to an exact physical distance, nor does it represent a consistent focus distance from device to device. This property is key-value observable. It can be read at any time, regardless of focus mode, but can only be set via setFocusModeLockedWithLensPosition:completionHandler:.
+ */
 @property(nonatomic, readonly) float lensPosition NS_AVAILABLE_IOS(8_0);
 
 /*!
  @constant AVCaptureLensPositionCurrent
-    A special value that may be passed as the lensPosition parameter of setFocusModeLockedWithLensPosition:completionHandler: to
-    indicate that the caller does not wish to specify a value for the lensPosition property, and that it should instead be set 
-    to its current value. Note that the device may be adjusting lensPosition at the time of the call, in which case the value at 
-    which lensPosition is locked may differ from the value obtained by querying the lensPosition property.
-*/
+    A special value that may be passed as the lensPosition parameter of setFocusModeLockedWithLensPosition:completionHandler: to indicate that the caller does not wish to specify a value for the lensPosition property, and that it should instead be set to its current value. Note that the device may be adjusting lensPosition at the time of the call, in which case the value at which lensPosition is locked may differ from the value obtained by querying the lensPosition property.
+ */
 AVF_EXPORT const float AVCaptureLensPositionCurrent NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -904,21 +749,13 @@
     Sets focusMode to AVCaptureFocusModeLocked and locks lensPosition at an explicit value.
  
  @param lensPosition
-    The lens position, as described in the documentation for the lensPosition property. A value of AVCaptureLensPositionCurrent can be used
-    to indicate that the caller does not wish to specify a value for lensPosition.
+    The lens position, as described in the documentation for the lensPosition property. A value of AVCaptureLensPositionCurrent can be used to indicate that the caller does not wish to specify a value for lensPosition.
  @param handler
-    A block to be called when lensPosition has been set to the value specified and focusMode is set to AVCaptureFocusModeLocked. If
-    setFocusModeLockedWithLensPosition:completionHandler: is called multiple times, the completion handlers will be called in FIFO order. 
-    The block receives a timestamp which matches that of the first buffer to which all settings have been applied. Note that the timestamp 
-    is synchronized to the device clock, and thus must be converted to the master clock prior to comparison with the timestamps of buffers 
-    delivered via an AVCaptureVideoDataOutput. The client may pass nil for the handler parameter if knowledge of the operation's completion 
-    is not required.
+    A block to be called when lensPosition has been set to the value specified and focusMode is set to AVCaptureFocusModeLocked. If setFocusModeLockedWithLensPosition:completionHandler: is called multiple times, the completion handlers will be called in FIFO order. The block receives a timestamp which matches that of the first buffer to which all settings have been applied. Note that the timestamp is synchronized to the device clock, and thus must be converted to the master clock prior to comparison with the timestamps of buffers delivered via an AVCaptureVideoDataOutput. The client may pass nil for the handler parameter if knowledge of the operation's completion is not required.
  
  @discussion
-    This is the only way of setting lensPosition.
-    This method throws an NSRangeException if lensPosition is set to an unsupported level.
-    This method throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:.
-*/
+    This is the only way of setting lensPosition. This method throws an NSRangeException if lensPosition is set to an unsupported level. This method throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:.
+ */
 - (void)setFocusModeLockedWithLensPosition:(float)lensPosition completionHandler:(void (^)(CMTime syncTime))handler NS_AVAILABLE_IOS(8_0);
 
 @end
@@ -931,13 +768,12 @@
  @constant AVCaptureExposureModeLocked
     Indicates that the exposure should be locked at its current value.
  @constant AVCaptureExposureModeAutoExpose
-    Indicates that the device should automatically adjust exposure once and then change the exposure mode to 
-    AVCaptureExposureModeLocked.
+    Indicates that the device should automatically adjust exposure once and then change the exposure mode to AVCaptureExposureModeLocked.
  @constant AVCaptureExposureModeContinuousAutoExposure
     Indicates that the device should automatically adjust exposure when needed.
  @constant AVCaptureExposureModeCustom
     Indicates that the device should only adjust exposure according to user provided ISO, exposureDuration values.
-*/
+ */
 typedef NS_ENUM(NSInteger, AVCaptureExposureMode) {
 	AVCaptureExposureModeLocked                            = 0,
 	AVCaptureExposureModeAutoExpose                        = 1,
@@ -959,7 +795,7 @@
 
  @discussion
     The receiver's exposureMode property can only be set to a certain mode if this method returns YES for that mode.
-*/
+ */
 - (BOOL)isExposureModeSupported:(AVCaptureExposureMode)exposureMode;
 
 /*!
@@ -968,17 +804,8 @@
     Indicates current exposure mode of the receiver, if it has adjustable exposure.
 
  @discussion
-    The value of this property is an AVCaptureExposureMode that determines the receiver's exposure mode, if it has
-    adjustable exposure.  -setExposureMode: throws an NSInvalidArgumentException if set to an unsupported value 
-    (see -isExposureModeSupported:).  -setExposureMode: throws an NSGenericException if called without first obtaining 
-    exclusive access to the receiver using lockForConfiguration:. When using AVCaptureStillImageOutput with
-    automaticallyEnablesStillImageStabilizationWhenAvailable set to YES (the default behavior), the receiver's ISO and 
-    exposureDuration values may be overridden by automatic still image stabilization values if the scene is dark enough 
-    to warrant still image stabilization. To ensure that the receiver's ISO and exposureDuration values are honored while
-    in AVCaptureExposureModeCustom or AVCaptureExposureModeLocked, you must set AVCaptureStillImageOutput's
-    automaticallyEnablesStillImageStabilizationWhenAvailable property to NO. Clients can observe automatic changes to 
-    the receiver's exposureMode by key value observing this property.
-*/
+    The value of this property is an AVCaptureExposureMode that determines the receiver's exposure mode, if it has adjustable exposure. -setExposureMode: throws an NSInvalidArgumentException if set to an unsupported value (see -isExposureModeSupported:). -setExposureMode: throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:. When using AVCaptureStillImageOutput with automaticallyEnablesStillImageStabilizationWhenAvailable set to YES (the default behavior), the receiver's ISO and exposureDuration values may be overridden by automatic still image stabilization values if the scene is dark enough to warrant still image stabilization. To ensure that the receiver's ISO and exposureDuration values are honored while in AVCaptureExposureModeCustom or AVCaptureExposureModeLocked, you must set AVCaptureStillImageOutput's automaticallyEnablesStillImageStabilizationWhenAvailable property to NO. Clients can observe automatic changes to the receiver's exposureMode by key value observing this property.
+ */
 @property(nonatomic) AVCaptureExposureMode exposureMode;
 
 /*!
@@ -988,7 +815,7 @@
  
  @discussion
     The receiver's exposurePointOfInterest property can only be set if this property returns YES.
-*/
+ */
 @property(nonatomic, readonly, getter=isExposurePointOfInterestSupported) BOOL exposurePointOfInterestSupported;
 
 /*!
@@ -997,14 +824,8 @@
     Indicates current exposure point of interest of the receiver, if it has one.
 
  @discussion
-    The value of this property is a CGPoint that determines the receiver's exposure point of interest, if it has
-    adjustable exposure. A value of (0,0) indicates that the camera should adjust exposure based on the top left
-    corner of the image, while a value of (1,1) indicates that it should adjust exposure based on the bottom right corner. The
-    default value is (0.5,0.5). -setExposurePointOfInterest: throws an NSInvalidArgumentException if isExposurePointOfInterestSupported 
-    returns NO.  -setExposurePointOfInterest: throws an NSGenericException if called without first obtaining exclusive access 
-    to the receiver using lockForConfiguration:.  Note that setting exposurePointOfInterest alone does not initiate an exposure
-    operation.  After setting exposurePointOfInterest, call -setExposureMode: to apply the new point of interest.
-*/
+    The value of this property is a CGPoint that determines the receiver's exposure point of interest, if it has adjustable exposure. A value of (0,0) indicates that the camera should adjust exposure based on the top left corner of the image, while a value of (1,1) indicates that it should adjust exposure based on the bottom right corner. The default value is (0.5,0.5). -setExposurePointOfInterest: throws an NSInvalidArgumentException if isExposurePointOfInterestSupported returns NO. -setExposurePointOfInterest: throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:. Note that setting exposurePointOfInterest alone does not initiate an exposure operation. After setting exposurePointOfInterest, call -setExposureMode: to apply the new point of interest.
+ */
 @property(nonatomic) CGPoint exposurePointOfInterest;
 
 /*!
@@ -1013,11 +834,8 @@
     Indicates whether the receiver is currently adjusting camera exposure.
 
  @discussion
-    The value of this property is a BOOL indicating whether the receiver's camera exposure is being automatically
-    adjusted because its exposure mode is AVCaptureExposureModeAutoExpose or AVCaptureExposureModeContinuousAutoExposure.
-    Clients can observe the value of this property to determine whether the camera exposure is stable or is being
-    automatically adjusted.
-*/
+    The value of this property is a BOOL indicating whether the receiver's camera exposure is being automatically adjusted because its exposure mode is AVCaptureExposureModeAutoExpose or AVCaptureExposureModeContinuousAutoExposure. Clients can observe the value of this property to determine whether the camera exposure is stable or is being automatically adjusted.
+ */
 @property(nonatomic, readonly, getter=isAdjustingExposure) BOOL adjustingExposure;
 
 /*!
@@ -1026,9 +844,8 @@
     The size of the lens diaphragm.
  
  @discussion
-    The value of this property is a float indicating the size (f number) of the lens diaphragm.
-    This property does not change.
-*/
+    The value of this property is a float indicating the size (f number) of the lens diaphragm. This property does not change.
+ */
 @property(nonatomic, readonly) float lensAperture NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -1037,10 +854,8 @@
     The length of time over which exposure takes place.
  
  @discussion
-    Only exposure duration values between activeFormat.minExposureDuration and activeFormat.maxExposureDuration are supported.
-    This property is key-value observable. It can be read at any time, regardless of exposure mode, but can only be set
-    via setExposureModeCustomWithDuration:ISO:completionHandler:.
-*/
+    Only exposure duration values between activeFormat.minExposureDuration and activeFormat.maxExposureDuration are supported. This property is key-value observable. It can be read at any time, regardless of exposure mode, but can only be set via setExposureModeCustomWithDuration:ISO:completionHandler:.
+ */
 @property(nonatomic, readonly) CMTime exposureDuration NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -1049,29 +864,20 @@
     The current exposure ISO value.
  
  @discussion
-    This property controls the sensor's sensitivity to light by means of a gain value applied to the signal. Only ISO values
-    between activeFormat.minISO and activeFormat.maxISO are supported. Higher values will result in noisier images.
-    This property is key-value observable. It can be read at any time, regardless of exposure mode, but can only be set
-    via setExposureModeCustomWithDuration:ISO:completionHandler:.
-*/
+    This property controls the sensor's sensitivity to light by means of a gain value applied to the signal. Only ISO values between activeFormat.minISO and activeFormat.maxISO are supported. Higher values will result in noisier images. This property is key-value observable. It can be read at any time, regardless of exposure mode, but can only be set via setExposureModeCustomWithDuration:ISO:completionHandler:.
+ */
 @property(nonatomic, readonly) float ISO NS_AVAILABLE_IOS(8_0);
 
 /*!
  @constant AVCaptureExposureDurationCurrent
-    A special value that may be passed as the duration parameter of setExposureModeCustomWithDuration:ISO:completionHandler: to
-    indicate that the caller does not wish to specify a value for the exposureDuration property, and that it should instead be set to its 
-    current value. Note that the device may be adjusting exposureDuration at the time of the call, in which case the value to which
-    exposureDuration is set may differ from the value obtained by querying the exposureDuration property.
-*/
+    A special value that may be passed as the duration parameter of setExposureModeCustomWithDuration:ISO:completionHandler: to indicate that the caller does not wish to specify a value for the exposureDuration property, and that it should instead be set to its current value. Note that the device may be adjusting exposureDuration at the time of the call, in which case the value to which exposureDuration is set may differ from the value obtained by querying the exposureDuration property.
+ */
 AVF_EXPORT const CMTime AVCaptureExposureDurationCurrent NS_AVAILABLE_IOS(8_0);
 
 /*!
  @constant AVCaptureISOCurrent
-    A special value that may be passed as the ISO parameter of setExposureModeCustomWithDuration:ISO:completionHandler: to indicate
-    that the caller does not wish to specify a value for the ISO property, and that it should instead be set to its current value. Note that the
-    device may be adjusting ISO at the time of the call, in which case the value to which ISO is set may differ from the value obtained by querying
-    the ISO property.
-*/
+    A special value that may be passed as the ISO parameter of setExposureModeCustomWithDuration:ISO:completionHandler: to indicate that the caller does not wish to specify a value for the ISO property, and that it should instead be set to its current value. Note that the device may be adjusting ISO at the time of the call, in which case the value to which ISO is set may differ from the value obtained by querying the ISO property.
+ */
 AVF_EXPORT const float AVCaptureISOCurrent NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -1080,30 +886,15 @@
     Sets exposureMode to AVCaptureExposureModeCustom and locks exposureDuration and ISO at explicit values.
  
  @param duration
-    The exposure duration, as described in the documentation for the exposureDuration property. A value of AVCaptureExposureDurationCurrent
-    can be used to indicate that the caller does not wish to specify a value for exposureDuration.
-    Note that changes to this property may result in changes to activeVideoMinFrameDuration and/or activeVideoMaxFrameDuration.
+    The exposure duration, as described in the documentation for the exposureDuration property. A value of AVCaptureExposureDurationCurrent can be used to indicate that the caller does not wish to specify a value for exposureDuration. Note that changes to this property may result in changes to activeVideoMinFrameDuration and/or activeVideoMaxFrameDuration.
  @param ISO
-    The exposure ISO value, as described in the documentation for the ISO property. A value of AVCaptureISOCurrent
-    can be used to indicate that the caller does not wish to specify a value for ISO.
+    The exposure ISO value, as described in the documentation for the ISO property. A value of AVCaptureISOCurrent can be used to indicate that the caller does not wish to specify a value for ISO.
  @param handler
-    A block to be called when both exposureDuration and ISO have been set to the values specified and exposureMode is set to
-    AVCaptureExposureModeCustom. If setExposureModeCustomWithDuration:ISO:completionHandler: is called multiple times, the completion handlers 
-    will be called in FIFO order. The block receives a timestamp which matches that of the first buffer to which all settings have been applied.
-    Note that the timestamp is synchronized to the device clock, and thus must be converted to the master clock prior to comparison with the
-    timestamps of buffers delivered via an AVCaptureVideoDataOutput. The client may pass nil for the handler parameter if knowledge of the 
-    operation's completion is not required.
- 
- @discussion
-    This is the only way of setting exposureDuration and ISO.
-    This method throws an NSRangeException if either exposureDuration or ISO is set to an unsupported level.
-    This method throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:.
-    When using AVCaptureStillImageOutput with automaticallyEnablesStillImageStabilizationWhenAvailable set to YES (the default behavior),
-    the receiver's ISO and exposureDuration values may be overridden by automatic still image stabilization values if the scene is dark
-    enough to warrant still image stabilization.  To ensure that the receiver's ISO and exposureDuration values are honored while
-    in AVCaptureExposureModeCustom or AVCaptureExposureModeLocked, you must set AVCaptureStillImageOutput's
-    automaticallyEnablesStillImageStabilizationWhenAvailable property to NO.
-*/
+    A block to be called when both exposureDuration and ISO have been set to the values specified and exposureMode is set to AVCaptureExposureModeCustom. If setExposureModeCustomWithDuration:ISO:completionHandler: is called multiple times, the completion handlers will be called in FIFO order. The block receives a timestamp which matches that of the first buffer to which all settings have been applied. Note that the timestamp is synchronized to the device clock, and thus must be converted to the master clock prior to comparison with the timestamps of buffers delivered via an AVCaptureVideoDataOutput. The client may pass nil for the handler parameter if knowledge of the operation's completion is not required.
+ 
+ @discussion
+    This is the only way of setting exposureDuration and ISO. This method throws an NSRangeException if either exposureDuration or ISO is set to an unsupported level. This method throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:. When using AVCaptureStillImageOutput with automaticallyEnablesStillImageStabilizationWhenAvailable set to YES (the default behavior), the receiver's ISO and exposureDuration values may be overridden by automatic still image stabilization values if the scene is dark enough to warrant still image stabilization. To ensure that the receiver's ISO and exposureDuration values are honored while in AVCaptureExposureModeCustom or AVCaptureExposureModeLocked, you must set AVCaptureStillImageOutput's automaticallyEnablesStillImageStabilizationWhenAvailable property to NO.
+ */
 - (void)setExposureModeCustomWithDuration:(CMTime)duration ISO:(float)ISO completionHandler:(void (^)(CMTime syncTime))handler NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -1112,9 +903,8 @@
     Indicates the metered exposure level's offset from the target exposure value, in EV units.
  
  @discussion
-    The value of this read-only property indicates the difference between the metered exposure level of the current scene and the target exposure value.
-    This property is key-value observable.
-*/
+    The value of this read-only property indicates the difference between the metered exposure level of the current scene and the target exposure value. This property is key-value observable.
+ */
 @property(nonatomic, readonly) float exposureTargetOffset NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -1123,11 +913,8 @@
     Bias applied to the target exposure value, in EV units.
  
  @discussion
-    When exposureMode is AVCaptureExposureModeContinuousAutoExposure or AVCaptureExposureModeLocked, the bias will affect
-    both metering (exposureTargetOffset), and the actual exposure level (exposureDuration and ISO). When the exposure mode
-    is AVCaptureExposureModeCustom, it will only affect metering.
-    This property is key-value observable. It can be read at any time, but can only be set via setExposureTargetBias:completionHandler:.
-*/
+    When exposureMode is AVCaptureExposureModeContinuousAutoExposure or AVCaptureExposureModeLocked, the bias will affect both metering (exposureTargetOffset), and the actual exposure level (exposureDuration and ISO). When the exposure mode is AVCaptureExposureModeCustom, it will only affect metering. This property is key-value observable. It can be read at any time, but can only be set via setExposureTargetBias:completionHandler:.
+ */
 @property(nonatomic, readonly) float exposureTargetBias NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -1137,7 +924,7 @@
  
  @discussion
     This read-only property indicates the minimum supported exposure bias.
-*/
+ */
 @property(nonatomic, readonly) float minExposureTargetBias NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -1147,15 +934,13 @@
  
  @discussion
     This read-only property indicates the maximum supported exposure bias.
-*/
+ */
 @property(nonatomic, readonly) float maxExposureTargetBias NS_AVAILABLE_IOS(8_0);
 
 /*!
  @constant AVCaptureExposureTargetBiasCurrent
-    A special value that may be passed as the bias parameter of setExposureTargetBias:completionHandler: to indicate that the
-    caller does not wish to specify a value for the exposureTargetBias property, and that it should instead be set to its current
-    value.
-*/
+    A special value that may be passed as the bias parameter of setExposureTargetBias:completionHandler: to indicate that the caller does not wish to specify a value for the exposureTargetBias property, and that it should instead be set to its current value.
+ */
 AVF_EXPORT const float AVCaptureExposureTargetBiasCurrent NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -1166,18 +951,11 @@
  @param bias
     The bias to be applied to the exposure target value, as described in the documentation for the exposureTargetBias property.
  @param handler
-    A block to be called when exposureTargetBias has been set to the value specified. If setExposureTargetBias:completionHandler:
-    is called multiple times, the completion handlers will be called in FIFO order. The block receives a timestamp which matches 
-    that of the first buffer to which the setting has been applied. Note that the timestamp is synchronized to the device clock, 
-    and thus must be converted to the master clock prior to comparison with the timestamps of buffers delivered via an 
-    AVCaptureVideoDataOutput. The client may pass nil for the handler parameter if knowledge of the operation's completion is not 
-    required.
+    A block to be called when exposureTargetBias has been set to the value specified. If setExposureTargetBias:completionHandler: is called multiple times, the completion handlers will be called in FIFO order. The block receives a timestamp which matches that of the first buffer to which the setting has been applied. Note that the timestamp is synchronized to the device clock, and thus must be converted to the master clock prior to comparison with the timestamps of buffers delivered via an AVCaptureVideoDataOutput. The client may pass nil for the handler parameter if knowledge of the operation's completion is not required.
  
  @discussion
-    This is the only way of setting exposureTargetBias.
-    This method throws an NSRangeException if exposureTargetBias is set to an unsupported level.
-    This method throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:.
-*/
+    This is the only way of setting exposureTargetBias. This method throws an NSRangeException if exposureTargetBias is set to an unsupported level. This method throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:.
+ */
 - (void)setExposureTargetBias:(float)bias completionHandler:(void (^)(CMTime syncTime))handler NS_AVAILABLE_IOS(8_0);
 
 @end
@@ -1190,11 +968,10 @@
  @constant AVCaptureWhiteBalanceModeLocked
     Indicates that the white balance should be locked at its current value.
  @constant AVCaptureWhiteBalanceModeAutoWhiteBalance
-    Indicates that the device should automatically adjust white balance once and then change the white balance mode to 
-    AVCaptureWhiteBalanceModeLocked.
+    Indicates that the device should automatically adjust white balance once and then change the white balance mode to AVCaptureWhiteBalanceModeLocked.
  @constant AVCaptureWhiteBalanceModeContinuousAutoWhiteBalance
     Indicates that the device should automatically adjust white balance when needed.
-*/
+ */
 typedef NS_ENUM(NSInteger, AVCaptureWhiteBalanceMode) {
 	AVCaptureWhiteBalanceModeLocked				        = 0,
 	AVCaptureWhiteBalanceModeAutoWhiteBalance	        = 1,
@@ -1202,9 +979,10 @@
 } NS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED;
 
 /*!
- @typedef	AVCaptureWhiteBalanceGains
- @abstract	Structure containing RGB white balance gain values.
-*/
+ @typedef AVCaptureWhiteBalanceGains
+ @abstract
+    Structure containing RGB white balance gain values.
+ */
 typedef struct {
     float redGain;
     float greenGain;
@@ -1212,18 +990,20 @@
 } AVCaptureWhiteBalanceGains NS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED;
 
 /*!
- @typedef	AVCaptureWhiteBalanceChromaticityValues
- @abstract	Structure containing CIE 1931 xy chromaticity values
-*/
+ @typedef AVCaptureWhiteBalanceChromaticityValues
+ @abstract
+    Structure containing CIE 1931 xy chromaticity values.
+ */
 typedef struct {
     float x;
     float y;
 } AVCaptureWhiteBalanceChromaticityValues NS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED;
 
 /*!
- @typedef	AVCaptureWhiteBalanceTemperatureAndTintValues
- @abstract	Structure containing a white balance color correlated temperature in kelvin, plus a tint value in the range of [-150 - +150].
-*/
+ @typedef AVCaptureWhiteBalanceTemperatureAndTintValues
+ @abstract
+    Structure containing a white balance color correlated temperature in kelvin, plus a tint value in the range of [-150 - +150].
+ */
 typedef struct {
 	float temperature;
 	float tint;
@@ -1243,7 +1023,7 @@
 
  @discussion
     The receiver's whiteBalanceMode property can only be set to a certain mode if this method returns YES for that mode.
-*/
+ */
 - (BOOL)isWhiteBalanceModeSupported:(AVCaptureWhiteBalanceMode)whiteBalanceMode;
 
 /*!
@@ -1252,12 +1032,8 @@
     Indicates current white balance mode of the receiver, if it has adjustable white balance.
 
  @discussion
-    The value of this property is an AVCaptureWhiteBalanceMode that determines the receiver's white balance mode, if it
-    has adjustable white balance. -setWhiteBalanceMode: throws an NSInvalidArgumentException if set to an unsupported value 
-    (see -isWhiteBalanceModeSupported:).  -setWhiteBalanceMode: throws an NSGenericException if called without first obtaining 
-    exclusive access to the receiver using lockForConfiguration:.  Clients can observe automatic changes to the receiver's 
-    whiteBalanceMode by key value observing this property.
-*/
+    The value of this property is an AVCaptureWhiteBalanceMode that determines the receiver's white balance mode, if it has adjustable white balance. -setWhiteBalanceMode: throws an NSInvalidArgumentException if set to an unsupported value (see -isWhiteBalanceModeSupported:). -setWhiteBalanceMode: throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:. Clients can observe automatic changes to the receiver's whiteBalanceMode by key value observing this property.
+ */
 @property(nonatomic) AVCaptureWhiteBalanceMode whiteBalanceMode;
 
 /*!
@@ -1266,11 +1042,8 @@
     Indicates whether the receiver is currently adjusting camera white balance.
 
  @discussion
-    The value of this property is a BOOL indicating whether the receiver's camera white balance is being
-    automatically adjusted because its white balance mode is AVCaptureWhiteBalanceModeAutoWhiteBalance or
-    AVCaptureWhiteBalanceModeContinuousAutoWhiteBalance. Clients can observe the value of this property to determine
-    whether the camera white balance is stable or is being automatically adjusted.
-*/
+    The value of this property is a BOOL indicating whether the receiver's camera white balance is being automatically adjusted because its white balance mode is AVCaptureWhiteBalanceModeAutoWhiteBalance or AVCaptureWhiteBalanceModeContinuousAutoWhiteBalance. Clients can observe the value of this property to determine whether the camera white balance is stable or is being automatically adjusted.
+ */
 @property(nonatomic, readonly, getter=isAdjustingWhiteBalance) BOOL adjustingWhiteBalance;
 
 /*!
@@ -1279,14 +1052,8 @@
     Indicates the current device-specific RGB white balance gain values in use.
  
  @discussion
-    This property specifies the current red, green, and blue gain values used for white balance.  The values
-    can be used to adjust color casts for a given scene.
- 
-    For each channel, only values between 1.0 and -maxWhiteBalanceGain are supported.
- 
-    This property is key-value observable. It can be read at any time, regardless of white balance mode, but can only be
-    set via setWhiteBalanceModeLockedWithDeviceWhiteBalanceGains:completionHandler:.
-*/
+    This property specifies the current red, green, and blue gain values used for white balance. The values can be used to adjust color casts for a given scene. For each channel, only values between 1.0 and -maxWhiteBalanceGain are supported. This property is key-value observable. It can be read at any time, regardless of white balance mode, but can only be set via setWhiteBalanceModeLockedWithDeviceWhiteBalanceGains:completionHandler:.
+ */
 @property(nonatomic, readonly) AVCaptureWhiteBalanceGains deviceWhiteBalanceGains NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -1295,17 +1062,8 @@
     Indicates the current device-specific Gray World RGB white balance gain values in use.
  
  @discussion
-    This property specifies the current red, green, and blue gain values derived from the current scene to deliver
-    a neutral (or "Gray World") white point for white balance.
- 
-    Gray World values assume a neutral subject (e.g. a gray card) has been placed in the middle of the subject area and
-    fills the center 50% of the frame.  Clients can read these values and apply them to the device using
-    setWhiteBalanceModeLockedWithDeviceWhiteBalanceGains:completionHandler:.
- 
-    For each channel, only values between 1.0 and -maxWhiteBalanceGain are supported.
- 
-    This property is key-value observable. It can be read at any time, regardless of white balance mode.
-*/
+    This property specifies the current red, green, and blue gain values derived from the current scene to deliver a neutral (or "Gray World") white point for white balance. Gray World values assume a neutral subject (e.g. a gray card) has been placed in the middle of the subject area and fills the center 50% of the frame. Clients can read these values and apply them to the device using setWhiteBalanceModeLockedWithDeviceWhiteBalanceGains:completionHandler:. For each channel, only values between 1.0 and -maxWhiteBalanceGain are supported. This property is key-value observable. It can be read at any time, regardless of white balance mode.
+ */
 @property(nonatomic, readonly) AVCaptureWhiteBalanceGains grayWorldDeviceWhiteBalanceGains NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -1315,15 +1073,13 @@
  
  @discussion
     This property does not change for the life of the receiver.
-*/
+ */
 @property(nonatomic, readonly) float maxWhiteBalanceGain NS_AVAILABLE_IOS(8_0);
 
 /*!
  @constant AVCaptureWhiteBalanceGainsCurrent
-    A special value that may be passed as a parameter of setWhiteBalanceModeLockedWithDeviceWhiteBalanceGains:completionHandler: to
-    indicate that the caller does not wish to specify a value for deviceWhiteBalanceGains, and that gains should instead be
-    locked at their value at the moment that white balance is locked.
-*/
+    A special value that may be passed as a parameter of setWhiteBalanceModeLockedWithDeviceWhiteBalanceGains:completionHandler: to indicate that the caller does not wish to specify a value for deviceWhiteBalanceGains, and that gains should instead be locked at their value at the moment that white balance is locked.
+ */
 AVF_EXPORT const AVCaptureWhiteBalanceGains AVCaptureWhiteBalanceGainsCurrent NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -1332,23 +1088,13 @@
     Sets white balance to locked mode with explicit deviceWhiteBalanceGains values.
  
  @param whiteBalanceGains
-    The white balance gain values, as described in the documentation for the deviceWhiteBalanceGains property. A value of
-    AVCaptureWhiteBalanceGainsCurrent can be used to indicate that the caller does not wish to specify a value for deviceWhiteBalanceGains.
+    The white balance gain values, as described in the documentation for the deviceWhiteBalanceGains property. A value of AVCaptureWhiteBalanceGainsCurrent can be used to indicate that the caller does not wish to specify a value for deviceWhiteBalanceGains.
  @param handler
-    A block to be called when white balance gains have been set to the values specified and whiteBalanceMode is set to
-    AVCaptureWhiteBalanceModeLocked. If setWhiteBalanceModeLockedWithDeviceWhiteBalanceGains:completionHandler: is called multiple times, 
-    the completion handlers will be called in FIFO order. The block receives a timestamp which matches that of the first buffer to which 
-    all settings have been applied. Note that the timestamp is synchronized to the device clock, and thus must be converted to the master 
-    clock prior to comparison  with the timestamps of buffers delivered via an AVCaptureVideoDataOutput. This parameter may be nil if 
-    synchronization is not required.
+    A block to be called when white balance gains have been set to the values specified and whiteBalanceMode is set to AVCaptureWhiteBalanceModeLocked. If setWhiteBalanceModeLockedWithDeviceWhiteBalanceGains:completionHandler: is called multiple times, the completion handlers will be called in FIFO order. The block receives a timestamp which matches that of the first buffer to which all settings have been applied. Note that the timestamp is synchronized to the device clock, and thus must be converted to the master clock prior to comparison  with the timestamps of buffers delivered via an AVCaptureVideoDataOutput. This parameter may be nil if synchronization is not required.
  
  @discussion
-    For each channel in the whiteBalanceGains struct, only values between 1.0 and -maxWhiteBalanceGain are supported.
-    Gain values are normalized to the minimum channel value to avoid brightness changes (e.g. R:2 G:2 B:4 will be
-	normalized to R:1 G:1 B:2).
-    This method throws an NSRangeException if any of the whiteBalanceGains are set to an unsupported level.
-    This method throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:.
-*/
+    For each channel in the whiteBalanceGains struct, only values between 1.0 and -maxWhiteBalanceGain are supported. Gain values are normalized to the minimum channel value to avoid brightness changes (e.g. R:2 G:2 B:4 will be normalized to R:1 G:1 B:2). This method throws an NSRangeException if any of the whiteBalanceGains are set to an unsupported level. This method throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:.
+ */
 - (void)setWhiteBalanceModeLockedWithDeviceWhiteBalanceGains:(AVCaptureWhiteBalanceGains)whiteBalanceGains completionHandler:(void (^)(CMTime syncTime))handler NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -1357,18 +1103,13 @@
     Converts device-specific white balance RGB gain values to device-independent chromaticity values.
  
  @param whiteBalanceGains
-    White balance gain values, as described in the documentation for the deviceWhiteBalanceGains property.
-    A value of AVCaptureWhiteBalanceGainsCurrent may not be used in this function.
+    White balance gain values, as described in the documentation for the deviceWhiteBalanceGains property. A value of AVCaptureWhiteBalanceGainsCurrent may not be used in this function.
  @return
     A fully populated AVCaptureWhiteBalanceChromaticityValues structure containing device-independent values.
  
  @discussion
-    This method may be called on the receiver to convert device-specific white balance RGB gain values to
-    device-independent chromaticity (little x, little y) values.
- 
-    For each channel in the whiteBalanceGains struct, only values between 1.0 and -maxWhiteBalanceGain are supported.
-    This method throws an NSRangeException if any of the whiteBalanceGains are set to unsupported values.
-*/
+    This method may be called on the receiver to convert device-specific white balance RGB gain values to device-independent chromaticity (little x, little y) values. For each channel in the whiteBalanceGains struct, only values between 1.0 and -maxWhiteBalanceGain are supported. This method throws an NSRangeException if any of the whiteBalanceGains are set to unsupported values.
+ */
 - (AVCaptureWhiteBalanceChromaticityValues)chromaticityValuesForDeviceWhiteBalanceGains:(AVCaptureWhiteBalanceGains)whiteBalanceGains NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -1383,14 +1124,8 @@
     A fully populated AVCaptureWhiteBalanceGains structure containing device-specific RGB gain values.
  
  @discussion
-    This method may be called on the receiver to convert device-independent chromaticity values to device-specific RGB white
-    balance gain values.
- 
-    This method throws an NSRangeException if any of the chromaticityValues are set outside the range [0,1].
-	Note that some x,y combinations yield out-of-range device RGB values that will cause an exception to be thrown
-    if passed directly to -setWhiteBalanceModeLockedWithDeviceWhiteBalanceGains:completionHandler:.  Be sure to check that 
-    red, green, and blue gain values are within the range of [1.0 - maxWhiteBalanceGain].
-*/
+    This method may be called on the receiver to convert device-independent chromaticity values to device-specific RGB white balance gain values. This method throws an NSRangeException if any of the chromaticityValues are set outside the range [0,1]. Note that some x,y combinations yield out-of-range device RGB values that will cause an exception to be thrown if passed directly to -setWhiteBalanceModeLockedWithDeviceWhiteBalanceGains:completionHandler:. Be sure to check that red, green, and blue gain values are within the range of [1.0 - maxWhiteBalanceGain].
+ */
 - (AVCaptureWhiteBalanceGains)deviceWhiteBalanceGainsForChromaticityValues:(AVCaptureWhiteBalanceChromaticityValues)chromaticityValues NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -1399,18 +1134,13 @@
     Converts device-specific white balance RGB gain values to device-independent temperature and tint values.
  
  @param whiteBalanceGains
-    White balance gain values, as described in the documentation for the deviceWhiteBalanceGains property.
-    A value of AVCaptureWhiteBalanceGainsCurrent may not be used in this function.
+    White balance gain values, as described in the documentation for the deviceWhiteBalanceGains property. A value of AVCaptureWhiteBalanceGainsCurrent may not be used in this function.
  @return
     A fully populated AVCaptureWhiteBalanceTemperatureAndTintValues structure containing device-independent values.
  
  @discussion
-    This method may be called on the receiver to convert device-specific white balance RGB gain values to
-    device-independent temperature (in kelvin) and tint values.
- 
-    For each channel in the whiteBalanceGains struct, only values between 1.0 and -maxWhiteBalanceGain are supported.
-    This method throws an NSRangeException if any of the whiteBalanceGains are set to unsupported values.
-*/
+    This method may be called on the receiver to convert device-specific white balance RGB gain values to device-independent temperature (in kelvin) and tint values. For each channel in the whiteBalanceGains struct, only values between 1.0 and -maxWhiteBalanceGain are supported. This method throws an NSRangeException if any of the whiteBalanceGains are set to unsupported values.
+ */
 - (AVCaptureWhiteBalanceTemperatureAndTintValues)temperatureAndTintValuesForDeviceWhiteBalanceGains:(AVCaptureWhiteBalanceGains)whiteBalanceGains NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -1425,14 +1155,8 @@
     A fully populated AVCaptureWhiteBalanceGains structure containing device-specific RGB gain values.
  
  @discussion
-    This method may be called on the receiver to convert device-independent temperature and tint values to device-specific RGB white
-    balance gain values.
- 
-    You may pass any temperature and tint values and corresponding white balance gains will be produced. Note though that
-    some temperature and tint combinations yield out-of-range device RGB values that will cause an exception to be thrown
-    if passed directly to -setWhiteBalanceModeLockedWithDeviceWhiteBalanceGains:completionHandler:.  Be sure to check that 
-    red, green, and blue gain values are within the range of [1.0 - maxWhiteBalanceGain].
-*/
+    This method may be called on the receiver to convert device-independent temperature and tint values to device-specific RGB white balance gain values. You may pass any temperature and tint values and corresponding white balance gains will be produced. Note though that some temperature and tint combinations yield out-of-range device RGB values that will cause an exception to be thrown if passed directly to -setWhiteBalanceModeLockedWithDeviceWhiteBalanceGains:completionHandler:. Be sure to check that red, green, and blue gain values are within the range of [1.0 - maxWhiteBalanceGain].
+ */
 - (AVCaptureWhiteBalanceGains)deviceWhiteBalanceGainsForTemperatureAndTintValues:(AVCaptureWhiteBalanceTemperatureAndTintValues)tempAndTintValues NS_AVAILABLE_IOS(8_0);
 
 @end
@@ -1442,18 +1166,11 @@
 /*!
  @property subjectAreaChangeMonitoringEnabled
  @abstract
-	Indicates whether the receiver should monitor the subject area for changes.
+    Indicates whether the receiver should monitor the subject area for changes.
  
  @discussion
-	The value of this property is a BOOL indicating whether the receiver should
-	monitor the video subject area for changes, such as lighting changes, substantial
-	movement, etc.  If subject area change monitoring is enabled, the receiver
-	sends an AVCaptureDeviceSubjectAreaDidChangeNotification whenever it detects
-	a change to the subject area, at which time an interested client may wish
-	to re-focus, adjust exposure, white balance, etc.  The receiver must be locked 
-	for configuration using lockForConfiguration: before clients can set
-	the value of this property.
-*/
+    The value of this property is a BOOL indicating whether the receiver should monitor the video subject area for changes, such as lighting changes, substantial movement, etc. If subject area change monitoring is enabled, the receiver sends an AVCaptureDeviceSubjectAreaDidChangeNotification whenever it detects a change to the subject area, at which time an interested client may wish to re-focus, adjust exposure, white balance, etc. The receiver must be locked for configuration using lockForConfiguration: before clients can set the value of this property.
+ */
 @property(nonatomic, getter=isSubjectAreaChangeMonitoringEnabled) BOOL subjectAreaChangeMonitoringEnabled NS_AVAILABLE_IOS(5_0);
 
 @end
@@ -1467,7 +1184,7 @@
  
  @discussion
     The receiver's automaticallyEnablesLowLightBoostWhenAvailable property can only be set if this property returns YES.
-*/
+ */
 @property(nonatomic, readonly, getter=isLowLightBoostSupported) BOOL lowLightBoostSupported NS_AVAILABLE_IOS(6_0);
 
 /*!
@@ -1476,11 +1193,8 @@
     Indicates whether the receiver's low light boost feature is enabled.
  
  @discussion
-    The value of this property is a BOOL indicating whether the receiver is currently enhancing
-    images to improve quality due to low light conditions. When -isLowLightBoostEnabled returns
-    YES, the receiver has switched into a special mode in which more light can be perceived in images.
-    This property is key-value observable.
-*/
+    The value of this property is a BOOL indicating whether the receiver is currently enhancing images to improve quality due to low light conditions. When -isLowLightBoostEnabled returns YES, the receiver has switched into a special mode in which more light can be perceived in images. This property is key-value observable.
+ */
 @property(nonatomic, readonly, getter=isLowLightBoostEnabled) BOOL lowLightBoostEnabled NS_AVAILABLE_IOS(6_0);
 
 /*!
@@ -1489,17 +1203,8 @@
     Indicates whether the receiver should automatically switch to low light boost mode when necessary.
  
  @discussion
-    On a receiver where -isLowLightBoostSupported returns YES, a special low light boost mode may be
-    engaged to improve image quality. When the automaticallyEnablesLowLightBoostWhenAvailable
-    property is set to YES, the receiver switches at its discretion to a special boost mode under
-    low light, and back to normal operation when the scene becomes sufficiently lit.  An AVCaptureDevice that
-    supports this feature may only engage boost mode for certain source formats or resolutions.
-    Clients may observe changes to the lowLightBoostEnabled property to know when the mode has engaged.
-    The switch between normal operation and low light boost mode may drop one or more video frames.
-    The default value is NO. Setting this property throws an NSInvalidArgumentException if -isLowLightBoostSupported
-    returns NO. The receiver must be locked for configuration using lockForConfiguration: before clients
-    can set this method, otherwise an NSGenericException is thrown.
-*/
+    On a receiver where -isLowLightBoostSupported returns YES, a special low light boost mode may be engaged to improve image quality. When the automaticallyEnablesLowLightBoostWhenAvailable property is set to YES, the receiver switches at its discretion to a special boost mode under low light, and back to normal operation when the scene becomes sufficiently lit. An AVCaptureDevice that supports this feature may only engage boost mode for certain source formats or resolutions. Clients may observe changes to the lowLightBoostEnabled property to know when the mode has engaged. The switch between normal operation and low light boost mode may drop one or more video frames. The default value is NO. Setting this property throws an NSInvalidArgumentException if -isLowLightBoostSupported returns NO. The receiver must be locked for configuration using lockForConfiguration: before clients can set this method, otherwise an NSGenericException is thrown.
+ */
 @property(nonatomic) BOOL automaticallyEnablesLowLightBoostWhenAvailable NS_AVAILABLE_IOS(6_0);
 
 @end
@@ -1509,18 +1214,12 @@
 /*!
  @property videoZoomFactor
  @abstract
- Controls zoom level of image outputs
+    Controls zoom level of image outputs
  
  @discussion
- Applies a centered crop for all image outputs, scaling as necessary to maintain output
- dimensions.  Minimum value of 1.0 yields full field of view, increasing values will increase
- magnification, up to a maximum value specified in the activeFormat's videoMaxZoomFactor property.
- Modifying the zoom factor will cancel any active rampToVideoZoomFactor:withRate:, and snap
- directly to the assigned value.  Assigning values outside the acceptable range will generate
- an NSRangeException.  Clients can key value observe the value of this property.
+    Applies a centered crop for all image outputs, scaling as necessary to maintain output dimensions. Minimum value of 1.0 yields full field of view, increasing values will increase magnification, up to a maximum value specified in the activeFormat's videoMaxZoomFactor property. Modifying the zoom factor will cancel any active rampToVideoZoomFactor:withRate:, and snap directly to the assigned value. Assigning values outside the acceptable range will generate an NSRangeException. Clients can key value observe the value of this property.
  
- -setVideoZoomFactor: throws an NSGenericException if called without first obtaining exclusive
- access to the receiver using lockForConfiguration:.
+    -setVideoZoomFactor: throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:.
  
  @seealso AVCaptureDeviceFormat AVCaptureDeviceFormat - videoMaxZoomFactor and videoZoomFactorUpscaleThreshold
  */
@@ -1529,50 +1228,38 @@
 /*!
  @method rampToVideoZoomFactor:withRate:
  @abstract
- Provides smooth changes in zoom factor.
+    Provides smooth changes in zoom factor.
  
  @discussion
- This method provides a change in zoom by compounding magnification at the specified
- rate over time.  Although the zoom factor will grow exponentially, this yields a
- visually linear zoom in the image over time.
- 
- The zoom transition will stop at the specified factor, which must be in the valid range for
- videoZoomFactor.  Assignments to videoZoomFactor while a ramp is in progress will cancel the
- ramp and snap to the assigned value.
- 
- The zoom factor is continuously scaled by pow(2,rate * time).  A rate of 0 causes no
- change in zoom factor, equivalent to calling cancelVideoZoomRamp.  A rate of 1 will
- cause the magnification to double every second (or halve every second if zooming out),
- and similarly larger or smaller values will zoom faster or slower respectively.  Only
- the absolute value of the rate is significant--sign is corrected for the direction
- of the target.  Changes in rate will be smoothed by an internal acceleration limit.
+    This method provides a change in zoom by compounding magnification at the specified rate over time. Although the zoom factor will grow exponentially, this yields a visually linear zoom in the image over time.
+ 
+    The zoom transition will stop at the specified factor, which must be in the valid range for videoZoomFactor. Assignments to videoZoomFactor while a ramp is in progress will cancel the ramp and snap to the assigned value.
+ 
+    The zoom factor is continuously scaled by pow(2,rate * time). A rate of 0 causes no change in zoom factor, equivalent to calling cancelVideoZoomRamp. A rate of 1 will cause the magnification to double every second (or halve every second if zooming out), and similarly larger or smaller values will zoom faster or slower respectively. Only the absolute value of the rate is significant--sign is corrected for the direction of the target. Changes in rate will be smoothed by an internal acceleration limit.
  
- -rampToVideoZoomFactor:withRate: throws an NSGenericException if called without first
- obtaining exclusive access to the receiver using lockForConfiguration:.
+    -rampToVideoZoomFactor:withRate: throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:.
  */
 - (void)rampToVideoZoomFactor:(CGFloat)factor withRate:(float)rate NS_AVAILABLE_IOS(7_0);
 
 /*!
  @property rampingVideoZoom
  @abstract
- Indicates if the zoom factor is transitioning to a value set by rampToVideoZoomFactor:withRate:
+    Indicates if the zoom factor is transitioning to a value set by rampToVideoZoomFactor:withRate:
  
  @discussion
- Clients can observe this value to determine when a ramp begins or completes.
+    Clients can observe this value to determine when a ramp begins or completes.
  */
 @property(nonatomic,readonly,getter=isRampingVideoZoom) BOOL rampingVideoZoom NS_AVAILABLE_IOS(7_0);
 
 /*!
  @method cancelVideoZoomRamp
  @abstract
- Eases out of any video zoom transitions initiated by rampToVideoZoomFactor:withRate:
+    Eases out of any video zoom transitions initiated by rampToVideoZoomFactor:withRate:
  
  @discussion
- This method is equivalent to calling rampToVideoZoomFactor:withRate: using the current zoom factor
- target and a rate of 0.  This allows a smooth stop to any changes in zoom which were in progress.
+    This method is equivalent to calling rampToVideoZoomFactor:withRate: using the current zoom factor target and a rate of 0. This allows a smooth stop to any changes in zoom which were in progress.
  
- -cancelVideoZoomRamp: throws an NSGenericException if called without first
- obtaining exclusive access to the receiver using lockForConfiguration:.
+    -cancelVideoZoomRamp: throws an NSGenericException if called without first obtaining exclusive access to the receiver using lockForConfiguration:.
  */
 - (void)cancelVideoZoomRamp NS_AVAILABLE_IOS(7_0);
 
@@ -1586,8 +1273,7 @@
  @constant AVAuthorizationStatusNotDetermined
     Indicates that the user has not yet made a choice regarding whether the client can access the hardware.
  @constant AVAuthorizationStatusRestricted
-    The client is not authorized to access the hardware for the media type. The user cannot change
-    the client's status, possibly due to active restrictions such as parental controls being in place.
+    The client is not authorized to access the hardware for the media type. The user cannot change the client's status, possibly due to active restrictions such as parental controls being in place.
  @constant AVAuthorizationStatusDenied
     The user explicitly denied access to the hardware supporting a media type for the client.
  @constant AVAuthorizationStatusAuthorized
@@ -1614,10 +1300,7 @@
     The authorization status of the client
  
  @discussion
-    This method returns the AVAuthorizationStatus of the client for accessing the underlying hardware supporting
-    the media type.  Media type constants are defined in AVMediaFormat.h.  If any media type other than AVMediaTypeVideo or
-    AVMediaTypeAudio is supplied, an NSInvalidArgumentException will be thrown.  If the status is AVAuthorizationStatusNotDetermined,
-    you may use the +requestAccessForMediaType:completionHandler: method to request access by prompting the user.
+    This method returns the AVAuthorizationStatus of the client for accessing the underlying hardware supporting the media type. Media type constants are defined in AVMediaFormat.h. If any media type other than AVMediaTypeVideo or AVMediaTypeAudio is supplied, an NSInvalidArgumentException will be thrown. If the status is AVAuthorizationStatusNotDetermined, you may use the +requestAccessForMediaType:completionHandler: method to request access by prompting the user.
  */
 + (AVAuthorizationStatus)authorizationStatusForMediaType:(NSString *)mediaType NS_AVAILABLE_IOS(7_0);
 
@@ -1632,20 +1315,15 @@
     A block called with the result of requesting access
  
  @discussion
-    Use this function to request access to the hardware for a given media type.   Media type constants are defined in AVMediaFormat.h.
-    If any media type other than AVMediaTypeVideo or AVMediaTypeAudio is supplied, an NSInvalidArgumentException will be thrown.
+    Use this function to request access to the hardware for a given media type. Media type constants are defined in AVMediaFormat.h. If any media type other than AVMediaTypeVideo or AVMediaTypeAudio is supplied, an NSInvalidArgumentException will be thrown.
  
-    This call will not block while the user is being asked for access, allowing the client to continue running.  Until access has been granted,
-    any AVCaptureDevices for the media type will vend silent audio samples or black video frames.  The user is only asked for permission
-    the first time the client requests access.  Later calls use the permission granted by the user.
+    This call will not block while the user is being asked for access, allowing the client to continue running. Until access has been granted, any AVCaptureDevices for the media type will vend silent audio samples or black video frames. The user is only asked for permission the first time the client requests access. Later calls use the permission granted by the user.
  
-    Note that the authorization dialog will automatically be shown if the status is AVAuthorizationStatusNotDetermined when
-    creating an AVCaptureDeviceInput.
+    Note that the authorization dialog will automatically be shown if the status is AVAuthorizationStatusNotDetermined when creating an AVCaptureDeviceInput.
  
     Invoking this method with AVMediaTypeAudio is equivalent to calling -[AVAudioSession requestRecordPermission:].
 
-    The completion handler is called on an arbitrary dispatch queue.  Is it the client's responsibility to ensure that
-    any UIKit-related updates are called on the main queue or main thread as a result.
+    The completion handler is called on an arbitrary dispatch queue. Is it the client's responsibility to ensure that any UIKit-related updates are called on the main queue or main thread as a result.
  */
 + (void)requestAccessForMediaType:(NSString *)mediaType completionHandler:(void (^)(BOOL granted))handler NS_AVAILABLE_IOS(7_0);
 
@@ -1664,7 +1342,7 @@
     Indicates that the tape transport is not threaded through the play head.
  @constant AVCaptureDeviceTransportControlsPlayingMode
     Indicates that the tape transport is threaded through the play head.
-*/
+ */
 typedef NS_ENUM(NSInteger, AVCaptureDeviceTransportControlsPlaybackMode) {
 	AVCaptureDeviceTransportControlsNotPlayingMode      = 0,
 	AVCaptureDeviceTransportControlsPlayingMode         = 1
@@ -1678,10 +1356,8 @@
     Returns whether the receiver supports transport control commands.
 
  @discussion
-    For devices with transport controls, such as AVC tape-based camcorders or pro capture devices with
-    RS422 deck control, the value of this property is YES.  If transport controls are not supported,
-    none of the associated transport control methods and properties are available on the receiver.
-*/
+    For devices with transport controls, such as AVC tape-based camcorders or pro capture devices with RS422 deck control, the value of this property is YES. If transport controls are not supported, none of the associated transport control methods and properties are available on the receiver.
+ */
 @property(nonatomic, readonly) BOOL transportControlsSupported NS_AVAILABLE(10_7, NA);
 
 /*!
@@ -1690,9 +1366,8 @@
     Returns the receiver's current playback mode.
 
  @discussion
-    For devices that support transport control, this property may be queried to discover the 
-    current playback mode.
-*/
+    For devices that support transport control, this property may be queried to discover the current playback mode.
+ */
 @property(nonatomic, readonly) AVCaptureDeviceTransportControlsPlaybackMode transportControlsPlaybackMode NS_AVAILABLE(10_7, NA);
 
 /*!
@@ -1701,32 +1376,28 @@
     Returns the receiver's current playback speed as a floating point value.
 
  @discussion
-    For devices that support transport control, this property may be queried to discover the 
-    current playback speed of the deck.
+    For devices that support transport control, this property may be queried to discover the  current playback speed of the deck.
     0.0 -> stopped.
     1.0 -> forward at normal speed.
     -1.0-> reverse at normal speed.
     2.0 -> forward at 2x normal speed.
     etc.
-*/
+ */
 @property(nonatomic, readonly) AVCaptureDeviceTransportControlsSpeed transportControlsSpeed NS_AVAILABLE(10_7, NA);
 
 /*!
  @method setTransportControlsPlaybackMode:speed:
  @abstract
-    sets both the transport controls playback mode and speed in a single method.
+    Sets both the transport controls playback mode and speed in a single method.
 
  @param mode
-    A AVCaptureDeviceTransportControlsPlaybackMode indicating whether the deck should be put into
-    play mode.
+    A AVCaptureDeviceTransportControlsPlaybackMode indicating whether the deck should be put into play mode.
 @param speed
     A AVCaptureDeviceTransportControlsSpeed indicating the speed at which to wind or play the tape.
 
  @discussion
-    A method for setting the receiver's transport controls playback mode and speed.  The receiver must 
-    be locked for configuration using lockForConfiguration: before clients can set this method, otherwise
-    an NSGenericException is thrown.
-*/
+    A method for setting the receiver's transport controls playback mode and speed. The receiver must be locked for configuration using lockForConfiguration: before clients can set this method, otherwise an NSGenericException is thrown.
+ */
 - (void)setTransportControlsPlaybackMode:(AVCaptureDeviceTransportControlsPlaybackMode)mode speed:(AVCaptureDeviceTransportControlsSpeed)speed NS_AVAILABLE(10_7, NA);
 
 @end
@@ -1742,15 +1413,8 @@
     Indicates whether the receiver is allowed to turn high dynamic range streaming on or off.
  
  @discussion
-    The value of this property is a BOOL indicating whether the receiver is free to turn
-    high dynamic range streaming on or off.  This property defaults to YES. By default, AVCaptureDevice
-    always turns off videoHDREnabled when a client uses the -setActiveFormat: API to set a new format.
-    When the client uses AVCaptureSession's setSessionPreset: API instead, AVCaptureDevice turns
-    videoHDR on automatically if it's a good fit for the preset.  -setAutomaticallyAdjustsVideoHDREnabled:
-    throws an NSGenericException if called without first obtaining exclusive access to the receiver using
-    -lockForConfiguration:.  Clients can key-value observe videoHDREnabled to know when the receiver has automatically
-    changed the value.
-*/
+    The value of this property is a BOOL indicating whether the receiver is free to turn high dynamic range streaming on or off. This property defaults to YES. By default, AVCaptureDevice always turns off videoHDREnabled when a client uses the -setActiveFormat: API to set a new format. When the client uses AVCaptureSession's setSessionPreset: API instead, AVCaptureDevice turns videoHDR on automatically if it's a good fit for the preset. -setAutomaticallyAdjustsVideoHDREnabled: throws an NSGenericException if called without first obtaining exclusive access to the receiver using -lockForConfiguration:. Clients can key-value observe videoHDREnabled to know when the receiver has automatically changed the value.
+ */
 @property(nonatomic) BOOL automaticallyAdjustsVideoHDREnabled NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -1759,38 +1423,54 @@
     Indicates whether the receiver's streaming high dynamic range feature is enabled.
  
  @discussion
-    The value of this property is a BOOL indicating whether the receiver is currently streaming
-    high dynamic range video buffers. The property may only be set if you first set 
-    automaticallyAdjustsVideoHDREnabled to NO, otherwise an NSGenericException is thrown.
-    videoHDREnabled may only be set to YES if the receiver's activeFormat.isVideoHDRSupported property
-    returns YES, otherwise an NSGenericException is thrown.  This property may be key-value observed.
- 
-    Note that setting this property may cause a lengthy reconfiguration of the receiver,
-    similar to setting a new active format or AVCaptureSession sessionPreset.  If you are setting either the
-    active format or the AVCaptureSession's sessionPreset AND this property, you should bracket these operations
-    with [session beginConfiguration] and [session commitConfiguration] to minimize reconfiguration time.
-*/
+    The value of this property is a BOOL indicating whether the receiver is currently streaming high dynamic range video buffers. The property may only be set if you first set automaticallyAdjustsVideoHDREnabled to NO, otherwise an NSGenericException is thrown. videoHDREnabled may only be set to YES if the receiver's activeFormat.isVideoHDRSupported property returns YES, otherwise an NSGenericException is thrown. This property may be key-value observed.
+ 
+    Note that setting this property may cause a lengthy reconfiguration of the receiver, similar to setting a new active format or AVCaptureSession sessionPreset. If you are setting either the active format or the AVCaptureSession's sessionPreset AND this property, you should bracket these operations with [session beginConfiguration] and [session commitConfiguration] to minimize reconfiguration time.
+ */
 @property(nonatomic, getter=isVideoHDREnabled) BOOL videoHDREnabled NS_AVAILABLE_IOS(8_0);
 
 @end
 
+/*!
+ @enum AVCaptureColorSpace
+ @abstract
+    Constants indicating active or supported video color space.
+ 
+ @constant AVCaptureColorSpace_sRGB
+    The sGRB color space ( https://www.w3.org/Graphics/Color/srgb )
+ @constant AVCaptureColorSpace_P3_D65
+    The P3 D65 wide color space which uses Illuminant D65 as the white point.
+ */
+typedef NS_ENUM(NSInteger, AVCaptureColorSpace) {
+	AVCaptureColorSpace_sRGB   NS_SWIFT_NAME(sRGB)   = 0,
+	AVCaptureColorSpace_P3_D65 NS_SWIFT_NAME(P3_D65) = 1,
+} NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED;
+
+@interface AVCaptureDevice (AVCaptureDeviceColorSpaceSupport)
+
+/*!
+ @property activeColorSpace
+ @abstract
+    Indicates the receiver's current active color space.
+ 
+ @discussion
+    By default, an AVCaptureDevice attached to an AVCaptureSession is automatically configured for wide color by the AVCaptureSession (see AVCaptureSession automaticallyConfiguresCaptureDeviceForWideColor). You may also set the activeColorSpace manually. To prevent the AVCaptureSession from undoing your work, remember to set AVCaptureSession's automaticallyConfiguresCaptureDeviceForWideColor property to NO. Changing the receiver's activeColorSpace while the session is running requires a disruptive reconfiguration of the capture render pipeline. Movie captures in progress will be ended immediately; unfulfilled photo requests will be aborted; video preview will temporarily freeze. -setActiveColorSpace: throws an NSGenericException if called without first obtaining exclusive access to the receiver using -lockForConfiguration:.
+ */
+@property(nonatomic) AVCaptureColorSpace activeColorSpace NS_AVAILABLE_IOS(10_0);
+
+@end
+
 
 @class AVFrameRateRangeInternal;
 
 /*!
  @class AVFrameRateRange
  @abstract
-    An AVFrameRateRange expresses a range of valid frame rates as min and max
-    rate and min and max duration.
+    An AVFrameRateRange expresses a range of valid frame rates as min and max rate and min and max duration.
 
  @discussion
-    An AVCaptureDevice exposes an array of formats, and its current activeFormat may be queried.  The
-    payload for the formats property is an array of AVCaptureDeviceFormat objects and the activeFormat property
-    payload is an AVCaptureDeviceFormat.  AVCaptureDeviceFormat wraps a CMFormatDescription and
-    expresses a range of valid video frame rates as an NSArray of AVFrameRateRange objects.
-    AVFrameRateRange expresses min and max frame rate as a rate in frames per second and
-    duration (CMTime).  An AVFrameRateRange object is immutable.  Its values do not change for the life of the object.
-*/
+    An AVCaptureDevice exposes an array of formats, and its current activeFormat may be queried. The payload for the formats property is an array of AVCaptureDeviceFormat objects and the activeFormat property payload is an AVCaptureDeviceFormat. AVCaptureDeviceFormat wraps a CMFormatDescription and expresses a range of valid video frame rates as an NSArray of AVFrameRateRange objects. AVFrameRateRange expresses min and max frame rate as a rate in frames per second and duration (CMTime). An AVFrameRateRange object is immutable. Its values do not change for the life of the object.
+ */
 NS_CLASS_AVAILABLE(10_7, 7_0) __TVOS_PROHIBITED
 @interface AVFrameRateRange : NSObject
 {
@@ -1804,9 +1484,8 @@
     A Float64 indicating the minimum frame rate supported by this range.
 
  @discussion
-    This read-only property indicates the minimum frame rate supported by
-    this range in frames per second.
-*/
+    This read-only property indicates the minimum frame rate supported by this range in frames per second.
+ */
 @property(readonly) Float64 minFrameRate;
 
 /*!
@@ -1815,9 +1494,8 @@
     A Float64 indicating the maximum frame rate supported by this range.
 
  @discussion
-    This read-only property indicates the maximum frame rate supported by
-    this range in frames per second.
-*/
+    This read-only property indicates the maximum frame rate supported by this range in frames per second.
+ */
 @property(readonly) Float64 maxFrameRate;
 
 /*!
@@ -1826,10 +1504,8 @@
     A CMTime indicating the maximum frame duration supported by this range.
 
  @discussion
-    This read-only property indicates the maximum frame duration supported by
-    this range.  It is the reciprocal of minFrameRate, and expresses minFrameRate
-    as a duration.
-*/
+    This read-only property indicates the maximum frame duration supported by this range. It is the reciprocal of minFrameRate, and expresses minFrameRate as a duration.
+ */
 @property(readonly) CMTime maxFrameDuration;
 
 /*!
@@ -1838,10 +1514,8 @@
     A CMTime indicating the minimum frame duration supported by this range.
 
  @discussion
-    This read-only property indicates the minimum frame duration supported by
-    this range.  It is the reciprocal of maxFrameRate, and expresses maxFrameRate
-    as a duration.
-*/
+    This read-only property indicates the minimum frame duration supported by this range. It is the reciprocal of maxFrameRate, and expresses maxFrameRate as a duration.
+ */
 @property(readonly) CMTime minFrameDuration;
 
 @end
@@ -1855,18 +1529,12 @@
  @constant AVCaptureVideoStabilizationModeOff
     Indicates that video should not be stabilized.
  @constant AVCaptureVideoStabilizationModeStandard
-    Indicates that video should be stabilized using the standard video stabilization algorithm introduced with iOS 5.0.
-    Standard video stabilization has a reduced field of view.  Enabling video stabilization may introduce additional
-    latency into the video capture pipeline.
+    Indicates that video should be stabilized using the standard video stabilization algorithm introduced with iOS 5.0. Standard video stabilization has a reduced field of view. Enabling video stabilization may introduce additional latency into the video capture pipeline.
  @constant AVCaptureVideoStabilizationModeCinematic
-    Indicates that video should be stabilized using the cinematic stabilization algorithm for more dramatic results.
-    Cinematic video stabilization has a reduced field of view compared to standard video stabilization.
-    Enabling cinematic video stabilization introduces much more latency into the video capture pipeline than
-    standard video stabilization and consumes significantly more system memory.  Use narrow or identical min and max
-    frame durations in conjunction with this mode.
+    Indicates that video should be stabilized using the cinematic stabilization algorithm for more dramatic results. Cinematic video stabilization has a reduced field of view compared to standard video stabilization. Enabling cinematic video stabilization introduces much more latency into the video capture pipeline than standard video stabilization and consumes significantly more system memory. Use narrow or identical min and max frame durations in conjunction with this mode.
  @constant AVCaptureVideoStabilizationModeAuto
     Indicates that the most appropriate video stabilization mode for the device and format should be chosen.
-*/
+ */
 typedef NS_ENUM(NSInteger, AVCaptureVideoStabilizationMode) {
     AVCaptureVideoStabilizationModeOff       = 0,
     AVCaptureVideoStabilizationModeStandard	 = 1,
@@ -1882,13 +1550,10 @@
  @constant AVCaptureAutoFocusSystemNone
     Indicates that autofocus is not available.
  @constant AVCaptureAutoFocusSystemContrastDetection
-    Indicates that autofocus is achieved by contrast detection. 
-    Contrast detection performs a focus scan to find the optimal position.
+    Indicates that autofocus is achieved by contrast detection. Contrast detection performs a focus scan to find the optimal position.
  @constant AVCaptureAutoFocusSystemPhaseDetection
-    Indicates that autofocus is achieved by phase detection. 
-    Phase detection has the ability to achieve focus in many cases without a focus scan.
-    Phase detection autofocus is typically less visually intrusive than contrast detection autofocus.
-*/
+    Indicates that autofocus is achieved by phase detection. Phase detection has the ability to achieve focus in many cases without a focus scan. Phase detection autofocus is typically less visually intrusive than contrast detection autofocus.
+ */
 typedef NS_ENUM(NSInteger, AVCaptureAutoFocusSystem) {
 	AVCaptureAutoFocusSystemNone              = 0,
 	AVCaptureAutoFocusSystemContrastDetection = 1,
@@ -1901,17 +1566,11 @@
 /*!
  @class AVCaptureDeviceFormat
  @abstract
-    An AVCaptureDeviceFormat wraps a CMFormatDescription and other format-related information, such
-    as min and max framerate.
+    An AVCaptureDeviceFormat wraps a CMFormatDescription and other format-related information, such as min and max framerate.
 
  @discussion
-    An AVCaptureDevice exposes an array of formats, and its current activeFormat may be queried.  The
-    payload for the formats property is an array of AVCaptureDeviceFormat objects and the activeFormat property
-    payload is an AVCaptureDeviceFormat.  AVCaptureDeviceFormat is a thin wrapper around a 
-    CMFormatDescription, and can carry associated device format information that doesn't go in a
-    CMFormatDescription, such as min and max frame rate.  An AVCaptureDeviceFormat object is immutable.
-    Its values do not change for the life of the object.
-*/
+    An AVCaptureDevice exposes an array of formats, and its current activeFormat may be queried. The payload for the formats property is an array of AVCaptureDeviceFormat objects and the activeFormat property payload is an AVCaptureDeviceFormat. AVCaptureDeviceFormat is a thin wrapper around a CMFormatDescription, and can carry associated device format information that doesn't go in a CMFormatDescription, such as min and max frame rate. An AVCaptureDeviceFormat object is immutable. Its values do not change for the life of the object.
+ */
 NS_CLASS_AVAILABLE(10_7, 7_0) __TVOS_PROHIBITED
 @interface AVCaptureDeviceFormat : NSObject
 {
@@ -1925,9 +1584,8 @@
     An NSString describing the media type of an AVCaptureDevice active or supported format.
 
  @discussion
-    Supported mediaTypes are listed in AVMediaFormat.h.  This is a read-only
-    property.  The caller assumes no ownership of the returned value and should not CFRelease it.
-*/
+    Supported mediaTypes are listed in AVMediaFormat.h. This is a read-only property. The caller assumes no ownership of the returned value and should not CFRelease it.
+ */
 @property(nonatomic, readonly) NSString *mediaType;
 
 /*!
@@ -1936,9 +1594,8 @@
     A CMFormatDescription describing an AVCaptureDevice active or supported format.
 
  @discussion
-    A CMFormatDescription describing an AVCaptureDevice active or supported format.  This is a read-only
-    property.  The caller assumes no ownership of the returned value and should not CFRelease it.
-*/
+    A CMFormatDescription describing an AVCaptureDevice active or supported format. This is a read-only property. The caller assumes no ownership of the returned value and should not CFRelease it.
+ */
 @property(nonatomic, readonly) CMFormatDescriptionRef formatDescription;
 
 /*!
@@ -1947,9 +1604,8 @@
     A property indicating the format's supported frame rate ranges.
 
  @discussion
-    videoSupportedFrameRateRanges is an array of AVFrameRateRange objects, one for
-    each of the format's supported video frame rate ranges.
-*/
+    videoSupportedFrameRateRanges is an array of AVFrameRateRange objects, one for each of the format's supported video frame rate ranges.
+ */
 @property(nonatomic, readonly) NSArray *videoSupportedFrameRateRanges;
 
 #if TARGET_OS_IPHONE
@@ -1960,9 +1616,8 @@
     A property indicating the format's field of view.
 
  @discussion
-    videoFieldOfView is a float value indicating the receiver's field of view in degrees.
-    If field of view is unknown, a value of 0 is returned.
-*/
+    videoFieldOfView is a float value indicating the receiver's field of view in degrees. If field of view is unknown, a value of 0 is returned.
+ */
 @property(nonatomic, readonly) float videoFieldOfView NS_AVAILABLE_IOS(7_0);
 
 /*!
@@ -1971,9 +1626,8 @@
     A property indicating whether the format is binned.
 
  @discussion
-    videoBinned is a BOOL indicating whether the format is a binned format.
-    Binning is a pixel-combining process which can result in greater low light sensitivity at the cost of reduced resolution.
-*/
+    videoBinned is a BOOL indicating whether the format is a binned format. Binning is a pixel-combining process which can result in greater low light sensitivity at the cost of reduced resolution.
+ */
 @property(nonatomic, readonly, getter=isVideoBinned) BOOL videoBinned NS_AVAILABLE_IOS(7_0);
 
 /*!
@@ -1985,9 +1639,8 @@
     An AVCaptureVideoStabilizationMode to be checked.
  
  @discussion
-    isVideoStabilizationModeSupported: returns a boolean value indicating whether the format can be stabilized using
-    the given mode with -[AVCaptureConnection setPreferredVideoStabilizationMode:].
-*/
+    isVideoStabilizationModeSupported: returns a boolean value indicating whether the format can be stabilized using the given mode with -[AVCaptureConnection setPreferredVideoStabilizationMode:].
+ */
 - (BOOL)isVideoStabilizationModeSupported:(AVCaptureVideoStabilizationMode)videoStabilizationMode NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -1996,10 +1649,8 @@
     A property indicating whether the format supports video stabilization.
 
  @discussion
-    videoStabilizationSupported is a BOOL indicating whether the format can be stabilized using 
-    AVCaptureConnection -setEnablesVideoStabilizationWhenAvailable.
-    This property is deprecated.  Use isVideoStabilizationModeSupported: instead.
-*/
+    videoStabilizationSupported is a BOOL indicating whether the format can be stabilized using AVCaptureConnection -setEnablesVideoStabilizationWhenAvailable. This property is deprecated. Use isVideoStabilizationModeSupported: instead.
+ */
 @property(nonatomic, readonly, getter=isVideoStabilizationSupported) BOOL videoStabilizationSupported NS_DEPRECATED_IOS(7_0, 8_0, "Use isVideoStabilizationModeSupported: instead.");
 
 /*!
@@ -2008,24 +1659,17 @@
     Indicates the maximum zoom factor available for the AVCaptureDevice's videoZoomFactor property.
  
  @discussion
-    If the device's videoZoomFactor property is assigned a larger value, an NSRangeException will
-    be thrown. A maximum zoom factor of 1 indicates no zoom is available.
+    If the device's videoZoomFactor property is assigned a larger value, an NSRangeException will be thrown. A maximum zoom factor of 1 indicates no zoom is available.
  */
 @property(nonatomic, readonly) CGFloat videoMaxZoomFactor NS_AVAILABLE_IOS(7_0);
 
 /*!
  @property videoZoomFactorUpscaleThreshold
  @abstract
-    Indicates the value of AVCaptureDevice's videoZoomFactor property at which the image output
-    begins to require upscaling.
+    Indicates the value of AVCaptureDevice's videoZoomFactor property at which the image output begins to require upscaling.
  
  @discussion
-    In some cases the image sensor's dimensions are larger than the dimensions reported by the video
-    AVCaptureDeviceFormat.  As long as the sensor crop is larger than the reported dimensions of the
-    AVCaptureDeviceFormat, the image will be downscaled.  Setting videoZoomFactor to the value of
-    videoZoomFactorUpscalingThreshold will provide a center crop of the sensor image data without
-    any scaling.  If a greater zoom factor is used, then the sensor data will be upscaled to the
-    device format's dimensions.
+    In some cases the image sensor's dimensions are larger than the dimensions reported by the video AVCaptureDeviceFormat. As long as the sensor crop is larger than the reported dimensions of the AVCaptureDeviceFormat, the image will be downscaled. Setting videoZoomFactor to the value of videoZoomFactorUpscalingThreshold will provide a center crop of the sensor image data without any scaling. If a greater zoom factor is used, then the sensor data will be upscaled to the device format's dimensions.
  */
 @property(nonatomic, readonly) CGFloat videoZoomFactorUpscaleThreshold NS_AVAILABLE_IOS(7_0);
 
@@ -2036,7 +1680,7 @@
  
  @discussion
     This read-only property indicates the minimum supported exposure duration.
-*/
+ */
 @property(nonatomic, readonly) CMTime minExposureDuration NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -2046,7 +1690,7 @@
  
  @discussion
     This read-only property indicates the maximum supported exposure duration.
-*/
+ */
 @property(nonatomic, readonly) CMTime maxExposureDuration NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -2056,7 +1700,7 @@
  
  @discussion
     This read-only property indicates the minimum supported exposure ISO value.
-*/
+ */
 @property(nonatomic, readonly) float minISO NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -2066,7 +1710,7 @@
  
  @discussion
     This read-only property indicates the maximum supported exposure ISO value.
-*/
+ */
 @property(nonatomic, readonly) float maxISO NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -2075,9 +1719,8 @@
     A property indicating whether the format supports high dynamic range streaming.
 
  @discussion
-    videoHDRSupported is a BOOL indicating whether the format supports
-    high dynamic range streaming.  See AVCaptureDevice's videoHDREnabled property.
-*/
+    videoHDRSupported is a BOOL indicating whether the format supports high dynamic range streaming. See AVCaptureDevice's videoHDREnabled property.
+ */
 @property(nonatomic, readonly, getter=isVideoHDRSupported) BOOL videoHDRSupported NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -2086,10 +1729,8 @@
     CMVideoDimensions indicating the highest resolution still image that can be produced by this format.
  
  @discussion
-    Normally, AVCaptureStillImageOutput emits images with the same dimensions as its source AVCaptureDevice's
-    activeFormat.  However, if you set highResolutionStillImageOutputEnabled to YES, AVCaptureStillImageOutput
-    emits still images with its source AVCaptureDevice's activeFormat.highResolutionStillImageDimensions.
-*/
+    Normally, AVCaptureStillImageOutput emits images with the same dimensions as its source AVCaptureDevice's activeFormat. However, if you set highResolutionStillImageOutputEnabled to YES, AVCaptureStillImageOutput emits still images with its source AVCaptureDevice's activeFormat.highResolutionStillImageDimensions.
+ */
 @property(nonatomic, readonly) CMVideoDimensions highResolutionStillImageDimensions NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -2099,9 +1740,19 @@
  
  @discussion
     This read-only property indicates the autofocus system.
-*/
+ */
 @property(nonatomic, readonly) AVCaptureAutoFocusSystem autoFocusSystem NS_AVAILABLE_IOS(8_0);
 
+/*!
+ @property supportedColorSpaces
+ @abstract
+    A property indicating the receiver's supported color spaces.
+ 
+ @discussion
+    This read-only property indicates the receiver's supported color spaces as an array of AVCaptureColorSpace constants sorted from narrow to wide color.
+ */
+@property(nonatomic, readonly) NSArray<NSNumber *> *supportedColorSpaces NS_AVAILABLE_IOS(10_0);
+
 #endif // TARGET_OS_IPHONE
 
 @end
@@ -2116,11 +1767,8 @@
     An AVCaptureDeviceInputSource represents a distinct input source on an AVCaptureDevice object.
 
  @discussion
-    An AVCaptureDevice may optionally present an array of inputSources, representing distinct mutually
-    exclusive inputs to the device, for example, an audio AVCaptureDevice might have ADAT optical
-    and analog input sources.  A video AVCaptureDevice might have an HDMI input source, or a component 
-    input source.
-*/
+    An AVCaptureDevice may optionally present an array of inputSources, representing distinct mutually exclusive inputs to the device, for example, an audio AVCaptureDevice might have ADAT optical and analog input sources. A video AVCaptureDevice might have an HDMI input source, or a component input source.
+ */
 NS_CLASS_AVAILABLE(10_7, NA) __TVOS_PROHIBITED
 @interface AVCaptureDeviceInputSource : NSObject
 {
@@ -2134,9 +1782,8 @@
     An ID unique among the inputSources exposed by a given AVCaptureDevice.
 
  @discussion
-    An AVCaptureDevice's inputSources array must contain AVCaptureInputSource objects with unique
-    inputSourceIDs.
-*/
+    An AVCaptureDevice's inputSources array must contain AVCaptureInputSource objects with unique inputSourceIDs.
+ */
 @property(nonatomic, readonly) NSString *inputSourceID;
 
 /*!
@@ -2146,7 +1793,7 @@
 
  @discussion
     This property can be used for displaying the name of the capture device input source in a user interface.
-*/
+ */
 @property(nonatomic, readonly) NSString *localizedName;
 
 @end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureFileOutput.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureFileOutput.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureFileOutput.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureFileOutput.h	2016-05-24 07:21:24.000000000 +0200
@@ -0,0 +1,584 @@
+/*
+    File:  AVCaptureOutputBase.h
+ 	
+ 	Framework:  AVFoundation
+ 
+	Copyright 2010-2016 Apple Inc. All rights reserved.
+*/
+
+#import <AVFoundation/AVCaptureOutput.h>
+
+#pragma mark - AVCaptureFileOutput
+
+@class AVCaptureFileOutputInternal;
+@protocol AVCaptureFileOutputRecordingDelegate;
+
+#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
+@protocol AVCaptureFileOutputDelegate;
+#endif
+
+/*!
+ @class AVCaptureFileOutput
+ @abstract
+    AVCaptureFileOutput is an abstract subclass of AVCaptureOutput that provides an interface for writing captured media to files.
+ 
+ @discussion
+    This abstract superclass defines the interface for outputs that record media samples to files. File outputs can start recording to a new file using the startRecordingToOutputFileURL:recordingDelegate: method. On successive invocations of this method on Mac OS X, the output file can by changed dynamically without losing media samples. A file output can stop recording using the stopRecording method. Because files are recorded in the background, applications will need to specify a delegate for each new file so that they can be notified when recorded files are finished.
+
+    On Mac OS X, clients can also set a delegate on the file output itself that can be used to control recording along exact media sample boundaries using the captureOutput:didOutputSampleBuffer:fromConnection: method.
+
+    The concrete subclasses of AVCaptureFileOutput are AVCaptureMovieFileOutput, which records media to a QuickTime movie file, and AVCaptureAudioFileOutput, which writes audio media to a variety of audio file formats.
+ */
+NS_CLASS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED
+@interface AVCaptureFileOutput : AVCaptureOutput 
+{
+@private
+	AVCaptureFileOutputInternal *_fileOutputInternal;
+}
+
+#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
+
+/*!
+ @property delegate
+ @abstract
+    The receiver's delegate.
+
+ @discussion
+    The value of this property is an object conforming to the AVCaptureFileOutputDelegate protocol that will be able to monitor and control recording along exact sample boundaries.
+ */
+@property(nonatomic, assign) id<AVCaptureFileOutputDelegate> delegate NS_AVAILABLE(10_7, NA);
+
+#endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
+
+/*!
+ @property outputFileURL
+ @abstract
+    The file URL of the file to which the receiver is currently recording incoming buffers.
+
+ @discussion
+    The value of this property is an NSURL object containing the file URL of the file currently being written by the receiver. Returns nil if the receiver is not recording to any file.
+ */
+@property(nonatomic, readonly) NSURL *outputFileURL;
+
+/*!
+ @method startRecordingToOutputFileURL:recordingDelegate:
+ @abstract
+    Tells the receiver to start recording to a new file, and specifies a delegate that will be notified when recording is finished.
+ 
+ @param outputFileURL
+    An NSURL object containing the URL of the output file. This method throws an NSInvalidArgumentException if the URL is not a valid file URL.
+ @param delegate
+    An object conforming to the AVCaptureFileOutputRecordingDelegate protocol. Clients must specify a delegate so that they can be notified when recording to the given URL is finished.
+
+ @discussion
+    The method sets the file URL to which the receiver is currently writing output media. If a file at the given URL already exists when capturing starts, recording to the new file will fail.
+
+    Clients need not call stopRecording before calling this method while another recording is in progress. On Mac OS X, if this method is invoked while an existing output file was already being recorded, no media samples will be discarded between the old file and the new file.
+
+    When recording is stopped either by calling stopRecording, by changing files using this method, or because of an error, the remaining data that needs to be included to the file will be written in the background. Therefore, clients must specify a delegate that will be notified when all data has been written to the file using the captureOutput:didFinishRecordingToOutputFileAtURL:fromConnections:error: method. The recording delegate can also optionally implement methods that inform it when data starts being written, when recording is paused and resumed, and when recording is about to be finished.
+
+    On Mac OS X, if this method is called within the captureOutput:didOutputSampleBuffer:fromConnection: delegate method, the first samples written to the new file are guaranteed to be those contained in the sample buffer passed to that method.
+
+    Note: AVCaptureAudioFileOutput does not support -startRecordingToOutputFileURL:recordingDelegate:. Use -startRecordingToOutputFileURL:outputFileType:recordingDelegate: instead.
+ */
+- (void)startRecordingToOutputFileURL:(NSURL*)outputFileURL recordingDelegate:(id<AVCaptureFileOutputRecordingDelegate>)delegate;
+
+/*!
+ @method stopRecording
+ @abstract
+    Tells the receiver to stop recording to the current file.
+
+ @discussion
+    Clients can call this method when they want to stop recording new samples to the current file, and do not want to continue recording to another file. Clients that want to switch from one file to another should not call this method. Instead they should simply call startRecordingToOutputFileURL:recordingDelegate: with the new file URL.
+
+    When recording is stopped either by calling this method, by changing files using startRecordingToOutputFileURL:recordingDelegate:, or because of an error, the remaining data that needs to be included to the file will be written in the background. Therefore, before using the file, clients must wait until the delegate that was specified in startRecordingToOutputFileURL:recordingDelegate: is notified when all data has been written to the file using the captureOutput:didFinishRecordingToOutputFileAtURL:fromConnections:error: method.
+
+    On Mac OS X, if this method is called within the captureOutput:didOutputSampleBuffer:fromConnection: delegate method, the last samples written to the current file are guaranteed to be those that were output immediately before those in the sample buffer passed to that method.
+ */
+- (void)stopRecording;
+
+/*!
+ @property recording
+ @abstract
+    Indicates whether the receiver is currently recording.
+
+ @discussion
+    The value of this property is YES when the receiver currently has a file to which it is writing new samples, NO otherwise.
+ */
+@property(nonatomic, readonly, getter=isRecording) BOOL recording;
+
+#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
+
+/*!
+ @property recordingPaused
+ @abstract
+    Indicates whether recording to the current output file is paused.
+
+ @discussion
+    This property indicates recording to the file returned by outputFileURL has been previously paused using the pauseRecording method. When a recording is paused, captured samples are not written to the output file, but new samples can be written to the same file in the future by calling resumeRecording.
+ */
+@property(nonatomic, readonly, getter=isRecordingPaused) BOOL recordingPaused NS_AVAILABLE(10_7, NA);
+
+/*!
+ @method pauseRecording
+ @abstract
+    Pauses recording to the current output file.
+
+ @discussion
+    This method causes the receiver to stop writing captured samples to the current output file returned by outputFileURL, but leaves the file open so that samples can be written to it in the future, when resumeRecording is called. This allows clients to record multiple media segments that are not contiguous in time to a single file.
+
+    On Mac OS X, if this method is called within the captureOutput:didOutputSampleBuffer:fromConnection: delegate method, the last samples written to the current file are guaranteed to be those that were output immediately before those in the sample buffer passed to that method.
+ */
+- (void)pauseRecording NS_AVAILABLE(10_7, NA);
+
+/*!
+ @method resumeRecording
+ @abstract
+    Resumes recording to the current output file after it was previously paused using pauseRecording.
+
+ @discussion
+    This method causes the receiver to resume writing captured samples to the current output file returned by outputFileURL, after recording was previously paused using pauseRecording. This allows clients to record multiple media segments that are not contiguous in time to a single file.
+
+    On Mac OS X, if this method is called within the captureOutput:didOutputSampleBuffer:fromConnection: delegate method, the first samples written to the current file are guaranteed to be those contained in the sample buffer passed to that method.
+ */
+- (void)resumeRecording NS_AVAILABLE(10_7, NA);
+
+#endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
+
+/*!
+ @property recordedDuration
+ @abstract
+    Indicates the duration of the media recorded to the current output file.
+
+ @discussion
+    If recording is in progress, this property returns the total time recorded so far.
+ */
+@property(nonatomic, readonly) CMTime recordedDuration;
+
+/*!
+ @property recordedFileSize
+ @abstract
+    Indicates the size, in bytes, of the data recorded to the current output file.
+
+ @discussion
+    If a recording is in progress, this property returns the size in bytes of the data recorded so far.
+ */
+@property(nonatomic, readonly) int64_t recordedFileSize;	
+
+/*!
+ @property maxRecordedDuration
+ @abstract
+    Specifies the maximum duration of the media that should be recorded by the receiver.
+
+ @discussion
+    This property specifies a hard limit on the duration of recorded files. Recording is stopped when the limit is reached and the captureOutput:didFinishRecordingToOutputFileAtURL:fromConnections:error: delegate method is invoked with an appropriate error. The default value of this property is kCMTimeInvalid, which indicates no limit.
+ */
+@property(nonatomic) CMTime maxRecordedDuration;
+
+/*!
+ @property maxRecordedFileSize
+ @abstract
+    Specifies the maximum size, in bytes, of the data that should be recorded by the receiver.
+ 
+ @discussion
+    This property specifies a hard limit on the data size of recorded files. Recording is stopped when the limit is reached and the captureOutput:didFinishRecordingToOutputFileAtURL:fromConnections:error: delegate method is invoked with an appropriate error. The default value of this property is 0, which indicates no limit.
+ */
+@property(nonatomic) int64_t maxRecordedFileSize;
+
+/*!
+ @property minFreeDiskSpaceLimit
+ @abstract
+    Specifies the minimum amount of free space, in bytes, required for recording to continue on a given volume.
+
+ @discussion
+    This property specifies a hard lower limit on the amount of free space that must remain on a target volume for recording to continue. Recording is stopped when the limit is reached and the captureOutput:didFinishRecordingToOutputFileAtURL:fromConnections:error: delegate method is invoked with an appropriate error.
+ */
+@property(nonatomic) int64_t minFreeDiskSpaceLimit;
+
+@end
+
+/*!
+ @protocol AVCaptureFileOutputRecordingDelegate
+ @abstract
+    Defines an interface for delegates of AVCaptureFileOutput to respond to events that occur in the process of recording a single file.
+ */
+__TVOS_PROHIBITED
+@protocol AVCaptureFileOutputRecordingDelegate <NSObject>
+
+@optional
+
+/*!
+ @method captureOutput:didStartRecordingToOutputFileAtURL:fromConnections:
+ @abstract
+    Informs the delegate when the output has started writing to a file.
+
+ @param captureOutput
+    The capture file output that started writing the file.
+ @param fileURL
+    The file URL of the file that is being written.
+ @param connections
+    An array of AVCaptureConnection objects attached to the file output that provided the data that is being written to the file.
+
+ @discussion
+    This method is called when the file output has started writing data to a file. If an error condition prevents any data from being written, this method may not be called. captureOutput:willFinishRecordingToOutputFileAtURL:fromConnections:error: and captureOutput:didFinishRecordingToOutputFileAtURL:fromConnections:error: will always be called, even if no data is written.
+
+    Clients should not assume that this method will be called on a specific thread, and should also try to make this method as efficient as possible.
+ */
+- (void)captureOutput:(AVCaptureFileOutput *)captureOutput didStartRecordingToOutputFileAtURL:(NSURL *)fileURL fromConnections:(NSArray *)connections;
+
+#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
+
+/*!
+ @method captureOutput:didPauseRecordingToOutputFileAtURL:fromConnections:
+ @abstract
+    Called whenever the output is recording to a file and successfully pauses the recording at the request of the client.
+
+ @param captureOutput
+    The capture file output that has paused its file recording.
+ @param fileURL
+    The file URL of the file that is being written.
+ @param connections
+    An array of AVCaptureConnection objects attached to the file output that provided the data that is being written to the file.
+
+ @discussion
+    Delegates can use this method to be informed when a request to pause recording is actually respected. It is safe for delegates to change what the file output is currently doing (starting a new file, for example) from within this method. If recording to a file is stopped, either manually or due to an error, this method is not guaranteed to be called, even if a previous call to pauseRecording was made.
+
+    Clients should not assume that this method will be called on a specific thread, and should also try to make this method as efficient as possible.
+ */
+- (void)captureOutput:(AVCaptureFileOutput *)captureOutput didPauseRecordingToOutputFileAtURL:(NSURL *)fileURL fromConnections:(NSArray *)connections NS_AVAILABLE(10_7, NA);
+
+/*!
+ @method captureOutput:didResumeRecordingToOutputFileAtURL:fromConnections:
+ @abstract
+    Called whenever the output, at the request of the client, successfully resumes a file recording that was paused.
+
+ @param captureOutput
+    The capture file output that has resumed its paused file recording.
+ @param fileURL
+    The file URL of the file that is being written.
+ @param connections
+    An array of AVCaptureConnection objects attached to the file output that provided the data that is being written to the file.
+
+ @discussion
+    Delegates can use this method to be informed when a request to resume recording is actually respected. It is safe for delegates to change what the file output is currently doing (starting a new file, for example) from within this method. If recording to a file is stopped, either manually or due to an error, this method is not guaranteed to be called, even if a previous call to resumeRecording was made.
+
+    Clients should not assume that this method will be called on a specific thread, and should also try to make this method as efficient as possible.
+ */
+- (void)captureOutput:(AVCaptureFileOutput *)captureOutput didResumeRecordingToOutputFileAtURL:(NSURL *)fileURL fromConnections:(NSArray *)connections NS_AVAILABLE(10_7, NA);
+
+/*!
+ @method captureOutput:willFinishRecordingToOutputFileAtURL:fromConnections:error:
+ @abstract
+    Informs the delegate when the output will stop writing new samples to a file.
+
+ @param captureOutput
+    The capture file output that will finish writing the file.
+ @param fileURL
+    The file URL of the file that is being written.
+ @param connections
+    An array of AVCaptureConnection objects attached to the file output that provided the data that is being written to the file.
+ @param error
+    An error describing what caused the file to stop recording, or nil if there was no error.
+
+ @discussion
+    This method is called when the file output will stop recording new samples to the file at outputFileURL, either because startRecordingToOutputFileURL:recordingDelegate: or stopRecording were called, or because an error, described by the error parameter, occurred (if no error occurred, the error parameter will be nil). This method will always be called for each recording request, even if no data is successfully written to the file.
+
+    Clients should not assume that this method will be called on a specific thread, and should also try to make this method as efficient as possible.
+ */
+- (void)captureOutput:(AVCaptureFileOutput *)captureOutput willFinishRecordingToOutputFileAtURL:(NSURL *)fileURL fromConnections:(NSArray *)connections error:(NSError *)error NS_AVAILABLE(10_7, NA);
+
+#endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
+
+@required
+
+/*!
+ @method captureOutput:didFinishRecordingToOutputFileAtURL:fromConnections:error:
+ @abstract
+    Informs the delegate when all pending data has been written to an output file.
+
+ @param captureOutput
+    The capture file output that has finished writing the file.
+ @param fileURL
+    The file URL of the file that has been written.
+ @param connections
+    An array of AVCaptureConnection objects attached to the file output that provided the data that was written to the file.
+ @param error
+    An error describing what caused the file to stop recording, or nil if there was no error.
+
+ @discussion
+    This method is called when the file output has finished writing all data to a file whose recording was stopped, either because startRecordingToOutputFileURL:recordingDelegate: or stopRecording were called, or because an error, described by the error parameter, occurred (if no error occurred, the error parameter will be nil). This method will always be called for each recording request, even if no data is successfully written to the file.
+
+    Clients should not assume that this method will be called on a specific thread.
+
+    Delegates are required to implement this method.
+ */
+- (void)captureOutput:(AVCaptureFileOutput *)captureOutput didFinishRecordingToOutputFileAtURL:(NSURL *)outputFileURL fromConnections:(NSArray *)connections error:(NSError *)error;
+
+@end
+
+#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
+
+/*!
+ @protocol AVCaptureFileOutputDelegate
+ @abstract
+    Defines an interface for delegates of AVCaptureFileOutput to monitor and control recordings along exact sample boundaries.
+ */
+@protocol AVCaptureFileOutputDelegate <NSObject>
+
+@required
+
+/*!
+ @method captureOutputShouldProvideSampleAccurateRecordingStart:
+ @abstract
+    Allows a client to opt in to frame accurate record-start in captureOutput:didOutputSampleBuffer:fromConnection:
+
+ @param captureOutput
+    The AVCaptureFileOutput instance with which the delegate is associated.
+
+ @discussion
+    In apps linked before Mac OS X 10.8, delegates that implement the captureOutput:didOutputSampleBuffer:fromConnection: method can ensure frame accurate start / stop of a recording by calling startRecordingToOutputFileURL:recordingDelegate: from within the callback. Frame accurate start requires the capture output to apply outputSettings when the session starts running, so it is ready to record on any given frame boundary. Compressing all the time while the session is running has power, thermal, and CPU implications. In apps linked on or after Mac OS X 10.8, delegates must implement captureOutputShouldProvideSampleAccurateRecordingStart: to indicate whether frame accurate start/stop recording is required (returning YES) or not (returning NO). The output calls this method as soon as the delegate is added, and never again. If your delegate returns NO, the capture output applies compression settings when startRecordingToOutputFileURL:recordingDelegate: is called, and disables compression settings after the recording is stopped.
+ */
+- (BOOL)captureOutputShouldProvideSampleAccurateRecordingStart:(AVCaptureOutput *)captureOutput NS_AVAILABLE(10_8, NA);
+
+@optional
+
+/*!
+ @method captureOutput:didOutputSampleBuffer:fromConnection:
+ @abstract
+    Gives the delegate the opportunity to inspect samples as they are received by the output and optionally start and stop recording at exact times.
+
+ @param captureOutput
+    The capture file output that is receiving the media data.
+ @param sampleBuffer
+    A CMSampleBuffer object containing the sample data and additional information about the sample, such as its format and presentation time.
+ @param connection
+    The AVCaptureConnection object attached to the file output from which the sample data was received.
+
+ @discussion
+    This method is called whenever the file output receives a single sample buffer (a single video frame or audio buffer, for example) from the given connection. This gives delegates an opportunity to start and stop recording or change output files at an exact sample boundary if -captureOutputShouldProvideSampleAccurateRecordingStart: returns YES. If called from within this method, the file output's startRecordingToOutputFileURL:recordingDelegate: and resumeRecording methods are guaranteed to include the received sample buffer in the new file, whereas calls to stopRecording and pauseRecording are guaranteed to include all samples leading up to those in the current sample buffer in the existing file.
+
+    Delegates can gather information particular to the samples by inspecting the CMSampleBuffer object. Sample buffers always contain a single frame of video if called from this method but may also contain multiple samples of audio. For B-frame video formats, samples are always delivered in presentation order.
+
+    Clients that need to reference the CMSampleBuffer object outside of the scope of this method must CFRetain it and then CFRelease it when they are finished with it.
+
+    Note that to maintain optimal performance, some sample buffers directly reference pools of memory that may need to be reused by the device system and other capture inputs. This is frequently the case for uncompressed device native capture where memory blocks are copied as little as possible. If multiple sample buffers reference such pools of memory for too long, inputs will no longer be able to copy new samples into memory and those samples will be dropped. If your application is causing samples to be dropped by retaining the provided CMSampleBuffer objects for too long, but it needs access to the sample data for a long period of time, consider copying the data into a new buffer and then calling CFRelease on the sample buffer if it was previously retained so that the memory it references can be reused.
+ 
+    Clients should not assume that this method will be called on a specific thread. In addition, this method is called periodically, so it must be efficient to prevent capture performance problems.
+ */
+- (void)captureOutput:(AVCaptureFileOutput *)captureOutput didOutputSampleBuffer:(CMSampleBufferRef)sampleBuffer fromConnection:(AVCaptureConnection *)connection NS_AVAILABLE(10_7, NA);
+
+@end
+
+#endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
+
+
+#pragma mark - AVCaptureMovieFileOutput
+
+@class AVCaptureMovieFileOutputInternal;
+
+/*!
+ @class AVCaptureMovieFileOutput
+ @abstract
+    AVCaptureMovieFileOutput is a concrete subclass of AVCaptureFileOutput that writes captured media to QuickTime movie files.
+
+ @discussion
+    AVCaptureMovieFileOutput implements the complete file recording interface declared by AVCaptureFileOutput for writing media data to QuickTime movie files. In addition, instances of AVCaptureMovieFileOutput allow clients to configure options specific to the QuickTime file format, including allowing them to write metadata collections to each file, specify media encoding options for each track (Mac OS X), and specify an interval at which movie fragments should be written.
+ */
+NS_CLASS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED
+@interface AVCaptureMovieFileOutput : AVCaptureFileOutput
+{
+@private
+	AVCaptureMovieFileOutputInternal *_internal;
+}
+
+/*!
+ @property movieFragmentInterval
+ @abstract
+    Specifies the frequency with which movie fragments should be written.
+
+ @discussion
+    When movie fragments are used, a partially written QuickTime movie file whose writing is unexpectedly interrupted can be successfully opened and played up to multiples of the specified time interval. A value of kCMTimeInvalid indicates that movie fragments should not be used, but that only a movie atom describing all of the media in the file should be written. The default value of this property is ten seconds.
+
+    Changing the value of this property will not affect the movie fragment interval of the file currently being written, if there is one.
+ */
+@property(nonatomic) CMTime movieFragmentInterval;
+
+/*!
+ @property metadata
+ @abstract
+    A collection of metadata to be written to the receiver's output files.
+
+ @discussion
+    The value of this property is an array of AVMetadataItem objects representing the collection of top-level metadata to be written in each output file.
+ */
+@property(nonatomic, copy) NSArray *metadata;
+
+#if TARGET_OS_IPHONE
+
+/*!
+ @property availableVideoCodecTypes
+ @abstract
+    Indicates the supported video codec formats that can be specified in setOutputSettingsForConnection:.
+
+ @discussion
+    The value of this property is an NSArray of NSStrings that can be used as values for the AVVideoCodecKey in the receiver's setOutputSettingsForConnection: dictionary. The array of available video codecs may change depending on the current session preset.
+ */
+@property(nonatomic, readonly) NSArray *availableVideoCodecTypes NS_AVAILABLE_IOS(10_0);
+
+#endif // TARGET_OS_IPHONE
+
+/*!
+ @method outputSettingsForConnection:
+ @abstract
+    Returns the options the receiver uses to re-encode media from the given connection as it is being recorded.
+
+ @param connection
+    The connection delivering the media to be re-encoded.
+ @result
+    An NSDictionary of output settings.
+
+ @discussion
+    See AVAudioSettings.h for audio connections or AVVideoSettings.h for video connections for more information on how to construct an output settings dictionary. If the returned value is an empty dictionary (i.e. [NSDictionary dictionary], the format of the media from the connection will not be changed before being written to the file. If -setOutputSettings:forConnection: was called with a nil dictionary, this method returns a non-nil dictionary reflecting the settings used by the AVCaptureSession's current sessionPreset.
+ */
+- (NSDictionary *)outputSettingsForConnection:(AVCaptureConnection *)connection NS_AVAILABLE(10_7, 10_0);
+
+/*!
+ @method setOutputSettings:forConnection:
+ @abstract
+    Sets the options the receiver uses to encode media from the given connection as it is being recorded.
+
+ @param outputSettings
+    An NSDictionary of output settings.
+ @param connection
+    The connection delivering the media to be encoded.
+
+ @discussion
+    See AVAudioSettings.h for audio connections or AVVideoSettings.h for video connections for more information on how to construct an output settings dictionary. A value of an empty dictionary (i.e. [NSDictionary dictionary], means that the format of the media from the connection should not be changed before being written to the file. A value of nil means that the output format will be determined by the session preset. In this case, -outputSettingsForConnection: will return a non-nil dictionary reflecting the settings used by the AVCaptureSession's current sessionPreset.
+ 
+    On iOS, you may only specify the AVVideoCodecKey in the outputSettings. If you specify any other key, an NSInvalidArgumentException will be thrown. See the availableVideoCodecTypes property.
+ */
+- (void)setOutputSettings:(NSDictionary *)outputSettings forConnection:(AVCaptureConnection *)connection NS_AVAILABLE(10_7, 10_0);
+
+#if TARGET_OS_IPHONE
+
+/*!
+ @method recordsVideoOrientationAndMirroringChangesAsMetadataTrackForConnection:
+ @abstract
+    Returns YES if the movie file output will create a timed metadata track that records samples which reflect changes made to the given connection's videoOrientation and videoMirrored properties during recording.
+
+ @param connection
+    A connection delivering video media to the movie file output. This method throws an NSInvalidArgumentException if the connection does not have a mediaType of AVMediaTypeVideo or if the connection does not terminate at the movie file output.
+
+ @discussion
+    See setRecordsVideoOrientationAndMirroringChanges:asMetadataTrackForConnection: for details on the behavior controlled by this value. The default value returned is NO.
+ */
+- (BOOL)recordsVideoOrientationAndMirroringChangesAsMetadataTrackForConnection:(AVCaptureConnection *)connection NS_AVAILABLE_IOS(9_0);
+
+/*!
+ @method setRecordsVideoOrientationAndMirroringChanges:asMetadataTrackForConnection:
+ @abstract
+    Controls whether or not the movie file output will create a timed metadata track that records samples which reflect changes made to the given connection's videoOrientation and videoMirrored properties during recording.
+ 
+ @param doRecordChanges
+    If YES, the movie file output will create a timed metadata track that records samples which reflect changes made to the given connection's videoOrientation and videoMirrored properties during recording.
+
+ @param connection
+    A connection delivering video media to the movie file output. This method throws an NSInvalidArgumentException if the connection does not have a mediaType of AVMediaTypeVideo or if the connection does not terminate at the movie file output.
+
+ @discussion
+    When a recording is started the current state of a video capture connection's videoOrientation and videoMirrored properties are used to build the display matrix for the created video track. The movie file format allows only one display matrix per track, which means that any changes made during a recording to the videoOrientation and videoMirrored properties are not captured. For example, a user starts a recording with their device in the portrait orientation, and then partway through the recording changes the device to a landscape orientation. The landscape orientation requires a different display matrix, but only the initial display matrix (the portrait display matrix) is recorded for the video track.
+
+    By invoking this method the client application directs the movie file output to create an additional track in the captured movie. This track is a timed metadata track that is associated with the video track, and contains one or more samples that contain a Video Orientation value (as defined by EXIF and TIFF specifications, which is enumerated by CGImagePropertyOrientation in <ImageIO/CGImageProperties.h>). The value represents the display matrix corresponding to the AVCaptureConnection's videoOrientation and videoMirrored properties when applied to the input source. The initial sample written to the timed metadata track represents video track's display matrix. During recording additional samples will be written to the timed metadata track whenever the client application changes the video connection's videoOrienation or videoMirrored properties. Using the above example, when the client application detects the user changing the device from portrait to landscape orientation, it updates the video connection's videoOrientation property, thus causing the movie file output to add a new sample to the timed metadata track.
+	
+    After capture, playback and editing applications can use the timed metadata track to enhance their user's experience. For example, when playing back the captured movie, a playback engine can use the samples to adjust the display of the video samples to keep the video properly oriented. Another example is an editing application that uses the sample the sample times to suggest cut points for breaking the captured movie into separate clips, where each clip is properly oriented.
+	
+    The default behavior is to not create the timed metadata track.
+	
+    The doRecordChanges value is only observed at the start of recording. Changes to the value will not have any effect until the next recording is started.
+ */
+- (void)setRecordsVideoOrientationAndMirroringChanges:(BOOL)doRecordChanges asMetadataTrackForConnection:(AVCaptureConnection *)connection NS_AVAILABLE_IOS(9_0);
+
+#endif // TARGET_OS_IPHONE
+
+@end
+
+
+#pragma mark - AVCaptureAudioFileOutput
+
+#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
+
+@class AVCaptureAudioFileOutputInternal;
+
+/*!
+ @class AVCaptureAudioFileOutput
+ @abstract
+    AVCaptureAudioFileOutput is a concrete subclass of AVCaptureFileOutput that writes captured audio to any audio file type supported by CoreAudio.
+ 
+ @discussion
+    AVCaptureAudioFileOutput implements the complete file recording interface declared by AVCaptureFileOutput for writing media data to audio files. In addition, instances of AVCaptureAudioFileOutput allow clients to configure options specific to the audio file formats, including allowing them to write metadata collections to each file and specify audio encoding options.
+ */
+NS_CLASS_AVAILABLE(10_7, NA) __TVOS_PROHIBITED
+@interface AVCaptureAudioFileOutput : AVCaptureFileOutput
+{
+@private
+	AVCaptureAudioFileOutputInternal *_internal;
+}
+
+/*!
+ @method availableOutputFileTypes
+ @abstract		
+    Provides the file types AVCaptureAudioFileOutput can write.
+ 
+ @result
+    An NSArray of UTIs identifying the file types the AVCaptureAudioFileOutput class can write.
+ */
++ (NSArray *)availableOutputFileTypes;
+
+/*!
+ @method startRecordingToOutputFileURL:outputFileType:recordingDelegate:
+ @abstract
+    Tells the receiver to start recording to a new file of the specified format, and specifies a delegate that will be notified when recording is finished.
+
+ @param outputFileURL
+    An NSURL object containing the URL of the output file. This method throws an NSInvalidArgumentException if the URL is not a valid file URL.
+ @param fileType
+    A UTI indicating the format of the file to be written.
+ @param delegate
+    An object conforming to the AVCaptureFileOutputRecordingDelegate protocol. Clients must specify a delegate so that they can be notified when recording to the given URL is finished.
+
+ @discussion
+    The method sets the file URL to which the receiver is currently writing output media. If a file at the given URL already exists when capturing starts, recording to the new file will fail.
+
+    The fileType argument is a UTI corresponding to the audio file format that should be written. UTIs for common audio file types are declared in AVMediaFormat.h.
+
+    Clients need not call stopRecording before calling this method while another recording is in progress. If this method is invoked while an existing output file was already being recorded, no media samples will be discarded between the old file and the new file.
+
+    When recording is stopped either by calling stopRecording, by changing files using this method, or because of an error, the remaining data that needs to be included to the file will be written in the background. Therefore, clients must specify a delegate that will be notified when all data has been written to the file using the captureOutput:didFinishRecordingToOutputFileAtURL:fromConnections:error: method. The recording delegate can also optionally implement methods that inform it when data starts being written, when recording is paused and resumed, and when recording is about to be finished.
+
+    On Mac OS X, if this method is called within the captureOutput:didOutputSampleBuffer:fromConnection: delegate method, the first samples written to the new file are guaranteed to be those contained in the sample buffer passed to that method.
+ */
+- (void)startRecordingToOutputFileURL:(NSURL*)outputFileURL outputFileType:(NSString *)fileType recordingDelegate:(id<AVCaptureFileOutputRecordingDelegate>)delegate;
+
+/*!
+ @property metadata
+ @abstract
+    A collection of metadata to be written to the receiver's output files.
+
+ @discussion
+    The value of this property is an array of AVMetadataItem objects representing the collection of top-level metadata to be written in each output file. Only ID3 v2.2, v2.3, or v2.4 style metadata items are supported.
+ */
+@property(nonatomic, copy) NSArray *metadata; 
+
+/*!
+ @property audioSettings
+ @abstract
+    Specifies the options the receiver uses to re-encode audio as it is being recorded.
+
+ @discussion
+    The output settings dictionary can contain values for keys from AVAudioSettings.h. A value of nil indicates that the format of the audio should not be changed before being written to the file.
+ */
+@property(nonatomic, copy) NSDictionary *audioSettings;
+
+@end
+
+#endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureInput.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureInput.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureInput.h	2015-09-30 23:18:01.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureInput.h	2016-05-25 04:40:24.000000000 +0200
@@ -21,17 +21,11 @@
 /*!
  @class AVCaptureInput
  @abstract
-    AVCaptureInput is an abstract class that provides an interface for connecting capture input sources to an
-    AVCaptureSession.
+    AVCaptureInput is an abstract class that provides an interface for connecting capture input sources to an AVCaptureSession.
 
  @discussion
-    Concrete instances of AVCaptureInput representing input sources such as cameras can be added to instances of
-    AVCaptureSession using the -[AVCaptureSession addInput:] method. An AVCaptureInput vends one or more streams of
-    media data. For example, input devices can provide both audio and video data. Each media stream provided by an input
-    is represented by an AVCaptureInputPort object. Within a capture session, connections are made between
-    AVCaptureInput instances and AVCaptureOutput instances via AVCaptureConnection objects that define the mapping
-    between a set of AVCaptureInputPort objects and a single AVCaptureOutput.
-*/
+    Concrete instances of AVCaptureInput representing input sources such as cameras can be added to instances of AVCaptureSession using the -[AVCaptureSession addInput:] method. An AVCaptureInput vends one or more streams of media data. For example, input devices can provide both audio and video data. Each media stream provided by an input is represented by an AVCaptureInputPort object. Within a capture session, connections are made between AVCaptureInput instances and AVCaptureOutput instances via AVCaptureConnection objects that define the mapping between a set of AVCaptureInputPort objects and a single AVCaptureOutput.
+ */
 NS_CLASS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED
 @interface AVCaptureInput : NSObject 
 {
@@ -45,9 +39,8 @@
     The ports owned by the receiver.
 
  @discussion
-    The value of this property is an array of AVCaptureInputPort objects, each exposing an interface to a single stream
-    of media data provided by an input.
-*/
+    The value of this property is an array of AVCaptureInputPort objects, each exposing an interface to a single stream of media data provided by an input.
+ */
 @property(nonatomic, readonly) NSArray *ports;
 
 @end
@@ -60,7 +53,7 @@
 
  @discussion
     The notification object is the AVCaptureInputPort instance whose format description changed.
-*/
+ */
 AVF_EXPORT NSString *const AVCaptureInputPortFormatDescriptionDidChangeNotification NS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED;
 
 @class AVCaptureInputPortInternal;
@@ -68,15 +61,11 @@
 /*!
  @class AVCaptureInputPort
  @abstract
-    An AVCaptureInputPort describes a single stream of media data provided by an AVCaptureInput and provides an
-    interface for connecting that stream to AVCaptureOutput instances via AVCaptureConnection.
+    An AVCaptureInputPort describes a single stream of media data provided by an AVCaptureInput and provides an interface for connecting that stream to AVCaptureOutput instances via AVCaptureConnection.
 
  @discussion
-    Instances of AVCaptureInputPort cannot be created directly. An AVCaptureInput exposes its input ports via its ports
-    property. Input ports provide information about the format of their media data via the mediaType and
-    formatDescription properties, and allow clients to control the flow of data via the enabled property. Input ports
-    are used by an AVCaptureConnection to define the mapping between inputs and outputs in an AVCaptureSession.
-*/
+    Instances of AVCaptureInputPort cannot be created directly. An AVCaptureInput exposes its input ports via its ports property. Input ports provide information about the format of their media data via the mediaType and formatDescription properties, and allow clients to control the flow of data via the enabled property. Input ports are used by an AVCaptureConnection to define the mapping between inputs and outputs in an AVCaptureSession.
+ */
 NS_CLASS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED
 @interface AVCaptureInputPort : NSObject
 {
@@ -91,7 +80,7 @@
 
  @discussion
     The value of this property is an AVCaptureInput instance that owns the receiver.
-*/
+ */
 @property(nonatomic, readonly) AVCaptureInput *input;
 
 /*!
@@ -100,9 +89,8 @@
     The media type of the data provided by the receiver.
 
  @discussion
-    The value of this property is a constant describing the type of media, such as AVMediaTypeVideo or AVMediaTypeAudio,
-    provided by the receiver. Media type constants are defined in AVMediaFormat.h.
-*/
+    The value of this property is a constant describing the type of media, such as AVMediaTypeVideo or AVMediaTypeAudio, provided by the receiver. Media type constants are defined in AVMediaFormat.h.
+ */
 @property(nonatomic, readonly) NSString *mediaType;
 
 /*!
@@ -111,10 +99,8 @@
     The format of the data provided by the receiver.
 
  @discussion
-    The value of this property is a CMFormatDescription that describes the format of the media data currently provided
-    by the receiver. Clients can be notified of changes to the format by observing the
-    AVCaptureInputPortFormatDescriptionDidChangeNotification.
-*/
+    The value of this property is a CMFormatDescription that describes the format of the media data currently provided by the receiver. Clients can be notified of changes to the format by observing the AVCaptureInputPortFormatDescriptionDidChangeNotification.
+ */
 @property(nonatomic, readonly) CMFormatDescriptionRef formatDescription;
 
 /*!
@@ -123,19 +109,18 @@
     Whether the receiver should provide data.
 
  @discussion
-    The value of this property is a BOOL that determines whether the receiver should provide data to outputs when a
-    session is running. Clients can set this property to fine tune which media streams from a given input will be used
-    during capture. The default value is YES.
-*/
+    The value of this property is a BOOL that determines whether the receiver should provide data to outputs when a session is running. Clients can set this property to fine tune which media streams from a given input will be used during capture. The default value is YES.
+ */
 @property(nonatomic, getter=isEnabled) BOOL enabled;
 
 /*!
  @property clock
  @abstract
-	Provides access to the "native" clock used by the input port.
+    Provides access to the "native" clock used by the input port.
+ 
  @discussion
-	The clock is read-only.
- */
+    The clock is read-only.
+  */
 @property(nonatomic, readonly) __attribute__((NSObject)) CMClockRef clock NS_AVAILABLE(10_9, 7_0);
 
 @end
@@ -146,13 +131,11 @@
 /*!
  @class AVCaptureDeviceInput
  @abstract
-    AVCaptureDeviceInput is a concrete subclass of AVCaptureInput that provides an interface for capturing media from an
-    AVCaptureDevice.
+    AVCaptureDeviceInput is a concrete subclass of AVCaptureInput that provides an interface for capturing media from an AVCaptureDevice.
 
  @discussion
-    Instances of AVCaptureDeviceInput are input sources for AVCaptureSession that provide media data from devices
-    connected to the system, represented by instances of AVCaptureDevice.
-*/
+    Instances of AVCaptureDeviceInput are input sources for AVCaptureSession that provide media data from devices connected to the system, represented by instances of AVCaptureDevice.
+ */
 NS_CLASS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED
 @interface AVCaptureDeviceInput : AVCaptureInput 
 {
@@ -170,15 +153,11 @@
  @param outError
     On return, if the given device cannot be used for capture, points to an NSError describing the problem.
  @result
-    An AVCaptureDeviceInput instance that provides data from the given device, or nil, if the device could not be used
-    for capture.
+    An AVCaptureDeviceInput instance that provides data from the given device, or nil, if the device could not be used for capture.
 
  @discussion
-    This method returns an instance of AVCaptureDeviceInput that can be used to capture data from an AVCaptureDevice in
-    an AVCaptureSession. This method attempts to open the device for capture, taking exclusive control of it if
-    necessary. If the device cannot be opened because it is no longer available or because it is in use, for example,
-    this method returns nil, and the optional outError parameter points to an NSError describing the problem.
-*/
+    This method returns an instance of AVCaptureDeviceInput that can be used to capture data from an AVCaptureDevice in an AVCaptureSession. This method attempts to open the device for capture, taking exclusive control of it if necessary. If the device cannot be opened because it is no longer available or because it is in use, for example, this method returns nil, and the optional outError parameter points to an NSError describing the problem.
+ */
 + (instancetype)deviceInputWithDevice:(AVCaptureDevice *)device error:(NSError **)outError;
 
 /*!
@@ -191,15 +170,11 @@
  @param outError
     On return, if the given device cannot be used for capture, points to an NSError describing the problem.
  @result
-    An AVCaptureDeviceInput instance that provides data from the given device, or nil, if the device could not be used
-    for capture.
+    An AVCaptureDeviceInput instance that provides data from the given device, or nil, if the device could not be used for capture.
 
  @discussion
-    This method creates an instance of AVCaptureDeviceInput that can be used to capture data from an AVCaptureDevice in
-    an AVCaptureSession. This method attempts to open the device for capture, taking exclusive control of it if
-    necessary. If the device cannot be opened because it is no longer available or because it is in use, for example,
-    this method returns nil, and the optional outError parameter points to an NSError describing the problem.
-*/
+    This method creates an instance of AVCaptureDeviceInput that can be used to capture data from an AVCaptureDevice in an AVCaptureSession. This method attempts to open the device for capture, taking exclusive control of it if necessary. If the device cannot be opened because it is no longer available or because it is in use, for example, this method returns nil, and the optional outError parameter points to an NSError describing the problem.
+ */
 - (instancetype)initWithDevice:(AVCaptureDevice *)device error:(NSError **)outError;
 
 /*!
@@ -209,7 +184,7 @@
 
  @discussion
     The value of this property is the AVCaptureDevice instance that was used to create the receiver.
-*/
+ */
 @property(nonatomic, readonly) AVCaptureDevice *device;
 
 @end
@@ -222,13 +197,11 @@
 /*!
  @class AVCaptureScreenInput
  @abstract
-    AVCaptureScreenInput is a concrete subclass of AVCaptureInput that provides an interface for capturing media from
-    a screen or portion thereof.
+    AVCaptureScreenInput is a concrete subclass of AVCaptureInput that provides an interface for capturing media from a screen or portion thereof.
 
  @discussion
-    Instances of AVCaptureScreenInput are input sources for AVCaptureSession that provide media data from
-    one of the screens connected to the system, represented by CGDirectDisplayIDs.
-*/
+    Instances of AVCaptureScreenInput are input sources for AVCaptureSession that provide media data from one of the screens connected to the system, represented by CGDirectDisplayIDs.
+ */
 NS_CLASS_AVAILABLE(10_7, NA) __TVOS_PROHIBITED
 @interface AVCaptureScreenInput : AVCaptureInput 
 {
@@ -242,16 +215,13 @@
     Creates an AVCaptureScreenInput instance that provides media data from the given display.
  
  @param displayID
-    The id of the display from which to capture video.  CGDirectDisplayID is defined in <CoreGraphics/CGDirectDisplay.h>
+    The id of the display from which to capture video. CGDirectDisplayID is defined in <CoreGraphics/CGDirectDisplay.h>
  @result
-    An AVCaptureScreenInput instance that provides data from the given screen, or nil, if the screen could not be used
-    for capture.
+    An AVCaptureScreenInput instance that provides data from the given screen, or nil, if the screen could not be used for capture.
 
  @discussion
-    This method creates an instance of AVCaptureScreenInput that can be used to capture data from a display in
-    an AVCaptureSession. This method validates the displayID. If the display cannot be used because it is not available
-    on the system, for example, this method returns nil.
-*/
+    This method creates an instance of AVCaptureScreenInput that can be used to capture data from a display in an AVCaptureSession. This method validates the displayID. If the display cannot be used because it is not available on the system, for example, this method returns nil.
+ */
 - (instancetype)initWithDisplayID:(CGDirectDisplayID)displayID;
 
 /*!
@@ -260,10 +230,8 @@
     A property indicating the screen input's minimum frame duration.
 
  @discussion
-    An AVCaptureScreenInput's minFrameDuration is the reciprocal of its maximum frame rate.  This property
-    may be used to request a maximum frame rate at which the input produces video frames.  The requested
-    rate may not be achievable due to overall bandwidth, so actual frame rates may be lower.
-*/
+    An AVCaptureScreenInput's minFrameDuration is the reciprocal of its maximum frame rate. This property may be used to request a maximum frame rate at which the input produces video frames. The requested rate may not be achievable due to overall bandwidth, so actual frame rates may be lower.
+ */
 @property(nonatomic) CMTime minFrameDuration;
 
 /*!
@@ -272,11 +240,8 @@
     A property indicating the bounding rectangle of the screen area to be captured in pixels.
 
  @discussion
-    By default, AVCaptureScreenInput captures the entire area of the displayID with which it is associated.
-    To limit the capture rectangle to a subsection of the screen, set the cropRect property, which
-    defines a smaller section of the screen in the screen's coordinate system.  The origin (0,0) is
-    the bottom-left corner of the screen.
-*/
+    By default, AVCaptureScreenInput captures the entire area of the displayID with which it is associated. To limit the capture rectangle to a subsection of the screen, set the cropRect property, which defines a smaller section of the screen in the screen's coordinate system. The origin (0,0) is the bottom-left corner of the screen.
+ */
 @property(nonatomic) CGRect cropRect;
 
 /*!
@@ -285,10 +250,8 @@
     A property indicating the factor by which video buffers captured from the screen are to be scaled.
 
  @discussion
-    By default, AVCaptureScreenInput captures the video buffers from the display at a scale factor
-    of 1.0 (no scaling).  Set this property to scale the buffers by a given factor.  For instance,
-    a 320x240 capture area with a scaleFactor of 2.0f produces video buffers at 640x480.
-*/
+    By default, AVCaptureScreenInput captures the video buffers from the display at a scale factor of 1.0 (no scaling). Set this property to scale the buffers by a given factor. For instance, a 320x240 capture area with a scaleFactor of 2.0f produces video buffers at 640x480.
+ */
 @property(nonatomic) CGFloat scaleFactor;
 
 /*!
@@ -297,10 +260,8 @@
     A property indicating whether mouse clicks should be highlighted in the captured output.
 
  @discussion
-    By default, AVCaptureScreenInput does not highlight mouse clicks in its captured output.  If this
-    property is set to YES, mouse clicks are highlighted (a circle is drawn around the mouse for the
-    duration of the click) in the captured output.
-*/
+    By default, AVCaptureScreenInput does not highlight mouse clicks in its captured output. If this property is set to YES, mouse clicks are highlighted (a circle is drawn around the mouse for the duration of the click) in the captured output.
+ */
 @property(nonatomic) BOOL capturesMouseClicks;
 
 /*!
@@ -309,12 +270,8 @@
     A property indicating whether the cursor should be rendered to the captured output.
 
  @discussion
-    By default, AVCaptureScreenInput draws the cursor in its captured output.  If this property
-    is set to NO, the captured output contains only the windows on the screen.  Cursor is
-    omitted.  Note that cursor position and mouse button state at the time of capture is
-    preserved in CMSampleBuffers emitted from AVCaptureScreenInput.  See the inline documentation
-    for kCMIOSampleBufferAttachmentKey_MouseAndKeyboardModifiers in <CoreMediaIO/CMIOSampleBuffer.h>
-*/
+    By default, AVCaptureScreenInput draws the cursor in its captured output. If this property is set to NO, the captured output contains only the windows on the screen. Cursor is omitted. Note that cursor position and mouse button state at the time of capture is preserved in CMSampleBuffers emitted from AVCaptureScreenInput. See the inline documentation for kCMIOSampleBufferAttachmentKey_MouseAndKeyboardModifiers in <CoreMediaIO/CMIOSampleBuffer.h>
+ */
 @property(nonatomic) BOOL capturesCursor NS_AVAILABLE(10_8, NA);
 
 /*!
@@ -323,16 +280,10 @@
     A property indicating whether duplicate frames should be removed by the input.
 
  @discussion
-    If this property is set to YES, AVCaptureScreenInput performs frame differencing and when it
-	detects duplicate frames, it drops them.  If set to NO, the captured output receives all frames
-    from the input.  Prior to 10.9 this value defaulted to YES.  In 10.9 and later, it defaults to
-	NO, as modern platforms support frame differencing in hardware-based encoders.
+    If this property is set to YES, AVCaptureScreenInput performs frame differencing and when it detects duplicate frames, it drops them. If set to NO, the captured output receives all frames from the input. Prior to 10.9 this value defaulted to YES. In 10.9 and later, it defaults to NO, as modern platforms support frame differencing in hardware-based encoders.
 	
-	As of 10.10, this property has been deprecated and is ignored.  Clients wishing to re-create
-	this functionality can use an AVCaptureVideoDataOutput and compare frame contents in their
-	own code.  If they wish to write a movie file, they can then pass the unique frames to an
-	AVAssetWriterInput.
-*/
+    As of 10.10, this property has been deprecated and is ignored. Clients wishing to re-create this functionality can use an AVCaptureVideoDataOutput and compare frame contents in their own code. If they wish to write a movie file, they can then pass the unique frames to an AVAssetWriterInput.
+ */
 @property(nonatomic) BOOL removesDuplicateFrames NS_DEPRECATED(10_8, 10_10, NA, NA);
 
 @end
@@ -345,16 +296,11 @@
 /*!
  @class AVCaptureMetadataInput
  @abstract
-    AVCaptureMetadataInput is a concrete subclass of AVCaptureInput that provides a way for
-    clients to supply AVMetadataItems to an AVCaptureSession.
+    AVCaptureMetadataInput is a concrete subclass of AVCaptureInput that provides a way for clients to supply AVMetadataItems to an AVCaptureSession.
 
  @discussion
-    Instances of AVCaptureMetadataInput are input sources for AVCaptureSession that provide
-    AVMetadataItems to an AVCaptureSession.  AVCaptureMetadataInputs present one and only one
-    AVCaptureInputPort, which currently may only be connected to an AVCaptureMovieFileOutput.
-    The metadata supplied over the input port is provided by the client, and must conform to a
-    client-supplied CMFormatDescription.  The AVMetadataItems are supplied in an AVTimedMetadataGroup.
-*/
+    Instances of AVCaptureMetadataInput are input sources for AVCaptureSession that provide AVMetadataItems to an AVCaptureSession. AVCaptureMetadataInputs present one and only one AVCaptureInputPort, which currently may only be connected to an AVCaptureMovieFileOutput. The metadata supplied over the input port is provided by the client, and must conform to a client-supplied CMFormatDescription. The AVMetadataItems are supplied in an AVTimedMetadataGroup.
+ */
 NS_CLASS_AVAILABLE(NA, 9_0) __TVOS_PROHIBITED
 @interface AVCaptureMetadataInput : AVCaptureInput 
 {
@@ -365,44 +311,35 @@
 /*!
  @method metadataInputWithFormatDescription:clock:
  @abstract
-    Returns an AVCaptureMetadataInput instance that allows a client to provide
-    AVTimedMetadataGroups to an AVCaptureSession.
+    Returns an AVCaptureMetadataInput instance that allows a client to provide AVTimedMetadataGroups to an AVCaptureSession.
 
  @param desc
-    A CMFormatDescription that defines the metadata to be supplied by the client.
-    Throws an NSInvalidArgumentException if NULL is passed.
+    A CMFormatDescription that defines the metadata to be supplied by the client. Throws an NSInvalidArgumentException if NULL is passed.
  @param clock
-    A CMClock that provided the timebase for the supplied samples.
-    Throws an NSInvalidArgumentException if NULL is passed.
+    A CMClock that provided the timebase for the supplied samples. Throws an NSInvalidArgumentException if NULL is passed.
  @result
     An AVCaptureMetadataInput instance.
 
  @discussion
-    This method returns an instance of AVCaptureMetadataInput that can be used to capture
-    AVTimedMetadataGroups supplied by the client to an AVCaptureSession.
-*/
+    This method returns an instance of AVCaptureMetadataInput that can be used to capture AVTimedMetadataGroups supplied by the client to an AVCaptureSession.
+ */
 + (instancetype)metadataInputWithFormatDescription:(CMMetadataFormatDescriptionRef)desc clock:(CMClockRef)clock;
 
 /*!
  @method initWithFormatDescription:clock:
  @abstract
-    Creates an AVCaptureMetadataInput instance that allows a client to provide
-    AVTimedMetadataGroups to an AVCaptureSession.
+    Creates an AVCaptureMetadataInput instance that allows a client to provide AVTimedMetadataGroups to an AVCaptureSession.
 
  @param desc
-    A CMFormatDescription that defines the metadata to be supplied by the client.
-    Throws NSInvalidArgumentException if NULL is passed.
+    A CMFormatDescription that defines the metadata to be supplied by the client. Throws NSInvalidArgumentException if NULL is passed.
  @param clock
-    A CMClock that provided the timebase for the supplied samples.
-    Throws NSInvalidArgumentException if NULL is passed.
+    A CMClock that provided the timebase for the supplied samples. Throws NSInvalidArgumentException if NULL is passed.
  @result
-    An AVCaptureMetadataInput instance, or nil, if the device could not be used
-    for capture.
+    An AVCaptureMetadataInput instance, or nil, if the device could not be used for capture.
 
  @discussion
-    This method creates an instance of AVCaptureMetadataInput that can be used to capture
-    AVTimedMetadataGroups supplied by the client to an AVCaptureSession.
-*/
+    This method creates an instance of AVCaptureMetadataInput that can be used to capture AVTimedMetadataGroups supplied by the client to an AVCaptureSession.
+ */
 - (instancetype)initWithFormatDescription:(CMMetadataFormatDescriptionRef)desc clock:(CMClockRef)clock;
 
 /*!
@@ -411,16 +348,11 @@
     Provides metadata to the AVCaptureSession.
 
  @param metadata
-    An AVTimedMetadataGroup of metadata.  Will throw an exception if nil.
-    In order to denote a period of no metadata, an empty AVTimedMetadataGroup should
-    be passed.
+    An AVTimedMetadataGroup of metadata. Will throw an exception if nil. In order to denote a period of no metadata, an empty AVTimedMetadataGroup should be passed.
 
  @discussion
-    The provided AVTimedMetadataGroup will be provided to the AVCaptureSession.  The group's
-    presentation timestamp is expressed in the context of the clock supplied to the initializer.
-    It is not required that the AVTimedMetadataGroup have a duration;  an empty AVTimedMetadataGroup
-    can be supplied to denote a period of no metadata.
-*/
+    The provided AVTimedMetadataGroup will be provided to the AVCaptureSession. The group's presentation timestamp is expressed in the context of the clock supplied to the initializer. It is not required that the AVTimedMetadataGroup have a duration;  an empty AVTimedMetadataGroup can be supplied to denote a period of no metadata.
+ */
 - (BOOL)appendTimedMetadataGroup:(AVTimedMetadataGroup *)metadata error:(NSError **)outError;
 
 @end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureMetadataOutput.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureMetadataOutput.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureMetadataOutput.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureMetadataOutput.h	2016-05-24 07:21:24.000000000 +0200
@@ -0,0 +1,131 @@
+/*
+    File:  AVCaptureMetadataOutput.h
+ 	
+ 	Framework:  AVFoundation
+ 
+	Copyright 2010-2016 Apple Inc. All rights reserved.
+*/
+
+#import <AVFoundation/AVCaptureOutput.h>
+
+#pragma mark - AVCaptureMetadataOutput
+
+@class AVCaptureMetadataOutputInternal;
+@protocol AVCaptureMetadataOutputObjectsDelegate;
+
+/*!
+ @class AVCaptureMetadataOutput
+ @abstract
+    AVCaptureMetadataOutput is a concrete subclass of AVCaptureOutput that can be used to process metadata objects from an attached connection.
+
+ @discussion
+    Instances of AVCaptureMetadataOutput emit arrays of AVMetadataObject instances (see AVMetadataObject.h), such as detected faces. Applications can access the metadata objects with the captureOutput:didOutputMetadataObjects:fromConnection: delegate method.
+*/
+NS_CLASS_AVAILABLE(NA, 6_0) __TVOS_PROHIBITED
+@interface AVCaptureMetadataOutput : AVCaptureOutput 
+{
+@private
+	AVCaptureMetadataOutputInternal *_internal;
+}
+
+/*!
+ @method setMetadataObjectsDelegate:queue:
+ @abstract
+    Sets the receiver's delegate that will accept metadata objects and dispatch queue on which the delegate will be called.
+
+ @param objectsDelegate
+    An object conforming to the AVCaptureMetadataOutputObjectsDelegate protocol that will receive metadata objects after they are captured.
+ @param objectsCallbackQueue
+    A dispatch queue on which all delegate methods will be called.
+
+ @discussion
+    When new metadata objects are captured in the receiver's connection, they will be vended to the delegate using the captureOutput:didOutputMetadataObjects:fromConnection: delegate method. All delegate methods will be called on the specified dispatch queue.
+
+    Clients that need to minimize the chances of metadata being dropped should specify a queue on which a sufficiently small amount of processing is performed along with receiving metadata objects.
+
+    A serial dispatch queue must be used to guarantee that metadata objects will be delivered in order. The objectsCallbackQueue parameter may not be NULL, except when setting the objectsDelegate to nil.
+*/
+- (void)setMetadataObjectsDelegate:(id<AVCaptureMetadataOutputObjectsDelegate>)objectsDelegate queue:(dispatch_queue_t)objectsCallbackQueue;
+
+/*!
+ @property metadataObjectsDelegate
+ @abstract
+    The receiver's delegate.
+ 
+ @discussion
+    The value of this property is an object conforming to the AVCaptureMetadataOutputObjectsDelegate protocol that will receive metadata objects after they are captured. The delegate is set using the setMetadataObjectsDelegate:queue: method.
+*/
+@property(nonatomic, readonly) id<AVCaptureMetadataOutputObjectsDelegate> metadataObjectsDelegate;
+
+/*!
+ @property metadataObjectsCallbackQueue
+ @abstract
+    The dispatch queue on which all metadata object delegate methods will be called.
+
+ @discussion
+    The value of this property is a dispatch_queue_t. The queue is set using the setMetadataObjectsDelegate:queue: method.
+*/
+@property(nonatomic, readonly) dispatch_queue_t metadataObjectsCallbackQueue;
+
+/*!
+ @property availableMetadataObjectTypes
+ @abstract
+    Indicates the receiver's supported metadata object types.
+ 
+ @discussion
+    The value of this property is an NSArray of NSStrings corresponding to AVMetadataObjectType strings defined in AVMetadataObject.h -- one for each metadata object type supported by the receiver. Available metadata object types are dependent on the capabilities of the AVCaptureInputPort to which this receiver's AVCaptureConnection is connected. Clients may specify the types of objects they would like to process by calling setMetadataObjectTypes:. This property is key-value observable.
+*/
+@property(nonatomic, readonly) NSArray *availableMetadataObjectTypes;
+
+/*!
+ @property metadataObjectTypes
+ @abstract
+    Specifies the types of metadata objects that the receiver should present to the client.
+
+ @discussion
+    AVCaptureMetadataOutput may detect and emit multiple metadata object types. For apps linked before iOS 7.0, the receiver defaults to capturing face metadata objects if supported (see -availableMetadataObjectTypes). For apps linked on or after iOS 7.0, the receiver captures no metadata objects by default. -setMetadataObjectTypes: throws an NSInvalidArgumentException if any elements in the array are not present in the -availableMetadataObjectTypes array.
+*/
+@property(nonatomic, copy) NSArray *metadataObjectTypes;
+
+/*!
+ @property rectOfInterest
+ @abstract
+    Specifies a rectangle of interest for limiting the search area for visual metadata.
+ 
+ @discussion
+    The value of this property is a CGRect that determines the receiver's rectangle of interest for each frame of video. The rectangle's origin is top left and is relative to the coordinate space of the device providing the metadata. Specifying a rectOfInterest may improve detection performance for certain types of metadata. The default value of this property is the value CGRectMake(0, 0, 1, 1). Metadata objects whose bounds do not intersect with the rectOfInterest will not be returned.
+ */
+@property(nonatomic) CGRect rectOfInterest NS_AVAILABLE_IOS(7_0);
+
+@end
+
+/*!
+ @protocol AVCaptureMetadataOutputObjectsDelegate
+ @abstract
+    Defines an interface for delegates of AVCaptureMetadataOutput to receive emitted objects.
+*/
+__TVOS_PROHIBITED
+@protocol AVCaptureMetadataOutputObjectsDelegate <NSObject>
+
+@optional
+
+/*!
+ @method captureOutput:didOutputMetadataObjects:fromConnection:
+ @abstract
+    Called whenever an AVCaptureMetadataOutput instance emits new objects through a connection.
+
+ @param captureOutput
+    The AVCaptureMetadataOutput instance that emitted the objects.
+ @param metadataObjects
+    An array of AVMetadataObject subclasses (see AVMetadataObject.h).
+ @param connection
+    The AVCaptureConnection through which the objects were emitted.
+
+ @discussion
+    Delegates receive this message whenever the output captures and emits new objects, as specified by its metadataObjectTypes property. Delegates can use the provided objects in conjunction with other APIs for further processing. This method will be called on the dispatch queue specified by the output's metadataObjectsCallbackQueue property. This method may be called frequently, so it must be efficient to prevent capture performance problems, including dropped metadata objects.
+
+    Clients that need to reference metadata objects outside of the scope of this method must retain them and then release them when they are finished with them.
+*/
+- (void)captureOutput:(AVCaptureOutput *)captureOutput didOutputMetadataObjects:(NSArray *)metadataObjects fromConnection:(AVCaptureConnection *)connection;
+
+@end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureOutput.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureOutput.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureOutput.h	2015-09-30 23:18:01.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureOutput.h	2016-05-25 04:39:22.000000000 +0200
@@ -9,9 +9,6 @@
 #import <AVFoundation/AVBase.h>
 #import <Foundation/Foundation.h>
 #import <AVFoundation/AVCaptureSession.h>
-#import <CoreMedia/CMSampleBuffer.h>
-#import <QuartzCore/CALayer.h>
-#import <dispatch/dispatch.h>
 
 @class AVMetadataObject;
 @class AVCaptureOutputInternal;
@@ -22,17 +19,12 @@
     AVCaptureOutput is an abstract class that defines an interface for an output destination of an AVCaptureSession.
  
  @discussion
-    AVCaptureOutput provides an abstract interface for connecting capture output destinations, such as files and video
-    previews, to an AVCaptureSession.
+    AVCaptureOutput provides an abstract interface for connecting capture output destinations, such as files and video previews, to an AVCaptureSession.
 
-    An AVCaptureOutput can have multiple connections represented by AVCaptureConnection objects, one for each stream of
-    media that it receives from an AVCaptureInput. An AVCaptureOutput does not have any connections when it is first
-    created. When an output is added to an AVCaptureSession, connections are created that map media data from that
-    session's inputs to its outputs.
+    An AVCaptureOutput can have multiple connections represented by AVCaptureConnection objects, one for each stream of media that it receives from an AVCaptureInput. An AVCaptureOutput does not have any connections when it is first created. When an output is added to an AVCaptureSession, connections are created that map media data from that session's inputs to its outputs.
 
-    Concrete AVCaptureOutput instances can be added to an AVCaptureSession using the -[AVCaptureSession addOutput:] and
-    -[AVCaptureSession addOutputWithNoConnections:] methods.
-*/
+    Concrete AVCaptureOutput instances can be added to an AVCaptureSession using the -[AVCaptureSession addOutput:] and -[AVCaptureSession addOutputWithNoConnections:] methods.
+ */
 NS_CLASS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED
 @interface AVCaptureOutput : NSObject
 {
@@ -46,9 +38,8 @@
     The connections that describe the flow of media data to the receiver from AVCaptureInputs.
 
  @discussion
-    The value of this property is an NSArray of AVCaptureConnection objects, each describing the mapping between the
-    receiver and the AVCaptureInputPorts of one or more AVCaptureInputs.
-*/
+    The value of this property is an NSArray of AVCaptureConnection objects, each describing the mapping between the receiver and the AVCaptureInputPorts of one or more AVCaptureInputs.
+ */
 @property(nonatomic, readonly) NSArray *connections;
 
 /*!
@@ -60,10 +51,8 @@
     An AVMediaType constant from AVMediaFormat.h, e.g. AVMediaTypeVideo.
 
  @discussion
-    This convenience method returns the first AVCaptureConnection in the receiver's
-    connections array that has an AVCaptureInputPort of the specified mediaType.  If no
-    connection with the specified mediaType is found, nil is returned.
-*/
+    This convenience method returns the first AVCaptureConnection in the receiver's connections array that has an AVCaptureInputPort of the specified mediaType. If no connection with the specified mediaType is found, nil is returned.
+ */
 - (AVCaptureConnection *)connectionWithMediaType:(NSString *)mediaType NS_AVAILABLE(10_7, 5_0);
 
 /*!
@@ -73,1769 +62,56 @@
 
  @param metadataObject
     An AVMetadataObject originating from the same AVCaptureInput as the receiver.
- 
  @param connection
     The receiver's connection whose AVCaptureInput matches that of the metadata object to be converted.
-
  @result
     An AVMetadataObject whose properties are in output coordinates.
 
  @discussion
-    AVMetadataObject bounds may be expressed as a rect where {0,0} represents the top left of the picture area,
-    and {1,1} represents the bottom right on an unrotated picture.  Face metadata objects likewise express
-    yaw and roll angles with respect to an unrotated picture.  -transformedMetadataObjectForMetadataObject:connection: 
-	converts the visual properties in the coordinate space of the supplied AVMetadataObject to the coordinate space of 
-    the receiver.  The conversion takes orientation, mirroring, and scaling into consideration.
-    If the provided metadata object originates from an input source other than the preview layer's, nil will be returned.
+    AVMetadataObject bounds may be expressed as a rect where {0,0} represents the top left of the picture area, and {1,1} represents the bottom right on an unrotated picture. Face metadata objects likewise express yaw and roll angles with respect to an unrotated picture. -transformedMetadataObjectForMetadataObject:connection: converts the visual properties in the coordinate space of the supplied AVMetadataObject to the coordinate space of the receiver. The conversion takes orientation, mirroring, and scaling into consideration. If the provided metadata object originates from an input source other than the preview layer's, nil will be returned.
  
-    If an AVCaptureVideoDataOutput instance's connection's videoOrientation or videoMirrored properties are set to
-    non-default values, the output applies the desired mirroring and orientation by physically rotating and or flipping 
-    sample buffers as they pass through it.  AVCaptureStillImageOutput, on the other hand, does not physically rotate its buffers.
-    It attaches an appropriate kCGImagePropertyOrientation number to captured still image buffers (see ImageIO/CGImageProperties.h)
-    indicating how the image should be displayed on playback.  Likewise, AVCaptureMovieFileOutput does not physically
-    apply orientation/mirroring to its sample buffers -- it uses a QuickTime track matrix to indicate how the buffers
-    should be rotated and/or flipped on playback.
+    If an AVCaptureVideoDataOutput instance's connection's videoOrientation or videoMirrored properties are set to non-default values, the output applies the desired mirroring and orientation by physically rotating and or flipping sample buffers as they pass through it. AVCaptureStillImageOutput, on the other hand, does not physically rotate its buffers. It attaches an appropriate kCGImagePropertyOrientation number to captured still image buffers (see ImageIO/CGImageProperties.h) indicating how the image should be displayed on playback. Likewise, AVCaptureMovieFileOutput does not physically apply orientation/mirroring to its sample buffers -- it uses a QuickTime track matrix to indicate how the buffers should be rotated and/or flipped on playback.
  
-    transformedMetadataObjectForMetadataObject:connection: alters the visual properties of the provided metadata object 
-    to match the physical rotation / mirroring of the sample buffers provided by the receiver through the indicated 
-    connection.  I.e., for video data output, adjusted metadata object coordinates are rotated/mirrored.  For still image 
-    and movie file output, they are not.
-*/
+    transformedMetadataObjectForMetadataObject:connection: alters the visual properties of the provided metadata object to match the physical rotation / mirroring of the sample buffers provided by the receiver through the indicated connection. I.e., for video data output, adjusted metadata object coordinates are rotated/mirrored. For still image and movie file output, they are not.
+ */
 - (AVMetadataObject *)transformedMetadataObjectForMetadataObject:(AVMetadataObject *)metadataObject connection:(AVCaptureConnection *)connection NS_AVAILABLE_IOS(6_0);
 
 /*!
  @method metadataOutputRectOfInterestForRect:
  @abstract
-	Converts a rectangle in the receiver's coordinate space to a rectangle of interest in the coordinate space of an AVCaptureMetadataOutput
-	whose capture device is providing input to the receiver.
+    Converts a rectangle in the receiver's coordinate space to a rectangle of interest in the coordinate space of an AVCaptureMetadataOutput whose capture device is providing input to the receiver.
  
  @param rectInOutputCoordinates
-	A CGRect in the receiver's coordinates.
- 
+    A CGRect in the receiver's coordinates.
  @result
-	A CGRect in the coordinate space of the metadata output whose capture device is providing input to the receiver.
+    A CGRect in the coordinate space of the metadata output whose capture device is providing input to the receiver.
  
  @discussion
-	AVCaptureMetadataOutput rectOfInterest is expressed as a CGRect where {0,0} represents the top left of the picture area,
-	and {1,1} represents the bottom right on an unrotated picture.  This convenience method converts a rectangle in
-	the coordinate space of the receiver to a rectangle of interest in the coordinate space of an AVCaptureMetadataOutput
-	whose AVCaptureDevice is providing input to the receiver.  The conversion takes orientation, mirroring, and scaling into 
-	consideration.  See -transformedMetadataObjectForMetadataObject:connection: for a full discussion of how orientation and mirroring
-	are applied to sample buffers passing through the output.	
+    AVCaptureMetadataOutput rectOfInterest is expressed as a CGRect where {0,0} represents the top left of the picture area, and {1,1} represents the bottom right on an unrotated picture. This convenience method converts a rectangle in the coordinate space of the receiver to a rectangle of interest in the coordinate space of an AVCaptureMetadataOutput whose AVCaptureDevice is providing input to the receiver. The conversion takes orientation, mirroring, and scaling into consideration. See -transformedMetadataObjectForMetadataObject:connection: for a full discussion of how orientation and mirroring are applied to sample buffers passing through the output.
  */
 - (CGRect)metadataOutputRectOfInterestForRect:(CGRect)rectInOutputCoordinates NS_AVAILABLE_IOS(7_0);
 
 /*!
  @method rectForMetadataOutputRectOfInterest:
  @abstract
-	Converts a rectangle of interest in the coordinate space of an AVCaptureMetadataOutput whose capture device is
-	providing input to the receiver to a rectangle in the receiver's coordinates.
+    Converts a rectangle of interest in the coordinate space of an AVCaptureMetadataOutput whose capture device is providing input to the receiver to a rectangle in the receiver's coordinates.
  
  @param rectInMetadataOutputCoordinates
-	A CGRect in the coordinate space of the metadata output whose capture device is providing input to the receiver.
- 
+    A CGRect in the coordinate space of the metadata output whose capture device is providing input to the receiver.
  @result
-	A CGRect in the receiver's coordinates.
+    A CGRect in the receiver's coordinates.
  
  @discussion
-	AVCaptureMetadataOutput rectOfInterest is expressed as a CGRect where {0,0} represents the top left of the picture area,
-	and {1,1} represents the bottom right on an unrotated picture.  This convenience method converts a rectangle in the coordinate 
-	space of an AVCaptureMetadataOutput whose AVCaptureDevice is providing input to the coordinate space of the receiver.  The 
-	conversion takes orientation, mirroring, and scaling into consideration. See -transformedMetadataObjectForMetadataObject:connection: 
-	for a full discussion of how orientation and mirroring are applied to sample buffers passing through the output.
+    AVCaptureMetadataOutput rectOfInterest is expressed as a CGRect where {0,0} represents the top left of the picture area, and {1,1} represents the bottom right on an unrotated picture. This convenience method converts a rectangle in the coordinate space of an AVCaptureMetadataOutput whose AVCaptureDevice is providing input to the coordinate space of the receiver. The conversion takes orientation, mirroring, and scaling into consideration. See -transformedMetadataObjectForMetadataObject:connection: for a full discussion of how orientation and mirroring are applied to sample buffers passing through the output.
  */
 - (CGRect)rectForMetadataOutputRectOfInterest:(CGRect)rectInMetadataOutputCoordinates NS_AVAILABLE_IOS(7_0);
 
 @end
 
-
-@class AVCaptureVideoDataOutputInternal;
-@protocol AVCaptureVideoDataOutputSampleBufferDelegate;
-
-/*!
- @class AVCaptureVideoDataOutput
- @abstract
-    AVCaptureVideoDataOutput is a concrete subclass of AVCaptureOutput that can be used to process uncompressed or
-    compressed frames from the video being captured.
-
- @discussion
-    Instances of AVCaptureVideoDataOutput produce video frames suitable for processing using other media APIs.
-    Applications can access the frames with the captureOutput:didOutputSampleBuffer:fromConnection: delegate method.
-*/
-NS_CLASS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED
-@interface AVCaptureVideoDataOutput : AVCaptureOutput 
-{
-@private
-	AVCaptureVideoDataOutputInternal *_internal;
-}
-
-/*!
- @method setSampleBufferDelegate:queue:
- @abstract
-    Sets the receiver's delegate that will accept captured buffers and dispatch queue on which the delegate will be
-    called.
-
- @param sampleBufferDelegate
-    An object conforming to the AVCaptureVideoDataOutputSampleBufferDelegate protocol that will receive sample buffers
-    after they are captured.
- @param sampleBufferCallbackQueue
-    A dispatch queue on which all sample buffer delegate methods will be called.
-
- @discussion
-    When a new video sample buffer is captured it will be vended to the sample buffer delegate using the
-    captureOutput:didOutputSampleBuffer:fromConnection: delegate method. All delegate methods will be called on the
-    specified dispatch queue. If the queue is blocked when new frames are captured, those frames will be automatically
-    dropped at a time determined by the value of the alwaysDiscardsLateVideoFrames property. This allows clients to
-    process existing frames on the same queue without having to manage the potential memory usage increases that would
-    otherwise occur when that processing is unable to keep up with the rate of incoming frames. If their frame processing
-    is consistently unable to keep up with the rate of incoming frames, clients should consider using the
-    minFrameDuration property, which will generally yield better performance characteristics and more consistent frame
-    rates than frame dropping alone.
-
-    Clients that need to minimize the chances of frames being dropped should specify a queue on which a sufficiently
-    small amount of processing is being done outside of receiving sample buffers. However, if such clients migrate extra
-    processing to another queue, they are responsible for ensuring that memory usage does not grow without bound from
-    frames that have not been processed.
-
-    A serial dispatch queue must be used to guarantee that video frames will be delivered in order.
-    The sampleBufferCallbackQueue parameter may not be NULL, except when setting the sampleBufferDelegate
-    to nil.
-*/
-- (void)setSampleBufferDelegate:(id<AVCaptureVideoDataOutputSampleBufferDelegate>)sampleBufferDelegate queue:(dispatch_queue_t)sampleBufferCallbackQueue;
-
-/*!
- @property sampleBufferDelegate
- @abstract
-    The receiver's delegate.
-
- @discussion
-    The value of this property is an object conforming to the AVCaptureVideoDataOutputSampleBufferDelegate protocol that
-    will receive sample buffers after they are captured. The delegate is set using the setSampleBufferDelegate:queue:
-    method.
-*/
-@property(nonatomic, readonly) id<AVCaptureVideoDataOutputSampleBufferDelegate> sampleBufferDelegate;
-
-/*!
- @property sampleBufferCallbackQueue
- @abstract
-    The dispatch queue on which all sample buffer delegate methods will be called.
-
- @discussion
-    The value of this property is a dispatch_queue_t. The queue is set using the setSampleBufferDelegate:queue: method.
-*/
-@property(nonatomic, readonly) dispatch_queue_t sampleBufferCallbackQueue;
-
-/*!
- @property videoSettings
- @abstract
-    Specifies the settings used to decode or re-encode video before it is output by the receiver.
-
- @discussion
-    See AVVideoSettings.h for more information on how to construct a video settings dictionary.  To receive samples in their 
-    device native format, set this property to an empty dictionary (i.e. [NSDictionary dictionary]).  To receive samples in
-    a default uncompressed format, set this property to nil.  Note that after this property is set to nil, subsequent
-    querying of this property will yield a non-nil dictionary reflecting the settings used by the AVCaptureSession's current 
-    sessionPreset.
-
-    On iOS, the only supported key is kCVPixelBufferPixelFormatTypeKey. Supported pixel formats are
-    kCVPixelFormatType_420YpCbCr8BiPlanarVideoRange, kCVPixelFormatType_420YpCbCr8BiPlanarFullRange and kCVPixelFormatType_32BGRA.
-*/
-@property(nonatomic, copy) NSDictionary *videoSettings;
-
-/*!
- @method recommendedVideoSettingsForAssetWriterWithOutputFileType:
- @abstract
-    Specifies the recommended settings for use with an AVAssetWriterInput.
-
- @param outputFileType
-    Specifies the UTI of the file type to be written (see AVMediaFormat.h for a list of file format UTIs).
- 
- @return
-    A fully populated dictionary of keys and values that are compatible with AVAssetWriter.
- 
- @discussion
-    The value of this property is an NSDictionary containing values for compression settings keys defined in
-    AVVideoSettings.h.  This dictionary is suitable for use as the "outputSettings" parameter when creating an AVAssetWriterInput, such as,
-        
-       [AVAssetWriterInput assetWriterInputWithMediaType:AVMediaTypeVideo outputSettings:outputSettings sourceFormatHint:hint];
-    
-	The dictionary returned contains all necessary keys and values needed by AVAssetWriter (see AVAssetWriterInput.h, 
-    -initWithMediaType:outputSettings: for a more in depth discussion). For QuickTime movie and ISO file types,
-    the recommended video settings will produce output comparable to that of AVCaptureMovieFileOutput.
-
-    Note that the dictionary of settings is dependent on the current configuration of the receiver's AVCaptureSession
-    and its inputs.  The settings dictionary may change if the session's configuration changes.  As such, you should
-    configure your session first, then query the recommended video settings.  As of iOS 8.3, movies produced with these
-    settings successfully import into the iOS camera roll and sync to and from like devices via iTunes.
-*/
-- (NSDictionary *)recommendedVideoSettingsForAssetWriterWithOutputFileType:(NSString *)outputFileType NS_AVAILABLE_IOS(7_0);
-
-/*!
- @property availableVideoCVPixelFormatTypes
- @abstract
-    Indicates the supported video pixel formats that can be specified in videoSettings.
-
- @discussion
-    The value of this property is an NSArray of NSNumbers that can be used as values for the 
-    kCVPixelBufferPixelFormatTypeKey in the receiver's videoSettings property.  The first
-    format in the returned list is the most efficient output format.
-*/
-@property(nonatomic, readonly) NSArray *availableVideoCVPixelFormatTypes NS_AVAILABLE(10_7, 5_0);
-
-/*!
- @property availableVideoCodecTypes
- @abstract
-    Indicates the supported video codec formats that can be specified in videoSettings.
-
- @discussion
-    The value of this property is an NSArray of NSStrings that can be used as values for the 
-    AVVideoCodecKey in the receiver's videoSettings property.
-*/
-@property(nonatomic, readonly) NSArray *availableVideoCodecTypes NS_AVAILABLE(10_7, 5_0);
-
-/*!
- @property minFrameDuration
- @abstract
-    Specifies the minimum time interval between which the receiver should output consecutive video frames.
-
- @discussion
-    The value of this property is a CMTime specifying the minimum duration of each video frame output by the receiver,
-    placing a lower bound on the amount of time that should separate consecutive frames. This is equivalent to the
-    inverse of the maximum frame rate. A value of kCMTimeZero or kCMTimeInvalid indicates an unlimited maximum frame
-    rate. The default value is kCMTimeInvalid.  As of iOS 5.0, minFrameDuration is deprecated.  Use AVCaptureConnection's
-    videoMinFrameDuration property instead.
-*/
-@property(nonatomic) CMTime minFrameDuration NS_DEPRECATED_IOS(4_0, 5_0, "Use AVCaptureConnection's videoMinFrameDuration property instead.");
-
-/*!
- @property alwaysDiscardsLateVideoFrames
- @abstract
-    Specifies whether the receiver should always discard any video frame that is not processed before the next frame is
-    captured.
-
- @discussion
-    When the value of this property is YES, the receiver will immediately discard frames that are captured while the
-    dispatch queue handling existing frames is blocked in the captureOutput:didOutputSampleBuffer:fromConnection:
-    delegate method. When the value of this property is NO, delegates will be allowed more time to process old frames
-    before new frames are discarded, but application memory usage may increase significantly as a result. The default
-    value is YES.
-*/
-@property(nonatomic) BOOL alwaysDiscardsLateVideoFrames;
-
-@end
-
-/*!
- @protocol AVCaptureVideoDataOutputSampleBufferDelegate
- @abstract
-    Defines an interface for delegates of AVCaptureVideoDataOutput to receive captured video sample buffers and be
-    notified of late sample buffers that were dropped.
-*/
-__TVOS_PROHIBITED
-@protocol AVCaptureVideoDataOutputSampleBufferDelegate <NSObject>
-
-@optional
-
-/*!
- @method captureOutput:didOutputSampleBuffer:fromConnection:
- @abstract
-    Called whenever an AVCaptureVideoDataOutput instance outputs a new video frame.
-
- @param captureOutput
-    The AVCaptureVideoDataOutput instance that output the frame.
- @param sampleBuffer
-    A CMSampleBuffer object containing the video frame data and additional information about the frame, such as its
-    format and presentation time.
- @param connection
-    The AVCaptureConnection from which the video was received.
-
- @discussion
-    Delegates receive this message whenever the output captures and outputs a new video frame, decoding or re-encoding it
-    as specified by its videoSettings property. Delegates can use the provided video frame in conjunction with other APIs
-    for further processing. This method will be called on the dispatch queue specified by the output's
-    sampleBufferCallbackQueue property. This method is called periodically, so it must be efficient to prevent capture
-    performance problems, including dropped frames.
-
-    Clients that need to reference the CMSampleBuffer object outside of the scope of this method must CFRetain it and
-    then CFRelease it when they are finished with it.
-
-    Note that to maintain optimal performance, some sample buffers directly reference pools of memory that may need to be
-    reused by the device system and other capture inputs. This is frequently the case for uncompressed device native
-    capture where memory blocks are copied as little as possible. If multiple sample buffers reference such pools of
-    memory for too long, inputs will no longer be able to copy new samples into memory and those samples will be dropped.
-    If your application is causing samples to be dropped by retaining the provided CMSampleBuffer objects for too long,
-    but it needs access to the sample data for a long period of time, consider copying the data into a new buffer and
-    then calling CFRelease on the sample buffer if it was previously retained so that the memory it references can be
-    reused.
-*/
-- (void)captureOutput:(AVCaptureOutput *)captureOutput didOutputSampleBuffer:(CMSampleBufferRef)sampleBuffer fromConnection:(AVCaptureConnection *)connection;
-
-/*!
- @method captureOutput:didDropSampleBuffer:fromConnection:
- @abstract
-    Called once for each frame that is discarded.
-
- @param captureOutput
-    The AVCaptureVideoDataOutput instance that dropped the frame.
- @param sampleBuffer
-    A CMSampleBuffer object containing information about the dropped frame, such as its format and presentation time.
-    This sample buffer will contain none of the original video data.
- @param connection
-    The AVCaptureConnection from which the dropped video frame was received.
-
- @discussion
-    Delegates receive this message whenever a video frame is dropped. This method is called once 
-    for each dropped frame. The CMSampleBuffer object passed to this delegate method will contain metadata 
-    about the dropped video frame, such as its duration and presentation time stamp, but will contain no 
-    actual video data. On iOS, Included in the sample buffer attachments is the kCMSampleBufferAttachmentKey_DroppedFrameReason,
-    which indicates why the frame was dropped.  This method will be called on the dispatch queue specified by the output's
-    sampleBufferCallbackQueue property. Because this method will be called on the same dispatch queue that is responsible
-    for outputting video frames, it must be efficient to prevent further capture performance problems, such as additional
-    dropped video frames.
- */
-- (void)captureOutput:(AVCaptureOutput *)captureOutput didDropSampleBuffer:(CMSampleBufferRef)sampleBuffer fromConnection:(AVCaptureConnection *)connection NS_AVAILABLE(10_7, 6_0);
-
-@end
-
-
-@class AVCaptureAudioDataOutputInternal;
-@protocol AVCaptureAudioDataOutputSampleBufferDelegate;
-
-/*!
- @class AVCaptureAudioDataOutput
- @abstract
-    AVCaptureAudioDataOutput is a concrete subclass of AVCaptureOutput that can be used to process uncompressed or
-    compressed samples from the audio being captured.
- 
- @discussion
-    Instances of AVCaptureAudioDataOutput produce audio sample buffers suitable for processing using other media APIs.
-    Applications can access the sample buffers with the captureOutput:didOutputSampleBuffer:fromConnection: delegate
-    method.
-*/
-NS_CLASS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED
-@interface AVCaptureAudioDataOutput : AVCaptureOutput 
-{
-@private
-	AVCaptureAudioDataOutputInternal *_internal;
-}
-
-/*!
- @method setSampleBufferDelegate:queue:
- @abstract
-    Sets the receiver's delegate that will accept captured buffers and dispatch queue on which the delegate will be
-    called.
-
- @param sampleBufferDelegate
-    An object conforming to the AVCaptureAudioDataOutputSampleBufferDelegate protocol that will receive sample buffers
-    after they are captured.
- @param sampleBufferCallbackQueue
-    A dispatch queue on which all sample buffer delegate methods will be called.
-
- @discussion
-    When a new audio sample buffer is captured it will be vended to the sample buffer delegate using the
-    captureOutput:didOutputSampleBuffer:fromConnection: delegate method. All delegate methods will be called on the
-    specified dispatch queue. If the queue is blocked when new samples are captured, those samples will be automatically
-    dropped when they become sufficiently late. This allows clients to process existing samples on the same queue without
-    having to manage the potential memory usage increases that would otherwise occur when that processing is unable to
-    keep up with the rate of incoming samples.
-
-    Clients that need to minimize the chances of samples being dropped should specify a queue on which a sufficiently
-    small amount of processing is being done outside of receiving sample buffers. However, if such clients migrate extra
-    processing to another queue, they are responsible for ensuring that memory usage does not grow without bound from
-    samples that have not been processed.
-
-    A serial dispatch queue must be used to guarantee that audio samples will be delivered in order.
-    The sampleBufferCallbackQueue parameter may not be NULL, except when setting sampleBufferDelegate to nil.
-*/
-- (void)setSampleBufferDelegate:(id<AVCaptureAudioDataOutputSampleBufferDelegate>)sampleBufferDelegate queue:(dispatch_queue_t)sampleBufferCallbackQueue;
-
-/*!
- @property sampleBufferDelegate
- @abstract
-    The receiver's delegate.
-
- @discussion
-    The value of this property is an object conforming to the AVCaptureAudioDataOutputSampleBufferDelegate protocol that
-    will receive sample buffers after they are captured. The delegate is set using the setSampleBufferDelegate:queue:
-    method.
-*/
-@property(nonatomic, readonly) id<AVCaptureAudioDataOutputSampleBufferDelegate> sampleBufferDelegate;
-
-/*!
- @property sampleBufferCallbackQueue
- @abstract
-    The dispatch queue on which all sample buffer delegate methods will be called.
-
- @discussion
-    The value of this property is a dispatch_queue_t. The queue is set using the setSampleBufferDelegate:queue: method.
-*/
-@property(nonatomic, readonly) dispatch_queue_t sampleBufferCallbackQueue;
-
-#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
-
-/*!
- @property	 audioSettings
- @abstract
-    Specifies the settings used to decode or re-encode audio before it is output by the receiver.
-
- @discussion
-    The value of this property is an NSDictionary containing values for audio settings keys defined 
-    in AVAudioSettings.h.  When audioSettings is set to nil, the AVCaptureAudioDataOutput vends samples
-    in their device native format.
-*/
-@property(nonatomic, copy) NSDictionary *audioSettings NS_AVAILABLE(10_7, NA);
-
-#endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
-
-/*!
- @method recommendedAudioSettingsForAssetWriterWithOutputFileType:
- @abstract
-    Specifies the recommended settings for use with an AVAssetWriterInput.
-
- @param outputFileType
-    Specifies the UTI of the file type to be written (see AVMediaFormat.h for a list of file format UTIs).
- 
- @return
-    A fully populated dictionary of keys and values that are compatible with AVAssetWriter.
- 
- @discussion
-    The value of this property is an NSDictionary containing values for compression settings keys defined in
-    AVAudioSettings.h.  This dictionary is suitable for use as the "outputSettings" parameter when creating an AVAssetWriterInput, such as,
-        
-       [AVAssetWriterInput assetWriterInputWithMediaType:AVMediaTypeAudio outputSettings:outputSettings sourceFormatHint:hint];
-    
-	The dictionary returned contains all necessary keys and values needed by AVAssetWriter (see AVAssetWriterInput.h, 
-    -initWithMediaType:outputSettings: for a more in depth discussion).  For QuickTime movie and ISO files, the 
-    recommended audio settings will always produce output comparable to that of AVCaptureMovieFileOutput.
-
-	Note that the dictionary of settings is dependent on the current configuration of the receiver's AVCaptureSession
-    and its inputs.  The settings dictionary may change if the session's configuration changes.  As such, you should
-    configure your session first, then query the recommended audio settings.
-*/
-- (NSDictionary *)recommendedAudioSettingsForAssetWriterWithOutputFileType:(NSString *)outputFileType NS_AVAILABLE_IOS(7_0);
-
-@end
-
-/*!
- @protocol AVCaptureAudioDataOutputSampleBufferDelegate
- @abstract
-    Defines an interface for delegates of AVCaptureAudioDataOutput to receive captured audio sample buffers.
-*/
-__TVOS_PROHIBITED
-@protocol AVCaptureAudioDataOutputSampleBufferDelegate <NSObject>
-
-@optional
-
-/*!
- @method captureOutput:didOutputSampleBuffer:fromConnection:
- @abstract
-    Called whenever an AVCaptureAudioDataOutput instance outputs a new audio sample buffer.
-
- @param captureOutput
-    The AVCaptureAudioDataOutput instance that output the samples.
- @param sampleBuffer
-    A CMSampleBuffer object containing the audio samples and additional information about them, such as their format and
-    presentation time.
- @param connection
-    The AVCaptureConnection from which the audio was received.
-
- @discussion
-    Delegates receive this message whenever the output captures and outputs new audio samples, decoding or re-encoding
-    as specified by the audioSettings property. Delegates can use the provided sample buffer in conjunction with other
-    APIs for further processing. This method will be called on the dispatch queue specified by the output's
-    sampleBufferCallbackQueue property. This method is called periodically, so it must be efficient to prevent capture
-    performance problems, including dropped audio samples.
-
-    Clients that need to reference the CMSampleBuffer object outside of the scope of this method must CFRetain it and
-    then CFRelease it when they are finished with it.
-*/
-- (void)captureOutput:(AVCaptureOutput *)captureOutput didOutputSampleBuffer:(CMSampleBufferRef)sampleBuffer fromConnection:(AVCaptureConnection *)connection;
-
-@end
-
-
-@class AVCaptureFileOutputInternal;
-@protocol AVCaptureFileOutputRecordingDelegate;
-
-#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
-@protocol AVCaptureFileOutputDelegate;
-#endif
-
-/*!
- @class AVCaptureFileOutput
- @abstract
-    AVCaptureFileOutput is an abstract subclass of AVCaptureOutput that provides an interface for writing captured media
-    to files.
- 
- @discussion
-    This abstract superclass defines the interface for outputs that record media samples to files. File outputs can start
-    recording to a new file using the startRecordingToOutputFileURL:recordingDelegate: method. On successive invocations of this method on
-    Mac OS X, the output file can by changed dynamically without losing media samples. A file output can stop recording
-    using the stopRecording method. Because files are recorded in the background, applications will need to specify a
-    delegate for each new file so that they can be notified when recorded files are finished.
-
-    On Mac OS X, clients can also set a delegate on the file output itself that can be used to control recording along
-    exact media sample boundaries using the captureOutput:didOutputSampleBuffer:fromConnection: method.
-
-    The concrete subclasses of AVCaptureFileOutput are AVCaptureMovieFileOutput, which records media to a QuickTime movie
-    file, and AVCaptureAudioFileOutput, which writes audio media to a variety of audio file formats.
-*/
-NS_CLASS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED
-@interface AVCaptureFileOutput : AVCaptureOutput 
-{
-@private
-	AVCaptureFileOutputInternal *_fileOutputInternal;
-}
-
-#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
-
-/*!
- @property delegate
- @abstract
-    The receiver's delegate.
-
- @discussion
-    The value of this property is an object conforming to the AVCaptureFileOutputDelegate protocol that will be able to
-    monitor and control recording along exact sample boundaries.
-*/
-@property(nonatomic, assign) id<AVCaptureFileOutputDelegate> delegate NS_AVAILABLE(10_7, NA);
-
-#endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
-
-/*!
- @property outputFileURL
- @abstract
-    The file URL of the file to which the receiver is currently recording incoming buffers.
-
- @discussion
-    The value of this property is an NSURL object containing the file URL of the file currently being written by the
-    receiver. Returns nil if the receiver is not recording to any file.
-*/
-@property(nonatomic, readonly) NSURL *outputFileURL;
-
-/*!
- @method startRecordingToOutputFileURL:recordingDelegate:
- @abstract
-    Tells the receiver to start recording to a new file, and specifies a delegate that will be notified when recording is
-    finished.
- 
- @param outputFileURL
-    An NSURL object containing the URL of the output file. This method throws an NSInvalidArgumentException if the URL is
-    not a valid file URL.
- @param delegate
-    An object conforming to the AVCaptureFileOutputRecordingDelegate protocol. Clients must specify a delegate so that
-    they can be notified when recording to the given URL is finished.
-
- @discussion
-    The method sets the file URL to which the receiver is currently writing output media. If a file at the given URL
-    already exists when capturing starts, recording to the new file will fail.
-
-    Clients need not call stopRecording before calling this method while another recording is in progress. On Mac OS X,
-    if this method is invoked while an existing output file was already being recorded, no media samples will be
-    discarded between the old file and the new file.
-
-    When recording is stopped either by calling stopRecording, by changing files using this method, or because of an
-    error, the remaining data that needs to be included to the file will be written in the background. Therefore, clients
-    must specify a delegate that will be notified when all data has been written to the file using the
-    captureOutput:didFinishRecordingToOutputFileAtURL:fromConnections:error: method. The recording delegate can also
-    optionally implement methods that inform it when data starts being written, when recording is paused and resumed, and
-    when recording is about to be finished.
-
-    On Mac OS X, if this method is called within the captureOutput:didOutputSampleBuffer:fromConnection: delegate method,
-    the first samples written to the new file are guaranteed to be those contained in the sample buffer passed to that
-    method.
-
-    Note: AVCaptureAudioFileOutput does not support -startRecordingToOutputFileURL:recordingDelegate:.  Use
-    -startRecordingToOutputFileURL:outputFileType:recordingDelegate: instead.
-*/
-- (void)startRecordingToOutputFileURL:(NSURL*)outputFileURL recordingDelegate:(id<AVCaptureFileOutputRecordingDelegate>)delegate;
-
-/*!
- @method stopRecording
- @abstract
-    Tells the receiver to stop recording to the current file.
-
- @discussion
-    Clients can call this method when they want to stop recording new samples to the current file, and do not want to
-    continue recording to another file. Clients that want to switch from one file to another should not call this method.
-    Instead they should simply call startRecordingToOutputFileURL:recordingDelegate: with the new file URL.
-
-    When recording is stopped either by calling this method, by changing files using
-    startRecordingToOutputFileURL:recordingDelegate:, or because of an error, the remaining data that needs to be
-    included to the file will be written in the background. Therefore, before using the file, clients must wait until the
-    delegate that was specified in startRecordingToOutputFileURL:recordingDelegate: is notified when all data has been
-    written to the file using the captureOutput:didFinishRecordingToOutputFileAtURL:fromConnections:error: method.
-
-    On Mac OS X, if this method is called within the captureOutput:didOutputSampleBuffer:fromConnection: delegate method,
-    the last samples written to the current file are guaranteed to be those that were output immediately before those in
-    the sample buffer passed to that method.
-*/
-- (void)stopRecording;
-
-/*!
- @property recording
- @abstract
-    Indicates whether the receiver is currently recording.
-
- @discussion
-    The value of this property is YES when the receiver currently has a file to which it is writing new samples, NO
-    otherwise.
-*/
-@property(nonatomic, readonly, getter=isRecording) BOOL recording;
-
-#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
-
-/*!
- @property recordingPaused
- @abstract
-    Indicates whether recording to the current output file is paused.
-
- @discussion
-    This property indicates recording to the file returned by outputFileURL has been previously paused using the
-    pauseRecording method. When a recording is paused, captured samples are not written to the output file, but new
-    samples can be written to the same file in the future by calling resumeRecording.
-*/
-@property(nonatomic, readonly, getter=isRecordingPaused) BOOL recordingPaused NS_AVAILABLE(10_7, NA);
-
-/*!
- @method pauseRecording
- @abstract
-    Pauses recording to the current output file.
-
- @discussion
-    This method causes the receiver to stop writing captured samples to the current output file returned by
-    outputFileURL, but leaves the file open so that samples can be written to it in the future, when resumeRecording is
-    called. This allows clients to record multiple media segments that are not contiguous in time to a single file.
-
-    On Mac OS X, if this method is called within the captureOutput:didOutputSampleBuffer:fromConnection: delegate method,
-    the last samples written to the current file are guaranteed to be those that were output immediately before those in
-    the sample buffer passed to that method. 
-*/
-- (void)pauseRecording NS_AVAILABLE(10_7, NA);
-
-/*!
- @method resumeRecording
- @abstract
-    Resumes recording to the current output file after it was previously paused using pauseRecording.
-
- @discussion
-    This method causes the receiver to resume writing captured samples to the current output file returned by
-    outputFileURL, after recording was previously paused using pauseRecording. This allows clients to record multiple
-    media segments that are not contiguous in time to a single file. 
-
-    On Mac OS X, if this method is called within the captureOutput:didOutputSampleBuffer:fromConnection: delegate method,
-    the first samples written to the current file are guaranteed to be those contained in the sample buffer passed to
-    that method.
-*/
-- (void)resumeRecording NS_AVAILABLE(10_7, NA);
-
-#endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
-
-/*!
- @property recordedDuration
- @abstract
-    Indicates the duration of the media recorded to the current output file.
-
- @discussion
-    If recording is in progress, this property returns the total time recorded so far.
-*/
-@property(nonatomic, readonly) CMTime recordedDuration;
-
-/*!
- @property recordedFileSize
- @abstract
-    Indicates the size, in bytes, of the data recorded to the current output file.
-
- @discussion
-    If a recording is in progress, this property returns the size in bytes of the data recorded so far.
-*/
-@property(nonatomic, readonly) int64_t recordedFileSize;	
-
-/*!
- @property maxRecordedDuration
- @abstract
-    Specifies the maximum duration of the media that should be recorded by the receiver.
-
- @discussion
-    This property specifies a hard limit on the duration of recorded files. Recording is stopped when the limit is
-    reached and the captureOutput:didFinishRecordingToOutputFileAtURL:fromConnections:error: delegate method is invoked
-    with an appropriate error. The default value of this property is kCMTimeInvalid, which indicates no limit.
-*/
-@property(nonatomic) CMTime maxRecordedDuration;
-
-/*!
- @property maxRecordedFileSize
- @abstract
-    Specifies the maximum size, in bytes, of the data that should be recorded by the receiver.
- 
- @discussion
-    This property specifies a hard limit on the data size of recorded files. Recording is stopped when the limit is
-    reached and the captureOutput:didFinishRecordingToOutputFileAtURL:fromConnections:error: delegate method is invoked
-    with an appropriate error. The default value of this property is 0, which indicates no limit.
-*/
-@property(nonatomic) int64_t maxRecordedFileSize;
-
-/*!
- @property minFreeDiskSpaceLimit
- @abstract
-    Specifies the minimum amount of free space, in bytes, required for recording to continue on a given volume.
-
- @discussion
-    This property specifies a hard lower limit on the amount of free space that must remain on a target volume for
-    recording to continue. Recording is stopped when the limit is reached and the
-    captureOutput:didFinishRecordingToOutputFileAtURL:fromConnections:error: delegate method is invoked with an
-    appropriate error.
-*/
-@property(nonatomic) int64_t minFreeDiskSpaceLimit;
-
-@end
-
-/*!
- @protocol AVCaptureFileOutputRecordingDelegate
- @abstract
-    Defines an interface for delegates of AVCaptureFileOutput to respond to events that occur in the process of recording
-    a single file.
-*/
-__TVOS_PROHIBITED
-@protocol AVCaptureFileOutputRecordingDelegate <NSObject>
-
-@optional
-
-/*!
- @method captureOutput:didStartRecordingToOutputFileAtURL:fromConnections:
- @abstract
-    Informs the delegate when the output has started writing to a file.
-
- @param captureOutput
-    The capture file output that started writing the file.
- @param fileURL
-    The file URL of the file that is being written.
- @param connections
-    An array of AVCaptureConnection objects attached to the file output that provided the data that is being written to
-    the file.
-
- @discussion
-    This method is called when the file output has started writing data to a file. If an error condition prevents any
-    data from being written, this method may not be called.
-    captureOutput:willFinishRecordingToOutputFileAtURL:fromConnections:error: and
-    captureOutput:didFinishRecordingToOutputFileAtURL:fromConnections:error: will always be called, even if no data is
-    written.
-
-    Clients should not assume that this method will be called on a specific thread, and should also try to make this
-    method as efficient as possible.
-*/
-- (void)captureOutput:(AVCaptureFileOutput *)captureOutput didStartRecordingToOutputFileAtURL:(NSURL *)fileURL fromConnections:(NSArray *)connections;
-
-#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
-
-/*!
- @method captureOutput:didPauseRecordingToOutputFileAtURL:fromConnections:
- @abstract
-    Called whenever the output is recording to a file and successfully pauses the recording at the request of the client.
-
- @param captureOutput
-    The capture file output that has paused its file recording.
- @param fileURL
-    The file URL of the file that is being written.
- @param connections
-    An array of AVCaptureConnection objects attached to the file output that provided the data that is being written to
-    the file.
-
- @discussion
-    Delegates can use this method to be informed when a request to pause recording is actually respected. It is safe for
-    delegates to change what the file output is currently doing (starting a new file, for example) from within this
-    method. If recording to a file is stopped, either manually or due to an error, this method is not guaranteed to be
-    called, even if a previous call to pauseRecording was made.
-
-    Clients should not assume that this method will be called on a specific thread, and should also try to make this
-    method as efficient as possible.
-*/
-- (void)captureOutput:(AVCaptureFileOutput *)captureOutput didPauseRecordingToOutputFileAtURL:(NSURL *)fileURL fromConnections:(NSArray *)connections NS_AVAILABLE(10_7, NA);
-
-/*!
- @method captureOutput:didResumeRecordingToOutputFileAtURL:fromConnections:
- @abstract
-    Called whenever the output, at the request of the client, successfully resumes a file recording that was paused.
-
- @param captureOutput
-    The capture file output that has resumed its paused file recording.
- @param fileURL
-    The file URL of the file that is being written.
- @param connections
-    An array of AVCaptureConnection objects attached to the file output that provided the data that is being written to
-    the file.
-
- @discussion
-    Delegates can use this method to be informed when a request to resume recording is actually respected. It is safe for
-    delegates to change what the file output is currently doing (starting a new file, for example) from within this
-    method. If recording to a file is stopped, either manually or due to an error, this method is not guaranteed to be
-    called, even if a previous call to resumeRecording was made.
-
-    Clients should not assume that this method will be called on a specific thread, and should also try to make this
-    method as efficient as possible.
-*/
-- (void)captureOutput:(AVCaptureFileOutput *)captureOutput didResumeRecordingToOutputFileAtURL:(NSURL *)fileURL fromConnections:(NSArray *)connections NS_AVAILABLE(10_7, NA);
-
-/*!
- @method captureOutput:willFinishRecordingToOutputFileAtURL:fromConnections:error:
- @abstract
-    Informs the delegate when the output will stop writing new samples to a file.
-
- @param captureOutput
-    The capture file output that will finish writing the file.
- @param fileURL
-    The file URL of the file that is being written.
- @param connections
-    An array of AVCaptureConnection objects attached to the file output that provided the data that is being written to
-    the file.
- @param error
-    An error describing what caused the file to stop recording, or nil if there was no error.
-
- @discussion
-    This method is called when the file output will stop recording new samples to the file at outputFileURL, either
-    because startRecordingToOutputFileURL:recordingDelegate: or stopRecording were called, or because an error, described
-    by the error parameter, occurred (if no error occurred, the error parameter will be nil). This method will always be
-    called for each recording request, even if no data is successfully written to the file.
-
-    Clients should not assume that this method will be called on a specific thread, and should also try to make this
-    method as efficient as possible.
-*/
-- (void)captureOutput:(AVCaptureFileOutput *)captureOutput willFinishRecordingToOutputFileAtURL:(NSURL *)fileURL fromConnections:(NSArray *)connections error:(NSError *)error NS_AVAILABLE(10_7, NA);
-
-#endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
-
-@required
-
-/*!
- @method captureOutput:didFinishRecordingToOutputFileAtURL:fromConnections:error:
- @abstract
-    Informs the delegate when all pending data has been written to an output file.
-
- @param captureOutput
-    The capture file output that has finished writing the file.
- @param fileURL
-    The file URL of the file that has been written.
- @param connections
-    An array of AVCaptureConnection objects attached to the file output that provided the data that was written to the
-    file.
- @param error
-    An error describing what caused the file to stop recording, or nil if there was no error.
-
- @discussion
-    This method is called when the file output has finished writing all data to a file whose recording was stopped,
-    either because startRecordingToOutputFileURL:recordingDelegate: or stopRecording were called, or because an error,
-    described by the error parameter, occurred (if no error occurred, the error parameter will be nil).  This method will
-    always be called for each recording request, even if no data is successfully written to the file.
-
-    Clients should not assume that this method will be called on a specific thread.
-
-    Delegates are required to implement this method.
-*/
-- (void)captureOutput:(AVCaptureFileOutput *)captureOutput didFinishRecordingToOutputFileAtURL:(NSURL *)outputFileURL fromConnections:(NSArray *)connections error:(NSError *)error;
-
-@end
-
-#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
-
-/*!
- @protocol AVCaptureFileOutputDelegate
- @abstract
-    Defines an interface for delegates of AVCaptureFileOutput to monitor and control recordings along exact sample
-    boundaries.
-*/
-@protocol AVCaptureFileOutputDelegate <NSObject>
-
-@required
-
-/*!
- @method captureOutputShouldProvideSampleAccurateRecordingStart:
- @abstract
-    Allows a client to opt in to frame accurate record-start in captureOutput:didOutputSampleBuffer:fromConnection:
-
- @param captureOutput
-    The AVCaptureFileOutput instance with which the delegate is associated.
-
- @discussion
-    In apps linked before Mac OS X 10.8, delegates that implement the captureOutput:didOutputSampleBuffer:fromConnection: 
-    method can ensure frame accurate start / stop of a recording by calling startRecordingToOutputFileURL:recordingDelegate:
-    from within the callback.  Frame accurate start requires the capture output to apply outputSettings
-    when the session starts running, so it is ready to record on any given frame boundary.  Compressing
-    all the time while the session is running has power, thermal, and CPU implications.  In apps linked on or after
-    Mac OS X 10.8, delegates must implement captureOutputShouldProvideSampleAccurateRecordingStart: to indicate
-    whether frame accurate start/stop recording is required (returning YES) or not (returning NO).
-    The output calls this method as soon as the delegate is added, and never again.  If your delegate returns
-    NO, the capture output applies compression settings when startRecordingToOutputFileURL:recordingDelegate: is called, 
-    and disables compression settings after the recording is stopped.
-*/
-- (BOOL)captureOutputShouldProvideSampleAccurateRecordingStart:(AVCaptureOutput *)captureOutput NS_AVAILABLE(10_8, NA);
-
-@optional
-
-/*!
- @method captureOutput:didOutputSampleBuffer:fromConnection:
- @abstract
-    Gives the delegate the opportunity to inspect samples as they are received by the output and optionally start and
-    stop recording at exact times.
-
- @param captureOutput
-    The capture file output that is receiving the media data.
- @param sampleBuffer
-    A CMSampleBuffer object containing the sample data and additional information about the sample, such as its format
-    and presentation time.
- @param connection
-    The AVCaptureConnection object attached to the file output from which the sample data was received.
-
- @discussion
-    This method is called whenever the file output receives a single sample buffer (a single video frame or audio buffer,
-    for example) from the given connection. This gives delegates an opportunity to start and stop recording or change
-    output files at an exact sample boundary if -captureOutputShouldProvideSampleAccurateRecordingStart: returns YES. 
-    If called from within this method, the file output's startRecordingToOutputFileURL:recordingDelegate: and 
-    resumeRecording methods are guaranteed to include the received sample buffer in the new file, whereas calls to 
-    stopRecording and pauseRecording are guaranteed to include all samples leading up to those in the current sample 
-    buffer in the existing file.
-
-    Delegates can gather information particular to the samples by inspecting the CMSampleBuffer object. Sample buffers
-    always contain a single frame of video if called from this method but may also contain multiple samples of audio. For
-    B-frame video formats, samples are always delivered in presentation order.
-
-    Clients that need to reference the CMSampleBuffer object outside of the scope of this method must CFRetain it and
-    then CFRelease it when they are finished with it.
-
-    Note that to maintain optimal performance, some sample buffers directly reference pools of memory that may need to be
-    reused by the device system and other capture inputs. This is frequently the case for uncompressed device native
-    capture where memory blocks are copied as little as possible. If multiple sample buffers reference such pools of
-    memory for too long, inputs will no longer be able to copy new samples into memory and those samples will be dropped.
-    If your application is causing samples to be dropped by retaining the provided CMSampleBuffer objects for too long,
-    but it needs access to the sample data for a long period of time, consider copying the data into a new buffer and
-    then calling CFRelease on the sample buffer if it was previously retained so that the memory it references can be
-    reused. 
- 
-    Clients should not assume that this method will be called on a specific thread. In addition, this method is called
-    periodically, so it must be efficient to prevent capture performance problems.
-*/
-- (void)captureOutput:(AVCaptureFileOutput *)captureOutput didOutputSampleBuffer:(CMSampleBufferRef)sampleBuffer fromConnection:(AVCaptureConnection *)connection NS_AVAILABLE(10_7, NA);
-
-@end
-
-#endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
-
-
-@class AVCaptureMovieFileOutputInternal;
-
-/*!
- @class AVCaptureMovieFileOutput
- @abstract
-    AVCaptureMovieFileOutput is a concrete subclass of AVCaptureFileOutput that writes captured media to QuickTime movie
-    files.
-
- @discussion
-    AVCaptureMovieFileOutput implements the complete file recording interface declared by AVCaptureFileOutput for writing
-    media data to QuickTime movie files. In addition, instances of AVCaptureMovieFileOutput allow clients to configure
-    options specific to the QuickTime file format, including allowing them to write metadata collections to each file,
-    specify media encoding options for each track (Mac OS X), and specify an interval at which movie fragments should be written.
-*/
-NS_CLASS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED
-@interface AVCaptureMovieFileOutput : AVCaptureFileOutput
-{
-@private
-	AVCaptureMovieFileOutputInternal *_internal;
-}
-
-/*!
- @property movieFragmentInterval
- @abstract
-    Specifies the frequency with which movie fragments should be written.
-
- @discussion
-    When movie fragments are used, a partially written QuickTime movie file whose writing is unexpectedly interrupted can
-    be successfully opened and played up to multiples of the specified time interval. A value of kCMTimeInvalid indicates
-    that movie fragments should not be used, but that only a movie atom describing all of the media in the file should be
-    written. The default value of this property is ten seconds.
-
-    Changing the value of this property will not affect the movie fragment interval of the file currently being written,
-    if there is one.
-*/
-@property(nonatomic) CMTime movieFragmentInterval;
-
-/*!
- @property metadata
- @abstract
-    A collection of metadata to be written to the receiver's output files.
-
- @discussion
-    The value of this property is an array of AVMetadataItem objects representing the collection of top-level metadata to
-    be written in each output file.
-*/
-@property(nonatomic, copy) NSArray *metadata;
-
-#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
-
-/*!
- @method outputSettingsForConnection:
- @abstract
-    Returns the options the receiver uses to re-encode media from the given connection as it is being recorded.
-
- @param connection
-    The connection delivering the media to be re-encoded.
- @result
-    An NSDictionary of output settings.
-
- @discussion
-    See AVAudioSettings.h for audio connections or AVVideoSettings.h for video connections for more information on
-    how to construct an output settings dictionary.  If the returned value is an empty dictionary (i.e. [NSDictionary
-    dictionary], the format of the media from the connection will not be changed before being written to the file.  If
-    -setOutputSettings:forConnection: was called with a nil dictionary, this method returns a non-nil dictionary reflecting
-    the settings used by the AVCaptureSession's current sessionPreset.
-*/
-- (NSDictionary *)outputSettingsForConnection:(AVCaptureConnection *)connection NS_AVAILABLE(10_7, NA);
-
-/*!
- @method setOutputSettings:forConnection:
- @abstract
-    Sets the options the receiver uses to re-encode media from the given connection as it is being recorded.
-
- @param outputSettings
-    An NSDictionary of output settings.
- @param connection
-    The connection delivering the media to be re-encoded.
-
- @discussion
-    See AVAudioSettings.h for audio connections or AVVideoSettings.h for video connections for more information on
-    how to construct an output settings dictionary.  A value of an empty dictionary (i.e. [NSDictionary dictionary], means
-    that the format of the media from the connection should not be changed before being written to the file.  A value of
-    nil means that the output format will be determined by the session preset.  In this case, -outputSettingsForConnection:
-    will return a non-nil dictionary reflecting the settings used by the AVCaptureSession's current sessionPreset.
-*/
-- (void)setOutputSettings:(NSDictionary *)outputSettings forConnection:(AVCaptureConnection *)connection NS_AVAILABLE(10_7, NA);
-
-#endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
-
-#if TARGET_OS_IPHONE
-
-/*!
- @method recordsVideoOrientationAndMirroringChangesAsMetadataTrackForConnection:
- @abstract
-    Returns YES if the movie file output will create a timed metadata track that records samples which
-	reflect changes made to the given connection's videoOrientation and videoMirrored properties
-	during recording.
-
- @param connection
-    A connection delivering video media to the movie file output. This method throws an NSInvalidArgumentException
-	if the connection does not have a mediaType of AVMediaTypeVideo or if the connection does not terminate at
-	the movie file output.
-
- @discussion
-	See setRecordsVideoOrientationAndMirroringChanges:asMetadataTrackForConnection: for details on the behavior
-	controlled by this value.
-	
-	The default value returned is NO.
-*/
-- (BOOL)recordsVideoOrientationAndMirroringChangesAsMetadataTrackForConnection:(AVCaptureConnection *)connection NS_AVAILABLE_IOS(9_0);
-
-/*!
- @method setRecordsVideoOrientationAndMirroringChanges:asMetadataTrackForConnection:
- @abstract
-    Controls whether or not the movie file output will create a timed metadata track that records samples which
-	reflect changes made to the given connection's videoOrientation and videoMirrored properties during
-	recording.
- 
- @param doRecordChanges
-    If YES, the movie file output will create a timed metadata track that records samples which reflect changes
-	made to the given connection's videoOrientation and videoMirrored properties during recording.
-
- @param connection
-    A connection delivering video media to the movie file output. This method throws an NSInvalidArgumentException
-	if the connection does not have a mediaType of AVMediaTypeVideo or if the connection does not terminate at
-	the movie file output.
-
- @discussion
-    When a recording is started the current state of a video capture connection's videoOrientation and videoMirrored
-	properties are used to build the display matrix for the created video track. The movie file format allows only
-	one display matrix per track, which means that any changes made during a recording to the videoOrientation and
-	videoMirrored properties are not captured.  For example, a user starts a recording with their device in the portrait
-	orientation, and then partway through the recording changes the device to a landscape orientation. The landscape
-	orientation requires a different display matrix, but only the initial display matrix (the portrait display
-	matrix) is recorded for the video track.
-	
-	By invoking this method the client application directs the movie file output to create an additional track in the
-	captured movie. This track is a timed metadata track that is associated with the video track, and contains one or
-	more samples that contain a Video Orientation value (as defined by EXIF and TIFF specifications, which is enumerated
-	by CGImagePropertyOrientation in <ImageIO/CGImageProperties.h>).  The value represents the display matrix corresponding
-	to the AVCaptureConnection's videoOrientation and videoMirrored properties when applied to the input source.  The
-	initial sample written to the timed metadata track represents video track's display matrix. During recording additional
-	samples will be written to the timed metadata track whenever the client application changes the video connection's
-	videoOrienation or videoMirrored properties. Using the above example, when the client application detects the user
-	changing the device from portrait to landscape orientation, it updates the video connection's videoOrientation property,
-	thus causing the movie file output to add a new sample to the timed metadata track.
-	
-	After capture, playback and editing applications can use the timed metadata track to enhance their user's experience.
-	For example, when playing back the captured movie, a playback engine can use the samples to adjust the display of the
-	video samples to keep the video properly oriented.  Another example is an editing application that uses the sample
-	the sample times to suggest cut points for breaking the captured movie into separate clips, where each clip is properly
-	oriented.
-	
-	The default behavior is to not create the timed metadata track.
-	
-	The doRecordChanges value is only observed at the start of recording.  Changes to the value will not have any
-	effect until the next recording is started.
-*/
-- (void)setRecordsVideoOrientationAndMirroringChanges:(BOOL)doRecordChanges asMetadataTrackForConnection:(AVCaptureConnection *)connection NS_AVAILABLE_IOS(9_0);
-
-#endif // TARGET_OS_IPHONE
-
-@end
-
-
-#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
-
-@class AVCaptureAudioFileOutputInternal;
-
-/*!
- @class AVCaptureAudioFileOutput
- @abstract
-    AVCaptureAudioFileOutput is a concrete subclass of AVCaptureFileOutput that writes captured audio to any audio file
-    type supported by CoreAudio.
- 
- @discussion
-    AVCaptureAudioFileOutput implements the complete file recording interface declared by AVCaptureFileOutput for writing
-    media data to audio files. In addition, instances of AVCaptureAudioFileOutput allow clients to configure options
-    specific to the audio file formats, including allowing them to write metadata collections to each file and specify
-    audio encoding options.
-*/
-NS_CLASS_AVAILABLE(10_7, NA) __TVOS_PROHIBITED
-@interface AVCaptureAudioFileOutput : AVCaptureFileOutput
-{
-@private
-	AVCaptureAudioFileOutputInternal *_internal;
-}
-
-/*!
- @method availableOutputFileTypes
- @abstract		
-    Provides the file types AVCaptureAudioFileOutput can write.
- @result
-    An NSArray of UTIs identifying the file types the AVCaptureAudioFileOutput class can write.
-*/
-+ (NSArray *) availableOutputFileTypes;
-
-/*!
- @method startRecordingToOutputFileURL:outputFileType:recordingDelegate:
- @abstract
-    Tells the receiver to start recording to a new file of the specified format, and specifies a delegate that will be
-    notified when recording is finished.
-
- @param outputFileURL
-    An NSURL object containing the URL of the output file. This method throws an NSInvalidArgumentException if the URL is
-    not a valid file URL.
- @param fileType
-    A UTI indicating the format of the file to be written.
- @param delegate
-    An object conforming to the AVCaptureFileOutputRecordingDelegate protocol. Clients must specify a delegate so that they
-    can be notified when recording to the given URL is finished.
-
- @discussion
-    The method sets the file URL to which the receiver is currently writing output media. If a file at the given URL
-    already exists when capturing starts, recording to the new file will fail.
-
-    The fileType argument is a UTI corresponding to the audio file format that should be written. UTIs for common 
-    audio file types are declared in AVMediaFormat.h.
-
-    Clients need not call stopRecording before calling this method while another recording is in progress. If this method
-    is invoked while an existing output file was already being recorded, no media samples will be discarded between the
-    old file and the new file.
-
-    When recording is stopped either by calling stopRecording, by changing files using this method, or because of an
-    error, the remaining data that needs to be included to the file will be written in the background. Therefore, clients
-    must specify a delegate that will be notified when all data has been written to the file using the
-    captureOutput:didFinishRecordingToOutputFileAtURL:fromConnections:error: method. The recording delegate can also
-    optionally implement methods that inform it when data starts being written, when recording is paused and resumed, and
-    when recording is about to be finished.
-
-    On Mac OS X, if this method is called within the captureOutput:didOutputSampleBuffer:fromConnection: delegate method,
-    the first samples written to the new file are guaranteed to be those contained in the sample buffer passed to that
-    method.
-*/
-- (void)startRecordingToOutputFileURL:(NSURL*)outputFileURL outputFileType:(NSString *)fileType recordingDelegate:(id<AVCaptureFileOutputRecordingDelegate>)delegate;
-
-/*!
- @property metadata
- @abstract
-    A collection of metadata to be written to the receiver's output files.
-
- @discussion
-    The value of this property is an array of AVMetadataItem objects representing the collection of top-level metadata to
-    be written in each output file. Only ID3 v2.2, v2.3, or v2.4 style metadata items are supported.
-*/
-@property(nonatomic, copy) NSArray *metadata; 
-
-/*!
- @property audioSettings
- @abstract
-    Specifies the options the receiver uses to re-encode audio as it is being recorded.
-
- @discussion
-    The output settings dictionary can contain values for keys from AVAudioSettings.h. A value of nil indicates that the
-    format of the audio should not be changed before being written to the file.
-*/
-@property(nonatomic, copy) NSDictionary *audioSettings;
-
-@end
-
-#endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
-
-
-@class AVCaptureStillImageOutputInternal;
-
-/*!
- @class AVCaptureStillImageOutput
- @abstract
-    AVCaptureStillImageOutput is a concrete subclass of AVCaptureOutput that can be used to capture high-quality still
-    images with accompanying metadata.
-
- @discussion
-    Instances of AVCaptureStillImageOutput can be used to capture, on demand, high quality snapshots from a realtime
-    capture source. Clients can request a still image for the current time using the
-    captureStillImageAsynchronouslyFromConnection:completionHandler: method. Clients can also configure still image
-    outputs to produce still images in specific image formats.
-*/
-NS_CLASS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED
-@interface AVCaptureStillImageOutput : AVCaptureOutput 
-{
-@private
-	AVCaptureStillImageOutputInternal *_internal;
-}
-
-/*!
- @property outputSettings
- @abstract
-    Specifies the options the receiver uses to encode still images before they are delivered.
-
- @discussion
-    See AVVideoSettings.h for more information on how to construct an output settings dictionary.
-
-    On iOS, the only currently supported keys are AVVideoCodecKey and kCVPixelBufferPixelFormatTypeKey. 
-    Use -availableImageDataCVPixelFormatTypes and -availableImageDataCodecTypes to determine what 
-    codec keys and pixel formats are supported. AVVideoQualityKey is supported on iOS 6.0 and later
-    and may only be used when AVVideoCodecKey is set to AVVideoCodecJPEG.
-*/
-@property(nonatomic, copy) NSDictionary *outputSettings;
-
-/*!
- @property availableImageDataCVPixelFormatTypes
- @abstract
-    Indicates the supported image pixel formats that can be specified in outputSettings.
-
- @discussion
-    The value of this property is an NSArray of NSNumbers that can be used as values for the 
-    kCVPixelBufferPixelFormatTypeKey in the receiver's outputSettings property.  The first
-    format in the returned list is the most efficient output format.
-*/
-@property(nonatomic, readonly) NSArray *availableImageDataCVPixelFormatTypes;
-
-/*!
- @property availableImageDataCodecTypes
- @abstract
-    Indicates the supported image codec formats that can be specified in outputSettings.
-
- @discussion
-    The value of this property is an NSArray of NSStrings that can be used as values for the 
-    AVVideoCodecKey in the receiver's outputSettings property.
-*/
-@property(nonatomic, readonly) NSArray *availableImageDataCodecTypes;
-
-#if TARGET_OS_IPHONE
-
-/*!
- @property stillImageStabilizationSupported
- @abstract
-    Indicates whether the receiver supports still image stabilization.
- 
- @discussion
-    The receiver's automaticallyEnablesStillImageStabilizationWhenAvailable property can only be set 
-    if this property returns YES.  Its value may change as the session's -sessionPreset or input device's
-    -activeFormat changes.
-*/
-@property(nonatomic, readonly, getter=isStillImageStabilizationSupported) BOOL stillImageStabilizationSupported NS_AVAILABLE_IOS(7_0);
-
-/*!
- @property automaticallyEnablesStillImageStabilizationWhenAvailable
- @abstract
-    Indicates whether the receiver should automatically use still image stabilization when necessary.
- 
- @discussion
-    On a receiver where -isStillImageStabilizationSupported returns YES, image stabilization
-    may be applied to reduce blur commonly found in low light photos. When stabilization is enabled, still 
-    image captures incur additional latency. The default value is YES when supported, NO otherwise. Setting 
-    this property throws an NSInvalidArgumentException if -isStillImageStabilizationSupported returns NO.
-*/
-@property(nonatomic) BOOL automaticallyEnablesStillImageStabilizationWhenAvailable NS_AVAILABLE_IOS(7_0);
-
-/*!
- @property stillImageStabilizationActive
- @abstract
-    Indicates whether still image stabilization is in use for the current capture.
- 
- @discussion
-    On a receiver where -isStillImageStabilizationSupported returns YES, and
-    automaticallyEnablesStillImageStabilizationWhenAvailable is set to YES, this property may be key-value
-    observed, or queried from inside your key-value observation callback for the @"capturingStillImage"
-	property, to find out if still image stabilization is being applied to the current capture.
-*/
-@property(nonatomic, readonly, getter=isStillImageStabilizationActive) BOOL stillImageStabilizationActive NS_AVAILABLE_IOS(7_0);
-
-/*!
- @property highResolutionStillImageOutputEnabled
- @abstract
-    Indicates whether the receiver should emit still images at the highest resolution supported
-    by its source AVCaptureDevice's activeFormat.
- 
- @discussion
-    By default, AVCaptureStillImageOutput emits images with the same dimensions as its source AVCaptureDevice's
-    activeFormat.formatDescription.  However, if you set this property to YES, the receiver emits still images at its source
-    AVCaptureDevice's activeFormat.highResolutionStillImageDimensions.  Note that if you enable video stabilization
-    (see AVCaptureConnection's preferredVideoStabilizationMode) for any output, the high resolution still images 
-    emitted by AVCaptureStillImageOutput may be smaller by 10 or more percent.
-*/
-@property(nonatomic, getter=isHighResolutionStillImageOutputEnabled) BOOL highResolutionStillImageOutputEnabled NS_AVAILABLE_IOS(8_0);
-
-#endif // TARGET_OS_IPHONE
-
-/*!
- @property capturingStillImage
- @abstract
-    A boolean value that becomes true when a still image is being captured.
-
- @discussion
-    The value of this property is a BOOL that becomes true when a still image is being
-    captured, and false when no still image capture is underway.  This property is
-    key-value observable.
-*/
-@property(readonly, getter=isCapturingStillImage) BOOL capturingStillImage NS_AVAILABLE(10_8, 5_0);
-
-/*!
- @method captureStillImageAsynchronouslyFromConnection:completionHandler:
- @abstract
-    Initiates an asynchronous still image capture, returning the result to a completion handler.
-
- @param connection
-    The AVCaptureConnection object from which to capture the still image.
- @param handler
-    A block that will be called when the still image capture is complete. The block will be passed a CMSampleBuffer
-    object containing the image data or an NSError object if an image could not be captured.
-
- @discussion
-    This method will return immediately after it is invoked, later calling the provided completion handler block when
-    image data is ready. If the request could not be completed, the error parameter will contain an NSError object
-    describing the failure.
-
-    Attachments to the image data sample buffer may contain metadata appropriate to the image data format. For instance,
-    a sample buffer containing JPEG data may carry a kCGImagePropertyExifDictionary as an attachment. See
-    <ImageIO/CGImageProperties.h> for a list of keys and value types.
-
-    Clients should not assume that the completion handler will be called on a specific thread.
- 
-    Calls to captureStillImageAsynchronouslyFromConnection:completionHandler: are not synchronized with AVCaptureDevice
-    manual control completion handlers. Setting a device manual control, waiting for its completion, then calling
-    captureStillImageAsynchronouslyFromConnection:completionHandler: DOES NOT ensure that the still image returned reflects
-    your manual control change. It may be from an earlier time. You can compare your manual control completion handler sync time
-    to the returned still image's presentation time. You can retrieve the sample buffer's pts using 
-    CMSampleBufferGetPresentationTimestamp(). If the still image has an earlier timestamp, your manual control command 
-    does not apply to it.
-*/
-- (void)captureStillImageAsynchronouslyFromConnection:(AVCaptureConnection *)connection completionHandler:(void (^)(CMSampleBufferRef imageDataSampleBuffer, NSError *error))handler;
-
-/*!
- @method jpegStillImageNSDataRepresentation:
- @abstract
-    Converts the still image data and metadata attachments in a JPEG sample buffer to an NSData representation.
-
- @param jpegSampleBuffer
-    The sample buffer carrying JPEG image data, optionally with Exif metadata sample buffer attachments.
-    This method throws an NSInvalidArgumentException if jpegSampleBuffer is NULL or not in the JPEG format.
-
- @discussion
-    This method returns an NSData representation of a JPEG still image sample buffer, merging the image data and
-    Exif metadata sample buffer attachments without recompressing the image.
-    The returned NSData is suitable for writing to disk.
-*/
-+ (NSData *)jpegStillImageNSDataRepresentation:(CMSampleBufferRef)jpegSampleBuffer;
-
-@end
-
-#if TARGET_OS_IPHONE
-
-/*!
- @class AVCaptureBracketedStillImageSettings
- @abstract
-    AVCaptureBracketedStillImageSettings is an abstract base class that defines an interface for settings
-	pertaining to a bracketed capture.
- 
- @discussion
-    AVCaptureBracketedStillImageSettings may not be instantiated directly.
-*/
-NS_CLASS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED
-@interface AVCaptureBracketedStillImageSettings : NSObject
-@end
-
-/*!
- @class AVCaptureManualExposureBracketedStillImageSettings
- @abstract
-    AVCaptureManualExposureBracketedStillImageSettings is a concrete subclass of AVCaptureBracketedStillImageSettings
-    to be used when bracketing exposure duration and ISO.
- 
- @discussion
-    An AVCaptureManualExposureBracketedStillImageSettings instance defines the exposure duration and ISO
-    settings that should be applied to one image in a bracket. An array of settings objects is passed to
-    -[AVCaptureStillImageOutput captureStillImageBracketAsynchronouslyFromConnection:withSettingsArray:completionHandler:].
-    Min and max duration and ISO values are queryable properties of the AVCaptureDevice supplying data to
-    an AVCaptureStillImageOutput instance. If you wish to leave exposureDuration unchanged for this bracketed
-    still image, you may pass the special value AVCaptureExposureDurationCurrent. To keep ISO unchanged, you may
-    pass AVCaptureISOCurrent (see AVCaptureDevice.h).
-*/
-NS_CLASS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED
-@interface AVCaptureManualExposureBracketedStillImageSettings : AVCaptureBracketedStillImageSettings
-
-+ (instancetype)manualExposureSettingsWithExposureDuration:(CMTime)duration ISO:(float)ISO;
-
-@property(readonly) CMTime exposureDuration;
-@property(readonly) float ISO;
-
-@end
-
-/*!
- @class AVCaptureAutoExposureBracketedStillImageSettings
- @abstract
-    AVCaptureAutoExposureBracketedStillImageSettings is a concrete subclass of AVCaptureBracketedStillImageSettings
-    to be used when bracketing exposure target bias.
- 
- @discussion
-    An AVCaptureAutoExposureBracketedStillImageSettings instance defines the exposure target bias
-    setting that should be applied to one image in a bracket. An array of settings objects is passed to
-    -[AVCaptureStillImageOutput captureStillImageBracketAsynchronouslyFromConnection:withSettingsArray:completionHandler:].
-    Min and max exposure target bias are queryable properties of the AVCaptureDevice supplying data to
-    an AVCaptureStillImageOutput instance. If you wish to leave exposureTargetBias unchanged for this bracketed
-    still image, you may pass the special value AVCaptureExposureTargetBiasCurrent (see AVCaptureDevice.h).
-*/
-NS_CLASS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED
-@interface AVCaptureAutoExposureBracketedStillImageSettings : AVCaptureBracketedStillImageSettings
-
-+ (instancetype)autoExposureSettingsWithExposureTargetBias:(float)exposureTargetBias;
-
-@property(readonly) float exposureTargetBias;
-
-@end
-
-/*!
- @category AVCaptureStillImageOutput (BracketedCaptureMethods)
- @abstract
-    A category of methods for bracketed still image capture.
- 
- @discussion
-    A "still image bracket" is a batch of images taken as quickly as possible in succession,
-    optionally with different settings from picture to picture.
- 
-    In a bracketed capture, AVCaptureDevice flashMode property is ignored (flash is forced off), as is AVCaptureStillImageOutput's
-    automaticallyEnablesStillImageStabilizationWhenAvailable property (stabilization is forced off).
-*/
-@interface AVCaptureStillImageOutput ( BracketedCaptureMethods )
-
-/*!
- @property maxBracketedCaptureStillImageCount
- @abstract
-    Specifies the maximum number of still images that may be taken in a single bracket.
-
- @discussion
-    AVCaptureStillImageOutput can only satisfy a limited number of image requests in a single bracket without exhausting system
-    resources. The maximum number of still images that may be taken in a single bracket depends on the size of the images being captured,
-    and consequently may vary with AVCaptureSession -sessionPreset and AVCaptureDevice -activeFormat.  Some formats do not support
-    bracketed capture and return a maxBracketedCaptureStillImageCount of 0.  This read-only property is key-value observable.
-    If you exceed -maxBracketedCaptureStillImageCount, then -captureStillImageBracketAsynchronouslyFromConnection:withSettingsArray:completionHandler:
-    fails and the completionHandler is called [settings count] times with a NULL sample buffer and AVErrorMaximumStillImageCaptureRequestsExceeded.
-*/
-@property(nonatomic, readonly) NSUInteger maxBracketedCaptureStillImageCount NS_AVAILABLE_IOS(8_0);
-
-/*!
- @property lensStabilizationDuringBracketedCaptureSupported
- @abstract
-    Indicates whether the receiver supports lens stabilization during bracketed captures.
- 
- @discussion
-    The receiver's lensStabilizationDuringBracketedCaptureEnabled property can only be set 
-    if this property returns YES.  Its value may change as the session's -sessionPreset or input device's
-    -activeFormat changes.  This read-only property is key-value observable.
-*/
-@property(nonatomic, readonly, getter=isLensStabilizationDuringBracketedCaptureSupported) BOOL lensStabilizationDuringBracketedCaptureSupported NS_AVAILABLE_IOS(9_0);
-
-/*!
- @property lensStabilizationDuringBracketedCaptureEnabled
- @abstract
-    Indicates whether the receiver should use lens stabilization during bracketed captures.
- 
- @discussion
-    On a receiver where -isLensStabilizationDuringBracketedCaptureSupported returns YES, lens stabilization
-    may be applied to the bracket to reduce blur commonly found in low light photos.  When lens stabilization is 
-    enabled, bracketed still image captures incur additional latency.  Lens stabilization is more effective with longer-exposure
-    captures, and offers limited or no benefit for exposure durations shorter than 1/30 of a second.  It is possible 
-    that during the bracket, the lens stabilization module may run out of correction range and therefore will not be active for 
-    every frame in the bracket.  Each emitted CMSampleBuffer from the bracket will have an attachment of kCMSampleBufferAttachmentKey_StillImageLensStabilizationInfo
-    indicating additional information about stabilization was applied to the buffer, if any.  The default value of 
-    -isLensStabilizationDuringBracketedCaptureEnabled is NO.  This value will be set to NO when -isLensStabilizationDuringBracketedCaptureSupported
-    changes to NO.  Setting this property throws an NSInvalidArgumentException if -isLensStabilizationDuringBracketedCaptureSupported returns NO.
-    This property is key-value observable.
-*/
-@property(nonatomic, getter=isLensStabilizationDuringBracketedCaptureEnabled) BOOL lensStabilizationDuringBracketedCaptureEnabled NS_AVAILABLE_IOS(9_0);
-
-/*!
- @method prepareToCaptureStillImageBracketFromConnection:withSettingsArray:completionHandler:
- @abstract
-    Allows the receiver to prepare resources in advance of capturing a still image bracket.
- 
- @param connection
-    The connection through which the still image bracket should be captured.
- 
- @param settings
-    An array of AVCaptureBracketedStillImageSettings objects. All must be of the same kind of AVCaptureBracketedStillImageSettings
-    subclass, or an NSInvalidArgumentException is thrown.
- 
- @param completionHandler
-    A user provided block that will be called asynchronously once resources have successfully been allocated
-    for the specified bracketed capture operation. If sufficient resources could not be allocated, the
-    "prepared" parameter contains NO, and "error" parameter contains a non-nil error value. If [settings count]
-    exceeds -maxBracketedCaptureStillImageCount, then AVErrorMaximumStillImageCaptureRequestsExceeded is returned.
-    You should not assume that the completion handler will be called on a specific thread.
- 
- @discussion
-    -maxBracketedCaptureStillImageCount tells you the maximum number of images that may be taken in a single
-    bracket given the current AVCaptureDevice/AVCaptureSession/AVCaptureStillImageOutput configuration. But before
-    taking a still image bracket, additional resources may need to be allocated. By calling
-    -prepareToCaptureStillImageBracketFromConnection:withSettingsArray:completionHandler: first, you are able to 
-    deterministically know when the receiver is ready to capture the bracket with the specified settings array.
-
-*/
-- (void)prepareToCaptureStillImageBracketFromConnection:(AVCaptureConnection *)connection withSettingsArray:(NSArray *)settings completionHandler:(void (^)(BOOL prepared, NSError *error))handler NS_AVAILABLE_IOS(8_0);
-
-/*!
- @method captureStillImageBracketAsynchronouslyFromConnection:withSettingsArray:completionHandler:
- @abstract
-    Captures a still image bracket.
- 
- @param connection
-    The connection through which the still image bracket should be captured.
- 
- @param settings
-    An array of AVCaptureBracketedStillImageSettings objects. All must be of the same kind of AVCaptureBracketedStillImageSettings
-    subclass, or an NSInvalidArgumentException is thrown.
- 
- @param completionHandler
-    A user provided block that will be called asynchronously as each still image in the bracket is captured.
-    If the capture request is successful, the "sampleBuffer" parameter contains a valid CMSampleBuffer, the
-    "stillImageSettings" parameter contains the settings object corresponding to this still image, and a nil
-    "error" parameter. If the bracketed capture fails, sample buffer is NULL and error is non-nil.
-    If [settings count] exceeds -maxBracketedCaptureStillImageCount, then AVErrorMaximumStillImageCaptureRequestsExceeded 
-    is returned. You should not assume that the completion handler will be called on a specific thread.
- 
- @discussion
-    If you have not called -prepareToCaptureStillImageBracketFromConnection:withSettingsArray:completionHandler: for this 
-    still image bracket request, the bracket may not be taken immediately, as the receiver may internally need to 
-    prepare resources.
-*/
-- (void)captureStillImageBracketAsynchronouslyFromConnection:(AVCaptureConnection *)connection withSettingsArray:(NSArray *)settings completionHandler:(void (^)(CMSampleBufferRef sampleBuffer, AVCaptureBracketedStillImageSettings *stillImageSettings, NSError *error))handler NS_AVAILABLE_IOS(8_0);
-
-@end
-
-#endif // TARGET_OS_IPHONE
-
-
-#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
-
-@class AVCaptureAudioPreviewOutputInternal;
-
-/*!
- @class AVCaptureAudioPreviewOutput
- @abstract
-    AVCaptureAudioPreviewOutput is a concrete subclass of AVCaptureOutput that can be used to preview the audio being
-    captured.
- 
- @discussion
-    Instances of AVCaptureAudioPreviewOutput have an associated Core Audio output device that can be used to play audio
-    being captured by the capture session. The unique ID of a Core Audio device can be obtained from its
-    kAudioDevicePropertyDeviceUID property.
-*/
-NS_CLASS_AVAILABLE(10_7, NA) __TVOS_PROHIBITED
-@interface AVCaptureAudioPreviewOutput : AVCaptureOutput 
-{
-@private
-	AVCaptureAudioPreviewOutputInternal *_internal;
-}
-
-/*!
- @property outputDeviceUniqueID
- @abstract
-    Specifies the unique ID of the Core Audio output device being used to play preview audio.
-
- @discussion
-    The value of this property is an NSString containing the unique ID of the Core Audio device to be used for output, or
-    nil if the default system output should be used
-*/
-@property(nonatomic, copy) NSString *outputDeviceUniqueID;
-
-/*!
- @property volume
- @abstract
-    Specifies the preview volume of the output.
-
- @discussion
-    The value of this property is the preview volume of the receiver, where 1.0 is the maximum volume and 0.0 is muted. 
-*/
-@property(nonatomic) float volume;
-
-@end
-
-#endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
-
-
-@class AVCaptureMetadataOutputInternal;
-@protocol AVCaptureMetadataOutputObjectsDelegate;
-
-/*!
- @class AVCaptureMetadataOutput
- @abstract
-    AVCaptureMetadataOutput is a concrete subclass of AVCaptureOutput that can be used to process metadata objects
-    from an attached connection.
-
- @discussion
-    Instances of AVCaptureMetadataOutput emit arrays of AVMetadataObject instances (see AVMetadataObject.h), such 
-    as detected faces. Applications can access the metadata objects with the captureOutput:didOutputMetadataObjects:fromConnection: 
-    delegate method.
-*/
-NS_CLASS_AVAILABLE(NA, 6_0) __TVOS_PROHIBITED
-@interface AVCaptureMetadataOutput : AVCaptureOutput 
-{
-@private
-	AVCaptureMetadataOutputInternal *_internal;
-}
-
-/*!
- @method setMetadataObjectsDelegate:queue:
- @abstract
-    Sets the receiver's delegate that will accept metadata objects and dispatch queue on which the delegate will be
-    called.
-
- @param objectsDelegate
-    An object conforming to the AVCaptureMetadataOutputObjectsDelegate protocol that will receive metadata objects
-    after they are captured.
- @param objectsCallbackQueue
-    A dispatch queue on which all delegate methods will be called.
-
- @discussion
-    When new metadata objects are captured in the receiver's connection, they will be vended to the delegate using the
-    captureOutput:didOutputMetadataObjects:fromConnection: delegate method. All delegate methods will be called on the
-    specified dispatch queue.
-
-    Clients that need to minimize the chances of metadata being dropped should specify a queue on which a sufficiently
-    small amount of processing is performed along with receiving metadata objects.
-
-    A serial dispatch queue must be used to guarantee that metadata objects will be delivered in order.
-    The objectsCallbackQueue parameter may not be NULL, except when setting the objectsDelegate
-    to nil.
-*/
-- (void)setMetadataObjectsDelegate:(id<AVCaptureMetadataOutputObjectsDelegate>)objectsDelegate queue:(dispatch_queue_t)objectsCallbackQueue;
-
-/*!
- @property metadataObjectsDelegate
- @abstract
-    The receiver's delegate.
- 
- @discussion
-    The value of this property is an object conforming to the AVCaptureMetadataOutputObjectsDelegate protocol that
-    will receive metadata objects after they are captured. The delegate is set using the setMetadataObjectsDelegate:queue:
-    method.
-*/
-@property(nonatomic, readonly) id<AVCaptureMetadataOutputObjectsDelegate> metadataObjectsDelegate;
-
-/*!
- @property metadataObjectsCallbackQueue
- @abstract
-    The dispatch queue on which all metadata object delegate methods will be called.
-
- @discussion
-    The value of this property is a dispatch_queue_t. The queue is set using the setMetadataObjectsDelegate:queue: method.
-*/
-@property(nonatomic, readonly) dispatch_queue_t metadataObjectsCallbackQueue;
-
-/*!
- @property availableMetadataObjectTypes
- @abstract
-    Indicates the receiver's supported metadata object types.
- 
- @discussion
-    The value of this property is an NSArray of NSStrings corresponding to AVMetadataObjectType strings defined
-    in AVMetadataObject.h -- one for each metadata object type supported by the receiver.  Available 
-    metadata object types are dependent on the capabilities of the AVCaptureInputPort to which this receiver's 
-    AVCaptureConnection is connected.  Clients may specify the types of objects they would like to process
-    by calling setMetadataObjectTypes:.  This property is key-value observable.
-*/
-@property(nonatomic, readonly) NSArray *availableMetadataObjectTypes;
-
-/*!
- @property metadataObjectTypes
- @abstract
-    Specifies the types of metadata objects that the receiver should present to the client.
-
- @discussion
-	AVCaptureMetadataOutput may detect and emit multiple metadata object types.  For apps linked before iOS 7.0, the 
-	receiver defaults to capturing face metadata objects if supported (see -availableMetadataObjectTypes).  For apps 
-	linked on or after iOS 7.0, the receiver captures no metadata objects by default.  -setMetadataObjectTypes: throws 
-	an NSInvalidArgumentException if any elements in the array are not present in the -availableMetadataObjectTypes array.
-*/
-@property(nonatomic, copy) NSArray *metadataObjectTypes;
-
-/*!
- @property rectOfInterest
- @abstract
-	Specifies a rectangle of interest for limiting the search area for visual metadata.
- 
- @discussion
-	The value of this property is a CGRect that determines the receiver's rectangle of interest for each frame of video.  
-	The rectangle's origin is top left and is relative to the coordinate space of the device providing the metadata.  Specifying 
-	a rectOfInterest may improve detection performance for certain types of metadata. The default value of this property is the 
-	value CGRectMake(0, 0, 1, 1).  Metadata objects whose bounds do not intersect with the rectOfInterest will not be returned.
- */
-@property(nonatomic) CGRect rectOfInterest NS_AVAILABLE_IOS(7_0);
-
-@end
-
-/*!
- @protocol AVCaptureMetadataOutputObjectsDelegate
- @abstract
-    Defines an interface for delegates of AVCaptureMetadataOutput to receive emitted objects.
-*/
-__TVOS_PROHIBITED
-@protocol AVCaptureMetadataOutputObjectsDelegate <NSObject>
-
-@optional
-
-/*!
- @method captureOutput:didOutputMetadataObjects:fromConnection:
- @abstract
-    Called whenever an AVCaptureMetadataOutput instance emits new objects through a connection.
-
- @param captureOutput
-    The AVCaptureMetadataOutput instance that emitted the objects.
- @param metadataObjects
-    An array of AVMetadataObject subclasses (see AVMetadataObject.h).
- @param connection
-    The AVCaptureConnection through which the objects were emitted.
-
- @discussion
-    Delegates receive this message whenever the output captures and emits new objects, as specified by
-    its metadataObjectTypes property. Delegates can use the provided objects in conjunction with other APIs
-    for further processing. This method will be called on the dispatch queue specified by the output's
-    metadataObjectsCallbackQueue property. This method may be called frequently, so it must be efficient to 
-    prevent capture performance problems, including dropped metadata objects.
-
-    Clients that need to reference metadata objects outside of the scope of this method must retain them and
-    then release them when they are finished with them.
-*/
-- (void)captureOutput:(AVCaptureOutput *)captureOutput didOutputMetadataObjects:(NSArray *)metadataObjects fromConnection:(AVCaptureConnection *)connection;
-
-@end
+#import <AVFoundation/AVCaptureAudioDataOutput.h>
+#import <AVFoundation/AVCaptureAudioPreviewOutput.h>
+#import <AVFoundation/AVCaptureFileOutput.h>
+#import <AVFoundation/AVCaptureMetadataOutput.h>
+#import <AVFoundation/AVCapturePhotoOutput.h>
+#import <AVFoundation/AVCaptureStillImageOutput.h>
+#import <AVFoundation/AVCaptureVideoDataOutput.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCapturePhotoOutput.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCapturePhotoOutput.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCapturePhotoOutput.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCapturePhotoOutput.h	2016-05-25 04:40:24.000000000 +0200
@@ -0,0 +1,802 @@
+/*
+    File:  AVCapturePhotoOutput.h
+ 	
+ 	Framework:  AVFoundation
+ 
+	Copyright 2016 Apple Inc. All rights reserved.
+*/
+
+#import <AVFoundation/AVCaptureOutput.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class AVCapturePhotoSettings;
+@class AVCapturePhotoBracketSettings;
+@class AVCaptureResolvedPhotoSettings;
+@class AVCaptureBracketedStillImageSettings;
+@class AVMetadataItem;
+@class AVCapturePhotoOutputInternal;
+
+@protocol AVCapturePhotoCaptureDelegate;
+
+/*!
+ @class AVCapturePhotoOutput
+ @abstract
+    AVCapturePhotoOutput is a concrete subclass of AVCaptureOutput that supersedes AVCaptureStillImageOutput as the preferred interface for capturing photos. In addition to capturing all flavors of still image supported by AVCaptureStillImageOutput, it supports Live Photo capture, preview-sized image delivery, wide color, RAW, RAW+JPG and RAW+DNG formats.
+ 
+ @discussion
+    Taking a photo is multi-step process. Clients wishing to build a responsive UI need to know about the progress of a photo capture request as it advances from capture to processing to finished delivery. AVCapturePhotoOutput informs clients of photo capture progress through a delegate protocol. To take a picture, a client instantiates and configures an AVCapturePhotoSettings object, then calls AVCapturePhotoOutput's -capturePhotoWithSettings:delegate:, passing a delegate to be informed when events relating to the photo capture occur (e.g. the photo is about to be captured, the photo has been captured but not processed yet, the Live Photo movie is ready, etc.).
+ 
+    Some AVCapturePhotoSettings properties are "Auto", such as autoStillImageStabilizationEnabled. When set to YES, the photo output decides at capture time whether the current scene and lighting conditions require still image stabilization. Thus the client doesn't know with certainty which features are enabled when making the capture request. With the first and each subsequent delegate callback, the client is provided an AVCaptureResolvedPhotoSettings instance that indicates the settings that were applied to the capture. All "Auto" features have now been resolved to on or off. The AVCaptureResolvedPhotoSettings object passed in the client's delegate callbacks has a uniqueID identical to the AVCapturePhotoSettings request. This uniqueID allows clients to pair unresolved and resolved settings objects. See AVCapturePhotoCaptureDelegate below for a detailed discussion of the delegate callbacks.
+ 
+    Enabling certain photo features (Live Photo capture and high resolution capture) requires a reconfiguration of the capture render pipeline. Clients wishing to opt in for these features should call -setLivePhotoCaptureEnabled: and/or -setHighResolutionCaptureEnabled: before calling -startRunning on the AVCaptureSession. Changing any of these properties while the session is running requires a disruptive reconfiguration of the capture render pipeline. Live Photo captures in progress will be ended immediately; unfulfilled photo requests will be aborted; video preview will temporarily freeze. If you wish to capture Live Photos containing sound, you must add an audio AVCaptureDeviceInput to your AVCaptureSession.
+
+    Simultaneous Live Photo capture and MovieFileOutput capture is not supported. If an AVCaptureMovieFileOutput is added to your session, AVCapturePhotoOutput's livePhotoCaptureSupported property returns NO. Note that simultaneous Live Photo capture and AVCaptureVideoDataOutput is supported.
+ 
+    AVCaptureStillImageOutput and AVCapturePhotoOutput may not both be added to a capture session. You must use one or the other. If you add both to a session, a NSInvalidArgumentException is thrown.
+ 
+    AVCapturePhotoOutput implicitly supports wide color photo capture, following the activeColorSpace of the source AVCaptureDevice. If the source device's activeColorSpace is AVCaptureColorSpace_P3_D65, photos are encoded with wide color information, unless you've specified an output format of '420v', which does not support wide color.
+ */
+NS_CLASS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED
+@interface AVCapturePhotoOutput : AVCaptureOutput
+{
+@private
+	AVCapturePhotoOutputInternal *_internal;
+}
+
+/*!
+ @method capturePhotoWithSettings:delegate:
+ @abstract
+    Method for initiating a photo capture request with progress monitoring through the supplied delegate.
+ 
+ @param settings
+    An AVCapturePhotoSettings object you have configured. May not be nil.
+ @param delegate
+    An object conforming to the AVCapturePhotoCaptureDelegate protocol. This object's delegate methods are called back as the photo advances from capture to processing to finished delivery. May not be nil.
+ 
+ @discussion
+    This method initiates a photo capture. The receiver copies your provided settings to prevent unintentional mutation. It is illegal to re-use settings. The receiver throws a NSInvalidArgumentException if your settings.uniqueID matches that of any previously used settings. This method is used to initiate all flavors of photo capture: single photo, RAW capture with or without a processed image (such as a JPEG), bracketed capture, and Live Photo.
+ 
+    Clients need not wait for a capture photo request to complete before issuing another request. This is true for single photo captures as well as Live Photos, where movie complements of adjacent photo captures are allowed to overlap.
+ 
+    This method validates your settings and enforces the following rules in order to ensure deterministic behavior. If any of these rules are violated, a NSInvalidArgumentException is thrown.
+    RAW rules:
+        - If rawPhotoPixelFormatType is non-zero, it must be present in the receiver's -availableRawPhotoPixelFormatTypes array.
+        - If rawPhotoPixelFormatType is non-zero, autoStillImageStabilizationEnabled must be set to NO.
+        - If rawPhotoPixelFormatType is non-zero, your delegate must respond to -captureOutput:didFinishProcessingRawPhotoSampleBuffer:previewPhotoSampleBuffer:resolvedSettings:bracketSettings:error:.
+        - If rawPhotoPixelFormatType is non-zero, highResolutionPhotoEnabled may be YES or NO, but the setting only applies to the processed image, if you've specified one.
+        - If rawPhotoPixelFormatType is non-zero, the videoZoomFactor of the source device and the videoScaleAndCropFactor of the photo output's video connection must both be 1.0. Ensure no zoom is applied before requesting a RAW capture, and don't change the zoom during RAW capture.
+    Format rules:
+        - If format is non-nil, a kCVPixelBufferPixelFormatTypeKey or AVVideoCodecKey must be present, and both may not be present.
+        - If format has a kCVPixelBufferPixelFormatTypeKey, its value must be present in the receiver's -availablePhotoPixelFormatTypes array.
+        - If format has a AVVideoCodecKey, its value must be present in the receiver's -availablePhotoCodecTypes array.
+        - If format is non-nil, your delegate must respond to -captureOutput:didFinishProcessingPhotoSampleBuffer:previewPhotoSampleBuffer:resolvedSettings:bracketSettings:error:.
+    Flash rules:
+        - The specified flashMode must be present in the receiver's -supportedFlashModes array.
+    Live Photo rules:
+        - The receiver's livePhotoCaptureEnabled must be YES if settings.livePhotoMovieURL is non-nil.
+        - If settings.livePhotoMovieURL is non-nil, the receiver's livePhotoCaptureSuspended property must be set to NO.
+        - If settings.livePhotoMovieURL is non-nil, it must be a file URL that's accessible to your app's sandbox.
+        - If settings.livePhotoMovieURL is non-nil, your delegate must respond to -captureOutput:didFinishProcessingLivePhotoToMovieFileAtURL:duration:photoDisplayTime:resolvedSettings:error:.
+    Bracketed capture rules:
+        - bracketedSettings.count must be <= the receiver's maxBracketedCapturePhotoCount property.
+        - For manual exposure brackets, ISO value must be within the source device activeFormat's minISO and maxISO values.
+        - For manual exposure brackets, exposureDuration value must be within the source device activeFormat's minExposureDuration and maxExposureDuration values.
+        - For auto exposure brackets, exposureTargetBias value must be within the source device's minExposureTargetBias and maxExposureTargetBias values.
+ */
+- (void)capturePhotoWithSettings:(AVCapturePhotoSettings *)settings delegate:(id<AVCapturePhotoCaptureDelegate>)delegate;
+
+/*!
+ @property availablePhotoPixelFormatTypes
+ @abstract
+    An array of kCVPixelBufferPixelFormatTypeKey values that are currently supported by the receiver.
+
+ @discussion
+    If you wish to capture a photo in an uncompressed format, such as 420f, 420v, or BGRA, you must ensure that the format you want is present in the receiver's availablePhotoPixelFormatTypes array. If you've not yet added your receiver to an AVCaptureSession with a video source, no pixel format types are available. This property is key-value observable.
+ */
+@property(nonatomic, readonly) NSArray<NSNumber *> *availablePhotoPixelFormatTypes;
+
+/*!
+ @property availablePhotoCodecTypes
+ @abstract
+    An array of AVVideoCodecKey values that are currently supported by the receiver.
+
+ @discussion
+    If you wish to capture a photo in a compressed format, such as JPEG, you must ensure that the format you want is present in the receiver's availablePhotoCodecTypes array. If you've not yet added your receiver to an AVCaptureSession with a video source, no codec types are available. This property is key-value observable.
+ */
+@property(nonatomic, readonly) NSArray<NSString *> *availablePhotoCodecTypes;
+
+/*!
+ @property availableRawPhotoPixelFormatTypes
+ @abstract
+    An array of Bayer RAW CVPixelBufferPixelFormatTypeKey values that are currently supported by the receiver.
+
+ @discussion
+    If you wish to capture a RAW photo, you must ensure that the Bayer RAW format you want is present in the receiver's availableRawPhotoPixelFormatTypes array. If you've not yet added your receiver to an AVCaptureSession with a video source, no RAW formats are available. This property is key-value observable. RAW capture is not supported on all platforms.
+ */
+@property(nonatomic, readonly) NSArray<NSNumber *> *availableRawPhotoPixelFormatTypes;
+
+/*!
+ @property stillImageStabilizationSupported
+ @abstract
+    Indicates whether the still image stabilization feature is supported by the receiver.
+
+ @discussion
+    This property may change as the session's -sessionPreset or source device's -activeFormat change. When still image stabilization is not supported, your capture requests always resolve stillImageStabilizationEnabled to NO. This property is key-value observable.
+ */
+@property(nonatomic, readonly, getter=isStillImageStabilizationSupported) BOOL stillImageStabilizationSupported;
+
+/*!
+ @property isStillImageStabilizationScene
+ @abstract
+    Indicates whether the current scene is dark enough to warrant use of still image stabilization.
+
+ @discussion
+    This property reports whether the current scene being previewed by the camera is dark enough to benefit from still image stabilization. You can influence this property's answers by setting the photoSettingsForSceneMonitoring property, indicating whether autoStillImageStabilization monitoring should be on or off. If you set autoStillImageStabilization to NO, isStillImageStabilizationScene always reports NO. If you set it to YES, this property returns YES or NO depending on the current scene's lighting conditions. Note that some very dark scenes do not benefit from still image stabilization, but do benefit from flash. This property may be key-value observed.
+ */
+@property(nonatomic, readonly) BOOL isStillImageStabilizationScene;
+
+/*!
+ @property supportedFlashModes
+ @abstract
+    An array of AVCaptureFlashMode constants for the current capture session configuration.
+
+ @discussion
+    This property supersedes AVCaptureDevice's isFlashModeSupported: It returns an array of AVCaptureFlashMode constants. To test whether a particular flash mode is supported, use NSArray's containsObject API: [photoOutput.supportedFlashModes containsObject:@(AVCaptureFlashModeAuto)]. This property is key-value observable.
+ */
+@property(nonatomic, readonly) NSArray<NSNumber *> *supportedFlashModes;
+
+/*!
+ @property isFlashScene
+ @abstract
+    Indicates whether the current scene is dark enough to warrant use of the flash.
+
+ @discussion
+    This property reports whether the current scene being previewed by the camera is dark enough to need the flash. If -supportedFlashModes only contains AVCaptureFlashModeOff, isFlashScene always reports NO. You can influence this property's answers by setting the photoSettingsForSceneMonitoring property, indicating the flashMode you wish to monitor. If you set flashMode to AVCaptureFlashModeOff, isFlashScene always reports NO. If you set it to AVCaptureFlashModeAuto or AVCaptureFlashModeOn, isFlashScene answers YES or NO based on the current scene's lighting conditions. By default, isFlashScene assumes your desired flashMode is AVCaptureFlashModeAuto. Note that there is some overlap in the light level ranges that benefit from still image stabilization and flash. If your photoSettingsForSceneMonitoring indicate that both still image stabilization and flash scenes should be monitored, still image stabilization takes precedence, and isFlashScene becomes YES at lower overall light levels. This property may be key-value observed.
+ */
+@property(nonatomic, readonly) BOOL isFlashScene;
+
+/*!
+ @property photoSettingsForSceneMonitoring
+ @abstract
+    Settings that govern the behavior of isFlashScene and isStillImageStabilizationScene.
+
+ @discussion
+    You can influence the return values of isFlashScene and isStillImageStabilizationScene by setting this property, indicating the flashMode and autoStillImageStabilizationEnabled values that should be considered for scene monitoring. For instance, if you set flashMode to AVCaptureFlashModeOff, isFlashScene always reports NO. If you set it to AVCaptureFlashModeAuto or AVCaptureFlashModeOn, isFlashScene answers YES or NO based on the current scene's lighting conditions. Note that there is some overlap in the light level ranges that benefit from still image stabilization and flash. If your photoSettingsForSceneMonitoring indicate that both still image stabilization and flash scenes should be monitored, still image stabilization takes precedence, and isFlashScene becomes YES at lower overall light levels. The default values for this property are as follows:
+     
+     - flashMode == AVCaptureFlashModeAuto.
+     - autoStillImageStabilizationEnabled == YES.
+ */
+@property(nonatomic, copy) AVCapturePhotoSettings *photoSettingsForSceneMonitoring;
+
+/*!
+ @property highResolutionCaptureEnabled
+ @abstract
+    Indicates whether the photo render pipeline should be configured to deliver high resolution still images.
+
+ @discussion
+    Some AVCaptureDeviceFormats support outputting higher resolution stills than their streaming resolution (See AVCaptureDeviceFormat.highResolutionStillImageDimensions). Under some conditions, AVCaptureSession needs to set up the photo render pipeline differently to support high resolution still image capture. If you intend to take high resolution still images at all, you should set this property to YES before calling AVCaptureSession -startRunning. Once you've opted in for high resolution capture, you are free to issue photo capture requests with or without highResolutionCaptureEnabled in the AVCapturePhotoSettings. If you have not set this property to YES and call capturePhotoWithSettings:delegate: with settings.highResolutionCaptureEnabled set to YES, an NSInvalidArgumentException will be thrown.
+ */
+@property(nonatomic, getter=isHighResolutionCaptureEnabled) BOOL highResolutionCaptureEnabled;
+
+/*!
+ @property maxBracketedCapturePhotoCount
+ @abstract
+    Specifies the maximum number of photos that may be taken in a single bracket.
+
+ @discussion
+     AVCapturePhotoOutput can only satisfy a limited number of image requests in a single bracket without exhausting system resources. The maximum number of photos that may be taken in a single bracket depends on the size and format of the images being captured, and consequently may vary with AVCaptureSession -sessionPreset and AVCaptureDevice -activeFormat. Some formats do not support bracketed capture at all, and thus this property may return a value of 0. This read-only property is key-value observable. If you call -capturePhotoWithSettings:delegate: with a bracketedSettings whose count exceeds -maxBracketedCapturePhotoCount, an NSInvalidArgumentException is thrown.
+ */
+@property(nonatomic, readonly) NSUInteger maxBracketedCapturePhotoCount;
+
+/*!
+ @property lensStabilizationDuringBracketedCaptureSupported
+ @abstract
+    Indicates whether the receiver supports lens stabilization during bracketed captures.
+
+ @discussion
+    The AVCapturePhotoBracketSettings lensStabilizationEnabled property may only be set if this property returns YES. Its value may change as the session's -sessionPreset or input device's -activeFormat changes. This read-only property is key-value observable.
+ */
+@property(nonatomic, readonly, getter=isLensStabilizationDuringBracketedCaptureSupported) BOOL lensStabilizationDuringBracketedCaptureSupported;
+
+/*!
+ @property livePhotoCaptureSupported
+ @abstract
+    Indicates whether the receiver supports Live Photo capture.
+
+ @discussion
+    Live Photo capture is only supported for certain AVCaptureSession sessionPresets and AVCaptureDevice activeFormats. When switching cameras or formats this property may change. When this property changes from YES to NO, livePhotoCaptureEnabled also reverts to NO. If you've previously opted in for Live Photo capture and then change configurations, you may need to set livePhotoCaptureEnabled = YES again. 
+ */
+@property(nonatomic, readonly, getter=isLivePhotoCaptureSupported) BOOL livePhotoCaptureSupported;
+
+/*!
+ @property livePhotoCaptureEnabled
+ @abstract
+    Indicates whether the receiver is configured for Live Photo capture
+
+ @discussion
+    Default value is NO. This property may only be set to YES if livePhotoCaptureSupported is YES. Live Photo capture requires a lengthy reconfiguration of the capture render pipeline, so if you intend to do any Live Photo captures at all, you should set livePhotoCaptureEnabled to YES before calling AVCaptureSession -startRunning.
+ */
+@property(nonatomic, getter=isLivePhotoCaptureEnabled) BOOL livePhotoCaptureEnabled;
+
+/*!
+ @property livePhotoCaptureSuspended
+ @abstract
+    Indicates whether Live Photo capture is enabled, but currently suspended.
+
+ @discussion
+    This property allows you to cut current Live Photo movie captures short (for instance, if you suddenly need to do something that you don't want to show up in the Live Photo movie, such as take a non Live Photo capture that makes a shutter sound). By default, livePhotoCaptureSuspended is NO. When you set livePhotoCaptureSuspended = YES, any Live Photo movie captures in progress are trimmed to the current time. Likewise, when you toggle livePhotoCaptureSuspended from YES to NO, subsequent Live Photo movie captures will not contain any samples earlier than the time you un-suspended Live Photo capture. Setting this property to YES throws an NSInvalidArgumentException if livePhotoCaptureEnabled is NO. This property may only be set while the session is running. Setting this property to YES when the session is not running will fail resulting in livePhotoCaptureSuspended being reverted to NO.
+ */
+@property(nonatomic, getter=isLivePhotoCaptureSuspended) BOOL livePhotoCaptureSuspended;
+
+/*!
+ @property livePhotoAutoTrimmingEnabled
+ @abstract
+    Indicates whether Live Photo movies are trimmed in real time to avoid excessive movement.
+
+ @discussion
+    This property defaults to YES when livePhotoCaptureSupported is YES. Changing this property's value while your session is running will cause a lengthy reconfiguration of the session. You should set livePhotoAutoTrimmingEnabled to YES or NO before calling AVCaptureSession -startRunning. When set to YES, Live Photo movies are analyzed in real time and trimmed if there's excessive movement before or after the photo is taken. Nominally, Live Photos are approximately 3 seconds long. With trimming enabled, they may be shorter, depending on movement. This feature prevents common problems such as Live Photo movies containing shoe or pocket shots.
+ */
+@property(nonatomic, getter=isLivePhotoAutoTrimmingEnabled) BOOL livePhotoAutoTrimmingEnabled;
+
+/*!
+ @method JPEGPhotoDataRepresentationForJPEGSampleBuffer:previewPhotoSampleBuffer:
+ @abstract
+    A class method that writes a JPEG sample buffer to an NSData in the JPEG file format.
+ 
+ @param jpegSampleBuffer
+    A CMSampleBuffer containing JPEG compressed data.
+ @param previewSampleBuffer
+    An optional CMSampleBuffer containing pixel buffer image data to be written as a thumbnail image.
+ @result
+    An NSData containing bits in the JPEG file format. May return nil if the re-packaging process fails.
+
+ @discussion
+    AVCapturePhotoOutput delivers JPEG photos to clients as CMSampleBuffers. To re-package these buffers in a data format suitable for writing to a JPEG file, you may call this class method, optionally inserting your own metadata into the JPEG CMSampleBuffer first, and optionally passing a preview image to be written to the JPEG file format as a thumbnail image.
+ */
++ (nullable NSData *)JPEGPhotoDataRepresentationForJPEGSampleBuffer:(CMSampleBufferRef)JPEGSampleBuffer previewPhotoSampleBuffer:(nullable CMSampleBufferRef)previewPhotoSampleBuffer;
+
+/*!
+ @method DNGPhotoDataRepresentationForRawSampleBuffer:previewPhotoSampleBuffer:
+ @abstract
+    A class method that writes a RAW sample buffer to an NSData containing bits in the DNG file format.
+ 
+ @param rawSampleBuffer
+    A CMSampleBuffer containing Bayer RAW data.
+ @param previewSampleBuffer
+    An optional CMSampleBuffer containing pixel buffer image data to be written as a thumbnail image.
+ @result
+    An NSData containing bits in the DNG file format. May return nil if the re-packaging process fails.
+
+ @discussion
+    AVCapturePhotoOutput delivers RAW photos to clients as CMSampleBuffers. To re-package these buffers in a data format suitable for writing to a DNG file, you may call this class method, optionally inserting your own metadata into the RAW CMSampleBuffer first, and optionally passing a preview image to be written to the DNG file format as a thumbnail image. Only RAW images from Apple built-in cameras are supported.
+ */
++ (nullable NSData *)DNGPhotoDataRepresentationForRawSampleBuffer:(CMSampleBufferRef)rawSampleBuffer previewPhotoSampleBuffer:(nullable CMSampleBufferRef)previewPhotoSampleBuffer;
+
+@end
+
+
+/*!
+ @protocol AVCapturePhotoCaptureDelegate
+ @abstract
+    A set of delegate callbacks to be implemented by a client who calls AVCapturePhotoOutput's -capturePhotoWithSettings:delegate.
+ 
+ @discussion
+    AVCapturePhotoOutput invokes the AVCapturePhotoCaptureDelegate callbacks on a common dispatch queue — not necessarily the main queue. While the -captureOutput:willBeginCaptureForResolvedSettings: callback always comes first and the -captureOutput:didFinishCaptureForResolvedSettings: callback always comes last, none of the other callbacks can be assumed to come in any particular order. The AVCaptureResolvedPhotoSettings instance passed to the client with each callback has the same uniqueID as the AVCapturePhotoSettings instance passed in -capturePhotoWithSettings:delegate:. All callbacks are marked optional, but depending on the features you've specified in your AVCapturePhotoSettings, some callbacks become mandatory and are validated in -capturePhotoWithSettings:delegate:. If your delegate does not implement the mandatory callbacks, an NSInvalidArgumentException is thrown.
+
+    - If you initialize your photo settings with a format dictionary, or use one of the default constructors (that is, if you're not requesting a RAW-only capture), your delegate must respond to -captureOutput:didFinishProcessingPhotoSampleBuffer:previewPhotoSampleBuffer:resolvedSettings:bracketSettings:error:.
+    - If you initialize your photo settings with a rawPhotoPixelFormatType, your delegate must respond to -captureOutput:didFinishProcessingRawPhotoSampleBuffer:previewPhotoSampleBuffer:resolvedSettings:bracketSettings:error:.
+    - If you set livePhotoMovieFileURL to non-nil, your delegate must respond to -captureOutput:didFinishProcessingLivePhotoToMovieFileAtURL:duration:photoDisplayTime:resolvedSettings:error:.
+ 
+    In the event of an error, all expected callbacks are fired with an appropriate error.
+ */
+__TVOS_PROHIBITED
+@protocol AVCapturePhotoCaptureDelegate <NSObject>
+
+@optional
+/*!
+ @method captureOutput:willBeginCaptureForResolvedSettings:
+ @abstract
+    A callback fired as soon as the capture settings have been resolved.
+ 
+ @param captureOutput
+    The calling instance of AVCapturePhotoOutput.
+ @param resolvedSettings
+    An instance of AVCaptureResolvedPhotoSettings indicating which capture features have been selected.
+
+ @discussion
+    This callback is always delivered first for a particular capture request. It is delivered as soon as possible after you call -capturePhotoWithSettings:delegate:, so you can know what to expect in the remainder of your callbacks.
+ */
+- (void)captureOutput:(AVCapturePhotoOutput *)captureOutput willBeginCaptureForResolvedSettings:(AVCaptureResolvedPhotoSettings *)resolvedSettings;
+
+/*!
+ @method captureOutput:willCapturePhotoForResolvedSettings:
+ @abstract
+    A callback fired just as the photo is being taken.
+ 
+ @param captureOutput
+    The calling instance of AVCapturePhotoOutput.
+ @param resolvedSettings
+    An instance of AVCaptureResolvedPhotoSettings indicating which capture features have been selected.
+ 
+ @discussion
+    The timing of this callback is analogous to AVCaptureStillImageOutput's capturingStillImage property changing from NO to YES. The callback is delivered right after the shutter sound is heard (note that shutter sounds are suppressed when Live Photos are being captured).
+ */
+- (void)captureOutput:(AVCapturePhotoOutput *)captureOutput willCapturePhotoForResolvedSettings:(AVCaptureResolvedPhotoSettings *)resolvedSettings;
+
+/*!
+ @method captureOutput:didCapturePhotoForResolvedSettings:
+ @abstract
+    A callback fired just after the photo is taken.
+ 
+ @param captureOutput
+    The calling instance of AVCapturePhotoOutput.
+ @param resolvedSettings
+    An instance of AVCaptureResolvedPhotoSettings indicating which capture features have been selected.
+ 
+ @discussion
+    The timing of this callback is analogous to AVCaptureStillImageOutput's capturingStillImage property changing from YES to NO.
+ */
+- (void)captureOutput:(AVCapturePhotoOutput *)captureOutput didCapturePhotoForResolvedSettings:(AVCaptureResolvedPhotoSettings *)resolvedSettings;
+
+/*!
+ @method captureOutput:didFinishProcessingPhotoSampleBuffer:previewPhotoSampleBuffer:resolvedSettings:bracketSettings:error:
+ @abstract
+    A callback fired when the primary processed photo or photos are done.
+ 
+ @param captureOutput
+    The calling instance of AVCapturePhotoOutput.
+ @param photoSampleBuffer
+    A CMSampleBuffer containing an uncompressed pixel buffer or compressed data, along with timing information and metadata. May be nil if there was an error.
+ @param previewPhotoSampleBuffer
+    An optional CMSampleBuffer containing an uncompressed, down-scaled preview pixel buffer. May be nil.
+ @param resolvedSettings
+    An instance of AVCaptureResolvedPhotoSettings indicating which capture features have been selected.
+ @param bracketSettings
+    If this image is being delivered as part of a bracketed capture, the bracketSettings corresponding to this image. Otherwise nil.
+ @param error
+    An error indicating what went wrong if photoSampleBuffer is nil.
+ 
+ @discussion
+    If you've requested a single processed image (uncompressed or compressed) capture, the photo is delivered here. If you've requested a bracketed capture, this callback is fired bracketedSettings.count times (once for each photo in the bracket).
+ */
+- (void)captureOutput:(AVCapturePhotoOutput *)captureOutput didFinishProcessingPhotoSampleBuffer:(nullable CMSampleBufferRef)photoSampleBuffer previewPhotoSampleBuffer:(nullable CMSampleBufferRef)previewPhotoSampleBuffer resolvedSettings:(AVCaptureResolvedPhotoSettings *)resolvedSettings bracketSettings:(nullable AVCaptureBracketedStillImageSettings *)bracketSettings error:(nullable NSError *)error;
+
+/*!
+ @method captureOutput:didFinishProcessingRawPhotoSampleBuffer:previewPhotoSampleBuffer:resolvedSettings:bracketSettings:error:
+ @abstract
+    A callback fired when the RAW photo or photos are done.
+ 
+ @param captureOutput
+    The calling instance of AVCapturePhotoOutput.
+ @param rawSampleBuffer
+    A CMSampleBuffer containing Bayer RAW pixel data, along with timing information and metadata. May be nil if there was an error.
+ @param previewPhotoSampleBuffer
+    An optional CMSampleBuffer containing an uncompressed, down-scaled preview pixel buffer. May be nil.
+ @param resolvedSettings
+    An instance of AVCaptureResolvedPhotoSettings indicating which capture features have been selected.
+ @param bracketSettings
+    If this image is being delivered as part of a bracketed capture, the bracketSettings corresponding to this image. Otherwise nil.
+ @param error
+    An error indicating what went wrong if rawSampleBuffer is nil.
+ 
+ @discussion
+    Single RAW image and bracketed RAW photos are delivered here. If you've requested a RAW bracketed capture, this callback is fired bracketedSettings.count times (once for each photo in the bracket).
+ */
+- (void)captureOutput:(AVCapturePhotoOutput *)captureOutput didFinishProcessingRawPhotoSampleBuffer:(nullable CMSampleBufferRef)rawSampleBuffer previewPhotoSampleBuffer:(nullable CMSampleBufferRef)previewPhotoSampleBuffer resolvedSettings:(AVCaptureResolvedPhotoSettings *)resolvedSettings bracketSettings:(nullable AVCaptureBracketedStillImageSettings *)bracketSettings error:(nullable NSError *)error;
+
+/*!
+ @method captureOutput:didFinishRecordingLivePhotoMovieForEventualFileAtURL:resolvedSettings:
+ @abstract
+    A callback fired when the Live Photo movie has captured all its media data, though all media has not yet been written to file.
+ 
+ @param captureOutput
+    The calling instance of AVCapturePhotoOutput.
+ @param outputFileURL
+    The URL to which the movie file will be written. This URL is equal to your AVCapturePhotoSettings.livePhotoMovieURL.
+ @param resolvedSettings
+    An instance of AVCaptureResolvedPhotoSettings indicating which capture features have been selected.
+ 
+ @discussion
+    When this callback fires, no new media is being written to the file. If you are displaying a "Live" badge, this is an appropriate time to dismiss it. The movie file itself is not done being written until the -captureOutput:didFinishProcessingLivePhotoToMovieFileAtURL:duration:photoDisplayTime:resolvedSettings:error: callback fires.
+ */
+- (void)captureOutput:(AVCapturePhotoOutput *)captureOutput didFinishRecordingLivePhotoMovieForEventualFileAtURL:(NSURL *)outputFileURL resolvedSettings:(AVCaptureResolvedPhotoSettings *)resolvedSettings;
+
+/*!
+ @method captureOutput:didFinishProcessingLivePhotoToMovieFileAtURL:duration:photoDisplayTime:resolvedSettings:error:
+ @abstract
+    A callback fired when the Live Photo movie is finished being written to disk.
+ 
+ @param captureOutput
+    The calling instance of AVCapturePhotoOutput.
+ @param outputFileURL
+    The URL where the movie file resides. This URL is equal to your AVCapturePhotoSettings.livePhotoMovieURL.
+ @param duration
+    A CMTime indicating the duration of the movie file.
+ @param photoDisplayTime
+    A CMTime indicating the time in the movie at which the still photo should be displayed.
+ @param resolvedSettings
+    An instance of AVCaptureResolvedPhotoSettings indicating which capture features have been selected.
+ @param error
+    An error indicating what went wrong if the outputFileURL is damaged.
+ 
+ @discussion
+    When this callback fires, the movie on disk is fully finished and ready for consumption.
+ */
+- (void)captureOutput:(AVCapturePhotoOutput *)captureOutput didFinishProcessingLivePhotoToMovieFileAtURL:(NSURL *)outputFileURL duration:(CMTime)duration photoDisplayTime:(CMTime)photoDisplayTime resolvedSettings:(AVCaptureResolvedPhotoSettings *)resolvedSettings error:(nullable NSError *)error;
+
+/*!
+ @method captureOutput:didFinishCaptureForResolvedSettings:error:
+ @abstract
+    A callback fired when the photo capture is completed and no more callbacks will be fired.
+ 
+ @param captureOutput
+    The calling instance of AVCapturePhotoOutput.
+ @param resolvedSettings
+    An instance of AVCaptureResolvedPhotoSettings indicating which capture features were selected.
+ @param error
+    An error indicating whether the capture was unsuccessful. Nil if there were no problems.
+ 
+ @discussion
+    This callback always fires last and when it does, you may clean up any state relating to this photo capture.
+ */
+- (void)captureOutput:(AVCapturePhotoOutput *)captureOutput didFinishCaptureForResolvedSettings:(AVCaptureResolvedPhotoSettings *)resolvedSettings error:(nullable NSError *)error;
+
+@end
+
+
+@class AVCapturePhotoSettingsInternal;
+
+/*!
+ @class AVCapturePhotoSettings
+ @abstract
+    A mutable settings object encapsulating all the desired properties of a photo capture.
+ 
+ @discussion
+    To take a picture, a client instantiates and configures an AVCapturePhotoSettings object, then calls AVCapturePhotoOutput's -capturePhotoWithSettings:delegate:, passing the settings and a delegate to be informed when events relating to the photo capture occur. Since AVCapturePhotoSettings has no reference to the AVCapturePhotoOutput instance with which it will be used, minimal validation occurs while you configure an AVCapturePhotoSettings instance. The bulk of the validation is executed when you call AVCapturePhotoOutput's -capturePhotoWithSettings:delegate:.
+ */
+NS_CLASS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED
+@interface AVCapturePhotoSettings : NSObject <NSCopying>
+{
+@private
+	AVCapturePhotoSettingsInternal *_internal;
+}
+
+/*!
+ @method photoSettings
+ @abstract
+    Creates a default instance of AVCapturePhotoSettings.
+ 
+ @result
+    An instance of AVCapturePhotoSettings.
+ 
+ @discussion
+    A default AVCapturePhotoSettings object has a format of AVVideoCodecJPEG and autoStillImageStabilizationEnabled set to YES.
+ */
++ (instancetype)photoSettings;
+
+/*!
+ @method photoSettingsWithFormat:
+ @abstract
+    Creates an instance of AVCapturePhotoSettings with a user-specified output format.
+ 
+ @param format
+    A dictionary of Core Video pixel buffer attributes or AVVideoSettings, analogous to AVCaptureStillImageOutput's outputSettings property.
+ @result
+    An instance of AVCapturePhotoSettings.
+ 
+ @discussion
+    If you wish an uncompressed format, your dictionary must contain kCVPixelBufferPixelFormatTypeKey, and the format specified must be present in AVCapturePhotoOutput's -availablePhotoPixelFormatTypes array. kCVPixelBufferPixelFormatTypeKey is the only supported key when expressing uncompressed output. If you wish a compressed format, your dictionary must contain AVVideoCodecKey and the codec specified must be present in AVCapturePhotoOutput's -availablePhotoCodecTypes array. If you are specifying a compressed format, the AVVideoQualityKey is also supported. Passing a nil format dictionary is analogous to calling +photoSettings.
+ */
++ (instancetype)photoSettingsWithFormat:(nullable NSDictionary<NSString *, id> *)format;
+
+/*!
+ @method photoSettingsWithRawPixelFormatType:
+ @abstract
+    Creates an instance of AVCapturePhotoSettings specifying RAW only output.
+ 
+ @param rawPixelFormatType
+    A Bayer RAW pixel format OSType (defined in CVPixelBuffer.h).
+ @result
+    An instance of AVCapturePhotoSettings.
+
+ @discussion
+    rawPixelFormatType must be one of the OSTypes contained in AVCapturePhotoOutput's -availableRawPhotoPixelFormatTypes array. See AVCapturePhotoOutput's -capturePhotoWithSettings:delegate: inline documentation for a discussion of restrictions on AVCapturePhotoSettings when requesting RAW capture.
+ */
++ (instancetype)photoSettingsWithRawPixelFormatType:(OSType)rawPixelFormatType;
+
+/*!
+ @method photoSettingsWithRawPixelFormatType:processedFormat:
+ @abstract
+    Creates an instance of AVCapturePhotoSettings specifying RAW + a processed format (such as JPEG).
+ 
+ @param rawPixelFormatType
+    A Bayer RAW pixel format OSType (defined in CVPixelBuffer.h).
+ @param processedFormat
+    A dictionary of Core Video pixel buffer attributes or AVVideoSettings, analogous to AVCaptureStillImageOutput's outputSettings property.
+ @result
+    An instance of AVCapturePhotoSettings.
+ 
+ @discussion
+    rawPixelFormatType must be one of the OSTypes contained in AVCapturePhotoOutput's -availableRawPhotoPixelFormatTypes array. If you wish an uncompressed processedFormat, your dictionary must contain kCVPixelBufferPixelFormatTypeKey, and the processedFormat specified must be present in AVCapturePhotoOutput's -availablePhotoPixelFormatTypes array. kCVPixelBufferPixelFormatTypeKey is the only supported key when expressing uncompressed processedFormat. If you wish a compressed format, your dictionary must contain AVVideoCodecKey and the codec specified must be present in AVCapturePhotoOutput's -availablePhotoCodecTypes array. If you are specifying a compressed format, the AVVideoQualityKey is also supported. Passing a nil processedFormat dictionary is analogous to calling +photoSettingsWithRawPixelFormatType:. See AVCapturePhotoOutput's -capturePhotoWithSettings:delegate: inline documentation for a discussion of restrictions on AVCapturePhotoSettings when requesting RAW capture.
+ */
++ (instancetype)photoSettingsWithRawPixelFormatType:(OSType)rawPixelFormatType processedFormat:(nullable NSDictionary<NSString *, id> *)processedFormat;
+
+/*!
+ @method photoSettingsFromPhotoSettings:
+ @abstract
+    Creates an instance of AVCapturePhotoSettings with a new uniqueID from an existing instance of AVCapturePhotoSettings.
+ 
+ @param photoSettings
+     An existing AVCapturePhotoSettings instance.
+ @result
+    An new instance of AVCapturePhotoSettings with new uniqueID.
+ 
+ @discussion
+    Use this factory method to create a clone of an existing photo settings instance, but with a new uniqueID that can safely be passed to AVCapturePhotoOutput -capturePhotoWithSettings:delegate:.
+ */
++ (instancetype)photoSettingsFromPhotoSettings:(AVCapturePhotoSettings *)photoSettings;
+
+/*!
+ @property uniqueID
+ @abstract
+    A 64-bit number that uniquely identifies this instance.
+
+ @discussion
+    When you create an instance of AVCapturePhotoSettings, a uniqueID is generated automatically. This uniqueID is guaranteed to be unique for the life time of your process.
+ */
+@property(readonly) int64_t uniqueID;
+
+/*!
+ @property format
+ @abstract
+    A dictionary of Core Video pixel buffer attributes or AVVideoSettings, analogous to AVCaptureStillImageOutput's outputSettings property.
+
+ @discussion
+    The format dictionary you passed to one of the creation methods. May be nil if you've specified RAW-only capture.
+ */
+@property(nullable, readonly, copy) NSDictionary<NSString *, id> *format;
+
+/*!
+ @property rawPhotoPixelFormatType
+ @abstract
+    A Bayer RAW pixel format OSType (defined in CVPixelBuffer.h).
+
+ @discussion
+    The rawPixelFormatType you specified in one of the creation methods. Returns 0 if you did not specify RAW capture. See AVCapturePhotoOutput's -capturePhotoWithSettings:delegate: inline documentation for a discussion of restrictions on AVCapturePhotoSettings when requesting RAW capture.
+ */
+@property(readonly) OSType rawPhotoPixelFormatType;
+
+/*!
+ @property flashMode
+ @abstract
+    Specifies whether the flash should be on, off, or chosen automatically by AVCapturePhotoOutput.
+
+ @discussion
+    flashMode takes the place of the deprecated AVCaptureDevice -flashMode API. Setting AVCaptureDevice.flashMode has no effect on AVCapturePhotoOutput, which only pays attention to the flashMode specified in your AVCapturePhotoSettings. The default value is AVCaptureFlashModeOff. Flash modes are defined in AVCaptureDevice.h. If you specify a flashMode of AVCaptureFlashModeOn, it wins over autoStillImageStabilizationEnabled=YES. When the device becomes very hot, the flash becomes temporarily unavailable until the device cools down (see AVCaptureDevice's -flashAvailable). While the flash is unavailable, AVCapturePhotoOutput's -supportedFlashModes property still reports AVCaptureFlashModeOn and AVCaptureFlashModeAuto as being available, thus allowing you to specify a flashMode of AVCaptureModeOn. You should always check the AVCaptureResolvedPhotoSettings provided to you in the AVCapturePhotoCaptureDelegate callbacks, as the resolved flashEnabled property will tell you definitively if the flash is being used.
+ */
+@property(nonatomic) AVCaptureFlashMode flashMode;
+
+/*!
+ @property autoStillImageStabilizationEnabled
+ @abstract
+    Specifies whether still image stabilization should be used automatically.
+
+ @discussion
+    Default is YES unless you are capturing a RAW photo (RAW photos may not be processed by definition). When set to YES, still image stabilization is applied automatically in low light to counteract hand shake. If the device has optical image stabilization, autoStillImageStabilizationEnabled makes use of lens stabilization as well.
+ */
+@property(nonatomic, getter=isAutoStillImageStabilizationEnabled) BOOL autoStillImageStabilizationEnabled;
+
+/*!
+ @property highResolutionPhotoEnabled
+ @abstract
+    Specifies whether photos should be captured at the highest resolution supported by the source AVCaptureDevice's activeFormat.
+
+ @discussion
+    Default is NO. By default, AVCapturePhotoOutput emits images with the same dimensions as its source AVCaptureDevice's activeFormat.formatDescription. However, if you set this property to YES, the AVCapturePhotoOutput emits images at its source AVCaptureDevice's activeFormat.highResolutionStillImageDimensions. Note that if you enable video stabilization (see AVCaptureConnection's preferredVideoStabilizationMode) for any output, the high resolution photos emitted by AVCapturePhotoOutput may be smaller by 10 or more percent. You may inspect your AVCaptureResolvedPhotoSettings in the delegate callbacks to discover the exact dimensions of the capture photo(s).
+ */
+@property(nonatomic, getter=isHighResolutionPhotoEnabled) BOOL highResolutionPhotoEnabled;
+
+/*!
+ @property livePhotoMovieFileURL
+ @abstract
+    Specifies that a Live Photo movie be captured to complement the still photo.
+
+ @discussion
+    A Live Photo movie is a short movie (with audio, if you've added an audio input to your session) containing the moments right before and after the still photo. A QuickTime movie file will be written to disk at the URL specified if it is a valid file URL accessible to your app's sandbox. You may only set this property is AVCapturePhotoOutput's livePhotoCaptureSupported property is YES. When you specify a Live Photo, your AVCapturePhotoCaptureDelegate object must implement -captureOutput:didFinishProcessingLivePhotoToMovieFileAtURL:duration:photoDisplayTime:resolvedSettings:error:.
+ */
+@property(nonatomic, copy, nullable) NSURL *livePhotoMovieFileURL;
+
+/*!
+ @property livePhotoMovieMetadata
+ @abstract
+    Movie-level metadata to be written to the Live Photo movie.
+
+ @discussion
+    An array of AVMetadataItems to be inserted into the top level of the Live Photo movie. The receiver makes immutable copies of the AVMetadataItems in the array. Live Photo movies always contain a AVMetadataQuickTimeMetadataKeyContentIdentifier which allow them to be paired with a similar identifier in the MakerNote of the photo complement. AVCapturePhotoSettings generates a unique content identifier for you if you do not specify one of your own.
+ */
+@property(nonatomic, copy, null_resettable) NSArray<AVMetadataItem *> *livePhotoMovieMetadata;
+
+/*!
+ @property availablePreviewPhotoPixelFormatTypes
+ @abstract
+    An array of available kCVPixelBufferPixelFormatTypeKeys that may be used when specifying a previewPhotoFormat.
+ 
+ @discussion
+    The array is sorted such that the preview format requiring the fewest conversions is presented first.
+ */
+@property(nonatomic, readonly) NSArray<NSNumber *> *availablePreviewPhotoPixelFormatTypes;
+
+/*!
+ @property previewPhotoFormat
+ @abstract
+    A dictionary of Core Video pixel buffer attributes specifying the preview photo format to be delivered along with the RAW or processed photo.
+
+ @discussion
+    A dictionary of pixel buffer attributes specifying a smaller version of the RAW or processed photo for preview purposes. This image is sometimes referred to as a "thumbnail image". The kCVPixelBufferPixelFormatTypeKey is required and must be present in the receiver's -availablePreviewPhotoPixelFormatTypes array. Optional keys are { kCVPixelBufferWidthKey | kCVPixelBufferHeightKey }. If you wish to specify dimensions, you must add both width and height. Width and height must are only honored up to the display dimensions. If you specify a width and height whose aspect ratio differs from the RAW or processed photo, the larger of the two dimensions is honored and aspect ratio of the RAW or processed photo is always preserved.
+ */
+@property(nonatomic, copy, nullable) NSDictionary<NSString *, id> *previewPhotoFormat;
+
+@end
+
+
+@class AVCapturePhotoBracketSettingsInternal;
+
+/*!
+ @class AVCapturePhotoBracketSettings
+ @abstract
+    A concrete subclass of AVCapturePhotoSettings that describes a bracketed capture.
+ 
+ @discussion
+    In addition to the properties expressed in the base class, an AVCapturePhotoBracketSettings contains an array of AVCaptureBracketedStillImageSettings objects, where each describes one individual photo in the bracket. bracketedSettings.count must be <= AVCapturePhotoOutput's -maxBracketedCapturePhotoCount. Capturing a photo bracket may require the allocation of additional resources. By calling -prepareToCapturePhotoWithSettings:completionHandler: in advance, you can deterministically know when the AVCapturePhotoOutput instance is ready to capture a bracket with the given settings with no additional delay for allocation.
+
+    When you request a bracketed capture, your AVCapturePhotoCaptureDelegate's -captureOutput:didFinishProcessing{Photo | RawPhoto}... callbacks are called back bracketSettings.count times and provided with the corresponding AVCaptureBracketedStillImageSettings object from your request.
+ */
+NS_CLASS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED
+@interface AVCapturePhotoBracketSettings : AVCapturePhotoSettings
+{
+@private
+	AVCapturePhotoBracketSettingsInternal *_bracketSettingsInternal;
+}
+
+/*!
+ @method initWithFormat:rawPixelFormatType:bracketedSettings:
+ @abstract
+    Creates an instance of AVCapturePhotoBracketSettings.
+ 
+ @param format
+    A dictionary of Core Video pixel buffer attributes or AVVideoSettings, analogous to AVCaptureStillImageOutput's outputSettings property. If you wish an uncompressed format, your dictionary must contain kCVPixelBufferPixelFormatTypeKey, and the format specified must be present in AVCapturePhotoOutput's -availablePhotoPixelFormatTypes array. kCVPixelBufferPixelFormatTypeKey is the only supported key when expressing uncompressed output. If you wish a compressed format, your dictionary must contain AVVideoCodecKey and the codec specified must be present in AVCapturePhotoOutput's -availablePhotoCodecTypes array. If you are specifying a compressed format, the AVVideoQualityKey is also supported. If you only wish to capture RAW, you may pass a nil format dictionary and a non-zero rawPixelFormatType. If you pass a nil format dictionary AND a rawPixelFormatType of 0, the default output of AVVideoCodecJPEG will be delivered.
+ @param rawPixelFormatType
+    One of the OSTypes contained in AVCapturePhotoOutput's -availableRawPhotoPixelFormatTypes array. May be set to 0 if you do not desire RAW capture.
+ @param bracketedSettings
+    An array of AVCaptureBracketedStillImageSettings objects (defined in AVCaptureStillImageOutput.h). All must be of the same type, either AVCaptureManualExposureBracketedStillImageSettings or AVCaptureAutoExposureBracketedStillImageSettings. bracketedSettings.count must be <= AVCapturePhotoOutput's -maxBracketedCapturePhotoCount.
+ @result
+    An instance of AVCapturePhotoBracketSettings.
+
+ @discussion
+    An NSInvalidArgumentException is thrown if bracketedSettings is nil, contains zero elements, or mixes and matches different subclasses of AVCaptureBracketedStillImageSettings.
+ 
+    AVCapturePhotoBracketSettings do not support flashMode, autoStillImageStabilizationEnabled, livePhotoMovieFileURL or livePhotoMovieMetadata.
+ */
+- (instancetype)initWithFormat:(nullable NSDictionary<NSString *, id> *)format rawPixelFormatType:(OSType)rawPixelFormatType bracketedSettings:(NSArray<AVCaptureBracketedStillImageSettings *> *)bracketedSettings;
+
+/*!
+ @property bracketedSettings
+ @abstract
+    An array of AVCaptureBracketedStillImageSettings objects you passed in -initWithFormat:rawPixelFormatType:bracketedSettings:
+
+ @discussion
+    This read-only property never returns nil.
+ */
+@property(nonatomic, readonly) NSArray<AVCaptureBracketedStillImageSettings *> *bracketedSettings;
+
+/*!
+ @property lensStabilizationEnabled
+ @abstract
+    Specifies whether lens (optical) stabilization should be employed during the bracketed capture.
+
+ @discussion
+    Default value is NO. This property may only be set to YES if AVCapturePhotoOutput's isLensStabilizationDuringBracketedCaptureSupported is YES. When set to YES, AVCapturePhotoOutput holds the lens steady for the duration of the bracket to counter hand shake and produce a sharper bracket of images.
+ */
+@property(nonatomic, getter=isLensStabilizationEnabled) BOOL lensStabilizationEnabled;
+
+@end
+
+
+@class AVCaptureResolvedPhotoSettingsInternal;
+
+/*!
+ @class AVCaptureResolvedPhotoSettings
+ @abstract
+    An immutable object produced by callbacks in each and every AVCapturePhotoCaptureDelegate protocol method.
+ 
+ @discussion
+    When you initiate a photo capture request using -capturePhotoWithSettings:delegate:, some of your settings are not yet certain. For instance, auto flash and auto still image stabilization allow the AVCapturePhotoOutput to decide just in time whether to employ flash or still image stabilization, depending on the current scene. Once the request is issued, AVCapturePhotoOutput begins the capture, resolves the uncertain settings, and in its first callback informs you of its choices through an AVCaptureResolvedPhotoSettings object. This same object is presented to all the callbacks fired for a particular photo capture request. Its uniqueID property matches that of the AVCapturePhotoSettings instance you used to initiate the photo request.
+ */
+NS_CLASS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED
+@interface AVCaptureResolvedPhotoSettings : NSObject
+{
+@private
+	AVCaptureResolvedPhotoSettingsInternal *_internal;
+}
+
+/*!
+ @method init
+ @abstract
+    You may not create an instance of AVCaptureResolvedPhotoSettings directly.
+ 
+ @result
+    An instance of AVCaptureResolvedPhotoSettings (unavailable)
+
+ @discussion
+    An instance of AVCaptureResolvedPhotoSettings is handed to you in each of the AVCapturePhotoCaptureDelegate callback methods.
+ */
+- (instancetype)init NS_UNAVAILABLE;
+
+/*!
+ @property uniqueID
+ @abstract
+    uniqueID matches that of the AVCapturePhotoSettings instance you passed to -capturePhotoWithSettings:delegate:.
+ */
+@property(readonly) int64_t uniqueID;
+
+/*!
+ @property photoDimensions
+ @abstract
+    The resolved dimensions of the photo buffer that will be delivered to the -captureOutput:didFinishProcessingPhotoSampleBuffer:previewPhotoSampleBuffer:resolvedSettings:bracketSettings:error: callback.
+ 
+ @discussion
+    If you request a RAW capture with no processed companion image, photoDimensions resolve to { 0, 0 }.
+ */
+@property(readonly) CMVideoDimensions photoDimensions;
+
+/*!
+ @property rawPhotoDimensions
+ @abstract
+    The resolved dimensions of the RAW photo buffer that will be delivered to the -captureOutput:didFinishProcessingRawPhotoSampleBuffer:previewPhotoSampleBuffer:resolvedSettings:bracketSettings:error: callback.
+
+ @discussion
+    If you request a non-RAW capture, rawPhotoDimensions resolve to { 0, 0 }.
+ */
+@property(readonly) CMVideoDimensions rawPhotoDimensions;
+
+/*!
+ @property previewDimensions
+ @abstract
+    The resolved dimensions of the preview photo buffer that will be delivered to the -captureOutput:didFinishProcessing{Photo | RawPhoto}... AVCapturePhotoCaptureDelegate callbacks.
+
+ @discussion
+    If you don't request a preview image, previewDimensions resolve to { 0, 0 }.
+ */
+@property(readonly) CMVideoDimensions previewDimensions;
+
+/*!
+ @property livePhotoMovieDimensions
+ @abstract
+    The resolved dimensions of the video track in the movie that will be delivered to the -captureOutput:didFinishProcessingLivePhotoToMovieFileAtURL:duration:photoDisplayTime:resolvedSettings:error: callback.
+ 
+ @discussion
+    If you don't request Live Photo capture, livePhotoMovieDimensions resolve to { 0, 0 }.
+ */
+@property(readonly) CMVideoDimensions livePhotoMovieDimensions;
+
+/*!
+ @property flashEnabled
+ @abstract
+    Indicates whether the flash will fire when capturing the photo.
+
+ @discussion
+    When you specify AVCaptureFlashModeAuto as you AVCapturePhotoSettings.flashMode, you don't know if flash capture will be chosen until you inspect the AVCaptureResolvedPhotoSettings flashEnabled property. If the device becomes too hot, the flash becomes temporarily unavailable. You can key-value observe AVCaptureDevice's flashAvailable property to know when this occurs. If the flash is unavailable due to thermal issues, and you specify a flashMode of AVCaptureFlashModeOn, flashEnabled still resolves to NO until the device has sufficiently cooled off.
+ */
+@property(readonly, getter=isFlashEnabled) BOOL flashEnabled;
+
+/*!
+ @property stillImageStabilizationEnabled
+ @abstract
+    Indicates whether still image stabilization will be employed when capturing the photo.
+ */
+@property(readonly, getter=isStillImageStabilizationEnabled) BOOL stillImageStabilizationEnabled;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureSession.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureSession.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureSession.h	2015-09-30 23:18:01.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureSession.h	2016-05-25 04:40:24.000000000 +0200
@@ -18,23 +18,18 @@
     Posted when an unexpected error occurs while an AVCaptureSession instance is running.
  
  @discussion
-    The notification object is the AVCaptureSession instance that encountered a runtime error.
-    The userInfo dictionary contains an NSError for the key AVCaptureSessionErrorKey.
-*/
+    The notification object is the AVCaptureSession instance that encountered a runtime error. The userInfo dictionary contains an NSError for the key AVCaptureSessionErrorKey.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionRuntimeErrorNotification NS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED;
 
 /*!
  @constant AVCaptureSessionErrorKey
  @abstract
-    The key used to provide an NSError describing the failure condition in an
-    AVCaptureSessionRuntimeErrorNotification.
+    The key used to provide an NSError describing the failure condition in an AVCaptureSessionRuntimeErrorNotification.
  
  @discussion
-    AVCaptureSessionErrorKey may be found in the userInfo dictionary provided with
-    an AVCaptureSessionRuntimeErrorNotification.  The NSError associated with the
-    notification gives greater detail on the nature of the error, and in some cases
-    recovery suggestions. 
-*/
+    AVCaptureSessionErrorKey may be found in the userInfo dictionary provided with an AVCaptureSessionRuntimeErrorNotification. The NSError associated with the notification gives greater detail on the nature of the error, and in some cases recovery suggestions.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionErrorKey NS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED;
 
 /*!
@@ -43,9 +38,8 @@
     Posted when an instance of AVCaptureSession successfully starts running.
  
  @discussion
-    Clients may observe the AVCaptureSessionDidStartRunningNotification to know
-    when an instance of AVCaptureSession starts running.
-*/
+    Clients may observe the AVCaptureSessionDidStartRunningNotification to know when an instance of AVCaptureSession starts running.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionDidStartRunningNotification NS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED;
 
 /*!
@@ -54,11 +48,8 @@
     Posted when an instance of AVCaptureSession stops running.
  
  @discussion
-    Clients may observe the AVCaptureSessionDidStopRunningNotification to know
-    when an instance of AVCaptureSession stops running.  An AVCaptureSession instance
-    may stop running automatically due to external system conditions, such as the
-    device going to sleep, or being locked by a user.
-*/
+    Clients may observe the AVCaptureSessionDidStopRunningNotification to know when an instance of AVCaptureSession stops running. An AVCaptureSession instance may stop running automatically due to external system conditions, such as the device going to sleep, or being locked by a user.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionDidStopRunningNotification NS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED;
 
 #if TARGET_OS_IPHONE
@@ -69,42 +60,26 @@
     Posted when an instance of AVCaptureSession becomes interrupted.
  
  @discussion
-    Clients may observe the AVCaptureSessionWasInterruptedNotification to know
-    when an instance of AVCaptureSession has been interrupted, for example, by
-    an incoming phone call, or alarm, or another application taking control of 
-    needed hardware resources.  When appropriate, the AVCaptureSession instance
-    will stop running automatically in response to an interruption.
- 
-    Beginning in iOS 9.0, the AVCaptureSessionWasInterruptedNotification userInfo dictionary
-    contains an AVCaptureSessionInterruptionReasonKey indicating the reason for the interruption.
-*/
+    Clients may observe the AVCaptureSessionWasInterruptedNotification to know when an instance of AVCaptureSession has been interrupted, for example, by an incoming phone call, or alarm, or another application taking control of needed hardware resources. When appropriate, the AVCaptureSession instance will stop running automatically in response to an interruption.
+ 
+    Beginning in iOS 9.0, the AVCaptureSessionWasInterruptedNotification userInfo dictionary contains an AVCaptureSessionInterruptionReasonKey indicating the reason for the interruption.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionWasInterruptedNotification NS_AVAILABLE_IOS(4_0) __TVOS_PROHIBITED;
 
 /*!
  @enum AVCaptureSessionInterruptionReason
  @abstract
-    Constants indicating interruption reason.  One of these is returned with the
-    AVCaptureSessionWasInterruptedNotification (see AVCaptureSessionInterruptionReasonKey).
+    Constants indicating interruption reason. One of these is returned with the AVCaptureSessionWasInterruptedNotification (see AVCaptureSessionInterruptionReasonKey).
  
  @constant AVCaptureSessionInterruptionReasonVideoDeviceNotAvailableInBackground
-    An interruption caused by the app being sent to the background while using a camera. Camera usage 
-    is prohibited while in the background. Beginning in iOS 9.0, AVCaptureSession no longer produces an
-    AVCaptureSessionRuntimeErrorNotification if you attempt to start running a camera while in the background.
-    Instead, it sends an AVCaptureSessionWasInterruptedNotification with
-    AVCaptureSessionInterruptionReasonVideoDeviceNotAvailableInBackground. Provided you don't explicitly call 
-    [session stopRunning], your -startRunning request is preserved, and when your app comes back to foreground,
-    you receive AVCaptureSessionInterruptionEndedNotification and your session starts running.
+    An interruption caused by the app being sent to the background while using a camera. Camera usage is prohibited while in the background. Beginning in iOS 9.0, AVCaptureSession no longer produces an AVCaptureSessionRuntimeErrorNotification if you attempt to start running a camera while in the background. Instead, it sends an AVCaptureSessionWasInterruptedNotification with AVCaptureSessionInterruptionReasonVideoDeviceNotAvailableInBackground. Provided you don't explicitly call [session stopRunning], your -startRunning request is preserved, and when your app comes back to foreground, you receive AVCaptureSessionInterruptionEndedNotification and your session starts running.
  @constant AVCaptureSessionInterruptionReasonAudioDeviceInUseByAnotherClient
-    An interruption caused by the audio hardware temporarily being made unavailable, for instance,
-    for a phone call, or alarm.
+    An interruption caused by the audio hardware temporarily being made unavailable, for instance, for a phone call, or alarm.
  @constant AVCaptureSessionInterruptionReasonVideoDeviceInUseByAnotherClient
-    An interruption caused by the video device temporarily being made unavailable, for instance,
-    when stolen away by another AVCaptureSession.
+    An interruption caused by the video device temporarily being made unavailable, for instance, when stolen away by another AVCaptureSession.
  @constant AVCaptureSessionInterruptionReasonVideoDeviceNotAvailableWithMultipleForegroundApps
-    An interruption caused when the app is running in a multi-app layout, causing resource contention
-    and degraded recording quality of service. Given your present AVCaptureSession configuration, the 
-    session may only be run if your app occupies the full screen.
-*/
+    An interruption caused when the app is running in a multi-app layout, causing resource contention and degraded recording quality of service. Given your present AVCaptureSession configuration, the session may only be run if your app occupies the full screen.
+ */
 typedef NS_ENUM(NSInteger, AVCaptureSessionInterruptionReason) {
     AVCaptureSessionInterruptionReasonVideoDeviceNotAvailableInBackground               = 1,
     AVCaptureSessionInterruptionReasonAudioDeviceInUseByAnotherClient                   = 2,
@@ -115,14 +90,11 @@
 /*!
  @constant AVCaptureSessionInterruptionReasonKey
  @abstract
-    The key used to provide an NSNumber describing the interruption reason in an
-    AVCaptureSessionWasInterruptedNotification.
+    The key used to provide an NSNumber describing the interruption reason in an AVCaptureSessionWasInterruptedNotification.
  
  @discussion
-    AVCaptureSessionInterruptionReasonKey may be found in the userInfo dictionary provided with
-    an AVCaptureSessionWasInterruptedNotification.  The NSNumber associated with the
-    notification tells you why the interruption occurred.
-*/
+    AVCaptureSessionInterruptionReasonKey may be found in the userInfo dictionary provided with an AVCaptureSessionWasInterruptedNotification. The NSNumber associated with the notification tells you why the interruption occurred.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionInterruptionReasonKey NS_AVAILABLE_IOS(9_0) __TVOS_PROHIBITED;
 
 /*!
@@ -131,13 +103,8 @@
     Posted when an instance of AVCaptureSession ceases to be interrupted.
  
  @discussion
-    Clients may observe the AVCaptureSessionInterruptionEndedNotification to know
-    when an instance of AVCaptureSession ceases to be interrupted, for example, when
-    a  phone call ends, and hardware resources needed to run the session are again
-    available.  When appropriate, the AVCaptureSession instance that was previously
-    stopped in response to an interruption will automatically restart once the
-    interruption ends.
-*/
+    Clients may observe the AVCaptureSessionInterruptionEndedNotification to know when an instance of AVCaptureSession ceases to be interrupted, for example, when a phone call ends, and hardware resources needed to run the session are again available. When appropriate, the AVCaptureSession instance that was previously stopped in response to an interruption will automatically restart once the interruption ends.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionInterruptionEndedNotification NS_AVAILABLE_IOS(4_0) __TVOS_PROHIBITED;
 
 #endif // TARGET_OS_IPHONE
@@ -145,8 +112,7 @@
 /*!
  @enum AVCaptureVideoOrientation
  @abstract
-    Constants indicating video orientation, for use with AVCaptureVideoPreviewLayer 
-    (see AVCaptureVideoPreviewLayer.h) and AVCaptureConnection (see below).
+    Constants indicating video orientation, for use with AVCaptureVideoPreviewLayer (see AVCaptureVideoPreviewLayer.h) and AVCaptureConnection (see below).
  
  @constant AVCaptureVideoOrientationPortrait
     Indicates that video should be oriented vertically, home button on the bottom.
@@ -156,7 +122,7 @@
     Indicates that video should be oriented horizontally, home button on the right.
  @constant AVCaptureVideoOrientationLandscapeLeft
     Indicates that video should be oriented horizontally, home button on the left.
-*/
+ */
 typedef NS_ENUM(NSInteger, AVCaptureVideoOrientation) {
     AVCaptureVideoOrientationPortrait           = 1,
     AVCaptureVideoOrientationPortraitUpsideDown = 2,
@@ -170,9 +136,8 @@
     An AVCaptureSession preset suitable for high resolution photo quality output.
  
  @discussion
-    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPresetPhoto
-    for full resolution photo quality output.
-*/
+    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPresetPhoto for full resolution photo quality output.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionPresetPhoto NS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED;
 
 /*!
@@ -181,10 +146,8 @@
     An AVCaptureSession preset suitable for high quality video and audio output.
  
  @discussion
-    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPresetHigh
-    to achieve high quality video and audio output.  AVCaptureSessionPresetHigh is the
-    default sessionPreset value.
-*/
+    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPresetHigh to achieve high quality video and audio output. AVCaptureSessionPresetHigh is the default sessionPreset value.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionPresetHigh NS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED;
 
 /*!
@@ -193,9 +156,8 @@
     An AVCaptureSession preset suitable for medium quality output.
  
  @discussion
-    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPresetMedium
-    to achieve output video and audio bitrates suitable for sharing over WiFi.
-*/
+    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPresetMedium to achieve output video and audio bitrates suitable for sharing over WiFi.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionPresetMedium NS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED;
 
 /*!
@@ -204,9 +166,8 @@
     An AVCaptureSession preset suitable for low quality output.
  
  @discussion
-    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPresetLow
-    to achieve output video and audio bitrates suitable for sharing over 3G.
-*/
+    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPresetLow to achieve output video and audio bitrates suitable for sharing over 3G.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionPresetLow NS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED;
 
 #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
@@ -217,9 +178,8 @@
     An AVCaptureSession preset suitable for 320x240 video output.
  
  @discussion
-    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPreset320x240
-    to achieve 320x240 output.
-*/
+    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPreset320x240 to achieve 320x240 output.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionPreset320x240 NS_AVAILABLE(10_7, NA) __TVOS_PROHIBITED;
 
 #endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
@@ -230,9 +190,8 @@
     An AVCaptureSession preset suitable for 352x288 video output.
  
  @discussion
-    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPreset352x288
-    to achieve CIF quality (352x288) output.
-*/
+    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPreset352x288 to achieve CIF quality (352x288) output.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionPreset352x288 NS_AVAILABLE(10_7, 5_0) __TVOS_PROHIBITED;
 
 /*!
@@ -241,9 +200,8 @@
     An AVCaptureSession preset suitable for 640x480 video output.
  
  @discussion
-    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPreset640x480
-    to achieve VGA quality (640x480) output.
-*/
+    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPreset640x480 to achieve VGA quality (640x480) output.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionPreset640x480 NS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED;
 
 #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
@@ -254,9 +212,8 @@
     An AVCaptureSession preset suitable for 960x540 video output.
  
  @discussion
-    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPreset960x540
-    to achieve quarter HD quality (960x540) output.
-*/
+    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPreset960x540 to achieve quarter HD quality (960x540) output.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionPreset960x540 NS_AVAILABLE(10_7, NA) __TVOS_PROHIBITED;
 
 #endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
@@ -267,9 +224,8 @@
     An AVCaptureSession preset suitable for 1280x720 video output.
  
  @discussion
-    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPreset1280x720
-    to achieve 1280x720 output.
-*/
+    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPreset1280x720 to achieve 1280x720 output.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionPreset1280x720 NS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED;
 
 #if TARGET_OS_IPHONE
@@ -280,9 +236,8 @@
     An AVCaptureSession preset suitable for 1920x1080 video output.
  
  @discussion
-    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPreset1920x1080
-    to achieve 1920x1080 output.
-*/
+    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPreset1920x1080 to achieve 1920x1080 output.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionPreset1920x1080 NS_AVAILABLE(NA, 5_0) __TVOS_PROHIBITED;
 
 /*!
@@ -291,9 +246,8 @@
     An AVCaptureSession preset suitable for 3840x2160 (UHD 4K) video output.
 
  @discussion
-    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPreset3840x2160
-    to achieve 3840x2160 output.
-*/
+    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPreset3840x2160 to achieve 3840x2160 output.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionPreset3840x2160 NS_AVAILABLE(NA, 9_0) __TVOS_PROHIBITED;
 
 #endif // TARGET_OS_IPHONE
@@ -304,10 +258,8 @@
     An AVCaptureSession preset producing 960x540 Apple iFrame video and audio content.
 
 @discussion
-    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPresetiFrame960x540
-    to achieve 960x540 quality iFrame H.264 video at ~30 Mbits/sec with AAC audio.  QuickTime
-    movies captured in iFrame format are optimal for editing applications.
-*/
+    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPresetiFrame960x540 to achieve 960x540 quality iFrame H.264 video at ~30 Mbits/sec with AAC audio. QuickTime movies captured in iFrame format are optimal for editing applications.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionPresetiFrame960x540 NS_AVAILABLE(10_9, 5_0) __TVOS_PROHIBITED;
 
 /*!
@@ -316,10 +268,8 @@
     An AVCaptureSession preset producing 1280x720 Apple iFrame video and audio content.
 
 @discussion
-    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPresetiFrame1280x720
-    to achieve 1280x720 quality iFrame H.264 video at ~40 Mbits/sec with AAC audio.  QuickTime
-    movies captured in iFrame format are optimal for editing applications.
-*/
+    Clients may set an AVCaptureSession instance's sessionPreset to AVCaptureSessionPresetiFrame1280x720 to achieve 1280x720 quality iFrame H.264 video at ~40 Mbits/sec with AAC audio. QuickTime movies captured in iFrame format are optimal for editing applications.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionPresetiFrame1280x720 NS_AVAILABLE(10_9, 5_0) __TVOS_PROHIBITED;
 
 /*!
@@ -328,16 +278,8 @@
     An AVCaptureSession preset indicating that the formats of the session's inputs are being given priority.
 
 @discussion
-    By calling -setSessionPreset:, clients can easily configure an AVCaptureSession to produce a desired 
-    quality of service level.  The session configures its inputs and outputs optimally to produce the
-    QoS level indicated.  Clients who need to ensure a particular input format is chosen can use
-    AVCaptureDevice's -setActiveFormat: method.  When a client sets the active format on a device, the
-    associated session's -sessionPreset property automatically changes to AVCaptureSessionPresetInputPriority.
-    This change indicates that the input format selected by the client now dictates the quality of service 
-    level provided at the outputs.  When a client sets the session preset to anything other than 
-    AVCaptureSessionPresetInputPriority, the session resumes responsibility for configuring inputs and outputs,
-    and is free to change its inputs' activeFormat as needed.
-*/
+    By calling -setSessionPreset:, clients can easily configure an AVCaptureSession to produce a desired quality of service level. The session configures its inputs and outputs optimally to produce the QoS level indicated. Clients who need to ensure a particular input format is chosen can use AVCaptureDevice's -setActiveFormat: method. When a client sets the active format on a device, the associated session's -sessionPreset property automatically changes to AVCaptureSessionPresetInputPriority. This change indicates that the input format selected by the client now dictates the quality of service level provided at the outputs. When a client sets the session preset to anything other than AVCaptureSessionPresetInputPriority, the session resumes responsibility for configuring inputs and outputs, and is free to change its inputs' activeFormat as needed.
+ */
 AVF_EXPORT NSString *const AVCaptureSessionPresetInputPriority NS_AVAILABLE(NA, 7_0) __TVOS_PROHIBITED;
 
 @class AVCaptureInput;
@@ -351,12 +293,8 @@
     AVCaptureSession is the central hub of the AVFoundation capture classes.
  
  @discussion
-    To perform a real-time capture, a client may instantiate AVCaptureSession and add appropriate
-    AVCaptureInputs, such as AVCaptureDeviceInput, and outputs, such as AVCaptureMovieFileOutput.
-    [AVCaptureSession startRunning] starts the flow of data from the inputs to the outputs, and 
-    [AVCaptureSession stopRunning] stops the flow.  A client may set the sessionPreset property to 
-    customize the quality level or bitrate of the output.
-*/
+    To perform a real-time capture, a client may instantiate AVCaptureSession and add appropriate AVCaptureInputs, such as AVCaptureDeviceInput, and outputs, such as AVCaptureMovieFileOutput. [AVCaptureSession startRunning] starts the flow of data from the inputs to the outputs, and [AVCaptureSession stopRunning] stops the flow. A client may set the sessionPreset property to customize the quality level or bitrate of the output.
+ */
 NS_CLASS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED
 @interface AVCaptureSession : NSObject 
 {
@@ -375,11 +313,8 @@
     YES if the receiver can be set to the given preset, NO otherwise.
  
  @discussion
-    An AVCaptureSession instance can be associated with a preset that configures its inputs and outputs to fulfill common
-    use cases. This method can be used to determine if the receiver supports the desired preset given its
-    current input and output configuration.  The receiver's sessionPreset property may only be 
-    set to a certain preset if this method returns YES for that preset.
-*/
+    An AVCaptureSession instance can be associated with a preset that configures its inputs and outputs to fulfill common use cases. This method can be used to determine if the receiver supports the desired preset given its current input and output configuration. The receiver's sessionPreset property may only be set to a certain preset if this method returns YES for that preset.
+ */
 - (BOOL)canSetSessionPreset:(NSString*)preset;
 
 /*!
@@ -388,10 +323,8 @@
     Indicates the session preset currently in use by the receiver.
  
  @discussion
-    The value of this property is an NSString (one of AVCaptureSessionPreset*) indicating 
-    the current session preset in use by the receiver.  The sessionPreset property may be set 
-    while the receiver is running.
-*/
+    The value of this property is an NSString (one of AVCaptureSessionPreset*) indicating the current session preset in use by the receiver. The sessionPreset property may be set while the receiver is running.
+ */
 @property(nonatomic, copy) NSString *sessionPreset;
 
 /*!
@@ -400,9 +333,8 @@
     An NSArray of AVCaptureInputs currently added to the receiver.
 
  @discussion
-    The value of this property is an NSArray of AVCaptureInputs currently added to
-    the receiver.  Clients can add AVCaptureInputs to a session by calling -addInput:.
-*/
+    The value of this property is an NSArray of AVCaptureInputs currently added to the receiver. Clients can add AVCaptureInputs to a session by calling -addInput:.
+ */
 @property(nonatomic, readonly) NSArray *inputs;
 
 /*!
@@ -416,9 +348,8 @@
     YES if the proposed input can be added to the receiver, NO otherwise.
  
  @discussion
-    An AVCaptureInput instance can only be added to a session using -addInput: if
-    canAddInput: returns YES.
-*/
+    An AVCaptureInput instance can only be added to a session using -addInput: if -canAddInput: returns YES.
+ */
 - (BOOL)canAddInput:(AVCaptureInput *)input;
 
 /*!
@@ -430,9 +361,8 @@
     An AVCaptureInput instance.
  
  @discussion
-    An AVCaptureInput instance can only be added to a session using -addInput: if
-    canAddInput: returns YES.  -addInput: may be called while the session is running.
-*/
+    An AVCaptureInput instance can only be added to a session using -addInput: if -canAddInput: returns YES. -addInput: may be called while the session is running.
+ */
 - (void)addInput:(AVCaptureInput *)input;
 
 /*!
@@ -445,7 +375,7 @@
  
  @discussion
     -removeInput: may be called while the session is running.
-*/
+ */
 - (void)removeInput:(AVCaptureInput *)input;
 
 /*!
@@ -454,9 +384,8 @@
     An NSArray of AVCaptureOutputs currently added to the receiver.
 
  @discussion
-    The value of this property is an NSArray of AVCaptureOutputs currently added to
-    the receiver.  Clients can add AVCaptureOutputs to a session by calling -addOutput:.
-*/
+    The value of this property is an NSArray of AVCaptureOutputs currently added to the receiver. Clients can add AVCaptureOutputs to a session by calling -addOutput:.
+ */
 @property(nonatomic, readonly) NSArray *outputs;
 
 /*!
@@ -470,9 +399,8 @@
     YES if the proposed output can be added to the receiver, NO otherwise.
  
  @discussion
-    An AVCaptureOutput instance can only be added to a session using -addOutput: if
-    canAddOutput: returns YES.
-*/
+    An AVCaptureOutput instance can only be added to a session using -addOutput: if -canAddOutput: returns YES.
+ */
 - (BOOL)canAddOutput:(AVCaptureOutput *)output;
 
 /*!
@@ -484,9 +412,8 @@
     An AVCaptureOutput instance.
  
  @discussion
-    An AVCaptureOutput instance can only be added to a session using -addOutput: if
-    canAddOutput: returns YES.  -addOutput: may be called while the session is running.
-*/
+    An AVCaptureOutput instance can only be added to a session using -addOutput: if -canAddOutput: returns YES. -addOutput: may be called while the session is running.
+ */
 - (void)addOutput:(AVCaptureOutput *)output;
 
 /*!
@@ -499,7 +426,7 @@
  
  @discussion
     -removeOutput: may be called while the session is running.
-*/
+ */
 - (void)removeOutput:(AVCaptureOutput *)output;
 
 /*!
@@ -511,11 +438,8 @@
     An AVCaptureInput instance.
  
  @discussion
-    -addInputWithNoConnections: may be called while the session is running.
-    The -addInput: method is the preferred method for adding an input to an
-    AVCaptureSession.  -addInputWithNoConnections: may be called if you need 
-    fine-grained control over which inputs are connected to which outputs.
-*/
+    -addInputWithNoConnections: may be called while the session is running. The -addInput: method is the preferred method for adding an input to an AVCaptureSession. -addInputWithNoConnections: may be called if you need fine-grained control over which inputs are connected to which outputs.
+ */
 - (void)addInputWithNoConnections:(AVCaptureInput *)input NS_AVAILABLE(10_7, 8_0);
 
 /*!
@@ -527,11 +451,8 @@
     An AVCaptureOutput instance.
  
  @discussion
-    -addOutputWithNoConnections: may be called while the session is running.
-    The -addOutput: method is the preferred method for adding an output to an
-    AVCaptureSession.  -addOutputWithNoConnections: may be called if you need 
-    fine-grained control over which inputs are connected to which outputs.
-*/
+    -addOutputWithNoConnections: may be called while the session is running. The -addOutput: method is the preferred method for adding an output to an AVCaptureSession. -addOutputWithNoConnections: may be called if you need fine-grained control over which inputs are connected to which outputs.
+ */
 - (void)addOutputWithNoConnections:(AVCaptureOutput *)output NS_AVAILABLE(10_7, 8_0);
 
 /*!
@@ -543,12 +464,8 @@
     An AVCaptureConnection instance.
  
  @discussion
-    An AVCaptureConnection instance can only be added to a session using -addConnection:
-    if canAddConnection: returns YES.  When using -addInput: or -addOutput:, connections
-    are formed automatically between all compatible inputs and outputs.  Manually
-    adding connections is only necessary when adding an input or output with
-    no connections.
-*/
+    An AVCaptureConnection instance can only be added to a session using -addConnection: if canAddConnection: returns YES. When using -addInput: or -addOutput:, connections are formed automatically between all compatible inputs and outputs. Manually adding connections is only necessary when adding an input or output with no connections.
+ */
 - (BOOL)canAddConnection:(AVCaptureConnection *)connection NS_AVAILABLE(10_7, 8_0);
 
 /*!
@@ -560,12 +477,8 @@
     An AVCaptureConnection instance.
  
  @discussion
-    An AVCaptureConnection instance can only be added to a session using -addConnection:
-    if canAddConnection: returns YES.  When using -addInput: or -addOutput:, connections
-    are formed automatically between all compatible inputs and outputs.  Manually
-    adding connections is only necessary when adding an input or output with
-    no connections.  -addConnection: may be called while the session is running.
-*/
+    An AVCaptureConnection instance can only be added to a session using -addConnection: if canAddConnection: returns YES. When using -addInput: or -addOutput:, connections are formed automatically between all compatible inputs and outputs. Manually adding connections is only necessary when adding an input or output with no connections. -addConnection: may be called while the session is running.
+ */
 - (void)addConnection:(AVCaptureConnection *)connection NS_AVAILABLE(10_7, 8_0);
 
 /*!
@@ -578,41 +491,27 @@
  
  @discussion
     -removeConnection: may be called while the session is running.
-*/
+ */
 - (void)removeConnection:(AVCaptureConnection *)connection NS_AVAILABLE(10_7, 8_0);
 
 /*!
  @method beginConfiguration
  @abstract
-    When paired with commitConfiguration, allows a client to batch multiple configuration
-    operations on a running session into atomic updates.
+    When paired with commitConfiguration, allows a client to batch multiple configuration operations on a running session into atomic updates.
 
  @discussion
-    -beginConfiguration / -commitConfiguration are AVCaptureSession's mechanism
-    for batching multiple configuration operations on a running session into atomic
-    updates.  After calling [session beginConfiguration], clients may add or remove
-    outputs, alter the sessionPreset, or configure individual AVCaptureInput or Output
-    properties.  All changes will be pended until the client calls [session commitConfiguration],
-    at which time they will be applied together.  -beginConfiguration / -commitConfiguration
-    pairs may be nested, and will only be applied when the outermost commit is invoked.
-*/
+    -beginConfiguration / -commitConfiguration are AVCaptureSession's mechanism for batching multiple configuration operations on a running session into atomic updates. After calling [session beginConfiguration], clients may add or remove outputs, alter the sessionPreset, or configure individual AVCaptureInput or Output properties. All changes will be pended until the client calls [session commitConfiguration], at which time they will be applied together. -beginConfiguration / -commitConfiguration pairs may be nested, and will only be applied when the outermost commit is invoked.
+ */
 - (void)beginConfiguration;
 
 /*!
  @method commitConfiguration
  @abstract
-    When preceded by beginConfiguration, allows a client to batch multiple configuration
-    operations on a running session into atomic updates.
+    When preceded by beginConfiguration, allows a client to batch multiple configuration operations on a running session into atomic updates.
 
  @discussion
-    -beginConfiguration / -commitConfiguration are AVCaptureSession's mechanism
-    for batching multiple configuration operations on a running session into atomic
-    updates.  After calling [session beginConfiguration], clients may add or remove
-    outputs, alter the sessionPreset, or configure individual AVCaptureInput or Output
-    properties.  All changes will be pended until the client calls [session commitConfiguration],
-    at which time they will be applied together.  -beginConfiguration / -commitConfiguration
-    pairs may be nested, and will only be applied when the outermost commit is invoked.
-*/
+    -beginConfiguration / -commitConfiguration are AVCaptureSession's mechanism for batching multiple configuration operations on a running session into atomic updates. After calling [session beginConfiguration], clients may add or remove outputs, alter the sessionPreset, or configure individual AVCaptureInput or Output properties. All changes will be pended until the client calls [session commitConfiguration], at which time they will be applied together. -beginConfiguration / -commitConfiguration pairs may be nested, and will only be applied when the outermost commit is invoked.
+ */
 - (void)commitConfiguration;
 
 /*!
@@ -621,10 +520,8 @@
     Indicates whether the session is currently running.
  
  @discussion
-    The value of this property is a BOOL indicating whether the receiver is running.
-    Clients can key value observe the value of this property to be notified when
-    the session automatically starts or stops running.
-*/
+    The value of this property is a BOOL indicating whether the receiver is running. Clients can key value observe the value of this property to be notified when the session automatically starts or stops running.
+ */
 @property(nonatomic, readonly, getter=isRunning) BOOL running;
 
 
@@ -636,11 +533,8 @@
     Indicates whether the session is being interrupted.
  
  @discussion
-    The value of this property is a BOOL indicating whether the receiver is currently
-    being interrupted, such as by a phone call or alarm. Clients can key value observe 
-    the value of this property to be notified when the session ceases to be interrupted
-    and again has access to needed hardware resources.
-*/
+    The value of this property is a BOOL indicating whether the receiver is currently being interrupted, such as by a phone call or alarm. Clients can key value observe the value of this property to be notified when the session ceases to be interrupted and again has access to needed hardware resources.
+ */
 @property(nonatomic, readonly, getter=isInterrupted) BOOL interrupted NS_AVAILABLE_IOS(4_0);
 
 /*!
@@ -649,14 +543,8 @@
     Indicates whether the receiver will use the application's AVAudioSession for recording.
  
  @discussion
-    The value of this property is a BOOL indicating whether the receiver is currently
-    using the application's AVAudioSession (see AVAudioSession.h).  Prior to iOS 7, AVCaptureSession
-    uses its own audio session, which can lead to unwanted interruptions when interacting with
-    the application's audio session. In applications linked on or after iOS 7, AVCaptureSession
-    shares the application's audio session, allowing for simultaneous play back and recording
-    without unwanted interruptions.  Clients desiring the pre-iOS 7 behavior may opt out
-    by setting usesApplicationAudioSession to NO.  The default value is YES.
-*/
+    The value of this property is a BOOL indicating whether the receiver is currently using the application's AVAudioSession (see AVAudioSession.h). Prior to iOS 7, AVCaptureSession uses its own audio session, which can lead to unwanted interruptions when interacting with the application's audio session. In applications linked on or after iOS 7, AVCaptureSession shares the application's audio session, allowing for simultaneous play back and recording without unwanted interruptions. Clients desiring the pre-iOS 7 behavior may opt out by setting usesApplicationAudioSession to NO. The default value is YES.
+ */
 @property(nonatomic) BOOL usesApplicationAudioSession NS_AVAILABLE_IOS(7_0);
 
 /*!
@@ -665,15 +553,20 @@
     Indicates whether the receiver should configure the application's audio session for recording.
  
  @discussion
-    The value of this property is a BOOL indicating whether the receiver should configure the
-    application's audio session when needed for optimal recording.  When set to YES, the receiver
-    ensures the application's audio session is set to the PlayAndRecord category, and picks an appropriate
-    microphone and polar pattern to match the video camera being used. When set to NO, and -usesApplicationAudioSession
-    is set to YES, the receiver will use the application's audio session, but will not change any of its properties.  If
-    the session is not set up correctly for input, audio recording may fail. The default value is YES.
-*/
+    The value of this property is a BOOL indicating whether the receiver should configure the application's audio session when needed for optimal recording. When set to YES, the receiver ensures the application's audio session is set to the PlayAndRecord category, and picks an appropriate microphone and polar pattern to match the video camera being used. When set to NO, and -usesApplicationAudioSession is set to YES, the receiver will use the application's audio session, but will not change any of its properties. If the session is not set up correctly for input, audio recording may fail. The default value is YES.
+ */
 @property(nonatomic) BOOL automaticallyConfiguresApplicationAudioSession NS_AVAILABLE_IOS(7_0);
 
+/*!
+ @property automaticallyConfiguresCaptureDeviceForWideColor
+ @abstract
+    Indicates whether the receiver automatically configures its video device's activeFormat and activeColorSpace properties, preferring wide color for photos.
+ 
+ @discussion
+    The default value is YES. By default, the receiver automatically adjusts its source video AVCaptureDevice's activeFormat and activeColorSpace properties based on the supportedColorSpaces of the device's formats and the current AVCaptureSession topology. Wide color spaces are preferred over sRGB if an AVCapturePhotoOutput is present in the session. If you wish to set AVCaptureDevice's activeColorSpace manually, and prevent the AVCaptureSession from undoing your work, you must set automaticallyConfiguresCaptureDeviceForWideColor to NO. If the receiver's sessionPreset is set to AVCaptureSessionPresetInputPriority, the session will not alter the capture device's activeFormat, but might still alter its activeColorSpace.
+ */
+@property(nonatomic) BOOL automaticallyConfiguresCaptureDeviceForWideColor NS_AVAILABLE_IOS(10_0);
+
 #endif // TARGET_OS_IPHONE
 
 /*!
@@ -682,11 +575,8 @@
     Starts an AVCaptureSession instance running.
 
  @discussion
-    Clients invoke -startRunning to start the flow of data from inputs to outputs connected to 
-    the AVCaptureSession instance.  This call blocks until the session object has completely
-    started up or failed.  A failure to start running is reported through the AVCaptureSessionRuntimeErrorNotification
-    mechanism.
-*/
+    Clients invoke -startRunning to start the flow of data from inputs to outputs connected to the AVCaptureSession instance. This call blocks until the session object has completely started up or failed. A failure to start running is reported through the AVCaptureSessionRuntimeErrorNotification mechanism.
+ */
 - (void)startRunning;
 
 /*!
@@ -695,30 +585,26 @@
     Stops an AVCaptureSession instance that is currently running.
 
  @discussion
-    Clients invoke -stopRunning to stop the flow of data from inputs to outputs connected to 
-    the AVCaptureSession instance.  This call blocks until the session object has completely
-    stopped.
-*/
+    Clients invoke -stopRunning to stop the flow of data from inputs to outputs connected to the AVCaptureSession instance. This call blocks until the session object has completely stopped.
+ */
 - (void)stopRunning;
 
 /*!
  @property masterClock
  @abstract
-	Provides the master clock being used for output synchronization.
+    Provides the master clock being used for output synchronization.
  @discussion
-	The masterClock is readonly. Use masterClock to synchronize AVCaptureOutput data with external data sources (e.g motion samples). 
-	All capture output sample buffer timestamps are on the masterClock timebase.
+    The masterClock is readonly. Use masterClock to synchronize AVCaptureOutput data with external data sources (e.g motion samples). All capture output sample buffer timestamps are on the masterClock timebase.
 	
-	For example, if you want to reverse synchronize the output timestamps to the original timestamps, you can do the following:
-	In captureOutput:didOutputSampleBuffer:fromConnection:
+    For example, if you want to reverse synchronize the output timestamps to the original timestamps, you can do the following: In captureOutput:didOutputSampleBuffer:fromConnection:
  
-	AVCaptureInputPort *port = [[connection inputPorts] objectAtIndex:0];
-	CMClockRef originalClock = [port clock];
+    AVCaptureInputPort *port = [[connection inputPorts] objectAtIndex:0];
+    CMClockRef originalClock = [port clock];
  
-	CMTime syncedPTS = CMSampleBufferGetPresentationTime( sampleBuffer );
-	CMTime originalPTS = CMSyncConvertTime( syncedPTS, [session masterClock], originalClock );
+    CMTime syncedPTS = CMSampleBufferGetPresentationTime( sampleBuffer );
+    CMTime originalPTS = CMSyncConvertTime( syncedPTS, [session masterClock], originalClock );
  
-	This property is key-value observable.
+    This property is key-value observable.
  */
 @property(nonatomic, readonly) __attribute__((NSObject)) CMClockRef masterClock NS_AVAILABLE(10_9, 7_0);
 
@@ -729,8 +615,7 @@
 /*!
  @enum AVVideoFieldMode
  @abstract
-    Constants indicating video field mode, for use with AVCaptureConnection's videoFieldMode
-    property (see below).
+    Constants indicating video field mode, for use with AVCaptureConnection's videoFieldMode property (see below).
  
  @constant AVVideoFieldModeBoth
     Indicates that both top and bottom video fields in interlaced content should be passed thru.
@@ -740,7 +625,7 @@
     Indicates that the bottom video field only in interlaced content should be passed thru.
  @constant AVVideoFieldModeDeinterlace
     Indicates that top and bottom video fields in interlaced content should be deinterlaced.
-*/
+ */
 typedef NS_ENUM(NSInteger, AVVideoFieldMode) {
     AVVideoFieldModeBoth        = 0,
     AVVideoFieldModeTopOnly     = 1,
@@ -757,24 +642,15 @@
 /*!
  @class AVCaptureConnection
  @abstract
-    AVCaptureConnection represents a connection between an AVCaptureInputPort or ports, and an AVCaptureOutput or 
-    AVCaptureVideoPreviewLayer present in an AVCaptureSession.
+    AVCaptureConnection represents a connection between an AVCaptureInputPort or ports, and an AVCaptureOutput or AVCaptureVideoPreviewLayer present in an AVCaptureSession.
  
  @discussion
-    AVCaptureInputs have one or more AVCaptureInputPorts.  AVCaptureOutputs can accept
-    data from one or more sources (example - an AVCaptureMovieFileOutput accepts both video and audio data).
-    AVCaptureVideoPreviewLayers can accept data from one AVCaptureInputPort whose mediaType is
-    AVMediaTypeVideo. When an input or output is added to a session, or a video preview layer is
-    associated with a session, the session greedily forms connections between all the compatible AVCaptureInputs' 
-    ports and AVCaptureOutputs or AVCaptureVideoPreviewLayers.  Iterating through an output's connections or a
-    video preview layer's sole connection, a client may enable or disable the flow of data from a given input 
-    to a given output or preview layer.
+    AVCaptureInputs have one or more AVCaptureInputPorts. AVCaptureOutputs can accept data from one or more sources (example - an AVCaptureMovieFileOutput accepts both video and audio data). AVCaptureVideoPreviewLayers can accept data from one AVCaptureInputPort whose mediaType is AVMediaTypeVideo. When an input or output is added to a session, or a video preview layer is associated with a session, the session greedily forms connections between all the compatible AVCaptureInputs' ports and AVCaptureOutputs or AVCaptureVideoPreviewLayers. Iterating through an output's connections or a video preview layer's sole connection, a client may enable or disable the flow of data from a given input to a given output or preview layer.
      
-    Connections involving audio expose an array of AVCaptureAudioChannel objects, which can be used for
-    monitoring levels.
+    Connections involving audio expose an array of AVCaptureAudioChannel objects, which can be used for monitoring levels.
 
     Connections involving video expose video specific properties, such as videoMirrored and videoOrientation.
-*/
+ */
 NS_CLASS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED
 @interface AVCaptureConnection : NSObject 
 {
@@ -785,71 +661,52 @@
 /*!
  @method connectionWithInputPorts:output:
  @abstract
-    Returns an AVCaptureConnection instance describing a connection between the specified inputPorts 
-    and the specified output.
+    Returns an AVCaptureConnection instance describing a connection between the specified inputPorts and the specified output.
  
  @param ports
     An array of AVCaptureInputPort objects associated with AVCaptureInput objects.
  @param output
     An AVCaptureOutput object.
  @result
-    An AVCaptureConnection instance joining the specified inputPorts to the specified
-    output port.
+    An AVCaptureConnection instance joining the specified inputPorts to the specified output port.
  
  @discussion
-    This method returns an instance of AVCaptureConnection that may be subsequently added to an
-    AVCaptureSession instance using AVCaptureSession's -addConnection: method.  When using 
-    -addInput: or -addOutput:, connections are formed between all compatible inputs and outputs
-    automatically.  You do not need to manually create and add connections to the session unless
-    you use the primitive -addInputWithNoConnections: or -addOutputWithNoConnections: methods.
-*/
+    This method returns an instance of AVCaptureConnection that may be subsequently added to an AVCaptureSession instance using AVCaptureSession's -addConnection: method. When using -addInput: or -addOutput:, connections are formed between all compatible inputs and outputs automatically. You do not need to manually create and add connections to the session unless you use the primitive -addInputWithNoConnections: or -addOutputWithNoConnections: methods.
+ */
 + (instancetype)connectionWithInputPorts:(NSArray *)ports output:(AVCaptureOutput *)output NS_AVAILABLE(10_7, 8_0);
 
 /*!
  @method connectionWithInputPort:videoPreviewLayer:
  @abstract
-    Returns an AVCaptureConnection instance describing a connection between the specified inputPort 
-    and the specified AVCaptureVideoPreviewLayer instance.
+    Returns an AVCaptureConnection instance describing a connection between the specified inputPort and the specified AVCaptureVideoPreviewLayer instance.
  
  @param port
     An AVCaptureInputPort object associated with an AVCaptureInput object.
  @param layer
     An AVCaptureVideoPreviewLayer object.
  @result
-    An AVCaptureConnection instance joining the specified inputPort to the specified
-    video preview layer.
+    An AVCaptureConnection instance joining the specified inputPort to the specified video preview layer.
  
  @discussion
-    This method returns an instance of AVCaptureConnection that may be subsequently added to an
-    AVCaptureSession instance using AVCaptureSession's -addConnection: method.  When using 
-    AVCaptureVideoPreviewLayer's -initWithSession: or -setSession:, a connection is formed between 
-    the first compatible input port and the video preview layer automatically.  You do not need to 
-    manually create and add connections to the session unless you use AVCaptureVideoPreviewLayer's 
-    primitive -initWithSessionWithNoConnection: or -setSessionWithNoConnection: methods.
-*/
+    This method returns an instance of AVCaptureConnection that may be subsequently added to an AVCaptureSession instance using AVCaptureSession's -addConnection: method. When using AVCaptureVideoPreviewLayer's -initWithSession: or -setSession:, a connection is formed between the first compatible input port and the video preview layer automatically. You do not need to manually create and add connections to the session unless you use AVCaptureVideoPreviewLayer's primitive -initWithSessionWithNoConnection: or -setSessionWithNoConnection: methods.
+ */
 + (instancetype)connectionWithInputPort:(AVCaptureInputPort *)port videoPreviewLayer:(AVCaptureVideoPreviewLayer *)layer NS_AVAILABLE(10_7, 8_0);
 
 /*!
  @method initWithInputPorts:output:
  @abstract
-    Returns an AVCaptureConnection instance describing a connection between the specified inputPorts 
-    and the specified output.
+    Returns an AVCaptureConnection instance describing a connection between the specified inputPorts and the specified output.
  
  @param ports
     An array of AVCaptureInputPort objects associated with AVCaptureInput objects.
  @param output
     An AVCaptureOutput object.
  @result
-    An AVCaptureConnection instance joining the specified inputPorts to the specified
-    output port.
+    An AVCaptureConnection instance joining the specified inputPorts to the specified output port.
  
  @discussion
-    This method returns an instance of AVCaptureConnection that may be subsequently added to an
-    AVCaptureSession instance using AVCaptureSession's -addConnection: method.  When using 
-    -addInput: or -addOutput:, connections are formed between all compatible inputs and outputs
-    automatically.  You do not need to manually create and add connections to the session unless
-    you use the primitive -addInputWithNoConnections: or -addOutputWithNoConnections: methods.
-*/
+    This method returns an instance of AVCaptureConnection that may be subsequently added to an AVCaptureSession instance using AVCaptureSession's -addConnection: method. When using -addInput: or -addOutput:, connections are formed between all compatible inputs and outputs automatically. You do not need to manually create and add connections to the session unless you use the primitive -addInputWithNoConnections: or -addOutputWithNoConnections: methods.
+ */
 - (instancetype)initWithInputPorts:(NSArray *)ports output:(AVCaptureOutput *)output NS_AVAILABLE(10_7, 8_0);
 
 /*!
@@ -863,17 +720,11 @@
  @param layer
     An AVCaptureVideoPreviewLayer object.
  @result
-    An AVCaptureConnection instance joining the specified inputPort to the specified
-    video preview layer.
+    An AVCaptureConnection instance joining the specified inputPort to the specified video preview layer.
  
  @discussion
-    This method returns an instance of AVCaptureConnection that may be subsequently added to an
-    AVCaptureSession instance using AVCaptureSession's -addConnection: method.  When using 
-    AVCaptureVideoPreviewLayer's -initWithSession: or -setSession:, a connection is formed between 
-    the first compatible input port and the video preview layer automatically.  You do not need to 
-    manually create and add connections to the session unless you use AVCaptureVideoPreviewLayer's 
-    primitive -initWithSessionWithNoConnection: or -setSessionWithNoConnection: methods.
-*/
+    This method returns an instance of AVCaptureConnection that may be subsequently added to an AVCaptureSession instance using AVCaptureSession's -addConnection: method. When using AVCaptureVideoPreviewLayer's -initWithSession: or -setSession:, a connection is formed between the first compatible input port and the video preview layer automatically. You do not need to manually create and add connections to the session unless you use AVCaptureVideoPreviewLayer's primitive -initWithSessionWithNoConnection: or -setSessionWithNoConnection: methods.
+ */
 - (instancetype)initWithInputPort:(AVCaptureInputPort *)port videoPreviewLayer:(AVCaptureVideoPreviewLayer *)layer NS_AVAILABLE(10_7, 8_0);
 
 /*!
@@ -882,10 +733,8 @@
     An array of AVCaptureInputPort instances providing data through this connection.
 
  @discussion
-    An AVCaptureConnection may involve one or more AVCaptureInputPorts producing data
-    to the connection's AVCaptureOutput.  This property is read-only.  An AVCaptureConnection's
-    inputPorts remain static for the life of the object.  
-*/
+    An AVCaptureConnection may involve one or more AVCaptureInputPorts producing data to the connection's AVCaptureOutput. This property is read-only. An AVCaptureConnection's inputPorts remain static for the life of the object.
+ */
 @property(nonatomic, readonly) NSArray *inputPorts;
 
 /*!
@@ -894,11 +743,8 @@
     The AVCaptureOutput instance consuming data from this connection's inputPorts.
 
  @discussion
-    An AVCaptureConnection may involve one or more AVCaptureInputPorts producing data
-    to the connection's AVCaptureOutput.  This property is read-only.  An AVCaptureConnection's
-    output remains static for the life of the object.  Note that a connection can either
-    be to an output or a video preview layer, but never to both.
-*/
+    An AVCaptureConnection may involve one or more AVCaptureInputPorts producing data to the connection's AVCaptureOutput. This property is read-only. An AVCaptureConnection's output remains static for the life of the object. Note that a connection can either be to an output or a video preview layer, but never to both.
+ */
 @property(nonatomic, readonly) AVCaptureOutput *output;
 
 /*!
@@ -907,11 +753,8 @@
     The AVCaptureVideoPreviewLayer instance consuming data from this connection's inputPort.
  
  @discussion
-    An AVCaptureConnection may involve one AVCaptureInputPort producing data
-    to an AVCaptureVideoPreviewLayer object.  This property is read-only.  An AVCaptureConnection's
-    videoPreviewLayer remains static for the life of the object. Note that a connection can either
-    be to an output or a video preview layer, but never to both.
-*/
+    An AVCaptureConnection may involve one AVCaptureInputPort producing data to an AVCaptureVideoPreviewLayer object. This property is read-only. An AVCaptureConnection's videoPreviewLayer remains static for the life of the object. Note that a connection can either be to an output or a video preview layer, but never to both.
+ */
 @property(nonatomic, readonly) AVCaptureVideoPreviewLayer *videoPreviewLayer NS_AVAILABLE(10_7, 6_0);
 
 /*!
@@ -920,37 +763,28 @@
     Indicates whether the connection's output should consume data.
 
  @discussion
-    The value of this property is a BOOL that determines whether the receiver's output should consume data 
-    from its connected inputPorts when a session is running. Clients can set this property to stop the 
-    flow of data to a given output during capture.  The default value is YES.  
-*/
+    The value of this property is a BOOL that determines whether the receiver's output should consume data from its connected inputPorts when a session is running. Clients can set this property to stop the flow of data to a given output during capture. The default value is YES.
+ */
 @property(nonatomic, getter=isEnabled) BOOL enabled;
 
 /*!
  @property active
  @abstract
-    Indicates whether the receiver's output is currently capable of consuming
-    data through this connection.
+    Indicates whether the receiver's output is currently capable of consuming data through this connection.
 
  @discussion
-    The value of this property is a BOOL that determines whether the receiver's output
-    can consume data provided through this connection.  This property is read-only.  Clients
-    may key-value observe this property to know when a session's configuration forces a
-    connection to become inactive.  The default value is YES.  
-*/
+    The value of this property is a BOOL that determines whether the receiver's output can consume data provided through this connection. This property is read-only. Clients may key-value observe this property to know when a session's configuration forces a connection to become inactive. The default value is YES.
+ */
 @property(nonatomic, readonly, getter=isActive) BOOL active;
 
 /*!
  @property audioChannels
  @abstract
-    An array of AVCaptureAudioChannel objects representing individual channels of
-    audio data flowing through the connection.
+    An array of AVCaptureAudioChannel objects representing individual channels of audio data flowing through the connection.
 
  @discussion
-    This property is only applicable to AVCaptureConnection instances involving
-    audio.  In such connections, the audioChannels array contains one AVCaptureAudioChannel
-    object for each channel of audio data flowing through this connection.
-*/
+    This property is only applicable to AVCaptureConnection instances involving audio. In such connections, the audioChannels array contains one AVCaptureAudioChannel object for each channel of audio data flowing through this connection.
+ */
 @property(nonatomic, readonly) NSArray *audioChannels;
 
 /*!
@@ -959,37 +793,29 @@
     Indicates whether the connection supports setting the videoMirrored property.
 
  @discussion
-    This property is only applicable to AVCaptureConnection instances involving
-    video.  In such connections, the videoMirrored property may only be set if
+    This property is only applicable to AVCaptureConnection instances involving video. In such connections, the videoMirrored property may only be set if
     -isVideoMirroringSupported returns YES.
-*/
+ */
 @property(nonatomic, readonly, getter=isVideoMirroringSupported) BOOL supportsVideoMirroring;
 
 /*!
  @property videoMirrored
  @abstract
-    Indicates whether the video flowing through the connection should be mirrored
-    about its vertical axis.
+    Indicates whether the video flowing through the connection should be mirrored about its vertical axis.
 
  @discussion
-    This property is only applicable to AVCaptureConnection instances involving
-    video.  if -isVideoMirroringSupported returns YES, videoMirrored may be set
-    to flip the video about its vertical axis and produce a mirror-image effect.
-*/
+    This property is only applicable to AVCaptureConnection instances involving video. if -isVideoMirroringSupported returns YES, videoMirrored may be set to flip the video about its vertical axis and produce a mirror-image effect.
+ */
 @property(nonatomic, getter=isVideoMirrored) BOOL videoMirrored;
 
 /*!
  @property automaticallyAdjustsVideoMirroring
  @abstract
-    Specifies whether or not the value of @"videoMirrored" can change based on configuration
-    of the session.
+    Specifies whether or not the value of @"videoMirrored" can change based on configuration of the session.
 	
  @discussion		
-    For some session configurations, video data flowing through the connection will be mirrored 
-    by default.  When the value of this property is YES, the value of @"videoMirrored" may change 
-    depending on the configuration of the session, for example after switching to a different AVCaptureDeviceInput.
-    The default value is YES.
-*/
+    For some session configurations, video data flowing through the connection will be mirrored by default. When the value of this property is YES, the value of @"videoMirrored" may change depending on the configuration of the session, for example after switching to a different AVCaptureDeviceInput. The default value is YES.
+ */
 @property (nonatomic) BOOL automaticallyAdjustsVideoMirroring NS_AVAILABLE(10_7, 6_0);
 
 /*!
@@ -998,27 +824,18 @@
     Indicates whether the connection supports setting the videoOrientation property.
 
  @discussion
-    This property is only applicable to AVCaptureConnection instances involving
-    video.  In such connections, the videoOrientation property may only be set if
-    -isVideoOrientationSupported returns YES.
-*/
+    This property is only applicable to AVCaptureConnection instances involving video. In such connections, the videoOrientation property may only be set if -isVideoOrientationSupported returns YES.
+ */
 @property(nonatomic, readonly, getter=isVideoOrientationSupported) BOOL supportsVideoOrientation;
 
 /*!
  @property videoOrientation
  @abstract
-    Indicates whether the video flowing through the connection should be rotated
-    to a given orientation.
+    Indicates whether the video flowing through the connection should be rotated to a given orientation.
 
  @discussion
-    This property is only applicable to AVCaptureConnection instances involving
-    video.  If -isVideoOrientationSupported returns YES, videoOrientation may be set
-    to rotate the video buffers being consumed by the connection's output.  Note that
-    setting videoOrientation does not necessarily result in a physical rotation of
-    video buffers.  For instance, a video connection to an AVCaptureMovieFileOutput
-    handles orientation using a Quicktime track matrix.  In the AVCaptureStillImageOutput,
-    orientation is handled using Exif tags.
-*/
+    This property is only applicable to AVCaptureConnection instances involving video. If -isVideoOrientationSupported returns YES, videoOrientation may be set to rotate the video buffers being consumed by the connection's output. Note that setting videoOrientation does not necessarily result in a physical rotation of video buffers. For instance, a video connection to an AVCaptureMovieFileOutput handles orientation using a Quicktime track matrix. In the AVCaptureStillImageOutput, orientation is handled using Exif tags.
+ */
 @property(nonatomic) AVCaptureVideoOrientation videoOrientation;
 
 #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
@@ -1029,10 +846,8 @@
     Indicates whether the connection supports setting the videoFieldMode property.
  
  @discussion
-    This property is only applicable to AVCaptureConnection instances involving
-    video.  In such connections, the videoFieldMode property may only be set if
-    -isVideoFieldModeSupported returns YES.
-*/
+    This property is only applicable to AVCaptureConnection instances involving video. In such connections, the videoFieldMode property may only be set if -isVideoFieldModeSupported returns YES.
+ */
 @property(nonatomic, readonly, getter=isVideoFieldModeSupported) BOOL supportsVideoFieldMode NS_AVAILABLE(10_7, NA);
 
 /*!
@@ -1041,10 +856,8 @@
     Indicates how interlaced video flowing through the connection should be treated.
  
  @discussion
-    This property is only applicable to AVCaptureConnection instances involving
-    video.  If -isVideoFieldModeSupported returns YES, videoFieldMode may be set
-    to affect interlaced video content flowing through the connection.
-*/
+    This property is only applicable to AVCaptureConnection instances involving video. If -isVideoFieldModeSupported returns YES, videoFieldMode may be set to affect interlaced video content flowing through the connection.
+ */
 @property(nonatomic) AVVideoFieldMode videoFieldMode NS_AVAILABLE(10_7, NA);
 
 #endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
@@ -1055,15 +868,10 @@
     Indicates whether the connection supports setting the videoMinFrameDuration property.
  
  @discussion
-    This property is only applicable to AVCaptureConnection instances involving
-    video.  In such connections, the videoMinFrameDuration property may only be set if
-    -isVideoMinFrameDurationSupported returns YES.
- 
-    This property is deprecated on iOS, where min and max frame rate adjustments are applied
-    exclusively at the AVCaptureDevice using the activeVideoMinFrameDuration and activeVideoMaxFrameDuration
-    properties.  On Mac OS X, frame rate adjustments are supported both at the AVCaptureDevice
-    and at AVCaptureConnection, enabling connections to output different frame rates.
-*/
+    This property is only applicable to AVCaptureConnection instances involving video. In such connections, the videoMinFrameDuration property may only be set if -isVideoMinFrameDurationSupported returns YES.
+ 
+    This property is deprecated on iOS, where min and max frame rate adjustments are applied exclusively at the AVCaptureDevice using the activeVideoMinFrameDuration and activeVideoMaxFrameDuration properties. On Mac OS X, frame rate adjustments are supported both at the AVCaptureDevice and at AVCaptureConnection, enabling connections to output different frame rates.
+ */
 @property(nonatomic, readonly, getter=isVideoMinFrameDurationSupported) BOOL supportsVideoMinFrameDuration NS_DEPRECATED(10_7, NA, 5_0, 7_0, "Use AVCaptureDevice's activeFormat.videoSupportedFrameRateRanges instead.");
 
 /*!
@@ -1072,16 +880,10 @@
     Indicates the minimum time interval at which the receiver should output consecutive video frames.
  
  @discussion
-    The value of this property is a CMTime specifying the minimum duration of each video frame output by the receiver,
-    placing a lower bound on the amount of time that should separate consecutive frames. This is equivalent to
-    the reciprocal of the maximum frame rate. A value of kCMTimeZero or kCMTimeInvalid indicates an unlimited maximum frame
-    rate. The default value is kCMTimeInvalid.
- 
-    This property is deprecated on iOS, where min and max frame rate adjustments are applied
-    exclusively at the AVCaptureDevice using the activeVideoMinFrameDuration and activeVideoMaxFrameDuration
-    properties.  On Mac OS X, frame rate adjustments are supported both at the AVCaptureDevice
-    and at AVCaptureConnection, enabling connections to output different frame rates.
-*/
+    The value of this property is a CMTime specifying the minimum duration of each video frame output by the receiver, placing a lower bound on the amount of time that should separate consecutive frames. This is equivalent to the reciprocal of the maximum frame rate. A value of kCMTimeZero or kCMTimeInvalid indicates an unlimited maximum frame rate. The default value is kCMTimeInvalid.
+ 
+    This property is deprecated on iOS, where min and max frame rate adjustments are applied exclusively at the AVCaptureDevice using the activeVideoMinFrameDuration and activeVideoMaxFrameDuration properties. On Mac OS X, frame rate adjustments are supported both at the AVCaptureDevice and at AVCaptureConnection, enabling connections to output different frame rates.
+ */
 @property(nonatomic) CMTime videoMinFrameDuration NS_DEPRECATED(10_7, NA, 5_0, 7_0, "Use AVCaptureDevice's activeVideoMinFrameDuration instead.");
 
 /*!
@@ -1090,15 +892,10 @@
     Indicates whether the connection supports setting the videoMaxFrameDuration property.
  
  @discussion
-    This property is only applicable to AVCaptureConnection instances involving
-    video.  In such connections, the videoMaxFrameDuration property may only be set if
-    -isVideoMaxFrameDurationSupported returns YES.
- 
-	This property is deprecated on iOS, where min and max frame rate adjustments are applied
-	exclusively at the AVCaptureDevice using the activeVideoMinFrameDuration and activeVideoMaxFrameDuration
-	properties.  On Mac OS X, frame rate adjustments are supported both at the AVCaptureDevice
-	and at AVCaptureConnection, enabling connections to output different frame rates.
-*/
+    This property is only applicable to AVCaptureConnection instances involving video. In such connections, the videoMaxFrameDuration property may only be set if -isVideoMaxFrameDurationSupported returns YES.
+ 
+    This property is deprecated on iOS, where min and max frame rate adjustments are applied exclusively at the AVCaptureDevice using the activeVideoMinFrameDuration and activeVideoMaxFrameDuration properties. On Mac OS X, frame rate adjustments are supported both at the AVCaptureDevice and at AVCaptureConnection, enabling connections to output different frame rates.
+ */
 @property(nonatomic, readonly, getter=isVideoMaxFrameDurationSupported) BOOL supportsVideoMaxFrameDuration NS_DEPRECATED(10_9, NA, 5_0, 7_0, "Use AVCaptureDevice's activeFormat.videoSupportedFrameRateRanges instead.");
 
 /*!
@@ -1107,16 +904,10 @@
     Indicates the maximum time interval at which the receiver should output consecutive video frames.
  
  @discussion
-    The value of this property is a CMTime specifying the maximum duration of each video frame output by the receiver,
-    placing an upper bound on the amount of time that should separate consecutive frames. This is equivalent to
-    the reciprocal of the minimum frame rate. A value of kCMTimeZero or kCMTimeInvalid indicates an unlimited minimum frame
-    rate. The default value is kCMTimeInvalid.
- 
-	This property is deprecated on iOS, where min and max frame rate adjustments are applied
-	exclusively at the AVCaptureDevice using the activeVideoMinFrameDuration and activeVideoMaxFrameDuration
-	properties.  On Mac OS X, frame rate adjustments are supported both at the AVCaptureDevice
-	and at AVCaptureConnection, enabling connections to output different frame rates.
-*/
+    The value of this property is a CMTime specifying the maximum duration of each video frame output by the receiver, placing an upper bound on the amount of time that should separate consecutive frames. This is equivalent to the reciprocal of the minimum frame rate. A value of kCMTimeZero or kCMTimeInvalid indicates an unlimited minimum frame rate. The default value is kCMTimeInvalid.
+ 
+    This property is deprecated on iOS, where min and max frame rate adjustments are applied exclusively at the AVCaptureDevice using the activeVideoMinFrameDuration and activeVideoMaxFrameDuration properties. On Mac OS X, frame rate adjustments are supported both at the AVCaptureDevice and at AVCaptureConnection, enabling connections to output different frame rates.
+ */
 @property(nonatomic) CMTime videoMaxFrameDuration NS_DEPRECATED(10_9, NA, 5_0, 7_0, "Use AVCaptureDevice's activeVideoMaxFrameDuration instead.");
 
 #if TARGET_OS_IPHONE
@@ -1127,11 +918,8 @@
     Indicates the maximum video scale and crop factor supported by the receiver.
  
  @discussion
-    This property is only applicable to AVCaptureConnection instances involving
-    video.  In such connections, the videoMaxScaleAndCropFactor property specifies
-    the maximum CGFloat value that may be used when setting the videoScaleAndCropFactor
-    property.
-*/
+    This property is only applicable to AVCaptureConnection instances involving video. In such connections, the videoMaxScaleAndCropFactor property specifies the maximum CGFloat value that may be used when setting the videoScaleAndCropFactor property.
+ */
 @property(nonatomic, readonly) CGFloat videoMaxScaleAndCropFactor NS_AVAILABLE_IOS(5_0);
 
 /*!
@@ -1140,16 +928,10 @@
     Indicates the current video scale and crop factor in use by the receiver.
  
  @discussion
-    This property only applies to AVCaptureStillImageOutput connections.
-    In such connections, the videoScaleAndCropFactor property may be set
-    to a value in the range of 1.0 to videoMaxScaleAndCropFactor.  At a factor of
-    1.0, the image is its original size.  At a factor greater than 1.0, the image
-    is scaled by the factor and center-cropped to its original dimensions.
-    This factor is applied in addition to any magnification from AVCaptureDevice's
-    videoZoomFactor property.
+    This property only applies to AVCaptureStillImageOutput connections. In such connections, the videoScaleAndCropFactor property may be set to a value in the range of 1.0 to videoMaxScaleAndCropFactor. At a factor of 1.0, the image is its original size. At a factor greater than 1.0, the image is scaled by the factor and center-cropped to its original dimensions. This factor is applied in addition to any magnification from AVCaptureDevice's videoZoomFactor property.
  
  @see -[AVCaptureDevice videoZoomFactor]
-*/
+ */
 @property(nonatomic) CGFloat videoScaleAndCropFactor NS_AVAILABLE_IOS(5_0);
 
 /*!
@@ -1158,20 +940,8 @@
     Indicates the stabilization mode to apply to video flowing through the receiver when it is supported.
  
  @discussion
-    This property is only applicable to AVCaptureConnection instances involving video.
-    On devices where the video stabilization feature is supported, only a subset of available source
-    formats may be available for stabilization.  By setting the preferredVideoStabilizationMode
-    property to a value other than AVCaptureVideoStabilizationModeOff, video flowing through the receiver is stabilized
-    when the mode is available.  Enabling video stabilization introduces additional latency into the video capture pipeline and
-    may consume more system memory depending on the stabilization mode and format.  If the preferred stabilization mode isn't available,
-    the activeVideoStabilizationMode will be set to AVCaptureVideoStabilizationModeOff.  Clients may key-value observe the
-    activeVideoStabilizationMode property to know which stabilization mode is in use or when it is off.  The default value
-    is AVCaptureVideoStabilizationModeOff.  When setting this property to AVCaptureVideoStabilizationModeAuto, an appropriate
-    stabilization mode will be chosen based on the format and frame rate.  For apps linked before iOS 6.0, the default value
-    is AVCaptureVideoStabilizationModeStandard for a video connection attached to an AVCaptureMovieFileOutput instance.
-    For apps linked on or after iOS 6.0, the default value is always AVCaptureVideoStabilizationModeOff.  Setting a video stabilization
-    mode using this property may change the value of enablesVideoStabilizationWhenAvailable.
-*/
+    This property is only applicable to AVCaptureConnection instances involving video. On devices where the video stabilization feature is supported, only a subset of available source formats may be available for stabilization. By setting the preferredVideoStabilizationMode property to a value other than AVCaptureVideoStabilizationModeOff, video flowing through the receiver is stabilized when the mode is available. Enabling video stabilization introduces additional latency into the video capture pipeline and may consume more system memory depending on the stabilization mode and format. If the preferred stabilization mode isn't available, the activeVideoStabilizationMode will be set to AVCaptureVideoStabilizationModeOff. Clients may key-value observe the activeVideoStabilizationMode property to know which stabilization mode is in use or when it is off. The default value is AVCaptureVideoStabilizationModeOff. When setting this property to AVCaptureVideoStabilizationModeAuto, an appropriate stabilization mode will be chosen based on the format and frame rate. For apps linked before iOS 6.0, the default value is AVCaptureVideoStabilizationModeStandard for a video connection attached to an AVCaptureMovieFileOutput instance. For apps linked on or after iOS 6.0, the default value is always AVCaptureVideoStabilizationModeOff. Setting a video stabilization mode using this property may change the value of enablesVideoStabilizationWhenAvailable.
+ */
 @property(nonatomic) AVCaptureVideoStabilizationMode preferredVideoStabilizationMode NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -1180,12 +950,8 @@
     Indicates the stabilization mode currently being applied to video flowing through the receiver.
  
  @discussion
-    This property is only applicable to AVCaptureConnection instances involving video.
-    On devices where the video stabilization feature is supported, only a subset of available source formats may be stabilized.
-    The activeVideoStabilizationMode property returns a value other than AVCaptureVideoStabilizationModeOff
-    if video stabilization is currently in use.  This property never returns AVCaptureVideoStabilizationModeAuto.
-    This property is key-value observable.
-*/
+    This property is only applicable to AVCaptureConnection instances involving video. On devices where the video stabilization feature is supported, only a subset of available source formats may be stabilized. The activeVideoStabilizationMode property returns a value other than AVCaptureVideoStabilizationModeOff if video stabilization is currently in use. This property never returns AVCaptureVideoStabilizationModeAuto. This property is key-value observable.
+ */
 @property(nonatomic, readonly) AVCaptureVideoStabilizationMode activeVideoStabilizationMode NS_AVAILABLE_IOS(8_0);
 
 /*!
@@ -1194,14 +960,8 @@
     Indicates whether the connection supports video stabilization.
  
  @discussion
-    This property is only applicable to AVCaptureConnection instances involving video.
-    In such connections, the -enablesVideoStabilizationWhenAvailable property may only be set if
-    -supportsVideoStabilization returns YES.
-    This property returns YES if the connection's input device has one or more formats that support
-    video stabilization and the connection's output supports video stabilization.
-    See [AVCaptureDeviceFormat isVideoStabilizationModeSupported:] to check which video stabilization
-    modes are supported by the active device format.
-*/
+    This property is only applicable to AVCaptureConnection instances involving video. In such connections, the -enablesVideoStabilizationWhenAvailable property may only be set if -supportsVideoStabilization returns YES. This property returns YES if the connection's input device has one or more formats that support video stabilization and the connection's output supports video stabilization. See [AVCaptureDeviceFormat isVideoStabilizationModeSupported:] to check which video stabilization modes are supported by the active device format.
+ */
 @property(nonatomic, readonly, getter=isVideoStabilizationSupported) BOOL supportsVideoStabilization NS_AVAILABLE_IOS(6_0);
 
 /*!
@@ -1210,32 +970,18 @@
     Indicates whether stabilization is currently being applied to video flowing through the receiver.
  
  @discussion
-    This property is only applicable to AVCaptureConnection instances involving video.
-    On devices where the video stabilization feature is supported, only a subset of available source 
-    formats and resolutions may be available for stabilization.  The videoStabilizationEnabled 
-    property returns YES if video stabilization is currently in use.  This property is key-value
-    observable.  This property is deprecated.  Use activeVideoStabilizationMode instead.
-*/
+    This property is only applicable to AVCaptureConnection instances involving video. On devices where the video stabilization feature is supported, only a subset of available source formats and resolutions may be available for stabilization. The videoStabilizationEnabled property returns YES if video stabilization is currently in use. This property is key-value observable. This property is deprecated. Use activeVideoStabilizationMode instead.
+ */
 @property(nonatomic, readonly, getter=isVideoStabilizationEnabled) BOOL videoStabilizationEnabled NS_DEPRECATED_IOS(6_0, 8_0, "Use activeVideoStabilizationMode instead.");
 
 /*!
  @property enablesVideoStabilizationWhenAvailable;
  @abstract
-    Indicates whether stabilization should be applied to video flowing through the receiver
-    when the feature is available.
+    Indicates whether stabilization should be applied to video flowing through the receiver when the feature is available.
  
  @discussion
-    This property is only applicable to AVCaptureConnection instances involving video.
-    On devices where the video stabilization feature is supported, only a subset of available source 
-    formats and resolutions may be available for stabilization.  By setting the
-    enablesVideoStabilizationWhenAvailable property to YES, video flowing through the receiver
-    is stabilized when available.  Enabling video stabilization may introduce additional latency 
-    into the video capture pipeline.  Clients may key-value observe the videoStabilizationEnabled
-    property to know when stabilization is in use or not.  The default value is NO.
-    For apps linked before iOS 6.0, the default value is YES for a video connection attached to an 
-    AVCaptureMovieFileOutput instance.  For apps linked on or after iOS 6.0, the default value is
-    always NO.  This property is deprecated.  Use preferredVideoStabilizationMode instead.
-*/
+    This property is only applicable to AVCaptureConnection instances involving video. On devices where the video stabilization feature is supported, only a subset of available source formats and resolutions may be available for stabilization. By setting the enablesVideoStabilizationWhenAvailable property to YES, video flowing through the receiver is stabilized when available. Enabling video stabilization may introduce additional latency into the video capture pipeline. Clients may key-value observe the videoStabilizationEnabled property to know when stabilization is in use or not. The default value is NO. For apps linked before iOS 6.0, the default value is YES for a video connection attached to an AVCaptureMovieFileOutput instance. For apps linked on or after iOS 6.0, the default value is always NO. This property is deprecated. Use preferredVideoStabilizationMode instead.
+ */
 @property(nonatomic) BOOL enablesVideoStabilizationWhenAvailable NS_DEPRECATED_IOS(6_0, 8_0, "Use preferredVideoStabilizationMode instead.");
 
 #endif // TARGET_OS_IPHONE
@@ -1249,15 +995,11 @@
 /*!
  @class AVCaptureAudioChannel
  @abstract
-    AVCaptureAudioChannel represents a single channel of audio flowing through 
-    an AVCaptureSession.
+    AVCaptureAudioChannel represents a single channel of audio flowing through an AVCaptureSession.
  
  @discussion
-    An AVCaptureConnection from an input producing audio to an output receiving audio
-    exposes an array of AVCaptureAudioChannel objects, one for each channel of audio
-    available.  Iterating through these audio channel objects, a client may poll
-    for audio levels. Instances of AVCaptureAudioChannel cannot be created directly.
-*/
+    An AVCaptureConnection from an input producing audio to an output receiving audio exposes an array of AVCaptureAudioChannel objects, one for each channel of audio available. Iterating through these audio channel objects, a client may poll for audio levels. Instances of AVCaptureAudioChannel cannot be created directly.
+ */
 NS_CLASS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED
 @interface AVCaptureAudioChannel : NSObject
 {
@@ -1268,14 +1010,11 @@
 /*!
  @property averagePowerLevel
  @abstract
-    A measurement of the instantaneous average power level of the audio
-    flowing through the receiver.
+    A measurement of the instantaneous average power level of the audio flowing through the receiver.
 
  @discussion
-    A client may poll an AVCaptureAudioChannel object for its current
-    averagePowerLevel to get its instantaneous average power level in decibels.
-    This property is not key-value observable.
-*/
+    A client may poll an AVCaptureAudioChannel object for its current averagePowerLevel to get its instantaneous average power level in decibels. This property is not key-value observable.
+ */
 @property(nonatomic, readonly) float averagePowerLevel;
 
 /*!
@@ -1284,10 +1023,8 @@
     A measurement of the peak/hold level of the audio flowing through the receiver.
 
  @discussion
-    A client may poll an AVCaptureAudioChannel object for its current
-    peakHoldLevel to get its most recent peak hold level in decibels.
-    This property is not key-value observable.
-*/
+    A client may poll an AVCaptureAudioChannel object for its current peakHoldLevel to get its most recent peak hold level in decibels. This property is not key-value observable.
+ */
 @property(nonatomic, readonly) float peakHoldLevel;
 
 #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
@@ -1298,10 +1035,8 @@
     A property indicating the current volume (gain) of the receiver.
 
  @discussion
-    The volume property indicates the current volume or gain of the receiver as a floating
-    point value between 0.0 -> 1.0.  If you desire to boost the gain in software, you
-    may specify a a value greater than 1.0.
-*/
+    The volume property indicates the current volume or gain of the receiver as a floating point value between 0.0 -> 1.0. If you desire to boost the gain in software, you may specify a a value greater than 1.0.
+ */
 @property(nonatomic) float volume NS_AVAILABLE(10_7, NA);
 
 /*!
@@ -1310,9 +1045,8 @@
     A property indicating whether the receiver is currently enabled for data capture.
 
  @discussion
-    By default, all AVCaptureAudioChannel objects exposed by a connection are enabled.
-    You may set enabled to NO to stop the flow of data for a particular AVCaptureAudioChannel.
-*/
+    By default, all AVCaptureAudioChannel objects exposed by a connection are enabled. You may set enabled to NO to stop the flow of data for a particular AVCaptureAudioChannel.
+ */
 @property(nonatomic, getter=isEnabled) BOOL enabled NS_AVAILABLE(10_7, NA);
 
 #endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureStillImageOutput.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureStillImageOutput.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureStillImageOutput.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureStillImageOutput.h	2016-05-24 07:21:25.000000000 +0200
@@ -0,0 +1,285 @@
+/*
+    File:  AVCaptureStillImageOutput.h
+ 	
+ 	Framework:  AVFoundation
+ 
+	Copyright 2010-2016 Apple Inc. All rights reserved.
+*/
+
+#import <AVFoundation/AVCaptureOutput.h>
+
+#pragma mark - AVCaptureStillImageOutput
+
+@class AVCaptureStillImageOutputInternal;
+
+/*!
+ @class AVCaptureStillImageOutput
+ @abstract
+    AVCaptureStillImageOutput is a concrete subclass of AVCaptureOutput that can be used to capture high-quality still images with accompanying metadata.
+
+ @discussion
+    Instances of AVCaptureStillImageOutput can be used to capture, on demand, high quality snapshots from a realtime capture source. Clients can request a still image for the current time using the captureStillImageAsynchronouslyFromConnection:completionHandler: method. Clients can also configure still image outputs to produce still images in specific image formats.
+ */
+NS_CLASS_DEPRECATED(10_7, NA, 4_0, 10_0, "Use AVCapturePhotoOutput instead") __TVOS_PROHIBITED
+@interface AVCaptureStillImageOutput : AVCaptureOutput 
+{
+@private
+	AVCaptureStillImageOutputInternal *_internal;
+}
+
+/*!
+ @property outputSettings
+ @abstract
+    Specifies the options the receiver uses to encode still images before they are delivered.
+
+ @discussion
+    See AVVideoSettings.h for more information on how to construct an output settings dictionary.
+
+    On iOS, the only currently supported keys are AVVideoCodecKey and kCVPixelBufferPixelFormatTypeKey. Use -availableImageDataCVPixelFormatTypes and -availableImageDataCodecTypes to determine what codec keys and pixel formats are supported. AVVideoQualityKey is supported on iOS 6.0 and later and may only be used when AVVideoCodecKey is set to AVVideoCodecJPEG.
+ */
+@property(nonatomic, copy) NSDictionary *outputSettings;
+
+/*!
+ @property availableImageDataCVPixelFormatTypes
+ @abstract
+    Indicates the supported image pixel formats that can be specified in outputSettings.
+
+ @discussion
+    The value of this property is an NSArray of NSNumbers that can be used as values for the kCVPixelBufferPixelFormatTypeKey in the receiver's outputSettings property. The first format in the returned list is the most efficient output format.
+ */
+@property(nonatomic, readonly) NSArray *availableImageDataCVPixelFormatTypes;
+
+/*!
+ @property availableImageDataCodecTypes
+ @abstract
+    Indicates the supported image codec formats that can be specified in outputSettings.
+
+ @discussion
+    The value of this property is an NSArray of NSStrings that can be used as values for the AVVideoCodecKey in the receiver's outputSettings property.
+ */
+@property(nonatomic, readonly) NSArray *availableImageDataCodecTypes;
+
+#if TARGET_OS_IPHONE
+
+/*!
+ @property stillImageStabilizationSupported
+ @abstract
+    Indicates whether the receiver supports still image stabilization.
+ 
+ @discussion
+    The receiver's automaticallyEnablesStillImageStabilizationWhenAvailable property can only be set if this property returns YES. Its value may change as the session's -sessionPreset or input device's -activeFormat changes.
+ */
+@property(nonatomic, readonly, getter=isStillImageStabilizationSupported) BOOL stillImageStabilizationSupported NS_AVAILABLE_IOS(7_0);
+
+/*!
+ @property automaticallyEnablesStillImageStabilizationWhenAvailable
+ @abstract
+    Indicates whether the receiver should automatically use still image stabilization when necessary.
+ 
+ @discussion
+    On a receiver where -isStillImageStabilizationSupported returns YES, image stabilization may be applied to reduce blur commonly found in low light photos. When stabilization is enabled, still image captures incur additional latency. The default value is YES when supported, NO otherwise. Setting this property throws an NSInvalidArgumentException if -isStillImageStabilizationSupported returns NO.
+ */
+@property(nonatomic) BOOL automaticallyEnablesStillImageStabilizationWhenAvailable NS_AVAILABLE_IOS(7_0);
+
+/*!
+ @property stillImageStabilizationActive
+ @abstract
+    Indicates whether still image stabilization is in use for the current capture.
+ 
+ @discussion
+    On a receiver where -isStillImageStabilizationSupported returns YES, and automaticallyEnablesStillImageStabilizationWhenAvailable is set to YES, this property may be key-value observed, or queried from inside your key-value observation callback for the @"capturingStillImage" property, to find out if still image stabilization is being applied to the current capture.
+ */
+@property(nonatomic, readonly, getter=isStillImageStabilizationActive) BOOL stillImageStabilizationActive NS_AVAILABLE_IOS(7_0);
+
+/*!
+ @property highResolutionStillImageOutputEnabled
+ @abstract
+    Indicates whether the receiver should emit still images at the highest resolution supported by its source AVCaptureDevice's activeFormat.
+ 
+ @discussion
+    By default, AVCaptureStillImageOutput emits images with the same dimensions as its source AVCaptureDevice's activeFormat.formatDescription. However, if you set this property to YES, the receiver emits still images at its source AVCaptureDevice's activeFormat.highResolutionStillImageDimensions. Note that if you enable video stabilization (see AVCaptureConnection's preferredVideoStabilizationMode) for any output, the high resolution still images emitted by AVCaptureStillImageOutput may be smaller by 10 or more percent.
+ */
+@property(nonatomic, getter=isHighResolutionStillImageOutputEnabled) BOOL highResolutionStillImageOutputEnabled NS_AVAILABLE_IOS(8_0);
+
+#endif // TARGET_OS_IPHONE
+
+/*!
+ @property capturingStillImage
+ @abstract
+    A boolean value that becomes true when a still image is being captured.
+
+ @discussion
+    The value of this property is a BOOL that becomes true when a still image is being captured, and false when no still image capture is underway. This property is key-value observable.
+ */
+@property(readonly, getter=isCapturingStillImage) BOOL capturingStillImage NS_AVAILABLE(10_8, 5_0);
+
+/*!
+ @method captureStillImageAsynchronouslyFromConnection:completionHandler:
+ @abstract
+    Initiates an asynchronous still image capture, returning the result to a completion handler.
+
+ @param connection
+    The AVCaptureConnection object from which to capture the still image.
+ @param handler
+    A block that will be called when the still image capture is complete. The block will be passed a CMSampleBuffer object containing the image data or an NSError object if an image could not be captured.
+
+ @discussion
+    This method will return immediately after it is invoked, later calling the provided completion handler block when image data is ready. If the request could not be completed, the error parameter will contain an NSError object describing the failure.
+
+    Attachments to the image data sample buffer may contain metadata appropriate to the image data format. For instance, a sample buffer containing JPEG data may carry a kCGImagePropertyExifDictionary as an attachment. See <ImageIO/CGImageProperties.h> for a list of keys and value types.
+
+    Clients should not assume that the completion handler will be called on a specific thread.
+ 
+    Calls to captureStillImageAsynchronouslyFromConnection:completionHandler: are not synchronized with AVCaptureDevice manual control completion handlers. Setting a device manual control, waiting for its completion, then calling captureStillImageAsynchronouslyFromConnection:completionHandler: DOES NOT ensure that the still image returned reflects your manual control change. It may be from an earlier time. You can compare your manual control completion handler sync time to the returned still image's presentation time. You can retrieve the sample buffer's pts using CMSampleBufferGetPresentationTimestamp(). If the still image has an earlier timestamp, your manual control command does not apply to it.
+ */
+- (void)captureStillImageAsynchronouslyFromConnection:(AVCaptureConnection *)connection completionHandler:(void (^)(CMSampleBufferRef imageDataSampleBuffer, NSError *error))handler;
+
+/*!
+ @method jpegStillImageNSDataRepresentation:
+ @abstract
+    Converts the still image data and metadata attachments in a JPEG sample buffer to an NSData representation.
+
+ @param jpegSampleBuffer
+    The sample buffer carrying JPEG image data, optionally with Exif metadata sample buffer attachments. This method throws an NSInvalidArgumentException if jpegSampleBuffer is NULL or not in the JPEG format.
+
+ @discussion
+    This method returns an NSData representation of a JPEG still image sample buffer, merging the image data and Exif metadata sample buffer attachments without recompressing the image. The returned NSData is suitable for writing to disk.
+ */
++ (NSData *)jpegStillImageNSDataRepresentation:(CMSampleBufferRef)jpegSampleBuffer;
+
+@end
+
+#if TARGET_OS_IPHONE
+
+/*!
+ @class AVCaptureBracketedStillImageSettings
+ @abstract
+    AVCaptureBracketedStillImageSettings is an abstract base class that defines an interface for settings pertaining to a bracketed capture.
+ 
+ @discussion
+    AVCaptureBracketedStillImageSettings may not be instantiated directly.
+ */
+NS_CLASS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED
+@interface AVCaptureBracketedStillImageSettings : NSObject
+@end
+
+/*!
+ @class AVCaptureManualExposureBracketedStillImageSettings
+ @abstract
+    AVCaptureManualExposureBracketedStillImageSettings is a concrete subclass of AVCaptureBracketedStillImageSettings to be used when bracketing exposure duration and ISO.
+ 
+ @discussion
+    An AVCaptureManualExposureBracketedStillImageSettings instance defines the exposure duration and ISO settings that should be applied to one image in a bracket. An array of settings objects is passed to -[AVCaptureStillImageOutput captureStillImageBracketAsynchronouslyFromConnection:withSettingsArray:completionHandler:]. Min and max duration and ISO values are queryable properties of the AVCaptureDevice supplying data to an AVCaptureStillImageOutput instance. If you wish to leave exposureDuration unchanged for this bracketed still image, you may pass the special value AVCaptureExposureDurationCurrent. To keep ISO unchanged, you may pass AVCaptureISOCurrent (see AVCaptureDevice.h).
+ */
+NS_CLASS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED
+@interface AVCaptureManualExposureBracketedStillImageSettings : AVCaptureBracketedStillImageSettings
+
++ (instancetype)manualExposureSettingsWithExposureDuration:(CMTime)duration ISO:(float)ISO;
+
+@property(readonly) CMTime exposureDuration;
+@property(readonly) float ISO;
+
+@end
+
+/*!
+ @class AVCaptureAutoExposureBracketedStillImageSettings
+ @abstract
+    AVCaptureAutoExposureBracketedStillImageSettings is a concrete subclass of AVCaptureBracketedStillImageSettings to be used when bracketing exposure target bias.
+ 
+ @discussion
+    An AVCaptureAutoExposureBracketedStillImageSettings instance defines the exposure target bias setting that should be applied to one image in a bracket. An array of settings objects is passed to -[AVCaptureStillImageOutput captureStillImageBracketAsynchronouslyFromConnection:withSettingsArray:completionHandler:]. Min and max exposure target bias are queryable properties of the AVCaptureDevice supplying data to an AVCaptureStillImageOutput instance. If you wish to leave exposureTargetBias unchanged for this bracketed still image, you may pass the special value AVCaptureExposureTargetBiasCurrent (see AVCaptureDevice.h).
+ */
+NS_CLASS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED
+@interface AVCaptureAutoExposureBracketedStillImageSettings : AVCaptureBracketedStillImageSettings
+
++ (instancetype)autoExposureSettingsWithExposureTargetBias:(float)exposureTargetBias;
+
+@property(readonly) float exposureTargetBias;
+
+@end
+
+/*!
+ @category AVCaptureStillImageOutput (BracketedCaptureMethods)
+ @abstract
+    A category of methods for bracketed still image capture.
+ 
+ @discussion
+    A "still image bracket" is a batch of images taken as quickly as possible in succession, optionally with different settings from picture to picture.
+ 
+    In a bracketed capture, AVCaptureDevice flashMode property is ignored (flash is forced off), as is AVCaptureStillImageOutput's automaticallyEnablesStillImageStabilizationWhenAvailable property (stabilization is forced off).
+ */
+@interface AVCaptureStillImageOutput ( BracketedCaptureMethods )
+
+/*!
+ @property maxBracketedCaptureStillImageCount
+ @abstract
+    Specifies the maximum number of still images that may be taken in a single bracket.
+
+ @discussion
+    AVCaptureStillImageOutput can only satisfy a limited number of image requests in a single bracket without exhausting system resources. The maximum number of still images that may be taken in a single bracket depends on the size of the images being captured, and consequently may vary with AVCaptureSession -sessionPreset and AVCaptureDevice -activeFormat. Some formats do not support bracketed capture and return a maxBracketedCaptureStillImageCount of 0. This read-only property is key-value observable. If you exceed -maxBracketedCaptureStillImageCount, then -captureStillImageBracketAsynchronouslyFromConnection:withSettingsArray:completionHandler: fails and the completionHandler is called [settings count] times with a NULL sample buffer and AVErrorMaximumStillImageCaptureRequestsExceeded.
+ */
+@property(nonatomic, readonly) NSUInteger maxBracketedCaptureStillImageCount NS_AVAILABLE_IOS(8_0);
+
+/*!
+ @property lensStabilizationDuringBracketedCaptureSupported
+ @abstract
+    Indicates whether the receiver supports lens stabilization during bracketed captures.
+ 
+ @discussion
+    The receiver's lensStabilizationDuringBracketedCaptureEnabled property can only be set if this property returns YES. Its value may change as the session's -sessionPreset or input device's -activeFormat changes. This read-only property is key-value observable.
+ */
+@property(nonatomic, readonly, getter=isLensStabilizationDuringBracketedCaptureSupported) BOOL lensStabilizationDuringBracketedCaptureSupported NS_AVAILABLE_IOS(9_0);
+
+/*!
+ @property lensStabilizationDuringBracketedCaptureEnabled
+ @abstract
+    Indicates whether the receiver should use lens stabilization during bracketed captures.
+ 
+ @discussion
+    On a receiver where -isLensStabilizationDuringBracketedCaptureSupported returns YES, lens stabilization may be applied to the bracket to reduce blur commonly found in low light photos. When lens stabilization is enabled, bracketed still image captures incur additional latency. Lens stabilization is more effective with longer-exposure captures, and offers limited or no benefit for exposure durations shorter than 1/30 of a second. It is possible that during the bracket, the lens stabilization module may run out of correction range and therefore will not be active for every frame in the bracket. Each emitted CMSampleBuffer from the bracket will have an attachment of kCMSampleBufferAttachmentKey_StillImageLensStabilizationInfo indicating additional information about stabilization was applied to the buffer, if any. The default value of -isLensStabilizationDuringBracketedCaptureEnabled is NO. This value will be set to NO when -isLensStabilizationDuringBracketedCaptureSupported changes to NO. Setting this property throws an NSInvalidArgumentException if -isLensStabilizationDuringBracketedCaptureSupported returns NO. This property is key-value observable.
+ */
+@property(nonatomic, getter=isLensStabilizationDuringBracketedCaptureEnabled) BOOL lensStabilizationDuringBracketedCaptureEnabled NS_AVAILABLE_IOS(9_0);
+
+/*!
+ @method prepareToCaptureStillImageBracketFromConnection:withSettingsArray:completionHandler:
+ @abstract
+    Allows the receiver to prepare resources in advance of capturing a still image bracket.
+ 
+ @param connection
+    The connection through which the still image bracket should be captured.
+ 
+ @param settings
+    An array of AVCaptureBracketedStillImageSettings objects. All must be of the same kind of AVCaptureBracketedStillImageSettings subclass, or an NSInvalidArgumentException is thrown.
+ 
+ @param completionHandler
+    A user provided block that will be called asynchronously once resources have successfully been allocated for the specified bracketed capture operation. If sufficient resources could not be allocated, the "prepared" parameter contains NO, and "error" parameter contains a non-nil error value. If [settings count] exceeds -maxBracketedCaptureStillImageCount, then AVErrorMaximumStillImageCaptureRequestsExceeded is returned. You should not assume that the completion handler will be called on a specific thread.
+ 
+ @discussion
+    -maxBracketedCaptureStillImageCount tells you the maximum number of images that may be taken in a single bracket given the current AVCaptureDevice/AVCaptureSession/AVCaptureStillImageOutput configuration. But before taking a still image bracket, additional resources may need to be allocated. By calling -prepareToCaptureStillImageBracketFromConnection:withSettingsArray:completionHandler: first, you are able to deterministically know when the receiver is ready to capture the bracket with the specified settings array.
+
+ */
+- (void)prepareToCaptureStillImageBracketFromConnection:(AVCaptureConnection *)connection withSettingsArray:(NSArray *)settings completionHandler:(void (^)(BOOL prepared, NSError *error))handler NS_AVAILABLE_IOS(8_0);
+
+/*!
+ @method captureStillImageBracketAsynchronouslyFromConnection:withSettingsArray:completionHandler:
+ @abstract
+    Captures a still image bracket.
+ 
+ @param connection
+    The connection through which the still image bracket should be captured.
+ 
+ @param settings
+    An array of AVCaptureBracketedStillImageSettings objects. All must be of the same kind of AVCaptureBracketedStillImageSettings subclass, or an NSInvalidArgumentException is thrown.
+ 
+ @param completionHandler
+    A user provided block that will be called asynchronously as each still image in the bracket is captured. If the capture request is successful, the "sampleBuffer" parameter contains a valid CMSampleBuffer, the "stillImageSettings" parameter contains the settings object corresponding to this still image, and a nil "error" parameter. If the bracketed capture fails, sample buffer is NULL and error is non-nil. If [settings count] exceeds -maxBracketedCaptureStillImageCount, then AVErrorMaximumStillImageCaptureRequestsExceeded is returned. You should not assume that the completion handler will be called on a specific thread.
+ 
+ @discussion
+    If you have not called -prepareToCaptureStillImageBracketFromConnection:withSettingsArray:completionHandler: for this still image bracket request, the bracket may not be taken immediately, as the receiver may internally need to prepare resources.
+ */
+- (void)captureStillImageBracketAsynchronouslyFromConnection:(AVCaptureConnection *)connection withSettingsArray:(NSArray *)settings completionHandler:(void (^)(CMSampleBufferRef sampleBuffer, AVCaptureBracketedStillImageSettings *stillImageSettings, NSError *error))handler NS_AVAILABLE_IOS(8_0);
+
+@end
+
+#endif // TARGET_OS_IPHONE
+
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureVideoDataOutput.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureVideoDataOutput.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureVideoDataOutput.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureVideoDataOutput.h	2016-05-25 04:39:22.000000000 +0200
@@ -0,0 +1,195 @@
+/*
+    File:  AVCaptureVideoDataOutput.h
+ 	
+ 	Framework:  AVFoundation
+ 
+	Copyright 2010-2016 Apple Inc. All rights reserved.
+*/
+
+#import <AVFoundation/AVCaptureOutput.h>
+#import <CoreMedia/CMSampleBuffer.h>
+
+#pragma mark - AVCaptureVideoDataOutput
+
+@class AVCaptureVideoDataOutputInternal;
+@protocol AVCaptureVideoDataOutputSampleBufferDelegate;
+
+/*!
+ @class AVCaptureVideoDataOutput
+ @abstract
+    AVCaptureVideoDataOutput is a concrete subclass of AVCaptureOutput that can be used to process uncompressed or compressed frames from the video being captured.
+
+ @discussion
+    Instances of AVCaptureVideoDataOutput produce video frames suitable for processing using other media APIs. Applications can access the frames with the captureOutput:didOutputSampleBuffer:fromConnection: delegate method.
+ */
+NS_CLASS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED
+@interface AVCaptureVideoDataOutput : AVCaptureOutput 
+{
+@private
+	AVCaptureVideoDataOutputInternal *_internal;
+}
+
+/*!
+ @method setSampleBufferDelegate:queue:
+ @abstract
+    Sets the receiver's delegate that will accept captured buffers and dispatch queue on which the delegate will be called.
+
+ @param sampleBufferDelegate
+    An object conforming to the AVCaptureVideoDataOutputSampleBufferDelegate protocol that will receive sample buffers after they are captured.
+ @param sampleBufferCallbackQueue
+    A dispatch queue on which all sample buffer delegate methods will be called.
+
+ @discussion
+    When a new video sample buffer is captured it will be vended to the sample buffer delegate using the captureOutput:didOutputSampleBuffer:fromConnection: delegate method. All delegate methods will be called on the specified dispatch queue. If the queue is blocked when new frames are captured, those frames will be automatically dropped at a time determined by the value of the alwaysDiscardsLateVideoFrames property. This allows clients to process existing frames on the same queue without having to manage the potential memory usage increases that would otherwise occur when that processing is unable to keep up with the rate of incoming frames. If their frame processing is consistently unable to keep up with the rate of incoming frames, clients should consider using the minFrameDuration property, which will generally yield better performance characteristics and more consistent frame rates than frame dropping alone.
+
+    Clients that need to minimize the chances of frames being dropped should specify a queue on which a sufficiently small amount of processing is being done outside of receiving sample buffers. However, if such clients migrate extra processing to another queue, they are responsible for ensuring that memory usage does not grow without bound from frames that have not been processed.
+
+    A serial dispatch queue must be used to guarantee that video frames will be delivered in order. The sampleBufferCallbackQueue parameter may not be NULL, except when setting the sampleBufferDelegate to nil.
+ */
+- (void)setSampleBufferDelegate:(id<AVCaptureVideoDataOutputSampleBufferDelegate>)sampleBufferDelegate queue:(dispatch_queue_t)sampleBufferCallbackQueue;
+
+/*!
+ @property sampleBufferDelegate
+ @abstract
+    The receiver's delegate.
+
+ @discussion
+    The value of this property is an object conforming to the AVCaptureVideoDataOutputSampleBufferDelegate protocol that will receive sample buffers after they are captured. The delegate is set using the setSampleBufferDelegate:queue: method.
+ */
+@property(nonatomic, readonly) id<AVCaptureVideoDataOutputSampleBufferDelegate> sampleBufferDelegate;
+
+/*!
+ @property sampleBufferCallbackQueue
+ @abstract
+    The dispatch queue on which all sample buffer delegate methods will be called.
+
+ @discussion
+    The value of this property is a dispatch_queue_t. The queue is set using the setSampleBufferDelegate:queue: method.
+ */
+@property(nonatomic, readonly) dispatch_queue_t sampleBufferCallbackQueue;
+
+/*!
+ @property videoSettings
+ @abstract
+    Specifies the settings used to decode or re-encode video before it is output by the receiver.
+
+ @discussion
+    See AVVideoSettings.h for more information on how to construct a video settings dictionary. To receive samples in their device native format, set this property to an empty dictionary (i.e. [NSDictionary dictionary]). To receive samples in a default uncompressed format, set this property to nil. Note that after this property is set to nil, subsequent querying of this property will yield a non-nil dictionary reflecting the settings used by the AVCaptureSession's current sessionPreset.
+
+    On iOS, the only supported key is kCVPixelBufferPixelFormatTypeKey. Supported pixel formats are kCVPixelFormatType_420YpCbCr8BiPlanarVideoRange, kCVPixelFormatType_420YpCbCr8BiPlanarFullRange and kCVPixelFormatType_32BGRA.
+ */
+@property(nonatomic, copy) NSDictionary *videoSettings;
+
+/*!
+ @method recommendedVideoSettingsForAssetWriterWithOutputFileType:
+ @abstract
+    Specifies the recommended settings for use with an AVAssetWriterInput.
+
+ @param outputFileType
+    Specifies the UTI of the file type to be written (see AVMediaFormat.h for a list of file format UTIs).
+ 
+ @return
+    A fully populated dictionary of keys and values that are compatible with AVAssetWriter.
+ 
+ @discussion
+    The value of this property is an NSDictionary containing values for compression settings keys defined in AVVideoSettings.h. This dictionary is suitable for use as the "outputSettings" parameter when creating an AVAssetWriterInput, such as,
+        
+       [AVAssetWriterInput assetWriterInputWithMediaType:AVMediaTypeVideo outputSettings:outputSettings sourceFormatHint:hint];
+    
+    The dictionary returned contains all necessary keys and values needed by AVAssetWriter (see AVAssetWriterInput.h, -initWithMediaType:outputSettings: for a more in depth discussion). For QuickTime movie and ISO file types, the recommended video settings will produce output comparable to that of AVCaptureMovieFileOutput.
+
+    Note that the dictionary of settings is dependent on the current configuration of the receiver's AVCaptureSession and its inputs. The settings dictionary may change if the session's configuration changes. As such, you should configure your session first, then query the recommended video settings. As of iOS 8.3, movies produced with these settings successfully import into the iOS camera roll and sync to and from like devices via iTunes.
+ */
+- (NSDictionary *)recommendedVideoSettingsForAssetWriterWithOutputFileType:(NSString *)outputFileType NS_AVAILABLE_IOS(7_0);
+
+/*!
+ @property availableVideoCVPixelFormatTypes
+ @abstract
+    Indicates the supported video pixel formats that can be specified in videoSettings.
+
+ @discussion
+    The value of this property is an NSArray of NSNumbers that can be used as values for the kCVPixelBufferPixelFormatTypeKey in the receiver's videoSettings property. The first format in the returned list is the most efficient output format.
+ */
+@property(nonatomic, readonly) NSArray *availableVideoCVPixelFormatTypes NS_AVAILABLE(10_7, 5_0);
+
+/*!
+ @property availableVideoCodecTypes
+ @abstract
+    Indicates the supported video codec formats that can be specified in videoSettings.
+
+ @discussion
+    The value of this property is an NSArray of NSStrings that can be used as values for the AVVideoCodecKey in the receiver's videoSettings property.
+ */
+@property(nonatomic, readonly) NSArray *availableVideoCodecTypes NS_AVAILABLE(10_7, 5_0);
+
+/*!
+ @property minFrameDuration
+ @abstract
+    Specifies the minimum time interval between which the receiver should output consecutive video frames.
+
+ @discussion
+    The value of this property is a CMTime specifying the minimum duration of each video frame output by the receiver, placing a lower bound on the amount of time that should separate consecutive frames. This is equivalent to the inverse of the maximum frame rate. A value of kCMTimeZero or kCMTimeInvalid indicates an unlimited maximum frame rate. The default value is kCMTimeInvalid. As of iOS 5.0, minFrameDuration is deprecated. Use AVCaptureConnection's videoMinFrameDuration property instead.
+ */
+@property(nonatomic) CMTime minFrameDuration NS_DEPRECATED_IOS(4_0, 5_0, "Use AVCaptureConnection's videoMinFrameDuration property instead.");
+
+/*!
+ @property alwaysDiscardsLateVideoFrames
+ @abstract
+    Specifies whether the receiver should always discard any video frame that is not processed before the next frame is captured.
+
+ @discussion
+    When the value of this property is YES, the receiver will immediately discard frames that are captured while the dispatch queue handling existing frames is blocked in the captureOutput:didOutputSampleBuffer:fromConnection: delegate method. When the value of this property is NO, delegates will be allowed more time to process old frames before new frames are discarded, but application memory usage may increase significantly as a result. The default value is YES.
+ */
+@property(nonatomic) BOOL alwaysDiscardsLateVideoFrames;
+
+@end
+
+/*!
+ @protocol AVCaptureVideoDataOutputSampleBufferDelegate
+ @abstract
+    Defines an interface for delegates of AVCaptureVideoDataOutput to receive captured video sample buffers and be notified of late sample buffers that were dropped.
+ */
+__TVOS_PROHIBITED
+@protocol AVCaptureVideoDataOutputSampleBufferDelegate <NSObject>
+
+@optional
+
+/*!
+ @method captureOutput:didOutputSampleBuffer:fromConnection:
+ @abstract
+    Called whenever an AVCaptureVideoDataOutput instance outputs a new video frame.
+
+ @param captureOutput
+    The AVCaptureVideoDataOutput instance that output the frame.
+ @param sampleBuffer
+    A CMSampleBuffer object containing the video frame data and additional information about the frame, such as its format and presentation time.
+ @param connection
+    The AVCaptureConnection from which the video was received.
+
+ @discussion
+    Delegates receive this message whenever the output captures and outputs a new video frame, decoding or re-encoding it as specified by its videoSettings property. Delegates can use the provided video frame in conjunction with other APIs for further processing. This method will be called on the dispatch queue specified by the output's sampleBufferCallbackQueue property. This method is called periodically, so it must be efficient to prevent capture performance problems, including dropped frames.
+
+    Clients that need to reference the CMSampleBuffer object outside of the scope of this method must CFRetain it and then CFRelease it when they are finished with it.
+
+    Note that to maintain optimal performance, some sample buffers directly reference pools of memory that may need to be reused by the device system and other capture inputs. This is frequently the case for uncompressed device native capture where memory blocks are copied as little as possible. If multiple sample buffers reference such pools of memory for too long, inputs will no longer be able to copy new samples into memory and those samples will be dropped. If your application is causing samples to be dropped by retaining the provided CMSampleBuffer objects for too long, but it needs access to the sample data for a long period of time, consider copying the data into a new buffer and then calling CFRelease on the sample buffer if it was previously retained so that the memory it references can be reused.
+ */
+- (void)captureOutput:(AVCaptureOutput *)captureOutput didOutputSampleBuffer:(CMSampleBufferRef)sampleBuffer fromConnection:(AVCaptureConnection *)connection;
+
+/*!
+ @method captureOutput:didDropSampleBuffer:fromConnection:
+ @abstract
+    Called once for each frame that is discarded.
+
+ @param captureOutput
+    The AVCaptureVideoDataOutput instance that dropped the frame.
+ @param sampleBuffer
+    A CMSampleBuffer object containing information about the dropped frame, such as its format and presentation time. This sample buffer will contain none of the original video data.
+ @param connection
+    The AVCaptureConnection from which the dropped video frame was received.
+
+ @discussion
+    Delegates receive this message whenever a video frame is dropped. This method is called once for each dropped frame. The CMSampleBuffer object passed to this delegate method will contain metadata about the dropped video frame, such as its duration and presentation time stamp, but will contain no actual video data. On iOS, Included in the sample buffer attachments is the kCMSampleBufferAttachmentKey_DroppedFrameReason, which indicates why the frame was dropped. This method will be called on the dispatch queue specified by the output's sampleBufferCallbackQueue property. Because this method will be called on the same dispatch queue that is responsible for outputting video frames, it must be efficient to prevent further capture performance problems, such as additional dropped video frames.
+  */
+- (void)captureOutput:(AVCaptureOutput *)captureOutput didDropSampleBuffer:(CMSampleBufferRef)sampleBuffer fromConnection:(AVCaptureConnection *)connection NS_AVAILABLE(10_7, 6_0);
+
+@end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureVideoPreviewLayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureVideoPreviewLayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureVideoPreviewLayer.h	2015-09-30 23:18:01.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCaptureVideoPreviewLayer.h	2016-05-25 04:39:22.000000000 +0200
@@ -20,14 +20,8 @@
     A CoreAnimation layer subclass for previewing the visual output of an AVCaptureSession.
 
  @discussion		
-    An AVCaptureVideoPreviewLayer instance is a subclass of CALayer and is therefore
-    suitable for insertion in a layer hierarchy as part of a graphical interface.
-    One creates an AVCaptureVideoPreviewLayer instance with the capture session to be
-    previewed, using +layerWithSession: or -initWithSession:.  Using the @"videoGravity"
-    property, one can influence how content is viewed relative to the layer bounds.  On
-    some hardware configurations, the orientation of the layer can be manipulated using
-    @"orientation" and @"mirrored".
-*/
+    An AVCaptureVideoPreviewLayer instance is a subclass of CALayer and is therefore suitable for insertion in a layer hierarchy as part of a graphical interface. One creates an AVCaptureVideoPreviewLayer instance with the capture session to be previewed, using +layerWithSession: or -initWithSession:. Using the @"videoGravity" property, one can influence how content is viewed relative to the layer bounds. On some hardware configurations, the orientation of the layer can be manipulated using @"orientation" and @"mirrored".
+ */
 NS_CLASS_AVAILABLE(10_7, 4_0) __TVOS_PROHIBITED
 @interface AVCaptureVideoPreviewLayer : CALayer
 {
@@ -38,59 +32,49 @@
 /*!
  @method layerWithSession:
  @abstract
-    Creates an AVCaptureVideoPreviewLayer for previewing the visual output of the
-    specified AVCaptureSession.
+    Creates an AVCaptureVideoPreviewLayer for previewing the visual output of the specified AVCaptureSession.
 
  @param session
     The AVCaptureSession instance to be previewed.
  @result
     A newly initialized AVCaptureVideoPreviewLayer instance.
-*/
+ */
 + (instancetype)layerWithSession:(AVCaptureSession *)session;
 
 /*!
  @method initWithSession:
  @abstract
-    Creates an AVCaptureVideoPreviewLayer for previewing the visual output of the
-    specified AVCaptureSession.
+    Creates an AVCaptureVideoPreviewLayer for previewing the visual output of the specified AVCaptureSession.
 
  @param session
     The AVCaptureSession instance to be previewed.
  @result
     A newly initialized AVCaptureVideoPreviewLayer instance.
-*/
+ */
 - (instancetype)initWithSession:(AVCaptureSession *)session;
 
 /*!
  @method layerWithSessionWithNoConnection:
  @abstract
-    Creates an AVCaptureVideoPreviewLayer for previewing the visual output of the
-    specified AVCaptureSession, but creates no connections to any of the session's
-    eligible video inputs.  Only use this initializer if you intend to manually 
-    form a connection between a desired AVCaptureInputPort and the receiver using 
-    AVCaptureSession's -addConnection: method.
+    Creates an AVCaptureVideoPreviewLayer for previewing the visual output of the specified AVCaptureSession, but creates no connections to any of the session's eligible video inputs. Only use this initializer if you intend to manually form a connection between a desired AVCaptureInputPort and the receiver using AVCaptureSession's -addConnection: method.
  
  @param session
     The AVCaptureSession instance to be previewed.
  @result
     A newly initialized AVCaptureVideoPreviewLayer instance.
-*/
+ */
 + (instancetype)layerWithSessionWithNoConnection:(AVCaptureSession *)session NS_AVAILABLE(10_7, 8_0);
 
 /*!
  @method initWithSessionWithNoConnection:
  @abstract
-    Creates an AVCaptureVideoPreviewLayer for previewing the visual output of the
-    specified AVCaptureSession, but creates no connections to any of the session's
-    eligible video inputs.  Only use this initializer if you intend to manually 
-    form a connection between a desired AVCaptureInputPort and the receiver using 
-    AVCaptureSession's -addConnection: method.
+    Creates an AVCaptureVideoPreviewLayer for previewing the visual output of the specified AVCaptureSession, but creates no connections to any of the session's eligible video inputs. Only use this initializer if you intend to manually form a connection between a desired AVCaptureInputPort and the receiver using AVCaptureSession's -addConnection: method.
  
  @param session
     The AVCaptureSession instance to be previewed.
  @result
     A newly initialized AVCaptureVideoPreviewLayer instance.
-*/
+ */
 - (instancetype)initWithSessionWithNoConnection:(AVCaptureSession *)session NS_AVAILABLE(10_7, 8_0);
 
 /*!
@@ -100,34 +84,27 @@
 
  @discussion
     The session is retained by the preview layer.
-*/
+ */
 @property (nonatomic, retain) AVCaptureSession *session;
 
 /*!
  method setSessionWithNoConnection:
  @abstract
-    Attaches the receiver to a given session without implicitly forming a
-    connection to the first eligible video AVCaptureInputPort.  Only use this 
-    setter if you intend to manually form a connection between a desired 
-    AVCaptureInputPort and the receiver using AVCaptureSession's -addConnection:
-    method.
+    Attaches the receiver to a given session without implicitly forming a connection to the first eligible video AVCaptureInputPort. Only use this setter if you intend to manually form a connection between a desired AVCaptureInputPort and the receiver using AVCaptureSession's -addConnection: method.
  
  @discussion
     The session is retained by the preview layer.
-*/
+ */
 - (void)setSessionWithNoConnection:(AVCaptureSession *)session NS_AVAILABLE(10_7, 8_0);
 
 /*!
  @property connection
  @abstract
-    The AVCaptureConnection instance describing the AVCaptureInputPort to which
-    the receiver is connected.
+    The AVCaptureConnection instance describing the AVCaptureInputPort to which the receiver is connected.
  
  @discussion
-    When calling initWithSession: or setSession: with a valid AVCaptureSession instance, 
-    a connection is formed to the first eligible video AVCaptureInput.  If the receiver 
-    is detached from a session, the connection property becomes nil.
-*/
+    When calling initWithSession: or setSession: with a valid AVCaptureSession instance, a connection is formed to the first eligible video AVCaptureInput. If the receiver is detached from a session, the connection property becomes nil.
+ */
 @property (nonatomic, readonly) AVCaptureConnection *connection NS_AVAILABLE(10_7, 6_0);
 
 /*!
@@ -136,90 +113,68 @@
     A string defining how the video is displayed within an AVCaptureVideoPreviewLayer bounds rect.
 
  @discussion
-    Options are AVLayerVideoGravityResize, AVLayerVideoGravityResizeAspect 
-    and AVLayerVideoGravityResizeAspectFill. AVLayerVideoGravityResizeAspect is default.
-    See <AVFoundation/AVAnimation.h> for a description of these options.
-*/
+    Options are AVLayerVideoGravityResize, AVLayerVideoGravityResizeAspect and AVLayerVideoGravityResizeAspectFill. AVLayerVideoGravityResizeAspect is default. See <AVFoundation/AVAnimation.h> for a description of these options.
+ */
 @property (copy) NSString *videoGravity;
 
 /*!
  @method captureDevicePointOfInterestForPoint:
  @abstract
-    Converts a point in layer coordinates to a point of interest in the coordinate space of the capture device providing
-    input to the layer.
+    Converts a point in layer coordinates to a point of interest in the coordinate space of the capture device providing input to the layer.
 
  @param pointInLayer
     A CGPoint in layer coordinates.
-
  @result
     A CGPoint in the coordinate space of the capture device providing input to the layer.
 
  @discussion
-    AVCaptureDevice pointOfInterest is expressed as a CGPoint where {0,0} represents the top left of the picture area,
-    and {1,1} represents the bottom right on an unrotated picture.  This convenience method converts a point in 
-    the coordinate space of the receiver to a point of interest in the coordinate space of the AVCaptureDevice providing
-    input to the receiver.  The conversion takes frameSize and videoGravity into consideration.
-*/
+    AVCaptureDevice pointOfInterest is expressed as a CGPoint where {0,0} represents the top left of the picture area, and {1,1} represents the bottom right on an unrotated picture. This convenience method converts a point in the coordinate space of the receiver to a point of interest in the coordinate space of the AVCaptureDevice providing input to the receiver. The conversion takes frameSize and videoGravity into consideration.
+ */
 - (CGPoint)captureDevicePointOfInterestForPoint:(CGPoint)pointInLayer NS_AVAILABLE_IOS(6_0);
 
 /*!
  @method pointForCaptureDevicePointOfInterest:
  @abstract
-    Converts a point of interest in the coordinate space of the capture device providing
-    input to the layer to a point in layer coordinates.
+    Converts a point of interest in the coordinate space of the capture device providing input to the layer to a point in layer coordinates.
 
  @param captureDevicePointOfInterest
     A CGPoint in the coordinate space of the capture device providing input to the layer.
-
  @result
     A CGPoint in layer coordinates.
 
  @discussion
-    AVCaptureDevice pointOfInterest is expressed as a CGPoint where {0,0} represents the top left of the picture area,
-    and {1,1} represents the bottom right on an unrotated picture.  This convenience method converts a point in 
-    the coordinate space of the AVCaptureDevice providing input to the coordinate space of the receiver.  The conversion 
-    takes frame size and videoGravity into consideration.
-*/
+    AVCaptureDevice pointOfInterest is expressed as a CGPoint where {0,0} represents the top left of the picture area, and {1,1} represents the bottom right on an unrotated picture. This convenience method converts a point in the coordinate space of the AVCaptureDevice providing input to the coordinate space of the receiver. The conversion takes frame size and videoGravity into consideration.
+ */
 - (CGPoint)pointForCaptureDevicePointOfInterest:(CGPoint)captureDevicePointOfInterest NS_AVAILABLE_IOS(6_0);
 
 /*!
  @method metadataOutputRectOfInterestForRect:
  @abstract
-	Converts a rectangle in layer coordinates to a rectangle of interest in the coordinate space of an AVCaptureMetadataOutput
-	whose capture device is providing input to the layer.
+    Converts a rectangle in layer coordinates to a rectangle of interest in the coordinate space of an AVCaptureMetadataOutput whose capture device is providing input to the layer.
  
  @param rectInLayerCoordinates
-	A CGRect in layer coordinates.
- 
+    A CGRect in layer coordinates.
  @result
-	A CGRect in the coordinate space of the metadata output whose capture device is providing input to the layer.
+    A CGRect in the coordinate space of the metadata output whose capture device is providing input to the layer.
  
  @discussion
-	AVCaptureMetadataOutput rectOfInterest is expressed as a CGRect where {0,0} represents the top left of the picture area,
-	and {1,1} represents the bottom right on an unrotated picture.  This convenience method converts a rectangle in
-	the coordinate space of the receiver to a rectangle of interest in the coordinate space of an AVCaptureMetadataOutput 
-	whose AVCaptureDevice is providing input to the receiver.  The conversion takes frame size and videoGravity into consideration.
- */
+    AVCaptureMetadataOutput rectOfInterest is expressed as a CGRect where {0,0} represents the top left of the picture area, and {1,1} represents the bottom right on an unrotated picture. This convenience method converts a rectangle in the coordinate space of the receiver to a rectangle of interest in the coordinate space of an AVCaptureMetadataOutput whose AVCaptureDevice is providing input to the receiver. The conversion takes frame size and videoGravity into consideration.
+  */
 - (CGRect)metadataOutputRectOfInterestForRect:(CGRect)rectInLayerCoordinates NS_AVAILABLE_IOS(7_0);
 
 /*!
  @method rectForMetadataOutputRectOfInterest:
  @abstract
-	Converts a rectangle of interest in the coordinate space of an AVCaptureMetadataOutput whose capture device is 
-	providing input to the layer to a rectangle in layer coordinates.
+    Converts a rectangle of interest in the coordinate space of an AVCaptureMetadataOutput whose capture device is providing input to the layer to a rectangle in layer coordinates.
  
  @param rectInMetadataOutputCoordinates
-	A CGRect in the coordinate space of the metadata output whose capture device is providing input to the layer.
- 
+    A CGRect in the coordinate space of the metadata output whose capture device is providing input to the layer.
  @result
-	A CGRect in layer coordinates.
+    A CGRect in layer coordinates.
  
  @discussion
-	AVCaptureMetadataOutput rectOfInterest is expressed as a CGRect where {0,0} represents the top left of the picture area,
-	and {1,1} represents the bottom right on an unrotated picture.  This convenience method converts a rectangle in
-	the coordinate space of an AVCaptureMetadataOutput whose AVCaptureDevice is providing input to the coordinate space of the 
-	receiver.  The conversion takes frame size and videoGravity into consideration.
- */
+    AVCaptureMetadataOutput rectOfInterest is expressed as a CGRect where {0,0} represents the top left of the picture area, and {1,1} represents the bottom right on an unrotated picture. This convenience method converts a rectangle in the coordinate space of an AVCaptureMetadataOutput whose AVCaptureDevice is providing input to the coordinate space of the receiver. The conversion takes frame size and videoGravity into consideration.
+  */
 - (CGRect)rectForMetadataOutputRectOfInterest:(CGRect)rectInMetadataOutputCoordinates NS_AVAILABLE_IOS(7_0);
 
 /*!
@@ -229,18 +184,12 @@
 
  @param metadataObject
     An AVMetadataObject originating from the same AVCaptureInput as the preview layer.
-
  @result
     An AVMetadataObject whose properties are in layer coordinates.
 
  @discussion
-    AVMetadataObject bounds may be expressed as a rect where {0,0} represents the top left of the picture area,
-    and {1,1} represents the bottom right on an unrotated picture.  Face metadata objects likewise express
-    yaw and roll angles with respect to an unrotated picture.  -transformedMetadataObjectForMetadataObject: 
-	converts the visual properties in the coordinate space of the supplied AVMetadataObject to the coordinate space of 
-    the receiver.  The conversion takes orientation, mirroring, layer bounds and videoGravity into consideration.
-    If the provided metadata object originates from an input source other than the preview layer's, nil will be returned.
-*/
+    AVMetadataObject bounds may be expressed as a rect where {0,0} represents the top left of the picture area, and {1,1} represents the bottom right on an unrotated picture. Face metadata objects likewise express yaw and roll angles with respect to an unrotated picture. -transformedMetadataObjectForMetadataObject: converts the visual properties in the coordinate space of the supplied AVMetadataObject to the coordinate space of the receiver. The conversion takes orientation, mirroring, layer bounds and videoGravity into consideration. If the provided metadata object originates from an input source other than the preview layer's, nil will be returned.
+ */
 - (AVMetadataObject *)transformedMetadataObjectForMetadataObject:(AVMetadataObject *)metadataObject NS_AVAILABLE_IOS(6_0);
 
 #if TARGET_OS_IPHONE
@@ -251,11 +200,8 @@
     Specifies whether or not the preview layer supports orientation.
 
  @discussion
-    Changes in orientation are not supported on all hardware configurations.  An
-    application should check the value of @"orientationSupported" before attempting to
-    manipulate the orientation of the receiver.  This property is deprecated.  Use 
-    AVCaptureConnection's -isVideoOrientationSupported instead.
-*/
+    Changes in orientation are not supported on all hardware configurations. An application should check the value of @"orientationSupported" before attempting to manipulate the orientation of the receiver. This property is deprecated. Use AVCaptureConnection's -isVideoOrientationSupported instead.
+ */
 @property (nonatomic, readonly, getter=isOrientationSupported) BOOL orientationSupported NS_DEPRECATED_IOS(4_0, 6_0, "Use AVCaptureConnection's isVideoOrientationSupported instead.");
 
 /*!
@@ -264,11 +210,8 @@
     Specifies the orientation of the preview layer.
 
  @discussion
-    AVCaptureVideoOrientation and its constants are defined in AVCaptureSession.h.
-    The value of @"orientationSupported" must be YES in order to set @"orientation".  An
-    exception will be raised if this requirement is ignored.  This property is deprecated.
-    Use AVCaptureConnection's -videoOrientation instead.
-*/
+    AVCaptureVideoOrientation and its constants are defined in AVCaptureSession.h. The value of @"orientationSupported" must be YES in order to set @"orientation". An exception will be raised if this requirement is ignored. This property is deprecated. Use AVCaptureConnection's -videoOrientation instead.
+ */
 @property (nonatomic) AVCaptureVideoOrientation orientation NS_DEPRECATED_IOS(4_0, 6_0, "Use AVCaptureConnection's videoOrientation instead.");
 
 /*!
@@ -277,26 +220,18 @@
     Specifies whether or not the preview layer supports mirroring.
 
  @discussion
-    Mirroring is not supported on all hardware configurations.  An application should
-    check the value of @"mirroringSupported" before attempting to manipulate mirroring
-    on the receiver.  This property is deprecated.  Use AVCaptureConnection's 
-    -isVideoMirroringSupported instead.
-*/
+    Mirroring is not supported on all hardware configurations. An application should check the value of @"mirroringSupported" before attempting to manipulate mirroring on the receiver. This property is deprecated. Use AVCaptureConnection's -isVideoMirroringSupported instead.
+ */
 @property (nonatomic, readonly, getter=isMirroringSupported) BOOL mirroringSupported NS_DEPRECATED_IOS(4_0, 6_0, "Use AVCaptureConnection's isVideoMirroringSupported instead.");
 
 /*!
  @property automaticallyAdjustsMirroring
  @abstract
-    Specifies whether or not the value of @"mirrored" can change based on configuration
-    of the session.
+    Specifies whether or not the value of @"mirrored" can change based on configuration of the session.
 	
  @discussion		
-    For some session configurations, preview will be mirrored by default.  When the value 
-    of this property is YES, the value of @"mirrored" may change depending on the configuration 
-    of the session, for example after switching to a different AVCaptureDeviceInput.
-    The default value is YES.  This property is deprecated.  Use AVCaptureConnection's
-    -automaticallyAdjustsVideoMirroring instead.
-*/
+    For some session configurations, preview will be mirrored by default. When the value of this property is YES, the value of @"mirrored" may change depending on the configuration of the session, for example after switching to a different AVCaptureDeviceInput. The default value is YES. This property is deprecated. Use AVCaptureConnection's -automaticallyAdjustsVideoMirroring instead.
+ */
 @property (nonatomic) BOOL automaticallyAdjustsMirroring NS_DEPRECATED_IOS(4_0, 6_0, "Use AVCaptureConnection's automaticallyAdjustsVideoMirroring instead.");
 
 /*!
@@ -305,14 +240,8 @@
     Specifies whether or not the preview is flipped over a vertical axis.
 	
  @discussion		
-    For most applications, it is unnecessary to manipulate preview mirroring manually if 
-    @"automaticallyAdjustsMirroring" is set to YES.
-    The value of @"automaticallyAdjustsMirroring" must be NO in order to set @"mirrored".
-    The value of @"mirroringSupported" must be YES in order to set @"mirrored".  An
-    exception will be raised if the value of @"mirrored" is mutated without respecting
-    these requirements.  This property is deprecated.  Use AVCaptureConnection's 
-    -videoMirrored instead.
-*/
+    For most applications, it is unnecessary to manipulate preview mirroring manually if @"automaticallyAdjustsMirroring" is set to YES. The value of @"automaticallyAdjustsMirroring" must be NO in order to set @"mirrored". The value of @"mirroringSupported" must be YES in order to set @"mirrored". An exception will be raised if the value of @"mirrored" is mutated without respecting these requirements. This property is deprecated. Use AVCaptureConnection's -videoMirrored instead.
+ */
 @property (nonatomic, getter=isMirrored) BOOL mirrored NS_DEPRECATED_IOS(4_0, 6_0, "Use AVCaptureConnection's videoMirrored instead.");
 
 #endif // TARGET_OS_IPHONE
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVComposition.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVComposition.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVComposition.h	2015-09-30 23:18:01.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVComposition.h	2016-05-26 02:32:45.000000000 +0200
@@ -3,53 +3,47 @@
 
 	Framework:  AVFoundation
  
-	Copyright 2010-2015 Apple Inc. All rights reserved.
+	Copyright 2010-2016 Apple Inc. All rights reserved.
 
 */
 
 /*!
-    @class			AVComposition
+    @class          AVComposition
 
-    @abstract		An AVComposition combines media data from multiple local file-based sources in a custom temporal arrangement, in order to present or process media data from multiple sources together. All local file-based audiovisual
-    				assets are eligible to be combined, regardless of container type.
-	
-	@discussion		At its top-level, AVComposition is a collection of tracks, each presenting media of a specific media type, e.g. audio or video, according to a timeline. Each track is represented by an instance of AVCompositionTrack.
+    @abstract       An AVComposition combines media data from multiple local file-based sources in a custom temporal arrangement, in order to present or process media data from multiple sources together. All local file-based audiovisual assets are eligible to be combined, regardless of container type.
 
-					Each track is comprised of an array of track segments, each of which present a portion of the media data stored in a source container, specified by URL, a track identifier, and a time mapping, as represented by
-					an instance of AVCompositionTrackSegment.
-					
-					The URL specifies the source container, and the track identifier indicates the track of the source container to be presented.
-					
-					The time mapping specifies the temporal range of the source track that's to be presented and also specifies the temporal range of its presentation in the composition track. If the durations of the source and destination
-					ranges of the time mapping are the same, the media data for the segment will be presented at its natural rate. Otherwise, the segment will be presented at a rate equal to the ratio source.duration / target.duration.
-					
-					The track segments of a track are available via AVCompositionTrack's trackSegment property, an array of AVCompositionTrackSegment. The collection of tracks with media type information for each, and each with its
-					array of track segments (URL, track identifier, and time mapping), form a complete low-level representation of a composition.
+    @discussion
+      At its top-level, AVComposition is a collection of tracks, each presenting media of a specific media type, e.g. audio or video, according to a timeline. Each track is represented by an instance of AVCompositionTrack.
 
-					This representation can be written out by clients in any convenient form, and subsequently the composition can be reconstituted by instantiating a new AVMutableComposition with AVMutableCompositionTracks
-					of the appropriate media type, each with its trackSegment property set according to the stored array of URL, track identifier, and time mapping.
-					
-					A higher-level interface for constructing compositions is also presented by AVMutableComposition and AVMutableCompositionTrack, offering insertion, removal, and scaling operations without direct
-					manipulation of the trackSegment arrays of composition tracks. This interface makes use of higher-level constructs such as AVAsset and AVAssetTrack, allowing the client to make use of the same references to
-					candidate sources that it would have created in order to inspect or preview them prior to inclusion in a composition.
+      Each track is comprised of an array of track segments, each of which present a portion of the media data stored in a source container, specified by URL, a track identifier, and a time mapping, as represented by an instance of AVCompositionTrackSegment.
 
-					Immutable Snapshots
+      The URL specifies the source container, and the track identifier indicates the track of the source container to be presented.
 
-						To make an immutable snapshot of a mutable composition for playback or inspection:
-					
-						// myMutableComposition is a mutable composition; the client wants to inspect and play it in its current state
-						AVComposition *immutableSnapshotOfMyComposition = [myMutableComposition copy];
-				
-						// inspect and play at will, e.g.
-						AVPlayerItem *playerItemForSnapshottedComposition = [[AVPlayerItem alloc] initWithAsset:immutableSnapshotOfMyComposition];
+      The time mapping specifies the temporal range of the source track that's to be presented and also specifies the temporal range of its presentation in the composition track. If the durations of the source and destination ranges of the time mapping are the same, the media data for the segment will be presented at its natural rate. Otherwise, the segment will be presented at a rate equal to the ratio source.duration / target.duration.
 
-					Compositing Of Video Tracks
+      The track segments of a track are available via AVCompositionTrack's trackSegment property, an array of AVCompositionTrackSegment. The collection of tracks with media type information for each, and each with its array of track segments (URL, track identifier, and time mapping), form a complete low-level representation of a composition.
 
-						During playback or other processing, such as export, without the use of an AVVideoComposition only the first enabled video track will be processed. Other video tracks are effectively ignored. To control the compositing of multiple enabled video tracks, you must create and configure an instance of AVVideoComposition and set it as the value of the videoComposition property of the AVFoundation object you're using to control processing, such as an AVPlayerItem or AVAssetExportSession.
+      This representation can be written out by clients in any convenient form, and subsequently the composition can be reconstituted by instantiating a new AVMutableComposition with AVMutableCompositionTracks of the appropriate media type, each with its trackSegment property set according to the stored array of URL, track identifier, and time mapping.
 
-					Mixing Of Audio Tracks
+      A higher-level interface for constructing compositions is also presented by AVMutableComposition and AVMutableCompositionTrack, offering insertion, removal, and scaling operations without direct manipulation of the trackSegment arrays of composition tracks. This interface makes use of higher-level constructs such as AVAsset and AVAssetTrack, allowing the client to make use of the same references to candidate sources that it would have created in order to inspect or preview them prior to inclusion in a composition.
 
-						During playback or other processing, without the use of an AVAudioMix all of the asset's enabled audio tracks are mixed together at equal levels. To control the mixing of enabled audio tracks, you must create and configure an instance of AVAudioMix and set it as the value of the audioMix property of the AVFoundation object you're using to control processing, such as an AVPlayerItem or AVAssetExportSession.
+      Immutable Snapshots
+
+        To make an immutable snapshot of a mutable composition for playback or inspection:
+
+            // myMutableComposition is a mutable composition; the client wants to inspect and play it in its current state
+            AVComposition *immutableSnapshotOfMyComposition = [myMutableComposition copy];
+
+            // inspect and play at will, e.g.
+            AVPlayerItem *playerItemForSnapshottedComposition = [[AVPlayerItem alloc] initWithAsset:immutableSnapshotOfMyComposition];
+
+      Compositing Of Video Tracks
+
+        During playback or other processing, such as export, without the use of an AVVideoComposition only the first enabled video track will be processed. Other video tracks are effectively ignored. To control the compositing of multiple enabled video tracks, you must create and configure an instance of AVVideoComposition and set it as the value of the videoComposition property of the AVFoundation object you're using to control processing, such as an AVPlayerItem or AVAssetExportSession.
+
+      Mixing Of Audio Tracks
+
+        During playback or other processing, without the use of an AVAudioMix all of the asset's enabled audio tracks are mixed together at equal levels. To control the mixing of enabled audio tracks, you must create and configure an instance of AVAudioMix and set it as the value of the audioMix property of the AVFoundation object you're using to control processing, such as an AVPlayerItem or AVAssetExportSession.
 */
 
 #import <AVFoundation/AVAsset.h>
@@ -65,21 +59,27 @@
 @interface AVComposition : AVAsset <NSMutableCopying>
 {
 @private
-	AVCompositionInternal	*_priv;
+    AVCompositionInternal    *_priv;
 }
 
-/* provides the array of AVCompositionTracks contained by the composition */
+/*!
+    @property       tracks
+    @abstract       Provides the array of AVCompositionTracks contained by the composition.
+*/
 @property (nonatomic, readonly) NSArray<AVCompositionTrack *> *tracks;
 
-/*	indicates the authored size of the visual portion of the composition */
+/*!
+    @property       naturalSize
+    @abstract       Indicates the authored size of the visual portion of the composition.
+*/
 @property (nonatomic, readonly) CGSize naturalSize;
 
 /*!
-	@property		URLAssetInitializationOptions
-	@abstract		Specifies the initialization options for the creation of AVURLAssets by the receiver, e.g. AVURLAssetPreferPreciseDurationAndTimingKey. The default behavior for creation of AVURLAssets by an AVComposition is equivalent to the behavior of +[AVURLAsset URLAssetWithURL:options:] when specifying no initialization options.
-	@discussion
-		AVCompositions create AVURLAssets internally for URLs specified by AVCompositionTrackSegments of AVCompositionTracks, as needed, whenever AVCompositionTrackSegments were originally added to a track via -[AVMutableCompositionTrack setSegments:] rather than by inserting timeranges of already existing AVAssets or AVAssetTracks.
-		The value of URLAssetInitializationOptions can be specified at the time an AVMutableComposition is created via +compositionWithURLAssetInitializationOptions:.
+    @property       URLAssetInitializationOptions
+    @abstract       Specifies the initialization options for the creation of AVURLAssets by the receiver, e.g. AVURLAssetPreferPreciseDurationAndTimingKey. The default behavior for creation of AVURLAssets by an AVComposition is equivalent to the behavior of +[AVURLAsset URLAssetWithURL:options:] when specifying no initialization options.
+    @discussion
+      AVCompositions create AVURLAssets internally for URLs specified by AVCompositionTrackSegments of AVCompositionTracks, as needed, whenever AVCompositionTrackSegments were originally added to a track via -[AVMutableCompositionTrack setSegments:] rather than by inserting timeranges of already existing AVAssets or AVAssetTracks.
+      The value of URLAssetInitializationOptions can be specified at the time an AVMutableComposition is created via +compositionWithURLAssetInitializationOptions:.
  */
 @property (nonatomic, readonly, copy) NSDictionary<NSString *, id> *URLAssetInitializationOptions NS_AVAILABLE(10_11, 9_0);
 
@@ -88,32 +88,35 @@
 @interface AVComposition (AVCompositionTrackInspection)
 
 /*!
-  @method		trackWithTrackID:
-  @abstract		Provides an instance of AVCompositionTrack that represents the track of the specified trackID.
-  @param		trackID
-				The trackID of the requested AVCompositionTrack.
-  @result		An instance of AVCompositionTrack; may be nil if no track of the specified trackID is available.
-  @discussion	Becomes callable without blocking when the key @"tracks" has been loaded
+    @method         trackWithTrackID:
+    @abstract       Provides an instance of AVCompositionTrack that represents the track of the specified trackID.
+    @param          trackID
+                    The trackID of the requested AVCompositionTrack.
+    @result         An instance of AVCompositionTrack; may be nil if no track of the specified trackID is available.
+    @discussion
+      Becomes callable without blocking when the key @"tracks" has been loaded
 */
 - (nullable AVCompositionTrack *)trackWithTrackID:(CMPersistentTrackID)trackID;
 
 /*!
-  @method		tracksWithMediaType:
-  @abstract		Provides an array of AVCompositionTracks of the asset that present media of the specified media type.
-  @param		mediaType
-				The media type according to which the receiver filters its AVCompositionTracks. (Media types are defined in AVMediaFormat.h)
-  @result		An NSArray of AVCompositionTracks; may be empty if no tracks of the specified media type are available.
-  @discussion	Becomes callable without blocking when the key @"tracks" has been loaded
+    @method         tracksWithMediaType:
+    @abstract       Provides an array of AVCompositionTracks of the asset that present media of the specified media type.
+    @param          mediaType
+                    The media type according to which the receiver filters its AVCompositionTracks. (Media types are defined in AVMediaFormat.h)
+    @result         An NSArray of AVCompositionTracks; may be empty if no tracks of the specified media type are available.
+    @discussion
+      Becomes callable without blocking when the key @"tracks" has been loaded
 */
 - (NSArray<AVCompositionTrack *> *)tracksWithMediaType:(NSString *)mediaType;
 
 /*!
-  @method		tracksWithMediaCharacteristic:
-  @abstract		Provides an array of AVCompositionTracks of the asset that present media with the specified characteristic.
-  @param		mediaCharacteristic
-				The media characteristic according to which the receiver filters its AVCompositionTracks. (Media characteristics are defined in AVMediaFormat.h)
-  @result		An NSArray of AVCompositionTracks; may be empty if no tracks with the specified characteristic are available.
-  @discussion	Becomes callable without blocking when the key @"tracks" has been loaded
+    @method         tracksWithMediaCharacteristic:
+    @abstract       Provides an array of AVCompositionTracks of the asset that present media with the specified characteristic.
+    @param          mediaCharacteristic
+                    The media characteristic according to which the receiver filters its AVCompositionTracks. (Media characteristics are defined in AVMediaFormat.h)
+    @result         An NSArray of AVCompositionTracks; may be empty if no tracks with the specified characteristic are available.
+    @discussion
+      Becomes callable without blocking when the key @"tracks" has been loaded
 */
 - (NSArray<AVCompositionTrack *> *)tracksWithMediaCharacteristic:(NSString *)mediaCharacteristic;
 
@@ -129,94 +132,96 @@
     AVMutableCompositionInternal    *_mutablePriv;
 }
 
-/* provides the array of AVMutableCompositionTracks contained by the composition */
+/*!
+    @property       tracks
+    @abstract       Provides the array of AVMutableCompositionTracks contained by the composition.
+*/
 @property (nonatomic, readonly) NSArray<AVMutableCompositionTrack *> *tracks;
 
-/* Indicates the authored size of the visual portion of the asset.
-   If not set, the default behavior is to provide the size of the composition's first video track.
-   Set to CGSizeZero to revert to default behavior. */
+/*!
+    @property       naturalSize
+    @abstract       Indicates the authored size of the visual portion of the asset.
+    @discussion
+      If not set, the value is the size of the composition's first video track. Set to CGSizeZero to revert to default behavior.
+*/
 @property (nonatomic) CGSize naturalSize;
 
 /*!
-	@method			composition
-	@abstract		Returns an empty AVMutableComposition.
+    @method         composition
+    @abstract       Returns an empty AVMutableComposition.
 */
 + (instancetype)composition;
 
 /*!
-	@method			compositionWithURLAssetInitializationOptions:
-	@abstract		Returns an empty AVMutableComposition.
-	@param			URLAssetInitializationOptions
-					Specifies the initialization options that the receiver should use when creating AVURLAssets internally, e.g. AVURLAssetPreferPreciseDurationAndTimingKey. The default behavior for creation of AVURLAssets by an AVMutableComposition is equivalent to the behavior of +[AVURLAsset URLAssetWithURL:options:] when specifying no initialization options.
-	@discussion		AVMutableCompositions create AVURLAssets internally for URLs specified by AVCompositionTrackSegments of AVMutableCompositionTracks, as needed, whenever AVCompositionTrackSegments are added to tracks via -[AVMutableCompositionTrack setSegments:] rather than by inserting timeranges of already existing AVAssets or AVAssetTracks.
+    @method         compositionWithURLAssetInitializationOptions:
+    @abstract       Returns an empty AVMutableComposition.
+    @param          URLAssetInitializationOptions
+                    Specifies the initialization options that the receiver should use when creating AVURLAssets internally, e.g. AVURLAssetPreferPreciseDurationAndTimingKey. The default behavior for creation of AVURLAssets by an AVMutableComposition is equivalent to the behavior of +[AVURLAsset URLAssetWithURL:options:] when specifying no initialization options.
+    @discussion
+      AVMutableCompositions create AVURLAssets internally for URLs specified by AVCompositionTrackSegments of AVMutableCompositionTracks, as needed, whenever AVCompositionTrackSegments are added to tracks via -[AVMutableCompositionTrack setSegments:] rather than by inserting timeranges of already existing AVAssets or AVAssetTracks.
  */
 + (instancetype)compositionWithURLAssetInitializationOptions:(nullable NSDictionary<NSString *, id> *)URLAssetInitializationOptions NS_AVAILABLE(10_11, 9_0);
 
 @end
 
-    
+
 @interface AVMutableComposition (AVMutableCompositionCompositionLevelEditing)
 
 /*!
-	@method			insertTimeRange:ofAsset:atTime:error:
-	@abstract		Inserts all the tracks of a timeRange of an asset into a composition.
-	@param			timeRange
-					Specifies the timeRange of the asset to be inserted.
-	@param			asset
-					Specifies the asset that contains the tracks that are to be inserted. Only instances of AVURLAsset and AVComposition are supported (AVComposition starting in MacOS X 10.10 and iOS 8.0).
-	@param			startTime
-					Specifies the time at which the inserted tracks are to be presented by the composition.
-	@param			outError
-					Describes failures that may be reported to the user, e.g. the asset that was selected for insertion in the composition is restricted by copy-protection.
-	@result			A BOOL value indicating the success of the insertion.
-	@discussion	
-		You provide a reference to an AVAsset and the timeRange within it that you want to insert. You specify the start time in the destination composition at which the timeRange should be inserted.
-		
-		This method may add new tracks to ensure that all tracks of the asset are represented in the inserted timeRange.
-		
-		Note that the media data for the inserted timeRange will be presented at its natural duration and rate. It can be scaled to a different duration and presented at a different rate via -scaleTimeRange:toDuration:.
-		
-		Existing content at the specified startTime will be pushed out by the duration of timeRange. 
-*/
-- (BOOL)insertTimeRange:(CMTimeRange)timeRange ofAsset:(AVAsset *)asset atTime:(CMTime)startTime error:(NSError * __nullable * __nullable)outError;
-
-/*!
-	@method			insertEmptyTimeRange:
-	@abstract		Adds or extends an empty timeRange within all tracks of the composition.
-	@param			timeRange
-					Specifies the empty timeRange to be inserted.
-	@discussion	
-		If you insert an empty timeRange into the composition, any media that was presented
-		during that interval prior to the insertion will be presented instead immediately
-		afterward. You can use this method to reserve an interval in which you want a subsequently
-		created track to present its media.
+    @method         insertTimeRange:ofAsset:atTime:error:
+    @abstract       Inserts all the tracks of a timeRange of an asset into a composition.
+    @param          timeRange
+                    Specifies the timeRange of the asset to be inserted.
+    @param          asset
+                    Specifies the asset that contains the tracks that are to be inserted. Only instances of AVURLAsset and AVComposition are supported (AVComposition starting in MacOS X 10.10 and iOS 8.0).
+    @param          startTime
+                    Specifies the time at which the inserted tracks are to be presented by the composition.
+    @param          outError
+                    Describes failures that may be reported to the user, e.g. the asset that was selected for insertion in the composition is restricted by copy-protection.
+    @result         A BOOL value indicating the success of the insertion.
+    @discussion
+      You provide a reference to an AVAsset and the timeRange within it that you want to insert. You specify the start time in the destination composition at which the timeRange should be inserted.
+
+      This method may add new tracks to ensure that all tracks of the asset are represented in the inserted timeRange.
+
+      Note that the media data for the inserted timeRange will be presented at its natural duration and rate. It can be scaled to a different duration and presented at a different rate via -scaleTimeRange:toDuration:.
+
+      Existing content at the specified startTime will be pushed out by the duration of timeRange.
+*/
+- (BOOL)insertTimeRange:(CMTimeRange)timeRange ofAsset:(AVAsset *)asset atTime:(CMTime)startTime error:(NSError * _Nullable * _Nullable)outError;
+
+/*!
+    @method         insertEmptyTimeRange:
+    @abstract       Adds or extends an empty timeRange within all tracks of the composition.
+    @param          timeRange
+                    Specifies the empty timeRange to be inserted.
+    @discussion
+     If you insert an empty timeRange into the composition, any media that was presented during that interval prior to the insertion will be presented instead immediately afterward. You can use this method to reserve an interval in which you want a subsequently created track to present its media.
+      Note that you cannot add empty time ranges to the end of a composition.
 */
 - (void)insertEmptyTimeRange:(CMTimeRange)timeRange;
 
 /*!
-	@method			removeTimeRange:
-	@abstract		Removes a specified timeRange from all tracks of the composition.
-	@param			timeRange
-					Specifies the timeRange to be removed.
-	@discussion
-		Removal of a time range does not cause any existing tracks to be removed from the composition, 
-		even if removing timeRange results in an empty track.
-		Instead, it removes or truncates track segments that intersect with the timeRange.
+    @method         removeTimeRange:
+    @abstract       Removes a specified timeRange from all tracks of the composition.
+    @param          timeRange
+                    Specifies the timeRange to be removed.
+    @discussion
+      Removal of a time range does not cause any existing tracks to be removed from the composition, even if removing timeRange results in an empty track. Instead, it removes or truncates track segments that intersect with the timeRange.
 
-		After removing, existing content after timeRange will be pulled in.
+      After removing, existing content after timeRange will be pulled in.
 */
 - (void)removeTimeRange:(CMTimeRange)timeRange;
 
 /*!
-	@method			scaleTimeRange:toDuration:
-	@abstract		Changes the duration of a timeRange of all tracks.
-	@param			timeRange
-					Specifies the timeRange of the composition to be scaled.
-	@param			duration
-					Specifies the new duration of the timeRange.
-	@discussion
-		Each trackSegment affected by the scaling operation will be presented at a rate equal to
-		source.duration / target.duration of its resulting timeMapping.
+    @method         scaleTimeRange:toDuration:
+    @abstract       Changes the duration of a timeRange of all tracks.
+    @param          timeRange
+                    Specifies the timeRange of the composition to be scaled.
+    @param          duration
+                    Specifies the new duration of the timeRange.
+    @discussion
+      Each trackSegment affected by the scaling operation will be presented at a rate equal to source.duration / target.duration of its resulting timeMapping.
 */
 - (void)scaleTimeRange:(CMTimeRange)timeRange toDuration:(CMTime)duration;
 
@@ -226,48 +231,40 @@
 @interface AVMutableComposition (AVMutableCompositionTrackLevelEditing)
 
 /*!
-	@method			addMutableTrackWithMediaType:preferredTrackID:
-	@abstract		Adds an empty track to a mutable composition.
-	@param			mediaType
-					The media type of the new track.
-	@param			preferredTrackID
-					Specifies the preferred track ID for the new track.
-					The preferred track ID will be used for the new track provided that it is not currently in use and 
-					has not previously been used.
-					If you do not need to specify a preferred track ID, pass kCMPersistentTrackID_Invalid.
-					If the specified preferred track ID is not available, or kCMPersistentTrackID_Invalid was passed in,
-					a unique track ID will be generated.
-	@result			An instance of AVMutableCompositionTrack representing the new track.
-    				Its actual trackID is available via its @"trackID" key.
+    @method         addMutableTrackWithMediaType:preferredTrackID:
+    @abstract       Adds an empty track to a mutable composition.
+    @param          mediaType
+                    The media type of the new track.
+    @param          preferredTrackID
+                    Specifies the preferred track ID for the new track. If you do not need to specify a preferred track ID, pass kCMPersistentTrackID_Invalid. Otherwise the preferred track ID will be used for the new track, provided that it is not currently in use and has not previously been used.
+    @result         An instance of AVMutableCompositionTrack representing the new track. Its actual trackID is available via its @"trackID" key.
+    @discussion
+      If the specified preferred track ID is not available, or kCMPersistentTrackID_Invalid was passed in, a unique track ID will be generated.
 */
 - (AVMutableCompositionTrack *)addMutableTrackWithMediaType:(NSString *)mediaType preferredTrackID:(CMPersistentTrackID)preferredTrackID;
 
 /*!
-	@method			removeTrack:
-	@abstract		Removes a track of a mutable composition.
-	@param			track
-					A reference to the AVCompositionTrack to be removed.
-	@discussion
-		If you retain a reference to the removed track, note that its @"composition" key will have the value nil, and
-		the values of its other properties are undefined.
+    @method         removeTrack:
+    @abstract       Removes a track of a mutable composition.
+    @param          track
+                    A reference to the AVCompositionTrack to be removed.
+    @discussion
+      If you retain a reference to the removed track, note that its @"composition" key will have the value nil, and the values of its other properties are undefined.
 */
 - (void)removeTrack:(AVCompositionTrack *)track;
 
 /*!
-	@method			mutableTrackCompatibleWithTrack:
-	@abstract		Provides a reference to a track of a mutable composition into which any timeRange of an AVAssetTrack
-					can be inserted (via -[AVMutableCompositionTrack insertTimeRange:ofTrack:atTime:error:]).
-	@param			track
-					A reference to the AVAssetTrack from which a timeRange may be inserted.
-	@result			An AVMutableCompositionTrack that can accommodate the insertion.
-					If no such track is available, the result is nil. A new track of the same mediaType
-					as the AVAssetTrack can be created via -addMutableTrackWithMediaType:preferredTrackID:,
-					and this new track will be compatible.
-	@discussion		Similar to -[AVAsset compatibleTrackForCompositionTrack:].
-		For best performance, the number of tracks of a composition should be kept to a minimum, corresponding to the
-		number for which media data must be presented in parallel. If media data of the same type is to be presented
-		serially, even from multiple assets, a single track of that media type should be used. This method,
-		-mutableTrackCompatibleWithTrack:, can help the client to identify an existing target track for an insertion.
+    @method         mutableTrackCompatibleWithTrack:
+    @abstract       Provides a reference to a track of a mutable composition into which any timeRange of an AVAssetTrack can be inserted (via -[AVMutableCompositionTrack insertTimeRange:ofTrack:atTime:error:]).
+    @param          track
+                    A reference to the AVAssetTrack from which a timeRange may be inserted.
+    @result         An AVMutableCompositionTrack that can accommodate the insertion, or, if no such track is available, nil.
+    @discussion
+      If a compatible track is desired but the result of this method is nil, a new track of the same mediaType as the AVAssetTrack can be created via -addMutableTrackWithMediaType:preferredTrackID:, and this new track will be compatible.
+
+      For best performance, the number of tracks of a composition should be kept to a minimum, corresponding to the number for which media data must be presented in parallel. If media data of the same type is to be presented serially, even from multiple assets, a single track of that media type should be used. This method, -mutableTrackCompatibleWithTrack:, can help the client to identify an existing target track for an insertion.
+
+      Similar to -[AVAsset compatibleTrackForCompositionTrack:].
 */
 - (nullable AVMutableCompositionTrack *)mutableTrackCompatibleWithTrack:(AVAssetTrack *)track;
 
@@ -276,32 +273,35 @@
 @interface AVMutableComposition (AVMutableCompositionTrackInspection)
 
 /*!
-  @method		trackWithTrackID:
-  @abstract		Provides an instance of AVMutableCompositionTrack that represents the track of the specified trackID.
-  @param		trackID
-				The trackID of the requested AVMutableCompositionTrack.
-  @result		An instance of AVMutableCompositionTrack; may be nil if no track of the specified trackID is available.
-  @discussion	Becomes callable without blocking when the key @"tracks" has been loaded
+    @method         trackWithTrackID:
+    @abstract       Provides an instance of AVMutableCompositionTrack that represents the track of the specified trackID.
+    @param          trackID
+                    The trackID of the requested AVMutableCompositionTrack.
+    @result         An instance of AVMutableCompositionTrack; may be nil if no track of the specified trackID is available.
+    @discussion
+      Becomes callable without blocking when the key @"tracks" has been loaded
 */
 - (nullable AVMutableCompositionTrack *)trackWithTrackID:(CMPersistentTrackID)trackID;
 
 /*!
-  @method		tracksWithMediaType:
-  @abstract		Provides an array of AVMutableCompositionTracks of the asset that present media of the specified media type.
-  @param		mediaType
-				The media type according to which the receiver filters its AVMutableCompositionTracks. (Media types are defined in AVMediaFormat.h)
-  @result		An NSArray of AVMutableCompositionTracks; may be empty if no tracks of the specified media type are available.
-  @discussion	Becomes callable without blocking when the key @"tracks" has been loaded
+    @method         tracksWithMediaType:
+    @abstract       Provides an array of AVMutableCompositionTracks of the asset that present media of the specified media type.
+    @param          mediaType
+                    The media type according to which the receiver filters its AVMutableCompositionTracks. (Media types are defined in AVMediaFormat.h)
+    @result         An NSArray of AVMutableCompositionTracks; may be empty if no tracks of the specified media type are available.
+    @discussion
+      Becomes callable without blocking when the key @"tracks" has been loaded
 */
 - (NSArray<AVMutableCompositionTrack *> *)tracksWithMediaType:(NSString *)mediaType;
 
 /*!
-  @method		tracksWithMediaCharacteristic:
-  @abstract		Provides an array of AVMutableCompositionTracks of the asset that present media with the specified characteristic.
-  @param		mediaCharacteristic
-				The media characteristic according to which the receiver filters its AVMutableCompositionTracks. (Media characteristics are defined in AVMediaFormat.h)
-  @result		An NSArray of AVMutableCompositionTracks; may be empty if no tracks with the specified characteristic are available.
-  @discussion	Becomes callable without blocking when the key @"tracks" has been loaded
+    @method         tracksWithMediaCharacteristic:
+    @abstract       Provides an array of AVMutableCompositionTracks of the asset that present media with the specified characteristic.
+    @param          mediaCharacteristic
+                    The media characteristic according to which the receiver filters its AVMutableCompositionTracks. (Media characteristics are defined in AVMediaFormat.h)
+    @result         An NSArray of AVMutableCompositionTracks; may be empty if no tracks with the specified characteristic are available.
+    @discussion
+      Becomes callable without blocking when the key @"tracks" has been loaded
 */
 - (NSArray<AVMutableCompositionTrack *> *)tracksWithMediaCharacteristic:(NSString *)mediaCharacteristic;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCompositionTrack.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCompositionTrack.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCompositionTrack.h	2015-09-30 23:18:01.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCompositionTrack.h	2016-05-25 07:22:17.000000000 +0200
@@ -3,7 +3,7 @@
 
 	Framework:  AVFoundation
  
-	Copyright 2010-2015 Apple Inc. All rights reserved.
+	Copyright 2010-2016 Apple Inc. All rights reserved.
 
 */
 
@@ -18,11 +18,9 @@
 @class AVComposition;
 
 /*!
-    @class			AVCompositionTrack
+    @class          AVCompositionTrack
 
-    @abstract		AVCompositionTrack offers the low-level representation of tracks of AVCompositions, comprising
-    				a media type, a track identifier, and an array of AVCompositionTrackSegments, each comprising a URL,
-    				and track identifier, and a time mapping.
+    @abstract       AVCompositionTrack offers the low-level representation of tracks of AVCompositions, comprising a media type, a track identifier, and an array of AVCompositionTrackSegments, each comprising a URL, and track identifier, and a time mapping.
 */
 
 @class AVCompositionTrackInternal;
@@ -35,12 +33,12 @@
     AVCompositionTrackInternal    *_priv;
 }
 
-/* Provides access to the array of track segments, each an instance of AVCompositionTrackSegment.
-  	Note that timeMapping.target.start of the first AVCompositionTrackSegment must be kCMTimeZero,
-  	and the timeMapping.target.start of each subsequent AVCompositionTrackSegment must equal
-  	CMTimeRangeGetEnd(the previous AVCompositionTrackSegment's timeMapping.target).
-  	-validateTrackSegments:error: will perform a test to ensure that an array of AVCompositionTrackSegments
-  	conforms to this rule.
+/*!
+    @property       segments
+    @abstract       Provides read-only access to the array of track segments, each an instance of AVCompositionTrackSegment.
+    @discussion
+      Note that timeMapping.target.start of the first AVCompositionTrackSegment must be kCMTimeZero, and the timeMapping.target.start of each subsequent AVCompositionTrackSegment must equal CMTimeRangeGetEnd(the previous AVCompositionTrackSegment's timeMapping.target).
+      Use -validateTrackSegments:error: to perform a test to ensure that an array of AVCompositionTrackSegments conforms to this rule.
 */
 @property (nonatomic, readonly, copy) NSArray<AVCompositionTrackSegment *> *segments;
 
@@ -48,11 +46,10 @@
 
 
 /*!
-    @class			AVMutableCompositionTrack
+    @class          AVMutableCompositionTrack
 
-    @abstract		AVMutableCompositionTrack provides a convenient interface for insertions, removals, and scaling
-    				of track segments without direct manipulation of their low-level representation.
- */
+    @abstract       AVMutableCompositionTrack provides a convenient interface for insertions, removals, and scaling of track segments without direct manipulation of their low-level representation.
+*/
 
 @class AVMutableCompositionTrackInternal;
 
@@ -63,122 +60,138 @@
     AVMutableCompositionTrackInternal    *_mutablePriv;
 }
 
-/* Indicates a timescale in which time values for the track can be operated upon without extraneous numerical conversion.
-   If not set, returns the naturalTimeScale of the first non-empty edit, or 600 if there are no non-empty edits.
-   Set to 0 to revert to default behavior. */
+/*!
+    @property       naturalTimeScale
+    @abstract       Indicates a timescale in which time values for the track can be operated upon without extraneous numerical conversion.
+    @discussion
+      If not set, the value is the naturalTimeScale of the first non-empty edit, or 600 if there are no non-empty edits.
+      Set to 0 to revert to default behavior.
+*/
 @property (nonatomic) CMTimeScale naturalTimeScale;
 
-/* indicates the language associated with the track, as an ISO 639-2/T language code; if not set, returns nil */
+/*!
+    @property       languageCode
+    @abstract       Indicates the language associated with the track, as an ISO 639-2/T language code.
+    @discussion
+      The default value is nil.
+*/
 @property (nonatomic, copy, nullable) NSString *languageCode;
 
-/* indicates the language tag associated with the track, as an IETF BCP 47 (RFC 4646) language identifier; if not set, returns nil */
+/*!
+    @property       extendedLanguageTag
+    @abstract       Indicates the language tag associated with the track, as an IETF BCP 47 (RFC 4646) language identifier.
+    @discussion
+      The default value is nil.
+*/
 @property (nonatomic, copy, nullable) NSString *extendedLanguageTag;
 
-/* the preferred transformation of the visual media data for display purposes; if not set, returns CGAffineTransformIdentity */
+/*!
+    @property       preferredTransform
+    @abstract       The preferred transformation of the visual media data for display purposes.
+    @discussion
+      The default value is CGAffineTransformIdentity.
+*/
 @property (nonatomic) CGAffineTransform preferredTransform;
 
-/* the preferred volume of the audible media data; if not set, returns 1.0 */
+/*!
+    @property       preferredVolume
+    @abstract       The preferred volume of the audible media data.
+    @discussion
+      The default value is 1.0.
+*/
 @property (nonatomic) float preferredVolume;
 
-/* Provides read/write access to the array of track segments, each an instance of AVCompositionTrackSegment.
-  	Note that timeMapping.target.start of the first AVCompositionTrackSegment must be kCMTimeZero,
-  	and the timeMapping.target.start of each subsequent AVCompositionTrackSegment must equal
-  	CMTimeRangeGetEnd(the previous AVCompositionTrackSegment's timeMapping.target).
-  	-validateTrackSegments:error: will perform a test to ensure that an array of AVCompositionTrackSegments
-  	conforms to this rule.
+/*!
+    @property       segments
+    @abstract       Provides read/write access to the array of track segments, each an instance of AVCompositionTrackSegment.
+    @discussion
+      Note that timeMapping.target.start of the first AVCompositionTrackSegment must be kCMTimeZero, and the timeMapping.target.start of each subsequent AVCompositionTrackSegment must equal CMTimeRangeGetEnd(the previous AVCompositionTrackSegment's timeMapping.target).
+      Use -validateTrackSegments:error: to perform a test to ensure that an array of AVCompositionTrackSegments conforms to this rule.
 */
 @property (nonatomic, copy, null_resettable) NSArray<AVCompositionTrackSegment *> *segments;
 
 /*!
-	@method			insertTimeRange:ofTrack:atTime:error:
-	@abstract		Inserts a timeRange of a source track into a track of a composition.
-	@param			timeRange
-					Specifies the timeRange of the track to be inserted.
-	@param			track
-					Specifies the source track to be inserted. Only AVAssetTracks of AVURLAssets and AVCompositions are supported (AVCompositions starting in MacOS X 10.10 and iOS 8.0).
-	@param			startTime
-					Specifies the time at which the inserted track is to be presented by the composition track. You may pass kCMTimeInvalid for startTime to indicate that the timeRange should be appended to the end of the track.
-	@param			error
-					Describes failures that may be reported to the user, e.g. the asset that was selected for insertion in the composition is restricted by copy-protection.
-	@result			A BOOL value indicating the success of the insertion.
-	@discussion	
-		You provide a reference to an AVAssetTrack and the timeRange within it that you want to insert. You specify the start time in the target composition track at which the timeRange should be inserted.
-		
-		Note that the inserted track timeRange will be presented at its natural duration and rate. It can be scaled to a different duration (and presented at a different rate) via -scaleTimeRange:toDuration:.
-*/
-- (BOOL)insertTimeRange:(CMTimeRange)timeRange ofTrack:(AVAssetTrack *)track atTime:(CMTime)startTime error:(NSError * __nullable * __nullable)outError;
-
-/*!
-	@method			insertTimeRanges:ofTracks:atTime:error:
-	@abstract		Inserts the timeRanges of multiple source tracks into a track of a composition.
-	@param			timeRanges
-					Specifies the timeRanges to be inserted.  An NSArray of NSValues containing CMTimeRange. 
-					See +[NSValue valueWithCMTimeRange:] in AVTime.h.
-	@param			tracks
-					Specifies the source tracks to be inserted. Only AVAssetTracks of AVURLAssets and AVCompositions are supported (AVCompositions starting in MacOS X 10.10 and iOS 8.0).
-	@param			startTime
-					Specifies the time at which the inserted tracks are to be presented by the composition track. You may pass kCMTimeInvalid for startTime to indicate that the timeRanges should be appended to the end of the track.
-	@param			error
-					Describes failures that may be reported to the user, e.g. the asset that was selected for insertion in the composition is restricted by copy-protection.
-	@result			A BOOL value indicating the success of the insertion.
-	@discussion	
-		This method is equivalent to (but more efficient than) calling -insertTimeRange:ofTrack:atTime:error: for each timeRange/track pair. If this method returns an error, none of the time ranges will be inserted into the composition track. To specify an empty time range, pass NSNull for the track and a time range of starting at kCMTimeInvalid with a duration of the desired empty edit.
-*/
-- (BOOL)insertTimeRanges:(NSArray<NSValue *> *)timeRanges ofTracks:(NSArray<AVAssetTrack *> *)tracks atTime:(CMTime)startTime error:(NSError * __nullable * __nullable)outError NS_AVAILABLE(10_8, 5_0);
-
-/*!
-	@method			insertEmptyTimeRange:
-	@abstract		Adds or extends an empty timeRange within the composition track.
-	@param			timeRange
-					Specifies the empty timeRange to be inserted.
-	@discussion	
-		If you insert an empty timeRange into the track, any media that was presented
-		during that interval prior to the insertion will be presented instead immediately
-		afterward.
-		The exact meaning of the term "empty timeRange" depends upon the mediaType of the track.  
-		For example, an empty timeRange in a sound track presents silence.
+    @method         insertTimeRange:ofTrack:atTime:error:
+    @abstract       Inserts a timeRange of a source track into a track of a composition.
+    @param          timeRange
+                    Specifies the timeRange of the track to be inserted.
+    @param          track
+                    Specifies the source track to be inserted. Only AVAssetTracks of AVURLAssets and AVCompositions are supported (AVCompositions starting in MacOS X 10.10 and iOS 8.0).
+    @param          startTime
+                    Specifies the time at which the inserted track is to be presented by the composition track. You may pass kCMTimeInvalid for startTime to indicate that the timeRange should be appended to the end of the track.
+    @param          error
+                    Describes failures that may be reported to the user, e.g. the asset that was selected for insertion in the composition is restricted by copy-protection.
+    @result         A BOOL value indicating the success of the insertion.
+    @discussion
+      You provide a reference to an AVAssetTrack and the timeRange within it that you want to insert. You specify the start time in the target composition track at which the timeRange should be inserted.
+
+      Note that the inserted track timeRange will be presented at its natural duration and rate. It can be scaled to a different duration (and presented at a different rate) via -scaleTimeRange:toDuration:.
+*/
+- (BOOL)insertTimeRange:(CMTimeRange)timeRange ofTrack:(AVAssetTrack *)track atTime:(CMTime)startTime error:(NSError * _Nullable * _Nullable)outError;
+
+/*!
+    @method         insertTimeRanges:ofTracks:atTime:error:
+    @abstract       Inserts the timeRanges of multiple source tracks into a track of a composition.
+    @param          timeRanges
+                    Specifies the timeRanges to be inserted. An NSArray of NSValues containing CMTimeRange. (See +[NSValue valueWithCMTimeRange:] in AVTime.h.)
+    @param          tracks
+                    Specifies the source tracks to be inserted. Only AVAssetTracks of AVURLAssets and AVCompositions are supported (AVCompositions starting in MacOS X 10.10 and iOS 8.0).
+    @param          startTime
+                    Specifies the time at which the inserted tracks are to be presented by the composition track. You may pass kCMTimeInvalid for startTime to indicate that the timeRanges should be appended to the end of the track.
+    @param          error
+                    Describes failures that may be reported to the user, e.g. the asset that was selected for insertion in the composition is restricted by copy-protection.
+    @result         A BOOL value indicating the success of the insertion.
+    @discussion
+      This method is equivalent to (but more efficient than) calling -insertTimeRange:ofTrack:atTime:error: for each timeRange/track pair. If this method returns an error, none of the time ranges will be inserted into the composition track. To specify an empty time range, pass NSNull for the track and a time range of starting at kCMTimeInvalid with a duration of the desired empty edit.
+*/
+- (BOOL)insertTimeRanges:(NSArray<NSValue *> *)timeRanges ofTracks:(NSArray<AVAssetTrack *> *)tracks atTime:(CMTime)startTime error:(NSError * _Nullable * _Nullable)outError NS_AVAILABLE(10_8, 5_0);
+
+/*!
+    @method         insertEmptyTimeRange:
+    @abstract       Adds or extends an empty timeRange within the composition track.
+    @param          timeRange
+                    Specifies the empty timeRange to be inserted.
+    @discussion
+      If you insert an empty timeRange into the track, any media that was presented during that interval prior to the insertion will be presented instead immediately afterward.
+      The exact meaning of the term "empty timeRange" depends upon the mediaType of the track. For example, an empty timeRange in a sound track presents silence.
+      Note that you cannot add empty time ranges to the end of a composition track.
 */
 - (void)insertEmptyTimeRange:(CMTimeRange)timeRange;
 
 /*!
-	@method			removeTimeRange:
-	@abstract		Removes a specified timeRange from the track.
-	@param			timeRange
-					Specifies the timeRange to be removed.
-	@discussion
-		Removal of a timeRange does not cause the track to be removed from the composition.
-		Instead it removes or truncates track segments that intersect with the timeRange.
+    @method         removeTimeRange:
+    @abstract       Removes a specified timeRange from the track.
+    @param          timeRange
+                    Specifies the timeRange to be removed.
+    @discussion
+      Removal of a timeRange does not cause the track to be removed from the composition. Instead it removes or truncates track segments that intersect with the timeRange.
 */
 - (void)removeTimeRange:(CMTimeRange)timeRange;
 
 /*!
-	@method			scaleTimeRange:toDuration:
-	@abstract		Changes the duration of a timeRange of the track.
-	@param			timeRange
-					Specifies the timeRange of the track to be scaled.
-	@param			duration
-					Specifies the new duration of the timeRange.
-	@discussion
-		Each trackSegment affected by the scaling operation will be presented at a rate equal to
-		source.duration / target.duration of its resulting timeMapping.
+    @method         scaleTimeRange:toDuration:
+    @abstract       Changes the duration of a timeRange of the track.
+    @param          timeRange
+                    Specifies the timeRange of the track to be scaled.
+    @param          duration
+                    Specifies the new duration of the timeRange.
+    @discussion
+      Each trackSegment affected by the scaling operation will be presented at a rate equal to source.duration / target.duration of its resulting timeMapping.
 */
 - (void)scaleTimeRange:(CMTimeRange)timeRange toDuration:(CMTime)duration;
 
 /*!
-	@method			validateTrackSegments:error:
-	@abstract		Tests an array of AVCompositionTrackSegments to determine whether they conform
-					to the timing rules noted above (see the property key @"trackSegments").
-	@param			trackSegments
-					The array of AVCompositionTrackSegments to be validated.
-	@param			error
-					If validation fais, returns information about the failure.
-	@discussion
-		The array is tested for suitability for setting as the value of the trackSegments property.
-		If a portion of an existing trackSegments array is to be modified, the modification can
-		be made via an instance of NSMutableArray, and the resulting array can be tested via
-		-validateTrackSegments:error:.
+    @method         validateTrackSegments:error:
+    @abstract       Tests an array of AVCompositionTrackSegments to determine whether they conform to the timing rules noted above (see the property key @"trackSegments").
+    @param          trackSegments
+                    The array of AVCompositionTrackSegments to be validated.
+    @param          error
+                    If validation fais, returns information about the failure.
+    @result         YES if validation suceeds, otherwise NO.
+    @discussion
+      The array is tested for suitability for setting as the value of the trackSegments property. If a portion of an existing trackSegments array is to be modified, the modification can be made via an instance of NSMutableArray, and the resulting array can be tested via -validateTrackSegments:error:.
 */
-- (BOOL)validateTrackSegments:(NSArray<AVCompositionTrackSegment *> *)trackSegments error:(NSError * __nullable * __nullable)outError;
+- (BOOL)validateTrackSegments:(NSArray<AVCompositionTrackSegment *> *)trackSegments error:(NSError * _Nullable * _Nullable)outError;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVError.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVError.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVError.h	2016-02-20 01:13:12.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVError.h	2016-05-25 07:19:44.000000000 +0200
@@ -99,5 +99,6 @@
 #if !TARGET_OS_IPHONE
     AVErrorCreateContentKeyRequestFailed NS_AVAILABLE(10_11, NA) = -11860,
 #endif
-	
+    AVErrorUnsupportedOutputSettings NS_AVAILABLE(10_12, 10_0) = -11861,
+	AVErrorOperationNotAllowed NS_AVAILABLE(10_12, 10_0) = -11862,
 };
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVFAudio.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVFAudio.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVFAudio.h	2015-09-30 23:18:01.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVFAudio.h	2016-05-25 07:19:44.000000000 +0200
@@ -1,43 +1,9 @@
-//
-//  AVFAudio.h
-//  Copyright © 2015 Apple. All rights reserved.
-//
+/*
+	File:           AVFAudio.h
+	Framework:      AVFoundation
+	
+	Copyright 2016 Apple Inc. All rights reserved.
+*/
 
-#import <AVFoundation/AVAudioBuffer.h>
-#import <AVFoundation/AVAudioChannelLayout.h>
-#import <AVFoundation/AVAudioConnectionPoint.h>
-#import <AVFoundation/AVAudioConverter.h>
-#import <AVFoundation/AVAudioEngine.h>
-#import <AVFoundation/AVAudioEnvironmentNode.h>
-#import <AVFoundation/AVAudioFile.h>
-#import <AVFoundation/AVAudioFormat.h>
-#import <AVFoundation/AVAudioIONode.h>
-#import <AVFoundation/AVAudioMixerNode.h>
-#import <AVFoundation/AVAudioMixing.h>
-#import <AVFoundation/AVAudioNode.h>
-#import <AVFoundation/AVAudioPlayer.h>
-#import <AVFoundation/AVAudioPlayerNode.h>
-#import <AVFoundation/AVAudioRecorder.h>
-#import <AVFoundation/AVAudioSequencer.h>
-#import <AVFoundation/AVAudioSettings.h>
-#import <AVFoundation/AVAudioTime.h>
-#import <AVFoundation/AVAudioTypes.h>
-#import <AVFoundation/AVAudioUnit.h>
-#import <AVFoundation/AVAudioUnitComponent.h>
-#import <AVFoundation/AVAudioUnitDelay.h>
-#import <AVFoundation/AVAudioUnitDistortion.h>
-#import <AVFoundation/AVAudioUnitEQ.h>
-#import <AVFoundation/AVAudioUnitEffect.h>
-#import <AVFoundation/AVAudioUnitGenerator.h>
-#import <AVFoundation/AVAudioUnitMIDIInstrument.h>
-#import <AVFoundation/AVAudioUnitReverb.h>
-#import <AVFoundation/AVAudioUnitSampler.h>
-#import <AVFoundation/AVAudioUnitTimeEffect.h>
-#import <AVFoundation/AVAudioUnitTimePitch.h>
-#import <AVFoundation/AVAudioUnitVarispeed.h>
-#import <AVFoundation/AVMIDIPlayer.h>
+#import <AVFAudio/AVFAudio.h>
 
-#if TARGET_OS_IPHONE
-#import <AVFoundation/AVAudioSession.h>
-#import <AVFoundation/AVSpeechSynthesis.h>
-#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVFoundation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVFoundation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVFoundation.h	2016-02-25 00:53:33.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVFoundation.h	2016-05-25 07:19:44.000000000 +0200
@@ -9,10 +9,19 @@
 
 */
 
+#import <TargetConditionals.h>
+#if TARGET_OS_WATCH
+#if ! __has_include(<AVFoundation/AVAnimation.h>)
+#define AVF_IS_WATCHOS_SDK 1
+#endif
+#endif
+
 #import <AVFoundation/AVBase.h>
 
+#if ! AVF_IS_WATCHOS_SDK
 #import <AVFoundation/AVAnimation.h>
 #import <AVFoundation/AVAsset.h>
+#import <AVFoundation/AVAssetCache.h>
 #import <AVFoundation/AVAssetExportSession.h>
 #import <AVFoundation/AVAssetImageGenerator.h>
 #import <AVFoundation/AVAssetReader.h>
@@ -43,7 +52,11 @@
 #import <AVFoundation/AVCompositionTrack.h>
 #import <AVFoundation/AVCompositionTrackSegment.h>
 #import <AVFoundation/AVError.h>
+#endif
+
 #import <AVFoundation/AVFAudio.h>
+
+#if ! AVF_IS_WATCHOS_SDK
 #import <AVFoundation/AVMediaFormat.h>
 #import <AVFoundation/AVMediaSelection.h>
 #import <AVFoundation/AVMediaSelectionGroup.h>
@@ -65,6 +78,7 @@
 #endif
 #import <AVFoundation/AVPlayerItemTrack.h>
 #import <AVFoundation/AVPlayerLayer.h>
+#import <AVFoundation/AVPlayerLooper.h>
 #import <AVFoundation/AVPlayerMediaSelectionCriteria.h>
 #import <AVFoundation/AVSampleBufferDisplayLayer.h>
 #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
@@ -79,3 +93,4 @@
 #import <AVFoundation/AVVideoCompositing.h>
 #import <AVFoundation/AVVideoComposition.h>
 #import <AVFoundation/AVVideoSettings.h>
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMIDIPlayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMIDIPlayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMIDIPlayer.h	2015-09-30 23:18:01.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMIDIPlayer.h	2016-05-25 07:19:44.000000000 +0200
@@ -1,94 +1,9 @@
 /*
- 	File:		AVMIDIPlayer.h
- 	Framework:	AVFoundation
- 
- 	Copyright (c) 2014-2015 Apple Inc. All Rights Reserved.
+	File:           AVMIDIPlayer.h
+	Framework:      AVFoundation
+	
+	Copyright 2016 Apple Inc. All rights reserved.
 */
 
-#import <Foundation/Foundation.h>
+#import <AVFAudio/AVMIDIPlayer.h>
 
-NS_ASSUME_NONNULL_BEGIN
-
-@class AVAudioTime;
-
-/*! @typedef AVMIDIPlayerCompletionHandler
-	@abstract Generic callback block.
- */
-typedef void (^AVMIDIPlayerCompletionHandler)(void);
-
-/*! @class AVMIDIPlayer
-	@abstract A player for music file formats (MIDI, iMelody).
- */
-NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface AVMIDIPlayer : NSObject {
-@protected
-	void *_impl;
-}
-
-/*!	@method initWithContentsOfURL:soundBankURL:error:
- 	@abstract Create a player with the contents of the file specified by the URL.
-	@discussion
- 		'bankURL' should contain the path to a SoundFont2 or DLS bank to be used
- 		by the MIDI synthesizer.  For OSX it can be set to nil for the default,
- 		but for iOS it must always refer to a valid bank file.
-*/
-- (nullable instancetype)initWithContentsOfURL:(NSURL *)inURL soundBankURL:(NSURL * __nullable)bankURL error:(NSError **)outError;
-
-/*!	@method initWithData:soundBankURL:error:
-	@abstract Create a player with the contents of the data object
-	@discussion
-		'bankURL' should contain the path to a SoundFont2 or DLS bank to be used
-		by the MIDI synthesizer.  For OSX it can be set to nil for the default,
-		but for iOS it must always refer to a valid bank file.
- */
-- (nullable instancetype)initWithData:(NSData *)data soundBankURL:(NSURL * __nullable)bankURL error:(NSError **)outError;
-
-/* transport control */
-
-/*! @method prepareToPlay
-	@abstract Get ready to play the sequence by prerolling all events
-	@discussion
-		Happens automatically on play if it has not already been called, but may produce a delay in startup.
- */
-- (void)prepareToPlay;
-
-/*! @method play:
-	@abstract Play the sequence.
- */
-- (void)play:(AVMIDIPlayerCompletionHandler __nullable)completionHandler;
-
-/*! @method stop
-	@abstract Stop playing the sequence.
- */
-- (void)stop;
-
-/* properties */
-
-/*! @property duration
-	@abstract The length of the currently loaded file in seconds.
- */
-@property(nonatomic, readonly) NSTimeInterval duration;
-
-/*! @property playing
-	@abstract Indicates whether or not the player is playing
- */
-@property(nonatomic, readonly, getter=isPlaying) BOOL playing;
-
-/*! @property rate
-	@abstract The playback rate of the player
-	@discussion
-		1.0 is normal playback rate.  Rate must be > 0.0.
- */
-@property (nonatomic) float rate;
-
-/*! @property currentPosition
-	@abstract The current playback position in seconds
-	@discussion
-		Setting this positions the player to the specified time.  No range checking on the time value is done.
- 		This can be set while the player is playing, in which case playback will resume at the new time.
- */
-@property(nonatomic) NSTimeInterval currentPosition;
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMediaFormat.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMediaFormat.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMediaFormat.h	2015-09-30 23:18:02.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMediaFormat.h	2016-05-25 07:22:17.000000000 +0200
@@ -94,6 +94,14 @@
 AVF_EXPORT NSString *const AVMediaCharacteristicFrameBased  NS_AVAILABLE(10_7, 4_0);
 
 /*!
+ @constant AVMediaCharacteristicUsesWideGamutColorSpace
+ @abstract A media characteristic that indicates that a track uses a wide gamut color space and therefore may make use of colors that cannot be accurately represented otherwise.
+ @discussion
+ A wide color space such as AVVideo*_P3_D65 contains additional dynamic range that may benefit from special treatment when compositing. Care should be taken to avoid clamping. Non-wide spaces include AVVideo*_ITU_R_709_2 and AVVideo*_SMPTE_C.
+*/
+AVF_EXPORT NSString *const AVMediaCharacteristicUsesWideGamutColorSpace NS_AVAILABLE(10_12, 10_0);
+
+/*!
  @constant AVMediaCharacteristicIsMainProgramContent
  @abstract A media characteristic that indicates that a track or media selection option includes content that's marked by the content author as intrinsic to the presentation of the asset.
  @discussion
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataFormat.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataFormat.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataFormat.h	2016-02-25 00:50:14.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataFormat.h	2016-05-25 07:22:18.000000000 +0200
@@ -89,6 +89,13 @@
 // ISO UserData keys (includes 3GPP keys)
 AVF_EXPORT NSString *const AVMetadataISOUserDataKeyCopyright                             NS_AVAILABLE(10_7, 4_0);
 AVF_EXPORT NSString *const AVMetadataISOUserDataKeyTaggedCharacteristic                  NS_AVAILABLE(10_10, 8_0);
+
+/*!
+ @constant		AVMetadataISOUserDataKeyDate
+ @abstract		ISO User data key for the content creation date/time.
+ @discussion	The value is date and time, formatted according to ISO 8601, when the content was created. For clips captured by recording devices, this is typically the date and time when the clip’s recording started. When stored in AV(Mutable)MetadataItem, the value type must be either NSDate or NSString. When NSString is used, the value uses one of ISO 8601 formats such as "2016-01-11T17:31:10Z".
+*/
+AVF_EXPORT NSString *const AVMetadataISOUserDataKeyDate                                  NS_AVAILABLE(10_12, 10_0);
 AVF_EXPORT NSString *const AVMetadata3GPUserDataKeyCopyright                             NS_AVAILABLE(10_7, 4_0);
 AVF_EXPORT NSString *const AVMetadata3GPUserDataKeyAuthor                                NS_AVAILABLE(10_7, 4_0);
 AVF_EXPORT NSString *const AVMetadata3GPUserDataKeyPerformer                             NS_AVAILABLE(10_7, 4_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataIdentifiers.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataIdentifiers.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataIdentifiers.h	2015-09-30 23:18:02.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataIdentifiers.h	2016-05-24 07:21:27.000000000 +0200
@@ -77,6 +77,7 @@
 
 // ISO UserData (includes 3GPP)
 AVF_EXPORT NSString *const AVMetadataIdentifierISOUserDataCopyright                             NS_AVAILABLE(10_10, 8_0);
+AVF_EXPORT NSString *const AVMetadataIdentifierISOUserDataDate                                  NS_AVAILABLE(10_12, 10_0);
 AVF_EXPORT NSString *const AVMetadataIdentifierISOUserDataTaggedCharacteristic                  NS_AVAILABLE(10_10, 8_0);
 AVF_EXPORT NSString *const AVMetadataIdentifier3GPUserDataCopyright                             NS_AVAILABLE(10_10, 8_0);
 AVF_EXPORT NSString *const AVMetadataIdentifier3GPUserDataAuthor                                NS_AVAILABLE(10_10, 8_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataItem.h	2015-09-30 23:18:02.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataItem.h	2016-05-25 07:22:18.000000000 +0200
@@ -3,7 +3,7 @@
 
 	Framework:  AVFoundation
  
-	Copyright 2010-2015 Apple Inc. All rights reserved.
+	Copyright 2010-2016 Apple Inc. All rights reserved.
 
 */
 
@@ -101,7 +101,7 @@
 
 /* The following two methods of the AVAsynchronousKeyValueLoading protocol are re-declared here so that they can be annotated with availability information. See AVAsynchronousKeyValueLoading.h for documentation. */
 
-- (AVKeyValueStatus)statusOfValueForKey:(NSString *)key error:(NSError * __nullable * __nullable)outError NS_AVAILABLE(10_7, 4_2);
+- (AVKeyValueStatus)statusOfValueForKey:(NSString *)key error:(NSError * _Nullable * _Nullable)outError NS_AVAILABLE(10_7, 4_2);
 
 - (void)loadValuesAsynchronouslyForKeys:(NSArray<NSString *> *)keys completionHandler:(nullable void (^)(void))handler NS_AVAILABLE(10_7, 4_2);
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataObject.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataObject.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataObject.h	2015-09-30 23:18:02.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataObject.h	2016-05-25 04:40:25.000000000 +0200
@@ -19,11 +19,10 @@
     AVMetadataObject is an abstract class that defines an interface for a metadata object used by AVFoundation.
  
  @discussion
-    AVMetadataObject provides an abstract interface for metadata associated with a piece of media.  One example 
-    is face metadata that might be detected in a picture. All metadata objects have a time, duration, bounds, and type.
+    AVMetadataObject provides an abstract interface for metadata associated with a piece of media. One example is face metadata that might be detected in a picture. All metadata objects have a time, duration, bounds, and type.
  
     The concrete AVMetadataFaceObject is used by AVCaptureMetadataOutput for face detection.
-*/
+ */
 NS_CLASS_AVAILABLE(10_10, 6_0) __TVOS_PROHIBITED
 @interface AVMetadataObject : NSObject
 {
@@ -37,10 +36,8 @@
     The media time associated with this metadata object.
  
  @discussion
-    The value of this property is a CMTime associated with the metadata object. For capture, it is the time at 
-	which this object was captured. If this metadata object originates from a CMSampleBuffer, its time matches
-    the sample buffer's presentation time. This property may return kCMTimeInvalid.
-*/
+    The value of this property is a CMTime associated with the metadata object. For capture, it is the time at which this object was captured. If this metadata object originates from a CMSampleBuffer, its time matches the sample buffer's presentation time. This property may return kCMTimeInvalid.
+ */
 @property(readonly) CMTime time;
 
 /*!
@@ -49,10 +46,8 @@
     The media duration associated with this metadata object.
  
  @discussion
-    The value of this property is a CMTime representing the duration of the metadata object. If this metadata 
-    object originates from a CMSampleBuffer, its duration matches the sample buffer's duration. This property 
-    may return kCMTimeInvalid.
-*/
+    The value of this property is a CMTime representing the duration of the metadata object. If this metadata object originates from a CMSampleBuffer, its duration matches the sample buffer's duration. This property may return kCMTimeInvalid.
+ */
 @property(readonly) CMTime duration;
 
 /*!
@@ -61,11 +56,8 @@
     The bounding rectangle of the receiver.
  
  @discussion
-    The value of this property is a CGRect representing the bounding rectangle of the object with respect to the 
-    picture in which it resides.  The rectangle's origin is top left.  If the metadata originates from video, bounds 
-    may be expressed as scalar values from 0. - 1.  If the original video has been scaled down, the bounds of the 
-    metadata object still are meaningful.  This property may return CGRectZero if the metadata has no bounds.
-*/
+    The value of this property is a CGRect representing the bounding rectangle of the object with respect to the picture in which it resides. The rectangle's origin is top left. If the metadata originates from video, bounds may be expressed as scalar values from 0. - 1. If the original video has been scaled down, the bounds of the metadata object still are meaningful. This property may return CGRectZero if the metadata has no bounds.
+ */
 @property(readonly) CGRect bounds;
 
 /*!
@@ -74,19 +66,20 @@
     An identifier for the metadata object.
  
  @discussion
-    The value of this property is an NSString representing the type of the metadata object.  Clients inspecting
-    a collection of metadata objects can use this property to filter objects with a matching type.
-*/
+    The value of this property is an NSString representing the type of the metadata object. Clients inspecting a collection of metadata objects can use this property to filter objects with a matching type.
+ */
 @property(readonly) NSString *type;
 
 @end
 
 /*!
  @constant AVMetadataObjectTypeFace
- @abstract An identifier for an instance of AVMetadataFaceObject.
+ @abstract
+    An identifier for an instance of AVMetadataFaceObject.
+ 
  @discussion
     AVMetadataFaceObject objects return this constant as their type.
-*/
+ */
 AVF_EXPORT NSString *const AVMetadataObjectTypeFace NS_AVAILABLE(10_10, 6_0) __TVOS_PROHIBITED;
 
 @class AVMetadataFaceObjectInternal;
@@ -97,11 +90,10 @@
     AVMetadataFaceObject is a concrete subclass of AVMetadataObject defining the features of a detected face.
  
  @discussion
-    AVMetadataFaceObject represents a single detected face in a picture.  It is an immutable object
-    describing the various features found in the face.
+    AVMetadataFaceObject represents a single detected face in a picture. It is an immutable object describing the various features found in the face.
 
-    On supported platforms, AVCaptureMetadataOutput outputs arrays of detected face objects.  See AVCaptureOutput.h.
-*/
+    On supported platforms, AVCaptureMetadataOutput outputs arrays of detected face objects. See AVCaptureOutput.h.
+ */
 NS_CLASS_AVAILABLE(10_10, 6_0) __TVOS_PROHIBITED
 @interface AVMetadataFaceObject : AVMetadataObject <NSCopying>
 {
@@ -115,20 +107,15 @@
     A unique number associated with the receiver.
  
  @discussion
-    The value of this property is an NSInteger indicating the unique identifier of this face in the picture.
-    When a new face enters the picture, it is assigned a new unique identifier.  faceIDs are not re-used as
-    faces leave the picture and new ones enter.  Faces that leave the picture then re-enter are assigned
-    a new faceID.
-*/
+    The value of this property is an NSInteger indicating the unique identifier of this face in the picture. When a new face enters the picture, it is assigned a new unique identifier. faceIDs are not re-used as faces leave the picture and new ones enter. Faces that leave the picture then re-enter are assigned a new faceID.
+ */
 @property(readonly) NSInteger faceID;
 
 /*!
  @property hasRollAngle
  @abstract
     A BOOL indicating whether the rollAngle property is valid for this receiver.
- 
- @discussion
-*/
+ */
 @property(readonly) BOOL hasRollAngle;
 
 /*!
@@ -137,10 +124,8 @@
     The roll angle of the face in degrees.
  
  @discussion
-    The value of this property is a CGFloat indicating the face's angle of roll (or tilt) in degrees.
-    A value of 0.0 indicates that the face is level in the picture.  If -hasRollAngle returns NO,
-    then reading this property throws an NSGenericException.
-*/
+    The value of this property is a CGFloat indicating the face's angle of roll (or tilt) in degrees. A value of 0.0 indicates that the face is level in the picture. If -hasRollAngle returns NO, then reading this property throws an NSGenericException.
+ */
 @property(readonly) CGFloat rollAngle;
 
 /*!
@@ -149,7 +134,7 @@
     A BOOL indicating whether the yawAngle property is valid for this receiver.
  
  @discussion
-*/
+ */
 @property(readonly) BOOL hasYawAngle;
 
 /*!
@@ -158,17 +143,17 @@
     The yaw angle of the face in degrees.
  
  @discussion
-    The value of this property is a CGFloat indicating the face's angle of yaw (or turn) in degrees.
-    A value of 0.0 indicates that the face is straight on in the picture.  If -hasYawAngle returns NO,
-    then reading this property throws an NSGenericException.
-*/
+    The value of this property is a CGFloat indicating the face's angle of yaw (or turn) in degrees. A value of 0.0 indicates that the face is straight on in the picture. If -hasYawAngle returns NO, then reading this property throws an NSGenericException.
+ */
 @property(readonly) CGFloat yawAngle;
 
 @end
 
 /*!
  @constant AVMetadataObjectTypeUPCECode
- @abstract An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeUPCECode.
+ @abstract
+    An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeUPCECode.
+
  @discussion
     AVMetadataMachineReadableCodeObject objects generated from UPC-E codes return this constant as their type.
  */
@@ -176,7 +161,9 @@
 
 /*!
  @constant AVMetadataObjectTypeCode39Code
- @abstract An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeCode39Code.
+ @abstract
+    An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeCode39Code.
+ 
  @discussion
     AVMetadataMachineReadableCodeObject objects generated from Code 39 codes return this constant as their type.
  */
@@ -184,7 +171,9 @@
 
 /*!
  @constant AVMetadataObjectTypeCode39Mod43Code
- @abstract An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeCode39Mod43Code.
+ @abstract
+    An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeCode39Mod43Code.
+ 
  @discussion
     AVMetadataMachineReadableCodeObject objects generated from Code 39 mod 43 codes return this constant as their type.
  */
@@ -192,7 +181,9 @@
 
 /*!
  @constant AVMetadataObjectTypeEAN13Code
- @abstract An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeEAN13Code.
+ @abstract
+    An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeEAN13Code.
+ 
  @discussion
     AVMetadataMachineReadableCodeObject objects generated from EAN-13 (including UPC-A) codes return this constant as their type.
  */
@@ -200,7 +191,9 @@
 
 /*!
  @constant AVMetadataObjectTypeEAN8Code
- @abstract An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeEAN8Code.
+ @abstract
+    An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeEAN8Code.
+ 
  @discussion
     AVMetadataMachineReadableCodeObject objects generated from EAN-8 codes return this constant as their type.
  */
@@ -208,7 +201,9 @@
 
 /*!
  @constant AVMetadataObjectTypeCode93Code
- @abstract An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeCode93Code.
+ @abstract
+    An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeCode93Code.
+ 
  @discussion
     AVMetadataMachineReadableCodeObject objects generated from Code 93 codes return this constant as their type.
  */
@@ -216,7 +211,9 @@
 
 /*!
  @constant AVMetadataObjectTypeCode128Code
- @abstract An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeCode128Code.
+ @abstract
+    An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeCode128Code.
+ 
  @discussion
     AVMetadataMachineReadableCodeObject objects generated from Code 128 codes return this constant as their type.
  */
@@ -224,7 +221,9 @@
 
 /*!
  @constant AVMetadataObjectTypePDF417Code
- @abstract An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypePDF417Code.
+ @abstract
+    An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypePDF417Code.
+ 
  @discussion
     AVMetadataMachineReadableCodeObject objects generated from PDF417 codes return this constant as their type.
  */
@@ -232,7 +231,9 @@
 
 /*!
  @constant AVMetadataObjectTypeQRCode
- @abstract An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeQRCode.
+ @abstract
+    An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeQRCode.
+ 
  @discussion
     AVMetadataMachineReadableCodeObject objects generated from QR codes return this constant as their type.
  */
@@ -240,7 +241,9 @@
 
 /*!
  @constant AVMetadataObjectTypeAztecCode
- @abstract An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeAztecCode.
+ @abstract
+    An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeAztecCode.
+ 
  @discussion
     AVMetadataMachineReadableCodeObject objects generated from Aztec codes return this constant as their type.
  */
@@ -248,26 +251,32 @@
 
 /*!
  @constant AVMetadataObjectTypeInterleaved2of5Code
- @abstract An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeInterleaved2of5Code.
+ @abstract
+    An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeInterleaved2of5Code.
+ 
  @discussion
-	AVMetadataMachineReadableCodeObject objects generated from Interleaved 2 of 5 codes return this constant as their type.
-*/
+    AVMetadataMachineReadableCodeObject objects generated from Interleaved 2 of 5 codes return this constant as their type.
+ */
 AVF_EXPORT NSString *const AVMetadataObjectTypeInterleaved2of5Code NS_AVAILABLE(NA, 8_0) __TVOS_PROHIBITED;
 
 /*!
  @constant AVMetadataObjectTypeITF14Code
- @abstract An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeITF14Code.
+ @abstract
+    An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeITF14Code.
+ 
  @discussion
-	AVMetadataMachineReadableCodeObject objects generated from ITF14 codes return this constant as their type.
-*/
+    AVMetadataMachineReadableCodeObject objects generated from ITF14 codes return this constant as their type.
+ */
 AVF_EXPORT NSString *const AVMetadataObjectTypeITF14Code NS_AVAILABLE(NA, 8_0) __TVOS_PROHIBITED;
 
 /*!
  @constant AVMetadataObjectTypeDataMatrixCode
- @abstract An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeDataMatrixCode.
+ @abstract
+    An identifier for an instance of AVMetadataMachineReadableCodeObject having a type AVMetadataObjectTypeDataMatrixCode.
+ 
  @discussion
-	AVMetadataMachineReadableCodeObject objects generated from DataMatrix codes return this constant as their type.
-*/
+    AVMetadataMachineReadableCodeObject objects generated from DataMatrix codes return this constant as their type.
+ */
 AVF_EXPORT NSString *const AVMetadataObjectTypeDataMatrixCode NS_AVAILABLE(NA, 8_0) __TVOS_PROHIBITED;
 
 @class AVMetadataMachineReadableCodeObjectInternal;
@@ -275,14 +284,12 @@
 /*!
  @class AVMetadataMachineReadableCodeObject
  @abstract
-    AVMetadataMachineReadableCodeObject is a concrete subclass of AVMetadataObject defining the features of a detected one-dimensional
-    or two-dimensional barcode.
+    AVMetadataMachineReadableCodeObject is a concrete subclass of AVMetadataObject defining the features of a detected one-dimensional or two-dimensional barcode.
  
  @discussion
-    AVMetadataMachineReadableCodeObject represents a single detected machine readable code in a picture.  It is an immutable object
-    describing the features and payload of a barcode.
+    AVMetadataMachineReadableCodeObject represents a single detected machine readable code in a picture. It is an immutable object describing the features and payload of a barcode.
  
-    On supported platforms, AVCaptureMetadataOutput outputs arrays of detected machine readable code objects.  See AVCaptureMetadataOutput.h.
+    On supported platforms, AVCaptureMetadataOutput outputs arrays of detected machine readable code objects. See AVCaptureMetadataOutput.h.
  */
 NS_CLASS_AVAILABLE(NA, 7_0) __TVOS_PROHIBITED
 @interface AVMetadataMachineReadableCodeObject : AVMetadataObject
@@ -297,21 +304,17 @@
     The points defining the (X,Y) locations of the corners of the machine-readable code.
  
  @discussion
-    The value of this property is an NSArray of CFDictionaries, each of which has been created from a CGPoint using 
-    CGPointCreateDictionaryRepresentation(), representing the coordinates of the corners of the object with respect to the image 
-    in which it resides.  If the metadata originates from video, the points may be expressed as scalar values from 0. - 1. The 
-    points in the corners differ from the bounds rectangle in that bounds is axis-aligned to orientation of the captured image, 
-    and the values of the corners reside within the bounds rectangle. The points are arranged in counter-clockwise order 
-    (clockwise if the code or image is mirrored), starting with the top-left of the code in its canonical orientation.
+    The value of this property is an NSArray of CFDictionaries, each of which has been created from a CGPoint using CGPointCreateDictionaryRepresentation(), representing the coordinates of the corners of the object with respect to the image in which it resides. If the metadata originates from video, the points may be expressed as scalar values from 0. - 1. The points in the corners differ from the bounds rectangle in that bounds is axis-aligned to orientation of the captured image, and the values of the corners reside within the bounds rectangle. The points are arranged in counter-clockwise order (clockwise if the code or image is mirrored), starting with the top-left of the code in its canonical orientation.
  */
 @property(readonly) NSArray *corners;
 
 /*!
  @property stringValue
- @abstract Returns the receiver's errorCorrectedData decoded into a human-readable string.
+ @abstract
+    Returns the receiver's errorCorrectedData decoded into a human-readable string.
+ 
  @discussion
-    The value of this property is an NSString created by decoding the binary payload according to the format of the machine
-    readable code.  Returns nil if a string representation cannot be created from the payload.
+    The value of this property is an NSString created by decoding the binary payload according to the format of the machine readable code. Returns nil if a string representation cannot be created from the payload.
  */
 @property(readonly) NSString *stringValue;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayer.h	2015-09-30 23:18:02.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayer.h	2016-05-24 07:21:27.000000000 +0200
@@ -3,7 +3,7 @@
 
 	Framework:  AVFoundation
  
-	Copyright 2010-2015 Apple Inc. All rights reserved.
+	Copyright 2010-2016 Apple Inc. All rights reserved.
 
 */
 
@@ -83,7 +83,7 @@
 	@result			An instance of AVPlayer
 	@discussion		Useful in order to play items for which an AVAsset has previously been created. See -[AVPlayerItem initWithAsset:].
 */
-+ (instancetype)playerWithPlayerItem:(AVPlayerItem *)item;
++ (instancetype)playerWithPlayerItem:(nullable AVPlayerItem *)item;
 
 /*!
 	@method			initWithURL:
@@ -101,7 +101,7 @@
 	@result			An instance of AVPlayer
 	@discussion		Useful in order to play items for which an AVAsset has previously been created. See -[AVPlayerItem initWithAsset:].
 */
-- (instancetype)initWithPlayerItem:(AVPlayerItem *)item;
+- (instancetype)initWithPlayerItem:(nullable AVPlayerItem *)item;
 
 /*!
  @property status
@@ -132,23 +132,113 @@
 
 @interface AVPlayer (AVPlayerPlaybackControl)
 
-/* indicates the current rate of playback; 0.0 means "stopped", 1.0 means "play at the natural rate of the current item" */
+/*!
+ @property		rate
+ @abstract		Indicates the desired rate of playback; 0.0 means "paused", 1.0 indicates a desire to play at the natural rate of the current item.
+ @discussion
+ Setting the value of rate to 0.0 pauses playback, causing the value of timeControlStatus to change to AVPlayerTimeControlStatusPaused.
+ Setting the rate to a non-zero value causes the value of timeControlStatus to become either AVPlayerTimeControlStatusWaitingToPlayAtSpecifiedRate or AVPlayerTimeControlStatusPlaying, depending on whether sufficient media data has been buffered for playback to occur and whether the player's default behavior of waiting in order to minimize stalling is permitted. See discussion of AVPlayerTimeControlStatus for more details.
+ 
+ AVPlayer can reset the desired rate to 0.0 when a change in overall state requires playback to be halted, such as when an interruption occurs on iOS, as announced by AVAudioSession, or when the playback buffer becomes empty and playback stalls while automaticallyWaitsToMinimizeStalling is NO.
+
+ The effective rate of playback may differ from the desired rate even while timeControlStatus is AVPlayerTimeControlStatusPlaying, if the processing algorithm in use for managing audio pitch requires quantization of playback rate. For information about quantization of rates for audio processing, see AVAudioProcessingSettings.h. You can always obtain the effective rate of playback from the currentItem's timebase; see the timebase property of AVPlayerItem.
+ */
 @property (nonatomic) float rate;
 
 /*!
-	@method			play
-	@abstract		Begins playback of the current item.
-	@discussion		Same as setting rate to 1.0.
-*/
+ @method		play
+ @abstract		Signals the desire to begin playback at the current item's natural rate.
+ @discussion	Equivalent to setting the value of rate to 1.0.
+ */
 - (void)play;
 
 /*!
-	@method			pause
-	@abstract		Pauses playback.
-	@discussion		Same as setting rate to 0.0.
-*/
+ @method		pause
+ @abstract		Pauses playback.
+ @discussion	Equivalent to setting the value of rate to 0.0.
+ */
 - (void)pause;
 
+/*!
+ @enum AVPlayerTimeControlStatus
+ @abstract
+	These constants are the allowable values of AVPlayer's timeControlStatus property. This discussion pertains when automaticallyWaitsToMinimizeStalling is YES, the default setting, and exceptions are discussed in connection with automaticallyWaitsToMinimizeStalling.
+ 
+ @constant	 AVPlayerTimeControlStatusPaused
+	This state is entered upon receipt of a -pause message, an invocation of -setRate: with a value of 0.0, when a change in overall state requires playback to be halted, such as when an interruption occurs on iOS, as announced by AVAudioSession.
+    In this state, playback is paused indefinitely and will not resume until 1) a subsequent -play message is received or 2) a -setRate: or -playImmediatelyAtRate: message with a non-zero value for rate is received and sufficient media data has been buffered for playback to proceed.
+ @constant	 AVPlayerTimeControlStatusWaitingToPlayAtSpecifiedRate
+    This state is entered when 1) the playback buffer becomes empty and playback stalls in AVPlayerTimeControlStatusPlaying, 2) when rate is set from zero to non-zero in AVPlayerTimeControlStatusPaused and insufficient media data has been buffered for playback to occur, or 3) when the player has no item to play, i.e. when the receiver's currentItem is nil.
+    In this state, the value of the rate property is not currently effective but instead indicates the rate at which playback will start or resume. Refer to the value of reasonForWaitingToPlay for details about why the receiver is waiting and the conditions that allow waitStatus to change to AVPlayerWaitStatusPlaying.
+	While waiting for buffering, you can attempt to start playback of any available media data via -playImmediatelyAtRate:.
+ @constant	 AVPlayerTimeControlStatusPlaying
+	In this state, playback is currently progressing and rate changes will take effect immediately. Should playback stall because of insufficient media data, timeControlStatus will change to AVPlayerTimeControlStatusWaitingToPlayAtSpecifiedRate.
+ */
+typedef NS_ENUM(NSInteger, AVPlayerTimeControlStatus) {
+	AVPlayerTimeControlStatusPaused,
+	AVPlayerTimeControlStatusWaitingToPlayAtSpecifiedRate,
+	AVPlayerTimeControlStatusPlaying
+} NS_ENUM_AVAILABLE(10_12, 10_0);
+
+
+/*!
+ @property		timeControlStatus
+ @abstract		Indicates whether playback is currently paused indefinitely, suspend while waiting for appropriate conditions, or in progress.
+ @discussion    For possible values and discussion, see AVPlayerTimeControlStatus.
+ 
+When automaticallyWaitsToMinimizeStalling is YES, absent intervention in the form of invocations of -setRate: or -pause or, on iOS, an interruption that requires user intervention before playback can resume, the value of the property timeControlStatus automatically changes between AVPlayerTimeControlStatusPlaying and AVPlayerTimeControlStatusWaitingToPlayAtSpecifiedRate depending on whether sufficient media data is available to continue playback. This property is key value observable.
+*/
+@property (nonatomic, readonly) AVPlayerTimeControlStatus timeControlStatus NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @constant AVPlayerWaitingToMinimizeStallsReason
+ @abstract Indicates that the player is waiting for appropriate playback buffer conditions before starting playback
+ @discussion
+	The player is waiting for playback because automaticallyWaitToMinimizeStalling is YES and playback at the specified rate would likely cause the playback buffer to become empty before playback completes. Playback will resume when 1) playback at the specified rate will likely complete without a stall or 2) the playback buffer becomes full, meaning no forther buffering of media data is possible.
+	When the value of automaticallyWaitsToMinimizeStalling is NO, timeControlStatus cannot become AVPlayerTimeControlStatusWaitingToPlayAtSpecifiedRate for this reason.
+ */
+AVF_EXPORT NSString *const AVPlayerWaitingToMinimizeStallsReason NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @constant AVPlayerWaitingWhileEvaluatingBufferingRateReason
+ @abstract Indicates that the player is monitoring the playback buffer fill rate to determine if playback is likely to complete without interruptions.
+ @discussion
+	The player is waiting for playback because automaticallyWaitToMinimizeStalling is YES and it has not yet determined if starting playback at the specified rate would likely cause the buffer to become empty. When the brief initial monitoring period is over, either playback will begin or the value of reasonForWaitingToPlayAtSpecifiedRate will switch to AVPlayerWaitingToMinimizeStallsReason.
+	Recommended practice is not to show UI indicating the waiting state to the user while the value of reasonForWaitingToPlayAtSpecifiedRate is AVPlayerWaitingWhileEvaluatingBufferingRateReason.
+ */
+AVF_EXPORT NSString *const AVPlayerWaitingWhileEvaluatingBufferingRateReason NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @constant AVPlayerWaitingWithNoItemToPlayReason
+ @abstract Indicates that the AVPlayer is waiting because its currentItem is nil
+ @discussion
+	The player is waiting for playback because automaticallyWaitToMinimizeStalling is YES and the value of currentItem is nil. When an item becomes available, either because of a call to -replaceCurrentItemWithPlayerItem: or  -insertItem: afterItem:, playback will begin or the value of reasonForWaitingToPlay will change.
+ */
+AVF_EXPORT NSString *const AVPlayerWaitingWithNoItemToPlayReason NS_AVAILABLE(10_12, 10_0);
+
+
+/*!
+ @property		reasonForWaitingToPlay
+ @abstract		Indicates the reason for waiting when the value of timeControlStatus is AVPlayerTimeControlStatusWaitingToPlayAtSpecifiedRate
+ @discussion
+    When the value of timeControlStatus is AVPlayerTimeControlStatusWaitingToPlayAtSpecifiedRate, this property describes why the player is currently waiting. It is nil otherwise.
+    You can use the value of reasonForWaitingToPlay to show UI indicating the player's waiting state conditionally.
+    This property is key value observable.
+    Possible values are AVPlayerWaitingWithNoItemToPlayReason, AVPlayerWaitingWhileEvaluatingBufferingRateReason, and AVPlayerWaitingToMinimizeStallsReason.
+*/
+
+@property (nonatomic, readonly, nullable) NSString *reasonForWaitingToPlay NS_AVAILABLE(10_12, 10_0);
+
+
+/*!
+ @method		playImmediatelyAtRate:
+ @abstract		Immediately plays the available media data at the specified rate.
+ @discussion
+ When the player's currentItem has a value of NO for playbackBufferEmpty, this method causes the value of rate to change to the specified rate, the value of timeControlStatus to change to AVPlayerTimeControlStatusPlaying, and the receiver to play the available media immediately, whether or not prior buffering of media data is sufficient to ensure smooth playback.
+ If insufficient media data is buffered for playback to start (e.g. if the current item has a value of YES for playbackBufferEmpty), the receiver will act as if the buffer became empty during playback, except that no AVPlayerItemPlaybackStalledNotification will be posted.
+ */
+- (void)playImmediatelyAtRate:(float)rate NS_AVAILABLE(10_12, 10_0);
+
 @end
 
 
@@ -282,6 +372,26 @@
 
 @interface AVPlayer (AVPlayerAdvancedRateControl)
 
+
+/*!
+ @property		automaticallyWaitsToMinimizeStalling
+ @abstract		Indicates that the player is allowed to delay playback at the specified rate in order to minimize stalling
+ @discussion
+ 
+ When this property is YES, whenever 1) the rate is set from zero to non-zero or 2) the playback buffer becomes empty and playback stalls, the player will attempt to determine if, at the specified rate, its currentItem will play to the end without interruptions. Should it determine that such interruptions would occur and these interruptions can be avoided by delaying the start or resumption of playback, the value of timeControlStatus will become AVPlayerTimeControlStatusWaitingToPlayAtSpecifiedRate and playback will start automatically when the likelihood of stalling has been minimized.
+ 
+ You may want to set this property to NO when you need precise control over playback start times, e.g., when synchronizing multiple instances of AVPlayer. If the value of this property is NO, reasonForWaitingToPlay cannot assume a value of AVPlayerWaitingToMinimizeStallsReason.
+ This implies that setting rate to a non-zero value in AVPlayerTimeControlStatusPaused will cause playback to start immediately as long as the playback buffer is not empty. When the playback buffer becomes empty during AVPlayerTimeControlStatusPlaying and playback stalls, playback state will switch to AVPlayerTimeControlStatusPaused and the rate will become 0.0.
+ 
+ Changing the value of this property to NO while the value of timeControlStatus is AVPlayerTimeControlStatusWaitingToPlayAtSpecifiedRate with a reasonForWaitingToPlay of AVPlayerWaitingToMinimizeStallsReason will cause the player to attempt playback at the specified rate immediately.
+ 
+ For clients linked against iOS 10.0 and running on that version or later or linked against OS X 10.12 and running on that version or later, the default value of this property is YES.
+ In versions of iOS prior to iOS 10.0 and versions of OS X prior to 10.12, this property is unavailable, and the behavior of the AVPlayer corresponds to the type of content being played. For streaming content, including HTTP Live Streaming, the AVPlayer acts as if automaticallyWaitsToMinimizeStalling is YES. For file-based content, including file-based content accessed via progressive http download, the AVPlayer acts as if automaticallyWaitsToMinimizeStalling is NO. */
+
+@property (nonatomic) BOOL automaticallyWaitsToMinimizeStalling NS_AVAILABLE(10_12, 10_0);
+
+
+
 /*!
 	@method			setRate:time:atHostTime:
 	@abstract		Simultaneously sets the playback rate and the relationship between the current item's current time and host time.
@@ -290,14 +400,14 @@
 					The current item's timebase is adjusted so that its time will be (or was) itemTime when host time is (or was) hostClockTime.
 					In other words: if hostClockTime is in the past, the timebase's time will be interpolated as though the timebase has been running at the requested rate since that time.  If hostClockTime is in the future, the timebase will immediately start running at the requested rate from an earlier time so that it will reach the requested itemTime at the requested hostClockTime.  (Note that the item's time will not jump backwards, but instead will sit at itemTime until the timebase reaches that time.)
 
-					Note that advanced rate control is not currently supported for HTTP Live Streaming.
+					Note that setRate:time:atHostTime: is not currently supported for HTTP Live Streaming or when automaticallyWaitsToMinimizeStalling is YES. For clients linked against iOS 10.0 and later or OS X 12.0 and later, invoking setRate:time:atHostTime: when automaticallyWaitsToMinimizeStalling is YES will raise an NSInvalidArgument exception.
 	@param itemTime	The time to start playback from, specified precisely (i.e., with zero tolerance).
 					Pass kCMTimeInvalid to use the current item's current time.
 	@param hostClockTime
 					The host time at which to start playback.
 					If hostClockTime is specified, the player will not ensure that media data is loaded before the timebase starts moving.
 					If hostClockTime is kCMTimeInvalid, the rate and time will be set together, but without external synchronization;
-					a host time in the near future will be used, allowing some time for data media loading.
+					a host time in the near future will be used, allowing some time for media data loading.
 */
 - (void)setRate:(float)rate time:(CMTime)itemTime atHostTime:(CMTime)hostClockTime NS_AVAILABLE(10_8, 6_0);
 
@@ -519,6 +629,8 @@
 
 @end
 
+#endif // TARGET_OS_IPHONE
+
 /*
 	@category		AVPlayer (AVPlayerProtectedContent)
 	@abstract		Methods supporting protected content.
@@ -542,12 +654,10 @@
 		current item. These requirements are inherent to the content itself and cannot be externally specified.
 		If the current item does not require external protection, the value of this property will be NO.
  */
-@property (nonatomic, readonly) BOOL outputObscuredDueToInsufficientExternalProtection NS_AVAILABLE_IOS(6_0);
+@property (nonatomic, readonly) BOOL outputObscuredDueToInsufficientExternalProtection NS_AVAILABLE(10_12, 6_0);
 
 @end
 
-#endif // TARGET_OS_IPHONE
-
 /*!
 	@class			AVQueuePlayer
  
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItem.h	2016-02-20 00:13:12.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItem.h	2016-05-25 04:39:23.000000000 +0200
@@ -3,7 +3,7 @@
 
 	Framework:  AVFoundation
  
-	Copyright 2010-2015 Apple Inc. All rights reserved.
+	Copyright 2010-2016 Apple Inc. All rights reserved.
 
 */
 
@@ -94,7 +94,7 @@
  @result		An instance of AVPlayerItem.
  @discussion	Equivalent to +playerItemWithAsset:, passing [AVAsset assetWithURL:URL] as the value of asset.
  */
-+ (AVPlayerItem *)playerItemWithURL:(NSURL *)URL;
++ (instancetype)playerItemWithURL:(NSURL *)URL;
 
 /*!
  @method		playerItemWithAsset:
@@ -103,7 +103,7 @@
  @result		An instance of AVPlayerItem.
  @discussion	Equivalent to +playerItemWithAsset:automaticallyLoadedAssetKeys:, passing @[ @"duration" ] as the value of automaticallyLoadedAssetKeys.
   */
-+ (AVPlayerItem *)playerItemWithAsset:(AVAsset *)asset;
++ (instancetype)playerItemWithAsset:(AVAsset *)asset;
 
 /*!
  @method		playerItemWithAsset:automaticallyLoadedAssetKeys:
@@ -114,7 +114,7 @@
  @result		An instance of AVPlayerItem.
  @discussion	The value of each key in automaticallyLoadedAssetKeys will be automatically be loaded by the underlying AVAsset before the receiver achieves the status AVPlayerItemStatusReadyToPlay; i.e. when the item is ready to play, the value of -[[AVPlayerItem asset] statusOfValueForKey:error:] will be one of the terminal status values greater than AVKeyValueStatusLoading.
  */
-+ (AVPlayerItem *)playerItemWithAsset:(AVAsset *)asset automaticallyLoadedAssetKeys:(nullable NSArray<NSString *> *)automaticallyLoadedAssetKeys NS_AVAILABLE(10_9, 7_0);
++ (instancetype)playerItemWithAsset:(AVAsset *)asset automaticallyLoadedAssetKeys:(nullable NSArray<NSString *> *)automaticallyLoadedAssetKeys NS_AVAILABLE(10_9, 7_0);
 
 /*!
  @method		initWithURL:
@@ -332,6 +332,7 @@
  @param				time
  @discussion		Use this method to seek to a specified time for the item.
 					The time seeked to may differ from the specified time for efficiency. For sample accurate seeking see seekToTime:toleranceBefore:toleranceAfter:.
+					If the seek time is outside of seekable time ranges as indicated by seekableTimeRanges property, the seek request will be cancelled.
  */
 - (void)seekToTime:(CMTime)time;
 
@@ -344,6 +345,7 @@
  					The completion handler for any prior seek request that is still in process will be invoked immediately with the finished parameter 
  					set to NO. If the new request completes without being interrupted by another seek request or by any other operation the specified 
  					completion handler will be invoked with the finished parameter set to YES. 
+					If the seek time is outside of seekable time ranges as indicated by seekableTimeRanges property, the seek request will be cancelled and the completion handler will be invoked with the finished parameter set to NO.
  */
 - (void)seekToTime:(CMTime)time completionHandler:(void (^)(BOOL finished))completionHandler NS_AVAILABLE(10_7, 5_0);
 
@@ -359,6 +361,7 @@
 					Messaging this method with beforeTolerance:kCMTimePositiveInfinity and afterTolerance:kCMTimePositiveInfinity is the same as messaging seekToTime: directly.
 					Seeking is constrained by the collection of seekable time ranges. If you seek to a time outside all of the seekable ranges the seek will result in a currentTime
 					within the seekable ranges.
+					If the seek time is outside of seekable time ranges as indicated by seekableTimeRanges property, the seek request will be cancelled.
  */
 - (void)seekToTime:(CMTime)time toleranceBefore:(CMTime)toleranceBefore toleranceAfter:(CMTime)toleranceAfter;
 
@@ -376,6 +379,7 @@
 					The completion handler for any prior seek request that is still in process will be invoked immediately with the finished parameter set to NO. If the new 
 					request completes without being interrupted by another seek request or by any other operation the specified completion handler will be invoked with the 
 					finished parameter set to YES.
+					If the seek time is outside of seekable time ranges as indicated by seekableTimeRanges property, the seek request will be cancelled and the completion handler will be invoked with the finished parameter set to NO.
  */
 - (void)seekToTime:(CMTime)time toleranceBefore:(CMTime)toleranceBefore toleranceAfter:(CMTime)toleranceAfter completionHandler:(void (^)(BOOL finished))completionHandler NS_AVAILABLE(10_7, 5_0);
 
@@ -558,6 +562,14 @@
  */
 @property (nonatomic, assign) BOOL canUseNetworkResourcesForLiveStreamingWhilePaused NS_AVAILABLE(10_11, 9_0);
 
+/*!
+@property	preferredForwardBufferDuration
+@abstract	Indicates the media duration the caller prefers the player to buffer from the network ahead of the playhead to guard against playback disruption. 
+@discussion	The value is in seconds. If it is set to 0, the player will choose an appropriate level of buffering for most use cases.
+			Note that setting this property to a low value will increase the chance that playback will stall and re-buffer, while setting it to a high value will increase demand on system resources.
+*/
+@property (nonatomic) NSTimeInterval preferredForwardBufferDuration NS_AVAILABLE(10_12, 10_0);
+
 @end
 
 
@@ -732,6 +744,7 @@
 @private
 	AVPlayerItemAccessLogInternal	*_playerItemAccessLog;
 }
+AV_INIT_UNAVAILABLE
 
 /*!
  @method		extendedLogData
@@ -774,6 +787,7 @@
 @private
 	AVPlayerItemErrorLogInternal	*_playerItemErrorLog;
 }
+AV_INIT_UNAVAILABLE
 
 /*!
  @method		extendedLogData
@@ -817,6 +831,7 @@
 @private
 	AVPlayerItemAccessLogEventInternal	*_playerItemAccessLogEvent;
 }
+AV_INIT_UNAVAILABLE
 
 /*!
  @property		numberOfSegmentsDownloaded
@@ -942,6 +957,22 @@
 @property (nonatomic, readonly) double indicatedBitrate;
 
 /*!
+ @property		averageVideoBitrate
+ @abstract		The average bitrate of video track if it is unmuxed. Average bitrate of combined content if muxed. Measured in bits per second.
+ @discussion	Value is negative if unknown. Corresponds to "c-avg-video-bitrate".
+ This property is not observable.
+ */
+@property (nonatomic, readonly) double averageVideoBitrate NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property		averageAudioBitrate
+ @abstract		The average bitrate of audio track. This is not available if audio is muxed with video. Measured in bits per second.
+ @discussion	Value is negative if unknown. Corresponds to "c-avg-audio-bitrate".
+ This property is not observable.
+ */
+@property (nonatomic, readonly) double averageAudioBitrate NS_AVAILABLE(10_12, 10_0);
+
+/*!
  @property		numberOfDroppedVideoFrames
  @abstract		The total number of dropped video frames.
  @discussion	Value is negative if unknown. Corresponds to "c-frames-dropped".
@@ -1027,6 +1058,7 @@
 @private
 	AVPlayerItemErrorLogEventInternal	*_playerItemErrorLogEvent;
 }
+AV_INIT_UNAVAILABLE
 
 /*!
  @property		date
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItemOutput.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItemOutput.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItemOutput.h	2015-09-30 23:18:02.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItemOutput.h	2016-05-24 07:21:27.000000000 +0200
@@ -177,6 +177,23 @@
 - (instancetype)initWithPixelBufferAttributes:(nullable NSDictionary<NSString *, id> *)pixelBufferAttributes NS_DESIGNATED_INITIALIZER;
 
 /*!
+	@method			initWithOutputSettings:
+	@abstract		Returns an instance of AVPlayerItemVideoOutput, initialized with the specified output settings, for video image output.
+	@param			outputSettings
+					The client requirements for output CVPixelBuffers, expressed using the constants in AVVideoSettings.h.
+ 
+					For uncompressed video output, start with kCVPixelBuffer* keys in <CoreVideo/CVPixelBuffer.h>.
+	
+					In addition to the keys in CVPixelBuffer.h, uncompressed video settings dictionaries may also contain the following keys:
+ 
+					AVVideoAllowWideColorKey
+ 
+	@result			An instance of AVPlayerItemVideoOutput.
+ */
+
+- (instancetype)initWithOutputSettings:(nullable NSDictionary<NSString *, id> *)outputSettings NS_AVAILABLE(10_12, 10_0) NS_DESIGNATED_INITIALIZER;
+
+/*!
 	@method			hasNewPixelBufferForItemTime:
 	@abstract		Query if any new video output is available for an item time.
 	@discussion
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerLooper.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerLooper.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerLooper.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerLooper.h	2016-05-25 04:39:24.000000000 +0200
@@ -0,0 +1,148 @@
+/*
+ File:  AVPlayerLooper.h
+
+	Framework:  AVFoundation
+
+	Copyright 2016 Apple Inc. All rights reserved.
+
+ */
+
+/*!
+ @class AVPlayerLooper
+
+ @abstract
+    AVPlayerLooper is a helper object that repeatedly plays an AVPlayerItem with an AVQueuePlayer
+
+ @discussion
+    The same result can be accomplished with AVQueuePlayer directly, but AVPlayerLooper provides a simpler interface to loop a single AVPlayerItem with an option to specify a time range. AVPlayerLooper only supports looping for forward playback (positive player rate). Behavior is undefined for negative player rate.
+
+    Sample usage code:
+    // Create player and configure
+    AVQueuePlayer *player = [[AVQueuePlayer alloc] init];
+    AVPlayerLayer *playerLayer = [AVPlayerLayer playerLayerWithPlayer:player];
+    [player pause];
+    // Create looping item
+    AVPlayerItem* itemToLoop = [AVPlayerItem playerItemWithURL:@“loop.mov”];
+    // Create looping helper object. Loop item segment from 5sec to 7sec
+    AVPlayerLooper* looper = [AVPlayerLooper playerLooperWithPlayer:player templateItem:itemToLoop timeRange:CMTimeRangeMake(CMTimeMake(5000,1000), CMTimeMake(2000,1000))];
+    // Perform any other set up operations like setting AVPlayerItemDataOutputs on the looping item replicas
+    // Start playback
+    [player play];
+    // itemToLoop between 5s and 7s plays repeatedly
+    ....
+    // To end the looping
+    [looper disableLooping];
+    // Player will play through the end of the current looping item
+ */
+
+
+#import <AVFoundation/AVBase.h>
+#import <CoreMedia/CMTime.h>
+#import <CoreMedia/CMTimeRange.h>
+#import <Foundation/Foundation.h>
+#import <AVFoundation/AVPlayer.h>
+#import <AVFoundation/AVPlayerItem.h>
+
+@class AVPlayerLooperInternal;
+
+NS_ASSUME_NONNULL_BEGIN
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface AVPlayerLooper : NSObject
+{
+@private
+	AVPlayerLooperInternal *_looper;
+}
+AV_INIT_UNAVAILABLE
+
+/*!
+ @method playerLooperWithPlayer:templateItem:timeRange:
+ @abstract
+    Returns an instance of AVPlayerLooper to loop specified AVPlayerItem within the specified time range with specified AVQueuePlayer.
+ @param player
+    Must not be nil
+ @param itemToLoop
+    Must not be nil
+ @param loopRange
+    Playback time range in [0, itemToLoop's duration]. kCMTimeRangeInvalid means [0, itemToLoop's duration].
+ @result
+    An instance of AVPlayerLooper.
+ @discussion
+    The specified AVPlayerItem will be used as a template to generate at least 3 AVPlayerItem replicas and the replicas will be inserted into specified AVQueuePlayer's play queue to accomplish the looping playback. The specified AVPlayerItem should have its asset.duration property loaded beforehand so initialization would not be blocked until the duration value is known. The specified AVPlayerItem will not be used in the actual looping playback. Furthermore, AVPlayerItem replicas will be generated at initialization time so any changes made to the specified AVPlayerItem's property afterwards will not be reflected in the replicas used for looping playback. Specified CMTimeRange will limit each item loop iteration to playing within the specified time range. To play from beginning and the whole duration of the item, specify kCMTimeRangeInvalid for the range parameter. Time range will be accomplished by seeking to range start time and setting AVPlayerItem's forwardPlaybackEndTime property on the looping item replicas. Client should not modify AVQueuePlayer's play queue while AVPlayerLooper is performing the looping. AVPlayerLooper will insert the replica items before any existing items in the specified AVQueuePlayer's play queue and change the actionAtItemEnd to AVPlayerActionAtItemEndAdvance if required. AVQueuePlayer's play queue and actionAtItemEnd will be restored when -disableLooping method is called and then current looping item replicas completes playback or when AVPlayerLooper is destroyed. While AVPlayerLooper is being initialized, the specified AVQueuePlayer will be paused (rate of 0.0) if necessary and the original player rate will be restored after initialization completes. The client shall set the specified AVQueuePlayer's rate to 0 beforehand if additional set-up work needs to be performed after AVPlayerLooper initialization and before starting looping playback. An NSInvalidArgumentException will be raised if the player and template item are not specified or the template item has a 0 duration. An NSInvalidArgumentException will be raised if a valid time range has a duration of 0 or is not contained within time 0 and duration of the templateItem.
+*/
++ (instancetype)playerLooperWithPlayer:(AVQueuePlayer *)player templateItem:(AVPlayerItem *)itemToLoop timeRange:(CMTimeRange)loopRange;
+
+/*!
+ @method playerLooperWithPlayer:templateItem:
+ @abstract
+    Returns an instance of AVPlayerLooper to loop specified AVPlayerItem with specified AVQueuePlayer.
+ @param player
+    Must not be nil
+ @param itemToLoop
+    Must not be nil
+ @result
+    An instance of AVPlayerLooper.
+ @discussion
+    Equivalent to +playerLooperWithPlayer:templateItem:timeRange: and passing in kCMTimeRangeInvalid for timeRange parameter.
+*/
++ (instancetype)playerLooperWithPlayer:(AVQueuePlayer *)player templateItem:(AVPlayerItem *)itemToLoop;
+
+/*!
+ @method initWithPlayer:templateItem:timeRange:
+ @abstract
+    Initializes an instance of AVPlayerLooper to loop specified AVPlayerItem within the specified time range with specified AVQueuePlayer.
+ @param player
+    Must not be nil
+ @param itemToLoop
+    Must not be nil
+ @param loopRange
+    Playback time range in [0, itemToLoop's duration]. kCMTimeRangeInvalid means [0, itemToLoop's duration].
+ @result
+    An initialized AVPlayerLooper.
+ @discussion
+    The specified AVPlayerItem will be used as a template to generate at least 3 AVPlayerItem replicas and the replicas will be inserted into specified AVQueuePlayer's play queue to accomplish the looping playback. The specified AVPlayerItem should have its asset.duration property loaded beforehand so initialization would not be blocked until the duration value is known. The specified AVPlayerItem will not be used in the actual looping playback. Furthermore, AVPlayerItem replicas will be generated at initialization time so any changes made to the specified AVPlayerItem's property afterwards will not be reflected in the replicas used for looping playback. Specified CMTimeRange will limit each item loop iteration to playing within the specified time range. To play from beginning and the whole duration of the item, specify kCMTimeRangeInvalid for the range parameter. Time range will be accomplished by seeking to range start time and setting AVPlayerItem's forwardPlaybackEndTime property on the looping item replicas. Client should not modify AVQueuePlayer's play queue while AVPlayerLooper is performing the looping. AVPlayerLooper will insert the replica items before any existing items in the specified AVQueuePlayer's play queue and change the actionAtItemEnd to AVPlayerActionAtItemEndAdvance if required. AVQueuePlayer's play queue and actionAtItemEnd will be restored when -disableLooping method is called and then current looping item replicas completes playback or when AVPlayerLooper is destroyed. While AVPlayerLooper is being initialized, the specified AVQueuePlayer will be paused (rate of 0.0) if necessary and the original player rate will be restored after initialization completes. The client shall set the specified AVQueuePlayer's rate to 0 beforehand if additional set-up work needs to be performed after AVPlayerLooper initialization and before starting looping playback. An NSInvalidArgumentException will be raised if the player and template item are not specified or the template item has a 0 duration. An NSInvalidArgumentException will be raised if a valid time range has a duration of 0 or is not contained within time 0 and duration of the templateItem.
+ */
+- (instancetype)initWithPlayer:(AVQueuePlayer *)player templateItem:(AVPlayerItem *)itemToLoop timeRange:(CMTimeRange)loopRange NS_DESIGNATED_INITIALIZER;
+
+/*!
+ @method disableLooping
+ @abstract
+    Disables the item looping
+ @discussion
+    AVPlayerLooper will stop performing player queue operations for looping and let the current looping item replica play to the end. The player's original actionAtItemEnd property will be restored afterwards.
+ */
+- (void)disableLooping;
+
+/*!
+ @property loopingEnabled
+ @abstract
+    Boolean specifying whether AVPlayerLooper is looping or not.
+ @discussion
+    loopingEnabled returns NO if disableLooping method is called or if an error is encountered that prevents looping playback, which can occur either when a looping item fails to become ready for playback or when a looping item fails to play to its end time. Errors arising in the former case can be discovered by observing the AVPlayer keypath @“currentItem.error”. Errors arising in the latter case can be discovered by handling the NSNotification AVPlayerItemFailedToPlayToEndTimeNotification. This property is key value observable.
+ */
+@property (nonatomic, readonly, getter=isLoopingEnabled) BOOL loopingEnabled;
+
+/*!
+ @property loopCount
+ @abstract
+    Number of times the specified AVPlayerItem has been played
+ @discussion
+    Starts at 0 and increments when the player starts playback of the AVPlayerItem again. This property is key value observable.
+ */
+@property (nonatomic, readonly) NSInteger loopCount;
+
+/*!
+ @property loopingPlayerItems
+ @abstract
+    Returns an array containing replicas of specified AVPlayerItem used to accomplish the looping
+ @discussion
+    AVPlayerLooper creates replicas of the template AVPlayerItem using -copyWithZone: and inserts the replicas in the specified AVQueuePlayer to accomplish the looping. The AVPlayerItem replicas are for informational purposes and to allow the client to apply properties that are not transferred from the template AVPlayerItem to the replicas. The client can determine the number of replicas created and can listen for notifications and property changes from the replicas if desired. AVPlayerItemOutputs and AVPlayerItemMediaDataCollectors are not transferred to the replicas so the client should add them to each replica if desired. The client shall not modify the properties on the replicas that would disrupt looping playback. Examples of such properties are playhead time/date, selected media option, and forward playback end time.
+ @result
+    Array containing replicas of specified AVPlayerItem
+ */
+@property (nonatomic, readonly) NSArray<AVPlayerItem *> *loopingPlayerItems;
+
+@end
+
+NS_ASSUME_NONNULL_END
+
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVSampleBufferDisplayLayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVSampleBufferDisplayLayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVSampleBufferDisplayLayer.h	2015-09-30 23:18:03.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVSampleBufferDisplayLayer.h	2016-05-26 02:32:48.000000000 +0200
@@ -31,7 +31,7 @@
 	@constant	 AVQueuedSampleBufferRenderingStatusRendering
 	Indicates at least one sample buffer has been enqueued on the receiver.
 	@constant	 AVQueuedSampleBufferRenderingStatusFailed
-	Terminal state indicating that the receiver can no longer render sample buffers because of an error. The error is described by
+	Indicates that the receiver cannot currently enqueue or render sample buffers because of an error. The error is described by
 	the value of AVSampleBufferDisplayLayer's error property.
  */
 typedef NS_ENUM(NSInteger, AVQueuedSampleBufferRenderingStatus) {
@@ -81,7 +81,9 @@
 /*!
 	@property		status
 	@abstract		The ability of the display layer to be used for enqueuing sample buffers.
-	@discussion		The value of this property is an AVQueuedSampleBufferRenderingStatus that indicates whether the receiver can be used for enqueuing sample buffers. When the value of this property is AVQueuedSampleBufferRenderingStatusFailed, the receiver can no longer be used and a new instance needs to be created in its place. When this happens, clients can check the value of the error property to determine the failure. This property is key value observable.
+	@discussion		The value of this property is an AVQueuedSampleBufferRenderingStatus that indicates whether the receiver can be used for enqueuing and rendering sample buffers. When the value of this property is AVQueuedSampleBufferRenderingStatusFailed, clients can check the value of the error property to determine the failure. To resume rendering sample buffers using the display layer after a failure, clients must first reset the status to AVQueuedSampleBufferRenderingStatusUnknown. This can be achieved by invoking -flush on the display layer.
+		
+					This property is key value observable.
  */
 @property (nonatomic, readonly) AVQueuedSampleBufferRenderingStatus status NS_AVAILABLE(10_10, 8_0);
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVSpeechSynthesis.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVSpeechSynthesis.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVSpeechSynthesis.h	2015-09-30 23:18:03.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVSpeechSynthesis.h	2016-05-25 07:19:45.000000000 +0200
@@ -1,160 +1,9 @@
 /*
- File:  AVSpeechSynthesis.h
- 
- Framework:  AVFoundation
- 
- Copyright 2013-2015 Apple Inc. All rights reserved.
- */
+	File:           AVSpeechSynthesis.h
+	Framework:      AVFoundation
+	
+	Copyright 2016 Apple Inc. All rights reserved.
+*/
 
-#import <AVFoundation/AVBase.h>
-#import <Foundation/Foundation.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-typedef NS_ENUM(NSInteger, AVSpeechBoundary) {
-    AVSpeechBoundaryImmediate,
-    AVSpeechBoundaryWord
-} NS_ENUM_AVAILABLE_IOS(7_0);
-
-typedef NS_ENUM(NSInteger, AVSpeechSynthesisVoiceQuality) {
-    AVSpeechSynthesisVoiceQualityDefault = 1,
-    AVSpeechSynthesisVoiceQualityEnhanced
-} NS_ENUM_AVAILABLE_IOS(9_0);
-
-AVF_EXPORT const float AVSpeechUtteranceMinimumSpeechRate NS_AVAILABLE_IOS(7_0);
-AVF_EXPORT const float AVSpeechUtteranceMaximumSpeechRate NS_AVAILABLE_IOS(7_0);
-AVF_EXPORT const float AVSpeechUtteranceDefaultSpeechRate NS_AVAILABLE_IOS(7_0);
-
-// Use the Alex identifier with voiceWithIdentifier:. If the voice is present on the system,
-// an AVSpeechSynthesisVoice will be returned. Alex is en-US only.
-AVF_EXPORT NSString *const AVSpeechSynthesisVoiceIdentifierAlex NS_AVAILABLE_IOS(9_0);
-
-@protocol AVSpeechSynthesizerDelegate;
-
-/*!
- @class AVSpeechSynthesisVoice
- @abstract
- AVSpeechSynthesisVoice encapsulates the attributes of the voice used to synthesize speech on the system.
- 
- @discussion
- Retrieve a voice by specifying the language code your text should be spoken in, or by using voiceWithIdentifier
- for a known voice identifier.
- */
-NS_CLASS_AVAILABLE_IOS(7_0)
-@interface AVSpeechSynthesisVoice : NSObject<NSSecureCoding>
-
-+ (NSArray<AVSpeechSynthesisVoice *> *)speechVoices;
-+ (NSString *)currentLanguageCode;
-
-/*!
- @method        voiceWithLanguage:
- @abstract      Use a BCP-47 language tag to specify the desired language and region.
- @param			language
- Specifies the BCP-47 language tag that represents the voice.
- @discussion
- The default is the system's region and language.
- Passing in nil will return the default voice.
- Passing in an invalid languageCode will return nil.
- Will return enhanced quality voice if available, default quality otherwise.
- Examples: en-US (U.S. English), fr-CA (French Canadian)
- */
-+ (nullable AVSpeechSynthesisVoice *)voiceWithLanguage:(nullable NSString *)languageCode;
-
-/*!
- @method        voiceWithIdentifier:
- @abstract      Retrieve a voice by its identifier.
- @param			identifier
- A unique identifier for a voice.
- @discussion
- Passing in an invalid identifier will return nil.
- Returns nil if the identifier is valid, but the voice is not available on device (i.e. not yet downloaded by the user).
- */
-+ (nullable AVSpeechSynthesisVoice *)voiceWithIdentifier:(NSString *)identifier NS_AVAILABLE_IOS(9_0);
-
-@property(nonatomic, readonly) NSString *language;
-@property(nonatomic, readonly) NSString *identifier NS_AVAILABLE_IOS(9_0);
-@property(nonatomic, readonly) NSString *name NS_AVAILABLE_IOS(9_0);
-@property(nonatomic, readonly) AVSpeechSynthesisVoiceQuality quality NS_AVAILABLE_IOS(9_0);
-
-@end
-
-/*!
- @class AVSpeechUtterance
- @abstract
- AVSpeechUtterance is the atom of speaking a string or pausing the synthesizer.
- 
- @discussion
- To start speaking, specify the AVSpeechSynthesisVoice and the string to be spoken, then optionally change the rate, pitch or volume if desired.
- */
-NS_CLASS_AVAILABLE_IOS(7_0)
-@interface AVSpeechUtterance : NSObject<NSCopying, NSSecureCoding>
-
-+ (instancetype)speechUtteranceWithString:(NSString *)string;
-
-- (instancetype)initWithString:(NSString *)string;
-
-/* If no voice is specified, the system's default will be used. */
-@property(nonatomic, retain, nullable) AVSpeechSynthesisVoice *voice;
-
-@property(nonatomic, readonly) NSString *speechString;
-
-/* Setting these values after a speech utterance has been enqueued will have no effect. */
-
-@property(nonatomic) float rate;             // Values are pinned between AVSpeechUtteranceMinimumSpeechRate and AVSpeechUtteranceMaximumSpeechRate.
-@property(nonatomic) float pitchMultiplier;  // [0.5 - 2] Default = 1
-@property(nonatomic) float volume;           // [0-1] Default = 1
-
-@property(nonatomic) NSTimeInterval preUtteranceDelay;    // Default is 0.0
-@property(nonatomic) NSTimeInterval postUtteranceDelay;   // Default is 0.0
-
-
-@end
-
-/*!
- @class AVSpeechSynthesizer
- @abstract
- AVSpeechSynthesizer allows speaking of speech utterances with a basic queuing mechanism.
- 
- @discussion
- Create an instance of AVSpeechSynthesizer to start generating synthesized speech by using AVSpeechUtterance objects.
- */
-NS_CLASS_AVAILABLE_IOS(7_0)
-@interface AVSpeechSynthesizer : NSObject
-
-@property(nonatomic, assign, nullable) id<AVSpeechSynthesizerDelegate> delegate;
-
-@property(nonatomic, readonly, getter=isSpeaking) BOOL speaking;
-@property(nonatomic, readonly, getter=isPaused) BOOL paused;
-
-/* AVSpeechUtterances are queued by default. 
-   Enqueing the same AVSpeechUtterance that is already enqueued or is speaking will raise an exception. */
-- (void)speakUtterance:(AVSpeechUtterance *)utterance;
-
-/* These methods will operate on the speech utterance that is speaking. Returns YES if it succeeds, NO for failure. */
-
-/* Call stopSpeakingAtBoundary: to interrupt current speech and clear the queue. */
-- (BOOL)stopSpeakingAtBoundary:(AVSpeechBoundary)boundary;
-- (BOOL)pauseSpeakingAtBoundary:(AVSpeechBoundary)boundary;
-- (BOOL)continueSpeaking;
-
-@end
-
-/*!
- @protocol AVSpeechSynthesizerDelegate
- @abstract
- Defines an interface for delegates of AVSpeechSynthesizer to receive notifications of important speech utterance events.
- */
-@protocol AVSpeechSynthesizerDelegate <NSObject>
-
-@optional
-- (void)speechSynthesizer:(AVSpeechSynthesizer *)synthesizer didStartSpeechUtterance:(AVSpeechUtterance *)utterance;
-- (void)speechSynthesizer:(AVSpeechSynthesizer *)synthesizer didFinishSpeechUtterance:(AVSpeechUtterance *)utterance;
-- (void)speechSynthesizer:(AVSpeechSynthesizer *)synthesizer didPauseSpeechUtterance:(AVSpeechUtterance *)utterance;
-- (void)speechSynthesizer:(AVSpeechSynthesizer *)synthesizer didContinueSpeechUtterance:(AVSpeechUtterance *)utterance;
-- (void)speechSynthesizer:(AVSpeechSynthesizer *)synthesizer didCancelSpeechUtterance:(AVSpeechUtterance *)utterance;
-
-- (void)speechSynthesizer:(AVSpeechSynthesizer *)synthesizer willSpeakRangeOfSpeechString:(NSRange)characterRange utterance:(AVSpeechUtterance *)utterance;
-@end
-
-NS_ASSUME_NONNULL_END
+#import <AVFAudio/AVSpeechSynthesis.h>
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoCompositing.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoCompositing.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoCompositing.h	2015-09-30 23:18:03.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoCompositing.h	2016-05-24 07:21:29.000000000 +0200
@@ -161,6 +161,16 @@
 */
 - (void)cancelAllPendingVideoCompositionRequests;
 
+/*!
+ @property supportsWideColorSourceFrames
+ @abstract
+	Indicates that clients can handle frames that contains wide color properties.
+ 
+ @discussion 
+	Controls whether the client will receive frames that contain wide color information. Care should be taken to avoid clamping.
+ */
+@property (nonatomic, readonly) BOOL supportsWideColorSourceFrames NS_AVAILABLE(10_12, 10_0);
+
 @end
 
 /*!
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoComposition.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoComposition.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoComposition.h	2015-09-30 23:18:04.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoComposition.h	2016-05-25 04:40:26.000000000 +0200
@@ -3,7 +3,7 @@
 
 	Framework:  AVFoundation
  
-	Copyright 2010-2015 Apple Inc. All rights reserved.
+	Copyright 2010-2016 Apple Inc. All rights reserved.
 
 */
 
@@ -90,10 +90,69 @@
 
 @end
 
+/*
+ @category	   AVVideoCompositionColorimetery
+ @abstract
+    Indicates the color space of the frames output from the video composition.
+ @discussion
+    Collectively the properties colorPrimaries, colorYCbCrMatrix, and colorTransferFunction define the color space that the rendered frames will be tagged with. For custom video compositing these properties are also used to specify the required color space of the source frames.
+
+    Examples of common color spaces:
+	
+        TODO: SD
+        TODO: HD
+        TODO: HD-P3
+
+    How to preserve the color space of the source frames:
+ 
+        Decide which color space to be preserved by examining the source asset's video tracks. Copy the source track's primaries, matrix and transfer function into the video composition's colorPrimaries, colorYCbCrMatrix and colorTransferFunction respectively.
+		
+        TODO: <rdar://problem/25496972> sample code showing how to inspect the source asset track's primaries etc and setup a video composition to preserve them. Ideally we'll show the narrow-HD case and the wide-P3 case.
+
+        - When using custom video compositing
+			Setting these properties will cause source frames to be converted into the specified color space and tagged as such. New frames allocated using -[AVVideoCompositionRenderContext newPixelBuffer] will also be tagged correctly.
+
+        - When using Core Image via videoCompositionWithAsset:options:applyingCIFiltersWithHandler:
+			Setting these properties will cause source frames to be converted into the specified color space and tagged as such. The source frames provided as CIImages will have the appropriate CGColorSpace applied. The color space is preserved when the output CIImage is finally rendered internally.
+
+        - When using basic compositing (i.e. AVVideoCompositionLayerInstruction)
+			Setting these properties will ensure that the internal compositor renders (or passes through) frames in specified color space and are tagged as such.
+*/
+@interface AVVideoComposition (AVVideoCompositionColorimetery)
+
+/*
+ @property     colorPrimaries
+ @abstract
+    Rendering will use these primaries and frames will be tagged as such. If the value of this property is nil then the source's primaries will be propagated and used.
+ @discussion
+    Default is nil. Valid values are those suitable for AVVideoColorPrimariesKey. Generally set as a triple along with colorYCbCrMatrix and colorTransferFunction.
+*/
+@property (nonatomic, readonly, nullable) NSString *colorPrimaries NS_AVAILABLE(10_12, 10_0);
+
+/*
+ @property     colorYCbCrMatrix
+ @abstract
+    Rendering will use this matrix and frames will be tagged as such. If the value of this property is nil then the source's matrix will be propagated and used.
+ @discussion
+    Default is nil. Valid values are those suitable for AVVideoYCbCrMatrixKey. Generally set as a triple along with colorPrimaries and colorTransferFunction.
+*/
+@property (nonatomic, readonly, nullable) NSString *colorYCbCrMatrix NS_AVAILABLE(10_12, 10_0);
+
+/*
+ @property     colorTransferFunction
+ @abstract
+    Rendering will use this transfer function and frames will be tagged as such. If the value of this property is nil then the source's transfer function will be propagated and used.
+ @discussion
+    Default is nil. Valid values are those suitable for AVVideoTransferFunctionKey. Generally set as a triple along with colorYCbCrMatrix and colorYCbCrMatrix.
+*/
+@property (nonatomic, readonly, nullable) NSString *colorTransferFunction NS_AVAILABLE(10_12, 10_0);
+
+@end
+
 @interface AVVideoComposition (AVVideoCompositionFiltering)
 
 /*  
- @method		videoCompositionWithAsset:options:applyingFiltersWithHandler:
+ @method		videoCompositionWithAsset:options:applyingCIFiltersWithHandler:
  @abstract
 	Returns a new instance of AVVideoComposition with values and instructions that will apply the specified handler block to video frames represented as instances of CIImage.
  @param			asset		An instance of AVAsset. For best performance, ensure that the duration and tracks properties of the asset are already loaded before invoking this method.
@@ -200,10 +259,69 @@
 
 @end
 
+/*
+ @category	   AVMutableVideoCompositionColorimetery
+ @abstract
+    Indicates the color space of the frames output from the video composition.
+ @discussion
+    Collectively the properties colorPrimaries, colorYCbCrMatrix, and colorTransferFunction define the color space that the rendered frames will be tagged with. For custom video compositing these properties are also used to specify the required color space of the source frames.
+
+    Examples of common color spaces:
+	
+        TODO: SD
+        TODO: HD
+        TODO: HD-P3
+
+    How to preserve the color space of the source frames:
+ 
+        Decide which color space to be preserved by examining the source asset's video tracks. Copy the source track's primaries, matrix and transfer function into the video composition's colorPrimaries, colorYCbCrMatrix and colorTransferFunction respectively.
+		
+        TODO: <rdar://problem/25496972> sample code showing how to inspect the source asset track's primaries etc and setup a video composition to preserve them. Ideally we'll show the narrow-HD case and the wide-P3 case.
+
+        - When using custom video compositing
+			Setting these properties will cause source frames to be converted into the specified color space and tagged as such. New frames allocated using -[AVVideoCompositionRenderContext newPixelBuffer] will also be tagged correctly.
+
+        - When using Core Image via videoCompositionWithAsset:options:applyingCIFiltersWithHandler:
+			Setting these properties will cause source frames to be converted into the specified color space and tagged as such. The source frames provided as CIImages will have the appropriate CGColorSpace applied. The color space is preserved when the output CIImage is finally rendered internally.
+
+        - When using basic compositing (i.e. AVVideoCompositionLayerInstruction)
+			Setting these properties will ensure that the internal compositor renders (or passes through) frames in specified color space and are tagged as such.
+*/
+@interface AVMutableVideoComposition (AVMutableVideoCompositionColorimetery)
+
+/*
+ @property     colorPrimaries
+ @abstract
+    Rendering will use these primaries and frames will be tagged as such. If the value of this property is nil then the source's primaries will be propagated and used.
+ @discussion
+    Default is nil. Valid values are those suitable for AVVideoColorPrimariesKey. Generally set as a triple along with colorYCbCrMatrix and colorTransferFunction.
+*/
+@property (nonatomic, copy, nullable) NSString *colorPrimaries NS_AVAILABLE(10_12, 10_0);
+
+/*
+ @property     colorYCbCrMatrix
+ @abstract
+    Rendering will use this matrix and frames will be tagged as such. If the value of this property is nil then the source's matrix will be propagated and used.
+ @discussion
+    Default is nil. Valid values are those suitable for AVVideoYCbCrMatrixKey. Generally set as a triple along with colorPrimaries and colorTransferFunction.
+*/
+@property (nonatomic, copy, nullable) NSString *colorYCbCrMatrix NS_AVAILABLE(10_12, 10_0);
+
+/*
+ @property     colorTransferFunction
+ @abstract
+    Rendering will use this transfer function and frames will be tagged as such. If the value of this property is nil then the source's transfer function will be propagated and used.
+ @discussion
+    Default is nil. Valid values are those suitable for AVVideoTransferFunctionKey. Generally set as a triple along with colorYCbCrMatrix and colorYCbCrMatrix.
+*/
+@property (nonatomic, copy, nullable) NSString *colorTransferFunction NS_AVAILABLE(10_12, 10_0);
+
+@end
+
 @interface AVMutableVideoComposition (AVMutableVideoCompositionFiltering)
 
 /*  
- @method		videoCompositionWithAsset:options:applyingFiltersWithHandler:
+ @method		videoCompositionWithAsset:options:applyingCIFiltersWithHandler:
  @abstract
 	Returns a new instance of AVMutableVideoComposition with values and instructions that will apply the specified handler block to video frames represented as instances of CIImage.
  @param			asset		An instance of AVAsset. For best performance, ensure that the duration and tracks properties of the asset are already loaded before invoking this method.
@@ -264,7 +382,7 @@
 /* Indicates the background color of the composition. Solid BGRA colors only are supported; patterns and other color refs that are not supported will be ignored.
    If the background color is not specified the video compositor will use a default backgroundColor of opaque black.
    If the rendered pixel buffer does not have alpha, the alpha value of the backgroundColor will be ignored. */
-@property (nonatomic, readonly, retain, nullable) __attribute__((NSObject)) CGColorRef backgroundColor CF_RETURNS_RETAINED;
+@property (nonatomic, readonly, retain, nullable) __attribute__((NSObject)) CGColorRef backgroundColor;
 
 /* Provides an array of instances of AVVideoCompositionLayerInstruction that specify how video frames from source tracks should be layered and composed.
    Tracks are layered in the composition according to the top-to-bottom order of the layerInstructions array; the track with trackID of the first instruction
@@ -317,7 +435,7 @@
 /* Indicates the background color of the composition. Solid BGRA colors only are supported; patterns and other color refs that are not supported will be ignored.
    If the background color is not specified the video compositor will use a default backgroundColor of opaque black.
    If the rendered pixel buffer does not have alpha, the alpha value of the backgroundColor will be ignored. */
-@property (nonatomic, retain, nullable) __attribute__((NSObject)) CGColorRef backgroundColor CF_RETURNS_RETAINED;
+@property (nonatomic, retain, nullable) __attribute__((NSObject)) CGColorRef backgroundColor;
 
 /* Provides an array of instances of AVVideoCompositionLayerInstruction that specify how video frames from source tracks should be layered and composed.
    Tracks are layered in the composition according to the top-to-bottom order of the layerInstructions array; the track with trackID of the first instruction
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoSettings.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoSettings.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoSettings.h	2015-09-30 23:18:04.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoSettings.h	2016-05-24 07:21:29.000000000 +0200
@@ -27,6 +27,7 @@
 		AVVideoCleanApertureKey
 		AVVideoScalingModeKey
 		AVVideoColorPropertiesKey
+		AVVideoAllowWideColorKey
  
 	It is an error to add any other AVVideoSettings.h keys to an uncompressed video settings dictionary.
 */
@@ -79,8 +80,6 @@
 	/* AVVideoScalingModeResizeAspectFill - Preserve aspect ratio of the source, and crop picture to fit destination dimensions. */
 	AVF_EXPORT NSString *const AVVideoScalingModeResizeAspectFill							NS_AVAILABLE(10_7, 5_0);
 
-#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
-
 /*
 	Clients who specify AVVideoColorPropertiesKey must specify a color primary, transfer function, and Y'CbCr matrix.
 	Most clients will want to specify HD, which consists of:
@@ -95,23 +94,37 @@
 		AVVideoTransferFunction_ITU_R_709_2
 		AVVideoYCbCrMatrix_ITU_R_601_4
  
+	If you require wide gamut HD colorimetry, you can use:
+ 
+		 AVVideoColorPrimaries_P3_D65
+		 AVVideoTransferFunction_ITU_R_709_2
+		 AVVideoYCbCrMatrix_ITU_R_709_2
+ 
 	AVFoundation will color match if the source and destination color properties differ.
 	It is important that the source be tagged.
 */
-AVF_EXPORT NSString *const AVVideoColorPropertiesKey /* NSDictionary, all 3 below keys required */           NS_AVAILABLE(10_7, NA);
-	AVF_EXPORT NSString *const AVVideoColorPrimariesKey /* NSString */                                       NS_AVAILABLE(10_7, NA);
-		AVF_EXPORT NSString *const AVVideoColorPrimaries_ITU_R_709_2                                         NS_AVAILABLE(10_7, NA);
+AVF_EXPORT NSString *const AVVideoColorPropertiesKey /* NSDictionary, all 3 below keys required */           NS_AVAILABLE(10_7, 10_0);
+	AVF_EXPORT NSString *const AVVideoColorPrimariesKey /* NSString */                                       NS_AVAILABLE(10_7, 10_0);
+		AVF_EXPORT NSString *const AVVideoColorPrimaries_ITU_R_709_2                                         NS_AVAILABLE(10_7, 10_0);
 		AVF_EXPORT NSString *const AVVideoColorPrimaries_EBU_3213                                            NS_AVAILABLE(10_7, NA);
-		AVF_EXPORT NSString *const AVVideoColorPrimaries_SMPTE_C                                             NS_AVAILABLE(10_7, NA);
-	AVF_EXPORT NSString *const AVVideoTransferFunctionKey /* NSString */                                     NS_AVAILABLE(10_7, NA);
-		AVF_EXPORT NSString *const AVVideoTransferFunction_ITU_R_709_2                                       NS_AVAILABLE(10_7, NA);
+		AVF_EXPORT NSString *const AVVideoColorPrimaries_SMPTE_C                                             NS_AVAILABLE(10_7, 10_0);
+		AVF_EXPORT NSString *const AVVideoColorPrimaries_P3_D65                                              NS_AVAILABLE(10_12, 10_0);
+	AVF_EXPORT NSString *const AVVideoTransferFunctionKey /* NSString */                                     NS_AVAILABLE(10_7, 10_0);
+		AVF_EXPORT NSString *const AVVideoTransferFunction_ITU_R_709_2                                       NS_AVAILABLE(10_7, 10_0);
 		AVF_EXPORT NSString *const AVVideoTransferFunction_SMPTE_240M_1995                                   NS_AVAILABLE(10_7, NA);
-	AVF_EXPORT NSString *const AVVideoYCbCrMatrixKey /* NSString */                                          NS_AVAILABLE(10_7, NA);
-		AVF_EXPORT NSString *const AVVideoYCbCrMatrix_ITU_R_709_2                                            NS_AVAILABLE(10_7, NA);
-		AVF_EXPORT NSString *const AVVideoYCbCrMatrix_ITU_R_601_4                                            NS_AVAILABLE(10_7, NA);
+	AVF_EXPORT NSString *const AVVideoYCbCrMatrixKey /* NSString */                                          NS_AVAILABLE(10_7, 10_0);
+		AVF_EXPORT NSString *const AVVideoYCbCrMatrix_ITU_R_709_2                                            NS_AVAILABLE(10_7, 10_0);
+		AVF_EXPORT NSString *const AVVideoYCbCrMatrix_ITU_R_601_4                                            NS_AVAILABLE(10_7, 10_0);
 		AVF_EXPORT NSString *const AVVideoYCbCrMatrix_SMPTE_240M_1995                                        NS_AVAILABLE(10_7, NA);
-
-#endif // (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
+/*!
+ @constant	AVVideoAllowWideColorKey
+ @abstract	Indicates whether the client can process wide color
+ @discussion
+	Clients who wish to process wide color content should set the value of this key to @YES, or specify AVVideoColorPropertiesKey.
+ 
+	The default value, @NO, permits implicit color conversions to occur to a non-wide gamut color space.
+ */
+AVF_EXPORT NSString *const AVVideoAllowWideColorKey /* NSNumber(BOOL)	*/					NS_AVAILABLE(10_12, 10_0);
 
 /*!
  @constant	AVVideoCompressionPropertiesKey

```