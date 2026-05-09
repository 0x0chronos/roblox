ABYSS SURVIVAL  —  Guia Técnico: Terreno, Visuais e Áudio  |  Roblox Studio

🌊

**ABYSS SURVIVAL**

Guia Técnico de Produção

Terreno · Visuais · Iluminação · Partículas · Áudio  |  Roblox Studio

|**Módulo**|**Ferramenta principal**|**Prioridade**|
| :- | :- | :- |
|Terreno & Layout do Mundo|Roblox Terrain Editor + Parts|CRÍTICO|
|Iluminação & Atmosfera|Lighting Service + Atmosphere|CRÍTICO|
|Visuais por Bioma|Surface Appearance + MaterialVariants|ALTO|
|Partículas & VFX|ParticleEmitter + Beams|ALTO|
|Pós-Processamento|ColorCorrectionEffect + BlurEffect|MÉDIO|
|Áudio Ambiente|Sound + SoundService|ALTO|
|Música Adaptativa|SoundGroup + Script Luau|MÉDIO|
|Efeitos Sonoros (SFX)|LocalScript + RemoteEvent|ALTO|


# **1. Estrutura e Layout do Mundo**
## **1.1 Dimensões e Coordenadas**
O mundo é vertical — a câmera desce pelo eixo Y negativo conforme o jogador mergulha. Organize o workspace assim:

|**Zona**|**Y mínimo (studs)**|**Y máximo (studs)**|**Equivalência real**|**Tamanho horizontal (X/Z)**|
| :- | :- | :- | :- | :- |
|Zona 1 — Zona Costeira|Y -0|Y -400|0–50m|1\.200 × 1.200 studs|
|Zona 2 — Recife Profundo|Y -400|Y -1.600|50–200m|900 × 900 studs|
|Zona 3 — Abyss Raso|Y -1.600|Y -4.800|200–600m|700 × 700 studs|
|Zona 4 — Abyss Profundo|Y -4.800|Y -12.000|600–1500m|500 × 500 studs|
|Zona 5 — Hadal / Endgame|Y -12.000|Y -16.000|1500m+|300 × 300 studs|

**ESCALA:** Use 1 stud = 12,5 cm (escala padrão Roblox humanoides). Assim, 400 studs = 50 metros de profundidade real. Mantenha essa proporção para que as barras de pressão e O2 façam sentido numérico.

## **1.2 Organização do Workspace**
Estrutura de pastas recomendada no Workspace do Roblox Studio:

Workspace

├── World

│   ├── Zone1\_Coastal       ← Parts, Terrain, Props da Zona 1

│   ├── Zone2\_Reef          ← Parts, Terrain, Props da Zona 2

│   ├── Zone3\_AbyssShallow  ← Parts, Terrain, Props da Zona 3

│   ├── Zone4\_AbyssDeep     ← Parts, Terrain, Props da Zona 4

│   └── Zone5\_Hadal         ← Parts, Terrain, Props da Zona 5

├── Bases                   ← Módulos de base dos jogadores (instanciados via script)

├── Creatures               ← Modelos de criaturas (SpawnPoints + modelos)

├── Resources               ← Nós de recursos coletáveis (gerenciados via ResourceManager)

├── Events                  ← Objetos usados em eventos (wreck, hydrotermal, etc.)

└── FX                      ← Efeitos globais: partículas de água, névoa, bolhas ambiente

**DICA:** Cada zona deve ter um BoolValue chamado 'StreamingEnabled' dentro dela. O script AtmosphereController usa esse valor para saber qual zona carregar ao redor do jogador.

## **1.3 Terreno com Roblox Terrain Editor**
Use exclusivamente o Terrain Editor nativo do Roblox — não use Parts para o solo principal. Isso garante performance e compatibilidade com Streaming.

### **Materiais de Terreno por Zona**

|**Zona**|**Material base do fundo**|**Material das paredes/rochas**|**Material especial**|
| :- | :- | :- | :- |
|Z1 — Costeira|Sand (areia clara)|Rock, Limestone|Grass (algas no topo de rochas)|
|Z2 — Recife|Sand (cinza-azulado)|Rock, SmoothPlastic (coral)|Ground (lodo esverdeado)|
|Z3 — Abyss Raso|Mud (lama escura)|Basalt, Rock|Neon (fissuras de bioluminescência)|
|Z4 — Abyss Profundo|Slate (pedra negra)|Basalt, Granite|Obsidian via MeshPart|
|Z5 — Hadal|Slate + Basalt mesclados|Granite (formações alienígenas)|Magma (simulado via Neon + script)|

