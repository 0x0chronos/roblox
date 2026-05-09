🌊

**ABYSS SURVIVAL**

IA de Criaturas

*Máquina de Estados · Código Luau · Comportamentos por Espécie*

**Princípios da IA**

Cada criatura tem uma máquina de estados. Transições entre estados são baseadas em gatilhos (distância, visão, HP). O jogador aprende os padrões --- isso é o que torna o combate divertido.

> **REGRA:** Toda IA roda no servidor (Script, não LocalScript). O cliente só vê o resultado via posição dos modelos. Nunca deixe a IA rodar no cliente.

**Máquina de Estados Universal**

| **Estado** | **Descrição**                             | **Transição para PATROL**  | **Transição para ALERT**          | **Transição para CHASE**                          | **Transição para ATTACK**                 | **Transição para RETREAT**              |
|------------|-------------------------------------------|----------------------------|-----------------------------------|---------------------------------------------------|-------------------------------------------|-----------------------------------------|
| IDLE       | Parado no ponto de spawn. Animação idle.  | Timer de 3--8s aleatório   | Jogador entra em raio de detecção | ---                                               | ---                                       | ---                                     |
| PATROL     | Caminha entre waypoints predefinidos.     | ---                        | Jogador entra em raio de detecção | Jogador entra em raio de visão com linha de visão | ---                                       | HP \< 20% (só criaturas com retreat)    |
| ALERT      | Para. Vira para o jogador. Som de alerta. | Jogador sai do raio por 5s | ---                               | 0.5s de delay após ALERT                          | ---                                       | ---                                     |
| CHASE      | Persegue o jogador em alta velocidade.    | Jogador sai do raio por 8s | ---                               | ---                                               | Jogador entra em raio de ataque (3 studs) | HP \< 20% (só certas criaturas)         |
| ATTACK     | Executa animação de ataque. Aplica dano.  | ---                        | ---                               | Jogador sai do raio de ataque                     | ---                                       | Após 3 ataques consecutivos sem acertar |
| RETREAT    | Foge do jogador. Volta ao spawn.          | Chegou ao spawn            | ---                               | ---                                               | ---                                       | ---                                     |

**Módulo CreatureAI.lua --- Estrutura Base**

