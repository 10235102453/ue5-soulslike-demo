# UE5 类魂动作游戏 Demo（AI 辅助开发 / Vibe Coding）

基于 **Unreal Engine 5** 独立完成的第三人称类魂动作游戏原型 Demo，完整实现 **锁定战斗 → 拾取交互 → 血瓶回复 → 程序化音效反馈** 的核心玩法循环。

- **B 站实机演示视频**：https://www.bilibili.com/video/BV1fgyvztERA
- **开发范式**：Vibe Coding（自然语言与 Claude Code、WorkBuddy 协作，完成需求拆解、蓝图架构设计、脚本编写与工程排错全流程）
- **技术栈**：Unreal Engine 5 · Blueprint · ActorComponent · Enhanced Input · Blueprint Interface · Python（音频特征分析）

---

## 核心玩法与系统实现

1. **角色锁定系统（Lock-On）**
   - 采用「球形射线检测 + 三重校验」保证锁定可靠性与容错手感；
   - 每帧「向量转旋转」控制镜头朝向目标，并针对相机俯角导致的检测失效完成几何修正。
2. **解耦拾取交互系统**
   - 基于 **Enhanced Input** 与 **Blueprint Interface** 解耦，构建「范围检测 + 按键触发」两段式防误触拾取交互机制。
3. **血瓶回复与完整战斗循环**
   - 串联敌人锁定战斗、按键拾取与血瓶血量回复，形成完整可玩的类魂核心体验闭环。
4. **程序化音效管线（Python 自动化筛选）**
   - 通过 Python 脚本对 21 条免费音效素材进行低频占比、步频等声学特征量化筛选，并自动完成 16bit 转码与伪 WAV 文件头检测修复，搭建覆盖移动、战斗、拾取、回复的音效反馈系统。
5. **工程集成与问题治理**
   - 完成 440 个 UE 原生资产结构化迁移，并排查治理 Simulate 模式误用、调试绘制残留、渲染警告等 5 类工程问题。

---

## 仓库目录说明

为遵守 GitHub 单文件大小限制及第三方资产授权规范，本仓库包含项目配置与全部自研蓝图/交互/UI/音频资产，**不包含**体积较大的 Epic/Fab 第三方商城资产包与引擎编译缓存（已在 `.gitignore` 中排除）：

- `mysoul.uproject`：UE5 工程入口文件
- `Config/`：引擎、输入与项目配置文件
- `Content/Blueprints/`：核心蓝图逻辑与组件（锁定、战斗、交互等）
- `Content/ThirdPerson/`：第三人称角色与输入配置
- `Content/Audio/`：经 Python 特征筛选与转码修复后的游戏音效
- `Content/UI/`：血条、锁定与交互 HUD 界面
- `Content/LevelPrototyping/`：关卡原型结构

### 本地完整运行所需第三方免费资产（Fab / Epic 商城）
如需在本地 UE5 编辑器完整还原场景与角色表现，请在 Fab / Epic 商城免费获取以下资产包并导入 `Content/` 目录：
- `ParagonGrux` / `ParagonKwang`（Paragon 角色与特效资产）
- `Ft_Gothic_castle`（哥特城堡场景资产）
- `StarterContent`（UE 官方新手内容包）
- `FreeGameSoundsVol1`（免费游戏音效素材包）
