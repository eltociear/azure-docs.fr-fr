---
title: Azure Security Control – Protection des données
description: Contrôle de sécurité Azure – Protection des données
author: msmbaldwin
ms.service: security
ms.topic: conceptual
ms.date: 04/14/2020
ms.author: mbaldwin
ms.custom: security-benchmark
ms.openlocfilehash: 035894c80e619851264aae91daa2d7852d156964
ms.sourcegitcommit: b80aafd2c71d7366838811e92bd234ddbab507b6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81408545"
---
# <a name="security-control-data-protection"></a>Contrôle de sécurité : Protection des données

Les recommandations relatives à la protection des données se concentrent sur les problèmes de chiffrement, les listes de contrôle d’accès, le contrôle d’accès basé sur l’identité et l’enregistrement d’audit pour l’accès aux données.

## <a name="41-maintain-an-inventory-of-sensitive-information"></a>4.1 : Conserver un inventaire des informations sensibles

| Identifiant Azure | Identifiants CIS | Responsabilité |
|--|--|--|
| 4,1 | 13.1 | Customer |

Utilisez des balises pour faciliter le suivi des ressources Azure qui stockent ou traitent des informations sensibles.

- [Guide pratique pour créer et utiliser des étiquettes](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)

## <a name="42-isolate-systems-storing-or-processing-sensitive-information"></a>4.2 : Isoler les systèmes qui stockent ou traitent les informations sensibles

| Identifiant Azure | Identifiants CIS | Responsabilité |
|--|--|--|
| 4,2 | 13.2, 2.10 | Customer |

Implémentez une isolation en utilisant des abonnements et groupes d’administration distincts selon les domaines de sécurité (par exemple, le type d’environnement et le niveau de confidentialité des données). Vous pouvez limiter le niveau d’accès à vos ressources Azure demandées par vos applications et environnements d’entreprise. Il est possible de contrôler l’accès aux ressources Azure au moyen du contrôle d’accès en fonction du rôle Azure Active Directory. 

