#Speech.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionRequest.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionRequest.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionRequest.h	2016-09-24 04:24:15.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionRequest.h	2016-10-23 09:41:16.000000000 +0200
@@ -12,6 +12,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 // A request for a speech recognition from an audio source
+API_AVAILABLE(ios(10.0))
 @interface SFSpeechRecognitionRequest : NSObject
 
 @property (nonatomic) SFSpeechRecognitionTaskHint taskHint;
@@ -29,6 +30,7 @@
 @end
 
 // A request to recognize speech from a recorded audio file
+API_AVAILABLE(ios(10.0))
 @interface SFSpeechURLRecognitionRequest : SFSpeechRecognitionRequest
 
 - (instancetype)init NS_UNAVAILABLE;
@@ -41,6 +43,7 @@
 @end
 
 // A request to recognize speech from arbitrary audio buffers
+API_AVAILABLE(ios(10.0))
 @interface SFSpeechAudioBufferRecognitionRequest : SFSpeechRecognitionRequest
 
 // Preferred audio format for optimal speech recognition
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionResult.h	2016-09-24 04:24:15.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionResult.h	2016-10-23 09:41:16.000000000 +0200
@@ -11,6 +11,7 @@
 @class SFTranscription;
 
 // A recognized utterance, corresponding to a segment of recorded audio with speech and containing one or more transcriptions hypotheses
+API_AVAILABLE(ios(10.0))
 @interface SFSpeechRecognitionResult : NSObject <NSCopying, NSSecureCoding>
 
 @property (nonatomic, readonly, copy) SFTranscription *bestTranscription;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionTask.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionTask.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionTask.h	2016-09-24 04:24:15.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionTask.h	2016-10-23 09:41:16.000000000 +0200
@@ -17,8 +17,9 @@
     SFSpeechRecognitionTaskStateFinishing = 2,      // No more audio is being recorded, but more recognition results may arrive
     SFSpeechRecognitionTaskStateCanceling = 3,      // No more recognition reuslts will arrive, but recording may not have stopped yet
     SFSpeechRecognitionTaskStateCompleted = 4,      // No more results will arrive, and recording is stopped.
-};
+} API_AVAILABLE(ios(10.0));
 
+API_AVAILABLE(ios(10.0))
 @interface SFSpeechRecognitionTask : NSObject
 
 @property (nonatomic, readonly) SFSpeechRecognitionTaskState state;
@@ -38,6 +39,7 @@
 @end
 
 // Recognition result receiver, to be used for complex or multi-utterance speech recognition requests
+API_AVAILABLE(ios(10.0))
 @protocol SFSpeechRecognitionTaskDelegate <NSObject>
 
 @optional
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionTaskHint.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionTaskHint.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionTaskHint.h	2016-09-24 04:24:15.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionTaskHint.h	2016-10-23 09:41:16.000000000 +0200
@@ -9,4 +9,4 @@
     SFSpeechRecognitionTaskHintDictation = 1,       // General dictation/keyboard-style
     SFSpeechRecognitionTaskHintSearch = 2,          // Search-style requests
     SFSpeechRecognitionTaskHintConfirmation = 3,    // Short, confirmation-style requests ("Yes", "No", "Maybe")
-};
+} API_AVAILABLE(ios(10.0));
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognizer.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognizer.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognizer.h	2016-09-24 04:24:15.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognizer.h	2016-10-23 09:41:16.000000000 +0200
@@ -25,8 +25,9 @@
     SFSpeechRecognizerAuthorizationStatusDenied,
     SFSpeechRecognizerAuthorizationStatusRestricted,
     SFSpeechRecognizerAuthorizationStatusAuthorized,
-};
+} API_AVAILABLE(ios(10.0));
 
+API_AVAILABLE(ios(10.0))
 @interface SFSpeechRecognizer : NSObject
 
 // Locales which support speech recognition.
@@ -64,6 +65,7 @@
 
 @end
 
+API_AVAILABLE(ios(10.0))
 @protocol SFSpeechRecognizerDelegate <NSObject>
 @optional
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFTranscription.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFTranscription.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFTranscription.h	2016-09-24 04:24:15.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFTranscription.h	2016-10-23 09:41:16.000000000 +0200
@@ -10,6 +10,7 @@
 @class SFTranscriptionSegment;
 
 // A hypothesized text form of a speech recording
+API_AVAILABLE(ios(10.0))
 @interface SFTranscription : NSObject <NSCopying, NSSecureCoding>
 
 // Contains the entire recognition, formatted into a single user-displayable string
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFTranscriptionSegment.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFTranscriptionSegment.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFTranscriptionSegment.h	2016-09-24 04:24:15.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFTranscriptionSegment.h	2016-10-23 09:41:16.000000000 +0200
@@ -8,6 +8,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 // Substrings of a hypothesized transcription
+API_AVAILABLE(ios(10.0))
 @interface SFTranscriptionSegment : NSObject <NSCopying, NSSecureCoding>
 
 @property (nonatomic, readonly, copy) NSString *substring;

```