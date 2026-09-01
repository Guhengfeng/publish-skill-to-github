---
name: publish-skill-to-github
description: 把本地 skill / 项目发布到 GitHub 的完整实操流程。覆盖仓库创建（网页建空仓 vs Desktop 自建）、本地文件夹绑定远程、首次推送，并重点记录 WorkBuddy GitHub 连接器无法推送（只读 token，建仓/写文件报 403/404）、账号显示名与 login 混淆、邮箱隐私拦截、以及国内无法开通 Sponsors/贝宝收款等真实坑与解法。当用户说"发布到 github""上传 skill""推送到 github""怎么建仓库绑定"时使用。
---

# Publish Skill to GitHub

你正在帮用户把一个本地文件夹（通常是一个带 `SKILL.md` 的 WorkBuddy skill，或任意项目）发布到 GitHub。表面上"点一下 Publish"就行，但在这套环境里有几个**只有踩过才知道的坑**。按下面验证过的流程走，别走弯路。

## 0. 最重要的一条：别用 WorkBuddy 的 GitHub 连接器去发布

本机的 GitHub 连接器（`mcp__github__*` 系列工具）虽然连着、能读到你的身份，但拿的是**受限 / 只读 token**：

- ✅ 能：`get_me` 读身份、`search_repositories` 等只读查询
- ❌ 不能：建仓库（`create_repository` → **403 Resource not accessible by integration`）、写文件（`create_or_update_file` / `push_files` → **404**，因为 token 根本看不到你的仓库）

所以**不要试图用连接器建仓或推送**。正确做法是 **GitHub Desktop（图形界面）** 或 **git CLI**，在一台能联网的机器上推。这是和"别的地方教程"最大的不同——它们默认连接器能写，这里不行。

## 1. 准备本地发布目录

确认文件夹里至少有：

- `SKILL.md`（或项目入口文件）
- `references/`（如有）
- `LICENSE.txt`（建议 MIT，署名写法见 `references/readme-template.md`）
- `README.md`
- `.gitignore`

> 发布前把 README 里所有**私人项目名、真实联系方式**替换为通用示例或占位，避免泄露。

## 2. 创建仓库 + 绑定本地目录（两种走法，选一个）

### 走法 A：让 GitHub Desktop 直接建仓（最省心）
1. 打开 GitHub Desktop → **File → Add Local Repository…**
2. Choose 定位到你的发布文件夹
3. 提示"不是 git 仓库" → 点 **Create a repository**；**不要**勾 "Initialize with README"（README 你已有），**不要**勾 Git Ignore 模板（你已有）
4. 进入仓库，左下 Summary 填 `Initial publish`，点 **Commit to main**
5. 右上角 **Publish repository** → Name 填仓库名、取消勾 **Keep this code private**（要公开）→ 点 Publish
6. 完成

### 走法 B：网页先建空仓，Desktop 绑定后推送（适合你已在网页建好仓库）
1. 浏览器 github.com → New repository → 填名、**Public**、**不勾 README**（留空）→ Create
2. 回到 GitHub Desktop → **Repository → Repository settings…**
3. **Primary remote repository** 填 `https://github.com/<login>/<repo>.git` → Save
4. 右上角按钮会从 "Publish branch" 变成 **"Push origin"** → 点它
5. 完成

### ⚠️ 碰撞陷阱（最容易卡这里）
如果你**网页建了同名空仓**，又在 Desktop 里直接点 **Publish repository**（没先绑定 remote），Desktop 会试图**再建一个同名仓库** → 报：
`Repository creation failed. (name already exists on this account)`
- 解法 1（推荐）：走法 B，先绑定 remote 再 Push。
- 解法 2：去网页把那个空仓删掉（Settings → Danger Zone → Delete），再让 Desktop 自建（走法 A）。

## 3. 邮箱隐私拦截（第二个常见报错）

推送时报：
`Failed to push — Cannot push these commits as they contain an email address marked as private on GitHub.`
- 去 https://github.com/settings/emails → **取消勾选 "Keep my email addresses private"**
- 回 Desktop 再点一次 **Push origin**
- 推完建议**重新勾上**该选项，避免以后提交暴露真实邮箱

## 4. 账号身份：显示名 ≠ login（第三个坑，极易指错人）

GitHub 有两个名字：
- **显示名（Display name）**：如 `Fengbao`，只是昵称，可随便改
- **登录名（login）**：如 `Guhengfeng`，仓库 URL、Sponsors、README 里的链接都用它

确认方法：浏览器打开你的 GitHub 主页，看地址栏 `github.com/` 后面那串就是真实 login。
- README 里的赞助/主页链接必须写 **login**，写显示名会跳到别人页面。
- 真实案例：把显示名 `Fengbao` 当 login 写进 Sponsors 链接，导致指向了别人。

## 5. 验证

推送成功后，Desktop 右上角按钮从 "Publish branch" 变为 **"Fetch origin"**，且显示 "No local changes"。打开 `https://github.com/<login>/<repo>` 刷新，应能看到文件与渲染的 README。

## 6. 国内变现（详见 references/monetization.md）

- **GitHub Sponsors**：中国大陆账号基本开通不了（打款走 Stripe，Stripe 不支持大陆个人）——别依赖。
- **贝宝 / PayPal 中国**：只能付不能收境外款，收不了赞助。
- **爱发电（afdian.com）**：国内可直接打赏，提现到微信/支付宝，是 README 里最实用的"支持"入口。

详见 `references/monetization.md` 与 `references/readme-template.md`（含爱发电链接写法）。

## 参考文件
- `references/workflow.md` — 全流程逐字步骤 + 截图级指引
- `references/gotchas.md` — 每个报错的原话、原因、解法速查表
- `references/monetization.md` — 国内收款渠道对比与 README 写法
- `references/readme-template.md` — 可直接抄的 skill README 模板（中文、含 before/after 对比、爱发电入口）
