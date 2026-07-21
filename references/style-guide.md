# 寫作手法（style guide）

權威來源：Google Technical Writing Courses（One + Two，20 單元全讀）、Microsoft Writing Style
Guide、Apple Style Guide、Diátaxis Framework。每條規則行尾附原始出處 URL（規則的溯源以此為準；
整理過程使用的 digest 檔屬維護者設計素材，不隨 repo 發布）。

## Contents
- 動筆前：讀者與類型
- 開場（BLUF）
- 結構
- 句子
- 名詞紀律
- 程式碼與排版
- Diátaxis 分類與圍欄
- 自我編輯
- zh-TW 適配決議

## 動筆前：讀者與類型

- 讀者定位必填：大綱關卡必填「目標讀者＋假設先備知識」，決定內容的省略與鋪陳深度（https://developers.google.com/tech-writing/one/documents）

場景（`internal`／`blog`／`social`，定義見 scenes.md）決定預設讀者假設與篇幅，可在大綱關卡覆寫。

**大綱關卡必填欄位**（唯一人工確認點，交付以下五項等使用者確認；來源：spec §3、§4，非外部規則，故不附 URL）：

1. 目標讀者＋先備知識
2. Diátaxis 主類型（判定方式見下方「Diátaxis 分類與圍欄」節）
3. 切角：為什麼現在值得寫、對讀者的一句話價值
4. 逐節大綱＋來源：每節一句話說明內容，並標示取材自哪個分級來源（L1–L4，定義見 research-protocol.md）
5. 親身素材徵詢：有沒有相關踩坑經驗／立場想放進去

## 開場（BLUF）

- 首段講明解決什麼問題、適用場景、讀完帶走什麼；把最重要的答案放在最前面——多數讀者只讀第一段，核心結論不能留到最後（https://developers.google.com/tech-writing/one/documents）

## 結構

- 先寫大綱再動筆，用大綱把相關主題分組、定位哪裡需要補細節（https://developers.google.com/tech-writing/two/large-docs）
- 任務式標題：標題命名讀者要完成的任務，不用內部術語或工具名稱（https://developers.google.com/tech-writing/two/large-docs）
- 並列章節結構平行：逐一介紹 N 個同類概念時，各節採同一內部模板（一句白話定義 → 因應什麼 → 敘事 → 判定），定義永遠在最前；清單平行規則的章節級延伸（2026-07-21 實戰 bad case）
- 模板元素各自成段：定義、因應、敘事、判定各是一個任務，不擠進同一段——密集段落即使內容正確也難掃讀（2026-07-21 實戰 bad case）
- 標題後接引導句：每個標題（含子標題）在深入內容或帶出更低層標題之前，先給一句引導句（https://developers.google.com/tech-writing/two/large-docs）
- 段落首句破題：把段落的核心論點放在第一句，因為忙碌的讀者可能只看這一句（https://developers.google.com/tech-writing/one/paragraphs）

## 句子

- 預設主動語態；只有施事者無關或未知時才用被動（https://developers.google.com/tech-writing/one/active-voice）
- 一句一事：每個句子只限定一個概念、一個想法（https://developers.google.com/tech-writing/one/short-sentences）
- 行內列舉轉條列：句子裡用逗號或 or／and 串起來的並列項目，改寫成條列（https://developers.google.com/tech-writing/one/lists-and-tables）
- 清單項嚴格平行：同一份清單裡的文法結構、邏輯分類、大小寫、結尾標點都要一致（https://developers.google.com/tech-writing/one/lists-and-tables）
- 條列與散文的取捨仲裁：並列同構的多項事實用條列（上一條規則）；有因果或敘事流的內容維持散文。de-ai-rules 反對的是把敘事切碎成清單，不是禁用清單；全段最重要的結論獨立成段，不埋進清單。日期連鎖（三個以上帶日期的連續事件）用日期開頭的條列呈現，日期在散文裡會被淹沒（2026-07-21 實戰 bad case ×2）
- 日期一律絕對：不寫「昨天／前天／上週」這類相對時間，文章不是日記，發布後相對日期立即失真；敘事中的相對間隔（「六天後」）必須錨定在前文已給出的絕對日期上（2026-07-21 實戰 bad case）
- 比喻要付解釋成本：「敘事凝固」這類抽象比喻，讀者第一眼看不懂就換白話；要保留比喻，就在同一句給出白話對應（2026-07-21 實戰 bad case）

## 名詞紀律

- 一詞一義：同一概念全篇不換字，官方大小寫照抄如 `TypeScript`（https://learn.microsoft.com/en-us/style-guide/word-choice/use-technical-terms-carefully）
- 官方大小寫延伸：產品／服務／技術名稱的大小寫比照官方原始寫法，不自行正規化，也不新造內部大小寫（https://learn.microsoft.com/en-us/style-guide/capitalization）
- 首次出現即定義：不熟悉的名詞第一次出現就要定義；名詞多時集中整理成詞彙表（https://developers.google.com/tech-writing/one/words）
- 人名與機構名比照辦理，且以「全文出現順序」計算首次——表格、圖說常排在正文前，其中的人名也要帶身分（例：「Peter Steinberger（OpenClaw 創辦人）」），不得先用名字、後文才補介紹（2026-07-21 首篇實戰 bad case）

