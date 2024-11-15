Reflected Cross-Site Scripting (XSS) is a type of security vulnerability commonly found in web applications. It occurs when an attacker injects malicious code (typically JavaScript) into a website, and that code is "reflected" off the web server and executed in a user's browser. This allows the attacker to manipulate the user's browser in harmful ways, such as stealing sensitive information (like cookies or session tokens), impersonating the user, or performing unauthorized actions on their behalf.

### How Reflected XSS Works

Here's a basic breakdown of how a reflected XSS attack works:

1. **Injection of Malicious Script**: The attacker crafts a URL containing malicious script code. This URL typically targets a vulnerable web page that reflects parts of the URL or query parameters back to the user without properly sanitizing them.

2. **User Interaction**: The attacker persuades a victim to click on the malicious link, often by disguising it as a legitimate link (e.g., sending the link in an email or embedding it in a different website).

3. **Server Reflects the Script**: When the victim clicks on the link, the vulnerable web application includes the attacker’s script in the page response, "reflecting" it back to the user.

4. **Execution in Browser**: The victim’s browser receives the response from the server and executes the reflected script. Since the script is executed in the context of the legitimate website, it can access cookies, session tokens, or other sensitive information associated with that site.

5. **Impact on the Victim**: The attacker can use the script to steal the victim’s information, impersonate the user, or modify the content displayed in the browser.

### Example of Reflected XSS

Consider a search functionality on a website that takes a search term from the URL as a parameter and then reflects it in the page response, like so:

1. **URL Example**:
   ```
   https://vulnerable-site.com/search?query=<script>alert('XSS')</script>
   ```

2. **How the Attack Works**:
   - In this example, the attacker crafts a URL where the `query` parameter includes a malicious script (`<script>alert('XSS')</script>`).
   - When a user visits this URL, the page processes the `query` parameter and reflects it back into the HTML response.
   - If the site doesn't sanitize the input, the `<script>` tag is directly rendered on the page, causing the browser to execute it.

3. **Result**: This specific example would trigger an alert in the user's browser with the text “XSS,” indicating that the script was executed successfully. In a real attack, the script might steal cookies or perform other malicious actions instead of displaying an alert.

### Preventing Reflected XSS

To protect against reflected XSS vulnerabilities, developers should:

1. **Escape/Sanitize User Inputs**: Properly escape or sanitize any user-provided input before reflecting it in the HTML response. This can prevent malicious scripts from being injected into the page.

2. **Use Content Security Policy (CSP)**: Implementing a CSP can restrict the execution of scripts to only those explicitly allowed by the policy, making it harder for injected scripts to run.

3. **Use Secure Development Libraries and Frameworks**: Libraries such as OWASP’s AntiSamy, or frameworks that automatically handle escaping (like React or Django), can reduce the risk of XSS.

4. **Enable HTTP-only Cookies**: Mark cookies as HTTP-only so they cannot be accessed via JavaScript, reducing the risk of cookie theft.

5. **User Education and Awareness**: Since social engineering often plays a role in XSS attacks, educating users to avoid clicking suspicious links can also help limit the effectiveness of reflected XSS attacks.

### Conclusion

Reflected XSS is a common and potentially severe web security issue, as it exploits user interactions with a website to inject and execute malicious code in their browsers. Proper input validation, escaping, and security policies are key defenses against it.




## Reflected cross-site scripting

Reflected XSS is the simplest variety of cross-site scripting. It arises when an application receives data in an HTTP request and includes that data within the immediate response in an unsafe way.

Here is a simple example of a reflected XSS vulnerability:

```
https://insecure-website.com/status?message=All+is+well. <p>Status: All is well.</p>
```

The application doesn't perform any other processing of the data, so an attacker can easily construct an attack like this:

```
https://insecure-website.com/status?message=<script>/*+Bad+stuff+here...+*/</script> <p>Status: <script>/* Bad stuff here... */</script></p>
```

If the user visits the URL constructed by the attacker, then the attacker's script executes in the user's browser, in the context of that user's session with the application. At that point, the script can carry out any action, and retrieve any data, to which the user has access.