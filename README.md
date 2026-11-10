# 常用操作（Mac / Windows）

两种系统的 Git 命令相同，主要区别是终端和本地路径。两台电脑的文件夹路径不需要一致，只需关联同一个 GitHub 仓库，并在 `main` 分支上操作。

- Mac：使用“终端”，本地目录为 `/Users/grandbear/document/my-blog`。
- Windows：推荐使用 PowerShell。下面以 `D:\my-blog` 为例，**请替换成你电脑上实际的 my-blog 路径**。

## 1. 开始写之前：同步最新内容

### Mac

打开“终端”，运行：

```bash
cd /Users/grandbear/document/my-blog
git status
git pull --ff-only
```

### Windows

打开 PowerShell，运行（路径替换成实际目录）：

```powershell
cd "D:\my-blog"
git status
git pull --ff-only
```

如果有上次未提交的修改，先提交，或者按本文末尾的方法临时保存，再拉取。另一台电脑的内容必须已经推送到 GitHub，这台电脑才能同步到。

## 2. 新建或修改文章

使用编辑器打开仓库，文章通常放在 `source/_posts/`。

新建文章时，可以复制已有的 `.md` 文件，修改文件名、标题、日期和正文。保留开头 `---` 之间的配置格式，图片沿用已有文章的存放及引用方式。

示例：

```markdown
---
title: 我的日常记录
date: 2026-11-10 12:00:00
tags:
  - 日常
---

## 今天的记录

这里写正文。
```

日期替换成实际写作时间。Mac 和 Windows 都直接编辑同一套 Markdown 文件，不需要转换文件格式。

- 文件统一保存为 UTF-8，避免中文乱码。
- 图片引用沿用博客现有规则，使用 `/`，不要写 `C:\...` 或 `/Users/...` 这样的电脑本地绝对路径。
- 文件名避免使用 Windows 不允许的字符，例如 `: * ? " < > |`。
- 图片路径与文件名大小写保持一致，避免本地正常、网站图片却无法显示。

## 3. 写完后：检查、提交、上传

以下命令在 Mac 终端和 Windows PowerShell 中相同。先确认已进入 `my-blog` 根目录，保存编辑器中的文件，再运行：

```bash
git status
git diff
```

`git status` 查看新增、修改和删除的文件；`git diff` 查看已跟踪文件中尚未暂存的修改。新文件内容请在编辑器中检查。

确认修改都是本次要上传的内容后：

```bash
git add .
git diff --cached
git commit -m "更新"
git push origin main
```

- `git add .`：暂存当前目录及子目录中未被忽略的改动，包括新增、修改和删除。运行前确认没有密码、密钥或私人文件。
- `git diff --cached`：检查本次将提交的内容。
- `git commit`：保存到本地版本历史，引号中的说明可以自行修改。
- `git push`：上传到 GitHub，需要已配置好账号认证。

如果只想提交指定文件，把 `git add .` 换成：

```bash
git add "source/_posts/文章文件名.md"
```

文章用到的新图片也要单独添加，或确认已包含在 `git add .` 中。

## 4. 查看是否发布成功

推送完成后，检查仓库的 Actions：

https://github.com/grandbear/grandbear.github.io/actions

博客地址：

https://grandbear.github.io/

注意：推送成功代表源码已上传。网站是否自动更新取决于仓库已有的部署配置；如果没有部署任务或任务失败，需要检查配置或错误日志，而不是反复提交。

## 5. 常用查看命令

```bash
# 查看当前修改状态
git status

# 查看最近 5 次提交
git log --oneline -5

# 查看当前分支
git branch --show-current

# 查看关联的远程仓库
git remote -v
```

## 日常速查

### 在 Mac 上写

```bash
cd /Users/grandbear/document/my-blog
git status
git pull --ff-only

# 用编辑器写文章、保存文件

git status
git add .
git diff --cached
git commit -m "更新博客记录"
git push origin main
```

### 在 Windows 上写

把 `D:\my-blog` 替换成实际路径：

```powershell
cd "D:\my-blog"
git status
git pull --ff-only

# 用编辑器写文章、保存文件

git status
git add .
git diff --cached
git commit -m "更新"
git push origin main
```

### 切换电脑时

1. 离开当前电脑前：保存文件，执行 `git add`、`git commit`、`git push`，确认推送成功。
2. 到另一台电脑后：进入它自己的 `my-blog` 目录，执行 `git status`，确认没有未处理的改动，再执行 `git pull --ff-only`。
3. 拉取成功后再开始写；写完继续提交、推送。

两台电脑都遵循：**写前拉取 → 写完提交 → 推送后再换电脑**。只保存文件、只 commit 或只 stash，都不会把记录同步到另一台电脑。尽量不要在未同步时分别修改同一篇文章，也不要使用强制推送来解决同步问题。
