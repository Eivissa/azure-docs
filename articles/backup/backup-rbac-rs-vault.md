---
title: Manage Backups with Azure Role-Based Access Control'
description: Use Role-based Access Control to manage access to backup management operations in Recovery Services vault.
services: backup
author: trinadhk
manager: shreeshd
ms.service: backup
ms.topic: conceptual
ms.date: 7/11/2018
ms.author: trinadhk
---

# Use Role-Based Access Control to manage Azure Backup recovery points
Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure. Using RBAC, you can segregate duties within your team and grant only the amount of access to users that they need to perform their jobs.

> [!IMPORTANT]
> Roles provided by Azure Backup are limited to actions that can be performed in Azure portal or Recovery Services vault PowerShell cmdlets. Actions performed in Azure backup Agent Client UI or System center Data Protection Manager UI or Azure Backup Server UI are out of control of these roles.

Azure Backup provides 3 built-in roles to control backup management operations. Learn more on [Azure RBAC built-in roles](../role-based-access-control/built-in-roles.md)

* [Backup Contributor](../role-based-access-control/built-in-roles.md#backup-contributor) - This role has all permissions to create and manage backup except creating Recovery Services vault and giving access to others. Imagine this role as admin of backup management who can do every backup management operation.
* [Backup Operator](../role-based-access-control/built-in-roles.md#backup-operator) - This role has permissions to everything a contributor does except removing backup and managing backup policies. This role is equivalent to contributor except it can't perform destructive operations such as stop backup with delete data or remove registration of on-premises resources.
* [Backup Reader](../role-based-access-control/built-in-roles.md#backup-reader) - This role has permissions to view all backup management operations. Imagine this role to be a monitoring person.

If you're looking to define your own roles for even more control, see how to [build Custom roles](../role-based-access-control/custom-roles.md) in Azure RBAC.



## Mapping Backup built-in roles to backup management actions
The following table captures the Backup management actions and corresponding minimum RBAC role required to perform that operation.

| Management Operation | Minimum RBAC role required | Scope Required |
| --- | --- | --- |
| Create Recovery Services vault | Contributor | Resource group containing the vault |
| Enable backup of Azure VMs | Backup Operator | Resource group containing the vault |
| | Virtual Machine Contributor | VM resource |
| On-demand backup of VM | Backup Operator | Recovery vault resource |
| Restore VM | Backup Operator | Resource group in which VM will be deployed |
| | Virtual Machine Contributor | Resource group in which VM will be deployed |
| Restore unmanaged disks VM backup | Backup Operator | Recovery vault resource |
| | Virtual Machine Contributor | VM resource |
| | Storage Account Contributor | Storage account resource |
| Restore managed disks from VM backup | Backup Operator | Recovery vault resource |
| | Virtual Machine Contributor | VM resource |
| | Storage Account Contributor | Storage account resource |
| | Contributor | Resource group to which managed disk will be restored |
| Restore individual files from VM backup | Backup Operator | Recovery vault resource |
| | Virtual Machine Contributor | VM resource |
| Create backup policy for Azure VM backup | Backup Contributor | Recovery vault resource |
| Modify backup policy of Azure VM backup | Backup Contributor | Recovery vault resource |
| Delete backup policy of Azure VM backup | Backup Contributor | Recovery vault resource |
| Stop backup (with retain data or delete data) on VM backup | Backup Contributor | Recovery vault resource |
| Register on-premises Windows Server/client/SCDPM or Azure Backup Server | Backup Operator | Recovery vault resource |
| Delete registered on-premises Windows Server/client/SCDPM or Azure Backup Server | Backup Contributor | Recovery vault resource |

## Next steps
* [Role Based Access Control](../role-based-access-control/role-assignments-portal.md): Get started with RBAC in the Azure portal.
* Learn how to manage access with:
  * [PowerShell](../role-based-access-control/role-assignments-powershell.md)
  * [Azure CLI](../role-based-access-control/role-assignments-cli.md)
  * [REST API](../role-based-access-control/role-assignments-rest.md)
* [Role-Based Access Control troubleshooting](../role-based-access-control/troubleshooting.md): Get suggestions for fixing common issues.
