# Software Maintenence

## Hyper-v issue
Error message: VMware Player and Device/Credential Guard are not compatible.
<br>See below:
https://kb.vmware.com/s/article/2146361
<br>
https://docs.microsoft.com/en-us/windows/security/identity-protection/credential-guard/credential-guard-manage


## Worked solution to close Device/Credential Guard

Right-click CMD in start menu>> Run as Administrator>> type below command:
```sh
bcdedit /set hypervisorlaunchtype off
```
Then just restart the computer will solve the issue.


# Monitor Log or Text File Changes in Real Time

## mTail
Download URL: https://www.raymond.cc/blog/download/did/3776/


## SnakeTail

## Notepad ++

### Notepad Enable Silent Updates
![Notepad Enable Silent Updates](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/windows-operation/notepad_enable_silent_updtes.png)

### Notepad++ Monitoring In The Background
![Notepad Install Document Monitor](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/windows-operation/install_document_monitor.png)

## Monitoring From PowerShell
![PowerShell Get Content Tail](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/windows-operation/powershell_get-content_tail.png)

## Monitoring From Command Line
![Monitoring From Command Line](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/windows-operation/command_prompt_tail.png)


# Reference Links
https://stackoverflow.com/questions/39858200/vmware-workstation-and-device-credential-guard-are-not-compatible
 

