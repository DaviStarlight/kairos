# 06 — Dashboards e Analytics

> Projetados para receber dados reais. Cada dashboard é especificado com objetivo, métricas, KPIs, gráficos, filtros e insights esperados.

---

## Dashboard 1: Partidas

### Objetivo
Monitorar volume, duração e qualidade das partidas em tempo real e ao longo do tempo.

### Métricas e KPIs

| Métrica | KPI/Meta | Tipo de Gráfico |
|---|---|---|
| Total de partidas/dia | >10k (pós-lançamento) | Linha temporal |
| Partidas ativas simultâneas | Pico em horário nobre | Área temporal |
| Duração média por modo | Bullet: 3min, Blitz: 8min, Rapid: 20min, Standard: 30min | Box plot por modo |
| Taxa de conclusão | >85% (vs. abandono) | Barra empilhada |
| Taxa de rematch | >30% | Gauge + Linha temporal |
| Resultado: vitória Ouro vs Prata | ~50/50 (±3%) | Pizza |
| Causa da vitória | Captura Arconte vs Abandono vs Tempo | Barra horizontal |
| Turnos por partida | Média: 25-40 | Histograma |

### Filtros
- Período (dia, semana, mês, temporada)
- Modo de jogo (Bullet, Blitz, Rapid, Standard, Casual, Ranqueada)
- Faixa de elo dos jogadores
- Plataforma (web, iOS, Android)
- Região geográfica

### Dimensões Analíticas
- Modo de jogo × Duração → Identificar modos com partidas fora do esperado
- Faixa de elo × Taxa de abandono → Identificar frustração por nível
- Hora do dia × Volume → Otimizar manutenção e eventos

### Insights Esperados
- Horários de pico para programar eventos e torneios
- Modos mais populares vs. menos populares (informar priorização de features)
- Se o jogo está equilibrado entre primeiro/segundo jogador
- Se partidas estão longas demais (possível ajuste de regra)

---

## Dashboard 2: Performance do Jogador

### Objetivo
Oferecer ao jogador (e ao time de produto) visão profunda sobre métricas de performance individual.

### Métricas (visão jogador)

| Métrica | Gráfico |
|---|---|
| Elo ao longo do tempo | Linha temporal |
| Win rate geral | Número grande + sparkline |
| Win rate por cor (Ouro/Prata) | Barra comparativa |
| Win rate por modo | Barra horizontal |
| Peça mais capturada por adversário | Ranking |
| Peça mais usada para capturar | Ranking |
| Taxa de uso de Press | % + Linha temporal |
| Taxa de vitória com Press vs sem Press | Barra comparativa |
| Abertura mais usada | Lista + Win rate |
| Duração média das partidas | Número + trend |
| Maior sequência de vitórias | Número |
| Ameaças não percebidas ao Arconte | Número (via engine) |

### Métricas (visão time de produto)

| Métrica | KPI |
|---|---|
| Distribuição de elo | Curva normal (verificar se rating está calibrado) |
| Win rate por faixa de elo × modo | Verificar se matchmaking está funcionando |
| Evolução de elo de cohort | Retenção correlacionada ao progresso |
| Jogadores stuck (elo estagnado há 2+ semanas) | <20% da base ativa |

### Filtros
- Jogador específico (ID/username)
- Período
- Modo de jogo
- Adversário (opcional)

### Insights Esperados
- Quais peças/mecânicas o jogador domina e quais precisa melhorar
- Se o matchmaking está gerando partidas equilibradas
- Se jogadores progridem ou ficam estagnados (churn risk)

---

## Dashboard 3: Competitivo

### Objetivo
Monitorar saúde do ecossistema competitivo: ranqueadas, torneios, elo, integridade.

### Métricas e KPIs

| Métrica | KPI | Gráfico |
|---|---|---|
| Jogadores em ranqueada/dia | Growing MoM | Linha temporal |
| Distribuição de elo | Curva normal centrada em ~1200 | Histograma |
| Tempo de fila (matchmaking) | <30s (mediana) | Histograma + P50/P95 |
| Win rate top 100 | Nenhum jogador >70% (anti-smurf) | Scatter plot |
| Torneios realizados/semana | >5 | Barra |
| Participantes por torneio | >32 (média) | Box plot |
| Detecções anti-cheat | Próximo de zero (mas monitorado) | Contador |
| Empates em ranqueada | <10% | Gauge |

