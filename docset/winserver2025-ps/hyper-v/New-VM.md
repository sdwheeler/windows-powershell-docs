---
description: Use this topic to help manage Windows and Windows Server technologies with Windows PowerShell.
external help file: Microsoft.HyperV.PowerShell.Cmdlets.dll-Help.xml
Module Name: Hyper-V
ms.date: 10/15/2024
online version: https://learn.microsoft.com/powershell/module/hyper-v/new-vm?view=windowsserver2025-ps&wt.mc_id=ps-gethelp
schema: 2.0.0
title: New-VM
---

# New-VM

## SYNOPSIS
Creates a new virtual machine.

## SYNTAX

### No VHD (Default)

```
New-VM [[-Name] <String>] [[-MemoryStartupBytes] <Int64>] [-BootDevice <BootDevice>] [-NoVHD]
 [-SwitchName <String>] [-Path <String>] [-SourceGuestStatePath <String>] [-Version <Version>]
 [-Prerelease] [-Experimental] [[-Generation] <Int16>]
 [-GuestStateIsolationType <GuestIsolationType>] [-Force] [-AsJob] [-CimSession <CimSession[]>]
 [-ComputerName <String[]>] [-Credential <PSCredential[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

### New VHD

```
New-VM [[-Name] <String>] [[-MemoryStartupBytes] <Int64>] [-BootDevice <BootDevice>]
 [-SwitchName <String>] -NewVHDPath <String> -NewVHDSizeBytes <UInt64> [-Path <String>]
 [-SourceGuestStatePath <String>] [-Version <Version>] [-Prerelease] [-Experimental]
 [[-Generation] <Int16>] [-GuestStateIsolationType <GuestIsolationType>] [-Force] [-AsJob]
 [-CimSession <CimSession[]>] [-ComputerName <String[]>] [-Credential <PSCredential[]>] [-WhatIf]
 [-Confirm] [<CommonParameters>]
