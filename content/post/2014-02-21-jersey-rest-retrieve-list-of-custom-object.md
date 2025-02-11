+++
title = "Jersey REST retrieve List of custom object"
slug = "2014-02-21-jersey-rest-retrieve-list-of-custom-object"
published = 2014-02-21T01:30:00.001000-08:00
author = "Pandurang Patil"
tags = ["jersey", "REST"]
+++
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">It
took me while to understand how one require to  retrieve generic object
from ClientResponse.</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">I had
an array of objects in Json format as a response of an REST api, which I
was trying to deserialize it into List&lt;CustomObject&gt;
refer.</span>  
  

       ClientResponse rsp = webresource.path(id.toString()).type(MediaType.APPLICATION_JSON).get(ClientResponse.class);
        List<CustomObject> list = rsp.getEntity(new GenericType<List<CustomObject>>(CustomObject.class));

  
  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">But I
kept on getting following Error:</span>  
  

    Caused by: org.codehaus.jackson.map.JsonMappingException: Can not deserialize instance of test.CustomObject out of START_ARRAY token
     at [Source: sun.net.www.protocol.http.HttpURLConnection$HttpInputStream@3488b1e6; line: 1, column: 1]
        at org.codehaus.jackson.map.JsonMappingException.from(JsonMappingException.java:163)

  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Issue
got solved with following way</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>  

       ClientResponse rsp = webresource.path(id.toString()).type(MediaType.APPLICATION_JSON).get(ClientResponse.class);
        List<CustomObject> list = rsp.getEntity(new GenericType<List<CustomObject>>(){});

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>
