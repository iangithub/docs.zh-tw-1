---
title: .NET Framework 中的安全性變更
ms.date: 03/30/2017
helpviewer_keywords:
- Allow Partially Trusted Callers attribute
- .NET Framework 4, security changes
- .NET Framework security
- security-transparent code
- security-critical code
- code access security, changes
ms.assetid: 5e87881c-9c13-4b52-8ad1-e34bb46e8aaa
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 61f9e68bcc554dc3e4a4878e575d3f046a8ef9f5
ms.sourcegitcommit: 4735bb7741555bcb870d7b42964d3774f4897a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/30/2019
ms.locfileid: "66378596"
---
# <a name="security-changes-in-the-net-framework"></a>.NET Framework 中的安全性變更
在.NET Framework 4.5 中的安全性最重要的變更是在強式命名。 如需這些變更的說明，請參閱 [Enhanced Strong Naming](../../../docs/framework/app-domains/enhanced-strong-naming.md) 。  
  
 .NET Framework 提供 Managed 應用程式的兩層式安全性模型。 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 應用程式會在限制存取資源的 Windows 安全性容器內執行。 在該容器內，Managed 應用程式會在完全受信任的情況下執行。 從程式碼存取安全性 (CAS) 的觀點來看，開發人員不管做什麼也都無法提高權限。 如需 Windows 授與之權限的詳細資訊，請參閱 Windows 開發人員中心的 [應用程式功能宣告 (Windows 市集應用程式)](https://go.microsoft.com/fwlink/?LinkId=230436) 。 如需建立 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 應用程式的詳細資訊，請參閱 [使用 C# 或 Visual Basic 建立您的第一個 Windows 市集應用程式](https://go.microsoft.com/fwlink/?LinkId=230461)。
