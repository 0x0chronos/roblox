🌊

**ABYSS SURVIVAL**

Arquitetura de Servidor

*RemoteEvents · ModuleScripts · DataStore · Dependências*

**Visão Geral da Arquitetura**

Antes de escrever qualquer linha de gameplay, defina a arquitetura. Refatorar depois custa 3x mais tempo.

> **REGRA FUNDAMENTAL:** Nunca confie no cliente. Todo estado de jogo (inventário, HP, O₂, posição da base) vive no servidor. O cliente só envia intenções e recebe atualizações.

**Estrutura de Pastas no Roblox Studio**

> ServerScriptService
>
> ├── Main.server.lua ← inicialização de todos os sistemas
>
> ├── Modules/
>
> │ ├── OxygenSystem.lua
>
> │ ├── PressureSystem.lua
>
> │ ├── ResourceManager.lua
>
> │ ├── CraftingSystem.lua
>
> │ ├── BaseManager.lua
>
> │ ├── CreatureAI.lua
>
> │ ├── EventSystem.lua
>
> │ └── DataStore.lua
>
> └── RemoteHandler.server.lua ← único ponto de entrada de RemoteEvents
>
> ReplicatedStorage
>
> ├── Remotes/ ← todos os RemoteEvents e RemoteFunctions
>
> ├── Shared/ ← módulos usados por client e server
>
> │ ├── Config.lua ← valores de balanço (O₂, pressão, drops)
>
> │ ├── Recipes.lua ← receitas de crafting
>
> │ └── ZoneData.lua ← profundidades e biomas
>
> └── Assets/ ← sons, partículas (não modelos)
>
> StarterPlayerScripts
>
> ├── AtmosphereController.lua
>
> ├── HUDController.lua
>
> ├── InventoryClient.lua
>
> ├── SoundManager.lua
>
> └── InputHandler.lua

**Tabela Completa de RemoteEvents**

Todos os RemoteEvents ficam em ReplicatedStorage/Remotes. Nomenclatura: \[Ação\]\[Alvo\] em PascalCase.

| **RemoteEvent**   | **Direção**               | **Quem dispara**                              | **Payload (dados enviados)**                 | **Validação no servidor**                          |
|-------------------|---------------------------|-----------------------------------------------|----------------------------------------------|----------------------------------------------------|
| CollectResource   | Client → Server           | InputHandler ao pressionar E perto de recurso | {resourceId, resourceType, position}         | Checar distância \< 10 studs + cooldown 0.5s       |
| ResourceCollected | Server → Client           | ResourceManager após validar coleta           | {resourceType, amount, newInventory}         | Não precisa --- vem do servidor                    |
| CraftItem         | Client → Server           | InventoryClient ao confirmar crafting         | {recipeId, quantity}                         | Checar inventário tem ingredientes + rate limit    |
| CraftingResult    | Server → Client           | CraftingSystem após executar                  | {success, itemCrafted, newInventory, error?} | Não precisa                                        |
| PlaceBaseModule   | Client → Server           | BaseManager client ao soltar módulo           | {moduleType, cframe, serverId}               | Checar CFrame válida + sem sobreposição + tem item |
| BaseModuleUpdate  | Server → All              | BaseManager ao confirmar placement            | {action, moduleType, cframe, ownerId}        | Não precisa                                        |
| UpdateOxygen      | Server → Client           | OxygenSystem a cada 1s                        | {current, max, recharging}                   | Não precisa                                        |
| UpdatePressure    | Server → Client           | PressureSystem a cada 1s                      | {damage, zone, hasSuit}                      | Não precisa                                        |
| UpdateHP          | Server → Client           | Ao receber dano                               | {current, max, damageType}                   | Não precisa                                        |
| PlayerDied        | Server → Client           | Quando HP = 0                                 | {cause, lostResources, respawnIn}            | Não precisa                                        |
| RequestRespawn    | Client → Server           | HUDController ao clicar em respawn            | {}                                           | Rate limit: 1 vez a cada 10s                       |
| StartEvent        | Server → All              | EventSystem ao disparar evento                | {eventType, duration, location?}             | Não precisa                                        |
| EventEnded        | Server → All              | EventSystem ao finalizar                      | {eventType, rewards}                         | Não precisa                                        |
| ClaimEventReward  | Client → Server           | Player ao interagir com recompensa            | {eventId}                                    | Checar evento ativo + player participou            |
| UseItem           | Client → Server           | InputHandler ao usar item da hotbar           | {itemId, targetId?}                          | Checar item no inventário + cooldown por item      |
| PingLocation      | Client → All (via server) | InputHandler ao pressionar Q                  | {position, pingType}                         | Rate limit: 1 ping a cada 3s por jogador           |
| UpdateHUDData     | Server → Client           | Agregado a cada 0.1s                          | {o2, hp, depth, zone, pressure}              | Não precisa                                        |
| LoreFound         | Server → Client           | Player entra em trigger zone de lore          | {loreId, content, audioId}                   | Checar não foi encontrado antes (DataStore)        |
| SaveProgress      | Server → Client (ack)     | DataStore após salvar                         | {success, timestamp}                         | Não precisa                                        |

