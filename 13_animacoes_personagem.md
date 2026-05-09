ABYSS SURVIVAL — Guia de Animações do Personagem

🌊

**ABYSS SURVIVAL**

Guia de Animações do Personagem

*Lista · IDs da Toolbox · AnimationController · Blending*


# **Animações Necessárias — Lista Completa**
Todas as animações do personagem jogável. Algumas podem ser encontradas gratuitamente na Toolbox do Roblox; outras precisam ser criadas no Moon Animator.

|**ID de Animação**|**Quando toca**|**Loop?**|**Prioridade**|**Fonte sugerida**|
| :- | :- | :- | :- | :- |
|Idle\_Underwater|Parado debaixo d'água. Leve flutuação vertical|Sim|Core|Toolbox: "underwater idle float"|
|Swim\_Normal|Nadando em velocidade normal|Sim|Movement|Toolbox: "swimming animation roblox"|
|Swim\_Sprint|Nadando com propulsor ativado (mais dinâmico)|Sim|Movement|Criar no Moon Animator — baseado em Swim\_Normal + inclinação para frente|
|Collect|Braço estendido pegando objeto. 0.5s|Não|Action|Toolbox: "pickup animation" adaptado|
|Craft|Mãos trabalhando na bancada. 2–3s|Não|Action|Criar no Moon Animator — movimento de mãos|
|Place\_Module|Erguendo e posicionando módulo pesado. 1.5s|Não|Action|Criar no Moon Animator|
|Use\_Item|Usando consumível (kit médico, etc). 1s|Não|Action|Toolbox: "use item animation"|
|Fire\_Harpoon|Saque + disparo do arpão. 0.8s|Não|Action|Toolbox: "aim and shoot" adaptado|
|Take\_Damage|Recuo ao levar dano. 0.3s|Não|Action|Toolbox: "flinch hit reaction"|
|Pressure\_Pain|Personagem se contorce com dor de pressão. 0.5s|Não|Action|Criar no Moon Animator|
|Alert\_SOS|Braços agitando pedindo socorro (O₂ < 10%)|Sim|Action|Criar no Moon Animator — simples|
|Death\_Drown|Personagem "afunda" lentamente. 3s|Não|Action|Criar no Moon Animator|
|Idle\_InBase|Idle dentro da base — mais relaxado, sem flutuação|Sim|Core|Toolbox: "idle standing" adaptado|
|Enter\_Minisub|Entrando no veículo. 1s|Não|Action|Toolbox: "vehicle enter"|
|Drive\_Minisub|Mãos no controle dentro do sub. Loop|Sim|Core|Criar no Moon Animator|

# **AnimationController — Implementação**
Use um LocalScript para gerenciar transições de animação baseadas no estado do personagem:

-- StarterCharacterScripts/AnimationController (LocalScript)

local Players    = game:GetService("Players")

local RunService = game:GetService("RunService")

local player = Players.LocalPlayer

local char   = player.Character or player.CharacterAdded:Wait()

local hum    = char:WaitForChild("Humanoid")

local hrp    = char:WaitForChild("HumanoidRootPart")

local animCtrl = hum:WaitForChild("Animator")

-- Carrega animações (substitua IDs pelos reais)

local ANIM\_IDS = {

`  `idle\_water  = "rbxassetid://0",

`  `swim\_normal = "rbxassetid://0",

`  `swim\_sprint = "rbxassetid://0",

`  `idle\_base   = "rbxassetid://0",

`  `alert\_sos   = "rbxassetid://0",

}

local tracks = {}

for name, id in pairs(ANIM\_IDS) do

`  `local anim = Instance.new("Animation")

`  `anim.AnimationId = id

`  `tracks[name] = animCtrl:LoadAnimation(anim)

end

local currentAnim = nil

local function playAnim(name)

`  `if currentAnim == name then return end

`  `-- Para animação atual

`  `if currentAnim and tracks[currentAnim] then

`    `tracks[currentAnim]:Stop(0.2)  -- fade out 0.2s

`  `end

`  `currentAnim = name

`  `if tracks[name] then

`    `tracks[name]:Play(0.2)  -- fade in 0.2s

`  `end

end

-- Loop de estado: escolhe animação baseada no contexto

local inBase, o2Critical = false, false

game.ReplicatedStorage.Remotes.UpdateOxygen:Connect(function(data)

`  `o2Critical = data.current / data.max < 0.10

end)

RunService.Heartbeat:Connect(function()

`  `local speed = hrp.Velocity.Magnitude

`  `if o2Critical then

`    `playAnim("alert\_sos")

`  `elseif inBase then

`    `if speed < 1 then playAnim("idle\_base")

`    `else playAnim("swim\_normal") end

`  `else

`    `if speed < 1 then playAnim("idle\_water")

`    `elseif speed > 25 then playAnim("swim\_sprint")

`    `else playAnim("swim\_normal") end

`  `end

end)

# **Moon Animator — Guia Rápido**
1. Instale Moon Animator 2 da Toolbox (plugin gratuito de animação)
1. Selecione o modelo do personagem no workspace
1. Abra Moon Animator: Plugin → Moon Animator 2
1. Clique em "New" → escolha o Rig do personagem
1. Use keyframes para posicionar os ossos (HumanoidRootPart, UpperTorso, etc.)
1. Para flutuação idle: posicione frame 0 e frame 60 iguais, frame 30 com Y +0.3 studs
1. Export → "Export to Roblox" → copie o ID da animação gerada
1. Cole o ID no ANIM\_IDS do AnimationController

**DICA:** Instale também o plugin "Animation Editor" nativo do Roblox (já incluso no Studio). Para animações simples como Collect e Take\_Damage, o Editor nativo é mais rápido que o Moon Animator.
Abyss Survival — Guia de Animações do Personagem   v1.0
