# 🌐 成长相册 GitHub Pages 上传指南

> 把小朋友的成长相册网页发布到 GitHub Pages，免费托管，全世界都能访问！

---

## 📋 整体流程（3步搞定）

```
1️⃣ 初始化 Git 仓库 → 2️⃣ 推送到 GitHub → 3️⃣ 开启 GitHub Pages
```

---

## 第一步：初始化 Git 并推送

### 1. 打开终端，进入项目目录

```bash
cd /Users/nidexiaobaobaozhengzaishuruzhong/WorkBuddy/20260403215351
```

### 2. 初始化 Git 仓库

```bash
git init
```

### 3. 把所有文件添加到暂存区

```bash
git add growth-album-design.html
```

> 💡 **提示**：如果你之后还会加照片或其他文件，可以用 `git add .` 添加全部文件。

### 4. 创建首次提交

```bash
git commit -m "🎉 初始化成长相册网页"
```

### 5. 关联你的 GitHub 远程仓库

```bash
git remote add origin https://github.com/<你的用户名>/<你的仓库名>.git
```

> 🔑 把 `<你的用户名>` 和 `<你的仓库名>` 替换成你自己的。
> 
> 例如：`https://github.com/xiaoming/baby-album.git`

### 6. 推送到 GitHub

```bash
git branch -M main
git push -u origin main
```

> ⚠️ 第一次推送时可能会弹出登录窗口，按提示输入你的 GitHub 账号密码/Token 即可。

---

## 第二步：开启 GitHub Pages（超关键！）

### 方法一：通过 GitHub 网页设置（推荐 ✅）

1. 打开浏览器，访问你的仓库页面：
   ```
   https://github.com/<你的用户名>/<你的仓库名>
   ```

2. 点击仓库页面上方的 **「Settings」** 标签（最后一个）

3. 在左侧菜单中找到 **「Pages」** 选项，点击它

4. 在 **Source** 部分：
   - 将 `Deploy from a branch` 保持选中
   - **Branch** 选择 `main`
   - **Folder** 选择 `/ (root)` （根目录）
   
5. 点击 **「Save」** 按钮

6. 等待大约 1-2 分钟，页面顶部会显示：
   ```
   🎉 Your site is ready to be published at https://<你的用户名>.github.io/<你的仓庛名>/
   ```

### 方法二：用命令行创建 gh-pages 分支

如果你想部署到 `gh-pages` 分支：

```bash
git checkout -b gh-pages
git push origin gh-pages
```

然后在 GitHub Settings → Pages 中选择 Branch 为 `gh-pages`。

---

## 第三步：访问你的网站！🎉

部署成功后，你的相册地址是：

```
https://<你的用户名>.github.io/<你的仓库名>/
```

例如用户名是 `xiaoming`、仓库名是 `baby-album`：
```
https://xiaoming.github.io/baby-album/
```

把这个链接发给家人朋友，他们就能看到小朋友的可爱成长记录啦！💕

---

## 📸 后续如何更新照片？

### 日常添加新照片后，只需三步：

```bash
# 1. 添加修改的文件
git add .

# 2. 写提交信息
git commit -m "📸 新增第X个月照片"

# 3. 推送到 GitHub（自动触发 Pages 更新）
git push
```

> 推送完成后，GitHub Pages 会自动重新部署，通常 1-2 分钟后网站就更新了。

---

## 🔧 常见问题 FAQ

### Q：推送时提示 "Authentication failed" 怎么办？
**A：** 需要配置 GitHub Personal Access Token：
1. GitHub → Settings → Developer settings → Personal access tokens → Generate new token
2. 勾选 `repo` 权限
3. 生成 Token 后，推送时密码填这个 Token

### Q：网站显示 404？
**A：** 检查以下几点：
- 确认 Settings → Pages 中 Branch 选的是 `main`，Folder 是 `/ (root)`
- 等待 2-3 分钟让部署完成
- 确认仓库名拼写正确

### Q：中文文件名会不会有问题？
**A：** 建议照片文件名用英文或数字命名，如 `month-01-photo-01.jpg`，避免中文路径在服务器上出现编码问题。

### Q：想用自己的域名？
**A：** 在 Settings → Pages 的 Custom domain 中填写你的域名，然后在域名 DNS 添加 CNAME 记录指向 `<用户名>.github.io` 即可。

### Q：GitHub Pages 免费吗？有流量限制吗？
**A：** **完全免费！** 公开仓库的 GitHub Pages 没有流量限制，带宽也是免费的。对于个人家庭相册来说完全够用。

---

## 📁 建议的项目文件结构

```
your-repo/
├── index.html              ← 把 growth-album-design.html 改名为 index.html 更方便访问
├── photos/                 ← 照片文件夹
│   ├── month-01/           ← 第1个月的照片
│   │   ├── 01.jpg
│   │   ├── 02.jpg
│   │   └── ...
│   ├── month-02/
│   │   └── ...
│   └── month-38/
│       └── ...
├── css/                    ← 样式文件（如果拆分的话）
├── js/                     ← JavaScript 文件（如果拆分的话）
└── README.md               ← 项目说明文件
```

> 💡 **小建议**：把 `growth-album-design.html` 改名为 `index.html`，这样访问地址更简洁，直接就是根路径！

---

## ✅ 操作清单 Checklist

- [ ] 已确认 GitHub 仓库地址
- [ ] 终端进入项目目录并执行 `git init`
- [ ] 执行 `git add` 和 `git commit`
- [ ] 执行 `git remote add origin` 关联远程仓库
- [ ] 执行 `git push -u origin main` 推送代码
- [ ] GitHub 网页上 Settings → Pages 开启部署
- [ ] 访问 Pages 地址确认网站正常
- [ ] 把链接分享给家人朋友 ❤️

---

祝你上传顺利！有问题随时问我 😊