```

### Existing VHD

```
New-VM [[-Name] <String>] [[-MemoryStartupBytes] <Int64>] [-BootDevice <BootDevice>]
 [-SwitchName <String>] -VHDPath <String> [-Path <String>] [-SourceGuestStatePath <String>]
 [-Version <Version>] [-Prerelease] [-Experimental] [[-Generation] <Int16>]
 [-GuestStateIsolationType <GuestIsolationType>] [-Force] [-AsJob] [-CimSession <CimSession[]>]
 [-ComputerName <String[]>] [-Credential <PSCredential[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION

The `New-VM` cmdlet creates a new virtual machine.

## EXAMPLES

### Example 1

```powershell
New-VM -Name "VM01" -MemoryStartupBytes 512MB
```

This example creates a new virtual machine named `VM01` that has 512 MB of memory.

### Example 2

```powershell
New-VM -Name "VM01" -MemoryStartupBytes 1GB -NewVHDPath D:\vhd\base.vhdx -NewVHDSizeBytes 40GB
```

This example creates a virtual machine named `VM01` that has 1 GB of memory and that is connected to
a new 40 GB virtual hard disk that uses the `VHDX` format.

### Example 3

```powershell
New-VM -Name "VM01" -MemoryStartupBytes 1GB -VHDPath D:\vhd\BaseImage.vhdx
```

This example creates a virtual machine named `VM01` that has 1 GB of memory and connects it to an
existing virtual hard disk that uses the `VHDX` format.

### Example 4

```powershell
New-VM -Name "VM01" -MemoryStartupBytes 2GB -Credential (Get-Credential) -ComputerName HostServer01
```

This example asks for credentials, then creates a virtual machine named `VM01`, which has 2 GB of
memory, on the server named `HostServer01`.

### Example 5

```powershell
New-VM -Name "VM01" -Generation 1 -BootDevice CD -NoVHD
```

This example creates a virtual machine named `VM01`. The machine doesn't have any VHD disks and is
set to boot from a CD.

### Example 6

```powershell
$oldVM = Get-VM "PreviousVM"
$memory = (Get-VMMemory -VMName $oldVM.name).Startup
$switch = (Get-VMNetworkAdapter -VMName $oldVM.name).SwitchName
New-VM -Name "VM01" -Generation $oldVM.Generation -MemoryStartupBytes $memory -SwitchName $switch
```

This example creates a virtual machine named `VM01`. The machine has the same generation and amount
of assigned memory as the existing machine named `PreviousVM` and connects to the same network
switch.

## PARAMETERS

### -AsJob

Runs the cmdlet as a background job.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -BootDevice

Specifies the device to use as the boot device for the new virtual machine. Acceptable values are:

- `CD`
- `Floppy`
- `LegacyNetworkAdapter`
- `IDE`
- `NetworkAdapter`
- `VHD`

When `LegacyNetworkAdapter` is specified, this configures the new virtual machine with a network
adapter that can be used to perform a PXE boot and install a 32-bit operating system from a network
installation server.

Generation 2 virtual machines do not support `Floppy`, `LegacyNetworkAdapter` or `IDE`. Using these
values with a Generation 2 virtual machine will cause an error.

`VHD` and `NetworkAdapter` are new to Generation 2 virtual machines. If you specify them on a
Generation 1 virtual machine, then they are interpreted to be `IDE` and `LegacyNetworkAdapter`
respectively.

```yaml
Type: BootDevice
Parameter Sets: (All)
Aliases:
Accepted values: Floppy, CD, IDE, LegacyNetworkAdapter, NetworkAdapter, VHD

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -CimSession

Runs the cmdlet in a remote session or on a remote computer. Enter a computer name or a session
object, such as the output of a [New-CimSession](/powershell/module/cimcmdlets/new-cimsession) or
[Get-CimSession](/powershell/module/cimcmdlets/get-cimsession) cmdlet. The default is the
current session on the local computer.

```yaml
Type: CimSession[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ComputerName

Specifies one or more Hyper-V hosts on which the virtual machine is to be created. NetBIOS names,
IP addresses, and fully qualified domain names are allowable. The default is the local computer.
Use localhost or a dot (`.`) to specify the local computer explicitly.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Confirm

Prompts you for confirmation before running the cmdlet.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: cf

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Credential

Specifies one or more user accounts that have permission to perform this action. The default is the
current user.

```yaml
Type: PSCredential[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Experimental

Specific prerelease VM version 255.0. This parameter is used to experiment with new VM
functionality, but this is not supported and may fail across updates. This VM version is not
supported in release host builds, meaning you can only use this on pre-release host builds (Windows
Insider program).

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Force

Forces the command to run without asking for user confirmation.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Generation

Specifies the generation, as an integer, for the virtual machine. Acceptable values are:

- `1`
- `2`

```yaml
Type: Int16
Parameter Sets: (All)
Aliases:
Accepted values: 1, 2

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -GuestStateIsolationType

Specifies the level of isolation for the virtual machine being created. Acceptable values are:

- `TrustedLaunch`: Enables guest state isolation and Trusted Launch security features for the
  virtual machine.
- `VBS`: Enables Virtualization Based Security (VBS) isolation for the virtual machine.
- `SNP`: Enables AMD Secure Encrypted Virtualization-Secure Nested Paging (SEV-SNP) isolation for
  the virtual machine.
- `TDX`: Enables Intel Trust Domain Extensions (TDX) isolation for the virtual machine.
- `Disabled`: Disables all guest state isolation features for the virtual machine.

```yaml
Type: GuestIsolationType
Parameter Sets: (All)
Aliases:
Accepted values: TrustedLaunch, VBS, SNP, TDX, Disabled

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -MemoryStartupBytes

Specifies the amount of memory, in bytes, to assign to the virtual machine. The default value is
`512 MB`.

```yaml
Type: Int64
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Name

Specifies the name of the new virtual machine. The default name is New virtual machine.

```yaml
Type: String
Parameter Sets: (All)
Aliases: VMName

Required: False
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName, ByValue)
Accept wildcard characters: False
```

### -NewVHDPath

Creates a new virtual hard disk with the specified path and connects it to the new virtual machine.
Absolute paths are allowed. If only a file name is specified, the virtual hard disk is created in
the default path configured for the host.

```yaml
Type: String
Parameter Sets: New VHD
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -NewVHDSizeBytes

Specifies the size of the dynamic virtual hard disk that is created and attached to the new virtual
machine.

```yaml
Type: UInt64
Parameter Sets: New VHD
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -NoVHD

Creates a virtual machine without attaching any virtual hard disks.

```yaml
Type: SwitchParameter
Parameter Sets: No VHD
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path

Specifies the directory to store the files for the new virtual machine.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Prerelease

Specific prerelease VM version 254.0. This parameter is used to experiment with new VM
functionality, but this is not supported and may fail across updates. This VM version is not
supported in release host builds, meaning you can only use this on pre-release host builds (Windows
Insider program).

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -SourceGuestStatePath

Specifies the path to the guest state file for the virtual machine being created. Specifying the
guest state path allows for creation of a new virtual machine that has the same configuration and
state as the existing virtual machine.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -SwitchName

Specifies the friendly name of the virtual switch if you want to connect the new virtual machine to
an existing virtual switch to provide connectivity to a network. Hyper-V automatically creates a
virtual machine with one virtual network adapter, but connecting it to a virtual switch is
optional.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -VHDPath

Specifies the path to a virtual hard disk file.

```yaml
Type: String
Parameter Sets: Existing VHD
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Version

Specifies the version during the VM creation process. See,
[Get-VMHostSupportedVersion](/powershell/module/hyper-v/get-vmhostsupportedversion) for supported
VM versions on a given host.

```yaml
Type: Version
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf

Shows what would happen if the cmdlet runs. The cmdlet is not run.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: wi

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable,
-InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose,
-WarningAction, and -WarningVariable. For more information, see
[about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters).

## INPUTS

### System.String

## OUTPUTS

### Microsoft.HyperV.PowerShell.VirtualMachine

## NOTES

## RELATED LINKS
