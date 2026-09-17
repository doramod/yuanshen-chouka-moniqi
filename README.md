# 元神抽卡模拟器（点名）

原神抽卡模拟器（Genshin Impact Wish Simulator）的静态部署版本。100% 前端运行，抽卡记录保存在浏览器 localStorage / IndexedDB，无需后端。

## 在线地址

部署后由 Cloudflare Pages 生成，形如 `https://yuanshen-chouka-moniqi.pages.dev`

## 项目来源

- 上游仓库：<https://github.com/animation-picker/genshin-impact>
- 原始项目：<https://github.com/Mantan21/Genshin-Impact-Wish-Simulator>
- 技术栈：SvelteKit + Vite，输出为纯静态站点（adapter-vercel）
- 卡池数据版本：5.0 ~ 5.2

> 仓库自带的 `electron-static/static` 是 CI 产物，其 index.html 与 JS chunk 的 hash 对不上（缺 12 个核心模块），直接托管会白屏。本仓库的内容是从源码重新构建得到的，资源引用完整。

## 目录结构

```
/
├── index.html          # 应用入口（SSR 预渲染 + 客户端 hydrate）
├── internal/           # JS / CSS 构建产物
├── images/ videos/ sfx/ fonts/   # 卡池与角色素材
├── _redirects          # SPA 回退规则（Cloudflare Pages）
└── tools/serve.js      # 本地预览服务器
```

## 本地预览

```bash
node tools/serve.js
# 打开 http://localhost:5180
```

## 从源码重新构建

上游子项目位于 `Genshin-Impact-Wish-Simulator/`：

```bash
cd Genshin-Impact-Wish-Simulator
cp .env.example .env     # VITE_CHATROOM=false 关闭 firebase 聊天室
npm install --legacy-peer-deps
npm run build            # 产物输出到 .vercel/output/static
```

把 `.vercel/output/static` 的内容覆盖到本仓库根目录即可更新站点。

## Cloudflare Pages 部署设置

| 项目 | 值 |
| --- | --- |
| Framework preset | None |
| Build command | 留空 |
| Build output directory | `/` |
| Node version | 无需 |

仓库根目录已放好 `_redirects`，保证 `/wish`、`/inventory` 等客户端路由刷新时不会 404。

## 许可

上游项目采用 `CC BY-NC-SA 4.0`，**禁止商业用途**；核心模拟器部分继承 MIT 许可证。详见上游仓库 LICENSE。素材版权归米哈游所有，本项目仅作学习交流。
