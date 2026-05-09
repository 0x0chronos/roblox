ABYSS SURVIVAL  —  MVP Game Design Document    |    Confidencial

🌊

**ABYSS SURVIVAL**

Sobrevivência no Fundo do Oceano

MVP Game Design Document  •  Roblox

|**Versão**|1\.0 — MVP|
| :- | :- |
|**Gênero**|Sobrevivência / Exploração / Crafting|
|**Plataforma**|Roblox Studio (Lua/Luau)|
|**Público-alvo**|10–20 anos, fãs de survival/exploração|
|**Players/serv.**|8–12 jogadores por servidor|


# **1. Visão Geral e Conceito**
## **1.1 Elevator Pitch**
*Abyss Survival é um jogo de sobrevivência e exploração no fundo do oceano para Roblox. Os jogadores acordam dentro de um submarino avariado a centenas de metros de profundidade e precisam sobreviver, construir uma base subaquática, coletar recursos, pesquisar tecnologia e desvendar os mistérios das profundezas — enquanto gerenciam oxigênio, pressão, fome e as criaturas das trevas ao redor.*

## **1.2 Por que este jogo vai ser popular no Roblox**
O Roblox carece de jogos de sobrevivência subaquática com profundidade real. Os principais motivos de sucesso do Abyss Survival:

- Visual único e imersivo: o ambiente subaquático é raro no Roblox e imediatamente chama atenção nas thumbnails
- Loop de gameplay viciante: coletar → craftar → explorar → sobreviver → evoluir → repetir
- Tensão constante: oxigênio acabando, criaturas se aproximando, pressão aumentando — o jogador nunca para
- Progressão visível: base que cresce, equipamento que melhora, biomas que se abrem
- Social e competitivo: cooperação forçada + ranking de profundidade + eventos de servidor
- Alta rejogabilidade: biomas gerados com variação, eventos aleatórios, temporadas com novidades

## **1.3 Referências de Inspiração**

|**Jogo / Referência**|**O que adaptar para o Roblox**|
| :- | :- |
|Subnautica|Sistema de biomas, pressão por profundidade, base subaquática, criaturas únicas por zona|
|Minecraft (survival)|Loop de crafting acessível, progressão de ferramentas, mineração de recursos|
|Raft (Roblox)|Sobrevivência cooperativa, pressão de recursos, ameaça constante|
|Deepwoken (Roblox)|Atmosfera, tensão, progressão de personagem com risco de perda|
|Hungry Shark / Feed and Grow|Criaturas marinhas com comportamento agressivo e hierarquia de tamanho|


# **2. Core Loop e Game Feel**
## **2.1 Loop Principal (sessão de 20–40 min)**
O jogador nunca fica parado. Cada ação leva à próxima naturalmente:

|**Fase**|**Ação**|**Recompensa**|**Tensão**|
| :- | :- | :- | :- |
|1|Explorar bioma próximo|Recursos básicos (minerais, algas, sucata)|Oxigênio caindo, peixe hostil próximo|
|2|Voltar à base e craftar|Novo equipamento, expansão da base|Pressão de tempo, recursos limitados|
|3|Explorar bioma mais fundo|Recursos raros, blueprints, lore||
|4|Enfrentar criatura / Evento|XP, item especial, desbloqueio de área||
|5|Evoluir base / equipamento|Acesso a bioma ainda mais profundo|Novos perigos proporcionais|

## **2.2 Sessão Ideal — Timeline**
1. 0–2 min: Tutorial rápido — jogador acorda no sub avariado, aprende controles básicos, sai para coletar pela primeira vez
1. 2–8 min: Coleta inicial no Bioma 1 (Zona Costeira), monta a estrutura base mínima, crafta tanque de oxigênio básico
1. 8–15 min: Expande a base, descobre entrada para Bioma 2 (Recife Profundo), se depara com primeira criatura agressiva
1. 15–25 min: Cria equipamento anti-pressão, explora Bioma 2, coleta materiais para pesquisa, encontra fragmento de lore
1. 25–40 min: Evento de servidor (tempestade subaquática, swarm de criaturas, ou naufrágio), cooperação com outros players, recompensa de evento

