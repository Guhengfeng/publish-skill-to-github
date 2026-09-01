# 全流程逐字步骤（GitHub Desktop 图形界面）

适用：不想敲命令、在本机装了 GitHub Desktop 的用户。下面假设你已经把发布文件准备好在本地某个文件夹（例如 `publish-fdc/`）。

## 阶段一：让 Desktop 识别本地文件夹

1. 打开 **GitHub Desktop**。
2. 顶部菜单 **File → Add Local Repository…**（中文：文件 → 添加本地仓库）。
3. 点 **Choose…**，定位到发布文件夹。
4. 它会提示 "This directory does not look like a Git repository"（不是 git 仓库）。
5. 点 **Create a repository** —— 弹窗里：
   - **Name**：建议和 GitHub 上要用的仓库名一致（如 `frontend-design-craft`）
   - **Git ignore**：选 **None**（你已有 `.gitignore`）
   - **License**：选 **None**（你已有 `LICENSE.txt`）
   - **Initialize with README**：**取消勾选**（你已有 README，否则会冲突）
6. 点 **Create repository**。进入仓库主界面，Changes 区会列出所有文件。

## 阶段二：首次提交

1. 左下 **Summary（必填）** 填：`Initial publish: <仓库名>`
2. （可选）Description 填一句说明
3. 点 **Commit to main**

## 阶段三：推到 GitHub

### 情况 1：GitHub 上还没有这个仓库（让 Desktop 自建）
1. 提交后右上角出现 **Publish repository** 按钮 → 点它。
2. 弹窗：
   - **Name**：确认是你要的仓库名
   - **Description**：可填一句话简介
   - **Keep this code private**：**取消勾选**（要 Public）
3. 点 **Publish repository**。等进度条走完即上线。

### 情况 2：GitHub 上已经建了同名空仓库（绑定后推）
1. 提交后右上角是 **Publish repository** 按钮时，**先别急着点**。
2. 顶部菜单 **Repository → Repository settings…**
3. **Primary remote repository** 填 `https://github.com/<login>/<repo>.git` → Save。
   - `<login>` 是真实登录名（见 SKILL.md 第 4 节），不是显示名。
4. 右上角按钮变成 **Push origin** → 点它，把本地文件推到已存在的空仓库。

## 阶段四：验证
- 按钮变 **Fetch origin** + "No local changes" = 同步成功。
- 浏览器打开 `https://github.com/<login>/<repo>` 刷新，应能看到文件与渲染的 README。

## 备选：git CLI（无 Desktop 时）

在能联网的机器上：
```bash
cd <发布文件夹>
git init
git add .
git commit -m "Initial publish: <仓库名>"
git branch -M main
git remote add origin https://github.com/<login>/<repo>.git
git push -u origin main
```
> 前提：该机器装了 git 且能访问 github.com（本工作机之前连 GitHub 网络不通，需换环境）。
