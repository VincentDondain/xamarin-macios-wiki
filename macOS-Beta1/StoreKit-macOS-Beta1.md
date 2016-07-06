#StoreKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKDownload.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKDownload.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKDownload.h	2015-08-23 03:45:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKDownload.h	2016-05-21 08:04:35.000000000 +0200
@@ -10,7 +10,9 @@
 
 @class SKPaymentTransaction;
 
-typedef enum : NSInteger
+NS_ASSUME_NONNULL_BEGIN
+
+typedef NS_ENUM(NSInteger, SKDownloadState)
 {
 	SKDownloadStateWaiting,
 	SKDownloadStateActive,
@@ -18,50 +20,50 @@
 	SKDownloadStateFinished,
 	SKDownloadStateFailed,
 	SKDownloadStateCancelled
-}
-SKDownloadState;
+} NS_AVAILABLE_MAC(10_8);
 
 
 // Model class to define a download for a particular product
-NS_CLASS_AVAILABLE(10_8, NA) 
-NS_ASSUME_NONNULL_BEGIN
-@interface SKDownload : NSObject {
+SK_EXTERN_CLASS_AVAILABLE(10_8)
+@interface SKDownload : NSObject
+{
 @private
     id _internal;
 }
 
 // Product identifier entered in iTunesConnect
-@property(readonly) NSString *contentIdentifier;
+@property(nonatomic, readonly) NSString *contentIdentifier NS_AVAILABLE_MAC(10_8);
 
 // Download state
-@property(readonly) SKDownloadState state;
+@property(nonatomic, readonly) SKDownloadState state NS_AVAILABLE_MAC(10_8);
 
 // Content URL
-@property(nullable, copy, readonly) NSURL *contentURL;
+@property(nonatomic, readonly, nullable) NSURL *contentURL NS_AVAILABLE_MAC(10_8);
 
 // Download progress 
-@property(readonly) float progress;
+@property(nonatomic, readonly) float progress NS_AVAILABLE_MAC(10_8);
 
 // Last error, can be NULL
-@property(nullable, copy, readonly) NSError *error;
+@property(nonatomic, copy, readonly, nullable) NSError *error NS_AVAILABLE_MAC(10_8);
 
 // Estimated number of seconds remaining in the download
-@property(readonly) NSTimeInterval timeRemaining;
+@property(nonatomic, readonly) NSTimeInterval timeRemaining NS_AVAILABLE_MAC(10_8);
 
 // Filesize of the asset
-@property(copy, readonly) NSNumber *contentLength;
+@property(nonatomic, copy, readonly) NSNumber *contentLength NS_AVAILABLE_MAC(10_8);
 
 // Version string of the product
-@property(nullable, copy, readonly) NSString* contentVersion;
+@property(nonatomic, copy, readonly) NSString *contentVersion NS_AVAILABLE_MAC(10_8);
 
 // The transaction associated with the downloadable file
-@property(nullable, nonatomic, readonly) SKPaymentTransaction *transaction;
+@property(nonatomic, readonly) SKPaymentTransaction *transaction NS_AVAILABLE_MAC(10_11);
 
 //
-+ (nullable NSURL *) contentURLForProductID:(NSString *)productID;
++ (nullable NSURL *) contentURLForProductID:(NSString *)productID NS_AVAILABLE_MAC(10_8);
 
 // Deletes the content for that identifier from disk
-+ (void) deleteContentForProductID:(NSString *)productID;
++ (void) deleteContentForProductID:(NSString *)productID NS_AVAILABLE_MAC(10_8);
 
 @end
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKError.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKError.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKError.h	2015-08-23 03:45:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKError.h	2016-05-21 08:04:35.000000000 +0200
@@ -9,11 +9,12 @@
 #import <StoreKit/StoreKitDefines.h>
 
 
+NS_ASSUME_NONNULL_BEGIN
 
-extern NSString * const SKErrorDomain NS_AVAILABLE(10_7, NA);
+SK_EXTERN NSString * const SKErrorDomain NS_AVAILABLE_MAC(10_7);
 
 // error codes for the SKErrorDomain
-enum {
+typedef NS_ENUM(NSInteger, SKErrorCode) {
     SKErrorUnknown,
     SKErrorClientInvalid,       // client is not allowed to issue the request, etc.
     SKErrorPaymentCancelled,    // user cancelled the request, etc.
@@ -21,3 +22,4 @@
     SKErrorPaymentNotAllowed    // this machine is not allowed to make the payment
 };
 
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKPayment.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKPayment.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKPayment.h	2015-08-23 03:45:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKPayment.h	2016-05-21 08:04:35.000000000 +0200
@@ -10,42 +10,41 @@
 
 @class SKProduct;
 
-//Model class to define a payment for a particular product
-NS_CLASS_AVAILABLE(10_7, NA) 
 NS_ASSUME_NONNULL_BEGIN
-@interface SKPayment : NSObject <NSCopying, NSMutableCopying> {
-@private
+
+//Model class to define a payment for a particular product
+SK_EXTERN_CLASS_AVAILABLE(10_7)
+@interface SKPayment : NSObject <NSCopying, NSMutableCopying>
+{
+@protected
     id _internal;
 }
 
-+ (id)paymentWithProduct:(SKProduct *)product;
++ (instancetype)paymentWithProduct:(SKProduct *)product NS_AVAILABLE_MAC(10_7);
 
 // Identifier agreed upon with the store.  Required.
-@property(copy, readonly) NSString *productIdentifier;
+@property(nonatomic, copy, readonly) NSString *productIdentifier NS_AVAILABLE_MAC(10_7);
 
 // Payment request data agreed upon with the store.  Optional.
-@property(nullable, copy, readonly) NSData *requestData;
+@property(nonatomic, copy, readonly, nullable) NSData *requestData NS_AVAILABLE_MAC(10_7);
 
 // default: 1.  Must be at least 1.
-@property(readonly) NSInteger quantity;
+@property(nonatomic, readonly) NSInteger quantity NS_AVAILABLE_MAC(10_7);
 
 // Application-specific user identifier.  Optional.
-@property(nullable, nonatomic, copy, readonly) NSString *applicationUsername;
+@property(nonatomic, copy, readonly, nullable) NSString *applicationUsername NS_AVAILABLE_MAC(10_9);
 
 @end
-NS_ASSUME_NONNULL_END
 
 
-NS_CLASS_AVAILABLE(10_7, NA)
-NS_ASSUME_NONNULL_BEGIN
-@interface SKMutablePayment : SKPayment {
-}
+SK_EXTERN_CLASS_AVAILABLE(10_7)
+@interface SKMutablePayment : SKPayment
 
-@property(copy, readwrite) NSString *productIdentifier;
-@property(readwrite) NSInteger quantity;
-@property(nullable, copy, readwrite) NSData *requestData;
-@property(nullable, nonatomic, copy, readwrite) NSString *applicationUsername;
+@property(nonatomic, copy) NSString *productIdentifier NS_AVAILABLE_MAC(10_7);
+@property(nonatomic) NSInteger quantity NS_AVAILABLE_MAC(10_7);
+@property(nonatomic, copy, nullable) NSData *requestData NS_AVAILABLE_MAC(10_7);
+@property(nonatomic, copy, nullable) NSString *applicationUsername NS_AVAILABLE_MAC(10_9);
 
 @end
-NS_ASSUME_NONNULL_END
 
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKPaymentQueue.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKPaymentQueue.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKPaymentQueue.h	2015-08-23 03:45:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKPaymentQueue.h	2016-05-21 08:04:35.000000000 +0200
@@ -8,72 +8,71 @@
 #import <Foundation/Foundation.h>
 #import <StoreKit/StoreKitDefines.h>
 
-
-
-@class SKPayment, SKPaymentTransaction, SKDownload;
+@class SKDownload;
+@class SKPayment;
+@class SKPaymentTransaction;
 @protocol SKPaymentTransactionObserver;
 
-// SKPaymentQueue interacts with the server-side payment queue
-NS_CLASS_AVAILABLE(10_7, NA)
 NS_ASSUME_NONNULL_BEGIN
+
+// SKPaymentQueue interacts with the server-side payment queue
+SK_EXTERN_CLASS_AVAILABLE(10_7)
 @interface SKPaymentQueue : NSObject
 {
-	@private
-		id _internal;
+@private
+    id _internal;
 }
 
-+ (SKPaymentQueue *) defaultQueue;
++ (instancetype) defaultQueue NS_AVAILABLE_MAC(10_7);
 
 // NO if this device is not able or allowed to make payments
-+ (BOOL) canMakePayments;
++ (BOOL) canMakePayments NS_AVAILABLE_MAC(10_7);
 
 // Asynchronous.  Add a payment to the server queue.  The payment is copied to add an SKPaymentTransaction to the transactions array.  The same payment can be added multiple times to create multiple transactions.
-- (void) addPayment:(SKPayment *)payment;
+- (void) addPayment:(SKPayment *)payment NS_AVAILABLE_MAC(10_7);
 
 // Asynchronous.  Will add completed transactions for the current user back to the queue to be re-completed.  User will be asked to authenticate.  Observers will receive 0 or more -paymentQueue:updatedTransactions:, followed by either -paymentQueueRestoreCompletedTransactionsFinished: on success or -paymentQueue:restoreCompletedTransactionsFailedWithError: on failure.  In the case of partial success, some transactions may still be delivered.
-- (void) restoreCompletedTransactions;
-- (void) restoreCompletedTransactionsWithApplicationUsername:(nullable NSString *)username;
+- (void) restoreCompletedTransactions NS_AVAILABLE_MAC(10_7);
+- (void) restoreCompletedTransactionsWithApplicationUsername:(nullable NSString *)username NS_AVAILABLE_MAC(10_9);
 
 // Asynchronous.  Remove a finished (i.e. failed or completed) transaction from the queue.  Attempting to finish a purchasing transaction will throw an exception.
-- (void) finishTransaction:(SKPaymentTransaction *)transaction;
+- (void) finishTransaction:(SKPaymentTransaction *)transaction NS_AVAILABLE_MAC(10_7);
 
 // Observers are not retained.  The transactions array will only be synchronized with the server while the queue has observers.  This may require that the user authenticate.
-- (void) addTransactionObserver:(id <SKPaymentTransactionObserver>)observer;
-- (void) removeTransactionObserver:(id <SKPaymentTransactionObserver>)observer;
+- (void) addTransactionObserver:(id <SKPaymentTransactionObserver>)observer NS_AVAILABLE_MAC(10_7);
+- (void) removeTransactionObserver:(id <SKPaymentTransactionObserver>)observer NS_AVAILABLE_MAC(10_7);
 
 // Array of unfinished SKPaymentTransactions.  Only valid while the queue has observers.  Updated asynchronously.
-@property(nullable, readonly) NSArray<SKPaymentTransaction *> *transactions;
+@property(nonatomic, readonly) NSArray<SKPaymentTransaction *> *transactions NS_AVAILABLE_MAC(10_7);
 
 //
-- (void) startDownloads:(NSArray <SKDownload *> *)downloads;
-- (void) pauseDownloads:(NSArray <SKDownload *> *)downloads;
-- (void) resumeDownloads:(NSArray <SKDownload *> *)downloads;
-- (void) cancelDownloads:(NSArray <SKDownload *> *)downloads;
+- (void) startDownloads:(NSArray <SKDownload *> *)downloads NS_AVAILABLE_MAC(10_8);
+- (void) pauseDownloads:(NSArray <SKDownload *> *)downloads NS_AVAILABLE_MAC(10_8);
+- (void) resumeDownloads:(NSArray <SKDownload *> *)downloads NS_AVAILABLE_MAC(10_8);
+- (void) cancelDownloads:(NSArray <SKDownload *> *)downloads NS_AVAILABLE_MAC(10_8);
 
 @end
-NS_ASSUME_NONNULL_END
 
 
-NS_ASSUME_NONNULL_BEGIN
 @protocol SKPaymentTransactionObserver <NSObject>
 @required
 // Sent when the transaction array has changed (additions or state changes).  Client should check state of transactions and finish as appropriate.
-- (void) paymentQueue:(SKPaymentQueue *)queue updatedTransactions:(NSArray <SKPaymentTransaction *> *)transactions;
+- (void) paymentQueue:(SKPaymentQueue *)queue updatedTransactions:(NSArray <SKPaymentTransaction *> *)transactions NS_AVAILABLE_MAC(10_7);
 
 @optional
 // Sent when transactions are removed from the queue (via finishTransaction:).
-- (void) paymentQueue:(SKPaymentQueue *)queue removedTransactions:(NSArray <SKPaymentTransaction *> *)transactions;
+- (void) paymentQueue:(SKPaymentQueue *)queue removedTransactions:(NSArray <SKPaymentTransaction *> *)transactions NS_AVAILABLE_MAC(10_7);
 
 // Sent when an error is encountered while adding transactions from the user's purchase history back to the queue.
-- (void) paymentQueue:(SKPaymentQueue *)queue restoreCompletedTransactionsFailedWithError:(NSError *)error;
+- (void) paymentQueue:(SKPaymentQueue *)queue restoreCompletedTransactionsFailedWithError:(NSError *)error NS_AVAILABLE_MAC(10_7);
 
 // Sent when all transactions from the user's purchase history have successfully been added back to the queue.
-- (void) paymentQueueRestoreCompletedTransactionsFinished:(SKPaymentQueue *)queue;
+- (void) paymentQueueRestoreCompletedTransactionsFinished:(SKPaymentQueue *)queue NS_AVAILABLE_MAC(10_7);
 
 // Sent when the download state has changed.
-- (void) paymentQueue:(SKPaymentQueue *)queue updatedDownloads:(NSArray <SKDownload *> *)downloads;
+- (void) paymentQueue:(SKPaymentQueue *)queue updatedDownloads:(NSArray <SKDownload *> *)downloads NS_AVAILABLE_MAC(10_8);
 
 @end
-NS_ASSUME_NONNULL_END
 
+NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKPaymentTransaction.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKPaymentTransaction.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKPaymentTransaction.h	2015-08-23 03:45:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKPaymentTransaction.h	2016-05-21 08:04:35.000000000 +0200
@@ -9,43 +9,45 @@
 #import <StoreKit/StoreKitDefines.h>
 
 @class SKPayment;
+@class SKDownload;
 
-enum {
-    SKPaymentTransactionStatePurchasing,    // Transaction is being added to the server queue.
-    SKPaymentTransactionStatePurchased,     // Transaction is in queue, user has been charged.  Client should complete the transaction.
-    SKPaymentTransactionStateFailed,        // Transaction was cancelled or failed before being added to the server queue.
-    SKPaymentTransactionStateRestored,      // Transaction was restored from user's purchase history.  Client should complete the transaction.
-    SKPaymentTransactionStateDeferred,		// Transaction is neither purchased nor failed, yet.
-};
-typedef NSInteger SKPaymentTransactionState;
+typedef NS_ENUM(NSInteger, SKPaymentTransactionState) {
+    SKPaymentTransactionStatePurchasing,                                // Transaction is being added to the server queue.
+    SKPaymentTransactionStatePurchased,                                 // Transaction is in queue, user has been charged.  Client should complete the transaction.
+    SKPaymentTransactionStateFailed,                                    // Transaction was cancelled or failed before being added to the server queue.
+    SKPaymentTransactionStateRestored,                                  // Transaction was restored from user's purchase history.  Client should complete the transaction.
+    SKPaymentTransactionStateDeferred NS_ENUM_AVAILABLE_MAC(10_10),     // Transaction is neither purchased nor failed, yet.
+} NS_AVAILABLE_MAC(10_7);
 
-// Model object representing a transaction with the server
-NS_CLASS_AVAILABLE(10_7, NA)
 NS_ASSUME_NONNULL_BEGIN
-@interface SKPaymentTransaction : NSObject {
+
+// Model object representing a transaction with the server
+SK_EXTERN_CLASS_AVAILABLE(10_7)
+@interface SKPaymentTransaction : NSObject
+{
 @private
     id _internal;
 }
 
-// Only set if state is SKPaymentTransactionFailed
-@property(nullable, readonly) NSError *error;
+// Only set if state is SKPaymentTransactionStateFailed
+@property(nonatomic, readonly, nullable) NSError *error NS_AVAILABLE_MAC(10_7);
 
 // Only valid if state is SKPaymentTransactionStateRestored.
-@property(nullable, readonly) SKPaymentTransaction *originalTransaction;
+@property(nonatomic, readonly, nullable) SKPaymentTransaction *originalTransaction NS_AVAILABLE_MAC(10_7);
 
-@property(readonly) SKPayment *payment;
+@property(nonatomic, readonly) SKPayment *payment NS_AVAILABLE_MAC(10_7);
 
 // The date when the transaction was added to the server queue.  Only valid if state is SKPaymentTransactionStatePurchased or SKPaymentTransactionStateRestored.
-@property(nullable, readonly) NSDate *transactionDate;
+@property(nonatomic, readonly, nullable) NSDate *transactionDate NS_AVAILABLE_MAC(10_7);
 
 // The unique server-provided identifier.  Only valid if state is SKPaymentTransactionStatePurchased or SKPaymentTransactionStateRestored.
-@property(nullable, readonly) NSString *transactionIdentifier;
+@property(nonatomic, readonly, nullable) NSString *transactionIdentifier NS_AVAILABLE_MAC(10_7);
 
 // Array of SKDownload objects
 // Only valid if state is SKPaymentTransactionStatePurchased or SKPaymentTransactionStateRestored.
-@property(nullable, readonly) NSArray *downloads;
+@property(nonatomic, readonly) NSArray<SKDownload *> *downloads NS_AVAILABLE_MAC(10_8);
 
-@property(readonly) SKPaymentTransactionState transactionState;
+@property(nonatomic, readonly) SKPaymentTransactionState transactionState NS_AVAILABLE_MAC(10_7);
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKProduct.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKProduct.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKProduct.h	2015-08-23 03:45:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKProduct.h	2016-05-21 08:04:35.000000000 +0200
@@ -8,29 +8,34 @@
 #import <Foundation/Foundation.h>
 #import <StoreKit/StoreKitDefines.h>
 
-NS_CLASS_AVAILABLE(10_7, NA)
-@interface SKProduct : NSObject {
+NS_ASSUME_NONNULL_BEGIN
+
+SK_EXTERN_CLASS_AVAILABLE(10_7)
+@interface SKProduct : NSObject
+{
 @private
     id _internal;
 }
 
-@property(nullable, readonly) NSString *localizedDescription;
+@property(nonatomic, readonly) NSString *localizedDescription NS_AVAILABLE_MAC(10_7);
 
-@property(nullable, readonly) NSString *localizedTitle;
+@property(nonatomic, readonly) NSString *localizedTitle NS_AVAILABLE_MAC(10_7);
 
-@property(nullable, readonly) NSDecimalNumber *price;
+@property(nonatomic, readonly) NSDecimalNumber *price NS_AVAILABLE_MAC(10_7);
 
-@property(nullable, readonly) NSLocale *priceLocale;
+@property(nonatomic, readonly) NSLocale *priceLocale NS_AVAILABLE_MAC(10_7);
 
-@property(nullable, readonly) NSString *productIdentifier;
+@property(nonatomic, readonly) NSString *productIdentifier NS_AVAILABLE_MAC(10_7);
 
 // YES if the product's assets are hosted by the App Store. NO otherwise. 
-@property(readonly) BOOL downloadable;
+@property(nonatomic, readonly) BOOL downloadable NS_AVAILABLE_MAC(10_8);
 
 // Version string of the product
-@property(nullable, readonly) NSString* contentVersion;
+@property(nonatomic, readonly) NSString *contentVersion NS_AVAILABLE_MAC(10_8);
 
 // An array of filesizes of the assets associated with the product
-@property(nullable, readonly) NSArray<NSNumber *> *contentLengths;
+@property(nonatomic, readonly) NSArray<NSNumber *> *contentLengths NS_AVAILABLE_MAC(10_8);
 
 @end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKProductsRequest.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKProductsRequest.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKProductsRequest.h	2015-08-23 03:45:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKProductsRequest.h	2016-05-21 08:04:35.000000000 +0200
@@ -8,51 +8,48 @@
 #import <StoreKit/SKRequest.h>
 
 
-
 @class SKProductsRequest, SKProductsResponse, SKProduct;
 
 NS_ASSUME_NONNULL_BEGIN
+
 @protocol SKProductsRequestDelegate <SKRequestDelegate>
 
 @required
 // Sent immediately before -requestDidFinish:
-- (void)productsRequest:(SKProductsRequest *)request didReceiveResponse:(SKProductsResponse *)response;
+- (void)productsRequest:(SKProductsRequest *)request didReceiveResponse:(SKProductsResponse *)response NS_AVAILABLE_MAC(10_7);
 
 @end
-NS_ASSUME_NONNULL_END
 
 
 // request information about products for your application
-NS_CLASS_AVAILABLE(10_7, NA)
-NS_ASSUME_NONNULL_BEGIN
-@interface SKProductsRequest : SKRequest {
+SK_EXTERN_CLASS_AVAILABLE(10_7)
+@interface SKProductsRequest : SKRequest
+{
 @private
     id _productsRequestInternal;
 }
 
 // Set of string product identifiers
-- (id)initWithProductIdentifiers:(NSSet *)productIdentifiers;
+- (instancetype)initWithProductIdentifiers:(NSSet<NSString *> *)productIdentifiers NS_AVAILABLE_MAC(10_7);
 
-@property(nullable, assign) id <SKProductsRequestDelegate> delegate;
+@property(nonatomic, weak, nullable) id <SKProductsRequestDelegate> delegate NS_AVAILABLE_MAC(10_7);
 
 @end
-NS_ASSUME_NONNULL_END
 
 
-NS_CLASS_AVAILABLE(10_7, NA)
-NS_ASSUME_NONNULL_BEGIN
-@interface SKProductsResponse : NSObject {
+SK_EXTERN_CLASS_AVAILABLE(10_7)
+@interface SKProductsResponse : NSObject
+{
 @private
     id _internal;
 }
 
 // Array of SKProduct instances.
-@property(nullable, readonly) NSArray<SKProduct *> *products;
+@property(nonatomic, readonly) NSArray<SKProduct *> *products NS_AVAILABLE_MAC(10_7);
 
 // Array of invalid product identifiers.
-@property(nullable, readonly) NSArray<NSString *> *invalidProductIdentifiers;
+@property(nonatomic, readonly) NSArray<NSString *> *invalidProductIdentifiers NS_AVAILABLE_MAC(10_7);
 
 @end
-NS_ASSUME_NONNULL_END
-
 
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKReceiptRefreshRequest.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKReceiptRefreshRequest.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKReceiptRefreshRequest.h	2015-08-23 03:45:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKReceiptRefreshRequest.h	2016-05-21 08:04:35.000000000 +0200
@@ -9,20 +9,24 @@
 #import <StoreKit/SKRequest.h>
 #import <StoreKit/StoreKitDefines.h>
 
-NS_CLASS_AVAILABLE(10_9, NA)
 NS_ASSUME_NONNULL_BEGIN
+
+SK_EXTERN_CLASS_AVAILABLE(10_9)
 @interface SKReceiptRefreshRequest : SKRequest
 {
     NSDictionary *_properties;
 }
-- (nullable id)initWithReceiptProperties:(NSDictionary<NSString *, id> *)properties;
-@property (nullable, nonatomic, readonly) NSDictionary<NSString *, id> *receiptProperties;
+
+- (instancetype)initWithReceiptProperties:(nullable NSDictionary<NSString *, id> *)properties NS_AVAILABLE_MAC(10_9);
+
+@property (nonatomic, readonly, nullable) NSDictionary<NSString *, id> *receiptProperties NS_AVAILABLE_MAC(10_9);
 
 @end
 
 
 // Receipt properties for sandbox testing:
-SK_EXTERN NSString * const SKReceiptPropertyIsExpired;  // NSNumber BOOL, defaults to NO
-SK_EXTERN NSString * const SKReceiptPropertyIsRevoked;  // NSNumber BOOL, defaults to NO
-SK_EXTERN NSString * const SKReceiptPropertyIsVolumePurchase;  // NSNumber BOOL, defaults to NO
+SK_EXTERN NSString * const SKReceiptPropertyIsExpired  NS_AVAILABLE_MAC(10_9);  // NSNumber BOOL, defaults to NO
+SK_EXTERN NSString * const SKReceiptPropertyIsRevoked  NS_AVAILABLE_MAC(10_9);  // NSNumber BOOL, defaults to NO
+SK_EXTERN NSString * const SKReceiptPropertyIsVolumePurchase  NS_AVAILABLE_MAC(10_9);  // NSNumber BOOL, defaults to NO
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKRequest.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKRequest.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKRequest.h	2015-08-23 03:45:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKRequest.h	2016-05-21 08:04:35.000000000 +0200
@@ -8,37 +8,34 @@
 #import <Foundation/Foundation.h>
 #import <StoreKit/StoreKitDefines.h>
 
-
-
 NS_ASSUME_NONNULL_BEGIN
+
 @protocol SKRequestDelegate;
 
 // Base class used to fetch data from the store.  Should not be used directly.
-NS_CLASS_AVAILABLE(10_7, NA)
-@interface SKRequest : NSObject {
+SK_EXTERN_CLASS_AVAILABLE(10_7)
+@interface SKRequest : NSObject
+{
 @private
     id _requestInternal;
 }
 
-@property(nullable, assign) id <SKRequestDelegate> delegate;
+@property(nonatomic, weak, nullable) id <SKRequestDelegate> delegate NS_AVAILABLE_MAC(10_7);
 
 // Cancel the request if it has started.
-- (void)cancel;
+- (void)cancel NS_AVAILABLE_MAC(10_7);
 
 // Start the request if it has not already been started.
-- (void)start;
+- (void)start NS_AVAILABLE_MAC(10_7);
 
 @end
-NS_ASSUME_NONNULL_END
 
-NS_ASSUME_NONNULL_BEGIN
 @protocol SKRequestDelegate <NSObject>
 
 @optional
-- (void)requestDidFinish:(SKRequest *)request;
-- (void)request:(SKRequest *)request didFailWithError:(nullable NSError *)error;
+- (void)requestDidFinish:(SKRequest *)request NS_AVAILABLE_MAC(10_7);
+- (void)request:(SKRequest *)request didFailWithError:(NSError *)error NS_AVAILABLE_MAC(10_7);
 
 @end
-NS_ASSUME_NONNULL_END
-
 
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/StoreKit.framework/Headers/StoreKitDefines.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/StoreKit.framework/Headers/StoreKitDefines.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/StoreKit.framework/Headers/StoreKitDefines.h	2015-08-23 03:45:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/StoreKit.framework/Headers/StoreKitDefines.h	2016-05-21 08:04:35.000000000 +0200
@@ -5,7 +5,11 @@
 //  Copyright 2009 Apple, Inc. All rights reserved.
 //
 
-#define SK_EXTERN   extern __attribute__((visibility ("default"))) NS_AVAILABLE(10_7, NA)
-
-#define	SK_EXTERN_CLASS	__attribute__((visibility("default"))) NS_CLASS_AVAILABLE(10_7, NA) 
+#ifdef __cplusplus
+#define SK_EXTERN   extern "C" __attribute__((visibility ("default")))
+#else
+#define SK_EXTERN   extern __attribute__((visibility ("default")))
+#endif
 
+#define	SK_EXTERN_CLASS	__attribute__((visibility("default")))
+#define SK_EXTERN_CLASS_AVAILABLE(version) __attribute__((visibility("default"))) NS_CLASS_AVAILABLE_MAC(version)

```