## **2.3 Pilares do Game Feel**
**IMERSÃO:** Partículas de bolhas, luz volumétrica, sons de pressão, música ambiente tensa e bela. O jogador deve sentir que está debaixo d'água.

**TENSÃO:** Barra de oxigênio sempre visível. Criaturas que patrulham. Pressão que aumenta com a profundidade. O jogador nunca se sente completamente seguro.

**ALÍVIO:** Base = santuário. Ao entrar na base, a música muda, as ameaças param. É o "respiro" que torna a tensão suportável.

**PROGRESSÃO:** Cada sessão o jogador é visivelmente mais poderoso do que era. Novas áreas desbloqueadas, equipamento melhor, base maior.


# **3. Mecânicas Principais do MVP**
## **3.1 Sistema de Oxigênio**
Mecânica central e mais importante do jogo. Sempre presente, cria urgência constante.

|**Elemento**|**Detalhe**|
| :- | :- |
|Barra de O₂|0–100%, sempre visível no HUD. Abaixo de 20% a tela fica azulada e o som fica distorcido|
|Consumo base|1% por segundo (100 seg = tanque cheio). Atividades físicas consomem mais|
|Tanque Básico (início)|100 segundos de autonomia|
|Tanque Médio (craftável)|250 segundos de autonomia|
|Tanque Avançado (tier 3)|600 segundos + recarga mais rápida|
|Recarga|Dentro da base: recarga automática. Fora: estações de oxigênio espalhadas nos biomas (30 seg para recarregar completamente)|
|Morte por asfixia|Ao chegar a 0%: tela escurece, jogador reaparece na base com 50% dos recursos da sessão perdidos|

## **3.2 Sistema de Pressão**
Aumenta com a profundidade. Adiciona camada estratégica: você precisa de equipamento melhor para ir mais fundo.

|**Zona**|**Profundidade**|**Pressão**|**Equipamento necessário**|
| :- | :- | :- | :- |
|Zona 1 – Costeira|0–50m|Nenhuma|Roupa padrão|
|Zona 2 – Recife Profundo|50–200m|Leve (-5 HP/s sem proteção)|Roupa de pressão Tier 1|
|Zona 3 – Abyss Raso|200–600m|Moderada (-15 HP/s sem prot.)|Traje reforçado Tier 2|
|Zona 4 – Abyss Profundo|600–1500m|Severa (-30 HP/s sem prot.)|Traje de Titânio Tier 3|
|Zona 5 – Hadal (endgame)|1500m+|Extrema (morte rápida)|Traje Abissal + módulo especial|

## **3.3 Sistema de Crafting**
Simples de aprender, difícil de dominar. Todos os itens do jogo são craftados — nada cai pronto.

### **Categorias de Crafting**
- Mesa de Trabalho (nível 1): ferramentas simples, componentes, estruturas básicas da base
- Bancada de Engenharia (nível 2): equipamentos de pressão, geradores, veículos pequenos
- Laboratório Abissal (nível 3): tecnologia avançada, trajes endgame, itens únicos

### **Recursos do MVP (camadas de raridade)**

|**Raridade**|**Exemplos**|**Onde encontrar**|**Uso principal**|
| :- | :- | :- | :- |
|Comum|Algas, Sucata, Calcário|Zona 1 e 2, superfície||
|Incomum|Cristal Marinho, Ferro Abissal|Zona 2 e 3||
|Raro|Titânio das Profundezas, Gel Bioluminescente|Zona 3 e 4||
|Épico|Núcleo Térmico, Shard Hadal|Zona 4 e 5, boss drops||
|Único|Relíquias do Naufrágio|Eventos e locais secretos||

