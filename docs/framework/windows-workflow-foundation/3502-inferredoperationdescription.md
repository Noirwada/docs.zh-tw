---
title: "3502 - InferredOperationDescription | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6aebb614-3c72-4537-ba11-3cc7200ef1f1
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 3502 - InferredOperationDescription
## 屬性  
  
|||  
|-|-|  
|ID|3502|  
|關鍵字|WFServices|  
|層級|資訊|  
|通道|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## 描述  
 表示已從 WorkflowService 推斷出 OperationDescription。  
  
## 訊息  
 已從 WorkflowService 推斷出合約 '%2' 中 Name\='%1' 的 OperationDescription。  IsOneWay\=%3。  
  
## 詳細資料  
  
|資料項目名稱|資料項目型別|描述|  
|------------|------------|--------|  
|OperationName|xs:string|作業的名稱。|  
|ContractName|xs:string|合約的名稱。|  
|IsOneWay|xs:string|True 或 False 表示合約是否為單向。|  
|AppDomain|xs:string|由 AppDomain.CurrentDomain.FriendlyName 傳回的字串。|