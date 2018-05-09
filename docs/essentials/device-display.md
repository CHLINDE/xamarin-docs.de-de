---
title: Xamarin.Essentials Geräteinformationen anzeigen
description: Die DeviceDisplay-Klasse enthält Informationen zu dem Gerät Bildschirm Metriken, die Anwendung ausgeführt wird.
ms.assetid: 2821C908-C613-490D-8E8C-1BD3269FCEEA
ms.technology: xamarin-crossplatform
author: jamesmontemagno
ms.author: jamont
ms.date: 05/04/2018
ms.openlocfilehash: 4e78d0d22ee0766bbccdcd1617003cc9d0ccd73c
ms.sourcegitcommit: 46d3c9daa45350bdd536d9e105517f3c1c753c5b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2018
---
# <a name="xamarinessentials-device-display-information"></a>Xamarin.Essentials Geräteinformationen anzeigen

![Vorabversion NuGet](~/media/shared/pre-release.png)

Die **DeviceDisplay** -Klasse stellt Informationen über das Gerät Bildschirm Metriken, die die Anwendung ausgeführt wird.

## <a name="using-devicedisplay"></a>Verwenden von DeviceDisplay

Fügen Sie einen Verweis auf Xamarin.Essentials in Ihrer Klasse hinzu:

```csharp
using Xamarin.Essentials;
```

## <a name="screen-metrics"></a>Bildschirm Metriken

Zusätzlich zu den grundlegenden Geräteinformationen der **DeviceDisplay** -Klasse enthält Informationen über den Bildschirm und die Ausrichtung des Geräts.

```csharp
// Get Metrics
var metrics = DeviceDisplay.ScreenMetrics;

// Orientation (Landscape, Portrait, Square, Unknown)
var orientation = metrics.Orientation;

// Rotation (0, 90, 180, 270)
var rotation = metrics.Rotation;

// Width (in pixels)
var width = metrics.Width;

// Height (in pixels)
var height = metrics.Height;

// Screen density
var density = metrics.Density;
```

Die **DeviceDisplay** Klasse auch verfügbar macht und jedes öffentliche Ereignis, die abonniert werden kann, die ein Ereignis aus, wenn eine metrische Änderungen Bildschirm auslöst:

```csharp
public class ScreenMetricsTest
{
    public ScreenMetricsTest()
    {
        // Subscribe to changes of screen metrics
        DeviceDisplay.ScreenMetricsChanaged += OnScreenMetricsChanged;
    }

    void OnScreenMetricsChanged(ScreenMetricsChanagedEventArgs  e)
    {
        // Process changes
        var metrics = e.Metrics;
    }
}
```

## <a name="api"></a>API

- [DeviceDisplay-Quellcode](https://github.com/xamarin/Essentials/tree/master/Essentials/DeviceDisplay)
- [DeviceDisplay API-Dokumentation](xref:Xamarin.Essentials.DeviceDisplay)
