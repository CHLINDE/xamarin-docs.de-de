---
title: Arbeiten mit WatchOS App-Gruppen in Xamarin
description: Dieses Dokument beschreibt app-Gruppen und deren Verwendung in einer Anwendung WatchOS. Es wird erläutert, wie eine app-Verwaltungsgruppe, die Bereitstellung von Anforderungen, Entitlements.plist Überlegungen und die Bereitstellung konfigurieren.
ms.prod: xamarin
ms.technology: xamarin-ios
ms.assetid: 6968606B-C287-424F-A321-2492E12BC0BB
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/17/2017
ms.openlocfilehash: 5736b25af3993e2da794422a1a6f040461532497
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/05/2018
ms.locfileid: "34790678"
---
# <a name="working-with-watchos-app-groups-in-xamarin"></a>Arbeiten mit WatchOS App-Gruppen in Xamarin


Durch eine App-Gruppe können unterschiedliche Anwendungen (oder eine Anwendung und ihre Erweiterungen) auf einen freigegebenen Dateispeicherort zugreifen. App-Gruppen können für folgende Daten verwendet werden:

- Apple Watch [Einstellungen](~/ios/watchos/app-fundamentals/settings.md).
- Freigegebene [NSUserDefaults](~/ios/watchos/app-fundamentals/parent-app.md#nsuserdefaults).
- Freigegebene [Dateien](~/ios/watchos/app-fundamentals/parent-app.md#files).

## <a name="configure-an-app-group"></a>Konfigurieren Sie ein App-Gruppe

Mit der freigegebene Speicherort konfiguriert ein [App-Gruppe](https://developer.apple.com/library/ios/documentation/Miscellaneous/Reference/EntitlementKeyReference/Chapters/EnablingAppSandbox.html#//apple_ref/doc/uid/TP40011195-CH4-SW19), die konfiguriert ist, der **Zertifikate "," Bezeichner "und" Profile** Abschnitt [iOS Dev Center](https://developer.apple.com/devcenter/ios/). Dieser Wert muss auch in jedem Projekt verwiesen werden **Entitlements.plist**.

### <a name="provisioning"></a>Bereitstellung

Die app-Gruppe hat einen Bezeichner zeigen, die in der Regel die Paket-ID ist mit einem `group.` Präfix. Beispielsweise können wir die Paket-ID `com.xamarin.WatchSettings` und die app-Gruppe `group.com.xamarin.WatchSettings`.

[![](app-groups-images/app-group-sml.png "Verwenden Sie die Paket-ID com.xamarin.WatchSettings und group.com.xamarin.WatchSettings der app-Gruppe")](app-groups-images/app-group.png#lightbox)

### <a name="entitlementsplist"></a>Entitlements.plist

Sowie die provisioning-Profil konfigurieren **App-Gruppen aktivieren** in der **Entitlements.plist** und geben Sie die ID, die Sie ausgewählt haben:

[![](app-groups-images/entitlements-sml.png "Konfigurieren Sie die Plist, und geben Sie die ID")](app-groups-images/entitlements.png#lightbox)


### <a name="deployment"></a>Bereitstellung

Stellen Sie sicher, konfigurieren Sie die App-Gruppe, die in Ihrem [Bereitstellung](~/ios/watchos/deploy-test/index.md#App_Groups) bereitstellen.


Weitere Informationen finden Sie unter der [App Gruppenverwaltungsfunktionen](~/ios/deploy-test/provisioning/capabilities/app-groups-capabilities.md) Dokumentation.


## <a name="related-links"></a>Verwandte Links

- [Apple Freigeben von Daten mit der enthaltenden App](https://developer.apple.com/library/ios/documentation/General/Conceptual/ExtensibilityPG/ExtensionScenarios.html)
- [Apple App-Gruppe doc](https://developer.apple.com/library/ios/documentation/Miscellaneous/Reference/EntitlementKeyReference/Chapters/EnablingAppSandbox.html#//apple_ref/doc/uid/TP40011195-CH4-SW19)
