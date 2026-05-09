ABYSS SURVIVAL — Guia do Pipeline Blender + Roblox MCP

🌊

**ABYSS SURVIVAL**

Guia do Pipeline Blender + Roblox MCP

*Configuração · Convenções · Export · Escala · Nomenclatura*


# **Visão Geral do Pipeline**
O Claude Code coordena dois MCPs simultaneamente: o Blender MCP para modelagem 3D e o Roblox MCP para importação e configuração no Studio. Este documento define todas as convenções que ambos devem seguir para que os assets funcionem sem retrabalho.

|**Etapa**|**Ferramenta**|**O que acontece**|**Output**|
| :- | :- | :- | :- |
|1\. Prompt|Claude Code|Descreve o asset: nome, zona, dimensões, polycount, material|Prompt estruturado|
|2\. Modelagem|Blender MCP|Cria geometria, UV unwrap, aplica material básico|Arquivo .blend|
|3\. Bake de texturas|Blender MCP|Gera albedo, normal, roughness em PNG|3× PNG por asset|
|4\. Export|Blender MCP|Exporta .fbx com escala correta e eixos ajustados|arquivo .fbx|
|5\. Import|Roblox MCP|Importa .fbx como MeshPart, configura propriedades|MeshPart no Studio|
|6\. Material|Roblox MCP|Cria SurfaceAppearance com os PNGs de textura|Asset texturizado|
|7\. Posicionamento|Roblox MCP|Posiciona instâncias nas zonas via script|Asset no mundo|

# **Configuração dos MCPs no Claude Code**
## **Blender MCP**
\# Instalar o Blender MCP addon:

\# 1. Abra o Blender → Edit → Preferences → Add-ons → Install

\# 2. Selecione o arquivo blender\_mcp.py do repositório

\# 3. Ative o addon e anote a porta (padrão: 9876)

\# No Claude Code, configurar o MCP server:

\# claude\_code\_config.json

{

`  `"mcpServers": {

`    `"blender": {

`      `"command": "python",

`      `"args": ["-m", "blender\_mcp\_server"],

`      `"env": { "BLENDER\_PORT": "9876" }

`    `},

`    `"roblox": {

`      `"command": "node",

`      `"args": ["roblox\_mcp\_server.js"],

`      `"env": { "STUDIO\_PORT": "29999" }

`    `}

`  `}

}

## **Roblox MCP**
\# Instalar o Roblox MCP plugin no Studio:

\# 1. Baixe o plugin RobloxMCP.rbxmx do repositório

\# 2. No Studio: Plugins → Manage Plugins → Install from file

\# 3. Ative o plugin — ele abre um servidor local na porta 29999

\# 4. Certifique-se que o Studio está aberto com o projeto Abyss

# **Convenções de Nomenclatura**
## **Arquivos de asset**
Padrão obrigatório: [projeto]\_[zona]\_[tipo]\_[variacao].[ext]

|**Exemplo de nome**|**O que significa**|
| :- | :- |
|abyss\_z1\_coral\_01.fbx|Projeto Abyss, Zona 1, tipo coral, variação 01|
|abyss\_z2\_rock\_large.fbx|Zona 2, rocha grande|
|abyss\_z3\_crystal\_blue.fbx|Zona 3, cristal azul|
|abyss\_base\_module\_oxygen.fbx|Módulo de base — oxigênio|
|abyss\_creature\_shark.fbx|Criatura tubarão|
|abyss\_z1\_wreck\_main.fbx|Naufrágio principal da Z1|

## **Arquivos de textura**
Padrão: [nome\_do\_asset]\_[canal].png

|**Canal**|**Sufixo**|**Descrição**|**Tamanho padrão**|
| :- | :- | :- | :- |
|Albedo (cor base)|\_albedo.png|RGB — cor difusa do material|1024×1024|
|Normal Map|\_normal.png|RGB — detalhes de superfície em espaço tangente|1024×1024|
|Roughness|\_roughness.png|Grayscale — 0=brilhante, 1=fosco|512×512|
|Metallic|\_metallic.png|Grayscale — 0=não-metal, 1=metal|512×512|
|Emissive|\_emissive.png|RGB — áreas que emitem luz (só assets bioluminescentes)|512×512|

# **Configurações de Export do Blender**
## **Configurações obrigatórias para .fbx**
\# Blender: File → Export → FBX (.fbx)

\# Configurações que o Blender MCP deve usar em TODOS os exports:

Scale: 0.01

\# Roblox usa studs onde 1 unit Blender = 0.01 stud por padrão.

\# Com Scale 0.01: 100 units Blender = 1 stud.

\# REGRA: modele em Blender com 1 unit = 1 cm,

\#        então 100 units = 1 metro = 8 studs (escala Roblox).

Apply Scalings: FBX Units Scale

