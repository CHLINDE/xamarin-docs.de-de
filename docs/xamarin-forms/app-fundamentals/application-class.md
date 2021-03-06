---
title: Xamarin.Forms-App-Klasse
description: Dieser Artikel beschreibt die Funktionen von der App-Klasse, d., die h. eine Eigenschaft, auf der ersten Seite für die app festzulegen, und eine permanente Wörterbuch für einfache Werte über Änderungen im abonnementlebenszyklus Zustand speichern.
ms.prod: xamarin
ms.assetid: 421F8294-1944-46A4-8459-D2BD5AAABC9D
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 02/19/2016
ms.openlocfilehash: 15fb866d2cde9409f401d6d021b22b8cb0468795
ms.sourcegitcommit: 66682dd8e93c0e4f5dee69f32b5fc5a96443e307
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/08/2018
ms.locfileid: "35240540"
---
# <a name="xamarinforms-app-class"></a>Xamarin.Forms-App-Klasse

Die `Application` Basisklasse bietet die folgenden Funktionen, die in Ihrem Standard-Projekte verfügbar gemacht werden `App` Unterklasse:

* Ein `MainPage` -Eigenschaft, die wo die erste Seite für die app festgelegt wird.
* Einer dauerhaften [ `Properties` Wörterbuch](#Properties_Dictionary) einfache Werte über Änderungen im abonnementlebenszyklus Zustand zu speichern.
* Eine statische `Current` -Eigenschaft, die einen Verweis auf das aktuelle Anwendungsobjekt enthält.

Macht auch [Lebenszyklusmethoden](~/xamarin-forms/app-fundamentals/app-lifecycle.md) wie z. B. `OnStart`, `OnSleep`, und `OnResume` sowie modale Navigationsereignisse.

Je nach Sie ausgewählt haben, die `App` Klasse definiert werden, auf zwei Arten:

* **C#-**, oder
* **XAML UND C#**

Zum Erstellen einer **App** -Klasse unter Verwendung von XAML, der Standardwert **App** Klasse ersetzt werden muss, durch einen XAML-Code **App** Klasse und zugehörigen Code-Behind, wie im folgenden Codebeispiel wird gezeigt:

```xaml
<Application xmlns="http://xamarin.com/schemas/2014/forms" xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" x:Class="Photos.App">

</Application>
```

Das folgende Codebeispiel zeigt den zugehörigen Code-Behind:

```csharp
public partial class App : Application
{
    public App ()
    {
        InitializeComponent ();
        MainPage = new HomePage ();
    }
    ...
}
```

Sowie die Einstellung der [ `MainPage` ](https://developer.xamarin.com/api/property/Xamarin.Forms.Application.MainPage/) -Eigenschaft, die Code-Behind muss auch aufrufen, die `InitializeComponent` Methode zum Laden und analysieren den zugehörigen XAML-Code.

## <a name="mainpage-property"></a>MainPage-Eigenschaft

Die `MainPage` Eigenschaft auf die `Application` -Klasse legt die Stammseite der Anwendung.

Sie können z. B. Logik erstellen Ihrer `App` Klasse, je nachdem, ob der Benutzer oder nicht in angemeldet ist eine andere Seite anzeigen.

Die `MainPage` Eigenschaft sollte festgelegt werden, der `App` -Konstruktor

```csharp
public class App : Xamarin.Forms.Application
{
    public App ()
    {
        MainPage = new ContentPage { Title = "App Lifecycle Sample" }; // your page here
    }
}
```

<a name="Properties_Dictionary" />

## <a name="properties-dictionary"></a>Eigenschaftenwörterbuch

Die `Application` Unterklasse weist eine statische `Properties` Wörterbuch zum Speichern von Daten, insbesondere verwendet werden kann, für die Verwendung in der `OnStart`, `OnSleep`, und `OnResume` Methoden. Dies kann über eine beliebige Stelle in dem Code mit Xamarin.Forms zugegriffen werden `Application.Current.Properties`.

Die `Properties` Wörterbuch verwendet eine `string` Schlüssel und speichert eine `object` Wert.

Sie konnten z. B. eine Autorisierungstypen festgelegt `"id"` Eigenschaft an einer beliebigen Stelle im Code (wenn ein Element aktiviert ist und auf einer Seite `OnDisappearing` -Methode, oder in der `OnSleep` Methode) wie folgt:

```csharp
Application.Current.Properties ["id"] = someClass.ID;
```

In der `OnStart` oder `OnResume` Methoden können Sie dann diesen Wert um die benutzerfreundlichkeit in irgendeiner Form neu zu erstellen. Die `Properties` Wörterbuch speichert `object`s, daher Sie seinen Wert umgewandelt, bevor Sie ihn verwenden müssen.

```csharp
if (Application.Current.Properties.ContainsKey("id"))
{
    var id = Application.Current.Properties ["id"] as int;
    // do something with id
}
```

Überprüfen Sie immer auf das Vorhandensein des Schlüssels, vor dem Zugriff, um zu verhindern, dass unerwartete Fehler auf.

> [!NOTE]
> Die `Properties` Wörterbuch kann nur primitive Typen für den Speicher serialisieren. Andere Typen speichern möchten (z. B. `List<string>`) kann fehlschlagen, im Hintergrund.

<!-- bugzilla 28657 -->

### <a name="persistence"></a>Persistenz

Die `Properties` Wörterbuch wird automatisch auf dem Gerät gespeichert.
Daten, die dem Wörterbuch hinzugefügte stehen Rückkehr von die Anwendung von Hintergrund oder auch nach einem Neustart.

Xamarin.Forms 1.4 eine zusätzliche Anmeldemethode eingeführt, auf die `Application` Class - `SavePropertiesAsync()` -die kann aufgerufen werden, um proaktiv beizubehalten der `Properties` Wörterbuch. Dadurch soll können Sie Eigenschaften nach wichtigen Updates zu speichern, anstatt Sie zu riskieren sie nicht aufgrund eines Absturzes oder vom Betriebssystem beendet wird serialisiert abrufen.

Finden Sie Verweise auf die Verwendung der `Properties` Wörterbuch in das **Erstellen mobiler Apps mit Xamarin.Forms** book Kapiteln [6](https://developer.xamarin.com/r/xamarin-forms/book/chapter06.pdf), [15](https://developer.xamarin.com/r/xamarin-forms/book/chapter15.pdf), und [20 ](https://developer.xamarin.com/r/xamarin-forms/book/chapter20.pdf), und klicken Sie in der zugeordneten [Beispiele](https://github.com/xamarin/xamarin-forms-book-preview-2).



## <a name="the-application-class"></a>Die Application-Klasse

Eine vollständige `Application` klassenimplementierung Referenzzwecken unten angezeigt:

```csharp
public class App : Xamarin.Forms.Application
{
    public App ()
    {
        MainPage = new ContentPage { Title = "App Lifecycle Sample" }; // your page here
    }

    protected override void OnStart()
    {
        // Handle when your app starts
        Debug.WriteLine ("OnStart");
    }

    protected override void OnSleep()
    {
        // Handle when your app sleeps
        Debug.WriteLine ("OnSleep");
    }

    protected override void OnResume()
    {
        // Handle when your app resumes
        Debug.WriteLine ("OnResume");
    }
}

```

Diese Klasse ist dann in jedem Projekt plattformspezifischen instanziiert und übergeben der `LoadApplication` Methode ist, die `MainPage` geladen und dem Benutzer angezeigt wird.
Der Code für jede Plattform wird in den folgenden Abschnitten gezeigt. Die neuesten Xamarin.Forms-Projektmappenvorlagen enthalten bereits dieser Code für Ihre app vorkonfiguriert.


### <a name="ios-project"></a>iOS-Projekt

IOS `AppDelegate` Klasse erbt jetzt von `FormsApplicationDelegate`. Es sollten:

* Rufen Sie `LoadApplication` mit einer Instanz von der `App` Klasse.

* Stets `base.FinishedLaunching (app, options);`.

```csharp
[Register ("AppDelegate")]
public partial class AppDelegate :
    global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate // superclass new in 1.3
{
    public override bool FinishedLaunching (UIApplication app, NSDictionary options)
    {
        global::Xamarin.Forms.Forms.Init ();

        LoadApplication (new App ());  // method is new in 1.3

        return base.FinishedLaunching (app, options);
    }
}
```

### <a name="android-project"></a>Android-Projekt

Die Android `MainActivity` jetzt erbt von `FormsApplicationActivity`. In der `OnCreate` überschreiben die `LoadApplication` Methode wird aufgerufen, mit einer Instanz von der `App` Klasse.

```csharp
[Activity (Label = "App Lifecycle Sample", Icon = "@drawable/icon", MainLauncher = true,
    ConfigurationChanges = ConfigChanges.ScreenSize | ConfigChanges.Orientation)]
public class MainActivity :
    global::Xamarin.Forms.Platform.Android.FormsApplicationActivity // superclass new in 1.3
{
    protected override void OnCreate (Bundle bundle)
    {
        base.OnCreate (bundle);

        global::Xamarin.Forms.Forms.Init (this, bundle);

        LoadApplication (new App ()); // method is new in 1.3
    }
}
```

> [!NOTE]
> Es ist eine neuere [ `FormsAppCompatActivity` ](~/xamarin-forms/platform/android/appcompat.md) Basisklasse, die verwendet werden kann, Android Material Entwurf besser zu unterstützen.
> Dies wird die Standardvorlage für Android in Zukunft werden, aber Sie können befolgen [diese Anweisungen](~/xamarin-forms/platform/android/appcompat.md) Ihrer vorhandenen Android-apps zu aktualisieren.

### <a name="universal-windows-project-uwp-for-windows-10"></a>Universelle Windows-Projekt (UWP) für Windows 10

Finden Sie unter [Windows Setupprojekten](~/xamarin-forms/platform/windows/installation/index.md) Informationen zur uwp-Unterstützung in Xamarin.Forms.

Die Hauptseite im uwp-Projekt sollte Vererben `WindowsPage`. Dies bedeutet, dass der XAML und c# für `MainPage` Verweis der `FormsApplicationPage` -Klasse wie dargestellt.

Der XAML-Code wird einen benutzerdefinierten Namespace verwendet, sodass das Stammelement gibt der `FormsApplicationPage` Klasse:

```xaml
<forms:WindowsPage
   ...
   xmlns:forms="using:Xamarin.Forms.Platform.UWP"
   ...>
</forms:WindowsPage>
```

C#-Codebehind des Konstruktion muss Aufrufen `LoadApplication` zum Erstellen einer Instanz von Ihr Xamarin.Forms `App`. Beachten Sie, dass es empfiehlt sich, die anwendungsnamespace explizit zu verwenden, um zu kennzeichnen die `App` Schreibberechtigung uwp-Apps auch ihre eigenen `App` Klasse, die unabhängig vom stagingstatus Xamarin.Forms.

```csharp
public sealed partial class MainPage
{
    public MainPage()
    {
        InitializeComponent();

        LoadApplication(new YOUR_NAMESPACE.App());
    }
 }
```

Beachten Sie, dass `Forms.Init()` muss aufgerufen werden, **App.xaml.cs** um Linie 63.
