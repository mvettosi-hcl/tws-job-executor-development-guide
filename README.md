# How to develop a new Job Executor
This is how to develop a new Job Executor for the IBM Workload Scheduler

## Table of contents
[Setup](#setup)  
[User interface](#user-interface)  
[Execution](#execution)  
[Job Properties](#job-properties)  
[Job Output](#job-output)  
[Kill](#kill)  
[Reconnect](#reconnect)  
[Application Lab APIs](#application-lab-apis)  
[Build](#build)  

## Setup
For an introduction and an initial setup:  
1. Follow [this document](/IBM-TWS-Integration-Workbench-86_How-to-custom-Job-Type.pdf)  
2. [Add to the build](/Add-to-the-build.md)  
3. [Modify Job Executor Class](/Modify-Job-Executor-Class.md)  

## User Interface
Instructions to develop particoular elements of the UI
- [Develop user interface](/Develop-user-interface.md)  
- [Develop parameter validation](/Develop-parameter-validation.md)  
- [Develop pick list](/Develop-pick-list.md)  
Remember to verify modeling (composer), modeling (TDWC) and to document the user interface fields (SH)

## Execution
[Develop job execution](/Develop-job-execution.md) and verify it on IBMi