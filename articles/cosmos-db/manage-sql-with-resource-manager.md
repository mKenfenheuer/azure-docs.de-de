---
title: Erstellen und Verwalten von Azure Cosmos DB mit Resource Manager-Vorlagen
description: Verwenden von Azure Resource Manager-Vorlagen zum Erstellen und Konfigurieren der Core-API (SQL) von Azure Cosmos DB
author: markjbrown
ms.service: cosmos-db
ms.topic: how-to
ms.date: 06/19/2020
ms.author: mjbrown
ms.openlocfilehash: 2b4a572abec8007fe6f1c7e963be19d28c7b48d6
ms.sourcegitcommit: 0100d26b1cac3e55016724c30d59408ee052a9ab
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/07/2020
ms.locfileid: "86028154"
---
# <a name="manage-azure-cosmos-db-core-sql-api-resources-with-azure-resource-manager-templates"></a>Verwalten von Ressourcen für die Core-API (SQL) von Azure Cosmos DB mit Azure Resource Manager-Vorlagen

In diesem Artikel erfahren Sie, wie Sie Ihre Azure Cosmos DB-Konten, -Datenbanken und -Container mithilfe von Azure Resource Manager-Vorlagen bereitstellen und verwalten.

Dieser Artikel enthält nur Azure Resource Manager-Vorlagenbeispiele für Core-API-Konten (SQL). Es gibt jedoch auch Vorlagenbeispiele für [Cassandra-](manage-cassandra-with-resource-manager.md)-, [Gremlin](manage-gremlin-with-resource-manager.md)-, [MongoDB](manage-mongodb-with-resource-manager.md)- und [Table](manage-table-with-resource-manager.md)-APIs.

> [!IMPORTANT]
>
> * Die Länge von Kontonamen ist auf 44 Zeichen (ausschließlich Kleinbuchstaben) beschränkt.
> * Sie müssen die Vorlage mit aktualisierter Angabe der RU/s erneut bereitstellen, um die Durchsatzwerte ändern zu können.
> * Wenn Sie einem Azure Cosmos-Konto Speicherorte hinzufügen oder aus ihm entfernen, können Sie nicht gleichzeitig andere Eigenschaften ändern. Diese Vorgänge müssen separat ausgeführt werden.

Wenn Sie eine der unten aufgeführten Azure Cosmos DB-Ressourcen erstellen möchten, kopieren Sie die folgende Beispielvorlage in eine neue JSON-Datei. Optional können Sie eine JSON-Parameterdatei erstellen, die beim Bereitstellen mehrerer Instanzen derselben Ressource mit unterschiedlichen Namen und Werten verwendet werden soll. Für das Bereitstellen von Azure Resource Manager-Vorlagen stehen Ihnen viele Möglichkeiten zur Verfügung, beispielsweise das [Azure-Portal](../azure-resource-manager/templates/deploy-portal.md), die [Azure CLI](../azure-resource-manager/templates/deploy-cli.md), [Azure PowerShell](../azure-resource-manager/templates/deploy-powershell.md) und [GitHub](../azure-resource-manager/templates/deploy-to-azure-button.md).

<a id="create-autoscale"></a>

## <a name="azure-cosmos-account-with-autoscale-throughput"></a>Azure Cosmos-Konto mit automatisch skaliertem Durchsatz

Mit dieser Vorlage wird ein Azure Cosmos-Konto in zwei Regionen mit Optionen für Konsistenz und Failover erstellt, wobei Datenbank und Container für den automatisch skalierten Durchsatz konfiguriert sind, für den die meisten Richtlinienoptionen aktiviert sind. Diese Vorlage ist auch für die Bereitstellung mit nur einem Klick im Katalog der Azure-Schnellstartvorlagen verfügbar.

[:::image type="content" source="../media/template-deployments/deploy-to-azure.svg" alt-text="Bereitstellen in Azure":::](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-cosmosdb-sql-autoscale%2Fazuredeploy.json)

:::code language="json" source="~/quickstart-templates/101-cosmosdb-sql-autoscale/azuredeploy.json":::

