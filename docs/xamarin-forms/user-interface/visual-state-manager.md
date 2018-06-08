---
title: Xamarin.Forms Visual-Status-Manager
description: Verwenden Sie den visuellen Status-Manager, um Änderungen an XAML-Elementen, die basierend auf visuelle Zustände, die im Code festgelegt.
ms.prod: xamarin
ms.assetid: 17296F14-640D-484B-A24C-A4E9B7013E4F
ms.technology: xamarin-forms
ms.custom: xamu-video
author: charlespetzold
ms.author: chape
ms.date: 05/07/2018
ms.openlocfilehash: 3c0330d8d6d07112350db007d0500d57c236dc24
ms.sourcegitcommit: d80d93957040a14b4638a91b0eac797cfaade840
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2018
ms.locfileid: "34848023"
---
# <a name="the-xamarinforms-visual-state-manager"></a>Xamarin.Forms Visual-Status-Manager

_Verwenden Sie den visuellen Status-Manager, um Änderungen an XAML-Elementen, die basierend auf visuelle Zustände, die im Code festgelegt._

Visuellen Status-Manager (VSM) ist in Xamarin.Forms 3.0 neu. VSM bietet ein strukturiertes Verfahren visuelle Änderungen an der Benutzeroberfläche aus Code vornehmen. In den meisten Fällen wird die Benutzeroberfläche der Anwendung in XAML definiert und diesen XAML-Code enthält Markup, die beschreiben, wie die visuellen Status-Manager die visuellen Elemente der Benutzeroberfläche auswirkt.

VSM führt das Konzept der _visuelle Zustände_. Eine Xamarin.Forms-Sicht, z. B. eine `Button` kann mehrere unterschiedliche visuelle Darstellungen aufweisen, abhängig von der zugrunde liegende &mdash; gibt an, ob es deaktiviert ist, oder gedrückt oder hat den Eingabefokus. Hierbei handelt es sich um die Schaltfläche Status.

Visuelle Zustände werden gesammelt, im _visuellen Zustandsgruppen_. Das visuelle Zustände innerhalb einer Gruppe visuellen Zustands schließen sich gegenseitig aus. Visuelle Zustände und visuellen Zustandsgruppen werden durch einfache Textzeichenfolgen identifiziert.

Der Xamarin.Forms visuellen Status-Manager definiert einen visuellen Zustands-Gruppe, die mit dem Namen "CommonStates" mit drei visuelle Zustände:

- "Normal"
- "Disabled"
- "Mit Fokus"

Diese Gruppe visuellen Zustands wird für alle abgeleitete Klassen unterstützt [ `VisualElement` ](xref:Xamarin.Forms.VisualElement), dies ist die Basisklasse für [ `View` ](xref:Xamarin.Forms.View) und [ `Page` ](xref:Xamarin.Forms.Page). 

Sie können auch eigene Gruppen visuelle Zustände definieren, und visuelle Zustände, wie in diesem Artikel werden gezeigt.

> [!NOTE]
> Xamarin.Forms-Entwicklern vertraut sind mit [Trigger](~/xamarin-forms/app-fundamentals/triggers.md) sind, beachten Sie, dass Trigger in Visualisierungen in der Benutzeroberfläche, die aufgrund von Änderungen in den Eigenschaften einer Sicht oder das Auslösen von Ereignissen auch Änderungen vornehmen können. Verwenden von Triggern für den Umgang mit verschiedenen Kombinationen dieser Änderungen kann jedoch recht verwirrend sein. In der Vergangenheit wurde der visuellen Status-Manager in Windows-XAML-basierten Umgebungen aus Kombinationen visuelle Zustände resultierende Verwirrung vermieden eingeführt. Mit VSM sind immer das visuelle Zustände innerhalb einer visuellen Zustands Gruppe sich gegenseitig ausschließende. Zu jedem Zeitpunkt ist nur ein Status in jeder Gruppe den aktuellen Status.

## <a name="the-common-states"></a>Der allgemeine Status

Die visuellen Status-Manager können Sie Abschnitte in der XAML-Datei einschließen, die die visuelle Darstellung einer Sicht ändern können, wenn die Sicht normal "oder" deaktiviert ist, oder über den Eingabefokus verfügt. Diese werden als bezeichnet den _häufige Zustände_.

Nehmen wir beispielsweise an, Sie haben eine `Entry` Ansicht auf der Seite und möchten, dass die visuelle Darstellung der `Entry` auf folgende Weise ändern:

- Die `Entry` müssen eine rosa im Hintergrund, wenn die `Entry` ist deaktiviert.
- Die `Entry` Lime Hintergrund sollten normalerweise haben.
- Die `Entry` zweimal seiner normalen Höhe erweitern soll, wenn es den Eingabefokus besitzt.

Sie können das Markup VSM an eine einzelne Ansicht anfügen, oder Sie können es in einem Format definieren, trifft auf mehrere Ansichten. In den nächsten beiden Abschnitten werden diese Ansätze beschrieben.

