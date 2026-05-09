ABYSS SURVIVAL — Guia Completo de Produção  |  Roblox Studio

🌊

**ABYSS SURVIVAL**

Guia Completo de Produção

*Do zero ao launch — tudo que você precisa para construir o jogo*

|**Módulo**|**Conteúdo**|
| :- | :- |
|01 — Visão e Conceito|Pitch, público-alvo, referências, o que torna o jogo popular|
|02 — Core Loop|Sessão ideal, pilares de game feel, economia de tensão e alívio|
|03 — Mecânicas Core|Oxigênio, pressão, crafting, base, criaturas — valores exatos|
|04 — Mundo e Biomas|5 zonas, dimensões, terreno, assets, pontos de interesse|
|05 — Progressão e Retenção|Tiers, daily quests, eventos, ranking, lore, cooperação|
|06 — Iluminação e Atmosfera|Lighting Service, parâmetros por zona, efeitos de tela|
|07 — Partículas e VFX|Bolhas, neve marinha, efeitos de ação, efeitos de estado|
|08 — Áudio Completo|Música adaptativa, som ambiente, SFX, criaturas, estrutura|
|09 — Interface (HUD/UI)|HUD minimalista, menus, tutorial contextual, mobile|
|10 — Onboarding|Intro, primeiros objetivos, waypoints, tela de resumo|
|11 — Social e Multiplayer|Party, ping, chat de proximidade, cooperação forçada|
|12 — Polimento Visual|Animações de feedback, câmera shake, transições de zona|
|13 — Economia e Balanceamento|Drop rates, curva de dificuldade, anti-grind, custo de morte|
|14 — Lore e Narrativa|Fragmentos, codex, mistério central, backstory|
|15 — Técnico e Segurança|Scripts, anti-exploit, DataStore, mobile, performance|
|16 — Monetização|Game Passes, Developer Products, regras de design|
|17 — Marketing e Launch|Thumbnail, página, grupo, YouTubers, métricas|
|18 — Plano de Execução|14 semanas semana a semana, checklists de launch|


# **01 · Visão e Conceito**
## **Elevator Pitch**
*Abyss Survival é um jogo de sobrevivência e exploração no fundo do oceano para Roblox. Os jogadores acordam dentro de um submarino avariado a centenas de metros de profundidade e precisam sobreviver, construir uma base subaquática, coletar recursos, pesquisar tecnologia e desvendar os mistérios das profundezas — enquanto gerenciam oxigênio, pressão, fome e as criaturas das trevas ao redor.*

## **Por que vai ser popular**
- Visual único: ambiente subaquático é raro no Roblox e chama atenção imediata nas thumbnails
- Loop viciante: coletar → craftar → explorar → sobreviver → evoluir → repetir
- Tensão constante: oxigênio acabando, criaturas se aproximando, pressão aumentando
- Progressão visível: base que cresce, equipamento que melhora, biomas que se abrem
- Social e competitivo: cooperação forçada + ranking de profundidade + eventos de servidor
- Alta rejogabilidade: variação procedural de recursos, eventos aleatórios, temporadas

## **Referências**

|**Referência**|**O que adaptar**|
| :- | :- |
|Subnautica|Biomas, pressão por profundidade, base subaquática, criaturas únicas por zona|
|Minecraft survival|Loop de crafting acessível, progressão de ferramentas, mineração|
|Raft (Roblox)|Sobrevivência cooperativa, pressão de recursos, ameaça constante|
|Deepwoken (Roblox)|Atmosfera, tensão, progressão com risco de perda|
|Feed and Grow|Criaturas com comportamento agressivo e hierarquia de tamanho|

## **Ficha técnica**

|**Parâmetro**|**Valor**|
| :- | :- |
|Gênero|Sobrevivência / Exploração / Crafting|
|Plataforma|Roblox Studio (Luau)|
|Players por servidor|8–12 jogadores|
|Público-alvo|10–20 anos, fãs de survival e exploração|
|Sessão ideal|20–40 minutos|
|Monetização|Cosméticos e conveniência — sem pay-to-win|


# **02 · Core Loop e Game Feel**
## **Loop principal — sessão de 20–40 min**

|**Fase**|**Ação do jogador**|**Recompensa**|**Tensão presente**|
| :- | :- | :- | :- |
|1|Explorar bioma próximo|Recursos básicos (minerais, algas, sucata)|O₂ caindo, peixe hostil próximo|
|2|Voltar à base e craftar|Novo equipamento, expansão da base|Pressão de tempo, recursos limitados|
|3|Explorar bioma mais fundo|Recursos raros, blueprints, fragmentos de lore|Criaturas mais fortes, pressão aumenta|
|4|Enfrentar criatura / Evento|XP, item especial, desbloqueio de área|Vida em risco, O₂ consumido mais rápido|
|5|Evoluir base e equipamento|Acesso a bioma ainda mais profundo|Novos perigos proporcionais ao poder|

## **Timeline de uma sessão ideal**
1. 0–2 min: Tutorial — jogador acorda no sub avariado, aprende controles, sai para coletar pela primeira vez
1. 2–8 min: Coleta inicial na Zona 1, monta estrutura base mínima, crafta tanque de oxigênio básico
1. 8–15 min: Expande a base, descobre entrada para Zona 2, encontra primeira criatura agressiva
1. 15–25 min: Cria equipamento anti-pressão, explora Zona 2, coleta materiais, acha fragmento de lore
1. 25–40 min: Evento de servidor (tempestade, swarm, naufrágio), cooperação com outros jogadores

## **4 Pilares do Game Feel**

**IMERSÃO:** Partículas de bolhas, luz volumétrica, sons de pressão, música ambiente tensa e bela. O jogador deve sentir que está debaixo d'água a cada segundo.

**TENSÃO:** Barra de O₂ sempre visível. Criaturas que patrulham. Pressão que aumenta com profundidade. Nunca completamente seguro.

**ALÍVIO:** Base = santuário. Ao entrar, a música muda, ameaças param. O respiro que torna a tensão suportável e faz o jogador querer sair de novo.

**PROGRESSÃO:** Cada sessão o jogador é visivelmente mais poderoso. Novas áreas, equipamento melhor, base maior. A sensação de crescimento é o gancho principal.


# **03 · Mecânicas Core**
## **Sistema de Oxigênio**
Mecânica central. Sempre presente, cria urgência constante. Tudo o mais depende de estar vivo.

|**Elemento**|**Detalhe**|
| :- | :- |
|Barra de O₂|0–100%, sempre visível no HUD. Abaixo de 20% a tela fica azulada e o som distorce|
|Consumo base|1% por segundo (100 seg = tanque cheio). Atividades físicas consomem 1.5x mais|
|Tanque Básico (início)|100 segundos de autonomia|
|Tanque Médio (Tier 1)|250 segundos|
|Tanque Avançado (Tier 3)|600 segundos + recarga mais rápida|
|Recarga na base|Automática ao entrar. Completa em 8 segundos|
|Estações de O₂ (mundo)|Espalhadas nos biomas. 30 segundos para recarregar completamente|
|Morte por asfixia|A 0%: tela escurece, respawn na base, 40% dos recursos da mochila perdidos|

## **Sistema de Pressão**

|**Zona**|**Profundidade**|**Dano sem proteção**|**Equipamento necessário**|
| :- | :- | :- | :- |
|Z1 – Zona Costeira|0–50m|Nenhum|Roupa padrão|
|Z2 – Recife Profundo|50–200m|−5 HP/s|Traje de Pressão Tier 1|
|Z3 – Abyss Raso|200–600m|−15 HP/s|Traje Reforçado Tier 2|
|Z4 – Abyss Profundo|600–1500m|−30 HP/s|Traje de Titânio Tier 3|
|Z5 – Hadal|1500m+|−60 HP/s (morte rápida)|Traje Abissal + módulo especial|

