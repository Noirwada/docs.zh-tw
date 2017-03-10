---
title: "How to: Create a Lambda Expression (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "lambda expressions [Visual Basic]"
  - "expressions [Visual Basic], lambda"
ms.assetid: 3279bd5c-80f7-410a-a7ba-f7085ed36aa5
caps.latest.revision: 27
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 27
---
# How to: Create a Lambda Expression (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

「*Lambda 運算式*」\(Lambda expression\) 是不具名稱的函式或副程式，  當委派型別有效時，即可使用 Lambda 運算式。  
  
### 若要建立單行 Lambda 運算式函式  
  
1.  在可以使用委派型別的情形下，輸入關鍵字 `Function`，如下列範例所示：  
  
     `Dim add1 =`   `Function`  
  
2.  緊接著 `Function` 之後，於括號中輸入函式的參數。  請注意，不要在 `Function` 之後指定名稱。  
  
     `Dim add1 = Function`   `(num As Integer)`  
  
3.  在參數清單之後，輸入單一運算式做為函式主體。  運算式計算的值是函式傳回的值。  您不能使用 `As` 子句指定傳回型別。  
  
     [!code-vb[VbVbalrLambdas#1](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/Class1.vb#1)]  
  
     您可以藉由傳遞整數引數來呼叫 Lambda 運算式。  
  
     [!code-vb[VbVbalrLambdas#2](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/Class1.vb#2)]  
  
4.  或者，也可以透過下列範例來達到相同的結果：  
  
     [!code-vb[VbVbalrLambdas#3](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/Class1.vb#3)]  
  
### 若要建立單行 Lambda 運算式副程式  
  
1.  在可以使用委派型別的情形下，輸入關鍵字 `Sub`，如下列範例所示。  
  
     `Dim add1 =`   `Sub`  
  
2.  緊接著 `Sub` 之後，於括號中輸入副程式的參數。  請注意，不要在 `Sub` 之後指定名稱。  
  
     `Dim add1 = Sub`   `(msg As String)`  
  
3.  在參數清單之後，輸入單一陳述式做為副程式的主體。  
  
     [!code-vb[VbVbalrLambdas#17](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/Class1.vb#17)]  
  
     您可以藉由傳遞字串引數來呼叫 Lambda 運算式。  
  
     [!code-vb[VbVbalrLambdas#18](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/Class1.vb#18)]  
  
### 若要建立多行 Lambda 運算式函式  
  
1.  在可以使用委派型別的情形下，輸入關鍵字 `Function`，如下列範例所示。  
  
     `Dim add1 =`   `Function`  
  
2.  緊接著 `Function` 之後，於括號中輸入函式的參數。  請注意，不要在 `Function` 之後指定名稱。  
  
     `Dim add1 = Function`   `(index As Integer)`  
  
3.  請按 ENTER 鍵。  即會自動加入 `End Function` 陳述式。  
  
4.  在函式主體中，新增下列程式碼以建立運算式並傳回值。  您不能使用 `As` 子句指定傳回型別。  
  
     [!code-vb[VbVbalrLambdas#19](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/Class1.vb#19)]  
  
     您可以藉由傳遞整數引數來呼叫 Lambda 運算式。  
  
     [!code-vb[VbVbalrLambdas#20](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/Class1.vb#20)]  
  
### 若要建立多行 Lambda 運算式副程式  
  
1.  在可以使用委派型別的情形下，輸入關鍵字 `Sub`，如下列範例所示：  
  
     `Dim add1 =`   `Sub`  
  
2.  緊接著 `Sub` 之後，於括號中輸入副程式的參數。  請注意，不要在 `Sub` 之後指定名稱。  
  
     `Dim add1 = Sub`  `(msg As String)`  
  
3.  請按 ENTER 鍵。  即會自動加入 `End Sub` 陳述式。  
  
4.  在函式主體中，新增下列程式碼以在叫用副程式時加以執行。  
  
     [!code-vb[VbVbalrLambdas#21](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/Class1.vb#21)]  
  
     您可以藉由傳遞字串引數來呼叫 Lambda 運算式。  
  
     [!code-vb[VbVbalrLambdas#22](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/Class1.vb#22)]  
  
## 範例  
 Lambda 運算式的一般用途是定義函式，該函式可以傳遞為參數的引數，其型別為 `Delegate`。  在下列範例中，<xref:System.Diagnostics.Process.GetProcesses%2A> 方法會傳回本機電腦上執行之處理序的陣列。  <xref:System.Linq.Enumerable> 類別 \(Class\) 的 <xref:System.Linq.Enumerable.Where%2A> 方法需要 `Boolean` 委派做為其引數。  範例中的 Lambda 運算式便是用於此目的。  它會針對只有一個執行緒的各個處理序以及在 `filteredList` 中選取的處理序傳回 `True`。  
  
 [!code-vb[VbVbalrLambdas#10](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/Class4.vb#10)]  
  
 上述範例相當於使用 [!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext-md.md)] 語法撰寫的下列程式碼：  
  
 [!code-vb[VbVbalrLambdas#11](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/vbvbalrlambdas/Class5.vb#11)]  
  
## 請參閱  
 <xref:System.Linq.Enumerable>   
 [Lambda Expressions](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [Function Statement](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub Statement](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Delegates](../../../../visual-basic/programming-guide/language-features/delegates/delegates.md)   
 [How to: Pass Procedures to Another Procedure in Visual Basic](../../../../visual-basic/programming-guide/language-features/delegates/how-to-pass-procedures-to-another-procedure.md)   
 [Delegate Statement](../../../../visual-basic/language-reference/statements/delegate-statement.md)   
 [Introduction to LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)