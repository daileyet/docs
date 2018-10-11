# chapter5

This section will describe basic configuration for EasyWeb in **web.xml** file. When we need used EasyWeb framework in our project, we should configure it in **web.xml** file, make it enabled.

## Add servlet container listener

```markup
 <web-app>
   ...
   <listener>
    <listener-class>com.openthinks.easyweb.context.WebContextLoadListener</listener-class>
   </listener>
   ...
 </web-app>
```

This listener class will loaded when servlet container\(Tomcat/Jetty\) startup, and initialize EasyWeb framework ： 1. initialize and instance WebContext 2. call Bootstarp\#initial\(\) if configured in WebContext 3. initialize WebContainer and build request mapping for WebControllers and WebFilters

## Add core servlet and mapping

```markup
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

**NOTE** Here the url-patterns for this core servlet mapping are suffixation format; this style is normal and recommend, with this style, you should configure your project on configureClass

```java
@EasyConfigure
//...
@RequestSuffixs(".do,.htm")
//...
public class EasyWebConfigure {
}
```

## Point your project configure class

```markup
 <web-app>
   ...
  <context-param>
    <param-name>configureClassName</param-name>
    <param-value>com.openthinks.easywebexample.EasyWebConfigure</param-value>
  </context-param>
   ...
 </web-app>
```

After point this configure class, EasyWeb framework will know how to initialized itself.

## Add build-in filter and mapping

```markup
 <web-app>
   ...
  <filter>
      <filter-name>easyweb_filter</filter-name>
      <filter-class>com.openthinks.easyweb.EasyWebFilter</filter-class>
  </filter>
  <filter-mapping>
      <filter-name>easyweb_filter</filter-name>
      <servlet-name>easyweb</servlet-name>
  </filter-mapping> 
   ...
 </web-app>
```

This filter **EasyWebFilter** is option, if your project need add filters to do authentication, encoding and etc, you can add it in **web.xml**, then you can use POJO class as Filter just like Controller

## Set project class directory

```markup
 <web-app>
   ...
  <!-- remove this in production -->
  <context-param>
    <param-name>easywebClassDir</param-name>
    <param-value>R:\MyGit\easywebexample\target\classes</param-value>
  </context-param>
   ...
 </web-app>
```

This part is option too, it will be helpful when you in development or your web project class directory is not placed at normal path **/WEB-INF/classes/**.

