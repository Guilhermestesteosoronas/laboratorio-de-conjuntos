# Laboratório de Conjuntos

Trabalho em equipe para resolver **3 desafios de programação** com base na **Teoria dos Conjuntos**.

---

## Estrutura do projeto

```
laboratorio-de-conjuntos/
├── Parte 01/          # Operações básicas entre conjuntos (C)
│   └── src/
│       ├── main.c
│       └── funcoes/
│           ├── conjuntos.h
│           └── conjuntos.c
├── Parte 02/          # Classificação de números + divisores + primos (Java)
│   └── src/
│       ├── funcoes/
│       │   ├── Classificador.java
│       │   ├── Divisores.java
│       │   └── Primos.java
│       ├── TesteClassificador.java
│       ├── TesteDivisores.java
│       └── TestePrimos.java
├── Parte 03/          # Intervalos reais (união, interseção, pertinência) (Java)
│   └── src/
│       ├── Intervalo.java
│       └── Main.java
└── README.md
```

---

## Parte 01 — Operações com conjuntos (C)

### Decisões de projeto
- Representação de conjuntos como **vetores de inteiros** + tamanho (sem uso de estruturas avançadas).
- Menu interativo com 14 operações clássicas da teoria dos conjuntos.
- Elementos repetidos na entrada são tratados nas operações (cardinalidade conta apenas distintos).
- Complemento é calculado em relação a um **universo finito** definido pelo usuário (ou padrão 1..20).

### Como compilar e executar
```bash
cd "Parte 01/src"
gcc -o conjuntos main.c funcoes/conjuntos.c -I.
./conjuntos
```

### Exemplo de execução (cenário 1 — conjuntos com interseção)

**Entrada:**
- A = {1, 2, 3}
- B = {3, 4, 5}

| Operação              | Resultado esperado (à mão) | Saída do programa          |
|-----------------------|----------------------------|----------------------------|
| União (A ∪ B)         | {1, 2, 3, 4, 5}            | {1 2 3 4 5}                |
| Interseção (A ∩ B)    | {3}                        | { 3 }                      |
| Diferença (A − B)     | {1, 2}                     | {1 2 }                     |
| Diferença (B − A)     | {4, 5}                     | {4 5 }                     |
| Diferença simétrica   | {1, 2, 4, 5}               | { 1 2 4 5 }                |
| A ⊆ B                 | falso                      | O conjunto A não está contido no conjunto B |
| A ⊂ B                 | falso                      | O conjunto A não está propriamente contido no conjunto B |
| \|A\|                 | 3                          | \|A\| = 3                  |

### Casos de teste obrigatórios (Parte 01)

#### 1. Conjunto vazio
- A = ∅ (quantidade 0), B = {1, 2}
- União = B, Interseção = ∅, A − B = ∅, B − A = B, A ⊆ B = verdadeiro

#### 2. Conjuntos iguais
- A = {1, 2, 3}, B = {1, 2, 3}
- União = A, Interseção = A, Diferenças = ∅, A ⊆ B e B ⊆ A = verdadeiro, A ⊂ B = falso

#### 3. Conjuntos disjuntos
- A = {1, 2}, B = {3, 4}
- Interseção = ∅, Diferença simétrica = {1, 2, 3, 4}

#### 4. Elementos repetidos na entrada
- A = {1, 1, 2, 2, 3}, B = {2, 3, 3, 4}
- Cardinalidade |A| deve considerar apenas distintos → 3
- Interseção deve retornar {2, 3} (sem duplicatas extras)

---

## Parte 02 — Classificação de números, divisores e primos (Java)

### Decisões de projeto
- **Classificador**: reconhece inteiros, frações, dízimas periódicas, raízes e constantes (π, e) e classifica nos conjuntos ℕ, ℤ, ℚ, ℝ, 𝕀.
- Dízimas são convertidas para **fração geratriz** e depois classificadas.
- **Primos**: Crivo de Eratóstenes (eficiente e clássico).
- **Divisores**: iteração até √n + ordenação.

### Como compilar e executar
```bash
cd "Parte 02/src"
javac -encoding UTF-8 funcoes/*.java Teste*.java
java TesteClassificador
java TesteDivisores
java TestePrimos
```

### Exemplos de execução

**TesteClassificador (trecho):**
```
Entrada: 0.(3)
Dízima periódica = fração geratriz 1/3
Racional (ℚ) e Real (ℝ).

Entrada: 5
Natural (ℕ), Inteiro (ℤ), Racional (ℚ) e Real (ℝ).

Entrada: -7
Inteiro (ℤ), Racional (ℚ) e Real (ℝ).

Entrada: pi
Irracional (𝕀) e Real (ℝ).

Entrada: √2
Irracional (𝕀) e Real (ℝ).

Entrada: sqrt(9)
Natural (ℕ), Inteiro (ℤ), Racional (ℚ) e Real (ℝ).
```

