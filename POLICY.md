This is a vulnerability disclosure program for all of my personal projects and code that I publish.

# ⏳ Disclosure Policy

I will investigate legitimate reports and make every effort to quickly resolve any vulnerability. To encourage responsible reporting, I will not take legal action against you nor ask law enforcement to investigate you providing you comply with the following guidelines:

* Let me know as soon as possible upon discovery of a potential security issue, and I will make every effort to quickly resolve the issue.
* Provide me a reasonable amount of time to resolve the issue before any disclosure to the public or a third-party.
* Make a good faith effort to avoid privacy violations, destruction of data, and interruption or degradation of my services.

# 📋 Process

{F241462}

# 🔍 In-scope

All projects listed in the "In Scope" section at the very bottom of this page are in scope. **Please always verify that the security.txt file points to this page.** If it doesn't then that project does not belong to me.

```
$ curl http://example/.well-known/security.txt
# This project is in scope!
Contact: https://hackerone.com/ed
```

# 🚩 Targets of interest

I plan on using https://gitalk.github.io/ on https://edoverflow.com/ to allow readers to comment on posts, but before pushing the comment section to production, I have set up a test environment for you to play around with at http://doesfranshaveashell.com/test/. The comment section supports [Markdown](https://daringfireball.net/projects/markdown/) and also requires a GitHub secret token to be embedded in the source code\*. If you are able to trigger XSS or bypass the callback URL in the OAuth flow (currently set to `http://doesfranshaveashell.com/test`) for that comment section, these would be valid issues and could potentially have a high impact. Please do not spam the comment section with XSS payloads, instead edit your comment for each payload or set up https://gitalk.github.io/ locally and try to inject web script there. On top of that, please keep in mind that http://doesfranshaveashell.com/test/ has a fairly strict [Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP), therefore in order to demonstrate the impact of the issue, you should attempt to bypass that policy too.

```
default-src 'self'; 
script-src 'self' ajax.googleapis.com code.jquery.com cdnjs.cloudflare.com; 
connect-src 'self' api.github.com cors-anywhere.herokuapp.com; 
style-src 'unsafe-inline'; 
img-src *; 
font-src *; 
upgrade-insecure-requests; 
reflected-xss block; 
require-sri-for script;
```

{F242009}
{F242010}

\* It is important to note that [GitHub advises not to hardcode the client secret](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/), but the callback URL has been set to http://doesfranshaveashell.com/test, which should ensure that requests are only initiated by that website. If you are able to bypass this or believe that this is still an issue, please report it.

# ⚠️ Exclusions

The following **test types** are excluded from the scope:

* Findings from physical testing such as office access (e.g. open doors, tailgating).
* Findings derived primarily from social engineering (e.g. phishing, vishing).
* Findings from applications or systems not listed in the "Scope" section. **I do accept high-severity issues on out of scope assets if they directly affect me.**
* Vulnerability reports with video only PoCs.
* Reports that state that software is out of date or vulnerable without a proof of concept.
* Highly speculative reports about theoretical damage. Be concrete.
* Vulnerabilities as reported by automated tools without additional analysis as to how they’re an issue.
* Issues in third-party services should be reported to the respective team.

The following **issue types** are excluded from scope:

| Description | Reason |
|-------------|--------|
| Network-level Denial of Service (DoS/DDoS) vulnerabilities. | I do not want you to disrupt any of my services and to be honest with you if I want to take down a service I will always find a way. |
| Low severity issues that can be detected with tools such as [Hardenize](https://www.hardenize.com/) and [Security Headers](https://securityheaders.io/). | I run regular scans with these services and try to improve my score gradually. |
| Content injection issues. | The severity of this issue is so low that it does not warrant a report. |
| Cross-site Request Forgery (CSRF) with minimal security implications (Logout CSRF, etc.). | In order for CSRF to be a valid issue it must affect some important action such as deleting one's account. |
| Missing cookie flags on non-security-sensitive cookies. | These type of issues do not present a major risk and are usually picked up by scanners. |
| UI and UX bugs (including spelling mistakes). | No comment. |
| 401 injection. | This is usually an accepted risk.  |
| Stack traces that disclose information. | Most of my projects are open-source therefore this information is usually public knowledge. **That said, if you discover a stack trace that discloses information which is not located in my GitHub repositories, please do submit a report.** |
| Host header issues without an accompanying proof-of-concept demonstrating vulnerability. | PoC or GTFO. |
| Open ports without an accompanying proof-of-concept demonstrating vulnerability. | Same as above. |
| Banner grabbing issues (figuring out what web server I use, etc.). | I will happily share what web servers I am running. |
| Missing `X-Frame-Options` header (Clickjacking) | The lack of `X-Frame-Options` does not always indicate that a security vulnerability is present. This is an optional header that is only necessary on endpoints where there UI is rendered to invoke state changing actions. I recommend reading this informative post by David Ross: https://plus.google.com/u/0/+DavidRossX/posts/jVrtTRd5yKP |
| Proving me wrong on Twitter. |  |

# 📎 Proof of concepts

| Issue type | When to report the issue |
|------------|--------------------------|
|  XSS      |     For XSS, a simple `alert(document.domain)` should suffice. Bonus points for `alert('🐸')`. |
|  RCE     |  Please only execute harmless code. Simply printing something or evaluating an expression should be enough to demonstrate the issue.  |
|   SQLi         |   Report it as soon as you have a SQL error that indicates SQL injection or you are able to disclose the SQL server's version number.       |
| Unvalidated redirect | Set the redirect endpoint to http://example.com. |
| Information disclosure | If your report contains sensitive data, please use my [PGP key](https://keybase.pub/edoverflow/pgp_key.asc) to encrypt it. |
| CSRF | Either attach a file to demonstrate the issue or paste the code in a code block in your report. |
| SSRF | Do not go playing around on any internal networks. Leave the fun bit to me. |

# 📝 Advice

* I encourage hackers to read [Web Hacking 101](https://leanpub.com/web-hacking-101) and [Breaking into Information Security: Learning the Ropes 101](https://leanpub.com/ltr101-breaking-into-infosec) to get a good idea of the type of issues that I am looking for.
* If you have a question, please do not hesitate to include it in the report. I am always here to help. You may also contact me directly via [Twitter DMs](https://twitter.com/EdOverflow) or [Keybase](https://keybase.io/edoverflow). If your messages contain sensitive information, I would prefer you use the latter.

# 🍺 Rewards

I am not currently offering financial rewards as my software is free and open-source, but if we ever meet in person drinks are on me. For every valid report that I receive I plan on giving a little piece of bug bounty advice that might help the researcher in the future. Please note that this section may change in the future.

{F240600}

# 🔑 Keyword

To prove that you have read and understood these rules, please include the keyword `frog` somewhere in your report.

Thank you for helping me keep my projects safe!

---

# Footnotes

[1] Cover image is by [Igor Ovsyannykov](https://unsplash.com/@igorovsyannykov).
