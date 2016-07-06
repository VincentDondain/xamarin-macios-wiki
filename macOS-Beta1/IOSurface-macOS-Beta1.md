#IOSurface.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOSurface.framework/Headers/IOSurfaceAPI.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOSurface.framework/Headers/IOSurfaceAPI.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOSurface.framework/Headers/IOSurfaceAPI.h	2015-08-27 04:10:53.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOSurface.framework/Headers/IOSurfaceAPI.h	2016-05-12 08:05:32.000000000 +0200
@@ -12,127 +12,130 @@
 #include <IOKit/IOKitLib.h>
 #include <IOSurface/IOSurfaceBase.h>
 
-__BEGIN_DECLS
+typedef uint32_t IOSurfaceID;
 
-CF_IMPLICIT_BRIDGING_ENABLED
-CF_ASSUME_NONNULL_BEGIN
+typedef CF_OPTIONS(uint32_t, IOSurfaceLockOptions)
+{
+	// If you are not going to modify the data while you hold the lock, you should set this flag to avoid invalidating
+	// any existing caches of the buffer contents.  This flag should be passed both to the lock and unlock functions.
+	// Non-symmetrical usage of this flag will result in undefined behavior.
+	kIOSurfaceLockReadOnly  =		0x00000001,
+	
+	// If you want to detect/avoid a potentially expensive paging operation (such as readback from a GPU to system memory)
+	// when you lock the buffer, you may include this flag.   If locking the buffer requires a readback, the lock will
+	// fail with an error return of kIOReturnCannotLock.
+	kIOSurfaceLockAvoidSync =		0x00000002,
+};
 
 typedef struct  CF_BRIDGED_TYPE(id) __IOSurface *IOSurfaceRef;
 
-typedef uint32_t IOSurfaceID;
+__BEGIN_DECLS
+
+CF_IMPLICIT_BRIDGING_ENABLED
+CF_ASSUME_NONNULL_BEGIN
 
 /* The following list of properties are used with the CFDictionary passed to IOSurfaceCreate(). */
 
 /* kIOSurfaceAllocSize    - CFNumber of the total allocation size of the buffer including all planes.    
 				    Defaults to BufferHeight * BytesPerRow if not specified.   Must be specified for
 				    dimensionless buffers. */
-extern const CFStringRef kIOSurfaceAllocSize					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+extern const CFStringRef kIOSurfaceAllocSize					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
-/* kIOSurfaceWidth  - CFNumber for the width of the IOSurface buffer in pixels.  Required for planar IOSurfaces. */
-extern const CFStringRef kIOSurfaceWidth					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+/* kIOSurfaceWidth  - CFNumber for the width of the IOSurface buffer in pixels.   Required for planar IOSurfaces. */
+extern const CFStringRef kIOSurfaceWidth					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
-/* kIOSurfaceHeight - CFNumber for the height of the IOSurface buffer in pixels. Required for planar IOSurfaces. */
-extern const CFStringRef kIOSurfaceHeight					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+/* kIOSurfaceHeight - CFNumber for the height of the IOSurface buffer in pixels.  Required for planar IOSurfaces. */
+extern const CFStringRef kIOSurfaceHeight					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* kIOSurfaceBytesPerRow - CFNumber for the bytes per row of the buffer.   If not specified, IOSurface will first calculate
-                                   the number full elements required on each row (by rounding up), multiplied by the bytes per element
-				   for this buffer.   That value will then be appropriately aligned. */
-extern const CFStringRef kIOSurfaceBytesPerRow					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+   the number full elements required on each row (by rounding up), multiplied by the bytes per element
+   for this buffer.   That value will then be appropriately aligned. */
+extern const CFStringRef kIOSurfaceBytesPerRow					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* Optional properties for non-planar two dimensional images */
  
-/* kIOSurfaceBitsPerElement - CFNumber for the total number of bytes in an element.  Default to 1. */
-extern const CFStringRef kIOSurfaceBytesPerElement				IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+/* kIOSurfaceBytesPerElement - CFNumber for the total number of bytes in an element.  Default to 1. */
+extern const CFStringRef kIOSurfaceBytesPerElement				IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* kIOSurfaceElementWidth   - CFNumber for how many pixels wide each element is.   Defaults to 1. */ 
-extern const CFStringRef kIOSurfaceElementWidth					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+extern const CFStringRef kIOSurfaceElementWidth					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* kIOSurfaceElementHeight  - CFNumber for how many pixels high each element is.   Defaults to 1. */ 
-extern const CFStringRef kIOSurfaceElementHeight				IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+extern const CFStringRef kIOSurfaceElementHeight				IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* kIOSurfaceOffset - CFNumber for the starting offset into the buffer.  Defaults to 0. */
-extern const CFStringRef kIOSurfaceOffset					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+extern const CFStringRef kIOSurfaceOffset					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* Properties for planar surface buffers */
 
 /* kIOSurfacePlaneInfo    - CFArray describing each image plane in the buffer as a CFDictionary.   The CFArray must have at least one entry. */
