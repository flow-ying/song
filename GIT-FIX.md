# Git连接问题解决方案

## 问题：无法连接到GitHub

如果遇到以下错误：
- `Could not resolve host: github.com.cnpmjs.org`
- `Connection was reset`
- `Failed to connect to github.com`

## 解决方案

### 方案1：使用SSH方式（推荐）

1. **生成SSH密钥**（如果还没有）
   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```
   按回车使用默认设置

2. **复制公钥**
   ```bash
   # Windows (PowerShell)
   cat ~/.ssh/id_ed25519.pub
   
   # 或者
   type C:\Users\你的用户名\.ssh\id_ed25519.pub
   ```

3. **添加到GitHub**
   - 访问：https://github.com/settings/keys
   - 点击 "New SSH key"
   - 粘贴公钥内容
   - 点击 "Add SSH key"

4. **修改远程仓库地址为SSH**
   ```bash
   git remote set-url origin git@github.com:flow-ying/song-tea-game.git
   ```

5. **测试连接**
   ```bash
   ssh -T git@github.com
   ```

6. **推送代码**
   ```bash
   git push -u origin main
   ```

### 方案2：配置代理（如果使用代理）

```bash
# 设置HTTP代理
git config --global http.proxy http://127.0.0.1:7890
git config --global https.proxy https://127.0.0.1:7890

# 如果使用SOCKS5代理
git config --global http.proxy socks5://127.0.0.1:7890
git config --global https.proxy socks5://127.0.0.1:7890

# 取消代理
git config --global --unset http.proxy
git config --global --unset https.proxy
```

### 方案3：使用GitHub CLI

1. **安装GitHub CLI**
   - 下载：https://cli.github.com/
   - 或使用包管理器安装

2. **登录**
   ```bash
   gh auth login
   ```

3. **推送**
   ```bash
   git push -u origin main
   ```

### 方案4：手动上传文件（临时方案）

如果网络问题持续：

1. 在GitHub仓库页面点击 "uploading an existing file"
2. 拖拽项目文件上传（注意不要上传 `node_modules` 文件夹）
3. 提交

### 方案5：检查网络连接

```bash
# 测试连接
ping github.com

# 测试HTTPS连接
curl -I https://github.com
```

## 已修复的配置

我已经帮你：
- ✅ 移除了GitHub镜像重定向配置
- ✅ 设置了正确的远程仓库地址：`https://github.com/flow-ying/song-tea-game.git`

## 当前状态

远程仓库已配置为：`https://github.com/flow-ying/song-tea-game.git`

如果仍然无法连接，建议：
1. **优先使用SSH方式**（方案1）- 最稳定
2. **或等待网络恢复后再试**
3. **或使用GitHub Desktop等图形工具**

