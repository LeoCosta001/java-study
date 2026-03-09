# Lambdas em Java

Lambdas são **funções anônimas** introduzidas no Java 8. Se você conhece TypeScript/JavaScript, lambdas são equivalentes às **arrow functions** (`=>`).

## Índice

1. [O que são Lambdas?](#1-o-que-são-lambdas)
2. [Comparação com TypeScript](#2-comparação-com-typescript)
3. [Sintaxe](#3-sintaxe)
4. [Interfaces Funcionais](#4-interfaces-funcionais)
5. [Method Reference](#5-method-reference)
6. [Uso com Streams](#6-uso-com-streams)
7. [Exemplos Práticos](#7-exemplos-práticos)

---

## 1. O que são Lambdas?

Lambda é uma forma concisa de representar uma função que pode ser passada como argumento. Em vez de criar uma classe anônima completa, você escreve apenas a lógica.

**Antes do Java 8 (classe anônima):**
```java
Collections.sort(nomes, new Comparator<String>() {
    @Override
    public int compare(String a, String b) {
        return a.compareTo(b);
    }
});
```

**Com Lambda (Java 8+):**
```java
Collections.sort(nomes, (a, b) -> a.compareTo(b));
```

---

## 2. Comparação com TypeScript

O operador `->` em Java é equivalente ao `=>` em TypeScript/JavaScript:

| TypeScript/JavaScript | Java |
|----------------------|------|
| `=>` (arrow function) | `->` (lambda) |
| `(param) => expressão` | `(param) -> expressão` |
| `(param) => { bloco }` | `(param) -> { bloco }` |

### Exemplos Lado a Lado

**Função simples:**
```typescript
// TypeScript
const dobrar = (n: number): number => n * 2;
```

```java
// Java
Function<Integer, Integer> dobrar = n -> n * 2;
```

**Múltiplos parâmetros:**
```typescript
// TypeScript
const somar = (a: number, b: number): number => a + b;
```

```java
// Java
BiFunction<Integer, Integer, Integer> somar = (a, b) -> a + b;
```

**Com bloco de código:**
```typescript
// TypeScript
const processar = (n: number): number => {
    const resultado = n * 2;
    console.log(resultado);
    return resultado;
};
```

```java
// Java
Function<Integer, Integer> processar = n -> {
    int resultado = n * 2;
    System.out.println(resultado);
    return resultado;
};
```

---

## 3. Sintaxe

### Formas de escrever lambdas

```java
// 1. Expressão simples (sem parênteses quando só tem 1 parâmetro)
n -> n * 2

// 2. Com parênteses (obrigatório com 0 ou múltiplos parâmetros)
() -> System.out.println("Olá")
(a, b) -> a + b

// 3. Com tipo explícito (opcional)
(Integer n) -> n * 2
(String a, String b) -> a.compareTo(b)

// 4. Com bloco de código (precisa de return)
n -> {
    int resultado = n * 2;
    return resultado;
}

// 5. Sem retorno (void)
n -> System.out.println(n)
```

### Regras de sintaxe

| Situação | Sintaxe |
|----------|---------|
| Nenhum parâmetro | `() -> expressão` |
| Um parâmetro | `n -> expressão` ou `(n) -> expressão` |
| Múltiplos parâmetros | `(a, b) -> expressão` |
| Com tipos explícitos | `(Integer a, Integer b) -> expressão` |
| Bloco de código | `(params) -> { instruções; return valor; }` |

---

## 4. Interfaces Funcionais

Lambdas só funcionam onde se espera uma **interface funcional** - uma interface com apenas **um método abstrato**.

### Interfaces funcionais mais usadas

| Interface | Entrada | Saída | Equivalente TS | Uso comum |
|-----------|---------|-------|----------------|-----------|
| `Consumer<T>` | T | void | `(t: T) => void` | forEach |
| `Supplier<T>` | nada | T | `() => T` | lazy loading |
| `Function<T, R>` | T | R | `(t: T) => R` | map |
| `Predicate<T>` | T | boolean | `(t: T) => boolean` | filter |
| `BiFunction<T, U, R>` | T, U | R | `(t: T, u: U) => R` | reduce |
| `BiConsumer<T, U>` | T, U | void | `(t: T, u: U) => void` | forEach com 2 args |
| `Comparator<T>` | T, T | int | `(a: T, b: T) => number` | sort |
| `Runnable` | nada | void | `() => void` | threads |

### Exemplos de uso

```java
import java.util.function.*;

// Predicate - retorna boolean (usado no filter)
Predicate<Integer> ehPar = n -> n % 2 == 0;
boolean resultado = ehPar.test(4);  // true

// Consumer - não retorna nada (usado no forEach)
Consumer<String> imprimir = s -> System.out.println(s);
imprimir.accept("Olá");  // imprime "Olá"

// Function - transforma valor (usado no map)
Function<String, Integer> tamanho = s -> s.length();
int tam = tamanho.apply("Java");  // 4

// Supplier - fornece valor sem entrada
Supplier<Double> aleatorio = () -> Math.random();
double valor = aleatorio.get();

// BiFunction - dois parâmetros
BiFunction<Integer, Integer, Integer> somar = (a, b) -> a + b;
int soma = somar.apply(5, 3);  // 8

// Comparator - para ordenação
Comparator<String> porTamanho = (a, b) -> a.length() - b.length();
```

### Criando sua própria interface funcional

```java
@FunctionalInterface  // Anotação opcional, mas recomendada
interface Calculadora {
    int calcular(int a, int b);
}

// Uso
Calculadora soma = (a, b) -> a + b;
Calculadora mult = (a, b) -> a * b;

System.out.println(soma.calcular(5, 3));  // 8
System.out.println(mult.calcular(5, 3));  // 15
```

---

## 5. Method Reference

Method Reference (`::`) é um atalho para lambdas quando a lambda apenas chama um método existente.

### Tipos de Method Reference

| Tipo | Lambda | Method Reference |
|------|--------|------------------|
| Método estático | `n -> Math.abs(n)` | `Math::abs` |
| Método de instância (objeto) | `s -> System.out.println(s)` | `System.out::println` |
| Método de instância (tipo) | `s -> s.toUpperCase()` | `String::toUpperCase` |
| Construtor | `() -> new ArrayList<>()` | `ArrayList::new` |

### Exemplos

```java
List<String> nomes = List.of("ana", "bruno", "carlos");

// Lambda vs Method Reference

// Método de instância do tipo
nomes.stream()
    .map(s -> s.toUpperCase())    // lambda
    .map(String::toUpperCase);     // method reference

// Método estático
numeros.stream()
    .map(n -> Math.abs(n))         // lambda
    .map(Math::abs);               // method reference

// Método de instância de um objeto específico
nomes.stream()
    .forEach(s -> System.out.println(s))  // lambda
    .forEach(System.out::println);         // method reference

// Construtor
nomes.stream()
    .map(s -> new StringBuilder(s))    // lambda
    .map(StringBuilder::new);           // method reference

// Com getter de objeto
filmes.stream()
    .map(f -> f.getTitulo())      // lambda
    .map(Filme::getTitulo);        // method reference
```

### Quando usar Method Reference

**Use quando:**
- A lambda apenas chama um único método
- Os parâmetros da lambda são passados diretamente ao método
- Melhora a legibilidade

**Não use quando:**
- Precisa de lógica adicional
- Precisa manipular os parâmetros antes de passar

```java
// ✅ Bom uso de method reference
.map(String::toUpperCase)
.filter(Objects::nonNull)
.forEach(System.out::println)

// ❌ Não dá para usar method reference (lógica adicional)
.map(s -> s.toUpperCase() + "!")
.filter(n -> n > 5 && n < 10)
```

---

## 6. Uso com Streams

O uso mais comum de lambdas é com a API de Streams:

```java
List<String> nomes = List.of("Ana", "Bruno", "Carlos", "Amanda", "Daniel");

// filter - Predicate<T>
nomes.stream()
    .filter(n -> n.startsWith("A"));

// map - Function<T, R>
nomes.stream()
    .map(n -> n.toUpperCase());

// sorted - Comparator<T>
nomes.stream()
    .sorted((a, b) -> a.length() - b.length());

// forEach - Consumer<T>
nomes.stream()
    .forEach(n -> System.out.println(n));

// reduce - BinaryOperator<T> (ou BiFunction)
nomes.stream()
    .reduce("", (acc, n) -> acc + n + ", ");

// anyMatch/allMatch - Predicate<T>
boolean temAna = nomes.stream()
    .anyMatch(n -> n.equals("Ana"));
```

### Combinando com Comparator

```java
List<Filme> filmes = // ...

// Ordenar por nota (crescente)
filmes.stream()
    .sorted((a, b) -> Double.compare(a.getNota(), b.getNota()));

// Usando Comparator.comparing (mais legível)
filmes.stream()
    .sorted(Comparator.comparing(f -> f.getNota()));

// Com method reference
filmes.stream()
    .sorted(Comparator.comparing(Filme::getNota));

// Decrescente
filmes.stream()
    .sorted(Comparator.comparing(Filme::getNota).reversed());

// Múltiplos critérios
filmes.stream()
    .sorted(Comparator
        .comparing(Filme::getAno)
        .thenComparing(Filme::getNota)
        .reversed());
```

---

## 7. Exemplos Práticos

### Exemplo 1: Lista de tarefas

**TypeScript:**
```typescript
interface Tarefa {
    descricao: string;
    concluida: boolean;
}

const tarefas: Tarefa[] = [...];

// Filtrar não concluídas
const pendentes = tarefas.filter(t => !t.concluida);

// Marcar todas como concluídas
tarefas.forEach(t => t.concluida = true);
```

**Java:**
```java
List<Tarefa> tarefas = // ...

// Filtrar não concluídas
List<Tarefa> pendentes = tarefas.stream()
    .filter(t -> !t.isConcluida())
    .toList();

// Marcar todas como concluídas
tarefas.forEach(t -> t.setConcluida(true));
```

### Exemplo 2: Validações

```java
// Criar validadores reutilizáveis
Predicate<String> naoVazio = s -> s != null && !s.isEmpty();
Predicate<String> tamanhoMinimo = s -> s.length() >= 3;
Predicate<String> apenasLetras = s -> s.matches("[a-zA-Z]+");

// Combinar validadores
Predicate<String> nomeValido = naoVazio
    .and(tamanhoMinimo)
    .and(apenasLetras);

// Usar
boolean valido = nomeValido.test("João");  // true
boolean invalido = nomeValido.test("J1");   // false
```

### Exemplo 3: Transformações encadeadas

```java
Function<String, String> trim = String::trim;
Function<String, String> upper = String::toUpperCase;
Function<String, String> addPrefix = s -> "Sr(a). " + s;

// Combinar funções
Function<String, String> formatarNome = trim
    .andThen(upper)
    .andThen(addPrefix);

String resultado = formatarNome.apply("  joão  ");
// "Sr(a). JOÃO"
```

### Exemplo 4: Event handlers (similar a JS)

```java
// Em TypeScript/JavaScript
button.addEventListener('click', (e) => console.log('Clicado!'));

// Em Java (Swing/JavaFX)
button.setOnAction(e -> System.out.println("Clicado!"));

// Ou com method reference
button.setOnAction(this::handleClick);

private void handleClick(ActionEvent e) {
    System.out.println("Clicado!");
}
```

---

## Resumo

| Conceito | TypeScript | Java |
|----------|-----------|------|
| Sintaxe básica | `=>` | `->` |
| Parâmetro único | `n => n * 2` | `n -> n * 2` |
| Múltiplos parâmetros | `(a, b) => a + b` | `(a, b) -> a + b` |
| Sem parâmetros | `() => valor` | `() -> valor` |
| Com bloco | `() => { return x; }` | `() -> { return x; }` |
| Method reference | não existe | `Classe::metodo` |

### Dicas

1. **Prefira expressões simples**: `n -> n * 2` é melhor que `n -> { return n * 2; }`
2. **Use method reference quando possível**: `String::toUpperCase` é mais limpo que `s -> s.toUpperCase()`
3. **Nomeie lambdas complexas**: Se a lambda é complicada, extraia para um método e use method reference
4. **Lambdas capturam variáveis**: Variáveis externas usadas em lambdas devem ser efetivamente final

```java
// ❌ Erro - variável não é final
int contador = 0;
lista.forEach(item -> contador++);

// ✅ OK - usando AtomicInteger
AtomicInteger contador = new AtomicInteger(0);
lista.forEach(item -> contador.incrementAndGet());
```
