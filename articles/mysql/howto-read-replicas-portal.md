---
title: Verwalten von Lesereplikaten mit dem Azure-Portal in Azure Database for MySQL
description: Erfahren Sie, wie Sie mit dem Azure-Portal Lesereplikate in Azure Database for MySQL einrichten und verwalten.
author: ajlam
ms.author: andrela
ms.service: mysql
ms.topic: how-to
ms.date: 6/10/2020
ms.openlocfilehash: ad8fd20d744f7aaa113b4c46f8ca0f05a6cc6951
ms.sourcegitcommit: 53acd9895a4a395efa6d7cd41d7f78e392b9cfbe
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "90902845"
---
# <a name="how-to-create-and-manage-read-replicas-in-azure-database-for-mysql-using-the-azure-portal"></a>Informationen zum Erstellen und Verwalten von Lesereplikaten in Azure Database for MySQL mithilfe des Azure-Portals

In diesem Artikel erfahren Sie, wie Sie Lesereplikate im Azure Database for MySQL-Dienst über das Azure-Portal erstellen und verwalten.

## <a name="prerequisites"></a>Voraussetzungen

- Ein [Azure Database for MySQL-Server](quickstart-create-mysql-server-database-using-azure-portal.md), der als Masterserver verwendet wird

> [!IMPORTANT]
> Das Feature für Lesereplikate ist nur für Azure Database for MySQL-Server in den Tarifen „Universell“ oder „Arbeitsspeicheroptimiert“ verfügbar. Stellen Sie sicher, dass für den Masterserver einer dieser Tarife festgelegt ist.

## <a name="create-a-read-replica"></a>Erstellen eines Lesereplikats

> [!IMPORTANT]
> Wenn Sie ein Replikat für einen Master erstellen, der keine vorhandenen Replikate hat, startet der Master zunächst neu, um sich auf die Replikation vorzubereiten. Beachten Sie dies, und führen Sie diese Vorgänge nicht zu Spitzenzeiten durch.

Ein Lesereplikatserver kann mit den folgenden Schritten erstellt werden:

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/) an.

2. Wählen Sie den vorhandenen Azure Database for MySQL-Server aus, den Sie als Masterserver verwenden möchten. Mit dieser Aktion wird die Seite **Übersicht** geöffnet.

3. Wählen Sie im Menü unter **EINSTELLUNGEN** die Option **Replikation** aus.

4. Wählen Sie **Replikat hinzufügen**.

   :::image type="content" source="./media/howto-read-replica-portal/add-replica.png" alt-text="Azure Database for MySQL: Replikation":::

5. Geben Sie einen Namen für den Replikatserver ein.

    :::image type="content" source="./media/howto-read-replica-portal/replica-name.png" alt-text="Azure Database for MySQL – Replikatname":::

6. Wählen Sie den Standort für den Replikatserver aus. Der Standardstandort ist mit dem des Masterservers identisch.

    :::image type="content" source="./media/howto-read-replica-portal/replica-location.png" alt-text="Azure Database for MySQL – Replikatstandort":::

   > [!NOTE]
   > Weitere Informationen zu den Regionen, in denen Sie ein Replikat erstellen können, finden Sie im [Konzeptartikel zu Lesereplikaten](concepts-read-replicas.md). 

7. Wählen Sie **OK** aus, um die Erstellung des Replikats zu bestätigen.

