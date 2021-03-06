---
title: Stratégie de gestion des API Azure - Générer une signature d’accès partagé
titleSuffix: Azure API Management
description: 'Exemple de stratégie de gestion des API Azure : montre comment générer une signature d’accès partagé à l’aide d’expressions et transférer la demande vers le stockage Azure avec une stratégie rewrite-uri.'
services: api-management
documentationcenter: ''
author: vladvino
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 10/13/2017
ms.author: apimpm
ms.openlocfilehash: 0f003bc268af6b7f8bd6b046ae84734dbefeac28
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2020
ms.locfileid: "75442459"
---
# <a name="generate-shared-access-signature"></a>Générer une signature d’accès partagé

Cet article présente un exemple de stratégie de gestion des API Azure qui montre comment générer une [signature d’accès partagé](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) à l’aide d’expressions et transférer la demande vers le stockage Azure avec une stratégie rewrite-uri. Pour définir ou modifier un code de stratégie, suivez les étapes décrites dans [Définir ou modifier une stratégie](../set-edit-policies.md). Pour voir d’autres exemples, consultez [Exemples de stratégie](../policy-samples.md).

## <a name="policy"></a>Stratégie

Collez le code dans le bloc **inbound**.

[!code-xml[Main](../../../api-management-policy-samples/examples/Generate Shared Access Signature and forward request to Azure storage.policy.xml)]

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur les stratégies APIM :

+ [Stratégies de transformation](../api-management-transformation-policies.md)
+ [Exemples de stratégie](../policy-samples.md)

