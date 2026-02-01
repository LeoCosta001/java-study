# Requisições HTTP em Java

Java oferece formas nativas de fazer requisições HTTP. O `HttpClient` (Java 11+) é a forma moderna e recomendada.

## Resumo Rápido

| Método | Quando Usar |
|--------|-------------|
| `HttpClient` | **Recomendado** - Java 11+, moderno e simples |
| `HttpURLConnection` | Java antigo (< 11), código legado |
| Bibliotecas externas | Recursos avançados (OkHttp, Apache HttpClient) |

---

## 1. HttpClient (Java 11+) - Recomendado

### Setup Básico

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
```

### GET Simples

```java
HttpClient client = HttpClient.newHttpClient();

HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://api.exemplo.com/users"))
    .GET()  // GET é o padrão, pode omitir
    .build();

HttpResponse<String> response = client.send(request, 
    HttpResponse.BodyHandlers.ofString());

int statusCode = response.statusCode();  // 200
String body = response.body();           // JSON como String
```

### GET com Headers

```java
HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://api.exemplo.com/users"))
    .header("Authorization", "Bearer seu-token")
    .header("Accept", "application/json")
    .GET()
    .build();
```

### POST com JSON

```java
String json = """
    {
        "nome": "João",
        "email": "joao@email.com"
    }
    """;

HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://api.exemplo.com/users"))
    .header("Content-Type", "application/json")
    .POST(HttpRequest.BodyPublishers.ofString(json))
    .build();

HttpResponse<String> response = client.send(request,
    HttpResponse.BodyHandlers.ofString());
```

### PUT e DELETE

```java
// PUT
HttpRequest putRequest = HttpRequest.newBuilder()
    .uri(URI.create("https://api.exemplo.com/users/1"))
    .header("Content-Type", "application/json")
    .PUT(HttpRequest.BodyPublishers.ofString(json))
    .build();

// DELETE
HttpRequest deleteRequest = HttpRequest.newBuilder()
    .uri(URI.create("https://api.exemplo.com/users/1"))
    .DELETE()
    .build();
```

### Requisição Assíncrona

```java
client.sendAsync(request, HttpResponse.BodyHandlers.ofString())
    .thenApply(HttpResponse::body)
    .thenAccept(System.out::println)
    .join();  // Aguarda conclusão
```

### Timeout

```java
import java.time.Duration;

HttpClient client = HttpClient.newBuilder()
    .connectTimeout(Duration.ofSeconds(10))
    .build();

HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://api.exemplo.com/users"))
    .timeout(Duration.ofSeconds(30))
    .build();
```

---

## 2. Tratamento de Erros

```java
try {
    HttpResponse<String> response = client.send(request,
        HttpResponse.BodyHandlers.ofString());
    
    if (response.statusCode() == 200) {
        System.out.println("Sucesso: " + response.body());
    } else if (response.statusCode() == 404) {
        System.out.println("Não encontrado");
    } else if (response.statusCode() >= 500) {
        System.out.println("Erro no servidor");
    }
    
} catch (IOException e) {
    System.out.println("Erro de conexão: " + e.getMessage());
} catch (InterruptedException e) {
    System.out.println("Requisição interrompida");
    Thread.currentThread().interrupt();
}
```

---

## 3. Trabalhando com JSON

Java não tem suporte nativo a JSON. Use bibliotecas como **Gson** ou **Jackson**.

### Com Gson (Google)

```java
// Adicione ao pom.xml ou baixe o JAR
// <dependency>
//     <groupId>com.google.code.gson</groupId>
//     <artifactId>gson</artifactId>
//     <version>2.10.1</version>
// </dependency>

import com.google.gson.Gson;

// Classe que representa o JSON
class Usuario {
    String nome;
    String email;
    int idade;
}

// JSON → Objeto
Gson gson = new Gson();
Usuario user = gson.fromJson(response.body(), Usuario.class);
System.out.println(user.nome);

// Objeto → JSON
Usuario novoUser = new Usuario();
novoUser.nome = "Maria";
novoUser.email = "maria@email.com";
String json = gson.toJson(novoUser);
```

### Com Jackson

```java
// Adicione ao pom.xml
// <dependency>
//     <groupId>com.fasterxml.jackson.core</groupId>
//     <artifactId>jackson-databind</artifactId>
//     <version>2.15.2</version>
// </dependency>

import com.fasterxml.jackson.databind.ObjectMapper;

ObjectMapper mapper = new ObjectMapper();

