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
```
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

```
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
1. @**Controller**
2. @**Filter**
3. @**Mapping**
4. @**ResponseReturn**
5. @**Jsonp**
6. @**AutoComponent**




