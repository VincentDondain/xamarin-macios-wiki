#CoreText.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTDefines.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTDefines.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTDefines.h	2016-02-20 00:06:39.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTDefines.h	2016-05-21 08:00:49.000000000 +0200
@@ -2,7 +2,7 @@
  *  CTDefines.h
  *  CoreText
  *
- *  Copyright (c) 2010-2015 Apple Inc. All rights reserved.
+ *  Copyright (c) 2010-2016 Apple Inc. All rights reserved.
  *
  */
 
@@ -19,7 +19,7 @@
 # define __has_attribute(x) 0
 #endif
 
-#if defined(CT_BUILDING_CoreText)
+#if defined(CT_BUILDING_CoreText) || TARGET_OS_WIN32
 # define CT_AVAILABLE(_mac, _ios)
 # define CT_AVAILABLE_MAC(_mac)
 # define CT_AVAILABLE_IOS(_ios)
@@ -68,4 +68,27 @@
 # endif /* defined(__OBJC__) */
 #endif /*  __has_attribute(objc_bridge) */
 
+#if TARGET_OS_WIN32
+#define __nullable
+
+#define CF_BRIDGED_TYPE(T)
+#define CF_BRIDGED_MUTABLE_TYPE(T)
+#define CF_RELATED_TYPE(T,C,I)
+
+#define CF_ASSUME_NONNULL_BEGIN
+#define CF_ASSUME_NONNULL_END
+
+# if defined(CT_BUILDING_CoreText) && defined(__cplusplus)
+#  define CT_EXPORT extern "C" __declspec(dllexport)
+# elif defined(CT_BUILDING_CoreText) && !defined(__cplusplus)
+#  define CT_EXPORT extern __declspec(dllexport)
+# elif defined(__cplusplus)
+#  define CT_EXPORT extern "C" __declspec(dllimport)
+# else
+#  define CT_EXPORT extern __declspec(dllimport)
+# endif
+#else
+# define CT_EXPORT extern
+#endif
+
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFont.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFont.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFont.h	2016-02-20 00:06:38.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFont.h	2016-05-21 08:05:24.000000000 +0200
@@ -2,7 +2,7 @@
  *  CTFont.h
  *  CoreText
  *
- *  Copyright (c) 2006-2015 Apple Inc. All rights reserved.
+ *  Copyright (c) 2006-2016 Apple Inc. All rights reserved.
  *
  */
 
@@ -59,94 +59,94 @@
     @defined    kCTFontCopyrightNameKey
     @abstract   The name specifier for the copyright name.
 */
-extern const CFStringRef kCTFontCopyrightNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontCopyrightNameKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontFamilyNameKey
     @abstract   The name specifier for the family name.
 */
-extern const CFStringRef kCTFontFamilyNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontFamilyNameKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontSubFamilyNameKey
     @abstract   The name specifier for the subfamily name.
 */
-extern const CFStringRef kCTFontSubFamilyNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontSubFamilyNameKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontStyleNameKey
     @abstract   The name specifier for the style name.
 */
-extern const CFStringRef kCTFontStyleNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontStyleNameKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontUniqueNameKey
     @abstract   The name specifier for the unique name.
     @discussion Note that this name is often not unique and should not be
                 assumed to be truly unique.
 */
-extern const CFStringRef kCTFontUniqueNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontUniqueNameKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontFullNameKey
     @abstract   The name specifier for the full name.
 */
-extern const CFStringRef kCTFontFullNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontFullNameKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontVersionNameKey
     @abstract   The name specifier for the version name.
 */
-extern const CFStringRef kCTFontVersionNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontVersionNameKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontPostScriptNameKey
-    @abstract   The name specifier for the Postscript name.
+    @abstract   The name specifier for the PostScript name.
 */
-extern const CFStringRef kCTFontPostScriptNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontPostScriptNameKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontTrademarkNameKey
     @abstract   The name specifier for the trademark name.
 */
-extern const CFStringRef kCTFontTrademarkNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontTrademarkNameKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontManufacturerNameKey
     @abstract   The name specifier for the manufacturer name.
 */
-extern const CFStringRef kCTFontManufacturerNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontManufacturerNameKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontDesignerNameKey
     @abstract   The name specifier for the designer name.
 */
-extern const CFStringRef kCTFontDesignerNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontDesignerNameKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontDescriptionNameKey
     @abstract   The name specifier for the description name.
 */
-extern const CFStringRef kCTFontDescriptionNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontDescriptionNameKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontVendorURLNameKey
     @abstract   The name specifier for the vendor url name.
 */
-extern const CFStringRef kCTFontVendorURLNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontVendorURLNameKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontDesignerURLNameKey
     @abstract   The name specifier for the designer url name.
 */
-extern const CFStringRef kCTFontDesignerURLNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontDesignerURLNameKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontLicenseNameKey
     @abstract   The name specifier for the license name.
 */
-extern const CFStringRef kCTFontLicenseNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontLicenseNameKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontLicenseURLNameKey
     @abstract   The name specifier for the license url name.
 */
-extern const CFStringRef kCTFontLicenseURLNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontLicenseURLNameKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontSampleTextNameKey
     @abstract   The name specifier for the sample text name string.
 */
-extern const CFStringRef kCTFontSampleTextNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontSampleTextNameKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontPostScriptCIDNameKey
-    @abstract   The name specifier for the Postscript CID name.
+    @abstract   The name specifier for the PostScript CID name.
 */
-extern const CFStringRef kCTFontPostScriptCIDNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontPostScriptCIDNameKey CT_AVAILABLE(10_5, 3_2);
 
 /*! --------------------------------------------------------------------------
     @group Font Creation
@@ -939,7 +939,7 @@
     @param      glyph
                 The glyph.
 
-    @param      transform
+    @param      matrix
                 An affine transform applied to the path. Can be NULL, in which case CGAffineTransformIdentity will be used.
 
     @result     A retained CGPath reference containing the glyph outlines or NULL if there is no such glyph or it has no outline.
@@ -950,7 +950,7 @@
     const CGAffineTransform * __nullable matrix ) CT_AVAILABLE(10_5, 3_2);
 
 /*! --------------------------------------------------------------------------
-    @group Font Variations        (this functionality is not supported on iOS)
+    @group Font Variations
 *///--------------------------------------------------------------------------
 
 /*!
@@ -958,51 +958,55 @@
     @abstract   Key to get the variation axis identifier.
     @discussion This key is used with a variation axis dictionary to get the axis identifier value as a CFNumberRef.
 */
-extern const CFStringRef kCTFontVariationAxisIdentifierKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontVariationAxisIdentifierKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontVariationAxisMinimumValueKey
     @abstract   Key to get the variation axis minimum value.
     @discussion This key is used with a variation axis dictionary to get the minimum axis value as a CFNumberRef.
 */
-extern const CFStringRef kCTFontVariationAxisMinimumValueKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontVariationAxisMinimumValueKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontVariationAxisMaximumValueKey
     @abstract   Key to get the variation axis maximum value.
     @discussion This key is used with a variation axis dictionary to get the maximum axis value as a CFNumberRef.
 */
-extern const CFStringRef kCTFontVariationAxisMaximumValueKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontVariationAxisMaximumValueKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontVariationAxisDefaultValueKey
     @abstract   Key to get the variation axis default value.
     @discussion This key is used with a variation axis dictionary to get the default axis value as a CFNumberRef.
 */
-extern const CFStringRef kCTFontVariationAxisDefaultValueKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontVariationAxisDefaultValueKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontVariationAxisNameKey
     @abstract   Key to get the variation axis name string.
     @discussion This key is used with a variation axis dictionary to get the localized variation axis name.
 */
