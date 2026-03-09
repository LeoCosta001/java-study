# Anki Flashcards - Java

Cards gerados a partir das anotações de estudo. Gerenciados via Cursor AI (skill: `anki-deck-manager`).

## Arquivos

| Arquivo | Tipo | Cards | Conteúdo |
|---------|------|-------|----------|
| `java--basic.txt` | Pergunta/Resposta | 51 | Definições, comparações, conceitos |
| `java--cloze.txt` | Preencher Lacuna | 66 | Sintaxe, métodos, código |

## Como Importar no Anki

### Primeiro Import

1. Abrir **Anki**
2. Clicar em **Criar Deck** → nomear como `Java`
3. **File → Import**
4. Selecionar o arquivo `.txt`

### Para `java--basic.txt`

1. File → Import → selecionar `java--basic.txt`
2. **Note type**: Basic
3. **Deck**: Java (ou criar sub-deck `Java::Conceitos`)
4. **Campos**: Field 1 = Front, Field 2 = Back
5. Tags já são importadas automaticamente (coluna 3)
6. Clicar em **Import**

### Para `java--cloze.txt`

1. File → Import → selecionar `java--cloze.txt`
2. **Note type**: Cloze
3. **Deck**: Java (ou criar sub-deck `Java::Sintaxe`)
4. O tipo Cloze é detectado automaticamente pela coluna 1
5. Clicar em **Import**

### Re-importar (Atualizar)

Ao re-importar, o Anki detecta cards existentes e:
- **Adiciona** cards novos
- **Atualiza** cards modificados
- **Não remove** cards deletados do arquivo (segurança)

## Tópicos Cobertos

- `java::tipos-primitivos` - Tipos primitivos e casting
- `java::wrapper-classes` - Wrapper classes, autoboxing
- `java::lists` - ArrayList, LinkedList
- `java::maps` - HashMap, TreeMap
- `java::poo` - POO, herança, interfaces, SOLID
- `java::streams` - API de Streams
- `java::lambdas` - Lambdas e interfaces funcionais
- `java::imports` - Sistema de imports e packages
- `java::http` - Requisições HTTP
- `java::operadores` - Operadores e diferenças com TS
- `java::big-o` - Notação Big O e complexidade

## Gerenciamento

Para atualizar os cards, peça ao Cursor AI:
- "Atualize os cards do Anki com as novas anotações"
- "Adicione cards sobre [tópico] no deck Java"
- "Gere cards cloze para o arquivo [arquivo.md]"
