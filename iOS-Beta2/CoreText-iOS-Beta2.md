#CoreText.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFont.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFont.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFont.h	2016-05-21 08:05:24.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFont.h	2016-06-26 07:43:41.000000000 +0200
@@ -998,7 +998,7 @@
 /*!
     @function   CTFontCopyVariation
     @abstract   Returns a variation dictionary.
-    @discussion This function describes the current configuration of a variation font: a dictionary of number values with variation identifier number keys. As of OS X 10.12 and iOS 10.0, only non-default values (as determined by the variation axis) are returned.
+    @discussion This function describes the current configuration of a variation font: a dictionary of number values with variation identifier number keys. As of macOS 10.12 and iOS 10.0, only non-default values (as determined by the variation axis) are returned.
 
     @param      font
                 The font reference.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontDescriptor.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontDescriptor.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontDescriptor.h	2016-05-21 08:08:53.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontDescriptor.h	2016-06-26 07:43:41.000000000 +0200
@@ -2,7 +2,7 @@
  *  CTFontDescriptor.h
  *  CoreText
  *
- *  Copyright (c) 2006-2015 Apple Inc. All rights reserved.
+ *  Copyright (c) 2006-2016 Apple Inc. All rights reserved.
  *
  */
 
@@ -319,7 +319,7 @@
 
     @result     This function creates a new copy of the original font descriptor with attributes augmented by those specified. If there are conflicts between attributes, the new attributes will replace existing ones, except for kCTFontVariationAttribute and kCTFontFeatureSettingsAttribute which will be merged.
 
-                Starting with OS X 10.12 and iOS 10.0, setting the value of kCTFontFeatureSettingsAttribute to kCFNull will clear the feature settings of the original font descriptor. Setting the value of any individual feature settings pair in the kCTFontFeatureSettingsAttribute value array will clear that feature setting alone. For example, an element like @{ (id)kCTFontFeatureTypeIdentifierKey: @(kLigaturesType), (id)kCTFontFeatureSelectorIdentifierKey: (id)kCFNull } means clear the kLigatureType feature set in the original font descriptor. An element like @[ @"liga", (id)kCFNull ] will have the same effect.
+                Starting with macOS 10.12 and iOS 10.0, setting the value of kCTFontFeatureSettingsAttribute to kCFNull will clear the feature settings of the original font descriptor. Setting the value of any individual feature settings pair in the kCTFontFeatureSettingsAttribute value array to kCFNull will clear that feature setting alone. For example, an element like @{ (id)kCTFontFeatureTypeIdentifierKey: @(kLigaturesType), (id)kCTFontFeatureSelectorIdentifierKey: (id)kCFNull } means clear the kLigatureType feature set in the original font descriptor. An element like @[ @"liga", (id)kCFNull ] will have the same effect.
 */
 CTFontDescriptorRef CTFontDescriptorCreateCopyWithAttributes(
     CTFontDescriptorRef     original,

```