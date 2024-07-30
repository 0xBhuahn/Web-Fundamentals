### Cross-Site Scripting (XSS)

Cross-Site Scripting (XSS) is a vulnerability found in web applications that allows attackers to inject malicious scripts inject into webpages viewed by other users. This occurs when a web application includes untrusted data in a web page without proper validation or escaping.

**There are 3 types of XSS**

**Stored XSS:** The malicious script is stored on the server (e.g., in a database) and executed every time a user requests the affected page. **For Example:** An attacker posts a comment on a blog with a script embedded in it. Whenever users view the comment, the script executes, potentially stealing their session cookies.

**Reflected XSS:** The malicious script is embedded in a URL or request and is executed immediately when the server reflects the script back to the user's browser.**For Example:** An attacker sends a link to a user with a script embedded in a query parameter. When the user clicks the link, the script runs in their browser.   
 
**DOM-based XSS:** The vulnerability lies in the client-side code (JavaScript) that processes data from the user without proper sanitization.

**Where are you to Test XSS**  

**1. Input Fields:-**  
- **Search Boxes:** Test search fields where user input is reflected on the results page.  
- **Login/Registration Forms:** Check fields like username, password, and email.  
- **Contact Forms:** Test fields such as name, email, and message.  
- **Comment/Review Sections:** These often allow user-generated content that can be a target for XSS.  
- **Feedback Forms:** Fields where users submit bug reports or suggestions.  
     - **Example:** Parameter: Search  
     **URL:** https://example.com/search?query=
    
**2. URL Parameters:**  
- **Search Queries:** Test parameters used in search functionality.  
- **Filtering Parameters:** Any parameters used to filter or sort data.  
- **Resource Identifiers:** Parameters that identify resources, such as /user/{userId}.  
- **Dynamic Routing:** Parameters used to dynamically generate pages, such as /product/{productId}.  

    - **Example:** Parameter: search  
    URL: https://example.com/search?query=

- **Payloads:**

         Basic Payload: <script>alert('XSS')</script> 
         HTML Encoded: &lt;script&gt;alert(&#39;XSS&#39;)&lt;/script&gt;
         URL Encoded: %3Cscript%3Ealert%28%27XSS%27%29%3C/script%3E
         Image Payload:- <img src="x" onerror="alert('XSS')">
         SVG Payload:- <svg/onload=alert('XSS')>
         



**Prevention/Mitigation**

 - **Input Validation:** Always validate and sanitize user inputs. Use whitelists for acceptable input values.  
- **Output Encoding:** Encode data before including it in HTML, JavaScript, or other contexts to ensure it is treated as data rather than executable code.  
- **Content Security Policy (CSP):** Implement CSP to restrict the sources from which scripts can be loaded and executed.  
- **Use Security Libraries:** Utilize frameworks and libraries that provide built-in protection against XSS attacks.
