---
layout: post
title: Securing Web Applications with Grails
categories:
- Articles
tags:
- Web Security, Injection, XSS, XSRF, Authentication, Session Management, Encryption, Misconfiguration, URL Access, Unvalidated redirects
status: publish
type: post
published: true 
meta:
  _publicize_pending: '1'
author: Sathish Hariharan
---

As web applications become more complex by the day, security becomes an important aspect to consider during development.
One way to address the variety of security loopholes in the system is to follow a check-list based approach. Look at the
top 10 vulnerabilities web apps face today and address each one of these individually. OWASP (The Open Web Application
Security Project) provides a list of **top 10 security flaws that web applications face [here](https://www.owasp.org/index.php/Top_10_2013-Top_10)**.
Addressing these flaws will help applications reduce a significant percentage of attacks. The list of attacks and the facilities Grails provide to
counter these flaws is discussed by Burt Beckwith in his book [Programming Grails](http://www.amazon.com/gp/product/1449323936/ref=s9_psimh_gw_p14_d0_i1?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=center-2&pf_rd_r=0V1S7N5XDS49SC24MCXB&pf_rd_t=101&pf_rd_p=1688200342&pf_rd_i=507846)
A summary of the discussion is provided below.

**Injection (SQL / Javascript) :**  where a text input field is used to enter code (SQL or Javascript) that can compromise the application.
  Grails is mostly immune to this because most of ths queries are converted to Hibernate criteria queries (which uses PreparedStatement with parameter
  holders, and this escapes any injected code). In case you use HQL, care should be taken to avoid injection. Another possible injection vulnerability is if you use
  groovy command execution in the backend. So one needs to take care of escaping these scenarios.

**Broken Auth / Sessions :** where incorrect implementation of authentication and session management is taken advantage to compromise passwords, keys, or session tokens
  The simple solution to this is to use a library that implements authentication and session management. Grails uses the Spring-Security library and
  provides a plugin to integrate it easily into your web application. Just make sure the following parameters are set correctly
    - grails.views.enable.jsessionid = false
    - grails.plugins.springsecurity.useSessionFixationPrevention = true
    - make sure to use encodeURL instead of encodeRedirectURL if you are creating redirect URLs

**XSS (Cross site scripting) :** where untrusted data (using injection) is sent to browser (javascript code executed in place of data)
Setting
    grails.views.default.codec = "html"
allows automatic escaping of input data. But this is not fool-proof. Also make sure you don't use the following Groovy server pages technique for writing to
output which directly writes to output stream.
    <%=person.name%>

**Insecure Direct object references :** where urls point to internal objects and changing a url with a different parameter could provide access to unauthorized data.
In Grails this can be avoided by using Spring security authentication - get the appropriate user id in the server and use that to retrieve further
references instead of having them in the client. Another option would be to use ACLs, but this is more cumbersome

**Mis-configured security :** such as not using correct algorithms, not enabling SSL, etc. Grails does not have any explicit way to automate away misconfiguration

**Failure to restrict URL access :** The Spring Security plugin offers three approaches to guarding URLs: annotations,
database “requestmaps,” and a simple mapping of URLs and their required roles. In addition, there is a “strict” mode
option where URLs that do not have explicit access rules defined are blocked. Enabling this is simple, just a single line
in Config.groovy:
    grails.plugins.springsecurity.rejectIfNoRule = true

**Insufficient Transport Layer Protection :** One of the easiest ways to do this is to use SSL for your web traffic.
Although there is a small cost to using SSL due to the processing work encrypting the
pages, you should consider using SSL for the entire site. Then, everything is transmitted
securely and the data is significantly less likely to be accessed by attackers.
The certificate should use strong encryption, with a key size of at least 128 bits.

**CSRF :** A cross-site request forgery (CSRF) attack is similar to an XSS attack. An attacker will
often use XSS vulnerabilities to create pages that make requests on the behalf of other
users and send personal information, cookies, or session IDs to the attacker’s server, or
perform some action on behalf of the user. The first line of defense against CSRF attacks is to ensure that XSS attacks
are not possible.

The best way to defeat CSRF attacks is to generate a token for each clickable URL (appended
to the href) and form (using an <input type='hidden'> tag), and verify the token at the server. If a request is made
(either a GET or a POST), and there is no token or it’s not valid, the action is blocked. As long as the value is unique
and generated for each request, even if an attacker accesses someone else’s valid token, it won’t be usable,
because it is only valid for that user. The easiest way to implement this is to use grails HDIV plugin

**Using insecure cryptographic storage :** Storing data requires good libraries for Hashing and Encryption.
Passwords are typically hashed. There is rarely a need to decrypt a password stored in a database, because during
authentication, you merely need to hash the user’s supplied password and compare it with the previously hashed value.
MD5, and SHA-1 are popular algorithms but recent advances in computing have made it easy to break these.
One should prefer SHA-256 or SHA-512 for hashing. The best choice is Bcrypt where you can specify number of hash iterations.
Adding a "salt" to hashing makes it more robust.

The Jasypt library is an excellent tool to avoid having to deal with the implementation
details of encrypting data, and there’s even a Grails plugin for it: the [jasyptencryption plugin](http://grails.org/plugin/jasypt-encryption).

**Unvalidated redirects :** Redirecting or forwarding users to other URLs exposes them to being taken
advantage of by attackers by taking advantage of some XSS exploit. One way to deal with this
is to use server side redirects which cannot be exploited. Another way to address this specific to
grails is to use the 'flash' scope.







