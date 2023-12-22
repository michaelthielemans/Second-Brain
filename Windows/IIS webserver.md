#windows 

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

the location where the cert will be stored.

## HSTS

Strictly force users to connect over https.

it can be enable on the IIS server.
#### max age

this parameter is send to the browser so the browser caches how long he only should use httpshow long the site is available

# CSP
content security protocol

prevents cross-site scripting (XSS)
In IIs -> http response header

