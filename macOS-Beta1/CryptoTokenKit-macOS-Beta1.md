#CryptoTokenKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/CryptoTokenKit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/CryptoTokenKit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/CryptoTokenKit.h	2015-08-23 02:44:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/CryptoTokenKit.h	2016-06-03 23:16:34.000000000 +0200
@@ -4,6 +4,14 @@
 //
 
 #import <CryptoTokenKit/TKError.h>
+#import <CryptoTokenKit/TKTLVRecord.h>
+
+#import <CryptoTokenKit/TKToken.h>
+#import <CryptoTokenKit/TKTokenKeychainItem.h>
+#import <CryptoTokenKit/TKSmartCardToken.h>
+
+#import <CryptoTokenKit/TKTokenWatcher.h>
+
 #import <CryptoTokenKit/TKSmartCard.h>
+#import <CryptoTokenKit/TKSmartCardToken.h>
 #import <CryptoTokenKit/TKSmartCardATR.h>
-
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKError.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKError.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKError.h	2015-08-23 02:44:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKError.h	2016-06-03 23:16:34.000000000 +0200
@@ -18,6 +18,7 @@
     TKErrorCodeObjectNotFound        = -6,
     TKErrorCodeTokenNotFound         = -7,
     TKErrorCodeBadParameter          = -8,
+    TKErrorCodeAuthenticationNeeded  = -9,
 
     TKErrorAuthenticationFailed NS_ENUM_DEPRECATED(10_10, 10_11, 9_0, 9_0, "Use TKErrorCodeAuthenticationFailed")
       = TKErrorCodeAuthenticationFailed,
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKSmartCard.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKSmartCard.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKSmartCard.h	2015-10-24 02:24:07.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKSmartCard.h	2016-06-03 23:16:34.000000000 +0200
@@ -333,26 +333,55 @@
 
 @end
 
+/// Extension of base TKSmartCard interface implementing ISO7816-3 and ISO7816-4 structured APDU transmission.
 @interface TKSmartCard (APDULevelTransmit)
 
 /// CLA byte which will be used for sendIns: APDU transmits.  Default value is 0x00.
