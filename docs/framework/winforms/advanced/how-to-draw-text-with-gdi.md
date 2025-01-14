---
title: 作法：使用 GDI 繪製文字
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- GDI [Windows Forms], drawing text [Windows Forms]
- text [Windows Forms], drawing with TextRenderer
- drawing [Windows Forms], text
- Windows Forms, drawing text with GDI
ms.assetid: 2a19fe5d-2ace-451c-94db-01cb1118ef7b
ms.openlocfilehash: 3d5b79e82185c044314ff8807b86835ef6a87c45
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2019
ms.locfileid: "67505903"
---
# <a name="how-to-draw-text-with-gdi"></a>HOW TO：使用 GDI 繪製文字
具有<xref:System.Windows.Forms.TextRenderer.DrawText%2A>方法中的<xref:System.Windows.Forms.TextRenderer>類別，您可以存取在表單或控制項上繪製文字的 GDI 功能。 GDI 文字轉譯通常提供較佳的效能和更精確比 GDI + 中測量的文字。  
  
> [!NOTE]
>  <xref:System.Windows.Forms.TextRenderer.DrawText%2A>方法的<xref:System.Windows.Forms.TextRenderer>類別不支援列印。 列印時，一律使用<xref:System.Drawing.Graphics.DrawString%2A>方法的<xref:System.Drawing.Graphics>類別。  
  
## <a name="example"></a>範例  
 下列程式碼範例示範如何在多行內的矩形，使用上繪製文字<xref:System.Windows.Forms.TextRenderer.DrawText%2A>方法。  
  
 [!code-csharp[System.Windows.Forms.TextRendererExamples#7](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.TextRendererExamples/CS/Form1.cs#7)]
 [!code-vb[System.Windows.Forms.TextRendererExamples#7](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.TextRendererExamples/VB/Form1.vb#7)]  
  
 要呈現的文字<xref:System.Windows.Forms.TextRenderer>類別，您需要<xref:System.Drawing.IDeviceContext>，例如<xref:System.Drawing.Graphics>和<xref:System.Drawing.Font>，來繪製文字，並在其中它應該繪製的色彩的位置。 您可以選擇性地指定格式化所使用的文字<xref:System.Windows.Forms.TextFormatFlags>列舉型別。  
  
 如需取得詳細資訊<xref:System.Drawing.Graphics>，請參閱[How to:建立繪圖的圖形物件](how-to-create-graphics-objects-for-drawing.md)。 如需有關建構<xref:System.Drawing.Font>，請參閱[How to:建構字型系列和字型](how-to-construct-font-families-and-fonts.md)。  
  
## <a name="compiling-the-code"></a>編譯程式碼  
 上述程式碼範例專為搭配 Windows Form 使用，而且需要<xref:System.Windows.Forms.PaintEventArgs> `e`，這是參數的<xref:System.Windows.Forms.PaintEventHandler>。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Windows.Forms.TextRenderer>
- <xref:System.Drawing.Font>
- <xref:System.Drawing.Color>
- [使用字型和文字](using-fonts-and-text.md)