### Filtros
- Período, Faixa de elo, Região, Modo de tempo

### Insights Esperados
- Se o matchmaking está calibrado (tempo de fila vs qualidade de match)
- Se há smurfs (contas novas com win rate anormal)
- Se torneios estão com boa aderência
- Se o elo está inflacionando ou deflacionando ao longo do tempo

---

## Dashboard 4: Retenção e Engajamento

### Objetivo
Medir e otimizar retenção, engajamento e ciclo de vida do jogador.

### Métricas e KPIs

| Métrica | KPI | Gráfico |
|---|---|---|
| DAU (Daily Active Users) | Growing | Linha temporal |
| MAU (Monthly Active Users) | Growing | Linha temporal |
| DAU/MAU (stickiness) | >20% | Gauge + trend |
| Retenção D1 | >40% | Cohort heatmap |
| Retenção D7 | >20% | Cohort heatmap |
| Retenção D30 | >10% | Cohort heatmap |
| Sessões por dia por usuário | >1.5 | Histograma |
| Duração média da sessão | >12 min | Histograma |
| Partidas por sessão | >2 | Histograma |
| Taxa de churn (30 dias) | <70% | Linha temporal |
| Ressurreição (return after churn) | >5% | Linha temporal |

### Funil de Conversão

```
Download/Acesso → Tutorial Completo → 1ª Partida → 2ª Partida → 5ª Partida → Ranqueada → Recorrente
   100%              85%              75%          55%          35%         20%          12%
```

| Etapa | Conversão Alvo | Gráfico |
|---|---|---|
| Acesso → Tutorial | >85% | Funil |
| Tutorial → 1ª Partida | >75% | Funil |
| 1ª Partida → 2ª Partida | >55% | Funil |
| 2ª → 5ª Partida | >35% | Funil |
| 5ª Partida → Ranqueada | >20% | Funil |
| Ranqueada → Recorrente (D30 ativo) | >12% | Funil |

### Filtros
- Cohort de aquisição (semana/mês de cadastro)
- Canal de aquisição (orgânico, paid, referral)
- Plataforma
- Região

### Insights Esperados
- Onde jogadores estão abandonando no funil (priorizar melhorias)
- Qual cohort retém melhor (identificar campanhas/features eficazes)
- Correlação entre engagement features e retenção (puzzles diários → D7?)

---

## Dashboard 5: Balanceamento do Jogo

### Objetivo
Garantir que o jogo é justo, equilibrado e que nenhuma mecânica é dominante ou irrelevante.

### Métricas e KPIs

| Métrica | Alvo | Gráfico |
|---|---|---|
| Win rate Ouro vs Prata (por elo) | 50% ± 2% em todas as faixas | Linha por faixa de elo |
| Win rate por peça de captura final | Distribuído (sem peça >40%) | Barra |
| Taxa de uso de Press por turno | 30-50% dos turnos | Histograma |
| Win rate com Press vs sem Press | Sem diferença >5% | Barra comparativa |
| Taxa de uso de Muralha | >20% das partidas | Gauge |
| Taxa de sobrevivência por tipo de peça | Equilibrado | Heatmap |
| Peças promovidas vs tipo escolhido | Distribuído | Pizza |
| Promoção escolhida vs win rate | Sem opção >60% win rate | Barra |
| Aberturas mais usadas (top 10) | Sem abertura >20% | Tabela + win rate |
| Duração do jogo por faixa de elo | Crescente (mais elo = mais longo) | Box plot |
| Investida dupla: frequência e win rate | <5% dos jogos, ~70% win rate | Scatter |
| Ataque à Distância ao Arconte: frequência | <3% dos jogos | Counter |

### Filtros
- Faixa de elo (separar balanceamento por nível)
- Modo de tempo
- Período
- Patch/versão (se houver ajustes de balance)

### Dimensões Analíticas
- Elo × Win rate por estratégia → Verificar se estratégias são "quebradas" em algum elo
- Peça × Taxa de captura → Verificar se alguma peça é muito forte/fraca
- Abertura × Win rate por elo → Verificar se alguma abertura é dominante