-extern const CFStringRef kIOSurfacePlaneInfo					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+extern const CFStringRef kIOSurfacePlaneInfo					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* kIOSurfacePlaneWidth  - CFNumber for the width of this plane in pixels.  Required for image planes. */
-extern const CFStringRef kIOSurfacePlaneWidth					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+extern const CFStringRef kIOSurfacePlaneWidth					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* kIOSurfacePlaneHeight  - CFNumber for the height of this plane in pixels.  Required for image planes. */
-extern const CFStringRef kIOSurfacePlaneHeight					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+extern const CFStringRef kIOSurfacePlaneHeight					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* kIOSurfacePlaneBytesPerRow    - CFNumber for the bytes per row of this plane.  If not specified, IOSurface will first calculate
-                                   the number full elements required on each row (by rounding up), multiplied by the bytes per element
-				   for this plane.   That value will then be appropriately aligned. */
-extern const CFStringRef kIOSurfacePlaneBytesPerRow				IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+   the number full elements required on each row (by rounding up), multiplied by the bytes per element
+   for this plane.   That value will then be appropriately aligned. */
+extern const CFStringRef kIOSurfacePlaneBytesPerRow				IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* kIOSurfacePlaneOffset  - CFNumber for the offset into the buffer for this plane.  If not specified then IOSurface
    will lay out each plane sequentially based on the previous plane's allocation size. */
-extern const CFStringRef kIOSurfacePlaneOffset					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+extern const CFStringRef kIOSurfacePlaneOffset					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* kIOSurfacePlaneSize    - CFNumber for the total data size of this plane.  Defaults to plane height * plane bytes per row if not specified. */
-extern const CFStringRef kIOSurfacePlaneSize					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+extern const CFStringRef kIOSurfacePlaneSize					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* Optional properties for planar surface buffers */
 
 /* kIOSurfacePlaneBase    - CFNumber for the base offset into the buffer for this plane. Optional, defaults to the plane offset */
-extern const CFStringRef kIOSurfacePlaneBase					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+extern const CFStringRef kIOSurfacePlaneBase					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* kIOSurfacePlaneBytesPerElement    - CFNumber for the bytes per element of this plane.  Optional, default is 1. */
-extern const CFStringRef kIOSurfacePlaneBytesPerElement				IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+extern const CFStringRef kIOSurfacePlaneBytesPerElement				IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* kIOSurfacePlaneElementWidth    - CFNumber for the element width of this plane.  Optional, default is 1. */
-extern const CFStringRef kIOSurfacePlaneElementWidth				IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+extern const CFStringRef kIOSurfacePlaneElementWidth				IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* kIOSurfacePlaneElementHeight   - CFNumber for the element height of this plane.  Optional, default is 1. */
-extern const CFStringRef kIOSurfacePlaneElementHeight				IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+extern const CFStringRef kIOSurfacePlaneElementHeight				IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* Optional properties global to the entire IOSurface */
 
 /* kIOSurfaceCacheMode		- CFNumber for the CPU cache mode to be used for the allocation.  Default is kIOMapDefaultCache. */
-extern const CFStringRef kIOSurfaceCacheMode					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+extern const CFStringRef kIOSurfaceCacheMode					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
-/* kIOSurfaceIsGlobal - CFBoolean     If true, the IOSurface may be looked up by any task in the system by its ID.  Deprecated in Mac OS X 10.11. */
-extern const CFStringRef kIOSurfaceIsGlobal					IOSFC_AVAILABLE_BUT_DEPRECATED(__MAC_10_6, __MAC_10_11, __IPHONE_NA, __IPHONE_NA);
+/* kIOSurfaceIsGlobal - CFBoolean     If true, the IOSurface may be looked up by any task in the system by its ID. */
+extern const CFStringRef kIOSurfaceIsGlobal					IOSFC_AVAILABLE_BUT_DEPRECATED(__MAC_10_6, __MAC_10_11, __IPHONE_3_0, __IPHONE_9_0);
 
 /* kIOSurfacePixelFormat - CFNumber	A 32-bit unsigned integer that stores the traditional Mac OS X buffer format  */
