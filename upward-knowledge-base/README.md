# Upward Knowledge Base

> 从 原型（Figma/墨刀）到高质量测试用例的工程化知识库系统。
> 
> **当前项目**：圈子 App 端（墨刀原型）
> 
> **核心理念**：原型解析 → 自动推断 → 确认清单 → 结构化知识 → 生成用例

---

## 目录结构

```
upward-knowledge-base/
├── README.md                    ← 使用指南（本文件）
├── app-overview.md              ← 一级：应用总览（模块地图、43个页面、全局规范）
│
├── 圈子/                        ← 二级功能：圈子模块（页面+业务规则+参考）
│   ├── pages/                   ← 圈子页面知识
│   │   ├── modao-annotations.md ← 墨刀原型标注识别与确认
│   │   ├── group-chat.md        ← 群聊模块（12个页面）
│   │   ├── group-management.md  ← 群管理模块（5个页面）
│   │   ├── member-management.md ← 成员管理模块（4个页面）
│   │   ├── announcements.md     ← 群公告模块（4个页面）
│   │   ├── my-circle.md         ← 我的圈子模块（7个页面）
│   │   ├── create-circle.md     ← 创建圈子模块（3个页面）
│   │   ├── dynamic-post.md      ← 动态发布模块（3个页面）
│   │   └── event-race-list.md   ← 赛事/活动/榜单/用户主页模块（6个页面）
│   │
│   ├── business-rules/          ← 圈子业务规则
│   │   ├── circle-types.md      ← 圈子类型与自动创建
│   │   ├── group-lifecycle.md   ← 群生命周期
│   │   ├── permissions.md       ← 权限体系
│   │   ├── messages.md          ← 消息与群聊规则
│   │   ├── announcements.md     ← 群公告规则
│   │   ├── member-management.md ← 成员管理规则
│   │   └── notifications.md     ← 系统消息与通知
│   │
│   └── references/              ← 圈子参考文档
│       └── modao-full-parse.md  ← 墨刀原型全量解析
│
├── api-contracts/               ← 接口契约（请求、响应、错误码）
│   └── (按模块创建 .md)
│
├── checklist-archive/           ← 历史确认清单（归档追踪）
│
├── test-output/                 ← 生成的测试用例（Excel/Markdown）
│
└── _templates/                  ← 模板文件（新建条目时复制使用）
    ├── page-entry-template.md
    ├── business-rule-template.md
    ├── api-contract-template.md
    └── confirmation-checklist-template.md
```

> **目录设计原则**：一级放应用总览，二级按功能模块命名（如 `圈子/`），每个模块内部再分 `pages/`、`business-rules/`、`references/`。新增功能模块时只需新增一个二级目录即可。

---

## 快速开始

### 第一步：初始化应用总览

1. 打开 `app-overview.md`
2. 填写应用基本信息、模块地图、全局设计规范
3. 对着原型目录（墨刀/Figma），把能看到的所有页面列在"知识库索引"表格中

### 第二步：按功能模块录入（与 AI 配合）

**每个模块的标准流程（耗时约 15-30 分钟/模块）：**

```
① 提供原型页面 → 截图 或 分享链接
② AI 自动解析，生成页面知识条目草稿
③ AI 生成"待确认清单"
④ 你花 5-10 分钟浏览确认清单，勾选/填空
⑤ AI 将确认结果整合进页面条目，标记为"已确认"
⑥ 存入对应功能模块的 pages/ 目录（如 圈子/pages/）
```

> **目录组织规则**：一级为应用总览，二级按功能模块命名。每个模块目录内部包含 `pages/`、`business-rules/`、`references/` 子目录。新增模块时只需新增一个二级目录。

### 第三步：补充业务规则

1. 随着页面信息的积累，跨页面的业务规则会自然浮现
2. 在对应功能模块的 `business-rules/` 下为每个关键规则创建条目（如 `圈子/business-rules/`）
3. 标注"涉及页面"，建立页面与规则的关联

### 第四步：补充接口契约

1. 从接口文档平台（Swagger/Apifox/YApi 等）获取接口定义
2. 在 `api-contracts/` 下按模块创建接口条目
3. 填写"关联页面"字段，建立接口与页面的关联

### 第五步：生成测试用例

知识库具备一定规模后，使用 `figma-test-knowledge` 技能：
- AI 读取相关页面的知识条目 + 业务规则 + 接口契约
- 自动生成测试用例
- 输出到 `test-output/` 目录

---

## 团队共享方式

### 方式一：Git 仓库（推荐）

```bash
# 将 upward-knowledge-base/ 放入你们的项目仓库
git add upward-knowledge-base/
git commit -m "docs: 初始化测试知识库"

# 团队成员 clone 后即可使用
# 每个人更新知识条目后提交，其他人 pull 获取最新
```

### 方式二：共享文件夹

将 `upward-knowledge-base/` 放入团队的共享网盘/文档平台，团队成员共同编辑。

### 方式三：直接分享

将整个 `upward-knowledge-base/` 目录打包发送给团队成员，解压到各自的 WorkBuddy workspace 中即可使用。

---

## 维护原则

1. **渐进式录入**：不要试图一次性录入所有页面，每个需求迭代录入本次涉及的页面即可。3-4 个迭代后知识库自然成型。
2. **谁用谁更新**：生成测试用例时发现知识库过时，顺手更新对应条目。
3. **确认清单归档**：每次填完的确认清单保存到 `checklist-archive/`，方便后续溯源。
4. **定期回顾**：每月检查一次知识库覆盖率，补充遗漏的页面和规则。

---

## 文件格式说明

所有知识条目使用 Markdown 格式，原因：
- 纯文本，Git 友好，diff 可读
- 任何编辑器都能打开
- AI 可以直接读取和理解
- 可以在 Markdown 中嵌入截图（Base64 或相对路径引用）
