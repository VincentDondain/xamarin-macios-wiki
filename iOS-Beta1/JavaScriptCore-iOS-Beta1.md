#JavaScriptCore.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSBase.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSBase.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSBase.h	2015-10-02 23:34:51.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSBase.h	2016-05-25 07:00:15.000000000 +0200
@@ -57,6 +57,8 @@
 /*! @typedef JSPropertyNameAccumulatorRef An ordered set used to collect the names of a JavaScript object's properties. */
 typedef struct OpaqueJSPropertyNameAccumulator* JSPropertyNameAccumulatorRef;
 
+/*! @typedef JSTypedArrayBytesDeallocator A function used to deallocate bytes passed to a Typed Array constructor. The function should take two arguments. The first is a pointer to the bytes that were originally passed to the Typed Array constructor. The second is a pointer to additional information desired at the time the bytes are to be freed. */
+typedef void (*JSTypedArrayBytesDeallocator)(void* bytes, void* deallocatorContext);
 
 /* JavaScript data types */
 
@@ -136,7 +138,7 @@
 
 /* Enable the Objective-C API for platforms with a modern runtime. */
 #if !defined(JSC_OBJC_API_ENABLED)
-#define JSC_OBJC_API_ENABLED (defined(__clang__) && defined(__APPLE__) && ((defined(__MAC_OS_X_VERSION_MIN_REQUIRED) && __MAC_OS_X_VERSION_MIN_REQUIRED >= 1090 && !defined(__i386__)) || (defined(TARGET_OS_IPHONE) && TARGET_OS_IPHONE)))
+#define JSC_OBJC_API_ENABLED (defined(__clang__) && defined(__APPLE__) && !defined(BUILDING_GTK__) && ((defined(__MAC_OS_X_VERSION_MIN_REQUIRED) && !defined(__i386__)) || (defined(TARGET_OS_IPHONE) && TARGET_OS_IPHONE)))
 #endif
 
 #endif /* JSBase_h */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSContext.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSContext.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSContext.h	2015-10-02 23:34:51.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSContext.h	2016-05-25 07:05:59.000000000 +0200
@@ -35,14 +35,9 @@
 
 /*!
 @interface
-@discussion An instance of JSContext represents a JavaScript execution environment. All
- JavaScript execution takes place within a context.
- JSContext is also used to manage the life-cycle of objects within the
- JavaScript virtual machine. Every instance of JSValue is associated with a
- JSContext via a strong reference. The JSValue will keep the JSContext it
- references alive so long as the JSValue remains alive. When all of the JSValues
- that reference a particular JSContext have been deallocated the JSContext
- will be deallocated unless it has been previously retained.
+@discussion A JSContext is a JavaScript execution environment. All
+ JavaScript execution takes place within a context, and all JavaScript values
+ are tied to a context.
 */
 NS_CLASS_AVAILABLE(10_9, 7_0)
 @interface JSContext : NSObject
@@ -155,9 +150,6 @@
  This property may also be used to check for uncaught exceptions arising from
  API function calls (since the default behaviour of <code>exceptionHandler</code> is to
  assign an uncaught exception to this property).
-
- If a JSValue originating from a different JSVirtualMachine than this context
- is assigned to this property, an Objective-C exception will be raised.
 */
 @property (strong) JSValue *exception;
 
@@ -166,17 +158,16 @@
 @discussion If a call to an API function results in an uncaught JavaScript exception, the
  <code>exceptionHandler</code> block will be invoked. The default implementation for the
  exception handler will store the exception to the exception property on
- context. As a consequence the default behaviour is for unhandled exceptions
+ context. As a consequence the default behaviour is for uncaught exceptions
  occurring within a callback from JavaScript to be rethrown upon return.
- Setting this value to nil will result in all uncaught exceptions thrown from
- the API being silently consumed.
+ Setting this value to nil will cause all exceptions occurring
+ within a callback from JavaScript to be silently caught.
 */
 @property (copy) void(^exceptionHandler)(JSContext *context, JSValue *exception);
 
 /*!
 @property
-@discussion All instances of JSContext are associated with a single JSVirtualMachine. The
- virtual machine provides an "object space" or set of execution resources.
+@discussion All instances of JSContext are associated with a JSVirtualMachine.
 */
 @property (readonly, strong) JSVirtualMachine *virtualMachine;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSExport.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSExport.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSExport.h	2015-10-02 23:34:51.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSExport.h	2016-05-25 06:33:11.000000000 +0200
