#AVFoundation.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h	2015-08-23 04:02:14.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h	2016-05-25 07:22:12.000000000 +0200
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetCache.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetCache.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetCache.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetCache.h	2016-05-26 02:32:40.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetImageGenerator.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetImageGenerator.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetImageGenerator.h	2015-08-23 04:02:14.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetImageGenerator.h	2016-05-25 07:19:40.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetReader.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetReader.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetReader.h	2015-08-23 04:02:14.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetReader.h	2016-05-25 07:19:40.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetReaderOutput.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetReaderOutput.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetReaderOutput.h	2015-08-23 04:02:14.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetReaderOutput.h	2016-05-25 07:22:12.000000000 +0200
@@ -541,7 +541,6 @@
 
 @end
 
-
 @class AVAssetReaderSampleReferenceOutputInternal;
 
 /*!
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetResourceLoader.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetResourceLoader.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetResourceLoader.h	2015-08-23 04:02:14.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetResourceLoader.h	2016-05-25 07:19:41.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetTrack.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetTrack.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetTrack.h	2015-08-23 04:02:14.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetTrack.h	2016-05-25 07:19:41.000000000 +0200
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetWriter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetWriter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetWriter.h	2015-08-23 04:02:15.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetWriter.h	2016-05-24 07:21:19.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsynchronousKeyValueLoading.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsynchronousKeyValueLoading.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsynchronousKeyValueLoading.h	2015-08-23 04:02:15.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsynchronousKeyValueLoading.h	2016-05-25 07:22:13.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioBuffer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioBuffer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioBuffer.h	2015-08-23 04:02:15.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioBuffer.h	2016-05-26 02:32:42.000000000 +0200
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioChannelLayout.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioChannelLayout.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioChannelLayout.h	2015-08-23 04:02:15.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioChannelLayout.h	2016-05-26 02:32:42.000000000 +0200
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioConnectionPoint.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioConnectionPoint.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioConnectionPoint.h	2015-08-23 04:02:15.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioConnectionPoint.h	2016-05-26 02:32:42.000000000 +0200
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioConverter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioConverter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioConverter.h	2015-08-23 04:02:15.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioConverter.h	2016-05-26 02:32:42.000000000 +0200
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioEngine.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioEngine.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioEngine.h	2015-08-23 04:02:15.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioEngine.h	2016-05-26 02:32:42.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioEnvironmentNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioEnvironmentNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioEnvironmentNode.h	2015-08-23 04:02:15.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioEnvironmentNode.h	2016-05-26 02:32:42.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioFile.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioFile.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioFile.h	2015-08-23 04:02:15.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioFile.h	2016-05-26 02:32:42.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioFormat.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioFormat.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioFormat.h	2015-08-23 04:02:16.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioFormat.h	2016-05-26 02:32:42.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioIONode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioIONode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioIONode.h	2015-08-23 04:02:16.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioIONode.h	2016-05-26 02:32:42.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioMixerNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioMixerNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioMixerNode.h	2015-08-23 04:02:16.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioMixerNode.h	2016-05-26 02:32:42.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioMixing.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioMixing.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioMixing.h	2015-08-23 04:02:16.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioMixing.h	2016-05-26 02:32:43.000000000 +0200
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioNode.h	2015-08-23 04:02:16.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioNode.h	2016-05-26 02:32:43.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioPlayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioPlayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioPlayer.h	2015-08-23 04:02:16.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioPlayer.h	2016-05-26 02:32:43.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioPlayerNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioPlayerNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioPlayerNode.h	2015-08-23 04:02:16.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioPlayerNode.h	2016-05-26 02:32:43.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioRecorder.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioRecorder.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioRecorder.h	2015-08-23 04:02:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioRecorder.h	2016-05-26 02:32:43.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioSequencer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioSequencer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioSequencer.h	2015-08-23 04:02:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioSequencer.h	2016-05-26 02:32:43.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioSettings.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioSettings.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioSettings.h	2015-08-23 04:02:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioSettings.h	2016-05-26 02:32:43.000000000 +0200
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioTime.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioTime.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioTime.h	2015-08-23 04:02:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioTime.h	2016-05-26 02:32:43.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioTypes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioTypes.h	2015-08-23 04:02:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioTypes.h	2016-05-26 02:32:43.000000000 +0200
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnit.h	2015-08-23 04:02:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnit.h	2016-05-26 02:32:43.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitComponent.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitComponent.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitComponent.h	2015-08-23 04:02:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitComponent.h	2016-05-26 02:32:44.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitDelay.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitDelay.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitDelay.h	2015-08-23 04:02:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitDelay.h	2016-05-26 02:32:44.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitDistortion.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitDistortion.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitDistortion.h	2015-08-23 04:02:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitDistortion.h	2016-05-26 02:32:44.000000000 +0200
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitEQ.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitEQ.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitEQ.h	2015-08-23 04:02:18.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitEQ.h	2016-05-26 02:32:44.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitEffect.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitEffect.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitEffect.h	2015-08-23 04:02:18.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitEffect.h	2016-05-26 02:32:44.000000000 +0200
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitGenerator.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitGenerator.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitGenerator.h	2015-08-23 04:02:18.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitGenerator.h	2016-05-26 02:32:44.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitMIDIInstrument.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitMIDIInstrument.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitMIDIInstrument.h	2015-08-23 04:02:18.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitMIDIInstrument.h	2016-05-26 02:32:44.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitReverb.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitReverb.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitReverb.h	2015-08-23 04:02:18.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitReverb.h	2016-05-26 02:32:44.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitSampler.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitSampler.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitSampler.h	2015-08-23 04:02:18.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitSampler.h	2016-05-26 02:32:44.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitTimeEffect.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitTimeEffect.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitTimeEffect.h	2015-08-23 04:02:18.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitTimeEffect.h	2016-05-26 02:32:44.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitTimePitch.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitTimePitch.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitTimePitch.h	2015-08-23 04:02:18.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitTimePitch.h	2016-05-26 02:32:44.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitVarispeed.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitVarispeed.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitVarispeed.h	2015-08-23 04:02:18.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAudioUnitVarispeed.h	2016-05-26 02:32:45.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVBase.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVBase.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVBase.h	2015-08-23 04:02:19.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVBase.h	2016-05-24 07:21:24.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVComposition.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVComposition.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVComposition.h	2015-08-23 04:02:19.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVComposition.h	2016-05-26 02:32:45.000000000 +0200
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCompositionTrack.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCompositionTrack.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCompositionTrack.h	2015-08-23 04:02:19.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVCompositionTrack.h	2016-05-25 07:22:17.000000000 +0200
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVError.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVError.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVError.h	2016-02-21 03:47:44.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVError.h	2016-05-25 07:19:44.000000000 +0200
@@ -96,8 +96,9 @@
 #if TARGET_OS_IPHONE
     AVErrorRecordingAlreadyInProgress NS_AVAILABLE_IOS(9_0) = -11859, // on iOS, AVCaptureMovieFileOutput only supports one recording at a time
 #endif
-#if !TARGET_OS_EMBEDDED
+#if !TARGET_OS_IPHONE
     AVErrorCreateContentKeyRequestFailed NS_AVAILABLE(10_11, NA) = -11860,
 #endif
-	
+    AVErrorUnsupportedOutputSettings NS_AVAILABLE(10_12, 10_0) = -11861,
+	AVErrorOperationNotAllowed NS_AVAILABLE(10_12, 10_0) = -11862,
 };
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVFAudio.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVFAudio.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVFAudio.h	2015-08-23 04:02:20.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVFAudio.h	2016-05-26 02:32:46.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVFoundation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVFoundation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVFoundation.h	2015-08-23 04:02:20.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVFoundation.h	2016-05-26 02:32:46.000000000 +0200
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
@@ -58,12 +71,14 @@
 #import <AVFoundation/AVOutputSettingsAssistant.h>
 #import <AVFoundation/AVPlayer.h>
 #import <AVFoundation/AVPlayerItem.h>
+#import <AVFoundation/AVPlayerItemMediaDataCollector.h>
 #import <AVFoundation/AVPlayerItemOutput.h>
 #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
 #import <AVFoundation/AVPlayerItemProtectedContentAdditions.h>
 #endif
 #import <AVFoundation/AVPlayerItemTrack.h>
 #import <AVFoundation/AVPlayerLayer.h>
+#import <AVFoundation/AVPlayerLooper.h>
 #import <AVFoundation/AVPlayerMediaSelectionCriteria.h>
 #import <AVFoundation/AVSampleBufferDisplayLayer.h>
 #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
@@ -78,3 +93,4 @@
 #import <AVFoundation/AVVideoCompositing.h>
 #import <AVFoundation/AVVideoComposition.h>
 #import <AVFoundation/AVVideoSettings.h>
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMIDIPlayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMIDIPlayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMIDIPlayer.h	2015-08-23 04:02:20.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMIDIPlayer.h	2016-05-26 02:32:46.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMediaFormat.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMediaFormat.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMediaFormat.h	2015-08-23 04:02:20.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMediaFormat.h	2016-05-25 07:22:17.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataFormat.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataFormat.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataFormat.h	2015-08-23 04:02:20.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataFormat.h	2016-05-25 07:22:18.000000000 +0200
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
@@ -314,6 +321,8 @@
 // HTTP Live Streaming metadata
 AVF_EXPORT NSString *const AVMetadataFormatHLSMetadata                                   NS_AVAILABLE(10_10, 8_0);
 // HLS Metadata does not define its own keySpace or keys. Use of the keySpace AVMetadataKeySpaceQuickTimeMetadata and its keys is recommended.
+AVF_EXPORT NSString *const AVMetadataKeySpaceHLSDateRange								NS_AVAILABLE(10_11_3, 9_3);
+
 
 // Extra attribute keys
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataIdentifiers.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataIdentifiers.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataIdentifiers.h	2015-08-23 04:02:20.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataIdentifiers.h	2016-05-24 07:21:27.000000000 +0200
@@ -77,6 +77,7 @@
 
 // ISO UserData (includes 3GPP)
 AVF_EXPORT NSString *const AVMetadataIdentifierISOUserDataCopyright                             NS_AVAILABLE(10_10, 8_0);
+AVF_EXPORT NSString *const AVMetadataIdentifierISOUserDataDate                                  NS_AVAILABLE(10_12, 10_0);
 AVF_EXPORT NSString *const AVMetadataIdentifierISOUserDataTaggedCharacteristic                  NS_AVAILABLE(10_10, 8_0);
 AVF_EXPORT NSString *const AVMetadataIdentifier3GPUserDataCopyright                             NS_AVAILABLE(10_10, 8_0);
 AVF_EXPORT NSString *const AVMetadataIdentifier3GPUserDataAuthor                                NS_AVAILABLE(10_10, 8_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataItem.h	2015-08-23 04:02:20.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMetadataItem.h	2016-05-25 07:22:18.000000000 +0200
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMovie.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMovie.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMovie.h	2015-08-23 04:02:21.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMovie.h	2016-05-26 02:32:47.000000000 +0200
@@ -3,7 +3,7 @@
 
 	Framework:		AVFoundation
  
-	Copyright 2009-2015 Apple Inc. All rights reserved.
+	Copyright 2009-2016 Apple Inc. All rights reserved.
 
 */
 
