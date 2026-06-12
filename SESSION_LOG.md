# SESSION LOG

## 完成
- 2026-06-12 提交 index.html 第六届招生更新（第五届→第六届、新增培养特色/选拔流程/注意事项/工作要求）并推上 origin/main
- 2026-06-12 合并远程 c20e349 提交（23 届轮播图、实习风采视频板块、DEPLOY.md、wrangler.toml），解 5 处冲突后推送合并提交 b071df9
- 2026-06-12 本地起 Python http.server 8000 端口预览，用 Edge + Playwright 截图验证渲染
- 2026-06-12 重新授权 wrangler OAuth（refresh token 2025-12-31 过期），执行 wrangler pages deploy ./ 完成部署（29 文件 / 6.42s）
- 2026-06-12 验证生产 URL https://zhuoyue.yangzh.cn 资源（主页、23 届轮播图、申请表 doc、实习视频）全部 200

## 发现
- 2026-06-12 wrangler OAuth refresh token 失效后重授权：wrangler login --browser=false 后台跑 + start 打开打印的 URL + 浏览器完成确认；本地 8976 端口回调服务会等到用户授权
- 2026-06-12 Playwright MCP 强依赖系统 Chrome（C:\Users\yangj\AppData\Local\Google\Chrome\Application\chrome.exe），npx playwright install chrome 需要管理员权限；fallback 是 npx playwright install chromium + Python playwright.sync_api 调 chromium 截图
- 2026-06-12 HTML 冲突合并策略：远程给可读结构（br 分行），本地给独有内容（六、工作要求、招生宣传热线），两者都保留而不是二选一

## 待办
1. 询问宏哥是否停掉本地 Python http.server 8000 端口（任务 ID bqtqg34nw），目前仍在跑
