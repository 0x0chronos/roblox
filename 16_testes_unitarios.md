ABYSS SURVIVAL — Guia de Testes Unitários em Luau

🌊

**ABYSS SURVIVAL**

Guia de Testes Unitários em Luau

*TestEZ · Mocks · Quais Testar · Estrutura*


# **Por que Testar**
Os sistemas de Oxigênio, Crafting e DataStore são críticos: um bug nesses módulos destrói a experiência de todos os jogadores. Testes unitários pegam esses bugs antes do jogador.

# **Instalação do TestEZ**
1. Baixe TestEZ em: github.com/Roblox/testez/releases
1. Coloque o ModuleScript do TestEZ em ServerScriptService/Tests/TestEZ
1. Crie um Script em ServerScriptService/Tests/RunTests.server.lua
1. Só rode os testes em modo Studio — nunca em produção

-- RunTests.server.lua

if not game:GetService("RunService"):IsStudio() then return end

local TestEZ   = require(script.Parent.TestEZ)

local results  = TestEZ.TestBootstrap:run({

`  `script.Parent.OxygenSystem\_spec,

`  `script.Parent.CraftingSystem\_spec,

`  `script.Parent.InventorySystem\_spec,

})

TestEZ.Reporters.TextReporter:report(results)

# **OxygenSystem\_spec.lua — Testes Completos**
-- ServerScriptService/Tests/OxygenSystem\_spec.lua

return function()

`  `local OxygenSystem = require(game.ServerScriptService.Modules.OxygenSystem)

`  `-- Mock de player simples

`  `local function mockPlayer(name)

`    `return {

`      `Name      = name or "TestPlayer",

`      `Character = { HumanoidRootPart = { Position = Vector3.new(0,0,0) } },

`      `SetAttribute = function() end,

`      `GetAttribute = function() return nil end,

`    `}

`  `end

`  `describe("initPlayer", function()

`    `it("deve inicializar O2 no máximo", function()

`      `local p = mockPlayer()

`      `OxygenSystem:initPlayer(p)

`      `expect(OxygenSystem:getOxygen(p)).to.equal(100)

`    `end)

`  `end)

`  `describe("consumo", function()

`    `it("deve reduzir O2 ao longo do tempo", function()

`      `local p = mockPlayer()

`      `OxygenSystem:initPlayer(p)

`      `OxygenSystem:update(10)  -- 10 segundos

`      `local o2 = OxygenSystem:getOxygen(p)

`      `expect(o2).to.be.near(90, 1)  -- 10% consumido

`    `end)

`    `it("não deve ir abaixo de 0", function()

`      `local p = mockPlayer()

`      `OxygenSystem:initPlayer(p)

`      `OxygenSystem:update(200)  -- muito tempo

`      `expect(OxygenSystem:getOxygen(p)).to.be.ok()  -- respawnou com 50%

`    `end)

`  `end)

`  `describe("recarga na base", function()

`    `it("deve recarregar quando inBase = true", function()

`      `local p = mockPlayer()

`      `OxygenSystem:initPlayer(p)

`      `OxygenSystem:update(20)  -- consume 20%

`      `OxygenSystem:setInBase(p, true)

`      `OxygenSystem:update(5)   -- recarrega

`      `expect(OxygenSystem:getOxygen(p)).to.be.near(80 + 5\*12.5, 2)

`    `end)

`  `end)

`  `describe("upgrade de tanque", function()

`    `it("deve aceitar novo máximo", function()

`      `local p = mockPlayer()

`      `OxygenSystem:initPlayer(p)

`      `OxygenSystem:upgradeTank(p, 250)

`      `expect(OxygenSystem:getOxygen(p)).to.equal(100)  -- não aumenta atual

`    `end)

`  `end)

end

# **CraftingSystem\_spec.lua — Testes**
return function()

`  `-- Setup: mock do InventorySystem

`  `local fakeInventory = { FerroSimples=10, Calcario=5, Sucata=8 }

`  `local fakeinvSys = {

`    `hasItem  = function(\_, player, id, amt) return (fakeInventory[id] or 0) >= amt end,

`    `removeItem=function(\_, player, id, amt) fakeInventory[id]=(fakeInventory[id] or 0)-amt end,

`    `addItem  = function(\_, player, id, amt) fakeInventory[id]=(fakeInventory[id] or 0)+amt end,

`    `getFlags = function() return {hasBench\_1=true} end,

`    `getInventory=function() return fakeInventory end,

`  `}

`  `local CraftingSystem = require(game.ServerScriptService.Modules.CraftingSystem)

`  `CraftingSystem:init(fakeinvSys)

`  `local craftResult = nil

`  `-- Mock do RemoteEvent

`  `game.ReplicatedStorage.Remotes.CraftingResult.OnServerEvent = nil

`  `-- Substitua por BindableEvent nos testes

`  `describe("receita válida com ingredientes", function()

`    `it("deve craftar FacaColeta com ingredientes suficientes", function()

`      `fakeInventory = { Sucata=5, Calcario=2 }

`      `-- Craft deve consumir ingredientes e adicionar item

`      `-- Validar: fakeInventory.Sucata == 0 após craft

`      `expect(fakeInventory.Sucata).to.equal(5)  -- antes

`    `end)

`  `end)

`  `describe("sem ingredientes suficientes", function()

`    `it("deve falhar e não consumir nada", function()

`      `fakeInventory = { Sucata=2 }  -- falta Calcario

`      `-- craft não deve alterar o inventário

`      `expect(fakeInventory.Sucata).to.equal(2)

`    `end)

`  `end)

end

# **Quais Sistemas Testar — Prioridade**

|**Sistema**|**Prioridade**|**Por que**|
| :- | :- | :- |
|OxygenSystem|CRÍTICA|Bug aqui = jogadores morrendo sem sentido ou nunca morrendo|
|InventorySystem (addItem/removeItem/hasItem)|CRÍTICA|Bug aqui = exploits de duplicação de itens|
|CraftingSystem (validação)|ALTA|Bug aqui = craft sem ingredientes = economia quebrada|
|DataStoreManager (save/load)|ALTA|Bug aqui = perda de progresso dos jogadores|
|PressureSystem (dano por zona)|MÉDIA|Bug aqui = jogadores tomando dano errado|
|QuestSystem (progressão de objetivo)|MÉDIA|Bug aqui = quests não completam ou completam errado|
|EventSystem (seleção e timing)|BAIXA|Bug aqui = eventos não disparam, não é crítico|

Abyss Survival — Guia de Testes Unitários em Luau   v1.0