@@ -185,7 +185,7 @@
 	@result			An NSData object.
 	@discussion     The movie header will be a pure reference movie, with no base URL, suitable for use on the pasteboard.
 */
-- (nullable NSData *)movieHeaderWithFileType:(NSString *)fileType error:(NSError * __nullable * __nullable)outError NS_AVAILABLE_MAC(10_11);
+- (nullable NSData *)movieHeaderWithFileType:(NSString *)fileType error:(NSError * _Nullable * _Nullable)outError NS_AVAILABLE_MAC(10_11);
 
 /*!
 	@method			writeMovieHeaderToURL:fileType:options:error:
@@ -200,7 +200,7 @@
 					If an error occurs writing the movie header, describes the nature of the failure.
 	@discussion		Data references in the output movie header are adjusted to be relative to the destination URL. Note that modifications to instances of AVMutableMovie, to their constituent AVMutableMovieTracks, or to their collections of metadata are committed to storage when their movie headers are written.
 */
-- (BOOL)writeMovieHeaderToURL:(NSURL *)URL fileType:(NSString *)fileType options:(AVMovieWritingOptions)options error:(NSError * __nullable * __nullable)outError NS_AVAILABLE_MAC(10_11);
+- (BOOL)writeMovieHeaderToURL:(NSURL *)URL fileType:(NSString *)fileType options:(AVMovieWritingOptions)options error:(NSError * _Nullable * _Nullable)outError NS_AVAILABLE_MAC(10_11);
 
 /*!
 	@method			isCompatibleWithFileType:
@@ -283,7 +283,7 @@
                     If you want to create an AVMutableMovie from a file and then append sample buffers to any of its tracks, you must first set one of these properties 
                     to indicate where the sample data should be written.
 */