-extern const CFStringRef kCTFontVariationAxisNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontVariationAxisNameKey CT_AVAILABLE(10_5, 3_2);
 
 /*!
     @function   CTFontCopyVariationAxes
-    @abstract   Returns an array of variation axes.
+    @abstract   Returns an array of variation axis dictionaries.
 
     @param      font
                 The font reference.
 
-    @result     This function returns an array of variation axis dictionaries. Each variation axis dictionary contains the five variation axis keys above.
+    @result     This function returns an array of variation axis dictionaries or null if the font does not support variations. Each variation axis dictionary contains the five kCTFontVariationAxis* keys above.
 */
 CFArrayRef __nullable CTFontCopyVariationAxes( CTFontRef font ) CT_AVAILABLE(10_5, 3_2);
 
 /*!
     @function   CTFontCopyVariation
-    @abstract   Returns a variation dictionary from the font reference.
+    @abstract   Returns a variation dictionary.
+    @discussion This function describes the current configuration of a variation font: a dictionary of number values with variation identifier number keys. As of OS X 10.12 and iOS 10.0, only non-default values (as determined by the variation axis) are returned.
 
     @param      font
                 The font reference.
 
-    @result     This function returns the current variation instance as a dictionary. The keys for each variation correspond to the variation identifier obtained via kCTFontVariationAxisIdentifierKey which represents the axis' four character code as a CFNumber.
+    @result     This function returns a variation dictionary or null if the font does not support variations.
+    
+    @seealso    kCTFontVariationAxisIdentifierKey
+    @seealso    kCTFontVariationAxisDefaultValueKey
 */
 CFDictionaryRef __nullable CTFontCopyVariation( CTFontRef font ) CT_AVAILABLE(10_5, 3_2);
 
@@ -1015,61 +1019,61 @@
     @abstract   Key to get the OpenType feature tag.
     @discussion This key can be used with a font feature dictionary to get the tag as a CFStringRef.
 */
-extern const CFStringRef kCTFontOpenTypeFeatureTag CT_AVAILABLE(10_10, 8_0);
+CT_EXPORT const CFStringRef kCTFontOpenTypeFeatureTag CT_AVAILABLE(10_10, 8_0);
 /*!
     @defined    kCTFontOpenTypeFeatureValue
     @abstract   Key to get the OpenType feature value.
     @discussion This key can be used with a font feature dictionary to get the value as a CFNumberRef.
 */
-extern const CFStringRef kCTFontOpenTypeFeatureValue CT_AVAILABLE(10_10, 8_0);
+CT_EXPORT const CFStringRef kCTFontOpenTypeFeatureValue CT_AVAILABLE(10_10, 8_0);
 /*!
     @defined    kCTFontFeatureTypeIdentifierKey
     @abstract   Key to get the font feature type value.
     @discussion This key can be used with a font feature dictionary to get the type identifier as a CFNumberRef.
 */
-extern const CFStringRef kCTFontFeatureTypeIdentifierKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontFeatureTypeIdentifierKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontFeatureTypeNameKey
     @abstract   Key to get the font feature name.
     @discussion This key can be used with a font feature dictionary to get the localized type name string as a CFString.
 */
-extern const CFStringRef kCTFontFeatureTypeNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontFeatureTypeNameKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontFeatureTypeExclusiveKey
     @abstract   Key to get the font feature exclusive setting.
     @discussion This key can be used with a font feature dictionary to get the the exclusive setting of the feature as a CFBoolean. The value associated with this key indicates whether the feature selectors associated with this type should be mutually exclusive.
 */
-extern const CFStringRef kCTFontFeatureTypeExclusiveKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontFeatureTypeExclusiveKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontFeatureTypeSelectorsKey
     @abstract   Key to get the font feature selectors.
     @discussion This key can be used with a font feature dictionary to get the array of font feature selectors as a CFArrayRef. This is an array of selector dictionaries that contain the values for the following selector keys.
 */
-extern const CFStringRef kCTFontFeatureTypeSelectorsKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontFeatureTypeSelectorsKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontFeatureSelectorIdentifierKey
     @abstract   Key to get the font feature selector identifier.
     @discussion This key can be used with a selector dictionary corresponding to a feature type to obtain the selector identifier value as a CFNumberRef.
 */
-extern const CFStringRef kCTFontFeatureSelectorIdentifierKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontFeatureSelectorIdentifierKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontFeatureSelectorNameKey
     @abstract   Key to get the font feature selector name.
     @discussion This key is used with a selector dictionary to get the localized name string for the selector as a CFStringRef.
 */
-extern const CFStringRef kCTFontFeatureSelectorNameKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontFeatureSelectorNameKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontFeatureSelectorDefaultKey
     @abstract   Key to get the font feature selector default setting value.
     @discussion This key is used with a selector dictionary to get the default indicator for the selector. This value is a CFBooleanRef which if present and true indicates that this selector is the default setting for the current feature type.
 */
-extern const CFStringRef kCTFontFeatureSelectorDefaultKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontFeatureSelectorDefaultKey CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontFeatureSelectorSettingKey
     @abstract   Key to get or specify the current feature setting.
     @discussion This key is used with a selector dictionary to get or specify the current setting for the selector. This value is a CFBooleanRef to indicate whether this selector is on or off. If this key is not present, the default setting is used.
 */
-extern const CFStringRef kCTFontFeatureSelectorSettingKey CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontFeatureSelectorSettingKey CT_AVAILABLE(10_5, 3_2);
 
 /*!
     @function   CTFontCopyFeatures
@@ -1291,6 +1295,7 @@
                 The font reference.
 
     @param      options
+                The options used when copying font tables.
 
     @result     This function returns an array of CTFontTableTag values for the given font and the supplied options. The returned set will contain unboxed values, which may be extracted like so:
                 <code>CTFontTableTag tag = (CTFontTableTag)(uintptr_t)CFArrayGetValueAtIndex(tags, index);</code>
@@ -1310,6 +1315,7 @@
                 The font table identifier as a CTFontTableTag.
 
     @param      options
+                The options used when copying font table.
 
     @result     This function returns a retained reference to the font table data as CFDataRef or NULL if the table is not present.
 */
@@ -1339,8 +1345,6 @@
 
     @param      context
                 CGContext used to render the glyphs.
