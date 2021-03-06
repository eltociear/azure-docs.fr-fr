---
title: Machine Learning et IA avec ONNX dans Azure SQL Edge (préversion)
description: Dans Azure SQL Edge (préversion), l’apprentissage automatique prend en charge les modèles au format ONNX (Open Neural Network Exchange). ONNX est un format ouvert que vous pouvez utiliser pour échanger des modèles entre plusieurs infrastructures et outils de Machine Learning.
keywords: déployer SQL Edge
services: sql-database-edge
ms.service: sql-database-edge
ms.subservice: ''
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.date: 05/19/2020
ms.openlocfilehash: 12c1294a804c2063d405c5ec08440865283d51d3
ms.sourcegitcommit: bb0afd0df5563cc53f76a642fd8fc709e366568b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83594588"
---
# <a name="machine-learning-and-ai-with-onnx-in-sql-edge-preview"></a>Machine Learning et intelligence artificielle avec ONNX dans SQL Edge (préversion)

Dans Azure SQL Edge (préversion), l’apprentissage automatique prend en charge les modèles au format [ONNX (Open Neural Network Exchange)](https://onnx.ai/). ONNX est un format ouvert que vous pouvez utiliser pour échanger des modèles entre plusieurs [infrastructures et outils de Machine Learning](https://onnx.ai/supported-tools).

## <a name="overview"></a>Vue d’ensemble

Pour inférer des modèles d’apprentissage automatique dans Azure SQL Edge, vous devez d’abord obtenir un modèle. Il peut s’agir d’un modèle prééntraîné ou d’un modèle personnalisé entraîné avec le framework de votre choix. Azure SQL Edge prend en charge le format ONNX et vous devrez convertir le modèle dans ce format. Il ne doit normalement y avoir aucun impact sur la justesse du modèle et, une fois que vous disposez du modèle ONNX, vous pouvez le déployer dans Azure SQL Edge et utiliser le [scoring natif avec la fonction T-SQL PREDICT](/sql/advanced-analytics/sql-native-scoring/).

## <a name="get-onnx-models"></a>Obtenir des modèles ONNX

Pour obtenir un modèle au format ONNX :

- **Services de génération de modèles** : les services comme la [fonctionnalité de Machine Learning automatisé dans Azure Machine Learning](https://github.com/Azure/MachineLearningNotebooks/blob/master/how-to-use-azureml/automated-machine-learning/classification-bank-marketing-all-features/auto-ml-classification-bank-marketing-all-features.ipynb) et le [service Azure Custom Vision](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/getting-started-build-a-classifier) prennent en charge l’exportation directe du modèle entraîné dans le format ONNX.

- [**Convertir et/ou exporter des modèles existants**](https://github.com/onnx/tutorials#converting-to-onnx-format) : plusieurs infrastructures d’entraînement (par ex., [PyTorch](https://pytorch.org/docs/stable/onnx.html), Chainer et Caffe2) prennent en charge la fonctionnalité d’exportation native vers ONNX, ce qui vous permet d’enregistrer votre modèle entraîné dans une version spécifique du format ONNX. Pour les infrastructures qui ne prennent pas en charge l’exportation native, il existe des packages autonomes de conversion ONNX installables qui vous permettent de convertir au format ONNX des modèles entraînés à partir de différentes infrastructures de Machine Learning.

     **Infrastructures prises en charge**
   * [PyTorch](http://pytorch.org/docs/master/onnx.html)
   * [Tensorflow](https://github.com/onnx/tensorflow-onnx)
   * [Keras](https://github.com/onnx/keras-onnx)
   * [Scikit-learn](https://github.com/onnx/sklearn-onnx)
   * [CoreML](https://github.com/onnx/onnxmltools)
    
    Pour obtenir la liste complète des infrastructures prises en charge ainsi que des exemples, consultez [Conversion au format ONNX](https://github.com/onnx/tutorials#converting-to-onnx-format).

## <a name="limitations"></a>Limites

Actuellement, tous les modèles ONNX ne sont pas pris en charge par Azure SQL Edge. La prise en charge est limitée aux modèles avec des **types de données numériques** :

- [int et bigint](https://docs.microsoft.com/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)
- [real et float](https://docs.microsoft.com/sql/t-sql/data-types/float-and-real-transact-sql)
  
Les autres types numériques peuvent être convertis vers des types pris en charge avec [CAST et CONVERT](https://docs.microsoft.com/sql/t-sql/functions/cast-and-convert-transact-sql).

Les entrées de modèle doivent être structurées afin que chaque entrée du modèle corresponde à une colonne unique dans une table. Par exemple, si vous utilisez un dataframe pandas pour former un modèle, chaque entrée doit correspondre à une colonne distincte du modèle.

## <a name="next-steps"></a>Étapes suivantes

- [Déployer SQL Edge via le portail Azure](deploy-portal.md)
- [Déployer un modèle ONNX sur Azure SQL Edge (préversion) ](deploy-onnx.md)