-+ (nullable instancetype)movieWithURL:(NSURL *)URL options:(nullable NSDictionary<NSString *, id> *)options error:(NSError * __nullable * __nullable)outError;
++ (nullable instancetype)movieWithURL:(NSURL *)URL options:(nullable NSDictionary<NSString *, id> *)options error:(NSError * _Nullable * _Nullable)outError;
 
 /*!
 	@method			initWithURL:options:error:
@@ -299,7 +299,7 @@
                     If you want to create an AVMutableMovie from a file and then append sample buffers to any of its tracks, you must first set one of these properties 
                     to indicate where the sample data should be written.
 */
-- (nullable instancetype)initWithURL:(NSURL *)URL options:(nullable NSDictionary<NSString *, id> *)options error:(NSError * __nullable * __nullable)outError NS_DESIGNATED_INITIALIZER;
+- (nullable instancetype)initWithURL:(NSURL *)URL options:(nullable NSDictionary<NSString *, id> *)options error:(NSError * _Nullable * _Nullable)outError NS_DESIGNATED_INITIALIZER;
 
 /*!
 	@method			movieWithData:options:error:
@@ -315,7 +315,7 @@
  
                     By default, the defaultMediaDataStorage property will be nil and each associated AVMutableMovieTrack's mediaDataStorage property will be nil. If you want to create an AVMutableMovie from an NSData object and then append sample buffers to any of its tracks, you must first set one of these properties to indicate where the sample data should be written.
 */
