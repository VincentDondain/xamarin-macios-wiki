id:23e82b9c-09e5-428f-9aab-196687fb6ebd
title:Xamarin.iOS
version:9.11.0
releasedate:2016-07-14

<div class="note">
	<b>Cycle 9 Daily Builds</b>
	This version of Xamarin.iOS will likely ship after the release of Xcode 8 and Xamarin.iOS 10.
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

### watchOS

This version introduces stable support for native watchOS 2+ applications.

However due to the limited API available on watchOS, the managed networking stack is not available. This means that the following managed API will throw PlatformNotSupportedExceptions:

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

As an alternative use HttpClient, which will use the native networking stack through a custom HttpMessageHandler (NSUrlSessionHandler).

### Known Issues


### API diff

This is a live document so there's no static list to link to. However our [Jenkins bots](https://jenkins.mono-project.com/job/xamarin-macios-pr-builder/) produce this information for every commit that is being built. Pick on based on `master` and look for the **API diff** link on the left column.