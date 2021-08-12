## Make your website secure (https) for free!

First get a Free SSL Certificate for your website 

- Go to https://www.sslforfree.com/
- Add your domain — eg Codecloudservices.com
- Click create free ssl certificate
- Create an account and follow instructions
- select 90 day validity — Remember to renew this every 90days
- verify with email address and code, you should get an email
- open email and validate with opening url and pasting code from email
- go back to zerossl
- Download all certificates

Add your ssl to your web server. Below is instructions for cPanel
- Go to ssl certificates
- Click manage ssl certificates
- Open your certifications that you downloaded
- Open all certificates that you downloaded in notepad
- Copy and paste the values according to what is required by your cpanel
- click install certificate
- you should get a success message

Make your website forward to https automaticly
- Modify your htaccess to forward http to https — see other our other article for this
- Test connection in zero ssl
- Test all connections in browser

Below are wordpress related issues I had

If you get an error with images being not secure
- Save all images from media library
- edit http to http as below

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1624621081705/0V8kTpDyK.png)

- Re add images
- check when adding images to media library that it doesnt change back to http

Test all your pages and whether every page is secure


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1624621033819/DRiPSfqmX.png)

Hope this solution works well for you.
Please get in contact with if you need assistance.

Happy Coding,
Asrin
