# GitHub Push & Project Optimization Spec

## Why
将项目推送到 GitHub 远程仓库，并在推送前完成版本号统一、CI 工作流、流程图可视化、ISSUE 模板等优化。

## What Changes
1. **统一版本号**：README.md 和 SKILL.md 中的版本号从 v1.5.0 改为 v1.4.0
2. **新增 GitHub Actions 工作流**：创建 `.github/workflows/validate.yml`，包含 markdownlint 格式检查 + 链接有效性检查
3. **SKILL.md 顶部添加 Mermaid 流程图**：可视化展示六步工作流（采集→数据获取→匹配策略→场景分支→志愿表生成→自检清单）
4. **README.md 新增"工作流概览"章节**：在"文件结构"部分之后，引用 Mermaid 流程图
5. **创建 ISSUE 模板**：`ISSUE_TEMPLATE/bug_report.md` 和 `ISSUE_TEMPLATE/feature_request.md`
6. **Git 推送**：执行 git add → commit → push origin main

## Impact
- Affected specs: README.md, SKILL.md
- Affected code: `.github/workflows/validate.yml` (new), `.github/ISSUE_TEMPLATE/bug_report.md` (new), `.github/ISSUE_TEMPLATE/feature_request.md` (new)
- Breaking changes: 版本号从 v1.5.0 降为 v1.4.0

## ADDED Requirements

### Requirement: Version Unification
The system SHALL update version references to v1.4.0 in README.md and SKILL.md.

### Requirement: CI Workflow
The system SHALL create a validate.yml workflow with:
- markdownlint checks on all .md files
- Link validation for README.md and SKILL.md

### Requirement: Mermaid Flowchart
The system SHALL add a Mermaid flowchart at the top of SKILL.md (after frontmatter) showing the 6-step workflow.

### Requirement: Workflow Overview in README
The system SHALL add a "工作流概览" section after the "文件结构" section in README.md, referencing the Mermaid flowchart.

### Requirement: Issue Templates
The system SHALL create bug_report.md and feature_request.md in .github/ISSUE_TEMPLATE/.

### Requirement: Git Push
The system SHALL execute git add, commit with message "chore: 统一版本号、添加CI工作流、增加流程图、完善ISSUE模板", and push to origin main.

## MODIFIED Requirements
N/A - all new additions

## REMOVED Requirements
N/A