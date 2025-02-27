---
title: 編碼方式和 Windows Form 全球化
ms.date: 03/30/2017
helpviewer_keywords:
- ListView control [Windows Forms], lack of Unicode support
- DateTimePicker control [Windows Forms], lack of Unicode support
- TrackBar control [Windows Forms], lack of Unicode support
- ImageList component [Windows Forms], lack of Unicode support
- Unicode [Windows Forms]
- ToolBar control [Windows Forms], lack of Unicode support
- international applications [Windows Forms], character display
- StatusBar control [Windows Forms], lack of Unicode support
- MonthCalendar control [Windows Forms], lack of Unicode support
- international characters
- TabControl control [Windows Forms], lack of Unicode support
- Windows Forms, encoding
- TreeView control [Windows Forms], lack of Unicode support
- ProgressBar control [Windows Forms], Unicode-enabled forms
- localization [Windows Forms], character sets
- globalization [Windows Forms], character sets
ms.assetid: 22e8965d-a712-42b3-8167-3ee346bd70f9
ms.openlocfilehash: f8e56642b6325454d2d55cd3a3d3a83d201c2eb5
ms.sourcegitcommit: 5e05f983e63d5bbd8c0b246d02c6e4f23d2fc1db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2019
ms.locfileid: "67151985"
---
# <a name="encoding-and-windows-forms-globalization"></a>編碼方式和 Windows Form 全球化
Windows Forms 應用程式完全支援 Unicode，這表示不論是何種平台、程式或語言，每個字元都會以唯一號碼來表示。 如需有關 Unicode 的詳細資訊，請參閱 < [Unicode 協會網站](https://www.unicode.org)。  
  
## <a name="benefits-of-unicode"></a>Unicode 的優點  
 支援 Unicode 之表單的優點包括能夠使用僅限 Unicode 的字集，例如印度文。 此外，您可以在單一表單上使用多種語言。 在 Unicode 中，所有字元的長度都是兩個位元組，因此不需要特別表示雙位元組字元。 您也可以撰寫一組可在所有平台上運作的字碼。 這是從舊版的 Visual Basic 中，您必須在其中寫入不同的平台，例如 Windows NT 不同的程式碼的變更和[!INCLUDE[win98](../../../../includes/win98-md.md)]。  
  
 不過，在 [!INCLUDE[win98](../../../../includes/win98-md.md)] 和 Windows Millennium Edition 中，有些控制項並不支援 Unicode。 這些控制項，全部都是繼承自通用控制項，會將與 Windows 字碼頁的資料處理為 ANSI。 這些控制項包括：<xref:System.Windows.Forms.TabControl>、<xref:System.Windows.Forms.ListView>、<xref:System.Windows.Forms.TreeView>、<xref:System.Windows.Forms.DateTimePicker>、<xref:System.Windows.Forms.MonthCalendar>、<xref:System.Windows.Forms.TrackBar>、<xref:System.Windows.Forms.ProgressBar>、<xref:System.Windows.Forms.ImageList>、<xref:System.Windows.Forms.ToolBar> 和 <xref:System.Windows.Forms.StatusBar>。 因此在前述平台上，您無法在這些控制項中顯示 Unicode 資料。 例如，您無法在英文版的 [!INCLUDE[win98](../../../../includes/win98-md.md)] 作業系統上顯示日文字元。  
  
 如需 <xref:System.Windows.Forms.ToolBar> 和 <xref:System.Windows.Forms.StatusBar> 控制項的 Unicode 感知替代方式，請使用 <xref:System.Windows.Forms.ToolStrip> 和 <xref:System.Windows.Forms.StatusStrip> 控制項來取代這些舊版控制項。 若要維持應用程式中不同視覺項目的外觀和風格類似，請使用 <xref:System.Windows.Forms.MenuStrip> 控制項來呈現功能表，而不是使用 <xref:System.Windows.Forms.MainMenu>。 如同 <xref:System.Windows.Forms.ToolStrip> 和 <xref:System.Windows.Forms.StatusStrip>，<xref:System.Windows.Forms.MenuStrip> 也可以處理及顯示 Unicode 字元。  
  
## <a name="see-also"></a>另請參閱

- [全球化 Windows Forms 應用程式](globalizing-windows-forms.md)