## **3.4 Sistema de Base Subaquática**
A base é o coração emocional do jogo. Começa mínima e cresce junto com o jogador — é a representação visual do progresso.

### **Módulos da Base (MVP)**
- Casco Central: módulo inicial, inquebrável. Contém cama de respawn e baú inicial
- Módulo de Oxigênio: recarga o tanque do jogador. Upgrade aumenta velocidade de recarga
- Câmara de Pressão: permite guardar trajes e equipamentos de alta pressão com segurança
- Laboratório: habilita craftings avançados. Necessário para pesquisa de tecnologia
- Hangar Submersível: guarda e repara veículos. Desbloqueia no tier 2
- Módulo de Energia: abastece toda a base. Sem energia, luzes apagam e O₂ para de recarregar
- Torre de Sonar: revela o mapa ao redor da base em raio maior. Mostra criaturas próximas

**DICA DE DESIGN:** A base deve ter paredes translúcidas para o jogador ver as criaturas passando do lado de fora. Isso cria tensão mesmo dentro da 'zona segura'.

## **3.5 Sistema de Criaturas**
As criaturas são o maior diferencial do jogo. Cada uma tem comportamento único, não são só inimigos genéricos.

|**Criatura**|**Zona**|**Comportamento**|**Estratégia do jogador**|
| :- | :- | :- | :- |
|Peixe Fantasma|Z1|Passivo, foge da luz|Ignorar ou caçar para carne|
|Tubarão Caçador|Z1–Z2|Agressivo se ver jogador. Patrulha em área fixa|Evitar linha de visão, usar isca|
|Água-Viva Elétrica|Z2|Neutra. Ataca se tocar. AOE elétrico|Nadar devagar ao redor, não tocar|
|Polvo Abissal|Z3|Inteligente: atrai jogadores com bioluminescência como armadilha|Reconhecer o padrão de luz falsa|
|Leviatã das Profundezas|Z4|Boss de zona. Persiste mesmo após dano. Cria corrente que puxa o jogador|Trabalho em equipe obrigatório, explosivos|
|A Coisa (Z5)|Z5|Mini-boss secreto. Forma irregular, ataca a base diretamente|Pesquisa de fraqueza, defesa da base|


# **4. Biomas e Mundo do Jogo**
## **4.1 Estrutura do Mapa**
O mundo é vertical — a progressão é para baixo. Quanto mais fundo, mais perigoso e mais recompensador.

O mapa de cada servidor é gerado com variação procedural nos detalhes (posição de recursos, eventos, pontos de interesse) mantendo a estrutura de zonas fixa. Isso garante rejogabilidade sem confundir novos jogadores.

## **4.2 Os 5 Biomas do MVP**
### **Bioma 1 — Zona Costeira (0–50m)**
- Visual: luz solar penetrando a água, coral colorido, areia clara, muita vida
- Atmosfera: bonita, quase tranquila. O jogo 'te engana' com uma falsa segurança
- Recursos: Algas Nutritivas, Calcário, Sucata de Naufrágio, Ferro Simples
- Criaturas: Peixe Fantasma, Tubarão Caçador (patrulha borda)
- Pontos de interesse: Submarino Avariado (spawn), Naufrágio Raso (loot inicial), Caverna de Coral

### **Bioma 2 — Recife Profundo (50–200m)**
- Visual: luz azulada fraca, corais bioluminescentes, rochas escuras, visibilidade reduzida
- Atmosfera: bela mas inquietante. Criaturas maiores passam ao fundo
- Recursos: Cristal Marinho, Ferro Abissal, Esporo Bioluminescente, Algas Raras
- Criaturas: Água-Viva Elétrica, Enguia Gigante, Caranguejo Colono
- Pontos de interesse: Estação de Pesquisa Abandonada (lore), Formação de Cristal, Entrada para Bioma 3

