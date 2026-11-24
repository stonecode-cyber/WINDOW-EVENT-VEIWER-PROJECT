**There are three main ways of accessing these event logs within a Windows system:**

- Event Viewer (GUI-based application)
- Wevtutil.exe (command-line tool)
- Get-WinEvent (PowerShell cmdlet)

**Event Viewer has three panes.**

- The pane on the left provides a hierarchical tree listing of the event log providers.
- The pane in the middle will display a general overview and summary of the events specific to a selected provider.
- The pane on the right is the actions pane

<img width="483" height="374" alt="EVENT VIEWER PRE 1" src="https://github.com/user-attachments/assets/0eeffb48-cf50-4510-852e-6301d1df5957" />

The standard logs we had earlier defined on the left pane are visible under Windows Logs.
I opened  the Applications and Services Logs. Expand this section and drill down on Microsoft > Windows > PowerShell > Operational. PowerShell will log operations from the engine, providers, and cmdlets to the Windows event log. i then right click ion the operational  an then properties 

<img width="478" height="367" alt="EVEHT VEIWER PRE 2" src="https://github.com/user-attachments/assets/2c892a1c-a7fd-4fb7-9a3a-525b88412973" />

<img width="406" height="344" alt="EVENT VEIWE PRE 3" src="https://github.com/user-attachments/assets/cb8b0755-6081-4d62-ad16-2dbc88cc1499" />

 In secodnd screenshot above i can  see the log location, log size, and when it was created, modified, and last accessed i can also see the maximum set log size and what action to take once the criteria are met. This concept is known as** log rotation.** 
There is also a clear log bo=uuton in the corner that deal with cdeleting logs.

To filter event on event veiwer, i click on the action, then filter  current log and i input the event id i want to filter, in this case i want to check the login event wkith ID 4624.

<img width="476" height="358" alt="sysmon pre 1" src="https://github.com/user-attachments/assets/427e1163-0572-4cb0-852f-ef95f4bdee8e" />

<img width="329" height="337" alt="sysmon pre 2" src="https://github.com/user-attachments/assets/d6967a50-26c5-4af7-a92a-9f7d51487edd" />

<img width="296" height="326" alt="sysmon pre 3" src="https://github.com/user-attachments/assets/b1b1953d-774d-4793-a1c5-1986972d00d2" /.

TASK 1:What is the Event ID for the earliest recorded event? (Exclude the warning event)

 I open the pan as shown in thge picture above to filter the event  and filter the event for log at earlier  excludinmg the warning event as shown below the event id is 4103.

<img width="425" height="365" alt="EVENYT VIEWER TASK 1 A" src="https://github.com/user-attachments/assets/0b784e29-2833-4aa5-8b6c-cbfa4512face" />

TASK 2: Filter on Event ID 4104. What was the 2nd command executed in the PowerShell session?

I make use of the same filter method as above to filter all event id 4104.
which reveal the  command to be whoami  command on the powershell session

<img width="422" height="223" alt="EVENT VEWER TASK 2" src="https://github.com/user-attachments/assets/22c0b328-6a32-40aa-b900-aab5e8b944c3" />

TASK 3:What is the Task Category for Event ID 4104?
Execute a Remote Command

<img width="469" height="365" alt="EVENT VIEWER TASK 3" src="https://github.com/user-attachments/assets/31b86543-3f6c-4a9f-85bc-3674ec9849ff" />

TASK 4: Within the opened merged.evtx saved log, what is the Task Category for Event ID 800?

<img width="482" height="366" alt="EVENT VEIWER TASK 4" src="https://github.com/user-attachments/assets/401356f6-13eb-47a8-bee1-06c7cd338752" />


**### TOOLS TO QUERY EVENTS WITH COMMAND LINE OR POWERSHELL**

###  **wevtutil.exe :**
  Its a tool we to retrieve information about event logs and publishers, install and uninstall event manifests, run queries, and export, archive and clear log. I  installed wevtutil.exe using the command  **_wevtutil.exe /?._**.

<img width="476" height="362" alt="wevtutil task 1a" src="https://github.com/user-attachments/assets/65e319b2-c652-4f52-9026-6b62865881ad" />