@@ -29,40 +29,39 @@
 
 /*!
 @protocol
-@abstract JSExport provides a declarative way to export Objective-C instance methods,
- class methods, and properties to JavaScript code.
-
-@discussion When a JavaScript value is created from an instance of an Objective-C class
- for which no copying conversion is specified a JavaScript wrapper object will
- be created.
-
- In JavaScript, inheritance is supported via a chain of prototype objects, and
- for each Objective-C class (and per JSContext) an object appropriate for use
- as a prototype will be provided. For the class NSObject the prototype object
- will be the JavaScript context's Object Prototype. For all other Objective-C
- classes a Prototype object will be created. The Prototype object for a given
+@abstract JSExport provides a declarative way to export Objective-C objects and
+ classes -- including properties, instance methods, class methods, and
+ initializers -- to JavaScript.
+
+@discussion When an Objective-C object is exported to JavaScript, a JavaScript
+ wrapper object is created.
+
+ In JavaScript, inheritance works via a chain of prototype objects.
+ For each Objective-C class in each JSContext, an object appropriate for use
+ as a prototype will be provided. For the class NSObject the prototype
+ will be the Object prototype. For all other Objective-C
+ classes a prototype will be created. The prototype for a given
  Objective-C class will have its internal [Prototype] property set to point to
- the Prototype object of the Objective-C class's superclass. As such the
+ the prototype created for the Objective-C class's superclass. As such the
  prototype chain for a JavaScript wrapper object will reflect the wrapped
  Objective-C type's inheritance hierarchy.
 
- In addition to the Prototype object a JavaScript Constructor object will also
- be produced for each Objective-C class. The Constructor object has a property
- named 'prototype' that references the Prototype object, and the Prototype
- object has a property named 'constructor' that references the Constructor.
- The Constructor object is not callable.
-
- By default no methods or properties of the Objective-C class will be exposed
- to JavaScript; however methods and properties may explicitly be exported.
- For each protocol that a class conforms to, if the protocol incorporates the
- protocol JSExport, then the protocol will be interpreted as a list of methods
- and properties to be exported to JavaScript.
-
- For each instance method being exported a corresponding JavaScript function
- will be assigned as a property of the Prototype object. For each Objective-C
- property being exported a JavaScript accessor property will be created on the
- Prototype. For each class method exported a JavaScript function will be
- created on the Constructor object. For example:
+ JavaScriptCore also produces a constructor for each Objective-C class. The
+ constructor has a property named 'prototype' that references the prototype,
+ and the prototype has a property named 'constructor' that references the
+ constructor.
+
+ By default JavaScriptCore does not export any methods or properties from an
+ Objective-C class to JavaScript; however methods and properties may be exported
+ explicitly using JSExport. For each protocol that a class conforms to, if the
+ protocol incorporates the protocol JSExport, JavaScriptCore exports the methods
+ and properties in that protocol to JavaScript
+
+ For each exported instance method JavaScriptCore will assign a corresponding
+ JavaScript function to the prototype. For each exported Objective-C property
+ JavaScriptCore will assign a corresponding JavaScript accessor to the prototype.
+ For each exported class method JavaScriptCore will assign a corresponding
+ JavaScript function to the constructor. For example:
 
 <pre>
 @textblock
@@ -86,34 +85,29 @@
  since the class conforms to the <code>MyClassJavaScriptMethods</code> protocol, and this
  protocol incorporates <code>JSExport</code>. <code>bar</code> will not be exported.
 
- Properties, arguments, and return values of the following types are
- supported:
+ JSExport supports properties, arguments, and return values of the following types:
+
+ Primitive numbers: signed values up to 32-bits convert using JSValue's
+ valueWithInt32/toInt32. Unsigned values up to 32-bits convert using JSValue's
+ valueWithUInt32/toUInt32. All other numeric values convert using JSValue's
+ valueWithDouble/toDouble.
+
+ BOOL: values convert using JSValue's valueWithBool/toBool.
+
+ id: values convert using JSValue's valueWithObject/toObject.
+
+ Objective-C instance pointers: Pointers convert using JSValue's
+ valueWithObjectOfClass/toObject.
+
+ C structs: C structs for CGPoint, NSRange, CGRect, and CGSize convert using
+ JSValue's appropriate methods. Other C structs are not supported.
+
+ Blocks: Blocks convert using JSValue's valueWithObject/toObject.
 
- Primitive numbers: signed values of up to 32-bits are converted in a manner
-    consistent with valueWithInt32/toInt32, unsigned values of up to 32-bits
-    are converted in a manner consistent with valueWithUInt32/toUInt32, all
-    other numeric values are converted consistently with valueWithDouble/
-    toDouble.
-
- BOOL: values are converted consistently with valueWithBool/toBool.
-
- id: values are converted consistently with valueWithObject/toObject.
-
- Objective-C Class: - where the type is a pointer to a specified Objective-C
-    class, conversion is consistent with valueWithObjectOfClass/toObject.
-
- struct types: C struct types are supported, where JSValue provides support
-    for the given type. Support is built in for CGPoint, NSRange, CGRect, and
-    CGSize.
-
- block types: Blocks can only be passed if they had been converted 
-    successfully by valueWithObject/toObject previously.
-
- For any interface that conforms to JSExport the normal copying conversion for
- built in types will be inhibited - so, for example, if an instance that
- derives from NSString but conforms to JSExport is passed to valueWithObject:
- then a wrapper object for the Objective-C object will be returned rather than
- a JavaScript string primitive.
+ All objects that conform to JSExport convert to JavaScript wrapper objects,
+ even if they subclass classes that would otherwise behave differently. For
+ example, if a subclass of NSString conforms to JSExport, it converts to
+ JavaScript as a wrapper object rather than a JavaScript string.
 */
 @protocol JSExport
 @end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSManagedValue.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSManagedValue.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSManagedValue.h	2015-10-02 23:34:51.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSManagedValue.h	2016-05-25 06:27:58.000000000 +0200
