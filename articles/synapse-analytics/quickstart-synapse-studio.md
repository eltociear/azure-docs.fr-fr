---
title: Utiliser Synapse Studio (préversion)
description: Dans ce guide de démarrage rapide, vous allez voir et découvrir à quel point il est facile d’interroger différents types de fichiers en utilisant Synapse Studio.
services: synapse-analytics
author: jovanpop-msft
ms.service: synapse-analytics
ms.topic: quickstart
ms.subservice: ''
ms.date: 04/15/2020
ms.author: jovanpop
ms.reviewer: jrasnick, carlrab
ms.openlocfilehash: 64895e5f48168305aea3e83596cdbcae982a6cb9
ms.sourcegitcommit: 366e95d58d5311ca4b62e6d0b2b47549e06a0d6d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82692425"
---
# <a name="quickstart-using-synapse-studio-preview"></a>Démarrage rapide : Utilisation de Synapse Studio (préversion)

Dans ce guide de démarrage rapide, vous allez apprendre à interroger des fichiers à l’aide de Synapse Studio.

Si vous n’avez pas d’abonnement Azure, créez un compte [gratuit](https://azure.microsoft.com/free/) avant de commencer.

## <a name="sign-in-to-the-azure-portal"></a>Connectez-vous au portail Azure.

Connectez-vous au [portail Azure](https://portal.azure.com/).

## <a name="prerequisites"></a>Prérequis

[Créez un espace de travail Azure Synapse et un compte de stockage associé](quickstart-create-workspace.md).

## <a name="launch-synapse-studio"></a>Lancer Synapse Studio

Dans votre espace de travail Azure Synapse au sein du portail Azure, cliquez sur **Lancer Synapse Studio**.

![Lancer Synapse Studio](./media/quickstart-synapse-studio/launch-synapse-workspace.png)

Vous pouvez également lancer Synapse Studio en cliquant sur [Azure Synapse Analytics](https://web.azuresynapse.net) et en fournissant les valeurs appropriées pour le locataire, l’abonnement et l’espace de travail.

## <a name="browse-storage-accounts"></a>Parcourir les comptes de stockage

Une fois que vous ouvrez Synapse Studio, accédez à **Données**, puis développez **Comptes de stockage** pour afficher le compte de stockage dans l’espace de travail.

![Parcourir les fichiers sur le stockage](./media/quickstart-synapse-studio/browse-files-on-storage.png)

Vous pouvez créer des dossiers et charger des fichiers à l’aide des liens de la barre d’outils pour organiser vos fichiers.

## <a name="query-files-on-storage-account"></a>Interroger des fichiers sur le compte de stockage

> [!IMPORTANT]
> Vous devez être membre du rôle `Storage Blob Reader` sur le stockage sous-jacent afin de pouvoir interroger les fichiers. Découvrez comment [affecter des autorisations RBAC **Lecteur des données Blob du stockage** ou **Contributeur aux données Blob du stockage** sur Stockage Azure](../storage/common/storage-auth-aad-rbac-portal.md?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json#assign-a-built-in-rbac-role).

1. Chargez certains fichiers `PARQUET`.
2. Sélectionnez un ou plusieurs fichiers, puis créez un script SQL ou un notebook Spark pour voir le contenu des fichiers. Si vous souhaitez créer un notebook, vous devez créer un [pool Apache Spark dans l’espace de travail](quickstart-create-apache-spark-pool.md).

   ![Interroger des fichiers sur le stockage](./media/quickstart-synapse-studio/query-files-on-storage.png)

3. Exécutez la requête ou le notebook générés pour voir le contenu du fichier.

   ![Voir le contenu du fichier](./media/quickstart-synapse-studio/query-files-on-storage-result.png)

4. Vous pouvez changer la requête pour filtrer et trier les résultats. Pour découvrir les fonctionnalités de langage disponibles dans SQL à la demande, consultez la [présentation des fonctionnalités SQL](sql/overview-features.md).

## <a name="next-steps"></a>Étapes suivantes

- Autoriser les utilisateurs Azure AD à interroger des fichiers en affectant des autorisations RBAC [**Lecteur des données Blob du stockage** ou **Contributeur aux données Blob du stockage** sur Stockage Azure](../storage/common/storage-auth-aad-rbac-portal.md?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json#assign-a-built-in-rbac-role)
- [Interroger des fichiers sur le Stockage Azure à l’aide de SQL à la demande](sql/on-demand-workspace-overview.md)
- [Créer un pool Apache Spark à l’aide du portail Azure](quickstart-create-apache-spark-pool.md)
- [Créer un rapport Power BI sur les fichiers stockés sur le Stockage Azure](sql/tutorial-connect-power-bi-desktop.md)