-+ (nullable instancetype)movieWithData:(NSData *)data options:(nullable NSDictionary<NSString *, id> *)options error:(NSError * __nullable * __nullable)outError NS_AVAILABLE_MAC(10_11);
++ (nullable instancetype)movieWithData:(NSData *)data options:(nullable NSDictionary<NSString *, id> *)options error:(NSError * _Nullable * _Nullable)outError NS_AVAILABLE_MAC(10_11);
 
 /*!
 	@method			initWithData:options:error:
@@ -331,7 +331,7 @@
  
                     By default, the defaultMediaDataStorage property will be nil and each associated AVMutableMovieTrack's mediaDataStorage property will be nil. If you want to create an AVMutableMovie from an NSData object and then append sample buffers to any of its tracks, you must first set one of these properties to indicate where the sample data should be written.
 */
-- (nullable instancetype)initWithData:(NSData *)data options:(nullable NSDictionary<NSString *, id> *)options error:(NSError * __nullable * __nullable)outError NS_DESIGNATED_INITIALIZER;
+- (nullable instancetype)initWithData:(NSData *)data options:(nullable NSDictionary<NSString *, id> *)options error:(NSError * _Nullable * _Nullable)outError NS_DESIGNATED_INITIALIZER;
 
 /*!
 	@method			movieWithSettingsFromMovie:options:error:
@@ -347,7 +347,7 @@
                     By default, the defaultMediaDataStorage property will be nil and each associated AVMovieTrack's mediaDataStorage property will be nil.
                     If you want to create an AVMutableMovie from an NSData object and then append sample buffers to any of its tracks, you must first set one of these properties to indicate where the sample data should be written.
 */
-+ (nullable instancetype)movieWithSettingsFromMovie:(nullable AVMovie *)movie options:(nullable NSDictionary<NSString *, id> *)options error:(NSError * __nullable * __nullable)outError;
++ (nullable instancetype)movieWithSettingsFromMovie:(nullable AVMovie *)movie options:(nullable NSDictionary<NSString *, id> *)options error:(NSError * _Nullable * _Nullable)outError;
 
 /*!
 	@method			initWithSettingsFromMovie:options:error:
@@ -363,7 +363,7 @@
                     By default, the defaultMediaDataStorage property will be nil and each associated AVMovieTrack's mediaDataStorage property will be nil.
                     If you want to create an AVMutableMovie from an NSData object and then append sample buffers to any of its tracks, you must first set one of these properties to indicate where the sample data should be written.
 */
-- (nullable instancetype)initWithSettingsFromMovie:(nullable AVMovie *)movie options:(nullable NSDictionary<NSString *, id> *)options error:(NSError * __nullable * __nullable)outError NS_DESIGNATED_INITIALIZER;
+- (nullable instancetype)initWithSettingsFromMovie:(nullable AVMovie *)movie options:(nullable NSDictionary<NSString *, id> *)options error:(NSError * _Nullable * _Nullable)outError NS_DESIGNATED_INITIALIZER;
 
 /*!
 	@property       preferredRate
@@ -448,7 +448,7 @@
 	@discussion		This method may add new tracks to the target movie to ensure that all tracks of the asset are represented in the inserted timeRange.
 					Existing content at the specified startTime will be pushed out by the duration of timeRange.
 */
