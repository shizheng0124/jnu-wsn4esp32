# jnu-wsn4esp32
面向传感网原理及应用这门课程，我们基于ESP32开发一套“项目驱动、逐层递进”的教学方案。每一章对应一个实践项目，项目既紧扣章节理论，又充分利用ESP32的丰富特性（Wi-Fi、蓝牙、低功耗、外设接口等），让学生在“做中学”中深刻理解WSN的核心原理。


针对你提出的基于ESP32的课程设计需求，我为你规划了一套**“项目驱动、逐层递进”**的教学方案。每一章对应一个实践项目，项目既紧扣章节理论，又充分利用ESP32的丰富特性（Wi-Fi、蓝牙、低功耗、外设接口等），让学生在“做中学”中深刻理解WSN的核心原理。

以下是各章节的项目设计：

---

### **第1章 绪论：WSN初探**
- **项目名称**：我的第一个无线传感器节点
- **项目目标**：直观认识WSN节点构成，理解传感器、微控制器、无线的概念。
- **理论知识点**：WSN体系结构、节点组成、典型应用。
- **ESP32实践**：
  - 硬件：ESP32开发板、DHT11温湿度传感器（或板载霍尔传感器）。
  - 任务：编写程序读取传感器数据，通过串口打印；观察数据变化，理解“感知”过程。
  - 扩展：尝试用手机蓝牙连接ESP32（使用Serial Bluetooth Terminal App）查看数据，初步接触无线传输。
- **预期成果**：学生能独立搭建硬件并编写基础采集程序，对WSN产生感性认识。

---

### **第2章 WSN开发环境**
- **项目名称**：ESP32开发环境搭建与基础实验
- **项目目标**：掌握ESP32的开发流程，熟悉常用外设操作。
- **理论知识点**：嵌入式开发环境、编程语言、调试方法。
- **ESP32实践**：
  - 任务1：安装Arduino IDE或ESP-IDF，配置ESP32开发板支持包，编写“Hello World”（串口输出）。
  - 任务2：控制板载LED闪烁，学习GPIO输出。
  - 任务3：读取板载霍尔传感器（或外接按键），学习GPIO输入和中断。
- **预期成果**：学生能够独立完成开发环境配置，掌握基本的输入输出编程，为后续项目打下基础。

---

### **第3章 WSN拓扑结构、覆盖技术**
- **项目名称**：多节点组网与拓扑结构实验
- **项目目标**：理解星型、树型等拓扑结构，观察覆盖范围对通信的影响。
- **理论知识点**：网络拓扑、覆盖控制、连通性。
- **ESP32实践**：
  - 硬件：3块ESP32开发板。
  - 任务：配置一个ESP32为AP（协调器），另外两个为STA（终端节点）。终端节点定时发送温湿度数据给协调器，协调器通过串口显示。学生通过改变节点之间的距离或增加障碍物，观察RSSI变化和数据丢包情况，理解“覆盖”和“连通性”的概念。
  - 扩展：尝试组建树型拓扑（一个节点作为中继，转发另一个节点的数据），简单实现多跳。
- **预期成果**：学生能手动配置ESP32的Wi-Fi模式，理解不同拓扑的优缺点，并记录覆盖与信号强度的关系。

---

### **第4章 WSN通信与组网技术**
- **项目名称**：基于ESP-NOW的轻量级通信与多跳转发
- **项目目标**：学习WSN中的MAC层和网络层基本思想，体验无连接通信与数据转发。
- **理论知识点**：MAC协议、路由协议（如泛洪、按需路由）、CSMA/CA。
- **ESP32实践**：
  - 硬件：3~4块ESP32开发板。
  - 任务：使用**ESP-NOW**协议（一种无AP的轻量级通信协议）实现节点间直接通信。设计一个简单多跳实验：节点A发送数据给节点B，节点B自动转发给节点C，节点C串口输出。学生可以观察数据如何一跳一跳传递，并思考路由表如何维护。
  - 扩展：模拟泛洪——节点收到数据后广播给所有邻居，观察重复包问题，引出路由优化需求。
- **预期成果**：学生掌握ESP-NOW的使用，理解多跳通信的基本原理，并能对比单跳与多跳的差异。

---

### **第5章 WSN支撑技术**
- **项目名称**：节点定位、数据融合与低功耗管理
- **项目目标**：综合运用RSSI测距、数据聚合、睡眠唤醒等支撑技术。
- **理论知识点**：节点定位（基于RSSI）、数据融合、能量管理。
- **ESP32实践**：
  - 定位实验：放置3个已知位置的参考节点（ESP32），未知节点接收它们的RSSI，通过简单算法（如三边测量法）估算自身位置。学生需记录多组数据，分析定位精度与RSSI波动的关系。
  - 数据融合实验：多个传感器节点采集温度，汇聚节点收到后计算平均值并只上传均值，模拟数据融合减少通信量。
  - 低功耗实验：配置ESP32进入Deep Sleep模式，定时唤醒采集数据，测量工作电流，计算电池续航，理解能量管理的重要性。
- **预期成果**：学生能够实现简单的定位算法，理解数据融合的意义，并掌握低功耗编程。

---

### **第6章 WSN协议技术标准**
- **项目名称**：无线通信标准对比实验：Wi-Fi vs. BLE
- **项目目标**：对比不同无线标准在WSN中的适用性，理解协议设计的权衡。
- **理论知识点**：IEEE 802.11（Wi-Fi）、IEEE 802.15.1（蓝牙）、IEEE 802.15.4（ZigBee）等标准的特点（功耗、速率、距离、网络规模）。
- **ESP32实践**：
  - 硬件：ESP32开发板（支持Wi-Fi和BLE）、电流测量工具（如万用表）。
  - 任务1：分别实现Wi-Fi Station模式和BLE iBeacon广播，测量两种模式下的发射功耗和数据传输速率。
  - 任务2：测试Wi-Fi和BLE的有效通信距离（在无障碍环境下逐渐拉远距离，记录断连点）。
  - 任务3：组网对比——Wi-Fi可连接多个STA，BLE可组建piconet或mesh（使用ESP-BLE-MESH库），观察网络规模限制。
- **预期成果**：学生通过实测数据，能对比分析Wi-Fi和BLE在WSN中的适用场景，加深对标准设计的理解。

---

### **第7章 WSN接入技术**
- **项目名称**：WSN与云平台无缝接入
- **项目目标**：掌握WSN通过网关接入互联网的典型方法，学习物联网云平台的使用。
- **理论知识点**：网关设计、互联网协议（TCP/IP）、MQTT/CoAP、云平台架构。
- **ESP32实践**：
  - 硬件：ESP32开发板（作为网关）、DHT11传感器（可选多个节点）。
  - 任务：ESP32连接家庭Wi-Fi，通过**MQTT协议**将传感器数据发布到公共MQTT Broker（如Mosquitto）或云平台（如阿里云IoT、腾讯云IoT Explorer、ThingsBoard）。学生需在云平台上创建产品和设备，订阅数据并查看实时曲线。
  - 扩展：实现双向控制——从云平台下发命令，ESP32接收后控制LED开关。
- **预期成果**：学生能独立完成MQTT通信，理解物联网“云-管-边-端”架构，掌握云平台基本操作。

---

