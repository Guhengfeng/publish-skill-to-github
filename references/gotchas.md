# 报错速查表（踩过的坑）

| 报错原话 | 阶段 | 原因 | 解法 |
|---|---|---|---|
| `403 Resource not accessible by integration` | 用连接器 `create_repository` | 连接器 token 是只读/受限，无 `repo` 写权限 | 别用连接器发布；改用 GitHub Desktop / git CLI |
| `404 Not Found`（连接器 `create_or_update_file` / `push_files`） | 用连接器写文件 | token 看不到你的仓库（连 `get repos` 都 404） | 同上，走 Desktop/CLI |
| `Repository creation failed. (name already exists on this account)` | Desktop 点 Publish | 网页已建同名空仓，Desktop 又想再建一个 | 先绑定 remote（走法 B）或删掉网页空仓让 Desktop 自建（走法 A） |
| `Failed to push — Cannot push these commits as they contain an email address marked as private on GitHub.` | Desktop 推送 | GitHub 开了"邮箱隐私保护"，提交里的邮箱被标记私有 | github.com/settings/emails 取消勾 "Keep my email addresses private" → 重推 → 推完可重新勾上 |
| 赞助/主页链接跳到别人页面 | README 链接写错 | 把**显示名**（如 Fengbao）当 **login** 写进链接 | 用浏览器地址栏 `github.com/` 后的真实 login（如 Guhengfeng） |
| Sponsors 页面 404 / 地区不支持 | 申请 GitHub Sponsors | 中国大陆账号 Stripe 不支持 | 别依赖 Sponsors；用爱发电（afdian.com）收国内打赏 |

## 关键认知

1. **WorkBuddy GitHub 连接器 ≠ 能写**。它只能读，发布必须靠 Desktop/CLI。
2. **显示名和 login 是两回事**。所有对外链接用 login。
3. **邮箱隐私开关**会直接阻断首次推送，记得临时关掉再推。
4. **同名仓库碰撞**是 Desktop 最常见的卡点，先绑定 remote 最稳。
