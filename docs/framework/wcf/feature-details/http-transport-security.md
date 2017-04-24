---
title: "HTTP 傳輸安全性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d3439262-c58e-4d30-9f2b-a160170582bb
caps.latest.revision: 14
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 14
---
# HTTP 傳輸安全性
使用 HTTP 來傳輸時，會由安全通訊端層 \(SSL\) 實作提供安全性。  在網際網路上會廣泛使用 SSL 以對用戶端驗證服務，進而對通道提供機密性 \(加密\)。  這個主題會說明 SSL 的運作方式，以及如何在 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中實作 SSL。  
  
## 基本 SSL  
 利用銀行網站這個典型案例，就可以明白解釋 SSL 的運作方式。  這些銀行網站可讓客戶透過使用者名稱和密碼進行登入。  在通過驗證之後，使用者就可以開始執行交易，例如檢視帳戶結餘、付款以及將存款從某個帳戶移到其他帳戶等。  
  
 使用者第一次瀏覽網站時，SSL 機制會與使用者的用戶端 \(在這個例子中為 Internet Explorer\) 開始一系列的交涉，而這個動作就稱為「*信號交換*」\(Handshake\)。  SSL 會先對客戶驗證銀行網站。  這是很重要的一點，因為客戶必須先確定所進行通訊的網站是真正的網站，而不是嘗試誘惑他們輸入使用者名稱和密碼的詐騙網站。  SSL 會使用 VeriSign 這類信任授權單位所提供的 SSL 憑證來進行此驗證。  這種驗證方式的邏輯如下：VeriSign 會擔保銀行網站的身分識別。  由於 Internet Explorer 信任 VeriSign，就表示也會信任該網站。  如果您要聯繫 VeriSign，只要按一下 VeriSign 標誌即可。  接著就會顯示真實性聲明，其中並有到期日和發出的對象 \(銀行網站\) 等資訊。  
  
 要初始化安全工作階段時，用戶端會將同等於 "hello" 的訊息傳送至伺服器，其中並有用戶端可用來簽署、產生雜湊並用來加密和解密的密碼編譯演算法清單。  而網站的回應，則是將認可和所選擇的其中一個演算法套件傳回用戶端。  在此初始信號交換期間，雙方都會傳送和接收 Nonce。  *Nonce* 是一種隨機產生的資料片段，在與網站的公開金鑰結合之後可用來建立雜湊。  「*雜湊*」\(Hash\) 是透過標準演算法 \(例如 SHA1\) 從兩個數字中衍生的新數字   \(用戶端和網站也會交換訊息，以同意要使用的雜湊演算法\)。雜湊是獨一無二的，而且只能用於用戶端和網站之間的工作階段，以加密和解密訊息。  用戶端和服務都擁有原始 Nonce 和憑證的公開金鑰，因此這兩端才會產生相同的雜湊。  因此，用戶端可透過 \(a\) 使用同意的演算法從資料計算雜湊，以及 \(b\) 與服務傳送的雜湊相比較的方式，驗證服務所傳送的雜湊；如果兩者相符，用戶端就可以確定雜湊未遭受竄改。  用戶端接著會使用此雜湊做為金鑰，以加密其中還含有其他新雜湊的訊息。  服務可以使用雜湊來解密訊息，並復原這個所謂的第二到最後的雜湊。  現在這兩端都明確知道此累積資訊 \(Nonce、公開金鑰和其他資料\)，就可以建立最終雜湊 \(或主要金鑰\)。  將使用下一個到最後一個雜湊，並以加密形式傳送這個最終金鑰。  接著會使用主要金鑰來加密和解密訊息，以重設工作階段。  由於用戶端和服務使用了相同的金鑰，這個金鑰也就稱為「*工作階段金鑰*」\(Session Key\)。  
  
 工作階段金鑰也可以稱為對稱金鑰，或者「共用密碼」。對稱金鑰相當重要，因為它可以減少交易兩端所需的計算。  如果每則訊息都要求重新交換 Nonce 和雜湊，就會降低效能。  因此，SSL 的終極目標就是使用對稱金鑰，讓訊息在擁有極佳的安全性和有效性之下，仍可自由地在這兩端之間傳送。  
  
 之前的描述只要概要說明，因為每個網站所使用的通訊協定都不盡相同。  也可能用戶端和網站都會產生在信號交換期間以演算法系統結合的 Nonce，在交換資料期間一方面增加了複雜度但也提供更優良的保護方法。  
  
