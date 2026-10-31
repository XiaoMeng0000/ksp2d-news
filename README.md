# ksp2d-news

KSP 2D 的「最新消息」内容仓库。

游戏客户端在进入主菜单时，会从这个仓库在线读取一份 `news.json`，
渲染成一个启动弹窗（一张 4:3 配图 + 一段正文 + 按钮），用来向玩家展示
**制作组最近在干嘛 + 游戏最新消息** 的摘要，并引导玩家去游戏内的「游戏公告」面板查看详情。

本仓库只存放内容（一个 JSON 和配图），**与游戏本体仓库完全分离**：
改这里不影响游戏代码，游戏仓库的改动也不需要动这里。

## 仓库里有什么

| 文件 | 说明 |
|---|---|
| `news.json` | 唯一的数据文件，客户端只读这一个文件 |
| `images/` | 弹窗配图，文件名与 `news.json` 里的 `id` 同名 |
| `docs/最新消息编写规范.md` | 文案、图片、发布的完整规则，**改内容前先读它** |

## 怎么发一条新消息（最短步骤）

1. 按 `docs/最新消息编写规范.md` 写好文案、做好配图（4:3，文件名与新 `id` 同名，放进 `images/`）；
2. 修改 `news.json`：更新 `id`（格式 `YYYY-MM-DD-序号`，**改内容必须换新 id**）、
   `updated`（ISO 8601 UTC 时间）、`title`、`image`、`text`（≤200 字）；
3. 提交并推送到 `main` 分支；
4. 客户端下次启动即生效（raw 与 jsDelivr 都有数分钟 CDN 缓存，属正常现象，详见规范文档）。

想临时下线一条消息：把 `news.json` 里的 `enabled` 改成 `false` 再推送即可，客户端不会弹窗。

## 三种访问地址

以 `news.json` 为例（图片同理，把 `news.json` 换成 `images/2026-06-01-a.png`）：

```text
raw      : https://raw.githubusercontent.com/XiaoMeng0000/ksp2d-news/main/news.json
jsDelivr : https://cdn.jsdelivr.net/gh/XiaoMeng0000/ksp2d-news@main/news.json
Pages    : https://xiaomeng0000.github.io/ksp2d-news/news.json
```

三种地址内容相同，均无需任何密钥即可匿名访问（因此本仓库必须保持**公开**）。
根目录的 `.nojekyll` 用于关闭 GitHub Pages 的 Jekyll 处理，加快部署。
