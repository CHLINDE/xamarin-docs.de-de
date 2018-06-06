---
title: Erste Schritte mit macOS
description: Dieses Dokument beschreibt, wie erste Schritte mit .NET einbetten, mit MacOS. Es erläutert die Anforderungen und stellt eine beispielanwendung, die veranschaulichen, wie Sie die verwaltete Assembly binden und die generierte Ausgabe in Xcode-Projekt verwenden.
ms.prod: xamarin
ms.assetid: AE51F523-74F4-4EC0-B531-30B71C4D36DF
author: topgenorth
ms.author: toopge
ms.date: 11/14/2017
ms.openlocfilehash: 38049eae5e420e5f3610341c2682fa92d2ac426e
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/05/2018
ms.locfileid: "34793688"
---
# <a name="getting-started-with-macos"></a>Erste Schritte mit macOS

## <a name="what-you-will-need"></a>Sie benötigen

* Führen Sie die Anweisungen in der [Einstieg in Objective-C](~/tools/dotnet-embedding/get-started/objective-c/index.md) Handbuch.

## <a name="hello-world"></a>Hello World

Erstellen Sie zuerst ein einfaches Hello World-Beispiel in C# geschrieben.

### <a name="create-c-sample"></a>Erstellen der C#-Beispiel

Öffnen Sie Visual Studio für Mac, erstellen Sie ein neues Mac Class Library-Projekt namens **Hello aus Csharp**, und speichern Sie es **~/Projects/hello-from-csharp**.

Ersetzen Sie den Code in der **MyClass.cs** -Datei mit den folgenden Codeausschnitt:

```csharp
using AppKit;
public class MyNSView : NSTextView
{
    public MyNSView ()
    {
        Value = "Hello from C#";
    }
}
```

Erstellen Sie das Projekt. Die resultierende Assembly als gespeichert **~/Projects/hello-from-csharp/hello-from-csharp/bin/Debug/hello-from-csharp.dll**.

### <a name="bind-the-managed-assembly"></a>Die verwaltete Assembly binden

Nachdem Sie eine verwaltete Assembly haben, müssen binden Sie es, indem .NET Einbetten von aufrufen.

Wie in beschrieben die [Installation](~/tools/dotnet-embedding/get-started/install/install.md) Anleitung hierzu als Postbuildschritt in Ihrem Projekt eine benutzerdefinierte MSBuild-Ziel oder manuell:

```shell
cd ~/Projects/hello-from-csharp
objcgen ~/Projects/hello-from-csharp/hello-from-csharp/bin/Debug/hello-from-csharp.dll --target=framework --platform=macOS-modern --abi=x86_64 --outdir=output -c --debug
```

Das Framework wird in abgelegt **~/Projects/hello-from-csharp/output/hello-from-csharp.framework**.

### <a name="use-the-generated-output-in-an-xcode-project"></a>Verwenden Sie die generierte Ausgabe in einem Xcode-Projekt

Öffnen Sie Xcode, und erstellen Sie eine neue Kakao-Anwendung. Nennen Sie sie **Hello aus Csharp** , und wählen Sie die **Objective-C** Sprache.

Öffnen der **~/Projects/hello-from-csharp/output** Verzeichnis im Finder wählen **Hello aus csharp.framework**, ziehen Sie es in Xcode-Projekt, und legen Sie sie direkt über die **Hello aus Csharp**  Ordner des Projekts.

![Drag & Drop-framework](macos-images/hello-from-csharp-mac-drag-drop-framework.png)

Stellen Sie sicher, dass **Elemente kopieren, bei Bedarf** in der angezeigten Dialogfeld aktiviert ist, und klicken Sie auf **Fertig stellen**.

![Kopieren von Elementen, bei Bedarf](macos-images/hello-from-csharp-mac-copy-items-if-needed.png)

Wählen Sie die **Hello aus Csharp** Projekt, und navigieren Sie zu der **Hello aus Csharp** des Ziels **allgemeine** Registerkarte. In der **eingebettete binäre** Abschnitt, fügen Sie **Hello aus csharp.framework**.

![Eingebettete Binärdateien](macos-images/hello-from-csharp-mac-embedded-binaries.png)

Open **ViewController.m**, und Ersetzen Sie den Inhalt mit:

```objc
#import "ViewController.h"

#include "hello-from-csharp/hello-from-csharp.h"

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    
    MyNSView *view = [[MyNSView alloc] init];
    view.frame = CGRectMake(0, 200, 200, 200);
    [self.view addSubview: view];
}

@end
```

Führen Sie schließlich die Xcode-Projekt, und etwa Folgendes angezeigt wird:

![Hallo von C#-Beispiel im Simulator ausführen](macos-images/hello-from-csharp-mac.png)

Ein Beispiel für umfassendere und kreativer [steht hier](https://github.com/mono/Embeddinator-4000/tree/objc/samples/mac/weather).