> [!NOTE]
> Lesereplikate werden mit der gleichen Serverkonfiguration wie der Masterserver erstellt. Die Replikatserverkonfiguration kann nach der Erstellung geändert werden. Der Replikatserver wird immer in derselben Ressourcengruppe und demselben Abonnement wie der Masterserver erstellt. Wenn Sie einen Replikatserver in einer anderen Ressourcengruppe oder einem anderen Abonnement erstellen möchten, können Sie nach der Erstellung den [Replikatserver verschieben](https://docs.microsoft.com/azure/azure-resource-manager/management/move-resource-group-and-subscription). Für die Konfiguration des Replikatservers sollten mindestens die gleichen Werte verwendet werden wie für den Masterserver, damit das Replikat über genügend Kapazität verfügt.

Nach der Erstellung des Replikatservers kann dieser auf dem Blatt **Replikation** angezeigt werden.

   :::image type="content" source="./media/howto-read-replica-portal/list-replica.png" alt-text="Azure Database for MySQL: Auflisten der Replikate":::

## <a name="stop-replication-to-a-replica-server"></a>Beenden der Replikation auf einem Replikatserver

> [!IMPORTANT]
> Das Beenden der Replikation auf einem Server kann nicht rückgängig gemacht werden. Wenn die Replikation zwischen einem Master und dem Replikat beendet wurde, kann dies nicht rückgängig gemacht werden. Der Replikatserver wird zu einem eigenständigen Server und unterstützt nun Lese- und Schreibvorgänge. Der Server kann nicht wieder in ein Replikat umgewandelt werden.

Führen Sie die folgenden Schritte aus, um die Replikation zwischen einem Masterserver und einem Replikatserver im Azure-Portal zu beenden:

1. Wählen Sie im Azure-Portal Ihren Azure Database for MySQL-Masterserver aus. 

2. Wählen Sie im Menü unter **EINSTELLUNGEN** die Option **Replikation** aus.

3. Wählen Sie den Replikatserver aus, für den Sie die Replikation beenden möchten.

   :::image type="content" source="./media/howto-read-replica-portal/stop-replication-select.png" alt-text="Azure Database for MySQL: Beenden der Replikation, Auswählen des Servers":::

4. Wählen Sie **Replikation beenden** aus.

   :::image type="content" source="./media/howto-read-replica-portal/stop-replication.png" alt-text="Azure Database for MySQL: Replikation beenden":::

5. Klicken Sie auf **OK**, um zu bestätigen, dass Sie die Replikation beenden möchten.

   :::image type="content" source="./media/howto-read-replica-portal/stop-replication-confirm.png" alt-text="Azure Database for MySQL: Bestätigen, dass die Replikation beendet werden soll":::

## <a name="delete-a-replica-server"></a>Löschen eines Replikatservers

Führen Sie die folgenden Schritte aus, um einen Lesereplikatserver im Azure-Portal zu löschen:

1. Wählen Sie im Azure-Portal Ihren Azure Database for MySQL-Masterserver aus.

2. Wählen Sie im Menü unter **EINSTELLUNGEN** die Option **Replikation** aus.

3. Wählen Sie den Replikatserver aus, den Sie löschen möchten.

   :::image type="content" source="./media/howto-read-replica-portal/delete-replica-select.png" alt-text="Azure Database for MySQL: Replikat löschen, Auswählen des Servers":::

4. Wählen Sie **Replikat löschen** aus.

   :::image type="content" source="./media/howto-read-replica-portal/delete-replica.png" alt-text="Azure Database for MySQL: Replikat löschen":::

5. Geben Sie den Namen des Replikats ein, und klicken Sie auf **Löschen**, um das Löschen des Replikats zu bestätigen.  

   :::image type="content" source="./media/howto-read-replica-portal/delete-replica-confirm.png" alt-text="Azure Database for MySQL: Bestätigen der Replikatlöschung":::

## <a name="delete-a-master-server"></a>Löschen eines Masterservers

> [!IMPORTANT]
> Wenn Sie einen Masterserver löschen, wird die Replikation auf allen Replikatservern beendet und der Masterserver selbst gelöscht. Replikatserver werden zu eigenständigen Servern, die nun Lese- und Schreibvorgänge unterstützen.

Führen Sie die folgenden Schritte aus, um einen Masterserver im Azure-Portal zu löschen:

1. Wählen Sie im Azure-Portal Ihren Azure Database for MySQL-Masterserver aus.

2. Wählen Sie unter **Übersicht** die Option **Löschen** aus.

   :::image type="content" source="./media/howto-read-replica-portal/delete-master-overview.png" alt-text="Azure Database for MySQL: Löschen eines Masterservers":::

3. Geben Sie den Namen des Masterservers ein, und klicken Sie auf **Löschen**, um das Löschen des Masterservers zu bestätigen.  

   :::image type="content" source="./media/howto-read-replica-portal/delete-master-confirm.png" alt-text="Azure Database for MySQL: Löschen eines Masterservers":::

## <a name="monitor-replication"></a>Überwachen der Replikation

1. Wählen Sie im [Azure-Portal](https://portal.azure.com/) den zu überwachenden Azure Database for MySQL-Replikatserver aus.

2. Wählen Sie auf der Seitenleiste im Abschnitt **Überwachung** die Option **Metriken** aus:

3. Wählen Sie in der Dropdownliste der verfügbaren Metriken die Option **Replication lag in seconds** (Replikationsverzögerung in Sekunden) aus.

   :::image type="content" source="./media/howto-read-replica-portal/monitor-select-replication-lag.png" alt-text="Auswählen der Replikationsverzögerung":::

4. Wählen Sie den Zeitraum aus, den Sie anzeigen möchten. In der folgenden Abbildung wird ein Zeitraum von 30 Minuten ausgewählt.

   :::image type="content" source="./media/howto-read-replica-portal/monitor-replication-lag-time-range.png" alt-text="Auswählen eines Zeitbereichs":::

5. Zeigen Sie die Replikationsverzögerung für den ausgewählten Zeitraum an. Die folgende Abbildung zeigt die letzten 30 Minuten.

   :::image type="content" source="./media/howto-read-replica-portal/monitor-replication-lag-time-range-thirty-mins.png" alt-text="Auswählen eines Zeitbereichs":::

## <a name="next-steps"></a>Nächste Schritte

- Weitere Informationen zu [Lesereplikaten](concepts-read-replicas.md)