## **Sistema de Crafting**
Simples de aprender, difícil de dominar. Nada cai pronto — tudo é craftado.

### **Bancadas e tiers**
- Mesa de Trabalho (Tier 0): ferramentas simples, componentes, estruturas básicas
- Bancada de Engenharia (Tier 1): equipamentos de pressão, geradores, veículos
- Laboratório Abissal (Tier 2): tecnologia avançada, trajes endgame, itens únicos

### **Raridade de recursos**

|**Raridade**|**Exemplos**|**Onde encontrar**|**Uso principal**|
| :- | :- | :- | :- |
|Comum|Algas, Sucata, Calcário|Z1–Z2, superfície|Tudo do Tier 0|
|Incomum|Cristal Marinho, Ferro Abissal|Z2–Z3|Tier 1 e equipamentos|
|Raro|Titânio das Profundezas, Gel Bioluminescente|Z3–Z4|Tier 2 e base avançada|
|Épico|Núcleo Térmico, Shard Hadal|Z4–Z5, boss drops|Tier 3 e endgame|
|Único|Relíquias do Naufrágio|Eventos e locais secretos|Itens de prestígio|

## **Receitas de Crafting — Tier 0**

|**Item**|**Ingredientes**|**Uso**|
| :- | :- | :- |
|Faca de Coleta|5× Sucata + 2× Calcário|Coleta recursos 2× mais rápido|
|Lanterna Básica|3× Sucata + 1× Esporo Bioluminescente|Ilumina 15m à frente|
|Baú de Madeira|8× Algas Prensadas + 4× Calcário|16 slots de armazenamento na base|
|Kit Médico Simples|3× Algas Nutritivas + 1× Gel Básico|Restaura 40 HP imediatamente|
|Módulo de O₂ (base)|10× Sucata + 5× Calcário + 2× Ferro Simples|Recarrega O₂ dentro da base|
|Tanque de O₂ Médio|5× Ferro Simples + 3× Calcário + 2× Sucata|250 seg de autonomia|

## **Receitas de Crafting — Tier 1**

|**Item**|**Ingredientes**|**Uso**|
| :- | :- | :- |
|Traje de Pressão T1|8× Ferro Simples + 4× Calcário + 3× Algas Prensadas|Protege completamente na Z2|
|Propulsor Aquático|6× Sucata + 3× Ferro Simples + 2× Cristal Marinho|Nada 2× mais rápido|
|Gerador Solar (base)|10× Ferro Simples + 5× Cristal Marinho|Energia básica Z1–Z2|
|Sonar Portátil|4× Ferro Simples + 2× Cristal Marinho + 1× Sucata Eletrônica|Revela criaturas e recursos em 30m|
|Arpão Básico|5× Ferro Simples + 2× Calcário|Arma à distância. 3 usos antes de recarregar|
|Módulo Laboratório|15× Ferro Simples + 5× Cristal Marinho + 3× Ferro Abissal|Habilita crafting Tier 2|

## **Sistema de Base Subaquática**

|**Módulo**|**Função**|**Tier**|
| :- | :- | :- |
|Casco Central|Módulo inicial inquebrável. Cama de respawn e baú inicial|T0|
|Módulo de O₂|Recarrega tanque do jogador. Upgrade aumenta velocidade|T0|
|Câmara de Pressão|Guarda trajes de alta pressão com segurança|T0|
|Laboratório|Habilita craftings avançados e pesquisa|T1|
|Módulo de Energia|Abastece toda a base. Sem energia: luzes apagam, O₂ para|T1|
|Hangar Submersível|Guarda e repara veículos|T2|
|Torre de Sonar|Revela mapa ao redor. Mostra criaturas em raio maior|T2|

**DESIGN:** Paredes da base devem ser translúcidas — o jogador vê criaturas passando do lado de fora. Cria tensão mesmo dentro da 'zona segura'.

## **Sistema de Criaturas**

|**Criatura**|**Zona**|**Comportamento**|**Estratégia do jogador**|
| :- | :- | :- | :- |
|Peixe Fantasma|Z1|Passivo, foge da luz|Ignorar ou caçar para carne|
|Tubarão Caçador|Z1–Z2|Agressivo se ver jogador. Patrulha em área fixa|Evitar linha de visão, usar isca|
|Água-Viva Elétrica|Z2|Neutra. AOE elétrico se tocar|Nadar devagar ao redor — não tocar|
|Polvo Abissal|Z3|Atrai jogadores com bioluminescência falsa como armadilha|Reconhecer o padrão de luz falsa|
|Leviatã das Profundezas|Z4|Boss de zona. Persiste após dano. Cria corrente|Trabalho em equipe, explosivos|
|A Coisa (Z5)|Z5|Mini-boss secreto. Ataca a base diretamente|Pesquisa de fraqueza, defesa cooperativa|


# **04 · Mundo e Biomas**
## **Estrutura do Mapa**
O mundo é vertical — a progressão é para baixo. Quanto mais fundo, mais perigoso e mais recompensador. Dimensões em studs do Roblox (1 stud = 12,5 cm):

|**Zona**|**Y mínimo**|**Y máximo**|**Profundidade real**|**Tamanho horizontal**|
| :- | :- | :- | :- | :- |
|Z1 – Zona Costeira|Y 0|Y -400|0–50m|1\.200 × 1.200 studs|
|Z2 – Recife Profundo|Y -400|Y -1.600|50–200m|900 × 900 studs|
|Z3 – Abyss Raso|Y -1.600|Y -4.800|200–600m|700 × 700 studs|
|Z4 – Abyss Profundo|Y -4.800|Y -12.000|600–1.500m|500 × 500 studs|
|Z5 – Hadal|Y -12.000|Y -16.000|1\.500m+|300 × 300 studs|

## **Z1 — Zona Costeira (0–50m)**
- Visual: luz solar penetrando, coral colorido, areia clara, muita vida
- Atmosfera: bonita, quase tranquila. O jogo engana com uma falsa segurança
- Recursos: Algas Nutritivas, Calcário, Sucata de Naufrágio, Ferro Simples
- Criaturas: Peixe Fantasma, Tubarão Caçador (patrulha na borda da zona)
- Pontos de interesse: Submarino Avariado (spawn), Naufrágio Raso, Caverna de Coral, Entrada Z2
- Terreno: material Sand + Rock + Limestone. Coral via MeshParts coloridos
- Iluminação: Brightness 2.5, Atmosphere.Density 0.35, cor azul-turquesa

## **Z2 — Recife Profundo (50–200m)**
- Visual: luz azulada fraca, corais bioluminescentes, visibilidade reduzida
- Atmosfera: bela mas inquietante. Criaturas maiores passam ao fundo
- Recursos: Cristal Marinho, Ferro Abissal, Esporo Bioluminescente
- Criaturas: Água-Viva Elétrica, Enguia Gigante, Caranguejo Colono
- Pontos de interesse: Estação de Pesquisa Abandonada (lore), Formação de Cristal, Cavernas
- Terreno: Sand cinza-azulado + Basalt + Ground (lodo). Coral bioluminescente com PointLight
- Iluminação: Brightness 1.2, Density 0.55, Haze 2.5, cor azul médio

