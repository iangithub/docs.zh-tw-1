---
title: HOW TO：建立繫結控制項並格式化顯示的資料
ms.date: 03/30/2017
helpviewer_keywords:
- data [Windows Forms], formatting
- bound controls [Windows Forms], creating
- bound controls [Windows Forms], formatting data
ms.assetid: d5a56228-899d-41d9-8af8-87b3f4ec2f94
ms.openlocfilehash: d81995840aa4df4610d5b6e880b9cdbbc717f2e5
ms.sourcegitcommit: d8ebe0ee198f5d38387a80ba50f395386779334f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66690397"
---
# <a name="how-to-create-a-bound-control-and-format-the-displayed-data"></a>HOW TO：建立繫結控制項並格式化顯示的資料

Windows Form 資料繫結，您可以格式化顯示資料繫結控制項中使用的資料**格式化與進階繫結** 對話方塊。

> [!NOTE]
> 根據您目前使用的設定或版本，您所看到的對話方塊與功能表命令可能會與 [說明] 中描述的不同。 若要變更設定，請從 [ **工具** ] 功能表中選取 [ **匯入和匯出設定** ]。 如需詳細資訊，請參閱[將 Visual Studio IDE 個人化](/visualstudio/ide/personalizing-the-visual-studio-ide)。

### <a name="to-bind-a-control-and-format-the-displayed-data"></a>繫結控制項並格式化顯示的資料

1. 連接至資料來源。

     如需詳細資訊，請參閱 <<c0> [ 連接到資料來源](../data/adonet/connecting-to-a-data-source.md)。

2. 在表單中選取控制項，然後開啟屬性視窗。

3. 依序展開 **(DataBindings)** 屬性，然後在 **（進階）** 方塊中，按一下省略符號按鈕 (![Visual Studio 的 [屬性] 視窗中的省略符號按鈕 （...）。](./media/how-to-create-a-bound-control-and-format-the-displayed-data/visual-studio-ellipsis-button.png))若要顯示**格式化與進階繫結** 對話方塊中，具有該控制項屬性的完整清單。

4. 選取您想要繫結，然後按一下的屬性**繫結**箭號。

     會顯示可用資料來源清單。

5. 展開您想要繫結的資料來源，直到您找到您要的單一資料項目。

     例如，如果您要在資料集資料表中繫結資料行值，展開資料集的名稱，然後展開資料表名稱來顯示資料行名稱。

6. 按一下要繫結項目的名稱。

7. 在 **格式化型別**方塊中，按一下您想要套用至資料控制項中顯示的格式。

     在所有情況下，如果資料來源包含 <xref:System.DBNull>，則您可以指定顯示在控制項中的值。 否則，選項會稍微不同，視您所選擇的格式類型而定。 下列表格顯示格式類型和選項。

    |格式類型|格式化選項|
    |-----------------|-----------------------|
    |沒有格式化|沒有選項。|
    |數值|使用指定的小數位數**小數位數**上下按鈕控制項。|
    |貨幣|使用指定的小數位數**小數位數**上下按鈕控制項。|
    |日期時間|選取的日期和時間應該如何顯示選取的項目中的其中一項**型別**選取方塊。|
    |科學記號|使用指定的小數位數**小數位數**上下按鈕控制項。|
    |自訂|指定使用自訂格式字串。<br /><br /> 如需詳細資訊，請參閱[格式類型](../../standard/base-types/formatting-types.md)。 **注意：** 自訂格式字串不保證能成功地在資料來源和繫結的控制項之間反覆存取。 改為處理 <xref:System.Windows.Forms.Binding.Parse> 或 <xref:System.Windows.Forms.Binding.Format> 繫結的事件，以及在事件處理程式碼中套用自訂格式。|

8. 按一下 [ **[確定]** 以關閉**格式化與進階繫結**] 對話方塊中，並返回 [屬性] 視窗。

## <a name="see-also"></a>另請參閱

- [如何：建立 Windows Form 上的簡單繫結控制項](how-to-create-a-simple-bound-control-on-a-windows-form.md)
- [Windows Forms 中的使用者輸入驗證](user-input-validation-in-windows-forms.md)
- [Windows Forms 資料繫結](windows-forms-data-binding.md)
