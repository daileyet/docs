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
 This listener class will loaded when servlet container(Tomcat/Jetty) startup, and initialize EasyWeb framework ： 
 1. initialize and instance WebContext
 2. call Bootstarp#initial() if configured in WebContext
 3. initialize WebContainer and build request mapping for WebControllers and WebFilters
