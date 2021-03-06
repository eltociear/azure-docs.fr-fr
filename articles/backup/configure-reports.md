---
title: Configurer les rapports de la Sauvegarde Azure
description: Configurez et affichez les rapports de la Sauvegarde Azure à l’aide de Log Analytics et des classeurs Azure.
ms.topic: conceptual
ms.date: 02/10/2020
ms.openlocfilehash: c1af9a532b390b428e74957c455988dfd4df3967
ms.sourcegitcommit: 849bb1729b89d075eed579aa36395bf4d29f3bd9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2020
ms.locfileid: "82184943"
---
# <a name="configure-azure-backup-reports"></a>Configurer les rapports de la Sauvegarde Azure

Les administrateurs de sauvegarde ont souvent besoin d’insights sur les sauvegardes, en fonction de données couvrant une longue période. Voici quelques-uns des cas d’usage d’une telle solution :

- allocation et prévision du stockage cloud utilisé ;
- audit des sauvegardes et restaurations ;
- identification des tendances clés à différents niveaux de granularité.

Aujourd’hui, la Sauvegarde Azure fournit une solution de reporting qui utilise les [journaux Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/log-query/get-started-portal) et les [classeurs Azure](https://docs.microsoft.com/azure/azure-monitor/app/usage-workbooks). Ces ressources vous permettent d’obtenir de riches insights sur vos sauvegardes dans l’ensemble de votre espace de sauvegarde. Cet article explique comment configurer et afficher des rapports Sauvegarde Azure.

## <a name="supported-scenarios"></a>Scénarios pris en charge

- Les rapports de sauvegarde sont pris en charge pour les machines virtuelles Azure, SQL dans les machines virtuelles Azure, SAP HANA/ASE dans les machines virtuelles Azure, l’agent Microsoft Azure Recovery Services (MARS), le serveur de sauvegarde Microsoft Azure (MABS) et System Center Data Protection Manager (DPM). Les données pour la sauvegarde du partage de fichiers Azure ne sont actuellement pas visibles dans les Rapports de sauvegarde.
- Concernant les charges de travail DPM, les rapports de sauvegarde sont pris en charge pour la version 5.1.363.0 et les versions ultérieures de DPM et la version 2.0.9127.0 et les versions ultérieures de l’agent.
- Concernant les charges de travail MABS, les rapports de sauvegarde sont pris en charge pour la version 13.0.415.0 et les versions ultérieures de MABS ainsi que pour la version 2.0.9170.0 et les versions ultérieures de l’agent.
- Les rapports de sauvegarde peuvent être affichés sur l’ensemble des éléments de sauvegarde, des coffres, des abonnements et des régions, à condition que leurs données soient envoyées à un espace de travail Log Analytics auquel l’utilisateur a accès. Pour visualiser les rapports d’un ensemble de coffres, il suffit d’un accès lecteur à l’espace de travail Log Analytics auquel les coffres envoient leurs données. Il n’est pas nécessaire d’avoir accès aux différents coffres.
- Si vous utilisez [Azure Lighthouse](https://docs.microsoft.com/azure/lighthouse/) avec un accès délégué aux abonnements de vos clients, vous pouvez utiliser ces rapports avec Azure Lighthouse afin de les consulter pour tous vos locataires.
- Les données des travaux de sauvegarde de fichier journal ne sont pas affichées dans les rapports.

## <a name="get-started"></a>Bien démarrer

Suivez cette procédure pour commencer à utiliser les rapports.

### <a name="1-create-a-log-analytics-workspace-or-use-an-existing-one"></a>1. Créer un espace de travail Log Analytics ou utiliser un espace de travail existant

Configurez un ou plusieurs espaces de travail Log Analytics pour stocker vos données de rapport de sauvegarde. L’emplacement et l’abonnement dans lesquels ces espaces de travail peuvent être créés dépendent de l’emplacement et de l’abonnement où se trouvent les coffres.

Pour configurer un espace de travail Log Analytics, consultez [Création d’un espace de travail Log Analytics sur le Portail Azure](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace).

Par défaut, les données d’un espace de travail Log Analytics sont conservées pendant 30 jours. Pour consulter les données sur un horizon temporel plus long, changez la période de rétention de l’espace de travail Log Analytics. Pour modifier cette période, consultez [Gestion de l’utilisation et des coûts avec les journaux Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage).

### <a name="2-configure-diagnostics-settings-for-your-vaults"></a>2. Configurer les paramètres de diagnostic des coffres

Des ressources Azure Resource Manager, comme les coffres Recovery Services, enregistrent des informations sur les opérations planifiées et sur les opérations déclenchées par l’utilisateur au titre de données de diagnostics.

Dans la section de monitorage de votre coffre Recovery Services, sélectionnez **Paramètres de diagnostic** et spécifiez la cible des données de diagnostic du coffre Recovery Services. Pour plus d’informations sur l’utilisation des événements de diagnostic, consultez [Utilisation des paramètres de diagnostic pour les coffres Recovery Services](https://docs.microsoft.com/azure/backup/backup-azure-diagnostic-events).

![Volet Paramètres de diagnostic](./media/backup-azure-configure-backup-reports/resource-specific-blade.png)

Le service Sauvegarde Azure fournit également une définition Azure Policy intégrée qui automatise la configuration des paramètres de diagnostic pour tous les coffres dans une étendue donnée. Pour savoir comment utiliser cette stratégie, consultez [Configuration à grande échelle des paramètres de diagnostic des coffres](https://docs.microsoft.com/azure/backup/azure-policy-configure-diagnostics).

> [!NOTE]
> Une fois les diagnostics configurés, le Push de données initial peut prendre jusqu’à 24 heures. Lorsqu’elles commencent à arriver dans l’espace de travail Log Analytics, les données n’apparaissent pas forcément tout de suite dans les rapports, car les données d’une journée incomplète ne figurent pas dans les rapports. Pour plus d’informations, consultez [Conventions utilisées dans les rapports de sauvegarde](https://docs.microsoft.com/azure/backup/configure-reports#conventions-used-in-backup-reports). Il est recommandé d’afficher les rapports deux jours après avoir configuré les coffres en vue d’envoyer des données à Log Analytics.

#### <a name="3-view-reports-in-the-azure-portal"></a>3. Afficher les rapports sur le Portail Azure

Une fois que vous avez configuré vos coffres de façon à envoyer des données à Log Analytics, affichez vos rapports de sauvegarde en accédant au volet d’un des coffres et en sélectionnant **Rapports de sauvegarde**.

![Tableau de bord du coffre](./media/backup-azure-configure-backup-reports/vault-dashboard.png)

Sélectionnez ce lien pour ouvrir le classeur des rapports de sauvegarde.

> [!NOTE]
>
> - Le chargement initial du rapport peut prendre à l’heure actuelle jusqu’à une minute.
> - Le coffre Recovery Services est simplement un point d’entrée pour les rapports de sauvegarde. Quand le classeur des rapports de sauvegarde s’ouvre à partir du volet d’un coffre, sélectionnez l’ensemble d’espaces de travail Log Analytics concerné pour voir les données agrégées de tous vos coffres.

Le rapport contient différents onglets :

- **Résumé**: cet onglet donne une vue d’ensemble globale de votre espace de sauvegarde. Vous voyez d’un seul coup d’œil le nombre total d’éléments de sauvegarde, le stockage cloud total consommé, le nombre d’instances protégées et le taux de réussite des travaux par type de charge de travail. Pour obtenir des informations plus détaillées sur un type d’artefact de sauvegarde spécifique, accédez à l’onglet correspondant.

   ![Onglet Résumé](./media/backup-azure-configure-backup-reports/summary.png)

- **Éléments de sauvegarde** : cet onglet donne des informations et des tendances sur le stockage cloud consommé au niveau d’un élément de sauvegarde. Par exemple, si vous utilisez SQL dans une sauvegarde de machine virtuelle Azure, vous pouvez voir le stockage cloud consommé pour chaque base de données SQL en cours de sauvegarde. Vous pouvez également choisir de voir les données des éléments de sauvegarde ayant un état de protection particulier. Par exemple, si vous sélectionnez la vignette **Protection arrêtée** en haut de l’onglet, tous les widgets situés au-dessous sont filtrés pour n’afficher que les données des éléments de sauvegarde dont l’état est Protection arrêtée.

   ![Onglet Éléments de sauvegarde](./media/backup-azure-configure-backup-reports/backup-items.png)

- **Utilisation**: cet onglet indique les paramètres clés de facturation des sauvegardes. Les informations affichées se trouvent au niveau d’une entité de facturation (conteneur protégé). Par exemple, dans le cas d’un serveur DPM en cours de sauvegarde sur Azure, vous pouvez voir la tendance des instances protégées et du stockage cloud consommé pour ce serveur. De même, si vous utilisez SQL ou SAP HANA dans la Sauvegarde Azure, cet onglet fournit des informations sur l’utilisation au niveau de la machine virtuelle qui contient ces bases de données.

   ![Onglet Utilisation](./media/backup-azure-configure-backup-reports/usage.png)

- **Travaux** : cet onglet indique les tendances durables sur les travaux, par exemple le nombre de travaux ayant échoué par jour et les principales causes d’échec des travaux. Vous pouvez voir ces informations à la fois au niveau agrégé et au niveau d’un élément de sauvegarde. Sélectionnez un élément de sauvegarde en particulier dans une grille pour afficher des informations détaillées sur chacun des travaux qui se sont déclenchés sur cet élément dans l’intervalle de temps sélectionné.

   ![Onglet Travaux](./media/backup-azure-configure-backup-reports/jobs.png)

- **Stratégies** : cet onglet donne des informations sur toutes les stratégies actives, par exemple le nombre d’éléments associés et le stockage cloud total consommé par les éléments sauvegardés dans le cadre d’une stratégie donnée. Sélectionnez une stratégie en particulier pour afficher des informations sur chacun des éléments de sauvegarde associés.

   ![Onglet Stratégies](./media/backup-azure-configure-backup-reports/policies.png)

## <a name="export-to-excel"></a>Exporter vers Excel

Sélectionnez la flèche vers le bas située en haut à droite d’un widget, par exemple un tableau ou un graphe, pour exporter le contenu de ce widget sous forme de feuille Excel, en l’état, avec les filtres appliqués. Pour exporter d’autres lignes d’une table vers Excel, vous pouvez augmenter le nombre de lignes affichées sur la page avec la flèche déroulante vers le bas **Lignes par page** située en haut de chaque grille.

## <a name="pin-to-dashboard"></a>Épingler au tableau de bord

Sélectionnez le bouton Épingler en haut d’un widget pour épingler le widget sur votre tableau de bord sur le Portail Azure. Cette fonctionnalité vous permet de créer des tableaux de bord personnalisés qui présentent les informations les plus importantes pour vous.

## <a name="cross-tenant-reports"></a>Rapports multilocataires

Si vous utilisez [Azure Lighthouse](https://docs.microsoft.com/azure/lighthouse/) avec un accès délégué aux abonnements de plusieurs environnements de locataires, vous pouvez utiliser le filtre d’abonnement par défaut. Sélectionnez le bouton de filtre en haut à droite du Portail Azure pour choisir tous les abonnements dont vous souhaitez afficher les données. Cela vous permet de sélectionner des espaces de travail Log Analytics de plusieurs locataires pour afficher des rapports multilocataires.

## <a name="conventions-used-in-backup-reports"></a>Conventions utilisées dans les rapports de sauvegarde

- Les filtres fonctionnent de gauche à droite et de haut en bas sur chaque onglet. Autrement dit, un filtre s’applique uniquement à tous les widgets situés à sa droite ou au-dessous.
- Sélectionnez une vignette de couleur pour filtrer les widgets situés au-dessous de manière à récupérer les enregistrements correspondant à la valeur de cette vignette. Par exemple, si vous sélectionnez la vignette **Protection arrêtée** sur l’onglet **Éléments de sauvegarde**, toutes les grilles et tous les graphes situés au-dessous sont filtrés pour afficher les données des éléments de sauvegarde dont l’état est Protection arrêtée.
- Les vignettes qui ne sont pas en couleur ne sont pas cliquables.
- Les données d’une journée incomplète ne figurent pas dans les rapports. Ainsi, quand la valeur sélectionnée pour **Intervalle de temps** est **7 derniers jours**, le rapport affiche les enregistrements des sept derniers jours révolus. Le jour actuel n’est pas inclus.
- Le rapport affiche les détails des travaux (hors travaux de journalisation) qui se sont *déclenchés* dans l’intervalle de temps sélectionné.
- Les valeurs affichées pour **Stockage cloud** et **Instances protégées** se trouvent à la *fin* de l’intervalle de temps sélectionné.
- Les éléments de sauvegarde affichés dans les rapports sont ceux qui se trouvent à la *fin* de l’intervalle de temps sélectionné. Les éléments de sauvegarde qui ont été supprimés au milieu de l’intervalle de temps sélectionné ne sont pas affichés. La même convention vaut pour les stratégies de sauvegarde.

## <a name="query-load-times"></a>Temps de chargement des requêtes

Les widgets du rapport de sauvegarde reposent sur des requêtes Kusto, qui s’exécutent sur les espaces de travail Log Analytics de l’utilisateur. Ces requêtes impliquent généralement le traitement de grandes quantités de données, avec plusieurs jointures pour offrir des insights plus riches. Par conséquent, il peut arriver que les widgets ne se chargent pas instantanément lorsque l’utilisateur consulte des rapports sur un grand espace de sauvegarde. Ce tableau donne une estimation approximative du temps que peut prendre le chargement des différents widgets, en fonction du nombre d’éléments de sauvegarde et de l’intervalle de temps pendant lequel le rapport est affiché.

| **Nombre de sources de données**                         | **Horizon temporel** | **Durées de chargement approximatives**                                              |
| --------------------------------- | ------------- | ------------------------------------------------------------ |
| Environ 5 K                       | 1 mois          | Vignettes : 5 à 10 s <br> Grilles : 5 à 10 s <br> Graphiques : 5 à 10 s <br> Filtres au niveau du rapport : 5 à 10 s|
| Environ 5 K                       | 3 mois          | Vignettes : 5 à 10 s <br> Grilles : 5 à 10 s <br> Graphiques : 5 à 10 s <br> Filtres au niveau du rapport : 5 à 10 s|
| Environ 10 K                       | 3 mois          | Vignettes : 15 à 20 s <br> Grilles : 15 à 20 s <br> Graphiques : 1 à 2 minutes <br> Filtres au niveau du rapport : 25 à 30 s|
| Environ 15 K                       | 1 mois          | Vignettes : 15 à 20 s <br> Grilles : 15 à 20 s <br> Graphiques : 50 à 60 s <br> Filtres au niveau du rapport : 20 à 25 s|
| Environ 15 K                       | 3 mois          | Vignettes : 20 à 30 s <br> Grilles : 20 à 30 s <br> Graphiques : 2 à 3 minutes <br> Filtres au niveau du rapport : 50 à 60 s |

## <a name="what-happened-to-the-power-bi-reports"></a>Point sur les rapports Power BI

- L’ancienne application modèle Power BI pour la création de rapports, dont les données provenaient d’un compte de stockage Azure, est en voie de dépréciation. Nous vous recommandons de commencer à envoyer les données de diagnostic des coffres à Log Analytics pour afficher des rapports.

- * En outre, le [schéma v1](https://docs.microsoft.com/azure/backup/backup-azure-diagnostics-mode-data-model#v1-schema-vs-v2-schema) d’envoi de données de diagnostic à un compte de stockage ou à un espace de travail LA est également en voie de désapprobation. Cela signifie que si vous avez écrit des automatisations ou des requêtes personnalisées basées sur le schéma v1, nous vous recommandons de les mettre à jour afin qu’elles utilisent le schéma v2 pris en charge.

## <a name="next-steps"></a>Étapes suivantes

[Découvrez la supervision et la création de rapports avec Sauvegarde Azure](https://docs.microsoft.com/azure/backup/backup-azure-monitor-alert-faq)
