---
title: Datenzugriffsstrategien
description: Azure Data Factory unterstützt jetzt statische IP-Adressbereiche.
services: data-factory
ms.author: abnarain
author: nabhishek
ms.service: data-factory
ms.workload: data-services
ms.topic: conceptual
ms.date: 05/28/2020
ms.openlocfilehash: 76181f089511a6645a51707f9a8537c1589d82bf
ms.sourcegitcommit: de2750163a601aae0c28506ba32be067e0068c0c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2020
ms.locfileid: "89484951"
---
# <a name="data-access-strategies"></a>Datenzugriffsstrategien

[!INCLUDE[appliesto-adf-asa-md](includes/appliesto-adf-asa-md.md)]

Ein wichtiges Sicherheitsziel einer Organisation besteht darin, ihre Datenspeicher vor zufälligem Zugriff über das Internet zu schützen – unabhängig davon, ob es sich um einen lokalen oder einen Cloud-/SaaS-Datenspeicher handelt. 

Normalerweise steuert ein Clouddatenspeicher den Zugriff mithilfe der folgenden Mechanismen:
* Privater Link aus einem virtuellen Netzwerk zu Datenquellen, die für den privaten Endpunkt aktiviert sind
* Firewallregeln, die die Konnektivität nach IP-Adresse einschränken
* Authentifizierungsmechanismen, bei denen Benutzer ihre Identität nachweisen müssen
* Autorisierungsmechanismen, die Benutzer auf bestimmte Aktionen und Daten einschränken

