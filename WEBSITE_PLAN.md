# 个人学术网站建设方案 — Yifan (Emily) Feng

> 本文档是给 Claude Code 执行用的开发计划。所有网站正文内容用英文，本文档说明用中文。
>
> **技术栈**：Jekyll + al-folio 主题 · **托管**：GitHub Pages · **网址**：https://efanfeng2-ui.github.io

---

## 0. 已确认的决策

| 项目     | 决定                                                                |
| -------- | ------------------------------------------------------------------- |
| 网站定位 | 学术优先、工业界兼顾（academic-first, industry-aware）              |
| 技术栈   | Jekyll + al-folio                                                   |
| 仓库     | 重命名为 `efanfeng2-ui.github.io`（根域名，无 baseurl）             |
| 姓名显示 | **Yifan (Emily) Feng**                                              |
| 博士毕业 | Expected **December 2026**                                          |
| 本科学位 | 双学位：B.S. Biological Sciences + B.S. Food Science and Technology |

---

## 1. ⚠️ 开工前必读：两个必须先处理的问题

### 1.1 你的论文已经正式发表了，简历还在按 preprint 写

这是我在核对时发现的最重要的一件事：

你简历里所有版本都把 Aedes aegypti 那篇写成 `bioRxiv, 2024, 1–31`。但它**已经通过同行评审、正式见刊**了：

