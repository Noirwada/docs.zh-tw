---
title: "在工作流程中使用合約 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 939c64e9-e7cc-4abc-b41e-27cfce1d7e50
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 在工作流程中使用合約
實作服務時，您會定義許多合約，這些合約會描述服務及服務傳送與接收的資料。資料會以資料合約和訊息合約表示，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 和工作流程服務都會使用資料合約和訊息合約定義做為服務描述的一部分。服務本身會公開中繼資料 \(以 WSDL 的形式\) 來描述服務的作業。在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中，服務合約和作業合約會定義所支援的服務及作業。不過，在工作流程服務中，這些合約是商務程序本身的一部分，會由稱為「合約推斷」的處理序在中繼資料中公開。  
  
## 合約推斷  
 使用 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 裝載工作流程服務時，會檢查該工作流程定義，並根據在工作流程中找到的傳訊活動集產生合約。特別是，下列活動和屬性會用來產生合約：  
  
 <xref:System.ServiceModel.Activities.Receive> 活動  
  
-   <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A>  
  
-   <xref:System.ServiceModel.Activities.Receive.OperationContractName%2A>  
  
-   <xref:System.ServiceModel.Activities.Receive.Action%2A>  
  
-   <xref:System.ServiceModel.Activities.Receive.ValueType%2A>  
  
 <xref:System.ServiceModel.Activities.SendReply> 活動  
  
-   <xref:System.ServiceModel.Activities.SendReply.Action%2A>  
  
-   <xref:System.ServiceModel.Activities.SendReply.ValueType%2A>  
  
 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 活動  
  
 合約推斷的最終結果是與 WCF 服務和作業合約使用相同資料結構的服務描述。接著，這項資訊會用來公開工作流程服務的 WSDL。  
  
## 請參閱  
 [工作流程服務](../../../../docs/framework/wcf/feature-details/workflow-services.md)   
 [訊息活動](../../../../docs/framework/wcf/feature-details/messaging-activities.md)   
 [HOW TO：說明如何使用訊息活動建立工作流程服務。](../../../../docs/framework/wcf/feature-details/how-to-create-a-workflow-service-with-messaging-activities.md)   
 [HOW TO：建立會取用現有服務合約的工作流程服務](../../../../docs/framework/windows-workflow-foundation//how-to-create-a-workflow-service-that-consumes-an-existing-service-contract.md)