### **第9章 WSN与物联网（综合设计）**
- **项目名称**：智能环境监测物联网系统综合实践
- **项目目标**：整合全书知识，设计并实现一个具有实际应用价值的完整WSN系统。
- **理论知识点**：系统设计方法、异构网络融合、端-边-云协同、应用层协议。
- **ESP32实践**：
  - 场景：模拟智能农业/智能家居环境监测系统。
  - 系统组成：
    - **终端节点**（2~3个ESP32+传感器）：采集温湿度、光照、土壤湿度等，通过**ESP-NOW**或**BLE Mesh**将数据发送给网关。
    - **网关节点**（1个ESP32+Wi-Fi）：接收来自终端的数据，进行简单融合（如过滤异常值），然后通过**MQTT**上传至云平台。
    - **云平台**：存储数据并提供可视化面板，同时支持反向控制（如远程启动风扇）。
    - **用户端**：手机App或Web页面查看数据和控制。
  - 任务：学生分组完成系统设计、硬件搭建、代码编写、调试，最后进行演示和答辩。
- **预期成果**：学生能够综合运用所学，完成一个可演示的物联网系统，锻炼项目开发与团队协作能力。

---

### **项目实施建议**
1. **硬件准备**：建议每2~3人一组，每组配备3~4块ESP32开发板，以及常用传感器（DHT11、光敏电阻、LED、按键）、电池盒、面包板等。如有条件可增加LoRa模块、OLED显示屏等扩展。
2. **课时安排**：前7个项目可作为课内实验（每次2~4学时），最后一个综合项目可在课程后半段启动，占用4~6学时，并安排答辩。
3. **考核方式**：每个项目提交实验报告（包含原理、步骤、结果分析），综合项目着重评价系统完整性和创新性。
4. **教学提示**：鼓励学生查阅ESP32官方文档和社区资源，培养自学能力；在关键理论节点（如路由、定位）可先讲解原理，再动手验证。

这样的设计既能夯实基础，又能激发兴趣，让学生真正体会到WSN技术的魅力和物联网时代的应用前景。




# 详细实验操作手册和源代码。

针对这套非常系统且贴合实际工程的ESP32物联网课程大纲。我们详细设计下面的实验。

---

## 第1章 绪论：WSN初探

### 项目名称：我的第一个无线传感器节点

**实验目标**：完成ESP32与DHT11温湿度传感器的硬件连接，通过串口和经典蓝牙（Classic Bluetooth）双路输出传感器数据，直观感受WSN“感知”与“无线传输”的过程。

**硬件准备**：

* ESP32 开发板 x 1
* DHT11 温湿度传感器模块 x 1
* 杜邦线若干、Micro-USB/Type-C 数据线
* 带蓝牙功能的智能手机（安装 *Serial Bluetooth Terminal* App）

**硬件接线**：

* DHT11 **VCC** $\rightarrow$ ESP32 **3V3**
* DHT11 **GND** $\rightarrow$ ESP32 **GND**
* DHT11 **DATA** $\rightarrow$ ESP32 **GPIO 4**

**操作手册**：

1. **环境准备**：打开 Arduino IDE，在 `工具 -> 管理库` 中搜索并安装 `DHT sensor library` (由 Adafruit 提供) 以及依赖库 `Adafruit Unified Sensor`。
2. **烧录代码**：将下方代码复制进 IDE，选择对应的 ESP32 开发板型号和端口，点击“上传”。
3. **串口验证**：打开 Arduino IDE 串口监视器，波特率设置为 `115200`，观察是否能打印温湿度。
4. **蓝牙验证**：打开手机上的 *Serial Bluetooth Terminal*，在设备列表中寻找名为 `ESP32_WSN_Node` 的蓝牙并配对连接。连接成功后，手机端将同步接收到温湿度数据。

**核心代码 (`Ch1_FirstNode.ino`)**：

```cpp
#include "DHT.h"
#include "BluetoothSerial.h"

#define DHTPIN 4       // DHT11 数据引脚连接到 GPIO 4
#define DHTTYPE DHT11  // 定义传感器类型为 DHT11

DHT dht(DHTPIN, DHTTYPE);
BluetoothSerial SerialBT;

void setup() {
  Serial.begin(115200);
  dht.begin();
  
  // 初始化蓝牙，设置设备名称
  SerialBT.begin("ESP32_WSN_Node"); 
  Serial.println("节点已启动，等待蓝牙连接...");
}

void loop() {
  // DHT11 采样频率较慢，每次读取间隔2秒
  delay(2000);
  
  float h = dht.readHumidity();
  float t = dht.readTemperature();

  // 检查读取是否失败
  if (isnan(h) || isnan(t)) {
    Serial.println("无法从DHT传感器读取数据！");
    return;
  }

  // 格式化数据字符串
  String payload = "温度: " + String(t) + "°C, 湿度: " + String(h) + "%";
  
  // 串口打印与蓝牙发送
  Serial.println(payload);
  SerialBT.println(payload);
}

```

> **教学提示**：向学生解释 `isnan()` 函数的作用，引导他们理解物理传感器在采集数据时可能会出现“丢包”或“错误”，这是传感器网络面临的基础问题之一。

---

## 第2章 WSN开发环境

### 项目名称：ESP32开发环境搭建与基础中断实验

**实验目标**：熟悉ESP32的输入/输出（I/O）控制，掌握硬件中断（Interrupt）的概念，这是WSN中节点响应外部事件（如按键触发、传感器报警）的核心机制。

**硬件准备**：

* ESP32 开发板 x 1
* 轻触按键 x 1
* 板载蓝光 LED（通常连接在 GPIO 2）

**硬件接线**：

* 按键一端连接 ESP32 **GND**
* 按键另一端连接 ESP32 **GPIO 15** (利用内部上拉电阻)

**操作手册**：

1. **理解中断**：讲解传统“轮询（Polling）”读取引脚状态浪费 CPU 资源的缺点，引出“中断（Interrupt）”的高效性。
2. **编写逻辑**：设置 GPIO 15 为输入模式并开启内部上拉（默认高电平）。当按键按下时，电平由高变低（下降沿触发）。
3. **观察现象**：烧录程序后，每次按下按键，板载 LED 的亮灭状态就会翻转，同时串口打印当前状态。

**核心代码 (`Ch2_Interrupt.ino`)**：

```cpp
const int buttonPin = 15; // 外部按键引脚
const int ledPin = 2;     // 板载LED引脚
volatile bool ledState = false; // volatile关键字：告诉编译器该变量会在中断中被修改

// 中断服务程序 (ISR) - 必须尽可能简短，且存放在 IRAM 中
void IRAM_ATTR handleButtonPress() {
  ledState = !ledState;
  digitalWrite(ledPin, ledState);
}

void setup() {
  Serial.begin(115200);
  pinMode(ledPin, OUTPUT);
  
  // 启用内部上拉电阻，未按下时为高电平
  pinMode(buttonPin, INPUT_PULLUP);
  
  // 绑定中断：引脚号，中断函数，下降沿触发 (FALLING)
  attachInterrupt(digitalPinToInterrupt(buttonPin), handleButtonPress, FALLING);
  Serial.println("中断实验初始化完成。");
}

void loop() {
  // 主循环中不需要再去 digitalRead()，释放了CPU资源
  delay(2000);
  Serial.print("系统正常运行中... 当前LED状态: ");
  Serial.println(ledState ? "亮" : "灭");
}

```