**Diagrama de Dependências entre Módulos**

Leia as setas como \"depende de\". Nunca crie dependência circular.

> Main.server.lua
>
> └── inicializa todos os módulos abaixo na ordem:
>
> 1\. Config.lua (sem dependências --- valores puros)
>
> 2\. DataStore.lua (depende de: Config)
>
> 3\. ZoneData.lua (depende de: Config)
>
> 4\. OxygenSystem.lua (depende de: Config, DataStore)
>
> 5\. PressureSystem.lua (depende de: Config, ZoneData)
>
> 6\. ResourceManager.lua (depende de: Config, ZoneData, DataStore)
>
> 7\. CraftingSystem.lua (depende de: Config, Recipes, DataStore)
>
> 8\. BaseManager.lua (depende de: Config, CraftingSystem, DataStore)
>
> 9\. CreatureAI.lua (depende de: Config, ZoneData)
>
> 10\. EventSystem.lua (depende de: Config, ResourceManager)
>
> 11\. RemoteHandler.lua (depende de: TODOS --- ponto de entrada único)

**Config.lua --- Arquivo de Balanceamento**

Todos os valores numéricos do jogo ficam aqui. Nunca hardcode valores em scripts de gameplay.

> \-- ReplicatedStorage/Shared/Config.lua
>
> local Config = {}
>
> Config.Oxygen = {
>
> MaxCapacity = 100,
>
> BaseConsumption = 1, \-- % por segundo
>
> SprintMultiplier= 1.5, \-- multiplicador ao nadar rápido
>
> RechargeRate = 12.5, \-- % por segundo na base
>
> StationRate = 3.3, \-- % por segundo em estação
>
> CriticalThreshold = 15, \-- % para alarme
>
> DangerThreshold = 5, \-- % para blur de tela
>
> }
>
> Config.Pressure = {
>
> \[1\] = {minDepth=0, maxDepth=400, damage=0 },
>
> \[2\] = {minDepth=400, maxDepth=1600, damage=5 },
>
> \[3\] = {minDepth=1600,maxDepth=4800, damage=15 },
>
> \[4\] = {minDepth=4800,maxDepth=12000, damage=30 },
>
> \[5\] = {minDepth=12000,maxDepth=math.huge,damage=60},
>
> }
>
> Config.Death = {
>
> ResourceLossPercent = 0.40, \-- 40% perdido ao morrer
>
> RareItemLossChance = 0.20, \-- épico: 20% chance de perder
>
> UniqueItemLossChance= 0.10, \-- único: 10%
>
> RespawnDelay = 3, \-- segundos antes de respawnar
>
> }
>
> Config.Resources = {
>
> CollectDistance = 10, \-- studs
>
> CollectCooldown = 0.5, \-- segundos entre coletas
>
> RespawnTime = {min=300, max=600}, \-- segundos
>
> MaxStackSize = 99,
>
> }
>
> Config.Events = {
>
> Interval = 900, \-- 15 min entre eventos
>
> MinPlayers = 2, \-- mínimo para disparar evento
>
> }
>
> return Config

