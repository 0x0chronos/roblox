ABYSS SURVIVAL — Direção de Arte 3D para Blender MCP

🌊

**ABYSS SURVIVAL**

Direção de Arte 3D

*Guia completo para o Blender MCP modelar todos os assets do jogo*

Estilo: Estilizado com profundidade  ·  Fortnite underwater  ·  Sci-fi futurista

|**Decisão de estilo**|**Escolha feita**|**Impacto na modelagem**|
| :- | :- | :- |
|Estilo geral|Estilizado com profundidade (entre cartoon e semi-realista)|Formas limpas com detalhes estratégicos. Proporções levemente exageradas mas não absurdas.|
|Criaturas|Estilizadas mas ainda ameaçadoras — cartoon com personalidade|Olhos maiores que o real, silhuetas icônicas, mas sem perder o fator de medo|
|Base e módulos|Sci-fi futurista: linhas limpas, LEDs, vidro|Geometria precisa, arestas definidas, materiais reflexivos, detalhes de luz emissiva|
|Referência principal|Fortnite (proporções) + Subnautica (atmosfera) + Roblox (acessibilidade)|O jogo deve parecer premium no Roblox, mas nunca fora do lugar na plataforma|


# **1. Filosofia de Arte — O Estilo Abyss**
## **1.1 A Regra dos Três Níveis**
Cada asset do Abyss Survival deve funcionar em três níveis simultaneamente:

|**Nível**|**O que significa**|**Como aplicar na modelagem**|
| :- | :- | :- |
|Silhueta|Reconhecível a 200+ studs de distância|Formas simples e icônicas. O coral deve parecer coral mesmo sem textura. O leviatã deve ser assustador só pela silhueta.|
|Forma|Interessante a 50 studs|Volumes secundários, proporções exageradas estrategicamente, variedade de tamanhos dentro do mesmo asset.|
|Detalhe|Rica a 10 studs|Normal maps, texturas detalhadas, pequenos elementos geométricos que adicionam credibilidade sem peso de polígonos.|

**PRINCÍPIO:** Se a silhueta não funcionar, nenhum detalhe vai salvar o asset. Sempre comece pela silhueta e trabalhe para dentro.

## **1.2 O Equilíbrio Cartoon-Realista**
O estilo do Abyss é "grounded cartoon" — cartoon suficiente para ser lúdico e acessível no Roblox, realista suficiente para criar tensão e imersão. A régua de equilíbrio é:

|**Categoria**|**% Cartoon**|**% Realista**|**Justificativa**|
| :- | :- | :- | :- |
|Corais e plantas|70%|30%|Cores vibrantes, formas exageradas — a Z1 deve ser convidativa e bela|
|Rochas e terreno|40%|60%|Mais realistas para dar peso e credibilidade ao ambiente|
|Criaturas|65%|35%|Personalidade cartoonizada mas silhueta ameaçadora real|
|Base e módulos|20%|80%|Sci-fi limpo e preciso — a base é tecnologia, não fantasia|
|Ruínas e naufrágios|35%|65%|Mais realistas — transmitem história e perigo real|
|Props de interior|40%|60%|Reconhecíveis e funcionais, com toque estilizado|
|Zona 5 (Hadal)|10%|90%|A mais realista de todas — o horror vem da estranheza genuína|

## **1.3 Proporções e Exagero Estratégico**
O exagero de proporções é a ferramenta mais poderosa do cartoon. Use assim:

- Corais: 20-30% mais altos e finos que o real — parecem mais elegantes e alienígenas
- Criaturas: olhos 40% maiores que o real — transmitem personalidade e emoção legíveis
- Tubarão: mandíbula 25% maior, corpo 15% mais robusto — parece mais ameaçador sem perder credibilidade
- Módulos de base: arestas mais definidas e chanfradas que o real — parecem mais "high-tech"
- Rochas: 10% mais angulares que o real — parecem mais estilizadas sem parecer fake
- Ruínas: escala ligeiramente monumental (10% maior) — transmitem grandiosidade e mistério

**NUNCA:** Exagere proporções de forma inconsistente. Se o coral é 20% mais alto, todos os corais devem ser 20% mais altos. Consistência é o que cria identidade visual.


# **2. Técnicas de Modelagem no Blender MCP**
## **2.1 Técnica de Cartoon Shading — Cel Look**
Para alcançar o estilo "grounded cartoon" sem usar Shader complexo (o Roblox não suporta Toon Shaders nativos), a estilização deve vir da GEOMETRIA e das TEXTURAS, não do shader.

