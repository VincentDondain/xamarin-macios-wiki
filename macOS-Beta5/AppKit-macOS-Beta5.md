#AppKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDraggingSession.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDraggingSession.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDraggingSession.h	2016-07-27 05:10:07.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSDraggingSession.h	2016-08-06 05:42:10.000000000 +0200
 @protocol NSFilePromiseProviderDelegate <NSObject>
 @required
 /* Return the base filename (not a full path) for this promise item. Do not start writing the file yet. */
-- (NSString *)filePromiseProvider:(NSFilePromiseProvider*)filePromiseProvider fileNameForDestination:(NSURL *)destinationURL;
+- (NSString *)filePromiseProvider:(NSFilePromiseProvider*)filePromiseProvider fileNameForType:(NSString *)fileType;
 
-@optional
-/* Write the contents of this promise item to the provided URL and call completionHandler when done. NSFilePromiseReceiver automatically wraps this message with NSFileCoordinator when the promise destination is an NSFilePromiseReceiver. As such, the URL may be different than expected. Note: This request shall occur on the NSOperationQueue supplied by -promiseOperationQueue.
+
+/* Write the contents of this promise item to the provided URL and call completionHandler when done. NSFilePromiseReceiver automatically wraps this message with NSFileCoordinator when the promise destination is an NSFilePromiseReceiver. Always use the supplied URL. Note: This request shall occur on the NSOperationQueue supplied by -promiseOperationQueue.
  */
 - (void)filePromiseProvider:(NSFilePromiseProvider*)filePromiseProvider writePromiseToURL:(NSURL *)url completionHandler:(void (^)(NSError * __nullable errorOrNil))completionHandler;
 
+@optional
 /* The operation queue that the write request will be issued from. If this method is not implemented, the mainOperationQueue is used. */
-- (NSOperationQueue *)promiseOperationQueueForFilePromiseProvider:(NSFilePromiseProvider*)filePromiseProvider;
+- (NSOperationQueue *)operationQueueForFilePromiseProvider:(NSFilePromiseProvider*)filePromiseProvider;
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFilePromiseReceiver.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFilePromiseReceiver.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFilePromiseReceiver.h	2016-07-27 05:10:07.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSFilePromiseReceiver.h	2016-08-06 05:42:10.000000000 +0200
@@ -53,7 +53,7 @@
  This is an array, because legacy promises are an array of files on one pasteboard item.
  The reader block is called on the supplied operationQueue when the promised file is ready to be read. When the source is an NSFilePromiseProvider, the readerBlock call is wrapped in an NSFileCoordination read. Otherwise, a heuristic is used to determine when the promised file is ready to be read.
  The options dictionary is ignored for now.
- Note: Writing of the promised file may fail. When that occurs, the readerBlock is still called, but there may be nothing at the fileURL, or it may be a partial / corrupt file.
+ Note: Writing of the promised file may be cancelled or fail. When either occurs, the readerBlock is still called, but with a non-nil NSError. When NSError is non-nil, fileURL should be ignored.
  */
 - (void)receivePromisedFilesAtDestination:(NSURL *)destinationDir options:(NSDictionary *)options operationQueue:(NSOperationQueue *)operationQueue reader:(void(^)(NSURL *fileURL, NSError * __nullable errorOrNil))reader;
 @end
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPasteboard.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPasteboard.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPasteboard.h	2016-07-27 05:10:07.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSPasteboard.h	2016-08-06 05:42:10.000000000 +0200
@@ -43,6 +43,12 @@
 APPKIT_EXTERN NSString *NSFindPboard;
 APPKIT_EXTERN NSString *NSDragPboard;
 
+/* Options for prepareForNewContentsWithOptions: */
+
+typedef NS_OPTIONS(NSUInteger, NSPasteboardContentsOptions) {
+    NSPasteboardContentsCurrentHostOnly = 1 << 0, // Specifies that the pasteboard contents should not be available to other devices
+} NS_ENUM_AVAILABLE_MAC(10_12);
+
 
 /* An NSPasteboard can contain multiple items.  Any object that implements the NSPasteboardWriting and NSPasteboardReading protocols can be written and read on the pasteboard directly.  This allows common pasteboard classes such as URLs, colors, images, strings, attributed strings, and sounds to be written and read without an intermediary object.  The custom classes of an application can also implement these protocols for use with the pasteboard.
 */
@@ -74,8 +80,11 @@
 
 - (oneway void)releaseGlobally;
 
+/* Prepares the pasteboard for new contents, clearing the existing contents of the pasteboard. This is the first step in providing data on the pasteboard. Any options specified will persist until prepareForNewContentsWithOptions: or clearContents is called. Returns the change count of the pasteboard.
+ */
+- (NSInteger)prepareForNewContentsWithOptions:(NSPasteboardContentsOptions)options NS_SWIFT_NAME(prepareForNewContents(with:)) NS_AVAILABLE_MAC(10_12);
 
-/* Clears the existing contents of the pasteboard, preparing it for new contents.  This is the first step in providing data on the pasteboard.  Returns the change count of the pasteboard.
+/* Prepares the pasteboard for new contents, clearing the existing contents of the pasteboard.  This is equivalent to calling prepareForNewContentsWithOptions: with no options.  Returns the change count of the pasteboard.
 */
 - (NSInteger)clearContents NS_AVAILABLE_MAC(10_6);
 
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindow.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindow.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindow.h	2016-07-27 05:10:07.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AppKit.framework/Headers/NSWindow.h	2016-08-06 05:42:10.000000000 +0200
@@ -233,7 +233,7 @@
         unsigned int  haveFreeCursorRects:1;
         unsigned int  validCursorRects:1;
         unsigned int  docEdited:1;
-        unsigned int  dynamicDepthLimit:1;
+        unsigned int  staticDepthLimit:1;
         unsigned int  worksWhenModal:1;
         unsigned int  limitedBecomeKey:1;
         unsigned int  needsFlush:1;

```