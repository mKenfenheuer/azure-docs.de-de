---
title: Erstellen eines Projekts – Benutzerdefinierter Translator
titleSuffix: Azure Cognitive Services
description: In diesem Artikel wird erklärt, wie Sie ein Projekt im benutzerdefinierten Translator von Azure Cognitive Services erstellen und verwalten.
author: swmachan
manager: nitinme
ms.service: cognitive-services
ms.subservice: translator-text
ms.date: 08/17/2020
ms.author: swmachan
ms.topic: conceptual
ms.openlocfilehash: 3043ec0600f802a409387f0114aae5f56151da16
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2020
ms.locfileid: "88510976"
---
# <a name="create-a-project"></a>Erstellen eines Projekts

Ein Projekt ist ein Container für Modelle, Dokumente und Tests. Jedes Projekt enthält automatisch alle Dokumente, die in den Arbeitsbereich hochgeladen werden und über das korrekte Sprachenpaar verfügen.

Die Projekterstellung ist der erste Schritt auf dem Weg zur Modellerstellung.

## <a name="create-a-project"></a>So erstellen Sie ein Projekt:

1.  Klicken Sie im Portal [Custom Translator](https://portal.customtranslator.azure.ai) auf „Projekt erstellen“.

    ![Projekt erstellen](media/how-to/how-to-create-project.png)

2.  Geben Sie die folgenden Projektdetails in das Dialogfeld ein:

    a.  Projektname (erforderlich): Geben Sie Ihrem Projekt einen eindeutigen, aussagekräftigen Namen. Die Sprachen müssen im Titel nicht erwähnt werden.

    b.  Beschreibung: Eine kurze Zusammenfassung des Projekts. Diese Beschreibung hat keinerlei Einfluss auf das Verhalten von Custom Translator oder auf das resultierende benutzerdefinierte System, kann aber die Unterscheidung verschiedener Projekte erleichtern.

    c.  Sprachpaar (erforderlich): Wählen Sie die Ausgangs- und Zielsprache für die Übersetzung aus.

    d.  Kategorie (erforderlich): Wählen Sie die Kategorie aus, die am besten zu Ihrem Projekt passt. Die Kategorie beschreibt die Terminologie und den Stil der Dokumente, die Sie übersetzen möchten.

    e.  Kategoriebeschreibung: Geben Sie in diesem Feld eine genauere Beschreibung des Bereichs oder der Branche an, in dem bzw. in der Sie tätig sind. In der Kategorie „Medizin“ können Sie beispielsweise ein bestimmtes Dokument (etwa zum Thema Chirurgie oder Kinderheilkunde) hinzufügen. Die Beschreibung hat keinerlei Einfluss auf das Verhalten von Custom Translator oder auf das resultierende benutzerdefinierte System.

    f.  Projektbezeichnung: Die [Projektbezeichnung](workspace-and-project.md#project-labels) dient zur Unterscheidung von Projekten mit gleichem Sprachpaar und gleicher Kategorie. Eine Bezeichnung sollte *nur* verwendet werden, wenn Sie mehrere Projekte für das gleiche Sprachpaar und die gleiche Kategorie erstellen und auf diese Projekte jeweils mit einer anderen Kategorie-ID zugreifen möchten. Verwenden Sie dieses Feld nicht, wenn Sie Systeme für nur eine Kategorie erstellen. Eine Projektbezeichnung trägt nicht zur Unterscheidung zwischen Sprachpaaren bei. Die gleiche Bezeichnung kann für mehrere Projekte verwendet werden.

    ![Dialogfeld für die Projekterstellung](media/how-to/how-to-create-project-dialog.png)

3.  Klicken Sie auf „Erstellen“.

## <a name="view-project-details"></a>Anzeigen der Projektdetails

Auf der Landing Page von Custom Translator werden die ersten zehn Projekte in Ihrem Arbeitsbereich angezeigt. Die Anzeige umfasst den Projektnamen, das Sprachpaar, die Kategorie, den Status und die BLEU Bewertung.

Wenn Sie ein Projekt auswählen, wird eine Projektseite mit Folgendem angezeigt:

- CategoryID: Bei der Kategorie-ID handelt es sich um eine Verkettung von Arbeitsbereich-ID, Projektbezeichnung und Kategoriecode. Mithilfe der Kategorie-ID können Sie über die Textübersetzungs-API benutzerdefinierte Übersetzungen abrufen. Klicken Sie zum Kopieren auf das Kopiersymbol.

- Schaltfläche „Train“ (Trainieren): Diese Schaltfläche dient zum [Trainieren eines Modells](how-to-train-model.md).

- Schaltfläche „Add documents“ (Dokumente hinzufügen): Diese Schaltfläche dient zum [Hochladen von Dokumenten](how-to-upload-document.md).

- Schaltfläche „Filter documents“ (Dokumente filtern): Diese Schaltfläche dient zum Filtern von Dokumenten sowie zum Suchen nach bestimmten Dokumenten.

    ![Anzeigen der Projektdetails](media/how-to/how-to-view-project.png)

## <a name="next-steps"></a>Nächste Schritte

- Informieren Sie sich über das [Suchen, Bearbeiten und Löschen von Projekten](how-to-search-edit-delete-projects.md).
- Informieren Sie sich über das [Hochladen eines Dokuments](how-to-upload-document.md) zur Erstellung von Übersetzungsmodellen.