### **Passo a passo para esculpir cada zona**
1. Abra o Terrain Editor (Home → Editor → Terrain Editor)
1. Use a ferramenta 'Generate' para criar base rápida: escolha o material principal da zona e gere um volume inicial de 1200×400×1200 studs para Zona 1
1. Use 'Sculpt → Erode' para criar cavernas, ravinas e entradas entre zonas. Tamanho do brush: 30–60 studs para detalhes, 100+ studs para volumes maiores
1. Use 'Paint' para pintar diferentes materiais sobre o terreno gerado — isso cria variação natural sem modelagem manual
1. Use 'Sculpt → Smooth' para suavizar bordas artificiais — terreno subaquático não tem bordas afiadas
1. Adicione Parts e MeshParts (rochas, coral, ruínas) sobre o terreno gerado para detalhe visual — não modelados no Terrain

**PERFORMANCE:** Terreno do Roblox é otimizado automaticamente. Parts decorativas devem usar 'Anchored = true' e 'CanCollide = false' quando não precisam de física — reduz carga do servidor drasticamente.


# **2. Iluminação e Atmosfera por Zona**
## **2.1 Configuração Global do Lighting Service**
O Lighting Service controla a iluminação global de todo o jogo. Configure assim no início do projeto:

-- StarterPlayerScripts > LightingSetup (LocalScript)

local Lighting = game:GetService('Lighting')

Lighting.GlobalShadows    = true

Lighting.Brightness       = 1

Lighting.EnvironmentSpecularScale = 0.5

Lighting.EnvironmentDiffuseScale  = 0.5

Lighting.ClockTime        = 14  -- luz de tarde, neutra

Lighting.GeographicLatitude = 0

Adicione os seguintes efeitos como filhos do Lighting no Explorer:

- Atmosphere (obrigatório — cria neblina subaquática)
- ColorCorrectionEffect (ajuste de cor por zona via script)
- BlurEffect (desfoque por falta de O₂ — intensidade 0 padrão)
- DepthOfFieldEffect (foco em objetos próximos, blur no fundo — ativa em Zonas 3+)

## **2.2 Parâmetros de Iluminação por Zona**
Estes valores são aplicados pelo AtmosphereController (LocalScript) conforme o jogador muda de zona. Use TweenService para transição suave (2 segundos):

|**Propriedade**|**Z1 Costeira**|**Z2 Recife**|**Z3 Abyss Raso**|**Z4 Abyss Profundo**|**Z5 Hadal**|
| :- | :- | :- | :- | :- | :- |
|Lighting.Brightness|2\.5|1\.2|0\.4|0\.05|0\.02|
|Lighting.ClockTime|14|12|10|8|6|
|Atmosphere.Density|0\.35|0\.55|0\.72|0\.88|0\.95|
|Atmosphere.Offset|0\.1|0\.15|0\.2|0\.25|0\.3|
|Atmosphere.Color (RGB)|0,120,200|0,70,140|0,30,80|0,5,30|30,0,10|
|Atmosphere.Decay (RGB)|0,60,120|0,20,80|0,5,40|0,0,15|15,0,5|
|Atmosphere.Glare|0\.3|0\.1|0\.0|0\.0|0\.0|
|Atmosphere.Haze|1\.5|2\.5|3\.5|4\.5|5\.0|
|ColorCorrection.Brightness|0\.0|-0.05|-0.15|-0.3|-0.4|
|ColorCorrection.Contrast|0\.0|0\.05|0\.1|0\.2|0\.25|
|ColorCorrection.Saturation|0\.1|0\.0|-0.1|-0.3|-0.4|
|ColorCorrection.TintColor|Branco|Azul claro|Azul médio|Azul-negro|Vermelho escuro|
|DepthOfField ativo|Não|Não|Sim|Sim|Sim|

## **2.3 Iluminação Local por Zona**
Além da iluminação global, cada zona usa PointLights e SpotLights fixas para criar interesse visual:

### **Zona 1 — Zona Costeira**
- SurfaceLight em corais: Color (0, 200, 100), Brightness 2, Range 15 — simula algas com luz própria
- SpotLight apontando para baixo nos pontos mais fundos: Color (0, 100, 200), cria sombras dramáticas no fundo de areia
- Sem PointLights artificiais — a iluminação solar é suficiente nesta zona

