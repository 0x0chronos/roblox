ABYSS SURVIVAL — Wireframes de UI — Estrutura dos Menus

🌊

**ABYSS SURVIVAL**

Wireframes de UI — Estrutura dos Menus

*ScreenGui · Hierarquia · Tamanhos · Comportamento*


# **Padrão de Estrutura**
Todos os menus seguem a mesma hierarquia base no Roblox Studio:

PlayerGui

├── HUD (ScreenGui, ResetOnSpawn=false)

│   ├── OxygenBar (Frame)

│   │   ├── Fill (Frame)

│   │   └── Label (TextLabel)

│   ├── HPBar (Frame, Visible=false por padrão)

│   │   └── Fill (Frame)

│   ├── DepthIndicator (Frame)

│   │   ├── DepthText (TextLabel)

│   │   └── ZoneText (TextLabel)

│   ├── PressureBar (Frame)

│   ├── SonarMinimap (Frame)

│   ├── Hotbar (Frame)

│   │   └── Slot\_1..8 (Frame × 8)

│   ├── ObjectiveTracker (Frame)

│   ├── EventIndicator (Frame, Visible=false)

│   └── DamageOverlay (Frame, Transparency=1)

├── Inventory (ScreenGui, Enabled=false)

├── Crafting  (ScreenGui, Enabled=false)

├── BaseMenu  (ScreenGui, Enabled=false)

├── Codex     (ScreenGui, Enabled=false)

├── Map       (ScreenGui, Enabled=false)

├── Notifications (ScreenGui, ResetOnSpawn=false)

└── Tutorial  (ScreenGui, ResetOnSpawn=false)

# **HUD — Especificação de Layout**

|**Elemento**|**AnchorPoint**|**Position**|**Size**|**ZIndex**|
| :- | :- | :- | :- | :- |
|OxygenBar|(0.5,1)|(0.5,0, 1,-90)|(0,240, 0,16)|5|
|HPBar|(0,1)|(0,10, 1,-110)|(0,180, 0,12)|5|
|DepthIndicator|(1,0)|(1,-10, 0,10)|(0,180, 0,48)|5|
|PressureBar|(1,0)|(1,-10, 0,64)|(0,180, 0,10)|5|
|SonarMinimap|(0,0)|(0,10, 0,10)|(0,120, 0,120)|5|
|Hotbar|(0.5,1)|(0.5,0, 1,-50)|(0,396, 0,44)|5|
|EventIndicator|(0.5,0)|(0.5,0, 0,10)|(0,320, 0,36)|6|
|ObjectiveTracker|(1,0.5)|(1,-10, 0.5,0)|(0,220, 0,120)|5|
|DamageOverlay|(0,0)|(0,0, 0,0)|(1,0, 1,0)|10|

# **Menu de Inventário — Hierarquia Completa**
Inventory (ScreenGui)

└── Background (Frame) — AnchorPoint(0.5,0.5), Position(0.5,0,0.5,0), Size(0,600,0,450)

`    `├── TitleBar (Frame) — Size(1,0, 0,40)

`    `│   ├── Title (TextLabel) — "Inventário"

`    `│   └── CloseBtn (TextButton) — "✕", AnchorPoint(1,0.5)

`    `├── TabBar (Frame) — Size(1,0, 0,32)

`    `│   ├── Tab\_All (TextButton)      — "Todos"

`    `│   ├── Tab\_Resources (TextButton)— "Recursos"

`    `│   ├── Tab\_Equipment (TextButton)— "Equipamento"

`    `│   └── Tab\_Modules (TextButton)  — "Módulos"

`    `├── ItemGrid (Frame) — Size(1,-220,0, 1,-80)

`    `│   └── UIGridLayout — CellSize(0,72,0,72), CellPadding(0,6,0,6)

`    `│       └── ItemCard (Frame × N) — gerado por script

`    `│           ├── Icon (ImageLabel)

`    `│           ├── QuantityLabel (TextLabel)

`    `│           └── RarityBorder (UIStroke)

`    `└── ItemDetail (Frame) — Size(0,200, 1,-80), AnchorPoint(1,0)

`        `├── ItemIcon (ImageLabel) — Size(0,64,0,64)

`        `├── ItemName (TextLabel)

`        `├── ItemDesc (TextLabel)

`        `├── RarityLabel (TextLabel)

`        `└── ActionBtn (TextButton) — "Equipar" / "Usar" / "Descartar"

# **Menu de Crafting — Hierarquia Completa**
Crafting (ScreenGui)

└── Background (Frame) — Size(0,700,0,480)

`    `├── TitleBar — "Fabricação"

`    `├── TierFilter (Frame) — Size(1,0,0,32)

`    `│   ├── Btn\_Tier0 "Tier 0"

`    `│   └── Btn\_Tier1 "Tier 1"

`    `├── RecipeList (ScrollingFrame) — Size(0,260,1,-80)

`    `│   └── RecipeCard (Frame × N) — gerado por script

`    `│       ├── ItemIcon (ImageLabel)

`    `│       ├── RecipeName (TextLabel)

`    `│       └── StatusDot — verde (pode craftar) / vermelho (não pode)

`    `└── RecipeDetail (Frame) — Size(1,-270,1,-80), Position(0,270)

`        `├── OutputIcon (ImageLabel) — Size(0,80,0,80)

`        `├── OutputName (TextLabel)

`        `├── OutputDesc (TextLabel)

`        `├── IngredientsFrame (Frame)

`        `│   └── IngredientRow × N — Icon + "5× Ferro" + check/X

`        `├── QtySelector (Frame) — botões "-" e "+", label de quantidade

`        `├── CraftTime (TextLabel) — "Tempo: 8s"

`        `└── CraftBtn (TextButton) — "Fabricar" (disabled se não pode)

# **Tutorial — Hierarquia do Objective Tracker**
Tutorial (ScreenGui)

└── ObjectiveBox (Frame) — AnchorPoint(0,0.5), Size(0,220,0,80)

`    `├── Header (TextLabel) — "OBJETIVO", tamanho pequeno, cor Teal

`    `├── Title (TextLabel)  — nome da quest atual, bold

`    `├── Desc (TextLabel)   — descrição breve

`    `├── ProgressBar (Frame)

`    `│   └── Fill (Frame)   — atualizado por script

`    `└── ProgressText (TextLabel) — "2 / 5"

-- Animação de nova objective: slide da esquerda + highlight por 1s

-- Animação de conclusão: check verde + shrink + desaparece em 2s

# **Codex — Estrutura**
Codex (ScreenGui)

└── Background (Frame) — Size(0,700,0,500)

`    `├── TabBar

`    `│   ├── Tab\_Creatures "Criaturas"

`    `│   ├── Tab\_Lore      "Lore"

`    `│   └── Tab\_Blueprints"Blueprints"

`    `├── ListPanel (Frame) — Size(0,240,1,-80)

`    `│   └── EntryCard × N

`    `│       ├── Thumbnail (ImageLabel) — 48×48

`    `│       └── EntryName (TextLabel)

`    `└── DetailPanel (Frame) — Size(1,-250,1,-80)

`        `├── DetailImage (ImageLabel) — 120×120

`        `├── DetailTitle (TextLabel)

`        `├── DetailText (TextLabel) — TextWrapped=true

`        `└── [se lore] AudioPlayBtn (TextButton)
Abyss Survival — Wireframes de UI — Estrutura dos Menus   v1.0
