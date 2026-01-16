# NL-Mesh-Inspect 系统架构

## 系统概述

NL-Mesh-Inspect 是一个自然语言驱动的 3D 模型分析与检测平台，允许用户通过自然语言指令与 3D 模型进行交互。

## 核心架构层次

### 1. 前端展示层 (UI/UX Layer)
**技术栈**: React + Three.js + TypeScript

**主要组件**:
- `App.tsx` - 应用主入口，协调各组件
- `components/ModelViewer.tsx` - 3D 模型查看器 (Three.js)
- `components/ChatInterface.tsx` - 自然语言聊天界面
- `components/FileUpload.tsx` - STL 文件上传组件
- `hooks/useThreeScene.ts` - Three.js 场景管理 Hook
- `hooks/useApi.ts` - API 调用封装 Hook

**职责**:
- 提供直观的 3D 模型可视化
- 处理用户输入和交互
- 显示 AI 分析结果和特征高亮

### 2. 语义解析层 (NLP Engine Layer)
**技术栈**: Python + FastAPI + OpenAI GPT-4o

**主要模块**:
- `api/main.py` - FastAPI 应用入口
- `api/routes/upload.py` - 文件上传和解析路由
- `api/routes/analysis.py` - 模型分析路由
- `api/services/ai_service.py` - AI 服务封装
- `api/services/geometry_service.py` - 几何处理服务
- `api/models/stl_model.py` - STL 模型数据模型

**职责**:
- 解析用户自然语言指令
- 调用几何算法进行模型分析
- 生成结构化的特征描述

### 3. 几何处理层 (Geometry Processing Layer)
**技术栈**: Python + Trimesh

**主要功能**:
- STL 文件解析和验证
- 基础几何特征检测 (平面、圆柱面、边界)
- 尺寸测量和统计分析
- 空间关系分析

### 4. 数据流架构

```
用户输入 → 前端界面 → API调用 → 几何分析 → AI处理 → 结果返回 → 3D高亮
```

## 关键设计决策

### 前后端分离架构
- **优势**: 前端专注于交互体验，后端专注于计算密集型任务
- **通信**: RESTful API + WebSocket (未来扩展)

### 模块化设计
- 每个功能模块职责单一，便于测试和维护
- 清晰的接口定义，支持功能扩展

### 错误处理策略
- 前端: 用户友好的错误提示
- 后端: 详细的日志记录和异常处理
- AI服务: 降级策略，确保基础功能可用

## 性能考虑

### 前端优化
- Three.js 场景优化 (LOD、视锥体剔除)
- 异步操作避免界面卡顿
- 模型数据的分块加载

### 后端优化
- 几何计算的异步处理
- 结果缓存机制
- 大文件的分片处理

## 扩展性设计

### 插件化架构
- 几何检测算法可插拔
- AI 模型可替换
- 文件格式支持可扩展

### API 设计原则
- 遵循 RESTful 规范
- 版本化 API 端点
- 清晰的错误码体系