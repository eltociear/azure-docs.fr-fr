---
title: 'Langage de requête Azure Cosmos DB : REPLICATE'
description: Découvrez la fonction système SQL REPLICATE dans Azure Cosmos DB.
author: ginamr
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 03/03/2020
ms.author: girobins
ms.custom: query-reference
ms.openlocfilehash: 19fcde522c5cb0355e53a5616145f27fada7dad9
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2020
ms.locfileid: "78302183"
---
# <a name="replicate-azure-cosmos-db"></a>REPLICATE (Azure Cosmos DB)
 Répète une valeur de chaîne un nombre spécifié de fois.
  
## <a name="syntax"></a>Syntaxe
  
```sql
REPLICATE(<str_expr>, <num_expr>)
```  
  
## <a name="arguments"></a>Arguments
  
*str_expr*  
   Est une expression de chaîne.
  
*num_expr*  
   Est une expression numérique. Si *num_expr* est négative ou non finie, le résultat est indéfini.
  
## <a name="return-types"></a>Types de retour
  
  Retourne une expression de chaîne.
  
## <a name="remarks"></a>Notes
  La longueur maximale du résultat est 10 000 caractères : (length(*str_expr*)  *  *num_expr*) <= 10 000.

## <a name="examples"></a>Exemples
  
  L’exemple suivant montre comment utiliser `REPLICATE` dans une requête.
  
```sql
SELECT REPLICATE("a", 3) AS replicate
```  
  
 Voici le jeu de résultats obtenu.
  
```json
[{"replicate": "aaa"}]
```  

## <a name="remarks"></a>Notes

Cette fonction système n’utilisera pas l’index.

## <a name="next-steps"></a>Étapes suivantes

- [Fonctions de chaîne Azure Cosmos DB](sql-query-string-functions.md)
- [Fonctions système Azure Cosmos DB](sql-query-system-functions.md)
- [Présentation d’Azure Cosmos DB](introduction.md)
