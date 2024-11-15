Cross-site scripting is a web security vulnerability that allows an attacker to compromise the interactions that users have with a vulnerable application. It allows an attacker to circumvent the same origin policy, which is designed to segregate different websites from each other. Cross-site scripting vulnerabilities normally allow an attacker to masquerade as a victim user, to carry out any actions that the user is able to perform, and to access any of the user's data. If the victim user has privileged access within the application, then the attacker might be able to gain full control over all of the application's functionality and data.

## What are the types of XSS attacks?

There are three main types of XSS attacks. These are:

- [Reflected XSS](https://portswigger.net/web-security/cross-site-scripting#reflected-cross-site-scripting), where the malicious script comes from the current HTTP request.
- [Stored XSS](https://portswigger.net/web-security/cross-site-scripting#stored-cross-site-scripting), where the malicious script comes from the website's database.
- [DOM-based XSS](https://portswigger.net/web-security/cross-site-scripting#dom-based-cross-site-scripting), where the vulnerability exists in client-side code rather than server-side code.

## XSS between HTML tags

When the XSS context is text between HTML tags, you need to introduce some new HTML tags designed to trigger execution of JavaScript.

Some useful ways of executing JavaScript are:

`<script>alert(document.domain)</script> <img src=1 onerror=alert(1)>`

## XSS in HTML tag attributes

When the XSS context is into an HTML tag attribute value, you might sometimes be able to terminate the attribute value, close the tag, and introduce a new one. For example:

`"><script>alert(document.domain)</script>`

More commonly in this situation, angle brackets are blocked or encoded, so your input cannot break out of the tag in which it appears. Provided you can terminate the attribute value, you can normally introduce a new attribute that creates a scriptable context, such as an event handler. For example:

`" autofocus onfocus=alert(document.domain) x="`

The above payload creates an `onfocus` event that will execute JavaScript when the element receives the focus, and also adds the `autofocus` attribute to try to trigger the `onfocus` event automatically without any user interaction. Finally, it adds `x="` to gracefully repair the following markup.

Cross-Site Scripting (XSS) in HTML tag attributes is a type of vulnerability where an attacker injects malicious scripts into the attributes of HTML tags on a webpage. If this script is executed, it can compromise the security of the website and users' data. Here’s a breakdown of how XSS can happen within HTML tag attributes and what you should be aware of:

### 1. Understanding Attribute-based XSS Injection
In XSS attacks, the goal is to inject JavaScript (or other malicious code) into a page so it runs in the context of the user's browser. In attribute-based XSS, this script is injected into specific HTML tag attributes, such as:
- `src` (for `<img>` or `<iframe>`)
- `href` (for `<a>` tags)
- `onerror`, `onclick`, and other event attributes

When a browser loads this HTML and doesn’t properly sanitize it, the malicious code within these attributes can execute, leading to security breaches.

### 2. Example of an XSS Injection in HTML Attributes
Let’s say a website allows users to add comments, and those comments are rendered without proper sanitization. If an attacker posts something like:

```html
<img src="nonexistent.jpg" onerror="alert('XSS')">
```

This tag includes an `onerror` attribute, which triggers JavaScript when the `src` image cannot load (because it’s nonexistent in this case). When the page displays this comment, the script within `onerror` will execute, displaying an alert.

### 3. How it Works
HTML attributes like `onerror`, `onclick`, and other event handlers are designed to execute JavaScript code in response to user interactions. In XSS attacks, malicious code can be placed inside these attributes to:
- Steal cookies (session hijacking)
- Redirect users to malicious sites
- Log keystrokes or other sensitive actions

### 4. Examples of Common HTML Attributes Targeted by XSS
- **`onload`**: Used with `<body>`, `<iframe>`, `<img>`, etc. Fires when the element loads. E.g., `<body onload="maliciousFunction()">`.
- **`onclick`**: Used on clickable elements to execute code on click. E.g., `<button onclick="maliciousFunction()">`.
- **`href`**: Injected as JavaScript in links, e.g., `<a href="javascript:alert('XSS')">Click me</a>`.
  
### 5. Preventing Attribute-based XSS
To prevent this type of XSS, developers should:
- **Sanitize inputs**: Remove or encode potentially harmful characters in user input, especially in attributes that will be rendered on the page.
- **Avoid inline event handlers**: Instead, use external scripts with event listeners, as they’re harder to manipulate.
- **Set Content Security Policy (CSP)**: A strong CSP can restrict JavaScript execution from unauthorized sources.
- **Use attribute-specific escaping**: Use libraries or frameworks that offer context-sensitive escaping. For instance, escape `&` as `&amp;`, `<` as `&lt;`, and `"` as `&quot;` when outputting user data into HTML attributes.

### Conclusion
Attribute-based XSS is a potent attack vector if user input isn't sanitized in HTML attributes. Always validate and escape user input, avoid inline event handlers, and consider using security headers to mitigate risks associated with XSS.

#### Password lists
rockyou list . is available on kali linux