// JSON → Objeto
Usuario user = mapper.readValue(response.body(), Usuario.class);

// Objeto → JSON
String json = mapper.writeValueAsString(novoUser);
```

---

## 4. Exemplo Completo

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.time.Duration;

public class ApiClient {
    
    private final HttpClient client;
    private final String baseUrl;
    
    public ApiClient(String baseUrl) {
        this.baseUrl = baseUrl;
        this.client = HttpClient.newBuilder()
            .connectTimeout(Duration.ofSeconds(10))
            .build();
    }
    
    public String get(String endpoint) throws Exception {
        HttpRequest request = HttpRequest.newBuilder()
            .uri(URI.create(baseUrl + endpoint))
            .header("Accept", "application/json")
            .GET()
            .build();
        
        HttpResponse<String> response = client.send(request,
            HttpResponse.BodyHandlers.ofString());
        
        if (response.statusCode() != 200) {
            throw new RuntimeException("Erro: " + response.statusCode());
        }
        
        return response.body();
    }
    
    public String post(String endpoint, String json) throws Exception {
        HttpRequest request = HttpRequest.newBuilder()
            .uri(URI.create(baseUrl + endpoint))
            .header("Content-Type", "application/json")
            .POST(HttpRequest.BodyPublishers.ofString(json))
            .build();
        
        HttpResponse<String> response = client.send(request,
            HttpResponse.BodyHandlers.ofString());
        
        return response.body();
    }
    
    public static void main(String[] args) throws Exception {
        ApiClient api = new ApiClient("https://jsonplaceholder.typicode.com");
        
        // GET
        String users = api.get("/users");
        System.out.println(users);
        
        // POST
        String novoPost = """
            {"title": "Teste", "body": "Conteúdo", "userId": 1}
            """;
        String resultado = api.post("/posts", novoPost);
        System.out.println(resultado);
    }
}
```

---

## 5. HttpURLConnection (Java Antigo)

Use apenas se não puder usar Java 11+.

```java
import java.net.HttpURLConnection;
import java.net.URL;
import java.io.BufferedReader;
import java.io.InputStreamReader;

URL url = new URL("https://api.exemplo.com/users");
HttpURLConnection conn = (HttpURLConnection) url.openConnection();

conn.setRequestMethod("GET");
conn.setRequestProperty("Accept", "application/json");

int status = conn.getResponseCode();

BufferedReader reader = new BufferedReader(
    new InputStreamReader(conn.getInputStream()));

StringBuilder response = new StringBuilder();
String linha;
while ((linha = reader.readLine()) != null) {
    response.append(linha);
}
reader.close();
conn.disconnect();

System.out.println(response.toString());
```

---

## Tabela de Métodos HTTP

| Método | Uso | Tem Body |
|--------|-----|----------|
| `GET` | Buscar dados | Não |
| `POST` | Criar recurso | Sim |
| `PUT` | Atualizar recurso (completo) | Sim |
| `PATCH` | Atualizar recurso (parcial) | Sim |
| `DELETE` | Remover recurso | Geralmente não |

---

## Status Codes Comuns

| Código | Significado |
|--------|-------------|
| `200` | OK - Sucesso |
| `201` | Created - Recurso criado |
| `204` | No Content - Sucesso sem retorno |
| `400` | Bad Request - Erro na requisição |
| `401` | Unauthorized - Não autenticado |
| `403` | Forbidden - Sem permissão |
| `404` | Not Found - Não encontrado |
| `500` | Internal Server Error - Erro no servidor |

---

## Dicas

1. **Reutilize o HttpClient** - Crie uma instância e use em várias requisições
2. **Configure timeouts** - Evite que requisições fiquem penduradas
3. **Trate erros** - Sempre verifique o status code
4. **Use bibliotecas para JSON** - Gson é simples, Jackson é mais completo
5. **Considere bibliotecas externas** - Para casos complexos, OkHttp ou Retrofit facilitam

---

## Comparação: Java vs JavaScript/TypeScript

| Java (HttpClient) | JavaScript (fetch) |
|-------------------|-------------------|
| `HttpClient.newHttpClient()` | - |
| `HttpRequest.newBuilder()` | `fetch(url, options)` |
| `.uri(URI.create(url))` | Primeiro parâmetro |
| `.header("key", "value")` | `headers: { key: value }` |
| `.POST(BodyPublishers.ofString(json))` | `method: 'POST', body: json` |
| `client.send(request, ...)` | `await fetch(...)` |
| `response.body()` | `await response.json()` |