-- (BOOL)insertTimeRange:(CMTimeRange)timeRange ofAsset:(AVAsset *)asset atTime:(CMTime)startTime copySampleData:(BOOL)copySampleData error:(NSError * __nullable * __nullable)outError;
+- (BOOL)insertTimeRange:(CMTimeRange)timeRange ofAsset:(AVAsset *)asset atTime:(CMTime)startTime copySampleData:(BOOL)copySampleData error:(NSError * _Nullable * _Nullable)outError;
 
 /*!
 	@method			insertEmptyTimeRange:
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMovieTrack.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMovieTrack.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMovieTrack.h	2015-08-23 04:02:21.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMovieTrack.h	2016-05-26 02:32:47.000000000 +0200
@@ -3,7 +3,7 @@
 
 	Framework:		AVFoundation
  
-	Copyright 2009-2015 Apple Inc. All rights reserved.
+	Copyright 2009-2016 Apple Inc. All rights reserved.
 
 */
 
@@ -136,7 +136,7 @@
 @end
 
 
-@interface AVMutableMovieTrack (AVMutableMovieTrack_LanguageProperties)
+@interface AVMutableMovieTrack (AVMutableMovieTrackLanguageProperties)
 
 /*!
 	@property       languageCode
@@ -155,7 +155,7 @@
 @end
 
 
-@interface AVMutableMovieTrack (AVMutableMovieTrack_PropertiesForVisualCharacteristic)
+@interface AVMutableMovieTrack (AVMutableMovieTrackVisualProperties)
 
 /*!
 	@property       naturalSize
@@ -196,7 +196,7 @@
 @end
 
 
-@interface AVMutableMovieTrack (AVMutableMovieTrack_PropertiesForAudibleCharacteristic)
+@interface AVMutableMovieTrack (AVMutableMovieTrackAudibleProperties)
 
 /*!
 	@property       preferredVolume
@@ -207,10 +207,10 @@
 @end
 
 
-@interface AVMutableMovieTrack (AVMutableMovieTrack_ChunkProperties)
+@interface AVMutableMovieTrack (AVMutableMovieTrackChunkProperties)
 
 /*!
-	@category		AVMutableMovieTrack(AVMutableMovieTrack_ChunkProperties)
+	@category		AVMutableMovieTrack(AVMutableMovieTrackChunkProperties)
  
 	@discussion		Sample data in a movie file is stored in a series of "chunks". A chunk contains one or more samples, which may have different sizes from one another.
 					The collection of samples into chunks is intended to allow optimized access to the sample data during operations such as movie playback. 
@@ -252,7 +252,7 @@
 @end
 
 
-@interface AVMutableMovieTrack (AVMutableMovieTrack_TrackLevelEditing)
+@interface AVMutableMovieTrack (AVMutableMovieTrackTrackLevelEditing)
 
 /*!
 	@method			insertTimeRange:ofTrack:atTime:copySampleData:error:
@@ -275,7 +275,7 @@
 	@result			A BOOL value that indicates the success of the insertion.
 
 */