### Insights Esperados
- Se alguma peça ou mecânica precisa de ajuste (nerfs/buffs)
- Se o primeiro jogador (Ouro) tem vantagem significativa (e se precisa de correção)
- Se promoções estão equilibradas ou se todo mundo escolhe o mesmo tipo
- Se Press está sendo usado na frequência esperada (muito pouco = mecânica irrelevante, muito = mecânica obrigatória)

---

## Dashboard 6: Monetização Futura

### Objetivo
Rastrear receita, conversão e LTV quando monetização for implementada.

### Métricas e KPIs

| Métrica | KPI | Gráfico |
|---|---|---|
| Receita total/dia | Growing | Linha temporal |
| ARPU (Average Revenue Per User) | >$0.50/mês | Linha temporal |
| ARPPU (Average Revenue Per Paying User) | >$5/mês | Linha temporal |
| Taxa de conversão F2P → payer | >3% | Gauge |
| LTV (Lifetime Value) | >$10 | Linha + cohort |
| Items mais comprados | Top 10 | Ranking |
| Receita por categoria | Pizza: cosméticos, passe, premium | Pizza |
| Passe de temporada: taxa de compra | >8% da base ativa | Gauge |
| Passe de temporada: taxa de conclusão | >60% dos compradores | Barra |

### Filtros
- Período, Plataforma, País, Faixa de elo

### Insights Esperados
- Quais cosméticos vendem mais (informar criação futura)
- Se o passe está precificado corretamente
- Se payers retém mais que F2P (validar modelo)
- LTV por canal de aquisição (informar investimento em marketing)

---

## Dashboard 7: Comportamento e Funil

### Objetivo
Entender o comportamento granular do jogador e otimizar cada passo da jornada.

### Métricas e KPIs

| Métrica | Gráfico |
|---|---|
| Tutorial: taxa de erro por lição | Barra por lição |
| Tutorial: tempo médio por lição | Barra |
| Tutorial: drop-off por lição | Funil |
| Primeira partida: resultado | Pizza (vitória/derrota/abandono) |
| Primeira partida: duração | Histograma |
| Feature discovery: % que usa cada mecânica na 1ª semana | Barra (Press, Muralha, Ranged, Investida) |
| Sessão: fluxo de telas (sankey) | Sankey diagram |
| Partida: heatmap de posição do Arconte | Heatmap no tabuleiro |
| Partida: casas mais disputadas | Heatmap no tabuleiro |
| Partida: turnos até primeira captura | Histograma |
| Partida: Press por turno (média) | Linha temporal por turno# |
| Abandono: turno em que jogadores abandonam | Histograma |
| Rematch: taxa após vitória vs derrota | Barra comparativa |
| Social: % que adiciona amigo na 1ª semana | Gauge |

### Filtros
- Cohort, Plataforma, Elo, Modo, Período

### Insights Esperados
- Onde o tutorial confunde (otimizar lições)
- Quais mecânicas jogadores descobrem naturalmente vs. precisam ser ensinadas
- Heatmaps de tabuleiro informam balance (centro > bordas confirma bom design)
- Em qual turno abandonos ocorrem (posições frustrantes vs. partidas longas demais)
- Se rematches são mais comuns após derrotas (engajamento de aprendizado) ou vitórias (diversão)

---

## Resumo: Como Dados Alimentam Decisões

| Decisão | Dashboard(s) | Dado-chave |
|---|---|---|
| Ajustar regras/balance | Balanceamento | Win rate por peça/estratégia |
| Melhorar onboarding | Comportamento + Retenção | Drop-off no tutorial, D1 retention |
| Priorizar features | Retenção + Engajamento | Correlação feature uso × retenção |
| Precificar monetização | Monetização | ARPU, conversão, LTV |
| Calibrar matchmaking | Competitivo | Tempo de fila, win rate por match quality |
| Programar torneios | Partidas + Competitivo | Horários de pico, participação |
| Criar conteúdo (puzzles, lições) | Comportamento | Feature discovery, peças menos usadas |
| Corrigir bugs de gameplay | Partidas + Balanceamento | Anomalias em duração, win rate súbita |
