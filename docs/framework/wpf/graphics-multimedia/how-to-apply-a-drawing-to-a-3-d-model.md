---
title: 作法：對立體模型套用繪圖
ms.date: 03/30/2017
helpviewer_keywords:
- drawings [WPF], applying to 3-D models
- 3-D models [WPF], applying drawings to
ms.assetid: 68357577-b7fc-446e-8be9-a8cc7df3a350
ms.openlocfilehash: 8ac24fdf8d7e407e10764c17fcc12121aa5f51d7
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2019
ms.locfileid: "67662804"
---
# <a name="how-to-apply-a-drawing-to-a-3-d-model"></a>作法：對立體模型套用繪圖
此範例示範如何使用<xref:System.Windows.Media.DrawingBrush>做為<xref:System.Windows.Media.Media3D.Material>套用至 3d 模型。  
  
 下列程式碼定義<xref:System.Windows.Media.DrawingGroup>的內容<xref:System.Windows.Media.DrawingBrush>。  <xref:System.Windows.Media.DrawingBrush>設定為<xref:System.Windows.Media.Media3D.DiffuseMaterial.Brush%2A>屬性<xref:System.Windows.Media.Media3D.DiffuseMaterial>套用至 3d 的平面。  
  
 **注意：** 它通常會定義複雜的物件和值，例如下面繪製為資源，可以重複使用，並簡化您的程式碼。 請參閱[XAML 資源](../advanced/xaml-resources.md)如需詳細資訊。  
  
 [!code-xaml[3DGallery_snip#ApplyDrawingToMaterialInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/ApplyDrawingToMaterialExample.xaml#applydrawingtomaterialinline1)]  
  
## <a name="example"></a>範例  
 下列程式碼顯示整個範例。  
  
 [!code-xaml[3DGallery_snip#ApplyDrawingToMaterialExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/ApplyDrawingToMaterialExample.xaml#applydrawingtomaterialexamplewholepage)]  
  
## <a name="see-also"></a>另請參閱

- [XAML 資源](../advanced/xaml-resources.md)
- [建立立體場景](how-to-create-a-3-d-scene.md)
- [繪圖物件概觀](drawing-objects-overview.md)
- [立體圖形概觀](3-d-graphics-overview.md)
