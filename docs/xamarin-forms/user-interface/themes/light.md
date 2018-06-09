---
title: Xamarin.Forms hellen Design
description: Dieser Artikel beschreibt, wie Sie das Xamarin.Forms hellen Design in einer app nutzen.
ms.prod: xamarin
ms.assetid: D5D16AE3-F51F-4359-B37A-E1087ECE512B
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 09/01/2017
ms.openlocfilehash: 7f40e375d653acec60f8848627234ab46fcce8de
ms.sourcegitcommit: 66682dd8e93c0e4f5dee69f32b5fc5a96443e307
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/08/2018
ms.locfileid: "35245246"
---
# <a name="xamarinforms-light-theme"></a>Xamarin.Forms hellen Design

![](~/media/shared/preview.png "Diese API ist derzeit als Vorschau verfügbar")

> [!NOTE]
> Designs erfordern Xamarin.Forms 2.3 Preview-Release. Überprüfen Sie die [Tipps zur Problembehandlung](~/xamarin-forms/user-interface/themes/index.md) Wenn Fehler auftreten.

So verwenden Sie das Design "hell"

## <a name="1-add-nuget-packages"></a>1. Hinzufügen von NuGet-Paketen

* Xamarin.Forms.Theme.Base
* Xamarin.Forms.Theme.Light

## <a name="2-add-to-the-resource-dictionary"></a>2. Fügen Sie auf das Ressourcenwörterbuch hinzu

In der **App.xaml** Datei hinzufügen eine neue benutzerdefinierten `xmlns` für das Design, und vergewissern Sie sich dann mit das Design-Ressourcen mit der Anwendung Ressourcenverzeichnis zusammengeführt werden.
Eine Beispiel für XAML-Datei wird unten gezeigt:

```xaml
<?xml version="1.0" encoding="utf-8"?>
<Application xmlns="http://xamarin.com/schemas/2014/forms" xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" x:Class="EvolveApp.App"
             xmlns:light="clr-namespace:Xamarin.Forms.Themes;assembly=Xamarin.Forms.Theme.Light">
    <Application.Resources>
        <ResourceDictionary MergedWith="light:LightThemeResources" />
    </Application.Resources>
</Application>
```

## <a name="3-load-theme-classes"></a>3. Laden von designklassen

Führen Sie [Problembehandlung Schritt](~/xamarin-forms/user-interface/themes/index.md) und fügen Sie den erforderlichen Code in die IOS- und Android-Anwendungsprojekten.

## <a name="4-use-styleclass"></a>4. Verwenden Sie StyleClass

Hier ist ein Beispiel für Schaltflächen und Bezeichnungen in das Design "hell", zusammen mit das Markup, das sie erstellt.

[![](light-images/light-theme-sml.png "Schaltflächen und Bezeichnungen in das Design \"hell\"")](light-images/light-theme.png#lightbox "Schaltflächen und Bezeichnungen in das Design \"hell\"")

```xaml
<StackLayout Padding="20">
    <Button Text="Button Default" />
    <Button Text="Button Class Default" StyleClass="Default" />
    <Button Text="Button Class Primary" StyleClass="Primary" />
    <Button Text="Button Class Success" StyleClass="Success" />
    <Button Text="Button Class Info" StyleClass="Info" />
    <Button Text="Button Class Warning" StyleClass="Warning" />
    <Button Text="Button Class Danger" StyleClass="Danger" />
    <Button Text="Button Class Link" StyleClass="Link" />
    <Button Text="Button Class Default Small" StyleClass="Small" />
    <Button Text="Button Class Default Large" StyleClass="Large" />
</StackLayout>
```

Die [vollständige Liste der integrierten Klassen](~/xamarin-forms/user-interface/themes/index.md) zeigt, welche Formate für einige häufig verwendete Steuerelemente verfügbar sind.
