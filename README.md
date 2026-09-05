# Overture哥のMulti Macro

Sol's RNG 的電腦多開Macro。給需要多開的人用。

天氣改變就會傳到 Discord。直接讀 Roblox 自己寫的 log，所以不是 OCR、也不用一直截圖。

**v0.3.0-beta.2**（Beta 2）。視窗標題是 `Overture哥のMulti Macro v0.3.0-beta.2`。有問題再跟我講就好。

---

## 它會幹嘛

### 天氣
- 天氣開始 / 結束傳到 Discord
- Glitched / Dreamspace / Cyberspace 會自動 `@everyone`
- 多開的每個帳號分開追，訊息會寫是哪個帳號

### 帳戶
- 內建瀏覽器登入，cookie 用 Windows DPAPI 加密（換使用者 / 換電腦就解不開）
- 每個帳號可以有自己的私服連結、自己的 Webhook
- 一鍵開一個或一次開一排
- 可選 multi-instance（實驗），讓同一個 Windows 開多個 Roblox

### 防誤報 / 自動重進
- 可選：確認你在**自己的私服**，不然不要亂報
- 進到別人的服或公開服：自動停，或自動重進自己的私服並按 Start
- 斷線也可以自動重連再按 Start

### 其他
- Anti-AFK（F15 或空白鍵）
- Eden 偵測（獨立開關，被蓋住的視窗也能抓）
- F1 開始偵測，F2 停止
- 可以匯出 / 匯入設定，也可以丟一份不含 cookie 的診斷檔給我

---

## 你需要這些

- Windows 10 / 11（64-bit）
- 已安裝的 Roblox Player
- 一個 Discord Webhook
- Edge WebView2（安裝程式缺的話會自己裝）

設定存在 `%APPDATA%\OvertureMultiMacro\`。  
cookie 等同 Roblox 密碼，不要傳給別人。

---

## 安裝（新裝）

拿到 zip 之後：

1. 開一個**空資料夾**
2. 把 zip 全部解進去
3. 點 **Install.bat**

它會裝到 `%LOCALAPPDATA%\Programs\Overture Multi Macro`，做桌面 / 開始功能表捷徑。  

第一次開是空設定。用儀表板的「匯入設定」把帳號帶過去。  
只有「匯出全部設定（含帳號）」會帶 cookie，傳完請立刻刪掉。

之後要更新：儀表板按「檢查更新」。已經在用 Beta 1 的話，那顆按鈕沒用，請走上面的手動安裝。

---

## 設定

1. 打開 Macro。
2. **帳戶** → 瀏覽器登入，把私服連結填進去。
3. **Webhook和天氣統計** 貼上 Webhook，按一次測試。
4. 要防誤報的話，去 **防誤報** 打開伺服器檢查。
5. 儀表板按開始，或按 **F1**。停用 **F2**。

開始後 Discord 會收到已開始。停的時候會再丟已停止，還有這次的天氣統計。

---

## 多開怎麼開

1. 關掉所有 Roblox。
2. **帳戶** → **啟用 Roblox multi-instance**，等到狀態寫 `ROBLOX_singletonMutex 已取得`。
3. 一個一個啟動。中間 Roblox 跑去更新的話，批次會停，不會幫你刪安裝檔。
4. 嫌太久就按 **停止啟動**。再不行就關 multi-instance，按 **關閉所有 Roblox 用戶端** 重來。

已經開著的 Roblox 可以留著。但要再多開的話，mutex 還是得先拿到。

---

## Eden

跟天氣偵測是分開的，F1 / F2 不管它。

被蓋住的 Roblox 也能抓，靠旁邊那份 `OvertureCaptureHelper.exe`。沒有這檔的話只能用舊的前景擷取，蓋住就看不到。

Eden 有 **測試合成 Eden**：會做一個被蓋住的測試窗，走跟正式一樣的背景擷取。過了就代表這條路是通的。  
也可以播 YouTube Eden 片，按 **測試 YouTube 視窗**。測完記得停，再去開正式多帳號偵測。

只通知，不會幫你收。

---

## 自動重進

在 **防誤報**：

- **自動重進自己的私服並按 Start**：人不在自己私服就重進，然後自己按 Start
- **斷線時自動重連並按 Start**：被踢、timeout、連線中斷、被另一台裝置踢、或 Sol's RNG 遊戲內 Auto Rejoin（視窗可能還在）都會重開再按 Start

兩個都要該帳號有 cookie + 私服連結。  
按「關閉所有 Roblox」不會被當成斷線去重連。

---

## 常見問題

**Q: cookie 會被傳到哪？**  
A: 只會打 Roblox 自己的 API。Webhook 網址跟 cookie 都存在本機，還有 DPAPI。診斷匯出不會帶這些。

**Q: 開始了但 Discord 沒東西？**  
A: 先確認人在 Sol's RNG 裡面。儀表板看有沒有監聽到 Roblox。還沒進遊戲、log 還沒寫出來，看起來都會像沒反應。

**Q: 為什麼進公開服就停了 / 一直重進？**  
A: 你開了伺服器檢查。只想在自己私服報天氣的話，這樣是對的。不想用就關掉。

**Q: Beta 1 按檢查更新沒裝上 Beta 2？**  
A: 那版會關程式然後什麼都不做。請照上面「從 Beta 1 升上來」手動裝一次。標題變成 `v0.3.0-beta.2` 之後，之後的更新就可以按檢查更新。

**Q: 第二個帳號開不起來，跳出更新程式？**  
A: 現在的 Roblox 有時不給同一個 Windows 工作階段多開。先關所有 Roblox，確認 mutex 拿到了再試。Macro 不會幫你刪 Roblox 安裝檔。

**Q: Eden 測不到？**  
A: 看 Eden 頁狀態。沒有 `OvertureCaptureHelper.exe` 的話，被蓋住的窗抓不到。Helper 要跟 exe 放在同一層。

**Q: 換電腦怎麼搬？**  
A: 安全匯出（不含 cookie）最穩，到新電腦再登入一次。含 cookie 的完整匯出只在你自己能控制的電腦之間用，用完刪掉。
