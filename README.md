# WINDOW-EVENT-VEIWER-PROJECT
# WINDOWS-EVENT-LOG-INVESTIGATION-PROJECT

### Windows Event Log Analysis & Investigation Using Event Viewer, Wevtutil and PowerShell

## Table of Contents

1. [Project Overview](#project-overview)
2. [Windows Event Viewer](#windows-event-viewer)
3. [Event Log Filtering & PowerShell Logging](#event-log-filtering--powershell-logging)
4. [Command-Line Event Log Investigation with Wevtutil](#command-line-event-log-investigation-with-wevtutil)
5. [PowerShell Event Log Analysis with Get-WinEvent](#powershell-event-log-analysis-with-get-winevent)
6. [Tools & Technologies](#tools--technologies)
7. [Conclusion](#conclusion)

---

## 1. Project Overview

This project documents a hands-on Windows Event Log investigation lab exploring different methods of accessing, filtering, and analysing Windows event logs.

The investigation focuses on understanding the Windows Event Viewer interface, examining PowerShell Operational logs, querying event logs using `wevtutil.exe`, and retrieving event information through PowerShell's `Get-WinEvent` cmdlet.

The objective is to develop practical skills in Windows log analysis, event filtering, and command-line investigation for SOC monitoring and incident response.

## 2. Windows Event Viewer

Windows Event Viewer is a graphical application used to view and investigate system events.

It consists of three main panes:

- **Left Pane:** Displays the hierarchical tree of event log providers and categories.
- **Middle Pane:** Displays event summaries and details for the selected log.
- **Right Pane:** Provides available actions for managing and filtering events.

The investigation also explored the PowerShell Operational log under:

`Applications and Services Logs > Microsoft > Windows > PowerShell > Operational`

Log properties such as file location, maximum log size, and log retention behaviour were examined. This introduced the concept of **log rotation**, which determines how event logs are managed when size limits are reached.

## 3. Event Log Filtering & PowerShell Logging

Investigated PowerShell Operational events using Event Viewer and filtered logs by specific Event IDs.

**Important PowerShell Event IDs:**

- **Event ID 4103:** PowerShell Module Logging.
- **Event ID 4104:** PowerShell Script Block Logging.
- **Event ID 800:** PowerShell event examined during the merged log investigation.

**Investigation Findings:**
- Earliest recorded event, excluding the warning: Event ID `4103`.
- Second command identified in the PowerShell session: `whoami`.
- Task Category for Event ID 4104: Execute a Remote Command.

## 4. Command-Line Event Log Investigation with Wevtutil

`wevtutil.exe` is a Windows command-line utility used to retrieve information about event logs and publishers, execute queries, export logs, and manage event log configurations.

**Command explored:**

```cmd
wevtutil.exe /?
```

**Important command:**

```cmd
wevtutil el
```

The `el` command enumerates the available event logs on the system.

To count the available logs, I used:

```powershell
wevtutil el | Measure-Object
```

**Investigation Finding:**
- Total event logs enumerated: `1,072`

## 5. PowerShell Event Log Analysis with Get-WinEvent

`Get-WinEvent` is a PowerShell cmdlet used to retrieve events from local and remote Windows event logs and event tracing log files.

**Common commands explored:**

```powershell
# List available event logs
Get-WinEvent -ListLog *

# List event log providers
Get-WinEvent -ListProvider *

# Filter events by provider
Get-WinEvent -LogName Application |
Where-Object { $_.ProviderName -Match 'WLMS' }

# Display event IDs and descriptions for a provider
(Get-WinEvent -ListProvider Microsoft-Windows-PowerShell).Events |
Format-Table Id, Description
```

The investigation covered identifying OpenSSH-related event logs, examining PowerShell event providers, retrieving event IDs, and exploring filtering options such as the FilterHashtable parameter.

---

## 6. 📑 Lab Walkthrough & Documentation

Due to the practical nature of this lab, including Event Viewer screenshots, PowerShell Operational log analysis, `wevtutil` commands, and `Get-WinEvent` queries, the full step-by-step documentation has been placed in a dedicated file.

👉 [**Read the Full Step-by-Step Windows Event Log Investigation Walkthrough**](./Windows-Event-Log-Investigation-Walkthrough.md)

---

## 7. Tools & Technologies

- **Windows Event Viewer:** Graphical event log inspection and filtering.
- **Wevtutil.exe:** Command-line event log enumeration and management.
- **PowerShell:** Event log retrieval and investigation.
- **Get-WinEvent:** Filtering and querying Windows event records.
- **XPath & FilterHashtable:** Structured event log filtering.
- **Windows PowerShell Operational Logs:** Investigating PowerShell activity.

---

## 8. Conclusion

This project provided practical experience in accessing and analysing Windows event logs through graphical and command-line interfaces. It demonstrated how Event Viewer, Wevtutil, and Get-WinEvent can be used together to retrieve, filter, and investigate system activities.

> **Effective SOC investigations depend not only on collecting event logs but also on knowing how to query, filter, and interpret them efficiently. Understanding these tools improves an analyst's ability to investigate suspicious activity and extract meaningful security evidence.**
