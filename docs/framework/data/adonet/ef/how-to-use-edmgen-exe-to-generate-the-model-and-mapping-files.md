---
title: "HOW TO：使用 EdmGen.exe 產生模型和對應檔 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "ESQL"
  - "jsharp"
ms.assetid: 40db462d-2fd2-4cc1-ad86-d280403e63fa
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# HOW TO：使用 EdmGen.exe 產生模型和對應檔
本主題示範如何使用 EDM 產生器 \(EdmGen.exe\) 工具依據 School 資料庫產生下列檔案：  
  
-   概念模型 \(.csdl 檔\)。  
  
-   儲存體模型 \(.ssdl 檔\)。  
  
-   概念模型和儲存模型之間的對應 \(.msl 檔\)。  
  
-   Visual Basic 或 C\# 中的物件層程式碼。  
  
-   檢視檔案。  
  
 EdmGen.exe 工具使用 \/mode:FullGeneration 產生以上所列檔案。  如需 EdmGen.exe 命令的詳細資訊，請參閱 [EDM 產生器 \(EdmGen.exe\)](../../../../../docs/framework/data/adonet/ef/edm-generator-edmgen-exe.md)。  
  
 如果使用 EdmGen.exe 產生模型和對應檔，仍然必須將 [!INCLUDE[vsprvs](../../../../../includes/vsprvs-md.md)] 專案設定成使用 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]。  如需詳細資訊，請參閱[How to: Manually Configure an Entity Framework Project](http://msdn.microsoft.com/zh-tw/73f6ae1d-b3b2-4577-aebd-ad5a75954e9e)。  
  
> [!NOTE]
>  EdmGen.exe 所產生的概念模型會包括資料庫中的所有物件。  如果您想要產生僅包含特定物件的概念模型，請使用 Entity Data Model 精靈。  如需詳細資訊，請參閱[How to: Use the Entity Data Model Wizard](http://msdn.microsoft.com/zh-tw/dadb058a-c5d9-4c5c-8b01-28044112231d)。  
  
### 若要使用 EdmGen.exe 來產生 Visual Basic 專案的 School 模型  
  
1.  建立 School 資料庫。  如需詳細資訊，請參閱[Creating the School Sample Database](http://msdn.microsoft.com/zh-tw/c1bec483-a0ea-4660-aa0b-7b0a8b68fed0)。  
  
2.  在命令提示字元中，執行下列命令但不含分行符號：  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v4.0.30319\edmgen.exe" /mode:fullgeneration   
    /c:"Data Source=%datasourceserver%; Initial Catalog=School; Integrated Security=SSPI"   
    /project:School /entitycontainer:SchoolEntities /namespace:SchoolModel /language:VB  
  
    ```  
  
### 若要使用 EdmGen.exe 來產生 C\# 專案的 School 模型  
  
1.  建立 School 資料庫。  如需詳細資訊，請參閱[Creating the School Sample Database](http://msdn.microsoft.com/zh-tw/c1bec483-a0ea-4660-aa0b-7b0a8b68fed0)。  
  
2.  在命令提示字元中，執行下列命令但不含分行符號：  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v4.0.30319\edmgen.exe" /mode:fullgeneration   
    /c:"Data Source=%datasourceserver%; Initial Catalog=School; Integrated Security=SSPI"   
    /project:School /entitycontainer:SchoolEntities /namespace:SchoolModel /language:CSharp  
    ```  
  
## 請參閱  
 [模型化及對應檔案](../../../../../docs/framework/data/adonet/ef/modeling-and-mapping.md)   
 [How to: Manually Configure an Entity Framework Project](http://msdn.microsoft.com/zh-tw/73f6ae1d-b3b2-4577-aebd-ad5a75954e9e)   
 [How to: Pre\-Generate Views to Improve Query Performance](http://msdn.microsoft.com/zh-tw/b18a9d16-e10b-4043-ba91-b632f85a2579)   
 [ADO.NET Entity Data Model  Tools](http://msdn.microsoft.com/zh-tw/91076853-0881-421b-837a-f582f36be527)   
 [HOW TO：使用 EdmGen.exe 驗證模型和對應檔](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-validate-model-and-mapping-files.md)