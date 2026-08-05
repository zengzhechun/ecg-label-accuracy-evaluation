# ECG Label Accuracy Evaluation · 心电图大模型训练数据准确性评价

> **English (repo description):** Accuracy evaluation of training labels for ECG foundation models — expert review of label noise across PTB-XL, MIMIC-IV-ECG, and a Ningbo ECG database, with interactive HTML reports and simulators.
>
> **中文说明：** 本项目评估心电图（ECG）大模型训练数据的标签准确性。基于三个数据库（PTB-XL、MIMIC-IV-ECG、宁波心电图数据库）的专家复阅，量化标签噪声并给出错误分类学、噪声容忍度与标签清洗方法建议；全部交付物为自包含 HTML 报告与交互式模拟器。

---

## 一、项目背景（Background）

心电图（ECG）大模型（如 ECG-Founder、DeepECG）普遍以 PTB-XL、MIMIC-IV-ECG 等公开数据集为训练源。但这些数据集的**标签并非金标准**：存在遗漏型错误（自由文本命名空间复杂）、类别不平衡、标注者分歧等问题。本项目通过对三库抽样数据进行**专家独立复阅**，用统一受控词表将原始标签映射为诊断节点，量化标签准确性、构建错误分类学，并探讨噪声对下游模型性能的传递规律。

本仓库收录已定稿的分析报告、交互式模拟器与一篇方法论综述，面向**团队内部协作与学术共享**。

---

## 二、仓库结构（Repository Structure）

```
ECG-Label-Accuracy-Evaluation/
├── index.html              # 报告门户（导航入口，GitHub Pages 首页）
├── README.md               # 本文件
├── .gitignore              # 忽略本地数据，仅保留 data/ 空目录占位
├── reports/                # 全部已定稿 HTML 报告
│   ├── KimiWork_宁波标签质量综合分析_v8.0.html
│   ├── KimiWork_v15.0_标签噪声容忍度分析.html
│   ├── MIMIC标签噪声分析.html
│   ├── PTB-XL标签质量分析.html        (+ PTB-XL标签质量分析_files/ 资源)
│   ├── PTB-XL双阅一致性分析.html      (+ PTB-XL双阅一致性分析_files/ 资源)
│   ├── 核心心律失常错误子集分析.html
│   └── 脏标签处理与对抗方法_综合研究报告.html
├── simulators/             # 交互式标签噪声模拟器（单文件，纯前端）
│   ├── KimiWork_v15_标签噪声模拟器.html
│   ├── KimiWork_MIMIC_标签噪声模拟器.html
│   └── KimiWork_PTBXL标签噪声模拟器_v2.html
└── data/                   # 本地原始数据【不入库】，仅占位
    ├── raw/.gitkeep        #   未来同步：专家审阅原始 Excel
    └── processed/.gitkeep  #   未来同步：去重/映射后数据
```

> **说明：** 报告以中文命名以保证与内部资料一致；文件夹使用英文（`reports/`、`simulators/`、`data/`）以保持结构清晰。带 `_files` 的文件夹是 Quarto 报告的图表与样式依赖，**必须随 HTML 一同存在**，否则图表/样式无法正常显示。

---

## 三、各报告与模拟器用途（Contents）

### 报告（reports/）
| 文件 | 数据库 | 用途 |
|---|---|---|
| `KimiWork_宁波标签质量综合分析_v8.0.html` | 宁波 | 宁波 ECG 标签质量综合分析主报告（去重 623 例 / 主分析集 613 例） |
| `KimiWork_v15.0_标签噪声容忍度分析.html` | 三库综合 | ⭐ 主报告：标签噪声容忍度 + 错误分类学 + 三库对照 |
| `MIMIC标签噪声分析.html` | MIMIC-IV-ECG | MIMIC 1000 例随机抽样标签噪声分析，含三库对照组件 |
| `PTB-XL标签质量分析.html` | PTB-XL | PTB-XL 674 例标签质量分析（含图表） |
| `PTB-XL双阅一致性分析.html` | PTB-XL | 双标注者一致性（Dawid–Skene / 贝叶斯），量化标注者分歧 |
| `核心心律失常错误子集分析.html` | 三库综合 | 核心心律失常诊断错误/缺失子集分析 |
| `脏标签处理与对抗方法_综合研究报告.html` | 方法学 | ⭐ 脏标签（Noisy Labels）处理与对抗方法综述 + 市场调研 + 交互模拟器（53 篇文献） |

