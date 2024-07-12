### Frontend

**Mudanças Realizadas:**

1. **Estilos Globais:**
    
    - Atualizei os estilos globais para definir a cor de fundo do aplicativo como azul petróleo (`#004d61`).
    - A cor do texto padrão foi definida como branco (`#ffffff`).
2. **Rotas e Componentes:**
    
    - **Novo Componente:** Adicionei um componente `SelectProduct` que após validar o usuário no login, o sistema redireciona para uma tela onde ele pode escolher qual produto deseja acessar.
    - **App Component:** A estrutura de rotas foi mantida com as páginas de login, registro, verificação SSO, seleção de produto e callback.

**Objetivo das Mudanças:**

- Melhorar a aparência visual do aplicativo com um fundo azul petróleo uniforme.
- Manter a estrutura das rotas intacta, garantindo que o novo componente de fundo seja aplicado globalmente.

### Backend

**Mudanças Realizadas:**

1. **Seeders:**
    - **Adição de Logos:** Atualizei o `DatabaseSeeder` para incluir o atributo `logo` para as aplicações. Cada aplicação agora possui uma URL de logo associada.
    - **Empresas e Aplicações:**
        - **Empresa 1:** Criada com SSO, incluindo atributos como `name`, `cnpj`, `sso_name`, `client_id`, `client_secret`, `tenant_id`.
        - **Empresa 2:** Criada sem SSO.
        - **Empresa 3:** Criada com SSO.
        - **Aplicações:** Adicionadas com seus respectivos atributos e URLs de logos, como SGC, ERP, e FAS.

**Objetivo das Mudanças:**

- Assegurar que cada aplicação tenha uma logo visualmente identificável.
- Melhorar a clareza e a organização das seeders, facilitando a gestão de dados iniciais.

## Reflexões

### Frontend

**Desafios:**

- Garantir que a nova cor de fundo não interferisse na legibilidade do texto e na usabilidade geral do aplicativo.

**Soluções:**

- Escolha cuidadosa da cor do texto para manter um bom contraste com o fundo.
- Testes visuais em diferentes tamanhos de tela para assegurar a responsividade e a estética.

### Backend

**Desafios:**

- Garantir que a inclusão do atributo `logo` nas seeders não causasse conflitos ou erros.

**Soluções:**

- Testar a criação das empresas e aplicações no ambiente de desenvolvimento para garantir que todas as associações e atributos estejam corretos.

---

**Próximos Passos:**

- Implementar e testar mais funcionalidades no frontend, como a integração com o backend para validar tokens e redirecionar usuários corretamente.
- Continuar a melhorar a estética e a usabilidade do aplicativo com base no feedback dos usuários.

---