### **Bioma 3 — Abyss Raso (200–600m)**
- Visual: quase sem luz solar. Bioluminescência é a única iluminação. Pressão visível nos efeitos de tela
- Atmosfera: opressiva, sombria. Sons de pressão no submarino. Sensação de solidão
- Recursos: Titânio das Profundezas, Gel Bioluminescente, Núcleo Térmico Menor
- Criaturas: Polvo Abissal, Peixe Lanterna Gigante, Anêmona Devoradora
- Pontos de interesse: Chaminé Hydrotérmica (fonte de energia), Ruínas Submarinas Misteriosas, Laboratório Perdido

### **Bioma 4 — Abyss Profundo (600–1500m)**
- Visual: escuridão total exceto pela lanterna do jogador e criaturas bioluminescentes. Partículas de neve marinha
- Atmosfera: terror. Silêncio pesado interrompido por sons estranhos. Leviatã visível ao fundo
- Recursos: Núcleo Térmico, Shard Hadal, Minério de Obsidiana Abissal
- Criaturas: Leviatã das Profundezas (boss de zona), Cardume de Piranha Abissal, Serpente do Vazio
- Pontos de interesse: Naufrágio de Navio de Pesquisa (lore principal), Caldeira Térmica (crafting especial)

### **Bioma 5 — Zona Hadal / Endgame (1500m+)**
- Visual: geologia alienígena, cristais negros, luz vermelha vinda de baixo
- Atmosfera: sensação de outro mundo. Música completamente diferente — quase silêncio com tons graves
- Recursos: Materiais Únicos para equipamento endgame e itens de prestígio
- Criaturas: A Coisa, Guardião Hadal, entidades sem nome
- Pontos de interesse: A Fissura (local final do lore), Altar Abissal (crafting de itens únicos)


# **5. Progressão e Retenção de Jogadores**
## **5.1 Progressão do Personagem**
Sem levels numéricos expostos — a progressão é visível pelo equipamento, pela base e pelas áreas desbloqueadas. Isso é mais satisfatório e menos intimidador para novos jogadores.

|**Tier**|**Desbloqueios**|**Tempo estimado**|**Gatilho de progressão**|
| :- | :- | :- | :- |
|Tier 0 (início)|Ferramentas básicas, base mínima, acesso Z1|0–10 min|Tutorial completo|
|Tier 1|Tanque de O₂ médio, traje pressão 1, acesso Z2|10–30 min/sessão|Craftar traje pressão T1|
|Tier 2|Veículo básico (minisub), laboratório, acesso Z3|3–5 sessões|Construir laboratório|
|Tier 3|Traje titânio, drone de exploração, acesso Z4|10–15 sessões|Derrotar leviatã|
|Endgame|Traje abissal, acesso Z5, itens únicos|20+ sessões|Explorar Hadal|

## **5.2 Sistemas de Retenção (o que traz o jogador de volta)**
### **Daily Quests**
3 missões diárias simples com recompensas de recursos raros. Exemplos:

- 'Colete 10 Cristais Marinhos' → 50 Cristais Marinhos bônus
- 'Sobreviva 5 minutos na Zona 3 sem morrer' → Blueprint raro
- 'Construa 3 módulos novos hoje' → Material de crafting Tier 2

### **Ranking de Profundidade**
Placar público mostrando qual jogador (ou grupo) chegou mais fundo naquele servidor / naquela semana. Cria competição saudável e dá status social.

### **Sistema de Codex / Lore**
Conforme o jogador explora, ele descobre fragmentos da história: o que aconteceu com a tripulação do submarino? O que são as ruínas submarinas? Quem construiu o laboratório da Zona 3? Isso cria curiosidade e motiva exploração.

### **Eventos de Servidor (a cada 15 minutos)**

