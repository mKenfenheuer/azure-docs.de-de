---
title: Azure CDN-Endpunkt mit mehreren Ursprüngen (Vorschau)
description: Hier finden Sie Informationen zu den ersten Schritten mit einem Azure CDN-Endpunkt mit mehreren Ursprüngen.
services: cdn
author: asudbring
manager: KumudD
ms.service: azure-cdn
ms.topic: how-to
ms.date: 9/06/2020
ms.author: allensu
ms.openlocfilehash: f9293206526778f8c3de8a368a1916a2cb3f88c2
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2020
ms.locfileid: "89504672"
---
# <a name="azure-cdn-endpoint-multi-origin-preview"></a>Azure CDN-Endpunkt mit mehreren Ursprüngen (Vorschau)

Die Unterstützung für mehrere Ursprünge beseitigt Ausfallzeiten und sorgt für globale Redundanz. 

Durch die Auswahl mehrerer Ursprünge an einem Azure CDN-Endpunkt wird das Risiko durch die bereitgestellte Redundanz, durch das Testen der Integrität der einzelnen Ursprünge und ggf. durch ein Failover verteilt.

Richten Sie eine oder mehrere Ursprungsgruppen ein, und wählen Sie eine Standardursprungsgruppe aus. Jede Ursprungsgruppe ist eine Sammlung von einem oder mehreren Ursprüngen, die ähnliche Workloads übernehmen können.

> [!NOTE]
> Dieses Feature ist derzeit nur über Azure CDN von Microsoft verfügbar. 

> [!IMPORTANT]
> Azure CDN-Endpunkt mit mehreren Ursprüngen befindet sich aktuell in der öffentlichen Vorschauphase.
> Diese Vorschauversion wird ohne Vereinbarung zum Servicelevel bereitgestellt und ist nicht für Produktionsworkloads vorgesehen. Manche Features werden möglicherweise nicht unterstützt oder sind nur eingeschränkt verwendbar. Weitere Informationen finden Sie unter [Zusätzliche Nutzungsbestimmungen für Microsoft Azure-Vorschauen](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## <a name="create-the-origin-group"></a>Erstellen der Ursprungsgruppe

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com)

2. Wählen Sie Ihr Azure CDN-Profil und dann den Endpunkt aus, der für mehrere Ursprünge konfiguriert werden soll.

3. Wählen Sie in der Endpunktkonfiguration unter **Einstellungen** die Option **Ursprung** aus:

    :::image type="content" source="./media/endpoint-multiorigin/endpoint-multiorigin-1.png" alt-text="CDN-Endpunkt" border="true":::

4. Zum Aktivieren von mehreren Ursprüngen benötigen Sie mindestens eine Ursprungsgruppe. Wählen Sie **Ursprungsgruppe erstellen** aus:

    :::image type="content" source="./media/endpoint-multiorigin/endpoint-multiorigin-2.png" alt-text="CDN-Endpunkt" border="true":::

5. Geben Sie unter der Konfiguration **Ursprungsgruppe hinzufügen** die folgenden Informationen ein, oder wählen Sie sie aus:

   | Einstellung           | Wert                                                                 |
   |-------------------|-----------------------------------------------------------------------|
   | Name der Ursprungsgruppe | Geben Sie einen Namen für die Ursprungsgruppe ein.                                   |
   | Teststatus      | Wählen Sie **Aktiviert**. </br> Azure CDN führt Integritätstests von verschiedenen Punkten auf der ganzen Welt aus, um die Integrität des Ursprungs zu ermitteln. Aktivieren Sie diese Einstellung nicht, wenn die aktuelle Ursprungsgruppe nicht aktiv ist, um zusätzliche Kosten zu vermeiden.
   | Testpfad        | Der Pfad im Ursprung, der zum Ermitteln der Integrität verwendet wird. |
   | Testintervall    | Wählen Sie ein Testintervall von 1, 2 oder 4 Minuten aus.                        |
   | Testprotokoll    | Wählen Sie **HTTP** oder **HTTPS** aus.                                         |
   | Testmethode      | Wählen Sie **Head** oder **Get** aus.                                           |
   | Standardursprungsgruppe | Aktivieren Sie das Kontrollkästchen, um die Standardursprungsgruppe festzulegen.
    
   :::image type="content" source="./media/endpoint-multiorigin/endpoint-multiorigin-3.png" alt-text="CDN-Endpunkt" border="true":::

