---
title: Xamarin.Mac-Linkeroptionen
description: "Verknüpfen ist ein leistungsstarkes Optimierungstool, das die Größe Ihrer Anwendung verringert, indem nicht verwendeter Code entfernt wird."
ms.topic: article
ms.prod: xamarin
ms.assetid: F03176C3-F8D4-4DE8-870C-7F27D8CE525A
ms.technology: xamarin-mac
author: bradumbaugh
ms.author: brumbaug
ms.date: 11/10/2017
ms.openlocfilehash: bee5f86682048fcd72d2212706c188c894eb148a
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2018
---
# <a name="xamarinmac-linker-options"></a>Xamarin.Mac-Linkeroptionen

_Verknüpfen ist ein leistungsstarkes Optimierungstool, das die Größe Ihrer Anwendung verringert, indem nicht verwendeter Code entfernt wird._

## <a name="overview"></a>Übersicht

Die verfügbaren Linkeroptionen können auf Grundlage des [Zielframeworks](~/mac/platform/target-framework.md), das Ihr Projekt verwendet, eingeschränkt sein. Dies ist darauf zurückzuführen, dass für die Verknüpfung die Erstellung eines Objektgraphs von jedem von Ihrer Anwendung verwendeten Typ erforderlich ist. Für „Full“ (vollständig) (oder „Unsupported“ – Nicht unterstützt) ist dies aufgrund von „System.Configuration“ nicht möglich.

Es gibt vier Möglichkeiten:

- **Keine** – Deaktiviert alle Verknüpfungen. Standard bei der Debugkonfiguration in Modern und allen Konfiguration in Full (vollständig)
- **SDK**: Verknüpft alle SDK-Assemblys (Benutzerassemblys ausgenommen). Standard in der Releasekonfiguration in Modern. Für „Full“ (vollständig) nicht verfügbar.
- **Full** (vollständig): Verknüpfen aller Assemblys. Dies erfordert, dass Benutzercode für den Linker sicher ist. Weitere Informationen finden Sie in den [Anmerkungen](~/ios/deploy-test/linker.md). Für „Full“ (vollständig) nicht verfügbar.
- **Plattform**: Verknüpft nur „Xamarin.Mac.dll“. Details finden Sie weiter unten.

## <a name="platform-linking"></a>Plattformverknüpfung

Das Verknüpfen von Anwendungen mithilfe des [Zielframeworks](~/mac/platform/target-framework.md) „Full“ ist in der Regel nicht sicher. In einigen Fällen ist jedoch eine eingeschränkte Form des Verknüpfens erforderlich.

Anwendungen, die z.B. an den macOS App Store übermittelt werden, dürfen auf keine verwalteten APIs (wie etwa QTKit) verweisen, von denen Xamarin.Mac Bindungen enthält. Auch wenn eine Anwendung diese Bindungen nicht aufruft, ist der Aufruf jedoch im SDK vorhanden und wird abgelehnt.

Die Plattformverknüpfung geht davon aus, dass die Anwendung und BCL nicht sicher für den Linker sind und entfernt nicht verwendeten Code aus „Xamarin.Mac.dll“. 

Alle Anwendungen, die sich nicht auf Xamarin.Mac.dll-Typen beziehen, erfahren eine geringe Leistungsverbesserung beim Start durch die Entfernung unnötiger Typen.

Die Plattformverknüpfung eignet sich in der Regel nur für Anwendung, die das Full-Zielframework verwenden, da die Modern-Anwendung die leistungsstärkere SDK-Option verwenden kann.

## <a name="setting-the-linker-configuration"></a>Festlegen der Linkerkonfiguration

Um zur Linkerkonfiguration für ein Xamarin.Mac-Projekt zu wechseln, führen Sie folgende Schritte aus:

1. Öffnen Sie das Xamarin.Mac-Projekt in Visual Studio für Mac.
2. Doppelklicken Sie auf die Projektdatei im **Projektmappen-Explorer**, um die **Projektoptionen** zu öffnen.
3. Wählen Sie auf der Registerkarte **Mac-Build** den Typ des **Linkerverhaltens**, der am besten zu Ihrer Anwendung passt:

  ![Auswählen des zu verwendenden Linkerverhaltens](linker-images/link-behavior.png "Choose which linker behavior to use")

4. Die Plattformverknüpfung für Full-Zielframeworks wird erst in einem späteren Update zur IDE hinzugefügt. Fügen Sie bis dahin stattdessen den **zusätzlichen mmp-Argumenten** `--linkplatform` hinzu.
5. Klicken Sie auf **OK**, um die Änderungen zu speichern.


## <a name="related-links"></a>Verwandte Links

- [Linking on iOS (Verknüpfung unter iOS)](~/ios/deploy-test/linker.md)
