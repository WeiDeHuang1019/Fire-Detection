# Fire-Detection 火焰偵測期末專案

## :one:專案概述
### 1.目標（Objective）

本專案旨在開發一套**基於純影像資訊（vision-only）之火焰偵測系統**，透過傳統影像處理方法，在不依賴深度學習模型與其他感測器的前提下，實現對影片中火焰的自動辨識與區域標記功能。

系統將運行於低功耗嵌入式平台（如 Raspberry Pi 4 或同等級設備），以達成低成本、可部署之火焰監測解決方案。

---

### 2.限制（Constrain）

本研究明確聚焦於以下範疇：

#### (2.1)單一資料來源（Single Modality）

* 僅使用 **RGB 影像或影片**
* 不使用：

  * 溫度感測器（thermal sensor）
  * 紅外線（IR）
  * 煙霧感測器
  * 多模態融合（multi-modal fusion）

> 系統僅依賴「畫面本身」進行判斷

---

#### (2.2) 非深度學習方法（Non-Deep Learning）

* 不使用：

  * CNN / Transformer
  * 預訓練模型
* 採用：

  * 傳統影像處理與規則式判斷

* 降低計算成本
* 提升可解釋性
* 符合嵌入式系統需求

---

#### (2.3) 邊緣裝置部署（Edge Deployment）

系統需具備以下特性：

* 可於 Raspberry Pi 4 即時運行
* 不依賴雲端運算
* 可獨立完成火焰判斷與標記

---

### 3.功能（Functional Objectives）

系統需具備以下基本能力：

#### (3.1) 火焰存在判斷

* 判斷畫面中是否存在火焰

---

#### (3.2) 火焰區域定位

* 將火焰區域以 bounding box 方式標示於影像上

---

#### (3.3) 即時處理能力

* 可處理連續影片流（video stream）
* 達到基本即時反應（real-time or near real-time）

---

#### (3.4) 誤判控制能力

在僅使用影像資訊的限制下，盡可能降低以下誤判：

* 燈光（黃色 / 橘色光源）
* 夕陽或強光
* 反光物體



---

### 4.預期成果（Expected Outcomes）

本專案預期完成：

* 一套可於嵌入式平台執行的火焰偵測系統
* 可對影片中的火焰進行：

  * 偵測（detection）
  * 定位（localization）
* 在純影像條件下達到合理準確度與穩定性

:arrow_down_small:預期結果示意圖(非實際成果)
<img width="1222" height="569" alt="image" src="https://github.com/user-attachments/assets/1e4a99ad-3e76-4861-806d-248d36f741db" />


---
## :two:專案分析
### 1.Breakdown
<img width="4404" height="1764" alt="image" src="https://github.com/user-attachments/assets/b02d1452-90e1-4b09-810a-919105eb6bea" />

該階層圖拆解了 *Video in/process/out* 的組成，其中也提及了可能使用到的硬體元件，以及主要的coding任務。
