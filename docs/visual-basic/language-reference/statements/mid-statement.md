---
title: Mid 陳述式 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.MidB
- vb.Mid
helpviewer_keywords:
- substrings [Visual Basic], Mid statement
- strings [Visual Basic], substrings
- Mid statement [Visual Basic]
- strings [Visual Basic], replacing
ms.assetid: 2b82d7a8-9646-4cb0-bec5-80abc98297bf
ms.openlocfilehash: ff3b908e2805f4d51463a82d90f2305efc9f1608
ms.sourcegitcommit: c4dfe37032c64a1fba2cc3d5947550d79f95e3b5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/13/2019
ms.locfileid: "67041577"
---
# <a name="mid-statement"></a>Mid 陳述式
取代字元的指定的數目`String`變數與另一個字串中的字元。  
  
## <a name="syntax"></a>語法  
  
```  
Mid( _  
   ByRef Target As String, _  
   ByVal Start As Integer, _  
   Optional ByVal Length As Integer _  
) = StringExpression  
```  
  
## <a name="parts"></a>組件  
 `Target`  
 必要項。 名稱`String`修改的變數。  
  
 `Start`  
 必要項。 `Integer` 運算式。 字元在位置`Target`取代文字的開始位置。 `Start` 使用以一為基的索引。  
  
 `Length`  
 選擇性。 `Integer` 運算式。 若要取代的字元數。 如果省略，所有`String`用。  
  
 `StringExpression`  
 必要項。 `String` 取代一部分的運算式`Target`。  
  
## <a name="exceptions"></a>例外狀況  
  
|例外狀況類型|條件|  
|--------------------|---------------|  
|<xref:System.ArgumentException>|`Start` < = 0 或`Length`< 0。|  
  
## <a name="remarks"></a>備註  
 被取代的字元數目一律為小於或等於中的字元數`Target`。  
  
 Visual Basic 也有<xref:Microsoft.VisualBasic.Strings.Mid%2A>函式和`Mid`陳述式。 這些項目都會運作指定的字串中的字元數，但`Mid`函式會傳回的字元時`Mid`陳述式會取代字元。 如需詳細資訊，請參閱 <xref:Microsoft.VisualBasic.Strings.Mid%2A>。  
  
> [!NOTE]
>  `MidB`舊版的 Visual Basic 的陳述式可以取代子字串的位元組，而不是字元。 它是主要用於將雙位元組字元集 (DBCS) 應用程式中的字串轉換。 所有的 Visual Basic 字串為 Unicode，和`MidB`不受支援。  
  
## <a name="example"></a>範例  
 這個範例會使用`Mid`陳述式來取代指定的字串變數中的字元數，從另一個字串的字元。  
  
 [!code-vb[VbVbalrStrings#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class1.vb#5)]  
  
## <a name="requirements"></a>需求  
 **命名空間：** [Microsoft.VisualBasic](../../../visual-basic/language-reference/runtime-library-members.md)  
  
 **模組：** `Strings`  
  
 **組件：** Visual Basic Runtime Library (位於 Microsoft.VisualBasic.dll)  
  
## <a name="see-also"></a>另請參閱

- <xref:Microsoft.VisualBasic.Strings.Mid%2A>
- [字串](../../../visual-basic/programming-guide/language-features/strings/index.md)
- [Visual Basic 中的字串簡介](../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)