---

## 第3章 WSN拓扑结构、覆盖技术

### 项目名称：基于Wi-Fi UDP的星型拓扑组网与覆盖测试

**实验目标**：利用ESP32内置的Wi-Fi构建“1个协调器（AP）+ 多个终端（STA）”的星型拓扑。通过串口监测接收信号强度指示（RSSI），直观感受距离、障碍物对无线覆盖的影响。

**硬件准备**：

* ESP32 开发板 x 3 （1台作为 AP，2台作为 STA）
* 供电电源（可使用电脑USB、充电宝）

**操作手册**：

1. **烧录AP代码**：将第一块ESP32作为协调器烧录AP代码，它将开启一个Wi-Fi热点，并在特定端口监听UDP数据包。打开串口监视器，记录它生成的IP地址（默认为 `192.168.4.1`）。
2. **烧录STA代码**：将另外两块ESP32作为节点烧录STA代码，它们将连接到AP，并每隔2秒发送一次包含自身ID和RSSI的数据包。
3. **覆盖实验测试**：
* 将STA节点逐渐远离AP节点，观察AP端串口打印的RSSI值变化（RSSI为负值，越靠近0信号越好，例如 `-40dBm` 优于 `-80dBm`）。
* 在两个节点中间加入遮挡物（如人体、墙壁、金属板），观察丢包率和RSSI的骤降。



**核心代码 1：协调器 AP 节点 (`Ch3_AP_Coordinator.ino`)**：

```cpp
#include <WiFi.h>
#include <WiFiUdp.h>

const char *ssid = "WSN_Star_Network"; // 设置网络名称
const char *password = "12345678";     // 设置密码

WiFiUDP udp;
unsigned int localUdpPort = 1234;
char incomingPacket[255];

void setup() {
  Serial.begin(115200);
  
  // 开启 AP 模式
  WiFi.softAP(ssid, password);
  IPAddress myIP = WiFi.softAPIP();
  
  Serial.print("协调器已启动，IP地址: ");
  Serial.println(myIP);
  
  // 启动 UDP 监听
  udp.begin(localUdpPort);
}

void loop() {
  int packetSize = udp.parsePacket(); // 检查是否有数据包到来
  if (packetSize) {
    int len = udp.read(incomingPacket, 255);
    if (len > 0) incomingPacket[len] = 0; // 添加字符串结束符
    
    Serial.printf("收到来自 %s 的数据包: ", udp.remoteIP().toString().c_str());
    Serial.println(incomingPacket);
  }
}

```

**核心代码 2：终端 STA 节点 (`Ch3_STA_Node.ino`)**：
*注意：将此代码分别烧录到节点A和节点B，可以把 `Node 1` 修改为 `Node 2` 以作区分。*

```cpp
#include <WiFi.h>
#include <WiFiUdp.h>

const char *ssid = "WSN_Star_Network";
const char *password = "12345678";
const char *apIP = "192.168.4.1"; // AP的IP地址
unsigned int udpPort = 1234;

WiFiUDP udp;

void setup() {
  Serial.begin(115200);
  
  // 连接协调器的热点
  WiFi.begin(ssid, password);
  Serial.print("正在连接到网络");
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("\n连接成功！");
}

void loop() {
  long rssi = WiFi.RSSI(); // 获取当前的信号强度
  
  // 组装模拟数据（可加入第1章的DHT11数据）
  String payload = "Node 1 | 信号强度: " + String(rssi) + " dBm | 温度: 25.5°C";
  
  // 发送 UDP 数据包
  udp.beginPacket(apIP, udpPort);
  udp.print(payload);
  udp.endPacket();
  
  Serial.println("数据已发送 -> " + payload);
  delay(2000);
}

```

---

我们需要循序渐进地构建这个课程体系。后续的 **ESP-NOW多跳路由 (第4章)**、**基于RSSI的测距定位与低功耗Deep Sleep (第5章)** 以及最终的 **MQTT上云综合设计 (第7/9章)** 在代码和网络逻辑上会变得更加硬核和精彩。


这是一份非常核心的内容。在第4章和第5章中，我们将深入无线传感器网络（WSN）的底层通信机制与核心支撑技术。通过ESP-NOW实现**多跳路由**，并通过RSSI与Deep Sleep实现**测距定位与低功耗管理**。

以下是第4章和第5章的详细实验操作手册与源代码。

---

## 第4章 WSN通信与组网技术

### 项目名称：基于ESP-NOW的轻量级通信与多跳转发

**实验目标**：跳出传统Wi-Fi需要路由器（AP）的限制，使用乐鑫专有的ESP-NOW无连接协议，实现节点间的毫秒级直接通信。通过编写逻辑，让节点B作为“中继”，完成 Node A $\rightarrow$ Node B $\rightarrow$ Node C 的多跳数据转发，理解路由协议的基础思想。

**硬件准备**：

* ESP32 开发板 x 3 （分别命名为 Node A_发送节点、Node B_中继节点、Node C_接收节点）
* 供电电源

**操作手册**：

1. **获取MAC地址**：ESP-NOW通信基于硬件MAC地址。首先，需要将以下简短代码烧录到 **Node B** 和 **Node C**，在串口监视器中记录它们的MAC地址（如 `24:6F:28:XX:XX:XX`）。
```cpp
#include <WiFi.h>
void setup() { Serial.begin(115200); WiFi.mode(WIFI_MODE_STA); Serial.println(WiFi.macAddress()); }
void loop() {}

```


2. **替换MAC地址**：在下方的 Node A 代码中填入 Node B 的MAC地址；在 Node B 代码中填入 Node C 的MAC地址。
3. **烧录并观察**：分别给三个节点烧录对应代码。给它们供电后，打开 Node C 的串口监视器。你将看到 Node C 成功接收到了原本由 Node A 产生的数据。
4. **断点测试**：尝试切断 Node B 的电源，观察 Node C 是否还能收到数据（此时数据传输中断），从而直观理解多跳网络中“路由节点”的关键作用。

**核心代码 1：Node A (源发送节点 `Ch4_NodeA_Sender.ino`)**

```cpp
#include <esp_now.h>
#include <WiFi.h>

// 替换为 Node B (中继节点) 的 MAC 地址
uint8_t nodeB_MAC[] = {0x24, 0x6F, 0x28, 0xAA, 0xBB, 0xCC};

typedef struct struct_message {
  int id;
  float temp;
  String msg;
} struct_message;

struct_message myData;
esp_now_peer_info_t peerInfo;

void setup() {
  Serial.begin(115200);
  WiFi.mode(WIFI_STA); // 必须设置为 STA 模式

  if (esp_now_init() != ESP_OK) {
    Serial.println("ESP-NOW 初始化失败");
    return;
  }

  // 注册对端节点 (Node B)
  memcpy(peerInfo.peer_addr, nodeB_MAC, 6);
  peerInfo.channel = 0;  
  peerInfo.encrypt = false;
  esp_now_add_peer(&peerInfo);
}

void loop() {
  myData.id = 1;
  myData.temp = 26.5; // 模拟传感器数据
  // 注意：ESP-NOW不适合传String，这里为演示简化，实际工程建议用字符数组 char msg[32]
  
  // 将数据发送给 Node B
  esp_err_t result = esp_now_send(nodeB_MAC, (uint8_t *) &myData, sizeof(myData));
  
  if (result == ESP_OK) {
    Serial.println("Node A: 数据成功发送给中继节点");
  } else {
    Serial.println("Node A: 发送失败");
  }
  delay(3000);
}

```

