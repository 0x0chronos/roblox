ABYSS SURVIVAL — Guia de Materiais e Texturas PBR

🌊

**ABYSS SURVIVAL**

Guia de Materiais e Texturas PBR

*Albedo · Normal · Roughness · Metallic · Emissive · SurfaceAppearance*


# **PBR no Roblox — Conceitos**
O Roblox usa o modelo de material PBR (Physically Based Rendering) via SurfaceAppearance. Cada asset pode ter até 5 mapas de textura que juntos definem como a luz interage com a superfície.

|**Canal**|**Arquivo**|**Formato**|**O que controla**|
| :- | :- | :- | :- |
|Albedo (Color Map)|\_albedo.png|RGB 8bit|Cor base da superfície sem iluminação|
|Normal Map|\_normal.png|RGB 8bit espaço tangente|Detalhes de relevo sem geometria extra|
|Roughness Map|\_roughness.png|Grayscale 8bit|0=espelho perfeito, 255=totalmente fosco|
|Metallic Map|\_metallic.png|Grayscale 8bit|0=não-metal (dielétrico), 255=metal puro|
|Emissive Map|\_emissive.png|RGB 8bit|Áreas que emitem luz própria (bioluminescência)|

**IMPORTANTE:** O Roblox NÃO usa Specular Map separado. O specular é calculado automaticamente pelo canal Metallic. Não crie specular maps.

# **Paleta de Materiais por Zona**
## **Zona 1 — Zona Costeira**

|**Material**|**Albedo base (RGB)**|**Roughness**|**Metallic**|**Notas**|
| :- | :- | :- | :- | :- |
|Areia do fundo|(220, 200, 160)|0\.9|0\.0|Variação sutil de cor em noise|
|Calcário / rocha clara|(180, 170, 150)|0\.85|0\.0|Detalhes brancos nas arestas|
|Coral laranja-vivo|(255, 120, 60)|0\.7|0\.0|Gradiente para branco na ponta|
|Coral rosa|(230, 100, 130)|0\.7|0\.0|Mesma estrutura, cor diferente|
|Alga verde|(60, 140, 50)|0\.9|0\.0|Translucidez via alpha no albedo|
|Metal enferrujado (sub)|(80, 50, 30)|0\.8|0\.4|Patches de ferrugem via máscara|
|Vidro do sub|(150, 180, 200)|0\.05|0\.0|Transparency 0.7 no Roblox|

## **Zona 2 — Recife Profundo**

|**Material**|**Albedo base (RGB)**|**Roughness**|**Metallic**|**Emissive**|
| :- | :- | :- | :- | :- |
|Basalto úmido|(40, 45, 60)|0\.9|0\.0|Nenhum|
|Lodo do fundo|(30, 50, 40)|0\.95|0\.0|Nenhum|
|Coral Z2 bioluminescente|(20, 80, 120)|0\.6|0\.0|(0, 180, 255) — fraco|
|Metal oxidado (estação)|(60, 80, 70)|0\.75|0\.5|Nenhum|
|Anemôna|(180, 60, 100)|0\.8|0\.0|(80, 0, 40) — muito fraco|

## **Zona 3 — Abyss Raso**

|**Material**|**Albedo base (RGB)**|**Roughness**|**Metallic**|**Emissive**|
| :- | :- | :- | :- | :- |
|Lama abissal|(20, 25, 35)|0\.98|0\.0|Nenhum|
|Basalto Z3|(15, 20, 30)|0\.95|0\.0|Nenhum|
|Cristal Z3|(10, 60, 80)|0\.1|0\.0|(0, 200, 255) — forte|
|Rocha da chaminé|(40, 20, 10)|0\.9|0\.0|(200, 80, 0) — fraco nas fendas|
|Fissura bioluminescente|(0, 20, 30)|0\.3|0\.0|(0, 255, 120) — muito forte|

