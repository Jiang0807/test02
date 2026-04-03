# 🔄 GitHub 网页更新指南

> 每次在相册网页上添加/修改了内容后，用以下步骤同步到 GitHub Pages

---

## 📌 核心原理（先搞懂这个）

```
你的电脑（本地）  ←→  GitHub（远程）
    ↓                    ↓
  编辑HTML文件        托管网页
  上传照片到localStorage →  GitHub Pages 自动部署
```

⚠️ **关键点**：当前版本的相册用的是 **localStorage** 存储照片，
这意味着：

| 数据类型 | 存储位置 | 能否通过 Git 推送到 GitHub |
|---------|---------|------------------------|
| HTML/CSS/JS 代码 | 本地文件 | ✅ 可以 |
| 通过上传按钮添加的照片 | 浏览器 localStorage | ❌ 不能直接推送 |

所以有两种情况需要区分处理：

---

## 方案一：只更新代码（没改照片）

如果你只是修改了代码（比如改文字、调样式），直接推就行：

```bash
# 1. 进入项目目录
cd /Users/nidexiaobaobaozhengzaishuruzhong/WorkBuddy/20260403215351

# 2. 查看哪些文件改了
git status

# 3. 添加修改的文件
git add growth-album-design.html

# 4. 提交更改
git commit -m "🎨 更新相册样式/功能"

# 5. 推送到 GitHub
git push
```

> 推送后约 1-2 分钟，GitHub Pages 会自动更新 ✅

---

## 方案二：添加了新照片（最常见的情况！）

因为照片存在浏览器的 localStorage 里，**不在本地文件中**，
所以需要先「导出」再推送。我来帮你加一个导出功能！

### 操作步骤：

#### 第 1 步：打开网页，点击导出

在相册网页上，我会帮你加上一个 **「导出数据」** 按钮：
- 点击后把所有照片和配置打包成一个 JSON 文件
- 文件会自动下载到你的电脑上

#### 第 2 步：把导出的数据放到项目中

```bash
# 在项目目录下创建数据文件夹
mkdir -p photos-data

# 把下载的 JSON 文件移动进去
mv ~/Downloads/album-data.json ./photos-data/
```

#### 第 3 步：推送到 GitHub

```bash
git add .
git commit -m "📸 新增照片数据"
git push
```

---

## ⚡ 最推荐的方式：一键脚本

我把上面的步骤写成一个自动化脚本，以后每次更新只需运行一条命令！

### 创建更新脚本

```bash
cat > update-github.sh << 'EOF'
#!/bin/bash
echo "🚀 开始更新 GitHub Pages..."
cd /Users/nidexiaobaobaozhengzaishuruzhong/WorkBuddy/20260403215351

# 添加所有改动
git add -A

# 检查是否有变更
if git diff --cached --quiet; then
    echo "✅ 没有新的变更，无需更新"
else
    # 提交并推送
    git commit -m "📝 相册更新 - $(date '+%Y-%m-%d %H:%M')"
    git push
    echo "🎉 推送成功！等待1-2分钟让 GitHub Pages 部署完成"
fi
EOF

chmod +x update-github.sh
```

### 以后每次更新只需要：

```bash
./update-github.sh
```

搞定！一条命令全搞定 🎉

---

## 📋 完整操作流程图

```
┌─────────────────────────────────────────────┐
│           你的日常操作流程                     │
├─────────────────────────────────────────────┤
│                                             │
│  ① 打开相册网页                               │
│     ↓                                       │
│  ② 点击「上传照片」→ 选择月份 → 拖入照片         │
│     ↓                                       │
│  ③ 确认添加 ✓                                │
│     ↓                                       │
│  ④ （可选）点击「导出数据」保存备份              │
│     ↓                                       │
│  ⑤ 打开终端运行：                             │
│     $ ./update-github.sh                     │
│     ↓                                       │
│  ⑥ 完成！等1-2分钟后访问最新网站                │
│                                             │
└─────────────────────────────────────────────┘
```

---

## 🔧 常见问题

### Q1：推送时提示 "nothing to commit"？
**A：** 说明文件没有变化。可能你只是在浏览器里上传了照片（存在localStorage），
但本地 HTML 文件本身没有改过。这种情况下需要先「导出数据」（见方案二）。

### Q2：推送后网站还是旧的？
**A：** 正常！GitHub Pages 部署需要 1-3 分钟。
你可以在这里查看部署状态：
```
仓库页面 → Actions → 查看构建进度
```
或者去 Settings → Pages 页面查看部署状态。

### Q3：想同时保留 localStorage 和 GitHub 版本？
**A：** 建议的流程：
1. 平时正常使用网页上传（存在浏览器里，速度快）
2. 定期（比如每周/每月）点一次「导出数据」+ `git push` 做备份
3. 这样即使换电脑/清浏览器数据，也能从 GitHub 恢复

### Q4：照片太多，JSON 文件太大怎么办？
**A：** 如果照片总量超过 100MB：
- GitHub 单文件限制是 100MB
- 建议使用 Git LFS (Large File Storage)
- 或者考虑升级为云存储方案（如阿里云 OSS、腾讯云 COS）

---

## 📱 快捷命令速查表

| 命令 | 作用 |
|------|------|
| `cd /Users/nidexi.../20260403215351` | 进入项目目录 |
| `git status` | 查看哪些文件变了 |
| `git add -A` | 添加所有改动 |
| `git commit -m "说明"` | 提交更改 |
| `git push` | 推送到 GitHub |
| `./update-github.sh` | 一键更新（推荐）|
| `git log --oneline -5` | 查看最近5次提交记录 |

---

## 💡 进阶技巧

### 设置 Git 别名（更懒更爽）

```bash
# 一行命令设置常用别名
git config --global alias.ac '!f() { git add -A && git commit -m "$1"; }; f'
git config --global alias.pushy 'push origin main'
```

之后就可以这样用：
```bash
git ac "更新照片"    # = git add -A + git commit
git pushy            # = git push origin main
```

两行搞定更新 😎

---

有问题随时问我！
