# Develop job execution
Modify the **_<name>JobExecutor.java_**:
- modify the method execute:  
```java
public void execute() throws JobExecutorException {
    String methodName = "execute"; //$NON-NLS-1$
    logger.entering(CLASS_NAME, methodName);
     
    if (logger.isLoggable(Level.FINEST)) {
        logger.logp(Level.FINEST, CLASS_NAME, methodName,
            "ENTRY with - JobId = {0}", //$NON-NLS-1$
            new Object[] {
                getJobIdentifier().toString(),
            }
        );
    }
    try {
        this.validateParameters(salesforceParameters, Locale.getDefault());   
    } catch (Exception e) {
        String msg = e.getMessage();
        logger.logp(Level.FINE, CLASS_NAME, methodName, e.toString());
        changeStatus(JobStatusEvent.FAILED_SUBMISSION, -1, msg);
    }
    setJobProperties();
 
    runAndMonitorPattern(jobProperties);
    logger.exiting(CLASS_NAME, methodName);
}
```
Where **_runAndMonitorPattern_** could also be **_runPattern_** depending on your plugin behavior.
- create the private method setJobProperties() where you have to build the map with the parameters to be used in the plugin.  
  here is an example:  
```java
private void setJobProperties() {
    logger.info("Taking information from panel");
    String server = salesforceParameters.getSalesforceParms().getServerConnection().getServer().getText();
    String username = salesforceParameters.getSalesforceParms().getServerConnection().getUserID().getText();
    String password = salesforceParameters.getSalesforceParms().getServerConnection().getPassword().getText();
    String apexClass = salesforceParameters.getSalesforceParms().getAPEXJobDetails().getAPEXClass().getText();
    logger.info("Taking information from configuration file");
    String proxyServer=properties.getProperty(PROXYSERVER);
    String proxyServerPort=properties.getProperty(PROXYSERVERPORT);
    String pollingPeriod=properties.getProperty(POLLINGPERIOD);
    String pollingTimeout=properties.getProperty(POLLINGTIMEOUT);
    
    //validate properties read from file and set default if needed
    if (proxyServer==null) proxyServer="";
    
    if (proxyServerPort==null)
        proxyServerPort="0";
    else {
        try {
            int i=Integer.parseInt(proxyServerPort);
            if (i<0) proxyServerPort="0";
        } catch (NumberFormatException e) {
            logger.fine(PROXYSERVERPORT + " " + e.getLocalizedMessage());
            proxyServerPort="0";
        }
    }
        
    if (pollingPeriod==null || pollingPeriod.isEmpty()){
        pollingPeriod="10";
    } else {
        try {
            int i=Integer.parseInt(pollingPeriod);
            if (i<=5) pollingPeriod="5";
        } catch (NumberFormatException e) {
            logger.fine(POLLINGPERIOD + " " + e.getLocalizedMessage());
            pollingPeriod="10";
        }
    }
    
    if (pollingTimeout==null || pollingTimeout.isEmpty()){
        pollingTimeout="1800";
    } else {
        try {
            int i=Integer.parseInt(pollingTimeout);
            if (i<=10) pollingTimeout="10";
        } catch (NumberFormatException e) {
            logger.fine(POLLINGTIMEOUT + " " + e.getLocalizedMessage());
            pollingTimeout="1800";
        }
    }
    
    jobProperties.put(SERVER,server);
    jobProperties.put(USERNAME,username);
    jobProperties.put(PASSWORD,getEncrypted(password, key1, key2, key3));
    jobProperties.put(APEXCLASS,apexClass);
    jobProperties.put(PROXYSERVER,proxyServer);
    jobProperties.put(PROXYSERVERPORT,proxyServerPort);
    jobProperties.put(POLLINGPERIOD,pollingPeriod);
    jobProperties.put(POLLINGTIMEOUT,pollingTimeout);
}
```
- If you have a configuration file then use the method **_protected void addJobProperty(String key, StringValue value, String keyInFile, Properties propertiesFile)_** to fill the jobproperties reading properties form the file. See Oozie plugin example for help
- Modify the **_<name>JobExecutor__* constructor adding:  
```java  
properties = loadPropertiesFromFile(System.getProperty(CONFIGDIR), CONFIG_FILENAME, PROP_FILE);
```
- add in the class:
```java  
protected Properties properties;
```
- Modify the **_<name>JobExecutorContants.java_** adding:
```java  
// Encryption key
public static final byte[] key1 = new byte[] {(byte) 0x5c, (byte) 0x37, (byte) 0x92, (byte) 0x3a, (byte) 0x02, (byte) 0x85, (byte) 0x56, (byte) 0xc7, (byte) 0xda, (byte) 0x41, (byte) 0xd6, (byte) 0xdb, (byte) 0x0a, (byte) 0x03, (byte) 0xea, (byte) 0xe0};
public static final byte[] key2 = new byte[] {(byte) 0x5e, (byte) 0x38, (byte) 0x92, (byte) 0x81, (byte) 0x80, (byte) 0xee, (byte) 0xdb, (byte) 0xda, (byte) 0x15, (byte) 0x7c, (byte) 0x04, (byte) 0xf3, (byte) 0xa8, (byte) 0x43, (byte) 0x93, (byte) 0xb0};
public static final byte[] key3 = new byte[] {(byte) 0x0d, (byte) 0xff, (byte) 0x38, (byte) 0xaf, (byte) 0x8e, (byte) 0xe5, (byte) 0x68, (byte) 0x5f, (byte) 0x42, (byte) 0xee, (byte) 0xa9, (byte) 0xa4, (byte) 0x81, (byte) 0x04, (byte) 0x06, (byte) 0x78};
public static final String CONFIGDIR = "ConfigDir";
public static final String CONFIG_FILENAME = "SalesforceJobExecutor.properties";
public static final String PROP_FILE = "cfg/" + CONFIG_FILENAME;   
```
- Modify the **_<name>Action.java_**:
  1. replace the **_doAction_** method with the **_runAction_** method.
  2. if the **_runAndMonitorPattern_** has been used then implement also the **_monitorAction_** method

- Modify the **_runExecutorCommand_** and **_validateJsdl_** methods adding the following line:
```java  
catalog = (ListResourceBundle)ListResourceBundle.getBundle(<name>JobExecutorMsg.CLASS_NAME, loc);
```