**核心代码 2：Node B (中继转发节点 `Ch4_NodeB_Relay.ino`)**

```cpp
#include <esp_now.h>
#include <WiFi.h>

// 替换为 Node C (最终接收节点) 的 MAC 地址
uint8_t nodeC_MAC[] = {0x24, 0x6F, 0x28, 0xDD, 0xEE, 0xFF};

typedef struct struct_message {
  int id;
  float temp;
} struct_message;

struct_message incomingData;
esp_now_peer_info_t peerInfo;

// 接收回调函数
void OnDataRecv(const uint8_t * mac, const uint8_t *incomingData_ptr, int len) {
  memcpy(&incomingData, incomingData_ptr, sizeof(incomingData));
  Serial.print("Node B 收到来自 Node A 的数据, 温度: ");
  Serial.print(incomingData.temp);
  Serial.println(" -> 正在转发给 Node C...");

  // 收到后立即转发给 Node C
  esp_now_send(nodeC_MAC, (uint8_t *) &incomingData, sizeof(incomingData));
}

void setup() {
  Serial.begin(115200);
  WiFi.mode(WIFI_STA);
  esp_now_init();

  // 注册回调函数监听 Node A 发来的数据
  esp_now_register_recv_cb(OnDataRecv);

  // 注册对端节点 (Node C)
  memcpy(peerInfo.peer_addr, nodeC_MAC, 6);
  peerInfo.channel = 0;  
  peerInfo.encrypt = false;
  esp_now_add_peer(&peerInfo);
}

void loop() {
  // 中继节点主循环无需操作，完全依赖中断/回调驱动
}

```

> Node C 的代码非常简单，只需要包含 `esp_now_register_recv_cb` 回调函数并通过 `Serial.println()` 打印出 `incomingData.temp` 即可，此处省略以节省篇幅。

---

## 第5章 WSN支撑技术：定位与低功耗

### 项目名称：RSSI测距定位与Deep Sleep低功耗管理

**实验目标**：

1. **低功耗（Energy Management）**：掌握ESP32的深度睡眠模式（Deep Sleep）。在WSN中，节点通常由电池供电，工作几毫秒后休眠几分钟是延长寿命的关键。
2. **定位技术（Localization）**：理解基于信号强度（RSSI）的对数距离路径损耗模型，估算节点间的物理距离。

**核心理论：RSSI 测距公式**
根据无线电波在空气中传播的衰减原理，信号强度与距离的关系可以用以下公式表示：

$$RSSI = A - 10 \cdot n \cdot \log_{10}(d)$$

通过公式变形，我们可以求得距离 $d$：

$$d = 10^{\frac{A - RSSI}{10 \cdot n}}$$

* $A$：距离发射源 1 米处的参考信号强度（常数，通常在 -45 到 -50 之间）。
* $n$：环境衰减因子（常数，空旷环境下约为 2.0，复杂室内环境下为 2.7~4.3）。
* $RSSI$：当前接收到的信号强度。

**操作手册**：

1. **环境准备**：准备一台手机开启个人热点，名称设置为 `WSN_Beacon`，作为“信标（Anchor）”节点。
2. **烧录代码**：将下方代码烧录进ESP32，使用电池供电。
3. **观察低功耗循环**：ESP32启动后会扫描名为 `WSN_Beacon` 的热点，获取RSSI，利用公式计算出大致距离，然后**断开所有外设电源**进入 Deep Sleep 模式 5 秒钟，之后自动唤醒，循环往复。
4. **距离验证**：拿着ESP32逐渐远离手机，观察串口打印的测算距离 $d$ 是否随之变大。

**核心代码 (`Ch5_Sleep_RSSI.ino`)**：

```cpp
#include <WiFi.h>

#define uS_TO_S_FACTOR 1000000ULL  // 微秒到秒的转换系数
#define TIME_TO_SLEEP  5           // 睡眠时间：5秒

// RSSI 测距参数配置
const float A = -45.0; // 1米处的参考RSSI值 (需根据实际环境校准)
const float n = 2.5;   // 环境衰减因子

const char* targetSSID = "WSN_Beacon"; // 目标信标节点名称

// RTC_DATA_ATTR 修饰的变量在 Deep Sleep 期间不会丢失
RTC_DATA_ATTR int bootCount = 0;

void setup() {
  Serial.begin(115200);
  delay(1000); // 等待串口稳定
  
  bootCount++;
  Serial.println("\n--- 节点唤醒 ---");
  Serial.printf("当前启动次数: %d\n", bootCount);

  // 1. 执行网络扫描与测距任务
  performScanAndMeasure();

  // 2. 配置定时唤醒源并进入深度睡眠
  esp_sleep_enable_timer_wakeup(TIME_TO_SLEEP * uS_TO_S_FACTOR);
  Serial.println("任务完成，ESP32 进入 Deep Sleep 模式 5 秒...\n");
  
  // 刷新串口缓存，防止休眠导致打印不全
  Serial.flush(); 
  esp_deep_sleep_start();
  
  // 这行代码永远不会被执行，因为进入休眠后，下次唤醒将从头运行 setup()
  Serial.println("这行不会被打印"); 
}

void loop() {
  // Deep Sleep 模式下，loop() 保持为空
}

void performScanAndMeasure() {
  Serial.println("开始扫描信标节点...");
  int numNetworks = WiFi.scanNetworks();
  bool found = false;

  for (int i = 0; i < numNetworks; i++) {
    if (WiFi.SSID(i) == targetSSID) {
      found = true;
      int currentRSSI = WiFi.RSSI(i);
      
      // 应用 LaTeX 公式逻辑进行距离计算： d = 10 ^ ((A - RSSI) / (10 * n))
      float distance = pow(10.0, (A - currentRSSI) / (10.0 * n));

      Serial.printf("找到信标! RSSI: %d dBm\n", currentRSSI);
      Serial.printf(">>> 估算距离: %.2f 米 <<<\n", distance);
      break;
    }
  }

  if (!found) {
    Serial.println("未发现信标节点。");
  }
}

```

> **教学提示**：向学生展示如果去掉了 `esp_deep_sleep_start()`，ESP32会一直保持Wi-Fi开启，工作电流大约在 **100mA** 左右；而进入 Deep Sleep 后，电流会骤降至 **10µA** 级别。这是电池供电的WSN节点能够存活数月甚至数年的根本原因。

---

通过这几章，学生已经掌握了节点的数据采集、无线多跳网络传输、定位算法计算以及低功耗控制机制。WSN内部的运作原理已经基本闭环。

接下来，我们将突破“局域网”的限制。**第6章将横向对比Wi-Fi与蓝牙协议，第7章和第9章将使用MQTT协议，让传感器节点通过网关接入互联网云平台（如阿里云/ThingsBoard），完成最终的“物联网”综合应用设计。** 