### **Zona 2 — Recife Profundo**
- PointLight dentro de cada coral bioluminescente: Color (0, 180, 255), Brightness 3, Range 20
- PointLight azul fraca espalhada pelo fundo: Color (0, 50, 150), Brightness 0.8, Range 40 — simula luz solar difusa chegando de cima
- SpotLight em entradas de cavernas: Color (0, 20, 80), aponta para dentro, cria curiosidade

### **Zona 3 — Abyss Raso**
- PointLight verde nas fissuras de bioluminescência do terreno: Color (0, 255, 80), Brightness 5, Range 10
- PointLight azul-esverdeada em criaturas vivas (attached ao modelo): pulsa via script Tween
- SpotLight vermelha fraca nas chaminés hidrotérmicas: Color (255, 60, 0), Brightness 4, Range 25

### **Zona 4 e 5**
- Quase sem luz ambiente — a lanterna do jogador é a única fonte principal
- PointLight nas próprias criaturas bioluminescentes (cores únicas por espécie)
- Zona 5: PointLight laranja-avermelhada no magma simulado, Brightness 8, Range 50

**LANTERNA DO JOGADOR:** Adicione um SpotLight ao HumanoidRootPart do personagem via LocalScript. Ângulo: 50°, Range: 60 studs, Brightness: 3. Nas Zonas 1 e 2, defina Enabled = false automaticamente pois há luz suficiente.


# **3. Assets Visuais e Modelagem por Bioma**
## **3.1 Zona 1 — Zona Costeira: Lista de Assets**
Esta zona deve ser visualmente a mais rica e colorida — é a vitrine do jogo para novos players.

|**Asset**|**Como criar no Roblox Studio**|**Detalhes técnicos**|
| :- | :- | :- |
|Coral grande (5 variações)|MeshPart importado (.fbx simples) ou unions de Parts cilíndricas|SurfaceAppearance com textura de coral, emissive leve|
|Coral pequeno (scattered)|SpecialMesh tipo 'Sphere' achatada + colorida|CastShadow = false para performance|
|Algas ondulando|MeshPart plano + script de rotação suave (sin wave no CFrame)|Anchored = true, CanCollide = false|
|Pedras redondas do fundo|Union de esferas achatadas ou MeshPart básico|Material: Rock, tamanho variado (2–8 studs)|
|Areia do fundo|Terrain material Sand — não usar Parts|Sculpt leve para ondulações sutis|
|Naufrágio inicial (spawn)|MeshParts ou unions grandes, enferrujadas|Material: SmoothPlastic com cor enferrujada + decals de dano|
|Cardume de peixe (decorativo)|Billboard GUI com sprite animado OU ParticleEmitter tipo peixe|LocalScript apenas — não afeta servidor|
|Raios de sol subaquáticos|Beam entre dois Attachments com textura de raia de luz|Transparency gradiente de 0.2 a 1.0|
|Bolhas ascendentes (fundo)|ParticleEmitter no fundo do terreno|Ver seção de partículas|

## **3.2 Zona 2 — Recife Profundo: Lista de Assets**

|**Asset**|**Como criar**|**Detalhes técnicos**|
| :- | :- | :- |
|Coral bioluminescente|MeshPart + PointLight filho + script de pulso de brilho|Color azul-esverdeado, pulso a cada 2–4s (Tween)|
|Anemônas gigantes|Unions de esferas/cones alongados|Script de abertura/fechamento ao detectar jogador próximo|
|Rocha texturizada escura|MeshPart ou terrain Basalt|SurfaceAppearance: textura de rocha húmida|
|Cavernas com entrada visível|Sculpt no Terrain Editor (Erode tool), paredes de Basalt|PointLight na entrada para atrair atenção|
|Fragmentos de Estação|Unions de Parts metálicas (cilindros + cubos)|Decals de texto científico, janelas quebradas|
|Lodo no fundo|Terrain material Ground pintado sobre Sand|Sculpt suave para sensação pesada|
|Corrente d'água (VFX)|Beam horizontal entre dois Attachments com textura de fluxo|Move via script no CFrame dos Attachments|

## **3.3 Zona 3 — Abyss Raso: Lista de Assets**