## **Zonas 4 e 5 — Abyss Profundo e Hadal**

|**Material**|**Albedo base (RGB)**|**Roughness**|**Metallic**|**Emissive**|
| :- | :- | :- | :- | :- |
|Granito negro Z4|(10, 10, 15)|0\.9|0\.0|Nenhum|
|Obsidiana Z5|(5, 5, 8)|0\.15|0\.0|Nenhum|
|Cristal negro Z5|(8, 8, 12)|0\.05|0\.0|Nenhum (fosco escuro)|
|Magma Z5|(30, 10, 0)|0\.6|0\.0|(255, 80, 0) — muito forte|
|Pedra alienígena (altar)|(15, 10, 20)|0\.85|0\.0|(80, 0, 120) — fraquíssimo|

# **Processo de Bake no Blender**
## **Passo a passo para o Blender MCP**
1. Criar material PBR no Principled BSDF com os valores da tabela acima
1. Para o Normal Map: adicionar subdivisão + sculpt de detalhes no high-poly. Bake do high-poly para o low-poly.
1. Criar Image Texture node para cada canal (albedo, normal, roughness) — NÃO conectar ao shader durante o bake
1. Render → Bake → selecionar tipo (Diffuse para albedo, Normal para normal, Roughness para roughness)
1. Exportar cada imagem: Image → Save As → nome correto com sufixo

\# Script Python para automatizar o bake no Blender MCP:

import bpy

def bake\_asset(obj\_name, resolution=1024):

`    `obj = bpy.data.objects[obj\_name]

`    `bpy.context.view\_layer.objects.active = obj

`    `bpy.ops.object.select\_all(action="DESELECT")

`    `obj.select\_set(True)

`    `textures = {

`        `"albedo":    ("DIFFUSE",   resolution, resolution),

`        `"normal":    ("NORMAL",    resolution, resolution),

`        `"roughness": ("ROUGHNESS", resolution//2, resolution//2),

`    `}

`    `for name, (bake\_type, w, h) in textures.items():

`        `img = bpy.data.images.new(f"{obj\_name}\_{name}", w, h)

`        `# Conectar ao nó de imagem do material

`        `mat = obj.data.materials[0]

`        `nodes = mat.node\_tree.nodes

`        `img\_node = nodes.new("ShaderNodeTexImage")

`        `img\_node.image = img

`        `nodes.active = img\_node

`        `bpy.ops.object.bake(type=bake\_type)

`        `img.filepath\_raw = f"/tmp/{obj\_name}\_{name}.png"

`        `img.file\_format = "PNG"

`        `img.save()

`        `nodes.remove(img\_node)

# **SurfaceAppearance no Roblox MCP**
-- Script que o Roblox MCP executa após import do .fbx:

local function applySurfaceAppearance(meshPart, assetName, textureIds)

`  `local sa = Instance.new("SurfaceAppearance")

`  `sa.ColorMap     = textureIds.albedo    or ""

`  `sa.NormalMap    = textureIds.normal    or ""

`  `sa.RoughnessMap = textureIds.roughness or ""

`  `sa.MetalnessMap = textureIds.metallic  or ""

`  `if textureIds.emissive then

`    `-- Emissive via propriedade do meshPart + script de luz separado

`    `meshPart:SetAttribute("HasEmissive", true)

`    `meshPart:SetAttribute("EmissiveColor", textureIds.emissiveColor or "0,255,100")

`  `end

`  `sa.Parent = meshPart

`  `return sa

end

-- Exemplo de uso:

applySurfaceAppearance(

`  `workspace.Zone1\_Coastal.coral\_01,

`  `"abyss\_z1\_coral\_01",

`  `{

`    `albedo    = "rbxassetid://111111111",

`    `normal    = "rbxassetid://222222222",

`    `roughness = "rbxassetid://333333333",

`  `}

)
Abyss Survival — Pipeline Blender + Roblox   v1.0