## **Z3 — Abyss Raso (200–600m)**
- Visual: quase sem luz solar. Bioluminescência é a única iluminação
- Atmosfera: opressiva, sombria. Sons de pressão. Sensação de solidão
- Recursos: Titânio das Profundezas, Gel Bioluminescente, Núcleo Térmico Menor
- Criaturas: Polvo Abissal, Peixe Lanterna Gigante, Anêmona Devoradora
- Pontos de interesse: Chaminé Hidrotérmica, Ruínas Submarinas Misteriosas, Laboratório Perdido
- Terreno: Mud (lama escura) + Basalt. Parts Neon para fissuras bioluminescentes
- Iluminação: Brightness 0.4, Density 0.72, Haze 3.5, DepthOfField ativo

## **Z4 — Abyss Profundo (600–1500m)**
- Visual: escuridão total exceto lanterna do jogador e bioluminescência das criaturas
- Atmosfera: terror. Silêncio interrompido por sons estranhos. Leviatã visível ao fundo
- Recursos: Núcleo Térmico, Shard Hadal, Minério de Obsidiana Abissal
- Criaturas: Leviatã das Profundezas (boss), Cardume de Piranha Abissal, Serpente do Vazio
- Terreno: Slate + Granite. Assets: pedras negras monumentais, serpentinas de sal
- Iluminação: Brightness 0.05, Density 0.88, Haze 4.5. Lanterna do jogador é essencial

## **Z5 — Hadal / Endgame (1500m+)**
- Visual: geologia alienígena, cristais negros, luz vermelha vinda de baixo
- Atmosfera: outro mundo. Música completamente diferente — quase silêncio com tons graves
- Recursos: materiais únicos para endgame e itens de prestígio
- Criaturas: A Coisa, Guardião Hadal, entidades sem nome
- Pontos de interesse: A Fissura (local final do lore), Altar Abissal
- Terreno: Slate + Basalt mesclados. Magma simulado: Parts Neon laranja + PointLight
- Iluminação: Brightness 0.02, Density 0.95, Haze 5.0. Paleta vermelho-preto

## **Assets por Zona — Guia de Modelagem**

|**Asset**|**Como criar no Studio**|**Detalhes técnicos**|
| :- | :- | :- |
|Coral grande (5 variações)|MeshPart importado (.fbx simples) ou unions de Parts cilíndricas|SurfaceAppearance com emissive leve. CastShadow = false|
|Coral bioluminescente Z2|MeshPart + PointLight filho + script de pulso (Tween)|Pulso a cada 2–4s. Cor azul-esverdeado|
|Algas ondulando|MeshPart plano + script de rotação suave (sin wave no CFrame)|Anchored = true, CanCollide = false|
|Pedras do fundo|Union de esferas achatadas ou MeshPart básico, Material: Rock|Tamanho variado 2–8 studs|
|Naufrágio (spawn Z1)|MeshParts ou unions grandes com Material SmoothPlastic enferrujado|Decals de dano, janelas quebradas, interior navegável|
|Raios de sol (Z1)|Beam entre Attachments com textura de raio de luz|Transparency gradiente 0.2 → 1.0|
|Fissuras bioluminescentes Z3|Unions finas com Material Neon, cor verde/azul|PointLight de baixa intensidade filho|
|Chaminé hidrotérmica Z3|Cilindros de Basalt + ParticleEmitter no topo|2 emitters: fumaça branca + fagulha laranja|
|Cristais negros Z5|Unions de prismas finos altos, SmoothPlastic preto|Geometria alienígena, sem textura adicional|
|Magma Z5|Parts planas Neon laranja + PointLight laranja|ParticleEmitter de fagulhas ascendentes|


# **05 · Progressão e Retenção**
## **Tiers de Progressão**

|**Tier**|**Desbloqueios**|**Tempo estimado**|**Gatilho**|
| :- | :- | :- | :- |
|Tier 0 (início)|Ferramentas básicas, base mínima, acesso Z1|0–10 min|Tutorial completo|
|Tier 1|Tanque O₂ médio, traje pressão, acesso Z2|10–30 min/sessão|Craftar traje pressão T1|
|Tier 2|Minisub, laboratório, acesso Z3|3–5 sessões|Construir laboratório|
|Tier 3|Traje titânio, drone, acesso Z4|10–15 sessões|Derrotar leviatã|
|Endgame|Traje abissal, acesso Z5, itens únicos|20+ sessões|Explorar Hadal|

## **Daily Quests — Exemplos**
- Colete 10 Cristais Marinhos → 50 Cristais Marinhos bônus
- Sobreviva 5 minutos na Zona 3 sem morrer → Blueprint raro
- Construa 3 módulos novos hoje → Material de crafting Tier 2
- Derrote 3 Tubarões Caçadores → Fragmento de lore inédito
- Leve um parceiro à Zona 2 → Cosmético de traje especial

## **Eventos de Servidor (a cada 15 minutos)**

|**Evento**|**Mecânica**|**Recompensa**|
| :- | :- | :- |
|Tempestade Subaquática|Correntes fortes, visibilidade zero, monstros agitados|Materiais raros na superfície após|
|Naufrágio Emergencial|Novo naufrágio aparece com loot especial no mapa|Recursos raros, blueprints exclusivos|
|Swarm de Criaturas|Ataque em massa à base. Cooperação obrigatória|XP bônus, item de evento|
|Sinal Misterioso|Coordenada revelada. Primeiro a chegar ganha item único|Relíquia única, cosmético exclusivo|
|Erupção Hidrotermal|Zona de crafting especial temporária na Z3|Materiais Tier 3 acessíveis antes da hora|

## **Mecânicas de Cooperação**
- Módulos grandes da base requerem 2+ jogadores para posicionar
- Leviatã na Z4 requer ao menos 3 jogadores para derrotar com segurança
- Sistema de papéis voluntários: Engenheiro (base), Explorador (coleta), Combatente
- Compartilhamento de oxigênio: jogadores podem emprestar O₂ uns aos outros
- Animação de pedido de socorro automática quando O₂ < 10%

## **Sistemas de Retenção a Longo Prazo**
- Ranking de profundidade semanal: placar público, reset toda segunda-feira
- Codex de criaturas: incentiva explorar todas as zonas para completar
- Fragmentos de lore: história contada gradualmente, nunca completamente revelada
- Tela de resumo ao sair: profundidade máxima, recursos coletados, criaturas encontradas
- Badge de conquistas: primeira morte, primeira Z3, leviatã derrotado, Z5 alcançada


# **06 · Iluminação e Atmosfera**
## **Configuração Inicial do Lighting Service**
-- Explorer: Lighting > propriedades

GlobalShadows              = true

Brightness                 = 1

EnvironmentSpecularScale   = 0.5

EnvironmentDiffuseScale    = 0.5

ClockTime                  = 14

-- Filhos obrigatórios do Lighting:

• Atmosphere              (neblina subaquática)

• ColorCorrectionEffect   (tint por zona)

• BlurEffect              (O₂ crítico e morte)

• DepthOfFieldEffect      (profundidade Z3+)

## **Parâmetros por Zona — tabela completa**

|**Propriedade**|**Z1**|**Z2**|**Z3**|**Z4**|**Z5**|
| :- | :- | :- | :- | :- | :- |
|Lighting.Brightness|2\.5|1\.2|0\.4|0\.05|0\.02|
|Lighting.ClockTime|14|12|10|8|6|
|Atmosphere.Density|0\.35|0\.55|0\.72|0\.88|0\.95|
|Atmosphere.Haze|1\.5|2\.5|3\.5|4\.5|5\.0|
|Atmosphere.Color (R,G,B)|0,120,200|0,70,140|0,30,80|0,5,30|30,0,10|
|Atmosphere.Decay (R,G,B)|0,60,120|0,20,80|0,5,40|0,0,15|15,0,5|
|Atmosphere.Glare|0\.3|0\.1|0\.0|0\.0|0\.0|
|ColorCorrection.Brightness|0\.0|-0.05|-0.15|-0.3|-0.4|
|ColorCorrection.Contrast|0\.0|0\.05|0\.1|0\.2|0\.25|
|ColorCorrection.Saturation|0\.1|0\.0|-0.1|-0.3|-0.4|
|DepthOfField ativo|Não|Não|Sim|Sim|Sim|
|Lanterna do jogador|Off|Off|On|On|On|

