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


### :small_blue_diamond:1.1.3 煙霧偵測（Smoke Detection）

* 系統需能判斷輸入影像/影片中是否存在煙霧
* 輸出為：

  * Smoke / Non-Smoke（二元判斷）

* 系統可依據以下影像特徵判斷煙霧：

  * 灰白色 / 淡灰色區域
  * 低飽和度（Low Saturation）區域
  * 煙霧造成的邊緣模糊或邊緣衰減
  * 連續影像中煙霧緩慢飄動、擴散或形變


### :small_blue_diamond:1.1.4 煙霧定位（Smoke Localization）

* 系統需能在影像中標示煙霧區域
* 輸出形式：

  * Bounding Box（矩形框）
  * 或 Smoke Mask（煙霧遮罩）

* 若煙霧邊界不明顯，允許輸出近似區域，而不要求完全精準輪廓


### :small_blue_diamond:1.1.5 即時影像處理（Real-time Processing）

* 系統需支援連續影像串流（video stream）
* 可即時或近即時顯示偵測結果


### :small_blue_diamond:1.1.6 誤判控制（False Positive Reduction）

* 系統需具備降低誤判能力
* 需能避免誤判以下情境：

  * 黃色 / 橘色光源
  * 夕陽 / 強光
  * 反光物體
  * 白牆 / 灰牆
  * 雲霧 / 天空
  * 強光造成的泛白區域
  * 攝影機模糊或失焦
  * 灰色物體或陰影區域


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
  * 能穩定偵測煙霧
  * 誤判率需可控（不需 SOTA，但需合理）


---

## :large_blue_diamond: 1.3 介面需求（Interface Requirements）

### :small_blue_diamond:1.3.1 輸入介面（Input Interface）

* 支援：

  * USB Camera（OpenCV）

* 輸入格式：

  * RGB Frame（影像幀）


### :small_blue_diamond:1.3.2 輸出介面（Output Interface）

* 即時顯示：

  * HDMI 螢幕顯示（含 bounding box）

* 可選輸出：

  * 影片儲存（Video recording）
  * 圖片輸出（snapshot）

* 偵測結果顯示：

  * Fire / Non-Fire
  * Smoke / Non-Smoke
  * 火焰 bounding box
  * 煙霧 bounding box 或 smoke mask


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


#### 正樣本（Smoke cases）

* 含煙霧影片：

  * 室內煙霧
  * 戶外煙霧
  * 火焰產生之煙霧
  * 無明顯火焰但有煙霧擴散之情境


#### 負樣本（Non-fire / Non-smoke cases）

* 無火焰但易誤判：

  * 黃光燈
  * 日落
  * 車燈
  * 反光物體

* 無煙霧但易誤判：

  * 白牆
  * 灰色背景
  * 雲霧天空
  * 強光泛白
  * 攝影機模糊
  * 低對比場景


### :small_blue_diamond:1.4.2 期待輸入 / 輸出（Expected I/O）

#### Input

* Video stream / 影像序列

#### Output

* Fire / Non-Fire 判斷
* Smoke / Non-Smoke 判斷
* Bounding box（若有火焰）
* Bounding box 或 smoke mask（若有煙霧）
<img width="1655" height="612" alt="image" src="https://github.com/user-attachments/assets/d4d94f85-515f-40c7-b915-60976c3edcbf" />


### :small_blue_diamond:1.4.3 測試方法（Testing Method）

#### 演算法正確性（Algorithm Accuracy）

1. 正樣本:
   * Fire / Non-Fire 判斷   -> Fire ✔️
   * Bounding box           -> 正確框出火焰區域 ✔️
2. 煙霧正樣本:
   * Smoke / Non-Smoke 判斷 -> Smoke ✔️
   * Bounding box / smoke mask -> 正確標示煙霧區域 ✔️
3. 負樣本:
   * Fire / Non-Fire 判斷   -> Non-Fire ✔️
   * Smoke / Non-Smoke 判斷 -> Non-Smoke ✔️
   * Bounding box           -> 無框選 ✔️

#### 硬體效能（Hardware Performanced）

測試條件:
```Text
平台：Raspberry Pi 4
解析度：320×240 / 640×480
輸入來源：USB Camera 
輸出方式：HDMI display / video recording
```

