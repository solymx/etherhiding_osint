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