|**Asset**|**Como criar**|**Detalhes técnicos**|
| :- | :- | :- |
|Fissuras bioluminescentes|Unions finas de Parts com Material: Neon, cor verde/azul|PointLight filho de baixa intensidade|
|Chaminé hidrotérmica|Cilindros empilhados com Material: Basalt, ParticleEmitter no topo|Partículas de fumaça + vapor ascendentes|
|Ruínas submersas (pedra)|MeshParts ou unions de blocos irregulares|Material: Slate, textura envelhecida, partes cobertas de lodo|
|Cristais de rocha|Unions de pirâmides/cones, Material: Neon ou SmoothPlastic|Cor ciano-esverdeada, PointLight sutil|
|Neve marinha (partícula)|ParticleEmitter global descendente|Ver seção de partículas — essencial para imersão|
|Vegetação mutante|MeshParts orgânicos irregulares|Cores não-naturais: roxo, magenta, laranja|
|Laboratório Perdido|Construção modular de Parts/Unions com materiais metálicos|Janelas com vidro translúcido, interior com props|

## **3.4 Zona 4 e 5 — Abyss Profundo e Hadal**
Nestas zonas o visual é mais abstrato e aterrorizante. Menos assets mas mais impactantes.

- Pedras negras monumentais: MeshParts grandes, irregulares, Material Slate/Granite. Sem detalhes — a forma é suficiente
- Serpentinas de sal: unions de formas cristalinas brancas agrupadas — contraste perturbador com o fundo negro
- Magma simulado (Z5): Parts planas com Material: Neon, cor laranja, com PointLight laranja + ParticleEmitter de fagulhas
- Cristais negros (Z5): unions de prismas finos e altos, Material: SmoothPlastic cor preta — geometria alienígena
- O Altar Abissal (Z5): estrutura modular central, partes de Unions + Decals de símbolos. O único ponto de interesse da zona

**OTIMIZAÇÃO ZONAS 4 e 5:** Estas zonas têm poucos jogadores simultâneos. Priorize imersão sobre variedade de assets. 10 assets únicos bem colocados valem mais que 50 assets repetidos.


# **4. Partículas e Efeitos Visuais (VFX)**
## **4.1 Sistema de Partículas Globais**
Estes ParticleEmitters ficam ativos em todas as zonas e criam a sensação constante de estar debaixo d'água:

### **Bolhas Ambiente (zona inteira)**
Um ParticleEmitter por bloco de 200×200 studs do fundo do terreno, apontado para cima:

Texture       = rbxassetid://[id de bolha circular translúcida]

Rate          = 2          -- bolhas por segundo por emitter

Lifetime      = NumberRange(8, 20)

Speed         = NumberRange(3, 8)   -- ascensão lenta

Size          = NumberSequence(0.3 a 1.2 a 0.3)  -- cresce e some

Transparency  = NumberSequence(0.3 a 0.0 a 1.0)

Rotation      = NumberRange(-45, 45)

RotSpeed      = NumberRange(-20, 20)

LightEmission = 0.1

Color         = ColorSequence(branco levemente azulado)

### **Neve Marinha (Zonas 3, 4, 5)**
ParticleEmitter em plano invisível 50 studs acima do jogador, apontado para baixo. Segue o jogador via LocalScript:

Texture       = rbxassetid://[id de ponto/floco branco]

Rate          = 40

Lifetime      = NumberRange(15, 30)

Speed         = NumberRange(0.5, 2)  -- descida muito lenta

Size          = NumberSequence(0.05 a 0.2 a 0.05)

Transparency  = NumberSequence(0.6 a 0.2 a 0.8)

SpreadAngle   = Vector2(25, 25)      -- espalha horizontalmente

RotSpeed      = NumberRange(-5, 5)

### **Partículas de Respiração do Jogador**
ParticleEmitter no rosto do personagem, emite bolhas ao pressionar W ou a cada 3 segundos:

Texture       = rbxassetid://[bolha pequena]

Rate          = 0  -- controlado por script, não contínuo

Lifetime      = NumberRange(2, 4)

Speed         = NumberRange(2, 5)

Size          = NumberSequence(0.1 a 0.4 a 0)

Emit(3)       -- chamado via script a cada respiração

## **4.2 Efeitos de Partículas por Evento**