-extern const CFStringRef kIOSurfacePixelFormat					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+extern const CFStringRef kIOSurfacePixelFormat					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
+
+/* kIOSurfacePixelSizeCastingAllowed - If false the creator promises that there will be no pixel size casting when used on the GPU.  Default is true.  */
+extern const CFStringRef kIOSurfacePixelSizeCastingAllowed					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_9_0);
 
 CFTypeID IOSurfaceGetTypeID(void)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* Create a brand new IOSurface object */
-IOSurfaceRef __nullable IOSurfaceCreate(CFDictionaryRef properties)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+IOSurfaceRef _Nullable IOSurfaceCreate(CFDictionaryRef properties)
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* Perform an atomic lookup and retain of a IOSurface by its IOSurfaceID.
    Note: Performing multiple lookups of the same IOSurface will *NOT* return
    the same IOSurfaceRef.   If you need to compare two IOSurface objects
    for equality, you must either do so by comparing their IOSurfaceIDs, or by 
    using CFEqual(). */
-IOSurfaceRef __nullable IOSurfaceLookup(IOSurfaceID csid) CF_RETURNS_RETAINED
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+IOSurfaceRef _Nullable IOSurfaceLookup(IOSurfaceID csid) CF_RETURNS_RETAINED
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* Retrieve the unique IOSurfaceID value for a IOSurface */
 IOSurfaceID IOSurfaceGetID(IOSurfaceRef buffer)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
-typedef CF_OPTIONS(uint32_t, IOSurfaceLockOptions)
-{
-	// If you are not going to modify the data while you hold the lock, you should set this flag to avoid invalidating
-	// any existing caches of the buffer contents.  This flag should be passed both to the lock and unlock functions.
-	// Non-symmetrical usage of this flag will result in undefined behavior.
-	kIOSurfaceLockReadOnly  =		0x00000001,
-	
-	// If you want to detect/avoid a potentially expensive paging operation (such as readback from a GPU to system memory)
-	// when you lock the buffer, you may include this flag.   If locking the buffer requires a readback, the lock will
-	// fail with an error return of kIOReturnCannotLock.
-	kIOSurfaceLockAvoidSync =		0x00000002
-};
-			
 /* "Lock" or "Unlock" a IOSurface for reading or writing.
 
     The term "lock" is used loosely in this context, and is simply used along with the
@@ -153,47 +156,47 @@
     so care should be taken to avoid the calls whenever possible.   The seed values are 
     particularly useful for keeping a cache of the buffer contents.
 */
-IOReturn IOSurfaceLock(IOSurfaceRef buffer, IOSurfaceLockOptions options, uint32_t * __nullable seed)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);	
-IOReturn IOSurfaceUnlock(IOSurfaceRef buffer, IOSurfaceLockOptions options, uint32_t * __nullable seed)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+IOReturn IOSurfaceLock(IOSurfaceRef buffer, IOSurfaceLockOptions options, uint32_t * _Nullable seed)
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
+IOReturn IOSurfaceUnlock(IOSurfaceRef buffer, IOSurfaceLockOptions options, uint32_t * _Nullable seed)
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* These routines are all fairly self explanatory.  0 is returned if buffer is invalid or NULL */
 size_t IOSurfaceGetAllocSize(IOSurfaceRef buffer)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 size_t IOSurfaceGetWidth(IOSurfaceRef buffer)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 	
 size_t IOSurfaceGetHeight(IOSurfaceRef buffer)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 size_t IOSurfaceGetBytesPerElement(IOSurfaceRef buffer)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 size_t IOSurfaceGetBytesPerRow(IOSurfaceRef buffer)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 void *IOSurfaceGetBaseAddress(IOSurfaceRef buffer)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 size_t IOSurfaceGetElementWidth(IOSurfaceRef buffer)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 size_t IOSurfaceGetElementHeight(IOSurfaceRef buffer)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 OSType IOSurfaceGetPixelFormat(IOSurfaceRef buffer)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* This will return the current seed value of the buffer and is a cheap call to make to see
    if the contents of the buffer have changed since the last lock/unlock. */
 uint32_t IOSurfaceGetSeed(IOSurfaceRef buffer)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* Return the number of planes in this buffer.  May be 0.   Returns 0 for an invalid or NULL buffer pointer. */
 size_t IOSurfaceGetPlaneCount(IOSurfaceRef buffer)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* These routines return information about a particular plane of a IOSurface.   
 
