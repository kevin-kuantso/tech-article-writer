# tech-article-writer

## 這個 skill 做什麼

給一個技術題目與發布場景（`internal` 內部技術分享／`blog` 公開部落格／`social` 社群短文），這個 skill 會先做多來源深度查證，經過大綱關卡讓你確認讀者定位、切角與逐節大綱後才動筆，產出最新、可溯源、無 AI 味的技術分享文章。

## 安裝

```bash
git clone <your-fork-url> ~/.claude/skills/tech-article-writer
```

`<your-fork-url>` 是你 fork 這個 repo 之後的實際網址，發布或安裝時自行替換——本 repo 不綁定特定 URL。

首次執行時會詢問輸出位置，並在 skill 目錄下生成 `config.json`；此檔案已列入 `.gitignore`，不會隨 repo 一起發布或進版控。

## 使用方式

三個輸入：

- **題目**：任何技術主題
- **場景**：`internal`／`blog`／`social`，沒指定會先問一題
- **語言**：預設 zh-TW（技術名詞、程式碼、專有名詞保留英文），可指定英文

**大綱關卡**（全流程唯一的人工確認點）：深度查證完成後，skill 會列出目標讀者＋先備知識、Diátaxis 主類型、切角、逐節大綱＋來源、親身素材徵詢這五項，連同查證來源的分級清單一併交付給你確認或調整；你確認後才會動筆寫文章。

呼叫範例：

```
你：幫我寫一篇關於「Core Web Vitals 優化」的技術分享，場景是 blog。

skill：
1. 若 config.json 不存在，先詢問輸出位置完成初始化
2. 確認題目／場景／語言（語言未指定則用 zh-TW）
3. 派 subagent 做多來源深度查證，產出 research-digest.md
4. 大綱關卡：列出目標讀者＋先備知識、Diátaxis 主類型、切角、逐節大綱＋來源、親身素材徵詢，等你確認
5. 你確認後動筆，跑完三道自檢（保真回讀、去 AI 味自評、link check）後交付 article-blog.md 與交付摘要
```

## 產出結構

```
<output_dir>/<YYYY-MM-DD>-<topic-slug>/
├── research-digest.md   # 分級查證來源紀錄
├── outline.md            # 大綱關卡確認後的定稿大綱與切角
└── article-<scene>.md   # 對應場景的完稿文章
```

同一題目換場景呼叫（例如先寫完 `internal` 再補 `blog`）時，沿用既有的 `research-digest.md` 與 `outline.md`，不重跑查證、不重新過大綱關卡，只依新場景的規格撰寫並新增對應的 `article-<scene>.md`；查證抓取日期超過 14 天時，會先提醒可能過期，問你是否要重新查證。

## References

- [Google Technical Writing Courses](https://developers.google.com/tech-writing) — 句子與文件結構骨幹
- [Diátaxis Framework](https://diataxis.fr)（Daniele Procida）— 文章類型分類
- [Microsoft Writing Style Guide](https://learn.microsoft.com/en-us/style-guide/welcome/) — 名詞一致性與語氣
- [Apple Style Guide](https://support.apple.com/guide/applestyleguide/) — 術語與格式慣例
- [blader/humanizer](https://github.com/blader/humanizer)（Siqi Chen，MIT）— AI 味 pattern 概念來源
- speak-human-tw（Raymond Hou，MIT）— zh-TW 去 AI 味與台灣在地化規則（已內化）
- [Anthropic Agent Skills best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices) — skill 撰寫規範

## License

MIT，見 [LICENSE](LICENSE)。

上方 References 表中的 blader/humanizer 與 speak-human-tw 皆為 MIT 授權專案；本 skill 內化了兩者的概念（AI 味 pattern 判斷、zh-TW 在地化去 AI 味規則），並已在表中標注來源與授權。
