---
title: Internationalisierung Codierungen in Xamarin.iOS
description: Dieses Dokument beschreibt die Internationalisierung Codierungen in Xamarin.iOS, erläutern die verfügbaren Codierungen und wie sie eine app hinzugefügt.
ms.prod: xamarin
ms.assetid: F5117294-28BB-4583-B6A0-A339B050FDE1
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.openlocfilehash: 4963b0f95ae48ee56462a82d2f82a8dcaa231a23
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/05/2018
ms.locfileid: "34784125"
---
# <a name="internationalization-encodings-in-xamarinios"></a>Internationalisierung Codierungen in Xamarin.iOS

Nicht alle Codierungen sind in der Klassenbibliothek Xamarin.iOS standardmäßig eingeschlossen.

Zum Reduzieren der Größe der Anwendung Xamarin.iOS umfasst jedoch nicht den speziellen Codierung, und Sie weisen Mtouch enthalten die Assemblys, die die Unterstützung für die Codierung, die Sie benötigen.

Dies geschieht durch Auswählen von zusätzlichen Codierungen aus dem Bereich des iOS-Builds/erweiterte in Visual Studio für Mac oder Visual Studio:

 [![](encodings-images/00.png "Die zusätzlichen Codierungen auswählen")](encodings-images/00.png#lightbox)

 [![](encodings-images/00a.png "Die zusätzlichen Codierungen auswählen")](encodings-images/00a.png#lightbox)

Sie können eine der folgenden auswählen:

-  CJK-Schriftarten: für Chineese, Japanisch und Koreanisch
-  Naher Osten: Arabisch und Hebräisch, Türkisch Latin5.
-  andere: Kyrillisch, Baltisch, Vietnamesisch, Ukrainisch und Thai
-  seltenen: EBCDIC-Codierungen und anderen seltenen Codepages
-  West: lateinischen Sprachen, Ostern und Westeuropäisch
-  alle


 <a name="cjk" />


## <a name="cjk"></a>CJK-Schriftarten

-  CP51932
-  CP932
-  CP936
-  CP949
-  CP950
-  CP54936


 <a name="mideast" />


## <a name="mideast"></a>Naher Osten

-  CP1254
-  CP1255
-  CP1256
-  CP28596
-  CP28598
-  CP28599
-  CP38598


 <a name="other" />


## <a name="other"></a>Andere

-  CP1251
-  CP1257
-  CP1258
-  CP20866
-  CP21866
-  CP28594
-  CP28595
-  CP57002
-  CP874


 <a name="rare" />


## <a name="rare"></a>seltenen

-  CP1026
-  CP1047
-  CP1140
-  CP1141
-  CP1142
-  CP1143
-  CP1144
-  CP1145
-  CP1146
-  CP1147
-  CP1148
-  CP1149
-  CP20273
-  CP20277
-  CP20278
-  CP20280
-  CP20284
-  CP20285
-  CP20290
-  CP20297
-  CP20420
-  CP20424
-  CP20871
-  CP21025
-  CP37
-  CP500
-  CP708
-  CP852
-  CP855
-  CP857
-  CP858
-  CP862
-  CP864
-  CP866
-  CP869
-  CP870
-  CP875


 <a name="west" />


## <a name="west"></a>West

-  CP10000
-  CP10079
-  CP1250
-  CP1252
-  CP1253
-  CP28592
-  CP28593
-  CP28597
-  CP28605
-  CP437
-  CP850
-  CP860
-  CP861
-  CP863
-  CP865