@@ -203,48 +206,48 @@
    higher level code to treat planar and non-planar buffers is a more uniform fashion. */
 
 size_t IOSurfaceGetWidthOfPlane(IOSurfaceRef buffer, size_t planeIndex)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 size_t IOSurfaceGetHeightOfPlane(IOSurfaceRef buffer, size_t planeIndex)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 size_t IOSurfaceGetBytesPerElementOfPlane(IOSurfaceRef buffer, size_t planeIndex)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 size_t IOSurfaceGetBytesPerRowOfPlane(IOSurfaceRef buffer, size_t planeIndex)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 void *IOSurfaceGetBaseAddressOfPlane(IOSurfaceRef buffer, size_t planeIndex)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 size_t IOSurfaceGetElementWidthOfPlane(IOSurfaceRef buffer, size_t planeIndex)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 size_t IOSurfaceGetElementHeightOfPlane(IOSurfaceRef buffer, size_t planeIndex)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* These calls let you attach CF property list types to a IOSurface buffer.  These calls are 
    expensive (they essentially must serialize the data into the kernel) and thus should be avoided whenever
    possible.   Note:  These functions can not be used to change the underlying surface properties. */
 void IOSurfaceSetValue(IOSurfaceRef buffer, CFStringRef key, CFTypeRef value)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
-CFTypeRef __nullable IOSurfaceCopyValue(IOSurfaceRef buffer, CFStringRef key)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+CFTypeRef _Nullable IOSurfaceCopyValue(IOSurfaceRef buffer, CFStringRef key)
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 void IOSurfaceRemoveValue(IOSurfaceRef buffer, CFStringRef key)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* Bulk setters and getters for setting, retrieving or removing the entire
    set of values at once .*/
 void IOSurfaceSetValues(IOSurfaceRef buffer, CFDictionaryRef keysAndValues)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
-CFDictionaryRef __nullable IOSurfaceCopyAllValues(IOSurfaceRef buffer)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+CFDictionaryRef _Nullable IOSurfaceCopyAllValues(IOSurfaceRef buffer)
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 void IOSurfaceRemoveAllValues(IOSurfaceRef buffer)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* This call lets you get a mach_port_t that holds a reference to the IOSurface. This is useful 
    if you need to atomically or securely pass an IOSurface to another task without making the surface global to
@@ -252,22 +255,22 @@
    Note: Any live mach ports created from an IOSurfaceRef implicity increase the IOSurface's global use
    count by one until the port is deleted. */
 mach_port_t IOSurfaceCreateMachPort(IOSurfaceRef buffer)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* This call lets you take a mach_port_t created via IOSurfaceCreatePort() and recreate an IOSurfaceRef from it.
    Note: This call does NOT destroy the port. */
-IOSurfaceRef __nullable IOSurfaceLookupFromMachPort(mach_port_t port) CF_RETURNS_RETAINED
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+IOSurfaceRef _Nullable IOSurfaceLookupFromMachPort(mach_port_t port) CF_RETURNS_RETAINED
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 	
 /* This call lets you get an xpc_object_t that holds a reference to the IOSurface.
    Note: Any live XPC objects created from an IOSurfaceRef implicity increase the IOSurface's global use
    count by one until the object is destroyed. */
 xpc_object_t IOSurfaceCreateXPCObject(IOSurfaceRef aSurface) XPC_RETURNS_RETAINED
-	IOSFC_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_5_0);
 
 /* This call lets you take an xpc_object_t created via IOSurfaceCreatePort() and recreate an IOSurfaceRef from it. */
-IOSurfaceRef __nullable IOSurfaceLookupFromXPCObject(xpc_object_t xobj) CF_RETURNS_RETAINED
-	IOSFC_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_NA);
+IOSurfaceRef _Nullable IOSurfaceLookupFromXPCObject(xpc_object_t xobj) CF_RETURNS_RETAINED
+	IOSFC_AVAILABLE_STARTING(__MAC_10_7, __IPHONE_5_0);
 
 /* 
    IOSurfaceGetPropertyMaximum() will return the maximum of a given property that is guaranteed to be 
@@ -289,7 +292,7 @@
       
 */   
 size_t	IOSurfaceGetPropertyMaximum(CFStringRef property)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* 
    If a property has a particular alignment requirement, then IOSurfaceGetPropertyAlignment() will return it.  
