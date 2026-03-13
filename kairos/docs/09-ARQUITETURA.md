# 09 — Arquitetura Técnica Recomendada

---

## Visão Geral da Arquitetura

```
┌─────────────────────────────────────────────────────────────────┐
│                         CLIENTES                                │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐                      │
│  │ Web PWA  │  │   iOS    │  │ Android  │                      │
│  │ React+   │  │  (PWA ou │  │ (PWA ou  │                      │
│  │ Canvas   │  │  nativo) │  │  nativo) │                      │
│  └────┬─────┘  └────┬─────┘  └────┬─────┘                      │
│       │              │              │                            │
│       └──────────────┼──────────────┘                            │
│                      │                                           │
│              HTTPS + WebSocket (WSS)                             │
└──────────────────────┼───────────────────────────────────────────┘
                       │
┌──────────────────────┼───────────────────────────────────────────┐
│                  API GATEWAY / LOAD BALANCER                     │
│              (Nginx / Cloudflare / AWS ALB)                      │
└──────────────────────┼───────────────────────────────────────────┘
                       │
        ┌──────────────┼──────────────┐
        │              │              │
┌───────┴───┐  ┌───────┴───┐  ┌──────┴────┐
│  REST API │  │ WebSocket │  │  Worker   │
│  (Auth,   │  │  Server   │  │ (Puzzles, │
│  Profile, │  │ (Matches, │  │  Engine,  │
│  Ranking) │  │  Real-    │  │  Events)  │
│           │  │  time)    │  │           │
│ Node.js + │  │ Node.js + │  │ Node.js / │
│ Express   │  │ Socket.io │  │ Python    │
└─────┬─────┘  └─────┬─────┘  └─────┬─────┘
      │               │              │
      └───────────────┼──────────────┘
                      │
        ┌─────────────┼─────────────┐
        │             │             │
  ┌─────┴────┐ ┌──────┴───┐ ┌──────┴──────┐
  │PostgreSQL│ │  Redis   │ │ClickHouse / │
  │ (dados   │ │ (cache,  │ │ BigQuery    │
  │ persist.)│ │ sessões, │ │ (analytics) │
  │          │ │ fila,    │ │             │
  │          │ │ matchmk.)│ │             │
  └──────────┘ └──────────┘ └─────────────┘
```

---

## Stack Frontend

### Tecnologias

| Camada | Tecnologia | Justificativa |
|---|---|---|
| **Framework** | React 18+ (ou Next.js para SSR/SEO) | Ecossistema maduro, componentes reutilizáveis, grande pool de devs |
| **Renderização do tabuleiro** | HTML5 Canvas (via Konva.js ou PixiJS) | Performance superior a DOM para animações de peças |
| **Estado** | Zustand (ou Jotai) | Leve, sem boilerplate, perfeito para game state |
| **WebSocket** | Socket.io-client | Reconexão automática, rooms nativas, fallback para polling |
| **Estilização** | Tailwind CSS + CSS Modules | Produtividade + escopo de estilos |
| **Animações** | Framer Motion (UI) + Canvas nativo (tabuleiro) | Animações suaves sem comprometer performance |
| **PWA** | Workbox | Caching, offline support, instalação |
| **Testes** | Vitest + Testing Library + Playwright (E2E) | Rápido, integrado com Vite, testes de ponta a ponta |
| **Build** | Vite | Build rápido, HMR, tree-shaking |

### Estrutura do Frontend

