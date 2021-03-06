# Quick Start

### Add dependency to pom.xml

```markup
<dependency>
  <groupId>com.openthinks</groupId>
  <artifactId>easyweb</artifactId>
  <version>1.2</version>
</dependency>
```

### Configure project by annotationed POJO class

```java
/*
 * File name:com.openthinks.easywebexample.EasyWebConfigure
*/
@EasyConfigure
@ScanPackages({ "com.openthinks.easywebexample" })
@RequestSuffixs(".do,.htm")
public class EasyWebConfigure{}
```

### Enable easyweb in web.xml

```markup
  ...
  <servlet>
    <servlet-name>easyweb</servlet-name>
    <servlet-class>com.openthinks.easyweb.EasyWebDispatcher</servlet-class>
    <load-on-startup>0</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>easyweb</servlet-name>
    <url-pattern>*.do</url-pattern>
  </servlet-mapping>
  <servlet-mapping>
    <servlet-name>easyweb</servlet-name>
    <url-pattern>*.htm</url-pattern>
  </servlet-mapping>
  <listener>
    <listener-class>com.openthinks.easyweb.context.WebContextLoadListener</listener-class>
  </listener>
  <context-param>
    <param-name>configureClassName</param-name>
    <param-value>com.openthinks.easywebexample.EasyWebConfigure</param-value>
  </context-param>
  ...
```

### Create Controller with POJO class

```java
@Controller
public class HelloController {
    @Mapping("/index")
    public String index() {
        return "hello.jsp";
    }
}
```

## Deploy app to web container and run

After deploy your web application to Servlet container\(Tomcat/Resin\)

Access by URL: [http://localhost:8080/easywebexample/index.htm](http://localhost:8080/easywebexample/index.htm) or [http://localhost:8080/easywebexample/index.do](http://localhost:8080/easywebexample/index.do) to get page which render by **hello.jsp**

_easywebexample_ is app web root context.