### **Método de Arestas Cartoon (Bevel Estratégico)**
Em vez de arestas afiadas (realista) ou arestas muito suaves (foam toy), use bevel moderado e seletivo:

\# Para cada asset, aplicar Bevel com estas configurações:

\# Assets orgânicos (coral, alga, criatura):

Bevel Modifier:

`  `Amount: 0.02–0.05 (relativo ao tamanho do objeto)

`  `Segments: 2

`  `Profile: 0.7 (ligeiramente convexo)

`  `Limit Method: Angle (30 graus)

\# Assets tecnológicos (módulo de base, submarino):

Bevel Modifier:

`  `Amount: 0.01–0.03

`  `Segments: 1

`  `Profile: 0.5 (chanfro reto)

`  `Limit Method: Angle (45 graus)

\# Rochas e ruínas:

Bevel Modifier:

`  `Amount: 0.03–0.08 (variado)

`  `Segments: 1

`  `Profile: 0.3 (levemente côncavo)

`  `Limit Method: Angle (25 graus)

### **Método de Subdivisão para Organicidade**
Assets orgânicos (corais, criaturas, algas) devem parecer suaves mas não blobby:

\# Fluxo de trabalho para assets orgânicos:

1\. Modelar em baixo poly (forma base blocky)

2\. Adicionar Subdivision Surface (level 1 ou 2)

3\. Usar Edge Creases (Shift+E) para manter arestas importantes

`   `Crease 1.0 = aresta afiada mesmo com subdivisão

`   `Crease 0.5 = aresta semi-suave

`   `Crease 0.0 = totalmente suavizada pela subdivisão

4\. Apply Subdivision antes de exportar

5\. Verificar polycount — se passou do limite, usar Decimate

\# Valores de crease por tipo de aresta:

\- Aresta de silhueta principal: 0.8

\- Aresta de volume secundário: 0.5

\- Aresta de detalhe suave: 0.0–0.2

### **Método de Noise para Organicidade (rochas, terreno)**
\# Para rochas e superfícies naturais:

1\. Criar forma base (cubo ou icosphere deformado)

2\. Adicionar Modifier: Displace

`   `Texture: Clouds

`   `Size: 0.8 (rochas pequenas) até 2.0 (rochas grandes)

`   `Strength: 0.05–0.15 (relativo ao tamanho)

3\. Subdivide antes do Displace (mínimo 3 levels de subdivisão)

4\. Apply tudo antes de exportar

\# Para fissuras e fendas naturais:

\# Use Boolean Modifier com cilindros finos

\# rotacionados aleatoriamente para criar rachadura orgânica

## **2.2 Técnica de Textura Cartoon — Painterly PBR**
As texturas devem parecer pintadas à mão mas com profundidade PBR. O segredo é no processo de pintura do albedo:

### **Regras de Pintura do Albedo**
- Sombra falsa pintada: adicione uma camada escura (multiply 0.3) nas cavidades e frestas — simula iluminação mesmo em ambientes escuros
- Highlight pintado: adicione uma camada clara (add 0.2) nas arestas mais expostas — dá a sensação de volume cartoon
- Variação de cor: nunca use cor sólida. Adicione noise sutil (5-10% de variação) em toda a superfície — faz parecer pintado à mão
- Saturação alta nas zonas coloridas (Z1, Z2): 1.2–1.4x a saturação natural — cores mais vibrantes que o real
- Saturação baixa nas zonas profundas (Z3, Z4, Z5): 0.3–0.6x — dessatura progressivamente com a profundidade

### **Roughness Cartoon**
No estilo grounded cartoon, a roughness é menos gradual e mais contrastada que o realismo:

|**Superfície**|**Roughness real**|**Roughness cartoon (Abyss)**|**Efeito visual**|
| :- | :- | :- | :- |
|Metal limpo|0\.2|0\.15|Mais reflexivo — parece mais hi-tech|
|Metal sujo/enferrujado|0\.7|0\.85|Mais fosco — contraste dramático com metal limpo|
|Coral|0\.6|0\.75|Mais fosco — evita brilho plástico|
|Cristal|0\.1|0\.05|Extremamente reflexivo — bioluminescência aparece mais|
|Rocha seca|0\.9|0\.95|Quase completamente fosco — peso e solidez|
|Rocha molhada|0\.4|0\.25|Mais reflexiva — transmite umidade sem shader especial|
|Pele de criatura|0\.6|0\.7|Ligeiramente mais fosca que o real — evita aspecto úmido demais|