<a id="create-analytical-store"></a>

## <a name="azure-cosmos-account-with-analytical-store"></a>Azure Cosmos-Konto mit Analysespeicher

Mit dieser Vorlage wird ein Azure Cosmos-Konto in einer Region mit einem Container mit aktivierter analytischer Gültigkeitsdauer und Optionen für die manuelle oder automatische Skalierung des Durchsatzes erstellt. Diese Vorlage ist auch für die Bereitstellung mit nur einem Klick im Katalog der Azure-Schnellstartvorlagen verfügbar.

[:::image type="content" source="../media/template-deployments/deploy-to-azure.svg" alt-text="Bereitstellen in Azure":::](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-cosmosdb-sql-analytical-store%2Fazuredeploy.json)

:::code language="json" source="~/quickstart-templates/101-cosmosdb-sql-analytical-store/azuredeploy.json":::

<a id="create-manual"></a>

## <a name="azure-cosmos-account-with-standard-provisioned-throughput"></a>Azure Cosmos-Konto mit standardmäßig bereitgestelltem Durchsatz

Mit dieser Vorlage wird ein Azure Cosmos-Konto in zwei Regionen mit Optionen für Konsistenz und Failover erstellt, wobei Datenbank und Container für den Standarddurchsatz konfiguriert sind, für den die meisten Richtlinienoptionen aktiviert sind. Diese Vorlage ist auch für die Bereitstellung mit nur einem Klick im Katalog der Azure-Schnellstartvorlagen verfügbar.

[:::image type="content" source="../media/template-deployments/deploy-to-azure.svg" alt-text="Bereitstellen in Azure":::](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-cosmosdb-sql%2Fazuredeploy.json)

:::code language="json" source="~/quickstart-templates/101-cosmosdb-sql/azuredeploy.json":::

<a id="create-sproc"></a>

## <a name="azure-cosmos-db-container-with-server-side-functionality"></a>Azure Cosmos DB-Container mit serverseitiger Funktionalität

Mit dieser Vorlage werden ein Azure Cosmos-Konto, eine Datenbank und ein Container mit einer gespeicherten Prozedur, einem Trigger und einer benutzerdefinierten Funktion erstellt. Diese Vorlage ist auch für die Bereitstellung mit nur einem Klick im Katalog der Azure-Schnellstartvorlagen verfügbar.

[:::image type="content" source="../media/template-deployments/deploy-to-azure.svg" alt-text="Bereitstellen in Azure":::](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-cosmosdb-sql-container-sprocs%2Fazuredeploy.json)

:::code language="json" source="~/quickstart-templates/101-cosmosdb-sql-container-sprocs/azuredeploy.json":::

<a id="free-tier"></a>

## <a name="free-tier-azure-cosmos-db-account"></a>Azure Cosmos DB-Konto im Free-Tarif

Mit dieser Vorlage werden ein Azure Cosmos-Konto im Free-Tarif und eine Datenbank mit gemeinsam genutztem Durchsatz erstellt, der von bis zu 25 Containern gemeinsam genutzt werden kann. Diese Vorlage ist auch für die Bereitstellung mit nur einem Klick im Katalog der Azure-Schnellstartvorlagen verfügbar.

[:::image type="content" source="../media/template-deployments/deploy-to-azure.svg" alt-text="Bereitstellen in Azure":::](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-cosmosdb-free%2Fazuredeploy.json)

:::code language="json" source="~/quickstart-templates/101-cosmosdb-free/azuredeploy.json":::

## <a name="next-steps"></a>Nächste Schritte

Hier sind einige zusätzlichen Ressourcen:

* [Dokumentation zu Azure Resource Manager](/azure/azure-resource-manager/)
* [Schema von Azure Cosmos DB-Ressourcenanbietern](/azure/templates/microsoft.documentdb/allversions)
* [Schnellstartvorlagen für Azure Cosmos DB](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Documentdb&pageNumber=1&sort=Popular)
* [Beheben gängiger Azure-Bereitstellungsfehler mit Azure Resource Manager](../azure-resource-manager/templates/common-deployment-errors.md)
