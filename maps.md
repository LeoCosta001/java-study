# Map e HashMap em Java

Maps são coleções de pares **chave-valor**. Cada chave é única e mapeia para um valor.

## Resumo Rápido

| Map | Quando Usar | Características |
|-----|-------------|-----------------|
| `HashMap` | Caso geral, mais usado | Rápido, sem ordem garantida |
| `LinkedHashMap` | Manter ordem de inserção | Ordem de inserção preservada |
| `TreeMap` | Chaves ordenadas | Ordenado por chave, mais lento |
| `Hashtable` | **Legado** - evite | Thread-safe, mas lento |

---

## 1. HashMap (Mais Usado)

**Use quando**: precisa de mapeamento chave-valor rápido, ordem não importa.

```java
import java.util.HashMap;
import java.util.Map;

Map<String, Integer> idade = new HashMap<>();

// Adicionar
idade.put("Ana", 25);
idade.put("Bruno", 30);
idade.put("Carlos", 22);

// Acessar
int idadeAna = idade.get("Ana");           // 25
int idadeOuPadrao = idade.getOrDefault("Zé", 0);  // 0 (não existe)

// Verificar
boolean existe = idade.containsKey("Ana");        // true
boolean temValor = idade.containsValue(30);       // true

// Modificar (put sobrescreve)
idade.put("Ana", 26);                      // Ana agora tem 26

// Remover
idade.remove("Carlos");                    // Remove Carlos

// Tamanho
int total = idade.size();                  // 2
```

### Iterando

```java
// Por chaves
for (String nome : idade.keySet()) {
    System.out.println(nome);
}

// Por valores
for (Integer valor : idade.values()) {
    System.out.println(valor);
}

// Por pares (mais comum)
for (Map.Entry<String, Integer> entry : idade.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}

// Com forEach (Java 8+)
idade.forEach((nome, anos) -> System.out.println(nome + ": " + anos));
```

---

## 2. LinkedHashMap

**Use quando**: precisa manter a ordem de inserção.

```java
import java.util.LinkedHashMap;
import java.util.Map;

Map<String, String> config = new LinkedHashMap<>();
config.put("host", "localhost");
config.put("port", "8080");
config.put("timeout", "30");

// Itera na ordem: host → port → timeout
```

---

## 3. TreeMap

**Use quando**: precisa das chaves ordenadas automaticamente.

```java
import java.util.TreeMap;
import java.util.Map;

Map<String, Integer> ranking = new TreeMap<>();
ranking.put("Carlos", 100);
ranking.put("Ana", 200);
ranking.put("Bruno", 150);

// Itera em ordem alfabética: Ana → Bruno → Carlos

// Métodos extras
TreeMap<String, Integer> tree = new TreeMap<>();
tree.firstKey();     // Primeira chave
tree.lastKey();      // Última chave
tree.higherKey("B"); // Próxima chave maior que "B"
tree.lowerKey("B");  // Chave anterior a "B"
```

---

## Métodos Comuns (Todos os Maps)

| Método | Descrição |
|--------|-----------|
| `put(chave, valor)` | Adiciona ou atualiza |
| `get(chave)` | Retorna valor (ou null) |
| `getOrDefault(chave, padrão)` | Retorna valor ou padrão |
| `remove(chave)` | Remove entrada |
| `containsKey(chave)` | Verifica se chave existe |
| `containsValue(valor)` | Verifica se valor existe |
| `size()` | Quantidade de entradas |
| `isEmpty()` | Verifica se vazio |
| `clear()` | Remove tudo |
| `keySet()` | Conjunto de chaves |
| `values()` | Coleção de valores |
| `entrySet()` | Conjunto de pares |

---

## Métodos Úteis (Java 8+)

```java
Map<String, Integer> mapa = new HashMap<>();

// putIfAbsent - só adiciona se chave não existe
mapa.putIfAbsent("novo", 100);

// computeIfAbsent - computa valor se chave não existe
mapa.computeIfAbsent("contador", k -> 0);

// merge - combina valores
mapa.put("pontos", 10);
mapa.merge("pontos", 5, Integer::sum);  // pontos = 15

// replace - substitui apenas se existe
mapa.replace("pontos", 20);

// replaceAll - aplica função em todos
mapa.replaceAll((k, v) -> v * 2);
```

---

## Criação Rápida

```java
import java.util.Map;

// Map imutável (Java 9+)
Map<String, Integer> fixo = Map.of(
    "um", 1,
    "dois", 2,
    "três", 3
);

// Map.ofEntries para mais de 10 pares
Map<String, Integer> grande = Map.ofEntries(
    Map.entry("a", 1),
    Map.entry("b", 2)
);
```

---

## Quando Usar Cada Um?

```
┌─────────────────────────────────────────────────────────┐
│ Precisa de chaves ordenadas?                            │
│   SIM → TreeMap                                         │
│   NÃO ↓                                                 │
├─────────────────────────────────────────────────────────┤
│ Precisa manter ordem de inserção?                       │
│   SIM → LinkedHashMap                                   │
│   NÃO ↓                                                 │
├─────────────────────────────────────────────────────────┤
│ Apenas mapeamento rápido chave-valor?                   │
│   SIM → HashMap (padrão)                                │
└─────────────────────────────────────────────────────────┘
```

---

## Cuidados Importantes

### 1. Chaves null
```java
HashMap<String, String> hm = new HashMap<>();
hm.put(null, "valor");   // ✅ HashMap aceita 1 chave null

TreeMap<String, String> tm = new TreeMap<>();
tm.put(null, "valor");   // ❌ TreeMap NÃO aceita null (NullPointerException)
```

### 2. Chaves devem ter hashCode() e equals()
```java
// Para usar objetos como chave, implemente:
@Override
public int hashCode() { ... }

@Override
public boolean equals(Object o) { ... }
```

### 3. Valores null são permitidos
```java
mapa.put("chave", null);  // ✅ OK em HashMap e LinkedHashMap
```

---

## Dica de Ouro

Declare com a interface `Map`, instancie com a implementação:

```java
// ✅ Bom - flexível
Map<String, Integer> mapa = new HashMap<>();

// ❌ Evite - menos flexível
HashMap<String, Integer> mapa = new HashMap<>();
```

---

## Comparação: Map vs List

| Característica | Map | List |
|----------------|-----|------|
| Estrutura | Chave → Valor | Índice → Valor |
| Acesso | Por chave | Por índice (0, 1, 2...) |
| Duplicatas | Chaves únicas | Permite duplicatas |
| Uso | Dicionário, cache | Sequência ordenada |