|**Evento**|**Mecânica**|**Recompensa**|
| :- | :- | :- |
|Tempestade Subaquática|Correntes fortes, visibilidade 0, monstros agitados|Materiais raros na superfície após|
|Naufrágio Emergencial|Novo naufrágio aparece no mapa com loot especial|Recursos raros, blueprints|
|Swarm de Criaturas|Ataque em massa à base. Cooperação obrigatória|XP bônus, item de evento|
|Sinal Misterioso|Coordenada revelada. Primeiro a chegar ganha item único|Reliquia única, cosmético|
|Erupção Hidrotermal|Zona de crafting especial temporária na Zona 3|Materiais Tier 3 acessíveis cedo|

## **5.3 Cooperação entre Jogadores**
O jogo pode ser jogado solo, mas é muito mais fácil (e divertido) em grupo. Mecânicas que incentivam cooperação:

- Construção de base colaborativa: módulos grandes requerem 2+ jogadores para ser posicionados
- Leviatã na Zona 4: requer pelo menos 3 jogadores para ser derrotado de forma segura
- Sistema de papéis voluntários: jogador pode se especializar em Engenheiro (base), Explorador (coleta), ou Combatente (proteção)
- Compartilhamento de oxigênio: jogadores podem emprestar oxigênio uns aos outros em emergências


# **6. Monetização (Robux)**
A monetização NUNCA deve criar vantagem competitiva. Tudo que afeta gameplay deve ser ganhável jogando. Robux são apenas para cosméticos e conveniência.

## **6.1 Game Pass (compra única)**

|**Game Pass**|**Preço sugerido**|**Benefício**|
| :- | :- | :- |
|Abyss Explorer|199 R$|Slot extra de base, mochila maior (mais itens carregados), cosmético exclusivo de traje|
|Deep Diver Bundle|399 R$|Veículo cosmético exclusivo (mini-submarino dourado), acesso antecipado a novos biomas em updates|
|Founder's Pack|799 R$|Badge exclusiva, cosmético de traje único, nome destacado no placar de profundidade|

## **6.2 Developer Products (compra repetível)**

|**Produto**|**Preço sugerido**|**Descrição**|
| :- | :- | :- |
|Boost de Oxigênio (x2 por 1h)|25 R$|Consumo de O₂ reduzido 50% por 1 hora. Conveniência, não power|
|Slot de Baú Extra|50 R$|Adiciona 1 baú extra permanente à base no servidor atual|
|Mapa do Tesouro|75 R$|Revela 3 locais de recursos raros no mapa atual|
|Cosmético de Traje (variedade)|50–150 R$|Skins para o traje de mergulho. Sem impacto no gameplay|

**REGRA DE OURO:** Nunca venda O₂ ou HP extras. Nunca venda recursos raros diretamente. Se um jogador free puder atingir o mesmo objetivo jogando, a monetização está correta.


# **7. Interface e HUD**
## **7.1 HUD (Heads-Up Display)**
Minimalista. Só mostra o que importa agora. Sem poluição visual.

|**Elemento**|**Posição na tela**|**Comportamento**|
| :- | :- | :- |
|Barra de Oxigênio|Centro inferior|Azul (OK) → Amarelo (30%) → Vermelho piscando (10%). Som de alarme em 15%|
|HP / Integridade do traje|Esquerda inferior|Só aparece quando abaixo de 80%. Some quando cheio para não poluir|
|Indicador de Profundidade|Superior direito|Metros atuais + zona atual ('Zona 2 — Recife Profundo')|
|Pressão|Superior direito (abaixo)|Barra de pressão com cor. Verde = seguro, vermelho = crítico|
|Sonar mini-map|Superior esquerdo|Círculo de radar. Pontos verdes = recursos, vermelhos = criaturas hostis|
|Barra de ação rápida|Inferior central|6 slots para itens equipados. Similar a hotbar do Minecraft|
|Indicador de Evento|Superior central|Aparece APENAS durante eventos. Conta regressiva + nome do evento|

