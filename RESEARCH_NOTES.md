# RESEARCH_NOTES

## 项目目标与范围

Chao He 的公开学术主页。Jekyll / al-folio v1 / GitHub Pages；只展示用户明确授权的三篇论文。

## 当前已确认结论

- 源码已核实：基于官方 starter `fde4cbf`，核心 gem 固定 `al_folio_core 1.0.15`；运行时由版本化插件提供。
- 用户明确要求：毕业于 Soochow University；不声明现任机构、学位或工作。无照片、CV、Scholar 账号。
- 文献报告：Endo-GSG 的作者、DOI、页码和官方 PDF 链接已由 IJCAI 页面核实；Endo-4SRF 的卷期、页码、作者与 DOI 由 PubMed 核实。IEEE 页面有机器人验证限制。
- 用户明确要求：ROBIO 论文入围 Best Paper Finalist，已接收但未见刊，显示 `ACCEPTED · Not yet published`；完整作者与 DOI 尚未提供；YAML 适配记录不输出作者或伪造 citation。
- 决策：首页与 Publications 共用 Scholar + 一个公共 include，排序沿 BibTeX 输入再附加 ROBIO。无图记录不留空图框。
- 决策：不转载权限未确认的出版商图像。已检查 Endo-GSG 官方 PDF 首图；当前三篇均为文字展示，可在取得获准图像后添加 teaser。

## 当前状态、阻碍与下一步

- 用户改为项目站点：`https://hansello218.github.io/ChaoHe-research/`，`baseurl: /ChaoHe-research`；此前空 baseurl 的用户主页配置已取代。
- 用户已完成仓库改名；`git ls-remote origin` 成功。用户已明确授权提交、推送与部署，正在执行首次发布。
- 源码已推送 origin/main，提交 `42240c5`；GitHub Actions 与 Pages 上线验证进行中。
- 用户主页版本的既有验证见历史记录；项目路径验证见本次更新记录。

## 研究记录

### 2026-11-18 | 初始化与来源核实

- 类型：源码已核实 / 用户明确要求 / 决策。
- 本地项目由官方公开模板建立；不是现有用户仓库的覆盖修改。
- 已阅读 AGENTS、bootstrap skill、INSTALL、CUSTOMIZE、BOUNDARIES 和相关 ARCHITECTURE 段落。
- 出版来源：https://www.ijcai.org/proceedings/2026/129 ，https://pubmed.ncbi.nlm.nih.gov/40030513/ 。
- 本站有意覆盖 head（移除外部字体请求）、header（精简无脚本导航）；新增独立 academic layout、Scholar template 和共享论文 include，不修改 gem。

### 2026-11-18 | 本地构建与页面验证

- 类型：实验已验证。
- 环境：仓库内 `.tools/ruby` 的 Ruby 3.3.6 / Node 22；Bundler 4.0.6；Gemfile.lock 固定依赖。未修改共享 Conda/base 环境。
- 配置与验证：`JEKYLL_ENV=production bundle exec jekyll build` 成功；`npm ci`、`npm run lint:prettier` 通过；同部署流程执行 PurgeCSS。
- `bundle exec al-folio upgrade audit`：0 blocking / 0 non-blocking；两个 head/header 覆盖已经 diff 审阅、accept，并写入 `.al-folio-overrides.yml`。
- Chromium：1440、1024、768、390px，首页和 Publications 共八个页面组合；3 篇条目、姓名加粗、Accepted 空作者行为、无横向溢出、BibTeX 展开、Tab/Enter skip link、资源请求和 JS 错误检查通过。已目视桌面和手机截图。
- 渲染结果：两篇已发表条目均有真实 Paper / DOI，Endo-GSG 另有官方 PDF；无 ROBIO 假作者或链接，无模板导航，无照片框。
- 本次修正：核心 CSS 把 `.mt-5` 作为 components 层内的 important 规则；用同层的精准站点规则去除多余顶部 margin。未复制核心样式实现。
- 部署：保留 Actions → gh-pages；显式 `force: false`。未运行远端 Actions，未创建仓库，未推送。站点维护与部署步骤见 `docs/SITE_MAINTENANCE.md`。
- 局限：可选 jupyter-nbconvert 不在 PATH，当前无 notebook 内容不受影响；未测 Firefox/Safari；三篇 teaser 均缺少已确认的转载授权。

