# Unciv Mod Development Guide

This is an Unciv mod repository - a JSON-based content mod for the Unciv game (open-source Civilization clone).

## Build/Test Commands

Unciv mods are JSON-based and don't require compilation. To test changes:
1. Copy the mod folder to your Unciv mods directory
2. Launch Unciv and enable the mod in game settings
3. Start a new game with the mod enabled

No build commands, linting, or automated tests exist for this mod type.

## Project Structure

```
├── jsons/              # Game definition files
│   ├── Nations.json    # Civilization definitions
│   ├── Buildings.json  # Building definitions
│   └── Units.json      # Unit definitions
├── Images/             # Texture assets
│   ├── NationIcons/
│   ├── BuildingIcons/
│   └── UnitIcons/
├── sounds/             # Sound files
├── Atlases.json        # Texture atlas configuration
└── README.md           # Mod documentation
```

## Code Style Guidelines

### JSON Formatting
- Use tabs for indentation (consistent with existing files)
- No trailing whitespace
- Arrays should be comma-separated with proper formatting
- Use double quotes for all strings
- Maintain alphabetical ordering where logical

### File Conventions
- JSON files must be valid JSON arrays `[]`
- Each JSON file contains an array of objects
- Image files should match the `name` field in JSON definitions
- Sound files referenced by `attackSound` or similar fields

### Naming Conventions
- Nations: PascalCase (e.g., "Aliens", "Romans")
- Buildings: PascalCase (e.g., "Holodeck", "Breeders")
- Units: PascalCase (e.g., "Phasers", "Legion")
- Leaders: PascalCase (e.g., "Zyxxyz", "Caesar")
- Cities: PascalCase with apostrophes allowed (e.g., "The Hive", "Q'Throczan")

### Nation JSON Structure
Required fields:
- `name`: Nation name (string)
- `leaderName`: Leader name (string)
- `adjective`: Array of adjectives (e.g., ["alien"])
- `outerColor`: [R, G, B] array (0-255)
- `innerColor`: [R, G, B] array (0-255)

Optional fields:
- `startBias`: Terrain preference (array)
- `preferredVictoryType`: Victory type (string)
- `unique`: Unique ability name (string)
- `cities`: Array of city name strings
- `startIntroPart1`, `startIntroPart2`: Intro text
- `declaringWar`, `attacked`, `defeated`, `introduction`: Diplomacy text
- `neutralHello`, `hateHello`, `afterPeace`, `tradeRequest`: Diplomacy text
- `neutralLetsHearIt`, `neutralNo`, `neutralYes`: Response arrays
- `hateLetsHearIt`, `hateNo`, `hateYes`: Response arrays

### Building JSON Structure
Common fields:
- `name`: Building name (string)
- `replaces`: Base game building to replace (string)
- `uniqueTo`: Nation that can build this (string)
- `cost`: Production cost (integer)
- `maintenance`: Gold maintenance (integer)
- `requiredTech`: Technology requirement (string)
- `isNationalWonder`: Boolean for national wonders
- `uniques`: Array of unique ability strings

Stat fields:
- `happiness`: Happiness provided (integer)
- `culture`: Culture provided (integer)
- `science`: Science provided (integer)
- `production`: Production modifier (integer)
- `food`: Food provided (integer)

### Unit JSON Structure
Required fields:
- `name`: Unit name (string)
- `unitType`: "Ranged", "Melee", "Civilian", etc. (string)
- `movement`: Movement points (integer)
- `strength`: Combat strength (integer)
- `cost`: Production cost (integer)

Optional fields:
- `replaces`: Base game unit to replace (string)
- `uniqueTo`: Nation that can build this (string)
- `rangedStrength`: Ranged attack strength (integer)
- `range`: Attack range (integer)
- `requiredTech`: Technology requirement (string)
- `requiredResource`: Resource requirement (string)
- `promotions`: Array of promotion names
- `attackSound`: Sound effect name (string)

### Error Handling
- Invalid JSON will cause the mod to fail loading
- Missing required fields will cause undefined behavior
- Image files must exist or game will crash
- Referenced techs/buildings/units must exist in base game or mod

### Best Practices
- Always test mod in Unciv after changes
- Keep mod content balanced with base game
- Use descriptive names for cities and abilities
- Include diplomacy text for all scenarios
- Verify color contrast for nation colors
- Document special abilities in comments if needed
