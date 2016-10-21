# Modify Job Executor Class
- Add the following in the *<name>JobExecutorConstants* class    
```java
public static final ListResourceBundle CATALOG = (ListResourceBundle)ListResourceBundle.getBundle( <Name>JobExecutorMsg.CLASS_NAME );  
```
- Add the following statement in the constructor of the *<name>JobExecutor* class:  
```java
catalog=CATALOG;  
```
- Remove the Timer class from the *<name>JobExecutor* class.
- Remove the *getExecutionLog* method