### 2026-11-18 | ROBIO 已接收未见刊标注

- 类型：用户明确要求 / 实验已验证。
- 修正：原先只写 Accepted 不够明确；现在在 `IEEE ROBIO 2026` 下方单独显示 `ACCEPTED · Not yet published`，不把接收视为正式出版。
- 修改：`_data/accepted_papers.yml`、共享论文 include、状态样式；首页与 Publications 自动同步。
- 验证：生产 Jekyll 构建成功；检查两个生成页面的状态文字和位置、每页仍为三篇论文且只有 ROBIO 显示此状态，通过。未提交、推送或部署。

### 2026-11-18 | 远端仓库创建确认

- 类型：用户明确告知 / 实际检查已验证。
- `git ls-remote origin` 成功，返回空 refs；origin 为 `git@github.com:Hansello218/Hansello218.github.io.git`，当前分支 main，`git diff --check` 通过。
- 尚未提交、推送或部署；遵循用户最初不自动推送/部署的约束，等待发布授权。

### 2026-11-18 | 改为 ChaoHe-research 项目站点

- 类型：用户明确要求 / 实验已验证。
- 取代此前用户主页方案：保留域名 `url: https://hansello218.github.io`，设置 `baseurl: /ChaoHe-research`；origin 改为 `git@github.com:Hansello218/ChaoHe-research.git`。
- 同步 AGENTS、README 和维护部署文档；本地目录保留原名，避免移动已安装的绝对路径工具环境。
- 生产构建通过；首页、Publications、404 的 canonical 与全部内部文件路径，以及 sitemap 项目路径检查通过；升级审计零问题，覆盖审计仍为两个 acknowledged。
- Chromium 在 1440/1024/768/390px 检查带项目路径的首页和 Publications，通过资源请求、状态标签、BibTeX、键盘跳转及无横向溢出检查。临时使用 4001 端口，未停止用户原有的 4000 预览进程。
- 新远端 SSH 查询仍返回 Repository not found；待用户在 GitHub Settings → General 中将原仓库改名为 ChaoHe-research。未提交、推送或部署。

### 2026-11-18 | ROBIO 最佳论文入围与仓库改名确认

- 类型：用户明确要求 / 源码与渲染已验证。
- 用户告知 ROBIO 论文入选 best paper final list；按学术英文显示 `Best Paper Finalist`。依据为用户确认，未声称已获最佳论文奖，也未补写官方获奖链接。
- 在 `_data/accepted_papers.yml` 添加 award，共享组件在 ROBIO 接收状态下方显示；保留 `ACCEPTED · Not yet published`。
- 生产构建通过；首页与 Publications 均仅 ROBIO 有入围文字，仍为三篇论文且无虚构作者。
- `git ls-remote origin` 成功返回空 refs，确认新仓库路径可访问。未提交、推送或部署。

### 2026-11-18 | 首次发布授权与检查

- 类型：用户明确要求 / 实际检查已验证。
- 用户明确授权“允许推送部署”。目标为 `Hansello218/ChaoHe-research` 的 main；SSH 远端仍为空，GitHub connector 确认是用户拥有的 public 仓库。
- 发布前生产构建、Prettier、upgrade audit 与 override audit 通过；部署使用的 action v7 标签已向官方远端核实存在。
- 准备提交当前站点改动；忽略 `.tools`、`vendor`、`_site`、`node_modules`，不上传本地环境与生成缓存。

### 2026-11-18 | 首次源码推送成功

- 类型：实际操作已验证。
- 源码提交 `42240c589516c0212529f01e4101f36c32266372` 已通过普通 `git push -u origin main` 成功推送；未 force-push。
- 初次浅克隆推送失败：远端 index-pack 报缺少预期对象。`git fetch --unshallow upstream main` 补全历史后，`git fsck --connectivity-only` 通过，重试推送成功。
- GitHub 已识别全部工作流，但首次导入后未出现 runs；本次同步发布记录后继续触发、检查部署。
- Pages 尚未启用，待 `gh-pages` 生成后选择分支发布源。当前接口无 Pages 设置更新能力，不通过修改权限或提取凭据绕过。
