---
title: 偵錯 LINQ to DataSet 查詢
ms.date: 03/30/2017
ms.assetid: f4c54015-8ce2-4c5c-8d18-7038144cc66d
ms.openlocfilehash: 38eda9f352c4a8d8590e5e57b48c694eadd0397b
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2019
ms.locfileid: "67503978"
---
# <a name="debugging-linq-to-dataset-queries"></a>偵錯 LINQ to DataSet 查詢

Visual Studio 支援偵錯 LINQ 的資料集的程式碼。 不過，有一些資料集的程式碼和受管理的資料集的程式碼的非 LINQ 偵錯 LINQ 的差異。 大部分偵錯功能時，用於 LINQ 的資料集的陳述式，包括逐步執行、 設定中斷點，以及檢視偵錯工具視窗所示的結果。 不過，延後的查詢執行中有某些資料集的程式碼偵錯 LINQ 時，您應該考慮的副作用，而且有一些限制，若要使用 [編輯後繼續]。 本主題討論 LINQ to DataSet 相較於受管理的資料集的程式碼的非 LINQ 獨有偵錯的觀點。  
  
## <a name="viewing-results"></a>檢視結果  
 您可以使用 DataTips、 監看式 視窗中和 快速監看式 對話方塊中檢視 LINQ to DataSet 陳述式的結果。 藉由使用來源視窗，您可以在來源視窗中暫停查詢的指標，而且 DataTip 將會出現。 您可以將 LINQ 複製到資料集的變數，並將它貼到 [監看式] 視窗或 [快速監看式] 對話方塊。 在 LINQ to DataSet 時建立或宣告，, 但只有在執行查詢時，不會評估查詢。 這就叫做*延後執行*。 因此，查詢變數在接受評估前沒有值。 如需詳細資訊，請參閱 < [LINQ to DataSet 中的查詢](../../../../docs/framework/data/adonet/queries-in-linq-to-dataset.md)。  
  
 偵錯工具必須評估查詢，才能顯示查詢結果。 當您在偵錯工具，檢視 LINQ to DataSet 查詢結果，而且有一些您應該考慮的效果，就會發生這個隱含評估。 每個查詢評估會耗費些許時間。 展開結果節點也會耗用時間。 對於某些查詢而言，重複的評估可能會造成明顯的效能影響。 評估查詢也可能造成變更資料值與程式狀態的副作用。 並不是所有的查詢都有副作用。 若要判斷是否可以沒有副作用安全地評估查詢，您必須了解實作查詢的程式碼。 如需詳細資訊，請參閱 <<c0> [ 副作用和運算式](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/a7a250bs(v=vs.120))。  
  
## <a name="edit-and-continue"></a>編輯後繼續  
 編輯後繼續不支援 linq to DataSet 查詢的變更。 如果您新增、 移除或變更 LINQ 偵錯工作階段的資料集陳述式，會出現對話方塊，告訴您的變更不支援編輯後繼續。 此時，您可以復原變更，或者是停止偵錯工作階段並使用編輯過的程式碼重新啟動新的工作階段。  
  
 此外，編輯並繼續 不支援變更類型或使用 LINQ to DataSet 陳述式中的變數的值。 同樣地，您可以復原變更，或者是停止並重新啟動偵錯工作階段。  
  
 在視覺效果C#在 Visual Studio 中，您無法使用 編輯後繼續在包含 LINQ to DataSet 查詢方法中的任何程式碼。  
  
 在 Visual Basic 在 Visual Studio 中，您可以使用 編輯後繼續於非 LINQ to DataSet 的程式碼中，即使在包含 LINQ to DataSet 查詢的方法。 您可以新增或移除 LINQ to DataSet 陳述式之前的程式碼，即使這些變更會影響 LINQ to DataSet 查詢的行號。 LINQ to DataSet 推出之前，Visual Basic 偵錯體驗，非 LINQ to DataSet 的程式碼維持不變。 您無法變更、 新增或移除 LINQ to DataSet 查詢，不過，除非您停止偵錯以套用所做的變更。  
  
## <a name="see-also"></a>另請參閱

- [偵錯 Managed 程式碼](/visualstudio/debugger/debugging-managed-code)
- [程式設計手冊](../../../../docs/framework/data/adonet/programming-guide-linq-to-dataset.md)
