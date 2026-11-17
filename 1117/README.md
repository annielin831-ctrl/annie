# 故宮南院・拾境｜3D文化探索網站

以 React + Vite + Three.js (React Three Fiber) 建立的跨裝置 3D 網站起始專案。

## 已包含
- 3D 湖泊、島嶼、橋梁、可操作角色與跟隨鏡頭
- 桌機 WASD / 方向鍵移動；手機觸控方向鍵
- 五個文化主題島嶼與 NPC 對話視窗
- 會員登入介面：未設定 Supabase 時使用本機展示模式
- 文創商品清單、購物車與本機購物車保存
- 響應式版面，可在 iPhone / iPad / PC 瀏覽器開啟

## 本機啟動
```bash
npm install
npm run dev
```
打開終端機顯示的網址。測試正式版：
```bash
npm run build
npm run preview
```

## GitHub 與 Vercel 部署
1. 在 GitHub 建立新 repository。
2. 將本資料夾內所有檔案上傳至 repository 根目錄。
3. 登入 Vercel，選擇 Add New → Project，匯入該 GitHub repository。
4. Framework Preset 選 Vite；Build Command `npm run build`；Output Directory `dist`。
5. 若要啟用正式會員系統，在 Vercel Project → Settings → Environment Variables 設定：
   - `VITE_SUPABASE_URL`
   - `VITE_SUPABASE_ANON_KEY`
6. 重新部署。

## Supabase 會員設定
建立 Supabase 專案，從 Project Settings → API 複製 Project URL 與 anon/public key，填入 `.env`（本機）及 Vercel Environment Variables。
註冊、登入、登出會使用 Supabase Auth。若未設定，會以 localStorage 模擬展示帳號，**不適合正式上線存放真實會員資料**。

## 後續正式上線前要補強
- 購物付款：串接合法金流服務與伺服器端訂單驗證；目前購物車是展示功能，不會真的扣款。
- 多人即時角色：已加入 Supabase Realtime Presence + Broadcast 原型；設定 Supabase 後，同一個公開頻道中的訪客可看到彼此的動漫風角色位置。正式上線前請限制頻道存取、加入暱稱審核、更新頻率限制與斷線清理。文字聊天、好友及私訊仍需另外開發。
- 3D 美術：目前是可操作的低多邊形原型，正式版可替換成依授權取得的故宮南院 3D 模型、材質與音效。
- 文化內容：正式公開前，請由館方資料或可靠來源審閱文字；本專案故事為原創概念，不代表官方展覽。

## 參考
故宮南院官方介紹：https://south.npm.gov.tw/AboutUs/Info.htm
園區平面圖：https://south.npm.gov.tw/Visit/ParkIntroduction/Plan.htm


## 多人角色同步
設定 Supabase URL 與 anon key 後，網站會加入 `npm-south-world` Realtime channel，使用 Presence 顯示在線旅人，使用 Broadcast 同步角色位置。此為多人同步原型；請在 Supabase 專案啟用 Realtime，並依正式環境需求設定頻道權限與濫用防護。未設定 Supabase 時，仍可單人探索與使用 NPC 對話。
