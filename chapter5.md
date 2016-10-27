# easywebexample (1)

 This section will describe basic configuration for EasyWeb in **web.xml** file.
 When we need used EasyWeb framework in our project, we should configure it in **web.xml** file, make it enabled.
 
 ### Add servlet container listener
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

### Add core servlet and mapping

 ```xml
 <web-app>
   ...
  <servlet>
    <servlet-name>easyweb</servlet-name>
    <servlet-class>com.openthinks.easyweb.EasyWebDispatcher</servlet-class>
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>easyweb</servlet-name>
    <url-pattern>*.do</url-pattern>
  </servlet-mapping>
  <servlet-mapping>
    <servlet-name>easyweb</servlet-name>
    <url-pattern>*.htm</url-pattern>
  </servlet-mapping>
   ...
 </web-app>
 ```
 
This core servlet will take charge of all the HTTP requests those mapping to this servlet, so this servlet is the entry for the framework.

**NOTE**
Here the url-patterns for this core servlet mapping are suffixation format; this style is normal and recommend, with this style, you should configure your project on configureClass 

