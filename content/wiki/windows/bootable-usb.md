# Making a Windows Bootable USB Drive

## Format the USB drive and make it bootable

Replace ``?`` with the letter of your USB Drive below

```
diskpart
list disk
select disk ?
clean
create partition primary
select partition 1
active
format fs=ntfs quick label="Windows Setup"
exit
```


## Make it boot Windows 10 Installer

### Copy over Windows 10 files

Use 7-zip to extract the contents of the .iso to the USB drive


### Update Bootcode on the USB Drive

Replace ``?`` with the drive letter of your USB Drive

```
C:\> & bootsect.exe /nt60 ?:

Target volumes will be updated with BOOTMGR compatible bootcode.

?: (\\?\Volume{guid})

    Successfully updated NTFS filesystem bootcode.

Bootcode was successfully updated on all targeted volumes.
```