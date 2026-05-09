ABYSS SURVIVAL  —  Plano de Moderação e Segurança  |  Roblox Studio

🌊

**ABYSS SURVIVAL**

Plano de Moderação e Segurança

*Exploits · Griefers · Chat · Políticas · Processo de Ban*


# **Tipos de Comportamento Problemático**

|**Tipo**|**Exemplo**|**Severidade**|**Ação**|
| :- | :- | :- | :- |
|Exploit de duplicação|Duplicar itens via bug ou script externo|Alta|Ban permanente do servidor + report ao Roblox|
|Griefing de base|Destruir módulos de base de outros jogadores (se possível)|Alta|Remover permissão de interação com bases alheias no código|
|Spam de chat|Flood de mensagens ou links no chat|Média|Filtro automático do Roblox + mute de 10 min via script|
|Linguagem ofensiva|Palavrões, ataques pessoais|Média|Filtro automático do Roblox (TextService)|
|AFK farming|Bot ou jogador AFK coletando recursos sem jogar|Baixa|AFK kick após 5 min sem input|
|Bug abuse|Usar bugs conhecidos para benefício sem reportar|Média|Aviso + correção do bug. Ban só se intencional e repetido|

# **Proteções Técnicas no Código**
## **Anti-exploit implementado no RemoteHandler**
- Rate limiting em todas as ações críticas (ver Arquitetura de Servidor)
- Validação de distância: jogador deve estar próximo do objeto para interagir
- Validação server-side de inventário: cliente nunca define quantidades
- CFrame validation: posições de módulos de base verificadas pelo servidor

## **AFK Kick**
-- ServerScriptService > AFKKick.server.lua

local TIMEOUT = 300  -- 5 minutos sem input

local lastInput = {}

game.Players.PlayerAdded:Connect(function(player)

`  `lastInput[player] = tick()

end)

-- cliente envia heartbeat a cada 30s enquanto tem input

game.ReplicatedStorage.Remotes.PlayerInput.OnServerEvent:Connect(function(p)

`  `lastInput[p] = tick()

end)

while task.wait(30) do

`  `for player, t in pairs(lastInput) do

`    `if tick() - t > TIMEOUT then

`      `player:Kick("Desconectado por inatividade.")

`      `lastInput[player] = nil

`    `end

`  `end

end

## **Filtro de Chat com TextService**
-- Qualquer mensagem exibida no jogo deve passar pelo filtro

local TextService = game:GetService("TextService")

local function filterText(text, fromPlayer, toPlayer)

`  `local success, filtered = pcall(function()

`    `return TextService:FilterStringAsync(text,

`      `fromPlayer.UserId,

`      `Enum.TextFilterContext.PublicChat)

`  `end)

`  `if not success then return "[mensagem filtrada]" end

`  `local ok, result = pcall(function()

`    `return filtered:GetNonChatStringForUserAsync(toPlayer.UserId)

`  `end)

`  `return ok and result or "[mensagem filtrada]"

end

# **Sistema de Report**
O Roblox tem sistema nativo de report. Adicionalmente, implemente:

- Botão de report no menu de pause — abre formulário simples
- Report envia UserId do suspeito + timestamp + ação suspeita para um DataStore de logs
- Você revisa o DataStore semanalmente. 3+ reports do mesmo UserId = investigação

# **Política de Ban — Níveis**

|**Nível**|**Duração**|**Quando aplicar**|**Como implementar**|
| :- | :- | :- | :- |
|Aviso|Nenhum|Primeira infração leve|Mensagem privada no chat do servidor|
|Kick|Sessão atual|Segunda infração ou infração média|player:Kick("Motivo") via script admin|
|Ban temporário|24–72 horas|Exploit confirmado primeira vez|DataStore de bans + verificação no PlayerAdded|
|Ban permanente|Permanente|Exploit grave, reincidente, ou bot|DataStore de bans permanentes + report ao Roblox|

-- Sistema de ban simples via DataStore

local BanStore = game:GetService("DataStoreService"):GetDataStore("Bans")

game.Players.PlayerAdded:Connect(function(player)

`  `local ok, banData = pcall(function()

`    `return BanStore:GetAsync(tostring(player.UserId))

`  `end)

`  `if ok and banData then

`    `if banData.permanent or banData.until > os.time() then

`      `player:Kick("Você está banido. Motivo: " .. (banData.reason or "violação de regras"))

`    `end

`  `end

end)

-- Para banir um jogador (via script admin ou console):

-- BanStore:SetAsync(tostring(userId), {permanent=true, reason="exploit", by=adminId})

# **Configurações de Segurança do Jogo**
- Filtering Enabled: SEMPRE ativo. Nunca desativar.
- Allow Third Party Sales: desativar se não usar marketplace externo
- Genre: marcar como Adventure para classificação etária correta
- Maximum Players: 12 (definido e testado)
- Server Fill: Roblox Standard (não Empty — evita servidores com 1 jogador)
- Friend Joins Only: desativado (público) — mas considere Private Servers pagos
Abyss Survival — Plano de Moderação e Segurança	v1.0
