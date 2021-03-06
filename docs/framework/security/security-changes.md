---
title: ".NET Framework 中的安全性變更 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "Allow Partially Trusted Callers 屬性"
  - ".NET Framework 4, 安全性變更"
  - ".NET Framework 安全性"
  - "安全性透明的程式碼"
  - "安全性關鍵程式碼"
  - "程式碼存取安全性, 變更"
ms.assetid: 5e87881c-9c13-4b52-8ad1-e34bb46e8aaa
caps.latest.revision: 52
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 52
---
# .NET Framework 中的安全性變更
在 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 中對於安全性最重要的變更為強式命名。 如需這些變更的說明，請參閱 [進階強式命名](../../../docs/framework/app-domains/enhanced-strong-naming.md)。  
  
 .NET Framework 提供 Managed 應用程式的兩層式安全性模型。[!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]應用程式會在限制存取資源的 Windows 安全性容器內執行。 在該容器內，Managed 應用程式會在完全受信任的情況下執行。 從程式碼存取安全性 \(CAS\) 的觀點來看，開發人員不管做什麼也都無法提高權限。 如需 Windows 授與之權限的詳細資訊，請參閱 Windows 開發人員中心的[應用程式功能宣告 \(Windows 市集應用程式\)](http://go.microsoft.com/fwlink/?LinkId=230436)。 如需建立 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]應用程式的詳細資訊，請參閱[使用 C\# 或 Visual Basic 建立您的第一個 Windows 市集應用程式](http://go.microsoft.com/fwlink/?LinkId=230461)。