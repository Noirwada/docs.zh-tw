---
title: "/utf8output (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/utf8output"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "utf8output compiler option [C#]"
  - "/utf8output compiler option [C#]"
  - "-utf8output compiler option [C#]"
ms.assetid: 27ff7381-c281-45d7-b2eb-1ad644b1354e
caps.latest.revision: 10
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 10
---
# /utf8output (C# Compiler Options)
**\/utf8output** 選項會使用 UTF\-8 編碼方式顯示編譯器輸出。  
  
## 語法  
  
```  
/utf8output  
```  
  
## 備註  
 在某些國際化組態中，編譯器的輸出不能正確地顯示在主控台上。  在這種組態中，請使用 **\/utf8output** 並將編譯器輸出重新導向至檔案。  
  
 在 Visual Studio 中無法使用這個編譯器選項，而且無法利用程式設計的方式變更它。  
  
## 請參閱  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)