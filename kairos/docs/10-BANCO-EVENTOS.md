# 10 — Estrutura de Banco de Dados e Eventos Analíticos

---

## Modelagem de Dados (Prisma Schema)

### Entidade: users

```prisma
model User {
  id            String   @id @default(cuid())
  email         String?  @unique
  username      String   @unique
  displayName   String
  avatarUrl     String?
  passwordHash  String?  // null se OAuth-only
  provider      String   @default("email") // email, google, apple
  providerId    String?
  
  elo           Int      @default(1200)
  eloDeviation  Float    @default(350)
  eloVolatility Float    @default(0.06)
  peakElo       Int      @default(1200)
  
  totalWins     Int      @default(0)
  totalLosses   Int      @default(0)
  totalDraws    Int      @default(0)
  
  currentStreak Int      @default(0)
  bestStreak    Int      @default(0)
  
  role          String   @default("player") // player, moderator, admin
  
  createdAt     DateTime @default(now())
  updatedAt     DateTime @updatedAt
  lastLoginAt   DateTime?
  
  // Relações
  matchPlayers    MatchPlayer[]
  rankings        Ranking[]
  achievements    UserAchievement[]
  sessions        Session[]
  puzzleAttempts  PuzzleAttempt[]
  cosmetics       UserCosmetic[]
  friendsFrom     Friendship[]  @relation("friendFrom")
  friendsTo       Friendship[]  @relation("friendTo")
}
```

### Entidade: matches

```prisma
model Match {
  id             String   @id @default(cuid())
  
  mode           String   // casual, ranked, tournament, puzzle_duel
  timeControl    String   // bullet_1_1, blitz_3_2, rapid_10_5, standard_25_10
  
  status         String   // waiting, active, finished, abandoned
  result         String?  // gold_win, silver_win, draw
  winReason      String?  // archon_capture, resignation, timeout, abandonment
  
  totalTurns     Int      @default(0)
  durationMs     Int?     // duração total em milliseconds
  
  pressCount     Int      @default(0)   // total de Press na partida
  captureCount   Int      @default(0)   // total de capturas
  
  startedAt      DateTime @default(now())
  finishedAt     DateTime?
  
  tournamentId   String?
  
  // Relações
  players        MatchPlayer[]
  turns          MatchTurn[]
  events         MatchEvent[]
  tournament     Tournament?    @relation(fields: [tournamentId], references: [id])
  
  @@index([status])
  @@index([mode, startedAt])
  @@index([finishedAt])
}
```

### Entidade: match_players

```prisma
model MatchPlayer {
  id           String  @id @default(cuid())
  
  matchId      String
  userId       String
  
  color        String  // gold, silver
  
  eloBefore    Int
  eloAfter     Int?
  eloChange    Int?
  
  result       String? // win, loss, draw
  
  timeSpentMs  Int     @default(0)  // tempo total gasto pensando
  pressCount   Int     @default(0)  // quantas vezes fez Press
  capturesMade Int     @default(0)
  piecesLost   Int     @default(0)
  
  // Relações
  match        Match   @relation(fields: [matchId], references: [id])
  user         User    @relation(fields: [userId], references: [id])
  
  @@unique([matchId, userId])
  @@unique([matchId, color])
  @@index([userId, result])
}
```

### Entidade: match_turns

