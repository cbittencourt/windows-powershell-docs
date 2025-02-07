---
external help file: Microsoft.ActiveDirectory.Management.dll-Help.xml
Module Name: ActiveDirectory
online version: https://docs.microsoft.com/powershell/module/activedirectory/add-adgroupmember?view=windowsserver2012-ps&wt.mc_id=ps-gethelp
schema: 2.0.0
---

# Add-ADGroupMember

## SYNOPSIS
Adds one or more members to an Active Directory group.

## SYNTAX

```
Add-ADGroupMember [-WhatIf] [-Confirm] [-AuthType <ADAuthType>] [-Credential <PSCredential>]
 [-Identity] <ADGroup> [-Members] <ADPrincipal[]> [-Partition <String>] [-PassThru] [-Server <String>]
 [<CommonParameters>]
```

## DESCRIPTION
The Add-ADGroupMember cmdlet adds one or more users, groups, service accounts, or computers as new members of an Active Directory group.

The Identity parameter specifies the Active Directory group that receives the new members.
You can identify a group by its distinguished name (DN), GUID, security identifier (SID) or Security Accounts Manager (SAM) account name.
You can also specify group object variable, such as $\<localGroupObject\>, or pass a group object through the pipeline to the Identity parameter.
For example, you can use the Get-ADGroup cmdlet to get a group object and then pass the object through the pipeline to the Add-ADGroupMember cmdlet.

The Members parameter specifies the new members to add to a group.
You can identify a new member by its distinguished name (DN), GUID, security identifier (SID) or SAM account name.
You can also specify user, computer, and group object variables, such as $\<localUserObject\>.
If you are specifying more than one new member, use a comma-separated list.
You cannot pass user, computer, or group objects through the pipeline to this cmdlet.
To add user, computer, or group objects to a group by using the pipeline, use the Add-ADPrincipalGroupMembership cmdlet.

For AD LDS environments, the Partition parameter must be specified except in the following two conditions:

-The cmdlet is run from an Active Directory provider drive.

-A default naming context or partition is defined for the AD LDS environment.
To specify a default naming context for an AD LDS environment, set the msDS-defaultNamingContext property of the Active Directory directory service agent (DSA) object (nTDSDSA) for the AD LDS instance.

## EXAMPLES

### -------------------------- EXAMPLE 1 --------------------------
```
C:\PS>Add-ADGroupMember SvcAccPSOGroup SQL01,SQL02
```

Description

-----------

Adds the user accounts with SamAccountNames SQL01,SQL02 to the group SvcAccPSOGroup.

### -------------------------- EXAMPLE 2 --------------------------
```
C:\PS>Add-ADGroupMember

cmdlet Add-ADGroupMember at command pipeline position 1
Supply values for the following parameters:
Identity: RodcAdmins
Members[0]: JohnSmith
Members[1]: JeffPrice
Members[2]:
```

Description

-----------

Demonstrates default behavior for this cmdlet (no parameters specified).
Adds user accounts with SamAccountNames JohnSmith and JeffPrice to the group RodcAdmins.

### -------------------------- EXAMPLE 3 --------------------------
```
C:\PS>Get-ADGroup -Server localhost:60000 -SearchBase "OU=AccountDeptOU,DC=AppNC" -filter "name -like 'AccountLeads'" | Add-ADGroupMember -Members "CN=SanjayPatel,OU=AccountDeptOU,DC=AppNC"
```

Description

-----------

Gets a group from the Organizational Unit "OU=AccountDeptOU,DC=AppNC" in the AD LDS instance localhost:60000 that has the name "AccountLeads" and then pipes it to Add-ADGroupMember, which then adds the user account with DistinguishedName "CN=SanjayPatel,OU=AccountDeptOU,DC=AppNC" to it.

### -------------------------- EXAMPLE 4 --------------------------
```
C:\PS>$user = Get-ADUser "CN=Glen John,OU=UserAccounts,DC=NORTHAMERICA,DC=FABRIKAM,DC=COM" -Server "northamerica.fabrikam.com";
$group = Get-ADGroup "CN=AccountLeads,OU=UserAccounts,DC=EUROPE,DC=FABRIKAM,DC=COM" -Server "europe.fabrikam.com";
Add-ADGroupMember $group -Members $user -Server "europe.fabrikam.com"
```

