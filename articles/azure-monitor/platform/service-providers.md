---
title: Journaux Azure Monitor pour les fournisseurs de services | Microsoft Docs
description: Les journaux Azure Monitor permettent aux fournisseurs de services gérés (MSP), aux grandes entreprises, aux éditeurs de logiciels indépendants (ISV) et aux fournisseurs de service d’hébergement de gérer et de surveiller les serveurs situés dans l’infrastructure locale ou cloud d’un client.
ms.subservice: logs
ms.topic: conceptual
author: MeirMen
ms.author: meirm
ms.date: 02/03/2020
ms.openlocfilehash: ed398e12ee90f2eef2cfa78e2ed02701e6012517
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2020
ms.locfileid: "77658878"
---
# <a name="azure-monitor-logs-for-service-providers"></a>Journaux Azure Monitor pour les fournisseurs de services

Les espaces de travail Log Analytics dans Azure Monitor permettent aux fournisseurs de services managés (MSP), aux grandes entreprises, aux éditeurs de logiciels indépendants (ISV) et aux fournisseurs de service d’hébergement de gérer et de surveiller les serveurs situés dans l’infrastructure locale ou cloud d’un client.

Les grandes entreprises et les fournisseurs de services présentent de nombreux points communs, en particulier si les ressources informatiques de plusieurs divisions sont gérées par une équipe informatique centralisée. Le terme *fournisseur de services* est utilisé dans ce document par souci de simplicité, mais sachez que les entreprises et d’autres clients bénéficient de la même fonctionnalité.

