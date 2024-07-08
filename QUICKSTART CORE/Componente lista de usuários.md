### Estrutura dos Componentes

1. **ListUsers**
    - Componente principal que gerencia a lista de usuários.
    - Responsável por buscar os dados, aplicar filtros e gerenciar o estado de edição.
2. **UserTable**
    - Componente que exibe a tabela de usuários.
    - Recebe dados e funções de `ListUsers`.
3. **UserRow**
    - Componente que representa uma linha na tabela de usuários.
    - Exibe informações de um único usuário e inclui o menu para ações (editar).

### Fluxo de Funcionalidade

1. **Buscar Dados dos Usuários**
    
    - `ListUsers` usa o hook `useEffect` para buscar os dados dos usuários da API quando o componente é montado.
    - Os dados são armazenados nos estados `users` e `filteredUsers`.
2. **Filtragem e Ordenação**
    
    - `ListUsers` possui lógica para filtrar e ordenar os usuários com base no termo de busca (`searchTerm`) e no critério de ordenação (`sortBy`).
    - A filtragem e ordenação são aplicadas usando um `useEffect` que depende desses estados.
3. **Edição de Usuários**
    
    - Ao clicar no menu de opções de um usuário (`UserRow`), a função `handleEditClick` é chamada e define o estado `editUser`.
    - Um modal de edição é exibido permitindo a edição dos campos do usuário.
    - Ao salvar, `handleEditSave` chama a API para atualizar os dados e atualiza o estado `users`.
### Passos para Implementar uma Nova Funcionalidade na Listagem de usuários

1. **Defina a Nova Funcionalidade**
    
    - Especifique claramente o que a nova funcionalidade deve fazer.
2. **Adicione Estados Necessários em `ListUsers`**
    
    - Adicione qualquer novo estado necessário para gerenciar a funcionalidade.
3. **Crie/Modifique Componentes Necessários**
    
    - Se necessário, crie novos componentes ou modifique componentes existentes.
    - Exemplo: Adicionar um novo modal para uma nova ação.
4. **Integre a Lógica no Componente Principal (`ListUsers`)**
    
    - Adicione a lógica para gerenciar a nova funcionalidade em `ListUsers`.
    - Garanta que os componentes filhos recebam as props necessárias.
5. **Atualize a Interface do Usuário**
    
    - Modifique os componentes de interface para refletir a nova funcionalidade.
    - Exemplo: Adicionar novos botões ou opções de menu.
6. **Teste a Funcionalidade**
    
    - Garanta que a nova funcionalidade funciona conforme esperado.
    - Teste casos de uso e fluxos possíveis para garantir estabilidade.


## Cypress Test: Gerenciamento de Usuários

### Descrição

Este conjunto de testes verifica o fluxo de gerenciamento de usuários, incluindo a criação e edição de usuários no sistema.

### Configurações

1. **Dependências necessárias**:
    
    - Cypress
    - Cypress-Testing-Library
2. **Comandos customizados**:
    
    - `cy.login(userName, password, redirectTo)`: Realiza o login no sistema com as credenciais fornecidas e redireciona para a URL especificada.

### Descrição dos Testes

#### Teste 1: Criar um novo usuário

- **Passos**:
    1. Navegar para o dashboard.
    2. Clicar no ícone de menu para abrir o drawer.
    3. Expandir o menu de usuário.
    4. Selecionar a opção "Gerenciar usuário".
    5. Preencher o formulário de criação de usuário.
    6. Submeter o formulário.
- **Verificações**:
    - Verificar se a URL contém `/gerenciar-usuario`.
    - Verificar se a mensagem "Usuário criado com sucesso!" é exibida.

#### Teste 2: Editar um usuário existente

- **Passos**:
    1. Navegar para o dashboard.
    2. Clicar no ícone de menu para abrir o drawer.
    3. Expandir o menu de usuário.
    4. Selecionar a opção "Listar usuários".
    5. Filtrar pelo usuário criado.
    6. Editar as informações do usuário.
    7. Salvar as alterações.
- **Verificações**:
    - Verificar se a URL contém `/listar-usuarios`.
    - Verificar se a mensagem "Usuário atualizado com sucesso!" é exibida.

### Notas Adicionais

- As IDs e os seletors usados devem corresponder aos elementos presentes no DOM da aplicação.
- As credenciais de login e os valores dos formulários podem ser ajustados conforme necessário para o ambiente de teste específico.