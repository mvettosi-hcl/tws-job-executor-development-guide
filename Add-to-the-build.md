# Add to the build
- Rename these files  

| before | before |
|:---:|:---:|
| executorGUI.auiml | <name>.auiml |
| executorGUI.properties | <name>.properties  |
| labels.properties | labels<name>.properties |

- Create the **_build.xml_** file
- Create the xml message file (in the **_src/com/ibm/scheduling/msg_** directory)
- Remove the **_com.ibm.scheduling.agent.\<name\>.msg package__*
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
**_/META-INF/services/com.ibm.scheduling.jobdispatcher.spi.ApplicationDescriptor_**  
```  
and add the following lines:  
```
version=${agent.executors.ver}
label=<name>
category=<category>  
```
- Remove the following jar files from the **_\<name\>JobExecutor\lib_** path:  
```
SchedulerSDO.jar
SchedulerSPI.jar
SchedulerUtil.jar  
```
- Add the java dependencies to the SchedluerSDO, SchedulerSPI and SchedulerUtil projects
- Add the Copyright at the beginning of each source java classes.
- Refactor the packages (if needed) to com.ibm.scheduling.agent
- Refactor the project name to <Executor>JobExecutor