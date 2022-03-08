
**deployed on:** https://pyrestapiflaskapp.herokuapp.com


# Sobre a API e projeto

Projeto iniciou-se derivado de um curso onde foi desenvolvido uma Rest API em Flask, a API foi inspirada em como se comporta o site Trivago, onde o site da Trivago procura hotéis em outros sites e fazem a comparação entre eles. A API conta com a criação de usuários para que possam “cadastrar” sites, hotéis e seus atributos, podendo criar, ler, atualizar, e deletar, fazendo assim um CRUD completo. Além da API no projeto também é mostrado como consumir esses dados e filtrá-los totalmente utilizando o Python. No modelo relacional abaixo podemos ter uma melhor visualização de como se comporta a API, usuários possuem um sistema de login e também de ativação, para a parte de login foi utilizado JWT,já a ativação simula um envio de e-mail para a ativação do usuário para que possam realizar operações de GET,POST,PUT, DELETE  nos sites e hoteis.

![image](https://user-images.githubusercontent.com/97971018/157048123-e51337d5-be1e-4323-88ea-8fa7505e22da.png)


# ENDPOINTS

## Endpoints relacionados aos usuários

## Criação de usuário:
Method | URL 
:-------:|:----:
POST | /cadastro

<table>
  <tr>
    <td colspan="2"> Header </td>
  </tr>
  <tr>
    <td> Content-Type  </td>
    <td> application/json  </td>
  </tr>
</table>

<table>
  <tr>
    <td> Request Body </td>
  </tr>
  <tr>
    <td> {"login": "exemplo","senha": "exemplo"} </td>
  </tr>
</table>

<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 201 Created </td>
    <td> {"message": "User created successfully!"}</td>
  </tr>
</table>

**Se o usuário já existir a resposta é:**

<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 400 Bad Request </td>
    <td> {"message": "The login 'exemplo' already exists."}</td>
  </tr>
</table>

## Pesquisa de usuário

<table>
  <tr>
    <td> Method </td>
    <td> URL </td>
  </tr>
  <tr>
    <td> GET </td>
    <td> /usuarios/{user_id} </td>
  </tr>
</table>

<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 200 Ok </td>
    <td> {"user_id": 2,"login": "exemplo","ativado": false}</td>
  </tr>
</table>

**Se não encontrar o usuário a resposta é:**
<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 404 Not Found </td>
    <td> {"message": "User not found."}</td>
  </tr>
</table>

## Confirmação de usuário

Como mencionado anteriormente, a aplicação possui um sistema de confirmação de usuário, que simula uma confirmação de usuário via e-mail.

<table>
  <tr>
    <td> Method </td>
    <td> URL </td>
  </tr>
  <tr>
    <td> GET </td>
    <td> /confirmacao/{user_id} </td>
  </tr>
</table>

<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 200 Ok </td>
    <td> {"message": "User id '2' confirmed successfully."}</td>
  </tr>
</table>

Se dermos um novo GET no /usuario{user_id} podemos ver a informação "ativado" como verdadeira.

<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 200 Ok </td>
    <td> {"user_id": 2,"login": "exemplo",<b>"ativado": true}</b></td>
  </tr>
</table>

**Se não encontrar o usuário a resposta é:**
<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 404 Not Found </td>
    <td> {"User id '5' not found."}</td>
  </tr>
</table>

## Login dos usuários

Para realizar certas ações na API o usuário precisa estar logado, foi implementado um sistema de token com jwt.


<table>
  <tr>
    <td> Method </td>
    <td> URL </td>
  </tr>
  <tr>
    <td> POST </td>
    <td> /login </td>
  </tr>
</table>

<table>
  <tr>
    <td colspan="2"> Header </td>
  </tr>
  <tr>
    <td> Content-Type  </td>
    <td> application/json  </td>
  </tr>
</table>

<table>
  <tr>
    <td> Request Body </td>
  </tr>
  <tr>
    <td> {"login": "exemplo","senha": "exemplo"} </td>
  </tr>
</table>

<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 200 Ok </td>
    <td> {"access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTY0NjY2NTA0MCwianRpIjoiN2IzYmM0OTMtYWIxOS00MmFlLTlkMjctNTUyMjY3YjdmZTY5IiwidHlwZSI6ImFjY2VzcyIsInN1YiI6MSwibmJmIjoxNjQ2NjY1MDQwLCJleHAiOjE2NDY2NjU5NDB9.2yJJBVt9DZRje0wWZXg-SomBDihEVK9Qh7fHUWx-mds"}</b></td>
  </tr>
</table>

**Se não encontrar o usuário ou dados estiverem incorretos a resposta é:**
<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 404 Not Found </td>
    <td> {"message": "The username or password is incorrect."}</td>
  </tr>
</table>


## Logout dos usuários

<table>
  <tr>
    <td> Method </td>
    <td> URL </td>
  </tr>
  <tr>
    <td> POST </td>
    <td> /logout </td>
  </tr>
</table>

<table>
  <tr>
    <td colspan="2"> Header </td>
  </tr>
  <tr>
    <td> Authorization </td>
    <td> Bearer {token_de_acesso} </td>   
  </tr>
</table>
<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 200 Ok </td>
    <td>{"message": "Logged out successfully!"}</td>
  </tr>
</table>

 ## Endpoints relacionados aos sites
 
 ## Criando site
 
 <table>
  <tr>
    <td> Method </td>
    <td> URL</td>
  </tr>
  <tr>
    <td> POST </td>
    <td>/sites{url} <b> exemplo /sites/www.exemplo.com</b></td> 
  </tr>
</table>

<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 200 Ok </td>
    <td>
{
    "site_id": 1,
    "url": "www.exemplo.com",
    "hoteis": [ ]
}
    </td>
  </tr>
</table>

**Se o site já existir:**

<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 400 Bad request </td>
    <td>{"message": "The site already exists."}</td>
  </tr>
</table>

## Pesquisando sites

<table>
  <tr>
    <td> Method </td>
    <td> URL </td>
  </tr>
  <tr>
    <td> GET </td>
    <td> /sites </td>
  </tr>
</table>

<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 200 Ok </td>
    <td>{"sites": [{"site_id": 1,"url": "www.exemplo.com","hoteis": [ ]}, {"site_id": 2, "url": "www.exemplo2.com","hoteis": [ ]},]}</td>
  </tr>
</table>

**Também é possível realizar a pesquisa de um site especifico:**
<table>
  <tr>
    <td> Method </td>
    <td> URL </td>
  </tr>
  <tr>
    <td> GET </td>
    <td> /site/{url} <b>exemplo /site/www.exemplo.com</b> </td>
  </tr>
</table>

<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 200 Ok </td>
    <td>{"sites": [{"site_id": 1,"url": "www.exemplo.com","hoteis": [ ]}]}</td>
  </tr>
</table>

## Deletando sites

<table>
  <tr>
    <td> Method </td>
    <td> URL </td>
  </tr>
  <tr>
    <td> DELETE </td>
    <td> /sites/{url} <b>/site/www.exemplo.com</b> </td>
  </tr>
</table>

<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 200 Ok </td>
    <td>{"message": "Site deleted."}</td>
  </tr>
</table>

**Se não encontrar o site:**

<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 404 Not Found </td>
    <td>{"message": "Site not found."}</td>
  </tr>
</table>

## Endpoints relacionados aos hotéis
## Criação de hotéis:
<table>
  <tr>
    <td> Method </td>
    <td> URL </td>
  </tr>
  <tr>
    <td> POST </td>
    <td> /hoteis/{hotel_id}</b> </td>
  </tr>
</table>

<table>
  <tr>
    <td colspan="2"> Header </td>
  </tr>
  <tr>
    <td> Content-Type  </td>
    <td> application/json  </td>
  </tr>
  <tr>
    <td> Authorization  </td>
    <td> Bearer {token_de_acesso}  </td>
  </tr>
</table>
<table>
  <tr>
    <td> Request Body </td>
  </tr>
  <tr>
    <td> {"hotel_id": "exemplo","nome": "Exemplo Hotel","estrelas": 4.0,"diaria": 600.0,"cidade": "Araras","site_id": 2}</td>
  </tr>
</table>
<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 201 Created </td>
    <td>{"hotel_id": "exemplo","nome": "Exemplo Hotel","estrelas": 4.0,"diaria": 600.0,"cidade": "Araras","site_id": 2}</td>
  </tr>
</table>

**Se o hotel existir:**

<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 400 Bad Requests </td>
    <td>{"message": "Hotel id 'exemplo2' already exists."}</td>
  </tr>
</table>

## Atualizar hotéis:

<table>
  <tr>
    <td> Method </td>
    <td> URL </td>
  </tr>
  <tr>
    <td> PUT </td>
    <td> /hoteis/{hotel_id}</b> </td>
  </tr>
</table>
<table>
  <tr>
    <td colspan="2"> Header </td>
  </tr>
  <tr>
    <td> Content-Type  </td>
    <td> application/json  </td>
  </tr>
  <tr>
    <td> Authorization  </td>
    <td> Bearer {token_de_acesso}  </td>
  </tr>
</table>

**Neste exemplo trocamos o nome do hotel de "Exemplo Hotel" para "Exemplo Hotel Alterado"**
<table>
  <tr>
    <td> Request Body </td>
  </tr>
  <tr>
    <td> {"nome": "Exemplo Hotel <b>Alterado</b>","estrelas": 4.0,"diaria": 600.0,"cidade": "Araras","site_id": 2}</td>
  </tr>
</table>

**Se o hotel_id existir vamos atualizar os dados**

<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 200 Ok </td>
    <td>{"hotel_id": "exemplo","nome": "Exemplo Hotel <b>Alterado</b>","estrelas": 4.0,"diaria": 600.0,"cidade": "Araras","site_id": 2}</td>
  </tr>
</table>

**Se o hotel_id não existir é criado um novo hotel**
<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 201 Created </td>
    <td>{"hotel_id": "exemplo5","nome": "Exemplo Hotel <b>Alterado</b>","estrelas": 4.0,"diaria": 600.0,"cidade": "Araras","site_id": 2}</td>
  </tr>
</table>

**Sem código de autenticação ou código de autenticação expirado**

<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 500 Internal Server Error </td>
    <td>{"message": "Internal Server Error"}</td>
  </tr>
</table>

## Deletar Hotéis:
<table>
  <tr>
    <td> Method </td>
    <td> URL </td>
  </tr>
  <tr>
    <td> DELETE </td>
    <td> /hoteis/{hotel_id}  exemplo /hoteis/exemplo</b> </td>
  </tr>
</table>
<table>
  <tr>
    <td colspan="2"> Header </td>
  </tr>
  <tr>
    <td> Authorization  </td>
    <td> Bearer {token_de_acesso}  </td>
  </tr>
</table>
<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 200 Ok </td>
    <td>{"message": "Hotel deleted."}</td>
  </tr>
</table>

**Se o hotel_id não existir**
<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 404 Not Found </td>
    <td>{"message": "Hotel not found."}</td>
  </tr>
</table>

**Sem código de autenticação ou código de autenticação expirado**

<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 500 Internal Server Error </td>
    <td>{"message": "Internal Server Error"}</td>
  </tr>
</table>

## Pesquisar Hotéis:
**Pesquisa geral, retorna todos os hoteis**
<table>
  <tr>
    <td> Method </td>
    <td> URL </td>
  </tr>
  <tr>
    <td> GET </td>
    <td> /hoteis</td>
  </tr>
</table>
<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 200 OK </td>
    <td>{"hoteis": [{"hotel_id": "exemplo","nome": "Exemplo Hotel","estrelas": 4.0,"diaria": 600.0,"cidade": "Araras","site_id": 2},
        {"hotel_id": "exemplo2","nome": "Exemplo Hotel 2","estrelas": 4.2,"diaria": 467.0,"cidade": "São Paulo","site_id": 2},<br>
        {"hotel_id": "exemplo3","nome": "Exemplo Hotel 3","estrelas": 4.3,"diaria": 732.0,"cidade": "Rio de Janeiro","site_id": 2}]}</td>
  </tr>
</table>

**Pesquisa específica, retorna hotel específico**

<table>
  <tr>
    <td> Method </td>
    <td> URL </td>
  </tr>
  <tr>
    <td> GET </td>
    <td> /hoteis/{hotel_id} exemplo <b>/hoteis/exemplo</b></td>
  </tr>
</table>
<table>
  <tr>
    <td> Status </td>
    <td> Response Body </td>
  </tr>
  <tr>
    <td> 200 OK </td>
    <td>{"hotel_id": "exemplo","nome": "Exemplo Hotel","estrelas": 4.0,"diaria": 600.0,"cidade": "Araras","site_id": 2}</td>
  </tr>
</table>

## Pesquisa de Hotéis Avançada:

**Parâmetros para consulta**
* cidade - Filtrar hotéis pela cidade escolhida. Padrão: Nulo 
* estrelas_min - Avaliações mínimas de hotéis de 0 a 5. Padrão: 0
* estrelas_max - Avaliações máximas de hotéis de 0 a 5. Padrão: 5
* diaria_min - Valor mínimo da diária do hotel de R$ 0 a R$ 10.000,00. Padrão: 0
* diaria_max - Valor máximo da diária do hotel de R$ 0 a R$ 10.000,00. Padrão: 10000
* limit - Quantidade máxima de elementos exibidos por página. Padrão: 50
* offset - Quantidade de elementos pular (geralmente múltiplo de limit). Padrão: 0

[![flask_api](https://yt-embed.herokuapp.com/embed?v=lofoP4OR1vo)](https://www.youtube.com/watch?v=lofoP4OR1vo "flask_api")


<hr>

Estou aberto a feedbacks comentários e críticas quaisquer dúvidas entrem em contato comigo <a href="mailto:matheusvicentesj5@hotmail.com">Matheus Vicente</a>
