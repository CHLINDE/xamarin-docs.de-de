---
title: Eine Einführung in die SkiaSharp
description: Dies bietet eine kurze Einführung in die Konzepte hinter SkiaSharp
ms.prod: xamarin
ms.assetid: 19506F08-2603-465E-A806-6BD01638DE90
ms.technology: xamarin-cross-platform
author: charlespetzold
ms.author: chape
ms.date: 09/14/2017
ms.openlocfilehash: 0e5a0cbbf5490b0fa0ffaca9be40d8e9357fce5a
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="an-introduction-to-skiasharp"></a>Eine Einführung in die SkiaSharp

_Dies bietet eine kurze Einführung in die Konzepte hinter SkiaSharp_

SkiaSharp bietet eine umfassende und leistungsfähige 2D 3D-Grafik-API, die zum Rendern in 2D Puffer verwendet werden kann.  Sie können diese implementieren Sie benutzerdefinierte Elemente der Benutzeroberfläche und 2D Grafiken, die in der Anwendung integriert werden können.  SkiaSharp ist eine .NET Bindung an die [Skia](https://skia.org) Bibliothek und die Features und Leistungsfähigkeit von dieser Bibliothek erbt.

Die Bibliothek ist derzeit verfügbar ist, wie eine plattformübergreifende [NuGet-Paket](https://www.nuget.org/packages/SkiaSharp), indem Sie das NuGet-Verweis hinzufügen zum Projekt hinzufügen.

Zum Zeichnen der Code erstellt ein `SkCanvas` der beschrieben wird, der Oberfläche, in denen die Zeichenoperationen wirksam.

## <a name="obtaining-an-skcanvas"></a>Abrufen einer SKCanvas

```csharp
using (var surface = SKSurface.Create (width: 640, height: 480, SKImageInfo.PlatformColorType, SKAlphaType.Premul)) {
    SKCanvas myCanvas = surface.Canvas;

    // Your drawing code goes here.
}
```

## <a name="drawing-on-skcanvas"></a>Die Zeichnung SKCanvas

Die `SKCanvas` verwendet ein zeichnen Modell ähnlich wie ein Willen andere modelliert, dass Sie möglicherweise mit vertraut sind, Farben mit einer optionalen transparenzkanal verwendet und können Zeichnen von Linien, Bögen, Text und Bildern.

Im folgenden sind nur einige der viele verschiedene Aufgaben, die mit SkiaSharp erledigt werden können.  In den Beispielen unten die Variable `canvas` ist vom Typ SKCanvas.

### <a name="drawing-xamagon"></a>Zeichnen von Xamagon

In diesem Beispiel zeichnet die Xamarin Logo der Xamagon:

```csharp
// clear the canvas / fill with white
canvas.Clear (SKColors.White);

// set up drawing tools
using (var paint = new SKPaint ()) {
  paint.IsAntialias = true;
  paint.Color = new SKColor (0x2c, 0x3e, 0x50);
  paint.StrokeCap = SKStrokeCap.Round;

  // create the Xamagon path
  using (var path = new SKPath ()) {
    path.MoveTo (71.4311121f, 56f);
    path.CubicTo (68.6763107f, 56.0058575f, 65.9796704f, 57.5737917f, 64.5928855f, 59.965729f);
    path.LineTo (43.0238921f, 97.5342563f);
    path.CubicTo (41.6587026f, 99.9325978f, 41.6587026f, 103.067402f, 43.0238921f, 105.465744f);
    path.LineTo (64.5928855f, 143.034271f);
    path.CubicTo (65.9798162f, 145.426228f, 68.6763107f, 146.994582f, 71.4311121f, 147f);
    path.LineTo (114.568946f, 147f);
    path.CubicTo (117.323748f, 146.994143f, 120.020241f, 145.426228f, 121.407172f, 143.034271f);
    path.LineTo (142.976161f, 105.465744f);
    path.CubicTo (144.34135f, 103.067402f, 144.341209f, 99.9325978f, 142.976161f, 97.5342563f);
    path.LineTo (121.407172f, 59.965729f);
    path.CubicTo (120.020241f, 57.5737917f, 117.323748f, 56.0054182f, 114.568946f, 56f);
    path.LineTo (71.4311121f, 56f);
    path.Close ();

    // draw the Xamagon path
    canvas.DrawPath (path, paint);
  }
}
```

### <a name="drawing-text"></a>Zeichnen von Text

```csharp
// clear the canvas / fill with white
canvas.DrawColor (SKColors.White);

// set up drawing tools
using (var paint = new SKPaint ()) {
  paint.TextSize = 64.0f;
  paint.IsAntialias = true;
  paint.Color = new SKColor (0x42, 0x81, 0xA4);
  paint.IsStroke = false;

  // draw the text
  canvas.DrawText ("Skia", 0.0f, 64.0f, paint);
}
```

### <a name="drawing-bitmaps"></a>Zeichnen von Bitmaps

```csharp
Stream fileStream = File.OpenRead ("MyImage.png");

// clear the canvas / fill with white
canvas.DrawColor (SKColors.White);

// decode the bitmap from the stream
using (var stream = new SKManagedStream(fileStream))
using (var bitmap = SKBitmap.Decode(stream))
using (var paint = new SKPaint()) {
  canvas.DrawBitmap(bitmap, SKRect.Create(Width, Height), paint);
}
```

### <a name="drawing-with-image-filters"></a>Zeichnen mit Image-Filter

```csharp
Stream fileStream = File.OpenRead ("MyImage.png"); // open a stream to an image file

// clear the canvas / fill with white
canvas.DrawColor (SKColors.White);

// decode the bitmap from the stream
using (var stream = new SKManagedStream(fileStream))
using (var bitmap = SKBitmap.Decode(stream))
using (var paint = new SKPaint()) {
  // create the image filter
  using (var filter = SKImageFilter.CreateBlur(5, 5)) {
    paint.ImageFilter = filter;

    // draw the bitmap through the filter
    canvas.DrawBitmap(bitmap, SKRect.Create(width, height), paint);
  }
}
```

# <a name="more-information"></a>Weitere Informationen

Weitere Informationen zum Verwenden von SkiaSharp befinden sich auf die [online-API-Dokumentation](https://developer.xamarin.com/api/namespace/SkiaSharp/)


## <a name="related-links"></a>Verwandte Links

- [SkiaSharp iOS Arbeitsmappe](https://developer.xamarin.com/workbooks/graphics/skiasharp/logo/skialogo-ios.workbook)
