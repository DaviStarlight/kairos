# 14 — Entrega Final Executiva

---

## 1. Resumo Executivo do Produto

**KAIRÓS** é um jogo de estratégia abstrata original para 2 jogadores, projetado para ser o primeiro jogo de tabuleiro estratégico digital-native com potencial de se tornar referência no gênero.

**Proposta:** Um jogo com a profundidade do xadrez, acessibilidade superior e mecânicas inéditas — especialmente o **Sistema Press** (mover 2 peças por turno ao custo de mobilidade futura), que cria um eixo estratégico que não existe em nenhum outro jogo abstrato.

**Mercado:** O boom do xadrez digital (Chess.com: 100M+ contas) provou que há demanda massiva por jogos de estratégia. Mas nenhum novo jogo abstrato surgiu como alternativa real. Kairós preenche essa lacuna com IP proprietária, mecânicas inovadoras e design de produto moderno.

**Modelo de negócio:** Free-to-play com monetização cosmética. Jogo completo gratuito; receita de skins, temas, passe de temporada e assinatura premium de analytics.

**Diferencial competitivo:**
- Sistema Press (tempo como recurso estratégico)
- Ataque à Distância (captura sem movimento)
- Muralha de Escudos (imunidade condicional)
- Captura direta do Arconte (sem xeque — decisivo)
- IP proprietária (controle de balance, marca, evolução)

**Métricas-alvo (12 meses):** 50k MAU, D1 >40%, $15k/mês receita.

---

## 2. Manual Resumido de Regras

### Setup
- Tabuleiro 8×8, 12 peças por jogador (6 tipos), posição inicial simétrica

### Peças e Movimentação
| Peça (Qtd) | Movimento | Especial |
|---|---|---|
| **Arconte (1)** | 1 casa, qualquer dir. | Nunca pode ser Pressado |
| **Strategos (1)** | Até 3 casas, qualquer dir. | Peça mais poderosa |
| **Hoplita (2)** | Até 2 casas, ortogonal | Muralha: 2 Hoplitas adj. = invulneráveis |
| **Toxotes (2)** | Até 2 casas, diagonal | Ataque à Distância: captura a 2 casas sem se mover |
| **Hippeus (2)** | L (2+1 ou 3+1), salta | Investida: +1 casa após capturar (pode capturar de novo) |
| **Doríforo (4)** | 1 frente (2 no 1º mov.) | Promoção na última linha |

### Turno
1. **Recuperar** peças Exaustas
2. **Mover** 1 peça (obrigatório)
3. **Press** (opcional): mover 2ª peça (≠ Arconte), que fica Exausta

### Vitória
Capturar o Arconte adversário. Sem aviso de "xeque".

### Empate
Material insuficiente, 50 turnos sem captura, repetição tripla, ou acordo mútuo.

---

## 3. Pitch de Mercado

### Elevator Pitch (30 segundos)
> "Kairós é o primeiro jogo de estratégia abstrata criado para a era digital. Imagine xadrez, mas você pode mover duas peças por turno — ao custo de uma delas ficar temporariamente indisponível. Essa mecânica, o Press, cria uma dimensão de timing que nenhum jogo abstrato possui. Combinado com arqueiros que atiram à distância, escudeiros que formam muralhas invulneráveis e cavalaria com ataques duplos — Kairós é tão profundo quanto xadrez, mas mais acessível, mais decisivo e mais emocionante de assistir."

### Pitch Expandido (2 minutos)

> O xadrez tem 1500 anos e continua dominante. A pergunta que guiou a criação de Kairós foi: **por que nenhum novo jogo de estratégia abstrata se estabeleceu desde então?**
>
> A resposta: porque ninguém criou um jogo com profundidade real E inovação mecânica genuína. Kairós resolve isso com o **Sistema Press** — a possibilidade de mover 2 peças por turno, ao custo de uma ficar temporariamente indisponível. Essa mecânica transforma o tempo em recurso estratégico, algo que não existe em nenhum jogo abstrato. Quando Pressionar? Quando conservar? Quando explorar a Exaustão do adversário? Essas decisões são o coração do jogo.
>
> Mas o Press é só o começo. Kairós tem **Ataque à Distância** (arqueiros capturam sem se mover), **Muralha de Escudos** (dois soldados adjacentes ficam invulneráveis), **Investida** (cavalaria ataca duas vezes) e **captura direta** do líder (sem aviso de xeque — o que reduz empates para menos de 10%).
>
> O jogo é free-to-play, mobile-first, com partidas de 15-30 minutos (ou 3 minutos em Blitz). O modelo de negócio é monetização cosmética sem comprometer a integridade competitiva.
>
> O mercado está pronto: Chess.com tem 100 milhões de contas. O interesse por jogos de estratégia nunca foi tão alto. Mas todas as plataformas disputam o mesmo jogo de domínio público. **Kairós é uma IP proprietária** — podemos controlar balance, evoluir as regras, criar marca e ecossistema.
>
> Estamos buscando construir o jogo de estratégia abstrata definitivo da era digital.

