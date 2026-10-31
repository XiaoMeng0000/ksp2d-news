# ksp2d-news

KSP 2D 的「最新消息」内容仓库。

游戏客户端启动时会从本仓库在线读取 `news.json`，渲染成启动弹窗
（一张内置插画 + 一段正文 + 「去公告查看」按钮），用来向玩家展示
**制作组最近在干嘛 + 游戏最新消息** 的摘要，详情引导玩家去游戏内的「游戏公告」面板查看。

## 仓库里有什么

- `news.json` —— **唯一的数据文件**，客户端只读这一个文件；
- `docs/最新消息编写规范.md` —— 字段、文案、发布流程的完整规范，**改内容前先读它**。

本仓库**没有图片目录**：配图已改为游戏内置图库（随游戏本体发布），
`news.json` 里的通知类型字段 `type`（`release` / `progress` / `issue`）决定客户端用哪张插画，
远端不下发任何图片。本仓库与游戏本体仓库完全分离：**改这里不影响游戏代码**。

## 怎么发一条新消息（最短步骤）

1. 改 `news.json` 的 `text`（≤200 字纯文本）和 `type`（`release` / `progress` / `issue` 三选一）；
2. **换新 `id`**（格式 `YYYY-MM-DD-序号`，改内容必须换）并同步更新 `updated`（ISO 8601 UTC 时间）；
3. 提交并推送到 `main`；
4. 等 CDN / Pages 缓存数分钟；
5. 重启游戏即可看到。

临时下线一条消息：把 `news.json` 里的 `enabled` 改成 `false` 再推送，
客户端会清掉本地缓存、不弹窗。规则细节见 `docs/最新消息编写规范.md`。

## 三种访问地址（客户端三源并行竞速，谁先返回合法内容用谁）

```text
pages    : https://xiaomeng0000.github.io/ksp2d-news/news.json
jsdelivr : https://cdn.jsdelivr.net/gh/XiaoMeng0000/ksp2d-news@main/news.json
raw      : https://raw.githubusercontent.com/XiaoMeng0000/ksp2d-news/main/news.json
```

三种地址内容相同，均无需任何密钥即可匿名访问（因此本仓库必须保持**公开**）。
根目录的 `.nojekyll` 用于关闭 GitHub Pages 的 Jekyll 处理，加快部署。
