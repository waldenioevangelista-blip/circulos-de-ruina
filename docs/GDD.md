# Círculos de Ruína — GDD

## Visão
Dois Arquimagos disputam um território vivo e amaldiçoado. No tabuleiro hexagonal, comandam tropas, revelam terreno, disputam recursos e armam rituais. Quando unidades inimigas se encontram, o hexágono disputado se expande para uma arena gerada a partir daquele terreno. O resultado muda o tabuleiro com controle territorial, dano e cicatrizes persistentes.

Projeto independente de Legiões das Armadilhas. A inspiração é apenas estrutural: estratégia no mapa e confronto em arena. Não reutilizar personagens, lore, arte, interface ou regras de Dark Legions.

## Pilares
- Tabuleiro importa: posição, visão, rotas e objetivos definem as lutas.
- Arena decide: confrontos de 60 a 90 segundos favorecem habilidade, composição e cenário.
- Cicatrizes persistentes alteram o território.
- Poucas unidades, muitas escolhas.
- Partidas entre 15 e 25 minutos.

## Vitória
- Derrotar o Arquimago inimigo.
- Controlar 3 Obeliscos por 2 turnos próprios consecutivos.
- Acumular 10 Éteres e manter uma unidade no Santuário Central por 1 turno.

## Loop
1. Escolher Arquimago e hoste de até 6 unidades.
2. Alternar turnos: mover 1 unidade e executar 1 ação de Arquimago ou ritual.
3. Entrar em hexágono inimigo abre uma arena.
4. A arena resolve a disputa.
5. O mapa recebe ocupação, dano e cicatriz.

## Tabuleiro
- Grade inicial: 7 x 7 hexágonos, com neblina de guerra.
- Santuários controlados produzem 1 Éter por turno.
- Ações: mover, explorar, invocar, ocultar, fortificar, corromper, purificar e ativar ritual.

| Terreno | Tabuleiro | Arena |
|---|---|---|
| Bosque Petrificado | Bloqueia visão | Colunas quebráveis e raízes que prendem |
| Necrópole Inundada | Cura mortos-vivos | Poças lentas e lacaios neutros |
| Mar de Cinzas | Dano leve ao permanecer | Chão incendiável e rajadas de calor |
| Ruínas Arcanas | Bônus de defesa | Mecanismos e cobertura ativáveis |

## Transição
A câmera aproxima-se do hexágono disputado. Runas e rachaduras acendem sob as peças; o terreno cresce, expande-se e vira uma arena tridimensional compacta. Após a luta, a câmera volta ao mapa revelando a cicatriz deixada.

## Arena
- Controle direto da unidade principal; aliados recebem ordens: avançar, proteger, focar ou recuar.
- Comandos: movimento, ataque básico, duas habilidades, suprema, defesa ou esquiva e ordem de equipe.
- Vitória por eliminação, domínio do foco de poder por 20 segundos acumulados ou objetivo específico do cenário.
- Sobreviventes retornam feridos. Derrotados ficam indisponíveis por 2 turnos no vertical slice.

## Escalas normalizadas
Toda medida usa U (unidade de mundo). Referência visual inicial: 1 U = 32 px, mas nenhuma regra depende de pixels.

| Variável | Valor |
|---|---:|
| HEX_RAIO_U | 3.0 |
| UNIDADE_RAIO_U | 0.65 |
| DIST_ENCONTRO_U | 1.30 |
| ARENA_RAIO_BASE_U | 12.0 |
| ARENA_RAIO_POR_UNIDADE_U | 1.5 |
| ARENA_RAIO_MAX_U | 20.0 |
| RAIO_CAPTURA_U | 2.25 |

`raioArena = clamp(12 + (totalDeUnidades - 2) × 1.5, 12, 20)`

Cada unidade tem raio físico, raio de ataque e raio de ameaça separados.

## Fórmula de atributos
Atributos de design usam escala de 1 a 10.
- Vida: `80 + resistência × 20`
- Dano básico: `8 + poder × 4`
- Velocidade: `3.0 + mobilidade × 0.22 U/s`
- Defesa: `resistência × 3%`, máximo de 30%
- Alcance: `1.2 + alcance × 0.35 U`

## Arquimagos
| Arquimago | Estilo | Tabuleiro | Arena |
|---|---|---|---|
| Tecelã do Luto | Ilusão e controle | Revela intenções e unidades próximas | Duplicata instável e névoa cegante |
| Ferreiro Oco | Defesa e terreno | Ergue fortificação temporária | Barreira metálica ou arma ritual |

