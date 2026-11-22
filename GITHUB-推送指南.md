# GitHub 推送指南（手动操作）

> 这份指南帮你把本地仓库 `G:\ESP32-DevBoard` 挂到 GitHub。全程你自己操作，我不用你的 Token。

---

## 第一步：在 GitHub 官网创建空仓库

1. 打开 https://github.com/new （登录后）
2. **Repository name** 填：`esp32-devboard`（名字可以改，但后面命令里要一致）
3. **Description** 可以填：`ESP32 开发板硬件设计实战项目`
4. 选 **Public**（公开，方便以后给面试官看）
5. **不要勾** "Add a README file"、".gitignore"、"license" —— 全部留空
   - 原因：本地已经有这些文件，勾了会冲突
6. 点 **Create repository**

建完后页面会显示一段命令，先别管，用下面我给你的。

---

## 第二步：找到你的仓库地址

建好后，页面上有类似这样的地址：

```
https://github.com/你的用户名/esp32-devboard.git
```

复制这个地址，填进下面的命令。

---

## 第三步：在本地关联并推送

打开 **PowerShell**（或 Git Bash），执行下面三行：

```powershell
cd G:\ESP32-DevBoard
git remote add origin https://github.com/你的用户名/esp32-devboard.git
git branch -M main
git push -u origin main
```

逐行执行，每执行完一行看有没有报错。

### 每一行是什么意思

| 命令 | 作用 |
|---|---|
| `cd G:\ESP32-DevBoard` | 进入本地仓库目录 |
| `git remote add origin ...` | 告诉本地仓库"远程仓库在这个地址" |
| `git branch -M main` | 确保分支叫 main |
| `git push -u origin main` | 把本地内容推到远程，并建立跟踪关系 |

---

## 第四步：验证

打开你刚建的 GitHub 仓库页面，刷新。应该能看到：

- `README.md` 的内容显示在页面上
- `ESP32/` 文件夹和里面的 6 个子目录都在
- 提交记录显示 `init: ESP32开发板实战项目仓库`

看到这些就成功了。

---

## 常见问题

### 报错 `remote origin already exists`

说明之前已经关联过远程。先执行：

```powershell
git remote remove origin
```

然后再执行第三步的 `git remote add origin ...`。

### 报错 `Authentication failed` 或要求登录

GitHub 从 2021 年起**不再接受账号密码**推送，要用 Token：

1. 去 GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Generate new token (classic)，只勾 `public_repo` 权限，有效期设 90 天
3. 生成后复制 token（只显示一次）
4. 再执行 `git push` 时，用户名填你的 GitHub 用户名，密码**粘贴那个 token**

> 推送成功后这个 token 就可以删掉了。

### 报错 `failed to push some refs`

多半是建仓库时勾了 README。回到 GitHub 仓库页面，确认是空的；或者执行：

```powershell
git pull origin main --allow-unrelated-histories
git push -u origin main
```

### 中文乱码

本地文件夹是中文名，GitHub 上显示应该是正常的 UTF-8 中文。如果乱码，在 PowerShell 里先执行 `chcp 65001` 切换 UTF-8 编码再操作。

---

## 推送成功后告诉我

把 GitHub 仓库地址发我，我记进项目的文档里，以后每次更新都知道往哪推。
