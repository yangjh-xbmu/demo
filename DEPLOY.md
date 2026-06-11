# 部署说明

本页说明如何把仓库部署到 Cloudflare Pages。

## 线上地址

| 类型 | URL |
| --- | --- |
| 自定义域 | https://zhuoyue.yangzh.cn |
| Pages 默认域 | https://zhuoyue-dkq.pages.dev |
| Pages 项目 | `zhuoyue`（Account ID: `1302a6e18876381b6b098877ea8ea22c`） |

## 一次性准备

1. 安装 wrangler

   ```bash
   npm install -g wrangler
   ```

2. 登录 Cloudflare 账号

   ```bash
   wrangler login
   ```

   本地会启动浏览器 OAuth 流程，完成后凭据存在 `%APPDATA%\xdg.config\.wrangler\config\default.toml`（Windows）。

## 部署命令

仓库根目录里已有 `wrangler.toml`，里面固化了项目名 `zhuoyue` 和输出目录 `.`，所以部署时无需带参数。

```bash
wrangler pages deploy ./
```

部署完会输出新的预览 URL，形如 `https://<hash>.zhuoyue-dkq.pages.dev`。

## 验证清单

部署后跑以下检查：

```bash
# 主页响应
curl -sI https://zhuoyue.yangzh.cn | head -1
# 期望：HTTP/2 200

# 轮播图资源
curl -sI https://zhuoyue.yangzh.cn/首轮1.jpg | head -1
# 期望：HTTP/2 200

# doc 申请表下载
curl -sI "https://zhuoyue.yangzh.cn/附件3 西北民族大学卓越新闻学实验班申请表.doc" | head -1
# 期望：HTTP/2 200
```

## 自定义域

- DNS：`zhuoyue.yangzh.cn` CNAME 指向 `zhuoyue-dkq.pages.dev`，Proxied（橙云）
- SSL：由 Cloudflare 自动签发（Google CA）
- 添加自定义域的命令是 `POST /accounts/{account_id}/pages/projects/zhuoyue/domains`，需 `pages:write` 权限的 API Token

## 切换到 Git 自动部署（可选）

1. 打开 https://dash.cloudflare.com/ → Workers & Pages → zhuoyue
2. Settings → Builds → Connect to Git
3. 选 `yangjh-xbmu/demo` 仓库，Build command 留空，Build output directory 填 `/`
4. 之后 `git push` 到 main 分支就会自动部署

## 仓库文件

```
.
├── AI图表标.png                          # AI 助手浮窗图标
├── index.html                            # 主页（HTML + Tailwind CDN + 内联 JS）
├── 附件3 西北民族大学卓越新闻学实验班申请表.doc  # 招生申请表
├── 首轮1.jpg ~ 首轮7.jpg                  # 轮播图（7 张）
├── wrangler.toml                         # Pages 项目配置
├── .gitignore                            # 忽略 Playwright / 构建产物
└── DEPLOY.md                             # 本文件
```
