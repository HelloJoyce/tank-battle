# Git 工作流程文档

> 本文档记录了坦克大战项目从本地创建到推送到GitHub的完整Git操作流程。

---

## 📁 项目信息

- **项目名称**: tank-battle（坦克大战）
- **本地路径**: `D:\Desktop\tank_battle`
- **GitHub地址**: https://github.com/HelloJoyce/tank-battle.git
- **创建日期**: 2026/06/14

---

## 🚀 完整操作流程

### 第一步：初始化本地Git仓库

```bash
# 进入项目目录
cd D:\Desktop\tank_battle

# 初始化Git仓库（创建.git目录）
git init
```

**输出示例**:
```
Initialized empty Git repository in D:/Desktop/tank_battle/.git/
```

---

### 第二步：添加文件到暂存区

```bash
# 添加所有文件到暂存区（Staging Area）
git add .

# 或者添加指定文件
git add index.html
git add README.md
git add .gitignore
```

---

### 第三步：提交代码到本地仓库

```bash
# 提交并添加描述信息
git commit -m "Initial commit: 坦克大战游戏 v1.0"
```

**输出示例**:
```
[master (root-commit) 6d8520b] Initial commit: 坦克大战游戏 v1.0
 3 files changed, 677 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 README.md
 create mode 100644 index.html
```

> 💡 **提示**: `-m` 参数用于添加提交说明，应该清晰描述本次提交的内容。

---

### 第四步：在GitHub创建远程仓库

#### 方式A：使用GitHub CLI（命令行）⭐推荐

```bash
# 登录GitHub账号
gh auth login

# 创建公开仓库并自动关联推送
gh repo create tank-battle --public --source=. --remote=origin --push
```

参数说明：
- `--public`: 创建公开仓库
- `--source=.`: 使用当前目录作为源代码
- `--remote=origin`: 远程仓库别名为origin
- `--push`: 自动推送到远程

#### 方式B：手动在网页创建（本项目使用的方式）

1. 打开浏览器访问: https://github.com/new
2. 填写仓库信息：
   - **Repository name**: `tank-battle`
   - **Description**: `经典坦克大战游戏 - HTML5 Canvas`
   - **Public**: ✅ 选择公开
   - **Add a README file**: ❌ 不勾选（已有README）
   - **Add .gitignore**: ❌ 不勾选
   - **Choose a license**: ❌ 不勾选
3. 点击 **Create repository** 按钮

---

### 第五步：关联远程仓库

```bash
# 添加远程仓库地址（替换为你的用户名）
git remote add origin https://github.com/HelloJoyce/tank-battle.git
```

**验证远程仓库**:
```bash
git remote -v
```

**输出**:
```
origin  https://github.com/HelloJoyce/tank-battle.git (fetch)
origin  https://github.com/HelloJoyce/tank-battle.git (push)
```

---

### 第六步：重命名分支为main

```bash
# 将默认分支从master重命名为main（GitHub标准）
git branch -M main
```

---

### 第七步：推送到GitHub

```bash
# 推送到远程仓库的main分支
# -u 参数表示设置上游分支，后续可直接使用 git push
git push -u origin main
```

**输出示例**:
```
branch 'main' set up to track 'origin/main'.
To https://github.com/HelloJoyce/tank-battle.git
 * [new branch]      main -> main
```

🎉 **推送成功！**

---

## 📋 常用Git命令速查表

### 基础命令

| 命令 | 作用 |
|:---|:---|
| `git init` | 初始化本地Git仓库 |
| `git status` | 查看当前仓库状态 |
| `git add <文件名>` | 添加指定文件到暂存区 |
| `git add .` | 添加所有变更文件到暂存区 |
| `git commit -m "描述"` | 提交暂存区的文件 |
| `git log` | 查看提交历史 |
| `git log --oneline` | 查看简洁的提交历史 |

### 远程操作

| 命令 | 作用 |
|:---|:---|
| `git remote -v` | 查看已配置的远程仓库 |
| `git remote add origin <url>` | 添加远程仓库 |
| `git remote remove origin` | 删除远程仓库关联 |
| `git push -u origin main` | 推送到远程仓库 |
| `git push` | 推送到已设置上游的分支 |
| `git pull origin main` | 从远程拉取最新代码 |
| `git clone <url>` | 克隆远程仓库到本地 |

### 分支管理

| 命令 | 作用 |
|:---|:---|
| `git branch` | 查看本地分支列表 |
| `git branch -M main` | 重命名当前分支为main |
| `git checkout -b <分支名>` | 创建并切换到新分支 |
| `git checkout <分支名>` | 切换到指定分支 |
| `git merge <分支名>` | 合并指定分支到当前分支 |
| `git branch -d <分支名>` | 删除本地分支 |

---

## 🔧 常见问题处理

### 问题1：远程仓库已存在

**错误信息**:
```
fatal: remote origin already exists.
```

**解决方法**:
```bash
# 先删除旧的远程关联
git remote remove origin

# 再添加新的远程仓库
git remote add origin https://github.com/用户名/仓库名.git
```

---

### 问题2：分支名称不匹配

**错误信息**:
```
error: src refspec main does not match any
```

**解决方法**:
```bash
# 检查当前分支名
git branch

# 如果当前是master分支，重命名为main
git branch -M main

# 或者推送master分支
git push -u origin master
```

---

### 问题3：远程有更新需要先拉取

**错误信息**:
```
error: failed to push some refs to 'https://github.com/...'
```

**解决方法**:
```bash
# 先拉取远程更新（允许合并不相关历史）
git pull origin main --allow-unrelated-histories

# 解决可能的冲突后，再次推送
git push -u origin main
```

---

### 问题4：Windows换行符警告

**警告信息**:
```
warning: in the working copy of 'file', LF will be replaced by CRLF
```

**解决方法**:
```bash
# 配置Git自动处理换行符
git config --global core.autocrlf true
```

---

## 🌐 开启GitHub Pages（在线预览）

要让游戏可以通过网页直接访问，需要开启GitHub Pages：

1. 访问仓库设置页面：
   ```
   https://github.com/HelloJoyce/tank-battle/settings/pages
   ```

2. 配置Pages：
   - **Source**: 选择 `Deploy from a branch`
   - **Branch**: 选择 `main` / `/(root)`
   - 点击 **Save**

3. 等待1-2分钟部署完成

4. 访问地址：
   ```
   https://hellojoyce.github.io/tank-battle/
   ```

---

## 📝 后续更新代码流程

当修改了代码后，再次推送到GitHub：

```bash
# 1. 查看变更状态
git status

# 2. 添加修改的文件
git add .

# 3. 提交变更
git commit -m "描述本次修改的内容"

# 4. 推送到GitHub
git push
```

---

## 📚 学习资源

- [Git官方文档](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com/cn)
- [Git可视化学习](https://learngitbranching.js.org/?locale=zh_CN)

---

**文档创建时间**: 2026/06/14  
**适用项目**: tank-battle（坦克大战）  
**作者**: Claude Code
