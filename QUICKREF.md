# 快速参考卡

## 常用链接

### 生产环境
- 🌐 Wiki 网站: https://TanHaonan.github.io/wiki2test/
- ⚙️ CMS 管理: https://TanHaonan.github.io/wiki2test/admin/
- 📦 GitHub 仓库: https://github.com/TanHaonan/wiki2test

### Netlify（如已配置）
- 🌐 Netlify 站点: https://your-site-name.netlify.app/
- ⚙️ Netlify 管理: https://app.netlify.com/sites/your-site-name
- 👥 Identity 管理: https://app.netlify.com/sites/your-site-name/identity

## 本地开发命令

```bash
# 安装依赖
pip install -r requirements.txt

# 启动开发服务器
mkdocs serve

# 构建静态站点
mkdocs build

# 本地测试 CMS（需要先安装 Node.js）
npx decap-server
```

## Git 工作流

```bash
# 克隆仓库
git clone https://github.com/TanHaonan/wiki2test.git
cd wiki2test

# 创建新分支
git checkout -b feature/your-feature

# 添加更改
git add .
git commit -m "描述您的更改"

# 推送到远程
git push origin feature/your-feature

# 在 GitHub 上创建 Pull Request
```

## CMS 编辑工作流

### 方式 1: 通过 CMS 界面（推荐）

1. 访问 https://TanHaonan.github.io/wiki2test/admin/
2. 使用 Netlify Identity 登录
3. 选择内容类型（项目进度、周报等）
4. 编辑或创建新内容
5. 点击 **Publish** 发布
6. 等待 2-3 分钟，自动部署完成

### 方式 2: 直接编辑 Markdown 文件

1. 编辑 `docs/` 目录下的 `.md` 文件
2. 提交并推送到 `main` 分支
3. GitHub Actions 自动部署

## 目录结构

```
wiki2test/
├── docs/                      # 文档源文件
│   ├── admin/                # CMS 配置
│   │   ├── index.html       # CMS 入口页面
│   │   └── config.yml       # CMS 集合配置
│   ├── index.md             # 首页
│   ├── projects/            # 项目进度
│   ├── weekly_reports/      # 个人周报
│   ├── meetings/            # 会议记录
│   ├── research/            # 科研规划
│   ├── resources/           # 资源与规范
│   ├── assets/              # 静态资源
│   └── stylesheets/         # 自定义样式
├── overrides/               # 主题覆盖
│   └── main.html           # 自定义 HTML 模板
├── .github/workflows/       # GitHub Actions
│   └── deploy.yml          # 部署工作流
├── mkdocs.yml              # MkDocs 配置
├── requirements.txt        # Python 依赖
├── README.md               # 项目说明
├── DEPLOYMENT.md           # 部署指南
└── SETUP.md                # 仓库配置指南
```

## CMS 集合说明

| 集合名称 | 文件位置 | 用途 |
|---------|---------|------|
| 项目进度 | `docs/projects/` | 记录各项目的进展 |
| 个人周报 | `docs/weekly_reports/` | 团队成员的周报 |
| 会议记录 | `docs/meetings/` | 组会和讨论记录 |
| 科研规划 | `docs/research/` | 论文投稿计划等 |
| 资源与规范 | `docs/resources/` | 常用链接和规范 |
| 其他页面 | `docs/*.md` | 首页等特殊页面 |

## Markdown 语法快速参考

```markdown
# 一级标题
## 二级标题
### 三级标题

**粗体文本**
*斜体文本*

- 无序列表项
- 另一个列表项

1. 有序列表项
2. 另一个有序项

[链接文本](https://example.com)

![图片alt文本](assets/images/image.png)

`行内代码`

\```python
# 代码块
def hello():
    print("Hello, World!")
\```

> 引用块

---

水平分隔线

| 表头1 | 表头2 |
|------|------|
| 单元格 | 单元格 |
```

## 故障排除快速检查

### 部署失败

```bash
# 检查 GitHub Actions 状态
# 访问: https://github.com/TanHaonan/wiki2test/actions

# 本地测试构建
mkdocs build

# 检查依赖
pip install -r requirements.txt
```

### CMS 无法访问

1. ✅ Netlify Identity 已启用？
2. ✅ Git Gateway 已启用？
3. ✅ 用户已被邀请？
4. ✅ 浏览器允许第三方 Cookie？
5. ✅ 检查浏览器控制台错误？

### 页面显示异常

1. 清除浏览器缓存
2. 等待 GitHub Pages 缓存更新（可能需要几分钟）
3. 检查 Markdown 语法错误

## 获取帮助

- 📖 文档: [DEPLOYMENT.md](DEPLOYMENT.md)
- ⚙️ 配置: [SETUP.md](SETUP.md)
- 🐛 报告问题: https://github.com/TanHaonan/wiki2test/issues

## 有用的快捷键

### MkDocs Material 主题

- `/` 或 `s` - 打开搜索
- `Esc` - 关闭搜索/对话框
- `p` 或 `,` - 上一页
- `n` 或 `.` - 下一页

### CMS 界面

- `Ctrl/Cmd + S` - 保存草稿
- `Ctrl/Cmd + P` - 发布更改

## 维护任务

### 每周

- 审查新内容和更改
- 检查部署状态

### 每月

- 审查用户权限
- 更新依赖（如需要）
- 备份重要内容（Git 已提供版本控制）

### 每季度

- 审查和更新文档结构
- 清理不再使用的内容
- 性能优化