# **3. Direção de Arte por Categoria de Asset**
## **3.1 Corais — Zona 1**
Os corais são a primeira impressão do jogo. Devem ser imediatamente belos e únicos. O jogador deve querer explorar só para ver mais deles.

|**Elemento**|**Direção cartoon**|**Como implementar no Blender**|
| :- | :- | :- |
|Forma geral|Elegante, ascendente, orgânico — como esculturas naturais|Curves convertidas para mesh. Nunca modelar coral como cilindros empilhados.|
|Proporção|20% mais alto e fino que o real|Scale Y 1.2 após modelar na proporção real|
|Arestas|Suaves e orgânicas — sem arestas afiadas|Subdivision Surface level 2 + creases 0.3 nas principais ramificações|
|Pontas|Levemente arredondadas — não pontiagudas|Icosphere achatado 0.3 nas pontas de cada ramo|
|Superfície|Textura de pequenos nódulos — como pele de laranja|Displace modifier com textura Clouds, Size 0.3, Strength 0.03|
|Cor|Vibrante, quente, oversaturada 1.3x|Albedo: saturação aumentada em pós-processamento no Blender|
|Bioluminescência Z2|Pontas dos ramos emitem luz azul-cyan|Emissive map apenas nas pontas — resto sem emissive|

## **3.2 Rochas — Todas as Zonas**

|**Zona**|**Caráter visual**|**Técnica Blender**|**Cores**|
| :- | :- | :- | :- |
|Z1 — Costeira|Redondas, desgastadas pela água, cobertas de vida|Icosphere + Displace + algas via particle system|Bege claro (220,200,160) com patches de verde|
|Z2 — Recife|Mais angulares, basálticas, algumas cobertas de lodo|Box com Bevel menor + Displace menos suave|Azul-escuro (35,40,55) com manchas esverdeadas|
|Z3 — Abyss Raso|Angulares, escuras, sem vida aparente, fissuras emissivas|Box com cortes geométricos via Boolean|Quase preto (15,20,30) com frestas cyan|
|Z4 — Abyss Profundo|Monumentais, negras, parecem artificialmente colocadas|Formas mais geométricas e menos orgânicas|Preto absoluto (8,8,12)|
|Z5 — Hadal|Alienígenas, geometria não-natural, cristalinas|Formas que não existem na natureza — prismas irregulares|Preto com reflexo violeta (10,5,15)|

## **3.3 Criaturas — Estilizadas mas Ameaçadoras**
A chave para criaturas "cartoon com personalidade" é a leitura emocional imediata. O jogador deve entender a personalidade da criatura nos primeiros 3 segundos.

|**Criatura**|**Personalidade**|**Exagero de proporção**|**Expressão facial**|**Silhueta icônica**|
| :- | :- | :- | :- | :- |
|Tubarão Caçador|Determinado, implacável, focado|Mandíbula 30% maior, corpo 15% mais robusto, cauda mais longa|Olhos negros e vazios — sem expressão — mais assustador que raiva óbvia|Triângulo agressivo de cima para baixo|
|Água-Viva Elétrica|Alienígena, indiferente, perigosa por natureza|Dome 40% maior que real, tentáculos 50% mais longos e finos|Sem face — a indiferença é o horror|Círculo com raios descendentes|
|Polvo Abissal|Inteligente, calculista, paciente|Olhos 50% maiores — transmitem inteligência, cabeça 20% maior|Olhos amarelos que se movem independentemente — parecem estar avaliando|Massa central com tentáculos que se curvam para baixo como garra|
|Leviatã|Antigo, imenso, indiferente à existência humana|Cabeça 40% maior em relação ao corpo, olhos 60% maiores (mas parecem pequenos no rosto enorme)|4 olhos que emitem luz verde — expressão permanente de fome ancestral|Serpente com cabeça triangular enorme — ocupa toda a tela|
|Peixe Lanterna|Voraz, surpresa, emboscada|Boca 60% do tamanho do corpo, dentes longos e transparentes, olhos pequenos acima da boca|A boca enorme É a expressão — surpresa constante com a própria voracidade|Boca aberta em frente, corpo pequeno atrás|
|A Coisa|Incompreensível, errada, não deve existir|Sem proporção definida — cada parte do corpo está no tamanho errado|Sem face — sem olhos — ausência total de expressão|Amorfa — nunca lembra nada familiar|

