---
title: 'CLI Azure Service Fabric : sfctl mesh secret'
description: Apprenez-en plus sur sfctl, l’interface de ligne de commande d’Azure Service Fabric. Contient une liste de commandes pour l’obtention et la suppression de ressources de secret Service Fabric Mesh.
author: jeffj6123
ms.topic: reference
ms.date: 1/16/2020
ms.author: jejarry
ms.openlocfilehash: fab388ff223eb95020e2ba0945c76532bc54f224
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2020
ms.locfileid: "76905986"
---
# <a name="sfctl-mesh-secret"></a>sfctl mesh secret
Récupère et supprime les ressources mesh secret.

## <a name="commands"></a>Commandes

|Commande|Description|
| --- | --- |
| supprimer | Supprime la ressource Secret. |
| list | Répertorie toutes les ressources secrètes. |
| show | Récupère la ressource Secret portant le nom spécifié. |

## <a name="sfctl-mesh-secret-delete"></a>sfctl mesh secret delete
Supprime la ressource Secret.

Supprime la ressource Secret spécifiée et toutes ses valeurs nommées.

### <a name="arguments"></a>Arguments

|Argument|Description|
| --- | --- |
| --name -n [obligatoire] | Nom de la ressource secrète. |

### <a name="global-arguments"></a>Arguments globaux

|Argument|Description|
| --- | --- |
| --debug | Augmentez le niveau de détail de la journalisation pour afficher tous les journaux de débogage. |
| --help -h | Affichez ce message d’aide et quittez. |
| --output -o | Format de sortie.  Valeurs autorisées \: json, jsonc, table, tsv.  Valeur par défaut \: json. |
| --query | Chaîne de requêtes JMESPath. Pour obtenir plus d’informations et des exemples, consultez : http\://jmespath.org/. |
| --verbose | Augmentez le niveau de détail de la journalisation. Utilisez --debug pour des journaux de débogage complets. |

## <a name="sfctl-mesh-secret-list"></a>sfctl mesh secret list
Répertorie toutes les ressources secrètes.

Récupère les informations relatives à toutes les ressources secrètes d’un groupe de ressources donné. Les informations incluent la description et d’autres propriétés du Secret.

### <a name="global-arguments"></a>Arguments globaux

|Argument|Description|
| --- | --- |
| --debug | Augmentez le niveau de détail de la journalisation pour afficher tous les journaux de débogage. |
| --help -h | Affichez ce message d’aide et quittez. |
| --output -o | Format de sortie.  Valeurs autorisées \: json, jsonc, table, tsv.  Valeur par défaut \: json. |
| --query | Chaîne de requêtes JMESPath. Pour obtenir plus d’informations et des exemples, consultez : http\://jmespath.org/. |
| --verbose | Augmentez le niveau de détail de la journalisation. Utilisez --debug pour des journaux de débogage complets. |

## <a name="sfctl-mesh-secret-show"></a>sfctl mesh secret show
Récupère la ressource Secret portant le nom spécifié.

Récupère les informations relatives à la ressource Secret portant le nom spécifié. Les informations incluent la description et d’autres propriétés du Secret.

### <a name="arguments"></a>Arguments

|Argument|Description|
| --- | --- |
| --name -n [obligatoire] | Nom de la ressource secrète. |

### <a name="global-arguments"></a>Arguments globaux

|Argument|Description|
| --- | --- |
| --debug | Augmentez le niveau de détail de la journalisation pour afficher tous les journaux de débogage. |
| --help -h | Affichez ce message d’aide et quittez. |
| --output -o | Format de sortie.  Valeurs autorisées \: json, jsonc, table, tsv.  Valeur par défaut \: json. |
| --query | Chaîne de requêtes JMESPath. Pour obtenir plus d’informations et des exemples, consultez : http\://jmespath.org/. |
| --verbose | Augmentez le niveau de détail de la journalisation. Utilisez --debug pour des journaux de débogage complets. |


## <a name="next-steps"></a>Étapes suivantes
- [Configurez](service-fabric-cli.md) l’interface de ligne de commande Service Fabric.
- Découvrez comment utiliser l’interface de ligne de commande (CLI) Service Fabric à l’aide d’[exemples de scripts](/azure/service-fabric/scripts/sfctl-upgrade-application).