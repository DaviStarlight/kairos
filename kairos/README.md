# KAIRÓS — O Jogo do Momento Decisivo

> *"Em estratégia, não vence quem move mais — vence quem move no momento certo."*

---

## Visão Geral

**KAIRÓS** é um jogo de tabuleiro estratégico original para 2 jogadores, jogado em um tabuleiro 8×8. Inspirado pela palavra grega *καιρός* (o momento oportuno, o instante decisivo), o jogo combina profundidade posicional com uma mecânica de tempo inédita — o **Sistema Press** — que transforma cada turno em uma decisão entre poder imediato e flexibilidade futura.

Com 6 tipos de peças, cada uma com habilidades únicas (incluindo **Ataque à Distância**, **Muralha de Escudos** e **Investida**), Kairós oferece a profundidade estratégica do xadrez com identidade própria, regras mais acessíveis e partidas mais dinâmicas.

---

## Highlights do Projeto

| Aspecto | Descrição |
|---|---|
| **Gênero** | Jogo de estratégia abstrato com camada tática |
| **Jogadores** | 2 |
| **Tabuleiro** | 8×8 (64 casas) |
| **Peças por jogador** | 12 (6 tipos distintos) |
| **Tempo médio de partida** | 15–30 minutos |
| **Mecânica central** | Sistema Press (tempo tático) |
| **Condição de vitória** | Captura do Arconte adversário |
| **Aleatoriedade** | Zero — informação completa, determinístico |
| **Público-alvo** | Jogadores casuais-a-competitivos, 12+ anos |

---

## Mecânicas Exclusivas

### 1. Sistema Press (Tempo Tático)
Cada turno, você move UMA peça. Opcionalmente, pode **"Pressionar"** — mover uma SEGUNDA peça, mas ela fica **Exausta** e não pode agir no próximo turno. Isso cria uma tensão única entre agressividade imediata e mobilidade futura.

### 2. Ataque à Distância (Toxotai)
Os Arqueiros podem capturar peças inimigas a exatamente 2 casas de distância SEM se mover. Projeção de ameaça sem exposição.

### 3. Muralha de Escudos (Hoplitas)
Dois Hoplitas aliados adjacentes ortogonalmente formam uma Muralha de Escudos — ficam imunes à captura enquanto permanecerem conectados.

### 4. Investida (Hippeis)
A Cavalaria, ao capturar, pode se mover 1 casa adicional (podendo capturar outra peça). Golpes táticos duplos devastadores.

### 5. Vitória por Captura Direta
Não existe "xeque" ou aviso. Se o Arconte está vulnerável e o adversário o captura, o jogo acaba. Vigilância constante é obrigatória.

---

## Estrutura da Documentação

| # | Documento | Conteúdo |
|---|---|---|
| 01 | [Conceito do Jogo](docs/01-CONCEITO.md) | Proposta, fantasia, diferencial, público-alvo |
| 02 | [Regras Completas](docs/02-REGRAS.md) | Manual oficial com todas as regras |
| 03 | [Estratégia e Profundidade](docs/03-ESTRATEGIA.md) | Estilos de jogo, táticas, leitura de adversário |
| 04 | [Como Vencer](docs/04-COMO-VENCER.md) | Fundamentos, mentalidade, raciocínio |
| 05 | [Produto Digital](docs/05-PRODUTO-DIGITAL.md) | MVP, retenção, loops, progressão |
| 06 | [Dashboards e Analytics](docs/06-DASHBOARDS.md) | KPIs, métricas, gráficos, insights |
| 07 | [Roadmap](docs/07-ROADMAP.md) | Fases de evolução do produto |
| 08 | [Expansões e Features](docs/08-EXPANSOES.md) | Leaderboard, torneios, IA, temporadas |
| 09 | [Arquitetura Técnica](docs/09-ARQUITETURA.md) | Stack, infra, multiplayer, CI/CD |
| 10 | [Banco de Dados e Eventos](docs/10-BANCO-EVENTOS.md) | Modelagem, eventos analíticos |
| 11 | [UX/UI](docs/11-UX-UI.md) | Telas, interação, feedback, identidade visual |
| 12 | [Monetização](docs/12-MONETIZACAO.md) | Cosméticos, passe, premium, integridade |
| 13 | [Diferenciais Revolucionários](docs/13-DIFERENCIAIS.md) | Por que Kairós pode ser referência |
| 14 | [Entrega Executiva](docs/14-ENTREGA-FINAL.md) | Resumo, pitch, backlog, MVP, próximos passos |

---

## Posição Inicial

```
     a    b    c    d    e    f    g    h
  ┌────┬────┬────┬────┬────┬────┬────┬────┐
8 │ Hi │ To │ Ho │ St │ Ar │ Ho │ To │ Hi │  ← PRATA
  ├────┼────┼────┼────┼────┼────┼────┼────┤
7 │    │    │ Do │ Do │ Do │ Do │    │    │
  ├────┼────┼────┼────┼────┼────┼────┼────┤
6 │    │    │    │    │    │    │    │    │
  ├────┼────┼────┼────┼────┼────┼────┼────┤
5 │    │    │    │    │    │    │    │    │
  ├────┼────┼────┼────┼────┼────┼────┼────┤
4 │    │    │    │    │    │    │    │    │
  ├────┼────┼────┼────┼────┼────┼────┼────┤
3 │    │    │    │    │    │    │    │    │
  ├────┼────┼────┼────┼────┼────┼────┼────┤
2 │    │    │ Do │ Do │ Do │ Do │    │    │
  ├────┼────┼────┼────┼────┼────┼────┼────┤
1 │ Hi │ To │ Ho │ Ar │ St │ Ho │ To │ Hi │  ← OURO
  └────┴────┴────┴────┴────┴────┴────┴────┘
     a    b    c    d    e    f    g    h

Legenda: Ar=Arconte, St=Strategos, Ho=Hoplita, To=Toxotes, Hi=Hippeus, Do=Doríforo
```

---

## Status do Projeto

- [x] Game Design completo
- [x] Regras finalizadas
- [x] Documentação de produto
- [x] Arquitetura técnica
- [ ] Protótipo jogável (próximo passo)
- [ ] Interface digital
- [ ] Multiplayer online

---

## Licença

Propriedade intelectual original. Todos os direitos reservados.

© 2026 Kairós Game Project
