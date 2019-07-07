---
title: Signing
---

# Authenticode

* Store the certificate in a secure location such as Azure KeyVault, and restrict access
* You could consider only timestamping when ready for release, to prevent things like continuous integration builds "spamming" the timestamp server, getting eventually rate limited and failing builds

```powershell

$certSecret = Get-AzureKeyVaultSecret -VaultName $vaultName -Name $secretName
$certBytes = [System.Convert]::FromBase64String($certSecret.SecretValueText)

$flags =  [System.Security.Cryptography.X509Certificates.X509KeyStorageFlags]::EphemeralKeySet

$certificateSecret = Get-AzureKeyVaultSecret -VaultName "MyVault" -Name "MySecret"
$certificateBytes = [System.Convert]::FromBase64String($certificateSecret.SecretValueText)
$certificate = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 ($certificateBytes, $null, [System.Security.Cryptography.X509Certificates.X509KeyStorageFlags]::EphemeralKeySet);
$store = New-Object System.Security.Cryptography.X509Certificates.X509Store("MY", [System.Security.Cryptography.X509Certificates.StoreLocation]::CurrentUser);
$store.Open([System.Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite);
$store.Add($certificate);
$store.Close();
```

```powershell
$secret = Get-AzureKeyVaultSecret -VaultName "MyVault" -Name "MyPrivateKey"
$certificateBytes = [io.file]::ReadAllBytes($env:DOWNLOADSECUREFILE_SECUREFILEPATH);
$certificate = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 ($certificateBytes, $secret.SecretValue, [System.Security.Cryptography.X509Certificates.X509KeyStorageFlags]::EphemeralKeySet);
$store = New-Object System.Security.Cryptography.X509Certificates.X509Store("MY", [System.Security.Cryptography.X509Certificates.StoreLocation]::CurrentUser);
$store.Open([System.Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite);
$store.Add($certificate);
$store.Close();
```