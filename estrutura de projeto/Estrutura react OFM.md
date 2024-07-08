Este documento descreve como organizar a estrutura do projeto React utilizando Vite. Siga estas diretrizes para garantir uma organização consistente e facilitar a manutenção do código.

### Estrutura do Diretório

A estrutura de diretórios do projeto deve seguir o modelo abaixo:

project-root/
├── dist/
├── node_modules/
├── public/
├── src/
│   ├── assets/
│   ├── components/
│   ├── hooks/
│   ├── pages/
│   ├── services/
│   ├── App.tsx
│   ├── main.tsx
├── cypress/
│   ├── fixtures/
│   ├── integration/
│   ├── plugins/
│   ├── support/
├── .gitignore
├── cypress.json
├── index.html
├── package.json
├── README.md
├── tsconfig.json
├── vite.config.ts



#### 📁 `dist/`

- **Descrição**: Diretório gerado automaticamente pelo Vite ao realizar o build da aplicação.
- **Conteúdo**: Arquivos otimizados para produção. Não modificar manualmente.

#### 📁 `node_modules/`

- **Descrição**: Diretório onde ficam as dependências do projeto instaladas pelo npm.
- **Conteúdo**: Arquivos de pacotes de terceiros. Não modificar manualmente.

#### 📁 `public/`

- **Descrição**: Arquivos estáticos públicos que não passam pelo processo de build.
- **Conteúdo**:
    - **Imagens, fontes e outros recursos estáticos**: Esses arquivos são acessíveis diretamente via URL.
    - **index.html**: Arquivo HTML principal, referência para a aplicação.

#### 📁 `src/`

- **Descrição**: Diretório principal do código-fonte da aplicação.
- **Subdiretórios e Arquivos**:
    - **📁 `assets/`**: Arquivos estáticos utilizados no código-fonte, como imagens e fontes que são importadas diretamente em componentes.
    - **📁 `components/`**: Componentes React reutilizáveis na aplicação.
        - **Componentes de UI**: Botões, modais, inputs, etc.
        - **Componentes funcionais**: Componentes específicos que encapsulam uma funcionalidade específica e são reutilizáveis.
    - **📁 `hooks/`**: Custom hooks utilizados na aplicação.
        - **Hooks de estado**: Custom hooks para gerenciamento de estado complexo.
        - **Hooks de efeitos colaterais**: Hooks que encapsulam lógica de efeitos colaterais, como chamadas de API.
    - **📁 `pages/`**: Componentes de página que representam rotas da aplicação.
        - **Páginas principais**: Componentes que representam cada rota principal da aplicação (e.g., Login, Dashboard, Profile).
        - **Sub-páginas**: Componentes que representam sub-rotas ou seções de uma página principal.
    - **📁 `services/`**: Módulos para comunicação com APIs e lógica de negócios.
        - **Serviços de API**: Módulos que encapsulam chamadas a APIs externas.
        - **Serviços de utilidade**: Funções utilitárias que podem ser compartilhadas entre diferentes partes da aplicação.
    - **📄 `App.tsx`**: Componente raiz da aplicação que configura rotas e provedores de contexto.
    - **📄 `main.tsx`**: Ponto de entrada da aplicação que renderiza o componente raiz.

#### 📁 `cypress/`

- **Descrição**: Diretório de testes end-to-end utilizando o Cypress.
- **Subdiretórios e Arquivos**:
    - **📁 `fixtures/`**: Arquivos de dados estáticos utilizados nos testes.
    - **📁 `integration/`**: Arquivos de testes que verificam a integração entre diferentes partes da aplicação.
    - **📁 `plugins/`**: Plugins do Cypress para estender sua funcionalidade.
    - **📁 `support/`**: Arquivos de configuração e comandos customizados para suporte aos testes.

### Arquivos de Configuração

- **📄 `.gitignore`**: Define quais arquivos e diretórios devem ser ignorados pelo Git.
- **📄 `cypress.json`**: Configurações do Cypress.
- **📄 `index.html`**: Arquivo HTML principal que serve como template para a aplicação.
- **📄 `package.json`**: Lista as dependências do projeto e scripts de execução.
- **📄 `README.md`**: Documentação principal do projeto, incluindo informações de configuração e execução.
- **📄 `tsconfig.json`**: Configurações do compilador TypeScript.
- **📄 `vite.config.ts`**: Configurações do bundler Vite.

### Convenções e Boas Práticas

1. **Nomenclatura Consistente**:
    
    - Utilize nomes descritivos e consistentes para arquivos e pastas.
    - Use `PascalCase` para nomes de componentes e `camelCase` para nomes de variáveis e funções.
2. **Componentização**:
    
    - Quebre componentes grandes em componentes menores e reutilizáveis.
    - Mantenha a lógica de apresentação separada da lógica de negócios.
3. **Organização de Código**:
    
    - Centralize a lógica de negócios em `services`.
    - Utilize `hooks` para encapsular e reutilizar lógica de estado e efeitos colaterais.
4. **Documentação**:
    
    - Documente componentes e funções com comentários claros.
    - Atualize a documentação conforme mudanças no código.
5. **Testes End-to-End com Cypress**:
    
    - Organize testes em `integration` para cobrir diferentes fluxos de usuário.
    - Utilize `fixtures` para dados estáticos que simulam respostas de API.
    - Personalize comandos em `support` para reutilização em múltiplos testes.