> \-- ServerScriptService/Modules/CreatureAI.lua
>
> local RunService = game:GetService(\"RunService\")
>
> local Config = require(script.Parent.Config)
>
> local CreatureAI = {}
>
> local States = {IDLE=\"IDLE\",PATROL=\"PATROL\",ALERT=\"ALERT\",
>
> CHASE=\"CHASE\",ATTACK=\"ATTACK\",RETREAT=\"RETREAT\"}
>
> function CreatureAI:new(model, config)
>
> local self = setmetatable({}, {\_\_index=CreatureAI})
>
> self.model = model
>
> self.config = config \-- tabela de config da espécie
>
> self.state = States.IDLE
>
> self.target = nil
>
> self.hp = config.maxHP
>
> self.waypoints= config.waypoints or {}
>
> self.waypointIndex = 1
>
> self.stateTimer = 0
>
> self.attackCooldown= 0
>
> return self
>
> end
>
> function CreatureAI:update(dt)
>
> self.stateTimer = self.stateTimer - dt
>
> self.attackCooldown = self.attackCooldown - dt
>
> if self.state == States.IDLE then self:updateIdle(dt)
>
> elseif self.state == States.PATROL then self:updatePatrol(dt)
>
> elseif self.state == States.ALERT then self:updateAlert(dt)
>
> elseif self.state == States.CHASE then self:updateChase(dt)
>
> elseif self.state == States.ATTACK then self:updateAttack(dt)
>
> elseif self.state == States.RETREAT then self:updateRetreat(dt)
>
> end
>
> end
>
> function CreatureAI:getNearestPlayer()
>
> local hrp = self.model:FindFirstChild(\"HumanoidRootPart\")
>
> local best, bestDist = nil, math.huge
>
> for \_, player in pairs(game.Players:GetPlayers()) do
>
> local char = player.Character
>
> if char then
>
> local phrp = char:FindFirstChild(\"HumanoidRootPart\")
>
> if phrp then
>
> local dist = (hrp.Position - phrp.Position).Magnitude
>
> if dist \< bestDist then bestDist=dist; best=player end
>
> end
>
> end
>
> end
>
> return best, bestDist
>
> end
>
> function CreatureAI:hasLineOfSight(target)
>
> local hrp = self.model:FindFirstChild(\"HumanoidRootPart\")
>
> local tHRP = target.Character and target.Character:FindFirstChild(\"HumanoidRootPart\")
>
> if not tHRP then return false end
>
> local ray = Ray.new(hrp.Position, (tHRP.Position - hrp.Position).Unit \* self.config.visionRange)
>
> local hit = workspace:FindPartOnRayWithIgnoreList(ray,
>
> {self.model, target.Character})
>
> return hit == nil \-- sem obstáculo = linha de visão livre
>
> end
>
> function CreatureAI:takeDamage(amount)
>
> self.hp = math.max(0, self.hp - amount)
>
> if self.hp \<= 0 then self:die() end
>
> if self.hp / self.config.maxHP \< 0.2 and self.config.canRetreat then
>
> self:setState(States.RETREAT)
>
> end
>
> end
>
> function CreatureAI:setState(newState)
>
> self.state = newState
>
> self.stateTimer = 0
>
> \-- disparar animação e som correspondente
>
> end
>
> return CreatureAI

**Comportamentos por Espécie --- Tabela Completa**

| **Espécie**        | **maxHP** | **Velocidade** | **detectionRange** | **visionRange** | **attackRange** | **attackDamage** | **attackCooldown** | **canRetreat** | **Comportamento especial**                                                                  |
|--------------------|-----------|----------------|--------------------|-----------------|-----------------|------------------|--------------------|----------------|---------------------------------------------------------------------------------------------|
| Peixe Fantasma     | 20        | 12             | 15                 | 8               | ---             | ---              | ---                | Sim            | Foge da luz. Se jogador acender lanterna perto: RETREAT imediato                            |
| Tubarão Caçador    | 150       | 28             | 40                 | 30              | 4               | 25               | 2.0s               | Não            | Patrulha rota fixa. ALERT dura 0.3s (reage rápido). Persiste no chase                       |
| Água-Viva Elétrica | 80        | 6              | 0                  | 0               | 3               | 20 (AOE)         | 3.0s               | Não            | Sem estados de ALERT/CHASE. ATTACK ao contato. AOE radius 8 studs                           |
| Polvo Abissal      | 200       | 18             | 60                 | 0               | 5               | 30               | 2.5s               | Sim            | Emite bioluminescência falsa para atrair. Só ataca ao ser tocado ou após 10s de proximidade |
| Leviatã            | 2000      | 20             | 80                 | 60              | 10              | 80               | 4.0s               | Não            | Cria corrente que puxa jogadores (BodyVelocity no servidor). Chama reforços ao 50% HP       |
| A Coisa            | 500       | 35             | 0                  | 0               | 8               | 50               | 1.5s               | Não            | Aparece sem detecção --- surge do chão. Ataca a base diretamente. Invisível no sonar        |

**updatePatrol e updateChase --- Implementação**

> function CreatureAI:updateIdle(dt)
>
> if self.stateTimer \<= 0 then
>
> self.stateTimer = math.random(3, 8)
>
> self:setState(States.PATROL)
>
> end
>
> local player, dist = self:getNearestPlayer()
>
> if player and dist \< self.config.detectionRange then
>
> self.target = player
>
> self:setState(States.ALERT)
>
> end
>
> end
>
> function CreatureAI:updatePatrol(dt)
>
> local player, dist = self:getNearestPlayer()
>
> if player and dist \< self.config.visionRange and self:hasLineOfSight(player) then
>
> self.target = player
>
> self:setState(States.ALERT)
>
> return
>
> end
>
> \-- mover para próximo waypoint
>
> local hrp = self.model:FindFirstChild(\"HumanoidRootPart\")
>
> local wp = self.waypoints\[self.waypointIndex\]
>
> if wp and (hrp.Position - wp).Magnitude \< 3 then
>
> self.waypointIndex = (self.waypointIndex % \#self.waypoints) + 1
>
> end
>
> if wp then
>
> self.model.Humanoid:MoveTo(wp)
>
> end
>
> end
>
> function CreatureAI:updateAlert(dt)
>
> if self.stateTimer \<= 0 then
>
> \-- delay de reação: 0.5s
>
> if -self.stateTimer \>= 0.5 then
>
> self:setState(States.CHASE)
>
> end
>
> end
>
> end
>
> function CreatureAI:updateChase(dt)
>
> if not self.target or not self.target.Character then
>
> self:setState(States.PATROL) return
>
> end
>
> local hrp = self.model:FindFirstChild(\"HumanoidRootPart\")
>
> local tHRP = self.target.Character:FindFirstChild(\"HumanoidRootPart\")
>
> local dist = (hrp.Position - tHRP.Position).Magnitude
>
> if dist \< self.config.attackRange then
>
> self:setState(States.ATTACK) return
>
> end
>
> if dist \> self.config.detectionRange \* 1.5 then
>
> self.target = nil
>
> self:setState(States.PATROL) return
>
> end
>
> self.model.Humanoid.WalkSpeed = self.config.speed
>
> self.model.Humanoid:MoveTo(tHRP.Position)
>
> end
>
> function CreatureAI:updateAttack(dt)
>
> if self.attackCooldown \> 0 then return end
>
> local hrp = self.model:FindFirstChild(\"HumanoidRootPart\")
>
> local tHRP = self.target and self.target.Character
>
> and self.target.Character:FindFirstChild(\"HumanoidRootPart\")
>
> if not tHRP then self:setState(States.PATROL) return end
>
> if (hrp.Position - tHRP.Position).Magnitude \> self.config.attackRange \* 1.5 then
>
> self:setState(States.CHASE) return
>
> end
>
> \-- aplicar dano
>
> local hum = self.target.Character:FindFirstChild(\"Humanoid\")
>
> if hum then hum:TakeDamage(self.config.attackDamage) end
>
> self.attackCooldown = self.config.attackCooldown
>
> end

**Spawner de Criaturas**

> \-- ServerScriptService/Modules/CreatureSpawner.lua
>
> local SPAWN_CONFIG = {
>
> Zone1 = {
>
> {type=\"PeixeFantasma\", count=6, respawnTime=120},
>
> {type=\"TubaraoEspreita\",count=3, respawnTime=180},
>
> },
>
> Zone2 = {
>
> {type=\"AguaVivaEletrica\",count=4, respawnTime=200},
>
> {type=\"EnguiaGigante\", count=2, respawnTime=240},
>
> },
>
> Zone3 = {
>
> {type=\"PolvoAbissal\", count=3, respawnTime=300},
>
> },
>
> Zone4 = {
>
> {type=\"Leviata\", count=1, respawnTime=600},
>
> },
>
> }
>
> \-- Ao matar criatura: desativar modelo + task.delay(respawnTime, reativar)
>
> \-- Nunca destruir e recriar --- use pooling (Enabled = false/true)

**Checklist de Implementação**

- \[ \] CreatureAI.lua base implementado com máquina de estados

- \[ \] Tabela de config por espécie criada em Config.lua

- \[ \] Waypoints de patrulha criados no Workspace como Parts (invisíveis)

- \[ \] Leviatã: implementar BodyVelocity para corrente de atração

- \[ \] Peixe Fantasma: detectar lanterna ativa do jogador

- \[ \] Polvo Abissal: PointLight de isca ligada/desligada por script

- \[ \] Sistema de pooling: morrer = Enabled false, respawn = Enabled true

- \[ \] Testar: criatura não atravessa paredes da base

- \[ \] Testar: dois jogadores próximos --- criatura ataca o mais próximo