-
-    @result     void
 */
 void CTFontDrawGlyphs(
     CTFontRef       font, 
@@ -1391,7 +1395,7 @@
  
     @discussion This key can be used with a baseline info dictionary to offset to the Roman baseline as a CFNumberRef float. It can also be used as the value for kCTBaselineClassAttributeName.
 */
-extern const CFStringRef kCTBaselineClassRoman CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTBaselineClassRoman CT_AVAILABLE(10_8, 6_0);
 
 /*!
     @defined    kCTBaselineClassIdeographicCentered
@@ -1400,7 +1404,7 @@
  
     @discussion This key can be used with a baseline info dictionary to offset to the Ideographic Centered baseline as a CFNumberRef float. It can also be used as the value for kCTBaselineClassAttributeName.
 */
-extern const CFStringRef kCTBaselineClassIdeographicCentered CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTBaselineClassIdeographicCentered CT_AVAILABLE(10_8, 6_0);
     
 /*!
     @defined    kCTBaselineClassIdeographicLow
@@ -1409,7 +1413,7 @@
  
     @discussion This key can be used with a baseline info dictionary to offset to the Ideographic Low baseline as a CFNumberRef float. It can also be used as the value for kCTBaselineClassAttributeName.
 */
-extern const CFStringRef kCTBaselineClassIdeographicLow CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTBaselineClassIdeographicLow CT_AVAILABLE(10_8, 6_0);
     
 /*!
     @defined    kCTBaselineClassIdeographicHigh
@@ -1418,7 +1422,7 @@
 
     @discussion This key can be used with a baseline info dictionary to offset to the Ideographic High baseline as a CFNumberRef float. It can also be used as the value for kCTBaselineClassAttributeName.
 */
-extern const CFStringRef kCTBaselineClassIdeographicHigh CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTBaselineClassIdeographicHigh CT_AVAILABLE(10_8, 6_0);
 
 /*!
     @defined    kCTBaselineClassHanging
@@ -1427,7 +1431,7 @@
  
     @discussion This key can be used with a baseline info dictionary to offset to the Hanging baseline as a CFNumberRef float. It can also be used as the value for kCTBaselineClassAttributeName.
 */
-extern const CFStringRef kCTBaselineClassHanging CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTBaselineClassHanging CT_AVAILABLE(10_8, 6_0);
 
 /*!
     @defined    kCTBaselineClassMathKey
@@ -1436,7 +1440,7 @@
 
     @discussion This key can be used with a baseline info dictionary to offset to the Math baseline as a CFNumberRef float. It can also be used as the value for kCTBaselineClassAttributeName.
 */
-extern const CFStringRef kCTBaselineClassMath CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTBaselineClassMath CT_AVAILABLE(10_8, 6_0);
 
 /*!
     @defined    kCTBaselineReferenceFont
@@ -1445,7 +1449,7 @@
  
     @discussion This key can be used to specify a font for the reference baseline. The value is a CTFontRef or the kCTBaselineOriginalFont constant.
 */
-extern const CFStringRef kCTBaselineReferenceFont CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTBaselineReferenceFont CT_AVAILABLE(10_8, 6_0);
 
 /*!
     @defined    kCTBaselineOriginalFont
@@ -1454,7 +1458,7 @@
  
     @discussion This constant can be used as the value for kCTBaselineReferenceFont to specify that the original font should be used for the reference baseline.
 */
-extern const CFStringRef kCTBaselineOriginalFont CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTBaselineOriginalFont CT_AVAILABLE(10_8, 6_0);
 
 
 /*!
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontCollection.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontCollection.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontCollection.h	2016-02-19 23:48:11.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontCollection.h	2016-05-21 08:08:53.000000000 +0200
@@ -76,21 +76,21 @@
     @abstract   Option key to specify filtering of duplicates.
     @discussion Specify this option key in the options dictionary with a non- zero value to enable automatic filtering of duplicate font descriptors.
 */
-extern const CFStringRef kCTFontCollectionRemoveDuplicatesOption CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontCollectionRemoveDuplicatesOption CT_AVAILABLE(10_5, 3_2);
 
 /*!
     @defined    kCTFontCollectionIncludeDisabledFontsOption
     @abstract   Option key to include disabled fonts in the matching results.
     @discussion Specify this option key in the options dictionary with a non-zero value to enable matching of disabled fonts. You can pass font descriptors specifying disabled fonts to CTFontManagerEnableFontDescriptors, but you cannot use such a font descriptor to query font attributes from the system database or create a CTFontRef.
 */
-extern const CFStringRef kCTFontCollectionIncludeDisabledFontsOption CT_AVAILABLE_MAC(10_7);
+CT_EXPORT const CFStringRef kCTFontCollectionIncludeDisabledFontsOption CT_AVAILABLE_MAC(10_7);
 
 /*!
     @defined    kCTFontCollectionDisallowAutoActivationOption
     @abstract   Option key to avoid auto-activating fonts.
     @discussion Specify this option key in the options dictionary with a non-zero value to disallow searches for missing fonts (font descriptors returning no results).
 */
-extern const CFStringRef kCTFontCollectionDisallowAutoActivationOption CT_AVAILABLE_MAC(10_7);
+CT_EXPORT const CFStringRef kCTFontCollectionDisallowAutoActivationOption CT_AVAILABLE_MAC(10_7);
 
 /*! --------------------------------------------------------------------------
     @group Collection Creation
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontDescriptor.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontDescriptor.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontDescriptor.h	2015-12-17 18:57:20.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontDescriptor.h	2016-05-21 08:08:53.000000000 +0200
@@ -63,91 +63,91 @@
     @abstract   The font URL.
     @discussion This is the key for accessing the font URL from the font descriptor. The value associated with this key is a CFURLRef.
 */
-extern const CFStringRef kCTFontURLAttribute CT_AVAILABLE(10_6, 3_2);
+CT_EXPORT const CFStringRef kCTFontURLAttribute CT_AVAILABLE(10_6, 3_2);
 /*!
     @defined    kCTFontNameAttribute
     @abstract   The PostScript name.
     @discussion This is the key for retrieving the PostScript name from the font descriptor. When matching, this is treated more generically: the system first tries to find fonts with this PostScript name. If none is found, the system tries to find fonts with this family name, and, finally, if still nothing, tries to find fonts with this display name. The value associated with this key is a CFStringRef. If unspecified, defaults to "Helvetica", if unavailable falls back to global font cascade list.
 */
-extern const CFStringRef kCTFontNameAttribute CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontNameAttribute CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontDisplayNameAttribute
     @abstract   The display name.
     @discussion This is the key for accessing the name used to display the font. Most commonly this is the full name. The value associated with this key is a CFStringRef.
 */
-extern const CFStringRef kCTFontDisplayNameAttribute CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontDisplayNameAttribute CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontFamilyNameAttribute
     @abstract   The family name.
     @discussion This is the key for accessing the family name from the font descriptor. The value associated with this key is a CFStringRef.
 */
-extern const CFStringRef kCTFontFamilyNameAttribute CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontFamilyNameAttribute CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontStyleNameAttribute
     @abstract   The style name.
     @discussion This is the key for accessing the style name of the font. This name represents the designer's description of the font's style. The value associated with this key is a CFStringRef.
 */
-extern const CFStringRef kCTFontStyleNameAttribute CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontStyleNameAttribute CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontTraitsAttribute
     @abstract   The font traits dictionary.
     @discussion This is the key for accessing the dictionary of font traits for stylistic information. See CTFontTraits.h for the list of font traits. The value associated with this key is a CFDictionaryRef.
 */
-extern const CFStringRef kCTFontTraitsAttribute CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontTraitsAttribute CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontVariationAttribute
     @abstract   The font variation dictionary.
     @discussion This key is used to obtain the font variation instance as a CFDictionaryRef. If specified in a font descriptor, fonts with the specified axes will be primary match candidates, if no such fonts exist, this attribute will be ignored.
 */
-extern const CFStringRef kCTFontVariationAttribute CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontVariationAttribute CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontSizeAttribute
     @abstract   The font point size.
     @discussion This key is used to obtain or specify the font point size. Creating a font with this unspecified will default to a point size of 12.0. The value for this key is represented as a CFNumberRef.
 */
-extern const CFStringRef kCTFontSizeAttribute CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontSizeAttribute CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontMatrixAttribute
     @abstract   The font transformation matrix.
     @discussion This key is used to specify the font transformation matrix when creating a font. The default value is CGAffineTransformIdentity. The value for this key is a CFDataRef containing a CGAffineTransform, of which only the a, b, c, and d fields are used.
 */
-extern const CFStringRef kCTFontMatrixAttribute CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontMatrixAttribute CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontCascadeListAttribute
     @abstract   The font cascade list.
     @discussion This key is used to specify or obtain the cascade list used for a font reference. The cascade list is a CFArrayRef containing CTFontDescriptorRefs. If unspecified, the global cascade list is used. This list is not consulted for private-use characters on OS X 10.10, iOS 8, or earlier.
 */
-extern const CFStringRef kCTFontCascadeListAttribute CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontCascadeListAttribute CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontCharacterSetAttribute
     @abstract   The font unicode character coverage set.
     @discussion This key is used to specify or obtain the character set for a font reference. This value for this key is a CFCharacterSetRef. If specified this can be used to restrict the font to a subset of its actual character set. If unspecified this attribute is ignored and the actual character set is used.
 */
-extern const CFStringRef kCTFontCharacterSetAttribute CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontCharacterSetAttribute CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontLanguagesAttribute
     @abstract   The list of supported languages.
     @discussion This key is used to specify or obtain a list of covered languages for a font reference. The value for this key is a CFArrayRef of CFStringRefs. If specified this restricts the search to matching fonts that support the specified languages. The language identifier string should conform to UTS #35. If unspecified this attribute is ignored.
 */
-extern const CFStringRef kCTFontLanguagesAttribute CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontLanguagesAttribute CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontBaselineAdjustAttribute
     @abstract   The baseline adjustment to apply to font metrics.
     @discussion This key is used to specify or obtain the baseline adjustment for a font reference. This is primary used when defining font descriptors for a cascade list to keep the baseline of all fonts even. The value associated with this is a float represented as a CFNumberRef.
 */
-extern const CFStringRef kCTFontBaselineAdjustAttribute CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontBaselineAdjustAttribute CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontMacintoshEncodingsAttribute
     @abstract   The macintosh encodings attribute.
-    @discussion This key is used to specify or obtain the macintosh encodings for a font reference. The value associated with this key is a CFNumberRef containing a bitfield of the Macintosh encodings. This attribute is provided for legacy compatibility.
+    @discussion This key is used to specify or obtain the Macintosh encodings for a font reference. The value associated with this key is a CFNumberRef containing a bitfield of the script codes in <CoreText/SFNTTypes.h>; bit 0 corresponds to kFontRomanScript, and so on. This attribute is provided for legacy compatibility.
 */
-extern const CFStringRef kCTFontMacintoshEncodingsAttribute CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontMacintoshEncodingsAttribute CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontFeaturesAttribute
     @abstract   The array of font features.
     @discussion This key is used to specify or obtain the font features for a font reference. The value associated with this key is a CFArrayRef of font feature dictionaries. This features list contains the feature information from the 'feat' table of the font. See the CTFontCopyFeatures() API in   CTFont.h.
 */
-extern const CFStringRef kCTFontFeaturesAttribute CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontFeaturesAttribute CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontFeatureSettingsAttribute
     @abstract   The array of typographic feature settings.
@@ -159,19 +159,19 @@
                 An OpenType setting can be either an array pair of tag string and value number, or a tag string on its own. For example: @[ @"c2sc", @1 ] or simply @"c2sc". An unspecified value enables the feature and a value of zero disables it.
                 An AAT setting can be specified as an array pair of type and selector numbers. For example: @[ @(kUpperCaseType), @(kUpperCaseSmallCapsSelector) ].
 */
-extern const CFStringRef kCTFontFeatureSettingsAttribute CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontFeatureSettingsAttribute CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontFixedAdvanceAttribute
     @abstract   Specifies advance width.
     @discussion This key is used to specify a constant advance width, which affects the glyph metrics of any font instance created with this key; it overrides font values and the font transformation matrix, if any. The value associated with this key must be a CFNumberRef.
 */
-extern const CFStringRef kCTFontFixedAdvanceAttribute CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontFixedAdvanceAttribute CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontOrientationAttribute
     @abstract   The orientation attribute.
     @discussion This key is used to specify a particular orientation for the glyphs of the font. The value associated with this key is a int as a CFNumberRef. If you want to receive vertical metrics from a font for vertical rendering, specify kCTFontVerticalOrientation. If unspecified, the font will use its native orientation.
 */
-extern const CFStringRef kCTFontOrientationAttribute CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontOrientationAttribute CT_AVAILABLE(10_5, 3_2);
 
 /*!
     @enum       CTFontOrientation
@@ -192,7 +192,7 @@
     @abstract   Specifies the recognized format of the font.
     @discussion The attribute is used to specify or obtain the format of the font. The returned value is a CFNumber containing one of the constants defined below.
 */
-extern const CFStringRef kCTFontFormatAttribute CT_AVAILABLE(10_6, 3_2);
+CT_EXPORT const CFStringRef kCTFontFormatAttribute CT_AVAILABLE(10_6, 3_2);
 
 /*!
     @constant   kCTFontFormatUnrecognized
@@ -222,13 +222,13 @@
     @abstract   Specifies the font descriptor's registration scope.
     @discussion The attribute is used to specify or obtain the font registration scope. The value returned is a CFNumberRef containing one of the CTFontManagerScope enumerated values. A value of NULL can be returned for font descriptors that are not registered.
 */
-extern const CFStringRef kCTFontRegistrationScopeAttribute CT_AVAILABLE(10_6, 3_2);
+CT_EXPORT const CFStringRef kCTFontRegistrationScopeAttribute CT_AVAILABLE(10_6, 3_2);
 /*!
     @defined    kCTFontPriorityAttribute
     @abstract   The font descriptors priority when resolving duplicates and sorting match results.
     @discussion This key is used to obtain or specify the font priority. The value returned is a CFNumberRef containing an integer value as defined below. The higher the value, the higher the priority of the font. Only registered fonts will have a priority. Unregistered font descriptors will return NULL.
 */
-extern const CFStringRef kCTFontPriorityAttribute CT_AVAILABLE(10_6, 3_2);
+CT_EXPORT const CFStringRef kCTFontPriorityAttribute CT_AVAILABLE(10_6, 3_2);
 
 /*!
     @constant   kCTFontPrioritySystem
@@ -259,21 +259,21 @@
     @abstract   The font enabled state.
     @discussion This key is used to obtain the font state. The returned value is a CFNumberRef representing a boolean value. Unregistered font descriptors will return NULL, which is equivalent to false.
 */
-extern const CFStringRef kCTFontEnabledAttribute CT_AVAILABLE(10_6, 3_2);
+CT_EXPORT const CFStringRef kCTFontEnabledAttribute CT_AVAILABLE(10_6, 3_2);
 
 /*!
 	@defined    kCTFontDownloadableAttribute
 	@abstract   The font downloadable state.
 	@discussion The value associated with this key is a CFBoolean.  If it is kCFBooleanTrue, CoreText attempts to download a font if necessary when matching a descriptor.
 */
-extern const CFStringRef kCTFontDownloadableAttribute CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTFontDownloadableAttribute CT_AVAILABLE(10_8, 6_0);
 
 /*!
     @defined    kCTFontDownloadedAttribute
     @abstract   The download state.
     @discussion The value associated with this key is a CFBoolean.  If it is kCFBooleanTrue, corresponding FontAsset has been downloaded. (but still it may be necessary to call appropriate API in order to use the font in the FontAsset.)
 */
-extern const CFStringRef kCTFontDownloadedAttribute CT_AVAILABLE_IOS(7_0);
+CT_EXPORT const CFStringRef kCTFontDownloadedAttribute CT_AVAILABLE(10_12, 7_0);
 
 /*! --------------------------------------------------------------------------
     @group Descriptor Creation
@@ -318,6 +318,8 @@
                 A CFDictionaryRef of arbitrary attributes.
 
     @result     This function creates a new copy of the original font descriptor with attributes augmented by those specified. If there are conflicts between attributes, the new attributes will replace existing ones, except for kCTFontVariationAttribute and kCTFontFeatureSettingsAttribute which will be merged.
+
+                Starting with OS X 10.12 and iOS 10.0, setting the value of kCTFontFeatureSettingsAttribute to kCFNull will clear the feature settings of the original font descriptor. Setting the value of any individual feature settings pair in the kCTFontFeatureSettingsAttribute value array will clear that feature setting alone. For example, an element like @{ (id)kCTFontFeatureTypeIdentifierKey: @(kLigaturesType), (id)kCTFontFeatureSelectorIdentifierKey: (id)kCFNull } means clear the kLigatureType feature set in the original font descriptor. An element like @[ @"liga", (id)kCFNull ] will have the same effect.
 */
 CTFontDescriptorRef CTFontDescriptorCreateCopyWithAttributes(
     CTFontDescriptorRef     original,
@@ -459,28 +461,28 @@
  */
 
 /* CTFontDescriptorRef; The current font descriptor.   Valid when state is kCTFontDescriptorMatchingDidMatch. */
-extern const CFStringRef kCTFontDescriptorMatchingSourceDescriptor CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTFontDescriptorMatchingSourceDescriptor CT_AVAILABLE(10_8, 6_0);
 
 /* CFArray; Array of descriptors to be queried.   Valid while downloading or when state is kCTFontDescriptorMatchingWillBeginQuerying. */
-extern const CFStringRef kCTFontDescriptorMatchingDescriptors CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTFontDescriptorMatchingDescriptors CT_AVAILABLE(10_8, 6_0);
 
 /* CFArray; Array of matched font descriptors.   Valid when state is kCTFontDescriptorMatchingDidMatch or CTFontDescriptorMatchingEnd. */
-extern const CFStringRef kCTFontDescriptorMatchingResult CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTFontDescriptorMatchingResult CT_AVAILABLE(10_8, 6_0);
 
 /* CFNumber; Download progress in 0 - 100.   Valid during Downloading state. */
-extern const CFStringRef kCTFontDescriptorMatchingPercentage CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTFontDescriptorMatchingPercentage CT_AVAILABLE(10_8, 6_0);
 
 /* CFNumber; Byte size to download for the current descriptor.   Valid during Downloading state. */
-extern const CFStringRef kCTFontDescriptorMatchingCurrentAssetSize CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTFontDescriptorMatchingCurrentAssetSize CT_AVAILABLE(10_8, 6_0);
 
 /* CFNumber; Total downloaded byte size.   Valid during Downloading state. */
-extern const CFStringRef kCTFontDescriptorMatchingTotalDownloadedSize CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTFontDescriptorMatchingTotalDownloadedSize CT_AVAILABLE(10_8, 6_0);
 
 /* CFNumber; Total byte size to download.   Always valid, but may be Zero when information is not available. */
-extern const CFStringRef kCTFontDescriptorMatchingTotalAssetSize CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTFontDescriptorMatchingTotalAssetSize CT_AVAILABLE(10_8, 6_0);
 
 /* CFError; Valid when state kCTFontDescriptorMatchingDidFailWithError. */
-extern const CFStringRef kCTFontDescriptorMatchingError CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTFontDescriptorMatchingError CT_AVAILABLE(10_8, 6_0);
 
 #if defined(__BLOCKS__)
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontManager.h	2016-02-24 22:54:47.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontManager.h	2016-05-21 08:05:24.000000000 +0200
@@ -2,7 +2,7 @@
  *  CTFontManager.h
  *  CoreText
  *
- *  Copyright (c) 2008-2015 Apple Inc. All rights reserved.
+ *  Copyright (c) 2008-2016 Apple Inc. All rights reserved.
  *
  */
 
@@ -40,7 +40,7 @@
  
     @result     An array of CFStrings.
 */
-CFArrayRef CTFontManagerCopyAvailablePostScriptNames( void ) CT_AVAILABLE_MAC(10_6);
+CFArrayRef CTFontManagerCopyAvailablePostScriptNames( void ) CT_AVAILABLE(10_6, 10_0);
 
 /*!
     @function   CTFontManagerCopyAvailableFontFamilyNames
@@ -48,7 +48,7 @@
 
     @result     An array of CFStrings.
 */
-CFArrayRef CTFontManagerCopyAvailableFontFamilyNames( void ) CT_AVAILABLE_MAC(10_6);
+CFArrayRef CTFontManagerCopyAvailableFontFamilyNames( void ) CT_AVAILABLE(10_6, 10_0);
 
 /*!
     @function   CTFontManagerCopyAvailableFontURLs
@@ -165,7 +165,7 @@
 /*!
     @function   CTFontManagerRegisterGraphicsFont
     @abstract   Registers the specified graphics font with the font manager. Registered fonts are discoverable through font descriptor matching.
-                Attempts to register a font that is either already registered or contains the same Postscript of an already registered font will fail.
+                Attempts to register a font that is either already registered or contains the same PostScript name of an already registered font will fail.
                 This functionality is useful for fonts that may be embedded in documents or present/constructed in memory. A graphics font is obtained
                 by calling CGFontCreateWithDataProvider. Fonts that are backed by files should be registered using CTFontManagerRegisterFontsForURL.
  
@@ -300,7 +300,7 @@
     @abstract   CTFontManage bundle identifier
     @discussion The CTFontManager bundle identifier to be used with get or set global auto-activation settings.
 */
-extern const CFStringRef kCTFontManagerBundleIdentifier CT_AVAILABLE_MAC(10_6);
+CT_EXPORT const CFStringRef kCTFontManagerBundleIdentifier CT_AVAILABLE_MAC(10_6);
 
 /*!
     @enum
@@ -331,7 +331,7 @@
                 will set the global auto-activation settings.
     @param      setting
                 The new setting.
-    @result     Function will apply the setting to the appropriate preferences location.
+    @discussion Function will apply the setting to the appropriate preferences location.
 */
 void CTFontManagerSetAutoActivationSetting(
     CFStringRef __nullable              bundleIdentifier,
@@ -362,7 +362,7 @@
                 for changes in session or user scopes and with the local notification center for changes in process scope.
                 iOS clients should register as an observer of the notification with the local notification center for all changes.
 */
-extern const CFStringRef kCTFontManagerRegisteredFontsChangedNotification CT_AVAILABLE(10_6, 7_0);
+CT_EXPORT const CFStringRef kCTFontManagerRegisteredFontsChangedNotification CT_AVAILABLE(10_6, 7_0);
 
 CF_ASSUME_NONNULL_END
 CF_EXTERN_C_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontManagerErrors.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontManagerErrors.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontManagerErrors.h	2016-02-20 00:06:38.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontManagerErrors.h	2016-05-21 08:00:48.000000000 +0200
@@ -20,14 +20,14 @@
     @abstract   CFError domain for CTFontManager errors
     @discussion CFErrors with this domain will have error codes corresponding to one of the CTFontManagerErrors above.
 */
-extern const CFStringRef kCTFontManagerErrorDomain CT_AVAILABLE(10_6, 3_2);
+CT_EXPORT const CFStringRef kCTFontManagerErrorDomain CT_AVAILABLE(10_6, 3_2);
 
 /*!
     @constant   kCTFontManagerErrorFontURLsKey
     @abstract   User info key to be used with CFError references returned from registration functions.
     @discussion The value associated with this key in the user info dictionary of a CFError is a CFArray of font URLs that failed with given error.
 */
-extern const CFStringRef kCTFontManagerErrorFontURLsKey CT_AVAILABLE(10_6, 3_2);
+CT_EXPORT const CFStringRef kCTFontManagerErrorFontURLsKey CT_AVAILABLE(10_6, 3_2);
 
 /*!
     @enum
@@ -43,10 +43,6 @@
                 The file contains invalid font data that could cause system problems.
     @constant   kCTFontManagerErrorAlreadyRegistered
                 The file has already been registered in the specified scope.
-*/
-/*!
-    @enum
-    @abstract   Font un-registration errors
     @discussion Errors that would prevent un-registration of fonts for a specified font file URL.
     @constant   kCTFontManagerErrorNotRegistered
                 The file is not registered in the specified scope.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontTraits.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontTraits.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontTraits.h	2016-02-19 23:48:11.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFontTraits.h	2016-05-21 08:08:53.000000000 +0200
@@ -21,25 +21,25 @@
     @abstract   Dictionary key to access the symbolic traits value.
     @discussion Use this key to access the symbolic traits value from the font traits dictionary. The value is returned as a CFNumberRef.
 */
-extern const CFStringRef kCTFontSymbolicTrait CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontSymbolicTrait CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontWeightTrait
     @abstract   Dictionary key to access the weight trait value.
     @discussion Use this key to access the normalized weight trait from the font traits dictionary. The value returned is a CFNumberRef representing a float value between -1.0 and 1.0 for normalized weight. The value of 0.0 corresponds to the regular or medium font weight.
 */
-extern const CFStringRef kCTFontWeightTrait CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontWeightTrait CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontWidthTrait
     @abstract   Dictionary key to access the width (condense/expand) trait value.
     @discussion Use this key to access the normalized proportion trait from the font traits dictionary. This value corresponds to the relative inter-glyph spacing for a given font. The value returned is a CFNumberRef representing a float between -1.0 and 1.0. The value of 0.0 corresponds to regular glyph spacing while negative values represent condensed glyph spacing.
 */
-extern const CFStringRef kCTFontWidthTrait CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontWidthTrait CT_AVAILABLE(10_5, 3_2);
 /*!
     @defined    kCTFontSlantTrait
     @abstract   Dictionary key to access the slant trait value.
     @discussion Use this key to access the normalized slant angle from the font traits dictionary. The value returned is a CFNumberRef representing a float value between -1.0 and 1.0 for normalized slant angle. The value or 0.0 corresponds to 0 degree clockwise rotation from the vertical and 1.0 corresponds to 30 degrees clockwise rotation.
 */
-extern const CFStringRef kCTFontSlantTrait CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontSlantTrait CT_AVAILABLE(10_5, 3_2);
 
 /*!
     @const      kCTFontClassMaskShift
@@ -84,7 +84,7 @@
 /*!
     @enum       CTFontStylisticClass
     @abstract   Stylistic class values.
-    @discussion CTFontStylisticClass classifies certain stylistic qualities of the font. These values correspond closely to the font class values in the OpenType 'OS/2' table. The class values are bundled in the upper four bits of the CTFontSymbolicTraits and can be obtained via the kCTFontClassMaskTrait.
+    @discussion CTFontStylisticClass classifies certain stylistic qualities of the font. These values correspond closely to the font class values in the OpenType 'OS/2' table. The class values are bundled in the upper four bits of the CTFontSymbolicTraits and can be obtained via the kCTFontTraitClassMask.
 */
 typedef CF_OPTIONS(uint32_t, CTFontStylisticClass) {
     kCTFontClassUnknown             = (0 << kCTFontClassMaskShift),
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFrame.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFrame.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFrame.h	2015-12-17 18:57:20.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTFrame.h	2016-05-21 08:00:48.000000000 +0200
@@ -86,7 +86,7 @@
 	@seealso	CTFramesetterCreateFrame
 */
 
-extern const CFStringRef kCTFrameProgressionAttributeName CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFrameProgressionAttributeName CT_AVAILABLE(10_5, 3_2);
 
 /*!
 	@enum		CTFramePathFillRule
@@ -121,7 +121,7 @@
 	@seealso	CTFramesetterCreateFrame
  */
 
-extern const CFStringRef kCTFramePathFillRuleAttributeName CT_AVAILABLE(10_7, 4_2);
+CT_EXPORT const CFStringRef kCTFramePathFillRuleAttributeName CT_AVAILABLE(10_7, 4_2);
 
 /*!
 	@const		kCTFramePathWidthAttributeName
@@ -134,7 +134,7 @@
 	@seealso	CTFramesetterCreateFrame
  */
 
-extern const CFStringRef kCTFramePathWidthAttributeName CT_AVAILABLE(10_7, 4_2);
+CT_EXPORT const CFStringRef kCTFramePathWidthAttributeName CT_AVAILABLE(10_7, 4_2);
 
 	
 /*!
@@ -148,7 +148,7 @@
 	@seealso	CTFramesetterCreateFrame
 */
 
-extern const CFStringRef kCTFrameClippingPathsAttributeName CT_AVAILABLE(10_7, 4_3);
+CT_EXPORT const CFStringRef kCTFrameClippingPathsAttributeName CT_AVAILABLE(10_7, 4_3);
 
 /*!
 	@const		kCTFramePathClippingPathAttributeName
@@ -160,7 +160,7 @@
 	@seealso	kCTFrameClippingPathsAttributeName
  */
 
-extern const CFStringRef kCTFramePathClippingPathAttributeName CT_AVAILABLE(10_7, 4_3);
+CT_EXPORT const CFStringRef kCTFramePathClippingPathAttributeName CT_AVAILABLE(10_7, 4_3);
 
 /* --------------------------------------------------------------------------- */
 /* Frame Accessors */
@@ -314,7 +314,7 @@
 	@param		context
 				The context to draw the frame to.
 
-	@result		If both the frame and the context are valid, the frame will be
+	@discussion	If both the frame and the context are valid, the frame will be
 				drawn in the context.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTParagraphStyle.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTParagraphStyle.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTParagraphStyle.h	2016-02-24 22:50:12.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTParagraphStyle.h	2016-05-21 08:08:53.000000000 +0200
@@ -160,7 +160,7 @@
                 of the first script contained in the paragraph.
 
                 Type: CTTextAlignment
-                Default: kCTNaturalTextAlignment
+                Default: kCTTextAlignmentNatural
                 Application: CTFramesetter
 
 
@@ -339,7 +339,7 @@
     kCTParagraphStyleSpecifierLineHeightMultiple = 7,
     kCTParagraphStyleSpecifierMaximumLineHeight = 8,
     kCTParagraphStyleSpecifierMinimumLineHeight = 9,
-    kCTParagraphStyleSpecifierLineSpacing = 10,			/* deprecated */
+    kCTParagraphStyleSpecifierLineSpacing CT_ENUM_DEPRECATED(10_5, 10_8, 3_2, 6_0) = 10,
     kCTParagraphStyleSpecifierParagraphSpacing = 11,
     kCTParagraphStyleSpecifierParagraphSpacingBefore = 12,
     kCTParagraphStyleSpecifierBaseWritingDirection = 13,
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTRubyAnnotation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTRubyAnnotation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTRubyAnnotation.h	2016-02-24 22:54:47.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTRubyAnnotation.h	2016-05-21 07:01:15.000000000 +0200
@@ -2,7 +2,7 @@
  *  CTRubyAnnotation.h
  *  CoreText
  *
- *  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+ *  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
  *
  */
 
@@ -19,6 +19,7 @@
 
 #include <CoreText/CTDefines.h>
 #include <CoreGraphics/CGBase.h>
+#include <CoreFoundation/CFDictionary.h>
 
 CF_IMPLICIT_BRIDGING_ENABLED
 CF_EXTERN_C_BEGIN
@@ -164,7 +165,7 @@
     @param      text
                 An array of CFStringRef, indexed by CTRubyPosition. Supply NULL for any unused positions.
 
-    @result     This function will return a reference to a CTRubyAlignment object.
+    @result     This function will return a reference to a CTRubyAnnotation object.
 */
 
 CTRubyAnnotationRef CTRubyAnnotationCreate(
@@ -174,6 +175,62 @@
     CFStringRef text[kCTRubyPositionCount] ) CT_AVAILABLE(10_10, 8_0);
 
 /*!
+    @const      kCTRubyAnnotationSizeFactorAttributeName
+    @abstract   Specifies the size of the annotation text as a percent of the size of the base text.
+
+    @discussion Value must be a CFNumberRef.
+*/
+
+CT_EXPORT const CFStringRef kCTRubyAnnotationSizeFactorAttributeName CT_AVAILABLE(10_12, 10_0);
+
+/*!
+    @const      kCTRubyAnnotationScaleToFitAttributeName
+    @abstract   Treat the size specified in kCTRubyAnnotationSizeFactorAttributeName as the maximum
+                scale factor, when the base text size is smaller than annotation text size, we will
+                try to scale the annotation font size down so that it will fit the base text without
+                overhang or adding extra padding between base text.
+
+    @discussion Value must be a CFBooleanRef. Default is false.
+*/
+
+CT_EXPORT const CFStringRef kCTRubyAnnotationScaleToFitAttributeName CT_AVAILABLE(10_12, 10_0);
+
+/*!
+    @function   CTRubyAnnotationCreateWithAttributes
+    @abstract   Creates an immutable ruby annotation object.
+
+    @discussion Using this function to create a ruby annotation object with more precise
+                control of the annotation text.
+
+    @param      alignment
+                Specifies how the ruby text and the base text should be aligned relative to each other.
+
+    @param      overhang
+                Specifies how the ruby text can overhang adjacent characters.
+
+    @param      position
+                The position of the annotation text.
+
+    @param      string
+                A string without any formatting, its format will be derived from the attrs specified below.
+
+    @param      attributes
+                A attribute dictionary to combine with the string specified above. If you don't specify
+                kCTFontAttributeName, the font used by the Ruby annotation will be deduced from the base
+                text, with a size factor specified by a CFNumberRef value keyed by
+                kCTRubyAnnotationSizeFactorAttributeName.
+
+    @result     This function will return a reference to a CTRubyAnnotation object.
+*/
+
+CTRubyAnnotationRef CTRubyAnnotationCreateWithAttributes(
+    CTRubyAlignment alignment,
+    CTRubyOverhang overhang,
+    CTRubyPosition position,
+    CFStringRef string,
+    CFDictionaryRef attributes ) CT_AVAILABLE(10_12, 10_0);
+
+/*!
     @function   CTRubyAnnotationCreateCopy
     @abstract   Creates an immutable copy of a ruby annotation object.
 
@@ -241,7 +298,7 @@
     @param      rubyAnnotation
                 The ruby annotation object.
 
-    @param      postion
+    @param      position
                 The position for which you want to get the ruby text.
 
     @result     If the "rubyAnnotation" reference and the position are valid, then this
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTStringAttributes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTStringAttributes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTStringAttributes.h	2016-02-24 22:54:47.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTStringAttributes.h	2016-05-21 07:54:29.000000000 +0200
@@ -34,7 +34,7 @@
     @discussion Value must be a CTFontRef. Default is Helvetica 12.
 */
 
-extern const CFStringRef kCTFontAttributeName CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTFontAttributeName CT_AVAILABLE(10_5, 3_2);
 
 
 /*!
@@ -52,7 +52,7 @@
                 overrides the foreground color.
 */
 
-extern const CFStringRef kCTForegroundColorFromContextAttributeName CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTForegroundColorFromContextAttributeName CT_AVAILABLE(10_5, 3_2);
 
 
 /*!
@@ -69,7 +69,7 @@
                 set to 0.0, no kerning will be done at all.
 */
 
-extern const CFStringRef kCTKernAttributeName CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTKernAttributeName CT_AVAILABLE(10_5, 3_2);
 
 
 /*!
@@ -95,7 +95,7 @@
                 shaping tables (or the lack thereof) are treated as definitive.
 */
 
-extern const CFStringRef kCTLigatureAttributeName CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTLigatureAttributeName CT_AVAILABLE(10_5, 3_2);
 
 
 /*!
@@ -105,7 +105,16 @@
     @discussion Value must be a CGColorRef. Default value is black.
 */
 
-extern const CFStringRef kCTForegroundColorAttributeName CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTForegroundColorAttributeName CT_AVAILABLE(10_5, 3_2);
+
+/*!
+    @const      kCTBackgroundColorAttributeName
+    @abstract   The background color.
+
+    @discussion Value must be a CGColorRef. Default is no background color.
+*/
+
+CT_EXPORT const CFStringRef kCTBackgroundColorAttributeName CT_AVAILABLE(10_12, 10_0);
 
 
 /*!
@@ -114,11 +123,14 @@
                 line alignment, tab rulers, writing direction, etc.
 
     @discussion Value must be a CTParagraphStyleRef. Default is an empty
-                CTParagraphStyle object. See CTParagraphStyle.h for more
-                information.
+                CTParagraphStyle object: see CTParagraphStyle.h for more
+                information. The value of this attribute must be uniform over
+                the range of any paragraphs to which it is applied.
+
+    @seealso    CFStringGetParagraphBounds
 */
 
-extern const CFStringRef kCTParagraphStyleAttributeName CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTParagraphStyleAttributeName CT_AVAILABLE(10_5, 3_2);
 
 
 /*!
@@ -132,7 +144,7 @@
                 typical value for outlined text is 3.0.
 */
 
-extern const CFStringRef kCTStrokeWidthAttributeName CT_AVAILABLE(10_6, 3_2);
+CT_EXPORT const CFStringRef kCTStrokeWidthAttributeName CT_AVAILABLE(10_6, 3_2);
 
 
 /*!
@@ -142,7 +154,7 @@
     @discussion Value must be a CGColorRef. Default is the foreground color.
 */
 
-extern const CFStringRef kCTStrokeColorAttributeName CT_AVAILABLE(10_6, 3_2);
+CT_EXPORT const CFStringRef kCTStrokeColorAttributeName CT_AVAILABLE(10_6, 3_2);
 
 
 /*!
@@ -157,7 +169,7 @@
                 will be determined by the text's foreground color.
 */
 
-extern const CFStringRef kCTUnderlineStyleAttributeName CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTUnderlineStyleAttributeName CT_AVAILABLE(10_5, 3_2);
 
 
 /*!
@@ -169,7 +181,7 @@
                 value of -1 enables subscripting.
 */
 
-extern const CFStringRef kCTSuperscriptAttributeName CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTSuperscriptAttributeName CT_AVAILABLE(10_5, 3_2);
 
 
 /*!
@@ -179,7 +191,7 @@
     @discussion Value must be a CGColorRef. Default is the foreground color.
 */
 
-extern const CFStringRef kCTUnderlineColorAttributeName CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTUnderlineColorAttributeName CT_AVAILABLE(10_5, 3_2);
 
 
 /*!
@@ -191,8 +203,20 @@
                 indicates that vertical glyph forms are to be used.
 */
 
-extern const CFStringRef kCTVerticalFormsAttributeName CT_AVAILABLE(10_5, 4_3);
+CT_EXPORT const CFStringRef kCTVerticalFormsAttributeName CT_AVAILABLE(10_5, 4_3);
+
+/*!
+    @const      kCTHorizontalInVerticalFormsAttributeName
+    @abstract   Setting text in tate-chu-yoko form (horizontal numerals in vertical text).
+
+    @discussion Value must be a CFNumberRef. Default is int value 0. A value of 1
+                to 4 indicates the number of digits or letters to set in horizontal
+                form. This is to apply the correct feature settings for the text.
+                This attribute only works when kCTVerticalFormsAttributeName is set
+                to true.
+*/
 
+CT_EXPORT const CFStringRef kCTHorizontalInVerticalFormsAttributeName CT_AVAILABLE(10_12, 10_0);
 
 /*!
     @const      kCTGlyphInfoAttributeName
@@ -205,7 +229,7 @@
                 kCTFontAttributeName. See CTGlyphInfo.h for more information.
 */
 
-extern const CFStringRef kCTGlyphInfoAttributeName CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTGlyphInfoAttributeName CT_AVAILABLE(10_5, 3_2);
 
 
 /*!
@@ -218,7 +242,7 @@
                 an attribute value of 1 corresponds to kTraditionalCharactersSelector.
 */
 
-extern const CFStringRef kCTCharacterShapeAttributeName CT_DEPRECATED(10_5, 10_11, 3_2, 9_0);
+CT_EXPORT const CFStringRef kCTCharacterShapeAttributeName CT_DEPRECATED(10_5, 10_11, 3_2, 9_0);
 
 
 /*!
@@ -231,7 +255,7 @@
                 locale-specific line breaking rules.
 */
 
-extern const CFStringRef kCTLanguageAttributeName CT_AVAILABLE(10_9, 7_0);
+CT_EXPORT const CFStringRef kCTLanguageAttributeName CT_AVAILABLE(10_9, 7_0);
 
 
 /*!
@@ -250,7 +274,7 @@
                 CTRunDelegate.h for more information.
 */
 
-extern const CFStringRef kCTRunDelegateAttributeName CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTRunDelegateAttributeName CT_AVAILABLE(10_5, 3_2);
 
 
 /*!
@@ -305,7 +329,7 @@
     @seealso    kCTBaselineClassMath
 */
 
-extern const CFStringRef kCTBaselineClassAttributeName CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTBaselineClassAttributeName CT_AVAILABLE(10_8, 6_0);
 
 
 /*!
@@ -327,7 +351,7 @@
     @seealso    kCTBaselineClassMath
 */
 
-extern const CFStringRef kCTBaselineInfoAttributeName CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTBaselineInfoAttributeName CT_AVAILABLE(10_8, 6_0);
 
 
 /*!
@@ -351,7 +375,7 @@
     @seealso    kCTBaselineReferenceFont
 */
 
-extern const CFStringRef kCTBaselineReferenceInfoAttributeName CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTBaselineReferenceInfoAttributeName CT_AVAILABLE(10_8, 6_0);
 
 
 /*!
@@ -371,9 +395,9 @@
                 pair in plain text or a <span dir="rtl"></span> in HTML,
                 (kCTWritingDirectionLeftToRight | kCTWritingDirectionOverride)
                 corresponding to a LRO/PDF pair in plain text or
-                <bdo dir="ltr"></span> in HTML, and (kCTWritingDirectionRightToLeft
+                <bdo dir="ltr"></bdo> in HTML, and (kCTWritingDirectionRightToLeft
                 | kCTWritingDirectionOverride) corresponding to a RLO/PDF
-                pair in plain text or <bdo dir="rtl"></span> in HTML.
+                pair in plain text or <bdo dir="rtl"></bdo> in HTML.
 
     @seealso    kCTWritingDirectionLeftToRight
     @seealso    kCTWritingDirectionRightToLeft
@@ -381,7 +405,7 @@
     @seealso    kCTWritingDirectionOverride
 */
 
-extern const CFStringRef kCTWritingDirectionAttributeName CT_AVAILABLE(10_8, 6_0);
+CT_EXPORT const CFStringRef kCTWritingDirectionAttributeName CT_AVAILABLE(10_8, 6_0);
 
 
 /*!
@@ -408,7 +432,7 @@
                 more information.
  */
 
-extern const CFStringRef kCTRubyAnnotationAttributeName CT_AVAILABLE(10_10, 8_0);
+CT_EXPORT const CFStringRef kCTRubyAnnotationAttributeName CT_AVAILABLE(10_10, 8_0);
 
 
 CF_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTTextTab.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTTextTab.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTTextTab.h	2015-12-17 18:57:20.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTTextTab.h	2016-05-21 07:54:29.000000000 +0200
@@ -69,7 +69,7 @@
 				optional.
 */
 
-extern const CFStringRef kCTTabColumnTerminatorsAttributeName CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTTabColumnTerminatorsAttributeName CT_AVAILABLE(10_5, 3_2);
 
 
 /* --------------------------------------------------------------------------- */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTTypesetter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTTypesetter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTTypesetter.h	2015-12-17 18:57:20.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTTypesetter.h	2016-05-21 08:05:24.000000000 +0200
@@ -53,7 +53,7 @@
 				performed and any directional control characters are ignored.
 */
 
-extern const CFStringRef kCTTypesetterOptionDisableBidiProcessing CT_DEPRECATED(10_5, 10_8, 3_2, 6_0);
+CT_EXPORT const CFStringRef kCTTypesetterOptionDisableBidiProcessing CT_DEPRECATED(10_5, 10_8, 3_2, 6_0);
 
 /*!
 	@const		kCTTypesetterOptionForcedEmbeddingLevel
@@ -64,7 +64,7 @@
 				level and any directional control characters are ignored.
 */
 
-extern const CFStringRef kCTTypesetterOptionForcedEmbeddingLevel CT_AVAILABLE(10_5, 3_2);
+CT_EXPORT const CFStringRef kCTTypesetterOptionForcedEmbeddingLevel CT_AVAILABLE(10_5, 3_2);
 
 
 /* --------------------------------------------------------------------------- */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CoreText.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CoreText.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CoreText.h	2016-02-20 00:06:39.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CoreText.h	2016-05-21 08:00:49.000000000 +0200
@@ -70,6 +70,7 @@
 #define kCTVersionNumber10_9 0x00060000
 #define kCTVersionNumber10_10 0x00070000
 #define kCTVersionNumber10_11 0x00080000
+#define kCTVersionNumber10_12 0x00090000
 
 CF_EXTERN_C_END
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/SFNTLayoutTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/SFNTLayoutTypes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/SFNTLayoutTypes.h	2015-08-12 07:36:47.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/SFNTLayoutTypes.h	2016-05-21 08:08:53.000000000 +0200
@@ -2,14 +2,18 @@
  *  SFNTLayoutTypes.h
  *  CoreText
  *
- *  Copyright 1994-2015 Apple Inc. All rights reserved.
+ *  Copyright 1994-2016 Apple Inc. All rights reserved.
  *
  */
 
 #ifndef __SFNTLAYOUTTYPES__
 #define __SFNTLAYOUTTYPES__
 
+#if !TARGET_OS_WIN32
 #include <MacTypes.h>
+#elif !defined(__MACTYPES__)
+typedef SInt32 Fixed;
+#endif
 
 #ifdef __cplusplus
 extern "C" {
@@ -638,7 +642,8 @@
   kSFNTLookupSegmentSingle      = 2,    /* segment mapping to single value */
   kSFNTLookupSegmentArray       = 4,    /* segment mapping to lookup array */
   kSFNTLookupSingleTable        = 6,    /* sorted list of glyph, value pairs */
-  kSFNTLookupTrimmedArray       = 8     /* a simple trimmed array indexed by glyph code */
+  kSFNTLookupTrimmedArray       = 8,    /* a simple trimmed array indexed by glyph code */
+  kSFNTLookupVector             = 10    /* a simple trimmed vector indexed by glyph code */
 };
 
 typedef UInt16                          SFNTLookupTableFormat;
@@ -671,6 +676,14 @@
   SFNTLookupValue     valueArray[1];
 };
 typedef struct SFNTLookupTrimmedArrayHeader SFNTLookupTrimmedArrayHeader;
+/* A format 10 lookup table maps some range of glyphs in the font to lookup values of the specified size */
+struct SFNTLookupVectorHeader {
+  UInt16              valueSize;
+  UInt16              firstGlyph;
+  UInt16              count;
+  UInt8               values[1];
+};
+typedef struct SFNTLookupVectorHeader SFNTLookupVectorHeader;
 /*
     Format 2 and format 4 lookup tables map ranges of glyphs to either single lookup
     values (format 2), or per-glyph lookup values (format 4). Since both formats
@@ -705,6 +718,7 @@
   SFNTLookupSegmentHeader  segment;
   SFNTLookupSingleHeader  single;
   SFNTLookupTrimmedArrayHeader  trimmedArray;
+  SFNTLookupVectorHeader  vector;
 };
 typedef union SFNTLookupFormatSpecificHeader SFNTLookupFormatSpecificHeader;
 /* The overall subtable header */
@@ -1465,8 +1479,8 @@
   kKERXOrderedList              = 0,    /* ordered list of kerning pairs */
   kKERXStateTable               = 1,    /* state table for n-way contextual kerning */
   kKERXSimpleArray              = 2,    /* simple n X m array of kerning values */
-  kKERXIndexArray               = 3,    /* modified version of SimpleArray */
-  kKERXControlPoint             = 4     /* state table for control point positioning */
+  kKERXControlPoint             = 4,    /* state table for control point positioning */
+  kKERXIndexArray               = 6     /* index-based n X m array of kerning values */
 };
 
 /* Message Type Flags */
@@ -1490,6 +1504,11 @@
   kKERXActionOffsetMask         = 0x00FFFFFF, /* Mask to extract offset to action table */
 };
 
+/* Flags in KerxIndexArrayHeader */
+enum {
+  kKERXValuesAreLong            = 0x00000001
+};
+
 /* TYPES */
 typedef UInt32                          KerxSubtableCoverage;
 typedef UInt32                          KerxArrayOffset;
@@ -1599,15 +1618,13 @@
 typedef struct KerxSimpleArrayHeader    KerxSimpleArrayHeader;
 /* Index Array */
 struct KerxIndexArrayHeader {
-  UInt16              glyphCount;
-  UInt16              kernValueCount;
-  UInt16              leftClassCount;
-  UInt16              rightClassCount;
-  UInt16              flags;                  /* set to 0 for now */
-  SInt16              kernValue[1];           /* actual kerning values reference by index in kernIndex */
-  UInt16              leftClass[1];           /* maps left glyph to offset into kern index */
-  UInt16              rightClass[1];          /* maps right glyph to offset into kern index */
-  UInt16              kernIndex[1];           /* contains indicies into kernValue */
+  UInt32              flags;
+  UInt16              rowCount;
+  UInt16              columnCount;
+  UInt32              rowIndexTableOffset;    /* offset to row index lookup table */
+  UInt32              columnIndexTableOffset; /* offset to column index offset table */
+  UInt32              kerningArrayOffset;     /* offset to start of kerning array */
+  UInt32              kerningVectorOffset;    /* offset to start of kerning vectors (if tupleCount is 1 or more) */
 };
 typedef struct KerxIndexArrayHeader     KerxIndexArrayHeader;
 /* format specific part of subtable header */
@@ -1617,14 +1634,13 @@
   KerxSimpleArrayHeader  simpleArray;
   KerxIndexArrayHeader  indexArray;
   KerxControlPointHeader  controlPoint;
-
 };
 typedef union KerxFormatSpecificHeader  KerxFormatSpecificHeader;
 /* Overall Subtable header format */
 struct KerxSubtableHeader {
   UInt32              length;                 /* length in bytes (including this header) */
   KerxSubtableCoverage  stInfo;               /* subtable coverage */
-  UInt32              tupleIndex;             /* tuple index for variation subtables */
+  UInt32              tupleCount;             /* tuple count for variation subtables (ignored if the 'kerx' table version is less than 4) */
   KerxFormatSpecificHeader  fsHeader;         /* format specific sub-header */
 };
 typedef struct KerxSubtableHeader       KerxSubtableHeader;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/SFNTTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/SFNTTypes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/SFNTTypes.h	2015-08-12 07:36:47.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/SFNTTypes.h	2016-05-21 08:05:24.000000000 +0200
@@ -9,7 +9,11 @@
 #ifndef __SFNTTYPES__
 #define __SFNTTYPES__
 
+#if !TARGET_OS_WIN32
 #include <MacTypes.h>
+#elif !defined(__MACTYPES__)
+typedef SInt32 Fixed;
+#endif
 
 #ifdef __cplusplus
 extern "C" {

```