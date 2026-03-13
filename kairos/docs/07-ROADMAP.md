# 07 — Roadmap Completo de Evolução

---

## Fase 1: Fundação e Regras-Base

### Objetivo
Estabelecer as regras definitivas do jogo através de playtesting analógico e simulação.

### Entregáveis
- [x] Documento de regras completo (v1.0)
- [ ] Kit de playtesting físico (tabuleiro impresso + peças de papel/madeira)
- [ ] 50+ partidas de playtesting documentadas
- [ ] Relatório de balance (win rate Ouro vs Prata, peças mais/menos capturadas)
- [ ] Ajustes de regras baseados em playtesting
- [ ] Regras finais (v1.1) pós-playtesting

### Prioridades
1. Validar que o Press não quebra o jogo (nem underpowered nem overpowered)
2. Validar que Muralha de Escudos não gera stalemates
3. Validar que Ataque à Distância não é dominante
4. Confirmar que partidas duram 15-30 minutos

### Riscos
| Risco | Probabilidade | Impacto | Mitigação |
|---|---|---|---|
| Press muito forte (quem pressa sempre ganha) | Média | Alto | Ajustar custo de Exaustão (ex: 2 turnos em vez de 1) |
| Muralha gera empates infinitos | Baixa | Alto | Limitar duração da Muralha ou adicionar peça que a quebre |
| Primeiro jogador (Ouro) vantagem >55% | Média | Médio | Ajustar setup ou dar vantagem compensatória a Prata |
| Partidas muito longas (>45 min) | Média | Médio | Reduzir peças ou aumentar mobilidade |

### Critérios de Sucesso
- Win rate Ouro vs Prata entre 48-52%
- Duração média de partidas entre 15-35 minutos
- >80% dos playtesters querem jogar novamente
- Press é usado em 30-60% dos turnos

### O que pode ser adiado
- Nomenclatura final (nomes das peças podem mudar)
- Arte e design visual
- Qualquer feature digital

---

## Fase 2: Protótipo Jogável Digital

### Objetivo
Criar a primeira versão digital jogável, validar UX e mecânicas em formato interativo.

### Entregáveis
- [ ] Engine de regras (game logic) em TypeScript
- [ ] Tabuleiro renderizado em Canvas/WebGL
- [ ] Interação básica: clicar peça → ver movimentos → clicar destino → executar
- [ ] Indicadores visuais de Exaustão, Muralha, Press
- [ ] IA básica (minimax α-β profundidade 3-4)
- [ ] Modo "Hot Seat" (2 jogadores, 1 dispositivo)
- [ ] Detecção automática de vitória/derrota/empate
- [ ] Registro de movimentos (algebraic notation)

### Prioridades
1. Engine de regras 100% correto (todas as regras testadas)
2. UX fluida para selecionar e mover peças
3. Feedback visual claro de estado (de quem é o turno, peças Exaustas, etc.)

### Riscos
| Risco | Probabilidade | Impacto | Mitigação |
|---|---|---|---|
| Bugs na engine de regras | Alta | Alto | Testes unitários extensivos (>200 test cases) |
| IA muito lenta | Média | Médio | Limitar profundidade, otimizar avaliação |
| UX confusa (peças difíceis de distinguir) | Média | Médio | Testes de usabilidade com 5 usuários |

### Critérios de Sucesso
- 0 bugs nas regras após 100 partidas de teste
- IA fácil perde para humano médio em ~70% das vezes
- Tempo de resposta da IA < 2 segundos
- 5/5 testers entendem a interface sem explicação

### Dependências
- Fase 1 completa (regras finalizadas)

---

## Fase 3: Interface Digital Completa

### Objetivo
Produto polido com identidade visual, tutorial, e experiência completa para jogador solo.

### Entregáveis
- [ ] Identidade visual completa (cores, tipografia, iconografia de peças)
- [ ] Tabuleiro com tema greco-antigo estilizado
- [ ] Animações: movimento de peças, captura, Press, Investida, Promoção
- [ ] Efeitos sonoros: movimento, captura, Press, vitória, derrota
- [ ] Tutorial interativo (5 lições)
- [ ] 3 níveis de IA (Fácil, Médio, Difícil)
- [ ] Tela inicial com menu
- [ ] Tela de vitória/derrota com resumo
- [ ] Histórico de movimentos na lateral
- [ ] Configurações (som, tema claro/escuro)
- [ ] Responsivo: mobile (vertical) + desktop (horizontal)
- [ ] PWA instalável

