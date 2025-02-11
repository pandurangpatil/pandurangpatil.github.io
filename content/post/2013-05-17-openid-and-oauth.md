+++
title = "OpenID and OAuth"
slug = "2013-05-17-openid-and-oauth"
published = 2013-05-17T05:29:00.001000-07:00
author = "Pandurang Patil"
tags = [ "Identity", "openId", "Oauth",]
+++

First of all OpenID and OAuth are two different standards don't mix them
together.  
  
**OpenID** is only limited to authenticate the end user i.e. getting user
authenticated from the third party provider like Google, Yahoo etc.

Following are the benefits   


-   End user don't have to remember another credentials for your site.
    They will be able to authenticate themself with their existing
    registered account with any of the third party service provider.
-   Along with that it also gives you advantage of Single Sign on for
    your site.

  
**Oauth** provides way to authenticate (Authenticate with Oauth 2.0) the end
user as well as, provides a mechanism to get end user's authorization to
access his / her data with the given provider.


**Comparison:**

Both are different standars targeted to solve different problems. **OpenId** is targeted to get
authentication done from third party service rather than having own
system for the same. One can support multiple third service providers
for authenticating user's with openId on their site.

Where as **Oatuh** is targeted to get user's authorization (for
you application / site) to access his / her data from given service
provider using respective api, exposed by same service provider.
