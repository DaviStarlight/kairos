# 11 — UX/UI e Experiência do Jogador

---

## Princípios de Design

| Princípio | Aplicação |
|---|---|
| **Clareza acima de tudo** | O estado do jogo deve ser lido em <2 segundos: de quem é o turno, quais peças estão Exaustas, quem está vencendo |
| **Mobile-first** | Projetado para toque em tela de 5-6"; desktop é adaptação, não o contrário |
| **Zero decoração desnecessária** | Cada pixel serve um propósito: informação, feedback ou identidade |
| **Feedback imediato** | Toda ação tem resposta visual e sonora em <100ms |
| **Acessibilidade** | Contraste WCAG AA, indicadores não dependem só de cor, texto legível |

---

## Identidade Visual

### Paleta de Cores

| Uso | Cor | Hex |
|---|---|---|
| Fundo principal | Grafite escuro | `#1A1A2E` |
| Fundo secundário | Azul noturno | `#16213E` |
| Acento principal | Dourado Grego | `#D4A843` |
| Acento secundário | Prata Olímpico | `#B8C5D6` |
| Ouro (jogador) | Dourado quente | `#F0C040` |
| Prata (jogador) | Azul prateado | `#A8B8CC` |
| Sucesso/Vitória | Verde esmeralda | `#2ECC71` |
| Perigo/Derrota | Vermelho terracota | `#E74C3C` |
| Press/Exaustão | Âmbar | `#F39C12` |
| Muralha de Escudos | Azul céu intenso | `#3498DB` |

### Tipografia
- **Títulos:** Cinzel (serif, remete à Grécia) ou Playfair Display
- **Corpo:** Inter ou DM Sans (sans-serif, legível em qualquer tamanho)
- **Monospace (notação):** JetBrains Mono

### Iconografia das Peças
Estilo: **silhuetas minimalistas** com traço geométrico, inspiradas em cerâmica grega (black-figure pottery).

| Peça | Silhueta |
|---|---|
| Arconte | Perfil de capacete ateniense com crista |
| Strategos | Espada cruzada com manto |
| Hoplita | Escudo Aspis (redondo com lambda) |
| Toxotes | Arco tensionado com flecha |
| Hippeus | Cavalo em posição de galope |
| Doríforo | Lança vertical com escudo pequeno |

---

## Fluxo de Telas

```
┌─────────────┐
│  SPLASH     │ → Logo Kairós + loading
└──────┬──────┘
       │
┌──────▼──────┐
│  HOME       │ → Hub principal
│  ┌────────┐ │
│  │ JOGAR  │ │ → Modo de jogo
│  │ PUZZLE │ │ → Desafio diário
│  │ PERFIL │ │ → Stats e cosméticos
│  │ SOCIAL │ │ → Amigos e clubes
│  │ LOJA   │ │ → Cosméticos (futuro)
│  └────────┘ │
└──────┬──────┘
       │
┌──────▼──────┐     ┌─────────────┐
│  MODO SELECT│ ──→ │  MATCHMAKING│ → Fila de espera
│  (Casual,   │     │  (animação  │
│   Ranked,   │     │   de busca) │
│   vs IA,    │     └──────┬──────┘
│   Amigo)    │            │
└─────────────┘     ┌──────▼──────┐
                    │  PARTIDA    │ → Tabuleiro + HUD
                    │  (core      │
                    │   gameplay) │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │  RESULTADO  │ → Vitória/Derrota + Stats
                    │  ┌────────┐ │
                    │  │REMATCH │ │
                    │  │ANÁLISE │ │
                    │  │ HOME   │ │
                    │  └────────┘ │
                    └─────────────┘
```

---

## Tela Inicial (Home)

### Layout (Mobile)

```
┌─────────────────────────────┐
│  ★ KAIRÓS                ⚙  │  ← Logo + Settings
│                              │
│  ┌─────────────────────────┐ │
│  │  Elo: 1247  🥇 Ouro II │ │  ← Rating badge
│  │  W:45  L:38  D:2       │ │
│  └─────────────────────────┘ │
│                              │
│  ┌─────────────────────────┐ │
│  │  ▶ JOGAR                │ │  ← CTA principal (botão grande)
│  └─────────────────────────┘ │
│                              │
│  ┌────────┐ ┌──────────────┐ │
│  │ PUZZLE │ │ vs IA        │ │  ← Botões secundários
│  │ DIÁRIO │ │              │ │
│  └────────┘ └──────────────┘ │
│                              │
│  ┌─────────────────────────┐ │
│  │ 📊 Missões: 2/5         │ │  ← Progresso semanal
│  │ ████████░░░░ 40%        │ │
│  └─────────────────────────┘ │
│                              │
│  ┌─────────────────────────┐ │
│  │ 🏆 Temporada 1: Nv 12   │ │  ← Passe de temporada
│  │ █████████░░░ Próx: Emote│ │
│  └─────────────────────────┘ │
│                              │
│  ┌──┐ ┌──┐ ┌──┐ ┌──┐ ┌──┐  │
│  │🏠│ │⚔│ │🧩│ │👤│ │🏪│  │  ← Bottom nav
│  └──┘ └──┘ └──┘ └──┘ └──┘  │
└─────────────────────────────┘
```