## 程式碼與排版

- 程式碼只貼關鍵邏輯：只留下教學重點必要的部分，其餘該刪就刪（https://developers.google.com/tech-writing/two/sample-code）
- 註解講 why 不講 what：對有經驗的讀者，程式碼註解要說明「為什麼這樣做」，不是重述「做了什麼」（https://developers.google.com/tech-writing/two/sample-code）
- 引用的範例碼須驗證可跑：每份範例都要能建置無誤，且真的完成它宣稱要做的事（https://developers.google.com/tech-writing/two/sample-code）
- 比較用表格：需要比較的資訊改用表格呈現（來源：使用者提供之寫作心法，經 spec §6 採納；三份 digest 無對應原始規則行，故不附 URL）
- 資訊階層靠標題與留白：用標題分層、短段落製造留白，取代堆疊大段文字（https://learn.microsoft.com/en-us/style-guide/scannable-content/）
- mermaid 圖自帶配色主題：區塊開頭用 `%%{init}%%` 指定明確的底色與文字色，不依賴渲染平台的預設主題（預設主題常見底色與文字對比不足）。時間軸／序數資料用單一色相由淺到深，深色底配白字、淺色底配深字；顏色階距要拉開到肉眼可辨；圖示語言說明以斜體圖說（*…*）緊跟圖後（2026-07-21 實戰 bad case）
- 程式碼與正文不需反覆對照：讀者複製貼上程式碼後會需要的說明，直接寫進程式碼註解，讓程式碼自身可讀，不必要求讀者回頭對照正文（https://developers.google.com/tech-writing/two/sample-code）

## Diátaxis 分類與圍欄

- 大綱關卡定主類型：對整篇文章（甚至單一段落、單一句子）都要問「這是行動還是認知？是習得還是應用？」，決定這篇文章的主要服務對象（https://diataxis.fr/compass/）
- Explanation 型文章必答三問：是什麼（定義）、因應什麼（這個東西為了解決什麼問題而出現）、接下來看什麼（展望用「可觀察的指標」表達，不做預言）；只答第一問的概念介紹會讓判定顯得突兀（2026-07-21 實戰 bad case）
- 次類型只能以明確圍欄區塊出現：把兩種文件類型混在同一份內容裡會同時損害雙方的品質（https://diataxis.fr/reference-explanation/）；因此主類型以外的內容只能收進清楚標示的獨立區塊（例如 Explanation 文中一小段標明的「步驟」區塊），不能逐句混雜（圍欄機制為推導規則，非 diataxis.fr 原文）
- 社群短文禁止混型：social 場景篇幅太短，容不下圍欄區塊，主類型只能是壓縮過的 Explanation 論點，不得混型（推導規則，非 diataxis.fr 原文；框架出處 https://diataxis.fr/）

## 自我編輯

- 延遲重讀：把稿子放一段時間，之後用新鮮的眼光重讀，再做最後編輯（https://developers.google.com/tech-writing/two/editing）
- checklist 自檢：訂一份風格檢查清單（或採用既有的），並讓每篇稿子都對照這份清單，維持前後一致（https://developers.google.com/tech-writing/two/editing）
- 修一類，不修一點：review 發現的每個問題都先問「同類問題全文還有幾處」，用 grep 或逐節掃描找出全部實例一次修完；新增規則後同樣拿新規則重掃全文——只修觸發點會讓同型錯誤反覆被讀者抓到（2026-07-21 實戰 bad case，同型錯誤第二次被使用者抓到）

## zh-TW 適配決議

以下 8 條為 2026-07-21 使用者簽核，全數採納，逐字搬入，不做語意調整：

1. 被動語態：不搬英文 be+p.p. 判別，改判「被／由／遭＋翻譯腔」→ 改主動（範例：❌「渲染效能因為新機制而被顯著地提升了」→ ✅「新的虛擬列表機制顯著提升了渲染效能」）
2. 字數門檻不硬換算：代名詞（它／這／該）與指涉對象隔超過一句就重複名詞；句長以一句一事為準
3. 段落 3–5 句為宜、超過 7 句必拆（照搬）
4. that/which 限定子句規則：僅英文版文章啟用
5. 標點：zh-TW 全形標點、破折號 300–500 字最多一次（沿用 speak-human-tw）；英文版採 Oxford comma、**避免 em dash**（來源衝突決議：Google/MS 允許，humanizer 列硬約束——humanizer 優先，因去 AI 味是本 skill 目的）
6. 縮寫：首次出現給英文全稱＋縮寫，不譯中文；有約定俗成中文名可括注；之後用縮寫
7. 第二人稱統一用「你」，允許省略主語
8. Diátaxis 三場景對應（推導規則，非 diataxis.fr 原文）：internal／blog 預設 Explanation、程序型題目走 How-to、social＝壓縮的 Explanation 論點；主類型在大綱關卡定案

（2026-07-21 使用者簽核）
