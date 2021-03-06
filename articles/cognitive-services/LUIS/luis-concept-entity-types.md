---
title: Types d’entités - LUIS
description: Une entité extrait des données d’un énoncé de l’utilisateur au moment de l’exécution de la prédiction. Un objectif secondaire _facultatif_ est d’améliorer la prédiction de l’intention ou d’autres entités à l’aide de l’entité en tant que caractéristique.
ms.topic: conceptual
ms.date: 04/30/2020
ms.openlocfilehash: 9d8afd5a660b3af5556256835486e984d7d657bc
ms.sourcegitcommit: bb0afd0df5563cc53f76a642fd8fc709e366568b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83585638"
---
# <a name="extract-data-with-entities"></a>Extraire des données avec des entités

Une entité extrait des données d’un énoncé de l’utilisateur au moment de l’exécution de la prédiction. Un objectif secondaire _facultatif_ est d’améliorer la prédiction de l’intention ou d’autres entités à l’aide de l’entité en tant que caractéristique.

Il existe plusieurs types d’entités .

* [Entité issue du Machine Learning](reference-entity-machine-learned-entity.md)
* Non issue du Machine Learning utilisée en tant que [fonctionnalité](luis-concept-feature.md) : requise pour les correspondances de texte exactes, les correspondances de modèle ou la détection par des entités prédéfinies
* [Pattern.any](#patternany-entity) : pour extraire du texte de forme libre tel que des titres de livres à partir d’un [modèle](reference-entity-pattern-any.md)

Les entités issues du Machine Learning fournissent la plus large gamme de choix d’extraction de données. Les entités qui ne sont pas issues du Machine Learning fonctionnent par correspondance de texte et sont utilisées en tant que [fonctionnalité requise](#design-entities-for-decomposition) pour une entité ou une intention issue du Machine Learning.

## <a name="entities-represent-data"></a>Les entités représentent les données

Les entités sont des données que vous souhaitez extraire de l’énoncé, telles que des noms, des dates, des noms de produit ou des groupes de mots significatifs. Un énoncé peut inclure plusieurs entités ou aucune. Une application cliente _peut_ avoir besoin des données pour accomplir sa tâche.

Les entités doivent être étiquetées de manière cohérente sur tous les énoncés d’entraînement pour chaque intention dans un modèle.

 Vous pouvez définir vos propres entités ou utiliser des entités prédéfinies afin de gagner du temps pour les concepts courants comme [datetimeV2](luis-reference-prebuilt-datetimev2.md), [ordinal](luis-reference-prebuilt-ordinal.md), [e-mail](luis-reference-prebuilt-email.md) et [numéro de téléphone](luis-reference-prebuilt-phonenumber.md).

|Énoncé|Entité|Données|
|--|--|--|
|Acheter 3 tickets pour New York|Nombre prédéfini<br>Destination|3<br>New York|


### <a name="entities-are-optional-but-recommended"></a>Les entités sont facultatives mais recommandées

Les [intentions](luis-concept-intent.md) sont requises mais les entités sont facultatives. Vous n’avez pas besoin de créer d’entités pour chaque concept dans votre application, mais uniquement pour celles où l’application cliente a besoin des données, ou l’entité agit comme un conseil ou un signal auprès d’une autre entité ou intention.

À mesure que votre application se développe et qu’un nouveau besoin de données est identifié, vous pouvez ajouter des entités appropriées à votre modèle LUIS par la suite.

## <a name="entity-compared-to-intent"></a>Comparaison entre entité et intention

L’entité représente un concept de données _à l’intérieur de l’énoncé_ que vous souhaitez extraire. Une intention classe _tout l’énoncé_.

Prenons les quatre énoncés suivants :

|Énoncé|Intention prédite|Entités extraites|Explication|
|--|--|--|--|
|Aide|help|-|Rien à extraire.|
|Envoyer quelque chose|sendSomething|-|Rien à extraire. Le modèle n’a pas de fonctionnalité requise pour extraire `something` dans ce contexte, et aucun destinataire n’est indiqué.|
|Envoyer un cadeau à Bob|sendSomething|`Bob`, `present`|Le modèle extrait `Bob` en ajoutant une fonctionnalité requise d’une entité `personName` prédéfinie. Une entité issue de machine learning a été utilisée pour extraire `present`.|
|Envoyer une boîte de chocolats à Bob|sendSomething|`Bob`, `box of chocolates`|Les deux éléments de données importants, `Bob` et la `box of chocolates`, ont été extraits par des entités.|

## <a name="design-entities-for-decomposition"></a>Concevez des entités pour la décomposition

Les entités issues du Machine Learning vous permettent de concevoir le schéma de votre application pour la décomposition, en divisant un long concept en sous-entités.

Concevoir pour la décomposition permet à LUIS de restituer un degré élevé de résolution des entités à votre application cliente. Cela permet à votre application cliente de se concentrer sur les règles métier et de confier la résolution des données à LUIS.

Une entité issue du Machine Learning est déclenchée en fonction du contexte appris par le biais d’exemples d’énoncés.

Les [**entités issues du Machine Learning**](tutorial-machine-learned-entity.md) constituent des extracteurs de niveau supérieur. Les sous-entités sont des entités enfants d’entités issues du Machine Learning.

<a name="composite-entity"></a>
<a name="list-entity"></a>
<a name="patternany-entity"></a>
<a name="prebuilt-entity"></a>
<a name="regular-expression-entity"></a>
<a name="simple-entity"></a>

## <a name="types-of-entities"></a>Types d’entités

Une sous-entité d’un parent doit être une entité issue du Machine Learning. La sous-entité peut utiliser une entité non issue du Machine Learning comme [fonctionnalité](luis-concept-feature.md).

Choisissez l’entité en fonction de la façon dont les données doivent être extraites et être représentées une fois extraites.

|Type d'entité|Objectif|
|--|--|
|[**Issue de l’apprentissage automatique**](tutorial-machine-learned-entity.md)|Extrayez les données imbriquées et complexes tirées des exemples étiquetés. |
|[**Liste**](reference-entity-list.md)|Liste d’éléments et de leurs synonymes extraits avec une **correspondance exacte du texte**.|
|[**Pattern.any**](#patternany-entity)|Entité dans laquelle la détermination de la fin de l’entité est difficile à déterminer parce que l’entité est de forme libre. Disponible uniquement dans les [modèles](luis-concept-patterns.md).|
|[**Prédéfinie**](luis-reference-prebuilt-entities.md)|Déjà entraînée à extraire un type spécifique de données comme une URL ou un e-mail. Certaines de ces entités prédéfinies dans le projet open source [Recognizers-Text](https://github.com/Microsoft/Recognizers-Text). Si votre culture ou entité spécifique n’est pas encore prise en charge, vous pouvez contribuer au projet.|
|[**Expression régulière**](reference-entity-regular-expression.md)|Utilise l’expression régulière pour une **correspondance exacte du texte**.|

## <a name="extracting-contextually-related-data"></a>Extraction de données relatives au contexte

Un énoncé peut contenir au moins deux occurrences d’une entité où la signification des données est basée sur le contexte dans l’énoncé. Par exemple, un énoncé pour la réservation d’un vol a deux localisations géographiques : l’origine et la destination.

`Book a flight from Seattle to Cairo`

Les deux localisations doivent être extraites de manière à ce que l’application cliente sache le type de chaque localisation, pour mener l’achat du billet.

Pour extraire l’origine et la destination, créez deux sous-entités dans le cadre de l’entité « billet » issue du Machine Learning. Pour chacune des sous-entités, créez une fonctionnalité requise qui utilise geographyV2.

<a name="using-component-constraints-to-help-define-entity"></a>
<a name="using-subentity-constraints-to-help-define-entity"></a>

### <a name="using-required-features-to-constrain-entities"></a>Utilisation des fonctionnalités requises pour contraindre les entités

En savoir plus sur les [fonctionnalités requises](luis-concept-feature.md)

## <a name="patternany-entity"></a>Entité Pattern.any

Une entité Pattern.any est uniquement disponible dans un [modèle](luis-concept-patterns.md).

<a name="if-you-need-more-than-the-maximum-number-of-entities"></a>
## <a name="exceeding-app-limits-for-entities"></a>Dépassement des limites d’application pour les entités

Si vous devez dépasser la [limite](luis-limits.md#model-limits), contactez le support. Pour cela, rassemblez des informations détaillées sur votre système, accédez au site web [LUIS](luis-reference-regions.md#luis-website), puis sélectionnez **Support**. Si votre abonnement Azure comprend des services de support, contactez le [support technique Azure](https://azure.microsoft.com/support/options/).

## <a name="entity-prediction-status"></a>État de prédiction d’entité

Le portail LUIS indique quand l’entité a une prédiction d’entité différente de celle de l’entité que vous avez sélectionnée dans un exemple d’énoncé. Ce score différent est basé sur le modèle entraîné actuel. Utilisez ces informations pour résoudre les erreurs d’apprentissage à l’aide d’un ou plusieurs des éléments suivants :
* Créez une [fonctionnalité](luis-concept-feature.md) pour l’entité afin d’identifier le concept de l’entité.
* Ajoutez des [exemples d’énoncés](luis-concept-utterance.md) et étiquetez-les avec l’entité.
* [Passez en revue les suggestions d’apprentissage actif](luis-concept-review-endpoint-utterances.md) pour les énoncés reçus au point de terminaison de prédiction qui peuvent aider à identifier le concept de l’entité.

## <a name="next-steps"></a>Étapes suivantes

Découvrez les concepts relatifs aux bons [énoncés](luis-concept-utterance.md).

Consulter [Ajouter des entités](luis-how-to-add-entities.md) pour découvrir comment ajouter des entités à votre application LUIS.

Voir le [tutoriel : Extraire des données structurées à partir d’un énoncé utilisateur avec des entités issues du Machine Learning dans LUIS](tutorial-machine-learned-entity.md) pour apprendre à extraire des données structurées d’un énoncé à l’aide de l’entité issue de machine learning.