## **Iluminação Local por Zona**
### **Zona 1 — Zona Costeira**
- SurfaceLight em corais: Color (0,200,100), Brightness 2, Range 15
- SpotLight apontando para baixo nos pontos mais fundos: Color (0,100,200)
- Sem PointLights artificiais — iluminação solar é suficiente

### **Zona 2 — Recife Profundo**
- PointLight dentro de cada coral bioluminescente: Color (0,180,255), Brightness 3, Range 20
- PointLight azul fraca espalhada pelo fundo: Color (0,50,150), Brightness 0.8, Range 40

### **Zonas 3–5 — Abyss**
- Z3: PointLight verde nas fissuras Neon: Color (0,255,80), Brightness 5, Range 10
- Z3: SpotLight vermelha nas chaminés: Color (255,60,0), Brightness 4, Range 25
- Z4–Z5: criaturas bioluminescentes têm PointLight de cor única da espécie
- Z5: PointLight laranja no magma: Brightness 8, Range 50

## **Efeitos de Tela por Estado do Jogador**

|**Estado**|**Efeito**|**Transição**|
| :- | :- | :- |
|O₂ 100–30%|Nenhum efeito adicional|—|
|O₂ 29–15%|ColorCorrection.TintColor azulado leve, Saturation -0.1|Tween 2s|
|O₂ 14–5%|Blur.Size = 5, tint azul forte, tela pulsa levemente|Tween 1s|
|O₂ 0–morte|Blur.Size = 20, tudo escurece, Brightness -0.8|Tween 0.5s|
|Dano de pressão|Flash rápido de borda vermelha via GUI Frame|Tween 0.1s → 0.3s|
|Dentro da base|Sem efeitos, Brightness ligeiramente aumentado|Tween 2s|
|Z4 e Z5|DepthOfField.FarIntensity = 0.8 permanente|Tween 3s ao entrar|
|Criatura próxima|Vibração leve de câmera (sin wave amplitude 0.1)|Enquanto criatura < 30 studs|

## **AtmosphereController — Script Completo**
-- StarterPlayerScripts > AtmosphereController (LocalScript)

local TweenService = game:GetService('TweenService')

local RunService   = game:GetService('RunService')

local Lighting     = game:GetService('Lighting')

local Players      = game:GetService('Players')

local player = Players.LocalPlayer

local char   = player.Character or player.CharacterAdded:Wait()

local hrp    = char:WaitForChild('HumanoidRootPart')

local currentZone = 0

local ZONE\_DEPTHS = {0, 400, 1600, 4800, 12000}

local ZONE\_CONFIG = {

`  `[1]={brightness=2.5,density=0.35,haze=1.5,color=Color3.fromRGB(0,120,200)},

`  `[2]={brightness=1.2,density=0.55,haze=2.5,color=Color3.fromRGB(0,70,140)},

`  `[3]={brightness=0.4,density=0.72,haze=3.5,color=Color3.fromRGB(0,30,80)},

`  `[4]={brightness=0.05,density=0.88,haze=4.5,color=Color3.fromRGB(0,5,30)},

`  `[5]={brightness=0.02,density=0.95,haze=5.0,color=Color3.fromRGB(30,0,10)},

}

local function getZone(d)

`  `for i=#ZONE\_DEPTHS,1,-1 do if d>=ZONE\_DEPTHS[i] then return i end end return 1

end

local function applyZone(zone)

`  `if zone == currentZone then return end

`  `currentZone = zone

`  `local cfg = ZONE\_CONFIG[zone]

`  `local ti  = TweenInfo.new(2, Enum.EasingStyle.Sine)

`  `TweenService:Create(Lighting,ti,{Brightness=cfg.brightness}):Play()

`  `TweenService:Create(Lighting.Atmosphere,ti,

`    `{Density=cfg.density,Haze=cfg.haze,Color=cfg.color}):Play()

`  `-- chamar switchMusic(zone) aqui

end

RunService.Heartbeat:Connect(function()

`  `local depth = math.max(0, -hrp.Position.Y)

`  `applyZone(getZone(depth))

end)


# **07 · Partículas e VFX**
## **Bolhas Ambiente**
ParticleEmitter por bloco de 200×200 studs do fundo, apontado para cima:

Texture      = [id bolha circular translúcida]

Rate         = 2

Lifetime     = NumberRange(8, 20)

Speed        = NumberRange(3, 8)

Size         = NumberSequence: 0→0.3, 0.5→1.2, 1→0.3

Transparency = NumberSequence: 0→0.3, 0.5→0.0, 1→1.0

LightEmission = 0.1

## **Neve Marinha (Zonas 3–5)**
Part invisível 50 studs acima do jogador, apontado para baixo. Segue o jogador via LocalScript:

Rate         = 40

Lifetime     = NumberRange(15, 30)

Speed        = NumberRange(0.5, 2)   -- descida muito lenta

Size         = NumberSequence: 0→0.05, 0.5→0.2, 1→0.05

Transparency = NumberSequence: 0→0.6, 0.5→0.2, 1→0.8

SpreadAngle  = Vector2(25, 25)

## **Bolhas de Respiração**
ParticleEmitter no rosto do personagem, emite a cada 3 segundos:

Rate     = 0   -- controlado por script

Lifetime = NumberRange(2, 4)

Speed    = NumberRange(2, 5)

Size     = NumberSequence: 0→0.1, 0.5→0.4, 1→0

-- chamada: emitter:Emit(3) a cada 3 segundos

## **Efeitos de Ação — Todos os VFX**

|**Situação**|**Efeito**|**Parâmetros-chave**|
| :- | :- | :- |
|Coletar recurso|Burst de partículas brilhantes no local|Rate=0, Emit(15), Lifetime 0.5s, LightEmission 1|
|Receber dano|Burst de bolhas vermelho-escuro|Rate=0, Emit(8), cor (120,0,0)|
|O₂ crítico (<15%)|Bolhas de pânico ao redor do jogador|Rate=30, tamanho pequeno, spread amplo|
|Morte|Nuvem de bolhas explodindo do personagem|Emit(50), alta velocidade, direções aleatórias|
|Chaminé hidrotérmica|Fumaça branca + fagulhas ascendentes|2 emitters: fumaça (rate 10, life 8s) + fagulha|
|Criatura bioluminescente|Partículas flutuando ao redor do corpo|Rate=3, LightEmission 0.8, Lifetime 3s|
|Evento: Tempestade|Detritos horizontais em alta velocidade|Rate=60, Speed 20+, SpreadAngle estreito|
|Arpão disparado|Whoosh + rastro de cavitação|Beam entre Attachment do arpão e ponto de impacto|
|Construção de módulo|Faíscas de solda + bolhas|Rate=20 durante 3s, LightEmission 0.5, laranja|


# **08 · Sistema de Áudio Completo**
## **Estrutura de SoundGroups**
SoundService

├── SoundGroup: Music       (Volume 0.6)  ← Músicas ambiente

├── SoundGroup: Ambience    (Volume 0.8)  ← Sons contínuos

├── SoundGroup: SFX         (Volume 1.0)  ← Efeitos pontuais

├── SoundGroup: Creature    (Volume 0.9)  ← Sons de criaturas

├── SoundGroup: UI          (Volume 0.7)  ← Cliques e notificações

