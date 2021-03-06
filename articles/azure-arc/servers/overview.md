---
title: 'Azure Arc-fähige Server: Übersicht'
description: Hier erfahren Sie, wie Sie außerhalb von Azure gehostete Server mithilfe von Servern mit Azure Arc-Unterstützung wie eine Azure-Ressource verwalten.
keywords: Azure Automation, DSC, PowerShell, Desired State Configuration, Updateverwaltung, Änderungsnachverfolgung, Bestand, Runbooks, Python, grafisch, Hybrid
ms.date: 09/16/2020
ms.topic: overview
ms.openlocfilehash: 9fcac35f943eefb15a200e9b148b22ce67cc3941
ms.sourcegitcommit: eb6bef1274b9e6390c7a77ff69bf6a3b94e827fc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "90887530"
---
# <a name="what-is-azure-arc-enabled-servers"></a>Was sind Server mit Azure Arc-Aktivierung?

Mit Servern mit Azure Arc-Unterstützung können Sie Windows- und Linux-Computer, die außerhalb von Azure in Ihrem Unternehmensnetzwerk oder von einem anderen Cloudanbieter gehostet werden, auf ähnliche Weise verwalten wie native virtuelle Azure-Computer. Wenn ein Hybridcomputer mit Azure verbunden wird, wird er zu einem verbundenen Computer und in Azure wie eine Ressource behandelt. Jeder verbundene Computer verfügt über eine Ressourcen-ID, wird als Teil einer Ressourcengruppe unter einem Abonnement verwaltet und profitiert von Azure-Standardkonstrukten wie Azure Policy und Tagging. Dienstanbieter, die die lokale Infrastruktur eines Kunden verwalten, können ihre Hybridcomputer genau wie heute mit [Azure Lighthouse](../../lighthouse/how-to/manage-hybrid-infrastructure-arc.md) mit Azure Arc mit nativen Azure-Ressourcen über mehrere Kundenumgebungen hinweg verwalten.

Um diese Möglichkeit für Ihre außerhalb von Azure gehosteten Hybridcomputer nutzen zu können, muss auf jedem Computer, den Sie mit Azure verbinden möchten, der Azure Connected Machine-Agent installiert werden. Dieser Agent bietet keine weiteren Funktionen und ist kein Ersatz für den [Log Analytics-Agent](../../azure-monitor/platform/log-analytics-agent.md) von Azure. Der Log Analytics-Agent für Windows und Linux ist erforderlich, wenn Sie das Betriebssystem und die Workloads auf dem Computer proaktiv überwachen, den Computer mithilfe von Automation-Runbooks oder Lösungen wie der Updateverwaltung verwalten oder andere Azure-Dienste wie [Azure Security Center](../../security-center/security-center-intro.md) verwenden möchten.

## <a name="supported-scenarios"></a>Unterstützte Szenarios

Wenn Sie Ihren Computer mit Servern mit Azure Arc-Unterstützung verbinden, können Sie die folgenden Aufgaben für die Konfigurationsverwaltung und Überwachungsaufgaben ausführen:

- Zuweisen von [Azure Policy-Gastkonfigurationen](../../governance/policy/concepts/guest-configuration.md) mit der gleichen Vorgehensweise wie bei der Richtlinienzuweisung für virtuelle Azure-Computer

- Melden Sie Konfigurationsänderungen zu installierter Software, Microsoft-Diensten, Windows-Registrierung und -Dateien und Linux-Daemons auf überwachten Servern mit [Änderungsnachverfolgung und Bestand](../../automation/change-tracking.md) von Azure Automation.

- Überwachen der Leistung des Gastbetriebssystems des verbundenen Computers und Erkennen von Anwendungskomponenten, um deren Prozesse und Abhängigkeiten mit anderen, von der Anwendung kommunizierten Ressourcen über [Azure Monitor für VMs](../../azure-monitor/insights/vminsights-overview.md) zu überwachen

