---
title: Benutzerprofil
ms.topic: article
ms.prod: xamarin
ms.assetid: 1C58E12B-4634-4691-BF59-D5A3F6B0E6F7
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 06/21/2017
ms.openlocfilehash: 53ac30abea05095583fcac5ddc315f93ce7024f2
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2018
---
# <a name="user-profile"></a>Benutzerprofil

Aufzählen von Kontakten mit Android unterstützt die `ContactsContract` Anbieter seit API-Ebene 5. Um z. B. auf die Liste Kontakte ist so einfach wie mit der `ContactContracts.Contacts` -Klasse, wie im folgenden Code dargestellt:

```csharp
var uri = ContactsContract.Contacts.ContentUri;
           
string[] projection = {
    ContactsContract.Contacts.InterfaceConsts.Id,
    ContactsContract.Contacts.InterfaceConsts.DisplayName };
           
var cursor = ManagedQuery (uri, projection, null, null, null);
           
if (cursor.MoveToFirst ()) {
    do {
        Console.WriteLine ("Contact ID: {0}, Contact Name: {1}",
            cursor.GetString (cursor.GetColumnIndex (projection [0])),
            cursor.GetString (cursor.GetColumnIndex (projection [1])));
                   
    } while (cursor.MoveToNext());
}
```

Mit Android 4 (API-Ebene 14) ein neues `ContactsContact.Profile` Klasse über den ContactsContract-Anbieter verfügbar ist. Die `ContactsContact.Profile` Zugang zu einem persönlichen Profil für den Besitzer eines Geräts, die Kontaktdaten, z. B. Name und Phone Besitzer des Geräts umfasst.

<a name="Required_Permissions" />

## <a name="required-permissions"></a>Erforderliche Berechtigungen

Zum Lesen und Schreiben von Daten, Anwendungen anfordern müssen die `Read_Contacts` und `Write_Contacts` Berechtigungen bzw. Darüber hinaus zum Lesen und bearbeiten das Benutzerprofil, Anwendungen müssen anfordern der `Read_Profile` und `Write_Profile` Berechtigungen.

<a name="Updating_Profile_Data" />

## <a name="updating-profile-data"></a>Aktualisieren von Profildaten

Sobald diese Berechtigungen festgelegt wurden, kann eine Anwendung normale Android Techniken verwenden, für die Interaktion mit Daten für das Benutzerprofil. Beispielsweise, um den Anzeigenamen für das Profil aktualisieren nennen wir `ContentResolver.Update` mit einer `Uri` abgerufen, die über die `ContactsContract.Profile.ContentRawContactsUri` -Eigenschaft verwenden, wie unten dargestellt:

```csharp
var values = new ContentValues ();
          
values.Put (ContactsContract.Contacts.InterfaceConsts.DisplayName,
    "John Doe");
           
ContentResolver.Update (ContactsContract.Profile.ContentRawContactsUri,
    values, null, null);
```

<a name="Reading_Profile_Data" />

## <a name="reading-profile-data"></a>Lesen von Profildaten

Ausgeben einer Abfrage, die `ContactsContact.Profile.ContentUri` Lesevorgänge zurück, die Profildaten. Im folgende Code wird z. B. Anzeigenamen für das Benutzerprofil lesen:

```csharp
string[] projection = {
    ContactsContract.Contacts.InterfaceConsts.DisplayName };
           
var cursor = ManagedQuery (uri, projection, null, null, null);

if (cursor.MoveToFirst ()) {
    Console.WriteLine(
        cursor.GetString (cursor.GetColumnIndex (projection [0])));
}
```

<a name="Navigating_to_the_People_App" />

## <a name="navigating-to-the-people-app"></a>Navigieren zur App Personen

Um das Benutzerprofil in das neue Kontakte-app zu navigieren, die mit Android 4 ausgeliefert wird, einfach erstellen Sie abschließend Priorität mit einer `ActionView` Aktion und ein `ContactsContract.Profile.ContentUri`, und übergeben sie an die `StartActivity` Methode wie folgt:

```csharp
var intent = new Intent (Intent.ActionView,
    ContactsContract.Profile.ContentUri);           
StartActivity (intent);
```

Bei der Ausführung des obigen Codes lädt die Kontakte-app das Benutzerprofil, wie im folgenden Screenshot gezeigt:

[![Screenshot der Kontakte-app, die das Benutzerprofil John Doe anzeigen](user-profile-images/15-people-app.png)](user-profile-images/15-people-app.png)

Arbeiten mit dem Benutzerprofil ist jetzt etwa dem interagieren mit anderen Daten in Android und bietet ein höheres Maß an Gerät Personalisierung.



## <a name="related-links"></a>Verwandte Links

- [ContactsProviderDemo (Beispiel)](https://developer.xamarin.com/samples/monodroid/ContactsProviderDemo/)
- [Einführung in Eis Rustikal Sandwich](http://www.android.com/about/ice-cream-sandwich/)
- [Android 4.0 Platform](http://developer.android.com/sdk/android-4.0.html)
