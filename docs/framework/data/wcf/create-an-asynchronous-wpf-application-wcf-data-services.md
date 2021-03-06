---
title: "HOW TO：建立非同步 Windows Presentation Framework 應用程式 (WCF Data Service) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF Data Services, 非同步作業"
ms.assetid: 834614df-1427-4839-b0be-90f68e5afffd
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# HOW TO：建立非同步 Windows Presentation Framework 應用程式 (WCF Data Service)
使用 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 時，您可以將從資料服務取得的資料繫結至 Windows Presentation Framework \(WPF\) 應用程式的 UI 項目。  如需詳細資訊，請參閱[將資料繫結至控制項](../../../../docs/framework/data/wcf/binding-data-to-controls-wcf-data-services.md)。您也可以透過非同步方式，針對資料服務執行作業，這樣能讓應用程式在等待資料服務要求回應時繼續回應。  若要透過非同步方式存取資料服務，則需要 Silverlight 應用程式。  如需詳細資訊，請參閱[非同步作業](../../../../docs/framework/data/wcf/asynchronous-operations-wcf-data-services.md)。  
  
 本主題說明如何透過非同步方式存取資料服務，並且將結果繫結至 WPF 應用程式的項目。  本主題的範例使用 Northwind 範例資料服務和自動產生的用戶端資料服務類別。  此服務和用戶端資料類別會在您完成 [WCF Data Services 快速入門](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)時建立。  
  
## 範例  
 下列 XAML 定義 WPF 應用程式的視窗。  
  
 [!code-xml[Astoria Northwind Client#WpfDataBindingAsyncXaml](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerordersasync.xaml#wpfdatabindingasyncxaml)]  
  
## 範例  
 下列 XAML 檔案的程式碼後置頁面會使用資料服務執行非同步查詢，然後將結果繫結至 WPF 視窗中的項目。  
  
 [!code-csharp[Astoria Northwind Client#WpfDataBindingAsync](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerordersasync.xaml.cs#wpfdatabindingasync)]
 [!code-vb[Astoria Northwind Client#WpfDataBindingAsync](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerordersasync.xaml.vb#wpfdatabindingasync)]  
  
## 請參閱  
 [WCF Data Services 用戶端程式庫](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)