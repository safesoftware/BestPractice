# BestPractice
A Best Practices analysis tool for FME Workspaces. Related post on FME Knowledge center can be found here: https://knowledge.safe.com/questions/37858/fme-best-practice-validation-project-you-can-help.html

This project includes workspaces and custom transformers that carry out best practice tests. There are (currently) two workspaces in the project. One of them is for use on FME Server, particularly with notifications. The other is for use on FME Desktop.

**Version:** Will work on FME(R) 2017.0.0.0 (20170228 - Build 17259) or newer

## Installing the Project (Desktop) ##
The easiest way to install this project is to download/fork it onto a local machine and in FME Workbench use Tools &gt; FME Options &gt; Default Paths, add the download folder as a Shared FME Folder.

Because the download folder includes subfolders for Workspaces and Transformers, FME Workbench will automatically locate and install this functionality on startup.

## Using the Project (Desktop) ##
On FME Desktop open and run the main workspace, pointing its published parameters to the workspace you wish to analyze.

A HTML report will be generated and written to the desired location, reporting on the Best Practices used in developing that workspace.

## Installing the Project (Server) ##
This method is to install the project for use with the email notification services.

- Copy the transformers to Resources\Engine\Transformers on FME Server. You can use either a file browser or the FME Server web interface.
- Create two notification topics; one for incoming notifications and one for outgoing
- Create a notification publication of type email that is tied to the incoming notification topic
- Create a notification subscription of type email that is tied to the outgoing notification topic
- Publish the workspace to FME Server
	- Register the workspace against the notification service
	- Under the notification service parameters:
		- Set the workspace to subscribe to the incoming notification topic
		- Set the Source TextFile reader to receive the incoming topic message
		- Set the workspace to post (on success) to the outgoing notification topic
		- Set the Destination TextFile writer to post data to the outgoing topic message

## Using the Project (Server) ##
Send an email to the incoming email publication. The workspace should be added as an attachment. The topic will be triggered and run the assessment workspace. The workspace will create the output report and send it by email back to the From email address.

The name of the report will be taken from the email subject line.

The report and a copy of the workspace will be copied to the folder Resources\Data\BestPractice


## Contribute
Please do contribute and help improve this project if you wish.

The ToDo list markdown document in this repository includes a list of suggested updates you might wish to try.

**TODO:** *Tutorial on how to submit your suggested updates.*

Some rules and suggestions for contributions:

- Only use this version of FME to edit the files: 2017.0.0.0 (20170228 - Build 17259)
- Before doing any work, make sure you have the latest versions of the files (in case someone else has made changes too)
- All the tests fall inside custom transformers, that way the same transformers can be used for both desktop and server workspaces
	- Because the custom transformers are used by both desktop and server, use only functionality that is compatible with both platforms
	- for example, avoid using paths and/or assuming this will be on a Windows platform
- If there are changes that are platform specific then make them to the **workspace** not to the **transformers** 
- If you update one workspace, please update the other too
	- for example if you add a new input port to a custom transformer, you should update that transformer in both the desktop and server workspaces
	- hopefully we can someday merge the two to create a single, unified workspace  