@@ -37,18 +37,16 @@
 /*!
 @interface
 @discussion JSManagedValue represents a "conditionally retained" JSValue. 
- "Conditionally retained" means that as long as either the JSManagedValue's 
- JavaScript value is reachable through the JavaScript object graph
- or the JSManagedValue object is reachable through the external Objective-C 
- object graph as reported to the JSVirtualMachine using 
- addManagedReference:withOwner:, the corresponding JavaScript value will 
- be retained. However, if neither of these conditions are true, the 
+ "Conditionally retained" means that as long as the JSManagedValue's 
+ JSValue is reachable through the JavaScript object graph,
+ or through the Objective-C object graph reported to the JSVirtualMachine using
+ addManagedReference:withOwner:, the corresponding JSValue will 
+ be retained. However, if neither graph reaches the JSManagedValue, the 
  corresponding JSValue will be released and set to nil.
 
- The primary use case for JSManagedValue is for safely referencing JSValues 
- from the Objective-C heap. It is incorrect to store a JSValue into an 
- Objective-C heap object, as this can very easily create a reference cycle, 
- keeping the entire JSContext alive.
+The primary use for a JSManagedValue is to store a JSValue in an Objective-C
+or Swift object that is exported to JavaScript. It is incorrect to store a JSValue
+in an object that is exported to JavaScript, since doing so creates a retain cycle.
 */ 
 NS_CLASS_AVAILABLE(10_9, 7_0)
 @interface JSManagedValue : NSObject
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSTypedArray.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSTypedArray.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSTypedArray.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSTypedArray.h	2016-05-25 06:33:10.000000000 +0200
@@ -0,0 +1,180 @@
+/*
+ * Copyright (C) 2015 Dominic Szablewski (dominic@phoboslab.org)
+ * Copyright (C) 2015-2016 Apple Inc. All rights reserved.
+ *
+ * Redistribution and use in source and binary forms, with or without
+ * modification, are permitted provided that the following conditions
+ * are met:
+ * 1. Redistributions of source code must retain the above copyright
+ *    notice, this list of conditions and the following disclaimer.
+ * 2. Redistributions in binary form must reproduce the above copyright
+ *    notice, this list of conditions and the following disclaimer in the
+ *    documentation and/or other materials provided with the distribution.
+ *
+ * THIS SOFTWARE IS PROVIDED BY APPLE COMPUTER, INC. ``AS IS'' AND ANY
+ * EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
+ * IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
+ * PURPOSE ARE DISCLAIMED.  IN NO EVENT SHALL APPLE COMPUTER, INC. OR
+ * CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
+ * EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
+ * PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
+ * PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY
+ * OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
+ * (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
+ * OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
+ */
+
+#ifndef JSTypedArray_h
+#define JSTypedArray_h
+
+#include <JavaScriptCore/JSBase.h>
+#include <JavaScriptCore/JSValueRef.h>
+
+#ifdef __cplusplus
+extern "C" {
+#endif
+
+// ------------- Typed Array functions --------------
+
+/*!
+ @function
+ @abstract           Creates a JavaScript Typed Array object with the given number of elements.
+ @param ctx          The execution context to use.
+ @param arrayType    A value identifying the type of array to create. If arrayType is kJSTypedArrayTypeNone or kJSTypedArrayTypeArrayBuffer then NULL will be returned.
+ @param length       The number of elements to be in the new Typed Array.
+ @param exception    A pointer to a JSValueRef in which to store an exception, if any. Pass NULL if you do not care to store an exception.
+ @result             A JSObjectRef that is a Typed Array with all elements set to zero or NULL if there was an error.
+ */
+JS_EXPORT JSObjectRef JSObjectMakeTypedArray(JSContextRef ctx, JSTypedArrayType arrayType, size_t length, JSValueRef* exception) CF_AVAILABLE(10_12, 10_0);
+
+/*!
+ @function
+ @abstract                 Creates a JavaScript Typed Array object from an existing pointer.
+ @param ctx                The execution context to use.
+ @param arrayType          A value identifying the type of array to create. If arrayType is kJSTypedArrayTypeNone or kJSTypedArrayTypeArrayBuffer then NULL will be returned.
+ @param bytes              A pointer to the byte buffer to be used as the backing store of the Typed Array object.
+ @param byteLength         The number of bytes pointed to by the parameter bytes.
+ @param bytesDeallocator   The allocator to use to deallocate the external buffer when the JSTypedArrayData object is deallocated.
+ @param deallocatorContext A pointer to pass back to the deallocator.
+ @param exception          A pointer to a JSValueRef in which to store an exception, if any. Pass NULL if you do not care to store an exception.
+ @result                   A JSObjectRef Typed Array whose backing store is the same as the one pointed to by bytes or NULL if there was an error.
+ @discussion               If an exception is thrown during this function the bytesDeallocator will always be called.
+ */
+JS_EXPORT JSObjectRef JSObjectMakeTypedArrayWithBytesNoCopy(JSContextRef ctx, JSTypedArrayType arrayType, void* bytes, size_t byteLength, JSTypedArrayBytesDeallocator bytesDeallocator, void* deallocatorContext, JSValueRef* exception) CF_AVAILABLE(10_12, 10_0);
+
+/*!
+ @function
+ @abstract           Creates a JavaScript Typed Array object from an existing JavaScript Array Buffer object.
+ @param ctx          The execution context to use.
+ @param arrayType    A value identifying the type of array to create. If arrayType is kJSTypedArrayTypeNone or kJSTypedArrayTypeArrayBuffer then NULL will be returned.
+ @param buffer       An Array Buffer object that should be used as the backing store for the created JavaScript Typed Array object.
+ @param exception    A pointer to a JSValueRef in which to store an exception, if any. Pass NULL if you do not care to store an exception.
+ @result             A JSObjectRef that is a Typed Array or NULL if there was an error. The backing store of the Typed Array will be buffer.
+ */
+JS_EXPORT JSObjectRef JSObjectMakeTypedArrayWithArrayBuffer(JSContextRef ctx, JSTypedArrayType arrayType, JSObjectRef buffer, JSValueRef* exception) CF_AVAILABLE(10_12, 10_0);
+
+/*!
+ @function
+ @abstract           Creates a JavaScript Typed Array object from an existing JavaScript Array Buffer object with the given offset and length.
+ @param ctx          The execution context to use.
+ @param arrayType    A value identifying the type of array to create. If arrayType is kJSTypedArrayTypeNone or kJSTypedArrayTypeArrayBuffer then NULL will be returned.
+ @param buffer       An Array Buffer object that should be used as the backing store for the created JavaScript Typed Array object.
+ @param byteOffset   The byte offset for the created Typed Array. byteOffset should aligned with the element size of arrayType.
+ @param length       The number of elements to include in the Typed Array.
+ @param exception    A pointer to a JSValueRef in which to store an exception, if any. Pass NULL if you do not care to store an exception.
+ @result             A JSObjectRef that is a Typed Array or NULL if there was an error. The backing store of the Typed Array will be buffer.
+ */
+JS_EXPORT JSObjectRef JSObjectMakeTypedArrayWithArrayBufferAndOffset(JSContextRef ctx, JSTypedArrayType arrayType, JSObjectRef buffer, size_t byteOffset, size_t length, JSValueRef* exception) CF_AVAILABLE(10_12, 10_0);
+
+/*!
+ @function
+ @abstract           Returns a temporary pointer to the backing store of a JavaScript Typed Array object.
+ @param ctx          The execution context to use.
+ @param object       The Typed Array object whose backing store pointer to return.
+ @param exception    A pointer to a JSValueRef in which to store an exception, if any. Pass NULL if you do not care to store an exception.
+ @result             A pointer to the raw data buffer that serves as object's backing store or NULL if object is not a Typed Array object.
+ @discussion         The pointer returned by this function is temporary and is not guaranteed to remain valid across JavaScriptCore API calls.
+ */
+JS_EXPORT void* JSObjectGetTypedArrayBytesPtr(JSContextRef ctx, JSObjectRef object, JSValueRef* exception) CF_AVAILABLE(10_12, 10_0);
+
+/*!
+ @function
+ @abstract           Returns the length of a JavaScript Typed Array object.
+ @param ctx          The execution context to use.
+ @param object       The Typed Array object whose length to return.
+ @param exception    A pointer to a JSValueRef in which to store an exception, if any. Pass NULL if you do not care to store an exception.
+ @result             The length of the Typed Array object or 0 if the object is not a Typed Array object.
+ */
+JS_EXPORT size_t JSObjectGetTypedArrayLength(JSContextRef ctx, JSObjectRef object, JSValueRef* exception) CF_AVAILABLE(10_12, 10_0);
+
+/*!
+ @function
+ @abstract           Returns the byte length of a JavaScript Typed Array object.
+ @param ctx          The execution context to use.
+ @param object       The Typed Array object whose byte length to return.
+ @param exception    A pointer to a JSValueRef in which to store an exception, if any. Pass NULL if you do not care to store an exception.
+ @result             The byte length of the Typed Array object or 0 if the object is not a Typed Array object.
+ */
+JS_EXPORT size_t JSObjectGetTypedArrayByteLength(JSContextRef ctx, JSObjectRef object, JSValueRef* exception) CF_AVAILABLE(10_12, 10_0);
+
+/*!
+ @function
+ @abstract           Returns the byte offset of a JavaScript Typed Array object.
+ @param ctx          The execution context to use.
+ @param object       The Typed Array object whose byte offset to return.
+ @param exception    A pointer to a JSValueRef in which to store an exception, if any. Pass NULL if you do not care to store an exception.
+ @result             The byte offset of the Typed Array object or 0 if the object is not a Typed Array object.
+ */
+JS_EXPORT size_t JSObjectGetTypedArrayByteOffset(JSContextRef ctx, JSObjectRef object, JSValueRef* exception) CF_AVAILABLE(10_12, 10_0);
+
+/*!
+ @function
+ @abstract           Returns the JavaScript Array Buffer object that is used as the backing of a JavaScript Typed Array object.
+ @param ctx          The execution context to use.
+ @param object       The JSObjectRef whose Typed Array type data pointer to obtain.
+ @param exception    A pointer to a JSValueRef in which to store an exception, if any. Pass NULL if you do not care to store an exception.
+ @result             A JSObjectRef with a JSTypedArrayType of kJSTypedArrayTypeArrayBuffer or NULL if object is not a Typed Array.
+ */
+JS_EXPORT JSObjectRef JSObjectGetTypedArrayBuffer(JSContextRef ctx, JSObjectRef object, JSValueRef* exception) CF_AVAILABLE(10_12, 10_0);
+
+// ------------- Array Buffer functions -------------
+
+/*!
+ @function
+ @abstract                 Creates a JavaScript Array Buffer object from an existing pointer.
+ @param ctx                The execution context to use.
+ @param bytes              A pointer to the byte buffer to be used as the backing store of the Typed Array object.
+ @param byteLength         The number of bytes pointed to by the parameter bytes.
+ @param bytesDeallocator   The allocator to use to deallocate the external buffer when the Typed Array data object is deallocated.
+ @param deallocatorContext A pointer to pass back to the deallocator.
+ @param exception          A pointer to a JSValueRef in which to store an exception, if any. Pass NULL if you do not care to store an exception.
+ @result                   A JSObjectRef Array Buffer whose backing store is the same as the one pointed to by bytes or NULL if there was an error.
+ @discussion               If an exception is thrown during this function the bytesDeallocator will always be called.
+ */
+JS_EXPORT JSObjectRef JSObjectMakeArrayBufferWithBytesNoCopy(JSContextRef ctx, void* bytes, size_t byteLength, JSTypedArrayBytesDeallocator bytesDeallocator, void* deallocatorContext, JSValueRef* exception) CF_AVAILABLE(10_12, 10_0);
+
+/*!
+ @function
+ @abstract         Returns a pointer to the data buffer that serves as the backing store for a JavaScript Typed Array object.
+ @param buffer     The Array Buffer object whose internal backing store pointer to return.
+ @param exception  A pointer to a JSValueRef in which to store an exception, if any. Pass NULL if you do not care to store an exception.
+ @result           A pointer to the raw data buffer that serves as object's backing store or NULL if object is not an Array Buffer object.
+ @discussion       The pointer returned by this function is temporary and is not guaranteed to remain valid across JavaScriptCore API calls.
+ */
+JS_EXPORT void* JSObjectGetArrayBufferBytesPtr(JSContextRef ctx, JSObjectRef object, JSValueRef* exception) CF_AVAILABLE(10_12, 10_0);
+
+/*!
+ @function
+ @abstract         Returns the number of bytes in a JavaScript data object.
+ @param ctx        The execution context to use.
+ @param object     The JS Arary Buffer object whose length in bytes to return.
+ @param exception  A pointer to a JSValueRef in which to store an exception, if any. Pass NULL if you do not care to store an exception.
+ @result           The number of bytes stored in the data object.
+ */
+JS_EXPORT size_t JSObjectGetArrayBufferByteLength(JSContextRef ctx, JSObjectRef object, JSValueRef* exception) CF_AVAILABLE(10_12, 10_0);
+
+#ifdef __cplusplus
+}
+#endif
+
+#endif /* JSTypedArray_h */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSValue.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSValue.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSValue.h	2015-10-02 23:34:51.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSValue.h	2016-05-25 06:33:11.000000000 +0200
@@ -34,21 +34,15 @@
 
 /*!
 @interface
-@discussion A JSValue is a reference to a value within the JavaScript object space of a
- JSVirtualMachine. All instances of JSValue originate from a JSContext and
- hold a strong reference to this JSContext. As long as any value associated with 
- a particular JSContext is retained, that JSContext will remain alive. 
- Where an instance method is invoked upon a JSValue, and this returns another 
- JSValue, the returned JSValue will originate from the same JSContext as the 
- JSValue on which the method was invoked.
-
- All JavaScript values are associated with a particular JSVirtualMachine
- (the associated JSVirtualMachine is available indirectly via the context
- property). An instance of JSValue may only be passed as an argument to
- methods on instances of JSValue and JSContext that belong to the same
- JSVirtualMachine - passing a JSValue to a method on an object originating
- from a different JSVirtualMachine will result in an Objective-C exception
- being raised.
+@discussion A JSValue is a reference to a JavaScript value. Every JSValue
+ originates from a JSContext and holds a strong reference to it.
+ When a JSValue instance method creates a new JSValue, the new value
+ originates from the same JSContext.
+
+ All JSValues values also originate from a JSVirtualMachine
+ (available indirectly via the context property). It is an error to pass a
+ JSValue to a method or property of a JSValue or JSContext originating from a
+ different JSVirtualMachine. Doing so will raise an Objective-C exception.
 */
 NS_CLASS_AVAILABLE(10_9, 7_0)
 @interface JSValue : NSObject
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSValueRef.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSValueRef.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSValueRef.h	2015-10-02 23:34:51.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JSValueRef.h	2016-05-25 07:05:59.000000000 +0200
@@ -52,6 +52,36 @@
     kJSTypeObject
 } JSType;
 
