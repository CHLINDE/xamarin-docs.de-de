---
title: Informationen zur App-Xamarin.Essentials
description: Die AppInfo-Klasse stellt Informationen zu Ihrer Anwendung bereit.
ms.assetid: 15924FCB-19E0-45B2-944E-E94FD7AE12FA
author: jamesmontemagno
ms.author: jamont
ms.date: 05/04/2018
ms.openlocfilehash: 4591f1256dc574299bb573ef9ec5afb35af7c542
ms.sourcegitcommit: 3e05b135b6ff0d607bc2378c1b6e66d2eebbcc3e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2018
---
# <a name="xamarinessentials-app-information"></a>Informationen zur App-Xamarin.Essentials

![Vorabversion NuGet](~/media/shared/pre-release.png)

Die **AppInfo** Klasse enthält Informationen zu Ihrer Anwendung.

## <a name="using-appinfo"></a>Mithilfe der AppInfo

Fügen Sie einen Verweis auf Xamarin.Essentials in Ihrer Klasse hinzu:

```csharp
using Xamarin.Essentials;
```

Die folgende Informationen werden über die API verfügbar gemacht:

```csharp
// Application Name
var appName = AppInfo.Name;

// Package Name/Application Identifier (com.microsoft.testapp)
var packageName = AppInfo.PackageName;

// Application Version (1.0.0)
var version = AppInfo.VersionString;

// Application Build Number (1)
var build = AppInfo.BuildString;
```

## <a name="api"></a>API

- [AppInfo-Quellcode](https://github.com/xamarin/Essentials/tree/master/Xamarin.Essentials/AppInfo)
- [AppInfo-API-Dokumentation](xref:Xamarin.Essentials.AppInfo)
