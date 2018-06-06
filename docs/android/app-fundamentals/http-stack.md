---
title: HttpClient-Stapel und Implementierung von SSL/TLS-Selektor für Android
description: Der Stapel für "HttpClient" und die Implementierung von SSL/TLS-Selektoren bestimmen die "HttpClient" und SSL/TLS-Implementierung, die von Ihrer Xamarin.Android-apps verwendet wird.
ms.prod: xamarin
ms.assetid: D7ABAFAB-5CA2-443D-B902-2C7F3AD69CE2
ms.technology: xamarin-android
author: topgenorth
ms.author: toopge
ms.date: 04/20/2018
ms.openlocfilehash: 765c51346ac63a00838fec52bde87b38091e2dd9
ms.sourcegitcommit: a4c2a63ba76b839cda99e4474e7ab46fe307cd39
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2018
ms.locfileid: "34689473"
---
# <a name="httpclient-stack-and-ssltls-implementation-selector-for-android"></a>HttpClient-Stapel und Implementierung von SSL/TLS-Selektor für Android

Der Stapel für "HttpClient" und die Implementierung von SSL/TLS-Selektoren bestimmen die "HttpClient" und SSL/TLS-Implementierung, die von Ihrer Xamarin.Android-apps verwendet wird.

Projekte verweisen müssen die **System.Net.Http** Assembly.

> [!WARNING]
> **April, 2018** – aufgrund der erhöhten Sicherheit Anforderungen, einschließlich der PCI-Konformität Hauptversion Cloud-Anbieter und der Webserver unterstützen TLS-Versionen, die älter sind als 1.2 zu beenden.  Xamarin-Projekte erstellt, die in früheren Versionen von Visual Studio standardmäßig die frühere Versionen von TLS zu verwenden.
>
> Um sicherzustellen, dass Ihre apps mit diesen Servern und -Dienste, funktionieren weiterhin **sollten Sie Ihre Projekte Xamarin mit Aktualisieren der `Android HttpClient` und `Native TLS 1.2` Einstellungen sehen Sie unten, klicken Sie dann erneut erstellen und erneut bereitstellen Ihrer apps** zu Ihrem Benutzer.

# <a name="visual-studiotabwindows"></a>[Visual Studio](#tab/windows)

Die Konfiguration Xamarin.Android "HttpClient" befindet sich in **Projektoptionen > Android Options**, klicken Sie dann auf die **erweiterte Optionen** Schaltfläche.

Dies sind die empfohlenen Einstellungen für TLS 1.2-Unterstützung:

