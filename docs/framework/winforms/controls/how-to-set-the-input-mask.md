---
title: HOW TO：設定輸入遮罩
ms.date: 03/30/2017
f1_keywords:
- net.ComponentModel.MaskPropertyEditor
helpviewer_keywords:
- MaskedTextBox control [Windows Forms]
ms.assetid: 779b3a12-cd74-4e58-b46e-04983bda5b2c
ms.openlocfilehash: ac747bf46c4dd1451e58615b1ec0311d75c899e8
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67760485"
---
# <a name="how-to-set-the-input-mask"></a>作法：設定輸入遮罩
遮罩的文字方塊控制項是支援的宣告式語法，以接受或拒絕使用者輸入增強的文字方塊控制項。 藉由設定 [遮罩] 屬性，您可以指定允許使用者輸入，而不需要撰寫任何自訂驗證邏輯應用程式中。 如需詳細資訊，請參閱的 < 備註 > 一節<xref:System.Windows.Forms.MaskedTextBox>類別。  
  
## <a name="setting-the-mask-property-manually"></a>手動設定遮罩屬性  
 如果您已熟悉使用遮罩屬性支援的字元，您可以手動輸入。 如需摘要的遮罩屬性支援的字元，請參閱 < 備註 > 一節<xref:System.Windows.Forms.MaskedTextBox.Mask%2A>屬性。  
  
### <a name="to-set-the-mask-property-manually"></a>若要手動設定遮罩屬性  
  
1. 在 **設計**檢視中，選取<xref:System.Windows.Forms.MaskedTextBox>。  
  
2. 在 [**屬性**] 視窗中，找出<xref:System.Windows.Forms.MaskedTextBox.Mask%2A>屬性。  
  
3. 輸入您想要的遮罩。 例如，輸入 `###`。  
  
## <a name="using-the-input-mask-dialog-box"></a>使用 [輸入的遮罩] 對話方塊  
 [輸入遮罩] 對話方塊中提供一些預先定義的輸入的遮罩。 您也可以變更預先定義的遮罩，或以手動方式輸入您自己的遮罩。  
  
### <a name="to-open-the-input-mask-dialog-box"></a>若要開啟 [輸入遮罩] 對話方塊  
  
1. 在 **設計**檢視中，選取<xref:System.Windows.Forms.MaskedTextBox>。  
  
    1. 按一下以開啟的智慧標籤**MaskedTextBox 工作**面板。  
  
    2. 按一下 **設定遮罩**。  
  
     \-或-  
  
    1. 在 **屬性**視窗中，選取<xref:System.Windows.Forms.MaskedTextBox.Mask%2A>屬性。  
  
    2. 按一下省略符號按鈕，在屬性資料行。  
  
     **輸入遮罩** 對話方塊隨即出現。  
  
### <a name="to-use-the-input-mask-dialog-box"></a>若要使用 [輸入遮罩] 對話方塊  
  
1. （選擇性）按一下其中一個預先定義的遮罩，在清單中。  
  
2. （選擇性）編輯中的預先定義的遮罩**遮罩** 方塊中。  
  
3. （選擇性）輸入新遮罩**遮罩** 方塊中。 也就是說，您不必使用其中一個預先定義的遮罩。  
  
    > [!NOTE]
    >  [預覽] 方塊會顯示在中的使用者會看到的字元<xref:System.Windows.Forms.MaskedTextBox>。 這些字元是幫助使用者輸入正確的資料。  
  
4. 選取或清除**使用 ValidatingType**核取方塊。 **使用 ValidatingType**核取方塊可讓您指定的資料類型是否用來驗證資料輸入的使用者。 如需詳細資訊，請參閱 <xref:System.Windows.Forms.MaskedTextBox.ValidatingType%2A> 屬性 (Property)。  
  
5. 按一下 [確定 **Deploying Office Solutions**]。  
  
     在 輸入遮罩**遮罩**中的屬性**屬性**視窗。  
  
## <a name="see-also"></a>另請參閱

- [逐步解說：使用 MaskedTextBox 控制項](walkthrough-working-with-the-maskedtextbox-control.md)
