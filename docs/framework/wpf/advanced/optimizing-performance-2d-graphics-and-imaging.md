---
title: 最佳化效能：2D 圖形和影像處理
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [WPF], performance
- drawing [WPF], optimizing performance
- imaging [WPF], optimizing performance
- shapes [WPF], optimizing performance
- 2-D graphics [WPF]
- images [WPF], optimizing performance
ms.assetid: e335601e-28c8-4d64-ba27-778fffd55f72
ms.openlocfilehash: 25803bd772832cd22e855f530d10a3f3639c180c
ms.sourcegitcommit: 127343afce8422bfa944c8b0c4ecc8f79f653255
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/25/2019
ms.locfileid: "67348439"
---
# <a name="optimizing-performance-2d-graphics-and-imaging"></a>最佳化效能：2D 圖形和影像處理
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供各種 2D 圖形和影像處理功能，可以針對您的應用程式需求最佳化。 本主題提供下列領域的效能最佳化相關資訊。  

<a name="Drawing_and_Shapes"></a>   
## <a name="drawing-and-shapes"></a>繪圖和圖形  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了<xref:System.Windows.Media.Drawing>和<xref:System.Windows.Shapes.Shape>物件來代表圖形繪圖內容。 不過，<xref:System.Windows.Media.Drawing>物件是簡單的建構比<xref:System.Windows.Shapes.Shape>物件，並提供較佳的效能特性。  
  
 A<xref:System.Windows.Shapes.Shape>可讓您將圖形描繪至螢幕。 因為它們衍生自<xref:System.Windows.FrameworkElement>類別，<xref:System.Windows.Shapes.Shape>物件都可以使用在面板和大部分的控制項。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了數層的圖形和轉譯服務存取權。 在最上層的<xref:System.Windows.Shapes.Shape>物件很容易使用，並提供許多實用的功能，例如版面配置和事件處理。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 則提供數個立即可用的 Shape 物件。 所有的 shape 物件繼承自<xref:System.Windows.Shapes.Shape>類別。 可用的 shape 物件包含<xref:System.Windows.Shapes.Ellipse>， <xref:System.Windows.Shapes.Line>， <xref:System.Windows.Shapes.Path>， <xref:System.Windows.Shapes.Polygon>， <xref:System.Windows.Shapes.Polyline>，和<xref:System.Windows.Shapes.Rectangle>。  
  
 <xref:System.Windows.Media.Drawing> 物件，相反地，非衍生自<xref:System.Windows.FrameworkElement>類別，並提供輕量型實作呈現圖形、 影像和文字。  
  
 有四種類型的<xref:System.Windows.Media.Drawing>物件：  
  
- <xref:System.Windows.Media.GeometryDrawing> 繪製圖形。  
  
- <xref:System.Windows.Media.ImageDrawing> 繪製影像。  
  
- <xref:System.Windows.Media.GlyphRunDrawing> 繪製文字。  
  
- <xref:System.Windows.Media.DrawingGroup> 繪製其他繪圖。 您可以使用繪圖群組，來將其他繪圖結合為單一複合繪圖。  
  
 <xref:System.Windows.Media.GeometryDrawing>物件用來呈現幾何內容。 <xref:System.Windows.Media.Geometry>類別和衍生，這類的具象類別<xref:System.Windows.Media.CombinedGeometry>， <xref:System.Windows.Media.EllipseGeometry>，和<xref:System.Windows.Media.PathGeometry>、 提供方法來轉譯 2D 圖形，以及提供點擊測試和裁剪的支援。 舉例來說，Geometry 物件可用來定義控制項的區域，或定義要套用至影像的裁剪區域。 Geometry 物件可以是矩形和圓形之類的簡單區域，或從兩個或多個 Geometry 物件建立的複合區域。 更複雜的幾何區域可能由合併<xref:System.Windows.Media.PathSegment>-衍生的物件，例如<xref:System.Windows.Media.ArcSegment>， <xref:System.Windows.Media.BezierSegment>，和<xref:System.Windows.Media.QuadraticBezierSegment>。  
  
 在介面中，<xref:System.Windows.Media.Geometry>類別和<xref:System.Windows.Shapes.Shape>類別是相當類似。 呈現 2D 圖形中同時使用，兩者都有類似的具象類別，例如衍生自這些<xref:System.Windows.Media.EllipseGeometry>和<xref:System.Windows.Shapes.Ellipse>。 不過，這兩組類別之間有非常重要的差異。 第一，<xref:System.Windows.Media.Geometry>類別缺少的功能的一些<xref:System.Windows.Shapes.Shape>類別，例如能夠繪製本身。 若要繪製 Geometry 物件，必須使用 DrawingContext、Drawing 或 Path (注意，Path 也是一種 Shape) 等其他類別來執行繪製作業。 填滿、筆觸以及筆觸粗細等呈現屬性位於可繪製 Geometry 物件的類別中，而 Shape 物件則包含這些屬性。 針對這項差異的其中一個理解方式是：Geometry 物件可定義區域 (例如圓形)；而 Shape 物件則可定義區域、該區域的填滿方式和外框方式，並參與版面配置系統。  
  
 由於<xref:System.Windows.Shapes.Shape>物件衍生自<xref:System.Windows.FrameworkElement>使用它們的類別可以在您的應用程式中新增更多的記憶體耗用量。 如果您真的不需要<xref:System.Windows.FrameworkElement>功能的圖形化的內容，請考慮使用輕量<xref:System.Windows.Media.Drawing>物件。  
  
 如需詳細資訊<xref:System.Windows.Media.Drawing>物件，請參閱[繪圖物件概觀](../graphics-multimedia/drawing-objects-overview.md)。  
  