-@property UInt8 cla;
+@property UInt8 cla
+__OSX_AVAILABLE(10.10) __IOS_AVAILABLE(9.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE;
 
-/// Flag indicating whether extended length APDUs should be used. It is automatically enabled only when used slot supports transmitting extended length commands and card announces that extended length APDU are supported in its ATR. However, caller can explicitely override this decision at its will.
-@property BOOL useExtendedLength;
+/// Flag indicating whether extended length APDUs should be used. It is automatically enabled only when used slot supports transmitting extended length commands and card announces that extended length APDU are supported in its ATR. However, caller can explicitly override this decision.
+@property BOOL useExtendedLength
+__OSX_AVAILABLE(10.10) __IOS_AVAILABLE(9.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE;
+
+/// Flag indicating whether command chaining of APDU with data field longer than 255 bytes can be used.  It is automatically enabled when card announces that command chaining is supported in its ATR.  However, caller can explicitly override this decision.
+@property BOOL useCommandChaining
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE;
 
 /// Transmits APDU to the card and returns response.
-/// @discussion Asynchronous high level variant of command for transmitting APDU to the card.  Handles all ISO7816-4 APDU cases translation to proper sequences according to used protocol.  If useExtendedLength is enabled and it is decided that it is beneficial for current set of arguments, extended APDUs are used automatically.
+/// @discussion Asynchronous high level variant of command for transmitting APDU to the card.  Handles all ISO7816-4 APDU cases translation to proper sequences according to used protocol.  Consults useExtendedAPDU and useCommandChaining properties and uses these modes whenever appropriate and beneficial for sending requested APDU request.
 /// @param ins INS code of the APDU
 /// @param p1 P1 code of the APDU
 /// @param p2 P2 code of the APDU
 /// @param requestData Data field of the APDU, or nil if no input data field should be present (i.e case1 or case2 APDUs).  Length of the data serves as Lc field of the APDU.
 /// @param le Expected number of bytes to be returned, or nil if no output data are expected (i.e. case1 or case3 APDUs). To get as much bytes as card provides, pass @0.
 /// @param replyData Block of returned data without SW1SW2 bytes, or nil if an error occured.
-/// @param sw SW1SW2 result code
+/// @param sw SW1SW2 result code, first two bytes of returned card's reply.
 /// @param error Contains error details when nil is returned.  Specific error is also filled in if there was no communication error, but card returned other SW code than 0x9000.
 - (void)sendIns:(UInt8)ins p1:(UInt8)p1 p2:(UInt8)p2 data:(nullable NSData *)requestData le:(nullable NSNumber *)le
-          reply:(void(^)(NSData *__nullable replyData, UInt16 sw, NSError *__nullable error))reply;
+          reply:(void(^)(NSData *__nullable replyData, UInt16 sw, NSError *__nullable error))reply
+__OSX_AVAILABLE(10.10) __IOS_AVAILABLE(9.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE;
+
+/// Synchronous variant of session creation.  Begins the session, executes given block and ends session.
+/// @param error Error receiving more information when transaction failed to start or block failed for some reason.
+/// @param block Block to be executed when the session was successfully begun.
+/// @return Returns YES if the session was successfully begun and block returned YES, otherwise NO.
+- (BOOL)inSessionWithError:(NSError **)error executeBlock:(BOOL(^)(NSError **error))block
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE;
+
+/// Transmits APDU to the card and returns response.
+/// @discussion Synchronous high level variant of command for transmitting APDU to the card.  Handles all ISO7816-4 APDU cases translation to proper sequences according to used protocol.  Should be used in block passed to -[TKSmartCard inSessionWithError:executeBlock:] method.
+/// @param ins INS code of the APDU
+/// @param p1 P1 code of the APDU
+/// @param p2 P2 code of the APDU
+/// @param data Data field of the APDU.  Length of the data serves as Lc field of the APDU
+/// @param le Expected number of bytes to be returned, or nil if no output data are expected (i.e. case1 or case3 APDUs). To get as much bytes as card provides, pass @0.
+/// @param sw On output, filled with SW1SW2 result code
+/// @param error Contains error details when nil is returned.  Specific error is also filled in if there was no communication error, but card returned other SW code than 0x9000.
+/// @return Returned data field, excluding SW status bytes.  If an error occured, returns nil.
+- (nullable NSData *)sendIns:(UInt8)ins p1:(UInt8)p1 p2:(UInt8)p2 data:(nullable NSData *)requestData
+                          le:(nullable NSNumber *)le sw:(UInt16 *)sw error:(NSError **)error
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKSmartCardATR.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKSmartCardATR.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKSmartCardATR.h	2015-08-23 02:44:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKSmartCardATR.h	2016-06-03 23:16:34.000000000 +0200
@@ -5,6 +5,8 @@
 
 #import <Foundation/Foundation.h>
 
+#import "TKTLVRecord.h"
+
 NS_ASSUME_NONNULL_BEGIN
 
 /// Bitmask of available smartcard protocols.
@@ -66,6 +68,14 @@
 /// Just historical bytes of ATR, without Tck and interface bytes.
 @property (nonatomic, readonly) NSData *historicalBytes;
 
+/// An array of TKCompactTLVRecord instances with TLV records parsed from historical bytes.  If historical bytes are
+/// not structured using Compact TLV encoding, nil is returned.
+/// @note In case that ATR historical bytes begin with 0x00, the last three bytes (status indicator) are automatically
+///       appended into the returned records as if historical bytes would begin with 0x80 and 0x8 record is present
+///       in historical bytes.
+@property (nonatomic, readonly, nullable) NSArray<TKCompactTLVRecord *> *historicalRecords
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE;
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKSmartCardToken.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKSmartCardToken.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKSmartCardToken.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKSmartCardToken.h	2016-06-03 23:16:34.000000000 +0200
@@ -0,0 +1,116 @@
+//
+//  TKSmartCardToken.h
+//  Copyright (c) 2015 Apple. All rights reserved.
+//
+
+#import <CryptoTokenKit/TKToken.h>
+#import <CryptoTokenKit/TKSmartCard.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class TKSmartCardTokenSession;
+@class TKSmartCardToken;
+@protocol TKSmartCardTokenDriverDelegate;
+@class TKSmartCardTokenDriver;
+
+/*!
+ @discussion Context of a SmartCard PIN authentication operation.
+ */
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@interface TKTokenSmartCardPINAuthOperation : TKTokenAuthOperation
+
+/*!
+ @discussion PIN formatting properties.
+ @note The property is initialized with a default instance of TKSmartCardPINFormat.
+ */
+@property TKSmartCardPINFormat *PINFormat;
+
+/*!
+ @discussion APDU template into which PIN gets filled in. If set to nil, the system will not attempt to authenticate by sending the formatted APDU to the SmartCard, but rather the token itself is expected to perform the authentication.  It is preferred to provide APDUTemplate if possible, because it allows using hardware PINPad for secure PIN entry (provided that the reader has one).
+ */
+@property (nullable, copy) NSData *APDUTemplate;
+
+/*!
+ @discussion Offset in bytes within APDU template to mark the location for filling in the PIN.
+ */
+@property NSInteger PINByteOffset;
+
+/*!
+ @discussion TKSmartCard to which the formatted APDU gets sent in order to authenticate (used only if 'APDUTemplate' is set).
+ */
+@property (nullable) TKSmartCard *smartCard;
+
+/*!
+ @discussion PIN value which will be set when 'finishWithError:' gets triggered.  Note that the PIN is not set in case that APDUTemplate was set.  In this case, PIN was already sent to the card using specified template.
+ */
+@property (nullable, copy) NSString *PIN;
+
+@end
+
+/*!
+ @abstract TKSmartCardTokenSession represents token session based on smart card token.
+ @discussion When implementing Smart Card token extension, subclass TKSmartCardTokenSession and implement TKTokenSessionDelegate on it.  Use #token property to get access and send APDUs to the underlying smart card.
+ */
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@interface TKSmartCardTokenSession : TKTokenSession
+
+/*!
+ @abstract contains TKSmartCard instance with active exclusive session and smart card application selected.
+ @discussion This property can be accessed only when handling one of the methods of TKTokenSessionDelegate protocol.  If associated token has set AID property, then the returned card has opened exclusive session to the card and the application is already selected.  Therefore there is no need to call -[TKSmartCard beginSessionWithReply:]) on returned smart card instance in such case and system will take care of terminating session when current token request servicing is finished,  -[TKSmartCard endSession] must not be called either.
+
+ You can store any kind of context state information representing state of the card into smartCard.context property.  This property will be automatically set to nil if the card is reset or accessed by different TKSmartCard instance (possibly in another process).  Checking TKSmartCard.context property for previously stored value can be used to avoid potentially costly restoring of smart card state before performing the operation.
+ */
+@property (readonly) TKSmartCard *smartCard;
+
+@end
+
+/*!
+ @abstract TKSmartCardToken base class for implementing smart card based token.
+ @discussion When implementing Smart Card token extension, subclass TKSmartCardToken and implement TKTokenDelegate on it.
+ */
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@interface TKSmartCardToken : TKToken
+
+/*!
+ @discussion Initializes token instance with specified attributes.
+ @param smartCard TKSmartCard instance representing connection to smart card on which the intance should operate.
+ @param AID ISO7816-4 application ID which is preselected on the card.
+ @param instanceID Unique, persistent identifier of this token.  This is typically implemented by some kind of smart card serial number.
+ @param tokenDriver associated driver which initiated creation of this token.
+ */
+- (instancetype)initWithSmartCard:(TKSmartCard *)smartCard AID:(nullable NSData *)AID instanceID:(NSString *)instanceID tokenDriver:(TKSmartCardTokenDriver *)tokenDriver NS_DESIGNATED_INITIALIZER;
+
+/*!
+ @discussion This is AID which is specified in extension's plist NSExtensionAttributes as @c com.apple.ctk.aid attribute. If the attribute specifies array of multiple AIDs, this parameter represents AID which was found on the card and is already preselected.  If @c com.apple.ctk.aid is not present, no application is automatically preselected and value of this property is nil.
+ */
+@property (readonly, nullable) NSData *AID;
+
+- (instancetype)initWithTokenDriver:(TKTokenDriver *)tokenDriver instanceID:(NSString *)instanceID NS_UNAVAILABLE;
+
+@end
+
+/*!
+ @abstract TKSmartCardTokenDriver represents driver for specific smart card type.
+ */
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@interface TKSmartCardTokenDriver : TKTokenDriver
+
+@end
+
+/*!
+ @discussion TKSmartCardTokenDriverDelegate is used to implement creation of new token instance according to the smart card.
+ */
+@protocol TKSmartCardTokenDriverDelegate<TKTokenDriverDelegate>
+
+/*!
+ @discussion Called by system when new smart card is detected.  You must override this method to create a new valid token TKSmartCardToken instance for @c smartCard.
+ @param smartCard Target smart card.
+ @param AID ISO7816-4 AID (application ID) which is already selected on the card.  If @c com.apple.ctk.aid is not present, no application is selected and this parameter is nil.
+ @param error Error details if operation fails.
+ @return Newly created token instance representing @c smartCard.  If an error occurs or driver decides that it does not want to handle specified smartCard as token, return nil.
+ */
+- (nullable TKSmartCardToken *)tokenDriver:(TKSmartCardTokenDriver *)driver createTokenForSmartCard:(TKSmartCard *)smartCard AID:(nullable NSData *)AID error:(NSError **)error;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKTLVRecord.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKTLVRecord.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKTLVRecord.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKTLVRecord.h	2016-06-03 23:16:34.000000000 +0200
@@ -0,0 +1,99 @@
+//
+//  TKTLVRecord.h
+//  Copyright (c) 2013-2016 Apple. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+/// Type used for identifying TLV format tags.
+/// Although for some encodings tags can have theoretically any length,
+/// this implementation supports tag length only up to 64bits.
+typedef UInt64 TKTLVTag
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE;
+
+/// Base class representing Tag-Length-Value record.
+/// Every record has its tag and binary value represented as NSData instance.  Allows retrieving record's tag,
+/// value (as NSData object) and binary representation of the record. Existing subclasses implement assorted
+/// encodings - TKBERTLVRecord, TKSimpleTLVRecord and TKCompactTLVRecord.
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@interface TKTLVRecord : NSObject
+
+/// Tag value of the record.
+@property (nonatomic, readonly) TKTLVTag tag;
+
+/// Value field of the record.
+@property (nonatomic, readonly) NSData *value;
+
+/// Data object containing whole encoded record, including tag, length and value.
+@property (nonatomic, readonly) NSData *data;
+
+/// Parses TLV record from data block
+/// @param bytes Data block containing serialized form of TLV record.
+/// @return newly parsed record instance or nil if data do not represent valid record.
++ (nullable instancetype)recordFromData:(NSData *)data;
+
+/// Parses sequence of TLV records from data block.
+/// The amount of records is determined by the length of input data block.
+/// @param bytes Data block containing zero or more serialized forms of TLV record.
+/// @return An array of TLV record instances parsed from input data block or nil if data do not form valid TLV record sequence.
++ (nullable NSArray<TKTLVRecord *> *)sequenceOfRecordsFromData:(NSData *)data;
+
+- (instancetype)init NS_UNAVAILABLE;
+
+@end
+
+/// TKBERTLVRecord implements encoding using BER-TLV encoding rules.
+/// It is able to parse BER-encoded data and always produces DER-encoded data.
+/// No interpretation of tag values is made, all values are treated only as NSData irrespective of the tag.
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@interface TKBERTLVRecord : TKTLVRecord
+
+/// Encodes tag using BER-TLV tag encoding rules.
+/// @param tag Tag value to encode
+/// @return Binary block containing encoded tag value.
++ (NSData *)dataForTag:(TKTLVTag)tag;
+
+/// Creates TLV record with specified tag and value.
+/// @param tag Tag value for the new record.
+/// @param value Value for the new record.
+/// @return Newly created TLV record.
+- (instancetype)initWithTag:(TKTLVTag)tag value:(NSData *)value;
+
+/// Creates TKBERTLVRecord with specified tag and array of children TKTLVRecord instances as subrecords.
+/// @param tag Tag value for the new record.
+/// @param records Array of TKTLVRecord instances serving as subrecords of this record.
+/// @return Newly created TLV record.
+- (instancetype)initWithTag:(TKTLVTag)tag records:(NSArray<TKTLVRecord *> *)records;
+
+@end
+
+/// TKSimpleTLVRecord implements Simple-TLV encoding according to ISO7816-4.
+/// Tag is number in range <1..254> encoded as single byte, length is either single byte specifying length 0-254
+/// or 3 bytes encoded as 0xff followed by 2 bytes of big-endian encoded number.
+@interface TKSimpleTLVRecord : TKTLVRecord
+
+/// Creates TLV record with specified tag and value.
+/// @param tag Tag value for the new record.
+/// @param value Value for the new record.
+/// @return Newly created TLV record.
+- (instancetype)initWithTag:(UInt8)tag value:(NSData *)value;
+
+@end
+
+/// TKCompactTLVRecord implements Compact-TLV encoding according to ISO7816-4
+/// Tag is number in range <0..15> encoded as high 4 bits of initial byte, length is number in range <0..15>
+/// encoded as low 4 bits of initial byte.  Value immediatelly follows leading byte.
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@interface TKCompactTLVRecord : TKTLVRecord
+
+/// Creates TLV record with specified tag and value.
+/// @param tag Tag value for the new record.
+/// @param value Value for the new record.
+/// @return Newly created TLV record.
+- (instancetype)initWithTag:(UInt8)tag value:(NSData *)value;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKToken.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKToken.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKToken.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKToken.h	2016-06-03 23:16:34.000000000 +0200
@@ -0,0 +1,288 @@
+//
+//  TKToken.h
+//  Copyright (c) 2015 Apple. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <Security/Security.h>
+
+#import <CryptoTokenKit/TKSmartCard.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@protocol TKTokenSessionDelegate;
+@class TKTokenSession;
+@class TKTokenKeyAlgorithm;
+@class TKTokenKeyExchangeParameters;
+@protocol TKTokenDelegate;
+@class TKToken;
+@protocol TKTokenDriverDelegate;
+@class TKTokenDriver;
+@class TKTokenKeychainContents;
+@class TKTokenAuthOperation;
+
+/*!
+ @abstract TKTokenObjectID Unique and persistent identification of objects on the token.
+ @discussion Uniquely and persistently identifies objects (keys and certificates) present on the token.  Type of this identifier must be compatible with plist and its format is defined by the implementation of token extension.
+ */
+typedef id TKTokenObjectID
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE;
+
+/*!
+ @enum TKTokenOperation enumerates operations which can be performed with objects (keys and certificates) on the token.
+ */
+typedef NS_ENUM(NSInteger, TKTokenOperation) {
+    TKTokenOperationNone                = 0,
+
+    /*! Reading of raw data of certificate. */
+    TKTokenOperationReadData            = 1,
+
+    /*! Cryptographic signature using private key. */
+    TKTokenOperationSignData            = 2,
+
+    /*! Decrypting data using private key. */
+    TKTokenOperationDecryptData         = 3,
+
+    /*! Performing Diffie-Hellman style of cryptographic key exchange using private key. */
+    TKTokenOperationPerformKeyExchange  = 4,
+} __OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE;
+
+/*!
+ @abstract TKTokenOperationConstraint represents authentication constraint of token object for specific token operation.
+ @discussion Persistently identifies constraint for performing specific operation on specific object.  Value of constraint can be either:
+  - @YES: the operation is always allowed without any authentication needed
+  - @NO: the operation is never allowed, typically not implemented
+  - any other plist-compatible value: defined by the token extension implementation.  Such constraint is opaque to the system and is required to stay constant for the given object during the whole token's lifetime.  For example, smart card token extension might decide to use string 'PIN' to indicate that the operation is protected by presenting valid PIN to the card first.
+ */
+typedef id TKTokenOperationConstraint
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE;
+
+/*!
+ @abstract TKTokenKeyAlgorithm Encapsulates cryptographic algorithm, possibly with additional associated required algorithms.
+ @discussion An algorithm supported by a key can be usually described by one value of @c SecKeyAlgorithm enumeration.  However, some tokens (notably smartcards) require that input data for the operation are in generic format, but that generic format must be formatted according to some more specific algorithm.  An example for this would be token accepting raw data for cryptographic signature but requiring that raw data are formatted according to PKCS1 padding rules.  To express such requirement, TKTokenKeyAlgorithm defines target algorithm (@c kSecKeyAlgorithmRSASignatureRaw in our example) and a set of other algorithms which were used (continuing example above, @c kSecKeyAlgorithmRSASignatureDigestPKCS1v15SHA1 will be reported as supported).
+ */
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@interface TKTokenKeyAlgorithm : NSObject
+
+- (instancetype)init NS_UNAVAILABLE;
+
+/*!
+ @brief Checks if specified algorithm is base operation algorithm.
+ */
+- (BOOL)isAlgorithm:(SecKeyAlgorithm)algorithm;
+
+/*!
+ @brief Checks whether specified algorithm is either target algorithm or one of the algorithms through which the operation passed.
+ */
+- (BOOL)supportsAlgorithm:(SecKeyAlgorithm)algorithm;
+
+@end
+
+/*!
+ @abstract TKTokenKeyExchangeParameters Encapsulates parameters needed for performing specific Key Exchange operation types.
+ */
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@interface TKTokenKeyExchangeParameters : NSObject
+
+/*!
+ @discussion Requested output size of key exchange result.  Should be ignored if output size is not configurable for specified key exchange algorithm.
+ */
+@property (readonly) NSInteger requestedSize;
+
+/*!
+ @discussion Additional shared information input, typically used for key derivation (KDF) step of key exchange algorithm.  Should be ignored if shared info is not used for specified key exchange algorithm.
+ */
+@property (readonly, nullable, copy) NSData *sharedInfo;
+
+@end
+
+/*!
+ @abstract TKTokenSession represents token session which shares authentication status.
+ @discussion Token implementation must inherit its own session implementation from TKTokenSession (or its subclass TKSmartCardTokenSession in case of smart card tokens).
+
+ TKTokenSession should keep an authentication state of the token.  Authentication status (e.g. entered PIN to unlock smart card) should not be shared across borders of single TKTokenSession instance.
+
+ TKTokenSession is always instantiated by TKToken when framework detects access to the token from new authentication session.
+ */
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@interface TKTokenSession : NSObject
+
+/*!
+ @param token Token instance to which is this session instance bound.
+ */
+- (instancetype)initWithToken:(TKToken *)token NS_DESIGNATED_INITIALIZER;
+@property (readonly) TKToken *token;
+@property (weak, nullable) id<TKTokenSessionDelegate> delegate;
+
+- (instancetype)init NS_UNAVAILABLE;
+
+@end
+
+/*!
+ @abstract TKTokenSessionDelegate contains operations with token objects provided by token implementors which should be performed in the context of authentication session.
+ */
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@protocol TKTokenSessionDelegate<NSObject>
+
+@optional
+
+/*!
+ @discussion Establishes a context for the requested authentication operation.
+ @param tokenSession Related TKTokenSession instance.
+ @param operation Identifier of the operation.
+ @param constraint Constraint to be satisfied by this authentication operation.
+ @param error Error details (see TKError.h).
+ @return authOperation Resulting context of the operation, which will be eventually finalized by receiving 'finishWithError:'.  The resulting 'authOperation' can be of any type based on TKTokenAuthOperation. For known types (e.g. TKTokenPasswordAuthOperation) the system will first fill in the context-specific properties (e.g. 'password') before triggering 'finishWithError:'.
+ */
+- (nullable TKTokenAuthOperation *)tokenSession:(TKTokenSession *)session beginAuthForOperation:(TKTokenOperation)operation constraint:(TKTokenOperationConstraint)constraint error:(NSError **)error;
+
+/*!
+ @discussion Checks whether specified operation and algorithm is supported on specified key.
+ @param tokenSession Related TKTokenSession instance.
+ @param operation Type of cryptographic operation for which the list of supported algorithms should be retrieved.
+ @param keyObjectID Identifier of the private key object.
+ @param algorithm Algorithm with which the oepration should be performed.
+ @return YES if the operation is supported, NO otherwise.
+ */
+- (BOOL)tokenSession:(TKTokenSession *)session supportsOperation:(TKTokenOperation)operation usingKey:(TKTokenObjectID)keyObjectID algorithm:(TKTokenKeyAlgorithm *)algorithm;
+
+/*!
+ @discussion Performs cryptographic signature operation.
+ @param tokenSession Related TKTokenSession instance.
+ @param dataToSign Input data for the signature operation.
+ @param keyObjectID Identifier of the private key object.
+ @param algorithm Requested signature algorithm to be used.
+ @param error Error details (see TKError.h).  If authentication is required (by invoking beginAuthForOperation:), @c TKErrorCodeAuthenticationNeeded should be used.
+ @return Resulting signature, or nil if an error happened.
+ */
+- (nullable NSData *)tokenSession:(TKTokenSession *)session signData:(NSData *)dataToSign usingKey:(TKTokenObjectID)keyObjectID algorithm:(TKTokenKeyAlgorithm *)algorithm error:(NSError **)error;
+
+/*!
+ @discussion Decrypts ciphertext using private key.
+ @param tokenSession Related TKTokenSession instance.
+ @param ciphertext Encrypted data to decrypt.
+ @param keyObjectID Identifier of the private key object.
+ @param algorithm Requested encryption/decryption algorithm to be used.
+ @param error Error details (see TKError.h).  If authentication is required (by invoking beginAuthForOperation:), @c TKErrorCodeAuthenticationNeeded should be used.
+ @return Resulting decrypted plaintext, or nil if an error happened.
+ */
+- (nullable NSData *)tokenSession:(TKTokenSession *)session decryptData:(NSData *)ciphertext usingKey:(TKTokenObjectID)keyObjectID algorithm:(TKTokenKeyAlgorithm *)algorithm error:(NSError **)error;
+
+/*!
+ @discussion Performs Diffie-Hellman style key exchange operation.
+ @param tokenSession Related TKTokenSession instance.
+ @param otherPartyPublicKeyData Raw public data of other party public key.
+ @param keyObjectID Identifier of the private key object.
+ @param algorithm Requested key exchange algorithm to be used.
+ @param parameters Additional parameters for key exchange operation.  Chosen algorithm dictates meaning of parameters.
+ @param error Error details (see TKError.h).  If authentication is required (by invoking beginAuthForOperation:), @c TKErrorCodeAuthenticationNeeded should be used.
+ @return Result of key exchange operation, or nil if the operation failed.
+ */
+- (nullable NSData *)tokenSession:(TKTokenSession *)session performKeyExchangeWithPublicKey:(NSData *)otherPartyPublicKeyData usingKey:(TKTokenObjectID)objectID algorithm:(TKTokenKeyAlgorithm *)algorithm parameters:(TKTokenKeyExchangeParameters *)parameters error:(NSError **)error;
+
+@end
+
+/*!
+ @discussion Class representing single token.  When implementing smart card based token, it is recommended to inherit the implementation from TKSmartCardToken.  Token object serves as synchronization point, all operations invoked upon token and all its sessions are serialized.
+ */
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@interface TKToken : NSObject
+
+/*!
+ @discussion Initializes token instance
+ @param tokenDriver Creating token driver.
+ @param instanceID Unique, persistent identifier of this token.  This is typically implemented by some kind of serial number of the target hardware, for example smart card serial number.
+ */
+- (instancetype)initWithTokenDriver:(TKTokenDriver *)tokenDriver instanceID:(NSString *)instanceID NS_DESIGNATED_INITIALIZER;
+@property (readonly) TKTokenDriver *tokenDriver;
+@property (weak, nullable) id<TKTokenDelegate> delegate;
+
+/*!
+ @discussion Keychain contents (certificate and key items) representing this token.
+ */
+@property (nullable, readonly) TKTokenKeychainContents *keychainContents;
+
+- (instancetype)init NS_UNAVAILABLE;
+
+@end
+
+/*!
+ @abstract TKTokenDelegate contains operations implementing functionality of token class.
+ @discussion TKTokenDelegate represents protocol which must be implemented by token implementors' class representing token.  Apart from being able to identify itself with its unique identifier, and must be able to establish new TKTokenSession when requested.
+ */
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@protocol TKTokenDelegate<NSObject>
+
+@required
+
+/*!
+ @abstract Create new session instance
+ @discussion All operations with objects on the token are performed inside TKTokenSession which represent authentication context.  This method is called whenever new authentication context is needed (typically when client application wants to perform token operation using keychain object which has associated LocalAuthentication LAContext which was not yet seen by this token instance).
+ @param token Related token instance.
+ */
+- (nullable TKTokenSession *)token:(TKToken *)token createSessionWithError:(NSError **)error;
+
+@optional
+
+/*!
+ @abstract Terminates previously created session, implementation should free all associated resources.
+ @param token Related token instance.
+ */
+- (void)token:(TKToken *)token terminateSession:(TKTokenSession *)session;
+
+@end
+
+/*!
+ @discussion Base class for token drivers.  Smart card token drivers should use TKSmartCardTokenDriver subclass.
+ */
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@interface TKTokenDriver : NSObject
+
+@property (weak, nullable) id<TKTokenDriverDelegate> delegate;
+
+@end
+
+/*!
+ @discussion Delegate for customizing token driver operations.  Smart card tokens should implement TKSmartcardTokenDriverDelegate instead of this base protocol.
+ */
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@protocol TKTokenDriverDelegate<NSObject>
+
+@optional
+
+/*!
+ @discussion Terminates previously created token, should release all resources associated with it.
+ */
+- (void)tokenDriver:(TKTokenDriver *)driver terminateToken:(TKToken *)token;
+
+@end
+
+/*!
+ @discussion Context of a pending authentication operation.
+ */
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@interface TKTokenAuthOperation : NSObject<NSSecureCoding>
+
+/*!
+ @discussion Handler triggered by the system in order to let the token finalize the authentication operation.
+ @param error Error details (see TKError.h).
+ @return Finalization status.
+ */
+- (BOOL)finishWithError:(NSError **)error;
+
+@end
+
+/*!
+ @discussion Context of a password authentication operation.
+ */
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@interface TKTokenPasswordAuthOperation : TKTokenAuthOperation
+
+/*!
+ @discussion Password, which will be filled in by the system when 'finishWithError:' is called.
+ */
+@property (nullable, copy) NSString *password;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKTokenKeychainItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKTokenKeychainItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKTokenKeychainItem.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKTokenKeychainItem.h	2016-06-03 23:16:34.000000000 +0200
@@ -0,0 +1,152 @@
+//
+//  TKTokenKeychainItem.h
+//  Copyright © 2015-2016 Apple. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+#import <CryptoTokenKit/TKToken.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class TKTokenKeychainItem;
+@class TKTokenKeychainCertificate;
+@class TKTokenKeychainKey;
+@class TKTokenKeychainState;
+
+/*!
+ @interface TKTokenKeychainItem
+ @brief Base interface for propagation token's items into the keychain.
+ */
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@interface TKTokenKeychainItem : NSObject
+
+/*! @brief Initializes item with objectID. */
+- (instancetype)initWithObjectID:(TKTokenObjectID)objectID NS_DESIGNATED_INITIALIZER;
+- (instancetype)init NS_UNAVAILABLE;
+
+/*! @brief object ID for item identification */
+@property (readonly, copy) TKTokenObjectID objectID;
+
+/*!
+ @discussion Contains the user-visible label for this item.  This property is an equivalent of kSecAttrLabel in SecItem.h
+ */
+@property (nullable, copy) NSString *label;
+
+/*!
+ @discussion Contains access constraints for this object keyed by TKTOpenOperation wrapped in NSNumber.
+ */
+@property (nullable, copy) NSDictionary<NSNumber *, TKTokenOperationConstraint> *constraints;
+
+@end
+
+/*!
+ @interface TKTokenKeychainCertificate
+ @brief Interface for propagation token's certificates into the keychain.
+ */
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@interface TKTokenKeychainCertificate : TKTokenKeychainItem
+
+/*!
+ @discussion initialize TKTokenKeychainCertificate with data from SecCertificateRef.  Use SecCertificateCreateWithData to obtain SecCertificateRef.  @c constraints property is initialized indicating that reading of certificate is always allowed, all other operations are disallowed.
+ */
+- (nullable instancetype)initWithCertificate:(SecCertificateRef)certificateRef objectID:(TKTokenObjectID)objectID NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithObjectID:(TKTokenObjectID)objectID NS_UNAVAILABLE;
+
+/*!
+ @discussion Contains DER-encoded representation of an X.509 certificate.
+ */
+@property (copy, readonly) NSData *data;
+
+@end
+
+/*!
+ @interface TKTokenKeychainKey
+ @brief Interface for propagation token's keys into the keychain.
+ */
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@interface TKTokenKeychainKey : TKTokenKeychainItem
+
+/*!
+ @discussion Initialize TKTokenKeychainKey with informations from SecCertificateRef associated with the key.  Use SecCertificateCreateWithData to obtain SecCertificateRef.  If NULL is passed instead of certificate, all properties of created instance must be initialized manually.
+ */
+- (nullable instancetype)initWithCertificate:(nullable SecCertificateRef)certificateRef objectID:(TKTokenObjectID)objectID NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithObjectID:(TKTokenObjectID)objectID NS_UNAVAILABLE;
+
+/*!
+ @discussion Type of the key, currently kSecAttrKeyTypeRSA and kSecAttrKeyTypeECSECPrimeRandom is supported).  The property is an equivalent to kSecAttrKeyType in SecItem.h
+ */
+@property (copy) NSString *keyType;
+
+/*!
+ @discussion Represents private tag data.  The property is an equivalent to kSecAttrApplicationTag in SecItem.h
+ */
+@property (copy, nullable) NSData *applicationTag;
+
+/*!
+ @discussion Indicates the number of bits in this key.  The property is an equivalent to kSecAttrKeySizeInBits in SecItem.h
+ */
+@property NSInteger keySizeInBits;
+
+/*!
+ @discussion Contains raw public key data for this private key.
+ */
+@property (copy, nullable) NSData *publicKeyData;
+
+/*!
+ @discussion SHA1 hash of the raw public key.  The property is an equivalent to kSecAttrApplicationLabel in SecItem.h
+ */
+@property (copy, nullable) NSData *publicKeyHash;
+
+/*!
+ @discussion Indicates whether this key can be used to decrypt data.  The property is an equivalent to kSecAttrCanDecrypt in SecItem.h
+ */
+@property BOOL canDecrypt;
+
+/*!
+ @discussion Indicates whether this key can be used to create a digital signature.  The property is an equivalent to kSecAttrCanSign in SecItem.h
+ */
+@property BOOL canSign;
+
+/*!
+ @discussion Indicates whether this key can be used to perform Diffie-Hellman style cryptographic key exchange.
+ */
+@property BOOL canPerformKeyExchange;
+
+/*!
+ @discussion Indicates whether this key can be used for login in to the system.
+ */
+@property (getter=isSuitableForLogin) BOOL suitableForLogin;
+
+@end
+
+/*!
+ @discussion Contains TKTokenKeychainItem instances (keys and certificates) which represent keychain state (i.e. set of items) of specific token.
+ */
+__OSX_AVAILABLE(10.12) __IOS_AVAILABLE(10.0) __TVOS_UNAVAILABLE __WATCHOS_UNAVAILABLE
+@interface TKTokenKeychainContents : NSObject
+
+/*!
+ @discussion Fills keychain with the set of specified items.  All items belonging to token are first removed from the keychain and then the keychain is populated with new items.
+ @param items New items to be stored into the keychain.
+ */
+- (void)fillWithItems:(NSArray<TKTokenKeychainItem *> *)items;
+
+/*! @brief All items related to this token in the keychain. */
+@property (readonly, copy) NSArray<TKTokenKeychainItem *> *items;
+
+/*!
+ @discussion Returns key with specified objectID.  Fills error with TKTokenErrorCodeObjectNotFound if no such key exists.
+ */
+- (nullable TKTokenKeychainKey *)keyForObjectID:(TKTokenObjectID)objectID error:(NSError **)error;
+
+/*!
+ @discussion Returns certificate with specified objectID.  Fills error with TKTokenErrorCodeObjectNotFound if no such certificate exists.
+ */
+- (nullable TKTokenKeychainCertificate *)certificateForObjectID:(TKTokenObjectID)objectID error:(NSError **)error;
+
+- (instancetype)init NS_UNAVAILABLE;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKTokenWatcher.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKTokenWatcher.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKTokenWatcher.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CryptoTokenKit.framework/Headers/TKTokenWatcher.h	2016-06-03 23:16:34.000000000 +0200
@@ -0,0 +1,31 @@
+//
+//  TKTokenWatcher.h
+//  Copyright (c) 2015 Apple. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@interface TKTokenWatcher : NSObject
+
+/// Array of currently known TokenIDs in the system.  Tokens are identified by instance's names. It is possible to use KVO to be notified about token arrivals and removals.
+@property (readonly) NSArray<NSString *> *tokenIDs;
+
+/// Init watcher
+- (instancetype)init;
+
+/// Init watcher with insertion handler
+/// @disscussion init watcher with insertion handler which is called when a new token arrives
+/// @param insertionHandler
+- (instancetype)initWithInsertionHandler:(void(^)(NSString* tokenID)) insertionHandler;
+
+/// Add removal watcher for specific tokenID
+/// @disscussion after removalHandler for a specific tokenID is called the reference to this handler is removed. For one tokenID just one handler can be added, so next call to addRemovalHandler will replace previous handler
+/// @param removalHandler
+/// @param tokenID specified tokenID, if tokenID does not exist removal handler is called imediately
+- (void)addRemovalHandler:(void(^)(NSString* tokenID)) removalHandler forTokenID:(NSString*) tokenID;
+
+@end
+
+NS_ASSUME_NONNULL_END
\ No newline at end of file

```