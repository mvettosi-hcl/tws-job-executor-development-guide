# Develop parameter validation
In **_\<name\>JobExecutor.java_**:
- Add the following method:  
```java
private ListResourceBundle getPluginCatalog(Locale loc) {
      return getCatalog(loc, this.getClass().getClassLoader());
}
```
- implement the validateJsdl(String jsdl, Locale loc) method.  
  Use this code as sample:  
```java
String methodName = "validateJsdl";
logger.entering(CLASS_NAME, methodName);

catalog = (ListResourceBundle)ListResourceBundle.getBundle(JSR352JavaBatchJobExecutorMsg.CLASS_NAME, loc);
Map<String, Object> parameters = jsdlToParameters(jsdl, EXEC_TYPE, loc);
ListResourceBundle bundle = getPluginCatalog(loc);
//validate parameters
ParameterValidator validator = new ParameterValidator(bundle);
String appName = (String) parameters.get("applicationname");
validator.validateNotEmpty(appName, JSR352JavaBatchJobExecutorMsg.AWKJBJ011E_MISSING_APPLICATION_NAME);
```