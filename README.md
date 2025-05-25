# AI如何塑造新的学习范式：STEAIM

### 团队：Agent4Edu 

几乎所有人都相信AI能够改变教育，我们也不例外。因此我们制作了 **STEAIM** ，它是一个由后端 AI Agents 集群驱动的实时互动学习系统。它通过大模型驱动的教学规划、动态内容生成、苏格拉底式互动教学以及学习效果分析，旨在提供高度个性化的学习体验。
**基本用法：** 用户只需要输入一个主题，然后回答系统的三个问题，就可以生成一个个性化的学习课程，不论你出于哪种学习目的，系统性学习还是单纯满足自己的好奇心，本系统都可以给出一个适合学习者情况的完整主题学习方案，然后用户只需要跟着AI教师去思考和互动，就能实现个性化的学习。

**基本界面：** 
- 着陆页：
![image](https://github.com/user-attachments/assets/125e5e0c-2e9f-4323-ab50-9fef78d42d3d)

- 课程信息页：
![image](https://github.com/user-attachments/assets/62ad564a-e9a7-4b0e-98e6-3ab2853ea3b8)

- 互动问答页
![image](https://github.com/user-attachments/assets/707ea590-f0bb-49b7-a104-a3bed42214d1)


## 主要亮点

-   **AI Agent驱动**: 由多个专门的AI Agent协同工作，覆盖主要教学流程。
-   **个性化课程规划**: `CoursePlanner` Agent 根据用户主题和学情生成定制化课程大纲。
-   **动态内容生成**: `ContentDesigner` Agent 为每个课程章节创建详细的多媒体教学内容。
-   **内容审查与迭代**: `ContentVerifier` Agent 负责审核教学内容的质量，并提供反馈进行优化。
-   **苏格拉底式互动教学**: `Teacher` Agent 以对话方式逐步引导学习，启发思考。
-   【时间关系，尚未实现】**学习伴侣**: `LearningCompanion` Agent 辅助教学，鼓励学习者参与。
-   【时间关系，尚未实现】**学习分析与反馈**: `Monitor Team` (包含 `SessionAnalyst` 和 `LearningProfiler`) 监测学习过程，分析学习效果，并提供优化建议。

## 项目结构

项目采用前后端分离架构：

```
quest-agent-verse/
├── backend/             # 后端代码 (Python, FastAPI, Agno)
│   ├── src/
│   │   ├── agents/      # 实现各类AI Agents (Teaching, Learning, Monitor Teams)
│   │   ├── api/         # FastAPI路由和API端点定义
│   │   ├── services/    # 后端核心业务逻辑服务 (如AgentService)
│   │   └── utils/       # 通用工具函数
│   ├── requirements.txt # 后端Python依赖
│   └── ...
├── src/                 # 前端代码 (React, Vite, TypeScript)
│   ├── components/      # UI组件
│   ├── contexts/        # React上下文管理
│   ├── hooks/           # 自定义React Hooks
│   ├── lib/             # 前端工具函数库
│   ├── pages/           # 应用页面级组件
│   └── services/        # 前端API服务对接
├── docs/                # 项目文档 (如prd.md)
├── start_dev.sh         # 开发环境一键启动脚本
└── README.md            # 本文档
```

## 🤖 后端 Agents 设计

后端系统由三个核心 Agent 团队组成，每个团队包含多个具有特定职责的 Agent：

### 1. Teaching Team (教学团队)
负责规划和执行教学任务。

-   **CoursePlanner (课程规划师)**: 接收用户学习主题、目标、时长和背景知识，生成结构化的课程大纲，包括章节划分、核心内容、学习目标、时长安排及课标对齐。
-   **ContentDesigner (内容设计师)**: 基于课程大纲，为每个章节设计详细的多媒体教学材料，包括情景故事、讲解文本、图片提示词、代码示例、练习题和互动环节。
-   **ContentVerifier (内容审核员)**: 审查 `CoursePlanner` 和 `ContentDesigner` 生成的内容，检查其与用户需求/学情的匹配度、准确性、完整性、课标对齐等，并提供评分和修改意见。
-   **Teacher (教师)**: 执行经验证的课程内容，以苏格拉底式对话与学习者互动，引导学习，解答疑问，并评估理解程度。

### 2. Learning Team (学习团队)
辅助学习者进行学习任务。

-   **LearningCompanion (学习伙伴)**: 作为课堂讨论的参与者，配合 `Teacher` 启发人类学习者思考，适时提供见解（不直接给答案），建立同伴关系，鼓励学习者主动输出。
-   **CodeCompanion (代码伙伴)**: *[暂不启用]* 未来版本中，将提供编程学习内容的专业辅助，如代码示例、调试帮助等。

### 3. Monitor Team (监控团队)
负责监测教学效果，形成评价与优化建议。

-   **SessionAnalyst (会话分析师)**: 实时监测和分析单次学习会话中的交互数据（问题准确率、参与度、反应速度），识别学习者困惑点，并向 `Teacher` 提供实时教学调整建议。
-   **LearningProfiler (学习档案分析师)**: 维护学习者的长期学习档案和知识图谱，整合多次会话数据，识别学习模式与趋势，生成综合评估报告，并提出个性化学习路径和课程优化建议。

## 🛠️ 技术栈

-   **前端**:
    -   [Vite](https://vitejs.dev/)
    -   [TypeScript](https://www.typescriptlang.org/)
    -   [React](https://reactjs.org/)
    -   [shadcn-ui](https://ui.shadcn.com/)
    -   [Tailwind CSS](https://tailwindcss.com/)
-   **后端**:
    -   [Python](https://www.python.org/downloads/) (3.8 或更高版本) 和 pip
    -   [FastAPI](https://fastapi.tiangolo.com/) (用于构建API)
    -   [Agno](https://deepwiki.com/agno-agi/agno) (AI Agent 开发框架)
    -   [Ollama](https://ollama.ai/) (用于本地运行大语言模型，如Qwen)


### Agent 开发框架
本项目后端 Agent 使用 [Agno](https://deepwiki.com/agno-agi/agno) 框架开发。

### MCP使用方法
Agno 框架天然支持MCP工具，只需在初始化时进行配置，即可在Agent中启用MCP服务。然后就能够在Agent任务中进行调用。

```python
async with MultiMCPTools([  
    "npx -y @openbnb/mcp-server-airbnb --ignore-robots-txt",  
    "npx -y @modelcontextprotocol/server-google-maps"  
]) as mcp_tools:  
    agent = Agent(tools=[mcp_tools])
```
### UI/UX
基于React框架，由 Figma + lovable 负责实现，鸣谢两款先进的设计软件。

## 未来展望
这次恰逢学生毕业季，人手、精力都严重短缺，分身乏术，虽然熬了几个夜依然没有拿出很漂亮的DEMO，深感遗憾。但是已经付出了这么多精力，我们总要给自己一个交代，因此还是决定提交这个粗糙、稚嫩的作品，作为对自己努力的一种肯定，并能起到抛砖引玉的效果。接下来，将在如下几个方面继续探索：
1. 继续探索AI尤其是生成式AI在STEM教育领域的新玩法，比如对接语音大模型，可以实现实时对话交互，提升学习的沉浸感和代入感；
2. 在本项目基础上完善Agent的设计，设计良好的Agent团队协作机制，能够形成有效的自监督的提升生成质量；
3. 继续探索「人」在AI教育时代的作用，设计并实践人类以不同角色与AI主导的教育体系的协作的方式和效果，争取为未来的人机共育摸索出一条可行的路径。

**实干家向右👉，我们相信「教育」是一个处于被AI彻底变革的前沿地带的领域，我们愿意做这个探索者，也不会停下探索的脚步！**

## 团队成员分工
1. 队长: 统筹协调并负责 `TeachingTeam` 中各个 Agents 的开发；
2. 队员1: 实现`LearningTeam` Agents 的开发
3. 队员2: 实现文生图逻辑的集成
4. 队员3: RAG功能集成

---
