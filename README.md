# Mapable AI Studio

<p align="center"><img src="assets/logo%20-%20AI%20studio%20-%20white.png" alt="Mapable AI Studio" width="420"></p>
<p align="center"><strong>以 Mapable HK 路線證據為基礎的無障礙出行 AI 解說介面</strong></p>
<p align="center"><a href="https://ellthy0721.github.io/Mapable-AI-Studio/">線上版本</a> · <a href="https://github.com/Ellthy0721/Mapable-HK">Mapable HK</a> · <a href="https://ellthy0721.github.io/Mapable-HK/">Mapable HK 線上版</a></p>

## 項目簡介

Mapable AI Studio 是一個可由 GitHub Pages 直接託管的靜態 AI 路線建議介面。使用者輸入起點、終點和出行需要後，系統會先在瀏覽器內查找及比較路線，再把目前選取路線的結構化證據交給使用者指定的 AI API，生成繁體中文的走法說明、路線優點及注意事項。

本項目面向需要更容易理解路線資訊的長者、殘障人士、照顧者及一般乘客。AI 只負責解說既有路線證據，不負責憑空建立交通服務、票價、設施或無障礙條件。

> 重要：Mapable AI Studio 不是政府、公共交通營辦商、醫療機構、AI 供應商或緊急服務的官方產品。AI 回覆可能有錯誤或遺漏；出發前應以路線證據、營辦商公告及現場資訊為準。

## 與 Mapable HK 的關係

