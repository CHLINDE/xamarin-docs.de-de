---
title: Binden von systemeigenen Frameworks
description: Dieses Dokument beschreibt, wie Objective Sharpie des - Framework-Option, um eine Bindung an eine Bibliothek erstellen, die als Framework verteilt.
ms.prod: xamarin
ms.assetid: 91AE058A-3A1F-41A9-9DE4-4B96880A1869
author: asb3993
ms.author: amburns
ms.date: 01/15/2016
ms.openlocfilehash: 02ee21ce58ecf945893f7e4f94763731abe92018
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/05/2018
ms.locfileid: "34781444"
---
# <a name="binding-native-frameworks"></a>Binden von systemeigenen Frameworks

In einigen Fällen wird eine systemeigene Bibliothek als verteilt eine [Framework](https://developer.apple.com/library/mac/documentation/MacOSX/Conceptual/BPFrameworks/Concepts/WhatAreFrameworks.html). Objektive Sharpie bietet eine Annehmlichkeit für Frameworks über Bindung ordnungsgemäß definiert werden. die `-framework` Option.

Binden Sie z. B. die [Adobe Creative SDK Framework](https://creativesdk.adobe.com/downloads.html) für iOS einfach ist:

<pre>$ <b>sharpie bind \
    -framework AdobeCreativeSDKFoundation.framework \
    -sdk iphoneos8.1</b></pre>

In einigen Fällen wird ein Framework geben einen **"Info.plist"** für welche SDK das Framework womit kompiliert werden soll. Wenn diese Informationen vorhanden ist und keine explizite `-sdk` Option übergeben wird, Ziel Sharpie wird aus der Frameworks ableiten **"Info.plist"** (entweder die `DTSDKName` Schlüssel oder eine Kombination der `DTPlatformName` und `DTPlatformVersion`Schlüssel).

Die `-framework` Option lässt keine explizite Headerdateien übergeben werden. Die Dach-Headerdatei wird gemäß der Konvention basierend auf den Namen des ausgewählt wird. Wenn ein übergeordneter-Header wurde nicht gefunden, Ziel Sharpie versucht nicht, um das Framework zu binden und Sie die Bindung manuell ausführen müssen, durch die Bereitstellung der richtigen Schirm-Header-Dateien zusammen mit Framework Argumente für die Clang analysiert (z. B. die `-F`Framework Suchoption-Pfad).

Hinter den Kulissen angeben `-framework` ist lediglich eine Kurzform. Die folgenden Argumente für die Bindung sind identisch mit der `-framework` Kurzschreibweise oben.
Ist von besonderer Bedeutung der `-F .` Framework Suchpfad bereitgestellt, um Clang (Beachten Sie den Speicherplatz und den Zeitraum, die als Teil des Befehls erforderlich sind).

<pre>$ <b>sharpie bind \
    -sdk iphoneos8.1 \
    AdobeCreativeSDKFoundation.framework/Headers/AdobeCreativeSDKFoundation.h \
    -scope AdobeCreativeSDKFoundation.framework/Headers \
    -c -F .</b></pre>

