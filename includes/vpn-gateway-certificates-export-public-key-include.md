---
title: include file
description: include file
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 03/19/2020
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: f71703dcb6afb5ce7610bf1c5374de1cc98816b0
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2020
ms.locfileid: "90606951"
---
Exportieren Sie nach dem Erstellen eines selbstsignierten Stammzertifikats die CER-Datei für den öffentlichen Schlüssel des Stammzertifikats (nicht den privaten Schlüssel). Sie laden diese Datei später in Azure hoch. Führen Sie die folgenden Schritte aus, um die CER-Datei für Ihr selbstsigniertes Stammzertifikat zu exportieren:

1. Öffnen Sie **Benutzerzertifikate verwalten**, um eine CER-Datei für das Zertifikat zu erhalten. Suchen Sie das selbstsignierte Stammzertifikat (in der Regel in „Zertifikate – Aktueller Benutzer\Eigene Zertifikate\Zertifikate“), und klicken Sie mit der rechten Maustaste darauf. Klicken Sie auf **Alle Aufgaben** und anschließend auf **Exportieren**. Dadurch wird der **Zertifikatexport-Assistent**geöffnet. Wenn Sie das Zertifikat unter „Aktueller Benutzer\Eigene Zertifikate\Zertifikate“ nicht finden, haben Sie unter Umständen versehentlich „Zertifikate – Lokaler Benutzer“ anstelle von „Zertifikate – Aktueller Benutzer“ geöffnet. Wenn Sie den Zertifikat-Manager im Bereich für den aktuellen Benutzer mithilfe von PowerShell öffnen möchten, geben Sie *certmgr* ins Konsolenfenster ein.

   ![Screenshot des Fensters „Zertifikate“ für den aktuellen Benutzer, in dem „Zertifikate“ und in einem Kontextmenü „Alle Aufgaben“ und „Exportieren“ ausgewählt sind.](./media/vpn-gateway-certificates-export-public-key-include/export.png)
2. Klicken Sie im Assistenten auf **Weiter**.

   ![Exportieren des Zertifikats](./media/vpn-gateway-certificates-export-public-key-include/exportwizard.png)
3. Wählen Sie **Nein, privaten Schlüssel nicht exportieren** aus, und klicken Sie dann auf **Weiter**.

   ![Nein, privaten Schlüssel nicht exportieren](./media/vpn-gateway-certificates-export-public-key-include/notprivatekey.png)
4. Wählen Sie auf der Seite **Dateiformat für den Export** die Option **Base-64-codiert X.509 (.CER)** aus, und klicken Sie dann auf **Weiter**.

   ![Base64-codiert](./media/vpn-gateway-certificates-export-public-key-include/base64.png)
5. Wählen Sie unter **Zu exportierende Datei** die Option **Durchsuchen** aus, um zu dem Speicherort zu wechseln, an den das Zertifikat exportiert werden soll. Geben Sie unter **Dateiname**einen Namen für die Zertifikatdatei ein. Klicken Sie auf **Weiter**.

   ![Screenshot des Zertifikatexport-Assistenten mit dem Textfeld „Dateiname“ und der Option „Durchsuchen“](./media/vpn-gateway-certificates-export-public-key-include/browse.png)
6. Klicken Sie auf **Fertig stellen** , um das Zertifikat zu exportieren.

   ![Screenshot der letzten Seite des Zertifikatexport-Assistenten mit den ausgewählten Einstellungen](./media/vpn-gateway-certificates-export-public-key-include/finish.png)
7. Das Zertifikat wurde erfolgreich exportiert.

   ![Screenshot einer Meldung, die angibt, dass der Export erfolgreich war](./media/vpn-gateway-certificates-export-public-key-include/success.png)
8. Das exportierte Zertifikat sieht in etwa wie folgt aus:

   ![Screenshot eines Zertifikatsymbols und eines Dateinamens mit der Dateinamenerweiterung „C E R“](./media/vpn-gateway-certificates-export-public-key-include/exported.png)
9. Wenn Sie das exportierte Zertifikat mit Editor öffnen, ähnelt die Datei diesem Beispiel. Der blaue Abschnitt enthält die Informationen, die in Azure hochgeladen werden. Wenn Sie das Zertifikat mit Editor öffnen und es nicht so ähnlich aussieht, bedeutet dies in der Regel, dass Sie es nicht als Base64-codiertes X.509-Zertifikat (.cer) exportiert haben. Wenn Sie darüber hinaus einen anderen Text-Editor verwenden möchten, sollten Sie beachten, dass einige Editoren unbeabsichtigte Formatierung im Hintergrund einführen können. Dies kann Probleme beim Hochladen des Texts aus diesem Zertifikat in Azure verursachen.

   ![Mit Editor öffnen](./media/vpn-gateway-certificates-export-public-key-include/notepad.png)
