---
title: Einrichten der Windows-Projekte
description: Hinzufügen von neuen Windows-Projekten zu einer vorhandenen Xamarin.Forms-Projektmappe
ms.prod: xamarin
ms.assetid: A0774D2E-6994-4D91-84E8-DAB66FC92320
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 02/16/2016
ms.openlocfilehash: 071239abc71a41798a240128f8339687026296f9
ms.sourcegitcommit: 1561c8022c3585655229a869d9ef3510bf83f00a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/27/2018
---
# <a name="setup-windows-projects"></a>Einrichten der Windows-Projekte

_Hinzufügen von neuen Windows-Projekten zu einer vorhandenen Xamarin.Forms-Projektmappe_

Ältere Xamarin.Forms-Lösungen (oder solche, die auf MacOS erstellt) weisen keine app-Projekte der universellen Windows-Plattform (UWP). Aus diesem Grund müssen Sie eine uwp-Projekt zum Erstellen einer app für Windows 10 (UWP) manuell hinzufügen.

<a name="pcl" />

## <a name="update-the-pcl-profile"></a>Aktualisieren Sie das PCL-Profil

Wenn Ihre vorhandene Xamarin.Forms-app die Portable Klassenbibliothek (PCL)-Vorlage verwendet, müssen Sie ein Profil aktualisieren.

1. **mit der rechten Maustaste > Eigenschaften** (bestehenden Einstellungen können abweichen)

  ![](images/targets.png "PCL-Ziele")

2. Klicken Sie auf die **ändern...**  Schaltfläche

3. Stellen Sie sicher der **Windows 8** und **Windows Phone 8.1** Optionen aktiviert sind (und **Windows Phone Silveright** ist *deaktiviert*):

  ![](images/pcl.png "PCL Zieloptionen")

4. Drücken Sie **OK** und die Änderungen zu speichern.

Dies ist identisch mit dem **Profil 111** , wenn Sie Ihre PCL in Visual Studio für Mac mithilfe der Dropdown-Liste konfigurieren.

  ![](images/pcl-xs.png "PCL Profil 111")

## <a name="add-a-universal-windows-platform-app"></a>Fügen Sie eine universelle Windows Plattform-app

Sie sollten ausgeführt werden **Visual Studio 2017** auf **Windows 10** uwp-apps erstellen. Weitere Informationen zu universellen Windows-Plattform, finden Sie unter [Einführung in die universelle Windows-Plattform](/windows/uwp/get-started/universal-application-platform-guide/).

Universelle Windows-Plattform ist in Xamarin.Forms 2.1 und höher verfügbar und Xamarin.Forms.Maps wird in Xamarin.Forms 2.2 und höher unterstützt.

Überprüfen Sie die <a href="#troubleshooting">Problembehandlung</a> Abschnitt, um nützliche Tipps.

