# LM2 Group Wiki

LM2 Research Group Documentation - 一个支持协作编辑的在线知识库。

## 🚀 快速开始

本项目使用 [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) 构建，并集成了 [Decap CMS](https://decapcms.org/) 实现协作编辑功能。

### 在线访问

- **Wiki 网站**: [https://TanHaonan.github.io/wiki2test/](https://TanHaonan.github.io/wiki2test/)
- **CMS 管理后台**: [https://TanHaonan.github.io/wiki2test/admin/](https://TanHaonan.github.io/wiki2test/admin/)

### 本地开发

```bash
# 安装依赖
pip install -r requirements.txt

# 启动开发服务器
mkdocs serve

# 访问 http://127.0.0.1:8000
```

## 📖 部署指南

详细的部署和协作编辑配置指南，请参阅 [DEPLOYMENT.md](DEPLOYMENT.md)。

该指南包括：
- 如何部署到 GitHub Pages
- 如何配置 Netlify Identity 和 Git Gateway
- 如何邀请用户协作编辑
- 本地开发和测试

## 📁 项目结构

```
.
├── docs/                    # 文档源文件
│   ├── admin/              # CMS 管理界面配置
│   ├── index.md            # 首页
│   ├── projects/           # 项目进度
│   ├── weekly_reports/     # 个人周报
│   ├── meetings/           # 会议记录
│   ├── research/           # 科研规划
│   └── resources/          # 资源与规范
├── mkdocs.yml              # MkDocs 配置文件
├── requirements.txt        # Python 依赖
└── .github/workflows/      # GitHub Actions 工作流
```

## ✨ 特性

- 📝 **Markdown 编写**: 使用 Markdown 格式编写文档
- 🎨 **Material Design**: 美观的 Material Design 主题
- 🔍 **全文搜索**: 内置强大的搜索功能
- 🌓 **深色模式**: 支持浅色/深色主题切换
- 👥 **协作编辑**: 通过 CMS 界面实现多人协作编辑
- 🚀 **自动部署**: GitHub Actions 自动构建和部署

## 📝 贡献

欢迎团队成员通过以下方式贡献内容：

1. **通过 CMS 界面**（推荐）:
   - 访问 `/admin/` 路径
   - 使用 Netlify Identity 登录
   - 直接在 Web 界面编辑内容

2. **通过 Git**:
   - Fork 本仓库
   - 创建特性分支
   - 提交 Pull Request

## 📄 许可

本项目仅供 LM2 研究组内部使用。