## **7.2 Menus Principais**
- Menu de Inventário: grid simples, organizado por categoria. Abre com E
- Menu de Crafting: lista com ícones grandes. Mostra o que pode e não pode craftar (e o que falta)
- Menu da Base: visão isométrica da base com módulos clicáveis para upgrade/reparo
- Codex: coleção de criaturas descobertas, fragmentos de lore, blueprints obtidos
- Mapa: abre com M. Mostra zonas desbloqueadas, posição da base, pontos de interesse revelados pelo sonar

## **7.3 Tutorial**
Tutorial contextual — aparece como dicas flutuantes na primeira vez que o jogador encontra cada mecânica. Nunca interrompe o gameplay com longas telas de texto. Exemplos:

- Primeira vez que O₂ chega a 50%: pequena dica 'Seu oxigênio está caindo. Encontre uma estação de recarga ou volte à base.'
- Primeira criatura hostil avistada: 'Cuidado! Essa criatura te ataca se entrar no campo de visão dela.'
- Primeiro recurso coletado: 'Abra o inventário (E) e vá à bancada de crafting para criar itens.'


# **8. Direção de Arte e Áudio**
## **8.1 Identidade Visual**
Paleta de cores que evolui com a profundidade — de bela e colorida para sombria e aterrorizante:

|**Zona**|**Cores dominantes**|**Mood visual**|
| :- | :- | :- |
|Zona 1|Azul turquesa, coral, branco|Tropical, luminoso, convidativo|
|Zona 2|Azul médio, verde-azulado, bioluminescência suave|Belo mas tenso|
|Zona 3|Azul escuro, preto, pontos de luz orgânica|Misterioso, opressor|
|Zona 4|Preto, azul profundo, vermelho distante|Terror, ameaça|
|Zona 5|Preto, vermelho magma, cristal negro|Alienígena, final|

Estilo geral: levemente estilizado (não realista). Proporcional ao estilo do Roblox mas com maior detalhe ambiental. Foco em partículas: bolhas, névoa subaquática, poeira de fundo, neve marinha.

## **8.2 Direção de Áudio**
O áudio é metade da imersão. Deve ser tratado como prioridade igual à arte.

- Música ambiente: instrumental, atmosférico. Zona 1 = calma com notas agudas. Zona 5 = quase silêncio + graves pesados
- Som de respiração: sempre audível quando O₂ < 40%. Acelera conforme cai
- Pressão: som de rangido de metal ao entrar em zonas de alta pressão
- Criaturas: cada criatura tem assinatura sonora única antes de aparecer. O jogador aprende a reconhecer pelo som
- Base: som ambiente de maquinário suave. Contrasta com o silêncio ameaçador lá fora
- Eventos: música específica ao iniciar cada evento. O jogador imediatamente sabe que algo está acontecendo
- Morte: não usar som de 'game over'. Usar som gradual de afundamento e silêncio — mais impactante


# **9. Guia de Implementação no Roblox Studio**
## **9.1 Estrutura de Scripts Recomendada**

|**Script / Module**|**Tipo**|**Responsabilidade**|
| :- | :- | :- |
|OxygenSystem|ModuleScript (Server)|Controla consumo, recarga e morte por asfixia de cada jogador|
|PressureSystem|ModuleScript (Server)|Monitora profundidade do jogador, aplica dano de pressão conforme zona|
|ResourceManager|ModuleScript (Server)|Spawna e controla recursos no mapa, reseta após coleta|
|CraftingSystem|ModuleScript (Server)|Valida receitas, consome recursos do inventário, cria itens|
|CreatureAI|Script (Server)|Comportamento de cada tipo de criatura: patrulha, agressão, fuga|
|BaseManager|ModuleScript (Server)|Controla módulos da base, energia, O₂ recharge na base|
|EventSystem|Script (Server)|Dispara eventos aleatórios a cada 15 min, gerencia duração e recompensas|
|HUDController|LocalScript (Client)|Atualiza HUD em tempo real com dados do servidor via RemoteEvents|
|InventoryClient|LocalScript (Client)|UI de inventário e crafting. Envia pedidos de crafting ao servidor|
|AtmosphereController|LocalScript (Client)|Efeitos visuais por zona: fog, cor da água, partículas, iluminação|
|SoundManager|LocalScript (Client)|Música ambiente, sons de O₂, som de criaturas, efeitos de pressão|
|DataStore|Script (Server)|Salva progressão do jogador: base construída, itens, codex, tier atual|

