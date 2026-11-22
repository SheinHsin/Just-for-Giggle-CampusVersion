# 图一乐 · Just for Giggle

[中文](#中文) · [English](#english) · [在线试玩 / Play online](https://sheinhsin.github.io/Just-for-Giggle-CampusVersion/) · [英文版 / Play in English](https://sheinhsin.github.io/Just-for-Giggle-CampusVersion/?lang=en)

## 中文

### 项目简介

**图一乐（Just for Giggle，简称 JfG）** 是为广东财经大学 1024 创新日搭建的网页小程式。课间、等人的时候，或者刚写完一段作业时，有些同学会觉得无聊，却一时想不到可以做些什么。图一乐把这些五到二十分钟的碎片时间变成一次随手可做的小挑战。抽张卡，找点新鲜事，图的就是一乐。

### 网站功能

| 栏目 | 可以做什么 |
| --- | --- |
| **找点乐子** | 从 84 张趣事卡中抽取挑战。按 5、10 或 20 分钟、原地或外出、独自或与朋友筛选。每张卡都有玩法和完成条件，例如给桌面物件写展签、和朋友互相描述并画出图形，或去走廊寻找有趣的字体。换卡时可以说明原因，下一次抽取会参考时间、地点、伙伴、工具和安静程度等限制。 |
| **今天吃啥** | 从 44 道内置示例菜开始，按食堂或外卖、主食类型、菜系、口味和每 5 元一档的价格区间筛选。符合条件的餐食以弹窗呈现，可以换一道、确认这顿吃什么，或者维护自己的菜单。示例价格供试玩参考。 |
| **开始学习** | 输入要完成的任务与当前卡点，生成一组可编辑的步骤。「快速拆解」无需下载。本机 AI 可给出更贴合输入的计划。做完一步后可以继续下一步，也可以留一个断点，回来接着做。 |
| **口袋与成就** | 完成的趣事、选好的餐食和保存的学习计划可以在口袋里回看。每累计完成三次趣事挑战，就会获得一个结合已完成卡片主题的称号。探索和连续完成新卡也可以解锁徽章。登录后可选择公开用户名和完成数量，参加本周榜单。 |

游客可以直接使用主要功能。注册时验证邮箱，之后可用用户名和密码登录，将卡片记录、菜单与学习计划同步到其他设备。网页右上角可切换中文或 English，语言选择保存在当前浏览器。

### 技术实现

- **单文件前端**采用原生 HTML、CSS、JavaScript 和内联 SVG。站点由 GitHub Pages 托管，也可下载一个 HTML 文件直接打开。
- **球形转盘**用 JavaScript 计算双层卡片在球面上的位置，再用 CSS 变换和 `requestAnimationFrame` 绘制。转盘在空闲时持续缓转，随鼠标移动调整视角。抽取时加速，再减速把选中的卡片带到中央。也可以暂停动效，页面会响应系统的「减少动态效果」设置。
- **卡片和菜单**使用固定卡片 ID、分类字段和规则筛选。抽卡优先挑选近期没见过的内容，并参考用户给出的换卡原因。中英文使用同一份记录和筛选值，用户自填内容保留原文。
- **学习规划**提供两种路径。快速拆解在浏览器内按任务类型生成步骤。本机 AI 通过 WebAssembly 和 wllama 运行 Qwen2.5-0.5B-Instruct 的 GGUF 量化模型。模型文件约 429 MB，可以下载或手动载入。推理在设备上进行，登录后保存的学习内容可随账户同步。
- **存储、账户和榜单**使用浏览器存储保留游客记录、会话和语言偏好，经允许后使用 IndexedDB 缓存学习模型。线上账户由 Supabase Auth 管理，用户名登录经 Edge Function 处理。PostgreSQL 保存云端记录和榜单数据，并使用行级安全策略与受权限控制的数据库函数限制访问。

### 本地打开

在下方版本表中选择「HTML」，将文件保存为 `.html`，再用浏览器打开。双击本地文件会进入游客模式。需要注册、登录或跨设备同步时，请使用在线站点。

## English

### About the project

**Just for Giggle (JfG)**, or **图一乐**, is a small web app built for 1024 Innovation Day at Guangdong University of Finance and Economics (GDUFE). Between classes, while waiting for a friend, or after finishing part of an assignment, there's often a little time to fill and no obvious way to spend it. JfG turns those spare five to twenty minutes into something you can try on the spot. The Chinese name means doing something just for the fun of it.

### What you can do

| Section | What it offers |
| --- | --- |
| **Find Fun** | Draw from 84 challenge cards. Filter for 5, 10, or 20 minutes, staying put or going outside, and playing solo or with a friend. Every card explains what to do and what counts as finishing. You might write a museum label for a desk object, describe and draw a picture with a friend, or look for interesting lettering down the hall. If you skip a card, you can tell JfG why so the next draw can account for limits such as time, company, supplies, or noise. |
| **What to Eat** | Start with 44 sample dishes. Filter by canteen or delivery, staple, cuisine, flavor tags, and price ranges in CNY 5 increments. Review the suggestion in a dialog, try another dish, save your choice, or edit your own menu. Sample prices are for reference. |
| **Study** | Describe a task and where you're stuck, then generate editable steps. Quick plan works without a model download. On-device AI can tailor the plan to what you write. Work through the steps or leave a note about where to pick up later. |
| **Pocket and achievements** | Revisit completed challenges, chosen meals, and saved study plans in Pocket. Every three challenge completions earns a personal title based on the cards you've finished. Exploring and completing new cards on consecutive days can unlock badges. Signed-in users can opt in to the weekly leaderboard by sharing their username and completion count. |

The main features are available in guest mode. Verify your email when registering, then log in with your username and password to sync cards, menus, and study plans across devices. Use the language menu in the upper-right corner to switch between Chinese and English. The browser remembers your choice.

### How it works

- **Single-file frontend.** The app uses plain HTML, CSS, and JavaScript with inline SVG. GitHub Pages hosts the live site, and a standalone HTML file can be opened in a browser.
- **Spherical spinner.** JavaScript positions two layers of cards on a sphere. CSS transforms and `requestAnimationFrame` animate the layout. The deck rotates slowly at rest and responds to the pointer, then speeds up during a draw before bringing the selected card to the center. Motion can be paused and follows the system's reduced-motion setting.
- **Cards and menus.** Stable card IDs, category fields, and filtering rules keep the data consistent across languages. Draws prioritize cards the user has not seen recently and account for skip reasons. User-entered content stays in its original language.
- **Study planning.** Quick plan generates steps in the browser using rules for different task types. The optional AI path uses WebAssembly and wllama to run the quantized Qwen2.5-0.5B-Instruct GGUF model. The roughly 429 MB file can be downloaded or loaded manually. Inference runs on the device, and saved study content can sync when the user is signed in.
- **Storage, accounts, and rankings.** Browser storage keeps guest activity, session data, and language preferences. IndexedDB caches the model when allowed. Supabase Auth manages online accounts. An Edge Function handles username login, while PostgreSQL stores synced activity and rankings behind row-level security and permission-controlled database functions.

### Open it locally

Choose an **HTML** link in the archive below, save the file with an `.html` extension, and open it in your browser. Opening the file directly starts guest mode. Use the live site for registration, login, and cross-device sync.

## 版本存档与单文件网页 / Version archive and standalone HTML

| 版本 / Version | 在线 / Online | 单文件 / Standalone |
| --- | --- | --- |
| 当前双语版 / Current bilingual build | [中文](https://sheinhsin.github.io/Just-for-Giggle-CampusVersion/) · [English](https://sheinhsin.github.io/Just-for-Giggle-CampusVersion/?lang=en) | [HTML](https://raw.githubusercontent.com/SheinHsin/Just-for-Giggle-CampusVersion/main/index.html) |
| 1.2 · 用户协议与 Cookie 设置 / Terms of use and Cookie settings | [存档 / Archive](https://sheinhsin.github.io/Just-for-Giggle-CampusVersion/versions/v1.2.0/) | [HTML](https://raw.githubusercontent.com/SheinHsin/Just-for-Giggle-CampusVersion/main/versions/v1.2.0/index.html) |
| 1.1.1 · 恢复空闲轮转 / Restored idle rotation | [存档 / Archive](https://sheinhsin.github.io/Just-for-Giggle-CampusVersion/versions/v1.1.1/) | [HTML](https://raw.githubusercontent.com/SheinHsin/Just-for-Giggle-CampusVersion/main/versions/v1.1.1/index.html) |
| 1.1 · Skydiver 界面更新 / Skydiver interface update | [存档 / Archive](https://sheinhsin.github.io/Just-for-Giggle-CampusVersion/versions/v1.1.0/) | [HTML](https://raw.githubusercontent.com/SheinHsin/Just-for-Giggle-CampusVersion/main/versions/v1.1.0/index.html) |
| 1.0 · 正式版 / First stable release | [存档 / Archive](https://sheinhsin.github.io/Just-for-Giggle-CampusVersion/versions/v1.0.0/) | [HTML](https://raw.githubusercontent.com/SheinHsin/Just-for-Giggle-CampusVersion/main/versions/v1.0.0/index.html) |
| Demo Beta · 早期试玩版 / Early public demo | [存档 / Archive](https://sheinhsin.github.io/Just-for-Giggle-CampusVersion/downloads/tuyile-demo-beta.html) | [HTML](https://raw.githubusercontent.com/SheinHsin/Just-for-Giggle-CampusVersion/main/downloads/tuyile-demo-beta.html) |

## 联系方式 / Contact

项目反馈或合作交流，欢迎发邮件。

For feedback or collaboration, get in touch by email.

[xinshen181@student.gdufe.edu.cn](mailto:xinshen181@student.gdufe.edu.cn)
