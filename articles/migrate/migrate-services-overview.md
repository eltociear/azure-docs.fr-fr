---
title: À propos d’Azure Migrate
description: Découvrez le service Azure Migrate.
ms.topic: overview
ms.date: 04/15/2020
ms.custom: mvc
ms.openlocfilehash: fe6386346282cf182397f6420c541d629ba0aab3
ms.sourcegitcommit: d57d2be09e67d7afed4b7565f9e3effdcc4a55bf
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2020
ms.locfileid: "81768398"
---
# <a name="about-azure-migrate"></a>À propos d’Azure Migrate

Cet article donne une vue d’ensemble du service Azure Migrate.

Azure Migrate fournit un hub centralisé pour évaluer et migrer les serveurs, l’infrastructure, les applications et les données locales vers Azure.

Azure Migrate fournit les fonctionnalités suivantes :

- **Plateforme de migration unifiée** : un portail unique pour démarrer, exécuter et effectuer le suivi de votre migration vers Azure.
- **Panoplie d’outils** : panoplie d’outils d’évaluation et de migration. Les outils incluent Azure Migrate : Server Assessment et Azure Migrate : Server Migration. Azure Migrate s’intègre avec d’autres services Azure ainsi qu’avec d’autres outils et offres d’ISV (éditeur de logiciels indépendant).
- **Évaluation et migration** : dans le hub Azure Migrate, vous pouvez évaluer et migrer les éléments suivants :
    - **Serveurs** : évaluez les serveurs locaux et migrez-les vers des machines virtuelles Azure.
    - **Bases de données** : évaluez vos bases de données locales et migrez-les vers Azure SQL Database ou une instance managée Azure SQL Database.
    - **Applications web** : évaluez les applications web locales et migrez-les vers Azure App Service à l’aide d’Azure App Service Migration Assistant.
    - **Bureaux virtuels** : évaluez votre infrastructure VDI (infrastructure de bureau virtuel) locale et migrez-la vers Windows Virtual Desktop dans Azure.
    - **Données** : migrez rapidement et à moindre coût de grandes quantités de données vers Azure à l’aide des produits Azure Data Box.

## <a name="integrated-tools"></a>Outils intégrés

Le hub Azure Migrate comprend ces outils :

