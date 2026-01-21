# Imports em Java

Guia rápido sobre o sistema de imports do Java e comparação com Node.js.

## 📑 Índice

1. [Estrutura de Código: Classes Obrigatórias](#estrutura-de-código-classes-obrigatórias)
2. [Sintaxe Básica](#sintaxe-básica)
3. [Diferenças Java vs Node.js](#diferenças-java-vs-nodejs)
4. [Package vs Import: Entendendo a Diferença](#package-vs-import-entendendo-a-diferença)
5. [Tipos de Import](#tipos-de-import)
   - [Import de Classe Específica](#import-de-classe-específica)
   - [Import com Wildcard](#import-com-wildcard)
   - [Import Estático](#import-estático)
6. [Comparação de Sintaxe](#comparação-de-sintaxe)
7. [Pontos Importantes](#pontos-importantes)
8. [Boas Práticas](#boas-práticas)

---

## Estrutura de Código: Classes Obrigatórias

**Diferença fundamental:** No Java, **TODO o código precisa estar dentro de uma classe**. Diferente do Node.js, você não pode ter variáveis ou funções "soltas" no nível do arquivo.

### ❌ Não é possível em Java

```java
// Isso não compila!
double TAX_RATE = 0.15;
String API_URL = "https://api.com";

public void calculateDiscount() {
    // ...
}
```

### ✅ Como deve ser feito

```java
public class Constants {
    public static final double TAX_RATE = 0.15;
    public static final String API_URL = "https://api.com";
    
    public static double calculateDiscount(double value) {
        return value * 0.9;
    }
}
```

### Comparação: Node.js vs Java

**Node.js (código solto no arquivo):**
```javascript
// constants.js
export const VALID_COUPON = "NEWOFFER";
export const DISCOUNT_PERCENTAGE = 15;

export function calculateDiscount(value) {
    return value * 0.9;
}

// Pode usar diretamente
import { VALID_COUPON, calculateDiscount } from './constants.js';
```

**Java (tudo dentro de classes):**
```java
// Constants.java
public class Constants {
    public static final String VALID_COUPON = "NEWOFFER";
    public static final int DISCOUNT_PERCENTAGE = 15;
    
    public static double calculateDiscount(double value) {
        return value * 0.9;
    }
}

// Main.java
import Constants;

public class Main {
    public static void main(String[] args) {
        System.out.println(Constants.VALID_COUPON);
        double discount = Constants.calculateDiscount(100.0);
    }
}
```

### Por que Java é assim?

Java é uma linguagem **puramente orientada a objetos**, onde:
- ✅ Tudo deve estar organizado em classes
- ✅ Melhor encapsulamento e controle de acesso
- ✅ Estrutura mais previsível e organizada
- ✅ Todo arquivo `.java` deve conter pelo menos uma classe (ou interface, enum, record)

### Compartilhando Valores entre Arquivos

**Opção 1: Classe com membros estáticos**
```java
public class AppConfig {
    public static final String DATABASE_URL = "localhost:5432";
    public static final int MAX_CONNECTIONS = 10;
}
```

**Opção 2: Classe de constantes (utility class)**
```java
public class Constants {
    // Construtor privado para impedir instanciação
    private Constants() {
        throw new AssertionError("Não pode instanciar esta classe");
    }
    
    public static final String VALID_COUPON = "NEWOFFER";
    public static final int DISCOUNT = 15;
}
```

---

## Sintaxe Básica

```java
import java.util.ArrayList;           // importa uma classe específica
import java.util.*;                   // importa todas as classes do pacote
import static java.lang.Math.PI;     // import estático (constantes/métodos)
```

## Diferenças Java vs Node.js

| Aspecto | Java | Node.js |
|---------|------|---------|
| **Resolução** | Tempo de compilação | Tempo de execução (require) / estático (ES modules) |
| **Sistema** | Pacotes hierárquicos (`com.empresa.projeto`) | Sistema de arquivos + `node_modules` |
| **Wildcard** | `import java.util.*` | Não existe equivalente direto |
| **Sintaxe** | `import pacote.Classe;` | `require('modulo')` ou `import from 'modulo'` |

---

## Package vs Import: Entendendo a Diferença

**Confusão comum para quem vem do Node.js:** Em JavaScript/Node.js, o `import` resolve tudo (define o que você usa E de onde vem). Em Java, há uma separação clara entre `package` e `import`.

### `package` - Declaração de Pacote

**O que faz:** Define ONDE a sua classe está localizada (como um endereço ou namespace).

**Características:**
- Declarado **uma vez** no topo do arquivo (primeira linha não-comentário)
- Define a organização hierárquica do seu código
- Previne conflitos de nomes entre classes
- Cria um namespace único para cada classe

**Exemplo:**

```java
package com.empresa.projeto.modelos;

public class Usuario {
    private String nome;
    // ...
}
```

### `import` - Importação

**O que faz:** Traz classes de OUTROS pacotes para usar no seu código.

**Características:**
- Permite usar o nome curto da classe (sem o caminho completo)
- Pode importar várias classes
- Vem **depois** da declaração `package`
- Não é obrigatório (você pode usar nomes qualificados completos)

**Exemplo:**

```java
package com.empresa.projeto.servicos;

import com.empresa.projeto.modelos.Usuario;  // importa de outro pacote
import java.util.ArrayList;
import java.util.List;

public class UsuarioService {
    private List<Usuario> usuarios = new ArrayList<>();
    
    public void adicionarUsuario(Usuario usuario) {
        usuarios.add(usuario);
    }
}
```

### Comparação: Node.js vs Java

#### Node.js
```javascript
// UsuarioService.js

// Import FAZ TUDO: define o que você está usando E de onde vem
import { Usuario } from './modelos/Usuario.js';
import { readFile } from 'fs';
import express from 'express';

export class UsuarioService {
    // ...
}
```

#### Java Equivalente
```java
// Primeiro: declare onde VOCÊ está (seu endereço)
package com.empresa.projeto.servicos;

// Depois: importe o que você VAI USAR (dependências)
import com.empresa.projeto.modelos.Usuario;
import java.io.File;
import java.util.List;

public class UsuarioService {
    // ...
}
```

### Resumo das Diferenças

| Aspecto | `package` | `import` |
|---------|-----------|----------|
| **Propósito** | Declara onde SUA classe está | Traz classes de outros lugares |
| **Obrigatoriedade** | Opcional (mas recomendado) | Opcional (pode usar nomes completos) |
| **Quantidade** | Uma declaração por arquivo | Várias importações possíveis |
| **Posição** | Primeira linha não-comentário | Depois do `package` |
| **Equivalente Node.js** | Estrutura de pastas | `import` / `require` |

### Por que Java faz essa separação?

Java foi projetado para projetos corporativos muito grandes, onde:

1. **Organização rígida:** O `package` cria uma hierarquia clara (como `com.google.maps.api`)
2. **Prevenção de conflitos:** Duas empresas podem ter uma classe `Usuario`, mas `com.empresa1.Usuario` é diferente de `com.empresa2.Usuario`
3. **Distribuição:** Pacotes facilitam a criação de bibliotecas (JARs) com namespaces únicos
4. **Clareza:** Fica explícito onde cada classe está e de onde vem cada dependência

### Exemplo Completo

**Estrutura de pastas:**
```
src/
  com/
    empresa/
      projeto/
        modelos/
          Usuario.java
          Produto.java
        servicos/
          UsuarioService.java
        Main.java
```

**Usuario.java:**
```java
package com.empresa.projeto.modelos;

public class Usuario {
    private String nome;
    
    public Usuario(String nome) {
        this.nome = nome;
    }
    
    public String getNome() {
        return nome;
    }
}
```

**UsuarioService.java:**
```java
package com.empresa.projeto.servicos;

import com.empresa.projeto.modelos.Usuario;
import java.util.ArrayList;
import java.util.List;

public class UsuarioService {
    private List<Usuario> usuarios = new ArrayList<>();
    
    public void adicionar(Usuario usuario) {
        usuarios.add(usuario);
    }
    
    public List<Usuario> listar() {
        return usuarios;
    }
}
```

**Main.java:**
```java
package com.empresa.projeto;

import com.empresa.projeto.modelos.Usuario;
import com.empresa.projeto.servicos.UsuarioService;

public class Main {
    public static void main(String[] args) {
        UsuarioService service = new UsuarioService();
        Usuario usuario = new Usuario("João");
        service.adicionar(usuario);
        
        System.out.println("Usuário: " + usuario.getNome());
    }
}
```

### Sem Import (usando nomes qualificados)

Você pode usar classes sem importar, usando o nome completo:

```java
package com.empresa.projeto;

public class Main {
    public static void main(String[] args) {
        // Sem import, usando nomes completos
        com.empresa.projeto.servicos.UsuarioService service = 
            new com.empresa.projeto.servicos.UsuarioService();
        
        com.empresa.projeto.modelos.Usuario usuario = 
            new com.empresa.projeto.modelos.Usuario("João");
        
        service.adicionar(usuario);
    }
}
```

Mas isso fica **muito verboso**, por isso usamos `import`!

---

## Tipos de Import

### Import de Classe Específica
```java
import java.util.ArrayList;
import java.util.HashMap;
```

### Import com Wildcard
```java
import java.util.*;  // importa todas as classes do pacote
```

### Import Estático
```java
import static java.lang.Math.PI;
import static java.lang.Math.sqrt;

// Uso sem qualificação
double area = PI * raio * raio;
double resultado = sqrt(16);
```

## Comparação de Sintaxe

### Java
```java
import java.util.ArrayList;
import java.util.HashMap;

ArrayList<String> lista = new ArrayList<>();
```

### Node.js (CommonJS)
```javascript
const express = require('express');
const { readFile } = require('fs');
```

### Node.js (ES Modules)
```javascript
import express from 'express';
import { readFile } from 'fs';
```

## Pontos Importantes

- Imports em Java são **verificados em tempo de compilação**
- Erros de import impedem a compilação do código
- Wildcards (`*`) só importam classes do pacote direto, não de subpacotes
- Import estático permite usar métodos/constantes sem qualificar com a classe
- Não há "tree-shaking" como no JavaScript moderno

## Boas Práticas

✅ **Recomendado:**
- Importar apenas classes específicas necessárias
- Usar import estático com moderação (pode causar conflitos)

❌ **Evitar:**
- Uso excessivo de wildcards (dificulta saber a origem das classes)
- Import de pacotes inteiros quando usar poucas classes
