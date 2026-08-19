# Baozi Store API

Trabalho de Desenvolvimento Web Back-End — API REST simples com Spring Boot para controlar clientes, produtos e pedidos de uma loja de pão chinês.

**Aluna:** Lorrane — **RU:** 4918902

---

## Passo a passo — Eclipse (do zero)

### Passo 1 — Instalar o Java (JDK 17)

1. Acesse https://adoptium.net/pt-BR/temurin/releases/
2. Baixe a versão **17 (LTS)** para o seu sistema operacional (Windows/Mac/Linux).
3. Instale normalmente, clicando em "Avançar" até o fim.

### Passo 2 — Instalar o Eclipse

1. Acesse https://www.eclipse.org/downloads/
2. Baixe o **Eclipse IDE for Enterprise Java and Web Developers** (essa versão já vem preparada para projetos Spring/Maven).
3. Instale e abra o Eclipse.
4. Na primeira tela, ele vai pedir uma pasta de "workspace" — pode deixar a sugestão padrão e clicar em "Launch".

### Passo 3 — Descompactar o projeto

1. Baixe o arquivo `baozi-store.zip` que te enviei.
2. Clique com o botão direito nele e escolha **Extrair aqui** (ou "Extrair tudo", no Windows).
3. Guarde a pasta `baozi-store` em um lugar fácil de achar, por exemplo `Documentos\baozi-store`.

### Passo 4 — Importar o projeto no Eclipse

1. No Eclipse, vá no menu **File > Import...**
2. Vai abrir uma janela. Escolha **Maven > Existing Maven Projects** e clique em **Next**.
3. Em "Root Directory", clique em **Browse...** e selecione a pasta `baozi-store` (a que tem o arquivo `pom.xml` dentro).
4. O Eclipse vai mostrar o projeto encontrado com uma caixinha marcada. Deixe marcado e clique em **Finish**.
5. Aguarde. No canto inferior direito vai aparecer uma barra de progresso baixando as dependências do projeto — a primeira vez demora alguns minutos (precisa de internet).

Se aparecer algum "X" vermelho de erro estranho no projeto depois de importar, clique com o botão direito no projeto (no painel esquerdo, chamado "Project Explorer") e vá em **Maven > Update Project...**, deixe a opção "Force Update of Snapshots/Releases" marcada e clique em **OK**.

### Passo 5 — Rodar a aplicação

1. No **Project Explorer** (painel da esquerda), abra as pastas até chegar em:
   `baozi-store > src/main/java > com.baozi.store`
2. Clique com o **botão direito** no arquivo `BaoziStoreApplication.java`.
3. Escolha **Run As > Java Application**.
4. Aguarde. Vai aparecer bastante texto na aba **Console** (embaixo). Quando aparecer algo como:
   ```
   Baozi Store API rodando em http://localhost:8080
   ```
   significa que deu certo! A API está no ar.

**Importante:** deixe essa janela do Eclipse aberta e rodando enquanto for testar no Postman. Se você fechar ou clicar no quadrado vermelho (Stop), a API para.

---

## Passo a passo — Testando no Postman

### Passo 1 — Instalar o Postman

Baixe em https://www.postman.com/downloads/ e instale (pode usar sem criar conta, só clicar em "Skip" / "Pular" quando pedir login).

### Passo 2 — Criar o cliente (POST)

1. Abra o Postman e clique em **New > HTTP Request** (ou no "+" para abrir uma nova aba).
2. No menu suspenso ao lado da URL, troque de `GET` para **POST**.
3. Na barra de URL, digite:
   ```
   http://localhost:8080/clientes
   ```
4. Clique na aba **Body** (logo abaixo da URL), escolha a opção **raw**, e no menu que aparece do lado direito escolha **JSON**.
5. Cole este JSON no corpo (assim já usa seu nome + RU, conforme pedido no enunciado):
   ```json
   {
     "nome": "Lorrane4918902",
     "clienteDesde": "2026-08-19"
   }
   ```
6. Clique no botão azul **Send**.
7. Deve aparecer uma resposta como esta, com status **201 Created**:
   ```json
   {
     "id": 1,
     "nome": "Lorrane4918902",
     "clienteDesde": "2026-08-19"
   }
   ```
8. **Tire o print dessa tela** (mostrando a URL, o Body enviado e a resposta) — esse é um dos prints obrigatórios.

### Passo 3 — Criar o produto (POST)

1. Nova aba no Postman, método **POST**, URL:
   ```
   http://localhost:8080/produtos
   ```
2. Em **Body > raw > JSON**, cole:
   ```json
   {
     "nome": "Baozi - Pão Chinês",
     "preco": 8.50,
     "estoque": true
   }
   ```
3. Clique em **Send**. Resposta esperada (status 201):
   ```json
   {
     "id": 1,
     "nome": "Baozi - Pão Chinês",
     "preco": 8.50,
     "estoque": true
   }
   ```
4. **Tire o print.**