```
src/
├── app/                    # Rotas e layouts (Next.js) ou páginas (React Router)
├── components/
│   ├── board/              # Tabuleiro, casas, peças, animações
│   ├── hud/                # HUD da partida (relógio, turnos, peças capturadas)
│   ├── lobby/              # Seleção de modo, matchmaking
│   ├── profile/            # Perfil do jogador, stats
│   ├── tutorial/           # Componentes do tutorial
│   └── ui/                 # Componentes genéricos (botões, modais, etc.)
├── engine/                 # Game logic PURA (compartilhada com backend)
│   ├── board.ts            # Estado do tabuleiro
│   ├── moves.ts            # Cálculo de movimentos legais
│   ├── rules.ts            # Validação de regras
│   ├── press.ts            # Lógica de Press/Exaustão
│   ├── abilities.ts        # Muralha, Ataque à Distância, Investida
│   ├── promotion.ts        # Promoção de Doríforos
│   ├── victory.ts          # Detecção de vitória/derrota/empate
│   └── notation.ts         # Notação KGN (Kairós Game Notation)
├── ai/                     # IA client-side (para modo offline)
│   ├── minimax.ts          # Minimax com alpha-beta pruning
│   ├── evaluation.ts       # Função de avaliação posicional
│   └── mcts.ts             # Monte Carlo Tree Search
├── hooks/                  # React hooks customizados
├── services/               # API client, WebSocket client
├── stores/                 # Estado global (Zustand)
├── types/                  # TypeScript types/interfaces
└── utils/                  # Utilitários
```

### Engine de Regras Compartilhada
O módulo `engine/` é **isomórfico** — roda tanto no client quanto no server. Isso garante:
- Client pode prever movimentos (UX responsiva) sem esperar server
- Server valida tudo (segurança) usando a mesma lógica
- Zero divergência entre regras do client e server
- Publicado como pacote NPM interno: `@kairos/engine`

---

## Stack Backend

### Tecnologias

| Camada | Tecnologia | Justificativa |
|---|---|---|
| **Runtime** | Node.js 20+ (LTS) | Mesmo ecossistema do frontend, TypeScript compartilhado |
| **REST API** | Express.js (ou Fastify para performance) | Maduro, extensível, middleware rico |
| **WebSocket** | Socket.io | Rooms, namespaces, reconexão, scaling via adapter |
| **Validação** | Zod | Type-safe validation compartilhada com frontend |
| **ORM** | Prisma | Type-safe queries, migrations, boa DX |
| **Auth** | Passport.js + JWT | Flexível, múltiplos providers |
| **Job Queue** | BullMQ (Redis-backed) | Jobs assíncronos: analytics, puzzles, notificações |
| **Testes** | Vitest + Supertest | Unitários + integração API |

### Estrutura do Backend

```
server/
├── src/
│   ├── api/                # REST endpoints
│   │   ├── auth/           # Login, registro, OAuth
│   │   ├── users/          # Perfil, stats
│   │   ├── matches/        # Histórico, replay
│   │   ├── rankings/       # Leaderboard, elo
│   │   ├── puzzles/        # Desafios diários
│   │   └── tournaments/    # CRUD torneios
│   ├── ws/                 # WebSocket handlers
│   │   ├── matchmaking.ts  # Fila de matchmaking
│   │   ├── game-room.ts    # Sala de partida (estado, turnos, sincronia)
│   │   ├── spectator.ts    # Espectador
│   │   └── chat.ts         # Mensagens pré-definidas
│   ├── engine/             # @kairos/engine (importado como pacote)
│   ├── services/
│   │   ├── elo.ts          # Cálculo Glicko-2
│   │   ├── matchmaker.ts   # Algoritmo de matchmaking
│   │   ├── anti-cheat.ts   # Validação de jogadas, detecção de anomalias
│   │   └── analytics.ts    # Event tracking
│   ├── jobs/               # BullMQ workers
│   │   ├── elo-update.ts   # Atualizar elo pós-partida
│   │   ├── puzzle-gen.ts   # Gerar puzzles diários
│   │   └── event-flush.ts  # Flush eventos para data warehouse
│   ├── middleware/          # Auth, rate limiting, error handling
│   ├── config/             # Configs, env vars
│   └── types/              # Tipos compartilhados
├── prisma/
│   └── schema.prisma       # Schema do banco
└── tests/
```

---

## Banco de Dados

