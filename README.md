# 高考志愿填报助手 (Gaokao Volunteer Assistant)

一个面向 Trae IDE 的 AI Agent Skill，辅助考生进行高考志愿填报策略分析，提供院校推荐、梯度设计、多场景填报指引。

> ⚠️ **定位**：本项目是 AI Agent Skill 定义项目，核心交付物是 `.trae/skills/SKILL.md`（工作流定义）和 `references/`（知识参考资料），**不是可运行的 Web 应用**，不包含任何具体的录取分数数据库。

---

## 功能特色

- **智能采集考生信息**：自动收集省份、科类、成绩、位次、选科等关键字段
- **自动适配新高考填报模式**：识别省份后切换"院校专业组"（粤/鄂等）或"专业+院校"（浙/鲁等）模式
- **双数据获取路径**：联网时优先检索省教育考试院、阳光高考平台等官方渠道；离线时如实声明数据为估算
- **扩展场景覆盖**：专科批、强基计划、综合评价、艺术体育类、中外合作办学、提前批（军警/公费师范/免费医学生）
- **"冲-稳-保"梯度设计**：根据风险偏好自动调整比例，输出结构化的志愿表
- **输出前自检清单**：梯度比例、免责声明、服从调剂、选科要求、数据真实性逐一校验

---

## 文件结构

```
gaokao-volunteer-assistant/
├── .trae/
│   └── skills/
│       └── SKILL.md                  # Skill 主定义文件（YAML frontmatter + 六步工作流）
├── README.md                         # 本文件
├── LICENSE                           # MIT 协议
├── CHANGELOG.md                      # 更新日志
├── CONTRIBUTING.md                   # 贡献指南
├── references/                       # 知识参考资料目录
│   ├── data/                         # （可选）录取数据存放目录
│   ├── 高考志愿填报通用知识.md        # 通用知识文档（含院校专业组/强基综评/艺体类详解）
│   ├── 平行志愿规则.md                # 平行志愿规则与核心原则
│   ├── 冲稳保策略.md                  # 冲稳保梯度策略详解
│   ├── 专业级差与调剂.md              # 专业级差说明与服从调剂分析
│   ├── 提前批与特殊类型.md            # 提前批、强基计划、综合评价、定向招生
│   ├── 新高考选科与填报模式.md        # 新高考选科要求与两种填报模式对比
│   ├── 常见误区.md                    # 十大常见误区提醒
│   └── index.md                      # 知识库索引
└── examples/                         # 端到端示例目录
    ├── 院校专业组模式-广东省示例.md    # 院校专业组模式案例（占位数据）
    ├── 专业+院校模式-浙江省示例.md     # 专业+院校模式案例（占位数据）
    ├── 场景1-缺少位次.md              # 缺失关键信息处理示例
    ├── 场景2-不服从调剂.md            # 不服从调剂风险提示
    ├── 场景3-提前批师范咨询.md        # 提前批公费师范生政策解读
    └── 场景4-选科与专业冲突.md        # 选科冲突检测与调整建议
```

---

## 安装方法

### 方式一：复制到 Trae IDE 的 skills 目录

```bash
git clone https://github.com/GZgreywolfy/gaokao-volunteer-assistant.git
# 将 SKILL.md 所在目录复制到 Trae IDE 对应的 skills 配置路径
```

**Trae IDE 操作步骤**：

1. 打开 Trae IDE，进入项目设置
2. 找到 AI Agent / Skills 配置区域
3. 将本项目 `.trae/skills/SKILL.md` 加载为 AI Skill
4. 将 `references/` 目录下的知识文档导入知识库
5. 当用户输入高考志愿相关问题（如"志愿填报""选大学""冲稳保"等）时，Skill 将自动触发

### 方式二：Git 子模块（推荐团队协作）

```bash
cd /path/to/你的项目/.trae/skills/
git submodule add https://github.com/GZgreywolfy/gaokao-volunteer-assistant.git
```

---

## 使用演示

**用户输入**：

> 我是广东物理类考生，580 分，位次 35000，选科物化生，想去珠三角，学计算机或电子信息。

**AI 响应流程**：

1. **信息采集** → 识别广东为"院校专业组"模式
2. **数据获取** → 联网检索广东省教育考试院往年投档数据（或离线估算策略）
3. **匹配策略** → 按院校专业组模式输出"冲-稳-保"志愿表
4. **可选分支** → 如果涉及强基/综评/艺体等，切换对应指引
5. **志愿表生成** → 输出带梯度的推荐表格
6. **自检清单** → 逐一校验梯度比例、免责声明、选科要求、数据真实性

详细示例见 [examples/](examples/) 目录。

---

## 能做什么 / 不能做什么

### 能做的
- 根据用户分数、位次等信息，按"冲稳保"梯度推荐院校和专业方向
- 解释平行志愿规则、专业级差、服从调剂等填报概念
- 识别新高考不同填报模式（院校专业组 vs 专业+院校）并差异化处理
- 提示专业级差、体检限制、单科要求等风险
- 覆盖专科批、强基计划、综合评价等特殊类型场景

