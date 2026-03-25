---
name: art-design-skill
description: 服化道设计技能。当需要为人物和场景设计参考图提示词时使用此技能。人物参考图采用面部特写 + 三视图格式，场景参考图采用宫格图格式。所有参考图提示词写入全局素材库，跨集累积。
---

# Art Design Skill - 服化道设计技能

## 核心理念

**参考图是保持人物和场景一致性的关键。**

有了参考图，不需要在每条提示词里反复描述角色长什么样、场景是什么布局，Seedance 能直接"看到"。

---

## 人物参考图设计

### 输出格式

**单人物参考图**：
- **左半边**：面部特写（清晰展示五官）
- **右半边**：全身正面、侧面、背面三视图
- **背景**：纯白色，无阴影
- **比例**：16:9

### 提示词模板

```markdown
## [角色名] - 人物参考图

**用途**：角色一致性参考，用于所有该角色出镜的镜头

**提示词**：
```
character sheet of [角色名], split composition, left side is extreme close-up of face showing detailed facial features, right side is full body three-view drawing including front view, side view, back view, [外貌描述], [服装描述], pure white background, no shadow, symmetrical lighting, character design sheet, 8k quality --ar 16:9 --style raw
```

**生成参数**：
- 比例：16:9
- 风格：角色设定图
- 背景：纯白

**使用范围**：第 X 集 - 第 X 集

**状态**：✅ 已生成 / ⬜ 待生成
```

### 人物描述维度

| 维度 | 描述要点 | 示例 |
|------|----------|------|
| **年龄** | 具体年龄或年龄段 | "28 岁" / "中年" |
| **体型** | 身高、胖瘦、肌肉 | "身高 185cm，精瘦，有肌肉线条" |
| **发型** | 长度、颜色、样式 | "黑色短发，微乱，刘海遮住额头" |
| **面部** | 五官特点、表情习惯 | "剑眉，眼神锐利，嘴角常带冷笑" |
| **服装** | 款式、颜色、材质 | "黑色丝绸唐装，金色龙纹刺绣" |
| **配饰** | 手表、戒指、项链等 | "左手戴翡翠扳指，脖子上挂玉佩" |
| **气质** | 整体给人的感觉 | "不怒自威，有上位者气场" |

---

## 场景参考图设计

### 输出格式

**场景宫格图**：
- **1-9 个场景**：3×3 九宫格
- **10-12 个场景**：3×4 十二宫格
- **13-16 个场景**：4×4 十六宫格
- **背景**：无统一背景，每个场景独立

### 提示词模板

```markdown
## 场景宫格图 - 第 X 集

**用途**：本集所有场景的环境参考

**提示词**：
```
contact sheet of scene designs, [数量]grid layout, each cell shows a different location from the drama: [场景 1 描述]; [场景 2 描述]; [场景 3 描述]; ... consistent art style, cinematic lighting, 8k quality --ar 1:1 --style raw
```

**生成参数**：
- 比例：1:1（正方形）
- 风格：电影感
- 布局：[数量]grid

**拆分解说**：
| 格号 | 场景名 | 用途 |
|------|--------|------|
| 1 | 苏家别墅门口 | 第 1 集开场 |
| 2 | 苏家客厅 | 对话场景 |
| 3 | ... | ... |

**状态**：✅ 已生成 / ⬜ 待生成
```

### 场景描述维度

| 维度 | 描述要点 | 示例 |
|------|----------|------|
| **地点** | 室内/室外、具体位置 | "苏家别墅客厅，豪华装修" |
| **时间** | 日/夜、具体时段 | "深夜，只有台灯照明" |
| **色调** | 主色调、色温 | "暖黄色调，3000K 灯光" |
| **光源** | 光源方向、类型 | "左侧落地窗射入月光，冷白色" |
| **道具** | 关键道具有哪些 | "真皮沙发、大理石茶几、水晶吊灯" |
| **氛围** | 整体感觉 | "压抑、紧张" |
| **空间** | 空间大小、布局 | "挑高 5 米，东西长 10 米" |

---

## 全局素材库管理

### 文件结构

```
assets/
├── character-prompts.md 人物参考图提示词库
├── scene-prompts.md 场景参考图提示词库
└── reference-images/ 生成的参考图（可选）
    ├── characters/
    └── scenes/
```

### 跨集累积规则

| 情况 | 处理方式 | 标注 |
|------|----------|------|
| **新角色首次出现** | 新增条目 | `【新增】` |
| **已有角色换装** | 新增变体条目 | `【变体】晚礼服版` |
| **已有角色服装不变** | 跳过，不重复生成 | `【复用】见第 1 集` |
| **新场景首次出现** | 新增条目 | `【新增】` |
| **已有场景复用** | 跳过，不重复生成 | `【复用】见第 1 集` |

### 素材库更新流程