### PostgreSQL (dados transacionais)
- **Por quê:** ACID, JSON support, full-text search, extensões (pg_trgm para busca), confiável
- **Uso:** Users, matches, rankings, tournaments, achievements, cosmetics
- **Scaling:** Read replicas para queries de leaderboard. Partitioning por data para matches antigas.

### Redis (cache, sessões, real-time)
- **Por quê:** Sub-millisecond latency, pub/sub, sorted sets
- **Uso:**
  - Cache de leaderboard (sorted set com elo como score)
  - Sessões de WebSocket
  - Fila de matchmaking (sorted set com elo + tempo de espera)
  - Cache de partidas ativas (game state)
  - Rate limiting
  - Lock distribuído (para matchmaking)

### ClickHouse ou BigQuery (analytics)
- **Por quê:** Colunar, otimizado para queries analíticas sobre bilhões de eventos
- **Uso:** Todos os eventos analíticos, dashboards, queries ad-hoc
- **Decisão:** ClickHouse self-hosted (custo menor, controle) vs. BigQuery managed (menos ops)
- **Recomendação inicial:** BigQuery (managed, serverless, escala sem ops)

---

## Multiplayer Architecture

### Server-Authoritative Model
O servidor é a **fonte única de verdade** para o estado do jogo:

```
CLIENT A                   SERVER                    CLIENT B
   │                         │                          │
   │──── move(d2→d4) ──────→│                          │
   │                         │ ← valida com engine/    │
   │                         │    rules.ts              │
   │                         │                          │
   │← state_update ─────────│──── state_update ───────→│
   │                         │                          │
   │   (client renderiza     │   (client renderiza      │
   │    novo estado)         │    novo estado)           │
```

1. Client envia **intenção** de jogada (peça, destino, press?)
2. Server valida com `@kairos/engine`
3. Se válida: atualiza estado, broadcast para ambos os clients
4. Se inválida: rejeita, envia estado correto ao client

### Reconexão
- Client guarda `matchId` em localStorage
- Ao reconectar, envia `rejoin(matchId)` ao server
- Server reenvia o estado completo da partida
- Relógio pausa por até 30s durante reconexão
- Se jogar não reconecta em 60s: perde por abandono

---

## Autenticação

### Métodos
| Método | Prioridade | Implementação |
|---|---|---|
| Google OAuth 2.0 | P0 | Passport.js strategy |
| Email + senha | P0 | bcrypt + JWT |
| Apple Sign-in | P1 | Passport.js strategy |
| Conta anônima (guest) | P0 | JWT temporário, upgrade para conta completa |

### Segurança
- JWT com expiração curta (15 min) + refresh token (7 dias)
- Refresh token em httpOnly cookie (não acessível por JS)
- Rate limiting: 10 requests/min para login, 100/min para API geral
- CSRF protection para cookies
- Senhas: bcrypt com cost factor 12
- 2FA opcional (TOTP) para contas de alto elo

---

## Observabilidade

| Camada | Ferramenta | Uso |
|---|---|---|
| **Logs** | Pino (estruturado) → enviado para Grafana Loki ou Datadog | Debugging, auditoria |
| **Métricas** | Prometheus + Grafana | Latência de API, WebSocket connections, queue depth |
| **Tracing** | OpenTelemetry → Jaeger ou Tempo | Rastrear request flow (client → API → DB) |
| **Alerting** | Grafana Alerting ou PagerDuty | Latência >500ms, error rate >1%, WebSocket disconnects |
| **Uptime** | Pingdom ou BetterUptime | Status page pública |

### Métricas Chave para Monitorar

| Métrica | Threshold de Alerta |
|---|---|
| API response time P95 | >500ms |
| WebSocket message latency P95 | >200ms |
| Error rate (5xx) | >1% |
| Active WebSocket connections | >80% do limite |
| Redis memory | >75% |
| PostgreSQL connection pool | >80% |
| Matchmaking queue time P95 | >60s |
| CPU usage | >70% sustained |

---

## Deploy e Infraestrutura

### Recomendação Inicial (custo-eficiente)

