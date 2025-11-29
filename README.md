# 📚 Aula de Java Básico - Noções Fundamentais

Este guia contém exemplos práticos de todos os conceitos básicos de Java que você precisa saber.

---

## 📋 Índice

1. [Tipos Primitivos](#1-tipos-primitivos)
2. [Tipos de Referência (Objetos)](#2-tipos-de-referência-objetos)
3. [Operadores](#3-operadores)
4. [Strings](#4-strings)
5. [Arrays](#5-arrays)
6. [Collections](#6-collections-listas-maps-sets)
7. [Condicionais](#7-condicionais)
8. [Loops](#8-loops)
9. [Métodos/Funções](#9-métodosfunções)
10. [Null Safety](#10-null-safety)
11. [Classes e Objetos](#11-classes-e-objetos)
12. [Resumo Rápido](#12-resumo-rápido)

---

## 1. Tipos Primitivos

### Números Inteiros

```java
byte pequeno = 127;                    // -128 a 127 (8 bits)
short curto = 32000;                   // -32,768 a 32,767 (16 bits)
int numero = 2147483647;               // -2bi a 2bi (32 bits) - MAIS USADO
long grande = 9223372036854775807L;    // muito grande (64 bits) - precisa do L
```

### Números Decimais

```java
float decimal = 3.14f;           // 32 bits - precisa do f
double precisao = 3.14159265359; // 64 bits - MAIS USADO
```

### Outros Tipos

```java
boolean verdadeiro = true;       // true ou false
char letra = 'A';                // um caractere (aspas simples)
```

---

## 2. Tipos de Referência (Objetos)

### String

```java
String nome = "João";    // texto (aspas duplas)
String vazio = "";
String nulo = null;      // sem valor
```

### Wrappers (versão objeto dos primitivos)

```java
Integer numeroObj = 42;        // int como objeto
Double valorObj = 3.14;        // double como objeto
Boolean ativoObj = true;       // boolean como objeto
Long idObj = 123L;             // long como objeto
```

> **Por que usar Wrappers?**
> - Podem ser `null` (primitivos não podem)
> - Necessários em Collections (List, Map, etc.)
> - Usados em entidades JPA no Spring

### Constantes

```java
final int MAXIMO = 100;
final String PAIS = "Brasil";
// MAXIMO = 200; // ERRO! Não pode alterar
```

### Inferência de Tipo (Java 10+)

```java
var texto = "Olá";                       // Java sabe que é String
var num = 42;                            // Java sabe que é int
var lista = new ArrayList<String>();    // Java infere o tipo
```

---

## 3. Operadores

### Aritméticos

```java
int soma = 5 + 3;              // 8
int subtracao = 5 - 3;         // 2
int multiplicacao = 5 * 3;     // 15
int divisao = 5 / 3;           // 1 (inteiro! descarta decimal)
double divisaoReal = 5.0 / 3;  // 1.666... (pelo menos um double)
int resto = 5 % 3;             // 2 (módulo - resto da divisão)
```

### Incremento/Decremento

```java
int x = 5;
x++;    // x = 6
x--;    // x = 5
x += 3; // x = 8
x -= 2; // x = 6
x *= 2; // x = 12
```

### Comparação (retornam boolean)

```java
5 == 5   // true  (igual)
5 != 3   // true  (diferente)
5 > 3    // true  (maior)
5 < 3    // false (menor)
5 >= 5   // true  (maior ou igual)
5 <= 3   // false (menor ou igual)
```

### Lógicos

```java
true && false   // false (AND - E)
true || false   // true  (OR - OU)
!true           // false (NOT - NEGAÇÃO)
```

---

## 4. Strings

### Concatenação

```java
String nome = "João";
String sobrenome = "Silva";
String completo = nome + " " + sobrenome;  // "João Silva"
```

### Métodos Úteis

```java
nome.length();                    // 4
nome.toUpperCase();               // "JOÃO"
nome.toLowerCase();               // "joão"
nome.contains("oã");              // true
nome.startsWith("Jo");            // true
nome.endsWith("ão");              // true
nome.substring(0, 2);             // "Jo"
nome.replace("o", "0");           // "J0ã0"
"  oi  ".trim();                  // "oi"
```

### Split e Join

```java
String[] partes = "a,b,c".split(",");    // ["a", "b", "c"]
String junto = String.join("-", partes);  // "a-b-c"
```

### ⚠️ Comparando Strings

> **NUNCA use `==` para comparar Strings!**

```java
String s1 = "João";
String s2 = "João";
String s3 = new String("João");

s1.equals(s2);               // true ✅
s1.equals(s3);               // true ✅
s1 == s2;                    // true (pool de strings)
s1 == s3;                    // FALSE! ❌ (objetos diferentes)
s1.equalsIgnoreCase("JOÃO"); // true (ignora maiúsculas)
```

### String Formatada

```java
String msg = String.format("Olá, %s! Idade: %d, Valor: %.2f", nome, 25, 3.14159);
// "Olá, João! Idade: 25, Valor: 3.14"
```

### Text Block (Java 15+)

```java
String html = """
    <html>
        <body>Olá</body>
    </html>
    """;
```

---

## 5. Arrays

### Declaração e Inicialização

```java
int[] numeros = {1, 2, 3, 4, 5};
String[] nomes = {"Ana", "Bob", "Carlos"};

// Com tamanho fixo (valor padrão 0)
int[] vetor = new int[5];
```

### Acessando Elementos

> ⚠️ **O índice começa em 0!**

```java
numeros[0];      // 1 (primeiro)
numeros[4];      // 5 (último)
numeros[0] = 100; // altera o primeiro
numeros.length;   // 5 (tamanho)
```

### Percorrendo

```java
// For tradicional
for (int i = 0; i < nomes.length; i++) {
    System.out.println(nomes[i]);
}

// For-each (mais simples)
for (String nome : nomes) {
    System.out.println(nome);
}
```

---

## 6. Collections (Listas, Maps, Sets)

### ArrayList - Lista Dinâmica

```java
List<String> nomes = new ArrayList<>();
nomes.add("Ana");
nomes.add("Bob");
nomes.add("Carlos");

nomes.get(0);           // "Ana"
nomes.size();           // 3
nomes.contains("Bob");  // true
nomes.remove("Bob");    // remove
nomes.set(0, "Amanda"); // substitui índice 0
```

### Inicialização Rápida

```java
List<String> imutavel = List.of("X", "Y", "Z");  // não pode modificar!
List<String> mutavel = new ArrayList<>(List.of("A", "B", "C"));
```

### HashMap - Chave/Valor

```java
Map<String, Integer> idades = new HashMap<>();
idades.put("João", 25);
idades.put("Maria", 30);
idades.put("Pedro", 35);

idades.get("João");          // 25
idades.containsKey("Maria"); // true
idades.keySet();             // todas as chaves
idades.values();             // todos os valores
idades.remove("Pedro");      // remove

// Percorrendo
for (Map.Entry<String, Integer> entry : idades.entrySet()) {
    System.out.println(entry.getKey() + " -> " + entry.getValue());
}
```

### HashSet - Valores Únicos

```java
Set<String> unicos = new HashSet<>();
unicos.add("A");
unicos.add("B");
unicos.add("A");  // ignorado! já existe
unicos.add("C");

unicos.size();        // 3 (não 4!)
unicos.contains("A"); // true
```

---

## 7. Condicionais

### if-else

```java
int idade = 18;

if (idade >= 18) {
    System.out.println("Maior de idade");
} else if (idade >= 16) {
    System.out.println("Pode votar");
} else {
    System.out.println("Menor de idade");
}
```

### Operador Ternário

```java
String status = idade >= 18 ? "Adulto" : "Menor";
```

### Switch Tradicional

```java
int dia = 3;
switch (dia) {
    case 1:
        System.out.println("Domingo");
        break;
    case 2:
        System.out.println("Segunda");
        break;
    case 3:
        System.out.println("Terça");
        break;
    default:
        System.out.println("Outro dia");
}
```

### Switch Moderno (Java 14+)

```java
String nomeDia = switch (dia) {
    case 1 -> "Domingo";
    case 2 -> "Segunda";
    case 3 -> "Terça";
    case 4 -> "Quarta";
    case 5 -> "Quinta";
    case 6 -> "Sexta";
    case 7 -> "Sábado";
    default -> "Inválido";
};
```

---

## 8. Loops

### For Tradicional

```java
for (int i = 0; i < 5; i++) {
    System.out.println(i);  // 0, 1, 2, 3, 4
}
```

### For-each

```java
List<String> frutas = List.of("Maçã", "Banana", "Laranja");
for (String fruta : frutas) {
    System.out.println(fruta);
}
```

### While

```java
int i = 0;
while (i < 3) {
    System.out.println(i);
    i++;
}
```

### Do-While

> Executa **pelo menos uma vez**

```java
int j = 0;
do {
    System.out.println(j);
    j++;
} while (j < 3);
```

### Break e Continue

```java
for (int n = 0; n < 10; n++) {
    if (n == 3) {
        continue;  // pula para próxima iteração
    }
    if (n == 6) {
        break;     // sai do loop
    }
    System.out.println(n);  // 0, 1, 2, 4, 5
}
```

---

## 9. Métodos/Funções

### Método sem Retorno (void)

```java
public static void imprimir(String msg) {
    System.out.println(msg);
}
```

### Método com Retorno

```java
public static int somar(int a, int b) {
    return a + b;
}
```

### Método com Múltiplos Parâmetros

```java
public static double calcular(double valor, double taxa, int meses) {
    return valor * taxa * meses;
}
```

### Método que Retorna Boolean

```java
public static boolean ehPar(int numero) {
    return numero % 2 == 0;
}
```

### Método Recursivo

```java
public static int fatorial(int n) {
    if (n <= 1) return 1;
    return n * fatorial(n - 1);
}
```

### Chamando Métodos

```java
imprimir("Olá, mundo!");
int resultado = somar(5, 3);        // 8
double calc = calcular(1000, 0.05, 12);
boolean par = ehPar(4);             // true
int fat = fatorial(5);              // 120
```

---

## 10. Null Safety

### Verificação Manual

```java
String nome = null;

if (nome != null) {
    System.out.println(nome.length());
} else {
    System.out.println("nome é null!");
}
```

### Optional (Java 8+)

```java
Optional<String> optNome = Optional.ofNullable(nome);

// Verificar se tem valor
optNome.isPresent();              // false

// Valor padrão se for null
String resultado = optNome.orElse("Sem nome");

// Com valor presente
Optional<String> optValor = Optional.of("João");
optValor.get();                   // "João"

// Executar só se tiver valor
optValor.ifPresent(v -> System.out.println(v));

// Map - transforma o valor se presente
String maiusculo = optValor.map(String::toUpperCase).orElse("");
```

---

## 11. Classes e Objetos

### Definindo uma Classe

```java
class Pessoa {
    // Atributos (privados por encapsulamento)
    private String nome;
    private int idade;
    private String email;

    // Construtor padrão (vazio)
    public Pessoa() {
    }

    // Construtor com parâmetros
    public Pessoa(String nome, int idade) {
        this.nome = nome;
        this.idade = idade;
    }

    // Construtor completo
    public Pessoa(String nome, int idade, String email) {
        this.nome = nome;
        this.idade = idade;
        this.email = email;
    }

    // GETTERS - retornam o valor
    public String getNome() {
        return nome;
    }

    public int getIdade() {
        return idade;
    }

    public String getEmail() {
        return email;
    }

    // SETTERS - alteram o valor
    public void setNome(String nome) {
        this.nome = nome;
    }

    public void setIdade(int idade) {
        if (idade >= 0) {  // validação
            this.idade = idade;
        }
    }

    public void setEmail(String email) {
        this.email = email;
    }

    // Método da classe
    public void apresentar() {
        System.out.println("Olá, sou " + nome + " e tenho " + idade + " anos.");
    }

    // Verifica se é maior de idade
    public boolean ehMaiorDeIdade() {
        return idade >= 18;
    }

    // toString - representação em texto
    @Override
    public String toString() {
        return "Pessoa{nome='" + nome + "', idade=" + idade + ", email='" + email + "'}";
    }
}
```

### Usando a Classe

```java
// Construtor vazio + setters
Pessoa p1 = new Pessoa();
p1.setNome("João");
p1.setIdade(25);

// Construtor com parâmetros
Pessoa p2 = new Pessoa("Maria", 30);
p2.apresentar();  // "Olá, sou Maria e tenho 30 anos."

// Construtor completo
Pessoa p3 = new Pessoa("Pedro", 35, "pedro@email.com");
System.out.println(p3);  // Pessoa{nome='Pedro', idade=35, email='pedro@email.com'}
```

---

## 12. Resumo Rápido

### Tipos Primitivos

| Tipo | Exemplo | Descrição |
|------|---------|-----------|
| `int` | `42` | Números inteiros |
| `long` | `123L` | Inteiros grandes |
| `double` | `3.14` | Números decimais |
| `float` | `3.14f` | Decimais (menos precisão) |
| `boolean` | `true/false` | Verdadeiro/Falso |
| `char` | `'A'` | Um caractere |
| `byte` | `127` | Inteiro pequeno |
| `short` | `32000` | Inteiro médio |

### Tipos de Referência

| Tipo | Exemplo | Descrição |
|------|---------|-----------|
| `String` | `"texto"` | Texto |
| `Integer` | `42` | int como objeto |
| `List<T>` | `ArrayList` | Lista ordenada |
| `Map<K,V>` | `HashMap` | Chave/Valor |
| `Set<T>` | `HashSet` | Valores únicos |

### Operadores

| Categoria | Operadores |
|-----------|------------|
| Aritméticos | `+` `-` `*` `/` `%` |
| Comparação | `==` `!=` `>` `<` `>=` `<=` |
| Lógicos | `&&` `\|\|` `!` |
| Atribuição | `=` `+=` `-=` `*=` `/=` |

### Loops

| Tipo | Uso |
|------|-----|
| `for` | Quando sabe quantas vezes |
| `for-each` | Percorrer coleções |
| `while` | Enquanto condição for true |
| `do-while` | Executa pelo menos uma vez |
| `break` | Sai do loop |
| `continue` | Pula iteração |

### Métodos

```java
public static tipo nome(parametros) {
    return valor;
}
```
- `void` = sem retorno

### Classes

- **Atributos**: `private` (encapsulamento)
- **Construtores**: inicializam objetos
- **Getters**: retornam valores
- **Setters**: alteram valores
- **Métodos**: comportamentos

---
