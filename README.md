# 树成林 AI 榜 · SHU CHENG LIN · AI FOREST

> 全国大学生 AI 创造力与实践成长榜
> **一人一树，众人成林。** 让每一次创造被看见，让每一种成长都有坐标。

这是一个**纯静态、零依赖、可双击打开**的网站项目：原生 HTML / CSS / JavaScript，无框架、无构建步骤、无外部 CDN、无联网字体、无网络图片。所有图形（森林、树木、勋章、年轮、二维码占位）均由内联 SVG / CSS / Canvas 绘制；演示状态用 `localStorage` 本地保存。

> ⚠️ **重要说明：** 本站为**产品演示 Demo**。所有成员、项目、城市、高校、数据、收入与用户反馈**均为虚构示例**；AI 模拟评分由**前端逻辑根据你的输入动态生成**，**并非真实大模型调用**，仅用于成长参考，不代表正式榜单结果。代码已为未来接入真实数据库与 AI API 预留接口位置（见 `calculateAIScore()` 注释）。

---

## 一、文件清单

```
/
├─ index.html                       # 可部署的主站（完全自包含）
├─ README.md                        # 本文件
├─ vercel.json                      # Vercel 部署配置
├─ netlify.toml                     # Netlify 部署配置
├─ .nojekyll                        # GitHub Pages 用（跳过 Jekyll 处理）
├─ robots.txt                       # 基础 SEO
├─ CLAUDE.md                        # 项目产品 / 设计 / 开发总规范
└─ dist/
   └─ shuchenglin-ai-board.html     # 单文件版（与 index.html 内容一致，可独立分发）
```

`index.html` 与 `dist/shuchenglin-ai-board.html` 都是**完整自包含**的单个 HTML 文件，二者内容一致。前者用于网站部署，后者用于直接发给别人双击打开。

---

## 二、本地打开方式

**最简单：** 直接在文件管理器中**双击** `dist/shuchenglin-ai-board.html`（或 `index.html`），用任意现代浏览器（Chrome / Edge / Safari / Firefox）打开即可，无需任何环境。

**可选：本地起一个静态服务器**（便于体验 Web Share、`history` 等需要 `http://` 的能力）：

```bash
# Python 3
python -m http.server 8080
# 然后访问 http://localhost:8080

# 或 Node
npx serve .
```

> 提示：`file://` 方式打开时，所有核心交互（榜单、筛选、生长舱、评分、冲榜、投票、分享卡片下载、收藏、localStorage）都可正常演示；仅「系统分享」按钮在不支持 Web Share 的环境下会自动降级为「复制链接」。

---

## 三、部署到公开平台（任选其一）

本项目是纯静态站点，**根目录直接发布**即可，无需构建命令、无需 `node_modules`。

### 方案 A · GitHub Pages（免费、最常用）

1. 新建一个 GitHub 仓库，例如 `shuchenglin-ai-forest`。
2. 把本目录所有文件推送上去：
   ```bash
   git init
   git add .
   git commit -m "树成林 AI 榜 初始版本"
   git branch -M main
   git remote add origin https://github.com/<你的用户名>/shuchenglin-ai-forest.git
   git push -u origin main
   ```
3. 仓库 → **Settings → Pages** → Source 选 **Deploy from a branch** → 选 `main` 分支、`/ (root)` 目录 → Save。
4. 等待 1–2 分钟，公开地址为：
   `https://<你的用户名>.github.io/shuchenglin-ai-forest/`
   （仓库已含 `.nojekyll`，可避免 Jekyll 对文件的处理。）

### 方案 B · Vercel（无需命令行）

1. 访问 <https://vercel.com> 并用 GitHub 登录。
2. **Add New → Project** → 导入上面的仓库。
3. Framework Preset 选 **Other**；Build Command 留空；Output Directory 填 `.`（已由 `vercel.json` 处理）。
4. **Deploy**，完成后获得 `https://<项目名>.vercel.app`。

> 也可用 CLI：`npm i -g vercel` → 在本目录运行 `vercel`，按提示操作。

### 方案 C · Netlify（拖拽即可）

- **最快：** 打开 <https://app.netlify.com/drop>，把**整个项目文件夹**拖进去，秒级获得公开地址。
- **或** 连接 Git 仓库：Build command 留空，Publish directory 填 `.`（已由 `netlify.toml` 配置）。

### 方案 D · Cloudflare Pages

1. 登录 Cloudflare Dashboard → **Workers & Pages → Create → Pages**。
2. 连接 Git 仓库；Framework preset 选 **None**；Build command 留空；Build output directory 填 `/`。
3. **Save and Deploy**，获得 `https://<项目名>.pages.dev`。

