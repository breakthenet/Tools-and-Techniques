http://blog.gosecure.ca/2016/04/27/binary-webshell-through-opcache-in-php-7/

First, we must obtain the location of the cache folder ( /tmp/opcache/[system_id]) and the location of the targeted PHP file ( /var/www/...).

For the sake of simplicity, let’s assume that the website has left a phpinfo() file, from which we can obtain the cache folder location, the file source code location, and all the fields necessary to calculate the system_id.

(There exists a tool which calculates the system_id  from a website’s phpinfo(). You can find it this GitHub repository here https://github.com/GoSecure/php7-opcache-override)

It is important to note that the targeted website must also be vulnerable to unrestricted file upload.

...