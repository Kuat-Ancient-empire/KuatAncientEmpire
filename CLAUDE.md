# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Stellaris mod** called "Star Wars: Dawn of the Kuat" (descriptor.mod). It is a large-scale Star Wars universe mod featuring the Eternal Empire, Kuat shipyards, invasion systems, custom megastructures, and extensive event chains.

**Supported Version:** Stellaris v4.*

## Project Structure

```
Kuat Ancient Empire/
├── common/               # All game entity definitions
│   ├── buildings/        # Custom buildings (kuat_eternal_buildings.txt, etc.)
│   ├── events/           # Event chain definitions
│   ├── technology/       # Tech trees (exe_technology.txt, exe_eternal_technology.txt)
│   ├── traditions/       # Tradition trees (kuat_tradition.txt)
│   ├── scripted_triggers/  # Reusable trigger functions
│   ├── scripted_effects/   # Reusable effect functions
│   ├── scripted_variables/ # @variable definitions for balance tuning
│   ├── on_actions/       # Game event hooks (kuat_custom_on_actions.txt)
│   ├── defines/          # Game rule overrides (exe_kuat_defines.txt)
│   ├── megastructures/   # Custom megastructures
│   ├── component_templates/  # Ship weapons/components
│   ├── inline_scripts/   # Code templates for reuse
│   └── ...
├── events/              # 30+ event files (kuat_eternal_throne_events.txt, etc.)
├── localisation/        # English and Simplified Chinese
│   ├── english/
│   └── simp_chinese/
├── interface/           # GUI (.gui) and graphical (.gfx) files
├── gfx/                 # Graphics assets (icons, models, event pictures)
├── flags/               # Country/faction flags
└── sound/               # Audio files
```

## Development Workflow

### No Build Required
Stellaris mods are pure script/text files. There is no compilation step. To test:
1. Copy the mod folder to your Stellaris mod directory
2. Enable the mod in the game launcher

### Validation
- **CWTools** (VSCode extension: `eddy.eddy-stellaris-cwt`) provides real-time validation
- CWTools logs are the authoritative reference for triggers, effects, modifiers, and scopes

### Key CWTools Log Locations
| Content | Path |
|---------|------|
| Triggers & Effects | `C:\Users\<user>\.vscode\extensions\eddy.eddy-stellaris-cwt-1.1.5\.cwtools\stellaris\config\logs\trigger_docs.log` |
| Modifiers | Same directory: `modifiers.log` |
| Scopes | Same directory: `scopes.log` |

## Important Conventions

### Event Namespacing
Events use `namespace = xxx` at the top of each file. Example:
```pdx
namespace = kuat_EEstart

country_event = { id = kuat_EEstart.1 ... }
planet_event = { id = kuat_EEstart.2 ... }
```

### Localization Files
- Located in `localisation/<language>/xxx_l_<language>.yml`
- **Must be UTF-8 with BOM** encoding
- Language keys: `l_english:`, `l_simp_chinese:`

### Flag Naming Convention
The mod uses `kuat_` prefix for most custom flags/triggers/effects:
- `kuat_is_enable_eternal_origin` (scripted_trigger)
- `kuat_invasion_battle_system_effect` (scripted_effect)
- `kuat_post_apocalyptic_enable_eternalthrone_tech` (country_flag)

### Scripted Variables
Defined in `common/scripted_variables/` with `@` prefix:
```pdx
@kuat_global_weapon_range_factor = 1.0
@kuat_bio_ship_component_decrease_factor = 0.8
```

### Event Targets
The mod uses `save_global_event_target_as` and `save_event_target_as` extensively for cross-event state sharing (e.g., `event_target:Eternalempire`, `event_target:EE_Home_World`).

## Code Architecture Patterns

### Ship Component System
The mod has a complex component override system in `inline_scripts/components/` handling:
- Damage, range, cooldown, windup fixes for different ship sizes
- Separate factors for `standard_ship`, `bio_ship`, and `mutation` ship types

### Invasion System
Key files:
- `common/scripted_effects/kuat_invasion_battle_system_effect.txt`
- `common/scripted_effects/kuat_invasion_kuat_fleet.txt`
- `common/scripted_effects/kuat_invasion_eternal_fleet.txt`
- `events/kuat_eternal_invasion_events.txt`

### Automatic Colony System
Planet automation with custom variable `planet_production_array` and yearly refresh calculations in `kuat_automatic_colony_desc`.

## Mod-Specific Rules

1. **Never use hardcoded values** — Use scripted_variables from `common/scripted_variables/` for balance numbers
2. **Check prerequisites** — Buildings often require `tr_eternal_building_*` technology prerequisites
3. **Scope verification** — Always verify current scope supports the trigger/effect being used
4. **Flag cleanup** — Invasion events set many flags; ensure cleanup in event chains
5. **Localization sync** — Any new entity must have entries in both English and Simplified Chinese localization files
