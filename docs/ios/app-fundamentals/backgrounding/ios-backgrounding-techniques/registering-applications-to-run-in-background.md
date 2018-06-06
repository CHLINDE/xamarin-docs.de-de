---
title: Registrierung von Xamarin.iOS Anwendungen im Hintergrund ausgeführt.
description: Dieses Dokument beschreibt, wie zum Registrieren einer Anwendung Xamarin.iOS im Hintergrund ausgeführt wird. Es wird erläutert, Audio-apps, VoIP-apps, externe Zubehör und Bluetooth und vieles mehr.
ms.prod: xamarin
ms.assetid: 8F89BE63-DDB5-4740-A69D-F60AEB21150D
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/18/2017
ms.openlocfilehash: f4774f6b4f5412c44dc985bd40129a178b1e813c
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/05/2018
ms.locfileid: "34783674"
---
# <a name="registering-xamarinios-apps-to-run-in-the-background"></a>Registrierung von Xamarin.iOS Anwendungen im Hintergrund ausgeführt.

Registrieren Sie einzelne Aufgaben für den Hintergrund Berechtigungen funktioniert für einige Anwendungen, aber was geschieht, wenn eine Anwendung ständig aufgerufen wird, um wichtige, lang andauernde, Aufgaben wie das Abrufen von Anweisungen für den Benutzer über GPS? Solche Anwendungen sollte stattdessen als bekannte Hintergrund erforderlichen Anwendungen registriert werden.

Registrieren einer app für iOS-signalisiert, dass die Anwendung spezielle Berechtigungen zum Ausführen von Tasks im Hintergrund notwendig gewährt werden soll.

## <a name="application-registration-categories"></a>Registrierung Anwendungskategorien

Registrierten apps können in verschiedene Kategorien fallen:

-  **Audio** -Musik-Player und anderen Anwendungen, die mit Audioinhalte arbeiten möglicherweise registriert werden, um den Vorgang fortsetzen Audiowiedergabe auch wenn die app nicht mehr im Vordergrund ist. Wenn eine Anwendung in dieser Kategorie versucht, die als Play Audio- oder Download im Hintergrund keine Wirkung, wird es iOS beendet werden.
-  **VoIP** -Stimme über Internet Protocol (VoIP) Anwendungen abrufen, der den gleichen Berechtigungen für Audio / Anwendungen für die Verarbeitung von Audio im Hintergrund zu halten. Sie dürfen außerdem nach Ihren Anforderungen an die VoIP-Dienste zu reagieren, die sie, um ihre Verbindungen aufrechtzuerhalten power.
-  **Externe Zubehör und Bluetooth** -Registrierung unter dieser Kategorien für Anwendungen, die für die Kommunikation mit Bluetooth-Geräte und andere externe Hardwarezubehör reserviert, ermöglicht es der app auf Hardware verbunden bleiben.
-  **Newsstand** -Anwendung ein Newsstand kann weiterhin Inhalte im Hintergrund synchronisiert.
-  **Speicherort** - Anwendungen, die Stellen verwenden GPS oder Netzwerk-Standortdaten können senden und Empfangen von Updates Speicherort im Hintergrund.
-  **Abrufen von Daten (iOS 7 und höher)** – eine Anwendung, die registriert wird, für die Fetch-Berechtigungen im Hintergrund einen Anbieter für den neuen Inhalt überprüfen können, in regelmäßigen Abständen, die den Benutzer mit aktualisiertem Inhalt darstellen, wenn sie an die Anwendung zurückgegeben.
-  **Remote-Benachrichtigungen (iOS 7 und höher)** -Anwendungen können zum Empfangen von Benachrichtigungen von einem Anbieter registrieren und verwenden Sie die Benachrichtigung, um ein Update starten, bevor der Benutzer die Anwendung öffnet. Benachrichtigungen können in Form von Pushbenachrichtigungen stammen, oder abonnieren, um die Anwendung automatisch zu reaktivieren.


Anwendungen können registriert werden, durch Festlegen der **Hintergrundmodi erforderlich** Eigenschaft in der Anwendungsverzeichnis *"Info.plist"*. Zum Registrieren einer Anwendung kann so viele Kategorien benötigt wird:

 [![](registering-applications-to-run-in-background-images/bgmodes.png "Festlegen der hintergrundmodi")](registering-applications-to-run-in-background-images/bgmodes.png#lightbox)

Eine schrittweise Anleitung zum Registrieren einer Anwendung für Updates der Hintergrund-Speicherort, finden Sie unter der [Hintergrund Speicherort Exemplarische Vorgehensweise](~/ios/app-fundamentals/backgrounding/ios-backgrounding-walkthroughs/location-walkthrough.md).

## <a name="application-does-not-run-in-background-property"></a>Anwendung wird im Hintergrundeigenschaft nicht ausgeführt.

Eine andere Eigenschaft, die festgelegt werden kann, in *"Info.plist"* ist die *Anwendung wird nicht ausgeführt, im Hintergrund*, oder `UIApplicationExitsOnSuspend` Eigenschaft:

 [![](registering-applications-to-run-in-background-images/plist.png "Deaktivieren im Hintergrund ausgeführt wird")](registering-applications-to-run-in-background-images/plist.png#lightbox)

Dies ist genaue die gleiche Wirkung wie das Festlegen der App zu aktualisieren, im Hintergrund Einstellung Off in iOS 7 und höher, außer es kann nur auf der Seite Entwickler geändert werden und ist für iOS 4 und höher verfügbar. Die Anwendung sofort nach der Eingabe Hintergrund angehalten und wird nicht in der Lage, Verarbeitungsvorgänge ausführen.

Verwenden Sie diese Eigenschaft, wenn Ihre Anwendung nicht zur Unterstützung ist im Hintergrund zu verarbeiten konzipiert, wie sie die hilft, unerwartetes Verhalten zu vermeiden.

## <a name="background-fetch-and-remote-notifications"></a>Abrufen im Hintergrund und Remote-Benachrichtigungen

Abrufen im Hintergrund und remote-Benachrichtigungen sind besondere Registrierung Kategorien in iOS 7 eingeführt wurden. Diese Kategorien können Anwendungen zum neuen Inhalt von einem Anbieter empfangen und im Hintergrund aktualisieren. Im nächste Abschnitt wird erklärt, Fetch und remote Benachrichtigungen ausführlicher und führt auch Netzwerkadressinformationen als Mittel zum Aktualisieren einer Anwendung im Hintergrund auf iOS 6.