### Detalhes UX
- **Botão JOGAR** é o elemento dominante — 1 toque para entrar na fila ranqueada (modo preferido salvo)
- Badge de elo com cor da faixa (Bronze cobre, Prata prata, Ouro dourado...)
- Missões e temporada mostram progresso para incentivar ação
- Bottom nav com 5 tabs: Home, Jogar, Puzzle, Perfil, Loja

---

## Lobby / Seleção de Modo

### Layout

```
┌─────────────────────────────┐
│  ← Voltar        MODO DE JOGO│
│                              │
│  ┌─────────────────────────┐ │
│  │ ⚔ RANQUEADA            │ │  ← Modo principal
│  │ Elo: 1247 | Rapid 10+5 │ │
│  │ [JOGAR]                  │ │
│  └─────────────────────────┘ │
│                              │
│  ┌─────────────────────────┐ │
│  │ 🎯 CASUAL               │ │
│  │ Sem impacto no rating   │ │
│  │ [JOGAR]                  │ │
│  └─────────────────────────┘ │
│                              │
│  ┌────────┐ ┌──────────────┐ │
│  │ 🤖 IA  │ │ 👥 AMIGO    │ │  ← Cards menores
│  │ 3 dif. │ │ Por link    │ │
│  └────────┘ └──────────────┘ │
│                              │
│  CONTROLE DE TEMPO           │
│  ┌──┐ ┌──┐ ┌──┐ ┌──┐       │
│  │1'│ │3'│ │10│ │25│       │  ← Seletor de tempo
│  └──┘ └──┘ └──┘ └──┘       │
│  Bul  Bli  Rap  Std         │
└─────────────────────────────┘
```

---

## Tabuleiro (Tela de Partida)

### Layout (Mobile — vertical)

```
┌─────────────────────────────┐
│ PRATA  ⏱ 09:42   Elo:1305  │  ← Info adversário + relógio
│ [Do][Ho][  ][St]            │  ← Peças capturadas pelo Prata
│                              │
│ ┌──┬──┬──┬──┬──┬──┬──┬──┐   │
│ │  │  │  │  │  │  │  │  │ 8 │
│ ├──┼──┼──┼──┼──┼──┼──┼──┤   │  ← Tabuleiro 8×8
│ │  │  │  │  │  │  │  │  │ 7 │     (cores alternadas)
│ ├──┼──┼──┼──┼──┼──┼──┼──┤   │
│ │  │  │  │●│  │  │  │  │ 6 │     ● = peça selecionada
│ ├──┼──┼──┼──┼──┼──┼──┼──┤   │     ○ = movimento possível
│ │  │  │○│  │○│  │  │  │ 5 │     ◉ = captura possível
│ ├──┼──┼──┼──┼──┼──┼──┼──┤   │     ⚡ = peça Exausta
│ │  │  │  │  │  │  │  │  │ 4 │
│ ├──┼──┼──┼──┼──┼──┼──┼──┤   │
│ │  │  │  │  │  │  │  │  │ 3 │
│ ├──┼──┼──┼──┼──┼──┼──┼──┤   │
│ │  │  │  │  │  │  │  │  │ 2 │
│ ├──┼──┼──┼──┼──┼──┼──┼──┤   │
│ │  │  │  │  │  │  │  │  │ 1 │
│ └──┴──┴──┴──┴──┴──┴──┴──┘   │
│   a  b  c  d  e  f  g  h    │
│                              │
│ [Ho][To]                    │  ← Peças capturadas por Ouro
│ OURO   ⏱ 08:15   Elo:1247  │  ← Info própria + relógio
│                              │
│ ┌──────┐ ┌──────┐ ┌──────┐  │
│ │ PRESS│ │DESFAZ│ │ MENU │  │  ← Ações (Press, undo, menu)
│ └──────┘ └──────┘ └──────┘  │
│                              │
│ Histórico: 1. Dd4 Ste5 ...  │  ← Notação colapsável
└─────────────────────────────┘
```

