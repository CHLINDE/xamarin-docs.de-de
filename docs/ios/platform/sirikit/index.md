---
title: SiriKit
description: "Dieser Artikel zeigt, wie SiriKit in einem Xamarin.iOS-app verwenden, um Dienste bereitzustellen, die für den Benutzer mithilfe von Siri auf einem iOS-Gerät zugänglich sind."
ms.topic: article
ms.prod: xamarin
ms.assetid: 4E1FF652-28F0-4566-B383-9D12664401A4
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/16/2017
ms.openlocfilehash: c4fdf61b35ca28af82e3890242d54a75e50d2f82
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2018
---
# <a name="sirikit"></a>SiriKit

_Dieser Artikel zeigt, wie SiriKit in einem Xamarin.iOS-app verwenden, um Dienste bereitzustellen, die für den Benutzer mithilfe von Siri auf einem iOS-Gerät zugänglich sind._

Neue iOS 10, SiriKit ermöglicht eine iOS-app, um Dienste bereitzustellen, die für den Benutzer mithilfe von Siri und die Maps-app auf einem iOS-Gerät mithilfe von App-Erweiterungen und die neue zugänglich sind **Intents** und **Intents UI** Frameworks.

Siri funktioniert mit dem Konzept der **Domänen**, Gruppen von wissen Aktionen für verwandte Aufgaben. Jede Aktivität, die eine app mit Siri besitzt muss wie folgt in einen bekannten Dienst Domäne fallen:

- Audio oder video aufrufen.
- Buchung eine fuhr an.
- Verwalten von Training.
- Messaging.
- Suchen Fotos.
- Senden oder Empfangen von Zahlungen.

Wenn der Benutzer eine Anforderung Siri im Zusammenhang mit einer der Dienste für eine App-Erweiterung stellt, sendet SiriKit die Erweiterung ein **Absicht** -Objekt, das der Benutzer-Anforderung sowie alle unterstützungsdaten beschreiben. Die App-Erweiterung generiert dann das entsprechende **Antwort** -Objekt für den angegebenen **Absicht**, mit Details wie die Erweiterung für die Anforderung verarbeiten kann.

## <a name="understanding-sirikit-conceptsiosplatformsirikitunderstanding-sirikitmd"></a>[Grundlegendes zu SiriKit-Konzepten](~/ios/platform/sirikit/understanding-sirikit.md)

Dieser Artikel behandelt die grundlegenden Konzepte, die für das Arbeiten mit SiriKit in einer app Xamarin.iOS benötigt werden. Er behandelt die neue Intents und UI-Erweiterungspunkte Intents und deren Funktionsweise mit App "und" Benutzer Vokabular ", um eine app auf Siri öffnen.

## <a name="implementing-sirikitiosplatformsirikitimplementing-sirikitmd"></a>[Implementieren von SiriKit](~/ios/platform/sirikit/implementing-sirikit.md)

Dieser Artikel behandelt die erforderlichen Schritte zum SiriKit-Unterstützung in einem Xamarin.iOS-apps zu implementieren. Der Entwickler sollte die im Handbuch "Grundlegendes zu SiriKit Konzepten" oben lesen, vor dem SiriKit Unterstützung an eine app, als Schlüssel, die Konzepte behandelt werden hinzugefügt, die für die erfolgreiche Implementierung benötigt werden.





## <a name="related-links"></a>Verwandte Links

- [ElizaChat-Beispiel](https://developer.xamarin.com/samples/monotouch/ios10/ElizaChat/)
- [Programmierhandbuch SiriKit](https://developer.apple.com/library/prerelease/content/documentation/Intents/Conceptual/SiriIntegrationGuide/index.html)
- [Intents Frameworkverweis](https://developer.apple.com/reference/intents)
- [Referenz zur Benutzeroberfläche des Framework Intents](https://developer.apple.com/reference/intentsui)