|**Situação**|**Efeito de partícula**|**Parâmetros-chave**|
| :- | :- | :- |
|Coletar recurso|Burst de partículas brilhantes no local do recurso|Rate=0, Emit(15), Lifetime 0.5s, Speed alto, LightEmission 1|
|Receber dano|Burst de bolhas de sangue vermelho-escuro|Rate=0, Emit(8), cor (120,0,0), Speed moderado|
|O₂ crítico (<15%)|Bolhas de pânico ao redor do jogador, rápidas|Rate=30, tamanho pequeno, cor azulada, spread amplo|
|Morte|Nuvem de bolhas explodindo do personagem|Emit(50), alta velocidade, direções aleatórias|
|Chaminé hidrotérmica|Fumaça branca/cinza densa + fagulhas ascendentes|2 emitters: fumaça (rate 10, life 8s) + fagulha (rate 5, LightEmission 1)|
|Criatura bioluminescente|Partículas flutuando ao redor do corpo da criatura|Rate=3, cor da espécie, LightEmission 0.8, Lifetime 3s|
|Evento: Tempestade|Partículas de detritos horizontais em alta velocidade|Rate=60, size pequeno, Speed 20+, SpreadAngle estreito horizontal|
|Explosão de arpão|Flash de bolhas + detritos do impacto|Emit(30) mixed: bolhas + partícula de rocha, velocidades distintas|
|Construção de módulo|Faíscas de solda + bolhas de material|Rate=20 durante 3s, LightEmission 0.5, cor laranja|

## **4.3 Efeitos de Tela (Screen Effects via LocalScript)**
Aplicados via ColorCorrectionEffect e BlurEffect no Lighting, controlados por LocalScript conforme estado do jogador:

|**Estado do jogador**|**Efeito visual**|**Transição**|
| :- | :- | :- |
|O₂ 100–30%|Nenhum efeito adicional|—|
|O₂ 29–15%|ColorCorrection.TintColor azulado leve, Saturation -0.1|Tween 2s|
|O₂ 14–5%|Blur.Size = 5, Tint azul forte, tela pulsa levemente|Tween 1s|
|O₂ 0–morte|Blur.Size = 20, tudo escurece, ColorCorrection.Brightness -0.8|Tween 0.5s|
|Dano por pressão|Flash rápido de borda vermelha (Frame de GUI com cor vermelha transparente)|Tween 0.1s → 0.3s|
|Dentro da base|Sem efeitos, Brightness ligeiramente aumentado|Tween 2s|
|Zona 4 e 5|DepthOfField.FarIntensity = 0.8 (fundo desfocado permanente)|Tween 3s ao entrar|
|Criatura próxima|Vibração leve de câmera (CFrame offset sin wave, amplitude 0.1)|Enquanto criatura < 30 studs|


# **5. Simulação de Água e Superfície**
## **5.1 Água do Terrain**
Use o material Water nativo do Roblox Terrain para preencher todo o espaço acima do fundo em cada zona. É a forma mais performática e já tem animação básica:

1. No Terrain Editor → Fill: selecione Material 'Water' e preencha o volume de cada zona (de Y\_fundo até Y\_topo da zona)
1. Ajuste a propriedade WaterColor do Terrain para cada zona via script — tons progressivamente mais escuros e azul-esverdeados
1. WaterTransparency: ajuste de 0.5 (Z1, visível) até 0.85 (Z5, quase opaco) para simular visibilidade reduzida por profundidade
1. WaveSize e WaveSpeed: reduza progressivamente em zonas mais fundas (ondas apenas na Zona 1, zero nas Zonas 4 e 5)

## **5.2 Simulação de Flutuabilidade**
O Roblox não tem física de fluido real. Simule pelo script de movimento do personagem:

-- Em PlayerMovementScript (LocalScript)

local player = game.Players.LocalPlayer

local char   = player.Character

local hrp    = char:WaitForChild('HumanoidRootPart')

local hum    = char:WaitForChild('Humanoid')

-- Reduz gravidade enquanto debaixo d'água

local RunService = game:GetService('RunService')

RunService.Heartbeat:Connect(function()

`    `local depth = -hrp.Position.Y

`    `if depth > 50 then  -- dentro d'água

`        `hum.WalkSpeed     = 12  -- mais lento que em terra

`        `workspace.Gravity = 30  -- reduz de 196.2 para 30

`    `else

`        `workspace.Gravity = 196.2

`    `end

end)

**ATENÇÃO:** Gravity é global no workspace. Se houver partes do jogo fora d'água, use BodyVelocity ou LinearVelocity no personagem ao invés de alterar workspace.Gravity — assim só o personagem é afetado.


# **6. Sistema de Áudio Completo**
## **6.1 Estrutura de SoundGroups**
Organize todos os sons em SoundGroups dentro do SoundService. Isso permite controle global de volume por categoria:

SoundService

