# Notação Big O

Forma padrão de descrever **quanto tempo uma operação leva** conforme o tamanho dos dados cresce. Não mede tempo em segundos — mede **como o tempo escala**.

## Resumo Rápido

| Notação | Nome | Velocidade | Exemplo |
|---------|------|------------|---------|
| O(1) | Constante | Sempre rápido | `ArrayList.get(i)`, `HashMap.get(k)` |
| O(log n) | Logarítmico | Muito rápido | Busca binária, `TreeMap.get(k)` |
| O(n) | Linear | Proporcional ao tamanho | Percorrer lista, `LinkedList.get(i)` |
| O(n log n) | Linearítmico | Bom para ordenação | `Arrays.sort()`, `Collections.sort()` |
| O(n²) | Quadrático | Lento para dados grandes | Loop dentro de loop |

---

## O(1) — Tempo Constante

A operação é **sempre rápida**, independente do tamanho dos dados.

**Analogia:** Abrir um livro na página marcada — não importa se tem 100 ou 10.000 páginas.

```java
ArrayList<String> lista = new ArrayList<>(); // ... 1 milhão de itens

lista.get(0);        // O(1) — rápido
lista.get(999999);   // O(1) — igualmente rápido
```

**Por que ArrayList.get() é O(1)?**
Internamente é um array contíguo na memória. O Java calcula o endereço exato do índice sem percorrer nada.

```
Memória: [A][B][C][D][E]
get(3) → endereço_base + (3 × tamanho_elemento) → vai direto no D
```

**Outros exemplos O(1):**
- `HashMap.get(chave)` / `HashMap.put(chave, valor)`
- `ArrayList.add(elemento)` (no final, sem redimensionar)
- `Stack.push()` / `Stack.pop()`

---

## O(n) — Tempo Linear

A operação fica **mais lenta proporcionalmente** ao tamanho dos dados. Dobrou os dados → dobrou o tempo.

**Analogia:** Procurar alguém numa fila de pessoas — quanto maior a fila, mais demora.

```java
LinkedList<String> lista = new LinkedList<>(); // ... 1 milhão de itens

lista.get(500000);   // O(n) — percorre nó a nó até chegar lá
```

**Por que LinkedList.get() é O(n)?**
É uma cadeia de nós onde cada nó aponta pro próximo. Não tem como pular direto — precisa seguir os ponteiros um a um.

```
Memória: [A]→[B]→[C]→[D]→[E]
get(3) → começa em A → segue pra B → segue pra C → segue pra D ✓
```

**Outros exemplos O(n):**
- `ArrayList.add(0, elemento)` (inserir no início — empurra todos)
- `ArrayList.remove(0)` (remover do início — puxa todos)
- `ArrayList.contains(elemento)` (percorre até achar)
- `LinkedList.get(i)` (percorre nó a nó)

---

## O(log n) — Tempo Logarítmico

A cada passo, **descarta metade** dos dados. Muito eficiente mesmo com milhões de elementos.

**Analogia:** Procurar uma palavra no dicionário — abre no meio, vê se a palavra vem antes ou depois, e repete com a metade restante.

```
1.000.000 de elementos → ~20 passos
1.000.000.000 de elementos → ~30 passos
```

**Exemplo clássico: Busca Binária**
```java
int[] ordenado = {1, 3, 5, 7, 9, 11, 13, 15};

// Procurando o 11:
// Passo 1: meio = 7  → 11 > 7, descarta metade esquerda
// Passo 2: meio = 11 → encontrou!
```

**Outros exemplos O(log n):**
- `TreeMap.get(chave)` / `TreeMap.put(chave, valor)`
- `TreeSet.contains(elemento)`
- `Collections.binarySearch(lista, elemento)`

---

## O(n log n) — Tempo Linearítmico

É o melhor caso possível para **algoritmos de ordenação baseados em comparação**. Mais rápido que O(n²), mais lento que O(n).

```java
List<Integer> numeros = new ArrayList<>(List.of(5, 2, 8, 1, 9));

Collections.sort(numeros);   // O(n log n)
numeros.stream().sorted();   // O(n log n)
Arrays.sort(array);          // O(n log n)
```

---

## O(n²) — Tempo Quadrático

A operação cresce com o **quadrado** do tamanho dos dados. Geralmente acontece com **loop dentro de loop**.

**Analogia:** Comparar cada pessoa de um grupo com todas as outras — 10 pessoas = 100 comparações, 100 pessoas = 10.000.

```java
// Encontrar duplicatas de forma ingênua
for (int i = 0; i < lista.size(); i++) {
    for (int j = i + 1; j < lista.size(); j++) {
        if (lista.get(i).equals(lista.get(j))) {
            // duplicata!
        }
    }
}
```

---

## Visualização de Crescimento

Com 1.000 elementos, quantas operações cada complexidade faz?

```
O(1)       →           1  operação   ⚡
O(log n)   →          10  operações  ⚡
O(n)       →       1.000  operações  ✓
O(n log n) →      10.000  operações  ✓
O(n²)      →   1.000.000  operações  ⚠️
```

---

## Big O nas Coleções Java

### ArrayList vs LinkedList

| Operação | ArrayList | LinkedList | Por quê? |
|----------|-----------|------------|----------|
| `get(i)` | **O(1)** | O(n) | Array vai direto pelo índice; LinkedList percorre nó a nó |
| `add(final)` | **O(1)** | **O(1)** | Ambos adicionam direto no final |
| `add(início)` | O(n) | **O(1)** | ArrayList empurra todos; LinkedList reconecta ponteiros |
| `add(meio)` | O(n) | **O(1)*** | ArrayList empurra metade; LinkedList reconecta ponteiros |
| `remove(início)` | O(n) | **O(1)** | ArrayList puxa todos; LinkedList reconecta ponteiros |
| `contains()` | O(n) | O(n) | Ambos precisam percorrer para procurar |

*\*O(1) para a inserção em si, mas O(n) para chegar até a posição.*

### HashMap vs TreeMap

| Operação | HashMap | TreeMap | Por quê? |
|----------|---------|---------|----------|
| `get(k)` | **O(1)** | O(log n) | Hash vai direto; Tree percorre árvore binária |
| `put(k, v)` | **O(1)** | O(log n) | Mesma razão |
| `containsKey(k)` | **O(1)** | O(log n) | Mesma razão |
| Ordenado? | Não | **Sim** | TreeMap mantém chaves ordenadas |

---

## Regras Práticas

1. **O(1) > O(log n) > O(n) > O(n log n) > O(n²)** — da esquerda (melhor) pra direita (pior)
2. **Big O ignora constantes** — O(2n) é simplificado para O(n)
3. **Big O pega o pior caso** — O(n) significa que no pior cenário, percorre todos
4. **Loops aninhados multiplicam** — loop O(n) dentro de loop O(n) = O(n²)
5. **Operações sequenciais somam** — O(n) + O(n) = O(2n) = O(n)

---

## Quando Usar Cada Um?

```
┌─────────────────────────────────────────────────────────┐
│ Precisa de acesso direto por índice/chave?              │
│   SIM → ArrayList (índice) ou HashMap (chave) → O(1)   │
│   NÃO ↓                                                │
├─────────────────────────────────────────────────────────┤
│ Precisa de dados ordenados?                             │
│   SIM → TreeMap/TreeSet → O(log n) por operação         │
│   NÃO ↓                                                │
├─────────────────────────────────────────────────────────┤
│ Muitas inserções/remoções no início?                    │
│   SIM → LinkedList → O(1) para inserir/remover          │
│   NÃO → ArrayList (padrão)                              │
└─────────────────────────────────────────────────────────┘
```
