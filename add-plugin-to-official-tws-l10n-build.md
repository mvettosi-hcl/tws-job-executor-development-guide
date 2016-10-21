# add plugin to official TWS L10N build
- Add the property SRC_XLATE=yes to the  "Jazz Source Control->User Properties" of the following files:  
```
labels<plugin_name>.properties
<plugin_name>.properties
<plugin_name>JobExecutorMsg.xml  
```
 
- Add to the beginning of file labels<plugin_name>.properties:  
```
# NLS_ENCODING=UNICODE
# NLS_MESSAGEFORMAT_VAR  
```
 
- Add in the middle of <plugin_name>.properties before all the xxxx.TEXT labels:  
```
# NLS_ENCODING=UNICODE
# NLS_MESSAGEFORMAT_VAR  
```