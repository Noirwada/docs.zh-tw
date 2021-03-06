---
title: "安全性交涉與逾時 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 02a428f1-84e5-4d28-a11f-53ce31d63196
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# 安全性交涉與逾時
當用戶端和伺服器進行驗證時，[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 支援一種在驗證過程中交涉服務認證的模式。在這類案例中，用戶端和伺服器之間可能會進行 multi\-leg 交換，以便將服務認證傳播至用戶端。<xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.NegotiationTimeout%2A> 屬性會控制完成 multi\-leg 交換所需要的時間。不過，只有在交換所花費的實際時間超過單一要求\-回應的時間時，這個逾時情況才適用。如果在單一來回行程中完成交涉，逾時就不適用。  
  
## 請參閱  
 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>   
 [HOW TO：設定最大時鐘誤差](../../../../docs/framework/wcf/feature-details/how-to-set-a-max-clock-skew.md)