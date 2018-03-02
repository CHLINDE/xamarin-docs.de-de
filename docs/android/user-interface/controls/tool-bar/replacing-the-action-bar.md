---
title: Ersetzen der Aktionsleiste
ms.topic: article
ms.prod: xamarin
ms.assetid: 5341D28E-B203-478D-8464-6FAFDC3A4110
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 02/06/2018
ms.openlocfilehash: 91d5612991c2297418cf7003c499c1a1bbfc7558
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2018
---
# <a name="replacing-the-action-bar"></a>Ersetzen der Aktionsleiste

<a name="overview" />

## <a name="overview"></a>Übersicht

Eine der am häufigsten verwendet, für die `Toolbar` ist das Ersetzen der Aktionsleiste standardmäßig mit einem benutzerdefinierten `Toolbar` (wenn ein neues Android-Projekt erstellt wird, verwendet die Aktionsleiste Standard). Da die `Toolbar` bietet die Möglichkeit, mit dem app-Leiste-Abschnitt einer Aktivität mit Branding Logos, Titel, Menüelemente, Navigationsschaltflächen und auch benutzerdefinierte Ansichten hinzufügen-Benutzeroberfläche bietet eine wichtige Aktualisierung über die Standard-Aktionsleiste.

Ersetzen Sie eine app standardmäßig Aktionsleiste mit einem `Toolbar`: 

1.  Erstellen Sie ein neues benutzerdefiniertes Design, und ändern Sie die app-Eigenschaften, sodass das neue Design verwendet. 

2.  Deaktivieren der `windowActionBar` Attribut im benutzerdefinierten Design, und aktivieren Sie die `windowNoTitle` Attribut.

3.  Definieren Sie ein Layout für die `Toolbar`.

4.  Enthalten die `Toolbar` Layout in der Aktivitätssymbols **Main.axml** Layoutdatei. 

5.  Fügen Sie Code hinzu, um der Aktivitätssymbols `OnCreate` Methode zum Suchen der `Toolbar` , und rufen Sie `SetActionBar` zum Installieren der `ToolBar` als der Aktionsleiste.

In den folgenden Abschnitten wird dieser Prozess im Detail erläutert. Eine einfache app wird erstellt und dessen Aktionsleiste ersetzt mit einer benutzerdefinierten `Toolbar`. 


<a name="start_project" />

## <a name="start-an-app-project"></a>Starten Sie ein App-Projekt

Erstellen Sie ein neues Android-Projekt namens **ToolbarFun** (finden Sie unter [Hello, Android](~/android/get-started/hello-android/hello-android-quickstart.md) für Weitere Informationen zum Erstellen eines neuen Android-Projekts). Nachdem das Projekt erstellt wurde, legen Sie die Ziel- und mindestens Android-API-Ebenen auf **Android 5.0.x (API-Ebene 21 - Lollipop)**. Weitere Informationen zu Android Versionsebenen festlegen, finden Sie unter [Grundlegendes zu Android-API-Ebenen](~/android/app-fundamentals/android-api-levels.md). Wenn die app erstellt und ausgeführt wird, zeigt die Aktionsleiste Standard, wie in diesem Screenshot dargestellt: 

[![Screenshot der Aktionsleiste Standard](replacing-the-action-bar-images/01-before-sml.png)](replacing-the-action-bar-images/01-before.png)


<a name="custom_theme" />

## <a name="create-a-custom-theme"></a>Erstellen Sie ein benutzerdefiniertes Design

Öffnen der **Ressourcen/Werte** Verzeichnis und erstellen eine neue Datei namens **styles.xml**. Ersetzen Sie den Inhalt durch folgendes XML: 

```xml
<?xml version="1.0" encoding="utf-8" ?>
<resources>
  <style name="MyTheme" parent="@android:style/Theme.Material.Light.DarkActionBar">
    <item name="android:windowNoTitle">true</item>
    <item name="android:windowActionBar">false</item>
    <item name="android:colorPrimary">#5A8622</item>
  </style>
</resources>
```

Diese XML-Datei definiert, ein neues benutzerdefiniertes Design aufgerufen **MeineDesigns** auf Grundlage der **Theme.Material.Light.DarkActionBar** Design in Lollipop. Die `windowNoTitle` -Attributsatz zur `true` So blenden Sie die Titelleiste aus: 