- Vereinfachen der Bereitstellung mit anderen Azure-Diensten wie Azure Automation [State Configuration](../../automation/automation-dsc-overview.md) und Azure Monitor Log Analytics-Arbeitsbereich unter Verwendung der unterstützten [Azure-VM-Erweiterungen](manage-vm-extensions.md) für Ihren Azure-fremden Windows- oder Linux-Computer. Dies schließt die Konfiguration nach der Bereitstellung oder die Softwareinstallation unter Verwendung der benutzerdefinierten Skripterweiterung mit ein.

- Verwalten Sie Betriebssystemupdates für Ihre Windows- und Linux-Server mithilfe der [Updateverwaltung](../../automation/update-management/update-mgmt-overview.md) in Azure Automation. Stellen Sie zunächst die [Hybrid Runbook-Workerrolle](../../automation/automation-hybrid-runbook-worker.md) bereit, und befolgen Sie dann die Schritte zum [Aktivieren der Updateverwaltung](../../automation/update-management/update-mgmt-enable-portal.md) auf Ihrem Azure-fremden Windows- oder Linux-Computer.

- Schließen Sie Ihren Azure-fremden Server für die Bedrohungserkennung ein, und überwachen Sie proaktiv potenzielle Sicherheitsbedrohungen mit dem [Azure Security Center](../../security-center/security-center-intro.md).

Erfasste und in einem Log Analytics-Arbeitsbereich gespeicherte Protokolldaten des Hybridcomputers enthalten jetzt computerspezifische Eigenschaften wie etwa eine Ressourcen-ID. Dies kann zur Unterstützung des Protokollzugriffs im [Ressourcenkontext](../../azure-monitor/platform/design-logs-deployment.md#access-mode) verwendet werden.

[!INCLUDE [azure-lighthouse-supported-service](../../../includes/azure-lighthouse-supported-service.md)]

## <a name="supported-regions"></a>Unterstützte Regionen

Eine definitive Liste der unterstützten Regionen mit Azure Arc-fähigen Servern finden Sie auf der Seite [Verfügbare Produkte nach Region](https://azure.microsoft.com/global-infrastructure/services/?products=azure-arc).

In den meisten Fällen sollte der Standort, den Sie beim Erstellen des Installationsskripts auswählen, die Azure-Region sein, die dem Standort Ihres Computers geografisch am nächsten ist. Ruhende Daten werden innerhalb der geografischen Azure-Region gespeichert, in der sich die von Ihnen angegebene Region befindet, was ggf. auch Auswirkungen auf die Wahl der Region hat, wenn Data Residency-Anforderungen erfüllt werden müssen. Wenn die Azure-Region, mit der Ihr Computer verbunden ist, von einem Ausfall betroffen ist, wird der verbundene Computer zwar nicht beeinträchtigt, es kann jedoch sein, dass Verwaltungsvorgänge mit Azure nicht abgeschlossen werden können. Wenn Sie über mehrere Standorte verfügen, die einen geografisch redundanten Dienst unterstützen, empfiehlt es sich im Falle eines regionalen Ausfalls, die Computer an den einzelnen Standorten jeweils mit einer anderen Azure-Region zu verbinden.

### <a name="agent-status"></a>Agent-Status

Der Connected Machine-Agent sendet alle fünf Minuten eine reguläre Heartbeatnachricht an den Dienst. Wenn der Dienst keine solchen Heartbeatnachrichten mehr von einem Computer empfängt, wird dieser Computer als offline betrachtet, und der Status wird im Portal innerhalb von 15 bis 30 Minuten automatisch in **Getrennt** geändert. Wenn wieder eine Heartbeatnachricht des Connected Machine-Agents empfangen wird, ändert sich der Status automatisch in **Verbunden**.

## <a name="next-steps"></a>Nächste Schritte

Bevor Sie Server mit Arc-Unterstützung auf mehreren Hybridcomputern auswerten oder aktivieren, lesen Sie [Übersicht über den Connected Machine-Agent](agent-overview.md), um die Anforderungen, technischen Details zum Agent und Bereitstellungsmethoden zu verstehen.