@@ -305,12 +308,12 @@
    
 */   
 size_t	IOSurfaceGetPropertyAlignment(CFStringRef property)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* This is a convenience function to automatically align property values.  For properties with no alignment
    requirements, the original value will be returned. */
 size_t	IOSurfaceAlignProperty(CFStringRef property, size_t value)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 
 /* There are cases where it is useful to know whether or not an IOSurface buffer is considered to be "in use"
@@ -335,19 +338,38 @@
    
 /* Increment the per-process usage count for an IOSurface */
 void IOSurfaceIncrementUseCount(IOSurfaceRef buffer)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 	
 /* Decrement the per-process usage count for an IOSurface */
 void IOSurfaceDecrementUseCount(IOSurfaceRef buffer)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* Return the per-process usage count for an IOSurface */
 int32_t IOSurfaceGetUseCount(IOSurfaceRef buffer)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 	
 /* Returns true of an IOSurface is in use by any process in the system, otherwise false. */
 Boolean IOSurfaceIsInUse(IOSurfaceRef buffer)
-	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_NA);
+	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
+
+/* Rerturns true if this IOSurface allows pixel size casting */
+Boolean IOSurfaceAllowsPixelSizeCasting(IOSurfaceRef buffer)
+	IOSFC_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+
+#if TARGET_OS_EMBEDDED
+// These will go away soon.
+extern const CFStringRef kIOSurfaceDisplayDitherThresholds;
+extern const CFStringRef kIOSurfaceDisplayDitherYThresholds;
+extern const CFStringRef kIOSurfaceDisplayDitherCbThresholds;
+extern const CFStringRef kIOSurfaceDisplayDitherCrThresholds;
+extern const CFStringRef kIOSurfaceTimingInfo;
+extern const CFStringRef kIOSurfaceGPUTimes;
+extern const CFStringRef kIOSurfaceDisplayTimes;
+extern const CFStringRef kIOSurfaceScalerTimes;
+extern const CFStringRef kIOSurfaceEncoderTimes;
+extern const CFStringRef kIOSurfaceDecoderTimes;
+extern const CFStringRef kIOSurfaceTouchEventTimes;
+#endif
 
 __END_DECLS
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOSurface.framework/Headers/IOSurfaceBase.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOSurface.framework/Headers/IOSurfaceBase.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/IOSurface.framework/Headers/IOSurfaceBase.h	2015-08-27 04:10:53.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOSurface.framework/Headers/IOSurfaceBase.h	2016-05-12 08:05:32.000000000 +0200
@@ -11,19 +11,18 @@
 
 #include <sys/cdefs.h>
 
-#  include <AvailabilityMacros.h>
-#  if defined(MAC_OS_X_VERSION_10_11)
-#    include <Availability.h>
-#  endif /* defined(MAC_OS_X_VERSION_10_11) */
+#include <Availability.h>
 
-#if !defined(MAC_OS_X_VERSION_10_11) || defined(IOSFC_BUILDING_IOSFC)
+#if !(defined(MAC_OS_X_VERSION_10_12) || defined(__IPHONE_10_0)) || defined(IOSFC_BUILDING_IOSFC)
 #  define IOSFC_DEPRECATED 
 #  define IOSFC_AVAILABLE_STARTING(_mac,_iphone)
 #  define IOSFC_AVAILABLE_BUT_DEPRECATED(_mac,_macDep,_iphone,_iphoneDep)
+#  define IOSFC_CLASS_AVAILABLE(a, b)
 #else /* !defined(IOSFC_BUILDING_IOSFC) */
 #  define IOSFC_DEPRECATED DEPRECATED_ATTRIBUTE
 #  define IOSFC_AVAILABLE_STARTING __OSX_AVAILABLE_STARTING
 #  define IOSFC_AVAILABLE_BUT_DEPRECATED __OSX_AVAILABLE_BUT_DEPRECATED
+#  define IOSFC_CLASS_AVAILABLE NS_CLASS_AVAILABLE
 #endif /* !defined(IOSFC_BUILDING_IOSFC) */
 
 #include <CoreFoundation/CFBase.h>

```