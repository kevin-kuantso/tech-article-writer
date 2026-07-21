# 去 AI 味規則（de-AI rules）

內化來源：`speak-human-tw` v1.4.0（38 種痕跡，Raymond Hou，MIT）＋ [`blader/humanizer`](https://github.com/blader/humanizer)（33 patterns，Siqi Chen，MIT）。素材：`research/humanizer-digest.md`（維護者設計素材，不隨 repo 發布；規則本身的出處以各行行尾標注為準）。以下規則在**生成時**直接避免，不是成稿後才回頭清洗。

## 生成時硬約束

草稿撰寫當下就要避免以下七種痕跡：

- **罐頭開場（時代大帽子）**：用「在這個⋯的時代」之類宏大敘事破題，取代真正的破題（❌「在這個 AI 快速發展的時代，開發者比以往任何時候都更需要掌握自動化工具。」）（內化自 speak-human-tw，Raymond Hou，MIT）
- **通用積極結論**：結尾給不具體的正向總結，沒有實際判斷或行動建議（❌「總而言之，這個方法能為團隊帶來更好的開發體驗。」）（內化自 speak-human-tw，Raymond Hou，MIT；humanizer 亦收錄：https://github.com/blader/humanizer）
- **立場真空（各有優缺點／因人而異）**：面對取捨不給判斷，用「各有優缺點」「視情況而定」帶過（❌「兩種方案各有優缺點，實際選擇因團隊而異。」）（內化自 speak-human-tw，Raymond Hou，MIT）
- **rule-of-three 濫用**：把內容硬湊成三項並列，不管是否真有三個對等要點（❌「這套工具具備輕量、彈性、高效能三大優勢。」）（內化自 speak-human-tw，Raymond Hou，MIT；humanizer 亦收錄：https://github.com/blader/humanizer）
- **「不是 A 而是 B」全篇最多一次**：這個對比句型全文只能出現一次，第二次即違規（❌ 全文重複兩次以上「不是 A，而是 B」句型，例如先寫「不是效能問題，而是架構問題」，稍後又寫「不是設計缺陷，而是取捨」）（內化自 speak-human-tw，Raymond Hou，MIT）
- **em dash（英文版禁用）**：英文版輸出不得使用 em dash（—）；zh-TW 版本本就不使用此符號，此條只對英文版有約束力（❌ "The refactor improved throughput — significantly."）（https://github.com/blader/humanizer）
- **無源權威鋪墊**：用「研究顯示」「業界普遍認為」等權威語氣起頭卻不附來源（❌「研究顯示，採用微前端架構能大幅降低耦合度。」）（內化自 speak-human-tw，Raymond Hou，MIT；humanizer 亦收錄：https://github.com/blader/humanizer）

## Register 界線

- 技術說明段落中性精確**就是**正確人聲，不需要刻意加入語氣或個人風格。（https://github.com/blader/humanizer）
- 人味只放在引言、結論、踩坑經驗段——這幾處才適合帶入立場、語氣轉折、真實情緒。（https://github.com/blader/humanizer）

## 正向訊號

- 具體到難以捏造的細節：真實數字、真實錯誤訊息、真實版本號，這種細節 AI 難以無中生有。（https://github.com/blader/humanizer）
- 長短句交錯：避免每句長度與結構都相近。（內化自 speak-human-tw，Raymond Hou，MIT；humanizer 亦收錄：https://github.com/blader/humanizer）
- 資訊密度不平均：最有話說的地方給兩倍篇幅，其餘從簡，不強求段落篇幅均等。（內化自 speak-human-tw，Raymond Hou，MIT）
- 允許不收尾：段落或小節可以在提出觀點後就結束，不必每段都補一句總結。（內化自 speak-human-tw，Raymond Hou，MIT）

## zh-TW 層

- 全形標點：中文內文一律使用全形標點符號。
- 破折號：每 300–500 字最多用一次，不得連續使用。
- 台灣用語：優先使用台灣慣用詞彙與語序。
- 中國用語替換（節錄，內化自 speak-human-tw）：

| 中國用語 | 台灣用語 |
|---|---|
| 視頻 | 影片 |
| 質量 | 品質 |
| 信息 | 資訊 |
| 軟件 | 軟體 |
| 網絡 | 網路 |

以上詞表精神內化自 speak-human-tw（Raymond Hou，MIT）。

## 技術文章專屬 AI 味（自建）

上游兩份來源皆未覆蓋技術文章特有的 AI 味，以下四種為本 skill 自建：

- **過度解釋 trivial code**：對一望即知的程式碼行逐字翻譯成中文說明（❌ 為 `let count = 0` 加註解「宣告一個變數 count，並將其初始值設為 0」）
- **罐頭免責聲明**：不具體、可套用在任何文章的警語（❌「需要注意的是，實際結果可能因環境不同而有所差異。」）
- **每段結尾總結一次**：機械式地在每個段落最後補一句總結，不管是否需要（❌ 每段最後都寫「總結來說，這個做法能有效解決上述問題。」）
- **目錄式導言**：開頭條列整篇文章架構，取代真正的破題（❌「本文將依序介紹背景、原理、實作方式與未來展望。」）

## 終檢自問

- 逐段自問：「這篇哪裡一看就是 AI 寫的？」——初稿完成後逐段掃一次，把答得出來的痕跡改掉（https://github.com/blader/humanizer）。
- 不虛構作者經驗（鐵律）：人味段落（踩坑經驗、立場轉折）需要親身素材時，先在大綱關卡向使用者索取；使用者沒提供，就在對應位置輸出「（需作者補充：⋯）」佔位，絕不代編。
