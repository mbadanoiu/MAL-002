# MAL-002

Once a software is successfully installed on the system, one or more trusted MSI files will appear in the “C:\Windows\Installer” folder and may allow a low privilege user to perform “repair” and/or “modify” actions as the “NT Authority\System” user without requiring UAC. By using the “msiexec.exe” program with the “/forcerestart” flag, if an attacker successfully performs the “repair” action, the target system will be restarted.

<strong>Note:</strong> Several MSIs may require Admin authentication even for the repair procedure, but these are usually the exception, not the norm (e.g. Vmware Tools).

### Usecases:

Restarting a Windows server as a low privilege user may be useful when:
<br/>
- Performing local privilege escalation attacks that may crash a service (e.g. buffer overflow attacks), in order to forcefully restart the respective service in case it becomes unresponsive
- Modifying/Writing a configuration file, DLL and/or executable that requires a service/the system to be restarted in order for the changes to take effect (e.g. [DLL Search order attack](https://fuzzysecurity.com/tutorials/16.html))
- Potential DoS via contionusly restarting the target

### Why no CVE?

Neither Microsoft nor I consider this to be a high impact vulnerability by itself, so, no CVE was needed.

With that being said, I find the vulnerability to be rather interesting and hope it is useful to somebody that stumbles upon this repo.

### Requirements:

This vulnerability requires:
<br/>
- Local access on the target system
- One or more usable MSIs to have been installed on the target

### Proof Of Concept:

More details and the exploitation process can be found in this [PDF](https://github.com/mbadanoiu/MAL-002/blob/main/Microsoft%20MSI%20-%20MAL-002.pdf).

### Timeline:

- This vulnerability was initially reported to https://msrc.microsoft.com/ on 18-May-2022
- Vulnerability was considered a non-issue
- Retested the vulnerability on 23-Jan-2023 and noticed that the vulnerability still works on the newest versions of Windows 11 (OS Build: 22621.3007)
- Publically disclosed the vulnerability on 03-Feb-2024