### 不能做的
- **不提供具体院校的实时录取分数线** — 不编造未经核实的数据
- **不做录取概率的精确计算** — 录取概率只能做大致估算
- **不替代官方数据和招生章程** — 所有推荐以官方信息为准
- **不替代最终决策** — 填报是重大决策，需考生与家长共同商议

---

## 数据源接入指南

本 Skill 支持接入第三方录取数据，以便 AI Agent 在联网检索时引用更准确的往年录取数据。

### 数据格式规范

推荐使用 CSV 或 JSON 格式存储录取数据，包含以下字段：

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `province` | string | 是 | 省份名称（如"广东省"） |
| `year` | integer | 是 | 数据对应年份（如 2024） |
| `batch` | string | 是 | 录取批次（如"本科批""专科批"） |
| `category` | string | 是 | 科类（如"物理""历史""综合"） |
| `college_code` | string | 否 | 院校代码 |
| `college_name` | string | 是 | 院校名称 |
| `major_group` | string | 否 | 专业组代码/名称（院校专业组模式） |
| `major_name` | string | 否 | 专业名称（专业+院校模式） |
| `subject_requirement` | string | 否 | 选科要求 |
| `min_score` | integer | 否 | 最低录取分数 |
| `min_rank` | integer | 是 | 最低录取位次（推荐作为主要参考） |

### CSV 格式示例

```csv
province,year,batch,category,college_code,college_name,major_group,subject_requirement,min_score,min_rank
广东省,2024,本科批,物理,10560,深圳大学,201专业组,物理+化学,592,28000
广东省,2024,本科批,物理,10560,深圳大学,202专业组,物理,588,30500
浙江省,2024,普通批,综合,11646,杭州电子科技大学,计算机科学与技术,物理,615,29000
浙江省,2024,普通批,综合,11646,杭州电子科技大学,软件工程,物理,612,30500
```

### JSON 格式示例

```json
[
  {
    "province": "广东省",
    "year": 2024,
    "batch": "本科批",
    "category": "物理",
    "college_code": "10560",
    "college_name": "深圳大学",
    "major_group": "201专业组",
    "subject_requirement": "物理+化学",
    "min_score": 592,
    "min_rank": 28000
  },
  {
    "province": "浙江省",
    "year": 2024,
    "batch": "普通批",
    "category": "综合",
    "college_code": "11646",
    "college_name": "杭州电子科技大学",
    "major_name": "计算机科学与技术",
    "subject_requirement": "物理",
    "min_score": 615,
    "min_rank": 29000
  }
]
```

### 数据目录约定

建议将录取数据文件存放在 `references/data/` 目录下，按省份和年份组织：

```
references/
├── data/
│   ├── guangdong/
│   │   ├── 2024_physical.csv    # 广东省2024物理类
│   │   └── 2024_history.csv     # 广东省2024历史类
│   ├── zhejiang/
│   │   └── 2024_comprehensive.csv # 浙江省2024综合
│   └── ……
├── index.md
└── …
```

### 引用要求

在 SKILL.md 工作流中引用数据时的规范：

1. 在第二步"数据获取分支"中，如果在联网检索时使用了导入的录取数据，须注明：
   - 数据来源文件名
   - 数据年份
   - 数据覆盖范围（省份、科类）
2. 在输出志愿表时，须在表头或表尾标注数据来源：
   > *位次数据来源：references/data/guangdong/2024_physical.csv（广东省教育考试院2024年公开数据）*
3. 所有引用的数据须附带免责声明：
   > ⚠️ 引用数据为历史公开数据，仅供参考。实际录取位次可能因招生计划、考生人数等因素发生变化，请以当年官方数据为准。

### 接入示例（Python）

```python
import csv

def load_admission_data(filepath):
    """加载录取数据文件"""
    data = []
    with open(filepath, 'r', encoding='utf-8') as f:
        reader = csv.DictReader(f)
        for row in reader:
            data.append(row)
    return data

def query_by_rank_range(data, target_rank, range_percent=0.1):
    """按位次范围查询院校"""
    lower = int(target_rank * (1 - range_percent))
    upper = int(target_rank * (1 + range_percent))
    results = [row for row in data if lower <= int(row['min_rank']) <= upper]
    return sorted(results, key=lambda x: int(x['min_rank']))

# 使用示例
# data = load_admission_data('references/data/guangdong/2024_physical.csv')
# matches = query_by_rank_range(data, target_rank=35000, range_percent=0.1)
```

---

## 注意事项

- 本 Skill 提供的建议仅供参考，不构成填报决策的唯一依据
- 高考政策每年可能调整，请以当年官方文件为准
- 建议结合《志愿填报指南》、高校招生章程等多方信息综合决策
- 推荐结果受限于 AI 的知识边界，可能不包含最新招生变动

---

## 版本与更新

当前最新版本：**v1.4.0**

完整的版本历史和详细变更内容请参阅 [CHANGELOG.md](CHANGELOG.md)。

## 贡献

欢迎提交 Issue 或 Pull Request 来完善参考资料和策略逻辑。详情请参阅 [CONTRIBUTING.md](CONTRIBUTING.md)。

## 许可

MIT

## 免责声明

本项目和其贡献者不对因使用本 Skill 而产生的任何录取结果或决策失误承担责任。高考志愿填报是重大人生决策，请务必结合官方数据和多方意见审慎决定。