---

## 4. Roadmap Resumido (Formato Executivo)

| Fase | Meses | Objetivo | Entregável-Chave | Marco |
|---|---|---|---|---|
| **1. Fundação** | M1-M2 | Validar regras | 50+ playtests documentados | Rules v1.1 |
| **2. Protótipo** | M2-M4 | Jogo jogável digital | Engine + IA + interface básica | **Alpha** |
| **3. Polimento** | M4-M6 | Produto visual completo | Tutorial, IA 3 níveis, identidade visual | **Beta Fechado** |
| **4. Multiplayer** | M6-M8 | Jogar online | WebSocket, auth, salas | **Beta Aberto** |
| **5. Competitivo** | M8-M10 | Ranqueada funcional | Elo, matchmaking, leaderboard | **Lançamento v1.0** |
| **6. Analytics** | M8-M12 | Dados reais | Dashboards, event pipeline | Decisões data-driven |
| **7. Expansão** | M10-M15 | Retenção + receita | Puzzles, torneios, cosméticos, passe | **v2.0** |
| **8. Escala** | M15-M24 | Ecossistema global | API, IA avançada, multirregião, 1M MAU | **v3.0** |

---

## 5. Sugestão de Backlog Inicial de Desenvolvimento

### Epics

| # | Epic | Prioridade | Estimativa |
|---|---|---|---|
| E1 | Engine de Regras (@kairos/engine) | P0 | 3-4 semanas |
| E2 | Renderização do Tabuleiro (Canvas) | P0 | 2-3 semanas |
| E3 | Interação (selecionar, mover, capturar) | P0 | 2 semanas |
| E4 | Sistema Press (UX + lógica) | P0 | 1-2 semanas |
| E5 | Habilidades (Muralha, Ranged, Investida, Promoção) | P0 | 2 semanas |
| E6 | IA Básica (minimax α-β) | P0 | 2-3 semanas |
| E7 | Tutorial Interativo | P1 | 2 semanas |
| E8 | Interface de Partida (HUD, relógio, histórico) | P1 | 2 semanas |
| E9 | Identidade Visual + Animações | P1 | 3 semanas |
| E10 | Backend + Auth + Perfil | P1 | 2 semanas |
| E11 | WebSocket (multiplayer) | P1 | 3 semanas |
| E12 | Matchmaking + Fila | P1 | 2 semanas |
| E13 | Sistema de Elo (Glicko-2) | P1 | 1 semana |
| E14 | Leaderboard | P2 | 1 semana |
| E15 | Event Tracking (analytics) | P2 | 2 semanas |
| E16 | Puzzles Diários | P2 | 2 semanas |
| E17 | Cosméticos + Loja | P3 | 2-3 semanas |
| E18 | Passe de Temporada | P3 | 2 semanas |
| E19 | Torneios | P3 | 3 semanas |
| E20 | IA Avançada (MCTS/Neural) | P3 | 4-6 semanas |

### User Stories (E1 — Engine de Regras)

| # | User Story | Critério de Aceite |
|---|---|---|
| US1 | Como engine, represento o estado do tabuleiro 8×8 com peças posicionadas | Board state serializável, posição inicial correta |
| US2 | Como engine, calculo todos os movimentos legais para cada peça | Testes unitários para cada tipo de peça, edge cases |
| US3 | Como engine, valido se um movimento é legal | Rejeita movimentos ilegais, aceita legais |
| US4 | Como engine, executo um movimento e atualizo o estado | Estado consistente após cada movimento |
| US5 | Como engine, implemento o Sistema Press (Fase 3 do turno) | Press correto, Exaustão marcada, Arconte protegido |
| US6 | Como engine, implemento Recuperação de Exaustão (Fase 1) | Exaustas recuperam no início do turno |
| US7 | Como engine, detecto Muralha de Escudos ativa | 2 Hoplitas adj. ort. → imunes a captura |
| US8 | Como engine, implemento Ataque à Distância | Toxotes captura a 2 casas, linha de visão, sem mover |
| US9 | Como engine, implemento Investida | Hippeus: +1 casa após captura, pode capturar |
| US10 | Como engine, implemento Promoção | Doríforo na última linha → escolha de tipo |
| US11 | Como engine, detecto vitória (captura do Arconte) | Jogo termina imediatamente |
| US12 | Como engine, detecto condições de empate | Material, repetição, 50 turnos |
| US13 | Como engine, gero notação KGN para cada turno | Notação legível e parseável |

---

