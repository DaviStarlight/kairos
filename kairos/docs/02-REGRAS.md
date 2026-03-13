# 02 — Regras Completas de KAIRÓS

> Manual Oficial — Versão 1.0

---

## Sumário

1. [Componentes](#1-componentes)
2. [Preparação](#2-preparação)
3. [Objetivo](#3-objetivo)
4. [Estrutura do Turno](#4-estrutura-do-turno)
5. [Sistema Press](#5-sistema-press)
6. [Peças e Movimentação](#6-peças-e-movimentação)
7. [Capturas](#7-capturas)
8. [Habilidades Especiais](#8-habilidades-especiais)
9. [Promoção](#9-promoção)
10. [Condições de Vitória](#10-condições-de-vitória)
11. [Condições de Empate](#11-condições-de-empate)
12. [Regras Especiais e Esclarecimentos](#12-regras-especiais-e-esclarecimentos)
13. [Exemplos Práticos](#13-exemplos-práticos)
14. [Referência Rápida](#14-referência-rápida)
15. [Curva de Aprendizado](#15-curva-de-aprendizado)

---

## 1. Componentes

### Tabuleiro
- Grade 8×8 com **64 casas** alternando cores claras e escuras
- Colunas identificadas de **a** a **h** (esquerda para direita)
- Linhas identificadas de **1** a **8** (Ouro embaixo, Prata em cima)
- Notação algébrica: cada casa é identificada por coluna+linha (ex: `d4`, `f7`)

### Peças
Cada jogador possui **12 peças** de 6 tipos:

| Tipo | Abreviação | Quantidade | Símbolo Sugerido |
|---|---|---|---|
| Arconte | **Ar** | 1 | ★ Coroa / Capacete com crista |
| Strategos | **St** | 1 | ✦ Espada cruzada |
| Hoplita | **Ho** | 2 | ◈ Escudo redondo |
| Toxotes | **To** | 2 | ◇ Arco |
| Hippeus | **Hi** | 2 | ◆ Cavalo |
| Doríforo | **Do** | 4 | ● Lança |

### Marcadores de Exaustão
- **Tokens de Exaustão** (fichas ou anéis coloridos) para indicar peças Exaustas após um Press
- Na versão digital, indicado visualmente (brilho reduzido, ícone de fadiga)

### Cores/Facções
- **Ouro** (primeiro jogador): joga a partir das linhas 1–2
- **Prata** (segundo jogador): joga a partir das linhas 7–8

---

## 2. Preparação

### Posição Inicial

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
```

**Detalhamento por casa (Ouro):**
- a1: Hippeus | b1: Toxotes | c1: Hoplita | d1: Arconte | e1: Strategos
- f1: Hoplita | g1: Toxotes | h1: Hippeus
- c2: Doríforo | d2: Doríforo | e2: Doríforo | f2: Doríforo

**Detalhamento por casa (Prata) — espelhamento horizontal:**
- a8: Hippeus | b8: Toxotes | c8: Hoplita | d8: Strategos | e8: Arconte
- f8: Hoplita | g8: Toxotes | h8: Hippeus
- c7: Doríforo | d7: Doríforo | e7: Doríforo | f7: Doríforo

### Determinação do Primeiro Jogador
- Em partidas casuais: sorteio (moeda, par-ímpar)
- Em partidas competitivas: alternância entre jogos de uma série
- Ouro **sempre** faz o primeiro movimento

---

## 3. Objetivo

**Capturar o Arconte adversário.**

Não existe "xeque" ou aviso. Se uma peça sua, em seu turno, pode se mover para a casa do Arconte inimigo, ela captura o Arconte e **você vence imediatamente**.

---

## 4. Estrutura do Turno

Cada turno é composto de **3 fases** executadas na ordem:

### Fase 1 — Recuperação
Todas as suas peças atualmente marcadas como **Exaustas** são recuperadas. Remova os marcadores de Exaustão.

> **Nota:** A recuperação acontece no INÍCIO do seu turno, portanto uma peça Exausta fica indisponível por exatamente **1 turno completo do oponente**.

### Fase 2 — Movimento Principal
Você **deve** mover exatamente **uma peça** de acordo com suas regras de movimentação.

Regras do Movimento Principal:
- Você pode mover qualquer peça que **não esteja Exausta**
- A peça deve realizar um movimento legal (ver seção 6)
- Você não pode pular o turno — deve mover uma peça

### Fase 3 — Press (Opcional)
Após o Movimento Principal, você **pode** optar por **Pressionar**: mover uma **segunda peça diferente** de acordo com suas regras de movimentação.

Regras do Press:
- A peça Pressada **não pode ser o Arconte**
- A peça Pressada **não pode estar Exausta**
- A peça Pressada **não pode ser a mesma** peça movida na Fase 2
- Após a execução do Press, a peça Pressada recebe um **marcador de Exaustão**
- Peças Exaustas **não podem mover nem usar habilidades** até serem recuperadas

### Diagrama do Turno

```
INÍCIO DO TURNO
     │
     ▼
[FASE 1: RECUPERAÇÃO]
  └─ Todas as peças Exaustas → Prontas
     │
     ▼
[FASE 2: MOVIMENTO PRINCIPAL]
  └─ Mover 1 peça (obrigatório)
     │
     ▼
[FASE 3: PRESS] (opcional)
  └─ Mover 1 peça adicional (≠ Arconte, ≠ Exausta, ≠ peça da Fase 2)
  └─ Peça Pressada → marcada como Exausta
     │
     ▼
FIM DO TURNO → Turno do oponente
```

---

## 5. Sistema Press

O Press é o coração mecânico de Kairós. Entender quando e como usá-lo separa iniciantes de especialistas.

### Regras Detalhadas

| Regra | Descrição |
|---|---|
| Quem pode ser Pressado | Qualquer peça que não seja o Arconte e não esteja Exausta |
| Custo | A peça Pressada fica Exausta (indisponível no próximo turno) |
| Duração da Exaustão | A peça recupera na Fase 1 do seu **próximo** turno |
| Press com captura | A peça Pressada PODE capturar durante o Press |
| Press com habilidade | A peça Pressada PODE usar sua habilidade especial (Ataque à Distância, etc.) |
| Press do Arconte | **PROIBIDO** — o Arconte não pode ser Pressado |
| Peça movida na Fase 2 | **NÃO PODE** ser Pressada na Fase 3 do mesmo turno |
| Press obrigatório? | **NÃO** — o Press é sempre opcional |
| Quantas vezes por turno | No máximo **1 Press** por turno |

### Exemplo de Press

> Ouro move o Strategos de e1 para e4 (Movimento Principal). Em seguida, Ouro Pressa o Toxotes de b1 para d3 (Press). O Toxotes em d3 recebe um marcador de Exaustão. No próximo turno de Ouro, durante a Fase 1, o Toxotes se recupera.

### Considerações Estratégicas do Press

- ✅ **Use Press para:** criar ameaças duplas, finalizar, posicionar duas peças em coordenação
- ⚠️ **Cuidado:** a peça Pressada fica vulnerável (não pode se mover para fugir)
- ❌ **Evite Press quando:** a peça Pressada ficar em posição insegura, ou quando a mobilidade é mais importante que velocidade

---

## 6. Peças e Movimentação

### 6.1 Arconte (Ar) — O Líder

```
  . M .
  M ★ M
  . M .
```

| Atributo | Valor |
|---|---|
| Quantidade | 1 |
| Movimento | 1 casa em qualquer direção (ortogonal ou diagonal) |
| Captura | Por deslocamento (move-se para a casa da peça inimiga) |
| Especial | **Não pode ser Pressado.** Nunca fica Exausto. |
| Restrição | Nenhuma — pode mover-se para qualquer casa adjacente livre ou ocupada por inimigo |

**Detalhes:**
- O Arconte se move exatamente como o Rei do xadrez: 1 casa em qualquer das 8 direções
- Diferente do xadrez: NÃO existe "xeque". O Arconte PODE se mover para uma casa ameaçada por peça inimiga (por sua conta e risco)
- Se o Arconte for capturado, o jogo acaba imediatamente
- O Arconte pode capturar qualquer peça inimiga adjacente (exceto Hoplitas em Muralha de Escudos)

---

### 6.2 Strategos (St) — O General

```
  D . D . D
  . D D D .
  . D ✦ D .
  . D D D .
  D . D . D
```

| Atributo | Valor |
|---|---|
| Quantidade | 1 |
| Movimento | Até 3 casas em qualquer **direção única** (ortogonal ou diagonal) |
| Captura | Por deslocamento |
| Especial | Nenhuma habilidade adicional |
| Restrição | Não pode pular sobre outras peças |

**Detalhes:**
- O Strategos é a peça mais poderosa e versátil do jogo
- Move-se em linha reta: até 3 casas para norte, sul, leste, oeste, ou qualquer diagonal
- Não pode mudar de direção durante o movimento (move em linha reta)
- Não pode pular sobre peças (amigas ou inimigas) — caminho deve estar livre
- Pode parar em qualquer casa ao longo do caminho (1, 2 ou 3 casas)
- Captura ocupando a casa da peça inimiga (se alcançável)

**Exemplo:** Strategos em d4 pode mover-se para: d5, d6, d7 (norte); d3, d2, d1 (sul); e4, f4, g4 (leste); c4, b4, a4 (oeste); e5, f6, g7 (NE diagonal); e3, f2, g1 (SE diagonal); c5, b6, a7 (NW diagonal); c3, b2, a1 (SW diagonal) — desde que o caminho esteja livre.

---

### 6.3 Hoplita (Ho) — A Infantaria Pesada

```
  . M .
  . ◈ .
  . M .
```
*(apenas ortogonal, até 2 casas)*

| Atributo | Valor |
|---|---|
| Quantidade | 2 |
| Movimento | Até 2 casas em direção **ortogonal** (norte, sul, leste, oeste) |
| Captura | Por deslocamento |
| Especial | **Muralha de Escudos** (ver seção 8.1) |
| Restrição | Não se move na diagonal. Não pula sobre peças. |

**Detalhes:**
- Move-se ortogonalmente (cima, baixo, esquerda, direita) até 2 casas
- Não se move na diagonal em hipótese nenhuma
- Não pode pular sobre peças
- Individualmente, é uma peça modesta — seu poder está na formação

---

### 6.4 Toxotes (To) — O Arqueiro

```
  D . . . D
  . D . D .
  . . ◇ . .
  . D . D .
  D . . . D
```
*(diagonal até 2, + Ataque à Distância)*

| Atributo | Valor |
|---|---|
| Quantidade | 2 |
| Movimento | Até 2 casas na **diagonal** |
| Captura (normal) | Por deslocamento (movendo-se até a casa do inimigo diagonalmente) |
| Especial | **Ataque à Distância** (ver seção 8.2) |
| Restrição | Não se move ortogonalmente. Não pula sobre peças durante movimento. |

**Detalhes:**
- Move-se diagonalmente até 2 casas (como um bispo limitado)
- Seu verdadeiro poder é o Ataque à Distância (habilidade especial)
- Peça de controle e ameaça — projeta perigo sem se expor

---

### 6.5 Hippeus (Hi) — A Cavalaria

```
  . X . X .
  X . . . X
  . . ◆ . .
  X . . . X
  . X . X .
```
*(movimento em L)*

| Atributo | Valor |
|---|---|
| Quantidade | 2 |
| Movimento | Em **L**: 2 casas em uma direção ortogonal + 1 casa perpendicular (ou 3+1) |
| Captura | Por deslocamento |
| Especial | **Investida** — após capturar, pode mover mais 1 casa em qualquer direção (ver seção 8.3) |
| Restrição | Nenhuma — **salta sobre peças** no caminho |

**Detalhes:**
- Move-se exatamente como o Cavalo do xadrez: 2 casas numa direção + 1 perpendicular
- Pode também mover 3 casas numa direção + 1 perpendicular (L estendido – "Grande L")
- **IMPORTANTE:** O "Grande L" (3+1) é uma mecânica exclusiva de Kairós que amplia o alcance da cavalaria
- Pula sobre qualquer peça (amiga ou inimiga) no caminho
- Exemplo de casas alcançáveis a partir de d4:
  - L padrão (2+1): c6, e6, f5, f3, e2, c2, b3, b5
  - L estendido (3+1): c7, e7, g5, g3, e1, c1, a3, a5

> **Nota sobre balanceamento:** O Grande L (3+1) dá ao Hippeus um alcance excepcional, compensando ter apenas 2 unidades. O jogador deve escolher entre o L padrão (2+1) ou o Grande L (3+1) — não ambos no mesmo movimento.

---

### 6.6 Doríforo (Do) — O Lanceiro

```
  X M X      (direção de ataque do Ouro: ↑)
  . ● .
  . . .
```

| Atributo | Valor |
|---|---|
| Quantidade | 4 |
| Movimento | **1 casa para frente** (em direção ao lado do oponente). No primeiro movimento, pode avançar **1 ou 2** casas para frente. |
| Captura | **1 casa na diagonal frontal** (diagonal-esquerda ou diagonal-direita, avançando) |
| Especial | **Promoção** ao alcançar a última linha (ver seção 9) |
| Restrição | Não se move para trás. Não se move para os lados. Não captura para frente. |

**Detalhes:**
- "Frente" para Ouro = em direção à linha 8. "Frente" para Prata = em direção à linha 1.
- Primeiro movimento (da posição inicial): pode avançar 1 ou 2 casas. Depois, sempre 1.
- Captura apenas na diagonal frontal (exatamente como o peão do xadrez)
- Não pode recuar em hipótese nenhuma
- Não existe "en passant" em Kairós

---

## 7. Capturas

### 7.1 Captura por Deslocamento (padrão)
A maioria das capturas em Kairós é por **deslocamento**: uma peça se move para uma casa ocupada por uma peça inimiga, removendo a peça inimiga do tabuleiro.

**Regras gerais de captura:**
- Capturar é **opcional** (exceto quando é a única jogada legal)
- Peças capturadas são **removidas permanentemente** do jogo
- A peça que captura **ocupa a casa** da peça capturada
- Você **não pode** capturar suas próprias peças
- Você **pode** capturar o Arconte inimigo (o que encerra o jogo)

### 7.2 Exceções

| Situação | Regra |
|---|---|
| Hoplita em Muralha de Escudos | **Não pode ser capturado** (ver seção 8.1) |
| Ataque à Distância (Toxotes) | Captura **sem se mover** — a peça atacante permanece na casa de origem (ver seção 8.2) |
| Investida (Hippeus) | Após capturar, pode mover 1 casa adicional, podendo capturar novamente (ver seção 8.3) |

---

## 8. Habilidades Especiais

### 8.1 Muralha de Escudos (Hoplitas)

**Condição de ativação:**
Dois Hoplitas **aliados** (do mesmo jogador) estão em casas **adjacentes ortogonalmente** (lado a lado horizontal ou verticalmente — NÃO na diagonal).

**Efeito:**
- Enquanto em Muralha, **nenhum dos dois Hoplitas pode ser capturado** por nenhuma peça inimiga (nem por Ataque à Distância)
- A Muralha é **passiva e automática** — não custa ação para ativar
- A Muralha **se desfaz** quando um dos Hoplitas se move para fora da adjacência

**Esclarecimentos:**
- Hoplitas em Muralha ainda podem se mover livremente (mas ao mover, a muralha pode se desfazer)
- Hoplitas Exaustos MANTÊM a Muralha (a proteção não depende de estar Pronto)
- A Muralha funciona contra TODAS as formas de captura, incluindo Investida e Ataque à Distância
- O Arconte NÃO pode formar Muralha (apenas Hoplitas entre si)
- Se um Hoplita é o único do jogador (o outro foi capturado), ele nunca pode formar Muralha

**Exemplo:**
```
  . . . . .
  . Ho Ho . .    ← Muralha ativa (f4-g4): nenhum é capturável
  . . . . .
```
Se Ho(f4) se move para f5:
```
  . Ho . . .
  . . Ho . .    ← Muralha desfeita: g4 voltou a ser capturável
  . . . . .
```

**Exceção crítica:** A Muralha protege contra captura, mas NÃO impede outras peças de **passarem** ou **moverem-se adjacentemente**. Ela não bloqueia movimento — apenas torna os Hoplitas imunes à captura.

---

### 8.2 Ataque à Distância (Toxotes)

**Ação:** Em vez de se mover, o Toxotes pode remover uma peça inimiga a exatamente **2 casas de distância** em qualquer direção reta (ortogonal ou diagonal), sem sair da sua casa.

**Condições:**
- A casa entre o Toxotes e o alvo deve estar **vazia** (linha de visão livre)
- O alvo deve ser uma **peça inimiga** (não pode atacar peça amiga)
- O alvo NÃO pode ser um Hoplita em Muralha de Escudos
- O Toxotes **não se move** — permanece na sua casa
- Conta como a ação do turno (Movimento Principal ou Press)

**Alcance visual:**
```
  X . X . X
  . . . . .       X = possíveis alvos do Toxotes em d4
  X . ◇ . X       (se casa intermediária estiver vazia)
  . . . . .
  X . X . X
```

O Toxotes em d4 pode atingir: d6, d2, f4, b4, f6, b6, f2, b2

**Exemplo:**
```
Antes:                          Depois:
  . . . . .                      . . . . .
  . . Ho* . .   Ataque à          . . [x] . .   Ho* removido
  . . . . .    distância          . . . . .     Toxotes
  . . ◇ . .   ─────────→         . . ◇ . .     não se moveu
  . . . . .                      . . . . .

  *Ho = Hoplita inimigo (NÃO em Muralha)
  Condição: casa entre ◇ e Ho* estava vazia ✓
```

**Esclarecimentos:**
- Se a casa intermediária estiver ocupada (por qualquer peça), o tiro é BLOQUEADO naquela direção
- O Ataque à Distância pode ser usado como ação de Press (a peça fica Exausta mesmo sem mover)
- Ataque à Distância pode capturar o Arconte inimigo (vitória imediata!)

---

### 8.3 Investida (Hippeus)

**Ativação:** Quando um Hippeus **captura** uma peça inimiga (por deslocamento normal, movendo-se para a casa do inimigo).

**Efeito:** Após a captura, o Hippeus pode opcionalmente mover-se **1 casa adicional em qualquer direção** (ortogonal ou diagonal). Se essa casa adicional contiver uma peça inimiga, o Hippeus a captura também.

**Regras da Investida:**
- O movimento adicional é de **exatamente 1 casa** (não em L)
- É **opcional** — o Hippeus pode parar na casa da primeira captura
- Pode capturar uma segunda peça inimiga (dupla captura)
- NÃO pode capturar peça amiga
- NÃO pode capturar Hoplita em Muralha de Escudos
- O movimento adicional NÃO pode ser outro movimento em L
- A Investida NÃO gera uma terceira captura — é apenas 1 movimento extra

**Exemplo:**
```
Antes:                       Depois da captura + Investida:
  . . . . .                   . . . . .
  . . St* . .                  . . . . .     St* capturado
  . . . . .                   . . ◆ . .     Hippeus usa Investida
  . ◆ . . .     ────→         . . . . .     +1 casa (p/ cima-direita)
  . . . . .                   . . . . .

Hippeus em b3 captura St* em c5 (L: 2↑1→)
Investida: move 1 casa adicional para d4 (ou qualquer direção)
```

**Investida Dupla (captura dupla):**
```
Antes:                       Passo 1: Captura em L    Passo 2: Investida
  . . . To* .                 . . . To* .              . . . . .
  . . . . .                   . . ◆ . .               . . . ◆ .
  . ◆ . . .     ────→         . . . . .     ────→     . . . . .
  . . . . .                   . . . . .               . . . . .

Hippeus b3→c5 (captura peça em c5). Investida d6 captura To* em d6.
```

---

## 9. Promoção

### Regra de Promoção

Quando um **Doríforo** alcança a **última linha** do tabuleiro (linha 8 para Ouro, linha 1 para Prata), ele é **imediatamente promovido** à escolha do jogador.

### Opções de Promoção

O jogador escolhe transformar o Doríforo em **uma** das seguintes peças:

| Promoção | Quando escolher |
|---|---|
| **Strategos** | Máxima versatilidade e poder ofensivo |
| **Hoplita** | Reforço defensivo, possibilidade de formar Muralha |
| **Toxotes** | Controle à distância, projeção de ameaça |
| **Hippeus** | Mobilidade tática, potencial de Investida |

### Regras da Promoção
- A promoção é **obrigatória** (o Doríforo não pode permanecer como Doríforo na última linha)
- A promoção é **imediata** — acontece no mesmo turno em que o Doríforo alcança a última linha
- O jogador pode ter múltiplas peças do mesmo tipo (ex: 3 Hoplitas após promoção)
- **Não pode promover a Arconte** — existe apenas 1 Arconte por jogador
- Se o Doríforo chegar à última linha por Press, a promoção ocorre normalmente e a peça promovida fica Exausta

---

## 10. Condições de Vitória

### Vitória Principal: Captura do Arconte

Você vence imediatamente ao **capturar o Arconte adversário**. Isso pode acontecer por:

1. **Deslocamento direto** — qualquer peça sua se move para a casa do Arconte inimigo
2. **Ataque à Distância** — um Toxotes remove o Arconte inimigo à distância
3. **Investida** — um Hippeus captura outra peça e, no movimento extra, captura o Arconte

O jogo acaba **no instante** da captura. Não há "match point" ou "último turno".

### Vitória Secundária: Abandono

O oponente pode **abandonar** (resignar) a qualquer momento, concedendo a vitória.

### Vitória por Tempo (apenas em partidas cronometradas)

Se o relógio de um jogador chegar a zero, ele perde — desde que o adversário tenha **material suficiente para forçar a captura do Arconte** (pelo menos 1 peça além do próprio Arconte).

---

## 11. Condições de Empate

Empates são raros em Kairós por design, mas podem ocorrer:

### 11.1 Material Insuficiente
Se ambos os jogadores possuem APENAS o Arconte (todas as outras peças foram capturadas), o jogo é empate. Nenhum Arconte pode capturar o outro sem se expor.

> **Exceção:** Arconte + 1 peça vs. Arconte sozinho NÃO é empate — o lado com vantagem pode forçar a captura.

### 11.2 Regra dos 50 Movimentos
Se **50 turnos consecutivos** (25 de cada jogador) passarem sem nenhuma captura e sem nenhum movimento de Doríforo, qualquer jogador pode reivindicar empate.

### 11.3 Repetição Tripla
Se a **mesma posição exata** (mesmas peças, mesmas casas, mesmo estado de Exaustão, mesmo jogador a mover) ocorrer **3 vezes** durante a partida, qualquer jogador pode reivindicar empate.

### 11.4 Acordo Mútuo
Ambos os jogadores podem concordar com empate a qualquer momento.

### 11.5 Impossibilidade de Mover (raríssimo)
Se um jogador não possui nenhuma jogada legal (todas as peças estão bloqueadas e o Arconte cercado), o jogo é empate. Na prática, isso é quase impossível dado que o Arconte sempre pode se mover para casas adjacentes.

### Nota sobre Empates Competitivos
Em torneios, o empate por acordo mútuo pode ser proibido antes do turno 30 para evitar empates prematuros.

---

## 12. Regras Especiais e Esclarecimentos

### 12.1 Peças Bloqueadas
- Uma peça que não pode se mover (todas as casas de destino estão ocupadas por peças amigas ou fora do tabuleiro) simplesmente não pode ser escolhida para o turno
- Se NENHUMA peça pode se mover (situação extremamente rara), o jogo é empate

### 12.2 Exaustão e Muralha de Escudos
- Um Hoplita Exausto MANTÉM a Muralha de Escudos se adjacente a outro Hoplita aliado
- A Muralha não depende de a peça estar Pronta — depende apenas de posição

### 12.3 Exaustão e Captura
- Uma peça Exausta **pode ser capturada** normalmente (Exaustão não dá proteção, exceto via Muralha)
- Uma peça Exausta **não pode se mover, capturar, ou usar habilidades**

### 12.4 Cadeia de Habilidades
- **Investida durante Press:** Se um Hippeus é Pressado e captura, ele PODE usar Investida. Porém, o Hippeus fica Exausto ao final (por ter sido Pressado)
- **Ataque à Distância durante Press:** Se um Toxotes é Pressado e usa Ataque à Distância, ele fica Exausto ao final

### 12.5 Auto-captura
- Você NÃO pode colocar uma peça em uma casa ocupada por peça aliada (não existe auto-captura)

### 12.6 Sem Movimentos Especiais de Posição Inicial
- Não existe equivalente a "roque" em Kairós

### 12.7 Precedência de Regras
Em caso de conflito, a precedência é:
1. Muralha de Escudos (imunidade) prevalece sobre qualquer forma de captura
2. O Arconte não pode ser Pressado (prevalece sobre qualquer benefício tático)
3. Promoção é obrigatória (prevalece sobre preferência do jogador)

---

## 13. Exemplos Práticos

### Exemplo 1: Abertura Básica (3 primeiros turnos)

**Turno 1 — Ouro:**
- Fase 2: Do(d2)→d4 (Doríforo avança 2 casas)
- Fase 3: Não Pressa

**Turno 1 — Prata:**
- Fase 2: Do(e7)→e5 (Doríforo avança 2 casas)
- Fase 3: Não Pressa

**Turno 2 — Ouro:**
- Fase 2: St(e1)→e3 (Strategos avança para apoiar centro)
- Fase 3: Press — To(b1)→c2 (Toxotes se posiciona na diagonal). To(c2) fica Exausto.

**Turno 2 — Prata:**
- Fase 1: (nenhuma peça Exausta para recuperar)
- Fase 2: Ho(c8)→c6 (Hoplita avança)
- Fase 3: Press — Ho(f8)→f6 (segundo Hoplita avança). Prata posicionou ambos os Hoplitas para potencial Muralha futura.

**Turno 3 — Ouro:**
- Fase 1: To(c2) recupera (remove marcador de Exaustão)
- Fase 2: Ho(c1)→c3 (Hoplita avança para proteger flanco)
- Fase 3: Não Pressa (conserva mobilidade)

### Exemplo 2: Muralha de Escudos em Ação

Situação: Prata possui Ho(d5) e Ho(e5).
```
  . . . Ho Ho . . .     ← Muralha ativa: d5-e5
  . . . . . . . .
```

Ouro tem St(d3) que poderia capturar Ho(d5). Mas a Muralha impede!

**Ouro precisa:** Forçar um dos Hoplitas a se mover (talvez ameaçando uma peça atrás deles), desfazendo a Muralha. Só então pode capturá-los.

### Exemplo 3: Ataque à Distância Decisivo

Situação:
```
  . . . . . . . .
  . . Ar* . . . . .     ← Arconte de Prata em c7
  . . . . . . . .
  . . ◇ . . . . .       ← Toxotes de Ouro em c5
  . . . . . . . .
```

Casa entre c5 e c7 (que é c6) está vazia? **SIM.**

**Ouro joga:** Ataque à Distância → Toxotes(c5) captura Arconte(c7) à distância.

**OURO VENCE!** O Arconte foi capturado sem aviso, sem xeque. O Prata deveria ter previsto a ameaça.

### Exemplo 4: Investida Dupla

```
  . . . Do* . . . .      ← Doríforo de Prata em d6
  . . . . Ar* . . .      ← Arconte de Prata em e5
  . . . . . . . .
  . . ◆ . . . . .        ← Hippeus de Ouro em c3
```

**Ouro joga:** Hippeus(c3) move em L (2↑1→) para d5, capturando... nada em d5 (casa vazia).

Espere — vamos reposicionar para um exemplo melhor:

```
  . . . . . . . .
  . . . To* . . . .      ← Toxotes de Prata em d6
  . . . . Ar* . . .      ← Arconte de Prata em e5
  . . . . . . . .
  . . ◆ . . . . .        ← Hippeus de Ouro em c3
```

**Ouro joga:** Hippeus(c3) move em L (2↑1→) para d5. Essa casa está vazia, então não há captura.

Outro exemplo correto:

```
  . . . . . . . .
  . . . . . . . .
  . . . To* Ar* . . .    ← Prata: To*(d5), Ar*(e5)
  . . . . . . . .
  . . ◆ . . . . .        ← Ouro: Hippeus em c3
```

**Ouro joga:** Hippeus(c3) → captura To*(d5) via L (2↑1→).
**Investida:** Hippeus agora em d5, move 1 casa para e5 → captura Ar*(e5).

**OURO VENCE!** Investida dupla — capturou o Toxotes e na sequência o Arconte. Jogada devastadora.

### Exemplo 5: Dilema de Press

Situação: Ouro precisa defender o Arconte E atacar uma peça valiosa.

```
  . . . . . . . .
  . . . St . . . .       ← Strategos de Ouro em d6, pode capturar peça em d8
  . . . . . . . .
  Hi* . . . . . . .      ← Hippeus de Prata em a4, ameaça Arconte de Ouro
  . . . Ar . . . .       ← Arconte de Ouro em d3
  . . . . . . . .
```

**Opções de Ouro:**
1. **Mover Arconte** (d3→c2) para fugir do Hippeus — seguro mas perde oportunidade de ataque
2. **Mover Strategos** (d6→d8 captura peça) + **Press Arconte** — PROIBIDO! Arconte não pode ser Pressado
3. **Mover Arconte** (d3→c2) + **Press Strategos** (d6→d8 captura) — Legal! Arconte foge como movimento principal, Strategos ataca como Press. Strategos fica Exausto.

Opção 3 é a melhor: resolve ambos os problemas, ao custo de Strategos Exausto por 1 turno.

---

## 14. Referência Rápida

### Tabela de Movimentação

| Peça | Direção | Alcance | Captura | Pula peças? |
|---|---|---|---|---|
| Arconte (★) | Qualquer | 1 casa | Deslocamento | Não |
| Strategos (✦) | Qualquer | 1-3 casas | Deslocamento | Não |
| Hoplita (◈) | Ortogonal | 1-2 casas | Deslocamento | Não |
| Toxotes (◇) | Diagonal | 1-2 casas | Deslocamento + Ranged | Não |
| Hippeus (◆) | L (2+1 ou 3+1) | Fixo | Deslocamento | **Sim** |
| Doríforo (●) | Frente | 1 (ou 2 no 1º mov.) | Diagonal frontal | Não |

### Tabela de Habilidades Especiais

| Habilidade | Peça | Efeito |
|---|---|---|
| Imune a Press | Arconte | Nunca pode ser Pressado/Exausto |
| Muralha de Escudos | Hoplita | 2 Hoplitas adjacentes = imunes a captura |
| Ataque à Distância | Toxotes | Captura a 2 casas sem mover (linha de visão) |
| Investida | Hippeus | +1 movimento após captura (pode capturar de novo) |
| Promoção | Doríforo | Vira St/Ho/To/Hi na última linha |

### Checklist de Turno

```
□ Fase 1: Recuperar peças Exaustas
□ Fase 2: Mover 1 peça (obrigatório)
□ Fase 3: Press? (opcional — custa Exaustão)
```

---

## 15. Curva de Aprendizado

### Nível 1 — Iniciante (1ª partida)
**Foco:** Aprender a movimentação de cada peça e a condição de vitória.
- Jogue sem usar Press nos primeiros jogos
- Concentre-se em mover Doríforos para frente e peças maiores para posições centrais
- Aprenda que o Arconte deve ser protegido (cercado por peças amigas)
- Cometa o erro de deixar o Arconte exposto e aprenda com a derrota

### Nível 2 — Aprendiz (5-10 partidas)
**Foco:** Introduzir o Press e habilidades especiais.
- Comece a usar Press em situações claras (atacar E defender no mesmo turno)
- Pratique a Muralha de Escudos (posicionar Hoplitas adjacentes)
- Experimente o Ataque à Distância dos Toxotai
- Tente a Investida dupla dos Hippeis

### Nível 3 — Intermediário (20-50 partidas)
**Foco:** Posicionamento estratégico e gestão de Press.
- Desenvolva senso de quando Pressionar (vale a Exaustão?)
- Planeje com 2-3 turnos de antecedência
- Reconheça padrões de ameaça (Toxotes alinhado com Arconte a 2 casas)
- Gerencie trocas de material (vale sacrificar Hoplita por Toxotes?)

### Nível 4 — Avançado (100+ partidas)
**Foco:** Controle de tempo, blefe posicional, abertura e finais.
- Domine aberturas (sequências iniciais conhecidas)
- Use Press como ferramenta psicológica (forçar decisões difíceis)
- Planeje finais (Arconte + Strategos vs Arconte + Hoplita)
- Leia padrões do adversário (estilo agressivo vs defensivo)

### Nível 5 — Especialista (500+ partidas)
**Foco:** Criação de teoria, inovação, domínio completo.
- Crie novas linhas de abertura
- Calcule variantes de 5+ turnos com Press
- Domine o tempo como recurso (sacrificar Exaustão por vantagem posicional)
- Jogue com relógio em configurações competitivas
