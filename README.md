# bazi-name-master

`bazi-name-master` 是一个面向 Codex / Agent 场景的八字命名技能项目，用于把“出生信息收集、四柱计算核验、命局分析、候选名评估”串成一条可执行、可复核的工作流。

这个项目的目标不是泛泛给名字灵感，而是让命名过程先立盘、再辨病药、最后评估名字是否真正对盘。

## 项目内容

- `SKILL.md`：技能主说明，定义触发条件、对话路由、子任务职责和输出结构。
- `scripts/calculate_bazi.py`：统一的八字计算脚本，使用 `lunar-python` 进行排盘与四柱一致性核验。
- `references/`：命名原则、资料优先级、平台风格研究等参考资料。
- `evals/evals.json`：用于验证技能行为是否符合预期的评测样例。

## 适用场景

- 用户只提供出生年月日时、历法和出生地，需要先计算八字。
- 用户已经给出四柱八字，希望直接分析命局与命名方向。
- 用户已经有候选名字，希望结合已核验的八字做拆字解读、打分和排序。

## 工作流概览

1. 收集必要信息，确认姓氏、性别、出生时间、历法、出生地等基础输入。
2. 使用脚本统一计算四柱，必要时与用户自带四柱做一致性核验。
3. 基于核验后的八字分析日元旺衰、病药、喜用忌用和命名补益方向。
4. 对候选名字进行字义、音律、字形与命理适配度评估。

## 八字脚本使用方式

本项目默认使用 `uv` 运行脚本。

### 公历示例

```bash
uv run /Users/Bai/.agents/skills/bazi-name-master/scripts/calculate_bazi.py \
  --calendar solar \
  --date 2024-04-22 \
  --time 13:30 \
  --birthplace "江苏南京"
```

### 农历示例

```bash
uv run /Users/Bai/.agents/skills/bazi-name-master/scripts/calculate_bazi.py \
  --calendar lunar \
  --date 2024-03-14 \
  --time 13:30 \
  --birthplace "江苏南京"
```

### 一致性核验示例

```bash
uv run /Users/Bai/.agents/skills/bazi-name-master/scripts/calculate_bazi.py \
  --calendar solar \
  --date 2024-04-22 \
  --time 13:30 \
  --birthplace "江苏南京" \
  --expected-pillars "甲辰,戊辰,丙辰,乙未"
```

## 设计原则

- 先核盘，再分析，不在信息不完整时抢跑下结论。
- 命局判断优先于审美修辞。
- 名字推荐必须先过补益与避讳筛选，再比较出处、音律与现代审美。
- 候选名字评估必须基于已核验的八字结果，不允许跳过前置计算。

## 维护建议

- 如果项目目录名变更，务必同步检查 `SKILL.md`、`evals/evals.json` 与文内绝对路径。
- 如果更新排盘规则或脚本参数，记得同时更新 `README.md` 和 `SKILL.md` 中的示例命令。
- 新增参考资料时，优先放入 `references/`，避免把大段资料直接堆进 `SKILL.md`。
