---
title: 'Activation du Proxy d’application Azure AD : Historique de publication des versions | Microsoft Docs'
description: Cet article répertorie toutes les publications du Proxy d’application Azure AD et détaille les nouvelles fonctionnalités ainsi que les problèmes corrigés
services: active-directory
documentationcenter: ''
author: msmimart
manager: CelesteDG
editor: ''
ms.assetid: ''
ms.service: active-directory
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/07/2020
ms.subservice: app-mgmt
ms.author: mimart
ms.collection: M365-identity-device-management
ms.openlocfilehash: f027fbce66a73306165a0ad35d1ba3faa7a5c0bc
ms.sourcegitcommit: 7d8158fcdcc25107dfda98a355bf4ee6343c0f5c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/09/2020
ms.locfileid: "80983889"
---
# <a name="azure-ad-application-proxy-version-release-history"></a>Activation du Proxy d’application Azure AD : Historique de publication des versions
Cet article répertorie les versions et les fonctionnalités du Proxy d’application Azure Active Directory (Azure AD) qui ont été publiées. L’équipe Azure AD met régulièrement à jour le Proxy d’application avec de nouvelles fonctions et fonctionnalités. Les connecteurs du Proxy d’application sont mis à jour automatiquement lorsqu’une nouvelle version est publiée. 

Nous vous recommandons de veiller à ce que les mises à jour automatiques soient activées pour vos connecteurs afin de vous assurer que vous disposez des dernières fonctionnalités et des correctifs de bogues. Microsoft offre une prise en charge directe de la version la plus récente du connecteur et de la version précédente.

Voici la liste des ressources connexes :

Ressource |  Détails
--------- | --------- |
Activer le Proxy d’application | Les prérequis pour l’activation du Proxy d’application et l’installation et l’inscription d’un connecteur sont détaillés dans ce [tutoriel](application-proxy-add-on-premises-application.md).
Présentation des connecteurs de proxy d’application Azure AD | Apprenez-en plus sur la [gestion des connecteurs](application-proxy-connectors.md) et leur [mise à niveau automatique](application-proxy-connectors.md#automatic-updates).
Télécharger le connecteur de proxy d’application Azure AD |  [Téléchargez le connecteur le plus récent](https://download.msappproxy.net/subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/connector/download).

## <a name="1515260"></a>1.5.1526.0

### <a name="release-status"></a>État de la version

7 avril 2020 : publiée pour téléchargement

### <a name="new-features-and-improvements"></a>Améliorations et nouvelles fonctionnalités
-   Les connecteurs utilisent uniquement TLS 1.2 pour toutes les connexions. Pour plus d’informations, consultez [Prérequis pour le connecteur](application-proxy-add-on-premises-application.md#before-you-begin).
- Signalisation améliorée entre le connecteur et les services Azure. Cela comprend la prise en charge des sessions fiables pour la communication WCF entre le connecteur et les services Azure et des améliorations de la mise en cache DNS pour les communications WebSocket.
- Prise en charge de la configuration d’un proxy entre le connecteur et l’application back-end. Pour plus d’informations, consultez [Utiliser des serveurs proxy locaux existants](application-proxy-configure-connectors-with-proxy-servers.md).

### <a name="fixed-issues"></a>Problèmes résolus
- Suppression du retour au port 8080 pour les communications entre le connecteur et les services Azure.
- Ajout de traces de débogage pour les communications WebSocket. 
- Résolution de la préservation de l’attribut SameSite lorsqu’il est défini sur les cookies de l’application back-end.

## <a name="156120"></a>1.5.612.0

### <a name="release-status"></a>État de la version

20 septembre 2018 : publiée pour téléchargement

### <a name="new-features-and-improvements"></a>Améliorations et nouvelles fonctionnalités

- Ajout de la prise en charge de WebSocket pour l’application QlikSense. Pour en savoir plus sur l’intégration de QlikSense avec le Proxy d’application, consultez cette [procédure pas à pas](application-proxy-qlik.md). 
- Amélioration de l’assistant d’installation pour simplifier la configuration d’un proxy de sortie. 
- Définissez TLS 1.2 comme protocole par défaut pour les connecteurs. 
- Ajout d’un nouveau contrat de licence de l’utilisateur final (EULA).  

### <a name="fixed-issues"></a>Problèmes résolus

- Correction d’un bogue entraînant des fuites de mémoire dans le connecteur.
- Mise à jour de la version d’Azure Service Bus, comprenant un correctif des problèmes de délais d’expiration du connecteur.

## <a name="154020"></a>1.5.402.0

### <a name="release-status"></a>État de la version

19 janvier 2018 : publiée pour téléchargement

### <a name="fixed-issues"></a>Problèmes résolus

- Ajout de la prise en charge des domaines personnalisés nécessitant une traduction de domaine dans le cookie.

## <a name="151320"></a>1.5.132.0

### <a name="release-status"></a>État de la version 

25 mai 2017 : publiée pour téléchargement 

### <a name="new-features-and-improvements"></a>Améliorations et nouvelles fonctionnalités 

Amélioration du contrôle des limites de connexion de sortie des connecteurs. 

## <a name="15360"></a>1.5.36.0

### <a name="release-status"></a>État de la version

15 avril 2017 : publiée pour téléchargement

### <a name="new-features-and-improvements"></a>Améliorations et nouvelles fonctionnalités

- Intégration simplifiée et gestion nécessitant moins de ports. Le Proxy d’application nécessite désormais l’ouverture de seulement deux ports de sortie standards : 443 et 80. Le Proxy d’application continue d’utiliser des connexions sortantes uniquement. Vous n’avez donc toujours pas besoin de composants dans une zone DMZ. Pour plus d’informations, consultez notre [documentation relative à la configuration](application-proxy-add-on-premises-application.md).  
- Si pris en charge par votre proxy ou votre pare-feu, vous pouvez maintenant ouvrir votre réseau via DNS à la place d’une plage d’adresses IP. Les services du Proxy d’application nécessitent des connexions à *.msappproxy.net et *.servicebus.windows.net uniquement.


## <a name="earlier-versions"></a>Versions antérieures

Si vous utilisez une version de connecteur du Proxy d’Application antérieure à 1.5.36.0, mettez-la à jour vers la dernière version pour vous assurer les dernières fonctionnalités entièrement prises en charge.

## <a name="next-steps"></a>Étapes suivantes
- En savoir plus sur l’[Accès à distance aux applications locales via le service Proxy d’application Azure AD](application-proxy.md).
- Pour commencer à utiliser Proxy d’application, consultez [Tutoriel : Ajouter des applications locales pour un accès à distance via le service Proxy d’application](application-proxy-add-on-premises-application.md).
