# HTML版本使用说明

## 图片路径问题

HTML版本需要使用相对路径访问图片。请确保：

1. **如果直接双击打开**：图片路径使用 `public/photos/xxx.png`

2. **如果通过本地服务器访问**（推荐）：
   - 使用Python: `python -m http.server 8000`
   - 使用Node.js: `npx serve .`
   - 然后访问 `http://localhost:8000/index-html.html`
   - 此时图片路径可以使用 `/public/photos/xxx.png` 或 `./public/photos/xxx.png`

## 推荐使用方法

由于浏览器的安全限制，直接打开HTML文件（file://协议）可能无法加载图片。

**推荐方式：使用本地服务器**

### 方法1：使用Python（如果已安装）
```bash
python -m http.server 8000
```
然后访问：`http://localhost:8000/index-html.html`

### 方法2：使用Node.js serve
```bash
npx serve .
```
然后访问显示的地址 + `/index-html.html`

### 方法3：使用Vite（如果项目已配置）
```bash
npm run dev
```
然后将浏览器地址改为：`http://localhost:5173/index-html.html`