The command will follow these sequence:

wevtutil COMMAND [ARGUMENT [ARGUMENT] …] [/OPTION:VALUE [/OPTION:VALUE] …]

**TASK 1:How many log names are in the machine?** 

In this task i need to enumerate the given log using the command **_el (enumerate-logs)_** as  **_wevtutil el_** This reveal a lot of output 

<img width="404" height="301" alt="WEVTUTIL  TASK1A" src="https://github.com/user-attachments/assets/66ef488a-98a8-4efa-9acb-8b4dd662966a" />

I then pipe the result so i can veiw  the total number of log with the command  **_wevtutil el |Measure-object_**
This show the total number of logs to be 1072

<img width="248" height="118" alt="WEVTUTIL TASK 1B" src="https://github.com/user-attachments/assets/ef6524f2-199d-40a3-8a2c-787967623e8b" />


**### Get-WinEvent**

The Get-WinEvent cmdlet "gets events from event logs and event tracing log files on local and remote computers." It provides information on event logs and event log providers. Inresd more about this with the microsoft event veiw page[ EVENTVEIW
](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.diagnostics/get-winevent?view=powershell-7.6&viewFallbackFrom=powershell-7.1)

COMMON Get- WinEvent Powershell command:

- **Get-WinEvent -ListLog*:**  List  all event logs locally, and the list starts with classic logs first, followed by new Windows Event logs. It is possible to have a log's RecordCount be zero or null.

- **Get-WinEvent -ListProvider *** :List the event log providers and their associated logs. The Name is the provider, and LogLinks is the log that is written to.

**Log filtering**:   to select events from an event log. We can filter event logs using the Where-Object cmdlet as follows:**Get-WinEvent -LogName Application | Where-Object { $_.ProviderName -Match 'WLMS' }** 

In the task below i will be making use of the online guide  for the task below:

**TASK 1: Execute the commandto look for  names of the logs related to OpenSSH?**
 
I made use of the powershell cmdlet  **_Get-WinEvent -ListLog *_** to get all even log and seach for the openssh event. the output can be seen in the screenshot below: as seen the the second screenshot  the openssh event is  **_OpenSSH/Admin,OpenSSH/Operational_**

<img width="488" height="364" alt="Get-WInEvent task 1a" src="https://github.com/user-attachments/assets/f41e3999-f87e-4d92-898e-ac159c3cff12" />
<img width="456" height="276" alt="Get-win event tks 1b" src="https://github.com/user-attachments/assets/75cc3cb8-6ae2-4d45-85c1-ab9835fe2ba4" />
 
**TASK 2: Execute the command to search for *PowerShell*. What is the name of the 3rd log provider?**
In  this task i mke use of the cmlet Get-WinEvent Get-WinEvent -ListProvider  *powershell* to have a loook of the list of log provider  as shown in the screenshot below:

<img width="437" height="269" alt="getwin task 2" src="https://github.com/user-attachments/assets/e12ab1ec-5fc2-41f1-843b-5412cc14fe2e" />

Execute the command  search for  Microsoft-Windows-PowerShell as the log provider. How many event ids are displayed for this event provider?

As i have read through the microsoft officual page for example i will mke use of the cmlet  

**_(Get-WinEvent -ListProvide Microsoft-Windows-PowerShell).Events | Format-Table Id, Description | Measure-object_**
Where the total  as shown in the screenshot below:
<img width="478" height="350" alt="getwin task 3" src="https://github.com/user-attachments/assets/24a9468a-7601-4940-9ebd-cb619ad9dbe2" />

TASK 3: How do you specify the number of events to display?

Through the same official link, i was about to  read through the Filter hash table  with this[ page](https://learn.microsoft.com/en-us/powershell/scripting/samples/creating-get-winevent-queries-with-filterhashtable?view=powershell-7.6&viewFallbackFrom=powershell-7.3)
The table was shown in the screenshot beow.

<img width="515" height="314" alt="get win task 4" src="https://github.com/user-attachments/assets/3cad585f-c0b3-4e11-90d5-04f791437264" />












 