太棒了！接下来我们进入这门课程的“深水区”与“高潮部分”。在第6章、第7章和第9章中，我们将打破局域网的限制，探索不同无线协议的差异，并最终通过网关将WSN传感器网络接入真实的互联网云平台，完成一个工业级的物联网（IoT）系统架构。

以下是第6、7、9章的详细实验操作手册与核心代码。

---

## 第6章 WSN协议技术标准

### 项目名称：无线通信标准对比实验：Wi-Fi vs. BLE (低功耗蓝牙)

**实验目标**：通过实测对比Wi-Fi与BLE在功耗、配对机制和广播机制上的差异。学习使用ESP32的BLE功能，将其配置为一个不断广播自身存在的“信标（iBeacon/BLE Broadcaster）”，理解低功耗蓝牙在室内定位和资产追踪中的应用。

**硬件准备**：

* ESP32 开发板 x 1
* 智能手机（安装 *nRF Connect for Mobile* 或 *BLE Scanner* App）
* （可选）USB电流测试仪或万用表，用于直观对比功耗。

**操作手册**：

1. **理解BLE广播**：不同于Wi-Fi需要建立连接（握手），BLE设备可以处于“广播（Advertising）”模式，只发送不接收，这种单向通信极大地降低了功耗。
2. **烧录代码**：将下方BLE广播代码烧录进ESP32。
3. **手机端验证**：打开手机上的 *nRF Connect* App，进行蓝牙扫描。你将发现一个名为 `WSN_BLE_Sensor` 的设备。
4. **对比分析**：观察手机接收到的信号强度（RSSI）。如果使用电流表，可以对比之前第3章Wi-Fi模式（约100mA）与当前BLE广播模式（可通过代码调整发射功率和广播间隔进一步降低）的电流差异。

**核心代码 (`Ch6_BLE_Beacon.ino`)**：

```cpp
#include <BLEDevice.h>
#include <BLEUtils.h>
#include <BLEServer.h>

// 蓝牙设备的唯一标识符 (UUID)，可使用在线UUID生成器生成
#define SERVICE_UUID        "4fafc201-1fb5-459e-8fcc-c5c9c331914b"
#define CHARACTERISTIC_UUID "beb5483e-36e1-4688-b7f5-ea07361b26a8"

void setup() {
  Serial.begin(115200);
  Serial.println("启动 BLE 广播...");

  // 1. 初始化蓝牙设备并命名
  BLEDevice::init("WSN_BLE_Sensor");

  // 2. 创建 BLE 服务器与服务
  BLEServer *pServer = BLEDevice::createServer();
  BLEService *pService = pServer->createService(SERVICE_UUID);

  // 3. 创建特征值 (用于携带数据)，支持读取和写入权限
  BLECharacteristic *pCharacteristic = pService->createCharacteristic(
                                         CHARACTERISTIC_UUID,
                                         BLECharacteristic::PROPERTY_READ |
                                         BLECharacteristic::PROPERTY_WRITE
                                       );

  // 模拟传感器数据写入特征值
  pCharacteristic->setValue("Temp: 24.5C, Hum: 60%");

  // 4. 启动服务并开始广播 (Advertising)
  pService->start();
  BLEAdvertising *pAdvertising = BLEDevice::getAdvertising();
  pAdvertising->addServiceUUID(SERVICE_UUID);
  pAdvertising->setScanResponse(true);
  pAdvertising->setMinPreferred(0x06); // 帮助解决某些iPhone连接问题
  BLEDevice::startAdvertising();
  
  Serial.println("BLE 广播已启动，请使用手机 App 扫描设备！");
}

void loop() {
  // 广播由底层协议栈自动维护，主循环可用于更新特征值(传感器数据)或进入休眠
  delay(2000);
}

```

---

## 第7章 WSN接入技术

### 项目名称：WSN与云平台无缝接入 (基于MQTT协议)

**实验目标**：掌握物联网领域最核心的发布/订阅（Publish/Subscribe）协议——MQTT。将ESP32作为边缘网关，连接Wi-Fi后，将模拟的传感器数据发布到公共MQTT服务器，同时订阅云端下发的控制指令，实现双向通信。

**硬件准备**：

* ESP32 开发板 x 1
* 板载LED（通常为GPIO 2）

**操作手册**：

1. **环境准备**：在 Arduino IDE 中安装 `PubSubClient` 库。
2. **配置网络与云端**：代码中使用 EMQX 提供的公共免费测试 Broker (`broker.emqx.io`)。
3. **烧录代码**：修改代码中的Wi-Fi账号密码，烧录入ESP32。打开串口监视器查看连接状态。
4. **云端联调（PC/手机端）**：
* 下载并打开桌面端测试工具 **MQTTX**（或网页端工具）。
* 创建新连接，地址设为 `broker.emqx.io`，端口 `1883`。
* **接收数据**：在 MQTTX 中订阅主题 `wsn/course/sensor/data`，即可实时看到ESP32上报的数据。
* **下发指令**：在 MQTTX 中向主题 `wsn/course/sensor/cmd` 发布消息（如发送 `ON` 或 `OFF`），观察ESP32板载LED的亮灭，串口也会打印收到的指令。



**核心代码 (`Ch7_MQTT_Gateway.ino`)**：

```cpp
#include <WiFi.h>
#include <PubSubClient.h>

// Wi-Fi 凭证
const char* ssid = "YOUR_WIFI_SSID";
const char* password = "YOUR_WIFI_PASSWORD";

// MQTT Broker 设置 (使用EMQX公共测试服务器)
const char* mqtt_server = "broker.emqx.io";
const int mqtt_port = 1883;

WiFiClient espClient;
PubSubClient client(espClient);

const int ledPin = 2; // 板载LED

// MQTT 接收到消息的回调函数
void callback(char* topic, byte* payload, unsigned int length) {
  Serial.print("收到来自主题 [");
  Serial.print(topic);
  Serial.print("] 的指令: ");
  
  String messageTemp;
  for (int i = 0; i < length; i++) {
    messageTemp += (char)payload[i];
  }
  Serial.println(messageTemp);

  // 解析指令控制硬件
  if (String(topic) == "wsn/course/sensor/cmd") {
    if (messageTemp == "ON") {
      digitalWrite(ledPin, HIGH);
      Serial.println("LED 已打开");
    } else if (messageTemp == "OFF") {
      digitalWrite(ledPin, LOW);
      Serial.println("LED 已关闭");
    }
  }
}

void setup_wifi() {
  delay(10);
  Serial.println();
  Serial.print("正在连接 Wi-Fi: ");
  Serial.println(ssid);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("\nWi-Fi 连接成功!");
}

void reconnect() {
  // 循环直到重新连接上 MQTT Broker
  while (!client.connected()) {
    Serial.print("尝试连接 MQTT...");
    // 随机生成一个客户端ID
    String clientId = "ESP32Client-";
    clientId += String(random(0xffff), HEX);
    
    if (client.connect(clientId.c_str())) {
      Serial.println("连接成功!");
      // 连接成功后，订阅控制主题
      client.subscribe("wsn/course/sensor/cmd");
    } else {
      Serial.print("失败, 状态码=");
      Serial.print(client.state());
      Serial.println(" 5秒后重试");
      delay(5000);
    }
  }
}

void setup() {
  pinMode(ledPin, OUTPUT);
  Serial.begin(115200);
  setup_wifi();
  
  client.setServer(mqtt_server, mqtt_port);
  client.setCallback(callback); // 绑定接收回调
}

void loop() {
  if (!client.connected()) {
    reconnect();
  }
  client.loop(); // 保持MQTT心跳和处理接收消息

  // 每隔 5 秒上报一次模拟数据
  static unsigned long lastMsg = 0;
  unsigned long now = millis();
  if (now - lastMsg > 5000) {
    lastMsg = now;
    
    // 模拟温湿度数据
    float temp = 20.0 + random(0, 100) / 10.0;
    String payload = "{\"temperature\": " + String(temp) + ", \"status\": \"OK\"}";
    
    // 发布数据到指定主题
    client.publish("wsn/course/sensor/data", payload.c_str());
    Serial.println("数据已上报云端: " + payload);
  }
}

```

