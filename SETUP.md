# 寶島集章護照：架設步驟

這個資料夾有兩個檔案：

- `index.html`：遊戲本體
- `firestore.rules`：Firebase 資料庫的安全規則

整個架設大約 15 分鐘，全部免費。

---

## A. 設定 Firebase（資料庫）

1. 到 https://console.firebase.google.com ，用 Google 帳號登入，按「新增專案」。
   名稱隨意，例如 `taiwan-passport`。Google Analytics 可以關掉。
2. **開啟匿名登入**
   左側選單「建構 Build」→「Authentication」→「開始使用」→「Sign-in method」→ 選「匿名 Anonymous」→ 啟用 → 儲存。
3. **建立資料庫**
   「建構 Build」→「Firestore Database」→「建立資料庫」
   - 位置：選 `asia-east1 (Taiwan)`
   - 模式：選「正式版模式 production mode」
4. **貼上安全規則**
   在 Firestore 頁面上方點「規則 Rules」，把 `firestore.rules` 的內容整份貼上，取代原本的內容，按「發布 Publish」。
5. **拿到設定碼**
   左上角齒輪 ⚙ →「專案設定」→ 往下找「你的應用程式」→ 點網頁圖示 `</>`。
   暱稱隨意，**不用**勾 Firebase Hosting，按「註冊應用程式」。
   畫面會出現一段 `const firebaseConfig = { apiKey: "...", ... };`，把大括號裡的內容複製下來。
6. 用文字編輯器打開 `index.html`（電腦上的「記事本」或「文字編輯」都可以）。
   找到最上面那段 `firebaseConfig`，把 `PASTE...` 那幾行換成你剛剛複製的內容，存檔。

> 這段設定碼放在公開網頁上是正常的，它不是密碼。真正保護資料的是第 4 步的規則。

## B. 放上 GitHub Pages（網址）

1. 到 https://github.com 註冊或登入。
2. 右上角「+」→「New repository」
   - Repository name：`taiwan-passport`
   - 選 **Public**（免費帳號的 GitHub Pages 需要公開）
   - 按「Create repository」
3. 在新 repo 的頁面點「uploading an existing file」，把**已經貼好設定的** `index.html` 拖進去，按「Commit changes」。
4. 進 repo 的「Settings」→ 左側「Pages」
   - Source：`Deploy from a branch`
   - Branch：`main`，資料夾 `/ (root)` → Save
5. 等 1–2 分鐘，網址會出現在同一頁：
   `https://<你的GitHub帳號>.github.io/taiwan-passport/`
6. 回到 Firebase：「Authentication」→「設定 Settings」→「授權網域 Authorized domains」→「新增網域」，填 `<你的GitHub帳號>.github.io`。

## C. 開始玩

1. 用手機打開上面的網址，按「建立我們的護照」。
2. 你會被帶到「出題」分頁，上面有兩個連結：
   - **旅人連結**：傳給對方
   - **出題者連結**：你自己留著（加入書籤）
3. 把 6 個範例任務改成你們自己的地點和秘密訊息。
   座標可以在 Google Maps 長按地點後複製。
4. 對方打開旅人連結後，在 Safari 按「分享 → 加入主畫面」（Android Chrome 是「⋮ → 加到主畫面」），用起來就像 App。

## 之後要修改

在 GitHub 的 repo 頁面點 `index.html` → 右上角鉛筆圖示編輯，或重新上傳一份覆蓋。存檔後 1–2 分鐘網站就會更新，資料不會不見。

## 你需要知道的

- **誰看得到**：只有拿到連結的人。每本護照的代碼是 24 位隨機字元，猜不到。
- **秘密訊息**：一般人在打卡前看不到。不過懂網頁程式的人可以從瀏覽器工具裡翻出來，這是個情侶遊戲的信任機制，不是保險箱。
- **照片**：會自動壓縮到大約 100–300 KB 再存進資料庫。免費額度有 1 GB，放幾千張都夠。
- **GPS**：手機會詢問是否允許使用位置，要按允許。如果 GPS 不準，旅人可以按「我確定我在這裡」，出題者這邊會標示「沒有用 GPS 驗證」。