├── SoundGroup: Music        (Volume 0.6)  ← Músicas ambiente

├── SoundGroup: Ambience     (Volume 0.8)  ← Sons de ambiente contínuos

├── SoundGroup: SFX          (Volume 1.0)  ← Efeitos sonoros pontuais

├── SoundGroup: Creature     (Volume 0.9)  ← Sons de criaturas

├── SoundGroup: UI           (Volume 0.7)  ← Cliques, notificações

└── SoundGroup: Player       (Volume 1.0)  ← Respiração, dano, morte

## **6.2 Músicas Ambiente por Zona**
Cada zona tem sua própria música. A transição ocorre com FadeOut (2s) → FadeIn (2s) ao mudar de zona. Coloque os Sound objects em ReplicatedStorage > Sounds > Music:

|**Zona**|**Estilo musical**|**Características técnicas**|**Onde encontrar / referência**|
| :- | :- | :- | :- |
|Z1 — Costeira|Ambient oceânico, suave. Notas altas de piano ou flauta sobre pad de fundo|Tempo: 70–80 BPM, sem percussão. Loop sem corte. Volume 0.5|Roblox toolbox: 'underwater ambient calm' ou Freesound.org|
|Z2 — Recife|Mais tenso, drones graves adicionados. Ainda melódico mas inquietante|Tempo: 60 BPM, drone constante. Loop. Volume 0.55|Buscar: 'deep sea ambient tense drone'|
|Z3 — Abyss Raso|Minimalista. Drones profundos. Ocasional nota isolada de instrumento de corda|Tempo: indefinível. Quase atonal. Loop. Volume 0.5|Buscar: 'abyss ambient horror dark drone'|
|Z4 — Profundo|Quase silêncio. Baixo industrial muito lento. Sons que parecem gritos distantes|Volume 0.3, sons passam de um ouvido ao outro (Panning)|Buscar: 'deep horror ambient no melody'|
|Z5 — Hadal|Silêncio cortado por pulsos graves rítmicos. Outros tons não-musicais|Volume 0.25. Sons de 'presença'. Não é música — é atmosfera|Buscar: 'hadal zone horror soundscape'|
|Base|Contraste total: mecânico suave, quase doméstico. Computadores, ventiladores|Volume 0.4. Sem tensão. O alívio sonoro da base é intencional|Buscar: 'submarine interior ambient hum'|
|Evento|Música de evento específica (5 variações) — urgente, percussão forte|Inicia em 0.5s ao disparar o evento. Loop até evento acabar|Buscar: 'underwater action intense'|

## **6.3 Sons de Ambiente Contínuos**
Estes sons ficam ativos o tempo todo e criam a camada base da imersão. São Sound objects com Looped = true dentro do personagem ou em partes do mundo:

|**Som**|**Localização do objeto Sound**|**Volume**|**Comportamento**|
| :- | :- | :- | :- |
|Água ambiente (bolhas/fluxo)|Part invisível no centro de cada zona|0\.4|Sempre ativo. Pitch varia levemente por profundidade (Roblox PitchShiftSoundEffect)|
|Rangido de pressão|HumanoidRootPart do personagem (LocalScript)|0\.0|Volume aumenta de 0 a 0.7 conforme profundidade. Pitch diminui|
|Zumbido elétrico da base|Part central de cada módulo de base|0\.3|Ativo apenas quando módulo de energia ligado. PitchShiftSoundEffect leve|
|Corrente de chaminé|Part da chaminé hidrotérmica|0\.5|MaxDistance: 100 studs. RollOffMode: Inverse (atenua com distância)|
|Batimento cardíaco|HumanoidRootPart do personagem (LocalScript)|0\.0|Volume 0→0.8 quando O₂ < 20%. Pitch aumenta conforme O₂ cai|
|Vento subaquático (correntes)|Beam de corrente + Part invisível associada|0\.25|Ativo apenas em zonas com correntes. Direional (panning)|

## **6.4 SFX Pontuais (Efeitos Sonoros)**
Sons disparados via script em momentos específicos. Todos devem ser curtos (< 3 segundos) e precisos:

