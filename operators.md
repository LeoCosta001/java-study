# Operadores em Java

No Java temos diversos tipos de operadores para lidar com os dados que estamos trabalhando em nossa aplicação. Este documento detalha os principais operadores da linguagem.

## Índice

1. [Operadores de Atribuição](#1-operadores-de-atribuição)
   - [Operadores de Atribuição Combinados](#operadores-de-atribuição-combinados)
2. [Operadores Aritméticos](#2-operadores-aritméticos)
3. [Operadores Relacionais](#3-operadores-relacionais)
4. [Operadores Lógicos](#4-operadores-lógicos)
   - [Operador AND (&&)](#operador-and-)
   - [Operador OR (||)](#operador-or-)
   - [Operador NOT (!)](#operador-not-)
5. [Operadores de Incremento e Decremento](#5-operadores-de-incremento-e-decremento)
   - [Operador de Pré-incremento (++variavel)](#operador-de-pré-incremento-variavel)
   - [Operador de Pós-incremento (variavel++)](#operador-de-pós-incremento-variavel)
6. [Diferenças entre Operadores Java e TypeScript/Node.js](#6-diferenças-entre-operadores-java-e-typescriptnodejs)
   - [Operadores de Igualdade](#61-operadores-de-igualdade)
   - [Divisão de Números](#62-divisão-de-números)
   - [Operador de Exponenciação](#63-operador-de-exponenciação)
   - [Operador de Coalescência Nula (??)](#64-operador-de-coalescência-nula-)
   - [Optional Chaining (?.)](#65-optional-chaining-)
   - [Operador typeof](#66-operador-typeof)
   - [Operador Ternário](#67-operador-ternário)
   - [Spread Operator (...)](#68-spread-operator-)
   - [Tipagem Estática vs Dinâmica](#69-tipagem-estática-vs-dinâmica)
   - [Resumo das Diferenças](#resumo-das-diferenças)

---

## 1. Operadores de Atribuição

Os operadores de atribuição são usados para atribuir um valor a uma variável. O operador de atribuição básico é o `=` (sinal de igual).

**Exemplo:**
```java
int valor = 5; // Atribui o valor 5 à variável valor
```

### Operadores de Atribuição Combinados

Existem também operadores de atribuição combinados, que são uma forma abreviada de atribuição. Por exemplo, o operador `+=` adiciona um valor à variável existente.

**Exemplo:**
```java
int valor = 10; 
valor += 15; // Equivalente a valor = valor + 15, atribui o valor 25 à variável valor
```

---

## 2. Operadores Aritméticos

Os operadores aritméticos são usados para realizar operações matemáticas básicas:

| Operador | Operação | Descrição |
|----------|----------|-----------|
| `+` | Adição | Soma dois valores |
| `-` | Subtração | Subtrai um valor de outro |
| `*` | Multiplicação | Multiplica dois valores |
| `/` | Divisão | Divide um valor por outro |
| `%` | Módulo | Retorna o resto da divisão |

**Exemplos:**
```java
int a = 10 + 5;  // Atribui o valor 15 à variável a
int b = 10 - 5;  // Atribui o valor 5 à variável b
int c = 10 * 5;  // Atribui o valor 50 à variável c
int d = 10 / 5;  // Atribui o valor 2 à variável d
int e = 10 % 3;  // Atribui o valor 1 à variável e (o resto da divisão de 10 por 3 é 1)
```

---

## 3. Operadores Relacionais

Os operadores relacionais são usados para comparar valores. Eles retornam um valor booleano (`true` ou `false`). Estes operadores são fundamentais quando trabalhamos com condicionais.

| Operador | Descrição |
|----------|-----------|
| `==` | Igual a |
| `!=` | Diferente de |
| `>` | Maior que |
| `>=` | Maior ou igual a |
| `<` | Menor que |
| `<=` | Menor ou igual a |

**Exemplo:**
```java
int a = 10;  // Atribui o valor 10 à variável a
int b = 5;   // Atribui o valor 5 à variável b
int c = 30;  // Atribui o valor 30 à variável c

boolean igual = (b == a);      // false - o valor de b não é igual ao valor de a
boolean diferente = (b != c);  // true - o valor de b é diferente do valor de c
boolean maior = (b > a);       // false - o valor de b é menor que o valor de a
boolean menorIgual = (b <= c); // true - o valor de b é menor que o valor de c
```

---

## 4. Operadores Lógicos

Esses operadores são usados quando queremos verificar duas ou mais condições e/ou expressões na aplicação. Eles fazem a comparação de valores booleanos e retornam também um resultado booleano.

### Operadores disponíveis:
- **AND (`&&`)** - E
- **OR (`||`)** - OU
- **NOT (`!`)** - NÃO

### Operador AND (`&&`)

O operador AND é usado para verificar se duas condições são verdadeiras. Se ambas as condições forem verdadeiras, o resultado será verdadeiro. Caso contrário, o resultado será falso.

**Exemplo:**
```java
boolean a = true;
boolean b = false;
if (a && b) {
    // Este código não será executado, já que a é verdadeiro e b é falso
}
```

### Operador OR (`||`)

O operador OR é usado para verificar se pelo menos uma das condições é verdadeira. Se pelo menos uma das condições for verdadeira, o resultado será verdadeiro. Caso contrário, o resultado será falso.

**Exemplo:**
```java
boolean a = true;
boolean b = false;
if (a || b) {
    // Este código será executado, já que a é verdadeiro, mesmo que b seja falso
}
```

### Operador NOT (`!`)

O operador NOT é usado para negar uma condição. Se a condição for verdadeira, o resultado será falso. Se a condição for falsa, o resultado será verdadeiro.

**Exemplo:**
```java
boolean a = true;
if (!a) {
    // Este código não será executado, já que a é verdadeiro
}
```

---

## 5. Operadores de Incremento e Decremento

Além dos operadores citados anteriormente, os operadores de incremento e decremento são usados para aumentar ou diminuir o valor de uma variável em 1.

### Tipos de Operadores:
- **Pré-incremento**: `++variavel`
- **Pós-incremento**: `variavel++`
- **Pré-decremento**: `--variavel`
- **Pós-decremento**: `variavel--`

### Operador de Pré-incremento (`++variavel`)

Aumenta o valor da variável em 1 **antes** de usar a variável em uma expressão.

**Exemplo:**
```java
int num = 5;
int resultado = ++num; // num é incrementado para 6 e depois atribuído a resultado
System.out.println(num);       // imprime 6
System.out.println(resultado); // imprime 6
```

### Operador de Pós-incremento (`variavel++`)

Aumenta o valor da variável em 1 **depois** de usar a variável em uma expressão.

**Exemplo:**
```java
int num = 5;
int resultado = num++; // num é atribuído primeiramente à variável resultado e depois incrementado para 6
System.out.println(num);       // imprime 6
System.out.println(resultado); // imprime 5
```

---

## Resumo

Os operadores em Java são ferramentas essenciais para manipular dados e controlar o fluxo da aplicação. Dominar esses operadores é fundamental para escrever código eficiente e legível.

---

## 6. Diferenças entre Operadores Java e TypeScript/Node.js

Se você está familiarizado com TypeScript, existem algumas diferenças importantes entre os operadores do Java e do TypeScript/JavaScript que vale a pena conhecer:

### 6.1. Operadores de Igualdade

**Java:**
```java
int a = 5;
int b = 5;
boolean igual = (a == b); // true - compara valores
```

**TypeScript:**
```typescript
const a = 5;
const b = "5";
console.log(a == b);  // true - comparação com coerção de tipo
console.log(a === b); // false - comparação estrita (valor e tipo)
```

**Diferença:** Em Java, o operador `==` compara valores primitivos diretamente. Em TypeScript/JavaScript, temos `==` (comparação com coerção de tipo) e `===` (comparação estrita). **Em TypeScript, é recomendado sempre usar `===` e `!==`**.

### 6.2. Divisão de Números

**Java:**
```java
int a = 10;
int b = 3;
int resultado = a / b; // resultado = 3 (divisão inteira)

double c = 10.0;
double d = 3.0;
double resultado2 = c / d; // resultado2 = 3.333... (divisão real)
```

**TypeScript:**
```typescript
const a = 10;
const b = 3;
const resultado = a / b; // resultado = 3.3333... (sempre retorna número decimal)
```

**Diferença:** Em Java, a divisão entre inteiros retorna um inteiro (truncado). Em TypeScript/JavaScript, a divisão sempre retorna um número de ponto flutuante.

### 6.3. Operador de Exponenciação

**Java:**
```java
double resultado = Math.pow(2, 3); // 8.0 - usa método Math.pow()
```

**TypeScript:**
```typescript
const resultado = 2 ** 3; // 8 - operador de exponenciação nativo
```

**Diferença:** TypeScript/JavaScript tem o operador `**` para exponenciação, enquanto Java usa o método `Math.pow()`.

### 6.4. Operador de Coalescência Nula (`??`)

**TypeScript:**
```typescript
const valor = null ?? "valor padrão"; // "valor padrão"
const valor2 = 0 ?? "valor padrão";   // 0
```

**Java:**
```java
// Não existe operador equivalente nativo
// Precisa usar ternário ou Optional
String valor = texto != null ? texto : "valor padrão";
```

**Diferença:** TypeScript tem o operador `??` que retorna o valor da direita apenas se o da esquerda for `null` ou `undefined`. Java não possui esse operador nativo.

### 6.5. Optional Chaining (`?.`)

**TypeScript:**
```typescript
const user = { name: "João", address: { city: "São Paulo" } };
const city = user?.address?.city; // "São Paulo"
const country = user?.address?.country; // undefined (sem erro)
```

**Java:**
```java
// Não existe operador equivalente nativo
// Precisa usar Optional ou verificações manuais
String city = user != null && user.getAddress() != null 
    ? user.getAddress().getCity() 
    : null;
```

**Diferença:** TypeScript tem o operador `?.` para acesso seguro a propriedades. Java não possui esse operador, mas pode usar a classe `Optional` para casos similares.

### 6.6. Operador `typeof`

**TypeScript:**
```typescript
console.log(typeof 42);        // "number"
console.log(typeof "texto");   // "string"
console.log(typeof true);      // "boolean"
console.log(typeof undefined); // "undefined"
```

**Java:**
```java
// Não existe operador typeof
// Usa instanceof para verificar tipos de objetos
String texto = "Olá";
boolean ehString = texto instanceof String; // true
```

**Diferença:** JavaScript/TypeScript tem o operador `typeof` para verificar tipos em runtime. Java usa `instanceof` para verificar tipos de objetos (não funciona com primitivos).

### 6.7. Operador Ternário

**Ambos têm o operador ternário com sintaxe similar:**

**Java:**
```java
int idade = 18;
String resultado = idade >= 18 ? "Maior de idade" : "Menor de idade";
```

**TypeScript:**
```typescript
const idade = 18;
const resultado = idade >= 18 ? "Maior de idade" : "Menor de idade";
```

### 6.8. Spread Operator (`...`)

**TypeScript:**
```typescript
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5]; // [1, 2, 3, 4, 5]

const obj1 = { a: 1, b: 2 };
const obj2 = { ...obj1, c: 3 }; // { a: 1, b: 2, c: 3 }
```

**Java:**
```java
// Não existe spread operator
// Precisa usar métodos como Arrays.copyOf() ou coleções
List<Integer> list1 = Arrays.asList(1, 2, 3);
List<Integer> list2 = new ArrayList<>(list1);
list2.add(4);
list2.add(5);
```

**Diferença:** TypeScript tem o spread operator (`...`) para trabalhar com arrays e objetos. Java não possui esse operador.

### 6.9. Tipagem Estática vs Dinâmica

**Java:**
- Tipagem **estática e forte**: os tipos são verificados em tempo de compilação
- Todas as variáveis precisam ter tipo declarado (ou inferido pelo `var` a partir do Java 10)

**TypeScript:**
- Tipagem **estática em tempo de desenvolvimento**, mas compila para JavaScript (tipagem dinâmica)
- Tipos são opcionais e verificados apenas durante desenvolvimento

**JavaScript/Node.js:**
- Tipagem **dinâmica**: os tipos são verificados em tempo de execução
- Variáveis podem mudar de tipo durante a execução

### Resumo das Diferenças

| Recurso | Java | TypeScript/JavaScript |
|---------|------|----------------------|
| Comparação de igualdade | `==`, `!=` | `==`, `!=`, `===`, `!==` |
| Divisão de inteiros | Retorna inteiro | Sempre retorna decimal |
| Exponenciação | `Math.pow()` | `**` |
| Coalescência nula | Não tem | `??` |
| Optional chaining | Não tem | `?.` |
| Typeof | `instanceof` | `typeof` |
| Spread operator | Não tem | `...` |
| Tipagem | Estática e forte | Estática (TS) / Dinâmica (JS) |

**Dica:** Ao migrar de TypeScript para Java, lembre-se de que Java é mais rigoroso com tipos e não possui alguns operadores modernos de conveniência. Por outro lado, Java oferece maior segurança de tipos em tempo de compilação.
