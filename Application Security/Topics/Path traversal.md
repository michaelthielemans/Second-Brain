
when a webserver stores it images at /var/www/images it might be possible to enter a new path:
filename=/var/www/images/../../../etc/passwd

### The null byte
%00

When using the null byte?
If there is an extension checker for example the webapplication will only show .png files, you are not able to open a .txt file , unless you make use of the null byte

name_of_the_file.txt%00.png

the webserver will check that it is indeed a png file. the operating system running the webserver will trow away everything behind the null byte so it leaves the .txt file bypassing the extension checker.