### <a name="vsm-markup-on-a-view"></a>VSM Markup für eine Sicht

VSM Markup zum Anfügen einer `Entry` anzuzeigen, trennen Sie zunächst die `Entry` in Start- und Endtags:

```xaml
<Entry FontSize="18">

</Entry>
```

Es wurde eine explizite Schriftgrad erhalten, da eine der Zustände verwendet die `FontSize` Eigenschaft, um die Größe des Texts im verdoppeln der `Entry`.

Legen Sie als Nächstes `VisualStateManager.VisualStateGroups` Tags zwischen die Tags:

```xaml
<Entry FontSize="18">
    <VisualStateManager.VisualStateGroups>

    </VisualStateManager.VisualStateGroups>
</Entry>
```

[`VisualStateGroups`](xref:Xamarin.Forms.VisualStateManager.VisualStateGroupsProperty) ist eine angefügte bindbare Eigenschaft definiert, indem Sie die [ `VisualStateManager` ](xref:Xamarin.Forms.VisualStateManager) Klasse. (Weitere Informationen zu angefügten bindbare Eigenschaften finden Sie im Artikel [angefügte Eigenschaften](~/xamarin-forms/xaml/attached-properties.md).) Dies ist wie die `VisualStateGroups` Eigenschaft angefügt ist die `Entry` Objekt.

Die `VisualStateGroups` -Eigenschaft ist vom Typ [ `VisualStateGroupList` ](xref:Xamarin.Forms.VisualStateGroupList), dies ist eine Auflistung von [ `VisualStateGroup` ](xref:Xamarin.Forms.VisualStateGroup) Objekte. Innerhalb der `VisualStateManager.VisualStateGroups` Tags, fügen Sie ein Paar von `VisualStateGroup` Tags für jede Gruppe von visuelle Zustände, die Sie einschließen möchten:

```xaml
<Entry FontSize="18">
    <VisualStateManager.VisualStateGroups>
        <VisualStateGroup x:Name="CommonStates">

        </VisualStateGroup>
    </VisualStateManager.VisualStateGroups>
</Entry>
```

Beachten Sie, dass die `VisualStateGroup` Tag weist ein `x:Name` Attribut, die den Namen der Gruppe. Die `VisualStateGroup` Klasse definiert ein `Name` -Eigenschaft, die Sie verwenden können:

```xaml
<VisualStateGroup Name="CommonStates">
```

Verwenden Sie entweder `x:Name` oder `Name` jedoch nicht beide im selben Element.

