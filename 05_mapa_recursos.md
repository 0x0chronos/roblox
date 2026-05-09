🌊

**ABYSS SURVIVAL**

Mapa de Calor de Recursos

*Densidade · Posicionamento Estratégico · Guia de Exploração Natural*

**Princípio de Design de Recursos**

Recursos não devem ser posicionados aleatoriamente. Cada recurso tem uma função narrativa e de gameplay: guiar o jogador, recompensar exploração e criar decisões de risco vs recompensa.

> **REGRA DE OURO:** O jogador nunca deve precisar voltar a uma zona anterior para progredir. Cada zona tem exatamente os recursos necessários para avançar para a próxima.

**Zona 1 --- Zona Costeira**

**Densidade e distribuição**

| **Recurso**            | **Quantidade no mapa** | **Tipo de spawn**       | **Posicionamento estratégico**                                            |
|------------------------|------------------------|-------------------------|---------------------------------------------------------------------------|
| Algas Nutritivas       | 30--40 nós             | Clusters de 3--5 juntos | Perto do sub de spawn e ao longo do caminho natural de exploração         |
| Sucata de Naufrágio    | 20--25 nós             | Espalhados no naufrágio | Dentro e ao redor do sub avariado --- obriga o jogador a explorar o spawn |
| Calcário               | 25--30 nós             | Singulares nas rochas   | Na borda das rochas do terreno --- visíveis mas requerem aproximação      |
| Ferro Simples          | 10--15 nós             | Singulares em fendas    | Em fendas de rocha mais escuras --- recompensa exploração além do óbvio   |
| Esporo Bioluminescente | 4--6 nós               | Singulares, brilhantes  | Em locais levemente ocultos --- ativa curiosidade do jogador              |

**Pontos Garantidos (fixed spawns)**

- 5 Algas dentro ou ao lado do sub de spawn --- garantia de tutorial funcionar

- 3 Sucatas dentro do sub avariado --- tutorial de crafting não pode falhar

- 2 Calcários na plataforma de base predefinida --- jogador sempre pode construir Casco

**Pontos Aleatórios (procedural dentro de zona)**

- Resto dos recursos randomizados dentro das boundaries da zona a cada servidor

- Respeitam distância mínima de 8 studs entre nós --- evita clusters irreais

- Respeitam distância mínima de 20 studs de qualquer criatura agressiva

**Zona 2 --- Recife Profundo**

| **Recurso**            | **Quantidade** | **Tipo de spawn**              | **Posicionamento**                                          |
|------------------------|----------------|--------------------------------|-------------------------------------------------------------|
| Cristal Marinho        | 20--25 nós     | Clusters de 2--3 nas rochas    | Em formações de rocha bioluminescente --- visualmente óbvio |
| Ferro Abissal          | 12--15 nós     | Singulares em fendas profundas | Nas partes mais escuras da zona --- recompensa ir fundo     |
| Esporo Bioluminescente | 8--10 nós      | Clusters                       | Em corredores entre rochas --- guia o caminho para Z3       |
| Algas Raras            | 6--8 nós       | Singulares                     | Dentro de cavernas --- recompensa curiosidade               |
| Sucata Eletrônica      | 4--5 nós       | Na Estação Abandonada          | Concentrados no ponto de interesse --- motivo para visitar  |

**Posicionamento Narrativo Z2**

- Cristais Marinhos estão no caminho entre o sub de spawn e a entrada da Z3 --- o jogador os encontra naturalmente

- A Estação Abandonada é o único local com Sucata Eletrônica --- força visita ao ponto de interesse de lore

- Ferro Abissal concentrado perto da entrada da Z3 --- último recurso antes de mergulhar

**Zona 3 --- Abyss Raso**

| **Recurso**                | **Quantidade** | **Posicionamento**                     | **Por que aqui**                                   |
|----------------------------|----------------|----------------------------------------|----------------------------------------------------|
| Titânio das Profundezas    | 15--18 nós     | Nas paredes e teto de cavernas         | Requer exploração ativa --- não está no chão óbvio |
| Gel Bioluminescente        | 10--12 nós     | Ao redor das chaminés hidrotérmicas    | Concentrado em pontos de interesse específicos     |
| Núcleo Térmico Menor       | 6--8 nós       | Dentro das chaminés (coleta cuidadosa) | Alta recompensa, alta dificuldade de coleta        |
| Fragmento de Cristal Hadal | 3--4 nós       | Nas ruínas misteriosas                 | Preview de Z4 --- cria vontade de ir mais fundo    |