## **9.2 Ordem de Desenvolvimento Recomendada**
Siga esta ordem para ter sempre uma versão jogável e testável:

1. SEMANA 1–2: Core Survival — Sistema de Oxigênio + HP + Morte + Respawn. Testar com cubo simples representando o mapa. Nada mais importa se isso não for divertido.
1. SEMANA 3–4: Mundo Básico — Construir Bioma 1 completo com assets definitivos. Recursos coletáveis. 3 criaturas com IA básica.
1. SEMANA 5–6: Crafting + Base — Sistema de crafting funcional. Módulos de base posicionáveis. Save/Load de base via DataStore.
1. SEMANA 7–8: Progressão + Pressão — Sistema de pressão por zona. Bioma 2. Tier 1 de equipamento. Daily quests básicas.
1. SEMANA 9–10: Conteúdo + Polimento — Bioma 3. Eventos de servidor. Tutorial contextual. HUD polido. Otimização de performance.
1. SEMANA 11–12: Beta Fechado — Testar com 20–50 jogadores reais. Coletar feedback. Balancear dificuldade, crafting e drop rates.
1. SEMANA 13–14: Launch Preparation — Monetização. Assets de marketing (thumbnail, ícone, descrição). Bioma 4 como conteúdo de lançamento surpresa.

## **9.3 Otimização de Performance**
Roblox tem limitações importantes. Siga estas práticas desde o início:

- Streaming Enabled: ative em todas as partes do jogo. Assets carregam conforme o jogador se aproxima
- LoD (Level of Detail): criaturas distantes usam mesh simplificado. Partículas reduzidas longe do jogador
- Server-side validation: NUNCA confie no cliente para dados de inventário, HP ou posição. Tudo validado no servidor
- Pooling de objetos: criaturas e recursos 'mortos' são desativados e reaproveitados, não deletados e recriados
- RemoteEvents com throttle: HUD não precisa atualizar 60x por segundo. 10x/segundo é suficiente para O₂ e HP
- Limite de partículas: máximo de 3 sistemas de partículas ativos por jogador simultaneamente

## **9.4 Checklist de Launch**
- [ ] Sistema de Oxigênio testado e balanceado
- [ ] Sistema de Pressão por zona funcionando
- [ ] Crafting com todas as receitas do Tier 0 e Tier 1
- [ ] Base com 5+ módulos posicionáveis e upgradeable
- [ ] Biomas 1, 2 e 3 com assets, recursos e criaturas
- [ ] 5+ criaturas com IA distinta
- [ ] 3+ eventos de servidor funcionando
- [ ] Tutorial contextual para todas as mecânicas principais
- [ ] DataStore salvando progresso corretamente
- [ ] HUD completo e legível em mobile
- [ ] Monetização implementada (Game Pass + Developer Products)
- [ ] Thumbnail e ícone profissionais criados
- [ ] Testado com 10+ jogadores simultâneos sem lag
- [ ] Sem exploits de duplicação de itens ou bypass de crafting


# **10. Marketing e Crescimento**
## **10.1 Thumbnail e Ícone**
No Roblox, o thumbnail é a diferença entre alguém clicar ou não no jogo. Invista tempo aqui.

