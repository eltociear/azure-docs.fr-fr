---
title: Lister les définitions de rôles dans le RBAC Azure avec le portail Azure, Azure PowerShell, Azure CLI ou l’API REST | Microsoft Docs
description: Découvrez comment lister les rôles intégrés et personnalisés dans le RBAC Azure en utilisant le portail Azure, Azure PowerShell, Azure CLI ou l’API REST.
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: role-based-access-control
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/19/2020
ms.author: rolyon
ms.reviewer: bagovind
ms.openlocfilehash: aa888eedc81ceb3188f801e273c70722207bf512
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2020
ms.locfileid: "80062981"
---
# <a name="list-role-definitions-in-azure-rbac"></a>Lister les définitions de rôles dans le RBAC Azure

Une définition de rôle est une collection d’autorisations qui peuvent être effectuées, comme lire, écrire et supprimer. Elle est généralement simplement appelée « rôle ». Le [contrôle d’accès en fonction du rôle (RBAC) Azure](overview.md) compte plus de 120 [rôles intégrés](built-in-roles.md). Vous pouvez également créer vos propres rôles personnalisés. Cet article explique comment lister les rôles intégrés et personnalisés que vous pouvez utiliser pour accorder l’accès aux ressources Azure.

Pour voir la liste des rôles d’administrateur pour Azure Active Directory, consultez [Autorisations des rôles d’administrateur dans Azure Active Directory](../active-directory/users-groups-roles/directory-assign-admin-roles.md).

## <a name="azure-portal"></a>Portail Azure

### <a name="list-all-roles"></a>Répertorier tous les rôles

Suivez ces étapes pour lister tous les rôles dans le portail Azure.

1. Dans le portail Azure, cliquez sur **Tous les services**, puis sélectionnez n’importe quelle étendue. Par exemple, vous pouvez sélectionner **Groupes d’administration**, **Abonnements**, **Groupes de ressources**, ou une ressource.

1. Cliquez sur la ressource spécifique.

1. Cliquez sur **Contrôle d’accès (IAM)** .

1. Cliquez sur l’onglet **Rôles** pour afficher une liste de tous les rôles intégrés et personnalisés.

   Vous pouvez voir le nombre d’utilisateurs et de groupes affectés à chaque rôle dans cette étendue.

   ![Liste de rôles](./media/role-definitions-list/roles-list.png)

## <a name="azure-powershell"></a>Azure PowerShell

### <a name="list-all-roles"></a>Répertorier tous les rôles

Pour lister tous les rôles dans Azure PowerShell, utilisez [Get-AzRoleDefinition](/powershell/module/az.resources/get-azroledefinition).

```azurepowershell
Get-AzRoleDefinition | FT Name, Description
```

```Example
AcrImageSigner                                    acr image signer
AcrQuarantineReader                               acr quarantine data reader
AcrQuarantineWriter                               acr quarantine data writer
API Management Service Contributor                Can manage service and the APIs
API Management Service Operator Role              Can manage service but not the APIs
API Management Service Reader Role                Read-only access to service and APIs
Application Insights Component Contributor        Can manage Application Insights components
Application Insights Snapshot Debugger            Gives user permission to use Application Insights Snapshot Debugge...
Automation Job Operator                           Create and Manage Jobs using Automation Runbooks.
Automation Operator                               Automation Operators are able to start, stop, suspend, and resume ...
...
```

### <a name="list-a-role-definition"></a>Lister les définitions de rôle

Pour lister les détails d’un rôle spécifique, utilisez [Get-AzRoleDefinition](/powershell/module/az.resources/get-azroledefinition).

```azurepowershell
Get-AzRoleDefinition <role_name>
```

```Example
PS C:\> Get-AzRoleDefinition "Contributor"

Name             : Contributor
Id               : b24988ac-6180-42a0-ab88-20f7382dd24c
IsCustom         : False
Description      : Lets you manage everything except access to resources.
Actions          : {*}
NotActions       : {Microsoft.Authorization/*/Delete, Microsoft.Authorization/*/Write,
                   Microsoft.Authorization/elevateAccess/Action}
DataActions      : {}
NotDataActions   : {}
AssignableScopes : {/}
```

### <a name="list-a-role-definition-in-json-format"></a>Lister les définitions de rôle au format JSON

Pour lister un rôle au format JSON, utilisez [Get-AzRoleDefinition](/powershell/module/az.resources/get-azroledefinition).

```azurepowershell
Get-AzRoleDefinition <role_name> | ConvertTo-Json
```

