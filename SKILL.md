---
name: tech-article-writer
version: 1.2.5
description: |
  給一個技術題目與發布場景（internal 內部技術分享／blog 公開部落格／social 社群短文），先做多來源深度查證並經大綱確認，產出最新、可溯源、無 AI 味的技術分享文章。預設 zh-TW（技術名詞、程式碼、專有名詞保留英文），可指定英文。
  觸發時機：使用者說「幫我寫一篇關於 X 的技術分享」「寫篇文章介紹 X」「這個題目寫成部落格文／社群短文」，或給出題目並要求產出文章。
  不要觸發：改寫或潤稿既有文章（那是 speak-human-tw 的職責）、純翻譯、產生程式碼、行銷文案、官方文件／README。
user-invocable: true
license: MIT
changelog:
  - "1.2.5 (2026-07-21): 平台確認清單三件事→四件事，新增「標題長度上限：超限先砍 SEO 價值最低的詞組、其餘維持全拼一致」；源自 iT邦幫忙標題 100 字元限制。"
  - "1.2.4 (2026-07-21): 邊界修訂——平台不渲染 mermaid 時允許把自己的 mermaid 決定性轉為圖片檔（格式轉換非 AI 生圖）；源自首篇實戰 iT邦幫忙發布（mermaid 顯示為程式碼牆）。"
  - "1.2.3 (2026-07-21): 標題搜尋規則補充「同類名詞縮寫一致性：全拼或全縮，不混用」；源自首篇實戰標題定稿。"
  - "1.2.2 (2026-07-21): scenes.md blog 場景新增「發文前確認平台三件事」（標題兼 meta？mermaid 渲染？表格支援？）；源自首篇實戰發布到 iT邦幫忙的平台限制。"
  - "1.2.1 (2026-07-21): scenes.md blog 場景新增標題搜尋規則——新詞完整拼出（精確詞組匹配）、低競爭新詞優先入標、縮寫式範圍丟失中間詞；源自首篇實戰標題討論。"
  - "1.2.0 (2026-07-21): 新增「規則收割」流程節——使用者回饋揭露的缺陷類型歸納成規則寫回 references，形成長期進化循環；style-guide 新增「模板元素各自成段」與「圖說斜體」；final-review 維度 5 補段落密度檢查。首篇實戰共收割 11 條規則。"
  - "1.1.1 (2026-07-21): 條列與散文仲裁規則新增「日期連鎖」子案——三個以上帶日期的連續事件用日期開頭的條列，日期在散文裡會被淹沒；源自首篇實戰 bad case。"
  - "1.1.0 (2026-07-21): 階段 5 新增第四道自檢「對抗式終審」（references/final-review.md）——每次執行由全新 context 審稿 subagent 依八維度檢查（通順／文字正確／引用對位／保真紀律／結構排版／視覺／de-AI／一致性），修復採「修一類不修一點」；交付摘要新增終審結果欄。源自首篇實戰：三道自動自檢抓不到的問題類別全由新眼睛發現。"
  - "1.0.6 (2026-07-21): style-guide 自我編輯節新增「修一類，不修一點」——review 發現問題先找同類全部實例一次修完，新規則要回頭重掃全文；源自首篇實戰同型錯誤二度被抓。"
  - "1.0.5 (2026-07-21): style-guide Diátaxis 節新增「Explanation 必答三問：是什麼／因應什麼／接下來看什麼（可觀察指標，不預言）」；源自首篇實戰 bad case（判定缺因果鋪墊顯得突兀）。"
  - "1.0.4 (2026-07-21): style-guide 結構規則新增「並列章節結構平行（定義→敘事→判定，定義在前）」；源自首篇實戰 bad case（五節格式不一、部分節缺定義開頭）。"
  - "1.0.3 (2026-07-21): style-guide 排版規則新增「mermaid 圖自帶 %%{init}%% 配色主題」——不依賴渲染平台預設，序數資料單色相漸層＋依底色深淺配字色；源自首篇實戰 bad case（預設主題底字撞色）。"
  - "1.0.2 (2026-07-21): style-guide 句子規則新增三條——日期一律絕對、比喻要付解釋成本、條列與散文的取捨仲裁（Google 列舉規則 vs de-AI 降格式規則的裁決）；均源自首篇實戰 bad case。"
  - "1.0.1 (2026-07-21): style-guide 名詞紀律新增「人名／機構名以全文出現順序首次定義（含表格與圖說）」，源自首篇實戰 bad case。"
  - "1.0.0 (2026-07-21): 初版。config 初始化＋六階段流程＋四個 references。"
---

# tech-article-writer

給一個技術題目與發布場景，經多來源深度查證與大綱關卡確認後，產出最新、可溯源、無 AI 味的技術分享文章。

## 透明性聲明（開源審計用）

本 skill 會做的網路存取與檔案寫入僅限以下項目，除此之外不做任何網路或檔案操作：

- **網路存取**：階段 2 深度查證時的 WebSearch／WebFetch；交付前 link check 用的 `curl -sIL`（跟隨轉址後以最終 HTTP 狀態碼判定）
- **檔案寫入**：skill 目錄下的 `config.json`；`output_dir` 下每個題目的文章資料夾（`research-digest.md`、`outline.md`、`article-<scene>.md`）

## 使用者設定（config.json）

Schema：

```json
{"output_dir": "<絕對路徑>"}
```

`config.json` 位於 skill 目錄下（與本檔同層），列入 `.gitignore`，不隨 repo 發布。

**初始化防呆**（缺一不可）：

