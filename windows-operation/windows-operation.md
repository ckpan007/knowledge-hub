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




# Reference Links
https://stackoverflow.com/questions/39858200/vmware-workstation-and-device-credential-guard-are-not-compatible
 

