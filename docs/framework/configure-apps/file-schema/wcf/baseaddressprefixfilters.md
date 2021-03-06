---
title: "&lt;baseAddressPrefixFilters&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8cab2a9a-c51f-4283-bb60-2ad0c274fd46
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# &lt;baseAddressPrefixFilters&gt;
表示組態項目的集合，這個集合會指定通過篩選條件，而且這些篩選條件提供了一項機制，可在將 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 應用程式裝載於 Internet Information Services \(IIS\) 時挑選適當的 IIS 繫結。  
  
> [!WARNING]
>  \<baseAddressPrefixFilters\> 無法辨識 “localhost”，請改用完整電腦名稱。  
  
## 語法  
  
```  
  
<serviceHostingEnvironment>  
     <baseAddressPrefixFilters>  
        <add prefix="string"/>  
     </baseAddressPrefixFilters>  
</serviceHostingEnvironment>  
```  
  
## 屬性和項目  
 下列章節說明屬性、子項目和父項目。  
  
### 屬性  
 無。  
  
### 子項目  
  
|項目|描述|  
|--------|--------|  
|[\<add\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-baseaddressprefixfilter.md)|新增組態項目，這個項目會指定由服務主機使用之基底位址的前置詞篩選條件。|  
  
### 父項目  
  
|項目|描述|  
|--------|--------|  
|[\<serviceHostingEnvironment\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md)|定義服務裝載環境為特定傳輸產生的類型。|  
  
## 備註  
 前置詞篩選條件為共用裝載提供者提供一種方式，使其可指定服務所要使用的 URI。  它可讓共用主機在同一個網站上裝載多個應用程式，而且同一個配置中可以有不同的基底位址。  
  
 IIS 網站是包含虛擬目錄的虛擬應用程式的容器 \(Container\)。  網站中的應用程式則可以透過一個或多個 IIS 繫結來存取。  IIS 繫結提供繫結通訊協定和繫結這兩項資訊。  繫結通訊協定 \(例如 HTTP\) 會定義產生通訊的配置，而繫結資訊 \(例如 IPAddress、Port、Hostheader\) 包含用來存取該網站的資料。  
  
 IIS 支援為每個網站指定多個 IIS 繫結，讓每個配置都有多個基底位址。  由於裝載在網站下的 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 服務僅允許每個配置繫結至一個基底位址，因此，您可以使用前置詞篩選功能挑選所裝載服務所需的基底位址。  IIS 提供的傳入基底位址會依據選擇性的前置詞清單篩選條件進行篩選。  
  
 例如，您的網站可能包含下列基底位址。  
  
```  
http://testl.fabrikam.com/Service.svc  
http://test2.fabrikam.com/Service.svc  
```  
  
 您可以使用下列組態檔在 appdomain 層級指定前置詞篩選條件。  
  
```  
<system.serviceModel>  
  <serviceHostingEnvironment>  
     <baseAddressPrefixFilters>  
        <add prefix=”net.tcp://test1.fabrikam.com:8000”/>  
        <add prefix=”http://test2.fabrikam.com:9000”/>  
    </baseAddressPrefixFilters>  
  </serviceHostingEnvironment>  
</system.serviceModel>  
```  
  
 在此範例中，`net.tcp://test1.fabrikam.com:8000` 和 `http://test2.fabrikam.com:9000` 分別是其配置的唯一基底位址，而且已被允許通過篩選。  
  
 根據預設，如果沒有指定前置詞，則所有位址都會通過。  如果指定前置詞，則只會允許要通過之配置的相符基底位址。  
  
> [!NOTE]
>  篩選條件不支援任何萬用字元。  此外，IIS 提供的 baseAddress 中，可能會有位址繫結至不在 `baseAddressPrefixFilters` 清單中的配置，  而且這些位址尚未經過篩選。  
  
## 請參閱  
 <xref:System.ServiceModel.Configuration.BaseAddressPrefixFilterElementCollection>   
 <xref:System.ServiceModel.Configuration.ServiceHostingEnvironmentSection>   
 <xref:System.ServiceModel.ServiceHostingEnvironment>   
 [裝載](../../../../../docs/framework/wcf/feature-details/hosting.md)