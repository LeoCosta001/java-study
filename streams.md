# Streams em Java

Streams são uma API introduzida no Java 8 que permite processar coleções de dados de forma **declarativa** e **funcional**. Se você já conhece TypeScript/JavaScript, Streams são equivalentes aos métodos de array como `.map()`, `.filter()`, `.reduce()`.

## Índice

1. [O que são Streams?](#1-o-que-são-streams)
2. [Comparação com TypeScript](#2-comparação-com-typescript)
3. [Criando Streams](#3-criando-streams)
4. [Operações Intermediárias](#4-operações-intermediárias)
5. [Operações Terminais](#5-operações-terminais)
6. [Exemplos Práticos](#6-exemplos-práticos)
7. [Collectors](#7-collectors)
8. [Diferenças Importantes](#8-diferenças-importantes)

---

## 1. O que são Streams?

Stream é um **pipeline de operações** para processar sequências de elementos. Características principais:

- **Declarativo**: você descreve *o que* quer fazer, não *como* fazer
- **Encadeável**: operações podem ser conectadas em cadeia
- **Lazy (Preguiçoso)**: nada executa até uma operação terminal ser chamada
- **Uso único**: um Stream só pode ser consumido uma vez

```java
import java.util.List;
import java.util.stream.Collectors;

List<String> nomes = List.of("Ana", "Bruno", "Carlos", "Amanda");

List<String> nomesComA = nomes.stream()       // cria o Stream
    .filter(n -> n.startsWith("A"))           // operação intermediária
    .map(String::toUpperCase)                 // operação intermediária
    .collect(Collectors.toList());            // operação terminal

// Resultado: [ANA, AMANDA]
```

---

## 2. Comparação com TypeScript

Se você conhece TypeScript/JavaScript, a tabela abaixo mostra as equivalências:

| Operação | TypeScript/JavaScript | Java Stream |
|----------|----------------------|-------------|
| Transformar | `.map()` | `.map()` |
| Filtrar | `.filter()` | `.filter()` |
| Reduzir | `.reduce()` | `.reduce()` |
| Encontrar primeiro | `.find()` | `.findFirst()` |
| Verificar se algum | `.some()` | `.anyMatch()` |
| Verificar se todos | `.every()` | `.allMatch()` |
| Verificar se nenhum | `!.some()` | `.noneMatch()` |
| Ordenar | `.sort()` | `.sorted()` |
| Pegar N primeiros | `.slice(0, n)` | `.limit(n)` |
| Pular N primeiros | `.slice(n)` | `.skip(n)` |
| Para cada | `.forEach()` | `.forEach()` |
| Achatar | `.flat()` | `.flatMap()` |
| Contar | `.length` | `.count()` |

### Exemplo Comparativo

**TypeScript:**
```typescript
const numeros = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

const resultado = numeros
    .filter(n => n % 2 === 0)      // pega pares
    .map(n => n * 2)               // multiplica por 2
    .reduce((acc, n) => acc + n, 0); // soma tudo

console.log(resultado); // 60
```

**Java:**
```java
List<Integer> numeros = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

int resultado = numeros.stream()
    .filter(n -> n % 2 == 0)       // pega pares
    .map(n -> n * 2)               // multiplica por 2
    .reduce(0, (acc, n) -> acc + n); // soma tudo

System.out.println(resultado); // 60
```

---

## 3. Criando Streams

### A partir de coleções
```java
List<String> lista = List.of("A", "B", "C");
lista.stream();  // Stream<String>

Set<Integer> conjunto = Set.of(1, 2, 3);
conjunto.stream();  // Stream<Integer>
```

### A partir de arrays
```java
String[] array = {"A", "B", "C"};
Arrays.stream(array);  // Stream<String>
```

### Diretamente com Stream.of()
```java
Stream<String> stream = Stream.of("A", "B", "C");
```

### Stream de números (IntStream, LongStream, DoubleStream)
```java
IntStream.range(1, 5);      // 1, 2, 3, 4
IntStream.rangeClosed(1, 5); // 1, 2, 3, 4, 5
IntStream.of(1, 2, 3);       // 1, 2, 3
```

---

## 4. Operações Intermediárias

Operações intermediárias retornam um novo Stream e são **lazy** (não executam até uma operação terminal).

### filter() - Filtrar elementos
```java
// TypeScript: numeros.filter(n => n > 5)
numeros.stream()
    .filter(n -> n > 5);
```

### map() - Transformar elementos
```java
// TypeScript: nomes.map(n => n.toUpperCase())
nomes.stream()
    .map(n -> n.toUpperCase());

// Com method reference
nomes.stream()
    .map(String::toUpperCase);
```

### sorted() - Ordenar
```java
// TypeScript: numeros.sort((a, b) => a - b)
numeros.stream()
    .sorted();  // ordem natural

numeros.stream()
    .sorted((a, b) -> b - a);  // ordem decrescente

// Ordenar objetos por propriedade
filmes.stream()
    .sorted(Comparator.comparing(Filme::getNota));

// Ordem decrescente
filmes.stream()
    .sorted(Comparator.comparing(Filme::getNota).reversed());
```

### distinct() - Remover duplicados
```java
// TypeScript: [...new Set(numeros)]
numeros.stream()
    .distinct();
```

### limit() e skip() - Paginação
```java
// TypeScript: numeros.slice(0, 5)
numeros.stream()
    .limit(5);  // pega os 5 primeiros

// TypeScript: numeros.slice(3)
numeros.stream()
    .skip(3);   // pula os 3 primeiros

// Combinados: pega elementos 4, 5, 6 (índices 3, 4, 5)
numeros.stream()
    .skip(3)
    .limit(3);
```

### flatMap() - Achatar coleções aninhadas
```java
// TypeScript: arrays.flat()
List<List<Integer>> listas = List.of(
    List.of(1, 2),
    List.of(3, 4),
    List.of(5, 6)
);

listas.stream()
    .flatMap(lista -> lista.stream());
// Resultado: Stream de 1, 2, 3, 4, 5, 6
```

### peek() - Debug (ver elementos sem modificar)
```java
numeros.stream()
    .filter(n -> n > 5)
    .peek(n -> System.out.println("Passou: " + n))
    .map(n -> n * 2)
    .collect(Collectors.toList());
```

---

## 5. Operações Terminais

Operações terminais **executam** o pipeline e retornam um resultado (não um Stream).

### collect() - Coletar em uma coleção
```java
// Para List
List<String> lista = stream.collect(Collectors.toList());
// Java 16+
List<String> lista = stream.toList();

// Para Set
Set<String> conjunto = stream.collect(Collectors.toSet());

// Para Map
Map<String, Integer> mapa = filmes.stream()
    .collect(Collectors.toMap(
        Filme::getTitulo,    // chave
        Filme::getNota       // valor
    ));
```

### forEach() - Executar ação em cada elemento
```java
// TypeScript: numeros.forEach(n => console.log(n))
numeros.stream()
    .forEach(n -> System.out.println(n));

// Com method reference
numeros.forEach(System.out::println);
```

### reduce() - Reduzir a um único valor
```java
// TypeScript: numeros.reduce((acc, n) => acc + n, 0)
int soma = numeros.stream()
    .reduce(0, (acc, n) -> acc + n);

// Ou usando Integer::sum
int soma = numeros.stream()
    .reduce(0, Integer::sum);
```

### count() - Contar elementos
```java
// TypeScript: numeros.filter(...).length
long quantidade = numeros.stream()
    .filter(n -> n > 5)
    .count();
```

### findFirst() e findAny() - Encontrar elemento
```java
// TypeScript: numeros.find(n => n > 5)
Optional<Integer> primeiro = numeros.stream()
    .filter(n -> n > 5)
    .findFirst();

// Usar o valor
primeiro.ifPresent(n -> System.out.println(n));  // se existir
int valor = primeiro.orElse(0);                   // ou valor padrão
```

### anyMatch(), allMatch(), noneMatch() - Verificações
```java
// TypeScript: numeros.some(n => n > 5)
boolean algumMaior = numeros.stream().anyMatch(n -> n > 5);

// TypeScript: numeros.every(n => n > 0)
boolean todosMaiores = numeros.stream().allMatch(n -> n > 0);

// TypeScript: !numeros.some(n => n < 0)
boolean nenhumNegativo = numeros.stream().noneMatch(n -> n < 0);
```

### min() e max() - Encontrar extremos
```java
Optional<Integer> minimo = numeros.stream().min(Integer::compareTo);
Optional<Integer> maximo = numeros.stream().max(Integer::compareTo);

// Com objetos
Optional<Filme> melhorFilme = filmes.stream()
    .max(Comparator.comparing(Filme::getNota));
```

---

## 6. Exemplos Práticos

### Exemplo 1: Processar lista de filmes

**TypeScript:**
```typescript
interface Filme {
    titulo: string;
    nota: number;
    ano: number;
}

const filmes: Filme[] = [...];

const melhoresFilmes = filmes
    .filter(f => f.nota > 8)
    .sort((a, b) => b.nota - a.nota)
    .slice(0, 5)
    .map(f => f.titulo);
```

**Java:**
```java
List<String> melhoresFilmes = filmes.stream()
    .filter(f -> f.getNota() > 8)
    .sorted(Comparator.comparing(Filme::getNota).reversed())
    .limit(5)
    .map(Filme::getTitulo)
    .toList();
```

### Exemplo 2: Agrupar por categoria

**TypeScript:**
```typescript
const porCategoria = filmes.reduce((acc, filme) => {
    const cat = filme.categoria;
    acc[cat] = acc[cat] || [];
    acc[cat].push(filme);
    return acc;
}, {} as Record<string, Filme[]>);
```

**Java:**
```java
Map<String, List<Filme>> porCategoria = filmes.stream()
    .collect(Collectors.groupingBy(Filme::getCategoria));
```

### Exemplo 3: Estatísticas

```java
// Média das notas
double media = filmes.stream()
    .mapToDouble(Filme::getNota)
    .average()
    .orElse(0);

// Soma, min, max, média de uma vez
IntSummaryStatistics stats = numeros.stream()
    .mapToInt(Integer::intValue)
    .summaryStatistics();

stats.getSum();
stats.getAverage();
stats.getMin();
stats.getMax();
stats.getCount();
```

### Exemplo 4: Concatenar strings

**TypeScript:**
```typescript
const nomes = ["Ana", "Bruno", "Carlos"];
const resultado = nomes.join(", "); // "Ana, Bruno, Carlos"
```

**Java:**
```java
String resultado = nomes.stream()
    .collect(Collectors.joining(", ")); // "Ana, Bruno, Carlos"
```

---

## 7. Collectors

A classe `Collectors` oferece vários coletores úteis:

```java
import java.util.stream.Collectors;

// toList() - para lista
.collect(Collectors.toList())

// toSet() - para conjunto (sem duplicados)
.collect(Collectors.toSet())

// toMap() - para mapa
.collect(Collectors.toMap(keyMapper, valueMapper))

// joining() - concatenar strings
.collect(Collectors.joining(", "))

// groupingBy() - agrupar
.collect(Collectors.groupingBy(Filme::getCategoria))

// partitioningBy() - dividir em dois grupos (true/false)
.collect(Collectors.partitioningBy(f -> f.getNota() > 8))

// counting() - contar em grupos
.collect(Collectors.groupingBy(Filme::getCategoria, Collectors.counting()))

// summarizingInt/Double() - estatísticas
.collect(Collectors.summarizingDouble(Filme::getNota))

// averagingDouble() - média
.collect(Collectors.averagingDouble(Filme::getNota))
```

---

## 8. Diferenças Importantes

### Stream vs Array Methods (JS/TS)

| Aspecto | Java Stream | TypeScript Array |
|---------|-------------|------------------|
| Criação | Precisa chamar `.stream()` | Métodos já disponíveis no array |
| Execução | Lazy (só executa no terminal) | Eager (executa imediatamente) |
| Reutilização | Uso único | Pode iterar múltiplas vezes |
| Coleta | Precisa de `.collect()` ou `.toList()` | Retorna array automaticamente |
| Performance | Pode usar `.parallelStream()` | Single-threaded |

### Exemplo de Lazy Evaluation

```java
// NADA acontece aqui - só monta o pipeline
Stream<Integer> stream = numeros.stream()
    .filter(n -> {
        System.out.println("Filtrando: " + n);
        return n > 5;
    })
    .map(n -> n * 2);

// SÓ AQUI executa tudo
List<Integer> resultado = stream.collect(Collectors.toList());
```

### Parallel Streams

```java
// Processamento paralelo (múltiplas threads)
List<Integer> resultado = numeros.parallelStream()
    .filter(n -> n > 5)
    .map(n -> n * 2)
    .toList();
```

---

## Resumo Rápido

```java
// Padrão básico
colecao.stream()
    .operacoesIntermediarias()  // filter, map, sorted, etc
    .operacaoTerminal();         // collect, forEach, reduce, etc

// Exemplo completo
List<String> resultado = nomes.stream()
    .filter(n -> n.length() > 3)     // filtrar
    .map(String::toUpperCase)         // transformar
    .sorted()                         // ordenar
    .limit(5)                         // limitar
    .toList();                        // coletar
```

**Lembre-se:**
1. Chamar `.stream()` para começar
2. Encadear operações intermediárias
3. Finalizar com operação terminal
4. Stream só pode ser usado uma vez
