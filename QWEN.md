# Kuat Ancient Empire - Stellaris Mod 项目

## 项目概述

这是一个为 Paradox Interactive 的策略游戏 **Stellaris（群星）** 开发的大型模组（Mod）。

**Mod 名称**: Star Wars: Dawn of the Kuat（星球大战：夸特的黎明）

**版本信息**:
- Mod 版本: 8.0
- 支持的游戏版本: Stellaris v4.*
- Steam 创意工坊 ID: 2461014769

**标签**: Diplomacy（外交）, Economy（经济）, Events（事件）

### 主题与背景

这是一个 **星球大战（Star Wars）** 主题的 Stellaris Mod，核心围绕 **Kuat（夸特）** 这个星球大战宇宙中的著名造船帝国。该 Mod 为游戏添加了丰富的 Star Wars 元素，包括：

- 永恒的舰队入侵事件链
- Kuat 失落帝国/觉醒帝国系统
- 新的飞升路线和传统
- 自定义舰船设计和武器系统
- 独特的建筑、区域和决策
- 复杂的剧情事件链（遗产、瘟疫、远古拉克塔等）
- 超级武器系统（如 Starkiller Base）

---

## 目录结构

### 核心目录

```
Kuat Ancient Empire/
├── descriptor.mod              # Mod 描述文件（Steam 创意工坊使用）
├── thumbnail.png               # Mod 缩略图
├── common/                     # 游戏机制定义（78个子目录）
├── events/                     # 事件脚本（33个文件）
├── localisation/               # 本地化文件
│   ├── english/               # 英文本地化
│   └── simp_chinese/          # 简体中文本地化（10个文件）
├── gfx/                        # 图形资源（12个子目录）
├── interface/                  # 界面自定义
├── flags/                      # 旗帜图标
├── fonts/                      # 自定义字体
└── sound/                      # 音效资源
```

### common/ 目录关键内容

| 目录 | 说明 |
|------|------|
| `ascension_perks/` | 自定义飞升天赋（如 ap_eternalway） |
| `buildings/` | 自定义建筑系统 |
| `component_templates/` | 舰船武器组件定义 |
| `component_sets/` | 武器组件集合 |
| `decisions/` | 行星决策 |
| `edicts/` | 法令 |
| `event_chains/` | 事件链定义 |
| `governments/` | 政府和公民（包括起源） |
| `global_ship_designs/` | 全局舰船设计 |
| `megastructures/` | 巨型建筑 |
| `on_actions/` | 事件触发器 |
| `scripted_effects/` | 脚本效果 |
| `scripted_triggers/` | 脚本触发器 |
| `technology/` | 科技定义 |
| `traditions/` | 传统 |
| `traits/` | 特质 |

### events/ 目录关键文件

| 文件 | 说明 |
|------|------|
| `kuat_eternal_return_invasion_events.txt` | 永恒舰队入侵事件 |
| `kuat_empire_return_event.txt` | 帝国回归事件 |
| `kuat_legacy_events.txt` | 遗产事件链 |
| `kuat_plague_system_events.txt` | 瘟疫系统事件 |
| `kuat_starkillerbase_events.txt` | 弑星者基地事件 |
| `kuat_shipyard_events.txt` | 造船厂事件 |
| `kuat_situation_events.txt` | 局势事件 |
| `kuat_origin_event.txt` | 起源事件 |

---

## 主要特性

### 1. 永恒舰队系统
- 来自河外星系的大规模入侵
- 动态舰队生成和进攻逻辑
- 独特的舰船设计和武器系统
- 可研究的永恒旗舰

### 2. Kuat 帝国系统
- 失落帝国和觉醒帝国机制
- 独特的飞升路线（ap_eternalway）
- 夸特造船厂系统
- 自定义政府和公民

### 3. 武器和舰船系统
- 能量武器（离子炮、激光炮、涡轮激光炮）
- 自定义舰船组件和槽位
- 动态成本计算
- 佣兵和 Boss 舰船设计

### 4. 事件和剧情
- 多线剧情事件链
- 遗产系统（Legacy）
- 远古拉克塔入侵
- 永恒王座事件

---

## 开发规范

### 文件格式

Stellaris Mod 使用以下文件格式：

- **`.txt`**: 游戏数据定义文件（使用 Paradox 脚本语法）
- **`.yml`**: 本地化文件（YAML 格式）
- **`.txt`**: 事件脚本文件

### 命名约定

- 文件前缀: `kuat_` 或 `exe_` 表示 Kuat Mod 内容
- 占位符文件: 使用 `!!!!` 前缀标记（如 `!!!!_building_placeholder.txt`）
- 覆盖文件: 使用 `!!_` 前缀（如 `!!_kuat_overwirte_events.txt`）

### 本地化

- 支持英语和简体中文
- 本地化键使用命名空间前缀（如 `exe_`, `kuat_`）
- 支持格式化文本（使用 `§E`, `§Y`, `§G`, `§R` 等颜色标签）

### 脚本模式

Mod 使用了大量 Paradox 脚本特性：

- `scripted_effects`: 可复用的脚本效果
- `scripted_triggers`: 可复用的触发器
- `inline_scripts`: 内联脚本模板（用于武器组件等）
- `on_actions`: 事件触发器
- `custom_tooltip`: 自定义工具提示

---

## 开发和测试

### Mod 开发基本流程

1. **编辑数据文件** - 修改 `common/` 目录下的 `.txt` 文件
2. **编写事件** - 在 `events/` 目录下添加事件逻辑
3. **更新本地化** - 在 `localisation/` 添加对应翻译
4. **测试 Mod** - 在 Stellaris 启动器中启用 Mod 并启动游戏

### 注意事项

- 文件修改后通常需要重启游戏才能生效
- 确保本地化键与代码中的引用一致
- 使用 `custom_tooltip` 提供玩家友好的错误提示
- 检查脚本触发器和效果的逻辑正确性

### 常见调试技巧

- 使用 `kuat_testing_events.txt` 进行功能测试
- 查看游戏日志文件排查脚本错误
- 使用游戏控制台命令调试事件

---

## 相关资源

- **Stellaris Mod 文档**: https://stellaris.paradoxwikis.com/Modding
- **Paradox 脚本参考**: https://stellaris.paradoxwikis.com/Mod_events
- **Steam 创意工坊页面**: https://steamcommunity.com/sharedfiles/filedetails/?id=2461014769

---

## 技术栈

| 类别 | 技术/格式 |
|------|-----------|
| 脚本语言 | Paradox 脚本（类 JSON 语法） |
| 本地化 | YAML 格式 |
| 图形资源 | DDS, PNG, TGA |
| 模型 | .mesh（Paradox 专用格式） |
| 音效 | .ogg, .wav |
| 版本控制 | Git |
