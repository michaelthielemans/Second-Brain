#windows 

# Path of default site
` \initpub\wwwroot\start.html
http://localhost:80

# Bindings

Bind a webpage/webapplication to a url and/or port.
# https config
## Certificate request

The common name is the exact name of the server
### Cryptographic service provider
A provider is a 'template' of how the cryptographic key should be created.
	- how to exchange keys
	- which diffie-hellman group
	- which hashing 
	- which aes
	- ........
	- 

default available providers in windows.
RSA
DH

bitlength 1024
## Signing the request

make sure to select the webserver certificate template
-> this is needed because otherwise it will not show up in the iis to select.
--> IIS only sees webserver certificates that are available in the cert store.
# certificate
when importing a certificate you can add a friendly name to it in order to make it easier to manage.
### Certificate store

The location where the cert will be stored.

## HSTS - HTTP Strict Transport Security

Strictly force client browsers to connect over https.
It can be enable on the IIS server.

The http response header includes the "Strict-Transport-Security" along with a "max age". The browser receives the header, and memorizes the HSTS policy for the number of seconds specified by the “max-age” directive. So within the "max age" time frame the browser will automatically redirect all request to HTTPS. ( even if the user enters http://)
#### max age

This parameter is send to the browser so the browser caches how long he only should use https.

## CSP
The Content Security Policy header implements an additional layer of security. This policy helps prevent attacks such as Cross-Site Scripting (XSS) and other code injection attacks by limiting content sources that are approved and thus permitting the browser to load them.

This uses the whitelisting method which tells the browser from where to fetch the images, scripts, CSS, etc.

