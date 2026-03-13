# 08 — Expansões e Features Futuras

---

## Leaderboard Global

### Design
- **Top 100** global com ranking atualizado em tempo real
- **Top 100 regional** (América do Sul, América do Norte, Europa, Ásia, Oceania)
- **Leaderboard mensal** (reset no início de cada mês — quem joga mais recente rankeia)
- **Leaderboard de temporada** (rankings que determinam recompensas ao final)

### Dados Exibidos
Nome, avatar, elo, faixa, país, partidas jogadas, win rate, maior sequência de vitórias.

### Anti-Manipulação
- Elo mínimo para aparecer no leaderboard (ex: 50 partidas ranqueadas)
- Detecção de wintrading (padrões de matchup repetitivo)
- Contas com menos de 14 dias não aparecem no top 100

---

## Ranking por Elo

### Sistema Glicko-2
- **Rating inicial:** 1200 ± 350 RD (Rating Deviation)
- **K-factor dinâmico:** Alto nos primeiros 20 jogos (placement), estabiliza depois
- **Volatility:** Mede consistência — jogadores erráticos têm mais volatilidade
- **Placement matches:** 10 partidas iniciais para calibrar (elo oculto durante placement)

### Divisões

| Faixa | Elo | Ícone | Cor |
|---|---|---|---|
| Bronze I-III | 0-799 | Lança partida | Cobre |
| Prata I-III | 800-1199 | Escudo | Prata |
| Ouro I-III | 1200-1599 | Arco | Dourado |
| Platina I-III | 1600-1899 | Cavalo | Azul cristal |
| Diamante I-III | 1900-2199 | Espada | Diamante |
| Mestre | 2200-2499 | Coroa | Púrpura |
| Grande Mestre | 2500+ | Kairós (sol + ampulheta) | Preto & Dourado |

---

## Modos de Jogo

### Por Tempo
| Modo | Tempo/Jogador | Incremento | Público |
|---|---|---|---|
| Bullet | 1 min | +1s | Ultra-casual, adrenalina |
| Blitz | 3 min | +2s | Casual rápido |
| Rapid | 10 min | +5s | Padrão competitivo |
| Standard | 25 min | +10s | Competitivo sério |
| Correspondência | 24h/movimento | - | Assíncrono |

### Modos Especiais
| Modo | Regra | Rotação |
|---|---|---|
| **Sem Press** | Press desativado. Volta ao xadrez clássico de 1 movimento por turno. | Permanente |
| **Press Duplo** | Os dois jogadores podem Pressionar — ambas as peças ficam Exaustas. | Evento |
| **Blitz Arconte** | Só o Arconte pode capturar. Todas as outras peças apenas bloqueiam/posicionam. | Evento |
| **Espelho** | Ambos veem o tabuleiro do mesmo lado. Quem joga Prata vê invertido. | Evento |
| **Contagem Regressiva** | 30 turnos para capturar o Arconte. Se ninguém capturar, vence quem tem mais material. | Evento |
| **Fog of War** | Peças inimigas >3 casas de distância de qualquer peça sua ficam ocultas. | Evento mensal |

---

## Desafios Diários

### Estrutura
- 1 puzzle novo por dia, disponível por 24h
- 3 níveis de dificuldade (rodam entre fácil/médio/difícil)
- Tempo para resolver exibido no leaderboard de puzzle
- Sequência de dias consecutivos ("streak") com recompensas

### Tipos de Puzzle
| Tipo | Descrição |
|---|---|
| **Kairós em 1** | Capture o Arconte em 1 turno (com ou sem Press) |
| **Kairós em 2** | Capture o Arconte em 2 turnos (adversário joga otimamente) |
| **Kairós em 3** | Capture em 3 turnos |
| **Defesa** | Adversário ameaça seu Arconte. Encontre a defesa que salva. |
| **Melhor Press** | Qual é o Press ótimo nesta posição? |
| **Promoção** | Avance e promova o Doríforo de forma a criar ameaça irresistível |

### Recompensas
- 1 acerto → 5 XP
- 7 dias seguidos → Emote especial
- 30 dias seguidos → Borda de perfil "Disciplinado"

---

## Temporadas

