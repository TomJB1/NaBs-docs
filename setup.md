Note: this hasn't really been tested yet

## What you need
A server with:
  - PHP
  - SQLite
  - Any Web server software, such as apache or lighttpd (testing pending)
  - Lets Encrypt Certbot (optional - for tls (https))

Also:
  - A domain name (can be added later, or get a free subdomain at https://freedns.afraid.org)

## Setting up the web server software
### Set root directory
For lighttpd add this to the config file:
```
server.document-root = "/path/to/news-and-blog-system"
```
and thats it.

For apache find this:
```
#/etc/apache2/sites-available/000-default.conf
DocumentRoot /var/www/html
```
and change it to:
```
#/etc/apache2/sites-available/000-default.conf
DocumentRoot /path/to/news-and-blog-system
```
and also find this1:
```
#/etc/apache2/apache2.conf
<Directory /var/www/html/>
Options Indexes FollowSymLinks
AllowOverride None
Require all granted
</Directory>
```
and change it to:
```
#/etc/apache2/apache2.conf
<Directory /path/to/news-and-blog-system/>
Options Indexes FollowSymLinks
AllowOverride None
Require all granted
</Directory>
```


### Redirecting
Requests need to be redirected to news-and-blog-system/index.php if they aren't a static file.

If you are using apache this is managed by the .htaccess file and you don't need to do anything.

Other web servers will need to be configured to do this. In Lighttpd you can put this in the config file:
``` 
server.modules += ("mod_rewrite")
url.rewrite-if-not-file = (
    rewrite "index.php";
) 
```

### TLS (https)

Run `certbot` and follow the instructions to set up https.

### Next step
[Starting writing](writer/starting.md)
