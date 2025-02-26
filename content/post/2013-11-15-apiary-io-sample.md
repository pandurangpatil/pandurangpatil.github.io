+++
title = "apiary.io sample "
slug = "2013-11-15-apiary-io-sample"
published = 2013-11-15T05:06:00-08:00
author = "Pandurang Patil"
tags = [ "apiary", "documentation", "api"]
+++
First of all I must mention `apiary.io` has done great job by providing some easy means to have `REST` api documentation, collaborate as well as expose it to public or keep it private. With the new release of the same I was struggling little bit to make use of the new version, for that I had to go through the detailed documentation ([refer](http://apiary.io/blueprint)). But I felt this tutorial just demonstrates blueprint code, it doesn't show the corresponding preview related to given blueprint code. I had to invest some time to figure out what code generate which effect. So I have created one sample blueprint for which you can refer the code below and result of the same http://docs.pandurangpatil.apiary.io/. For more details [refer](http://apiary.io/blueprint) api tutorial , one can add more styling in documentation using [markdown](http://whatismarkdown.com/), for more help on markdown [refer](http://daringfireball.net/projects/markdown/syntax). 
  

     FORMAT: 1A  
     HOST: http://sample.pandurangpatil.com  
       
     # Sample API Documentation  
     Sample api documentation for sample project.  
       
     # Allowed HTTPs requests:  
     <pre>  
     PUT   : To create resource   
     POST  : Update resource  
     GET   : Get a resource or list of resources  
     DELETE : To delete resource  
     </pre>  
       
     # Description Of Usual Server Responses:  
     - 200 `OK` - the request was successful (some API calls may return 201 instead).  
     - 201 `Created` - the request was successful and a resource was created.  
     - 204 `No Content` - the request was successful but there is no representation to return (i.e. the response is empty).  
     - 400 `Bad Request` - the request could not be understood or was missing required parameters.  
     - 401 `Unauthorized` - authentication failed or user doesn't have permissions for requested operation.  
     - 403 `Forbidden` - access denied.  
     - 404 `Not Found` - resource was not found.  
     - 405 `Method Not Allowed` - requested method is not supported for resource.  
       
     # Some sample  
       Test sample         |  test column two  
       First column sadf asdfads  |  sfsdsadf  
       
     ---  
       test one          | Another column    
     ---  
       
     # Table sample  
     <table>  
       <tr>  
         <td> First Column </td>  
         <td> Second Column </td>    
       </tr>  
       <tr>  
         <td> First Column </td>  
         <td> Second Column </td>   
       </tr>  
     </table>  
       
       
     # Code Sample  
     <pre>  
       Some code here  
     </pre>  
       
     # Group User  
     Represents user details.   
       
     ---  
     **User attributes:**  
       
     - id `(Number)` : unique identifier.   
     - fname `(String)` : First Name.  
     - lname `(String)` : Last Name.  
     - email `(String)` : email id of the user.  
       
     ---  
     ## User Collection [/users(?since,limit)]  
     ### List all users [GET]  
     Retrieve paginated list of users.  
       
     + Parameters  
       + since (optional, String) ... Timestamp in ISO 8601 format: `YYYY-MM-DDTHH:MM:SSZ` Only users updated at or after this time are returned.  
       + limit (optional, Number) ... maximum number of records expected by client.  
       
     + Response 200 (application/json)  
       
         [  
           {  
             "id": 1,  
             "fname": "Pandurang",  
             "lname": "Patil",  
             "email": "pandurang@email.com"  
           },  
           {  
             "id": 2,  
             "fname": "Sangram",  
             "lname": "Shinde",  
             "email": "sangram@email.com"  
           }  
         ]  
       
     + Response 401 (application/json)  
       
         {  
           "error": "error.unauthorized"  
         }  
       
     ### Create a User [PUT]  
     + Request (application/json)  
       
         {  
           "fname": "Ram",  
           "lname": "Jadhav",  
           "email": "ram@email.com"  
         }  
       
     + Response 201 (application/json)  
       
         {  
           "id": 3,  
           "fname": "Ram",  
           "lname": "Jadhav",  
           "email": "ram@email.com"  
         }  
       
     ## User [/users/{id}]  
     A single User object with all its details  
       
     + Parameters  
       + id (required, Number, `1`) ... Numeric `id` of the User to perform action with.  
       
     ### Retrieve a User [GET]  
     + Response 200 (application/json)  
       
       + Header  
       
           X-My-Header: The Value  
       
       + Body  
       
           {  
             "id": 1,  
             "fname": "Pandurang",  
             "lname": "Patil",  
             "email": "pandurang@email.com"  
           }  
             
     + Response 401 (application/json)  
       
         {  
           "error": "error.unauthorized"  
         }  
       
     ### Update a User [POST]  
     Update user details  
     + Request (application/json)  
       
         {  
           "id": 1,  
           "fname": "Pandurang",  
           "lname": "Patil",  
           "email": "pandurangpatil@email.com"  
         }  
       
     + Response 200 (application/json)  
       
         {  
           "id": 1,  
           "fname": "Pandurang",  
           "lname": "Patil",  
           "email": "pandurangpatil@email.com"  
         }  
       
     + Response 401 (application/json)  
       
         {  
           "error": "error.unauthorized"  
         }  
       
     ### Remove a User [DELETE]  
     + Response 204  
       
     + Response 401 (application/json)  
       
         {  
           "error": "error.unauthorized"  
         }
