# Listas em Java

Listas são coleções ordenadas que permitem elementos duplicados. Todas implementam a interface `List<E>`.

## Resumo Rápido

| Lista | Quando Usar | Performance |
|-------|-------------|-------------|
| `ArrayList` | Acesso por índice frequente, mais leituras | Leitura: O(1), Inserção/Remoção: O(n) |
| `LinkedList` | Muitas inserções/remoções no início/meio | Leitura: O(n), Inserção/Remoção: O(1) |
| `Vector` | **Legado** - prefira ArrayList | Thread-safe, mas lento |
| `Stack` | Pilha (LIFO) - prefira `Deque` | push/pop: O(1) |

---

## 1. ArrayList (Mais Usado)

Array dinâmico. **Use quando**: leituras frequentes, poucas inserções no meio.

```java
import java.util.ArrayList;

ArrayList<String> nomes = new ArrayList<>();

// Adicionar
nomes.add("Ana");              // [Ana]
nomes.add("Bruno");            // [Ana, Bruno]
nomes.add(0, "Carlos");        // [Carlos, Ana, Bruno]

// Acessar
String primeiro = nomes.get(0);     // "Carlos"
int tamanho = nomes.size();         // 3

// Modificar
nomes.set(1, "Amanda");             // [Carlos, Amanda, Bruno]

// Remover
nomes.remove(0);                    // [Amanda, Bruno]
nomes.remove("Bruno");              // [Amanda]

// Verificar
boolean existe = nomes.contains("Amanda");  // true
boolean vazia = nomes.isEmpty();            // false

// Iterar
for (String nome : nomes) {
    System.out.println(nome);
}

// Limpar
nomes.clear();
```

---

## 2. LinkedList

Lista duplamente encadeada. **Use quando**: muitas inserções/remoções no início ou meio.

```java
import java.util.LinkedList;

LinkedList<Integer> numeros = new LinkedList<>();

// Mesmo métodos do ArrayList, mais:
numeros.addFirst(1);    // Adiciona no início
numeros.addLast(2);     // Adiciona no final
numeros.getFirst();     // Pega primeiro
numeros.getLast();      // Pega último
numeros.removeFirst();  // Remove primeiro
numeros.removeLast();   // Remove último
```

**Também funciona como Fila (Queue) e Pilha (Deque):**
```java
numeros.offer(10);      // Adiciona no final (fila)
numeros.poll();         // Remove do início (fila)
numeros.peek();         // Vê primeiro sem remover

numeros.push(20);       // Adiciona no início (pilha)
numeros.pop();          // Remove do início (pilha)
```

---

## 3. Vector (Legado)

**Evite usar.** É thread-safe mas lento. Prefira `ArrayList` com `Collections.synchronizedList()`.

```java
import java.util.Vector;

Vector<String> vetor = new Vector<>();
vetor.add("item");  // Mesmos métodos do ArrayList
```

---

## 4. Stack (Pilha)

**Prefira `Deque`** (mais moderno). Stack é LIFO (Last In, First Out).

```java
import java.util.Stack;

Stack<String> pilha = new Stack<>();
pilha.push("A");        // Empilha
pilha.push("B");
String topo = pilha.pop();      // Remove e retorna "B"
String ver = pilha.peek();      // Vê "A" sem remover
boolean vazia = pilha.empty();  // false
```

**Alternativa moderna com Deque:**
```java
import java.util.ArrayDeque;
import java.util.Deque;

Deque<String> pilha = new ArrayDeque<>();
pilha.push("A");
pilha.pop();
pilha.peek();
```

---

## Métodos Comuns (Todos os tipos)

| Método | Descrição |
|--------|-----------|
| `add(elemento)` | Adiciona no final |
| `add(indice, elemento)` | Adiciona na posição |
| `get(indice)` | Retorna elemento |
| `set(indice, elemento)` | Substitui elemento |
| `remove(indice)` | Remove por posição |
| `remove(objeto)` | Remove por valor |
| `size()` | Tamanho da lista |
| `isEmpty()` | Verifica se vazia |
| `contains(elemento)` | Verifica se existe |
| `indexOf(elemento)` | Índice do elemento (-1 se não existe) |
| `clear()` | Remove todos |

---

## Criação Rápida

```java
import java.util.List;
import java.util.Arrays;

// Lista imutável (não pode adicionar/remover)
List<String> fixa = List.of("A", "B", "C");

// Lista a partir de array
List<String> deArray = Arrays.asList("X", "Y", "Z");

// ArrayList a partir de outra lista
ArrayList<String> copia = new ArrayList<>(fixa);
```

---

## Quando Usar Cada Um?

```
┌─────────────────────────────────────────────────────────┐
│ Precisa de acesso rápido por índice?                    │
│   SIM → ArrayList                                       │
│   NÃO ↓                                                 │
├─────────────────────────────────────────────────────────┤
│ Muitas inserções/remoções no início ou meio?            │
│   SIM → LinkedList                                      │
│   NÃO ↓                                                 │
├─────────────────────────────────────────────────────────┤
│ Precisa de pilha (LIFO)?                                │
│   SIM → ArrayDeque (não Stack)                          │
│   NÃO ↓                                                 │
├─────────────────────────────────────────────────────────┤
│ Precisa de fila (FIFO)?                                 │
│   SIM → LinkedList ou ArrayDeque                        │
│   NÃO → ArrayList (padrão)                              │
└─────────────────────────────────────────────────────────┘
```

---

## Dica de Ouro

Declare com a interface, instancie com a implementação:

```java
// ✅ Bom - flexível
List<String> lista = new ArrayList<>();

// ❌ Evite - menos flexível
ArrayList<String> lista = new ArrayList<>();
```

Isso permite trocar a implementação facilmente sem mudar o resto do código.