+/*!
+ @enum JSTypedArrayType
+ @abstract     A constant identifying the Typed Array type of a JSObjectRef.
+ @constant     kJSTypedArrayTypeInt8Array            Int8Array
+ @constant     kJSTypedArrayTypeInt16Array           Int16Array
+ @constant     kJSTypedArrayTypeInt32Array           Int32Array
+ @constant     kJSTypedArrayTypeUint8Array           Uint8Array
+ @constant     kJSTypedArrayTypeUint8ClampedArray    Uint8ClampedArray
+ @constant     kJSTypedArrayTypeUint16Array          Uint16Array
+ @constant     kJSTypedArrayTypeUint32Array          Uint32Array
+ @constant     kJSTypedArrayTypeFloat32Array         Float32Array
+ @constant     kJSTypedArrayTypeFloat64Array         Float64Array
+ @constant     kJSTypedArrayTypeArrayBuffer          ArrayBuffer
+ @constant     kJSTypedArrayTypeNone                 Not a Typed Array
+
+ */
+typedef enum {
+    kJSTypedArrayTypeInt8Array,
+    kJSTypedArrayTypeInt16Array,
+    kJSTypedArrayTypeInt32Array,
+    kJSTypedArrayTypeUint8Array,
+    kJSTypedArrayTypeUint8ClampedArray,
+    kJSTypedArrayTypeUint16Array,
+    kJSTypedArrayTypeUint32Array,
+    kJSTypedArrayTypeFloat32Array,
+    kJSTypedArrayTypeFloat64Array,
+    kJSTypedArrayTypeArrayBuffer,
+    kJSTypedArrayTypeNone,
+} JSTypedArrayType CF_ENUM_AVAILABLE(10_12, 10_0);
+
 #ifdef __cplusplus
 extern "C" {
 #endif
@@ -147,6 +177,16 @@
 */
 JS_EXPORT bool JSValueIsDate(JSContextRef ctx, JSValueRef value) CF_AVAILABLE(10_11, 9_0);
 
+/*!
+@function
+@abstract           Returns a JavaScript value's Typed Array type.
+@param ctx          The execution context to use.
+@param value        The JSValue whose Typed Array type to return.
+@param exception    A pointer to a JSValueRef in which to store an exception, if any. Pass NULL if you do not care to store an exception.
+@result             A value of type JSTypedArrayType that identifies value's Typed Array type, or kJSTypedArrayTypeNone if the value is not a Typed Array object.
+ */
+JS_EXPORT JSTypedArrayType JSValueGetTypedArrayType(JSContextRef ctx, JSValueRef value, JSValueRef* exception) CF_AVAILABLE(10_12, 10_0);
+
 /* Comparing values */
 
 /*!
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JavaScript.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JavaScript.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JavaScript.h	2015-10-02 23:34:51.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/JavaScript.h	2016-05-25 06:27:58.000000000 +0200
@@ -31,6 +31,7 @@
 #include <JavaScriptCore/JSContextRef.h>
 #include <JavaScriptCore/JSStringRef.h>
 #include <JavaScriptCore/JSObjectRef.h>
+#include <JavaScriptCore/JSTypedArray.h>
 #include <JavaScriptCore/JSValueRef.h>
 
 #endif /* JavaScript_h */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/WebKitAvailability.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/WebKitAvailability.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/WebKitAvailability.h	2015-10-02 23:34:52.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/JavaScriptCore.framework/Headers/WebKitAvailability.h	2016-05-25 06:27:58.000000000 +0200
@@ -26,7 +26,7 @@
 #ifndef __WebKitAvailability__
 #define __WebKitAvailability__
 
-#ifdef __APPLE__
+#if defined(__APPLE__)
 
 #include <AvailabilityMacros.h>
 #include <CoreFoundation/CoreFoundation.h>
@@ -46,6 +46,10 @@
 #define __NSi_10_11 introduced=10.0 // Use 10.0 to indicate that everything is available.
 #endif
 
+#ifndef __NSi_10_12 // Building from trunk rather than SDK.
+#define __NSi_10_12 introduced=10.0 // Use 10.0 to indicate that everything is available.
+#endif
+
 #ifndef __AVAILABILITY_INTERNAL__MAC_10_9
 #define __AVAILABILITY_INTERNAL__MAC_10_9
 #endif
@@ -64,8 +68,16 @@
 
 #endif /* __MAC_OS_X_VERSION_MIN_REQUIRED <= 101100 */
 
+#if defined(BUILDING_GTK__)
+#undef CF_AVAILABLE
+#define CF_AVAILABLE(_mac, _ios)
+#undef CF_ENUM_AVAILABLE
+#define CF_ENUM_AVAILABLE(_mac, _ios)
+#endif
+
 #else
 #define CF_AVAILABLE(_mac, _ios)
+#define CF_ENUM_AVAILABLE(_mac, _ios)
 #endif
 
 #endif /* __WebKitAvailability__ */

```