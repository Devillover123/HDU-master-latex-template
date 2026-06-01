# 杭州电子科技大学硕士学位论文 LaTeX 模板

本模板基于 [wennboo/HDU-latex-template-for-master](https://github.com/wennboo/HDU-latex-template-for-master) 修改而来，特此感谢原作者 [wennboo](https://github.com/wennboo) 的贡献。

原模板支持本科毕业设计（论文）、学术/专业硕士、（工程）博士等多种学位类型。本版本在原模板基础上精简，**仅保留硕士学位论文相关模板**，方便课题组后续同学快速上手使用。

## 模板模式

在 `main-thesis.tex` 中通过 `\documentclass[<mode>]{hdu-thesis}` 选择模式：

| 模式 | 说明 |
|---|---|
| `master` | 学术型硕士学位论文模板（最终版） |
| `promaster` | 专业学位硕士学位论文模板（最终版） |
| `master_review` | 学术型硕士送审模板（盲审用，隐藏个人信息） |
| `promaster_review` | 专业学位硕士送审模板（盲审用，隐藏个人信息） |

> **学位版与送审版的页面差异：** 学位论文（`master`/`promaster`）打印时需要每个章节从奇数页（右侧）起始，因此可能自动插入空白页填充。送审版（`master_review`/`promaster_review`）因盲审专家直接查看电子版 PDF，取消了强制奇数页起始的设置（即使用 `openany`），不会出现空白填充页。

## 项目结构

```
latex-template/
├── main-thesis.tex          # 主文件：论文元信息、文档结构编排
├── hdu-thesis.cls           # 文档类：页眉页脚、章节格式、参考文献等全局样式
├── hdu-thesis.cfg           # 配置文件：封面生成、原创性声明、学位类型定义
├── hdu-thesis.bst           # 参考文献格式文件（GB/T 7714-2005）
├── latexmkrc                # latexmk 自动编译配置
├── chapter/                 # 各章节 .tex 文件
│   ├── introduction.tex     #   第一章：绪论
│   ├── preliminary.tex      #   第二章：基础理论
│   ├── cha_3.tex            #   第三章：研究内容一
│   └── cha_4.tex            #   第四章：研究内容二
├── contents/                # 摘要、致谢等附属内容
│   ├── cnabstract.tex       #   中文摘要
│   ├── enabstract.tex       #   英文摘要
│   ├── acknowledgement.tex  #   致谢
│   ├── personalresult.tex   #   攻读学位期间取得的成果
│   └── appendix.tex         #   附录
├── ref/
│   └── reference.bib        # BibTeX 参考文献数据库
└── pic/                     # 图片资源目录（\graphicspath 默认指向此处）
```

### 各文件作用

| 文件 | 作用 | 是否需要修改 |
|---|---|---|
| `main-thesis.tex` | **论文主文件**，设置标题、作者、导师等信息，定义文档结构（章节顺序） | **是** — 填入个人信息、调整章节顺序 |
| `hdu-thesis.cls` | 全局格式控制：字体、字号、行距、页眉页脚、章节编号、公式/图表编号等 | **一般不需要** — 除非学校格式要求变化 |
| `hdu-thesis.cfg` | 封面生成逻辑、原创性声明内容、学位类型对应的中英文字符串 | **一般不需要** — 除非封面格式变化 |
| `hdu-thesis.bst` | 参考文献著录格式（基于 GB/T 7714-2005） | **不需要** |
| `chapter/*.tex` | 各章节正文内容 | **是** — 替换为自己的章节内容 |
| `contents/cnabstract.tex` | 中文摘要及关键词 | **是** |
| `contents/enabstract.tex` | 英文摘要及关键词 | **是** |
| `contents/acknowledgement.tex` | 致谢 | **是** |
| `contents/personalresult.tex` | 攻读学位期间取得的成果（论文、专利等） | **是** |
| `ref/reference.bib` | BibTeX 格式的参考文献条目 | **是** — 替换为自己的参考文献 |

## 快速开始

### 环境准备

推荐使用 **TeX Live + VS Code（LaTeX Workshop 插件）** 组合。

- TeX Live 下载：https://tug.org/texlive/
- VS Code 插件：搜索安装 `LaTeX Workshop`

### 第一次使用

1. **修改论文信息：** 编辑 `main-thesis.tex`，将 `\title`、`\author`、`\advisor`、`\school`、`\major`、`\authornumber` 等命令中的占位信息替换为自己的信息。

2. **编写章节内容：** 在 `chapter/` 目录下创建或修改各章节 `.tex` 文件，通过 `main-thesis.tex` 中的 `\input{}` 命令引入。

3. **添加参考文献：** 在 `ref/reference.bib` 中添加 BibTeX 格式的文献条目，正文中使用 `\cite{}`（直接引用）或 `\citep{}`（上标引用）引用。

4. **放置图片：** 将论文中使用的图片放入 `pic/` 目录，正文中通过 `\includegraphics{<文件名>}` 引用（无需带路径前缀）。

### 编译

推荐使用 `latexmk` 一键编译：

```bash
latexmk main-thesis.tex
```

清理编译缓存：

```bash
latexmk -c
```

手动编译（需要多次运行以处理交叉引用和参考文献）：

```bash
xelatex main-thesis.tex
bibtex main-thesis.aux
xelatex main-thesis.tex
xelatex main-thesis.tex
```

> **注意：** 必须使用 **XeLaTeX** 引擎编译，模板使用 `xeCJK` 宏包处理中文字体，pdfLaTeX 无法编译。

---

## 写作指南

### 一、封面信息

封面信息在 `main-thesis.tex` 导言区通过以下命令设置：

| 命令 | 参数说明 | 需要填写 |
|---|---|---|
| `\title{中文标题}{英文标题}` | 论文题目（中/英） | **是** |
| `\author{中文名}{英文名}` | 作者姓名 | **是** |
| `\advisor{姓名~职称}{Prof. Name}` | 指导教师 | **是** |
| `\secondadvisor{姓名~职称}{Prof. Name}` | 第二指导教师（无则注释掉） | 视情况 |
| `\school{中文学院}{英文学院}` | 所在学院 | **是** |
| `\major{中文专业}{英文专业}` | 专业名称 | **是** |
| `\majorfield{专业领域中文名}{Major Field in English}` | 专业领域（仅专硕 promaster 模式封面显示） | 视情况 |
| `\authornumber{学号}` | 学号 | **是** |
| `\authordirection{中文方向}{英文方向}` | 研究方向（仅盲审模式使用） | 视情况 |
| `\completedate{年}{月}{英文月}` | 完成日期，如 `{2026}{5}{May}` | **是** |
| `\confidential{密级}` | 密级（非国防项目留空） | 视情况 |
| `\delaypublic{是/否}` | 是否延期公开 | **是** |
| `\schoolcode{10336}` | 学校代码（默认 10336） | 一般不需要 |

> **注意事项：**
> - 封面由本模板作者自行设计，与学院给出的 Word 模板在布局上存在一定差异，但核心内容（题目、作者、导师、学院、专业、学号、完成日期等）均完整包含，可以正常使用。
> - 如果论文标题过长导致封面排版不美观，或者希望自行调整封面各元素间距，请前往 `hdu-thesis.cfg` 文件中修改 `\thetitlepage@master@one`（学术硕士封面）或 `\thetitlepage@promaster@one`（专业硕士封面）的定义，其中关键间距处均有注释标记。

### 二、盲审（送审）注意事项

使用送审模式（`master_review` / `promaster_review`）时，需要注意以下几点：

**1. 盲审不包含的内容**

根据学院盲审要求，送审版 PDF 中不允许出现以下内容，应在 `main-thesis.tex` 中注释掉（模板在送审模式下会自动切换为盲审封面并跳过原创性声明，但致谢和个人成果的 `\input{}` 命令仍需手动注释）：

```latex
% \makecover          % 学位版封面（送审版由 \documentclass 自动生成盲审封面）
% \makedeclaration    % 原创性声明（含签名等个人信息）
% \input{contents/acknowledgement.tex}  % 致谢
% \input{contents/personalresult.tex}   % 攻读学位期间取得的成果
```

> **注意：** 盲审模板不包含中英文标题页（即 `\thetitlepage@master@two` 对应的内封面页）以及原创性声明。此外，本模板在盲审模式下依然保留了**图目录**和**表目录**，这符合学位论文的写作规范，无需删除。

**2. 个人成果放入附录**

攻读学位期间取得的成果虽然不能单独成节出现，但需要放入附录中，**并隐去所有个人信息**（作者姓名、导师姓名、论文标题中可能暴露身份的关键词等）。具体做法：

- 将成果内容写入 `contents/appendix.tex`
- 在 `main-thesis.tex` 中取消 `\input{contents/appendix.tex}` 的注释
- 成果内容中涉及姓名处用 "XXX" 或 "本人" 替代

盲审后的最终版可以继续使用附录展示成果的方式，届时可以正常展示个人信息。

**3. 无空白填充页**

送审版取消了学位版中强制章节从奇数页起始的规则（`openany`），PDF 中不会因章节末尾的空白而出现多余的填充页。

**4. 页眉显示**

送审版的页眉统一显示 "浙江省硕士学位论文"，而非 "杭州电子科技大学硕士学位论文"。个人信息（如作者姓名等）不出现在页眉中。

### 三、中英文摘要

中英文摘要分别写入 `contents/cnabstract.tex` 和 `contents/enabstract.tex`。

- 中文摘要使用 `\cnabstract` 环境，中文关键词使用 `\cnkeyword{}` 命令，**多个关键词之间用中文逗号（，）隔开**。
- 英文摘要使用 `\enabstract` 环境，英文关键词使用 `\enkeyword{}` 命令，**多个关键词之间用英文逗号（,）隔开**。

示例：

```latex
% 中文摘要 (contents/cnabstract.tex)
\cnabstract

这里是中文摘要的正文内容……

\cnkeyword{关键词1，关键词2，关键词3，关键词4}

% 英文摘要 (contents/enabstract.tex)
\enabstract

Here is the English abstract content……

\enkeyword{Keyword1, Keyword2, Keyword3, Keyword4}
```

> **注意：** 中英文关键词分别使用中文/英文逗号分隔，符合学位论文写作规范。

### 四、学位论文正文撰写

正文是学位论文的核心部分，使用者需要根据自身论文的实际情况，掌握以下 LaTeX 学术写作的基础规范：

**文字格式：**
- **中文加粗**使用 `\heiti`（黑体），**英文/数字加粗**使用 `\textbf{}`。模板中的 `\bfseries` 为全局加粗命令，作用于其后所有文本，需配合花括号 `{}` 限定作用范围。
- **字体大小**：模板提供了从 `\chuhao`（42pt）到 `\qihao`（5.5pt）的完整中文字号命令，正文默认小四号（12pt）。

**数学公式：**
- **行内公式**使用 `$...$`，**行间编号公式**使用 `\begin{equation}...\end{equation}`，**多行对齐公式**推荐 `\begin{align}...\end{align}`。
- 变量符号约定俗成使用**斜体**（`$x$`），矩阵和向量根据学科习惯使用**粗体**（`\mathbf{X}` 或 `\boldsymbol{x}`）。
- 矩阵环境可选择 `pmatrix`（圆括号）、`bmatrix`（方括号）等；张量建议自行定义宏命令（如 `\newcommand{\tensor}[1]{\mathbf{#1}}`）以保持全文一致。

**段落与版式：**
- 模板已设置首行缩进 2 字符（24pt）、1.391 倍行距，无需额外调整。正文中如需强制换行但不另起段落，使用 `\\`；如需另起段落且不缩进，使用 `\noindent`。

以上内容需要使用者自行学习和配合使用，建议参考权威 LaTeX 教程（如《一份不太简短的 LaTeX 2ε 介绍》）及本模板各章节中的示例代码。

### 五、图、表

#### 5.1 插入图片

图片文件统一放入 `pic/` 目录，`\graphicspath` 已默认指向此处，因此 `\includegraphics` 中只需写文件名，无需带路径前缀。

**调整图片大小的常用方式：**

| 方式 | 示例 | 说明 |
|---|---|---|
| 相对缩放 | `[scale=0.8]` | 缩放至原图的 80%，保持宽高比 |
| 固定宽度 | `[width=0.8\textwidth]` | 宽度固定为文本宽度的 80%，高度自适应 |
| 固定高度 | `[height=6cm]` | 高度固定为 6cm，宽度自适应 |
| 同时指定 | `[width=0.6\textwidth, height=5cm, keepaspectratio]` | 限制最大宽高，同时保持宽高比 |

**插入矢量图（.svg）的方法：**

大论文和小论文均推荐使用矢量图以获得最佳清晰度。操作流程如下：

1. **绘制并导出 .svg：** 在任意绘图软件（如 draw.io、Visio、Inkscape、Matplotlib 等）中绘制图表，导出为 `.svg` 格式的矢量图。

2. **浏览器打印为 PDF：** 用 Edge 浏览器打开 `.svg` 文件，点击页面空白处右键 → **打印** → **另存为 PDF**。在此步骤中可以设置缩放比例来适应 A4 页面大小；也可以不调整，等插入论文时再通过 `[scale]` 或 `[width]` 调整大小。

3. **裁剪空白区域（关键步骤）：** 上一步生成的 PDF 包含了整张 A4 纸的页面，除核心图形外还有大量空白边距，直接插入论文效果很差。需要使用 TeX Live 自带的 `pdfcrop` 工具裁剪：
   - 以**管理员身份**打开 PowerShell（或任意命令行终端）
   - `cd` 进入 `.pdf` 文件所在文件夹
   - 执行命令：
     ```powershell
     pdfcrop 你的文件名.pdf
     ```
   - 命令会生成 `你的文件名-crop.pdf`，该文件已自动裁剪掉所有无用空白，仅保留核心图形区域。

4. **放入论文：** 将 `-crop.pdf` 文件复制到 `pic/` 目录，按正常方式插入即可：
   ```latex
   \includegraphics[scale=0.8]{你的文件名-crop.pdf}
   ```

> **说明：** 经过 `pdfcrop` 裁剪后的矢量 PDF 图像边缘紧凑、无冗余留白，插入论文后排版美观且专业，强烈推荐所有插图均采用此流程处理。

**`[htbp]` 浮动体位置参数：**

| 参数 | 含义 |
|---|---|
| `h` | here，优先放置在代码所在位置 |
| `t` | top，优先放置在页面顶部 |
| `b` | bottom，优先放置在页面底部 |
| `p` | page，优先放置在一个单独的浮动页上 |

LaTeX 按照 `[htbp]` 的顺序尝试放置图片，推荐使用 `[htbp]` 以获得较好的排版效果。如果希望强制放在当前位置，可使用 `[H]`（需 `\usepackage{float}`，模板已加载）。

**`\caption{}` 与 `\label{}` 的作用：**
- `\caption{图片标题}` — 生成图题，自动编号（如「图 1-1」），并录入图目录。
- `\label{fig:your-label}` — 为图片设置引用标签，用于正文中的交叉引用。

**完整的插图和引用示例：**

```latex
\begin{figure}[htbp]
    \centering
    \includegraphics[scale=0.8]{your-image.pdf}
    \caption{图片标题}
    \label{fig:your-label}
\end{figure}
```

正文中使用：

```latex
如图~\ref{fig:your-label}~所示，……
```

> **技巧：** 使用 `~` 作为不可断行空格（占位符），防止「如图 1-1」在换行时被拆开，排版更为美观。

#### 5.2 插入表格

使用者需要学会使用 LaTeX 绘制适合自己论文内容的表格。推荐使用 `tabular` 环境配合 `booktabs` 宏包（模板已加载）绘制三线表。

**为符合学位论文写作规范，表格内容建议使用 `\wuhao`（五号，10.5pt）字号，并适当调整列间距和行高以美化排版：**

```latex
\begin{table}[htbp]
    \centering
    \wuhao  % 表格内容为五号字
    {% 使用括号组将 tabcolsep 和 arraystretch 的修改限定在本表格内
    \setlength{\tabcolsep}{6mm}  % 调整列间距，美化排版
    \renewcommand{\arraystretch}{1.5}  % 调整行高，使表格更舒展
    \caption{表格标题}
    \label{tab:your-label}
    \begin{tabular}{lcc}
        \toprule
        \textbf{方法} & \textbf{准确率（\%）} & \textbf{F1 分数} \\
        \midrule
        方法一 & 85.3 & 0.82 \\
        方法二 & 91.7 & 0.89 \\
        \bottomrule
    \end{tabular}
    }
\end{table}
```

> **说明：**
> - `\setlength{\tabcolsep}{6mm}` 调整列与列之间的水平间距，使表格不显拥挤。
> - `\renewcommand{\arraystretch}{1.5}` 调整行间距（默认为 1.0），使表格在纵向上更舒展、可读性更强。
> - 表格标题使用 `\caption{}` 自动编号，引用方式同图片：`如表~\ref{tab:your-label}~所示`。

### 六、定理环境

模板提供了以下数学定理环境，使用时直接调用对应环境即可：

| 环境 | 中文名称 | 环境 | 中文名称 |
|---|---|---|---|
| `theorem` | 定理 | `axiom` | 公理 |
| `corollary` | 推论 | `lemma` | 引理 |
| `definition` | 定义 | `example` | 举例 |
| `proposition` | 命题 | `problem` | 问题 |
| `assumption` | 假设 | `remark` | 注 |

示例：

```latex
\begin{theorem}
这是一个定理。
\end{theorem}

\begin{definition}
这是一个定义。
\end{definition}
```

定理环境的编号格式为 `章节号.序号`（如「定理 2.1」），由模板自动管理。更多详细用法可参考原模板 [wennboo/HDU-latex-template-for-master](https://github.com/wennboo/HDU-latex-template-for-master) 中的示例。

### 七、参考文献

参考文献使用 BibTeX 管理，所有条目写入 `ref/reference.bib`。文献格式遵循 **GB/T 7714-2005** 标准，由 `hdu-thesis.bst` 自动控制输出格式。

#### 7.1 正文引用方式

中文学位论文中，引用参考文献推荐使用**上标引用** `\citep{}`：

```latex
\citep{zhou2014novel}                     % 引用单篇文献
\citep{zhou2014novel, al2018review}       % 引用多篇文献，在{}中用逗号隔开
```

具体引用方式以模板各章节中的实际引用为准，可参照 `chapter/introduction.tex` 等文件。

#### 7.2 获取 BibTeX 条目

正确的使用方法为：**前往各需要引用的期刊、会议论文的官方页面**（如 IEEE Xplore、Elsevier、Springer 等），也可以结合**谷歌学术（Google Scholar）**等各类学术资源库，下载或复制 BibTeX 格式的信息，粘贴到 `ref/reference.bib` 中。

> **重要提醒：** 从网上复制的 BibTeX 信息可能不全面，需要结合参考文献的实际信息**手动补全**关键字段。以下为各类文献的必要字段：

**期刊论文 `@article`** — 以下字段**必不可少**：

| 字段 | 说明 |
|---|---|
| `title` | 论文标题 |
| `author` | 作者列表 |
| `journal` | 期刊名称 |
| `volume` | 卷号 |
| `number` | 期号 |
| `pages` | 起止页码 |
| `year` | 出版年份 |

**会议论文 `@inproceedings`** — 以下字段**必不可少**：

| 字段 | 说明 |
|---|---|
| `title` | 论文标题 |
| `author` | 作者列表 |
| `booktitle` | 会议名称（全称） |
| `pages` | 起止页码 |
| `year` | 出版年份 |
| `address` | 会议地点（城市/国家） |
| `publisher` | 出版者 |

**专著 `@book`（[M]）** — 以下字段**必不可少**：

| 字段 | 说明 |
|---|---|
| `title` | 书名 |
| `author` | 作者 |
| `address` | 出版地 |
| `publisher` | 出版者 |
| `year` | 出版年份 |

> **学院特殊要求：** 专著除了年份，还需要给出起止页码（虽然不太理解，但需尊重学院规定）。

#### 7.3 标题大小写规则（可能需要手动调整）

BibTeX 条目中的标题大小写需要手动检查，规则如下：

- **论文 `title`：** 首字母大写，冒号「:」后的首字母大写，其他单词保持小写（专有名词除外）。
  ```
  正确：A double-square-based electrode sequence learning method for odor concentration identification
  错误：A Double-Square-Based Electrode Sequence Learning Method For Odor Concentration Identification
  ```
- **期刊 `journal` 和会议 `booktitle`：** 实词（名词、动词、形容词、副词）首字母均需大写，虚词（a, an, the, of, for, and 等）保持小写。
  ```
  正确：IEEE Transactions on Pattern Analysis and Machine Intelligence
  错误：Ieee Transactions On Pattern Analysis And Machine Intelligence
  ```

### 八、致谢与个人成果

**非盲审时**，致谢写入 `contents/acknowledgement.tex`，攻读学位期间取得的成果写入 `contents/personalresult.tex`。

**盲审时**，攻读学位期间取得的成果不能单独成节出现，需要放入附录中（参见上文「盲审注意事项」部分），并隐去所有个人信息（作者姓名、导师姓名、论文标题中可能暴露身份的关键词等），以 "XXX" 或 "本人" 替代。盲审后的最终版本可以继续使用附录展示成果，并可以正常展示个人信息。

### 九、附录

- 只有一章附录：使用 `\singleappendix` 命令。
- 有多章附录：使用 `\thesisappendix` 命令（在 `main-thesis.tex` 中替换 `\singleappendix`）。

附录内容写入 `contents/appendix.tex`。

---

## 补充说明

### 缩略词表

本模板**不包含缩略词表功能**（原模板使用了 `glossaries` 宏包支持缩略词列表，本版已精简）。如有缩略词表需求，可自行引入 `glossaries` 宏包并参照其官方文档配置。

### 编译产物

编译过程中会生成 `.aux`、`.log`、`.toc`、`.out`、`.synctex.gz` 等辅助文件。建议将以下条目加入 `.gitignore`：

```gitignore
*.aux
*.log
*.toc
*.out
*.synctex.gz
*.bbl
*.blg
*.fdb_latexmk
*.fls
*.xdv
```

---

## 致谢与参考

- 原模板作者：[wennboo](https://github.com/wennboo) — [HDU-latex-template-for-master](https://github.com/wennboo/HDU-latex-template-for-master)
- 原模板部分建立在东南大学（SEU）与电子科技大学（UESTC）的学位论文模板基础之上。
- 本版本在原模板基础上精简和修改，仅供课题组内部学术使用。