6. Wählen Sie **Hinzufügen**.

## <a name="add-multiple-origins"></a>Hinzufügen mehrerer Ursprünge

1. Wählen Sie unter den Ursprungseinstellungen für Ihren Endpunkt die Option **+ Ursprung erstellen** aus:

    :::image type="content" source="./media/endpoint-multiorigin/endpoint-multiorigin-5.png" alt-text="CDN-Endpunkt" border="true":::

2. Geben Sie unter der Konfiguration **Ursprung hinzufügen** die folgenden Informationen ein, oder wählen Sie sie aus:

   | Einstellung           | Wert                                                                 |
   |-------------------|-----------------------------------------------------------------------|
   | Name        | Geben Sie einen Namen für den Ursprung ein.        |
   | Ursprungstyp | Wählen Sie **Speicher**, **Clouddienst**, **Web-App** oder **Benutzerdefinierter Ursprung** aus.                                   |
   | Hostname des Ursprungs        | Wählen Sie den Hostnamen des Ursprungs aus, oder geben Sie ihn ein.  In der Dropdownliste werden alle verfügbaren Ursprünge des Typs aufgelistet, den Sie in der vorherigen Einstellung angegeben haben. Wenn Sie **Benutzerdefinierter Ursprung** als Ursprungstyp ausgewählt haben, geben Sie die Domäne Ihres Kundenursprungsservers ein. |
   | Header des Ursprungshosts    | Geben Sie den Hostheader ein, den das Azure CDN bei jeder Anforderung senden soll, oder übernehmen Sie den Standardwert.                        |
   | HTTP-Port   | Geben Sie den HTTP-Port ein.                                         |
   | HTTPS-Port     | Geben Sie den HTTPS-Port ein.                                           |
   | Priorität    | Geben Sie eine Zahl zwischen 1 und 5 ein.       |
   | Weight      | Geben Sie eine Zahl zwischen 1 und 1000 ein.   |

    > [!NOTE]
    > Wenn ein Ursprung innerhalb einer Ursprungsgruppe erstellt wird, muss ihm eine Priorität und Gewichtung zugewiesen werden. Wenn eine Ursprungsgruppe nur einen Ursprung enthält, wird die Standardpriorität und die Standardgewichtung auf 1 festgelegt. Der Datenverkehr wird an die Ursprünge mit der höchsten Priorität weitergeleitet, sofern der Ursprung fehlerfrei ist. Wenn ein Ursprung als fehlerhaft erkannt wird, werden die Verbindungen an einen anderen Ursprung in Reihenfolge der Priorität umgeleitet. Wenn zwei Ursprünge dieselbe Priorität aufweisen, wird der Datenverkehr gemäß der für den Ursprung festgelegten Gewichtung verteilt. 

    :::image type="content" source="./media/endpoint-multiorigin/endpoint-multiorigin-6.png" alt-text="CDN-Endpunkt" border="true":::

3. Wählen Sie **Hinzufügen**.

4. Wählen Sie **Ursprung konfigurieren** aus, um den Ursprungspfad für alle Ursprünge festzulegen:

    :::image type="content" source="./media/endpoint-multiorigin/endpoint-multiorigin-7.png" alt-text="CDN-Endpunkt" border="true":::

5. Klicken Sie auf **OK**.

## <a name="configure-origins-and-origin-group-settings"></a>Konfigurieren von Ursprüngen und Ursprungsgruppeneinstellungen

Sobald Sie über mehrere Ursprünge und eine Ursprungsgruppe verfügen, können Sie die Ursprünge in verschiedenen Gruppen hinzufügen oder daraus entfernen. Ursprünge innerhalb derselben Gruppe sollten ähnlichen Workloads dienen. Der Datenverkehr wird basierend auf dem fehlerfreien Status, der Priorität und dem Gewichtungswert auf diese Ursprünge verteilt. 