### 憑證和公開金鑰基礎結構  
 在信號交換期間，服務也會將其 SSL 憑證傳送至用戶端。  憑證所含的資訊為：到期日、發行授權單位和網站的統一資源識別元 \(URI\)。  用戶端會比較此 URI 以及之前連絡時所用的原始 URI，確定相符之後也會檢查日期和發行授權單位。  
  
 每個憑證都有私密金鑰和公開金鑰這兩個金鑰，而這兩個金鑰也稱為「*交換金鑰組*」\(Exchange Key Pair\)。  簡而言之，只有憑證擁有者才知道私密金鑰，而公開金鑰則可以從憑證中讀取。  您可以使用任一金鑰來加密或解密摘要、雜湊或其他金鑰，不過前提是這兩個金鑰的作業必須為相反。  舉例來說，如果用戶端使用公開金鑰進行加密，則只有網站可以使用私密金鑰來解密訊息。  同樣地，如果網站使用私密金鑰進行加密，則用戶端可以透過公開金鑰來解密。  如此一來，用戶端便可確定只有私密金鑰的處理者可以交換訊息，因為只有以私密金鑰加密的訊息可以透過公開金鑰來解密。  網站會確定是與使用公開金鑰進行加密的用戶端來交換訊息。  這樣的交換只對初始信號交換來說是安全的，這也說明了何以我們較常透過建立實際的對稱金鑰來執行。  無論如何，所有通訊都會依據具有有效 SSL 憑證的服務。  
  
## 以 WCF 實作 SSL  
 將在外部對 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供 HTTP 傳輸安全性 \(或 SSL\)。  您可以使用這兩種方法實作 SSL；決定的因素則視裝載您應用程式的方式而定：  
  
-   如果正在使用 Internet Information Services \(IIS\) 做為 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 主機，請使用 IIS 基礎結構來設定 SSL 服務。  
  
-   如果正在建立自我裝載的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 應用程式，則可以使用 HttpCfg.exe 工具將 SSL 憑證繫結至位址。  
  
### 在傳輸安全性中使用 IIS  
  
#### IIS 7.0  
 若要將 [!INCLUDE[iisver](../../../../includes/iisver-md.md)] 設定為安全主機 \(使用 SSL\)，請參閱 [IIS 7.0 Beta：在 IIS 7.0 中設定安全通訊端層](http://go.microsoft.com/fwlink/?LinkId=88600)。  
  
 若要設定憑證以與 [!INCLUDE[iisver](../../../../includes/iisver-md.md)] 搭配使用，請參閱 [IIS 7.0 Beta：在 IIS 7.0 中設定伺服器憑證](http://go.microsoft.com/fwlink/?LinkID=88595)。  
  
#### IIS 6.0  
 若要將 [!INCLUDE[iis601](../../../../includes/iis601-md.md)] 設定為安全主機 \(使用 SSL\)，請參閱[設定安全通訊端層](http://go.microsoft.com/fwlink/?LinkId=88601)。  
  
 若要設定憑證以與 [!INCLUDE[iis601](../../../../includes/iis601-md.md)] 搭配使用，請參閱 [Certificates\_IIS\_SP1\_Ops](http://go.microsoft.com/fwlink/?LinkId=88602)。  
  
### 對 SSL 使用 HttpCfg  
 如果您正在建立自我裝載的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 應用程式，請從 [Windows XP Service Pack 2 支援工具網站](http://go.microsoft.com/fwlink/?LinkId=29002)下載 HttpCfg.exe 工具。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]使用 HttpCfg.exe 工具以使用 X.509 憑證設定連接埠的詳細資訊，請參閱 [HOW TO：使用 SSL 憑證設定連接埠](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)。  
  
## 請參閱  
 [傳輸安全性](../../../../docs/framework/wcf/feature-details/transport-security.md)   
 [訊息安全性](../../../../docs/framework/wcf/feature-details/message-security-in-wcf.md)