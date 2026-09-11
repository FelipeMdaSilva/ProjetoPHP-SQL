# API de Produtos - Integração PHP + MySQL

Projeto simples de backend em PHP puro para cadastro e listagem de produtos, utilizando PDO para conexão com o banco de dados.

## 📋 Sobre o projeto

Este projeto é uma API REST básica que permite:

- **Cadastrar** um novo produto no banco de dados (via `POST`)
- **Listar** todos os produtos cadastrados, ordenados por ID (via `GET`)

A comunicação é feita em formato **JSON**, tanto no envio quanto no recebimento dos dados.

## 🗂️ Estrutura do projeto

```
├── conexao.php     # Configurações de conexão com o banco (NÃO versionado)
└── produtos.php    # Rotas de cadastro (POST) e listagem (GET) de produtos
└── api-cep.py      # Teste de API
```

> ⚠️ O arquivo `conexao.php` contém informações sensíveis (host, usuário, senha, nome do banco) e por isso está incluído no `.gitignore`, não sendo enviado ao repositório.

## ⚙️ Tecnologias utilizadas

- PHP (nativo, sem frameworks)
- PDO (PHP Data Objects) para acesso ao banco de dados
- PostgreSQL

## 🔌 Como funciona

O arquivo `produtos.php` verifica o método HTTP da requisição (`$_SERVER["REQUEST_METHOD"]`) e executa a ação correspondente:

### `POST` - Cadastrar produto

Recebe um JSON no corpo da requisição com os campos `nome` e `preco`, e insere um novo registro na tabela `produtos`.

**Exemplo de requisição:**
```json
{
  "nome": "Teclado Mecânico",
  "preco": 250.00
}
```

**Resposta:**
```json
{
  "Mensagem": "Produto cadastrado com sucesso!"
}
```

### `GET` - Listar produtos

Retorna todos os produtos cadastrados, em formato JSON, ordenados por `id`.

**Resposta:**
```json
[
  {
    "id": 1,
    "nome": "Teclado Mecânico",
    "preco": "250.00"
  }
]
```

## 🛠️ Configuração do banco de dados

Crie um arquivo `conexao.php` na raiz do projeto com o seguinte conteúdo (ajuste conforme seu ambiente):

```php
<?php

$host = "localhost";
$dbname = "nome_do_banco";
$user = "usuario";
$senha = "senha";

$pdo = new PDO(
    "pgsql:host=$host;port=5432;dbname=$banco",
    $usuario,
    $senha
);
```

E crie a tabela `produtos` no seu banco:

```sql
CREATE TABLE produtos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    preco DECIMAL(10,2) NOT NULL
);
```

## ▶️ Como rodar o projeto

1. Clone o repositório
2. Crie o arquivo `conexao.php` com suas credenciais (veja seção acima)
3. Inicie um servidor local, por exemplo:
```bash
   php -S localhost:8000
```
4. Faça as requisições para `http://localhost:8000/produtos.php`

## 📌 Próximos passos (ideias de melhoria)

- Adicionar validação dos dados recebidos
- Implementar métodos `PUT` (atualizar) e `DELETE` (remover)
- Adicionar tratamento de erros mais detalhado
- Criar autenticação para proteger as rotas

## 📄 Licença

Este projeto está sob a licença MIT. Sinta-se livre para usar e modificar.