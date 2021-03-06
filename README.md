These are documents helping myself to better understand and remember the
various topics i am concerned with in my daily work.
As well as serve as reference and act as
"fantastic but to long to read again and again"
kinda repository.

# General

> Collection of general information, information scientist should be aware of

- [Latency numbers](https://github.com/SebastianGlonner/docs/blob/master/general/latency_numbers.md)

# CheatSheets

> Collection of CheatSheets / Summaries / References about various topics

- [css-projects](https://github.com/SebastianGlonner/docs/blob/master/cheatsheets/css-projects.md)
- [js-performance](https://github.com/SebastianGlonner/docs/blob/master/cheatsheets/js-performance.md)
- [unit tests](https://github.com/SebastianGlonner/docs/blob/master/cheatsheets/unit-tests.md)

# Guidelines

> Collection of complete Guideline about various topics

- [css](https://github.com/SebastianGlonner/docs/blob/master/guidelines/css.md)

# Why

> A set of documents explaining why you should go for various topics.
Or helping to explain yourself to others.

- [Guidelines](https://github.com/SebastianGlonner/docs/blob/master/why/css.md)
- [Unit Tests](https://github.com/SebastianGlonner/docs/blob/master/why/unit-tests.md)

# Security

### General Security Things

* ALWAYS sanitize user input. NEVER asume users input can be trusted.

### SSL / Certificates

* StartCom (StartSSL) and WoSign are considered untrusted by Chrome, Safari and Firefox. Dont buy these certificates. [@see this link](https://ma.ttias.be/despite-revoked-cas-startcom-wosign-continue-sell-certificates/)


### "Growing" list of security issues, information scientists should be aware of

- [XSS - Cross-Site Scripting](https://en.wikipedia.org/wiki/Cross-site_scripting)
- [CSRF - Cross-site request forgery](https://en.wikipedia.org/wiki/Cross-site_request_forgery)
- [JSON Vulnerability](http://haacked.com/archive/2008/11/20/anatomy-of-a-subtle-json-vulnerability.aspx/)
- [Session fixation](https://en.wikipedia.org/wiki/Session_fixation)
- [HTTP response splitting](https://en.wikipedia.org/wiki/HTTP_response_splitting)
- [Directory traversal attack](https://en.wikipedia.org/wiki/Directory_traversal_attack)
- [target=_blank + rel=noreferrer|noopener](https://mathiasbynens.github.io/rel-noopener/)

### Worth reading for any project/language:

- [Wordpress Data Validation](https://codex.wordpress.org/Data_Validation)

### PHP comparison "glitches" you should know: 
```php 
1 == '1 malicious string'; // => true - use strict comparison
in_array('1 malicious string', [1, 2]) // => true - use strict mode in_array($str, $arr, true)

// switch does lose comparison!
switch('1 aml') {
	case 1: echo "true"; break; // => true 
}

// better:
$test = '1 aml';
switch(true) {
	case 1 === $test:
		echo "true";
	break;
}

