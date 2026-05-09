ABYSS SURVIVAL  —  Protocolo de Playtest  |  Roblox Studio

🌊

**ABYSS SURVIVAL**

Protocolo de Playtest

*Alpha · Beta · Launch — Roteiro, Formulários e Critérios de Aprovação*


# **Por que Playtest Estruturado**
A maioria dos jogos falha não por bugs, mas por problemas de UX que o desenvolvedor nunca percebe porque já conhece o jogo. Um protocolo estruturado força você a observar jogadores reais sem interferir.

**REGRA:** Nunca explique como jogar durante um playtest. Se o jogador trava, anote. Se você explicar, contamina o resultado.

# **Fase Alpha — Teste de Core Gameplay**
## **Quando realizar**
Semana 8–10 do desenvolvimento. Quando o loop básico (O₂ + coleta + crafting + base) estiver funcional mas sem polimento visual.

## **Objetivo**
Verificar se a mecânica central é divertida por si só. Sem arte bonita, sem música. Só gameplay.

## **Quem convidar**
- 3–5 pessoas que jogam Roblox regularmente mas não conhecem o projeto
- Idade alvo: 12–18 anos se possível — são o público principal
- NÃO convidar amigos próximos que vão ser gentis — você precisa de feedback honesto

## **Roteiro do Facilitador — Alpha**

|**Minuto**|**O que fazer**|**O que NÃO fazer**|
| :- | :- | :- |
|0–1|Diga apenas: "Você acorda dentro de um submarino avariado. Descubra o que fazer." Não diga mais nada.|Explicar controles, mecânicas ou objetivos|
|1–10|Observe em silêncio. Anote cada vez que o jogador trava por mais de 10 segundos.|Sugerir ações ou dar dicas|
|10–15|Ainda em silêncio. Se o jogador morreu: "O que você acha que aconteceu?"|Explicar por que ele morreu|
|15–20|Perguntar: "O que você está tentando fazer agora?" — ouça sem comentar.|Corrigir a estratégia do jogador|
|20+|Sessão livre. Observe onde o jogador vai naturalmente.|Interferir|
|Pós-sessão|Fazer as perguntas da lista abaixo. Anotar TUDO.|Defender suas escolhas de design|

## **Perguntas Pós-Sessão — Alpha**
- O que você estava tentando fazer quando travou em [momento X]?
- O que você achou mais confuso?
- Teve algum momento em que você quis parar de jogar? O que causou isso?
- Teve algum momento em que você ficou animado? O que causou isso?
- O que você acha que vai acontecer se continuar jogando?
- O que deveria aparecer na tela que não apareceu?

## **Critérios de Aprovação — Alpha**

|**Critério**|**Meta**|**Se falhar — ação**|
| :- | :- | :- |
|Jogador sai do sub sem instrução|90% dos testadores|Tutorial implícito mais claro (porta mais visível, luz de saída)|
|Jogador coleta algo nos primeiros 3 min|90%|Recursos do spawn estão escondidos — reposicionar|
|Jogador entende que O₂ cai|80%|Barra de O₂ não está clara — redesenhar HUD|
|Jogador não morre nos primeiros 5 min|70%|Início muito difícil — reduzir consumo de O₂ inicial ou adicionar estação próxima|
|Jogador quer continuar após 15 min|60%|Loop principal não está engajante — rever ritmo do gameplay|

# **Fase Beta — Teste de Conteúdo e Balanceamento**
## **Quando realizar**
Semana 12–13. Jogo com arte, música e pelo menos os Biomas 1 e 2 completos.

## **Quem convidar**
- 20–50 jogadores via grupo do Roblox ou Discord da comunidade
- Incluir mistura de casuais (1–2h/semana de jogos) e hardcore (10h+/semana)

## **Métricas para Coletar via Analytics do Roblox**

|**Métrica**|**Como coletar**|**Meta Beta**|**Alerta se**|
| :- | :- | :- | :- |
|Tempo até primeira morte|Custom event: logDeathTime(tick()-joinTime)|> 8 min|< 5 min (muito difícil)|
|Taxa de conclusão do tutorial|Custom event: tutorialComplete()|> 75%|< 60%|
|Profundidade máxima média|LogMaxDepth ao sair|> 80 studs em sessão 1|< 40 studs|
|Tempo médio de sessão|Analytics nativo|> 15 min|< 10 min|
|Taxa de retorno no dia seguinte|Analytics nativo (D1 retention)|> 25%|< 20%|
|Quests completadas por sessão|Custom event por quest|> 1 quest/sessão|0 quests|

## **Formulário de Feedback Beta (enviar por Google Forms)**
- Nota geral do jogo (1–10)
- O que você mais gostou? (resposta aberta)
- O que te impediu de continuar jogando? (resposta aberta)
- Você voltaria a jogar amanhã? (Sim / Talvez / Não)
- O jogo foi muito fácil / na medida certa / muito difícil? (escala)
- Você entendeu o sistema de crafting? (Sim / Parcialmente / Não)
- Você recomendaria para um amigo? (NPS 1–10)

## **Critérios de Aprovação — Beta**

|**Critério**|**Meta**|**Se falhar — ação**|
| :- | :- | :- |
|D1 Retention|> 25%|Rever onboarding e primeiro loop de sessão|
|Tempo médio de sessão|> 15 min|Loop de gameplay não está retendo — rever progressão|
|Avaliação média|> 7/10|Identificar problema mais citado no formulário|
|NPS|> 6/10|Atenção: problemas graves de UX ou bugs bloqueantes|
|Taxa de tutorial completo|> 75%|Tutorial muito longo ou confuso|
|Zero crashes reportados|100%|Investigar e corrigir antes do launch|

# **Fase Launch — Checklist Final de QA**
## **1–2 dias antes do launch**
- [ ] Testar fluxo completo do zero em servidor vazio: spawn → coletar → craftar → base → Z2
- [ ] Testar com 10 contas simultâneas: verificar servidor estável, sem lag
- [ ] Testar Mobile: todas as ações realizáveis com touch
- [ ] Testar morte e respawn: recursos corretos perdidos, respawn na base
- [ ] Testar todos os eventos de servidor: nenhum quebra o jogo
- [ ] Verificar DataStore: sair e entrar recupera exatamente o estado anterior
- [ ] Verificar monetização: Game Pass e Developer Products funcionam
- [ ] Sem exploit conhecido: tentativa de duplicar item falha
- [ ] Tutorial completo: dicas aparecem no momento certo
Abyss Survival — Protocolo de Playtest	v1.0
