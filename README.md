# Introdução:

Essa é uma API, que armazena os produtos de um ecomerce, nela o usuario pode interagir para adicionar ao carrinho de compras os produtos que estão disponiveis na vitrine, contanto que esteja logado. Os dados do usuario sempre que for logar estarão guardados caso resolver efetuar a finalização da compra.

## Endpoints

### Login

Vai retornar uma lista de usuarios já cadastrados dentro da plataforma.

`GET /user: mostrar os usuarios cadastrados dentro da plataforma`

```json
[
  {
    "email": "ivangilhom@mail.com",
    "password": "$2a$10$9UaL/4ENcwDfAU6qr.rVf.X5lcoPRouHzsqkVEZYV4Gx.W8m7JSIu",
    "name": "ivan",
    "age": 38,
    "id": 6
  },
  {
    "email": "marcelo@mail.com",
    "password": "$2a$10$I4dNmZfH/k39xZmGBXlta.7XCbdkHlSlgdjLh7J5G1w7sX1/XOqNK",
    "name": "marcelo",
    "age": 30,
    "id": 7
  }
]
```

### Cadastro

Para esse metodo deve passar um corpo JSON com email e senha para ser registrado;

`POST /register: pode criar novos usuarios para interagir com a vitrine da plataforma`

```json
{
  "email": "ivangilhom@mail.com",
  "password": "654321",
  "name": "ivan",
  "age": 38
}
```

A resposta ira voltar algo parecido com isso;

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Iml2YW5naWxob21AbWFpbC5jb20iLCJpYXQiOjE2NDI0NDM1MzIsImV4cCI6MTY0MjQ0NzEzMiwic3ViIjoiNiJ9.f4RYeyCJR7cyWFpkNIIspsEhT8BPVpUe-7d677izxfw",
  "user": {
    "email": "ivangilhom@mail.com",
    "name": "ivan",
    "age": 38,
    "id": 6
  }
}
```

Com o `acessToken` do usuário, ele irá lhe permitir que possa interagir na plataforma adicionando novos produtos ao carrinho do usuario para futuras compras.

### Interação com a API

Vamos listar os produtos armazenados na vitrine;
Todos os produtos tem um `Id` que é utilizado como um marcador para aquele produto ser unico.

`GET /produtos: são listados todos os produtos disponiveis para venda, mas o usuario tem que estar logado para interagir e visualizar a vitrine`

> Deve retornar um objeto com essas caracteristicas;

```json
{
  "titulo": "Coca Cola",
  "categoria": "Bebidas",
  "imagem": "https://i.ibb.co/fxCGP7k/coca-cola.png",
  "preco": 7,
  "id": 2
}
```

### Metodo para adicionar produtos ao carrinho:

`Post /carrinho: esse metodo nos permite adicionar o produto selecionado ao nosso carrinho`
Nesse metodo é necessario passar o `accessToken` de autenticação do usuario logado e o id do usuario, com isso o produto selecionado ira entrar na lista de produtos a venda com o marcador `userId` que é gerado automaticamente pela API para identificar que aquele produto agora pertence aquele usuario.

Deve retornar um corpo igual a esse;

```json
{
  "titulo": "Coca Cola",
  "categoria": "Bebidas",
  "imagem": "https://i.ibb.co/fxCGP7k/coca-cola.png",
  "preco": 7,
  "userId": 2,
  "id": 2
}
```

> Para o usário com ID=2 o produto recebera o `userId` igual ao ID do usuário.

### Metodo para listar produtos ao carrinho que pertence ao usuário:

`GET /carrinho: esse método ira listar todos os produtos que pertecem àquele usuário`
O usuario deve estar logado. Nesse metodo é necessario passar o `accessToken` de autenticação do usuario logado e o id do usuario, para identificar apenas os produtos que contem o `userID` igual ao ID do usuário logado.

> end point: `http://localhost:3001/carrinho?userId=3`

```json
[
  {
    "titulo": "Big Kenzie",
    "categoria": "Sanduiches",
    "preco": 18,
    "imagem": "https://i.ibb.co/FYBKCwn/big-kenzie.png",
    "userId": 3,
    "id": 25
  },
  {
    "titulo": "Combo Kenzie",
    "categoria": "Combo",
    "preco": 26,
    "imagem": "https://e7.pngegg.com/pngimages/602/53/png-clipart-hamburger-french-fries-fizzy-drinks-chicken-sandwich-veggie-burger-fried-chicken.png",
    "userId": 3,
    "id": 26
  }
]
```

### Metodo para deletar produtos do carrinho:

O usuario deve estar logado. Nesse metodo é necessario passar o `accessToken` de autenticação do usuario porém não precisamos do id do usuário, pois iremos deletar o produto do carrinho a partir do ID do produto.
`DELETE /carrinho/id`

> E é isso! Vamos ver nosso Ecomerce.

# Happy codin!!!
