# Add to the build
1. Rename these files  

| before | before |
|:---:|:---:|
| executorGUI.auiml | <name>.auiml |
| executorGUI.properties | <name>.properties  |
| labels.properties | labels<name>.properties |

2. Create the build.xml file
3. Create the xml message file (in the src/com/ibm/scheduling/msg directory)
7. Remove the com.ibm.scheduling.agent.<name>.msg package
8. Rename the /META-INF/services/com.ibm.scheduling.jobdispatcher.spi.ApplicationDescriptor.base to com.ibm.scheduling.jobdispatcher.spi.ApplicationDescriptor
9 Edit the /META-INF/services/com.ibm.scheduling.jobdispatcher.spi.ApplicationDescriptor. file and add the following lines:  
```
version=${agent.executors.ver}
label=<Name>
category=<category>  
```
10. Remove the following jar files from the <Name>JobExecutor\lib path:  
```
       SchedulerSDO.jar
       SchedulerSPI.jar
       SchedulerUtil.jar  
```
11. Add the java dependencies to the SchedluerSDO, SchedulerSPI and SchedulerUtil projects
12. Add the Copyright at the beginning of each source java classes.
13. Refactor the packages (if needed) to com.ibm.scheduling.agent
14. Refactor the project name to <Executor>JobExecutor