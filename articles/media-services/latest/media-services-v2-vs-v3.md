---
title: Migrer d’Azure Media Services v2 vers v3
description: Cet article décrit les changements qui ont été introduits dans Azure Media Services v3 et montre les différences entre les deux versions.
services: media-services
documentationcenter: na
author: Juliako
manager: femila
editor: ''
tags: ''
keywords: azure media services, flux, diffusion, en direct, hors connexion
ms.service: media-services
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: media
ms.date: 03/09/2020
ms.author: juliako
ms.openlocfilehash: fd094e35ceaa718ec1b258d74106b39744cbd16f
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2020
ms.locfileid: "79087823"
---
# <a name="media-services-v2-vs-v3"></a>Media Services v2 par rapport à Media Services v3

Cet article décrit les changements qui ont été introduits dans Azure Media Services v3 et montre les différences entre les deux versions.

## <a name="general-changes-from-v2"></a>Modifications générales par rapport à v2

* Pour les ressources créées avec la version v3, Media Services prend en charge uniquement le [chiffrement du stockage côté serveur de Stockage Azure](https://docs.microsoft.com/azure/storage/common/storage-service-encryption).
    * Vous pouvez utiliser des API v3 avec des ressources créées à l’aide d’API v2 qui disposaient d’un [chiffrement de stockage](../previous/media-services-rest-storage-encryption.md) (AES 256) fourni par Media Services.
    * Vous ne pouvez pas créer de ressources avec le [chiffrement du stockage](../previous/media-services-rest-storage-encryption.md) AES 256 hérité à l’aide d’API v3.
* Si les propriétés de la [ressource](assets-concept.md) dans v3 sont différentes de celles de v2, voir [comment les propriétés sont mappées](#map-v3-asset-properties-to-v2).
* Les kits de développement logiciel (SDK) v3 sont dissociés du Storage SDK, ce qui vous offre davantage de contrôle sur la version de SDK Stockage à utiliser, et évite les problèmes de gestion de version. 
* Dans les API v3, toutes les vitesses d’encodage sont exprimées en bits par seconde. Ceci diffère des préréglages de Media Encoder Standard v2. Par exemple, un débit en bits dans v2 exprimé sous la forme 128 Kbits/s, sera exprimé dans v3 sous la forme 128000 (bits/seconde). 
* Les entités AssetFiles, AccessPolicies et IngestManifests n’existent pas dans v3.
* La propriété IAsset.ParentAssets n’existe pas dans la version 3.
* ContentKeys n’est plus une entité, mais une propriété du localisateur de streaming.
* La prise en charge de la grille d’événements remplace NotificationEndpoints.
* Les entités suivantes ont été renommées :
    * JobOutput remplace Task et fait désormais partie d’un travail.
    * StreamingLocator remplace Locator.
    * LiveEvent remplace Channel.<br/>La facturation des événements en direct est basée sur les compteurs de canal live. Pour plus d’informations, consultez [facturation](live-event-states-billing.md) et [tarifs](https://azure.microsoft.com/pricing/details/media-services/).
    * LiveOutput remplace Program.
* Les sorties en direct démarrent dès leur création et s’arrêtent à leur suppression. Les programmes fonctionnaient différemment dans les API v2. Il fallait les démarrer après leur création.
* Pour obtenir des informations sur un travail, vous devez connaître le nom de la transformation sous lequel le travail a été créé. 
* Dans la v2, les fichiers XML de métadonnées [entrants](../previous/media-services-input-metadata-schema.md) et [sortants](../previous/media-services-output-metadata-schema.md) sont générés à la suite d’un travail d’encodage. Dans la v3, le format de métadonnées est passé de XML à JSON. 
* Dans Media Services v2, vous pouvez spécifier le vecteur d’initialisation (IV). Dans Media Services V3, vous ne pouvez pas spécifier le système FairPlay IV. Bien qu’il n’ait pas d’impact sur les clients qui utilisent Media Services pour l’empaquetage et la remise de licence, il peut être problématique lors de l’utilisation d’un système DRM tiers pour fournir les licences FairPlay (mode hybride). Dans ce cas, il est important de savoir que le système FairPlay IV est dérivé de l’ID de clé CBCS et peut être récupéré à l’aide de la formule suivante :

    ```
    string cbcsIV =  Convert.ToBase64String(HexStringToByteArray(cbcsGuid.ToString().Replace("-", string.Empty)));
    ```

    par

    ``` 
    public static byte[] HexStringToByteArray(string hex)
    {
        return Enumerable.Range(0, hex.Length)
            .Where(x => x % 2 == 0)
            .Select(x => Convert.ToByte(hex.Substring(x, 2), 16))
            .ToArray();
    }
    ```

    Pour plus d’informations, voir le [code C# Azure Functions pour Media Services V3 en mode hybride pour les opérations en direct et VOD](https://github.com/Azure-Samples/media-services-v3-dotnet-core-functions-integration/tree/master/LiveAndVodDRMOperationsV3).
 
> [!NOTE]
> Examinez les conventions d’affectation de noms appliquées aux [ressources Media Services v3](media-services-apis-overview.md#naming-conventions). Voir également [Attribution de noms à des objets blob](assets-concept.md#naming).

## <a name="feature-gaps-with-respect-to-v2-apis"></a>Différences de fonctionnalités par rapport aux API v2

Les API v3 présentent les différences de fonctionnalités suivantes par rapport aux API v2. Le gommage de ces différences est en cours.

* L’[Encodeur Premium](../previous/media-services-premium-workflow-encoder-formats.md) et les [processeurs d’analytique multimédia](../previous/media-services-analytics-overview.md) hérités (indexeur Azure Media Services 2 en préversion, Face Redactor, etc.) ne sont pas accessibles via v3.<br/>Les clients qui souhaitent migrer à partir de l’indexeur multimédia 1 ou 2 en préversion peuvent utiliser immédiatement l’AudioAnalyzer prédéfini dans l’API v3.  Cet nouveau préréglage contient davantage de fonctionnalités que l’ancien indexeur multimédia 1 ou 2. 
* La plupart des [fonctionnalités avancées de Media Encoder Standard dans les API v2](../previous/media-services-advanced-encoding-with-mes.md) ne sont actuellement pas disponibles dans v3, par exemple :
  
    * Combinaison de ressources
    * Superpositions
    * Rognage
    * Sprites de miniatures
    * Insertion d’une piste audio en mode silencieux lorsque l’entrée ne produit pas de son
    * Insertion d’une piste vidéo lorsque l’entrée ne comporte aucune vidéo
* Les événements en direct avec transcodage ne gèrent actuellement pas l’insertion d’ardoise à mi-parcours ni l’insertion de marqueur publicitaire par le biais d’un appel d’API. 
 
## <a name="asset-specific-changes"></a>Modifications spécifiques aux ressources

### <a name="map-v3-asset-properties-to-v2"></a>Mapper les propriétés de l’élément multimédia v3 à v2

Le tableau suivant montre comment les propriétés de l’[élément multimédia](https://docs.microsoft.com/rest/api/media/assets/createorupdate#asset)de v3 sont mappées aux propriétés de l’élément multimédia de v2.

|Propriétés de v3|Propriétés de v2|
|---|---|
|`id` : (unique) chemin d’accès complet à Azure Resource Manager, voir les exemples dans [Élément multimédia](https://docs.microsoft.com/rest/api/media/assets/createorupdate)||
|`name` : (unique) consultez [Convention d’affectation de noms](media-services-apis-overview.md#naming-conventions) ||
|`alternateId`|`AlternateId`|
|`assetId`|`Id` : valeur (unique) commençant par le préfixe `nb:cid:UUID:`.|
|`created`|`Created`|
|`description`|`Name`|
|`lastModified`|`LastModified`|
|`storageAccountName`|`StorageAccountName`|
|`storageEncryptionFormat`| `Options` (options de création)|
|`type`||

### <a name="storage-side-encryption"></a>Chiffrement côté stockage

Pour protéger vos éléments au repos, les ressources doivent être chiffrées par le chiffrement côté stockage. Le tableau suivant montre comment le chiffrement côté stockage fonctionne dans Media Services :

|Option de chiffrement|Description|Media Services v2|Media Services v3|
|---|---|---|---|
|Chiffrement du stockage de Media Services|Chiffrement AES-256, clé gérée par Media Services.|Pris en charge<sup>(1)</sup>|Non pris en charge<sup>(2)</sup>|
|[Storage Service Encryption pour les données au repos](https://docs.microsoft.com/azure/storage/common/storage-service-encryption)|Chiffrement côté serveur proposé par le stockage Azure, clé gérée par Azure ou par un client.|Prise en charge|Prise en charge|
|[Chiffrement de stockage côté client](https://docs.microsoft.com/azure/storage/common/storage-client-side-encryption)|Chiffrement côté client proposé par le stockage Azure, clé gérée par un client dans un coffre de clés.|Non pris en charge|Non pris en charge|

<sup>1</sup> Bien que Media Services prenne en charge la gestion de contenu en clair/sans aucune forme de chiffrement, ce n’est pas conseillé.

<sup>2</sup> Dans Media Services v3, le chiffrement de stockage (chiffrement AES-256) est uniquement pris en charge pour la compatibilité descendante lorsque vos ressources ont été créées avec Media Services v2. Cela signifie que la version v3 fonctionne avec les ressources chiffrées du stockage existant mais qu’elle n’autorisera pas de nouvelles créations.

## <a name="code-differences"></a>Différences de code

Le tableau suivant présente les différences de code entre v2 et v3 pour des scénarios courants.

|Scénario|API V2|API V3|
|---|---|---|
|Créer une ressource et charger un fichier |[Exemple .NET v2](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-aes/blob/master/DynamicEncryptionWithAES/DynamicEncryptionWithAES/Program.cs#L113)|[Exemple .NET v3](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#L169)|
|Soumettre un travail|[Exemple .NET v2](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-aes/blob/master/DynamicEncryptionWithAES/DynamicEncryptionWithAES/Program.cs#L146)|[Exemple .NET v3](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#L298)<br/><br/>Montre comment créer au préalable une transformation, puis soumettre un travail.|
|Publier une ressource avec chiffrement AES |1. Créer une ContentKeyAuthorizationPolicyOption<br/>2. Créer une ContentKeyAuthorizationPolicy<br/>3. Créer une AssetDeliveryPolicy<br/>4. Créer une ressource et charger du contenu OU soumettre un travail et utiliser une ressource en sortie<br/>5. Associer une AssetDeliveryPolicy à un Asset<br/>6. Créer une ContentKey<br/>7. Attacher un ContentKey à un Asset<br/>8. Créer une AccessPolicy<br/>9. Créer un Locator<br/><br/>[Exemple .NET v2](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-aes/blob/master/DynamicEncryptionWithAES/DynamicEncryptionWithAES/Program.cs#L64)|1. Créer une stratégie de clé de contenu<br/>2. Créer un Asset<br/>3. Charger du contenu ou utiliser un Asset comme JobOutput<br/>4. Créer un localisateur de streaming<br/><br/>[Exemple .NET v3](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/EncryptWithAES/Program.cs#L105)|
|Obtenir des détails de travaux et gérer des travaux |[Gérer des travaux avec v2](../previous/media-services-dotnet-manage-entities.md#get-a-job-reference) |[Gérer des travaux avec v3](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/UploadEncodeAndStreamFiles/Program.cs#L546)|

> [!NOTE]
> Veuillez marquer cet article d’un signet afin de pouvoir continuer à suivre les mises à jour.

## <a name="ask-questions-give-feedback-get-updates"></a>Poser des questions, envoyer des commentaires, obtenir des mises à jour

Découvrez l’article [Communauté Azure Media Services](media-services-community.md) pour découvrir les différentes façons dont vous pouvez poser des questions, faire des commentaires et obtenir des mises à jour sur Media Services.

## <a name="next-steps"></a>Étapes suivantes

[Conseils de migration pour le passage de Media Services v2 à Media Services v3](migrate-from-v2-to-v3.md)