### Feedback Visual de Jogadas

| Ação | Feedback Visual | Feedback Sonoro |
|---|---|---|
| **Selecionar peça** | Peça fica destacada (glow dourado). Casas de destino mostram círculos. | Click suave |
| **Movimento** | Peça desliza suavemente para destino (~200ms). Rastro sutil. | Slide suave |
| **Captura** | Peça capturada dissolve (fade + partículas). Peça capturadora ocupa casa. | Som de impacto satisfatório |
| **Press** | Botão PRESS brilha quando disponível. Após selecionar, borda fica âmbar. | Som de "power up" |
| **Exaustão** | Peça Exausta fica com opacity reduzida (70%) + ícone ⚡ sutil. | - |
| **Recuperação** | No início do turno, peças Exaustas brilham brevemente ao recuperar. | Som de "refresh" sutil |
| **Muralha de Escudos** | Linha brilhante azul conecta os 2 Hoplitas. Pulsa suavemente. | Hum suave quando formada |
| **Ataque à Distância** | Seta/projétil animado do Toxotes ao alvo. Alvo dissolve. | Som de flecha |
| **Investida** | Após captura, flash branco + trail de velocidade no movimento extra. | Som de galope + impacto |
| **Promoção** | Doríforo brilha → transformação animada para a peça escolhida. | Fanfarra breve |
| **Ameaça ao Arconte** | Quadrado do Arconte pulsa em vermelho sutil (se ameaçado). | - (sem aviso sonoro, por design) |
| **Vitória** | Tela escurece gradualmente + "KAIRÓS!" em letras douradas + animação de peças celebrando. | Acorde triunfal |
| **Derrota** | Arconte capturado com animação dramática. "Derrota" em letras sutis. | Acorde menor suave |

### Indicadores de Turno

- **De quem é o turno:** Borda do tabuleiro brilha na cor do jogador ativo (dourado/prateado). Nome e relógio do jogador ativo ficam em destaque.
- **Fase do turno:** Indicador textual discreto: "Mova uma peça" → "Press? (opcional)" → "Turno do adversário"
- **Relógio:** Contagem regressiva com cores: verde (>50%), amarelo (25-50%), vermelho pulsante (<25%)

### Destaque de Peças

- **Peça selecionada:** Borda brilhante dourada + elevação (shadow sutil)
- **Movimentos possíveis:** Círculos semi-opacos nas casas de destino (verdes para casa vazia, vermelhos para captura)
- **Peça sob ataque:** Sutil pulsação vermelha quando uma peça aliada está ameaçada
- **Última jogada:** Casas de origem e destino da última jogada levemente destacadas (persiste até próximo movimento)

---

## Tutorial Guiado

### Design do Tutorial

Cada lição é uma mini-partida pré-configurada com explicação contextual:

```
┌─────────────────────────────┐
│ LIÇÃO 1: O ARCONTE          │
│                              │
│ ┌─────────────────────────┐ │
│ │  Mini-tabuleiro 4×4      │ │  ← Tabuleiro reduzido para foco
│ │  (apenas peças relevant.)│ │
│ └─────────────────────────┘ │
│                              │
│ ┌─────────────────────────┐ │
│ │ "O Arconte é seu líder.  │ │  ← Caixa de texto com dica
│ │  Mova-o para capturar   │ │
│ │  o Arconte inimigo."    │ │
│ │                          │ │
│ │         [ENTENDI →]      │ │
│ └─────────────────────────┘ │
│                              │
│ ████████░░  Lição 1/5       │  ← Progresso
└─────────────────────────────┘
```

### Fluxo por Lição

1. **Texto explicativo** (2-3 frases)
2. **Demonstração animada** (o jogo move peças mostrando o conceito)
3. **"Sua vez"** — jogador executa a ação ensinada
4. **Feedback** — "Correto!" ou "Tente novamente" com dica
5. **Próximo conceito** ou **Lição completa**

---

## Tela de Vitória/Derrota

### Layout