**TÉCNICA PARA CRIATURAS:** Para transmitir ameaça em estilo cartoon, use "silhueta negativa" — a criatura deve ter partes que bloqueiam a visão do jogador estrategicamente. O Leviatã deve bloquear 70% da tela quando está perto. O Tubarão deve sempre aparecer pelo ângulo mais intimidador.

## **3.4 Base e Módulos — Sci-fi Futurista**
A base é o único lugar seguro do jogo. O visual deve comunicar "tecnologia confiável" imediatamente — o jogador deve sentir alívio ao entrar.

|**Elemento**|**Direção visual**|**Como implementar**|
| :- | :- | :- |
|Forma geral|Octagonal ou hexagonal — nunca cubos simples|Boolean union de formas geométricas. Chanfros em todas as arestas expostas.|
|Material externo|Metal escuro com coating reflexivo azul-petróleo|Albedo (20,30,45), Roughness 0.3, Metallic 0.8|
|LEDs e painéis|Listras emissivas azul-ciano nos painéis e junções|Emissive map nas bordas dos painéis: cor (0,180,255), intensidade forte|
|Janelas|Vidro levemente tingido de azul, reflexivo|MeshPart separado, Transparency 0.3, SurfaceAppearance com roughness 0.05|
|Junções entre módulos|Encaixe visível — como lego de alta tecnologia|Chanfro de 45° nas bordas de encaixe. Detalhe de parafusos esculpido no normal map.|
|Proporções|Ligeiramente maiores que o real — transmite solidez|Scale 1.1 em relação ao tamanho "normal" de um módulo habitável|
|Detalhe de superfície|Painéis, alças, entradas de ventilação, antenas pequenas|Normal map com detalhes de parafusos, bordas de acesso, selos de pressão|

## **3.5 Naufrágios e Ruínas — História Visual**
Naufrágios e ruínas contam história sem texto. Cada dano deve parecer ter uma causa. O jogador deve querer investigar.

- Danos do submarino: amassados grandes (impacto), buracos rasgados para fora (explosão interna), placas dobradas para fora (pressão). NUNCA danos simétricos — parece fake.
- Cor de enferrujamento: ferrugem ativa (laranja-vermelho) nas bordas dos buracos, ferrugem passiva (marrom-escuro) nas superfícies planas, metal exposto (cinza metálico) nas arestas recentes.
- Ruínas da Z3: a pedra deve parecer mais velha que a civilização humana. Use erosão arredondada nas arestas — não angular. Cobertura de sedimento marinho de 20-30% das superfícies.
- Símbolos nas ruínas: geométricos, não alfanuméricos. Círculos, triângulos e linhas. Esculpidos no normal map — não texturas coladas.


# **4. Paleta de Cores por Zona — Guia para o Blender MCP**
## **4.1 Zona 1 — Zona Costeira: Paraíso Tropical**
A Z1 deve ser a zona mais colorida e vibrante do jogo. O objetivo é que o jogador pense "que lugar bonito" antes de perceber o perigo.

|**Elemento**|**Cor base (RGB)**|**Variação secundária**|**Saturação**|**Nota**|
| :- | :- | :- | :- | :- |
|Areia do fundo|(220,200,160)|(235,215,170) a (200,180,145)|Normal|Ondulações sutis pintadas no albedo|
|Coral laranja|(255,120,60)|Gradiente para (255,200,150) nas pontas|1\.3x|Ponta mais clara — efeito de luz passando|
|Coral rosa-magenta|(230,80,140)|Gradiente para (255,150,180) nas pontas|1\.3x||
|Coral roxo|(150,60,200)|Gradiente para (200,120,255) nas pontas|1\.2x||
|Coral amarelo-verde|(200,220,60)|Gradiente para (240,255,150) nas pontas|1\.2x||
|Alga verde|(50,160,60)|(80,200,80) nas bordas iluminadas|1\.1x|Alpha nas bordas para transparência|
|Rocha calcária|(180,170,150)|Patches de (130,160,100) onde há algas|0\.8x|Menos saturada que o coral — não compete|
|Metal do naufrágio|(70,45,25)|Ferrugem: (160,80,20)|0\.9x|Contraste dramático com o coral colorido|

## **4.2 Zona 2 — Recife Profundo: Beleza Inquietante**