> 部署成功后，请把 `index.html` 中 `<link rel="canonical">` 与 Open Graph 的占位域名替换为你的真实公开地址，分享预览会更完整。

---

## 四、当前部署状态（务必如实阅读）

> 本项目文件已全部生成并通过本地校验，但**尚未部署到任何公开平台**——当前执行环境中**没有可用的 Git 远端 / GitHub / Vercel / Netlify / Cloudflare 登录凭据与发布权限，也未确认外网发布通道**。因此本文件**不提供任何公开链接**（按规范：未真实部署不得虚构网址）。
>
> 你只需按上面**任一方案**操作（最快是 Netlify 拖拽或 GitHub Pages），即可获得真实可分享的公开链接。

---

## 五、已实现的核心功能

- **首页 Hero 森林主视觉**：晨光 + 雾气 + 数据驱动生成的成长树，从「种子」生长成「森林」的入场动效（支持 `prefers-reduced-motion`）。
- **AI 榜（排行榜）**：12 个一级榜单（综合 / 技术 / 变现 / 审美 / 创意 / 社会价值 / 新芽 / 共生 / 成长 / 城市林 / 高校林 / 团队榜）+ 子赛道筛选 + 时间 / 范围筛选 + 实时搜索；前三名为三棵不同形态的代表树（非领奖台）；排名下降用中性「蓄力中」表达。
- **AI 生长舱**：完整作品表单 + 本地文件预览（不上传网络）+ 评分动画 + **动态评分报告**（综合分、七维度、优势短板、证据完整度、适合榜单与预计位次、三个具体行动、置信度、需人工复核项、风险与合规提醒）。
- **AI 评审官**：评分权重（AI 30% / 评委 30% / 成员评议 25% / 证据 15%）、职责说明、可解释的示例评分详情、申诉与人工复核入口。
- **模拟冲榜**：根据你的作品生成可执行成长任务，勾选任务实时预估分数与排名变化。
- **潜力森林**：不按热度，而是发现高潜 / 持续进步 / 来自非热门城市高校 / 帮助他人的作品，每张卡片标注推荐理由。
- **作品森林**：每个项目一棵数据驱动的树，可按开源 / 合作 / 社会价值 / 商业 / 新成员 / 技术等筛选，点击查看项目详情。
- **城市林 / 高校林**：地区与高校的创造密度视图（注明不代表优劣）。
- **成长等级 + 勋章墙**：7 级成长阶段、14 枚抽象符号勋章（点击查看条件与成长故事）。
- **社会价值**：「改变正在发生」真实问题故事卡。
- **公平规则 + AI 透明中心**：10 条公平原则、模型版本、人工复核比例、无效票与异常投票说明、规则更新时间。
- **投票评议**：查看作品 → 选择理由 → 投票（隐藏实时票数、禁止自投、新叶动效），不生成定向拉票链接。
- **分享**：分享卡片预览 + Web Share API + 复制链接降级 + **Canvas 离线生成分享卡片 PNG 下载**（含二维码预留区）。
- **成员详情抽屉 / 个人主页**：简介、代表项目、技能、勋章墙、成长年轮、AI 报告摘要、用户反馈、合作方向。
- **工程与无障碍**：语义化结构、键盘操作、`ESC` 关闭弹窗、焦点管理、移动端导航与响应式、`localStorage` 持久化、控制台无报错、完整 SEO / Open Graph / Twitter Card。

---

## 六、二次开发指引

- **示例数据集中管理**：成员见 `MEMBERS`，榜单见 `BOARDS`，勋章见 `BADGES`，城市/高校见 `PLACES`，社会价值见 `STORIES`，评分标准见 `CRITERIA`。
- **接入真实 AI**：把 `calculateAIScore()` 内的前端逻辑替换为后端 / 大模型 API 调用（函数顶部已注明位置），返回结构保持一致即可无缝替换。
- **接入真实数据库**：将 `MEMBERS` 等改为接口拉取，渲染函数（`renderBoard` / `renderForest` 等）无需改动。
- **核心函数**：`calculateAIScore()`、`calculateLeaderboardScore()`、`generateGrowthTasks()`、`generateRecommendations()`、`filterLeaderboard()`、`submitVote()`、`createShareCard()`、`treeSVG()`。

---

## 七、隐私、安全与伦理

只展示成员主动公开的信息；不公开私人手机号与邮箱；城市可隐藏、高校可模糊；收入以区间展示；成员可申请下架作品与删除 AI 评审记录；评审证据仅用于评审。**禁止**虚假收入、盗用作品、冒用客户案例、AI 伪造证明、刷票与诱导投票。本站所有示例数据均为虚构。

---

**愿我们在 AI 时代，不只是学会使用工具。更能用工具创造价值、帮助他人，并共同长成一片森林。**
