---
title: Guide pratique pour auditer les opérations de plan de contrôle Azure Cosmos DB
description: Découvrez comment auditer les opérations de plan de contrôle telles que l’ajout d’une région, la mise à jour du débit, le basculement de région, l’ajout d’un réseau virtuel, etc., dans Azure Cosmos DB
author: SnehaGunda
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 04/23/2020
ms.author: sngun
ms.openlocfilehash: a5df7866f7897109dbd7a0ea8a52b857ab671875
ms.sourcegitcommit: 4499035f03e7a8fb40f5cff616eb01753b986278
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2020
ms.locfileid: "82735349"
---
# <a name="how-to-audit-azure-cosmos-db-control-plane-operations"></a>Guide pratique pour auditer les opérations de plan de contrôle Azure Cosmos DB

Dans Azure Cosmos DB, le plan de contrôle est un service RESTful qui vous permet d’effectuer un ensemble diversifié d’opérations sur le compte Azure Cosmos. Il expose un modèle de ressource publique (par exemple, une base de données ou un compte) et différentes opérations aux utilisateurs finaux pour effectuer des actions sur le modèle de ressource. Les opérations de plan de contrôle incluent les modifications apportées au compte ou au conteneur Azure Cosmos. Par exemple, des opérations telles que la création d’un compte Azure Cosmos, l’ajout d’une région, la mise à jour du débit, le basculement de région, l’ajout d’un réseau virtuel, etc., sont des opérations de plan de contrôle. Cet article explique comment auditer les opérations de plan de contrôle dans Azure Cosmos DB. Vous pouvez exécuter les opérations du plan de contrôle sur les comptes Azure Cosmos à l’aide d’Azure CLI, de PowerShell ou du Portail Azure, tandis que pour les conteneurs, vous devez utiliser Azure CLI ou PowerShell.

Voici quelques exemples de scénarios dans lesquels l’audit des opérations du plan de contrôle est utile :

* Vous souhaitez recevoir une alerte lorsque les règles de pare-feu pour votre compte Azure Cosmos sont modifiées. L’alerte est nécessaire pour détecter les modifications non autorisées des règles qui régissent la sécurité réseau de votre compte Azure Cosmos et agir rapidement.

* Vous souhaitez recevoir une alerte si une région est ajoutée ou supprimée de votre compte Azure Cosmos. L’ajout ou la suppression de régions a des implications sur les exigences en matière de facturation et de souveraineté des données. Cette alerte vous permet de détecter l’ajout ou la suppression accidentels de la région sur votre compte.

* Vous souhaitez obtenir plus de détails dans les journaux de diagnostic sur ce qui a changé. Par exemple, un réseau virtuel a été modifié.

## <a name="disable-key-based-metadata-write-access"></a>Désactiver l’accès en écriture aux métadonnées basé sur les clés

