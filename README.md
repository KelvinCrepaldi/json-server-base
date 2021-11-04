# json-server-base

Esse é o repositório com a base de JSON-Server + JSON-Server-Auth já configurada, feita para ser usada no desenvolvimento das API's nos Capstones do Q2. https://github.com/Kenzie-Academy-Brasil-Developers/json-server-base <br />
Estou usando para entregar a atividade da aula "5A04 - Atividade - JSON-Server do início ao Deploy"

# Endpoints

Assim como a documentação do JSON-Server-Auth traz (https://www.npmjs.com/package/json-server-auth), existem 3 endpoints que podem ser utilizados para cadastro e 2 endpoints que podem ser usados para login.

Alem dessas foram criados mais dois, sendo list e cart.

### Cadastro

POST /register <br/>
POST /signup <br/>
POST /users <br/>

Qualquer um desses 3 endpoints irá cadastrar o usuário na lista de "Users", sendo que os campos obrigatórios são os de email e password. Você pode ficar a vontade para adicionar qualquer outra propriedade no corpo do cadastro dos usuários.

### Login

POST /login <br/>
POST /signin <br/>

Qualquer um desses 2 endpoints pode ser usado para realizar login com um dos usuários cadastrados na lista de "Users"

### List

Rota na qual todos os usuários tem acesso a leitura, e apenas usuarios logados tem acesso a escrita.

POST /list - Para criar um item na lista.

`Exemplo de requisição`

```json
{
  "name": "item",
  "price": "1,00",
  "userId": 2
}
```

`Resposta - 201`

```json
{
  "name": "item",
  "price": "1,00",
  "userId": 2,
  "id": 4
}
```

GET /list - Para acessar os itens da lista de itens.

`Exemplo de resposta - 200`

```json
[
  {
    "id": 1,
    "name": "item",
    "price": "1,00"
  }
]
```

### Cart

Rota na qual apenas usuários logados tem acesso a leitura e escrita.

POST /cart - Para criar um item na lista.

`Exemplo de requisição`

```json
{
  "name": "meia",
  "price": "5,00",
  "userId": 2
}
```

`Resposta - 201`

```json
{
  "name": "meia",
  "price": "5,00",
  "userId": 2,
  "id": 8
}
```

GET /cart - Para acessar os itens da lista de itens.

`Exemplo de resposta - 200`

```json
[
  {
    "name": "meia",
    "price": "5,00",
    "userId": 2,
    "id": 8
  }
]
```

Para acessar itens do carrinho de um usuário específico use:
`/users/id?_embed=cart`
onde "id" é o numero de identificação do usuário.

`Formato da resposta - 200`

```json
{
  "email": "pinguim@hotmail.com",
  "password": "$2a$10$SqmraCQ8iC5Nu7/jJJHBke7WTt6H6cnFT0KqdOeV3GV1TQq6n8GY.",
  "name": "pinguim",
  "id": 2,
  "cart": [
    {
      "name": "short",
      "price": "39,99",
      "userId": 2,
      "id": 2
    },
    {
      "name": "luva",
      "price": "9,99",
      "userId": 2,
      "id": 2
    },
    {
      "name": "short",
      "price": "39,99",
      "userId": 2,
      "id": 3
    },
    {
      "name": "meia",
      "price": "9,99",
      "userId": 2,
      "id": 4
    },
    {
      "name": "teste",
      "price": "9,99",
      "userId": 2,
      "id": 5
    }
  ]
}
```

### Possivel erro de POST:

`Resposta - 403`

```json
"Private resource creation: request body must have a reference to the owner id"
```

É necessario inserir o id do usuario logado, userId.
