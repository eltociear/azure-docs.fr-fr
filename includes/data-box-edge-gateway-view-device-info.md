---
author: alkohli
ms.service: databox
ms.topic: include
ms.date: 03/04/2019
ms.author: alkohli
ms.openlocfilehash: 94c132421f1e113b667341b094acad8047e5f465
ms.sourcegitcommit: 856db17a4209927812bcbf30a66b14ee7c1ac777
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2020
ms.locfileid: "82561762"
---
1. [Connectez-vous à l’interface PowerShell](#connect-to-the-powershell-interface).
2. Utilisez `Get-HcsApplianceInfo` pour obtenir les informations pour votre appareil.

    L’exemple suivant montre comment utiliser cette cmdlet :

    ```
    [10.100.10.10]: PS>Get-HcsApplianceInfo
    
    Id                            : b2044bdb-56fd-4561-a90b-407b2a67bdfc
    FriendlyName                  : DBE-NBSVFQR94S6
    Name                          : DBE-NBSVFQR94S6
    SerialNumber                  : HCS-NBSVFQR94S6
    DeviceId                      : 40d7288d-cd28-481d-a1ea-87ba9e71ca6b
    Model                         : Virtual
    FriendlySoftwareVersion       : Data Box Gateway 1902
    HcsVersion                    : 1.4.771.324
    IsClustered                   : False
    IsVirtual                     : True
    LocalCapacityInMb             : 1964992
    SystemState                   : Initialized
    SystemStatus                  : Normal
    Type                          : DataBoxGateway
    CloudReadRateBytesPerSec      : 0
    CloudWriteRateBytesPerSec     : 0
    IsInitialPasswordSet          : True
    FriendlySoftwareVersionNumber : 1902
    UploadPolicy                  : All
    DataDiskResiliencySettingName : Simple
    ApplianceTypeFriendlyName     : Data Box Gateway
    IsRegistered                  : False
    ```

    Voici un tableau récapitulant les informations importantes sur les appareils :
    
    | Paramètre                             | Description                                                                                                                                                  |   |
    |--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|---|
    | FriendlyName                   | Nom convivial configuré pour l’appareil via l’interface utilisateur web locale lors du déploiement de l’appareil. Le nom convivial par défaut est le numéro de série de l’appareil.  |   |
    | SerialNumber                   | Le numéro de série de l’appareil est un numéro unique attribué en usine.                                                                             |   |
    | Modèle                          | Le modèle de votre appareil Azure Stack Edge ou Data Box Gateway. Le modèle est physique pour Azure Stack Edge et virtuel pour Data Box Gateway.                   |   |
    | FriendlySoftwareVersion        | Chaîne conviviale qui correspond à la version du logiciel de l’appareil. Pour un système exécutant la préversion, la version conviviale du logiciel serait Data Box Edge 1902. |   |
    | HcsVersion                     | Version du logiciel HCS exécutée sur votre appareil. Par exemple, la version du logiciel HCS correspondant à Data Box Edge 1902 est 1.4.771.324.            |   |
    | LocalCapacityInMb              | Capacité totale locale de l’appareil en mégabits.                                                                                                        |   |
    | IsRegistered                   | Cette valeur indique si votre appareil est activé avec le service.                                                                                         |   |


