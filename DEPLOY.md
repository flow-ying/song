# GitHub Pages 部署详细步骤

## 前置准备

1. **安装Git**（如果还没安装）
   - 下载：https://git-scm.com/downloads
   - 安装后打开Git Bash或命令提示符

2. **注册GitHub账号**（如果还没有）
   - 访问：https://github.com
   - 注册并登录

## 步骤1：在GitHub创建仓库

1. 登录GitHub
2. 点击右上角 `+` → `New repository`
3. 填写仓库信息：
   - Repository name: `song-tea-game`（或你喜欢的名字）
   - Description: `宋韵百茶戏 - 宋代点茶工艺展示`
   - 选择 Public（GitHub Pages需要公开仓库）
   - **不要**勾选 README、.gitignore、license
4. 点击 `Create repository`

## 步骤2：初始化本地Git仓库并上传

在项目目录（`C:\Users\flowying\Desktop\song`）执行以下命令：

```bash
# 初始化Git仓库
git init

# 添加所有文件
git add .

# 提交文件
git commit -m "Initial commit: 宋韵百茶戏项目"

# 添加远程仓库（替换为你的仓库地址）
git remote add origin https://github.com/你的用户名/仓库名.git

# 推送到GitHub
git branch -M main
git push -u origin main
```

**注意**：
- 首次推送可能需要输入GitHub用户名和密码（或使用Personal Access Token）
- 如果遇到认证问题，参考GitHub文档设置SSH密钥或Personal Access Token

## 步骤3：配置GitHub Pages

### 方法A：使用public目录（推荐，最简单）

1. 在GitHub仓库页面，点击 `Settings`
2. 左侧菜单找到 `Pages`
3. 在 `Source` 部分：
   - 选择 `Deploy from a branch`
   - Branch: 选择 `main`
   - Folder: 选择 `/public`
   - 点击 `Save`
4. 等待1-2分钟，GitHub会显示你的网站地址：
   ```
   https://你的用户名.github.io/仓库名/
   ```

### 方法B：部署Vue构建版本

如果需要部署Vue版本（需要构建）：

1. **修改 `vite.config.js`**
   ```js
   import { defineConfig } from 'vite'
   import vue from '@vitejs/plugin-vue'

   export default defineConfig({
     base: '/仓库名/',  // 改为你的仓库名，如 '/song-tea-game/'
     plugins: [vue()],
     server: {
       port: 5173,
       strictPort: false,
       hmr: {
         overlay: true
       }
     }
   })
   ```

2. **构建项目**
   ```bash
   npm run build
   ```

3. **部署dist目录**
   
   方法1：手动部署
   ```bash
   # 进入dist目录
   cd dist
   
   # 初始化git（如果还没有）
   git init
   git add .
   git commit -m "Deploy to GitHub Pages"
   
   # 推送到gh-pages分支
   git branch -M gh-pages
   git remote add origin https://github.com/你的用户名/仓库名.git
   git push -u origin gh-pages
   ```
   
   方法2：使用GitHub Actions（自动部署）
   - 参考 README.md 中的 GitHub Actions 配置

## 步骤4：访问你的网站

部署成功后（等待1-2分钟），访问：
- **HTML版本**：`https://你的用户名.github.io/仓库名/` 或 `https://你的用户名.github.io/仓库名/index.html`
- **Vue版本**：`https://你的用户名.github.io/仓库名/`（如果配置了base路径）

## 常见问题

### 1. 图片不显示
- 检查图片路径是否正确
- 确保 `public/photos/` 目录已上传
- 检查GitHub Pages的Folder设置是否为 `/public`

### 2. 404错误
- 检查仓库的Pages设置
- 确认分支和文件夹设置正确
- 等待几分钟让GitHub更新

### 3. 样式不正常
- 清除浏览器缓存（Ctrl+F5）
- 检查控制台是否有错误

### 4. 推送代码时认证失败
- 使用Personal Access Token代替密码
- 或配置SSH密钥
- 参考：https://docs.github.com/en/authentication

## 更新网站

每次修改代码后，只需：

```bash
git add .
git commit -m "更新描述"
git push
```

GitHub Pages会自动重新部署（通常需要1-2分钟）。

## 推荐方案

**最简单方案**：直接使用 `public/index.html`
- 无需构建
- 直接部署
- 访问速度快
- 配置简单


