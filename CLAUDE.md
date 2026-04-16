# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是《星球大战：库阿特帝国黎明》(Star Wars: Dawn of the Kuat) - 一个基于《星际迷航》(Stellaris) 的星战主题模组。模组包含自定义政府、建筑、舰队系统、武器、星球入侵机制和事件链。

## 模组结构

```
├── common/              # 游戏数据定义
│   ├── buildings/      # 建筑定义
│   ├── districts/       # 区域定义
│   ├── deposits/        # 星球资源点
│   ├── governments/     # 政府类型与公民理念
│   ├── civics/          # 公民理念(civics)
│   ├── technology/      # 科技
│   ├── scripted_effects/ # 脚本化效果
│   ├── scripted_variables/ # 脚本变量
│   ├── event_chains/    # 事件链
│   ├── decisions/       # 决策
│   ├── button_effects/  # 按钮效果
│   └── defines/         # 游戏规则调整
├── localisation/        # 文本本地化
│   ├── english/         # 英文
│   └── simp_chinese/    # 简体中文
├── gfx/                 # 图形资源(DDS格式)
│   ├── interface/       # UI图标
│   ├── models/          # 舰船模型
│   └── event_pictures/  # 事件图片
└── flags/               # 旗帜图片
```

## 文件格式说明

- **.txt 文件**: Stellaris 游戏数据脚本，使用 Paradox Scripting Language
  - 触发器(trigger): `has_country_flag`, `exists`, `is_at_war_with` 等
  - 效果(effect): `set_flag`, `add_resource`, `create_fleet` 等
  - 作用域(scope): `ROOT` = 当前触发对象, `THIS` = 事件所有者, `FROM` = 触发来源

- **.yml 文件**: 本地化文件，键值对格式
  - `key: "翻译文本"` 或 `key:0 "翻译文本"` (用于复数形式)

## 开发说明

- **无构建命令**: 模组无需编译，直接在游戏中测试
- **测试方法**: 启用模组后通过启动新游戏或加载存档测试
- **调试标志**: 代码中常见 `kuat_debug_*` 标志用于开发调试

## 关键文件

- `descriptor.mod` - 模组元数据(名称、版本、支持版本)
- `common/defines/exe_kuat_defines.txt` - 游戏规则修改(相机、图形等)
- `common/scripted_effects/` - 核心脚本化系统(自动战斗、舰队调用等)
- `localisation/*/exe_feature_l_*.yml` - 主要特性本地化
