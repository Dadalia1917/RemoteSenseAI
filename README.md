# 基于计算机图像检测与大模型反馈的遥感卫星系统

这是一个基于计算机视觉和大语言模型的遥感卫星图像分析系统，用于检测和识别遥感图像中的目标，并提供智能分析反馈。

## 系统架构

本项目采用前后端分离架构，包含三个主要组件：

1. **前端(Vue)**：基于Vue3+TypeScript构建的用户界面，提供图像上传、检测结果展示和历史记录查询等功能。
2. **后端(SpringBoot)**：负责用户管理、数据存储和请求转发的Java服务。
3. **AI模型服务(Flask)**：运行深度学习模型和大语言模型的Python服务，提供图像分析和智能诊断功能。

## 主要功能

- 遥感图像目标检测与识别（支持20种目标类别）
- 目标检测结果可视化
- 实时摄像头监控模式
- 基于大语言模型的智能分析与建议
- 历史记录管理与查询
- 用户权限管理系统

## 技术栈

- **前端**：Vue 3、TypeScript、Element Plus
- **后端**：SpringBoot 3.5.4 (最新版)、MyBatis-Plus、MySQL
- **AI服务**：Flask、YOLOv8、大型语言模型API
- **Java版本**：JDK 24 (最新LTS版本)
- **部署**：Docker (可选)

## 🚀 最新更新

### 版本升级 (2024年12月)
- **JDK升级**：从Java 1.8 升级到 JDK 24，带来以下改进：
  - 更好的垃圾回收性能
  - 增强的安全特性
  - 改进的JVM性能和内存管理
- **Spring Boot升级**：从2.3.7升级到3.5.4
  - 支持更多现代化特性
  - 更好的性能和稳定性
  - 增强的安全性
- **依赖库更新**：升级了所有核心依赖到最新稳定版本
- **警告修复**：解决了JDK 24下的所有编译和运行时警告
  - 添加了`--sun-misc-unsafe-memory-access=allow`参数解决FastJSON2的sun.misc.Unsafe警告
  - 升级FastJSON2到2.0.58版本（最新稳定版）
  - 配置了完整的JVM参数确保在JDK 24下正常运行

## 快速开始

### 前提条件

- **JDK 24** (已升级到最新版本，包含性能优化和安全改进)
- Node.js 16+
- Python 3.8+
- MySQL 8.0+
- CUDA支持的GPU (推荐用于模型推理)
- LM-Studio (用于本地部署大模型)

### JDK 24 兼容性说明

本项目已完全适配JDK 24，所有JVM警告均已解决：

- ✅ **sun.misc.Unsafe警告** - 通过`--sun-misc-unsafe-memory-access=allow`参数解决
- ✅ **模块系统** - 配置了必要的`--add-opens`参数
- ✅ **动态代理** - 启用了`-XX:+EnableDynamicAgentLoading`
- ✅ **参数名保留** - 编译器配置了`-parameters`标志

如需手动运行，请使用以下JVM参数：
```bash
--enable-native-access=ALL-UNNAMED
--add-opens java.base/java.lang=ALL-UNNAMED 
--add-opens java.base/java.util=ALL-UNNAMED
--add-opens java.base/sun.misc=ALL-UNNAMED
--sun-misc-unsafe-memory-access=allow
-XX:+EnableDynamicAgentLoading
```

### 数据库配置

1. 创建名为`ai`的数据库
2. 运行`database.sql`脚本初始化数据库结构

### 后端服务启动

1. 进入springboot目录
2. 使用Maven构建项目：`mvn clean package`
3. 运行生成的jar文件：`java -jar target/Kcsj-0.0.1-SNAPSHOT.jar`

### AI服务启动

1. 进入flask目录
2. 安装依赖：`pip install -r requirements.txt`
3. 启动Flask服务：
   ```bash
   python main\(YOLO\).py  # YOLOv8模型
   # 或
   python main\(DETR\).py  # RT-DETR模型
   ```

### 前端启动

1. 进入vue目录
2. 安装依赖：`npm install`
3. 启动开发服务器：`npm run dev`
4. 构建生产版本：`npm run build`

## 大模型部署与使用

本系统支持多种大模型部署方式，用于生成遥感图像分析报告和建议：

### 支持的模型

- **云端API模型**
  - Deepseek-R1
  - Qwen

- **局域网部署模型**
  - Deepseek-R1-LAN
  - Qwen3-LAN
  - Qwen2.5-VL-LAN
  - Qwen2.5-Omni-LAN
  - Gemma3-LAN

- **本地部署模型**
  - Deepseek-R1-Local
  - Qwen3-Local
  - Qwen2.5-VL-Local
  - Qwen2.5-Omni-Local
  - Gemma3-Local

### 使用LM-Studio进行本地部署

1. 下载并安装 [LM-Studio](https://lmstudio.ai/)
2. 从Hugging Face或其他来源下载所需模型（如Deepseek-R1、Qwen等）
3. 在LM-Studio中加载模型
4. 启动本地API服务器（通常在http://localhost:1234）
5. 在系统设置中选择对应的"本地"模型选项

### 思考模式

系统支持开启思考模式（thinkMode），启用后大模型会提供更详细的分析过程和检测依据，适合科学研究和详细分析使用。

## 系统访问

- 前端页面：http://localhost:3000
- Spring Boot 后端：http://localhost:9999
- Flask AI 服务：http://localhost:5000

### 默认登录账号

- **管理员账号**：admin
- **密码**：admin123

## 使用说明

1. 访问系统前端界面
2. 使用默认管理员账号登录：admin/admin123
3. 进入系统后可以进行遥感图像的目标检测和分析
4. 选择合适的大模型进行智能分析和反馈

## 实现目标检测的类别

系统目前支持以下20种遥感目标的检测：

1. 港口 (Harbor)
2. 船舶 (Ship)
3. 储油罐 (Storage tank)
4. 烟囱 (Chimney)
5. 水坝 (Dam)
6. 火车站 (Train station)
7. 篮球场 (Basketball court)
8. 机场 (Airport)
9. 高速服务区 (Expressway service area)
10. 飞机 (Airplane)
11. 棒球场 (Baseball field)
12. 高速收费站 (Expressway toll station)
13. 车辆 (Vehicle)
14. 高尔夫场 (Golf field)
15. 桥梁 (Bridge)
16. 田径场 (Track field)
17. 立交桥 (Overpass)
18. 风车 (Windmill)
19. 网球场 (Tennis court)
20. 体育场 (Stadium)

## 模型信息

### 遥感图像检测模型

本系统使用YOLOv8模型对遥感图像进行目标检测和识别。预训练模型存储在`flask/weights/`目录下。

### 大语言模型

支持多种大语言模型，既可以通过API密钥访问云端模型，也可以通过LM-Studio在本地部署运行。系统会根据选定的模型自动配置请求参数。

## 许可证

MIT

## 贡献

欢迎提交问题和贡献代码，请通过创建Issue或Pull Request参与项目开发。

## 致谢

感谢所有为本项目提供支持和贡献的人员。