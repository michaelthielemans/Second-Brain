Shell injections

When the web application makes use of an external application it is possible to exploit it.

the web application sends parameters to the operating system .
### Blind command injection
the application does not return the output from the command within its http response.
- for example it can be done with email.
- with time delays so you know that the system in vulnerable
- Redirecting the output to a file.
	- & whoami > /var/www/static/whoami.txt &