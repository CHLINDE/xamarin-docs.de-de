---
title: UrhoSharp Mac-Unterstützung
description: Bestimmte Mac-Setup und Funktionen für UrhoSharp.
ms.prod: xamarin
ms.assetid: 95FFBD36-14E9-4C17-B1E8-9A04E81E824D
ms.technology: xamarin-cross-platform
author: charlespetzold
ms.author: chape
ms.date: 03/29/2017
ms.openlocfilehash: ed396097f55f5f4a2f8a3b718b324919d0f8daea
ms.sourcegitcommit: 775a7d1cbf04090eb75d0f822df57b8d8cff0c63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="urhosharp-mac-support"></a>UrhoSharp Mac-Unterstützung

_Bestimmte Mac-Setup und Funktionen_

Während Urho eine portable Klassenbibliothek ist, und ermöglicht die gleiche API über die verschiedenen Plattform verwendet werden, für die Spiellogik Sie weiterhin Urho in Ihren jeweiligen Treiber, Plattform und in einigen Fällen zu initialisieren müssen, sollten Sie bestimmte Funktionen der Plattform nutzen .

In den nachfolgenden Seiten wird angenommen, dass `MyGame` ist eine Unterklasse von der `Application` Klasse.

## <a name="macos"></a>macOS

**Unterstützte Architekturen:** X86/x86-64 für 32-Bit und 64-Bit.

## <a name="creating-a-project"></a>Erstellen eines Projekts

Erstellen eines Konsolenprojekts, verweisen die Urho NuGet, und stellen Sie sicher, dass Sie die Ressourcen (die Verzeichnisse, die das Datenverzeichnis enthält) zugreifen können.

```csharp
DesktopUrhoInitializer.AssetsDirectory = "../Assets";
new MyGame().Run();
```

## <a name="example"></a>Beispiel

[Vollständiges Beispiel](https://github.com/xamarin/urho-samples/tree/master/FeatureSamples/Cocoa)


