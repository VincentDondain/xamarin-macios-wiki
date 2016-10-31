#AVFoundation.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h	2016-09-22 23:56:42.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h	2016-10-22 04:44:53.000000000 +0200
@@ -346,11 +346,18 @@
 
 /*!
   @property		containsFragments
-  @abstract		Indicates whether the asset is extended by at least one movie fragment.
+  @abstract		Indicates whether the asset is extended by at least one fragment.
   @discussion	For QuickTime movie files and MPEG-4 files, the value of this property is YES if canContainFragments is YES and at least one 'moof' box is present after the 'moov' box.
 */
 @property (nonatomic, readonly) BOOL containsFragments NS_AVAILABLE(10_11, 9_0);
 
+/*!
+  @property		overallDurationHint
+  @abstract		Indicates the total duration of fragments that either exist now or may be appended in the future in order to extend the duration of the asset.
+  @discussion	For QuickTime movie files and MPEG-4 files, the value of this property is obtained from the 'mehd' box of the 'mvex' box, if present. If no total fragment duration hint is available, the value of this property is kCMTimeInvalid.
+*/
+@property (nonatomic, readonly) CMTime overallDurationHint NS_AVAILABLE(10_12_3, 10_3);
+
 @end
 
 

```