└── SoundGroup: Player      (Volume 1.0)  ← Respiração, dano, morte

## **Músicas Ambiente por Zona**

|**Zona**|**Estilo musical**|**Características**|**Onde buscar**|
| :- | :- | :- | :- |
|Z1 – Costeira|Ambient oceânico suave, notas altas de piano|70–80 BPM, sem percussão, loop sem corte|Freesound.org: 'underwater ambient calm'|
|Z2 – Recife|Mais tenso, drones graves adicionados, ainda melódico|60 BPM, drone constante, loop|'deep sea ambient tense drone'|
|Z3 – Abyss Raso|Minimalista, drones profundos, notas isoladas de corda|Quase atonal, loop|'abyss ambient horror dark drone'|
|Z4 – Profundo|Quase silêncio, baixo industrial muito lento, sons distantes|Volume 0.3, panning de lado a lado|'deep horror ambient no melody'|
|Z5 – Hadal|Silêncio cortado por pulsos graves. Não é música, é atmosfera|Volume 0.25. Sons de 'presença'|'hadal zone horror soundscape'|
|Base|Mecânico suave, computadores, ventiladores|Volume 0.4. Sem tensão intencional|'submarine interior ambient hum'|

## **Script de Música Adaptativa**
-- Dentro do applyZone(zone) no AtmosphereController:

local tracks = {'Zone1','Zone2','Zone3','Zone4','Zone5'}

local function switchMusic(zone)

`  `local MusicGroup = game:GetService('SoundService'):FindFirstChild('Music')

`  `for \_,s in pairs(MusicGroup:GetChildren()) do

`    `TweenService:Create(s,TweenInfo.new(2),{Volume=0}):Play()

`    `task.delay(2, function() s:Stop() end)

`  `end

`  `local track = MusicGroup:FindFirstChild(tracks[zone])

`  `if track then

`    `track.Volume = 0 ; track:Play()

`    `TweenService:Create(track,TweenInfo.new(2),{Volume=0.5}):Play()

`  `end

end

## **Sons de Ambiente Contínuos**

|**Som**|**Onde colocar**|**Volume base**|**Comportamento dinâmico**|
| :- | :- | :- | :- |
|Água / bolhas / fluxo|Part invisível no centro de cada zona|0\.4|Pitch aumenta com profundidade via PitchShiftSoundEffect|
|Rangido de pressão|HumanoidRootPart do personagem|0\.0|Volume 0→0.7 conforme profundidade aumenta|
|Zumbido da base|Part central de cada módulo energizado|0\.3|Só ativo quando módulo de energia ligado|
|Batimento cardíaco|HumanoidRootPart do personagem|0\.0|Volume 0→0.8 quando O₂ < 20%|
|Vento / correntes|Part invisível na zona de corrente|0\.25|Ativo só onde há correntes. Panning direcional|

## **SFX Pontuais — Lista Completa**

|**Ação / Evento**|**Som**|**Canal**|**Disparo**|
| :- | :- | :- | :- |
|Coletar recurso|Borbulha satisfatória + clique|SFX|LocalScript ao coletar|
|Abrir inventário|Click mecânico suave|UI|LocalScript|
|Crafting concluído|Dois tons ascendentes (ding ding)|SFX|LocalScript ao receber item|
|Construir módulo|Cliques metálicos + confirmar|SFX|LocalScript ao finalizar|
|Receber dano físico|Golpe surdo + bolha distorcida|Player|LocalScript ao levar dano|
|Dano de pressão|Rangido metálico forte do traje|Player|LocalScript a cada tick|
|Alarme O₂ (<15%)|Bipe eletrônico intermitente (2/seg)|Player|LocalScript ao cruzar 15%|
|Morte do jogador|Silêncio crescente + pulso de baixo|Player|LocalScript ao morrer|
|Evento de servidor|Sirene + anúncio de áudio da zona|SFX|RemoteEvent → LocalScript|
|Arpão disparado|Whoosh + cavitação|SFX|LocalScript ao usar|
|Base sem energia|Alarme baixo + sistemas desligando|SFX|RemoteEvent → LocalScript|

## **Assinaturas Sonoras das Criaturas**

|**Criatura**|**Som de aproximação**|**Som de ataque**|**Som de morte**|
| :- | :- | :- | :- |
|Tubarão Caçador|Baixo pulsante rítmico sutil|Rangido + splash|Borbulha pesada descendente|
|Água-Viva Elétrica|Estática elétrica distante|Descarga: buzz elétrico forte|Sizzle + borbulha|
|Polvo Abissal|Sussurro invertido + click de tentáculo|Splash + grito abafado|Jato (woosh + borbulha)|
|Leviatã|Vibração de baixa freq., 4 seg antes|Rugido distorcido subaquático|Agonia de 8 seg + silêncio|
|A Coisa|Nenhum — aparece em silêncio|Som não-natural, não-animal|Sem morte — ela some|

**PANNING:** Use RollOffMode = 'Linear' nos Sons de criaturas. O jogador ouve de qual direção a criatura vem — essencial para o gameplay de sobrevivência.


# **09 · Interface (HUD e Menus)**
## **HUD — Elementos e Posicionamento**

|**Elemento**|**Posição**|**Comportamento**|
| :- | :- | :- |
|Barra de O₂|Centro inferior|Azul → Amarelo (30%) → Vermelho piscando (10%). Alarme sonoro em 15%|
|HP / Integridade do traje|Esquerda inferior|Só aparece quando < 80%. Some quando cheio|
|Indicador de profundidade|Superior direito|Metros atuais + zona ('Zona 2 — Recife Profundo')|
|Barra de pressão|Superior direito (abaixo)|Verde = seguro, vermelho = crítico|
|Sonar mini-map|Superior esquerdo|Círculo de radar. Verde = recursos, Vermelho = criaturas|
|Barra de ação rápida|Inferior central|6 slots. Similar ao hotbar do Minecraft|
|Indicador de Evento|Superior central|APENAS durante eventos. Conta regressiva + nome|
|Objetivo ativo|Lateral direita|1–3 objetivos com progresso. Desaparece ao completar|
|Ranking de profundidade|Lateral esquerda (recolhível)|Top 5 do servidor. Atualiza a cada 30s|

## **Menus Principais**
- Inventário (E): grid com ícones grandes, organizado por categoria. Drag & drop
- Crafting (C): lista com ícones, mostra o que pode e o que falta. Filtros por tier
- Base (B): visão isométrica da base com módulos clicáveis para upgrade e reparo
- Codex (Tab): criaturas descobertas, lore coletado, blueprints obtidos
- Mapa (M): zonas desbloqueadas, posição da base, pontos de interesse do sonar

## **Design Mobile**
- Botões de ação grandes na parte inferior da tela (área do polegar)
- Coletar recurso: botão flutuante aparece quando próximo de recurso
- Inventário e mapa: ícones no canto superior. Ocupam no máximo 15% da tela
- HUD de O₂ maior que no PC — deve ser legível em tela de 5 polegadas
- Testar em resoluções: 375×667, 390×844 e 412×915 (iPhones e Androids comuns)


# **10 · Onboarding e Tutorial**
## **Cutscene de Introdução (15 segundos)**
1. Tela preta com som de água crescendo
1. Câmera afunda lentamente pelo oceano, Z1 aparece com toda a sua beleza
1. Câmera continua descendo, ficando mais escuro, até revelar o sub avariado no fundo
1. Luz de emergência piscando dentro do sub. Título ABYSS SURVIVAL aparece e some
1. Fade in no personagem dentro do sub. O jogador já está no controle

