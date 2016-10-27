# easywebexample (1)

 This section will describe basic configuration for EasyWeb in **web.xml** file.
 When we need used EasyWeb framework in our project, we should configure it in **web.xml** file, make it enabled.
 
 #### Add servlet container listener
 ```xml
 <web-app>
 ...
   <listener>
    <listener-class>com.openthinks.easyweb.context.WebContextLoadListener</listener-class>
   </listener>
 ...
 </web-app>
 ```