Avant d’auditer les opérations de plan de contrôle dans Azure Cosmos DB, désactivez l’accès en écriture aux métadonnées basé sur les clés sur votre compte. Quand l’accès en écriture aux métadonnées basé sur les clés est désactivé, les clients qui se connectent au compte Azure Cosmos par le biais de clés de compte ne peuvent pas accéder au compte. Vous pouvez désactiver l’accès en écriture en affectant à la propriété `disableKeyBasedMetadataWriteAccess` la valeur true. Une fois cette propriété définie, les modifications apportées à une ressource peuvent être effectuées par un utilisateur qui a le rôle de contrôle d’accès en fonction du rôle (RBAC) et les informations d’identification appropriés. Pour en savoir plus sur la définition de cette propriété, consultez l’article [Prévention des modifications à partir des SDK](role-based-access-control.md#preventing-changes-from-cosmos-sdk). 

Une fois le `disableKeyBasedMetadataWriteAccess` activé, si les clients basés sur le kit de développement logiciel (SDK) exécutent des opérations de création ou de mise à jour, une erreur *« l’opération « POST » sur la ressource « ContainerNameorDatabaseName » n’est pas autorisée via le point de terminaison Azure Cosmos DB* est retournée. Vous devez activer l’accès à ces opérations pour votre compte ou effectuer les opérations de création/mise à jour via Azure Resource Manager, Azure CLI ou Azure PowerShell. Pour revenir en arrière, définissez la valeur de disableKeyBasedMetadataWriteAccess sur **false** à l’aide de Azure CLI comme décrit dans l’article [Éviter les modifications dans le kit de développement logiciel (SDK) Cosmos](role-based-access-control.md#preventing-changes-from-cosmos-sdk). Veillez à remplacer la valeur de `disableKeyBasedMetadataWriteAccess` par false au lieu de true.

Tenez compte des points suivants lors de la désactivation de l’accès en écriture aux métadonnées :

* Vérifiez que vos applications n’effectuent pas d’appels de métadonnées qui changent les ressources mentionnées plus haut (par exemple, création d’une collection, mise à jour du débit, etc.) à l’aide du SDK ou de clés de compte.

* Comme le portail Azure utilise des clés de compte pour les opérations de métadonnées, ces opérations sont bloquées. Vous pouvez également utiliser Azure CLI, les kits SDK ou les déploiements de modèle Resource Manager pour effectuer ces opérations.

## <a name="enable-diagnostic-logs-for-control-plane-operations"></a>Activer les journaux de diagnostic pour les opérations de plan de contrôle

Vous pouvez activer les journaux de diagnostic pour les opérations de plan de contrôle à l’aide du portail Azure. Après l’activation, les journaux de diagnostic enregistrent l’opération en tant que paire d’événements de démarrage et de fin avec des détails pertinents. Par exemple, les *RegionFailoverStart* et *RegionFailoverComplete* terminent l’événement de basculement de la région.

Effectuez les étapes suivantes pour activer la journalisation sur les opérations du plan de contrôle :

1. Connectez-vous au [portail Azure](https://portal.azure.com) et accédez à votre compte Azure Cosmos.

1. Ouvrez le volet **Paramètres de diagnostic**, puis fournissez un **Nom** pour les journaux à créer.

1. Sélectionnez **ControlPlaneRequests** comme type de journal et sélectionnez l’option **Envoyer à Log Analytics**.

Vous pouvez également stocker les journaux dans un compte de stockage ou les transmettre à un hub d’événements. Cet article explique comment envoyer des journaux à Log Analytics, puis les interroger. Une fois l’activation effectuée, la prise en compte des journaux de diagnostic prend quelques minutes. Toutes les opérations de plan de contrôle effectuées par la suite peuvent faire l’objet d’un suivi. La capture d’écran suivante montre comment activer les journaux du plan de contrôle :

![Activer la journalisation des demandes du plan de contrôle](./media/audit-control-plane-logs/enable-control-plane-requests-logs.png)

## <a name="view-the-control-plane-operations"></a>Afficher les opérations de plan de contrôle

Après avoir activé la journalisation, suivez les étapes ci-dessous pour effectuer le suivi des opérations d’un compte spécifique :

1. Connectez-vous au [portail Azure](https://portal.azure.com).

1. Ouvrez l’onglet **Superviser** à partir de la barre de navigation de gauche, puis sélectionnez le volet **Journaux**. Une interface utilisateur s’ouvre, dans laquelle vous pouvez facilement exécuter des requêtes avec ce compte spécifique dans l’étendue. Exécutez la requête suivante pour voir les journaux du plan de contrôle :

   ```kusto
   AzureDiagnostics
   | where ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="ControlPlaneRequests"
   | where TimeGenerated >= ago(1h)
   ```

Les captures d’écran suivantes capturent des journaux lorsqu’un niveau de cohérence est modifié par un compte Azure Cosmos :

![Journaux du plan de contrôle lors de l’ajout d’un réseau virtuel](./media/audit-control-plane-logs/add-ip-filter-logs.png)

La capture d’écran suivante montre les journaux générés lors de la mise à jour du débit d’une table Cassandra :

![Journaux du plan de contrôle lors de la mise à jour du débit](./media/audit-control-plane-logs/throughput-update-logs.png)

## <a name="identify-the-identity-associated-to-a-specific-operation"></a>Identifier l’identité associée à une opération spécifique

Si vous souhaitez effectuer un débogage supplémentaire, vous pouvez identifier une opération spécifique dans le **journal d’activité** à l’aide de l’ID d’activité ou de l’horodatage de l’opération. L’horodatage est utilisé pour certains clients Resource Manager dans les cas où l’ID d’activité n’est pas explicitement passée. Le journal d’activité fournit des détails sur l’identité sous laquelle l’opération a été lancée. La capture d’écran suivante montre comment utiliser l’ID d’activité et rechercher les opérations qui lui sont associées dans le journal d’activité :

![Utiliser l’ID d’activité et rechercher les opérations](./media/audit-control-plane-logs/find-operations-with-activity-id.png)

## <a name="control-plane-operations-for-azure-cosmos-account"></a>Opérations du plan de contrôle pour le compte Azure Cosmos

Voici les opérations du plan de contrôle accessibles au niveau du compte. La plupart des opérations sont suivies au niveau du compte. Ces opérations sont accessibles en tant que métriques dans Azure Monitor :

* Région ajoutée
* Région supprimée
* Compte supprimé
* Région basculée
* Compte créé
* Réseau virtuel supprimé
* Paramètres réseau de compte mis à jour
* Paramètres de réplication de compte mis à jour
* Clés de compte mises à jour
* Paramètres de sauvegarde du compte mis à jour
* Paramètres de diagnostic du compte mis à jour

## <a name="control-plane-operations-for-database-or-containers"></a>Opérations du plan de contrôle pour la base de données ou les conteneurs

Voici les opérations du plan de contrôle accessibles au niveau de la base de données et di conteneur. Ces opérations sont accessibles en tant que métriques dans Azure Monitor :

* Base de données SQL mise à jour
* Conteneur SQL mis à jour
* Débit de base de données SQL mis à jour
* Débit de conteneur SQL mis à jour
* Base de données SQL supprimée
* Conteneur SQL supprimé
* Espace de clés Cassandra mis à jour
* Table Cassandra mise à jour
* Débit d’espace de clés Cassandra mis à jour
* Débit de table Cassandra mis à jour
* Espace de clés Cassandra supprimé
* Table Cassandra supprimée
* Base de données Gremlin mise à jour
* Graphique Gremlin mis à jour
* Débit de base de données Gremlin mis à jour
* Débit de graphique Gremlin mis à jour
* Base de données Gremlin supprimée
* Graphique Gremlin supprimé
* Base de données Mongo mise à jour
* Collection Mongo mise à jour
* Débit de base de données Mongo mis à jour
* Débit de collection Mongo mis à jour
* Base de données Mongo supprimée
* Collection Mongo supprimée
* Table AzureTable mise à jour
* Débit de table AzureTable mis à jour
* Table AzureTable supprimée

## <a name="diagnostic-log-operations"></a>Opérations sur le journal de diagnostic

Voici les noms d’opération dans les journaux de diagnostic pour différentes opérations :

* RegionAddStart, RegionAddComplete
* RegionRemoveStart, RegionRemoveComplete
* AccountDeleteStart, AccountDeleteComplete
* RegionFailoverStart, RegionFailoverComplete
* AccountCreateStart, AccountCreateComplete
* AccountUpdateStart, AccountUpdateComplete
* VirtualNetworkDeleteStart, VirtualNetworkDeleteComplete
* DiagnosticLogUpdateStart, DiagnosticLogUpdateComplete

Pour les opérations spécifiques à l’API, l’opération est nommée selon le format suivant :

* GenreApi + TypeRessourceGenreApi + TypeOpération + Start/Complete
* GenreApi + TypeRessourceGenreApi + « Throughput » + TypeOpération + Start/Complete

**Exemple** 

* CassandraKeyspacesUpdateStart, CassandraKeyspacesUpdateComplete
* CassandraKeyspacesThroughputUpdateStart, CassandraKeyspacesThroughputUpdateComplete
* SqlContainersUpdateStart, SqlContainersUpdateComplete

La propriété *ResourceDetails* contient l’intégralité du corps de la ressource en tant que charge utile de la demande, ainsi que toutes les propriétés requises pour la mise à jour.

## <a name="diagnostic-log-queries-for-control-plane-operations"></a>Requêtes de journaux de diagnostic pour les opérations de plan de contrôle

Voici quelques exemples pour obtenir des journaux de diagnostic pour les opérations de plan de contrôle :

```kusto
AzureDiagnostics 
| where Category =="ControlPlaneRequests"
| where  OperationName startswith "SqlContainersUpdateStart"
```

```kusto
AzureDiagnostics 
| where Category =="ControlPlaneRequests"
| where  OperationName startswith "SqlContainersThroughputUpdateStart"
```

## <a name="next-steps"></a>Étapes suivantes

* [Explorer Azure Monitor pour Azure Cosmos DB](../azure-monitor/insights/cosmosdb-insights-overview.md?toc=/azure/cosmos-db/toc.json&bc=/azure/cosmos-db/breadcrumb/toc.json)
* [Superviser et déboguer à l’aide de métriques dans Azure Cosmos DB](use-metrics.md)
