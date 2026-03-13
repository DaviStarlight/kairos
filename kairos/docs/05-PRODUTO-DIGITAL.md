# 05 — Design de Produto Digital

---

## Visão de Produto

Kairós não é apenas um jogo de tabuleiro — é uma **plataforma de estratégia competitiva** projetada desde o dia zero para escalar como produto digital com retenção de longo prazo, comunidade ativa e economia sustentável.

---

## Versões do Produto

### MVP (v0.1 — Minimum Viable Product)

**Objetivo:** Validar se as regras funcionam e se jogadores querem jogar novamente.

| Feature | Inclusão | Prioridade |
|---|---|---|
| Tabuleiro 8×8 funcional | ✅ | P0 |
| 6 tipos de peças com movimentação | ✅ | P0 |
| Sistema Press completo | ✅ | P0 |
| Muralha de Escudos | ✅ | P0 |
| Ataque à Distância | ✅ | P0 |
| Investida | ✅ | P0 |
| Promoção | ✅ | P0 |
| Detecção de vitória/derrota | ✅ | P0 |
| Jogo local (2 jogadores, tela dividida) | ✅ | P0 |
| IA básica (nível fácil-médio) | ✅ | P0 |
| Tutorial mínimo (regras básicas) | ✅ | P1 |
| Histórico de movimentos | ✅ | P1 |
| Desfazer jogada (modo casual/treino) | ✅ | P2 |
| Relógio de xadrez | ❌ | Adiado |
| Multiplayer online | ❌ | Adiado |
| Contas de usuário | ❌ | Adiado |
| Cosméticos | ❌ | Adiado |

**Plataforma:** Web (React/Canvas), acessível por mobile e desktop.

**Métrica de sucesso:** >60% dos testadores jogam pelo menos 3 partidas consecutivas.

---

### Versão Intermediária (v1.0 — Launch)

**Objetivo:** Produto público com capacidade multiplayer e retenção.

| Feature | Prioridade |
|---|---|
| Tudo do MVP | P0 |
| Multiplayer online (WebSocket) | P0 |
| Sistema de contas (email/Google/Apple) | P0 |
| Matchmaking básico (casual) | P0 |
| Relógio de partida (Bullet/Blitz/Rapid/Standard) | P0 |
| Tutorial interativo guiado (5 lições) | P0 |
| Perfil do jogador (stats básicos) | P1 |
| Histórico de partidas | P1 |
| Elo/rating básico | P1 |
| 3 níveis de IA (Fácil/Médio/Difícil) | P1 |
| Desafio diário (puzzle) | P2 |
| Notificações (desafio, convite) | P2 |
| Modo espectador | P2 |

**Plataforma:** Web + PWA mobile.

**Métricas de sucesso:**
- Retenção D1 > 40%
- Retenção D7 > 20%
- Taxa de rematch > 30%
-  NPS > 40

---

### Versão Avançada (v2.0 — Competitive)

**Objetivo:** Ecossistema competitivo completo.

| Feature | Prioridade |
|---|---|
| Tudo da v1.0 | P0 |
| Partidas ranqueadas com elo | P0 |
| Leaderboard global | P0 |
| Temporadas (3 meses) | P0 |
| Torneios automatizados | P1 |
| Análise pós-partida (engine) | P1 |
| Replay de partidas | P1 |
| Sistema anti-smurf/anti-cheat | P1 |
| Passe de temporada (cosméticos) | P2 |
| Loja de cosméticos | P2 |
| Clube/equipe | P2 |
| Sistema social (amigos, convites) | P2 |

---

## Visão de Longo Prazo

```
ANO 1: Validação + Lançamento (MVP → v1.0)
   └── Provar product-market fit, comunidade core
   
ANO 2: Competitivo + Crescimento (v1.0 → v2.0)
   └── Elo, torneios, temporadas, monetização, 100k MAU
   
ANO 3: Ecossistema + Escala (v2.0 → v3.0)
   └── IA avançada, API pública, SDK torneios, parcerias esports, 1M MAU
   
ANO 4+: Plataforma + IP
   └── Variantes oficiais, versão física premium, conteúdo educacional, franquia
```

---

## Diferenciais para Mercado Casual e Competitivo

| Casual | Competitivo |
|---|---|
| Partidas de 3 min (Bullet) | Partidas de 30 min (Standard) |
| IA para treinar | Matchmaking por elo |
| Puzzles diários (5 min/dia) | Torneios semanais |
| Cosméticos desbloquáveis | Ranking + Temporadas |
| Tutorial interativo | Análise de partida com engine |
| Sem pressão de rating | Leaderboard global |
| Desafios temáticos | Anti-cheat rigoroso |

---

## Formas de Retenção

### Curto Prazo (sessão)
1. **Press feedback** — som/vibração satisfatória no Press
2. **Animação de vitória** — celebração visual ao capturar o Arconte
3. **Botão de rematch** — 1 clique para jogar novamente
4. **"Perto de subir de nível"** — barra de progresso visível

### Médio Prazo (semanal)
1. **Desafio diário** — puzzle tático novo a cada dia
2. **Missões semanais** — "Vença 3 partidas usando Investida", "Forme Muralha 5x"
3. **Temporada** — progressão com recompensas cosméticas
4. **Ranking dinâmico** — ver evolução do elo

### Longo Prazo (mensal+)
1. **Sistema de maestria** — títulos permanentes baseados em conquistas
2. **Estatísticas profundas** — gráficos de evolução, taxa de vitória por peça, por abertura
3. **Comunidade** — clubes, torneios recorrentes, fóruns
4. **Conteúdo educacional** — lições de estratégia, análise de partidas de top players

