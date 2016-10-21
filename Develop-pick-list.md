# Develop pick list
To develop a pick list, you have to implement the *runExecutorCommand* method

- Validate input parameters needed to perform the selected action, for example:  
```java
//Validate needed fields
try {
    //use common parameter validator
    ListResourceBundle bundle = getPluginCatalog(loc);               
    ParameterValidator validator = new ParameterValidator(bundle);           
    validator.validateNotEmpty(SalesforceConstants.SERVER, server, SalesforceJobExecutorMsg.AWKSAF009E_MISSING_SERVER );
    validator.validateNotEmpty(SalesforceConstants.USERNAME, username, SalesforceJobExecutorMsg.AWKSAF010E_MISSING_USERID );
    validator.validateNotEmpty(SalesforceConstants.PASSWORD, password, SalesforceJobExecutorMsg.AWKSAF011E_MISSING_USERPASSWORD );
} catch (ValidationException e1) { 
    actions.add(createPopUpMessage(SalesforceJobExecutorMsg.Error, e1.getMessage(),loc));
    return response;
}
```  
- Add the canRunOnConnector in the <name>JobExecutor.java, adding all pick list buttons actions you have in your UI that need to be executed on the agent side.
```java
/*
* (non-Javadoc)
*
* @see com.ibm.scheduling.spi.jobexecutor.JobExecutorSupport#canRunOnConnector(java.lang.String)
*/
public boolean canRunOnConnector(String command) {
    if (command.equals(TEST_CONNECTION) || command.equals(GET_PROMPT_LIST))
        return false;
    return true;
}
```
- If you have a configuration file  use method *protected String updateParameterFromFile(String key, Map<String, String> parametersMap, String keyOnFile, Properties propertiesFile, boolean isReverseOrder)* to fill the parameters with file properties. Oozie plugin is one example of this use.