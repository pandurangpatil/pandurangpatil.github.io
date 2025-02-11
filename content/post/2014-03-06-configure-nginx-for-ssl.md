+++
title = "Configure Nginx for SSL"
slug = "2014-03-06-configure-nginx-for-ssl"
published = 2014-03-06T04:22:00-08:00
author = "Pandurang Patil"
tags = [ "nginx", "SSL",]
+++
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">You
need to have private key and CA signed certificate (to test you may
generate your own [Self signed
certificate](http://www.pandurangpatil.com/2014/03/generate-self-signed-ssl-certificate.html))
to configure your nginx to serve request over SSL. Add following lines
into your nginx.conf file and make required changes to point
ssl\_certificate to location of your certificate in this configuration
it is "server.crt" (if you copy your .crt and .key file into "&lt;nginx
home&gt;/conf" folder . In that case you can specify only file name
other wise you need to specify absolute path of a file). Change
ssl\_certificate\_key to point your key file.</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Restart
nginx server and hit https url https://yourdomain.com. ( If you have
installed self signed certificate you will see Untrusted Exception. You
can safely continue with it.) </span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>  

        # HTTPS server
        #
        server {
            listen       443;
            server_name  yourdomain.com;

            ssl                  on;
            ssl_certificate      server.crt;
            ssl_certificate_key  server.key;

            ssl_session_timeout  5m;

            ssl_protocols  SSLv2 SSLv3 TLSv1;
            ssl_ciphers  HIGH:!aNULL:!MD5;
            ssl_prefer_server_ciphers   on;

            location / {
                root   html;
                index  index.html index.htm;
            }
        }

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>
