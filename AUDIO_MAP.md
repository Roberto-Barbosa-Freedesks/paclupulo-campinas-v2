# Mapa de Áudio e Efeitos

## Trilha de áudio disponibilizada
- `preloadAudio` instancia todos os efeitos do jogo clássico, mapeando cada arquivo em `sounds/` para uma trilha reutilizável (ex.: `coffee-break-music.mp3`, `miss.mp3`, `eating.mp3`, etc.).【F:pacman-original.js†L237-L267】

## Eventos de gameplay
- Fantasma comido: ao chamar `goHome`, todos os sons são silenciados e o efeito `eating-ghost.mp3` é reproduzido antes do fantasma entrar no modo "eaten".【F:pacman-original.js†L7785-L7795】
- Movimento de fantasmas: quando algum fantasma está retornando para casa toca o loop `ghost-return-to-home.mp3`; quando há fantasmas fora da casa e não assustados, toca o loop `ghost-normal-move.mp3`; ambos são interrompidos conforme o número de fantasmas em cada estado muda.【F:pacman-original.js†L7806-L7827】
- Comer pontos/energizadores: o loop `eating.mp3` inicia ao comer pastilhas ou energizadores e para quando o jogador está parado ou fora de um ponto; ao ativar o energizador, o loop de movimento normal dos fantasmas é parado e o loop `ghost-turn-to-blue.mp3` é iniciado, sendo encerrado no reset do efeito.【F:pacman-original.js†L8279-L8317】【F:pacman-original.js†L9025-L9075】
- Frutas: ao coletar fruta, todos os loops são silenciados e o efeito `eating-fruit.mp3` toca antes de retomar os sons de movimento dos fantasmas.【F:pacman-original.js†L9169-L9176】
- Transições de estado: ao trocar de estado principal (`switchState`) todas as trilhas são pausadas para evitar vazamento de áudio entre telas.【F:pacman-original.js†L9620-L9634】
- Telas de menu/título: no estado inicial do menu e no menu de seleção/ajuda a música de fundo `coffee-break-music.mp3` entra em loop contínuo.【F:pacman-original.js†L9751-L9777】【F:pacman-original.js†L10108-L10126】
- Início de fase: ao entrar no estado "Ready" o loop de menu é interrompido e o jingle `start-music.mp3` é reproduzido antes do jogo começar.【F:pacman-original.js†L10755-L10780】
- Fim de nível: quando todos os pontos são coletados, o jogo toca `extend.mp3` ao trocar para o estado de finalização.【F:pacman-original.js†L10941-L10945】
- Perda de vida: ao entrar no estado de morte, o efeito `miss.mp3` é disparado antes da animação de morte.【F:pacman-original.js†L11065-L11095】
- Cutscenes: ao iniciar uma cutscene, `coffee-break-music.mp3` é agendada para reiniciar após breve atraso para acompanhar a transição.【F:pacman-original.js†L11484-L11493】

## Áudio fora do gameplay imediato
- Tela inicial: o elemento `<audio id="bg-music">` aponta para `coffee-break-music.mp3`; a interação na tela de start dispara o priming (`gameaudio-prime-request`) e limpeza de áudio antes de abrir o login/jogo.【F:index.html†L487-L520】【F:index.html†L1191-L1214】
- Priming adicional do start: script duplicado reforça o priming do áudio, tenta tocar/pausear rapidamente o `<audio>` para liberar áudio em navegadores mobile, e oculta a tela inicial logo após o clique.【F:index.html†L1754-L1789】
- Visibilidade da aba: ao sair/voltar para a aba, o áudio é primado novamente ao retornar e silenciado quando a página fica oculta.【F:index.html†L1791-L1803】
- Guarda mobile e limpeza global: `pacman.js` registra ouvintes de toque/foco para acionar `gameaudio-prime-request` em dispositivos móveis e ouve `game:cleanup` para silenciar todos os sons e parar `bg-music`.【F:pacman.js†L1-L34】
- Conquistas: ao desbloquear uma conquista, tenta-se reproduzir o efeito `extend.mp3` reutilizando a mesma trilha do jogo.【F:achievements.js†L290-L299】

## Trilha definida mas não referenciada em runtime
- As faixas `ghost-spurt-move-1.mp3` a `ghost-spurt-move-4.mp3` e `credit.mp3` estão pré-carregadas, porém não há chamadas no código atual que acionem esses sons.【F:pacman-original.js†L239-L253】