### Prioridades
1. Tutorial que converte novos jogadores
2. IA difícil que desafia intermediários
3. Identidade visual memorável
4. Performance suave (60 FPS em mobile)

### Riscos
| Risco | Probabilidade | Impacto | Mitigação |
|---|---|---|---|
| Tutorial confuso → drop-off | Média | Alto | Iterar com testes de usabilidade |
| IA difícil muito fácil ou muito difícil | Alta | Médio | Calibrar com 20+ testers de diferentes níveis |
| Performance ruim em mobile antigo | Média | Médio | Canvas 2D fallback + otimização de sprites |

### Critérios de Sucesso
- >85% completam o tutorial
- >75% jogam primeira partida após tutorial
- NPS > 40 entre testers
- <3s tempo de carregamento inicial em 4G

### Dependências
- Fase 2 completa (engine funcional)

---

## Fase 4: Multiplayer Local/Online

### Objetivo
Permitir que dois jogadores joguem juntos, localmente e pela internet.

### Entregáveis
- [ ] Backend Node.js/Express com WebSocket (Socket.io)
- [ ] Sistema de salas (criar/entrar com código)
- [ ] Partida online funcional (sem matchmaking)
- [ ] Sistema de autenticação (email + Google OAuth)
- [ ] Perfil básico do jogador (nome, avatar)
- [ ] Relógio de partida (4 configurações de tempo)
- [ ] Reconexão automática se conexão cair
- [ ] Chat in-game (mensagens pré-definidas)
- [ ] Convite por link

### Prioridades
1. Latência <100ms para movimentos
2. Reconexão robusta (não perder partida por lag)
3. Autenticação segura
4. Relógio sincronizado entre servidor e clientes

### Riscos
| Risco | Probabilidade | Impacto | Mitigação |
|---|---|---|---|
| Dessincronização de estado | Alta | Crítico | Server-authoritative: server é fonte de verdade |
| Exploits/cheating (enviar movimentos ilegais) | Média | Alto | Server valida TODAS as jogadas |
| Latência alta em regiões distantes | Média | Médio | CDN + server multi-região futuro |

### Critérios de Sucesso
- 0 dessincronizações em 1000 partidas de teste
- Latência P95 <200ms
- Reconexão em <5s após disconnect

### Dependências
- Fase 3 completa (interface polida)

---

## Fase 5: Sistema Competitivo

### Objetivo
Estabelecer ecossistema ranqueado com elo, leaderboard e temporadas.

### Entregáveis
- [ ] Sistema de Elo (Glicko-2)
- [ ] Matchmaking por elo (fila ranqueada)
- [ ] Partidas ranqueadas vs. casuais
- [ ] Leaderboard global (top 100)
- [ ] Leaderboard por região
- [ ] Temporadas (reset parcial de elo a cada 3 meses)
- [ ] Recompensas de temporada (ícones, bordas)
- [ ] Faixas de ranking (Bronze → Kairós)
- [ ] Histórico de partidas completo
- [ ] Perfil público do jogador

### Prioridades
1. Matchmaking que gera partidas equilibradas (<200 elo de diferença)
2. Anti-smurf (detecção de contas novas com performance alta)
3. Temporadas com sensação de progresso e reset

### Riscos
| Risco | Probabilidade | Impacto | Mitigação |
|---|---|---|---|
| Player pool pequeno → fila longa | Alta (início) | Alto | Matchmaking adaptativo: expande busca ao longo do tempo |
| Smurfs | Média | Médio | Placement matches agressivos, detecção por winrate |
| Elo inflation/deflation | Baixa | Médio | Glicko-2 auto-corrige; monitorar distribuição |

### Critérios de Sucesso
- Tempo de fila mediano <30s com >1000 jogadores online
- Win rate 48-52% em matches ranqueados
- >50% da base ativa joga pelo menos 1 ranqueada/semana
- Distribuição de elo em curva normal

### Dependências
- Fase 4 completa (multiplayer funcional)

---

## Fase 6: Analytics e Dashboards Reais

### Objetivo
Implementar a camada de dados para informar decisões de produto e game design.

### Entregáveis
- [ ] Pipeline de eventos (client → API → data warehouse)
- [ ] Event tracking para todos os eventos analíticos definidos
- [ ] Dashboard de Partidas (Metabase/Grafana)
- [ ] Dashboard de Performance do Jogador
- [ ] Dashboard de Retenção e Engajamento
- [ ] Dashboard de Balanceamento
- [ ] Dashboard Competitivo
- [ ] Alertas automáticos para anomalias