**IMPORTANTE:** Sem texto durante a intro. A narrativa visual é suficiente e mais impactante. Não explique o que aconteceu — deixe o jogador descobrir.

## **Sequência de Objetivos Guiados (primeiros 10 minutos)**

|**Objetivo**|**Como ensina**|**Trigger de conclusão**|
| :- | :- | :- |
|Sair do submarino avariado|Porta do sub está aberta. Waypoint aponta para ela|Player sai do sub|
|Coletar 3 Algas|Algas visíveis logo na frente. Dica: 'Pressione E para coletar'|3 algas no inventário|
|Coletar 2 Sucatas|Sucatas visíveis no naufrágio ao lado|2 sucatas no inventário|
|Abrir o inventário|Dica flutuante: 'Pressione E para ver o que coletou'|Inventário aberto 1x|
|Ir até a plataforma da base|Waypoint aponta para área predefinida de base|Player chega à área|
|Construir o Casco Central|Mini-tutorial de construção aparece|Casco Central posicionado|
|Craftar o Módulo de O₂|Bancada de Trabalho no sub já está disponível|Módulo de O₂ no inventário|
|Instalar o Módulo de O₂ na base|Instrução visual de encaixe do módulo|Módulo instalado e funcionando|

## **Tutorial Contextual — Dicas Automáticas**
Aparecem na primeira vez que o jogador encontra cada situação. Nunca interrompem o gameplay:

- O₂ chega a 50% pela primeira vez → 'Seu oxigênio está caindo. Encontre uma estação ou volte à base.'
- Primeira criatura hostil avistada → 'Cuidado! Esta criatura ataca se entrar no campo de visão dela.'
- Primeiro recurso raro encontrado → 'Recurso Raro! Itens deste tipo são essenciais para Tier 2.'
- Primeira entrada de zona avistada → 'Zona 2 à frente. Você precisará de equipamento de pressão.'
- Primeira vez na base após acumular recursos → 'Você tem materiais para craftar. Abra a bancada (C).'
- Primeiro evento de servidor → 'Evento ativo! Coopere com outros jogadores para maximizar recompensas.'

## **Tela de Resumo de Sessão**
Aparece quando o jogador sai do jogo ou morre definitivamente. Cria identidade e vontade de melhorar:

- Profundidade máxima atingida nesta sessão (ex: '340m — Zona 2')
- Comparação com sessão anterior ('↑ +80m em relação à última sessão')
- Recursos coletados no total da sessão
- Criaturas encontradas pela primeira vez (se houver)
- Fragmentos de lore descobertos
- Próximo objetivo desbloqueado ('Próximo passo: craftar Traje de Pressão T1')


# **11 · Social e Multiplayer**
## **Sistema de Party**
- Jogadores do mesmo grupo spawnam no mesmo servidor automaticamente
- Limite de 4 por party dentro do servidor de 8–12 jogadores
- Líder da party pode marcar objetivos visíveis para todo o grupo
- Recursos coletados em dupla têm bônus de 10% (incentiva ficar junto)

## **Chat de Proximidade**
- Jogadores só ouvem quem está a menos de 50 studs de distância
- Cria isolamento real quando o grupo se separa — momento de tensão natural
- Comunicação com base: módulo de rádio permite falar com todos os jogadores da base

## **Sistema de Ping**
- Pressionar Q pinga localização no mapa com marcador de 30 segundos
- Segurar Q abre menu radial: 'Recurso aqui', 'Criatura aqui', 'Preciso de ajuda'
- Pings de 'Preciso de ajuda' piscam em vermelho no sonar de todos os jogadores do servidor

## **Papéis Voluntários**

|**Papel**|**Bônus passivo**|**Função ideal**|
| :- | :- | :- |
|Explorador|Consome O₂ 15% mais devagar|Vai primeiro a zonas novas, descobre recursos|
|Engenheiro|Constrói e repara módulos 30% mais rápido|Gerencia a base, mantém energia e O₂|
|Combatente|Leva 20% menos dano de criaturas|Protege o grupo, enfrenta criaturas maiores|

**DESIGN:** Papéis são voluntários — o jogador escolhe na tela de início de sessão. Não obrigatórios. A cooperação emergente é mais divertida quando surge naturalmente, não forçada.


# **12 · Polimento Visual**
## **Animações de Feedback**

|**Ação**|**Animação**|**Duração**|**Importância**|
| :- | :- | :- | :- |
|Coletar recurso|Item flutua até o inventário com trilha de partículas|0\.5s|CRÍTICA — satisfação imediata|
|Crafting concluído|Item aparece com flash de luz + efeito de escala 0→1.2→1.0|0\.8s|ALTA|
|Construir módulo de base|Módulo 'encaixa' com animação de montagem + faíscas|1\.5s|ALTA|
|Receber dano|Câmera shake leve (amplitude 0.3, duração 0.3s)|0\.3s|ALTA|
|Morte|Personagem 'afunda' lentamente → tela escurece → fade in na base|3s total|CRÍTICA|
|Leviatã derrotado|Câmera shake forte, partículas de dissolução, música de vitória|5s|CRÍTICA|
|Novo bioma desbloqueado|Texto épico aparece no centro: 'ZONA 3 DESBLOQUEADA'|2s|ALTA|
|Evento iniciado|Sirene + texto de evento + HUD de evento aparece|1s|ALTA|

## **Indicadores Direcionais**
- Seta vermelha na borda da tela indicando direção da criatura que atacou
- Seta azul piscando indicando a estação de O₂ mais próxima quando O₂ < 30%
- Seta verde indicando direção da base quando O₂ < 20%
- Indicadores são circulares na borda da tela, não setas pontiagudas — mais imersivo

## **Transição de Zona**
1. Quando o jogador cruza a fronteira de zona: mensagem discreta aparece no canto superior ('Zona 2 — Recife Profundo')
1. Iluminação começa a transicionar via Tween de 2 segundos
1. Música começa a mudar: fade out da atual (2s) + fade in da nova (2s)
1. Som de pressão começa se for Z2 em diante
1. Efeito de partículas de transição: bolhas densas por 1 segundo

## **Câmera e Sensação de Peso**
- Câmera padrão: ligeiramente mais baixa que o normal do Roblox. Simula flutuação
- Bob de câmera ao nadar: oscilação suave no eixo Y (amplitude 0.1, frequência 0.8 Hz)
- Sem bob quando parado dentro da base — cria contraste de tranquilidade
- FOV padrão: 70. Reduz para 55 ao estar em alta profundidade — simula pressão visual


# **13 · Economia e Balanceamento**
## **Drop Rates por Zona**

|**Recurso**|**Z1**|**Z2**|**Z3**|**Z4**|**Z5**|
| :- | :- | :- | :- | :- | :- |
|Algas / Sucata / Calcário|90%|40%|10%|0%|0%|
|Ferro Simples|60%|30%|5%|0%|0%|
|Cristal Marinho|0%|70%|20%|5%|0%|
|Ferro Abissal|0%|40%|30%|10%|0%|
|Titânio das Profundezas|0%|0%|60%|20%|5%|
|Gel Bioluminescente|0%|15%|50%|15%|5%|
|Núcleo Térmico|0%|0%|20%|50%|10%|
|Shard Hadal|0%|0%|0%|30%|70%|
|Relíqua Única|0%|0%|5%|10%|20%|

**NOTA:** % indica chance de encontrar o recurso em um nó de coleta da zona. Um nó de Z3 tem 60% de chance de ser Titânio. O tipo exato dentro da raridade ainda é aleatório.

## **Curva de Dificuldade**

