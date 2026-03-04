# 轨道交通知识服务系统

## 项目简介

轨道交通知识服务系统是一个基于 Vue 3 + FastAPI + Dify 的智能知识问答系统，旨在为用户提供轨道交通领域的专业知识查询和对话服务。

## 技术栈

### 前端
- Vue 3 + Vite
- Element Plus
- Vue Router
- Pinia
- Axios
- Marked (Markdown 渲染)
- KaTeX (数学公式)
- Highlight.js (代码高亮)

### 后端
- FastAPI
- SQLAlchemy
- JWT 认证
- Dify API 集成

## 快速开始

### 前置条件
- Node.js 18+
- Python 3.10+
- MySQL 数据库
- Dify 平台账号和 API Key

### 步骤 1: 克隆项目

```bash
git clone <repository-url>
cd rail-assistant
```

### 步骤 2: 配置后端环境

1. 进入后端目录并安装依赖

```bash
cd backend
python -m venv venv
source venv/bin/activate  # Windows 系统请使用 venv\Scripts\activate
pip install -r requirements.txt
```

2. 复制环境变量示例文件并修改

```bash
cp .env.example .env
```

在 `.env` 文件中填入以下信息：

```
# Dify 配置
DIFY_API_URL=<your-dify-api-url>
DIFY_API_KEY=<your-dify-api-key>
DIFY_KNOWLEDGE_API_KEY=<your-dify-knowledge-api-key>

# JWT 配置
JWT_SECRET=<your-jwt-secret>
JWT_ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30

# 数据库配置
DATABASE_URL=mysql+asyncmy://<username>:<password>@localhost:3306/<database-name>
```

### 步骤 3: 配置前端环境

1. 回到项目根目录并安装前端依赖

```bash
cd ..
npm install
```

### 步骤 4: 启动后端服务

```bash
cd backend
uvicorn app.main:app --reload --host 127.0.0.1 --port 8000
```

### 步骤 5: 启动前端服务

在另一个终端中执行：

```bash
cd rail-assistant
npm run dev
```

### 步骤 6: 访问系统

打开浏览器访问 `http://localhost:5173` 即可进入系统。

## 项目结构

```text
rail-assistant/
├── backend/                # FastAPI 后端
│   ├── app/                # 后端应用
│   │   ├── main.py         # FastAPI 入口
│   │   ├── config.py       # 配置文件
│   │   ├── db.py           # 数据库初始化
│   │   ├── routers/        # API 路由
│   │   ├── services/       # 业务逻辑
│   │   ├── models/         # 数据模型
│   │   └── deps/           # 依赖注入
│   ├── data/               # 数据存储
│   ├── .env.example        # 环境变量示例
│   ├── requirements.txt    # 依赖文件
│   └── run.bat             # 启动脚本
├── src/                    # Vue 前端
│   ├── api/                # API 调用
│   ├── assets/             # 静态资源
│   ├── router/             # 路由配置
│   ├── utils/              # 工具函数
│   ├── views/              # 页面组件
│   ├── App.vue             # 根组件
│   └── main.js             # 前端入口
├── docs/                   # 文档
├── public/                 # 公共资源
├── .gitignore              # Git 忽略文件
├── README.md               # 项目说明
├── index.html              # HTML 模板
├── package.json            # 前端依赖
└── vite.config.js          # Vite 配置
```

## 功能特性

### 1. 智能对话
- 基于 Dify 平台的智能问答
- 支持上下文对话
- 支持 Markdown 格式回复
- 支持代码高亮和数学公式

### 2. 知识库管理
- 文档上传功能
- 文档列表查看
- 文档删除功能
- 知识库检索

### 3. 用户管理
- 用户注册
- 用户登录
- JWT 认证
- 当前用户信息获取

## 接口说明

### 前端接口

#### 对话接口
- `POST /api/chat` - 发送消息并获取回复
- 请求体：`{ "message": string, "history": Array }`
- 响应体：`{ "success": true, "reply": string, "conversation_id": string | null, "error": null }`

#### 知识库接口
- `GET /api/knowledge/documents` - 获取文档列表
- `POST /api/knowledge/documents` - 上传文档（multipart/form-data）
- `DELETE /api/knowledge/documents/{id}` - 删除文档
- `POST /api/knowledge/query` - 知识库检索

#### 用户接口
- `POST /api/auth/register` - 用户注册
- `POST /api/auth/login` - 用户登录
- `GET /api/users/me` - 获取当前用户信息

### 后端接口

后端接口与前端接口一一对应，详细说明请参考 `backend/README.md` 文件。

## 注意事项

1. **端口配置**：前端 Vite 代理指向 `http://localhost:8000`，请确保后端服务使用端口 8000 启动。

2. **Dify 配置**：需要在 Dify 平台创建应用并获取 API Key，确保 Dify 应用配置正确。

3. **数据库配置**：需要配置 MySQL 数据库连接信息，确保数据库已创建。

4. **文件存储**：上传的文档存储在 `backend/data/documents/` 目录，请确保该目录存在且有写入权限。

5. **安全配置**：生产环境中请使用强密码和安全的 JWT 密钥。

## 开发指南

### 前端开发

- 启动开发服务器：`npm run dev`
- 构建生产版本：`npm run build`
- 预览生产版本：`npm run preview`

### 后端开发

- 启动开发服务器：`uvicorn app.main:app --reload --host 127.0.0.1 --port 8000`
- 健康检查：`curl http://localhost:8000/health`

## 部署指南

### 前端部署

1. 构建生产版本：

```bash
npm run build
```

2. 将 `dist` 目录部署到 Web 服务器（如 Nginx、Apache 等）。

### 后端部署

1. 安装依赖：

```bash
pip install -r requirements.txt
```

2. 启动生产服务器（推荐使用 Gunicorn）：

```bash
cd backend
gunicorn -w 4 -k uvicorn.workers.UvicornWorker app.main:app --bind 0.0.0.0:8000
```

3. 配置反向代理（如 Nginx）指向后端服务。

## 许可证

MIT License

## 联系方式

如有问题，请联系项目维护者。