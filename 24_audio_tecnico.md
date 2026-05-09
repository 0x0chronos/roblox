ABYSS SURVIVAL  —  Especificação de Áudio Técnica  |  Roblox Studio

🌊

**ABYSS SURVIVAL**

Especificação de Áudio Técnica

*Assets · Formatos · Fontes Gratuitas · Implementação*


# **Lista Completa de Assets de Áudio**
Todos os assets abaixo são necessários para o MVP. Organizados por categoria e ordem de implementação.

## **Músicas Ambiente (Categoria: Music)**

|**Asset**|**Duração alvo**|**Formato**|**Estéreo?**|**Volume norm.**|**Onde baixar gratuitamente**|
| :- | :- | :- | :- | :- | :- |
|Zone1\_Theme|3–5 min|OGG Vorbis|Sim (estéreo)|−14 LUFS|freesound.org: "underwater ambient peaceful"|
|Zone2\_Theme|3–5 min|OGG Vorbis|Sim|−16 LUFS|freesound.org: "deep sea drone ambient"|
|Zone3\_Theme|4–6 min|OGG Vorbis|Sim|−18 LUFS|freesound.org: "horror dark drone abyss"|
|Zone4\_Theme|4–6 min|OGG Vorbis|Sim|−20 LUFS|freesound.org: "deep horror silence pulse"|
|Zone5\_Theme|3–5 min|OGG Vorbis|Sim|−22 LUFS|freesound.org: "hadal soundscape"|
|Base\_Theme|2–4 min|OGG Vorbis|Sim|−16 LUFS|freesound.org: "submarine interior hum"|
|Event\_Action|1–2 min (loop)|OGG Vorbis|Sim|−14 LUFS|opengameart.org: "underwater action"|
|Victory\_Stinger|5–8 seg|OGG Vorbis|Sim|−12 LUFS|pixabay.com/music: "victory short"|

## **Sons de Ambiente (Categoria: Ambience)**

|**Asset**|**Duração**|**Loop?**|**Mono/Estéreo**|**Volume norm.**|**Fonte**|
| :- | :- | :- | :- | :- | :- |
|Water\_Ambience\_Zone1|30s+|Sim (seamless)|Estéreo|−12 LUFS|freesound.org: "shallow water bubbles loop"|
|Water\_Ambience\_Zone2|30s+|Sim|Estéreo|−14 LUFS|freesound.org: "deep water ambient loop"|
|Water\_Ambience\_Zone3|30s+|Sim|Estéreo|−16 LUFS|freesound.org: "underwater pressure loop"|
|Pressure\_Creak|20s+|Sim|Mono|−10 LUFS|freesound.org: "metal pressure creak loop"|
|Base\_Hum|60s+|Sim|Estéreo|−18 LUFS|freesound.org: "machine room hum loop"|
|Hydrotermal\_Steam|15s+|Sim|Mono|−10 LUFS|freesound.org: "steam vent loop"|
|Current\_Wind|20s+|Sim|Estéreo|−14 LUFS|freesound.org: "underwater current flow"|
|Base\_Generator|30s+|Sim|Mono|−16 LUFS|freesound.org: "generator hum loop"|

## **SFX de Gameplay (Categoria: SFX)**

|**Asset**|**Duração**|**Variações**|**Formato**|**Fonte**|
| :- | :- | :- | :- | :- |
|SFX\_Collect\_Common|0\.3–0.5s|3|OGG|freesound.org: "water bubble collect"|
|SFX\_Collect\_Rare|0\.5–0.8s|2|OGG|freesound.org: "crystal chime underwater"|
|SFX\_Craft\_Start|0\.5s|1|OGG|freesound.org: "mechanical click start"|
|SFX\_Craft\_Complete|0\.8–1s|1|OGG|freesound.org: "success ding double"|
|SFX\_Build\_Module|1\.5–2s|1|OGG|freesound.org: "metal assemble clank"|
|SFX\_Arpoon\_Fire|0\.4s|1|OGG|freesound.org: "underwater whoosh fast"|
|SFX\_Arpoon\_Hit|0\.3s|2|OGG|freesound.org: "impact thud underwater"|
|SFX\_Event\_Start|1–2s|1|OGG|freesound.org: "alert siren underwater"|
|SFX\_ZoneTransition|2s|1|OGG|freesound.org: "pressure whoosh deep"|
|SFX\_Base\_PowerOff|1\.5s|1|OGG|freesound.org: "power down machine"|
|SFX\_Base\_PowerOn|1\.5s|1|OGG|freesound.org: "power up hum"|
|SFX\_Lore\_Found|1s|1|OGG|freesound.org: "discovery chime"|

