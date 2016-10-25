# Annotations
EasWeb used annotation to tag and configure the framework. This is simplest and quickest. Of course, normal XML file configuration also can be used to configure the framework, but not implement now, only provider interface:
> com.openthinks.easyweb.context.parser.WebConfigureFileParser

### Configuration Annotations
Relative to the way of XML file configuration, the annotation configuration will parsed by 
> com.openthinks.easyweb.context.parser.WebConfigureAnnoationParser

As below is the configuration annotations list:
1. @EasyConfigure 
2. @ScanPackages
3. @RequestSuffixs
4. @BootstrapClass
5. @ScanWay



### Tag Annotations
Exclude configuration anntations, the rest are used to tag or mark a component such as Java POJO class, class field, class method
As below is the tag annotations list:
1. @Controller
2. @Filter
3. @Mapping
4. @ResponseReturn
5. @Jsonp
6. @AutoComponent




