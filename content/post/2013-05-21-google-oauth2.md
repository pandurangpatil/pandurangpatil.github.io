+++
title = "Google Oauth2"
slug = "2013-05-21-google-oauth2"
published = 2013-05-21T05:55:00-07:00
author = "Pandurang Patil"
tags = ["Google", "Oauth", "Oauth2"]
+++
**Purpose:**  
         To access end user's data through Google Service api's as third
party application. In some case's you may have to make use of Google
Oauth2 for accessing your own data through Google service api e.g.
Google Cloud Storage.  
  
**Setup:** ( You can skip this part if you already know how to setup
client ).  
  
Hit following url <https://code.google.com/apis/console/>. With the
assumption you are doing it first time. Following screenshots will guide
you through the process to setup client. On clicking above url you will
be asked to login with your google account. After login if you are
setting up the client secrets first time you will see below snapshot.  

[![](../images/thumbnails/2013-05-21-google-oauth2-google-oauth2-1.png)](../images/2013-05-21-google-oauth2-google-oauth2-1.png)

When you click on "Create Project". It will setup a project for you,
though which you can enable / disable different Google Service which you
want to access through your application. 

  

[![](../images/thumbnails/2013-05-21-google-oauth2-google-oauth2-2.png)](../images/2013-05-21-google-oauth2-google-oauth2-2.png)

  
With the same project you can access multiple Google service.  
  

[![](../images/thumbnails/2013-05-21-google-oauth2-google-oauth2-3.png)](../images/2013-05-21-google-oauth2-google-oauth2-3.png)

  
You need to setup OAuth 2.0 client ID. Now click on "Create an OAuth 2.0
client ID", it will ask you to add more details about your application,
fill in the required details.  
  

[![](../images/thumbnails/2013-05-21-google-oauth2-google-oauth2-4.png)](../images/2013-05-21-google-oauth2-google-oauth2-4.png)

  
On next screen you need specify Application type, and if application
type is Web Application. You need to provide authorized callback
redirect URIs, you can specify multiple URIs. You can specify required
call back url at run time.  
  

[![](../images/thumbnails/2013-05-21-google-oauth2-google-oauth2-5.png)](../images/2013-05-21-google-oauth2-google-oauth2-5.png)

  

At the end you have Client Id setup for your application, which you can
use to access Google service api.

  

[![](../images/thumbnails/2013-05-21-google-oauth2-google-oauth2-6.png)](../images/2013-05-21-google-oauth2-google-oauth2-6.png)
