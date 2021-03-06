---
title: Configurer un tunnel VPN Always On
titleSuffix: Azure VPN Gateway
description: Étapes de configuration d’un tunnel VPN Always On pour la passerelle VPN
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: conceptual
ms.date: 03/12/2020
ms.author: cherylmc
ms.openlocfilehash: 9036992a354b41cd75735e5ccd895d7287a00e91
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2020
ms.locfileid: "79371729"
---
# <a name="configure-an-always-on-vpn-device-tunnel"></a>Configurer un tunnel de périphérique VPN Always On

[!INCLUDE [intro](../../includes/vpn-gateway-vwan-always-on-intro.md)]

## <a name="configure-the-gateway"></a>Configurer la passerelle

Configurez la passerelle VPN pour utiliser IKEv2 et l'authentification basée sur les certificats à l'aide de l'article [Configurer une connexion VPN point à site](vpn-gateway-howto-point-to-site-resource-manager-portal.md).

## <a name="configure-the-device-tunnel"></a>Configurer le tunnel d’appareil

[!INCLUDE [device tunnel](../../includes/vpn-gateway-vwan-always-on-device.md)]

## <a name="to-remove-a-profile"></a>Pour supprimer un profil

Pour supprimer le profil, exécutez la commande suivante :

![Nettoyage](./media/vpn-gateway-howto-always-on-device-tunnel/cleanup.png)

## <a name="next-steps"></a>Étapes suivantes

Pour résoudre les problèmes, consultez [Problèmes de connexion point à site Azure](vpn-gateway-troubleshoot-vpn-point-to-site-connection-problems.md)
