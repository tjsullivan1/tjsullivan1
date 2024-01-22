# Configuring SSL

From here: https://serverfault.com/questions/589607/automatically-reconfigure-winrm-https-listener-with-new-certificate#:~:text=You%20would%20normally%20use%20the%20Set-WSManQuickConfig%20-UseSSL%20command,example.%20Set-Location%20-Path%20WSMan%3AlocalhostService%3B%20Set-Item%20-Path.CertificateThumbprint%20-Value%20%27THUMBPRINT%27%3B

This solution was needed, though I just grabbed the thumprint manually.

```
if (dir wsman:\localhost\listener | where {$_.Keys -like "Transport=https*"})
{
Write-Host "Already enabled"
exit
}
Else
{
#Variables
$zone = ".yourdomain.com"
$fqdn = "$env:computername$zone"
$Thumbprint = certutil -store My "Cert Template Name" | findstr /c:"Cert Hash(sha1)"
# removing cert hash(sha1): and the space after it
$discard,$keep=$Thumbprint.split(":")
$TP = $Keep -replace '\s',''
#enable WinRM HTTPS
winrm create winrm/config/Listener?Address=*+Transport=HTTPS '@{Hostname="'"$fqdn"'"; CertificateThumbprint="'"$TP"'"}'
}
```