```prisma
model MatchTurn {
  id              String  @id @default(cuid())
  
  matchId         String
  turnNumber      Int     // 1, 2, 3...
  playerColor     String  // gold, silver
  
  // Movimento Principal
  pieceType       String  // archon, strategos, hoplite, toxotes, hippeus, doryphoros
  fromSquare      String  // ex: "d2"
  toSquare        String  // ex: "d4"
  isCapture       Boolean @default(false)
  capturedPiece   String? // tipo da peça capturada
  
  // Habilidade usada
  abilityUsed     String? // ranged_strike, charge, shield_wall_formed, shield_wall_broken
  chargeTarget    String? // casa do alvo extra da Investida
  chargeCapture   Boolean @default(false)
  
  // Press
  pressUsed       Boolean @default(false)
  pressPieceType  String? // tipo da peça Pressada
  pressFrom       String? // casa de origem do Press
  pressTo         String? // casa de destino do Press
  pressCapture    Boolean @default(false)
  pressCaptured   String? // tipo da peça capturada no Press
  pressAbility    String? // habilidade usada no Press
  
  // Promoção
  promotionType   String? // tipo para o qual o Doríforo foi promovido
  
  // Metadados
  thinkTimeMs     Int?    // tempo que o jogador levou para fazer o movimento
  notation        String  // notação KGN do turno completo
  
  // Board state (para replay eficiente)
  boardStateFen   String? // estado do tabuleiro após o turno (formato compacto)
  
  // Relações
  match           Match   @relation(fields: [matchId], references: [id])
  
  @@unique([matchId, turnNumber])
  @@index([matchId])
}
```

### Entidade: rankings

```prisma
model Ranking {
  id          String   @id @default(cuid())
  
  userId      String
  season      Int      // 1, 2, 3...
  
  elo         Int
  peakElo     Int
  tier        String   // bronze, silver, gold, platinum, diamond, master, grandmaster
  
  wins        Int      @default(0)
  losses      Int      @default(0)
  draws       Int      @default(0)
  
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
  
  user        User     @relation(fields: [userId], references: [id])
  
  @@unique([userId, season])
  @@index([season, elo(sort: Desc)])
}
```

### Entidade: game_modes

```prisma
model GameMode {
  id          String   @id @default(cuid())
  
  slug        String   @unique  // casual, ranked, bullet, blitz, rapid, standard
  name        String
  description String
  
  isRanked    Boolean  @default(false)
  isActive    Boolean  @default(true)
  
  timeBase    Int?     // tempo base em segundos (null = sem relógio)
  timeIncrement Int?   // incremento por turno em segundos
  
  createdAt   DateTime @default(now())
}
```

### Entidade: puzzles

```prisma
model Puzzle {
  id          String   @id @default(cuid())
  
  difficulty  String   // easy, medium, hard
  type        String   // kairos_in_1, kairos_in_2, kairos_in_3, defense, best_press
  
  boardState  String   // posição inicial do puzzle (FEN-like)
  solution    String   // sequência de jogadas corretas (KGN)
  
  title       String?
  description String?
  
  publishDate DateTime?
  isDaily     Boolean  @default(false)
  
  attempts    PuzzleAttempt[]
  
  @@index([publishDate, isDaily])
  @@index([difficulty, type])
}
```

### Entidade: puzzle_attempts

```prisma
model PuzzleAttempt {
  id          String   @id @default(cuid())
  
  puzzleId    String
  userId      String
  
  solved      Boolean
  timeMs      Int      // tempo para resolver
  attempts    Int      // quantas tentativas
  
  createdAt   DateTime @default(now())
  
  puzzle      Puzzle   @relation(fields: [puzzleId], references: [id])
  user        User     @relation(fields: [userId], references: [id])
  
  @@unique([puzzleId, userId])
}
```

### Entidade: achievements

```prisma
model Achievement {
  id          String   @id @default(cuid())
  
  slug        String   @unique
  name        String
  description String
  iconUrl     String?
  
  condition   String   // JSON com critérios de desbloquear
  rarity      String   // common, rare, epic, legendary
  
  users       UserAchievement[]
}

model UserAchievement {
  id             String   @id @default(cuid())
  
  userId         String
  achievementId  String
  
  unlockedAt     DateTime @default(now())
  
  user           User        @relation(fields: [userId], references: [id])
  achievement    Achievement @relation(fields: [achievementId], references: [id])
  
  @@unique([userId, achievementId])
}
```

### Entidade: sessions

```prisma
model Session {
  id          String   @id @default(cuid())
  
  userId      String
  
  platform    String   // web, ios, android
  version     String   // app version
  userAgent   String?
  ipCountry   String?  // país (geolocalizado, anonimizado)
  
  startedAt   DateTime @default(now())
  endedAt     DateTime?
  durationMs  Int?
  
  user        User     @relation(fields: [userId], references: [id])
  
  @@index([userId, startedAt])
}
```

