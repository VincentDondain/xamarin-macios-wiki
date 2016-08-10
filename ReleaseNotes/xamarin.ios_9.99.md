<div class="note">
	<b>Classic Profile Deprecation:</b>
	The complete removal of classic support is scheduled for next fall with the release of Xamarin.iOS 10.0 and
	this preview of our iOS 10 support does <b>not</b> ship with <code>monotouch.dll</code>.
	Xamarin.iOS 9.10 (cycle 8) will be the last version to ship support for <code>monotouch.dll</code> this summer.
</div>

Requirements
============

- The latest features and API requires Xcode 8.0 beta 4 and the bundled iOS, tvOS and watchOS SDKs;
- Apple Xcode 8.0 requires a Mac running OSX 10.11.5 (El Capitan) or newer;

What's New
==========

This release is built upon our [open sourced SDK](https://github.com/xamarin/xamarin-macios),
using the `xcode8` branch, and include some additional IDE integratin tools.

This release is based on our **cycle 8** work, which will become XI 9.10 this summer.
It includes Mono 4.6 which continues to adopt more code from 
Microsoft's open sourced .NET code (reference source) to improve the conformance,
speed and memory usage of our base class libraries (BCL).

### iOS 10

The following new frameworks were added in iOS 10:

* CallKit (available, beta 4)
* Intents (available, beta 4)
* IntentsUI (available, beta 5)
* Message (available, beta 5)
* Speech (available, beta 5)
* UserNotification (available, beta 5)
* UserNotificationUI (available, beta 5)
* VideoSubscriberAccount (available, beta 5)

### tvOS 10

The following new frameworks were added in tvOS 10:

* ExternalAccessory (available, beta 5)
* HomeKit (available, beta 5)
* MultipeerConnectivity (available, beta 5)
* Photos (available, beta 5)
* PhotosUI (available, beta 5)
* ReplayKit (available, beta 5)
* UserNotification (available, beta 5)
* VideoSubscriberAccount (enabled, unaudited)

Note: New frameworks for tvOS are new to the platform, but already exists (or were just added) in iOS.

Bindings are also update for the exising frameworks:

* TVMLKit (available, beta 5)
* Several new API are also available (see **Work In Progress** and **API diff**)

### watchOS 3

The following new frameworks were added in watchOS 3:

* AVFoundation (not yet enabled)
* CloudKit (available, beta 5)
* CoreAudio (not yet enabled)
* GameKit (available, beta 5)
* SceneKit (available, beta 4, except API that require the AVFoundation framework)
* SpriteKit (available, beta 5, except API that require the AVFoundation framework)
* UserNotification (available, beta 5)

Note: New frameworks for watchOS are new to the platform, but already exists (or were just added) in iOS.

Bindings are also update for the exising frameworks:

* ClockKit (up to beta 5)
* WatchKit (up to beta 5)
* Several new API are also available (see **Work In Progress** and **API diff**)


### Work In Progress

Beside the new frameworks there are also many updates to the existing ones. You can track the [progress of our bindings](https://github.com/xamarin/xamarin-macios/wiki/Bindings) from the wiki.

In general we start iOS SDK and when a new beta gets out then we update existing bindings to match the latest changes, then we go back to bind other frameworks. Next we'll work on tvOS and watchOS SDK.

Starting with iOS means we're including most new, shared API with tvOS, watchOS and macOS. The later platforms generally do not require a lot of changes when iOS bindings are over (mostly auditing the API).


### Known Issues

* **Issue:** our watchOS 3.x support has the same limitations our watchOS 2.x support in the current [XI 9.10 alpha](releases/ios/xamarin.ios_9/xamarin.ios_9.10). The same version of mono (code and tooling) are shared between **cycle8** and **xcode8** branches;


### API diff

This is a live document so there's no static list to link to. However our [Jenkins bots](https://jenkins.mono-project.com/job/xamarin-macios-pr-builder/) produce this information for every commit that is being built. Pick any build based on `xcode8` and look for the **API diff** link on the left column.
