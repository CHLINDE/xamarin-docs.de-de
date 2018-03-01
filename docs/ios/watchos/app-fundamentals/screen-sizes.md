---
title: "Arbeiten mit Bildschirmgrößen"
ms.topic: article
ms.prod: xamarin
ms.assetid: 156D6D1C-83CA-4088-BA08-40B22312269C
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/17/2017
ms.openlocfilehash: c64e5821c1067b64caf3afc85c0e290a354e914d
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2018
---
# <a name="working-with-screen-sizes"></a>Arbeiten mit Bildschirmgrößen

Apple Watch ist in zwei Bildschirmgrößen verfügbar:

- **38mm**
  - 136 x 170 logische Pixel (272 x 340 physischen Pixel)

- **42mm**
  - 156 x 195 logische Pixel (312 x 390 physischen Pixel).

Sie sollten Bildschirmgröße beim Entwerfen und Testen Ihre apps berücksichtigen.

## <a name="watchos-interface-designer"></a>WatchOS Benutzeroberflächen-Designer

In der Standardeinstellung Visual Studio für Mac-Designer zeigt beobachten Schnittstelle Domänencontroller am **Any Apple Watch**.

![](screen-sizes-images/screen-any-sml.png "Zeigt der Designer beobachten Schnittstelle Domänencontroller am Any Apple Watch")

Verwenden Sie die Größe im Menü Bearbeiten und eine Vorschau des Storyboards auf eines der verfügbaren Bildschirmgrößen: **38mm** oder **42mm**:

![](screen-sizes-images/screen-menu-sml.png "Die Größe der 38mm oder 42mm auswählen")

Größere Bildschirmgröße werden manchmal Inhalt gerendert, die auf den kleineren Bildschirm abgeschnitten/ausgeblendet sind.
Achten Sie darauf, dass Sie auf beiden Größen zu testen.


### <a name="interface-design"></a>Schnittstellenentwurf

Ihre app sollte den gleichen Inhalt auf dem Bildschirm, unabhängig von der Größe, angezeigt und sollte erweitern oder Elemente nach Bedarf. Sie sollten in der Visual Studio für Mac-Designer, in dem Inspektor Attribut verwenden **relativ zum Container** oder **Größe an Inhalt anpassen** aufrufanweisung feste Größen.

![](screen-sizes-images/sizeattributepanel-sml.png "Verwenden Sie aufrufanweisung feste Größen relativ zu dem Container oder Größe an Inhalt anpassen")

Da auf der Bildschirm überwachen durch einen schwarzen here umgeben ist, wird das Bereitstellen des Abstands um Ihre Schnittstelle nicht empfohlen. Können Sie Elemente für den Rand des Bildschirms bewegen, und lassen die here einen natürlichen Rahmen um die app zu bilden.


## <a name="watchos-simulator"></a>WatchOS Simulator

Wenn im Emulator testen kann problemlos zwischen den zwei Bildschirmgrößen mithilfe der **Hardware > Gerät** Menü.

![](screen-sizes-images/simulator.png "Der Simulator kann zwischen den zwei Bildschirmgrößen mithilfe des Menüs Hardwaregerät wechseln.")


## <a name="image-resources"></a>Bildressourcen

Sie sollten mehrere Bildanlagen verwenden, wenn es sich bei einem einzelnen Medienobjekt mit unterschiedlichen Größen nicht optimal ist. Bild Asset Kataloge zulassen für separate Bitmaps für jede Größe angegeben werden:

![](screen-sizes-images/images-xcassets.png "Bildbearbeitung Asset-Katalog")

```csharp
// specify the asset name, the correct size will automatically be loaded
staticImage.SetImage(UIImage.FromBundle("Walkway"));
```

Alternativ können Sie per Code bestimmen die Größe des Bildschirms und verschiedene Bilder zu laden:

```csharp
bool large = WKInterfaceDevice.CurrentDevice.ScreenBounds.Size.Width > 136.0;
// Load image depending on screen size
using (var image = UIImage.FromBundle (large ? "42mm-Walkway" : "38mm-Walkway"))
{
   myImage.SetImage (image);

}
```

Weitere Informationen zum Verwenden der [Bild-Steuerelement](~/ios/watchos/user-interface/image.md).



## <a name="related-links"></a>Verwandte Links

- [Einführung in die WatchOS 3](~/ios/watchos/platform/introduction-to-watchos3/index.md)