[![Visual Studio-Android-Optionen](http-stack-images/android-win-sml.png)](http-stack-images/android-win.png#lightbox)


# <a name="visual-studio-for-mactabmacos"></a>[Visual Studio für Mac](#tab/macos)

Die Konfiguration Xamarin.Android "HttpClient" befindet sich in **Projektoptionen > Erstellen > Android erstellen** Einstellungen, und klicken Sie auf die **allgemeine** Registerkarte.

Dies sind die empfohlenen Einstellungen für TLS 1.2-Unterstützung:

[![Visual Studio für Mac-Android-Optionen](http-stack-images/android-mac-sml.png)](http-stack-images/android-mac.png#lightbox)

-----

## <a name="alternative-configuration-options"></a>Alternative Konfigurationsoptionen

### <a name="androidclienthandler"></a>AndroidClientHandler

AndroidClientHandler ist der neue Handler, der in systemeigenen Java/OS Code anstatt zu implementieren alles, was in verwaltetem Code delegiert.
**Dies ist die empfohlene Option.**

#### <a name="pros"></a>IT-Spezialisten

- Verwenden Sie für eine bessere Leistung und geringer Größe ausführbarer systemeigenen API.
- Unterstützung für die aktuellsten Standards, z. B. ein. TLS 1.2.

#### <a name="cons"></a>Nachteile

- Erfordert Android 5.0 oder höher.
- Einige "HttpClient" Features/Optionen sind nicht verfügbar.

### <a name="managed-httpclienthandler"></a>Verwaltete (HttpClientHandler)

Verwaltete Handler ist der vollständig verwalteter HttpClient-Handler, der mit früheren Versionen von Xamarin.Android geliefert wurde.

#### <a name="pros"></a>IT-Spezialisten

- Die meisten kompatibel (Features) mit MS .NET und ältere Versionen von Xamarin ist.

#### <a name="cons"></a>Nachteile

- Es ist nicht vollständig mit dem Betriebssystem (z. b. integriert beschränkt auf TLS 1.0).
- Es ist in der Regel sehr viel langsamer ist (z. b. Verschlüsselung) als systemeigene API.
- Es ist mehr verwalteten Code, Erstellen von größeren Anwendungen erforderlich.



### <a name="choosing-a-handler"></a>Wählen einen Handler

Die Wahl zwischen `AndroidClientHandler` und `HttpClientHandler` hängt von den Anforderungen Ihrer Anwendung. `AndroidClientHandler` wird z. B. für die aktuelle sicherheitsunterstützung für empfohlen.

-   Es ist erforderlich, dass die Unterstützung von TLS 1.2 +.
-   Ihre app Android 5.0.x (API 21) vorgesehen ist oder höher.
-   Sie benötigen die TLS 1.2-Unterstützung für `HttpClient`.
-   Sie müssen nicht die TLS 1.2 +-Unterstützung für `WebClient`.

`HttpClientHandler` ist eine gute Wahl, wenn Sie TLS 1.2 + benötigen jedoch muss Unterstützung für Android-Versionen vor Android 5.0. Es ist auch eine gute Wahl, wenn die gewünschte TLS 1.2-Unterstützung für `WebClient`.

Beginnend mit Xamarin.Android 8.3 `HttpClientHandler` standardmäßig Ausdrehen SSL (`btls`) als den zugrunde liegenden TLS-Anbieter. Der Ausdrehen SSL TLS-Anbieter bietet folgende Vorteile:

-   TLS 1.2 + unterstützt.
-   Alle Android-Versionen unterstützt.
-   Es bietet TLS 1.2 +-Unterstützung für beide `HttpClient` und `WebClient`.

Der Nachteil der Verwendung von SSL Ausdrehen als fangen TLS-Anbieter ist, dass es die Größe der resultierenden APK erhöhen kann (ungefähr 1MB zusätzlicher APK-Größe pro unterstützten ABI hinzugefügt).

8.3-Xamarin.Android ab, der TLS-Standardanbieter ist SSL Ausdrehen (`btls`). Wenn Sie nicht Ausdrehen SSL verwenden möchten, können Sie wiederherstellen, die Verlaufsdaten verwaltete SSL-Implementierung durch Festlegen der `$(AndroidTlsProvider)` Eigenschaft `legacy` (Weitere Informationen zu den Einstellungseigenschaften für Build, finden Sie unter [Buildprozess](~/android/deploy-test/building-apps/build-process.md)).


### <a name="programatically-using-androidclienthandler"></a>Programmgesteuertes verwenden. `AndroidClientHandler`

Die `Xamarin.Android.Net.AndroidClientHandler` ist ein `HttpMessageHandler` Implementierung speziell für Xamarin.Android.
Instanzen dieser Klasse verwendet das systemeigene `java.net.URLConnection` Implementierung für alle HTTP-Verbindungen. Dadurch erhalten theoretisch die Leistung der HTTP-Anforderungen sowie kleinere APK-Größen.

Dieser Codeausschnitt ist ein Beispiel zum explizit für eine einzelne Instanz der `HttpClient` Klasse:

```csharp
// Android 5.0 or higher, Xamarin.Android 6.1 or higher
HttpClient client = new HttpClient(new Xamarin.Android.Net.AndroidClientHandler ());
```

> [!NOTE]
> Das zugrunde liegende Android-Gerät muss (d. h. TLS 1.2-Unterstützung Android 5.0 und höher)


## <a name="ssltls-implementation-build-option"></a>Buildoption SSL/TLS-Implementierung

Diese Option "Project" steuert, welche zugrunde liegenden TLS-Bibliothek von allen Web-Anforderung verwendet werden beide `HttpClient` und `WebRequest`. Standardmäßig wird die TLS 1.2 ausgewählt:

# <a name="visual-studiotabwindows"></a>[Visual Studio](#tab/windows)

[![Implementierung von TLS/SSL-Kombinationsfeld in Visual Studio](http-stack-images/tls06-vs.png)](http-stack-images/tls05-vs.png#lightbox)

# <a name="visual-studio-for-mactabmacos"></a>[Visual Studio für Mac](#tab/macos)

[![Implementierung von TLS/SSL-Kombinationsfeld in Visual Studio für Mac](http-stack-images/tls06-xs.png)](http-stack-images/tls05-xs.png#lightbox)

-----

Zum Beispiel:

```csharp
var client = new HttpClient();
```

Wenn die Implementierung für "HttpClient", um festgelegt wurde **verwaltet** und auf die TLS-Implementierung festgelegt wurde **Native TLS 1.2 +**, und klicken Sie dann die `client` Objekt verwenden automatisch die verwaltete `HttpClientHandler` und TLS 1.2 (bereitgestellt von der Bibliothek BoringSSL) für die HTTP-Anforderungen.

Jedoch wenn die **"HttpClient" Implementierung** auf festgelegt ist `AndroidHttpClient`, klicken Sie dann alle `HttpClient` Objekte werden die zugrunde liegenden Java-Klasse verwenden `java.net.URLConnection` und sind nicht betroffen von der **TLS/SSL-Implementierung** Wert. `WebRequest` Objekte, würde die BoringSSL-Bibliothek verwenden.

## <a name="other-ways-to-control-ssltls-configuration"></a>Andere Möglichkeiten zum Steuern von SSL/TLS-Konfiguration

Es gibt drei Möglichkeiten, um eine Anwendung Xamarin.Android steuern, die TLS-Einstellungen:

1. Wählen Sie die "HttpClient" Implementierung und Standard-TLS-Bibliothek, in den Projekt-Optionen.
2. Programmgesteuert mithilfe von `Xamarin.Android.Net.AndroidClientHandler`.
3. Deklarieren Sie Umgebungsvariablen (optional).

Der drei Optionen, die empfohlene Vorgehensweise ist die Verwendung der Xamarin.Android-Projektoptionen deklarieren Sie die Standardeinstellung `HttpMessageHandler` und TLS für die gesamte app. Klicken Sie dann bei Bedarf programmgesteuert instanziieren `Xamarin.Android.Net.AndroidClientHandler` Objekte. Diese Optionen sind oben beschrieben.

Die dritte Option &ndash; Verwenden von Umgebungsvariablen &ndash; nachfolgend beschrieben.

### <a name="declare-environment-variables"></a>Deklarieren von Umgebungsvariablen

Es gibt zwei Umgebungsvariablen, die für die Verwendung von TLS in Xamarin.Android beziehen:

- `XA_HTTP_CLIENT_HANDLER_TYPE` &ndash; Diese Umgebungsvariable wird deklariert, den Standardwert `HttpMessageHandler` , die die Anwendung verwenden. Zum Beispiel:

    ```csharp
    XA_HTTP_CLIENT_HANDLER_TYPE=Xamarin.Android.Net.AndroidClientHandler
    ```

- `XA_TLS_PROVIDER` &ndash; Diese Umgebungsvariable wird die TLS-Bibliothek verwendet werden soll, entweder deklarieren `btls`, `legacy`, oder `default` (Dies ist identisch mit dieser Variable auslassen):

    ```csharp
    XA_TLS_PROVIDER=btls
    ```

Diese Umgebungsvariable wird festgelegt, durch Hinzufügen einer _Umgebungsdatei_ zum Projekt. Eine umgebungs-Datei ist eine Unix-Format nur-Text-Datei mit dem Buildvorgang **AndroidEnvironment**:

# <a name="visual-studiotabwindows"></a>[Visual Studio](#tab/windows)

![Screenshot des Buildvorgangs AndroidEnvironment in Visual Studio.](http-stack-images/tls03-vs.png)

# <a name="visual-studio-for-mactabmacos"></a>[Visual Studio für Mac](#tab/macos)

![Screenshot der AndroidEnvironment Buildvorgang in Visual Studio für Mac.](http-stack-images/tls03-xs.png)

-----

Finden Sie unter der [Xamarin.Android Umgebung](~/android/deploy-test/environment.md) ausführliche Informationen zu Umgebungsvariablen und Xamarin.Android-Handbuch.


## <a name="related-links"></a>Verwandte Links

- [Transport Layer Security (TLS)](~/cross-platform/app-fundamentals/transport-layer-security.md)