---

## Loop Principal de Engajamento

```
┌──────────────────────────────────────────────────────────┐
│                                                          │
│    JOGAR ──→ RESULTADO ──→ APRENDER ──→ PROGREDIR       │
│     ↑                                        │           │
│     └────────────────────────────────────────┘           │
│                                                          │
│    Jogar: Encontrar partida (10s)                        │
│    Resultado: Vitória/Derrota (15-30 min)                │
│    Aprender: Análise pós-partida, puzzles                │
│    Progredir: Elo sobe, missão completa, reward          │
│                                                          │
└──────────────────────────────────────────────────────────┘
```

### Detalhamento do Loop

1. **Descoberta** → Tutorial, primeira partida contra IA
2. **Hook** → Vitória na primeira partida (IA fácil), satisfação de uma jogada bem feita
3. **Hábito** → Desafio diário, missões semanais, notificação "Seu amigo está online"
4. **Investimento** → Elo, estatísticas, cosméticos desbloqueados, histórico
5. **Recompensa Variável** → Resultado incerto de cada partida, puzzles variados
6. **Social** → Clubes, amigos, torneios, espectador

---

## Progressão do Jogador

### Sistema de Ranking (Elo)

| Faixa | Elo | Título | % Jogadores |
|---|---|---|---|
| Bronze | 0–799 | Doríforo | ~30% |
| Prata | 800–1199 | Hoplita | ~30% |
| Ouro | 1200–1599 | Toxotes | ~20% |
| Platina | 1600–1899 | Hippeus | ~12% |
| Diamante | 1900–2199 | Strategos | ~5% |
| Mestre | 2200–2499 | Arconte | ~2% |
| Grande Mestre | 2500+ | Kairós | ~1% |

### Sistema de Maestria (permanente)

Conquistas que nunca são perdidas:
- **Primeiro kairós** — Vença por captura direta do Arconte
- **Investida Dupla** — Capture 2 peças em 1 turno com Hippeus
- **Muralha Inabalável** — Mantenha Muralha por 10 turnos consecutivos
- **Tiro Certeiro** — Vença com Ataque à Distância ao Arconte
- **Pressão Máxima** — Vença uma partida fazendo Press em 5+ turnos consecutivos

---

## Onboarding

### Estrutura do Tutorial (5 lições, ~15 min total)

| Lição | Conteúdo | Duração | Mecânica |
|---|---|---|---|
| 1. **Primeiros Passos** | Tabuleiro, Arconte, movimentação básica, vitória | 3 min | Mover e capturar com Arconte e Strategos |
| 2. **O Exército** | Hoplitas, Toxotai, Hippeis, Doríforos | 4 min | Mini-puzzles com cada peça |
| 3. **O Press** | Como Pressionar, custo de Exaustão | 3 min | Puzzle: use Press para criar ameaça dupla |
| 4. **Poderes Especiais** | Muralha, Ataque à Distância, Investida, Promoção | 3 min | Puzzle: use cada habilidade |
| 5. **Primeira Batalha** | Partida completa vs IA fácil (guiada) | 2 min | IA perde de propósito se necessário |

### Métricas de Onboarding
- Taxa de conclusão de cada lição
- Tempo por lição
- Taxa de erro por puzzle
- Drop-off entre lições
- Conversão: tutorial → primeira partida real

---

## Desafios e Missões

### Desafios Diários (Puzzles)
Posições de jogo com 1 solução ótima:
- "Capture o Arconte em 1 turno"
- "Capture o Arconte em 2 turnos (com Press)"
- "Forme Muralha de Escudos e sobreviva 3 turnos"
- "Use Ataque à Distância para vencer"

Dificuldade escala com o elo do jogador.

### Missões Semanais
| Tipo | Exemplo | Recompensa |
|---|---|---|
| Vitórias | "Vença 5 partidas esta semana" | 50 XP |
| Mecânica | "Use Investida 3 vezes" | Cosmético aleatório |
| Exploração | "Jogue com cada modo de tempo" | 30 XP |
| Social | "Convide 1 amigo para jogar" | Ícone exclusivo |

---

## Perfil de Usuário e Jornadas

### Persona 1: "O Casual Curioso" (Ana, 24)
- Joga no ônibus, 15 min por sessão
- Quer partidas rápidas contra IA ou casual
- Motivada por puzzles diários e desbloqueáveis
- **Jornada:** Tutorial → IA Fácil → Partida casual → Puzzle diário → Missões

### Persona 2: "O Competitivo Dedicado" (Lucas, 29)
- Joga 1h por dia, busca melhorar elo
- Quer partidas ranqueadas e análise pós-jogo
- Motivado por ranking e temporadas
- **Jornada:** Ranqueada → Análise → Puzzle avançado → Ranqueada → Leaderboard

### Persona 3: "O Social Streamer" (Felipe, 22)
- Joga para criar conteúdo e interagir
- Quer torneios, espectador, cosméticos
- Motivado por comunidade e personalização
- **Jornada:** Torneio → Stream → Custom match → Cosméticos → Clip compartilhado

### Persona 4: "O Estrategista Analítico" (Mariana, 35)
- Ex-jogadora de xadrez, busca profundidade
- Quer análise de engine, estatísticas, teoria de aberturas
- Motivada por domínio e compreensão
- **Jornada:** Ranqueada → Análise detalhada → Estudo de aberturas → Partida de teste → Repetir