1. 提問輸出位置時可附建議值，但必須等使用者明確回答才寫入 config；不得因使用者無回應就自動採用建議值
2. `config.json` 存在但 JSON 壞損、或缺 `output_dir` 欄位 → 視同不存在：回報壞損內容並重新提問；不得沿用片段或自行猜補
3. 非互動環境（一次性 CLI 呼叫、CI、排程）且無有效 config → 中止並回報「需先互動執行一次完成初始化」；不得自行猜路徑寫檔

## 六階段流程

工作資料夾：`<output_dir>/<YYYY-MM-DD>-<topic-slug>/`，一題一夾（topic-slug：題目的英文 kebab-case 短語；中文題目改用其英文技術關鍵詞，例如「React Server Components 的現況」→ `react-server-components`）。

### 階段 1：初始化檢查、收題與判場景

skill 目錄沒有 `config.json` 時先完成上方初始化，才繼續。收題目＋場景（`internal`／`blog`／`social`，定義見 references/scenes.md）＋語言（預設 zh-TW）；場景沒給就問一題。檢查同題目資料夾是否已有可重用的 research（見下方「research 重用」）。

### 階段 2：深度查證

每篇必做，無輕量模式。派平行 subagent 分四路搜尋，產出 `research-digest.md`。協定、來源分級、交叉驗證規則與 digest 格式（「research-digest.md 格式」一節）見 references/research-protocol.md。

### 階段 3：大綱關卡（唯一人工確認點）

交付以下五項等使用者確認（欄位定義見 references/style-guide.md「動筆前：讀者與類型」）：目標讀者＋先備知識、Diátaxis 主類型、切角、逐節大綱＋來源、親身素材徵詢；並同時附上 `research-digest.md` 的分級來源清單供一併簽核。使用者調整完才動筆；確認後把定稿的切角與大綱寫入工作資料夾 `outline.md`。此關卡是全流程唯一的人工確認點。

### 階段 4：撰寫

按 references/scenes.md 的場景規格、references/style-guide.md 的手法、references/de-ai-rules.md 的硬約束下筆，第一稿就寫乾淨；關鍵技術主張標來源連結。

### 階段 5：自檢（四道，全自動）

(a) **保真回讀**：文中每個技術主張都要能對回 `research-digest.md` 的來源；對不回的刪除或標「需查證」，不留無源主張

(b) **去 AI 味自評**：內化 references/de-ai-rules.md 的 checklist，逐段自問終檢問句「這篇哪裡一看就是 AI 寫的？」

(c) **link check**：

```bash
# 對文章內每個引用 URL 執行；2xx/3xx 過關，其餘視為死鏈（換來源或明確標註）
curl -sIL -o /dev/null -w "%{http_code}" --max-time 15 "<url>"
```

(d) **對抗式終審**：派一個全新 context 的審稿 subagent，依 [references/final-review.md](references/final-review.md) 的八個維度檢查（通順、文字正確、引用對位、保真紀律、結構排版、視覺、de-AI 硬約束、全文一致性）；findings 依「修一類，不修一點」修復，Critical／Important 修後聚焦複審

### 階段 6：交付

`article-<scene>.md` 寫入工作資料夾，附交付摘要：字數、來源數（分級統計）、資訊基準日、時效警示點、終審結果（輪數與發現數）。初稿完成後不再設人工關卡，改稿走事後修改。

## research 重用

同題目資料夾已有 `research-digest.md` 時直接重用、不重跑查證。抓取日期超過 14 天，先提醒可能過期，問使用者是否要重新查證。衍生場景版本時共用既有的 `research-digest.md` 與 `outline.md`、不重新過大綱關卡，只依新場景規格撰寫並新增 `article-<scene>.md`。

## 邊界

- 不改寫既有文章
- 不做行銷文案、不寫官方文件／README
- 不自動發布到任何平台（Confluence／Medium／社群貼文都是使用者的動作）
- **不虛構作者經驗（鐵律）**：人味段落（踩坑經驗、立場轉折）需要親身素材時，在大綱關卡向使用者索取；使用者沒提供，就在對應位置輸出「（需作者補充：⋯）」佔位，絕不代編
- 不生成圖片：需要架構圖／流程圖時用 mermaid 區塊，或標注「建議配圖」位置；發布平台不渲染 mermaid 時，可把自己寫的 mermaid 決定性轉出為圖片檔交付（本機瀏覽器渲染截圖，屬格式轉換，不是 AI 生圖）
- v1 不含 evals／benchmark、不含 voice calibration

## 規則收割（交付後）

交付不是終點。使用者回饋若揭露新的缺陷類型（不是單一錯字，而是一「類」問題），照這個循環處理：

1. 修當下的實例，並依「修一類，不修一點」（style-guide 自我編輯節）掃全文修完同型實例
2. 把缺陷歸納成一條通用規則，寫進對應的 references 檔，行尾標注「（日期 實戰 bad case）」
3. bump patch version、changelog 記一筆「規則＋出處」
4. 累積的 bad case 即是未來 evals 的種子用例

規則只從真實缺陷長出來，不憑空設計；同型錯誤被使用者抓到第二次，代表第 1 步的重掃沒做完整。

## 參考導航

- [references/research-protocol.md](references/research-protocol.md) — 查證協定：來源分級、四路搜尋、交叉驗證、research-digest.md 格式
- [references/style-guide.md](references/style-guide.md) — 寫作手法：讀者定位、BLUF、結構、句子、名詞紀律、Diátaxis 分類、zh-TW 適配決議
- [references/de-ai-rules.md](references/de-ai-rules.md) — 去 AI 味規則：生成時硬約束、register 界線、正向訊號、終檢自問
- [references/scenes.md](references/scenes.md) — 場景規格：`internal`／`blog`／`social` 的篇幅、讀者假設、結構要點
- [references/final-review.md](references/final-review.md) — 交付前終審：八維度對抗式 review 與修復紀律
</content>