- [Guide pratique pour créer des abonnements Azure supplémentaires](https://docs.microsoft.com/azure/billing/billing-create-subscription)

- [Guide pratique pour créer des groupes d’administration](https://docs.microsoft.com/azure/governance/management-groups/create)

- [Guide pratique pour créer et utiliser des étiquettes](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)

## <a name="43-monitor-and-block-unauthorized-transfer-of-sensitive-information"></a>4.3. : Surveiller et bloquer le transfert non autorisé d’informations sensibles

| Identifiant Azure | Identifiants CIS | Responsabilité |
|--|--|--|
| 4.3 | 13.3 | Partagé |

Exploitez une solution tierce issue de la Place de marché Azure sur les périmètres du réseau, qui surveille et bloque les transferts non autorisés d’informations sensibles tout en alertant les professionnels de la sécurité de l’information.

Pour la plateforme sous-jacente, gérée par Microsoft, Microsoft traite tout le contenu client comme sensible et assure une protection contre la perte et l’exposition de données client. Pour garantir la sécurité des données client dans Azure, Microsoft a implémenté et tient à jour une suite de contrôles et de fonctionnalités de protection des données robustes.

- [Présentation de la protection des données client dans Azure](https://docs.microsoft.com/azure/security/fundamentals/protection-customer-data)

## <a name="44-encrypt-all-sensitive-information-in-transit"></a>4.4 : Chiffrer toutes les informations sensibles en transit

| Identifiant Azure | Identifiants CIS | Responsabilité |
|--|--|--|
| 4.4 | 14.4 | Partagé |

Chiffrer toutes les informations sensibles en transit. Assurez-vous que les clients qui se connectent à vos ressources Azure peuvent négocier TLS 1.2 ou une version ultérieure.

Suivez les recommandations d’Azure Security Center relatives au chiffrement au repos et au chiffrement en transit, le cas échéant.

- [Présentation du chiffrement en transit avec Azure](https://docs.microsoft.com/azure/security/fundamentals/encryption-overview#encryption-of-data-in-transit)

## <a name="45-use-an-active-discovery-tool-to-identify-sensitive-data"></a>4.5 : Utiliser un outil de découverte actif pour identifier les données sensibles

| Identifiant Azure | Identifiants CIS | Responsabilité |
|--|--|--|
| 4.5 | 14.5 | Partagé |

Si aucune fonctionnalité n’est disponible pour votre service spécifique dans Azure, utilisez un outil de découverte actif tiers pour identifier toutes les informations sensibles stockées, traitées ou transmises par les systèmes technologiques de l’organisation, y compris celles situées sur site ou à un fournisseur de services à distance et mettez à jour l’inventaire des informations sensibles de l’organisation.

Utilisez Azure Information Protection pour identifier les informations sensibles dans les documents Office 365.

Utilisez Azure SQL Information Protection pour faciliter la classification et l’étiquetage des informations stockées dans les bases de données SQL Azure.

- [Guide pratique pour implémenter la recherche de données Azure SQL](https://docs.microsoft.com/azure/sql-database/sql-database-data-discovery-and-classification)

- [Guide pratique pour implémenter Azure Information Protection](https://docs.microsoft.com/azure/information-protection/deployment-roadmap)

- [Présentation de la protection des données client dans Azure](https://docs.microsoft.com/azure/security/fundamentals/protection-customer-data)

## <a name="46-use-role-based-access-control-to-control-access-to-resources"></a>4.6 : Utiliser le contrôle d’accès en fonction du rôle pour contrôler l’accès aux ressources

| Identifiant Azure | Identifiants CIS | Responsabilité |
|--|--|--|
| 4.6 | 14.6 | Customer |

Utilisez Azure AD RBAC pour contrôler l’accès aux données et aux ressources, sinon utilisez des méthodes de contrôle d’accès spécifiques au service.

- [Guide pratique pour configurer le contrôle RBAC dans Azure](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal)

## <a name="47-use-host-based-data-loss-prevention-to-enforce-access-control"></a>4.7 : Utiliser la protection contre la perte de données basée sur l’hôte pour appliquer le contrôle d’accès

| Identifiant Azure | Identifiants CIS | Responsabilité |
|--|--|--|
| 4,7 | 14.7 | Partagé |

Si nécessaire à des fins de conformité sur les ressources de calcul, implémentez un outil tiers (par exemple, une solution automatisée de protection contre la perte de données basée sur un hôte) pour appliquer des contrôles d’accès aux données même lorsque celles-ci sont copiées à partir d’un système.

Pour la plateforme sous-jacente qui est gérée par Microsoft, Microsoft traite tout le contenu client comme sensible et déploie d'importants efforts pour vous protéger contre la perte et l’exposition des données client. Pour garantir la sécurité des données client dans Azure, Microsoft a implémenté et tient à jour une suite de contrôles et de fonctionnalités de protection des données robustes.

- [Présentation de la protection des données client dans Azure](https://docs.microsoft.com/azure/security/fundamentals/protection-customer-data)

## <a name="48-encrypt-sensitive-information-at-rest"></a>4.8 : Chiffrer des informations sensibles au repos

| Identifiant Azure | Identifiants CIS | Responsabilité |
|--|--|--|
| 4.8 | 14.8 | Customer |

Utilisez le chiffrement au repos sur toutes les ressources Azure. Microsoft recommande d’autoriser Azure à gérer vos clés de chiffrement, mais il existe une option vous permettant de gérer vos propres clés dans certains cas. 

- [Présentation du chiffrement au repos dans Azure](https://docs.microsoft.com/azure/security/fundamentals/encryption-atrest)

- [Guide pratique pour configurer des clés de chiffrement gérées par le client](https://docs.microsoft.com/azure/storage/common/storage-encryption-keys-portal)

## <a name="49-log-and-alert-on-changes-to-critical-azure-resources"></a>4.9 : Consigner et alerter les modifications apportées aux ressources Azure critiques

| Identifiant Azure | Identifiants CIS | Responsabilité |
|--|--|--|
| 4,9 | 14.9 | Customer |

Utilisez Azure Monitor avec le journal des activités Azure pour créer des alertes lorsque des modifications sont apportées à des ressources Azure critiques.

- [Guide pratique pour créer des alertes sur les événements du journal d’activité Azure](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-activity-log)


## <a name="next-steps"></a>Étapes suivantes

- Consultez le contrôle de sécurité suivant :  [Gestion des vulnérabilités](security-control-vulnerability-management.md)