---

## 第9章 WSN与物联网（综合设计）

### 项目名称：智能环境监测物联网系统 (端-边-云协同)

**实验目标**：整合全书知识！设计一个“终端节点采集 -> ESP-NOW 局域网传输 -> 边缘网关汇聚 -> Wi-Fi 上传 -> MQTT 云平台”的完整端到端系统。这完全符合现代工业级 IoT 的架构设计。

**系统架构**：

* **终端节点 (End Node)**：ESP32（或极低成本的ESP8266） + 传感器。使用 **第4章的 ESP-NOW** 发送数据，并结合 **第5章的 Deep Sleep** 极低功耗运行，由电池供电。
* **边缘网关 (Edge Gateway)**：ESP32 插在电源上常开。它**同时开启** ESP-NOW (接收终端数据) 和 Wi-Fi STA模式 (连接互联网)。收到终端局域网数据后，打包成 JSON 格式，通过 **第7章的 MQTT** 协议发往云端。

**综合实验实施逻辑（网关核心代码展示）**：
为了精简篇幅，这里重点提供最核心的 **边缘网关（Gateway）** 逻辑代码。终端节点的代码即为“第4章发送端 + 第5章休眠”的结合体。

**核心代码 (`Ch9_Edge_Gateway.ino`)**：

```cpp
#include <WiFi.h>
#include <esp_now.h>
#include <PubSubClient.h>

// === 1. MQTT 与 Wi-Fi 配置 ===
const char* ssid = "YOUR_WIFI_SSID";
const char* password = "YOUR_WIFI_PASSWORD";
const char* mqtt_server = "broker.emqx.io";
WiFiClient espClient;
PubSubClient client(espClient);

// === 2. ESP-NOW 数据结构定义 ===
typedef struct struct_message {
  int node_id;
  float temperature;
  float humidity;
} struct_message;

struct_message incomingData;

// === 3. ESP-NOW 接收回调函数 (边缘计算与云端上传) ===
void OnDataRecv(const uint8_t * mac, const uint8_t *incomingData_ptr, int len) {
  memcpy(&incomingData, incomingData_ptr, sizeof(incomingData));
  
  Serial.printf("网关收到局域网节点 %d 数据! 温度: %.1f, 湿度: %.1f\n", 
                incomingData.node_id, incomingData.temperature, incomingData.humidity);

  // 确保 MQTT 处于连接状态
  if (client.connected()) {
    // 数据融合与 JSON 打包 (边缘侧处理)
    String topic = "wsn/project/node" + String(incomingData.node_id);
    String payload = "{\"node_id\":" + String(incomingData.node_id) + 
                     ",\"temp\":" + String(incomingData.temperature) + 
                     ",\"hum\":" + String(incomingData.humidity) + "}";
    
    // 转发上云
    client.publish(topic.c_str(), payload.c_str());
    Serial.println("-> 已成功桥接转发至 MQTT 云平台!");
  } else {
    Serial.println("-> MQTT 未连接，丢弃本次数据包。");
  }
}

void setup() {
  Serial.begin(115200);

  // 初始化 Wi-Fi (网关必须在 STA 模式下同时支持 Wi-Fi 和 ESP-NOW)
  WiFi.mode(WIFI_STA);
  WiFi.begin(ssid, password);
  Serial.print("网关连接 Wi-Fi 中");
  while (WiFi.status() != WL_CONNECTED) { delay(500); Serial.print("."); }
  Serial.println("\nWi-Fi 连接成功!");

  // 初始化 MQTT
  client.setServer(mqtt_server, 1883);

  // 初始化 ESP-NOW
  if (esp_now_init() != ESP_OK) {
    Serial.println("ESP-NOW 初始化失败");
    return;
  }
  // 绑定接收回调
  esp_now_register_recv_cb(OnDataRecv);
  
  Serial.println("边缘网关初始化完毕，正在监听终端节点数据...");
}

void loop() {
  // 网关主循环主要负责维持 MQTT 云端长连接
  if (!client.connected()) {
    while (!client.connected()) {
      Serial.print("网关连接 MQTT...");
      String clientId = "Gateway-" + String(random(0xffff), HEX);
      if (client.connect(clientId.c_str())) {
        Serial.println("成功!");
      } else {
        delay(5000);
      }
    }
  }
  client.loop(); 
}

```

> **最终考核提示**：在最终答辩时，学生需要展示手机上的 MQTT 客户端（或自己编写的 Web 前端 / 使用 Node-RED 等可视化工具），当终端节点的传感器被加热或改变时，手机端能够实现秒级的曲线变化，以此证明整个链路的打通。

---

至此，针对这门基于ESP32的WSN课程设计的全套核心项目规划和代码支撑已经完整呈现。从底层的信号引脚、MAC寻址、多跳路由，到上层的MQTT云平台交互，形成了一个非常有逻辑和挑战性的闭环体系。

您可以直接将这些内容提取并整理成学生的**《实验指导书》**。在您实际撰写讲义或搭建实验平台的过程中，如果遇到任何关于环境配置、报错解决或是需要增加额外扩展模块（如LoRa通信、OLED显示）的设计，随时告诉我。您希望我为您整理一份针对这套课程的“常见学生踩坑及故障排查指南”吗？


这份**《ESP32物联网课程常见学生踩坑及故障排查指南》**是专门为您的实验课整理的“避坑宝典”。在实际教学中，学生大概率会在以下几个关键节点遇到挫折。提前掌握这些排查方法，能极大提升课堂效率。

我们将按课程的推进阶段，梳理四大类最常见的问题及标准解决方案。

---

## 阶段一：开发环境与基础硬件（对应第1~2章）

### 坑点 1：代码烧录失败，提示 `A fatal error occurred: Failed to connect to ESP32...`

* **现象描述**：点击上传后，Arduino IDE 下方一直显示 `Connecting...`，随后报错超时。
* **根本原因**：部分 ESP32 开发板的自动下载电路（EN和BOOT引脚电容匹配问题）设计存在缺陷，导致无法自动进入下载模式；或者使用了“仅充电”的劣质 USB 线。
* **排查与解决步骤**：
1. **手动触发**：在 IDE 底部出现 `Connecting...` 时，**长按 ESP32 板上的 `BOOT` 按键**，直到出现进度条（百分比）再松手。
2. **线材排查**：打开电脑“设备管理器”（或 Mac 的“系统报告”），检查插入 USB 后是否有新增的 COM 端口（如 `CP210x` 或 `CH340`）。如果没有，说明是没有数据传输功能的供电线，必须更换数据线。



