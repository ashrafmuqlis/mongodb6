# VirtualBox Core Dump Issue

## Run a Privileged CMD
```
bcdedit /set hypervisorlaunchtype off
```

```
DISM /Online /Disable-Feature:Microsoft-Hyper-V
```

## Configure VM to enable nested virtualization
VBoxManage modifyvm <vmname> --nested-hw-virt on
