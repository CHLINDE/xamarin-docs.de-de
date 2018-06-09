---
title: Xamarin.Forms Zellen
description: Xamarin.Forms Zellen können Listenansichten und TableViews hinzugefügt werden. In diesem Artikel werden die Zellen enthalten in Xamarin.Forms aufgelistet.
ms.prod: xamarin
ms.assetid: 77DA0C89-35D6-4C09-A072-3ADE53FD56CF
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 01/12/2016
ms.openlocfilehash: 0947027b43eacd0bac269ebf7a779746e0d22866
ms.sourcegitcommit: 66682dd8e93c0e4f5dee69f32b5fc5a96443e307
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/08/2018
ms.locfileid: "35243355"
---
# <a name="xamarinforms-cells"></a>Xamarin.Forms Zellen

_Xamarin.Forms Zellen können Listenansichten und TableViews hinzugefügt werden._

Ein *Zelle* ist eine spezielle Element für Elemente in einer Tabelle verwendet und es wird beschrieben, wie jedes Element in einer Liste gerendert werden soll. Die [ `Cell` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Cell/) Klasse abgeleitet [ `Element` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Element/), von dem [ `VisualElement` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Element/) auch abgeleitet wird. Eine Zelle ist nicht selbst ein visuelles Element; Es wird stattdessen eine Vorlage zum Erstellen eines visuellen Elements.

`Cell` dient ausschließlich mit [ `ListView` ](views.md#listView) und [ `TableView` ](views.md#tableView) Steuerelemente. Weitere Informationen zum verwenden und Anpassen von Zellen, finden Sie in der [ `ListView` ](~/xamarin-forms/user-interface/listview/index.md) und [ `TableView` ](~/xamarin-forms/user-interface/tableview.md) Dokumentation.

## <a name="cells"></a>Zellen

Xamarin.Forms unterstützt die folgenden Zelle:

<a name="textCell" />

### <a name="textcell"></a>TextCell

|     |     |
| --- | --- |
| Ein [ `TextCell` ](https://developer.xamarin.com/api/type/Xamarin.Forms.TextCell) werden ein oder zwei Textzeichenfolgen angezeigt. Legen Sie die [ `Text` ](https://developer.xamarin.com/api/property/Xamarin.Forms.TextCell.Text/) Eigenschaft und optional die [ `Detail` ](https://developer.xamarin.com/api/property/Xamarin.Forms.TextCell.Detail/) Eigenschaft, um diese Textzeichenfolgen.<br /><br />[API-Dokumentation](https://developer.xamarin.com/api/type/Xamarin.Forms.TextCell) / [Handbuch](~/xamarin-forms/user-interface/listview/customizing-cell-appearance.md#TextCell) | [![Beispiel für TextCell](cells-images/TextCell.png "TextCell Beispiel")](cells-images/TextCell-Large.png#lightbox "TextCell-Beispiel")<br />[C#-Code für diese Seite](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/TextCellDemoPage.cs) / [XAML-Seite](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/TextCellDemoPage.xaml) |
|     |     |

### <a name="imagecell"></a>ImageCell

|     |     |
| --- | --- |
| Die [ `ImageCell` ](https://developer.xamarin.com/api/type/Xamarin.Forms.ImageCell) zeigt die gleiche Informationen wie [ `TextCell` ](#textCell) , sondern umfasst eine Bitmap, die Sie festlegen, mit der [ `Source` ](https://developer.xamarin.com/api/property/Xamarin.Forms.Image.Source/) Eigenschaft.<br /><br />[API-Dokumentation](https://developer.xamarin.com/api/type/Xamarin.Forms.ImageCell) / [Handbuch](~/xamarin-forms/user-interface/listview/customizing-cell-appearance.md#ImageCell) | [![Beispiel für ImageCell](cells-images/ImageCell.png "ImageCell Beispiel")](cells-images/ImageCell-Large.png#lightbox "ImageCell-Beispiel")<br />[C#-Code für diese Seite](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/ImageCellDemoPage.cs) / [XAML-Seite](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/ImageCellDemoPage.xaml) |
|     |     |

### <a name="switchcell"></a>SwitchCell

|     |     |
| --- | --- |
| Die [ `SwitchCell` ](https://developer.xamarin.com/api/type/Xamarin.Forms.SwitchCell) enthält Text festgelegt, mit der [ `Text`"](https://developer.xamarin.com/api/property/Xamarin.Forms.SwitchCellText/) Eigenschaft und und ein/aus-Schalter, die ursprünglich mit der boolesche Wert festlegen [ `On` ](https://developer.xamarin.com/api/property/Xamarin.Forms.SwitchCell.On/) Eigenschaft. Behandeln der [ `OnChanged` ](https://developer.xamarin.com/api/event/Xamarin.Forms.SwitchCell.OnChanged/) Ereignis, wenn benachrichtigt werden die `On` -Eigenschaft ändert.<br /><br />[API-Dokumentation](https://developer.xamarin.com/api/type/Xamarin.Forms.SwitchCell) / [Handbuch](~/xamarin-forms/user-interface/tableview.md#switchcell) | [![Beispiel für SwitchCell](cells-images/SwitchCell.png "SwitchCell Beispiel")](cells-images/SwitchCell-Large.png#lightbox "SwitchCell-Beispiel")<br />[C#-Code für diese Seite](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/SwitchCellDemoPage.cs) / [XAML-Seite](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/SwitchCellDemoPage.xaml) |
|     |     |

### <a name="entrycell"></a>EntryCell

|     |     |
| --- | --- |
| Die [ `EntryCell` ](https://developer.xamarin.com/api/type/Xamarin.Forms.EntryCell) definiert eine [ `Label` ](https://developer.xamarin.com/api/property/Xamarin.Forms.EntryCell.Label/) Eigenschaft identifiziert die Zelle, und eine einzelne Textzeile bearbeitet werden in der [ `Text` ](https://developer.xamarin.com/api/property/Xamarin.Forms.EntryCell.Text/) Eigenschaft. Behandeln der [ `Completed` ](https://developer.xamarin.com/api/event/Xamarin.Forms.EntryCell.Completed/) Ereignis benachrichtigt, wenn der Benutzer die Texteingabe abgeschlossen hat.<br /><br />[API-Dokumentation](https://developer.xamarin.com/api/type/Xamarin.Forms.EntryCell) / [Handbuch](~/xamarin-forms/user-interface/tableview.md#entrycell) | [![Beispiel für EntryCell](cells-images/EntryCell.png "EntryCell Beispiel")](cells-images/EntryCell-Large.png#lightbox "EntryCell-Beispiel")<br />[C#-Code für diese Seite](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/EntryCellDemoPage.cs) / [XAML-Seite](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/EntryCellDemoPage.xaml) |
|     |     |


## <a name="related-links"></a>Verwandte Links

- [Introduction to Xamarin.Forms (Einführung in Xamarin.Forms)](~/xamarin-forms/get-started/introduction-to-xamarin-forms.md)
- [Xamarin.Forms FormsGallery-Beispiel](https://developer.xamarin.com/samples/xamarin-forms/FormsGallery/)
- [Xamarin.Forms Samples (Beispiele für Xamarin.Forms)](https://developer.xamarin.com/samples/xamarin-forms/all/)
- [Xamarin.Forms-API-Dokumentation](https://developer.xamarin.com/api/root/Xamarin.Forms/)
