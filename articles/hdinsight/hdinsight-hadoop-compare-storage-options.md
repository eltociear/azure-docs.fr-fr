---
title: Comparer les options de stockage à utiliser avec les clusters Azure HDInsight
description: Fournit une vue d’ensemble des types de stockage et de leur fonctionnement avec Azure HDInsight.
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: conceptual
ms.custom: seoapr2020
ms.date: 04/21/2020
ms.openlocfilehash: ed93ba937a843618f36bac6e88b15ff77355ca75
ms.sourcegitcommit: 50ef5c2798da04cf746181fbfa3253fca366feaa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2020
ms.locfileid: "82610698"
---
# <a name="compare-storage-options-for-use-with-azure-hdinsight-clusters"></a>Comparer les options de stockage à utiliser avec les clusters Azure HDInsight

Vous pouvez choisir parmi plusieurs services de stockage Azure lors de la création de clusters HDInsight :

* [Stockage Azure](./overview-azure-storage.md)
* [Azure Data Lake Storage Gen2](./overview-data-lake-storage-gen2.md)
* [Azure Data Lake Storage Gen1](./overview-data-lake-storage-gen1.md)

Cet article fournit une vue d’ensemble de ces types de stockage, ainsi que de leurs caractéristiques uniques.

## <a name="storage-types-and-features"></a>Types de stockage et fonctionnalités

Le tableau suivant récapitule les services de stockage Azure pris en charge avec les différentes versions de HDInsight :

| Service de stockage | Type de compte | Type d’espace de noms | Services pris en charge | Niveaux de performances pris en charge | Niveaux d’accès pris en charge | Version de HDInsight | Type de cluster |
|---|---|---|---|---|---|---|---|
|Azure Data Lake Storage Gen2| Universel v2 | Hiérarchique (système de fichiers) | Objet blob | standard | Chaud, froid, archive | 3.6+ | Tout sauf Spark 2.1 et 2.2|
|Stockage Azure| Universel v2 | Object | Objet blob | standard | Chaud, froid, archive | 3.6+ | Tous |
|Stockage Azure| Universel v1 | Object | Objet blob | standard | N/A | Tous | Tous |
|Stockage Azure| Stockage Blob** | Object | Objet blob de blocs | standard | Chaud, froid, archive | Tous | Tous |
|Azure Data Lake Storage Gen1| N/A | Hiérarchique (système de fichiers) | N/A | N/A | N/A | 3.6 uniquement | Tout sauf HBase |

** Pour les clusters HDInsight, seuls les comptes de stockage secondaires peuvent être de type BlobStorage. Par ailleurs, les objets blob de pages ne font pas partie des options de stockage prises en charge.

Pour plus d’informations sur les types de comptes de stockage Azure, consultez l’article [Vue d’ensemble des comptes de stockage Azure](../storage/common/storage-account-overview.md).

Pour plus d’informations sur les niveaux d’accès du stockage Azure, consultez [Stockage Blob Azure : niveaux de stockage Premium (préversion), chaud, froid et archive](../storage/blobs/storage-blob-storage-tiers.md)

Vous pouvez créer des clusters à l’aide de combinaisons de services pour le stockage principal et le stockage secondaire facultatif. Le tableau suivant résume les configurations de stockage de cluster actuellement prises en charge dans HDInsight :

| Version de HDInsight | Stockage principal | Stockage secondaire | Prise en charge |
|---|---|---|---|
| 3.6 et 4.0 | Universel V1, Universel V2 | Universel V1, Universel V2, BlobStorage (objets blob de blocs) | Oui |
| 3.6 et 4.0 | Universel V1, Universel V2 | Data Lake Storage Gen2 | Non  |
| 3.6 et 4.0 | Data Lake Storage Gen2* | Data Lake Storage Gen2 | Oui |
| 3.6 et 4.0 | Data Lake Storage Gen2* | Universel V1, Universel V2, BlobStorage (objets blob de blocs) | Oui |
| 3.6 et 4.0 | Data Lake Storage Gen2 | Data Lake Storage Gen 1 | Non  |
| 3.6 | Data Lake Storage Gen 1 | Data Lake Storage Gen 1 | Oui |
| 3.6 | Data Lake Storage Gen 1 | Universel V1, Universel V2, BlobStorage (objets blob de blocs) | Oui |
| 3.6 | Data Lake Storage Gen 1 | Data Lake Storage Gen2 | Non  |
| 4.0 | Data Lake Storage Gen 1 | Quelconque | Non  |
| 4.0 | Universel V1, Universel V2 | Data Lake Storage Gen 1 | Non  |

* = Il peut s’agir d’un ou de plusieurs comptes Data Lake Storage Gen2, à condition qu’ils sont tous configurés pour utiliser la même identité managée pour l’accès au cluster.

> [!NOTE]
> Le stockage principal Data Lake Storage Gen2 n’est pas pris en charge pour les clusters Spark 2.1 ou 2.2.

## <a name="next-steps"></a>Étapes suivantes

* [Vue d’ensemble de Stockage Azure](./overview-azure-storage.md)
* [Vue d’ensemble d’Azure Data Lake Storage Gen1](./overview-data-lake-storage-gen1.md)
* [Vue d’ensemble d’Azure Data Lake Storage Gen2](./overview-data-lake-storage-gen2.md)
* [Présentation d’Azure Data Lake Storage Gen2](../storage/blobs/data-lake-storage-introduction.md)
* [Introduction à Azure Storage](../storage/common/storage-introduction.md)