**TestePrimos:**
```
Digite um número: 20
Primos até 20: [2, 3, 5, 7, 11, 13, 17, 19]
```

**TesteDivisores:**
```
Digite um número: 12
Divisores de 12: [1, 2, 3, 4, 6, 12]
```

### Casos de teste (Parte 02)
- Inteiro positivo / negativo / zero
- Fração própria e imprópria (6/3 → natural)
- Dízima 0.(9) → 1 (natural)
- Raiz perfeita vs não-perfeita
- Entrada inválida (“abc”, “5/0”)

---

## Parte 03 — Intervalos reais (Java)

### Decisões de projeto
- Classe `Intervalo` imutável com extremos aberto/fechado e suporte a ±∞.
- Interseção retorna `Optional<Intervalo>` (vazio quando não há interseção).
- União retorna `List<Intervalo>` (pode resultar em 1 ou 2 intervalos).
- Validação no construtor: início ≤ fim e intervalo unitário só se fechado.

### Como compilar e executar
```bash
cd "Parte 03/src"
javac -encoding UTF-8 *.java
java Main
```

### Exemplos de execução (saída do `Main`)

```
===== contem =====
[1.0, 5.0] contem 1?    true
[1.0, 5.0] contem 5?    true
(1.0, 5.0) contem 1?    false

===== interseccao =====
[1.0, 5.0] ∩ [3.0, 8.0] = [3.0, 5.0]
[1.0, 5.0] ∩ (5.0, 8.0] = vazia
[1.0, 2.0] ∩ [3.0, 4.0] = vazia

===== uniao =====
[1.0, 3.0] ∪ [2.0, 5.0] = [[1.0, 5.0]]
[1.0, 3.0] ∪ [5.0, 8.0] = [[1.0, 3.0], [5.0, 8.0]]
[1.0, 3.0) ∪ [3.0, 5.0] = [[1.0, 5.0]]

===== validacoes =====
Erro ao criar: O início não pode ser maior que o fim.
Erro ao criar: Intervalo vazio.
Criado: [3.0, 3.0]

===== infinitos =====
Criado: [0.0, Infinity)
(-Infinity, 3.0] ∩ [0.0, Infinity) = [0.0, 3.0]
(-Infinity, 0.0) ∪ [0.0, Infinity) = [(-Infinity, Infinity)]
```

### Casos de teste (Parte 03)
- Intervalos abertos, fechados e semiabertos
- Interseção vazia / ponto único / intervalo
- União de intervalos disjuntos, adjacentes e sobrepostos
- Intervalo degenerado [a, a]
- Extremos ±∞

---

## Onde a Teoria dos Conjuntos aparece no código

| Conceito              | Onde aparece                                      |
|-----------------------|---------------------------------------------------|
| União, interseção, diferença, diferença simétrica | `Parte 01` — funções `uniao`, `intersecao`, `diferencaAB/BA`, `diferencaSimetrica` |
| Pertinência (∈)       | `Parte 01` — `pertinencia` e `Parte 03` — `contem` |
| Inclusão (⊆, ⊂)       | `Parte 01` — `contidoAB`, `propriamenteContidoAB` |
| Cardinalidade (\| \|) | `Parte 01` — `cardinalidadeA/B`                   |
| Complemento           | `Parte 01` — `complementoA/B` (universo finito)   |
| Conjuntos numéricos ℕ, ℤ, ℚ, ℝ, 𝕀 | `Parte 02` — `Classificador`                  |
| Intervalos como conjuntos de ℝ | `Parte 03` — classe `Intervalo` (união e interseção) |

---

## Operação mais difícil de implementar

A **união de intervalos** (`Parte 03`) foi a mais trabalhosa.

Motivos:
1. É preciso considerar **todos os casos de abertura/fechamento** dos extremos (aberto + aberto, aberto + fechado etc.).
2. Intervalos adjacentes (ex.: [1, 3) ∪ [3, 5]) devem ser **fundidos** ou não, dependendo se o ponto de contato fica coberto.
3. O resultado pode ser **um ou dois intervalos**, exigindo retorno de lista.
4. Extremos infinitos adicionam casos especiais (nunca são fechados).

---

## Autores / Equipe
- Repositório: [Guilhermestesteosoronas/laboratorio-de-conjuntos](https://github.com/Guilhermestesteosoronas/laboratorio-de-conjuntos)