**RemoteHandler.lua --- Ponto de Entrada Único**

Toda lógica de validação fica aqui antes de chamar qualquer módulo.

> \-- ServerScriptService/RemoteHandler.server.lua
>
> local Players = game:GetService(\"Players\")
>
> local RS = game:GetService(\"ReplicatedStorage\")
>
> local Remotes = RS:WaitForChild(\"Remotes\")
>
> local OxygenSystem = require(script.Parent.Modules.OxygenSystem)
>
> local CraftingSystem = require(script.Parent.Modules.CraftingSystem)
>
> local ResourceManager= require(script.Parent.Modules.ResourceManager)
>
> local BaseManager = require(script.Parent.Modules.BaseManager)
>
> \-- Rate limiting por jogador
>
> local cooldowns = {}
>
> local function checkCooldown(player, action, seconds)
>
> local key = player.UserId .. \"\_\" .. action
>
> local now = tick()
>
> if cooldowns\[key\] and now - cooldowns\[key\] \< seconds then
>
> return false
>
> end
>
> cooldowns\[key\] = now
>
> return true
>
> end
>
> \-- Validar distância
>
> local function checkDistance(player, position, maxDist)
>
> local hrp = player.Character and player.Character:FindFirstChild(\"HumanoidRootPart\")
>
> if not hrp then return false end
>
> return (hrp.Position - position).Magnitude \<= maxDist
>
> end
>
> Remotes.CollectResource.OnServerEvent:Connect(function(player, data)
>
> if not checkCooldown(player, \"collect\", 0.5) then return end
>
> if not checkDistance(player, data.position, 10) then return end
>
> ResourceManager:Collect(player, data)
>
> end)
>
> Remotes.CraftItem.OnServerEvent:Connect(function(player, data)
>
> if not checkCooldown(player, \"craft\", 1.0) then return end
>
> CraftingSystem:Craft(player, data)
>
> end)
>
> Remotes.PlaceBaseModule.OnServerEvent:Connect(function(player, data)
>
> if not checkCooldown(player, \"place\", 2.0) then return end
>
> BaseManager:PlaceModule(player, data)
>
> end)

**DataStore --- Estrutura dos Dados Salvos**

O que é salvo por jogador e como está estruturado:

> \-- Estrutura do save (JSON serializado)
>
> {
>
> version = 1,
>
> lastSaved = 1234567890,
>
> inventory = {
>
> \[\"AlgasNutritivas\"\] = 12,
>
> \[\"FerroSimples\"\] = 5,
>
> \-- etc
>
> },
>
> base = {
>
> serverId = \"abc123\", \-- base só existe no servidor atual
>
> modules = {
>
> {type=\"OxygenModule\", cframe=\"\...\", level=1},
>
> {type=\"CascoBase\", cframe=\"\...\", level=1},
>
> }
>
> },
>
> progression = {
>
> currentTier = 1,
>
> maxDepth = 340, \-- profundidade máxima já atingida
>
> totalSessions= 7,
>
> },
>
> codex = {
>
> creatures = {\"TubaraoEspreita\", \"AguaVivaEletrica\"},
>
> lore = {\"Log01\", \"Diario03\"},
>
> blueprints= {\"TrajeT1\", \"Propulsor\"},
>
> },
>
> dailyQuests = {
>
> date = \"2025-05-01\",
>
> completed= {1, 3}, \-- índices das quests concluídas hoje
>
> }
>
> }

**Checklist de Implementação**

- \[ \] Criar pasta Remotes em ReplicatedStorage com todos os RemoteEvents listados

- \[ \] Criar Config.lua com todos os valores. Não hardcode nada fora dele

- \[ \] Implementar RemoteHandler.lua com rate limiting antes de qualquer módulo

- \[ \] Implementar DataStore com retry (ver Guia Master, Cap. 15)

- \[ \] Testar: cliente não consegue alterar inventário diretamente

- \[ \] Testar: rate limiting bloqueia spam de coleta

- \[ \] Testar: save e load funcionam após sair e entrar no servidor
