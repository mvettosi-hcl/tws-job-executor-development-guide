# add plugin to official TWS build
1. In  the file tws_build/tdwb_java/src/build.xml
   - add *<name>JobExecutor* to property **_ExecutorsProjects_** at the line **_<property name="ExecutorsProjects" value="........................."/>_**
   - add **_<name>JobExecutor_** to the for loop ====> **_for list="${ExecutorsProjects}" at line <contains string="......................." substring="@{project}" />_**
 
2. In  the file tws_build/tdwb_java/src/agent/build.xml
   - add **_<name>JobExecutor_** to the file list **_<filelist id="agent" dir="${build.date}" files="...........................r" />_**
 
3. To add the plugin to the install package open the file /cdrom/src/Makefile  in tws_install component
   - add **_com.ibm.scheduling.agent.<name>_$(VERSION_CONST).jar_**  to the property **_tws-executors-base_** and **_tws-equinox-plugin-base_**
 
4. Add the following line to **_/tws_agents_bom/images_template/unix/twsinst_** in the section "Remove old jre and java plugins"  
```
rm -f $TWS_DIR/TWS/JavaExt/eclipse/plugins/com.ibm.scheduling.agent.<name>_*.jar  
```
 
5. Add the following line to **_/tws_agents_bom/images_template/windows/twsinst.vbs_** in the section "Remove old java plugins"  
```
objFSO.DeleteFile TWS_DIR & "\TWS\JavaExt\eclipse\plugins\com.ibm.scheduling.agent.<name>_*.jar", 1  
```
 
6. (optional) To add the plugin properties file (if any) to the install package open the file **_tws_install/cdrom/src/Makefile_**
   - add **_$(TOP)/../tdwb_java/src/agent/<name>Executor/cfg/<name>Executor.properties_**  to the property **_tws-equinox-cfg-files_** and **_tws-equinox-cfg-files-win_**