|**Evento / Ação**|**Som**|**Quem dispara**|**Canal**|
| :- | :- | :- | :- |
|Coletar recurso|Borbulha satisfatória + clique|LocalScript ao coletar|SFX|
|Abrir inventário|Click mecânico suave|LocalScript (UI)|UI|
|Crafting concluído|Dois tons ascendentes (ding ding)|LocalScript ao receber item|SFX|
|Construir módulo de base|Série de cliques metálicos + confirmar|LocalScript ao finalizar|SFX|
|Receber dano físico|Golpe surdo + bolha distorcida|LocalScript ao levar dano|Player|
|Dano de pressão|Rangido metálico forte do traje|LocalScript a cada tick|Player|
|Alarme de O₂ (<15%)|Bipe eletrônico intermitente (2 por seg)|LocalScript ao cruzar 15%|Player|
|Morte do jogador|Silêncio crescente + pulso de baixo final|LocalScript ao morrer|Player|
|Criatura detectada|Som único da criatura (ver tabela abaixo)|Script do servidor|Creature|
|Evento de servidor|Sirene + anúncio de áudio da zona|RemoteEvent → LocalScript|SFX|
|Arpão disparado|Whoosh + cavitação|LocalScript ao usar arpão|SFX|
|Acerto de arpão|Impacto + som da criatura atingida|LocalScript ao colidir|SFX|
|Módulo de base sem energia|Alarme baixo + sistemas desligando|RemoteEvent → LocalScript|SFX|

## **6.5 Assinaturas Sonoras das Criaturas**
Cada criatura tem 3 sons distintos: aproximação (ouvido antes de ver), agressão (atacando), morte. Isso ensina o jogador a reconhecer pelo som:

|**Criatura**|**Som de aproximação**|**Som de ataque**|**Som de morte**|
| :- | :- | :- | :- |
|Tubarão Caçador|Baixo pulsante rítmico (tipo Jaws, mas sutil)|Rangido + splash|Borbulha pesada descendente|
|Água-Viva Elétrica|Estática elétrica distante (crackle)|Descarga: buzz elétrico forte|Sizzle + borbulha|
|Polvo Abissal|Sussurro invertido + click de tentáculo|Splash violento + grito abafado|Jato de tinta (woosh + borbulha)|
|Leviatã das Profundezas|Vibração de baixo frequência que dura 4 segundos|Rugido distorcido subaquático|Sequência de 8 seg de agonia + silêncio|
|Peixe Lanterna|Clique bioluminescente rítmico|Mordida rápida seca|Clique irregular + som de afundar|
|A Coisa (Z5)|Nenhum — aparece em silêncio (terror)|Som não-natural, não-animal|Sem morte — ela some|

**PANNING DIRECIONAL:** Use SoundService.RespectFilteringEnabled = true e defina RollOffMode = 'Linear' nos Sons de criaturas. Assim o jogador ouve de qual direção a criatura vem — crucial para o gameplay de sobrevivência.


# **7. Script Principal de Atmosfera (AtmosphereController)**
## **7.1 Lógica de Zona Detection**
Este LocalScript monitora a profundidade do personagem e aplica todas as mudanças visuais e sonoras de transição de zona:

-- StarterPlayerScripts > AtmosphereController (LocalScript)

local Players     = game:GetService('Players')

local RunService  = game:GetService('RunService')

local TweenService= game:GetService('TweenService')

local Lighting    = game:GetService('Lighting')

local SoundService= game:GetService('SoundService')

local player = Players.LocalPlayer

local char   = player.Character or player.CharacterAdded:Wait()

local hrp    = char:WaitForChild('HumanoidRootPart')

local currentZone = 0

local ZONE\_DEPTHS = {0, 400, 1600, 4800, 12000}  -- Y negativos

local ZONE\_CONFIG = {

`  `[1] = { brightness=2.5, density=0.35, haze=1.5, atmoColor=Color3.fromRGB(0,120,200) },

`  `[2] = { brightness=1.2, density=0.55, haze=2.5, atmoColor=Color3.fromRGB(0,70,140)  },

`  `[3] = { brightness=0.4, density=0.72, haze=3.5, atmoColor=Color3.fromRGB(0,30,80)   },

`  `[4] = { brightness=0.05,density=0.88, haze=4.5, atmoColor=Color3.fromRGB(0,5,30)    },

`  `[5] = { brightness=0.02,density=0.95, haze=5.0, atmoColor=Color3.fromRGB(30,0,10)   },

}

local function getZone(depth)

`  `for i = #ZONE\_DEPTHS, 1, -1 do

`    `if depth >= ZONE\_DEPTHS[i] then return i end

`  `end

`  `return 1

end

local function applyZone(zone)

`  `if zone == currentZone then return end

`  `currentZone = zone

`  `local cfg = ZONE\_CONFIG[zone]

