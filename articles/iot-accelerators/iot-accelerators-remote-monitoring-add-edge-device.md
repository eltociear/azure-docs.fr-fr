---
title: Ajouter un appareil Edge à la solution de supervision à distance - Azure | Microsoft Docs
description: Cet article décrit comment ajouter un appareil IoT Edge à un accélérateur de solution de supervision à distance
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 10/09/2018
ms.topic: conceptual
ms.openlocfilehash: 0a42763ff47cccfa506acbbbd95d20d41eb0827f
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2020
ms.locfileid: "72965371"
---
# <a name="add-an-iot-edge-device-to-your-remote-monitoring-solution-accelerator"></a>Ajouter un appareil IoT Edge à votre accélérateur de solution de supervision à distance

Pour ajouter un appareil [IoT Edge](../iot-edge/about-iot-edge.md) à votre accélérateur de solution, effectuez les deux étapes suivantes :

1. Ajoutez l’appareil Edge dans la page **Explorateur d’appareils** de l’interface utilisateur web de l’accélérateur de solution de supervision à distance.
1. Installez le runtime IoT Edge sur votre appareil Edge.

## <a name="add-the-iot-edge-device"></a>Ajouter l’appareil IoT Edge

Pour ajouter un appareil IoT Edge à l’accélérateur de solution de supervision à distance, accédez à la page **Device Explorer** dans l’interface utilisateur web, puis cliquez sur **+ Nouvel appareil**.

Dans le panneau **Nouvel appareil**, choisissez **Appareil IoT Edge**. Vous pouvez conserver les valeurs par défaut des autres paramètres. Cliquez alors sur **Appliquer** :

![Ajouter un appareil IoT Edge](media/iot-accelerators-remote-monitoring-add-edge-device/addedgedevice.png)

### <a name="alternative-ways-to-add-an-iot-edge-device"></a>Autres manières d’ajouter un appareil IoT Edge

Il est également possible d’inscrire un appareil IoT Edge directement auprès de l’instance IoT Hub dans votre accélérateur de solution. Vous devez connaître le nom du hub IoT dans votre accélérateur de solution avant de suivre l’un de ces guides pratiques :

- [Inscrire un nouvel appareil Azure IoT Edge à partir du portail Azure](../iot-edge/how-to-register-device.md#register-in-the-azure-portal)
- [Inscrire un nouvel appareil Azure IoT Edge avec Azure CLI](../iot-edge/how-to-register-device.md#register-with-the-azure-cli)
- [Inscrire un nouvel appareil Azure IoT Edge à partir de Visual Studio Code](../iot-edge/how-to-register-device.md#register-with-visual-studio-code)

Quand vous inscrivez un appareil directement auprès du hub IoT dans l’accélérateur de solution de supervision à distance, l’appareil est listé dans la page **Explorateur d’appareils** de l’interface utilisateur web.

## <a name="install-the-iot-edge-runtime"></a>Installer le runtime IoT Edge

Avant de pouvoir déployer des modules sur votre appareil Edge, vous devez installer le runtime IoT Edge sur l’appareil réel. Les guides pratiques suivants vous montrent comment installer le runtime sur les plateformes d’appareils courantes :

- [Installer le runtime Azure IoT Edge sur Linux (x64)](../iot-edge/how-to-install-iot-edge-linux.md)
- [Installer le runtime Azure IoT Edge sur Linux (ARM32v7/armhf)](../iot-edge/how-to-install-iot-edge-linux-arm.md)
- [Installer le runtime Azure IoT Edge sur Windows pour l’utiliser avec des conteneurs Windows](../iot-edge/how-to-install-iot-edge-windows-with-windows.md)
- [Installer le runtime Azure IoT Edge sur Windows pour l’utiliser avec des conteneurs Linux](../iot-edge/how-to-install-iot-edge-windows-with-linux.md)
- [Installer le runtime IoT Edge sur Windows IoT Standard](../iot-edge/how-to-install-iot-core.md)

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez préparé votre appareil IoT Edge, l’étape suivante consiste à déployer des modules sur celui-ci. Consultez [Importer un package IoT Edge dans votre accélérateur de solution de supervision à distance](iot-accelerators-remote-monitoring-import-edge-package.md)
