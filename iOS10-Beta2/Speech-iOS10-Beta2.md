#Speech.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionRequest.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionRequest.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionRequest.h	2016-05-25 05:46:00.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionRequest.h	2016-06-25 02:36:06.000000000 +0200
@@ -17,15 +17,9 @@
 @property (nonatomic) SFSpeechRecognitionTaskHint taskHint;
 
 // If true, partial (non-final) results for each utterance will be reported.
-// Default is false for file requests and true for recording requests
+// Default is true
 @property (nonatomic) BOOL shouldReportPartialResults;
 
-// If true, utterances will be automatically segmented. Each "final" result will
-// correspond to the end of a single utterance; further results for the next
-// utterance will follow if it is in the audio source.
-// Default is false
-@property (nonatomic) BOOL detectMultipleUtterances;
-
 // Phrases which should be recognized even if they are not in the system vocabulary
 @property (nonatomic, copy) NSArray<NSString *> *contextualStrings;
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionTask.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionTask.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionTask.h	2016-05-25 05:46:00.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognitionTask.h	2016-06-25 02:36:06.000000000 +0200
@@ -35,19 +35,6 @@
 // Reports error that occurred during recognition, if applicable
 @property (nonatomic, readonly, copy, nullable) NSError *error;
 
-// True if power metering is availble for this request.
-// Currently only available when using SFSpeechRecordingRecognitionRequest
-@property (nonatomic, readonly, getter=isPowerAvailable) BOOL powerAvailable;
-
-// Current peak power, in decibels, for the sound being recorded.
-// A return value of 0 dB indicates full scale, or maximum power; a return value of -160 dB indicates minimum power
-// Valid only if powerAvailable is true
-@property (nonatomic, readonly) float peakPower;
-
-// Average power for a given channel, in decibels, for any sound being recorded
-// Valid only if powerAvailable is true
-@property (nonatomic, readonly) float averagePower;
-
 @end
 
 // Recognition result receiver, to be used for complex or multi-utterance speech recognition requests
@@ -74,10 +61,6 @@
 // If successfully is false, the error property of the task will contain error information
 - (void)speechRecognitionTask:(SFSpeechRecognitionTask *)task didFinishSuccessfully:(BOOL)successfully;
 
-// Called as audio is recorded. Not called for audio which is not recorded.
-// A task will only send this message to its delegate if the calling process has permission to record the user's audio.
-- (void)speechRecognitionTask:(SFSpeechRecognitionTask *)task didRecordAudioPCMBuffer:(AVAudioPCMBuffer *)audioPCMBuffer;
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognizer.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognizer.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognizer.h	2016-05-25 05:46:00.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Speech.framework/Headers/SFSpeechRecognizer.h	2016-06-25 02:36:06.000000000 +0200
@@ -40,7 +40,6 @@
 - (nullable instancetype)initWithLocale:(NSLocale *)locale NS_DESIGNATED_INITIALIZER; // returns nil if the locale is not supported
 
 @property (nonatomic, readonly, getter=isAvailable) BOOL available;
-@property (nonatomic, readonly, getter=isAvailableForRecordingRecognition) BOOL availableForRecordingRecognition;
 @property (nonatomic, readonly, copy) NSLocale *locale;
 
 @property (nonatomic, weak) id<SFSpeechRecognizerDelegate> delegate;
@@ -48,10 +47,6 @@
 // Default task for requests, overrides SFSpeechRecognitionTaskHintUnspecified for requests
 @property (nonatomic) SFSpeechRecognitionTaskHint defaultTaskHint;
 
-// Hint to the recognizer to become ready for an imminent recognition request.
-// Purely an optional performance optimization.
-- (void)prepareWithRequest:(SFSpeechRecordingRecognitionRequest *)request;
-
 // Recognize speech utterance with a request
 // If request.shouldReportPartialResults is true, result handler will be called
 // repeatedly with partial results, then finally with a final result or an error.

```