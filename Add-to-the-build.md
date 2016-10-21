# Add to the build
- Rename these files  

| before | before |
|:---:|:---:|
| executorGUI.auiml | <name>.auiml |
| executorGUI.properties | <name>.properties  |
| labels.properties | labels<name>.properties |

- Create the build.xml file
- Create the xml message file (in the src/com/ibm/scheduling/msg directory)
- Remove the com.ibm.scheduling.agent.<name>.msg package
- Rename the file  
```
/META-INF/services/com.ibm.scheduling.jobdispatcher.spi.ApplicationDescriptor.base  
```  
to  
```
com.ibm.scheduling.jobdispatcher.spi.ApplicationDescriptor  
```
- Edit the file  
```
/META-INF/services/com.ibm.scheduling.jobdispatcher.spi.ApplicationDescriptor  
```  
and add the following lines:  
```
version=${agent.executors.ver}
label=<Name>
category=<category>  
```
- Remove the following jar files from the <Name>JobExecutor\lib path:  
```
SchedulerSDO.jar
SchedulerSPI.jar
SchedulerUtil.jar  
```
- Add the java dependencies to the SchedluerSDO, SchedulerSPI and SchedulerUtil projects
- Add the Copyright at the beginning of each source java classes.
- Refactor the packages (if needed) to com.ibm.scheduling.agent
- Refactor the project name to <Executor>JobExecutor