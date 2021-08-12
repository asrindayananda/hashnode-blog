## How to forward http to https with .htaccess file

Below is instructions for linux based hosting with a wordpress installation.

- Log into your hosting where you edit your files

- Find and Open your .htaccess file

- Between this statement


```
<IfModule mod_rewrite.c>
..
</IfModule>
``` 

- Add these three lines of code (if any of theses lines appear don’t re add them)


```
RewriteEngine On
RewriteCond %{SERVER_PORT} 80
RewriteRule ^(.*)$ https://example.com/$1 [R=301,L]
``` 

- Change https://example.com/ to your website domain

- Open your page in private browsing htttp should forward to https

- Hope this solution worked for you!

- If this didn't please comment and I will try help you.

- Remember to like, post a comment and share this blog if this worked for you. 

Happy Coding :)

Asrin






**References**

- Image from https://www.serif.net/serif-news/title/Should-you-run-your-website-securely-on-https-with-an-SSL-certificate/post/11147