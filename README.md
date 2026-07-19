# Mapable AI Studio

Mapable AI Studio 是一個可由 GitHub Pages 直接託管的靜態 AI 路線建議介面。使用者輸入起點、終點和出行需要後，系統會先查找項目路線，再按目前選取的路線向 AI 請求繁體中文 Markdown 建議。

## 使用

1. 開啟頁面並輸入起點和終點。
2. 如需 AI 建議，在「連接 AI API」中填入 API Key、Endpoint 和 Model。
3. API 連接成功後，主按鈕會同時查找路線並取得 AI 建議。

API Key 只保存在目前瀏覽器分頁的記憶體中，不會寫入此儲存庫。

## 本地預覽

GitHub Pages 及本地 HTTP 伺服器均可執行此版本。不要直接以 `file://` 開啟，因為瀏覽器可能阻擋本地 JSON 請求：

```powershell
python -m http.server 8080
```

然後開啟 <http://localhost:8080/>。

## 發行內容

- `index.html`：AI Studio 入口頁面
- `scripts/services/`：搜尋、出行偏好及路線服務
- `data/`：搜尋索引、交通資料、無障礙資料及路線形狀
- `assets/MTR_Exit_Sign.svg`：路線出口圖示
- `.github/workflows/pages.yml`：GitHub Pages 自動部署流程

路線服務保留項目原有的遠端 fallback，用於未打包的路網 tile 資料；主要搜尋、交通和無障礙資料已隨發行包提供。
