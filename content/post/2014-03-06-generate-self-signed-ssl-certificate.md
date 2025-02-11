+++
title = "Generate self signed SSL certificate"
slug = "2014-03-06-generate-self-signed-ssl-certificate"
published = 2014-03-06T04:16:00.001000-08:00
author = "Pandurang Patil"
tags = [ "SelfSigned", "SSL",]
+++
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Follow
below steps to generate self signed certificate:</span>  

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">1.
You need to first generate your own private key.</span>

    $ openssl genrsa -des3 -out server.key 1024

    Generating RSA private key, 1024 bit long modulus
    .......................++++++
    .......++++++
    e is 65537 (0x10001)
    Enter pass phrase for server.key:
    Verifying - Enter pass phrase for server.key:

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">With
above command it will generate private key, while doing that it will ask
you to enter pass phrase which will make this private key useful who
knows this pass phrase. This will generate the private server key
"server.key".</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">2.
Then you need to generate Certificate Signing Request.</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>  

    $ openssl req -new -key server.key -out server.csr

    Enter pass phrase for server.key:
    You are about to be asked to enter information that will be incorporated
    into your certificate request.
    What you are about to enter is what is called a Distinguished Name or a DN.
    There are quite a few fields but you can leave some blank
    For some fields there will be a default value,
    If you enter '.', the field will be left blank.
    -----
    Country Name (2 letter code) [AU]:IN
    State or Province Name (full name) [Some-State]:Maharashtra
    Locality Name (eg, city) []:Pune
    Organization Name (eg, company) [Internet Widgits Pty Ltd]:Pandurang Patil Pvt. Ltd.
    Organizational Unit Name (eg, section) []:Pune
    Common Name (e.g. server FQDN or YOUR name) []:www.pandurangpatil.com    
    Email Address []:mail@pandurangpatil.com

    Please enter the following 'extra' attributes
    to be sent with your certificate request
    A challenge password []:
    An optional company name []:

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Here
you need to enter required details, you can refer above request output.
You may chose to skip last to questions. This step will generate the
certificate signing request server.csr. </span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">3. To
self sign the certificate we need to create signing certificate as well
(that is your own CA certificate). For that you need to first create
private key for CA.</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>  

    $ openssl genrsa -des3 -out ca.key 1024
    Generating RSA private key, 1024 bit long modulus
    .......................++++++
    .......++++++
    e is 65537 (0x10001)
    Enter pass phrase for ca.key:
    Verifying - Enter pass phrase for ca.key:

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span><span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">This
private key pass phrase will be required to be used while signing the
Certificate Signing Request.</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">4.
Now we have to generate CA certificate</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>  

    $ openssl req -new -x509 -days 365 -key ca.key -out ca.crt

    Enter pass phrase for ca.key:
    You are about to be asked to enter information that will be incorporated
    into your certificate request.
    What you are about to enter is what is called a Distinguished Name or a DN.
    There are quite a few fields but you can leave some blank
    For some fields there will be a default value,
    If you enter '.', the field will be left blank.
    -----
    Country Name (2 letter code) [AU]:IN
    State or Province Name (full name) [Some-State]:Maharashtra
    Locality Name (eg, city) []:Pune
    Organization Name (eg, company) [Internet Widgits Pty Ltd]:Pandurang Patil CA
    Organizational Unit Name (eg, section) []:Pune
    Common Name (e.g. server FQDN or YOUR name) []:www.pandurangpatil.com
    Email Address []:mail@pandurangpati.com

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span><span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">5.
Now we have to sign .csr request that we have generated in step 2. For
that we need to provide .conf file through which utility will take
required inputs. Somebody has created [<span
id="goog_763260983"></span>this<span
id="goog_763260984"></span>](http://www.opensource.apple.com/source/apache/apache-683/mod_ssl/pkg.contrib/sign.sh)
nice script which will automate next steps to sign .csr request. You can
download this .sh file on your machine, I am assuming it will be saved
on sign.sh at the same location from where you are executing above
commands. Make this sign.sh executable.</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>  

    $ ./sign.sh server.csr

    CA signing: server.csr -> server.crt:
    Using configuration from ca.config
    Enter pass phrase for ./ca.key:
    Check that the request matches the signature
    Signature ok
    The Subject's Distinguished Name is as follows
    countryName           :PRINTABLE:'IN'
    stateOrProvinceName   :PRINTABLE:'Maharashtra'
    localityName          :PRINTABLE:'Pune'
    organizationName      :PRINTABLE:'Pandurang Patil Pvt.Ltd.'
    organizationalUnitName:PRINTABLE:'Pune'
    commonName            :PRINTABLE:'www.pandurangpatil.com'
    emailAddress          :IA5STRING:'mail@pandurangpatil.com'
    Certificate is to be certified until Mar  6 09:52:59 2015 GMT (365 days)
    Sign the certificate? [y/n]:y


    1 out of 1 certificate requests certified, commit? [y/n]y
    Write out database with 1 new entries
    Data Base Updated
    CA verifying: server.crt <-> CA cert
    server.crt: OK

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">While
signing you need to enter pass phrase for ca.key and confirm the
details. This step will generate "server.crt". This way you have your
private key "server.key" and self signed certificate "sever.crt"
generated.</span>

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>
