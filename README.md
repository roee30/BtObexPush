# BtObexPush

Discover and push files to bluetooth devices from the command line.

## Installation

Download `BtObexPush.exe` from the latest release to a directory in your `PATH`.

## Usage

List paired devices:
```shell
> BtObexPush.exe list
Name of Device                               AABBCCDDEEFF
...
```

This is somewhat [broken](https://github.com/inthehand/32feet/issues/465) on Windows 10/11,
so use this powershell alternative if no devices are shown:

```powershell
Get-PnpDevice -Class Bluetooth | ? Status -eq 'OK' | % {if ($_.HardwareId[0] -match '\w{12}$') {[pscustomobject]@{Name=$_.FriendlyName;Address=$matches[0].ToUpper()}}} | sort -unique Address
```

Send file to device:
```shell
> BtObexPush.exe AABBCCDDEEFF file.txt
```
