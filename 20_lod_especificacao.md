ABYSS SURVIVAL — Especificação de LOD — Level of Detail

🌊

**ABYSS SURVIVAL**

Especificação de LOD — Level of Detail

*LOD0 · LOD1 · LOD2 · Distâncias de Swap · Configuração no Studio*


# **O que é LOD e por que importa**
Level of Detail é o sistema que usa versões mais simples de um asset quando ele está longe do jogador. Sem LOD, um servidor com 12 jogadores em zonas diferentes renderizaria todos os assets em alta qualidade simultaneamente, causando lag.

|**Nível**|**Nome**|**Distância do jogador**|**Polycount alvo**|**Descrição**|
| :- | :- | :- | :- | :- |
|LOD0|Alta qualidade|0–40 studs|100% do poly original|Asset completo com todos os detalhes|
|LOD1|Qualidade média|40–120 studs|40–50% do original|Detalhes menores removidos, silhueta preservada|
|LOD2|Baixa qualidade|120–250 studs|10–15% do original|Silhueta básica apenas|
|Billboard|Sprite 2D|250+ studs|8 tris (2 triângulos)|Textura 2D sempre virada para a câmera|

**ROBLOX:** Use a propriedade LevelOfDetail do MeshPart. Valor "Disabled" = sempre LOD0 (sem otimização). Valor "StreamingMesh" = Roblox gerencia automaticamente. Para controle manual, use modelos separados com suffix \_LOD0/\_LOD1/\_LOD2.

# **LOD por Categoria de Asset**

|**Categoria**|**LOD0**|**LOD1**|**LOD2**|**Billboard?**|**Método**|
| :- | :- | :- | :- | :- | :- |
|Coral pequeno (Z1)|400 tris|180 tris|60 tris|Não|Decimate modifier|
|Coral grande (Z1-Z2)|1\.000 tris|450 tris|120 tris|Sim|Decimate + sprite|
|Rocha pequena|150 tris|60 tris|20 tris|Não|Decimate|
|Rocha grande|500 tris|200 tris|60 tris|Não|Decimate|
|Alga ondulante|150 tris|80 tris|30 tris|Não|Decimate|
|Ruína modular|250 tris|100 tris|30 tris|Não|Decimate|
|Chaminé hidrotérmica|700 tris|300 tris|80 tris|Não|Decimate|
|Cristal|400 tris|160 tris|40 tris|Não|Decimate|
|Módulo de base|600 tris|250 tris|—|Não|LOD1 apenas (sempre perto)|
|Submarino spawn|5\.000 tris|2\.000 tris|500 tris|Não|Retopo manual|
|Criaturas (exceto boss)|1\.200 tris|500 tris|—|Não|LOD1 apenas|
|Leviatã (boss)|4\.000 tris|1\.600 tris|400 tris|Não|Decimate + retopo|

# **Como Gerar LODs no Blender MCP**
## **Usando o modifier Decimate**
\# Script Python para gerar LOD1 e LOD2 automaticamente:

import bpy

def generate\_lods(obj\_name):

`    `original = bpy.data.objects[obj\_name]

`    `original.name = obj\_name + "\_LOD0"

`    `lod\_ratios = {"LOD1": 0.45, "LOD2": 0.12}

`    `for lod\_name, ratio in lod\_ratios.items():

`        `# Duplicar o objeto

`        `bpy.ops.object.select\_all(action="DESELECT")

`        `original.select\_set(True)

`        `bpy.context.view\_layer.objects.active = original

`        `bpy.ops.object.duplicate()

`        `lod\_obj = bpy.context.active\_object

`        `lod\_obj.name = obj\_name + "\_" + lod\_name

`        `# Aplicar Decimate

`        `dec = lod\_obj.modifiers.new("Decimate", "DECIMATE")

`        `dec.ratio = ratio

`        `bpy.ops.object.modifier\_apply(modifier="Decimate")

`        `# Exportar

`        `bpy.ops.export\_scene.fbx(

`            `filepath=f"/tmp/{obj\_name}\_{lod\_name}.fbx",

`            `use\_selection=True,

`            `global\_scale=0.01,

`            `axis\_forward="-Z",

`            `axis\_up="Y",

`            `mesh\_smooth\_type="FACE",

`        `)

`        `print(f"Exportado: {obj\_name}\_{lod\_name}.fbx")

`        `print(f"  Polys: {len(lod\_obj.data.polygons)}")

# **Configuração de LOD no Roblox MCP**
-- Script que o Roblox MCP executa para configurar LOD:

local function setupLOD(parentModel)

`  `-- Busca LOD0, LOD1, LOD2 dentro do Model

`  `local lod0 = parentModel:FindFirstChild(parentModel.Name .. "\_LOD0")

`  `local lod1 = parentModel:FindFirstChild(parentModel.Name .. "\_LOD1")

`  `local lod2 = parentModel:FindFirstChild(parentModel.Name .. "\_LOD2")

`  `-- LOD0: sempre visível perto

`  `if lod0 then

`    `lod0:SetAttribute("LODLevel", 0)

`    `lod0:SetAttribute("LODMaxDist", 40)

`  `end

`  `-- LOD1: visível de 40–120 studs

`  `if lod1 then

`    `lod1:SetAttribute("LODLevel", 1)

`    `lod1:SetAttribute("LODMinDist", 40)

`    `lod1:SetAttribute("LODMaxDist", 120)

`    `lod1.Transparency = 1  -- começa invisível

`  `end

`  `-- LOD2: visível de 120–250 studs

`  `if lod2 then

`    `lod2:SetAttribute("LODLevel", 2)

`    `lod2:SetAttribute("LODMinDist", 120)

`    `lod2:SetAttribute("LODMaxDist", 250)

`    `lod2.Transparency = 1

`  `end

end

-- LODManager (LocalScript) — troca visibilidade baseado em distância

local RunService = game:GetService("RunService")

local camera    = workspace.CurrentCamera

RunService.Heartbeat:Connect(function()

`  `-- Iterar todos os Models com LOD

`  `for \_, model in ipairs(workspace:GetDescendants()) do

`    `if not model:IsA("Model") then continue end

`    `local lod0 = model:FindFirstChild(model.Name.."\_LOD0")

`    `if not lod0 then continue end

`    `local dist = (camera.CFrame.Position - model:GetPivot().Position).Magnitude

`    `local lod1 = model:FindFirstChild(model.Name.."\_LOD1")

`    `local lod2 = model:FindFirstChild(model.Name.."\_LOD2")

`    `lod0.Transparency = dist > 40  and 1 or 0

`    `if lod1 then lod1.Transparency = (dist <= 40 or dist > 120) and 1 or 0 end

`    `if lod2 then lod2.Transparency = (dist <= 120 or dist > 250) and 1 or 0 end

`  `end

end)

**OTIMIZAÇÃO:** O LODManager acima roda para todos os modelos com LOD a cada frame. Em servidores com muitos assets, adicione debounce de 0.1s (10x/s) para reduzir carga. O resultado visual é imperceptível.
Abyss Survival — Pipeline Blender + Roblox   v1.0