```Example
PS C:\> Get-AzRoleDefinition "Contributor" | ConvertTo-Json

{
  "Name": "Contributor",
  "Id": "b24988ac-6180-42a0-ab88-20f7382dd24c",
  "IsCustom": false,
  "Description": "Lets you manage everything except access to resources.",
  "Actions": [
    "*"
  ],
  "NotActions": [
    "Microsoft.Authorization/*/Delete",
    "Microsoft.Authorization/*/Write",
    "Microsoft.Authorization/elevateAccess/Action",
    "Microsoft.Blueprint/blueprintAssignments/write",
    "Microsoft.Blueprint/blueprintAssignments/delete"
  ],
  "DataActions": [],
  "NotDataActions": [],
  "AssignableScopes": [
    "/"
  ]
}
```

### <a name="list-permissions-of-a-role-definition"></a>Lister les autorisations d’une définition de rôle

Pour lister les autorisations pour un rôle spécifique, utilisez [Get-AzRoleDefinition](/powershell/module/az.resources/get-azroledefinition).

```azurepowershell
Get-AzRoleDefinition <role_name> | FL Actions, NotActions
```

```Example
PS C:\> Get-AzRoleDefinition "Contributor" | FL Actions, NotActions

Actions    : {*}
NotActions : {Microsoft.Authorization/*/Delete, Microsoft.Authorization/*/Write,
             Microsoft.Authorization/elevateAccess/Action,
             Microsoft.Blueprint/blueprintAssignments/write...}
```

```azurepowershell
(Get-AzRoleDefinition <role_name>).Actions
```

```Example
PS C:\> (Get-AzRoleDefinition "Virtual Machine Contributor").Actions

Microsoft.Authorization/*/read
Microsoft.Compute/availabilitySets/*
Microsoft.Compute/locations/*
Microsoft.Compute/virtualMachines/*
Microsoft.Compute/virtualMachineScaleSets/*
Microsoft.DevTestLab/schedules/*
Microsoft.Insights/alertRules/*
Microsoft.Network/applicationGateways/backendAddressPools/join/action
Microsoft.Network/loadBalancers/backendAddressPools/join/action
...
```

## <a name="azure-cli"></a>Azure CLI

### <a name="list-all-roles"></a>Répertorier tous les rôles

