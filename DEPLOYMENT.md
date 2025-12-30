# Wiki 部署和协作编辑指南

本指南将帮助您部署 LM2 Group Wiki 并启用协作编辑功能。

> 📖 **另见**: [SETUP.md](SETUP.md) - 详细的 GitHub 仓库和 Netlify 配置指南

## 目录

- [部署到 GitHub Pages](#部署到-github-pages)
- [启用协作编辑](#启用协作编辑)
- [本地开发](#本地开发)

## 部署到 GitHub Pages

### 前提条件

确保您的 GitHub 仓库已经创建并推送了代码。

### 步骤 1: 启用 GitHub Pages

1. 进入 GitHub 仓库设置页面
2. 在左侧菜单中找到 **Pages**
3. 在 **Source** 下选择 **GitHub Actions**

### 步骤 2: 推送代码触发部署

当您推送代码到 `main` 分支时，GitHub Actions 会自动构建并部署您的 Wiki：

```bash
git add .
git commit -m "部署 Wiki"
git push origin main
```

### 步骤 3: 访问您的 Wiki

部署完成后，您可以在以下地址访问您的 Wiki：
`https://<username>.github.io/<repository>/`

例如：`https://TanHaonan.github.io/wiki2test/`

## 启用协作编辑

为了让其他人能够通过 Web 界面编辑 Wiki 内容，需要配置 Netlify Identity 和 Git Gateway。

### 步骤 1: 创建 Netlify 账户（如果还没有）

1. 访问 [Netlify](https://app.netlify.com/)
2. 使用 GitHub 账户登录

### 步骤 2: 创建新站点

1. 在 Netlify 控制台，点击 **Add new site** > **Import an existing project**
2. 选择 **Deploy with GitHub**
3. 授权 Netlify 访问您的 GitHub 仓库
4. 选择 `TanHaonan/wiki2test` 仓库
5. 使用以下构建设置：
   - **Build command**: `mkdocs build`
   - **Publish directory**: `site`
6. 点击 **Deploy site**

### 步骤 3: 启用 Netlify Identity

1. 在 Netlify 站点设置中，转到 **Identity**
2. 点击 **Enable Identity**

### 步骤 4: 配置 Git Gateway

1. 在 Identity 设置页面，向下滚动到 **Services** > **Git Gateway**
2. 点击 **Enable Git Gateway**
3. 这将允许 Netlify Identity 用户通过 CMS 界面编辑 GitHub 仓库

### 步骤 5: 配置注册选项

1. 在 Identity 设置中，转到 **Registration**
2. 选择 **Invite only**（仅邀请）或 **Open**（开放注册）
   - 建议选择 **Invite only** 以控制访问权限

### 步骤 6: 邀请用户

1. 在 **Identity** 标签中，点击 **Invite users**
2. 输入要邀请的用户邮箱地址
3. 用户将收到邀请邮件，可以设置密码并访问 CMS

### 步骤 7: 访问 CMS 管理界面

有两种方式访问 CMS：

1. **通过 Netlify 部署的站点**:
   - `https://<your-site-name>.netlify.app/admin/`

2. **通过 GitHub Pages**:
   - `https://<username>.github.io/<repository>/admin/`
   - 注意：需要在 GitHub Pages 部署的站点上加载 Netlify Identity widget

## 本地开发

### 安装依赖

```bash
pip install -r requirements.txt
```

### 启动开发服务器

```bash
mkdocs serve
```

访问 `http://127.0.0.1:8000` 查看本地预览。

### 本地测试 CMS

1. 安装 Decap CMS 后端服务器：

```bash
npx decap-server
```

2. 在另一个终端启动 MkDocs：

```bash
mkdocs serve
```

3. 访问 `http://127.0.0.1:8000/admin/` 进入 CMS 界面

## 使用 CMS 编辑内容

### 登录

1. 访问 `/admin/` 路径
2. 使用 Netlify Identity 凭据登录

### 编辑内容

1. 在左侧菜单选择要编辑的内容类型（项目进度、个人周报、会议记录等）
2. 点击现有条目进行编辑，或点击 **New [类型]** 创建新内容
3. 使用 Markdown 编辑器编写内容
4. 点击 **Publish** 发布更改

### 更改会发生什么

- CMS 会将您的更改作为 Git commit 提交到 GitHub 仓库
- GitHub Actions 会自动构建并部署更新后的 Wiki
- 几分钟后，您的更改将在线可见

## 故障排除

### CMS 无法加载

- 确保 Netlify Identity 和 Git Gateway 已启用
- 检查浏览器控制台是否有错误信息
- 确保您已登录 Netlify Identity

### 部署失败

- 检查 GitHub Actions 日志：仓库 > Actions 标签
- 确保 `requirements.txt` 中的所有依赖都正确安装
- 确保 GitHub Pages 已启用并设置为使用 GitHub Actions

### 权限问题

- 确保 Netlify 有权限访问您的 GitHub 仓库
- 在 GitHub 设置中检查已安装的应用程序

## 进阶配置

### 自定义域名

如果您有自定义域名：

1. 在 Netlify 站点设置中配置域名
2. 在 GitHub 仓库中添加 `CNAME` secret（如需要）
3. 更新 `mkdocs.yml` 中的 `site_url`

### 添加更多内容类型

编辑 `docs/admin/config.yml` 添加新的集合：

```yaml
collections:
  - name: "new_collection"
    label: "新集合"
    folder: "docs/new_folder"
    create: true
    slug: "{{slug}}"
    fields:
      - {label: "标题", name: "title", widget: "string"}
      - {label: "内容", name: "body", widget: "markdown"}
```

## 资源链接

- [MkDocs 文档](https://www.mkdocs.org/)
- [Material for MkDocs 文档](https://squidfunk.github.io/mkdocs-material/)
- [Decap CMS 文档](https://decapcms.org/docs/)
- [Netlify Identity 文档](https://docs.netlify.com/visitor-access/identity/)

## 支持

如有问题，请在 GitHub 仓库中创建 Issue。
