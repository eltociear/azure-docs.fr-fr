---
title: Gérer les instances d’alerte dans Azure Monitor
description: Gestion des instances d’alerte dans Azure
ms.subservice: alerts
ms.topic: conceptual
ms.date: 09/24/2018
ms.openlocfilehash: 1910b3b474012365e8117f584379b2b29f8ce3de
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2020
ms.locfileid: "77667616"
---
# <a name="manage-alert-instances-with-unified-alerts"></a>Gérer les instances d’alerte avec des alertes unifiées

L’[expérience des alertes unifiées](https://aka.ms/azure-alerts-overview) dans Azure Monitor, vous permet de voir vos différents types d’alertes dans Azure. Elle s’étend sur plusieurs abonnements dans un seul volet. Cet article explique comment afficher vos instances d’alerte et comment rechercher des instances d’alerte spécifiques pour résoudre des problèmes.

> [!NOTE]
> Vous ne pouvez accéder qu’aux alertes générées au cours des 30 derniers jours.

## <a name="go-to-the-alerts-page"></a>Accéder à la page des alertes

Vous pouvez accéder à la page des alertes de l’une des manières suivantes :

- Dans le [portail Azure](https://portal.azure.com/), sélectionnez **Surveiller** > **Alertes**.  

     ![Capture d’écran de la surveillance des alertes](media/alerts-managing-alert-instances/monitoring-alerts-managing-alert-instances-toc.jpg)
  
- Utilisez le contexte d’une ressource spécifique. Ouvrez une ressource, accédez à la section **Analyse**, puis sélectionnez **Alertes**. La page d’accueil est pré-filtrée pour les alertes sur cette ressource spécifique.

     ![Capture d’écran des alertes d’analyse des ressources](media/alerts-managing-alert-instances/alert-resource.JPG)

- Utilisez le contexte d’un groupe de ressources spécifique. Ouvrez un groupe de ressources, accédez à la section **Analyse**, puis sélectionnez **Alertes**. La page d’accueil est pré-filtrée pour les alertes sur ce groupe de ressources spécifique.    

     ![Capture d’écran des alertes d’analyse de groupe de ressources](media/alerts-managing-alert-instances/alert-rg.JPG)

## <a name="find-alert-instances"></a>Rechercher des instances d’alerte

La page **Résumé des alertes** affiche une vue d’ensemble de toutes vos instances d’alerte dans Azure. Vous pouvez modifier l’affichage du résumé en sélectionnant **plusieurs abonnements** (jusqu’à 5) ou en filtrant sur des **groupes de ressources**, des **ressources** spécifiques ou des **intervalles de temps**. Sélectionnez **Nombre total d’alertes** ou l’une des bandes de gravité pour accéder à la liste de vos alertes.     

![Capture d’écran de la page Récapitulatif des alertes](media/alerts-managing-alert-instances/alerts-summary.jpg)
 
La page **Toutes les alertes** répertorie toutes les instances d’alerte dans Azure. Si vous accédez au portail à partir d’une notification d’alerte, vous pouvez utiliser les filtres disponibles pour vous concentrer sur cette instance d’alerte spécifique.

> [!NOTE]
> Si vous avez accédé à la page en sélectionnant l’une des bandes de gravité, la liste est pré-filtrée sur ce niveau de gravité.

En plus des filtres disponibles dans la page précédente, vous pouvez filtrer sur la base du service de surveillance (par exemple, la plateforme pour les mesures), de la condition de surveillance (déclenchée ou résolue), de la gravité, de l’état de l’alerte (nouvelle/reconnue/fermée) ou de l’ID de groupe intelligent.

![Capture d’écran de la page Toutes les alertes](media/alerts-managing-alert-instances/all-alerts.jpg)

> [!NOTE]
> Si vous avez accédé à la page en sélectionnant l’une des bandes de gravité, la liste est pré-filtrée sur ce niveau de gravité.

La sélection d’une instance d’alerte a pour effet d’ouvrir la page **Détails de l’alerte** qui affiche des détails supplémentaires sur cette instance d’alerte spécifique.   

![Capture d’écran de la page Détails de l’alerte](media/alerts-managing-alert-instances/alert-details.jpg)  

