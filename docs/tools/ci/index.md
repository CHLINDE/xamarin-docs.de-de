---
title: "Einführung in die fortlaufende Integration mit Xamarin"
description: "Fortlaufende Integration ist eine Software Engineering-Methode in der ein automatischen Buildvorgang kompiliert und optional testet eine app, wenn Code hinzugefügt oder von Entwicklern im Repository der Versionskontrolle des Projekts geändert. In diesem Artikel werden die allgemeinen Konzepte der kontinuierlichen Integration und einige der verfügbaren Optionen für die kontinuierliche Integration mit Xamarin-Projekten erläutert."
ms.topic: article
ms.prod: xamarin
ms.assetid: 99484E96-DC69-4697-8BBB-1B44C5CBB5ED
ms.technology: xamarin-cross-platform
author: topgenorth
ms.author: toopge
ms.date: 05/04/2017
ms.openlocfilehash: c28389479148829ee87eeda307915aacf7007b21
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2018
---
# <a name="introduction-to-continuous-integration-with-xamarin"></a>Einführung in die fortlaufende Integration mit Xamarin

_Fortlaufende Integration ist eine Software Engineering-Methode in der ein automatischen Buildvorgang kompiliert und optional testet eine app, wenn Code hinzugefügt oder von Entwicklern im Repository der Versionskontrolle des Projekts geändert. In diesem Artikel werden die allgemeinen Konzepte der kontinuierlichen Integration und einige der verfügbaren Optionen für die kontinuierliche Integration mit Xamarin-Projekten erläutert._

> [!Video https://youtube.com/embed/wXgnh2Q7Uv8]


##  <a name="introduction-to-continuous-integrationtoolsciintro-to-cimd"></a>[Einführung in die fortlaufende Integration](~/tools/ci/intro-to-ci.md)

Dieser Abschnitt enthält die verschiedenen Komponenten, die mit dem fortlaufende Integration und ihre Beziehungen sind. Sie enthält die fortlaufende Integration-Umgebungen, die in den entsprechenden Abschnitten weiter unten erläutert werden.

[!include[](~/tools/ci/includes/firewall-information.md)]

## <a name="working-with-continuous-integration-environments"></a>Arbeiten mit Continuous Integration-Umgebung


### <a name="using-app-center-build-with-xamarinappcenterbuildxamarin"></a>[Verwenden von App-Center-Build mit Xamarin](/appcenter/build/xamarin/)

Erstellen von Xamarin.iOS und Xamarin.Android Projektmappen mit App-Center gerade von GitHub VSTS oder Bitbucket.

### <a name="using-teamcity-with-xamarintoolsciteamcitymd"></a>[Verwenden von TeamCity mit Xamarin](~/tools/ci/teamcity.md)

Dieses Handbuch beschreibt die Schritte, die mit der Verwendung von TeamCity zum Kompilieren von mobilen apps und sie mit Xamarin Test Cloud zu senden.

###  <a name="using-jenkins-with-xamarintoolscijenkins-walkthroughmd"></a>[Verwendung von Jenkins mit Xamarin](~/tools/ci/jenkins-walkthrough.md)

Diese Anleitung wird veranschaulicht, wie Jenkins als fortlaufende Integration-Server einrichten und automatisieren Kompilieren von mobilen apps mit Xamarin erstellt wurden. Es wird beschrieben, wie Jenkins unter OS X installieren, um ihn zu konfigurieren, richten Sie Aufträge, Xamarin.iOS und Xamarin.Android apps kompiliert, wenn Änderungen an Versionskontrollsystems übergeben werden.

