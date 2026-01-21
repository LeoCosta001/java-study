# Tipos Primitivos em Java

Em Java, assim como na maioria das linguagens de programação, existem os tipos primitivos, que são os tipos de dados mais básicos e fundamentais da linguagem. Eles são utilizados para representar valores simples e são definidos pela própria linguagem.

## Índice

1. [Os 8 Tipos Primitivos](#1-os-8-tipos-primitivos)
   - [boolean](#boolean)
   - [byte](#byte)
   - [char](#char)
   - [short](#short)
   - [int](#int)
   - [long](#long)
   - [float](#float)
   - [double](#double)
2. [Tabela Resumida dos Tipos Primitivos](#2-tabela-resumida-dos-tipos-primitivos)
3. [Casting (Conversão de Tipos)](#3-casting-conversão-de-tipos)
   - [Casting Implícito](#casting-implícito)
   - [Casting Explícito](#casting-explícito)
   - [Tabela de Conversões](#tabela-de-conversões)
4. [Diferenças entre Tipos Primitivos Java e TypeScript/JavaScript](#4-diferenças-entre-tipos-primitivos-java-e-typescriptjavascript)

---

## 1. Os 8 Tipos Primitivos

Java possui **oito tipos primitivos** diferentes. Cada um desses tipos possui suas próprias características e faixa de valores permitidos, conforme será descrito a seguir.

### boolean

O tipo `boolean` é utilizado para representar valores lógicos, podendo assumir apenas dois valores: `true` ou `false`. É utilizado em expressões condicionais, loops e outros casos onde se deseja avaliar se uma determinada condição é verdadeira ou falsa.

**Exemplo:**
```java
boolean ativo = true;
boolean maiorDeIdade = false;

if (ativo) {
    System.out.println("Usuário está ativo");
}
```

### byte

O tipo `byte` é utilizado para representar valores numéricos inteiros de **8 bits**. Ele possui uma faixa de valores de **-128 a 127**.

**Exemplo:**
```java
byte idade = 25;
byte temperatura = -10;
byte nota = 100;
```

### char

O tipo `char` é utilizado para representar **caracteres individuais**. Ele pode armazenar qualquer caractere Unicode e é representado por **aspas simples (`''`)**.

**Exemplo:**
```java
char letra = 'A';
char simbolo = '@';
char numero = '7'; // Armazena o caractere '7', não o número 7
```

### short

O tipo `short` é utilizado para representar valores numéricos inteiros de **16 bits**. Ele possui uma faixa de valores de **-32.768 a 32.767**.

**Exemplo:**
```java
short ano = 2026;
short populacao = 15000;
```

### int

O tipo `int` é utilizado para representar valores numéricos inteiros de **32 bits**. É um dos tipos de dados mais utilizados para representar números inteiros em Java e possui uma faixa de valores de **-2.147.483.648 a 2.147.483.647**.

**Exemplo:**
```java
int idade = 30;
int populacaoCidade = 1000000;
int saldo = -500;
```

### long

O tipo `long` é utilizado para representar valores numéricos inteiros de **64 bits**. Ele é utilizado para representar valores inteiros muito grandes e possui uma faixa de valores de **-9.223.372.036.854.775.808 a 9.223.372.036.854.775.807**.

**Exemplo:**
```java
long populacaoMundial = 7800000000L; // Note o 'L' no final
long distanciaKm = 384400L;
```

> **Nota:** É recomendado adicionar o sufixo `L` ao final de literais long para evitar confusão com int.

### float

O tipo `float` é utilizado para representar valores numéricos de **ponto flutuante** (valores com casas decimais), ocupando **32 bits** de memória. Ele pode representar números decimais com até **7 dígitos** e tem uma precisão limitada, o que significa que ele pode arredondar os números se eles forem muito grandes ou muito pequenos.

**Exemplo:**
```java
float preco = 19.99f; // Note o 'f' no final
float temperatura = -5.5f;
float pi = 3.14159f;
```

> **Nota:** É obrigatório adicionar o sufixo `f` ou `F` ao final de literais float.

### double

O tipo `double` é similar ao `float`, entretanto ele ocupa **64 bits** de memória e pode representar números decimais com até **15 dígitos**, oferecendo maior precisão.

**Exemplo:**
```java
double salario = 5500.75;
double pi = 3.141592653589793;
double distancia = 384400.5;
```

---

## 2. Tabela Resumida dos Tipos Primitivos

| Tipo | Tamanho | Faixa de Valores | Descrição |
|------|---------|------------------|-----------|
| `boolean` | 1 bit | `true` ou `false` | Valores lógicos |
| `byte` | 8 bits | -128 a 127 | Números inteiros pequenos |
| `char` | 16 bits | 0 a 65.535 (caracteres Unicode) | Caracteres individuais |
| `short` | 16 bits | -32.768 a 32.767 | Números inteiros médios |
| `int` | 32 bits | -2.147.483.648 a 2.147.483.647 | Números inteiros (mais comum) |
| `long` | 64 bits | -9.223.372.036.854.775.808 a 9.223.372.036.854.775.807 | Números inteiros muito grandes |
| `float` | 32 bits | ±3.4 × 10^38 (7 dígitos de precisão) | Números decimais com precisão simples |
| `double` | 64 bits | ±1.7 × 10^308 (15 dígitos de precisão) | Números decimais com precisão dupla |

---

## 3. Casting (Conversão de Tipos)

Casting é um recurso utilizado em Java para converter um tipo de dado em outro. Essa conversão pode ser feita de forma automática pelo compilador (**conversão implícita**), quando o tipo de dado de destino é compatível com o tipo de dado de origem, ou de forma manual (**conversão explícita**), utilizando o operador de casting.

O casting é utilizado para permitir que tipos de dados incompatíveis possam ser utilizados em uma mesma operação ou expressão. Por exemplo, se um método espera um parâmetro do tipo `int` e o valor que se deseja passar é do tipo `double`, é necessário fazer um casting para converter o valor em `int`.

### Casting Implícito

O casting implícito é realizado **automaticamente pelo compilador** quando o tipo de dado de origem é compatível com o tipo de dado de destino. Isso ocorre quando não há risco de perda de dados, ou seja, quando o tipo de destino é maior que o tipo de origem.

**Exemplo:**
```java
int x = 10;
double y = x; // casting implícito - int para double
System.out.println(y); // imprime 10.0

byte a = 5;
int b = a; // casting implícito - byte para int
System.out.println(b); // imprime 5

float preco = 19.99f;
double precoDouble = preco; // casting implícito - float para double
System.out.println(precoDouble); // imprime 19.989999771118164
```

### Casting Explícito

O casting explícito é realizado quando o tipo de dado de origem é **incompatível** com o tipo de dado de destino. Nesse caso, devemos utilizar o **operador de casting** para realizar a conversão. Isso é necessário quando há risco de perda de dados.

**Sintaxe:**
```java
tipoDestino variavel = (tipoDestino) valorOrigem;
```

**Exemplos:**
```java
double x = 10.5;
int y = (int) x; // casting explícito - double para int
System.out.println(y); // imprime 10 (a parte decimal é descartada)

int valor = 130;
byte valorByte = (byte) valor; // casting explícito - int para byte
System.out.println(valorByte); // imprime -126 (overflow, pois 130 está fora da faixa do byte)

long numeroGrande = 1000000L;
int numeroMenor = (int) numeroGrande; // casting explícito - long para int
System.out.println(numeroMenor); // imprime 1000000

double preco = 29.99;
float precoFloat = (float) preco; // casting explícito - double para float
System.out.println(precoFloat); // imprime 29.99
```

> **Atenção:** No casting explícito, pode haver perda de dados. Por exemplo, ao converter `double` para `int`, a parte decimal é descartada. Se o valor estiver fora da faixa do tipo de destino, pode ocorrer **overflow**.

### Tabela de Conversões

Esta tabela mostra quando o casting é implícito (✓) ou quando é necessário fazer casting explícito (✗):

| DE → PARA | byte | short | char | int | long | float | double |
|-----------|------|-------|------|-----|------|-------|--------|
| **byte** | - | ✓ | ✗ | ✓ | ✓ | ✓ | ✓ |
| **short** | ✗ | - | ✗ | ✓ | ✓ | ✓ | ✓ |
| **char** | ✗ | ✗ | - | ✓ | ✓ | ✓ | ✓ |
| **int** | ✗ | ✗ | ✗ | - | ✓ | ✓ | ✓ |
| **long** | ✗ | ✗ | ✗ | ✗ | - | ✓ | ✓ |
| **float** | ✗ | ✗ | ✗ | ✗ | ✗ | - | ✓ |
| **double** | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | - |

**Legenda:**
- ✓ = Casting implícito (automático)
- ✗ = Casting explícito (manual)

**Regra geral:** A conversão é implícita quando o tipo de destino é "maior" que o tipo de origem. A ordem de "tamanho" é:

```
byte → short → int → long → float → double
       char ↗
```

---

## 4. Diferenças entre Tipos Primitivos Java e TypeScript/JavaScript

Se você está familiarizado com TypeScript/JavaScript, existem diferenças importantes nos tipos primitivos:

### 4.1. Quantidade de Tipos Numéricos

**Java:**
- Possui **7 tipos numéricos** diferentes (`byte`, `short`, `int`, `long`, `float`, `double`, `char`)
- Cada tipo tem tamanho e precisão específicos

```java
byte pequeno = 10;
int medio = 1000;
long grande = 1000000L;
float decimal1 = 10.5f;
double decimal2 = 10.5;
```

**TypeScript/JavaScript:**
- Possui apenas **1 tipo numérico**: `number`
- Todos os números são representados como ponto flutuante de 64 bits (equivalente ao `double` do Java)

```typescript
const pequeno: number = 10;
const medio: number = 1000;
const grande: number = 1000000;
const decimal1: number = 10.5;
const decimal2: number = 10.5;
```

### 4.2. Tipo Boolean

**Java:**
```java
boolean ativo = true;
// boolean valor = 1; // ERRO: não aceita números como boolean
```

**TypeScript/JavaScript:**
```typescript
const ativo: boolean = true;
// Em JavaScript puro, valores "truthy" e "falsy" são comuns:
if (1) { } // 1 é considerado "truthy"
if ("") { } // "" é considerado "falsy"
```

**Diferença:** Em Java, `boolean` só aceita `true` ou `false`. Em JavaScript, existe o conceito de valores "truthy" e "falsy", onde vários valores podem ser avaliados como verdadeiro ou falso.

### 4.3. Tipo Char vs String

**Java:**
```java
char letra = 'A';      // um único caractere (aspas simples)
String palavra = "Olá"; // cadeia de caracteres (aspas duplas)
// char erro = "A"; // ERRO: char só aceita aspas simples
```

**TypeScript/JavaScript:**
```typescript
const letra = 'A';     // string com um caractere
const palavra = "Olá";  // string
// Aspas simples e duplas são equivalentes
const texto1 = 'texto';
const texto2 = "texto"; // ambos são válidos e equivalentes
```

**Diferença:** Java diferencia `char` (um caractere) de `String` (cadeia de caracteres). JavaScript/TypeScript não tem tipo `char`, apenas `string`.

### 4.4. BigInt

**TypeScript/JavaScript (ES2020+):**
```typescript
const numeroGigante = 9007199254740991n; // BigInt nativo
const outro = BigInt("9007199254740991");
```

**Java:**
```java
import java.math.BigInteger;
BigInteger numeroGigante = new BigInteger("9007199254740991");
```

**Diferença:** JavaScript tem `BigInt` nativo. Java usa a classe `BigInteger` (não é tipo primitivo).

### 4.5. Conversão de Tipos

**Java:**
```java
// Conversão explícita necessária em muitos casos
double x = 10.5;
int y = (int) x; // casting explícito obrigatório
```

**TypeScript:**
```typescript
// TypeScript verifica tipos em tempo de desenvolvimento
const x: number = 10.5;
const y: number = x; // OK, ambos são number

// JavaScript faz coerção de tipos automaticamente
const resultado = "5" + 3; // "53" (concatenação)
const resultado2 = "5" - 3; // 2 (subtração numérica)
```

**Diferença:** Java exige casting explícito entre tipos incompatíveis. JavaScript faz coerção de tipos automática (às vezes inesperada). TypeScript adiciona verificação de tipos em tempo de desenvolvimento.

### 4.6. Resumo das Diferenças

| Recurso | Java | TypeScript/JavaScript |
|---------|------|----------------------|
| Tipos numéricos | 7 tipos diferentes | 1 tipo: `number` |
| Tipo boolean | Apenas `true`/`false` | `true`/`false` + "truthy"/"falsy" |
| Tipo char | `char` (um caractere) | Não existe, apenas `string` |
| Aspas | Simples para `char`, duplas para `String` | Simples e duplas equivalentes |
| BigInt/BigInteger | `BigInteger` (classe) | `BigInt` (tipo primitivo) |
| Casting | Explícito e rigoroso | Coerção automática (JS) / Verificação estática (TS) |
| Verificação de tipos | Em tempo de compilação | Em runtime (JS) / desenvolvimento (TS) |

**Dica:** Java oferece mais controle e precisão sobre os tipos de dados, o que pode prevenir bugs relacionados a overflow ou perda de precisão. TypeScript/JavaScript oferece mais flexibilidade, mas requer mais atenção do desenvolvedor para evitar erros de tipo.

---

## Resumo

Os tipos primitivos são a base da programação em Java. Conhecer suas características, faixas de valores e quando utilizar cada um é fundamental para escrever código eficiente e evitar erros. O casting permite converter entre diferentes tipos, mas deve ser usado com cuidado para evitar perda de dados ou comportamentos inesperados.