|**Elemento**|**Cor base (RGB)**|**Emissive (se aplicável)**|**Nota**|
| :- | :- | :- | :- |
|Basalto|(35,40,55)|Nenhum|Azul-escuro — água tingindo a percepção|
|Lodo|(25,40,30)|Nenhum|Verde-musgo escuro|
|Coral bioluminescente|(15,50,100)|(0,180,255) — moderado|O emissive contrasta com o albedo escuro|
|Anemôna|(150,40,80)|(60,0,40) — fraquíssimo|Roxo-magenta — beleza perigosa|
|Metal da estação|(50,65,58)|Nenhum|Verde-cinza envelhecido|
|Vidro da estação|(100,140,180)|(0,60,120) — fraquíssimo|Translúcido azulado|

## **4.3 Zona 3 — Abyss Raso: Profundidade Alienígena**

|**Elemento**|**Cor base (RGB)**|**Emissive**|**Intensidade emissive**|
| :- | :- | :- | :- |
|Lama abissal|(18,22,32)|Nenhum|—|
|Basalto Z3|(12,15,25)|Nenhum|—|
|Fissura bioluminescente|(5,15,20)|(0,255,120)|Muito forte — fonte de luz principal|
|Cristal azul|(8,50,70)|(0,200,255)|Forte|
|Chaminé (fendas)|(25,12,5)|(200,80,0)|Moderado — brilho de lava distante|
|Vegetação mutante|(80,20,100)|(40,0,60)|Fraquíssimo — quase imperceptível|

## **4.4 Zonas 4 e 5 — Horror Cromático**
Nas zonas mais profundas, a quase ausência de cor É a direção de arte. O jogador sente a profundidade pelo que não vê.

|**Zona**|**Paleta**|**Única cor presente**|**Efeito psicológico**|
| :- | :- | :- | :- |
|Z4 — Abyss Profundo|Preto (5,5,8) dominante|Verde (0,200,60) dos olhos do Leviatã|O verde parece ameaçador porque é a única coisa visível|
|Z5 — Hadal|Preto absoluto (2,2,3) + magma|Laranja-vermelho (255,60,0) do magma|O calor parece errado no fundo do oceano — desorientação|


# **5. Prompts Prontos para o Blender MCP**
Cole estes prompts diretamente no Claude Code para cada categoria de asset. Eles incorporam todas as direções de arte deste documento.

## **5.1 Prompt Base — Coral Z1**
Modele um coral para o jogo Abyss Survival no Blender.

ESTILO: Grounded cartoon — entre Fortnite e Subnautica.

Silhueta elegante e ascendente. 20% mais alto que o real.

GEOMETRIA:

\- Comece com uma curva Bezier ascendente como espinha dorsal

\- Converta para mesh e adicione ramos secundários

\- Subdivision Surface level 2 com Edge Creases 0.7 nas

`  `principais ramificações para manter forma com suavidade

\- Pontas: Icosphere achatado (Scale Z 0.4) soldado nas extremidades

\- Displace Modifier: Clouds, Size 0.3, Strength 0.04 para

`  `textura de nódulos na superfície

\- Bevel Modifier: Amount 0.03, Segments 2, Profile 0.7

PROPORÇÃO: 320 x 480 x 320 Blender units

POLYCOUNT: máximo 1000 triângulos após apply de todos os modifiers

TEXTURA (bake após modelar):

\- Albedo 1024x1024: Cor base (255,120,60), gradiente para

`  `(255,200,150) nas pontas. Saturação 1.3x. Sombra falsa

`  `pintada nas cavidades (multiply 0.3 escuro).

\- Normal 1024x1024: Bake do high poly (subdivisão level 4)

\- Roughness 512x512: 0.75 na maior parte, 0.5 nas pontas

EXPORT: abyss\_z1\_coral\_01.fbx

Scale 0.01, Forward -Z, Up Y, Triangulate YES

## **5.2 Prompt Base — Módulo de Base Sci-fi**
Modele um módulo de base subaquática sci-fi para Abyss Survival.

ESTILO: Sci-fi futurista — linhas limpas, tecnologia confiável.

O jogador deve sentir segurança e proteção ao olhar para ele.

GEOMETRIA:

\- Forma base: octágono extrudado (não cubo — octágono)

\- Chanfro em TODAS as arestas externas: Bevel 0.02, Segments 1

\- Painéis na superfície: rebaixos de 0.015 units criando

`  `divisões retangulares na face principal

\- Janelas: buracos retangulares com borda chanfrada