**Outil** | **Évaluer et migrer** | **Détails**
--- | --- | ---
**Azure Migrate : Server Assessment** | Évaluez des serveurs. | Découvrez et évaluez les machines virtuelles VMware, les machines virtuelles Hyper-V et les serveurs physiques locaux pour les préparer à une migration vers Azure.
**Azure Migrate : Server Migration** | Migrez des serveurs. | Migrez des machines virtuelles VMware, des machines virtuelles Hyper-V, des serveurs physiques, d’autres machines virtualisées ainsi que des machines virtuelles de cloud public vers Azure.
**Assistant de migration des données** | Évaluez les bases de données SQL Server locales pour la migration vers Azure SQL Database, une instance managée Azure SQL Database ou des machines virtuelles Azure exécutant SQL Server. | Assistant Migration de données aide à identifier les problèmes potentiels bloquant la migration. Il identifie les fonctionnalités non prises en charge, les nouvelles fonctionnalités dont vous pouvez bénéficier après la migration, et le chemin approprié pour la migration de base de données. [Plus d’informations](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017)
**Azure Database Migration Service** | Migrez des bases de données locales vers des machines virtuelles Azure exécutant SQL Server, Azure SQL Database ou des instances managées Azure SQL Database. | [En savoir plus](https://docs.microsoft.com/azure/dms/dms-overview) sur Database Migration Service.
**Movere** | Évaluez des serveurs. | [En savoir plus](#movere) sur Movere.
**Assistant Migration d’applications web** | Évaluez les applications web locales et migrez-les vers Azure. |  Utilisez Azure App Service Migration Assistant pour évaluer les sites web locaux en vue de leur migration vers Azure App Service.<br/><br/> Utilisez Migration Assistant pour migrer des applications web .NET et PHP vers Azure. [En savoir plus](https://appmigration.microsoft.com/) sur Azure App Service Migration Assistant.
**Azure Data Box** | Migrez des données hors connexion. | Pour déplacer de grandes quantités de données hors connexion vers Azure, utilisez la gamme de produits Azure Data Box. [Plus d’informations](https://docs.microsoft.com/azure/databox/)

> [!NOTE]
> Si vous êtes dans Azure Government, les outils intégrés externes et les offres d’éditeurs de logiciels indépendants ne peuvent pas envoyer de données à des projets Azure Migrate. Vous pouvez employer les outils de manière indépendante.

## <a name="isv-integration"></a>Intégration d’éditeurs de logiciels indépendants

Azure Migrate s’intègre à plusieurs offres d’éditeurs de logiciels indépendants. 

**Fournisseurs de logiciels indépendants**    | **Fonctionnalité**
--- | ---
[Carbonite](https://www.carbonite.com/globalassets/files/datasheets/carb-migrate4azure-microsoft-ds.pdf) | Migrez des serveurs.
[Cloudamize](https://www.cloudamize.com/platform) | Évaluez des serveurs.
[Corent Technology](https://www.corenttech.com/AzureMigrate/) | Évaluez et migrez des serveurs.
[Device42](https://docs.device42.com/) | Évaluez des serveurs.
[Lakeside](https://go.microsoft.com/fwlink/?linkid=2104908) | Évaluez l’infrastructure VDI.
[RackWare](https://go.microsoft.com/fwlink/?linkid=2102735) | Migrez des serveurs.
[Turbonomic](https://learn.turbonomic.com/azure-migrate-portal-free-trial) | Évaluez des serveurs.
[UnifyCloud](https://www.cloudatlasinc.com/cloudrecon/) | Évaluez des serveurs et des bases de données.

## <a name="azure-migrate-server-assessment-tool"></a>Azure Migrate : Server Assessment

Azure Migrate : Server Assessment découvre et évalue les machines virtuelles VMware et Hyper-V ainsi que les serveurs physiques locaux en vue de leur migration vers Azure.

Voici ce que fait l’outil :

- **Préparé pour Azure** : vous permet d’évaluer si les machines locales sont prêtes pour une migration vers Azure.
- **Dimensionnement d’Azure** : vous permet d’estimer la taille des machines virtuelles Azure après la migration.
- **Estimation des coûts Azure** : estimez les coûts liés à l’exécution de serveurs locaux dans Azure.
- **Analyse des dépendances** : identifie les dépendances entre serveurs et les stratégies d’optimisation pour déplacer les serveurs interdépendants vers Azure. Apprenez-en davantage sur Server Assessment avec l’[analyse des dépendances](concepts-dependency-visualization.md).

L’outil d’évaluation de serveur utilise une [appliance Azure Migrate](migrate-appliance.md) légère que vous déployez localement.

- L’appliance s’exécute sur une machine virtuelle ou un serveur physique. Vous pouvez l’installer facilement à l’aide d’un modèle téléchargé.
- L’appliance découvre des machines locales. Elle envoie aussi continuellement les métadonnées et les données de performances des machines vers Azure Migrate.
- La découverte de l’appliance se fait sans agent. Rien n’est installé sur les machines découvertes.
- Une fois la découverte effectuée, vous pouvez regrouper les machines découvertes et exécuter des évaluations pour chaque groupe.

## <a name="azure-migrate-server-migration-tool"></a>Azure Migrate : Outil Server Migration

Azure Migrate : Server Migration vous aide à migrer vers Azure les éléments suivants :

- Machines virtuelles VMware locales
- Machines virtuelles Hyper-V
- Serveurs physiques
- Autres machines virtualisées
- Machines virtuelles de cloud public

Vous pouvez migrer des machines après les avoir évaluées ou les migrer sans les avoir évaluées.

Pour une migration sans agent des machines virtuelles VMware et des machines virtuelles Hyper-V, Server Migration utilise une appliance Azure Migrate que vous déployez localement. L’appliance est également utilisée si vous configurez l’évaluation de serveur. Ceci est décrit dans la section précédente.

## <a name="selecting-assessment-and-migration-tools"></a>Sélection des outils d’évaluation et de migration

Dans le hub Azure Migrate, vous sélectionnez l’outil à utiliser pour l’évaluation ou la migration, puis vous l’ajoutez à un projet Azure Migrate. Si vous ajoutez un outil d’un éditeur de logiciels indépendant ou Movere :

- Pour commencer, obtenez une licence ou inscrivez-vous pour obtenir un essai gratuit en suivant les instructions de l’outil. Chaque ISV ou outil spécifie la gestion des licences d’outils.
- Chaque outil a une option permettant de se connecter à Azure Migrate. Suivez les instructions de l’outil pour vous connecter.
- Suivez votre migration parmi l’ensemble des outils à partir du projet Azure Migrate.

## <a name="movere"></a>Movere

Movere est une plateforme SaaS (Software as a Service). Elle améliore les fonctionnalités décisionnelles en présentant avec précision des environnements informatiques complets en une seule journée. Les organisations et entreprises croissent, évoluent et optimisent numériquement. Ce faisant, Movere leur procure la confiance nécessaire pour visualiser et contrôler leurs environnements, quelle que soit la plateforme, l’application ou la géographie.

Microsoft a fait l’[acquisition](https://azure.microsoft.com/blog/microsoft-acquires-movere-to-help-customers-unlock-cloud-innovation-with-seamless-migration-tools/) de Movere, qui aujourd’hui n’est plus vendu en tant qu’offre autonome. Movere est disponible par le biais des programmes « Microsoft Solution Assessment » et « Microsoft Cloud Economics ». [En savoir plus](https://www.movere.io) sur Movere.

Nous vous encourageons à examiner aussi Azure Migrate, notre service de migration intégré. Azure Migrate fournit un hub central pour simplifier votre migration vers le cloud. Le hub prend en charge de manière complète les charges de travail, telles que les serveurs physiques et virtuels, les bases de données et les applications. La visibilité de bout en bout facilite le suivi de la progression tout au long de la découverte, de l’évaluation et de la migration.

Grâce aux outils d’ISV partenaires et Azure intégrés, Azure Migrate offre un large éventail de fonctionnalités, notamment :

- Découverte des serveurs virtuels et physiques
- Dimensionnement correct basé sur les performances
- Planification des coûts
- Évaluations basée sur l’importation
- Analyse des dépendances des applications sans agent

Si vous recherchez des conseils d’experts pour démarrer, laissez-vous guider par le programme [Fournisseurs de services managés Azure Expert](https://azure.microsoft.com/partners) de Microsoft. Consultez le [site web Azure Migrate](https://azure.microsoft.com/services/azure-migrate/). 

## <a name="azure-migrate-versions"></a>Versions d’Azure Migrate

Il existe deux versions du service Azure Migrate.

- **Version actuelle** : utilisez cette version pour créer des projets Azure Migrate, découvrir des machines locales et orchestrer des évaluations et migrations. [Apprenez-en davantage](whats-new.md) sur les nouveautés de cette version.
- **Version précédente** : La version précédente d’Azure Migrate prend uniquement en charge l’évaluation des machines virtuelles VMware locales. Si vous utilisiez la version précédente, vous devez maintenant utiliser la version actuelle. Vous ne pouvez plus créer de projets Azure Migrate à l’aide de la version précédente. Nous vous recommandons également de ne pas effectuer de nouvelles découvertes avec elle.

    Pour accéder à des projets existants dans le portail Azure, recherchez et sélectionnez **Azure Migrate**. Le tableau de bord **Azure Migrate** affiche une notification et un lien permettant d’accéder aux anciens projets Azure Migrate.

## <a name="next-steps"></a>Étapes suivantes

- Essayez nos tutoriels pour évaluer des [machines virtuelles VMware](tutorial-prepare-vmware.md), des [machines virtuelles Hyper-V](tutorial-prepare-hyper-v.md) ou des [serveurs physiques](tutorial-prepare-physical.md).
- [Revoir les questions fréquemment posées](resources-faq.md) sur Azure Migrate.
