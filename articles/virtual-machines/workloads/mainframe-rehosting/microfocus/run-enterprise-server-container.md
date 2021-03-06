---
title: Exécuter Micro Focus Enterprise Server 4.0 dans un conteneur Docker sur des machines virtuelles Azure
description: Hébergez à nouveau vos charges de travail de mainframe IBM z/OS en exécutant Micro Focus Enterprise Server dans un conteneur Docker sur des machines virtuelles Azure.
services: virtual-machines-linux
documentationcenter: ''
author: njray
ms.author: sread
ms.date: 04/02/2019
ms.topic: article
ms.service: multiple
ms.openlocfilehash: 30d99c3f4767eb50361f7074c0d508fcf309faca
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2020
ms.locfileid: "61488336"
---
# <a name="run-micro-focus-enterprise-server-40-in-a-docker-container-on-azure"></a>Exécuter Micro Focus Enterprise Server 4.0 dans un conteneur Docker sur Azure

Vous pouvez exécuter Micro Focus Enterprise Server 4.0 dans un conteneur Docker sur Azure. Ce didacticiel vous explique les procédures. Il utilise la démonstration acctdemo CICS (Customer Information Control System) Windows pour Enterprise Server.

Docker ajoute la portabilité et l’isolation aux applications. Par exemple, vous pouvez exporter une image Docker d’une machine virtuelle Windows à s’exécuter sur une autre, ou d’un référentiel sur un serveur Windows avec Docker. L’image Docker s’exécute au nouvel emplacement avec la même configuration, sans devoir installer Enterprise Server. Il est inclus dans l’image. Les considérations relatives aux licences s’appliquent toujours.

Ce didacticiel installe la machine virtuelle **Windows 2016 Datacenter with Containers** à partir de la Place de marché Azure. Cette machine virtuelle inclut **Docker 18.09.0**. Les étapes ci-dessous vous montrent comment déployer le conteneur, l’exécuter, puis le connecter à un émulateur 3270.

## <a name="prerequisites"></a>Prérequis

Avant de commencer, consultez les prérequis suivants :

- Un abonnement Azure. Si vous n’en avez pas, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