Forward: -Z Forward

Up: Y Up

\# Roblox usa Y como eixo vertical — essencial para import correto.

Apply Unit: YES

Apply Transform: YES

\# Garante que rotações e escalas são aplicadas antes do export.

Mesh: Triangulate Faces = YES

\# Roblox só suporta triângulos. Quadfaces causam artefatos.

Armature: Add Leaf Bones = NO

\# Reduz peso do arquivo. Bones de criatura são adicionados pelo Roblox MCP.

## **Escala de referência — assets vs studs**

|**Asset**|**Tamanho no mundo real**|**Tamanho em studs**|**Units no Blender**|
| :- | :- | :- | :- |
|Coral pequeno|40cm × 60cm|3\.2 × 4.8 studs|320 × 480 units|
|Coral grande|80cm × 150cm|6\.4 × 12 studs|640 × 1200 units|
|Rocha média|50cm × 30cm|4 × 2.4 studs|400 × 240 units|
|Módulo de base|1m × 1m × 1m|8 × 8 × 8 studs|800 × 800 × 800 units|
|Submarino spawn|16m × 6m × 5m|128 × 48 × 40 studs|12800 × 4800 × 4000 units|
|Tubarão|3m comprimento|24 studs|2400 units|
|Leviatã|20m comprimento|160 studs|16000 units|

# **Configurações do Roblox MCP pós-import**
## **Propriedades padrão para cada categoria**

|**Categoria de asset**|**CollisionFidelity**|**CastShadow**|**CanCollide**|**Anchored**|
| :- | :- | :- | :- | :- |
|Asset decorativo (coral, rocha, alga)|Box|false|false|true|
|Asset de colisão (chão, parede, plataforma)|PreciseConvexDecomposition|true|true|true|
|Módulo de base|Box|true|true|true|
|Criatura (MeshPart do modelo)|Box|false|true|false|
|Prop de interior (barril, caixa)|Box|false|true|true|
|Naufrágio exterior|Hull|true|true|true|
|Naufrágio interior (navegável)|PreciseConvexDecomposition|false|true|true|

**PERFORMANCE:** CollisionFidelity=Box é o mais leve. Use PreciseConvexDecomposition apenas onde o jogador precisa andar em cima ou colidir de forma precisa. Decorativos sempre Box ou sem colisão.

# **Workflow do Claude Code — Prompt Template**
Para cada asset, o Claude Code deve enviar este prompt estruturado ao Blender MCP:

ASSET: abyss\_z1\_coral\_01

TIPO: Decorativo — Coral Z1

DIMENSOES: 3.2 studs largura × 4.8 studs altura (320 × 480 Blender units)

POLYCOUNT\_ALVO: 800–1200 triângulos

VARIACOES: 1 de 5 (galho grosso ascendente)

GEOMETRIA:

\- Base cilíndrica irregular (radius 60 units, height 80 units)

\- 3 ramos principais saindo da base em ângulos 30–60 graus

\- Pontas levemente arredondadas

\- Subdivide Surface level 1 para suavizar

\- Adicionar noise texture no modifier para irregularidade

UV UNWRAP:

\- Smart UV Project, angle 66 graus, margin 0.02

\- Empacotar ilhas em quadrante 0–1

MATERIAL (apenas para referência de cor — textura será baked):

\- Albedo base: RGB(255, 120, 80) coral-laranja

\- Roughness: 0.7

\- Specular: 0.1

EXPORT:

\- Filename: abyss\_z1\_coral\_01.fbx

\- Scale: 0.01, Forward: -Z, Up: Y

\- Triangulate: YES

BAKE TEXTURES:

\- Albedo: 1024×1024 → abyss\_z1\_coral\_01\_albedo.png

\- Normal: 1024×1024 → abyss\_z1\_coral\_01\_normal.png

\- Roughness: 512×512 → abyss\_z1\_coral\_01\_roughness.png


# **Checklist de Qualidade por Asset**
- [ ] Polycount dentro do limite da categoria
- [ ] Triangulado antes do export
- [ ] Eixos corretos: Y=up, -Z=forward
- [ ] Scale aplicado (não deve ter scale ≠ 1 no FBX)
- [ ] UV sem UV islands sobrepostas
- [ ] UV preenche 80%+ do espaço 0-1
- [ ] Texturas com resolução correta e formato PNG
- [ ] Normal map em espaço tangente (não objeto)
- [ ] Sem vértices duplos (Merge by Distance no Blender)
- [ ] Sem faces internas (Interior Faces checker)
- [ ] Import no Roblox: sem deformações visíveis
- [ ] SurfaceAppearance aplicado e visível no Studio
- [ ] CollisionFidelity correto para a categoria
- [ ] CastShadow desativado se decorativo
Abyss Survival — Pipeline Blender + Roblox   v1.0
