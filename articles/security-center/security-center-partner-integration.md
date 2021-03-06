---
title: Intégrer des solutions de sécurité dans Azure Security Center | Microsoft Docs
description: Découvrez comment Azure Security Center s’intègre avec les partenaires pour améliorer la sécurité globale de vos ressources Azure.
services: security-center
documentationcenter: na
author: memildin
manager: rkarlin
ms.assetid: 6af354da-f27a-467a-8b7e-6cbcf70fdbcb
ms.service: security-center
ms.topic: conceptual
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2020
ms.author: memildin
ms.openlocfilehash: 48869140ba8cd1a9598562b0057b0005d8fcd9c7
ms.sourcegitcommit: 849bb1729b89d075eed579aa36395bf4d29f3bd9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2020
ms.locfileid: "81758029"
---
# <a name="integrate-security-solutions-in-azure-security-center"></a>Intégrer des solutions de sécurité dans Azure Security Center
Ce document vous aide à gérer les solutions de sécurité déjà connectées à Azure Security Center et à en ajouter de nouvelles.

## <a name="integrated-azure-security-solutions"></a>Solutions de sécurité Azure intégrées
Security Center simplifie l’activation des solutions de sécurité intégrées dans Azure. Voici les avantages :

- **Déploiement simplifié** : Security Center permet un provisionnement simplifié des solutions de partenaire intégrées. Pour les solutions telles que les logiciels anti-programme malveillant et l’évaluation des vulnérabilités, Security Center peut provisionner l’agent sur vos machines virtuelles. Pour les appliances de pare-feu, Security Center peut prendre en charge une grande partie de la configuration réseau requise.
- **Détections intégrées** : les événements de sécurité des solutions de partenaire sont automatiquement collectés, agrégés et affichés dans le cadre des alertes et des incidents de Security Center. Ces événements sont également fusionnés avec les détections d’autres sources pour fournir des fonctions de détection de menaces avancées.
- **Gestion et surveillance unifiées de l’intégrité** : Les clients peuvent utiliser des événements d’intégrité intégrés pour surveiller facilement les solutions des partenaires. La gestion de base offre un accès facile à la configuration avancée avec la solution de partenaire.

