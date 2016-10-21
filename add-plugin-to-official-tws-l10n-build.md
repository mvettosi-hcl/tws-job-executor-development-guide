# add plugin to official TWS L10N build
- Add the property **_SRC_XLATE=yes_** to the  "Jazz Source Control->User Properties" of the following files:  
```
labels<plugin_name>.properties
<plugin_name>.properties
<plugin_name>JobExecutorMsg.xml  
```
 
- Add to the beginning of file **_labels<plugin_name>.properties_**:  
```
# NLS_ENCODING=UNICODE
# NLS_MESSAGEFORMAT_VAR  
```
 
- Add in the middle of **_<plugin_name>.properties_** before all the **_xxxx.TEXT_** labels:  
```
# NLS_ENCODING=UNICODE
# NLS_MESSAGEFORMAT_VAR  
```