---
title: "如何：處理資料繫結時所發生的錯誤和例外狀況 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "BindingSource 元件 [Windows Form], 處理錯誤和例外狀況"
  - "資料繫結, 錯誤處理"
  - "資料繫結, 範例"
  - "錯誤處理, 資料繫結"
  - "錯誤處理, 範例"
  - "範例 [Windows Form], 錯誤處理"
ms.assetid: eddc5bad-9513-47df-ab28-f02d8dff7892
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：處理資料繫結時所發生的錯誤和例外狀況
當您將它們繫結至控制項時，有時候基礎商務物件會發生例外狀況和錯誤。  您可以攔截這些錯誤和例外狀況然後復原，或藉由為特定的 <xref:System.Windows.Forms.Binding> 、 <xref:System.Windows.Forms.BindingSource> 或 <xref:System.Windows.Forms.CurrencyManager> 元件處理 <xref:System.Windows.Forms.Binding.BindingComplete> 事件，將錯誤資訊傳遞給使用者。  
  
## 範例  
 這個程式碼範例會示範如何處理錯誤以及資料繫結作業期間發生的例外狀況。  它示範如何藉由處理 <xref:System.Windows.Forms.Binding> 物件中的 <xref:System.Windows.Forms.Binding.BindingComplete?displayProperty=fullName> 事件來攔截錯誤。  若要藉由處理這個事件來攔截錯誤和例外狀況，您必須為繫結啟用格式化。  您可以於繫結被建構或加到繫結集合中時，或藉由設定 <xref:System.Windows.Forms.Binding.FormattingEnabled%2A> 屬性為 `true` 來啟用格式化。  
  
 [!code-cpp[System.Windows.Forms.DataConnectorBindingComplete#3](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorBindingComplete/CPP/form1.cpp#3)]
 [!code-csharp[System.Windows.Forms.DataConnectorBindingComplete#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorBindingComplete/CS/form1.cs#3)]
 [!code-vb[System.Windows.Forms.DataConnectorBindingComplete#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorBindingComplete/VB/form1.vb#3)]  
  
 當程式碼正在執行，同時在部分名稱輸入空字串或在部分編號輸入小於 100 的值時，會出現訊息方塊。  這是為了這些文字方塊繫結處理 <xref:System.Windows.Forms.Binding.BindingComplete?displayProperty=fullName> 事件所得到的結果。  
  
## 編譯程式碼  
 這個範例需要：  
  
-   System、System.Drawing 和 System.Windows.Forms 組件的參考。  
  
 如需從 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 或 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 的命令列建置這個範例的相關資訊，請參閱[從命令列建置](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) 或[使用 csc.exe 建置命令列](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。  您也可以將程式碼貼在新的專案中，以在 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 中建置這個範例。  另請參閱[如何：使用 Visual Studio 編譯及執行完整的 Windows Form 程式碼範例](http://msdn.microsoft.com/library/Bb129228%20\(v=vs.110\))。  
  
## 請參閱  
 <xref:System.Windows.Forms.Binding.BindingComplete?displayProperty=fullName>   
 <xref:System.Windows.Forms.BindingSource.BindingComplete?displayProperty=fullName>   
 [BindingSource 元件](../../../../docs/framework/winforms/controls/bindingsource-component.md)