# publish-skill-to-github

> 把本地 skill / 项目发布到 GitHub 的完整实操流程 skill。重点记录只有踩过才知道的真实坑。

当你说"发布到 github""上传 skill""推送到 github""怎么建仓库绑定"时，这个 skill 会被加载，按验证过的流程走，不走弯路。

## 它解决什么

表面"点一下 Publish"就行，但这套环境里有几个只有踩过才知道的坑：

- **WorkBuddy 的 GitHub 连接器无法推送** —— 它拿的是只读 token，`create_repository` 报 403、`push_files` / `create_or_update_file` 报 404（token 根本看不到你的仓库）。所以发布必须走 **GitHub Desktop** 或 **git CLI**，不能靠连接器代推。
- **账号显示名 ≠ login** —— 显示名（如 `Fengbao`）只是昵称，仓库 URL / Sponsors / README 链接都得用真实 login（如 `Guhengfeng`），写错会指向别人。
- **邮箱隐私拦截** —— 推送报 `email marked as private`，要去 Settings → Emails 取消勾 "Keep my email private" 再推。
- **同名仓库碰撞** —— 网页建了同名空仓又用 Desktop 直接 Publish，会报 `name already exists`，得先绑 remote 再 Push 或删空仓。
- **国内变现受限** —— GitHub Sponsors / 贝宝国内都收不了款，真正能用的是微信 / 支付宝 / 爱发电（见 `references/monetization.md`）。

## 仓库内容

| 文件 | 作用 |
|---|---|
| `SKILL.md` | 6 步核心流程 |
| `references/workflow.md` | GitHub Desktop 逐字步骤 + git CLI 备选 |
| `references/gotchas.md` | 报错速查表（403 / 404 / 撞名 / 邮箱 / 指错人）|
| `references/monetization.md` | 国内收款渠道对比 |
| `references/readme-template.md` | 可直接抄的 skill README 模板（中文）|
| `LICENSE.txt` | MIT |

## 怎么用

把本文件夹放进 skills 目录（如 `~/.workbuddy/skills/publish-skill-to-github/`），之后让 Agent 发布东西时它会自动套用。

或直接照 `references/workflow.md` 手动操作。

## 许可证

MIT —— 见 [LICENSE.txt](LICENSE.txt)。
