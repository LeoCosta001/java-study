# Wrapper Classes em Java

Classes que "envolvem" tipos primitivos, permitindo usá-los como objetos.

## Resumo Rápido

| Primitivo | Wrapper | Quando Usar |
|-----------|---------|-------------|
| `int` | `Integer` | Generics, Collections, valores `null` |
| `double` | `Double` | Generics, Collections, valores `null` |
| `boolean` | `Boolean` | Generics, Collections, valores `null` |

**Regra:** Generics só aceitam objetos → `List<int>` ❌ → `List<Integer>` ✅

---

## 1. Tabela Completa de Wrappers

| Primitivo | Wrapper | Parse String | Para String |
|-----------|---------|--------------|-------------|
| `boolean` | `Boolean` | `Boolean.parseBoolean("true")` | `Boolean.toString(true)` |
| `byte` | `Byte` | `Byte.parseByte("10")` | `Byte.toString((byte) 10)` |
| `char` | `Character` | - | `Character.toString('A')` |
| `short` | `Short` | `Short.parseShort("100")` | `Short.toString((short) 100)` |
| `int` | `Integer` | `Integer.parseInt("42")` | `Integer.toString(42)` |
| `long` | `Long` | `Long.parseLong("1000")` | `Long.toString(1000L)` |
| `float` | `Float` | `Float.parseFloat("3.14")` | `Float.toString(3.14f)` |
| `double` | `Double` | `Double.parseDouble("3.14")` | `Double.toString(3.14)` |

---

## 2. Autoboxing e Unboxing

Java converte automaticamente entre primitivo e wrapper.

### Autoboxing (primitivo → objeto)

```java
Integer num = 10;          // int → Integer (automático)
List<Integer> lista = new ArrayList<>();
lista.add(5);              // int → Integer (automático)
```

### Unboxing (objeto → primitivo)

```java
Integer wrapper = 10;
int primitivo = wrapper;   // Integer → int (automático)

int valor = lista.get(0);  // Integer → int (automático)
```

### Cuidado com Null

```java
Integer numero = null;
int valor = numero;        // NullPointerException!
```

**Solução:**
```java
int valor = (numero != null) ? numero : 0;
// Ou com Java 9+:
int valor = Objects.requireNonNullElse(numero, 0);
```

---

## 3. Métodos Úteis

### Integer

```java
// Parse
int n = Integer.parseInt("42");           // String → int
int hex = Integer.parseInt("FF", 16);     // 255 (hexadecimal)

// Comparação
Integer.compare(10, 20);     // -1 (menor)
Integer.compare(20, 10);     // 1 (maior)
Integer.compare(10, 10);     // 0 (igual)

// Min/Max
Integer.max(10, 20);         // 20
Integer.min(10, 20);         // 10

// Conversão
Integer.toString(42);        // "42"
Integer.toBinaryString(10);  // "1010"
Integer.toHexString(255);    // "ff"

// Constantes
Integer.MAX_VALUE;           // 2147483647
Integer.MIN_VALUE;           // -2147483648
```

### Double

```java
double d = Double.parseDouble("3.14");
Double.isNaN(0.0/0.0);       // true
Double.isInfinite(1.0/0.0);  // true
Double.compare(1.5, 2.5);    // -1

Double.MAX_VALUE;            // 1.7976931348623157E308
Double.MIN_VALUE;            // 4.9E-324
```

### Boolean

```java
boolean b = Boolean.parseBoolean("true");   // true
boolean b2 = Boolean.parseBoolean("TRUE");  // true (case-insensitive)
boolean b3 = Boolean.parseBoolean("yes");   // false (só "true" funciona)

Boolean.toString(true);      // "true"
Boolean.compare(true, false); // 1
```

### Character

```java
Character.isDigit('5');      // true
Character.isLetter('A');     // true
Character.isLetterOrDigit('A'); // true
Character.isWhitespace(' '); // true
Character.isUpperCase('A');  // true
Character.isLowerCase('a');  // true

Character.toUpperCase('a');  // 'A'
Character.toLowerCase('A');  // 'a'
```

---

## 4. Uso com Collections

```java
// ArrayList
List<Integer> numeros = new ArrayList<>();
numeros.add(10);
numeros.add(20);
int soma = numeros.get(0) + numeros.get(1);  // 30

// HashMap
Map<String, Double> precos = new HashMap<>();
precos.put("café", 5.50);
precos.put("pão", 2.00);
double preco = precos.get("café");  // 5.50

// Set
Set<Boolean> flags = new HashSet<>();
flags.add(true);
flags.add(false);
```

---

## 5. Comparação de Wrappers

### Cuidado com `==`

```java
Integer a = 127;
Integer b = 127;
System.out.println(a == b);      // true (cache de -128 a 127)

Integer c = 128;
Integer d = 128;
System.out.println(c == d);      // false (fora do cache!)
System.out.println(c.equals(d)); // true (sempre use equals!)
```

**Regra:** Sempre use `.equals()` para comparar Wrappers.

### Cache de Integer

Java mantém em cache valores de `-128` a `127` para `Integer`, `Byte`, `Short`, `Long` e `Character` (0 a 127).

---

## 6. Performance

| Operação | Primitivo | Wrapper |
|----------|-----------|---------|
| Memória | Menor | Maior (objeto + referência) |
| Velocidade | Mais rápido | Mais lento (boxing/unboxing) |
| Null | Não aceita | Aceita |

**Dica:** Use primitivos quando possível. Use Wrappers apenas quando necessário (Collections, nullable).

```java
// Preferível para loops
for (int i = 0; i < 1000000; i++) { }

// Evite (cria muitos objetos)
for (Integer i = 0; i < 1000000; i++) { }
```

---

## 7. Comparação: Java vs JavaScript

| Aspecto | Java | JavaScript |
|---------|------|------------|
| Primitivo | `int`, `double`, etc. | `number`, `boolean`, etc. |
| Objeto | `Integer`, `Double`, etc. | Autoboxing implícito |
| Parse | `Integer.parseInt("42")` | `parseInt("42")` ou `Number("42")` |
| Conversão | Manual ou autoboxing | Automática (coerção) |

**JavaScript:**
```javascript
const num = 42;
num.toString();  // JS faz autoboxing implícito para Number
```

**Java:**
```java
int num = 42;
// num.toString();  // ERRO! Primitivo não tem métodos
Integer.toString(num);  // OK
// Ou
Integer numWrapper = num;
numWrapper.toString();  // OK
```

---

## Resumo

| Cenário | Use |
|---------|-----|
| Cálculos intensivos | Primitivo (`int`, `double`) |
| Collections/Generics | Wrapper (`Integer`, `Double`) |
| Pode ser `null` | Wrapper |
| Parse de String | Métodos estáticos (`Integer.parseInt()`) |
| Comparação | `.equals()` para Wrappers |