1. **读取导演讲戏本**，提取本集所有人物和场景
2. **对比已有素材库**，识别新增/变体/复用
3. **编写新增参考图提示词**
4. **更新素材库文件**
5. **标注使用范围**（哪几集使用）

---

## 创作流程

### 步骤 1：读取导演讲戏本

读取 `03-director-notes.md`，提取：
- 所有出场人物（按场次）
- 所有场景（按场次）

### 步骤 2：对比素材库

检查 `assets/character-prompts.md` 和 `assets/scene-prompts.md`：
- 哪些人物是新的？
- 哪些人物需要换装变体？
- 哪些人物可以复用？
- 哪些场景是新的？
- 哪些场景可以复用？

### 步骤 3：编写人物提示词

为每个新增/变体人物编写参考图提示词

### 步骤 4：编写场景提示词

为本集所有场景编写宫格图提示词

### 步骤 5：更新素材库

追加到 `assets/character-prompts.md` 和 `assets/scene-prompts.md`

---

## 输出模板

### assets/character-prompts.md

```markdown
# 人物参考图提示词库

> 剧名：[剧名]
> 更新时间：YYYY-MM-DD

---

## 主角

### 叶辰

**首次出现**：第 1 集

**身份**：龙王殿殿主 / 苏家赘婿（表面）

**提示词**：
```
character sheet of Ye Chen, split composition, left side is extreme close-up of face showing detailed facial features: sharp sword-like eyebrows, cold determined eyes, stubble on chin; right side is full body three-view drawing including front view, side view, back view: 28 years old, height 185cm, lean muscular build, wearing worn blue security guard uniform, white T-shirt underneath, black worn jeans, black leather shoes, pure white background, no shadow, symmetrical lighting, character design sheet, 8k quality --ar 16:9 --style raw
```

**使用范围**：第 1-80 集

**变体**：
- 【变体】龙王装：黑色丝绸唐装，金色龙纹刺绣（第 4 集起）
- 【变体】保安装：蓝色保安制服（第 1-3 集）

**状态**：✅ 已生成

**参考图**：`reference-images/characters/ye-chen-main.png`

---

### 苏清雪

**首次出现**：第 2 集

**身份**：苏家大小姐 / 叶辰妻子

**提示词**：
```
character sheet of Su Qingxue, split composition, left side is extreme close-up of face: gentle features, large watery eyes, soft expression; right side is full body three-view: 26 years old, height 165cm, slim figure, wearing white evening dress, long black hair, pure white background, character design sheet, 8k quality --ar 16:9 --style raw
```

**使用范围**：第 2-80 集

**变体**：
- 【变体】睡裙版：白色睡裙（第 3 集）
- 【复用】礼服版：见第 2 集

**状态**：✅ 已生成
```

### assets/scene-prompts.md

```markdown
# 场景参考图提示词库

> 剧名：[剧名]
> 更新时间：YYYY-MM-DD

---

## 第 1 集

**场景宫格**：3×3 九宫格（共 3 个场景）

**提示词**：
```
contact sheet of scene designs, 3grid layout, each cell shows a different location from the drama: 
Cell 1: exterior of luxury villa, modern Chinese architecture style, iron gate half open, morning sunlight casting long shadows on marble steps; 
Cell 2: living room of villa, luxurious decoration, crystal chandelier, leather sofas, marble coffee table, warm yellow lighting; 
Cell 3: entrance hall of villa, dim lighting, only street light coming through curtain gap, cold white light; 
consistent art style, cinematic lighting, 8k quality --ar 1:1 --style raw
```

**拆解**：
| 格号 | 场景名 | 用途 | 状态 |
|------|--------|------|------|
| 1 | 苏家别墅门口 | 第 1 集开场 | ✅ |
| 2 | 苏家客厅 | 生日宴场景 | ✅ |
| 3 | 别墅玄关 | 昏暗场景 | ✅ |

**状态**：✅ 已生成

**参考图**：`reference-images/scenes/ep1-scenes.png`

---

## 第 2 集

**新增场景**：无

**状态**：【全部复用】见第 1 集
```

---

## 注意事项

1. **人物提示词必须包含**：面部特写 + 三视图
2. **场景提示词必须标注**：每个格号对应的场景名
3. **跨集累积**：不要重复生成已有的角色/场景
4. **变体标注清晰**：换装、换发型等要单独标注
5. **状态及时更新**：生成后标记✅

---

## 与分镜师对接

分镜师写分镜表时，直接引用参考图：

```markdown
| 镜号 | 景别 | 内容 | 运镜 | 时长 | 参考图 |
|------|------|------|------|------|--------|
| 1-1 | 中景 | 叶辰站在门口 | 固定 | 4s | @ye-chen-main.png |
| 1-2 | 近景 | 王桂芳走出来 | 推镜 | 5s | @wang-guifang-main.png |
```

---

*服化道的任务：为导演清单中的每个人物和场景设计参考图提示词，建立全局视觉基准*