### Estrutura
- Duração: **3 meses** (4 temporadas/ano)
- Nomes temáticos: "Temporada da Falanx", "Temporada do Kairós", "Temporada da Sombra", "Temporada da Ascensão"
- Elo soft-reset: reduzido em 25% em direção a 1200 (ex: 1800 → 1650)
- Placement matches no início de cada temporada

### Recompensas de Temporada
| Faixa Alcançada | Recompensa |
|---|---|
| Bronze | Ícone de participação |
| Prata | Borda de Prata |
| Ouro | Borda + Emote exclusivo |
| Platina | Borda + Skin de peça |
| Diamante | Borda + Tema de tabuleiro |
| Mestre | Borda + Título permanente |
| Grande Mestre | Borda animada + Titulo + Skin exclusiva |

---

## Replay e Análise

### Replay
- Gravação automática de todas as partidas (server-side)
- Navegação turno-a-turno com controles de player de vídeo
- Seta de avançar/retroceder turno
- Possibilidade de compartilhar replay via link
- Exportar partida em notação Kairós (KGN — Kairós Game Notation)

### Análise Automática
- Engine analisa cada movimento e classifica como:
  - ✅ **Ótimo** — a melhor jogada ou equivalente
  - 🟢 **Bom** — jogada forte, pode não ser a melhor
  - 🟡 **Imprecisão** — perdeu uma oportunidade menor
  - 🟠 **Erro** — jogada claramente inferior
  - 🔴 **Blunder** — jogada que perde material ou o jogo
- Resumo de acurácia da partida (% de jogadas ótimas/boas)
- Sugestão de "melhor Press" em cada turno
- Detecção de ameaças não percebidas ao Arconte

---

## IA Adversária

### Níveis Planejados

| Nível | Elo Equivalente | Algoritmo | Tempo de Resposta |
|---|---|---|---|
| Tutorial | ~400 | Random semi-aleatório (favorece jogadas legais não-suicidas) | Instantâneo |
| Fácil | ~600 | Minimax α-β, profundidade 2 | <1s |
| Médio | ~1000 | Minimax α-β, profundidade 4 + evaluação posicional | <2s |
| Difícil | ~1400 | MCTS (Monte Carlo Tree Search) + heurísticas | <3s |
| Expert | ~1800 | MCTS + rede neural treinada por self-play | <5s |
| Master | ~2200+ | Rede neural profunda (AlphaZero-style) | <5s |

### Treinamento da IA
- Self-play com reinforcement learning
- Avaliação por torneio interno (níveis de IA jogando entre si)
- Calibração contra jogadores humanos de elo conhecido

---

## Torneios

### Tipos
| Tipo | Formato | Jogadores | Duração |
|---|---|---|---|
| **Arena** | Round-robin contínuo (tempo limitado) | Ilimitado | 1-2h |
| **Swiss** | Pareamento Swiss (rounds fixos) | 8-64 | 2-4h |
| **Eliminação** | Single/Double elimination | 8-256 | 2-6h |
| **Copa Semanal** | Swiss → Top 8 Eliminação | 32-128 | Sábado, 3h |

### Features de Torneio
- Inscrição com 1 clique
- Pareamento automático
- Relógio padronizado por torneio
- Leaderboard de torneio ao vivo
- Prêmios: XP, cosméticos exclusivos, pontos de campeonato
- Spectator mode para partidas do torneio

---

## Social

### Sistema de Amigos
- Adicionar amigo por username ou link
- Lista de amigos com status online/offline/em partida
- Desafio direto com 1 clique
- Histórico de confronto direto (head-to-head record)

### Clubes/Equipes
- Criar clube (nome, logo, descrição)
- Convidar membros (até 50)
- Leaderboard interno do clube
- "Club Wars" — torneios entre clubes
- Chat de clube

### Espectador
- Assistir partidas ao vivo de amigos ou jogadores do top 100
- Delay de 1 turno (para evitar coaching em tempo real)
- Chat de espectador
- Reações (equivalente a "clap" em momentos brilhantes)

### Chat In-Game
- **Sem text chat livre** (previne toxicidade)
- Mensagens pré-definidas:
  - "Boa jogada!"
  - "Bem jogado"
  - "Oops!"
  - "Pensei que tinha visto tudo..."
  - "Kairós!" (equivalente a "Xeque-mate!")
  - "Rematch?"
- Emotes desbloqueáveis via temporada/loja