|**Marco**|**Tempo esperado**|**Se levar mais tempo — problema**|
| :- | :- | :- |
|Primeiro módulo de base construído|5–8 min|Tutorial confuso ou recursos escassos demais em Z1|
|Tier 1 (Traje de Pressão)|15–25 min/sessão|Drop rate de Ferro muito baixo ou receita muito cara|
|Primeira morte|10–20 min|Se < 10 min: jogo muito difícil. Se > 30 min: muito fácil|
|Primeira entrada na Z2|20–35 min total|Transição de zona não está clara ou barreira de Tier alta|
|Leviatã derrotado (Z4)|10–15 sessões|Requer balancear dano do boss vs dano máximo do Tier 3|
|Acesso à Z5|20+ sessões|Deve ser conquista rara — não facilite demais|

## **Anti-Grind**
- Recursos têm cooldown de respawn: 5–10 min após coleta. Força exploração de novos pontos
- Limite de stack no inventário: 99 unidades de cada recurso. Evita hyperacumulação
- Daily quests recompensam variação — não repetir sempre a mesma ação
- Cada zona tem exatamente os recursos que você precisa para sair dela — sem grinding em zona anterior

## **Custo de Morte — Regra de Ouro**
**NUNCA:** Perda de 100% dos recursos. Destrói a vontade de jogar de uma vez.

**IDEAL:** Perda de 40% dos recursos da mochila. Base e módulos ficam intactos. Jogador perde tempo, não progresso permanente.

- Recursos mais raros têm chance menor de perda: Épico perde 20%, Único perde 10%
- Game Pass pode reduzir perda na morte — único uso legítimo de Robux afetando gameplay (conveniência, não poder)


# **14 · Lore e Narrativa**
## **Premissa e Mistério Central**
*Você é um engenheiro de manutenção do Submarino Kosmos-7. Ao acordar, o sub está avariado a 340 metros de profundidade. Sem contato com a superfície. Sem memória do que aconteceu. Os outros tripulantes: desaparecidos.*

O mistério central que o jogador deve ir descobrindo ao longo das zonas:

- O que aconteceu com a tripulação?
- Para que servem as ruínas nas Z3 e Z4 — elas são antigas demais para ser humanas
- O que é A Coisa na Z5 — não é uma criatura natural
- A Fissura Hadal não é geológica — foi aberta por alguém

**REGRA:** O MVP não revela nenhuma resposta. Só perguntas. As respostas ficam para updates futuros — é o que mantém jogadores voltando.

## **8 Fragmentos de Lore — Posicionamento e Conteúdo**

|**Fragmento**|**Onde encontrar**|**Conteúdo (breve)**|
| :- | :- | :- |
|Log de Áudio #1|Dentro do Kosmos-7 (sub do spawn)|Voz do capitão, cortada. 'Não devíamos ter chegado tão fundo...'|
|Nota do Engenheiro|Gaveta no módulo de rádio do sub|Lista técnica de falhas. Última linha: 'Ela ouviu nós.'|
|Log de Áudio #2|Estação de Pesquisa Abandonada (Z2)|Pesquisadora descreve primeiros sinais do 'padrão de luz'|
|Diário de Campo|Caverna oculta em Z2|Anotações de mergulhador. Desenhos de criatura que não existe|
|Transmissão Fragmentada|Laboratório Perdido (Z3)|Sinal de rádio ainda ativo. Coordenadas de A Fissura|
|Gravação em Pedra|Ruínas de Z3 (estilo pictograma)|Representação de criaturas + humanoides. Parece ritual|
|Log Final do Capitão|Naufrágio de navio de pesquisa (Z4)|A expedição anterior. Eles chegaram ao mesmo lugar. Não voltaram.|
|O Altar Abissal|Z5 — apenas quem chega ao endgame|Sem texto. Uma imagem. O jogador interpreta sozinho.|

## **Codex**
- Menu acessado via Tab. Dividido em: Criaturas, Lore, Blueprints
- Criaturas: imagem + nome + zona + nota de comportamento. Desbloqueada ao avistar
- Lore: fragmentos em ordem encontrada, não em ordem cronológica — propositalmente confuso
- Blueprints: receitas de crafting desbloqueadas. Alguns só aparecem após encontrar item raro


# **15 · Técnico e Segurança**
## **Estrutura de Scripts**

|**Script / Module**|**Tipo**|**Responsabilidade**|
| :- | :- | :- |
|OxygenSystem|ModuleScript (Server)|Consumo, recarga, morte por asfixia de cada jogador|
|PressureSystem|ModuleScript (Server)|Monitora profundidade, aplica dano por zona|
|ResourceManager|ModuleScript (Server)|Spawna e controla recursos, reset após coleta|
|CraftingSystem|ModuleScript (Server)|Valida receitas, consome inventário, cria itens|
|CreatureAI|Script (Server)|Comportamento de cada tipo: patrulha, agressão, fuga|
|BaseManager|ModuleScript (Server)|Módulos da base, energia, O₂ recharge|
|EventSystem|Script (Server)|Dispara eventos aleatórios a cada 15 min|
|HUDController|LocalScript (Client)|Atualiza HUD via RemoteEvents. Máximo 10x/seg|
|InventoryClient|LocalScript (Client)|UI de inventário e crafting. Envia pedidos ao servidor|
|AtmosphereController|LocalScript (Client)|Efeitos visuais por zona (ver Cap. 06)|
|SoundManager|LocalScript (Client)|Música, O₂, criaturas, efeitos de pressão|
|DataStore|Script (Server)|Salva progressão: base, itens, codex, tier atual|

## **Anti-Exploit — Regras Fundamentais**
**NUNCA CONFIE NO CLIENTE:** Quantidade de itens, HP, posição de base e crafting devem ser sempre re-validados no servidor.

- Rate limiting em RemoteEvents críticos: máximo 1 chamada de 'coletar' por 0.5 segundos por jogador
- Validar distância: jogador deve estar a menos de 10 studs do recurso para coletar
- Receitas de crafting ficam apenas no servidor. Cliente envia pedido, servidor valida e executa
- HP nunca pode ser alterado pelo cliente — só pelo servidor via RemoteEvent de dano validado
- Posições de módulos de base verificadas pelo servidor — não aceitar posições inválidas ou sobrepostas

## **DataStore com Retry**
local DataStoreService = game:GetService('DataStoreService')

local store = DataStoreService:GetDataStore('PlayerData\_v1')

local function saveWithRetry(userId, data, attempts)

`  `attempts = attempts or 0

`  `local ok, err = pcall(function()

`    `store:SetAsync(tostring(userId), data)

`  `end)

`  `if not ok and attempts < 3 then

`    `task.wait(2)

`    `saveWithRetry(userId, data, attempts + 1)

`  `elseif not ok then

`    `warn('DataStore falhou após 3 tentativas:', err)

`    `-- notificar jogador via RemoteEvent

`  `end

end

## **Performance — Regras**
- Streaming Enabled: ativo. Assets carregam conforme proximidade do jogador
- Pooling de criaturas: criaturas mortas são desativadas (Enabled = false), não deletadas
- Pooling de recursos: mesma lógica — reativa o Part existente ao invés de criar novo
- CastShadow = false em todos os assets decorativos (coral, rocha, algas)
- HUD não atualiza mais que 10× por segundo — usa Heartbeat com debounce
- Limite de 3 ParticleEmitters simultâneos por jogador
- Meta de performance: servidor com 12 jogadores < 50ms de tick
- Teste obrigatório antes do launch com 10 bots ou jogadores reais


# **16 · Monetização**
## **Princípio Fundamental**
**REGRA DE OURO:** Tudo que afeta gameplay deve ser conquistável jogando. Robux são apenas para cosméticos e conveniência.

## **Game Passes — Compra Única**

