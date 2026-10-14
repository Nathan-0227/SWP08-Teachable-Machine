# ☄️ 手勢隕石閃避（SWP08）

用 Teachable Machine 訓練的**圖片分類模型**，透過攝影機辨識身體動作來駕駛太空船、閃避落下的隕石。

🔗 線上遊玩：`https://<你的帳號>.github.io/<repo 名稱>/`

## 遊戲玩法

隕石從上方落下，用身體動作控制底部的太空船左右移動閃避。撞到一次扣一顆心，三顆心用完就結束；存活越久分數越高，隕石也會越來越快。

| 類別 | 動作 | 遊戲效果 |
|---|---|---|
| 左 | 身體往畫面左邊傾（或舉左手） | 太空船左移、背景變藍、顯示「⬅ 向左」 |
| 右 | 身體往畫面右邊傾（或舉右手） | 太空船右移、背景變橘、顯示「向右 ➡」 |
| 無 | 正常坐好 | 太空船停住 |
| 護盾（選用） | 雙手在胸前交叉 | 開啟 2 秒護盾、背景變綠、播放音效 |

- 頁面左側顯示攝影機畫面、目前辨識結果、信心分數，以及每個類別的機率條。
- 信心分數 ≥ 75% 才會觸發動作。
- 撞到隕石時畫面閃紅、震動、播放撞擊音效。
- 沒有攝影機也能用鍵盤 `←` `→` `空白鍵` 試玩。

## 模型訓練（Teachable Machine）

1. 到 https://teachablemachine.withgoogle.com/ → Get Started → **Image Project** → Standard。
2. 建立類別：`左`、`右`、`無`（可再加 `護盾`）。類別名稱需包含這些字，程式才會對應到動作。
3. 每類用 Webcam 錄 150–300 張，過程中稍微移動位置、距離，盡量在同一個光線環境。
4. Train Model → 在右側預覽確認辨識正確。
5. Export Model → Tensorflow.js → **Upload (shareable link)**，複製網址。

## 設定模型

二擇一：

- **用分享連結**：把 `index.html` 裡的 `CONFIG.MODEL_URL` 改成你的網址，例如
  `MODEL_URL: 'https://teachablemachine.withgoogle.com/models/AbCdEf123/'`
- **用本機檔案**：Export 時選 Download，把解壓出的 `model.json`、`metadata.json`、`weights.bin` 放進 repo 的 `my_model/` 資料夾（預設值就是 `./my_model/`）。

## 部署到 GitHub Pages

1. 在 GitHub 建立新的 public repo。
2. 上傳 `index.html`、`README.md`（以及 `my_model/` 資料夾，如果用本機檔案）。
3. Settings → Pages → Source 選 **Deploy from a branch**，Branch 選 `main` / `(root)` → Save。
4. 約 1 分鐘後網址會出現在 Pages 頁面上，打開並允許攝影機權限即可遊玩。