### Entidade: tournaments

```prisma
model Tournament {
  id          String   @id @default(cuid())
  
  name        String
  type        String   // arena, swiss, elimination
  status      String   // upcoming, active, finished
  
  timeControl String
  maxPlayers  Int?
  currentRound Int     @default(0)
  totalRounds  Int?
  
  startsAt    DateTime
  endsAt      DateTime?
  
  matches     Match[]
  participants TournamentParticipant[]
}

model TournamentParticipant {
  id            String  @id @default(cuid())
  
  tournamentId  String
  userId        String
  
  score         Float   @default(0)
  wins          Int     @default(0)
  losses        Int     @default(0)
  draws         Int     @default(0)
  
  placement     Int?    // posição final
  
  tournament    Tournament @relation(fields: [tournamentId], references: [id])
  
  @@unique([tournamentId, userId])
}
```

### Entidade: cosmetics e inventário

```prisma
model Cosmetic {
  id          String   @id @default(cuid())
  
  slug        String   @unique
  name        String
  category    String   // board_theme, piece_skin, border, avatar, emote, capture_effect, victory_effect
  rarity      String   // common, rare, epic, legendary
  
  assetUrl    String
  previewUrl  String?
  
  price       Int?     // null = não comprável (só via reward)
  seasonId    Int?     // null = disponível sempre
  
  users       UserCosmetic[]
}

model UserCosmetic {
  id          String   @id @default(cuid())
  
  userId      String
  cosmeticId  String
  
  equipped    Boolean  @default(false)
  acquiredAt  DateTime @default(now())
  acquiredVia String   // purchase, season_pass, achievement, mission, gift
  
  user        User     @relation(fields: [userId], references: [id])
  cosmetic    Cosmetic @relation(fields: [cosmeticId], references: [id])
  
  @@unique([userId, cosmeticId])
}
```

### Social

```prisma
model Friendship {
  id        String   @id @default(cuid())
  
  fromId    String
  toId      String
  status    String   // pending, accepted, blocked
  
  createdAt DateTime @default(now())
  
  from      User     @relation("friendFrom", fields: [fromId], references: [id])
  to        User     @relation("friendTo", fields: [toId], references: [id])
  
  @@unique([fromId, toId])
}
```

---

## Eventos Analíticos

### Nomenclatura
- Snake_case: `match_started`, `move_played`
- Formato: `{domínio}_{ação}` ex: `match_started`, `tutorial_completed`
- Cada evento tem: `event_id` (UUID), `timestamp`, `user_id`, `session_id`, `platform`, `version`

### Catálogo de Eventos

#### Session & Auth

| Evento | Propriedades | Dashboard |
|---|---|---|
| `session_started` | platform, version, country | Retenção, DAU/MAU |
| `session_ended` | duration_ms, screens_visited | Engajamento |
| `signup_completed` | provider (email/google/apple) | Funil |
| `login_completed` | provider | Retenção |

#### Tutorial

| Evento | Propriedades | Dashboard |
|---|---|---|
| `tutorial_started` | lesson_id | Funil, Comportamento |
| `tutorial_step_completed` | lesson_id, step, duration_ms | Comportamento |
| `tutorial_step_failed` | lesson_id, step, error_type | Comportamento |
| `tutorial_completed` | lesson_id, total_duration_ms | Funil, Retenção |
| `tutorial_abandoned` | lesson_id, last_step | Funil |

#### Match

| Evento | Propriedades | Dashboard |
|---|---|---|
| `match_started` | match_id, mode, time_control, player_elos | Partidas |
| `match_finished` | match_id, winner_color, reason, turns, duration_ms, press_count, capture_count | Partidas, Balance |
| `match_abandoned` | match_id, abandoner_color, turn_number, reason | Partidas, Comportamento |
| `rematch_requested` | match_id, requester_color | Retenção |
| `rematch_accepted` | match_id, new_match_id | Retenção |

