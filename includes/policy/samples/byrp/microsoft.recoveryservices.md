---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 05/13/2020
ms.author: dacoulte
ms.custom: generated
ms.openlocfilehash: bf8b98db98faf2aef3e634518da4914d46142739
ms.sourcegitcommit: fdec8e8bdbddcce5b7a0c4ffc6842154220c8b90
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83635816"
---
|Nom |Description |Effet(s) |Version |GitHub |
|---|---|---|---|---|
|[La sauvegarde Azure doit être activée pour les machines virtuelles](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F013e242c-8828-4970-87b3-ab247555486d) |Cette stratégie permet de vérifier si le service Sauvegarde Azure est activé pour toutes les machines virtuelles. Sauvegarde Azure est une solution de sauvegarde économique en un clic, qui simplifie la récupération des données et peut être activée plus facilement que d’autres services de sauvegarde cloud. |AuditIfNotExists, Désactivé |1.0.0 |[Lien](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Backup/VirtualMachines_EnableAzureBackup_Audit.json) |
|[Configurer la sauvegarde sur les machines virtuelles d’un emplacement dans un coffre central existant au même emplacement](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F09ce66bc-1220-4153-8104-e3f51c936913) |Cette stratégie configure la protection de Sauvegarde Azure sur les machines virtuelles d’un emplacement donné dans un coffre central existant au même emplacement. Elle s’applique uniquement aux machines virtuelles qui ne sont pas déjà configurées pour la sauvegarde. Nous vous recommandons de ne pas attribuer cette stratégie à plus de 200 machines virtuelles. Si la stratégie est attribuée à plus de 200 machines virtuelles, la sauvegarde peut être déclenchée quelques heures après la planification définie. Cette stratégie sera améliorée pour prendre en charge davantage d’images de machine virtuelle. |deployIfNotExists, auditIfNotExists, désactivé |1.0.0 |[Lien](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Backup/VirtualMachineBackup_Backup_DeployIfNotExists.json) |
|[Déployez les paramètres de diagnostic du coffre Recovery Services sur l’espace de travail Log Analytics pour les catégories propres à une ressource.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc717fb0c-d118-4c43-ab3d-ece30ac81fb3) |Déployez les paramètres de diagnostic du coffre Recovery Services afin de les envoyer vers l’espace de travail Log Analytics pour les catégories propres à une ressource. Si l’une des catégories propres à la ressource n’est pas activée, un nouveau paramètre de diagnostic est créé. |deployIfNotExists |1.0.0-preview |[Lien](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Monitoring/EnableRecoveryServiceVaultDiagnosticSetting_Backup_DeployIfNotExist.json) |