### Prioridades
1. Event pipeline confiável (0 eventos perdidos)
2. Dashboards de Retenção e Balanceamento (informam decisões críticas)
3. Alertas de anomalia (win rate, crash rate)

### Riscos
| Risco | Probabilidade | Impacto | Mitigação |
|---|---|---|---|
| Eventos perdidos | Média | Alto | Queue resiliente (Redis/Kafka), retry com backoff |
| Dashboard lento com dados grandes | Média | Médio | Materializar views, agregações incrementais |
| Privacy compliance (GDPR/LGPD) | Baixa | Alto | Anonimizar dados analíticos, consent management |

### Critérios de Sucesso
- >99.9% de eventos capturados
- Dashboards carregam em <5s
- Time de produto usa dashboards diariamente

### Dependências
- Fase 5 parcial (dados de ranking e matches)

---

## Fase 7: Expansão de Features

### Objetivo
Enriquecer a experiência com features secundárias que aumentam retenção e monetização.

### Entregáveis
- [ ] Puzzles/Desafios diários
- [ ] Missões semanais com recompensas
- [ ] Replay de partidas
- [ ] Análise automática de partida (engine sugere melhores jogadas)
- [ ] Torneios automatizados (Swiss/Elimination)
- [ ] Sistema de amigos
- [ ] Clubes/equipes
- [ ] Modo espectador
- [ ] Cosméticos: temas de tabuleiro, skins de peças
- [ ] Passe de temporada

### Prioridades
1. Puzzles e missões (retenção imediata)
2. Torneios (retenção competitiva)
3. Cosméticos e passe (monetização)
4. Social (amigos, clubes) (retenção social)

### O que pode ser adiado
- Análise automática de partida (requer engine forte)
- Clubes (feature social complexa)
- Modo espectador ao vivo

### Critérios de Sucesso
- Puzzles: >30% da DAU resolve puzzle diário
- Torneios: >50 jogadores por torneio semanal
- Passe: >5% de conversão

---

## Fase 8: Ecossistema e Escala

### Objetivo
Transformar Kairós de um jogo em uma plataforma/ecossistema escalável.

### Entregáveis
- [ ] API pública para desenvolvedores (bots, análise, integração)
- [ ] SDK de torneios (organizadores externos)
- [ ] IA avançada (rede neural, engine competitiva)
- [ ] App nativo iOS e Android (ou manter PWA se performance OK)
- [ ] Infraestrutura multi-região (América, Europa, Ásia)
- [ ] Localização (10+ idiomas)
- [ ] Programa de parceiros/streamers
- [ ] Versão física premium (tabuleiro + peças produzidos)
- [ ] Conteúdo educacional (cursos de estratégia)
- [ ] Variantes oficiais do jogo (tabuleiro hexagonal, 4 jogadores)
- [ ] Parcerias com plataformas de esports

### Prioridades
1. Escala de infraestrutura (suportar 1M+ MAU)
2. IA competitiva (benchmark vs jogadores humanos)
3. Expansão internacional

### Critérios de Sucesso
- 1M MAU
- Receita sustentável
- Comunidade auto-organizada de torneios
- Menção em mídia esportiva/gaming relevante

---

## Timeline Visual

```
     M1  M2  M3  M4  M5  M6  M7  M8  M9  M10 M11 M12  M13-M18  M19-M24
     ────────────────────────────────────────  ────────  ─────────
F1   ████                                       
F2       ████████                              
F3               ████████                      
F4                       ████████              
F5                               ████████      
F6                           ████████████      
F7                                       ████████████
F8                                                       ████████████████

F = Fase, M = Mês (a partir do início do desenvolvimento)
```

### Marcos Chave
| Marco | Mês | Entregável |
|---|---|---|
| **Alpha** | M3 | Protótipo jogável (solo + IA) |
| **Beta Fechado** | M6 | Interface completa + IA 3 níveis |
| **Beta Aberto** | M8 | Multiplayer online funcionando |
| **Lançamento v1.0** | M10 | Ranqueadas + leaderboard |
| **Temporada 1** | M11 | Sistema competitivo + passe |
| **v2.0** | M15 | Torneios + analytics + cosméticos |
| **v3.0** | M21 | Ecossistema completo + escala global |
