---
title: Stile
description: Mithilfe von Stilen Darstellung anpassen
ms.topic: article
ms.prod: xamarin
ms.assetid: 344A34AA-B19A-4765-BC8A-875D9A6B5EA8
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 02/17/2016
ms.openlocfilehash: 934948579e5f3fb19c7afe49f4e86a1ef255b77f
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2018
---
# <a name="styles"></a>Stile

## <a name="introductionintroductionmd"></a>[Introduction (Einführung)](introduction.md)

Xamarin.Forms-Anwendungen enthalten häufig mehrere Steuerelemente, die eine identische Darstellung haben. Die Darstellung der einzelnen Steuerelemente festlegen kann sich wiederholende und fehleranfällig. Stattdessen können Stile erstellt werden, die Darstellung anpassen Gruppierung und legt die Eigenschaften für den Steuerelementtyp "verfügbar.

## <a name="explicit-stylesexplicitmd"></a>[Explizite Stile](explicit.md)

Ein *explizite* Stil ist eine, die selektiv auf Steuerelemente angewendet wird, durch Festlegen von deren [ `Style` ](https://developer.xamarin.com/api/property/Xamarin.Forms.VisualElement.Style/) Eigenschaften.

## <a name="implicit-stylesimplicitmd"></a>[Impliziten Stilen](implicit.md)

Ein *implizite* Stil ist eine, die von allen Steuerelementen des gleichen verwendet wird [ `TargetType` ](https://developer.xamarin.com/api/property/Xamarin.Forms.Style.TargetType/), ohne dass jedes Steuerelement auf den Stil zu verweisen.

## <a name="global-stylesapplicationmd"></a>[Die globalen Formatvorlagen](application.md)

Stile verfügbar gemacht werden global von der Anwendungsverzeichnis hinzugefügt [ `ResourceDictionary` ](https://developer.xamarin.com/api/type/Xamarin.Forms.ResourceDictionary/). Dies hilft, um Formatvorlagen auf Seiten oder Steuerelemente Rechnung zu tragen.

## <a name="style-inheritanceinheritancemd"></a>[Stil-Vererbung](inheritance.md)

Stile können von anderen Formatvorlagen Duplizierung zu reduzieren, und aktivieren die Wiederverwendung erben.

## <a name="dynamic-stylesdynamicmd"></a>[Dynamische Formate](dynamic.md)

Stile nicht reagieren auf eigenschaftenänderungen, und für die Dauer einer Anwendung unverändert bleiben. Allerdings können Anwendungen auf Änderungen an Formatvorlagen zur Laufzeit dynamisch zu reagieren, dynamische Ressourcen nutzen.

## <a name="device-stylesdevicemd"></a>[Geräte-Stile](device.md)

Xamarin.Forms enthält sechs *dynamische* Formatvorlagen, bekannt als *Gerät* Stile, in der [ `Devices.Styles` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Device+Styles/) Klasse. Alle sechs Formatvorlagen können angewendet werden, um [ `Label` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Label/) nur Instanzen.