```xml
<item name="android:windowNoTitle">true</item>
```

Zum Anzeigen der benutzerdefinierten Symbolleiste standardmäßig `ActionBar` muss deaktiviert werden: 

```xml
<item name="android:windowActionBar">false</item>
```

Ein Olivgrün gefärbt `colorPrimary` Einstellung wird für die Hintergrundfarbe der Symbolleiste verwendet: 
 
```xml
<item name="android:colorPrimary">#5A8622</item>
```

Bearbeiten Sie **Properties/AndroidManifest.xml** und fügen Sie die folgenden `android:theme` -Attribut auf die `<application>` Element so, dass die app verwendet die `MyTheme` benutzerdefiniertes Design: 

```xml
<application android:label="@string/app_name" android:theme="@style/MyTheme"></application>
```

Weitere Informationen zum Anwenden von eines benutzerdefinierten Designs an eine app, finden Sie unter [mithilfe von benutzerdefinierten Designs](~/android/user-interface/material-theme.md#customtheme). 


<a name="toolbar_layout" />

## <a name="define-a-toolbar-layout"></a>Definieren Sie eine Symbolleistenlayout

In der **Ressourcen/Layout** Verzeichnis erstellen Sie eine neue Datei namens **toolbar.xml**. Ersetzen Sie den Inhalt durch folgendes XML: 

```xml
<?xml version="1.0" encoding="utf-8"?>
<Toolbar xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/toolbar"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:minHeight="?android:attr/actionBarSize"
    android:background="?android:attr/colorPrimary"
    android:theme="@android:style/ThemeOverlay.Material.Dark.ActionBar"/>
```

Diese XML-Datei definiert die benutzerdefinierte `Toolbar` die Standard-Aktionsleiste ersetzt. Die Mindesthöhe der `Toolbar` festgelegt ist, auf die Größe des Balkens Aktion, die diese Kombination ersetzt: 

```csharp
android:minHeight="?android:attr/actionBarSize"
```

Die Hintergrundfarbe der `Toolbar` festgelegt ist, auf die zuvor definierte Olivgrün gefärbt Farbe **styles.xml**:

```csharp
android:background="?android:attr/colorPrimary"
```

Lollipop, ab der `android:theme` Attribut kann verwendet werden, um eine einzelne Ansicht formatieren. Die `ThemeOverlay.Material` Designs Lollipop eingeführten ermöglichen, überlagern Sie die Standardeinstellung `Theme.Material` Designs, überschreiben die relevanten Attribute zum entweder hell oder dunkel machen. In diesem Beispiel wird die `Toolbar` verwendet ein Design "dunkel", damit dessen Inhalt helle Farbe sind: 

```csharp
android:theme="@android:style/ThemeOverlay.Material.Dark.ActionBar"
```

Diese Einstellung wird verwendet, sodass Menüelemente mit dunkleren Farbe des Hintergrunds für Vergleiche.


<a name="include_layout" />

## <a name="include-the-toolbar-layout"></a>Schließen Sie das Symbolleistenlayout

Bearbeiten Sie die Layoutdatei **Resources/layout/Main.axml** und Ersetzen Sie den Inhalt durch folgendes XML:

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <include
        android:id="@+id/toolbar"
        layout="@layout/toolbar" />
    <Button
        android:id="@+id/MyButton"
        android:layout_below="@+id/toolbar"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Hello World, Click Me!" />
</RelativeLayout>
```

Dieses Layout enthält die `Toolbar` in definierten **toolbar.xml** und verwendet eine `RelativeLayout` angeben, dass die `Toolbar` ganz oben auf der Benutzeroberfläche (über die Schaltfläche "") platziert werden soll. 


<a name="activate_toolbar" />

## <a name="find-and-activate-the-toolbar"></a>Suchen Sie und aktivieren Sie die Symbolleiste

Bearbeiten Sie **MainActivity.cs** und fügen Sie die folgende Anweisung:

```csharp
using Android.Views;
```

Darüber hinaus die folgenden Codezeilen hinzufügen, bis zum Ende der `OnCreate` Methode:

```csharp
var toolbar = FindViewById<Toolbar>(Resource.Id.toolbar);
SetActionBar(toolbar);
ActionBar.Title = "My Toolbar";
```

Dieser Code sucht den `Toolbar` und ruft `SetActionBar` , damit die `Toolbar` auf standardmäßige Aktion Leiste Merkmalen dauert. Der Titel der Symbolleiste geändert wird, um **Meine Symbolleiste**. Wie in diesem Codebeispiel wird die `ToolBar` als eine Aktionsleiste direkt verwiesen werden kann. Kompilieren und Ausführen dieser app &ndash; den angepassten `Toolbar` wird anstelle der Standardeinstellung Aktionsleiste angezeigt: 

[![Screenshot der angepassten Symbolleiste mit Grün-Schema](replacing-the-action-bar-images/02-after-sml.png)](replacing-the-action-bar-images/02-after.png)

Beachten Sie, dass die `Toolbar` formatiert wird, unabhängig von der `Theme.Material.Light.DarkActionBar` Design, das für den Rest der app angewendet wird. 


<a name="main_menus" />
 
## <a name="add-menu-items"></a>Hinzufügen von Menüelementen 

In diesem Abschnitt werden Menüs hinzugefügt, die `Toolbar`. Im oberen rechten Bereich des der `ToolBar` ist reserviert für Menüelemente &ndash; jedes Menüelement (so genannte ein *Aktionselement, über das*) eine Aktion innerhalb der aktuellen Aktivität ausführen oder sie können eine Aktion für die gesamte app ausführen. 

Hinzufügen von Menüs zu dem `Toolbar`: 

1.  Fügen Sie im Menüsymbole (falls erforderlich) die `mipmap-` Ordner des app-Projekts. Google bietet eine Reihe von freien Symbole auf der [Material Symbole](https://design.google.com/icons/) Seite. 

2.  Definieren Sie den Inhalt der Menüelemente durch Hinzufügen einer neuen Menü Ressourcendatei unter **Ressourcen/Menü**. 

3.  Implementieren der `OnCreateOptionsMenu` -Methode der Aktivität &ndash; diese Methode vergrößert die Menüelemente. 

4.  Implementieren der `OnOptionsItemSelected` -Methode der Aktivität &ndash; diese Methode führt eine Aktion aus, wenn ein Menüelement abgerufen werden. 

Die folgenden Abschnitte zeigen diesen Vorgang im Detail durch Hinzufügen von **bearbeiten** und **speichern** Menüelemente, die angepasste `Toolbar`. 


<a name="menu_icons" />

### <a name="install-menu-icons"></a>Installieren Sie im Menüsymbole

Fortsetzen der `ToolbarFun` Beispiel-app fügen Sie im Menüsymbole der app-Projekt. Herunterladen [Symbolleiste icons.zip](https://github.com/xamarin/monodroid-samples/blob/master/Supportv7/AppCompat/Toolbar/Resources/toolbar-icons.zip?raw=true) und Entpacken Sie es. Kopieren Sie den Inhalt von den extrahierten *Mipmap -* Ordnern dem Projekt *Mipmap -* Ordner unter **ToolbarFun/Ressourcen** und jede hinzugefügte Icon-Datei in das Projekt einfügen.

<a name="menu_resource" />

### <a name="define-a-menu-resource"></a>Definieren Sie eine Menüressource

Erstellen Sie ein neues **Menü** Unterverzeichnis **Ressourcen**. In der **Menü** Unterverzeichnis erstellen eine neue Menü Ressourcendatei namens **top_menus.xml** und Ersetzen Sie den Inhalt durch folgendes XML: 

```xml
<?xml version="1.0" encoding="utf-8" ?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
  <item
       android:id="@+id/menu_edit"
       android:icon="@mipmap/ic_action_content_create"
       android:showAsAction="ifRoom"
       android:title="Edit" />
  <item
       android:id="@+id/menu_save"
       android:icon="@mipmap/ic_action_content_save"
       android:showAsAction="ifRoom"
       android:title="Save" />
  <item
       android:id="@+id/menu_preferences"
       android:showAsAction="never"
       android:title="Preferences" />
</menu>
```

Durch dieses XML werden drei Menüelemente erstellt:

-   Ein **bearbeiten** Menüelement, das verwendet die `ic_action_content_create.png` Symbol (ein Stift). 

-   Ein **speichern** Menüelement, das mithilfe der `ic_action_content_save.png` Symbol (eine Diskette). 

-   Ein **Voreinstellungen** Menüelement, das nicht über ein Symbol verfügt.

Die `showAsAction` Attribute der **bearbeiten** und **speichern** Menüelemente werden festgelegt, um `ifRoom` &ndash; diese Einstellung bewirkt, dass diese Menüelemente angezeigt werden die `Toolbar` liegt ausreichend Speicherplatz vorhanden, damit sie angezeigt werden. Die **Voreinstellungen** Menü Element legt `showAsAction` auf `never` &ndash; Dies bewirkt, dass die **Voreinstellungen** Menü angezeigt werden die *Überlauf* Menü (drei vertikale Punkte). 

<a name="on_create_options_menu" />

### <a name="implement-oncreateoptionsmenu"></a>Implementieren von OnCreateOptionsMenu

Fügen Sie die folgende Methode hinzu **MainActivity.cs**:

```csharp
public override bool OnCreateOptionsMenu(IMenu menu)
{
    MenuInflater.Inflate(Resource.Menu.top_menus, menu);
    return base.OnCreateOptionsMenu(menu);
}
```

Android Aufrufe der `OnCreateOptionsMenu` Methode, damit die app die Menüressource für eine Aktivität angeben kann. Bei dieser Methode die **top_menus.xml** Ressource aufgebläht wird in den übergebenen `menu`. Dieser Code bewirkt, dass die neue **bearbeiten**, **speichern**, und **Voreinstellungen** Menüelemente angezeigt werden die `Toolbar`. 


<a name="on_options_item_selected" />

### <a name="implement-onoptionsitemselected"></a>Implementieren von OnOptionsItemSelected

Fügen Sie die folgende Methode hinzu **MainActivity.cs**:

```csharp
public override bool OnOptionsItemSelected(IMenuItem item)
{
    Toast.MakeText(this, "Action selected: " + item.TitleFormatted,
        ToastLength.Short).Show();
    return base.OnOptionsItemSelected(item);
}
```

Wenn ein Benutzer ein Menüelement tippt, Android Ruft die `OnOptionsItemSelected` -Methode auf und übergibt das Menüelement, das ausgewählt wurde. In diesem Beispiel zeigt die Implementierung gerade ein Popups, um anzugeben, welche Menüelement abgerufen wurde. 

Erstellen und ausführen `ToolbarFun` neue Menüelemente in der Symbolleiste angezeigt. Die `Toolbar` zeigt jetzt drei Symbole aus, wie in diesem Screenshot dargestellt: 

[![Diagramm zur Veranschaulichung Speicherorte der bearbeiten, speichern und Menüelemente "Überlauf"](replacing-the-action-bar-images/04-menu-items-sml.png)](replacing-the-action-bar-images/04-menu-items.png)

Wenn ein Benutzer Taps der **bearbeiten** Menüelement klicken, einen Toast wird angezeigt, um anzugeben, dass die `OnOptionsItemSelected` -Methode wurde aufgerufen: 

[![Screenshot der Toast angezeigt, wenn bearbeiten Element abgerufen werden](replacing-the-action-bar-images/05-toast-displayed-sml.png)](replacing-the-action-bar-images/05-toast-displayed.png)

Wenn ein Benutzer die Überlaufmenü tippt der **Voreinstellungen** Menüelement angezeigt wird. In der Regel weniger übliche Aktionen im Menü "Überlauf" platziert werden sollten &ndash; in diesem Beispiel verwendet die Überlaufmenü für **Voreinstellungen** , da sie nicht so oft verwendet wird als **bearbeiten** und  **Speichern Sie**: 

[![Screenshot der Voreinstellungen-Menüelement, das im Menü "Überlauf" wird angezeigt.](replacing-the-action-bar-images/06-preferences-sml.png)](replacing-the-action-bar-images/06-preferences.png)

Weitere Informationen zu Android-Menüs, finden Sie in der Android-Entwickler [Menüs](https://developer.android.com/guide/topics/ui/menus.html) Thema. 
 



## <a name="related-links"></a>Verwandte Links

- [Lollipop-Symbolleiste (Beispiel)](https://developer.xamarin.com/samples/monodroid/android5.0/Toolbar/)
- [AppCompat-Symbolleiste (Beispiel)](https://developer.xamarin.com/samples/monodroid/Supportv7/AppCompat/Toolbar/)