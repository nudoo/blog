---
title: Git 简明指南
date: 2026-03-05 00:50:40
author: moea
summary: git config # 初始化本地git仓库（创建新仓库）
img: https://i.loli.net/2018/07/30/5b5f2f319a4c8.jpg
categories: 开发工具
tags:
  - git
---

# Git 简明指南

## 1 安装 Git

使用 Scoop 在 Windows 上安装：

```bash
scoop install git
```

## 2 基本配置

### 2.1 代理（可选）

示例：使用 socks5 或 http 代理（请根据本地代理端口调整）：

```bash
git config --global http.proxy socks5://127.0.0.1:10808
git config --global https.proxy socks5://127.0.0.1:10808

git config --global http.proxy http://127.0.0.1:10809
git config --global https.proxy https://127.0.0.1:10809

# 查看配置
git config -l
```

> 注意：命令中的 `--global` 使用两个短横（`-`），避免使用长破折号或其他字符。

### 2.2 用户信息

```bash
git config --global user.name "你的GitHub用户名"
git config --global user.email "你的GitHub邮箱"
```

### 2.3 SSH 方式（推荐）

1) 生成 SSH 密钥（推荐 ed25519 算法）：

```bash
ssh-keygen -t ed25519 -C "你的GitHub邮箱"
```

在生成时可按回车使用默认路径（Linux/macOS: `~/.ssh`，Windows: `C:\Users\你的用户名\\.ssh\\`），并可选择设置 passphrase 提高安全性。

2) 启动 ssh-agent 并添加私钥（以 Git Bash 为例）：

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

（Windows 上也可使用 `ssh-agent` 服务或 Git Credential Manager 的 SSH 支持，或使用 Pageant/Putty 等工具。）

3) 将公钥复制到 GitHub：

```bash
cat ~/.ssh/id_ed25519.pub
```

登录 GitHub -> Settings -> SSH and GPG keys -> New SSH key，粘贴公钥并保存。

4) 测试连接：

```bash
ssh -T git@github.com
```

成功示例："Hi <你的用户名>! You've successfully authenticated..."

### 2.4 HTTPS 方式

从仓库页面点击 "Code" -> 选择 HTTPS -> 复制地址并 `git clone`。

从 2021 年起，GitHub 要求使用个人访问令牌（PAT）替代账户密码进行推送认证。

生成 PAT：GitHub -> Settings -> Developer settings -> Personal access tokens（选择需要的权限，如 `repo`）。

推荐在 Windows 上启用凭证管理器以缓存凭据：

```bash
git config --global credential.helper manager-core
```

### 2.5 已用 HTTPS 克隆，改为 SSH 推送

在本地仓库目录下：

```bash
git remote set-url origin git@github.com:用户名/仓库名.git
```

## 3 常用操作示例

```bash
# 查看状态
git status

# 添加更改并提交
git add .
git commit -m "提交说明"

# 拉取远程更新
git pull origin 分支名

# 推送到远程分支
git push origin 分支名
```

## 4 建议补充项（建议在文档中增加）

- **凭证管理**：说明 `credential.helper manager-core`（Windows）或 `cache`（Linux）用法。
- **core.autocrlf**：在 Windows 上推荐 `git config --global core.autocrlf true`，在 macOS/Linux 上推荐 `git config --global core.autocrlf input`，避免换行符问题。
- **全局 .gitignore**：如何配置 `~/.gitignore_global` 并设置 `git config --global core.excludesfile ~/.gitignore_global`。
- **默认分支名称**：如何设置 `init.defaultBranch`（例如 `main`）：

```bash
git config --global init.defaultBranch main
```

- **pull 策略**：`git config --global pull.rebase false|true|merges` 的含义与推荐值。
- **SSH agent 在 Windows 的注意事项**：如何启用 `ssh-agent` 服务并确保存储私钥。
- **GPG 签名提交**：简单说明如何生成 GPG 密钥并启用 `commit.gpgSign`。
- **常用工作流**：分支（feature/main/release）、PR 流程、合并或 rebase 的简要说明。
- **冲突解决 & 回滚**：常见 `git merge` 冲突处理、`git revert` 与 `git reset` 的区别。
- **大文件管理**：提示使用 Git LFS 管理大文件。

## 5 参考链接

- https://git-scm.com/docs
- https://docs.github.com/en/authentication

---

如需，我可以：
- 将上述建议中的某些项扩展为详细步骤（例如在 Windows 上启用 ssh-agent、配置 GPG 或配置全局 .gitignore）；
- 或根据你的偏好把文档重命名为 `GIT-README.md` 并添加目录（TOC）。