## Unidades iniciais
| Unidade | Papel | Vida | Dano | Velocidade | Raio físico | Alcance |
|---|---|---:|---:|---:|---:|---:|
| Sentinela de Sal | Tanque | 240 | 20 | 3.44 U/s | 0.82 U | 1.55 U |
| Corvo de Vela | Batedor | 140 | 24 | 4.76 U/s | 0.42 U | 3.30 U |
| Viúva de Bronze | Duelista | 180 | 32 | 4.32 U/s | 0.58 U | 1.90 U |
| Cão de Cinzas | Agressor | 160 | 36 | 4.54 U/s | 0.60 U | 1.55 U |

### Sentinela de Sal
- Martelo Mineral: 20 dano, alcance 1.55 U, intervalo 1.1 s.
- Muralha de Sal: parede de 3.2 U por 5 s, 120 de vida, recarga 12 s.
- Marca de Absorção: reduz 35% do próximo dano de aliado em 3.5 U, recarga 10 s.
- Abalo Sísmico: 30 dano em 2.2 U, empurra 1.6 U, recarga 16 s.

### Corvo de Vela
- Bico Ígneo: 24 dano, alcance 3.3 U, intervalo 0.85 s.
- Voo Rasante: avança 4.5 U; primeiro alvo sofre 18 dano e fica marcado por 5 s, recarga 9 s.
- Olho da Chama: revela inimigos, armadilhas e ilusões em 6 U por 6 s, recarga 14 s.
- Última Centelha: alvo abaixo de 30% de vida sofre 50 dano extra, recarga 18 s.

### Viúva de Bronze
- Lâmina Filamentar: 32 dano, alcance 1.9 U, intervalo 1 s.
- Cabo de Tração: 4.8 U; puxa inimigo leve 2.2 U ou puxa a Viúva até alvo pesado; 16 dano, recarga 8 s.
- Giro de Lâminas: 22 dano/s em 1.8 U por 2 s e -25% velocidade, recarga 13 s.
- Retaliação de Bronze: bloqueia dano por 0.6 s e responde com 45 dano, recarga 15 s.

### Cão de Cinzas
- Mordida Carbonizada: 36 dano, alcance 1.55 U, intervalo 1.15 s.
- Investida Incandescente: até 4 U e 38 dano; contra obstáculo, autoatordoa por 0.75 s; recarga 10 s.
- Rastro de Cinzas: faixa de 1.2 U × 5 U por 4 s, 10 dano/s e -40% cura, recarga 14 s.
- Explosão da Matilha: 55 dano em 1.6 U contra alvo marcado ou queimando, recarga 18 s.

## Regras de balanceamento
- Dano comum: 16 a 40; alto impacto: 45 a 65.
- Recargas curtas: 8 a 10 s; controle forte ou área: 12 a 18 s.
- Empurrão máximo: 2.2 U.
- Atordoamento máximo no protótipo: 0.75 s.
- Nenhuma unidade fica alta em dano, mobilidade e resistência ao mesmo tempo.

## Mapa inicial
**Vale das Coroas Quebradas:** bases em cantos opostos, dois Obeliscos laterais e um central entre Ruínas Arcanas; Santuário Central de alto risco; gargalos no Bosque Petrificado e rotas alternativas pelo Mar de Cinzas.

## Vertical slice
- 1 tabuleiro 7 x 7.
- 2 Arquimagos e 4 unidades.
- 3 terrenos: Bosque Petrificado, Necrópole e Mar de Cinzas.
- 1 arena modular com 3 variações.
- IA local e transição tabuleiro → arena → tabuleiro.
- Vitória por Arquimago derrotado ou domínio de 2 Obeliscos por 2 turnos.

## Godot 4
- `Board`: hexágonos, turnos, neblina, objetivos e estado da partida.
- `Arena`: combate, IA, obstáculos e condições de vitória.
- `MatchState` autoload: unidades, vida, recursos, território e cicatrizes entre cenas.
- `Resources`: Arquimago, unidade, habilidade, terreno e arena.

## Ordem de implementação
1. Tabuleiro, seleção e turnos.
2. Vida, visão e ocupação.
3. Combate numérico provisório.
4. Arena com um combatente controlável por lado.
5. Retorno com dano, ocupação e cicatriz.
6. IA.
7. Obeliscos, Éter e vitórias.
8. Habilidades, variação de arena, animações e arte.

## Limite de escopo
No protótipo, cada arena terá atacante, defensor e no máximo um reforço por lado. O ciclo a provar é: mover, encontrar, cair na arena, vencer e ver o mapa mudar.
