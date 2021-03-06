---
title: "使用平台叫用封送處理資料 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "資料封送處理, 平台叫用"
  - "封送處理, 平台叫用"
  - "平台叫用, 封送處理資料"
ms.assetid: dc5c76cf-7b12-406f-b79c-d1a023ec245d
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# 使用平台叫用封送處理資料
若要呼叫從 Unmanaged 程式庫匯出的函式，.NET Framework 應用程式需要代表此 Unmanaged 函式之 Managed 程式碼中的函式原型。  若要建立使平台叫用正確地封送處理資料的原型，您必須執行下列動作：  
  
-   套用 [DLLImportAttribute](frlrfSystemRuntimeInteropServicesDllImportAttributeClassTopic) 屬性到靜態函式或 Managed 程式碼中的方法。  
  
-   將 Unmanaged 資料類型替代為 Managed 資料類型。  
  
 您可以使用 Unmanaged 函式所提供的文件，以選擇性欄位套用屬性，並且將 Unmanaged 資料類型替代為 Managed 資料類型，來建構對等的 Managed 原型。  如需有關如何套用 **DllImportAttribute** 的指示，請參閱[使用 Unmanaged DLL 函式](../../../docs/framework/interop/consuming-unmanaged-dll-functions.md)。  
  
 本節提供範例，示範如何建立 Managed 函式原型，供傳遞引數至函式和接收 Unmanaged 程式庫所匯出函式的傳回值。  此範例也會示範使用 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 屬性和 <xref:System.Runtime.InteropServices.Marshal> 類別來明確封送處理資料的時機。  
  
## 平台叫用資料類型  
 下表列出 Win32 API \(Wtypes.h 中所列\) 和 C 樣式函式中所使用的資料類型。  許多 Unmanaged 程式庫包含傳遞資料類型做為參數和傳回值的函式。  第三個行列出對應的 .NET Framework 內建實值類型或您在 Managed 程式碼中使用的類別。  在某些情況下，您可將本表格中所列的類型取代為相同大小的類型。  
  
|在 Wtypes.h 中的 Unmanaged 類型|Unmanaged C 語言類型|Managed 類別名稱|描述|  
|--------------------------------|----------------------|------------------|--------|  
|**HANDLE**|**void\***|<xref:System.IntPtr?displayProperty=fullName>|在 32 位元 Windows 作業系統上為 32 位元，在 64 位元 Windows 作業系統上為 64 位元。|  
|**BYTE**|**unsigned char**|<xref:System.Byte?displayProperty=fullName>|8 位元|  
|**SHORT**|**short**|<xref:System.Int16?displayProperty=fullName>|16 位元|  
|**WORD**|**unsigned short**|<xref:System.UInt16?displayProperty=fullName>|16 位元|  
|**INT**|**int**|<xref:System.Int32?displayProperty=fullName>|32 位元|  
|**UINT**|**unsigned int**|<xref:System.UInt32?displayProperty=fullName>|32 位元|  
|**LONG**|**long**|<xref:System.Int32?displayProperty=fullName>|32 位元|  
|**BOOL**|**long**|[\<caps:sentence id\="tgt48" sentenceid\="f5f846452032b75e5fcec49a05fe125a" class\="tgtSentence"\>System.Int32\<\/caps:sentence\>](https://msdn.microsoft.com/en-us/library/system.byte.aspx)|32 位元|  
|**DWORD**|**unsigned long**|<xref:System.UInt32?displayProperty=fullName>|32 位元|  
|**ULONG**|**unsigned long**|<xref:System.UInt32?displayProperty=fullName>|32 位元|  
|**CHAR**|**char**|<xref:System.Char?displayProperty=fullName>|使用 ANSI 裝飾。|  
|**WCHAR**|**wchar\_t**|<xref:System.Char?displayProperty=fullName>|使用 Unicode 裝飾。|  
|**LPSTR**|**char\***|<xref:System.String?displayProperty=fullName> 或 <xref:System.Text.StringBuilder?displayProperty=fullName>|使用 ANSI 裝飾。|  
|**LPCSTR**|**Const char\***|<xref:System.String?displayProperty=fullName> 或 <xref:System.Text.StringBuilder?displayProperty=fullName>|使用 ANSI 裝飾。|  
|**LPWSTR**|**wchar\_t\***|<xref:System.String?displayProperty=fullName> 或 <xref:System.Text.StringBuilder?displayProperty=fullName>|使用 Unicode 裝飾。|  
|**LPCWSTR**|**Const wchar\_t\***|<xref:System.String?displayProperty=fullName> 或 <xref:System.Text.StringBuilder?displayProperty=fullName>|使用 Unicode 裝飾。|  
|**FLOAT**|**浮動**|<xref:System.Single?displayProperty=fullName>|32 位元|  
|**DOUBLE**|**Double**|<xref:System.Double?displayProperty=fullName>|64 位元|  
  
 如需 C\# 和 C\+\+ 之 [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)] 中的對應類型，請參閱 [.NET Framework 類別庫簡介](../../../docs/standard/class-library-overview.md)。  
  
## PinvokeLib.dll  
 下列程式碼定義 Pinvoke.dll 所提供的程式庫函式。  本節所描述的許多範例會呼叫此程式庫。  
  
### 範例  
 [!code-cpp[PInvokeLib#1](../../../samples/snippets/cpp/VS_Snippets_CLR/pinvokelib/cpp/pinvokelib.cpp#1)]  
  
 [!code-cpp[PInvokeLib#2](../../../samples/snippets/cpp/VS_Snippets_CLR/pinvokelib/cpp/pinvokelib.h#2)]