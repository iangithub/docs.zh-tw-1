---
title: 技術領域概觀
ms.date: 03/30/2017
helpviewer_keywords:
- window regions [WPF]
- Win32 code [WPF], WPF interoperation
- Win32 code [WPF], airspace
- airspace [WPF]
- interoperability [WPF], airspace
- Win32 code [WPF], window regions
ms.assetid: b7cc350f-b9e2-48b1-be14-60f3d853222e
ms.openlocfilehash: 6fd924f5ccb07d92c0952526a185ffc007ed23a1
ms.sourcegitcommit: 83ecdf731dc1920bca31f017b1556c917aafd7a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67860036"
---
# <a name="technology-regions-overview"></a>技術領域概觀
如果應用程式中使用了多種展示技術 (例如 WPF、Win32 或 DirectX)，它們就必須在通用的最上層視窗中共用轉譯區域。 本主題所描述的問題可能會影響您 WPF 交互操作應用程式的展示與輸入。  
  
## <a name="regions"></a>區域  
 您可以在最上層視窗中，將下列作業概念化：每個由交互操作應用程式的技術之一所組成的 HWND 都擁有自己的區域 (亦稱為「空間」)。 視窗內的每個像素只能屬於一個 HWND，其會構成該 HWND 的區域 (嚴格說來，如果有多個 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] HWND，就會有一個以上的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 區域，但基於本討論的目的，您可以假設只有一個)。 區域意謂在應用程式存留期間，嘗試以高於該像素的方式來轉譯的所有層級或其他視窗都必須屬於相同轉譯層技術的一部分。 嘗試呈現[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]像素為單位，透過[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]會導致非預期的結果，並不允許盡可能透過交互操作的 Api。  
  
### <a name="region-examples"></a>區域範例  
 下圖顯示混用 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]、[!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] 和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的應用程式。 每一種技術都會使用一組自己個別的非重疊像素，因此不會產生區域問題。  
  
 ![混用之 Win32、 DirectX 和 WPF 應用程式的範例。](./media/technology-regions-overview/win32-directx-windows-presentation-foundation-application.png)  
  
 假設此應用程式會使用滑鼠指標位置來建立動畫，此動畫會嘗試透過這三個區域的任一個來轉譯。 無論哪一個技術負責動畫本身，該技術都可能違反其他兩個區域。 下圖顯示嘗試透過 Win32 區域來轉譯 WPF 圓形。  
  
 ![嘗試透過 Win32 區域轉譯 WPF 圓形。](./media/technology-regions-overview/render-windows-presentation-foundation-circle-over-win32-region.png)  
  
 另一項違反是，如果您嘗試在不同技術之間使用透明度/Alpha 透明混色。  在下圖中，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 方塊違反了 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 和 [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] 區域。 因為 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 方塊中的像素呈現半透明效果，所以它們必須由 [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] 和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 共同擁有，但這是不可能。  因此，這是另一項違反且無法建置。  
  
 ![此圖表顯示 WPF 方塊違反的 Win32 和 DirectX 的區域。](./media/technology-regions-overview/windows-foundation-presentation-box-violate-win32-directx-region.png)  
  
 前三個範例使用了矩形區域，但可能會有不同的圖形。  例如，區域可以有一個洞。 下圖顯示 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 區域且其中有一個矩形的洞，這是結合 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] 區域的大小。  
  
 ![顯示與矩形的洞的 Win32 區域的圖表。](./media/technology-regions-overview/win32-region-rectangular-hole.png)  
  
 區域不一定是矩形，也可以是 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] HRGN (區域) 所描述的任何圖形。  
  
 ![顯示非矩形區域的圖表。](./media/technology-regions-overview/nonrectangular-win32-region.png)  
  
## <a name="transparency-and-top-level-windows"></a>透明度和最上層視窗  
 事實上，只有 Windows 中的視窗管理員才能處理 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] HWND。 因此，每隔[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Window>是一個 HWND。 <xref:System.Windows.Window> System.windows.window>hwnd 必須遵守的一般規則針對任何 HWND。 在該 HWND 中，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]程式碼可以執行任何整體[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]Api 支援。 但與桌面上的其他 HWND 互動時，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 必須遵守 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 處理和轉譯規則。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 支援非矩形視窗使用[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]Api — 非矩形視窗，和每一像素 alpha 的分層的視窗的視窗使用 Hrgn。  
  
 不支援常數的 Alpha 和色鍵。  [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 分層視窗功能會因平台而異。  
  
 分層視窗可讓整個視窗呈現半透明狀態，方法是指定要套用至視窗中每個像素的 Alpha 值  ([!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 實際上支援每個像素的 Alpha，但這很難在實際程式中使用，因為在此模式中，您可能需要自行繪製任何子系 HWND，包括對話方塊和下拉式清單)。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 支援 Hrgn;不過，沒有受管理的 Api，這項功能。 您可以使用平台叫用並<xref:System.Windows.Interop.HwndSource>來呼叫相關[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]Api。 如需詳細資訊，請參閱[從 Managed 程式碼呼叫原生函式](/cpp/dotnet/calling-native-functions-from-managed-code)。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 分層視窗在不同作業系統上有不同的功能。 這是因為 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 會使用 [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] 來轉譯，而分層視窗主要是設計來轉譯 [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)] ，而不是轉譯 [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)]。  
  
- [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 在 [!INCLUDE[TLA#tla_longhorn](../../../../includes/tlasharptla-longhorn-md.md)] 和更新版本上支援硬體加速的分層視窗。 [!INCLUDE[TLA2#tla_winxp](../../../../includes/tla2sharptla-winxp-md.md)] 上硬體加速的分層視窗需要來自 [!INCLUDE[TLA#tla_dx](../../../../includes/tlasharptla-dx-md.md)] 的支援，因此功能將取決於該機器上的 [!INCLUDE[TLA#tla_dx](../../../../includes/tlasharptla-dx-md.md)] 版本。  
  
- [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 不支援透明色鍵，因為 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 無法保證可確實呈現您要求的色彩，特別當轉譯是透過硬體加速時。  
  
- 如果您的應用程式是在 [!INCLUDE[TLA2#tla_winxp](../../../../includes/tla2sharptla-winxp-md.md)] 上執行，位於 [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] 介面上方的分層視窗就會在 [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] 應用程式轉譯時閃爍  (實際轉譯順序是 [!INCLUDE[TLA#tla_gdi](../../../../includes/tlasharptla-gdi-md.md)] 會隱藏分層視窗，接著 [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] 會繪製，然後 [!INCLUDE[TLA#tla_gdi](../../../../includes/tlasharptla-gdi-md.md)] 會將分層視窗推送回來)。  非 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的分層視窗也有這項限制。  
  
## <a name="see-also"></a>另請參閱

- [WPF 和 Win32 交互操作](wpf-and-win32-interoperation.md)
- [逐步解說：裝載 WPF 時鐘在 Win32 中](walkthrough-hosting-a-wpf-clock-in-win32.md)
- [在 WPF 中裝載 Win32 內容](hosting-win32-content-in-wpf.md)
