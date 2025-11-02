# 宋韵百茶戏

一个展示宋代点茶工艺的图片浏览应用。

## 项目结构

- **Vue版本**：使用Vue 3 + Vite构建的现代化应用
- **HTML版本**：纯HTML文件，无需构建，可直接使用

## 本地开发

### Vue版本
```bash
# 安装依赖
npm install

# 启动开发服务器
npm run dev

# 构建生产版本
npm run build
```

### HTML版本
直接打开 `public/index.html` 或通过本地服务器访问

## GitHub Pages 部署

### 方法一：部署HTML版本（推荐，最简单）

1. **创建GitHub仓库**
   - 在GitHub上创建新仓库（如：`song-tea-game`）

2. **初始化并上传代码**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/你的用户名/仓库名.git
   git push -u origin main
   ```

3. **配置GitHub Pages**
   - 进入仓库 Settings → Pages
   - Source 选择 "Deploy from a branch"
   - Branch 选择 `main`
   - Folder 选择 `/public`
   - 点击 Save

4. **访问网站**
   - 等待几分钟后，访问：`https://你的用户名.github.io/仓库名/`
   - 或者访问：`https://你的用户名.github.io/仓库名/index.html`

### 方法二：部署Vue构建版本

1. **构建项目**
   ```bash
   npm run build
   ```

2. **配置Vite输出目录**
   确保 `vite.config.js` 中 `base` 设置为仓库路径：
   ```js
   export default defineConfig({
     base: '/仓库名/',
     // ...
   })
   ```

3. **部署dist目录**
   - 将 `dist` 目录的内容推送到 `gh-pages` 分支
   - 或使用 GitHub Actions 自动部署

### 方法三：使用GitHub Actions自动部署

创建 `.github/workflows/deploy.yml`：

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]
  workflow_dispatch:

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      
      - name: Install dependencies
        run: npm install
      
      - name: Build
        run: npm run build
      
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
```

## 项目文件说明

- `index.html` - Vue应用入口
- `src/App.vue` - Vue主组件（图片浏览）
- `public/index.html` - 纯HTML版本
- `public/photos/` - 图片资源目录

## 功能特性

- ✅ 10张图片顺序浏览
- ✅ 左右箭头切换
- ✅ 键盘方向键支持
- ✅ 移动端和PC端完美适配
- ✅ 响应式布局