> [!TIP]
> Mit der [Einführung des statischen IP-Adressbereichs](https://docs.microsoft.com/azure/data-factory/azure-integration-runtime-ip-addresses) können Sie jetzt Listen-IP-Adressbereiche für die jeweilige Azure Integration Runtime-Region zulassen, um sicherzustellen, dass Sie in Ihren Clouddatenspeichern nicht alle Azure-IP-Adressen zulassen müssen. Auf diese Weise können Sie die IP-Adressen einschränken, denen der Zugriff auf die Datenspeicher gestattet wird.

> [!NOTE] 
> Die IP-Adressbereiche sind für Azure Integration Runtime gesperrt und werden derzeit nur für Datenverschiebungs-, Pipeline- und externe Aktivitäten verwendet. Dataflows und Azure Integration Runtimes, die ein verwaltetes virtuelles Netzwerk aktivieren, verwenden diese IP-Adressbereiche derzeit nicht. 

Dies sollte in vielen Szenarien funktionieren, und wir verstehen, dass eine eindeutige statische IP-Adresse pro Integration Runtime wünschenswert wäre. Dies wäre aber bei der derzeitigen Verwendung von Azure Integration Runtime nicht möglich, weil es serverlos ist. Bei Bedarf können Sie eine selbstgehostete Integration Runtime jederzeit einrichten und dabei Ihre statische IP-Adresse verwenden. 

## <a name="data-access-strategies-through-azure-data-factory"></a>Datenzugriffsstrategien für Azure Data Factory

* **[Private Link](https://docs.microsoft.com/azure/private-link/private-link-overview)** : Sie können eine Azure Integration Runtime in einem verwalteten virtuellen Azure Data Factory-Netzwerk erstellen. Diese nutzt private Endpunkte, um eine sichere Verbindung mit unterstützten Datenspeichern herzustellen. Der Datenverkehr zwischen dem verwalteten virtuellen Netzwerk und den Datenquellen wird über das Microsoft-Backbonenetzwerk übertragen und nicht für das öffentliche Netzwerk verfügbar gemacht.
* **[Vertrauenswürdiger Dienst](https://docs.microsoft.com/azure/storage/common/storage-network-security#exceptions)** – Azure Storage (Blob, ADLS Gen2) unterstützt die Firewallkonfiguration, die ausgewählten vertrauenswürdigen Azure-Plattformdiensten einen sicheren Zugriff auf das Speicherkonto ermöglicht. Vertrauenswürdige Dienste erzwingen die Authentifizierung der verwalteten Identität. Dadurch wird sichergestellt, dass keine andere Data Factory eine Verbindung mit diesem Speicher herstellen kann – außer wenn die Whitelist den Vermerk enthält, dass dies mithilfe von dessen verwalteter Identität möglich ist. Weitere Informationen finden Sie in **[diesem Blog](https://techcommunity.microsoft.com/t5/azure-data-factory/data-factory-is-now-a-trusted-service-in-azure-storage-and-azure/ba-p/964993)** . Deshalb ist dies extrem sicher und empfehlenswert. 
* **Eindeutige statische IP-Adresse** – Sie müssen eine selbstgehostete Integration Runtime einrichten, um eine statische IP-Adresse für Data Factory-Connectors zu erhalten. Durch diesen Mechanismus wird sichergestellt, dass Sie den Zugriff von allen anderen IP-Adressen blockieren können. 
* **[Statischer IP-Adressbereich](https://docs.microsoft.com/azure/data-factory/azure-integration-runtime-ip-addresses)** – Sie können die IP-Adressen der Azure Integration Runtime verwenden, um deren Auflistung in Ihrem Speicher (z B. S3, Salesforce usw.) zuzulassen. Er schränkt IP-Adressen, die eine Verbindung mit den Datenspeichern herstellen können, sicherlich ein, basiert aber auch auf Authentifizierungs-/Autorisierungsregeln.
* **[Diensttag](https://docs.microsoft.com/azure/virtual-network/service-tags-overview)** – Ein Diensttag stellt eine Gruppe von IP-Adresspräfixen eines bestimmten Azure-Diensts (wie Azure Data Factory) dar. Microsoft verwaltet die Adresspräfixe, für die das Diensttag gilt, und aktualisiert das Tag automatisch, wenn sich die Adressen ändern. Auf diese Weise wird die Komplexität häufiger Updates an Netzwerksicherheitsregeln minimiert. Dies ist nützlich beim Whitelisting des Datenzugriffs auf in IaaS gehostete Datenspeicher in Virtual Network.
* **Azure-Dienste zulassen** – Einige Dienste ermöglichen es Ihnen, die Verbindung aller Azure-Dienste damit zuzulassen, falls Sie diese Option auswählen. 

Weitere Informationen zu unterstützten Netzwerksicherheitsmechanismen für Datenspeicher in Azure Integration Runtime und selbstgehosteter Integration Runtime finden Sie in den nachstehenden zwei Tabellen.  
* **Azure Integration Runtime**

    | Datenspeicher                  | Unterstützter Netzwerksicherheitsmechanismus für Datenspeicher | Private Link     | Vertrauenswürdiger Dienst     | Statischer IP-Adressbereich | Diensttags | Azure-Dienste zulassen |
    |------------------------------|-------------------------------------------------------------|---------------------|-----------------|--------------|----------------------|-----------------|
    | Azure PaaS-Datenspeicher       | Azure Cosmos DB                                     | Ja              | -                   | Ja             | -            | Ja                  |
    |                              | Azure-Daten-Explorer                                 | -                | -                   | Ja*            | Ja*         | -                    |
    |                              | Azure Data Lake Gen1                                | -                | -                   | Ja             | -            | Ja                  |
    |                              | Azure Database for MariaDB, MySQL, PostgreSQL       | -                | -                   | Ja             | -            | Ja                  |
    |                              | Azure File Storage                                  | Ja              | -                   | Ja             | -            | .                    |
    |                              | Azure Storage (Blob, ADLS Gen2)                     | Ja              | Ja (nur MSI-Authentifizierung) | Ja             | -            | .                    |
    |                              | Azure SQL DB, Azure Synapse Analytics, SQL ML  | Ja (nur Azure SQL DB/DW)        | -                   | Ja             | -            | Ja                  |
    |                              | Azure Key Vault (zum Abrufen von Geheimnissen/Verbindungszeichenfolge) | ja      | Ja                 | Ja             | -            | -                    |
    | Andere PaaS-/SaaS-Datenspeicher | AWS S3, SalesForce, Google Cloud Storage usw.    | -                | -                   | Ja             | -            | -                    |
    | Azure laaS                   | SQL Server, Oracle usw.                          | -                | -                   | Ja             | Ja          | -                    |
    | Lokales IaaS              | SQL Server, Oracle usw.                          | -                | -                   | Ja             | -            | -                    |
    
    **Gilt nur, wenn Azure Data Explorer in das virtuelle Netzwerk eingefügt wird und der IP-Adressbereich auf NSG/Firewall angewendet werden kann.* 

* **Selbstgehostete Integration Runtime (in VNET/lokal)**
    
    | Datenspeicher                  | Unterstützter Netzwerksicherheitsmechanismus für Datenspeicher         | Statische IP | Vertrauenswürdige Dienste  |
    |--------------------------------|---------------------------------------------------------------|-----------|---------------------|
    | Azure PaaS-Datenspeicher       | Azure Cosmos DB                                               | Ja       | -                   |
    |                                | Azure-Daten-Explorer                                           | -         | -                   |
    |                                | Azure Data Lake Gen1                                          | Ja       | -                   |
    |                                | Azure Database for MariaDB, MySQL, PostgreSQL               | Ja       | -                   |
    |                                | Azure File Storage                                            | Ja       | -                   |
    |                                | Azure Storage (Blog, ADLS Gen2)                             | Ja       | Ja (nur MSI-Authentifizierung) |
    |                                | Azure SQL DB, Azure Synapse Analytics, SQL ML          | Ja       | -                   |
    |                                | Azure Key Vault (zum Abrufen von Geheimnissen/Verbindungszeichenfolge) | Ja       | Ja                 |
    | Andere PaaS-/SaaS-Datenspeicher | AWS S3, SalesForce, Google Cloud Storage usw.              | Ja       | -                   |
    | Azure laaS                     | SQL Server, Oracle usw.                                  | Ja       | -                   |
    | Lokales laaS              | SQL Server, Oracle usw.                                  | Ja       | -                   |    

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen finden Sie in den folgenden verwandten Artikeln:
* [Unterstützte Datenspeicher](https://docs.microsoft.com/azure/data-factory/copy-activity-overview#supported-data-stores-and-formats)
* [Azure Key Vault – „Vertrauenswürdige Dienste“](https://docs.microsoft.com/azure/key-vault/key-vault-overview-vnet-service-endpoints#trusted-services)
* [Azure Storage – „Vertrauenswürdige Microsoft-Dienste“](https://docs.microsoft.com/azure/storage/common/storage-network-security#trusted-microsoft-services)
* [Verwaltete Identität für Data Factory](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity)