| 效能項目         | 測量方式                         |
| ------------ | ---------------------------- |
| FPS          | 計算1秒內最高能處理幀數                       |
| Latency      | 從 frame input 到 output 顯示的延遲 |
| CPU Usage    | Raspberry Pi CPU 使用率         |
| Memory Usage | RAM 使用量                      |
| Stability    | 連續執行 60 分鐘是否正常            |


---

# 2️⃣ Breakdown
<img width="5444" height="2248" alt="image" src="https://github.com/user-attachments/assets/af7c1eb8-8263-42e6-8113-1bcfc93129e6" />

---

# 3️⃣ 設計
## 架構圖
<img width="5848" height="1048" alt="image" src="https://github.com/user-attachments/assets/5f34b018-f2a1-4083-bf05-5516b1f62b94" />

## What/Why/How
### `cv2.VideoCapture`
>#### What
>使用 OpenCV 從 USB camera 讀取即時影像 frame。
>#### Why
>Raspberry Pi 需要先取得 camera 的每一幀影像，後面的 HSV、形態學、光流、畫框都需要以這些 frame 作為輸入。
>#### How
>用 cv2.VideoCapture(0) 開啟 USB camera，然後在 while 迴圈中用 ret, frame = cap.read() 不斷讀取影像。
### `HSV`
>#### What
>將 BGR 影像轉成 HSV 色彩空間，並根據顏色範圍產生初步 mask。
>#### Why
>如果是火焰偵測，火焰通常具有紅、橘、黃等顏色特徵，用 HSV 比直接用 RGB 更容易設定顏色門檻。HSV 可以把「色相 H」、「飽和度 S」、「亮度 V」分開處理。
>#### How
>使用 cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)，再用 cv2.inRange() 擷取符合火焰顏色範圍的區域。
### `Morphology`
>#### What
>對 HSV 產生的 binary mask 做形態學處理，例如 erosion、dilation、opening、closing。
>#### Why
>HSV mask 通常會有雜訊、小白點、破碎區域。形態學可以去除小雜訊、填補破洞、讓偵測區域更完整。
>#### How
>使用 cv2.morphologyEx() 搭配 kernel，例如 opening 去雜訊，closing 補洞。
### `Farneback`
>#### What
>使用 Farneback dense optical flow 計算前後兩幀之間每個 pixel 的移動向量。
>#### Why
>火焰和煙霧除了顏色特徵之外，還有動態特徵。火焰會閃爍、跳動；煙霧會緩慢飄動、擴散。光流可以幫助判斷某個區域是不是真的有動態變化，而不是單純顏色相似的靜態物體。
>#### How
>將前一幀和當前幀轉成 grayscale，使用 cv2.calcOpticalFlowFarneback() 計算 dense optical flow，再取 magnitude 作為運動強度。
### `mask decision`
>#### What
>將 HSV/morphology mask 和 Farneback motion mask 做融合判斷，決定最終偵測區域。
>#### Why
>單靠 HSV 容易誤判顏色相似物；單靠光流容易受到 camera shake、背景移動、行人移動影響。因此需要融合顏色與動態資訊。
>#### How
>可以使用 AND、OR、加權分數、區域面積門檻、連續幀穩定判斷等方法。
### `Bounding Box Drawing`
>#### What
>根據 final mask 找出連通區域或輪廓，並在原始影像上畫出偵測框。
>#### Why
>只輸出 binary mask 不直觀。畫 bounding box 可以讓展示者和觀眾直接看到系統判斷哪裡有火焰或煙霧。
>#### How
>使用 cv2.findContours() 找輪廓，再用 cv2.boundingRect() 取得矩形座標，最後用 cv2.rectangle() 畫框。
## `cv2.imshow`
>### What
>將處理後的影像顯示出來。
>### Why
>需要讓使用者即時看到 camera 畫面、mask 結果、bounding box 偵測結果。
>### How
>使用 cv2.imshow() 顯示 frame，Raspberry Pi 透過 HDMI 接到 monitor，畫面就會出現在螢幕上。

---

# Result


https://github.com/user-attachments/assets/6c10a5b0-fd9b-4661-9dca-7cb5035030c1