-- (BOOL)insertTimeRange:(CMTimeRange)timeRange ofTrack:(AVAssetTrack *)track atTime:(CMTime)startTime copySampleData:(BOOL)copySampleData error:(NSError * __nullable * __nullable)outError;
+- (BOOL)insertTimeRange:(CMTimeRange)timeRange ofTrack:(AVAssetTrack *)track atTime:(CMTime)startTime copySampleData:(BOOL)copySampleData error:(NSError * _Nullable * _Nullable)outError;
 
 /*!
 	@method			insertEmptyTimeRange:
@@ -343,6 +343,62 @@
 @end
 
 
+@interface AVMutableMovieTrack (AVMutableMovieTrackSampleLevelEditing)
+
+/*!
+	@method			appendSampleBuffer:decodeTime:presentationTime:error:
+	@abstract		Appends sample data to a media file and adds sample references for the added data to a track's media sample tables.
+	@param			sampleBuffer
+					The CMSampleBuffer to be appended; this may be obtained from an instance of AVAssetReader.
+	@param			outDecodeTime
+					A pointer to a CMTime structure to receive the decode time in the media of the first sample appended from the sample buffer. Pass NULL if you do not need this information.
+	@param			outPresentationTime
+					A pointer to a CMTime structure to receive the presentation time in the media of the first sample appended from the sample buffer. Pass NULL if you do not need this information.
+	@param			outError
+					If the appending fails, describes the nature of the failure. For example, if the device containing the track's media data storage is full, AVErrorDiskFull is returned.
+	@result			A BOOL value indicating the success of the operation.
+	@discussion
+                    If the sample buffer carries sample data, the sample data is written to the container specified by the track property mediaDataStorage if non-nil,
+                    or else by the movie property defaultMediaDataStorage if non-nil, and sample references will be appended to the track's media.
+                    If both media data storage properties are nil, the method will fail and return NO.
+                    If the sample buffer carries sample references only, sample data will not be written and sample references to the samples in their
+                    original container will be appended to the track's media as necessary.
+
+                    Note regarding sample timing: in a track's media, the first sample's decode timestamp must always be zero.
+                    For an audio track, each sample buffer's duration is used as the sample decode duration.
+                    For other track types, difference between a sample's decode timestamp and the following 
+                    sample's decode timestamps is used as the first sample's decode duration, so as to preserve the relative timing.
+                    
+                    Note that this method does not modify the track's sourceTimeMappings but only appends sample references and sample data to the track's media.  
+                    To make the new samples appear in the track's timeline, invoke -insertMediaTimeRange:intoTimeRange:.
+                    You can retrieve the mediaPresentationTimeRange property before and after appending a sequence of samples,
+                    using CMTimeRangeGetEnd on each to calculate the media TimeRange for -insertMediaTimeRange:intoTimeRange:.
+
+                    It's safe for multiple threads to call this method on different tracks at once.
+*/
+- (BOOL)appendSampleBuffer:(CMSampleBufferRef)sampleBuffer decodeTime:(nullable CMTime *)outDecodeTime presentationTime:(nullable CMTime *)outPresentationTime error:(NSError * _Nullable * _Nullable)outError NS_AVAILABLE_MAC(10_12);
+
+/*!
+	@method			insertMediaTimeRange:intoTimeRange:
+	@abstract		Inserts a reference to a media time range into a track.
+	@param			mediaTimeRange
+					The presentation time range of the media to be inserted.
+	@param			trackTimeRange
+					The time range of the track into which the media is to be inserted.
+    @result			A BOOL value indicating the success of the operation.
+	@discussion
+                    Use this method after you have appended samples or sample references to a track's media.
+                    
+                    To specify that the media time range be played at its natural rate, pass mediaTimeRange.duration == trackTimeRange.duration;
+                    otherwise, the ratio between these is used to determine the playback rate.
+                    
+                    Pass kCMTimeInvalid for trackTimeRange.start to indicate that the segment should be appended to the end of the track.
+*/
+- (BOOL)insertMediaTimeRange:(CMTimeRange)mediaTimeRange intoTimeRange:(CMTimeRange)trackTimeRange NS_AVAILABLE_MAC(10_12);
+
+@end
+
+
 #pragma mark --- AVFragmentedMovieTrack ---
 /*!
 	@class			AVFragmentedMovieTrack
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayer.h	2015-08-23 04:02:21.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayer.h	2016-05-24 07:21:27.000000000 +0200
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
  
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItem.h	2015-08-23 04:02:21.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItem.h	2016-05-25 04:39:23.000000000 +0200
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
 
 
@@ -687,6 +699,36 @@
 
 @end
 
+@class AVPlayerItemMediaDataCollector;
+
+@interface AVPlayerItem (AVPlayerItemMediaDataCollectors)
+
+/*!
+ @method		addMediaDataCollector:
+ @abstract		Adds the specified instance of AVPlayerItemMediaDataCollector to the receiver's collection of mediaDataCollectors.
+ @discussion
+	This method may incur additional I/O to collect the requested media data asynchronously.
+ @param			collector
+				An instance of AVPlayerItemMediaDataCollector
+*/
+- (void)addMediaDataCollector:(AVPlayerItemMediaDataCollector *)collector NS_AVAILABLE(10_11_3, 9_3);
+
+/*!
+ @method		removeMediaDataCollector:
+ @abstract		Removes the specified instance of AVPlayerItemMediaDataCollector from the receiver's collection of mediaDataCollectors.
+ @param			collector
+				An instance of AVPlayerItemMediaDataCollector
+*/
+- (void)removeMediaDataCollector:(AVPlayerItemMediaDataCollector *)collector NS_AVAILABLE(10_11_3, 9_3);
+
+/*!
+ @property		mediaDataCollectors
+ @abstract		The collection of associated mediaDataCollectors.
+*/
+@property (nonatomic, readonly) NSArray<AVPlayerItemMediaDataCollector *> *mediaDataCollectors NS_AVAILABLE(10_11_3, 9_3);;
+
+@end
+
 @class AVPlayerItemAccessLogEvent;
 
 /*!
@@ -702,6 +744,7 @@
 @private
 	AVPlayerItemAccessLogInternal	*_playerItemAccessLog;
 }
+AV_INIT_UNAVAILABLE
 
 /*!
  @method		extendedLogData
@@ -744,6 +787,7 @@
 @private
 	AVPlayerItemErrorLogInternal	*_playerItemErrorLog;
 }
+AV_INIT_UNAVAILABLE
 
 /*!
  @method		extendedLogData
@@ -787,6 +831,7 @@
 @private
 	AVPlayerItemAccessLogEventInternal	*_playerItemAccessLogEvent;
 }
+AV_INIT_UNAVAILABLE
 
 /*!
  @property		numberOfSegmentsDownloaded
@@ -912,6 +957,22 @@
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
@@ -997,6 +1058,7 @@
 @private
 	AVPlayerItemErrorLogEventInternal	*_playerItemErrorLogEvent;
 }
+AV_INIT_UNAVAILABLE
 
 /*!
  @property		date
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItemMediaDataCollector.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItemMediaDataCollector.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItemMediaDataCollector.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItemMediaDataCollector.h	2016-05-25 07:19:45.000000000 +0200
@@ -0,0 +1,115 @@
+/*
+ File:  AVPlayerItemMediaDataCollector.h
+
+	Framework:  AVFoundation
+
+	Copyright 2015 Apple Inc. All rights reserved.
+
+ */
+
+#import <AVFoundation/AVBase.h>
+#import <Foundation/Foundation.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class AVPlayerItemMediaDataCollectorInternal;
+
+/*!
+	@class			AVPlayerItemMediaDataCollector
+	@abstract		AVPlayerItemMediaDataCollector is an abstract class encapsulating the common API for all AVPlayerItemMediaDataCollector subclasses.
+	@discussion
+		Instances of AVPlayerItemMediaDataCollector permit the collection of media data from an AVAsset during playback by an AVPlayer. As opposed to AVPlayerItemOutputs, AVPlayerItemMediaDataCollectors collect all media data across an AVPlayerItem's timebase, relevant to the specific collector being used. Attaching an AVPlayerItemMediaDataCollector may incur additional I/O accordingly.
+
+		You manage an association of an AVPlayerItemMediaDataCollector instance with an AVPlayerItem as the source input using the AVPlayerItem methods:
+
+		• addMediaDataCollector:
+		• removeMediaDataCollector:
+*/
+NS_CLASS_AVAILABLE(10_11_3, 9_3)
+@interface AVPlayerItemMediaDataCollector : NSObject
+{
+@private
+	AVPlayerItemMediaDataCollectorInternal *_collectorInternal;
+}
+@end
+
+@protocol AVPlayerItemMetadataCollectorPushDelegate;
+@class AVPlayerItemMetadataCollectorInternal;
+@class AVDateRangeMetadataGroup;
+
+/*!
+	@class			AVPlayerItemMetadataCollector
+	@abstract		A subclass of AVPlayerItemMediaDataCollector that provides AVMetadataGroups for an AVPlayerItem.
+	@discussion
+		This class can be used to inform clients of the current set of AVMetadataGroups on an AVPlayerItem, and when new AVMetadataGroups become available - e.g. in a Live HLS stream.
+*/
+NS_CLASS_AVAILABLE(10_11_3, 9_3)
+@interface AVPlayerItemMetadataCollector : AVPlayerItemMediaDataCollector
+{
+@private
+	AVPlayerItemMetadataCollectorInternal *_metadataCollectorInternal;
+}
+
+/*!
+	@method			initWithIdentifiers:classifyingLabels:
+	@abstract		Returns an instance of AVPlayerItemMetadataCollector that can provide all available AVMetadataGroups matching a set of criteria.
+	@param			identifiers
+					A array of metadata identifiers indicating the metadata items that the output should provide. See AVMetadataIdentifiers.h for publicly defined metadata identifiers. Pass nil to include metadata with any identifier.
+	@param			classifyingLabels
+					If the metadata format supports labeling each metadata group with a string, supplying an array of group labels indicates that the output should provide metadata groups that match one of the supplied labels. Pass nil to include metadata with any (or no) classifying label.
+	@result			An instance of AVPlayerItemMetadataCollector.
+	@discussion
+		Some metadata available in some formats - such as timed metadata embedded in HLS segments - is not available for collector output.
+		The default init method can be used as an alternative to setting both identifiers and classifyingLabels to nil.
+*/
+- (instancetype)initWithIdentifiers:(nullable NSArray<NSString *> *)identifiers classifyingLabels:(nullable NSArray<NSString *> *)classifyingLabels;
+
+/*!
+	@method			setDelegate:queue:
+	@abstract		Sets the receiver's delegate and a dispatch queue on which the delegate will be called.
+	@param			delegate
+					An object conforming to AVPlayerItemMetadataCollectorPushDelegate protocol.
+	@param			delegateQueue
+					A dispatch queue on which all delegate methods will be called.
+*/
+- (void)setDelegate:(nullable id <AVPlayerItemMetadataCollectorPushDelegate>)delegate queue:(nullable dispatch_queue_t)delegateQueue;
+
+/*!
+	@property		delegate
+	@abstract		The receiver's delegate.
+	@discussion
+		The delegate is held using a zeroing-weak reference, so this property will have a value of nil after a delegate that was previously set has been deallocated.  This property is not key-value observable.
+*/
+@property (nonatomic, readonly, weak, nullable) id <AVPlayerItemMetadataCollectorPushDelegate> delegate;
+
+/*!
+	@property		delegateQueue
+	@abstract		The dispatch queue on which messages are sent to the delegate.
+	@discussion
+		This property is not key-value observable.
+*/
+@property (nonatomic, readonly, nullable) dispatch_queue_t delegateQueue;
+
+@end
+
+@protocol AVPlayerItemMetadataCollectorPushDelegate <NSObject>
+
+/*!
+	@method			metadataCollector:didCollectDateRangeMetadataGroups:indexesOfNewGroup:indexesOfModifiedGroups:
+	@abstract		A delegate callback that delivers the total set of AVDateRangeMetadataGroups for this collector.
+	@param			metadataCollector
+					The AVPlayerItemMetadataCollector source.
+	@param			metadataGroups
+					The set of all metadata groups meeting the criteria of the output.
+	@param			indexesOfNewGroups
+					Indexes of metadataGroups added since the last delegate invocation of this method.
+	@param			indexesOfModifiedGroups
+					Indexes of metadataGroups modified since the last delegate invocation of this method.
+	@discussion
+		This method will be invoked whenever new AVDateRangeMetadataGroups are added to metadataGroups or whenever any AVDateRangeMetadataGroups in metadataGroups have been modified since previous invocations. The initial invocation will have indexesOfNewGroup referring to every index in metadataGroups. Subsequent invocations may not contain all previously collected metadata groups if they no longer refer to a region in the AVPlayerItem's seekableTimeRanges.
+*/
+- (void)metadataCollector:(AVPlayerItemMetadataCollector *)metadataCollector didCollectDateRangeMetadataGroups:(NSArray<AVDateRangeMetadataGroup *> *)metadataGroups indexesOfNewGroups:(NSIndexSet *)indexesOfNewGroups indexesOfModifiedGroups:(NSIndexSet *)indexesOfModifiedGroups;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItemOutput.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItemOutput.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItemOutput.h	2015-08-23 04:02:21.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItemOutput.h	2016-05-24 07:21:27.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerLooper.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerLooper.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerLooper.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerLooper.h	2016-05-25 04:39:24.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVSampleBufferDisplayLayer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVSampleBufferDisplayLayer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVSampleBufferDisplayLayer.h	2015-08-23 04:02:22.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVSampleBufferDisplayLayer.h	2016-05-26 02:32:48.000000000 +0200
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVSampleCursor.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVSampleCursor.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVSampleCursor.h	2015-08-23 04:02:22.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVSampleCursor.h	2016-05-26 02:32:48.000000000 +0200
@@ -224,7 +224,7 @@
 	@abstract		The URL of the storage container of the current sample, as well as other samples that are intended to be loaded in the same operation as a "chunk".
 	@discussion		May be nil; if nil, the storage location of the chunk is the URL of the sample cursor's track's asset, if it has one.
 */