## 6. MVP Técnico com Prioridades

### MVP Scope (Alpha — Mês 3-4)

```
Must Have (P0):
├── @kairos/engine (regras 100% corretas com testes)
├── Tabuleiro Canvas renderizado
├── Interação: tocar peça → ver movimentos → tocar destino → executar
├── Indicadores visuais: turno, Exaustão, Muralha ativa
├── Detecção de vitória/derrota/empate
├── IA básica (minimax profundidade 3)
└── Modo Hot Seat (2 jogadores, 1 tela)

Should Have (P1 — para Beta):
├── Tutorial (5 lições interativas)
├── 3 níveis de IA
├── Animações suaves de movimento e captura
├── Relógio de partida
├── Histórico de movimentos
└── Identidade visual (cores, ícones, tipografia)

Won't Have (adiado):
├── Multiplayer online
├── Contas de usuário
├── Matchmaking
├── Ranking
├── Cosméticos
├── Puzzles
├── Torneios
└── Analytics
```

### Definição de Pronto (DoD) para MVP
- [ ] Todas as regras implementadas e testadas (>200 test cases)
- [ ] IA funcional em 3 níveis
- [ ] Tutorial de 5 lições com >85% taxa de conclusão em testes
- [ ] Performance: 60 FPS em dispositivos móveis médios
- [ ] Tempo de carga <3s
- [ ] 0 bugs críticos em regras após 100 partidas de teste
- [ ] Responsivo: funciona em mobile (320px+) e desktop

---

## 7. Próximos Passos para Construir o Projeto Imediatamente

### Sprint 0 — Setup (1 semana)

| # | Tarefa | Responsável |
|---|---|---|
| 1 | Criar monorepo com Turborepo | Dev |
| 2 | Setup `packages/engine` com TypeScript + Vitest | Dev |
| 3 | Setup `apps/web` com React + Vite + Canvas | Dev |
| 4 | Definir CI com GitHub Actions (lint + test + build) | Dev |
| 5 | Criar kit de playtesting físico (imprimir tabuleiro, recortar peças) | Design/Produto |
| 6 | Jogar 10 partidas de playtesting e documentar resultados | Equipe |

### Sprint 1 — Engine Core (2 semanas)

| # | Tarefa |
|---|---|
| 1 | Implementar representação do tabuleiro (Board class) |
| 2 | Implementar movimentação de cada peça (6 tipos) |
| 3 | Implementar cálculo de movimentos legais |
| 4 | Implementar captura por deslocamento |
| 5 | Implementar Sistema Press + Exaustão + Recuperação |
| 6 | Escrever >100 testes unitários para regras |

### Sprint 2 — Habilidades + Vitória (2 semanas)

| # | Tarefa |
|---|---|
| 1 | Implementar Muralha de Escudos |
| 2 | Implementar Ataque à Distância |
| 3 | Implementar Investida (incluindo captura dupla) |
| 4 | Implementar Promoção |
| 5 | Implementar detecção de vitória/derrota/empate |
| 6 | Implementar notação KGN |
| 7 | Completar testes (>200 test cases) |

### Sprint 3 — Interface + IA (2 semanas)

| # | Tarefa |
|---|---|
| 1 | Renderizar tabuleiro 8×8 em Canvas |
| 2 | Renderizar peças com ícones diferenciados |
| 3 | Implementar interação: seleção + movimento + Press |
| 4 | Implementar indicadores visuais (Exaustão, Muralha, turnos) |
| 5 | Implementar IA minimax com avaliação posicional |
| 6 | Integrar engine + canvas + IA em fluxo de jogo completo |

### Sprint 4 — Polimento MVP (2 semanas)

| # | Tarefa |
|---|---|
| 1 | Tutorial interativo (5 lições) |
| 2 | Animações de movimento e captura |
| 3 | Efeitos sonoros básicos |
| 4 | Tela inicial, menu, seleção de modo (vs IA fácil/médio/difícil) |
| 5 | Tela de vitória/derrota com resumo |
| 6 | Responsividade mobile |
| 7 | Testes de usabilidade com 5 pessoas |
| 8 | **RELEASE ALPHA** |

### Após Alpha

1. **Validar com 20-50 jogadores** → métricas de retenção e feedback qualitativo
2. **Iterar regras** se necessário (balance baseado em dados do playtesting)
3. **Iniciar backend** (auth, WebSocket, matchmaking)
4. **Beta fechado** com multiplayer
5. **Beta aberto** com ranking
6. **Lançamento público v1.0**

---

## Conclusão

Kairós não é um conceito — é um projeto com regras testáveis, arquitetura definida, roadmap executável e modelo de negócio validável. O próximo passo é abrir o editor, criar o repositório e começar a Sprint 0.

O momento oportuno é agora. *Kairós.*