Die `VisualStateGroup` Klasse definiert eine Eigenschaft namens [ `States` ](xref:Xamarin.Forms.VisualStateGroup.States), dies ist eine Auflistung von [ `VisualState` ](xref:Xamarin.Forms.VisualState) Objekte. `States` ist die _content-Eigenschaft_ von `VisualStateGroups` damit eingeschlossen werden können die `VisualState` tags direkt zwischen den `VisualStateGroup` Tags. (Content-Eigenschaften werden im Artikel erläutert [grundlegende XAML-Syntax](~/xamarin-forms/xaml/xaml-basics/essential-xaml-syntax.md#content-properties).)

Der nächste Schritt besteht ein Paar von Tags für jedes visuelle Zustände in dieser Gruppe eingeschlossen werden sollen. Diese auch können ermittelt werden mit `x:Name` oder `Name`:

```xaml
<Entry FontSize="18">
    <VisualStateManager.VisualStateGroups>
        <VisualStateGroup x:Name="CommonStates">
            <VisualState x:Name="Normal">

            </VisualState>

            <VisualState x:Name="Focused">

            </VisualState>

            <VisualState x:Name="Disabled">

            </VisualState>
        </VisualStateGroup>
    </VisualStateManager.VisualStateGroups>
</Entry>
```

`VisualState` definiert eine Eigenschaft mit dem Namen [ `Setters` ](xref:Xamarin.Forms.VisualState.Setters), dies ist eine Auflistung von [ `Setter` ](xref:Xamarin.Forms.Setter) Objekte. Diese entsprechen `Setter` Objekte, die auf eine [ `Style` ](xref:Xamarin.Forms.Style) Objekt.

`Setters` ist _nicht_ die Inhaltseigenschaft des `VisualState`, daher ist es notwendig, Eigenschaftselementtags für enthalten die `Setters` Eigenschaft:

```xaml
<Entry FontSize="18">
    <VisualStateManager.VisualStateGroups>
        <VisualStateGroup x:Name="CommonStates">
            <VisualState x:Name="Normal">
                <VisualState.Setters>

                </VisualState.Setters>
            </VisualState>

            <VisualState x:Name="Focused">
                <VisualState.Setters>
    
                </VisualState.Setters>
            </VisualState>

            <VisualState x:Name="Disabled">
                <VisualState.Setters>

                </VisualState.Setters>
            </VisualState>
        </VisualStateGroup>
    </VisualStateManager.VisualStateGroups>
</Entry>
```

Sie können jetzt eine oder mehrere einfügen `Setter` Objekte zwischen jedem Paar von `Setters` Tags. Dies sind die `Setter` -Objekten, die zuvor beschriebenen visuelle Zustände definieren:

```xaml
<Entry FontSize="18">
    <VisualStateManager.VisualStateGroups>
        <VisualStateGroup x:Name="CommonStates">
            <VisualState x:Name="Normal">
                <VisualState.Setters>
                    <Setter Property="BackgroundColor" Value="Lime" />
                </VisualState.Setters>
            </VisualState>

            <VisualState x:Name="Focused">
                <VisualState.Setters>
                    <Setter Property="FontSize" Value="36" />
                </VisualState.Setters>
            </VisualState>

            <VisualState x:Name="Disabled">
                <VisualState.Setters>
                    <Setter Property="BackgroundColor" Value="Pink" />
                </VisualState.Setters>
            </VisualState>
        </VisualStateGroup>
    </VisualStateManager.VisualStateGroups>
</Entry>
```

Jede `Setter` Tag gibt den Wert einer bestimmten Eigenschaft aus, wenn dieser Status aktuell ist. Eine Eigenschaft verwiesen wird, indem ein `Setter` Objekt muss eine bindbare Eigenschaft gesichert werden.

Ähnlich wie dieses Markup bildet die Grundlage der der **VSM %.*ls'-Sicht** auf der Seite der **[VsmDemos](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/VsmDemos/)** Beispielprogramm. Die Seite enthält drei `Entry` Sichten, aber nur auf dem zweiten Ausdruck hat der VSM Markup angefügt ist:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:VsmDemos"
             x:Class="VsmDemos.MainPage"
             Title="VSM Demos">

    <StackLayout>
        <StackLayout.Resources>
            <Style TargetType="Entry">
                <Setter Property="Margin" Value="20, 0" />
                <Setter Property="FontSize" Value="18" />
            </Style>

            <Style TargetType="Label">
                <Setter Property="Margin" Value="20, 30, 20, 0" />
                <Setter Property="FontSize" Value="Large" />
            </Style>
        </StackLayout.Resources>

        <Label Text="Normal Entry:" />

        <Entry />

        <Label Text="Entry with VSM: " />

        <Entry>
            <VisualStateManager.VisualStateGroups>
                <VisualStateGroup x:Name="CommonStates">
                    
                    <VisualState x:Name="Normal">
                        <VisualState.Setters>
                            <Setter Property="BackgroundColor" Value="Lime" />
                        </VisualState.Setters>
                    </VisualState>

                    <VisualState x:Name="Focused">
                        <VisualState.Setters>
                            <Setter Property="FontSize" Value="36" />
                        </VisualState.Setters>
                    </VisualState>

                    <VisualState x:Name="Disabled">
                        <VisualState.Setters>
                            <Setter Property="BackgroundColor" Value="Pink" />
                        </VisualState.Setters>
                    </VisualState>
                </VisualStateGroup>
            </VisualStateManager.VisualStateGroups>

            <Entry.Triggers>
                <DataTrigger TargetType="Entry"
                             Binding="{Binding Source={x:Reference entry3},
                                               Path=Text.Length}"
                             Value="0">
                    <Setter Property="IsEnabled" Value="False" />
                </DataTrigger>
            </Entry.Triggers>
        </Entry>

        <Label Text="Entry to enable 2nd Entry:" />

        <Entry x:Name="entry3"
               Text=""
               Placeholder="Type something to enable 2nd Entry" />
    </StackLayout>
</ContentPage>
```

Beachten Sie, dass die zweite `Entry` verfügt auch über eine `DataTrigger` als Teil seiner `Trigger` Auflistung. Dies bewirkt, dass die `Entry` deaktiviert werden soll, bis der Eingabe in die dritte `Entry`. So sieht die Seite beim Start, die unter iOS, Android und die universelle Windows-Plattform (UWP):

[![VSM für Sicht: deaktiviert](vsm-images/VsmOnViewDisabled.png "VSM auf Ansicht – deaktiviert")](vsm-images/VsmOnViewDisabled-Large.png#lightbox)

Der aktuellen visuelle Status ist "Disabled" daher den Hintergrund des zweiten `Entry` rosa auf IOS- und Android-Bildschirmen ist. Die uwp-Implementierung von `Entry` lässt kein Festlegen von Hintergrund Farbe, wenn die `Entry` ist deaktiviert. 

Wenn Sie Text eingeben, in die dritte `Entry`, die zweite `Entry` wechselt in den Zustand "Normal", und der Hintergrund ist jetzt Lime:

[![VSM für Sicht: Normal](vsm-images/VsmOnViewNormal.png "VSM auf Ansicht – normal")](vsm-images/VsmOnViewNormal-Large.png#lightbox)

Wenn Sie die zweite berühren `Entry`, es den Eingabefokus erhält. Er wechselt in den Zustand "Fokussiert", und um zweimal seine Höhe erweitert:

[![VSM für Sicht: mit Fokus](vsm-images/VsmOnViewFocused.png "VSM-Sicht - mit Fokus")](vsm-images/VsmOnViewFocused-Large.png#lightbox)

Beachten Sie, dass die `Entry` Lime Hintergrund wird nicht beibehalten werden, wenn es den Eingabefokus erhält. Wie die visuellen Status-Manager zwischen visuellen Zustände gewechselt wird, sind die Eigenschaften, die festlegen, indem dem ursprünglichen Zustand nicht festgelegt. Denken Sie daran, die angibt, das visuelle Element schließen sich gegenseitig aus. Der Zustand "Normal" bedeutet nicht nur, dass die `Entry` aktiviert ist. Bedeutet, dass die `Entry` aktiviert ist und keine Eingabefokus. 

Wenn Sie möchten die `Entry` um einen Hintergrund Lime im Zustand "Fokussiert", fügen einen anderen `Setter` für diesen visuellen Status:

```xaml
<VisualState x:Name="Focused">
    <VisualState.Setters>
        <Setter Property="FontSize" Value="36" />
        <Setter Property="BackgroundColor" Value="Lime" />
    </VisualState.Setters>
</VisualState>
```

In der Reihenfolge für diese `Setter` Objekte ordnungsgemäß funktioniert, eine `VisualStateGroup` darf `VisualState` Objekte für alle Bundesstaaten in dieser Gruppe. Es ist eine visuelle Zustände, die keine `Setter` Objekte, fügen Sie ihn trotzdem als ein leeres Tag:

```xaml
<VisualState x:Name="Normal" />
``` 

### <a name="visual-state-manager-markup-in-a-style"></a>Visual-Status-Manager-Markup in einem Format

Es ist häufig erforderlich, um die gleichen visuellen Status-Manager-Markup zwischen mindestens zwei Ansichten freizugeben. In diesem Fall möchten Sie das Markup einfügen eine `Style` Definition.

Hier wird die vorhandene implizite `Style` für die `Entry` Elemente in der **VSM Ansicht** Seite:

```xaml
<Style TargetType="Entry">
    <Setter Property="Margin" Value="20, 0" />
    <Setter Property="FontSize" Value="18" />
</Style> 
```

Hinzufügen `Setter` tags für die `VisualStateManager.VisualStateGroups` -bindbare Eigenschaft:

```xaml
<Style TargetType="Entry">
    <Setter Property="Margin" Value="20, 0" />
    <Setter Property="FontSize" Value="18" />
    <Setter Property="VisualStateManager.VisualStateGroups">

    </Setter>
</Style> 
```

Die Content-Eigenschaft für `Setter` ist `Value`, sodass der Wert des der `Value` -Eigenschaft kann direkt in diese Tags angegeben werden. Diese Eigenschaft ist vom Typ `VisualStateGroupList`:

```xaml
<Style TargetType="Entry">
    <Setter Property="Margin" Value="20, 0" />
    <Setter Property="FontSize" Value="18" />
    <Setter Property="VisualStateManager.VisualStateGroups">
        <VisualStateGroupList>

        </VisualStateGroupList>
    </Setter>
</Style> 
```

In diese Tags können Sie ein oder mehrere einschließen `VisualStateGroup` Objekte:

```xaml
<Style TargetType="Entry">
    <Setter Property="Margin" Value="20, 0" />
    <Setter Property="FontSize" Value="18" />
    <Setter Property="VisualStateManager.VisualStateGroups">
        <VisualStateGroupList>
            <VisualStateGroup x:Name="CommonStates">

            </VisualStateGroup>
        </VisualStateGroupList>
    </Setter>
</Style> 
```

Der Rest des Markups VSM ist der gleiche wie zuvor.

So sieht die **VSM-Formats** Seite "zeigt die vollständige VSM Markup:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="VsmDemos.VsmInStylePage"
             Title="VSM in Style">
    <StackLayout>
        <StackLayout.Resources>
            <Style TargetType="Entry">
                <Setter Property="Margin" Value="20, 0" />
                <Setter Property="FontSize" Value="18" />
                <Setter Property="VisualStateManager.VisualStateGroups">
                    <VisualStateGroupList>
                        <VisualStateGroup x:Name="CommonStates">

                            <VisualState x:Name="Normal">
                                <VisualState.Setters>
                                    <Setter Property="BackgroundColor" Value="Lime" />
                                </VisualState.Setters>
                            </VisualState>

                            <VisualState x:Name="Focused">
                                <VisualState.Setters>
                                    <Setter Property="FontSize" Value="36" />
                                    <Setter Property="BackgroundColor" Value="Lime" />
                                </VisualState.Setters>
                            </VisualState>

                            <VisualState x:Name="Disabled">
                                <VisualState.Setters>
                                    <Setter Property="BackgroundColor" Value="Pink" />
                                </VisualState.Setters>
                            </VisualState>
                        </VisualStateGroup>
                    </VisualStateGroupList>
                </Setter>
            </Style>

            <Style TargetType="Label">
                <Setter Property="Margin" Value="20, 30, 20, 0" />
                <Setter Property="FontSize" Value="Large" />
            </Style>
        </StackLayout.Resources>

        <Label Text="Normal Entry:" />

        <Entry />
        
        <Label Text="Entry with VSM: " />

        <Entry>
            <Entry.Triggers>
                <DataTrigger TargetType="Entry"
                             Binding="{Binding Source={x:Reference entry3},
                                               Path=Text.Length}"
                             Value="0">
                    <Setter Property="IsEnabled" Value="False" />
                </DataTrigger>
            </Entry.Triggers>
        </Entry>

        <Label Text="Entry to enable 2nd Entry:" />

        <Entry x:Name="entry3"
               Text=""
               Placeholder="Type something to enable 2nd Entry" />
    </StackLayout>
</ContentPage>
```

Jetzt alle der `Entry` Sichten auf dieser Seite die gleiche Weise, ihre visuelle Zustände zu reagieren. Beachten Sie außerdem, dass der Zustand "Fokussiert" jetzt eine zweite enthält `Setter` , die erhält jeder `Entry` eine Lime Hintergrund auch, wenn es den Eingabefokus besitzt:

[![VSM-Formats](vsm-images/VsmInStyle.png "VSM-Formats")](vsm-images/VsmInStyle-Large.png#lightbox)

## <a name="defining-your-own-visual-states"></a>Definieren eigene visuelle Zustände

Jede Klasse, die abgeleitet `VisualElement` unterstützt die drei allgemeinen Status "Normal", "Mit Fokus" und "Disabled". Intern können die [ `VisualElement` ](https://github.com/xamarin/Xamarin.Forms/blob/master/Xamarin.Forms.Core/VisualElement.cs) Klasse erkennt, wenn er aktiviert oder deaktiviert ist, oder fokussierte oder ohne Fokus gewinnt, und die statische ruft [ `VisualStateManager.GoToState` ](https://developer.xamarin.com/api/member/Xamarin.Forms.VisualStateManager.GoToState/p/Xamarin.Forms.VisualElement/System.String/) Methode:

```csharp
VisualStateManager.GoToState(this, "Focused");
```

Dies ist die einzige visuellen Status-Manager-Code, den finden Sie in der `VisualElement` Klasse. Da `GoToState` heißt für jedes Objekt basierend auf jede Klasse, die abgeleitet `VisualElement`, können Sie mit den visuellen Status-Manager `VisualElement` Objekt so reagieren Sie auf diese Änderungen.

Interessanterweise, der Namen der Gruppe der visuellen Zustands "CommonStates" wird nicht explizit verwiesen `VisualElement`. Der Gruppenname ist nicht Teil der API für den visuellen Status-Manager. In einem der beiden Beispielprogramm bisher angezeigt wird, können Sie den Namen der Gruppe "aus"CommonStates"etwas anderes ändern und das Programm weiterhin funktionieren. Der Gruppenname ist lediglich eine allgemeine Beschreibung der Status in dieser Gruppe. Er wird implizit verstanden, dass die visuelle Zustände in einer beliebigen Gruppe sich gegenseitig ausschließende sind: eine und nur einen Zustand zu einem beliebigen Zeitpunkt aktuell ist.

Wenn Sie eine eigene visuelle Zustände zu implementieren möchten, müssen Sie zum Aufrufen `VisualStateManager.GoToState` von Code. Am häufigsten treffen Sie diesen Aufruf aus der CodeBehind-Datei der Page-Klasse.

Die **VSM Überprüfung** auf der Seite der **[VsmDemos](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/VsmDemos/)** Beispiel zeigt, wie die visuellen Status-Manager im Zusammenhang mit der Validierung von Benutzereingaben. Die XAML-Datei besteht aus zwei `Label` Elemente ein `Entry`, und `Button`:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="VsmDemos.VsmValidationPage"
             Title="VSM Validation">
    <StackLayout Padding="10, 10">
        
        <Label Text="Enter a U.S. phone number:"
               FontSize="Large" />

        <Entry Placeholder="555-555-5555"
               FontSize="Large"
               Margin="30, 0, 0, 0"
               TextChanged="OnTextChanged" />

        <Label x:Name="helpLabel"
               Text="Phone number must be of the form 555-555-5555, and not begin with a 0 or 1">
            <VisualStateManager.VisualStateGroups>
                <VisualStateGroup Name="ValidityStates">
                    
                    <VisualState Name="Valid">
                        <VisualState.Setters>
                            <Setter Property="TextColor" Value="Transparent" />
                        </VisualState.Setters>
                    </VisualState>

                    <VisualState Name="Invalid" />
                    
                </VisualStateGroup>
            </VisualStateManager.VisualStateGroups>
        </Label>

        <Button x:Name="submitButton"
                Text="Submit"
                FontSize="Large"
                Margin="0, 20"
                VerticalOptions="Center"
                HorizontalOptions="Center">
            <VisualStateManager.VisualStateGroups>
                <VisualStateGroup Name="ValidityStates">
                    
                    <VisualState Name="Valid" />

                    <VisualState Name="Invalid">
                        <VisualState.Setters>
                            <Setter Property="IsEnabled" Value="False" />
                        </VisualState.Setters>
                    </VisualState>
                    
                </VisualStateGroup>
            </VisualStateManager.VisualStateGroups>
        </Button>
    </StackLayout>
</ContentPage>
```

VSM Markup angefügt ist, auf dem zweiten `Label` (mit dem Namen `helpLabel`) und die `Button` (mit dem Namen `submitButton`). Es gibt zwei sich gegenseitig ausschließende Zuständen, mit dem Namen "Gültig" und "Ungültig". Beachten Sie, dass jede der beiden Gruppen "ValidationState" enthält `VisualState` tags für "Gültig" und "Ungültig", obwohl eine von ihnen in jedem Fall leer ist. 

Wenn die `Entry` enthält keine gültige Telefonnummer, und klicken Sie dann der aktuelle Status "Ungültig" ist, und damit die zweite `Label` sichtbar ist und die `Button` ist deaktiviert:

[![VSM-Überprüfung: Ungültiger State](vsm-images/VsmValidationInvalid.png "VSM Überprüfung - ungültig")](vsm-images/VsmValidationInvalid-Large.png#lightbox)

Wenn Sie eine gültige Telefonnummer eingegeben wird, klicken Sie dann der aktuelle Status ist "Gültig". Die zweite `Entry` nicht mehr angezeigt wird und die `Button` ist jetzt aktiviert:

[![VSM-Überprüfung: Kontostände](vsm-images/VsmValidationValid.png "VSM Überprüfung - ungültig")](vsm-images/VsmValidationValid-Large.png#lightbox)

Die Code-Behind-Datei ist für die Behandlung von Reponsible der `TextChanged` Ereignis aus der `Entry`. Der Handler verwendet einen regulären Ausdruck, um zu bestimmen, ob die Eingabezeichenfolge gültig ist. Die Methode in der Code-Behind-Datei mit dem Namen `GoToState` Ruft die statische `VisualStateManager.GoToState` Methode für beide `helpLabel` und `submitButton`:

```csharp
public partial class VsmValidationPage : ContentPage
{
    public VsmValidationPage ()
    {
        InitializeComponent ();

        GoToState(false);
    }

    void OnTextChanged(object sender, TextChangedEventArgs args)
    {
        bool isValid = Regex.IsMatch(args.NewTextValue, @"^[2-9]\d{2}-\d{3}-\d{4}$");
        GoToState(isValid);
    }

    void GoToState(bool isValid)
    {
        string visualState = isValid ? "Valid" : "Invalid";
        VisualStateManager.GoToState(helpLabel, visualState);
        VisualStateManager.GoToState(submitButton, visualState);
    }
}
```

Beachten Sie auch, dass die `GoToState` Methode wird vom Konstruktor initialisiert werden, den Zustand aufgerufen. Es sollte immer der aktuellen Zustand vorhanden sein. Aber nie im Code gibt es alle Verweise auf den Namen der Gruppe der visuellen Zustands, obwohl es in der XAML-Code als "ValidationStates" Gründen der Klarheit verwiesen wird. 

Beachten Sie, dass die Code-Behind-Datei berücksichtigen muss jedes Objekt auf der Seite, die betroffen sind durch diese visuelle Zustände und zum Aufrufen `VisualStateManager.GoToState` für jedes dieser Objekte. In diesem Beispiel ist es nur zwei Objekte (die `Label` und die `Button`), aber es ist möglicherweise mehrere weitere.

Sie Fragen sich vielleicht: Wenn die Code-Behind-Datei aller Objekte auf der Seite beziehen, die diese visuelle Zustände betroffen ist, warum kann nicht die Code-Behind-Datei einfach Zugriff auf die Objekte direkt? Es könnte sich sicherlich. Der Vorteil der Verwendung der VSM ist jedoch, dass Sie, wie visuelle Elemente steuern können zu reagieren, Status, der nicht vollständig in XAML, die alle das Design der Benutzeroberfläche im Speicherorten abgelegt sind. Dadurch wird die visuelle Darstellung der Einstellung durch Zugreifen auf visuelle Elemente direkt aus dem Code-Behind vermieden.

Ist es möglicherweise zu berücksichtigenden Ableiten einer Klasse von verlockend `Entry` und vielleicht Definieren einer Eigenschaft, die Sie auf eine externe Überprüfungsfunktion festlegen können. Die Klasse, die abgeleitet `Entry` kann durch einen Aufruf der `VisualStateManager.GoToState` Methode. Dieses Schema funktioniert gut, aber nur, wenn die `Entry` das einzige Objekt, das die unterschiedlicher visueller Zustände betroffen waren. In diesem Beispiel wird eine `Label` und ein `Button` sind ebenfalls betroffen sein. Es gibt keine Möglichkeit für VSM Markup angefügt ein `Entry` anderer Objekte auf der Seite ", und keine Möglichkeit zu steuern, für VSM Markup auf andere Objekte, um eine Änderung im visuellen Zustands von einem anderen Objekt verweisen angefügt.

<a name="adaptive-layout" />

## <a name="using-the-visual-state-manager-for-adaptive-layout"></a>Verwenden den visuellen Status-Manager für das adaptive layout

Eine Xamarin.Forms, die auf einem Telefon ausgeführte Anwendung in der Regel auf ein Portrait oder Querformat Seitenverhältnis und einer Xamarin.Forms-Programm auf dem Desktop ausgeführte angezeigt werden kann kann geändert werden, um viele verschiedene Größen und Seitenverhältnissen angenommen. Eine wohlgeformte Anwendung möglicherweise den Inhalt für diese verschiedenen Formfaktoren Seiten- oder Fenster unterschiedlich angezeigt. 

Diese Technik wird auch bezeichnet als _adaptive Layout_. Da adaptive Layout ausschließlich ein Programm visuelle Elemente umfasst, ist es eine ideale visuellen Status-Manager-Anwendung.

Ein einfaches Beispiel ist eine Anwendung, die eine kleine Sammlung von Schaltflächen angezeigt, die der Inhalt der Anwendung zu beeinflussen. Im Hochformat können diese Schaltflächen in einer horizontalen Reihe oben auf der Seite angezeigt werden:

[![Adaptive VSM-Layout: Hochformat](vsm-images/VsmAdaptiveLayoutPortrait.png "VSM adaptive Layout - Hochformat")](vsm-images/VsmAdaptiveLayoutPortrait-Large.png#lightbox)

Im Querformat das Array von Schaltflächen möglicherweise auf einer Seite verschoben, und in einer Spalte angezeigt:

[![Adaptive VSM-Layout: Querformat](vsm-images/VsmAdaptiveLayoutLandscape.png "VSM adaptive Layout - Querformat")](vsm-images/VsmAdaptiveLayoutLandscape-Large.png#lightbox)

Von oben nach unten wird das Programm auf die universelle Windows-Plattform, Android und iOS ausgeführt.

Die **VSM Adaptive Layout** auf der Seite der [VsmDemos](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/VsmDemos/) Beispiel definiert eine Gruppe namens "OrientationStates" mit zwei visuelle Zustände, die mit dem Namen "Hochformat" und "Querformat". (Ein komplexer Ansatz kann auf mehrere verschiedene Seiten- oder Fenster breiten basieren.) 

VSM Markup erfolgt in vier Stellen in der XAML-Datei. Die `StackLayout` mit dem Namen `mainStack` enthält das Menü und der Inhalt, d. h. ein `Image` Element. Dies `StackLayout` eine vertikale Ausrichtung im Hochformat und eine horizontale Ausrichtung im Querformat aufweisen:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="VsmDemos.VsmAdaptiveLayoutPage"
             Title="VSM Adaptive Layout">

    <StackLayout x:Name="mainStack">
        <VisualStateManager.VisualStateGroups>
            <VisualStateGroup Name="OrientationStates">

                <VisualState Name="Portrait">
                    <VisualState.Setters>
                        <Setter Property="Orientation" Value="Vertical" />
                    </VisualState.Setters>
                </VisualState>

                <VisualState Name="Landscape">
                    <VisualState.Setters>
                        <Setter Property="Orientation" Value="Horizontal" />
                    </VisualState.Setters>
                </VisualState>
            </VisualStateGroup>
        </VisualStateManager.VisualStateGroups>
        
        <ScrollView x:Name="menuScroll">
            <VisualStateManager.VisualStateGroups>
                <VisualStateGroup Name="OrientationStates">
                    
                    <VisualState Name="Portrait">
                        <VisualState.Setters>
                            <Setter Property="Orientation" Value="Horizontal" />
                        </VisualState.Setters>
                    </VisualState>

                    <VisualState Name="Landscape">
                        <VisualState.Setters>
                            <Setter Property="Orientation" Value="Vertical" />
                        </VisualState.Setters>
                    </VisualState>
                </VisualStateGroup>
            </VisualStateManager.VisualStateGroups>
            
            <StackLayout x:Name="menuStack">
                <VisualStateManager.VisualStateGroups>
                    <VisualStateGroup Name="OrientationStates">

                        <VisualState Name="Portrait">
                            <VisualState.Setters>
                                <Setter Property="Orientation" Value="Horizontal" />
                            </VisualState.Setters>
                        </VisualState>

                        <VisualState Name="Landscape">
                            <VisualState.Setters>
                                <Setter Property="Orientation" Value="Vertical" />
                            </VisualState.Setters>
                        </VisualState>
                    </VisualStateGroup>
                </VisualStateManager.VisualStateGroups>

                <StackLayout.Resources>
                    <Style TargetType="Button">
                        <Setter Property="VisualStateManager.VisualStateGroups">
                            <VisualStateGroupList>
                                <VisualStateGroup Name="OrientationStates">

                                    <VisualState Name="Portrait">
                                        <VisualState.Setters>
                                            <Setter Property="HorizontalOptions" Value="CenterAndExpand" />
                                            <Setter Property="Margin" Value="10, 5" />
                                        </VisualState.Setters>
                                    </VisualState>

                                    <VisualState Name="Landscape">
                                        <VisualState.Setters>
                                            <Setter Property="VerticalOptions" Value="CenterAndExpand" />
                                            <Setter Property="HorizontalOptions" Value="Center" />
                                            <Setter Property="Margin" Value="10" />
                                        </VisualState.Setters>
                                    </VisualState>
                                </VisualStateGroup>
                            </VisualStateGroupList>
                        </Setter>
                    </Style>
                </StackLayout.Resources>

                <Button Text="Banana"
                        Command="{Binding SelectedCommand}"
                        CommandParameter="Banana.jpg" />
                
                <Button Text="Face Palm"
                        Command="{Binding SelectedCommand}"
                        CommandParameter="FacePalm.jpg" />
                
                <Button Text="Monkey"
                        Command="{Binding SelectedCommand}"
                        CommandParameter="monkey.png" />
                
                <Button Text="Seated Monkey"
                        Command="{Binding SelectedCommand}"
                        CommandParameter="SeatedMonkey.jpg" />
            </StackLayout>
        </ScrollView>

        <Image x:Name="image"
               VerticalOptions="FillAndExpand"
               HorizontalOptions="FillAndExpand" />
    </StackLayout>
</ContentPage>
```

Die innere `ScrollView` mit dem Namen `menuScroll` und `StackLayout` mit dem Namen `menuStack` im Menü von Schaltflächen zu implementieren. Die Ausrichtung des für diese Layouts wird entgegengesetzten von `mainStack`. Klicken Sie im Menü sollte im Hochformat horizontale und vertikale im Querformat.

Der vierte Abschnitt VSM Markup ist in einem impliziten Stil für die Schaltflächen selbst. Dieses Markup legt `VerticalOptions`, `HorizontalOptions`, und `Margin` Eigenschaften, die spezifisch für die Ausrichtungen an Portait und Querformat.

Im Code-Behind-Datei wird die `BindingContext` Eigenschaft `menuStack` implementieren `Button` Befehle, und außerdem Fügt einen Handler die `SizeChanged` -Ereignis für die Seite:

```csharp
public partial class VsmAdaptiveLayoutPage : ContentPage
{
    public VsmAdaptiveLayoutPage ()
    {
        InitializeComponent ();

        SizeChanged += (sender, args) =>
        {
            string visualState = Width > Height ? "Landscape" : "Portrait";
            VisualStateManager.GoToState(mainStack, visualState);
            VisualStateManager.GoToState(menuScroll, visualState);
            VisualStateManager.GoToState(menuStack, visualState);

            foreach (View child in menuStack.Children)
            {
                VisualStateManager.GoToState(child, visualState);
            }
        };

        SelectedCommand = new Command<string>((filename) =>
        {
            image.Source = ImageSource.FromResource("VsmDemos.Images." + filename);
        });

        menuStack.BindingContext = this;
    }

    public ICommand SelectedCommand { private set; get; }
}
```

Die `SizeChanged` Ereignishandler ruft `VisualStateManager.GoToState` für die beiden `StackLayout` und `ScrollView` Elemente, und klicken Sie dann durchläuft die untergeordneten Elemente des `menuStack` Aufrufen `VisualStateManager.GoToState` für die `Button` Elemente.

Es mag, als ob die Code-Behind-Datei Ausrichtung Änderungen behandeln direkt durch Festlegen der Eigenschaften von Elementen in der XAML-Datei, jedoch den visuellen Status-Manager ein strukturierter Ansatz ist. Alles, was die visuellen Elemente in der XAML-Datei gespeichert werden, in denen sie einfacher zu untersuchen sind, verwalten und ändern.

## <a name="visual-state-manager-with-xamarinuniversity"></a>Visual-Status-Manager mit Xamarin.University

> [!VIDEO https://youtube.com/embed/qhUHbVP5mIQ]

**Xamarin.Forms 3.0 Visual-Status-Manager, von [Xamarin University](https://university.xamarin.com/)**

## <a name="related-links"></a>Verwandte Links

- [VsmDemos](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/VsmDemos/)

