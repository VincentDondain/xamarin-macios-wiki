#LatentSemanticMapping.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/LatentSemanticMapping.framework/Headers/LatentSemanticMapping.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/LatentSemanticMapping.framework/Headers/LatentSemanticMapping.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/LatentSemanticMapping.framework/Headers/LatentSemanticMapping.h	2015-08-23 03:35:32.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/LatentSemanticMapping.framework/Headers/LatentSemanticMapping.h	2016-05-11 18:02:28.000000000 +0200
@@ -5,7 +5,7 @@
 
 	Version:	Mac OS X
 
-	Copyright:	© 2001-2010 by Apple Computer, Inc., all rights reserved.
+	Copyright:	© 2001-2015 by Apple Inc., all rights reserved.
 
 	Bugs?:		For bug reports, consult the following page on
 				the World Wide Web:
@@ -36,6 +36,8 @@
 #include <stdio.h>
 #include <stdint.h>
 
+CF_ASSUME_NONNULL_BEGIN
+
 #ifdef __cplusplus
 extern "C" {
 #endif
@@ -64,7 +66,7 @@
  *	
  * An opaque Core Foundation type representing an LSM map (mutable).
  */
-typedef struct __LSMMap *	LSMMapRef;
+typedef struct CF_BRIDGED_TYPE(id) __LSMMap *	LSMMapRef;
 
 /*! @function LSMMapGetTypeID
  *
@@ -76,7 +78,7 @@
  *	
  * An opaque Core Foundation type representing an input text (mutable).
  */
-typedef struct __LSMText *	LSMTextRef;
+typedef struct CF_BRIDGED_TYPE(id) __LSMText *	LSMTextRef;
 
 /*! @function LSMTextGetTypeID
  *
@@ -88,7 +90,7 @@
  *
  * An opaque Core Foundation type representing the result of a lookup (immutable).
  */
-typedef struct __LSMResult * LSMResultRef;
+typedef struct CF_BRIDGED_TYPE(id) __LSMResult * LSMResultRef;
 
 /*! @function LSMResultGetTypeID
  *
@@ -106,7 +108,7 @@
  *
  *	Creates a new LSM map. Call CFRelease to dispose.
  */
-LSMMapRef LSMMapCreate(CFAllocatorRef alloc, CFOptionFlags flags);
+LSMMapRef LSMMapCreate(CFAllocatorRef __nullable alloc, CFOptionFlags flags);
 
 /*! @enum Map Flags
  *	@discussion Options that can be specified for LSMMapCreate. These options
@@ -232,8 +234,8 @@
  *  If subset is non-NULL, only perform clustering on the categories 
  *  or words listed.
  */
-CFArrayRef LSMMapCreateClusters(CFAllocatorRef alloc,
-			  LSMMapRef mapref, CFArrayRef subset,
+CFArrayRef __nullable LSMMapCreateClusters(CFAllocatorRef __nullable alloc,
+			  LSMMapRef mapref, CFArrayRef __nullable subset,
 			  CFIndex numClusters, CFOptionFlags flags);		
 
 /* @enum Clustering Flags
@@ -265,8 +267,8 @@
  *	Returns, in decreasing order of likelihood, the categories or words
  *	that best match when a text is mapped into a map.
  */
-LSMResultRef LSMResultCreate(CFAllocatorRef alloc,
-				LSMMapRef mapref, LSMTextRef textref, 
+LSMResultRef LSMResultCreate(CFAllocatorRef __nullable alloc,
+				LSMMapRef mapref, LSMTextRef textref,
 				CFIndex numResults, CFOptionFlags flags);
 
 /*! @enum Result Flags
@@ -299,25 +301,25 @@
  *
  * Returns the word for the n-th best (zero based) result.
  */
-CFStringRef	LSMResultCopyWord(LSMResultRef result, CFIndex n);
+CFStringRef	__nullable LSMResultCopyWord(LSMResultRef result, CFIndex n);
 
 /*! @function LSMResultCopyToken
  *
  * Returns the token for the n-th best (zero based) result.
  */
-CFDataRef	LSMResultCopyToken(LSMResultRef mapref, CFIndex n);
+CFDataRef __nullable LSMResultCopyToken(LSMResultRef result, CFIndex n);
 
 /*! @function LSMResultCopyWordCluster
  *
  * Returns the cluster of words for the n-th best (zero based) result.
  */
-CFArrayRef	LSMResultCopyWordCluster(LSMResultRef result, CFIndex n);
+CFArrayRef __nullable LSMResultCopyWordCluster(LSMResultRef result, CFIndex n);
 
 /*! @function LSMResultCopyTokenCluster
  *
  * Returns the cluster of tokens for the n-th best (zero based) result.
  */
-CFArrayRef	LSMResultCopyTokenCluster(LSMResultRef mapref, CFIndex n);
+CFArrayRef __nullable LSMResultCopyTokenCluster(LSMResultRef result, CFIndex n);
 
 /*! @function LSMMapWriteToURL
  *
@@ -329,7 +331,7 @@
  *
  *	Loads a map from a given file.
  */
-LSMMapRef LSMMapCreateFromURL(CFAllocatorRef alloc, CFURLRef file, 
+LSMMapRef __nullable LSMMapCreateFromURL(CFAllocatorRef __nullable alloc, CFURLRef file,
 							  CFOptionFlags flags);
 
 /*! @enum Storage Flags
@@ -356,14 +358,14 @@
  *	
  * 	Writes information about a map and/or text to a stream in text form
  */
-OSStatus LSMMapWriteToStream(LSMMapRef mapref, LSMTextRef textref,
+OSStatus LSMMapWriteToStream(LSMMapRef mapref, LSMTextRef __nullable textref,
 							 CFWriteStreamRef stream, CFOptionFlags options);
 
 /*! @function LSMTextCreate
  *
  *	Creates a new text.
  */
-LSMTextRef LSMTextCreate(CFAllocatorRef alloc, LSMMapRef mapref);
+LSMTextRef LSMTextCreate(CFAllocatorRef __nullable alloc, LSMMapRef mapref);
 
 /*! @function LSMTextAddWord
  *
@@ -377,8 +379,8 @@
  *	Breaks a string into words using the locale provided and adds the words 
  *  to the text. 
  */
-OSStatus LSMTextAddWords(LSMTextRef textref, CFStringRef words, 
-						 CFLocaleRef locale, CFOptionFlags flags);
+OSStatus LSMTextAddWords(LSMTextRef textref, CFStringRef words,
+						 CFLocaleRef __nullable locale, CFOptionFlags flags);
 
 /*! @enum Parsing Flags
  *	@discussion Options you can specify for LSMTextAddWords. 
@@ -405,4 +407,6 @@
 }
 #endif
 
+CF_ASSUME_NONNULL_END
+
 #endif /* __LATENTSEMANTICMAPPING__ */

```