### Passo 4 — Criar o pedido (POST)

1. Nova aba, método **POST**, URL:
   ```
   http://localhost:8080/pedidos
   ```
2. Em **Body > raw > JSON**, use o `id` do cliente e do produto que você acabou de criar (no exemplo acima, ambos são `1`):
   ```json
   {
     "clienteId": 1,
     "produtoId": 1,
     "quantidade": 5
   }
   ```
3. Clique em **Send**. Resposta esperada (status 201):
   ```json
   {
     "id": 1,
     "clienteId": 1,
     "produtoId": 1,
     "quantidade": 5
   }
   ```
4. **Tire o print.**

### Passo 5 — Listar tudo (GET geral)

Para cada entidade, troque o método para **GET** e mande a mesma URL sem nada no Body:

- `GET http://localhost:8080/clientes` → lista todos os clientes
- `GET http://localhost:8080/produtos` → lista todos os produtos
- `GET http://localhost:8080/pedidos` → lista todos os pedidos

**Tire print de pelo menos um desses (ex: listagem geral).**

### Passo 6 — Consultar por ID (GET)

Método **GET**, URL com o id no final, por exemplo:
```
http://localhost:8080/clientes/1
```
Isso deve devolver só o cliente de id 1. **Tire o print.**

### Passo 7 — Apagar (DELETE)

Método **DELETE**, mesma URL com id, por exemplo:
```
http://localhost:8080/pedidos/1
```
Clique em **Send**. A resposta deve vir vazia com status **204 No Content**, o que indica que apagou com sucesso. Se quiser confirmar, faça um GET na mesma URL depois — deve vir **404 Not Found**.

---

## Endpoints da API (para copiar na sua especificação do PDF)

### Cliente — `/clientes`
| Método | Rota | O que faz |
|---|---|---|
| POST | /clientes | Cria um cliente |
| GET | /clientes | Lista todos os clientes |
| GET | /clientes/{id} | Busca um cliente pelo id |
| PUT | /clientes/{id} | Atualiza um cliente (opcional) |
| DELETE | /clientes/{id} | Apaga um cliente |

Campos: `id` (Long, gerado automaticamente), `nome` (String), `clienteDesde` (LocalDate, formato AAAA-MM-DD)

### Produto — `/produtos`
| Método | Rota | O que faz |
|---|---|---|
| POST | /produtos | Cria um produto |
| GET | /produtos | Lista todos os produtos |
| GET | /produtos/{id} | Busca um produto pelo id |
| PUT | /produtos/{id} | Atualiza um produto (opcional) |
| DELETE | /produtos/{id} | Apaga um produto |

Campos: `id` (Long, gerado automaticamente), `nome` (String), `preco` (BigDecimal), `estoque` (Boolean — true/false)

### Pedido — `/pedidos`
| Método | Rota | O que faz |
|---|---|---|
| POST | /pedidos | Cria um pedido |
| GET | /pedidos | Lista todos os pedidos |
| GET | /pedidos/{id} | Busca um pedido pelo id |
| PUT | /pedidos/{id} | Atualiza um pedido (opcional) |
| DELETE | /pedidos/{id} | Apaga um pedido |

Campos: `id` (Long, gerado automaticamente), `clienteId` (Long), `produtoId` (Long), `quantidade` (Integer)

---

## Estrutura do projeto (arquitetura mínima pedida no enunciado)

```
baozi-store/
├── pom.xml
└── src/main/java/com/baozi/store/
    ├── BaoziStoreApplication.java   -> classe principal (main)
    ├── model/                       -> Produto.java, Cliente.java, Pedido.java
    ├── repository/                  -> ProdutoRepository, ClienteRepository, PedidoRepository
    └── controller/                  -> ProdutoController, ClienteController, PedidoController
```

---

## Quer usar MySQL em vez de H2?

O enunciado permite H2, MySQL ou MariaDB — este projeto já vem pronto com **H2** (mais simples, não precisa instalar nada). Se seu professor pedir especificamente MySQL, troque o arquivo `pom.xml` e o `application.properties`:

**No `pom.xml`**, troque a dependência do H2 por:
```xml
<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
    <scope>runtime</scope>
</dependency>
```

**No `application.properties`**, troque as linhas do banco por:
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/baozidb?createDatabaseIfNotExist=true
spring.datasource.username=root
spring.datasource.password=SUA_SENHA_DO_MYSQL
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```
(seria necessário ter o MySQL instalado e rodando na máquina)

---

## Subindo para o GitHub (para o link pedido no PDF)

1. Crie uma conta em https://github.com se ainda não tiver.
2. Clique em **New repository**, dê um nome (ex: `baozi-store-api`) e crie.
3. Na página do repositório, existe um botão **uploading an existing file** — clique nele.
4. Arraste a pasta `baozi-store` inteira (ou todos os arquivos dela) para a área indicada.
5. Clique em **Commit changes**.
6. Copie o link da página do repositório — esse é o link que vai no PDF.
