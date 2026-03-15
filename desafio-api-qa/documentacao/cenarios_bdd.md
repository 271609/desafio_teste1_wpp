# Cenários BDD
Cenários de Testes

1. Feature: Criação de Post
Cenário: Criar Post

Dado que envio um payload válido para criação de post
Quando envio a requisição POST /posts
Exemplo de Body:

{
  "title": "Criando post com sucesso",
  "body": "Este é um exemplo de criação de post para testes de QA.",
  "userId": 5
}
Então devo receber status 201 com um id gerado.

Cenário: Criar Post com Payload Inválido
Dado que envio um payload sem o campo userId
Quando envio POST /posts
Então o comportamento é inesperado, pois a API não valida campos.


2- Feature de Consultas de Posts

Cenário: Consultar Lista de Posts
Dado que envio uma requisição GET /posts
Então a API deve retornar a lista completa de Posts.

Cenário: Consultar Post por ID
Dado que existe um post com id = 1
Quando envio GET /posts/1
Então a API deve retornar o post correspondente ao ID.

Cenário: Consultar Post por Id Inválido
Dado que não existe um post com id 9999
Quando envio GET /posts/9999
Então o status deve ser 404

3- Feature de Atualização de Post 

Cenário: Atualizar Post 
Dado que envio um payload completo para atualizar um post existente 
Quando envio PUT /posts/1 
Então devo receber status 200 
E o corpo deve refletir os dados enviados no payload

4- Feature de Edição de Post

Cenário: Edição de Post
Dado que envio apenas o campo title 
Quando envio PATCH /posts/1 
Então devo receber status 200 
E o campo title deve ser atualizado no retorno

5- Feature de Exclusão de Post

Cenário: Excluir Post
Dado que desejo excluir um post 
Quando envio DELETE /posts/1 
Então devo receber status 200 
E o corpo deve estar vazio

6- Feature de criação de comentários de Post

Cenário: Criar comentário de Post
Dado que envio um payload válido para criação 
Quando envio POST /comments 
Então recebo status 201 
E o retorno contém os dados enviados

7- Feature de Comentários de Post

Cenário: Consultar comentários de Post
Dado que a API está disponível 
Quando envio GET /comments 
Então devo receber status 200 
E uma lista com os comentários

Cenário: Consultar comentário por Id 
Dado que existe um post com id 1 
Quando envio GET /posts/1/comments 
Então devo receber status 200 
E somente comentários referentes ao postId 1

8- Feature de Usuário

Cenário: Consultar Usuários
Quando envio GET /users 
Então recebo status 200 
E uma lista de usuários

Cenário: Consulta Usuário por ID
Quando envio GET /users/3 
Então recebo status 200 
E retorno contém username, email, address e company

9- Features de Filtros 

Cenário: Filtrar por userId
Quando envio GET /posts?userId=2 
Então recebo status 200 
E todos os posts têm userId igual a 2

Cenário: Filtrar posts de Usuários 
Quando envio GET /users
Então recebo status 200 
E todos os posts dos usuários

Cenário: Filtrar Post por E-mail
Quando envio GET /comments?email= Eliseo@gardner.biz 
 Então recebo status 200 
E retorno somente comentários com o email especificado

Cenário: Filtrar Post sem comentário por E-mail 
Quando envio GET /comments?email= test@test.com
 Então recebo status 200 
E retorno somente comentários com o email especificado









