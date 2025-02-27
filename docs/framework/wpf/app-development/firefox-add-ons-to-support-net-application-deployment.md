---
title: 支援 .NET 應用程式部署的 Firefox 附加元件
ms.date: 03/30/2017
helpviewer_keywords:
- Firefox add-ons for .NET application deployment
- WPF plug-in for Firefox
- .NET application deployment [WPF], deploying with Firefox add-ons
- .NET Framework Assistant for Firefox
ms.assetid: 2403403b-9b14-48e9-b70d-fa288a3c9081
ms.openlocfilehash: 39f4548bfe9e505c1369a0de8262560070fd6221
ms.sourcegitcommit: 34593b4d0be779699d38a9949d6aec11561657ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2019
ms.locfileid: "66833919"
---
# <a name="firefox-add-ons-to-support-net-application-deployment"></a>支援 .NET 應用程式部署的 Firefox 附加元件
啟用 Windows Presentation Foundation (WPF) 外掛程式 Firefox 和.NET Framework Assistant for Firefox [!INCLUDE[TLA#tla_winfxwebapp#plural](../../../../includes/tlasharptla-winfxwebappsharpplural-md.md)]、 鬆散[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，與 ClickOnce 應用程式，才能使用 Mozilla Firefox 瀏覽器。  
  
## <a name="wpf-plug-in-for-firefox"></a>外掛程式適用於 Firefox 的 WPF  
 外掛程式適用於 Firefox 的 WPF 可讓[!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)]和鬆散[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]瀏覽至並執行最上層或在 HTML IFRAME Firefox 瀏覽器中的檔案。 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]是[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]可以發行至 Web 伺服器和中啟動應用程式支援的瀏覽器。 鬆散[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]是僅限 XAML 的檔案，可以瀏覽至並顯示在支援的瀏覽器，如同 XML 檔案。  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]外掛程式的 Firefox 會隨.NET Framework 3.5。 Window 7 包含.NET Framework 3.5，但不包含[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]Firefox 的外掛程式。 您無法安裝[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]在 Windows 7 上的 Firefox 的外掛程式。  
  
 .NET Framework 4 不包含[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]Firefox 的外掛程式。 不過，如果已安裝.NET Framework 3.5 和.NET Framework 4，外掛程式適用於 Firefox 的 WPF 會隨.NET Framework 3.5。 因此.NET Framework 4 應用程式仍會執行因為 WPF 主應用程式會載入正確的 framework 版本。 如需詳細資訊，請參閱 < [WPF 主應用程式 (PresentationHost.exe)](wpf-host-presentationhost-exe.md)。  
  
## <a name="net-framework-assistant-for-firefox"></a>.NET Framework Assistant for Firefox  
 若要從 Firefox 瀏覽器執行的獨立 ClickOnce 應用程式可讓.NET Framework Assistant for Firefox。 .NET Framework Assistant for Firefox 函式只有在安裝之前和之後的 Firefox 瀏覽器時相同。 當啟動 Firefox 瀏覽器，並安裝.NET Framework 3.5 SP1 時，Firefox 會尋找並會安裝.NET Framework Assistant for Firefox。 使用者可以設定.NET Framework Assistant for Firefox 來執行下列作業：  
  
- 執行 ClickOnce 應用程式之前提示。  
  
- 報告所有已安裝的新版.NET Framework 或只是最新版本。  
  
 .NET Framework Assistant for Firefox 會隨附在.NET Framework 3.5 SP1。 移除適用於 Firefox 的.NET Framework Assistant 的詳細資訊，請參閱[如何移除適用於 Firefox 的.NET Framework Assistant](https://go.microsoft.com/fwlink/?LinkId=177944)。  
  
## <a name="see-also"></a>另請參閱

- [部署 WPF 應用程式](deploying-a-wpf-application-wpf.md)
- [WPF XAML 瀏覽器應用程式概觀](wpf-xaml-browser-applications-overview.md)
- [偵測有無安裝 Firefox 的 WPF 外掛程式](how-to-detect-whether-the-wpf-plug-in-for-firefox-is-installed.md)
