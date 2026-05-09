ABYSS SURVIVAL — Guia de Otimização de Performance

🌊

**ABYSS SURVIVAL**

Guia de Otimização de Performance

*LOD · Pooling · RunService · Memory · Profiler*


# **Meta de Performance**
Servidor com 12 jogadores: < 50ms de tick. Cliente: 60fps estável em mobile (iPhone SE 2020 como baseline).

**REGRA PRINCIPAL:** Meça antes de otimizar. Use o Microprofiler do Roblox (Ctrl+F6) para identificar onde o tempo está sendo gasto antes de fazer mudanças cegas.

# **Level of Detail (LOD)**
## **Criaturas distantes**
-- CreatureAI.lua — dentro do update loop

local LOD\_DISTANCE = 150  -- studs

RunService.Heartbeat:Connect(function(dt)

`  `for \_, creature in pairs(activeCreatures) do

`    `local nearestPlayer, dist = creature:getNearestPlayer()

`    `if dist > LOD\_DISTANCE then

`      `-- LOD: só atualiza a cada 5 frames

`      `creature.lodCounter = (creature.lodCounter or 0) + 1

`      `if creature.lodCounter % 5 ~= 0 then continue end

`    `else

`      `creature.lodCounter = 0

`    `end

`    `creature:update(dt)

`  `end

end)

## **Assets decorativos — streaming e LoD visual**
- Todo asset decorativo (coral, rocha, algas): CastShadow = false
- Modelos distantes > 200 studs: substituir por BillboardGui simples ou desativar
- Ativar "Level of Detail" = Disabled em MeshParts decorativos (Studio → Properties)
- StreamingEnabled = true no workspace — assets carregam só próximos ao jogador

# **Object Pooling**
## **Pool de criaturas**
-- Em vez de Destroy() + Instance.new(), use pool:

local CreaturePool = {}

local function getFromPool(creatureType)

`  `for \_, obj in ipairs(CreaturePool) do

`    `if obj.type == creatureType and not obj.active then

`      `obj.active = true

`      `obj.model.Parent = workspace.Creatures

`      `return obj

`    `end

`  `end

`  `-- Pool vazia: cria novo

`  `local template = ReplicatedStorage.Creatures:FindFirstChild(creatureType)

`  `local model = template:Clone()

`  `local obj = {type=creatureType, model=model, active=true}

`  `table.insert(CreaturePool, obj)

`  `model.Parent = workspace.Creatures

`  `return obj

end

local function returnToPool(obj)

`  `obj.active = false

`  `obj.model.Parent = nil  -- remove do workspace mas não destrói

`  `-- reset posição e HP aqui

end

## **Pool de nós de recursos**
-- ResourceManager.lua — ao coletar, não destrói o Part

local function deactivateNode(node)

`  `node.part.Transparency = 1

`  `node.part.CanCollide   = false

`  `node.part.CanTouch     = false

`  `node.available = false

end

local function reactivateNode(node)

`  `node.part.Transparency = 0

`  `node.part.CanCollide   = true

`  `node.part.CanTouch     = true

`  `node.available = true

end

# **Debounce em RunService**
-- Errado: checa toda lógica em todo frame (60x/s)

RunService.Heartbeat:Connect(function()

`  `checkAllZones()       -- pesado

`  `updateAllCreatures()  -- pesado

`  `broadcastHUD()        -- pesado

end)

-- Certo: usa acumuladores de tempo

local timers = { zone=0, creature=0, hud=0, lore=0 }

RunService.Heartbeat:Connect(function(dt)

`  `timers.zone    = timers.zone    + dt

`  `timers.creature= timers.creature+ dt

`  `timers.hud     = timers.hud     + dt

`  `timers.lore    = timers.lore    + dt

`  `if timers.creature >= 0.0167 then  -- 60fps para IA

`    `CreatureAI:update(timers.creature)

`    `timers.creature = 0

`  `end

`  `if timers.zone >= 0.5 then         -- 2x/s para zona

`    `PressureSystem:update(timers.zone)

`    `LoreSystem:checkProximity()

`    `timers.zone = 0

`  `end

`  `if timers.hud >= 0.1 then          -- 10x/s para HUD

`    `OxygenSystem:update(timers.hud)

`    `OxygenSystem:broadcastHUD()

`    `timers.hud = 0

`  `end

`  `if timers.lore >= 1.0 then         -- 1x/s para lore

`    `timers.lore = 0

`  `end

end)

# **Limite de Partículas**
-- ParticleManager (LocalScript) — máximo 3 emitters ativos por jogador

local activeEmitters = {}

local MAX\_EMITTERS   = 3

local function activateEmitter(emitter)

`  `if #activeEmitters >= MAX\_EMITTERS then

`    `-- Remove o mais antigo

`    `local oldest = table.remove(activeEmitters, 1)

`    `oldest.Enabled = false

`  `end

`  `emitter.Enabled = true

`  `table.insert(activeEmitters, emitter)

end

# **Como Usar o Microprofiler**
1. No Roblox Studio em Play mode: pressione Ctrl+F6 para abrir
1. Procure por funções que aparecem mais de 1ms por frame
1. Hover sobre uma barra para ver qual função está custando tempo
1. Labels a procurar: "Heartbeat", "RunService", "Render"
1. Se "Render" domina: problema em assets/partículas. Se "Heartbeat": problema em scripts
1. Use debug.profilebegin("MinhaFuncao") e debug.profileend() para medir funções específicas

|**Sintoma**|**Causa provável**|**Solução**|
| :- | :- | :- |
|Server tick > 50ms|Loop de IA rodando muito frequentemente|Adicionar LOD e debounce nas criaturas|
|FPS < 30 no cliente|Muitas partículas ou MeshParts sem LOD|Desativar CastShadow, limitar emitters, streaming|
|Memory leak (RAM sobe)|Objetos sendo criados mas não destruídos|Verificar pooling, checar Clone() sem Destroy()|
|RemoteEvent lag|Muitos eventos por segundo|Agregar dados em uma mensagem só (UpdateHUDData)|
|Travada ao salvar|DataStore síncrono bloqueando thread|Sempre usar task.spawn() ou pcall async|

Abyss Survival — Guia de Otimização de Performance   v1.0
