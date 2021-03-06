---
title: Envoyer des notifications planifiées | Microsoft Docs
description: Cette rubrique décrit l'utilisation de notifications planifiées avec Azure Notification Hubs.
services: notification-hubs
documentationcenter: .net
keywords: notifications push,notification push,planification de notifications push
author: sethmanheim
manager: femila
editor: jwargo
ms.assetid: 6b718c75-75dd-4c99-aee3-db1288235c1a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: dotnet
ms.topic: article
ms.date: 01/04/2019
ms.author: sethm
ms.reviewer: jowargo
ms.lastreviewed: 01/04/2019
ms.openlocfilehash: ef5eedaa903480ae670f9bc48d0af89744a99d22
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2020
ms.locfileid: "71213004"
---
# <a name="how-to-send-scheduled-notifications"></a>Procédure : Envoyer des notifications planifiées

Si vous avez un scénario dans lequel vous souhaitez envoyer une notification à un moment donné dans le futur, mais que vous ne disposez pas d'un moyen simple d'activer votre code principal pour envoyer la notification. Notification Hubs de niveau Standard prend en charge une fonctionnalité qui vous permet de planifier des notifications jusqu’à 7 jours à l’avance.


## <a name="schedule-your-notifications"></a>Planifier vos notifications
Lorsque vous envoyez une notification, utilisez simplement la classe [`ScheduledNotification`](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) dans le Kit de développement logiciel (SDK) Notification Hubs, comme indiqué dans l'exemple suivant :

```csharp
Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));
```

## <a name="cancel-scheduled-notifications"></a>Annuler des notifications planifiées
Vous pouvez également annuler une notification précédemment planifiée à l'aide de son ID de notification :

```csharp
await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);
```

Il n'existe aucune limite quant au nombre de notifications planifiées que vous pouvez envoyer.

## <a name="next-steps"></a>Étapes suivantes

Consultez les didacticiels suivants :

 - [Notifications push vers tous les appareils inscrits](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)
 - [Notifications Push vers des appareils spécifiques](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md)
 - [Notifications push localisées](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
 - [Notifications Push vers des utilisateurs spécifiques](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) 
 - [Notifications Push en fonction de la localisation](notification-hubs-push-bing-spatial-data-geofencing-notification.md)
