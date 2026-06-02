# MiDAS Hole A 每日報告

DAS 光纖 Hole A 井下每日 RMS 偵測報告，自動產生並發佈於 GitHub Pages。

## 🌐 網站入口

**總入口（從這裡點日期）：**
https://charliebai605.github.io/midas-daily/

進去後依 `年 → 年-月 → 日` 分層點選。

**直接到某一天（最快）：**

```
https://charliebai605.github.io/midas-daily/YYYY/MM/YYYYMMDD/
```

例如 2026-05-30 → https://charliebai605.github.io/midas-daily/2026/05/20260530/

> 建議把總入口加書籤；知道日期時可直接套上面的網址規則跳轉，不必逐層點。
> 新報告 push 後 GitHub Pages 約需 1 分鐘重建，剛更新可重整一次。

## 📊 每日報告內容

每天的頁面包含：

- **互動 RMS 時序圖**（Plotly）：y 軸為 log amplitude（log RMS）。
  點擊紅色 **up** 事件（或洋紅 **noise_large**）即顯示該事件的 waterfall plot。
- **每日圖**：STA/LTA 4-panel、深度 RMS overlay、RMS histogram。
- **Peaks 清單**：`peaks.txt`，4 欄 `ID / 時間(UTC+8) / RMS / 分類`。
- **Waterfall**：每個 up / noise_large 事件，ch 1208–1377（Hole A 全段，深度 0–695 m），
  事件前 3 s 到後 5 s，bandpass 1–20 Hz。

## 🏷️ 事件分類（f-k beamforming）

| 標籤 | 顏色 | 說明 |
| :--- | :--- | :--- |
| `up` | 紅 | 上行波（地震 P 波由下方入射，深通道領先） |
| `down` | 橘 | 下行波（地表源，淺通道領先） |
| `noise` | 綠 | k≈0，視速度極高 → 噪訊 |
| `noise_large` | 洋紅 | f-k 判為 noise 但 RMS > 8 → 多為近垂直入射的大地震（如 5/30 ev 400 M4.2） |

## 📂 資料夾結構

```
midas-daily/
├── index.html                       ← 總入口（年/月/日分組）
└── YYYY/MM/YYYYMMDD/
    ├── index.html                   ← 當日互動報告
    ├── rms.png  rms_hist.png  depth_rms_overlay.png
    ├── peaks.txt
    └── waterfalls/ev_NNN.png
```

報告由伺服器端 `daily_blog.py` + `midas_daily_report.py` 自動產生並 push。
