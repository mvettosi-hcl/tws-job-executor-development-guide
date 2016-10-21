# Develop job execution
Modify the *<name>JobExecutor.java*:
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