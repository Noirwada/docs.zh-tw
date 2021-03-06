---
title: "HOW TO：手動產生用戶端資料服務類別 (WCF Data Services) | Microsoft Docs"
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
  - "WCF Data Services, 用戶端程式庫"
  - "WCF Data Services, 設定"
ms.assetid: b98cb1d6-956a-4e50-add6-67e4f2587346
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# HOW TO：手動產生用戶端資料服務類別 (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 與 Visual Studio 的整合，可讓您在使用 \[**加入服務參考**\] 對話方塊於 Visual Studio 專案中加入資料服務參考時，自動產生用戶端資料服務類別。  如需詳細資訊，請參閱[HOW TO：加入資料服務參考](../../../../docs/framework/data/wcf/how-to-add-a-data-service-reference-wcf-data-services.md)。  您也可以使用程式碼產生工具 `DataSvcUtil.exe`，手動產生相同的用戶端資料服務類別。隨附在 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 中的這個工具會從資料服務定義產生 .NET Framework 類別。  同時，這項工具也可根據概念模型 \(.csdl\) 檔案，以及在 Visual Studio 專案中代表 Entity Framework 模型的 .edmx 檔案產生資料服務類別。  
  
 本主題的範例會根據 Northwind 範例資料服務建立用戶端資料服務類別。  此服務會在您完成 [WCF Data Services 快速入門](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)時建立。  本主題中的某些範例需要 Northwind 模型的概念模型檔案。  如需詳細資訊，請參閱[HOW TO：使用 EdmGen.exe 產生模型和對應檔](../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)。  本主題中的某些範例需要 Northwind 模型的 .edmx 檔。  如需詳細資訊，請參閱[.edmx File Overview](http://msdn.microsoft.com/zh-tw/f4c8e7ce-1db6-417e-9759-15f8b55155d4)。  
  
### 產生支援資料繫結的 C\# 類別  
  
-   在命令提示字元中，執行下列命令但不含分行符號：  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /dataservicecollection /version:2.0 /language:CSharp /out:Northwind.cs /uri:http://localhost:12345/Northwind.svc  
    ```  
  
    > [!NOTE]
    >  您必須將提供給 `/uri:` 參數的值改為您的 Northwind 範例資料服務執行個體的 URI。  
  
### 產生支援資料繫結的 Visual Basic 類別  
  
-   在命令提示字元中，執行下列命令但不含分行符號：  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /dataservicecollection /version:2.0 /language:VB /out:Northwind.vb /uri:http://localhost:12345/Northwind.svc  
    ```  
  
    > [!NOTE]
    >  您必須將提供給 `/uri:` 參數的值改為您的 Northwind 資料服務範本之執行個體的 URI。  
  
### 根據服務 URI 產生 C\# 類別  
  
-   在命令提示字元中，執行下列命令但不含分行符號：  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /language:CSharp /out:northwind.cs /uri:http://localhost:12345/Northwind.svc  
    ```  
  
    > [!NOTE]
    >  您必須將提供給 `/uri:` 參數的值改為您的 Northwind 範例資料服務執行個體的 URI。  
  
### 根據服務 URI 產生 Visual Basic 類別  
  
-   在命令提示字元中，執行下列命令但不含分行符號：  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /out:Northwind.vb /uri:http://localhost:12345/Northwind.svc  
    ```  
  
    > [!NOTE]
    >  您必須將提供給 `/uri:` 參數的值改為您的 Northwind 資料服務範本之執行個體的 URI。  
  
### 根據概念模型檔 \(CSDL\) 產生 C\# 類別  
  
-   在命令提示字元中，執行下列命令但不含分行符號：  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:CSharp /in:Northwind.csdl /out:Northwind.cs  
    ```  
  
### 根據概念模型檔 \(CSDL\) 產生 Visual Basic 類別  
  
-   在命令提示字元中，執行下列命令但不含分行符號：  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /in:Northwind.csdl /out:Northwind.vb  
    ```  
  
### 根據 .edmx 檔產生 C\# 類別  
  
-   在命令提示字元中，執行下列命令但不含分行符號：  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:CSharp /in:Northwind.edmx /out:c:\northwind.cs   
    ```  
  
### 根據服務 .edmx 檔產生 Visual Basic 類別  
  
-   在命令提示字元中，執行下列命令但不含分行符號：  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /in:Northwind.edmx /out:c:\northwind.vb   
    ```  
  
## 請參閱  
 [產生資料服務用戶端程式庫](../../../../docs/framework/data/wcf/generating-the-data-service-client-library-wcf-data-services.md)   
 [HOW TO：加入資料服務參考](../../../../docs/framework/data/wcf/how-to-add-a-data-service-reference-wcf-data-services.md)   
 [WCF Data Services 用戶端公用程式 \(DataSvcUtil.exe\)](../../../../docs/framework/data/wcf/wcf-data-service-client-utility-datasvcutil-exe.md)