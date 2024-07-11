## Contexto e Objetivos

Foi realizada uma mudança no Quickstart, a página inicial foi alterada para ser a página do SSO de cara, não precisando passar um redirectTo na url. Feito o login, sabendo que o usuário consta no banco de dados é armazenado o token, name e userName no localStorage, além de ser redirecionado para a rota de dashboard.

```typescript

const handleLogin = async (e: React.FormEvent) => {

e.preventDefault();

setLoading(true);

setError(null);


try {

const response = await login(userName, password);

if (response && response.token) {

// Armazenar o token, nome e nome de usuário no localStorage

localStorage.setItem('token', response.token);

localStorage.setItem('name', response.customerData.name);

localStorage.setItem('userName', response.customerData.userName);

  

// Redirecionar para o dashboard

window.location.href = '/dashboard';

} else {

setError('Falha no login. Verifique suas credenciais.');

}

} catch (err) {

setError('Falha no login. Verifique suas credenciais.');

} finally {

setLoading(false);

}

};
```