<a name="StreamGeometry_Objects"></a>   
## <a name="streamgeometry-objects"></a>StreamGeometry 物件  
 <xref:System.Windows.Media.StreamGeometry>物件是輕量型替代方案<xref:System.Windows.Media.PathGeometry>來建立幾何圖形。 使用<xref:System.Windows.Media.StreamGeometry>當您需要描繪複雜幾何。 <xref:System.Windows.Media.StreamGeometry> 最適合處理許多<xref:System.Windows.Media.PathGeometry>物件，並執行得更好，相較於使用許多個別<xref:System.Windows.Media.PathGeometry>物件。  
  
 下列範例會使用屬性語法以建立三角形<xref:System.Windows.Media.StreamGeometry>在[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]。  
  
 [!code-xaml[GeometriesMiscSnippets_snip#StreamGeometryTriangleExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/GeometriesMiscSnippets_snip/XAML/StreamGeometryExample.xaml#streamgeometrytriangleexamplewholepage)]  
  
 如需詳細資訊<xref:System.Windows.Media.StreamGeometry>物件，請參閱[圖形使用 StreamGeometry 建立](../graphics-multimedia/how-to-create-a-shape-using-a-streamgeometry.md)。  
  
<a name="DrawingVisual_Objects"></a>   
## <a name="drawingvisual-objects"></a>DrawingVisual 物件  
 <xref:System.Windows.Media.DrawingVisual>物件是輕量型繪圖類別，用來呈現圖形、 影像或文字。 此類別之所以被視為輕量型，是因為它不提供版面配置或事件處理，這使它有更好的效能。 基於此原因，它適合用於背景或美工圖案繪圖。 如需詳細資訊，請參閱[使用 DrawingVisual 物件](../graphics-multimedia/using-drawingvisual-objects.md)。  
  
<a name="Images"></a>   
## <a name="images"></a>影像  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 影像處理功能比舊版 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 影像處理功能有更大幅的改良。 以往，影像處理功能 (例如顯示點陣圖或使用通用控制項上的影像) 主要是由 Microsoft Windows 圖形裝置介面 (GDI) 或 Microsoft Windows GDI+ 應用程式開發介面 (API) 進行處理。 這些 API 提供基本影像處理功能，但無法支援轉碼器擴充性和高畫質影像等功能。 WPF 影像處理 API 的設計目的是克服 GDI 和 GDI+ 的缺點，並提供一組新的 API 以在應用程式內顯示及使用影像。  
  
 使用影像時，請考慮下列建議事項以取得較佳的效能：  
  
- 如果您的應用程式需要顯示縮圖影像，請考慮建立影像的縮小版本。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 預設會載入您的影像，並將其解碼到完整大小。 如果您只需要影像的縮圖版本，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 仍會多此一舉地將影像解碼到完整大小，然後再縮至縮圖大小。 為了避免不必要的額外負荷，您可以要求 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 解碼影像至縮圖大小，或要求 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 載入縮圖大小的影像。  
  
- 一律將影像解碼至所需大小，而非預設大小。 如上所述，您可以要求 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 將影像解碼至所需大小，而不是預設的完整大小。 這麼做不只能減少應用程式的工作集，還會降低執行速度。  
  
- 因此，可能的話，請將影像合併單一影像，例如多張影像組成的底片。  
  
- 如需詳細資訊，請參閱 [影像處理概觀](../graphics-multimedia/imaging-overview.md)。  
  
### <a name="bitmapscalingmode"></a>BitmapScalingMode  
 建立任何點陣圖的比例動畫時，預設的高品質影像重新取樣演算法有時會耗用過多系統資源，導致畫面播放速率降低，從而造成動畫中斷。 藉由設定<xref:System.Windows.Media.RenderOptions.BitmapScalingMode%2A>的屬性<xref:System.Windows.Media.RenderOptions>物件到<xref:System.Windows.Media.BitmapScalingMode.LowQuality>縮放點陣圖時，您可以建立更順暢的動畫。 <xref:System.Windows.Media.BitmapScalingMode.LowQuality> 模式會告知[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]處理映像時，從品質最佳化的演算法切換為速度最佳化演算法的轉譯引擎。  
  
 下列範例示範如何設定<xref:System.Windows.Media.BitmapScalingMode>映像物件。  
  
 [!code-csharp[RenderOptions#RenderOptionsSnippet2](~/samples/snippets/csharp/VS_Snippets_Wpf/RenderOptions/CSharp/Window1.xaml.cs#renderoptionssnippet2)]
 [!code-vb[RenderOptions#RenderOptionsSnippet2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RenderOptions/visualbasic/window1.xaml.vb#renderoptionssnippet2)]  
  
### <a name="cachinghint"></a>CachingHint  
 根據預設，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]不會快取的呈現的內容<xref:System.Windows.Media.TileBrush>物件，例如<xref:System.Windows.Media.DrawingBrush>和<xref:System.Windows.Media.VisualBrush>。 在靜態案例其中的內容和使用<xref:System.Windows.Media.TileBrush>在場景會變更，這很合理，因為它可以節省視訊記憶體。 不會因為許多感測時<xref:System.Windows.Media.TileBrush>具有靜態內容使用中的非靜態方法 — 例如，當靜態<xref:System.Windows.Media.DrawingBrush>或<xref:System.Windows.Media.VisualBrush>旋轉 3D 物件的介面對應。 預設行為[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]是重新呈現內容的整個<xref:System.Windows.Media.DrawingBrush>或<xref:System.Windows.Media.VisualBrush>每個框架，即使內容不變亦同。  
  
 藉由設定<xref:System.Windows.Media.RenderOptions.CachingHint%2A>的屬性<xref:System.Windows.Media.RenderOptions>物件到<xref:System.Windows.Media.CachingHint.Cache>您可以使用並排筆刷物件的快取的版本，以提升效能。  
  
 <xref:System.Windows.Media.RenderOptions.CacheInvalidationThresholdMinimum%2A>並<xref:System.Windows.Media.RenderOptions.CacheInvalidationThresholdMaximum%2A>屬性的值是相對大小值，判斷何時<xref:System.Windows.Media.TileBrush>應該重新產生物件，因為變更小數位數。 例如，藉由設定<xref:System.Windows.Media.RenderOptions.CacheInvalidationThresholdMaximum%2A>屬性為 2.0 時，快取<xref:System.Windows.Media.TileBrush>只需要重新產生它的大小超過兩次目前的快取的大小。  
  
 下列範例示範如何使用的快取提示選項<xref:System.Windows.Media.DrawingBrush>。  
  
 [!code-csharp[RenderOptions#RenderOptionsSnippet3](~/samples/snippets/csharp/VS_Snippets_Wpf/RenderOptions/CSharp/Window1.xaml.cs#renderoptionssnippet3)]
 [!code-vb[RenderOptions#RenderOptionsSnippet3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RenderOptions/visualbasic/window1.xaml.vb#renderoptionssnippet3)]  
  
## <a name="see-also"></a>另請參閱

- [最佳化 WPF 應用程式效能](optimizing-wpf-application-performance.md)
- [應用程式效能規劃](planning-for-application-performance.md)
- [運用硬體](optimizing-performance-taking-advantage-of-hardware.md)
- [版面配置與設計](optimizing-performance-layout-and-design.md)
- [物件行為](optimizing-performance-object-behavior.md)
- [應用程式資源](optimizing-performance-application-resources.md)
- [Text](optimizing-performance-text.md)
- [資料繫結](optimizing-performance-data-binding.md)
- [其他效能建議](optimizing-performance-other-recommendations.md)
- [動畫祕訣和訣竅](../graphics-multimedia/animation-tips-and-tricks.md)
