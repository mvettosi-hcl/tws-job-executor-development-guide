# Develop job properties
- In the **_runAction(Map<String, String> jobProperties,Map<String, String> properties)_** method fill the "properties" map with the properties to be exported.
- In the **_monitorAction_** method fill the "properties" map with the properties to be exported.
- Create the label for these properties. In the message file add an entry like the following:  
```xml
<Label ID="AWKSAF108I">
    <LabelText pgmKey="ApexJobID" varFormat="Java">Apex job ID</LabelText>
</Label>
```
where ApexJobID is the name of the property.
- Send the message file to the id team for a review
- Also store the properties needed for  a reconnect to the jobProperties. For example:  
```java
jobProperties.put(BOINSTANCEID_PROP, instanceID);
```
- At the end of the runAction remember to save the jobProperties in the instance:
```java
storeJobInstanceProperties(jobProperties);
```