**Zona 4 --- Abyss Profundo**

| **Recurso**            | **Quantidade**          | **Posicionamento**              | **Nota de design**                                                    |
|------------------------|-------------------------|---------------------------------|-----------------------------------------------------------------------|
| Núcleo Térmico         | 8--10 nós               | Em torno da Caldeira Central    | Principal razão para visitar Z4 além do lore                          |
| Shard Hadal            | 5--6 nós                | Nas paredes do canyon principal | Visíveis de longe pela bioluminescência --- isca                      |
| Obsidiana Abissal      | 4--5 nós                | Nas ruínas do navio de pesquisa | Ligados ao lore --- recompensa ler o fragmento que revela localização |
| Drop do Leviatã (boss) | 1 garantido ao derrotar | Corpo do Leviatã                | Único recurso drop de criatura no MVP                                 |

**Zona 5 --- Hadal**

| **Recurso**           | **Quantidade** | **Posicionamento**        | **Raridade**                              |
|-----------------------|----------------|---------------------------|-------------------------------------------|
| Shard Hadal Puro      | 3--4 nós       | No Altar Abissal          | Épico --- usado apenas para traje endgame |
| Cristal Abissal Negro | 2--3 nós       | Nas formações alienígenas | Épico --- cosmético funcional para base   |
| Relíquia do Fundo     | 1 por servidor | A Fissura (local final)   | Único --- item de prestígio máximo        |

**Script ResourceManager --- Spawn e Respawn**

> \-- ServerScriptService/Modules/ResourceManager.lua
>
> local Config = require(script.Parent.Config)
>
> local ResourceManager = {}
>
> local activeNodes = {} \-- {nodeId: {part, type, cooldownUntil}}
>
> function ResourceManager:init()
>
> \-- carregar todos os Parts com tag \"ResourceNode\" do Workspace
>
> for \_, part in pairs(workspace.Resources:GetDescendants()) do
>
> if part:IsA(\"BasePart\") and part:GetAttribute(\"ResourceType\") then
>
> activeNodes\[part\] = {
>
> part = part,
>
> rtype = part:GetAttribute(\"ResourceType\"),
>
> amount = part:GetAttribute(\"Amount\") or 1,
>
> available = true,
>
> }
>
> end
>
> end
>
> end
>
> function ResourceManager:Collect(player, data)
>
> local node = activeNodes\[data.nodeRef\]
>
> if not node or not node.available then return end
>
> \-- desativar nó
>
> node.available = false
>
> node.part.Transparency = 1
>
> node.part.CanCollide = false
>
> \-- adicionar ao inventário do jogador (via DataStore module)
>
> \-- \...
>
> \-- reagendar respawn
>
> local respawnTime = math.random(
>
> Config.Resources.RespawnTime.min,
>
> Config.Resources.RespawnTime.max
>
> )
>
> task.delay(respawnTime, function()
>
> node.available = true
>
> node.part.Transparency = 0
>
> node.part.CanCollide = true
>
> end)
>
> end
>
> return ResourceManager

**Como Posicionar no Studio --- Passo a Passo**

1.  Crie uma pasta \"Resources\" dentro da pasta da zona (ex: Zone1_Coastal/Resources)

2.  Para cada nó de recurso: adicione uma Part esférica pequena (radius 1.5 studs)

3.  Defina os Attributes da Part: ResourceType (string) e Amount (number)

4.  Use um color coding para visualizar no Studio: Verde=comum, Azul=incomum, Roxo=raro, Laranja=épico

5.  Fixed spawns: marque com Attribute \"Fixed = true\" --- nunca respawnam em posição diferente

6.  Procedural spawns: marque com Attribute \"Procedural = true\" --- posição varia por servidor

7.  Para testar densidade: entre no Play e verifique se consegue Tier 1 em 15--20 minutos

**Checklist de Posicionamento**

- \[ \] Zona 1: 5 Algas e 3 Sucatas fixas no ponto de spawn

- \[ \] Zona 1: Caminho natural de exploração passa por recursos suficientes para Tier 0

- \[ \] Zona 2: Cristais Marinhos visíveis imediatamente ao entrar na zona

- \[ \] Zona 2: Estação Abandonada tem Sucata Eletrônica exclusiva (motivo para visitar)

- \[ \] Zona 3: Recursos nas chaminés e ruínas --- não no chão

- \[ \] Teste: jogador consegue Tier 1 em 15--20 min sem grinding

- \[ \] Teste: nenhuma zona requer recursos de zona anterior para progredir
