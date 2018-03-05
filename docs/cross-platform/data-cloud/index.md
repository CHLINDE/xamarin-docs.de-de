---
title: Microsoft Azure
description: "Dokumentation und Beispielcode für Azure-downloads."
ms.topic: article
ms.prod: xamarin
ms.assetid: 7b9aa8d9-c181-4c33-8ab0-2f56e4dbfc04
ms.technology: xamarin-cross-platform
author: asb3993
ms.author: amburns
ms.date: 10/09/2017
ms.openlocfilehash: 55213de8d2c93349598bcc9b10232535f09bc3d6
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2018
---
# <a name="microsoft-azure"></a>Microsoft Azure

_Dokumentation und Beispielcode für Azure-downloads._

[ ![](images/evolve-mikej-azure-sml.png "Azure App Services-Funktionen sind einfach zu Xamarin-Apps, einschließlich cloudspeicherung von Daten und plattformübergreifende Pushbenachrichtigungen hinzufügen")](https://evolve.xamarin.com/session/56ec886fde91c6253c277bc6)

[Entwickeln 2016: Verbundenen Apps mithilfe von Azure und Xamarin entwickeln](https://evolve.xamarin.com/session/56ec886fde91c6253c277bc6)

## <a name="connected-services-in-visual-studio-for-mac"></a>Von verbundenen Diensten in Visual Studio für Mac

Die neue [verbundene Dienste](connected-services.md) Funktion von Visual Studio für Mac kann Entwickler schnell und einfach für mobile Anwendungen aus der IDE Funktionen der Azure hinzufügen. Verfügbar für Tests in den Alpha-Kanal.


## <a name="azure-app-services"></a>Azure App Services

Es ist eine Sammlung von [Azure Mobile Apps Dokumentation](~/cross-platform/data-cloud/mobile-apps.md) führt, die Sie durch den Prozess der Implementierung der [Azure Mobile Client](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/).
Xamarin bietet auch eine Azure-Messaging NuGet-Pakete für [iOS](https://www.nuget.org/packages/Xamarin.Azure.NotificationHubs.iOS/) und [Android](https://www.nuget.org/packages/Xamarin.Azure.NotificationHubs.Android/) Pushbenachrichtigungen plattformübergreifend implementieren können.

Konfigurieren Sie Ihre apps auf die [Azure App Services-Portal](https://portal.azure.com/) auf Mobile Apps, Web-APIs, Speicher und vieles mehr. Erfahren Sie mehr über [wie app-Dienste unterscheiden](http://azure.microsoft.com/en-us/updates/whats-new-with-azure-app-service/) und sehen Sie sich [diese Videos von Microsoft](http://azure.microsoft.com/en-us/campaigns/azure-march-announcement/).

## <a name="active-directory-authentication"></a>Active Directory-Authentifizierung

[Azure Active Directory](~/cross-platform/data-cloud/active-directory/index.md) können verwendet werden, um die Anmeldung von Benutzern im Xamarin-apps über die [Xamarin.Auth Komponente](https://www.nuget.org/packages/Xamarin.Auth/).
Die apps können Sie weitere Dienste wie Office 365 zugreifen.

## <a name="webapi"></a>WebAPI

Microsoft Web-API macht eine REST-ähnliche-Schnittstelle, die problemlos von Xamarin-Anwendungen genutzt werden kann.
Sie können leicht Hochfahren ein [Azure-Website](https://trywebsites.azurewebsites.net/) , und erstellen Sie eine WebAPI-basierten Anwendung zur Verbindung mit Xamarin-apps.


###  <a name="introduction-to-web-servicescross-platformdata-cloudweb-servicesindexmd"></a>[Einführung in Webdienste](~/cross-platform/data-cloud/web-services/index.md)

In diesem Lernprogramm erläutert, wie REST, integrieren WCF und SOAP-Webdienst-diensttechnologien mit Xamarin mobile Anwendungen. Verschiedene dienstimplementierungen untersucht, wertet verfügbare Tools und Bibliotheken, die sie integrieren und bietet von Beispiel-Muster für die Nutzung von Daten. Schließlich bietet es eine grundlegende Übersicht über die zum Erstellen einen RESTful-Webdienst zur Verwendung mit einer mobilen Anwendung von Xamarin.

## <a name="samples"></a>Proben

Zusätzlich zu den [Dokumentationsbeispiele](https://github.com/xamarin/mobile-samples/tree/master/Azure), die folgenden vollständige Anwendungen veranschaulichen verschiedene Funktionen von Azure in die Xamarin-apps integriert:

- [Sport](https://github.com/xamarin/Sport) – angezeigten Sport-League Tracking-app, die Daten Speicher und Push-Benachrichtigungen verwendet.
- [Momente](https://github.com/pierceboggan/Moments) – sofortige Foto freigeben, die Azure-Speicher für Bilder verwendet.
- [Xamarin CRM](https://github.com/xamarin/app-crm) – Web-API für das Back-End verwendet.
- [MyShoppe](https://github.com/jamesmontemagno/MyShoppe) -Azure-Mobile Apps.

- [Shopping](https://github.com/dotnet-architecture/eShopOnContainers) – Beispiel für die [Architektur Reihe](https://www.microsoft.com/net/learn/architecture) der e-Books.
- [MyDriving](https://azure.microsoft.com/en-us/campaigns/mydriving/) – Azure + IoT-Beispiels in Build 2016.


## <a name="related-links"></a>Verwandte Links

- [Azure PCL-Beispiel (durch @paulbatum) (Beispiel)](https://github.com/paulbatum/mobile-services-xamarin-pcl)
- [Azure-portal](http://azure.microsoft.com/)
- [Mobilen Client für Xamarin (NuGet)](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/)
