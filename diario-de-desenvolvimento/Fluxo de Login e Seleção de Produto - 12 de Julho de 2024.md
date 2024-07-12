

**Login**

- Quando o usuário faz login em `/auth/login`, o sistema retorna a seguinte estrutura:

```json
{

"message": "Login realizado com sucesso",

"token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbG9jYWxob3N0Ojg5ODkvYXBpL2F1dGgvbG9naW4iLCJpYXQiOjE3MjA3ODkyOTksImV4cCI6MTcyMDc5Mjg5OSwibmJmIjoxNzIwNzg5Mjk5LCJqdGkiOiI4Z2ZBcGxSNzRLVXo1Nlh3Iiwic3ViIjoiNCIsInBydiI6IjIzYmQ1Yzg5NDlmNjAwYWRiMzllNzAxYzQwMDg3MmRiN2E1OTc2ZjciLCJuYW1lIjoiV2VzbGV5IE9saXZlaXJhIiwidXNlck5hbWUiOiJ3ZXNsZXlAcnl6emFuc2FsbWFub2ZtY29tLm9ubWljcm9zb2Z0LmNvbSIsImVtcHJlc2EiOiJDb3JwdXMgTFREQSIsInBlcm1pc3Npb25zIjpbeyJhcHBsaWNhdGlvbiI6eyJuYW1lIjoiRVJQIiwiZGVzY3JpcHRpb24iOiJFbnRlcnByaXNlIFJlc291cmNlIFBsYW5uaW5nIiwiZGV2ZWxvcFVybCI6Imh0dHA6Ly9sb2NhbGhvc3Q6NTE3MyIsImhvbW9sb2dVcmwiOiJodHRwOi8vbG9jYWxob3N0OjUxNzMiLCJwcm9kdWN0aW9uVXJsIjoiaHR0cDovL2xvY2FsaG9zdDo1MTczIn0sIm1vZHVsZXMiOlt7Im5hbWUiOiJHZXJlbmNpYXIgUHJvZHV0b3MiLCJnZXQiOnRydWUsInBvc3QiOnRydWUsInB1dCI6dHJ1ZSwiZGVsZXRlIjpmYWxzZX1dfV19.Nbg13BM_tGCLKoD1Ybd02GKJuwOjO6Hb_BqMZylXo1c",

"customerData": {

"name": "Wesley Oliveira",

"userName": "wesley@ryzzansalmanofmcom.onmicrosoft.com",

"empresa": "Corpus LTDA",

"permissions": [

{

"application": {

"name": "ERP",

"description": "Enterprise Resource Planning",

"developUrl": "http://localhost:5173",

"homologUrl": "http://localhost:5173",

"productionUrl": "http://localhost:5173"

},

"modules": [

{

"name": "Gerenciar Produtos",

"get": true,

"post": true,

"put": true,

"delete": false

}

]

}

]

}

}
```

**Seleção de Produto**

- Após validar o usuário no login, o sistema redireciona para uma tela onde ele pode escolher qual produto deseja acessar.
- Os produtos disponíveis são listados com base nas permissões do usuário, detalhadas no retorno do login.
- Cada aplicação possui as seguintes informações:
    - **Nome:** `name`
    - **Descrição:** `description`
    - **URLs:**
        - Desenvolvimento: `developUrl`
        - Homologação: `homologUrl`
        - Produção: `productionUrl`
    - **Módulos:**
        - Nome do módulo: `name`
        - Permissões:
            - `get`
            - `post`
            - `put`
            - `delete`

**Redirecionamento para o Produto**

- Ao selecionar um produto, o sistema redireciona o usuário para a URL de produção correspondente com o token de autenticação.
- O redirecionamento é feito carregando a URL `/callback` com o token na query string.
- Exemplo de redirecionamento:

```typescript 
window.location.href = `${selectedProduct.productionUrl}/callback?token=${token}`;
```

### Resumo do Processo

1. Usuário faz login em `/auth/login`.
2. Sistema retorna mensagem de sucesso com token e dados do usuário.
3. Usuário é redirecionado para a tela de seleção de produto.
4. Usuário seleciona um produto.
5. Sistema redireciona para a URL do produto selecionado com o token de autenticação.