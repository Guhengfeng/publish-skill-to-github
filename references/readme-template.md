# 可直接抄的 skill README 模板（中文）

把 `<...>` 占位替换成你自己的内容。注意：**不要暴露私人项目名和真实联系方式**，示例用通用名。

```markdown
# <skill-名称>

> <一句话定位：这个 skill 解决什么问题>

改编自 / 灵感来自 <原作者/原项目>（<协议，如 Apache-2.0>）。

## 这是什么

<2-3 句说清它做什么、和别的有什么不同>

## 我做了哪些修改（你的二次创作价值）

- <扩充点 1：例如"从 Web 扩成跨平台方法论">
- <扩充点 2：例如"新增方向库，给出具体配色与字体配对">
- <扩充点 3：例如"新增 AI-slop 反模式检测器">

## 使用前 / 使用后

| 维度 | 使用前（普通 AI 生成） | 使用后（本 skill） |
|---|---|---|
| 配色 | <踩了什么 slop> | <用了什么方向> |
| 字体 | <默认脸> | <具体配对> |
| 结构 | <模板化> | <信息驱动> |
| 文案 | <空话> | <具体> |

效果对比：
- 使用前：见 `demo/before.html`
- 使用后：见 `demo/after.html`

![使用前](demo/before.svg)
![使用后](demo/after.svg)

## 用法

<怎么调用这个 skill / 放哪个目录>

## 协议

MIT。改编自 <原作者/原项目>（<协议>），保留其署名。
```

## LICENSE.txt（MIT，含署名）

```
MIT License

Copyright (c) <年份> <你的名字/GitHub login>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND.

---

Adapted from <原作者/原项目> (licensed under <Apache-2.0 或其他>).
Original copyright held by <原作者>. This adaptation is distributed under MIT
with the above notice.
```

## .gitignore（skill 发布够用）

```
# 系统/编辑器
.DS_Store
Thumbs.db
*.swp

# 本地缓存
.node_modules/
__pycache__/
*.pyc

# 不要把本地草稿推上去
draft/
tmp/
```
