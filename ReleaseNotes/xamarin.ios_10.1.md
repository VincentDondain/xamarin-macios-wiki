id:23e82b9c-09e5-428f-9aab-196687fb6ebd
title:Xamarin.iOS
version:10.1.0
releasedate:2016-10-04

<div class="note">
	<b>Master / Cycle 9 Daily Builds</b>
	This version of Xamarin.iOS will ship as part of Xamarin **cycle 9** releases.
	Some fixes might be backported into `cycle8` and released long before other parts of `master` becomes public.
</div>

Requirements
============

- The latest features and API requires Xcode 8 and the bundled iOS, tvOS and watchOS SDKs;
- Apple Xcode 8 requires a Mac running OSX 10.11.5 (El Capitan) or newer;

What's New
==========

This release is built upon our [open sourced SDK](https://github.com/xamarin/xamarin-macios),
using the `master` branch, and include some additional IDE integratin tools.

* It's now possible to specify how many parallel AOT processes mtouch can launch by using the `-j #` argument to mtouch (in the project's iOS Build options). The default is the number of processors on the machine, but builds on high-end machines may profit from increasing this value.

* A new implementation of `NSUrlSessionHandler` was [contributed](https://github.com/xamarin/xamarin-macios/pull/31) by Nick Berardi. The new version offers the same features as the previous one but requires less memory and, by resuing it, less time spent in the garbage collector;

### watchOS

This version introduces stable support for native watchOS 2+ applications.

However due to the limited API available on watchOS, the managed networking stack is not available. This means that the following managed API will throw `PlatformNotSupportedException`:

#### System assembly

* System.Net.AuthenticationManager
* System.Net.ServicePoint
* System.Net.ServicePointManager
* System.Net.Mail.SmtpClient
* System.Net.Security.SslStream
* System.Net.Sockets.Socket:Bind
* System.Net.Sockets.TcpClient
* System.Net.Sockets.TcpListener
* System.Net.Sockets.UdpClient
* System.Net.WebSockets.ClientWebSocket
* System.Net.Dns:[Begin]GetHostByName
* System.Net.Dns:[Begin]GetHostEntry
* System.Net.Dns:[Begin]Resolve
* System.Net.FtpWebRequest
* System.Net.FtpWebResponse
* System.Net.HttpListener
* System.Net.HttpListenerContext
* System.Net.HttpListenerPrefixCollection
* System.Net.HttpListenerRequest
* System.Net.HttpListenerResponse
* System.Net.HttpWebRequest
* System.Net.HttpWebResponse

#### System.Net.Http assembly

* System.Net.Http.HttpClientHandler

#### System.Data assembly

* System.Data.SqlClient namespace

And the following assemblies are not shipped at all:

* Mono.Data.Tds.dll
* Mono.Security.dll

As an alternative you can use

* Native API, e.g. `NSUrlSession*`; or
* `System.Net.Http.HttpClient` which will use the native networking stack through a custom `HttpMessageHandler`: `NSUrlSessionHandler`

### Xamarin Analysis

We added a new rule to our project analysis tool which ensures that iOS distribution builds do not include TestCloud support. App builds that initialize the Test Cloud agent will be rejected by Apple when submitted, as they use private API.

*As a reminder you can run the Xamarin Analysis rules from Xamarin Studio's menu bar by selecting Project > Run Code Analysis.*

### Known Issues

* **Issue: App may slow down your iPhone** (ex "App not optimized for iOS10") warning: This happens when a 32bit-only application executes on a 64 bits capable platform, e.g. a i386 build running on a iPhone 6 simulator (capable of 64bit). The warning simply means you're not using the optimal build for the platform. This can be normal when testing and, by default, simulator builds are only 32 or 64 bits (to make them faster).
	* **Workaround** You can change your project settings to remove the warning. Application submitted to the app store should have both 32 and 64 bits, in general, or be 64 bits only.

### API diff

This is a live document so there's no static list to link to. However our [Jenkins bots](https://jenkins.mono-project.com/job/xamarin-macios-pr-builder/) produce this information for every commit that is being built. Pick on based on `master` and look for the **API diff** link on the left column.