#### Gameplay (por turno)

| Evento | Propriedades | Dashboard |
|---|---|---|
| `move_played` | match_id, turn, color, piece, from, to, is_capture, captured_piece, think_time_ms | Balance, Replay |
| `press_used` | match_id, turn, press_piece, press_from, press_to, press_capture | Balance |
| `ability_used` | match_id, turn, ability (ranged/charge/shield_wall), details | Balance |
| `promotion_chosen` | match_id, turn, promoted_to | Balance |
| `archon_threatened` | match_id, turn, threatening_piece, threat_type | Balance, Comportamento |

#### Competitive

| Evento | Propriedades | Dashboard |
|---|---|---|
| `ranked_queue_joined` | user_id, elo, mode | Competitivo |
| `ranked_queue_left` | user_id, wait_time_ms, reason (found/timeout/cancel) | Competitivo |
| `elo_changed` | user_id, old_elo, new_elo, match_id | Competitivo, Performance |
| `tier_changed` | user_id, old_tier, new_tier, direction (up/down) | Competitivo |
| `leaderboard_viewed` | user_id, leaderboard_type (global/regional/friends) | Engajamento |

#### Puzzle

| Evento | Propriedades | Dashboard |
|---|---|---|
| `puzzle_started` | user_id, puzzle_id, difficulty, type | Engajamento |
| `puzzle_attempt` | user_id, puzzle_id, attempt_number, correct | Engajamento |
| `puzzle_completed` | user_id, puzzle_id, correct, time_ms, attempts | Engajamento |
| `puzzle_abandoned` | user_id, puzzle_id, time_spent_ms | Engajamento |

#### Social

| Evento | Propriedades | Dashboard |
|---|---|---|
| `friend_added` | user_id, friend_id | Social, Retenção |
| `friend_match_started` | user_id, friend_id, match_id | Social |
| `club_joined` | user_id, club_id | Social |
| `spectate_started` | user_id, match_id | Engajamento |

#### Monetização (futuro)

| Evento | Propriedades | Dashboard |
|---|---|---|
| `store_viewed` | user_id, category | Monetização |
| `item_purchased` | user_id, item_id, price, currency | Monetização |
| `season_pass_purchased` | user_id, season_id, price | Monetização |
| `season_pass_level_up` | user_id, season_id, level | Monetização |

---

## Como Eventos Alimentam Dashboards

### Fluxo de Dados

```
Client → Event API → Message Queue (Redis/Kafka) → Consumer → Data Warehouse (BigQuery)
                                                                        │
                                                                   Dashboard Tool
                                                                   (Metabase/Looker)
```

### Mapeamento Evento → Insight → Decisão

| Evento | Insight | Decisão de Produto |
|---|---|---|
| `tutorial_abandoned` (lesson 3, step 2 = Press) | Press é difícil de entender no tutorial | Simplificar explicação do Press, adicionar gif animado |
| `match_finished` (win_reason = archon_capture por ranged_strike, frequência >20%) | Ataque à Distância está capturando Arcontes demais | Possível nerf: reduzir alcance ou bloquear Arconte como alvo de Ranged |
| `press_used` (frequência <15% dos turnos) | Press está subutilizado | Melhorar tutorial de Press, adicionar puzzles focados em Press |
| `elo_changed` (distribuição bimodal) | Matchmaking não está separando bem os jogadores | Ajustar parâmetros do Glicko-2 ou ampliar placement |
| `session_ended` (duração <2 min) | Jogadores abrindo e saindo sem jogar | Investigar: onboarding confuso? Performance? Bug? |
| `rematch_requested` (taxa >40% após derrota) | Jogadores derrotados querem jogar de novo (bom sinal) | Destacar botão de rematch, tornar mais visível |
| `puzzle_completed` (taxa <30% no "hard") | Puzzles hard estão difíceis demais | Recalibrar dificuldade ou adicionar hints |
| `match_abandoned` (turno <5) | Jogadores desistindo cedo | Possíveis causas: matchmaking ruim, UI confusa, conexão |
