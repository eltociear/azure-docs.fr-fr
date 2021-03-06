---
title: Se connecter à Windows Virtual Desktop à partir d’iOS – Azure
description: Guide pratique pour se connecter à Windows Virtual Desktop à l’aide du client iOS.
services: virtual-desktop
author: heidilohr
ms.service: virtual-desktop
ms.topic: conceptual
ms.date: 03/30/2020
ms.author: helohr
manager: lizross
ms.openlocfilehash: 80bbb90c46376d29c1f4f8b0701cf4059db32246
ms.sourcegitcommit: 50ef5c2798da04cf746181fbfa3253fca366feaa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2020
ms.locfileid: "82614138"
---
# <a name="connect-with-the-ios-client"></a>Se connecter avec le client iOS

> S’applique à : iOS 13.0 ou ultérieur. Compatible avec iPhone, iPad et iPod touch.

>[!IMPORTANT]
>Ce contenu s’applique à la version Automne 2019 qui ne prend pas en charge les objets Azure Resource Manager Windows Virtual Desktop. Si vous essayez de gérer les objets Azure Resource Manager Windows Virtual Desktop introduits dans la mise à jour Printemps 2020, consultez [cet article](../connect-ios.md).

Vous pouvez accéder aux ressources Windows Virtual Desktop à partir de votre appareil iOS avec notre client téléchargeable. Ce guide vous explique comment configurer le client iOS.

## <a name="install-the-ios-client"></a>Installer le client iOS

Pour commencer, [téléchargez](https://aka.ms/rdios) et installez le client sur votre appareil iOS.

## <a name="subscribe-to-a-feed"></a>S’abonner à un flux

Abonnez-vous au flux fourni par votre administrateur pour obtenir la liste des ressources managées auxquelles vous pouvez accéder sur votre appareil iOS.

Pour s’abonner à un flux :

1. Dans le Centre de connexion, appuyez sur **+** , puis sur **Add Workspace** (Ajouter un espace de travail).
2. Entrez l’URL du flux dans le champ **Feed URL** (URL du flux). Il peut s’agir d’une URL ou d’une adresse e-mail.
   - Si vous utilisez une URL, utilisez celle que votre administrateur vous a donnée. Normalement, l’URL est <https://rdweb.wvd.microsoft.com>.
   - Pour utiliser l’e-mail, entrez votre adresse e-mail. Cela indique au client de rechercher une URL associée à votre adresse e-mail si votre administrateur a configuré le serveur de cette manière.
3. Appuyez sur **Suivant**.
4. À l’invite, indiquez vos informations d’identification.
   - Pour **Nom d’utilisateur**, indiquez le nom de l’utilisateur ayant l’autorisation d’accéder aux ressources.
   - Pour **Mot de passe**, indiquez le mot de passe associé au nom d’utilisateur.
   - Vous pouvez également être invité à fournir des facteurs supplémentaires si votre administrateur a configuré l’authentification de cette manière.
5. Appuyez sur **Save** (Enregistrer).

Le Centre de connexion doit ensuite afficher les ressources distantes.

Une fois que vous êtes abonné à un flux, son contenu est mis à jour automatiquement et régulièrement. Des ressources peuvent être ajoutées, modifiées ou supprimées en fonction des modifications apportées par votre administrateur.

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur l’utilisation du client iOS, consultez [Bien démarrer avec le client iOS](/windows-server/remote/remote-desktop-services/clients/remote-desktop-ios/).