### 模拟器（simulators/）
| 文件 | 用途 |
|---|---|
| `KimiWork_v15_标签噪声模拟器.html` | 标签噪声衰减沙盘 / 错误率阈值推演 / 核心心律失常子集（含宁波+PTB-XL） |
| `KimiWork_MIMIC_标签噪声模拟器.html` | MIMIC 专用：重复/准确性/分布/三库对照/补充词汇 6 模块 |
| `KimiWork_PTBXL标签噪声模拟器_v2.html` | PTB-XL 专用：标签分布 / 噪声注入 / 双阅冲突 |

---

## 四、本地打开与在线访问（How to Open）

### 本地打开（Local）
1. 克隆或下载本仓库；
2. 双击 `index.html` 即可打开**报告门户**（导航首页）；
3. 点击门户中的卡片，在新标签页打开对应报告/模拟器；
4. 报告与模拟器均为**自包含单文件**（或带同目录 `_files`），无需联网、无需服务器。

```bash
git clone https://github.com/zengzhechun/ecg-label-accuracy-evaluation.git
cd ecg-label-accuracy-evaluation
open index.html        # macOS
```

### 在线访问（GitHub Pages）
本仓库已启用 GitHub Pages（发布自 `main` 分支根目录）：

- **门户首页：** https://zengzhechun.github.io/ecg-label-accuracy-evaluation/
- **各报告/模拟器：** 在上述首页点击卡片即可，或直接使用以下链接：
  - 报告： `https://zengzhechun.github.io/ecg-label-accuracy-evaluation/reports/<文件名>`
  - 模拟器： `https://zengzhechun.github.io/ecg-label-accuracy-evaluation/simulators/<文件名>`

> 注意：部分报告内部会链接到对应的 `.docx` Word 版（未上传，避免体积过大），在线打开这些链接会 404；本地仓库若放有对应 docx 则可正常打开。

---

## 五、如何共享给团队（Sharing）

本仓库为 **Public（公开）**，任何人都可通过上述 GitHub Pages 链接访问，无需登录。如需团队协作（共同编辑/提交），有两种方式：

1. **协作者邀请（Collaborator）：** 仓库 `Settings → Collaborators → Add people`，输入同事 GitHub 用户名/邮箱，对方接受后即可 `git push`。
2. **Fork + Pull Request：** 适合外部贡献者；同事 Fork 后改完提 PR，由你审核合并。
3. **团队/组织（可选）：** 若团队有 GitHub Organization，可将仓库 Transfer 至组织下，便于统一权限管理。

> 当前仅发布**已定稿**报告（约 53 MB）。早期草稿版本（v1–v14，约 186 MB）保留在本地，未上传以保持仓库轻量；如需纳入，可在 `reports/archive/` 下补充并重新推送。

---

## 六、后续维护建议（Maintenance）

1. **数据同步：** 原始 Excel 不入库。待数据可公开时，放入 `data/raw/` 并调整 `.gitignore`（取消对应忽略规则）后提交；处理后数据放 `data/processed/`。
2. **报告更新：** 重新生成报告后，覆盖 `reports/` 下对应文件并 `git add && git commit && git push`；若文件名变化，请同步更新 `index.html` 中 `const DATA` 的 `href` 与 `path`。
3. **门户再生：** `index.html` 由本地脚本（`/tmp/gen_portal.py` 思路）生成；新增/移除文件后重新生成门户，保持链接一致。
4. **大文件：** 单个 HTML 已含内嵌资源，请勿再引入 >50 MB 的二进制；如需更大资源，建议放释放版（Release）而非仓库。
5. **版本一致：** 分析结论以"主报告 v15.0（三库综合）"为准；宁波数据主分析集为 **613 例**（研究团队补充数据后的最终版本）。
6. **学术规范：** 引用文献以 `脏标签处理与对抗方法_综合研究报告.html` 文末参考文献为准；发表前请人工复核 DISC、ECG-ITR 等条目的原始出处。

---

© 2026 心电图标签准确性验证课题组 · 本仓库用于学术共享与团队协作。