So fügen Sie einer uwp-app hinzu, die auf Windows 10-Smartphones, Tablets und Desktops ausgeführt wird, gehen Sie wie folgt vor:

 1. Mit der rechten Maustaste auf die Projektmappe, und wählen Sie **hinzufügen > Neues Projekt...**  und Hinzufügen einer **leere App (universelle Windows)** Projekt:

  ![](universal-images/add-wu.png "Dialogfeld "Neues Projekt" hinzufügen")

 2. In der **neue universelle Windows-Plattform-Projekt** Dialogfeld wählen die Minimum und Ziel-Versionen von Windows 10, unter dem die app ausgeführt wird:

  ![](universal-images/target-version.png "Dialogfeld "Neues universelle Windows Plattform-Projekt"")

 3. Mit der rechten Maustaste auf das uwp-Projekt, und wählen Sie **NuGet-Pakete verwalten...**  und Hinzufügen der **Xamarin.Forms** Paket. Stellen Sie sicher, dass auf die gleiche Version des Pakets Xamarin.Forms auch andere Projekte in der Lösung aktualisiert wurden.

 4. Stellen Sie sicher, dass das neue uwp-Projekt erstellt werden der **erstellen > Configuration Manager** Fenster (dies wahrscheinlich wird nicht Volumenamen standardmäßig). Tick der **erstellen** und **bereitstellen** Felder für das universelle Projekt:

  [![](universal-images/configuration-sml.png "Fenster "Konfigurations-Manager"")](universal-images/configuration.png#lightbox "Fenster "Konfigurations-Manager"")

 5. Mit der rechten Maustaste auf das Projekt, und wählen **hinzufügen > Verweis** , und erstellen Sie einen Verweis auf das Anwendungsprojekt Xamarin.Forms (PCL, .NET Standard oder freigegebenes Projekt).

  ![](universal-images/addref-sml.png "Dialogfeld "Verweis-Manager"")

 6. Bearbeiten Sie im uwp-Projekt **App.xaml.cs** einschließen der `Init` Methodenaufruf innerhalb der `OnLaunched` Methode um Linie 52:

```csharp
// under this line
rootFrame.NavigationFailed += OnNavigationFailed;
// add this line
Xamarin.Forms.Forms.Init (e); // requires the `e` parameter
```

 7. Bearbeiten Sie im uwp-Projekt **"MainPage.xaml"** durch das Entfernen der `Grid` enthaltenen der `Page` Element.

 8. In **"MainPage.xaml"**, fügen Sie einen neuen `xmlns` Eintrag für `Xamarin.Forms.Platform.UWP`:

```csharp
xmlns:forms="using:Xamarin.Forms.Platform.UWP"
```

 9. In **"MainPage.xaml"**, ändern Sie den Stamm `<Page` Element `<forms:WindowsPage`:

```xaml
<forms:WindowsPage
...
   xmlns:forms="using:Xamarin.Forms.Platform.UWP"
...
</forms:WindowsPage>
```

 10. In uwp-Projekt bearbeiten **"MainPage.Xaml.cs"** So entfernen Sie die `: Page` Vererbung Spezifizierer nach dem Klassennamen (da es nun erbt, `WindowsPage` aufgrund der Änderung, die im vorherigen Schritt):

```csharp
public sealed partial class MainPage  // REMOVE ": Page"
```

 11. In **"MainPage.Xaml.cs"**, Hinzufügen der `LoadApplication` rufen Sie in der `MainPage` Konstruktor, um die Xamarin.Forms-app zu starten:

```csharp
// below this existing line
this.InitializeComponent();
// add this line
LoadApplication(new YOUR_NAMESPACE.App());
```

<!--
11 . Double-click **Package.appxmanifest** to set these capabilities
  that are often required:

  Capabilities set:

  * Internet (Client)
  * Location
-->

12. Fügen Sie alle lokalen Ressourcen (z. b. Bilddateien) aus den vorhandenen plattformprojekten, die erforderlich sind.

## <a name="troubleshooting"></a>Problembehandlung

<a name="target-invocation-exception" />

### <a name="target-invocation-exception-when-using-compile-with-net-native-tool-chain"></a>"Als Ziel aufrufen Ausnahme" Verwendung "Mit .NET Native-toolkette kompilieren"

Wenn die uwp-app wird mehrere auf Assemblys verweisen (z. B. dritte Partei Bibliotheken steuern oder die app selbst wird in mehreren Bibliotheken aufgeteilt), Xamarin.Forms möglicherweise keine Objekte aus diesen Assemblys (z. B. benutzerdefinierte Renderer) zu laden.

Dies kann auftreten, wenn mit der **mit .NET Native-toolkette Kompilieren** ist eine Option für die uwp-apps in der **Eigenschaften > Erstellen > Allgemein** Fenster für das Projekt.

Können Sie korrigieren, indem Sie eine UWP-spezifische Überladung von der `Forms.Init` Aufrufen in **App.xaml.cs** wie im folgenden Code gezeigt (ersetzen Sie `ClassInOtherAssembly` mit eine tatsächliche Klasse der Code verweist):

```csharp
// You'll need to add `using System.Reflection;`
List<Assembly> assembliesToInclude = new List<Assembly>();

// Now, add in all the assemblies your app uses
assembliesToInclude.Add(typeof (ClassInOtherAssembly).GetTypeInfo().Assembly);

// Also do this for all your other 3rd party libraries
Xamarin.Forms.Forms.Init(e, assembliesToInclude);
// replaces Xamarin.Forms.Forms.Init(e);
```

Fügen Sie einen Verweis auf jede Assembly, die von der app verwiesen wird.

#### <a name="dependency-services-and-net-native-compilation"></a>Abhängigkeitsdienste und .NET Native-Kompilierung

Releasebuilds verwenden die .NET Native Kompilierung ausgeführt werden kann, um Abhängigkeitsdienste aufzulösen, die außerhalb der Haupt-app ausführbare Datei (z. B. in einem separaten Projekt oder eine Bibliothek) definiert sind.

Verwenden der `DependencyService.Register<T>()` Methode, um die Abhängigkeit Dienstklassen manuell registrieren. Basierend auf dem obigen Beispiel, fügen Sie die Register-Methode wie folgt hinzu:

```csharp
Xamarin.Forms.Forms.Init(e, assembliesToInclude);
Xamarin.Forms.DependencyService.Register<ClassInOtherAssembly>(); // add this
```
