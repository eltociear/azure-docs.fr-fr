---
title: 'Ajouter des lignes : Informations de référence sur les modules'
titleSuffix: Azure Machine Learning
description: Découvrez comment utiliser le module Ajouter des lignes dans Azure Machine Learning pour concaténer deux jeux de données.
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: reference
author: likebupt
ms.author: keli19
ms.date: 02/22/2020
ms.openlocfilehash: cd9b5f8f182c4deab746d2c41e516a6ac23fb7aa
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2020
ms.locfileid: "79477729"
---
# <a name="add-rows-module"></a>Module Ajouter des lignes

Cet article décrit un module dans le concepteur Azure Machine Learning (version préliminaire).

Utilisez ce module pour concaténer 2 jeux de données. Dans la concaténation, les lignes du deuxième jeu de données sont ajoutées à la fin du premier jeu de données.  
  
La concaténation de lignes est utile dans des scénarios tels que les suivants :  
  
+ Vous avez généré une série de statistiques d’évaluation, et vous souhaitez les combiner dans une table pour simplifier la génération de rapports.  
  
+ Vous utilisez des jeux de données différents, et vous souhaitez combiner les jeux de données pour créer un jeu de données final.  

## <a name="how-to-use-add-rows"></a>Procédure d’utilisation de Ajouter des lignes  

Pour concaténer des lignes de deux jeux de données, les lignes doivent avoir exactement le même schéma. Cela signifie le même nombre de colonnes et le même type de données dans les colonnes.

1.  Faites glisser le module **Ajouter des lignes** dans votre pipeline (il se trouve sous **Transformation des données**).

2. Connectez les jeux de données aux deux ports d’entrée. Le jeu de données que vous souhaitez ajouter doit être connecté au deuxième port (droite). 
  
3.  Envoyez le pipeline. Le nombre de lignes dans le jeu de données de sortie doit être égal à la somme des lignes de deux jeux de données d’entrée.

    Si vous ajoutez le même jeu de données aux deux entrées du module **Ajouter des lignes**, le jeu de données est dupliqué. 

## <a name="next-steps"></a>Étapes suivantes

Consultez [l’ensemble des modules disponibles](module-reference.md) pour Azure Machine Learning. 