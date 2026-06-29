# 增强高考填报志愿助手 AI Agent Skill 规范

## Why
已有项目结构不完整（仅含 LICENSE），SKILL.md 工作流缺乏数据检索分支、新高考填报单位适配、专科批/强基计划等扩展场景、输出前自检清单；工程文档缺失 CHANGELOG.md、CONTRIBUTING.md、examples/ 目录；参考资料不完整。需一次性补全所有缺失模块，形成可交付的完整技能包。

## What Changes
- 创建完整目录结构：SKILL.md、README.md、CHANGELOG.md、CONTRIBUTING.md、LICENSE（保留MIT）
- 在 SKILL.md 中增强工作流：数据获取分支、新高考双模式、扩展场景、输出自检清单
- 新增 references/高考志愿填报通用知识.md（补充院校专业组、强基/综评、艺术体育类内容）
- 新增 examples/ 目录（至少 2 个端到端案例）
- git add / commit / push 到 GitHub remote main 分支

## Impact
- Affected specs: 无已有 specs，此为初始创建
- Affected code: 所有新增文件

## ADDED Requirements

### Requirement: SKILL.md 增强工作流
系统 SHALL 提供一份增强版 SKILL.md，包含以下改进：

#### Scenario: 数据获取分支
- **WHEN** AI 运行环境支持联网检索
- **THEN** 指引 AI 优先调用内置检索能力，从省教育考试院官网、阳光高考平台（gaokao.chsi.com.cn）等官方渠道核对往年位次/投档线
- **AND WHEN** 运行环境不支持联网检索
- **THEN** AI SHALL 如实声明数据为估算，并标注"需查阅最新招生计划"

#### Scenario: 新高考填报单位适配
- **WHEN** 信息采集阶段识别用户省份为广东/湖北等
- **THEN** 自动适配"院校专业组"模式输出结构
- **AND WHEN** 用户省份为浙江/山东等
- **THEN** 自动适配"专业+院校"模式输出结构

#### Scenario: 覆盖扩展场景
- **WHEN** 用户属于专科/强基计划/综合评价/艺术体育/中外合作办学/提前批（军警/公费师范/免费医学生）
- **THEN** AI SHALL 提供差异化填报指引作为可选分支

#### Scenario: 输出前自检清单
- **WHEN** AI 生成最终建议前
- **THEN** SHALL 校验梯度比例与用户偏好匹配、含免责声明、提醒服从调剂与选科要求、表格未编造数据

### Requirement: 工程结构完善
系统 SHALL 包含以下新增文件：

- SKILL.md frontmatter 含 version 字段（1.1.0）
- CHANGELOG.md 记录本次更新
- CONTRIBUTING.md 说明贡献方式与提交规范
- examples/ 目录含 2 个端到端案例（院校专业组 + 专业+院校），使用占位数据并标注非真实分数线
- README.md 聚焦"是什么/如何安装/如何使用"，补充功能特色清单和简短使用演示片段

### Requirement: 参考资料扩充
系统 SHALL 在 references/高考志愿填报通用知识.md 中补充：
- 院校专业组填报详解
- 强基计划与综合评价简介
- 艺术体育类志愿规则要点
- 保持"仅通用知识、不含实时数据"风格与免责声明

### Requirement: 合规与免责
系统 SHALL：
- 保持 MIT LICENSE 不变
- 不编造具体录取分数线数据
- 所有输出表格含"非真实数据"标注或免责声明