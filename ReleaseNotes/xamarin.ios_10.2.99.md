id:23e82b9c-09e5-428f-9aab-196687fb6ebd
title:Xamarin.iOS
version:10.2.99
releasedate:2016-11-01

<div class="note">
	<b>Xcode 8.2 Daily Builds</b>
	This version of Xamarin.iOS is based on XI 10.2.1 (C8 SR1) and will be released when Xcode 8.2 final version becomes public.
</div>

Requirements
============

- The latest features and API requires Xcode 8.2 beta 1 and the bundled iOS, tvOS and watchOS SDKs;
- Apple Xcode 8.2 requires a Mac running OSX 10.11.5 (El Capitan) or newer;

What's New
==========

This release is built upon our [open sourced SDK](https://github.com/xamarin/xamarin-macios),
using the `xcode8.2` branch, and include some additional IDE integratin tools.

### iOS 10.2

Minor API additions were made to:

* AVFoundation [not yet available]
* CloudKit [not yet available]
* HomeKit [not yet available]
* Intents [not yet available]
* MediaPlayer [not yet available]
* Messages [not yet available]
* ModelIO [not yet available]
* PassKit [done, up to beta 1]
* Photos [not yet available]
* ReplayKit [not yet available]
* Security [done, up to beta 1]
* Speech [not yet available]
* SpriteKit [not yet available]
* UIKit [done, up to beta 1]
* VideoSubscriberAccount [not yet available]
* WatchConnectivity [done, up to beta 1]
* WatchKit [not yet available]

### tvOS 10.1

Minor API additions were made to:

* AVFoundation [not yet available]
* AVKit [not yet available]
* CloudKit [not yet available]
* HomeKit [not yet available]
* MediaPlayer [not yet available]
* ModelIO [not yet available]
* Photos [not yet available]
* ReplayKit [not yet available]
* Security [done, up to beta 1]
* SpriteKit [not yet available]
* StoreKit [not yet available]
* UIKit [done, up to beta 1]
* VideoSubscriberAccount [not yet available]

### watchOS 3.1.1

There are no API changes in Xcode 8.2 beta 1 wrt watchOS 3.1.1.

### API diff

This is a live document so there's no static list to link to. However our [Jenkins bots](https://jenkins.mono-project.com/job/xamarin-macios-pr-builder/) produce this information for every commit that is being built. Pick on based on `master` and look for the **API diff** link on the left column.