`  `(MeshPart separado para o vidro)

\- Detalhe de junção: chanfro de 45° nas bordas de encaixe

\- LEDs: extrude muito fino (0.005 units) nas bordas dos painéis

`  `— serão o emissive channel

PROPORÇÃO: 800 x 800 x 800 Blender units

POLYCOUNT: máximo 700 triângulos

MATERIAL (para referência de bake):

\- Albedo: (20,30,45) metal escuro azul-petróleo

`  `Roughness: 0.3 (moderadamente reflexivo)

`  `Metallic: 0.8

\- LEDs/Emissive: (0,180,255) azul-ciano brilhante

`  `Apenas nas extrusões finas das bordas dos painéis

EXPORT: abyss\_base\_module\_core.fbx + abyss\_base\_module\_core\_windows.fbx

Scale 0.01, Forward -Z, Up Y, Triangulate YES

## **5.3 Prompt Base — Criatura Estilizada**
Modele o Tubarão Caçador para Abyss Survival.

ESTILO: Cartoon ameaçador — grande, determinado, implacável.

Deve assustar sem parecer caricato.

PROPORÇÕES EXAGERADAS (intencionais):

\- Mandíbula: 30% maior que um tubarão branco real

\- Corpo: 15% mais robusto (mais musculoso)

\- Cauda: 20% mais longa — transmite velocidade

\- Olhos: negros, sem íris visível, tamanho real (não aumentar)

`  `O horror está na ausência de expressão, não no tamanho

\- 5 fendas branquiais claramente visíveis e geométricas

GEOMETRIA:

\- Box modeling → Subdivision Surface level 2

\- Edge Creases 0.8 nas fendas branquiais (manter definição)

\- Edge Creases 0.6 na linha lateral do corpo

\- Boca: modelar semi-aberta (15 graus) para ver dentes

\- Dentes: prismas triangulares, 3 fileiras, tamanhos variados

\- RIG: spine (5 bones), tail (2 bones), jaw (1 bone), fins (4 bones)

PROPORÇÃO: 800 x 600 x 2400 Blender units (24 studs de comprimento)

POLYCOUNT: máximo 1400 triângulos

COR:

\- Dorso: (55,65,85) azul-cinza escuro

\- Ventre: (200,195,185) quase branco-sujo

\- Gradiente suave entre dorso e ventre na lateral

\- Roughness: 0.65 (pele levemente reflexiva quando molhada)

EXPORT: abyss\_creature\_shark.fbx (com armature)

Scale 0.01, Forward -Z, Up Y, Triangulate YES

Add Leaf Bones: NO


# **6. Checklist de Qualidade Visual por Asset**
Antes de exportar qualquer asset, verificar todos os itens:

## **6.1 Checklist de Forma**
- [ ] A silhueta é reconhecível sem textura?
- [ ] As proporções seguem os exageros especificados para a categoria?
- [ ] O Bevel está aplicado corretamente (orgânico vs tecnológico)?
- [ ] Não há arestas não-intencionalmente afiadas?
- [ ] O asset parece parte do mesmo universo visual dos outros?
- [ ] Se criatura: a personalidade é legível em 3 segundos?
- [ ] Se módulo de base: transmite tecnologia e segurança?

## **6.2 Checklist de Textura**
- [ ] O albedo tem variação de cor (não é sólido)?
- [ ] A sombra falsa está pintada nas cavidades?
- [ ] O highlight está pintado nas arestas expostas?
- [ ] A saturação está correta para a zona (alta Z1, baixa Z4-Z5)?
- [ ] O normal map tem detalhe suficiente para justificar o polycount baixo?
- [ ] O roughness está no valor correto para a categoria?
- [ ] Se bioluminescente: o emissive está só nas áreas corretas?

## **6.3 Checklist de Estilo**
- [ ] O asset parece "Fortnite underwater" (não muito realista, não muito brinquedo)?
- [ ] Se Z1: é imediatamente belo e convidativo?
- [ ] Se Z3-Z5: transmite opressão e profundidade?
- [ ] Se criatura: assusta sem parecer caricata?
- [ ] Se base: transmite segurança e tecnologia?
- [ ] O asset vai parecer consistente ao lado dos outros no jogo?


**ABYSS SURVIVAL — Direção de Arte 3D v1.0**

*Este documento deve ser lido pelo Blender MCP antes de modelar qualquer asset.*
Abyss Survival — Art Direction v1.0   |   Blender MCP + Roblox MCP
