---
title: "out (泛型修飾詞) (C# 參考) | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- covariance, out keyword [C#]
- out keyword [C#]
ms.assetid: f8c20dec-a8bc-426a-9882-4076b1db1e00
caps.latest.revision: 15
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: a5b488eab5966a556b3e3c91ae8c748d11e61367
ms.lasthandoff: 03/13/2017

---
# <a name="out-generic-modifier-c-reference"></a>out (泛型修飾詞) (C# 參考)
若為泛型型別參數，`out` 關鍵字會指定型別參數是 Covariant。 您可以在泛型介面及委派中使用 `out` 關鍵字。  
  
 共變數可讓您使用比泛型參數指定的衍生程度更高的衍生型別。 這可隱含轉換實作 Variant 介面的類別和隱含轉換委派型別。 參考型別支援共變數和反變數，但實值型別不支援它們。  
  
 具有 Covariant 型別參數的介面可讓其方法傳回的衍生型別，衍生程度高過型別參數指定的衍生型別。 例如，因為在 .NET Framework 4 的 <xref:System.Collections.Generic.IEnumerable%601> 中， T 型別是 covariant，所以您可以不使用任何特殊的轉換方法，將 `IEnumerabe(Of String)` 型別的物件指派給 `IEnumerable(Of Object)` 型別的物件。  
  
 Covariant 委派可以指派給同型別的另一個委派，但具有衍生程度較大的泛型型別參數。  
  
 如需詳細資訊，請參閱 [Covariance and Contravariance](http://msdn.microsoft.com/library/a58cc086-276f-4f91-a366-85b7f95f38b8) (共變數和反變數 (C# 和 Visual Basic))。  
  
## <a name="example"></a>範例  
 下例會示範如何宣告、擴充及實作 Covariant 泛型介面。 它也會示範如何針對實作 Covariant 介面的類別使用隱含轉換。  
  
 [!code-cs[csVarianceKeywords#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/out-generic-modifier_1.cs)]  
  
 在泛型介面中，型別參數如果滿足下列條件即可宣告為 Covariant︰  
  
-   型別參數僅用為介面方法的傳回型別，不用為方法引數的型別。  
  
    > [!NOTE]
    >  這個規則只有一個例外。 如果您在 Covariant 介面中以 Contravariant 泛型委派作為方法參數，則可將 Covariant 型別用為此委派的泛型型別參數。 如需 Covariant 和 Contravariant 泛型委派的詳細資訊，請參閱 [Variance in Delegates](http://msdn.microsoft.com/library/e3b98197-6c5b-4e55-9c6e-9739b60645ca) (委派中的變異數) 和 [Using Variance for Func and Action Generic Delegates](http://msdn.microsoft.com/library/e69c4f39-09aa-4c6d-a752-08cc767d8290) (針對 Func 與 Action 委派使用變異數)。  
  
-   型別參數不是用為介面方法的泛型條件約束。  
  
## <a name="example"></a>範例  
 下例會示範如何宣告、具現化及叫用 Covariant 泛型委派。 它也會顯示如何以隱含方式轉換委派型別。  
  
 [!code-cs[csVarianceKeywords#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/out-generic-modifier_2.cs)]  
  
 在泛型委派中，如果型別只用為方法傳回型別，不用於方法引數，則可以宣告為 Covariant。  
  
## <a name="c-language-specification"></a>C# 語言規格  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [泛型介面中的變異數](http://msdn.microsoft.com/library/e14322da-1db3-42f2-9a67-397daddd6b6a)   
 [in](../../../csharp/language-reference/keywords/in-generic-modifier.md)   
 [修飾詞](../../../csharp/language-reference/keywords/modifiers.md)
