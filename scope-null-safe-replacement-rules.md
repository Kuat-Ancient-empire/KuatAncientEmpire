# Scope Null-Safe 替换规则

将项目中所有已知的 scope change 关键字（如 `FROM = { }`, `ROOT = { }`, `capital_scope = { }`, `PREV = { }` 等）从 `scope = { }` 替换为 `scope? = { }` 格式，规则如下：

## 替换范围

1. **`events/` 目录**：替换所有 scope change（事件代码天然处于 trigger/effect 上下文中）
2. **`common/scripted_triggers/` 目录**：整个文件属于 trigger 上下文，替换所有 scope change
3. **`common/scripted_effects/` 目录**：整个文件属于 effect 上下文，替换所有 scope change

## 排除规则

1. **`prescripted_countries/` 目录**：不替换，跳过
2. **`common/` 目录**中除了 `scripted_triggers/` 和 `scripted_effects/` 之外的子目录：不替换，跳过
3. **以下 scope change 系列不替换**：
   - `every_*`（如 `every_owned_planet`, `every_country`）
   - `random_*`（如 `random_owned_planet`, `random_country`）
   - `any_*`（如 `any_owned_planet`, `any_country`）
   - `ordered_*`（如 `ordered_owned_planet`）
   - `last_*`（如 `last_created_country`）
4. **已有 `?` 的 scope**（如 `FROM? = { }`）：不重复替换，跳过
5. **`scope = <value>` 赋值语句**（如 `type = country`）：不是 scope change，不替换
6. **代码块定义关键字**（如 `trigger = { }`, `option = { }`, `immediate = { }`）：不是 scope change，不替换

## 操作方式

- 执行前先进行 dry-run 统计影响范围（文件数和替换数）
- 展示替换前后的对比示例
- 确认无误后再执行
