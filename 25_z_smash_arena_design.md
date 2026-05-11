# Z-Smash Arena — Design inicial do jogo browser/anime

## Visão rápida

Sim, dá para transformar a ideia em um jogo de navegador com cara de anime competitivo. O MVP deve focar em partidas 1v1 curtas, bola acelerando a cada troca, timing de rebate, progressão por equipamentos e baús. A referência visual é de esporte arcade com personagens estilizados, mas o diferencial fica no sistema RPG: o personagem equipa peças que somam HP/status e a arma define o superpoder carregável.

## Pilar principal

O jogo precisa parecer simples em 3 segundos e profundo depois de 3 partidas:

1. **Simples:** a bola vem, o player aperta rebater no timing.
2. **Tenso:** cada rally aumenta o dano, então ninguém fica seguro para sempre.
3. **Colecionável:** armas e sets mudam status, visual e poder especial.
4. **Competitivo:** ranked entrega baús melhores conforme elo, mas habilidade de timing ainda decide lutas.

## Mecânica de dano escalável

A sua sugestão de aumentar dano por rebatida é essencial para evitar luta infinita. A regra recomendada é:

```text
Dano do próximo impacto =
  danoBaseDaArma
+ incrementoDoRally × quantidadeDeRebatidas
+ bônusDeImpactoDasLuvas
× multiplicadorDeTiming
× multiplicadorDoZPowerQuandoAtivo
```

### Timing do rebate

| Resultado | Condição | Multiplicador | Carga Z | Sensação esperada |
| --- | --- | ---: | ---: | --- |
| Perfect | bola no centro da zona/arma | 1.55x | +2 | explosão visual, texto grande, som forte |
| Good | dentro da zona principal | 1.15x | +1 | seguro e satisfatório |
| Early/Late | borda da zona | 0.80x | +0 | rebate fraco, bola mais lenta |
| Miss | fora da zona | recebe dano | +0 | punição clara |

### Overtime anti-luta eterna

- Dano inicial do set comum: **10**.
- Incremento normal por rebate: **+10**.
- A partir da 8ª rebatida: entra **Overtime**.
- No Overtime, o incremento vira **+18 por rebate** e a zona de timing reduz **8%**.

Isso mantém a partida curta, mas ainda permite viradas se o jogador acertar Perfect ou carregar o Z-Power.

## Equipamentos e atributos

Todo jogador começa com o **Set do Recruta**. O HP final e os status vêm da soma das peças equipadas.

| Slot | Função | Exemplo de status |
| --- | --- | --- |
| Capacete | defesa e resistência a atordoamento | +DEF, -stun |
| Armadura | maior bônus de HP | +HP alto |
| Luvas | dano de impacto e velocidade da bola | +impacto |
| Calças | estamina e mobilidade | +stamina |
| Botas | dash, pulo e reposicionamento | +dash/pulo |
| Arma | dano base, crítico e Z-Power | +dano, habilidade única |

### Bônus de sinergia

Se o jogador equipar o set completo do mesmo tema ou raridade, ganha bônus extra. Exemplo: **Set do Dragão completo = +15% de HP total e aura visual**.

## Set inicial

| Peça | Nome | Raridade | Efeito |
| --- | --- | --- | --- |
| Arma | Espada de Madeira | Comum | Impacto Pesado: aumenta um pouco a velocidade/dano do próximo rebate |
| Capacete | Faixa de Treino | Comum | pequena defesa |
| Armadura | Roupa de Pano | Comum | base para fechar 100 HP |
| Luvas | Luvas de Recruta | Comum | pequeno impacto |
| Calças | Calça de Treino | Comum | stamina básica |
| Botas | Tênis de Quadra | Comum | dash básico |

## Raridades e chances base

| Raridade | Cor | Chance padrão | Papel no jogo |
| --- | --- | ---: | --- |
| Comum | Branco | 60% | itens iniciais e upgrades simples |
| Incomum | Verde | 25% | pequenos buffs perceptíveis |
| Raro | Azul | 10% | primeira mudança forte de visual e kit |
| Épico | Roxo | 4% | VFX, status altos, habilidades melhores |
| Lendário | Dourado | 1% | Z-Power devastador e aura marcante |

## Baús

### Baú de Ranked

- Recebido ao vencer certas partidas.
- Qualidade depende do elo: Bronze, Prata, Ouro, Platina, Diamante, Celestial.
- Abre com tempo de espera.
- Para reduzir/avançar abertura, o player precisa continuar vencendo partidas.
- Chances devem ser mostradas de forma transparente na UI.

### Baú da Loja

- Compra com Coins ou Robux.
- Abre instantaneamente.
- Pode ter variações com chances melhores, mas sem esconder probabilidade.
- Deve evitar vender poder absoluto; o ideal é vender velocidade de progressão, skins e baús com pity/garantia.

## 10 armas iniciais

| Arma | Raridade sugerida | Z-Power | Função |
| --- | --- | --- | --- |
| Espada de Madeira | Comum | Impacto Pesado | acelera e aumenta levemente o próximo dano |
| Manopla Neon | Comum | Turbo Shot | rebate rápido e reto |
| Katana Relâmpago | Incomum | Corte Duplo | aplica dois ticks de dano menor |
| Raquete Oni | Incomum | Intimidação | reduz a zona de timing do rival por 1 rebate |
| Martelo de Gravidade | Raro | Buraco de Peso | deixa a bola pesada e muda velocidade |
| Foice Lunar | Raro | Curva Fantasma | curva a trajetória e engana o rival |
| Lança Solar | Épico | Raio Perfurante | ignora parte da defesa |
| Bastão Oni | Épico | Stun Break | aplica micro-atordoamento se for Perfect |
| Canhão Dragão | Lendário | Explosão Z | alto dano e VFX de dragão |
| Orbe Celestial | Lendário | Tempo Congelado | desacelera a bola para o usuário e acelera para o rival |

## 5 arenas para a primeira fase

| Arena | Identidade | Mecânica leve |
| --- | --- | --- |
| Campo Neon | quadra tutorial colorida | sem modificador |
| Dojo Solar | templo anime quente | bola acelera mais rápido |
| Arena do Vazio | espaço/gravidade baixa | dash/pulo maior |
| Templo Dragão | arena premium visual | partículas e câmera mais dramáticas |
| Estádio Celestial | rank alto | overtime chega mais cedo |

## MVP recomendado

1. Partida 1v1 contra bot e depois multiplayer.
2. Sistema de timing com Perfect/Good/Early/Miss.
3. Dano escalável por rally e Overtime.
4. 6 slots de equipamento e 10 armas.
5. 5 raridades com UI de cor.
6. Baú ranked com timer e baú loja instantâneo.
7. Inventário, equipar item e cálculo de HP.
8. Pelo menos 3 arenas jogáveis no primeiro corte.

## Próximo passo técnico

O protótipo HTML `z_smash_arena_prototype.html` valida a sensação base no navegador: rally, timing, dano escalável, carga Z, lista de armas, raridades, arenas e regra anti-luta infinita. Depois disso, o ideal é separar em módulos JavaScript (`combat`, `equipment`, `loot`, `ui`) e transformar o canvas em uma build com engine leve, como Phaser, ou portar as regras para Roblox/Luau se a decisão final for Roblox.
