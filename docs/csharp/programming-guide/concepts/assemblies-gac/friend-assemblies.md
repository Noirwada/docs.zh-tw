---
title: "Friend 組件 (C#) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: b65ea7de-0801-477a-a39c-e914c2cc107c
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ca01b9e91de08f3bdf53cd0572a3e1d1af0cf0af
ms.lasthandoff: 03/13/2017

---
# <a name="friend-assemblies-c"></a>Friend 組件 (C#)
「friend 組件」**是可以存取另一個組件的[內部](../../../../csharp/language-reference/keywords/internal.md)類型和成員的組件。 如果將組件指定為 friend 組件，就不再需要將類型和成員標記為 public，以供其他組件存取。 這在下列情況下特別方便：  
  
-   在單元測試期間，當測試程式碼在另一個組件中執行，但需要存取所測試組件中標記為 `internal` 的成員時。  
  
-   當您要開發類別庫且類別庫的新增項目包含在不同的組件，但需要存取現有組件中標記為 `internal` 的成員時。  
  
## <a name="remarks"></a>備註  
 您可以使用 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 屬性，為特定組件指定一或多個 friend 組件。 下列範例在組件 A 中使用 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 屬性，並將組件 `AssemblyB` 指定為 friend 組件。 這可讓組件 `AssemblyB` 存取組件 A 中所有標記為 `internal` 的類型和成員。  
  
> [!NOTE]
>  如果您編譯的組件 (組件 `AssemblyB`) 會存取另一個組件 (組件 *A*) 的內部類型或內部成員，您必須使用 **/out** 編譯器選項明確指定輸出檔案的名稱 (.exe 或 .dll)。 因為編譯器尚未針對在繫結至外部參考時所建立的組件產生名稱，所以這是必要動作。 如需詳細資訊，請參閱 [/out (C#)](../../../../csharp/language-reference/compiler-options/out-compiler-option.md)。  
  
```csharp  
using System.Runtime.CompilerServices;  
using System;  
  
[assembly: InternalsVisibleTo("AssemblyB")]  
  
// The class is internal by default.  
class FriendClass  
{  
    public void Test()  
    {  
        Console.WriteLine("Sample Class");  
    }  
}  
  
// Public class that has an internal method.  
public class ClassWithFriendMethod  
{  
    internal void Test()  
    {  
        Console.WriteLine("Sample Method");  
    }  
  
}  
```  
  
 只有明確指定為 friend 的組件才能存取 `internal` 類型和成員。 例如，如果組件 B 是組件 A 的 friend，而且組件 C 參考組件 B，則 C 無法存取 A 中的 `internal` 類型。  
  
 編譯器會對傳遞給 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 屬性的 friend 組件名稱執行一些基本驗證。 如果組件 *A* 將 *B* 宣告為 friend 組件，則驗證規則如下：  
  
-   如果組件 *A* 具有強式名稱，則組件 *B* 也必須具有強式名稱。 傳遞給這個屬性的 friend 組件名稱必須包含組件名稱，以及簽署組件 *B* 時所用強式名稱金鑰的公開金鑰。  
  
     傳遞給 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 屬性的 friend 組件名稱不能是組件 *B* 的強式名稱 (請勿包含組件版本、文化特性、架構或公開金鑰語彙基元)。  
  
-   如果組件 *A* 不具強式名稱，friend 組件名稱只應包含組件名稱。 如需詳細資訊，請參閱[如何：建立未簽署的 Friend 組件 (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/how-to-create-unsigned-friend-assemblies.md)。  
  
-   如果組件 *B* 具有強式名稱，您必須使用專案設定或命令列的 `/keyfile` 編譯器選項，為組件 *B* 指定強式名稱金鑰。 如需詳細資訊，請參閱[如何：建立簽署的 Friend 組件 (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/how-to-create-signed-friend-assemblies.md)。  
  
 <xref:System.Security.Permissions.StrongNameIdentityPermission> 類別也提供共用類型的功能，但具有下列差異：  
  
-   <xref:System.Security.Permissions.StrongNameIdentityPermission> 適用於個別類型，而 friend 組件適用整個組件。  
  
-   如果要將組件 *A* 中數百個類型與組件 *B* 共用，必須將 <xref:System.Security.Permissions.StrongNameIdentityPermission> 新增至所有類型。 如果使用 friend 組件，您只需要宣告 friend 關聯性一次。  
  
-   如果使用 <xref:System.Security.Permissions.StrongNameIdentityPermission>，您要共用的類型必須宣告為 public。 如果使用 friend 組件，共用的類型會宣告為 `internal`。  
  
 如需如何從從模組檔 (副檔名為 .netmodule 的檔案) 存取組件之 `internal` 類型和方法的資訊，請參閱 [/moduleassemblyname (C#)](../../../../csharp/language-reference/compiler-options/moduleassemblyname-compiler-option.md)。  
  
## <a name="see-also"></a>另請參閱  
 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>   
 <xref:System.Security.Permissions.StrongNameIdentityPermission>   
 [如何：建立未簽署的 Friend 組件 (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/how-to-create-unsigned-friend-assemblies.md)   
 [如何：建立簽署的 Friend 組件 (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/how-to-create-signed-friend-assemblies.md)   
 [組件和全域組件快取 (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/index.md)   
 [C# 程式設計指南](../../../../csharp/programming-guide/index.md)
