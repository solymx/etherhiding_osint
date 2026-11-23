# New Group on the Block: UNC5142 Leverages EtherHiding to Distribute Malware

date: 2025.10.17
source: https://cloud.google.com/blog/topics/threat-intelligence/unc5142-etherhiding-distribute-malware

---

## Summary

etherhiding 就是將 c2 放在 blockchain 上面

unc5142 主要利用有漏洞的 wordpress 作為起手式

最終部署的惡意程式有觀察到有
- ATOMIC
- VIDAR
- LUMMAC.V2
- RADTHIEF
最終部署的惡意程式不是本文的重點，也不是以此去歸因為 UNC5142 ，這些惡意程式為資料竊取型惡意程式

---

## 攻擊概述
- CLEARSHORT ：一款多階段 JavaScript Downloader，用於發 payload
- 有漏洞的 wordpress 網站
- 智能合約
- etherHiding

下圖為 google 官方
![](https://storage.googleapis.com/gweb-cloudblog-publish/images/unc5142-etherhiding-fig1a.max-900x900.png)

### 第一階段

#### clearfake v.s clearshort

CLEARSHORT 是 CLEARFAKE 下載器的升級版，UNC5142 曾在 2023 年末至 2024 年中期的行動中使用過 CLEARFAKE。 

CLEARFAKE 是一個惡意 JavaScript 框架，偽裝成 Google Chrome 瀏覽器的更新通知。其嵌入的 JavaScript 的主要功能是在使用者點擊「更新 Chrome」按鈕後下載惡意程式碼。這個惡意程式碼的第二階段是儲存在 BNB 智慧鏈上部署的智慧合約中的 Base64 編碼 JavaScript 程式碼。

#### 常見第一階段

將惡意 js 放到有漏洞的 wordpress ，當受害者瀏覽，會透過惡意 js 連到智能合約拿下一段的惡意 js (CLEARSHORT 的登陸頁面)

#### 被入侵的 wordpress 網站

一般漏洞出現在三個地方
1. plugin (本身有漏洞)
2. Theme files: ex: index.php, header.php 等 (這些檔案被修改)
3. database (直接惡意檔案注入到 db)

### 文章有簡介智能合約

### Etherhiding 架構

取自 google 官方
![](https://storage.googleapis.com/gweb-cloudblog-publish/images/unc5142-etherhiding-fig4a.max-1100x1100.png)

## UNC5142 TTP 的演變

主要有 3 個變化
1. 用的合約越來越多
2. 濫用 Cloudflare Pages 等合法服務託管惡意誘餌
3. 從簡單的 Base64 編碼過渡到 AES 加密

<img width="484" height="604" alt="image" src="https://github.com/user-attachments/assets/e4ddb0c5-4bfc-4bb5-baf1-d62194c37222" />

上圖取自 google 官方

### 多合約架構

這種新架構借鑒了一種名為代理模式的合法軟體設計原則，開發者利用該原則使合約易於升級。

一個穩定且不可更改的代理會將呼叫轉發到一個獨立的二級合約，該二級合約可以被替換以修復錯誤或添加新功能。

這種架構採用高效率的路由-邏輯-儲存機制，每個合約都承擔特定的任務。這種設計允許快速更新攻擊的關鍵部分，
例如目標網頁 URL 或解密金鑰，而無需修改被入侵網站上的 JavaScript 程式碼。因此，攻擊活動更加靈活，也更難被下架。
