# Orientação a Objetos em Java

A Programação Orientada a Objetos (POO) é um paradigma de programação que organiza o código em torno de objetos que representam entidades do mundo real. Java é uma linguagem totalmente orientada a objetos, o que significa que quase tudo em Java é um objeto ou está relacionado a objetos.

## Índice

1. [Os 4 Pilares da POO](#1-os-4-pilares-da-poo)
   - [Abstração](#abstração)
   - [Encapsulamento](#encapsulamento)
   - [Herança](#herança)
   - [Polimorfismo](#polimorfismo)
2. [Classes e Objetos](#2-classes-e-objetos)
   - [Definindo uma Classe](#definindo-uma-classe)
   - [Criando Objetos](#criando-objetos)
   - [Atributos](#atributos)
   - [Métodos](#métodos)
3. [Modificadores de Acesso](#3-modificadores-de-acesso)
   - [Tabela de Modificadores](#tabela-de-modificadores)
4. [Construtores](#4-construtores)
   - [Construtor Padrão](#construtor-padrão)
   - [Construtor Parametrizado](#construtor-parametrizado)
   - [Sobrecarga de Construtores](#sobrecarga-de-construtores)
5. [Métodos Especiais](#5-métodos-especiais)
   - [Getters e Setters](#getters-e-setters)
   - [Método toString()](#método-tostring)
   - [Métodos Static](#métodos-static)
6. [Herança](#6-herança)
   - [Palavra-chave extends](#palavra-chave-extends)
   - [Palavra-chave super](#palavra-chave-super)
   - [Sobrescrita de Métodos](#sobrescrita-de-métodos)
7. [Classes Abstratas](#7-classes-abstratas)
8. [Interfaces](#8-interfaces)
9. [Polimorfismo na Prática](#9-polimorfismo-na-prática)
10. [Boas Práticas POO](#10-boas-práticas-poo)

---

## 1. Os 4 Pilares da POO

Os quatro pilares da Programação Orientada a Objetos são conceitos fundamentais que guiam o design e implementação de código orientado a objetos.

### Abstração

**Definição:** Abstração é o processo de identificar as características essenciais de um objeto e ignorar os detalhes irrelevantes. Focamos no "o que" o objeto faz, não no "como" ele faz.

**Exemplo:**
```java
// Abstraímos um carro pelas suas características essenciais
public class Carro {
    private String marca;
    private String modelo;
    private int ano;
    
    public void ligar() {
        // Usuário não precisa saber como o motor liga
        System.out.println("Carro ligado");
    }
    
    public void acelerar() {
        System.out.println("Acelerando...");
    }
}
```

### Encapsulamento

**Definição:** Encapsulamento é o princípio de esconder os detalhes internos de implementação e expor apenas o necessário através de uma interface pública. Protege os dados e controla o acesso a eles.

**Exemplo:**
```java
public class ContaBancaria {
    private double saldo; // Atributo privado - encapsulado
    
    // Acesso controlado através de métodos públicos
    public double getSaldo() {
        return saldo;
    }
    
    public void depositar(double valor) {
        if (valor > 0) {
            saldo += valor;
        }
    }
    
    public boolean sacar(double valor) {
        if (valor > 0 && valor <= saldo) {
            saldo -= valor;
            return true;
        }
        return false;
    }
}
```

**Benefícios:**
- Proteção dos dados
- Controle de validação
- Facilita manutenção
- Reduz acoplamento

### Herança

**Definição:** Herança permite que uma classe (subclasse/filha) herde atributos e métodos de outra classe (superclasse/pai), promovendo reutilização de código.

**Exemplo:**
```java
// Classe pai
public class Animal {
    protected String nome;
    
    public void comer() {
        System.out.println(nome + " está comendo");
    }
}

// Classe filha herda de Animal
public class Cachorro extends Animal {
    public void latir() {
        System.out.println(nome + " está latindo");
    }
}

// Uso
Cachorro dog = new Cachorro();
dog.nome = "Rex";
dog.comer();  // Método herdado
dog.latir();  // Método próprio
```

### Polimorfismo

**Definição:** Polimorfismo permite que objetos de diferentes classes sejam tratados de forma uniforme através de uma interface comum. "Poli" = muitas, "morfismo" = formas.

**Tipos:**
- **Polimorfismo de Sobrecarga (Overloading):** Múltiplos métodos com mesmo nome, mas parâmetros diferentes
- **Polimorfismo de Sobrescrita (Overriding):** Subclasse redefine método da superclasse

**Exemplo:**
```java
public class Animal {
    public void emitirSom() {
        System.out.println("Animal fazendo som");
    }
}

public class Cachorro extends Animal {
    @Override
    public void emitirSom() {
        System.out.println("Au au!");
    }
}

public class Gato extends Animal {
    @Override
    public void emitirSom() {
        System.out.println("Miau!");
    }
}

// Polimorfismo em ação
Animal animal1 = new Cachorro();
Animal animal2 = new Gato();
animal1.emitirSom(); // Au au!
animal2.emitirSom(); // Miau!
```

---

## 2. Classes e Objetos

### Definindo uma Classe

Uma **classe** é um modelo/template que define as características (atributos) e comportamentos (métodos) de objetos.

**Sintaxe:**
```java
public class NomeDaClasse {
    // Atributos (variáveis de instância)
    private tipo atributo1;
    private tipo atributo2;
    
    // Construtor
    public NomeDaClasse(tipo param1, tipo param2) {
        this.atributo1 = param1;
        this.atributo2 = param2;
    }
    
    // Métodos
    public void metodo() {
        // código
    }
}
```

**Exemplo Completo:**
```java
public class Pessoa {
    // Atributos
    private String nome;
    private int idade;
    private String cpf;
    
    // Construtor
    public Pessoa(String nome, int idade, String cpf) {
        this.nome = nome;
        this.idade = idade;
        this.cpf = cpf;
    }
    
    // Métodos
    public void apresentar() {
        System.out.println("Olá, meu nome é " + nome);
    }
    
    public boolean ehMaiorDeIdade() {
        return idade >= 18;
    }
}
```

### Criando Objetos

Um **objeto** é uma instância de uma classe. Para criar um objeto, usamos o operador `new`.

**Sintaxe:**
```java
NomeDaClasse nomeDoObjeto = new NomeDaClasse(parametros);
```

**Exemplo:**
```java
// Criando objetos
Pessoa pessoa1 = new Pessoa("João", 25, "123.456.789-00");
Pessoa pessoa2 = new Pessoa("Maria", 17, "987.654.321-00");

// Usando os objetos
pessoa1.apresentar(); // Olá, meu nome é João
System.out.println(pessoa1.ehMaiorDeIdade()); // true
System.out.println(pessoa2.ehMaiorDeIdade()); // false
```

### Atributos

Atributos (ou variáveis de instância) representam as **características** do objeto.

**Boas Práticas:**
- Sempre declarar atributos como `private` (encapsulamento)
- Usar nomes descritivos
- Inicializar no construtor ou com valores padrão

**Exemplo:**
```java
public class Carro {
    private String marca;      // Atributo privado
    private String modelo;     // Atributo privado
    private int ano;           // Atributo privado
    private boolean ligado = false; // Inicializado com valor padrão
}
```

### Métodos

Métodos representam os **comportamentos** ou ações que o objeto pode realizar.

**Sintaxe:**
```java
modificadorAcesso tipoRetorno nomeMetodo(parametros) {
    // corpo do método
    return valor; // se tipoRetorno != void
}
```

**Exemplo:**
```java
public class Calculadora {
    // Método que retorna valor
    public int somar(int a, int b) {
        return a + b;
    }
    
    // Método sem retorno (void)
    public void exibirResultado(int resultado) {
        System.out.println("Resultado: " + resultado);
    }
    
    // Método com múltiplos parâmetros
    public double calcularMedia(double nota1, double nota2, double nota3) {
        return (nota1 + nota2 + nota3) / 3;
    }
}
```

---

## 3. Modificadores de Acesso

Modificadores de acesso controlam a visibilidade de classes, atributos e métodos.

### Tabela de Modificadores

| Modificador | Classe Própria | Pacote | Subclasse | Todos |
|-------------|----------------|--------|-----------|-------|
| `private` | ✓ | ✗ | ✗ | ✗ |
| **(default)** | ✓ | ✓ | ✗ | ✗ |
| `protected` | ✓ | ✓ | ✓ | ✗ |
| `public` | ✓ | ✓ | ✓ | ✓ |

**Descrição:**

- **`private`:** Acesso apenas dentro da própria classe
- **`(default)`:** Acesso apenas dentro do mesmo pacote (quando não especifica modificador)
- **`protected`:** Acesso dentro do pacote e por subclasses
- **`public`:** Acesso de qualquer lugar

**Exemplo:**
```java
public class Pessoa {
    private String cpf;          // Apenas dentro da classe
    protected String nome;       // Classe, pacote e subclasses
    public int idade;            // Qualquer lugar
    String endereco;             // Default: apenas no pacote
    
    private void validarCPF() {  // Método privado
        // Lógica interna
    }
    
    public String getNome() {    // Método público
        return nome;
    }
}
```

**Boas Práticas:**
- Atributos: sempre `private`
- Métodos públicos (API): `public`
- Métodos auxiliares: `private`
- Herança: `protected` quando necessário

---

## 4. Construtores

Construtores são métodos especiais chamados quando um objeto é criado. Eles inicializam os atributos do objeto.

**Características:**
- Mesmo nome da classe
- Não tem tipo de retorno (nem `void`)
- Pode receber parâmetros
- Pode haver múltiplos construtores (sobrecarga)

### Construtor Padrão

Se você não criar nenhum construtor, Java fornece um construtor padrão sem parâmetros.

**Exemplo:**
```java
public class Produto {
    private String nome;
    private double preco;
    
    // Construtor padrão (sem parâmetros)
    public Produto() {
        this.nome = "Sem nome";
        this.preco = 0.0;
    }
}

// Uso
Produto p = new Produto(); // Chama construtor padrão
```

### Construtor Parametrizado

Construtor que recebe parâmetros para inicializar os atributos.

**Exemplo:**
```java
public class Produto {
    private String nome;
    private double preco;
    
    // Construtor parametrizado
    public Produto(String nome, double preco) {
        this.nome = nome;
        this.preco = preco;
    }
}

// Uso
Produto p = new Produto("Notebook", 2500.00);
```

> **Nota:** A palavra-chave `this` refere-se ao atributo da instância atual, diferenciando-o do parâmetro.

### Sobrecarga de Construtores

Você pode ter múltiplos construtores com diferentes parâmetros.

**Exemplo:**
```java
public class Pessoa {
    private String nome;
    private int idade;
    private String email;
    
    // Construtor 1: apenas nome
    public Pessoa(String nome) {
        this.nome = nome;
        this.idade = 0;
        this.email = "";
    }
    
    // Construtor 2: nome e idade
    public Pessoa(String nome, int idade) {
        this.nome = nome;
        this.idade = idade;
        this.email = "";
    }
    
    // Construtor 3: todos os atributos
    public Pessoa(String nome, int idade, String email) {
        this.nome = nome;
        this.idade = idade;
        this.email = email;
    }
    
    // Construtor 4: usando this() para chamar outro construtor
    public Pessoa() {
        this("Anônimo", 0, "");
    }
}

// Uso
Pessoa p1 = new Pessoa("João");
Pessoa p2 = new Pessoa("Maria", 25);
Pessoa p3 = new Pessoa("Pedro", 30, "pedro@email.com");
Pessoa p4 = new Pessoa();
```

---

## 5. Métodos Especiais

### Getters e Setters

Métodos que permitem acessar e modificar atributos privados de forma controlada.

**Nomenclatura:**
- **Getter:** `getTipoAtributo()` ou `isAtributo()` para boolean
- **Setter:** `setAtributo(tipo valor)`

**Exemplo:**
```java
public class Produto {
    private String nome;
    private double preco;
    private boolean disponivel;
    
    // Getter para nome
    public String getNome() {
        return nome;
    }
    
    // Setter para nome
    public void setNome(String nome) {
        this.nome = nome;
    }
    
    // Getter para preco
    public double getPreco() {
        return preco;
    }
    
    // Setter para preco com validação
    public void setPreco(double preco) {
        if (preco >= 0) {
            this.preco = preco;
        } else {
            System.out.println("Preço inválido!");
        }
    }
    
    // Getter para boolean usa "is" ao invés de "get"
    public boolean isDisponivel() {
        return disponivel;
    }
    
    // Setter para disponivel
    public void setDisponivel(boolean disponivel) {
        this.disponivel = disponivel;
    }
}
```

**Quando usar:**
- ✓ Sempre para atributos `private` que precisam ser acessados externamente
- ✓ Quando precisa validação ou lógica adicional
- ✗ Não criar getters/setters se o atributo não deve ser acessado externamente

### Método toString()

Método que retorna uma representação em String do objeto. É útil para debug e exibição.

**Exemplo:**
```java
public class Pessoa {
    private String nome;
    private int idade;
    
    public Pessoa(String nome, int idade) {
        this.nome = nome;
        this.idade = idade;
    }
    
    @Override
    public String toString() {
        return "Pessoa{nome='" + nome + "', idade=" + idade + "}";
    }
}

// Uso
Pessoa p = new Pessoa("João", 25);
System.out.println(p); // Pessoa{nome='João', idade=25}
```

### Métodos Static

Métodos estáticos pertencem à **classe**, não a instâncias individuais. Podem ser chamados sem criar um objeto.

**Características:**
- Não podem acessar atributos de instância
- Não podem usar `this`
- Úteis para utilitários e constantes

**Exemplo:**
```java
public class Matematica {
    // Método static
    public static int somar(int a, int b) {
        return a + b;
    }
    
    public static double calcularArea(double raio) {
        return Math.PI * raio * raio;
    }
}

// Uso (sem criar objeto)
int resultado = Matematica.somar(5, 3);
double area = Matematica.calcularArea(5.0);

// Comparação
// Math.pow() - método static da classe Math
// String.valueOf() - método static da classe String
```

---

## 6. Herança

Herança é um mecanismo que permite criar uma nova classe baseada em uma classe existente, reutilizando código e estabelecendo uma relação "é um".

### Palavra-chave extends

Usamos `extends` para indicar que uma classe herda de outra.

**Sintaxe:**
```java
public class ClasseFilha extends ClassePai {
    // atributos e métodos adicionais
}
```

**Exemplo:**
```java
// Classe pai (superclasse)
public class Veiculo {
    protected String marca;
    protected String modelo;
    protected int ano;
    
    public Veiculo(String marca, String modelo, int ano) {
        this.marca = marca;
        this.modelo = modelo;
        this.ano = ano;
    }
    
    public void ligar() {
        System.out.println("Veículo ligado");
    }
    
    public void desligar() {
        System.out.println("Veículo desligado");
    }
}

// Classe filha (subclasse)
public class Carro extends Veiculo {
    private int numeroPortas;
    
    public Carro(String marca, String modelo, int ano, int numeroPortas) {
        super(marca, modelo, ano); // Chama construtor da classe pai
        this.numeroPortas = numeroPortas;
    }
    
    public void abrirPortaMalas() {
        System.out.println("Porta-malas aberto");
    }
}

// Uso
Carro carro = new Carro("Toyota", "Corolla", 2023, 4);
carro.ligar();           // Método herdado
carro.abrirPortaMalas(); // Método próprio
```

### Palavra-chave super

`super` é usado para:
1. Chamar o construtor da classe pai
2. Acessar métodos da classe pai

**Exemplo:**
```java
public class Animal {
    protected String nome;
    
    public Animal(String nome) {
        this.nome = nome;
    }
    
    public void emitirSom() {
        System.out.println("Animal fazendo som");
    }
}

public class Cachorro extends Animal {
    private String raca;
    
    public Cachorro(String nome, String raca) {
        super(nome); // Chama construtor de Animal
        this.raca = raca;
    }
    
    @Override
    public void emitirSom() {
        super.emitirSom(); // Chama método da classe pai
        System.out.println("Au au!");
    }
}
```

### Sobrescrita de Métodos

Sobrescrita (override) permite que a subclasse redefina um método da superclasse.

**Regras:**
- Mesma assinatura (nome, parâmetros, retorno)
- Usar anotação `@Override` (boa prática)
- Não pode reduzir a visibilidade

**Exemplo:**
```java
public class Funcionario {
    protected String nome;
    protected double salario;
    
    public double calcularBonus() {
        return salario * 0.10; // 10% de bônus
    }
}

public class Gerente extends Funcionario {
    @Override
    public double calcularBonus() {
        return salario * 0.20; // 20% de bônus para gerentes
    }
}

public class Diretor extends Funcionario {
    @Override
    public double calcularBonus() {
        return salario * 0.30; // 30% de bônus para diretores
    }
}
```

---

## 7. Classes Abstratas

Classes abstratas são classes que **não podem ser instanciadas** e servem como base para outras classes.

**Características:**
- Usam palavra-chave `abstract`
- Podem ter métodos abstratos (sem implementação)
- Podem ter métodos concretos (com implementação)
- Podem ter atributos
- Subclasses devem implementar métodos abstratos

**Exemplo:**
```java
// Classe abstrata
public abstract class Forma {
    protected String cor;
    
    public Forma(String cor) {
        this.cor = cor;
    }
    
    // Método abstrato (sem implementação)
    public abstract double calcularArea();
    
    // Método concreto (com implementação)
    public void exibirCor() {
        System.out.println("Cor: " + cor);
    }
}

// Subclasse implementa método abstrato
public class Circulo extends Forma {
    private double raio;
    
    public Circulo(String cor, double raio) {
        super(cor);
        this.raio = raio;
    }
    
    @Override
    public double calcularArea() {
        return Math.PI * raio * raio;
    }
}

public class Retangulo extends Forma {
    private double largura;
    private double altura;
    
    public Retangulo(String cor, double largura, double altura) {
        super(cor);
        this.largura = largura;
        this.altura = altura;
    }
    
    @Override
    public double calcularArea() {
        return largura * altura;
    }
}

// Uso
// Forma f = new Forma("azul"); // ERRO: não pode instanciar classe abstrata
Circulo c = new Circulo("vermelho", 5.0);
Retangulo r = new Retangulo("azul", 4.0, 6.0);

System.out.println(c.calcularArea()); // 78.54
System.out.println(r.calcularArea()); // 24.0
```

**Quando usar:**
- Quando há comportamento comum entre classes
- Quando algumas implementações devem ser obrigatórias nas subclasses
- Para criar hierarquias de classes

---

## 8. Interfaces

Interfaces definem um **contrato** que as classes devem seguir. Especificam "o que" fazer, não "como" fazer.

**Características:**
- Palavra-chave `interface`
- Todos os métodos são abstratos por padrão (até Java 7)
- Não podem ter atributos de instância (apenas constantes)
- Uma classe pode implementar múltiplas interfaces
- Usam palavra-chave `implements`

**Exemplo:**
```java
// Definindo interface
public interface Pagavel {
    void processarPagamento(double valor);
    boolean validarPagamento();
}

// Implementando interface
public class CartaoCredito implements Pagavel {
    private String numero;
    
    @Override
    public void processarPagamento(double valor) {
        System.out.println("Pagamento de R$" + valor + " no cartão");
    }
    
    @Override
    public boolean validarPagamento() {
        return numero != null && numero.length() == 16;
    }
}

public class Pix implements Pagavel {
    private String chave;
    
    @Override
    public void processarPagamento(double valor) {
        System.out.println("Pagamento de R$" + valor + " via PIX");
    }
    
    @Override
    public boolean validarPagamento() {
        return chave != null && !chave.isEmpty();
    }
}
```

**Múltiplas Interfaces:**
```java
public interface Autenticavel {
    boolean autenticar(String senha);
}

public interface Imprimivel {
    void imprimir();
}

// Classe implementa múltiplas interfaces
public class Usuario implements Autenticavel, Imprimivel {
    private String nome;
    private String senha;
    
    @Override
    public boolean autenticar(String senha) {
        return this.senha.equals(senha);
    }
    
    @Override
    public void imprimir() {
        System.out.println("Usuário: " + nome);
    }
}
```

**Interface vs Classe Abstrata:**

| Aspecto | Interface | Classe Abstrata |
|---------|-----------|-----------------|
| Herança múltipla | ✓ Sim (implementa várias) | ✗ Não (extends apenas uma) |
| Métodos abstratos | Todos (por padrão) | Podem ter abstratos e concretos |
| Atributos | Apenas constantes | Pode ter atributos normais |
| Construtor | ✗ Não tem | ✓ Pode ter |
| Quando usar | Definir contrato/comportamento | Compartilhar código entre classes |

---

## 9. Polimorfismo na Prática

Polimorfismo permite tratar objetos de diferentes classes de forma uniforme através de uma interface comum.

**Exemplo Completo:**
```java
// Interface comum
public interface Funcionario {
    double calcularSalario();
    void exibirDetalhes();
}

// Diferentes implementações
public class FuncionarioHorista implements Funcionario {
    private String nome;
    private double valorHora;
    private int horasTrabalhadas;
    
    @Override
    public double calcularSalario() {
        return valorHora * horasTrabalhadas;
    }
    
    @Override
    public void exibirDetalhes() {
        System.out.println(nome + " - Horista");
    }
}

public class FuncionarioMensalista implements Funcionario {
    private String nome;
    private double salarioBase;
    
    @Override
    public double calcularSalario() {
        return salarioBase;
    }
    
    @Override
    public void exibirDetalhes() {
        System.out.println(nome + " - Mensalista");
    }
}

public class FuncionarioComissionado implements Funcionario {
    private String nome;
    private double salarioBase;
    private double comissao;
    
    @Override
    public double calcularSalario() {
        return salarioBase + comissao;
    }
    
    @Override
    public void exibirDetalhes() {
        System.out.println(nome + " - Comissionado");
    }
}

// Polimorfismo em ação
public class FolhaPagamento {
    public void processar(Funcionario[] funcionarios) {
        double total = 0;
        
        for (Funcionario f : funcionarios) {
            f.exibirDetalhes();
            double salario = f.calcularSalario();
            System.out.println("Salário: R$" + salario);
            total += salario;
        }
        
        System.out.println("Total: R$" + total);
    }
}

// Uso
Funcionario[] equipe = new Funcionario[3];
equipe[0] = new FuncionarioHorista(...);
equipe[1] = new FuncionarioMensalista(...);
equipe[2] = new FuncionarioComissionado(...);

FolhaPagamento folha = new FolhaPagamento();
folha.processar(equipe); // Trata todos uniformemente
```

---

## 10. Boas Práticas POO

### Princípios SOLID

**S - Single Responsibility Principle (Princípio da Responsabilidade Única)**
- Uma classe deve ter apenas uma razão para mudar
- Cada classe deve ter uma única responsabilidade

```java
// ❌ Ruim: classe com múltiplas responsabilidades
public class Usuario {
    public void salvarNoBanco() { }
    public void enviarEmail() { }
    public void gerarRelatorio() { }
}

// ✓ Bom: classes com responsabilidades únicas
public class Usuario {
    private String nome;
    private String email;
}

public class UsuarioRepository {
    public void salvar(Usuario usuario) { }
}

public class EmailService {
    public void enviar(String destinatario, String mensagem) { }
}

public class RelatorioService {
    public void gerar(Usuario usuario) { }
}
```

**O - Open/Closed Principle (Princípio Aberto/Fechado)**
- Classes devem estar abertas para extensão, mas fechadas para modificação

```java
// ✓ Bom: usar interfaces e polimorfismo
public interface DescontoStrategy {
    double calcular(double valor);
}

public class DescontoCliente implements DescontoStrategy {
    public double calcular(double valor) {
        return valor * 0.10;
    }
}

public class DescontoVIP implements DescontoStrategy {
    public double calcular(double valor) {
        return valor * 0.20;
    }
}
```

**L - Liskov Substitution Principle (Princípio da Substituição de Liskov)**
- Subclasses devem poder substituir suas superclasses sem quebrar o programa

```java
// ✓ Bom: subclasse comporta-se como esperado
public class Retangulo {
    protected double largura;
    protected double altura;
    
    public void setLargura(double largura) {
        this.largura = largura;
    }
    
    public void setAltura(double altura) {
        this.altura = altura;
    }
    
    public double calcularArea() {
        return largura * altura;
    }
}

// ❌ Ruim: Quadrado quebraria LSP se herdasse de Retangulo
// porque setLargura() e setAltura() teriam comportamento diferente
```

**I - Interface Segregation Principle (Princípio da Segregação de Interface)**
- Interfaces específicas são melhores que uma interface genérica

```java
// ❌ Ruim: interface muito grande
public interface Funcionario {
    void trabalhar();
    void receberSalario();
    void gerenciarEquipe();    // Nem todos gerenciam
    void aprovarOrcamento();   // Nem todos aprovam
}

// ✓ Bom: interfaces segregadas
public interface Trabalhador {
    void trabalhar();
    void receberSalario();
}

public interface Gerente {
    void gerenciarEquipe();
}

public interface Diretor {
    void aprovarOrcamento();
}
```

**D - Dependency Inversion Principle (Princípio da Inversão de Dependência)**
- Dependa de abstrações, não de implementações concretas

```java
// ❌ Ruim: depende de implementação concreta
public class Pedido {
    private MySQLDatabase db = new MySQLDatabase();
}

// ✓ Bom: depende de abstração
public interface Database {
    void salvar(Object obj);
}

public class Pedido {
    private Database db;
    
    public Pedido(Database db) {
        this.db = db; // Injeção de dependência
    }
}
```

### Outras Boas Práticas

**1. Encapsulamento Adequado**
```java
// ✓ Sempre use getters/setters para atributos privados
private String nome;

public String getNome() {
    return nome;
}

public void setNome(String nome) {
    if (nome != null && !nome.isEmpty()) {
        this.nome = nome;
    }
}
```

**2. Nomenclatura Clara**
```java
// ❌ Ruim
public class D { }
private int x;
public void proc() { }

// ✓ Bom
public class Cliente { }
private int idade;
public void processarPedido() { }
```

**3. Composição sobre Herança**
```java
// ❌ Evite herança quando composição é mais apropriada
public class Cachorro extends AnimalComCauda { }

// ✓ Prefira composição
public class Cachorro {
    private Cauda cauda;
}
```

**4. Imutabilidade Quando Possível**
```java
// ✓ Classes imutáveis são mais seguras
public final class Ponto {
    private final int x;
    private final int y;
    
    public Ponto(int x, int y) {
        this.x = x;
        this.y = y;
    }
    
    // Apenas getters, sem setters
    public int getX() { return x; }
    public int getY() { return y; }
}
```

**5. Validação no Construtor**
```java
public class Pessoa {
    private String nome;
    private int idade;
    
    public Pessoa(String nome, int idade) {
        if (nome == null || nome.isEmpty()) {
            throw new IllegalArgumentException("Nome não pode ser vazio");
        }
        if (idade < 0 || idade > 150) {
            throw new IllegalArgumentException("Idade inválida");
        }
        this.nome = nome;
        this.idade = idade;
    }
}
```

**6. Use @Override**
```java
// ✓ Sempre use @Override ao sobrescrever métodos
@Override
public String toString() {
    return "MinhaClasse";
}

@Override
public boolean equals(Object obj) {
    // implementação
}
```

**7. Evite Retornar null**
```java
// ❌ Ruim
public List<String> buscarNomes() {
    return null; // Pode causar NullPointerException
}

// ✓ Bom
public List<String> buscarNomes() {
    return new ArrayList<>(); // Retorna lista vazia
}

// ✓ Ou use Optional (Java 8+)
public Optional<Usuario> buscarPorId(int id) {
    // retorna Optional.empty() se não encontrar
}
```

---

## Resumo

A Orientação a Objetos em Java se baseia em:

**4 Pilares Fundamentais:**
1. **Abstração:** Focar no essencial, esconder complexidade
2. **Encapsulamento:** Proteger dados, controlar acesso
3. **Herança:** Reutilizar código, criar hierarquias
4. **Polimorfismo:** Tratar diferentes objetos de forma uniforme

**Elementos Principais:**
- **Classes:** Templates para criar objetos
- **Objetos:** Instâncias de classes
- **Atributos:** Características dos objetos (sempre `private`)
- **Métodos:** Comportamentos dos objetos
- **Construtores:** Inicializam objetos
- **Modificadores:** Controlam visibilidade (`private`, `protected`, `public`)

**Recursos Avançados:**
- **Classes Abstratas:** Base para outras classes, não instanciáveis
- **Interfaces:** Contratos que classes devem seguir
- **Herança:** `extends` para herdar de classes
- **Implementação:** `implements` para implementar interfaces
- **Sobrescrita:** Redefinir métodos com `@Override`

**Boas Práticas:**
- Sempre encapsular atributos (private)
- Usar getters/setters com validação
- Seguir princípios SOLID
- Nomenclatura clara e descritiva
- Composição sobre herança quando apropriado
- Validar no construtor
- Preferir imutabilidade
- Evitar retornar null

A POO permite criar código mais organizado, reutilizável, manutenível e escalável!
