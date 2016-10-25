id:23e82b9c-09e5-428f-9aab-196687fb6ebd
title:Xamarin.iOS
version:10.3.0
releasedate:2016-10-25

<div class="note">
	<b>Master / Cycle 9 Daily Builds</b>
	This version of Xamarin.iOS will ship as part of Xamarin **cycle 9** releases.
	Some fixes might be backported into `cycle8` and released long before other parts of `master` becomes public.
</div>

<div class="note">
	<b>Mono TLS Deprecation:</b>
	This version of Xamarin.iOS (C9) is the last one to ship with the optional Mono (managed) SSL/TLS provider.
	This old provider only supports the SSLv3 and TLSv1 standards, which several servers don't support anymore.
	Support for the newer TLSv1.1 and 1.2 is only available using the newer AppleTLS provider. 
	This new provider is already used, by default, when building applications (since XI 9.8 / C7).
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

### API diff

This is a live document so there's no static list to link to. However our [Jenkins bots](https://jenkins.mono-project.com/job/xamarin-macios-pr-builder/) produce this information for every commit that is being built. Pick on based on `master` and look for the **API diff** link on the left column.