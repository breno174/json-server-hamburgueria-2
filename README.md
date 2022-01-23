# Introdução:

Essa é uma API, que tem o intuito de mostrar alguns dados sobre jogos famosos de epoca, entre 2003 e 2008. Nela é possivel ver uma lista desses jogos e interagir com outros jogadores da epoca através do forum.

## Endpoints

### Login

Vai retornar uma lista de usuario já cadastrados dentro da plataforma.

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

### Interação com a API

Vamos listar nosso forum para interagir na comunidade;
`GET /forum: são listados todas os assuntos debatidos dentro da plataforma`

```json
[
  {
    "debate": "canudos de papel",
    "descrição": "pesquisa pro meu TCC, oque vocês acham dos canudos de papel e como estão sendo utilizados hoje?",
    "comentarios": [
      {
        "titular": "francisco",
        "exposicao": "acho muito util, porém a duração de vida dentro dos milk shakes acaba muito rapido, tanto que não consigo terminar de beber um todo por o canudo já se derfazer no meio tempo"
      },
      {
        "titular": "fernando",
        "exposicao": "salva tartarugas, francisco é chato"
      }
    ],
    "id": 1
  }
]
```

Agora para pegar os jogos que são visualizados;

`GET /games: Mostra a lista de jogos que obtiveram fama entre 2003 - 2008`

```json
[
  {
    "name": "black",
    "categoria": "tiro - 1° pessoa",
    "idade": "+18"
  },
  {
    "name": "pes 2008",
    "categoria": "futebol - 3° pessoa",
    "idade": "+10"
  },
  {
    "name": "shadow of the colossus",
    "categoria": "aventura - 1° pessoa",
    "idade": "+16"
  },
  {
    "name": "warcraft III",
    "categoria": "rpg - 3° pessoa",
    "idade": "+14"
  }
]
```

### Cadastro

Para esse metodo deve passar um corpo JSON com email e senha para ser registrado;

`POST /register: pode criar novos usuarios para interagir no forum da plataforma`

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

### update;

Com o `acessToken` do usuário, ele irá lhe permitir que possa interagir no forúm criando novos temas para debates ou comentar em debates já criados por outros usuarios.

Este deve conter um corpo parecido com esse abaixo ao enviar os dados;

`POST /forum: criado novos debates no forum da plataforma`

```json
{
  "debate": "qualquer",
  "descrição": "descriçao qualquer?",
  "comentarios": [
    {
      "titular": "alguem",
      "exposicao": "texto qualquer"
    }
  ]
}
```

Perceba que ao fazer o metodo `GET` um "ID" é mostrado para cada debate, logo abaixo;

```json
  <...>
  "id": "numero qualquer"
  <...>
```

Ao fazer o metodo `POST` nos debates, logo você vera que seu debate recebera uma nova numeração para identificalo.

> E é isso! Vamos debater sobre jogos nostálgicos

# Happy codin!!!
