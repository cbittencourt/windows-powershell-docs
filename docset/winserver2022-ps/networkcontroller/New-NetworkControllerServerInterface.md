---
description: Use this topic to help manage Windows and Windows Server technologies with Windows PowerShell.
external help file: Microsoft.NetworkController.Powershell.dll-help.xml
Module Name: NetworkController
ms.date: 12/20/2016
online version: https://docs.microsoft.com/powershell/module/networkcontroller/new-networkcontrollerserverinterface?view=windowsserver2022-ps&wt.mc_id=ps-gethelp
schema: 2.0.0
title: New-NetworkControllerServerInterface
---

# New-NetworkControllerServerInterface

## SYNOPSIS
Creates or updates a physical network interface resource in the Network Controller.

## SYNTAX

```
New-NetworkControllerServerInterface [-ServerId] <String> [-ResourceId] <String>
 [-Properties] <NwInterfaceProperties> [[-ResourceMetadata] <ResourceMetadata>] [[-Etag] <String>] [-Force]
 -ConnectionUri <Uri> [-CertificateThumbprint <String>] [-Credential <PSCredential>] [-PassInnerException]
 [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION
The **New-NetworkControllerServerInterface** cmdlet creates a physical network interface resource or updates an existing physical network interface resource in the Network Controller.
Before you can create an interface resource, there must be a server resource to which it belongs.
For more information, see the **New-NetworkControllerServer** cmdlet.

## EXAMPLES

### Example 1: Create a server interface
```
PS C:\> $InterfaceIPConfig = New-Object Microsoft.Windows.NetworkController.InterfaceIPConfiguration
PS C:\> $InterfaceIPConfig.IpAddress = "10.0.0.1"
PS C:\> $InterfaceIPConfig.NetworkPrefix = "24"
PS C:\> $InterfaceIPConfig.DefaultGateway = "10.0.0.100"
PS C:\> $InterfaceIPConfig.VLAN = "1"
PS C:\> $InterfaceIPConfig.IsDhcpEnabled = "False"
PS C:\> $NwInterfaceProp = New-Object Microsoft.Windows.NetworkController.NwInterfaceProperties
PS C:\> $NwInterfaceProp.IPConfiguration = @($InterfaceIPConfig)
PS C:\> $NwInterfaceProp.InterfaceIndex = "2"
PS C:\> $NwInterfaceProp.InterfaceName = "Corp"
PS C:\> $NwInterfaceProp.Mac = "00:11:22:33:44:AA"
PS C:\> New-NetworkControllerServerInterface -ConnectionUri "https://networkcontroller" -ServerId "Server01" -ResourceId "Interface01" -Properties $NwInterfaceProp
```

The first command creates an **InterfaceIPConfiguration** by using the **New-Object** cmdlet.
The command stores the object in the $InterfaceIPConfig variable.

The next five commands assign values to properties of $InterfaceIPConfig.

The seventh command creates an **NwInterfaceProperties** object by using **New-Object**.
The command stores the object in the $NwInterfaceProp variable.

The next four commands assign values to properties of $NwInterfaceProp.
This includes the value of $InterfaceIPConfig for the **IPConfiguration** property.

The final command creates a server interface that has the resource ID Interface01.
The interface is on a server that has the resource ID Server01.
The URI identifies the Network Controller.
The $NwInterfaceProp variable specifies the properties of the interface.

## PARAMETERS

### -CertificateThumbprint
Specifies the certificate thumbprint of a digital public key X.509 certificate of a user account that has permission to perform this action.
In order for Network Controller to authorize the account, specify this thumbprint by using the *ClientCertificateThumbprint* parameter of the **Install-NetworkController** or **Set-NetworkController** cmdlet.

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

### -Confirm
Prompts you for confirmation before running the cmdlet.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: cf

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -ConnectionUri
Specifies the Uniform Resource Identifier (URI) of the Network Controller.
All Representational State Transfer (REST) clients use this URI to connect to Network Controller.

```yaml
Type: Uri
Parameter Sets: (All)
Aliases: 

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Credential
Specifies a user credential that has permission to perform this action.
The default value is the current user.
This user must be present in the security group specified in the *ClientSecurityGroup* parameter in **Install-NetworkController**.

```yaml
Type: PSCredential
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Etag
Specifies the entity tag (ETag) parameter of the resource.
An ETag is an HTTP response header returned by an HTTP-compliant web server.
An ETag is used to determine change in the content of a resource.
The value of the header is an opaque string that represents the state of the resource when the response was generated.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: 6
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
Position: 7
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -PassInnerException
This thumbprint must also be provided in the **ClientCertificateThumbprint** parameter in the **Install-NetworkController** or **Set-NetworkController** cmdlet so that Network Controller can authorize this user.

The thumbprint must be provided only if the network controller client authentication is X509 certificates.
**Get-NetworkController** retrieves that client authentication and authorization information.

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

### -Properties
Specifies properties of a server interface that this cmdlet adds or updates.
You can specify the following properties: 

- Interface index.
- Interface name.
- Interface speed.
- IP configuration of the interface.
The configuration contains an IP address, network prefix, default gateway, VLANs, and whether the IP address has been obtained over DHCP.
- Logical subnets to which the network interface is connected.
- MAC address.
- VLAN IDs of networks to which the interface is connected.
- Whether this interface is a baseboard management controller (BMC) interface.

```yaml
Type: NwInterfaceProperties
Parameter Sets: (All)
Aliases: 

Required: True
Position: 3
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -ResourceId
Specifies the resource ID of the server interface that this cmdlet adds or updates.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: True
Position: 1
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -ResourceMetadata
Specifies metadata information for the client, such as the tenant ID, group ID, and resource name.

```yaml
Type: ResourceMetadata
Parameter Sets: (All)
Aliases: 

Required: False
Position: 4
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ServerId
Specifies the server to which the interface belongs.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -WhatIf
Shows what would happen if the cmdlet runs.
The cmdlet is not run.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: wi

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### System.String

### Microsoft.Windows.NetworkController.NwInterfaceProperties

## OUTPUTS

### System.Object

## NOTES

## RELATED LINKS

[Get-NetworkControllerServerInterface](./Get-NetworkControllerServerInterface.md)

[Install-NetworkController](./Install-NetworkController.md)

[Remove-NetworkControllerServerInterface](./Remove-NetworkControllerServerInterface.md)

[Set-NetworkController](./Set-NetworkController.md)