- Le logiciel Micro Focus et une licence valide (ou licence d’essai). Si vous êtes déjà client de Micro Focus, contactez votre représentant Micro Focus. Sinon, [demandez une version d’évaluation](https://www.microfocus.com/products/enterprise-suite/enterprise-server/trial/).

     > [!NOTE]
     > Les fichiers de démonstration Docker sont inclus avec Enterprise Server 4.0. Ce didacticiel utilise ent\_server\_dockerfiles\_4.0\_windows.zip. Accédez-y du même endroit où vous avez accédé au fichier d’installation d’Enterprise Server, ou accédez à *Micro Focus* pour commencer.

- La documentation de [Enterprise Server and Enterprise Developer](https://www.microfocus.com/documentation/enterprise-developer/#").

## <a name="create-a-vm"></a>Créer une machine virtuelle

1. Sécurisez le média du fichier ent\_server\_dockerfiles\_4.0\_windows.zip. Sécurisez le fichier de licence ES-Docker-Prod-XXXXXXXX.mflic (nécessaire pour créer les images Docker).

2. Créez la machine virtuelle. Pour cela, ouvrez le Portail Azure, sélectionnez **Créer une ressource** en haut à gauche et filtrez par *serveur windows*. Dans les résultats, sélectionnez **Windows Server 2016 Datacenter – with Containers**.

     ![Résultats de la recherche du Portail Azure](media/01-portal.png)

3. Pour configurer les propriétés de la machine virtuelle, choisissez des détails d’instance :

    1. Choisissez une taille de machine virtuelle. Pour ce didacticiel, envisagez d’utiliser une machine virtuelle **Standard DS2\_v2** avec 2 processeurs virtuels et 7 Go de mémoire.

    2. Sélectionnez la **région** et le **groupe de ressources** sur lesquels vous souhaitez déployer.

    3. Pour les **options de disponibilité**, utilisez le paramètre par défaut.

    4. Pour le **nom d’utilisateur**, saisissez le compte administrateur que vous souhaitez utiliser et le mot de passe.

    5. Assurez-vous que le **port 3389 RDP** est ouvert. Seul ce port doit être exposé publiquement pour que vous puissiez vous connecter à la machine virtuelle. Acceptez ensuite toutes les valeurs par défaut, puis cliquez sur **Vérifier+créer**.

     ![Volet Créer une machine virtuelle](media/container-02.png)

4. Attendez que le déploiement se termine (quelques minutes). Un message indique que votre machine virtuelle a été créée.

5. Cliquez sur **Accéder à la ressource** pour accéder au panneau **Vue d’ensemble** de votre machine virtuelle.

6. Sur la droite, cliquez sur le bouton **Connecter** . Les options **Se connecter à la machine virtuelle** apparaissent à droite.

7. Cliquez sur le bouton **Téléchargement du fichier RDP** pour télécharger le fichier RDP qui vous permet d’être lié à la machine virtuelle.

8. Lorsque le téléchargement du fichier est terminé, ouvrez-le et saisissez le nom d’utilisateur et le mot de passe que vous avez créés pour la machine virtuelle.

     > [!NOTE]
     > N’utilisez pas vos informations d’identification d’entreprise pour vous connecter. (Le client RDP suppose que vous souhaitez les utiliser. Mais vous ne le voulez pas.)

9.  Sélectionnez **Autres choix**, puis sélectionnez les informations d’identification de votre machine virtuelle.

À ce stade, la machine virtuelle est en cours d’exécution et est jointe via RDP. Vous êtes connecté et prêt pour l’étape suivante.

## <a name="create-a-sandbox-directory-and-upload-the-zip-file"></a>Créer un répertoire de bac à sable et charger le fichier zip

1.  Créez un répertoire sur la machine virtuelle dans lequel vous pouvez télécharger les fichiers de démonstration et de licence. Par exemple, **C:\\Sandbox**.

2.  Chargez **ent\_server\_dockerfiles\_4.0\_windows.zip** et le fichier **ES-Docker-Prod-XXXXXXXX.mflic** dans le répertoire que vous avez créé.

3.  Extrayez le contenu du fichier zip dans le répertoire le **ent\_server\_dockerfiles\_4.0\_windows** créé par le processus d’extraction. Ce répertoire inclut un fichier readme (aux formats .html et .txt) et deux sous-répertoires, **EnterpriseServer** et **Examples**.

4.  Copiez le fichier **ES-Docker-Prod-XXXXXXXX.mflic** dans les répertoires C:\\Sandbox\\ent\_server\_dockerfiles\_4.0\_windows\\EnterpriseServer et C:\\Sandbox\\ent\_server\_dockerfiles\_4.0\_windows\\Examples\\CICS.

> [!NOTE]
> Assurez-vous de copier le fichier de licence dans les deux répertoires. Ils sont nécessaires dans l’étape de création Docker pour s’assurer que les images disposent des licences adéquates.

## <a name="check-docker-version-and-create-base-image"></a>Vérifier la version de Docker et créer l’image de base

> [!IMPORTANT]
> La création de l’image Docker appropriée est un processus en deux étapes. Créez tout d’abord l’image de base Enterprise Server 4.0. Puis créez une autre image pour la plateforme x64. Bien que vous puissiez créer une image x86 (32 bits), utilisez l’image 64 bits.

1. Ouvrez une invite de commandes.

2. Vérifiez que Docker est installé. À l’invite de commandes, tapez :

    ```
        docker version
    ```

     Par exemple, la version était 18.09.0 au moment de l’écriture.

3. Pour changer de répertoire, saisissez **cd \Sandbox\ent_server_dockerfiles_4.0_windows\EnterpriseServer**.

4. Saisissez **bld.bat IacceptEULA** pour commencer le processus de création de l’image de base initiale. Attendez quelques minutes pour que ce processus s’exécute. Dans les résultats, notez les deux images qui ont été créées : une pour x64 et l’autre pour x86 :

     ![Fenêtre Commande montrant les images](media/container-04.png)

5. Pour créer l’image finale pour la démonstration CICS, basculez vers le répertoire CICS en saisissant **cd\\Sandbox\\ent\_server\_dockerfiles\_4.0\_windows\\Examples\\CICS**.

6. Pour créer l’image, saisissez **bld.bat x64**. Attendez quelques minutes pour que le processus s’exécute et que le message indiquant que l’image a été créée s’affiche.

7. Saisissez **images docker** pour afficher une liste de toutes les images Docker installées sur la machine virtuelle. Assurez-vous que **microfocus/es-acctdemo** est l’une d’entre elles.

     ![Fenêtre Commande montrant l’image es-acctdemo](media/container-05.png)

## <a name="run-the-image"></a>Exécuter l’image 

1.  Pour lancer Enterprise Server 4.0 et l’application acctdemo, à l’invite de commandes, saisissez :

    ```
         docker run -p 16002:86/tcp -p 16002:86/udp -p 9040-9050:9040-9050 -p 9000-9010:9000-9010 -ti --network="nat" --rm microfocus/es-acctdemo:win_4.0_x64
    ```

2.  Installez un émulateur de terminal 3270 tel que [x3270](http://x3270.bgp.nu/) et utilisez-le pour vous lier, via le port 9040, à l’image est en cours d’exécution.

3.  Obtenez l’adresse IP du conteneur acctdemo, Docker peut donc agir comme un serveur DHCP pour les conteneurs qu’il gère :

    1.  Obtenez l’ID du conteneur en cours d’exécution. Saisissez **Docker ps** à l’invite de commandes et notez l’ID (**22a0fe3159d0** dans cet exemple). Notez-le pour l’étape suivante.

    2.  Pour obtenir l’adresse IP du conteneur acctdemo, utilisez l’ID de conteneur de l’étape précédente comme suit :

    ```
       docker inspect <containerID> --format="{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}"
    ```

       Par exemple :

    ```   
        docker inspect 22a0fe3159d0 --format="{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}"
    ```
4. Notez l’adresse IP de l’image acctdemo. Par exemple, l’adresse dans la sortie suivante est 172.19.202.52.

     ![Fenêtre Commande montrant l’adresse IP](media/container-06.png)

5. Montez l’image à l’aide de l’émulateur. Configurez l’émulateur pour utiliser l’adresse de l’image acctdemo et le port 9040. Il s’agit ici de **172.19.202.52:9040**. La vôtre sera similaire. L’écran **Signon to CICS** (Se connecter à CICS) s’ouvre.

    ![Écran de connexion à CICS](media/container-07.png)

6. Connectez-vous à la région CICS en entrant **SYSAD** pour **USERID** et **SYSAD** pour **Mot de passe**.

7. Effacez l’écran à l’aide du mappage de touches de l’émulateur. Pour x3270, sélectionnez l’option de menu **Keymap** (Mappage de touches).

8. Pour lancer l’application acctdemo, saisissez **ACCT**. L’écran initial de l’application s’affiche.

     ![Écran de démonstration de compte](media/container-08.png)

9. Faites des essais avec les types de compte d’affichage. Par exemple, saisissez **D** pour la requête et **11111** pour le **compte**. D’autres numéros de comptes à essayer sont 22222, 33333 et ainsi de suite.

     ![Écran de démonstration de compte](media/container-09.png)

10. Pour afficher la console d’administration d’Enterprise Server, accédez à l’invite de commandes et saisissez **start http:172.19.202.52:86**

     ![Console d’administration d’Enterprise Server](media/container-010.png)

Et voilà ! Vous exécutez et gérez maintenant une application CICS dans un conteneur Docker.

## <a name="next-steps"></a>Étapes suivantes

- [Installer Micro Focus Enterprise Server 4.0 et Enterprise Developer 4.0 sur Azure](./set-up-micro-focus-azure.md)
- [Migration d’applications mainframe](/azure/architecture/cloud-adoption/infrastructure/mainframe-migration/application-strategies)
