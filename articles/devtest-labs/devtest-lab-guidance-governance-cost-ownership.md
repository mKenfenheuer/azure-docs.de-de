---
title: Verwalten von Kosten und Besitz in Azure DevTest Labs
description: Die Informationen in diesem Artikel helfen Ihnen beim Optimieren der Kosten und beim Festlegen des Besitzes in Ihrer gesamten Umgebung.
ms.topic: article
ms.date: 06/26/2020
ms.reviewer: christianreddington,anthdela,juselph
ms.openlocfilehash: dbf0bb9cae87a51eb6e0a4fb25c700ec6f423ff1
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2020
ms.locfileid: "85476256"
---
# <a name="governance-of-azure-devtest-labs-infrastructure---manage-cost-and-ownership"></a>Governance der Azure DevTest Labs-Infrastruktur – Verwalten der Kosten und des Besitzes
Kosten und Besitz sind zentrale Überlegungen beim Aufbau Ihrer Entwicklungs- und Testumgebungen. In diesem Abschnitt finden Sie Informationen, die Ihnen beim Optimieren der Kosten und beim Festlegen des Besitzes in Ihrer gesamten Umgebung helfen.

## <a name="optimize-for-cost"></a>Optimieren für Kosten

### <a name="question"></a>Frage
Wie kann ich in meiner DevTest Labs-Umgebung für die Kosten optimieren?

### <a name="answer"></a>Antwort
Es gibt verschiedene integrierte Features von DevTest Labs, die Ihnen dabei helfen, die Kosten zu optimieren. Informationen zum Beschränken der Benutzeraktivitäten finden Sie in den Artikeln [zur Kostenverwaltung und zu Schwellenwerten](devtest-lab-configure-cost-management.md) [und zu Richtlinien](devtest-lab-set-lab-policy.md). 

Wenn Sie DevTest Labs für Entwicklungs- und Testworkloads verwenden, sollten Sie den [Enterprise Dev/Test-Abonnementvorteil](https://azure.microsoft.com/offers/ms-azr-0148p/) im Rahmen Ihres Enterprise Agreements in Erwägung ziehen. Wenn Sie ein Kunde mit nutzungsbasierter Zahlung sind, sollten Sie stattdessen das Angebot [Dev/Test Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0023p/) berücksichtigen.

Dieser Ansatz bietet zahlreiche Vorteile:

- Niedrigere Dev/Test-Tarife für virtuelle Windows-Computer, Clouddienste, HDInsight, App Service und Logic Apps
- Großartige Enterprise Agreement-Tarife (EA) für andere Azure-Dienste
- Zugriff auf exklusive Dev/Test-Images im Katalog, einschließlich Windows 8.1 und Windows 10
 
Nur aktive Visual Studio-Abonnenten (Standardabonnements oder Jahres- und Monatscloudabonnements) können die im Rahmen eines Enterprise Dev/Test-Abonnements ausgeführten Azure-Dienste nutzen. Endbenutzer können jedoch auch auf die Anwendung zugreifen, um Feedback zu geben oder Akzeptanztests durchzuführen. Die Nutzung von Ressourcen im Rahmen dieses Abonnements ist auf das Entwickeln und Testen von Anwendungen beschränkt, und es wird keinerlei Garantie in Bezug auf die Betriebszeit gewährt.

Wenn Sie das DevTest-Angebot nutzen möchten, beachten Sie, dass dieser Vorteil ausschließlich für das Entwickeln und Testen Ihrer Anwendungen gilt. Die Nutzung im Rahmen des Abonnements unterliegt keiner Vereinbarung zum Servicelevel (SLA) mit finanzieller Absicherung, mit Ausnahme der Nutzung von Azure DevOps und HockeyApp.

## <a name="define-a-role-based-access-across-your-organization"></a>Definieren eines rollenbasierten Zugriffs in Ihrer gesamten Organisation
### <a name="question"></a>Frage
Wie definiere ich die rollenbasierte Zugriffssteuerung für meine DevTest Labs-Umgebungen, um sicherzustellen, dass die IT-Abteilung die Steuerung übernimmt, während Entwickler und Tester ihre Arbeit erledigen können? 

### <a name="answer"></a>Antwort
Es gibt ein allgemeines Muster, aber die Details sind von Ihrer Organisation abhängig.

Die IT-Zentrale sollte nur über die benötigten Informationen verfügen und den Projekt- und Anwendungsteams den erforderlichen Grad an Kontrolle ermöglichen. In der Regel bedeutet dies, dass die IT-Zentrale der Besitzer des Abonnements ist und die wichtigsten IT-Funktionen übernimmt, z.B. Netzwerkkonfigurationen. Die Gruppe von **Besitzern** eines Abonnement sollte klein sein. Diese Besitzer können weitere Besitzer vorschlagen, wenn dies erforderlich ist, oder Richtlinien auf Abonnementebene anwenden, z.B. „keine öffentliche IP-Adresse“.

Möglicherweise gibt es eine Teilmenge von Benutzern, die Zugriff auf ein Abonnement benötigen, z.B. der Support auf erster und zweiter Ebene. In diesem Fall wird empfohlen, diesen Benutzern Zugriff auf der Ebene **Mitwirkender** zu gewähren, sodass sie die Ressourcen verwalten können, aber keinen Benutzerzugriff erhalten oder Richtlinien anpassen können.

Die DevTest Labs-Ressource sollte im Besitz von Personen aus dem Umfeld des Projekt-/Anwendungsteams sein. Der Grund dafür ist, dass diesen Personen die Anforderungen an Computer und Software klar sind. In den meisten Organisationen ist der Besitzer dieser DevTest Labs-Ressource meist der Projekt-/Entwicklungsleiter. Dieser Besitzer kann Benutzer und Richtlinien in der Labumgebung und alle virtuellen Computer in der DevTest Labs-Umgebung verwalten.

Die Projekt-/Anwendungsteammitglieder sollten der Rolle „DevTest Lab-Benutzer“ hinzugefügt werden. Diese Benutzer können virtuelle Computer erstellen (entsprechend den Richtlinien auf Lab- und Abonnementebene). Sie können auch ihre eigenen virtuellen Computer verwalten. Sie können keine virtuellen Computer verwalten, die anderen Benutzern gehören.

Weitere Informationen finden Sie in der Dokumentation [Azure-Unternehmensgerüst – präskriptive Abonnementgovernance](/azure/architecture/cloud-adoption/appendix/azure-scaffold).


## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen finden Sie unter [Unternehmensrichtlinie und Compliance](devtest-lab-guidance-governance-policy-compliance.md).