[Mapable HK](https://github.com/Ellthy0721/Mapable-HK) 是主要的香港無障礙優先多模式路線規劃器，負責搜尋地點、建立候選路線、套用出行 Profile、比較成本，以及呈現地圖、票價、站點、出口與資料風險。

Mapable AI Studio 是其延伸實驗介面，重用 Mapable HK 的路線服務、出行 Profile 和已整理資料快照，再加入以下能力：

- 把選定路線轉成結構化 JSON 證據。
- 讓使用者連接自己的 AI API、Endpoint 和 Model。
- 要求 AI 只根據所選路線解釋實際走法、好處和注意事項。
- 顯示發送給 AI 的路線證據及提示詞，方便檢查輸出依據。
- 以語音輸入旅程需要，並朗讀已生成的建議。

兩個倉庫獨立發佈。AI Studio 內的路線資料是隨發行包保存的快照，未必與 Mapable HK 每次更新即時同步。

## 主要功能

### 路線規劃

- 搜尋香港地點，或使用瀏覽器定位把目前位置設為起點。
- 支援步行、九巴、龍運巴士、城巴、新大嶼山巴士、港鐵巴士、港鐵、輕鐵及混合交通換乘。
- 比較時間、步行距離、轉乘、票價、候車、無障礙風險和資料可信度。
- 提供長者、輪椅、視障、色弱、嬰兒車／照顧者及一般六種出行 Profile。
- 顯示可選路線、摘要指標、分段步驟、沿途站點、港鐵出口及路線地圖。
- 在可用時加入即時到站、營運時間及目前天氣背景。

### AI 路線解說

- 只分析目前選取的路線，不把其他候選路線混入回覆。
- 固定以「路線怎麼走」、「這條路線的好處」和「注意事項」組織內容。
- 可選擇整段輸出或 Markdown 分點輸出。
- 把待核實、fallback 或連接可信度不足的資料明確帶入提示詞。
- 天氣資料可用時，只加入與步行、轉乘或候車直接相關的提醒。
- 切換路線後可為每一個候選方案分別生成和保存當前分頁內的分析結果。

### API 連接

- 提供常用 AI 供應商、Endpoint 和模型名稱快照。
- 支援直接輸入未列出的自訂 Endpoint 及 Model。
- 填妥 API Key、Endpoint 和 Model 後自動測試連接。
- 處理常見 Bearer Token、Anthropic `x-api-key` 及 Azure `api-key` 請求標頭。
- API 可用時，「查找路線」會同時規劃路線並請求 AI 建議。

供應商和模型清單只用作輸入捷徑，不代表服務可用性、瀏覽器 CORS 支援、帳戶權限、價格或模型名稱永遠有效。

### 語音與可讀性

- 支援瀏覽器語音辨識，從語句提取起點、終點及出行需要。
- 可選擇廣東話或普通話作語音偏好。
- 可使用瀏覽器語音合成朗讀 AI 建議。
- 尊重 `prefers-reduced-motion`，減少不必要動畫。
- 提供清晰狀態提示、可見標籤和響應式桌面／手機版面。

### 證據透明度

- 可展開查看發送給 AI 的路線證據 JSON。
- 可展開查看發送給 AI 的提示詞。
- 路線事實、AI 解說及錯誤狀態分開呈現。
- AI 回覆不會直接改寫 Mapable 路線、排序、票價或無障礙指標。

## 使用流程

1. 輸入起點和終點，或使用定位功能。
2. 選擇最符合乘客需要的出行 Profile。
3. 按「查找路線」取得 Mapable 路線候選。
4. 選擇要分析的路線並檢查路線步驟及地圖。
5. 在「連接 AI API」填入 API Key、Endpoint 和 Model。
6. 連接成功後生成 AI 路線解說。
7. 必要時查看 JSON 證據與提示詞，核對 AI 回覆是否有依據。

## 資料流程

```mermaid
flowchart LR
  A["起點、終點及出行 Profile"] --> B["Mapable 路線搜尋與成本比較"]
  B --> C["選取一條候選路線"]
  C --> D["建立路線、時間、天氣及風險 JSON"]
  D --> E["瀏覽器直接請求使用者指定的 AI API"]
  E --> F["繁體中文路線解說"]
  C --> G["路線步驟、地圖及原始證據"]
```

## 發送給 AI 的內容

AI 請求可包含以下資料：

- 起點和終點名稱及地點類型。
- 目前選取的出行 Profile。
- 所選路線的模式、時間、步行距離、票價、標籤和分段資料。
- 已知樓梯、斜坡、過路處、斜道、升降機及資料可信度摘要。
- 本地時間、目前地區及可用的天氣背景。
- 使用者選擇的輸出格式和語音偏好。

API Key 只用於請求驗證，不會放入路線證據、提示詞或頁面顯示的 JSON。

## 私隱與安全

- 項目沒有自有後端、帳號系統或 API 代理伺服器。
- API Key 只保存在目前瀏覽器分頁的記憶體及輸入欄位中，不會寫入此倉庫或路線資料。
- AI 請求由瀏覽器直接發送到使用者填寫的 Endpoint；資料處理受該第三方供應商的條款和私隱政策約束。
- 不應在共用或不受信任裝置輸入長期有效、權限過高或含有重要餘額的 API Key。
- 瀏覽器定位只在使用者啟動功能後用於設定起點和取得當前背景。
- 語音辨識及語音合成是否在裝置上處理，取決於瀏覽器與作業系統的實作。
- 地點搜尋、天氣、地圖、即時到站及 AI 功能會直接請求相應第三方服務。

純前端直接連接 AI API 適合展示、個人測試和原型驗證。正式多人服務應使用受控後端保存密鑰、限制來源、管理配額並記錄錯誤。

## 技術結構

- 原生 HTML、CSS 和 JavaScript。
- Mapable HK 搜尋、Profile、路線及資料服務。
- Leaflet 路線地圖及標記圖層。
- 瀏覽器 Fetch API 直接連接 AI 與開放資料服務。
- Web Speech API 提供語音辨識及朗讀。
- 本地靜態 JSON 提供地點、交通、票價、出口、設施及路線形狀。
- GitHub Actions 與 GitHub Pages 負責靜態部署。

## 倉庫結構

```text
.
├── index.html                 # AI Studio 介面及互動邏輯
├── styles/main.css           # Mapable 路線結果基礎樣式
├── scripts/services/         # 搜尋、Profile、資料及路線服務
├── data/                     # 發佈用交通、地點與無障礙資料
├── assets/                   # 品牌與路線圖示資源
├── .github/workflows/        # GitHub Pages 部署流程
└── README.md
```

## 本地執行

項目使用 `fetch()` 讀取本地 JSON，請不要直接以 `file://` 開啟 `index.html`。在倉庫根目錄執行：

```powershell
python -m http.server 8080
```

然後開啟 <http://localhost:8080/>。

如連接 AI API，瀏覽器必須能從目前來源直接請求該 Endpoint。若供應商不允許跨來源請求，即使密鑰和模型正確，連接測試仍可能失敗。

## 部署

`main` 分支保存可由 GitHub Pages 發佈的靜態內容。推送後，既有 GitHub Actions 工作流程會部署網站：

<https://ellthy0721.github.io/Mapable-AI-Studio/>

部署前應確認 `index.html` 引用的腳本、樣式、資料及資源已一併更新。

## 已知限制

- AI 只能根據提供的證據生成文字，不能證明路線實際無障礙或設施當時可用。
- AI 仍可能誤讀 JSON、忽略限制或生成不受證據支持的描述。
- 路線、班次、票價、出口、設施和天氣資料可能過時、不完整或暫時不可用。
- AI Studio 的 Mapable 資料快照可能落後於 [Mapable HK](https://github.com/Ellthy0721/Mapable-HK) 最新版本。
- 供應商可能更改 Endpoint、認證方式、模型名稱、費率、配額或 CORS 政策。
- 部分瀏覽器不支援語音辨識，或只支援特定語言和語音。
- 在緊急情況下不要依賴 AI 建議，應立即致電香港緊急服務 `999`。

## 瀏覽器支援

建議使用近期版本的 Chrome、Edge、Firefox 或 Safari。核心路線功能依賴 Fetch API、Geolocation API、CSS Grid、Flexbox 及 JavaScript；語音功能另依賴瀏覽器對 Web Speech API 的支援。

## 資料來源與授權

路線和無障礙資料的主要來源、構建方式、覆蓋範圍及限制記錄於 [Mapable HK `reference.md`](https://github.com/Ellthy0721/Mapable-HK/blob/main/reference.md)。各地圖、交通、設施、字體、第三方程式庫及開放資料分別受提供者條款、版權或開放資料許可約束。

本倉庫目前未附加統一的程式碼許可證。除非另有明確說明，倉庫內容不自動授予再使用許可。

## 問題回報

報告問題時，請提供起點、終點、Profile、所選路線、AI 供應商、Endpoint 類型、模型、瀏覽器、錯誤訊息及預期結果。不要在公開 Issue、截圖或日誌中提交 API Key、精確住址、即時位置或其他個人資料。

## 鳴謝

感謝 Mapable HK 使用的香港開放資料提供機構、公共交通營辦商、OpenStreetMap、HOTOSM、Hong Kong Community GTFS、Leaflet 及相關開放資料社群，也感謝提供瀏覽器可連接模型服務的 AI 平台。
