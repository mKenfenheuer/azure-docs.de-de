---
title: Was ist Custom Vision?
titleSuffix: Azure Cognitive Services
description: Hier erfahren Sie, wie Sie mithilfe des Custom Vision-Diensts in Azure benutzerdefinierte KI-Bildklassifizierungen und Objekterkennungen in der Azure-Cloud erstellen.
services: cognitive-services
author: PatrickFarley
manager: nitinme
ms.service: cognitive-services
ms.subservice: custom-vision
ms.topic: overview
ms.date: 09/14/2020
ms.author: pafarley
ms.custom: cog-serv-seo-aug-2020
keywords: bilderkennung, bildbezeichner, app für bilderkennung, custom vision
ms.openlocfilehash: 47227a60b1ed45499afdb42fbc062abc5ae51ff9
ms.sourcegitcommit: eb6bef1274b9e6390c7a77ff69bf6a3b94e827fc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "90605465"
---
# <a name="what-is-custom-vision"></a>Was ist Custom Vision?

[!INCLUDE [TLS 1.2 enforcement](../../../includes/cognitive-services-tls-announcement.md)]

Azure Custom Vision ist ein Bilderkennungsdienst zum Erstellen, Bereitstellen und Optimieren benutzerdefinierter Bildbezeichner. Ein Bildbezeichner wendet entsprechend den visuellen Merkmalen auf einem Bild Bezeichnungen (die Klassen oder Objekte darstellen) auf Bilder an. Anders als beim Dienst für [maschinelles Sehen](https://docs.microsoft.com/azure/cognitive-services/computer-vision/home) können Sie bei Custom Vision die Bezeichnungen angeben und benutzerdefinierte Modelle für deren Erkennung trainieren.

## <a name="what-it-does"></a>Funktionsbeschreibung

Der Custom Vision-Dienst verwendet einen Machine-Learning-Algorithmus, um Bilder zu analysieren. Sie als Entwickler müssen Gruppen von Bildern übermitteln, auf denen die betreffenden Merkmale vorhanden bzw. nicht vorhanden sind. Die Bezeichnungen wenden Sie selbst beim Übermitteln auf die Bilder an. Der Algorithmus wird dann mit diesen Daten trainiert und berechnet seine eigene Genauigkeit, indem er Tests anhand dieser Bilder durchführt. Nachdem der Algorithmus trainiert wurde, können Sie ihn testen, noch mal trainieren und schließlich für Ihre Bilderkennungs-App verwenden, um neue Bilder zu klassifizieren. Darüber hinaus kann das Modell exportiert und offline verwendet werden.

### <a name="classification-and-object-detection"></a>Klassifizierung und Objekterkennung

Custom Vision bietet zwei Features: Die **Bildklassifizierung** wendet eine oder mehrere Bezeichnungen auf ein Bild an. Die **Objekterkennung** funktioniert ähnlich, gibt aber auch die Koordinaten zurück, an denen sich die angewendeten Bezeichnungen im Bild befinden.

### <a name="optimization"></a>Optimization

Der Custom Vision-Dienst ist für die schnelle Erkennung wesentlicher Unterschiede zwischen Bildern optimiert, sodass Sie anhand einer kleinen Datenmenge mit der Prototyperstellung für Ihr Modell beginnen können. 50 Bilder pro Bezeichnung sind im Allgemeinen ein guter Ausgangspunkt. Für die Erkennung geringfügiger Bildunterschiede (etwa kleinere Risse oder Dellen in Qualitätssicherungsszenarien) ist der Dienst dagegen weniger geeignet.

Darüber hinaus stehen verschiedene Varianten des Custom Vision-Algorithmus zur Verfügung, die jeweils für Bilder mit bestimmtem Material optimiert sind, z. B. für Wahrzeichen oder Einzelhandelsartikel. Weitere Informationen finden Sie in den Schnellstartanleitungen [Schnellstart: Erstellen einer Klassifizierung mit Custom Vision](getting-started-build-a-classifier.md) und [Schnellstart: Informationen zum Erstellen einer Objekterkennung mit Custom Vision](get-started-build-detector.md).

## <a name="what-it-includes"></a>Lieferumfang

Der Custom Vision-Dienst ist als Gruppe nativer SDKs sowie über eine webbasierte Oberfläche auf der [Custom Vision-Website](https://customvision.ai/) verfügbar. Beide Schnittstellen können einzeln oder zusammen zum Erstellen, Testen und Trainieren eines Modells verwendet werden.

![Custom Vision-Website in einem Chrome-Browserfenster](media/browser-home.png)

## <a name="data-privacy-and-security"></a>Datenschutz und Sicherheit

Wie bei allen Cognitive Services-Diensten müssen Entwickler, die den Custom Vision-Dienst nutzen, die Microsoft-Richtlinien zu Kundendaten beachten. Weitere Informationen finden Sie im Microsoft Trust Center auf der [Seite zu Cognitive Services](https://www.microsoft.com/trustcenter/cloudservices/cognitiveservices).

## <a name="next-steps"></a>Nächste Schritte

Unter [Schnellstart: Erstellen einer Klassifizierung mit Custom Vision](getting-started-build-a-classifier.md) werden die ersten Schritte mit Custom Vision im Webportal beschrieben. Sie können aber auch die Anleitungen im [Schnellstart: Erstellen eines Bildklassifizierungsprojekts mit der Custom Vision-Clientbibliothek](quickstarts/image-classification.md) absolvieren, um ein einfaches Szenario mit Code zu implementieren.