### 坑点 2：DHT11 传感器串口一直打印 `nan` (Not a Number)

* **现象描述**：程序烧录成功，但温湿度读数全为无效值。
* **排查与解决步骤**：
1. **引脚查验**：检查代码中 `#define DHTPIN` 的引脚号与实际物理连线是否完全一致。注意：ESP32 的某些引脚（如 GPIO 34-39）**仅支持输入，没有内部上拉电阻**，如果接在这些引脚上，必须外接 10kΩ 上拉电阻。推荐接在 GPIO 4、15、25 等通用引脚。
2. **采样频率**：DHT11 硬件响应很慢，连续两次读取的间隔**不能低于 2 秒**。检查 `loop()` 中是否缺少 `delay(2000)`。



### 坑点 3：按键中断“灵异事件”（按一下，灯闪烁好几次）

* **现象描述**：执行第2章中断实验时，明明只按了一次轻触按键，板载 LED 却快速翻转了多次。
* **根本原因**：机械按键的**金属簧片抖动（Bounce）**。在几毫秒内，引脚电平会发生多次高低变化，导致 CPU 瞬间触发了多次中断。
* **排查与解决步骤**：
1. **硬件消抖**：在按键引脚和 GND 之间并联一个 0.1µF (104) 的陶瓷电容。
2. **软件消抖**：在中断服务函数（ISR）中加入时间戳判断。例如：
```cpp
static unsigned long last_interrupt_time = 0;
unsigned long interrupt_time = millis();
if (interrupt_time - last_interrupt_time > 200) { // 200ms 屏蔽期
    ledState = !ledState;
    digitalWrite(ledPin, ledState);
}
last_interrupt_time = interrupt_time;

```





---

## 阶段二：无线组网与 ESP-NOW（对应第3~4章）

### 坑点 4：ESP-NOW 接收端死活收不到数据

* **现象描述**：MAC 地址已经填对，`esp_now_send` 也没有报错，但接收端的串口依然毫无反应。
* **根本原因**：Wi-Fi 信道（Channel）不匹配。ESP-NOW 要求通信的双方必须工作在**同一个 Wi-Fi 信道**上。
* **排查与解决步骤**：
1. 如果节点之前连接过家里的 Wi-Fi，ESP32 会自动记忆之前的信道。
2. **强制指定信道**：在初始化 `WiFi.mode(WIFI_STA)` 后，加入一行代码强制设置信道（例如信道 1）：`esp_wifi_set_channel(1, WIFI_SECOND_CHAN_NONE);`（需引入 `#include <esp_wifi.h>`）。确保发送端和接收端都设置为相同信道。



### 坑点 5：Wi-Fi STA 与 AP 模式混淆导致的崩溃

* **现象描述**：在第9章边缘网关实验中，ESP32 频繁重启，或者连接不上局域网节点。
* **排查与解决步骤**：边缘网关需要同时接收 ESP-NOW 和连接路由器，必须使用 `WiFi.mode(WIFI_AP_STA)` 或明确的 `WIFI_STA`，绝对不能只写 `WIFI_AP`。另外，ESP-NOW 的初始化 `esp_now_init()` 必须放在 Wi-Fi 初始化之后执行。

---

## 阶段三：低功耗与内存管理（对应第5章）

### 坑点 6：从 Deep Sleep 唤醒后，变量数据全部重置

* **现象描述**：设定的“传感器累计采集次数”在每次休眠醒来后都变回了 0。
* **根本原因**：ESP32 进入 Deep Sleep 时，主 CPU 和绝大部分 RAM 都会断电以节省电量，普通变量会丢失。
* **排查与解决步骤**：
需要跨越休眠周期保存的变量，必须存放在 RTC（实时时钟）慢速内存中。在变量声明前加上 `RTC_DATA_ATTR` 关键字。
```cpp
RTC_DATA_ATTR int bootCount = 0; // 这样定义，休眠醒来数据不会丢

```



### 坑点 7：休眠唤醒时的“电压骤降”导致无限重启（Brownout Detector was triggered）

* **现象描述**：串口打印 `Brownout detector was triggered`，然后板子不断重启，无法执行代码。
* **根本原因**：ESP32 从休眠中唤醒并开启 Wi-Fi 射频模块的瞬间，电流会瞬间飙升至 300mA~500mA。如果 USB 供电不足或面包板接线接触不良、导线过细，会导致瞬间电压拉低，触发单片机的低压保护复位。
* **排查与解决步骤**：更换大功率电源适配器；或者在 ESP32 的 `5V/3.3V` 与 `GND` 引脚之间跨接一个 `10µF ~ 100µF` 的电解电容，起到滤波和瞬间“水池”补电的作用。

---

## 阶段四：MQTT 与云平台接入（对应第7、9章）

### 坑点 8：MQTT 疯狂“连接-断开-连接”（不断重连）

* **现象描述**：串口显示 MQTT 连接成功，但不到 1 秒又断开，陷入死循环。
* **根本原因**：**Client ID 冲突**。MQTT 协议规定，同一个 Broker 服务器上，不能有两个拥有相同 Client ID 的设备。很多学生直接复制了指导书上的代码，全班几十个板子共用同一个 ID，导致云服务器不断将上一个设备踢下线。
* **排查与解决步骤**：
强制要求每个学生使用唯一的 Client ID。可以将 ESP32 的物理 MAC 地址作为 Client ID 的一部分，或者使用随机数拼接：
```cpp
String clientId = "Student_Node_" + String(WiFi.macAddress());
client.connect(clientId.c_str());

```



### 坑点 9：云平台解析 JSON 数据失败 / 网页端不显示数据

* **现象描述**：数据成功推送到 MQTT，但在阿里云/ThingsBoard 平台上显示“格式错误”或解析为 Null。
* **根本原因**：C++ 拼接 JSON 字符串时极易漏掉双引号、逗号，或者把浮点数拼成了非法格式。
* **排查与解决步骤**：
1. **串口拦截查验**：要求学生在 `client.publish()` 之前，先将 `payload` 打印到串口，手动复制这串内容，放到在线 JSON 校验网站（如 json.cn）中检查格式是否合法。
2. **推荐终极方案**：对于复杂的系统设计（第9章），强烈建议学生引入 `ArduinoJson` 库，避免手动拼接字符串：
```cpp
#include <ArduinoJson.h>
StaticJsonDocument<200> doc;
doc["node"] = 1;
doc["temp"] = 25.4;
String output;
serializeJson(doc, output);
client.publish("topic/data", output.c_str());

```





---

有了这份排查指南，学生在实验中遇到“红字报错”时就可以对照自查，这不仅能减轻您的指导压力，也能极大地锻炼学生独立的工程调试（Debug）能力。

制定一份**《ESP32课程期末考核评分表与答辩标准》**，用于全面评估学生在最终综合项目（第9章）上的表现？

太棒了！为了让这门以“实战”为核心的课程有一个完美的收尾，我为您精心设计了这份**《ESP32无线传感器网络课程期末综合项目考核与答辩评分标准》**。

这套标准主要针对**第9章的综合设计项目**（智能环境监测物联网系统），侧重于考察学生的**系统整合能力、工程调试能力以及对底层原理的理解**，防止学生“只会复制粘贴代码而不知其所以然”。