Pour lister tous les rôles dans Azure CLI, utilisez[az role definition list](/cli/azure/role/definition#az-role-definition-list).

```azurecli
az role definition list
```

L’exemple suivant liste le nom et la description de toutes les définitions de rôles disponibles :

```azurecli
az role definition list --output json | jq '.[] | {"roleName":.roleName, "description":.description}'
```

```Output
{
  "roleName": "API Management Service Contributor",
  "description": "Can manage service and the APIs"
}
{
  "roleName": "API Management Service Operator Role",
  "description": "Can manage service but not the APIs"
}
{
  "roleName": "API Management Service Reader Role",
  "description": "Read-only access to service and APIs"
}

...
```

L’exemple suivant liste tous les rôles intégrés.

```azurecli
az role definition list --custom-role-only false --output json | jq '.[] | {"roleName":.roleName, "description":.description, "roleType":.roleType}'
```

```Output
{
  "roleName": "API Management Service Contributor",
  "description": "Can manage service and the APIs",
  "roleType": "BuiltInRole"
}
{
  "roleName": "API Management Service Operator Role",
  "description": "Can manage service but not the APIs",
  "roleType": "BuiltInRole"
}
{
  "roleName": "API Management Service Reader Role",
  "description": "Read-only access to service and APIs",
  "roleType": "BuiltInRole"
}

...
```

### <a name="list-a-role-definition"></a>Lister les définitions de rôle

Pour lister les détails d’un rôle, utilisez [az role definition list](/cli/azure/role/definition#az-role-definition-list).

```azurecli
az role definition list --name <role_name>
```

L’exemple suivant liste la définition de rôle *Contributeur* :

```azurecli
az role definition list --name "Contributor"
```

```Output
[
  {
    "additionalProperties": {},
    "assignableScopes": [
      "/"
    ],
    "description": "Lets you manage everything except access to resources.",
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Authorization/roleDefinitions/b24988ac-6180-42a0-ab88-20f7382dd24c",
    "name": "b24988ac-6180-42a0-ab88-20f7382dd24c",
    "permissions": [
      {
        "actions": [
          "*"
        ],
        "additionalProperties": {},
        "dataActions": [],
        "notActions": [
          "Microsoft.Authorization/*/Delete",
          "Microsoft.Authorization/*/Write",
          "Microsoft.Authorization/elevateAccess/Action"
        ],
        "notDataActions": []
      }
    ],
    "roleName": "Contributor",
    "roleType": "BuiltInRole",
    "type": "Microsoft.Authorization/roleDefinitions"
  }
]
```

### <a name="list-permissions-of-a-role-definition"></a>Lister les autorisations d’une définition de rôle

L’exemple suivant liste simplement les *actions* et les *notActions* du rôle *Contributeur*.

```azurecli
az role definition list --name "Contributor" --output json | jq '.[] | {"actions":.permissions[0].actions, "notActions":.permissions[0].notActions}'
```

```Output
{
  "actions": [
    "*"
  ],
  "notActions": [
    "Microsoft.Authorization/*/Delete",
    "Microsoft.Authorization/*/Write",
    "Microsoft.Authorization/elevateAccess/Action"
  ]
}
```

L’exemple suivant liste simplement les actions du rôle *Contributeur de machines virtuelles*.

```azurecli
az role definition list --name "Virtual Machine Contributor" --output json | jq '.[] | .permissions[0].actions'
```

```Output
[
  "Microsoft.Authorization/*/read",
  "Microsoft.Compute/availabilitySets/*",
  "Microsoft.Compute/locations/*",
  "Microsoft.Compute/virtualMachines/*",
  "Microsoft.Compute/virtualMachineScaleSets/*",
  "Microsoft.Insights/alertRules/*",
  "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
  "Microsoft.Network/loadBalancers/backendAddressPools/join/action",

  ...

  "Microsoft.Storage/storageAccounts/listKeys/action",
  "Microsoft.Storage/storageAccounts/read"
]
```

## <a name="rest-api"></a>API REST

### <a name="list-role-definitions"></a>Lister les définitions de rôles

Pour répertorier les définitions de rôles, utilisez l’API REST [Définitions de rôles - Liste](/rest/api/authorization/roledefinitions/list). Pour affiner vos résultats, vous spécifiez une étendue et un filtre facultatif.

1. Commencez par la requête suivante :

    ```http
    GET https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?$filter={$filter}&api-version=2015-07-01
    ```

1. Dans l’URI, remplacez *{scope}* par l’étendue dont vous souhaitez lister les définitions de rôles.

    > [!div class="mx-tableFixed"]
    > | Étendue | Type |
    > | --- | --- |
    > | `providers/Microsoft.Management/managementGroups/{groupId1}` | Groupe d’administration |
    > | `subscriptions/{subscriptionId1}` | Abonnement |
    > | `subscriptions/{subscriptionId1}/resourceGroups/myresourcegroup1` | Resource group |
    > | `subscriptions/{subscriptionId1}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1` | Ressource |

    Dans l’exemple précédent, microsoft.web est un fournisseur de ressources qui fait référence à une instance App Service. De la même façon, vous pouvez utiliser tout autre fournisseur de ressources et spécifier l’étendue. Pour plus d’informations, consultez [Fournisseurs et types de ressources Azure](../azure-resource-manager/management/resource-providers-and-types.md) et [Opérations du fournisseur de ressources Azure Resource Manager](resource-provider-operations.md) prises en charge.  
     
1. Remplacez *{filter}* par la condition que vous voulez appliquer pour filtrer la liste des définitions de rôles.

    > [!div class="mx-tableFixed"]
    > | Filtrer | Description |
    > | --- | --- |
    > | `$filter=atScopeAndBelow()` | Répertorie les définitions de rôles pour l’étendue spécifiée et toutes les sous-étendues. |
    > | `$filter=type+eq+'{type}'` | Répertorie les définitions de rôles du type spécifié. Le type de rôle peut être `CustomRole` ou `BuiltInRole`. |

### <a name="list-a-role-definition"></a>Lister les définitions de rôle

Pour répertorier les détails d’un rôle spécifique, utilisez l'API REST [Role Definitions - Get](/rest/api/authorization/roledefinitions/get) ou [Role Definitions - Get By Id](/rest/api/authorization/roledefinitions/getbyid).

1. Commencez par la requête suivante :

    ```http
    GET https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{roleDefinitionId}?api-version=2015-07-01
    ```

    Pour une définition de rôle au niveau du répertoire, vous pouvez utiliser cette requête :

    ```http
    GET https://management.azure.com/providers/Microsoft.Authorization/roleDefinitions/{roleDefinitionId}?api-version=2015-07-01
    ```

1. Dans l’URI, remplacez *{scope}* par l’étendue dont vous souhaitez lister la définition de rôle.

    > [!div class="mx-tableFixed"]
    > | Étendue | Type |
    > | --- | --- |
    > | `providers/Microsoft.Management/managementGroups/{groupId1}` | Groupe d’administration |
    > | `subscriptions/{subscriptionId1}` | Abonnement |
    > | `subscriptions/{subscriptionId1}/resourceGroups/myresourcegroup1` | Resource group |
    > | `subscriptions/{subscriptionId1}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1` | Ressource |
     
1. Remplacez *{roleDefinitionId}* par l’identificateur de définition de rôle.

## <a name="next-steps"></a>Étapes suivantes

- [Rôles intégrés pour les ressources Azure](built-in-roles.md)
- [Rôles intégrés pour les ressources Azure](custom-roles.md)
- [Lister les attributions de rôles à l’aide du RBAC Azure et du portail Azure](role-assignments-list-portal.md)
- [Ajouter ou supprimer des attributions de rôles à l’aide du RBAC Azure et du portail Azure](role-assignments-portal.md)
