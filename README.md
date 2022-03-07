# FLASK API

**deployed on:** https://pyrestapiflaskapp.herokuapp.com


Sobre a API e projeto

Projeto iniciou-se derivado de um curso onde foi desenvolvido uma Rest API em Flask, a API foi inspirada em como se comporta o site Trivago, onde o site da Trivago procura hotéis em outros sites e fazem a comparação entre eles. A API conta com a criação de usuários para que possam “cadastrar” sites, hotéis e seus atributos, podendo criar, ler, atualizar, e deletar, fazendo assim um CRUD completo. Além da API no projeto também é mostrado como consumir esses dados e filtrá-los totalmente utilizando o Python. No modelo relacional abaixo podemos ter uma melhor visualização de como se comporta a API, usuários possuem um sistema de login e também de ativação, para a parte de login foi utilizado JWT,já a ativação simula um envio de e-mail para a ativação do usuário para que possam realizar operações de GET,POST,PUT, DELETE  nos sites e hoteis.

![image](https://user-images.githubusercontent.com/97971018/157048123-e51337d5-be1e-4323-88ea-8fa7505e22da.png)


# ENDPOINTS

 **Endpoints relacionados aos usuários**

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


