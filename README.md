# Baozi Store API

API REST para gerenciamento de clientes, produtos e pedidos de uma loja fictícia de pão chinês (Baozi Store).

Trabalho da disciplina de Desenvolvimento Web Back-End.

**Autora:** Lorrane — **RU:** 4918902

---

## Tecnologias

- Java 17
- Spring Boot 3
- Spring Data JPA
- Banco de dados H2 (em memória)
- Maven
- Postman

---

## Como rodar

```bash
mvn spring-boot:run
```

A API sobe em `http://localhost:8080`.

---

## Entidades

### Cliente
| Campo | Tipo |
|---|---|
| id | Long |
| nome | String |
| clienteDesde | LocalDate |

### Produto
| Campo | Tipo |
|---|---|
| id | Long |
| nome | String |
| preco | BigDecimal |
| estoque | Boolean |

### Pedido
| Campo | Tipo |
|---|---|
| id | Long |
| clienteId | Long |
| produtoId | Long |
| quantidade | Integer |

---

## Endpoints

### Cliente — `/clientes`
| Método | Rota | Descrição |
|---|---|---|
| POST | /clientes | Cria um cliente |
| GET | /clientes | Lista todos os clientes |
| GET | /clientes/{id} | Busca um cliente pelo id |
| PUT | /clientes/{id} | Atualiza um cliente |
| DELETE | /clientes/{id} | Apaga um cliente |

### Produto — `/produtos`
| Método | Rota | Descrição |
|---|---|---|
| POST | /produtos | Cria um produto |
| GET | /produtos | Lista todos os produtos |
| GET | /produtos/{id} | Busca um produto pelo id |
| PUT | /produtos/{id} | Atualiza um produto |
| DELETE | /produtos/{id} | Apaga um produto |

### Pedido — `/pedidos`
| Método | Rota | Descrição |
|---|---|---|
| POST | /pedidos | Cria um pedido |
| GET | /pedidos | Lista todos os pedidos |
| GET | /pedidos/{id} | Busca um pedido pelo id |
| PUT | /pedidos/{id} | Atualiza um pedido |
| DELETE | /pedidos/{id} | Apaga um pedido |

---

## Estrutura do projeto

```
baozi-store/
├── pom.xml
└── src/main/java/com/baozi/store/
    ├── BaoziStoreApplication.java
    ├── model/
    ├── repository/
    └── controller/
```