| Componente | Plataforma | Custo Estimado |
|---|---|---|
| Frontend | Vercel ou Cloudflare Pages | Free tier → $20/mês |
| REST API | Railway ou Render | $7-25/mês |
| WebSocket Server | Railway ou Fly.io | $7-25/mês |
| PostgreSQL | Supabase ou Neon | Free tier → $25/mês |
| Redis | Upstash | Free tier → $10/mês |
| Analytics | BigQuery | Free tier → $10/mês |
| CDN | Cloudflare | Free |
| DNS | Cloudflare | Free |

**Custo total inicial: $0-50/mês** (free tiers + baixo tráfego)

### Escala (10k+ usuários simultâneos)

| Componente | Plataforma |
|---|---|
| Frontend | CDN (Cloudflare/CloudFront) |
| API + WS | AWS ECS Fargate ou GCP Cloud Run (auto-scaling) |
| PostgreSQL | AWS RDS ou GCP Cloud SQL (read replicas) |
| Redis | AWS ElastiCache ou GCP Memorystore (cluster) |
| Analytics | BigQuery (serverless, escala infinita) |
| Infra as Code | Terraform |
| Container Registry | AWS ECR ou GCP Artifact Registry |

---

## Escalabilidade

### Horizontal Scaling
- **REST API:** Stateless — escala adicionando instâncias atrás de load balancer
- **WebSocket:** Socket.io Redis adapter — compartilha rooms entre instâncias
- **Workers:** BullMQ — múltiplos workers consumindo da mesma fila
- **DB reads:** Read replicas para leaderboard e queries pesadas

### Vertical Considerations
- **Engine de IA:** Computação intensiva — pode precisar de instâncias maiores ou GPU para rede neural
- **Puzzle generation:** CPU-intensive — rodar em worker dedicado

---

## Segurança

| Área | Medida |
|---|---|
| **Input validation** | Zod em TODAS as entradas (API + WebSocket) |
| **SQL injection** | Prisma (query parametrizado) — NUNCA raw SQL sem parametrização |
| **XSS** | React escapa por padrão; CSP headers; sanitize em chat |
| **CSRF** | SameSite cookies + CSRF token |
| **Rate limiting** | express-rate-limit + Redis (distribuído) |
| **DoS via WS** | Limite de mensagens/segundo por socket (10/s) |
| **Cheating** | Server-authoritative; toda jogada validada server-side |
| **Data privacy** | LGPD/GDPR: consent, data export, delete account |
| **Secrets** | Variáveis de ambiente, NUNCA no código. Vault para produção. |
| **Dependencies** | Dependabot + npm audit regular |
| **HTTPS** | Forçado em todas as rotas (HSTS) |

---

## Versionamento e Branching

### Git Strategy
- **main:** Produção — sempre deployável
- **develop:** Branch de integração para próximo release
- **feature/xxx:** Feature branches com PR para develop
- **hotfix/xxx:** Correções urgentes, merge direto para main + develop

### Monorepo vs Multi-repo
**Recomendação: Monorepo** (Turborepo ou Nx)

```
kairos/
├── packages/
│   └── engine/           # @kairos/engine — game logic compartilhada
├── apps/
│   ├── web/              # Frontend React
│   ├── api/              # REST API
│   ├── ws/               # WebSocket server
│   └── worker/           # Background jobs
├── prisma/               # Schema compartilhado
├── turbo.json            # Turborepo config
└── package.json          # Workspace root
```

**Vantagens:**
- `@kairos/engine` compartilhado entre client e server com 0 overhead
- CI/CD unificado
- Atomic commits quando engine + client + server mudam juntos
- Dependency management centralizado

---

## Testes

