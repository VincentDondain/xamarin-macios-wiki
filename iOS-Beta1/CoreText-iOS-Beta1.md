#CoreText.framework

###DONE

*Note: The diff bellow corresponds to not bound APIs (Ruby stuff).*

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTRubyAnnotation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTRubyAnnotation.h 
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTRubyAnnotation.h 2015-10-03 00:01:27.000000000 +0200 
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/CTRubyAnnotation.h 2016-05-21 07:01:15.000000000 +0200 
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
  
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/SFNTLayoutTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/SFNTLayoutTypes.h 
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/SFNTLayoutTypes.h 2015-10-03 00:01:27.000000000 +0200 
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreText.framework/Headers/SFNTLayoutTypes.h 2016-05-21 08:08:53.000000000 +0200 
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
```