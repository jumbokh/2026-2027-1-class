建議課程名稱可以定為：

**《AI 智能體與物聯網實踐》**
48 課時，建議採用 **24 課時 AI 智能體 + 24 課時感測器／物聯網整合實作**。

核心定位不是單純教 ChatGPT，而是讓學生最後能做出一個：

> **可以讀取感測器資料、判斷環境狀態、回答問題、觸發控制動作的 AI 智能體系統。**

---

## 一、建議採用的系統架構

我建議用這一套：

### 1. AI 智能體平台：Dify 為主

**推薦主系統：Dify + 國內大模型 API**

原因是 Dify 適合教學，能做：

* 智能體 Agent
* 工作流 Workflow / Chatflow
* 知識庫 RAG
* 工具調用 Tool Calling
* HTTP API 串接外部系統
* 可視化拖拉式設計

Dify 官方文件說明，它是用於建立 agentic workflows 的開源平台，可以視覺化連接模型、工具與資料來源；其 Agent 節點可讓大模型自主判斷何時使用工具來完成任務。([Dify 文檔][1])

### 2. 大模型選擇：優先用中國可用模型

建議順序：

| 類型       | 建議                                   |
| -------- | ------------------------------------ |
| 教學穩定方案   | 阿里雲百鍊 / 通義千問 Qwen                    |
| 程式與工具調用  | DeepSeek API                         |
| 校內私有部署進階 | Qwen / DeepSeek 開源模型 + Ollama 或 vLLM |
| 無程式快速展示  | 扣子 Coze、百度千帆 AppBuilder              |

阿里雲百鍊官方說明其為一站式大模型開發與應用平台，支援通義模型、第三方模型、OpenAI 相容 API，也能建立智能體與知識庫問答應用。([阿里云帮助中心][2]) DeepSeek 官方文件也明確支援 Tool Calls，可讓模型調用外部工具，例如查詢天氣、資料庫或物聯網 API。([DeepSeek API Docs][3])

### 3. 物聯網平台：ESP32 + MQTT + EMQX + Node-RED

物聯網端建議用：

| 功能          | 系統                       |
| ----------- | ------------------------ |
| 感測器開發板      | ESP32 / ESP32-S3         |
| 開發工具        | Arduino IDE 或 PlatformIO |
| 通訊協議        | MQTT                     |
| MQTT Broker | EMQX                     |
| 視覺化流程       | Node-RED                 |
| API 串接      | Python FastAPI           |
| AI 智能體串接    | Dify 自訂工具 / HTTP Request |

ESP32 官方文件建議可使用 Arduino-ESP32 支援套件，且特別提醒中國使用者若 GitHub 下載速度不穩，可使用 Jihulab 鏡像來源。([Espressif Systems][4]) Node-RED 是適合事件驅動應用的低程式碼工具，可用瀏覽器拖拉流程，連接硬體、API 與線上服務。([Node-RED][5]) EMQX 則是完整支援 MQTT 3.x / 5.0 的物聯網訊息平台，適合用於裝置資料上傳與即時訊息傳遞。([EMQX 文件說明][6])

---

## 二、我建議的最終作品方向

最適合這門課的期末作品是：

## **AI 物聯網環境監測智能體**

例如：

**「智慧教室環境助理」**
或更貼近您的研究方向：

**「文物保存環境監測 AI 智能體」**

功能可以設計為：

1. ESP32 讀取溫度、濕度、光照、空氣品質。
2. 資料透過 MQTT 傳到 EMQX。
3. Node-RED 顯示即時儀表板。
4. Python API 提供目前感測器資料。
5. Dify 智能體透過工具調用 API。
6. 學生可以問：

> 目前展示櫃環境是否適合文物保存？
> 濕度是否過高？
> 是否需要開啟警報？
> 請產生今日環境巡檢報告。

這樣 AI 智能體就不是純聊天，而是真的能「讀資料、判斷、建議、控制」。

---

# 三、48 課時正式教學大綱

建議採用 **12 次課，每次 4 課時**。

---

## 第一部分：AI 智能體實踐，24 課時

| 次數    | 課時 | 主題              | 實作內容                                                         |
| ----- | -: | --------------- | ------------------------------------------------------------ |
| 第 1 次 |  4 | AI 智能體概論與系統環境   | 認識 Agent、RAG、Workflow、Tool Calling；建立 Dify 或百鍊帳號；完成第一個 AI 助手 |
| 第 2 次 |  4 | 提示詞工程與角色設計      | 設計「教學助理」「設備維護助理」「文物保存助理」提示詞                                  |
| 第 3 次 |  4 | 知識庫 RAG 應用      | 上傳課程文件、感測器說明書、文物保存規範，建立知識庫問答                                 |
| 第 4 次 |  4 | 工作流 Workflow 設計 | 設計條件判斷流程：輸入問題 → 判斷類型 → 查知識庫 → 生成答案                           |
| 第 5 次 |  4 | 工具調用與 API 串接    | 建立自訂工具，讓 AI 查詢外部 API，例如天氣、設備狀態、感測器資料                         |
| 第 6 次 |  4 | AI 智能體小專題       | 完成一個可查詢資料、可根據條件回答的智能體原型                                      |

---

## 第二部分：感測器與物聯網實作，24 課時