- Thumbnail: Personagem em traje futurista, lanterna acesa, criatura bioluminescente enorme ao fundo, profundidade e escuridão visíveis. Texto: 'ABYSS SURVIVAL' em fonte bold. Deve causar curiosidade e levemente assustar.
- Ícone (quadrado): Close no rosto do personagem com máscara refletindo uma criatura enorme. Fundo escuro azulado.
- Descrição do jogo: Primeira frase deve ser o gancho: '500 metros abaixo da superfície. Oxigênio acabando. Algo se aproxima.'

## **10.2 Crescimento Orgânico**
- YouTubers e streamers de Roblox: entre em contato com criadores de médio porte (100k–500k subs) com acesso antecipado. Custo-benefício muito melhor que grandes criadores
- TikTok: clips de 15–30 segundos mostrando os momentos mais tensos (O₂ quase zero, leviatã aparecendo) têm potencial viral
- Reddit r/roblox: post de 'como eu fiz' com processo de criação gera engajamento genuíno
- Grupo do Roblox: crie grupo do jogo desde o início. Membros do grupo recebem recompensa exclusiva (cosmético). Objetivo: 10k membros antes do launch
- Update frequente: primeiro update em 2 semanas pós-launch (Bioma 4). Anuncia antes do launch para criar antecipação

## **10.3 Métricas de Sucesso do MVP**

|**Métrica**|**Meta (1 mês)**|**Meta (3 meses)**|
| :- | :- | :- |
|Visitas totais|100\.000|1\.000.000|
|Players concorrentes (pico)|200+|1\.000+|
|Tempo médio de sessão|20+ minutos|30+ minutos|
|Taxa de retorno (D1)|30%+|40%+|
|Conversão para Robux|3%+|5%+|
|Avaliação (likes/total)|75%+|80%+|


# **Apêndice — Receitas de Crafting (MVP)**
Lista completa das receitas do Tier 0 e Tier 1 para guiar o desenvolvimento inicial:

## **Tier 0 — Mesa de Trabalho Básica**

|**Item**|**Ingredientes**|**Uso**|
| :- | :- | :- |
|Faca de Coleta|5x Sucata + 2x Calcário|Coleta recursos 2x mais rápido|
|Lanterna Básica|3x Sucata + 1x Esporo Bioluminescente|Ilumina 15m à frente do jogador|
|Baú de Madeira|8x Algas Prensadas + 4x Calcário|Armazenamento de 16 slots na base|
|Kit Médico Simples|3x Algas Nutritivas + 1x Gel Básico|Restaura 40 HP imediatamente|
|Módulo de O₂ (base)|10x Sucata + 5x Calcário + 2x Ferro Simples|Recarrega O₂ dentro da base|
|Tanque de O₂ Médio|5x Ferro Simples + 3x Calcário + 2x Sucata|250 segundos de autonomia|

## **Tier 1 — Mesa de Trabalho + Bancada de Engenharia**

|**Item**|**Ingredientes**|**Uso**|
| :- | :- | :- |
|Traje de Pressão T1|8x Ferro Simples + 4x Calcário + 3x Algas Prensadas|Protege completamente na Zona 2|
|Propulsor Aquático|6x Sucata + 3x Ferro Simples + 2x Cristal Marinho|Nada 2x mais rápido|
|Gerador Solar (base)|10x Ferro Simples + 5x Cristal Marinho|Energia básica para a base na Zona 1–2|
|Sonar Portátil|4x Ferro Simples + 2x Cristal Marinho + 1x Sucata Eletrônica|Revela criaturas e recursos em 30m|
|Arpão Básico|5x Ferro Simples + 2x Calcário|Arma de combate à distância. 3 usos antes de recarregar|
|Módulo Laboratório (base)|15x Ferro Simples + 5x Cristal Marinho + 3x Ferro Abissal|Habilita crafting Tier 2|


**ABYSS SURVIVAL — MVP Game Design Document**

*Este documento é um guia vivo. Ajuste conforme o feedback dos jogadores.*
Roblox Game Design — Abyss Survival	Página 
