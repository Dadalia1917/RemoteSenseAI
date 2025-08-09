# 基于计算机图像检测与大模型反馈的遥感卫星系统

这是一个基于计算机视觉和大语言模型的遥感卫星图像分析系统，用于检测和识别遥感图像中的目标，并提供智能分析反馈。

## 项目结构

项目由三个主要部分组成：

- **前端 (Vue)**：自主设计的用户界面，用于上传图像、查看检测结果和分析报告。
- **Spring Boot 后端**：自行开发的业务逻辑处理层，负责用户认证和数据管理。
- **Flask AI 服务**：自主搭建的图像检测和大模型集成服务。

## 功能特点

- 遥感图像目标检测与识别
- 目标检测结果可视化
- 多种类型目标识别（港口、船舶、储油罐等20类目标）
- 基于大语言模型的智能分析与建议
- 历史记录管理与查询
- 用户权限管理系统
- 实时摄像头监控模式

## 技术栈

- **前端**：Vue 3 + TypeScript + Element Plus
- **后端**：Spring Boot + MyBatis Plus
- **AI服务**：Flask + Ultralytics YOLOv8 + 大语言模型
- **数据库**：MySQL

## 运行环境要求

### 前端
- Node.js 16+
- npm 或 yarn

### Spring Boot 后端
- JDK 1.8
- Maven 3.6+
- MySQL 8.0+

### Flask AI 服务
- Python 3.11
- CUDA 支持（用于GPU加速，推荐CUDA 12.8）

## 快速开始

### 数据库配置
1. 创建名为`ai`的MySQL数据库
2. 导入根目录下的`database.sql`文件

### 后端配置与运行
1. 进入`springboot`目录
2. 修改`src/main/resources/application.properties`中的数据库配置
3. 执行以下命令：
   ```bash
   mvn clean package
   java -jar target/Kcsj-0.0.1-SNAPSHOT.jar
   ```

### AI服务配置与运行
1. 进入`flask`目录
2. 创建Python虚拟环境并安装依赖：
   ```bash
   python -m venv venv
   source venv/bin/activate  # Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```
3. 运行AI服务：
   ```bash
   python app.py
   ```

### 大语言模型部署
本项目使用LM-Studio进行大模型的本地部署与调用：

1. 下载并安装[LM-Studio](https://lmstudio.ai/)
2. 在LM-Studio中下载所需的大语言模型（推荐使用Llama3系列或其他开源模型）
3. 启动本地服务器，设置端口为5000或在配置文件中修改对应端口
4. Flask服务将自动连接到LM-Studio提供的API接口

#### 支持的AI模型选项

前端界面支持以下AI模型选项：

- **云端模型**：
  - `Deepseek-R1` - 使用Deepseek-R1云端API
  - `Qwen` - 使用通义千问云端API

- **局域网模型**：
  - `Deepseek-R1-LAN` - 使用局域网部署的Deepseek-R1
  - `Qwen3-LAN` - 使用局域网部署的Qwen 3.0
  - `Qwen2.5-VL-LAN` - 使用局域网部署的Qwen 2.5多模态视觉版
  - `Qwen2.5-Omni-LAN` - 使用局域网部署的Qwen 2.5 Omni全能版
  - `Gemma3-LAN` - 使用局域网部署的Gemma 3

- **本地模型**（通过LM-Studio部署）：
  - `Deepseek-R1-Local` - 本地部署的Deepseek-R1
  - `Qwen3-Local` - 本地部署的Qwen 3.0
  - `Qwen2.5-VL-Local` - 本地部署的Qwen 2.5多模态视觉版
  - `Qwen2.5-Omni-Local` - 本地部署的Qwen 2.5 Omni全能版
  - `Gemma3-Local` - 本地部署的Gemma 3
  
- `不使用AI` - 不使用大模型，仅使用目标检测功能

> 注意：本地模型需要通过LM-Studio下载并部署，局域网模型需要在局域网内有相应的服务器部署。云端模型需要配置相应的API密钥。

### 前端配置与运行
1. 进入`vue`目录
2. 安装依赖并启动服务：
   ```bash
   npm install
   npm run dev
   ```

## 系统访问
- 前端页面：http://localhost:3000
- Spring Boot 后端：http://localhost:9999
- Flask AI 服务：http://localhost:5000

## 实现目标检测的类别

系统目前支持以下20种遥感目标的检测：
- 港口
- 船舶
- 储油罐
- 烟囱
- 水坝
- 火车站
- 篮球场
- 机场
- 高速服务区
- 飞机
- 棒球场
- 高速收费站
- 车辆
- 高尔夫场
- 桥梁
- 田径场
- 立交桥
- 风车
- 网球场
- 体育场