|**Game Pass**|**Preço sugerido**|**Benefício**|
| :- | :- | :- |
|Abyss Explorer|199 R$|Slot extra de base, mochila maior, cosmético exclusivo de traje|
|Deep Diver Bundle|399 R$|Veículo cosmético exclusivo, acesso antecipado a novos biomas em updates|
|Founder's Pack|799 R$|Badge exclusiva, traje único, nome destacado no placar de profundidade|

## **Developer Products — Compra Repetível**

|**Produto**|**Preço sugerido**|**Descrição**|
| :- | :- | :- |
|Boost de O₂ (×2 por 1h)|25 R$|Consumo de O₂ reduzido 50% por 1 hora. Conveniência, não poder|
|Slot de Baú Extra|50 R$|Adiciona 1 baú extra permanente à base no servidor atual|
|Mapa do Tesouro|75 R$|Revela 3 locais de recursos raros no mapa atual|
|Cosméticos de Traje|50–150 R$|Skins para o traje. Sem impacto em gameplay|

**NUNCA VENDER:** O₂ extra, HP bônus, recursos raros diretamente, speed permanente, dano extra. Qualquer coisa que faça um jogador pago ser mecanicamente superior.


# **17 · Marketing e Launch**
## **Thumbnail Principal**
- Dimensão: 1:1 (quadrado), mínimo 512×512, idealmente 1024×1024
- Cena: personagem de traje futurista olhando para criatura enorme saindo das trevas
- Iluminação: fundo escuro, lanterna do personagem iluminando a criatura parcialmente
- Texto: 'ABYSS SURVIVAL' em fonte bold, branca, no terço inferior. Nada mais
- Teste: thumbnail deve ser reconhecível reduzida a 80×80 pixels (tamanho no feed)

## **Ícone do Jogo (512×512)**
- Close no visor do capacete refletindo uma criatura enorme no interior do reflexo
- Fundo: azul-escuro profundo
- Sem texto — deve ser icônico pela imagem

## **Descrição da Página**
*500 metros abaixo da superfície. Oxigênio acabando. Algo se aproxima.*

*Explore o fundo do oceano, construa uma base subaquática e sobreviva às criaturas das profundezas. Gerencie oxigênio e pressão enquanto desvenda os mistérios de um mundo nunca explorado.*

*✔ 5 biomas únicos   ✔ Base totalmente customizável   ✔ Criaturas com IA real   ✔ Lore misterioso*

## **Screenshots da Página (mínimo 3)**
- Screenshot 1: Zona 1 com todo o coral colorido + personagem explorando — mostra beleza visual
- Screenshot 2: Base construída com módulos + jogador dentro da base — mostra progressão
- Screenshot 3: Criatura enorme de perto com bioluminescência — mostra tensão e criatividade

## **Crescimento Orgânico**
- Grupo do Roblox: crie antes do launch. Recompensa: cosmético exclusivo para membros. Meta: 1.000 antes do dia 1
- Badge de boas-vindas: todo jogador recebe ao entrar pela primeira vez. Custo zero, gera engajamento
- TikTok: clips de 15–30s mostrando momentos tensos (O₂ quase zero, leviatã aparecendo). Potencial viral
- YouTubers de médio porte: 100k–500k inscritos. Melhor custo-benefício. Ofereça acesso antecipado
- Reddit r/roblox: post de 'como eu fiz' com processo de criação. Gera engajamento genuíno
- Anunciar Bioma 4 como conteúdo do primeiro update antes do launch — cria antecipação

## **Métricas de Sucesso**

|**Métrica**|**Meta (1 mês)**|**Meta (3 meses)**|
| :- | :- | :- |
|Visitas totais|100\.000|1\.000.000|
|Players simultâneos (pico)|200+|1\.000+|
|Tempo médio de sessão|20+ min|30+ min|
|Taxa de retorno D1|30%+|40%+|
|Conversão para Robux|3%+|5%+|
|Avaliação (likes/total)|75%+|80%+|


# **18 · Plano de Execução — 14 Semanas**
## **Semana 1–2: Core Survival**
- Sistema de Oxigênio com todos os valores (consumo, recarga, morte)
- Sistema de HP básico com dano e respawn
- Controles de movimento subaquático (gravidade reduzida, flutuação)
- Teste com cena simples — cubo representando o mapa. Nada visual ainda

**CRITÉRIO:** Só avance quando o loop de sobrevivência (nadar, consumir O₂, morrer, respawnar) for divertido por si só.

## **Semana 3–4: Mundo Base**
- Bioma 1 completo no Terrain Editor com assets definitivos
- Sistema de coleta de recursos (5 tipos)
- 3 criaturas com IA básica: Peixe Fantasma, Tubarão, Água-Viva
- Iluminação da Zona 1 configurada

## **Semana 5–6: Crafting e Base**
- Sistema de crafting funcional com todas as receitas Tier 0
- Módulos de base posicionáveis (Casco, O₂, Câmara de Pressão)
- DataStore salvando inventário e base
- HUD básico (O₂, HP, profundidade)

## **Semana 7–8: Progressão**
- Sistema de pressão por zona com dano
- Bioma 2 completo com iluminação
- Receitas Tier 1 e traje de pressão
- Daily quests (3 por dia)
- Tutorial contextual para mecânicas principais

## **Semana 9–10: Conteúdo e Atmosfera**
- Bioma 3 completo
- AtmosphereController com transições entre Z1–Z3
- Sistema de áudio completo (música, SFX, criaturas)
- Todos os ParticleEmitters implementados
- 3 eventos de servidor funcionando
- 6–8 fragmentos de lore posicionados

## **Semana 11–12: Polimento e Social**
- Animações de feedback (coleta, crafting, morte)
- Indicadores direcionais de dano e O₂
- Sistema de party e ping
- Chat de proximidade
- Mobile: botões touch e HUD adaptado
- Cutscene de introdução
- Tela de resumo de sessão

## **Semana 13: Beta Fechado**
- Testar com 20–50 jogadores reais
- Foco: dificuldade, drop rates, tempo de progressão
- Corrigir exploits identificados
- Ajustar balanceamento com base no feedback

## **Semana 14: Launch**
- Monetização implementada e testada
- Thumbnail, ícone e descrição finalizados
- Grupo do Roblox com recompensa ativa
- Teste de performance com 10+ jogadores simultâneos
- Bioma 4 em produção (para primeiro update em 2 semanas pós-launch)

## **Checklist Final de Launch**

|**✅ Core gameplay**|
| :- |
|- Sistema de O₂ testado e balanceado|
|- Sistema de pressão por zona funcionando|
|- Crafting com receitas T0 e T1 completas|
|- Base com 5+ módulos funcionais|
|- DataStore com retry — sem perda de progresso|
||

|**✅ Conteúdo**|
| :- |
|- Biomas 1, 2 e 3 com assets, recursos e criaturas|
|- 5+ criaturas com IA distinta|
|- 3+ eventos de servidor funcionando|
|- 6+ fragmentos de lore posicionados|
|- Tutorial contextual para todas as mecânicas|
||

|**✅ Polimento**|
| :- |
|- HUD completo e legível em mobile|
|- Animações de feedback implementadas|
|- Música e SFX funcionando em todas as zonas|
|- Cutscene de introdução rodando|
|- Tela de resumo de sessão ativa|
||

|**✅ Launch**|
| :- |
|- Monetização implementada (Game Pass + Developer Products)|
|- Thumbnail e ícone profissionais|
|- Descrição da página otimizada|
|- 3+ screenshots na página|
|- Grupo do Roblox com recompensa ativa|
|- Testado com 10+ jogadores sem lag|
||

Abyss Survival — Documento Master v1.0	www.roblox.com
