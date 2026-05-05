# Fire Detection System — Requirement Specification

---

# 1️⃣ 需求（Requirements）

---

## :large_blue_diamond: 1.1 功能需求（Functional Requirements）

### :small_blue_diamond:1.1.1 火焰偵測（Fire Detection）

* 系統需能判斷輸入影像/影片中是否存在火焰
* 輸出為：

  * Fire / Non-Fire（二元判斷）


### :small_blue_diamond:1.1.2 火焰定位（Fire Localization）

* 系統需能在影像中標示火焰區域
* 輸出形式：

  * Bounding Box（矩形框）


### :small_blue_diamond:1.1.3 即時影像處理（Real-time Processing）

* 系統需支援連續影像串流（video stream）
* 可即時或近即時顯示偵測結果


### :small_blue_diamond:1.1.4 誤判控制（False Positive Reduction）

* 系統需具備降低誤判能力
* 需能避免誤判以下情境：

  * 黃色 / 橘色光源
  * 夕陽 / 強光
  * 反光物體


---

## :large_blue_diamond: 1.2 效能需求（Performance Requirements）

### :small_blue_diamond:1.2.1 即時性（Real-time Constraint）

* 需於嵌入式平台上達到：

  * ≥ 10–20 FPS@640x480（目標值）
  * 或具備可接受之 near real-time 表現

### :small_blue_diamond:1.2.2 計算資源限制（Resource Constraint）

* 可運行於 Raspberry Pi 4
* 僅使用 CPU（不依賴 GPU）


### :small_blue_diamond:1.2.3 系統穩定性（Stability）

* 在連續影像輸入下穩定運行
* 不產生頻繁錯誤或崩潰


### :small_blue_diamond:1.2.4 準確性（Accuracy）

* 在純影像條件下：

  * 能穩定偵測火焰
  * 誤判率需可控（不需 SOTA，但需合理）


---

## :large_blue_diamond: 1.3 介面需求（Interface Requirements）

### :small_blue_diamond:1.3.1 輸入介面（Input Interface）

* 支援：

  * USB Camera（V4L2 / OpenCV）
  * CSI Camera（libcamera / Picamera2）

* 輸入格式：

  * RGB Frame（影像幀）


### :small_blue_diamond:1.3.2 輸出介面（Output Interface）

* 即時顯示：

  * HDMI 螢幕顯示（含 bounding box）

* 可選輸出：

  * 影片儲存（Video recording）
  * 圖片輸出（snapshot）


### :small_blue_diamond:1.3.3 系統運行環境（System Environment）

* 嵌入式平台：

  * Raspberry Pi 4 或同級以下設備

* 軟體環境：

  * Python + OpenCV


---

## :large_blue_diamond: 1.4 驗證（Verification）


### :small_blue_diamond:1.4.1 測試資料（Test Data）

#### 正樣本（Fire cases）

* 含火焰影片：

  * 室內火焰（蠟燭、瓦斯爐）
  * 戶外火焰（營火、燃燒物）


#### 負樣本（Non-fire cases）

* 無火焰但易誤判：

  * 黃光燈
  * 日落
  * 車燈
  * 反光物體


### :small_blue_diamond:1.4.2 期待輸入 / 輸出（Expected I/O）

#### Input

* Video stream / 影像序列

#### Output

* Fire / Non-Fire 判斷
* Bounding box（若有火焰）
<img width="1655" height="612" alt="image" src="https://github.com/user-attachments/assets/d4d94f85-515f-40c7-b915-60976c3edcbf" />


### :small_blue_diamond:1.4.3 測試方法（Testing Method）

#### 演算法正確性（Algorithm Accuracy）

1. 正樣本:
   * Fire / Non-Fire 判斷   -> Fire ✔️
   * Bounding box           -> 正確框出火焰區域 ✔️
3. 負樣本:
   * Fire / Non-Fire 判斷   -> Non-Fire ✔️
   * Bounding box           -> 無框選 ✔️

#### 硬體效能（Hardware Performanced）

測試條件:
```Text
平台：Raspberry Pi 4
解析度：320×240 / 640×480
輸入來源：USB Camera 或 CSI Camera
輸出方式：HDMI display / video recording
```

| 效能項目         | 測量方式                         |
| ------------ | ---------------------------- |
| FPS          | 計算1秒內最高能處理幀數                       |
| Latency      | 從 frame input 到 output 顯示的延遲 |
| CPU Usage    | Raspberry Pi CPU 使用率         |
| Memory Usage | RAM 使用量                      |
| Stability    | 連續執行 10–30 分鐘是否正常            |


---

# 2️⃣ Breakdown
<img width="4404" height="1764" alt="image" src="https://github.com/user-attachments/assets/b02d1452-90e1-4b09-810a-919105eb6bea" />

---

# 3️⃣ 設計（略過）

---


