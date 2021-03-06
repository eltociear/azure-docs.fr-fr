---
title: Liaisons Azure Cosmos DB pour Azure Functions 2.x
description: Découvrez comment utiliser des déclencheurs et liaisons Azure Cosmos DB dans Azure Functions.
author: craigshoemaker
ms.topic: reference
ms.date: 02/24/2017
ms.author: cshoe
ms.openlocfilehash: f258a7aff52796a53540706bc8413575d63c9e7d
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2020
ms.locfileid: "77605757"
---
# <a name="azure-cosmos-db-trigger-and-bindings-for-azure-functions-2x-overview"></a>Présentation du déclencheur et des liaisons Azure Cosmos DB pour Azure Functions 2.x

> [!div class="op_single_selector" title1="Sélectionnez la version du runtime Azure Functions que vous utilisez : "]
> * [Version 1](functions-bindings-cosmosdb.md)
> * [Version 2](functions-bindings-cosmosdb-v2.md)

Cet ensemble d’articles explique comment utiliser des liaisons [Azure Cosmos DB](../cosmos-db/serverless-computing-database.md) dans Azure Functions 2.x. Azure Functions prend en charge les liaisons de déclencheur, d’entrée et de sortie pour Azure Cosmos DB.

| Action | Type |
|---------|---------|
| Exécuter une fonction lors de la création ou de la modification d’un document Azure Cosmos DB | [Déclencheur](./functions-bindings-cosmosdb-v2-trigger.md) |
| Lire un document Azure Cosmos DB | [Liaison d’entrée](./functions-bindings-cosmosdb-v2-input.md) |
| Enregistrer les modifications apportées à un document Azure Cosmos DB  |[Liaison de sortie](./functions-bindings-cosmosdb-v2-output.md) |

> [!NOTE]
> Cette référence concerne [Azure Functions version 2.x](functions-versions.md).  Pour plus d’informations sur l’utilisation de ces liaisons dans Functions 1.x, consultez [Liaisons Azure Cosmos DB pour Azure Functions 1.x](functions-bindings-cosmosdb.md).
>
> Cette liaison était nommée à l’origine DocumentDB. Dans Functions version 2.x, le déclencheur, les liaisons et le package sont tous renommés Cosmos DB.

## <a name="supported-apis"></a>API prises en charge

[!INCLUDE [SQL API support only](../../includes/functions-cosmosdb-sqlapi-note.md)]

## <a name="add-to-your-functions-app"></a>Ajouter à votre application de fonction

### <a name="functions-2x-and-higher"></a>Functions 2.x et versions ultérieures

Pour utiliser le déclencheur et les liaisons, vous devez référencer le package approprié. Le package NuGet est utilisé pour les bibliothèques de classes .NET, tandis que le bundle d’extensions est utilisé pour tous les autres types d’applications.

| Langage                                        | Ajouter via...                                   | Notes 
|-------------------------------------------------|---------------------------------------------|-------------|
| C#                                              | L’installation du [package NuGet], version 3.x | |
| Script C#, Java, JavaScript, Python, PowerShell | L’inscription du [bundle d’extensions]          | Il est recommandé d’utiliser l’[extension Azure Tools] avec Visual Studio Code. |
| Script C# (en ligne uniquement dans le portail Azure)         | Ajout d’une liaison                            | Pour mettre à jour des extensions de liaison existantes sans avoir à republier votre application de fonction, voir [Mettre à jour vos extensions]. |

[Package NuGet]: https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.CosmosDB
[core tools]: ./functions-run-local.md
[Bundle d’extensions]: ./functions-bindings-register.md#extension-bundles
[Mettre à jour vos extensions]: ./install-update-binding-extensions-manual.md
[Extension Azure Tools]: https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack

### <a name="functions-1x"></a>Functions 1.x

Les applications Functions 1.x ont automatiquement une référence au package NuGet [Microsoft.Azure.WebJobs](https://www.nuget.org/packages/Microsoft.Azure.WebJobs), version 2.x.

## <a name="next-steps"></a>Étapes suivantes

- [Exécuter une fonction lors de la création ou de la modification d'un document Azure Cosmos DB (Déclencheur)](./functions-bindings-cosmosdb-v2-trigger.md)
- [Lire un document Azure Cosmos DB (liaison d’entrée)](./functions-bindings-cosmosdb-v2-input.md)
- [Enregistrer les modifications apportées à un document Azure Cosmos DB (liaison de sortie)](./functions-bindings-cosmosdb-v2-output.md)