```
┌─────────────────────────────┐
│                              │
│         ★ KAIRÓS! ★          │  ← (ou "Derrota" / "Empate")
│                              │
│     Captura do Arconte       │  ← Razão da vitória
│     em 28 turnos            │
│                              │
│  ┌──────────┬──────────┐    │
│  │  OURO    │  PRATA   │    │
│  │  ★ Você  │  Oponente│    │
│  │  Capt: 5 │  Capt: 3 │    │  ← Resumo da partida
│  │  Press: 4│  Press: 6│    │
│  │  Elo +15 │  Elo -15 │    │
│  └──────────┴──────────┘    │
│                              │
│  ┌─────────────────────────┐ │
│  │  ▶ REMATCH              │ │  ← CTA principal
│  └─────────────────────────┘ │
│  ┌────────┐ ┌──────────────┐ │
│  │ANÁLISE │ │  NOVA PARTIDA│ │
│  └────────┘ └──────────────┘ │
│  ┌─────────────────────────┐ │
│  │  🏠 VOLTAR AO MENU      │ │
│  └─────────────────────────┘ │
└─────────────────────────────┘
```

---

## Perfil do Jogador

### Layout

```
┌─────────────────────────────┐
│  ← Voltar        PERFIL     │
│                              │
│  ┌──────────────────────┐   │
│  │  [Avatar]            │   │
│  │  NomeDoJogador       │   │
│  │  🥇 Ouro II          │   │
│  │  Elo: 1247           │   │
│  │  Membro desde Mar/26 │   │
│  └──────────────────────┘   │
│                              │
│  ┌──────────────────────┐   │
│  │ W: 45  L: 38  D: 2   │   │  ← Record
│  │ Win rate: 52.9%       │   │
│  │ Melhor sequência: 7   │   │
│  └──────────────────────┘   │
│                              │
│  📈 ELO AO LONGO DO TEMPO   │
│  ┌──────────────────────┐   │
│  │    ╱╲    ╱╲ ╱╲       │   │  ← Gráfico sparkline
│  │╲╱╱  ╲╱╱    ╲  ╲      │   │
│  └──────────────────────┘   │
│                              │
│  ESTATÍSTICAS                │
│  ┌────────┬────────┐        │
│  │Press/  │Win rate│        │
│  │partida │c/ Press│        │
│  │ 3.2    │ 58%   │        │
│  └────────┴────────┘        │
│                              │
│  CONQUISTAS                  │
│  🏆 Primeiro Kairós          │
│  🏆 Investida Dupla          │
│  🔒 Muralha Inabalável       │
│  🔒 Tiro Certeiro            │
│                              │
│  HISTÓRICO DE PARTIDAS       │
│  ┌────────────────────────┐ │
│  │ vs Player2  W  28t  +15│ │
│  │ vs Player3  L  19t  -12│ │
│  │ vs Player4  W  35t  +14│ │
│  └────────────────────────┘ │
└─────────────────────────────┘
```

---

## Leaderboard

```
┌─────────────────────────────┐
│  ← Voltar      LEADERBOARD  │
│                              │
│  [Global] [Regional] [Amigos]│  ← Tabs
│                              │
│  ┌──────────────────────────┐│
│  │ #1  GrandMaster42  2687  ││
│  │ #2  KairosKing     2645  ││
│  │ #3  StrategyMind   2601  ││
│  │ ...                       ││
│  │ #127 ★ Você        1247  ││  ← Destaque do jogador
│  │ ...                       ││
│  └──────────────────────────┘│
│                              │
│  Sua posição: #127 de 12.4k  │
│  Top 1.0%                    │
└─────────────────────────────┘
```

---

## Recomendações de UX/UI Premium

### 1. Micro-interações
- Toda ação tem feedback tátil (vibração em mobile) e visual
- Transições entre telas: slide suave (250ms, ease-out)
- Hover em peças (desktop): mostra nome e alcance sutil

### 2. Dark Mode Nativo
- O jogo é dark-mode por padrão (tema grafite/dourado)
- Light mode disponível como opção (para ambientes claros)
- Cores do tabuleiro ajustam automaticamente para contraste

### 3. Acessibilidade
- Alt-text para peças (screen readers)
- Peças distinguíveis por silhueta, não apenas por cor
- Tamanho de toque mínimo: 44×44px (guidelines Apple/Google)
- Modo de alto contraste

### 4. Onboarding Progressivo
- Na primeira visita: tutorial é sugerido (não forçado)
- Features avançadas reveladas gradualmente (Press explicado após 3 partidas, análise após 10)
- Tooltips contextuais desaparecem após primeiro uso

### 5. Performance
- Animações em 60 FPS (Canvas otimizado)
- Tempo de carregamento inicial <3s em 4G
- Tamanho do bundle <500KB (lazy loading para features secundárias)
- Offline capable: pode jogar vs IA sem conexão (PWA + cache)