-@property (nonatomic, readonly) NSURL *currentChunkStorageURL;
+@property (nonatomic, readonly, nullable) NSURL *currentChunkStorageURL;
 
 /*!
     @struct		AVSampleCursorStorageRange
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVTimedMetadataGroup.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVTimedMetadataGroup.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVTimedMetadataGroup.h	2015-08-23 04:02:23.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVTimedMetadataGroup.h	2016-05-04 00:21:21.000000000 +0200
@@ -32,6 +32,16 @@
 
 @end
 
+@interface AVMetadataGroup (AVMetadataGroupIdentification)
+
+/* indicates the classifyingLabel of the group; nil if no classifyingLabel is indicated */
+@property (nonatomic, readonly, nullable) NSString *classifyingLabel NS_AVAILABLE(10_11_3, 9_3);
+
+/* indicates the unique identifier of the group; nil if no unique identifier is indicated */
+@property (nonatomic, readonly, nullable) NSString *uniqueID NS_AVAILABLE(10_11_3, 9_3);
+
+@end
+
 /*!
 	@class		AVTimedMetadataGroup
  
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoCompositing.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoCompositing.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoCompositing.h	2015-08-23 04:02:23.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoCompositing.h	2016-05-24 07:21:29.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoComposition.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoComposition.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoComposition.h	2015-08-23 04:02:23.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoComposition.h	2016-05-25 04:40:26.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoSettings.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoSettings.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoSettings.h	2015-08-23 04:02:23.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoSettings.h	2016-05-24 07:21:29.000000000 +0200
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