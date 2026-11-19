# 第 4 步：建 GitHub 私有仓库并推送

为什么要用 GitHub：资料库放在网上，家里、公司的电脑和所有 AI 工具都能读到同一份；每次修改都有历史记录，不怕丢。

**仓库必须是私有的（Private）**，里面有用户自己和别人的个人信息。

用户可以选择**先跳过**这一步：资料库照样能用，只是数据只在这台电脑上。跳过时在 `设置.md` 里写“GitHub：未建”，并告诉他以后说“帮我建 GitHub 仓库”随时补上。

这一步里**登录 GitHub 必须用户自己操作**，AI 代替不了。密码和验证码不要让用户发给你。

## 1. 先检查

- 电脑上有没有 git：运行 `git --version`。没有的话，Mac 运行 `xcode-select --install`；Windows 让用户到 git-scm.com 下载安装，一路点“下一步”就行
- 有没有 GitHub CLI（`gh --version`），以及是否已经登录（`gh auth status`）

## 2. 建仓库

**有 gh 而且已登录**（最简单）：

```bash
cd <资料库文件夹>
git init && git add -A && git commit -m "初始化个人成长数据库"
gh repo create <仓库名> --private --source=. --push
```

仓库名默认 `my-growth-db`，问用户要不要改。

**没有 gh**：一步一步带用户在网页上建：

1. 打开 github.com，登录（没账号就先注册）
2. 右上角“+” → New repository
3. Repository name 填 `my-growth-db`，**选 Private**，其他都不勾，点 Create repository
4. 把页面上的仓库地址发给你（类似 `https://github.com/<用户名>/my-growth-db.git`）

然后你来运行：

```bash
cd <资料库文件夹>
git init && git add -A && git commit -m "初始化个人成长数据库"
git branch -M main
git remote add origin <仓库地址>
git push -u origin main
```

第一次推送会弹出登录窗口，让用户在窗口里登录 GitHub 授权。

## 3. 确认是私有的

推送后，让用户退出 GitHub 登录，或者用无痕窗口打开仓库地址，应该显示 404。能看到内容就说明是公开的，马上带他到仓库的 Settings → 最下面 Change visibility → 改成 Private。

## 常见问题

- **推送时要密码，输了 GitHub 密码却失败**：GitHub 不再支持用密码推送。装 GitHub CLI 后运行 `gh auth login` 按提示登录；或者用 GitHub Desktop 登录一次
- **提示 “rejected / fetch first”**：先 `git pull --rebase`，再 `git push`
- 更多问题见 `系统/常见问题.md`