Les solutions de sécurité intégrées incluent l’évaluation des vulnérabilités par [Qualys](https://www.qualys.com/public-cloud/#azure) et [Rapid7](https://www.rapid7.com/products/insightvm/), et le pare-feu d’applications web Application Gateway de Microsoft.

> [!NOTE]
> Security Center n’installe pas l’agent Log Analytics sur les appliances virtuelles de partenaire, car la plupart des fournisseurs de sécurité n’autorisent pas l’exécution d’agents externes sur leurs appliances.

Pour en savoir plus sur l’intégration des outils d’analyse des vulnérabilités de Qualys, y compris un analyseur intégré disponible pour les clients de niveau standard, consultez : 

- [Analyseur de vulnérabilité intégré pour machines virtuelles](built-in-vulnerability-assessment.md).
- [Déploiement d’une solution de partenaire d’analyse des vulnérabilités](partner-vulnerability-assessment.md).

Security Center offre également une analyse des vulnérabilités pour les éléments suivants :

* Bases de données SQL : consultez [Explorer les rapports d’évaluation des vulnérabilités dans le tableau de bord de l’évaluation des vulnérabilités](security-center-iaas-advanced-data.md#explore-vulnerability-assessment-reports).
* Images Azure Container Registry : consultez [Intégration d’Azure Container Registry à Security Center (préversion)](azure-container-registry-integration.md).

## <a name="how-security-solutions-are-integrated"></a>Comment sont intégrées les solutions de sécurité
Les solutions de sécurité Azure déployées à partir de Security Center sont automatiquement connectées. Vous pouvez également connecter d’autres sources de données de sécurité, notamment des ordinateurs s’exécutant en local ou dans d’autres clouds.

[![Partner solutions integration](./media/security-center-partner-integration/security-solutions-page.png)](./media/security-center-partner-integration/security-solutions-page.png#lightbox)

## <a name="manage-integrated-azure-security-solutions-and-other-data-sources"></a>Gérer des solutions de sécurité Azure intégrées et d’autres sources de données

1. Dans le [Portail Azure](https://azure.microsoft.com/features/azure-portal/), ouvrez **Security Center**.

1. Dans le menu de Security Center, sélectionnez **Solutions de sécurité**.

Sur la page **Solutions de sécurité**, vous pouvez voir l’intégrité des solutions de sécurité Azure intégrées et exécuter des tâches de gestion de base.

### <a name="connected-solutions"></a>Solutions connectées

La section **Solutions connectées** inclut les solutions de sécurité qui sont connectées à Security Center. Elle indique également l’état d’intégrité de chaque solution.  

![Solutions connectées](./media/security-center-partner-integration/connected-solutions.png)

L’état d’une solution de partenaire peut être :

* **Sain** (vert) : aucun problème d’intégrité.
* **Non sain** (rouge) : problème d’intégrité nécessitant une action immédiate.
* **Arrêté** (orange) : état d’intégrité non signalé par la solution.
* **Non signalé** (gris) : la solution n’a encore rien signalé et aucune donnée d’intégrité n’est disponible. L’état d’une solution peut être non signalé si celle-ci a été récemment connectée et qu’elle est toujours en cours de déploiement.

> [!NOTE]
> Si les données sur l’état d’intégrité ne sont pas disponibles, Security Center affiche la date et l’heure du dernier événement reçu pour indiquer si la solution signale ou non des données. Si aucune donnée d’intégrité n’est disponible et qu’aucune alerte n’a été reçue au cours des 14 derniers jours, Security Center indique que la solution est non saine ou qu’elle ne signale pas de données.
>
>

Sélectionnez **AFFICHAGE** pour obtenir des informations et des options supplémentaires, par exemple :

   - **Console de la solution** : ouvre l’expérience de gestion pour cette solution.
   - **Associer la machine virtuelle**. : ouvre la page Associer les applications. Il vous permet de connecter des ressources à la solution de partenaire.
   - **Supprimer la solution**
   - **Configurer**

   ![Détail de la solution partenaire](./media/security-center-partner-integration/partner-solutions-detail.png)


### <a name="discovered-solutions"></a>Solutions découvertes

Security Center découvre automatiquement les solutions exécutées dans Azure mais qui ne sont pas connectées à Security Center. Elles sont ensuite affichées dans la section **Solutions découvertes**. Ces solutions incluent les solutions Azure, telles qu’[Azure AD Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection), et les solutions partenaires.

> [!NOTE]
> Le niveau Standard de Security Center est requis au niveau de l’abonnement pour la fonctionnalité de découverte des solutions. Consultez [Tarification](security-center-pricing.md) pour en savoir plus sur les niveaux tarifaires.
>

Sélectionnez **CONNECTER** sous une solution pour l’intégrer à Security Center et être notifié des alertes de sécurité.

### <a name="add-data-sources"></a>Ajouter des sources de données

La section **Ajouter des sources de données** comprend d’autres sources de données disponibles qui peuvent être connectées. Pour obtenir des instructions sur l’ajout de données à partir d’une de ces sources, cliquez sur **AJOUTER**.

![Sources de données](./media/security-center-partner-integration/add-data-sources.png)



## <a name="next-steps"></a>Étapes suivantes

Dans cet article, vous avez appris à intégrer des solutions de partenaires dans Security Center. Pour accéder à des informations connexes, voir les articles suivants :

* [Exporter les alertes et recommandations de sécurité](continuous-export.md). Découvrez comment configurer une intégration avec Azure Sentinel ou tout autre SIEM.
* [Surveillance de l’intégrité de la sécurité dans Security Center](security-center-monitoring.md). découvrez comment surveiller l’intégrité de vos ressources Azure.