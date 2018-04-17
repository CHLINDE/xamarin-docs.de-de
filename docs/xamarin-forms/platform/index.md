---
title: Plattformfeatures
description: Clientplattform-spezifische Funktionen mit Xamarin.Forms nutzen
ms.prod: xamarin
ms.assetid: 2C6CE42C-E380-4BB9-90CC-D0F4E60C4C03
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 12/20/2017
ms.openlocfilehash: fd46411f3662652ef26addc76f273d6071401a6f
ms.sourcegitcommit: bc39d85b4585fcb291bd30b8004b3f7edcac4602
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="platform-features"></a>Plattformfeatures

Xamarin.Forms ist erweiterbar und können Sie Sie integrieren Clientplattform-spezifische Funktionen, die mit [Effekte](~/xamarin-forms/app-fundamentals/effects/index.md), [benutzerdefinierten Renderer](~/xamarin-forms/app-fundamentals/custom-renderer/index.md), [DependencyService](~/xamarin-forms/app-fundamentals/dependency-service/index.md), die [MessagingCenter](~/xamarin-forms/app-fundamentals/messaging-center.md), und vieles mehr.

## <a name="androidandroidindexmd"></a>[Android](android/index.md)

Dieses Handbuch beschreibt die Material Entwurf zu implementieren, indem vorhandene Xamarin.Forms Android-apps aktualisieren.

## <a name="application-indexing-and-deep-linkingdeep-linkingmd"></a>[Anwendungsindizierung und Deep Linking](deep-linking.md)

Indizieren Sie die Anwendung ermöglicht Anwendungen, die andernfalls vergessen würde, nachdem ein Paar wird verwendet, um die relevanten bleiben, indem Sie in den Suchergebnissen angezeigt wird. Deep Links ermöglicht Anwendungen, die auf ein Suchergebnis reagieren, die Anwendungsdaten, in der Regel durch Navigieren zu einer Seite aus dem deep-Link enthält.

## <a name="device-classdevicemd"></a>[Geräteklasse](device.md)

Gewusst wie: Verwenden der `Device` Klasse, um plattformspezifische Verhalten im freigegebenen Code und die Benutzeroberfläche (einschließlich der Verwendung von XAML) zu erstellen. Deckt auch `BeginInvokeOnMainThread` Vorbereitung ist wichtig, beim Ändern von UI-Steuerelementen in Hintergrundthreads ausgeführt.

## <a name="iosiosindexmd"></a>[iOS](ios/index.md)

Einige iOS Styling ausgeführt werden kann, über **"Info.plist"** und `UIAppearance` API. Dieses Handbuch enthält Beispiele für iOS 9-Clientfeatures in der iOS-app von einer Xamarin.Forms-Projektmappe, einschließlich Core Spotlight-Suche.

## <a name="gtkgtkmd"></a>[GTK](gtk.md)

Xamarin.Forms verfügt jetzt über Preview-Unterstützung für GTK-apps.

## <a name="macmacmd"></a>[Mac](mac.md)

Xamarin.Forms verfügt jetzt über Preview-Unterstützung für Mac OS-apps.

## <a name="wpfwpfmd"></a>[WPF](wpf.md)

Xamarin.Forms verfügt jetzt über Preview-Unterstützung für Windows Presentation Foundation (WPF)-apps.

## <a name="native-formsnative-formsmd"></a>[Native Formulare](native-forms.md)

Systemeigene Forms zulassen Xamarin.Forms [ `ContentPage` ](https://developer.xamarin.com/api/type/Xamarin.Forms.ContentPage/)-abgeleitete Seiten von systemeigene universelle Windows-Plattform (UWP), Xamarin.iOS und Xamarin.Android Projekte verwendet wird.

## <a name="native-viewsnative-viewsindexmd"></a>[Native Ansichten](native-views/index.md)

Systemeigene Ansichten von iOS, Android und universellen Windows-Plattform können direkt von Xamarin.Forms verwiesen werden. Eigenschaften und Ereignishandler für systemeigene Sichten festgelegt werden können, und sie können mit Xamarin.Forms Sichten interagieren.

## <a name="platform-specificsplatform-specificsindexmd"></a>[Platform-Besonderheiten](platform-specifics/index.md)

Plattform Einzelheiten können Sie Funktionen zu nutzen, die nur auf eine bestimmte Plattform verfügbar ist ohne benutzerdefinierten Renderer oder Auswirkungen.

## <a name="pluginspluginsmd"></a>[Plug-Ins](plugins.md)

Stehen eine Vielzahl von Open-Source-Plug-ins auf Github, Nuget sowie der Komponentenspeicher Xamarin, um Xamarin.Forms-apps zu erweitern.

## <a name="windowswindowsindexmd"></a>[Windows](windows/index.md)

Xamarin.Forms verfügt über Unterstützung für vier verschiedene Typen von Windows-Projekt:

* Windows Phone 8 Silverlight (die ursprüngliche Windows-Plattform von Xamarin.Forms unterstützt)
* Windows Phone 8.1 (WinRT),
* Windows 8.1 (WinRT), und
* Universelle Windows-Plattform (Windows 10).

Dieser Abschnitt beschreibt die Unterschiede zwischen ihnen und wie sie eine vorhandene Xamarin.Forms-Projektmappe hinzuzufügen.
