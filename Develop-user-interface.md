# Develop user interface
- Set the password with the standard auiml component:  
   In the file **_\<name\>JobExecutor/resources/\<name\>.auiml_** change the password entries
```xml  
<STRING NAME="myPassword" MANDATORY="TRUE" OBSCURED="TRUE">
```  
   with the following one:
```xml  
<STRING NAME="myPassword" BINDING="passwordSelector#modeling.widgets.password.PasswordSelector:userID" MANDATORY="TRUE" OBSCURED="TRUE">
```  
   where userID is neme of the user component in the auiml file to which the password is referred.
- When the UI is rendered the labels that appear in the UI has to be placed above the text fields, move them if not already there.