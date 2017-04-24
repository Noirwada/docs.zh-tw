---
title: "序列化 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a15ae411-8dc2-4ca3-84d2-01c9d5f1972a
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 序列化
本主題描述 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 序列化 \(Serialization\) 功能。  後續段落會提供有關如何在設計階段的程式碼產生期間加入序列化以及 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 類別 \(Class\) 的執行階段序列化行為。  
  
 您可以透過下列其中一種方法，在設計階段加入序列化程式碼：  
  
-   在[!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)]中，將 \[**序列化模式**\] 屬性變更為 \[**單向**\]。  
  
-   在 SQLMetal 命令列上，加入 **\/serialization** 選項。  如需詳細資訊，請參閱[SqlMetal.exe \(程式碼產生工具\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md)。  
  
## 概觀  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 所產生的程式碼預設會提供延後載入功能。  在視需要透明載入資料的中介層中，延後載入非常方便。  但是，由於不論是否需要延後載入，序列化程式都會觸發延後載入，所以序列化會有問題。  事實上，序列化物件後，在所有傳出延後載入的參考之下的遞移封閉 \(Transitive Closure\) 也已序列化。  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 序列化功能會處理這個問題，主要透過下列兩個機制：  
  
-   用於關閉延後載入的 <xref:System.Data.Linq.DataContext> 模式 \(<xref:System.Data.Linq.DataContext.ObjectTrackingEnabled%2A>\)。  如需詳細資訊，請參閱<xref:System.Data.Linq.DataContext>。  
  
-   程式碼產生參數，用在產生的實體上產生 <xref:System.Runtime.Serialization.DataContractAttribute?displayProperty=fullName> 和 <xref:System.Runtime.Serialization.DataMemberAttribute?displayProperty=fullName> 屬性 \(Attribute\)。  這個方面 \(包含序列化之下延後載入類別的行為\) 為本主題的主旨。  
  
### 定義  
  
-   *DataContract 序列化程式* \(DataContract Serializer\)：由 .NET Framework 3.0 或較新版本的 Windows Communication Framework \(WCF\) 元件使用的預設序列化程式。  
  
-   *單向序列化* \(Unidirectional Serialization\)：只含有單向關聯屬性 \(Poperty\) \(可避免循環\) 之類別的序列化版本。  依照慣例，主索引鍵\-外部索引鍵關聯性之父端上的屬性 \(Poperty\) 會標記為即將序列化。  雙向關聯中的另一端則不會序列化。  
  
     單向序列化是 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 唯一支援的序列化類型。  
  
## 程式碼範例  
 下列程式碼會使用 Northwind 範例資料庫中的傳統 `Customer` 和 `Order` 類別，並且顯示如何使用序列化屬性 \(Attribute\) 裝飾這些類別。  
  
 [!code-csharp[DLinqSerialization#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#1)]
 [!code-vb[DLinqSerialization#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#1)]  
  
 [!code-csharp[DLinqSerialization#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#2)]
 [!code-vb[DLinqSerialization#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#2)]  
  
 [!code-csharp[DLinqSerialization#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#3)]
 [!code-vb[DLinqSerialization#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#3)]  
  
 至於下列範例中的 `Order` 類別，只有對應至 `Customer` 類別的反向關聯屬性 \(Property\) 會簡短顯示。  該類別沒有 `DataMember` 屬性 \(Attribute\) 可避免循環。  
  
 [!code-csharp[DLinqSerialization#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#4)]
 [!code-vb[DLinqSerialization#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#4)]  
  
 [!code-csharp[DLinqSerialization#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#5)]
 [!code-vb[DLinqSerialization#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#5)]  
  
### 如何將實體序列化  
 您可以在上一節顯示的程式碼中將實體序列化，如下所示：  
  
 [!code-csharp[DLinqSerialization#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/Program.cs#6)]
 [!code-vb[DLinqSerialization#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/Module1.vb#6)]  
  
### 自我遞迴關聯性  
 自我遞迴關聯性會依循相同的模式。  對應至外部索引鍵的關聯屬性 \(Property\) 沒有 `DataMember` 屬性 \(Attribute\)，然而父屬性 \(Property\) 卻有該屬性 \(Attribute\)。  
  
 請考慮下列具有兩個自我遞迴關聯性的類別：Employee.Manager\/Reports 和 Employee.Mentor\/Mentees。  
  
 [!code-csharp[DLinqSerialization#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#7)]
 [!code-vb[DLinqSerialization#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#7)]  
  
## 請參閱  
 [背景資訊](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)   
 [SqlMetal.exe \(程式碼產生工具\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md)   
 [HOW TO：如何將實體設為可序列化](../../../../../../docs/framework/data/adonet/sql/linq/how-to-make-entities-serializable.md)