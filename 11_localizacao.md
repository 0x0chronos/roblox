ABYSS SURVIVAL  —  Localização PT / EN / ES  |  Roblox Studio

🌊

**ABYSS SURVIVAL**

Localização PT / EN / ES

*Sistema de Localização do Roblox · Strings Traduzidas · Guia de Implementação*


# **Por que Localizar**
O Roblox tem 88 milhões de usuários ativos mensais. Apenas 15% são brasileiros. Inglês dobra o alcance potencial. Espanhol adiciona LATAM e Espanha. Os três idiomas cobrem 90%+ do público do Roblox.

# **Como Funciona o Sistema de Localização do Roblox**
1. Acesse Creator Hub → seu jogo → "Localization" no menu lateral
1. Clique em "Manage Translations" → Roblox gera uma tabela de strings automaticamente escaneando o jogo
1. Exporte a tabela como CSV ou edite direto na interface
1. Para cada string: adicione a tradução em EN e ES (Português já é a língua base)
1. Publique o jogo — o Roblox detecta o idioma do jogador e exibe a tradução correta automaticamente

**IMPORTANTE:** Strings dinâmicas (ex: "Você coletou 5 Cristais Marinhos") precisam usar LocalizationService no código para funcionar. Strings estáticas (labels, menus) são detectadas automaticamente.

# **Tabela de Strings — HUD e Menus**

|**ID da String**|**Português (base)**|**English**|**Español**|
| :- | :- | :- | :- |
|hud\_oxygen|Oxigênio|Oxygen|Oxígeno|
|hud\_depth|Profundidade|Depth|Profundidad|
|hud\_zone|Zona {n} — {name}|Zone {n} — {name}|Zona {n} — {name}|
|hud\_pressure|Pressão|Pressure|Presión|
|zone\_name\_1|Zona Costeira|Coastal Zone|Zona Costera|
|zone\_name\_2|Recife Profundo|Deep Reef|Arrecife Profundo|
|zone\_name\_3|Abyss Raso|Shallow Abyss|Abismo Somero|
|zone\_name\_4|Abyss Profundo|Deep Abyss|Abismo Profundo|
|zone\_name\_5|Zona Hadal|Hadal Zone|Zona Hadal|
|menu\_inventory|Inventário|Inventory|Inventario|
|menu\_crafting|Fabricação|Crafting|Fabricación|
|menu\_base|Base|Base|Base|
|menu\_codex|Codex|Codex|Codex|
|menu\_map|Mapa|Map|Mapa|
|btn\_craft|Fabricar|Craft|Fabricar|
|btn\_build|Construir|Build|Construir|
|btn\_collect|Coletar|Collect|Recoger|
|btn\_equip|Equipar|Equip|Equipar|
|btn\_discard|Descartar|Discard|Descartar|
|notif\_zone\_entered|Entrando em {zone}|Entering {zone}|Entrando en {zone}|
|notif\_event\_started|Evento: {event}|Event: {event}|Evento: {event}|
|notif\_depth\_record|Novo recorde! {depth}m|New record! {depth}m|¡Nuevo récord! {depth}m|

# **Tabela de Strings — Recursos e Itens**

|**ID**|**Português**|**English**|**Español**|
| :- | :- | :- | :- |
|item\_algas|Algas Nutritivas|Nutritious Seaweed|Algas Nutritivas|
|item\_sucata|Sucata|Scrap Metal|Chatarra|
|item\_calcario|Calcário|Limestone|Caliza|
|item\_ferro|Ferro Simples|Simple Iron|Hierro Simple|
|item\_cristal|Cristal Marinho|Sea Crystal|Cristal Marino|
|item\_ferro\_abissal|Ferro Abissal|Abyssal Iron|Hierro Abisal|
|item\_titanio|Titânio das Profundezas|Deep Titanium|Titanio Abisal|
|item\_gel|Gel Bioluminescente|Bioluminescent Gel|Gel Bioluminiscente|
|item\_nucleo|Núcleo Térmico|Thermal Core|Núcleo Térmico|
|item\_shard|Shard Hadal|Hadal Shard|Fragmento Hadal|
|item\_reliquia|Relíquia do Naufrágio|Shipwreck Relic|Reliquia del Naufragio|
|item\_kit\_medico|Kit Médico Simples|Basic Medical Kit|Kit Médico Básico|
|item\_tanque\_o2|Tanque de Oxigênio|Oxygen Tank|Tanque de Oxígeno|
|item\_traje\_t1|Traje de Pressão T1|Pressure Suit T1|Traje de Presión T1|
|item\_arpao|Arpão Básico|Basic Harpoon|Arpón Básico|

# **Strings Dinâmicas — Código**
-- LocalScript — usando LocalizationService para strings dinâmicas

local LocalizationService = game:GetService("LocalizationService")

local Players = game:GetService("Players")

local translator

pcall(function()

`  `translator = LocalizationService:GetTranslatorForPlayerAsync(

`    `Players.LocalPlayer)

end)

local function translate(key, args)

`  `if translator then

`    `local ok, result = pcall(function()

`      `return translator:FormatByKey(key, args)

`    `end)

`    `if ok then return result end

`  `end

`  `return key  -- fallback: mostrar a key se falhar

end

-- Exemplos de uso:

print(translate("notif\_zone\_entered", {zone = "Recife Profundo"}))

-- EN output: "Entering Deep Reef"

-- ES output: "Entrando en Arrecife Profundo"

print(translate("notif\_depth\_record", {depth = 340}))

-- EN output: "New record! 340m"

# **Strings de Lore — Não Localizar por Enquanto**
Os fragmentos de lore (logs de áudio, diários, notas) são em Português no MVP. Localize apenas após o launch, se o analytics mostrar audiência significativa de EN/ES.

Prioridade de localização para updates futuros:

1. Tutorial e objetivos guiados (maior impacto em novos jogadores EN/ES)
1. Nomes de zonas e recursos (já na tabela acima)
1. Fragmentos de lore (mais trabalhoso — deixe por último)
Abyss Survival — Localização PT / EN / ES	v1.0
