# Paper-Learning

一个用于分享、学习、整理和收藏论文撰写经验的项目，记录科研过程中可复用的规范、模板、方法与推导，便于日后查阅和交流。

目前包含三组资料：

- [实验数据分析与绘图 Agent](PLOTTING_AGENT.md)：Python / Matplotlib 绘图规范，涵盖脚本结构、数据表达、图表尺寸、布局、字体和结果检查。
- [TACO 审稿回复模板](HA-TACO-response/)：以实际 response 为例，整理 LaTeX 回复结构、逐位审稿人的回复、配套图表与参考资料。
- [并行排序平方加速比推导](Sorting_square_speedup.md)：分析选择排序分组并行、随后归并的复杂度，以及固定并行度下加速比趋近并行度平方的条件。

## 目录树

以下展示主要资料；重复图表和 LaTeX 编译辅助文件合并列示，省略 `.git/`。

```text
Paper-Learning/
├── README.md                         # 项目介绍与资料索引
├── PLOTTING_AGENT.md                  # 实验数据分析与绘图规范
├── Sorting_square_speedup.md          # 并行排序平方加速比推导
├── HA-TACO-response/                  # TACO 审稿回复模板及实例
│   ├── AGENTS.md                      # 回复文档的编辑与排版约定
│   ├── response.tex                   # LaTeX 主文件
│   ├── reviewer1.tex                  # Reviewer 1 的逐条回复
│   ├── reviewer2.tex                  # Reviewer 2 的逐条回复
│   ├── reviewer3.tex                  # Reviewer 3 的逐条回复
│   ├── response.pdf                   # 回复文档 PDF
│   ├── TACO-2026-55_Response_to_Reviewers.pdf
│   ├── TACO-2026-55_Response_Summary.txt
│   ├── [SPAM] TACO-2026-55_ Decision.eml
│   ├── response-audit.txt             # 回复检查记录
│   ├── response-audit-visual.txt       # 视觉检查记录
│   ├── figures/                       # 图表图片及 PSD 源文件
│   ├── news/                          # 按审稿问题命名的图表素材
│   ├── literature/
│   │   └── R1-Q11/                    # 相关文献、元数据与比较笔记
│   └── response.*                     # 其他 LaTeX 编译辅助文件
└── test
```

## 使用说明

- 绘图前参考 `PLOTTING_AGENT.md`，按目标论文格式和实验内容落实规范。
- 撰写审稿回复时，从 `HA-TACO-response/response.tex` 查看整体结构，结合 `reviewer1.tex`–`reviewer3.tex` 学习逐条回复的组织方式；复用时替换论文信息、审稿意见和回复内容。
- 阅读排序推导时注意其算法与极限条件：平方加速比对应文中模型在固定并行度、数据规模趋于无穷时的结果。

后续可继续收录论文写作、实验设计、数据分析、投稿和审稿回复中的经验，并在本文件中更新索引与目录树。
