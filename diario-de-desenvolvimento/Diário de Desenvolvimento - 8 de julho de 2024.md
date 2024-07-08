
## Contexto e Objetivos

Implementamos mudanças de design na página de login do Quickstart, incluindo a adição de um vídeo de fundo, o uso de componentes do Material UI para estilização e a implementação de um modal de carregamento para o login SSO. Essas mudanças foram feitas para proporcionar uma experiência de login mais moderna e atrativa para os usuários.

![[Captura de tela de 2024-07-08 13-36-43.png]]

![[Captura de tela de 2024-07-08 13-36-57.png]]
#### 1. Importação de Componentes e Estilos

Importamos componentes essenciais do Material UI, como `Box`, `Typography`, `Paper`, `Modal` e `CircularProgress`, para a construção da interface. Além disso, utilizamos a biblioteca `@emotion/styled` para a estilização dos componentes.

#### 2. Adição de Vídeo de Fundo

Adicionamos um vídeo de fundo otimizado ao lado esquerdo do formulário de login para tornar a página mais dinâmica e visualmente atraente.

#### 3. Estrutura do Componente `Login`

Atualizamos o componente `Login` para incluir um layout dividido com o vídeo de fundo e o formulário de login. Utilizamos o Material UI para estilização e implementamos um modal de carregamento que é exibido durante o redirecionamento para o login SSO.

### Considerações Finais

As mudanças na página de login foram realizadas para proporcionar uma interface mais moderna e dinâmica, incluindo um vídeo de fundo e um modal de carregamento, melhorando assim a experiência do usuário durante o processo de login.


## Problemas enfrentados

### Reload e Logout no Projeto Quick Start

### Problema

Ao recarregar a página, o usuário era redirecionado para o dashboard independentemente da página atual. Além disso, ao clicar em sair, o usuário só era redirecionado para a página de login após atualizar a página.

### Solução

Para resolver esses problemas, foram feitas as seguintes mudanças no projeto:

1. **Verificação de Autenticação e Estado de Carregamento**
2. **Passagem da Função de Logout para o Componente `Header`**
3. **Uso do `useNavigate` para Redirecionamento Imediato no Logout**
#### Verificação de Autenticação e Estado de Carregamento

Adicionamos um estado de carregamento (`isLoading`) e verificamos a autenticação apenas uma vez durante a montagem do componente.

```plaintext 
useEffect(() => { const token = localStorage.getItem('token'); setIsAuthenticated(!!token); setIsLoading(false); }, []); 

globalStyles();

const toggleDrawer = () => { setDrawerOpen(!drawerOpen); };

const handleLogout = () => {
localStorage.removeItem('token'); setIsAuthenticated(false); }; if (isLoading){ 
return <div>Loading...</div>;  }

em app.tsx
```

#### 2. Passagem da Função de Logout para o Componente `Header`

Passamos a função `handleLogout` como prop para o componente `Header`.

#### 3. Uso do `useNavigate` para Redirecionamento Imediato no Logout

No componente `Header`, usamos o hook `useNavigate` do React Router para redirecionar o usuário após o logout.

```plaintext
interface HeaderProps { pageTitle: string; toggleDrawer: () => void; onLogout: () => void; }

...

const handleLogout = () => { onLogout(); navigate('/'); };

/components/Header
```

### Conclusão

Com essas mudanças, o estado de autenticação é verificado corretamente durante a montagem do componente e, ao clicar no botão "Sair", o usuário é redirecionado imediatamente para a página de login, garantindo uma melhor experiência de uso.