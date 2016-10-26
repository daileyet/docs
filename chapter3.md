# Annotations
EasWeb used annotation to tag and configure the framework. This is simplest and quickest. Of course, normal XML file configuration also can be used to configure the framework, but not implement now, only provider interface:
> com.openthinks.easyweb.context.parser.WebConfigureFileParser

### Configuration Annotations
Relative to the way of XML file configuration, the annotation configuration will parsed by 
> com.openthinks.easyweb.context.parser.WebConfigureAnnoationParser

As below is the configuration annotations list:
1. @**EasyConfigure** Tag a class, make it as configuration class
2. @**ScanPackages**  Indicate which packages need to be scan and where the Tag annotations annotated objects places 
3. @**RequestSuffixs** Indicate the HTTP request path suffix for this framework
4. @**BootstrapClass** Indicate the class name which realize the interface **Bootstrap**
5. @**ScanWay**
  * ScanWayEnum.FILE_PATH : default value; apply for app deployed by folder
  * ScanWayEnum.ADVANCE : used third-party lib [Reflections](https://github.com/ronmamo/reflections); apply for app deployed by war


Sample code:
```java
@EasyConfigure
@ScanPackages({ "com.openthinks.easywebexample" })
@ScanWay(ScanWayEnum.FILE_PATH)
@RequestSuffixs(".do,.htm")
@BootstrapClass("com.openthinks.easywebexample.MyBootstrap")
public class EasyWebConfigure {
}
```
If the configuration class also is bootstrap class whcih implemented type: **com.openthinks.easyweb.context.Bootstrap**
and will use default package sacn way: **ScanWayEnum.FILE_PATH**

```java
@EasyConfigure
@ScanPackages({ "com.openthinks.easywebexample" })
@RequestSuffixs(".do,.htm")
public class EasyWebConfigure implements Bootstrap{
    @Override
	public void cleanUp() {
        //TODO clear resource when app contextDestroyed
	}

	@Override
	public void initial() {
		//TODO initial resource and other things when app contextInitialized
	}
}
```


### Tag Annotations
Exclude configuration anntations, the rest are used to tag or mark a component such as Java POJO class, class field, class method
As below is the tag annotations list:
1. @**Controller** Tag a POJO class which take charge of interacting with a group of HTTP requests
2. @**Filter** Tag a POJO class which take charge of interacting with a group of HTTP filters
3. @**Mapping** Tag a method in Controller/Filter class, which take charge of interacting with one special HTTP request
4. @**ResponseReturn** Tag on the method which with Mapping, that will represent the response trait for the HTTP request
5. @**Jsonp** Tag on the method which with Mapping, that will represent the response as JSONP data format
6. @**AutoComponent** Tag on the filed in Controller/Filter class, which represent a autowire field


Sample code:
default controller name and value(path); interactive HTTP URL:
http://localhost/easywebexample/index.do
```java
@Controller
public class HelloController {
	/**
	 * auto initialize {@link HelloService}
	 */
	@AutoComponent
	HelloService helloService;
	/**
	 * Usage 1: with String return value
	 * forward to hello.jsp
	 * @return jsp view page path
	 */
	@Mapping("/index")
	public String index() {
		return "hello.jsp";
	}
}
```

```java
@Controller("/welcome")
public class WelcomeController {

	@Mapping("/index3")
	@ResponseReturn(contentType = ResponseReturnType.TEXT_XML)
	public String index3() {
		return "<?xml version=\"1.0\" encoding=\"UTF-8\"?> <welcome-file-list><welcome-file>index.do</welcome-file></welcome-file-list>";
	}
}
```

```java
@Controller(name="welcomeController",value="/welcome")
public class WelcomeController {
    @AutoComponent
	WelcomeService welcomeService;
    
	@Mapping("/login/action3")
	@ResponseReturn(contentType = ResponseReturnType.TEXT_JAVASCRIPT)
	@Jsonp
	public String doLogin3(WebAttributers ws) {
		String username = (String) ws.get("username");
		String userpass = (String) ws.get("pass");
		if (helloService.isValidate(username, userpass)) {
			ws.storeSession("LOGIN_NAME", username);
			return OperationJson.build().sucess().toString();
		}
		return OperationJson.build().error().toString();
	}
}

```
