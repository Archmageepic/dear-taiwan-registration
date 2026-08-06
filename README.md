# 《給台灣的情書 Dear Taiwan,》活動報名網頁

這個專案同時保留 Google Apps Script 網頁版，並提供適合 Facebook 內建瀏覽器的 GitHub Pages 靜態前端。兩個入口都會將報名資料寫入同一份 Google 試算表。

## 部署方式

1. 開啟 [Google Apps Script](https://script.google.com/) 並建立「新專案」。
2. 將預設的 `Code.gs` 內容替換成此資料夾中的 `Code.gs`。
3. 點選左側「＋」→「HTML」，檔名輸入 `Index`，將 `Index.html` 全部貼入。
4. 點選左側「專案設定」，勾選「在編輯器中顯示 appsscript.json 資訊清單檔案」。
5. 將 `appsscript.json` 替換成此資料夾中的版本。
6. 右上角點選「部署」→「新增部署作業」→ 類型選「網頁應用程式」。
7. 「執行身分」選「我」；「誰可以存取」選「任何人」。
8. 按「部署」並完成授權，即可取得公開網址。

## 資料流向

- 專用試算表：[給台灣的情書－活動報名名單](https://docs.google.com/spreadsheets/d/1jNHRx9anGAbPIbya6jB2NZVbZxEYB2c1ftaejWN-aTo/edit)
- `基本資料` 頁籤保存報名時間、姓名、Email、嘖嘖贊助編號（選填）、年齡、居住地、留言及所有報名場次。
- 每個活動另有獨立頁籤，保存該場次報名者的姓名、Email 與嘖嘖贊助編號（選填）。
- `Code.gs` 會驗證必填欄位、活動選項及 Email 格式，並使用寫入鎖避免同時送出造成資料覆蓋。
- 主視覺圖片存放於專案的 Google Drive 資料夾；`Code.gs` 會透過檔案 ID 讀取並嵌入網頁。圖檔不需設定為公開，但部署帳號必須保有檔案讀取權限。
- 若活動選項或頁籤名稱變更，需同步更新 `Index.html` 與 `Code.gs` 的 `EVENT_SHEET_MAP`。

## GitHub Pages 版本

`github-pages` 資料夾內是可直接發布到 GitHub Pages 的完整靜態前端：

- `index.html`：保留原版面，改用標準表單 POST 將資料送回 Apps Script。
- `dear-taiwan-hero.webp`：GitHub Pages 使用的主視覺圖片。
- `Code.gs` 的 `doPost()`：接收 GitHub Pages 表單，沿用原本的驗證、寫入鎖與各場次頁籤邏輯。

發布流程：

1. 先將最新版 `Code.gs` 更新到原 Apps Script 專案。
2. 編輯原有部署，選擇「建立新版本」後重新部署；原 Apps Script 網址不變。
3. 將 `github-pages` 資料夾內的檔案放到新的 GitHub repository 根目錄。
4. 在 repository 的 `Settings` → `Pages`，選擇 `Deploy from a branch`、`main`、`/(root)`。
5. GitHub Pages 網址建立後，先用一筆測試資料確認試算表與場次頁籤皆有收到資料，再更新 Facebook 貼文連結。

GitHub Pages 版本不包含試算表 ID、Drive 圖片 ID或其他後端權限；這些設定仍只存在 Apps Script 的 `Code.gs` 中。

## 上線前檢查

- 用測試資料送出一筆，確認 `基本資料` 與所選活動頁籤都有收到資料。
- 刪除測試資料後，再對外發布網址。


<!-- Pages deployment refresh: 2026-08-06 -->