Description

-----------

Adds the user "CN=Glen John,OU=UserAccounts" from the North America domain to the group "CN=AccountLeads,OU=UserAccounts" in the Europe domain.

## PARAMETERS

### -AuthType
Specifies the authentication method to use.
Possible values for this parameter include:

Negotiate or 0

Basic or 1

The default authentication method is Negotiate.

A Secure Sockets Layer (SSL) connection is required for the Basic authentication method.

The following example shows how to set this parameter to Basic.

-AuthType Basic

```yaml
Type: ADAuthType
Parameter Sets: (All)
Aliases: 
Accepted values: Negotiate, Basic

Required: False
Position: Named
Default value: Microsoft.ActiveDirectory.Management.AuthType.Negotiate
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

### -Credential
Specifies the user account credentials to use to perform this task.
The default credentials are the credentials of the currently logged on user unless the cmdlet is run from an Active Directory PowerShell provider drive.
If the cmdlet is run from such a provider drive, the account associated with the drive is the default.

To specify this parameter, you can type a user name, such as "User1" or "Domain01\User01" or you can specify a PSCredential object.
If you specify a user name for this parameter, the cmdlet prompts for a password.

You can also create a PSCredential object by using a script or by using the Get-Credential cmdlet.
You can then set the Credential parameter to the PSCredential object The following example shows how to create credentials.

$AdminCredentials = Get-Credential "Domain01\User01"

The following shows how to set the Credential parameter to these credentials.

-Credential $AdminCredentials

If the acting credentials do not have directory-level permission to perform the task, Active Directory PowerShell returns a terminating error.

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

### -Identity
Specifies an Active Directory group object by providing one of the following values.
The identifier in parentheses is the LDAP display name for the attribute.

Distinguished Name

Example: CN=saradavisreports,OU=europe,CN=users,DC=corp,DC=contoso,DC=com

GUID (objectGUID)

Example: 599c3d2e-f72d-4d20-8a88-030d99495f20

Security Identifier (objectSid)

Example: S-1-5-21-3165297888-301567370-576410423-1103

Security Accounts Manager (SAM) Account Name (sAMAccountName)

Example: saradavisreports

The cmdlet searches the default naming context or partition to find the object.
If two or more objects are found, the cmdlet returns a non-terminating error.

This parameter can also get this object through the pipeline or you can set this parameter to an object instance.

This example shows how to set the parameter to a distinguished name.

-Identity  "CN=saradavisreports,OU=europe,CN=users,DC=corp,DC=contoso,DC=com"

This example shows how to set this parameter to a group object instance named "ADGroupInstance".

-Identity $ADGroupInstance

```yaml
Type: ADGroup
Parameter Sets: (All)
Aliases: 

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Members
Specifies a set of user, group, and computer objects in a comma-separated list to add to a group.
To identify each object, use one of the following property values.
Note: The identifier in parentheses is the LDAP display name.

Distinguished Name

Example:  CN=SaraDavis,CN=Europe,CN=Users,DC=corp,DC=contoso,DC=com

GUID (objectGUID)

Example: 599c3d2e-f72d-4d20-8a88-030d99495f20

Security Identifier (objectSid)

Example: S-1-5-21-3165297888-301567370-576410423-1103

SAM Account Name (sAMAccountName)

Example: saradavis

You can also provide objects to this parameter directly.

The following examples show how to specify this parameter.

This example specifies a user and group to add by specifying the distinguished name and the SAM Account Name properties.

-Members "CN=SaraDavis,CN=employees,CN=Users,DC=contoso,DC=com", "saradavisreports"

This example specifies a user and a group object that are defined in the current Windows PowerShell session as input for the parameter.

-Members $userObject, $groupObject

The objects specified for this parameter are processed as Microsoft.ActiveDirectory.Management.ADPrincipal objects.
Derived types, such as the following are also received by this parameter.

Microsoft.ActiveDirectory.Management.ADUser

