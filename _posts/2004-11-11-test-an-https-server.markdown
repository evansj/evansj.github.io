---
layout: post
title: Test an https server
tags:
- t'internet
typo_id: 33
---
<p>This is so useful (to a developer) that I'm blogging it so I have a record of it when I need it in the future.

You know how you can test a webserver by opening a telnet connection to port 80?  Well by the magic of <a href="http://www.openssl.org/" class="external">OpenSSL</a> you can do the same thing on port 443.</p>

<p>
<samp>
openssl s_client -connect <em>example.com</em>:443 -state
</samp>
<br/>
Then you just type away the same as if it was a normal telnet session to port 80, i.e.<br/>
<samp>
GET /some/url HTTP/1.0<br/>
Host:example.com<br/>
<br/>
<em>server response here...</em>
</samp>

</p>
