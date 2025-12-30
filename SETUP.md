# GitHub 仓库配置指南

本文档介绍如何配置 GitHub 仓库以支持自动部署和协作编辑。

## 必需的仓库设置

### 1. 启用 GitHub Pages

1. 进入仓库设置: `Settings` > `Pages`
2. 在 **Source** 部分:
   - 选择 **GitHub Actions** 作为源

### 2. 配置分支保护（可选但推荐）

1. 进入 `Settings` > `Branches`
2. 添加分支保护规则:
   - Branch name pattern: `main`
   - 启用 "Require a pull request before merging"（可选）
   - 启用 "Require status checks to pass before merging"（可选）

### 3. 验证 GitHub Actions 权限

1. 进入 `Settings` > `Actions` > `General`
2. 在 **Workflow permissions** 部分:
   - 选择 "Read and write permissions"
   - 勾选 "Allow GitHub Actions to create and approve pull requests"

这样 GitHub Actions 才能部署到 gh-pages 分支。

## 自动部署工作流

仓库已配置 GitHub Actions 工作流 (`.github/workflows/deploy.yml`)，它将：

1. 当代码推送到 `main` 分支时自动触发
2. 安装 Python 依赖
3. 构建 MkDocs 站点
4. 部署到 GitHub Pages

### 手动触发部署

您也可以手动触发部署：

1. 进入 `Actions` 标签
2. 选择 "Deploy MkDocs to GitHub Pages" 工作流
3. 点击 "Run workflow"

## Netlify 配置（用于协作编辑）

### 前提条件

- Netlify 账户（使用 GitHub 登录）
- 仓库必须授权给 Netlify

### 创建 Netlify 站点

1. 登录 [Netlify](https://app.netlify.com/)
2. 点击 "Add new site" > "Import an existing project"
3. 选择 "Deploy with GitHub"
4. 选择 `TanHaonan/wiki2test` 仓库
5. 构建设置：
   ```
   Build command: mkdocs build
   Publish directory: site
   ```
6. 点击 "Deploy site"

### 配置 Netlify Identity

1. 在 Netlify 站点仪表板，进入 `Site settings` > `Identity`
2. 点击 "Enable Identity"

### 配置 Git Gateway

1. 在 Identity 设置页面，滚动到 "Services"
2. 点击 "Git Gateway" 下的 "Enable Git Gateway"
3. 选择 GitHub 作为 OAuth provider（如果尚未配置）

### 设置注册选项

建议设置为仅邀请模式：

1. 在 `Site settings` > `Identity` > `Registration`
2. 选择 "Invite only"

### 配置邮件模板（可选）

1. 在 `Site settings` > `Identity` > `Emails`
2. 自定义邀请邮件模板

## 邀请协作者

1. 进入 Netlify 站点的 `Identity` 标签
2. 点击 "Invite users"
3. 输入用户的邮箱地址
4. 用户将收到邀请邮件
5. 用户点击邮件中的链接设置密码
6. 完成后，用户可以访问 `/admin/` 并使用 Netlify Identity 登录

## CMS 访问地址

协作者可以通过以下地址访问 CMS：

- **通过 GitHub Pages**: `https://TanHaonan.github.io/wiki2test/admin/`
- **通过 Netlify**: `https://your-site-name.netlify.app/admin/`

## 工作流程

### 通过 CMS 编辑内容

1. 访问 `/admin/`
2. 使用 Netlify Identity 登录
3. 选择要编辑的内容类型
4. 编辑或创建新内容
5. 点击 "Publish" 发布

### 后台发生的事情

1. Decap CMS 通过 Git Gateway 将更改提交到 GitHub
2. 提交触发 GitHub Actions 工作流
3. 工作流构建并部署新版本
4. 几分钟后，更改在两个站点上都可见：
   - GitHub Pages: `https://TanHaonan.github.io/wiki2test/`
   - Netlify: `https://your-site-name.netlify.app/`

## 故障排除

### 部署失败

检查 GitHub Actions 日志：
1. 进入仓库的 `Actions` 标签
2. 查看失败的工作流运行
3. 检查错误信息

常见问题：
- 依赖安装失败：检查 `requirements.txt`
- 权限错误：确认 Actions 有写入权限
- 构建错误：检查 Markdown 文件语法

### CMS 无法访问

1. 确认 Netlify Identity 已启用
2. 确认 Git Gateway 已启用
3. 确认用户已被邀请并接受邀请
4. 检查浏览器控制台错误

### 推送权限问题

1. 在 GitHub，进入 `Settings` > `Applications` > `Installed GitHub Apps`
2. 找到 "Netlify" 应用
3. 确认仓库访问权限已授予

## 高级配置

### 自定义域名

如果使用自定义域名：

1. 在 GitHub Pages 设置中配置域名
2. 在 Netlify 中也配置相同域名
3. 更新 `mkdocs.yml` 中的 `site_url`
4. 如需要，添加 GitHub secret `CNAME`

### 添加更多 CMS 集合

编辑 `docs/admin/config.yml` 添加新集合：

```yaml
collections:
  - name: "collection_name"
    label: "显示名称"
    folder: "docs/folder_name"
    create: true
    slug: "{{slug}}"
    fields:
      - {label: "标题", name: "title", widget: "string"}
      - {label: "内容", name: "body", widget: "markdown"}
```

提交更改后，新集合将出现在 CMS 界面中。

## 安全建议

1. 使用仅邀请模式限制 CMS 访问
2. 定期审查有权限的用户
3. 对于敏感信息，考虑使用私有仓库
4. 启用分支保护以防止直接推送到 main 分支

## 支持资源

- [GitHub Pages 文档](https://docs.github.com/en/pages)
- [GitHub Actions 文档](https://docs.github.com/en/actions)
- [Netlify Identity 文档](https://docs.netlify.com/visitor-access/identity/)
- [Decap CMS 文档](https://decapcms.org/docs/)

## 获取帮助

如遇到问题，请在 GitHub 仓库中创建 Issue，并提供：
- 错误描述
- 错误日志或截图
- 重现步骤
