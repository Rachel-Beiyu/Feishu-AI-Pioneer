# Feishu-AI-Pioneer
效傲 X 分钟 - 飞书 AI 效率先锋演讲教练 SKILL
一个专为飞书 AI 效率先锋大赛参赛者设计的 Agent SKILL，帮你从「有想法」到「拿高分」

**这个 SKILL 能干什么**
**📝 场景一：基于你的业务文档，生成完整演讲稿**
提供企业名称、分享时长、业务文档，agent 会：
1. 对齐四大评分维度（AI技术创新30% / 业务提效30% / 可推广性20% / 展示专业度20%）
2. 生成完整逐字稿，每段标注建议时长和「评委视角」
3. 提供 3-5 个标题方案 + 5 个高频答辩问题应对框架
4. 一键创建飞书文档，直接拿去练习


**🎬 场景二：分析试讲妙记，给你直接能用的反馈**
把试讲录制成飞书妙记，丢给 agent 一个链接，它会：
1. 自动调用飞书 CLI 读取完整逐字稿（不依赖导出，不需要你是妙记所有者）
2. 从六个维度精准诊断：开场钩子、故事线节奏、数字与证据、技术可懂度、表达状态、答辩预判
3. 输出「改了能直接提分」的优先改进清单


**文件结构**
efficiency-pioneer-coach/
├── SKILL.md                     # 主文件：妙记读取方式 + 演讲教练指令
└── references/
    ├── scoring-criteria.md      # 四大维度评分标准详解（30/30/20/20）
    ├── speech-structures.md     # 三种演讲结构模板（故事型/逻辑型/影响型）
    ├── title-examples.md        # 演讲标题参考库 + 5种创作公式
    └── qna-prep.md              # 评委高频问题 × 10 + 应对框架

**安装方式**
前置要求：
1. 已安装 lark-cli：npm install -g @larksuite/cli
2. 已完成飞书 App 配置：lark-cli config init


**授权妙记读取权限（首次使用）：**
lark-cli auth login --scope "minutes:minutes:readonly minutes:minutes.transcript:export"

**使用示例**
1. 分析试讲:基于这个试讲妙记，给我一些分享建议，8分钟的分享：https://xxx.feishu.cn/minutes/obcnxxxx
2. 生成演讲稿:帮我基于这份飞书文档，生成一个8分钟的效率先锋演讲稿
3. 优化故事线:帮我优化一下这个效率先锋大赛的故事线，要有记忆点

**核心设计原则**
评分标准优先：所有建议必须对齐四大维度，不做无效优化
大白话原则：把技术黑话翻译成评委能听懂的业务语言
数据驱动：不接受"效率提升了"，只接受"从3天缩短到2小时"
故事优先：问题→行动→结果→意义，多讲人的故事

**关于飞书妙记读取的技术说明**
本 SKILL 使用 lark-cli api GET 直接调用 Feishu Transcript API，无需是妙记所有者，无需导出文件：

lark-cli api GET "/open-apis/minutes/v1/minutes/{token}/transcript" \
  --params '{"need_speaker":"true","need_timestamp":"true"}' \
  --as user

这是在实践中踩坑后验证的可靠方案——lark-cli vc +notes 对非所有者会返回 HTTP 403，本 SKILL 已绕开这个限制。

**适用人群**
参加飞书 AI 效率先锋大赛的参赛团队
需要准备 AI 提效类演讲/汇报的职场人
希望把 Claude 用于比赛辅助的效率工具探索者

Built with lark-cli + Claude Agent SKILL 框架