Microsoft.ActiveDirectory.Management.ADComputer

Microsoft.ActiveDirectory.Management.ADServiceAccount

Microsoft.ActiveDirectory.Management.ADGroup

You cannot pass objects through the pipeline to this parameter.

```yaml
Type: ADPrincipal[]
Parameter Sets: (All)
Aliases: 

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Partition
Specifies the distinguished name of an Active Directory partition.
The distinguished name must be one of the naming contexts on the current directory server.
The cmdlet searches this partition to find the object defined by the Identity parameter.

The following two examples show how to specify a value for this parameter.

-Partition "CN=Configuration,DC=EUROPE,DC=TEST,DC=CONTOSO,DC=COM"

-Partition "CN=Schema,CN=Configuration,DC=EUROPE,DC=TEST,DC=CONTOSO,DC=COM"

In many cases, a default value will be used for the Partition parameter if no value is specified. 
The rules for determining the default value are given below. 
Note that rules listed first are evaluated first and once a default value can be determined, no further rules will be evaluated.

In AD DS environments, a default value for Partition will be set in the following cases:  - If the Identity parameter is set to a distinguished name, the default value of Partition is automatically generated from this distinguished name.

- If running cmdlets from an Active Directory provider drive, the default value of Partition is automatically generated from the current path in the drive.
- If none of the previous cases apply, the default value of Partition will be set to the default partition or naming context of the target domain.

In AD LDS environments, a default value for Partition will be set in the following cases:

- If the Identity parameter is set to a distinguished name, the default value of Partition is automatically generated from this distinguished name.
- If running cmdlets from an Active Directory provider drive, the default value of Partition is automatically generated from the current path in the drive.
- If the target AD LDS instance has a default naming context, the default value of Partition will be set to the default naming context.  To specify a default naming context for an AD LDS environment, set the msDS-defaultNamingContext property of the Active Directory directory service agent (DSA) object (nTDSDSA) for the AD LDS instance.
- If none of the previous cases apply, the Partition parameter will not take any default value.

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

### -PassThru
Returns the new or modified object.
By default (i.e.
if -PassThru is not specified), this cmdlet does not generate any output.

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

### -Server
Specifies the Active Directory Domain Services instance to connect to, by providing one of the following values for a corresponding domain name or directory server.
The service may be any of the following:  Active Directory Lightweight Domain Services, Active Directory Domain Services or Active Directory Snapshot instance.

Domain name values:

Fully qualified domain name

Examples: corp.contoso.com

NetBIOS name

Example: CORP

Directory server values:

Fully qualified directory server name

Example: corp-DC12.corp.contoso.com

NetBIOS name

Example: corp-DC12

Fully qualified directory server name and port

Example: corp-DC12.corp.contoso.com:3268

The default value for the Server parameter is determined by one of the following methods in the order that they are listed:

-By using Server value from objects passed through the pipeline.

-By using the server information associated with the Active Directory PowerShell provider drive, when running under that drive.

-By using the domain of the computer running Windows PowerShell.

The following example shows how to specify a full qualified domain name as the parameter value.

-Server "corp.contoso.com"

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
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### Microsoft.ActiveDirectory.Management.ADGroup
A group object is received by the Identity parameter.

## OUTPUTS

### None or Microsoft.ActiveDirectory.Management.ADGroup
Returns the modified group object when the PassThru parameter is specified.
By default, this cmdlet does not generate any output.

## NOTES
* This cmdlet does not work with a read-only domain controller.
* This cmdlet does not work with an Active Directory snapshot.
* This cmdlet will allow you to add a group as a member of itself which could lead to unstable behavior.

## RELATED LINKS

[Add-ADPrincipalGroupMembership](./Add-ADPrincipalGroupMembership.md)

[Get-ADGroup](./Get-ADGroup.md)

[Get-ADGroupMember](./Get-ADGroupMember.md)

[Get-ADPrincipalGroupMembership](./Get-ADPrincipalGroupMembership.md)

[Remove-ADGroupMember](./Remove-ADGroupMember.md)

[Remove-ADPrincipalGroupMembership](./Remove-ADPrincipalGroupMembership.md)