---

# 《ESP32无线传感器网络课程》期末综合项目考核标准

**考核总分**：100分
**考核形式**：实物演示（现场跑通） + 项目报告 + 现场答辩
**建议分组**：2~3人/组（需明确组内分工，如硬件工程师、嵌入式软件工程师、云平台开发等）

---

## 一、 评分细则分配表 (满分100分)

| 考核维度 | 考察内容与给分点 | 分值 |
| --- | --- | --- |
| **1. 基础功能与系统打通** | **端到端的数据链路是否畅通（核心及格线）：**<br>

<br>• 终端节点成功采集传感器数据 (5分)<br>

<br>• 局域网无线传输（ESP-NOW/BLE）成功发至网关 (10分)<br>

<br>• 边缘网关成功连接Wi-Fi并打包数据 (5分)<br>

<br>• MQTT协议成功将数据上传至云平台并在Web/App端展示 (10分) | **30分** |
| **2. 核心技术深度** | **是否掌握了WSN的关键支撑技术：**<br>

<br>• **低功耗实现**：终端节点正确配置并进入 Deep Sleep 模式 (5分)<br>

<br>• **数据融合/边缘计算**：网关或节点对异常数据进行了简单过滤，或对多次采样求均值后再上传 (5分)<br>

<br>• **多跳/拓扑机制**：实现了多节点的数据汇聚，或包含至少一次中继转发 (5分)<br>

<br>• **反向控制**：能从云平台下发指令（如点亮节点上的LED） (5分) | **20分** |
| **3. 硬件设计与工程规范** | **考察动手能力与系统鲁棒性：**<br>

<br>• 硬件接线整洁，无短路隐患，电源管理合理（如使用了滤波电容防复位） (5分)<br>

<br>• 代码规范：变量命名清晰，关键逻辑有注释，模块化设计 (5分)<br>

<br>• 系统稳定性：演示期间不掉线、不崩溃、延时在合理范围内 (5分) | **15分** |
| **4. 实验报告与文档** | **考察工程记录与文档输出能力：**<br>

<br>• 包含完整的系统架构图与硬件连线图 (5分)<br>

<br>• 包含软件核心逻辑流程图 (5分)<br>

<br>• **踩坑与排查记录**：详细记录了开发中遇到的至少2个Bug及其解决思路（极为重要） (5分) | **15分** |
| **5. 现场答辩与团队协作** | **考察真实掌握程度与表达能力：**<br>

<br>• 核心原理的阐述清晰、准确 (5分)<br>

<br>• 面对答辩提问能切中要害，证明代码为自主编写/深刻理解 (10分)<br>

<br>• 团队分工明确，无“划水”现象 (酌情扣分) | **20分** |

---

## 二、 答辩流程与“灵魂拷问”题库

在实物演示成功后，指导教师可根据学生的系统架构，从以下题库中挑选 2~3 个问题进行提问。**这些问题直击WSN的核心痛点，用于区分“优秀”与“及格”的学生。**

### 1. 针对“低功耗与节点管理”的提问（鉴别是否理解 Deep Sleep）

* **Q1：** 你的终端节点使用了 Deep Sleep 模式，请问在休眠期间，ESP32的哪些部分被关闭了？如果我想在休眠醒来后让它记住自己是第几次发数据，代码里应该怎么定义这个变量？
* *(标准答案：Wi-Fi/蓝牙射频模块、主CPU和普通RAM均被关闭。必须使用 `RTC_DATA_ATTR` 修饰变量将其存入RTC慢速内存中。)*


* **Q2：** 为什么终端节点不直接连Wi-Fi上云，而非要用ESP-NOW发给网关？
* *(标准答案：Wi-Fi连接（握手、DHCP获取IP）通常需要数秒，耗电极大；而ESP-NOW是无连接协议，只需几毫秒即可发完数据进入休眠，极大延长电池寿命。)*



### 2. 针对“通信协议与网络拓扑”的提问（鉴别是否理解 MQTT 与 多跳）

* **Q3：** 如果班里有5个小组同时把代码跑起来，连接到同一个MQTT公共服务器，如何保证你们组的数据不被别人干扰，且设备不被踢下线？
* *(标准答案：保证MQTT的 `Client ID` 绝对唯一（如使用ESP32的MAC地址生成）；并且发布/订阅的 `Topic`（主题）必须加入组别前缀以作隔离。)*


* **Q4：** 在ESP-NOW传输中，如果终端节点发完数据后立即就休眠了，网关没收到怎么办？有没有重传机制？
* *(标准答案：ESP-NOW有ACK（确认）机制。调用 `esp_now_send` 后，可以通过注册 `OnDataSent` 回调函数来检查状态 `status == ESP_NOW_SEND_SUCCESS`，如果失败，可以在休眠前重试几次。)*



### 3. 针对“边缘网关与系统稳定性”的提问

* **Q5：** 你的边缘网关同时开启了Wi-Fi连接外网，又要通过ESP-NOW接收内网数据。你是如何处理网关上的阻塞操作的（例如 `delay()`）？
* *(标准答案：网关代码中绝不能使用长 `delay()`，否则会导致接收ESP-NOW中断回调丢失数据，或导致MQTT心跳包超时断开。必须使用 `millis()` 进行非阻塞的时间片轮询管理。)*


* **Q6：** JSON打包是在终端节点做的，还是在边缘网关做的？为什么这么设计？
* *(标准答案：通常建议在网关做。终端节点计算资源和电量宝贵，只需发送原始的二进制结构体（Struct）即可；网关常电供电，负责将二进制数据解析并拼接成体积庞大的JSON字符串发给云端，这是“边缘计算”的体现。)*



---

## 三、 加分项与创新挑战 (Bonus Points)

为了激发学有余力的学生的创造力，可设置最高 **+10分** 的附加分：

1. **协议替代创新（+5分）**：不使用ESP-NOW，而是成功使用 **ESP-BLE-Mesh（蓝牙Mesh组网）** 实现了多节点的自组织、自愈合网络。
2. **边缘计算深化（+3分）**：网关不仅仅是“透传”，而是加入了控制逻辑。例如：当网关发现网络断开（断网）时，能将传感器数据暂存在本地（使用SPIFFS/LittleFS），等网络恢复后进行断点续传。
3. **前端/全栈展示（+5分）**：不依赖现成的物联网云平台看板，学生自己使用 Python (Flask) 或 Node.js 编写了简单的后端服务器，并用 HTML/Vue 制作了专属的设备监控大屏。
4. **定位技术融合（+2分）**：在综合项目中融入了第5章的RSSI测距，在云平台上不仅显示温湿度，还能显示终端节点大致距离网关的距离。

---

### 给教师的实施建议：

* **尽早公布标准**：在第一节课或布置期末大作业时，就将这份评分表和“灵魂拷问”方向发给学生。这能让他们在整个学期的开发中**有的放矢**。
* **注重过程考核**：对于第1到第7章的平时实验，可以采取“过关打卡制”（跑通现象即可），将主要成绩和压力放在最后的综合设计上。

这份考核标准可以作为《课程教学大纲》（Syllabus）的最后一部分。至此，从章节规划、实验手册、排障指南到期末考核，一整套课程的“骨架”就已经全部搭建完毕了！