| 次數     | 課時 | 主題                 | 實作內容                                          |
| ------ | -: | ------------------ | --------------------------------------------- |
| 第 7 次  |  4 | ESP32 基礎與感測器讀取     | 安裝 Arduino IDE；讀取 DHT22/SHT31 溫濕度、光照感測器資料     |
| 第 8 次  |  4 | Wi-Fi 與 MQTT 通訊    | ESP32 連接 Wi-Fi；將感測器資料發布到 MQTT Topic           |
| 第 9 次  |  4 | EMQX 與 MQTT 訊息管理   | 架設或使用 EMQX；理解 publish/subscribe；使用 MQTTX 測試訊息 |
| 第 10 次 |  4 | Node-RED 視覺化儀表板    | 建立 Dashboard，顯示溫度、濕度、光照、警報狀態                  |
| 第 11 次 |  4 | Python API 與 AI 串接 | 使用 FastAPI 將感測器資料包裝成 API；Dify 調用 API 讀取即時資料   |
| 第 12 次 |  4 | 期末整合專題             | 完成「AI + IoT 智能體」展示：查詢、判斷、報告、警示或控制             |

---

# 四、建議硬體清單

每 2–3 位學生一組即可。

## 基礎套件

| 設備            |  數量 | 用途    |
| ------------- | --: | ----- |
| ESP32 開發板     |   1 | 主控板   |
| USB 線         |   1 | 燒錄與供電 |
| 麵包板           |   1 | 電路連接  |
| 杜邦線           |  若干 | 接線    |
| DHT22 或 SHT31 |   1 | 溫濕度   |
| BH1750        |   1 | 光照    |
| LED           | 2–3 | 狀態顯示  |
| 蜂鳴器           |   1 | 警報    |
| OLED 顯示屏      |   1 | 本地顯示  |

## 進階可選

| 設備        | 用途              |
| --------- | --------------- |
| MQ-135    | 空氣品質            |
| PIR 人體感測器 | 教室有人 / 無人偵測     |
| 繼電器模組     | 控制風扇、燈光         |
| ESP32-CAM | 圖像擷取，進階 AI 視覺應用 |

---

# 五、建議軟體環境

## 教師端伺服器

建議準備一台教師端主機或雲端伺服器：

| 項目   | 建議                              |
| ---- | ------------------------------- |
| 作業系統 | Ubuntu 22.04 / 24.04            |
| 部署方式 | Docker Compose                  |
| 服務   | Dify、EMQX、Node-RED、FastAPI      |
| 模型   | 阿里雲百鍊 / DeepSeek API / Qwen API |
| 連線方式 | 校內 LAN 或雲端網址                    |

## 學生端電腦

| 軟體              | 用途                              |
| --------------- | ------------------------------- |
| Arduino IDE 2.x | ESP32 程式開發                      |
| VS Code         | Python / API 開發                 |
| Python 3.10+    | FastAPI、資料處理                    |
| MQTTX           | MQTT 測試                         |
| 瀏覽器             | 使用 Dify、Node-RED、EMQX Dashboard |

---

# 六、課程考核方式建議

| 項目    |  比例 | 說明                |
| ----- | --: | ----------------- |
| 平時實作  | 30% | 每次課完成指定任務         |
| 小作業   | 20% | AI 工作流、MQTT、感測器讀取 |
| 期末專題  | 40% | AI + IoT 整合系統     |
| 報告與展示 | 10% | 系統架構、功能展示、問題分析    |

---

# 七、期末專題要求

學生最終需要完成：

## **AI 物聯網智能體系統**

最低要求：

1. ESP32 能讀取至少 2 種感測器資料。
2. 感測器資料能透過 MQTT 上傳。
3. Node-RED 能顯示即時資料。
4. AI 智能體能查詢目前感測器狀態。
5. AI 能根據規則給出判斷，例如「濕度過高」「光照過強」。
6. 能產生一份簡短巡檢報告。

進階要求：

1. AI 可控制 LED、蜂鳴器或繼電器。
2. 可加入知識庫，例如文物保存標準、教室環境標準。
3. 可生成每日報告。
4. 可加入異常提醒。
5. 可做成簡單 Web App。

---

# 八、推薦課程名稱與定位

我建議不要只叫 **AI 智能體實踐**，因為您想保留一半物聯網內容，名稱可以改成：

## 方案一

**AI 智能體與物聯網實踐**

## 方案二

**AI Agent 與智慧感測應用實踐**

## 方案三

**生成式 AI 智能體與智慧物聯網應用**

## 方案四

**AIoT 智能體系統開發實踐**

如果是正式課程，我最推薦：

> **《AI 智能體與物聯網實踐》**

名稱清楚，學生也容易理解，內容可以自然涵蓋 AI Agent、感測器、MQTT、API、智慧控制與專題製作。

---

# 九、整體建議

這門 48 課時課程最好不要把 AI 智能體和物聯網分開教，而是採用：

> **前半段學 AI 智能體，後半段學物聯網，最後兩週整合成 AIoT 專題。**

最終學生完成的不是單一聊天機器人，而是：

> **一個能理解問題、查詢知識庫、讀取感測器、判斷異常、產生報告，甚至控制設備的 AI 智能體。**

這樣課程會比一般「AI 工具應用課」更有特色，也更適合大數據、人工智慧、物聯網、智慧管理類專業。

[1]: https://docs.dify.ai/en/guides/tools/mcp?utm_source=chatgpt.com "Introduction - Dify Docs"
[2]: https://help.aliyun.com/zh/model-studio/what-is-model-studio?utm_source=chatgpt.com "阿里云-大模型服务平台百炼(Model Studio)"
[3]: https://api-docs.deepseek.com/zh-cn/guides/tool_calls?utm_source=chatgpt.com "Tool Calls"
[4]: https://docs.espressif.com/projects/arduino-esp32/en/latest/installing.html?utm_source=chatgpt.com "Installing - - — Arduino ESP32 latest documentation"
[5]: https://nodered.org/?utm_source=chatgpt.com "Low-code programming for event-driven applications : Node-RED"
[6]: https://docs.emqx.com/en/emqx/latest/configuration/mqtt.html?utm_source=chatgpt.com "MQTT Configuration | EMQX Enterprise Docs"