1. Wählen Sie unter den Ursprungseinstellungen für den Azure CDN-Endpunkt den Namen der Ursprungsgruppe aus, die Sie konfigurieren möchten:

    :::image type="content" source="./media/endpoint-multiorigin/endpoint-multiorigin-8.png" alt-text="CDN-Endpunkt" border="true":::

2. Wählen Sie unter **Ursprungsgruppe aktualisieren** die Option **+ Ursprung auswählen** aus:

    :::image type="content" source="./media/endpoint-multiorigin/endpoint-multiorigin-9.png" alt-text="CDN-Endpunkt" border="true":::

4. Wählen Sie im Pulldownfeld den Ursprung aus, den Sie der Gruppe hinzufügen möchten, und wählen Sie dann **OK** aus.

5. Vergewissern Sie sich, dass der Ursprung der Gruppe hinzugefügt wurde, und wählen Sie dann **Speichern** aus:

    :::image type="content" source="./media/endpoint-multiorigin/endpoint-multiorigin-10.png" alt-text="CDN-Endpunkt" border="true":::

## <a name="remove-origin-from-origin-group"></a>Entfernen eines Ursprung aus der Ursprungsgruppe

1. Wählen Sie unter den Ursprungseinstellungen für den Azure CDN-Endpunkt den Namen der Ursprungsgruppe aus:

    :::image type="content" source="./media/endpoint-multiorigin/endpoint-multiorigin-8.png" alt-text="CDN-Endpunkt" border="true":::

2. Um einen Ursprung aus der Ursprungsgruppe zu entfernen, wählen Sie das Papierkorbsymbol neben dem Ursprung und dann **Speichern** aus:

    :::image type="content" source="./media/endpoint-multiorigin/endpoint-multiorigin-11.png" alt-text="CDN-Endpunkt" border="true":::

## <a name="override-origin-group-with-rules-engine"></a>Außerkraftsetzen einer Ursprungsgruppe mit der Regel-Engine

Passen Sie die Verteilung des Datenverkehrs auf die verschiedenen Ursprungsgruppen mithilfe der Standardregel-Engine an.

Verteilen Sie den Datenverkehr basierend auf der Anforderungs-URL auf eine andere Gruppe.

1. Wählen Sie an Ihrem CDN-Endpunkt die Option **Regel-Engine** unter **Einstellungen** aus:

:::image type="content" source="./media/endpoint-multiorigin/endpoint-multiorigin-12.png" alt-text="CDN-Endpunkt" border="true":::

2. Wählen Sie **+ Regel hinzufügen** aus.

3. Geben Sie unter **Name** einen Namen für die Regel ein.

4. Wählen Sie **+ Bedingung** und dann **URL-Pfad** aus.

5. Wählen Sie im Pulldownmenü **Operator** die Option **Enthält** aus.

6. Geben Sie in **Wert** die Zeichenfolge **/images** ein.

7. Wählen Sie **+ Aktion hinzufügen** und dann **Ursprungsgruppe überschreiben** aus.

8. Wählen Sie im Pulldownmenü in **Ursprungsgruppe** Ihre Ursprungsgruppe aus.

:::image type="content" source="./media/endpoint-multiorigin/endpoint-multiorigin-13.png" alt-text="CDN-Endpunkt" border="true":::

Für alle eingehenden Anforderungen gilt: Wenn der URL-Pfad **/images** enthält, wird die Anforderung der Ursprungsgruppe im Aktionsabschnitt **(myorigingroup)** zugewiesen. 

## <a name="next-steps"></a>Nächste Schritte
In diesem Artikel haben Sie den Azure CDN-Endpunkt mit mehreren Ursprüngen aktiviert.

Weitere Informationen zu Azure CDN und den anderen in diesem Artikel erwähnten Azure-Diensten finden Sie unter den folgenden Quellen:

* [Azure CDN](./cdn-overview.md)
* [Vergleichen von Azure CDN-Produktfeatures](./cdn-features.md)