---

## Matchmaking Inteligente

### Parâmetros
1. **Elo** — prioridade máxima (diff <200, expande com tempo de fila)
2. **Volatility** — prioriza jogadores com volatilidade similar
3. **Região** — prioriza menor latência
4. **Tempo na fila** — expande busca a cada 10s
5. **Comportamento** — jogadores com muitos abandonos matcham entre si (shadow queue)

### Anti-Smurf
- Placement matches com K-factor alto (sobe rápido se winrate alta)
- Detecção: conta nova com >80% winrate em 20+ jogos → flag para revisão
- Se detectado: acelerar elo para nível real (não banir)
- Novas contas não podem jogar ranqueada antes de 5 partidas casuais

---

## Balance Patches

### Filosofia
- Kairós é um jogo de regras fixas (como xadrez), mas com possibilidade de micro-ajustes numéricos
- Patches são raros (1-2 por ano) e apenas se dados mostram desequilíbrio claro

### Tipos de Ajuste Possíveis
| Ajuste | Exemplo | Quando Aplicar |
|---|---|---|
| Alcance de peça | Strategos: 3→2 casas | Se win rate de jogadores com Strategos vivo é >60% |
| Custo de Exaustão | 1 turno → 2 turnos | Se Press é usado em >70% dos turnos |
| Condição de Muralha | Ortogonal → Ortogonal ou diagonal | Se Muralha é usada em <10% das partidas |
| Regra de promoção | Qualquer peça → apenas de peças capturadas | Se promoção é dominante demais |

### Processo
1. Dados indicam problema
2. Análise de game design
3. Teste interno com ajuste
4. Beta patch (servidor de teste)
5. Release com notas de patch

---

## Eventos Especiais

### Tipos
| Evento | Frequência | Descrição |
|---|---|---|
| **Festival do Kairós** | Anual | Torneio global, cosméticos exclusivos, desafios especiais |
| **Modo Especial do Mês** | Mensal | Modo de jogo rotativo (Fog of War, Press Duplo, etc.) |
| **Desafio de Comunidade** | Bimestral | Meta coletiva (ex: comunidade joga 1M partidas = recompensa para todos) |
| **Marco Histórico** | Ad-hoc | Quando atingir marcos (100k partidas, 10k jogadores, etc.) |

---

## Cosméticos e Personalização

### Categorias
| Categoria | Exemplos | Rarity |
|---|---|---|
| **Temas de Tabuleiro** | Mármore, Obsidiana, Floresta, Oceano, Neon | Comum → Épico |
| **Skins de Peças** | Clássicas, Cristal, Sombra, Fogo, Gelo | Comum → Lendário |
| **Bordas de Perfil** | Ranking, Temporada, Conquista | Varia |
| **Avatares** | Personagens gregos, símbolos abstratos | Comum → Raro |
| **Emotes** | Animações de reação in-game | Raro → Épico |
| **Efeitos de Captura** | Partículas no momento da captura | Épico → Lendário |
| **Efeitos de Vitória** | Animação especial de "Kairós!" | Lendário |

### Obtenção
- **Grátis:** Temporadas, conquistas, missões, puzzles
- **Compra:** Loja (itens individuais ou pacotes)
- **Passe de Temporada:** Trilha gratuita + trilha premium

---

## Passe de Temporada

### Estrutura
- **30 níveis** de progressão por temporada (3 meses)
- XP ganho por: partidas (vitória/derrota), puzzles, missões
- **Trilha gratuita:** A cada 5 níveis, 1 recompensa (cosmético comum, XP boost)
- **Trilha premium:** Todos os níveis desbloqueiam recompensa (cosméticos raros, temas, skins, emotes)
- Preço sugerido: $4.99/temporada

### Recompensas (exemplo Temporada 1)
| Nível | Gratuito | Premium |
|---|---|---|
| 1 | - | Avatar exclusivo |
| 5 | Ícone Bronze | Emote "Kairós!" |
| 10 | - | Tema "Mármore Grego" |
| 15 | 100 XP | Skin "Peças de Cristal" |
| 20 | - | Borda "Temporada 1" |
| 25 | Ícone Especial | Efeito de captura "Fogo Sagrado" |
| 30 | - | Efeito de vitória "Ascensão do Arconte" |
