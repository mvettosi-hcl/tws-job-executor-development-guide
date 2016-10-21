# Modify Job Executor Class
- Add the following in the **_<name>JobExecutorConstants_** class    
```java
public static final ListResourceBundle CATALOG = (ListResourceBundle)ListResourceBundle.getBundle( <Name>JobExecutorMsg.CLASS_NAME );  
```
- Add the following statement in the constructor of the **_<name>JobExecutor_** class:  
```java
catalog=CATALOG;  
```
- Remove the Timer class from the **_<name>JobExecutor_** class.
- Remove the **_getExecutionLog_** method