# CloudConvert Integration
CloudConvert (https://cloudconvert.com/) is an online convertion tool you can use to convert files between different formats. Think HTML to PDF, or PNG to JPG etc., but where it's really valueble is to convert old Excel XLS files to new Excel XLSX files. 


## Overview

Linx can work with XLSX-files (The new ones), however, due to the restrictions on the old format, Linx cannot use XLS files. There are Powershell scripts available for you to do your own conversion between XLS and XLSX, but normally that would require you to install (and license) Office on the machine running Linx. Using an online converter like CloudConvert takes this hassle out of the equation.

Of course you can also use this same solution to do any of the other conversions available on CloudConvert, not just Excel. 

## How to use this sample

### CloudConvert Setup:
- First you will need to register on https://cloudconvert.com/
- Once registered, go onto your CloudConvert Dashboard, and select "API v2" --> "Authorization" on the left menu
- Select "Create New API Key" and select the scopes (at a minimum you'll need tasks.read and tasks.write)
- Save the API key

### Linx Setup:
- Using Linx Designer, open the solution file "CloudConvert.lsoz"
- Select "Settings" and set up your details:
-- APIKey: The key you just created in CloudConvert
-- APIKeyName: As you've defined it in CloudConvert. Not used in Linx, but good for referencing back to which key you are using.
-- CCPassword: Again, not used in Linx
-- CCUrl: Can keep as is
-- CCUsername: For your reference, you can save your CloudConvert username here
-- TempTaskFolder: The folder this example with use to place your .tasks files in.


## Additional resources

- Download Linx at https://linx.software
- API References for CloudConvert: https://cloudconvert.com/api/v2

## Dependencies

- Linx Designer 5.20 or newer


## Description

This example includes two different flows to demonstrate the CloudConvert Process. Because CloudConvert uses the principle of tasks and jobs, there are many different ways you can perform the Conversions. However, in this example, Linx is only using Tasks, and keeping track of them. The two flows in this example are:

- **Task Manager Using Sleeps**: In this flow, there is a singular straight down process which keeps looping and checking the status of a task, until it's complete, and then go onto the next. This is not recommended as you could easily go into an infinate loop, however, this is the easiest way to understand how CloudConvert tasks work.
- **Tasks Manager Using TXT Files**: This is a TXT-based database illustrating how you could set up your tasks and then go through the phases of the convertion flow. 

The actuall calls to CloudConvert are done in the APICalls folder

Ideally however, when you build this yourself, you would probably use a Database to track the tasks.

### Data Structure

You can view the data setup of the calls under the "Types" folder.

### Functions

To test this solution, you can follow either of the 2 flows:

For "TaskManagerUsingSleeps" run the "StartTaskUsingSleeps" function. Remember to provide Debug with the starting values:
- OriginalFileFullPath: The full path of the file you want to convert (i.e C:\temp\mytext.txt)
- DestinationFullPath: A path and filename for where you want to save the converted file (i.e. C:\temp\mypdf.pdf)
- FromType: The type of file you are converting from (i.e. txt or xls)
- ToType: The type of file you want to convert to (i.e. pdf or xlsx)

For "TasksManagerUsingTXTFiles" run the "StartTaskUsingTXTFiles" function to initiate the tasks. You will then also need to allow the timer "TaskTimer" to run. For every minute the timer runs, it takes the tasks to the next status. Again, remember to provide the starting values when you run "StartTaskUsingTXTFiles"