Pour les partenaires et fournisseurs de services qui font partie du programme [Fournisseur de solutions Cloud (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview), Log Analytics dans Azure Monitor est l’un des services Azure disponibles parmi les abonnements Azure CSP.

Log Analytics dans Azure Monitor peut également être utilisé par un fournisseur de services qui gère les ressources client par le biais de la fonctionnalité de gestion déléguée des ressources Azure dans [Azure Lighthouse](https://docs.microsoft.com/azure/lighthouse/overview).

## <a name="architectures-for-service-providers"></a>Architecture des fournisseurs de services

Les espaces de travail Log Analytics fournissent une méthode permettant à l'administrateur de contrôler le flux et l'isolation des données des [journaux](data-platform-logs.md), et de créer une architecture répondant à ses besoins métier. [Cet article](design-logs-deployment.md) traite de la conception, du déploiement et de la migration d'un espace de travail, et l'article consacré à la [gestion des accès](manage-access.md) explique comment appliquer et gérer les autorisations pour journaliser les données. Les fournisseurs de services n’y sont pas abordés.

En ce qui concerne les espaces de travail Log Analytics, il existe trois architectures possibles pour les fournisseurs de services :

### <a name="1-distributed---logs-are-stored-in-workspaces-located-in-the-customers-tenant"></a>1. Distribuée : les journaux d’activité sont stockés dans les espaces de travail situés dans le locataire du client

Dans cette architecture, un espace de travail est déployé dans le locataire du client lequel est utilisé pour tous les journaux d’activité de ce client.

Il existe deux façons pour les administrateurs de fournisseurs de services d’accéder à un espace de travail Log Analytics dans un locataire client :

- Un client peut ajouter des utilisateurs individuels à partir du fournisseur de services en tant qu’[utilisateurs invités (B2B) Azure Active Directory](https://docs.microsoft.com/azure/active-directory/b2b/what-is-b2b). Pour accéder à ces espaces de travail, l’administrateur du fournisseur de services doit se connecter à l’annuaire de chaque client, dans le Portail Microsoft Azure. Cela requiert également que les clients gèrent un accès individuel pour chaque administrateur de fournisseur de services.
- Pour une plus grande extensibilité et flexibilité, les fournisseurs de services peuvent utiliser la fonctionnalité de [gestion déléguée des ressources Azure](https://docs.microsoft.com/azure/lighthouse/concepts/azure-delegated-resource-management) d’[Azure Lighthouse](https://docs.microsoft.com/azure/lighthouse/overview) pour accéder au locataire du client. Avec cette méthode, les administrateurs de fournisseurs de services sont inclus dans un groupe d’utilisateurs Azure AD dans le locataire du fournisseur de services, et ce groupe se voit accorder un accès pendant le processus d’intégration pour chaque client. Ces administrateurs peuvent ensuite accéder aux espaces de travail de chaque client à partir de leur propre locataire du fournisseur de services, au lieu de se connecter individuellement au locataire de chaque client. Accéder de cette manière aux ressources des espaces de travail Log Analytics des clients réduit le travail requis côté client et peut faciliter la collecte et l’analyse des données sur plusieurs clients gérés par le même fournisseur de services via des outils tels que les [classeurs Azure Monitor](https://docs.microsoft.com/azure//azure-monitor/platform/workbooks-overview). Pour plus d’informations, consultez [Surveiller les ressources client à l’échelle](https://docs.microsoft.com/azure/lighthouse/how-to/monitor-at-scale).

Les avantages de l’architecture distribuée sont les suivants :

* Le client peut confirmer des niveaux spécifiques d’autorisations via la [gestion déléguée des ressources Azure](https://docs.microsoft.com/azure/lighthouse/concepts/azure-delegated-resource-management) ou peut gérer l’accès aux journaux à l’aide de son propre [accès basé sur les rôles](https://docs.microsoft.com/azure/role-based-access-control/overview).
* Les journaux peuvent être collectés à partir de tous les types de ressources, et non uniquement des données de machines virtuelles basées sur agent. Par exemple, les journaux d’activité d’audit Azure.
* Chaque client peut avoir des paramètres différents pour son espace de travail, par exemple, pour la rétention ou la limitation des données.
* Elle permet l’isolation entre les clients pour répondre aux exigences réglementaires et de conformité.
* Les frais liés à chaque espace de travail sont intégrés à l’abonnement du client.

Les avantages de l’architecture distribuée sont les suivants :

* La visualisation et l’analyse centralisées des données sur les locataires à l’aide d’outils tels que les classeurs Azure Monitor peuvent entraîner un ralentissement des expériences, en particulier lors de l’analyse de données dans plus de 50 espaces de travail.
* Si les clients ne sont pas intégrés pour la gestion déléguée des ressources Azure, les administrateurs de fournisseurs de services doivent être approvisionnés dans le répertoire du client et il est plus difficile pour le fournisseur de services de gérer un grand nombre de locataires clients à la fois.

### <a name="2-central---logs-are-stored-in-a-workspace-located-in-the-service-provider-tenant"></a>2. Central : les journaux d’activité sont stockés dans un espace de travail situé dans le locataire du fournisseur de services

Dans cette architecture, les journaux d’activité ne sont pas stockés dans les locataires du client, mais dans un emplacement central situé dans l’un des abonnements du fournisseur de services. Les agents qui sont installés sur les machines virtuelles du client sont configurés pour envoyer leurs journaux d’activité vers cet espace de travail à l’aide de l’ID et de la clé secrète de l’espace de travail.

Les avantages de l’architecture centralisée sont les suivants :

* Il est facile de gérer de nombreux clients et de les intégrer à différents systèmes backend.
* Le fournisseur de services dispose d’une propriété complète sur les journaux d’activité et les divers artefacts, tels que les fonctions et les requêtes enregistrées.
* Le fournisseur de services peut effectuer des analyses sur l’ensemble de ses clients.

Les inconvénients de l’architecture centralisée sont les suivants :

* Cette architecture est applicable uniquement pour les données de machines virtuelles basées sur agent. Elle ne prend pas en compte les sources de données PaaS, SaaS et Azure Fabric.
* Il peut être difficile de distinguer les données des différents clients lorsqu’elles sont fusionnées dans un même espace de travail. La seule bonne méthode consiste à utiliser le nom de domaine complet (FQDN) de l’ordinateur ou l’ID de l’abonnement Azure. 
* Toutes les données de tous les clients sont stockées dans la même région avec une seule facture, et les mêmes paramètres de rétention et de configuration.
* Les services Azure Fabric et PaaS, par exemple Diagnostics Azure et les journaux d’audit Azure, nécessitent que l’espace de travail se trouve dans le même locataire que la ressource. Ils ne peuvent donc pas envoyer les journaux vers l’espace de travail central.
* Tous les agents de machine virtuelle de l’ensemble des clients sont authentifiés auprès de l’espace de travail central à l’aide du même ID et de la même clé d’espace de travail. Il n’existe aucune méthode permettant de bloquer les journaux d’activité d’un client sans interrompre les autres clients.

### <a name="3-hybrid---logs-are-stored-in-workspace-located-in-the-customers-tenant-and-some-of-them-are-pulled-to-a-central-location"></a>3. Hybride : les journaux d’activité sont stockés dans l’espace de travail situé dans le locataire du client, et certains d’entre eux sont envoyés vers un emplacement central.

Cette troisième architecture est un mélange des deux précédentes. Elle est basée sur l’architecture distribuée où les journaux d’activité sont stockés localement pour chaque client, mais elle utilise un mécanisme permettant de créer un référentiel central pour les journaux d’activité. Une partie des journaux d’activité est extraite et envoyée vers un emplacement central à des fins de création de rapports et d’analyse. Cette partie correspond parfois à un petit nombre de types de données ou à un récapitulatif d’activité, par exemple des statistiques quotidiennes.

Il existe deux options pour implémenter des journaux dans un emplacement central :

1. Espace de travail central : le fournisseur de services peut créer un espace de travail dans son locataire et utiliser un script qui utilise [l’API de requête](https://dev.loganalytics.io/) avec [l’API de collecte de données](../../azure-monitor/platform/data-collector-api.md) pour importer les données des différents espaces de travail dans l’emplacement central. Une autre option (autre que le script) consiste à utiliser une [Azure Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-overview).

2. Power BI comme emplacement central : Power BI peut servir d’emplacement central quand les différents espaces de travail exportent des données vers lui en utilisant l’intégration entre l’espace de travail Log Analytics et [Power BI](../../azure-monitor/platform/powerbi.md). 

## <a name="next-steps"></a>Étapes suivantes

* Automatiser la création et la configuration des espaces de travail à l’aide de [modèles Resource Manager](template-workspace-configuration.md)

* Automatiser la création des espaces de travail à l’aide de [PowerShell](../../azure-monitor/platform/powershell-workspace-configuration.md) 

* Utiliser [Alertes](../../azure-monitor/platform/alerts-overview.md) pour intégrer les espaces de travail aux systèmes existants

* Générer des rapports de synthèse à l’aide de [Power BI](../../azure-monitor/platform/powerbi.md)

* Intégrer des clients à la [gestion déléguée des ressources Azure](https://docs.microsoft.com/azure/lighthouse/concepts/azure-delegated-resource-management)