> Liang J., Rose N.H., Brusentsov I.I., Lukyanchikova V., Karagodin D.A., **Feng Y.**, Yurchenko A.A., Sharma A., Sylla M., Lutomiah J., Badolo A., Aribodor O., Gonzalez Acosta C., Alto B.W., Wasi Ahmad N., Baricheva E.M., Tu Z., Ayala D., Gloria-Soria A., Black W.C., Powell J.R., Sharakhov I.V., McBride C.S., Sharakhova M.V. (2025).
> **"Chromosomal Inversions and Their Potential Impact on the Evolution of Arboviral Vector _Aedes aegypti_."**
> _Genome Biology and Evolution_ **17**(7): evaf118.
> DOI: [10.1093/gbe/evaf118](https://doi.org/10.1093/gbe/evaf118)

一篇 GBE 的 peer-reviewed 论文，和一篇 bioRxiv preprint，在 recruiter 和 PI 眼里完全是两个量级。**网站上必须用发表版**，同时建议你把 7 份简历、LinkedIn、Google Scholar 全部同步更新。

（顺带一提：核对时看到 Sharakhov 组 2025 年在 _STAR Protocols_ 发了 "Protocol for Hi-C-based identification of chromosomal inversions in mosquitoes"，作者里没有你。如果你实际有贡献，值得去问一下。）

### 1.2 你有两个重复的 GitHub 仓库，需要二选一

```
/Users/sunny/Desktop/Yifan/yifanWebsite/          → github.com/efanfeng2-ui/yifan-website   （外层，README 已删，未提交）
└── yifan/                                        → github.com/efanfeng2-ui/yifan           （内层，干净，就是当前工作目录）
```

嵌套 git 仓库会让后续所有操作出问题。**建议方案**：保留内层 `yifan`（干净且有正常提交历史），把它重命名成 `efanfeng2-ui.github.io`；外层 `yifanWebsite/.git` 删掉，GitHub 上的 `yifan-website` 归档或删除。

具体步骤见 §6.1。

---

## 2. 定位策略

### 核心定位句（贯穿全站的一句话）

> **I use chromosome-scale genomics and cytogenetics to understand how structural variation shapes mosquito adaptation — and how that knowledge translates into vector control.**

### 你真正的差异化优势

大多数博士要么是纯 wet-lab，要么是纯 bioinformatics。**你两边都能独立干活**，而且是在同一个课题上闭环的：

```
Hi-C 建库（湿实验）→ 基因组组装/scaffolding（干实验）→ FISH 物理定位验证（湿实验）
    → PCR breakpoint 分型（湿实验）→ 群体基因组分析 FST/PCA/AMOVA（干实验）
    → 关联到生态适应与媒介性状（生物学解释）
```

**这条完整链路就是全站的叙事主线。** 学术界看到的是"能独立完成从样本到结论的完整研究"；工业界看到的是"assay development + data analysis 双栖、能跨职能协作"。两个受众看同一套内容，各取所需——这就是"学术优先、工业兼顾"的实现方式，而不是做两套割裂的内容。

### 设计上的三个原则

1. **首页 5 秒定位** — 打开就知道：谁、研究什么、什么阶段、怎么联系、简历在哪。
2. **让图说话** — 你有 Hi-C 接触矩阵、FISH 荧光图、染色体图这类视觉冲击力极强的素材。绝大多数生物学博士主页是纯文字的，放图立刻拉开差距。
3. **可维护性** — 论文用 BibTeX 驱动，加一篇只改一个文件。别把内容写死在模板里。

---

## 3. 信息架构

```
/                     About         首页：定位、照片、研究关键词、News、快速入口
/research/            Research      三条研究主线 + 方法链路图（学术深度主场）
/publications/        Publications  BibTeX 驱动，含 Presentations
/cv/                  CV            结构化 CV + PDF 下载
/teaching/            Teaching      教学与 mentoring
/toolbox/             Toolbox       湿/干实验技能矩阵（工业界主场）
/gallery/             Gallery       显微与基因组图像（可选，强烈建议做）
```

导航栏顺序：`About · Research · Publications · CV · Teaching · Toolbox`
（Gallery 从 Research 页内链进去，不占导航栏）

**明确不做**：Blog（没内容会显得荒废，比没有更糟）、Repositories 页（GitHub 上没有可展示的代码仓库）。两个都在 `_config.yml` 里关掉。

---

## 4. 逐页内容规格

> 以下英文文案是**可直接使用的初稿**，你可以照抄或在此基础上改。

### 4.1 About（首页 `/`）

**al-folio 配置**（`_config.yml`）：

```yaml
first_name: Yifan
middle_name: (Emily)
last_name: Feng
title: Yifan (Emily) Feng
description: >
  Ph.D. Candidate in Entomology at Virginia Tech studying chromosomal
  inversions and genome evolution in mosquitoes.
keywords: mosquito genomics, chromosomal inversions, Hi-C, FISH, cytogenetics,
  population genomics, Culex pipiens, Aedes, vector biology
```

**`_pages/about.md` front matter**：

```yaml
---
layout: about
title: About
permalink: /
subtitle: >
  Ph.D. Candidate, <a href="https://www.ento.vt.edu/">Department of Entomology</a> &
  <a href="https://fralinlifesci.vt.edu/">Fralin Life Sciences Institute</a>,
  Virginia Tech · Advised by Dr. Maria Sharakhova

profile:
  align: right
  image: prof_pic.jpg
  image_circular: false
  more_info: >
    <p>Blacksburg, Virginia</p>
    <p><a href="mailto:efanfeng@vt.edu">efanfeng@vt.edu</a></p>

selected_papers: true
social: true
announcements:
  enabled: true
  scrollable: true
  limit: 5
---
```

**正文（英文初稿）**：

```markdown
I am a Ph.D. candidate in Entomology at Virginia Tech, where I study how
**chromosomal inversions** shape adaptation and speciation in mosquitoes.

Large structural rearrangements can lock together hundreds of genes and carry
them through evolution as a single unit. In disease vectors, these inversions
have been tied to traits that matter enormously for public health — climatic
tolerance, host preference, insecticide resistance. My work asks where these
inversions are, how they behave in natural populations, and what they do.

To answer that, I work across the full arc of a genomics project: I build
**Hi-C libraries** at the bench, assemble and scaffold **chromosome-scale
genomes** computationally, validate rearrangements physically by **fluorescence
in situ hybridization (FISH)**, genotype them across wild populations with
**PCR breakpoint assays**, and connect the resulting variation to ecology through
**population genomic analysis**. My dissertation applies this pipeline to the
_Culex pipiens_ complex — the vectors of West Nile virus and lymphatic
filariasis — where hybridization between forms with sharply different behaviors
makes structural variation especially consequential.

I expect to defend in **December 2026**. I am interested in roles where genome
structure meets applied biology, in academia or in industry R&D.
```

> **要点**：第二段用"为什么这重要"钩住外行读者，第三段的加粗技术词是给 recruiter 和 PI 扫读用的。既不牺牲学术深度，也不让工业界读者看不懂。

**页面底部加三个 CTA 按钮**：`Download CV (PDF)` · `Publications` · `Email me`

**News（`_news/` 集合，每条一个 `.md`）**：

```
2026-XX-XX  Presented at [conference]                        ← 待补
2025-07-XX  Our Aedes aegypti inversion paper is out in Genome Biology and Evolution
2024-11-XX  Poster presented at the ASTMH Annual Meeting, New Orleans
2024-XX-XX  Started mentoring undergraduate researchers in the Sharakhova Lab
2023-10-XX  Presented at the CeZAP Infectious Disease Symposium
```

（日期需要你补准确；ASTMH 2024 年会地点请核对）

---

### 4.2 Research（`/research/`）

学术深度的主场。三条主线，每条配一张图。

**Thrust 1 — Chromosomal inversions in the _Culex pipiens_ complex**（博士论文核心）

- 背景：_Cx. pipiens_ / _Cx. quinquefasciatus_ / _Cx. pipiens f. molestus_ 之间行为与生态差异巨大（宿主偏好、滞育、交配行为），杂交带上这些差异如何维持？
- 方法：Hi-C 检测倒位 → FISH 物理验证 → PCR breakpoint assay 分型
- 结果：FST / PCA / AMOVA 关联结构变异与生态适应
- 状态：manuscript in preparation
- 配图：Hi-C 接触矩阵（倒位在图上呈现的特征信号）

**Thrust 2 — Chromosome-scale genome assembly of _Aedes albopictus_**（2025）

- trio-binning：亲本 Illumina reads + 子代 Nanopore long reads
- Hi-C scaffolding 到染色体级别
- 候选倒位经 FISH 物理定位确认
- 状态：manuscript in preparation（对应 `albopictus_manuscript.docx`）
- 配图：FISH 荧光显微图 或 组装前后 contiguity 对比

**Thrust 3 — Comparative inversion landscapes across vector mosquitoes**

- 作为共同作者参与的 _Aedes aegypti_ 倒位研究（GBE 2025）
- 跨物种视角：倒位在不同媒介蚊中的分布规律与演化意义
- 状态：**已发表**
- 配图：染色体倒位示意图（BioRender 画）

**页面顶部放一张方法链路图**（这是整页的视觉锚点）：

```
Field / colony sampling
        ↓
Hi-C library prep  ──────────────┐
        ↓                        │
Genome assembly & scaffolding    │  wet lab ↔ dry lab
        ↓                        │  在同一课题上闭环
FISH physical validation  ───────┘
        ↓
PCR breakpoint genotyping (population scale)
        ↓
Population genomics: FST · PCA · AMOVA
        ↓
Ecological & vectorial interpretation
```

建议用 BioRender 或 Illustrator 画成横向流程图，导出 SVG。**这张图是全站最有价值的单个视觉元素** —— 它一眼说明你的差异化优势，学术和工业受众都能读懂。

**每条 Thrust 的写法模板**（英文）：

```
### <Title>
*<Status: Published in X (2025) / Manuscript in preparation>*

**The question.**  <1–2 句，为什么这个问题重要>
**The approach.**  <1–2 句，用了什么方法，技术词加粗>
**What we found.**  <1–2 句，结论。还没结果就写 what we are testing>
```

---

### 4.3 Publications（`/publications/`）

al-folio 用 `jekyll-scholar` 从 `_bibliography/papers.bib` 渲染。

**`_config.yml`**：

```yaml
scholar:
  last_name: Feng
  first_name: [Yifan, Y., Y] # 让你的名字在作者列表里自动加粗
  source: /_bibliography/
  bibliography: papers.bib
  bibliography_template: bib
  sort_by: year
  order: descending

enable_publication_badges:
  altmetric: true
  dimensions: true
  google_scholar: true
```

**`_bibliography/papers.bib`**（完整初稿，可直接用）：

```bibtex
@article{liang2025aedes,
  title     = {Chromosomal Inversions and Their Potential Impact on the Evolution
               of Arboviral Vector {Aedes} aegypti},
  author    = {Liang, Jiangtao and Rose, Noah H. and Brusentsov, Ilya I. and
               Lukyanchikova, Varvara and Karagodin, Dmitriy A. and Feng, Yifan and
               Yurchenko, Andrey A. and Sharma, Atashi and Sylla, Massamba and
               Lutomiah, Joel and Badolo, Athanase and Aribodor, Ogechukwu and
               Gonzalez Acosta, Cassandra and Alto, Barry Wilmer and
               Wasi Ahmad, Nazni and Baricheva, Elina M. and Tu, Zhijian and
               Ayala, Diego and Gloria-Soria, Andrea and Black, William C. and
               Powell, Jeffrey R. and Sharakhov, Igor V. and McBride, Carolyn S. and
               Sharakhova, Maria V.},
  journal   = {Genome Biology and Evolution},
  volume    = {17},
  number    = {7},
  pages     = {evaf118},
  year      = {2025},
  doi       = {10.1093/gbe/evaf118},
  url       = {https://doi.org/10.1093/gbe/evaf118},
  publisher = {Oxford University Press},
  abbr      = {GBE},
  selected  = {true},
  preview   = {aedes_inversions.jpg},
  abstract  = {<粘贴 GBE 页面上的官方 abstract>}
}

@article{feng2026culex,
  title    = {Chromosomal inversions differentiate mosquitoes in the
              {Culex} pipiens complex},
  author   = {Feng, Yifan and Lukyanchikova, Varvara and Liang, Jiangtao and
              Brusentsov, Ilya I. and Karagodin, Dmitriy A. and Fritz, Megan L. and
              Sharakhova, Maria V.},
  journal  = {Manuscript in preparation},
  year     = {2026},
  abbr     = {In prep.},
  selected = {true},
  preview  = {culex_hic.jpg}
}

@article{feng2026albopictus,
  title    = {<Aedes albopictus 基因组组装论文标题 — 待补>},
  author   = {Feng, Yifan and others},
  journal  = {Manuscript in preparation},
  year     = {2026},
  abbr     = {In prep.}
}
```

**Presentations** 单独一个小节（在 `_pages/publications.md` 的 bibliography 下面手写，不要塞进 .bib）：

```markdown
## Conference Presentations

**Feng, Y.**, & Lahondère, C. (November 2024).
_Hi-C based discovery of structural variants in the Culex pipiens complex._
Poster presentation, **American Society of Tropical Medicine and Hygiene (ASTMH)
Annual Meeting**.

**Feng, Y.**, Lukyanchikova, V., Liang, J., Brusentsov, I. I., Karagodin, D. A.,
Fritz, M. L., & Sharakhova, M. V. (October 2023).
_Chromosomal inversions differentiate mosquitoes in the Culex pipiens complex._
**CeZAP Infectious Disease Symposium**, Blacksburg, VA.
```

> **注意**：`in preparation` 的稿子放在网站上是学术界通行做法，但务必标注清楚状态，绝不能和已发表的混在一起不加区分。上面的 `abbr` 字段就是干这个的。

---

### 4.4 CV（`/cv/`）

**两条腿**：页面顶部一个显眼的 **Download CV (PDF)** 按钮 + 页面内完整 HTML 版本（利于 SEO 和手机阅读）。

al-folio 支持用 `_data/cv.yml` 生成结构化 CV。章节顺序（学术优先）：

1. **Basics** — 姓名、邮箱、地点、一句话定位
2. **Education**
   - Ph.D. Entomology, Virginia Tech, 2021 – Dec 2026 (expected)
     Advisor: Dr. Maria Sharakhova
     Dissertation: _Chromosomal Inversions Differentiate Mosquitoes in the Culex pipiens Complex_
   - B.S. Biological Sciences, Virginia Tech, 2017 – 2021
   - B.S. Food Science and Technology, Virginia Tech, 2017 – 2021
3. **Research Experience**
   - Graduate Research Assistant — Dept. of Entomology & Fralin Life Sciences Institute, Virginia Tech · Aug 2021 – present
   - Undergraduate Researcher — Dept. of Food Science and Technology, Virginia Tech · Sep 2020 – Dec 2020
     _Aerosolized Listeria contamination from cavitation treatment of raw produce_（MATLAB 建模 + 高性能计算模拟）
   - Undergraduate Research Assistant — Food Microbiology Lab, Virginia Tech · Jan 2020 – May 2021
   - Research Intern — Molecular Genetics Laboratory · Mar 2020 – Dec 2021
4. **Publications**（链接到 `/publications/`，不重复列）
5. **Presentations**
6. **Teaching & Mentoring**
7. **Grants & Awards** — GRDP、F31（**见 §7，需要你确认是"撰写经历"还是"获资助"**）
8. **Professional Service & Membership**
   - Volunteer, Blacksburg Mosquito Control Initiative
   - Member, Entomological Society of America
   - Member, Virginia Mosquito Control Association
9. **Technical Skills**（简版，详版在 Toolbox）

**PDF 放在** `assets/pdf/Yifan_Feng_CV.pdf`。建议由 `main.tex` 编译产出——但 `main.tex` 里有几处 `Long long line of blah blah...` 的占位符文字必须先清掉（见 §7）。

---

### 4.5 Teaching（`/teaching/`）

```markdown
## Teaching

### ENT 2004 — Insects and Human Society

**Graduate Teaching Assistant**, Virginia Tech · Aug 2023 – May 2024

A general-education course introducing non-biology majors to entomology.
I led weekly laboratory sessions and discussion sections covering insect
taxonomy, physiology, and ecology; developed visual teaching materials; and
graded lab reports and examinations.

## Mentoring

### Undergraduate Researchers, Sharakhova Lab · 2024 – 2025

I mentored two undergraduate researchers through full project cycles —
from PCR optimization and troubleshooting, through experimental design and
data interpretation, to scientific writing.

## Outreach

**Blacksburg Mosquito Control Initiative** — Volunteer field collection and
public outreach on vector-borne disease prevention.
```

---

### 4.6 Toolbox（`/toolbox/`）— 工业界主场

这一页是"学术优先、工业兼顾"里"工业"的落点。核心呈现方式：**湿实验 / 干实验双栏技能矩阵**，直观展示你两边都能干。

```markdown
# Toolbox

I work at the bench and at the terminal. Below is what I can do independently,
without supervision, today.

|                               | **Wet Lab**                                                                                                   | **Dry Lab**                                                                                  |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| **Nucleic acids**             | DNA/RNA extraction · PCR · qPCR · RT-qPCR · ddPCR · gel electrophoresis · cloning · nucleic acid purification | —                                                                                            |
| **Library prep & sequencing** | Hi-C library preparation · Illumina library prep · Sanger sequencing · Nanopore long-read workflows           | Read QC · adapter trimming · alignment (BWA, Minimap2)                                       |
| **Genome assembly**           | —                                                                                                             | Hi-C scaffolding (Juicer, Juicebox) · trio-binning · contiguity assessment · gene annotation |
| **Cytogenetics & imaging**    | Chromosome preparation · FISH probe synthesis & hybridization · fluorescence microscopy (Zeiss ZEN)           | Image analysis (ImageJ) · physical map construction                                          |
| **Population genetics**       | PCR breakpoint genotyping at population scale                                                                 | FST · PCA · AMOVA · STRUCTURE · PLINK                                                        |
| **Cell & assay work**         | Mammalian and insect cell culture · sterile technique · ELISA · Western blot · BSL-2 practice                 | —                                                                                            |
| **Programming & analysis**    | —                                                                                                             | R (ggplot2) · Python · Linux/Unix · MATLAB · Galaxy · Geneious · BLAST/NCBI                  |
| **Communication**             | Lab notebook & data documentation · reagent inventory · safety compliance                                     | Scientific writing · grant writing (GRDP, F31) · GraphPad Prism · BioRender                  |
```

**页面底部加一段 "Beyond the bench"**（这段是给 hiring manager 看的软技能，用具体事实说话，不要空喊）：

```markdown
## Beyond the bench

- **Independent project ownership** — I designed, executed, and troubleshot my
  dissertation projects end-to-end, from assay development through publication.
- **Cross-institutional collaboration** — My published work involved
  coordination across research groups in the United States, Russia, France,
  Senegal, Kenya, Burkina Faso, Nigeria, Mexico, and Malaysia.
- **Mentoring** — Trained two undergraduate researchers in molecular protocols,
  experimental design, and scientific writing.
- **Scientific communication** — Poster and oral presentations at national
  meetings including ASTMH; grant proposal writing (GRDP, F31).
```

> 第二条的国家清单直接来自 GBE 论文的作者单位——这是真实、可核查、且极有说服力的国际协作证据，比任何 "excellent teamwork skills" 都强。

---

### 4.7 Gallery（`/gallery/`）— 可选但强烈建议

你手上有普通博士主页拿不出来的东西：Hi-C 接触矩阵、FISH 荧光图、染色体核型图。放 6–10 张，每张配 1–2 句说明。

al-folio 的 `projects` 集合可以改造成图集，或直接用 `_pages/gallery.md` + 图片网格。

每张图必须有 caption，说明"这是什么、怎么来的、说明了什么"。**注意：只放已发表或你有权公开的图，未发表数据先和 Sharakhova 老师确认。**

---

## 5. 视觉设计规范

### 配色

主色用 **Virginia Tech Chicago Maroon `#861F41`**，辅色 **Burnt Orange `#E5751F`**（少量点缀，用于 hover / badge）。理由：立刻建立学校身份识别，和 al-folio 默认的蓝紫色拉开距离，且在深浅两种模式下都好看。

al-folio 通过 SCSS 变量控制主题色。**执行时先在拉下来的模板里确认实际机制**（新版 al-folio 正在迁移到 Tailwind，主题色的定义位置可能与旧版文档不同）：

```bash
grep -rn "global-theme-color\|theme-color" _sass/ tailwind.config.js 2>/dev/null | head -20
```

找到后设置：

```scss
--global-theme-color: #861f41;
--global-hover-color: #e5751f;
```

同时在 `_config.yml` 里设 `enable_darkmode: true`，并**在深色模式下实测一遍**——`#861F41` 在深色背景上对比度偏低，可能需要调亮到 `#B03A5B` 左右。

### 字体与排版

al-folio 默认字体（Roboto / Roboto Slab）已经够用，不建议折腾。物种名（_Culex pipiens_、_Aedes aegypti_ 等）**全站必须斜体**——这是生物学写作的硬规范，写错会被同行扣印象分。建议在 CSS 里加一个工具类：

```scss
.sp {
  font-style: italic;
}
```

### 照片

需要一张**专业头像**（`assets/img/prof_pic.jpg`）：正方形，≥ 800×800，光线均匀，实验室或户外背景都可以，但要清爽。这是首页最先被看到的元素之一。

如果暂时没有，可以先用一张你自己拍的显微图或 Hi-C 矩阵图代替，但优先补上真人照片——学术主页有脸和没脸，信任感差很多。

### 响应式与可访问性

- 手机上必须能正常读（al-folio 默认已处理，但要实测）
- 所有图片必须有 `alt` 文字
- 表格（Toolbox 那张）在窄屏上要能横向滚动，不能撑破页面

---

## 6. 技术实施步骤

### 6.1 仓库整理（先做，且需要你在 GitHub 网页上操作）

```bash
# 1. 备份当前状态
cd /Users/sunny/Desktop/Yifan/yifanWebsite/yifan
git log --oneline          # 确认历史干净

# 2. 删除外层嵌套的 git 仓库（只删 .git，不动文件）
rm -rf /Users/sunny/Desktop/Yifan/yifanWebsite/.git
```

**然后在 GitHub 网页上**（这步只能你自己做）：

1. 打开 `github.com/efanfeng2-ui/yifan` → Settings → 把仓库名改为 **`efanfeng2-ui.github.io`**
2. 把 `github.com/efanfeng2-ui/yifan-website` 归档（Settings → Archive）或删除

```bash
# 3. 更新本地 remote
git remote set-url origin https://github.com/efanfeng2-ui/efanfeng2-ui.github.io.git
git remote -v              # 验证
```

> al-folio 官方文档明确要求：想用根域名 `https://<username>.github.io`，仓库名**必须**恰好是 `<username>.github.io`。

### 6.2 引入 al-folio

有两种方式，各有取舍：

**方式 A（推荐）— GitHub "Use this template"**
在 GitHub 上用 al-folio 的 template 按钮建一个新仓库，然后把内容合并到 `efanfeng2-ui.github.io`。优点是文件结构最标准、后续升级最顺；缺点是要处理一次合并。

**方式 B — 本地拉取模板文件**

```bash
cd /tmp && git clone --depth 1 https://github.com/alshedivat/al-folio.git
# 把除 .git 外的所有文件复制进项目目录
```

优点是保留现有仓库历史，操作直接。**Claude Code 执行时选方式 B**，更可控。

复制完成后：

```bash
cd /Users/sunny/Desktop/Yifan/yifanWebsite/yifan
bundle install
bundle exec jekyll serve            # → http://localhost:4000
```

> 需要本机有 Ruby 和 Bundler。如果 Ruby 环境有问题，al-folio 官方也支持 Docker：`docker compose up` → http://localhost:8080。**先跑通空白模板再改内容**，不要一上来就大改。

### 6.3 关键配置（`_config.yml`）

```yaml
url: https://efanfeng2-ui.github.io
baseurl: # ← 留空，但不要删掉这一行

title: Yifan (Emily) Feng
first_name: Yifan
middle_name: (Emily)
last_name: Feng

email: efanfeng@vt.edu
description: >
  Ph.D. Candidate in Entomology at Virginia Tech studying chromosomal
  inversions and genome evolution in mosquitoes.

# 社交链接 — 逐项确认后填，没有的留空，不要填占位符
scholar_userid: # Google Scholar ID — 见 §7
orcid_id: # ORCID — 见 §7
linkedin_username: # 见 §7
github_username: efanfeng2-ui
research_gate_profile:

enable_darkmode: true
enable_google_analytics: false # 需要再开

# 关掉不用的功能
blog_name: # 不做 blog
```

### 6.4 部署到 GitHub Pages

al-folio 自带 `.github/workflows/deploy.yml`，流程是：push 到 `main` → Actions 构建 → 产物推到 `gh-pages` 分支 → Pages 从 `gh-pages` 发布。

**需要你在 GitHub 网页上配置**（Claude Code 做不了）：

1. 仓库 → **Actions** 标签页 → 启用 GitHub Actions
2. **Settings → Actions → General → Workflow permissions** → 选 **"Read and write permissions"**
3. push 到 `main`，等 Actions 跑完
4. 确认自动生成了 `gh-pages` 分支（**不要手动编辑这个分支**）
5. **Settings → Pages** → Source 设为 `gh-pages` 分支

> 第 2 步最容易漏。权限没给够的话 Actions 会构建成功但推送失败，表现为"没有 gh-pages 分支"。

首次部署通常 3–5 分钟生效。

### 6.5 上线前自查清单

- [ ] `bundle exec jekyll serve` 本地无报错、无 broken link
- [ ] 手机尺寸下所有页面正常（Chrome DevTools 响应式模式）
- [ ] 深色模式下配色对比度足够
- [ ] 所有物种名斜体
- [ ] 所有图片有 alt 文字
- [ ] 所有外链（DOI、VT 院系、LinkedIn）可点且正确
- [ ] CV PDF 能正常下载，且**不含任何占位符文字**
- [ ] `mailto:` 链接正确
- [ ] favicon 已替换（别留 al-folio 默认的）
- [ ] Google 搜 "Yifan Feng Virginia Tech" 能找到（上线后 1–2 周）

---

## 7. ⚠️ 待你核对的事实清单

以下是我在 7 份简历里发现的**互相矛盾或信息缺失**之处。Claude Code 会按左侧"我的处理"先填，**但你上线前必须逐条核对**——学术主页上的事实错误代价很高。

| #   | 问题                  | 各版本的说法                                                                                                                    | 我的处理                                                                                       |
| --- | --------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| 1   | 博士毕业时间          | Dec 2025 / Dec 2026                                                                                                             | **Dec 2026**（你已确认）                                                                       |
| 2   | 博士入学时间          | 2021 / 2022 / "Aug 2021"                                                                                                        | 用 **2021**，与 "Aug 2021 – Present" 一致                                                      |
| 3   | 本科学位              | 双学位 Biology + Food Science / Biological Sciences 主修 + Food Science 辅修 / "Biological Sciences and Computational Modeling" | **双学位**（你已确认）。但"Computational Modeling"这个说法只出现在一份里，需你确认是否真实存在 |
| 4   | 电话号码              | +1 540 000 0000（明显占位符）/ (848) 285-9808                                                                                   | **网站上不放电话**（学术主页放邮箱即可，放电话会招垃圾骚扰）                                   |
| 5   | LinkedIn URL          | `linkedin.com/in/yifan-feng` / `linkedin.com/` / `www.linkedin.com/in/`（后两个是占位符）                                       | **需要你提供真实 URL**，否则不放这个链接                                                       |
| 6   | Google Scholar        | 简历里完全没有                                                                                                                  | **建议你去建一个**——GBE 论文已发表，学术主页配 Scholar 是标配                                  |
| 7   | ORCID                 | 简历里完全没有                                                                                                                  | **建议注册**（免费，5 分钟）。GBE 投稿时可能已经有了，去查一下                                 |
| 8   | GRDP / F31            | 只写了 "grant writing"，没说结果                                                                                                | 需明确是**"撰写经历"还是"获得资助"**。措辞差别很大，写错是学术诚信问题                         |
| 9   | ASTMH 2024 会议地点   | 未注明                                                                                                                          | 需补（2024 年 ASTMH 年会在新奥尔良，请自行确认）                                               |
| 10  | `main.tex` 占位符     | 有 4 处 `Long long line of blah blah that will wrap...` 和一个 `\href{https://your-link.com}{[Link to Demo]}`                   | **编译 CV PDF 前必须全部清除**                                                                 |
| 11  | 本科研究院系          | Food Science and Technology / Biological Systems Engineering / Food Microbiology Lab（三种说法）                                | 需你确认 Listeria 那个项目到底挂在哪个院系                                                     |
| 12  | _Ae. albopictus_ 论文 | 有 `albopictus_manuscript.docx`，但简历publication列表里没有                                                                    | 需你提供**正式标题和作者列表**                                                                 |
| 13  | 论文发表状态          | 全部按 bioRxiv preprint 写                                                                                                      | **已改为 GBE 2025 正式版**（见 §1.1）——请同步更新所有简历和 LinkedIn                           |

---

## 8. 分阶段执行计划

建议分四步走，**每步跑通再进下一步**，不要一次性全做完再调试。

### Phase 1 — 地基（先让空白站点跑起来）

1. 整理仓库（§6.1）——含你在 GitHub 网页上的重命名操作
2. 引入 al-folio 模板，`bundle install` 跑通
3. 填 `_config.yml` 基础配置
4. 关掉 blog、repositories 等不用的功能
5. 配好 GitHub Actions 并**成功部署一次空白站点**

> ✅ **验收标准**：`https://efanfeng2-ui.github.io` 能打开一个 al-folio 默认页面。
> 地基不通就往下做，后面每个问题都会变成复合问题。

### Phase 2 — 核心内容

6. About 首页（§4.1）
7. Publications + `papers.bib`（§4.3）—— 用 §1.1 的 GBE 正式版
8. CV 页面 + `_data/cv.yml`（§4.4）
9. 清理 `main.tex` 占位符 → 编译 PDF → 放进 `assets/pdf/`

> ✅ **验收标准**：一个陌生人打开网站，能在 1 分钟内说清你是谁、做什么、发过什么。
> **到这一步网站已经可以对外用了**——即使后面暂时不做，也不丢人。

### Phase 3 — 深度与差异化

10. Research 页面（§4.2）—— 含方法链路图
11. Toolbox 页面（§4.6）
12. Teaching 页面（§4.5）
13. VT 配色、favicon、头像

> ✅ **验收标准**：能同时满足 PI 看学术深度、hiring manager 看可迁移技能。

### Phase 4 — 打磨

14. Gallery 图集（§4.7）
15. News 时间线
16. 深色模式实测、响应式实测
17. SEO：`description`、`keywords`、Open Graph 预览图
18. 走一遍 §6.5 上线自查清单

---

## 9. 上线之后

- **同步更新**：LinkedIn、Google Scholar、ORCID、简历签名档、邮件签名，全部加上网站链接
- **GBE 论文状态**：7 份简历全部从 "bioRxiv 2024" 改成 "GBE 2025"（§1.1）
- **维护节奏**：论文接收、会议报告、答辩日期确定时更新。**建了不维护的网站比没有更糟**——所有内容都设计成改一个文件就能更新，就是为了降低维护成本
- **答辩前**：把 Research 页面升级成"论文成果展示"，加上答辩日期和最终结果

---

## 附录 A — 完整内容清单

Claude Code 执行时的事实来源，全部提取自 `/Users/sunny/Desktop/Yifan/68e2e4a8ef5b9104f321613e/`。

**身份**
Yifan (Emily) Feng · Ph.D. Candidate, Department of Entomology & Fralin Life Sciences Institute, Virginia Tech · Blacksburg, VA · efanfeng@vt.edu · Advisor: Dr. Maria Sharakhova · Expected Dec 2026

**学位**

- Ph.D. Entomology, Virginia Tech, 2021 – Dec 2026 (expected)
  Dissertation: _Chromosomal Inversions Differentiate Mosquitoes in the Culex pipiens Complex_
  Coursework: Molecular Genetics, Bioinformatics, Experimental Design, Biochemistry, Genomics
- B.S. Biological Sciences, Virginia Tech, 2017 – 2021
- B.S. Food Science and Technology, Virginia Tech, 2017 – 2021

**研究经历**

1. Graduate Research Assistant — VT Entomology / Fralin Life Sciences Institute · Aug 2021 – present
   Hi-C scaffolding · Nanopore sequencing · FISH cytogenetic mapping · PCR breakpoint assays · FST/AMOVA/PCA · 蚊虫种群维护 · 分子解剖 · 荧光显微成像 · 指导 2 名本科实习生
2. Graduate Teaching Assistant — ENT 2004 Insects and Human Society · Aug 2023 – May 2024
3. Undergraduate Researcher — VT Food Science and Technology · Sep 2020 – Dec 2020
   Aerosolized _Listeria_ contamination from cavitation treatment of raw produce · microbubble treatment · MATLAB · 高性能计算模拟
4. Undergraduate Research Assistant — Food Microbiology Lab, VT · Jan 2020 – May 2021
5. Research Intern — Molecular Genetics Laboratory · Mar 2020 – Dec 2021

**项目**

1. Chromosomal Inversions in the _Culex pipiens_ Complex（博士论文核心）
2. Hi-C Genome Assembly of _Aedes albopictus_（2025，trio-binning + Nanopore）
3. Hybrid Zone Genotyping in _Culex pipiens_ Complex（2024，Virginia 杂交带）
4. Aerosolized _Listeria_ Contamination（本科）

**发表**

1. Liang et al. (2025) _Genome Biology and Evolution_ 17(7):evaf118 — **已发表**，DOI 10.1093/gbe/evaf118
2. Feng et al. — _Culex pipiens_ inversions — in preparation
3. Feng et al. — _Aedes albopictus_ 组装 — in preparation（标题待补）

**会议**

1. ASTMH Annual Meeting, Nov 2024 — Poster（与 C. Lahondère）
2. CeZAP Infectious Disease Symposium, Blacksburg, Oct 2023

**服务与会员**
Volunteer, Blacksburg Mosquito Control Initiative · Member, Entomological Society of America · Member, Virginia Mosquito Control Association

**技能**（完整清单见 §4.6 表格）

---

## 附录 B — 参考链接

- al-folio 主仓库 — https://github.com/alshedivat/al-folio
- al-folio 安装文档 — https://github.com/alshedivat/al-folio/blob/main/docs/INSTALL.md
- GBE 论文 — https://doi.org/10.1093/gbe/evaf118
- GitHub Pages 文档 — https://docs.github.com/en/pages
- VT Entomology — https://www.ento.vt.edu/
- Fralin Life Sciences Institute — https://fralinlifesci.vt.edu/