| Tipo | Ferramenta | Cobertura Alvo | Foco |
|---|---|---|---|
| **Unit** | Vitest | >90% para `engine/` | Regras do jogo, movimentos, edge cases |
| **Integration** | Vitest + Supertest | >70% para API | Endpoints, auth, matchmaking |
| **E2E** | Playwright | Fluxos críticos | Tutorial, jogar partida, matchmaking |
| **Load** | k6 | N/A | WebSocket connections, API throughput |
| **Snapshot** | Vitest | Engine states | Posições do jogo |

### Test Cases Críticos para Engine

```
✓ Arconte move 1 casa em todas as 8 direções
✓ Arconte não pode ser Pressado
✓ Strategos move até 3 casas, bloqueado por peças
✓ Hoplita move até 2 casas ortogonalmente
✓ Muralha ativa quando 2 Hoplitas adjacentes ortogonalmente
✓ Muralha impede captura (todas as peças)
✓ Muralha se desfaz quando Hoplita se move
✓ Toxotes move até 2 casas na diagonal
✓ Ataque à Distância: alcance 2, linha de visão, sem movimento
✓ Ataque à Distância bloqueado por peça intermediária
✓ Hippeus move em L (2+1) e Grande L (3+1)
✓ Hippeus salta sobre peças
✓ Investida: +1 casa após captura, pode capturar
✓ Investida não encadeia (máximo 2 capturas)
✓ Doríforo move para frente (1 ou 2 no primeiro move)
✓ Doríforo captura na diagonal frontal
✓ Promoção obrigatória na última linha
✓ Press: segunda peça movida, fica Exausta
✓ Press: peça Exausta não pode ser movida/pressada
✓ Press: Arconte não pode ser Press target
✓ Recuperação: Exausta → Pronta no início do turno
✓ Vitória por captura do Arconte (todas as formas)
✓ Empate por material insuficiente
✓ Empate por repetição tripla
✓ Empate pela regra dos 50 movimentos
```

---

## CI/CD

### Pipeline

```
Push/PR → Lint → Type Check → Unit Tests → Integration Tests → Build → Deploy Preview
                                                                          │
Merge to main → (same pipeline) → E2E Tests → Deploy Staging → Smoke Tests → Deploy Production
```

### Ferramentas
| Etapa | Ferramenta |
|---|---|
| CI/CD | GitHub Actions |
| Lint | ESLint + Prettier |
| Type check | TypeScript (strict mode) |
| Tests | Vitest + Playwright |
| Build | Turborepo (cached builds) |
| Deploy Preview | Vercel (frontend) |
| Deploy Prod | GitHub Actions → Railway/Fly.io (backend) |
| Database Migrations | Prisma migrate (com review em PRs) |

---

## Modelagem de Dados Base

### Diagrama ER Simplificado

```
users ─────────┬───── matches (via match_players)
               │
               ├───── rankings
               │
               ├───── achievements
               │
               └───── sessions

matches ───────┬───── match_turns
               │
               ├───── match_players
               │
               └───── match_events (analytics)

puzzles ───────┬───── puzzle_attempts
               │
               └───── users (via puzzle_attempts)

tournaments ───┬───── tournament_participants
               │
               └───── tournament_rounds
```

### Eventos que Precisam ser Rastreados desde o Início
Mesmo no MVP, os seguintes eventos devem ser emitidos (para armazenar e analisar depois):

| Evento | Dados | Por quê |
|---|---|---|
| `session_started` | user_id, platform, version | Contabilizar DAU/MAU |
| `tutorial_started` | user_id, lesson_id | Medir onboarding |
| `tutorial_completed` | user_id, lesson_id, duration | Medir onboarding |
| `match_started` | match_id, players, mode, time_control | Volume de partidas |
| `move_played` | match_id, turn, piece, from, to, is_press, is_capture | Replay + analytics |
| `ability_used` | match_id, turn, ability_type | Balanceamento |
| `match_finished` | match_id, winner, reason, turns, duration | Win rate, duração |
| `rematch_requested` | match_id, user_id | Retenção |
| `puzzle_started` | user_id, puzzle_id | Engajamento |
| `puzzle_completed` | user_id, puzzle_id, correct, time | Engajamento |