## **SFX do Jogador (Categoria: Player)**

|**Asset**|**Duração**|**Variações**|**Uso**|**Fonte**|
| :- | :- | :- | :- | :- |
|Player\_Breathe|1\.5–2s|3 (ritmos diferentes)|A cada 3s, acelera com O₂ baixo|freesound.org: "scuba breathing loop"|
|Player\_Bubble\_Breath|0\.3s|4|Ao mover + ao respirar|freesound.org: "bubble exhale small"|
|Player\_Damage|0\.3s|3|Ao receber qualquer dano|freesound.org: "underwater hit thud"|
|Player\_Pressure\_Pain|0\.5s|2|A cada segundo com dano de pressão|freesound.org: "metal stress creak sharp"|
|Player\_O2\_Alarm|0\.3s (loop bipe)|1|Loop quando O₂ < 15%|freesound.org: "electronic beep warning"|
|Player\_Heartbeat|0\.8s|1|Loop quando O₂ < 20%|freesound.org: "heartbeat slow accelerating"|
|Player\_Death|3–4s|1|Ao morrer — não usar som genérico|freesound.org: "drowning fade silence"|
|Player\_Respawn|1s|1|Ao respawnar na base|freesound.org: "gasp breath surface"|

## **Sons de Criaturas (Categoria: Creature)**

|**Criatura**|**Asset**|**Duração**|**Especificação**|**Fonte**|
| :- | :- | :- | :- | :- |
|Tubarão|Shark\_Approach|3–5s|Baixo pulsante, 60–80Hz, grave|freesound.org: "bass pulse low frequency"|
|Tubarão|Shark\_Attack|0\.5s|Rangido + splash rápido|freesound.org: "animal attack growl"|
|Tubarão|Shark\_Death|2s|Borbulha pesada descendente|freesound.org: "bubble descend heavy"|
|Água-Viva|Jellyfish\_Approach|2s|Estática elétrica crescente|freesound.org: "static electricity crackle"|
|Água-Viva|Jellyfish\_Attack|0\.4s|Descarga elétrica: buzz forte|freesound.org: "electric shock zap"|
|Polvo|Octopus\_Approach|3s|Sussurro invertido + click|freesound.org: "click organic reversed"|
|Polvo|Octopus\_Attack|0\.8s|Splash + som abafado|freesound.org: "underwater splash impact"|
|Leviatã|Leviathan\_Approach|5–8s|Vibração de baixíssima frequência|freesound.org: "subsonic rumble 40hz"|
|Leviatã|Leviathan\_Attack|2s|Rugido distorcido subaquático|freesound.org: "monster roar underwater"|
|Leviatã|Leviathan\_Death|8s|Agonia longa + silêncio final|freesound.org: "large creature death long"|

# **Sites de Assets Gratuitos — Guia**

|**Site**|**Licença**|**Melhor para**|**URL**|
| :- | :- | :- | :- |
|Freesound.org|Creative Commons (verificar por asset)|SFX e ambience — maior biblioteca|freesound.org|
|OpenGameArt.org|CC0 / GPL|Músicas para jogos, sem restrições|opengameart.org|
|Pixabay Music|Royalty-free|Músicas ambiente e trilhas|pixabay.com/music|
|Mixkit.co|Mixkit License (free)|SFX e trilhas curtas|mixkit.co|
|ZapSplat.com|ZapSplat License|SFX variados, boa qualidade|zapsplat.com|

**IMPORTANTE:** Sempre verifique a licença individual de cada asset no Freesound. Prefira CC0 (domínio público) ou CC-BY (crédito necessário). Evite CC-NC (não comercial) — jogos do Roblox são considerados comerciais.

# **Implementação no Roblox Studio**
## **Passo a passo para importar áudio**
1. Crie uma conta no Roblox e acesse Creator Hub (create.roblox.com)
1. Vá em "Audio" → "Upload Audio". Limite: 7 segundos grátis, maior requer Robux
1. Para áudio > 7s grátis: use áudio já disponível na toolbox com search terms
1. Após upload, copie o Asset ID do áudio
1. No Studio, crie um Sound object e cole o ID no campo SoundId
1. Configure Volume, RollOffMaxDistance e Looped conforme tabela acima

## **Dica para contornar o limite de 7 segundos**
- Músicas ambiente longas: busque na toolbox "underwater ambient loop" — há muitos assets gratuitos
- Alternativamente: use o Roblox Audio Marketplace (Creator Hub → Audio → Search)
- Assets com "Looped" ativo dispensam duração — mesmo 30s de música em loop funciona
Abyss Survival — Especificação de Áudio Técnica	v1.0
