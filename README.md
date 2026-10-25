# Círculos de Ruína — Protótipo 0.1

Protótipo HTML5 de estratégia em tabuleiro hexagonal com transição para arena de combate.

## Como jogar
1. Abra `index.html` no navegador.
2. Clique numa unidade da equipe ativa.
3. Clique em hexágono adjacente vazio para mover e trocar o turno.
4. Clique no inimigo adjacente para abrir a arena.
5. Na arena, use WASD ou setas para mover e Espaço para atacar.

## Onde editar
- `data/config.json`: arena, hexágonos e limites.
- `data/units.json`: vida, dano, velocidade, raios e cores.
- `data/terrains.json`: terrenos e cicatrizes.

Os dados também estão espelhados em `game.js`, para o jogo abrir diretamente sem servidor local.