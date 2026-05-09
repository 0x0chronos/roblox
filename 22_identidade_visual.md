ABYSS SURVIVAL  —  Guia de Identidade Visual  |  Roblox Studio

🌊

**ABYSS SURVIVAL**

Guia de Identidade Visual

*Paleta · Tipografia · Ícones · Componentes de UI*


# **Princípios Visuais**
- Coesão: todos os elementos parecem parte do mesmo universo
- Legibilidade: tudo legível em mobile (tela de 5 polegadas, 375px de largura)
- Imersão: a UI não quebra a atmosfera subaquática
- Clareza: o jogador nunca tem dúvida sobre o que um elemento representa

# **Paleta de Cores Oficial**

|**Nome**|**Hex**|**Uso**|
| :- | :- | :- |
|Deep Black|#0A0E1A|Background de menus, overlay de morte, tela de loading|
|Abyss Blue|#062B3A|Cor primária de UI — painéis, HUD background|
|Teal Principal|#0B7A8A|Cor de destaque — botões ativos, bordas de seleção, ícones principais|
|Teal Claro|#1AABBD|Hover states, texto de destaque, barras de progresso|
|Água Rasa|#48D1CC|Brilhos bioluminescentes, efeitos de O₂ ok, Z1|
|Branco Azulado|#D6F2F5|Texto principal nos menus escuros, barra de O₂ cheia|
|Perigo Vermelho|#C0392B|HP crítico, dano de pressão, alertas urgentes|
|Alerta Âmbar|#E67E22|O₂ médio (30–15%), recursos incomuns, avisos|
|Sucesso Verde|#1D6A3A|Crafting concluído, construção ok, conexão com base|
|Bioluminescente|#39FF14|Apenas efeitos de tela e partículas — nunca UI|
|Comum (cinza)|#7F8C8D|Recursos comuns, texto secundário, elementos inativos|
|Incomum (azul)|#2980B9|Recursos incomuns, tier 1 de equipamento|
|Raro (roxo)|#8E44AD|Recursos raros, tier 2|
|Épico (laranja)|#E67E22|Recursos épicos, tier 3|
|Único (dourado)|#F1C40F|Itens únicos, relíquias, itens de prestígio|

# **Tipografia**

|**Uso**|**Fonte**|**Tamanho**|**Peso**|**Cor**|
| :- | :- | :- | :- | :- |
|Título de menu grande|Bangers ou Oswald|28–36px|Bold|Branco Azulado|
|Nome de zona (notificação)|Oswald|20px|Medium|Teal Claro|
|Label de HUD (O₂, HP, Depth)|Roboto Mono|14px|Regular|Branco Azulado com 80% opacity|
|Valor de HUD (números)|Roboto Mono|20px|Bold|Branco ou cor de estado (vermelho/âmbar)|
|Texto de crafting (nome item)|Roboto|15px|Medium|Branco Azulado|
|Texto de crafting (ingredientes)|Roboto|13px|Regular|Cinza claro|
|Texto de lore / log|Roboto Slab|14px|Regular|Branco Azulado, fundo Abyss Blue|
|Texto de tutorial (dica)|Roboto|13px|Regular|Branco, fundo semi-transparente Abyss Blue|
|Aviso de zona (pressão, etc)|Oswald|16px|Bold|Alerta Âmbar ou Perigo Vermelho|

**ROBLOX:** No Roblox Studio, use as fontes disponíveis nativamente: GothamBlack para títulos, Gotham Medium para UI e Gotham Book para texto de lore. Elas são as mais próximas das fontes acima.

# **Sistema de Ícones de Recursos**
Todos os ícones de recursos seguem o mesmo padrão visual: forma simples + cor de raridade + leve brilho bioluminescente.

|**Recurso**|**Forma do ícone**|**Cor base**|**Efeito visual**|
| :- | :- | :- | :- |
|Algas Nutritivas|3 tiras onduladas verticais|Verde (#27AE60)|Leve transparência, parecem flutuar|
|Sucata / Sucata Eletrônica|Engrenagem quebrada|Cinza (#7F8C8D)|Textura metálica básica|
|Calcário|Cubo irregular|Bege (#D5CBA7)|Sem efeito — material mais básico|
|Ferro Simples|Barra horizontal|Azul-cinza (#4A6FA5)|Reflexo sutil de luz|
|Cristal Marinho|Prisma hexagonal|Azul (#2980B9)|Brilho pulsante leve|
|Ferro Abissal|Barra com textura de fissura|Azul escuro (#1A3A5C)|Partícula de luz mínima|
|Titânio das Profundezas|Dois triângulos interligados|Roxo (#8E44AD)|Brilho de raridade|
|Gel Bioluminescente|Gota arredondada|Verde biolum. (#39FF14)|Brilha e pulsa|
|Núcleo Térmico|Esfera com raios internos|Laranja (#E67E22)|Rotação lenta do ícone|
|Shard Hadal|Cristal irregular com arestas vivas|Dourado (#F1C40F)|Partículas douradas ao redor|

# **Componentes de HUD — Especificações**
## **Barra de Oxigênio**
- Largura: 240px. Altura: 16px. Border-radius: 8px
- Background: Abyss Blue (#062B3A) com border Teal Principal 1px
- Fill: gradiente linear de Água Rasa → Teal Claro quando > 30%
- Fill: gradiente Alerta Âmbar quando 30–15%
- Fill: Perigo Vermelho com animação de pulse (opacity 1→0.5→1, 0.5s) quando < 15%
- Ícone: bolha de ar pequena à esquerda, 16px

## **Barra de HP / Integridade do Traje**
- Mesmas dimensões da barra de O₂
- Fill: Sucesso Verde quando > 50%
- Fill: Alerta Âmbar quando 50–25%
- Fill: Perigo Vermelho quando < 25%
- Visível apenas quando < 80% — some gradualmente quando regenera acima disso

## **Indicador de Profundidade**
- Background: Abyss Blue semi-transparente (80% opacity), border-radius 6px, padding 6px 10px
- Texto do número: Roboto Mono, 20px, Bold, Branco Azulado
- Texto da zona: Roboto, 12px, Regular, Teal Claro
- Formato: "347m" na linha 1, "Zona 2 — Recife Profundo" na linha 2

## **Slots da Hotbar**
- 8 slots de 48×48px cada. Gap de 4px entre eles
- Background: Abyss Blue 70% opacity. Border: 1px Teal Principal
- Slot selecionado: border 2px Teal Claro + leve glow
- Ícone do item: 36×36px centralizado
- Quantidade: número no canto inferior direito, Roboto Mono 11px

# **Componentes de Menu — Especificações**
## **Painel de Background**
- Background: Abyss Blue (#062B3A) 95% opacity
- Border: 1px Teal Principal (#0B7A8A)
- Border-radius: 8px
- Animação de entrada: slide de baixo para cima + fade in, 0.2s Quad easing

## **Botão Principal**
- Background: Teal Principal (#0B7A8A). Border: none
- Texto: Oswald 15px Bold, Branco
- Hover: Teal Claro (#1AABBD). Active: escala 0.97
- Disabled: Cinza (#7F8C8D), cursor not-allowed

## **Card de Item (inventário e crafting)**
- Background: Deep Black (#0A0E1A). Border: 1px da cor de raridade do item
- Ícone: 40×40px. Nome: 13px. Quantidade: Roboto Mono 11px âmbar
- Hover: border 2px, leve brilho na cor de raridade
- Selecionado: background Abyss Blue, border 2px Teal Claro
Abyss Survival — Guia de Identidade Visual	v1.0
