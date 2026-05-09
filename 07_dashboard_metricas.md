ABYSS SURVIVAL  —  Dashboard de Métricas Pós-Launch  |  Roblox Studio

🌊

**ABYSS SURVIVAL**

Dashboard de Métricas Pós-Launch

*Analytics · Thresholds · Plano de Ação por Cenário*


# **Métricas Fundamentais**
O Roblox Analytics fornece um conjunto de métricas nativas. Você também deve implementar Custom Events para métricas específicas do Abyss Survival.

# **Métricas Nativas do Roblox Analytics**

|**Métrica**|**Definição**|**Meta 1 mês**|**Meta 3 meses**|**Alerta vermelho se**|
| :- | :- | :- | :- | :- |
|DAU (Daily Active Users)|Usuários únicos por dia|200+|1\.000+|< 50 após semana 2|
|MAU (Monthly Active Users)|Usuários únicos no mês|2\.000+|10\.000+|< 500 após mês 1|
|D1 Retention|% que volta no dia seguinte|30%+|40%+|< 20%|
|D7 Retention|% que volta 7 dias depois|15%+|22%+|< 10%|
|D30 Retention|% que volta 30 dias depois|8%+|12%+|< 5%|
|Average Session Duration|Tempo médio de sessão|20 min+|30 min+|< 12 min|
|Sessions per DAU|Sessões por usuário ativo|1\.5+|2\.0+|< 1.1|
|Revenue (Robux)|Robux ganhos por dia|Variável|Variável|Verificar se Game Pass funciona|
|Payer Conversion|% de jogadores que compraram|3%+|5%+|< 1%|
|ARPPU|Receita média por pagador|150 R$+|250 R$+|< 80 R$|

# **Custom Events para Implementar**
Adicione estas chamadas no código do jogo para rastrear métricas específicas:

-- Usar AnalyticsService do Roblox

local Analytics = game:GetService("AnalyticsService")

-- Profundidade máxima ao sair

game.Players.PlayerRemoving:Connect(function(player)

`  `Analytics:LogCustomEvent(player, "MaxDepth", maxDepthThisSession)

`  `Analytics:LogCustomEvent(player, "TierReached", currentTier)

`  `Analytics:LogCustomEvent(player, "SessionResources", resourcesCollected)

end)

-- Tutorial concluído

Analytics:LogCustomEvent(player, "TutorialComplete", 1)

-- Primeira morte (e causa)

Analytics:LogCustomEvent(player, "FirstDeath", {cause=deathCause, time=timeSinceJoin})

-- Zona desbloqueada

Analytics:LogCustomEvent(player, "ZoneUnlocked", zoneNumber)

-- Quest concluída

Analytics:LogCustomEvent(player, "QuestCompleted", questId)

-- Criatura derrotada

Analytics:LogCustomEvent(player, "CreatureKilled", creatureType)

# **Plano de Ação por Cenário — Semana 1**

|**Cenário**|**Sintoma**|**Causa provável**|**Ação imediata**|
| :- | :- | :- | :- |
|D1 Retention < 20%|Jogadores não voltam no dia seguinte|Onboarding ruim ou primeira sessão chata|Analisar onde jogadores saem. Rever tutorial e primeiros 10 min|
|Session Duration < 10 min|Jogadores saem rápido|Muito difícil, muito fácil ou confuso|Verificar mortes precoces no analytics. Ajustar balanceamento|
|MaxDepth médio < 60 studs|Jogadores não saem da Z1|Progressão bloqueada ou recursos escassos|Verificar drop rates e custo de crafting Tier 0|
|TutorialComplete < 50%|Metade não conclui o tutorial|Tutorial muito longo ou confuso|Encurtar tutorial. Tornar objetivos mais óbvios|
|Payer Conversion < 1%|Quase ninguém compra|Game Pass não aparente ou inútil|Verificar se Game Passes estão visíveis no menu. Rever proposta de valor|
|Server crashes frequentes|Jogadores reportam bugs|Erro de script ou memory leak|Prioridade máxima: ativar output do Developer Console, identificar erro|

# **Calendário de Decisões — 4 Primeiras Semanas**

|**Semana**|**O que analisar**|**Decisão a tomar**|**Threshold**|
| :- | :- | :- | :- |
|Semana 1 (dias 1–7)|D1 Retention + Session Duration + crashes|Patch de equilíbrio se necessário. Hotfix de bugs críticos.|D1 < 20% = ajuste urgente|
|Semana 2 (dias 8–14)|D7 Retention + MaxDepth médio + ZoneUnlocked|Verificar se jogadores chegam à Z2. Ajustar progressão se necessário.|D7 < 10% = rever loop de sessão|
|Semana 3 (dias 15–21)|DAU trend + Quest completions + Revenue|Confirmar se crescimento orgânico está acontecendo. Avaliar monetização.|DAU caindo = anunciar update|
|Semana 4 (dias 22–30)|D30 Retention preview + Reviews + NPS|Decidir conteúdo do Update 1 com base em feedback real.|D30 < 5% = rever retenção longa|

# **Update 1 — Planejamento (2 semanas pós-launch)**
O primeiro update deve ser anunciado ANTES do launch para criar antecipação. Conteúdo base:

- Bioma 4 (Abyss Profundo) — a maior adição de conteúdo
- 2 novas criaturas: Serpente do Vazio + Cardume de Piranha Abissal
- Novo evento de servidor: Erupção Vulcânica Abissal
- Correções de bug baseadas no feedback da semana 1 e 2
- 1 cosmético novo para dar aos Early Adopters (jogadores da semana 1)

**COMUNICAÇÃO:** Poste preview do Bioma 4 (screenshot) no grupo do Roblox e em qualquer rede social 3 dias antes do update. Crie expectativa. Anuncie a data exata.
Abyss Survival — Dashboard de Métricas Pós-Launch	v1.0
