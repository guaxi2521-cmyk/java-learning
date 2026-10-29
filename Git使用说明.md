# Git 与 GitHub 使用说明

> 配置完成：2026-10-29

## 已完成

| 项目 | 状态 |
|---|---|
| Git 版本 | 2.56.0 |
| 用户名 | `Guaxi2521-CMYK` |
| 邮箱 | `Guaxi2521-CMYK@users.noreply.github.com` |
| 远程仓库 | https://github.com/guaxi2521-cmyk/java-learning |
| 认证方式 | HTTPS + Personal Access Token（已存入凭据管理器） |
| 首次推送 | ✅ 成功，3 次提交已上线 |

---

## 日常三连（90% 的操作都在这里）

```powershell
cd C:\Users\95843\Documents\deepseek-harness\default-workspace\java-learning

git add -A                          # 把改动加入暂存区
git commit -m "完成了XX练习"          # 提交，引号里写你做了什么
git push                            # 推到 GitHub
```

**每天学完就执行一次**，你的 GitHub 主页会累积绿色格子。一年后这是简历上最实在的东西。

---

## 必会的查看命令

```powershell
git status          # 现在有哪些改动（最常用，迷糊时先敲它）
git log --oneline   # 提交历史（q 退出）
git diff            # 具体改了哪几行
git remote -v       # 远程地址对不对
```

---

## 撤销与回退（新手最需要的救命命令）

| 场景 | 命令 | 说明 |
|---|---|---|
| 改了文件想恢复原样 | `git restore 文件名` | 丢弃未暂存的修改，**不可恢复** |
| `git add` 错了想撤回 | `git restore --staged 文件名` | 只是退出暂存区，文件内容不变 |
| 提交信息写错了 | `git commit --amend -m "新信息"` | 只改最近一次提交 |
| 想看某个历史版本 | `git log --oneline` 找到 SHA，`git show <sha>` | 只查看，不改动 |

> ⚠️ **永远不要**用 `git reset --hard` 或 `git push -f`，除非你清楚后果。在你还没熟练前，这两个命令能让你丢代码。

---

## 关于认证（重要）

### 现在是怎么认证的

用 **HTTPS + Token**，token 已存进 Windows 凭据管理器，所以 `git push` **不再需要输入密码**。

当前保存的 token：
- 权限：`repo`
- 有效期：**90 天**（约 2027 年 1 月底过期）

### Token 过期了怎么办

`git push` 会提示认证失败，重新生成一个即可：

1. 打开 <https://github.com/settings/tokens/new?scopes=repo&description=java-learning-push>
2. Note 随便写，Expiration 选 90 days 或 No expiration
3. 勾 **repo**，点 Generate token
4. 复制 `ghp_...` 那串，然后执行：

```powershell
git remote set-url origin https://Guaxi2521-CMYK:新TOKEN@github.com/guaxi2521-cmyk/java-learning.git
git push
git remote set-url origin https://github.com/guaxi2521-cmyk/java-learning.git   # 推完记得把 token 从地址里去掉
```

### 为什么没用 SSH

你家网络把 **22 端口封了**（DNS 走 Clash 的 fake-ip `198.18.0.30`），SSH 连不上。虽然也配了 443 端口的备用通道（`~/.ssh/config` 里已有 `ssh.github.com:443`），但公钥始终没成功加到 GitHub 上。

**目前 HTTPS 完全够用**，不影响任何学习进度。以后想换 SSH，把下面这把公钥加到 <https://github.com/settings/ssh/new> 即可：

```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIB0DYtmoabMsiyQYgJYS4TK8/f3OuiwMu/Yi2gZPb1AT github-java-learning
```

添加后测试：`ssh -T -p 443 git@ssh.github.com`

---

## 已配置的全局设置

```ini
user.name       = Guaxi2521-CMYK
user.email      = Guaxi2521-CMYK@users.noreply.github.com
init.defaultBranch = main
core.autocrlf   = true          # Windows 换行符自动转换
credential.helper = manager     # 用 Windows 凭据管理器存密码
```

---

## 常见问题

| 现象 | 原因 | 解决 |
|---|---|---|
| `Authentication failed` | token 过期或输错 | 重新生成 token，见上文 |
| `Updates were rejected` | GitHub 上有本地没有的提交 | `git pull --rebase` 后再 push |
| `fatal: not a git repository` | 当前目录不对 | `cd` 到 `java-learning` 目录 |
| 中文文件名显示乱码 | Git 默认转义非 ASCII | `git config --global core.quotepath false` |
| 提交后 GitHub 上没显示 | 忘了 `git push` | `git status` 看是否 `ahead of origin` |

---

## 仓库结构

```
java-learning/
├── .gitignore          # 排除 *.class、.idea、.vscode 等
├── README.md           # 仓库说明
├── 环境说明.md          # JDK/Git/VSCode 安装位置
└── day01/
    └── HelloWorld.java # 第一个程序
```
