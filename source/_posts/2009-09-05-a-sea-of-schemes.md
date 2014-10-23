---
title: A Sea of Schemes
author: gxbsst
layout: post
permalink: /archives/273
post_views_count:
  - 332
views:
  - 116
categories:
  - Xhtml/css
---
2.5 A Sea of Schemes

In this section, we&#8217;ll take a look at the more common scheme formats on the Web. Appendix A gives a fairly exhaustive list of schemes and references to their individual documentation.

Table 2-4 summarizes some of the most popular schemes. Reviewing Section 2.2 will make the syntax portion of the table a little more familiar.

Table 2-4. Common scheme formats

Scheme

Description

http

The Hypertext Transfer Protocol scheme conforms to the general URL format, except that there is no username or password. The port defaults to 80 if omitted.

Basic form:

http://<host>:<port>/<path>?<query>#<frag>

Examples:

http://www.joes-hardware.com/index.html

http://www.joes-hardware.com:80/index.html

https

The https scheme is a twin to the http scheme. The only difference is that the https scheme uses Netscape&#8217;s Secure Sockets Layer (SSL), which provides end-to-end encryption of HTTP connections. Its syntax is identical to that of HTTP, with a default port of 443.

Basic form:

https://<host>:<port>/<path>?<query>#<frag>

Example:

https://www.joes-hardware.com/secure.html

mailto

Mailto URLs refer to email addresses. Because email behaves differently from other schemes (it does not refer to objects that can be accessed directly), the format of a mailto URL differs from that of the standard URL. The syntax for Internet email addresses is documented in Internet RFC 822.

Basic form:

mailto:<RFC-822-addr-spec>

Example:

mailto:joe@joes-hardware.com

ftp

File Transfer Protocol URLs can be used to download and upload files on an FTP server and to obtain listings of the contents of a directory structure on an FTP server.

FTP has been around since before the advent of the Web and URLs. Web applications have assimilated FTP as a data-access scheme. The URL syntax follows the general form.

Basic form:

ftp://<user>:<password>@<host>:<port>/<path>;<params>

Example:

ftp://anonymous:joe%40joes-hardware.com@prep.ai.mit.edu:21/pub/gnu/

rtsp, rtspu

RTSP URLs are identifiers for audio and video media resources that can be retrieved through the Real Time Streaming Protocol.

The &#8220;u&#8221; in the rtspu scheme denotes that the UDP protocol is used to retrieve the resource.

Basic forms:

rtsp://<user>:<password>@<host>:<port>/<path>

rtspu://<user>:<password>@<host>:<port>/<path>

Example:

rtsp://www.joes-hardware.com:554/interview/cto_video

file

The file scheme denotes files directly accessible on a given host machine (by local disk, a network filesystem, or some other file-sharing system). The fields follow the general form. If the host is omitted, it defaults to the local host from which the URL is being used.

Basic form:

file://<host>/<path>

Example:

file://OFFICE-FS/policies/casual-fridays.doc

news

The news scheme is used to access specific articles or newsgroups, as defined by RFC 1036. It has the unusual property that a news URL in itself does not contain sufficient information to locate the resource.

The news URL is missing information about where to acquire the resource—no hostname or machine name is supplied. It is the interpreting application&#8217;s job to acquire this information from the user. For example, in your Netscape browser, under the Options menu, you can specify your NNTP (news) server. This tells your browser what server to use when it has a news URL.

News resources can be accessed from multiple servers. They are said to be location-independent, as they are not dependent on any one source for access.

The &#8220;@&#8221; character is reserved within a news URL and is used to distinguish between news URLs that refer to newsgroups and news URLs that refer to specific news articles.

Basic forms:

news:<newsgroup>

news:<news-article-id>

Example:

news:rec.arts.startrek

telnet

The telnet scheme is used to access interactive services. It does not represent an object per se, but an interactive application (resource) accessible via the telnet protocol.

Basic form:

telnet://<user>:<password>@<host>:<port>/

Example:

telnet://slurp:webhound@joes-hardware.com:23/

转载请注明：[韦旭红的点点滴滴][1] &raquo; [A Sea of Schemes][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/273