`  `local ti  = TweenInfo.new(2, Enum.EasingStyle.Sine)

`  `TweenService:Create(Lighting,           ti, {Brightness = cfg.brightness}):Play()

`  `TweenService:Create(Lighting.Atmosphere,ti, {Density = cfg.density, Haze = cfg.haze, Color = cfg.atmoColor}):Play()

`  `-- trocar música aqui (ver MusicController)

`  `-- ajustar lanterna do jogador aqui

end

RunService.Heartbeat:Connect(function()

`  `local depth = math.max(0, -hrp.Position.Y)

`  `applyZone(getZone(depth))

end)

## **7.2 Script de Música Adaptativa**
Complementa o AtmosphereController para trocar músicas suavemente:

-- Dentro do applyZone(), adicionar:

local MusicGroup = SoundService:FindFirstChild('Music')

local trackNames = {'Zone1\_Theme','Zone2\_Theme','Zone3\_Theme','Zone4\_Theme','Zone5\_Theme'}

local function switchMusic(zone)

`  `for \_, sound in pairs(MusicGroup:GetChildren()) do

`    `if sound:IsA('Sound') then

`      `TweenService:Create(sound, TweenInfo.new(2), {Volume = 0}):Play()

`      `task.delay(2, function() sound:Stop() end)

`    `end

`  `end

`  `local newTrack = MusicGroup:FindFirstChild(trackNames[zone])

`  `if newTrack then

`    `newTrack.Volume = 0

`    `newTrack:Play()

`    `TweenService:Create(newTrack, TweenInfo.new(2), {Volume = 0.5}):Play()

`  `end

end


# **8. Checklist Técnico de Produção**
## **8.1 Terreno e Mundo**
- [ ] 5 zonas esculpidas no Terrain Editor com materiais corretos
- [ ] Transições entre zonas com abertura de caverna/fissura (entrada visual clara)
- [ ] Naufrágio inicial (Z1) posicionado e props internos colocados
- [ ] Todos os pontos de interesse de Z1 e Z2 modelados
- [ ] Assets de coral (Z1) com pelo menos 5 variações
- [ ] Fissuras bioluminescentes (Z3) com PointLight
- [ ] Chaminés hidrotérmicas (Z3) com ParticleEmitter
- [ ] Terreno de Z4 e Z5 mais abstrato e monumental
- [ ] Workspace organizado por pastas de zona

## **8.2 Iluminação**
- [ ] Lighting Service configurado (GlobalShadows, Brightness, ClockTime)
- [ ] Atmosphere adicionado ao Lighting com parâmetros de Z1
- [ ] ColorCorrectionEffect no Lighting
- [ ] BlurEffect no Lighting (valor 0 por padrão)
- [ ] DepthOfFieldEffect configurado
- [ ] AtmosphereController LocalScript implementado e testado
- [ ] Lanterna do personagem implementada e desligada em Z1/Z2
- [ ] PointLights em corais e elementos bioluminescentes

## **8.3 Partículas**
- [ ] ParticleEmitter de bolhas ambiente espalhados pela Z1 e Z2
- [ ] ParticleEmitter de neve marinha seguindo jogador em Z3, Z4, Z5
- [ ] ParticleEmitter de respiração no rosto do personagem
- [ ] Efeitos de coleta (burst) testados
- [ ] Efeitos de dano (burst de sangue) testados
- [ ] Partículas de chaminé hidrotérmica (fumaça + fagulha)
- [ ] Efeitos de tela (blur, tint) para estados de O₂ testados

## **8.4 Áudio**
- [ ] SoundGroups criados no SoundService
- [ ] Músicas de todas as 5 zonas + base importadas e testadas em loop
- [ ] MusicController com fade entre zonas funcionando
- [ ] Som de água ambiente em todas as zonas
- [ ] Som de rangido de pressão com volume dinâmico por profundidade
- [ ] Som de batimento cardíaco com intensidade por O₂
- [ ] Alarme de O₂ (<15%) funcionando
- [ ] Sons de respiração do personagem
- [ ] Pelo menos 3 criaturas com sons de aproximação, ataque e morte
- [ ] SFX de coleta, crafting e construção implementados
- [ ] Som de evento de servidor testado


**ABYSS SURVIVAL — Guia Técnico de Produção Visual e Áudio**

*Use este documento junto ao MVP GDD. Ajuste valores testando no Studio.*
Abyss Survival — Produção Visual e Técnica	Documento v1.0
